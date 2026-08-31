# Design de Software Avançado

> [!info] Metadados
> **Disciplina:** Arquitetura Avançada, Segurança e Inovação
> **Bloco:** 5.3 — Arquitetura Avançada, Segurança e Inovação (FASE 5 — Frontend e Interfaces)
> **Tópico:** 3. Design de Software
> **Subtópicos:** Design patterns avançados (Builder, Prototype, Registry, Service Locator) · DDD (entidades, value objects, agregados) · Event-Driven Architecture (event sourcing, CQRS)
> **Pré-requisitos:** [[Padroes-de-Projeto-e-Arquitetura]] (padrões GoF, SOA, mensageria), [[Paradigma-Orientado-a-Objetos]] (encapsulamento, herança, polimorfismo, SOLID), [[Transacoes-e-ACID]] (atomicidade/consistência), [[Seguranca-de-Comunicacoes]] (integridade de dados)
> **Cargo:** Analista de TI — Perfil 3: Desenvolvimento de Software
> **Data:** 2026-08-31

## 1. Por que estudar design de software avançado?

No Bloco 4.1 você aprendeu os **padrões GoF clássicos** — Singleton, Factory, Strategy, Observer — e a **orientação a objetos** (encapsulamento, SOLID). Aqui nós **elevamos o nível**: não para criar uma única classe, mas para **projetar um domínio de negócio inteiro** e arquiteturas orientadas a eventos.

A pergunta-chave: quando um sistema (como o do Meu INSS ou de benefícios) manipula **regras de negócio complexas** — quem é o "dono" dessas regras? Onde elas vivem? Como manter o código **fiel ao negócio** quando há milhares de entidades, processos e integrações?

> [!question]
> O código reflete a linguagem do banco de dados (tabelas, colunas) ou a linguagem do **especialista de negócio** (benefício, parcela, revisão)? Quando essas linguagens divergem, quem sofre é a compreensão do sistema. Como alinhá-las?

Este tópico responde com **DDD** (alinhar código e linguagem do negócio), **padrões avançados** (estruturar a criação e a localização de objetos) e **arquitetura orientada a eventos** (organizar o fluxo de dados entre serviços).

## 2. Design patterns avançados

No 4.1 você viu a **classificação dos GoF** (criação, estruturais, comportamentais) e os exemplos mais clássicos. Aqui avançamos para padrões **de criação e de localização** que costumam aparecer em aplicações empresariais — e que a banca usa para testar se você domina além do "básico".

### 2.1 Builder — construção passo a passo

O **Builder** separa a **construção** de um objeto complexo da sua **representação**. Em vez de um construtor gigante com dezenas de parâmetros (o "construtor telefônico"), você monta o objeto **passo a passo**, método a método.

```java
// Sem Builder: construtor gigante e confuso
Pessoa p = new Pessoa("Ana", "Silva", 30, "Rua A", 123, "Bairro", "Cidade", "SP", "12345-678");

// Com Builder: legível e passo a passo
Pessoa p = Pessoa.builder()
        .nome("Ana")
        .sobrenome("Silva")
        .idade(30)
        .endereco("Rua A, 123")
        .cidade("São Paulo")
        .build();
```

> [!tip] Builder no mundo real
> Você já viu isso em prática nos frameworks Java da Fase 4: o **Builder** é usado extensivamente para montar objetos de configuração e entidades imutáveis (ex.: builders de estruturas em frameworks como o Lombok `@Builder`). Para a prova, guarde: Builder = **construção passo a passo de objetos complexos**, legível e controlada.

### 2.2 Prototype — clonar em vez de recriar

O **Prototype** cria **novos objetos copiando (clonando) uma instância existente** (o "protótipo"), em vez de instanciar do zero. É útil quando criar um objeto é **caro** (muitas configurações) ou quando você quer **variar** a partir de uma base.

> [!example]
> Em um sistema de formulários, você tem um formulário-padrão já preenchido com valores típicos. Em vez de construir do zero cada formulário, você **clona o protótipo** e ajusta o que mudou. Para a prova: **Prototype = clonagem** de objetos a partir de um modelo.

### 2.3 Registry — registro central de instâncias

