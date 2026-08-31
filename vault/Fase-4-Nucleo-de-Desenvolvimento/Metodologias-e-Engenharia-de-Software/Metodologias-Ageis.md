# Metodologias Ágeis

> [!info] Metadados
> **Disciplina:** Metodologias e Engenharia de Software
> **Bloco:** 4.2 — Metodologias e Engenharia de Software (FASE 4 — Núcleo de Desenvolvimento)
> **Tópico:** 1. Metodologias Ágeis
> **Subtópicos:** Scrum (papéis: Product Owner, Scrum Master, Dev Team; eventos: Sprint, Daily, Review, Retrospective; artefatos: Product Backlog, Sprint Backlog, Increment) · Kanban (tabuleiro, WIP limits, fluxo contínuo) · XP (programação em par, TDD, refatoração, integração contínua)
> **Pré-requisitos:** [[Desenvolvimento-de-Sistemas]] (Git/CI/CD, ciclo de vida do código, DevOps)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-31

---

## 1. Por que estudar metodologias ágeis?

Você já domina o **código** — Java, JavaScript, Spring, Git, CI/CD, Docker. Mas *escrever* código bem não é o mesmo que *entregar* software com qualidade, no prazo e em equipe. É aqui que entram as **metodologias ágeis**: abordagens de **organização do trabalho** que substituíram o modelo cascata tradicional por ciclos curtos, entrega contínua e adaptação constante.

A DATAPREV, como empresa pública que desenvolve e mantém sistemas críticos da seguridade social, trabalha com **times distribuídos, prazos regulatórios e demandas que mudam** — o cenário perfeito para metodologias ágeis. E, para o concurso, **Scrum é o framework mais cobrado** pela FGV dentro deste bloco. Entender seus papéis, eventos e artefatos é essencial.

> [!question] Pergunta orientadora
> Imagine que o INSS solicita uma mudança na regra de cálculo de um benefício. No modelo tradicional (cascata), essa mudança exigiria refazer todo o planejamento, análise e design — meses de atraso. Em uma abordagem ágil, o time poderia incorporar a mudança já na próxima sprint, em semanas. O que muda entre as duas abordagens não é o código — é a **forma de organizar o trabalho**.

Este tópico se apoia no que você já viu no [[DevOps-e-Controle-de-Versao|Bloco 4.1 sobre DevOps]]: a **integração contínua** e o **CI/CD** são práticas que surgiram do universo ágil (especificamente do XP) e hoje são base da entrega moderna de software.

---

## 2. Ágil vs. Cascata — a mudança de paradigma

Antes de mergulhar nos frameworks, vale entender **por que** o ágil surgiu. O modelo tradicional de desenvolvimento — o **Waterfall (cascata)** — organiza o projeto em **fases sequenciais e completas**: requisitos → design → implementação → testes → entrega. Cada fase precisa estar 100% concluída antes da próxima começar.

O problema: em projetos reais (especialmente em TI governamental), os **requisitos mudam constantemente**, as equipes descobrem problemas tarde demais, e o produto final pode não atender ao que o usuário realmente precisa — porque ele só viu o resultado no final.

A **filosofia ágil** (formalizada no *Manifesto Ágil* de 2001) propõe:

- **Entregas incrementais e frequentes** (não uma entrega big-bang no final);
- **Colaboração com o cliente** ao longo de todo o projeto;
- **Adaptação a mudanças** em vez de seguir um plano rígido;
- **Times auto-organizados** e multidisciplinares;
- **Software funcionando** como principal métrica de progresso.

> [!important] O Manifesto Ágil
> O **Manifesto Ágil** é a declaração fundadora. Ele estabelece **4 valores** e **12 princípios**. Os 4 valores são: (1) **Indivíduos e interações** sobre processos e ferramentas; (2) **Software funcionando** sobre documentação abrangente; (3) **Colaboração com o cliente** sobre negociação de contratos; (4) **Responder a mudanças** sobre seguir um plano. Não que os itens à direita não importem — são importantes — mas os da esquerda têm **mais peso**. A FGV cobra os valores.

---

## 3. Scrum — o framework mais cobrado

O **Scrum** é o **framework de gerenciamento e desenvolvimento de software** mais utilizado e mais cobrado em concursos. Ele não é uma metodologia completa (não prescreve *como* programar), mas sim um **framework leve** para gerenciar trabalho complexo por meio de **iterações curtas** chamadas **sprints**.

### 3.1 Os três papéis

O Scrum define **três papéis** (e apenas três):

