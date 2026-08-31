# Java e Ecossistema JVM

> [!info] Metadados
> **Disciplina:** Desenvolvimento de Sistemas
> **Bloco:** 4.1 — Desenvolvimento de Sistemas (FASE 4 — Núcleo de Desenvolvimento)
> **Tópico:** 2. Java e Ecossistema JVM
> **Subtópicos:** Java (tipos primitivos, coleções, tratamento de exceções, generics) · JavaEE (Servlets, JSP, CDI, Bean Validation, JAX-RS) · JakartaEE (evolução, mudança de namespace) · JPA (mapeamento ORM, entidades, repositórios, JPQL) · Hibernate (configuração, cascata, lazy/eager, cache)
> **Pré-requisitos:** [[Raciocinio-Matematico-Aplicado|Raciocínio Lógico Matemático]] (lógica de programação) e [[SQL-DDL-e-DML|SQL/Banco de Dados]] (consultas, mapeamento entidade-relacional) e [[Paradigma-Orientado-a-Objetos|POO]] (classe, objeto, encapsulamento)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-31

---

## 1. Por que estudar Java e o ecossistema JVM?

A ementa é categórica: **"Java é o tópico de maior profundidade — priorizar o ecossistema Spring, que é o mais cobrado."** Não é exagero: na DATAPREV, e em praticamente todo o mundo de sistemas corporativos públicos brasileiros (bancos, previdência, governo), o Java é a espinha dorsal do desenvolvimento. O contexto da DATAPREV — com seus sistemas de benefícios, consignação, gestão do CNIS — é majoritariamente construído na plataforma Java.

Para entender por que isso importa, conecte com o que você já construiu:

- Na [[Paradigma-Orientado-a-Objetos|nota anterior]], você aprendeu o **POO** de forma conceitual — classe, objeto, herança, polimorfismo, encapsulamento. O Java é a **linguagem** onde esses conceitos se materializam em código. Tudo que vimos lá (visibilidade `private`/`protected`, `extends`, `@Override`) é sintaxe real de Java.
- Na [[Fundamentos-e-Modelagem|Fase 3 de Banco de Dados]], você modelou **entidades** e consultou com **SQL**. No Java empresarial, essas entidades viram **classes**, as tabelas viram classes anotadas, e o SQL vira **JPQL** — a ponte automática entre os dois mundos. É o **JPA/Hibernate**.

> [!question] Pergunta orientadora
> Todo sistema corporativo conversa com um banco relacional (como os que você modelou na Fase 3). Se a aplicação é escrita em Java (objetos) e o banco é relacional (tabelas), existe uma "incompatibilidade" de paradigmas. Quem resolve essa tradução automática, para que o programador não escreva SQL e mapeamento manual a cada consulta? A resposta está no coração deste tópico: o **ORM**.

---

## 2. Tipos primitivos e wrappers

O Java tem **dois mundos de tipos de dados**: os **primitivos** (valores puros, rápidos, sem métodos) e os **wrappers** (classes que "embrulham" cada primitivo em um objeto). Essa distinção é uma das pegadinhas mais frequentes.

### 2.1 Os 8 tipos primitivos

| Tipo | Tamanho | Faixa típica | Observação |
|---|---|---|---|
| `byte` | 8 bits | −128 a 127 | |
| `short` | 16 bits | −32.768 a 32.767 | |
| `int` | 32 bits | −2³¹ a 2³¹−1 | o inteiro padrão |
| `long` | 64 bits | −2⁶³ a 2⁶³−1 | precisa sufixo `L` |
| `float` | 32 bits | precisão simples | precisa sufixo `f` |
| `double` | 64 bits | precisão dupla | o ponto-flutuante padrão |
| `char` | 16 bits | caractere Unicode | um caractere |
| `boolean` | — | `true`/`false` | não é 0/1 como em C |

```java
int idade = 32;
long cpfNumerico = 12345678901L;   // sufixo L (senão é int e estoura)
double salario = 4250.75;
float taxa = 0.05f;                // sufixo f
char uf = 'P';
boolean ativo = true;
```

> [!warning] PEGADINHA — `float` sem `f` e `long` sem `L`
> Escrever `float x = 0.5;` **não compila** em Java na atribuição literal, porque `0.5` é por padrão um `double` (64 bits) e você não pode estreitar para `float` sem cast ou sufixo `f`. Da mesma forma, um literal inteiro grande demais para `int` precisa de `L`. A FGV costuma cobrar o **comportamento padrão** dos literais.

