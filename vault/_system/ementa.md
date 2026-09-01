# Ementa Pedagógica — Concurso DATAPREV 2026

## Cargo: Analista de TI — Perfil 3: Desenvolvimento de Software

---

## Visão Geral

Esta ementa organiza o conteúdo do edital em sequência didática, respeitando dependências cognitivas entre blocos. A ordem apresentada não reflete a ordem de aparecimento no edital, mas sim a progressão necessária para que cada conceito seja compreendido antes de ser utilizado.

### Pesos por Módulo

| Módulo | Questões | Peso Unitário | Peso Total |
|--------|----------|---------------|------------|
| I — Conhecimentos Gerais | 40 | 1,0 | 40,0 |
| II — Conhecimentos Específicos | 30 | 2,5 | 75,0 |

> **Observação pedagógica:** O peso maior do Módulo II (2,5x) indica que o domínio técnico é o fator decisivo. Porém, os tópicos de Gerais funcionam como alicerce cognitivo para o conteúdo específico.

---

## Mapa de Dependências (Visão Macro)

```
BLOCO FUNDAMENTOS (sem pré-requisitos)
├── Português
├── Raciocínio Lógico Matemático
└── Legislação (LGPD, Segurança da Informação)

BLOCO LINGUAGENS E ACESSO
├── Inglês (pré-req: Português — estrutura linguística)
└── Atualidades e IA (pré-req: RLM + Legislação)

BLOCO INFRAESTRUTURA DE DADOS
├── Banco de Dados (pré-req: RLM + Legislação/Segurança)
└── BI e Data Warehouse (pré-req: Banco de Dados)

BLOCO DESENVOLVIMENTO CORE
├── Desenvolvimento de Sistemas (pré-req: RLM + Português técnico + BD)
├── Metodologias e Eng. de Software (pré-req: Desenvolvimento de Sistemas)
└── Testes de Software (pré-req: Desenvolvimento de Sistemas + Metodologias)

BLOCO FRONTEND E INTERFACES
├── Frontend Web (pré-req: Desenvolvimento de Sistemas + UX)
├── UX e Gestão de Conteúdo (pré-req: Frontend Web)
└── Arquitetura Avançada (pré-req: Desenvolvimento + BD + Segurança)

BLOCO GESTÃO E GOVERNANÇA
├── Segurança da Informação (pré-req: Legislação + Arquitetura)
└── Gestão e Governança de TI (pré-req: Metodologias + Segurança + ITIL/COBIT)
```

---

## Sequência Didática Recomendada

### FASE 1 — Fundamentos (estudar primeiro, sem dependências)

#### Bloco 1.1: Língua Portuguesa

> **Função na ementa:** Base para compreensão de qualquer texto técnico, elaboração de documentação e interpretação de enunciados de prova.

**Pré-requisitos:** Nenhum.

**Tópicos:**

1. [[Compreensao-e-Interpretacao-de-Textos|Compreensão e interpretação de textos]]
   - Interpretação literal e inferencial
   - Identificação de ideia central e ideias secundárias
   - Reconhecimento de intenção comunicativa do autor

2. [[Tipos-e-Generos-Textuais|Tipos e gêneros textuais]]
   - Narrativo, dissertativo (argumentativo e expositivo), descritivo, injuntivo
   - Gêneros: editorial, artigo, resenha, relatório, manual técnico, email profissional

3. [[Ortografia-Oficial|Ortografia oficial]]
   - Regras de acentuação (oxítona, paroxítona, proparoxítona)
   - Uso de hífen e crase
   - Letras maiúsculas e minúsculas
   - Divisão silábica

4. [[Coesao-Textual|Coesão textual]]
   - Referenciação: pronomes, sinonímia, hiperonímia, substituição, elipse
   - Conectores lógicos e temporais (portanto, entretanto, ademais, além disso)
   - Tempos verbais e coerência narrativa

5. [[Estrutura-Morfossintatica|Estrutura morfossintática]]
   - [[Classes-de-Palavras|Classes de palavras]]: substantivos, adjetivos, verbos, advérbios, preposições, conjunções, pronomes, interjeições
   - [[Sintaxe-da-Oracao|Sintaxe]]: sujeito, predicado, complementos, apostos, adjuntos
   - Coordenação (e, ou, mas, porém, todavia)
   - Subordinação (substantiva, adjectival, adverbial)
   - [[Pontuacao|Pontuação]]: vírgula, ponto e vírgula, dois-pontos, ponto final, pontinhos suspensivos
   - [[Concordancia|Concordância nominal e verbal]]
   - [[Regencia-e-Crase|Regência verbal e nominal]]
   - [[Regencia-e-Crase|Crase]]: regras e exceções
   - [[Colocacao-Pronominal|Pronomes oblíquos átonos]] (colocação: próclise, mesóclise,ênclise)

