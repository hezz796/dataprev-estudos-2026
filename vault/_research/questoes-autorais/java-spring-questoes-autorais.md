# Java e Spring — Questões Autorais Comentadas

> **Disciplina:** Desenvolvimento de Sistemas · **Bloco:** 4.1 — Desenvolvimento de Sistemas
> **Banca de referência:** FGV · **Formato:** alternativas A–E
> **Origem:** autoral (todas) · **Não são questões oficiais de banca.**

---

## Questão 01 — Spring IoC/DI e Anotações

**id:** JAVA-SPRING-001
**disciplina:** Desenvolvimento de Sistemas
**tópico:** Frameworks Java
**subtópico:** Spring (IoC, DI, anotações por camada)
**origem:** autoral
**habilidade cognitiva:** aplicação e análise
**dificuldade:** média
**conhecimento avaliado:** IoC vs. DI; papel de @Component, @Service, @Repository, @Controller e @Autowired; relação entre DI e DIP (SOLID)

Um desenvolvedor está implementando uma aplicação Spring Boot para o sistema de cadastro de beneficiários da DATAPREV. Considere as afirmativas abaixo:

I. No Spring, IoC e DI são sinônimos: ambos referem-se à injeção automática de dependências por meio de anotações.

II. A anotação @Autowired é responsável por realizar a injeção de dependência de um bean gerenciado pelo Spring em outro bean.

III. A anotação @Service é uma especialização de @Component e é indicada para a camada de regra de negócio.

IV. A anotação @Controller é indicada para a camada de acesso a dados e habilita a tradução automática de exceções de persistência.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I e II
B) II e III
C) I, II e III
D) II, III e IV
E) Apenas II

---

**Gabarito:** B

### Comentário

**Raciocínio:** A questão exige avaliar cada afirmação sobre as anotações do Spring e a relação entre IoC e DI. É preciso distinguir o que cada anotação faz e em qual camada é utilizada.

**Palavra-chave:** IoC (princípio) ≠ DI (técnica); @Autowired; @Service; @Controller; @Repository; @Component

**Conceito:**
- **IoC (Inversão de Controle)** é um **princípio de design** — o controle da criação de objetos é invertido: em vez de o código instanciar suas dependências com `new`, um container externo faz isso.
- **DI (Injeção de Dependência)** é a **técnica concreta** que implementa o IoC — as dependências são fornecidas de fora, geralmente pelo container Spring.
- Portanto, IoC ≠ DI: um é princípio, o outro é implementação. **Afirmativa I é falsa.**
- **@Autowired** injeta automaticamente um bean gerenciado pelo Spring em outro bean. **Afirmativa II é verdadeira.**
- **@Service** é uma especialização de @Component, usada na camada de negócio. **Afirmativa III é verdadeira.**
- **@Controller** é usada na camada web (recebe requisições HTTP), **não** na camada de dados. Quem faz isso é **@Repository**. **Afirmativa IV é falsa.**

**Análise das alternativas:**
- **A (I e II):** errada — inclui I (falsa).
- **B (II e III):** correta — apenas II e III são verdadeiras.
- **C (I, II e III):** errada — inclui I (falsa).
- **D (II, III e IV):** errada — inclui IV (falsa).
- **E (Apenas II):** errada — III também é verdadeira.

**Pegadinha:** A alternativa I tenta confundir IoC com DI. A banca FGV adora cobrar essa distinção: IoC é o **princípio** (inverter o controle de criação); DI é a **técnica** (injetar de fora). E a alternativa IV troca @Controller por @Repository — reverte as camadas para testar se o candidato sabe qual anotação pertence a qual camada.

---

## Questão 02 — Coleções Java

**id:** JAVA-SPRING-002
**disciplina:** Desenvolvimento de Sistemas
**tópico:** Java e Ecossistema JVM
**subtópico:** Coleções Java (List, Set, Map)
**origem:** autoral
**habilidade cognitiva:** compreensão e aplicação
**dificuldade:** fácil-média
**conhecimento avaliado:** comportamento de List, Set e Map; a regra de duplicatas; relação Map-Collection

Considere o trecho de código abaixo:

