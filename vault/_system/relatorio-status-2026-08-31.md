# Relatório de Status — Projeto Pedagógico DATAPREV 2026

> [!info] Metadados do relatório
> **Data de geração:** 2026-08-31
> **Cargo:** Analista de TI — Perfil 3: Desenvolvimento de Software
> **Finalidade:** Registro do estado atual da produção pedagógica, para orientar futuras correções e ajustes (NOTA: nenhum arquivo de conteúdo foi alterado na geração deste relatório).
> **Fonte de verdade utilizada:** [[vault/_system/ementa|ementa.md]], inventário do vault e histórico de versionamento (git log).

---

## 1. Estado Geral da Ementa

**Status: COMPLETA E ATUAL**

- Arquivo: `vault/_system/ementa.md`
- Versão: v1.0 (2026-08-26)
- Estrutura: 6 fases, 13 blocos/disciplinas, tópicos e subtópicos definidos.
- Contém: pesos por módulo, matriz de pré-requisitos e sequência didática recomendada.

---

## 2. Inventário de Disciplinas

| # | Disciplina (Bloco) | Fase | Notas produzidas | Status |
|---|--------------------|------|------------------|--------|
| 1 | Língua Portuguesa | 1 | 13 | Concluída* |
| 2 | Raciocínio Lógico Matemático | 1 | 5 | Concluída |
| 3 | Legislação de Seg. Info. e LGPD | 1 | 4 | Concluída |
| 4 | Língua Inglesa | 2 | 2 | Concluída |
| 5 | Atualidades e Inteligência Artificial | 2 | 3 | Concluída |
| 6 | Banco de Dados | 3 | 6 | Concluída |
| 7 | Desenvolvimento de Sistemas | 4 | 8 | Concluída |
| 8 | Metodologias e Eng. de Software | 4 | 5 | Concluída |
| 9 | Testes de Software | 4 | 5 | Concluída |
| 10 | Frontend Web | 5 | 3 | Concluída |
| 11 | UX e Gestão de Conteúdo | 5 | 2 | Concluída |
| 12 | Arquitetura Avançada | 5 | 5 | Concluída |
| 13 | Segurança da Informação | 6 | 2 | Em andamento |
| 14 | Gestão e Governança de TI | 6 | 0 | Pendente |

> \* Língua Portuguesa está completa em notas, **porém com uma pendência de revisão textual** (ver seção 4).

### Resumo das disciplinas

- **Concluídas (10):** Língua Portuguesa, Raciocínio Lógico Matemático, Legislação, Língua Inglesa, Atualidades e IA, Banco de Dados, Desenvolvimento de Sistemas, Metodologias e Engenharia de Software, Testes de Software, Arquitetura Avançada.
- **Em andamento (1):** Segurança da Informação (Bloco 6.1) — 2 de 4 tópicos.
- **Pendentes (1):** Gestão e Governança de TI (Bloco 6.2) — 0 de 4 tópicos.

> **Observação — BI e Data Warehouse:** figura apenas na Matriz de Pré-requisitos da ementa (dependência de Banco de Dados), sem bloco formal com tópicos na sequência didática. Não é contabilizado como pendência de nota no fluxo atual; revisar se o edital exige tratamento dedicado.

---

## 3. Notas de Estudo

- **Total produzido: 63**
- **Pendentes (faltam na ementa): 6 tópicos**

### Notas pendentes

| Disciplina | Tópico | Subtópicos (ementa) |
|-----------|--------|---------------------|
| Segurança da Informação | 3. Gestão de Riscos | Identificação e avaliação de riscos · Matriz de risco (probabilidade × impacto) · Planos de contingência e recuperação |
| Segurança da Informação | 4. Segurança no Desenvolvimento | SDL (Security Development Lifecycle) · OWASP Top 10 · SAST · DAST · Dependabot e gestão de dependências |
| Gestão e Governança de TI | 1. Gerenciamento de Projetos | Tradicional (Waterfall), Híbrido, Ágil · Métricas (CPI, SPI, EVM) |
| Gestão e Governança de TI | 2. ITIL v4 | Serviço de TI · Dimensões · Práticas · Ciclo de vida do serviço |
| Gestão e Governança de TI | 3. COBIT 2019 | Governança e gestão · Objetivos · Princípios · Relação com ITIL |
| Gestão e Governança de TI | 4. BPMN | Notação · Modelagem · Subprocessos e pools/lanes · BPMN × UML |

---

## 4. Revisão Textual

