# Lei Carolina Dieckmann — Lei nº 12.737/2012

> [!info] Metadados
> **Disciplina:** Legislação de Segurança da Informação e LGPD
> **Bloco:** 1.3 — Legislação (FASE 1 — Fundamentos)
> **Tópico:** 2. Lei Carolina Dieckmann (Lei 12.737/2012)
> **Subtópicos:** Inserção de dispositivos no Código Penal · Acesso indevido a dispositivo informático (art. 154-A) · Penas e circunstâncias agravantes · Ação penal (art. 154-B)
> **Pré-requisitos:** Nenhum
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-28

---

## 1. Por que estudar este tópico?

Você já estudou a [[Lei-de-Acesso-a-Informacao-LAI|LAI]] e conhece o princípio de que a informação pública é a regra e o sigilo, a exceção. Agora o Bloco 1.3 muda de ângulo: em vez de garantir o *direito de acessar* informações, ele passa a **punir quem acessa sem autorização** — ou seja, entra na perspectiva daquele que *viola* o sistema. É a face criminal da Segurança da Informação.

A **Lei Carolina Dieckmann** (Lei nº 12.737, de 30 de novembro de 2012) é o marco que **tipificou como crime a invasão de computadores e dispositivos informáticos** no direito brasileiro. Ela é especialmente relevante para o seu cargo de **Analista de TI na DATAPREV** porque:

- qualquer profissional de TI precisa saber **o que é crime** na prática de invasão, mesmo que por "curiosidade" ou "testes de segurança" não autorizados;
- a lei abrange não apenas quem invade, mas também quem **produz, vende ou distribui ferramentas de invasão** (malwares, trojans, exploit kits) — atividade que pode parecer inofensiva no meio de desenvolvimento;
- a FGV costuma cobrar a estrutura do tipo penal com foco nas **palavras-chave exatas** e nas **diferenças entre a redação original (2012) e a atual (após Lei 14.155/2021)** — o que exige atenção redobrada.

> [!question] Pergunta orientadora
> Um desenvolvedor cria um pequeno programa que abre uma porta de acesso remoto em um computador sem que o usuário saiba. Ele não "invade" pessoalmente — apenas distribui o programa. A lei pune esse ato? A resposta está no §1º do art. 154-A, e é um dos pontos mais cobrados em provas.

> [!tip] Palavras-chave que a banca usa (guarde desde já)
> **Dispositivo informático de uso alheio** · **conectado ou não à rede** · **vantagem ilícita** · **detenção → reclusão** · **violação indevida de mecanismo de segurança** (redação original) · **ação penal pública condicionada à representação** · **exceção: administração pública** · **figura equiparada (§1º)** · **causa de aumento (§2º, §3º, §4º, §5º)** · **Comunicações eletrônicas privadas** · **segredos comerciais/industriais** · **controle remoto não autorizado**.

---

## 2. Contexto histórico: o caso que deu nome à lei

A expressão "Lei Carolina Dieckmann" faz referência ao caso da atriz **Carolina Dieckmann**, que em 2012 teve seu computador invadido por hackers. Os invasores obtiveram **fotos íntimas** e dados pessoais da atriz, que depois foram **divulgados publicamente**. O caso ganhou enorme repercussão midiática e expôs uma lacuna grave no ordenamento jurídico brasileiro: na época, **não existia um tipo penal específico** para a invasão de computadores. As condutas eram, no máximo, enquadradas de forma forçada em figuras como "estelionato" ou "inserção de dados falsos em sistema de informações" (art. 313-A do CP), que não tinham a invasão em si como núcleo do tipo.

Diante da pressão pública, o Congresso aprovou rapidamente a Lei 12.737, sancionada em **30 de novembro de 2012** e com vigência a partir de **2 de abril de 2013**. A lei é curta — apenas dois artigos —, mas seu impacto é enorme: o **art. 1º** alterou a Lei 10.826/2003 (Estatuto do Desarmamento) para equiparar armas de impressão 3D a armas de fogo (ponto não cobrado neste tópico); o **art. 2º** é o que nos interessa, pois **acrescentou ao Código Penal os arts. 154-A e 154-B**, criando os crimes de invasão de dispositivo informático e regulando a ação penal para eles.