### 2.2 Wrappers: primitivo em forma de objeto

Cada primitivo tem sua classe wrapper: `Integer`, `Long`, `Double`, `Float`, `Short`, `Byte`, `Character`, `Boolean`. O **autoboxing** converte automaticamente primitivo → wrapper; o **unboxing**, wrapper → primitivo.

```java
Integer n = 10;          // autoboxing: int 10 -> Integer
int m = n;               // unboxing: Integer -> int
```

Por que os wrappers existem? Porque as **coleções do Java (`List`, `Set`, `Map`) só armazenam objetos, não primitivos** — e porque wrappers aceitam `null` (representam "ausência de valor"), enquanto primitivos não.

```java
List<Integer> numeros = new ArrayList<>();   // NÃO aceita List<int>
numeros.add(5);                              // autoboxing dentro da coleção
```

> [!warning] PEGADINHA — `null` no unboxing
> `Integer n = null; int m = n;` dispara **`NullPointerException`** no unboxing. Primitivos não podem ser `null`; wrappers podem. A banca explora isso para testar se você sabe que a remoção do objeto (unboxing) pode falhar se o valor for `null`.

---

## 3. Coleções Java

As **coleções** agrupam objetos. A hierarquia central é a da interface `Collection`, com duas grandes famílias — **`List`** e **`Set`** — e uma estrutura à parte, o **`Map`** (que não é um `Collection`, um detalhe que já caiu em prova).

| Interface | Ordem | Duplicados | Acesso | Implementação típica |
|---|---|---|---|---|
| `List` | sim (indexada) | **permite** | por índice | `ArrayList`, `LinkedList` |
| `Set` | não garante (no `HashSet`) | **não permite** | por valor | `HashSet`, `LinkedHashSet`, `TreeSet` |
| `Map` | depende | chaves **únicas** | por chave | `HashMap`, `LinkedHashMap`, `TreeMap` |

```java
// List — permite duplicados, acessa por índice
List<String> nomes = new ArrayList<>();
nomes.add("Ana");
nomes.add("Ana");           // permitido na List
nomes.get(0);               // "Ana"

// Set — não permite duplicados
Set<String> cidades = new HashSet<>();
cidades.add("Recife");
cidades.add("Recife");      // ignorado (já existe)
cidades.size();             // 1

// Map — chave -> valor, chaves únicas
Map<String, Double> margens = new HashMap<>();
margens.put("INSS", 0.30);
margens.put("BANCO", 0.05);
margens.get("INSS");        // 0.30
```

> [!warning] PEGADINHA — Map NÃO é Collection, e a regra do Set
> O `Map` **não** herda de `Collection` (ele é uma raiz própria no framework de coleções). E a regra de ouro: **`Set` não permite elementos duplicados** — um `HashSet` de nomes com repetidos devolve somente os únicos. Já o `List` permite duplicados e mantém ordem de inserção (indexação). A questão clássica: "qual estrutura não admite duplicados?" → `Set`; "qual mantém ordem por índice?" → `List`.

**`ArrayList` vs. `LinkedList`:** o `ArrayList` usa um array dinâmico (acesso por índice rápido, inserção no meio mais custosa); o `LinkedList` usa nós encadeados (inserção/remoção nas extremidades rápida, acesso por índice lento). Como o `TreeSet`/`TreeMap` mantêm os elementos **ordenados** (via `compareTo`), são as escolhas para dados ordenados.

---

## 4. Tratamento de exceções

O Java trata erros em tempo de execução com **exceções** — objetos que representam uma situação anormal — manipuladas com `try`, `catch`, `finally`.

### 4.1 A hierarquia

```
Throwable
├── Error            (problemas graves de máquina/JVM — não tratamos)
└── Exception
    ├── RuntimeException  (unchecked — não é obrigatório declarar/tratar)
    │      └── NullPointerException, ArithmeticException, IndexOutOfBounds
    └── (checked — obrigatório tratar ou declarar)
          └── IOException, SQLException, ClassNotFoundException
```

A distinção mais cobrada: **checked vs. unchecked (runtime)**.

