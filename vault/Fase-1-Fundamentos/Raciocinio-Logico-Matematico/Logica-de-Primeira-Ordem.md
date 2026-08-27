# Lógica de Primeira Ordem

> [!info] Metadados
> **Disciplina:** Raciocínio Lógico Matemático
> **Bloco:** 1.2 — Raciocínio Lógico Matemático (FASE 1 — Fundamentos)
> **Tópico:** 4. Lógica de primeira ordem
> **Subtópicos:** Quantificadores (universal e existencial) · Predicados e variáveis · Negação de quantificadores
> **Pré-requisitos:** [[Estruturas-Logicas]], [[Logica-de-Argumentacao]] e [[Logica-Sentencial]]
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-27

---

## 1. Por que estudar lógica de primeira ordem?

Nas notas anteriores, construímos uma peça de engenharia impressionante. Na [[Estruturas-Logicas]], aprendemos o que é uma proposição e como os conectivos ($\neg$, $\land$, $\lor$, $\to$, $\leftrightarrow$) combinam proposições. Na [[Logica-Sentencial]], ganhamos a *máquina de calcular*: as tabelas-verdade calculam o valor de verdade de qualquer combinação, e as equivalências nos deixam trocar uma expressão por outra sem mudar resultado nenhum.

Mas repare em um limite dessa máquina: ela trata cada proposição como um **bloco fechado**. $P$ é $P$; $Q$ é $Q$; a máquina combina blocos e pronto. Ela nunca pergunta o que há **dentro** de cada bloco.

Agora tente resolver este argumento usando apenas blocos:

> **Premissa 1:** Todo servidor da DATAPREV fez o curso de capacitação.
> **Premissa 2:** Ana é servidora da DATAPREV.
> **Conclusão:** Ana fez o curso de capacitação.

O argumento é claramente válido — é o mesmo padrão "todo $A$ é $B$; $x$ é $A$; logo $x$ é $B$" que você viu na dedução em [[Logica-de-Argumentacao]]. Mas a lógica sentencial não consegue provar isso. Para representar a premissa 1 com blocos, teríamos de engolir a frase inteira como um único $P$ — e aí a premissa 2 não conversa com ela. A validade do argumento depende do **conteúdo interno** das proposições: existe um sujeito ("servidor da DATAPREV") e um predicado ("fez o curso"), e existe uma palavra mágica — "**todo**" — que percorre os indivíduos um a um.

A **lógica de primeira ordem** (também chamada **lógica de predicados** ou **cálculo de predicados**) é a ampliação da lógica que abre a proposição e olha para dentro. Ela dá nomes para as partes (sujeito, predicado) e símbolos precisos para as "palavras de quantidade": **todo**, **algum**, **nenhum**, **ninguém**.

Nas notas anteriores, essa promessa ficou explicitamente registrada. Na [[Estruturas-Logicas]], a seção *Variável livre vs. quantificada* avisou que aquele contraste entre "$x > 5$" (variável solta) e "$\exists x\,(x > 5)$" (variável presa) era a porta de entrada para este tópico — e que aqui formalizaríamos exatamente como "alguém", "ninguém", "todos" e "nenhum" se traduzem em símbolos. Na [[Logica-Sentencial]], a seção de diagramas de Venn também adiou a formalização: dissemos que "todo/nenhum/algum" seriam escritos com $\forall$ e $\exists$ no próximo tópico, e a notação foi deliberadamente evitada lá. Pois bem: **este é o momento.** Vamos pagar as duas promessas.

> [!tip] Relevância para o Analista de TI
> Regras de negócio e validações de sistema são quantificadores disfarçados:
> - "**Todo** registro deve ter chave primária" é uma afirmação universal ($\forall$): ela cai por terra no instante em que **existe** um registro sem chave (um contraexemplo, $\exists$).
> - "**Nenhum** usuário pode acessar um dado sem permissão" é a negação de uma existência: violá-la é encontrar **um** caso de acesso indevido.
> - Em consultas e testes, a pergunta "todos os itens passaram na validação?" ($\forall$) é respondida procurando "existe item que não passou?" ($\exists$). Quem confunde os dois escreve a validação errada — e o teste passa quando deveria falhar.

---

## 2. Predicados e variáveis

### 2.1 Proposição aberta × proposição fechada

Na [[Estruturas-Logicas]], estabelecemos uma regra dura: proposição é todo enunciado com valor de verdade definido. E vimos o caso estranho de "$x > 5$": para $x = 1$ é falsa, para $x = 7$ é verdadeira — o valor **depende** de $x$. Esse tipo de expressão recebe agora um nome: **proposição aberta** (ou **sentença aberta**, ou **função proposicional**). Ela é aberta porque contém uma "lacuna" — a variável — que ainda não foi preenchida.

O que preenche a lacuna? Duas coisas, e apenas duas:

1. **Substituir a variável por um indivíduo concreto** (uma **constante**): "$3 > 5$" é F; "$7 > 5$" é V. A proposição **fechou**.
2. **Prender a variável com um quantificador**: "$\exists x\,(x > 5)$" e "$\forall x\,(x > 5)$" não mencionam nenhum indivíduo em particular, mas mesmo assim têm valor definido. A proposição **fechou** do mesmo jeito.

