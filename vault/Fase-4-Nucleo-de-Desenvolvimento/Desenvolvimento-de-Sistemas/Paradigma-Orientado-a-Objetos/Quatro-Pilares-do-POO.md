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

Em um sistema de benefícios da DATAPREV, cada um dos pilares aparece em uma situação concreta:

- **Abstração:** do beneficiário, o sistema precisa de `cpf` e `rendaMensal`, mas não da cor dos olhos. Modelar só o relevante.
- **Encapsulamento:** o CPF deve ser validado antes de ser aceito — ninguém deveria atribuir um CPF direto no atributo, sem verificação.
- **Herança:** `Servidor`, `Pensionista` e `Beneficiario` compartilham dados comuns (nome, CPF) mas têm regras distintas.
- **Polimorfismo:** um pagamento pode ser Pix ou cartão — o método `processar` não precisa saber qual é; cada tipo calcula o valor do seu jeito.

> [!question] Pergunta orientadora
> Se você pudesse resumir em uma frase por que a indústria abandonou a programação procedural em massa, qual seria? A resposta tem a ver com estes quatro pilares.

---

## 2. Abstração — modelar só o que importa

**Abstração** é a capacidade de **modelar apenas os aspectos relevantes** de uma entidade do mundo real, **ignorando os detalhes que não interessam** ao sistema. No contexto de benefícios, do beneficiário interessa a `rendaMensal` e o `cpf` — mas não a cor do cabelo ou a marca do carro. Abstrair é **selecionar o que importa** para o domínio.

A pergunta socrática que guia a abstração é sempre: **"para o sistema que estamos construindo, esse dado é relevante?"** Se a resposta for não, ele não entra no modelo.

Veja a diferença na prática:

