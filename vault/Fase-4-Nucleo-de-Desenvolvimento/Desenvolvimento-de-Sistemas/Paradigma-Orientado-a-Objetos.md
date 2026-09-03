# Paradigma Orientado a Objetos

> [!info] Metadados
> **Disciplina:** Desenvolvimento de Sistemas
> **Bloco:** 4.1 — Desenvolvimento de Sistemas (FASE 4 — Núcleo de Desenvolvimento)
> **Tópico:** 1. Paradigma Orientado a Objetos
> **Subtópicos:** Conceitos (classe, objeto, herança, polimorfismo, encapsulamento, abstração) · SOLID (princípios básicos) · Clean Code (nomes significativos, funções pequenas, comentários úteis) · Análise estática de código e SonarQube
> **Pré-requisitos:** [[Raciocinio-Matematico-Aplicado|Raciocínio Lógico Matemático]] (lógica de programação, condicionais, estruturas de dados) e [[Fundamentos-e-Modelagem|Banco de Dados]] (modelagem de entidades e relacionamentos)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-31

---

## 1. Por que estudar o paradigma orientado a objetos?

Esta nota abre o coração do edital. A ementa é explícita: a **FASE 4 — Núcleo de Desenvolvimento** é onde todo o conhecimento anterior converge e onde, estatisticamente, a FGV concentra a maior profundidade do Módulo II. E o ponto de partida desse núcleo é o **paradigma orientado a objetos (POO)** — porque é o modelo mental sobre o qual quase todo software moderno é construído, incluindo praticamente tudo o que a DATAPREV desenvolve.

Pense no seu contexto: a DATAPREV processa dados da seguridade social — o **CNIS** (Cadastro Nacional de Informações Sociais), o INSS digital, sistemas de benefícios, consignação, folha de pagamento de benefícios. Nesses domínios, tratamos de *cidadãos*, *vínculos empregatícios*, *contribuições*, *benefícios*, *órgãos concedentes*. Cada uma dessas "coisas" do mundo real vira um **objeto** no software — e é exatamente aí que o POO se conecta com aquilo que você já estudou na Fase 3.

> [!note] A ponte com o Banco de Dados
> Na [[Fundamentos-e-Modelagem|modelagem conceitual]], você desenhou **entidades** como CLIENTE, PEDIDO e PRODUTO, com atributos e relacionamentos. Pois bem: o POO constrói a aplicação com a mesma visão, mas no código. A **entidade** do banco (uma tabela) e a **classe** do POO (um molde) são leituras do mesmo mundo real. E quando o banco é relacional e o código é orientado a objetos, é preciso de um "tradutor" entre os dois mundos — você verá isso com o **JPA/Hibernate** no tópico 2 desta fase. Guarde essa ponte: *tabela* (banco) e *classe* (objeto) são duas visões da mesma entidade do mundo real.

E por que o [[Raciocinio-Matematico-Aplicado|Raciocínio Lógico Matemático]] é pré-requisito? Porque programar é **aplicar lógica**: condicionais (`se... então`), repetições, representação de conjuntos de dados. O POO é a camada que organiza essa lógica em unidades coerentes chamadas *objetos*. Sem a base lógica, você entende a sintaxe, mas não constrói o raciocínio por trás do design.

> [!question] Pergunta orientadora
> Por que, depois de décadas de programação "procedural" (que apenas seguia uma lista de instruções), a indústria migrou massivamente para um modelo que "embrulha" dados e comportamentos juntos? O que essa "embrulhada" resolve? A seção 2 começa a responder.

---

## 2. Classe e objeto — o molde e a peça

### 2.1 Objeto: a unidade do mundo real

Um **objeto** é a representação, no software, de uma *coisa* do mundo real (ou conceitual) que tem **estado**, **comportamento** e **identidade**:

- **estado:** os dados que o objeto guarda — seus **atributos** (no banco, as *colunas* da tabela);
- **comportamento:** o que o objeto *faz* — seus **métodos** (operações que podem alterar o estado ou produzir resultados);
- **identidade:** o que o torna único, distinguível dos demais objetos da mesma categoria (no banco, a *chave primária*).

Pense num **funcionário** do INSS: seu estado são os atributos `nome`, `CPF`, `matrícula`, `lotação`; seu comportamento são métodos como `calcularSalario()`, `validarVinculo()`, `mudarLotacao()`. Um objeto reúne **o dado e a operação** em uma mesma unidade — essa é a diferença essencial para a programação procedural, onde os dados ficavam em estruturas separadas e as funções operavam sobre elas de fora.

### 2.2 Classe: o molde

Uma **classe** é o **molde** (o *template*, a *planta*) que define os atributos e métodos que os objetos daquela categoria terão. O objeto é a **instância** (o *exemplar*) concreto criado a partir da classe. A analogia clássica de prova:

- a **classe** é a **receita de bolo**; o objeto é o **bolo** assado com ela;
- a classe define *quais* atributos existem; o objeto preenche *quais valores* cada um tem.

```java
// Classe (molde) — define quais atributos e métodos existirão
public class Beneficiario {
    // atributos (estado)
    private String nome;
    private String cpf;
    private double rendaMensal;

    // construtor: cria (instancia) o objeto preenchendo o estado
    public Beneficiario(String nome, String cpf, double rendaMensal) {
        this.nome = nome;
        this.cpf = cpf;
        this.rendaMensal = rendaMensal;
    }

    // método (comportamento)
    public double calcularSextoMergulho(double margem) {
        return this.rendaMensal * (margem / 100.0);
    }
}

// Uso: criar (instanciar) dois objetos a partir da mesma classe
Beneficiario jose = new Beneficiario("José da Silva", "123.456.789-00", 3200.00);
Beneficiario maria = new Beneficiario("Maria Souza", "987.654.321-00", 4100.00);
```

> [!important] Classe vs. objeto
> A **classe** é o molde (definição, abstrato, "um só por categoria"); o **objeto** é a instância concreta (com valores, "vários possíveis"). A FGV adora inverter: dizer que "o objeto é o molde" ou que "a classe é a instância". Pergunte sempre: *é a definição (classe) ou é um exemplar concreto com valores (objeto)?*

Com a classe como molde, podemos agora entender o que significa **abstração** e como ela se conecta aos três outros pilares — **encapsulamento**, **herança** e **polimorfismo**.

---

## 3. Os quatro pilares do POO

### 3.1 Abstração

