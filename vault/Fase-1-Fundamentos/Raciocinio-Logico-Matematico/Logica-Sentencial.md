# Lógica Sentencial

> [!info] Metadados
> **Disciplina:** Raciocínio Lógico Matemático
> **Bloco:** 1.2 — Raciocínio Lógico Matemático (FASE 1 — Fundamentos)
> **Tópico:** 3. Lógica sentencial
> **Subtópicos:** Tabelas-verdade · Equivalências lógicas (leis de De Morgan, distributiva, associativa, exportação) · Diagramas de Venn para proposições simples
> **Pré-requisitos:** [[Estruturas-Logicas]] e [[Logica-de-Argumentacao]]
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-27

---

## 1. Por que estudar lógica sentencial?

Pense no que já construímos até aqui. Na [[Estruturas-Logicas]], você aprendeu as **peças** do raciocínio: o que é uma proposição, quais são os conectivos ($\neg$, $\land$, $\lor$, $\oplus$, $\to$, $\leftrightarrow$), como eles funcionam e qual a ordem de precedência. Na [[Logica-de-Argumentacao]], você aprendeu a **avaliar raciocínios inteiros**: distinguir dedução de indução e abdução, encadear premissas com Modus Ponens e Modus Tollens, reconhecer quando uma conclusão se segue ou não das premissas.

Mas ficou uma lacuna importante. Em vários momentos daquelas notas, afirmamos coisas como "a condicional só é falsa quando a hipótese é verdadeira e a conclusão é falsa" ou "o Modus Tollens funciona porque $P \to Q$ não pode ser verdadeira com $P$ verdadeira e $Q$ falsa". Como sabemos disso com certeza? De onde vem essa garantia? A resposta é exatamente o objeto deste tópico: a **lógica sentencial** é a máquina de calcular da lógica. Ela nos dá dois instrumentos poderosos:

1. as **tabelas-verdade**, que permitem calcular o valor de verdade de *qualquer* proposição composta, em *todas* as situações possíveis; e
2. as **equivalências lógicas**, que permitem afirmar que duas proposições diferentes dizem exatamente a mesma coisa — e portanto podem ser trocadas uma pela outra sem alterar nenhum resultado.

Essa capacidade de "calcular" e "comparar" valores de verdade não é um luxo teórico. Em programação — o seu cargo é Analista de TI — toda condição de `if`, todo filtro de uma consulta, toda regra de negócio é, no fundo, uma proposição composta. Saber negar corretamente a condição "se o usuário está logado e tem permissão, então a ação é liberada" é exatamente aplicar De Morgan e a negação da condicional. As bancas de concurso sabem disso e cobram esse tópico com altíssima frequência, tanto na forma direta (montar a tabela, identificar tautologia) quanto na forma aplicada (qual expressão é equivalente a outra, qual negação está correta).

> [!tip] Conexão com o pré-requisito
> Se conectivos, precedência ou as regras de Modus Ponens/Tollens ainda não estão firmes, revisite [[Estruturas-Logicas]] e [[Logica-de-Argumentacao]] antes de prosseguir. Este tópico parte do pressuposto de que você sabe, por exemplo, que $\land$ exige as duas verdadeiras e que $\to$ só falha em um único caso: $V \to F$.

---

## 2. Tabelas-verdade

### 2.1 O que é e para que serve

Uma **tabela-verdade** é um quadro que organiza, lado a lado, todas as combinações possíveis de valores de verdade das proposições simples que compõem uma proposição composta e o valor resultante da proposição composta em cada combinação.

Para que serve? Pense em um laboratório. Uma proposição composta é uma "máquina" com entradas ($P$, $Q$, $R$, ...) e uma saída (o valor final). A tabela-verdade liga a máquina em **todas** as configurações possíveis de entrada e registra a saída em cada uma. Com esse registro em mãos, conseguimos responder perguntas definitivas:

- Em que situações a proposição é verdadeira? Em que situações é falsa?
- Duas proposições diferentes sempre produzem a mesma saída? (isso é equivalência — seção 3)
- A proposição é verdadeira em *todos* os casos? (tautologia), em *nenhum*? (contradição), ou depende? (contingência)

> [!question] Pergunta orientadora
> Uma proposição composta com uma única proposição simples $P$, como $\neg P$, tem duas situações possíveis: $P$ verdadeira ou $P$ falsa. E com duas proposições $P$ e $Q$? Quantas combinações de valores existem? E com três? Note o padrão: cada proposição nova **dobra** a quantidade de combinações.

### 2.2 Quantas linhas? A fórmula $2^n$ (e a pegadinha das proposições distintas)

Se cada proposição simples pode assumir dois valores (V ou F), e cada proposição nova dobra a quantidade de combinações, então uma proposição composta com $n$ **proposições simples distintas** gera uma tabela-verdade com:

$$2^n \text{ linhas}$$

| Número de proposições simples distintas | Linhas da tabela |
|:---:|:---:|
| 1 | $2^1 = 2$ |
| 2 | $2^2 = 4$ |
| 3 | $2^3 = 8$ |
| 4 | $2^4 = 16$ |

Aqui mora a primeira grande pegadinha do tópico — e talvez a mais frequente nas provas que cobram o cálculo do número de linhas:

> [!warning] PEGADINHA nº 1 — o $n$ da fórmula são as proposições simples **distintas**
> O expoente $n$ é o número de proposições simples **diferentes** que aparecem na expressão, e não o número de conectivos e nem o número de ocorrências de letras.
>
> Veja três exemplos que confundem candidatos:
> - $P \lor Q$ → duas proposições distintas ($P$ e $Q$) → $2^2 = 4$ linhas.
> - $P \land P$ → **uma** proposição distinta (o $P$ aparece duas vezes, mas é a mesma) → $2^1 = 2$ linhas.
> - $\neg(P \lor Q) \to R$ → três proposições distintas ($P$, $Q$, $R$) → $2^3 = 8$ linhas, mesmo tendo três conectivos.
>
> **Regra de ouro:** sublinhe cada letra diferente na expressão. Se "P" apareceu cinco vezes, conta **uma** vez. O conectivo não conta nada — ele só *liga* proposições, não cria proposição nova.

> [!warning] PEGADINHA nº 2 — contar conectivos em vez de proposições
> Uma questão pode apresentar "$P \land Q \lor \neg R$" e perguntar quantas linhas tem a tabela. O candidato apressado conta três conectivos ($\land$, $\lor$, $\neg$) e responde $2^3 = 8$. Coincidentemente, nesse caso, acertou — porque também há três proposições distintas. Mas a banca pode apresentar algo como "$P \lor \neg P$": um conectivo de cada tipo, mas apenas **uma** proposição distinta. A tabela tem $2^1 = 2$ linhas, e não $2^2 = 4$. **Sempre ignore os conectivos na contagem: o que importa são as letras diferentes.**