| Papel | Responsabilidade | O que NÃO é |
|---|---|---|
| **Product Owner (PO)** | Define **o quê** fazer: prioriza o backlog, representa o usuário/stakeholder, maximiza o valor do produto | Não gerencia pessoas, não manda no time técnico |
| **Scrum Master (SM)** | Garante que o Scrum **funcione**: remove impedimentos, facilita eventos, protege o time de distrações | **Não é chefe do time**, não atribui tarefas, não reporta progresso a gestores |
| **Development Team (Dev Team)** | **Entrega** o incremento: time auto-organizado, multifuncional (5-9 pessoas), assume responsabilidade coletiva | Não se divide em "desenvolvedores", "testadores" etc. dentro do time; é **multifuncional** |

> [!warning] PEGADINHA — Scrum Master não é gerente de projeto
> A pegadinha mais clássica da FGV: "O Scrum Master é o líder do time" ou "O Scrum Master atribui tarefas e reporta ao gestor". **Falso.** O **Scrum Master** é um **facilitador/servo-líder** — ele **servi** o time, removendo impedimentos e garantindo que o processo funcione. Ele **não manda**, **não atribui tarefas** e **não é hierarquicamente superior** ao Dev Team. O **Product Owner** é quem decide o quê fazer; o **Dev Team** decide como fazer.

> [!question] Qual é a diferença entre Product Owner e Scrum Master?
> O **Product Owner** é a **voz do negócio** — ele diz *o quê* e *por quê* priorizar algo. O **Scrum Master** é o **guardião do processo** — ele garante que o Scrum funcione bem e que o time possa trabalhar sem barreiras. Um cuida do *produto*; o outro cuida do *processo*. São papéis **distintos** e **complementares** — nunca confunda um com o outro.

### 3.2 Os cinco eventos

O Scrum estrutura o trabalho em **cinco eventos** (reuniões/ocorrências):

| Evento | Duração | O que acontece |
|---|---|---|
| **Sprint** | 1-4 semanas (fixa) | O **ciclo de trabalho** — um período no qual o time entrega um incremento de software funcional |
| **Sprint Planning** | início da sprint | O time planeja **o quê** será feito (PO define prioridades) e **como** (Dev Team planeja o trabalho) |
| **Daily Scrum** (Daily) | 15 min/dia | O Dev Team sincroniza: o que fiz ontem? o que farei hoje? há impedimentos? |
| **Sprint Review** | final da sprint | O time **demonstra** o incremento para stakeholders e coleta feedback |
| **Sprint Retrospective** | após a Review | O time reflete: **o que deu certo, o que melhorar, como melhorar** nos processos |

> [!warning] PEGADINHA — Daily Scrum não é reunião de status para o gestor
> A **Daily Scrum** é uma reunião **do time, para o time** — não é um status report para o Scrum Master ou para um gestor. Se o gestor quer saber o progresso, ele deve olhar o **Sprint Backlog** ou participar do **Sprint Review** — mas a Daily não é o momento. A banca adora dizer que "a daily serve para o Scrum Master reportar ao gestor" — **falso**.

> [!note] A Sprint como "caixa de tempo"
> A **Sprint** é a unidade fundamental. Ela tem **duração fixa** (geralmente 2 semanas) e **não pode ser estendida**. Se o trabalho não foi concluído, ele volta ao backlog para ser planejado em outra sprint. Essa previsibilidade (sempre 2 semanas) cria um **ritmo constante** de entrega.

```mermaid
flowchart LR
    A[Sprint Planning] --> B[Sprint\n(ciclo de trabalho)]
    B --> C[Daily Scrum\n(15 min/dia)]
    B --> D[Sprint Review\n(demo + feedback)]
    D --> E[Sprint Retrospective\n(melhoria do processo)]
    E -->|"próxima sprint"| A
```

### 3.3 Os três artefatos

| Artefato | O que é | Responsável |
|---|---|---|
| **Product Backlog** | Lista **ordenada** de tudo que o produto precisa (requisitos, funcionalidades, correções). **Vivo** — muda constantemente | Product Owner |
| **Sprint Backlog** | Subconjunto do Product Backlog selecionado para a sprint atual, com o **plano de como** entregar | Dev Team + PO |
| **Increment** | A **soma do trabalho** concluído na sprint — um **software funcionando**, potencialmente librável | Dev Team |

> [!question] O que é um "Increment"?
> O **Increment** é o resultado concreto de uma sprint: um pedaço de software **funcional e testado** que agrega valor. No final de cada sprint, o time deve ter um incremento que *poderia* ser colocado em produção (mesmo que ainda não seja — isso depende da estratégia de liberação). Essa cultura de **"sempre há algo funcionando"** é o coração do ágil.

