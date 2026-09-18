# Os Quatro Pilares do POO

> [!info] Metadados
> **Disciplina:** Desenvolvimento de Sistemas
> **Bloco:** 4.1 — Desenvolvimento de Sistemas (FASE 4 — Núcleo de Desenvolvimento)
> **Tópico:** 2. Paradigma Orientado a Objetos — Os Quatro Pilares do POO
> **Subtópicos:** Conceitos (abstração, encapsulamento, herança, polimorfismo) · Classe abstrata (molde incompleto, método abstrato) · Interface (contrato, implements, default method) · Visibilidade dos membros (private, default, protected, public)
> **Pré-requisitos:** [[Classe-e-Objeto]] (classe, objeto, atributos, métodos) e [[Java-Fundamentos-da-Linguagem|Java — Fundamentos da Linguagem]] (sintaxe da classe, `new`, métodos)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-09-17

---

## 1. Por que estudar os pilares?

Se a [[Classe-e-Objeto|classe e o objeto]] são o molde e a peça, os **quatro pilares** são o **motor do design** — as regras que orientam como esses moldes se relacionam, se protegem, se especializam e se comportam. Sem eles, você escreve código que "funciona"; com eles, você escreve código que **escala, mantém e evolui**.

Em um sistema de benefícios da DATAPREV, cada pilar aparece em uma situação concreta:

- **Abstração:** do beneficiário, o sistema precisa de `cpf` e `rendaMensal`, mas não da cor dos olhos. Modelar só o relevante.
- **Encapsulamento:** o CPF deve ser validado antes de ser aceito — ninguém deveria atribuir um CPF direto no atributo, sem verificação.
- **Herança:** `Servidor`, `Pensionista` e `Beneficiario` compartilham dados comuns (nome, CPF) mas têm regras distintas.
- **Polimorfismo:** um pagamento pode ser Pix ou cartão — o método `processar` não precisa saber qual é; cada tipo calcula o valor do seu jeito.

---

## 2. Abstração — modelar só o que importa

**Abstração** é a capacidade de **modelar apenas os aspectos relevantes** de uma entidade, **ignorando os detalhes que não interessam** ao sistema. Abstrair é **selecionar o que importa** para o domínio — do beneficiário, interessa a `rendaMensal` e o `cpf`, não a cor do cabelo.

> [!warning] PEGADINHA — abstração (pilar) ≠ classe abstrata (mecanismo)
> A classe abstrata (seção 5) é apenas **uma das ferramentas** da abstração, não o pilar em si.

Veja a diferença na prática:

```java
// ABSTRAÇÃO RUIM — atributos demais, irrelevantes para o domínio
public class Beneficiario {
    private String nome;
    private String cpf;
    private double rendaMensal;
    private String corDoCabelo;      // irrelevante para benefícios
    private int idadeDoGato;         // irrelevante para benefícios
    // ...
}

// ABSTRAÇÃO BOA — apenas o que o sistema precisa
public class Beneficiario {
    private String nome;
    private String cpf;
    private double rendaMensal;
}
```

> [!warning] PEGADINHA — abstração vs. encapsulamento
> A FGV costuma misturar os termos. **Abstração** é *simplificar*: modelar só o essencial. **Encapsulamento** é *proteger*: esconder o estado interno, expondo apenas uma interface controlada. Abstração decide *o que* o objeto representa; encapsulamento decide *como* isso fica protegido. Dizer que abstração é "esconder dados do usuário" está **misturando os conceitos**.

---

## 3. Encapsulamento — proteger o estado interno

**Encapsulamento** é o princípio de **proteger os dados internos** do objeto, permitindo acesso e modificação apenas por **métodos controlados** — não por acesso direto aos atributos. Na prática, os atributos ficam **privados** (`private`) e o acesso passa por **getters/setters** (ou por métodos que representam regras de negócio).

**Getter** é o método de **leitura**; **setter**, o de **escrita** (frequentemente validando antes). Juntos implementam o encapsulamento: o mundo externo não toca o atributo `private` — passa pelos métodos controlados. Getter/setter **não são palavras-chave da linguagem**; são **convenção de nomenclatura** (`get<Atributo>()`, `set<Atributo>(valor)`, `is<Atributo>()` para booleanos) — distinção que a FGV pode cobrar.

Veja o problema e a correção:

```java
// Campo público: acesso direto, sem validação
public class Beneficiario {
    public String cpf;   // público — nada impede o acesso direto
}

// Em algum ponto do sistema:
beneficiario.cpf = "123";   // sem validação — a regra não existe aqui
```

O problema: a regra de validação **não está em lugar nenhum** — os bugs de consistência se espalham. A correção **centraliza** a regra: `private` impede o acesso direto e `setCpf()` concentra a validação em um único ponto.

```java
public class Beneficiario {
    private String cpf;            // atributo privado — ninguém acessa de fora

    public String getCpf() {       // getter: leitura controlada
        return cpf;
    }

    public void setCpf(String cpf) {
        // setter: escrita com validação (regra de negócio)
        if (cpf == null || cpf.length() != 11) {
            throw new IllegalArgumentException("CPF inválido");
        }
        this.cpf = cpf;
    }
}
```