```java
Set<String> linguagens = new HashSet<>();
linguagens.add("Java");
linguagens.add("Python");
linguagens.add("Java");
System.out.println(linguagens.size());
```

Qual será a saída do código?

A) 3
B) 2
C) Erro em tempo de compilação
D) NullPointerException
E) 1

---

**Gabarito:** B

### Comentário

**Raciocínio:** A questão testa o conhecimento do comportamento fundamental das coleções Java, especificamente a regra de duplicatas do `Set`.

**Palavra-chave:** Set; HashSet; duplicatas; tamanho da coleção

**Conceito:**
- **`Set`** é uma interface que **não permite elementos duplicados**. Quando se tenta adicionar um elemento já existente em um `HashSet`, a operação é simplesmente ignorada (o `add` retorna `false`, mas não lança exceção).
- O código adiciona "Java", "Python" e "Java" novamente — mas como "Java" já existe, a terceira adição é ignorada.
- O `Set` fica com 2 elementos: "Java" e "Python".
- `linguagens.size()` retorna **2**.

**Análise das alternativas:**
- **A (3):** errada — considera que duplicatas são permitidas (comportamento de `List`, não de `Set`).
- **B (2):** correta — o `Set` ignora a duplicata "Java".
- **C (erro de compilação):** errada — adicionar duplicata a um `Set` não gera erro de compilação; é tratado em execução.
- **D (NullPointerException):** errada — o código não envolve `null` nem unboxing de wrapper.
- **E (1):** errada — o `Set` aceita os dois elementos distintos ("Java" e "Python").

**Pegadinha:** A alternativa A é a armadilha clássica — quem confunde `Set` com `List` responde 3. A alternativa D tenta confundir com a armadilha de `null` em `Integer` (unboxing), que não se aplica aqui. Lembre-se: **`Set` não permite duplicatas; `List` permite; `Map` não é `Collection`.**

---

## Questão 03 — JPA, Hibernate e JPQL

**id:** JAVA-SPRING-003
**disciplina:** Desenvolvimento de Sistemas
**tópico:** Java e Ecossistema JVM
**subtópico:** JPA, Hibernate (especificação vs. implementação), JPQL vs. SQL
**origem:** autoral
**habilidade cognitiva:** análise
**dificuldade:** média
**conhecimento avaliado:** relação JPA/Hibernate (especificação/implementação); diferença entre JPQL e SQL; cache do Hibernate

Considere as afirmativas abaixo sobre JPA e Hibernate:

I. JPA é uma implementação de ORM para Java; Hibernate é uma especificação que padroniza o mapeamento objeto-relacional.

II. Na JPQL, a consulta `FROM Beneficiario WHERE cpf = :cpf` referencia o nome da tabela no banco de dados.

III. O cache de primeiro nível (L1) do Hibernate é sempre ativo e não pode ser desligado; o cache de segundo nível (L2) é opcional e precisa ser configurado.

IV. No Hibernate, um objeto no estado **transiente** foi persistido mas não está mais associado a uma sessão ativa.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I e II
B) II e IV
C) Apenas III
D) III e IV
E) Apenas II

---

**Gabarito:** C

### Comentário

**Raciocínio:** A questão combina três pontos clássicos de cobrança FGV: (1) a relação especificação/implementação entre JPA e Hibernate; (2) a diferença entre JPQL e SQL; (3) o cache do Hibernate. É preciso avaliar cada afirmação separadamente.

**Palavra-chave:** JPA = especificação; Hibernate = implementação; JPQL consulta entidades (nome da classe), não tabelas; cache L1 obrigatório, L2 opcional