---

## 4. Kanban — fluxo contínuo sem sprints

O **Kanban** não é um framework de "sprints" — é um sistema de **gestão do fluxo de trabalho** baseado no **tabuleiro visual** e nos **limites de trabalho em progresso (WIP limits)**.

### 4.1 Tabuleiro Kanban

O tabuleiro é a ferramenta central. Ele divide o trabalho em **colunas** que representam **estágios do fluxo**:

```text
| A Fazer (To Do)  | Em Progresso (Doing) | Concluído (Done) |
|-------------------|----------------------|-------------------|
| tarefa A          | tarefa C             | tarefa X          |
| tarefa B          | tarefa D             | tarefa Y          |
```

Quando uma tarefa avança, ela se move de uma coluna para a outra. O tabuleiro é **visual e compartilhado** — qualquer pessoa do time pode ver onde está cada item.

### 4.2 WIP Limits (Work In Progress)

O **WIP limit** (limite de trabalho em progresso) é a regra mais importante do Kanban: cada coluna (estágio) tem um **número máximo de itens** que podem estar "em andamento" ao mesmo tempo.

> [!question] Por que limitar o trabalho em progresso?
> Se um desenvolvedor tem 10 tarefas abertas ao mesmo tempo, ele **troca de contexto** constantemente — e a produtividade cai. O **WIP limit** força o time a **terminar** o que começou antes de começar algo novo. É a aplicação do princípio "finalize antes de iniciar" — e melhora drasticamente o fluxo.

### 4.3 Fluxo contínuo vs. sprints

| Critério | Scrum | Kanban |
|---|---|---|
| **Ciclo** | Sprint (período fixo) | **Fluxo contínuo** (sem sprints) |
| **Mudanças** | não podem ser adicionadas no meio da sprint | podem ser adicionadas **a qualquer momento** |
| **Papéis** | PO, SM, Dev Team | não prescreve papéis |
| **Métricas** | velocity (pontos da sprint) | **lead time** e **cycle time** (tempo de entrega) |
| **Melhoria** | retrospectiva (periódica) | melhoria contínua (à medida que os limites são ajustados) |

> [!important] Kanban não é apenas um tabuleiro
> Muita gente acha que "usar um quadro com post-its" é Kanban. Não é. O Kanban **só é Kanban** quando há **WIP limits** e **gestão do fluxo** (medir lead time, identificar gargalos). Um quadro sem limites é apenas um quadro. A banca cobra os **WIP limits** como característica definidora.

---

## 5. XP (Extreme Programming) — práticas de engenharia

O **XP** (Extreme Programming) é um método ágil que se concentra nas **práticas de engenharia de software** — como o time de desenvolvimento **escreve e organiza o código**. Enquanto o Scrum organiza o *trabalho*, o XP organiza o *código*.

As principais práticas do XP:

| Prática | O que é |
|---|---|
| **Programação em par (Pair Programming)** | Dois desenvolvedores trabalham em **um mesmo computador**: um "dirige" (escreve código) e o outro "navega" (revisa, sugere). Resultado: menos defeitos, compartilhamento de conhecimento |
| **TDD (Test-Driven Development)** | Escrever o **teste antes** do código. Ciclo: escrever teste (que falha) → escrever código mínimo para passar → refatorar. Veremos com detalhes no [[Testes-de-Software|Bloco 4.3]] |
| **Refatoração (Refactoring)** | **Melhorar a estrutura do código** sem alterar seu comportamento externo — eliminar duplicação, simplificar, nomear melhor |
| **Integração Contínua (CI)** | Integrar o código ao repositório **várias vezes ao dia**, executando testes automaticamente a cada integração. Você já viu isso no [[DevOps-e-Controle-de-Versao|DevOps]] |
| **Design Simples (Simple Design)** | O código deve ser o **mais simples possível** para funcionar agora — sem abstrações antecipadas |

> [!note] TDD — menção conceitual (detalhamento no Bloco 4.3)
> O **TDD** é uma prática do XP em que se escreve um **teste antes** do código de produção. O ciclo é: (1) escrever um teste que falha (**Red**); (2) escrever o código mínimo para o teste passar (**Green**); (3) **refatorar** o código mantendo os testes passando. A ideia é garantir que cada linha de código tenha um teste associado. Aprofundaremos o ciclo Red-Green-Refactor no [[Testes-de-Software|Bloco 4.3 — Testes de Software]].

