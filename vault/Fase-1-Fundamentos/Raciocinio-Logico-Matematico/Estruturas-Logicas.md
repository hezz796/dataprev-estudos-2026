# Estruturas Lógicas

> [!info] Metadados
> **Disciplina:** Raciocínio Lógico Matemático
> **Bloco:** 1.2 — Raciocínio Lógico Matemático (FASE 1 — Fundamentos)
> **Tópico:** 1. Estruturas lógicas
> **Subtópicos:** Proposições e conectivos · Leitura e construção de argumentos
> **Pré-requisitos:** Nenhum
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-26

---

## 1. Por que estudar estruturas lógicas?

Você certamente já precisou tomar uma decisão que dependia de mais de uma condição. Pense numa situação simples: quer sair de casa, mas só vai sair **se** estiver ensolarado **e** você não estiver cansado. Se chover ou você estiver exausto, fica em casa. Esse raciocínio do dia a dia — combinar condições, avaliar situações, tirar conclusões — é exatamente o que a **lógica proposicional** formaliza.

Estudar **estruturas lógicas** é aprender a linguagem precisa por trás do raciocínio. É o alicerce sobre o qual se constrói tudo o que vem depois na ementa: [[Logica-de-Argumentacao]], [[Logica-Sentencial]], e por consequência, programação, banco de dados e arquitetura. Mesmo que você nunca tenha programado, a lógica proposicional será o ferramental que tornará esses conteúdos futuros muito mais acessíveis.

---

## 2. O que é uma proposição?

Antes de falar de conectivos, precisamos entender a unidade fundamental: a **proposição**.

Uma **proposição** (ou **sentença declarativa**) é qualquer enunciado que pode ser classificado como **verdadeiro** ou **falso**, **de forma inequívoca**. Não existe uma terceira possibilidade — nem "talvez", nem "depende", nem "em parte".

> [!example] Exemplos de proposições
> - "O Sol é uma estrela." → **Verdadeira**
> - "Todo mamífero é quadrúpede." → **Falsa** (baleias são mamíferos e não são quadrúpedes)
> - "Brasília é a capital do Brasil." → **Verdadeira**
> - "A próxima Copa do Mundo será na Ásia." → **Falsa ou verdadeira** (mas é uma proposição, pois tem valor definido)

Note que, para ser proposição, não interessa se o conteúdo é verdadeiro ou falso — interessa que **possua um valor de verdade determinado**.

### O que NÃO é proposição

Aqui mora a primeira armadilha de prova. Certos enunciados **parecem** proposições, mas não são:

| Enunciado | Por que não é proposição |
|-----------|--------------------------|
| "Feche a porta!" | É **imperativo** — uma ordem, não se declara um fato |
| "Que horas são?" | É **interrogativo** — uma pergunta, não declara verdadeiro/falso |
| "Que dia lindo!" | É **exclamativo** — expressa emoção |
| "Se $x > 5$, então..." | Possui **variável livre** — o valor de verdade depende de $x$ |
| "Esta frase é falsa." | É **paradoxo** — não admite valor de verdade coerente |

> [!warning] Pegadinha clássica de prova
> Questões frequentemente apresentam perguntas ("O servidor está ativo?") ou frases com "talvez" e perguntam se são proposições. **Responda não.** Apenas enunciados **declarativos** com valor de verdade **definido** são proposições.
>
> **Dica rápida:** Se a frase poderia ser respondida com "sim" ou "não" sem ambiguidade, provavelmente é uma proposição. Se é uma ordem, pergunta ou exclamação, não é.

### 2.1 Além dos 5 casos básicos — o que mais NÃO é proposição

A seção anterior apresentou os cinco casos clássicos: **imperativo, interrogativo, exclamativo, variável livre e paradoxo**. São a base — mas não são tudo. As bancas (especialmente CESPE/Cebraspe e FCC) adoram explorar variações que fogem desses cinco modelos e pegam candidato que estudou superficialmente. Nesta seção, vamos revelar pelo menos cinco variações a mais — e os macetes para não cair nelas.

---

#### 1. Palavras da incerteza (modalidade)

Uma família inteira de pegadinhas gira em torno de palavras que expressam **grau de certeza indefinido**. Sinônimos que aparecem em prova: "talvez", "possivelmente", "provavelmente", "é provável que", "pode ser que", "quase certo".

A regra é direta: tudo o que carrega **incerteza modal** — ou seja, o enunciado não afirma nem nega com certeza, apenas aponta uma probabilidade — **não tem valor de verdade determinado** → não é proposição.

> [!warning] Pegadinha clássica de prova
> "É provável que o sistema caia amanhã." → **NÃO é proposição.**
>
> O enunciado não declara que o sistema caiu nem que não caiu — ele apenas aponta uma possibilidade. Sem valor V/F determinado, não passa no teste da proposição.

Compare com o caso do **futuro incerto** que já vimos:

| Enunciado | Classificação | Por quê? |
|-----------|---------------|----------|
| "A próxima Copa será no Japão." | **É proposição** | Valor existe (V ou F), só está desconhecido |
| "Talvez a próxima Copa seja no Japão." | **NÃO é proposição** | "Talvez" destrói o valor de verdade — não há V/F definido |