Outra pegadinha associada: proposições repetidas alteram a tabela? Não. A expressão $P \land P$ é logicamente idêntica a $P$ (veremos isso na idempotência, seção 3.10). Uma tabela de duas linhas é suficiente porque o comportamento de $P \land P$ já está completamente determinado pelo valor de $P$.

### 2.3 Construção passo a passo

Construir uma tabela-verdade é um procedimento mecânico — e, como todo procedimento mecânico, quem segue os passos na ordem certa não erra. O fluxo é este:

```text
1. Identificar as proposições simples DISTINTAS da expressão
                        │
                        ▼
2. Contar n = número de proposições distintas
                        │
                        ▼
3. Calcular 2ⁿ = número de linhas
                        │
                        ▼
4. Preencher as colunas das proposições simples
   (distribuir V/F no padrão: metade V, metade F, alternando)
                        │
                        ▼
5. Montar as colunas intermediárias
   (na ordem de precedência: ¬ antes de ∧/∨ antes de → antes de ↔)
                        │
                        ▼
6. Montar a coluna final
   (aplicando o conectivo de menor precedência sobre os resultados)
                        │
                        ▼
7. Analisar a coluna final
   toda V → tautologia | toda F → contradição | tem V e F → contingência
```

O passo 4 merece atenção. Para a **primeira** coluna (a proposição mais à esquerda), preencha a metade superior com V e a metade inferior com F. Para cada coluna seguinte, divida o bloco pela metade e alterne V/F: na segunda proposição, blocos de V e F; na terceira, blocos menores ainda. O resultado é o padrão "alternado" que garante que todas as combinações apareçam exatamente uma vez.

> [!note] Reutilizando os "tijolos" já estudados
> Você não precisa recalcular nada de novo: as tabelas de cada conectivo já foram estudadas em [[Estruturas-Logicas]] e são os **tijolos** da construção. A conjunção só é V quando as duas partes são V; a disjunção só é F quando as duas partes são F; a condicional só é F em $V \to F$; o bicondicional só é V quando os valores são iguais; a negação inverte. Toda coluna intermediária e a coluna final são obtidas aplicando esses tijolos sobre colunas anteriores.

Vamos aplicar o procedimento em dois exemplos completos.

> [!example] Exemplo 1 — construção completa com 3 proposições simples: $(P \land Q) \to R$
>
> **Passo 1:** proposições distintas: $P$, $Q$, $R$ → $n = 3$.
> **Passo 2:** $2^3 = 8$ linhas.
> **Passo 3:** distribuir valores: $P$ com 4 V e 4 F; $Q$ com blocos de 2; $R$ alternando.
> **Passo 4:** coluna intermediária $P \land Q$ (tijolo da conjunção).
> **Passo 5:** coluna final $(P \land Q) \to R$ (tijolo da condicional: só dá F quando o antecedente é V e o consequente é F).
>
> | $P$ | $Q$ | $R$ | $P \land Q$ | $(P \land Q) \to R$ |
> |:---:|:---:|:---:|:---:|:---:|
> | V | V | V | V | **V** |
> | V | V | F | V | **F** |
> | V | F | V | F | **V** |
> | V | F | F | F | **V** |
> | F | V | V | F | **V** |
> | F | V | F | F | **V** |
> | F | F | V | F | **V** |
> | F | F | F | F | **V** |
>
> Perceba o padrão: o resultado só é **F** em uma única linha — exatamente a linha em que $P \land Q$ é V (o antecedente) e $R$ é F (o consequente). É a regra da condicional funcionando como previsto.

> [!example] Exemplo 2 — colunas intermediárias em cascata: o caso $P \to Q \equiv \neg P \lor Q$
>
> Vamos montar a tabela de $P \to Q$, mas passando por colunas intermediárias: primeiro $\neg P$, depois $\neg P \lor Q$. Ao final, comparamos com a coluna de $P \to Q$:
>
> | $P$ | $Q$ | $\neg P$ | $\neg P \lor Q$ | $P \to Q$ |
> |:---:|:---:|:---:|:---:|:---:|
> | V | V | F | V | **V** |
> | V | F | F | F | **F** |
> | F | V | V | V | **V** |
> | F | F | V | V | **V** |
>
> As duas últimas colunas são idênticas, linha por linha. Isso já demonstra, na prática, uma equivalência importante (seção 3.5): $P \to Q \equiv \neg P \lor Q$. Guarde este exemplo — ele será um atalho enorme na resolução de questões.

> [!important] Precedência e parênteses: sua defesa contra a ambiguidade
> Na hora de decidir **quais** colunas intermediárias montar, respeite a precedência estudada: $\neg$ primeiro; depois $\land$ e $\lor$ (mesmo nível, da esquerda para a direita); depois $\to$; por último $\leftrightarrow$. Mas não confie apenas nela: **use parênteses** sempre que houver qualquer dúvida. Uma expressão com parênteses explícitos não deixa margem para interpretação — e a banca adora incluir, entre as alternativas, o resultado da interpretação *errada* da precedência.

### 2.4 Tautologia, contradição e contingência

Depois que a coluna final está montada, basta olhar para ela. Três classificações cobrem todos os casos possíveis:

| Classificação | Coluna final da tabela-verdade | Exemplo típico |
|---|---|---|
| **Tautologia** | Todas as linhas são **V** | $P \lor \neg P$ |
| **Contradição** | Todas as linhas são **F** | $P \land \neg P$ |
| **Contingência** | Tem pelo menos uma **V** e pelo menos uma **F** | $P \to Q$ |

- **Tautologia** é a proposição que é verdadeira em *qualquer* situação, independentemente dos valores das proposições simples. "Chove ou não chove" — um dos dois lados sempre é verdadeiro. Na prova, dizemos que a proposição é **tautológica** ou é uma **tautologia**, e o operador lógico correspondente é o $\top$ (verdade lógica).
- **Contradição** é o oposto exato: falsa em *todas* as situações, por uma impossibilidade estrutural. "Chove e não chove" não pode ser verdadeiro em nenhum cenário. Simboliza-se por $\bot$ (falsidade lógica).
- **Contingência** é tudo o que sobra: depende dos valores das entradas. A grande maioria das proposições compostas reais é contingente. "Se chover, levarei guarda-chuva" é verdadeira em alguns cenários e falsa em outros (justamente quando chove e eu não levo).

> [!warning] PEGADINHA — tautologia ≠ proposição "sempre verdadeira no mundo"
> A tautologia é uma propriedade **estrutural**: a proposição é verdadeira em *todas as linhas da tabela*, por pura forma, não por conteúdo. "$P \lor \neg P$" é tautologia porque a estrutura "P ou não-P" cobre todas as possibilidades — não porque descobrimos algo sobre o mundo. Da mesma forma, "$P \land \neg P$" é contradição mesmo que você nunca tenha visto o que $P$ significa. A banca pode tentar convencer você de que "O Sol é uma estrela" é tautologia porque é verdadeira — **não é**. Tautologia só se verifica na tabela-verdade, nunca no conteúdo.

