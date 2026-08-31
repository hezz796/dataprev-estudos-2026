# Inteligência Artificial — Conceitos Fundamentais

> [!info] Metadados
> **Disciplina:** Atualidades e Inteligência Artificial
> **Bloco:** 2.2 — Atualidades e IA (FASE 2 — Linguagens e Acesso)
> **Tópico:** 2. Inteligência Artificial — Conceitos fundamentais
> **Subtópicos:** Definição de IA, ML e Deep Learning · Aprendizagem supervisionada, não-supervisionada e por reforço · Redes neurais (conceito geral) · Modelos generativos e LLMs · Prompt engineering (conceito básico)
> **Pré-requisitos:** [[Raciocinio-Matematico-Aplicado|Raciocínio Lógico Matemático]] e [[LGPD-Lei-Geral-de-Protecao-de-Dados|Legislação/LGPD]]
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-28

---

## 1. Por que estudar IA deste jeito?

Se você é iniciante, a primeira confusão é a mais comum de todas: *"IA, machine learning, deep learning, redes neurais, LLMs... tudo isso é a mesma coisa?"* A resposta é **não** — e saber distingui-los é exatamente o que a FGV cobra com mais insistência neste tópico. A ementa foi clara: para IA, **não é necessário domínio técnico profundo — o foco é conceitual e ético**. Ou seja, você não vai derivar fórmulas; vai entender *o que cada coisa é*, *como elas se relacionam* e *por que funcionam*.

A boa notícia: você já tem toda a base exigida. Da [[Logica-Sentencial|Lógica Sentencial]] e das [[Estruturas-Logicas|Estruturas Lógicas]] você traz a capacidade de pensar em *regras, condições e padrões* — e é assim que um modelo aprende padrões a partir de dados. Do [[Raciocinio-Matematico-Aplicado|Raciocínio Matemático Aplicado]] você traz o hábito de lidar com relações entre grandezas — e "pesos" em uma rede neural são, conceitualmente, valores numéricos que ajustam a importância de cada entrada. Não vamos avançar para fórmulas; vamos apenas reconhecer que por trás do "mágico" existe **matemática e estatística** — a mesma matemática que você já estuda.

> [!tip] Conexão com o pré-requisito
> Pense em um modelo de machine learning como alguém tentando encontrar um **padrão** em um conjunto de dados — algo muito próximo de reconhecer uma "regra" ou "conclusão" que se segue de premissas (como na [[Logica-de-Argumentacao|Lógica de Argumentação]]), só que aprendida a partir de exemplos, não deduzida de axiomas. Guarde essa ponte: **ML aprende padrões por indução a partir de dados**; a lógica dedutiva que você estudou parte de regras dadas.

---

## 2. IA, Machine Learning e Deep Learning: a hierarquia

Vamos começar pela pergunta mais básica: *o que é Inteligência Artificial?*

Em termos simples, **IA (Inteligência Artificial)** é o campo que busca criar sistemas capazes de realizar tarefas que, tradicionalmente, exigiriam **inteligência humana** — como reconhecer imagens, compreender linguagem, tomar decisões e aprender com a experiência. Esse é um campo **amplo e antigo**; a ideia de "máquinas que pensam" precede os computadores modernos.

Dentro desse campo enorme, existem subdivisões. A mais importante para a prova:

> [!important] A hierarquia que a FGV cobra
> $$
> IA \supset Machine\ Learning \supset Deep\ Learning
> $$
>
> **Inteligência Artificial** é o campo maior. **Machine Learning (ML / Aprendizado de Máquina)** é uma *subárea* da IA: máquinas que **aprendem a partir de dados** em vez de seguirem regras programadas à mão. **Deep Learning (Aprendizado Profundo)** é uma *subárea* do ML, baseada em **redes neurais profundas** (muitas camadas). Nem toda IA é ML; nem todo ML é Deep Learning — mas todo DL é ML e todo ML é IA.

### 2.1 Por que essa hierarquia importa

Antes do ML, os sistemas de IA eram, na prática, conjuntos de **regras escritas por humanos** (*if isto, então aquilo*). Um sistema que decide "se o e-mail contém a palavra 'prêmio' e 'clique aqui', marque como spam" é uma IA *por regras* — mas **não** é machine learning, porque não aprendeu nada: um humano codificou a regra.

