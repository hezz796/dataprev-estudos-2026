# Normalização

> [!info] Metadados
> **Disciplina:** Banco de Dados
> **Bloco:** 3.1 — Banco de Dados (FASE 3 — Infraestrutura de Dados)
> **Tópico:** 2. Normalização
> **Subtópicos:** Formas normais (1FN, 2FN, 3FN, BCNF) · Dependências funcionais · Decomposição e perda de informação · Anomalias de atualização
> **Pré-requisitos:** [[Fundamentos-e-Modelagem]] (entidade, atributo, relacionamento, chaves primárias e estrangeiras), [[Raciocinio-Matematico-Aplicado|Raciocínio Lógico Matemático]] (conjuntos, funções, transitividade) e [[LGPD-Lei-Geral-de-Protecao-de-Dados|Legislação/Segurança]] (privacidade, qualidade dos dados, dados sensíveis)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-28

---

## 1. Por que estudar normalização?

Na [[Fundamentos-e-Modelagem]], você aprendeu a construir o modelo lógico: entidades viram tabelas, relacionamentos viram chaves estrangeiras, e a integridade referencial garante que um pedido não aponte para um cliente inexistente. Mas o modelo lógico produzido ali pode ser **bom no desenho e ruim no projeto**: basta uma única tabela que misture dados de naturezas diferentes para aparecerem repetição, inconsistência e até perda de informação.

A **normalização** é a disciplina que responde a duas perguntas: *como saber se uma tabela está bem projetada?* e *como transformar uma tabela mal projetada em várias tabelas bem projetadas?* Ela foi proposta por **Edgar Codd**, o mesmo criador do modelo relacional — o que faz dela não um enfeite, mas uma parte estrutural da teoria relacional.

A ementa do DATAPREV tem um aviso explícito: *"Normalização é alvo frequente de questões — praticar com exercícios de decomposição."* Ou seja: a FGV não cobra apenas definições decoradas; ela cobra **raciocínio sobre dependências e decomposição**. Por isso, esta nota termina com dois exemplos resolvidos, passo a passo — um até a 3FN e outro até a BCNF — e você deve refazê-los sozinho, de olhos fechados para a solução, até o processo virar automático.

Há ainda uma ponte com a Fase 1 que vale registrar: a [[LGPD-Lei-Geral-de-Protecao-de-Dados|LGPD]] lista, entre os princípios do tratamento de dados (art. 6º), o da **qualidade dos dados** — os dados devem ser exatos, claros, relevantes e atualizados. Uma tabela não normalizada dificulta exatamente isso: o mesmo produto com três grafias diferentes, o telefone antigo do cliente repetido em vinte pedidos. Normalizar é, também, uma exigência de conformidade.

---

## 2. O problema: anomalias de atualização

Comecemos pelo exemplo que vamos carregar pela nota. A loja da nota anterior decidiu, por preguiça de modelar, registrar tudo em uma **tabela única** de vendas:

**VENDA**

| cod_venda | cod_produto | nome_produto | preco_produto | cod_cliente | nome_cliente | cidade_cliente | uf_cliente | data_venda | quantidade |
|---|---|---|---|---|---|---|---|---|---|
| 501 | 7 | Teclado mecânico | 320,00 | 1 | Ana Souza | Recife | PE | 2026-08-10 | 1 |
| 502 | 9 | Mouse sem fio | 95,00 | 2 | Bruno Lima | Olinda | PE | 2026-08-11 | 2 |
| 503 | 7 | Teclado mecânico | 320,00 | 1 | Ana Souza | Recife | PE | 2026-08-12 | 1 |
| 504 | 9 | Mouse sem fio | 95,00 | 1 | Ana Souza | Recife | PE | 2026-08-13 | 1 |
| 505 | 15 | Monitor 24 polegadas | 850,00 | 3 | Carla Dias | Olinda | PE | 2026-08-14 | 1 |