> [!important] O edital citou "Art. 2º" da Lei 12.737 — e não "arts. 154-A e 154-B" do Código Penal
> Quando o edital diz "Lei nº 12.737/2012 (art. 2º)", ele está se referindo ao artigo da **lei em si** — que acrescentou os dispositivos ao CP. Mas o conteúdo **substantivo** que você precisa dominar está nos **arts. 154-A e 154-B do Código Penal**, hoje incorporados ao texto permanente do Código. A banca pode formular questões tanto citando a lei quanto citando os artigos do CP — saiba reconhecer os dois caminhos.

---

## 3. O art. 154-A: o núcleo do tipo — acesso indevido a dispositivo informático

### 3.1 A redação original de 2012 e a redação atual

Para entender bem o que a lei faz, é preciso comparar a **redação original** de 2012 com a **redação atual**, resultante da alteração feita pela **Lei nº 14.155/2021**. Essa comparação é uma das formas mais eficazes de fixar o conteúdo — e é exatamente onde moram as maiores pegadinhas.

> [!important] Art. 154-A, caput — antes e depois

> **Redação ORIGINAL (Lei 12.737/2012):**
> "Invadir dispositivo informático **alheio**, conectado ou não à rede de computadores, **mediante violação indevida de mecanismo de segurança** e com o fim de obter, adulterar ou destruir dados ou informações **sem autorização expressa ou tácita do titular do dispositivo** ou instalar vulnerabilidades para obter vantagem ilícita: Pena — **detenção**, de **3 (três) meses a 1 (um) ano**, e multa."

> **Redação ATUAL (após Lei 14.155/2021):**
> "Invadir dispositivo informático **de uso alheio**, conectado ou não à rede de computadores, com o fim de obter, adulterar ou destruir dados ou informações **sem autorização expressa ou tácita do usuário do dispositivo** ou de instalar vulnerabilidades para obter vantagem ilícita: Pena — **reclusão**, de **1 (um) a 4 (quatro) anos**, e multa."

Note que a estrutura geral é a mesma, mas **três mudanças** alteram profundamente o alcance e a gravidade do crime. Vamos destrinchar cada uma.

### 3.2 As três mudanças-chave da Lei 14.155/2021

**Mudança 1 — Retirada do "mediante violação indevida de mecanismo de segurança"**

Esta é, sem dúvida, a alteração mais importante e a mais cobrada em provas. Na redação de 2012, o tipo exigia que o invasor **vencesse um mecanismo de segurança** para que a conduta fosse criminosa. Se o computador não tivesse senha, firewall ou qualquer proteção, a invasão *não se encaixava no tipo penal* — era uma lacuna absurda que favorecia o criminoso justamente quando a vítima era mais vulnerável.

A Lei 14.155/2021 **retirou esse elemento**. Agora, basta **invadir** o dispositivo — não importa se ele estava protegido ou não. Um computador ligado sem senha, um pen drive abandonado com dados, um servidor com porta aberta: todos são protegidos pelo tipo penal atual.

> [!warning] PEGADINHA nº 1 — a "violação de mecanismo de segurança" NÃO é mais requisito
> Questão que disser que "é necessário que o agente venceu mecanismo de segurança para configurar o crime" está ERRADA. Isso era verdade em 2012, mas não é mais. Na prova, quando você vir essa exigência, marque como incorreta. A redação atual dispensa qualquer menção a mecanismo de segurança.

**Mudança 2 — "Alheio" → "de uso alheio"**