- **Erros (`Error`):** falhas internas da JVM (ex.: `OutOfMemoryError`). Não devem ser tratados pelo programador.
- **Exceções verificadas (checked):** o compilador **obriga** a tratar com `try/catch` **ou** a declarar com `throws` no método. Ex.: `IOException`, `SQLException`.
- **Exceções não verificadas (unchecked / `RuntimeException`):** não obrigatórias de declarar/tratar; ocorrem por bugs de programação. Ex.: `NullPointerException`, `ArithmeticException` (dividir por zero), `IndexOutOfBoundsException`.

```java
// checked — o compilador exige try/catch ou throws
try {
    FileReader arquivo = new FileReader("dados.txt");
} catch (FileNotFoundException e) {
    System.out.println("Arquivo não encontrado");
}

// unchecked — não obriga, mas divide por zero lança ArithmeticException
int a = 10, b = 0;
int r = a / b;   // lança ArithmeticException em tempo de execução
```

### 4.2 try, catch, finally — a ordem e o papel

- **`try`:** bloco que pode lançar exceção.
- **`catch`:** captura e trata a exceção (um por tipo; o mais específico primeiro).
- **`finally`:** bloco que **sempre** executa, havendo ou não exceção — usado para liberar recursos (fechar arquivo, conexão).

```java
try {
    conexao = obterConexao();
    conexao.query(...);
} catch (SQLException e) {
    logErro(e);
} finally {
    // sempre roda: fecha a conexão, havendo erro ou não
    if (conexao != null) conexao.close();
}
```

> [!warning] PEGADINHA — `finally` sempre executa (com a exceção do `System.exit`)
> O bloco `finally` **sempre** executa — mesmo se houver `return` dentro do `try` ou do `catch`. As únicas situações em que ele não roda são: `System.exit()`, uma falha da JVM, ou um looping infinito. E mais uma armadilha: um `return` dentro de `finally` **sobrescreve** qualquer retorno anterior do `try`/`catch` — comportamento que a banca adora perguntar.

### 4.3 `throws` vs. `throw`

- **`throws`:** declara, na **assinatura do método**, que ele pode lançar uma exceção (delega a responsabilidade a quem chamou).
- **`throw`:** **lança de fato** um objeto de exceção dentro do código.

```java
public double calcular(double valor) throws IllegalArgumentException {   // declara
    if (valor < 0) {
        throw new IllegalArgumentException("Valor negativo");          // lança de fato
    }
    return valor;
}
```

---

## 5. Generics

**Generics** (genéricos) permitem escrever classes, interfaces e métodos que trabalham com **tipos parametrizados** — ou seja, definem o "tipo de dados" que serão manipulados, ganhando **segurança de tipos em tempo de compilação** e eliminando casts manuais.

```java
// Sem generics: precisa cast e arrisca ClassCastException
List lista = new ArrayList();
lista.add("texto");
String s = (String) lista.get(0);   // cast manual

// Com generics: tipo garantido pelo compilador, sem cast
List<String> nomes = new ArrayList<>();
nomes.add("Ana");
String nome = nomes.get(0);         // nenhum cast, tipo garantido
// nomes.add(123);                  // erro de compilação! tipo errado
```

Antes dos generics (Java 5), uma `List` podia misturar qualquer `Object` e a conversão era manual e perigosa. Com generics, o **erro de tipo é pego em compilação**, não em execução.

> [!note] Por que os generics conectam com as coleções?
> Como as coleções armazenam objetos e você quer listas de beneficiários, de strings, de inteiros sem misturar tipos, os generics (`List<Beneficiario>`) são a ferramenta. A coleção + generics é o "pacote completo" do desenvolvimento Java.

---

## 6. Java EE, Jakarta EE e a transição de namespace

Aqui cruza um dos pontos mais cobrados pelo edital e um dos que mais confundem: a distinção entre **Java SE**, **Java EE** e **Jakarta EE**.

- **Java SE (Standard Edition):** a linguagem e a plataforma base (tipos, coleções, exceções, `java.util`, `java.lang`). É o núcleo que vimos até aqui.
- **Java EE (Enterprise Edition, hoje *Jakarta EE*):** um conjunto de **especificações** para sistemas corporativos — web (Servlets, JSP), acesso a banco (JPA), injeção de dependência (CDI), validação (Bean Validation), serviços REST (JAX-RS), entre outras.