> [!tip] Como a banca cobra
> A cobrança típica é tríplice: (1) calcular o número de linhas ($2^n$); (2) montar a tabela e pedir o valor em uma linha específica; (3) perguntar "a proposição é tautológica, contraditória ou contingente?". Verificar tautologia é o atalho favorito para questões de equivalência: **$P \equiv Q$ se e somente se $P \leftrightarrow Q$ é uma tautologia** (retomaremos isso na seção 3.1).

---

## 3. Equivalências lógicas

### 3.1 O que é uma equivalência lógica (e como verificar)

Duas proposições compostas $A$ e $B$ são **logicamente equivalentes** quando produzem o mesmo valor de verdade em **todas** as linhas — ou seja, quando a tabela-verdade de uma é idêntica à da outra. Escrevemos $A \equiv B$ e lemos "A é equivalente a B". Trocar A por B (ou B por A) em qualquer contexto **nunca altera um resultado**: é como trocar "2 + 2" por "4" numa conta. O símbolo $\equiv$ **não é** um conectivo da linguagem — é uma afirmação do lógico *sobre* duas proposições: "essas duas dizem exatamente a mesma coisa".

> [!warning] Cuidado: $\equiv$ não é $\leftrightarrow$
> O bicondicional $\leftrightarrow$ é um conectivo que *forma* uma proposição composta ($P \leftrightarrow Q$); a equivalência $\equiv$ é uma *relação* entre proposições. A ponte entre eles é útil na prova: $A \equiv B$ vale exatamente quando $A \leftrightarrow B$ é uma **tautologia**. Ou seja, para testar se duas expressões são equivalentes, monte o bicondicional entre elas e verifique se a coluna final é toda V.

A verificação por tabela-verdade é o método mais seguro e o que a banca espera que você domine. O procedimento: montar lado a lado as colunas de $A$ e de $B$ e conferir, linha por linha, se são idênticas. Nada de "achar que faz sentido" — a tabela decide.

> [!question] Pergunta orientadora
> Se $A \equiv B$ e $B \equiv C$, o que podemos afirmar sobre $A$ e $C$? Se duas proposições são equivalentes a uma terceira, ambas dizem a mesma coisa que a terceira — portanto dizem a mesma coisa entre si. A equivalência é **transitiva**, e isso permite simplificar em cadeia, trocando trechos de uma expressão por equivalentes mais convenientes.

### 3.2 Leis de De Morgan

As **leis de De Morgan** (em homenagem ao matemático Augustus De Morgan) respondem a uma pergunta que aparece em toda prova: **como negar uma conjunção ou uma disjunção?**

A resposta intuitiva seria "negue cada lado". Mas é exatamente aí que mora o erro mais clássico do tópico. Vamos descobrir a resposta certa com uma pergunta:

> [!question] Pergunta orientadora
> Se a conjunção $P \land Q$ exige as **duas** verdadeiras, o que acontece quando negamos a conjunção? A afirmação "é falso que P e Q" significa que **nenhuma** das duas é verdadeira, ou que **pelo menos uma** é falsa? Pense no exemplo: "É falso que o candidato é formado E tem experiência." Isso significa que ele não é formado **e** não tem experiência — ou que ele pode até ser formado, mas sem experiência (ou vice-versa)?

A resposta: negar "P e Q" exige apenas que **pelo menos uma** das partes seja falsa. E negar "P ou Q" exige que **ambas** sejam falsas (afinal, para o "ou" inclusivo ser falso, os dois lados precisam ser falsos). Formalizando:

$$
\begin{split}
\neg(P \land Q) &\equiv \neg P \lor \neg Q \\
\neg(P \lor Q) &\equiv \neg P \land \neg Q
\end{split}
$$

**Leia assim:** a negação de "P e Q" é "não-P **ou** não-Q"; a negação de "P ou Q" é "não-P **e** não-Q". O que era $\land$ vira $\lor$; o que era $\lor$ vira $\land$; e a negação "entra" distribuindo-se sobre cada proposição.

> [!warning] PEGADINHA — a negação da conjunção NÃO é $\neg P \land \neg Q$
> O erro mais cobrado de todo este tópico: achar que $\neg(P \land Q)$ equivale a $\neg P \land \neg Q$. Formalmente, isso seria "os dois são falsos" — muito mais forte do que a negação exige. Pense no exemplo do recrutador: dizer que é falso que "o candidato é formado **e** tem experiência" não significa que ele não é formado **e** não tem experiência; pode ter uma das qualificações. A única leitura correta é $\neg P \lor \neg Q$.

Vamos verificar a primeira lei com a tabela-verdade lado a lado:

| $P$ | $Q$ | $P \land Q$ | $\neg(P \land Q)$ | $\neg P$ | $\neg Q$ | $\neg P \lor \neg Q$ |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| V | V | V | F | F | F | **F** |
| V | F | F | V | F | V | **V** |
| F | V | F | V | V | F | **V** |
| F | F | F | V | V | V | **V** |

Colunas $\neg(P \land Q)$ e $\neg P \lor \neg Q$ idênticas. A segunda lei se verifica do mesmo jeito:

| $P$ | $Q$ | $\neg P$ | $\neg Q$ | $\neg(P \lor Q)$ | $\neg P \land \neg Q$ |
|:---:|:---:|:---:|:---:|:---:|:---:|
| V | V | F | F | F | **F** |
| V | F | F | V | F | **F** |
| F | V | V | F | F | **F** |
| F | F | V | V | V | **V** |

> [!tip] De Morgan em linguagem natural (a tradução que a banca usa)
> - $\neg(P \land Q)$: "**Não** é verdade que chove **e** faz frio" ≡ "**Não** chove **ou não** faz frio".
> - $\neg(P \lor Q)$: "**Não** é verdade que estudo **ou** trabalho" ≡ "**Não** estudo **e não** trabalho".
>
> A banca raramente escreve os símbolos. Ela disfarça: coloca uma frase negada e pergunta qual frase equivale a ela. Traduzir a frase para símbolos primeiro — e depois aplicar De Morgan — é a estratégia que evita o erro.
>
> **Para o Analista de TI:** negar uma condição em código é De Morgan. Se a regra é "entrar se (logado **e** admin)", a negação é "bloquear se (não logado **ou** não admin)". Algumas linguagens chamam isso de *De Morgan's laws* em expressões booleanas — é exatamente a mesma coisa.

