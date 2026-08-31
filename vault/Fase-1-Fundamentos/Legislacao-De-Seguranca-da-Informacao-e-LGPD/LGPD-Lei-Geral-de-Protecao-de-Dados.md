# Lei Geral de Proteção de Dados — LGPD (Lei nº 13.709/2018)

> [!info] Metadados
> **Disciplina:** Legislação de Segurança da Informação e LGPD
> **Bloco:** 1.3 — Legislação (FASE 1 — Fundamentos)
> **Tópico:** 4. Lei Geral de Proteção de Dados — LGPD (Lei 13.709/2018)
> **Subtópicos:** Princípios (art. 6º) · Bases legais (art. 7º) · Direitos dos titulares · Papel do Controlador e do Operador · RIPD · ANPD · Sanções administrativas
> **Pré-requisitos:** Nenhum (mas se beneficia do conhecimento das leis anteriores deste bloco)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-28

---

## 1. Por que estudar este tópico?

Você já estudou três leis que, juntas, formam um sistema de proteção da informação:

- A [[Lei-de-Acesso-a-Informacao-LAI|LAI]] garantiu o direito de acessar informações públicas e protegeu **dados pessoais** por até 100 anos (art. 31), mas focou no **Estado como titular** da informação — como o cidadão acessa o que o governo guarda.
- A [[Lei-Carolina-Dieckmann|Lei Carolina Dieckmann]] **puniu criminalmente** quem invade computadores para obter dados (art. 154-A), mas cobriu apenas o **aspecto penal** — a invasão em si.
- O [[Marco-Civil-da-Internet|Marco Civil da Internet]] regulou a **internet como infraestrutura** — princípios, neutralidade, responsabilidade dos provedores — e incluiu proteções de dados pessoais nos arts. 7º e 10, mas seu foco não era o tratamento de dados em si, e sim a **regulação do ecossistema da internet**.

O que faltava era uma lei que dissesse: *"quando alguém — público ou privado — coleta, armazena, usa ou compartilha dados pessoais, quais são as regras?"* Essa lei é a **LGPD** — e ela é, de longe, o **tema mais cobrado neste bloco** em provas da FGV.

A **Lei nº 13.709**, de 14 de agosto de 2018 — **Lei Geral de Proteção de Dados Pessoais (LGPD)** — estabelece um regime jurídico completo para o tratamento de dados pessoais no Brasil. Ela não se limita à internet (como o Marco Civil) nem ao Estado (como a LAI): seu alcance é **universal** — pública, privada, digital, analógica.

Para o seu cargo de **Analista de TI na DATAPREV**, a LGPD é essencial porque:

- você trabalhará com sistemas que **coletam, processam, armazenam e transmitem dados pessoais** — e precisa saber quando e como isso é legal, quais são os direitos dos titulares, e quais são as consequências de errar;
- a **segurança da informação** (arts. 46-51) será parte central do seu cotidiano profissional — e a LGPD é a base legal dessa exigência;
- a FGV cobra a LGPD de forma **detalhada e literal**: princípios, bases legais, prazos, sanções e definições são alvos frequentes.

> [!question] Pergunta orientadora
> Se a LAI já protegia dados pessoais e o Marco Civil já exigia consentimento para fornecimento de dados a terceiros, por que foi necessária uma lei "nova" e tão abrangente? Porque a LAI regulava o **Estado** (e não a iniciativa privada), e o Marco Civil regulava a **internet** (e não o tratamento offline). A LGPD unifica: ela se aplica a **qualquer pessoa** (física ou jurídica, pública ou privada) que realize **tratamento de dados pessoais**, independentemente do meio (digital ou físico) e do contexto.

> [!tip] Palavras-chave que a banca usa (guarde desde já)
> **Dados pessoais** · **dados sensíveis** · **dados anonimizados** · **titular** · **controlador** · **operador** · **encarregado (DPO)** · **agentes de tratamento** · **tratamento** · **consentimento** · **bases legais** · **legítimo interesse** · **princípios** (finalidade, adequação, necessidade, etc.) · **RIPD** · **ANPD** · **sanções** (advertência, multa de até 2% ou R$ 50 milhões) · **incidente de segurança** · **decisões automatizadas** · **portabilidade** · **anonimização vs. pseudonimização** · **Lei 15.352/2026** (Agência Nacional de Proteção de Dados).

Ao longo desta nota, vamos destrinchar cada um desses pontos em *prosa explicativa*, com exemplos e pegadinhas — porque a LGPD tem uma densidade conceitual alta e a FGV cobra a **letra exata** dos artigos.

---

## 2. Contexto, estrutura e alcance da lei

### 2.1 O que é a LGPD e por que ela existe

A LGPD é a resposta brasileira à preocupação global com a privacidade e a proteção de dados pessoais. Ela foi influenciada pelo **Regulamento Geral de Proteção de Dados (GDPR)** da União Europeia, mas adapta o modelo à realidade brasileira — com uma **autoridade nacional independente** (a ANPD), **sanções pecuniárias** com limites definidos e um **catálogo de bases legais** ampliado.

A lei foi sancionada em **14 de agosto de 2018**, mas sua **vigência plena** (isto é, o início da aplicação de suas regras e sanções) só ocorreu em **18 de setembro de 2020** — ou seja, dois anos de *vacatio legis* para que empresas, órgãos públicos e a sociedade se adaptassem. As **sanções administrativas** (arts. 52-54), por sua vez, tiveram sua entrada em vigor prorrogada até **1º de agosto de 2021**, em razão da pandemia de COVID-19 (Lei 14.010/2020).

> [!important] Datas que a banca pode cobrar
> - **Sanção:** 14 de agosto de 2018
> - **Vigência plena:** 18 de setembro de 2020
> - **Sanções (arts. 52-54):** 1º de agosto de 2021
> - A LGPD também **alterou o Marco Civil da Internet** (Lei 12.965/2014) em suas disposições finais — ponto que você já viu na nota anterior.

### 2.2 A estrutura da lei: o que o edital cobra

O edital do DATAPREV 2026 cita expressamente: **Capítulos I, II, III, IV, VII, VIII e IX**. Veja o mapeamento:

| Capítulo | Artigos | Tema principal |
|:---|:---:|:---|
| **Cap. I** — Disposições Preliminares | 1º a 4º | Fundamentos, âmbito de aplicação, definições |
| **Cap. II** — Do Tratamento de Dados Pessoais | 5º a 16 | Definições (art. 5º), **princípios** (art. 6º), **bases legais** (art. 7º), consentimento (art. 8º), legítimo interesse (art. 10), dados sensíveis (art. 11), crianças (art. 14), término do tratamento (arts. 15-16) |
| **Cap. III** — Dos Direitos do Titular | 17 a 22 | **Direitos do titular** (art. 18), confirmação/acesso (art. 19), revisão de decisões automatizadas (art. 20) |
| **Cap. IV** — Do Poder Público | 23 a 32 | Tratamento pelo poder público, uso compartilhado |
| **Cap. VII** — Da Segurança e Boas Práticas | 46 a 51 | Segurança da informação, **notificação de incidente** (art. 48), boas práticas e governança |
| **Cap. VIII** — Da Fiscalização e das Sanções Administrativas | 52 a 54 | **Sanções administrativas** (art. 52) |
| **Cap. IX** — Da Autoridade Nacional e do Conselho Nacional | 55 a 59 | **ANPD** |

> [!note] Recorte do edital vs. ementa
> Os detalhes sobre **Controlador, Operador, Encarregado (DPO) e RIPD** — substancialmente o Cap. VI (arts. 37-45) — **não estão na citação literal do edital**. No entanto, a ementa do Bloco 1.3 exige esses subtópicos ("Papel do Controlador e do Operador" e "Relatório de Impacto à Proteção de Dados"). Seguiremos a mesma estratégia adotada na nota do [[Marco-Civil-da-Internet|Marco Civil]]: os **conceitos essenciais** serão ancorados no **art. 5º** (definições — Cap. I, que É citado no edital), e os detalhes das obrigações do Cap. VI serão tratados de forma **concisa e com ressalva explícita** de que estão fora do escopo literal do edital.

### 2.3 Dois conceitos centrais: âmbito de aplicação e exceções

O **art. 3º** define o **âmbito de aplicação** da LGPD — ou seja, *a quem* e *em que situações* ela se aplica:

> [!important] Art. 3º — âmbito de aplicação
> A LGPD se aplica a **qualquer operação de tratamento** de dados pessoais realizada:
>
> I — no **território nacional**;
> II — com o objetivo de **ofertar ou fornecer** bens ou serviços, ou de tratar dados de indivíduos localizados no **território nacional**;
> III — quando os dados tiverem sido **coletados no território nacional**.

Isso é amplo: empresas estrangeiras que tratam dados de brasileiros também estão sujeitas à lei — mesmo que seus servidores estejam no exterior. Note a semelhança com o art. 11 do [[Marco-Civil-da-Internet|Marco Civil]]: o critério é a **coleta ou a oferta a indivíduos no Brasil**, não o local de armazenamento.

**Exceções** (art. 4º): a LGPD **não se aplica** ao tratamento de dados quando realizado:
- por **pessoa natural exclusivamente para fins particulares e não econômicos** (art. 4º, I) — exemplo: caderno de contatos doméstico, uma agenda pessoal, sem finalidade comercial;
- para fins **exclusivamente jornalísticos e artísticos** (art. 4º, II, "a");
- para fins **exclusivamente acadêmicos** (art. 4º, II, "b"), aplicando-se a esta hipótese os arts. 7º e 11 (bases legais e dados sensíveis);
- para fins **exclusivamente de segurança pública, defesa nacional, segurança do Estado ou atividades de investigação e repressão de infrações penais** (art. 4º, III) — regido por legislação específica;
- quando se tratar de dados **provenientes de fora do território nacional**, que não sejam objeto de comunicação ou uso compartilhado com agentes de tratamento brasileiros nem de transferência internacional (art. 4º, IV).

> [!question] Pergunta orientadora
> Um blogueiro que publica críticas a restaurantes e, para isso, coleta dados pessoais de donos de estabelecimentos — ele está sujeito à LGPD? Depende: se o blogueiro atua como **pessoa física com fins não econômicos** (blog hobby), a exceção do art. 4º, I, pode se aplicar. Se ele monetiza o blog (publicidade, patrocínio), ele passa a ter **finalidade econômica** e a LGPD se aplica. A distinção é a **finalidade**, não o tamanho.

---

## 3. Definições fundamentais (art. 5º)

O art. 5º da LGPD é um dos mais longos e mais cobrados de toda a lei — ele define **toda a terminologia** que o texto usa. Não é necessário memorizar todas as 49 definições, mas é **imperativo** dominar as principais, porque a banca adora trocar definições entre si ou alterar uma palavra-chave para tornar a alternativa falsa.

### 3.1 Dado pessoal, dado sensível, dado anonimizado e pseudonimizado

A distinção entre esses conceitos é um dos pontos mais cobrados em qualquer prova sobre a LGPD:

| Conceito | Definição (art. 5º) | Exemplo |
|:---|:---|:---|
| **Dado pessoal** (art. 5º, I) | Informação relacionada a pessoa natural **identificada ou identificável** | Nome, CPF, e-mail, endereço, RG |
| **Dado pessoal sensível** (art. 5º, II) | Dados sobre origem racial/étnica, convicção religiosa, opinião política, filiação sindical/religiosa/filosófica/política, dado referente à **saúde ou vida sexual**, dado **genético ou biométrico** quando vinculado a pessoa natural | Doença diagnosticada, voto político, religião, impressão digital, fotos biométricas |
| **Dado anonimizado** (art. 5º, III) | Dado que **não pode ser identificado**, considerando meios técnicos **razoáveis e disponíveis** na ocasião do tratamento | Dados estatísticos agregados que não permitem rastrear o indivíduo |
| **Dado pseudonimizado** (art. 5º, §2º, combinado com art. 13, §4º) | Dado que perdeu a associação direta ou indireta, **exceto** pelo uso de **informação adicional mantida separadamente** pelo controlador em ambiente controlado e seguro | Base de dados com IDs substitutos, cuja chave de correlação fica em outro sistema acessível apenas pelo controlador |

> [!warning] PEGADINHA nº 1 — dado anonimizado NÃO é dado pessoal
> Esta é uma das pegadinhas mais recorrentes da FGV. Se um dado é **verdadeiramente anonimizado** — ou seja, não permite a identificação do titular por meios técnicos razoáveis — ele **não é mais dado pessoal** e, portanto, **não se sujeita à LGPD**. A banca testa isso com alternativas como "dado anonimizado continua sendo dado pessoal sob a LGPD" — isso é **falso**. O critério é técnico: se meios razoáveis existem para reverter a anonimização, o dado não está verdadeiramente anonimizado.

> [!warning] PEGADINHA nº 2 — pseudonimização ≠ anonimização
> **Pseudonimização** é diferente de **anonimização**: no pseudonimizado, existe uma **chave de correlação** mantida separadamente que permite, em tese, identificar o titular. Portanto, dado pseudonimizado **continua sendo dado pessoal** sob a LGPD. A banca pode trocar os termos — se disser que "dado pseudonimizado não é dado pessoal", está errado. A definição de pseudonimização consta do art. 13, §4º.

### 3.2 Os agentes de tratamento: titular, controlador, operador e encarregado