O nome das partes, agora: em "$x$ é servidor da DATAPREV", chamamos de **predicado** a parte que se afirma sobre o sujeito — "é servidor da DATAPREV". O **sujeito** é a variável $x$ (ou uma constante, como "Ana"). Representamos o predicado com uma letra maiúscula seguida de parênteses:

$$S(x) = \text{"}x\text{ é servidor da DATAPREV"}$$

> [!note] Convenção de notação desta nota
> Para não confundir com as variáveis proposicionais das notas anteriores ($P$, $Q$, $R$ maiúsculas, representando proposições inteiras), usaremos **predicados** com letras como $A(x)$, $B(x)$, $S(x)$, $T(x)$. Em regras gerais, escrevemos $P(x)$ para significar "um predicado qualquer aplicado a $x$" — o contexto deixará claro.

O predicado funciona como uma **função**: ele recebe um indivíduo e devolve uma proposição. Pense em $P(x) =$ "$x$ é par":

| Entrada (indivíduo) | Saída (proposição) | Valor |
|---|---|---|
| $x = 4$ | $P(4)$: "4 é par" | V |
| $x = 3$ | $P(3)$: "3 é par" | F |
| $x = 8$ | $P(8)$: "8 é par" | V |

Assim como uma função matemática $f(x) = 2x$ devolve um número para cada $x$, o predicado devolve uma **proposição** para cada $x$. Por isso o nome *função proposicional*.

> [!warning] PEGADINHA — "P(x) é proposição?"
> A banca pergunta: *"A expressão $P(x)$ é uma proposição?"* **Não.** Sem constante e sem quantificador, $P(x)$ é uma proposição aberta — não tem valor de verdade, porque $x$ está solto. Ela vira proposição apenas com quantificador ($\forall x\,P(x)$ ou $\exists x\,P(x)$) ou com constante ($P(\text{ana})$). É exatamente o contraste "$x > 5$" vs "$\exists x\,(x > 5)$" que estudamos em [[Estruturas-Logicas]].

### 2.2 Variável livre × variável ligada — a retomada prometida

A [[Estruturas-Logicas]] deixou registrado o contraste com uma tabela que vale reprisar:

| Expressão | Classificação | Por quê? |
|---|---|---|
| $x > 5$ | ❌ **Não é proposição** | $x$ está **livre** (solto) — o valor muda conforme $x$ |
| $\exists x\,(x > 5)$ | ✅ **É proposição** | $\exists$ **prende** $x$ — "existe pelo menos um valor que satisfaz" |
| $\forall x\,(x > 5)$ | ✅ **É proposição** | $\forall$ **prende** $x$ — "para todo valor, a condição vale" |

A terminologia técnica que faltava: uma variável **livre** é aquela que não está sob o comando de nenhum quantificador; uma variável **ligada** (ou **amarrada**) é aquela que está no escopo de um $\forall$ ou $\exists$. Ligue-se ao macete da nota anterior: **variável solta = porta aberta = não é proposição; quantificador = trava = é proposição.**

### 2.3 Domínio do discurso (universo)

Quando dizemos "para todo $x$" ou "existe $x$", de onde $x$ pode ser escolhido? A resposta é o **domínio do discurso** (também chamado **universo do discurso**): o conjunto de indivíduos sobre os quais as variáveis podem variar. Pode ser "todas as pessoas", "os servidores da DATAPREV", "os números inteiros", "os registros do banco de dados" — o que o enunciado estabelecer.

E aqui mora uma pegadinha silenciosa: **mudar o domínio muda o valor de verdade.**

> [!example] O mesmo símbolo, outro domínio
> Tome a fórmula $\forall x\,(\text{"}x\text{ é par"})$:
> - No domínio dos **números inteiros**: **F** — 3 é ímpar, contraexemplo.
> - No domínio $\{2, 4, 6\}$: **V** — todos os elementos do domínio são pares.
>
> Nenhum símbolo mudou: mesma fórmula, mesmo predicado. Mudou apenas o **domínio** — e o valor de verdade virou de F para V. Por isso, em prova, preste atenção no universo anunciado no enunciado. Quando a banca não diz nada, costuma valer a leitura natural da frase (pessoas, números, etc.).

### 2.4 Predicados com múltiplos lugares: relações

Nem todo predicado fala de um único indivíduo. Quando o predicado recebe **dois** argumentos, ele expressa uma **relação** entre dois objetos:

$$P(x, y) = \text{"}x\text{ é servidor de }y\text{"}$$

Exemplo: $P(\text{Ana}, \text{DATAPREV})$ é a proposição "Ana é servidora da DATAPREV".

A ordem dos argumentos importa! $P(\text{Ana}, \text{DATAPREV})$ não é o mesmo que $P(\text{DATAPREV}, \text{Ana})$. Para o Analista de TI, isso é o dia a dia da autorização:

$$Permissao(U, R) = \text{"o usuário }U\text{ tem permissão de acesso ao recurso }R\text{"}$$

