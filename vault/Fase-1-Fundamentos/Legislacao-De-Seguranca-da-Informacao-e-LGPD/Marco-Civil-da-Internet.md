# Marco Civil da Internet — Lei nº 12.965/2014

> [!info] Metadados
> **Disciplina:** Legislação de Segurança da Informação e LGPD
> **Bloco:** 1.3 — Legislação (FASE 1 — Fundamentos)
> **Tópico:** 3. Marco Civil da Internet (Lei 12.965/2014)
> **Subtópicos:** Princípios de uso da internet no Brasil · Privacidade e proteção de dados · Neutralidade da rede · Responsabilidade dos provedores · Retenção de dados
> **Pré-requisitos:** Nenhum
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-28

---

## 1. Por que estudar este tópico?

Você já estudou a [[Lei-de-Acesso-a-Informacao-LAI|LAI]] (que garante o direito de acessar informações públicas e protege dados pessoais em até 100 anos) e a [[Lei-Carolina-Dieckmann|Lei Carolina Dieckmann]] (que pune criminalmente a invasão de computadores). O Bloco 1.3 agora dá um passo mais amplo: em vez de cuidar apenas do acesso à informação (LAI) ou da punição à invasão (Carolina Dieckmann), ele passa a regular **o uso da internet em si** — os direitos de quem navega, os deveres de quem provede serviços online, e as regras que mantêm a rede aberta, segura e neutra.

A **Lei nº 12.965**, de 23 de abril de 2014 — conhecida como **Marco Civil da Internet** — é a "Constituição da Internet" brasileira. Ela estabelece os princípios, garantias, direitos e deveres para o uso da internet no Brasil. Foi acelerada no Congresso Nacional após o escândalo de espionagem da NSA (Agência de Segurança Nacional dos EUA), revelado por Edward Snowden em 2013, que expôs e-mails da então Presidenta Dilma Rousseff sendo monitorados. A repercussão internacional tornou urgente a aprovação de um marco regulatório que protegesse a privacidade e a liberdade dos brasileiros na rede.

Para o seu cargo de **Analista de TI na DATAPREV**, o Marco Civil é relevante porque:

- você trabalhará com sistemas que **coletam, armazenam e transmitem dados** de usuários pela internet — e precisa conhecer as regras de privacidade, retenção e responsabilidade que regem esse ciclo;
- o conceito de **neutralidade de rede** influencia decisões de arquitetura de software e infraestrutura de sistemas que dependem de conexão à internet;
- a **responsabilidade dos provedores** de aplicação e de conexão é um dos temas mais cobrados em provas da FGV, e diretamente aplicável ao trabalho com APIs, serviços web e plataformas digitais.

> [!question] Pergunta orientadora
> A LAI já protegia dados pessoais (art. 31) e a Lei Carolina Dieckmann já punia invasões (art. 154-A). Por que foi necessário criar uma *terceira* lei para cuidar da internet? Porque a LAI regula o *Estado* (acesso a informações públicas) e a Carolina Dieckmann regula o *penal* (o crime de invasão). Faltava uma lei que regulasse a *relação entre o cidadão e os provedores de internet* — quem provede conexão, quem provede aplicações (sites, apps, redes sociais), e o que eles podem ou não fazer com os dados dos usuários. O Marco Civil preenche exatamente essa lacuna.

> [!tip] Palavras-chave que a banca usa (guarde desde já)
> **Uso da internet no Brasil** · **princípios** (arts. 2º e 3º) · **neutralidade de rede** · **privacidade** · **proteção de dados pessoais** · **provedor de conexão** · **provedor de aplicações** · **registros de conexão** · **registros de acesso a aplicações** · **consentimento livre, expresso e informado** · **ordem judicial** · **sigilo das comunicações** · **vedação de suspensão de conexão por débito** · **isenção de responsabilidade do provedor de conexão** · **responsabilidade do provedor de aplicação** · **prazo de guarda de registros** (1 ano × 6 meses) · **multa de até 10% do faturamento** · **Decreto nº 8.771/2016** (regulamentação da neutralidade de rede).

Ao longo desta nota, vamos destrinchar cada ponto em *prosa explicativa*, com exemplos e pegadinhas — porque a FGV adora testar a diferença precisa entre provedor de conexão e provedor de aplicação, entre registros de conexão e registros de acesso, e entre as hipóteses em que a retenção é obrigatória e em que depende de ordem judicial.

---

## 2. Contexto, estrutura e alcance da lei

### 2.1 O que é o Marco Civil e por que ele existe

O Marco Civil da Internet (Lei 12.965/2014) é a **lei marco** que disciplina o uso da internet no Brasil. Diferente de muitas leis de tecnologia que nascem reativas a um problema específico (como a Lei Carolina Dieckmann, reação ao caso da atriz), o Marco Civil foi concebido de forma **preventiva e estrutural**: ele não regula uma atividade pontual, mas sim **o ecossistema inteiro da internet brasileira** — os princípios, os direitos, os deveres e as relações entre os agentes.

A lei foi sancionada em **23 de abril de 2014** e entrou em vigor em **23 de junho de 2014** (60 dias após a publicação). Seu regulamento é o **Decreto nº 8.771/2016**.

### 2.2 A estrutura da lei: o que o edital cobra

O edital do concurso DATAPREV 2026 cita expressamente: **Capítulo II (Seção I) e Capítulo III (Seções I e II)**. Isso significa que o cerne da prova será:

| Capítulo / Seção | Artigos | Tema principal |
|:---|:---:|:---|
| **Cap. I** (Fundamentos) | 2º e 3º | Fundamentos e princípios |
| **Cap. II, Seção I** (Direitos e Garantias) | 7º a 9º | Direitos dos usuários, privacidade e neutralidade de rede |
| **Cap. III, Seção I** (Guarda e Disponibilização de Registros) | 10 a 12 | Guarda de registros de conexão e acesso, sanções |
| **Cap. III, Seção II** (Guarda de Registros de Conexão) | 13 e 14 | Prazos e procedimentos de guarda de registros de conexão |

> [!note] Recorte do edital vs. ementa
> A ementa do Bloco 1.3 inclui o subtópico "Responsabilidade dos provedores", que na lei está na **Seção IV do Capítulo III** (arts. 18 a 21) — fora da citação expressa do edital. Trataremos essa seção de forma **concisa** ao final da nota, para que você esteja preparado caso a banca extrapole o recorte literal. Mas o **foco da prova** será nos arts. 7º a 14.

### 2.3 Dois conceitos-chave que percorrem toda a lei

Antes de entrar nos artigos, é fundamental distinguir dois tipos de provedor, porque **toda a lei gira em torno dessa distinção**:

- **Provedor de conexão**: empresa que fornece o **acesso à internet** (conectividade). É o provedor de internet (ISP): Vivo, Claro, Oi, TIM, GVT, entre outros. Quando você contrata um plano de internet residencial ou de celular, está contratando um provedor de conexão. Ele é responsável pelo **transporte dos dados** (roteamento, comutação, transmissão).

- **Provedor de aplicação**: empresa ou pessoa que oferece **serviços, conteúdos e ferramentas** acessíveis pela internet — como sites, redes sociais, e-mails, aplicativos, plataformas de streaming. Google, Facebook/Meta, WhatsApp, Instagram, Netflix, Mercado Livre, UOL são todos provedores de aplicação. Eles **não** fornecem a conexão em si, mas oferecem o que você acessa *por meio* da conexão.

> [!warning] PEGADINHA nº 1 — não confundir os dois provedores
> A banca faz uma distinção rigorosa: o **provedor de conexão** é obrigado a guardar registros de **conexão** por **1 ano** (art. 13); o **provedor de aplicação** é obrigado a guardar registros de **acesso a aplicações** por **6 meses** (art. 15, Seção III). Esses prazos são diferentes, os registros são diferentes, e os deveres de cada um também. Se a questão trocar um pelo outro, a resposta está errada.

---

## 3. Fundamentos e princípios (arts. 2º e 3º)

### 3.1 Os fundamentos do uso da internet (art. 2º)

O **art. 2º** é o preâmbulo filosófico da lei. Ele estabelece que a disciplina do uso da internet no Brasil tem como **fundamento primeiro** o respeito à **liberdade de expressão**, e a isso se somam seis pilares:

| Inciso | Fundamento |
|:---:|:---|
| I | Reconhecimento da **escala mundial** da rede |
| II | **Direitos humanos**, desenvolvimento da personalidade e exercício da **cidadania** em meios digitais |
| III | **Pluralidade** e diversidade |
| IV | **Abertura** e colaboração |
| V | **Livre iniciativa**, livre concorrência e defesa do **consumidor** |
| VI | **Finalidade social** da rede |

> [!question] Pergunta orientadora
> Por que a liberdade de expressão ocupa lugar de destaque, antes mesmo dos direitos humanos e da finalidade social? Porque a internet, antes de ser mercado ou ferramenta, é um **espaço de expressão e comunicação**. O legislador quis deixar claro que qualquer regulamentação posterior não pode suprimir a liberdade de expressão — ela é o alicerce, não o teto.

### 3.2 Os princípios (art. 3º)

O **art. 3º** avança dos fundamentos (filosofia) para os **princípios** (regras orientadoras para toda a interpretação da lei). São oito:

| Inciso | Princípio |
|:---:|:---|
| I | Garantia da **liberdade de expressão**, comunicação e manifestação de pensamento |
| II | **Proteção da privacidade** |
| III | **Proteção dos dados pessoais** |
| IV | Preservação e garantia da **neutralidade de rede** |
| V | Preservação da **estabilidade, segurança e funcionalidade** da rede |
| VI | **Responsabilização dos agentes** segundo suas atividades |
| VII | Preservação da natureza **participativa** da rede |
| VIII | **Liberdade dos modelos de negócio** (vedação a mudanças unilaterais ou de surpresa) |

> [!tip] Memorize os princípios como "duplas"
> A banca costuma testar a identificação de princípios. Uma dica: agrupar em pares.
> - **Liberdade e privacidade** (I e II) — protegem o cidadão
> - **Dados e neutralidade** (III e IV) — protegem os dados e o tráfego
> - **Segurança e responsabilidade** (V e VI) — protegem a infraestrutura e atribuem responsabilidade
> - **Participação e modelo de negócio** (VII e VIII) — protegem a dinâmica da rede
>
> Se a questão listar quatro princípios e um deles não estiver neste artigo, é o divergente.

