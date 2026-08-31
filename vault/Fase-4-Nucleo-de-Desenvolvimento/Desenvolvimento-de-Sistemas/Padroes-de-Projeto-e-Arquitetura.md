# Padrões de Projeto e Arquitetura

> [!info] Metadados
> **Disciplina:** Desenvolvimento de Sistemas
> **Bloco:** 4.1 — Desenvolvimento de Sistemas (FASE 4 — Núcleo de Desenvolvimento)
> **Tópico:** 5. Padrões de Projeto e Arquitetura
> **Subtópicos:** Padrões GoF (criação, estruturais, comportamentais: Singleton, Factory, Strategy, Observer etc.) · MVC, MVP, MVVM · SOA · Web Services (SOAP, REST, GraphQL — conceito) · Mensageria (assíncrona, fila, tópico, broker, JMS) · APIs RESTful (verbos HTTP, status codes, recursos) · Swagger/OpenAPI
> **Pré-requisitos:** [[Paradigma-Orientado-a-Objetos|POO]] (polimorfismo, herança, encapsulamento) e [[Frameworks-Java|Frameworks Java]] (MVC, Spring, IoC/DI)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-31

---

## 1. Por que estudar padrões de projeto e arquitetura?

Os **padrões de projeto** são **soluções reutilizáveis e testadas** para problemas recorrentes de design de software. Eles são a "língua comum" que os desenvolvedores usam para resolver problemas de forma comprovada, em vez de reinventar a roda a cada projeto. E a **arquitetura** — o nível superior — define como as grandes peças do sistema (o frontend, o backend, os serviços, as APIs) se organizam e se comunicam.

Para a DATAPREV, isso é essencial: os sistemas de benefícios e consignação precisam ser **estáveis, escaláveis e integrados** — e os padrões e arquiteturas são o que garante isso. Este tópico conecta:

- A [[Paradigma-Orientado-a-Objetos|nota de POO]]: os padrões GoF são construídos **sobre os pilares do POO** (polimorfismo, herança, encapsulamento) e aplicam o **SOLID**.
- A [[Frameworks-Java|nota de Frameworks]]: o **MVC** que o Spring implementa e a **injeção de dependência** são, na prática, manifestações de padrões arquiteturais. Quando estudamos `@Controller`, `@Service`, `@Repository`, estávamos aplicando o padrão em camadas.

> [!question] Pergunta orientadora
> Se você precisa garantir que exista **apenas uma única** instância de um objeto (por exemplo, uma configuração global do sistema), como faz sem que ninguém crie uma segunda cópia? E se você precisa criar objetos de tipos variados sem que o código saiba qual classe concreta usar? Esses são problemas tão comuns que ganharam nomes e soluções consagradas — os **padrões de projeto**.

---

## 2. Padrões de projeto GoF — visão geral

Os **padrões GoF** (do livro *Design Patterns* de Erich Gamma et al., "Gang of Four" — "Banda dos Quatro") classificam padrões em **três categorias**, conforme seu **propósito**:

| Categoria | Propósito | Exemplos |
|---|---|---|
| **Criação** (creational) | Lidam com a **criação** de objetos | **Singleton**, **Factory Method**, Abstract Factory, Builder, Prototype |
| **Estrutural** (structural) | Organizam a **composição/estrutura** de classes e objetos | Adapter, Decorator, Facade, Composite, Proxy |
| **Comportamental** (behavioral) | Gerenciam **comportamento/algoritmos** e responsabilidade entre objetos | **Strategy**, **Observer**, Template Method, Command, Iterator |

> [!note] Palavras-chave da classificação
> **Criação** = como criar o objeto · **Estrutural** = como compor/estruturar · **Comportamental** = como os objetos se comportam e se comunicam. A FGV pede para **classificar** um padrão na categoria certa. Guarde os quatro mais cobrados: **Singleton e Factory** (criação), **Strategy e Observer** (comportamental).

### 2.1 Singleton (criação)

O **Singleton** garante que uma classe tenha **apenas uma única instância** em todo o programa, com um ponto de acesso global a ela.

```java
public class Configuracao {
    private static Configuracao instancia;      // a única instância

    private Configuracao() { /* construtor privado impede novas instâncias */ }

    public static Configuracao getInstancia() {
        if (instancia == null) {
            instancia = new Configuracao();
        }
        return instancia;
    }
}
```