O **Registry** é um **registro central** (um catálogo) que guarda e disponibiliza instâncias/serviços por nome ou chave. Em vez de cada cliente **saber como** criar/obter um objeto, ele **consulta o registro**.

> [!note] Conexão com o que já estudou
> O Registry se parece com o que você viu em mensageria e em Service Discovery na Fase 4 (Eureka, por exemplo): um ponto central que "sabe onde as coisas estão". O **Registry** é o conceito-irmão aplicado a objetos dentro da aplicação.

### 2.4 Service Locator — localização de serviços

O **Service Locator** fornece uma forma de **obter serviços** por uma **interface central** (o "localizador"), pretendendo **desacoplar** o cliente das implementações concretas.

> [!warning] PEGADINHA — Service Locator vs. Injeção de Dependência
> O **Service Locator** e a **Injeção de Dependência (DI)** são duas estratégias para obter dependências — e a banca testa a diferença. No **Service Locator**, o objeto **pede** a dependência a um localizador central (ele "vai buscar"). Na **DI** (que você viu no Spring, Fase 4), o **container injeta** a dependência no objeto (ele "recebe"). São abordagens distintas de alcançar o mesmo fim (desacoplamento) — não são sinônimas, e opções arquiteturais diferentes têm prós e contras que a banca explora.

> [!important] Não repetir os padrões do 4.1
> A ementa pede **avançar** — não recapitular os GoF clássicos. Se a questão pede "padrão avançado", esteja pronto para **Builder, Prototype, Registry, Service Locator** e padrões empresariais/arquiteturais. Reserve os clássicos para quando a questão explicitamente tratar do GoF básico.

## 3. DDD — Domain-Driven Design

O **DDD (Domain-Driven Design)** é uma abordagem de projeto de software cuja ideia central é: o **domínio de negócio** (as regras e conceitos do problema) deve ser o **coração do sistema**, e o código deve refletir a **linguagem do especialista de negócio**, não a linguagem do banco ou da infraestrutura.

Duas ideias-base antes dos três conceitos centrais:

- **Linguagem ubíqua** (*ubiquitous language*): uma **mesma terminologia** compartilhada entre desenvolvedores e especialistas de negócio, usada em código, documentos e reuniões. Se o negócio chama de "benefício" e o código chama de "tabela_aux1", há uma quebra — a linguagem ubíqua evita isso.
- **Bounded context** (contexto delimitado): um domínio grande é dividido em **contextos** com **modelos próprios e fronteiras claras**. O mesmo conceito pode ter significados diferentes em contextos diferentes (o "cliente" do módulo de atendimento pode ser diferente do "cliente" do módulo financeiro). Cada contexto tem seu próprio modelo explícito.

Agora, os **três conceitos centrais da ementa**.

### 3.1 Entidades

Uma **entidade** é um objeto do domínio que possui **identidade própria e contínua** e um **ciclo de vida**. Dois objetos com os **mesmos atributos** podem ser **diferentes** porque possuem **identidades distintas** — pensadas precisamente por um identificador único (ID).

> [!example]
> Um "benefício previdenciário" tem um **número** que o identifica. Dois registros com o mesmo número são **a mesma entidade**, mesmo que os demais dados sejam recém-atualizados. A **identidade** permite rastrear a entidade ao longo do tempo, apesar das mudanças de estado.

### 3.2 Value Objects

Um **value object (objeto de valor)** é um objeto que **não tem identidade própria** — o que importa é **o seu valor**. Dois value objects são **iguais se tiverem os mesmos valores**, e são **imutáveis** (não mudam; ao mudar, cria-se um novo).

> [!warning] PEGADINHA — Value Object vs. Entidade (identidade)
> A distinção é **identidade**: uma **Entidade** tem identidade contínua (dois objetos com mesmos atributos são diferentes; importa o ID). Um **Value Object** **não tem identidade** (dois objetos com mesmos valores são **iguais**; importa o valor). Exemplo: o "CPF" de uma pessoa — dois registros com o mesmo CPF são o **mesmo valor**, não faz sentido haver "dois CPFs iguais e diferentes". Já o "benefício" tem número de identificação → entidade. A banca adora: "value object possui identidade própria" → **falso**.