$Permissao(\text{joao}, \text{/api/dados})$ é uma permissão verdadeira ou falsa — um booleano, exatamente como o que um método de um sistema de autorização retorna. Note que dá para fazer a mesma pergunta com **variáveis** e depois prender cada uma com um quantificador — por exemplo, $\exists U\,Permissao(U, \text{/api/dados})$ pergunta "existe usuário com permissão nesse recurso?" (em SQL, um `WHERE EXISTS`). Esse é o salto de qualidade da lógica de primeira ordem: a proposição sentencial dizia *o que* acontece; agora podemos dizer *sobre quantos* e *para qual* indivíduo acontece.

---

## 3. Quantificadores

### 3.1 Quantificador universal ($\forall$)

O **quantificador universal** $\forall$ é lido "**para todo**", "**para qualquer**", "**todos**", "**cada**", "**qualquer que seja**". A fórmula

$$\forall x\,P(x)$$

afirma que **todos** os indivíduos do domínio satisfazem o predicado $P$. É uma proposição **falsa se existir ao menos um** indivíduo do domínio que não satisfaz — esse indivíduo é o **contraexemplo**.

> [!question] Pergunta orientadora
> Quantos contraexemplos são necessários para derrubar um $\forall$? Um só. "Todo registro tem chave primária" cai no momento em que encontramos **um** registro sem chave. Para testes de software, essa é a lógica do caso de teste negativo: uma única entrada inválida desmente a regra universal.

Na [[Logica-Sentencial]], vimos a tabela da condicional: a condicional só é falsa em $V \to F$. Esse detalhe voltará com força total na seção 3.5 — o $\forall$ costuma andar de mãos dadas com o $\to$.

### 3.2 Quantificador existencial ($\exists$)

O **quantificador existencial** $\exists$ é lido "**existe**", "**existe pelo menos um**", "**há um**", "**algum**". A fórmula

$$\exists x\,P(x)$$

afirma que **pelo menos um** indivíduo do domínio satisfaz o predicado. Basta um — um único elemento já torna a sentença verdadeira.

> [!example] Dois quantificadores, um só domínio
> Sobre o domínio "habitantes do Brasil":
> - "Alguém é brasileiro" = $\exists x\,Brasileiro(x)$ — **V** (basta um; na verdade, milhões).
> - "Todos são brasileiros" = $\forall x\,Brasileiro(x)$ — **V** (o domínio inteiro é de brasileiros).
>
> Troque o domínio para "habitantes de Tóquio": a existencial continua verdadeira apenas se houver brasileiro em Tóquio; a universal quase certamente vira **F**. Mesma fórmula, domínio diferente, resposta diferente — a pegadinha da seção 2.3 em ação.

### 3.3 Leitura e escrita: o vocabulário da banca

A banca quase nunca escreve $\forall$ e $\exists$; ela disfarça com palavras. O quadro de tradução:

| Palavra na frase | Quantificador |
|---|---|
| para todo, todo, todos, toda, todas, cada, qualquer, qualquer que seja, sempre | $\forall$ |
| existe, existe pelo menos um, há, algum, alguns, alguém, pelo menos um, em geral | $\exists$ |

> [!warning] PEGADINHA — "cada" é universal
> "Cada usuário deve ter um perfil" soa específico, mas é **universal**: vale para *todos* os usuários, um a um. $\forall x\,(Usuario(x) \to TemPerfil(x))$. Cuidado também com "**um**" no sentido de "qualquer um" ("um sistema que falha é inaceitável" = universal disfarçado) em vez de "pelo menos um" (existencial). O contexto decide.

### 3.4 As quatro formas categóricas: a ponte com os diagramas de Venn

Na [[Logica-Sentencial]], você desenhou os diagramas: "todo $A$ é $B$" é o **círculo $A$ dentro do círculo $B$**; "nenhum $A$ é $B$" são **círculos separados**; "algum $A$ é $B$" é **interseção não vazia**; "algum $A$ não é $B$" é **existir parte de $A$ fora de $B$**. Ficou prometido que a formalização viria aqui. Pois ela vem agora — traduzindo cada desenho para a notação de predicados e quantificadores:

| Forma da linguagem natural | Notação formal | Leitura em palavras | Desenho (estudado em [[Logica-Sentencial]]) |
|---|---|---|---|
| **Todo $A$ é $B$** | $\forall x\,(A(x) \to B(x))$ | "para todo $x$, **se** $x$ é $A$, **então** $x$ é $B$" | $A \subseteq B$ — círculo $A$ dentro do círculo $B$ |
| **Nenhum $A$ é $B$** | $\forall x\,(A(x) \to \neg B(x))$ (equivale a $\neg\exists x\,(A(x) \land B(x))$) | "para todo $x$, se é $A$, então **não** é $B$" | $A \cap B = \varnothing$ — círculos disjuntos |
| **Algum $A$ é $B$** | $\exists x\,(A(x) \land B(x))$ | "existe $x$ que **é** $A$ **e** é $B$" | $A \cap B \neq \varnothing$ — interseção não vazia |
| **Algum $A$ não é $B$** | $\exists x\,(A(x) \land \neg B(x))$ | "existe $x$ que é $A$ **e não** é $B$" | existe elemento de $A$ fora de $B$ |