O valor didático vai além de "esconder": o encapsulamento **centraliza a validação e a regra de negócio** e **adiciona comportamento** à atribuição — não é só barreira, é **lógica de negócio embutida**.

> [!question] Por que não deixar os atributos públicos?
> Se 10 pontos do sistema atribuírem CPF com validações diferentes, mudar a regra exige caçar os 10. Com encapsulamento, muda-se **um único método** `setCpf` — **manutenibilidade** em forma de código.

O `private` é o mecanismo que **implementa** o encapsulamento em Java. A seção 9 mostra os quatro modificadores de acesso (`private`, padrão, `protected`, `public`).

---

## 4. Herança — herdar e especializar

**Herança** é a relação em que uma classe (**subclasse**/filha) **herda atributos e métodos** de outra (**superclasse**/pai), podendo **adicionar** novos e **sobrescrever** (especializar) os herdados. É a materialização da relação "é-um".

Veja o problema e a correção:

```java
// Sem herança: cada classe repete nome e cpf, sem relação entre elas
public class Servidor {
    private String nome;
    private String cpf;
    // ...
}

public class Pensionista {
    private String nome;
    private String cpf;
    // ...
}
```

O problema: `nome` e `cpf` são **copiados** em cada classe — mudar a superclasse exige alterar todas; nada expressa que são variações da mesma coisa. A correção **extrai o comum** para a superclasse `Pessoa` via `extends`; cada subclasse só declara o próprio.

```java
public class Pessoa {
    protected String nome;
    protected String cpf;

    public void setNome(String nome) { this.nome = nome; }
    public String getNome() { return nome; }
}

// Beneficiario "é um(a)" Pessoa — herda nome e cpf
public class Beneficiario extends Pessoa {
    private double rendaMensal;          // atributo próprio

    public double getRendaMensal() { return rendaMensal; }
}
```

`Beneficiario` não redeclara `nome` e `cpf` — herda via `extends`; `protected` permite à subclasse acessar diretamente os atributos herdados.

A herança promove **reutilização** e **especialização**, mas cria **ligação forte** entre pai e filho — mudar a superclasse afeta todas as subclasses.

> [!note] Detalhes que completam a herança
> Classe declarada **`final` não pode ser estendida** (mesmo raciocínio dos métodos `final` da seção 6.3). E toda classe herda de **`Object`**, a raiz das hierarquias do Java: `equals`, `hashCode`, `toString` vêm de lá.

> [!warning] PEGADINHA — upcast e downcast
> Referência do tipo **pai** aponta para objeto **filho** (upcast — seguro e implícito). O inverso (downcast) exige **`instanceof`** antes; sem ele, **`ClassCastException`** em execução.

> [!warning] PEGADINHA — herança vs. composição
> *"Deve-se preferir herança ou composição?"* A resposta favorita da banca moderna é **composição** ("prefira composição a herança" — princípio de Clean Code). Composição é "tem-um" (um `Carro` *tem* um `Motor`); herança é "é-um" (um `Carro` *é* um `Veículo`). Herança cria **acoplamento forte** — mudar o pai afeta os filhos — e hierarquias rígidas; composição é mais flexível. Na prova: **composição antes de herança**, exceto quando a "é-um" for genuína e estável.

---

## 5. Classe abstrata: a herança que obriga a implementar

A classe abstrata é o **molde incompleto**: define estrutura e comportamento comuns para um grupo de subclasses, mas **não pode ser instanciada**. Os **métodos abstratos** são métodos **sem corpo** — apenas a assinatura; a subclasse concreta, via `extends`, é **obrigada a implementá-los** — se não implementar, também será abstrata.

Veja um exemplo no domínio previdenciário — o número do benefício é consultado do mesmo jeito, mas o cálculo depende do tipo:

```java
// Classe abstrata: o molde incompleto
public abstract class Beneficio {
    private String numeroBeneficio;

    // método concreto: tem corpo e é compartilhado pela herança
    public String getNumeroBeneficio() {
        return numeroBeneficio;
    }

    // método abstrato: sem corpo — a subclasse concreta é obrigada a implementar
    public abstract double calcularValor();
}

// Subclasse concreta: completa o molde
public class BeneficioAposentadoria extends Beneficio {
    private double salarioBase;
    private int anosContribuicao;

    public double calcularValor() {   // obrigatório — sem isso, não compila
        return salarioBase * (0.0175 * anosContribuicao);
    }
}

public class BeneficioPensao extends Beneficio {
    private double valorContribuicao;
    private double percentual;

    public double calcularValor() {
        return valorContribuicao * percentual;
    }
}

// Uso: o molde incompleto não pode ser instanciado
// Beneficio b = new Beneficio();   // ERRO de compilação — classe abstrata
Beneficio aposentadoria = new BeneficioAposentadoria();
double valor = aposentadoria.calcularValor();
```

> [!question] Por que não deixar `Beneficio` ser instanciada diretamente?
> Um "benefício genérico" com `calcularValor()` sem regra não existe no domínio real — todo benefício é aposentadoria, pensão, auxílio... A classe abstrata traduz isso em código: não há objeto "benefício em geral"; há objetos de benefícios **específicos** com a base comum.