O salto do ML foi inverter isso: em vez de o humano dizer *qual regra usar*, dá-se ao sistema **muitos exemplos** e ele **descobre o padrão** sozinho. Aqui está a ponte com a [[Logica-Sentencial|Lógica Sentencial]]: em vez de você montar a tabela-verdade de cada situação, o modelo *induz* o padrão a partir dos dados.

> [!question] Pergunta orientadora
> Um sistema de IA anti-fraude que segue uma lista fixa de regras ("bloqueie compras acima de R$ 5.000 do exterior") é machine learning? **Não.** Ele não aprende — segue regras programadas. ML exigiria que o sistema *descobrisse* os padrões de fraude a partir de milhares de transações históricas, sem que alguém as listasse previamente.

### 2.2 Tipos de IA: geral, estreita e forte

Outra classificação que aparece com frequência distingue a **abrangência** da IA:

- **IA estreita (narrow/weak)**: especializada em **uma tarefa**. Um sistema que reconhece rostos, um tradutor, um assistente que responde perguntas. É **toda** a IA que existe hoje na prática. O nome "fraca" não significa "inútil" — significa "limitada a um domínio".
- **IA geral (AGI — Artificial General Intelligence)**: a que realizaria **qualquer tarefa intelectual** que um ser humano faz, com flexibilidade similar à humana. É um **objetivo teórico**, ainda não alcançado.
- **IA forte**: em filosofia, refere-se a uma máquina com **consciência e entendimento real** — também conceito teórico.

> [!tip] Palavras-chave
> **IA estreita/narrow** (toda IA atual) · **IA geral/AGI** (teórica) · **IA forte** (consciência, teórica) · **regra programada × aprendizado a partir de dados**.

A pegadinha clássica: a banca pergunta "a IA utilizada hoje em assistentes e reconhecimento facial é..." — resposta: **IA estreita**, não geral nem forte.

---

## 3. Machine Learning: os três tipos de aprendizado

O núcleo do ML está em **como** o sistema aprende. Há três grandes paradigmas, e a distinção entre eles é um dos alvos mais frequentes. A chave para diferenciá-los está em uma única pergunta: **que tipo de informação o sistema recebe durante o treinamento?**

### 3.1 Aprendizagem supervisionada