6. [[Reescrita-de-Frases-e-Paragrafos|Reescrita de frases e parágrafos]]
   - Transformação de voz (ativa/passiva)
   - Substituição de vocabulário (paráfrase)
   - Reorganização de períodos complexos
   - Correção de erros sintáticos e ortográficos

**Observações pedagógicas:**
- Dominar coesão e conectores é essencial para a compreensão de textos longos de outras disciplinas
- A concordância e regência são alvos frequentes de questões com "pegadinhas"
- Praticar reescrita de frases do edital técnico ajuda a internalizar o conteúdo de outras disciplinas

---

#### Bloco 1.2: Raciocínio Lógico Matemático

> **Função na ementa:** Base para pensamento estruturado, resolução de problemas, modelagem de dados e algoritmos. Indispensável para Desenvolvimento de Sistemas, Banco de Dados e Arquitetura.

**Pré-requisitos:** Nenhum.

**Tópicos:**

1. [[Estruturas-Logicas|Estruturas lógicas]]
   - Proposições e conectivos (e, ou, se...então, não, se e somente se)
   - Leitura e construção de argumentos

2. [[Logica-de-Argumentacao|Lógica de argumentação]]
   - Analogias: identificação de relações entre pares
   - Inferências: dedutivas, indutivas e abdutivas
   - Deduções em cadeia a partir de premissas

3. [[Logica-Sentencial|Lógica sentencial]]
   - Tabelas-verdade
   - Equivalências lógicas (leis de De Morgan, distributiva, associativa)
   - Diagramas de Venn para proposições simples

4. [[Logica-de-Primeira-Ordem|Lógica de primeira ordem]]
   - Quantificadores (universal e existencial)
   - Predicados e variáveis
   - Negação de quantificadores

5. [[Raciocinio-Matematico-Aplicado|Raciocínio matemático aplicado]]
   - Problemas aritméticos: porcentagem, regra de três, juros simples e compostos, média ponderada
   - Problemas geométricos: áreas, volumes, relações de semelhança e congruência
   - Problemas matriciais: operações com matrizes, sistemas lineares elementares
   - Sequências e progressões (PA e PG)

**Observações pedagógicas:**
- A lógica sentencial é o fundamento para expressões booleanas em programação
- Os problemas aritméticos frequentemente envolvem raciocínio proporcional, úteis para estimativas de projetos (APF, Story Points)
- Praticar tabelas-verdade ajuda a pensar em condicionais (if/else) e validação de testes

---

#### Bloco 1.3: Legislação de Segurança da Informação e LGPD

> **Função na ementa:** Fornece o embasamento jurídico para o módulo de Segurança da Informação e para o tratamento adequado de dados em sistemas. Conexão direta com Arquitetura de Software e Bancos de Dados.

**Pré-requisitos:** Nenhum (mas se beneficia de conhecimento básico de lógica para interpretar artigos).

**Tópicos:**

1. [[Lei-de-Acesso-a-Informacao-LAI|Lei de Acesso à Informação — LAI]] (Lei 12.527/2011)
   - Princípio da publicidade e transparência
   - Classificação da informação: reservado, secreto, altamente secreto
   - Procedimento de requisição e prazos
   - Informações pessoais e dados sensíveis

2. [[Lei-Carolina-Dieckmann|Lei Carolina Dieckmann]] (Lei 12.737/2012)
   - Inserção de dispositivos no Código Penal
   - Acesso indevido a dispositivo informático
   - Penas e circunstâncias agravantes

3. [[Marco-Civil-da-Internet|Marco Civil da Internet]] (Lei 12.965/2014)
   - Princípios de uso da internet no Brasil
   - Privacidade e proteção de dados
   - Neutralidade da rede
   - Responsabilidade dos provedores
   - Retenção de dados

4. [[LGPD-Lei-Geral-de-Protecao-de-Dados|Lei Geral de Proteção de Dados — LGPD]] (Lei 13.709/2018)
   - Princípios: finalidade, adequação, necessidade, livre acesso, qualidade dos dados, transparência, segurança, prevenção, não discriminação, responsabilização e prestação de contas
   - Bases legais (art. 7): consentimento, obrigação legal, política pública, etc.
   - Direitos dos titulares
   - Papel do Controlador e do Operador
   - Relatório de Impacto à Proteção de Dados (RIPD)
   - Autoridade Nacional de Proteção de Dados (ANPD)
   - Sanções administrativas