> [!warning] PEGADINHA nº 2 — "neutralidade de rede" já aparece como princípio
> O art. 3º, IV, insere a **neutralidade de rede** como um dos oito princípios. Isso significa que ela não é apenas uma regra técnica — é um **princípio interpretativo** de toda a lei. Quando você estudar o art. 9º (que regulamenta a neutralidade em detalhe), lembre-se de que o fundamento está aqui, no art. 3º. A banca pode perguntar em que artigo a neutralidade aparece pela primeira vez como princípio — a resposta é o **art. 3º, IV**.

---

## 4. Direitos e garantias dos usuários (Capítulo II, arts. 7º a 9º)

### 4.1 Os direitos do usuário (art. 7º)

O **art. 7º** é um dos mais importantes do Marco Civil. Ele enumera os **direitos** de quem usa a internet no Brasil — e a banca adora testar a discriminação entre eles. Vejamos cada um:

**I — Inviolabilidade da intimidade e da vida privada.**
A intimidade e a vida privada do usuário são invioláveis. Se houver violação, o usuário tem direito a **indenização pelo dano material ou moral**. Essa é a consagração constitucional (art. 5º, X, da CF/88) no contexto da internet.

**II — Inviolabilidade e sigilo do fluxo das comunicações pela internet.**
O **fluxo** de comunicações (o que trafega pela rede em tempo real) é sigiloso. A única exceção é **ordem judicial**. Ninguém — nem provedor, nem governo — pode interceptar o fluxo de dados sem autorização do juiz.

**III — Inviolabilidade e sigilo das comunicações privadas armazenadas.**
Aqui a lei vai além do fluxo: mesmo as comunicações **já armazenadas** (e-mails salvos, mensagens no servidor, fotos na nuvem) são sigilosas. A exceção é a mesma: **ordem judicial**.

> [!warning] PEGADINHA nº 3 — fluxo vs. armazenamento
> O art. 7º, II, protege o **fluxo** (dados em trânsito); o art. 7º, III, protege o **conteúdo armazenado** (dados em repouso). São regimes diferentes, mas com a mesma exceção: **ordem judicial**. A banca pode perguntar se a proteção se aplica apenas ao fluxo ou também ao armazenado — a resposta é **ambos**.

**IV — Vedação de suspensão da conexão por débito.**
A conexão à internet **não pode ser suspensa** por inadimplência, **salvo** duas hipóteses: (a) débito **diretamente decorrente da utilização** da internet (ou seja, a própria fatura da internet); ou (b) **ordem judicial**.

> [!warning] PEGADINHA nº 4 — a suspensão por débito tem exceção limitada
> Muitos candidatos erram ao marcar que "a conexão nunca pode ser suspensa". Isso é falso: ela **pode** ser suspensa se o débito for **da própria internet** (a fatura do plano). Se eu deixo de pagar a luz, o provedor não pode cortar minha internet. Mas se eu deixo de pagar *a internet*, ele pode cortar. E, claro, uma ordem judicial sempre pode autorizar a suspensão. A banca testa se você sabe a exceção.

**V — Manutenção da qualidade contratada.**
O provedor deve manter a qualidade de serviço que foi contratada. Essa previsão protege contra "throttling" (redução intencional de velocidade) não prevista contratualmente — e se conecta diretamente com o princípio da neutralidade de rede.

**VI — Informações claras e completas nos contratos.**
Os contratos de internet devem conter informações claras sobre: planos contratados, velocidade de upload e download, preços, termos de uso e cláusulas de **sigilo de comunicações**.

**VII — Não fornecimento a terceiros de dados pessoais.**
O provedor **não pode fornecer dados pessoais do usuário a terceiros** sem o **consentimento livre, expresso e informado** do titular, ou salvo quando houver **obrigação legal** (por exemplo, ordem judicial ou obrigação de retenção de dados).

> [!tip] A "fórmula" da proteção de dados no Marco Civil
> Três palavras-chave: **consentimento livre**, **expresso** e **informado**. O consentimento precisa ser dado sem coação (livre), de forma explícita (expresso), e com pleno conhecimento do que está sendo consentido (informado). A mesma fórmula aparecerá na LGPD — memorize essa combinação agora.

**VIII — Informações sobre sistemas de coleta de dados.**
O usuário tem direito a informações claras sobre: (a) os **sistemas de coleta** de dados adotados; (b) as **práticas de segurança** da informação; e (c) as **informações de terceiros** que eventualmente terão acesso aos seus dados. Essa é a versão "proto-transparência" do Marco Civil — a LGPD a expandirá enormemente.

### 4.2 A privacidade como condição para o acesso livre (art. 8º)

O **art. 8º** estabelece um princípio que parece simples, mas é profundamente significativo:

> [!important] Art. 8º — privacidade e liberdade como condição de acesso
> "A **garantia do direito à privacidade e à liberdade de expressão** nas comunicações é condição para o pleno exercício do direito de acesso à internet."

O que isso significa? Que **privacidade e liberdade não são "extras"** da internet — elas são **pré-condições**. Sem privacidade, o cidadão não navega com segurança; sem liberdade de expressão, a internet perde sua natureza participativa. O art. 8º coloca esses direitos como **base de sustentação** do acesso.

Os parágrafos detalham essa proteção:

- **§1º:** a violação ao segredo de comunicação é **crime** (Lei 9.296/1996 — Lei das Escutas) e aplica-se o Código Penal e legislação complementar. A proteção penal reforça a proteção civil do Marco Civil.