### 5.1 Qual é a utilidade prática?

**Reuso + obrigação** — a utilidade prática em uma frase: a classe abstrata entrega o **código comum pronto** (`getNumeroBeneficio()` é herdado) e **força cada variação a se declarar** (`calcularValor()` abstrato — se não implementar, não compila). O desdobramento ("esqueleto" com passos fixos e variáveis) será retomado nos padrões de projeto.

### 5.2 O que aconteceria sem a classe abstrata?

Numa versão "ingênua", com `Beneficio` **concreta** e `calcularValor()` retornando `0` como padrão, `new Beneficio()` **compila** — e cria um objeto que não existe no domínio, devolvendo `0` silencioso; uma subclasse que esquece `calcularValor()` só erraria em **execução**. Com a classe abstrata, os dois problemas morrem juntos: `new Beneficio()` **não compila** e a subclasse que esquece o método abstrato **não compila** — o compilador vira o guardião do domínio.

### 5.3 Por que não usar sempre interface?

A resposta está no que cada uma carrega: a **classe abstrata** carrega **estado e código** (relação "é-um" com base compartilhada); a **interface** carrega apenas **contrato** (o comum é o que as classes **fazem**, não o que são). A tabela da seção 8 resume essa divisão — vale fixá-la.

- **(a)** **Classe abstrata não é instanciável** — `new ClasseAbstrata()` NÃO compila, mesmo que todos os métodos sejam concretos. A regra é a declaração `abstract`, não a presença de métodos abstratos.
- **(b)** **Pode ter construtor** — diferentemente da interface. O construtor não é chamado com `new`, mas **indiretamente**, via `super()` na subclasse, para inicializar os atributos do molde.
- **(c)** **Pode ter atributos e estado** — variáveis de instância normais, com valores que variam de objeto para objeto.
- **(d)** **Método abstrato não tem corpo** — termina com `;` após a assinatura. `{}` após a assinatura, mesmo vazio, o torna concreto.
- **(e)** **Uma classe só pode estender uma classe abstrata** — herança única via `extends`. As interfaces (seção 7) permitem implementação múltipla.

> [!warning] PEGADINHA — "instanciável se tiver método concreto", "método abstrato com corpo", "abstrata só se tiver método abstrato"
> - "Classe abstrata pode ser instanciada se tiver pelo menos um método concreto" — **FALSO**. A instanciabilidade é decidida pela palavra `abstract`, nada mais.
> - "Método abstrato pode ter corpo" — **FALSO**. Corpo é exatamente o que ele não tem; só a assinatura.
> - "Uma classe só pode ser abstrata se tiver método abstrato" — **FALSO**. Pode ser declarada `abstract` sem nenhum método abstrato — para impedir a instanciação ou servir de base comum.

---

## 6. Polimorfismo — muitas formas, mesma interface

**Polimorfismo** (do grego, "muitas formas") é a capacidade de **tratar objetos de classes diferentes de maneira uniforme**, através de uma **interface comum**, de modo que cada objeto **responda de forma própria** à mesma chamada. O polimorfismo tem duas faces que a FGV cobra:

- **sobrescrita (override):** a subclasse **redefine** um método herdado — cada classe tem sua versão, com a mesma assinatura;
- **sobrecarga (overload):** a mesma classe tem **vários métodos com o mesmo nome**, mas assinaturas (parâmetros) diferentes — **herança não é exigida**. Uma subclasse pode criar sobrecarga de método herdado, mas isso não é requisito do mecanismo.

Veja o problema e a correção:

```java
// Sem polimorfismo: um único método decide pelo tipo, com if/else
public void processar(String tipo, double valor) {
    if (tipo.equals("PIX")) {
        System.out.println("Valor final: " + valor * 0.95);   // 5% de desconto
    } else if (tipo.equals("CARTAO")) {
        System.out.println("Valor final: " + valor * 1.03);   // 3% de taxa
    }
    // novo tipo de pagamento? novo else if aqui dentro...
}
```

O problema: cada novo tipo exige **alterar** `processar` — viola o princípio aberto/fechado (OCP): aberto para extensão, fechado para modificação. A correção (subseção 6.1) usa o **override**: um novo tipo é apenas uma **nova subclasse**, sem tocar no método existente.

### 6.1 Sobrescrita (override) — mesma assinatura, comportamento próprio

```java
// Sobrescrita: mesma assinatura, comportamento diferente por classe
public class Pagamento {
    public double calcularValor() { return 0; }
}

public class PagamentoPix extends Pagamento {
    private double valor;
    private double desconto = 0.05;   // 5%
    public PagamentoPix(double valor) {   // construtor — inicializa o campo
        this.valor = valor;
    }
    @Override
    public double calcularValor() {
        return valor * (1 - desconto);
    }
}

public class PagamentoCartao extends Pagamento {
    private double valor;
    private double taxa = 0.03;       // 3%
    public PagamentoCartao(double valor) {   // construtor — inicializa o campo
        this.valor = valor;
    }
    @Override
    public double calcularValor() {
        return valor * (1 + taxa);
    }
}

// Uso polimórfico: o mesmíssimo código trata todos os pagamentos
public void processar(Pagamento p) {
    System.out.println("Valor final: " + p.calcularValor());
}
processar(new PagamentoPix(100.0));
processar(new PagamentoCartao(100.0));
```

