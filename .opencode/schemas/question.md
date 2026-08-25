---
name: question
description: "Define a estrutura lógica de questões e avaliações produzidas pelo Question Author."
---

# Question

Uma questão representa uma unidade de avaliação do conhecimento.

## Identificação

```text
id
disciplina
tópico
subtópico
```

## Origem

A questão deve ser identificada como:

```text
autoral
real
adaptada
```

Quando for real, registre somente informações conhecidas:

```text
banca
concurso
cargo
ano
```

Não invente origem.

## Avaliação

Quando pertinente:

```text
habilidade cognitiva
dificuldade
conhecimento avaliado
```

## Estrutura

Uma questão pode possuir:

```text
enunciado
alternativas
gabarito
```

## Comentário

Quando for questão comentada:

```text
raciocínio
análise das alternativas
palavra-chave
pegadinha
```

## Simulado

Um simulado pode possuir:

```text
id
nome
escopo
disciplinas
tópicos
quantidade
dificuldade
questões
gabarito
```

## Regras

- questão autoral não deve ser apresentada como oficial;
- resposta deve ser inequívoca;
- distratores devem ser plausíveis;
- conteúdo deve pertencer à ementa;
- pré-requisitos devem ser respeitados;
- questões não devem depender de conteúdo posterior à etapa avaliada.