**Abstração** é a capacidade de **modelar apenas os aspectos relevantes** de uma entidade do mundo real, **ignorando os detalhes que não interessam** ao sistema. No exemplo acima, para o sistema de benefícios, interessa do beneficiário a `rendaMensal` e o `cpf` — mas não, digamos, a cor do cabelo ou a marca do carro. Abstrair é **selecionar o que importa** para o domínio.

> [!warning] PEGADINHA — abstração vs. encapsulamento
> A FGV costuma misturar os termos. **Abstração** é *simplificar*: modelar só o essencial, escondendo a complexidade do que não interessa. **Encapsulamento** é *proteger*: esconder o estado interno do objeto, expondo apenas uma interface controlada. Abstração decide *o que* o objeto representa; encapsulamento decide *como* isso fica protegido. Uma alternativa que diz que abstração é "esconder dados do usuário" está misturando os conceitos.

### 3.2 Encapsulamento

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

Observe o valor didático: o **encapsulamento** não é apenas "esconder"; é **centralizar a validação e a regra de negócio** no próprio objeto. Qualquer outro código que tente atribuir um CPF inválido passa pelo mesmo `setCpf` e é barrado. Sem encapsulamento, cada ponto do sistema validaria seu próprio jeito — e os bugs de consistência se espalhariam.

> [!question] Por que não deixar os atributos públicos?
> Imagine que 10 partes do sistema atribuam CPF diretamente, cada uma com uma validação diferente. Quando a regra muda (ex.: novos dígitos verificadores), é preciso caçar todos os 10 pontos. Com encapsulamento, muda-se **um único método** `setCpf`. A pergunta se responde sozinha: encapsulamento é uma **manutenibilidade** em forma de código.

### 3.3 Herança

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

### 3.4 Herança vs. Composição

A seção 3.3 definiu herança como a relação "é-um". Mas existe outro mecanismo para reutilizar código: a **composição**, relação "tem-um" (*has-a*). A pergunta clássica de prova é: *"deve-se preferir herança ou composição?"* A resposta da banca moderna é **composição antes de herança** — mas para entender por que, é preciso ver os dois lado a lado.

**Composição** significa que uma classe **contém** outra como atributo, em vez de herdar dela. A classe "dono" **delega** o trabalho para o objeto que guarda, em vez de assumir o comportamento como próprio.

#### Exemplo 1 — A mesma ideia, dois caminhos

Imagine um sistema de benefícios da DATAPREV. Um benefício precisa calcular seu valor. Veja como ficaria com herança e com composição:

```java
// ═══════════════════════════════════════════════════
// CAMINHO A — HERANÇA ("é-um")
// ═══════════════════════════════════════════════════
public class CalculoBeneficio {
    protected double valorBase;

    public double calcular() {
        return valorBase;   // comportamento padrão: retorna o valor base
    }
}

public class CalculoAposentadoria extends CalculoBeneficio {
    // herda valorBase e calcular()

    public double calcularComAcrescimo() {
        return calcular() * 1.10;   // acresce 10% sobre o cálculo do pai
    }
}

public class CalculoPensao extends CalculoBeneficio {
    // herda valorBase e calcular()

    public double calcularComDesconto() {
        return calcular() * 0.90;   // desconta 10% sobre o cálculo do pai
    }
}
```

```java
// ═══════════════════════════════════════════════════
// CAMINHO B — COMPOSIÇÃO ("tem-um")
// ═══════════════════════════════════════════════════
// Cada regra de cálculo é uma classe independente
public class RegraAposentadoria {
    public double calcular(double valorBase) {
        return valorBase * 1.10;   // acresce 10%
    }
}

public class RegraPensao {
    public double calcular(double valorBase) {
        return valorBase * 0.90;   // desconta 10%
    }
}

// A classe Beneficio NÃO herda nada — ela TEM UMA regra
public class Beneficio {
    private double valorBase;
    private RegraAposentadoria regra;   // composição: "tem-um"

    public Beneficio(double valorBase) {
        this.valorBase = valorBase;
        this.regra = new RegraAposentadoria();  // cria a regra internamente
    }

    public double getValorFinal() {
        return regra.calcular(valorBase);       // delega o cálculo
    }
}
```

Repare na diferença central: no caminho A, `CalculoAposentadoria` **é um** `CalculoBeneficio` — ela herda `valorBase` e o método `calcular()`. No caminho B, `Beneficio` **não herda** nada — ele apenas **guarda** um objeto `RegraAposentadoria` como atributo e **chama** seu método quando precisa. A `Beneficio` não interessa *como* a regra calcula; ela só pede: "calcule isso para mim".

#### Exemplo 2 — Por que composição é mais flexível

Suponha que amanhã a DATAPREV precise criar uma nova regra: o BPC (Benefício de Prestação Continuada), que não aplica acréscimo nem desconto. Compare o impacto:

```java
// COM HERANÇA: preciso criar uma nova subclasse
public class CalculoBPC extends CalculoBeneficio {
    public double calcularSemAcrescimo() {
        return calcular();   // retorna o valor base sem alteração
    }
}
// Problema: CalculoBPC "é" um CalculoBeneficio — mas e se o cálculo
// do BPC precisar usar dados que NÃO existem em CalculoBeneficio?
// Ex.: dados do Órgão Concedente, que não tem nada a ver com herança.
```

```java
// COM COMPOSIÇÃO: basta criar uma nova classe simples
public class RegraBPC {
    public double calcular(double valorBase) {
        return valorBase;   // BPC não tem acréscimo
    }
}

// E posso usar a mesma regra fora de Beneficio, se precisar:
RegraBPC regra = new RegraBPC();
double valorCalculado = regra.calcular(1412.0);   // funciona sozinha
```

A composição permite **trocar a regra** (de `RegraAposentadoria` para `RegraBPC`) e **reutilizar a regra** em qualquer lugar — algo impossível com herança, que amarra a identidade do objeto à sua árvore genealógica.

#### Exemplo 3 — O problema do acoplamento forte

O perigo real da herança aparece quando a superclasse muda:

```java
// Cenário: herança profunda
public class Pessoa {
    protected String nome;
    protected String cpf;

    public String getNome() { return nome; }
}

public class Servidor extends Pessoa {
    protected String matricula;

    public String getMatricula() { return matricula; }
}

public class ServidorDATAPREV extends Servidor {
    protected String lotacao;
    // herda getNome() de Pessoa e getMatricula() de Servidor
}

// PROBLEMA: se alguém mudar Pessoa.getNome() para retornar
// nome.toUpperCase(), TODAS as subclasses são afetadas:
// Servidor e ServidorDATAPREV passam a retornar nome em maiúsculas,
// sem ter pedido isso.
// E se Pessoa passar a exigir construtor com parâmetro?
// TODOS os filhos quebram — precisam repassar o parâmetro.
```

