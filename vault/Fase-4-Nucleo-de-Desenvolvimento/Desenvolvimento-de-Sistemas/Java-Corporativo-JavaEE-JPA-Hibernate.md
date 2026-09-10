# Java Corporativo — JavaEE, JakartaEE, JPA e Hibernate

> [!info] Metadados
> **Disciplina:** Desenvolvimento de Sistemas
> **Bloco:** 4.1 — Desenvolvimento de Sistemas (FASE 4 — Núcleo de Desenvolvimento)
> **Tópico:** 3. Java Corporativo — JavaEE, JakartaEE, JPA e Hibernate
> **Subtópicos:** JavaEE (Servlets, JSP, CDI, Bean Validation, JAX-RS) · JakartaEE (evolução, mudança de namespace javax.* → jakarta.*) · JPA (mapeamento ORM, entidades, repositórios, JPQL) · Hibernate (configuração, cascata, lazy/eager, cache)
> **Pré-requisitos:** [[Java-Fundamentos-da-Linguagem|Java — Fundamentos da Linguagem]] (sintaxe, tipos, coleções) e [[Paradigma-Orientado-a-Objetos|POO]] (classe, objeto, herança, encapsulamento) e [[SQL-DDL-e-DML|Banco de Dados]] (SQL, mapeamento entidade-relacional)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-09-09

---

## 1. Por que estudar Java corporativo — JavaEE, JakartaEE, JPA e Hibernate?

A progressão do Bloco 4.1 tem uma lógica de construção em três andares. No **tópico 1 ([[Java-Fundamentos-da-Linguagem|Java — Fundamentos da Linguagem]])**, você aprendeu a **sintaxe**: como se escreve um programa, variáveis, coleções, exceções. No **tópico 2 ([[Paradigma-Orientado-a-Objetos|Paradigma Orientado a Objetos]])**, você elevou o nível para o **paradigma**: classe, objeto, herança, encapsulamento, SOLID — o modelo mental de design. Agora, neste **tópico 3**, os dois mundos se encontram com o **banco de dados** que você estudou na Fase 3: as classes viram **entidades JPA** e o paradigma vira **POO aplicado ao banco**.

Guarde a ponte que você já construiu na nota de POO — ela é o mapa do tesouro deste tópico:

| Mundo do banco ([[Fundamentos-e-Modelagem|modelagem]]) | Mundo do POO/Java (código) |
|---|---|
| Entidade / tabela | Classe (`@Entity`) |
| Ocorrência / tupla (linha) | Objeto |
| Coluna | Atributo |
| Chave primária | Identidade (campo `@Id`) |
| Relacionamento 1:N / N:M | Referência entre objetos / coleções (`@OneToMany`, `@ManyToMany`) |

A pergunta central que este tópico responde: a aplicação é escrita em Java (**objetos**) e o banco é relacional (**tabelas**) — existe uma incompatibilidade de paradigmas por construção. Quem traduz automaticamente um mundo para o outro, para o programador não escrever SQL e mapeamento manual a cada consulta? A resposta é o **ORM**, padronizado pela especificação **JPA** e implementado pelo **Hibernate** — e já adiantando a pegadinha central do tópico, a mais cobrada do edital:

> [!important] JPA é especificação; Hibernate é implementação
> O **Java EE / Jakarta EE** é um conjunto de **especificações** (contratos, "regras"); existem **implementações** que as concretizam. A **JPA** define o contrato de mapeamento objeto-relacional; o **Hibernate** é a implementação mais famosa desse contrato. A FGV cobra essa relação com frequência: *"JPA é uma especificação; Hibernate é uma implementação"* — **verdadeiro**.

Além do ORM, este tópico cobre o **Java EE / Jakarta EE** — o conjunto de especificações corporativas (Servlets, JSP, CDI, Bean Validation, JAX-RS) que sustenta os sistemas da DATAPREV: portais de benefícios, integrações com o INSS, serviços REST de consulta ao **CNIS**.

> [!question] Pergunta orientadora
> Todo sistema corporativo conversa com um banco relacional (como os que você modelou na Fase 3). Se a aplicação é escrita em Java (objetos) e o banco é relacional (tabelas), existe uma "incompatibilidade" de paradigmas. Quem resolve essa tradução automática, para que o programador não escreva SQL e mapeamento manual a cada consulta? A resposta está no coração deste tópico: o **ORM**.

---

## 2. Java EE, Jakarta EE e a transição de namespace

Aqui cruza um dos pontos mais cobrados pelo edital e um dos que mais confundem: a distinção entre **Java SE**, **Java EE** e **Jakarta EE**.

- **Java SE (Standard Edition):** a linguagem e a plataforma base (tipos, coleções, exceções, `java.util`, `java.lang`). É o núcleo que você estudou no tópico 1.
- **Java EE (Enterprise Edition, hoje *Jakarta EE*):** um conjunto de **especificações** para sistemas corporativos — web (Servlets, JSP), acesso a banco (JPA), injeção de dependência (CDI), validação (Bean Validation), serviços REST (JAX-RS), entre outras.