> [!important] Especificação vs. Implementação
> O ponto de ouro: o **Java EE / Jakarta EE é uma *especificação* (um conjunto de contratos, de "regras")** — e existem **implementações** que a concretizam. O **Hibernate** é uma implementação da especificação **JPA**; o **WildFly/GlassFish** são *servidores* que implementam o conjunto Java EE. A FGV cobra isso com frequência: *"JPA é uma especificação; Hibernate é uma implementação"* — **verdadeiro**.

### 6.1 A mudança de namespace: `javax.*` → `jakarta.*`

Historicamente, as APIs corporativas Java ficavam sob o pacote **`javax.*`** (ex.: `javax.servlet`). Em **2017**, a Oracle cedeu o Java EE à **Eclipse Foundation**, que o renomeou para **Jakarta EE**. Com a **Jakarta EE 9** (2020), o namespace **público de todas as APIs mudou de `javax.*` para `jakarta.*`**:

- `javax.servlet.*` → `jakarta.servlet.*`
- `javax.persistence.*` (JPA) → `jakarta.persistence.*`
- `javax.validation.*` (Bean Validation) → `jakarta.validation.*`
- `javax.ws.rs.*` (JAX-RS) → `jakarta.ws.rs.*`

Essa mudança foi **apenas de namespace** — as classes, em geral, tiveram o mesmo nome, mas mudaram de pacote. Aplicações escritas com `javax.*` precisam **migrar o import** para `jakarta.*` para rodar em servidores Jakarta EE 9+.

> [!warning] PEGADINHA — evolução, não substituição técnica abrupta
> O edital adverte: *"A transição JavaEE → JakartaEE deve ser entendida como evolução, não substituição."* Não se trata de uma linguagem nova nem de APIs totalmente diferentes — é a **mesma plataforma corporativa**, transferida para a Eclipse Foundation e com o namespace renomeado de `javax.*` para `jakarta.*`. Uma alternativa de prova que diga que "Jakarta EE é uma linguagem nova" ou "um framework substituindo o Java EE" está errada.

### 6.2 As especificações principais (conceito de cada uma)

| Especificação | O que define | Implementação típica |
|---|---|---|
| **Servlets** | Programas Java que rodam no servidor e atendem requisições HTTP | faz parte do servidor (Tomcat, WildFly) |
| **JSP** (JavaServer Pages) | Páginas web que misturam HTML e código Java/lógica de apresentação | motor JSP do servidor |
| **CDI** (Contexts and Dependency Injection) | Injeção de dependência e ciclo de vida de objetos com contexto | Weld |
| **Bean Validation** | Validação declarativa de atributos (anotações como `@NotNull`) | Hibernate Validator |
| **JAX-RS** | Criação de APIs REST em Java (anotações `@Path`, `@GET`) | Jersey, RESTEasy |

**Servlets** são o alicerce mais antigo: um `HttpServlet` recebe requisições HTTP e produz respostas. **JSP** permite escrever páginas com código Java embutido (`<% %>`), embora hoje o `JSP` seja considerado técnica legada frente aos frameworks modernos. **CDI** é a injeção de dependência — o "motor" que monta os objetos e suas dependências automaticamente. **Bean Validation** valida dados com anotações como `@NotNull`, `@Size`, `@Email` nos atributos. **JAX-RS** permite expor recursos REST com anotações.

---

## 7. JPA — a especificação de mapeamento objeto-relacional

### 7.1 O que é ORM e por que existe

**ORM (Object-Relational Mapping, Mapeamento Objeto-Relacional)** é a técnica que **converte objetos Java em linhas de tabelas relacionais e vice-versa**, automaticamente. É a ponte entre os dois paradigmas (POO + relacional). **JPA (Java Persistence API)** é a **especificação** Java que padroniza esse mapeamento; **Hibernate** é a **implementação** mais famosa.

```java
// Entidade JPA — a classe anotada que vira tabela
@Entity                       // diz ao JPA: esta classe é uma entidade (tabela)
@Table(name = "beneficiario") // mapeia para a tabela beneficiario
public class Beneficiario {
    @Id                       // chave primária
    @GeneratedValue(strategy = GenerationType.IDENTITY)  // autoincremento
    private Long id;

    @Column(name = "nome", nullable = false)
    private String nome;

    @Column(name = "cpf", unique = true)
    private String cpf;
    // getters e setters omitidos
}
```