- **Construtor privado** (impede `new` de fora);
- **`static` getInstance()** que retorna sempre a **mesma** instância.

> [!warning] PEGADINHA — Singleton garante uma única instância
> A essência do Singleton é a **garantia de unicidade** (uma só instância por JVM). A **pegadinha de prova** costuma inverter: "o Singleton permite criar várias instâncias da classe" — **falso**. E note: o construtor **privado** é o que impede a criação externa. (Em arquiteturas modernas, esse padrão é criticado por esconder acoplamento — mas no edital, o conceito básico domina.)

### 2.2 Factory Method (criação)

O **Factory Method** desloca a **criação do objeto** para um método (a "fábrica"), de modo que o código que usa o objeto **não sabe qual classe concreta** está sendo criada. Isso dá flexibilidade: é possível adicionar novos tipos sem alterar o código que os consome (aplicando o Open/Closed).

```java
public interface Pagamento { void processar(); }

public class PagamentoPix implements Pagamento { public void processar() { /* ... */ } }
public class PagamentoCartao implements Pagamento { public void processar() { /* ... */ } }

// Factory: decide qual classe concreta criar
public class PagamentoFactory {
    public static Pagamento criar(String tipo) {
        if (tipo.equals("PIX")) return new PagamentoPix();
        if (tipo.equals("CARTAO")) return new PagamentoCartao();
        throw new IllegalArgumentException("Tipo desconhecido");
    }
}

// Uso: o chamador não sabe qual classe concreta é criada
Pagamento p = PagamentoFactory.criar("PIX");
p.processar();
```

> [!question] Por que a Factory é útil?
> Se o código que processa pagamentos chamasse `new PagamentoPix()` diretamente, ele estaria **acoplado** à classe concreta. Com a **Factory**, quem usa depende apenas da abstração `Pagamento` e de um método `criar`. Adicionar um `PagamentoBoleto` exige só alterar a factory, não o código consumidor. É a **inversão de dependência** (D de SOLID) na prática.

### 2.3 Strategy (comportamental)

O **Strategy** define uma **família de algoritmos** encapsulados em classes separadas e intercambiáveis, permitindo trocar o algoritmo em **tempo de execução** sem alterar o código que o utiliza.

```java
// Estratégia: interface comum para os algoritmos
public interface CalculoDesconto {
    double calcular(double valor);
}

// Estratégias concretas (algoritmos intercambiáveis)
public class DescontoPix implements CalculoDesconto {
    public double calcular(double valor) { return valor * 0.05; }
}
public class DescontoPrimeiraCompra implements CalculoDesconto {
    public double calcular(double valor) { return valor * 0.10; }
}

// Contexto: usa uma estratégia, podendo trocá-la
public class Pedido {
    private CalculoDesconto desconto;
    public void setDesconto(CalculoDesconto d) { this.desconto = d; }  // troca em runtime
    public double valorFinal(double valor) { return valor - desconto.calcular(valor); }
}

// Uso
Pedido pedido = new Pedido();
pedido.setDesconto(new DescontoPix());          // aplica desconto Pix
pedido.setDesconto(new DescontoPrimeiraCompra()); // troca a estratégia
```

> [!warning] PEGADINHA — Strategy vs. padrões relacionados
> O **Strategy** permite **trocar o algoritmo em tempo de execução** (por composição/atributo). Não confunda com **Factory** (que *cria* objetos). E não confunda com o simples `if/else`: o Strategy **encapsula cada algoritmo em uma classe própria**, evitando cadeias de `if` — por isso ele é um bom exemplo do Open/Closed. Na prova, "trocar algoritmo sem modificar o código" aponta para **Strategy**.

### 2.4 Observer (comportamental)

O **Observer** define uma **dependência um-para-muitos** entre objetos: quando um objeto (o **sujeito**/"observado") muda de estado, **todos os seus dependentes (os "observadores") são notificados automaticamente**.

