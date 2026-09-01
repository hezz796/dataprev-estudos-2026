# Pesquisa de Questões Reais — Padrões de Cobrança

> **Alvo:** DATAPREV 2026 · Analista de TI — Perfil 3: Desenvolvimento de Software · Banca: **FGV**

## Objetivo

Reunir **questões reais aplicadas pela FGV** como evidência de cobrança para fundamentar:

- notas do Writer;
- questões autorais do Question Author;
- simulados;
- análise de banca.

## Política (skill `question-research`)

- Questões **reais** → evidência de cobrança. Questões **autorais** → prática. Nunca misturar.
- Não inventar metadados (ano, concurso, cargo, gabarito). Quando não confirmados, fica ``—``.
- Preferir `metadados + referência + análise + padrão` à reprodução integral do enunciado.
- Não contornar restrições de acesso (ex.: provas em sites com assinatura).

## Aderência ao edital 2026

Cada arquivo de disciplina sinaliza, linha a linha, a aderência das evidências ao conteúdo programático do `Edital.md`:

- ✅ **Dentro** — o assunto consta explicitamente no programa;
- ⚠️ **Relacionado, não explícito** — o assunto não aparece por extenso no programa, mas deriva de um tópico previsto;
- ❌ **Fora** — o assunto não consta no programa (evidência útil apenas para conhecer o estilo da banca).

Resumo dos achados após auditoria contra o edital:

| Assunto nas evidências | Situação no edital 2026 |
|---|---|
| Probabilidade, Teorema de Bayes, análise combinatória (RLM) | ❌ Fora — não constam no programa de RLM |
| Backup, recuperação, otimização e monitoramento de BD | ❌ Fora — não constam na seção de Banco de Dados |
| Maven (ferramenta de build) | ⚠️ Relacionado — edital cita Java e frameworks, mas não Maven |
| BDD | ⚠️ Relacionado — edital cita TDD explicitamente, não BDD |
| ISO/IEC 38500:2024 | ⚠️ Relacionado — edital cita COBIT 2019 e ITIL v4, não a norma 38500 |
| FDE/TDE/VPN e criptografia em repouso/trânsito | ⚠️ Relacionado — derivado de "mecanismos de segurança" e "SSL/TLS" |

> **Rodada 2 (fechada em set/2026):** foram adicionadas evidências para tópicos antes sem questões — ISO 27001/27002, tríade CID, IAM/SSO/ABAC (ver [[seguranca-e-lgpd-fgv]]); **APF/Story Points** (ver [[desenvolvimento-de-software-fgv]]); **BPMN**, inclusive questão **DATAPREV 2024** (ver [[governanca-de-ti-fgv]]); negação de proposições e indução em RLM (ver [[raciocinio-logico-fgv]]); e a disciplina nova **Atualidades e IA**, com evidências de estilo FGV 2025–2026 em PDFs oficiais (`conhecimento.fgv.br`) — ver [[atualidades-e-ia-fgv]].

## Fontes utilizadas

- Provas oficiais e gabaritos FGV: `https://conhecimento.fgv.br` (página do concurso DATAPREV 2024 e PDFs de provas oficiais).
- QConcursos, Gran Questões, Questões Estratégicas, Gabarite, Magna Concursos, ResolvaMais.
- Caderno de questões DATAPREV 2024 (Editora Solução) e simulados baseados na prova oficial (JR Concursos, Gabarite).

## Estrutura da prova (edital 2026)

| Módulo | Disciplina | Questões | Peso unitário | Peso total |
|---|---|---|---|---|
| I — Conhecimentos Gerais | Língua Portuguesa | 12 | 1,0 | 12 |
| I — Conhecimentos Gerais | Língua Inglesa | 12 | 1,0 | 12 |
| I — Conhecimentos Gerais | Raciocínio Lógico Matemático | 5 | 1,0 | 5 |
| I — Conhecimentos Gerais | Atualidades e Inteligência Artificial | 6 | 1,0 | 6 |
| I — Conhecimentos Gerais | Legislação de Segurança da Informação e LGPD | 5 | 1,0 | 5 |
| II — Conhecimentos Específicos | Conhecimentos Específicos (perfil) | 30 | 2,5 | 75 |
| **Total** | | **70** | | **115** |

> O edital 2026 mantém o formato geral de 70 questões e 115 pontos (40 × 1,0 + 30 × 2,5). A distribuição interna do Módulo I mudou em relação a 2024: RLM saiu de 6 para **5** questões e Atualidades passou de 5 para **6** (como "Atualidades e Inteligência Artificial").

## Índice

| Arquivo | Disciplina |
|---|---|
| [[padroes-gerais-fgv\|Padrões gerais FGV]] | Estilo da banca (transversal) |
| [[portugues-fgv\|Português]] | Língua Portuguesa |
| [[raciocinio-logico-fgv\|Raciocínio Lógico-Matemático]] | RLM |
| [[ingles-fgv\|Inglês]] | Língua Inglesa |
| [[atualidades-e-ia-fgv\|Atualidades e IA]] | Atualidades + Inteligência Artificial |
| [[banco-de-dados-fgv\|Banco de Dados]] | BD, SQL, modelagem, NoSQL |
| [[desenvolvimento-de-software-fgv\|Desenvolvimento de Software]] | Java, Spring, engenharia ágil, testes, DevOps |
| [[seguranca-e-lgpd-fgv\|Segurança e LGPD]] | Segurança da Informação + legislação |
| [[governanca-de-ti-fgv\|Governança de TI]] | ITIL, COBIT, BPMN |

## Uso

1. **Question Author:** usar padrões e referências desta pasta para criar questões autorais com pegadinhas equivalentes, sem copiar questões reais.
2. **Simulados:** espelhar a distribuição da prova (12/12/5/6/5/30).
3. **Writer:** citar nos blocos de "como cai na prova" das notas — respeitando a aderência ao edital.