Outra mudança sutil, mas com impacto prático relevante. Na redação original, o dispositivo era descrito como "alheio" — ou seja, pertencente a outra pessoa. A redação atual fala em "**de uso alheio**". A mudança amplia o alcance: não importa a *propriedade* formal do dispositivo; importa que ele seja **usado por outra pessoa**. Exemplo: um servidor corporativo que não pertence formalmente ao funcionário, mas que ele utiliza no dia a dia — na redação atual, invadir esse servidor para obter dados sem autorização configura o crime.

**Mudança 3 — Detenção → Reclusão**

A redação original previa **detenção** de 3 meses a 1 ano. A atual prevê **reclusão** de 1 a 4 anos. Essa alteração tem consequência prática enorme:

> [!important] Detenção vs. Reclusão — por que isso importa na prova?
> - **Detenção** (art. 33, II, do CP): cumprimento inicial em **regime semiaberto** ou **fechado**, quando o juiz considerar que o réu não preenche os requisitos para o semiaberto. Crimes de detenção, em regra, são de **menor potencial ofensivo** (até 2 anos de pena máxima, conforme a Lei 9.099/95), o que abre possibilidade de suspensão condicional do processo e outras benesses.
> - **Reclusão** (art. 33, I, do CP): cumprimento em **regime fechado, semiaberto ou aberto**, conforme a pena e a progressão. E, com pena máxima de 4 anos, o crime deixa de ser de menor potencial ofensivo.
>
> Resumindo: antes, o invasor de computador podia se beneficiar de escape da Lei 9.099/95 (pena até 2 anos); hoje, com reclusão e máximo de 4 anos, ele responde pelo rito comum. A banca cobra essa distinção.

### 3.3 Os elementos do tipo penal atual (redação vigente)

Agora que você conhece as mudanças, vamos olhar a estrutura completa do tipo com atenção, porque é aqui que a FGV "faz a caça":

O **núcleo do tipo** é **"invadir"**. Invadir significa ingressar indevidamente, sem autorização, no território informático alheio. O objeto material é o **dispositivo informático de uso alheio** — e aqui a lei usa a expressão "conectado ou não à rede de computadores", o que amplia a cobertura para qualquer equipamento: desktop, notebook, smartphone, tablet, pen drive com dados, servidor, IoT (dispositivos de internet das coisas), entre outros.

Os **elementos subjetivos** (finalidade) são:

1. **obter** dados ou informações sem autorização;
2. **adulterar** dados ou informações sem autorização;
3. **destruir** dados ou informações sem autorização;
4. **instalar vulnerabilidades** para obter vantagem ilícita.

Note que a conduta exige **finalidade específica**: o invasor precisa querer obter, adulterar, destruir dados ou instalar vulnerabilidades. Se alguém acessa um computador alheio sem autorização mas **sem nenhuma dessas finalidades** (por exemplo, apenas para "olhar" a tela), a configuração do tipo pode ser discutida — mas na prática, a mera entrada no dispositivo com a intenção de acessar dados já costuma ser interpretada como tentativa de obtenção.

> [!warning] PEGADINHA nº 2 — "conectado ou não à rede"
> A lei deixa claro que o computador **não precisa estar conectado à internet** para que a invasão seja crime. Um notebook desligado, mas que alguém acessa e copia dados de um pen drive, também se enquadra. A banca adora testar se o candidato percebe que a conexão à rede **não é requisito** do tipo.

> [!warning] PEGADINHA nº 3 — "vantagem ilícita" no final da frase
> Na redação literal do caput, a expressão "para obter vantagem ilícita" aparece gramaticalmente vinculada ao último elemento listado no tipo — a instalação de vulnerabilidades. Contudo, parte da doutrina e da jurisprudência interpreta que **todas** as condutas descritas no tipo são orientadas por uma finalidade de vantagem ilícita — seja a obtenção indevida de dados, seja a manipulação. Essa é uma construção interpretativa, não uma leitura literal. A banca pode tentar confundir dizendo que "só a instalação de vulnerabilidades exige vantagem ilícita" — em prova, marque como correta a leitura que reconhece o debate e identifica a finalidade que orienta a conduta.

### 3.4 O §1º — a figura equiparada: quem cria e distribui o "instrumento do crime"