- **§2º:** é **vedado** ao provedor de conexão entregar dados pessoais a terceiros. Isso é um reforço do art. 7º, VII, aplicado especificamente ao provedor de conexão.

- **§3º:** quando o usuário acessa conteúdo de outro usuário por **erro ou acidente** (fortuito), o provedor deve **eliminar publicamente** esse acesso, se necessário. Exemplo: se por uma falha de configuração um usuário consegue acessar o painel administrativo de outro usuário, o provedor deve corrigir e tornar público que o acesso indevido foi eliminado.

### 4.3 A neutralidade de rede (art. 9º)

O **art. 9º** é, provavelmente, o artigo **mais cobrado** do Marco Civil em provas da FGV. Ele regulamenta o princípio da neutralidade de rede previsto no art. 3º, IV.

> [!important] Art. 9º — neutralidade de rede
> O **responsável pela transmissão, comutação ou roteamento** (ou seja, o provedor de conexão) tem o **dever de tratar de forma isonômica quaisquer pacotes de dados**, **sem distinção** por conteúdo, origem e destino, serviço, terminal ou aplicação.

Em palavras simples: a internet deve tratar **todos os dados por igual**. Um pacote de dados do Netflix não pode ser tratado de forma diferente de um pacote de dados do e-mail do usuário — não importa o conteúdo, a origem, o destino, o serviço, o dispositivo ou a aplicação. A isonomia é absoluta.

> [!question] Pergunta orientadora
> Imagine que uma empresa de telefonia é também provedora de internet e tem seu próprio aplicativo de mensagens. A neutralidade de rede impede que ela dê **prioridade ao tráfego do seu próprio aplicativo** e reduza a velocidade do WhatsApp de concorrentes? **Sim** — exatamente isso que o art. 9º proíbe. A distinção por "serviço" ou "aplicação" é vedada.

**§1º — Regulamentação pela Anatel e pelo CGI.br.**
A discriminação ou degradação de tráfego será regulamentada pelo Presidente da República mediante decreto, **ouvidos a Anatel e o Comitê Gestor da Internet (CGI.br)**. O regulamento atual é o Decreto 8.771/2016.

> [!warning] PEGADINHA nº 5 — quem regula a neutralidade?
> O edital e a banca podem testar se você sabe que a regulamentação da neutralidade envolve a **Anatel** e o **CGI.br**, e não outros órgãos como a ANPD (que regula a LGPD) ou o Conselho Nacional de Cibernética. Essa distinção de competências é cobrada literalmente.

**§2º — Exceções à neutralidade (não configuram violação).**
A lei prevê três hipóteses em que a discriminação de tráfego **não** configura violação da neutralidade:

| Exceção | Descrição |
|:---|:---|
| **I — Requisitos técnicos indispensáveis** | Priorização necessária para a prestação adequada de serviços e aplicações (por exemplo, videoconferência precisa de menor latência; telemedicina tem requisitos de prioridade) |
| **II — Priorização de serviços de emergência** | Tráfego relacionado a situações de emergência (190, SAMU, Defesa Civil) pode ser priorizado |
| **III — Proteção da segurança da rede e dos dados** | Medidas técnicas necessárias para proteger a integridade da rede e a segurança dos dados (por exemplo, bloqueio de tráfego malicioso, mitigação de ataques DDoS) |

> [!tip] As exceções são **restritivas**
> Note que as exceções não são portas abertas — são situações específicas e justificadas. A banca pode criar uma "quarta exceção" que não existe na lei (por exemplo, "priorização de tráfego por contrato comercial") — se não estiver nestas três, **não é exceção**.

**§3º — Vedação de bloqueio, monitoramento, filtragem e análise.**
Na provisão de conexão à internet, é **vedado** ao provedor:

- **bloquear** conteúdo;
- **monitorar** tráfego;
- **filtrar** pacotes de dados;
- **analisar** o conteúdo dos pacotes de dados;

...respeitadas as exceções do §2º. Essa vedação é a materialização prática da neutralidade: o provedor de conexão deve ser um **"tubo neutro"** — ele transporta os dados, mas não olha para o que há dentro deles, não decide quem recebe prioridade, e não bloqueia com base no conteúdo.

> [!note] Contexto atual: neutralidade e a pandemia
> Durante a pandemia de COVID-19, o governo brasileiro regulamentou temporariamente a possibilidade de priorização de tráfego para serviços essenciais (educação remota, telemedicina) por meio do Decreto 10.332/2020, com prazo determinado. A medida foi encerrada e a neutralidade foi restabelecida integralmente. Esse episódio mostra que a neutralidade de rede não é absoluta — mas que qualquer exceção deve ser **temporária, justificada e regulamentada**. Não espere que a banca cobre esse decreto em detalhes, mas saiba que o tema é vivo e pode aparecer em questões de atualidades.

---

## 5. Guarda e disponibilização de registros (Capítulo III, Seções I e II)

### 5.1 Disposição geral: privacidade na guarda de registros (art. 10)

O **art. 10** estabelece o princípio que orienta toda a Seção I: a guarda e a disponibilização dos registros devem atender à preservação da **intimidade, vida privada, honra e imagem** das partes.

Três regras centrais:

- **§1º:** a guarda dos registros só pode ocorrer com **consentimento livre, expresso e informado** do titular, ou por **obrigação legal**. Ou seja: não é livre — ou o usuário autoriza, ou a lei obriga.