A LGPD cria um ecossistema de papéis que você precisa distinguir com clareza:

| Papel | Definição (art. 5º) | Analogia simples |
|:---|:---|:---|
| **Titular** (art. 5º, V) | Pessoa natural a quem se referem os dados pessoais | O cidadão cujo nome, CPF e saúde estão registrados |
| **Controlador** (art. 5º, VI) | Pessoa (natural ou jurídica, **pública ou privada**) a quem competem as **decisões** referentes ao tratamento | A empresa ou órgão que **decide coletar, usar e compartilhar** os dados |
| **Operador** (art. 5º, VII) | Pessoa que realiza o tratamento de dados **em nome do controlador** | A empresa de nuvem ou RH que processa os dados por ordem do controlador |
| **Encarregado — DPO** (art. 5º, VIII) | Pessoa indicada pelo controlador e operador, que atua como **canal de comunicação** entre controlador, titulares e ANPD | O "ombudsman de dados" da organização |
| **Agentes de tratamento** (art. 5º, IX) | O **controlador** e o **operador** conjuntamente | Os dois atores principais do tratamento |

> [!question] Pergunta orientadora
> A DATAPREV contratou uma empresa de TI para hospedar o sistema do CNIS. Quem é o controlador e quem é o operador? O **controlador** é a DATAPREV — porque ela **decide** quais dados são coletados (nome, CPF, contribuições), para qual finalidade (administração da Previdência Social) e com quem serão compartilhados. A **empresa de TI** é o operador — porque ela **executa** o tratamento (hospeda, processa, armazena) em nome da DATAPREV, sem decidir a finalidade.

### 3.3 Consentimento e tratamento

| Conceito | Definição (art. 5º) |
|:---|:---|
| **Consentimento** (art. 5º, XII) | Manifestação livre, informada e inequívoca pela qual o titular concorda com o tratamento para uma **finalidade determinada** |
| **Tratamento** (art. 5º, X) | Toda operação com dados pessoais: coleta, produção, recepção, classificação, utilização, acesso, reprodução, transmissão, distribuição, processamento, arquivamento, armazenamento, eliminação, avaliação/controle da informação, modificação, comunicação, transferência, difusão ou extração |

### 3.4 RIPD, bloqueio e eliminação

| Conceito | Definição (art. 5º) |
|:---|:---|
| **RIPD** (art. 5º, XVII) | Documentação do controlador que contém a **descrição dos processos de tratamento** que podem gerar riscos às liberdades civis e direitos fundamentais, bem como **medidas, salvaguardas e mecanismos** de mitigação |
| **Bloqueio** (art. 5º, XIII) | Suspensão temporária de qualquer operação de tratamento, mediante guarda do dado ou banco de dados |
| **Eliminação** (art. 5º, XIV) | Exclusão de dado ou conjunto armazenado |

> [!tip] Definição de "tratamento" é extensa — mas compreensível
> A lista parece assustadora, mas não é preciso memorizar cada operação. O ponto que a banca cobra é que **"tratamento" é um conceito amplo**: tudo que se faz com dados pessoais — desde a coleta até a eliminação — é tratamento. Se uma questão perguntar se "armazenar dados em servidor configura tratamento", a resposta é sim.

---

## 4. Fundamentos (art. 2º) e Princípios (art. 6º)

### 4.1 Os sete fundamentos da LGPD (art. 2º)

O art. 2º é o preâmbulo filosófico da lei — assim como o art. 2º do [[Marco-Civil-da-Internet|Marco Civil]] listou os fundamentos do uso da internet. A LGPD enumera **sete fundamentos**:

| Inciso | Fundamento |
|:---:|:---|
| I | Respeito à **privacidade** |
| II | **Autodeterminação informativa** |
| III | **Liberdade de expressão**, informação, comunicação e opinião |
| IV | Inviolabilidade da **intimidade, honra e imagem** |
| V | Desenvolvimento **econômico e tecnológico** e inovação |
| VI | **Livre iniciativa**, livre concorrência e defesa do **consumidor** |
| VII | **Direitos humanos**, livre desenvolvimento da personalidade, **dignidade** e cidadania |

> [!question] Pergunta orientadora
> Note que "privacidade" aparece como fundamento (inciso I), mas a LGPD protege **muito mais que privacidade** — ela protege o **tratamento** de dados em si. A privacidade é o *ponto de partida*, não o *ponto de chegada*. E a "autodeterminação informativa" (inciso II) é um conceito que diz: o cidadão tem o direito de **decidir** quem acessa seus dados e para quê. É o fundamento filosófico do consentimento.

### 4.2 Os princípios do tratamento de dados (art. 6º)

O art. 6º é o **coração interpretativo** da LGPD — todo o restante da lei deve ser lido à luz destes princípios. São **dez princípios** acrescidos da **boa-fé** (que permeia todos):

| Inciso | Princípio | Significado prático |
|:---:|:---|:---|
| I | **Finalidade** | Tratamento para propósitos legítimos, específicos, explícitos e informados; vedado tratamento posterior incompatível |
| II | **Adequação** | Compatibilidade do tratamento com as finalidades informadas ao titular |
| III | **Necessidade** | Limitação ao mínimo necessário — dados pertinentes, proporcionais e não excessivos (princípio da **minimização**) |
| IV | **Livre acesso** | Consulta facilitada e gratuita sobre a forma e duração do tratamento, e sobre a integralidade dos dados pessoais |
| V | **Qualidade dos dados** | Garantia de exatidão, clareza, relevância e atualização dos dados |
| VI | **Transparência** | Garantia de informações claras, precisas e facilmente acessíveis sobre o tratamento e os agentes |
| VII | **Segurança** | Medidas técnicas e administrativas aptas a proteger os dados contra acessos não autorizados, destruição, perda, alteração, comunicação ou qualquer forma de tratamento inadequado ou ilícito |
| VIII | **Prevenção** | Adoção de medidas para **prevenir** a ocorrência de danos em virtude do tratamento |
| IX | **Não discriminação** | Impossibilidade de realização do tratamento para fins discriminatórios ilícitos ou abusivos |
| X | **Responsabilização e prestação de contas** (*accountability*) | Demonstração, pelo agente, da adoção de medidas eficazes que comprovem o cumprimento das normas de proteção de dados |

> [!tip] Dica de memorização: "FAN-trans-PQUAL-SEG-PREV-NAO-RESP"
> Para decorar, pense em uma sequência lógica: o tratamento precisa ter **Finalidade**, ser **Adequado** e **Necessário**. O titular precisa ter **Livre acesso** e dados de **Qualidade**. Tudo deve ser feito com **Transparência** e **Segurança**, de forma **Preventiva**, sem **Não discriminação**, e com **Responsabilização**. O acrônimo não é perfeito, mas a lógica ajuda: finalidade → adequação → necessidade → acesso → qualidade → transparência → segurança → prevenção → não discriminação → responsabilização.

