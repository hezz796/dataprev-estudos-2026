# Frameworks Java

> [!info] Metadados
> **Disciplina:** Desenvolvimento de Sistemas
> **Bloco:** 4.1 — Desenvolvimento de Sistemas (FASE 4 — Núcleo de Desenvolvimento)
> **Tópico:** 4. Frameworks Java
> **Subtópicos:** Spring (IoC, DI, Spring MVC, Spring Data) · Spring Boot (autoconfiguração, starters) · Spring Cloud (Discovery/Eureka, Config, Gateway, Circuit Breaker) · JSF (JavaServer Faces, ciclo de vida, componentes) · PrimeFaces (componentes, temas, integração com JSF)
> **Pré-requisitos:** [[Paradigma-Orientado-a-Objetos|POO]] (inversão de dependência, SOLID) e [[Java-e-Ecossistema-JVM|Java/JVM]] (CDI, JPA, repositórios, Jakarta EE)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-31

---

## 1. Por que estudar frameworks Java?

A ementa é enfática: *"priorizar o ecossistema Spring, que é o mais cobrado."* Não é por acaso: o **Spring** é, de longe, o framework mais usado no desenvolvimento corporativo Java — e a DATAPREV não foge a isso, com seus sistemas de benefícios, consignação e processamento de dados previdenciários construídos majoritariamente sobre a plataforma Spring.

Este tópico conecta dois pilares que você já domina:

- A [[Paradigma-Orientado-a-Objetos|nota de POO]] introduziu o **D de SOLID — Inversão de Dependência** e o princípio de **depender de abstrações, não de concretos**. O **Spring** é a materialização em escala desse princípio: ele gerencia automaticamente as dependências dos objetos via **injeção de dependência**.
- A [[Java-e-Ecossistema-JVM|nota de Java]] apresentou o **CDI** (injeção de dependência do Jakarta EE) e os **repositórios JPA**. O Spring Data aproveita exatamente esses repositórios para oferecer acesso a dados pronto.

> [!question] Pergunta orientadora
> No POO, aprendemos que "dependa de abstrações, não de concretos". Mas quem vai *de fato* montar essas abstrações? Quem vai criar o objeto `RepositorioDados` concreto e injetá-lo na classe que o usa? Num sistema com centenas de classes, ninguém faria isso manualmente. Quem assume essa responsabilidade? A resposta é o **container de injeção de dependência** — o coração do Spring.

---

## 2. IoC e DI — a base conceitual

### 2.1 O que é IoC (Inversão de Controle)

**Inversão de Controle (IoC)** é um princípio de design em que o **controle do fluxo** (quem cria os objetos e decide quando chamar as dependências) é **invertido**: em vez de o próprio código instanciar suas dependências com `new`, quem faz isso é um **container** externo. O programador define o *o quê* e o container decide o *como e quando*.

Pense no processo tradicional vs. o com inversão:

- **Sem IoC:** a classe `Servico` faz `new Repositorio()` dentro dela — ela controla a criação.
- **Com IoC:** o container cria o `Repositorio` e o **injeta** na `Servico` — o controle de criação saiu do código para o container.

### 2.2 O que é Injeção de Dependência (DI)

**Injeção de Dependência (DI)** é a **técnica concreta** que implementa o princípio IoC: em vez de a classe criar suas dependências, elas são **fornecidas (injetadas)** de fora — geralmente pelo container.

> [!important] IoC ≠ DI (mas estão intimamente ligados)
> **IoC é o princípio** (inverter o controle de criação); **DI é a técnica** que o aplica (injetar a dependência de fora). A FGV pergunta a diferença: IoC é princípio/sócio maior; DI é a implementação. O **Spring** é um **framework de IoC por meio de injeção de dependência**.

### 2.3 Anotações do Spring para IoC/DI

O Spring usa **anotações** para registrar classes como "beans" (objetos gerenciados pelo container) e para injetar dependências. Cada anotação tem uma função e um estereótipo:

| Anotação | Função | Estereótipo |
|---|---|---|
| **`@Component`** | classe genérica gerenciada pelo Spring | componente genérico |
| **`@Service`** | classe da camada de **serviço** (regra de negócio) | especialização de `@Component` |
| **`@Repository`** | classe da camada de **acesso a dados** (persistência) | especialização de `@Component` |
| **`@Controller`** | classe da camada **web/MVC** (recebe requisições) | especialização de `@Component` |
| **`@Autowired`** | injeta uma dependência automaticamente | injeção de dependência |