> [!warning] Pegadinha transversal — o "ou" envolvido em De Morgan é o **inclusivo**
> Quando aplicamos $\neg(P \lor Q) \equiv \neg P \land \neg Q$, estamos tratando o "ou" como inclusivo, o padrão da lógica formal (retomando a pegadinha já vista em [[Estruturas-Logicas]]: todo "ou" é inclusivo salvo indicação explícita). Se o enunciado disser "ou...ou, mas não ambos" ($\oplus$), as leis mudam — e o resultado não é $\neg P \land \neg Q$. A negação correta de $P \oplus Q$ é $P \leftrightarrow Q$ (veremos a ponte na seção 3.7). Desconfie sempre que a questão usar expressões como "exatamente um" ou "mas não ambos".

### 3.3 Negação da condicional

A condicional foi o conectivo mais traiçoeiro da nota [[Estruturas-Logicas]], e a pegadinha continua aqui. Qual é a negação de $P \to Q$?

Raciocine com a tabela da condicional. $P \to Q$ é falsa em **exatamente uma** situação: quando $P$ é V e $Q$ é F. Logo, negar a condicional é afirmar justamente esse caso: "$P$ é verdadeira **e** $Q$ é falsa". Formalmente:

$$\neg(P \to Q) \equiv P \land \neg Q$$

> [!warning] PEGADINHA — a negação da condicional NÃO é $\neg P \to \neg Q$
> O erro clássico: negar "se P então Q" como "se não-P então não-Q" (negar os dois lados e manter a seta). Está errado. Negar uma condicional **não é** uma condicional — é uma **conjunção**. Veja o exemplo cotidiano: "Se chover, levarei guarda-chuva." Qual é a negação? "Choveu **e** eu não levei" ($P \land \neg Q$), e não "se não chover, não levarei" ($\neg P \to \neg Q$). Matematicamente, $\neg P \to \neg Q$ é apenas a *inversa* da condicional, que tem valores de verdade diferentes.

Verificação por tabela-verdade:

| $P$ | $Q$ | $P \to Q$ | $\neg(P \to Q)$ | $P \land \neg Q$ |
|:---:|:---:|:---:|:---:|:---:|
| V | V | V | F | **F** |
| V | F | F | V | **V** |
| F | V | V | F | **F** |
| F | F | V | F | **F** |

Colunas idênticas. Guarde esse par no bolso: **negação de "se...então" = "e" com a segunda negada**.

> [!tip] Aplicação direta em prova
> Questões clássicas pedem a negação de frases como "Se o sistema está ativo, então os dados são sincronizados". A resposta correta é "O sistema está ativo **e** os dados **não** são sincronizados". A banca costuma colocar como alternativa atraente "Se o sistema não está ativo, então os dados não são sincronizados" — exatamente a pegadinha $\neg P \to \neg Q$.

### 3.4 Contraposição (contraposta)

Se a negação da condicional nos diz quando a promessa é quebrada, a **contraposição** nos dá uma segunda forma de *dizer a mesma promessa*. Compare as duas frases:

- "Se chover, levarei guarda-chuva." ($P \to Q$)
- "Se eu não levar guarda-chuva, então não choveu." ($\neg Q \to \neg P$)

Elas dizem a mesma coisa, em ordem diferente. A **contraposição** (ou **contraposta**) da condicional $P \to Q$ é a condicional $\neg Q \to \neg P$, obtida invertendo as posições **e** negando os dois lados:

$$P \to Q \equiv \neg Q \to \neg P$$

| $P$ | $Q$ | $P \to Q$ | $\neg Q$ | $\neg P$ | $\neg Q \to \neg P$ |
|:---:|:---:|:---:|:---:|:---:|:---:|
| V | V | **V** | F | F | **V** |
| V | F | **F** | V | F | **F** |
| F | V | **V** | F | V | **V** |
| F | F | **V** | V | V | **V** |

> [!important] Conexão com a lógica de argumentação
> A contraposição é a justificativa formal do **Modus Tollens** estudado em [[Logica-de-Argumentacao]]. Se $P \to Q$ é verdadeira, então $\neg Q \to \neg P$ também é — e afirmar $\neg Q$ torna $\neg P$ inevitável. Quando a banca pergunta "qual proposição é equivalente a 'se P então Q'?", a contraposição é uma alternativa quase sempre presente — e correta.

> [!warning] Não confunda contraposição com recíproca nem com inversa
> Dada $P \to Q$, existem três transformações clássicas, e a banca mistura as três:
>
> | Nome | Forma | Equivalente a $P \to Q$? |
> |---|---|---|
> | **Contraposição (contraposta)** | $\neg Q \to \neg P$ | ✅ Sim |
> | **Recíproca (conversa)** | $Q \to P$ | ❌ Não |
> | **Inversa** | $\neg P \to \neg Q$ | ❌ Não |
>
> Observe que a inversa e a recíproca são equivalentes *entre si* (uma é contraposição da outra) — mas **nenhuma** é equivalente à condicional original. A pegadinha favorita: oferecer $Q \to P$ como "equivalente" de $P \to Q$.

### 3.5 Condicional como disjunção

Lembre-se do Exemplo 2 da seção 2.3: a tabela de $P \to Q$ tinha a mesma coluna final que $\neg P \lor Q$. Essa é a equivalência que transforma toda condicional em disjunção:

$$P \to Q \equiv \neg P \lor Q$$

Por que isso funciona? A condicional só é falsa em $V \to F$. Em qualquer outro caso é verdadeira. Ora, $\neg P \lor Q$ é falsa apenas quando $\neg P$ é F ($P$ V) **e** $Q$ é F — exatamente o mesmo cenário. As duas expressões são duas maneiras de dizer "ou a hipótese não se cumpre, ou a conclusão se cumpre — ou ambas".

> [!tip] Quando essa equivalência é ouro na prova
> Questões que pedem "o valor de verdade de $P \to Q$" quando você conhece os valores de $P$ e $Q$ podem ser resolvidas mais rápido trocando a condicional por $\neg P \lor Q$. E questões que pedem a **negação da condicional** ganham um caminho alternativo: $\neg(P \to Q) \equiv \neg(\neg P \lor Q) \equiv P \land \neg Q$ — a última passagem aplica De Morgan (seção 3.2). Veja como as equivalências se conectam: uma alimenta a outra.

