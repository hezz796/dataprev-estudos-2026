# Desenvolvimento de Software — Questões Reais FGV

> Disciplinas: Desenvolvimento de Sistemas, Metodologias e Engenharia de Software, Testes de Software, DevOps · Banca: FGV · Módulo II (peso 2,5) — núcleo do Perfil 3.

> **Atenção (aderência ao edital 2026):** o edital lista explicitamente Java (v6+), JavaEE, JakartaEE, JPA, JavaScript, JUnit, Hibernate, JSF, Primefaces, Spring, Spring Cloud, Spring Boot, mobile, low-code/no-code, Clean Code/SonarQube, SOA, web services, APIs, REST, JSON, XML, XSLT, DevOps, GIT; Scrum/Kanban/XP; **APF/Story Points**; TDD e testes automatizados. **Maven não é citado** (apenas os frameworks da lista) e **BDD não é citado** (apenas TDD) — são temas relacionados, não explícitos.

## Questões reais localizadas

Classificação: **real** (todas as linhas abaixo). Sinalização: ✅ dentro · ⚠️ relacionado, não explícito · ❌ fora do programa.

| Ano | Concurso | Cargo | Tópico | Assunto cobrado | Edital 2026 | Referência |
|---|---|---|---|---|---|---|
| 2024 | DATAPREV | Analista — Desenvolvimento de Software | Java / Frameworks | Spring, Spring Cloud, Spring Boot, Hibernate, JUnit | ✅ Dentro | Gran Questões — prova DATAPREV 2024 |
| 2025 | AMAZUL | Analista de Desenvolvimento de Sistemas | Java / Ferramentas | Java 8 **Streams API** (✅ — Java); ciclo de vida do **Maven** (⚠️ — ferramenta não citada no edital) | ⚠️ Parcial | Prova oficial FGV — `ok-analista-de-desenvolvimento-de-sistemas-cnsa103-tipo-1.pdf` |
| 2024 | DATAPREV | Analista — Desenvolvimento de Software | Metodologias ágeis | Escolha da metodologia ágil adequada (Scrum, Kanban, XP, Waterfall, Lean) | ✅ Dentro | Gabarite — Q1042704 |
| 2025 | CGE SP (Controladoria SP) | Auditor Estadual — Controle TI (tarde) | Scrum | Papel responsável pelo **Product Backlog** (visível, transparente, claro) | ✅ Dentro | Questões Estratégicas — questão 48 |
| 2026 | MPE-ES | Agente Técnico — Desenvolvedor | Testes | **TDD × BDD** (living documentation, especificações em linguagem natural) — **B (BDD)** | ⚠️ Relacionado (TDD consta; BDD não é citado) | Gran Questões — Q4630955 / Questões Estratégicas — questão 34 |
| 2024 | TJ RR | Analista de TI — Gestão e Governança | Scrum / Kanban | Time Scrum (dono do produto não é superior hierárquico; Scrum Master responde pela efetividade); manifesto ágil (valores); WIP e lead time no Kanban | ✅ Dentro | Gabarite — Q1037577 e Q897116 |
| 2024 | INPE | Tecnologista Júnior — Desenvolvimento (embarcado) | Scrum | Pilares do Scrum ("eliminação de reuniões" é falso), backlog do produto, papel do Product Owner | ✅ Dentro | Questões Estratégicas — prova INPE 2024 |
| 2024 | TJ RJ | Programa de Residência — TI | DevOps | Prática de **CI/CD** (builds e testes automatizados) | ✅ Dentro (DevOps) | Gran Questões — prova TJ RJ 2024 |
| 2018 | BANESTES | Analista TI — Desenvolvimento de Sistemas | APF | APF: **independe da tecnologia**; não deriva de linhas de código; mede a funcionalidade do ponto de vista do usuário antes do desenvolvimento (somente III) | ✅ Dentro (APF/Story Points) | Gran Questões — Q975497 |
| 2022 | SEAD-AP | Professor de Educação Básica — Informática | APF | APF usada para **medir o software quantificando tarefas e serviços** visando estimativa de orçamento/dimensionamento — **D** | ✅ Dentro (APF/Story Points) | Estude Grátis — Q1007236 |
| 2024 | SES (PE) | Analista de Sistemas — DBA | APF | FPA/IFPUG: "ponto de função" mede **funcionalidades sob o ponto de vista do usuário** (o que o software faz) — não mede como foi construído | ✅ Dentro (APF/Story Points) | Gran Questões — Q3252363 |
| 2025 | — (FGV) | — | APF × Story Points | V/F: PF **não** necessariamente medem qualidade/produtividade comparando projetos (F); Story Points são métrica **informal/relativa** de métodos ágeis, não formal (F); PF cabem a projetos tradicionais e Story Points a projetos ágeis (F) — **F-F-F** | ✅ Dentro (APF/Story Points) | ResolvaMais — Q1548229 |
| — | BADESC | Analista de Sistemas | APF | Componentes da APF: relatório com totalização = **saída externa**; objetivo = medir funcionalidades requisitadas/recebidas pelo usuário; "Arquivo" = grupo de dados logicamente relacionados | ✅ Dentro (APF/Story Points) | Gabarite — Q115637 |

