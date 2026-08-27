---
description: "Cria simulados baseados no conteúdo estudado e, quando disponível, nos padrões observados em questões reais."
agent: coordinator
---

Crie um simulado com base no conteúdo disponível no vault.

Solicitação:

$ARGUMENTS

## Procedimento

1. Verifique o escopo solicitado.
2. Consulte a ementa.
3. Identifique os conteúdos já estudados.
4. Verifique os pré-requisitos.
5. Consulte questões reais relacionadas ao escopo, quando disponíveis.
6. Identifique padrões de cobrança relevantes.
7. Acione o `question-author`.
8. Produza o simulado.
9. Acione o `text-quality-reviewer`.
10. Valide o resultado.
11. Salve em:

```text
vault/_questions/simulados/
```

## Regras

Não inclua:

- conteúdo posterior ao estágio estudado;
- questões linguisticamente ambíguas por erro de redação;
- conteúdo fora do escopo sem justificativa.

Questões autorais podem reproduzir características de cobrança observadas nas questões reais, mas não devem copiar ou apenas parafrasear uma questão existente.

## Uso de questões reais

Questões reais devem servir como:

- evidência de cobrança;
- referência de dificuldade;
- fonte de padrões;
- inspiração para competências avaliadas.

Não apresente uma questão autoral como questão oficial.

## Resultado

Informe:

- quantidade de questões;
- disciplinas;
- tópicos;
- distribuição;
- dificuldade;
- padrões de cobrança utilizados;
- resultado da revisão textual;
- localização do simulado;
- localização do gabarito.