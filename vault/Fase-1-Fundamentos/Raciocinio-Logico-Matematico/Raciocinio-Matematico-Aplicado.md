# Raciocínio Matemático Aplicado

> [!info] Metadados
> **Disciplina:** Raciocínio Lógico Matemático
> **Bloco:** 1.2 — Raciocínio Lógico Matemático (FASE 1 — Fundamentos)
> **Tópico:** 5. Raciocínio matemático aplicado
> **Subtópicos:** Problemas aritméticos (porcentagem, regra de três, juros simples e compostos, média ponderada) · Problemas geométricos (áreas, volumes, semelhança e congruência) · Problemas matriciais (operações com matrizes, sistemas lineares elementares) · Sequências e progressões (PA e PG)
> **Pré-requisitos:** [[Estruturas-Logicas]], [[Logica-de-Argumentacao]], [[Logica-Sentencial]] e [[Logica-de-Primeira-Ordem]]
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-27

---

## 1. Por que estudar raciocínio matemático aplicado?

A [[Logica-de-Primeira-Ordem]] terminou com uma promessa que vamos cobrar agora: *"todo problema de porcentagem ou progressão é, no fundo, um enunciado a ser traduzido em estrutura precisa antes de ser calculado."* Esta nota é o acerto de contas com essa frase.

Nos quatro tópicos anteriores, você construiu a régua de interpretação: as **peças** do raciocínio — proposições, conectivos, precedência — ([[Estruturas-Logicas]]); a **avaliação** de argumentos, analogias e deduções em cadeia ([[Logica-de-Argumentacao]]); a **máquina de calcular** — tabelas-verdade, equivalências, De Morgan, diagramas de Venn — ([[Logica-Sentencial]]); e a **escrita precisa** de "todo/algum/nenhum" com predicados e quantificadores ([[Logica-de-Primeira-Ordem]]). Esse arsenal tem um destino prático imediato: **ler um enunciado, identificar o que é dado, o que é pedido e quais relações existem — e só então calcular.** O raciocínio matemático aplicado é exatamente isso: a lógica primeiro traduz a estrutura; a matemática depois executa o cálculo.

Veja como a tradução funciona na prática. Considere a frase: "**Todo** funcionário com mais de 5 anos de casa receberá um aumento de 10%." Você já sabe, pela lógica de primeira ordem, que isso é uma afirmação universal: $\forall x\,(Antiguidade(x) \to Aumento(x))$. O quantificador decide **quem entra no cálculo** — e o conectivo condicional decide **quando a regra dispara**. Para o funcionário que satisfaz a condição, o cálculo é um fator multiplicativo de $1,10$; para quem não satisfaz, a condicional é verdadeira por vacuidade e nada precisa ser calculado. Do mesmo modo, "**Se** o valor da compra ultrapassar R$ 1.000, **então** haverá desconto de 5%" é um `if` de programação disfarçado: a lógica diz quando a consequência vale, e a matemática diz quanto vale.

O senso crítico construído nos tópicos 1–4 também volta aqui com força. Na [[Logica-de-Primeira-Ordem]], aprendemos que "todo $A$ é $B$" não é simétrico e que a negação certa quase nunca é a que parece óbvia. Aplique essa desconfiança à aritmética: aumentar um preço em 10% e depois descontar 10% **não** o devolve ao valor original. A lógica já nos ensinou a desconfiar da simetria que "parece" natural; a seção 2.1 mostrará a conta: $1,10 \times 0,90 = 0,99$ — o preço final é 1% menor. A matemática aplicada não é uma coleção de fórmulas decoradas: é a consequência numérica das estruturas que você já domina.

> [!tip] Relevância para o Analista de TI
> O raciocínio proporcional treinado aqui move **estimativas de projeto** (esforço, prazo, tamanho relativo), **análise de indicadores** (variação percentual de métricas, médias ponderadas de tempos de resposta), **validação de regras de negócio** (descontos, prazos, limites) e o **pensamento estruturado** exigido para interpretar requisitos. Nada nesta nota depende de blocos futuros: apenas da lógica que você já estudou.

---

## 2. Problemas aritméticos

### 2.1 Porcentagem

#### O conceito: razão centesimal

**Porcentagem** é uma razão cujo denominador é 100:

$$p\% = \frac{p}{100}$$

Dizer "15% dos registros têm erro" é dizer que, em cada 100 registros, 15 têm erro. A palavra-chave é **razão**: porcentagem não é um número solto — é sempre uma proporção **em relação a um valor de referência**. Por isso, em prova, a primeira pergunta é sempre: *qual é o valor de referência?* "20% de desconto sobre o preço de tabela" refere-se ao preço de tabela; "20% sobre o preço já com desconto" refere-se a outra base. Identificar a base é metade da questão.

#### O fator multiplicativo: a ferramenta única

Em vez de calcular "primeiro a porcentagem, depois somar ou subtrair", o **fator multiplicativo** resolve tudo em uma multiplicação:

- aumento de $i\%$ → multiplicar por $(1 + i)$;
- desconto de $i\%$ → multiplicar por $(1 - i)$.

Se algo aumenta 25%, vira **1,25** vezes o original; se descontamos 25%, resta **0,75** do original. Os fatores mais comuns em prova:

| Operação | Fator multiplicativo | Operação | Fator multiplicativo |
|---|---|---|---|
| aumento de 1% | 1,01 | desconto de 1% | 0,99 |
| aumento de 5% | 1,05 | desconto de 5% | 0,95 |
| aumento de 10% | 1,10 | desconto de 10% | 0,90 |
| aumento de 20% | 1,20 | desconto de 20% | 0,80 |
| aumento de 25% | 1,25 | desconto de 25% | 0,75 |
| aumento de 50% | 1,50 | desconto de 50% | 0,50 |
| aumento de 100% | 2,00 | desconto de 100% | 0,00 |

Valem também as frações correspondentes: 10% = 1/10, 20% = 1/5, 25% = 1/4, 50% = 1/2, 75% = 3/4 — úteis para cálculo mental.

> [!example] Exemplo resolvido — aplicação direta do fator
> Um sistema passou de 400 requisições mensais para 500. Qual foi o aumento percentual?
>
> $$
> \begin{split}
> \text{variação percentual} &= \frac{V_f - V_i}{V_i} \times 100\% \\
> &= \frac{500 - 400}{400} \times 100\% \\
> &= \frac{100}{400} \times 100\% = 25\%
> \end{split}
> $$
>
> O aumento de 25% corresponde ao fator 1,25 — confirma: $400 \times 1,25 = 500$. Sempre que você calcular uma variação, confira multiplicando o valor inicial pelo fator para ver se chega no final.

#### Aumentos e descontos sucessivos: NUNCA somar percentuais

Aqui mora a regra de ouro da porcentagem: **aumentos e descontos sucessivos se multiplicam, não se somam.**

Pense: se uma mercadoria sofre um aumento de 20% e depois um desconto de 20%, o resultado é o preço original? Faça a conta com R$ 100: com o aumento, $100 \times 1,20 = 120$. O desconto de 20% incide sobre os **120** (o valor de referência mudou!): $120 \times 0,80 = 96$. O preço final é R$ 96 — houve **prejuízo de 4%**, não "empate". O fator combinado é $1,20 \times 0,80 = 0,96$.