Quem chama `processar` só vê a interface `Pagamento` — cada objeto responde do seu jeito. Esse é o **dispatch dinâmico** (late binding): o **compilador valida** que `calcularValor()` existe e gera chamada **indireta**; o **computador decide** pela JVM, com base no **tipo real** do objeto. A divisão de papéis está na tabela da subseção 6.3.

A anotação `@Override` é **recomendada**, não obrigatória: informa ao compilador que você pretende sobrescrever o método do pai — se a assinatura não bater, erro de compilação, sem bugs silenciosos.

> [!warning] Restrições do override
> Sobrescrever **não pode reduzir visibilidade**: trocar `protected` do pai por `private` no filho **não compila**; ampliar de `protected` para `public` é permitido. Vale também a **covariância de retorno**: a subclasse pode sobrescrever devolvendo um **subtipo** do tipo retornado pelo pai.

### 6.2 Sobrecarga (overload) — mesmo nome, assinaturas diferentes

```java
public class CalculadoraBeneficio {
    // Sobrecarga: mesmo nome, parâmetros diferentes
    public double calcular(double renda) {
        return renda * 0.30;
    }
    public double calcular(double renda, double margem) {
        return renda * (margem / 100.0);
    }
    public double calcular(double renda, double margem, int meses) {
        return renda * (margem / 100.0) * meses;
    }
}
```

Aqui não há herança — os três `calcular` coexistem na mesma classe; o compilador escolhe a variante pelos **parâmetros** (tempo de compilação), com a ordem de preferência da subseção 6.3.

### 6.3 Compilador vs computador: quando cada forma decide

A pergunta que a banca adora fazer: **quem decide o quê, e em qual momento?** As respostas são opostas — a tabela abaixo é a que cai em prova:

| | **Sobrescrita (override)** | **Sobrecarga (overload)** |
|---|---|---|
| **Quando a decisão ocorre** | Tempo de **execução** | Tempo de **compilação** |
| **Mecanismo** | Dispatch dinâmico / **late binding** / ligação tardia | **Early binding** / ligação estática |
| **Requisito** | Herança — a subclasse redefine um método herdado | Pode ocorrer na mesma classe, **sem herança** |
| **Assinatura** | Mesma assinatura, corpo diferente | Mesmo nome, assinaturas diferentes |

Decore o jogo de palavras: **"tempo de execução", "late binding", "ligação tardia", "dispatch dinâmico", "tipo real do objeto" → override**; **"tempo de compilação", "early binding", "ligação estática" → overload**.

A indireção do override tem custo: é levemente mais cara que uma chamada direta. Por isso os métodos `static`, `private` e `final` são **vinculados em tempo de compilação** — não participam do polimorfismo (`static` pertence à classe; `private` não é herdado; `final` não pode ser sobrescrito).

**No overload, a compilação decide e grava.** Ele resolve tudo pela **assinatura** — nome + tipos/quantidade de parâmetros — e grava no bytecode **qual método exato** será chamado. Em execução não há decisão. Ordem de preferência que cai em prova:

1. **match exato** — o tipo do argumento bate com o parâmetro;
2. **alargamento (widening)** — ex.: `int` → `double`;
3. **boxing** — ex.: `int` → `Integer`;
4. **varargs** — o argumento é aceito como elemento de um array variável.

E o detalhe que a FGV adora: o **tipo de retorno NÃO participa da distinção**. Dois métodos com o mesmo nome e os mesmos parâmetros, diferindo só no retorno, são **erro de compilação**.

> [!note] As três formas clássicas de polimorfismo
> A literatura classifica o polimorfismo em três formas: **subtyping** (sobrescrita), **ad-hoc** (sobrecarga) e **paramétrico** (generics — tema de [[Generics]]).

> [!warning] PEGADINHA — "qual forma decide quando" (o ângulo do compilador)
> Falsos clássicos: "no override, o compilador decide" (a decisão é da **execução**); "sobrecarga exige herança" (ocorre até na mesma classe); "sobrecarga distingue pelo retorno" (retorno não participa); "`private` pode ser sobrescrito" (não é herdado); "`@Override` é obrigatória" (é recomendada — valida a assinatura).
> Pergunta decisiva: *quem está decidindo — o compilador ou a execução?* Para se proteger: (1) quem escolhe a **assinatura**? o compilador (overload); (2) quem escolhe a **implementação**? a execução (override). Se a frase cruzar esses papéis, está errada.

### 6.4 A pegadinha avançada: overload + override juntos

Na vida real, os dois mecanismos aparecem **juntos** — e cada um faz a sua parte, em momentos diferentes. A confusão de prova é achar que eles disputam a mesma decisão. Não disputam:

- a **sobrecarga** escolhe a **assinatura** pelo **tipo declarado** da referência — em tempo de compilação;
- o **dispatch dinâmico** escolhe a **implementação** pelo **tipo real** do objeto — em tempo de execução.