O §1º do art. 154-A estende a mesma pena (reclusão de 1 a 4 anos, e multa) a quem **produz, oferece, distribui, vende ou difunde** dispositivo ou programa de computador **com o intuito de permitir a prática da conduta do caput**.

Isso significa que não apenas quem invade é punido — **quem fabrica e distribui a ferramenta de invasão** também é. Estamos falando de criadores de malwares, trojans, keyloggers, RATs (Remote Access Trojans), exploit kits e afins. A lei pune o **ato preparatório** que antes não seria alcançável pelo Código Penal comum.

> [!question] Pergunta orientadora
> Um programador cria um software que permite acessar remotamente computadores de terceiros sem autorização e o disponibiliza gratuitamente na internet. Ele próprio não invadiu ninguém. A lei pune? **Sim** — o §1º pune quem produz, oferece, distribui, vende ou difunde o programa **com o intuito** de viabilizar a invasão. O elemento subjetivo é o **intuito de permitir** a prática do crime do caput.

Note que o §1º usa verbos **amplos**: produzir, oferecer, distribuir, vender e difundir. Qualquer um deles, associado ao intuito de viabilizar a invasão, configura a conduta. E o dispositivo ou programa precisa ser **capaz** de permitir a prática — um software que, por sua natureza, não tem essa funcionalidade não se enquadra.

### 3.5 O §2º — causa de aumento por prejuízo econômico

O §2º prevê que a pena é **aumentada de um terço a dois terços** se da conduta resulta **prejuízo econômico** à vítima.

> [!note] Alteração pela Lei 14.155/2021
> Na redação original de 2012, o aumento era de **um sexto a um terço**. A Lei 14.155/2021 majorou para **um terço a dois terços**, refletindo a maior gravidade que o legislador passou a atribuir aos crimes informáticos.

O prejuízo econômico não precisa ser a finalidade do crime — basta que seja o **resultado**. Exemplo: o invasor obtém dados de um sistema bancário e, com isso, a vítima sofre perdas financeiras diretas. O §2º se aplica como causa de aumento.

### 3.6 O §3º — a qualificadora: conteúdo privado, segredos e controle remoto

Esta é a causa de aumento mais grave do tipo-base (caput). O §3º dispõe que, se da invasão resultar a **obtenção** de:

- **conteúdo de comunicações eletrônicas privadas** (e-mails, mensagens de WhatsApp, conversas em aplicativos);
- **segredos comerciais ou industriais**;
- **informações sigilosas**, na forma de lei (esta expressão remete a definições em leis específicas, como a LAI — veja a conexão com o tópico anterior); ou
- **controle remoto não autorizado** do dispositivo;

a pena é de **reclusão de 2 (dois) a 5 (cinco) anos, e multa**.

> [!warning] PEGADINHA nº 4 — a qualificadora fala em "obtenção" e não em "divulgação"
> O §3º pune o ato de **obter** esses dados sensíveis — não é necessário que tenham sido divulgados ou comercializados. A mera obtenção já agrava. A **divulgação/comercialização** desses mesmos dados é tratada separadamente no §4º, com causa de aumento adicional. São patamares distintos.

> [!note] Alteração pela Lei 14.155/2021
> Na redação de 2012, a qualificadora previa pena de **reclusão de 6 meses a 2 anos**. A Lei 14.155/2021 aumentou para **reclusão de 2 a 5 anos**, e multa. Note a diferença: o mínimo subiu de 6 meses para 2 anos, e o máximo de 2 anos para 5 anos.

### 3.7 O §4º — causa de aumento por divulgação, comercialização ou transmissão

O §4º aumenta a pena em **um terço a dois terços** se os dados obtidos na forma do §3º forem **divulgados, comercializados ou transmitidos** a terceiros. Em termos simples: o §3º pega quem **roubou** os dados; o §4º pega quem **vazou, vendeu ou passou adiante** o que roubou. São dois patamares de gravidade sobrepostos.