```java
// COM COMPOSIÇÃO, a mudança é isolada
public class Pessoa {
    private String nome;
    private String cpf;

    public String getNome() { return nome; }
    public String getNomeMaiusculo() { return nome.toUpperCase(); }
}

public class Servidor {
    private Pessoa dadosPessoais;   // guarda uma Pessoa, não herda
    private String matricula;

    public Servidor(String nome, String cpf, String matricula) {
        this.dadosPessoais = new Pessoa(nome, cpf);  // cria internamente
        this.matricula = matricula;
    }

    public String getNome() {
        return dadosPessoais.getNome();   // chama o método que sempre existiu
    }
}
// Se Pessoa mudar para adicionar getNomeMaiusculo(),
// Servidor NÃO é afetado — ele só usa getNome(), que continua igual.
```

#### Resumo: quando usar cada um

| Critério | Herança ("é-um") | Composição ("tem-um") |
|---|---|---|
| Relacionamento | Genuine e estável (`Beneficiario` *é* uma `Pessoa`) | Flexível e trocável (`Beneficio` *tem* uma `RegraAposentadoria`) |
| Acoplamento | **Forte** — filhos dependem da implementação do pai | **Fraco** — depende apenas do método chamado |
| Troca de comportamento | Precisa criar nova subclasse | Basta criar nova classe e injetar |
| Reutilização | Só dentro da hierarquia | Em qualquer contexto |
| Profundidade | Perigosa acima de 2-3 níveis | Não gera hierarquia |

> [!warning] PEGADINHA — FGV inverte a preferência
> A banca pode afirmar: *"É preferível usar herança a composição para promover a reutilização de código"* — **falso**. O princípio moderno é **"prefira composição a herança"** (*Favor Composition Over Inheritance*), defendido por GoF, Joshua Bloch (*Effective Java*) e Robert Martin (*Clean Code*). A única exceção aceita é quando o relacionamento "é-um" é genuíno e estável — como `Beneficiario` *é* uma `Pessoa`. Fora disso, composição é a escolha segura.

> [!note] Conexão com o polimorfismo (seção 3.5)
> Na seção 3.5 você verá como o **polimorfismo** eleva a composição a outro nível: ao definir uma **interface** comum (ex.: `RegraCalculo`), `Beneficio` poderia aceitar *qualquer* regra que implemente essa interface — não apenas `RegraAposentadoria`. Por enquanto, o ponto central é a **estrutura**: herança herda identidade, composição guarda e delega.

### 3.5 Polimorfismo

**Polimorfismo** (do grego, "muitas formas") é a capacidade de **tratar objetos de classes diferentes de maneira uniforme**, através de uma **interface comum**, de modo que cada objeto **responda de forma própria** à mesma chamada. O polimorfismo tem duas faces cobradas:

- **sobrescrita (override):** a subclasse **redefine** um método herdado — cada classe tem sua versão;
- **sobrecarga (overload):** a mesma classe tem **vários métodos com o mesmo nome**, mas assinaturas (parâmetros) diferentes.

#### Sobrescrita (Override) — herança especializa comportamento

**Override** ocorre quando uma **subclasse** redefine um método que herdou da superclasse. A ideia central: a subclasse **já tem** o método (por herança), mas **escolhe** fornecer uma implementação diferente. Para isso, a **assinatura deve ser idêntica** (mesmo nome, mesmos tipos de parâmetros, mesma quantidade).

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

Repare: quem chama `processar` **não sabe** se o pagamento é Pix ou cartão — ele só vê a interface `Pagamento` e chama `calcularValor()`. Cada objeto concreto responde do seu jeito. É a essência do polimorfismo: **mesmo código, comportamento variado conforme o objeto real**.

> [!important] Por que `@Override`?
> A anotação `@Override` não é obrigatória, mas é **recomendada** porque: (1) garante que você realmente está sobrescrevendo (se o método pai mudar de nome, o compilador avisa); (2) torna a intenção explícita no código. Muitas bancas cobram se `@Override` é obrigatório — **não é**, mas é boa prática.

#### Sobrecarga (Overload) — mesma classe, várias "faces"

**Overload** ocorre quando a **mesma classe** possui dois ou mais métodos com o **mesmo nome**, mas **assinaturas diferentes** (tipos, ordem ou quantidade de parâmetros). Isso é útil quando a mesma operação pode receber dados de formatos distintos.

```java
public class CalculadoraBeneficio {

    // Versão 1: recebe valor bruto
    public double calcular(double valor) {
        return valor;
    }

    // Versão 2: recebe valor bruto e percentual de desconto
    public double calcular(double valor, double desconto) {
        return valor * (1 - desconto);
    }

    // Versão 3: recebe valor bruto como String (ex.: importação de legado)
    public double calcular(String valorStr) {
        double valor = Double.parseDouble(valorStr);
        return valor;
    }
}

// Chamadas — o compilador escolhe a versão correta
CalculadoraBeneficio calc = new CalculadoraBeneficio();
calc.calcular(100.0);          // usa versão 1
calc.calcular(100.0, 0.10);   // usa versão 2
calc.calcular("150.0");       // usa versão 3
```

O compilador decide **qual versão chamar** com base nos argumentos fornecidos — isso se chama **resolução de sobrecarga**. Não há relação de herança: todos os métodos vivem na mesma classe.

#### Tabela comparativa: override vs. overload

| Critério | Override (sobrescrita) | Overload (sobrecarga) |
|---|---|---|
| **Relação entre classes** | Superclasse ↔ Subclasse | Mesma classe |
| **Assinatura** | Idêntica (mesmo nome, mesmos parâmetros) | Diferente (mesmo nome, parâmetros distintos) |
| **Anotação** | `@Override` (recomendada) | Nenhuma |
| **Polimorfismo?** | Sim — é a base do polimorfismo dinâmico | Não — é resolvido em **compilação** |
| **Quem decide qual método executar?** | O **tipo do objeto** em tempo de execução | O **compilador**, em tempo de compilação |