> [!warning] PEGADINHA nº 3 — "necessidade" vs. "conveniência"
> O princípio da **necessidade** (art. 6º, III) é o mais cobrado em situações práticas. Ele diz: colete **apenas o mínimo necessário** para a finalidade. Se um formulário de cadastro em um site pede CPF, endereço, telefone e profissão, mas a finalidade é apenas enviar uma newsletter, coletar CPF e profissão viola o princípio da necessidade — esses dados **não são pertinentes nem proporcionais** para essa finalidade. A banca adora criar cenários como esse para testar se você entende o princípio da minimização.

> [!warning] PEGADINHA nº 4 — "responsabilização" (accountability) é o mais novo
> O princípio da **responsabilização e prestação de contas** (art. 6º, X) é inspirado no GDPR europeu e é frequentemente esquecido por candidatos. Ele impõe ao controlador o dever de **demonstrar** que está cumprindo a lei — não basta cumprir, é preciso **provar**. É o princípio que alimenta o RIPD e as auditorias. A banca pode incluir um princípio "inventado" na lista e deixar de fora o da responsabilização — marque como divergente.

---

## 5. Bases legais do tratamento (art. 7º) e consentimento (art. 8º)

### 5.1 As dez bases legais: quando o tratamento é permitido

O art. 7º é um dos dispositivos mais importantes da LGPD: ele lista as **hipóteses em que o tratamento de dados pessoais é lícito**. A regra geral é: **sem base legal, não há tratamento**. São dez:

| Inciso | Base legal | Descrição |
|:---:|:---|:---|
| I | **Consentimento** | O titular autorizou o tratamento para finalidade específica |
| II | **Obrigação legal ou regulatória** | A lei obriga o controlador a realizar o tratamento |
| III | **Políticas públicas** (administração pública) | Execução de políticas públicas pela administração pública (art. 23) |
| IV | **Estudos por órgão de pesquisa** | Garantia de anonimização dos dados |
| V | **Execução de contrato** ou de procedimentos preliminares | Tratamento necessário para cumprir contrato ou negociações prévias |
| VI | **Exercício regular de direitos** | Em processo judicial, administrativo ou arbitral |
| VII | **Proteção da vida** ou incolumidade física | Situações de emergência em que a vida está em risco |
| VIII | **Tutela da saúde** | Exclusivamente, em procedimento realizado por profissionais ou serviços de saúde |
| IX | **Legítimo interesse** do controlador ou de terceiro | Exceto quando prevalecerem os direitos e liberdades fundamentais do titular |
| X | **Proteção do crédito** | Tutela do crédito do controlador |

> [!question] Pergunta orientadora
> Por que existem tantas bases legais? Porque nem sempre é possível (ou justo) exigir o consentimento do titular. Imagine um hospital em que um paciente chega inconsciente — o médico precisa acessar dados de saúde para salvar a vida. Haveria tempo para pedir consentimento? Não. A base legal aqui é a **proteção da vida** (inciso VII). Outro exemplo: a Receita Federal precisa cruzar dados fiscais para apurar impostos — a base é a **obrigação legal** (inciso II). O consentimento é importante, mas não é a única via legítima.

### 5.2 O consentimento em detalhe (art. 8º)

O consentimento é a base legal mais intuitiva, mas também a mais regulamentada. O art. 8º traz regras rígidas:

- Deve ser fornecido por **escrito ou outro meio** que demonstre a manifestação de vontade do titular;
- Se for escrito, a cláusula de consentimento deve ser apresentada de forma **destacada** das demais cláusulas contratuais;
- O **ônus da prova** do consentimento é do **controlador** — ou seja, é o controlador quem precisa provar que o titular consentiu;
- São **nulas** as autorizações genéricas — o consentimento deve indicar **finalidades determinadas**;
- O consentimento pode ser **revogado a qualquer tempo** por manifestação expressa do titular, por procedimento **gratuito e facilitado** (art. 8º, §5º).

> [!warning] PEGADINHA nº 5 — consentimento genérico é NULO
> Uma das pegadinhas mais clássicas da FGV: a empresa pede "aceito todos os termos" de forma genérica, sem especificar a finalidade. Isso é **nulo**. O art. 8º, §4º, é explícito: "são nulas as autorizações para o tratamento de dados pessoais para finalidades que não estejam previstas" no consentimento. O titular precisa saber **exatamente para quê** está dando o "sim". Se a questão disser que "consentimento genérico é válido desde que o titular seja maior de idade", está errada.

> [!warning] PEGADINHA nº 6 — o ônus da prova é do controlador
> Se surgir um conflito — "o titular diz que não consentiu; o controlador diz que sim" — quem precisa provar? O **controlador**. Se ele não conseguir demonstrar que obteve o consentimento devidamente, presume-se que **não houve consentimento**. A banca pode trocar a direção: dizer que "o titular deve provar que não consentiu" — isso está errado.

### 5.3 O legítimo interesse (art. 10)

O **legítimo interesse** (art. 7º, IX) é a base legal mais debatida e sutil da LGPD. O art. 10 regulamenta:

- Só pode fundamentar tratamento para **finalidades legítimas**;
- Quando baseado no legítimo interesse, o controlador deve utilizar apenas os dados **estritamente necessários** para a finalidade;
- A ANPD pode solicitar **RIPD** (Relatório de Impacto à Proteção de Dados) quando o tratamento for baseado no legítimo interesse.

> [!tip] Legítimo interesse ≠ "eu acho que é importante"
> O legítimo interesse não é um "cheque em branco". Ele exige um **balanceamento**: o interesse do controlador deve ser compatível com os **direitos fundamentais do titular**. Exemplo: uma loja online quer usar o histórico de compras para enviar propaganda — isso pode ser legítimo interesse. Mas se ela quer vender esse histórico a terceiros sem o consentimento, o legítimo interesse provavelmente não se sustenta, pois o titular tem expectativa razoável de privacidade. A ANPD pode exigir o RIPD para verificar se o balanceamento foi feito.

### 5.4 Dados sensíveis: regras específicas (art. 11)

Os dados sensíveis (art. 5º, II) merecem tratamento diferenciado. O art. 11 diz que o tratamento só pode ocorrer com **consentimento específico e destacado**, ou nas hipóteses seguintes (sem consentimento):

1. cumprimento de obrigação legal ou regulatória pelo controlador;
2. execução de políticas públicas pela administração pública;
3. realização de estudos por órgão de pesquisa (garantida a anonimização);
4. exercício regular de direitos em processo;
5. proteção da vida ou da incolumidade física;
6. tutela da saúde, exclusivamente em procedimento realizado por profissionais ou serviços de saúde;
7. garantia da prevenção à fraude e à segurança do titular, nos processos de identificação e autenticação em sistemas eletrônicos.

