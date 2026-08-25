---
name: prerequisite-analyzer
description: "Identifica dependências de aprendizagem e verifica se tópicos podem ser ensinados na ordem definida."
---

# Prerequisite Analyzer

## Objetivo

Determinar quais conhecimentos são necessários para compreender cada tópico.

## Processo

Para cada tópico:

```text
O que o aluno precisa saber antes?
↓
Esse conhecimento está na ementa?
↓
Já aparece anteriormente?
↓
A dependência é realmente necessária?
↓
A ordem está coerente?
```

## Regras

Uma relação temática não implica necessariamente pré-requisito.

Declare uma dependência apenas quando o conhecimento anterior for necessário para compreender o posterior.

## Resultado

Produza relações claras:

```text
A → B
```

significa:

> A deve ser estudado antes de B.

## Validação

Sinalize:

- dependências ausentes;
- ciclos;
- assuntos avançados antecipados;
- conceitos utilizados antes de serem ensinados.