```java
@Service                                   // camada de serviço (negócio)
public class ServicoBeneficio {
    @Autowired                             // injeta a dependência da camada de dados
    private RepositorioBeneficio repositorio;

    public List<Beneficiario> listarAtivos() {
        return repositorio.findByStatus("ATIVO");
    }
}

@Repository                                // camada de acesso a dados
public interface RepositorioBeneficio extends JpaRepository<Beneficiario, Long> {
    List<Beneficiario> findByStatus(String status);
}
```

> [!note] `@Service`, `@Repository`, `@Controller` são `@Component`
> As anotações `@Service`, `@Repository` e `@Controller` são **especializações** de `@Component`. Tecnicamente, são "o mesmo" ao registrar os beans — mas o **estereótipo** comunica a **camada** da aplicação e habilita comportamentos específicos (ex.: `@Repository` habilita tradução de exceções de persistência). A banca cobra o papel de camada de cada um.

---

## 3. Spring MVC — o padrão no framework

O **Spring MVC** implementa o padrão **MVC (Model-View-Controller)** — que você verá em detalhes no tópico de Padrões de Projeto, mas que antecipamos aqui no contexto do Spring:

- **Model:** os dados e a regra de negócio (as entidades e os serviços);
- **View:** a apresentação (no Spring MVC, tradicionalmente JSP ou templates);
- **Controller:** recebe requisições HTTP, invoca o service/model e decide a view.

As anotações-chave:

- **`@Controller` / `@RestController`:** classe que recebe requisições HTTP.
- **`@RequestMapping`:** mapeia URL e método HTTP.
- **`@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`:** atalhos para os verbos HTTP.

```java
@RestController                 // controller que devolve dados (JSON)
@RequestMapping("/api/beneficios")
public class ControllerBeneficio {

    @Autowired
    private ServicoBeneficio servico;

    @GetMapping("/{cpf}")       // GET /api/beneficios/123
    public Beneficiario buscar(@PathVariable String cpf) {
        return servico.buscarPorCpf(cpf);
    }
}
```

> [!note] `@RestController` vs. `@Controller`
> O **`@RestController`** combina `@Controller` **+ `@ResponseBody`**: ele devolve o objeto diretamente serializado (geralmente JSON), sem passar por uma view. O `@Controller` tradicional devolve uma **view** (página) para renderizar. No desenvolvimento moderno de APIs, o `@RestController` é o padrão. A banca cobra essa distinção.

---

## 4. Spring Data — acesso a dados simplificado

O **Spring Data** simplifica drasticamente o acesso a dados, reutilizando os **repositórios JPA** que você viu na nota de Java. Basta criar uma **interface** que estende `JpaRepository` — e o Spring Data **implementa automaticamente** as operações básicas (CRUD) e deriva consultas a partir do **nome dos métodos**.

```java
public interface RepositorioBeneficiario extends JpaRepository<Beneficiario, Long> {
    // método derivado: findBy + Campo + Operador
    List<Beneficiario> findByNomeContaining(String nome);
    Optional<Beneficiario> findByCpf(String cpf);
    List<Beneficiario> findByStatusOrderByNomeAsc(String status);
}
```

O **Spring Data** interpreta o nome do método (`findByNomeContaining`, `findByCpf`) e gera a consulta correspondente — sem escrever SQL/JPQL. Regras que a banca cobra: `findBy` inicia a busca; o **nome do campo** vem depois; e há operadores como `Containing` (LIKE), `Between`, `LessThan`, `OrderBy...Asc/Desc`.

> [!question] Quem cria a implementação do repositório?
> A interface `RepositorioBeneficiario` não tem um `class` que a implemente — então quem cria o objeto concreto? É o **Spring Data**, que em tempo de execução **gera automaticamente uma implementação** da interface, conectando-a ao Hibernate/JPA. É outro exemplo do princípio de IoC: você define o *contrato* e o framework fornece o *concreto*.

---

## 5. Spring Boot — autoconfiguração e starters

### 5.1 O problema que o Spring Boot resolve