> [!important] Especificação vs. Implementação
> O ponto de ouro: o **Java EE / Jakarta EE é uma *especificação* (um conjunto de contratos, de "regras")** — e existem **implementações** que a concretizam. O **Hibernate** é uma implementação da especificação **JPA**; o **WildFly/GlassFish** são *servidores* que implementam o conjunto Java EE. A FGV cobra isso com frequência: *"JPA é uma especificação; Hibernate é uma implementação"* — **verdadeiro**.

### 2.1 A mudança de namespace: `javax.*` → `jakarta.*`

Historicamente, as APIs corporativas Java ficavam sob o pacote **`javax.*`** (ex.: `javax.servlet`). Em **2017**, a Oracle cedeu o Java EE à **Eclipse Foundation**, que o renomeou para **Jakarta EE**. Com a **Jakarta EE 9** (2020), o namespace **público de todas as APIs mudou de `javax.*` para `jakarta.*`**:

- `javax.servlet.*` → `jakarta.servlet.*`
- `javax.persistence.*` (JPA) → `jakarta.persistence.*`
- `javax.validation.*` (Bean Validation) → `jakarta.validation.*`
- `javax.ws.rs.*` (JAX-RS) → `jakarta.ws.rs.*`

Essa mudança foi **apenas de namespace** — as classes, em geral, tiveram o mesmo nome, mas mudaram de pacote. Aplicações escritas com `javax.*` precisam **migrar o import** para `jakarta.*` para rodar em servidores Jakarta EE 9+.

> [!warning] PEGADINHA — evolução, não substituição técnica abrupta
> O edital adverte: *"A transição JavaEE → JakartaEE deve ser entendida como evolução, não substituição."* Não se trata de uma linguagem nova nem de APIs totalmente diferentes — é a **mesma plataforma corporativa**, transferida para a Eclipse Foundation e com o namespace renomeado de `javax.*` para `jakarta.*`. Uma alternativa de prova que diga que "Jakarta EE é uma linguagem nova" ou "um framework substituindo o Java EE" está errada.

### 2.2 As especificações principais (conceito de cada uma)

| Especificação | O que define | Implementação típica |
|---|---|---|
| **Servlets** | Programas Java que rodam no servidor e atendem requisições HTTP | faz parte do servidor (Tomcat, WildFly) |
| **JSP** (JavaServer Pages) | Páginas web que misturam HTML e código Java/lógica de apresentação | motor JSP do servidor |
| **CDI** (Contexts and Dependency Injection) | Injeção de dependência e ciclo de vida de objetos com contexto | Weld |
| **Bean Validation** | Validação declarativa de atributos (anotações como `@NotNull`) | Hibernate Validator |
| **JAX-RS** | Criação de APIs REST em Java (anotações `@Path`, `@GET`) | Jersey, RESTEasy |

**Servlets** são o alicerce mais antigo: um `HttpServlet` recebe requisições HTTP e produz respostas. **JSP** permite escrever páginas com código Java embutido (`<% %>`), embora hoje o `JSP` seja considerado técnica legada frente aos frameworks modernos. **CDI** é a injeção de dependência — o "motor" que monta os objetos e suas dependências automaticamente. **Bean Validation** valida dados com anotações como `@NotNull`, `@Size`, `@Email` nos atributos. **JAX-RS** permite expor recursos REST com anotações.

---

## 3. JPA — a especificação de mapeamento objeto-relacional

### 3.1 O que é ORM e por que existe

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

### 3.2 Anotações centrais da JPA

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

### 3.3 Repositórios e o acesso a dados

No padrão moderno, o acesso a dados não é feito pedaço por pedaço de JPA, mas por **repositórios** — interfaces que abstraem as operações de persistência (salvar, buscar, deletar). O **Spring Data** (que veremos no tópico 5) fornece os repositórios do JPA por herança de interface.

```java
// Repositório: interface que encapsula as operações de persistência
public interface BeneficiarioRepository extends JpaRepository<Beneficiario, Long> {
    // métodos herdados: save(), findById(), findAll(), delete()
    List<Beneficiario> findByCpf(String cpf);        // consulta derivada do nome
}
```

### 3.4 JPQL — a linguagem de consulta do JPA

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

## 4. Hibernate — a implementação da JPA

### 4.1 Especificação vs. implementação (o ponto de ouro)

Para fixar a pegadinha mais rentável do tópico:

> [!important] JPA é especificação; Hibernate é implementação
> A **JPA** define o *contrato* (as anotações e a API padrão). O **Hibernate** é a *implementação* desse contrato que de fato se conecta ao banco. Você escreve código contra a interface **JPA** (`EntityManager`, anotações `javax/jakarta.persistence`), e o **Hibernate** executa por baixo. Trocar a implementação (ex.: usar EclipseLink no lugar do Hibernate) não exige reescrever o código que usa a API JPA — justamente por depender da **especificação**, não da implementação. Isso é o **DIP** (D de SOLID) na prática.

### 4.2 Fluxo de vida das entidades (states)

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

### 4.3 Cascata — propagando operações