A distinção é sutil mas fundamental. Falaremos mais sobre ela na seção de [[Estruturas-Logicas#Nota de consistência — futuro incerto ≠ incerteza modal|Nota de consistência]] lá embaixo.

---

#### 2. Predicados vagos

"João é alto." — Essa frase é proposição?

Parece que sim, afirma algo sobre o mundo. Mas pense melhor: **alto em relação a quê?** Se o critério para "alto" não é definido (não há uma régua: $> 1{,}80\,\text{m}$? $> 1{,}90\,\text{m}$?), não conseguimos atribuir V/F de forma inequívoca.

O mesmo vale para:

- "Está quente." — Quente para quem? Em que contexto?
- "Isso é caro." — Caro comparado com o quê?
- "O filme foi bom." — Bom para quem?

A **vaguidão** impede que o enunciado tenha um valor de verdade **definido**. Se a banca não fornece o parâmetro objetivo (cm, °C, R$, escala de 1 a 10), o predicado é vago → não é proposição.

> [!tip] Macete da régua
> Pergunte: **"Existe uma régua objetiva para medir isso?"** Se sim, com o parâmetro fornecido, vira proposição. Se não há régua, é vago → não é proposição.
>
> - "João tem 1,85 m" → **tem régua (metros)** → **é proposição**
> - "João é alto" → **sem régua** → **não é proposição**

---

#### 3. Indexicais e pronomes — a família mais traiçoeira

Essa é, sem exagero, a parte que mais gera erro em prova. Praticamente todos os pronomes da língua portuguesa aparecem em questões de proposição — mas nem todos funcionam da mesma forma. Dividimos em **três famílias** com comportamentos completamente distintos.

**Família 1 — Pronomes deíticos** (apontam para o contexto)

São pronomes como: **eu, tu, ele, ela, isto, isso, aquele, meu, seu, aqui, agora**. Eles funcionam como um "dedo apontando" — dependem de **quem fala, onde e quando** para ter significado. Enquanto a referência não for fixada, não há valor de verdade → **não são proposição**.

| Pronome deítico | Enunciado | Problema |
|-----------------|-----------|----------|
| **ele** | "Ele é aprovado." | Quem é "ele"? |
| **isto** | "Isto é caro." | O que é "isto"? |
| **meu** | "Meu documento está pronto." | De quem? |
| **aqui** | "Aqui está chovendo." | Onde é "aqui"? |
| **agora** | "Agora faz frio." | Quando é "agora"? |

> [!warning] Pegadinha de prova
> "Ele passou no concurso." → **NÃO é proposição** (enquanto não soubermos quem é "ele"). Se o enunciado fosse "João passou no concurso" → **é proposição**. A banca troca o nome próprio por um pronome deítico e espera que você não perceba.

**Família 2 — Pronomes quantificacionais/indefinidos** (carregam quantificador)

São: **alguém, ninguém, tudo, nada, algum, qualquer, todos, nenhum**. A surpresa: esses pronomes **TÊM valor de verdade definido** → **SÃO proposição** (e já entram na lógica de primeira ordem, com quantificadores $\exists$ e $\forall$).

| Pronome | Equivalência lógica | Exemplo | É proposição? |
|---------|---------------------|---------|---------------|
| **alguém** | $\exists x$ | "Alguém telefonou." | ✅ Sim — $\exists x\,\text{telefonou}(x)$ |
| **ninguém** | $\neg \exists x$ | "Ninguém compareceu." | ✅ Sim — $\neg \exists x\,\text{compareceu}(x)$ |
| **tudo/nada** | $\forall x$ / $\neg \exists x$ | "Tudo foi perdido." | ✅ Sim |
| **algum** | $\exists x$ | "Algum candidato acertou." | ✅ Sim |

> [!tip] Por que são proposição?
> O segredo é que esses pronomes **quantificam** — eles dizem "existe pelo menos um" ($\exists$) ou "para todos" ($\forall$). Ao quantificar, prendem a variável e criam um valor de verdade definido. "Alguém telefonou" é **verdadeiro** se pelo menos uma pessoa telefonou e **falso** se ninguém telefonou. Não depende de contexto — depende da realidade.

**Família 3 — Pronomes relativos** (amarram variável)

São: **que, quem, o qual, cujo**. Eles ligam uma oração à outra e **amarram** a variável a um referente já mencionado. Por isso, **SÃO proposição**.

> "O candidato **que** estudou passou." → **É proposição** — o "que" amarra "candidato" a uma ação definida.

**A DUPLA CARA do "quem" — atenção máxima:**

| Enunciado | Tipo do "quem" | É proposição? |
|-----------|-----------------|---------------|
| "**Quem** chegou cedo?" | Interrogativo (pergunta) | ❌ Não |
| "O homem **que** chegou cedo foi recompensado." | Relativo (amarra variável) | ✅ Sim |

> [!warning] Pegadinha clássica
> A banca troca "que" por "quem" em contextos interrogativos e espera que você trate como se fosse sempre relativo. **"Quem" como pergunta NÃO é proposição** — é interrogativo. **"Quem" como relativo** (após vírgula ou em oração subordinada) **É proposição**.

> [!tip] Macete do pronome-deítico — o "dedo"
> Todo pronome deítico é um **dedo apontando**: ele precisa apontar para algo (fixar referência) para ter sentido. Sem o dedo (sem contexto que fixe a referência), não tem valor de verdade → não é proposição.
>
> "Isto é verdade" → Para ser proposição, precisamos saber: **isto o quê?** Se o contexto diz "A Terra é redonda. Isto é verdade." → agora é proposição, porque "isto" aponta para "A Terra é redonda".
>
> **Memorize:** "Sem dedo, sem valor."

---

#### 4. Variável livre vs. quantificada — o contraste que a banca adora

Esse é o ponto que conecta diretamente o que vimos na tabela original (variável livre = não é proposição) com a lógica de primeira ordem. A banca adora testar se você percebe a diferença entre uma variável **solta** e uma variável **presa** por um quantificador.

| Expressão | Classificação | Por quê? |
|-----------|---------------|----------|
| $x > 5$ | ❌ **NÃO é proposição** | $x$ está solta — vale para $x = 1$ (F), $x = 6$ (V), $x = 10$ (V) |
| $\exists x\,(x > 5)$ | ✅ **É proposição** | "$\exists$" prende $x$ — o enunciado afirma que **existe** pelo menos um valor que satisfaz |
| $\forall x\,(x > 5)$ | ✅ **É proposição** | "$\forall$" prende $x$ — o enunciado afirma que **para todo** valor, a condição vale |

A chave: o **quantificador** ($\exists$ ou $\forall$) transforma uma expressão com variável livre em uma proposição completa. Sem o quantificador, a variável está "pulando" entre valores — não dá para dizer se é V ou F.

> [!tip] Ponte com o próximo tópico
> Esse contraste é a porta de entrada para a [[Logica-de-Primeira-Ordem]], onde veremos quantificadores existencial ($\exists$) e universal ($\forall$) em profundidade. Lá, vamos formalizar exatamente como "alguém", "ninguém", "todos" e "nenhum" se traduzem em símbolos.
>
> Por agora, fixe: **variável solta = porta aberta = não é proposição**; **quantificador = trava = é proposição**.

---

#### 5. Paradoxos além do mentiroso

"Esta frase é falsa." é o paradoxo mais famoso da lógica — mas a banca não se limita a ele. Existem ao menos duas variações que caem em prova:

| Paradoxo | Por que não é proposição |
|----------|--------------------------|
| "Esta frase é falsa." | Se é V → é F; se é F → é V → **sem valor coerente** |
| "Estou mentindo agora." | Se é V → está mentindo → é F; se é F → não está mentindo → é V → **ciclo sem saída** |

> [!warning] Pegadinha clássica de prova
> A banca adora variar o **paradoxo do mentiroso**: troca "esta frase" por "estou mentindo agora", ou embute a auto-referência em frases diferentes. O ponto em comum é a **circularidade**: a frase se auto-avalia e não admite valor de verdade coerente.
>
> **Atenção:** nem toda auto-referência é paradoxo. "Esta frase é verdadeira" não gera contradição (pode ser simplesmente verdadeira), então, estritamente, **é uma proposição** — só é uma frase "estranha". A banca, porém, costuma agrupar frases auto-referenciais; o filtro seguro é: **se atribuir V ou F gera contradição, não é proposição; se dá para atribuir um valor sem contradição, é proposição**.
>
> **Regra geral:** Tudo que se **auto-avalia** e gera circularidade lógica não admite valor de verdade coerente → não é proposição.

---

#### Nota de consistência — futuro incerto ≠ incerteza modal

> [!important] Distinção que define 1 erro em cada prova
> O arquivo (na seção 2.2, Caso 3) trata o **futuro incerto** como proposição: "A próxima Copa será no Japão" → **é proposição**, porque o valor existe (V ou F), só está desconhecido.
>
> Já aqui dissemos que **"Talvez a próxima Copa seja no Japão"** → **NÃO é proposição**, porque o "talvez" destrói o valor de verdade.
>
> **Como conciliar?**
>
> | Tipo de incerteza | Exemplo | É proposição? | Por quê? |
> |-------------------|---------|---------------|----------|
> | **Incerteza no TEMPO** (futuro) | "A Copa será no Japão." | ✅ Sim | O valor existe em princípio — o evento acontece ou não |
> | **Incerteza na CERTEZA** (modal) | "Talvez a Copa seja no Japão." | ❌ Não | O "talvez" impede que o enunciado declare qualquer coisa com valor definido |
>
> **Memorize:**
> - **Futuro esconde a verdade** (mas ela existe) → é proposição
> - **"Talvez" destrói a verdade** (ela não fica definida) → não é proposição
>
> Essa distinção é o **erro nº 1** de quem estudou pela metade. Se a banca colocar uma frase com "talvez" e outra com "será", marque apenas a segunda como proposição.

---

#### Os MACETES — 9 regras para nunca mais errar

> [!tip] Macete 1 — Teste do SIM/NÃO
> Pergunte: **"Essa frase responde sim ou não sem ambiguidade?"** Se sim → provavelmente é proposição. Se a resposta é "depende", "talvez" ou "o quê?" → não é proposição.

> [!tip] Macete 2 — I.I.E. (3 modos do verbo)
> **I**mperativo (manda), **I**nterrogativo (pergunta), **E**xclamativo (sente). Os três **não declaram** fatos → **não são proposição**. Se o verbo está no imperativo, interrogativo ou exclamativo, é golpe de certeza: não é proposição.

> [!tip] Macete 3 — T.P.P. (palavras da dúvida)
> **T**alvez, **P**ossivelmente, **P**rovavelmente. Se aparecer qualquer uma dessas (ou sinônimo), o enunciado carrega **incerteza modal** → sem valor fixo → **não é proposição**.

> [!tip] Macete 4 — Régua do vago
> "João é alto" precisa de uma **régua** para decidir V/F? Se não há régua objetiva (cm, °C, R$), o predicado é vago → **não é proposição**. Se a régua existe no enunciado ("João tem 1,85 m"), vira proposição.

> [!tip] Macete 5 — Dedo do indexical/pronome-deítico
> **Eu, tu, ele, isto, aqui, agora, meu, seu** → são "dedos apontando". Sem fixar a referência (o "dedo" apontar para algo concreto), **não tem valor** → não é proposição. Fixou? Aí vira proposição.

> [!tip] Macete 6 — Variável presa
> "$x$ solto = porta aberta pro valor mudar" → **não é proposição**. O quantificador ($\forall$ ou $\exists$) **prende** a variável → vira proposição. "$x > 5$" não é; "$\exists x\,(x > 5)$" é.

> [!tip] Macete 7 — Espelho do paradoxo
> "Esta frase é falsa" → se é V, vira F; se é F, vira V → **espelho infinito, sem valor**. Tudo que se auto-avalia e gera contradição circular não é proposição.

> [!tip] Macete 8 — Tempo × Certeza
> **Futuro** esconde a verdade (mas ela existe) → é proposição. **"Talvez"** destrói a verdade (não fica definida) → não é proposição. Não confunda incerteza temporal com incerteza modal.

> [!tip] Macete 9 — Pronome: aponta / conta / amarra
> - **Deítico** (eu, ele, isto) → **aponta** (não é até fixar referência)
> - **Quantificacional** (alguém, ninguém, tudo) → **conta** (já é proposição — carrega $\exists$ ou $\forall$)
> - **Relativo** (que, quem) → **amarra** variável (já é proposição)
>
> A banca mistura os três e espera que você trate todos iguais. Não trate.

---

#### Tabela-mestre — TUDO que NÃO é proposição (e o que JÁ é)

| Categoria | Exemplo | Macete | Vira proposição se... |
|-----------|---------|--------|------------------------|
| **Imperativo** | "Feche a porta!" | I.I.E. — manda, não declara | Jamais — modo do verbo não é declarativo |
| **Interrogativo** | "Que horas são?" | I.I.E. — pergunta, não declara | Jamais — é pergunta |
| **Exclamativo** | "Que dia lindo!" | I.I.E. — sente, não declara | Jamais — é emoção |
| **Incerteza (T.P.P.)** | "Talvez chova." | T.P.P. — cheiro de dúvida | Se retirar o "talvez": "Choveu." → sim, é proposição |
| **Vago** | "João é alto." | Régua do vago | Se adicionar parâmetro: "João tem 1,85 m" → sim |
| **Indexical / Deítico** | "Isto é caro." | Dedo do indexical | Se fixar referência: "O carro custa R$ 80 mil e é caro" → sim |
| **Variável livre** | $x > 5$ | Variável presa | Se adicionar quantificador: $\exists x\,(x > 5)$ → sim |
| **Paradoxo** | "Esta frase é falsa." | Espelho do paradoxo | Jamais — auto-contradição lógica |
| **Pronome quantificacional** ✅ | "Alguém telefonou." | Já é proposição | — (já tem valor definido via $\exists$) |
| **Pronome relativo** ✅ | "O candidato que estudou passou." | Já é proposição | — (variável amarrada) |

> [!note] Leia a tabela de baixo para cima
> As duas últimas linhas (quantificacional e relativo) **já são proposições** — aparecem aqui apenas para reforçar a distinção. A banca adora colocar "Alguém telefonou" como alternativa de "não é proposição". Não caia: **já é**.

---

#### Regra de ouro final

> [!important] Proposição exige UMA só coisa
> **Valor de verdade DEFINIDO** (V ou F, sem ambiguidade).
>
> Se o enunciado for:
> - **Ordem** (imperativo) → não declara → ❌ não é proposição
> - **Pergunta** (interrogativo) → não declara → ❌ não é proposição
> - **Emoção** (exclamativo) → não declara → ❌ não é proposição
> - **Dúvida** (talvez, provavelmente) → sem valor fixo → ❌ não é proposição
> - **Vago** (sem régua objetiva) → sem V/F definido → ❌ não é proposição
> - **Dependente de contexto** (pronome deítico sem fixar referência) → ❌ não é proposição
> - **Variável solta** ($x > 5$ sem quantificador) → ❌ não é proposição
> - **Auto-contraditório** (paradoxo) → sem valor coerente → ❌ não é proposição
>
> Mas se for **futuro incerto** ("A próxima Copa será no Japão") → o valor **existe** (só está desconhecido) → ✅ **É proposição**.

### 2.2 Dúvidas frequentes sobre proposições

Antes de avançar, vale esclarecer duas dúvidas que aparecem o tempo todo — tanto em fóruns de estudo quanto em provas disfarçadas.

---

> [!question] "Uma proposição com 'não' é automaticamente falsa?"
>
> Essa confusão é **extremamente** comum. Muita gente olha para uma frase como "O Sol não é uma estrela" e pensa: "Tem um 'não' aí, então é falsa." Mas essa leitura está errada. Vamos desmontar isso.

A palavra **"não"** na linguagem cotidiana funciona como um **interruptor**: ela **inverte** o valor de verdade — troca V por F e F por V. Ela **não força** o resultado ser falso.

Pense assim: se uma afirmação é verdadeira, negá-la torna-a falsa. Mas se a afirmação original é **falsa**, negá-la torna-a **verdadeira**. O "não" é um espelho: ele reflete o contrário, não desliga a luz.

| Enunciado | Valor original | Negação | Valor da negação |
|-----------|---------------|---------|------------------|
| "O Sol é uma estrela" | **V** | "O Sol **não** é uma estrela" | **F** |
| "2 + 2 = 5" | **F** | "2 + 2 **não** é igual a 5" | **V** |
| "Brasília é a capital do Brasil" | **V** | "Brasília **não** é a capital do Brasil" | **F** |
| "Todo número natural é par" | **F** | "**Nem** todo número natural é par" | **V** |

Repare no padrão: o "não" **aparece em todas**, mas metade das negações é verdadeira e a outra metade é falsa. O que determina o valor final **não** é a presença da palavra "não" — é se o enunciado, **depois de negado**, corresponde ou não à realidade.

> [!important] Regra para prova
> Quando uma questão apresentar uma proposição negativa, **não julgue pelo "não"**. Primeiro, descubra o valor da proposição original. Depois, aplique a negação: se era V, agora é F; se era F, agora é V. **Sempre comece pelo original.**
>
> Veremos o símbolo formal dessa operação ($\neg$) na seção [[Estruturas-Logicas#3.1 Negação (¬) — "NÃO"|3.1 — Negação]].

---

> [!question] "De onde obtemos os valores lógicos das proposições?"
>
> O material diz que proposições têm "valor de verdade definido", mas... definido **como**? Quem decide se é V ou F? Essa pergunta parece filosófica, mas tem uma resposta prática que aparece em prova.

O valor de verdade de uma proposição vem da **correspondência entre o enunciado e aquilo que ele descreve**. Esse "aquilo" pode ser o mundo real, um sistema matemático ou um contexto hipotético. Veja os três casos:

**Caso 1 — Proposições sobre o mundo factual:**
Quando dizemos "O Sol é uma estrela", o valor de verdade vem da **observação do mundo real**. A astronomia confirma que o Sol é de fato uma estrela → proposição **verdadeira**. Já "O Sol orbita a Terra" contradiz a realidade → proposição **falsa**. O critério é a **correspondência com a realidade empírica**.

**Caso 2 — Proposições matemáticas:**
Quando dizemos "$2 + 2 = 4$", não consultamos telescópios — consultamos **axiomas e definições** do sistema numérico. Dentro dos axiomas padrão da aritmética, $2 + 2 = 4$ é demonstravelmente verdadeira. Já "$2 + 2 = 5$" é falsa **dentro desse mesmo sistema**. O critério é a **consistência com os axiomas**.

**Caso 3 — Proposições hipotéticas ou futuras:**
"A próxima Copa do Mundo será no Japão" — será verdadeira ou falsa? A resposta é: **é uma das duas, mas ainda não sabemos qual**. Isso não a impede de ser proposição. O valor de verdade existe **em princípio** — o evento vai acontecer ou não — mesmo que temporariamente não possamos verificá-lo. O critério é que o valor **está definido**, mesmo que **desconhecido** por nós.

> [!tip] Atribuição arbitrária — o que vem na prática
> Na lógica formal, especialmente quando construímos tabelas-verdade (que veremos em [[Logica-Sentencial]]), **nós escolhemos** os valores de verdade das proposições para testar se um argumento é válido. Não estamos dizendo "isso é verdadeiro no mundo real" — estamos dizendo "suponha que uma proposição é verdadeira; o que acontece com a expressão completa?"
>
> É como um laboratório: você altera variáveis para ver o comportamento do sistema. Nas tabelas-verdade, testamos **todas** as combinações possíveis (V/V, V/F, F/V, F/F) para garantir que a lógica funciona **independentemente** dos valores específicos.

> [!warning] Pegadinha de prova
> Questões podem tentar confundir perguntando: "A proposição 'O Brasil ganhará a próxima Copa' é verdadeira ou falsa?" A resposta correta **não é "verdadeira" nem "falsa"** — é **"é uma proposição, pois tem valor de verdade definido (embora desconhecido no momento)"**. A banca testa se você entende que "ter valor definido" não é o mesmo que "saber qual é o valor".

### Variáveis proposicionais

Para trabalhar com proposições de forma abstrata, substituímos cada proposição por uma **variável proposicional** — geralmente uma letra maiúscula:

- **P**: "O concurso terá provas objetivas"
- **Q**: "A prova terá questões de lógica"

Com isso, podemos construir **expressões lógicas** que combinam proposições simples em estruturas mais complexas — e é aí que entram os conectivos.

---

## 3. Conectivos lógicos

Os **conectivos lógicos** (também chamados de **operadores lógicos**) são os símbolos que combinam proposições para formar novas proposições. Cada conectivo possui uma regra precisa de funcionamento. Vamos estudá-los um a um.

### 3.1 Negação (¬) — "NÃO"

A negação **inverte** o valor de verdade de uma proposição.

Se **$P$** é verdadeira, então **$\neg P$** é falsa. Se **$P$** é falsa, então **$\neg P$** é verdadeira.

| $P$ | $\neg P$ |
|-----|----------|
| V | F |
| F | V |

É o conectivo mais simples, mas também o mais subestimado.

> [!example] Exemplo
> **$P$**: "O concurso será em agosto."
> **$\neg P$**: "O concurso **não** será em agosto."
>
> Se o concurso é realmente em agosto, **$\neg P$** é falsa. Simples assim.

### 3.2 Conjunção (∧) — "E"

A conjunção combina duas proposições e resulta em **verdadeira apenas quando ambas as partes são verdadeiras**.

| $P$ | $Q$ | $P \land Q$ |
|-----|-----|-------------|
| V | V | **V** |
| V | F | F |
| F | V | F |
| F | F | F |

A regra é intuitiva: **"P E Q" significa que P e Q são verdadeiros ao mesmo tempo**.

> [!tip] Dica de memorização
> Pense no "E" como um crivo exigente — **tudo** precisa passar para resultar em verdadeiro. É como uma lista de requisitos: se falta um, a condição não é satisfeita.

> [!example] Exemplo
> **$P$**: "O candidato é maior de 18 anos."
> **$Q$**: "O candidato possui ensino superior."
> **$P \land Q$**: "O candidato é maior de 18 anos **E** possui ensino superior."
>
> A condição **$P \land Q$** é verdadeira **somente** quando o candidato atende **ambos** os requisitos. Ter apenas um deles não basta.

### 3.3 Disjunção (∨) — "OU"

A disjunção combina duas proposições e resulta em **verdadeira quando pelo menos uma das partes é verdadeira**.

| $P$ | $Q$ | $P \lor Q$ |
|-----|-----|------------|
| V | V | **V** |
| V | F | **V** |
| F | V | **V** |
| F | F | F |

A disjunção é **inclusiva**: quando ambas as partes são verdadeiras, o resultado é verdadeiro.

> [!warning] Pegadinha clássica de prova
> Muitas questões exploram a confusão entre **disjunção inclusiva** e **exclusiva**. Na lógica formal, "ou" significa **inclusivo** — aceita ambas verdadeiras. A disjunção exclusiva (XOR) tem uma simbologia e comportamento próprios, que veremos na [[Estruturas-Logicas#3.3.1 Disjunção exclusiva (⊕) — "OU exclusivo" (XOR)|3.3.1 Disjunção exclusiva]].
>
> Se a banca pergunta sobre "$P \lor Q$" quando $P$ e $Q$ são ambas verdadeiras, a resposta é **verdadeiro**. Não caia no "ou" coloquial, que muitas vezes implica "um ou outro, mas não os dois".

> [!example] Exemplo
> **$P$**: "O candidato é formado em TI."
> **$Q$**: "O candidato possui 3 anos de experiência."
> **$P \lor Q$**: "O candidato é formado em TI **ou** possui 3 anos de experiência."
>
> Se o candidato é formado em TI **e** também tem experiência, a condição continua sendo satisfeita. No "ou" lógico, ter os dois não é problema.

#### 3.3.1 Disjunção exclusiva (⊕) — "OU exclusivo" (XOR)

Existe um "ou" escondido na língua que a banca adora explorar: o **"ou" que exclui**. Na disjunção inclusiva ($\lor$), "ou" significa "pelo menos um" — aceita os dois. Mas há situações em que "ou" significa **uma opção ou a outra, nunca as duas**. É exatamente isso que a **disjunção exclusiva** expressa.

> [!important] A regra de ouro da exclusiva
> $P \oplus Q$ é **verdadeiro quando EXATAMENTE uma** das proposições é verdadeira, e **falso quando ambas têm o mesmo valor** — ou ambas V, ou ambas F. É o "ou" que **exclui** a possibilidade de ambos.

**Tabela-verdade:**

| $P$ | $Q$ | $P \oplus Q$ |
|-----|-----|--------------|
| V | V | **F** |
| V | F | **V** |
| F | V | **V** |
| F | F | **F** |

A regra pode ser lida de forma ainda mais direta: a exclusiva é **verdadeira quando $P$ e $Q$ têm valores diferentes** e **falsa quando têm valores iguais** — quer sejam ambas V, quer ambas F. Se os valores são iguais, o XOR barra; se são diferentes, o XOR libera.

##### Simbologias que caem em prova

A exclusiva aparece com **várias faces** na notação, e a banca pode usar qualquer uma:

| Símbolo | Leitura | Onde aparece |
|---------|---------|--------------|
| $P \oplus Q$ | "P ou exclusivo Q" | Mais comum em lógica |
| $P \underline{\vee} Q$ | "P disjunto exclusivo Q" | Variante com o "V" sublinhado |
| $P \veebar Q$ (⊻) | "P ou exclusivo Q" | Variante gráfica |
| **XOR** | "exclusive OR" | Linguagem de programação (C, Java, Python) |

> [!tip] O fio lógico das simbologias
> Repare que a exclusiva é o **contrário** da disjunção inclusiva $\lor$. Onde $\lor$ aceita ambos, a exclusiva recusa. Ela também guarda uma conexão poderosa para a prova com o conectivo que estudaremos na seção [[Estruturas-Logicas#3.5 Bicondicional (↔) — "SE E SOMENTE SE"|3.5 Bicondicional]] — exploraremos essa relação no momento certo.

##### A ÚNICA diferença diante da inclusiva

Coloquemos as duas disjunções lado a lado. Nas quatro combinações possíveis, note onde elas concordam e onde divergem:

| $P$ | $Q$ | $P \lor Q$ (inclusiva) | $P \oplus Q$ (exclusiva) |
|-----|-----|------------------------|--------------------------|
| V | V | **V** | **F** |
| V | F | **V** | **V** |
| F | V | **V** | **V** |
| F | F | F | F |

> [!warning] Pegadinha nº 1 de provas: tratar todo "ou" como exclusivo
> Na lógica formal, **todo "ou" é inclusivo por padrão** — inclusive "ou...ou". A exclusiva **só aparece com indicação explícita**. A banca coloca "$P \lor Q$" e pergunta o valor quando $P$ e $Q$ são ambas verdadeiras; quem lê com o "ou" do cotidiano marca **F**, mas na lógica a resposta é **V**.
>
> A ÚNICA linha que muda entre as duas tabelas é a **V/V**. Em todas as outras, inclusiva e exclusiva dão o **mesmo** resultado. Decorar isso desarma a pegadinha mais comum.

##### Expressões equivalentes que valem pontos

A exclusiva pode ser reescrita de formas que a banca usa para disfarçar. São dois jeitos de dizer a mesma coisa:

$$
\begin{split}
P \oplus Q &\equiv (P \lor Q) \land \neg(P \land Q) \\
           &\equiv (P \land \neg Q) \lor (\neg P \land Q)
\end{split}
$$

Leia cada uma com calma:

- **$(P \lor Q) \land \neg(P \land Q)$** — "ou um dos dois, **mas não ambos**". A parte $\neg(P \land Q)$ é a trava: ela corta justamente o caso em que os dois são verdadeiros.
- **$(P \land \neg Q) \lor (\neg P \land Q)$** — as duas "rotas alternativas": ou $P$ **sem** $Q$, ou $Q$ **sem** $P$. Só um caminho pode ser trilhado.

> [!note] Conexão adiada — exclusiva × bicondicional
> A relação entre a disjunção exclusiva e o bicondicional será explorada na seção [[Estruturas-Logicas#3.5 Bicondicional (↔) — "SE E SOMENTE SE"|3.5 Bicondicional]].

##### Como a banca sinaliza exclusividade

A exclusiva quase nunca vem escrita como símbolo. Ela vem disfarçada por **expressões que indicam "um só"**. Fique atento a estes sinais:

| Sinal de exclusividade | Exemplo |
|------------------------|---------|
| "ou ... ou ... **mas não ambos**" | "Ou estuda, ou trabalha, **mas não ambos**" |
| "**um ou outro**, exclusivamente" | "Aprova-se um **ou outro**, exclusivamente" |
| "**só um** dos dois" | "**Só um** dos dois será escolhido" |
| "**exatamente um**" | "**Exatamente um** dos requisitos deve constar" |
| "um deles, **e não o outro**" | "Vale um deles, **e não o outro**" |
| "**alternativa**" | "São duas **alternativas** mutuamente excludentes" |

> [!warning] Pegadinha de prova — a partição exaustiva
> A banca coloca "**Ou João é aprovado ou reprovado**" e o candidato marca "exclusivo" por instinto. Na lógica formal, **sem indicação explícita, é inclusivo** ($\lor$) — e nesse caso específico o resultado é até **verdadeiro**, porque aprovado $\lor$ reprovado sempre tem uma parte V, e uma partição exaustiva como aprovado/reprovado cobre todos os casos. Use o "ou" do cotidiano como **pitada**, nunca como regra: a regra é **todo "ou" é inclusivo até que a banca diga o contrário**.

##### Exemplo prático

O tempero que não pode faltar na prova:

> [!example] Exemplo — aprovação em exatamente uma fase
> **$P$**: "O candidato foi aprovado na fase objetiva."
> **$Q$**: "O candidato foi aprovado na fase discursiva."
> **$P \oplus Q$**: "O candidato foi aprovado em **exatamente uma** das duas fases."
>
> | $P$ | $Q$ | $P \oplus Q$ | Leitura |
> |-----|-----|--------------|---------|
> | V | V | **F** | Aprovado nas duas → **não** atende (exige só uma) |
> | V | F | **V** | Só na objetiva → ✅ atende |
> | F | V | **V** | Só na discursiva → ✅ atende |
> | F | F | **F** | Reprovado nas duas → **não** atende |
>
> Se a banca disser apenas "aprovado na objetiva **ou** na discursiva" (sem "exatamente uma"), o conectivo é **inclusivo** ($\lor$) e o caso V/V passa a ser **verdadeiro**. A diferença de uma palavra muda a resposta.

> [!tip] Macete — "a porta de um só"
> A disjunção inclusiva tem o macete da **porta** ("basta uma abrir"). A exclusiva é a **porta que embute a trava da recusa dupla**: ela **deixa passar SÓ UM**. Se tentarem passar dois juntos, a porta **não abre**.
>
> Memorize: **"Ou um, ou outro, mas nunca os dois juntos."** Se os dois entram juntos (V/V), o XOR barra (F).

##### Pegadinha de prova — a precedência do $\oplus$

> [!warning] Pegadinha — onde entra o $\oplus$ na precedência?
> Na [[Estruturas-Logicas#3.7 Precedência de conectivos|precedência]], o $\oplus$ raramente aparece nas tabelas das bancas — e isso é proposital. Como é um "ou", costuma herdar o **mesmo nível da disjunção $\lor$**; porém, para evitar ambiguidade, as provas quase sempre o isolam com **parênteses**. Regra prática: se a expressão tem $\oplus$ sem parênteses, resolva junto com $\land$/$\lor$ da esquerda para a direita; se tem parênteses, **respeite-os**.

### 3.4 Condicional (→) — "SE... ENTÃO"

A condicional é, sem dúvida, o conectivo que gera mais dificuldades em provas. Seu funcionamento é **surpreendente** à primeira vista.

**$P \to Q$** se lê: "**Se** $P$, **então** $Q$." Aqui, **$P$** é a **hipótese** (ou antecedente) e **$Q$** é a **conclusão** (ou consequente).

| $P$ | $Q$ | $P \to Q$ |
|-----|-----|-----------|
| V | V | **V** |
| V | F | **F** |
| F | V | **V** |
| F | F | **V** |

Repare no que acontece: quando a hipótese (**$P$**) é falsa, a condicional é **sempre verdadeira**, independente de $Q$. Por quê?

> [!important] Entendendo a lógica da condicional
> A condicional é uma **promessa**. Dizer "Se chover, levarei guarda-chuva" é uma afirmação que **só é quebrada** se chover e eu **não** levar o guarda-chuva.
>
> - Choveu e levei? → Promessa cumprida (V)
> - Choveu e não levei? → Promessa quebrada (**F**)
> - Não choveu e levei? → Promessa não violada (V)
> - Não choveu e não levei? → Promessa não violada (V)
>
> A condicional só é **falsa** em um único caso: **hipótese verdadeira e conclusão falsa**.

> [!warning] Pegadinha clássica de prova
> A banca adora testar se o candidato aceita que **"Se 2 + 2 = 5, então a Terra é quadrada" é uma proposição VERDADEIRA**. E é! Como a hipótese é falsa (2 + 2 ≠ 5), a condicional é automaticamente verdadeira, independentemente do consequente. Não caia nessa tentativa de confusão.
>
> **Regra de ouro:** Para dizer que uma condicional é falsa, você precisa encontrar um caso em que a hipótese é verdadeira e a conclusão é falsa. Sem esse caso, a condicional é verdadeira.

### 3.5 Bicondicional (↔) — "SE E SOMENTE SE"

O bicondicional expressa **equivalência**: duas proposições possuem o mesmo valor de verdade em **todas** as situações.

> **$P \leftrightarrow Q$** se lê: "**$P$** se e somente se **$Q$**" (ou "$P$ **equivale** a $Q$").

| $P$ | $Q$ | $P \leftrightarrow Q$ |
|-----|-----|----------------------|
| V | V | **V** |
| V | F | F |
| F | V | F |
| F | F | **V** |

O bicondicional é verdadeiro quando ambas as proposições têm o **mesmo** valor de verdade — ou ambas verdadeiras, ou ambas falsas.

> [!tip] Decomposição prática
> **$P \leftrightarrow Q$** equivale a **$(P \to Q) \land (Q \to P)$** — ou seja, "se $P$ então $Q$" **E** "se $Q$ então $P$". É como uma ida e volta: a implicação funciona nos dois sentidos.

> [!example] Exemplo
> **$P$**: "O sol está brilhando."
> **$Q$**: "Está fazendo sol."
> **$P \leftrightarrow Q$**: "O sol está brilhando **se e somente se** está fazendo sol."
>
> Isso significa: se o sol está brilhando, então está fazendo sol. E se está fazendo sol, então o sol está brilhando. As duas proposições andam juntas — quando uma é verdadeira, a outra também é.

> [!important] Conexão com a disjunção exclusiva — são opostos!
> Agora que você conhece os dois conectivos, podemos revelar a relação que ficou guardada na [[Estruturas-Logicas#3.3.1 Disjunção exclusiva (⊕) — "OU exclusivo" (XOR)|3.3.1 Disjunção exclusiva]]:
>
> $$
> P \oplus Q \equiv \neg(P \leftrightarrow Q)
> $$
>
> A disjunção exclusiva é a **negação do bicondicional**. Compare as duas tabelas lado a lado:
>
> | $P$ | $Q$ | $P \leftrightarrow Q$ | $P \oplus Q$ |
> |-----|-----|----------------------|--------------|
> | V | V | **V** | **F** |
> | V | F | F | **V** |
> | F | V | F | **V** |
> | F | F | **V** | **F** |
>
> Repare no padrão: onde o bicondicional é **verdadeiro** (valores **iguais** — V/V ou F/F), a exclusiva é **falsa**; onde o bicondicional é **falso** (valores **diferentes** — V/F ou F/V), a exclusiva é **verdadeira**. Linha por linha, um é o **oposto exato** do outro.

> [!warning] Pegadinha — confundir exclusiva com bicondicional (são opostos!)
> Se $P$ e $Q$ são ambas **verdadeiras**: a exclusiva dá **F**, mas o bicondicional dá **V**. Muita gente decora "iguais = ..." e confunde os dois. São **exatamente opostos** ($P \oplus Q \equiv \neg(P \leftrightarrow Q)$). Na dúvida, monte uma linha da tabela antes de marcar.

### 3.6 Proposições simples e compostas

Até agora, cada proposição que usamos aparecia sozinha — $P$, $Q$, $R$ — e depois conectávamos com um operador para formar algo maior. Mas nem toda proposição que encontramos em prova vem pronta para receber um símbolo. Algumas são **bases isoladas**; outras são **construções montadas**. Saber identificar qual é qual é o primeiro passo para traduzir qualquer enunciado para a linguagem formal.

#### Proposição simples

Uma **proposição simples** é aquela que **não contém conectivos lógicos**. Ela é uma unidade mínima — um fato declarativo que pode ser julgado verdadeiro ou falso sem precisar ser decomposto.

> [!example] Proposições simples
> - "O Sol é uma estrela." → verdadeira, sem conectivos
> - "$2 + 2 = 4$" → verdadeira, é um único enunciado
> - "Brasília é a capital do Brasil." → verdadeira
> - "Todo número par é divisível por 2." → verdadeira

Na notação formal, representamos cada proposição simples por **uma única variável**:

$P$: "O Sol é uma estrela"
$Q$: "2 + 2 = 4"
$R$: "Brasília é a capital do Brasil"

Cada variável carrega **sozinha** todo o significado. Não há "e", "ou" nem "se...então" por dentro.

#### Proposição composta

Uma **proposição composta** é formada por **duas ou mais proposições simples** conectadas por conectivos lógicos. É como montar um quebra-cabeça: cada peça é uma proposição simples, e os conectivos são as travas que as unem.

> [!example] Proposição composta
> "O Sol é uma estrela **E** a Terra orbita o Sol."
>
> - $P$:   O Sol é uma estrela
> - $Q$:   A Terra orbita o Sol
> - Expressão:  $P \land Q$

A presença do "E" no meio revela que a frase não é mais uma unidade indivisível — ela contém **duas** proposições simples unidas por uma conjunção.

Mas atenção: a composta pode ser mais complexa, envolvendo mais de dois conectivos:

> [!example] Composta com múltiplos conectivos
> "Se o candidato estuda lógica **E** resolve simulados, **então** tem chances reais de aprovação."
>
> - $P$: "O candidato estuda lógica"
> - $Q$: "O candidato resolve simulados"
> - $R$: "O candidato tem chances reais de aprovação"

Essa expressão contém **três** proposições simples ($P$, $Q$, $R$) e **dois** conectivos ($\land$ e $\to$). Ela é composta — e bastante composta.

#### Como identificar se é simples ou composta

A pergunta que vai direto ao ponto é: **existem conectivos lógicos atuando sobre proposições dentro do enunciado?**

| Sinal de alerta | O que procurar | Exemplo |
|------------------|----------------|---------|
| **"e"** | Conjunção ($\land$) | "Chove **e** faz frio" |
| **"ou"** | Disjunção ($\lor$) | "Estudou **ou** vai estudar" |
| **"se...então"** | Condicional ($\to$) | "**Se** passar, **então** celebra" |
| **"se e somente se"** | Bicondicional ($\leftrightarrow$) | "Aprova **se e somente se** estuda" |
| **"não"** (formal) | Negação ($\neg$) | "Não é verdade que $P$" |

> [!warning] Cuidado: "não" na linguagem natural ≠ conectivo lógico
> A palavra "não" aparece em muitas proposições simples sem ser um conectivo. Por exemplo:
>
> - "O Sol **não** é um planeta." → Essa é uma proposição **simples**. O "não" está descrevendo uma característica do Sol, não conectando duas proposições.
>
> - "**Não** é verdade que 'O Sol é um planeta'." → Essa **é** uma proposição **composta**, porque o "não" está aplicado **sobre** outra proposição.
>
> A diferença está na **estrutura formal**: se o "não" pode ser isolado como $\neg P$ onde $P$ é uma proposição por si só, é composta. Se o "não" faz parte do conteúdo da própria frase, é simples.
>
> **Regra prática para prova:** Peça a si mesmo: *"posso extrair uma proposição completa e verdadeira/falsa antes do 'não'?"* Se sim, é composta ($\neg P$). Se não, é simples.

> [!tip] Resumo visual
> | Tipo | Estrutura | Notação |
> |------|-----------|---------|
> | **Simples** | Uma única proposição, sem conectivos | $P$ |
> | **Composta** | Duas ou mais proposições com conectivos | $P \land Q$, $P \to Q$, $\neg P$, etc. |
>
> **Pergunta-chave:** "Tem conectivo atuando sobre proposições dentro da frase?"
> - Sim → composta
> - Não → simples

#### Decompondo proposições compostas: exercício prático

A habilidade mais cobrada em prova não é apenas **reconhecer** se é simples ou composta — é **decompor** uma frase complexa nas suas proposições simples. Vamos treinar passo a passo.

> [!example] Exercício completo
> **Enunciado:** "O candidato é aprovado se e somente se estuda lógica e resolve simulados, ou se possui experiência anterior."
>
> **Passo 1 — Identificar os conectivos na frase:**
> - "se e somente se" → $\leftrightarrow$
> - "e" → $\land$
> - "ou" → $\lor$
>
> **Passo 2 — Separar as proposições simples:**
> - $P$: "O candidato é aprovado"
> - $Q$: "O candidato estuda lógica"
> - $R$: "O candidato resolve simulados"
> - $S$: "O candidato possui experiência anterior"
>
> **Passo 3 — Montar a expressão com parênteses:**
>
> Leia a frase com atenção e identifique **que partes se agrupam**:
>
> - "estuda lógica **e** resolve simulados" → essas duas proposições formam um bloco: $(Q \land R)$
> - "ou se possui experiência anterior" → o "ou" liga esse bloco a $S$: $((Q \land R) \lor S)$
> - "aprovado **se e somente se** ..." → o bicondicional liga $P$ ao bloco completo: $P \leftrightarrow ((Q \land R) \lor S)$
>
> **Dica:** Use parênteses sempre que a frase indicar agrupamento. Na dúvida, parênteses a mais é melhor que parênteses a menos.
>
> **Passo 4 — Verificar: a expressão reflete a frase original?**
>
> - "O candidato é aprovado" = $P$ ✓
> - "se e somente se" = $\leftrightarrow$ ligando $P$ ao restante ✓
> - "estuda lógica e resolve simulados" = $Q \land R$ ✓
> - "ou se possui experiência anterior" = $\lor S$ ✓
>
> **Resultado:** quatro proposições simples, três conectivos, uma composição completa.

> [!warning] Pegadinha clássica de prova
> Questões frequentemente apresentam uma frase como "Não é verdade que todos os candidatos passam" e perguntam quantas proposições simples existem. Muita gente responde **uma**, mas a resposta correta depende da estrutura:
>
> - "Todos os candidatos passam" pode ser uma proposição quantificada (veremos em [[Logica-de-Primeira-Ordem]])
> - "Não é verdade que..." aplica a negação sobre ela → composição com $\neg$
>
> **Estratégia:** Sempre tente decompor. Se você consegue isolar uma proposição completa antes de um conectivo, ela é simples e a frase é composta. Se não consegue decompor nada, é simples.

> [!tip] Conexão com o que vem depois
> Decompor proposições compostas é a base para construir **tabelas-verdade** (ver [[Logica-Sentencial]]). Cada variável simples ($P$, $Q$, $R$) corresponde a uma **coluna** da tabela, e os conectivos determinam as regras de combinação. Quanto melhor você decompor agora, mais fácil será montar tabelas depois.

### 3.7 Precedência de conectivos

Na seção anterior, decomponos proposições compostas e mencionamos "respeitar a precedência dos conectivos". Mas o que isso significa, exatamente? É aqui que muita gente tropeça — e a banca sabe disso.

#### O que é precedência e por que importa

Você já sabe que, na matemática, $2 + 3 \times 4$ resulta em **14**, e não em **20**. Por quê? Porque a multiplicação tem **precedência** sobre a soma — resolvemos o $3 \times 4$ primeiro, e depois somamos o 2. Se a matemática não tivesse essa regra, a expressão seria ambígua: alguém interpretaria como $(2 + 3) \times 4 = 20$, e outra pessoa como $2 + (3 \times 4) = 14$.

A lógica proposicional enfrenta o mesmo problema. Olhe para esta expressão:

$$P \lor Q \to R \land S$$

Sem uma regra de precedência, ela seria ambígua. Seria $(P \lor Q) \to (R \land S)$? Ou seria $P \lor (Q \to R) \land S$? Ou ainda $P \lor ((Q \to R) \land S)$? Cada interpretação produz resultados diferentes na tabela-verdade.

A **precedência de conectivos** é a regra que determina **qual conectivo é avaliado primeiro** quando uma expressão contém múltiplos operadores sem parênteses. É o equivalente lógico da "ordem das operações" da aritmética.

> [!important] Por que isso cai em prova
> Questões de [[Logica-Sentencial]] frequentemente apresentam expressões com vários conectivos e pedem o valor de verdade ou a tabela-verdade correspondente. Se você avaliar os conectivos na ordem errada, chegará a uma resposta completamente diferente — e a banca inclui exatamente essa resposta incorreta como alternativa.

#### Hierarquia completa de precedência

Do **maior** para o **menor**:

| Precedência | Conectivo | Leitura | Observação |
|:-----------:|-----------|---------|------------|
| 1 (maior) | $\neg$ | Negação | Processado primeiro |
| 2 | $\land$ | Conjunção | **Mesma precedência** — da esquerda para a direita |
| 2 | $\lor$ | Disjunção | **Mesma precedência** — da esquerda para a direita |
| 3 | $\to$ | Condicional | |
| 4 (menor) | $\leftrightarrow$ | Bicondicional | Processado por último |

> [!tip] Regra mnemotécnica
> Lembre-se: **"Não, E/OU, Se, Se-e-somente-se"** — negação primeiro, depois conjunção e disjunção (que compartilham o mesmo nível), depois condicional e, por último, bicondicional.

A regra crucial aqui é que $\land$ e $\lor$ **compartilham o mesmo nível de precedência**. Quando aparecem juntos na mesma expressão, são avaliados **da esquerda para a direita**. Por exemplo:

$$P \lor Q \land R$$

É avaliado como $(P \lor Q) \land R$ — primeiro a disjunção (à esquerda), depois a conjunção.

E quando temos múltiplos $\land$ ou múltiplos $\lor$ seguidos, a avaliação também segue a ordem de leitura:

$$P \land Q \land R \quad \Rightarrow \quad (P \land Q) \land R$$

Isso vale tanto para $\land$ quanto para $\lor$, que são **associativos** — o resultado final é o mesmo, independente de como agrupemos.

#### Exemplos práticos de resolução

Vamos resolver expressões reais, passo a passo, aplicando a hierarquia.

**Exemplo 1 — Expressão simples:** $P \lor Q \to R$

1. Identificamos os conectivos: $\lor$ (disjunção) e $\to$ (condicional)
2. $\lor$ tem precedência **maior** que $\to$
3. Primeiro: $A = P \lor Q$
4. Depois: $A \to R$
5. **Resultado:** $(P \lor Q) \to R$

**Exemplo 2 — Expressão complexa:** $\neg P \land Q \to R \lor S \leftrightarrow T$

1. **$\neg$ primeiro:** negamos $P$ → temos $\neg P$
2. **$\land$ e $\lor$ (mesma precedência, esquerda para direita):** $\neg P \land Q$ e depois $R \lor S$
3. **$\to$ depois:** $(\neg P \land Q) \to (R \lor S)$
4. **$\leftrightarrow$ por último:** $((\neg P \land Q) \to (R \lor S)) \leftrightarrow T$

Passo a passo visual:

$$
\begin{split}
&\neg P \land Q \to R \lor S \leftrightarrow T \\
\Rightarrow\; &(\neg P) \land Q \to R \lor S \leftrightarrow T \quad \text{(1. negação)} \\
\Rightarrow\; &((\neg P) \land Q) \to (R \lor S) \leftrightarrow T \quad \text{(2. conjunção e disjunção)} \\
\Rightarrow\; &(((\neg P) \land Q) \to (R \lor S)) \leftrightarrow T \quad \text{(3. condicional)} \\
\Rightarrow\; &\bigl(((\neg P) \land Q) \to (R \lor S)\bigr) \leftrightarrow T \quad \text{(4. bicondicional)}
\end{split}
$$

> [!note] Observe o padrão
> Cada conectivo "pega" os dois operandos mais próximos, mas só entra na avaliação quando chega a sua vez na hierarquia. A negação é instantânea (afeta só o que está imediatamente à sua direita). A conjunção e a disjunção formam "blocos". A condicional liga esses blocos. E o bicondicional é o último a agir, conectando tudo o que ficou à esquerda com o que ficou à direita.

#### A importância dos parênteses

Os parênteses têm **precedência absoluta** — eles sobrepõem qualquer regra da hierarquia. Quando um conectivo está entre parênteses, é avaliado **antes** de qualquer outro, independente de sua posição na tabela.

Compare estas duas expressões:

$$(P \lor Q) \to R \quad \neq \quad P \lor (Q \to R)$$

Na primeira, calculamos $P \lor Q$ primeiro e depois aplicamos a condicional com $R$. Na segunda, calculamos $Q \to R$ primeiro e depois fazemos a disjunção com $P$. Resultados completamente diferentes.

> [!warning] Pegadinha clássica de prova
> A banca adora inverter os parênteses para ver se você presta atenção. Uma expressão como "$P \to Q \lor R$" **não** é a mesma que "$P \to (Q \lor R)$" — pela precedência, $\lor$ é avaliado antes de $\to$, então a primeira expressão já equivale à segunda. Mas "$(P \to Q) \lor R$" é **totalmente diferente**: primeiro calculamos a condicional e depois fazemos a disjunção. Se a questão trocar os parênteses, o resultado muda.
>
> **Regra de ouro:** Quando em dúvida, **use parênteses**. É mais seguro, mais claro e evita erros. Em prova, quando a expressão já vem com parênteses, **respeite-os** — eles estão lá justamente para eliminar a ambiguidade.

#### Tabela-resumo da precedência

| Posição | Conectivo | Símbolo | Quando é avaliado |
|:-------:|-----------|:-------:|-------------------|
| 1º | Negação | $\neg$ | Primeiro — afeta só o que está imediatamente à sua direita |
| 2º | Conjunção | $\land$ | Da esquerda para a direita (mesmo nível que $\lor$) |
| 2º | Disjunção | $\lor$ | Da esquerda para a direita (mesmo nível que $\land$) |
| 3º | Condicional | $\to$ | Depois de todos os $\land$ e $\lor$ |
| 4º | Bicondicional | $\leftrightarrow$ | Por último — menos precedência de todos |

#### Exercício prático

Avalie a expressão abaixo, aplicando a precedência passo a passo:

$$\neg P \lor Q \to \neg R \land S \leftrightarrow T$$

> [!example] Resolução passo a passo
> **Passo 1 — Negações ($\neg$):**
> Identificamos $\neg P$ e $\neg R$
> $$\underbrace{(\neg P)}_{A} \lor Q \to \underbrace{(\neg R)}_{B} \land S \leftrightarrow T$$
>
> **Passo 2 — Conjunção e disjunção ($\land$ e $\lor$), esquerda para direita:**
> - $\lor$ aparece entre $A$ e $Q$ → calculamos $A \lor Q$
> - $\land$ aparece entre $B$ e $S$ → calculamos $B \land S$
> $$\underbrace{(A \lor Q)}_{C} \to \underbrace{(B \land S)}_{D} \leftrightarrow T$$
>
> **Passo 3 — Condicional ($\to$):**
> Calculamos $C \to D$
> $$\underbrace{(C \to D)}_{E} \leftrightarrow T$$
>
> **Passo 4 — Bicondicional ($\leftrightarrow$):**
> Calculamos $E \leftrightarrow T$
>
> **Resultado final:** $\bigl((\neg P \lor Q) \to (\neg R \land S)\bigr) \leftrightarrow T$

#### Pegadinhas de prova — erros comuns de precedência

> [!warning] Erro 1: avaliar $\to$ antes de $\land$ ou $\lor$
> Em $P \land Q \to R$, muita gente lê como $P \land (Q \to R)$. Isso está **errado**. A precedência é $\land$ antes de $\to$, então a leitura correta é $(P \land Q) \to R$. A banca inclui a interpretação errada como alternativa.

> [!warning] Erro 2: tratar $\land$ e $\lor$ com precedências diferentes
> $\land$ e $\lor$ têm **exatamente** a mesma precedência. Não existe "$\land$ antes de $\lor$" nem vice-versa. Quando aparecem juntos, resolva **da esquerda para a direita**. Exemplo: $P \lor Q \land R$ equivale a $(P \lor Q) \land R$.

> [!warning] Erro 3: esquecer que $\neg$ afeta só o próximo termo
> Em $\neg P \land Q$, a negação se aplica **apenas a $P$**, não a toda a expressão. O resultado é $(\neg P) \land Q$, e **não** $\neg(P \land Q)$. Para negar toda a expressão, seria necessário usar parênteses: $\neg(P \land Q)$.

> [!warning] Erro 4: trocar a direção da avaliação de $\land$ e $\lor$
> Quando múltiplos conectivos do mesmo nível aparecem, avalie **da esquerda para a direita**. Em $P \land Q \land R$, calcule $(P \land Q)$ primeiro e depois o resultado com $R$. Não comece pelo $\land$ da direita — a ordem importa (embora, para $\land$ e $\lor$, o resultado final seja o mesmo por associatividade, a banca pode cobrar o **processo**).

### 3.8 Outros termos e formas de expressar os conectivos

Até aqui, cada conectivo apareceu com seu nome canônico: "não", "e", "ou", "se...então", "se e somente se". Mas nas provas, a banca quase nunca escreve essas palavras exatas. Em vez disso, camufla os conectivos atrás de sinônimos, construções indiretas e variações linguísticas que fazem o candidato que só treinou com "E/OU/SE" tropeçar. Quem reconhece essas variações traduz a frase em segundos; quem não reconhece perde tempo (e pontos).

A pergunta central desta seção é: **como reconhecer cada conectivo mesmo quando a banca disfarça a palavra?** Vamos conectivo por conectivo.

---

#### Negação ($\neg$) — "NÃO"

| Termo / construção | Exemplo curto | Equivalência lógica |
|--------------------|---------------|---------------------|
| não | "Não chove hoje" | $\neg P$ |
| nunca | "Nunca chove em dezembro" | $\neg P$ |
| jamais | "Jamais voltaria" | $\neg P$ |
| nenhum / nenhuma | "Nenhum candidato faltou" | $\neg P$ |
| nem | "Nem um só passou" | $\neg P$ |
| "não é verdade que..." | "Não é verdade que todos passaram" | $\neg P$ |
| "é falso que..." | "É falso que o Sol orbita a Terra" | $\neg P$ |
| "ao contrário" | "Ao contrário do que se pensa..." | $\neg P$ |
| "impossível que..." | "Impossível que isso seja verdade" | $\neg P$ |

> [!tip] Macete — "O espelho"
> A negação é um espelho: ela **troca** V↔F. Não force o resultado ser falso — pergunte-se qual era o valor da frase original e **inverta**. Se o original era V, a negação é F; se o original era F, a negação é V. O "não" não é um interruptor que desliga — é um espelho que reflete o contrário.
>
> Memorize: **"Espelho inverte, não apaga."**

> [!warning] Pegadinha clássica — "nem" nega o quantificador
> Cuidado com frases como "nem todos os candidatos passaram". O "nem" aqui **nega o quantificador "todos"**, não a proposição inteira. Traduza assim:
>
> - "Todos passaram" = $\forall x \, P(x)$
> - "Nem todos passaram" = $\neg(\forall x \, P(x))$ = $\exists x \, \neg P(x)$
>
> A banca adora trocar "não todos" por "nem todos" para testar se você percebe que o "nem" é uma negação — e que a negação de "todos" **não** é "nenhum". O "nem todos" significa "pelo menos um não passou", não "todos ficaram de fora".

---

#### Conjunção ($\land$) — "E"

| Termo / construção | Exemplo curto | Equivalência lógica |
|--------------------|---------------|---------------------|
| e | "Chove **e** faz frio" | $P \land Q$ |
| mas | "Chove **mas** faço sol" | $P \land Q$ |
| porém | "É caro, **porém** vale a pena" | $P \land Q$ |
| contudo | "É difícil, **contudo** possível" | $P \land Q$ |
| bem como | "Estuda lógica **bem como** programação" | $P \land Q$ |
| assim como | "Estuda lógica, **assim como** matemática" | $P \land Q$ |
| tanto...quanto | "Estuda lógica **tanto quanto** português" | $P \land Q$ |
| além de | "**Além de** estudar, resolve simulados" | $P \land Q$ |
| juntamente com | "Chega cedo, **juntamente com** o colega" | $P \land Q$ |
| também | "Estuda lógica e **também** português" | $P \land Q$ |
| "que" (relativo ligando dois fatos) | "O candidato **que** estuda **e** passa é diligente" | $P \land Q$ |

> [!tip] Macete — "O crivo exigente"
> A conjunção é como uma **lista de checklist**: precisa marcar **TODAS** as caixas para passar. Se falta um único item, o crivo trava. Pense: "para ser V, precisa cumprir tudo — sem exceção."
>
> Memorize: **"Crivo exige tudo: um só faltando trava."**

> [!warning] Pegadinha clássica — "mas", "porém" e "contudo" são conjunção!
> Na vida cotidiana, "mas", "porém" e "contudo" soam como **oposição** — como se algo contradizesse o outro. Em lógica formal, eles são **sinônimos exatos de "e"**: precisam que **ambos** os lados sejam verdadeiros.
>
> Exemplo: "Chove **mas** faço sol" → $P \land Q$. Para essa expressão ser verdadeira, **precisa chover E precisa fazer sol ao mesmo tempo**. O "mas" não nega nada — apenas sinaliza que a combinação é surpreendente. A surpresa é psicológica, não lógica.
>
> **Regra de ouro para prova:** Substitua "mas"/"porém"/"contudo" por "e" na sua cabeça. Se a frase faz sentido com "e", é conjunção. Não caia na tentação de inverter o sinal por causa da "oposição" que a palavra sugere.

---

#### Disjunção ($\lor$) — "OU" (inclusivo)

| Termo / construção | Exemplo curto | Equivalência lógica |
|--------------------|---------------|---------------------|
| ou | "Estuda **ou** trabalha" | $P \lor Q$ |
| ou...ou | "**Ou** estuda, **ou** trabalha" | $P \lor Q$ |
| quer...quer | "**Quer** estuda, **quer** trabalha" | $P \lor Q$ |
| ora...ora | "**Ora** estuda, **ora** trabalha" | $P \lor Q$ |
| seja...seja | "**Seja** estuda, **seja** trabalha" | $P \lor Q$ |
| "pelo menos um de" | "**Pelo menos um** dos requisitos deve ser atendido" | $P \lor Q$ |
| "ao menos" | "Precisa de **ao menos** 3 anos" | $P \lor Q$ |
| "a menos que" | "Vai **a menos que** chova" | $P \lor Q$ (equivale a $\neg Q \to P$) |
| "a não ser que" | "Vai **a não ser que** chova" | $P \lor Q$ (equivale a $\neg Q \to P$) |

> [!tip] Macete — "Uma porta basta"
> A disjunção é uma **catraca com duas portas**: basta uma abrir para passar. Só trava quando **ambas** estão fechadas (F∧F). Pense: "se pelo menos uma opção funciona, eu passo."
>
> Memorize: **"Duas portas, basta uma. Só trava com ambas fechadas."**

> [!warning] Pegadinha 1 — "a menos que" NÃO é conjunção!
> Essa é uma das maiores armadilhas em prova. O candidato lê "a menos que" e pensa em "restrição", como se fosse um "e" (exigindo algo a mais). Mas **"a menos que" traduz para disjunção ($\lor$)** — e, mais precisamente, para uma **condicional** com o antecedente negado.
>
> **Regra formal:** "$P$ a menos que $Q$" $\equiv \neg Q \to P \equiv P \lor Q$.
>
> Veja o exemplo: "Vai à festa **a menos que** chova."
> - $V$ = "vai à festa", $C$ = "chova"
> - Tradução: "Se **não** chover, vai" = $\neg C \to V$, que equivale a $V \lor C$ (vai **ou** chova — pelo menos um dos dois).
>
> O ponto que importa para prova: **"a menos que" é $\lor$ / $\to$, nunca $\land$**. A banca conta com você pensar "restrição" e marcar conjunção. Se a dúvida persistir, use a fórmula-mestra: troque "a menos que $Q$" por "se não $Q$" e monte a condicional $\neg Q \to P$.

> [!warning] Pegadinha 2 — "ou...ou" é inclusivo salvo indicação explícita
> Na lógica formal, **todo "ou" é inclusivo** por padrão. "Ou...ou" também é. Só vira **exclusivo** (XOR) quando a banca coloca uma indicação **explícita** como "mas não os dois", "um ou outro, exclusivamente", ou símbolo $\oplus$.
>
> Exemplo: "O candidato é aprovado ou reprovado" → Em provas, considere isso como inclusivo ($\lor$) a menos que a banca especifique exclusividade. Muita gente marca "exclusivo" por instinto — e erra.

---

#### Condicional ($\to$) — "SE... ENTÃO"

| Termo / construção | Exemplo curto | Equivalência lógica |
|--------------------|---------------|---------------------|
| se | "**Se** estudar, passa" | $P \to Q$ |
| caso | "**Caso** estude, terá vantagem" | $P \to Q$ |
| supondo que | "**Supondo que** estude, passará" | $P \to Q$ |
| contanto que | "**Contanto que** estude, passará" | $P \to Q$ |
| desde que | "Passa **desde que** estude" | $P \to Q$ |
| "na hipótese de" | "**Na hipótese de** chover, levo guarda-chuva" | $P \to Q$ |
| "quando" (condicional) | "**Quando** chegar, aviso" | $P \to Q$ |
| "é condição SUFICIENTE para" | "Estudar é **suficiente** para passar" | $P \to Q$ |
| "é condição NECESSÁRIA para" | "Estudar é **necessário** para passar" | $Q \to P$ |

> [!tip] Macete — "SUficiente antes da seta, NEcessária depois"
> A confusão entre necessária e suficiente é o erro mais frequente em prova. Memorize assim:
>
> - **SU**ficiente → **S**ai **U**ma seta (antes da seta, no antecedente): "$P$ é suficiente para $Q$" → $P \to Q$
> - **NE**cessária → **N**a c**E**la (depois da seta, no consequente): "$Q$ é necessária para $P$" → $P \to Q$
>
> Ou de forma direta: o que é **suficiente** fica antes da seta; o que é **necessário** fica depois da seta. Se inverter, inverteu a seta — e errou.

> [!warning] Pegadinha — confundir necessária e suficiente inverte a seta
> A banca adora testar: "Estudar é condição **necessária** para ser aprovado. Qual a expressão correta?"
>
> - Muita gente marca: $E \to A$ (estudar implica aprovação) ← **ERRADO!**
> - Correto: "Estudar é necessário para ser aprovado" significa "sem estudo, não há aprovação". Tradução formal: $\neg E \to \neg A$ (equivalente a $A \to E$). Ou seja: **a aprovação implica o estudo** — $A \to E$.
>
> Note a diferença: no erro comum ($E \to A$), o estudo "garante" a aprovação. No correto ($A \to E$), a aprovação "pressupõe" o estudo. São sentidos opostos.
>
> **Dica de prova:** Sempre pergunte: **"Se acontece X, Y obrigatoriamente acontece?"** Se a resposta é "X é imprescindível para Y" (sem X não tem Y), então Y→X. O necessário vai **depois** da seta.

---

#### Bicondicional ($\leftrightarrow$) — "SE E SOMENTE SE"

| Termo / construção | Exemplo curto | Equivalência lógica |
|--------------------|---------------|---------------------|
| se e somente se | "Passa **se e somente se** estuda" | $P \leftrightarrow Q$ |
| sse (abrev. de "se e somente se") | "Passa **sse** estuda" | $P \leftrightarrow Q$ |
| "se, e apenas se" | "Passa **se, e apenas se**, estuda" | $P \leftrightarrow Q$ |
| "é condição necessária e suficiente" | "Estudar é **necessária e suficiente** para passar" | $P \leftrightarrow Q$ |
| "equivale a" | "$P$ **equivale** a $Q$" | $P \leftrightarrow Q$ |
| "tem o mesmo valor que" | "Tem o **mesmo valor que** ser aprovado" | $P \leftrightarrow Q$ |
| **"somente se"** (⚠️ **só uma direção!**) | "Passa **somente se** estuda" | $P \to Q$ (**não** é $\leftrightarrow$!) |

> [!tip] Macete — "Via de mão dupla"
> O bicondicional é uma **estrada de mão dupla**: funciona nos dois sentidos. O símbolo $\leftrightarrow$ são literalmente **duas setas encarando**: $P \to Q$ **E** $Q \to P$. Quando a banca usa "se e somente se", ela está dizendo: "isso só acontece junto — nunca um sem o outro."
>
> Memorize: **"$\leftrightarrow$ = duas setas = ida e volta = juntos ou nada."**

> [!warning] Pegadinha CRÍTICA — "somente se" sozinho é UMA via só
> Essa é provavelmente a pegadinha mais perigosa desta seção. "Somente se" **sozinho** NÃO é bicondicional — é **condicional em uma direção só**. O "somente" restringe, não equivale.
>
> Compare os três casos com o mesmo exemplo:
>
> | Enunciado | Forma lógica | Conectivo |
> |-----------|-------------|-----------|
> | "Passa **se** estudar" | $E \to P$ | Condicional |
> | "Passa **somente se** estudar" | $P \to E$ | Condicional (direção invertida!) |
> | "Passa **se e somente se** estudar" | $P \leftrightarrow E$ | Bicondicional ✅ |
>
> Veja a diferença:
> - "$E \to P$": "Se estuda, passa" — estudar garante aprovação.
> - "$P \to E$": "Se passa, estudou" — quem passou necessariamente estudou (mas pode ser que nem todo estudante passe).
> - "$P \leftrightarrow E$": "Passa se e somente se estudar" — os dois andam juntos sempre.
>
> **Regra de ouro:** "Somente se" sozinho = condicional (a direção do "somente" aponta para o antecedente da condicional). Só vira bicondicional com "**se e** somente se" — os dois precisam estar juntos.

---

> [!tip] Tabela de bolso para prova
> Leve esta tabela para a prova — é um resumo de tudo que vimos:
>
> | Conectivo | Sinônimos que caem em prova | Macete |
> |-----------|----------------------------|--------|
> | $\neg$ (Negação) | não, nunca, jamais, nem, "não é verdade que", "é falso que", impossível | **Espelho** — inverte V↔F |
> | $\land$ (Conjunção) | e, mas, porém, contudo, bem como, tanto...quanto, além de, também | **Crivo** — exige TODAS as caixas |
> | $\lor$ (Disjunção) | ou, quer...quer, ora...ora, "pelo menos um", "a menos que", "a não ser que" | **Porta** — basta uma abrir |
> | $\to$ (Condicional) | se, caso, desde que, contanto que, "é suficiente para", "é necessário para" | **Seta** — suficiente antes, necessário depois |
> | $\leftrightarrow$ (Bicondicional) | se e somente se, sse, "equivale a", "mesmo valor que" | **Via dupla** — ida e volta |

> [!important] Regra de ouro para o estudante
> Ao encontrar qualquer uma dessas construções em prova, **não procure o símbolo** — procure o **significado**. Faça a si mesmo estas três perguntas:
>
> 1. **"Isso exige tudo ou basta um?"** → Se exige tudo, é $\land$. Se basta um, é $\lor$.
> 2. **"Isso é uma promessa?"** (Se X acontecer, Y obrigatoriamente acontece?) → Se sim, é $\to$. A promessa só é quebrada com $V \to F$.
> 3. **"Dá pra voltar o caminho?"** (Se eu sei o resultado, posso garantir a causa?) → Se sim, e funciona nos dois sentidos, é $\leftrightarrow$. Se funciona em uma direção só, é $\to$.
>
> Essas três perguntas substituem qualquer decoreba — e funcionam mesmo quando a banca inventa sinônimos novos.

---

## 4. Tabela-resumo dos conectivos

Consolidando tudo em uma referência rápida:

| Conectivo | Símbolo | Leitura | Regra de ouro | Quando é FALSO? |
|-----------|---------|---------|---------------|-----------------|
| Negação | $\neg$ | "NÃO $P$" | Inverte o valor | Nunca é impossível (inverte o que tem) |
| Conjunção | $\land$ | "$P$ E $Q$" | Ambos devem ser V | Pelo menos um é F |
| Disjunção | $\lor$ | "$P$ OU $Q$" | Pelo menos um é V | Ambos são F |
| Condicional | $\to$ | "SE $P$ ENTÃO $Q$" | Só é F quando V$\to$F | Exatamente: $P$=V e $Q$=F |
| Bicondicional | $\leftrightarrow$ | "$P$ SE E SOMENTE SE $Q$" | Ambos iguais | Valores diferentes |

> [!tip] Atalho para prova
> Se você decorar apenas **uma** linha da tabela de cada conectivo, decore esta:
> - **$\land$ (E):** só é F se **pelo menos um** for F
> - **$\lor$ (OU):** só é F se **ambos** forem F
> - **$\to$ (SE...ENTÃO):** só é F se o **primeiro for V e o segundo for F**
> - **$\leftrightarrow$ (SE E SOMENTE SE):** só é F se forem **diferentes**

---

## 5. Leitura e construção de argumentos

Agora que dominamos proposições e conectivos, vamos ao segundo subtópico: como **ler**, **interpretar** e **construir argumentos** lógicos.

### 5.1 O que é um argumento?

Um **argumento** é um conjunto de proposições em que algumas (chamadas de **premissas**) são apresentadas como razão para aceitar outra proposição (chamada de **conclusão**).

A estrutura básica é:

```
Premissa 1: ...
Premissa 2: ...
...
Conclusão: ...
```

A questão central não é "o argumento é bonito?" ou "soa convincente?", mas sim: **dadas as premissas como verdadeiras, a conclusão necessariamente se segue?**

### 5.2 Modus Ponens (afirmação do antecedente)

Antes de decorar fórmulas, vamos construir o raciocínio juntos. Pense na situação abaixo:

> Se **chover hoje**, eu **levarei guarda-chuva**.

Agora responda mentalmente: choveu hoje? Se a resposta é **sim**, o que acontece com a promessa de levar guarda-chuva?

Se choveu — ou seja, a condição inicial se realizou —, eu **não tenho escolha**: preciso levar o guarda-chuva, senão quebro minha palavra. Esse é, em essência, o **Modus Ponens**: o padrão lógico que diz que, se a condição de uma promessa se cumpre, a consequência também deve se cumprir.

A estrutura formal é assim:

$$
\begin{aligned}
&P \to Q \quad \text{(se } P\text{, então } Q\text{)} \\
&P \quad \text{(}P\text{ é verdadeira)} \\
&\therefore \; Q \quad \text{(logo, } Q\text{ é verdadeira)}
\end{aligned}
$$

Repare na mecânica: a primeira premissa é uma **condicional** — uma relação do tipo "se...então". A segunda premissa **afirma** que o antecedente ($P$) é verdadeiro. A conclusão é inevitável: $Q$ também é verdadeira.

> [!important] Por que isso funciona?
> Lembre-se da analogia da [[Estruturas-Logicas#3.4 Condicional (→) — "SE... ENTÃO"|condicional como promessa]]. A única forma de uma condicional ser falsa é o antecedente ser verdadeiro e o consequente ser falso. Se sabemos que $P$ é verdadeira, então para a condicional $P \to Q$ ser verdadeira (que é nossa premissa), $Q$ **necessariamente** precisa ser verdadeira. Não existe saída lógica diferente.

> [!example] Exemplo com contexto de concurso
> **Premissa 1:** Se o candidato acerta todas as questões de lógica, então está na classificação final. ($P \to Q$)
> **Premissa 2:** O candidato acertou todas as questões de lógica. ($P$)
> **Conclusão:** Logo, o candidato está na classificação final. ($Q$)
>
> O raciocínio é direto: a condição ($P$) se realizou, portanto a consequência ($Q$) se realiza. É como apertar o botão certo: se o botão funciona, o resultado aparece.

> [!warning] Pegadinha clássica de prova: afirmação do consequente
> A banca adora inverter a lógica e apresentar o argumento assim:
>
> "Se o candidato acerta todas as questões de lógica, então está na classificação final. O candidato **está** na classificação final. Logo, acertou todas as questões de lógica."
>
> Isso é **inválido**! O candidato pode estar na classificação por outros motivos (notas altas em outras disciplinas, peso diferencial, etc.). Esse erro se chama **afirmação do consequente**:
>
> | Padrão | Estrutura | Válido? |
> |--------|-----------|---------|
> | **Modus Ponens** | $(P \to Q)$, $P$, $\therefore Q$ | ✅ Sim |
> | Afirmação do consequente | $(P \to Q)$, $Q$, $\therefore P$ | ❌ **Não** |
>
> **Dica de prova:** Ao ver um argumento do tipo "se...então", pergunte: **a segunda premissa está afirmando o que vem antes ou depois do "então"?** Se afirma o que vem **antes** (o antecedente), é Modus Ponens — válido. Se afirma o que vem **depois** (o consequente), é afirmação do consequente — inválido.

> [!example] Exercício: Condicional com hipótese falsa
> **Questão:** A seguinte afirmação é verdadeira ou falsa?
> "Se $2 + 2 = 5$, então a Terra é quadrada."
>
> **Resolução:**
> - $P$: "$2 + 2 = 5$" → **Falsa**
> - $Q$: "A Terra é quadrada" → **Falsa**
> - $P \to Q$ = **Verdadeira**
>
> **Explicação:** Quando a hipótese ($P$) é falsa, a condicional é **sempre verdadeira**, independente do consequente. Não caia na tentação de julgar a afirmação como falsa pelo conteúdo absurdo do consequente.

### 5.3 Modus Tollens (negação do consequente)

Agora vamos inverter a situação. Volte à mesma promessa:

> Se **chover hoje**, eu **levarei guarda-chuva**.

Mas desta vez, responda: você me viu **sem** guarda-chuva no final do dia. O que isso te diz sobre o clima?

Se eu **não levei** guarda-chuva, e minha promessa era válida, então **não pode ter chovido**. Porque se tivesse chovido, eu teria levado — era uma promessa! A ausência do consequente (guarda-chuva) revela a ausência do antecedente (chuva). Esse é o **Modus Tollens**: o padrão lógico que funciona pelo raciocínio contrário.

A estrutura formal é:

$$
\begin{aligned}
&P \to Q \quad \text{(se } P\text{, então } Q\text{)} \\
&\neg Q \quad \text{(não } Q\text{)} \\
&\therefore \; \neg P \quad \text{(logo, não } P\text{)}
\end{aligned}
$$

> [!important] Por que isso funciona?
> Lembre-se: a condicional $P \to Q$ só é falsa em um caso — quando $P$ é verdadeira e $Q$ é falsa. Agora, se sabemos que $Q$ é **falsa** ($\neg Q$), e a condicional $P \to Q$ é **verdadeira** (nossa premissa), então $P$ **não pode** ser verdadeira. Porque se $P$ fosse verdadeira, teríamos $P$ = V e $Q$ = F, o que faria a condicional ser falsa — contradizendo nossa premissa.
>
> Pense assim: **Modus Tollens é o teste da promessa quebrada.** Se a consequência não aconteceu, a condição não pode ter acontecido — porque, se tivesse, a consequência teria obrigatoriamente ocorrido.

> [!example] Exemplo com contexto de concurso
> **Premissa 1:** Se o candidato estuda todos os dias, então passa na prova objetiva. ($P \to Q$)
> **Premissa 2:** O candidato **não passou** na prova objetiva. ($\neg Q$)
> **Conclusão:** Logo, o candidato **não estudou** todos os dias. ($\neg P$)
>
> O raciocínio funciona porque a promessa era clara: estudar todos os dias garantiria a aprovação. Se a aprovação não veio, algo falhou na condição — e nesse caso, a condição era "estudar todos os dias". O candidato pode ter estudado, mas faltou disciplina em alguns dias.

> [!tip] Conexão com o Modus Ponens
> Repare que o Modus Tollens é o "espelho" do Modus Ponens. Enquanto o Ponens **afirma** o antecedente para chegar à conclusão, o Tollens **nega** o consequente para negar o antecedente. São dois lados da mesma moeda lógica — e ambos são **válidos**. Veremos essa relação lado a lado na seção abaixo.

> [!warning] Pegadinha clássica de prova: negação do antecedente
> A banca pode apresentar o argumento assim:
>
> "Se o candidato estuda todos os dias, então passa na prova. O candidato **não estudou** todos os dias. Logo, **não passou**."
>
> Isso é **inválido**! O candidato pode não ter estudado todos os dias e ainda assim passar — talvez já tivesse uma base sólida, ou a prova foi mais fácil que o esperado. Esse erro se chama **negação do antecedente**:
>
> | Padrão | Estrutura | Válido? |
> |--------|-----------|---------|
> | **Modus Tollens** | $(P \to Q)$, $\neg Q$, $\therefore \neg P$ | ✅ Sim |
> | Negação do antecedente | $(P \to Q)$, $\neg P$, $\therefore \neg Q$ | ❌ **Não** |
>
> **Dica de prova:** Ao ver uma negação na segunda premissa, verifique **o que está sendo negado**. Se é o consequente (o que vem depois do "então"), é Modus Tollens — válido. Se é o antecedente (o que vem antes do "então"), é negação do antecedente — inválido.

### 5.4 Comparação: Ponens vs Tollens

Agora que entendemos cada um isoladamente, vamos colocá-los lado a lado para fixar a relação entre eles. Pense no Modus Ponens e no Modus Tollens como **irmãos gêmeos**: nascem da mesma condicional ($P \to Q$), mas seguem direções opostas.

| | **Modus Ponens** | **Modus Tollens** |
|---|---|---|
| **Nome** | Afirmação do antecedente | Negação do consequente |
| **Premissa 1** | $P \to Q$ | $P \to Q$ |
| **Premissa 2** | $P$ (afirma o antecedente) | $\neg Q$ (nega o consequente) |
| **Conclusão** | $\therefore Q$ | $\therefore \neg P$ |
| **Analogia** | "Choveu → levei guarda-chuva" | "Não levei → não choveu" |
| **Mecanismo** | A condição se cumpre, logo a promessa vale | A consequência não veio, logo a condição falhou |
| **Válido?** | ✅ Sim | ✅ Sim |

> [!tip] Regra mnemotécnica para decorar
> Lembre-se da frase: **"Ponens afirma, Tollens nega."**
>
> - **Ponens** → **P**rova com **P**ositivo: afirma o que vem **antes** do "então"
> - **Tollens** → **T**ira com **T**roca: nega o que vem **depois** do "então"
>
> Ou, de forma ainda mais direta: **se a premissa bate com a condicional (ambas na mesma direção), é Ponens. Se a premissa vai contra a direção da condicional, é Tollens.**

> [!warning] Os quatro padrões que a banca cobra
> Aproveite esta seção para fixar **todos** os padrões de uma vez:
>
> | Padrão | Estrutura | Válido? |
> |--------|-----------|---------|
> | **Modus Ponens** | $(P \to Q)$, $P$, $\therefore Q$ | ✅ Sim |
> | **Modus Tollens** | $(P \to Q)$, $\neg Q$, $\therefore \neg P$ | ✅ Sim |
> | Afirmação do consequente | $(P \to Q)$, $Q$, $\therefore P$ | ❌ **Não** |
> | Negação do antecedente | $(P \to Q)$, $\neg P$, $\therefore \neg Q$ | ❌ **Não** |
>
> **Estratégia de prova:** Quando a questão apresentar um argumento, identifique primeiro a **condicional** (se...então), depois veja o que a segunda premissa faz — **afirma ou nega? O antecedente ou o consequente?** Com essas duas perguntas, você sempre chega ao padrão correto.

### 5.5 Construindo argumentos a partir de um enunciado

Em provas, é comum receber um texto e pedir para **identificar** as premissas e a conclusão, ou **reconstruir** o argumento na forma formal.

**Passo a passo para montar um argumento:**

1. **Identifique as proposições** — separar o enunciado em frases declarativas
2. **Ressalte as palavras indicadoras** — "logo", "portanto", "conclui-se que", "assim", "decorre que" sinalizam a **conclusão**; "porque", "visto que", "já que", "dado que" sinalizam **premissas**
3. **Atribua variáveis** — represente cada proposição com uma letra
4. **Reescreva com conectivos** — substitua "e", "ou", "se...então" pelos símbolos lógicos

> [!example] Exercício passo a passo
> **Enunciado:** "Todo candidato que estuda lógica tem vantagem na prova, porque a prova cobra muito lógica, e quem tem vantagem na prova aumenta suas chances."
>
> 1. **Proposições:**
>    - **$P$**: "Estuda lógica"
>    - **$Q$**: "Tem vantagem na prova"
>    - **$R$**: "Aumenta suas chances"
>
> 2. **Reescrevendo com conectivos:**
>    - Premissa 1: $P \to Q$ (quem estuda lógica tem vantagem)
>    - Premissa 2: $Q \to R$ (quem tem vantagem aumenta chances)
>    - Conclusão: $P \to R$ (quem estuda lógica aumenta suas chances)
>
> 3. **Validação:** Esse encadeamento é válido — veremos mais sobre deduções em cadeia no tópico [[Logica-de-Argumentacao]].

### 5.6 Argumentos compostos com múltiplos conectivos

Na prática, argumentos raramente usam um único conectivo. É comum encontrar proposições que misturam "e", "ou" e "se...então" na mesma frase.

> [!important] Regra de leitura
> Ao decompor uma frase complexa em proposições, leia **da esquerda para a direita**, identificando **primeiro** os conectivos de maior precedência:
>
> 1. $\neg$ (negação) — maior precedência
> 2. $\land$ e $\lor$ (conjunção e disjunção) — **mesma precedência** (avaliados da esquerda para a direita)
> 3. $\to$ (condicional)
> 4. $\leftrightarrow$ (bicondicional) — menor precedência
>
> Isso evita erros de interpretação em expressões como:
> $P \lor Q \to R \land S$
> que se lê como: $(P \lor Q) \to (R \land S)$, e **não** como $P \lor (Q \to R) \land S$.

> [!tip] Associatividade dos conectivos
> Os conectivos $\land$ e $\lor$ são **associativos** — $(P \land Q) \land R$ equivale a $P \land (Q \land R)$. O mesmo vale para $\lor$.
>
> Já a condicional **não** é associativa — $(P \to Q) \to R$ **não** equivale a $P \to (Q \to R)$. Por isso, o parênteses importa quando múltiplas condicionais aparecem juntas.

---

## 6. Resumo e pontos-chave para revisão

> [!tip] Checklist de revisão
> - [ ] Uma **proposição** é um enunciado declarativo com valor de verdade **definido** (V ou F)
> - [ ] Perguntas, ordens, exclamações e enunciados com variáveis livres **não** são proposições
> - [ ] Uma **proposição simples** não contém conectivos lógicos — representa uma unidade mínima ($P$, $Q$, $R$)
> - [ ] Uma **proposição composta** une duas ou mais simples com conectivos ($P \land Q$, $P \to Q$, etc.)
> - [ ] Para identificar se é composta, procure conectivos: "e", "ou", "se...então", "se e somente se", "não" formal
> - [ ] O "não" na linguagem natural nem sempre indica composição — analise se ele se aplica sobre uma proposição existente
> - [ ] $\neg P$ (negação): inverte o valor
> - [ ] $P \land Q$ (conjunção / E): verdadeiro só se **ambos** forem verdadeiros
> - [ ] $P \lor Q$ (disjunção / OU inclusivo): falso só se **ambos** forem falsos
> - [ ] $P \oplus Q$ (disjunção exclusiva / XOR): verdadeiro só se **exatamente um** for verdadeiro (iguais dão F); equivale a $\neg(P \leftrightarrow Q)$
> - [ ] $P \to Q$ (condicional / se...então): falso **só** quando $P$ = V e $Q$ = F
> - [ ] $P \leftrightarrow Q$ (bicondicional / se e somente se): verdadeiro quando **ambos iguais**
> - [ ] **Modus Ponens:** $(P \to Q)$, $P$, $\therefore Q$ → **Válido**
> - [ ] **Modus Tollens:** $(P \to Q)$, $\neg Q$, $\therefore \neg P$ → **Válido**
> - [ ] **Afirmação do consequente:** $(P \to Q)$, $Q$, $\therefore P$ → **Inválido**
> - [ ] **Negação do antecedente:** $(P \to Q)$, $\neg P$, $\therefore \neg Q$ → **Inválido**

> [!warning] O erro mais comum em prova
> Confundir o "ou" lógico (inclusivo) com o "ou" cotidiano (que muitas vezes é exclusivo). Na lógica formal, **"P OU Q" é verdadeiro mesmo quando P e Q são ambos verdadeiros**. A banca conta com essa confusão para montar alternativas atraentes mas incorretas.

---

## Próximos passos

Este tópico é a fundação. Os próximos tópicos deste bloco expandem esses conceitos:

- [[Logica-de-Argumentacao]] — analogias, inferências (dedutivas, indutivas, abdutivas) e deduções em cadeia
- [[Logica-Sentencial]] — tabelas-verdade, equivalências lógicas (Leis de De Morgan) e diagramas de Venn
- [[Logica-de-Primeira-Ordem]] — quantificadores, predicados e variáveis
- [[Raciocinio-Matematico-Aplicado]] — problemas aritméticos, geométricos, matriciais e progressões

Cada um desses tópicos usa os conceitos de proposições e conectivos como base. Domine-os agora para que o restante flua naturalmente.