**Observações pedagógicas:**
- A LGPD é o tema mais cobrado dentro deste bloco
- Conhecer a LGPD é essencial para o tópico "Segurança da Informação" do Módulo II
- A Lei Carolina Dieckmann conecta diretamente com OWASP e SDL (ciclo de vida seguro)
- Relacionar os princípios da LGPD com a "Tríade CID" (Confidencialidade, Integridade, Disponibilidade) do bloco de Segurança

---

### FASE 2 — Linguagens e Acesso ao Conhecimento Técnico

#### Bloco 2.1: Língua Inglesa

> **Função na ementa:** Capacidade de ler documentação técnica, especificações de frameworks e padrões de mercado em inglês. Domínio essencial para se manter atualizado.

**Pré-requisitos:**
- Língua Portuguesa (compreensão de estrutura linguística, classes de palavras, análise sintática básica)

**Tópicos:**

1. [[Compreensao-de-Textos-em-Ingles|Compreensão de textos em inglês]]
   - Leitura crítica de textos técnicos e acadêmicos
   - Identificação de ideia principal e argumentos secundários
   - Inferência de significado por contexto

2. [[Gramatica-Inglesa-Aplicada|Gramática inglesa aplicada]]
   - Tempos verbais: Simple Present, Past, Future; Present Perfect, Past Perfect; Continuous (Present/Past)
   - Condicionais: Zero, Primeira, Segunda, Terceira, Mistas
   - Voz passiva
   - Reported Speech (discurso indireto)
   - Modais: can, could, may, might, must, should, will, would
   - Conectivos acadêmicos e técnicos (however, furthermore, consequently, in contrast)

**Observações pedagógicas:**
- A prova de Inglês deste edital cobra "compreensão de textos e gramática" — o foco deve ser leitura técnica, não tradução literária
- Muitos frameworks e padrões possuem documentação exclusiva em inglês (Spring, React, Kubernetes)
- Praticar com textos de documentação técnica (ex: MDN, Spring Docs) é mais eficaz que textos genéricos

---

#### Bloco 2.2: Atualidades e Inteligência Artificial

> **Função na ementa:** Conecta o conhecimento técnico com o contexto societal, político e ético. A IA é uma força transversal que impacta todos os módulos de desenvolvimento.

**Pré-requisitos:**
- Raciocínio Lógico Matemático (para conceitos de ML e algoritmos)
- Legislação (para debates sobre ética e regulamentação de IA)

**Tópicos:**

1. [[Tematicas-Atuais|Temáticas atuais]]
   - Segurança nacional e ciberguerra
   - Política nacional e internacional
   - Economia digital e transformação digital
   - Sustentabilidade e tecnologia
   - Saúde pública e inovação

2. [[Inteligencia-Artificial-Conceitos-Fundamentais|Inteligência Artificial — Conceitos fundamentais]]
   - Definição de IA, ML e Deep Learning
   - Aprendizagem supervisionada, não-supervisionada e por reforço
   - Redes neurais: conceito geral
   - Modelos generativos e LLMs (Large Language Models)
   - Prompt engineering: conceito básico

3. [[IA-e-Etica|IA e Ética]]
   - Viés algorítmico (bias)
   - Transparência e explicabilidade
   - Regulamentação de IA no Brasil e no mundo
   - IA generativa no contexto corporativo e público
   - Impacto da IA no mercado de trabalho de TI

**Observações pedagógicas:**
- Este módulo exige estudo contínuo de atualidades (notícrias, revisões periódicas)
- Para IA, não é necessário domínio técnico profundo — o foco é conceitual e ético
- Relacionar IA com LGPD (tratamento de dados pessoais por algoritmos) é uma estratégia eficaz
- LLMs e geradores de código (Copilot, etc.) podem ser estudados como ferramentas que afetam o processo de desenvolvimento

---

### FASE 3 — Infraestrutura de Dados

#### Bloco 3.1: Banco de Dados

> **Função na ementa:** Fundamento para qualquer aplicação de software. Modelagem, consultas e integridade de dados são pré-requisitos para Desenvolvimento de Sistemas e Arquitetura.

**Pré-requisitos:**
- Raciocínio Lógico Matemático (para modelagem, normalização, conjuntos)
- Legislação/Segurança da Informação (para ACID, privacidade, dados sensíveis)

**Tópicos:**

1. [[Fundamentos-e-Modelagem|Fundamentos e Modelagem]]
   - Conceito de banco de dados e SGBD
   - Abordagens: hierárquica, rede, relacional, orientada a objetos
   - Modelagem conceitual: entidade, atributo, relacionamento, cardinalidade
   - Modelagem lógica: modelo relacional, chaves primárias e estrangeiras
   - Modelagem física: indexação, particionamento, tablespaces