> [!warning] PEGADINHA — XP é sobre práticas, Scrum é sobre organização
> A banca pode perguntar: "Qual prática é do XP e qual é do Scrum?" O **Scrum** lida com **papéis, eventos e artefatos** (organização do trabalho). O **XP** lida com **programação em par, TDD, refatoração, integração contínua** (práticas de código). São **complementares** — muitos times usam Scrum + XP juntos.

---

## 6. Comparação prática: Scrum, Kanban e XP

| Aspecto | Scrum | Kanban | XP |
|---|---|---|---|
| **Foco** | organização do trabalho | fluxo contínuo | práticas de código |
| **Unidade de tempo** | sprint (1-4 sem) | contínuo | contínuo |
| **Papéis** | PO, SM, Dev Team | não prescreve | não prescreve papéis formais |
| **Alterações no meio** | não na sprint | sim, a qualquer momento | sim |
| **WIP limits** | implícito (sprint = limit) | explícito (por coluna) | não é o foco |
| **Práticas de código** | não prescreve | não prescreve | TDD, par, refatoração, CI |
| **Métrica principal** | velocity | lead time / cycle time | defeitos / cobertura de testes |
| **Mais cobrado em concurso** | sim (muito) | moderadamente | moderadamente |

> [!tip] Regra de ouro para a prova
> Se a questão descreve **papéis, eventos (sprint, daily, review, retrospective) e artefatos (backlog, increment)** → é **Scrum**. Se descreve **tabuleiro com colunas e WIP limits** → é **Kanban**. Se descreve **programação em par, TDD, refatoração** → é **XP**. Essa separação é a chave.

---

## 7. Como a FGV cobra metodologias ágeis

- **Scrum é o framework mais cobrado** — com longa margem. A banca adora testar os três **papéis** (especialmente a diferença entre PO e SM), os **cinco eventos** (especialmente a função da Daily) e os **três artefatos**.
- **Kanban** cai quando a questão descreve um cenário de fluxo contínuo com WIP limits — e pede para identificar qual abordagem se aplica.
- **XP** cai pelas práticas (TDD, programação em par, refatoração) e pela relação com CI/CD.
- O **Manifesto Ágil** (4 valores) é cobrado direto — memorize os quatro pares de valores.

> [!warning] PEGADINHA — as cinco armadilhas mais rentáveis
> (1) **Scrum Master não é chefe/gerente** — é facilitador/servo-líder. (2) **Daily não é status report** — é sincronização do time. (3) **Product Owner não é o cliente** — é quem representa o negócio e prioriza. (4) **Kanban sem WIP limits não é Kanban** — é apenas um quadro. (5) **XP é práticas de código; Scrum é organização de trabalho** — não confunda.

---

## 8. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **Manifesto Ágil:** 4 valores (indivíduos > processos; software > docs; colaboração > contratos; mudança > plano)
> - [ ] **Scrum — papéis:** Product Owner (o quê fazer), Scrum Master (garante o processo), Dev Team (entrega)
> - [ ] **Scrum — eventos:** Sprint (ciclo), Planning (planeja), Daily (sincroniza), Review (demo), Retrospective (melhora)
> - [ ] **Scrum — artefatos:** Product Backlog (todo o produto), Sprint Backlog (sprint atual), Increment (software funcional)
> - [ ] **Scrum Master ≠ gerente** — facilitador, remove impedimentos, não atribui tarefas
> - [ ] **Kanban:** tabuleiro + **WIP limits** + fluxo contínuo; métricas: lead time, cycle time
> - [ ] **XP:** programação em par, **TDD** (Red-Green-Refactor), refatoração, **CI**, design simples
> - [ ] **Scrum** = organização · **Kanban** = fluxo · **XP** = práticas de código — são complementares

> [!warning] O erro mais comum em prova
> Confundir o **Scrum Master** com um gerente de projeto, e achar que a **Daily** é uma reunião de reporte. Na questão, pergunte: *quem decide o quê fazer? (PO) · quem garante o processo? (SM) · quem entrega? (Dev Team) · a reunião serve para sincronizar o time ou reportar ao gestor? (sincronizar)*.

---

## 9. Próximos passos

Você agora entende como o trabalho é **organizado** (Scrum, Kanban) e como o código é **escrito com qualidade** (XP). No próximo tópico, vamos estudar como as **soluções e padrões** que você já viu no Bloco 4.1 (padrões GoF, frameworks) são **reutilizados** através de **componentização, bibliotecas e frameworks** — o conceito de **reuso de software**.