> [!important] Vedação crucial: compartilhamento de dados sensíveis de saúde
> O art. 11, §3º, **veda** a comunicação ou o uso compartilhado, entre controladores, de dados pessoais sensíveis referentes à **saúde** com objetivo de obter **vantagem econômica** — exceto em duas hipóteses: (1) a portabilidade dos dados quando houver consentimento do titular; (2) a prestação de serviços de saúde, de assistência farmacêutica e de assistência à saúde. Essa vedação é extremamente relevante para o setor de saúde — e para a DATAPREV, que opera o SUS.

> [!warning] PEGADINHA nº 7 — dados sensíveis: consentimento "específico e destacado"
> Para dados sensíveis, o consentimento **não pode ser genérico** — ele precisa ser **específico e destacado** (art. 11). Ou seja: basta menos que o consentimento do art. 8º? Não — basta **mais**. É preciso que o titular manifeste consentimento **separado** para dados sensíveis, com atenção especial à finalidade. Se uma questão disser que "o consentimento para dados sensíveis é o mesmo do art. 8º", está errada.

---

## 6. Direitos dos titulares (art. 18) e revisão de decisões automatizadas (art. 20)

### 6.1 Os nove direitos do titular

O art. 18 é outro dispositivo essencial da LGPD: ele lista os **direitos** de quem é titular de dados pessoais. São **nove**:

| Inciso | Direito | Significado |
|:---:|:---|:---|
| I | **Confirmação** da existência de tratamento | O titular pode perguntar: "vocês estão tratando meus dados?" |
| II | **Acesso** aos dados | O titular pode ver quais dados são tratados e como |
| III | **Correção** de dados incompletos, inexatos ou desatualizados | Direito de pedir a correção |
| IV | **Anonimização, bloqueio ou eliminação** de dados desnecessários, excessivos ou em desconformidade com a lei | Direito de "limpar" os dados |
| V | **Portabilidade** dos dados | Transferir dados de um controlador para outro (mediante requisição expressa) |
| VI | **Eliminação** dos dados tratados com consentimento | O titular pode pedir para deletar tudo — salvo exceções (art. 16) |
| VII | **Informação** sobre entidades com quem houve **uso compartilhado** | "Com quem vocês compartilharam meus dados?" |
| VIII | **Informação** sobre a possibilidade de **não fornecer consentimento** e sobre as consequências da negativa | Transparência total sobre o que acontece se o titular disser "não" |
| IX | **Revogação** do consentimento | A qualquer tempo, mediante manifestação expressa |

> [!warning] PEGADINHA nº 8 — portabilidade não é absoluta
> A portabilidade (inciso V) **não** é irrestrita: ela observa **segredos comercial e industrial**, e é regulamentada pela ANPD. Ou seja: o titular pode pedir a portabilidade, mas o controlador pode se recusar a entregar dados que são segredo comercial ou industrial. A banca pode criar uma alternativa dizendo que "a portabilidade é absoluta e não admite restrição" — isso está errado.

### 6.2 O prazo de resposta: 15 dias (art. 19)

O art. 19 estabelece os prazos para o controlador atender aos pedidos de confirmação e acesso:

- **Formato simplificado:** imediatamente (resposta imediata e clara);
- **Declaração clara e completa:** até **15 dias**, contados da data do requerimento do titular.

> [!warning] PEGADINHA nº 9 — o prazo de 15 dias é um alvo clássico
> A banca adora testar o prazo. Se a questão perguntar "em quanto tempo o controlador deve fornecer declaração clara e completa sobre o tratamento?" a resposta é **até 15 dias**. Não confunda com prazos de outros dispositivos da LGPD ou de outras leis. O formato simplificado (resposta imediata) não tem prazo numérico — é "imediatamente".

### 6.3 Revisão de decisões automatizadas (art. 20)

O art. 20 garante ao titular o direito de solicitar a **revisão de decisões** tomadas **unicamente com base em tratamento automatizado** de dados pessoais — incluindo decisões de perfilamento — que afetem seus interesses, como decisões referentes a:

- perfil do titular (profissional, de consumo, crédito);
- decisão de crédito.

Essa revisão deve ser feita por **pessoa natural** — ou seja, um ser humano precisa estar envolvido no processo. A banca pode testar se "decisões automatizadas são irrevisáveis" — a resposta é **não**: o art. 20 garante a revisão humana.

> [!tip] "Pessoa natural" = humano
> Essa expressão aparece em vários contextos da LGPD. Quando a lei diz "por pessoa natural", ela significa "por um ser humano". Não é uma empresa nem um algoritmo. Se uma empresa usa um software que automaticamente nega crédito a um titular, o titular tem direito a que um **humano** revise essa decisão.

---

## 7. Controlador, Operador e Encarregado (DPO); RIPD

### 7.1 Conceitos ancorados no art. 5º (Cap. I — citado no edital)

Você já viu as definições na seção 3.2. Aqui, vamos complementar com aspectos práticos:

- **Controlador** é quem **decide** (finalidade, forma, meio). Não necessariamente coleta os dados diretamente — pode terceirizar para o operador. Mas quem decide *por que* e *para quê* os dados são tratados é o controlador.
- **Operador** é quem **executa** o tratamento em nome do controlador. Ele segue instruções — não decide a finalidade.
- **Encarregado (DPO)** é a **ponte** entre o controlador, os titulares e a ANPD. Ele pode ser pessoa física ou jurídica, e sua identidade e informações de contato devem ser divulgadas publicamente.

> [!question] Pergunta orientadora
> Por que a distinção entre controlador e operador importa na prática? Porque a **responsabilidade** se distribui de forma diferente. O controlador é o principal responsável perante o titular e a ANPD. O operador responde solidariamente quando agir **fora das instruções** do controlador ou quando descumprir obrigação legal. Se a banca perguntar "quem responde diretamente perante o titular?" a resposta é o **controlador**.

### 7.2 RIPD (Relatório de Impacto à Proteção de Dados)

O RIPD está definido no art. 5º, XVII, e detalhado no art. 38 (Cap. VI — fora da citação literal do edital, mas relevante para a ementa):

- É um **documento do controlador** que descreve os processos de tratamento que possam gerar riscos às liberdades civis e direitos fundamentais;
- Deve conter as **medidas, salvaguardas e mecanismos** de mitigação de risco;
- A ANPD pode determinar sua elaboração em situações específicas;
- É obrigatório quando o tratamento for baseado no **legítimo interesse** (art. 10, §3º) ou quando envolver **dados sensíveis**.