Veja o caso clássico, adaptado ao domínio previdenciário:

```java
class Beneficio {
    void calcular(Beneficio b) {
        System.out.println("Beneficio.calcular(Beneficio)");
    }
}

class Aposentadoria extends Beneficio {
    // OVERRIDE: mesma assinatura do pai, comportamento próprio
    void calcular(Beneficio b) {
        System.out.println("Aposentadoria.calcular(Beneficio)");
    }

    // OVERLOAD novo: mesma classe, assinatura diferente — não existe no pai
    void calcular(Aposentadoria a) {
        System.out.println("Aposentadoria.calcular(Aposentadoria)");
    }
}

Beneficio ref = new Aposentadoria();
ref.calcular(new Aposentadoria());
// imprime: Aposentadoria.calcular(Beneficio)
```

O que é impresso? A resposta correta — e contra-intuitiva — é **`Aposentadoria.calcular(Beneficio)`**. Raciocine em dois tempos:

1. **Tempo de compilação — a sobrecarga escolhe a assinatura.** `ref` é declarada como `Beneficio`. Para o compilador, o conjunto de métodos visíveis é o da classe `Beneficio`: apenas `calcular(Beneficio)`. O overload `calcular(Aposentadoria)`, definido só na subclasse, é **invisível** para essa referência — a escolha da assinatura fica congelada na compilação.
2. **Tempo de execução — o dispatch dinâmico escolhe a implementação.** O objeto real é `Aposentadoria`, que **sobrescreveu** `calcular(Beneficio)`. A JVM executa a versão da subclasse, com a assinatura decidida no passo 1.

O contraste fecha o entendimento: se a referência fosse declarada `Aposentadoria`, o resultado mudaria — `Aposentadoria ref2 = new Aposentadoria(); ref2.calcular(new Aposentadoria());` imprimiria **`Aposentadoria.calcular(Aposentadoria)`**, porque aí o overload fica visível em tempo de compilação.

> [!warning] PEGADINHA — a resposta apressada "Aposentadoria.calcular(Aposentadoria)"
> Quem responde "o objeto é `Aposentadoria`, logo executa `calcular(Aposentadoria)`" usou apenas o tempo de execução e ignorou o passo 1. A sobrecarga já tinha escolhido `calcular(Beneficio)` **na compilação**, antes de qualquer objeto ser consultado. O tipo real decide **qual versão da assinatura escolhida** será executada; ele não reabre a escolha da assinatura. Compilação escolhe assinatura; execução escolhe implementação.

> [!tip] Polimorfismo e o princípio Open/Closed
> O polimorfismo por sobrescrita é o mecanismo que torna possível o **Open/Closed** (aberto para extensão, fechado para modificação). Para adicionar `PagamentoBoleto`, basta criar uma nova subclasse sem alterar `processar`. Tema da nota [[Principios-SOLID]].

---

## 7. Interface: o contrato

Nem sempre queremos depender de uma classe concreta, de um "como" — muitas vezes o que importa é o **o quê**: o **contrato de comportamento**. A **interface** é o **tipo que define o contrato**: declara **o que** o objeto sabe fazer, **sem dizer como**; **não é instanciável**, e quem assume o contrato é a classe, com `implements`. No contexto DATAPREV: CPF e CNS têm regras de validação diferentes, mas para quem usa basta saber que existe "validar(documento)" — contrato único, regras de cada implementação.

Veja o problema e a correção:

```java
// Quem valida decide qual classe concreta usar, com if/else
public boolean validarDocumento(String tipo, String documento) {
    if (tipo.equals("CPF")) {
        return new ValidadorCpf().validar(documento);
    } else if (tipo.equals("CNS")) {
        return new ValidadorCns().validar(documento);
    }
    return false;
}
```

O problema: quem valida **acopla-se às classes concretas** e precisa de `if/else` para cada documento — novo documento, novo `else if`, alteração no chamador. A correção **inverte** isso: o chamador depende apenas do **contrato** `ValidaDocumento`; estender não exige modificar quem usa.

```java
// Interface: o contrato — declara o QUE, não o COMO
public interface ValidaDocumento {
    boolean validar(String documento);
}

// Quem assume o contrato: a classe implementa e define o COMO
public class ValidadorCpf implements ValidaDocumento {
    public boolean validar(String documento) {
        // regra de validação do CPF (dígitos verificadores, tamanho, ...)
        return documento != null && documento.length() == 11;
    }
}

public class ValidadorCns implements ValidaDocumento {
    public boolean validar(String documento) {
        // regra de validação do CNS (formato específico do cartão de saúde)
        return documento != null && documento.length() == 15;
    }
}
// Uso: quem valida só conhece o contrato, não a regra de cada documento
ValidaDocumento validador = new ValidadorCpf();
boolean ok = validador.validar("12345678900");
```

Repare: `validador` é do tipo da **interface**, mas o objeto é de uma **classe concreta** — o dispatch dinâmico da seção 6 decide, em execução, qual `validar()` será chamado.

> [!question] E se amanhã surgir um novo documento?
> Basta criar `ValidadorNit implements ValidaDocumento` — ninguém que já usa o contrato muda uma linha: **estender** sem **modificar** (espírito do OCP, tema de [[Principios-SOLID]]).

