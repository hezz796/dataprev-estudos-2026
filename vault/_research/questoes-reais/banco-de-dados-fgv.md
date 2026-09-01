# Banco de Dados — Questões Reais FGV

> Disciplina: Banco de Dados · Banca: FGV · Módulo II (Conhecimentos Específicos, peso 2,5). Evidências de provas FGV 2024–2026.

> **Atenção (aderência ao edital 2026):** a seção "Inteligência de Negócios (BI) e Banco de Dados" do edital prevê: modelagem (conceitual, lógica e física); abordagem relacional e multidimensional; normalização; integridade referencial; metadados; modelagem dimensional; SQL (DDL e DML); SGBDs e propriedades ACID; NoSQL e bancos em memória; Data Lakes e Big Data; dados estruturados/não estruturados; avaliação de modelos; ETL/ELT. **Administração de BD (backup, recuperação, otimização, monitoramento) não consta no programa 2026.**

## Questões reais localizadas

Classificação: **real** (todas as linhas abaixo). Sinalização: ✅ dentro · ⚠️ relacionado, não explícito · ❌ fora do programa.

| Ano | Concurso | Cargo | Tópico | Assunto cobrado | Edital 2026 | Referência |
|---|---|---|---|---|---|---|
| 2024 | DATAPREV | Analista — Engenharia e Sustentação | SQL / Modelagem | **3 questões encadeadas** sobre o mesmo esquema relacional (candidato, questao, candidato_questao): ordem dos nomes impressa por SELECT; integridade referencial e restrição CHECK; chave primária, superchave mínima e 2FN | ✅ Dentro | Magna Concursos — Prova Completa Analista TI Engenharia e Sustentação, Q3432025–Q3432028 |
| 2024 | DATAPREV | Analista de Processamento | Normalização | Critérios da **1FN** | ✅ Dentro | Magna Concursos — Prova Completa Analista de Processamento, Q3432019 |
| 2024 | DATAPREV | Analista — Engenharia e Sustentação | SGBDs / Administração | PostgreSQL e transações (✅); backup e recuperação, otimização e monitoramento (❌ — não constam no edital) | ⚠️ Parcial | Magna Concursos — Prova Completa Analista TI Engenharia e Sustentação, Q3432024 |
| — | FGV — CNS402 | Analista Administrativo — Tecnologia (especialidade BD) | Normalização / Transações / NoSQL | Normalização (afirmativas I/II/III); **ACID em V/F com definições trocadas** (pegadinha); NoSQL/MongoDB (serialização binária) | ✅ Dentro | Prova oficial FGV — `analista-administrativo-tecnologia-com-especialidade-em-banco-de-dadoscns402-tipo-1.pdf` (site conhecimento.fgv.br) |

## Análise das questões principais

- **Questões encadeadas sobre esquema SQL (DATAPREV 2024):** habilidade de **ler DDL/DML e prever resultado**. Conceitos necessários: chave primária/estrangeira, integridade referencial, `CHECK`, formas normais, `SELECT` com ordenação/agrupamento. Estratégia: simular mentalmente a execução passo a passo.
- **1FN (DATAPREV 2024):** conceitos necessários: atomicidade de atributos, ausência de grupos repetidos. Palavra-chave: "critérios da primeira forma normal".
- **ACID com definições trocadas (CNS402):** pegadinha clássica da FGV — apresentar a definição de uma propriedade no lugar de outra (ex.: dizer que Durabilidade garante correção das transações). Estratégia: memorizar as **quatro** propriedades com suas definições exatas.
- **NoSQL/MongoDB (CNS402):** cobrança de características concretas de produtos (serialização binária → BSON). Estratégia: revisar as diferenças entre bancos NoSQL (documento, chave-valor, colunar, grafo).
- **Alternativas tecnicamente próximas:** análise do Gran (blog Banco de Dados DATAPREV): a FGV "costuma apresentar situações práticas envolvendo modelagem, SQL, normalização, integridade e funcionamento de SGBDs", com alternativas muito parecidas — atenção a alias, agregações, JOIN, `WHERE` versus `HAVING`.

## Padrões de cobrança (observação)

1. DATAPREV 2024 cobrou **modelagem, modelo relacional, normalização, SQL, integridade referencial e transações** — núcleo que **permanece no edital 2026**.
2. **Esquema real em SQL + perguntas sobre resultado/propriedades** é formato FGV de alto valor preditivo.
3. **Normalização** (1FN–3FN) aparece tanto conceitual quanto com casos de dependência funcional.
4. **PostgreSQL** é SGBD citado na prova DATAPREV.
5. Diferenças **DDL/DML** (`CREATE`, `ALTER`, `DROP`, `TRUNCATE` × `INSERT`, `UPDATE`, `DELETE`) e efeitos de `UPDATE` sem `WHERE` são pontos de pegadinha.
6. **Administração de BD (backup, otimização, monitoramento)** apareceu na prova 2024, mas está fora do edital 2026 — não priorizar.

## Ligações com as notas

[[Fundamentos-e-Modelagem]] · [[Normalizacao]] · [[Transacoes-e-ACID]] · [[SQL-DDL-e-DML]] · [[NoSQL]] · [[Big-Data]]