O mesmo raciocínio vale para o exemplo clássico: aumentar 10% e descontar 10% não volta ao valor original:

$$1,10 \times 0,90 = 0,99 \quad \Rightarrow \quad \text{prejuízo de } 1\%$$

> [!warning] PEGADINHA — somar percentuais em vez de multiplicar fatores
> A banca apresenta: "Um produto sofreu aumento de 10% e, em seguida, desconto de 20%. Qual a variação total?" O candidato apressado responde "−10%". **Errado.** O correto é multiplicar os fatores: $1,10 \times 0,80 = 0,88$ → variação de **−12%**. Sempre que o enunciado disser **sucessivos**, **em seguida**, **depois de**, **sobre o novo valor**, desconfie: é multiplicação de fatores. E lembre a causa profunda: a segunda operação incide sobre uma **base diferente** — é o mesmo fenômeno do valor de referência que abre esta seção.

#### Porcentagem de porcentagem

"20% de 30% de um valor" não é 50% — é **6%**:

$$0,20 \times 0,30 = 0,06$$

Exemplo: 20% de 30% de R$ 200 = $0,06 \times 200 = 12$. O "de" da linguagem natural é a multiplicação das razões.

#### As palavras que mudam o cálculo

A interpretação — nossa velha amiga da lógica — decide a conta. Compare:

- "**X é 30% maior que Y**": $X = 1,30 \cdot Y$ (o fator multiplica);
- "**X corresponde a 30% de Y**": $X = 0,30 \cdot Y$ (a razão);
- "**diminuiu 30% em relação a**": fator $0,70$;
- "**voltou ao valor inicial após**": a pergunta é qual fator compensa o anterior (desconto que anula um aumento de 25% é $\frac{1}{1,25} = 0,80$, ou seja, 20% — pois $1,25 \times 0,80 = 1$).

### 2.2 Regra de três

#### O que é

A **regra de três** resolve problemas de **proporcionalidade** entre **duas grandezas** com três valores conhecidos e um desconhecido. A palavra-chave é **grandezas proporcionais** — e ela esconde a primeira pergunta da prova: a relação entre as grandezas é **direta** ou **inversa**?

**Diretamente proporcionais:** as duas crescem juntas (ou caem juntas) na mesma razão. Dobrou uma, dobra a outra. Exemplo: quantidade de metros de cabo e custo total.

**Inversamente proporcionais:** uma cresce e a outra cai, de modo que o **produto** permanece constante. Dobrou uma, a outra cai pela metade. Exemplo: velocidade média e tempo de viagem (distância fixa): $80 \times 3 = 240$ e $120 \times 2 = 240$ — o produto é sempre a distância.

#### Simples direta — exemplo resolvido

> 5 metros de cabo de rede custam R$ 40. Quanto custam 8 metros?

Mais cabo → mais custo: **direta**. Organize e monte a proporção:

$$\frac{x}{40} = \frac{8}{5} \quad \Rightarrow \quad x = \frac{40 \times 8}{5} = 64$$

Resposta: R$ 64. Confira o senso da proporcionalidade: 8/5 = 1,6; 64/40 = 1,6. A razão é constante.

#### Simples inversa — exemplo resolvido

> 4 pedreiros constroem um muro em 12 dias. Em quantos dias 6 pedreiros construiriam o mesmo muro?

Mais pedreiros → menos dias: **inversa**. Aqui não se monta a proporção "direta" — **inverte-se a razão**:

$$\frac{x}{12} = \frac{4}{6} \quad \Rightarrow \quad x = \frac{12 \times 4}{6} = 8$$

Resposta: 8 dias. O erro clássico é fazer $\frac{x}{12} = \frac{6}{4}$, o que daria 18 dias — absurdo, porque com mais gente o serviço não demora mais.

> [!tip] Método das setas para não errar
> 1. Monte a tabela com as duas grandezas e os valores conhecidos; a incógnita fica em uma linha.
> 2. Pergunte: *"se a grandeza conhecida aumenta, o que acontece com a incógnita?"*
> 3. **Direta**: mesma direção → monta a proporção diretamente. **Inversa**: direção contrária → inverte a razão antes de montar a proporção.

#### Regra de três composta — exemplo resolvido

Quando há **mais de duas grandezas**, isole a grandeza da incógnita e compare cada uma das outras com ela, aplicando o passo 2 do método das setas em cada comparação.

> 2 programadores, trabalhando 8 horas por dia, desenvolvem um sistema em 12 dias. Em quantos dias 4 programadores, trabalhando 6 horas por dia, desenvolveriam o mesmo sistema?

| Programadores | Horas/dia | Dias |
|---|---|---|
| 2 | 8 | 12 |
| 4 | 6 | x |

Compare **programadores** com **dias**: mais programadores → menos dias (**inversa**, razão invertida $\frac{2}{4}$). Compare **horas/dia** com **dias**: menos horas por dia → mais dias (**inversa**, razão invertida $\frac{8}{6}$). Monte:

$$x = 12 \times \frac{2}{4} \times \frac{8}{6} = 12 \times \frac{16}{24} = 8$$

Resposta: 8 dias. No caso de grandezas **diretas**, a razão entra **sem inverter** — a comparação segue sempre contra a grandeza da incógnita. Exemplo de conferência: se 4 máquinas produzem 600 peças em 8 horas, quantas peças produzem 6 máquinas em 6 horas? Mais máquinas → mais peças (**direta**, razão $\frac{6}{4}$); mais horas → mais peças (**direta**, razão $\frac{6}{8}$). Logo:

$$x = 600 \times \frac{6}{4} \times \frac{6}{8} = 600 \times \frac{36}{32} = 600 \times 1,125 = 675$$

Confira pelo outro caminho: 4 máquinas × 8 horas = 32 "máquina-horas" geram 600 peças; 6 máquinas × 6 horas = 36 máquina-horas; $600 \times \frac{36}{32} = 675$. As duas estradas fecham no mesmo número.

> [!warning] PEGADINHA — confundir inversa com direta
> A armadilha aparece em enunciados com "quanto mais ..., menos ..." disfarçado: "Quanto maior a equipe, menor o prazo", "quanto maior a velocidade, menor o tempo", "quanto mais operários, menos dias". A presença das palavras **menor**, **custar menos**, **mais rápido**, **menos tempo** não torna a grandeza "menor" — torna-a **inversa**. Outra armadilha: grandezas que crescem juntas por coincidência, mas **não são proporcionais** — idade e altura de uma criança crescem juntas por anos, mas não guardam razão constante; dobrar a idade não dobra a altura. **Proporcionalidade exige razão constante**, não apenas co-variação. A banca também usa o prisma da semelhança (seção 3.4): dobrar o lado de um quadrado quadruplica a área — área e lado crescem juntos, mas **não** são diretamente proporcionais; a razão não é constante.

### 2.3 Juros simples e compostos

#### Juros simples: juros só sobre o capital inicial

Nos **juros simples**, a taxa incide sempre sobre o **capital inicial** ($C$). Os juros ($J$) ao longo de $t$ períodos e o montante ($M$, capital + juros) são:

$$J = C \cdot i \cdot t$$

$$M = C + J = C(1 + i \cdot t)$$

A palavra-chave é **proporcional**: em juros simples, crescer 2% ao mês é crescer 12% em 6 meses — juros proporcionais ao tempo, sem "bola de neve".

> [!warning] PEGADINHA — taxa e tempo em unidades diferentes
> "Aplicou-se R$ 5.000 a 18% **ao ano** por **8 meses**." A taxa está ao ano; o tempo, em meses. **Antes de aplicar a fórmula, unifique as unidades**: $18\%$ a.a. = $1,5\%$ a.m. (basta dividir por 12, pois em juros simples a taxa é proporcional ao tempo). Então:
>
> $$J = 5.000 \times 0,015 \times 8 = 600 \quad \Rightarrow \quad M = 5.600$$
>
> Confira: R$ 600 de juros em 8 meses sobre R$ 5.000 — sentido correto. Quem esquece a conversão usa $0,18 \times 8$ e fabrica um absurdo de R$ 7.200 de juros.

#### Juros compostos: juros sobre juros

Nos **juros compostos**, a cada período a taxa incide sobre o **montante acumulado** — os juros do período passado passam a render juros. O montante é:

$$M = C(1 + i)^t$$

> [!example] Exemplo resolvido — composto passo a passo
> C = R$ 1.000, $i = 10\%$ a.m., $t = 3$ meses.
>
> $$
> \begin{split}
> M &= 1.000 \times (1,10)^3 \\
> &= 1.000 \times 1,10 \times 1,10 \times 1,10 \\
> &= 1.331
> \end{split}
> $$
>
> O rendimento total foi de R$ 331 — **mais** que os R$ 300 dos juros simples no mesmo período, porque o juro do 2º mês incidiu sobre 1.100, e o do 3º, sobre 1.210.

#### Comparação conceitual — o que a banca cobra

| Período | Simples (10% sempre sobre 1.000) | Composto (10% sobre o saldo) |
|---|---|---|
| 1 | 1.100 | 1.100 |
| 2 | 1.200 | 1.210 |
| 3 | 1.300 | 1.331 |
| 4 | 1.400 | 1.464,10 |

Observe: **no primeiro período, simples e composto coincidem** — porque ainda não há juros acumulados para render. A partir do segundo, o composto cresce mais — e a diferença aumenta com o tempo. Questão clássica de prova: "em juros compostos, a aplicação rende o mesmo que em simples no primeiro período?" Sim. Essa "igualdade no 1º período" é um ponto de partida para conferir contas e um alvo frequente de verdadeiro/falso.

#### Taxa proporcional × taxa equivalente

Duas noções que a banca adora confundir:

- **Taxas proporcionais** (juros simples): guardam a mesma razão dos tempos — 1% a.m. é proporcional a 12% a.a. **Em juros simples, taxas proporcionais são equivalentes de fato**: $1.000 \times (1 + 0,01 \times 12) = 1.120$ com as duas taxas, no mesmo prazo.
- **Taxas equivalentes** (juros compostos): produzem o mesmo montante no mesmo prazo — e aqui 1% a.m. **não** equivale a 12% a.a., pois o composto capitaliza mês a mês:

$$(1,01)^{12} - 1 \approx 0,1268 = 12,68\% \text{ a.a.}$$

> [!warning] PEGADINHA — confundir proporcional com equivalente
> Em juros compostos, "1% ao mês" **não** equivale a "12% ao ano": equivale a 12,68% ao ano. A banca cobra o conceito: em compostos, **trocar a taxa proporcionalmente é erro** — é preciso elevar à potência (cálculo de logaritmo, em geral, não é exigido em nível de concurso; a questão fica no conceito ou na potência simples). Outra pegadinha frequente: a pergunta "**quanto rendeu?**" pede $J$; a pergunta "**quanto ficou?**" pede $M$. Juros não é montante — $M = C + J$.

### 2.4 Média ponderada

#### Conceito e fórmula

A **média ponderada** é a média em que cada valor contribui com um **peso** (importância) diferente:

$$\bar{x} = \frac{\sum w_i \cdot x_i}{\sum w_i}$$

A **média simples** é o caso particular em que todos os pesos são iguais — e aí, e **somente aí**, as duas coincidem.

> [!example] Exemplo resolvido — o caso mais comum
> Um certame tem duas provas: a primeira vale peso 2 e a segunda vale peso 3. Um candidato tirou 7 na primeira e 9 na segunda. Qual a média final?
>
> $$
> \bar{x} = \frac{7 \times 2 + 9 \times 3}{2 + 3} = \frac{14 + 27}{5} = \frac{41}{5} = 8,2
> $$
>
> Note que a média simples seria $\frac{7+9}{2} = 8$ — diferente. O peso 3 da segunda prova "puxa" a média para cima.

#### O peso oculto — a pegadinha número 1

Muitas vezes o peso não vem numerado; ele está **escondido na quantidade**. O exemplo mais clássico:

> Em uma equipe, 10 desenvolvedores ganham R$ 4.000 e 30 ganham R$ 6.000. Qual o salário médio?

O peso de cada faixa é **quantas pessoas estão nela**. A média **não** é $\frac{4.000 + 6.000}{2} = 5.000$ — isso trataria as duas faixas como se tivessem o mesmo tamanho (portanto, erraria feio). A ponderação correta:

$$\frac{10 \times 4.000 + 30 \times 6.000}{10 + 30} = \frac{40.000 + 180.000}{40} = \frac{220.000}{40} = 5.500$$

O salário médio é R$ 5.500, puxado pela faixa mais populosa. Sempre que a questão falar em médias de grupos de **tamanhos diferentes**, pergunte: *qual é o peso de cada grupo?* — e pondere.

> [!warning] PEGADINHA — "média das médias" sem pesos
> "Uma turma A tem média 6 e uma turma B tem média 8. A média geral é 7?" **Não necessariamente.** Se a turma A tem 10 alunos e a B tem 30, a média geral é $\frac{10 \times 6 + 30 \times 8}{40} = \frac{60 + 240}{40} = 7,5$. A "média das médias" só vale com grupos de mesmo tamanho — e a banca raramente oferece esse luxo. Palavras-chave que indicam peso oculto: **número de**, **quantidade de**, **frequência**, **população**, **proporção**.

---

## 3. Problemas geométricos

### 3.1 Unidades e conversões — a pegadinha mais frequente

Antes das fórmulas, a conversão. Os três degraus:

- **Linear:** $1 \text{ m} = 100 \text{ cm}$; $1 \text{ km} = 1.000 \text{ m}$.
- **Área:** a razão linear **ao quadrado**. $1 \text{ m}^2 = 100 \times 100 = 10.000 \text{ cm}^2$; $1 \text{ km}^2 = 1.000.000 \text{ m}^2$.
- **Volume:** a razão linear **ao cubo**. $1 \text{ m}^3 = 1.000.000 \text{ cm}^3$.