**Conceito:**
- **Afirmativa I é falsa.** A relação é inversa: **JPA é a especificação** (define o contrato, as anotações `javax/jakarta.persistence`); **Hibernate é a implementação** (o framework que efetivamente se conecta ao banco). A banca FGV adora inverter essa relação.
- **Afirmativa II é falsa.** Na JPQL, o `FROM` referencia o **nome da classe/entidade** (ex.: `Beneficiario`), não o nome da tabela. Se a tabela se chama `tab_beneficiario` mas a classe é `Beneficiario`, a JPQL usa `FROM Beneficiario`. Já no SQL, usa-se o nome da tabela: `FROM tab_beneficiario`.
- **Afirmativa III é verdadeira.** O cache de primeiro nível (L1) é **obrigatório e sempre ativo** (durante a sessão). O cache de segundo nível (L2) é **compartilhado entre sessões** (no `SessionFactory`) e **opcional** — precisa ser configurado explicitamente.
- **Afirmativa IV é falsa.** Um objeto **transiente** é aquele criado com `new`, que **nunca foi persistido** e não está associado a nenhuma sessão. O objeto que *foi persistido* mas *saiu da sessão* está no estado **detached** (desanexado), não transiente.

**Análise das alternativas:**
- **A (I e II):** errada — ambas falsas.
- **B (II e IV):** errada — ambas falsas.
- **C (Apenas III):** correta.
- **D (III e IV):** errada — IV é falsa.
- **E (Apenas II):** errada — II é falsa.

**Pegadinha:** Esta questão usa **três inversões** clássicas da FGV: (1) trocar especificação por implementação (I); (2) trocar entidade por tabela na JPQL (II); (3) trocar transient por detached (IV). Cada uma é uma armadilha independente. O candidato que dominar essas três inversões elimina todas as falsas com rapidez.

---

## Questão 04 — Spring Boot (Autoconfiguração e Starters)

**id:** JAVA-SPRING-004
**disciplina:** Desenvolvimento de Sistemas
**tópico:** Frameworks Java
**subtópico:** Spring Boot (autoconfiguração, starters, relação com Spring)
**origem:** autoral
**habilidade cognitiva:** compreensão e aplicação
**dificuldade:** média
**conhecimento avaliado:** conceito de autoconfiguração; função dos starters; relação Spring Boot × Spring

Em uma equipe de desenvolvimento da DATAPREV, um membro pergunta sobre o papel do Spring Boot no projeto. Considere as afirmativas abaixo:

I. O Spring Boot é um framework independente que substitui completamente o Spring.

II. Os starters são dependências agregadoras que trazem todas as bibliotecas necessárias para uma funcionalidade específica.

III. A autoconfiguração do Spring Boot inspeciona as dependências no classpath e configura automaticamente os beans apropriados, seguindo o princípio de "convenção sobre configuração".

IV. Para criar uma API REST com acesso a banco de dados, é necessário adicionar individualmente cada dependência (Spring MVC, Tomcat, Hibernate, Spring Data) sem usar starters.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I e II
B) II e III
C) I, II e III
D) III e IV
E) II, III e IV

---

**Gabarito:** B

### Comentário

**Raciocínio:** A questão testa a compreensão do que o Spring Boot faz e como ele se relaciona com o Spring. É preciso avaliar a relação de "camada" (não substituição), o papel dos starters e o conceito de autoconfiguração.

**Palavra-chave:** Spring Boot = camada sobre o Spring; starters = dependências agregadoras; autoconfiguração = convenção sobre configuração

**Conceito:**
- **Afirmativa I é falsa.** O Spring Boot **não substitui** o Spring — ele é uma **camada** que **facilita** o uso do Spring, reduzindo a configuração manual. Usa o mesmo núcleo (IoC/DI, Spring MVC, Spring Data). "Substitui" é a palavra errada — ele *complementa* e *simplifica*.
- **Afirmativa II é verdadeira.** Os **starters** são artefatos de dependência agregadora. Um único starter (ex.: `spring-boot-starter-web`) traz Spring MVC + Tomcat embutido + JSON. `spring-boot-starter-data-jpa` traz Spring Data + Hibernate + configuração de banco.
- **Afirmativa III é verdadeira.** A **autoconfiguração** inspeciona o classpath e configura beans automaticamente. Se há `spring-boot-starter-web`, configura Tomcat e MVC; se há um banco no classpath, configura `DataSource` e Hibernate. É "convenção sobre configuração".
- **Afirmativa IV é falsa.** A existência dos starters é exatamente para **não** precisar adicionar cada dependência individualmente. `spring-boot-starter-web` + `spring-boot-starter-data-jpa` já trazem tudo necessário para uma API REST com banco.