2. [[Normalizacao|Normalização]]
   - Formas normais (1FN, 2FN, 3FN, BCNF)
   - Dependências funcionais
   - Decomposição e perda de informação
   - Anomalias de atualização

3. [[SQL-DDL-e-DML|SQL — DDL e DML]]
   - DDL: CREATE, ALTER, DROP, TRUNCATE
   - DML: SELECT, INSERT, UPDATE, DELETE
   - JOINs: INNER, LEFT, RIGHT, FULL, CROSS
   - Subconsultas, agrupamento (GROUP BY, HAVING), ordenação
   - Funções de agregação (COUNT, SUM, AVG, MIN, MAX)
   - Views, triggers, stored procedures (conceito)

4. [[Transacoes-e-ACID|Transações e ACID]]
   - Propriedades ACID: Atomicidade, Consistência, Isolamento, Durabilidade
   - Níveis de isolamento
   - Deadlocks: conceito e mecanismos de resolução

5. [[NoSQL|NoSQL]]
   - Quando usar NoSQL vs. SQL
   - Tipos: document, key-value, column-family, graph
   - Exemplos: MongoDB, Redis, Cassandra, Neo4j
   - Eventual consistency vs. strong consistency

6. [[Big-Data|Big Data]]
   - Características: Volume, Velocidade, Variabilidade, Veracidade, Valor
   - Hadoop e MapReduce (conceito)
   - Apache Spark (conceito)
   - Data Lakes

**Observações pedagógicas:**
- Normalização é alvo frequente de questões — praticar com exercícios de decomposição
- SQL é o tópico mais prático — montar queries complexas é essencial
- A conexão entre ACID e transações distribuídas (Arquitetura Avançada) deve ser feita na fase avançada
- Big Data é mais conceitual — não se aprofundar em implementação, mas entender o ecossistema

---

### FASE 4 — Núcleo de Desenvolvimento

#### Bloco 4.1: Desenvolvimento de Sistemas

> **Função na ementa:** Corpo central do edital. Conjuga programação, arquitetura de software, padrões e ferramentas. Todo o conteúdo anterior converge aqui.

**Pré-requisitos:**
- Raciocínio Lógico Matemático (algoritmos, lógica de programação)
- Língua Portuguesa (documentação técnica, nomes de classes, padrão CamelCase)
- Banco de Dados (SQL, JPA, mapeamento objeto-relacional)

**Tópicos:**

1. [[Paradigma-Orientado-a-Objetos|Paradigma Orientado a Objetos]]
   - Conceitos: classe, objeto, herança, polimorfismo, encapsulamento, abstração
   - SOLID: princípios básicos
   - Princípios de Clean Code: nomes significativos, funções pequenas, comentários úteis

2. [[Java-e-Ecossistema-JVM|Java e Ecossistema JVM]]
   - Java (v6+): tipos primitivos, coleções, tratamento de exceções, generics
   - JavaEE (v6+): Servlets, JSP, CDI, Bean Validation, JAX-RS
   - JakartaEE: evolução do JavaEE, mudanças de namespace
   - JPA (v2+): mapeamento ORM, entidades, repositórios, consultas JPQL
   - Hibernate: configuração, cascata, lazy/eager loading, cache

3. [[JavaScript|JavaScript]]
   - Sintaxe básica e tipos
   - Funções, closures, escopo
   - Prototype e cadeia de protótipos
   - Async/Await, Promises
   - ES6+: let/const, arrow functions, destructuring, spread/rest

4. [[Frameworks-Java|Frameworks Java]]
   - Spring: IoC, DI, Spring MVC, Spring Data
   - Spring Boot: autoconfiguração, starter dependencies
   - Spring Cloud: Discovery (Eureka), Config, Gateway, Circuit Breaker
   - JSF (JavaServer Faces): ciclos de vida, componentes
   - Primefaces: componentes, temas, integração com JSF

5. [[Padroes-de-Projeto-e-Arquitetura|Padrões de Projeto e Arquitetura]]
   - Padrões GoF (criação, estruturais, comportamentais): Singleton, Factory, Strategy, Observer, etc.
   - MVC, MVP, MVVM
   - SOA (Service Oriented Architecture)
   - Web Services: SOAP, REST, GraphQL (conceito)
   - APIs RESTful: verbos HTTP, status codes, recursos
   - Swagger/OpenAPI: especificação e documentação