```java
import java.util.List;
import java.util.ArrayList;

// Observador: a interface que quem quer ser notificado implementa
interface Observador { void atualizar(String estado); }

// Sujeito observado: mantém a lista de observadores e os notifica
class Sujeito {
    private List<Observador> observadores = new ArrayList<>();
    private String estado;

    public void adicionar(Observador o) { observadores.add(o); }
    public void remover(Observador o)   { observadores.remove(o); }

    public void setEstado(String estado) {
        this.estado = estado;
        notificarTodos();            // muda e notifica automaticamente
    }

    private void notificarTodos() {
        for (Observador o : observadores) o.atualizar(estado);
    }
}

// Observador concreto
class EmailObservador implements Observador {
    public void atualizar(String estado) {
        System.out.println("Email enviado: estado mudou para " + estado);
    }
}

// Uso
Sujeito sujeito = new Sujeito();
sujeito.adicionar(new EmailObservador());
sujeito.setEstado("APROVADO");   // observador é notificado automaticamente
```

**Um-para-muitos:** um sujeito, vários observadores; **acoplamento fraco:** o sujeito conhece apenas a interface `Observador`, não as classes concretas.

> [!note] Observer no mundo real
> O **Observer** é a base de sistemas de eventos: quando o status de um benefício muda, vários componentes (email, extrato, notificação) "observam" e reagem automaticamente. A **pegadinha**: o Observer é **comportamental**, envolve **notificação automática ao mudar o estado** em uma relação **um para muitos** — e o conjunto de observadores pode **crescer ou diminuir** sem afetar o sujeito.

---

## 3. Padrões arquiteturais: MVC, MVP e MVVM

Os padrões arquiteturais organizam a aplicação em **camadas**, separando a interface do usuário (visão) da lógica de negócio e dos dados.

### 3.1 MVC — Model-View-Controller

O **MVC** divide a aplicação em três componentes:

- **Model:** os **dados** e a **lógica de negócio** (no Java, as entidades e serviços);
- **View:** a **apresentação** (a interface que o usuário vê);
- **Controller:** recebe as **entradas** do usuário, atualiza o Model e seleciona a View.

```
Usuário → Controller → Model (atualiza)
                ←  View é atualizada e re-renderizada
```

Fluxo típico: o **Controller** recebe a interação do usuário, chama o **Model** para processar, e atualiza a **View**.

> [!note] O MVC no Spring
> Você já viu o **MVC** em ação no [[Frameworks-Java|Spring MVC]]: `@Controller` recebe requisições, os `@Service` e entidades formam o Model, e as views (JSP/templates) formam a View. O padrão arquitetural agora ganha um nome estruturado.

### 3.2 MVP — Model-View-Presenter

O **MVP** é uma variação do MVC onde:

- **Model:** dados/lógica;
- **View:** interface, que é **passiva** (só exibe e captura entrada);
- **Presenter:** **intermediário** que contém toda a lógica de apresentação e **atualiza a View**; a View **comunica-se com o Presenter** (não diretamente com o Model).

A principal diferença para o MVC: a **View não acessa o Model** — quem faz a ponte é o **Presenter**, que atualiza a View. Isso desacopla a View do Model e facilita testes (a View pode ser testada isoladamente via interface).

### 3.3 MVVM — Model-View-ViewModel

O **MVVM** adiciona o **ViewModel**:

- **Model:** dados/lógica;
- **View:** interface;
- **ViewModel:** expõe dados e comandos para a View, e é o **elo de ligação bidirecional** (binding) — a View se **liga** ao ViewModel e ambos se sincronizam automaticamente.

A principal característica do **MVVM** é o **data binding (ligação de dados) bidirecional**: quando um valor muda na View, o ViewModel é atualizado, e vice-versa. É a base de frameworks modernos como Angular/Vue/React (que você verá no frontend).

> [!warning] PEGADINHA — diferenciar MVP de MVVM
> No **MVP**, o **Presenter** é quem **manipula a View** (que é passiva). No **MVVM**, o **ViewModel** expõe dados e há **binding bidirecional** automático com a View (comum em frameworks modernos). A pegadinha: MVVM não tem "Presenter"; a sincronização é via binding. E o **MVP** tem View passiva manipulada pelo Presenter.

| Padrão | Componentes extras | Como a View se atualiza |
|---|---|---|
| **MVC** | Controller | Controller seleciona/atualiza a View |
| **MVP** | Presenter | Presenter manipula a View (View passiva) |
| **MVVM** | ViewModel | **Binding bidirecional** entre View e ViewModel |

---

## 4. SOA — Service Oriented Architecture

