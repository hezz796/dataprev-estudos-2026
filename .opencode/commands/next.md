---
description: "Identifica e executa a próxima etapa pedagógica válida, incluindo revisão textual e auditoria."
agent: coordinator
---

Determine qual é a próxima etapa válida da produção pedagógica.

Não peça ao usuário informações que possam ser obtidas a partir dos artefatos existentes.

## Analise

1. ementa;
2. disciplinas;
3. tópicos;
4. subtópicos;
5. notas existentes;
6. pré-requisitos;
7. revisão textual;
8. auditorias;
9. questões;
10. simulados.

## Determinação

Identifique:

```text
último ponto concluído
→ dependências satisfeitas
→ próxima unidade válida
→ agente responsável
```

## Produção de notas

Se a próxima etapa for uma nota:

```text
Writer
  ↓
Text Quality Reviewer
  ↓
Pedagogical Auditor
```

## Produção de questões

Se a próxima etapa for uma questão:

```text
Question Author
  ↓
Text Quality Reviewer
```

## Correções

Se houver material pendente de correção:

```text
correção
  ↓
Text Quality Reviewer
  ↓
Pedagogical Auditor
```

quando aplicável.

## Regras

- não recrie conteúdo existente;
- não ultrapasse pré-requisitos;
- não pule etapas pedagógicas;
- não considere material concluído sem as revisões necessárias;
- preserve a ordem da ementa.

Ao final, informe:

- etapa executada;
- agente utilizado;
- arquivos criados ou alterados;
- resultado das revisões;
- próxima etapa disponível.