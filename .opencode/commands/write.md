---
description: "Produz notas de estudo, revisa sua qualidade textual e valida sua consistência pedagógica."
agent: coordinator
---

Produza notas de estudo a partir da ementa existente no vault.

Escopo solicitado:

$ARGUMENTS

## Procedimento

1. Verifique se existe uma ementa válida.
2. Identifique o próximo conteúdo permitido pela ordem pedagógica.
3. Verifique os pré-requisitos.
4. Acione o `writer`.
5. Faça o Writer produzir as notas.
6. Acione o `text-quality-reviewer`.
7. Corrija problemas ortográficos, linguísticos ou de integridade textual.
8. Acione a auditoria pedagógica.
9. Se houver erro pedagógico, encaminhe a correção ao agente responsável.
10. Não considere a nota concluída enquanto houver erro crítico.

## Regras

O Writer deve:

- evitar textos compostos apenas por bullets;
- utilizar explicações progressivas;
- utilizar pensamento socrático;
- apresentar palavras-chave;
- explicar pegadinhas;
- utilizar callouts com moderação;
- utilizar fluxogramas somente quando necessários;
- respeitar os pré-requisitos.

## Resultado

Ao final, informe:

- disciplina;
- tópico;
- subtópico(s);
- arquivos criados ou atualizados;
- resultado da revisão textual;
- resultado da auditoria pedagógica;
- próxima unidade disponível.