> [!note] Recorte do edital
> Detalhes sobre obrigações do controlador e operador (art. 37-42), obrigatoriedade de RIPD em situações específicas (art. 38) e papel formal do DPO (art. 41) estão no **Cap. VI da LGPD** — não citado expressamente no edital. Contudo, a ementa inclui os subtópicos "Papel do Controlador e do Operador" e "RIPD", por isso tratamos aqui de forma **concisa**. Na prova, o foco deve ser nas **definições do art. 5º**, que estão no Cap. I (citado).

---

## 8. Segurança da informação e boas práticas; notificação de incidente (arts. 46-51)

### 8.1 O dever de segurança (art. 46)

O art. 46 impõe ao controlador e ao operador o dever de adotar **medidas de segurança, técnicas e administrativas** aptas a proteger os dados pessoais de acessos não autorizados e de situações acidentais ou ilícitas de destruição, perda, alteração, comunicação ou qualquer forma de tratamento inadequado ou ilícito.

> [!note] A Tríade CID (Confidencialidade, Integridade, Disponibilidade)
> O art. 46 não usa explicitamente o termo "Tríade CID", mas as medidas que ele exige correspondem aos três pilares da segurança da informação: **confidencialidade** (proteção contra acesso não autorizado), **integridade** (proteção contra alteração indevida) e **disponibilidade** (garantia de acesso legítimo). Essa Tríade será estudada em profundidade na **Fase de Segurança da Informação** — não antecipe esse conteúdo agora, mas saiba que a LGPD é uma das fontes legais que fundamentam a exigência de segurança da informação em organizações.

### 8.2 Notificação de incidente de segurança (art. 48)

O art. 48 é um dos mais importantes para o profissional de TI:

> [!important] Art. 48 — notificação de incidente
> O controlador deve comunicar à **autoridade nacional** e ao **titular** a ocorrência de **incidente de segurança** que possa acarretar **risco ou dano relevante** aos titulares.
>
> A comunicação deve ser feita em **prazo razoável** (conforme regulamento da ANPD) e deve conter, no mínimo:
> 1. a **descrição da natureza** dos dados pessoais afetados;
> 2. as informações sobre os **titulares** envolvidos;
> 3. a indicação das **medidas técnicas e de segurança** utilizadas para a proteção dos dados (medidas de contenção);
> 4. os **riscos** relacionados ao incidente;
> 5. os **motivos da demora**, no caso de comunicação fora do prazo;
> 6. as **medidas que foram ou serão adotadas** para reverter ou mitigar os efeitos do prejuízo.

> [!question] Pergunta orientadora
> Se um hacker invadir o sistema da DATAPREV e roubar dados pessoais de segurados, o que a DATAPREV precisa fazer? Ela precisa (1) comunicar à **ANPD** e (2) comunicar aos **titulares** afetados, em prazo razoável, com todas as informações do art. 48. Não basta apenas conter o ataque — é preciso **notificar**. Se a DATAPREV "esconder" o incidente, ela responde administrativamente (com sanções) e civilmente (com indenização).

> [!warning] PEGADINHA nº 10 — "risco ou dano relevante" é o gatilho
> A obrigação de notificar não é automática para qualquer incidente — ela se aplica quando o incidente possa acarretar **risco ou dano relevante** aos titulares. Uma tentativa de ataque bloqueada pelo firewall, sem qualquer vazamento, provavelmente não exige notificação. Mas um ataque que resultou em acesso a dados pessoais — mesmo que o controlador não saiba exatamente o que foi acessado — exige notificação. A banca pode testar a expressão "risco ou dano relevante" como condição.

---

## 9. ANPD e Sanções administrativas (arts. 52-54)

### 9.1 A ANPD: de "Autoridade" a "Agência"

A ANPD foi originalmente criada pela LGPD (Lei 13.709/2018) como a **Autoridade Nacional de Proteção de Dados** — um órgão da administração pública federal vinculado ao Ministério da Justiça e Segurança Pública.

> [!warning] ATUALIZAÇÃO IMPORTANTE — Lei 15.352/2026
> Em **25 de fevereiro de 2026**, foi sancionada a **Lei nº 15.352/2026** (conversão da Medida Provisória 1.317/2025), que **transformou a "Autoridade Nacional de Proteção de Dados" em "Agência Nacional de Proteção de Dados (ANPD)"**. A sigla **ANPD** foi mantida. A Agência agora é uma **autarquia de natureza especial** vinculada ao Ministério da Justiça e Segurança Pública, com **autonomia funcional, técnica, decisória, administrativa e financeira**. As definições dos artigos 5º, VIII (encarregado) e 5º, XIX (autoridade nacional) foram atualizadas para mencionar "Agência Nacional de Proteção de Dados (ANPD)".
>
> **Na prova:** a banca pode usar tanto "Autoridade" quanto "Agência". O mais importante é reconhecer a **sigla ANPD** e saber que ela é o órgão fiscalizador da LGPD. Se a questão mencionar "Agência Nacional de Proteção de Dados", saiba que se trata do mesmo órgão que antes se chamava "Autoridade Nacional de Proteção de Dados".

### 9.2 As sanções administrativas (art. 52)

O art. 52 é o "dente" da LGPD — ele dá poder de punição à ANPD. As sanções são aplicáveis após **processo administrativo** que garanta **ampla defesa e contraditório** e são graduadas, isoladas ou cumulativas, de acordo com as peculiaridades do caso concreto:

| Inciso | Sanção | Detalhe |
|:---:|:---|:---|
| I | **Advertência** | Com indicação de prazo para adoção de medidas corretivas |
| II | **Multa simples** | De até **2% do faturamento** da pessoa jurídica de direito privado, grupo ou conglomerado no Brasil no último exercício, excluídos os tributos, **limitada a R$ 50.000.000,00 por infração** |
| III | **Multa diária** | Observado o limite total previsto no inciso II |
| IV | **Publicização da infração** | Após devidamente apurada e confirmada a ocorrência da infração |
| V | **Bloqueio** dos dados pessoais a que se refere a infração | Até a regularização |
| VI | **Eliminação** dos dados pessoais a que se refere a infração | Até a regularização |
| X | **Suspensão parcial** do funcionamento do banco de dados | Prazo máximo de **6 meses**, prorrogável por igual período |
| XI | **Suspensão do exercício** da atividade de tratamento dos dados | Prazo máximo de **6 meses**, prorrogável por igual período |
| XII | **Proibição parcial ou total** do exercício de atividades relacionadas a tratamento de dados | Caráter mais grave |