O **Spring** tradicional exigia **configuração manual extensa** (XML ou classes de configuração) antes de rodar qualquer coisa. O **Spring Boot** veio para **acelerar** esse processo: ele **autoconfigura** a aplicação com base nas dependências presentes, reduzindo drasticamente a configuração manual, e entrega uma aplicação **"pronta para rodar"** com um executável embutido.

### 5.2 Starters

Os **starters** são **dependências agregadoras** — um único artefato que traz todas as bibliotecas necessárias para uma funcionalidade. Em vez de listar dezenas de dependências, você adiciona um starter.

| Starter | O que traz |
|---|---|
| `spring-boot-starter-web` | Spring MVC + servidor embutido (Tomcat) + JSON — p/ APIs REST |
| `spring-boot-starter-data-jpa` | Spring Data JPA + Hibernate + configuração de banco |
| `spring-boot-starter-security` | Segurança/autenticação (veremos na Fase 6) |
| `spring-boot-starter-test` | JUnit e ferramentas de teste |

```xml
<!-- Exemplo: um starter já traz tudo para uma API REST com acesso a banco -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

### 5.3 Autoconfiguração

A **autoconfiguração** do Spring Boot inspeciona as dependências no *classpath* e **configura automaticamente** os beans apropriados. Se o starter web está presente, ele configura o servidor Tomcat embutido e o MVC; se há um banco no classpath, configura o `DataSource` e o Hibernate; e assim por diante. É **convenção sobre configuração**: o framework assume o "jeito padrão" e você só ajusta quando precisa (via `application.properties`).

```properties
# application.properties — pouco a configurar graças à autoconfiguração
spring.datasource.url=jdbc:postgresql://localhost:5432/dataprev
spring.datasource.username=app
spring.datasource.password=segredo
```

> [!important] Spring Boot não substitui Spring; simplifica o uso
> O **Spring Boot** é uma **camada sobre o Spring** que o torna mais fácil de configurar e executar — não um framework novo que substitui o Spring. Ele usa o mesmo núcleo (IoC/DI, Spring MVC, Spring Data). A pegadinha da banca: "Spring Boot substitui o Spring" → **falso**; ele *facilita* o uso do Spring.

---

## 6. Spring Cloud — para arquiteturas distribuídas

O **Spring Cloud** traz ferramentas para construir **arquiteturas de microsserviços** (sistemas divididos em serviços pequenos independentes). O edital pede o **conceito** de alguns componentes-chave:

| Componente | Função |
|---|---|
| **Service Discovery (Eureka)** | **Registro e descoberta** de serviços: cada serviço se registra (nome + endereço) e os outros o localizam dinamicamente |
| **Spring Cloud Config** | **Configuração centralizada**: as configurações (properties) ficam em um repositório central e os serviços as consomem |
| **Spring Cloud Gateway** | **Gateway de API**: **porta de entrada única** que roteia requisições para os serviços corretos (roteamento, balanceamento, filtros) |
| **Circuit Breaker (Resiliência)** | **Interruptor de circuito**: quando um serviço falha, "abre o circuito" e evita que a falha se propague (evita chamadas a um serviço já indisponível) |

- **Eureka (Discovery):** numa arquitetura de muitos serviços, cada um precisa saber o endereço dos outros. O **Eureka** é um **registro central** onde cada serviço se *registra* e de onde os demais o *descobrem* — evitando endereços fixos configurados à mão.
- **Config Server:** centraliza as configurações em um único lugar, evitando espalhá-las por milhares de arquivos.
- **Gateway:** atua como o **único ponto de entrada** (a "porta única") da aplicação, roteando as requisições para os serviços internos.
- **Circuit Breaker:** se um serviço está com falha, o *circuit breaker* "abre o circuito" e passa a devolver uma resposta de fallback rapidamente, em vez de tentar (e falhar) repetidamente — o que protegeria o sistema inteiro. É inspirado no disjuntor elétrico: quando há sobrecarga, desarma para não queimar o circuito inteiro.

> [!note] Quando o edital cobra Spring Cloud
> O edital pede o **conceito** dos componentes. Foque no **papel de cada um**: Eureka (descobrir serviços), Config (centralizar configuração), Gateway (ponto único de entrada/roteamento), Circuit Breaker (proteção contra cascata de falhas). Não precisa decorar implementação detalhada.

---

## 7. JSF — JavaServer Faces

O **JSF (JavaServer Faces)** é um framework de **interface web** em Java baseado em **componentes** e no padrão **MVC** — para construir páginas com componentes reutilizáveis (botões, tabelas, formulários), em vez de escrever HTML puro. Ele é um **padrão de componentes server-side**: a página é montada no servidor e enviada ao navegador.

### 7.1 O ciclo de vida do JSF (6 fases)

O JSF define um **ciclo de vida de requisição/resposta** com **seis fases**, que a banca adora cobrar na ordem:

1. **Restore View (Restaurar a Visão):** recupera ou constrói a árvore de componentes da página.
2. **Apply Request Values (Aplicar Valores da Requisição):** os valores enviados pelo cliente são atribuídos aos componentes.
3. **Process Validations (Processar Validações):** valida os valores (Bean Validation).
4. **Update Model Values (Atualizar Valores do Modelo):** os valores validados são transferidos para os **beans** (o modelo).
5. **Invoke Application (Invocar a Aplicação):** executa a **lógica de negócio** (os action methods).
6. **Render Response (Renderizar a Resposta):** gera o HTML final enviado ao cliente.

> [!warning] PEGADINHA — a ordem das 6 fases
> A FGV cobra a sequência correta e o que acontece em cada fase. Um erro clássico de alternativa: trocar *Process Validations* por *Update Model*, ou dizer que a **validação** vem depois da **atualização do modelo**. A ordem é: **Restore → Apply → Validate → Update Model → Invoke → Render**. Memorize o mnemônico das iniciais: **R A P U I R**.

### 7.2 Componentes JSF

O JSF usa **componentes** com prefixo `h:` (HTML) ou `f:` (faces), incorporados em páginas XHTML:

```xml
<!-- Página JSF (Facelets / XHTML): formulário com componente -->
<html xmlns="http://www.w3.org/1999/xhtml"
      xmlns:h="http://xmlns.jcp.org/jsf/html"
      xmlns:f="http://xmlns.jcp.org/jsf/core">
    <h:body>
        <h:form>
            <h:outputLabel value="CPF" for="cpf"/>
            <h:inputText id="cpf" value="#{beneficioBean.cpf}"/>
            <h:commandButton value="Buscar" action="#{beneficioBean.buscar}"/>
        </h:form>
    </h:body>
