# Relatório — Lote de Questões Autorais (Setembro/2026)

> **Alvo:** DATAPREV 2026 · Analista de TI — Perfil 3: Desenvolvimento de Software · Banca de referência: **FGV**
> **Data de conclusão do lote:** 2026-09-01
> **Status:** ✅ APROVADO

## Escopo

Produção e validação de **22 questões autorais comentadas** distribuídas em 5 arquivos, cobrindo 5 disciplinas do Módulo II (Conhecimentos Específicos, peso 2,5x):

| Arquivo | Disciplina | Bloco | Questões | IDs |
|---|---|---|---|---|
| `testes-questoes-autorais.md` | Testes de Software | 4.3 | 4 | TESTES-001 a 004 |
| `banco-de-dados-questoes-autorais.md` | Banco de Dados | 3.1 | 5 | BD-001 a 005 |
| `frontend-questoes-autorais.md` | Frontend Web | 5.1 | 4 | FRONT-001 a 004 |
| `seguranca-da-informacao-questoes-autorais.md` | Segurança da Informação | 6.1 | 5 | SEG-001 a 005 |
| `governanca-de-ti-questoes-autorais.md` | Gestão e Governança de TI | 6.2 | 4 | GOV-001 a 004 |

Junto aos dois arquivos anteriores já validados (`java-spring`, `metodologias`), o diretório `questoes-autorais/` passa a totalizar **7 arquivos** de prática.

## Processo executado

1. **Question Author** produziu as questões autorais comentadas (5 despachos).
2. **Validação de saída** (coordenação):
   - **Schema:** todos os arquivos seguem o formato do README (id, disciplina, tópico, subtópico, origem, habilidade cognitiva, dificuldade, conhecimento avaliado, enunciado, alternativas A–E, gabarito, comentário com raciocínio/palavra-chave/conceito/análise das alternativas/pegadinha, padrões de cobrança).
   - **Sem cópia:** cenários e enunciados são originais; as referências a provas reais (DATAPREV 2024, FGV CNS402, AMAZUL 2026 etc.) são apenas indicação de *padrão de cobrança* que inspirou a questão — nenhum item real foi reproduzido ou parafraseado.
   - **Aderência ao edital:** todos os tópicos mapeiam para a ementa (Blocos 3.1, 4.3, 5.1, 6.1 e 6.2). Exclusões são justificadas (ISO/IEC 38500 fora do edital; CSRF não cobrado por ainda não constar das notas estudadas; VPN/FDE/TDE sinalizados como relacionados, não priorizados).
3. **Text Quality Reviewer** revisou os 5 arquivos (ver "Correções aplicadas").
4. **Auditoria pedagógica** (ver "Resultado da auditoria").

## Correções aplicadas

| Arquivo | Problema | Correção |
|---|---|---|
| `testes-questoes-autorais.md` | **Corrupção grave:** monólogo interno do autor (~87 linhas), artefato de tool call (`<tool_call>`), rascunho da Q04 (gabarito A) e conteúdo final duplicado coexistiam no arquivo | Arquivo reescrito: mantida a versão final (Q01–Q04 com gabaritos A, B, C, D, sendo a Q04 na versão com gabarito D), remoção de todo o resíduo de processo; arquivo final com 265 linhas |
| `governanca-de-ti-questoes-autorais.md` | Typo "BLoco" → "Bloco" (seção Padrões de cobrança, item 5) | Corrigido |
| `seguranca-da-informacao-questoes-autorais.md` | Concordância: "não foram incluídas" → "não foram incluídos" (sujeito composto misto, Q04) | Corrigido |
| `banco-de-dados-questoes-autorais.md` | Nenhum | — |
| `frontend-questoes-autorais.md` | Nenhum | — |

## Resultado da auditoria pedagógica

**Veredito: ✅ APROVADO** em todos os 5 arquivos.

- **Estrutura:** disciplinas, tópicos e subtópicos corretos conforme a ementa; localização correta no vault (`_research/questoes-autorais/`).
- **Progressão:** pré-requisitos respeitados (ex.: Testes assume Desenvolvimento/Scrum; Segurança assume LGPD/Módulo I); sem antecipação indevida; conceitos utilizados já constam das notas estudadas.
- **Conteúdo:** cobertura adequada dentro da amostra de 4–5 questões por disciplina; sem lacunas relevantes; conteúdo fora do escopo apenas quando justificado.
- **Didática:** cenários contextualizados no domínio DATAPREV/benefícios previdenciários; comentários integrando teoria e aplicação.
- **Prova:** palavras-chave e mnemônicos adequados ao formato FGV; pegadinhas explicadas corretamente (troca de definições, inversões de conceitos, afirmações absolutas); formatos de julgamento de afirmativas (V/F) compatíveis com o estilo da banca.

### Recomendações não bloqueantes (polimento futuro)

1. `testes-questoes-autorais.md` — seção "Padrões de cobrança", item 3: o rótulo **"Caixa-preta ≠ teste manual"** não corresponde fielmente ao corpo do item (que trata de conhecer o código → caixa-preta ≠ caixa-branca). Sugestão: renomear para **"Caixa-preta ≠ conhecimento do código"**.
2. `frontend-questoes-autorais.md` — Q03, comentário: a expressão **"Derivado normal disso:"** é informal. Sugestão: **"Consequência natural disso:"**.

## Registro de decisões

- Questões autorais **não** são apresentadas como oficiais; a origem é sempre marcada como `autoral`.
- Questões sem evidência FGV direta são marcadas como neutras ou com lacuna de evidência declarada (ex.: SDL/SAST/DAST).
- Não foi inventada nenhuma origem de banca/ano/concurso.

## Próximos passos sugeridos

- Incorporar as recomendações não bloqueantes em um passe de polimento.
- Expandir cobertura para lacunas de amostra quando houver novas notas estudadas (ex.: BDD em Testes; Big Data em BD; CSRF em Segurança no Desenvolvimento).
- Manter o ciclo: toda nova disciplina despachada ao Question Author deve atualizar o índice do README e este relatório.