Repare como os desenhos "viraram escrita":
- **A dentro de B** = não existe $A$ fora de $B$, ou seja, todo $A$ implica $B$: $\forall x\,(A(x) \to B(x))$.
- **Círculos disjuntos** = nada é $A$ e $B$ ao mesmo tempo: $\neg\exists x\,(A(x) \land B(x))$ — que, como veremos na seção 4, pode ser "reescrito" como $\forall x\,(A(x) \to \neg B(x))$.
- **Interseção com pelo menos um ponto** = $\exists x\,(A(x) \land B(x))$; o ponto na parte de $A$ fora de $B$ = $\exists x\,(A(x) \land \neg B(x))$.

> [!important] "Todo $A$ é $B$" equivale a "todo não-$B$ é não-$A$" — e **não** a "todo $B$ é $A$"
> Ponto a ponto, cada elemento obedece à contraposição estudada em [[Logica-Sentencial]]: $A(x) \to B(x) \equiv \neg B(x) \to \neg A(x)$. Logo, $\forall x\,(A(x) \to B(x)) \equiv \forall x\,(\neg B(x) \to \neg A(x))$ — "quem não é $B$ não é $A$". A recíproca $\forall x\,(B(x) \to A(x))$ ("todo $B$ é $A$") **não** é equivalente: o círculo $A$ dentro de $B$ não coloca $B$ dentro de $A$. A pegadinha da simetria do "todo" é a mesma da recíproca da condicional — e a escrita com $\to$ deixa isso explícito.

### 3.5 ATENÇÃO TÉCNICA — por que "todo" usa $\to$ e "algum" usa $\land$

Este é o ponto mais cobrado do tópico e a fonte do erro clássico. Por que "todo $A$ é $B$" escrevemos com condicional e "algum $A$ é $B$" com conjunção? Porque **trocar é um desastre lógico**. Vamos ver os dois desastres:

**Desastre 1 — "Todo $A$ é $B$" escrito como $\forall x\,(A(x) \land B(x))$:**

Leia em voz alta: "para todo $x$, $x$ é $A$ **e** $x$ é $B$". Isso afirma que **tudo no domínio é $A$** — porque o $x$ percorre o domínio inteiro. Se o domínio são as pessoas e $A$ = "servidor", a fórmula diz "toda pessoa é servidora **e** fez o curso". Mas a frase "todo servidor fez o curso" **não fala nada sobre quem não é servidor** — ela só restringe os que são servidores. A condicional resolve: "para todo $x$, **se** $x$ é servidor, **então** $x$ fez o curso". Para quem não é servidor, a condicional é verdadeira por vacuidade (o antecedente é F) — exatamente como a "promessa" de [[Estruturas-Logicas]]: "se chover, levarei guarda-chuva" não se quebra quando não chove. A forma com $\land$ seria **forte demais**.

**Desastre 2 — "Algum $A$ é $B$" escrito como $\exists x\,(A(x) \to B(x))$:**

Leia: "existe $x$ tal que, **se** $x$ é $A$, **então** $x$ é $B$". O problema: se no domínio houver **um único** indivíduo que não é $A$ (uma cadeira, um gato, um não candidato), para esse indivíduo a condicional é verdadeira por vacuidade — antecedente falso. Logo, a fórmula $\exists x\,(A(x) \to B(x))$ é verdadeira em quase **qualquer** domínio, mesmo que **nenhum** $A$ seja $B$! Ela seria **fraca demais** — diz qualquer coisa. O $\exists$ precisa de existência concreta, e por isso exige $\land$: $\exists x\,(A(x) \land B(x))$ = "existe um indivíduo que é $A$ **e** é $B$ de verdade".

> [!tip] Regra de ouro para a prova
> **$\forall$ casa com $\to$; $\exists$ casa com $\land$.** Se a alternativa apresentar $\forall x\,(A(x) \land B(x))$ para "todo $A$ é $B$", descarte — é forte demais. Se apresentar $\exists x\,(A(x) \to B(x))$ para "algum $A$ é $B$", descarte — é fraca demais e quase sempre verdadeira.

**E a existência das classes?** Uma consequência dessa escolha: $\forall x\,(A(x) \to B(x))$ **não exige que exista $A$**. Se não existe nenhum $A$ no domínio, a universal é verdadeira por vacuidade. Já $\exists x\,(A(x) \land B(x))$ **exige** existência. Na convenção de concurso (classes não vazias, como alertamos nos diagramas de [[Logica-Sentencial]]), "todo $A$ é $B$" implica "algum $A$ é $B$" — mas é bom saber que isso é uma convenção, não uma necessidade lógica pura.

> [!question] Prelúdio da negação
> Antes de seguirmos, faça o exercício: negar "todo $A$ é $B$" é escrever "nenhum $A$ é $B$"? Pense no desenho. "Todo $A$ é $B$" é $A$ dentro de $B$; sua negação deve desenhar um cenário que **quebra** essa inclusão. Um único elemento de $A$ fora de $B$ já quebra — ou seja, a negação de "todo" é "**algum $A$ não é $B$**", não "nenhum $A$ é $B$". Repare que negar "todo" não é negar o predicado — é trocar o quantificador e negar o conteúdo. Essa é exatamente a regra que formalizaremos na seção 4.

