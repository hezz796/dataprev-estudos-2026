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

> [!warning] PEGADINHA — herança vs. composição
> A pergunta clássica de prova: *"deve-se preferir herança ou composição?"* A resposta favorita da banca moderna é **favorável à composição** ("**prefira composição a herança**" — é um princípio defendido pela comunidade, inclusive por autores de Clean Code). Composição é a relação "tem-um" (um `Carro` *tem* um `Motor`), enquanto herança é "é-um" (um `Carro` *é* um `Veículo`). Herança cria um **acoplamento forte** entre as classes (mudar o pai afeta todos os filhos) e pode gerar hierarquias rígidas; composição é mais flexível. Quando a prova perguntar qual princípio orienta o design atual, a tendência é: **composição antes de herança**, exceto quando a "é-um" for genuína e estável.

### 3.4 Polimorfismo

**Polimorfismo** (do grego, "muitas formas") é a capacidade de **tratar objetos de classes diferentes de maneira uniforme**, através de uma **interface comum**, de modo que cada objeto **responda de forma própria** à mesma chamada. O polimorfismo tem duas faces cobradas:

- **sobrescrita (override):** a subclasse **redefine** um método herdado — cada classe tem sua versão;
- **sobrecarga (overload):** a mesma classe tem **vários métodos com o mesmo nome**, mas assinaturas (parâmetros) diferentes.

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

> [!tip] Por que o polimorfismo é a base das boas arquiteturas?
> É o polimorfismo que permite escrever uma regra genérica ("processe o pagamento") sem `if` gigantes para cada tipo. O código fica **aberto para extensão** (basta criar uma nova subclasse `PagamentoBoleto` sem alterar `processar`) — e isso é exatamente o princípio Open/Closed do SOLID que veremos na seção 6.

### 3.5 Visibilidade dos membros

Por trás do encapsulamento está o controle de visibilidade. A FGV cobra os quatro níveis:

| Modificador | Visível na mesma classe | Visível na subclasse | Visível no pacote | Visível fora do pacote |
|---|---|---|---|---|
| `private` | sim | **não** | **não** | **não** |
| *(padrão, sem modificador)* | sim | **não** | sim | **não** |
| `protected` | sim | sim | sim | **não** |
| `public` | sim | sim | sim | sim |

> [!warning] PEGADINHA — `protected` e o `private`
> O `private` **não é herdado** (a subclasse não enxerga o atributo `private` do pai — ela só acessa via métodos públicos/protegidos). Já o `protected` é herdado e visível na subclasse. Frase clássica de prova: "o membro `private` é acessível na subclasse" — **falso**. E atenção: `protected` é visível **no pacote** também, embora o nome sugira só a hierarquia.

---

## 4. A relação entre POO e o mundo dos dados

Antes de avançar para SOLID, vale consolidar a conexão com o Banco de Dados, pois ela reaparecerá nos tópicos 2, 4 e 5 desta fase.

| Mundo do banco ([[Fundamentos-e-Modelagem|modelagem]]) | Mundo do POO (código) |
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