**SOA (Arquitetura Orientada a Serviços)** é um **estilo arquitetural** em que o sistema é organizado como um conjunto de **serviços** independentes, reutilizáveis e interoperáveis que se comunicam por **contratos** bem definidos (Web Services). As características centrais:

- **Serviços:** unidades de negócio autônomas (ex.: "serviço de consulta de CNIS", "serviço de benefícios");
- **Baixo acoplamento:** cada serviço é independente e não conhece a implementação dos outros;
- **Contratos padronizados:** os serviços expõem **interfaces** definidas (WSDL para SOAP, ou contratos HTTP para REST) e **falam** via **Web Services**;
- **Reuso e orquestração:** serviços podem ser compostos/orquestrados para formar novos processos de negócio.

> [!question] Por que a SOA interessaria à DATAPREV?
> Uma organização que integra o INSS, bancos, órgãos públicos e seguradoras precisa que sistemas diferentes conversem por **padrões** — um "serviço de consignação" consumido por vários bancos, um "serviço de benefício" consultado por vários sistemas. É exatamente isso que a **SOA** e os **Web Services** proporcionam: **interoperabilidade** entre sistemas heterogêneos.

> [!note] SOA vs. microsserviços (antecipação conceitual)
> A **SOA** organiza a empresa em **serviços reutilizáveis de negócio**, frequentemente via um **barramento corporativo**. Os **microsserviços** (que serão detalhados na arquitetura avançada) são serviços **menores e independentes**, com implantação e comunicação mais leves. Para o edital, guarde que **SOA = serviços + contratos + interoperabilidade**.

---

## 5. Web Services: SOAP e REST

**Web Services** são mecanismos padronizados para **integração entre sistemas** através da web. Os dois estilos principais são **SOAP** e **REST** — e a diferença entre eles é uma das pegadinhas mais recorrentes.

### 5.1 SOAP

**SOAP (Simple Object Access Protocol)** é um **protocolo** de mensagens baseado em **XML**, com **contrato rígido** definido em **WSDL** (Web Services Description Language). Características:

- **Baseado em XML:** as mensagens são documentos XML com estrutura prescrita (envelope SOAP);
- **Contrato (WSDL):** define formalmente os serviços, operações e tipos;
- **Transporte:** frequentemente **HTTP**, mas pode usar outros protocolos (SMTP etc.);
- **Padrões (WS-*):** suporte a segurança, transações, confiabilidade;
- **Forte tipagem e formalismo:** adequado a cenários que exigem contratos rígidos e maior segurança/garantias.

```xml
<!-- Mensagem SOAP (envelope com cabeçalho e corpo) -->
<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope">
  <soap:Body>
    <consultar xmlns="http://dataprev.gov.br/ws">
      <cpf>12345678900</cpf>
    </consultar>
  </soap:Body>
</soap:Envelope>
```

### 5.2 REST

**REST (Representational State Transfer)** é um **estilo arquitetural** (não um protocolo) baseado em:
- **Recursos** identificados por **URLs**;
- **Verbos HTTP** (GET, POST, PUT, DELETE...);
- **Representações** dos recursos (geralmente **JSON**, mas pode ser XML);
- **Stateless** (sem estado de sessão no servidor); Estados transferidos nas representações.

> [!note] SOAP é um protocolo; REST é um estilo
> **SOAP é um *protocolo*** (com contrato WSDL e mensagens XML padronizadas). **REST é um *estilo arquitetural*** apoiado nos princípios da web (recursos, verbos HTTP). Essa é uma distinção favorita da banca: "SOAP é um protocolo; REST é um estilo arquitetural".

### 5.3 SOAP vs. REST — a tabela decisiva

| Critério | SOAP | REST |
|---|---|---|
| Natureza | **Protocolo** | **Estilo arquitetural** |
| Formato | **XML** obrigatório | **JSON** (também XML), diverso |
| Contrato | **WSDL** (formal/rígido) | informal; documentado via OpenAPI |
| Verbos/métodos | operações definidas no WSDL | **verbo HTTP** (GET, POST, PUT, DELETE) |
| Transporte | HTTP, SMTP etc. | **HTTP** |
| Estado | pode ter estado (WS-*) | **stateless** (sem estado no servidor) |
| Quando usar | contratos rígidos, segurança robusta, sistemas legados/empresariais | APIs simples, web, alto desempenho, integração leve |

