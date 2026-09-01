# Padrões Gerais da Banca FGV

> Análise de banca transversal. Base: questões reais localizadas em provas FGV 2023–2026 (amostra não exaustiva, ~50 itens). Nada aqui deve ser tratado como conclusão estatisticamente sustentada — são observações de padrão.

> **Aderência ao edital 2026:** os arquivos de disciplina sinalizam cada evidência como ✅ dentro, ⚠️ relacionado (não explícito) ou ❌ fora do programa (ver `Edital.md`). Evidências fora do edital (ex.: probabilidade e análise combinatória em RLM; backup/otimização em BD) servem apenas para conhecer o estilo da banca, não para definir prioridade de estudo.

## Estilo

- Enunciado curto e objetivo; cenário prático; alternativas **tecnicamente muito próximas**.
- Comando recorrente: "Assinale a opção correta/incorreta" e julgamento de afirmativas (V/F).
- Em TI, não cobra apenas decoreba: contextualiza (esquema SQL, cenário de ataque, cenário de projeto, texto em inglês).
- Questões **encadeadas**: 2–3 questões sobre o mesmo texto/cenário (observado em Inglês, Banco de Dados e interpretação).
- Em RLM, alternativas em faixas ("inferior a 0,01", "entre 0,05 e 0,08") aparecem com frequência.
- Na prova DATAPREV 2024 houve questões anuladas (marcadas com `*` no gabarito oficial). Por isso: gabarito só deve ser registrado quando confirmado.

## Habilidades mais exigidas (observação)

- Comparar e aplicar conceitos (mais que memorizar definições).
- Identificar a pegadinha de **troca de definições** (ACID, pilares do Scrum, COBIT versus ITIL). *Ex.: a norma ISO/IEC 38500 aparece em questão FGV de exemplo, mas não consta no edital 2026 — o padrão que importa é governança (COBIT) × gestão (ITIL).*
- Ler código/SQL e prever saída.
- Relacionar categoria de risco × exemplo de vulnerabilidade (OWASP).

## Pegadinhas recorrentes (observação)

- Afirmativa "dispensar mecanismo X porque Y garante segurança" é quase sempre falsa (API/OAuth, TLS).
- Confundir governança (COBIT — previsto no edital) com gestão/operação (ITIL, CMDB).
- Trocar definições de propriedades (ACID, princípios de segurança).
- Atribuir ao Product Owner tarefa que não é dele (planejar recursos do time).

## Observações versus conclusões

- **Observação (recorrência qualitativa):** tabelas verdade e negação em RLM; OWASP Top 10 em múltiplas provas recentes; Java/Spring no perfil de desenvolvimento; crase/regência/concordância e valores semânticos de preposições em Português; **BPMN com gateway exclusivo** em Governança; **IA conceitual-aplicada** (agente, prompt, ética/viés) em Atualidades e IA.
- **Conclusão estatística:** não sustentada por esta amostra. Para percentuais exatos por tópico, seria preciso catalogar provas completas.

## Fontes preferenciais

- Provas oficiais FGV: `https://conhecimento.fgv.br` (inclui página do concurso DATAPREV 2024 e PDFs de cadernos e gabaritos).
- Agregadores: QConcursos, Gran Questões, Questões Estratégicas, Gabarite, Magna Concursos, ResolvaMais.

## Ligações com a ementa

- Módulo I: [[Lingua-Portuguesa|Português]], [[Lingua-Inglesa|Inglês]], [[Raciocinio-Logico-Matematico|RLM]], [[LGPD-Lei-Geral-de-Protecao-de-Dados|LGPD]].
- Módulo II: [[Banco-de-Dados|Banco de Dados]], [[Desenvolvimento-de-Software|Desenvolvimento]], [[Seguranca-da-Informacao|Segurança]], [[Gestao-e-Governanca-de-TI|Governança]].