> [!warning] PEGADINHA CLÁSSICA — FGV troca os pares
> Banca afirma: *"Sobrecarga (overload) é quando a subclasse redefine um método da superclasse"* — **falso**. Isso é sobrescrita (override). Outra frase comum: *"Override permite múltiplos métodos com o mesmo nome e assinaturas diferentes"* — **falso**. Isso é overload. O truque da FGV é trocar os nomes dos conceitos.

> [!tip] Regra de ouro para não confundir
> **Override** = herança + assinatura igual → **redefinir comportamento herdadado**.
> **Overload** = mesma classe + assinatura diferente → **variar a entrada da mesma operação**.

> [!tip] Por que o polimorfismo é a base das boas arquiteturas?
> É o polimorfismo que permite escrever uma regra genérica ("processe o pagamento") sem `if` gigantes para cada tipo. O código fica **aberto para extensão** (basta criar uma nova subclasse `PagamentoBoleto` sem alterar `processar`) — e isso é exatamente o princípio Open/Closed do SOLID que veremos na seção 6.

### 3.6 Visibilidade dos membros

Por trás do encapsulamento está o controle de visibilidade. A FGV cobra os quatro níveis:

| Modificador | Visível na mesma classe | Visível no pacote | Visível na subclasse | Visível fora do pacote |
|---|---|---|---|---|
| `public` | sim | sim | sim | sim |
| `protected` | sim | sim | sim | **não** |
| *(padrão, sem modificador)* | sim | sim | **não** | **não** |
| `private` | sim | **não** | **não** | **não** |

> [!warning] PEGADINHA — `protected` e o `private`
> O `private` **não é herdado** (a subclasse não enxerga o atributo `private` do pai — ela só acessa via métodos públicos/protegidos). Já o `protected` é herdado e visível na subclasse. Frase clássica de prova: "o membro `private` é acessível na subclasse" — **falso**. E atenção: `protected` é visível **no pacote** também, embora o nome sugira só a hierarquia.

### 3.7 Interface vs. Abstract Class

Na seção 3.3 você viu que **herança** cria uma relação "é-um": `Beneficiario` *é* uma `Pessoa`. Na seção 3.5, o **polimorfismo** mostrou que podemos tratar objetos diferentes de forma uniforme, desde que compartilhem uma *interface comum*. Mas que tipo de "contrato" define essa interface comum? Em Java, existem dois mecanismos para isso: a **interface** e a **classe abstrata** (*abstract class*). Ambas servem para definir *o que* uma classe deve fazer, mas diferem radicalmente em *quanto* elas podem dizer sobre *como*.

> [!note] O que é um "contrato" em tecnologia?
> Sempre que você ler "contrato" (ou "especificação", "interface") em tecnologia, pense em uma pergunta simples: *o que cada lado pode esperar do outro?* O **contrato** é um acordo formal sobre o **que** algo deve fazer — separado de **como** isso é feito (a **implementação**). Em POO, a interface é o contrato (define *quais* métodos existem) e a classe concreta é a implementação (fornece o *código*). Essa mesma lógica reaparece em vários pontos do curso: **JPA** é a especificação/contrato e **Hibernate** a implementação; **WSDL/XSD** descreve o contrato de um Web Service e o **SOAP** transporta as mensagens. Quem depende do contrato fica livre para trocar a implementação sem reescrever nada — é exatamente essa flexibilidade que o **polimorfismo** (seção 3.5) e o DIP (seção 6.5) exploram.

#### Interface — contrato puro

Uma **interface** é um **contrato completamente abstrato**: ela define *quais métodos* existem, mas **não implementa** como eles funcionam (com exceção dos métodos `default` e `static`, introduzidos no Java 8). Quando uma classe "implementa" uma interface, ela se compromete a fornecer o código de *todos* os métodos abstratos — caso contrário, não compila.

Pense numa interface como o **regulamento de um concurso**: ele diz "o candidato deve provar conhecimentos em X, Y e Z", mas não ensina o conteúdo. Cada candidato (classe) decide *como* se preparar (implementar).

```java
// Interface — contrato puro: o QUE fazer
public interface CalculoBeneficio {
    double calcularValor(double valorBase);
    boolean ehElegivel(Beneficiario b);
}

// Uma classe concreta implementa o contrato
public class CalculoAposentadoria implements CalculoBeneficio {

    @Override
    public double calcularValor(double valorBase) {
        // Regra específica: aposentadoria pode incluir abono anual
        return valorBase + (valorBase * 0.08);
    }

    @Override
    public boolean ehElegivel(Beneficiario b) {
        return b.getIdade() >= 65 && b.getContribuicoes() >= 180;
    }
}

// Outra classe implementa o mesmo contrato de forma diferente
public class CalculoPensao implements CalculoBeneficio {

    @Override
    public double calcularValor(double valorBase) {
        // Pensão não inclui abono — retorna o valor base
        return valorBase;
    }

    @Override
    public boolean ehElegivel(Beneficiario b) {
        return b.getFalecido() != null && b.getDependentes() > 0;
    }
}
```

Note a consequência: o código que *usa* o cálculo não precisa saber se é aposentadoria ou pensão. Ele chama `calcularValor` na interface e recebe a resposta correta — é o polimorfismo em ação.

#### Classe abstrata — contrato parcial

Uma **classe abstrata** é um **contrato misto**: ela pode definir *quais métodos* existem (abstratos) **e também implementar** parte do comportamento (métodos concretos). Pode ter **atributos de estado**, **construtores** e **métodos com corpo completo**. A classe abstrata é usada quando existe uma **implementação parcial compartilhada** entre classes filhas — ou seja, quando parte do comportamento é igual para todas, mas parte varia.

A analogia é um **formulário padrão** com campos preenchidos e campos em branco: os campos preenchidos são os métodos concretos; os em branco são os abstratos que cada subclasse deve preencher.

```java
// Classe abstrata — contrato parcial: o QUE + parte do COMO
public abstract class BeneficioBase {
    protected double valorBase;
    protected String tipoBeneficio;

    // Construtor — interfaces NÃO podem ter
    public BeneficioBase(double valorBase, String tipoBeneficio) {
        this.valorBase = valorBase;
        this.tipoBeneficio = tipoBeneficio;
    }

    // Método concreto — compartilhado por todas as subclasses
    public double calcularIRRF(double valor) {
        // Regra comum de imposto de renda sobre benefício
        if (valor > 2815.00) {
            return valor * 0.275;
        }
        return 0.0;
    }

    // Método concreto utilitário
    public String formatarValor(double valor) {
        return String.format("R$ %.2f", valor);
    }

    // Método abstrato — cada filho DEVE implementar
    public abstract double calcularBeneficio();
}
```