6. [[Formatos-de-Dados-e-Integracao|Formatos de Dados e Integração]]
   - XML: sintaxe, namespaces, validação (XSD)
   - XSLT: transformação de XML
   - JSON: sintaxe, parsing, serialização
   - UDDI: registro e descoberta de serviços

7. [[Desenvolvimento-Mobile|Desenvolvimento Mobile]]
   - Android: Activity, Fragment, Intent, RecyclerView, lifecycle
   - iOS: UIKit, SwiftUI (conceito), ciclo de vida
   - Low-code e no-code: conceitos, plataformas, quando usar

8. [[DevOps-e-Controle-de-Versao|DevOps e Controle de Versão]]
   - Git: init, add, commit, branch, merge, rebase, pull request
   - CI/CD: conceito, Jenkins, GitHub Actions (conceito)
   - Containerização: Docker (conceito básico)
   - Ambientes: Internet, intranet, portal

**Observações pedagógicas:**
- Java é o tópico de maior profundidade — priorizar ecossistema Spring, que é o mais cobrado
- A transição JavaEE → JakartaEE deve ser entendida como evolução, não substituição
- JPA e Hibernate frequentemente aparecem juntos — entender a relação (JPA é especificação, Hibernate é implementação)
- Git é cobrado de forma prática — saber resolver conflitos e branch management
- O tópico "Low-code e no-code" é mais conceitual — entender quando aplicar

---

#### Bloco 4.2: Metodologias e Engenharia de Software

> **Função na ementa:** Organiza o processo de desenvolvimento. Dependente do conhecimento de programação para contextualizar práticas.

**Pré-requisitos:**
- Desenvolvimento de Sistemas (para entender o ciclo de vida do código)

**Tópicos:**

1. [[Metodologias-Ageis|Metodologias Ágeis]]
   - Scrum: papéis (Product Owner, Scrum Master, Dev Team), eventos (Sprint, Daily, Review, Retrospective), artefatos (Product Backlog, Sprint Backlog, Increment)
   - Kanban: tabuleiro, WIP limits, fluxo contínuo
   - XP (Extreme Programming): programação em par, TDD, refatoração, integração contínua

2. [[Padroes-de-Desenvolvimento-e-Reuso|Padrões de Desenvolvimento e Reuso]]
   - Padrões de projeto aplicados ao desenvolvimento
   - Componentização e modularização
   - Bibliotecas e frameworks como formas de reuso

3. [[Tipos-de-Codificacao|Tipos de Codificação]]
   - Sistemas transacionais: CRUD, integração, regras de negócio
   - Analíticos: relatórios, dashboards, processamento de dados
   - Mobile: nativo, híbrido, responsividade
   - API: desenvolvimento e versionamento

4. [[Estimativas|Estimativas]]
   - Pontos de Função (APF): contagem de transações, funções de dados, conversão para PF
   - Story Points: estimativa relativa, Planning Poker, fibonacci
   - Relação entre APF e Story Points (conceito)

5. [[Engenharia-de-Requisitos|Engenharia de Requisitos]]
   - Elicitação: entrevistas, questionários, observação, workshops
   - Documentação: User Stories, casos de uso, especificações
   - Gerenciamento de requisitos: rastreabilidade, priorização (MoSCoW, Kano)
   - Validação e verificação de requisitos

**Observações pedagógicas:**
- Scrum é o framework mais cobrado — dominar papéis e eventos
- APF é mais cobrado que Story Points em concursos públicos
- Engenharia de Requisitos é o elo entre o usuário e o desenvolvedor — não negligenciar

---

#### Bloco 4.3: Testes de Software

> **Função na ementa:** Garantia de qualidade. Depende do conhecimento de programação e metodologias.

**Pré-requisitos:**
- Desenvolvimento de Sistemas (para escrever e entender testes)
- Metodologias e Engenharia de Software (para contextualizar testes no ciclo de vida)

**Tópicos:**

1. [[Fundamentos-de-Teste|Fundamentos de Teste]]
   - Níveis: unitário, integração, sistema, aceitação
   - Tipos: funcionais, não-funcionais, estruturais, regressão
   - Estratégias: caixa-branca, caixa-preta, cinza

2. [[Testes-Ageis|Testes Ágeis]]
   - TDD (Test-Driven Development): ciclo Red-Green-Refactor
   - BDD (Behavior-Driven Development): Cucumber, Gherkin (conceito)
   - Testes em sprints: definição de pronto (DoD)

3. [[Testes-Automatizados|Testes Automatizados]]
   - JUnit: anotações, asserts, suítes de teste
   - Mockito: mocks e stubs
   - Selenium: testes de UI web (conceito)
   - Cobertura de código: métricas e ferramentas