### 3.8 O §5º — aumento contra autoridades públicas

O §5º prevê aumento de pena de **um terço à metade** quando o crime é praticado contra:

- **Presidente da República**;
- **Governadores** e **prefeitos**;
- **Presidente do Supremo Tribunal Federal (STF)**;
- **Presidentes da Câmara dos Deputados, do Senado Federal, de Assembleias Legislativas, da Câmara Legislativa do Distrito Federal ou de Câmaras Municipais**;
- **Dirigente máximo da administração direta e indireta federal, estadual, municipal ou do Distrito Federal**.

> [!warning] PEGADINHA nº 5 — a lista é taxativa
> A causa de aumento não se aplica contra "qualquer autoridade pública" — apenas contra as figuras **expressamente listadas** no §5º. Uma secretária de estado, um juiz de primeira instância ou um delegado **não** estão na lista. A banca pode tentar incluir autoridades que parecem importantes mas não constam do dispositivo.

> [!tip] Dica de memorização do §5º
> Pense na lista em três blocos: (1) **Chefes do Executivo** (Presidente, governadores, prefeitos); (2) **Chefes dos Legislativos** (presidentes de todas as Casas legislativas — Câmara, Senado, Assembleias, CLDF, Câmaras Municipais); (3) **Dirigentes da administração direta e indireta** (todos os níveis). Note que o **Presidente do STF** aparece isoladamente — ele é o único do Judiciário na lista.

### 3.9 Quadro-resumo do art. 154-A

Para facilitar a visualização, observe a estrutura completa do artigo:

| Dispositivo | Conduta | Pena (vigente — Lei 14.155/2021) | Observação |
|:---|:---|:---:|:---|
| **Caput** | Invadir dispositivo informático de uso alheio, conectado ou não à rede, para obter/adulterar/destruir dados ou instalar vulnerabilidades, sem autorização | **Reclusão: 1 a 4 anos + multa** | Antes era detenção 3m–1a |
| **§1º** | Produzir, oferecer, distribuir, vender ou difundir dispositivo/programa para permitir a prática do caput | **Reclusão: 1 a 4 anos + multa** | Figura equiparada (mesma pena do caput) |
| **§2º** | Se resultar prejuízo econômico | Aumento de **1/3 a 2/3** | Antes era 1/6 a 1/3 |
| **§3º** | Se da invasão resultar obtenção de comunicações privadas, segredos comerciais/industriais, informações sigilosas (em lei) ou controle remoto não autorizado | **Reclusão: 2 a 5 anos + multa** | Qualificadora — antiga: 6m–2a |
| **§4º** | Se os dados do §3º forem divulgados, comercializados ou transmitidos | Aumento de **1/3 a 2/3** | Causa de aumento sobre o §3º |
| **§5º** | Se o crime for praticado contra autoridades da lista (ver texto) | Aumento de **1/3 à metade** | Lista taxativa |

> [!question] Pergunta orientadora
> É possível acumular o §2º (prejuízo econômico) com o §3º (obtenção de dados sensíveis)? Na prática, sim — os dispositivos não são mutuamente exclusivos. Um invasor pode obter dados sensíveis (§3º) e, ao mesmo tempo, causar prejuízo econômico (§2º). E se divulgar esses dados, o §4º se soma ao §3º. A causa de aumento do §5º (autoridade) também pode se somar. A estrutura da lei admite **acúmulo de majorantes**, o que pode resultar em penas bem acima do mínimo do caput.

---

## 4. O art. 154-B: a ação penal — quem pode denunciar?

O art. 154-B regula **quem tem legitimidade para dar início ao processo penal** pelos crimes do art. 154-A. Essa questão é crucial porque define se o Ministério Público pode agir de ofício ou se depende de manifestação da vítima.

> [!important] Art. 154-B — regra e exceção
> "Nos crimes definidos no art. 154-A, somente se procede mediante **representação**, salvo se o crime é cometido contra a **administração pública direta ou indireta** de qualquer dos Poderes da União, dos Estados, do Distrito Federal ou dos Municípios, ou contra **empresas concessionárias de serviços públicos**."