> [!example]
> Endereço, moeda+valor (dinheiro), e o CPF de uma pessoa costumam ser modelados como **value objects**: são imutáveis e identificados pelo valor. Trocar de endereço cria um **novo** endereço (value object), enquanto a pessoa (entidade) permanece a mesma com sua identidade intacta.

### 3.3 Agregados

Um **agregado** é um **grupo de entidades e value objects** tratado como uma **unidade coesa** de consistência, organizado em torno de uma **raiz de agregação** (*aggregate root*). A raiz é a "porta de entrada": o acesso aos membros do agregado se dá **através dela**, e ela é responsável por manter as **invariantes** — as regras que devem ser sempre verdadeiras dentro daquele grupo.

> [!example]
> Um **pedido** (raiz de agregação) contém **itens de pedido** (entidades internas) e **valores** (preço total). A regra invariante: "o total do pedido é a soma dos itens" deve **sempre** valer. Alterações nos itens só podem ocorrer **pela raiz** (ex.: `pedido.adicionarItem(...)`), garantindo que a invariante seja mantida.

> [!warning] PEGADINHA — Agregado ≠ "apenas agregação de classes"
> "Agregado" em DDD não é qualquer conjunto de objetos ligados por relação. É um **grupo coeso com raiz de agregação** que **garante invariantes** e controla o acesso pela raiz. Não confunda o conceito de DDD com a noção vaga de "agregação" como composição em OO (a relação todo-parte). Em DDD a palavra tem significado **específico**: unidade de consistência com raiz.

### 3.4 Repositórios e Domain Events (conceito)

Dois apoios do DDD:

- **Repositório** (*repository*): abstração que **persiste e recupera agregados**, escondendo do domínio **como** os dados são armazenados (você já viu a materialização disso no Spring Data JPA da Fase 4 — JPA Repository).
- **Domain Events** (eventos de domínio): fatos relevantes que **aconteceram** no domínio (ex.: "benefício concedido") e podem **disparar** reações em outras partes do sistema. Esta é a **ponte** para a arquitetura orientada a eventos, a seguir.

> [!note] DDD ≠ microsserviços
> **DDD e microsserviços estão relacionados mas não são sinônimos.** DDD é uma **abordagem de modelagem de domínio**, que pode ser aplicada em um monolito ou em microsserviços. Microsserviço é um **estilo arquitetural** (assunto do Tópico 4). É comum que microsserviços **usem** DDD (cada serviço pode ser modelado como um bounded context), mas o DDD **não exige** microsserviços nem o contrário. A banca testa isso: "DDD é obrigatório para usar microsserviços" → **falso**.

## 4. Event-Driven Architecture

A **arquitetura orientada a eventos** (*event-driven architecture*) organiza o sistema em torno de **eventos** — fatos que ocorrem — e das **reações** a eles, em vez de chamadas diretas e síncronas. Você já viu a base disso na **mensageria** do 4.1 (fila, tópico, pub/sub, broker). Aqui aplicamos a eventos de domínio e a dois padrões específicos.

### 4.1 Event Sourcing

No modelo tradicional, você persiste **apenas o estado atual** (o "saldo final"). No **event sourcing**, você persiste **os eventos** como **fonte de verdade** (*source of truth*) — a sequência de fatos que **produziram** o estado. O estado atual passa a ser apenas uma **consequência derivada** dos eventos, que pode ser **reconstruída** a qualquer momento.

> [!example]
> Em vez de guardar só "saldo = R$ 50", você guarda os eventos: "depósito de R$ 100", "saque de R$ 30", "depósito de R$ 20". O saldo atual (R$ 90) pode ser **recalculado** reprocessando os eventos a partir de um ponto inicial. Cada evento é **imutável e em ordem** — isso dá um histórico completo e auditável.

> [!warning] PEGADINHA — Event Sourcing ≠ "só auditoria"
> Event sourcing é **especificamente** persistir **eventos como fonte de verdade** (não apenas o estado) para permitir **reconstrução** do estado e histórico completo. Manter um log de auditoria das mudanças **não** é, por si só, event sourcing — auditar registra mudanças para fiscalização, mas a **fonte de verdade** continua sendo o estado atual. A pegadinha da banca: "auditoria = event sourcing" → **falso**. A diferença está em **o que é a fonte de verdade**.