4. [[Gestao-do-Ciclo-de-Vida-de-Testes|Gestão do Ciclo de Vida de Testes]]
   - Planejamento: plano de teste, casos de teste, dados de teste
   - Execução: registro de defeitos, severidade e prioridade
   - Relatórios: métricas (defeitos por fase, taxa de falha, MTBF)

5. [[RPA|RPA (Robotic Process Automation)]]
   - Conceito e quando aplicar
   - Diferença entre RPA e automação de testes
   - Ferramentas: UiPath, Automation Anywhere (conceito)

**Observações pedagógicas:**
- TDD é frequentemente cobrado em conjunto com Scrum e XP
- Saber a diferença entre mock, stub e fake é uma pegadinha comum
- RPA é mais conceitual — entender o cenário de uso, não a implementação

---

### FASE 5 — Frontend e Interfaces

#### Bloco 5.1: Tecnologias e Práticas Frontend Web

> **Função na ementa:** Camada de apresentação do software. Requer conhecimento básico de web e programação.

**Pré-requisitos:**
- Desenvolvimento de Sistemas (JavaScript, programação web básica)

**Tópicos:**

1. [[Fundamentos-Web|Fundamentos Web]]
   - HTML5: semântica, forms, acessibilidade básica
   - CSS3: seletores, box model, flexbox, grid, responsividade
   - UX: princípios básicos de usabilidade, heurísticas de Nielsen
   - Ajax: requisições assíncronas, API calls do navegador

2. [[Frameworks-Frontend|Frameworks Frontend]]
   - VueJS: componentes, reatividade, Vue Router, Vuex/Pinia
   - Angular: componentes, diretivas, serviços, RxJS, Angular CLI
   - React: componentes, hooks, JSX, React Router, Context API

3. [[Arquiteturas-de-Apresentacao|Arquiteturas de Apresentação]]
   - SPA (Single Page Application): conceito, vantagens e limitações
   - PWA (Progressive Web App): service workers, manifest, offline capability
   - SSR (Server-Side Rendering) vs. CSR (Client-Side Rendering) — conceito

**Observações pedagógicas:**
- A prova cobra os três frameworks (Vue, Angular, React) — focar nas diferenças conceituais e não em detalhes de API
- UX é cobrado tanto aqui quanto no bloco de "UX e Gestão de Conteúdo" — estabelecer conexão
- PWA é um tópico emergente — entender o conceito de service worker e offline-first

---

#### Bloco 5.2: UX e Gestão de Conteúdo

> **Função na ementa:** Camada de experiência do usuário. Complementa o Frontend com foco em design e gestão editorial.

**Pré-requisitos:**
- Frontend Web (para entender como UX influencia a implementação)

**Tópicos:**

1. [[Conceitos-de-UX|Conceitos de UX (User Experience)]]
   - Design Centrado no Usuário
   - Heurísticas de Nielsen
   - Pesquisa com usuários: entrevistas, testes de usabilidade, A/B testing
   - Wireframes, protótipos, mockups
   - Acessibilidade: WCAG, leitores de tela, navegação por teclado

2. [[Gestao-de-Conteudo-e-CMS|Gestão de Conteúdo e CMS]]
   - Arquitetura da informação: taxonomia, ontologia, folksonomia
   - Portais: conceito, tipos, gestão editorial
   - CMS (Content Management System): conceito, tipos (headless, decoupled)
   - Workflow editorial: criação, revisão, publicação, arquivamento
   - SEO básico: meta tags, sitemap, estrutura de URLs

**Observações pedagógicas:**
- UX é mais conceitual que prático nesta prova — focar em princípios e heurísticas
- CMS é cobrado em contexto de portais governamentais (relevante para DATAPREV)
- Acessibilidade é um tema que conecta UX com legislação (inclusão digital)

---

#### Bloco 5.3: Arquitetura Avançada, Segurança e Inovação

> **Função na ementa:** Nível de abstração superior. Requer domínio de desenvolvimento, banco de dados e segurança.

**Pré-requisitos:**
- Desenvolvimento de Sistemas (SOA, APIs, padrões)
- Banco de Dados (transações, ACID)
- Legislação/Segurança da Informação (para HTTPS, SSL, segurança de APIs)

**Tópicos:**

1. [[Seguranca-de-Comunicacoes|Segurança de Comunicações]]
   - HTTPS: funcionamento, certificados digitais
   - SSL/TLS: handshake, cifragem, integridade
   - Certificados: CA, cadeia de confiança

2. [[Blockchain|Blockchain]]
   - Conceito: ledger distribuído, mineração, consenso
   - Criptomoedas: Bitcoin, Ethereum (conceito)
   - Smart contracts
   - Aplicações além das criptomoedas: supply chain, identidade digital