Parece inofensiva, mas observe: o nome do produto "Mouse sem fio" aparece **duas vezes**; o endereço da Ana aparece **três vezes**; o preço do teclado, **duas vezes**. Essa repetição é o sintoma — e as **anomalias de atualização** são a doença. São três tipos, e cada um vira questão:

- **Anomalia de inserção:** para cadastrar um produto novo que ainda não foi vendido (um "Monitor" que chegará amanhã), é preciso inventar um `cod_venda` e um `cod_cliente` que não existem — ou deixar essas colunas nulas, "fingindo" que houve uma venda. O mesmo vale para cadastrar um cliente que ainda não comprou: a tabela de vendas não é um lugar para clientes, mas é onde ele seria forçado a entrar.
- **Anomalia de exclusão:** se a venda 505 — a única venda do "Monitor 24 polegadas" — for excluída, o produto **some do sistema** junto com a venda. Para excluir uma venda, perdemos o produto; para manter o produto, não podemos excluir a venda. Um dado que só sobrevive enquanto outro existe é um dado mal projetado.
- **Anomalia de alteração:** para renomear "Mouse sem fio" para "Mouse sem fio recarregável", é preciso atualizar **todas** as linhas que contêm esse produto (502 e 504). Esqueceu uma? O sistema passa a exibir o mesmo produto com dois nomes diferentes — inconsistência silenciosa, a pior delas.

> [!question] Qual é a raiz do problema?
> Olhe as três anomalias juntas e pergunte: o que há de comum? A resposta é que a tabela **mistura dados de naturezas diferentes**: dados de *produto* (`nome_produto`, `preco_produto`), dados de *cliente* (`nome_cliente`, `cidade_cliente`, `uf_cliente`) e dados específicos da *venda* (`data_venda`, `quantidade`) — todos espremidos em uma só relação. Cada natureza repetida gera as anomalias. A normalização vai exatamente separar essas naturezas em tabelas próprias. E note o detalhe crucial: as anomalias não dependem dos *valores* — elas são consequência da **estrutura** da tabela.

> [!warning] PEGADINHA — o nome do fenômeno
> "Anomalia de atualização" não é um erro de digitação nem um `UPDATE` que falhou: é o **problema estrutural** que permite que uma inserção, uma exclusão ou uma alteração deixe o banco inconsistente. Na prova, a FGV descreve a situação ("para cadastrar X é preciso criar um Y falso") e pergunta qual anomalia é essa — a resposta está na *natureza do dado que é arrastado contra a vontade*.

---

## 3. Dependência funcional (DF)

Para consertar o projeto, precisamos de uma linguagem para dizer *quem determina quem*. Essa linguagem é a **dependência funcional**.

### 3.1 Definição

Dizemos que o atributo (ou conjunto de atributos) $X$ **determina funcionalmente** o atributo (ou conjunto) $Y$ — e escrevemos:

$$X \to Y$$

se, **para qualquer estado da relação**, cada valor de $X$ está associado a **exatamente um** valor de $Y$. Em outras palavras: *sabendo o valor de $X$, eu sei o valor de $Y$*. "Saber o CPF me diz o nome do cliente" é $cpf \to nome$; "saber o código do produto me diz o preço" é $cod\_produto \to preco\_produto$.

> [!note] A pergunta que identifica uma DF
> *"Dado um valor de X, o valor de Y é sempre o mesmo?"* Se sim, $X \to Y$. Se para o mesmo X podem existir vários Y diferentes, **não** é dependência funcional. Ex.: na tabela VENDA, `cidade_cliente \to uf_cliente` vale (cada cidade tem uma UF); `cidade_cliente \to nome_cliente` não vale (muitos clientes na mesma cidade).

Uma DF é **trivial** quando $Y$ é um subconjunto de $X$ (ex.: $\{cod\_venda\} \to cod\_venda$); dizemos que ela **não é trivial** quando $Y$ não está contido em $X$. As dependências que interessam à normalização são as **não triviais**.