O atributo **`cascade`** define quais operações são **propagadas** de uma entidade para suas associações. Ex.: se um `Beneficiario` é persistido e seus `Dependente` têm `cascade = CASCADE_TYPE.PERSIST`, salvá-lo salva também os dependentes.

```java
@OneToMany(mappedBy = "beneficiario", cascade = CascadeType.ALL)
private List<Dependente> dependentes;
```

Tipos: `PERSIST`, `MERGE`, `REMOVE`, `REFRESH`, `DETACH`, ou `ALL` (todos). A pegadinha: sem `cascade`, cada entidade precisa ser persistida individualmente; com `cascade`, a operação se propaga.

### 4.4 Lazy vs. Eager loading

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

### 4.5 Cache do Hibernate

O Hibernate usa **três níveis de cache** para evitar reprocessar consultas:

- **Cache de primeiro nível (L1):** o cache **da sessão**, sempre ativo e obrigatório; dura enquanto a sessão existe.
- **Cache de segundo nível (L2):** o cache **compartilhado entre sessões** (do *SessionFactory*), opcional, configurado explicitamente.
- **Cache de consulta (query cache):** armazena **resultados de consultas** (JPQL), opcional.

> [!warning] PEGADINHA — L1 é obrigatório; L2 é opcional
> O **cache de primeiro nível da sessão é sempre ativo e não pode ser desligado**. O **segundo nível é opcional e precisa ser configurado**. Uma alternativa que diga "o segundo nível é obrigatório" ou "o primeiro nível é opcional" está errada. Lembre ainda da ordem hierárquica: L1 < L2 (o L2 é compartilhado entre sessões; o L1 é exclusivo de cada sessão).

---

## 5. Como a FGV cobra este tópico

- **JavaEE → JakartaEE:** a mudança de namespace `javax.*` → `jakarta.*`, e que é uma **evolução**, não substituição.
- **JPA vs. Hibernate:** a relação **especificação vs. implementação** é a pegadinha mais cobrada do tópico.
- **JPQL:** consulta a **entidades** (não tabelas).
- **Hibernate:** estados da entidade, `cascade`, **lazy vs. eager**, e o cache (L1 obrigatório, L2 opcional).
- **Especificações Java EE:** saber o que cada uma define — Servlets (requisições HTTP), JSP (páginas), CDI (injeção de dependência), Bean Validation (`@NotNull`, `@Size`), JAX-RS (REST).

> [!warning] PEGADINHA — agrupando as armadilhas mais prováveis
> 1. "JPA é um framework?" — **não**, é especificação; Hibernate é implementação.
> 2. "JPQL consulta tabelas?" — **não**, consulta entidades (nome da classe).
> 3. "O cache de primeiro nível é opcional?" — **não**, é obrigatório; o segundo nível é que é opcional.
> 4. "Jakarta EE é um novo framework?" — **não**, é a evolução do Java EE com namespace `jakarta.*`.
> 5. "Eager carrega sob demanda?" — **não**, *lazy* é que carrega sob demanda; *eager* carrega imediatamente.

---

## 6. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **Java SE** (linguagem) vs. **Java EE/Jakarta EE** (especificações empresariais); namespace `javax.*` → `jakarta.*` como **evolução**
> - [ ] Especificações: Servlets, JSP, CDI, Bean Validation, JAX-RS
> - [ ] **JPA = especificação** (ORM); **Hibernate = implementação**
> - [ ] Entidades: `@Entity`, `@Table`, `@Id`, `@GeneratedValue`, `@Column`, `@OneToMany`/`@ManyToOne` (cardinalidades da [[Fundamentos-e-Modelagem|modelagem]])
> - [ ] **JPQL** consulta entidades (nome da classe), não tabelas
> - [ ] **Hibernate:** estados (transient, persistent, detached, removed); `cascade`; **lazy** (sob demanda) vs. **eager** (imediato); cache **L1 obrigatório**, L2 opcional

> [!warning] O erro mais comum em prova
> Afirmar que **JPA é uma implementação/framework** e que **Hibernate é a especificação** — a relação é exatamente a **inversa**. E também trocar **lazy por eager** no significado de "carregamento imediato/sob demanda".

---

## 7. Próximos passos

Com este tópico, o trio **sintaxe → paradigma → corporativo** fecha o núcleo Java do edital. Você agora entende as especificações Java EE/Jakarta EE e a ponte ORM entre o POO e o banco (JPA/Hibernate) — o alicerce que o framework mais cobrado do edital usa.

O **próximo tópico da ementa é o JavaScript (tópico 4)**: uma linguagem diferente, com outra filosofia — tipagem dinâmica, closures, escopo, async/await — que prepara o terreno para o frontend e para as soluções híbridas de mobile.

Depois do JavaScript, a ementa retorna ao mundo Java com os **Frameworks Java (tópico 5)**: o **Spring** usa o **CDI** que você viu aqui; o **Spring Data** usa os **repositórios JPA** que você acabou de conhecer; e o **Spring Boot** automatiza a configuração do **Hibernate**. O que você construiu neste tópico é exatamente o que o ecossistema Spring consome — por isso a ementa o coloca antes.