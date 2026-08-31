# Lei de Acesso à Informação — LAI (Lei nº 12.527/2011)

> [!info] Metadados
> **Disciplina:** Legislação de Segurança da Informação e LGPD
> **Bloco:** 1.3 — Legislação (FASE 1 — Fundamentos)
> **Tópico:** 1. Lei de Acesso à Informação — LAI (Lei 12.527/2011)
> **Subtópicos:** Princípio da publicidade e transparência · Classificação da informação (reservado, secreto, ultrassecreto) · Procedimento de requisição e prazos · Informações pessoais e dados sensíveis
> **Pré-requisitos:** Nenhum (a interpretação dos artigos se beneficia do raciocínio lógico já estudado na Fase 1)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-28

---

## 1. Por que estudar a Lei de Acesso à Informação?

Você inicia agora a disciplina de **Legislação de Segurança da Informação e LGPD**, o Bloco 1.3 da Fase 1 dos seus estudos. Este é o primeiro contato com a parte jurídica do conteúdo — e, diferente do que muitos candidatos imaginam, ela não é um "adendo" ao restante do edital. A ementa posiciona a legislação como **alicerce cognitivo**: é ela que dará embasamento jurídico ao módulo de Segurança da Informação (que você estudará bem mais adiante, na Fase 6) e ao tratamento de dados em sistemas — conexão imediata com Banco de Dados e Arquitetura de Software.

A **Lei de Acesso à Informação (LAI)**, Lei nº 12.527, de 18 de novembro de 2011, é a primeira das leis deste bloco. Ela regulamenta o direito de qualquer pessoa obter informações públicas do Estado. Não é exagero dizer que a LAI é o **marco da transparência** no Brasil: ela inverteu uma lógica histórica de que o que não era publicado era sigiloso, estabelecendo que a publicidade é a **regra** e o sigilo, a **exceção**.

> [!question] Pergunta orientadora
> Antes da LAI, se um cidadão quisesse saber quanto um órgão gastou em uma licitação, o que ele precisava fazer? Ele precisava *justificar* o interesse e convencer o órgão de que merecia a informação. A LAI mudou exatamente isso — por quê? Porque a informação pública é um **direito**, não um favor. E para ser direito, o pedido não pode depender de um "motivo justificável".

Para o seu cargo de **Analista de TI na DATAPREV**, essa lei tem peso concreto: você provavelmente trabalhará com sistemas que **armazenam, tratam e disponibilizam informações** — inclusive informações classificadas e dados pessoais — e precisará conhecer as regras de acesso, sigilo e responsabilidade que regem esse tratamento. A FGV costuma cobrar a LAI de forma **muito literal**, com foco em números (prazos) e nas estruturas de competência.

> [!tip] Palavras-chave que a banca usa (guarde desde já)
> **Publicidade como regra**, **sigilo como exceção**, **transparência ativa** e **passiva**, **SIC**, **graus de sigilo** (reservado, secreto, ultrassecreto), **informação sigilosa** vs. **informação pessoal**, **teste de dano** (imprescindibilidade à segurança da sociedade ou do Estado), **prazos** (5, 15, 25, 100 anos; 20+10 dias), **Comissão Mista de Reavaliação de Informações (CMRI)**.

Ao longo desta nota, vamos destrinchar cada um desses pontos em *prosa explicativa*, com exemplos e pegadinhas — porque é exatamente nas "pegadinhas de números" que as bancas perdem candidatos despreparados. Não decore primeiro: **compreenda a lógica**, e os números ficarão fixados com muito mais facilidade.

---

## 2. Princípio da publicidade e a transparência (quando o sigilo é a exceção)

### 2.1 A inversão da lógica: publicidade como regra

O coração filosófico da LAI está no **art. 3º**, que lista as diretrizes da lei. A primeira delas — e a mais cobrada — é a:

> [!important] Art. 3º, inciso I
> "Observância da **publicidade como preceito geral e do sigilo como exceção**."

O que isso significa na prática? Significa que **toda informação produzida ou custodiada pelo Estado é, em princípio, pública**. O sigilo não é a presunção; é uma exceção que precisa ser *justificada* e *formalizada*. Antes, o silêncio do Estado sobre um dado podia ser interpretado como "não posso mostrar". Agora, o silêncio sobre um dado *público* é ilegal: se não houver fundamento para classificar, o acesso deve ser concedido.

Vamos raciocinar com um caso concreto que ajuda a fixar a ideia:

> [!example] Exemplo — a mudança de padrão
> Um cidadão pede ao órgão X o valor pago a todos os servidores de um setor. Pela LAI, o órgão **deve** entregar. Se o órgão quiser negar, não basta dizer "não vou mostrar" — ele precisa demonstrar que aquela informação se enquadra em uma das hipóteses legais de restrição (por exemplo, tratar-se de informação pessoal ou classificada como sigilosa). **Quem invoca a exceção tem o ônus de provar que ela se aplica.**

As demais diretrizes do art. 3º completam esse quadro:

- **Inciso II** — divulgação de informações de interesse público **independentemente de solicitações** (é o germe da *transparência ativa*);
- **Inciso III** — utilização de **meios de comunicação viabilizados pela tecnologia da informação** (aqui entra a internet e os portais de transparência);
- **Inciso IV** — fomento à **cultura de transparência** na administração pública;
- **Inciso V** — desenvolvimento do **controle social** da administração pública.

> [!tip] Como a banca costuma cobrar
> Questões literais sobre o art. 3º pedem para identificar qual alternativa *não* é uma diretriz, ou para marcar a frase que melhor resume a inversão "regra x exceção". Lembre-se: **publicidade é a regra declarada textualmente**; qualquer alternativa que inverta — "sigilo como regra" ou "publicidade como exceção" — está errada.

### 2.2 Transparência ativa e passiva: as duas faces do acesso

A LAI prevê dois caminhos para a informação chegar ao cidadão: um em que o Estado age **por conta própria**, e outro em que ele reage a um **pedido**.