### 3.2 Dependência parcial e dependência transitiva

Dentro de uma relação, duas "doenças" de dependência aparecem quando a chave é composta:

- **Dependência parcial:** acontece quando um atributo **não chave** depende de **parte** da chave (e não da chave inteira). Na VENDA, a chave é composta — $\{cod\_venda, cod\_produto\}$ —, mas $cod\_produto \to nome\_produto$ depende apenas de `cod_produto`: o nome do produto está "parcialmente" amarrado à chave. Essa é a doença que a **2FN** cura.
- **Dependência transitiva:** acontece quando $X \to Z$ vale porque $X \to Y$ e $Y \to Z$, com $Y$ sendo um atributo **não chave**. Na VENDA, temos $cod\_cliente \to cidade\_cliente$ e $cidade\_cliente \to uf\_cliente$ — logo $cod\_cliente \to uf\_cliente$ **transitivamente**. Essa é a doença que a **3FN** cura.

Repare na beleza da ponte com o [[Raciocinio-Matematico-Aplicado|RLM]] e a lógica: a dependência transitiva é a **propriedade transitiva** das relações — se *A* determina *B* e *B* determina *C*, então *A* determina *C*. Você já raciocinava assim com "se... então", na Fase 1; aqui, a mesma estrutura decide se uma tabela está bem projetada.

### 3.3 Determinante, fecho e chave candidata

O **determinante** de uma DF é o lado esquerdo: em $cod\_produto \to preco\_produto$, o atributo `cod_produto` é o determinante. Em uma relação, um conjunto $X$ de atributos é **superchave** se ele determina **todos** os atributos da relação; o **fecho** de $X$ — usualmente escrito $X^+$ — é o conjunto de todos os atributos que $X$ determina, direta ou indiretamente. E a **chave candidata** é uma superchave **mínima**: seu fecho é a relação inteira e nenhum subconjunto próprio faz o mesmo.

No exemplo da VENDA, o fecho de $\{cod\_venda, cod\_produto\}$ abrange todos os atributos — pelas DFs da seção 3.4 — e nenhum dos dois sozinho o faz: `cod_venda` não determina `nome_produto`, e `cod_produto` não determina `quantidade`. Logo, $\{cod\_venda, cod\_produto\}$ é a chave candidata (e será a chave primária). Guarde esse método: em questões de normalização, **achar as chaves candidatas a partir das DFs é o primeiro passo**. (Traduzir para exercício: dada uma lista de DFs, pergunte "qual conjunto mínimo determina tudo?")

### 3.4 As dependências da VENDA

Listemos formalmente as DFs do nosso exemplo — elas serão usadas nos exemplos resolvidos das seções 6 e 7:

$$
cod\_venda \to data\_venda,\ cod\_cliente
$$

$$
cod\_venda \to nome\_cliente,\ cidade\_cliente,\ uf\_cliente \quad \text{(via } cod\_cliente\text{)}
$$

$$
cod\_produto \to nome\_produto,\ preco\_produto
$$

$$
cod\_cliente \to nome\_cliente,\ cidade\_cliente
$$

$$
cidade\_cliente \to uf\_cliente
$$

$$
\{cod\_venda,\ cod\_produto\} \to quantidade
$$

As três primeiras linhas e as duas últimas, isoladas, já revelam as doenças: dependências **parciais** (`cod_produto \to nome_produto`, `cod_venda \to data_venda`) e dependência **transitiva** (`cod_cliente \to ... \to uf_cliente`).

---

## 4. Formas normais

Uma **forma normal** é um critério de qualidade do projeto. A relação está na forma normal $N$ se cumpre a condição de $N$ (e, por herança, as anteriores). Vamos do nível mais baixo ao mais alto.

### 4.1 Primeira Forma Normal (1FN)