> [!note] Por que a tabela pula de VI para X?
> O art. 52 tem, originalmente, incisos **VII, VIII e IX**, mas todos foram **VETADOS** quando da Lei 13.853/2019 — por isso o texto consolidado da lei salta de VI para X. Se você abrir a LGPD e notar a lacuna, não é erro de impressão: aqueles incisos simplesmente não existem no texto em vigor. A banca cobra com frequência os incisos **I a VI** e **X a XII** listados acima.

> [!important] A multa: 2% × R$ 50 milhões
> O cálculo da multa tem dois limites: o **percentual** (até 2% do faturamento) e o **teto absoluto** (R$ 50 milhões por infração). Ou seja: mesmo que 2% do faturamento supere R$ 50 milhões, a multa será limitada a R$ 50 milhões por infração. E o faturamento considerado é o do **grupo ou conglomerado no Brasil**, não apenas da empresa infratora. Excluem-se os tributos (impostos).

> [!warning] PEGADINHA nº 11 — "faturamento do grupo" e o teto de R$ 50 milhões
> A banca adora misturar os elementos da multa: trocar "2%" por "10%" (confundindo com a multa do Marco Civil — art. 12), trocar "grupo ou conglomerado" por "empresa isoladamente", ou esquecer o teto de R$ 50 milhões. Lembre-se: LGPD = **2%** (máx. **R$ 50 milhões**). Marco Civil = **10%** (sem teto fixo). São multas diferentes.

### 9.3 Critérios de aplicação das sanções (art. 52, §1º)

A ANPD não aplica sanções aleatoriamente — ela deve considerar:

- gravidade e natureza das infrações e dos direitos pessoais afetados;
- **boa-fé** do infrator;
- vantagem auferida ou pretendida pelo infrator;
- condição econômica do infrator;
- reincidência;
- grau do dano;
- cooperação do infrator;
- adoção reiterada e demonstrada de mecanismos e procedimentos internos capazes de minimizar o dano;
- adoção de política de boas práticas e governança;
- adoção de procedimento de resposta a incidentes;
- custo da medida administrativa.

### 9.4 Sanções administrativas ≠ civis ≠ penais (art. 52, §2º)

> [!important] Art. 52, §2º — independência das esferas
> As sanções administrativas da LGPD **não substituem** as sanções civis e penais definidas em legislação respectiva. Ou seja: uma empresa pode receber multa da ANPD (sanção administrativa), ser condenada a indenizar o titular (sanção civil) e seu dirigente pode ser processado criminalmente (sanção penal — incluindo pela [[Lei-Carolina-Dieckmann|Lei Carolina Dieckmann]] em caso de invasão de sistemas).

---

## 10. Pegadinhas e estratégias de prova

Consolidamos aqui as principais pegadinhas da LGPD — pontos onde a FGV perde candidatos despreparados:

> [!warning] PEGADINHA nº 12 — "Autoridade" × "Agência": nomenclatura atualizada
> A banca pode mencionar tanto "Autoridade Nacional de Proteção de Dados" quanto "Agência Nacional de Proteção de Dados" — ambas referem-se ao mesmo órgão (ANPD). Se a questão usar "Agência", não fique confuso: é a nomenclatura atualizada pela Lei 15.352/2026. Se a questão disser que "a ANPD é um ministério" ou que "a ANPD é parte do Poder Judiciário", está errada — ela é **autarquia vinculada ao Ministério da Justiça e Segurança Pública**.

> [!warning] PEGADINHA nº 13 — não confundir os princípios da LGPD com os do Marco Civil
> Os princípios da LGPD (art. 6º — finalidade, adequação, necessidade, etc.) são **diferentes** dos princípios do [[Marco-Civil-da-Internet|Marco Civil]] (art. 3º — liberdade de expressão, neutralidade de rede, etc.). A banca pode misturar princípios de um e outro em uma mesma lista para identificar o "divergente". Guarde as duas listas separadamente.

> [!warning] PEGADINHA nº 14 — consentimento genérico é nulo, não "inválido"
> A lei usa a palavra **nulas** (art. 8º, §4º) para qualificar autorizações genéricas. Questão que disser que "consentimento genérico é válido mas pode ser revogado" está **errada**. Não é revogável — é **nulo ab initio** (desde o início).

> [!warning] PEGADINHA nº 15 — multa da LGPD vs. multa do Marco Civil
> | Lei | Base de cálculo | Teto |
> |:---|:---|:---|
> | **LGPD** (art. 52, II) | Até **2%** do faturamento do grupo/conglomerado no Brasil | **R$ 50 milhões** por infração |
> | **Marco Civil** (art. 12, II) | Até **10%** do faturamento do grupo econômico no Brasil | **Sem teto fixo** |
>
> A banca troca os percentuais e os tetos. Memorize o par.

> [!warning] PEGADINHA nº 16 — prazo de 15 dias (art. 19) × prazos de outras leis
> O prazo de **15 dias** para resposta do controlador (art. 19) não se confunde com prazos da LAI (20+10 dias), da Lei Carolina Dieckmann ou do Marco Civil. Se a questão perguntar "em quanto tempo o controlador deve fornecer declaração completa sobre o tratamento?" a resposta é **até 15 dias**. Não troque com outros prazos.

> [!warning] PEGADINHA nº 17 — dados anonimizados são dados pessoais? NÃO
> Repetimos porque é o erro mais comum: dados **verdadeiramente anonimizados** **não são dados pessoais** e, portanto, **não se sujeitam à LGPD**. A banca pode afirmar que "dado anonimizado é dados pessoais sob a LGPD" — isso é **falso**. Cuidado com pseudonimizado: esse **é** dado pessoal.

> [!warning] PEGADINHA nº 18 — "revogação" do consentimento ≠ "nulidade"
> O consentimento pode ser **revogado** (art. 8º, §5º) a qualquer tempo — é ato do titular. Mas autorizações genéricas são **nulas** (art. 8º, §4º) — é vício do ato. São situações jurídicas diferentes. A revogação retroage para o futuro (a partir da revogação, cessa o tratamento); a nulidade retroage para o passado (o consentimento nunca existiu juridicamente). A banca pode confundir os dois conceitos.

> [!warning] PEGADINHA nº 19 — CNPD (Conselho Nacional) não é a ANPD
> A LGPD criou também o **Conselho Nacional de Proteção de Dados Pessoais e da Privacidade** (CNPD — art. 58-A), que é um órgão **deliberativo** e **consultivo**, não fiscalizador. A **ANPD** é que é o órgão **executivo/fiscalizador** com poder de aplicar sanções. Não confunda: CNPD = conselho deliberativo. ANPD = agência fiscalizadora.

---