### 3.6 Um quantificador extra: existência única ($\exists!$) — leitura opcional

Existe ainda o quantificador de **existência única** $\exists!$: "existe **exatamente um**". A fórmula

$$\exists!x\,P(x)$$

afirma que há um único indivíduo satisfazendo $P$. Formalmente, é o existencial acompanhado da unicidade: existe um $x$ que satisfaz **e** qualquer outro que satisfaça é o próprio $x$:

$$\exists x\,\bigl(P(x) \land \forall y\,(P(y) \to y = x)\bigr)$$

É menos cobrado em concurso, mas aparece em frases como "existe **um único** responsável pelo sistema". Se aparecer, lembre: **existência + unicidade** — são duas exigências.

---

## 4. Negação de quantificadores

### 4.1 As duas regras-mãe

Se a [[Logica-Sentencial]] nos deu De Morgan e a negação da condicional, a lógica de primeira ordem acrescenta **duas regras-mãe** — as únicas de que você precisa para negar qualquer proposição quantificada:

$$\neg\forall x\,P(x) \equiv \exists x\,\neg P(x)$$

$$\neg\exists x\,P(x) \equiv \forall x\,\neg P(x)$$

Leia a primeira em português: negar "**todos** satisfazem $P$" equivale a "**existe pelo menos um** que **não** satisfaz $P$". "Não é verdade que todos passaram" = "pelo menos um não passou". **Não** é "todos não passaram"!

Leia a segunda: negar "**existe** $x$ que satisfaz $P$" equivale a "**nenhum** $x$ satisfaz $P$", isto é, "para todo $x$, **não** $P$". "Não existe erro no sistema" = "todo passo está correto" (nenhum erro).

> [!tip] O macete do coringa troca
> Para negar uma proposição quantificada, execute **sempre os DOIS passos**:
> 1. **Troque o quantificador**: $\forall$ vira $\exists$; $\exists$ vira $\forall$.
> 2. **Negue o predicado** (o conteúdo que estava no escopo).
>
> A pegadinha clássica é fazer **só um** dos dois passos — trocar o quantificador e deixar o predicado intacto ($\neg\forall x\,P(x) = \exists x\,P(x)$, absurdo: negar "todos" não me dá "existe" simples), ou negar o predicado sem trocar o quantificador ($\neg\forall x\,P(x) = \forall x\,\neg P(x)$, que, em vez da correta "pelo menos um não passou", entrega "todos não passaram" = "ninguém passou" — forte demais). Só os dois juntos fecham a conta.

```text
Negar uma proposição quantificada
        │
        ▼
Passo 1 — Trocar o quantificador: ∀ vira ∃, ∃ vira ∀
        │
        ▼
Passo 2 — Negar o predicado (o conteúdo do escopo)
        │
        ▼
Passo 3 — Se houver conectivos dentro do escopo,
          aplicar as leis sentenciais já estudadas
          (De Morgan, negação da condicional, dupla negação)
        │
        ▼
   Proposição negada corretamente
```

### 4.2 Aplicação às quatro formas categóricas

Combinando as regras-mãe com as equivalências de [[Logica-Sentencial]], obtemos as negações das quatro formas categóricas. Repare como cada passo usa o que você já sabe — a negação da condicional, De Morgan, a condicional como disjunção:

**1. Negação de "Todo $A$ é $B$":**

$$
\begin{split}
\neg\forall x\,(A(x) \to B(x)) &\equiv \exists x\,\neg(A(x) \to B(x)) \\
&\equiv \exists x\,(A(x) \land \neg B(x)) \quad \text{(negação da condicional)}
\end{split}
$$

Ou seja: negação de "todo $A$ é $B$" = "**algum $A$ não é $B$**".

**2. Negação de "Nenhum $A$ é $B$":**

$$
\begin{split}
\neg\forall x\,(A(x) \to \neg B(x)) &\equiv \exists x\,\neg(A(x) \to \neg B(x)) \\
&\equiv \exists x\,(A(x) \land \neg\neg B(x)) \\
&\equiv \exists x\,(A(x) \land B(x)) \quad \text{(dupla negação)}
\end{split}
$$

Ou seja: negação de "nenhum $A$ é $B$" = "**algum $A$ é $B$**".

**3. Negação de "Algum $A$ é $B$":**

$$
\begin{split}
\neg\exists x\,(A(x) \land B(x)) &\equiv \forall x\,\neg(A(x) \land B(x)) \\
&\equiv \forall x\,(\neg A(x) \lor \neg B(x)) \quad \text{(De Morgan)} \\
&\equiv \forall x\,(A(x) \to \neg B(x)) \quad \text{(condicional como disjunção)}
\end{split}
$$

Ou seja: negação de "algum $A$ é $B$" = "**nenhum $A$ é $B$**".

**4. Negação de "Algum $A$ não é $B$":**

$$
\begin{split}
\neg\exists x\,(A(x) \land \neg B(x)) &\equiv \forall x\,\neg(A(x) \land \neg B(x)) \\
&\equiv \forall x\,(\neg A(x) \lor B(x)) \quad \text{(De Morgan)} \\
&\equiv \forall x\,(A(x) \to B(x)) \quad \text{(condicional como disjunção)}
\end{split}
$$