- **§2º:** o fornecimento de comunicações secretas e registros só pode ocorrer mediante **ordem judicial**, nas hipóteses e na forma que a lei estabelecer.

- **§3º:** essas regras se aplicam tanto ao **provedor de conexão** quanto ao **provedor de aplicações** — o acesso aos dados de ambos depende de ordem judicial.

> [!question] Pergunta orientadora
> Por que o art. 10 usa "intimidade, vida privada, honra e imagem" — as mesmas expressões do art. 5º, X, da Constituição Federal? Porque o legislador quis ancorar a proteção de dados na internet nos **direitos fundamentais** da CF. Não é uma proteção "nova" — é a **tradução** dos direitos constitucionais para o contexto digital.

### 5.2 Jurisdição brasileira sobre dados coletados no país (art. 11)

O **art. 11** é curto, mas de enorme impacto:

> [!important] Art. 11 — dados coletados no Brasil sujeitam-se à legislação brasileira
> "A **jurisdição brasileira** aplica-se ao tratamento de dados coletados **no Brasil**, e o operador deve observar a legislação brasileira **independentemente de onde estejam localizados** os centros de armazenamento dos dados."

Isso significa: se um aplicativo coleta dados de usuários brasileiros — mesmo que os servidores estejam na Irlanda, nos EUA ou em qualquer outro país — o tratamento desses dados **obedece à legislação brasileira**. O Marco Civil afirmou, em 2014, o que depois seria reforçado pela LGPD em 2018: o critério é o **local da coleta**, não o local do armazenamento.

> [!warning] PEGADINHA nº 6 — "local de armazenamento" não define jurisdição
> Questão que disser que "os dados armazenados no exterior não se sujeitam à legislação brasileira" está **ERRADA**. O art. 11 é claro: o critério é a **coleta no Brasil**. Se o dado foi coletado aqui, a legislação brasileira se aplica, não importa onde ele esteja armazenado. Esse artigo é a base para exigir que empresas estrangeiras cumpram a lei brasileira quando operam no mercado brasileiro.

### 5.3 Sanções pela violação dos arts. 10 e 11 (art. 12)

O **art. 12** prevê as sanções aplicáveis quando um provedor viola as regras de guarda e disponibilização de registros. São quatro sanções, aplicáveis **cumulativa ou alternativamente**:

| Sanção | Detalhe |
|:---|:---|
| **I — Advertência** | Com indicação de prazo para adoção de medidas corretivas |
| **II — Multa** | Até **10% (dez por cento) do faturamento do grupo econômico no Brasil** no último exercício, excluídos os tributos; consideram-se a condição econômica do infrator e a proporcionalidade entre a gravidade da falta e a intensidade da sanção |
| **III — Suspensão temporária** | Das atividades que envolvam os tratamentos de dados afetados |
| **IV — Proibição de exercício** | Das atividades que envolvam os tratamentos de dados afetados |

> [!tip] A multa de 10% é o número que a FGV adora
> A multa pode chegar a **10% do faturamento do grupo econômico no Brasil** — e o grupo econômico, não apenas a empresa específica. É uma sanção pesada, desenhada para ter efeito dissuasório sobre grandes corporações. Note que o cálculo exclui tributos (impostos) — o faturamento considerado é o "limpo". A banca pode trocar "faturamento da empresa" por "faturamento do grupo econômico" — a resposta correta é **grupo econômico**.

**Parágrafo único:** a empresa **estrangeira** responde **solidariamente** com a sua filial ou sucursal no Brasil. Ou seja: se a matriz no exterior ordena o tratamento irregular e a filial brasileira executa, ambas respondem juntas.

---

## 6. Guarda de registros de conexão (Capítulo III, Seção II, arts. 13 e 14)

### 6.1 O dever de guarda (art. 13)

O **art. 13** é o ponto central da retenção de dados para o provedor de conexão. Ele estabelece:

> [!important] Art. 13 — guarda de registros de conexão
> O provedor de conexão deve **guardar os registros de conexão, sob sigilo, em ambiente controlado e de segurança, pelo prazo de 1 (um) ano**, nos termos do regulamento.

Três elementos essenciais:
1. **O quê:** registros de conexão (dados que identificam quem se conectou, quando, por quanto tempo, de onde — como IP, data/hora, duração da sessão).
2. **Como:** sob sigilo, em ambiente controlado e de segurança.
3. **Quanto tempo:** **1 ano** — prazo fixo e inegociável.

**§1º:** a obrigação de guarda se aplica mesmo quando o uso da internet for **gratuito**. Ou seja: um provedor de Wi-Fi gratuito em um café ou em uma praça pública também deve guardar os registros de conexão dos usuários pelo prazo de 1 ano.

> [!warning] PEGADINHA nº 7 — Wi-Fi gratuito também obriga guarda
> Muitos candidatos erram ao pensar que o Wi-Fi gratuito está isento. **Não está.** O §1º do art. 13 é claro: a responsabilidade de guarda se estende ao uso gratuito. A banca adora criar cenários com "café que oferece Wi-Fi" para testar se o candidato leu o §1º.

**§2º:** a autoridade policial, administrativa ou o Ministério Público podem requerer, **cautelarmente**, que os registros sejam guardados por prazo **superior a 1 ano**. Essa requisição deve ser feita antes do término do prazo de 1 ano — ou seja, se o provedor já deletou os registros, não dá para pedir mais.