- **Transparência ativa** (art. 8º): o órgão **divulga** as informações de interesse coletivo ou geral *independentemente de requerimentos*. É o dever de publicar proativamente. A forma mais visível disso é a divulgação obrigatória em **sítios oficiais da internet** (art. 8º, §2º).
- **Transparência passiva** (art. 9º, I; arts. 10 e 11): o órgão responde a **pedidos individuais** de acesso, apresentados por qualquer interessado. O principal instrumento é o **Serviço de Informações ao Cidadão (SIC)**, previsto no art. 9º.

Detalhe importante: o art. 9º prevê o SIC em **todos** os órgãos e entidades do poder público, com a função de atender e orientar o público, informar sobre a tramitação de documentos e **protocolizar** pedidos de acesso.

> [!warning] PEGADINHA nº 1 — "transparência ativa" vs. "divulgação espontânea"
> "Ativa" **não** significa "ágil" nem "sem custo". **Transparência ativa** = informação divulgada *de ofício*, sem que ninguém peça. **Transparência passiva** = informação entregue *em resposta a um pedido*. A banca adora trocar essas palavras: falar que transparência ativa é "aquela que atende a um pedido imediatamente" — errado, isso é passiva.

O art. 8º é um dos mais ricos da lei em detalhes cobráveis. O §1º lista o que deve constar na divulgação ativa, no mínimo:

1. registro das **competências e estrutura organizacional**, endereços, telefones e horários de atendimento;
2. registros de **repasses ou transferências de recursos financeiros**;
3. registros das **despesas**;
4. informações sobre **licitações**, editais, resultados e **contratos**;
5. dados gerais para o acompanhamento de **programas, ações, projetos e obras**;
6. **respostas a perguntas mais frequentes** da sociedade.

E o §3º exige que os sítios atendam a requisitos como: ferramenta de **pesquisa de conteúdo**; possibilidade de **gravar relatórios em formatos abertos e não proprietários**; acesso automatizado por sistemas externos; garantia da **autenticidade e integridade** das informações; e **acessibilidade** para pessoas com deficiência.

> [!warning] PEGADINHA nº 2 — municípios de pequeno porte
> O art. 8º, §4º, **dispensa** os Municípios com população de **até 10.000 (dez mil) habitantes** da divulgação obrigatória na internet — mas mantém a obrigatoriedade de divulgar, em tempo real, as informações de **execução orçamentária e financeira** (nos termos da Lei de Responsabilidade Fiscal). É uma exceção que já caiu e pode cair de novo: pequeno município não é totalmente isento; ele só fica liberado do site, não da transparência.

### 2.3 O dever estatal e os direitos do cidadão

O **art. 5º** enuncia o dever geral: "É dever do Estado garantir o direito de acesso à informação, que será franqueada, mediante **procedimentos objetivos e ágeis**, de forma **transparente, clara e em linguagem de fácil compreensão**."

Já o **art. 7º** detalha o que esse direito compreende — ou seja, *o que* o cidadão pode obter:

- **orientação** sobre como acessar a informação;
- **informação contida em registros ou documentos**, produzidos ou acumulados pelos órgãos, recolhidos ou não a arquivos públicos;
- informação produzida ou custodiada por **pessoa física ou entidade privada** em razão de vínculo com órgãos públicos (mesmo se o vínculo já cessou);
- informação **primária, íntegra, autêntica e atualizada**;
- informação sobre as **atividades** dos órgãos e entidades;
- informação sobre **administração do patrimônio público, licitações e contratos**;
- informação relativa à implementação de **programas e ações**, e ao resultado de **inspeções, auditorias e tomadas de contas**.

O §1º do art. 7º traz uma ressalva importante: o acesso **não compreende** informações referentes a projetos de pesquisa e desenvolvimento científicos ou tecnológicos **cujo sigilo seja imprescindível à segurança da sociedade e do Estado**. E o §2º garante o **acesso parcial**: se a informação for parcialmente sigilosa, deve ser assegurado o acesso à parte não sigilosa por meio de certidão, extrato ou cópia com ocultação da parte sob sigilo.

> [!question] Pergunta orientadora
> Por que a lei garante o acesso à parte *não* sigilosa de um documento parcialmente sigiloso? Porque a publicidade é a regra e o sigilo, a exceção restrita. Se fosse possível negar o documento inteiro por causa de um trecho sigiloso, a exceção "engoliria" a regra. O sigilo deve ser o **menor possível** — veremos essa mesma lógica no critério de classificação (art. 24, §5º).

---

## 3. Classificação da informação: os graus de sigilo e prazos

### 3.1 Quando uma informação pode ser sigilosa: o "teste de dano" (art. 23)

Nem toda informação pode ser classificada. A LAI é rigorosa: a classificação só é permitida quando a informação é considerada **imprescindível à segurança da sociedade ou do Estado**, porque sua divulgação ou acesso irrestrito **possa** causar determinados danos. Esse "poder causar dano" é conhecido nas provas como o **teste de dano** — a informação precisa, em abstrato, ameaçar algum interesse protegido.

O **art. 23** lista, em oito incisos, as hipóteses de informações passíveis de classificação. São elas, quando a divulgação puder: pôr em risco a **defesa e a soberania nacionais** ou a **integridade do território**; prejudicar a **condução de negociações ou relações internacionais**; pôr em risco a **vida, a segurança ou a saúde da população**; oferecer **elevado risco à estabilidade financeira, econômica ou monetária** do País; prejudicar **planos ou operações estratégicas das Forças Armadas**; prejudicar **projetos de pesquisa e desenvolvimento científico ou tecnológico** e sistemas de interesse estratégico; pôr em risco a **segurança de instituições ou altas autoridades**; ou comprometer **atividades de inteligência e investigações** em andamento.

> [!warning] PEGADINHA nº 3 — o fundamento da classificação
> A banca frequentemente tenta confundir *quando* algo pode ser sigiloso com *o que* é sigiloso por definição. Lembre-se do **art. 23**: a classificação exige que a informação seja *imprescindível à segurança da sociedade ou do Estado* **e** que caia em uma das hipóteses de dano. Sem esse duplo requisito, a informação é pública. Uma informação "constrangedora para um gestor" **jamais** pode ser classificada — não passa no teste de dano.