E a ponte com o dia a dia: **$1 \text{ dm}^3 = 1 \text{ litro}$**. Como $1 \text{ m}^3 = 1.000 \text{ dm}^3$, então **$1 \text{ m}^3 = 1.000$ litros**; e $1 \text{ cm}^3 = 1 \text{ mL}$.

> [!warning] PEGADINHA — "1 m² = 100 cm²"? Errado!
> Quem converte pensando "1 m tem 100 cm, logo 1 m² tem 100 cm²" erra por um fator de 100. **Área** converte com o **quadrado** da razão (1 m² = 10.000 cm²); **volume**, com o **cubo** (1 m³ = 1.000.000 cm³). É a mesma lição da semelhança (seção 3.4): as dimensões lineares não se comportam como as de área ou volume.
>
> Exemplo resolvido: um piso de 3 m × 4 m tem 12 m². Em cm²: $12 \times 10.000 = 120.000$ cm². Ou, direto: $300 \times 400 = 120.000$ cm². Quem responde "1.200 cm²" caiu na pegadinha.
>
> E com água: uma caixa de 1 m × 1 m × 1 m = 1 m³ = **1.000 litros**, não 100 litros. A pergunta "quantos litros cabem?" é um convite para essa confusão — lembre que o litro é o dm³.

### 3.2 Áreas

As fórmulas de áreas são o núcleo do subtópico. Vale memorizar a tabela e, sobretudo, **as unidades** (sempre ao quadrado):

| Figura | Fórmula | Variáveis |
|---|---|---|
| Quadrado | $A = a^2$ | $a$ = lado |
| Retângulo | $A = b \cdot h$ | $b$ = base, $h$ = altura |
| Triângulo | $A = \dfrac{b \cdot h}{2}$ | $b$ = base, $h$ = altura |
| Círculo | $A = \pi r^2$ | $r$ = raio |
| Trapézio | $A = \dfrac{(B + b) \cdot h}{2}$ | $B$ = base maior, $b$ = base menor |
| Losango | $A = \dfrac{D \cdot d}{2}$ | $D$ = diagonal maior, $d$ = diagonal menor |

> [!example] Exemplo resolvido — área composta
> Um terreno tem a forma de um retângulo de 8 m × 5 m com um triângulo anexado de base 8 m e altura 3 m. Qual a área total?
>
> $$A_{total} = (8 \times 5) + \frac{8 \times 3}{2} = 40 + 12 = 52 \text{ m}^2$$
>
> A palavra-chave na hora de resolver: **decompor** — separar a figura em peças cujas fórmulas você conhece. E atenção ao trapézio: o erro clássico é esquecer de dividir por 2. No círculo, o erro clássico é usar o diâmetro no lugar do raio — $\pi r^2$ exige **raio**.

### 3.3 Volumes

| Sólido | Fórmula | Variáveis |
|---|---|---|
| Cubo | $V = a^3$ | $a$ = aresta |
| Paralelepípedo | $V = a \cdot b \cdot c$ | três arestas |
| Cilindro | $V = \pi r^2 h$ | $r$ = raio da base, $h$ = altura |
| Prisma | $V = A_{base} \cdot h$ | área da base × altura |
| Cone | $V = \dfrac{1}{3} \pi r^2 h$ | um terço do cilindro de mesma base e altura |
| Esfera | $V = \dfrac{4}{3} \pi r^3$ | $r$ = raio |

> [!example] Exemplo resolvido — volume e litros juntos
> Um reservatório cilíndrico tem raio da base 0,5 m e altura 2 m. Qual a capacidade em litros?
>
> $$V = \pi \times (0,5)^2 \times 2 = 0,5\pi \approx 1,57 \text{ m}^3$$
>
> Convertendo: $1,57 \text{ m}^3 = 1.570 \text{ dm}^3 = 1.570$ litros.
>
> Se a banca desse as medidas em **centímetros** (raio 50 cm, altura 200 cm), o volume sairia em cm³ e precisaria de duas conversões: $50^2 \cdot \pi \cdot 200 = 1.570.000 \text{ cm}^3 = 1.570 \text{ dm}^3 = 1.570 \text{ L}$. Repare como as unidades guiam o caminho.

### 3.4 Semelhança de figuras