Uma relação está na **1FN** se todos os **valores são atômicos** (indivisíveis) e **não existem grupos repetitivos** — ou seja, nenhuma coluna contém listas ou múltiplos valores, e nenhuma repetição de colunas do tipo "telefone1, telefone2, telefone3" esconde uma lista.

> [!example] Violação de 1FN — telefones múltiplos
> Um projeto tentador para CLIENTE seria: `CLIENTE(cod_cliente, nome, telefones)`, guardando em `telefones` algo como "81-99999-1234; 81-98888-5678". Isso **viola a 1FN** de duas formas: o valor não é atômico (contém dois números) e esconde um grupo repetitivo. O conserto é uma tabela própria:
>
> **TELEFONE** (PK composta: `cod_cliente` + `telefone`; FK: `cod_cliente` → CLIENTE)
>
> | cod_cliente | telefone |
> |---|---|
> | 1 | 81-99999-1234 |
> | 1 | 81-98888-5678 |
>
> A 1FN é o requisito mínimo de qualquer relação: **na prática, todo banco relacional já nasce na 1FN** — a FGV costuma cobrá-la em questões conceituais ("o que é valor atômico?") e em casos de colunas multivaloradas.

### 4.2 Segunda Forma Normal (2FN)

Uma relação está na **2FN** se está na **1FN** e **todo atributo não chave depende da chave inteira**, e não apenas de parte dela. A 2FN só tem o que consertar quando a chave é **composta** — pegadinha clássica: uma tabela com chave de um único atributo já está, automaticamente, na 2FN, pois não existe "parte" da chave para depender.

Na VENDA, `nome_produto` e `preco_produto` dependem de `cod_produto` (parte da chave); `data_venda` e `cod_cliente` dependem de `cod_venda` (outra parte). Todos são atributos **não chave** com dependência **parcial** → a VENDA **não está na 2FN**. A decomposição correta virá na seção 6.

### 4.3 Terceira Forma Normal (3FN)

Uma relação está na **3FN** se está na **2FN** e **nenhum atributo não chave depende transitivamente da chave** — isto é, nenhum atributo não chave depende de outro atributo não chave. Na VENDA, `uf_cliente` depende da chave apenas **através** de `cidade_cliente` (atributo não chave): é a dependência transitiva. Uma relação com chave única pode estar na 2FN e ainda assim violar a 3FN — por isso a 3FN é um patamar acima.

### 4.4 Forma Normal Boyce-Codd (BCNF)

A **BCNF** é a versão mais estrita da 3FN: a relação está na BCNF se, para **toda** dependência funcional **não trivial** $X \to Y$, o determinante $X$ é uma **superchave** da relação. A diferença em relação à 3FN é sutil e famosa: a 3FN admite uma exceção — uma DF $X \to Y$ com $X$ que **não** é superchave quando $Y$ é um **atributo primo** (faz parte de alguma chave candidata). A BCNF não admite exceção nenhuma.

A hierarquia entre as formas normais é de inclusão:

$$
\text{BCNF} \subset \text{3FN} \subset \text{2FN} \subset \text{1FN}
$$

Toda relação na BCNF está na 3FN; toda 3FN está na 2FN; toda 2FN está na 1FN. **A recíproca não vale** — e é aí que mora a pegadinha.

> [!warning] PEGADINHA — a hierarquia das formas normais
> "Se a relação está na 3FN, então está automaticamente na BCNF"? **Falso** — a BCNF é mais forte: pode haver 3FN sem BCNF (veremos o exemplo na seção 7). "Se está na 2FN, está na 1FN"? **Verdadeiro** — cada forma normal inclui as anteriores. A banca testa a direção da implicação; desenhe a cadeia de inclusão no rascunho antes de responder.