```java
// ABSTRAÇÃO RUIM — atributos demais, irrelevantes para o domínio
public class Beneficiario {
    private String nome;
    private String cpf;
    private double rendaMensal;
    private String corDoCabelo;      // irrelevante para benefícios
    private String marcaDoCarro;     // irrelevante para benefícios
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

Quem não abstrai cria classes gigantes com dezenas de atributos irrelevantes — e isso dificulta manutenção, testes e compreensão. Quem abstrai bem cria classes enxutas, com responsabilidade clara. No contexto DATAPREV, isso significa: para um sistema de consignação, o que importa é o `valorDaPensao` e o `numeroDoBeneficio`, não o histórico de endereços.

> [!warning] PEGADINHA — abstração vs. encapsulamento
> A FGV costuma misturar os termos. **Abstração** é *simplificar*: modelar só o essencial, escondendo a complexidade do que não interessa. **Encapsulamento** é *proteger*: esconder o estado interno do objeto, expondo apenas uma interface controlada. Abstração decide *o que* o objeto representa; encapsulamento decide *como* isso fica protegido. Uma alternativa que diz que abstração é "esconder dados do usuário" está **misturando os conceitos**.

---

## 3. Encapsulamento — proteger o estado interno

**Encapsulamento** é o princípio de **proteger os dados internos** do objeto, permitindo acesso e modificação apenas por **métodos controlados** — não por acesso direto aos atributos. Na prática, os atributos ficam **privados** (`private`) e o acesso passa por **métodos getters/setters** (ou por métodos que representam regras de negócio).

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

O valor didático do encapsulamento vai além de "esconder": ele **centraliza a validação e a regra de negócio** no próprio objeto. Qualquer outro código que tente atribuir um CPF inválido passa pelo mesmo `setCpf` e é barrado. Sem encapsulamento, cada ponto do sistema validaria do seu jeito — e os bugs de consistência se espalhariam.

Observe que o `setCpf` não apenas protege: ele **adiciona comportamento** ao ato de atribuir um valor. Isso transforma uma operação simples (atribuição) em uma operação inteligente (atribuição + validação). Esse é o verdadeiro poder do encapsulamento — não é só barreira, é **lógica de negócio embutida** no objeto.

> [!question] Por que não deixar os atributos públicos?
> Imagine que 10 partes do sistema atribuam CPF diretamente, cada uma com uma validação diferente. Quando a regra muda (ex.: novos dígitos verificadores), é preciso caçar todos os 10 pontos. Com encapsulamento, muda-se **um único método** `setCpf`. A pergunta se responde sozinha: encapsulamento é **manutenibilidade** em forma de código.

A ligação com `private` é direta: o modificador `private` é o mecanismo que **implementa** o encapsulamento em Java. Sem ele, qualquer classe externa poderia alterar `cpf` diretamente, pulando a validação. Veremos na seção 9 como os quatro modificadores de acesso (`private`, padrão, `protected`, `public`) definem os limites do que pode ser acessado.

---

## 4. Herança — herdar e especializar

**Herança** é a relação em que uma classe (**subclasse**/classe derivada/filha) **herda atributos e métodos** de outra (**superclasse**/classe base/pai), podendo **adicionar** novos e **sobrescrever** (especializar) os herdados. É a materialização do relacionamento "é-um" ("é um tipo de").

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

Note que `Beneficiario` não precisa redeclarar `nome` e `cpf` — ele herda de `Pessoa`. Pode, porém, adicionar o que é próprio dele (`rendaMensal`) e sobrescrever métodos quando o comportamento precisa ser diferente. A palavra-chave `extends` materializa a herança; `protected` permite que a subclasse acesse diretamente os atributos herdados.

A herança promove **reutilização** (não repetir `nome` e `cpf` em cada subclasse) e **especialização** (cada subclasse adiciona o que é próprio). Porém, ela cria uma ligação forte entre pai e filho — mudar a superclasse afeta todas as subclasses.

Aqui reside a armadilha mais clássica de prova:

> [!warning] PEGADINHA — herança vs. composição
> A pergunta clássica: *"deve-se preferir herança ou composição?"* A resposta favorita da banca moderna é **composição** ("prefira composição a herança" — princípio defendido inclusive por autores de Clean Code). Composição é a relação "tem-um" (um `Carro` *tem* um `Motor`), enquanto herança é "é-um" (um `Carro` *é* um `Veículo`). Herança cria **acoplamento forte** entre as classes — mudar o pai afeta todos os filhos — e pode gerar hierarquias rígidas. Composição é mais flexível. Quando a prova perguntar qual princípio orienta o design atual, a tendência é: **composição antes de herança**, exceto quando a "é-um" for genuína e estável.

---

## 5. Classe abstrata: a herança que obriga a implementar

A classe abstrata é o **molde incompleto**: ela define estrutura e comportamento comuns para um grupo de subclasses, mas **não pode ser instanciada**. Pense nela como uma planta que não pode virar produto final sozinha — ela precisa de uma subclasse concreta que **complete** as partes que faltam.

O que falta são os **métodos abstratos**: métodos **sem corpo** — apenas a assinatura. Eles funcionam como um compromisso: "todo benefício será capaz de calcular seu valor, mas cada tipo calcula do seu jeito". A subclasse concreta, usando `extends` (que você já viu na seção de herança), é **obrigada a implementar** esses métodos — se não implementar, ela também será abstrata e continuará incompleta.

A relação com herança é direta: a classe abstrata é uma superclasse que a subclasse herda via `extends`. O `super()` é o mecanismo pelo qual a subclasse chama o construtor da superclasse — e é por ele que os atributos do molde abstrato são inicializados quando a subclasse concreta é criada. A diferença crucial é que a superclasse abstrata **não pode ser instanciada diretamente** — `new Beneficio()` não compila — mas o construtor dela roda indiretamente, via `super()`, quando a subclasse concreta é criada.

Veja um exemplo no domínio previdenciário: todo benefício do INSS tem um número de benefício, que pode ser consultado da mesma forma para todos — mas o cálculo do valor depende do tipo de benefício:

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

Note o que a herança fez aqui: `getNumeroBeneficio()` é herdado por ambos os benefícios — o comportamento comum fica no molde; o comportamento específico (o cálculo) fica em cada subclasse. A classe abstrata obriga cada subclasse a dar sua resposta para `calcularValor()` — é a herança funcionando como um contrato interno: "se você herda Benefício, é obrigada a saber calcular seu valor".

> [!question] Por que não deixar `Beneficio` ser instanciada diretamente?
> O que significaria um "benefício genérico" com `calcularValor()` sem regra definida? Ele não existe no domínio real: todo benefício é aposentadoria, pensão, auxílio... A classe abstrata traduz isso em código: não há objeto "benefício em geral"; há objetos de benefícios **específicos** que compartilham a base comum.

Pontos que caem em prova:

(a) **Classe abstrata não é instanciável** — `new ClasseAbstrata()` NÃO compila, mesmo que todos os seus métodos sejam concretos. A regra é a declaração `abstract`, não a presença de métodos abstratos.

(b) **Pode ter construtor** — e isso a diferencia da interface. O construtor da classe abstrata não é chamado com `new` diretamente, mas **indiretamente**, via `super()` na subclasse, para inicializar os atributos do molde.

(c) **Pode ter atributos e estado** — variáveis de instância normais, com valores que variam de objeto para objeto.

(d) **Método abstrato não tem corpo** — termina com `;` após a assinatura. Se você escrever `{}` após a assinatura, mesmo vazio, deixa de ser abstrato e passa a ser concreto.

(e) **Uma classe só pode estender uma classe abstrata** — herança única via `extends`. As interfaces, que veremos na seção 7, são diferentes: uma classe pode implementar várias delas.

> [!warning] PEGADINHA — "instanciável se tiver método concreto", "método abstrato com corpo", "abstrata só se tiver método abstrato"
> - "Classe abstrata pode ser instanciada se tiver pelo menos um método concreto" — **FALSO**. A instanciabilidade é decidida pela palavra `abstract` na declaração, nada mais.
> - "Método abstrato pode ter corpo" — **FALSO**. Corpo é exatamente o que ele não tem; só a assinatura.
> - "Uma classe só pode ser abstrata se tiver método abstrato" — **FALSO**. Uma classe pode ser declarada `abstract` mesmo sem nenhum método abstrato — por exemplo, para impedir que seja instanciada ou para servir apenas de base comum.

---

## 6. Polimorfismo — muitas formas, mesma interface

**Polimorfismo** (do grego, "muitas formas") é a capacidade de **tratar objetos de classes diferentes de maneira uniforme**, através de uma **interface comum** (contrato, definido adiante nesta nota), de modo que cada objeto **responda de forma própria** à mesma chamada. O polimorfismo tem duas faces que a FGV cobra:

- **sobrescrita (override):** a subclasse **redefine** um método herdado — cada classe tem sua versão, com a mesma assinatura;
- **sobrecarga (overload):** a mesma classe (ou classes diferentes) tem **vários métodos com o mesmo nome**, mas assinaturas (parâmetros) diferentes.

### 6.1 Sobrescrita (override) — mesma assinatura, comportamento próprio

```java
// Sobrescrita: mesma assinatura, comportamento diferente por classe
public class Pagamento {
    public double calcularValor() { return 0; }
}