Duas figuras são **semelhantes** quando têm a mesma forma e tamanhos proporcionais — uma é a "foto ampliada ou reduzida" da outra. A **razão de semelhança** $k$ é a razão entre medidas correspondentes: $\dfrac{a'}{a} = k$.

E aqui está a relação que sustenta as pegadinhas do subtópico:

- **Lados e medidas lineares**: multiplicam por $k$;
- **Áreas**: multiplicam por $k^2$;
- **Volumes**: multiplicam por $k^3$.

> [!warning] PEGADINHA — área e volume não escalam com $k$
> Se o lado de um quadrado dobra ($k = 2$), a área **quadruplica** ($k^2 = 4$), não dobra. Se a aresta de um cubo triplica ($k = 3$), o volume **multiplica por 27** ($k^3 = 27$), não por 3. A banca adora essa armadilha porque ela é a mesma da conversão de unidades: **as dimensões lineares, as áreas e os volumes se comportam em potências diferentes.**

> [!example] Exemplo resolvido — escala 1:50
> A planta de um salão está na escala 1:50 (cada 1 cm no desenho corresponde a 50 cm reais = razão $k = 50$). Uma sala desenhada com 6 cm × 4 cm tem dimensões reais $6 \times 50 = 300$ cm e $4 \times 50 = 200$ cm, ou seja, 3 m × 2 m. A área real:
>
> $$\text{área na planta} \times k^2 = (6 \times 4 \text{ cm}^2) \times 50^2 = 24 \times 2.500 = 60.000 \text{ cm}^2 = 6 \text{ m}^2$$
>
> Confira com a forma direta: $3 \text{ m} \times 2 \text{ m} = 6 \text{ m}^2$. Se a questão perguntasse o **volume** (altura da planta × largura × comprimento), o fator seria $k^3 = 125.000$.

### 3.5 Congruência

Duas figuras são **congruentes** quando têm a mesma forma **e** o mesmo tamanho — são exatamente iguais, uma sobrepondo a outra. Repare na relação com a semelhança: **congruência é uma semelhança com $k = 1$**. Se a razão de semelhança é 1, as medidas são idênticas.

No nível de concurso, o que importa são os **casos de congruência de triângulos** — as combinações mínimas de lados e ângulos que garantem que dois triângulos são idênticos:

| Caso | Condição |
|---|---|
| **LLL** (lado-lado-lado) | os três lados de um são iguais aos três lados do outro |
| **LAL** (lado-ângulo-lado) | dois lados iguais e o **ângulo entre eles** igual |
| **ALA** (ângulo-lado-ângulo) | dois ângulos iguais e o **lado entre eles** igual |

> [!example] Exemplo resolvido — a diagonal do quadrado
> Em um quadrado, a diagonal divide a figura em dois triângulos. Eles são congruentes pelo caso **LAL**: cada triângulo tem dois lados iguais (os lados do quadrado) e o ângulo entre eles igual (o ângulo reto de 90°). Conclusão prática: a diagonal divide o quadrado em duas metades idênticas — e cada metade tem 45° em cada canto.
>
> A palavra-chave em prova é **sobreposição**: se você consegue "encaixar" uma figura sobre a outra sem deformar, elas são congruentes. E cuidado com uma pegadinha típica: muitos candidatos acham que **LAA (lado-ângulo-ângulo)** não é caso de congruência — mas **é**! Dois ângulos conhecidos determinam o terceiro (a soma é 180°), e a situação reduz-se a ALA — daí o "L **A** L" e o "A **L** A" com as letras na ordem certa. O caso que **não** é garantia de congruência é o **LLA/A.LL** (dois lados e o ângulo **não compreendido** entre eles — o famoso caso ambíguo SSA). Fique com os três casos da tabela: LLL, LAL e ALA — e, se a banca citar LAA, lembre-se de que ele vale; se citar LLA, desconfie.

### 3.6 Teorema de Pitágoras — ferramenta de apoio (não é subtópico da ementa)

O **Teorema de Pitágoras** não está listado na ementa, mas é a ferramenta de apoio mais útil em problemas de área e volume — especialmente para encontrar alturas e diagonais. Em um triângulo retângulo de catetos $b$ e $c$ e hipotenusa $a$:

$$a^2 = b^2 + c^2$$

> [!example] Exemplo resolvido — diagonal como apoio
> A diagonal de um retângulo de 6 m × 8 m mede $d = \sqrt{6^2 + 8^2} = \sqrt{36 + 64} = \sqrt{100} = 10$ m. Sem esse resultado, metade dos problemas de área e volume ficaria sem a altura de que precisa. Os triângulos retângulos notáveis — 3-4-5, 5-12-13 e suas proporções — aparecem com frequência: reconhecê-los poupa cálculo (6-8-10 é o 3-4-5 dobrado).

---

## 4. Problemas matriciais

### 4.1 Notação: o que é uma matriz

Uma **matriz** é uma tabela retangular de números organizada em **linhas** e **colunas**. A **ordem** de uma matriz é $m \times n$ (lê-se "m por n"), com $m$ linhas e $n$ colunas. O elemento da **linha $i$** e **coluna $j$** é indicado por $a_{ij}$ — **linha primeiro, coluna depois**, sempre nessa ordem.

$$
A = \begin{pmatrix} a_{11} & a_{12} & a_{13} \\ a_{21} & a_{22} & a_{23} \end{pmatrix} \quad \text{é de ordem } 2 \times 3
$$

> [!example] Exemplo resolvido — localizar o elemento
> Seja
>
> $$A = \begin{pmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{pmatrix}$$
>
> A ordem de $A$ é $2 \times 3$. O elemento $a_{23}$ está na **linha 2, coluna 3**: vale 6. O elemento $a_{12}$ vale 2 (linha 1, coluna 2). Pegadinha frequente: inverter a ordem e ler $a_{23}$ como "coluna 2, linha 3" — que nem existe nesta matriz.

### 4.2 Operações

#### Adição e subtração

Só é possível **somar (ou subtrair) matrizes de mesma ordem** — a operação é feita elemento a elemento, posição a posição:

$$
\begin{pmatrix} 1 & 2 \\ 3 & 4 \end{pmatrix} + \begin{pmatrix} 5 & 6 \\ 7 & 8 \end{pmatrix} = \begin{pmatrix} 6 & 8 \\ 10 & 12 \end{pmatrix}
$$

> [!warning] PEGADINHA — somar matrizes de ordens diferentes
> Não existe soma de matriz $2 \times 3$ com matriz $2 \times 2$: as posições não correspondem. Questão de verdadeiro/falso adora essa pegadinha. A soma só existe quando as ordens coincidem — e o resultado mantém a mesma ordem.

#### Multiplicação por escalar

Multiplicar uma matriz por um número (escalar) é multiplicar **todos** os elementos por ele:

$$2 \times \begin{pmatrix} 1 & 2 \\ 3 & 4 \end{pmatrix} = \begin{pmatrix} 2 & 4 \\ 6 & 8 \end{pmatrix}$$

#### Multiplicação de matrizes: linha × coluna

A multiplicação $A \cdot B$ exige **compatibilidade**: o número de **colunas de $A$** deve ser igual ao número de **linhas de $B$**. Se $A$ é $m \times n$ e $B$ é $n \times p$, o produto $A \cdot B$ é $m \times p$ — os $n$ "do meio" se cancelam. Cada elemento $c_{ij}$ do produto é a soma dos produtos da **linha $i$ de $A$** com a **coluna $j$ de $B$**:

$$c_{ij} = a_{i1}b_{1j} + a_{i2}b_{2j} + \cdots + a_{in}b_{nj}$$

> [!example] Exemplo resolvido — o produto passo a passo
> Seja $A$ (ordem $2 \times 3$) e $B$ (ordem $3 \times 2$):
>
> $$A = \begin{pmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{pmatrix}, \qquad B = \begin{pmatrix} 7 & 8 \\ 9 & 10 \\ 11 & 12 \end{pmatrix}$$
>
> Compatíveis (colunas de $A$ = 3 = linhas de $B$). O produto é de ordem $2 \times 2$. O elemento $c_{11}$ (linha 1 de $A$ × coluna 1 de $B$):
>
> $$c_{11} = 1 \cdot 7 + 2 \cdot 9 + 3 \cdot 11 = 7 + 18 + 33 = 58$$
>
> Completo:
>
> $$A \cdot B = \begin{pmatrix} 58 & 64 \\ 139 & 154 \end{pmatrix}$$
>
> Confira o $c_{12}$: $1 \cdot 8 + 2 \cdot 10 + 3 \cdot 12 = 8 + 20 + 36 = 64$. ✓ E o $c_{21}$: $4 \cdot 7 + 5 \cdot 9 + 6 \cdot 11 = 28 + 45 + 66 = 139$. ✓

> [!warning] PEGADINHA — multiplicação de matrizes NÃO é comutativa
> $A \cdot B \neq B \cdot A$ em geral — e o pior: **$B \cdot A$ pode nem existir**. No exemplo acima, $A$ é $2 \times 3$ e $B$ é $3 \times 2$: $A \cdot B$ dá $2 \times 2$; mas $B \cdot A$ daria $3 \times 3$ (colunas de $B$ = 2 = linhas de $A$ — compatíveis) e os valores numéricos seriam **outros**. A banca pergunta: "a multiplicação de matrizes é comutativa?" Resposta: **não** — exceto em casos muito especiais. Fixe a noção: na hora da multiplicação, **a ordem importa**, ainda mais que na soma.

#### Transposta e identidade

A **matriz transposta** ($A^t$) troca linhas por colunas: $(A^t)_{ij} = a_{ji}$. Se $A$ é $m \times n$, $A^t$ é $n \times m$:

$$
A = \begin{pmatrix} 1 & 2 \\ 3 & 4 \\ 5 & 6 \end{pmatrix} \quad \Rightarrow \quad A^t = \begin{pmatrix} 1 & 3 & 5 \\ 2 & 4 & 6 \end{pmatrix}
$$

A **matriz identidade** ($I_n$) é a matriz quadrada de ordem $n$ com 1 na **diagonal principal** e 0 no restante. Ela é o **elemento neutro** da multiplicação: para matrizes quadradas, $A \cdot I = I \cdot A = A$ — o "1" das matrizes. (Para $A$ retangular $m \times n$, valem $A \cdot I_n = A$ e $I_m \cdot A = A$ — os neutros à direita e à esquerda são distintos.)

$$
I_2 = \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}
$$

### 4.3 Determinante

O **determinante** é um número associado a uma **matriz quadrada** (mesmo número de linhas e colunas) que resume propriedades importantes — a principal para nós: **se o determinante é diferente de zero, a matriz tem "solução única" nos sistemas** (seção 4.4).

#### Determinante de ordem 2: a pegadinha do sinal

Para $A = \begin{pmatrix} a & b \\ c & d \end{pmatrix}$:

$$\det(A) = a \cdot d - b \cdot c$$

> [!example] Exemplo resolvido
> $A = \begin{pmatrix} 3 & 4 \\ 2 & 5 \end{pmatrix}$: $\det(A) = 3 \cdot 5 - 4 \cdot 2 = 15 - 8 = 7$.
>
> > [!warning] PEGADINHA — o sinal dos termos cruzados
> > O produto **secundário** ($b \cdot c$) entra com **sinal negativo**. Esquecer o sinal (responder $15 + 8 = 23$) é o erro clássico. Fixe: **principal menos secundário**.

#### Determinante de ordem 3: Regra de Sarrus

Para $3 \times 3$, o método prático é a **Regra de Sarrus**: repita as duas primeiras colunas à direita, some os três produtos das diagonais "principais" e **subtraia** os três produtos das diagonais "secundárias".

$$
A = \begin{pmatrix} 1 & 2 & 3 \\ 2 & 0 & 1 \\ 1 & 1 & 2 \end{pmatrix}
$$

$$\det(A) = (1\!\cdot\!0\!\cdot\!2 + 2\!\cdot\!1\!\cdot\!1 + 3\!\cdot\!2\!\cdot\!1) - (3\!\cdot\!0\!\cdot\!1 + 1\!\cdot\!1\!\cdot\!1 + 2\!\cdot\!2\!\cdot\!2)$$

$$\det(A) = (0 + 2 + 6) - (0 + 1 + 8) = 8 - 9 = -1$$

O determinante pode ser **negativo** — não estranhe; o número é apenas o resultado algébrico.

### 4.4 Sistemas lineares elementares

Um **sistema linear** de duas equações e duas incógnitas ($2 \times 2$) é um conjunto de condições que devem valer **simultaneamente**. Por exemplo:

$$
\begin{cases}
x + y = 10 \\
x - y = 2
\end{cases}
$$

#### Resolver: o método da adição

Somar as duas equações elimina o $y$:

$$(x + y) + (x - y) = 10 + 2 \quad \Rightarrow \quad 2x = 12 \quad \Rightarrow \quad x = 6$$

Substitua em qualquer equação: $6 + y = 10 \Rightarrow y = 4$. A solução é o **par ordenado** $(6, 4)$.

#### Resolver: Regra de Cramer (2 × 2)

A **Regra de Cramer** usa determinantes. Para o sistema

$$
\begin{cases}
ax + by = e \\
cx + dy = f
\end{cases}
$$

com $D = \det\begin{pmatrix} a & b \\ c & d \end{pmatrix}$, temos $x = \dfrac{D_x}{D}$ e $y = \dfrac{D_y}{D}$, onde $D_x$ substitui a **coluna de $x$** pelos termos independentes e $D_y$ faz o mesmo com a **coluna de $y$**.

> [!example] Exemplo resolvido — Cramer no sistema acima
> $$D = \det\begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix} = 1\cdot(-1) - 1\cdot 1 = -2$$
> $$D_x = \det\begin{pmatrix} 10 & 1 \\ 2 & -1 \end{pmatrix} = 10\cdot(-1) - 1\cdot 2 = -12 \quad \Rightarrow \quad x = \frac{-12}{-2} = 6$$
> $$D_y = \det\begin{pmatrix} 1 & 10 \\ 1 & 2 \end{pmatrix} = 1\cdot 2 - 10\cdot 1 = -8 \quad \Rightarrow \quad y = \frac{-8}{-2} = 4$$
>
> Confere com o método da adição: $(6, 4)$. As duas estradas levam ao mesmo lugar — em prova, use a que for mais rápida e **confira substituindo na outra equação**.

#### Classificação: SPD, SPI e SI

A palavra-chave da classificação é **quantas soluções** o sistema admite, e o atalho da prova é o **determinante da matriz dos coeficientes** ($D$):

| Classificação | Significado | Critério rápido |
|---|---|---|
| **SPD** — sistema possível e **determinado** | **uma única** solução (par ordenado único) | $D \neq 0$ |
| **SPI** — sistema possível e **indeterminado** | **infinitas** soluções (as equações dizem a mesma coisa) | $D = 0$ e equações proporcionais entre si |
| **SI** — sistema **impossível** | **nenhuma** solução (as equações se contradizem) | $D = 0$ e equações inconsistentes |

Exemplos do mesmo tamanho:

- $x + y = 5$ e $2x + 2y = 10$ → a segunda é a primeira multiplicada por 2: dizem a mesma coisa, qualquer ponto da reta resolve → **SPI**.
- $x + y = 5$ e $2x + 2y = 12$ → se $x + y = 5$, então $2(x + y) = 10$, nunca 12 → contradição → **SI**.

> [!important] Conexão com a lógica: o sistema é um "E"
> Resolver o sistema é encontrar o par $(x, y)$ que torna **as duas** equações verdadeiras ao mesmo tempo — exatamente a **conjunção** da [[Logica-Sentencial]]. Se as equações são predicados $E_1(x,y)$ e $E_2(x,y)$, o sistema pede:
>
> $$E_1(x,y) \land E_2(x,y) = V$$
>
> O "E" é decisivo: um par que satisfaz só uma equação **não é solução** — a conjunção exige as duas. E a classificação é uma contagem do conjunto-solução: **exatamente um** (SPD), **infinitos** (SPI), **nenhum** (SI). A pergunta "o sistema é possível e determinado?" é, no fundo, a pergunta "existe uma única combinação que torna o E verdadeiro?" — quantificação existencial com unicidade, como o $\exists!$ que você viu em [[Logica-de-Primeira-Ordem]].

---

## 5. Sequências e progressões

### 5.1 Progressão aritmética (PA)

Uma **progressão aritmética** é uma sequência em que cada termo (a partir do segundo) é o anterior somado a uma constante — a **razão** $r$:

$$a_{n+1} = a_n + r \quad \Rightarrow \quad r = a_{n+1} - a_n$$

Exemplo: $2, 5, 8, 11, \dots$ é uma PA de razão $r = 3$.

#### Termo geral

O **termo geral** localiza qualquer termo sem percorrer a sequência:

$$a_n = a_1 + (n - 1) \cdot r$$

> [!warning] PEGADINHA — n ou n−1?
> O erro clássico é usar $n$ no lugar de $n - 1$: para o **10º** termo, somamos a razão **9 vezes** (do 1º ao 2º é 1 soma, do 1º ao 10º são 9). $a_{10} = a_1 + 9r$ — não $10r$. Pergunte sempre: *quantas razões separam o primeiro termo do termo procurado?* A resposta é sempre **um a menos** que a posição.

> [!example] Exemplo resolvido
> Na PA $2, 5, 8, \dots$, qual o 10º termo e a soma dos 10 primeiros?
>
> $$a_{10} = 2 + (10 - 1) \cdot 3 = 2 + 27 = 29$$
>
> A **soma dos $n$ primeiros termos** usa o primeiro e o último:
>
> $$S_n = \frac{n \cdot (a_1 + a_n)}{2} \quad \Rightarrow \quad S_{10} = \frac{10 \cdot (2 + 29)}{2} = \frac{310}{2} = 155$$

#### Termo médio e interpolação

Em três termos consecutivos de uma PA, o do meio é a **média aritmética** dos vizinhos:

$$a_m = \frac{a_{m-1} + a_{m+1}}{2}$$

**Interpolar** meios aritméticos é inserir termos entre dois extremos. Para inserir 4 meios entre 2 e 22, a sequência passa a ter **6 termos** (os 2 extremos + 4 meios): $22 = 2 + 5r \Rightarrow r = 4$. A PA interpolada é $2, 6, 10, 14, 18, 22$.

> [!tip] Como a banca costuma cobrar
> As palavras-chave de PA são **razão**, **termo geral**, **soma dos n primeiros**, **termo médio** e **interpolar/intercalar**. Palavras como "**em progressão aritmética**", "**sucessivamente**", "**mesma diferença**" indicam PA. E a conexão com a lógica já estudada: o termo geral é uma **afirmação universal** — "**para todo** $n$, o termo vale $a_1 + (n-1)r$" — e um único termo que não obedeça derruba a PA (um contraexemplo, como na negação do $\forall$).

### 5.2 Progressão geométrica (PG)

Uma **progressão geométrica** é uma sequência em que cada termo (a partir do segundo) é o anterior **multiplicado** por uma constante — a **razão** $q$:

$$a_{n+1} = a_n \cdot q \quad \Rightarrow \quad q = \frac{a_{n+1}}{a_n}$$

Exemplo: $3, 6, 12, 24, \dots$ tem razão $q = 2$.

#### Termo geral

$$a_n = a_1 \cdot q^{n-1}$$

> [!example] Exemplo resolvido
> Na PG $3, 6, 12, \dots$, o 5º termo:
>
> $$a_5 = 3 \cdot 2^{5-1} = 3 \cdot 2^4 = 3 \cdot 16 = 48$$

#### Termo médio: a média geométrica

Em três termos consecutivos de uma PG (positivos), o do meio satisfaz:

$$a_m^2 = a_{m-1} \cdot a_{m+1} \quad \Rightarrow \quad a_m = \sqrt{a_{m-1} \cdot a_{m+1}}$$

Exemplo: $2, x, 8$ em PG → $x^2 = 16 \Rightarrow x = 4$ (considerando termos positivos). Atenção: a média aritmética **não** vale aqui — é a **média geométrica**. E cuidado com a pegadinha do sinal: uma PG de razão **negativa** alterna os sinais ($3, -6, 12, -24, \dots$, com $q = -2$), e nesse caso $x = -4$ também é possível — o termo médio ao quadrado admite os dois sinais.

#### Soma dos termos

**Soma finita** (para $q \neq 1$):

$$S_n = \frac{a_1 \cdot (q^n - 1)}{q - 1}$$

Exemplo: $S_5$ da PG $3, 6, 12, 24, 48$: $S_5 = \frac{3(2^5 - 1)}{2 - 1} = 3 \cdot 31 = 93$ — confira somando à mão.

**Soma infinita** — e aqui a condição é tudo:

$$S_{\infty} = \frac{a_1}{1 - q}, \qquad \text{se } |q| < 1$$

> [!warning] PEGADINHA — esquecer a condição $|q| < 1$
> A fórmula da soma infinita **só existe** quando a razão está entre −1 e 1 (em módulo). Se $|q| \geq 1$, a soma **não converge** — cresce sem limite ($q > 1$) ou oscila ($q \le -1$) — e a fórmula não se aplica, pois daria um absurdo (denominador negativo ou nulo). A banca cobra a condição explicitamente: "uma PG infinita de razão 3 tem soma finita?" **Não.**
>
> Exemplo resolvido (a divisão ao meio): $8, 4, 2, 1, \frac{1}{2}, \dots$ tem $a_1 = 8$ e $q = \frac{1}{2}$:
>
> $$S_{\infty} = \frac{8}{1 - \frac{1}{2}} = \frac{8}{\frac{1}{2}} = 16$$
>
> Faz sentido: cada metade que sobra enche o caminho até 16.

### 5.3 Identificação de padrões — como atacar uma sequência desconhecida

A banca nem sempre anuncia que a sequência é PA ou PG; muitas vezes ela apresenta uma sequência mista e pergunta o próximo termo. O método de ataque (em ordem):

```text
Como atacar uma sequência desconhecida
        │
        ▼
1. Calcule as DIFERENÇAS entre termos consecutivos
        │
   ┌────┴─────────────────────┐
   ▼                          ▼
Diferenças constantes?      Não constantes?
   │ (PA: a_n = a₁+(n−1)r)     │
   ▼                          ▼
        │          2. Calcule as RAZÕES (termo ÷ anterior)
        │                    │
        │              ┌─────┴─────┐
        │              ▼           ▼
        │        Razões const.?  Não?
        │        (PG: a_n = a₁qⁿ⁻¹)│
        │                        ▼
        │            3. Olhe as 2ªs diferenças (dif. das dif.)
        │               const.? → padrão de 2º grau
        │                        ▼
        │            4. Procure ALTERNÂNCIA entre dois padrões
        │               (posições ímpares × pares)
        │                        ▼
        │            5. Procure RECORRÊNCIA (termo depende
        │               dos anteriores: ex. fibo: xₙ = xₙ₋₁ + xₙ₋₂)
        ▼
Nunca confie no padrão sem TESTAR pelo menos 2 transições
(ideal: 3) — um único contraexemplo derruba o chute
```

> [!example] Exemplo resolvido — sequência intercalada
> Qual o próximo termo de $2, 10, 4, 20, 6, 30, \dots$?
>
> As diferenças alternam: $+8, -6, +16, -14, +24, \dots$ — sem padrão direto. Então olhe **posições separadas**:
>
> - posições ímpares: $2, 4, 6, \dots$ → PA de razão $+2$ (próximo: 8);
> - posições pares: $10, 20, 30, \dots$ → PA de razão $+10$ (próximo: 40).
>
> Resposta: o próximo termo (7ª posição, ímpar) é **8**. A sequência intercala duas PAs. Palavra-chave da banca: **intercalada**, **alternada**, **intercalar**.

> [!example] Exemplo resolvido — multiplicações sucessivas
> $1, 2, 6, 24, 120, \dots$: as diferenças $1, 4, 18, 96$ não ajudam; as razões $2, 3, 4, 5$ revelam o padrão — $×2$, $×3$, $×4$, $×5$. Próximo termo: $120 \times 6 = 720$. (Essa é a sequência dos fatoriais: $1!, 2!, 3!, 4!, 5!$.)

> [!example] Exemplo resolvido — recorrência (Fibonacci)
> $1, 1, 2, 3, 5, 8, 13, \dots$: as diferenças $0, 1, 1, 2, 3, 5$ repetem a própria sequência deslocada — padrão de **recorrência**: cada termo é a soma dos dois anteriores. Próximo termo: $8 + 13 = 21$.

> [!warning] PEGADINHA — pressa em "chutar padrão"
> Com apenas três termos, quase qualquer chute "funciona". $1, 2, 4, \dots$ pode ser PG ($q = 2$, próximo = 8) **ou** PA de 2ª ordem pela regra das diferenças ($1, 2, 3, \dots$, próximo = 7) **ou** várias outras coisas. Por isso, **teste o padrão em pelo menos duas transições** (idealmente três) antes de responder. E lembre a lição de [[Logica-de-Primeira-Ordem]]: uma regra de sequência é uma afirmação universal — "o próximo termo **sempre** segue este padrão" — e **um único termo que não obedece é contraexemplo suficiente** para derrubá-la. A banca explora exatamente isso: a alternativa errada usa um padrão que só funciona nos dois primeiros passos.

---

## 6. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **Porcentagem**: $p\% = \frac{p}{100}$; aumento = $\times(1+i)$, desconto = $\times(1-i)$
> - [ ] **Sucessivos**: multiplicar fatores, **nunca somar** ($1,10 \times 0,90 = 0,99$ → −1%)
> - [ ] **Porcentagem de porcentagem**: 20% de 30% = **6%** (multiplicação das razões)
> - [ ] **Variação percentual**: $\frac{V_f - V_i}{V_i} \times 100\%$; "30% maior que" é $\times 1,30$, "30% de" é $\times 0,30$
> - [ ] **Regra de três**: direta (razões na mesma ordem); inversa (inverter a razão); composta (comparar cada grandeza com a incógnita)
> - [ ] **Juros simples**: $J = C \cdot i \cdot t$, $M = C(1 + i \cdot t)$ — taxa e tempo na **mesma unidade**
> - [ ] **Juros compostos**: $M = C(1+i)^t$; 1º período igual ao simples; "juros sobre juros"
> - [ ] **Taxa proporcional** (simples) ≠ **taxa equivalente** (composta): 1% a.m. ≈ 12,68% a.a. em compostos
> - [ ] **Média ponderada**: $\bar{x} = \frac{\sum w_i x_i}{\sum w_i}$; **peso oculto** = quantidade de elementos do grupo
> - [ ] **Conversões**: 1 m² = 10.000 cm²; 1 m³ = 1.000 L; 1 dm³ = 1 L (área/volume convertem com quadrado/cubo da razão)
> - [ ] **Áreas**: quadrado $a^2$, retângulo $b \cdot h$, triângulo $\frac{bh}{2}$, círculo $\pi r^2$, trapézio $\frac{(B+b)h}{2}$, losango $\frac{Dd}{2}$
> - [ ] **Volumes**: cubo $a^3$, paralelepípedo $abc$, cilindro $\pi r^2 h$, prisma $A_{base} \cdot h$, cone $\frac{1}{3}\pi r^2 h$, esfera $\frac{4}{3}\pi r^3$
> - [ ] **Semelhança**: $k$ nos lados, $k^2$ nas áreas, $k^3$ nos volumes
> - [ ] **Congruência**: LLL, LAL, ALA (casos de triângulos); congruência = semelhança com $k = 1$
> - [ ] **Pitágoras (apoio)**: $a^2 = b^2 + c^2$; ternos 3-4-5, 5-12-13
> - [ ] **Matrizes**: ordem $m \times n$; elemento $a_{ij}$ (linha, coluna); soma exige mesma ordem; $A \cdot B$ exige colunas de $A$ = linhas de $B$
> - [ ] **Multiplicação** é linha × coluna e **não é comutativa**; transposta troca linhas/colunas; identidade $I_n$ é o elemento neutro
> - [ ] **Determinante 2×2**: $a \cdot d - b \cdot c$ (atenção ao sinal); Sarrus para 3×3
> - [ ] **Sistemas**: $D \neq 0$ → SPD (solução única); $D = 0$ → analisar (SPI ou SI); Cramer: $x = \frac{D_x}{D}$
> - [ ] **PA**: $a_n = a_1 + (n-1)r$ **(o famoso n−1)**; $S_n = \frac{n(a_1 + a_n)}{2}$; termo médio = média aritmética
> - [ ] **PG**: $a_n = a_1 q^{n-1}$; termo médio = média geométrica ($a_m^2 = a_{m-1} a_{m+1}$); $S_\infty = \frac{a_1}{1-q}$ **só se $|q| < 1$**
> - [ ] **Sequências mistas**: olhar diferenças, razões, 2ªs diferenças, alternâncias, recorrências — e **testar o padrão em 2+ transições**

> [!warning] O erro mais comum em prova
> **Somar percentuais sucessivos em vez de multiplicar fatores.** "Aumento de 10% e desconto de 10%" **não** é "empate": é $1,10 \times 0,90 = 0,99$, prejuízo de 1%. Essa única confusão reaparece em descontos em cascata, reajustes de salário e variação de métricas — e é a favorita das questões de aritmética. O exercício mental que evita a pegadinha: sempre que houver **sucessivos**, **em seguida**, **sobre o novo valor**, escreva os fatores e **multiplique**; e sempre confira o resultado com um valor de teste (R$ 100 resolve).

---

## 7. Próximos passos

Com esta nota, o Bloco 1.2 — Raciocínio Lógico Matemático — está fechado, e com ele o tripé de fundamentos da FASE 1. Na [[Logica-de-Primeira-Ordem]], você fechou a caixa de ferramentas da lógica; aqui, você a usou para calcular: a lógica traduziu o enunciado, a matemática executou a conta, e o bom senso lógico conferiu o resultado — três movimentos que, juntos, resolvem a imensa maioria das questões de RLM.

A FASE 1 ainda tem dois blocos que podem ser estudados **em paralelo** com o que você acabou de ver: o 1.1 (Língua Portuguesa), que treina exatamente a mesma habilidade de interpretar enunciados com precisão, e o 1.3 (Legislação de Segurança da Informação e LGPD), cuja leitura de normas também se beneficia da estrutura "se...então" e das condições "todo/nenhum/algum" que agora você domina.

E a base construída aqui não fica na prateleira. O raciocínio proporcional e as progressões reaparecem em estimativas e métricas; as matrizes e os sistemas lineares voltam como ferramentas de modelagem; e a lógica que sustenta tudo — o "E" simultâneo dos sistemas, o "todo" dos padrões de sequência, o contraexemplo do teste de hipóteses — será a régua que você reutilizará nas fases seguintes, em Banco de Dados, Desenvolvimento de Sistemas, Testes e Segurança da Informação. Cada fase futura vai cobrar, disfarçadas de código, de consulta e de regra de negócio, as mesmas estruturas que este bloco estabeleceu. Você estará pronto para reconhecê-las — e para calculá-las.