Ou seja: negação de "algum $A$ não é $B$" = "**todo $A$ é $B$**".

A tabela de bolso — decore a frase e a notação juntas:

| Proposição | Notação | **Negação correta** | Notação da negação |
|---|---|---|---|
| Todo $A$ é $B$ | $\forall x\,(A(x) \to B(x))$ | **Algum $A$ não é $B$** | $\exists x\,(A(x) \land \neg B(x))$ |
| Nenhum $A$ é $B$ | $\forall x\,(A(x) \to \neg B(x))$ | **Algum $A$ é $B$** | $\exists x\,(A(x) \land B(x))$ |
| Algum $A$ é $B$ | $\exists x\,(A(x) \land B(x))$ | **Nenhum $A$ é $B$** | $\forall x\,(A(x) \to \neg B(x))$ |
| Algum $A$ não é $B$ | $\exists x\,(A(x) \land \neg B(x))$ | **Todo $A$ é $B$** | $\forall x\,(A(x) \to B(x))$ |

Observe o padrão circular: cada negação "gira" a forma para a próxima posição do quadrado. Negar duas vezes volta ao original (a dupla negação de [[Logica-Sentencial]] de novo): a negação de "algum $A$ não é $B$" é "todo $A$ é $B$". Esse giro é o seu mapa mental — na dúvida, ande uma casa no quadrado.

> [!warning] PEGADINHA — "nenhum $A$ é $B$" ≠ "algum $A$ não é $B$"
> Eles parecem gêmeos, mas não são. "Nenhum $A$ é $B$" fecha a interseção inteira (círculos disjuntos, $\forall x\,(A(x) \to \neg B(x))$). "Algum $A$ não é $B$" exige apenas **um** $A$ fora de $B$, admitindo que outros $A$ estejam dentro de $B$ (interseção permitida). E cuidado com a armadilha da dupla negação embutida: "**nenhum $A$ não é $B$**" = "nenhum $A$ é tal que não é $B$" = "todo $A$ é $B$" ($\forall x\,(A(x) \to \neg\neg B(x)) \equiv \forall x\,(A(x) \to B(x))$). Duas negações em "nenhum/não" se cancelam.

### 4.3 "Alguém", "ninguém", "todos", "nenhum": formalizar e negar (ponte 1)

Aqui está o acerto de contas com a [[Estruturas-Logicas]]. Naquela nota, a Família 2 dos pronomes quantificacionais ficou assim resumida — agora com as formalizações completas:

| Pronome | Formalização | Exemplo | Negação correta | Notação da negação |
|---|---|---|---|---|
| **alguém** | $\exists x\,T(x)$ | "Alguém telefonou" | "Ninguém telefonou" | $\neg\exists x\,T(x) \equiv \forall x\,\neg T(x)$ |
| **ninguém** | $\neg\exists x\,C(x) \equiv \forall x\,\neg C(x)$ | "Ninguém compareceu" | "Alguém compareceu" | $\exists x\,C(x)$ (dupla negação) |
| **todos** | $\forall x\,P(x)$ | "Todos passaram" | "Nem todos passaram" (= "alguém não passou") | $\exists x\,\neg P(x)$ |
| **nenhum** | $\neg\exists x\,F(x) \equiv \forall x\,\neg F(x)$ | "Nenhum faltou" | "Alguém faltou" | $\exists x\,F(x)$ |

Três observações que caem em prova:

1. **"Ninguém" e "nenhum" são a negação do "existe".** "Ninguém compareceu" = $\neg\exists x\,C(x)$, que reescrevemos como $\forall x\,\neg C(x)$ ("para todo o mundo, não compareceu"). São duas notações para a mesma proposição — a banca pode usar qualquer uma.
2. **Negar "ninguém" devolve "alguém".** $\neg\neg\exists x\,C(x) \equiv \exists x\,C(x)$. Como diz o macete, o coringa troca $\exists$ por $\forall$ e nega o predicado — mas aqui o outro $\neg$ "espera" do lado de fora, e a dupla negação se cancela.
3. **"Nem todos" ≠ "ninguém".** Já vimos a pegadinha do "nem" em [[Estruturas-Logicas]]: "nem todos passaram" = $\neg\forall x\,P(x) \equiv \exists x\,\neg P(x)$ = "pelo menos um não passou". Isso **não** equivale a "ninguém passou" ($\forall x\,\neg P(x)$), que é muito mais forte. "Nem todos" admite que muitos tenham passado — basta sobrar um.

> [!warning] PEGADINHA — "algum" não exclui "todo"
> Na lógica, "algum $A$ é $B$" significa apenas "pelo menos um $A$ é $B$". **Não** exclui a possibilidade de todos serem. A negação de "todo" é "algum **não**" — e esse "algum não" inclui até o caso extremo "nenhum". A banca adora oferecer "ninguém/nem todos" como alternativa para a negação de "todos": a correta é "**pelo menos um não**".

### 4.4 Negação de cadeias com múltiplos quantificadores