public class PagamentoPix extends Pagamento {
    private double valor;
    private double desconto = 0.05;   // 5%

    @Override
    public double calcularValor() {
        return valor * (1 - desconto);
    }
}

public class PagamentoCartao extends Pagamento {
    private double valor;
    private double taxa = 0.03;       // 3%

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

Quem chama `processar` **não sabe** se o pagamento é Pix ou cartão — ele só vê a interface `Pagamento` e chama `calcularValor()`. Cada objeto concreto responde do seu jeito. É a essência do polimorfismo: **mesmo código, comportamento variado conforme o objeto real**. Esse mecanismo se chama **dispatch dinâmico** (ou late binding) — a decisão de qual método executar é tomada em tempo de execução, não em tempo de compilação.

A anotação `@Override` não é obrigatória, mas é **recomendada**: ela informa ao compilador que você pretende sobrescrever um método da superclasse. Se a assinatura não bater com a do pai (ex.: nome diferente, parâmetros diferentes), o compilador gera erro — evitando bugs silenciosos.

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

Aqui não há herança — os três métodos `calcular` coexistem na mesma classe. O compilador escolhe qual chamar com base nos **parâmetros passados** (resolução em tempo de compilação). Essa é a diferença fundamental: **override** muda o comportamento por classe (tempo de execução); **overload** oferece variantes do mesmo nome por parâmetros (tempo de compilação).

> [!tip] Polimorfismo e o princípio Open/Closed
> O polimorfismo por sobrescrita é o mecanismo que torna possível o princípio **Open/Closed** (aberto para extensão, fechado para modificação) — um dos cinco pilares do SOLID. Para adicionar um novo tipo de pagamento (ex.: `PagamentoBoleto`), basta criar uma nova subclasse sem alterar o método `processar`. Esse será o tema da nota sobre [[Principios-SOLID]].

---

## 7. Interface: o contrato

O polimorfismo que acabamos de ver funciona porque cada subclasse sobrescreve um método comum. Mas nem sempre queremos que o código dependa de uma classe concreta — de um "como" específico. Muitas vezes, o que importa é apenas o **o quê**: o *contrato de comportamento* que o objeto promete cumprir. É exatamente isso que a **interface** representa: um **tipo que define um contrato**.

Uma interface declara **o que** um objeto sabe fazer (o comportamento esperado), **sem dizer como** ele faz. Ela é uma lista de compromissos: "quem assumir este contrato deverá, obrigatoriamente, saber executar estas operações". Por isso ela **não é instanciável** — não existe "objeto interface"; existe objeto de uma classe que **implementa** a interface. Quem assume o contrato é a classe, usando a palavra-chave `implements`.

Pense no contexto DATAPREV: um sistema de benefícios precisa validar documentos antes de aceitá-los. Um **CPF** e um **CNS** (Cartão Nacional de Saúde) são documentos diferentes, com regras de validação diferentes. Mas, para quem usa a validação, basta saber que existe uma operação "validar(documento)". O contrato é único; as regras são de cada implementação:

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

Repare na divisão de papéis: a variável `validador` é do tipo da **interface** (`ValidaDocumento`), mas o objeto criado é de uma **classe concreta** (`ValidadorCpf`). O código que usa `validador` sabe apenas que existe um método `validar(...)` — não sabe se a regra por trás é de CPF ou de CNS. Quem decide o comportamento é o objeto real, criado com `new`. Esse é o polimorfismo em ação: o dispatch dinâmico que você viu na seção anterior decide, em tempo de execução, qual `validar()` será chamado.

> [!question] E se amanhã surgir um novo documento?
> Se o INSS passar a exigir a validação do **NIT** (Número de Inscrição do Trabalhador), o que precisa ser alterado? Apenas criar uma nova classe `ValidadorNit implements ValidaDocumento` — ninguém que já usa `ValidaDocumento` muda uma linha. A interface permitiu **estender** o sistema sem **modificar** o que existia. Esse é exatamente o espírito do princípio aberto/fechado (OCP), que você verá com calma no [[Principios-SOLID]].

Agora os pontos que caem em prova:

(a) **`new Interface()` não compila.** Interface não é instanciável — ela é só o contrato. Quem se instancia com `new` é a classe concreta que a implementa.

(b) **Uma classe pode implementar várias interfaces.** O Java não tem herança múltipla de *classes*, mas uma classe pode assumir vários *contratos* ao mesmo tempo (`class X implements A, B`). Não confunda as duas coisas: herança múltipla de classe é proibida; múltiplas implementações de interface são permitidas e corriqueiras.

(c) **Métodos de interface são implicitamente `public abstract`.** Você pode escrever `boolean validar(String documento);` sem os modificadores — o compilador os insere. Ou seja: todo método de interface é público e sem corpo.

(d) **Atributos declarados em interface são implicitamente `public static final`** — isto é, **constantes**. Uma interface pode declarar, por exemplo, `int TAMANHO_CPF = 11;`, e isso vira uma constante única. Consequência importante: interface **não guarda estado** — não há variável de instância que mude de objeto para objeto.

(e) **Menção leve aos default methods (Java 8+):** hoje uma interface pode trazer um método **com corpo** desde que marcado como `default` (ou `static`). Isso foi introduzido para permitir evoluir contratos sem quebrar implementações existentes. Fique atento ao termo, mas não se aprofunde agora — o essencial continua sendo que o método *sem* corpo é a regra.

> [!warning] PEGADINHA — "interface instanciável", "herança múltipla via interface", "atributo que varia por objeto"
> A FGV testa os extremos desses pontos com alternativas aparentemente plausíveis:
> - "Interfaces podem ser instanciadas com `new` desde que tenham métodos default" — **FALSO**. Nenhuma interface é instanciável, com ou sem métodos default.
> - "Uma classe herda de várias classes por meio de interfaces" — **FALSO**. Quem implementa é a classe; interfaces não são classes, e o Java não tem herança múltipla de classe.
> - "Atributos de interface podem variar de objeto para objeto" — **FALSO**. São `public static final` — constantes únicas da interface, não estado de instância.
>
> A pergunta decisiva diante de qualquer alternativa: *estão atribuindo uma característica de classe concreta a uma interface?* Se sim, a alternativa está errada.

---

## 8. Interface vs. classe abstrata: a tabela que cai em prova

Qual usar? A regra prática da banca: **classe abstrata** é para relações "é-um" com estado e implementação compartilhada entre classes **próximas** (uma aposentadoria é um tipo específico de benefício); **interface** é para o **contrato de comportamento ou capacidade** que classes **não relacionadas** podem assumir (um CPF e um CNS não são da mesma família, mas ambos "são validáveis"). Quando a dúvida for "o que as classes têm em comum é estado e código?" → classe abstrata; quando for "o que têm em comum é o que prometem fazer?" → interface.

| Característica | Classe abstrata | Interface |
|---|---|---|
| **Instanciação** | Não é instanciável (`new` não compila) | Não é instanciável (`new` não compila) |
| **Ligação** | Herança única via `extends` | Múltiplas implementações via `implements` |
| **Métodos** | Concretos (com corpo) e abstratos (sem corpo) | Abstratos (sem corpo) — e `default`/`static` com corpo no Java 8+ |
| **Atributos** | Variáveis de instância (estado que varia por objeto) | Apenas constantes `public static final` — não guarda estado |
| **Construtor** | Existe (chamado via `super()` na subclasse) | Não existe |
| **Uso típico** | "É-um" com base comum e código compartilhado | Capacidade/contrato assumido por classes não relacionadas |

> [!warning] PEGADINHA — a FGV adora inverter as características
> O jogo mais comum da banca é **deslocar uma característica de um lado para o outro**: "interface pode ter atributos de instância"; "classe abstrata pode ser implementada com `implements`"; "interface pode ser instanciada". Todas são falsas — e todas parecem plausíveis para quem não fixou a tabela.
> Diante de qualquer alternativa, faça a pergunta decisiva: *essa característica pertence à interface ou à classe abstrata?* Se a frase diz "interface tem construtor" ou "classe abstrata é implementada", a alternativa está errada — marque a que estiver do lado certo.

---

## 9. Visibilidade dos membros — quem vê o quê?

Por trás do encapsulamento está o controle de visibilidade. A FGV cobra os quatro níveis de modificadores de acesso do Java:

| Modificador | Visível na mesma classe | Visível na subclasse | Visível no pacote | Visível fora do pacote |
|---|---|---|---|---|
| `private` | sim | **não** | **não** | **não** |
| *(padrão, sem modificador)* | sim | **não** | sim | **não** |
| `protected` | sim | sim | sim | **não** |
| `public` | sim | sim | sim | sim |

Cada nível abre um círculo a mais de acesso. O `private` é o mais restrito (só a própria classe enxerga); o `public` é o mais aberto (qualquer classe, de qualquer pacote, acessa). No meio, o **padrão** (package-private, sem palavra-chave) permite acesso dentro do mesmo pacote — e o `protected` amplia para a subclasse e o pacote.

A regra do "padrão" é frequentemente esquecida: ele permite acesso dentro do mesmo pacote, mas **não** é herdado pela subclasse se ela estiver em outro pacote. Na prática, `protected` é mais permissivo do que o nome sugere — ele abre para **duas** audiências: subclasses e classes do mesmo pacote.

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
> O `private` **não é herdado** — a subclasse não enxerga o atributo `private` do pai; ela só acessa via métodos públicos ou protegidos. Já o `protected` é herdado e visível na subclasse. Frase clássica de prova: "o membro `private` é acessível na subclasse" — **falso**. E atenção: `protected` é visível **no pacote** também, embora o nome sugira apenas a hierarquia.

---

## 10. Como a FGV cobra este tópico

### Palavras-chave do edital

abstração, encapsulamento, herança, composição, polimorfismo, override, overload, sobrescrita, sobrecarga, `private`, `protected`, `public`, visibilidade, subclasse, superclasse, relação "é-um", relação "tem-um", `extends`, `@Override`, classe abstrata, método abstrato, `abstract`, interface, contrato, `implements`, default method.

A banca explora o tema por vários ângulos:

| Palavra-chave no enunciado | O que está sendo testado |
|---|---|
| "simplificar o modelo" | Abstração |
| "proteger/esconder dados internos" | Encapsulamento |
| "é-um" vs. "tem-um" | Herança vs. composição |
| "mesma assinatura, subclasse" | Sobrescrita (override) |
| "mesmo nome, assinaturas diferentes" | Sobrecarga (overload) |
| `private`, `protected`, `public` | Tabela de visibilidade |
| "membro herdado pela subclasse" | Qual modificador permite herança de acesso |
| "não pode ser instanciada", `abstract` | Classe abstrata |
| "declara o quê, não o como" | Interface |
| "contrato", `implements` | Interface |
| "inverter características" | Interface vs. classe abstrata |

### Padrões de pegadinha

> [!warning] Armadilha 1 — "private é visível na subclasse"
> **Falso.** O modificador `private` restringe o acesso à própria classe. A subclasse herda o campo, mas **não pode acessá-lo diretamente** — só por métodos públicos ou protegidos da superclasse.

> [!warning] Armadilha 2 — "abstração é esconder dados do usuário"
> **Mistura conceitual.** Abstração é **simplificar o modelo**, selecionando quais atributos e comportamentos são relevantes para o domínio. Esconder dados e proteger o estado interno é **encapsulamento**. São coisas distintas.

> [!warning] Armadilha 3 — "sobrecarga reescreve o método da classe pai"
> **Falso.** **Sobrecarga** (overload) cria métodos com o mesmo nome mas assinaturas diferentes **na mesma classe** — sem herança envolvida. **Sobrescrita** (override) é que redefine um método herdado na subclasse, mantendo a mesma assinatura.

> [!warning] Armadilha 4 — "herança sempre promove reutilização"
> **Nem sempre.** A herança promove reutilização, mas também cria acoplamento forte. Quando a reutilização é apenas de código (sem relação "é-um" genuína), composição é preferível. A banca pode oferecer a alternativa "a herança é sempre o melhor mecanismo para reutilizar código" — **falso**.

> [!warning] Armadilha 5 — "protected impede acesso fora da hierarquia"
> **Falso.** `protected` é visível **no pacote** também. Uma classe que não é subclasse, mas está no mesmo pacote, acessa membros `protected` normalmente.

> [!warning] Armadilha 6 — trocar as características entre interface e classe abstrata
> **A armadilha:** a alternativa desloca uma característica de um conceito para o outro — "interfaces podem ter atributos de instância", "classes abstratas podem ser implementadas com `implements`", "interface pode ser instanciada com `new`".
> **O raciocínio errado:** decorar os conceitos separadamente, sem fixar a tabela comparativa — e aceitar a frase porque cada termo ("interface", "atributo") soa familiar.
> **Como se proteger:** não decore frases soltas; decore **a qual conceito pertence cada característica**. Instanciação: **nenhuma** é instanciável. Ligação: classe abstrata usa `extends`; interface usa `implements`. Atributos: classe abstrata tem variáveis de instância; interface só tem constantes `public static final`. Construtor: classe abstrata tem; interface não tem. Se a alternativa cruzar essas colunas, está errada.

> [!warning] Armadilha 7 — "interface instanciável com `new`"
> **A armadilha:** a alternativa afirma que "é possível criar um objeto de uma interface usando `new`" — às vezes justificada por "porque agora existem métodos default".
> **O raciocínio errado:** confundir "a interface tem método com corpo (default)" com "a interface pode ser instanciada".
> **Como se proteger:** em Java, **nenhuma** interface é instanciável — método default dá corpo a um método, mas não transforma a interface em classe concreta. Quem se instancia com `new` é sempre uma **classe** (concreta) que implementa a interface.

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
> A afirmação I está correta — abstração seleciona o que é relevante para o domínio. A afirmação II está **errada** — encapsulamento faz o oposto: protege os atributos com `private`, permitindo acesso apenas por métodos controlados. A afirmação III está **errada** — herança materializa a relação "é-um", não "tem-um" (essa é composição). A afirmação IV está correta — essa é a definição clássica de polimorfismo. A banca costuma inverter os pares: abstração/encapsulamento e herança/composição.

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
> `x` é `private` em `A`, então `B` **não pode acessá-lo diretamente**, mesmo estando no mesmo pacote — `private` restringe à própria classe. `y` é `protected`, visível na subclasse e no pacote. `z` usa o modificador padrão (package-private), visível no pacote — e como `A` e `B` estão no mesmo pacote, é acessível. A linha 1 gera erro; as linhas 2 e 3 funcionam. Se `B` estivesse em pacote diferente, apenas `z` ficaria inacessível — `y` (protected) continua acessível na subclasse, mas `z` (package-private) não viaja entre pacotes.

### Questão 3 — Polimorfismo na prática

> [!example] Enunciado
> Qual das alternativas melhor descreve o que ocorre quando `processar(pagamentoPix)` é chamado, sendo `PagamentoPix extends Pagamento`?
>
> **(A)** O método `calcularValor()` de `Pagamento` é executado, pois `Pagamento` é a classe referenciada.
> **(B)** O método `calcularValor()` de `PagamentoPix` é executado por ser a versão sobrescrita — comportamento decidido em tempo de execução.
> **(C)** O compilador seleciona o método com base no tipo da referência (`Pagamento`), ignorando o tipo real.
> **(D)** O Java executa ambos os métodos (pai e filho) e soma os resultados.
> **(E)** Ocorre erro de compilação, pois `Pagamento` é abstrata.

> [!tip] Gabarito e comentário
> **Resposta: (B)**
> Esse é o comportamento polimórfico por sobrescrita: embora o parâmetro seja do tipo `Pagamento`, o Java chama a versão do objeto real (`PagamentoPix`) em tempo de execução — isso se chama **dispatch dinâmico** (ou late binding). A alternativa A descreveria comportamento estático (o que não ocorre com métodos sobrescritos). A alternativa C descreveria resolução em tempo de compilação, o que vale apenas para sobrecarga, não para sobrescrita. D e E são incorretas conceitualmente.

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
> Métodos de interface são implicitamente públicos e abstratos (sem corpo) — o compilador os insere mesmo que você não escreva os modificadores; atributos de interface são implicitamente `public static final`, ou seja, constantes — por isso a interface não guarda estado. (A) é falsa: nenhuma interface é instanciável, com ou sem métodos default. (B) é falsa: a regra é a declaração `abstract` — qualquer classe abstrata, mesmo só com métodos concretos, não pode ser criada com `new`. (D) é falsa: uma classe pode implementar **várias** interfaces (`implements A, B`) — o que o Java proíbe é herança múltipla de classes. (E) é falsa: a classe abstrata pode — e frequentemente deve — declarar métodos abstratos; é justamente isso que a torna incompleta.

---

## 12. Revisão rápida

| Pilar / Conceito | O que é | Palavra-chave de prova | Erro mais comum em prova |
|---|---|---|---|
| **Abstração** | Modelar só o essencial, ignorar o irrelevante | simplificar, modelo, domínio | Confundir com encapsulamento |
| **Encapsulamento** | Proteger estado interno, acesso por métodos controlados | `private`, getters/setters, validação | Achar que é só "esconder" sem valor |
| **Herança** | Subclasse herda e especializa da superclasse | "é-um", `extends`, sobrescrita | Confundir com composição ("tem-um") |
| **Classe abstrata** | Molde incompleto — não instanciável; pode ter métodos concretos e abstratos | `abstract`, `extends`, método abstrato | Achar que pode ser instanciada se tiver método concreto |
| **Polimorfismo** | Mesma interface, comportamento próprio por classe | override, overload, dispatch dinâmico | Confundir sobrescrita com sobrecarga |
| **Interface** | Contrato de comportamento — declara o "quê" sem o "como"; não instanciável | `implements`, contrato, `public abstract` | Dizer que é instanciável ou que guarda estado |
| **Interface vs. classe abstrata** | Classe abstrata: "é-um" com estado; interface: contrato de capacidade | inverter características | Trocar características de um lado para o outro |
| **Visibilidade** | Controle de acesso: private, padrão, protected, public | `private` não é herdado; `protected` = pacote + subclasse | Achar que `private` é acessível na subclasse |

> [!note] As ideias que resumem a nota
> **1. Cada pilar resolve um problema diferente:** abstração simplifica o modelo, encapsulamento protege o estado, herança promove reutilização e especialização, polimorfismo permite tratamento uniforme com comportamento variado.
> **2. Classe abstrata e interface complementam herança e polimorfismo:** a classe abstrata é herança que obriga a implementar; a interface é polimorfismo por contrato.
> **3. A banca adora inverter:** trocar abstração por encapsulamento, herança por composição, sobrescrita por sobrecarga, e misturar características de interface e classe abstrata. Na hora da questão, pergunte sempre: *estão falando de simplificar (abstração) ou proteger (encapsulamento)? De "é-um" (herança) ou "tem-um" (composição)? Essa característica é de interface ou de classe abstrata?*

---

## 13. Próximos passos

Os quatro pilares — acrescidos de classe abstrata e interface — são a **base** de tudo que vem a seguir. Com eles dominados, você está pronto para os princípios de design que organizam esses pilares em boas práticas:

- [[Principios-SOLID]] — os cinco princípios que orientam código coeso, desacoplado e extensível. O Open/Closed, por exemplo, depende diretamente do polimorfismo por sobrescrita; o ISP (segregação de interfaces) e o DIP (inversão de dependência) exploram o contrato que a interface define.
- [[Clean-Code]] — nomes significativos, funções pequenas, comentários úteis. Os pilares do POO se materializam em código limpo quando aplicados com consciência.

O índice de referência para este tópico é [[Paradigma-Orientado-a-Objetos]].