Agora os pontos que caem em prova:

- **(a)** **`new Interface()` não compila.** Interface não é instanciável — ela é só o contrato. Quem se instancia com `new` é a classe concreta que a implementa.
- **(b)** **Uma classe pode implementar várias interfaces.** Java não tem herança múltipla de *classes*, mas uma classe assume vários *contratos* (`class X implements A, B`). Herança múltipla de classe é proibida; múltiplas implementações, permitidas.

> [!note] Interface também herda
> Interface pode herdar de interface — `interface A extends B` — inclusive **múltiplas** (`interface A extends B, C`). Herança de interface é permitida; herança múltipla de classe, não.

- **(c)** **Métodos de interface são implicitamente `public abstract`.** Você pode escrever `boolean validar(String documento);` sem os modificadores — o compilador os insere.
- **(d)** **Atributos de interface são implicitamente `public static final`** — **constantes** (ex.: `int TAMANHO_CPF = 11;`). Consequência: interface **não guarda estado** — não há variável de instância que mude por objeto.
- **(e)** **Default methods (Java 8+):** uma interface pode trazer método **com corpo** desde que marcado como `default` (ou `static`) — para evoluir contratos sem quebrar implementações. O essencial continua sendo o método *sem* corpo.

> [!warning] PEGADINHA — "interface instanciável", "herança múltipla via interface", "atributo que varia por objeto"
> - "Interfaces podem ser instanciadas com `new` se tiverem métodos default" — **FALSO**. Nenhuma interface é instanciável.
> - "Uma classe herda de várias classes por meio de interfaces" — **FALSO**. Quem implementa é a classe; Java não tem herança múltipla de classe.
> - "Atributos de interface variam por objeto" — **FALSO**. São `public static final` — constantes, não estado.
>
> Pergunta decisiva: *atribuíram uma característica de classe concreta a uma interface?* Se sim, está errada — e o método `default` dá corpo a um método, mas **não torna a interface instanciável** (quem se instancia com `new` é sempre a classe concreta).

---

## 8. Interface vs. classe abstrata: a tabela que cai em prova

A regra prática da banca: **classe abstrata** é para relações "é-um" com estado e implementação compartilhada entre classes **próximas**; **interface** é para o **contrato de comportamento** que classes **não relacionadas** podem assumir (CPF e CNS não são da mesma família, mas ambos "são validáveis").

| Característica | Classe abstrata | Interface |
|---|---|---|
| **Instanciação** | Não é instanciável (`new` não compila) | Não é instanciável (`new` não compila) |
| **Ligação** | Herança única via `extends` | Múltiplas implementações via `implements` |
| **Métodos** | Concretos (com corpo) e abstratos (sem corpo) | Abstratos (sem corpo) — e `default`/`static` com corpo no Java 8+ |
| **Atributos** | Variáveis de instância (estado que varia por objeto) | Apenas constantes `public static final` — não guarda estado |
| **Construtor** | Existe (chamado via `super()` na subclasse) | Não existe |
| **Uso típico** | "É-um" com base comum e código compartilhado | Capacidade/contrato assumido por classes não relacionadas |

> [!warning] PEGADINHA — a FGV adora inverter as características
> O jogo mais comum é **deslocar uma característica de um lado para o outro**: "interface pode ter atributos de instância"; "classe abstrata implementada com `implements`"; "interface pode ser instanciada" — todas falsas. Como se proteger: decore **a qual conceito pertence cada característica** — instanciação: nenhuma; ligação: `extends` vs `implements`; atributos: instância vs constantes; construtor: existe vs não existe. Se a alternativa cruzar as colunas, está errada.

---

## 9. Visibilidade dos membros — quem vê o quê?

Por trás do encapsulamento está o controle de visibilidade. A FGV cobra os quatro níveis de modificadores de acesso do Java:

| Modificador | Visível na mesma classe | Visível na subclasse | Visível no pacote | Visível fora do pacote |
|---|---|---|---|---|
| `private` | sim | **não** | **não** | **não** |
| *(padrão, sem modificador)* | sim | **não** | sim | **não** |
| `protected` | sim | sim | sim | **não** |
| `public` | sim | sim | sim | sim |

A regra do "padrão" é frequentemente esquecida: ele permite acesso dentro do mesmo pacote, mas **não** é herdado pela subclasse em outro pacote. `protected` é mais permissivo do que o nome sugere — abre para **duas** audiências: subclasses e classes do mesmo pacote.

```java
// Exemplo prático dos modificadores
public class Beneficiario {
    private String cpf;          // só Beneficiario enxerga
    String numeroDoBeneficio;    // pacote: classes do mesmo pacote
    protected double renda;      // subclasse + pacote
    public String nome;          // todos
}
```

> [!warning] PEGADINHA — `protected` e `private`
> O `private` **não é herdado** — a subclasse não enxerga o atributo `private` do pai; acessa via métodos públicos ou protegidos. Já o `protected` é herdado e visível na subclasse. Frase clássica: "o membro `private` é acessível na subclasse" — **falso**. E `protected` é visível **no pacote** também, embora o nome sugira apenas a hierarquia.