> [!warning] PEGADINHA — as afirmações "absolutas" sobre REST
> A banca gosta de oferecer afirmações rígidas: "REST obriga o uso de JSON" — **falso**, REST pode usar XML, embora JSON seja típico; "SOAP é mais leve que REST" — **falso**, SOAP é verborrágico (XML) e REST é mais leve; "REST é um protocolo" — **falso**, é um estilo. Fique atento às palavras "*obrigatório*" e "*protocolo*", que normalmente traem a armadilha.

### 5.4 GraphQL (conceito)

**GraphQL** é uma **linguagem de consulta** para APIs, criada pelo Facebook, que permite ao **cliente solicitar exatamente os campos que precisa** de uma única requisição. Em vez de múltiplos endpoints REST, o GraphQL expõe um **único endpoint** e o cliente descreve a consulta.

```graphql
# O cliente pede apenas os campos que deseja
{
  beneficiario(cpf: "123") {
    nome
    status
  }
}
```

- **Vantagem:** evita o **over-fetching/under-fetching** (buscar dados demais ou de menos) típico do REST, e reduz o número de requisições.
- **Conceito para a prova:** o **GraphQL é uma linguagem de consulta** com *esquema tipado*; o cliente **especifica a forma do retorno**. Ele **complementa** (não necessariamente substitui) REST e SOAP.

> [!note] GraphQL é "conceito" no edital
> A ementa pede GraphQL como **conceito**. Guarde: é uma **linguagem de consulta** em que o cliente pede exatamente os campos desejados via **um único endpoint**, evitando excesso/falta de dados.

### 5.5 Mensageria

Até aqui vimos a integração entre sistemas por meio de **chamadas diretas e síncronas**: um sistema *chama* o outro pela rede (SOAP, REST) e **espera a resposta** na hora. Mas há cenários em que essa espera é um problema — quando um sistema é lento, quando há picos de demanda, ou quando não é necessário que quem envia esperneie por uma devolutiva imediata. É exatamente aí que entra a **mensageria**.

A **mensageria** (mensageria orientada a mensagens, ou *message-driven*) é um estilo de **integração assíncrona e desacoplada** entre sistemas. Em vez de um sistema chamar outro diretamente, eles se comunicam por meio de uma **infraestrutura de mensagens** (o **broker**), que recebe e distribui **mensagens** de forma independente. O ponto central: o sistema que envia uma mensagem **não espera resposta imediata** — ele a "entrega" ao broker e segue o seu trabalho; o receptor a processa quando puder.

Para entender, precisamos dos componentes-chave:

- **Produtor** (producer): o sistema que **envia** (publica) a mensagem ao broker;
- **Consumidor** (consumer): o sistema que **recebe** (processa) a mensagem do broker;
- **Broker** (barramento de mensagens): o **intermediário** que recebe, armazena e entrega as mensagens aos consumidores;
- **Mensagem**: a unidade de comunicação — um conjunto de dados estruturados trocado entre produtor e consumidor;
- **Fila** (queue): um canal em que cada mensagem é entregue a **um único** consumidor (a mensagem é "consumida" uma vez);
- **Tópico** (topic): um canal em que cada mensagem pode ser recebida por **vários** consumidores interessados.

Os dois **padrões fundamentais** de mensageria são:

- **Fila (ponto a ponto):** o produtor envia a mensagem para uma fila, e **um único** consumidor a processa. Se houver vários consumidores, eles **competem** entre si — cada mensagem é processada por apenas um. É como uma esteira de atendimento: várias mensagens (tarefas) e vários trabalhadores (consumidores) disputando cada uma.
- **Publicação/Assinatura (pub/sub):** o produtor publica a mensagem em um **tópico**, e **todos** os consumidores que se inscreveram nesse tópico a recebem. Cada assinante recebe uma cópia. É como um canal de notícias: quando sai uma notícia, **todos** os assinantes são notificados.

> [!warning] PEGADINHA — integração síncrona vs. assíncrona
> Essa é uma armadilha conceitual frequente. Os **Web Services** (SOAP/REST) são exemplos de integração **síncrona**: o sistema que chama **fica esperando** a resposta do chamado — há **acoplamento temporal** (ambos precisam estar disponíveis no mesmo instante). A **mensageria** é uma integração **assíncrona**: o produtor envia a mensagem ao broker e **não espera** resposta imediata — há **desacoplamento temporal** (produtor e consumidor não precisam estar ativos ao mesmo tempo; o broker guarda a mensagem até o consumo). A banca adora trocar: dizer que "mensageria é síncrona e exige resposta imediata" ou que "Web Services são assíncronos" — ambos **falsos**.