**Análise das alternativas:**
- **A (I e II):** errada — I é falsa.
- **B (II e III):** correta.
- **C (I, II e III):** errada — I é falsa.
- **D (III e IV):** errada — IV é falsa.
- **E (II, III e IV):** errada — IV é falsa.

**Pegadinha:** A alternativa I usa a palavra "substitui" — a banca FGV adora oferecer essa alternativa porque soa plausível para quem não domina a relação Spring Boot × Spring. A alternativa IV inverte a própria definição de starter (que é dependência agregadora) para dizer que ele não existe. Lembre: **Spring Boot facilita o Spring, não o substitui.**

---

## Questão 05 — Spring Cloud (Microserviços)

**id:** JAVA-SPRING-005
**disciplina:** Desenvolvimento de Sistemas
**tópico:** Frameworks Java
**subtópico:** Spring Cloud (Eureka, Gateway, Circuit Breaker)
**origem:** autoral
**habilidade cognitiva:** compreensão
**dificuldade:** média
**conhecimento avaliado:** papel de cada componente do Spring Cloud; distinção entre Service Discovery, Gateway e Circuit Breaker

Um time da DATAPREV está migrando um sistema monolítico para uma arquitetura de microsserviços. Eles precisam escolher os componentes do Spring Cloud adequados para cada necessidade. Associe cada necessidade ao componente correto:

| Necessidade | Componente |
|---|---|
| I. Cada microsserviço precisa registrar seu endereço e ser descoberto dinamicamente pelos demais, sem endereços fixos. | **a)** Circuit Breaker |
| II. O sistema precisa de um único ponto de entrada que roteie requisições HTTP para o microsserviço correto. | **b)** Eureka (Service Discovery) |
| III. Quando um microsserviço falha, o sistema deve "abrir o circuito" para evitar que a falha se propague e devolver uma resposta de fallback. | **c)** Spring Cloud Gateway |

A associação correta é:

A) I — b; II — c; III — a
B) I — a; II — b; III — c
C) I — c; II — a; III — b
D) I — b; II — a; III — c
E) I — a; II — c; III — b

---

**Gabarito:** A

### Comentário

**Raciocínio:** A questão pede associar cada necessidade prática ao componente do Spring Cloud correto. É preciso conhecer o **papel** de cada componente, sem necessidade de saber detalhes de implementação.

**Palavra-chave:** Eureka = Service Discovery (registro e descoberta); Gateway = ponto único de entrada e roteamento; Circuit Breaker = proteção contra falha em cascata

**Conceito:**
- **I → Eureka (b).** O **Eureka** é o **Service Discovery**: cada microsserviço se registra (nome + endereço) e os demais o descobrem dinamicamente. Elimina endereços fixos.
- **II → Gateway (c).** O **Spring Cloud Gateway** é a **porta de entrada única**: recebe todas as requisições externas e as roteia para o microsserviço correto (balanceamento, filtros, roteamento).
- **III → Circuit Breaker (a).** O **Circuit Breaker** (Resiliência) funciona como um disjuntor elétrico: quando um serviço falha repetidamente, "abre o circuito" e devolve uma resposta de fallback, evitando que a falha se propague para toda a cadeia.

**Análise das alternativas:**
- **A (I-b, II-c, III-a):** correta — cada necessidade está associada ao componente certo.
- **B, C, D, E:** erradas — ao menos uma associação está invertida.

**Pegadinha:** A banca FGV gosta de trocar os papéis dos componentes do Spring Cloud. O candidato que sabe apenas "Eureka é discovery" mas não sabe o que o Gateway e o Circuit Breaker fazem pode errar ao associar. Guarde a analogia: **Eureka = agenda telefônica (descobre quem é quem)** · **Gateway = recepção (encaminha para o lugar certo)** · **Circuit Breaker = disjuntor (corta antes de queimar tudo)**.

---

## Questão 06 — APIs RESTful (Status Codes e Idempotência)

**id:** JAVA-SPRING-006
**disciplina:** Desenvolvimento de Sistemas
**tópico:** Padrões de Projeto e Arquitetura
**subtópico:** APIs RESTful (verbos HTTP, status codes, idempotência)
**origem:** autoral
**habilidade cognitiva:** análise
**dificuldade:** média-alta
**conhecimento avaliado:** distinção 401 vs. 403; idempotência de verbos HTTP; status code para criação de recurso