### 3.2 Os três graus de sigilo e seus prazos (art. 24)

A informação classificada recebe **um** dos três graus de sigilo. É aqui que mora a **maior concentração de pegadinhas numéricas** de toda a disciplina — memorize os valores com atenção máxima:

| Grau de sigilo | Prazo máximo de restrição de acesso |
|:---|:---:|
| **Reservado** | **5 anos** |
| **Secreto** | **15 anos** |
| **Ultrassecreto** | **25 anos** |

> [!important] Regra de ouro dos prazos
> **Reservado = 5 · Secreto = 15 · Ultrassecreto = 25.** Note que os prazos contam **a partir da data de produção** da informação (art. 24, §1º) — não da data da classificação nem do pedido. Esse é um detalhe que decide questões.

O grau **ultrassecreto** tem uma particularidade extra já no art. 24 e uma prorrogação especial. O art. 24, §2º, traz uma regra *sui generis*: as informações que puderem colocar em risco a segurança do **Presidente e Vice-Presidente da República** e respectivos cônjuges e filhos são classificadas como **reservadas** e ficam sob sigilo até o **término do mandato em exercício** (ou do último mandato, em caso de reeleição) — mesmo que isso ultrapasse os cinco anos usuais do grau reservado.

O §3º permite que, em vez de prazo fixo, o termo final da restrição seja a **ocorrência de determinado evento**, desde que este ocorra antes do prazo máximo de classificação. E o §5º impõe o critério mais importante da classificação: deve-se usar o **interesse público** e o **critério menos restritivo possível**, considerando a gravidade do risco e o prazo de restrição.

> [!tip] O "critério menos restritivo" é um conceito-chave
> Quando duas classificações são possíveis, o agente deve escolher o grau que menos restrinja o acesso — ou seja, se a informação se enquadra em reservado e em secreto, classifica-se como **reservado**. Isso materializa a regra de que o sigilo é exceção: a exceção deve ser a menor possível.

### 3.3 A prorrogação do ultrassecreto (a pegadinha do 25 + 25 = 50)

O prazo de 25 anos do ultrassecreto **pode ser prorrogado** — mas com condições muito específicas, previstas na **Comissão Mista de Reavaliação de Informações (CMRI)**, do art. 35 da LAI. Leia com atenção:

> [!important] Prorrogação do ultrassecreto (art. 35, §1º, III, e §2º)
> A CMRI pode prorrogar o prazo de sigilo da informação **ultrassecreta** por **uma única renovação**, sempre por **prazo determinado**, enquanto o acesso ou a divulgação puder ocasionar **ameaça externa à soberania nacional ou à integridade do território nacional, ou grave risco às relações internacionais** do País. A renovação é limitada a **até 25 anos**, e o **prazo total** da classificação fica limitado ao máximo de **50 anos**.

> [!warning] PEGADINHA nº 4 — a renovação é só do ultrassecreto
> A possibilidade de prorrogação **não** se aplica aos graus secreto (15) e reservado (5) — somente ao **ultrassecreto**. E, mesmo para ele, a renovação é **uma única vez**, com limite total de 50 anos, e exige hipótese gravíssima (ameaça externa à soberania ou à integridade do território). Questão que disser que "reservado pode ser renovado" está errada.

Outra regra temporal do art. 35, §3º e §4º: a CMRI deve realizar a **revisão de ofício** das informações ultrassecretas ou secretas, no máximo, a cada **4 anos**; se não deliberar nos prazos, as informações são **desclassificadas automaticamente**. E o **art. 39** obrigou os órgãos a reavaliarem, em até **2 anos** da vigência da lei, as informações já classificadas como ultrassecretas e secretas que existiam antes dela — as que não fossem reavaliadas se tornariam automaticamente públicas.

### 3.4 Quem tem competência para classificar (art. 27)

A classificação não pode ser feita por qualquer servidor: a LAI reserva essa competência a autoridades específicas, dispostas no **art. 27**, de forma escalonada conforme o grau.

- **Grau ultrassecreto:** Presidente da República; Vice-Presidente; **Ministros de Estado** e autoridades com as mesmas prerrogativas; **Comandantes da Marinha, Exército e Aeronáutica**; e **Chefes de Missões Diplomáticas e Consulares permanentes no exterior**.
- **Grau secreto:** todas as anteriores **mais** os titulares de **autarquias, fundações, empresas públicas e sociedades de economia mista**.
- **Grau reservado:** todas as anteriores **mais** as que exerçam funções de **direção, comando ou chefia** de nível **DAS 101.5 ou superior** (ou hierarquia equivalente).

O **§1º** do art. 27 permite a **delegação** da competência de classificar como ultrassecreta e secreta — mas **veda expressamente a subdelegação**. O §2º exige que a classificação ultrassecreta feita por comandantes das Forças e chefes de missões diplomáticas seja **ratificada** pelos respectivos Ministros de Estado, no prazo do regulamento. E o §3º obriga quem classificar informação como ultrassecreta a **encaminhar a decisão à CMRI**.

A classificação deve ser **formalizada em decisão escrita** — o art. 28 exige, no mínimo: o **assunto**; o **fundamento da classificação** (critérios do art. 24); a **indicação do prazo** de sigilo ou do evento que defina o termo final; e a **identificação da autoridade** que classificou. O Decreto 7.724 materializou essa formalização no **Termo de Classificação de Informação (TCI)**.

> [!question] Pergunta orientadora
> Por que é preciso *formalizar* a classificação em decisão com fundamento e autoridade identificada? Reflita: se o sigilo é uma exceção, ele precisa ser *rastreável*. A pessoa que classificou deve responder por isso; e quem teve o acesso negado deve saber a quem recorrer (para pedir desclassificação). Sem formalização, não há como fiscalizar — e a exceção vira arbítrio.

O **art. 30** impõe transparência até sobre o sigilo: a autoridade máxima de cada órgão deve publicar, **anualmente**, em sítio na internet, o **rol das informações desclassificadas** nos últimos 12 meses, o **rol de documentos classificados** em cada grau, e um **relatório estatístico** com a quantidade de pedidos recebidos, atendidos e indeferidos. Ou seja: o próprio universo das informações sigilosas é, em certa medida, concreto e auditável.