3. [[Design-de-Software-Avancado|Design de Software]]
   - Design patterns avançados
   - Domain-Driven Design (DDD): entidades, value objects, agregados
   - Event-Driven Architecture: event sourcing, CQRS

4. [[Arquitetura-de-Software-Avancada|Arquitetura de Software Avançada]]
   - Arquitetura Hexagonal (Ports and Adapters)
   - Microsserviços: princípios, desafios, comunicação (síncrona/assíncrona)
   - Containers: Docker (images, containers, volumes, networks)
   - Orquestração: Kubernetes (conceito: pods, services, deployments)
   - Service Mesh: conceito

5. [[Transacoes-Distribuidas|Transações Distribuídas]]
   - CAP Theorem
   - Two-Phase Commit (2PC)
   - Saga Pattern
   - Eventual consistency em microsserviços

**Observações pedagógicas:**
- Arquitetura Hexagonal é frequentemente cobrada em concursos — entender a separação entre núcleo e adaptadores
- Docker e Kubernetes são cobrados de forma conceitual — saber o que é um container vs. VM
- Transações distribuídas conectam com ACID do bloco de BD — fazer essa ponte explicitamente
- Blockchain é mais conceitual — não aprofundar em implementação

---

### FASE 6 — Segurança e Governança

#### Bloco 6.1: Segurança da Informação

> **Função na ementa:** Transversal a todo o sistema. Combina legislação (Fase 1) com práticas técnicas (arquitetura, APIs).

**Pré-requisitos:**
- Legislação de Segurança e LGPD (bases jurídicas)
- Arquitetura Avançada (HTTPS, SSL/TLS, autenticação)
- Desenvolvimento de Sistemas (para entender vulnerabilidades em código)

**Tópicos:**

1. [[Fundamentos-de-Seguranca|Fundamentos de Segurança da Informação]]
   - Tríade CID: Confidencialidade, Integridade, Disponibilidade
   - Políticas e procedimentos de segurança
   - Normas ISO 27001 e ISO 27002: estrutura e principais controles

2. [[Autenticacao-e-Autorizacao|Autenticação e Autorização]]
   - OAuth2: fluxos (Authorization Code, Client Credentials, PKCE)
   - SSO (Single Sign-On): conceito, SAML, OpenID Connect
   - JWT (JSON Web Tokens): estrutura, validade, refresh tokens
   - MFA (Multi-Factor Authentication): conceito

3. [[Gestao-de-Riscos|Gestão de Riscos]]
   - Identificação e avaliação de riscos
   - Matriz de risco: probabilidade x impacto
   - Planos de contingência e recuperação

4. [[Seguranca-no-Desenvolvimento|Segurança no Desenvolvimento]]
   - SDL (Security Development Lifecycle): fases e práticas
   - OWASP Top 10: principais vulnerabilidades (Injection, XSS, CSRF, Broken Auth, etc.)
   - SAST (Static Application Security Testing): análise estática
   - DAST (Dynamic Application Security Testing): análise dinâmica
   - Dependabot e gestão de dependências vulneráveis

**Observações pedagógicas:**
- OWASP Top 10 é alvo clássico de questões — memorizar as 10 vulnerabilidades
- OAuth2 é cobrado com foco nos fluxos — entender a diferença entre Authorization Code e Client Credentials
- ISO 27001/27002 é mais estrutural — saber o que é e quais domínios abrange
- SDL conecta com Metodologias Ágeis — integrar segurança no ciclo de vida

---

#### Bloco 6.2: Gestão e Governança de TI

> **Função na ementa:** Nível de gestão e estratégia. Requer visão panorâmica de todos os módulos anteriores.

**Pré-requisitos:**
- Metodologias e Engenharia de Software (processos de desenvolvimento)
- Segurança da Informação (governança de segurança)
- Todas as disciplinas anteriores (para entender o escopo total de TI)

**Tópicos:**

1. [[Gerenciamento-de-Projetos|Gerenciamento de Projetos]]
   - Tradicional (Waterfall): fases sequenciais, WBS, cronograma
   - Híbrido: combinação de ágil e tradicional
   - Ágil: Scrum, Kanban como gestão de projetos
   - Métricas: CPI, SPI, EVM (conceito básico)

2. [[ITIL-v4|ITIL v4]]
   - Conceito de serviço de TI
   - Dimensões: organização e pessoas, informação e tecnologia, parceiros e suprimentos, valor e fluxos de serviço
   - Práticas: gestão de incidentes, gestão de problemas, gestão de mudanças, gestão de serviço de segurança
   - Ciclo de vida do serviço: estratégia, desenho, transição, operação, melhoria contínua