**§4º:** o acesso aos registros de conexão só pode ser feito mediante **consentimento do titular** ou **ordem judicial**, e, nas hipóteses e prazos legais, da autoridade competente.

### 6.2 O fornecimento de registros (art. 14)

O **art. 14** detalha como os registros são fornecidos:

- Mediante **requisição** da autoridade policial, administrativa ou do Ministério Público, o provedor de conexão deve fornecer os registros em prazo definido.
- O juiz também pode requisitar diretamente.

**§2º:** a polícia e o MP poderão requerer ao juiz que os registros sejam **guardados por prazo superior a 1 ano** — reforçando que o prazo estendido depende de autorização judicial.

**§3º:** o prazo e a forma do fornecimento são definidos em regulamento.

### 6.3 Registros de acesso a aplicações (art. 15 — Seção III, fora do escopo explícito do edital)

> [!note] Fora do escopo expresso do edital, mas relevante para a ementa
> A Seção III do Capítulo III (arts. 15 a 17) trata da guarda de **registros de acesso a aplicações** — responsabilidade do **provedor de aplicação**. O prazo de guarda é de **6 (seis) meses** (art. 15). Esse prazo é **metade** do prazo de guarda de registros de conexão (1 ano). A distinção entre os dois regimes é um ponto clássico de cobrança. Atenção à incidência: essa obrigação de guarda recai sobre o provedor de aplicação constituído como **pessoa jurídica** e que exerça a atividade de forma **organizada, profissional e com fins econômicos** — não sobre qualquer pessoa física que ofereça um serviço.

### 6.4 Quadro comparativo: registros de conexão × registros de acesso a aplicações

| Elemento | Registros de **conexão** (arts. 13-14) | Registros de **acesso a aplicações** (art. 15) |
|:---|:---|:---|
| **Responsável pela guarda** | Provedor de **conexão** (ISP) | Provedor de **aplicação** (sites, apps, redes sociais) |
| **O que são** | Dados de identificação do acesso: IP, data/hora, duração, etc. | Dados sobre o que o usuário acessou nos serviços: login, IP de origem, data/hora, etc. |
| **Prazo de guarda** | **1 ano** | **6 meses** |
| **Exigência** | Sigilo, ambiente controlado e seguro | Idem |
| **Acesso** | Consentimento do titular **ou ordem judicial** (ou autoridade competente, nas hipóteses legais) | Idem |

> [!warning] PEGADINHA nº 8 — 1 ano vs. 6 meses
> Esta é uma das pegadinhas mais recorrentes da FGV: trocar os prazos. **Conexão = 1 ano. Aplicações = 6 meses.** Se a questão perguntar "qual o prazo mínimo de guarda de registros de conexão?" a resposta é 1 ano. Se perguntar "de registros de acesso a aplicações?", a resposta é 6 meses. Memorize o par — ele sempre aparece.

---

## 7. Responsabilidade dos provedores (arts. 18 a 21 — Seção IV, fora do escopo explícito do edital)

> [!note] Nota sobre o recorte do edital
> Esta seção trata da **responsabilidade dos provedores por danos decorrentes de conteúdo gerado por terceiros**, prevista nos arts. 18 a 21 (Seção IV do Capítulo III). O edital do DATAPREV 2026 cita expressamente apenas o Capítulo II (Seção I) e o Capítulo III (Seções I e II). No entanto, a **ementa** do Bloco 1.3 inclui o subtópico "Responsabilidade dos provedores", motivo pelo qual tratamos o tema aqui — de forma concisa e com a ressalva de que pode estar fora do foco da prova. Esteja preparado, mas não dedique excesso de tempo a estes artigos.

### 7.1 Provedor de conexão: isenção de responsabilidade (art. 18)

O **art. 18** é claro e direto:

> [!important] Art. 18
> "O provedor de conexão à internet **não será responsabilizado civilmente** por danos decorrentes de conteúdo gerado por terceiros."

O provedor de conexão é um "transportador" — ele move pacotes de dados, mas não tem controle sobre o conteúdo desses pacotes. Por isso, a lei o isenta de responsabilidade pelo conteúdo que trafega por sua rede. Isso é uma consequência lógica da neutralidade de rede: se o provedor não pode olhar o conteúdo dos pacotes, ele também não pode ser responsabilizado por esse conteúdo.

### 7.2 Provedor de aplicação: responsabilização condicionada à ordem judicial (art. 19)

O **art. 19** é mais sutil e é o mais cobrado da Seção IV:

> [!important] Art. 19
> "O provedor de aplicação de internet somente poderá ser responsabilizado civilmente por danos decorrentes de conteúdo gerado por terceiros se, após **ordem judicial específica**, não tomar as providências para, no prazo indicado, **tornar indisponível** o conteúdo apontado como violador."

A lógica é a seguinte:
1. O usuário publica conteúdo em um site ou aplicativo.
2. Se esse conteúdo causar dano a alguém, a vítima pode pedir ao juiz uma **ordem judicial** para que o provedor de aplicação remova o conteúdo.
3. Se o provedor **não cumprir** a ordem judicial no prazo indicado, ele será responsabilizado.
4. Se o provedor **cumprir**, ele fica **isento** de responsabilidade.

Essa regra é conhecida como o **regime de "notice and takedown" judicial** — diferente do modelo americano (DMCA), em que o provedor pode ser responsabilizado pela mera notificação extrajudicial. No Brasil, é necessária a **ordem do juiz**.

