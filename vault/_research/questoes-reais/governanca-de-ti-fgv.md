# Gestão e Governança de TI — Questões Reais FGV

> Disciplina: Gestão e Governança de TI (Módulo II) · Banca: FGV · Alinhado ao Bloco 6.2 da ementa ([[COBIT-2019]], [[ITIL-v4]], [[BPMN]], [[Gerenciamento-de-Projetos]]).

> **Atenção (aderência ao edital 2026):** a seção prevê gerenciamento de projetos (áreas, projetos/programas/portfólio, abordagens tradicional/híbrida/ágil, Guia Scrum); processos e grupos de processos; gestão de riscos em TI; **ITIL v4**; **COBIT 2019**; **BPMN**. A norma **ISO/IEC 38500 não consta** no edital — a questão CNS014 que a menciona foi mantida apenas como evidência de estilo de cobrança.

## Questões reais localizadas

Classificação: **real** (todas as linhas abaixo). Sinalização: ✅ dentro · ⚠️ relacionado, não explícito · ❌ fora do programa.

| Ano | Concurso | Cargo | Tópico | Assunto cobrado | Edital 2026 | Referência |
|---|---|---|---|---|---|---|
| — | FGV — CNS014 | Analista de Gestão de Tecnologia da Informação | Governança × Gestão | Julgamento V/F combinando **COBIT 2019** (✅) e **ITIL 4** (✅): governança × gestão, pegadinha sobre CMDB/COBIT; além deles, menciona **ISO/IEC 38500:2024** (⚠️ — norma não consta no edital) | ⚠️ Parcial | Prova oficial FGV — `analista-de-gestao-tecnologia-da-informacaocns014-tipo-1.pdf` |
| 2024 | DATAPREV | Analista — Análise de Negócio de TI | BPM | Modelagem de Processos de Negócio (BPM) presente na prova | ✅ Dentro (BPMN previsto) | QConcursos — prova DATAPREV 2024 Analista de Negócio de TI |
| 2024 | DATAPREV | Analista — Análise de Negócio de TI | BPMN | Decisão com base em **condições/regras de negócio** (bifurcação no fluxo) → **gateway exclusivo** | ✅ Dentro (BPMN) | Gabarite — Q1037200 |
| 2022 | SEFAZ-AM | Analista da Fazenda — TI | BPMN | V/F: objeto de prover recursos para modelar processos (I); compreendido por analistas, técnicos e usuários (II); expressar processos (III) | ✅ Dentro (BPMN) | Magna Concursos — Q2179787 |
| 2025 | TCE PE | Analista — TI | BPMN + BPMS | Tarefa manual (avaliação jurídica) fora do BPMS; tarefa de serviço (consulta a sistema) no BPMS; **gateway exclusivo** para decidir conceder/negar; eventos de mensagem | ✅ Dentro (BPMN) | Gabarite — Q1035898 |
| 2026 | TJ-RJ | Analista Judiciário — TI/Projetos | BPMN | Representar **entrada de dados** de uma tarefa → objeto de dados / associação de dados | ✅ Dentro (BPMN) | Magna Concursos — Q4016363 |
| 2026 | AMAZUL | Engenheiro de Produção | BPMN | Ponto de decisão entre caminhos (conforme × não conforme) → **gateway exclusivo** | ✅ Dentro (BPMN) | ConcursosBR — Q6099 |
| 2026 | AMAZUL | Engenheiro de Controle da Qualidade | BPM — conceitos | V/F: análise e melhoria de processos (I, V); BPM é disciplina gerencial focada em processos (II, V); gestão por processos adota visão **funcional/vertical** (III, F); processos definem como se entrega valor (IV, V) — **B (I, II e IV)** | ✅ Dentro (BPMN/processos) | ConcursosBR — Q6521 |

> **Observação:** as questões de Scrum/ágil do TJ RR 2024 foram classificadas pela fonte como "Gestão e Governança de TI", mas são de engenharia de software — estão registradas em [[desenvolvimento-de-software-fgv]].

## Análise das questões principais

- **BPMN — gateway exclusivo (DATAPREV 2024, TCE PE 2025, AMAZUL 2026):** o elemento mais cobrado dentro de BPMN é o ponto de **decisão/bifurcação baseado em condição**. Palavra-chave: "decisão com base em condições/regras de negócio" → **gateway exclusivo (XOR)**.
- **Objetos de dados (TJ-RJ 2026):** entrada/saída de dados de uma tarefa é representada por **objeto de dados conectado por associação de dados**; os artefatos são anexos, não fluxo principal.
- **BPMS (TCE PE 2025):** o que é **automatizável** (tarefas de serviço, eventos de mensagem, gateways) vai para o BPMS; **tarefa manual** (análise jurídica, decisão humana) ocorre fora da plataforma.
- **V/F sobre frameworks (CNS014):** cada afirmativa testa um framework. Governança (COBIT — direcionar, avaliar, monitorar) × gestão/operação (ITIL — práticas, CMDB, incidentes). **ISO/IEC 38500:2024**: aparece como terceiro framework em questão FGV, mas **não está no edital 2026** — estudar apenas como contexto.
- **Conceitos de BPM (AMAZUL 2026):** BPM é disciplina **gerencial** integrando estratégia a expectativas de clientes; gestão por processos adota visão **horizontal por processos**, não funcional/vertical. Pegadinha: afirmativa que troca visão funcional pela por processos.

## Padrões de cobrança (observação)

1. **BPMN é o tema dominante de Governança na FGV recente (DATAPREV 2024, TCE PE 2025, AMAZUL 2026, TJ-RJ 2026)** — dominar os elementos básicos: eventos, atividades, gateways (exclusivo/paralelo), raias, objetos de dados, mensagens.
2. Dentro de BPMN, o **gateway exclusivo (decisão)** é o alvo preferido.
3. A FGV diferencia **governança** de **gestão** dentro da mesma questão — a fronteira conceitual é o alvo.
4. Formato **V/F com três afirmativas**, cada uma abordando um framework distinto (COBIT, ITIL, e eventualmente 38500).
5. BPM/modelagem de processos aparece como assunto da própria DATAPREV 2024 (Análise de Negócio de TI).
6. **BPMS × tarefas manuais:** a FGV cobra o que é automatizável em plataforma versus o que exige intervenção humana.

> Limitação da amostra: ainda não foi localizada questão real FGV especificamente sobre **COBIT 2019** ou **ITIL v4** com enunciado completo (apenas a V/F do CNS014 e a presença do assunto na DATAPREV 2024 — perfil Gestão de Serviços de TIC).

## Ligações com as notas

[[Gerenciamento-de-Projetos]] · [[ITIL-v4]] · [[COBIT-2019]] · [[BPMN]]