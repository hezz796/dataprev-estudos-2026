---
name: note-writer
description: "Define como produzir notas didáticas, estruturadas e adequadas ao Obsidian."
---

# Note Writer

## Objetivo

Produzir notas de estudo claras, progressivas e agradáveis de ler a partir da ementa pedagógica.

## Estrutura

A nota deve respeitar:

- disciplina;
- tópico;
- subtópico;
- pré-requisitos;
- progressão pedagógica.

Não introduza conceitos que dependam de conteúdos ainda não estudados.

## Didática

Evite transformar a nota em uma sequência de listas.

Prefira:

- explicações em prosa;
- exemplos;
- comparações;
- tabelas quando úteis;
- perguntas orientadoras;
- aplicações práticas.

Utilize listas somente quando elas realmente facilitarem a compreensão.

## Pensamento socrático

Utilize perguntas para conduzir o aluno ao raciocínio.

Exemplo:

> Se as duas proposições precisam ser verdadeiras, o que acontece quando uma delas é falsa?

A pergunta deve ajudar o aluno a descobrir ou compreender o conceito.

Não transforme toda nota em um questionário.

## Concursos

Quando pertinente, explique:

- como a banca costuma cobrar o assunto;
- palavras-chave;
- diferenças entre conceitos;
- exceções;
- pegadinhas;
- erros comuns de interpretação;
- estratégias para identificar a resposta.

## Obsidian

Produza Markdown compatível com Obsidian.

Utilize quando apropriado:

- Wiki Links;
- callouts;
- tabelas;
- listas;
- código;
- fluxogramas.

Não utilize recursos visuais apenas para ornamentação.

## Callouts

Use callouts para destacar informações relevantes.

Exemplo:

> [!important]
> Atenção para a diferença entre os conceitos.

Outros tipos podem ser utilizados quando fizerem sentido:

- `[!tip]`
- `[!warning]`
- `[!example]`
- `[!note]`
- `[!important]`

Não exagere na quantidade.

## Fluxogramas

Utilize fluxogramas somente quando eles facilitarem a compreensão de:

- processos;
- decisões;
- classificações;
- relações;
- sequências.

Não transforme uma explicação simples em fluxograma.

## Notação matemática e formal

Quando o conteúdo envolver:

- matemática;
- raciocínio lógico;
- estatística;
- probabilidade;
- contabilidade com fórmulas;
- economia;
- física;
- computação matemática;
- lógica formal;

utilize LaTeX compatível com o Obsidian.

### Expressões inline

Utilize:

```text
$...$
```

Exemplo:

```text
A probabilidade do evento é $P(A)$.
```

### Expressões em bloco

Utilize:

```text
$$
...
$$
```

Exemplo:

```text
$$
P(A \cap B) = P(A)P(B \mid A)
$$
```

### Fórmulas multilinha

Quando uma expressão matemática precisar de quebra de linha ou alinhamento, utilize obrigatoriamente:

```text
$$
\begin{split}
...
\\
...
\end{split}
$$
```

Exemplo:

```text
$$
\begin{split}
A &= B + C \\
  &= D + E
\end{split}
$$
```

Não utilize `\\` isoladamente fora de um ambiente apropriado.

### Sistemas e sequências de transformações

Quando houver uma sequência de igualdades ou transformações, prefira:

```text
$$
\begin{split}
x + 2 &= 10 \\
x &= 10 - 2 \\
x &= 8
\end{split}
$$
```

### Sistemas de equações

Para sistemas, utilize uma estrutura compatível com o ambiente LaTeX disponível no Obsidian.

Exemplo:

```text
$$
\begin{cases}
x + y = 10 \\
x - y = 2
\end{cases}
$$
```

Quando houver necessidade de alinhamento interno entre expressões, utilize `split` adequadamente.

### Regra de preservação

Não utilize LaTeX para substituir texto comum.

A notação formal deve ser acompanhada de explicação em linguagem natural quando isso facilitar a compreensão.

Exemplo:

```markdown
A condicional é representada por:

$$
p \rightarrow q
$$

Ela pode ser lida como "se $p$, então $q$".
```

## Código

Blocos de código devem utilizar as cercas Markdown apropriadas e nunca devem ser tratados como LaTeX.

## Wiki Links

Utilize:

```text
[[Nome da nota]]
```

quando a nota relacionada existir no vault.

Não crie links artificiais apenas para aumentar a quantidade de conexões.

## Glossário

Quando um termo já possuir entrada no glossário, utilize:

```text
[[Termo]]
```

Não crie automaticamente uma entrada de glossário apenas porque um termo parece difícil.

O glossário é alimentado principalmente pelas dúvidas reais do estudante.

## Coerência

Uma nota expandida ou revisada deve preservar:

- estrutura;
- terminologia;
- Wiki Links;
- callouts;
- fórmulas;
- exemplos;
- progressão pedagógica.

Alterações posteriores não devem quebrar a coerência da nota.