A estrutura é clara e pode ser representada assim:

| Hipótese | Tipo de ação penal | Quem decide investigar/denunciar |
|:---|:---:|:---|
| Crime contra **particular** (pessoa física ou jurídica privada) | **Pública condicionada à representação** | O Ministério Público só age se a vítima **representar** (pedir investigação) |
| Crime contra a **administração pública** (direta ou indireta, qualquer poder, qualquer ente federativo) | **Pública incondicionada** | O Ministério Público age **de ofício**, sem depender da vítima |
| Crime contra **empresa concessionária de serviços públicos** | **Pública incondicionada** | Idem — não depende de representação |

### 4.1 Representação vs. queixa: não confunda

Uma confusão muito comum é trocar **representação** com **queixa**. São coisas diferentes:

- **Representação** (art. 154-B e art. 5º, do CPP): é a manifestação da vítima ao Ministério Público ou à autoridade policial, manifestando o desejo de que o fato seja apurado. A vítima **não** entra com a ação penal — ela apenas "aciona" o processo. O MP pode arquivar mesmo com a representação, se entender que não há elementos.
- **Queixa-crime** (art. 102 do CPP): é a manifestação da vítima ingressando **diretamente** com a ação penal — processo penal **privado**. A vítima é a titular da ação.

No caso do art. 154-B, a palavra usada é **"representação"** — ou seja, a ação penal é **pública** (titularizada pelo MP), mas **condicionada** à vontade da vítima no início.

> [!warning] PEGADINHA nº 6 — "representação" não é "queixa"
> Se a questão disser que "nos crimes do art. 154-A procede-se mediante **queixa**", está ERRADA. O art. 154-B usa a palavra **"representação"**. Queixa implica ação penal privada; representação implica ação penal pública condicionada. Essa troca de palavras é uma das pegadinhas mais recorrentes da FGV.

### 4.2 A exceção: administração pública e concessionárias

Quando o crime é praticado contra a **administração pública** (direta ou indireta, de qualquer dos Poderes, de qualquer ente federativo) ou contra **empresa concessionária de serviços públicos**, a ação penal passa a ser **incondicionada** — ou seja, o Ministério Público pode agir **sem que a vítima peça**.

Isso faz sentido: o patrimônio público e os serviços públicos interessam a **toda a sociedade**, não apenas à entidade lesada. Seria inadequado que um órgão público tivesse que "pedir" para que o crime contra si fosse investigado.

> [!tip] Entendendo a lógica da exceção
> Pense assim: se um hacker invade o computador de um **cidadão comum**, a vítima (cidadão) é quem decide se quer o processo — afinal, é um interesse privado. Mas se o hacker invade o sistema de um **órgão público**, o dano atinge o interesse público, e a sociedade não pode ficar refém de uma eventual decisão administrativa de representar.

---

## 5. Pegadinhas numéricas e estratégias de prova

A FGV é extremamente precisa com números e palavras. Vamos organizar as principais "pegadinhas" para que você não caia nelas:

### 5.1 Quadro comparativo: antes (2012) vs. depois (2021)

| Elemento | Redação original (Lei 12.737/2012) | Redação atual (Lei 14.155/2021) |
|:---|:---|:---|
| **Objeto** | Dispositivo informático **alheio** | Dispositivo informático **de uso alheio** |
| **Exigência de invasão** | Mediante **violação indevida de mecanismo de segurança** | **(retirada)** — basta invadir |
| **Referência à vítima** | "Titular do dispositivo" | "Usuário do dispositivo" |
| **Pena do caput** | **Detenção**: 3 meses a 1 ano + multa | **Reclusão**: 1 a 4 anos + multa |
| **Pena da qualificadora (§3º)** | **Reclusão**: 6 meses a 2 anos + multa | **Reclusão**: 2 a 5 anos + multa |
| **Aumento do §2º (prejuízo)** | 1/6 a 1/3 | 1/3 a 2/3 |
| **Crime de menor potencial ofensivo?** | Sim (máx. 2 anos — art. 61 da Lei 9.099/95 com redação vigente à época) | **Não** (máx. 4 anos → rito comum) |