As subclasses herdam tudo e precisam implementar apenas o que falta:

```java
public class Aposentadoria extends BeneficioBase {

    public Aposentadoria(double valorBase) {
        super(valorBase, "APOSENTADORIA");
    }

    @Override
    public double calcularBeneficio() {
        double bruto = valorBase * 1.08;   // inclui abono anual
        double irrf = calcularIRRF(bruto); // reutiliza método do pai
        return bruto - irrf;
    }
}

public class Pensao extends BeneficioBase {

    public Pensao(double valorBase) {
        super(valorBase, "PENSAO");
    }

    @Override
    public double calcularBeneficio() {
        double bruto = valorBase;          // sem abono
        double irrf = calcularIRRF(bruto);
        return bruto - irrf;
    }
}
```

Observe que `Aposentadoria` e `Pensao` **reutilizam** o `calcularIRRF` e o `formatarValor` do pai — código duplicado é eliminado, sem criar um novo construtor para cada regra de cálculo. A classe abstrata faz o meio-termo entre interface pura e classe concreta.

#### Tabela comparativa

| Critério | `interface` | `abstract class` |
|---|---|---|
| **Palavra-chave** | `interface` | `abstract class` |
| **Múltipla herança de contrato** | **Sim** — uma classe pode implementar várias interfaces | **Não** — uma classe pode herdar de uma única classe abstrata |
| **Construtor** | **Não** — não pode ter construtor | **Sim** — pode ter construtor (invocado com `super()`) |
| **Atributos de estado** | **Não** — apenas `public static final` (constantes) | **Sim** — pode ter atributos com `private`, `protected`, etc. |
| **Métodos concretos** | Só `default` (instância) e `static` (classe), desde Java 8 | Sim — métodos com corpo completo |
| **Métodos abstratos** | Sim — todos são abstratos por padrão | Sim — marcados com `abstract` |
| **Quando usar** | Quando é preciso definir um **contrato puro** — o QUE fazer, sem impor implementação | Quando existe **comportamento compartilhado** — o QUE + parte do COMO |

> [!important] A regra de ouro
> Use **interface** quando quiser definir um *contrato* que qualquer classe pode implementar, independentemente de sua hierarquia. Use **classe abstrata** quando quiser *reutilizar código concreto* entre classes que compartilham uma estrutura comum. A pergunta-chave é: *existe código concreto que se repete entre as subclasses?* Se sim, `abstract class`. Se não, `interface`.

#### PEGADINHAS FGV clássicas

> [!warning] "Interface pode ter atributos?"
> **Sim, mas com restrição.** Todo atributo em uma interface é implicitamente `public static final` — ou seja, uma **constante**. Não existe atributo de estado (variável de instância) em interface. A banca adora perguntar: *"Uma interface pode conter atributos?"* — a resposta correta é **sim**, mas eles são constantes. Se a alternativa disser "sim, variáveis de instância", é falso.

> [!warning] "Interface pode ter construtor?"
> **Não.** Interfaces não podem ser instanciadas — você não faz `new CalculoBeneficio()` porque `CalculoBeneficio` é uma interface. Sem instanciação, não faz sentido ter construtor. A alternativa que diz "interfaces podem ter construtores" está errada.

> [!warning] "Uma classe pode implementar várias interfaces?"
> **Sim.** Essa é a "múltipla herança de contrato": `class CalculoAposentadoria implements CalculoBeneficio, Serializable, Comparable<Beneficiario>` — perfeitamente válido. O que **não** se pode fazer é herdar de múltiplas classes (`extends ClasseA, ClasseB` — compilação falha). A FGV troca os termos: "uma classe pode herdar de múltiplas classes" (**falso**) vs. "uma classe pode implementar múltiplas interfaces" (**verdadeiro**).

> [!warning] "Classe abstrata pode ter construtor?"
> **Sim.** O construtor de uma classe abstrata não pode ser chamado diretamente com `new`, mas é invocado pelas subclasses via `super()`. O construtor existe para inicializar atributos comuns. A banca tenta confundir: "como classe abstrata não pode ser instanciada, ela não pode ter construtor" — raciocínio falso, porque o construtor serve para as *filhas*, não para instanciar a abstrata diretamente.

#### Conexão com SOLID

O uso correto de interfaces conecta diretamente com dois princípios vistos na seção 6:

O **ISP** (seção 6.4) — Interface Segregation Principle — recomenda que interfaces sejam **pequenas e específicas**. Em vez de criar uma única `InterfaceBeneficio` com 15 métodos (cálculo, notificação, relatório, auditoria), o ISP orienta a dividir em `CalculoBeneficio`, `NotificacaoBeneficio` e `AuditoriaBeneficio`. Assim, quem só precisa calcular não é obrigado a implementar métodos de notificação — reduzindo acoplamento e código morto.

O **DIP** (seção 6.5) — Dependency Inversion Principle — afirma que módulos de alto nível devem depender de **abstrações** (interfaces), não de **implementações concretas**. No contexto DATAPREV, um serviço de concessão de benefícios não deveria dizer `CalculoAposentadoria calc = new CalculoAposentadoria()`. Em vez disso, deveria receber um `CalculoBeneficio` via construtor (injeção de dependência) — e só descobriria qual implementação concreta usar no momento da configuração. Isso permite trocar a regra de cálculo sem alterar quem a usa.

> [!note] A ponte entre seções
> A interface `CalculoBeneficio` é exatamente o tipo de abstração que o DIP (seção 6.5) defende: quem *usa* o cálculo depende do *contrato*, não da *implementação concreta*. E o ISP (seção 6.4) garante que esse contrato não fique inchado com métodos que nem todos precisam implementar. Interface e classe abstrata são, portanto, as *ferramentas de implementação* dos princípios SOLID — não apenas conceitos soltos.

> [!tip] Resumo para revisão rápida
> **Interface** = contrato puro, sem construtor, sem estado, múltipla herança de contrato.
> **Classe abstrata** = contrato parcial, com construtor, com estado, herança simples.
> **A pergunta da prova:** *existe código concreto compartilhado entre as subclasses?* Sim → `abstract class`. Não → `interface`.

---

## 4. A relação entre POO e o mundo dos dados

Antes de avançar para SOLID, vale consolidar a conexão com o Banco de Dados, pois ela reaparecerá nos tópicos 2, 4 e 5 desta fase. A referência para [[Fundamentos-e-Modelagem|modelagem]] de dados é a ponte entre os dois mundos:

| Mundo do banco (modelagem) | Mundo do POO (código) |
|---|---|
| Entidade (conceitual) / tabela (lógico) | Classe |
| Ocorrência / tupla (linha) | Objeto |
| Coluna | Atributo |
| Chave primária | Identidade (e o campo `id`) |
| Relacionamento 1:N / N:M | Referência entre objetos / coleções |
| Regra de negócio no banco (constraint/trigger) | Regra nos métodos da classe |

Essa tabela é, na prática, o "mapa do tesouro" da próxima nota: quando estudarmos **JPA/Hibernate**, veremos como essa ponte é automatizada com as anotações de mapeamento — cada *entidade Java* vira uma *tabela*, cada *objeto* vira uma *linha*.

---

## 5. Princípios de Clean Code

O edital pede **Clean Code** de forma conceitual — três subitens: **nomes significativos, funções pequenas e comentários úteis**. A FGV costuma cobrar como asserções verdadeiras/falsas ou como "o que NÃO é Clean Code".

### 5.1 Nomes significativos

O código é lido muito mais vezes do que é escrito — por outros desenvolvedores e pelo próprio autor no futuro. Por isso, **nomes devem revelar a intenção**. Um nome bom dispensa comentários explicativos.

```java
// RUIM — nomes enigmáticos
int d;             // o que é d? dias?
double v;          // valor? de quê?

// BOM — nomes revelam a intenção
int diasDesdeUltimaConsulta;
double limiteDeMargemConsignavel;
```

Regras favoritas da banca: nomes **descritivos**, que respondam *o quê* e *por quê*, e não *como*; nomes de **métodos devem ser verbos** (`calcularSalario()`, `emitirExtrato()`); nomes de **classes devem ser substantivos** (`Beneficiario`, `EmprestimoConsignado`); evitam-se abreviações obscuras e termos sem significado. Acontece também o princípio do **CamelCase** (que já apareceu na nota de [[Estrutura-Morfossintatica|Português]] como parte do vocabulário técnico).

### 5.2 Funções pequenas

Funções pequenas defendem que **uma função deve fazer uma única coisa, e bem feita**. Funções gigantes que fazem dez coisas ao mesmo tempo são difíceis de entender, de testar e de reutilizar. Um bom indicador: se você precisa de um comentário para explicar o que uma parte da função faz, essa parte provavelmente deveria ser **extraída para outra função** (refatoração — conceito que será aprofundado na fase de metodologias).

```java
// RUIM — função que faz várias coisas
public void processarBeneficio(Beneficiario b) {
    // valida
    if (b.getCpf() == null) throw new IllegalArgumentException();
    // calcula
    double valor = b.getRendaMensal() * 0.30;
    // formata e envia
    String msg = "Seu benefício é " + formatar(valor);
    enviarEmail(b.getEmail(), msg);
}

// MELHOR — uma função, uma responsabilidade
public void processarBeneficio(Beneficiario b) {
    validar(b);
    double valor = calcularValor(b);
    notificar(b, valor);
}
```

### 5.3 Comentários úteis

Um dos princípios do Clean Code é que o **código bem nomeado não precisa de comentários explicativos** — o código deve se explicar sozinho. Mas existem comentários **úteis**: os que explicam o **porquê** (a lógica de negócio por trás de uma decisão), números mágicos, ou o **contexto** de um trecho complexo.

```java
// RUIM — comenta o óbvio (o código já diz isso)
int x = 0;      // seta x para zero

// ÚTIL — explica o "porquê", que o código não revela
// Margem consignável de 30% conforme Resolução INSS nº 100/2021
final double MARGEM_CONSIGNAVEL = 0.30;
```

> [!warning] PEGADINHA — o que Clean Code diz sobre comentários
> A pergunta favorita da banca: *"o Clean Code recomenda eliminar todos os comentários?"* **Não.** Ele recomenda que os **comentários dispensáveis** (os que repetem o código ou explicam o óbvio) sejam removidos, e que o código **seja expressivo o bastante para reduzir a dependência de comentários**. Comentários que explicam *regras de negócio* ou *decisões de design* são bem-vindos. A pegadinha é tornar a recomendação em proibição absoluta.

### 5.4 Análise estática de código e SonarQube

Os princípios de Clean Code — nomes significativos, funções pequenas, comentários úteis — são orientações *manuais* para escrever código limpo. Mas na prática, em um time de desenvolvimento com dezenas de milhares de linhas de código, confiar apenas na revisão visual de cada programador é insuficiente. É aí que entra a **análise estática de código**: ferramentas que examinam o **código-fonte sem executá-lo**, procurando automaticamente problemas de qualidade, *code smells* (sinais de que algo está mal no código), bugs potenciais e violações de boas práticas.

A ideia é simples: assim como um corretor ortográfico verifica um texto sem precisar publicá-lo, um analisador estático verifica o código sem precisar compilá-lo ou rodá-lo — ele lê a estrutura, os padrões e as convenções e aponta desvios. Quando o código viola uma regra (por exemplo, uma classe com mais de mil linhas, uma função que faz cinco coisas, ou um nome de variável incompreensível), a ferramenta gera um alerta classificado por severidade.

O edital menciona especificamente o **SonarQube** como ferramenta de análise estática. O SonarQube é uma plataforma *open source* de **análise estática contínua** da qualidade do código. Ele se integra ao fluxo de desenvolvimento (CI/CD, repositório Git) e, a cada compromisso (*commit*) ou construção (*build*), analisa o código e gera um relatório com:

- **Bugs** potenciais detectados no fluxo lógico;
- **Code smells** — trechos que funcionam mas violam boas práticas (funções longas, nomes ruins, complexidade excessiva, duplicação);
- **Duplicação de código** — trechos idênticos ou muito similares repetidos em vários arquivos;
- **Métricas de qualidade** — cobertura de testes (qual percentual do código é exercitado por testes), complexidade ciclomática, linhas de código.

O SonarQube materializa o Clean Code em **regras automatizadas**: ele detecta automaticamente nomes que não revelam intenção, funções com complexidade alta demais, comentários desnecessários que apenas repetem o código, e código duplicado. Quando a nota de Clean Code diz que "funções devem fazer uma coisa só", o SonarQube traduz isso em uma regra que aponta funções com múltiplas responsabilidades. Quando Clean Code diz "nomes devem ser significativos", o SonarQube alerta sobre variáveis com nomes genéricos como `x`, `d` ou `aux`.