| Forma normal | Condição | O que conserta | Palavra-chave |
|---|---|---|---|
| **1FN** | valores atômicos, sem grupos repetitivos | atributos multivalorados/listas | atomicidade |
| **2FN** | 1FN + todo não chave depende da chave inteira | dependência parcial (chave composta) | chave inteira |
| **3FN** | 2FN + nenhum não chave depende de outro não chave | dependência transitiva | nada de transitividade |
| **BCNF** | toda DF não trivial tem determinante superchave | exceção do atributo primo da 3FN | determinante é superchave |

---

## 5. Decomposição e perda de informação

**Decompor** uma relação $R$ é substituí-la por duas ou mais relações $R_1, R_2, \dots$ cujos atributos, **unidos**, reproduzem os de $R$ (sem criar atributos novos). O objetivo é eliminar as anomalias; o risco é **perder informação** — e existe um critério preciso para saber se a decomposição é segura.

Uma decomposição tem **perda** (não é *lossless*) quando, ao recombinarmos as relações decompostas, obtemos linhas que **não existiam** na original — as chamadas **linhas espúrias**. A decomposição é **sem perda** (ou *lossless join*) quando a recombinação (a *junção natural* pelas colunas em comum) devolve **exatamente** a relação original. O critério que a banca cobra:

> [!important] Critério da decomposição sem perda
> Para uma decomposição em duas relações $R_1$ e $R_2$, a decomposição é **sem perda** se a **interseção** dos atributos de $R_1$ e $R_2$ é **chave candidata** (ou contém uma) de pelo menos uma das duas relações. Intuitivamente: as duas partes precisam "conversar" por uma coluna que identifique unicamente os registros de um dos lados — senão, ao juntar, tudo se combina com tudo.

> [!example] Decomposição com perda — passo a passo
> Considere a relação **EMPREGADO_PROJETO** `(CPF, projeto, horas)`, em que um funcionário trabalha em vários projetos e `horas` depende do par `(CPF, projeto)` — chave composta. Alguém propõe decompor em:
>
> **R1** `(CPF, projeto)` e **R2** `(CPF, horas)`
>
> Repare: a interseção é `CPF`, e `CPF` **não é chave** de nenhuma das duas (não identifica unicamente as tuplas de R1 nem de R2). Decomposição **com perda**. Veja os dados:
>
> | CPF | projeto | horas |
> |---|---|---|
> | 111 | A | 10 |
> | 111 | B | 20 |
> | 222 | A | 15 |
>
> Após a decomposição e a recombinação pela coluna `CPF`, surgem as linhas (111, A, **20**) e (111, B, **10**) — **linhas espúrias**, que não existiam na original. Perdeu-se a informação de quantas horas o funcionário dedicou a *cada* projeto: agora a tabela "sabe" apenas que 111 trabalhou em A e B com 10 ou 20 horas, em qualquer combinação. Um banco assim fabrica dados falsos silenciosamente.

Além da propriedade de *junção sem perda*, existe um segundo critério de qualidade: a decomposição deve **preservar as dependências funcionais** — ou seja, toda DF da relação original deve poder ser verificada dentro das relações decompostas (ou ser consequência lógica delas). Em projetos saudáveis, buscamos decomposições que sejam **sem perda E preservem dependências**. Um alerta que você verá na prática (e que a BCNF ilustra na seção 7): às vezes a BCNF só é alcançável abrindo mão da preservação de alguma dependência — e aí a banca cobra o conceito de que a 3FN "preserva mais" do que a BCNF.

---

## 6. Exemplo resolvido 1 — VENDA até a 3FN

Vamos aplicar tudo à tabela VENDA da seção 2. Este é o exercício que a ementa manda praticar: **decomposição completa, passo a passo, até a 3FN**.

**Dado inicial.** A relação VENDA `(cod_venda, cod_produto, nome_produto, preco_produto, cod_cliente, nome_cliente, cidade_cliente, uf_cliente, data_venda, quantidade)`, com as DFs da seção 3.4.