### 3.5 Restrições que nunca podem vingar (art. 21)

A LAI também diz o que **jamais** pode ser restringido — e isso é outro ponto de pegadinha. O **art. 21**:

> [!important] Art. 21
> "Não poderá ser negado acesso à informação **necessária à tutela judicial ou administrativa de direitos fundamentais**."
> **Parágrafo único:** "As informações ou documentos que versem sobre condutas que impliquem **violação dos direitos humanos** praticada por agentes públicos ou a mando de autoridades públicas **não poderão ser objeto de restrição de acesso**."

Em outras palavras: mesmo que uma informação se enquadre formalmente nas hipóteses de sigilo, ela **não pode ser classificada** se for essencial à proteção de direitos fundamentais, e é **impossível** restringir informação sobre violações de direitos humanos por agentes do Estado. O sigilo cede diante da dignidade e dos direitos fundamentais.

> [!warning] PEGADINHA nº 5 — o sigilo não protege a ilicitude
> Na esfera administrativa, o art. 31, §4º, reforça ideia semelhante: a restrição de acesso a informação relativa à vida privada, honra e imagem **não pode** ser invocada para prejudicar a apuração de irregularidades em que o titular esteja envolvido nem ações de recuperação de fatos históricos relevantes. O sigilo protege o cidadão comum — não serve de escudo para quem deve prestar contas.

O **art. 22** fecha o quadro das restrições: a LAI **não exclui** as demais hipóteses legais de sigilo e segredo de justiça, nem o **segredo industrial** decorrente da exploração direta de atividade econômica pelo Estado ou por quem esteja vinculado ao poder público.

---

## 4. O procedimento de requisição: como pedir, prazos e recursos

### 4.1 O pedido de acesso (art. 10) e a resposta (art. 11)

O **art. 10** é o ponto de partida: *qualquer* interessado pode apresentar pedido de acesso, **por qualquer meio legítimo**, bastando conter a **identificação do requerente** e a **especificação da informação requerida**. Três garantias importantes acompanham esse artigo:

- **§1º:** para informação de interesse público, a identificação **não pode conter exigências que inviabilizem** a solicitação;
- **§2º:** os órgãos devem **viabilizar pedidos pelos sítios oficiais na internet**;
- **§3º:** são **vedadas quaisquer exigências relativas aos motivos** determinantes da solicitação de informações de interesse público.

> [!warning] PEGADINHA nº 6 — não se pode exigir "motivo"
> A LAI **proíbe** que o órgão pergunte ao cidadão *por que* ele quer a informação de interesse público. Exigir justificativa para o interesse público é ilegal. Esse é um clássico: a alternativa que diz "o cidadão deve justificar o interesse" está errada.

O **art. 11** regula a resposta. A regra é o **acesso imediato** à informação disponível. Se não for possível o acesso imediato, o órgão tem prazo de até **20 dias** para, cumulativa ou alternativamente conforme o caso: comunicar a data, local e modo da consulta/reprodução/certidão; indicar as **razões de fato ou de direito da recusa**; ou comunicar que **não possui a informação** e indicar quem a detém (ou remeter o pedido). Esse prazo de 20 dias pode ser **prorrogado por mais 10 dias, mediante justificativa expressa**, da qual o requerente será **cientificado** (art. 11, §2º).

> [!important] Prazos de resposta — fixe este par
> **Resposta em até 20 dias, prorrogáveis por mais 10** (com justificativa expressa e ciência ao requerente). Total máximo: **30 dias**. Cuidado: a prorrogação não é automática nem arbitrária — exige justificativa e comunicação formal. As bancas perguntam o número exato e a condição da prorrogação.

O §4º do art. 11 trata da negativa por sigilo: quando o acesso for negado por informação total ou parcialmente sigilosa, o requerente deve ser informado sobre a **possibilidade de recurso, prazos e condições**, devendo ser-lhe indicada a **autoridade competente** para apreciação. Já o §5º diz que informação armazenada em formato digital será fornecida nesse formato, se houver anuência do requerente.

### 4.2 Custo e gratuidade (art. 12)

O **art. 12** (redação dada pela Lei 14.129/2021) estabelece que o serviço de **busca e fornecimento** da informação é **gratuito**. É possível cobrar **exclusivamente** o valor necessário ao **ressarcimento dos custos** quando o serviço exigir **reprodução de documentos**. E quem não possa arcar com esse custo **sem prejuízo do sustento próprio ou da família** (situação econômica declarada) fica **isento**.

> [!tip] Nuance cobrável
> A *busca* e o *fornecimento* são livres de custo; o que pode ser cobrado é apenas o **ressarcimento dos custos de reprodução** de documentos — e ainda assim com isenção para quem declare não ter condições. Cobrar "taxa de atendimento" é ilegal.

### 4.3 O fluxo recursal: as instâncias e seus prazos

Quando o órgão **indefere** o acesso ou não informa as razões da negativa, o cidadão pode **recorrer**. Este é o processo mais cobrado em fluxograma — e o lugar onde o candidato precisa **não misturar os prazos**.

Vamos entender o fluxo *geral* da LAI (arts. 15 a 18) no **Poder Executivo Federal**, que é o foco do edital:

**1ª instância — recurso à autoridade hierarquicamente superior (art. 15):**
- O interessado interpõe recurso contra a decisão no prazo de **10 dias** da ciência.
- O recurso é dirigido à autoridade **hierarquicamente superior** à que exarou a decisão, que deve se manifestar em **5 dias**.

**2ª instância — recurso à autoridade máxima do órgão:**
- Previsto no **Decreto 7.724/2012**: caso a 1ª instância mantenha a negativa, cabe novo recurso à **autoridade máxima** do órgão ou entidade, também com **10 dias para interpor** e **5 dias para decidir**.