> [!tip] Quality Gate
> Uma funcionalidade central do SonarQube é o **Quality Gate** (portão de qualidade): uma regra configurável que define o *limite mínimo aceitável* de qualidade para que o código seja aceito. Por exemplo: "nenhum bug novo", "no máximo 3% de duplicação", "cobertura mínima de 80%". Se o código não passa no Quality Gate, o *pipeline* de entrega pode ser bloqueado — ou seja, o código **não é liberado** enquanto não atender aos critérios de qualidade. É uma forma de **governança de qualidade** no desenvolvimento.

> [!warning] PEGADINHA — análise estática vs. análise dinâmica
> Essa é uma armadilha conceitual recorrente. **Análise estática** examina o código **sem executá-lo** — ela lê o código-fonte e procura problemas estruturais, padrões ruins e violações de convenções. **Análise dinâmica** examina o software **durante a execução** — ela roda o programa e observa comportamento em tempo real (por exemplo, consumo de memória, erros em tempo de execução, comportamento inesperado em cenários reais). O SonarQube é uma ferramenta de **análise estática**: ele não precisa rodar o programa para encontrar problemas. Não confunda os dois conceitos — a banca adora inverter: "SonarQube é uma ferramenta de análise dinâmica" — **falso**.

> [!question] Por que a análise estática conecta com Clean Code?
> Clean Code é um *conjunto de princípios* (nomes claros, funções coesas, comentários úteis). A análise estática é o *mecanismo* que verifica se esses princípios estão sendo seguidos na prática, de forma automática e contínua. Um time que defende Clean Code mas não usa análise estática depende apenas da disciplina individual — e a história mostra que isso não escala. O SonarQube é o "fiscal" que garante que os princípios sejam cumpridos mesmo em projetos grandes, com muitos colaboradores.

**Palavras-chave do edital:** *análise estática*, *code smell*, *qualidade de código*, *quality gate*, *SonarQube*, *bugs*, *duplicação*.

---

## 6. SOLID — os cinco princípios

**SOLID** é um acrônimo mnemônico para cinco princípios de design orientado a objetos, que orientam a construção de código **coeso, desacoplado, extensível e fácil de manter**. O edital pede os "princípios básicos" — e a FGV quase sempre cobra a **definição** de cada um, além da diferença entre letras que se confundem (S, D, L). Vamos a cada um com violação e correção.

### 6.1 S — Single Responsibility Principle (SRP, Princípio da Responsabilidade Única)

> **Uma classe deve ter um único motivo para mudar** — ou seja, deve ter **uma única responsabilidade**.

Quando uma classe faz duas coisas distintas, uma mudança em uma delas força a reescrita da outra — acoplamento desnecessário.

```java
// VIOLAÇÃO — a classe cuida do cálculo E do envio de email (duas responsabilidades)
public class Beneficio {
    public double calcularValor(double renda, double margem) { ... }
    public void enviarEmail(Beneficiario b, double valor) { ... }   // responsabilidade alheia
}

// CORREÇÃO — cada responsabilidade em sua classe
public class CalculoBeneficio {
    public double calcular(double renda, double margem) { ... }
}

public class NotificacaoBeneficio {
    public void enviar(Beneficiario b, double valor) { ... }
}
```

> [!warning] PEGADINHA — SRP vs. "uma classe faz uma única coisa"
> O SRP **não** significa "uma classe tem um único método" nem "uma classe faz uma única operação elementar". Significa que ela tem **um único motivo para mudar** — uma única *responsabilidade* no sentido de *razão de ser alterada*. Uma classe `Beneficiario` pode ter vários métodos (`calcularRegra`, `validarCpf`, `listarDependentes`) e ainda assim ter responsabilidade única (representar o beneficiário). A pegadinha é reduzir o SRP a "uma função só".

### 6.2 O — Open/Closed Principle (OCP, Princípio Aberto/Fechado)

> **As entidades devem estar abertas para extensão, mas fechadas para modificação.**

Ou seja: você deve poder **adicionar** novos comportamentos (aberto para extensão) **sem modificar** o código existente (fechado para modificação). O polimorfismo (seção 3.4) é o mecanismo que torna isso possível.

```java
// VIOLAÇÃO — cada tipo novo exige um novo "if" e modifica a classe
public class Desconto {
    public double aplicar(double valor, String tipo) {
        if (tipo.equals("PIX")) return valor * 0.95;
        if (tipo.equals("CARTAO")) return valor * 1.03;
        // novo tipo => novo if => modificação da classe
        return valor;
    }
}

// CORREÇÃO — aberto para extensão via herança/polimorfismo
public interface RegraDesconto {
    double aplicar(double valor);
}

public class DescontoPix implements RegraDesconto {
    public double aplicar(double valor) { return valor * 0.95; }
}

public class DescontoCartao implements RegraDesconto {
    public double aplicar(double valor) { return valor * 1.03; }
}

// Para adicionar um novo tipo, basta criar uma nova classe que implemente
// RegraDesconto — sem tocar no código existente.
```

### 6.3 L — Liskov Substitution Principle (LSP, Princípio da Substituição de Liskov)

> **Se uma classe S é uma subclasse de T, então objetos de T devem poder ser substituídos por objetos de S sem quebrar o programa.**

Em outras palavras: a subclasse deve ser **substituível** pela superclasse — a herança não deve violar o contrato do pai.

```java
// VIOLAÇÃO — o Pato de borracha "é um" Pato, mas não nada
public class Pato { public void nadar() { } }
public class PatoDeBorracha extends Pato {
    @Override
    public void nadar() { throw new UnsupportedOperationException(); }
}
// Quem confia que "todo Pato nada" quebra ao receber um PatoDeBorracha.

// SOLUÇÃO — separar responsabilidades; nem todo "pato" nada
```

O exemplo clássico é o **retângulo/quadrado**: um Quadrado "é um" Retângulo, mas alterar a largura do quadrado deveria afetar também a altura, quebrando o comportamento esperado do Retângulo. A FGV gosta de cobrar o LSP dizendo "a herança deve permitir substituir a classe base pela derivada sem alterar o comportamento correto" — e a resposta errada inverte ou distorce essa ideia.

### 6.4 I — Interface Segregation Principle (ISP, Princípio da Segregação de Interfaces)

> **As interfaces devem ser específicas do cliente; nenhum cliente deve depender de métodos que não utiliza.**

Interfaces "gorduchas" (com muitos métodos) obrigam implementadores a implementar/usar o que não precisam. O ideal é **dividir** em interfaces menores e mais focadas.