**Passo 0 — achar a chave.** O fecho de $\{cod\_venda, cod\_produto\}$ cobre todos os atributos; nenhum dos dois sozinhos cobre. Chave candidata: $\{cod\_venda, cod\_produto\}$.

**Passo 1 — 1FN.** Todos os valores são atômicos e não há grupos repetitivos: **a VENDA já está na 1FN**. (Se houvesse uma coluna "telefones" com lista, este seria o momento de criar a tabela TELEFONE, como na seção 4.1.)

**Passo 2 — ir à 2FN.** Pergunta: *existe atributo não chave dependente de parte da chave?* Sim:

- $cod\_produto \to nome\_produto,\ preco\_produto$ (determinante: parte da chave)
- $cod\_venda \to data\_venda,\ cod\_cliente$ (determinante: a outra parte)

Regra prática da 2FN: **retire cada porção da chave com seus dependentes e crie uma relação própria; o que sobra (a chave completa + atributos que dependem dela inteira) fica na relação central.** Resultado:

- **VENDA_1** `(cod_venda, data_venda, cod_cliente)` — dados da venda, dependentes de `cod_venda`;
- **VENDA_2** `(cod_produto, nome_produto, preco_produto)` — dados do produto, dependentes de `cod_produto`;
- **VENDA_3** `(cod_venda, cod_produto, quantidade)` — a relação central, com a chave completa e `quantidade`, que depende da chave inteira;
- **VENDA_4** `(cod_cliente, nome_cliente, cidade_cliente, uf_cliente)` — dados do cliente, dependentes de `cod_cliente` (que "sobrou" como atributo não chave de VENDA_1, mas vira chave de sua própria relação).

Todas as quatro estão na **2FN**: em cada uma, todo atributo não chave depende da chave inteira (e só dela).

**Passo 3 — ir à 3FN.** Pergunta: *existe atributo não chave dependente de outro não chave?* Olhe a VENDA_4: `cidade_cliente \to uf_cliente`, e `cidade_cliente` é um atributo **não chave** (a chave é `cod_cliente`). Logo, `uf_cliente` depende transitivamente da chave — **a VENDA_4 está na 2FN, mas não na 3FN**.

Regra prática da 3FN: **retire o "meio" da transitividade e transforme-o em chave de uma relação nova.** Como $cod\_cliente \to cidade\_cliente$ e $cidade\_cliente \to uf\_cliente$, separa-se:

- **VENDA_4a** `(cod_cliente, nome_cliente, cidade_cliente)`;
- **VENDA_4b** `(cidade_cliente, uf_cliente)` — a cidade vira chave, e a UF depende apenas dela.

**Resultado final (3FN):**

$$
\text{VENDA\_1 } (cod\_venda, data\_venda, cod\_cliente)
$$

$$
\text{VENDA\_2 } (cod\_produto, nome\_produto, preco\_produto)
$$

$$
\text{VENDA\_3 } (cod\_venda, cod\_produto, quantidade)
$$

$$
\text{VENDA\_4a } (cod\_cliente, nome\_cliente, cidade\_cliente)
$$

$$
\text{VENDA\_4b } (cidade\_cliente, uf\_cliente)
$$

**Verificação.** Em cada relação, toda DF não trivial tem como determinante a chave (2FN) e não há cadeia de dependência entre não chaves (3FN). As chaves estrangeiras foram construídas no caminho: `VENDA_1.cod_cliente → VENDA_4a.cod_cliente` e `VENDA_3.(cod_venda, cod_produto)` apontando para `VENDA_1` e `VENDA_2`. E a decomposição é **sem perda**: a cada passo, a interseção entre a parte retirada e o restante é chave de uma das partes (ex.: `VENDA_4` ∩ restante = `cod_cliente`, que é chave de `VENDA_4`; `VENDA_2` ∩ restante = `cod_produto`, chave de `VENDA_2`). Junte tudo pelas chaves e você obtém a VENDA original — sem linhas espúrias.