**3ª instância — recurso à Controladoria-Geral da União (art. 16):**
- Esgotadas as instâncias internas, o requerente pode recorrer à **CGU**, que deliberará em **5 dias**, nas hipóteses do art. 16: (I) negado acesso a informação **não classificada** como sigilosa; (II) a decisão de negativa de acesso a informação **parcialmente sigilosa não indicar a autoridade classificadora** ou a hierarquicamente superior; (III) não observados os **procedimentos de classificação**; ou (IV) descumpridos **prazos ou procedimentos**.
- **Importante (art. 16, §1º):** o recurso à CGU **só pode ser dirigido após a apreciação de pelo menos uma autoridade hierarquicamente superior** — ou seja, não há recurso "direto" à CGU.

**Última instância — Comissão Mista de Reavaliação de Informações (art. 16, §3º, e art. 35):**
- Negado o acesso pela CGU, o interessado pode recorrer à **CMRI**. A CMRI também julga recursos em pedidos de **desclassificação** (art. 17) e pode rever a classificação de informações ultrassecretas e secretas.

> [!warning] PEGADINHA nº 7 — os prazos de *interpor* vs. de *decidir*
> Não confunda: o **prazo para interpor** o recurso (do cidadão) é de **10 dias**; o **prazo para a autoridade decidir** é de **5 dias**. Questões perguntam "em quantos dias o cidadão deve recorrer?" → 10. E "em quantos dias a autoridade deve responder o recurso?" → 5. São números diferentes de um mesmo processo.

> [!warning] PEGADINHA nº 8 — "recurso à CGU" não é a primeira opção
> O recurso à CGU é previsto apenas para o **Poder Executivo Federal**, e somente **depois** de passar por pelo menos uma autoridade superior. Além disso, o art. 18 lembra que os **Poderes Legislativo e Judiciário e o Ministério Público** regulamentam seus próprios procedimentos de revisão de decisões denegatórias nos seus âmbitos — a estrutura da CGU é específica do Executivo.

Para visualizar o processo completo, veja o fluxograma:

```text
Pedido de acesso ao órgão (art. 10)
        │
        ▼
RESPOSTA (art. 11): imediata ou em até 20 dias
        │                        (+10 dias prorrogáveis com justificativa)
        ▼
┌─────────────────────────────────────────────┐
│  Se NEGADO / razões não informadas          │
└──────────────────────────┬──────────────────┘
                           ▼
      1º recurso → autoridade hierarquicamente superior  (art. 15)
      interpor: 10 dias | decidir: 5 dias
                           │ se mantida a negativa
                           ▼
      2º recurso → autoridade máxima do órgão (Decreto 7.724)
      interpor: 10 dias | decidir: 5 dias
                           │ se mantida a negativa (Poder Executivo Federal)
                           ▼
      3º recurso → Controladoria-Geral da União (art. 16)
      deliberar: 5 dias
      (exige prévia apreciação de ao menos uma autoridade superior)
                           │ se mantida a negativa
                           ▼
      4º recurso → Comissão Mista de Reavaliação de Informações (CMRI)
      (art. 16, §3º, e art. 35)
```

> [!question] Pergunta orientadora
> Por que existem tantas instâncias recursais? Porque o direito de acesso é fundamental e o cidadão não pode ficar refém de uma única decisão de um único agente. A gradação — autoridade superior, autoridade máxima, CGU, CMRI — cria controles sucessivos e dá ao requerente caminhos para contestar a negativa, inclusive questionando a própria classificação.

### 4.4 O Serviço de Informações ao Cidadão (SIC) e a desclassificação

O **SIC**, criado pelo art. 9º da LAI e detalhado no Decreto 7.724/2012 (arts. 9º e 10), é o **ponto de contato** entre o cidadão e o órgão: recebe pedidos de acesso, registra em sistema eletrônico (entregando **número de protocolo** com a data), orienta o público e encaminha o pedido à unidade responsável. Ele deve estar instalado em **unidade física identificada, de fácil acesso e aberta ao público**.

Há também o procedimento específico de **pedido de desclassificação** (Decreto 7.724/2012, arts. 36 e 37): o pedido de desclassificação ou reavaliação é dirigido à **autoridade classificadora**, que decide em **30 dias**; negado, cabe recurso em **10 dias** ao **Ministro de Estado** (ou dirigente máximo, ou Comandante, nas Forças, ou ao Ministro da Defesa), que decide em **30 dias**; e, desprovido, cabe recurso em **10 dias** à **CMRI**. Note que pedido de desclassificação **não se confunde** com pedido de acesso: são ritos e processos distintos.

> [!tip] Palavras-chave do procedimento
> Qualquer interessado · identificação + especificação · qualquer meio legítimo · acesso imediato · 20 (+10) dias · recurso (10 p/ interpor, 5 p/ decidir) · CGU (5 dias) · CMRI · SIC · protocolo · desclassificação (30/10/30 dias).

---

## 5. Informações pessoais e dados sensíveis (art. 31)

### 5.1 A proteção da informação pessoal

O **art. 31** trata das **informações pessoais** — aquelas relativas à **pessoa natural identificada ou identificável** (definição do art. 4º, IV). A regra central está no §1º:

> [!important] Art. 31, §1º
> As informações pessoais relativas à **intimidade, vida privada, honra e imagem**:
>
> - **I** — terão seu acesso **restrito, independentemente de classificação de sigilo** e pelo prazo **máximo de 100 (cem) anos** a contar da data de produção, a **agentes públicos legalmente autorizados** e à **própria pessoa** a que se referirem;
> - **II** — poderão ter sua divulgação ou acesso por terceiros autorizados diante de **previsão legal** ou **consentimento expresso** da pessoa a que se referirem.

Guarde o número mais importante deste artigo: **100 anos**. E compreenda a distinção conceitual essencial:

> [!warning] PEGADINHA nº 9 — informação pessoal NÃO é informação classificada
> A informação pessoal tem acesso restrito **independentemente de classificação de sigilo** e pelo prazo máximo de **100 anos**. Já a informação sigilosa (classificada) depende de classificação formal e tem prazos de **5, 15 ou 25 anos**. São regimes **diferentes**! A informação pessoal é protegida em razão da **privacidade**; a informação classificada é protegida em razão da **segurança da sociedade ou do Estado**. Questão que misturar os dois e aplicar o prazo errado está errada.