Considere as afirmativas abaixo sobre APIs RESTful:

I. O status code **401 Unauthorized** indica que o cliente está autenticado, mas não possui permissão para acessar o recurso.

II. O verbo HTTP **POST** é idempotente: repetir a mesma requisição produz o mesmo efeito no servidor.

III. Após a criação bem-sucedida de um novo recurso via **POST**, a resposta adequada é o status code **201 Created**.

IV. O verbo HTTP **PUT** é usado para atualizar parcialmente um recurso e não é idempotente.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I e II
B) II e IV
C) III e IV
D) Apenas III
E) I, III e IV

---

**Gabarito:** D

### Comentário

**Raciocínio:** A questão combina duas armadilhas clássicas da FGV: (1) a confusão entre 401 e 403; (2) a idempotência dos verbos HTTP. Cada afirmativa precisa ser avaliada com cuidado.

**Palavra-chave:** 401 = não autenticado; 403 = autenticado mas sem permissão; POST = criar (não idempotente); PUT = atualizar (idempotente); 201 Created = resposta de criação

**Conceito:**
- **Afirmativa I é falsa.** 401 Unauthorized significa **não autenticado** — o servidor não sabe quem é o cliente (falta login/token). 403 Forbidden é que significa "autenticado, mas sem permissão". A banca troca os dois constantemente.
- **Afirmativa II é falsa.** POST **não é idempotente**: cada requisição POST cria um **novo** recurso. Enviar a mesma requisição POST duas vezes pode criar dois recursos idênticos. Já o **PUT** é idempotente: repetir a mesma requisição PUT produz o mesmo estado no servidor.
- **Afirmativa III é verdadeira.** Após criar um recurso com POST, a resposta correta é **201 Created**, indicando que o recurso foi criado com sucesso.
- **Afirmativa IV é falsa.** O **PUT** é usado para **atualizar** (substituir integralmente) um recurso — e **é idempotente**. A atualização **parcial** é feita com **PATCH**. E PUT é idempotente, não o contrário.

**Análise das alternativas:**
- **A (I e II):** errada — ambas falsas.
- **B (II e IV):** errada — ambas falsas.
- **C (III e IV):** errada — IV é falsa.
- **D (Apenas III):** correta.
- **E (I, III e IV):** errada — I e IV são falsas.

**Pegadinha:** Esta questão condensa **duas das maiores armadilhas** da FGV em APIs RESTful: (1) **401 vs. 403** — a banca troca os significados e quase todo mundo erra; (2) **POST vs. PUT na idempotência** — POST cria (não idempotente), PUT atualiza (idempotente). E a alternativa IV troca PUT por PATCH na atualização parcial. Domine essas quatro distinções e essa questão fica trivial.

---

## Padrões de cobrança utilizados

As questões autorais acima foram inspiradas nos seguintes padrões de cobrança identificados nas questões reais FGV:

1. **Java + Spring/Hibernate/JUnit** (DATAPREV 2024, AMAZUL 2025): questões sobre IoC/DI, anotações por camada, autoconfiguração Spring Boot, relação JPA/Hibernate. Inspiração para Q01, Q03, Q04.
2. **Spring Cloud — componentes** (edital DATAPREV 2026): conceito de Eureka, Config, Gateway, Circuit Breaker. Inspiração para Q05.
3. **APIs RESTful — status codes e verbos HTTP** (padrão recorrente FGV): distinção 401 vs. 403, idempotência de POST/PUT, status codes de criação. Inspiração para Q06.
4. **Java — coleções** (padrão recorrente FGV): comportamento de Set, List, Map; regra de duplicatas. Inspiração para Q02.
5. **Julgamento de afirmativas (V/F)** — formato FGV clássico: múltiplas afirmações com uma ou duas falsas sutis. Inspiração para todas as questões de julgamento.
6. **JPA vs. Hibernate — especificação vs. implementação** (padrão clássico FGV): a inversão mais cobrada do tópico. Inspiração para Q03.