Essa equivalência também explica por que "a menos que" vira disjunção: "Vou à festa **a menos que** chova" ($\neg C \to V$) equivale a $V \lor C$ — exatamente como estudado em [[Estruturas-Logicas#3.8 Outros termos e formas de expressar os conectivos|Estruturas Lógicas]].

### 3.6 Bicondicional em termos de condicionais

O bicondicional $P \leftrightarrow Q$ já foi introduzido em [[Estruturas-Logicas]] como "ida e volta". A formalização disso é uma equivalência:

$$P \leftrightarrow Q \equiv (P \to Q) \land (Q \to P)$$

Dizer "$P$ se e somente se $Q$" é dizer **duas** coisas ao mesmo tempo: "se $P$, então $Q$" **e** "se $Q$, então $P$". A conjunção entre as duas condicionais garante que os valores andem juntos. Na prática, questões difíceis "escondem" um bicondicional atrás de duas condicionais — e reconhecer essa forma ajuda a quebrar o enunciado.

> [!tip] Combinação com a seção 3.5
> Usando $P \to Q \equiv \neg P \lor Q$ duas vezes, podemos reescrever o bicondicional só com $\neg$, $\land$ e $\lor$:
>
> $$P \leftrightarrow Q \equiv (\neg P \lor Q) \land (\neg Q \lor P)$$
>
> Não decore essa forma estendida — apenas saiba que ela existe. O importante é reconhecer $(P \to Q) \land (Q \to P)$ como a definição de trabalho do bicondicional.

### 3.7 A ponte com a disjunção exclusiva

Na nota de [[Estruturas-Logicas]], ficou registrada uma relação poderosa: a disjunção exclusiva é a **negação** do bicondicional. Formalmente:

$$P \oplus Q \equiv \neg(P \leftrightarrow Q)$$

Onde o bicondicional é verdadeiro (valores iguais: V/V ou F/F), a exclusiva é falsa; onde o bicondicional é falso (valores diferentes: V/F ou F/V), a exclusiva é verdadeira. Linha a linha, são opostos exatos.

Essa ponte nos dá um resultado útil que dialoga com a pegadinha do "ou exclusivo": a negação de $P \oplus Q$ é $P \leftrightarrow Q$. Ou seja, negar "exatamente um dos dois" equivale a afirmar "os dois têm o mesmo valor" — os dois verdadeiros ou os dois falsos. Se a banca pedir a negação de uma frase com "ou...ou, mas não ambos", a resposta não é De Morgan ($\neg P \land \neg Q$), e sim o bicondicional.

### 3.8 Propriedades distributivas

A **distributividade** permite "abrir" uma expressão que combina $\land$ com $\lor$ — o equivalente lógico da propriedade distributiva da aritmética ($a \cdot (b + c) = a \cdot b + a \cdot c$). São duas leis, que formam um par:

$$
\begin{split}
P \land (Q \lor R) &\equiv (P \land Q) \lor (P \land R) \\
P \lor (Q \land R) &\equiv (P \lor Q) \land (P \lor R)
\end{split}
$$

A primeira diz que "P **e** (Q **ou** R)" abre em "(P **e** Q) **ou** (P **e** R)". A segunda — menos intuitiva — diz que "P **ou** (Q **e** R)" abre em "(P **ou** Q) **e** (P **ou** R)". Repare que, ao contrário da aritmética, **ambas** as distribuições valem na lógica: $\land$ distribui sobre $\lor$ **e** $\lor$ distribui sobre $\land$.

> [!question] Pergunta orientadora
> Na aritmética, $a + (b \cdot c)$ NÃO equivale a $(a + b) \cdot (a + c)$ — a soma não distribui sobre a multiplicação. Por que na lógica o "ou" distribui sobre o "e"? Porque os valores lógicos são apenas dois (V/F) e as regras do $\lor$ e do $\land$ são perfeitamente simétricas. Se você duvidar, monte a tabela-verdade das duas expressões com 8 linhas: elas saem idênticas.

A distributividade é a ferramenta de trabalho das **simplificações algébricas** da lógica: ela transforma uma expressão "fechada" em uma soma de produtos (ou produto de somas), o que costuma revelar padrões — como redundâncias que permitem eliminar termos.

### 3.9 Propriedades associativas

As **associatividades** são as mais tranquilas: elas garantem que, em cadeias do **mesmo** conectivo, a posição dos parênteses não altera o resultado.

$$(P \land Q) \land R \equiv P \land (Q \land R)$$

$$(P \lor Q) \lor R \equiv P \lor (Q \lor R)$$

Graças a elas, podemos escrever $P \land Q \land R$ e $P \lor Q \lor R$ sem parênteses, sem medo de ambiguidade — não importa como agrupemos, o valor final é o mesmo. Isso já foi mencionado em [[Estruturas-Logicas#5.6 Argumentos compostos com múltiplos conectivos|Estruturas Lógicas]] sobre associatividade de $\land$ e $\lor$.

> [!warning] A condicional NÃO é associativa — e isso é cobrado
> Enquanto $\land$ e $\lor$ são associativas, a condicional **não** é: $(P \to Q) \to R$ **não** equivale a $P \to (Q \to R)$. Expressões com duas ou mais condicionais **exigem** parênteses; sem eles, a precedência resolve da esquerda para a direita, mas o resultado raramente é o que o candidato intui. Desconfie de qualquer questão que trate condicionais encadeadas como se fossem intercambiáveis.

### 3.10 Outras equivalências úteis (complemento)

A ementa foca em De Morgan, distributivas e associativas, mas quatro equivalências aparecem com frequência como "combustível" das simplificações — vale conhecê-las:

| Nome | Forma | Leitura |
|---|---|---|
| **Dupla negação** | $\neg \neg P \equiv P$ | Negar duas vezes volta ao original |
| **Comutativa** | $P \land Q \equiv Q \land P$ e $P \lor Q \equiv Q \lor P$ | A ordem não importa em $\land$ e $\lor$ |
| **Idempotência** | $P \land P \equiv P$ e $P \lor P \equiv P$ | Repetir a mesma proposição não muda nada |
| **Exportação** | $(P \land Q) \to R \equiv P \to (Q \to R)$ | A condicional "exporta" uma premissa da conjunção para dentro do consequente |

Essas propriedades entram na resolução de questões de duas maneiras: simplificando expressões enormes até uma forma reconhecível, e justificando por que "contar ocorrências de letras" (seção 2.2) é diferente de contar proposições distintas. Note que $P \land P$ tem tabela idêntica a $P$ — por isso $2^1$, e não $2^2$, linhas bastam.

A última lei da tabela — a **exportação** — merece atenção redobrada, pois surge em questões em que as leis mais intuitivas não bastam. Ela afirma:

$$(P \land Q) \to R \;\;\equiv\;\; P \to (Q \to R)$$

**Leia assim:** "se **P e Q**, então R" equivale a "se **P**, então (se **Q**, então R)". A condicional **exporta** uma das premissas da conjunção para dentro do consequente. A volta também é válida — e recebe o nome **importação**:

$$P \to (Q \to R) \;\;\equiv\;\; (P \land Q) \to R$$

> [!question] Pergunta orientadora
> As duas frases realmente dizem a mesma coisa? Veja com um exemplo concreto: P = "João estuda", Q = "João resolve simulados", R = "João passa". $(P \land Q) \to R$ lê-se "se João estuda **e** resolve simulados, então passa"; $P \to (Q \to R)$ lê-se "se João estuda, então (se resolve simulados, então passa)". Qual das duas promete mais? Estruturalmente, nenhuma: são a **mesma** promessa, apenas com as cláusulas rearranjadas. A tabela-verdade (8 linhas) fecha a questão — as colunas finais saem idênticas.

> [!warning] Importante — a exportação NÃO é "associar" condicionais
> Cuidado para não confundir a exportação com a associatividade vista na seção 3.9. Lá ficou avisado que a condicional **não é associativa**: $(P \to Q) \to R$ **não** equivale a $P \to (Q \to R)$ (essa troca é **falsa**). A exportação é coisa totalmente diferente: o antecedente em que ela mexe é uma **conjunção**, $(P \land Q) \to R$, e não um encadeamento de condicionais. Quem troca as duas coisas na prova erra a questão.

> [!example] Exemplo no formato de prova — "qual é equivalente?"
> Questão: qual expressão é equivalente a $(P \land Q) \to R$?
>
> **Resposta:** $P \to (Q \to R)$ — por exportação.
>
> **Raio de pensamento:** quando o antecedente da condicional é uma **conjunção**, a lei permite "mover" uma premissa para dentro do consequente. Na dúvida, o método que a nota já ensina decide: monte a **tabela-verdade** das duas expressões (8 linhas; colunas finais idênticas) — infalível, mesmo sob pressão.

### 3.11 Aplicações: simplificar, transformar e responder "é equivalente a"

Como a banca cobra equivalências? Em três formatos principais, que valem estratégias distintas:

1. **"Qual proposição é equivalente a ...?"** — a alternativa correta pode ser uma contraposição, uma condicional como disjunção, uma aplicação de De Morgan ou uma distributiva. Estratégia: traduza o enunciado para símbolos e, se a resposta não aparecer de imediato, **verifique por tabela-verdade** as alternativas principais — o método nunca falha, mesmo sob pressão.
2. **"Qual é a negação de ...?"** — os casos mais cobrados são: negação da conjunção (De Morgan 1), negação da disjunção (De Morgan 2) e negação da condicional ($P \land \neg Q$). O enunciado costuma vir em linguagem natural: traduza e aplique a lei correspondente.
3. **"Simplifique a expressão ..."** — aplique distributivas, associativas e outras leis em cadeia. Exemplo típico:

> [!example] Simplificação em cadeia
> Simplifique $\neg[(P \land Q) \to R]$ usando as leis estudadas:
>
> $$
> \begin{split}
> \neg[(P \land Q) \to R] &\equiv (P \land Q) \land \neg R \quad \text{(negação da condicional)} \\
> &\equiv P \land Q \land \neg R \quad \text{(associatividade do } \land\text{)}
> \end{split}
> $$
>
> Partimos de uma expressão com condicional e negação e chegamos a uma conjunção simples. Essa habilidade de "destrinchar" expressões é o que diferencia quem acerta questões difíceis de equivalência por simplificação em segundos.

> [!warning] PEGADINHA — ler a expressão sem respeitar a precedência
> Em "$P \lor Q \to R$", pela precedência, o $\lor$ une $P$ e $Q$ primeiro: $(P \lor Q) \to R$. Negar isso resulta em $(P \lor Q) \land \neg R$, e depois De Morgan: $(\neg P \land \neg Q) \land \neg R$. Quem lê como $P \lor (Q \to R)$ obtém outra negação — e erra. Sempre **parênteseie conforme a precedência antes de aplicar qualquer lei**.

> [!tip] Tabela de bolso das equivalências
>
> | Equivalência | Nome |
> |---|---|
> | $\neg(P \land Q) \equiv \neg P \lor \neg Q$ | De Morgan (conjunção) |
> | $\neg(P \lor Q) \equiv \neg P \land \neg Q$ | De Morgan (disjunção) |
> | $\neg(P \to Q) \equiv P \land \neg Q$ | Negação da condicional |
> | $P \to Q \equiv \neg Q \to \neg P$ | Contraposição |
> | $P \to Q \equiv \neg P \lor Q$ | Condicional como disjunção |
> | $P \leftrightarrow Q \equiv (P \to Q) \land (Q \to P)$ | Bicondicional em condicionais |
> | $P \oplus Q \equiv \neg(P \leftrightarrow Q)$ | Exclusiva como negação da bicondicional |
> | $P \land (Q \lor R) \equiv (P \land Q) \lor (P \land R)$ | Distributiva |
> | $P \lor (Q \land R) \equiv (P \lor Q) \land (P \lor R)$ | Distributiva |
> | $(P \land Q) \land R \equiv P \land (Q \land R)$ | Associativa |
> | $(P \lor Q) \lor R \equiv P \lor (Q \lor R)$ | Associativa |
> | $(P \land Q) \to R \equiv P \to (Q \to R)$ | Exportação |
> | $\neg \neg P \equiv P$ | Dupla negação |

---

## 4. Diagramas de Venn para proposições simples

### 4.1 O que são diagramas lógicos

Uma proposição composta pode ser calculada com tabelas; mas certas afirmações do cotidiano — que falam de **categorias** de coisas — são melhor visualizadas com figuras. **Diagramas de Venn** (em homenagem ao matemático John Venn) representam cada categoria como um círculo dentro de um quadro, e as afirmações sobre as categorias como relações entre os círculos: um dentro do outro, separados, ou se tocando.

A ideia central é a de **conjunto**: a categoria "candidatos aprovados" é o conjunto de todos os candidatos aprovados; a categoria "candidatos que estudaram" é outro conjunto. Cada elemento (uma pessoa, um objeto) habita as regiões do diagrama conforme pertence ou não a cada conjunto. Uma **região** do diagrama é uma área delimitada: dentro do círculo A, fora do círculo B, na interseção de A e B, etc. Toda a pergunta "quem está onde?" se responde olhando as regiões.

> [!note] Sobre a formalização (um aviso importante)
> Nesta seção, trabalharemos com as palavras da linguagem natural: **todo**, **nenhum**, **algum**. Vamos entender o que cada uma exige no desenho de forma **intuitiva**. A formalização dessas palavras com símbolos precisos — os **quantificadores** universal e existencial — é o objeto do próximo tópico ([[Logica-de-Primeira-Ordem]]), que você estudará em seguida. Aqui, o objetivo é o raciocínio visual: desenhar, olhar e concluir.

### 4.2 As quatro formas categóricas

As bancas reduzem quase todas as frases com "todo/nenhum/algum" a **quatro formas básicas**. Cada uma tem um desenho característico e uma leitura precisa. Usaremos A e B como duas categorias quaisquer.

**1. "Todo A é B"** — o círculo de A está **totalmente dentro** do círculo de B. Todo elemento de A também é elemento de B (não existe região de A fora de B):

```text
      ┌──────────────────┐
      │        B         │
      │   ┌──────────┐   │
      │   │    A     │   │
      │   └──────────┘   │
      └──────────────────┘
```

**2. "Nenhum A é B"** — os círculos são **disjuntos** (não se tocam). Nenhum elemento de A é elemento de B:

```text
    ┌────────┐        ┌────────┐
    │   A    │        │   B    │
    └────────┘        └────────┘
```

**3. "Algum A é B"** — os círculos **se interceptam**, e a região de interseção **não é vazia** (existe pelo menos um elemento que pertence aos dois ao mesmo tempo):

```text
       ┌───────────┐
       │   A       │
       │    ┌──────┼──────┐
       │    │  ●   │      │
       └────┼──────┘   B  │
            └─────────────┘
```

**4. "Algum A não é B"** — existe **pelo menos um elemento de A que está fora de B**. O desenho é o mesmo do caso 3 (círculos com interseção), mas o que está em destaque é a parte de A **exterior** a B — ela precisa existir:

```text
       ┌───────────┐
       │   A       │
       │ ██ ┌──────┼──────┐
       │    │      │      │
       └────┼──────┘   B  │
            └─────────────┘
```

> [!important] A leitura exata de cada forma (como a banca representa)
> - **"Todo A é B"** = não existe elemento de A fora de B. Na prova, isso é o círculo A **dentro** do círculo B. Pode haver elementos de B fora de A (elementos de B que não são A) — o desenho não diz nada sobre eles.
> - **"Nenhum A é B"** = a interseção de A e B é **vazia**. Círculos totalmente separados.
> - **"Algum A é B"** = a interseção de A e B é **não vazia**. Existe **pelo menos um** elemento comum — um único ponto já basta.
> - **"Algum A não é B"** = existe **pelo menos um** elemento de A fora de B. Basta um; podem existir outros elementos de A dentro de B também.

> [!warning] PEGADINHA — "algum A é B" NÃO significa "somente alguns A são B"
> Na linguagem cotidiana, "algum" às vezes sugere "alguns, mas nem todos". Na lógica (e nas provas), **"algum A é B" significa apenas que existe pelo menos um A que é B** — não exclui a possibilidade de que todos os A sejam B. Se a questão disser apenas "algum A é B", o diagrama correto é "interseção não vazia", que admite tanto a situação "só um ponto na interseção" quanto a situação "A inteiro dentro de B". Simbolicamente, "algum" é um **compromisso mínimo de existência**, nada mais.

### 4.3 O que cada diagrama permite concluir (e o que não permite)

Esta é a parte que decide questões de provas: saber o que uma forma **implica** e o que ela **não autoriza**. Vamos examinar as relações mais cobradas.

**"Todo A é B" e "Algum A é B":**
- Todo A é B **implica** algum A é B, na convenção usual de concurso, que admite as classes com pelo menos um elemento (se existe A, e todo A está em B, então existe pelo menos um A em B).
- O contrário **não vale**: "algum A é B" **não** permite concluir "todo A é B". O desenho da interseção não vazia mostra apenas uma região comum — nada garante que toda a região A esteja dentro de B.
- Consequência clássica: "todo A é B" **não** implica "todo B é A". Simetria não vale: A dentro de B não coloca B dentro de A.

> [!warning] PEGADINHA — concluir "todo" a partir de "algum"
> A banca adora este formato: "Algum servidor é formado em TI. Logo, todo servidor é formado em TI." **Errado.** Para a conclusão valer, seria preciso outra premissa (por exemplo, "todo servidor é formado em TI"). "Algum" afirma um ponto de contato; "todo" exige a inclusão total. **Um diagrama de interseção não vira diagrama de inclusão sem informação nova.**

**"Nenhum A é B" e "Algum A não é B":**
- "Nenhum A é B" (interseção vazia) **implica** "algum A não é B" — se os círculos são separados, todo elemento de A está fora de B, logo existe (pelo menos um) A fora de B.
- O contrário **não vale**: "algum A não é B" admite que **outros** elementos de A estejam dentro de B. O desenho do caso 3/4 tem interseção não vazia — ou seja, permite que haja A em B.
- "Nenhum A é B" **implica** "nenhum B é A" — a relação "nenhum" é **simétrica**, pois o desenho é o mesmo dos dois lados: círculos disjuntos. Isso a distingue da relação "todo", que **não é simétrica** (A dentro de B não coloca B dentro de A).

> [!warning] PEGADINHA — confundir "nenhum" com "algum não é"
> "Nenhum A é B" e "algum A não é B" não são a mesma coisa. "Nenhum" é forte (fecha a interseção inteira); "algum não é" é fraco (exige apenas um elemento de A fora de B, deixando a porta aberta para haver outros A em B). Questões perguntam: "sabendo que algum A não é B, é correto concluir que nenhum A é B?" Resposta: **não** — o diagrama de "algum não é" admite interseção. Para concluir "nenhum", seria preciso a informação adicional de que não existe A em B.

**Relações entre "todo" e "nenhum":**
- "Todo A é B" e "nenhum A é B" são **incompatíveis**: o primeiro desenha A dentro de B; o segundo desenha A separado de B. Não dá para desenhar os dois ao mesmo tempo com o mesmo A e o mesmo B.
- O que **pode** ser desenhado junto: "todo A é B" e "nenhum A é C" (A dentro de B e A longe de C — possível), ou "algum A é B" e "algum A não é B" (a interseção existe e, além dela, há A fora de B — exatamente o desenho do caso 4).

### 4.4 Usando diagramas para validar argumentos

A conexão com a [[Logica-de-Argumentacao]] é direta: um argumento é **dedutivamente válido** quando a conclusão se segue necessariamente das premissas. Com diagramas, o teste é visual:

1. **Desenhe todas as premissas** — cada premissa vira uma imposição sobre as posições dos círculos.
2. **Tente desenhar um diagrama em que TODAS as premissas valham e a conclusão seja falsa.**
3. Se esse diagrama **existe**, o argumento é **inválido** (achamos um contraexemplo). Se **não existe** — qualquer desenho que respeite as premissas obriga a conclusão — o argumento é **válido**.

> [!example] Argumento válido — o contraexemplo é impossível
> **Premissa 1:** Todo A é B. **Premissa 2:** Algum C é A. **Conclusão:** Algum C é B.
>
> Desenhe: A inteiro dentro de B. O elemento de C que está dentro de A (existe, pela premissa 2) está, portanto, dentro de B — ele é o "algum C que é B". Não há como desenhar as premissas sem produzir a conclusão. **Válido.** (Este é o clássico argumento "todo cão é mamífero; Rex é cão; logo Rex é mamífero" em versão diagramática.)

> [!example] Argumento inválido — o contraexemplo existe
> **Premissa 1:** Todo A é B. **Premissa 2:** Algum C é B. **Conclusão:** Algum C é A.
>
> Desenhe: A dentro de B. A premissa 2 diz que há elemento de C em B — mas **não diz em que região de B**. Coloque esse elemento na parte de B que **não** está dentro de A. Todas as premissas valem, e a conclusão é falsa. **Inválido.** É a versão diagramática da pegadinha "afirmação do consequente" (se é B, então é A — falso).

> [!tip] Estratégia de prova para argumentos com diagramas
> Nas questões de múltipla escolha, use uma **busca dirigida pelo contraexemplo**: tente construir o desenho que derruba a conclusão. Se conseguir, a alternativa que diz "a conclusão não decorre das premissas" é a correta. Se o enunciado perguntar "qual conclusão é obrigatória?", desenhe as premissas e procure a região **comum a todas** as variações possíveis — somente o que aparecer em *todos* os desenhos pode ser concluído.

### 4.5 Pegadinhas típicas de diagramas

Reunindo as armadilhas mais frequentes das bancas em questões de diagramas:

> [!warning] PEGADINHA 1 — "algum" é ponto de contato, não inclusão
> De "algum A é B" não se conclui "todo A é B", nem "todo B é A", nem "algum B não é A". O único compromisso é: a interseção não está vazia. Questões que afirmam mais do que isso erram por **excesso de conclusão** — o erro mais comum do tópico.

> [!warning] PEGADINHA 2 — "nenhum" se confunde com "algum não é"
> "Nenhum A é B" é disjunção total; "algum A não é B" é apenas um ponto fora de B. Lembre-se: para concluir "nenhum", precisa-se de mais informação; "algum não é" sozinho deixa a interseção em aberto.

> [!warning] PEGADINHA 3 — "todo" não é simétrico
> "Todo A é B" não equivale a "todo B é A". O primeiro desenha A dentro de B; o segundo, B dentro de A — são desenhos diferentes. Concluir "todo B é A" a partir de "todo A é B" é o erro de **inversão** (recíproca), o mesmo visto nas equivalências (seção 3.4).

> [!warning] PEGADINHA 4 — sobre a existência das classes
> Uma sutileza que divide bancas: na interpretação clássica das proposições categóricas, admite-se que as classes mencionadas **têm elementos** (o círculo de A não é vazio). Nessa leitura, "todo A é B" implica "algum A é B". Em algumas questões de lógica mais "moderna", a classe A pode ser vazia, e a implicação deixa de valer. **Regra prática para RLM de concurso:** na ausência de indicação em contrário, desenhe os círculos como classes existentes (não vazias). Se a questão quiser explorar o caso vazio, ela dirá isso explicitamente — e aí a implicação "todo → algum" não vale.

---

## 5. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] A **tabela-verdade** lista todas as combinações de valores e o resultado da composta em cada uma
> - [ ] Número de linhas = $2^n$, onde $n$ é o número de proposições simples **distintas** (letras diferentes; repetições contam uma vez; conectivos não contam)
> - [ ] Construção: distribuir V/F em padrão alternado → colunas intermediárias na ordem de precedência (¬, depois ∧/∨, depois →, depois ↔) → coluna final
> - [ ] A conjunção só é V com as duas partes V; a disjunção só é F com as duas partes F; a condicional só é F em $V \to F$; o bicondicional só é V com valores iguais; $\oplus$ só é V com valores diferentes
> - [ ] **Tautologia:** coluna final toda V; **contradição:** toda F; **contingência:** tem V e F
> - [ ] $A \equiv B$ quando as tabelas são idênticas linha a linha (ou $A \leftrightarrow B$ é tautologia)
> - [ ] **De Morgan:** $\neg(P \land Q) \equiv \neg P \lor \neg Q$ e $\neg(P \lor Q) \equiv \neg P \land \neg Q$ — negar a conjunção **não** é $\neg P \land \neg Q$
> - [ ] **Negação da condicional:** $\neg(P \to Q) \equiv P \land \neg Q$ — negação de "se...então" é uma conjunção, não outra condicional
> - [ ] **Contraposição:** $P \to Q \equiv \neg Q \to \neg P$ — distinta da recíproca ($Q \to P$) e da inversa ($\neg P \to \neg Q$)
> - [ ] **Condicional como disjunção:** $P \to Q \equiv \neg P \lor Q$
> - [ ] **Bicondicional:** $P \leftrightarrow Q \equiv (P \to Q) \land (Q \to P)$ e $P \oplus Q \equiv \neg(P \leftrightarrow Q)$
> - [ ] **Distributivas:** $P \land (Q \lor R) \equiv (P \land Q) \lor (P \land R)$ e $P \lor (Q \land R) \equiv (P \lor Q) \land (P \lor R)$
> - [ ] **Associativas:** $(P \land Q) \land R \equiv P \land (Q \land R)$ e o mesmo para $\lor$ — a condicional **não** é associativa
> - [ ] **Exportação:** $(P \land Q) \to R \equiv P \to (Q \to R)$ — quando o antecedente é conjunção, uma premissa pode ir para dentro do consequente (e a volta vale: **importação**)
> - [ ] Diagramas: **todo** = círculo dentro; **nenhum** = círculos separados; **algum** = interseção não vazia; **algum não é** = existe parte de A fora de B
> - [ ] "Algum A é B" **não** autoriza "todo A é B"; "algum A não é B" **não** autoriza "nenhum A é B"; "todo A é B" **não** autoriza "todo B é A"
> - [ ] Argumento válido por diagramas = impossível desenhar as premissas com a conclusão falsa

> [!warning] O erro mais comum em prova
> **Negar a condicional como se fosse outra condicional** ($\neg P \to \neg Q$) em vez de $P \land \neg Q$, e **negar a conjunção como se fosse $\neg P \land \neg Q$** em vez de $\neg P \lor \neg Q$. Os dois erros aparecem lado a lado nas alternativas — e ambos são derrubados por uma pergunta simples: *"em qual linha exata a expressão original é falsa?"* A negação é verdadeira exatamente nessa linha.

---

## 6. Próximos passos

Este tópico fechou a caixa de ferramentas da lógica de proposições: calcular valores (tabelas-verdade), comparar proposições (equivalências) e raciocinar sobre categorias (diagramas). Os próximos tópicos deste bloco expandem o que foi iniciado aqui:

- [[Logica-de-Primeira-Ordem]] — a formalização dos quantificadores que usamos intuitivamente nos diagramas ("todo", "algum", "nenhum"), com predicados e variáveis, e a negação correta de proposições quantificadas
- [[Raciocinio-Matematico-Aplicado]] — problemas aritméticos (porcentagem, regra de três, juros), geométricos, matriciais e progressões

Você não precisa de nenhum deles para o que estudou agora — mas a lógica sentencial é o alicerce dos dois. Quando o próximo tópico introduzir $\forall$ e $\exists$, você reconhecerá, por trás dos símbolos novos, exatamente os diagramas que desenhou aqui. E quando o raciocínio matemático trouxer problemas de contagem e proporção, será a mesma habilidade de traduzir um enunciado em estrutura lógica que você vem treinando desde a primeira nota.