O edital pede a "Mensageria" dentro de "Arquitetura de software", ao lado de Web Services — porque ambos são mecanismos de **integração entre sistemas**, mas com filosofias opostas quanto ao tempo. Uma forma simples de guardar:

| | Web Services (SOAP/REST) | Mensageria |
|---|---|---|
| Comunicação | **Síncrona** (espera resposta) | **Assíncrona** (não espera) |
| Acoplamento | **Temporal** (ambos presentes) | **Desacoplada** no tempo |
| Quem entrega | Chamada direta via protocolo | **Broker** intermediário |
| Estrutura | Requisição/resposta | Fila (1 consumidor) ou tópico (vários) |

Em termos de padrões de projeto, nota-se uma ponte: o **Observer** (estudado na seção 2.4) é o primo conceitual da mensageria *pub/sub* — quando algo muda, vários interessados são notificados. A diferença é que o Observer notifica **dentro da mesma aplicação** (via chamada de método), enquanto a mensageria pública para consumidores **externos**, em outros sistemas, via broker.

**Ferramentas e padrões do mundo Java:** a **JMS** (*Java Message Service*) é a **API padrão do Java** para mensageria — um conjunto de interfaces que permite a um programa Java enviar e receber mensagens de forma padronizada, independentemente do broker usado por baixo. Para a prova, guarde **JMS = API Java de mensageria**. Quanto aos brokers, cite apenas conceitualmente o **RabbitMQ** (um broker de mensageria muito usado, baseado no padrão AMQP) e o **Apache Kafka** (uma plataforma de streaming de mensagens de alto volume). O aprofundamento dessas ferramentas é assunto de arquitetura avançada — aqui basta saber que elas **materializam** a mensageria em infraestrutura concreta.

> [!example] Mensageria na DATAPREV
> Pense no **processamento em lote de benefícios**: um órgão envia uma remessa com milhares de pedidos, que precisam ser processados em etapas. Com mensageria, cada pedido vira uma **mensagem** depositada em uma **fila**; um conjunto de consumidores processa as mensagens **concorrentemente**, e o sistema não precisa bloquear o solicitante esperando cada um terminar. Outro uso: a **integração entre sistemas heterogêneos** (INSS, bancos, órgãos) que não precisam estar sincronizados — um sistema publica eventos num **tópico** e vários outros reagem quando podem, sem bloqueio mútuo. A mensageria garante **escalabilidade** (mais consumidores = mais processamento) e **resiliência** (se um consumidor falha, a mensagem fica guardada no broker para reprocessamento).

**Palavras-chave do edital:** *assíncrono*, *desacoplamento*, *fila*, *tópico*, *produtor*, *consumidor*, *broker*, *JMS*, *pub/sub*.

---

## 6. APIs RESTful: verbos HTTP, status codes e recursos

### 6.1 O que é RESTful

Uma **API RESTful** é uma API que **segue os princípios REST**: expõe **recursos** (as "coisas" do sistema, como `beneficiarios`, `beneficios`) identificados por URLs, e opera sobre eles com **verbos HTTP**.

```
Recursos (substantivos na URL):
  /api/beneficiarios        → coleção de beneficiários
  /api/beneficiarios/123    → o beneficiário de id 123
```

### 6.2 Verbo HTTP e a ação (CRUD)

| Verbo HTTP | Ação | Uso típico | Idempotente |
|---|---|---|---|
| **GET** | **consultar** (ler) | buscar um recurso ou lista | sim |
| **POST** | **criar** | criar um novo recurso | não (cria novo a cada vez) |
| **PUT** | **atualizar** (substituir integralmente) | substituir recurso por estado completo | sim |
| **PATCH** | **atualizar parcialmente** | modificar parte do recurso | — |
| **DELETE** | **remover** | apagar recurso | sim |

> [!warning] PEGADINHA — POST vs. PUT e o CRUD do banco
> A relação "verbo HTTP ↔ operação SQL" é clássica: **GET → SELECT**, **POST → INSERT** (criar), **PUT → UPDATE**, **DELETE → DELETE**. A **pegadinha**: o **POST** é usado para **criar** e **não é idempotente** (repetir cria duplicatas); o **PUT** atualiza e é **idempotente** (repetir tem o mesmo efeito). A banca inverte: "POST responde por atualização" ou "PUT cria sempre" — cuidado.