3. [[COBIT-2019|COBIT 2019]]
   - Framework de governança e gestão de TI
   - Objetivos de governança e gestão
   - Princípios: atendendo às necessidades das partes interessadas
   - Relação com ITIL

4. [[BPMN|BPMN (Business Process Model and Notation)]]
   - Notação básica: eventos, atividades, gateway, fluxo de sequência
   - Modelagem de processos de negócio
   - Subprocessos e pools/lanes
   - Diferença entre BPMN e UML

**Observações pedagógicas:**
- ITIL v4 é o framework mais cobrado — focar nas práticas principais e dimensões
- COBIT 2019 é mais estrutural — saber a diferença entre governança e gestão
- BPMN é prático — saber ler e interpretar diagramas de processo
- A conexão entre ITIL e Segurança da Informação (gestão de incidentes de segurança) é uma pegadinha comum

---

## Matriz de Pré-requisitos (Referência Rápida)

| Tópico | Pré-requisitos Diretos |
|--------|----------------------|
| Português | — |
| Raciocínio Lógico Matemático | — |
| Legislação/Segurança (LGPD) | — |
| Inglês | Português |
| Atualidades e IA | RLM, Legislação |
| Banco de Dados | RLM, Legislação/Segurança |
| BI e Data Warehouse | Banco de Dados |
| Desenvolvimento de Sistemas | RLM, Português, Banco de Dados |
| Metodologias e Eng. Software | Desenvolvimento de Sistemas |
| Testes de Software | Desenvolvimento, Metodologias |
| Frontend Web | Desenvolvimento de Sistemas |
| UX e Gestão de Conteúdo | Frontend Web |
| Arquitetura Avançada | Desenvolvimento, BD, Segurança |
| Segurança da Informação | Legislação, Arquitetura Avançada, Desenvolvimento |
| Gestão e Governança TI | Metodologias, Segurança, todas anteriores |

---

## Observações Pedagógicas Gerais

### Sobre a Estrutura da Prova
- O Módulo I (40 questões, peso 1,0) cobre fundamentos ampla e rasa
- O Módulo II (30 questões, peso 2,5) cobre específicos profundos e estreitos
- **Estratégia:** dominar Módulo II é mais eficiente em termos de pontuação (peso 2,5x)

### Sobre a Progressão
- Os tópicos de Fundamentos (Fase 1) devem ser estudados primeiro e em paralelo
- A Fase 4 (Núcleo de Desenvolvimento) é o coração do edital — dedicar mais tempo
- A Fase 6 (Segurança e Governança) é a mais integradora — exigirá revisões dos blocos anteriores

### Sobre a Conexão entre Disciplinas
- **LGPD → Segurança da Informação → Arquitetura Avançada:** corrente jurídico-técnica
- **RLM → Desenvolvimento → Testes → Arquitetura:** corrente técnica
- **Português → Inglês → Documentação Técnica:** corrente comunicacional
- **BD → Desenvolvimento → Arquitetura Avançada:** corrente de dados

### Sobre Frequência de Cobrança (orientação, não determinismo)
- Java/Spring é o bloco mais cobrado no Módulo II
- LGPD é o bloco mais cobrado no Módulo I
- Scrum e ITIL são os frameworks de gestão mais frequentes
- OWASP Top 10 é clássico em Segurança da Informação

### Sobre Temas Emergentes
- IA generativa e LLMs (novo no edital — estudar com profundidade conceitual)
- Kubernetes e Service Mesh (temas crescentes em concursos)
- Arquitetura Hexagonal e DDD (padrões modernos, cada vez mais cobrados)
- Low-code/no-code (conceitual, não aprofundar)

---

## Controle de Versão

| Versão | Data | Alteração |
|--------|------|-----------|
| 1.0 | 2026-08-26 | Versão inicial — estrutura completa |

---

> **Nota para o Writer:** Esta ementa é o contrato de estrutura. Cada bloco deve ser transformado em nota de estudo seguindo a ordem e os pré-requisitos aqui estabelecidos. Não reorganizar a sequência sem justificativa pedagógica.
>
> **Nota para o Question Author:** As "Observações pedagógicas" de cada bloco indicam os alvos de questão e as pegadinhas mais prováveis. Utilize como guia para seleção de tópicos.
>
> **Nota para o Pedagogical Auditor:** Validar cada nota produzida contra esta ementa, verificando: (1) aderência ao tópico, (2) respeito aos pré-requisitos, (3) progressão dentro do bloco, (4) ausência de lacunas relevantes.