Cada **entidade** correspondente a uma tabela; cada **instância** da entidade, a uma **linha**; cada **atributo anotado**, a uma **coluna**. É exatamente a tabela da [[Paradigma-Orientado-a-Objetos|nota anterior]] (classe↔tabela, objeto↔linha, atributo↔coluna), agora automatizada por anotações.

### 7.2 Anotações centrais da JPA

- **`@Entity`:** marca a classe como entidade persistível (mapeará uma tabela).
- **`@Table(name=...)`:** define a tabela (opcional; sem ela usa o nome da classe).
- **`@Id`:** marca o campo de chave primária.
- **`@GeneratedValue`:** define como a chave é gerada (ex.: `IDENTITY`, `SEQUENCE`).
- **`@Column(name=..., nullable=..., length=...)`:** detalha a coluna e as restrições.
- **`@OneToMany`, `@ManyToOne`, `@ManyToMany`:** mapeiam os **relacionamentos** entre entidades — as mesmas cardinalidades 1:N, N:M que você estudou na [[Fundamentos-e-Modelagem|modelagem conceitual]].

```java
// Relacionamentos: um beneficiario tem vários dependentes (1:N)
@Entity
public class Beneficiario {
    @Id
    private Long id;

    @OneToMany(mappedBy = "beneficiario")   // um para muitos
    private List<Dependente> dependentes;
}

@Entity
public class Dependente {
    @Id
    private Long id;

    @ManyToOne                            // muitos dependentes para um beneficiario
    @JoinColumn(name = "beneficiario_id") // a FK no banco
    private Beneficiario beneficiario;
}
```

Compare com a modelagem da Fase 3: o relacionamento **1:N** no banco vira **`@OneToMany`/`@ManyToOne`** no JPA, e a **chave estrangeira** vira a `@JoinColumn`. O edital valoriza exatamente essa conexão.

### 7.3 Repositórios e o acesso a dados

No padrão moderno, o acesso a dados não é feito pedaço por pedaço de JPA, mas por **repositórios** — interfaces que abstraem as operações de persistência (salvar, buscar, deletar). O **Spring Data** (que veremos no tópico 4) fornece os repositórios do JPA por herança de interface.

```java
// Repositório: interface que encapsula as operações de persistência
public interface BeneficiarioRepository extends JpaRepository<Beneficiario, Long> {
    // métodos herdados: save(), findById(), findAll(), delete()
    List<Beneficiario> findByCpf(String cpf);        // consulta derivada do nome
}
```

### 7.4 JPQL — a linguagem de consulta do JPA

O **JPQL (Java Persistence Query Language)** é uma linguagem de consulta **orientada a entidades** definida pela JPA. Ela se parece com SQL, mas consulta **classes/entidades e seus atributos**, não tabelas/colunas diretamente.

```sql
-- SQL (consulta a tabela e coluna)
SELECT nome FROM beneficiario WHERE cpf = '123';

-- JPQL (consulta a entidade e atributo)
SELECT b.nome FROM Beneficiario b WHERE b.cpf = :cpf
```

Diferenças essenciais (favoritas da banca):

| | SQL | JPQL |
|---|---|---|
| Alvo | tabelas e colunas | entidades e atributos |
| Nome dos alvos | nome da tabela | nome da **classe** (`Beneficiario`) |
| Parâmetro nomeado | `?` / `:` dependente | `:cpf` (por padrão `:` antes) |
| Retorno | tuplas de colunas | objetos/valores de atributos |

> [!warning] PEGADINHA — JPQL consulta entidades, não tabelas
> Na JPQL, você escreve `FROM Beneficiario` (o nome da **classe**), não `FROM beneficiario` (o nome da tabela, que pode ser diferente via `@Table`). A banca adora trocar: apresentar uma JPQL com o nome da tabela no `FROM` como se fosse correta. Lembre: JPQL é **orientada a entidades**.

---

## 8. Hibernate — a implementação da JPA

### 8.1 Especificação vs. implementação (o ponto de ouro)

Para fixar a pegadinha mais rentável do tópico:

> [!important] JPA é especificação; Hibernate é implementação
> A **JPA** define o *contrato* (as anotações e a API padrão). O **Hibernate** é a *implementação* desse contrato que de fato se conecta ao banco. Você escreve código contra a interface **JPA** (`EntityManager`, anotações `javax/jakarta.persistence`), e o **Hibernate** executa por baixo. Trocar a implementação (ex.: usar EclipseLink no lugar do Hibernate) não exige reescrever o código que usa a API JPA — justamente por depender da **especificação**, não da implementação. Isso é o **DIP** (D de SOLID) na prática.

### 8.2 Fluxo de vida das entidades (states)

O Hibernate gerencia as entidades por **estados (estados de ciclo de vida)** — conceito que aparece em prova como *detached*, *persistent*, *transient*:

| Estado | Descrição | Está no banco? | Gerido pelo Hibernate? |
|---|---|---|---|
| **Transient** | objeto criado com `new`, ainda não associado ao Hibernate | não | não |
| **Persistent** | associado a uma sessão/gerido; mudanças são rastreadas e sincronizadas | sim | sim |
| **Detached** | foi persistido, mas saiu da sessão; mudanças não são mais rastreadas | sim (a linha existe) | não |
| **Removed** | marcado para exclusão | até o commit | — |

```java
Beneficiario b = new Beneficiario("Ana", "123");   // transient
em.persist(b);                                     // vira persistent (guarda)
...
em.detach(b);                                      // vira detached
// a partir daqui, mudanças em b não são mais rastreadas no banco
```

### 8.3 Cascata — propagando operações

O atributo **`cascade`** define quais operações são **propagadas** de uma entidade para suas associações. Ex.: se um `Beneficiario` é persistido e seus `Dependente` têm `cascade = CASCADE_TYPE.PERSIST`, salvá-lo salva também os dependentes.

```java
@OneToMany(mappedBy = "beneficiario", cascade = CascadeType.ALL)
private List<Dependente> dependentes;
```

Tipos: `PERSIST`, `MERGE`, `REMOVE`, `REFRESH`, `DETACH`, ou `ALL` (todos). A pegadinha: sem `cascade`, cada entidade precisa ser persistida individualmente; com `cascade`, a operação se propaga.

### 8.4 Lazy vs. Eager loading

O **carregamento (loading)** das associações pode ocorrer em dois momentos:

- **Eager (ansioso):** a associação é **carregada imediatamente** junto com a entidade principal — busca-se tudo de uma vez.
- **Lazy (preguiçoso):** a associação só é carregada **quando é acessada** — uma consulta adicional ocorre "sob demanda".

```java
@OneToMany(fetch = FetchType.LAZY)   // dependentes só carregam ao acessar
private List<Dependente> dependentes;

@ManyToOne(fetch = FetchType.EAGER)  // beneficiario carrega junto
private Beneficiario beneficiario;
```

> [!warning] PEGADINHA — Lazy e a LazyInitializationException
> No carregamento **lazy**, se você acessa a coleção **depois** que a sessão foi encerrada (fora do contexto de persistência), o Hibernate lança **`LazyInitializationException`** — porque não há mais a sessão para buscar os dados. O **eager**, por outro lado, carrega tudo de imediato (pode ser custoso e gerar N+1 consultas). A banca cobra: lazy = "carrega ao acessar, sob demanda"; eager = "carrega imediatamente"; e o risco do lazy fora da sessão.

### 8.5 Cache do Hibernate

O Hibernate usa **três níveis de cache** para evitar reprocessar consultas:

- **Cache de primeiro nível (L1):** o cache **da sessão**, sempre ativo e obrigatório; dura enquanto a sessão existe.
- **Cache de segundo nível (L2):** o cache **compartilhado entre sessões** (do *SessionFactory*), opcional, configurado explicitamente.
- **Cache de consulta (query cache):** armazena **resultados de consultas** (JPQL), opcional.

> [!warning] PEGADINHA — L1 é obrigatório; L2 é opcional
> O **cache de primeiro nível da sessão é sempre ativo e não pode ser desligado**. O **segundo nível é opcional e precisa ser configurado**. Uma alternativa que diga "o segundo nível é obrigatório" ou "o primeiro nível é opcional" está errada. Lembre ainda da ordem hierárquica: L1 < L2 (o L2 é compartilhado entre sessões; o L1 é exclusivo de cada sessão).

---

## 9. Como a FGV cobra este tópico