### 4.2 CQRS

O **CQRS** (*Command Query Responsibility Segregation*) propõe **separar as operações de escrita (comandos) das operações de leitura (consultas)** — responsabilidades diferentes com modelos possivelmente diferentes.

- **Comandos** (escrições): mudam o estado; seguem as regras e invariantes (ex.: "conceder benefício");
- **Consultas (queries)** (leituras): não mudam nada; podem ser otimizadas para leitura (ex.: "visualizar extrato").

Separar os dois caminhos permite **otimizar cada um independentemente** (ex.: um modelo de escrita com invariantes rígidas e um modelo de leitura desnormalizado e rápido).

> [!warning] PEGADINHA — CQRS ≠ "só por performance"
> CQRS **separa as responsabilidades de leitura e escrita**, e um dos **benefícios possíveis** é o desempenho — mas a motivação conceitual é a **segregação de responsabilidades** e os **modelos independentes**, não apenas "acelerar consultas". Afirmar que "CQRS é só uma técnica de performance" é **reduzir** o padrão. Também não confunda a sigla: **CQRS** separa **Command** (escrita) de **Query** (leitura) — não é "consulta vs. comando" em outro sentido.

> [!note] Event Sourcing + CQRS
> Event sourcing e CQRS são **complementares e frequentemente usados juntos**: os **eventos** (event sourcing) podem disparar a **atualização de um modelo de leitura** (consultas) otimizado, enquanto o **modelo de escrita** é alimentado por **comandos**. Mas não são obrigatoriamente acoplados — cada um pode existir sozinho. A banca testa entender essa relação de **complementaridade**, não de identidade.

## 5. Conexões com os pré-requisitos

Este tópico **costura** muito do que você já viu:

- **OO e SOLID** (4.1): DDD usa encapsulamento, coesão e os princípios de design para proteger o domínio.
- **Regras/invariantes** (ACID, 3.1): a "consistência" do domínio (invariantes dos agregados) dialoga com a consistência que você viu nas transações — embora uma seja de **regra de negócio** (DDD) e a outra de **banco** (ACID).
- **Mensageria** (4.1): a arquitetura orientada a eventos reaproveita os mesmos conceitos de fila, tópico, produtor/consumidor e broker.
- **Segurança de comunicações** (Tópico 1): a **integridade** dos eventos (não adulteráveis, em ordem) ecoa a garantia de integridade que você estudou em TLS.

## 6. Palavras-chave e como a FGV cobra

- **Palavras-chave:** *Builder, Prototype, Registry, Service Locator, DDD, domínio, linguagem ubíqua, bounded context, entidade, value object, agregado, aggregate root, invariante, repositório, domain event, event-driven, event sourcing, CQRS, comando, query.*

**Formas de cobrança típicas:**

1. **Value Object vs. Entidade** — qual tem identidade própria (Entidade); Value Object é por valor e imutável.
2. **Agregado** — grupo coeso com raiz de agregação e invariantes; acesso pela raiz; ≠ agregação comum de OO.
3. **DDD ≠ microsserviços** — modelagem de domínio vs. estilo arquitetural (relacionados, não iguais).
4. **Event sourcing ≠ auditoria** — eventos como fonte de verdade vs. log de auditoria.
5. **CQRS ≠ "só performance"** — separação de responsabilidades leitura/escrita (performance é benefício possível).
6. **Service Locator vs. DI** — buscar vs. receber a dependência.
7. **Padrões avançados** — Builder (construção passo a passo), Prototype (clonagem), Registry (registro central).

## 7. Próximos passos

Com o design de software avançado dominado — padrões empresariais, DDD (entidades, value objects, agregados) e arquitetura orientada a eventos (event sourcing, CQRS) — você tem o ferramental para modelar **domínios complexos** de forma fiel ao negócio. O próximo passo é o **Tópico 4 — Arquitetura de Software Avançada**, onde esses conceitos se materializam em **Hexagonal**, **microsserviços**, **containers** e **Kubernetes**. Ao concluir o bloco, você encaminha para a **Fase 6 — Segurança e Governança** (sem antecipar conteúdo).