### 5.2 As pegadinhas mais frequentes da FGV

> [!warning] PEGADINHA nº 7 — "mediante violação de mecanismo de segurança" já não existe
> Esta é a mais clássica. Se a questão descrever um caso em que o invasor acessou um computador **sem senha** e a alternativa disser que "não há crime porque não houve violação de mecanismo de segurança", essa alternativa está **ERRADA**. A redação atual **não exige** isso.

> [!warning] PEGADINHA nº 8 — "conectado ou não à rede"
> Outra frequente: uma questão descreve a invasão de um computador **desconectado da internet** (por meio de rede local, pen drive ou acesso físico) e tenta sugerir que isso não seria crime. **É crime sim** — a lei é clara ao dizer "conectado ou não à rede de computadores".

> [!warning] PEGADINHA nº 9 — a equiparação do §1º não tem pena diferente
> Alguns candidatos pensam que o §1º (quem produz malware) tem pena diferente do caput. **Não tem** — é a **mesma** pena (reclusão de 1 a 4 anos e multa). A confusão surge porque outros dispositivos penais costumam prever penas diferentes para figuras equiparadas. Aqui, a lei optou pela igualdade de pena.

> [!warning] PEGADINHA nº 10 — representação ≠ queixa ≠ ação penal privada
> Lembre-se sempre: **art. 154-B = representação**. Se a questão trocar por "queixa", marque como errada. A ação penal é **pública** — o que varia é se depende (condicionada) ou não (incondicionada) da manifestação da vítima.

> [!warning] PEGADINHA nº 11 — a exceção inclui "concessionárias de serviços públicos"
> A lista de exceções (ação pública incondicionada) não se limita à administração pública direta e indireta — ela inclui expressamente **empresas concessionárias de serviços públicos** (concessionárias de saneamento, transporte, telecomunicações, etc.). Questão que disser que a exceção é "apenas administração pública" está incompleta.

---

## 6. Conexão com a LAI e com a segurança da informação

Você pode estar se perguntando: qual a relação entre a Lei Carolina Dieckmann e a [[Lei-de-Acesso-a-Informacao-LAI|LAI]]? A conexão é conceitual e prática:

- A **LAI** define o que é **informação sigilosa** (art. 4º, III) e **informação pessoal** (art. 4º, IV e art. 31), e cria um regime de proteção administrativa (classificação, prazos, restrições). Quando o art. 154-A, §3º, fala em obtenção de "informações sigilosas, na forma de lei", ele faz referência direta a esse universo conceitual. Ou seja: invadir um sistema para obter informações que a LAI classifica como sigilosas configura a **qualificadora** do §3º.

- A **LAI** protege a informação pessoal por até 100 anos e proíbe o uso indevido. A **Lei Carolina Dieckmann** pune criminalmente quem invade o sistema para acessar esses dados. São dois planos de proteção — **administrativo** (LAI) e **penal** (Lei 12.737) — que se complementam.

> [!note] Conexão com o que vem depois (aviso apenas)
> Quando você estudar a **Lei Geral de Proteção de Dados (LGPD)**, verá que a invasão de sistemas para obter dados pessoais também configura violação à LGPD, com sanções administrativas pecuniárias. A Lei Carolina Dieckmann e a LGPD, juntas, criam um duplo efeito: penal (multa e prisão) + administrativo (multa pela ANPD). Não antecipe esse conteúdo agora — apenas registre que a legislação de segurança da informática forma um **ecossistema**.

---