- **Tipos primitivos vs. wrappers:** autoboxing/unboxing, necessidade de sufixo (`L`, `f`), e a impossibilidade de primitivo ser `null`.
- **Coleções:** `List` (ordem, duplicados permitidos), `Set` (sem duplicados), `Map` (não é `Collection`, chaves únicas); casos `ArrayList` vs. `LinkedList`.
- **Exceções:** checked vs. unchecked; comportamento do `finally`; `throws` (declara) vs. `throw` (lança).
- **Generics:** segurança de tipos em tempo de compilação, eliminação de casts.
- **JavaEE → JakartaEE:** a mudança de namespace `javax.*` → `jakarta.*`, e que é uma **evolução**, não substituição.
- **JPA vs. Hibernate:** a relação **especificação vs. implementação** é a pegadinha mais cobrada do tópico.
- **JPQL:** consulta a **entidades** (não tabelas).
- **Hibernate:** estados da entidade, `cascade`, **lazy vs. eager**, e o cache (L1 obrigatório, L2 opcional).

> [!warning] PEGADINHA — agrupando as armadilhas mais prováveis
> 1. "JPA é um framework?" — **não**, é especificação; Hibernate é implementação.
> 2. "JPQL consulta tabelas?" — **não**, consulta entidades (nome da classe).
> 3. "O cache de primeiro nível é opcional?" — **não**, é obrigatório; o segundo nível é que é opcional.
> 4. "Jakarta EE é um novo framework?" — **não**, é a evolução do Java EE com namespace `jakarta.*`.
> 5. "Eager carrega sob demanda?" — **não**, *lazy* é que carrega sob demanda; *eager* carrega imediatamente.

---

## 10. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **Primitivos** (8 tipos, valores rápidos, sem `null`) vs. **wrappers** (objetos, coleções, aceitam `null`); autoboxing/unboxing
> - [ ] **Coleções:** `List` (ordem + duplicados), `Set` (sem duplicados), `Map` (chave→valor, chaves únicas, **não é `Collection`**)
> - [ ] **Exceções:** checked (obrigatório tratar) vs. unchecked (`RuntimeException`); `try`/`catch`/`finally`; `finally` sempre executa; `throws` declara, `throw` lança
> - [ ] **Generics:** tipos parametrizados, segurança em compilação
> - [ ] **Java SE** (linguagem) vs. **Java EE/Jakarta EE** (especificações empresariais); namespace `javax.*` → `jakarta.*` como **evolução**
> - [ ] Especificações: Servlets, JSP, CDI, Bean Validation, JAX-RS
> - [ ] **JPA = especificação** (ORM); **Hibernate = implementação**
> - [ ] Entidades: `@Entity`, `@Table`, `@Id`, `@GeneratedValue`, `@Column`, `@OneToMany`/`@ManyToOne` (cardinalidades da [[Fundamentos-e-Modelagem|modelagem]])
> - [ ] **JPQL** consulta entidades (nome da classe), não tabelas
> - [ ] **Hibernate:** estados (transient, persistent, detached, removed); `cascade`; **lazy** (sob demanda) vs. **eager** (imediato); cache **L1 obrigatório**, L2 opcional

> [!warning] O erro mais comum em prova
> Afirmar que **JPA é uma implementação/framework** e que **Hibernate é a especificação** — a relação é exatamente a **inversa**. E também trocar **lazy por eager** no significado de "carregamento imediato/sob demanda".

---

## 11. Próximos passos

Você dominou a base: tipos, coleções, exceções, generics, o ecossistema corporativo (Java EE/Jakarta EE) e a ponte ORM com o banco de dados (JPA/Hibernate). Esse é exatamente o alicerce que o **Spring** — o framework mais cobrado do edital — usa.

O próximo tópico, **Frameworks Java**, aprofunda no **Spring (IoC, DI, Spring MVC, Spring Data)**, no **Spring Boot** (autoconfiguração e starters), no **Spring Cloud** (Eureka, Config, Gateway, Circuit Breaker) e nas tecnologias de interface como **JSF** e **PrimeFaces**. Você vai ver como a **injeção de dependência** (que já tocamos no D de SOLID e no CDI) vira o motor central do Spring — e como o **Spring Data** usa os **repositórios JPA** que você acabou de conhecer. Antes, porém, a ementa coloca um desvio pedagógico: o **JavaScript**, que prepara o terreno para o frontend — tema do tópico 3.