Quando há vários quantificadores, a regra é aplicar o coringa **da esquerda para a direita**, um quantificador de cada vez, trocando e negando ao final:

$$\neg\forall x\,\exists y\,P(x, y) \equiv \exists x\,\neg\exists y\,P(x, y) \equiv \exists x\,\forall y\,\neg P(x, y)$$

Em etapas: nega-se o $\forall x$ (vira $\exists x$), depois "desce" o $\neg$ para o interior e nega-se o $\exists y$ (vira $\forall y$), e o $\neg$ final atinge o predicado. O processo é mecânico: **troca, troca, nega o conteúdo**.

> [!example] Negação em cadeia com sabor de sistema
> Regra de negócio: "Para **todo** arquivo, **existe** um usuário com permissão de leitura."
>
> $\forall x\,\exists y\,Permissao(y, x)$ — onde $x$ é arquivo e $y$ é usuário.
>
> Negação: "**Existe** um arquivo tal que **nenhum** usuário tem permissão de leitura."
>
> $\exists x\,\forall y\,\neg Permissao(y, x)$.
>
> Para derrubar a regra universal, você precisa encontrar **um** arquivo abandonado — sem um único leitor autorizado. Um arquivo com ao menos um usuário autorizado não derruba nada.

---

## 5. Escopo, encadeamento e ordem dos quantificadores

### 5.1 Escopo do quantificador

O **escopo** de um quantificador é a parte da fórmula que ele "comanda". Compare:

$$\forall x\,P(x) \land Q(x)$$

Nessa expressão, o $\forall x$ comanda apenas $P(x)$ — o $x$ que aparece em $Q(x)$ está **fora do escopo** e é, portanto, uma **variável livre**. A fórmula inteira está aberta: não é proposição até que algo faça algo com aquele $x$ solto. Para que o quantificador comande os dois, é preciso **parênteses**:

$$\forall x\,\bigl(P(x) \land Q(x)\bigr)$$

Agora sim, ambas as ocorrências de $x$ estão ligadas. A lição: **o escopo se estende até o fim do parêntese** (ou até o fim da fórmula, se não houver parênteses). Esse é o retorno da pegadinha da variável livre em versão avançada — a banca escreve $\forall x\,P(x) \land Q(x)$ e pergunta se é proposição. A resposta é **não** (ou "depende de interpretação") enquanto $Q(x)$ tiver $x$ solto; com os parênteses, vira proposição.

### 5.2 A ordem importa: $\forall x\,\exists y$ ≠ $\exists y\,\forall x$

Com quantificadores de **tipos diferentes**, a ordem **altera o significado**. Compare as duas fórmulas sobre o domínio "pessoas", com $R(x, y)$ = "$x$ ama $y$":

| Fórmula | Leitura | Exemplo concreto | Exige o quê? |
|---|---|---|---|
| $\forall x\,\exists y\,R(x, y)$ | "para todo $x$, existe um $y$ tal que $x$ ama $y$" | "Todo mundo ama **alguém**" | Cada pessoa tem o **seu próprio** alguém (pode ser diferente para cada uma) |
| $\exists y\,\forall x\,R(x, y)$ | "existe um $y$ tal que, para todo $x$, $x$ ama $y$" | "**Existe alguém** que todo mundo ama" | **Uma única** pessoa amada por todos |

No primeiro caso, o $y$ pode mudar conforme $x$ — cada um escolhe o seu. No segundo, o **mesmo** $y$ precisa funcionar para todos. São proposições diferentes: a primeira pode ser verdadeira (quase todo mundo ama alguém) enquanto a segunda é falsa (ninguém é amado por todos). **Trocar a ordem na hora de traduzir é a pegadinha.**

No mundo de software, o mesmo par:

> [!example] Um responsável para cada pedido × um responsável por todos
> - "**Todo** pedido **tem um** responsável" = $\forall p\,\exists r\,Responsavel(r, p)$. Cada pedido pode ter um responsável diferente — e isso é realista.
> - "**Existe um** responsável por **todos** os pedidos" = $\exists r\,\forall p\,Responsavel(r, p)$. Um único responsável dá conta de tudo — afirmação muito mais forte e quase sempre falsa em sistemas reais.
>
> Quem traduz a primeira regra na ordem da segunda está autorizando um "super-responsável" que o negócio nunca pediu.

> [!tip] Quando a ordem NÃO importa
> Quantificadores do **mesmo tipo** comutam: $\forall x\,\forall y\,P(x,y)$ é o mesmo que $\forall y\,\forall x\,P(x,y)$ (a ordem não muda "para todos, todos"); $\exists x\,\exists y\,P(x,y)$ é o mesmo que $\exists y\,\exists x\,P(x,y)$ (a ordem não muda "existe um par"). A troca só é perigosa entre $\forall$ e $\exists$.

---