Revise o resultado à luz das anomalias da seção 2: agora o produto novo entra sem inventar venda (basta inserir em VENDA_2); o cliente novo entra em VENDA_4a sem venda; excluir a venda 505 não apaga o monitor; e renomear o mouse exige atualizar **uma** linha de VENDA_2, não duas. Todas as três anomalias desapareceram — esse é o teste prático de que a normalização funcionou.

---

## 7. Exemplo resolvido 2 — ENDERECO até a BCNF

Agora o caso que a 3FN **não** resolve sozinha. Considere a relação:

**ENDERECO** `(cidade, rua, cep)`

com as regras do mundo real:

- $cep \to cidade$ — um CEP identifica uma cidade;
- $\{cidade, rua\} \to cep$ — um endereço (cidade + rua) tem um CEP único.

**Passo 1 — chaves candidatas.** O fecho de $\{cidade, rua\}$ é a relação inteira ($\{cidade, rua\} \to cep$), e o par é mínimo. O fecho de $\{cep, rua\}$ também é a relação inteira: como $cep \to cidade$, o par determina `cidade` e, junto com `rua`, fecha o ciclo. Logo, há **duas chaves candidatas**: $\{cidade, rua\}$ e $\{cep, rua\}$. Escolhemos $\{cidade, rua\}$ como primária (a que "traduz" melhor a regra do negócio).

**Passo 2 — 3FN?** Atributos **primos** são aqueles que pertencem a alguma chave candidata: aqui, *todos* — `cidade`, `rua` e `cep` são primos. A 3FN exige que toda DF $X \to Y$ não trivial tenha $X$ superchave **ou** $Y$ primo. A DF $cep \to cidade$ tem $cep$ que não é superchave, mas `cidade` é primo: **a relação está na 3FN**. É exatamente a "exceção" que a 3FN admite.

**Passo 3 — BCNF?** A BCNF elimina a exceção: para *toda* DF não trivial $X \to Y$, $X$ deve ser superchave. Aqui, $cep \to cidade$ tem determinante `cep` que **não é superchave** (não determina a rua). Portanto: **3FN, mas não BCNF**.

> [!warning] PEGADINHA — 3FN sem BCNF só com atributo primo
> A situação que separa 3FN de BCNF sempre envolve uma DF cujo determinante não é superchave e cujo lado direito é um atributo **primo**. Se a banca afirmar "toda relação 3FN é BCNF", é falsa; se afirmar "uma relação sem atributos não primos está na 3FN", é verdadeira — mas isso **não** a coloca automaticamente na BCNF. O atributo primo é a brecha da 3FN, e a BCNF existe para fechá-la.

**Passo 4 — decompor.** Para eliminar a violação, retire o "vilão" $cep \to cidade$ em uma relação própria; o restante fica com `cep` como chave:

- **ENDERECO_CEP** `(cep, cidade)` — `cep` é a chave;
- **ENDERECO_RUA** `(cep, rua)` — `cep` é a chave.

**Verificação.** Na ENDERECO_CEP, a única DF não trivial é $cep \to cidade$, com `cep` superchave: **BCNF**. Na ENDERECO_RUA não há DF não trivial: **BCNF** (vacuamente). A decomposição é **sem perda**: a interseção entre as duas relações é `cep`, que é chave de **ambas**. Recombine pelas colunas em comum e a junção devolve exatamente a relação original, sem linhas espúrias.

> [!note] A nuance que a FGV pode explorar
> Note que a DF $\{cidade, rua\} \to cep$ **não** pode ser verificada dentro de uma única relação decomposta: é preciso juntar ENDERECO_CEP e ENDERECO_RUA para conferir se a rua naquela cidade tem o CEP certo. Ou seja, esta decomposição é **sem perda**, mas **não preserva todas as dependências** — um sacrifício típico da BCNF. Quando a prova perguntar "por que às vezes se prefere a 3FN à BCNF?", a resposta é: a 3FN (bem feita) sempre preserva dependências; a BCNF, nem sempre. Esse trade-off é o ponto mais fino do tópico — e o mais provável de diferenciar candidatos.