O **§2º** responsabiliza quem obtiver acesso a essas informações por seu **uso indevido**. E o **§3º** lista as hipóteses em que o **consentimento não será exigido** para o tratamento (ou seja, em que a informação pessoal pode ser usada sem o "sim" do titular):

1. **prevenção e diagnóstico médico**, quando a pessoa estiver física ou legalmente **incapaz**, e para uso exclusivo do tratamento médico;
2. realização de **estatísticas e pesquisas científicas** de evidente interesse público ou geral, previstas em lei, **vedada a identificação** da pessoa;
3. **cumprimento de ordem judicial**;
4. **defesa de direitos humanos**;
5. **proteção do interesse público e geral preponderante**.

> [!question] Pergunta orientadora
> Por que algumas hipóteses dispensam o consentimento? Porque em certas situações o interesse protegido é tão relevante (vida, saúde, justiça, direitos humanos) que não seria razoável exigir a concordância do titular — ou porque, na prática, ele não tem como manifestá-la (caso do incapaz no diagnóstico médico). A regra geral é o consentimento; as exceções são taxativas.

O **§4º** — já mencionado na seção 3.5 — impede que a restrição de acesso à informação sobre vida privada, honra e imagem seja usada para **prejudicar apuração de irregularidades** em que o titular esteja envolvido ou ações de recuperação de **fatos históricos de maior relevância**.

> [!note] Conexão com o que vem depois (aviso apenas)
> Você reparou que a LAI já fala em proteção de dados pessoais? Esse é o embrião conceitual da **Lei Geral de Proteção de Dados (LGPD)** e também dialoga com o **Marco Civil** e a **Lei Carolina Dieckmann** — todas estudadas **mais adiante** neste mesmo bloco. Por enquanto, a única coisa que você precisa guardar é: a LAI **protege a informação pessoal** (por isso o regime de 100 anos e a vedação de uso indevido); os detalhes de tratamento, bases legais e autoridade fiscalizadora vêm **depois**, com a LGPD. Não se antecipe — apenas saiba que essa semente será desenvolvida.

---

## 6. Restrições e exceções de acesso (síntese do Capítulo IV)

O Capítulo IV da LAI reúne as "barreiras" legítimas ao acesso. Vale organizá-las em uma visão clara, porque as bancas testam exatamente a capacidade de **separar o que pode do que não pode ser restringido**:

| Espécie | Legítima restrição? | Fundamento |
|:---|:---:|:---|
| Informação **sigilosa** (classificada) | Sim, por prazo limitado | arts. 23 e 24 (graus e prazos) |
| **Informação pessoal** | Sim, por até **100 anos** | art. 31 |
| Demais **hipóteses legais de sigilo** e **segredo de justiça** | Sim | art. 22 |
| **Segredo industrial** do Estado / vinculados ao poder público | Sim | art. 22 |
| Informação **necessária à tutela de direitos fundamentais** | **Não** | art. 21 |
| Informação sobre **violação de direitos humanos** por agentes do Estado | **Nunca** | art. 21, parágrafo único |

> [!warning] PEGADINHA nº 10 — quando o sigilo NÃO protege
> Três situações em que o desejo de "esconder" é barrado pela lei: (1) informação necessária à tutela de direitos fundamentais (art. 21); (2) informação sobre violações de direitos humanos (art. 21, parágrafo único); (3) informação sobre irregularidade usada para proteger o titular (art. 31, §4º). Em qualquer destas, a classificação ou a restrição **não pode prosperar** — mesmo que a informação, em tese, se enquadrasse em hipóteses de sigilo.

---

## 7. Sanções e responsabilidades (Capítulo V)

A LAI não se limita a *garantir* o acesso; ela **pune** quem o descumpre. O **art. 32** lista as condutas ilícitas que ensejam responsabilidade do **agente público ou militar**. São elas:

1. **recusar-se a fornecer** informação requerida, **retardar deliberadamente** o fornecimento, ou fornecê-la **intencionalmente** de forma incorreta, incompleta ou imprecisa;
2. **utilizar indevidamente** (bem como subtrair, destruir, inutilizar, desfigurar, alterar ou ocultar) informação sob guarda ou acesso em razão do cargo, emprego ou função;
3. **agir com dolo ou má-fé** na análise das solicitações de acesso;
4. **divulgar ou permitir a divulgação**, ou **acessar ou permitir acesso indevido**, a informação sigilosa ou pessoal;
5. **impor sigilo** à informação para obter proveito pessoal ou de terceiro, ou para **ocultar ato ilegal** cometido por si ou por outrem;
6. **ocultar da revisão** de autoridade superior informação sigilosa para beneficiar a si ou a outrem, ou em prejuízo de terceiros;
7. **destruir ou subtrair** documentos concernentes a possíveis **violações de direitos humanos** por parte de agentes do Estado.

> [!warning] PEGADINHA nº 11 — o "dolo" aparece no erro de conteúdo
> Atenção à palavra **intencionalmente** no inciso I: fornecer a informação *errada por erro honesto* não configura a conduta ilícita em si; o que o art. 32 pune é o fornecimento **intencional e incorreto**. E o inciso III fala em **dolo ou má-fé**. A banca pode inserir "mesmo sem intenção" para tentar te enganar — a conduta ilícita exige dolo/intencionalidade ou retardo deliberado.

As **consequências** dessas condutas (art. 32, §§1º e 2º) são: no âmbito da Lei 8.112 (regime dos servidores federais), **infrações administrativas** apenadas, no mínimo, com **suspensão**; nas Forças Armadas, **transgressões militares** médias ou graves, desde que não tipificadas como crime ou contravenção; e o agente pode responder também por **improbidade administrativa** (Leis 8.429/1992 e 1.079/1950).

Já o **art. 33** trata das sanções à **pessoa física ou entidade privada** que detiver informações por vínculo com o poder público e descumprir a LAI:

1. **advertência**;
2. **multa**;
3. **rescisão do vínculo** com o poder público;
4. **suspensão temporária** de participar em licitação e impedimento de contratar com a administração pública por prazo **não superior a 2 anos**;
5. **declaração de inidoneidade** para licitar ou contratar, até a **reabilitação** perante a própria autoridade que aplicou a penalidade.

O **art. 34** fixa que os **órgãos e entidades públicas respondem diretamente** pelos danos causados por divulgação não autorizada ou uso indevido de informações sigilosas ou pessoais, cabendo apuração de responsabilidade funcional nos casos de **dolo ou culpa**, com **direito de regresso**. Essa responsabilização também se aplica à pessoa física ou entidade privada vinculada ao poder público.

---

## 8. Os decretos regulamentadores: Decreto 7.724/2012 e Decreto 7.845/2012

A LAI foi regulamentada por dois decretos que costumam aparecer juntos nas questões. Vale diferenciá-los com precisão.

### 8.1 Decreto nº 7.724/2012 — a regulamentação da LAI no Executivo Federal

Este decreto **regulamenta, no âmbito do Poder Executivo federal**, os procedimentos para a garantia do acesso à informação e para a classificação de informações sob restrição de acesso. É ele que:

- institui e disciplina o **SIC** (arts. 9º e 10);
- detalha o **procedimento de pedido de acesso**, com a regra dos **20 dias prorrogáveis por mais 10** (arts. 15 e 16);
- prevê os **recursos** (inclusive a 2ª instância perante a autoridade máxima e a 3ª perante a CGU — art. 23);
- detalha a **classificação** (TCI, critérios, prazos), a **reavaliação** e a **desclassificação**;
- exige a **divulgação** de informações de transparência ativa e o fornecimento dos **CIDIC** para a publicação na internet (art. 45).

> [!tip] Foco no decreto
> Para este edital, guarde do Decreto 7.724: ele vale **somente para o Poder Executivo federal**; é nele que aparecem o **SIC**, a regra dos **20+10 dias** e os **procedimentos de classificação** (TCI) e desclassificação.

### 8.2 Decreto nº 7.845/2012 — o tratamento da informação classificada

Este decreto tem escopo **mais restrito e técnico**: ele **regulamenta procedimentos para o credenciamento de segurança e o tratamento de informação classificada em qualquer grau de sigilo**, e dispõe sobre o **Núcleo de Segurança e Credenciamento (NSC)**. É aqui que entram conceitos como:

- **credenciamento de segurança** (habilitação de pessoas, órgãos e entidades para tratar informação classificada);
- **credencial de segurança** (certificado que autoriza a pessoa para esse tratamento);
- **Termo de Compromisso de Manutenção de Sigilo (TCMS)**, assinado por pessoa não credenciada que, excepcionalmente, acessa informação classificada;
- **Código de Indexação de Documento que Contém Informação Classificada (CIDIC)**;
- medidas de **cifração** e uso de **algoritmo de Estado** para proteção da informação sigilosa.

> [!warning] PEGADINHA nº 12 — não confundir os dois decretos
> **7.724** = acesso à informação e classificação (o "como o cidadão acessa" + regras de classificação e prazos). **7.845** = credenciamento e tratamento seguro da informação *já classificada* (o "como o servidor protege o sigilo"). Questões que trocam o foco — dizendo que o 7.845 cuida do acesso do cidadão — estão erradas. Este é um alvo clássico de pegadinha por confusão de arquivo.

---

## 9. Glossário e palavras-chave

Reúna aqui as palavras que a banca usa como "atalho" para identificar o tema de cada questão:

| Termo | Significado na LAI |
|:---|:---|
| **Informação** | Dados, processados ou não, utilizáveis para produção e transmissão de conhecimento, em qualquer meio, suporte ou formato (art. 4º, I) |
| **Documento** | Unidade de registro de informações, qualquer que seja o suporte ou formato (art. 4º, II) |
| **Informação sigilosa** | Submetida temporariamente à restrição de acesso em razão da **imprescindibilidade para a segurança da sociedade e do Estado** (art. 4º, III) |
| **Informação pessoal** | Relacionada à pessoa natural identificada ou identificável (art. 4º, IV) |
| **Tratamento da informação** | Conjunto de ações: produção, recepção, classificação, utilização, acesso, reprodução, transporte, transmissão, distribuição, arquivamento, armazenamento, eliminação, avaliação, destinação ou controle (art. 4º, V) |
| **Disponibilidade** | Qualidade da informação que pode ser conhecida e utilizada por indivíduos, equipamentos ou sistemas **autorizados** (art. 4º, VI) |
| **Autenticidade** | Qualidade de ter sido produzida, expedida, recebida ou modificada por determinado indivíduo, equipamento ou sistema (art. 4º, VII) |
| **Integridade** | Qualidade de não ter sido modificada, inclusive quanto à origem, trânsito e destino (art. 4º, VIII) |
| **Primariedade** | Qualidade de ter sido coletada na fonte, com máximo detalhamento, sem modificações (art. 4º, IX) |
| **Transparência ativa** | Divulgação de informação de interesse público **independentemente de requerimentos** (art. 8º) |
| **Transparência passiva** | Atendimento a **pedidos** de acesso (arts. 9º a 14) |
| **SIC** | Serviço de Informações ao Cidadão — ponto de contato para receber, registrar e orientar pedidos (art. 9º) |
| **Informação imprescindível** | Aquela cuja divulgação ou acesso irrestrito **pode causar dano** à segurança da sociedade ou do Estado (art. 23) |
| **CMRI** | Comissão Mista de Reavaliação de Informações — decide sobre tratamento e classificação de sigilo; julga recursos; prorroga ultrassecreto (art. 35) |
| **TCI** | Termo de Classificação de Informação — formaliza a classificação (Decreto 7.724) |
| **CIDIC** | Código de Indexação de Documento que contém Informação Classificada (Decreto 7.845) |

> [!tip] Trinca da disponibilidade/autenticidade/integridade
> Note que a LAI definiu esses três termos (art. 4º, VI, VII e VIII) — eles guardam forte paralelo com a **Tríade CID** (Confidencialidade, Integridade, Disponibilidade) que você estudará na disciplina de Segurança da Informação. Por ora, basta conhecer as definições **literais** da LAI, pois a banca pode pedir o conceito exato.