## 11. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **Contexto:** Lei 13.709/2018, sanção 14/08/2018, vigência plena 18/09/2020, sanções 01/08/2021; influência do GDPR europeu; alterou o Marco Civil
> - [ ] **Lei 15.352/2026:** "Autoridade Nacional" → **"Agência Nacional de Proteção de Dados (ANPD)"** — autarquia de natureza especial, vinculada ao MJSP
> - [ ] **Âmbito (art. 3º):** qualquer pessoa (física/jurídica, pública/privada) que realize tratamento no território nacional, para oferta a indivíduos no Brasil, ou com dados coletados no Brasil
> - [ ] **Exceções (art. 4º):** pessoa física para fins particulares/não econômicos; fins exclusivamente jornalísticos/artísticos; fins exclusivamente acadêmicos (aplicando-se os arts. 7º e 11); fins exclusivos de segurança pública, defesa nacional, segurança do Estado ou investigação/repressão de infrações penais; dados provenientes do exterior sem comunicação/compartilhamento com agentes brasileiros
> - [ ] **Art. 5º (definições):** dado pessoal (identificação) × sensível (saúde, religião, política, etc.) × anonimizado (não reversível) × pseudonimizado (reversível via chave separada — ainda é dado pessoal); controlador (decide) × operador (executa) × encarregado (canal) × agentes de tratamento (controlador + operador)
> - [ ] **Art. 5º, extensão:** tratamento = toda operação (coleta até eliminação); consentimento = manifestação livre, informada, inequívoca, para finalidade determinada; RIPD = descrição de processos + riscos + mitigação
> - [ ] **Fundamentos (art. 2º):** sete — privacidade, autodeterminação informativa, liberdade de expressão, intimidade/honra/imagem, desenvolvimento tecnológico, livre iniciativa/consumidor, direitos humanos/dignidade/cidadania
> - [ ] **Princípios (art. 6º):** finalidade · adequação · necessidade (minimização) · livre acesso · qualidade dos dados · transparência · segurança · prevenção · não discriminação · responsabilização/accountability
> - [ ] **Bases legais (art. 7º):** consentimento · obrigação legal · políticas públicas · estudos · execução de contrato · exercício de direitos · proteção da vida · tutela da saúde · legítimo interesse · proteção do crédito
> - [ ] **Consentimento (art. 8º):** cláusula destacada se escrito; ônus da prova do **controlador**; autorizações genéricas são **nulas**; pode ser **revogado** a qualquer tempo, gratuitamente
> - [ ] **Legítimo interesse (art. 10):** finalidades legítimas; dados estritamente necessários; ANPD pode exigir RIPD
> - [ ] **Dados sensíveis (art. 11):** consentimento **específico e destacado**; vedação de compartilhamento de dados de saúde para vantagem econômica
> - [ ] **Direitos do titular (art. 18):** confirmação · acesso · correção · anonimização/bloqueio/eliminação · portabilidade (não é absoluta) · eliminação (com consentimento) · informação sobre compartilhamento · informação sobre consequências da negativa · revogação do consentimento
> - [ ] **Art. 19:** resposta em formato simplificado (imediata) ou declaração completa (até **15 dias**)
> - [ ] **Art. 20:** revisão de decisões automatizadas por **pessoa natural** (humano)
> - [ ] **Controlador × operador:** controlador = decide (responde diretamente); operador = executa (responde solidariamente fora das instruções)
> - [ ] **RIPD (art. 5º, XVII):** descrição de processos, riscos e medidas de mitigação; obrigatório para legítimo interesse e dados sensíveis
> - [ ] **Segurança (art. 46):** medidas técnicas e administrativas contra acessos não autorizados e tratamento inadequado
> - [ ] **Incidente (art. 48):** notificar ANPD + titulares em prazo razoável, quando houver risco ou dano relevante; conter natureza dos dados, titulares afetados, medidas de contenção, riscos, motivos de demora, medidas adotadas
> - [ ] **Sanções (art. 52):** advertência · multa de até **2%** (máx. **R$ 50 milhões**, faturamento do grupo) · multa diária · publicização · bloqueio · eliminação · suspensão (até 6 meses, prorrogável) · proibição de atividades
> - [ ] **Sanções ≠ civis ≠ penais** (art. 52, §2º): cumulam-se
> - [ ] **CNPD ≠ ANPD:** CNPD é conselho deliberativo/consultivo; ANPD é agência fiscalizadora com poder sancionatório

> [!warning] O erro mais comum em prova
> **Misturar conceitos, prazos e valores entre leis.** O candidato troca a multa da LGPD (2% / R$ 50 milhões) com a do Marco Civil (10%); confunde "dado anonimizado" com "dado pessoal"; troca "controlador" por "operador"; troca "consentimento nulo" (genérico) com "consentimento revogável"; ou troca "15 dias" (LGPD) com "20+10 dias" (LAI). **Estratégia:** ao ver uma questão sobre a LGPD, o primeiro passo é identificar **qual conceito está em jogo** (definição, princípio, base legal, direito, sanção) e só então aplicar o artigo correspondente. A FGV nunca erra a letra da lei — o erro está em forçar o candidato a ler com atenção. Quando a questão mencionar "Autoridade" ou "Agência", lembre-se: ambos são a ANPD, atualizada pela Lei 15.352/2026.

---

## 12. Próximos passos

Você estudou a **Lei Geral de Proteção de Dados (LGPD)** — o tema mais cobrado do Bloco 1.3. Ela fecha o ciclo de legislação de segurança da informação do Bloco 1.3:

- A [[Lei-de-Acesso-a-Informacao-LAI|LAI]] garantiu o acesso à informação pública e protegeu dados pessoais no contexto do Estado.
- A [[Lei-Carolina-Dieckmann|Lei Carolina Dieckmann]] pune criminalmente a invasão de computadores para obter dados.
- O [[Marco-Civil-da-Internet|Marco Civil]] regulamentou a internet — privacidade, neutralidade, responsabilidade dos provedores.
- A **LGPD** regulamenta o **tratamento de dados pessoais em todos os contextos** — público e privado, digital e analógico — com princípios, bases legais, direitos dos titulares, obrigações dos agentes, segurança da informação e sanções administrativas.

> [!note] Uma ponte para a Segurança da Informação
> Quando você estudar a disciplina de **Segurança da Informação**, verá que os princípios de segurança da LGPD (art. 46) dialogam diretamente com a **Tríade CID** (Confidencialidade, Integridade, Disponibilidade). A LGPD é a **base legal** que torna obrigatório o tratamento seguro de dados — e a Tríade CID é o **modelo técnico** que detalha como isso se faz na prática. Não antecipe esse conteúdo agora — mas saiba que a ponte entre eles é sólida e direta.
>
> Este é o **encerramento do Bloco 1.3** — Legislação de Segurança da Informação e LGPD. Você agora possui as bases jurídicas que sustentarão o restante dos seus estudos. A disciplina de Segurança da Informação, quando chegar, será mais fácil porque você já conhece o arcabouço legal.