---

## 8. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **Anomalias**: inserção (dado precisa de "disfarce" para entrar), exclusão (dado some junto com outro), alteração (repetição exige múltiplas atualizações → inconsistência)
> - [ ] **DF**: $X \to Y$ = "sabendo X, sei Y"; determinante é o lado esquerdo; DF trivial quando $Y \subseteq X$
> - [ ] **Dependência parcial**: não chave depende de parte da chave composta → **2FN**
> - [ ] **Dependência transitiva**: não chave depende de outro não chave → **3FN**
> - [ ] **Chave candidata**: superchave mínima (fecho da relação; nenhum subconjunto próprio cobre tudo)
> - [ ] **1FN**: valores atômicos, sem grupos repetitivos (telefones múltiplos viram tabela própria)
> - [ ] **2FN**: depende da chave **inteira**; chave de um atributo ⇒ automaticamente 2FN
> - [ ] **3FN**: nada de transitividade; os "meios" (ex.: cidade) viram chaves de relações novas
> - [ ] **BCNF**: para toda DF não trivial, determinante é **superchave** — fecha a brecha do atributo primo
> - [ ] **Hierarquia**: BCNF ⊂ 3FN ⊂ 2FN ⊂ 1FN (a recíproca não vale)
> - [ ] **Sem perda (lossless)**: a interseção dos atributos da decomposição é chave de uma das partes; senão, surgem **linhas espúrias**
> - [ ] **Preservação de dependências**: toda DF deve ser verificável nas relações decompostas (a BCNF pode sacrificá-la)

> [!warning] O erro mais comum em prova
> Confundir **dependência parcial com transitiva** e esquecer que a **2FN só existe quando a chave é composta**. Na hora da questão, siga o roteiro: (1) liste as DFs do enunciado; (2) ache as chaves candidatas; (3) procure não chave dependente de *parte* da chave (2FN) e não chave dependente de *outro não chave* (3FN); (4) verifique se todo determinante é superchave (BCNF). Esse roteiro de quatro passos resolve a grande maioria dos exercícios de normalização — e a ementa manda: **pratique até virar reflexo.**

---

## 9. Próximos passos

Com a normalização, você fechou o desenho de dados do Bloco 3.1: o modelo lógico saiu da [[Fundamentos-e-Modelagem]] em forma de tabelas e chaves, e agora essas tabelas passaram pelo crivo das formas normais — sem anomalias, sem perda de informação, com dependências preservadas. Se quiser, revisite o modelo lógico da loja na seção 5.3 da nota anterior: ele já era 3FN? (Sim — e agora você sabe provar por quê.)

O próximo tópico da ementa é **SQL — DDL e DML**: chegou a hora de transformar os esquemas normalizados em comandos — criar tabelas com `CREATE`, definir chaves primárias e estrangeiras, inserir dados e consultá-los com `SELECT` e junções. As decisões que tomamos aqui (quais tabelas existem, quais colunas são chave) serão escritas em SQL quase literalmente. Em seguida, o bloco segue para **Transações e ACID** (a garantia de consistência sob concorrência), **NoSQL** (onde a normalização perde sentido — e você entenderá por quê) e **Big Data**.

A recomendação final vem da própria ementa do concurso: a normalização é **alvo frequente de questões** e exige prática de decomposição. Refaca os exemplos das seções 6 e 7 sem consultar a solução; depois invente uma tabela do seu dia a dia (uma planilha de gastos, uma agenda de consultas), liste as dependências e normalize-a até a 3FN. Esse exercício de vinte minutos transforma o conhecimento desta nota em reflexo de prova.