</html>
```

Os componentes **encapsulam estado e comportamento**: um `h:inputText` guarda o valor, um `h:commandButton` dispara a ação no bean. Isso conecta diretamente ao **POO**: os componentes são, na prática, **objetos reutilizáveis** com estado e comportamento.

> [!note] JSF vs. Spring MVC
> O **JSF é componentizado e server-side** (monta a página no servidor), tradicional/exigente de servidor Java EE. O **Spring MVC** é um framework MVC onde o controller (lado servidor) decide a view. Ambos usam MVC, mas o JSF centraliza na árvore de componentes; já os frameworks de frontend (Vue/React/Angular, da Fase 5) são *client-side*. Para a prova, guarde que JSF = componentes server-side + ciclo de 6 fases.

---

## 8. PrimeFaces

O **PrimeFaces** é uma **biblioteca de componentes visuais** (extensão) para o **JSF**. Ele amplia o JSF com dezenas de componentes prontos — tabelas (`DataTable`), gráficos, calendários, diálogos, auto-complete, temas — que aceleram a construção de interfaces ricas.

- **Componentes:** oferece componentes prontos tipo `p:dataTable`, `p:calendar`, `p:chart`, `p:dialog`, com prefixo `p:` (PrimeFaces).
- **Temas (themes):** permite **personalizar a aparência** (cores, estilos) trocando o tema — sem reescrever a lógica.
- **Integração com JSF:** o PrimeFaces **não substitui o JSF**; ele **estende/suplementa**, usando o próprio ciclo de vida e a infraestrutura do JSF.

```xml
<!-- Componente PrimeFaces dentro de uma página JSF -->
<p:dataTable value="#{beneficioBean.lista}" var="b">
    <p:column headerText="Nome">#{b.nome}</p:column>
    <p:column headerText="CPF">#{b.cpf}</p:column>