> [!important] Supervisionada = as respostas certas (rótulos) estão no treinamento
> O algoritmo recebe exemplos **rotulados** — cada exemplo vem acompanhado da **resposta correta** (o *label*/**rótulo**). Ele aprende a mapear entrada → saída, e depois é testado em dados **não vistos**. Por isso "supervisionada": há um "supervisor" (os rótulos) ditando o certo.

Imaginemos que você quer um modelo que diga se um e-mail é spam ou não. Você treina com **milhares de e-mails já marcados** — "este é spam", "este não é" (esses rótulos). O modelo aprende os padrões que distinguem um do outro. Depois, recebe um e-mail novo, sem rótulo, e prevê a classe.

Dentro da supervisionada há dois subtipos que a banca separa:

- **Classificação**: a saída é uma **categoria discreta** — "spam ou não", "gato ou cachorro", "aprovado ou reprovado". Palavras-chave: *classe, categoria, rótulo*.
- **Regressão**: a saída é um **valor contínuo** (um número) — prever o preço de um imóvel, a temperatura de amanhã, o salário com base em anos de experiência. Palavras-chave: *valor numérico, previsão de grandeza*.

> [!example] Exemplo autoral — classificação vs. regressão
> Uma loja usa ML para prever "se o cliente vai comprar ou não" (classificação: duas classes) e, para quem compra, "quanto ele gastará" (regressão: um valor contínuo em reais). O primeiro seleciona categorias; o segundo estima números.

### 3.2 Aprendizagem não-supervisionada

Se a supervisionada tem rótulos, a **não-supervisionada** trabalha **sem rótulos**: a resposta certa *não* está no treinamento. O algoritmo recebe apenas os **dados** e precisa encontrar **estrutura, agrupamentos ou padrões ocultos** por conta própria.

**Palavra-chave central: clusterização (agrupamento).** O sistema agrupa itens **parecidos entre si** sem que ninguém lhe diga quais grupos existem.

> [!example] Exemplo autoral — clusterização
> Uma empresa tem dados de milhões de clientes (idade, renda, histórico de compras) **sem nenhuma categoria pré-definida**. Um algoritmo não-supervisionado agrupa esses clientes em **segmentos** parecidos — e então o time de marketing *dá nome* a esses grupos ("jovens engajados", "consumidores premium"). O algoritmo achou os grupos; o humano os interpretou. Note o contraste: na supervisionada, as classes existem *antes*; na não-supervisionada, os grupos emergem *do* dado.

> [!question] Pergunta orientadora
> Se eu já sei, de antemão, que os clientes se dividem em "baixa", "média" e "alta renda", e quero ensinar um modelo a classificar novos clientes nessas três classes, devo usar aprendizado supervisionado ou não-supervisionado? **Supervisionado** — porque as classes (rótulos) já existem e estarão no treinamento. Não-supervisionado só faz sentido quando não há respostas pré-definidas.

### 3.3 Aprendizagem por reforço

O terceiro paradigma é o mais diferente e, conceitualmente, o mais próximo de como um animal aprende por **tentativa e erro**. Aqui há um **agente** que age em um **ambiente**, e cada ação produz uma **recompensa** (positiva) ou **punição** (negativa). O objetivo do agente é aprender a sequência de ações que **maximiza a recompensa acumulada** ao longo do tempo.

**Palavras-chave: agente · ambiente · ação · recompensa · punição · recompensa acumulada.**

> [!example] Exemplo autoral — jogos
> Uma IA que aprende a jogar xadrez "sozinha" é o exemplo clássico. Ela faz milhares de jogadas; vencer dá recompensa, perder dá punição. Com o tempo, ela reforça as sequências de ações que levam à vitória. Não há um "rótulo" dizendo *qual é a jogada certa* em cada posição — há apenas a consequência (vitória/derrota). Por isso não é supervisionada: ninguém fornece as respostas corretas; o agente *descobre* a boa política por reforço dos acertos.

> [!important] Resumindo o que distingue os três (memorize assim)
> | Paradigma | Dados de treino | Tarefa típica | Palavra-chave |
> |:--|:--|:--|:--|
> | **Supervisionada** | Com rótulos (respostas) | Classificar / regredir | *rótulo, classe, valor* |
> | **Não-supervisionada** | Sem rótulos | Agrupar / descobrir padrão | *clusterização, agrupamento* |
> | **Por reforço** | Sem rótulos; com recompensa | Aprender por tentativa e erro | *agente, recompensa, punição* |

---

## 4. Redes neurais: o conceito geral

Você ouvirá muito o termo "rede neural". Conceitualmente — e é só isso que a prova pede — uma rede neural é um modelo inspirado, *de forma bem simplificada*, no funcionamento do cérebro. Ela é composta de **unidades de processamento chamadas neurônios artificiais**, organizadas em **camadas**.

### 4.1 Anatomia conceitual

- **Neurônios artificiais**: pequenas unidades que recebem entradas, processam uma informação e produzem uma saída. Cada entrada carrega um **peso** — um valor numérico que indica *quão importante* aquela entrada é para o resultado. Essa é a ponte com o [[Raciocinio-Matematico-Aplicado|raciocínio matemático]]: os pesos, no fundo, são números que servem para *ponderar* as entradas, como uma média ponderada.
- **Camadas**: um grupo de neurônios. Há a **camada de entrada** (recebe os dados), a(s) **camada(s) oculta(s)** (intermediária(s), onde ocorre o "aprendizado") e a **camada de saída** (produz o resultado).
- **Função de ativação**: uma regra que decide se um neurônio "dispara" (ativa) sua saída, introduzindo **não-linearidade** — é o que permite ao modelo capturar padrões complexos, e não apenas combinações lineares simples.

### 4.2 Como a rede "aprende"

Aqui está o coração conceitual. No treinamento, a rede **compara a saída que produziu com a resposta desejada** (um rótulo, no caso supervisionado) e calcula o **erro**. Então, ela **ajusta os pesos** para reduzir esse erro, repetindo milhões de vezes. O processo de ajustar os pesos a partir do erro, propagado das camadas finais para as iniciais, é chamado **retropropagação (backpropagation)**.

> [!tip] Palavras-chave de redes neurais
> **neurônio artificial** · **camadas** (entrada, ocultas, saída) · **pesos** · **função de ativação** · **treinamento** · **erro** · **retropropagação (backpropagation)** · **rede profunda** (muitas camadas ocultas).

> [!note] Não precisa da fórmula
> A banca cobra *reconhecimento conceitual*, não cálculo. Não memorize a matemática da retropropagação. Basta entender: **a rede erra, calcula o erro, e ajusta os pesos para errar menos** — repetidamente, até convergir. Deep Learning é apenas uma rede com **muitas camadas ocultas** (profunda).

---

## 5. Modelos generativos e LLMs

Agora chegamos ao segmento mais contemporâneo e mais ligado à atualidade — e ao seu futuro profissional. Dois termos precisam ser separados com clareza: **modelos discriminativos/preditivos vs. modelos generativos**.

### 5.1 Reconhecer vs. gerar

- Um modelo **discriminativo/preditivo** **reconhece e classifica**: dado um insumo, ele diz *o que é*. "Esta imagem é gato ou cachorro?", "Este e-mail é spam?" — exemplos de discriminação/classificação.
- Um modelo **generativo** **cria conteúdo novo**: dado um pedido, ele *gera* texto, imagem, áudio ou código que não existia antes. Em vez de "reconhecer o que está aí", ele "inventa o que poderia estar".

> [!important] A distinção central
> **Discriminativo/preditivo = reconhecer e classificar** (o que já existe). **Generativo = criar e gerar** (conteúdo novo). A banca adora essa oposição: "um modelo que gera texto novo em resposta a um prompt é..." — resposta: **generativo**.

### 5.2 O que são LLMs (Large Language Models)

**LLM (Large Language Model / Grande Modelo de Linguagem)** é um tipo de modelo generativo especializado em **linguagem (texto)**. As três palavras do nome explicam o conceito:

- **L (Large / Grande)**: são **redes neurais profundas** com **enorme número de parâmetros**, treinadas em **enormes volumes de texto** (livros, artigos, páginas da web).
- **L (Language / Linguagem)**: trabalham com linguagem natural — produzem e entendem texto.
- **M (Model / Modelo)**: são modelos estatísticos de linguagem.

O mecanismo básico de um LLM, em termos simples, é **prever o próximo token** (a próxima unidade de texto) dada a sequência anterior. Se você fala "A capital do Brasil é...", o modelo estima qual é o *token* mais provável de vir — "Brasília". Gerar texto longo é, em essência, **prever token a token**, repetidamente.

**Tokens**: os LLMs não trabalham com palavras inteiras necessariamente — dividem o texto em **tokens**, que podem ser palavras, partes de palavras ou caracteres. É uma unidade de processamento do texto.

**Transformers**: os LLMs modernos são baseados em uma arquitetura chamada **transformer** (não confundir com o transformador de tensão elétrica!). O conceito central, num nível simples, é o **mecanismo de atenção** — o modelo aprende *em que partes* do texto prestar atenção para produzir a resposta certa. Você não precisa aprofundar; basta reconhecer a arquitetura por nome.

> [!example] Exemplos de LLMs (reconhecer por nome)
> Modelos como GPT, Gemini, Claude e Llama são exemplos de LLMs. Um **LLM** é o modelo de linguagem; a **ferramenta/interface** que o usuário usa no dia a dia é o que o "embrulha" para conversar. A banca pode testar: "o componente-chave de um sistema como o ChatGPT, responsável por gerar o texto, é um..." — **LLM**.

> [!tip] Palavras-chave de LLMs
> **Large Language Model (LLM)** · **token** · **previsão de próxima palavra/token** · **transformer** · **mecanismo de atenção** · **parâmetros** · **conteúdo gerado** · **GPT · Gemini · Claude · Llama**.

### 5.3 Alucinação (um aviso para já)

Modelos generativos podem "inventar" informações com aparência de verdade — o fenômeno chamado **alucinação**. Veremos isso em profundidade na nota [[IA-e-Etica|IA e Ética]], mas já é bom fixar o termo: **alucinação = o modelo gera conteúdo falso/ineditamente inventado com confiança**. É um dos grandes riscos do uso corporativo e público.

---

## 6. Prompt engineering: o conceito básico

Chegamos ao tópico mais "prático" e mais diretamente útil para você. **Prompt** é a **instrução ou entrada** que você dá a um modelo generativo para obter uma resposta. **Prompt engineering (engenharia de prompt)** é a **prática de formular esses prompts de forma deliberada** para obter resultados melhores, mais precisos e mais úteis.

Pergunta natural: *por que isso importa?* Porque o mesmo modelo, com prompts diferentes, produz resultados de qualidade radicalmente diferente. O modelo não lê mentes: ele responde à qualidade da instrução que recebe.

> [!tip] Conceito-chave
> **Prompt** = a entrada/instrução. **Prompt engineering** = a arte de elaborar boas instruções para extrair melhores respostas do modelo. Quanto mais específico, claro e delimitado o prompt, melhor tende a ser a resposta.

### 6.1 Bom prompt vs. mau prompt

Vejamos com um contraste simples sobre o mesmo modelo:

- **Mau prompt:** "Me fala sobre IA."
- **Bom prompt:** "Explique, em três parágrafos e para um iniciante, a diferença entre IA, machine learning e deep learning, usando um exemplo de cada."

Por que o segundo é melhor? Porque define: o **assunto** (diferença entre os três), a **profundidade** (para iniciante), o **tamanho/tempo de resposta** (três parágrafos) e o **formato pedido** (exemplos). Quanto mais contexto e restrições precisos, menos espaço para resposta vaga.

### 6.2 Algumas técnicas básicas (conceitual)

- **Seja específico**: dê contexto e detalhe, não pergunte vago.
- **Instrua a estrutura**: peça formato, tamanho, tom, público-alvo.
- **Divida a tarefa**: tarefas complexas ficam melhores quando quebradas em etapas.
- **Forneça exemplos**: mostrar um exemplo do formato desejado (few-shot) guia melhor o modelo.

> [!note] Por que a FGV cobra isso
> Prompt engineering é uma **habilidade concreta de TI** e um tema "novo no edital" (ver observações pedagógicas da ementa). A banca tende a cobrar em nível conceitual: *o que é um prompt*, *o que é prompt engineering*, e *por que uma boa formulação melhora o resultado*. Não precisa dominar técnicas avançadas — precisa reconhecer o conceito e a utilidade.

---

## 7. Questões-modelo comentadas (estilo FGV)

Aqui estão duas questões autorais, no formato da FGV (5 alternativas), para você fixar os conceitos.

### Questão 1

> [!example] Questão-modelo 1
> Um sistema de reconhecimento facial foi treinado com milhares de fotos **já classificadas** como "do titular" ou "não do titular", para aprender a distinguir as duas classes. Diante de uma foto nova, sem rótulo, o sistema decide a qual das duas classes ela pertence. Esse cenário caracteriza um aprendizado de máquina:
>
> (A) por reforço, pois há recompensa por acertos.
> (B) não-supervisionado, pois os grupos são descobertos a partir dos dados.
> (C) **supervisionado**, pois o treinamento usou exemplos rotulados e a tarefa é de classificação.
> (D) generativo, pois o sistema cria novas imagens.
> (E) de rede neural profunda sem treinamento.

> [!example] Raciocínio comentado
> A alternativa **C** é a correta: o treinamento usou **rótulos** ("do titular"/"não do titular") — sinal inequívoco de **supervisionado**; e a saída é uma **categoria** (classe), logo é **classificação**. (A) erra: não há recompensa por tentativa e erro. (B) erra: grupos não são descobertos — as classes já existiam. (D) erra: o sistema *reconhece*, não *gera*. (E) erra: todo treinamento requer ajuste de pesos.

### Questão 2

> [!example] Questão-modelo 2
> Um LLM, ao receber a sequência de texto "O céu está claro, então vamos viajar de", calcula qual é o próximo token mais provável e responde "avião". Em termos conceituais, a capacidade central desse modelo é:
>
> (A) a classificação de imagens em categorias discretas.
> (B) a **previsão do próximo token com base no contexto, característica típica dos LLMs baseados em transformers**.
> (C) o aprendizado não-supervisionado por clusterização.
> (D) a retropropagação exclusivamente sobre números, sem texto.
> (E) a geração de conteúdo sem uso de parâmetros nem treinamento.

> [!example] Raciocínio comentado
> A alternativa **B** é a correta: LLMs essencialmente **preveem o próximo token** dado o contexto, e são construídos sobre a arquitetura **transformer**. (A) erra: é um modelo de *linguagem*, não de classificação de imagem. (C) erra: não é clusterização. (D) erra: a retropropagação é o mecanismo de treinamento, não a capacidade central de geração em uso. (E) erra: há parâmetros e treinamento.

---

## 8. Palavras-chave que a banca cobra

> [!important] Caixa de ferramentas de IA
> **Inteligência Artificial** · **IA estreita/narrow · IA geral/AGI · IA forte** · **Machine Learning (ML)** · **Deep Learning (DL)** · **aprendizado supervisionado** (rótulos, classificação, regressão) · **aprendizado não-supervisionado** (clusterização, agrupamento) · **aprendizado por reforço** (agente, recompensa, punição) · **rede neural** (neurônio artificial, camadas, pesos, ativação, retropropagação/backpropagation) · **modelo generativo × discriminativo** · **LLM** · **token** · **previsão de próxima palavra** · **transformer** · **mecanismo de atenção** · **alucinação** · **prompt** · **prompt engineering**.

---

## 9. Pegadinhas mais comuns

> [!warning] PEGADINHA 1 — inverter a hierarquia
> A banca tenta fazer você achar que "IA é uma subárea de machine learning" — é o **contrário**: IA ⊃ ML ⊃ DL. Todo ML é IA, mas nem toda IA é ML (ex.: sistemas por regras).

> [!warning] PEGADINHA 2 — confundir supervisionada e não-supervisionada
> O teste definitivo: **os rótulos (respostas certas) existem no treinamento?** Sim → supervisionada. Não → não-supervisionada (agrupa) ou por reforço (recompensa). Se a questão menciona "categorias pré-definidas" → supervisionada.

> [!warning] PEGADINHA 3 — classificação × regressão
> Classificação → categoria discreta ("sim/não", "gato/cachorro"). Regressão → valor numérico contínuo (preço, temperatura, quantidade). Trocar os dois é erro clássico.

> [!warning] PEGADINHA 4 — chamar todo modelo generativo de "reconhecer"
> Discriminativo reconhece/classifica; **generativo cria conteúdo novo**. Um chatbot que *gera* uma resposta nova é generativo; um sistema que só *rotula* uma imagem como gato/cachorro é discriminativo.

> [!warning] PEGADINHA 5 — dizer que IA atual é "geral" ou "forte"
> Toda IA utilizada hoje em produtos é **estreita (narrow)**. AGI e IA forte são teóricas. A pegadinha: exaltar a tecnologia e chamá-la de "inteligência geral" — incorreto.

> [!warning] PEGADINHA 6 — achar que LLM "entende" de verdade
> LLMs **preveem o próximo token** a partir de padrões estatísticos; não "compreendem" no sentido humano pleno. E podem **alucinar** (inventar com aparência de verdade). A banca pode testar se você cai na ideia de que "o modelo raciocina como uma pessoa".

> [!warning] PEGADINHA 7 — definir prompt engineering como "escrever qualquer pergunta"
> Não é "digitar qualquer coisa". Prompt engineering é a **formulação deliberada e otimizada de instruções** para melhorar a qualidade da resposta.

---

## 10. Próximos passos

Você agora domina a base conceitual de IA: a hierarquia IA ⊃ ML ⊃ DL, os três tipos de aprendizado, o conceito de redes neurais, o que são modelos generativos e LLMs, e o que é prompt engineering. Na próxima nota, **[[IA-e-Etica|IA e Ética]]**, você conecta tudo isso aos debates que mais interessam a um concurso público: **viés algorítmico, transparência e explicabilidade**, a **regulamentação** (com destaque para o EU AI Act e o "Marco Legal da IA" brasileiro) e o impacto da IA no trabalho de TI — usando a [[LGPD-Lei-Geral-de-Protecao-de-Dados|LGPD]] que você já estudou como espinha dorsal. Depois disso, você segue para a **Fase 3 — Banco de Dados**, que também tem como pré-requisitos o raciocínio lógico e a legislação que você já domina.