## 7. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **Lei 12.737/2012**, art. 2º: acrescentou os arts. **154-A e 154-B** ao Código Penal; sancionada em 30/11/2012, vigência em 02/04/2013
> - [ ] **Art. 154-A, caput:** invadir dispositivo informático **de uso alheio** (conectado ou não à rede) para obter/adulterar/destruir dados ou instalar vulnerabilidades, **sem autorização** — pena: **reclusão de 1 a 4 anos + multa**
> - [ ] **Redação original (2012):** exigia "mediante violação indevida de mecanismo de segurança"; a Lei 14.155/2021 **retirou** esse requisito
> - [ ] **Redação original (2012):** era "alheio" → atual: "**de uso alheio**"; "titular" → "**usuário**"
> - [ ] **Pena original:** **detenção** 3 meses–1 ano → atual: **reclusão** 1–4 anos; deixa de ser crime de menor potencial ofensivo
> - [ ] **§1º (equiparada):** quem produz, oferece, distribui, vende ou difunde programa/dispositivo para permitir a invasão → **mesma pena** do caput
> - [ ] **§2º (prejuízo econômico):** aumento de **1/3 a 2/3** (antes era 1/6 a 1/3)
> - [ ] **§3º (qualificadora):** obtenção de comunicações privadas, segredos comerciais/industriais, informações sigilosas (em lei), controle remoto não autorizado → **reclusão 2 a 5 anos + multa** (antes era 6 meses a 2 anos)
> - [ ] **§4º:** se os dados do §3º forem divulgados, comercializados ou transmitidos → aumento de **1/3 a 2/3**
> - [ ] **§5º:** causa de aumento (1/3 à metade) contra lista taxativa de autoridades (Presidente, governadores, prefeitos, Presidente do STF, presidentes de Casas legislativas, dirigentes da administração direta e indireta)
> - [ ] **Art. 154-B:** ação penal pública **condicionada à representação**; **exceção** (incondicionada) contra administração pública (direta/indireta, qualquer poder/ente) e **empresas concessionárias de serviços públicos**
> - [ ] **Representação ≠ queixa** — a ação é pública, não privada
> - [ ] **"Conectado ou não à rede"** — o dispositivo não precisa estar na internet
> - [ ] A qualificadora do §3º fala em **obtenção** (não em divulgação); a divulgação é §4º

> [!warning] O erro mais comum em prova
> **Confundir o que a lei pune hoje com o que punia antes.** O candidato que estuda a redação original (2012) sem olhar a atual cai em todas as pegadinhas: acha que é preciso "violar mecanismo de segurança", que a pena é de detenção, que o crime é de menor potencial ofensivo. **Estratégia:** Ao ver uma questão sobre a Lei Carolina Dieckmann, o primeiro passo é verificar se a banca está citando a **redação original** ou a **redação atual**. Se for uma questão genérica (sem data específica), aplique sempre a **redação vigente** (após Lei 14.155/2021). O edital cita a Lei 12.737/2012, mas o examinador espera que você saiba que o texto foi alterado — e é na alteração que estão as respostas.

---

## 8. Próximos passos

Você estudou agora a **Lei Carolina Dieckmann**, que introduziu no Código Penal a proteção penal contra invasões de dispositivos informáticos. Ela complementa a [[Lei-de-Acesso-a-Informacao-LAI|LAI]] no sentido de que, enquanto a LAI regula o *direito legítimo de acessar* e *protege* a informação, a Lei 12.737 **pune o acesso ilegítimo**.

O próximo tópico da ementa é:

- **Marco Civil da Internet (Lei nº 12.965/2014)** — que estabelece os princípios, garantias, direitos e deveres da internet no Brasil, incluindo privacidade, neutralidade de rede, responsabilidade dos provedores de internet e proteção dos dados pessoais dos usuários. É a ponte entre a proteção penal (Lei Carolina Dieckmann) e a proteção de dados (LGPD).

Depois virá a **LGPD (Lei nº 13.709/2018)**, o tema mais cobrado deste bloco, que desenvolverá em profundidade o tratamento de dados pessoais que a LAI apenas esboça no art. 31 e que a Lei Carolina Dieckmann protege criminalmente no art. 154-A.