---

## 10. Como a FGV cobra este tópico

### Palavras-chave do edital

abstração, encapsulamento, herança, composição, polimorfismo, override, overload, sobrescrita, sobrecarga, `private`, `protected`, `public`, visibilidade, subclasse, superclasse, relação "é-um", relação "tem-um", `extends`, `@Override`, classe abstrata, método abstrato, `abstract`, interface, contrato, `implements`, default method, tempo de compilação, tempo de execução, early binding, late binding, dispatch dinâmico, ligação estática, ligação tardia.

A banca explora o tema por vários ângulos:

| Palavra-chave no enunciado | O que está sendo testado |
|---|---|
| "simplificar o modelo" | Abstração |
| "proteger/esconder dados internos" | Encapsulamento |
| "é-um" vs. "tem-um" | Herança vs. composição |
| "mesma assinatura, subclasse" | Sobrescrita (override) |
| "mesmo nome, assinaturas diferentes" | Sobrecarga (overload) |
| "tempo de compilação" | Sobrecarga (overload) — resolução estática |
| "tempo de execução" / "tipo real do objeto" | Sobrescrita (override) — dispatch dinâmico |
| `private`, `protected`, `public` | Tabela de visibilidade |
| "membro herdado pela subclasse" | Qual modificador permite herança de acesso |
| "não pode ser instanciada", `abstract` | Classe abstrata |
| "declara o quê, não o como" | Interface |
| "contrato", `implements` | Interface |
| "inverter características" | Interface vs. classe abstrata |

---

## 11. Questões-modelo (pegada FGV)

### Questão 1 — Qual é a relação correta?

> [!example] Enunciado
> Considere as afirmações sobre os pilares do POO:
>
> I. Abstração decide quais atributos e métodos são relevantes para o modelo.
> II. Encapsulamento permite acesso direto aos atributos de uma classe.
> III. Herança materializa a relação "tem-um" entre classes.
> IV. Polimorfismo permite tratar objetos de classes diferentes por uma interface comum.
>
> Estão corretas **apenas**:
>
> **(A)** I e IV.
> **(B)** II e III.
> **(C)** I, III e IV.
> **(D)** II e IV.
> **(E)** I, II e III.

> [!tip] Gabarito e comentário
> **Resposta: (A)**
> I correta (abstração seleciona o relevante); II **errada** (encapsulamento protege com `private`); III **errada** (herança é "é-um", "tem-um" é composição); IV correta (definição clássica de polimorfismo). A banca inverte os pares abstração/encapsulamento e herança/composição.

### Questão 2 — Visibilidade e herança

> [!example] Enunciado
> Dado o código:
>
> ```java
> class A {
>     private int x = 10;
>     protected int y = 20;
>     int z = 30;       // modificador padrão (package-private)
> }
>
> class B extends A {
>     public void mostrar() {
>         System.out.println(x);    // linha 1
>         System.out.println(y);    // linha 2
>         System.out.println(z);    // linha 3
>     }
> }
> ```
>
> Considerando que `A` e `B` estão no **mesmo pacote**, qual das linhas gera erro de compilação?
>
> **(A)** Apenas a linha 1.
> **(B)** Apenas a linha 2.
> **(C)** Apenas a linha 3.
> **(D)** Nenhuma linha gera erro.
> **(E)** Todas as linhas geram erro.

> [!tip] Gabarito e comentário
> **Resposta: (A)**
> `x` é `private` — `B` **não pode acessá-lo diretamente**, mesmo no mesmo pacote. `y` é `protected` (subclasse + pacote). `z` é package-private e, como estão no mesmo pacote, é acessível. A linha 1 gera erro; 2 e 3 funcionam. Em pacotes diferentes, apenas `z` ficaria inacessível — `protected` vence entre pacotes para a subclasse.

### Questão 3 — Polimorfismo na prática

> [!example] Enunciado
> Qual das alternativas melhor descreve o que ocorre quando `processar(pagamentoPix)` é chamado, sendo `PagamentoPix extends Pagamento` e `pagamentoPix` criado com `new PagamentoPix(100.0)`?
>
> **(A)** O método `calcularValor()` de `Pagamento` é executado, pois `Pagamento` é a classe referenciada.
> **(B)** O método `calcularValor()` de `PagamentoPix` é executado por ser a versão sobrescrita — comportamento decidido em tempo de execução.
> **(C)** O compilador seleciona o método com base no tipo da referência (`Pagamento`), ignorando o tipo real.
> **(D)** O Java executa ambos os métodos (pai e filho) e soma os resultados.
> **(E)** Ocorre erro de compilação, pois `Pagamento` é abstrata.

> [!tip] Gabarito e comentário
> **Resposta: (B)**
> Embora o parâmetro seja `Pagamento`, o Java chama a versão do objeto real (`PagamentoPix`) em tempo de execução — **dispatch dinâmico** (late binding). A descreveria comportamento estático; C descreveria resolução de sobrecarga, não de sobrescrita; D e E são incorretas.

### Questão 4 — Interface vs. classe abstrata