### 6.3 Status codes HTTP

Os **status codes** (códigos de resposta HTTP) são agrupados em faixas — e a FGV cobra principalmente os de sucesso, erro de cliente e erro de servidor.

```
1xx → informativo
2xx → sucesso
3xx → redirecionamento
4xx → erro do cliente
5xx → erro do servidor
```

| Código | Classe | Significado |
|---|---|---|
| **200** OK | 2xx sucesso | requisição bem-sucedida |
| **201** Created | 2xx sucesso | recurso **criado** (resposta do POST) |
| **204** No Content | 2xx sucesso | sucesso sem corpo (ex.: DELETE) |
| **301/302** | 3xx | redirecionamento (permanente/temporário) |
| **400** Bad Request | 4xx | requisição malformada (erro do cliente) |
| **401** Unauthorized | 4xx | **não autenticado** |
| **403** Forbidden | 4xx | **autenticado, mas sem permissão** |
| **404** Not Found | 4xx | recurso não encontrado |
| **409** Conflict | 4xx | conflito de estado (ex.: duplicidade) |
| **500** Internal Server Error | 5xx | erro interno do servidor |

> [!warning] PEGADINHA — 401 vs. 403 e 404
> **401 Unauthorized** = **não autenticado** (o servidor não sabe *quem* você é — falta login/token). **403 Forbidden** = **autenticado, mas sem permissão** (o servidor sabe quem você é, mas **nega o acesso**). A banca troca: "401 é falta de permissão" (errado — é falta de autenticação) e "403 é falta de autenticação" (errado). E o clássico: **404** indica recurso **não encontrado** (não "proibido").

---

## 7. Swagger / OpenAPI

O **Swagger** e o **OpenAPI** referem-se à **documentação e especificação de APIs**. A distinção importante:

- **OpenAPI Specification (OAS):** o **padrão/formal** — um formato (`JSON` ou `YAML`) que **descreve** uma API (rotas, métodos, parâmetros, modelos de dados, tipos de resposta).
- **Swagger:** o **conjunto de ferramentas** que implementa o padrão OpenAPI — incluindo a **interface gráfica Swagger UI**, que renderiza a documentação de forma interativa, e o editor.

> [!important] OpenAPI é a especificação; Swagger é o ecossistema de ferramentas
> O **OpenAPI Specification** é o **padrão** de descrição de APIs; o **Swagger** é o **conjunto de ferramentas** (UI, editor, codegen) que usa esse padrão. Frase clássica de prova: "Swagger é uma ferramenta que documenta APIs com base na especificação OpenAPI" — correta; "OpenAPI é uma ferramenta" — cuidado, é uma **especificação/forma**.

```yaml
# Documentação OpenAPI (exemplo reduzido, formato YAML)
openapi: 3.0.0
info:
  title: API de Benefícios DATAPREV
  version: 1.0.0
paths:
  /beneficiarios:
    get:
      summary: Lista beneficiários
      responses:
        '200':
          description: OK
```

**Por que documentar com OpenAPI?** A especificação serve de **contrato** entre o time de backend e o de frontend, permite **gerar** clientes/servidores automaticamente, e fornece a **documentação interativa** (Swagger UI) que qualquer interessado pode explorar — sem escrever código.

> [!question] Para que serve documentar uma API que "se explica pelo código"?
> Uma API sem documentação é difícil de **descobrir** e **consumir**: quem a usa precisa adivinhar os endpoints, os campos aceitos e os erros possíveis. O **OpenAPI** cria um **contrato executável** — tanto para humanos (documentação interativa do Swagger UI) quanto para ferramentas (geração de código e testes). É a aplicação do princípio de **contrato explícito** das boas arquiteturas.

---

## 8. Como a FGV cobra este tópico