---

## 10. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **Art. 3º:** publicidade como **preceito geral**, sigilo como **exceção**; diretrizes: divulgação independente de solicitação, tecnologia da informação, cultura de transparência, controle social
> - [ ] **Transparência ativa** (art. 8º, divulgação de ofício, sítios oficiais) vs. **passiva** (art. 9º-14, resposta a pedidos, via **SIC**)
> - [ ] **Art. 8º, §4º:** Municípios com até **10.000 habitantes** dispensados do site na internet, mas **não** da transparência orçamentária em tempo real
> - [ ] **Art. 10:** qualquer interessado, qualquer meio legítimo, identificação + especificação; **vedada** exigência de motivos para interesse público
> - [ ] **Art. 11:** acesso **imediato**; senão, **20 dias**, prorrogáveis por **+10** com justificativa expressa e ciência ao requerente (total 30)
> - [ ] **Art. 12:** busca e fornecimento **gratuitos**; apenas ressarcimento de custos de **reprodução**; isenção para quem declare incapacidade
> - [ ] **Art. 23:** classificação exige **imprescindibilidade à segurança da sociedade ou do Estado** + oito hipóteses de dano (teste de dano)
> - [ ] **Graus e prazos (art. 24):** reservado **5** · secreto **15** · ultrassecreto **25** anos, contados da **produção**; critério **menos restritivo possível**
> - [ ] **Ultrassecreto:** prorrogável **uma única vez** pela CMRI, até **+25 anos** (total máx. **50**), apenas em ameaça externa à soberania/território ou grave risco às relações internacionais
> - [ ] **Competência (art. 27):** ultrassecreto (Presidente, Vice, Ministros, Comandantes, Chefes de missão); secreto (+ titulares de autarquias/fundações/estatais); reservado (+ DAS 101.5+); **delegação vedada a subdelegação**
> - [ ] **Art. 28:** classificação formalizada em decisão com assunto, fundamento, prazo e autoridade (TCI)
> - [ ] **Art. 30:** divulgação anual de rol de desclassificadas, classificadas e relatório de pedidos
> - [ ] **Art. 21:** **não** se nega informação necessária à tutela de direitos fundamentais; **nunca** se restringe informação sobre violações de direitos humanos
> - [ ] **Recursos:** interpor **10 dias** / decidir **5 dias** (1ª: autoridade superior — art. 15; 2ª: autoridade máxima — Dec. 7.724; 3ª: **CGU** — art. 16, 5 dias, exige prévia apreciação de autoridade superior; última: **CMRI**). Desclassificação: 30/10/30 dias
> - [ ] **Art. 31:** informação pessoal com acesso restrito **independentemente de classificação**, por até **100 anos**, a agentes autorizados e à própria pessoa; hipóteses sem consentimento no §3º; §4º veda uso do sigilo para proteger ilícitos
> - [ ] **Art. 32:** condutas ilícitas (recusar, retardar, fornecer incorreto **intencionalmente**, dolo/má-fé, divulgar indevidamente, impor sigilo para ocultar ilegalidade, destruir documentos); consequências: suspensão (mín. 8.112), transgressões militares, improbidade
> - [ ] **Art. 33:** sanções a pessoa física/entidade privada vinculada — advertência, multa, rescisão, suspensão de contratar (até 2 anos), inidoneidade
> - [ ] **Art. 34:** órgãos respondem diretamente por danos; direito de regresso; dolo ou culpa
> - [ ] **Decreto 7.724/2012:** regulamenta a LAI no **Poder Executivo federal** (SIC, 20+10 dias, classificação/TCI, desclassificação, CIDIC)
> - [ ] **Decreto 7.845/2012:** regulamenta **credenciamento de segurança e tratamento de informação classificada** (NSC, TCMS, CIDIC, cifração)

> [!warning] O erro mais comum em prova
> **Misturar os números e os regimes de proteção.** O candidato troca 5/15/25 entre os graus, confunde os 10 dias (para interpor o recurso) com os 5 dias (para a autoridade decidir), mistura os 20 dias da *resposta* com os prazos recursais, ou — o mais grave — confunde a **informação pessoal (100 anos, independe de classificação)** com a **informação classificada (5/15/25 anos)**. E, na mesma linha, troca os dois decretos (7.724 = acesso/classificação; 7.845 = credenciamento/tratamento). **Estratégia:** ao se deparar com a questão, pergunte-se primeiro "qual regime está em jogo (acesso, sigilo, dado pessoal ou sanção)?" e só então aplique o número correspondente. A pegadinha quase sempre está em forçar a aplicação do número certo no contexto errado.

---

## 11. Próximos passos

Você acabou de estudar a **LAI**, a primeira lei do Bloco 1.3. Ela te deu as bases de: publicidade/transparência, classificação e graus de sigilo, procedimento de acesso e recursos, proteção da informação pessoal, e responsabilidades. O próximo tópico da ementa é:

- **Lei Carolina Dieckmann (Lei nº 12.737/2012)** — que insere dispositivos no Código Penal sobre **acesso indevido a dispositivo informático**, com penas e agravantes. É a conexão da legislação com a segurança prática de sistemas.

Depois virão o **Marco Civil da Internet (Lei 12.965/2014)** — com privacidade, neutralidade de rede e responsabilidade dos provedores — e a **LGPD (Lei 13.709/2018)**, o tema mais cobrado deste bloco, que desenvolverá em profundidade o tratamento de dados pessoais que a LAI apenas esboça no art. 31.

> [!note] Uma ponte que você já pode construir
> Repare como a LAI já deixou "aberta a porta" para o que vem: o conceito de *informação pessoal* (art. 4º, IV e art. 31), o *tratamento da informação* e as *hipóteses de uso sem consentimento* são sementes que a **LGPD** vai expandir. Quando estudar a LGPD, volte a esta nota e veja como os regimes dialogam — a LAI é o ponto de partida do direito de acesso e da proteção de dados no Brasil.