> [!question] Pergunta orientadora
> Por que o legislador exigiu ordem judicial em vez de aceitar notificação extrajudicial? Porque exigir notificação judicial protege a **liberdade de expressão**: o provedor não remove conteúdo apenas porque alguém pediu — ele espera a ordem de um juiz, que avaliou se o conteúdo é de fato violador. Sem essa exigência, provedores seriam pressionados a remover qualquer conteúdo sob alegação de violação, gerando censura prévia.

### 7.3 Vedação de condicionamento do acesso a dados pessoais (art. 20)

O **art. 20** protege o usuário na outra ponta: é **vedado** ao provedor de aplicações (i) exigir disponibilização de dados pessoais como **condição para o acesso** a conteúdo ou serviços; e (ii) condicionar a **prestação de serviço** ao **consentimento para coleta de dados** ou para tratamento que não seja necessário. Em síntese: o acesso a um serviço não pode ser "cobrado" em dados pessoais além do estritamente necessário.

> [!tip] Art. 20 — dados como "moeda de troca"
> Essa vedação é a antecipação conceitual de debates que explodirão com a LGPD (consentimento e finalidade). Guarde a ideia central: **o usuário não pode ser obrigado a entregar dados como condição para usar um serviço**. A banca pode testar se tal condicionamento é permitido — **não é**, salvo quando o tratamento for necessário para a própria prestação do serviço.

### 7.4 Conteúdo íntimo sem autorização (art. 21)

O **art. 21** trata do caso específico de conteúdo que versem sobre **atividades íntimas** publicadas sem autorização do participante:

> [!important] Art. 21
> "O provedor de aplicação que disponibilize conteúdo que versem sobre atividades íntimas ou de conteúdo de natureza sexual será responsabilizado civilmente pela **divulgação não autorizada** de informação ou dado se, **mesmo após notificação**, não tomar providências para tornar indisponível o conteúdo."

Esse artigo é especialmente relevante no contexto do chamado "revenge porn" — a divulgação não autorizada de imagens ou vídeos íntimos. Note que ele se aplica ao **provedor de aplicação** (que hospeda o conteúdo), e não ao provedor de conexão.

---

## 8. Pegadinhas e estratégias de prova

A FGV é precisa com artigos, prazos e palavras. Vamos consolidar as principais pegadinhas do Marco Civil:

> [!warning] PEGADINHA nº 9 — "vedação de suspensão" tem exceção que a banca esconde
> Art. 7º, IV: a conexão **não pode ser suspensa** por débito — **salvo** débito da própria internet ou ordem judicial. Questão que disser que "a suspensão da conexão é sempre vedada" está errada.

> [!warning] PEGADINHA nº 10 — neutralidade ≠ vedação absoluta
> Art. 9º, §2º: há exceções à neutralidade (requisitos técnicos, emergência, segurança). Questão que disser que "a neutralidade de rede é absoluta e não admite exceções" está errada.

> [!warning] PEGADINHA nº 11 — provedor de conexão vs. aplicação: responsabilidade
> Art. 18 (conexão) = **isenção** de responsabilidade. Art. 19 (aplicação) = responsabilização **condicionada à ordem judicial**. Trocar os dois é uma das pegadinhas clássicas.

> [!warning] PEGADINHA nº 12 — prazos de guarda: 1 ano × 6 meses
> Registros de **conexão** = **1 ano** (art. 13). Registros de **acesso a aplicações** = **6 meses** (art. 15). A troca é recorrente.

> [!warning] PEGADINHA nº 13 — multa de 10% é do "grupo econômico", não da "empresa"
> Art. 12, II: multa de até 10% do **faturamento do grupo econômico no Brasil** — não apenas da empresa infratora. A expressão "grupo econômico" amplia a base de cálculo.

> [!warning] PEGADINHA nº 14 — dados coletados no Brasil, armazenados no exterior
> Art. 11: a jurisdição brasileira aplica-se aos dados coletados **no Brasil**, independentemente de onde estejam armazenados. O critério é o local da **coleta**, não do armazenamento.

---