## Análise das questões principais

- **TDD × BDD (MPE-ES 2026):** a FGV descreve a metodologia e pede o nome — *living documentation*, especificações em linguagem natural executáveis como testes → **BDD**. Palavra-chave: "linguagem natural" + "entendimento comum clientes/analistas/desenvolvedores". Acompanhar por ser tema próximo do programa (Testes); o edital cita TDD explicitamente.
- **Scrum — papéis:** Product Owner gerencia o backlog e decide o que construir; Scrum Master cuida da efetividade do processo; desenvolvedores criam o incremento. Pegadinhas: "PO é superior hierárquico" (falso), "PO planeja os recursos da Sprint" (falso), "pilar do Scrum é eliminar reuniões" (falso).
- **Manifesto ágil:** a FGV troca valores ("documentação abrangente mais que software funcionando" é **o inverso** do manifesto — falso). Palavra-chave: "mais do que X, Y".
- **Kanban:** WIP (limitar trabalho em progresso) e lead time (tempo da entrada à finalização da tarefa).
- **APF (BANESTES, SES, SEAD-AP, ResolvaMais, BADESC):** ponto de função mede **tamanho funcional sob a ótica do usuário**, **independente da tecnologia/linguagem**; aplicável antes do código (estimativa de tamanho e custo). Pegadinhas: "depende da tecnologia", "deriva de linhas de código", "mede como o software foi construído" — todas **falsas**.
- **Story Points (FGV 2025):** métrica **informal e relativa** dos métodos ágeis (Scrum/XP), por história; PF cabem a projetos tradicionais com estimativas padronizadas. A FGV inverte as duas e cobra como V/F — resposta **F-F-F**.
- **Java/ecossistema:** Spring Boot/Cloud, Hibernate, JUnit e Streams API aparecem no perfil de desenvolvimento (✅). **Maven** é cobrado pelo ciclo de vida (validate → compile → test → verify → install), mas **não consta no edital 2026** — registrar como conhecimento de apoio, não prioridade.

## Padrões de cobrança (observação)

1. **Java + Spring/Hibernate/JUnit** é o coração do Perfil 3 na FGV (DATAPREV 2024 e AMAZUL 2025) — todos com previsão explícita no edital.
2. **Scrum e o manifesto ágil** são os temas mais repetidos em metodologias (CGE SP, TJ RR, INPE, MPE-ES, DATAPREV).
3. **APF/Story Points** é assunto recorrente de engenharia de software na FGV (BANESTES 2018, SES 2024, FGV 2025) e agora **previsto no edital** — dominar conceitos de APF (independente de tecnologia, ótica do usuário) e a distinção PF × Story Points.
4. Formato frequente: **julgamento de afirmativas (V/F)** sobre papéis e práticas, com uma afirmativa falsa sutil.
5. **Testes** entram com distinção entre TDD/BDD e práticas de CI/CD (TDD e DevOps previstos; BDD como conhecimento de apoio).
6. Cobrança de **ferramentas práticas** (Streams, Maven) indica que o candidato deve conhecer APIs e ciclos, não só teoria.

## Ligações com as notas

[[Java-e-Ecossistema-JVM]] · [[Frameworks-Java]] · [[Metodologias-Ageis]] · [[Fundamentos-de-Teste]] · [[Testes-Automatizados]] · [[Testes-Ageis]] · [[DevOps-e-Controle-de-Versao]] · [[Padroes-de-Projeto-e-Arquitetura]] · [[Gestao-do-Ciclo-de-Vida-de-Testes]]