- **Classificação GoF:** criação (Singleton, Factory), estrutural, comportamental (Strategy, Observer). A FGV pede para encaixar o padrão na categoria.
- **Essência de cada padrão:** Singleton (uma única instância), Factory (desloca a criação), Strategy (trocar algoritmo em runtime), Observer (notificação automática um-para-muitos).
- **MVC/MVP/MVVM:** a diferença entre Presenter (MVP, View passiva) e ViewModel (MVVM, binding bidirecional).
- **SOA:** organização em serviços + contratos; interoperabilidade.
- **SOAP vs. REST:** protocolo vs. estilo; XML vs. JSON; WSDL no SOAP.
- **RESTful:** verbos HTTP (GET=ler, POST=criar, PUT=atualizar, DELETE=remover), status codes (200, 201, 401, 403, 404, 500).
- **OpenAPI/Swagger:** OpenAPI é a especificação; Swagger é o conjunto de ferramentas.
- **GraphQL:** linguagem de consulta em que o cliente pede exatamente os campos (via conceito).
- **Mensageria:** integração **assíncrona e desacoplada** via broker; fila (um consumidor) vs. tópico/pub-sub (vários); JMS como API Java; diferença essencial vs. Web Services síncronos.

> [!warning] PEGADINHA — as quatro armadilhas mais rentáveis
> (1) **401 vs. 403** — autenticação vs. permissão. (2) **POST (criar, não idempotente) vs. PUT (atualizar, idempotente)**. (3) **OpenAPI é a especificação; Swagger são as ferramentas**. (4) **REST é estilo arquitetural, não protocolo; SOAP é protocolo**. Decore essas quatro distinções e elimine os erros de prova com rapidez.

---

## 9. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **GoF:** criação (Singleton, Factory) · estrutural (composição) · comportamental (Strategy, Observer)
> - [ ] **Singleton:** uma única instância (construtor privado)
> - [ ] **Factory:** criação deslocada para um método; dependência de abstração
> - [ ] **Strategy:** trocar algoritmo em tempo de execução (Open/Closed)
> - [ ] **Observer:** notificação automática, um-para-muitos
> - [ ] **MVC** (Controller) vs. **MVP** (Presenter, View passiva) vs. **MVVM** (ViewModel, binding bidirecional)
> - [ ] **SOA:** serviços + contratos + interoperabilidade
> - [ ] **SOAP** (protocolo, XML, WSDL) vs. **REST** (estilo, recursos + verbos HTTP, stateless)
> - [ ] **Mensageria:** assíncrona e desacoplada via **broker**; **fila** (um consumidor) vs. **tópico/pub-sub** (vários); **JMS** = API Java; não espera resposta imediata
> - [ ] **GraphQL:** linguagem de consulta; cliente pede os campos (conceito)
> - [ ] **Verbos HTTP:** GET (ler), POST (criar, não idempotente), PUT (atualizar, idempotente), DELETE (remover)
> - [ ] **Status:** 200 OK · 201 Created · 204 No Content · 400 Bad Request · 401 (não autenticado) · 403 (sem permissão) · 404 · 500
> - [ ] **OpenAPI** (especificação) vs. **Swagger** (ferramentas: UI, editor)

> [!warning] O erro mais comum em prova
> Confundir **criação, estrutural e comportamental** na classificação GoF, e trocar **SOAP por REST** nas características (protocolo vs. estilo; XML vs. JSON; WSDL vs. verbos HTTP). E confundir **integração síncrona (Web Services)** com a **assíncrona (mensageria)**. Na questão, pergunte: *estamos criando objetos (criação), compondo (estrutural) ou gerenciando comportamento (comportamental)?* · *é protocolo rígido (SOAP) ou estilo sobre HTTP (REST)?* · *espera resposta imediata (síncrona/Web Service) ou não espera (assíncrona/mensageria)?*

---

## 10. Próximos passos

Você agora domina os **padrões de projeto** (GoF) e as **arquiteturas** (MVC/MVP/MVVM, SOA, Web Services, Mensageria, APIs RESTful e sua documentação com OpenAPI/Swagger). Esse é o vocabulário em que o **Spring** que você estudou se encaixa, e ele será a base das **APIs** que veremos nas integrações.

O próximo tópico mergulha no **formato dos dados que fluem nessas integrações**: **XML** (com namespaces e validação XSD), **XSLT** (transformação), **JSON** (o formato favorito das APIs REST) e o mecanismo de **UDDI** (registro e descoberta de serviços no contexto SOA). Ou seja: agora que você sabe como os sistemas se *comunicam* (SOAP/REST), vamos estudar *o que* viaja por esses canais — os **formatos de dados e a integração**.