## 9. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **Contexto:** Lei 12.965/2014, sancionada em 23/04/2014, vigência em 23/06/2014; "Constituição da Internet" brasileira; regulamentada pelo Decreto 8.771/2016
> - [ ] **Dois provedores-chave:** provedor de **conexão** (ISP — conectividade) vs. provedor de **aplicação** (sites, apps, serviços)
> - [ ] **Art. 2º (fundamentos):** liberdade de expressão em destaque + escala mundial, direitos humanos, pluralidade, abertura, livre iniciativa, finalidade social
> - [ ] **Art. 3º (princípios):** oito princípios — liberdade de expressão, privacidade, proteção de dados pessoais, neutralidade de rede, estabilidade/segurança/funcionalidade, responsabilização, natureza participativa, liberdade de modelos de negócio
> - [ ] **Art. 7º (direitos):** inviolabilidade da intimidade/vida privada (I); sigilo do fluxo (II); sigilo do conteúdo armazenado (III); vedação de suspensão por débito (salvo débito próprio ou ordem judicial) (IV); manutenção da qualidade contratada (V); informações claras nos contratos (VI); vedação de fornecimento de dados pessoais a terceiros sem consentimento livre/expresso/informado ou obrigação legal (VII); informações sobre sistemas de coleta e segurança (VIII)
> - [ ] **Art. 8º:** privacidade e liberdade como **condição** para o pleno exercício do acesso; §1º: violação de segredo = crime (Lei 9.296/96); §2º: vedado ao provedor de conexão fornecer dados pessoais a terceiros; §3º: acesso por erro/fortuito deve ser eliminado publicamente
> - [ ] **Art. 9º (neutralidade):** dever de tratar isonomicamente quaisquer pacotes, sem distinção por conteúdo, origem, destino, serviço, terminal ou aplicação; §1º: regulamentação pelo Presidente, ouvidos **Anatel e CGI.br**; §2º: exceções (requisitos técnicos, emergência, segurança); §3º: vedação de bloqueio, monitoramento, filtragem e análise de pacotes
> - [ ] **Art. 10:** guarda de registros sob privacidade; §1º: guarda mediante consentimento ou obrigação legal; §2º: fornecimento mediante **ordem judicial**; §3º: aplica-se a ambos os provedores
> - [ ] **Art. 11:** dados coletados no Brasil sujeitam-se à legislação brasileira, independentemente do local de armazenamento
> - [ ] **Art. 12 (sanções):** advertência; multa de até **10% do faturamento do grupo econômico no Brasil** (excluídos tributos); suspensão temporária; proibição de exercício; § único: empresa estrangeira responde solidariamente com filial/sucursal
> - [ ] **Art. 13 (registros de conexão):** guarda por **1 ano**, sob sigilo, ambiente controlado e seguro; §1º: aplica-se ao uso gratuito; §2º: autoridade pode requerer guarda superior a 1 ano; §4º: acesso mediante consentimento ou ordem judicial
> - [ ] **Art. 14:** fornecimento de registros de conexão mediante requisição da autoridade policial, MP ou juiz
> - [ ] **Decreto 10.332/2020:** exceção **temporária** à neutralidade durante a pandemia (educação remota, telemedicina) — encerrada, com neutralidade restabelecida
> - [ ] **Art. 15 (registros de aplicações):** guarda por **6 meses** — metade do prazo de conexão; aplica-se ao provedor pessoa jurídica que atue de forma organizada, profissional e com fins econômicos
> - [ ] **Art. 18:** provedor de conexão **não** é responsabilizado por conteúdo de terceiros
> - [ ] **Art. 19:** provedor de aplicação só é responsabilizado se **não cumprir ordem judicial** de remoção
> - [ ] **Art. 20:** vedado exigir dados pessoais como condição de acesso; vedado condicionar serviço ao consentimento para coleta de dados
> - [ ] **Art. 21:** conteúdo íntimo divulgado sem autorização — responsabilidade do provedor de aplicação

> [!warning] O erro mais comum em prova
> **Trocar os prazos e os regimes entre provedores.** O candidato confunde: 1 ano (conexão) com 6 meses (aplicações); atribui responsabilidade ao provedor de conexão pelo conteúdo (art. 18 diz o oposto); exige notificação extrajudicial para remoção (art. 19 exige ordem judicial); e troca "grupo econômico" por "empresa" na base de cálculo da multa. **Estratégia:** Ao ver uma questão sobre o Marco Civil, pergunte-se primeiro: *o que está sendo regulado — o provedor de conexão ou o de aplicação?* Essa distinção resolve 80% das questões. Em segundo lugar, memorize os dois prazos de guarda (1 ano × 6 meses) e o único caminho para responsabilizar o provedor de aplicação (ordem judicial). A FGV nunca erra a letra da lei — o erro está em fazer o candidato errar a leitura.

---

## 10. Próximos passos

Você estudou o **Marco Civil da Internet**, que regulamenta o uso da internet no Brasil — princípios, direitos, neutralidade, guarda de registros e responsabilidade dos provedores. Ele complementa a [[Lei-de-Acesso-a-Informacao-LAI|LAI]] (que regula o acesso a informações públicas) e a [[Lei-Carolina-Dieckmann|Lei Carolina Dieckmann]] (que pune invasões de sistemas) ao oferecer o **marco de regulação da internet** como um todo.

O próximo tópico da ementa é:

- **Lei Geral de Proteção de Dados — LGPD (Lei nº 13.709/2018)** — que será o tema mais cobrado deste bloco. Ela desenvolverá em profundidade o tratamento de dados pessoais que a LAI apenas esboça no art. 31, que o Marco Civil protege nos arts. 7º, 10 e 11, e que a Lei Carolina Dieckmann protege criminalmente no art. 154-A. A LGPD trará: princípios do tratamento de dados, bases legais, direitos dos titulares, papéis do Controlador e do Operador, a ANPD e sanções administrativas.

> [!note] Uma ponte que você já pode construir
> Repare como o ecossistema se encaixa: a **LAI** protege a informação pessoal no contexto do Estado; a **Lei Carolina Dieckmann** pune a invasão para obter dados; o **Marco Civil** regula a internet e a guarda de registros; e a **LGPD** regulamentará o tratamento de dados pessoais em *todos* os contextos — público e privado. Cada lei acrescenta uma camada de proteção. Quando estudar a LGPD, volte a esta nota e veja como os arts. 7º, 10 e 11 do Marco Civil dialogam com os princípios e bases legais da LGPD — eles são a espinha dorsal do regime de proteção de dados brasileiro.