```java
// VIOLAÇÃO — interface única e inchada
public interface Funcionario {
    void baterPonto();
    void programar();
    void gerenciarEquipe();
}
// Um programador precisaria implementar gerenciarEquipe (e vice-versa)

// CORREÇÃO — interfaces específicas
public interface RegistroPonto { void baterPonto(); }
public interface Desenvolvedor { void programar(); }
public interface Gestor { void gerenciarEquipe(); }
```

### 6.5 D — Dependency Inversion Principle (DIP, Princípio da Inversão de Dependência)

> **Módulos de alto nível não devem depender de módulos de baixo nível; ambos devem depender de abstrações. Abstrações não devem depender de detalhes; detalhes devem depender de abstrações.**

Em termos simples: o código deve depender de **interfaces/abstrações** (o "contrato"), e não de **implementações concretas** (o "como"). Isso permite trocar a implementação sem mexer em quem a usa — e é a base da **Injeção de Dependência**, que veremos a fundo nos tópicos de Spring (tópico 4).

```java
// VIOLAÇÃO — a classe alta depende diretamente de uma implementação concreta
public class EmissorRelatorio {
    private BancoPostgres banco = new BancoPostgres();   // acoplamento rígido
}

// CORREÇÃO — depende de uma abstração (interface)
public interface RepositorioDados { List<Registro> buscar(); }

public class RepositorioPostgres implements RepositorioDados { ... }
public class RepositorioCache implements RepositorioDados { ... }

public class EmissorRelatorio {
    private RepositorioDados repositorio;   // depende da abstração
    public EmissorRelatorio(RepositorioDados r) { this.repositorio = r; }
}
```

> [!note] Os cinco em uma frase — para revisão rápida
> **S** = uma responsabilidade por classe · **O** = aberto a extensão, fechado a modificação · **L** = subclasse substituível pela superclasse · **I** = interfaces específicas, não inchadas · **D** = dependa de abstrações, não de concretos. A tendência de prova da FGV é dar a definição e trocar as letras entre as alternativas — decore cada letra com sua frase.

---

## 7. Como a FGV cobra este tópico

- **Pilares do POO:** quase sempre por definição e distinção. Guarde os pares que se confundem: **abstração** (simplificar o modelo) vs. **encapsulamento** (esconder/proteger dados); **herança** (é-um) vs. **composição** (tem-um); **sobrescrita** (redefinir, override) vs. **sobrecarga** (mesmo nome, assinaturas diferentes, overload).
- **Classe vs. objeto:** a pegadinha do molde vs. a peça concreta.
- **Visibilidade:** a tabela da seção 3.5 — principalmente que `private` **não** é visto pela subclasse e que `protected` é visível no pacote.
- **SOLID:** definição de cada princípio; a FGV troca as definições entre as letras. Lembre que o edital pede "princípios básicos" — profundidade conceitual, não decoreba de casos.
- **Clean Code:** nomes significativos, funções pequenas (uma coisa por função), comentários *úteis* (explicam o "porquê", não o "como" óbvio). **Análise estática:** SonarQube como ferramenta que examina o código sem executá-lo; code smells, quality gate.
- **Contexto DATAPREV:** sistema previdenciário → entidades como `Beneficiario`, `Beneficio`, `EmprestimoConsignado`, `Vinculo` — use esse vocabulário nos exemplos físicos da prova.

> [!warning] PEGADINHA — "o POO elimina a lógica condicional"
> A banca costuma oferecer uma alternativa que diz que "o POO elimina a necessidade de lógica condicional". **Falso** — o POO *organiza* a lógica em objetos e pode *reduzir* `if`s por meio de polimorfismo, mas não elimina a lógica de programação (que exige a base de [[Raciocinio-Matematico-Aplicado|RLM]]). Seja cético com afirmações absolutas.

---

## 8. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **Objeto** = estado (atributos) + comportamento (métodos) + identidade; **classe** = molde
> - [ ] **Abstração** = modelar só o essencial; **encapsulamento** = proteger/esconder o estado com interface controlada
> - [ ] **Herança** = "é-um"; composição = "tem-um"; **prefira composição a herança** quando possível
> - [ ] **Polimorfismo** = mesma interface, comportamento próprio por classe; **sobrescrita** (override) ≠ **sobrecarga** (overload)
> - [ ] Visibilidade: `private` (classe), padrão (pacote), `protected` (pacote + subclasse), `public` (todos); `private` **não é herdado**
> - [ ] **Clean Code**: nomes significativos, funções pequenas (uma coisa só), comentários *úteis* (o "porquê")
> - [ ] **Análise estática** (SonarQube): examina código *sem executá-lo*; detecta code smells, bugs, duplicação; Quality Gate define limites mínimos de qualidade
> - [ ] **SOLID**: S (responsabilidade única), O (aberto/fechado), L (substituição de Liskov), I (segregação de interfaces), D (inversão de dependência)
> - [ ] Ponte com [[Fundamentos-e-Modelagem|banco de dados]]: tabela ↔ classe, linha ↔ objeto, coluna ↔ atributo — base do JPA do tópico 2

> [!warning] O erro mais comum em prova
> Confundir **abstração com encapsulamento** e **herança com composição**, e reduzir o **SRP** a "uma função só". Na hora da questão: *a frase fala em simplificar o modelo (abstração) ou em esconder/proteger dados (encapsulamento)?* E *a relação é "é-um" (herança) ou "tem-um" (composição)?*

---

## 9. Próximos passos

Você acaba de construir o alicerce conceitual de toda a FASE 4: sabe distinguir classe de objeto, domina os quatro pilares, entende o SOLID, os princípios de Clean Code e como a análise estática com SonarQube verifica esses princípios na prática. Esse vocabulário será usado em todos os tópicos seguintes — nos **padrões de projeto** (tópico 5), que são soluções prontas construídas sobre esses princípios, e no **ecossistema Spring** (tópico 4), que aplica a inversão de dependência em escala.

Antes disso, o próximo tópico da ementa é **Java e o Ecossistema JVM**: é lá que esses conceitos se transformam em código concreto — tipos, coleções e exceções da linguagem, e depois as tecnologias empresariais como **JPA e Hibernate** que fazem a ponte com o banco de dados que você estudou na Fase 3. Se o POO é a *filosofia*, o Java é a *linguagem* em que essa filosofia se materializa — e é exatamente isso que a próxima nota desenvolve.