> [!example] Enunciado
> Sobre interfaces e classes abstratas em Java, assinale a alternativa correta:
>
> **(A)** Uma interface pode ser instanciada diretamente com `new` quando possui métodos default.
> **(B)** Uma classe abstrata pode ser criada com `new` se todos os seus métodos forem concretos.
> **(C)** Métodos declarados em uma interface são implicitamente `public abstract` e seus atributos, `public static final`.
> **(D)** Uma classe pode implementar apenas uma interface, pois o Java não permite herança múltipla.
> **(E)** Uma classe abstrata pode ter métodos com corpo, mas não pode declarar métodos abstratos.

> [!tip] Gabarito e comentário
> **Resposta: (C)**
> Métodos de interface são implicitamente `public abstract`; atributos, `public static final` (constantes — por isso não guarda estado). (A) falsa: nenhuma interface é instanciável. (B) falsa: a regra é a declaração `abstract`. (D) falsa: pode implementar **várias** interfaces — proibida é a herança múltipla de classes. (E) falsa: pode — e frequentemente deve — declarar métodos abstratos.

### Questão 5 — Overload + override juntos: quem decide o quê?

> [!example] Enunciado
> Considere o código:
>
> ```java
> class Beneficio {
>     void calcular(Beneficio b) {
>         System.out.println("Beneficio.calcular(Beneficio)");
>     }
> }
>
> class Aposentadoria extends Beneficio {
>     void calcular(Beneficio b) {
>         System.out.println("Aposentadoria.calcular(Beneficio)");
>     }
>     void calcular(Aposentadoria a) {
>         System.out.println("Aposentadoria.calcular(Aposentadoria)");
>     }
> }
>
> Beneficio ref = new Aposentadoria();
> ref.calcular(new Aposentadoria());
> ```
>
> O que é impresso ao executar a última linha?
>
> **(A)** `Beneficio.calcular(Beneficio)`
> **(B)** `Aposentadoria.calcular(Beneficio)`
> **(C)** `Aposentadoria.calcular(Aposentadoria)`
> **(D)** Erro de compilação
> **(E)** As duas versões, em sequência

> [!tip] Gabarito e comentário
> **Resposta: (B)**
> O raciocínio completo está na subseção 6.4: em **tempo de compilação**, a sobrecarga escolhe a assinatura pelo tipo declarado (`Beneficio` → `calcular(Beneficio)`); em **tempo de execução**, o dispatch dinâmico escolhe a implementação pelo tipo real (`Aposentadoria` sobrescreveu essa assinatura). **(C)** é a resposta apressada — só valeria se a referência fosse `Aposentadoria`. **(A)**, **(D)** e **(E)** não ocorrem.

---

## 12. Revisão rápida

| Pilar / Conceito | O que é | Palavra-chave de prova | Erro mais comum em prova |
|---|---|---|---|
| **Abstração** | Modelar só o essencial, ignorar o irrelevante | simplificar, modelo, domínio | Confundir com encapsulamento |
| **Encapsulamento** | Proteger estado interno, acesso por métodos controlados | `private`, getters/setters, validação | Achar que é só "esconder" sem valor |
| **Herança** | Subclasse herda e especializa da superclasse | "é-um", `extends`, sobrescrita | Confundir com composição ("tem-um") |
| **Classe abstrata** | Molde incompleto — não instanciável; pode ter métodos concretos e abstratos | `abstract`, `extends`, método abstrato | Achar que pode ser instanciada se tiver método concreto |
| **Polimorfismo** | Mesma interface, comportamento próprio por classe | override, overload, dispatch dinâmico, tempo de compilação (overload) vs tempo de execução (override) | Confundir sobrescrita com sobrecarga |
| **Interface** | Contrato de comportamento — declara o "quê" sem o "como"; não instanciável | `implements`, contrato, `public abstract` | Dizer que é instanciável ou que guarda estado |
| **Interface vs. classe abstrata** | Classe abstrata: "é-um" com estado; interface: contrato de capacidade | inverter características | Trocar características de um lado para o outro |
| **Visibilidade** | Controle de acesso: private, padrão, protected, public | `private` não é herdado; `protected` = pacote + subclasse | Achar que `private` é acessível na subclasse |

> [!note] A ideia que resume a nota
> **A banca adora inverter:** abstração por encapsulamento, herança por composição, sobrescrita por sobrecarga e características de interface/classe abstrata. Na hora da questão: *simplificar ou proteger? "é-um" ou "tem-um"? Essa característica é de interface ou de classe abstrata?*

---

## 13. Próximos passos

Os quatro pilares — acrescidos de classe abstrata e interface — são a **base** de tudo que vem a seguir. Com eles dominados, você está pronto para os princípios de design que organizam esses pilares em boas práticas:

- [[Principios-SOLID]] — os cinco princípios que orientam código coeso, desacoplado e extensível. O Open/Closed depende diretamente do polimorfismo por sobrescrita; o ISP e o DIP exploram o contrato que a interface define.
- [[Clean-Code]] — nomes significativos, funções pequenas, comentários úteis. Os pilares do POO se materializam em código limpo quando aplicados com consciência.

O índice de referência para este tópico é [[Paradigma-Orientado-a-Objetos]].