</p:dataTable>
```

> [!warning] PEGADINHA — PrimeFaces é uma extensão do JSF
> O **PrimeFaces é uma biblioteca de componentes sobre o JSF** — não é um framework concorrente que substitui o JSF, nem uma alternativa ao Spring. Uma alternativa que diga "o PrimeFaces substitui o JSF" está errada: ele **integra-se ao JSF** e o utiliza. Os "temas" do PrimeFaces personalizam a **aparência visual**, não a lógica de negócio.

---

## 9. Como a FGV cobra este tópico

- **IoC vs. DI:** IoC é princípio (inverter o controle); DI é a técnica (injetar dependência de fora). Spring é framework de IoC via DI.
- **Anotações e camadas:** `@Component` (genérico), `@Service` (negócio), `@Repository` (dados), `@Controller` (web), `@Autowired` (injeção); são especializações de `@Component`.
- **Spring MVC:** `@Controller` vs. `@RestController`; mapeamento de verbos HTTP.
- **Spring Data:** repositórios por interface + nome do método.
- **Spring Boot:** não substitui Spring; usa **starters** (dependências agregadas) e **autoconfiguração** ("convenção sobre configuração").
- **Spring Cloud:** papéis de **Eureka** (descobrir), **Config** (centralizar), **Gateway** (ponto único de entrada), **Circuit Breaker** (proteção contra falha em cascata).
- **JSF:** ciclo de vida em **6 fases** na ordem certa (Restore → Apply → Validate → Update → Invoke → Render); componentes `h:`/`f:`.
- **PrimeFaces:** extensão/biblioteca de componentes **sobre o JSF**, com temas e integração.

> [!warning] PEGADINHA — confusões mais prováveis
> 1. "Spring Boot é um framework novo que substitui o Spring" → **falso**, é uma camada que facilita.
> 2. "PrimeFaces substitui o JSF" → **falso**, é uma biblioteca de componentes sobre ele.
> 3. "IoC e DI são a mesma coisa" → não, um é princípio, o outro é técnica.
> 4. A ordem do ciclo de vida JSF trocada → memorize **R A P U I R**.

---

## 10. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **IoC** (princípio: inverter o controle de criação) vs. **DI** (técnica: injetar de fora)
> - [ ] Anotações: `@Component`, `@Service`, `@Repository`, `@Controller` (especializações de `@Component`), `@Autowired`
> - [ ] **Spring MVC:** `@RestController` (devolve dados) vs. `@Controller` (devolve view)
> - [ ] **Spring Data:** repositórios por interface; métodos derivados do nome (`findBy...`)
> - [ ] **Spring Boot:** autoconfiguração + **starters**; "convenção sobre configuração"; **não substitui o Spring**
> - [ ] **Spring Cloud:** Eureka (descoberta), Config (configuração central), Gateway (ponto único), Circuit Breaker (resiliência)
> - [ ] **JSF:** ciclo de vida em **6 fases** (R A P U I R); componentes server-side
> - [ ] **PrimeFaces:** biblioteca de componentes **sobre o JSF**, com temas

> [!warning] O erro mais comum em prova
> Tratar **Spring Boot como substituto do Spring** e **PrimeFaces como substituto do JSF**, quando ambos são *camadas/extensões* sobre as tecnologias-base. E misturar as **camadas** das anotações (`@Repository` na camada de dados, `@Service` na de negócio, `@Controller` na web).

---

## 11. Próximos passos

Você agora conhece o ecossistema que move o desenvolvimento corporativo Java: o **Spring** com IoC/DI, MVC e Data; o **Spring Boot** que o torna rápido de configurar; o **Spring Cloud** para arquiteturas distribuídas; e as tecnologias de interface **JSF** com o **PrimeFaces**.

O próximo tópico, **Padrões de Projeto e Arquitetura**, sobe um nível de abstração: você vai ver soluções **reutilizáveis** (os padrões GoF, o MVC, arquiteturas de serviços e APIs RESTful) que são a "gramática" em que frameworks como o Spring se encaixam. O **MVC** que o Spring MVC implementa, a **injeção de dependência** como aplicação de princípios, e a organização em camadas serviço/repositório que vimos aqui voltarão lá como **padrões** — a ligação natural entre a prática do framework e a teoria do design de software.
