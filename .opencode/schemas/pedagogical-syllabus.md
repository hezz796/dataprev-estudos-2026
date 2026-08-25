---
name: pedagogical-syllabus
description: "Define a estrutura da ementa pedagógica utilizada como fonte de verdade para produção e avaliação do material."
---

# Pedagogical Syllabus

A ementa é a fonte de verdade da progressão pedagógica.

## Estrutura

```text
Ementa
├── objetivo
├── disciplinas
│   ├── tópicos
│   │   ├── subtópicos
│   │   ├── pré-requisitos
│   │   └── dependências
│   └── ...
├── mapa de dependências
├── cobertura do edital
└── ordem recomendada
```

## Disciplina

Uma disciplina deve possuir:

```text
id
nome
ordem
tópicos
```

## Tópico

Um tópico pode possuir:

```text
id
nome
ordem
pré-requisitos
dependências
subtópicos
prioridade
origem
```

## Subtópico

Um subtópico representa uma unidade de aprendizagem.

Pode possuir:

```text
id
nome
ordem
pré-requisitos
dependências
```

## Origem

Utilize:

```text
edital
pré-requisito
```

## Prioridade

Quando disponível:

```text
alta
média
baixa
não definida
```

Prioridade de prova não altera automaticamente a ordem pedagógica.

## Dependências

Se:

```text
A → B
```

então A deve ser compreendido antes de B.

Evite dependências artificiais.

## Cobertura

Todo conteúdo relevante do edital deve estar representado.

Conteúdos adicionados para permitir aprendizagem devem ser identificados como pré-requisitos pedagógicos.

## Função

A ementa serve de contrato para:

- Writer;
- Question Author;
- Pedagogical Auditor.