## 6. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] A lógica de primeira ordem **abre a proposição**: sujeito (variável) + predicado, com quantificadores para "todo/algum/nenhum"
> - [ ] **Proposição aberta** ($P(x)$, "$x > 5$") não tem valor de verdade; **fecha** com constante ($P(\text{ana})$) ou com quantificador ($\forall x\,P(x)$, $\exists x\,P(x)$)
> - [ ] **Variável livre** = fora do escopo de qualquer quantificador; **variável ligada** = presa por $\forall$ ou $\exists$ (macete: porta aberta × trava)
> - [ ] **Domínio do discurso** define de onde $x$ pode vir; mudar o domínio muda o valor de verdade
> - [ ] $\forall$ = "todo, todos, cada, qualquer, sempre"; $\exists$ = "existe, algum, pelo menos um, há, alguém"
> - [ ] **Regra de ouro:** $\forall$ casa com $\to$; $\exists$ casa com $\land$
> - [ ] **"Todo $A$ é $B$"** = $\forall x\,(A(x) \to B(x))$ (A dentro de B) — **não** é $\forall x\,(A(x) \land B(x))$
> - [ ] **"Nenhum $A$ é $B$"** = $\forall x\,(A(x) \to \neg B(x)) \equiv \neg\exists x\,(A(x) \land B(x))$ (círculos disjuntos)
> - [ ] **"Algum $A$ é $B$"** = $\exists x\,(A(x) \land B(x))$ — **não** é $\exists x\,(A(x) \to B(x))$
> - [ ] **"Algum $A$ não é $B$"** = $\exists x\,(A(x) \land \neg B(x))$ (existe $A$ fora de $B$)
> - [ ] **Regras-mãe:** $\neg\forall x\,P(x) \equiv \exists x\,\neg P(x)$ e $\neg\exists x\,P(x) \equiv \forall x\,\neg P(x)$
> - [ ] Macete do **coringa troca**: negar = trocar $\forall \leftrightarrow \exists$ **e** negar o predicado — **sempre os dois passos**
> - [ ] Negação das quatro formas: Todo→Algum não; Nenhum→Algum; Algum→Nenhum; Algum não→Todo (padrão circular)
> - [ ] "Alguém" = $\exists x$; "ninguém" = $\neg\exists x \equiv \forall x\,\neg$; "todos" = $\forall x$; "nenhum" = $\forall x\,\neg \equiv \neg\exists x$
> - [ ] **"Algum" não exclui "todo"** ("pelo menos um" é o compromisso mínimo)
> - [ ] "Nenhum $A$ é $B$" ≠ "algum $A$ não é $B$"; "nenhum $A$ não é $B$" = "todo $A$ é $B$"
> - [ ] **"Todo $A$ é $B$" não é simétrico** ("todo $B$ é $A$" é a recíproca, falsa em geral); a contraposição $\forall x\,(\neg B(x) \to \neg A(x))$ é que equivale
> - [ ] Negação em cadeia: $\neg\forall x\,\exists y\,P(x,y) \equiv \exists x\,\forall y\,\neg P(x,y)$ — trocar da esquerda para a direita
> - [ ] **Escopo:** $\forall x\,P(x) \land Q(x)$ deixa $x$ de $Q(x)$ livre; com parênteses $\forall x\,(P(x) \land Q(x))$ liga ambos
> - [ ] **Ordem importa:** $\forall x\,\exists y \neq \exists y\,\forall x$ (cada um tem o seu × um para todos); quantificadores do mesmo tipo comutam

> [!warning] O erro mais comum em prova
> **Negar "todo" fazendo apenas um dos dois passos do coringa.** A resposta errada mais frequente é $\neg\forall x\,P(x) \equiv \forall x\,\neg P(x)$ — **não trocar** o quantificador e apenas negar o predicado ("todos não passaram" em vez de "pelo menos um não passou"). A segunda errada mais frequente é **trocar o quantificador e deixar o predicado intacto** ($\neg\forall x\,P(x) = \exists x\,P(x)$). As duas ignoram metade da regra. Sempre se confira: **a negação troca o quantificador E nega o predicado.** Se a frase original era "Todos passaram", a negação é "pelo menos um não passou" — não "todos não passaram", não "pelo menos um passou".

---

## 7. Próximos passos

Este tópico completou a caixa de ferramentas da lógica: em [[Estruturas-Logicas]] aprendemos as peças; em [[Logica-de-Argumentacao]], a avaliar raciocínios; em [[Logica-Sentencial]], a calcular proposições; agora, em lógica de primeira ordem, aprendemos a escrever com precisão afirmações sobre "quantos" e "quais" indivíduos.

O próximo tópico do bloco é o [[Raciocinio-Matematico-Aplicado]] — problemas aritméticos (porcentagem, regra de três, juros, médias), geométricos (áreas, volumes, semelhança), matriciais e progressões (PA e PG). Você não precisa dele para nada que estudou aqui; ele é que vai se beneficiar da sua lógica: todo problema de porcentagem ou progressão é, no fundo, um enunciado a ser traduzido em estrutura precisa antes de ser calculado.

E a lógica de primeira ordem não fica guardada na prateleira: quando você estudar banco de dados (consultas com `EXISTS`, a negação do "todos" em SQL), desenvolvimento de sistemas (validações, regras de negócio) e testes (casos de teste que procuram o contraexemplo), vai reencontrar $\forall$ e $\exists$ de terno e gravata, disfarçados de palavras e consultas. Reconhecê-los é a vantagem competitiva que este bloco constrói.