- **Aprovadas:** sem registro formal (não há painel de status de revisão aprovada).
- **Pendentes (1), registrada explicitamente:**
  - **Nota 6 de Língua Portuguesa** — `vault/Fase-1-Fundamentos/Lingua-Portuguesa/Reescrita-de-Frases-e-Paragrafos.md`
  - Indicada em `vault/PARA PESQUISAR.md`: *"Falta checar a qualidade de texto da nota 6 de língua portuguesa"*.
  - Confirmada pelo commit `4c3aea9` — *"Língua portuguesa completa sem chegar a qualidade de texto da nota 6"*.
- **Com problemas:** nenhum detectado na inspeção (arquivos em UTF-8 válido, acentuação íntegra).

> **Ação recomendada:** executar o fluxo `Text Quality Reviewer` sobre a nota 6 de Língua Portuguesa ("Reescrita de Frases e Parágrafos").

---

## 5. Auditoria Pedagógica

- **Aprovadas:** sem registro.
- **Pendentes:** 63 (nenhuma nota com evidência de auditoria registrada).
- **Com problemas:** nenhum identificado até o momento.

> **Nota:** a auditoria pedagógica (Pedagogical Auditor) e a revisão textual não possuem painel/índice de rastreamento no vault. Recomenda-se criar um mecanismo de registro de status por nota para acompanhar o fluxo `Writer → Revisão Textual → Auditoria`.

---

## 6. Questões

- **Quantidade: 0**
- A infraestrutura de pesquisa e geração de questões foi preparada (agentes, skills e comandos — ver commit `8abf1f9`), mas **nenhuma questão autoral, questão comentada ou relatório de pesquisa foi produzido**.
- Não há diretório/arquivo para questões no vault.

---

## 7. Simulados

- **Quantidade: 0**
- Nenhum simulado gerado.

---

## 8. Próxima Etapa Recomendada

A unidade imediata e com pré-requisitos satisfeitos:

```text
DISCIPLINA : Segurança da Informação (Bloco 6.1)
TÓPICO     : 3. Gestão de Riscos
SUBTOPICOS : Identificação/avaliação de riscos · Matriz probabilidade x impacto ·
             Planos de contingência e recuperação
AGENTE     : Writer → Text Quality Reviewer → Pedagogical Auditor
```

A nota **"Autenticacao-e-Autorizacao"** (Tópico 2) encerra apontando o Tópico 3 — Gestão de Riscos como próximo passo.

---

## 9. Bloqueios e Riscos

### Bloqueios atuais

- **Nenhum bloqueio de dependência** para a próxima nota (Gestão de Riscos depende de Fundamentos de Segurança + LGPD — ambos já produzidos).

### Riscos e pontos de atenção para etapas futuras

1. **Bloco 6.2 (Gestão e Governança de TI):** exige Metodologias + Segurança da Informação 6.1 + visão integrada das fases anteriores. Fica **bloqueado** até a conclusão do Bloco 6.1.
2. **Revisão textual da nota 6 de Língua Portuguesa** segue pendente (ver seção 4).
3. **Ausência de rastreio de revisão/auditoria:** convém implantar um painel de status para evitar re-trabalho e garantir que o material passe integralmente pelo fluxo de qualidade.
4. **Questões e simulados:** a criação só deve ser apresentada como "baseada em padrões de banca" **após** a pesquisa de questões reais (evitar afirmar aderência sem evidência).

---

## 10. Plano de Ação Sugerido (ordem)

| Ordem | Ação | Agente |
|-------|------|--------|
| 1 | Revisão textual da nota 6 de Língua Portuguesa | Text Quality Reviewer |
| 2 | Produzir nota "Gestão de Riscos" (Bloco 6.1, Tópico 3) | Writer |
| 3 | Revisão textual e auditoria da nota "Gestão de Riscos" | Text Quality Reviewer / Pedagogical Auditor |
| 4 | Produzir nota "Segurança no Desenvolvimento" (Bloco 6.1, Tópico 4) | Writer |
| 5 | Revisão textual e auditoria da nota "Segurança no Desenvolvimento" | Text Quality Reviewer / Pedagogical Auditor |
| 6 | Produzir as 4 notas do Bloco 6.2 (Gestão e Governança de TI), na ordem da ementa | Writer |
| 7 | Revisão textual e auditoria das notas do Bloco 6.2 | Text Quality Reviewer / Pedagogical Auditor |
| 8 | (Recomendado) Implantar painel de status de revisão/auditoria por nota | Coordenador |
| 9 | (Quando a pesquisa estiver disponível) Produzir questões autorais e simulados | Question Researcher / Question Author |

---

> [!note] Controle de revisão deste relatório
> Ao aplicar correções, atualize este documento marcando o item concluído com a data e o commit correspondente, para manter o rastreio do projeto.
