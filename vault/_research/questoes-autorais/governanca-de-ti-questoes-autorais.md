# Gestão e Governança de TI — Questões Autorais Comentadas

> **Disciplina:** Gestão e Governança de TI · **Bloco:** 6.2 — Gestão e Governança de TI (FASE 6 — Segurança e Governança)
> **Banca de referência:** FGV · **Formato:** alternativas A–E
> **Origem:** autoral (todas) · **Não são questões oficiais de banca.**

---

## Questão 01 — Gerenciamento de Projetos (Waterfall, WBS e EVM)

**id:** GOV-001
**disciplina:** Gestão e Governança de TI
**tópico:** Gerenciamento de Projetos
**subtópico:** Tradicional (Waterfall, WBS), híbrido e métricas EVM (CPI/SPI)
**origem:** autoral
**habilidade cognitiva:** aplicação e análise
**dificuldade:** média
**conhecimento avaliado:** fases do modelo em cascata; WBS/EAP como decomposição do escopo por entregáveis (não por fases); fórmulas e interpretação de CPI e SPI no EVM; conceito de projeto híbrido

Uma equipe da DATAPREV está definindo a abordagem de gerenciamento de um projeto de modernização do sistema de concessão de benefícios. Considere as afirmativas abaixo:

I. No modelo em cascata (Waterfall), o projeto é executado em fases sequenciais e completas — cada fase só se inicia após a conclusão da anterior —, com o planejamento detalhado concentrado no início do projeto.

II. A EAP/WBS (Estrutura Analítica do Projeto) decompõe o projeto em fases do ciclo de vida (requisitos, projeto, implementação, testes), de modo que cada nível da estrutura corresponda a uma fase sequencial do cronograma.

III. Na técnica de Valor Agregado (EVM), o SPI é calculado por EV/PV e o CPI por EV/AC; quando SPI > 1, o projeto está adiantado em relação ao cronograma, e, quando CPI > 1, os custos estão abaixo do planejado.

IV. No modelo híbrido, elementos do modelo tradicional e das práticas ágeis são combinados de forma consciente — por exemplo, análise de requisitos formal nas fases iniciais com desenvolvimento iterativo em sprints.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I, III e IV
B) I e III
C) II e IV
D) I, II e III
E) II, III e IV

---

**Gabarito:** A

### Comentário

**Raciocínio:** A questão exige avaliar quatro afirmações sobre gerenciamento de projetos, cada uma testando um conceito distinto: o modelo em cascata, a natureza da WBS/EAP, as fórmulas do EVM e o modelo híbrido. É preciso julgar cada afirmativa isoladamente e, em seguida, montar a combinação correta.

**Palavra-chave:** Waterfall = fases sequenciais e completas; WBS/EAP = decomposição por **entregáveis** (não por fases); SPI = EV/PV (prazo); CPI = EV/AC (custo); `> 1` = bom nos dois índices; híbrido = combinação consciente

**Conceito:**
- **Afirmativa I é verdadeira.** O **Waterfall** organiza o projeto em fases sequenciais e completas (requisitos → análise → projeto → implementação → testes → implantação). Cada fase só começa após a anterior terminar 100%, e o planejamento detalhado é feito no início. É adequado quando os requisitos são **estáveis e bem compreendidos**.
- **Afirmativa II é falsa.** A **WBS/EAP** decompõe o **escopo** do projeto em **entregáveis e pacotes de trabalho** gerenciáveis — não em fases do ciclo de vida. Fases sequenciais são representadas pelo **cronograma**; a WBS é a decomposição do trabalho em produtos/resultados (ex.: Sistema → Módulo → Tela → Ficha de Cadastro). É a base para estimativas, cronograma e atribuição de responsabilidade.
- **Afirmativa III é verdadeira.** No **EVM**, o **SPI** mede eficiência de **prazo** e é calculado por **EV/PV**; o **CPI** mede eficiência de **custo** e é calculado por **EV/AC**. Nos dois índices, **> 1 é bom**: SPI > 1 = adiantado; CPI > 1 = custo abaixo do planejado. Exemplo numérico: PV = R$ 100 mil, EV = R$ 80 mil, AC = R$ 90 mil → SPI = 0,80 (atrasado) e CPI = 0,89 (estourou o orçamento).
- **Afirmativa IV é verdadeira.** O **modelo híbrido** combina, de forma **consciente**, elementos do modelo tradicional e do ágil conforme a fase do projeto — por exemplo, análise de requisitos formal com o INSS (Waterfall) e construção do sistema em sprints (Scrum). Não é "fazer tudo pela metade": é uma decisão fundamentada de onde a rigidez e onde a adaptabilidade são necessárias.

**Análise das alternativas:**
- **A (I, III e IV):** correta — reúne exatamente as afirmativas verdadeiras.
- **B (I e III):** errada — omite IV, que também é verdadeira.
- **C (II e IV):** errada — inclui II (falsa).
- **D (I, II e III):** errada — inclui II (falsa).
- **E (II, III e IV):** errada — inclui II (falsa).

**Pegadinha:** A afirmativa II é a armadilha clássica: a banca descreve a WBS/EAP como se ela organizasse o projeto **por fases do ciclo de vida**. Isso é **falso** — a WBS decompõe por **entregáveis**; quem organiza por tempo é o **cronograma**. A afirmativa III, por sua vez, testa a inversão mais lucrativa do EVM: **CPI é de custo (EV/AC); SPI é de prazo (EV/PV)** — e nos dois, **> 1 é sempre positivo**. Guarde o mnemônico: **C**PI → **C**usto → **C**ompara EV com AC (**A**ctual **C**ost); **S**PI → **S**chedule → **S**e compara EV com PV (**P**lanned **V**alue).

---

## Questão 02 — ITIL v4 (serviço, utilidade × garantia, incidentes, problemas e segurança)

**id:** GOV-002
**disciplina:** Gestão e Governança de TI
**tópico:** ITIL v4
**subtópico:** Conceito de serviço, utilidade e garantia, práticas (incidentes, problemas, mudanças e segurança)
**origem:** autoral
**habilidade cognitiva:** compreensão e análise
**dificuldade:** média
**conhecimento avaliado:** conceito de serviço de TI; distinção utilidade × garantia; diferença entre gestão de incidentes e gestão de problemas; tratamento de incidentes de segurança na ITIL v4

A equipe de operações da DATAPREV está revisando as práticas de gestão de serviços de TI da organização, baseadas na ITIL v4. Considere as afirmativas abaixo:

I. Um serviço de TI é um meio de entregar valor ao cliente, facilitando os resultados que ele deseja alcançar, sem que o cliente tenha de arcar com os custos e riscos específicos da infraestrutura de TI.

II. Na ITIL v4, um incidente é uma interrupção não planejada ou uma redução da qualidade de um serviço de TI; a gestão de incidentes busca restaurar o serviço o mais rapidamente possível, enquanto a gestão de problemas investiga a causa raiz de incidentes recorrentes ou potenciais.

III. Em um serviço de TI, a utilidade corresponde à confiança de que o serviço funcionará conforme o esperado — disponibilidade, capacidade e segurança —, enquanto a garantia corresponde às funcionalidades oferecidas pelo serviço.

IV. Na ITIL v4, incidentes de segurança da informação, como uma tentativa de invasão ou um vazamento de dados, são tratados pela própria gestão de incidentes, que considera também os impactos sobre a confidencialidade, a integridade e a disponibilidade — não existe uma prática separada e exclusiva para incidentes de segurança.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I e III
B) II e IV
C) I, II e III
D) I, III e IV
E) I, II e IV

---

**Gabarito:** E

### Comentário

**Raciocínio:** A questão combina os conceitos mais cobrados da ITIL v4: o que é um serviço de TI, a composição do valor (utilidade × garantia), a distinção entre incidente e problema e o tratamento de incidentes de segurança. É preciso avaliar cada afirmativa com precisão terminológica.

**Palavra-chave:** serviço = entregar valor facilitando resultados; utilidade = funcionalidade; garantia = confiabilidade; incidente = sintoma (restaurar); problema = causa (investigar); incidentes de segurança = mesma gestão de incidentes (sem prática separada)

**Conceito:**
- **Afirmativa I é verdadeira.** O **serviço de TI** é um meio de **entregar valor** ao cliente ao **facilitar os resultados** que ele deseja alcançar, **sem que ele assuma os custos e riscos específicos** da infraestrutura. O sistema de benefícios que funciona 24/7 oculta a complexidade (rede, backup, segurança) e entrega o resultado ao usuário.
- **Afirmativa II é verdadeira.** O **incidente** é a interrupção ou degradação de um serviço em operação — a gestão de incidentes é **reativa e rápida**: restaurar o serviço o quanto antes (muitas vezes com *workaround*). O **problema** é a **causa** de um ou mais incidentes (ou potencial) — a gestão de problemas é **analítica e preventiva**: investigar e eliminar a causa raiz. Lembre: **problemas causam incidentes**, não o contrário.
- **Afirmativa III é falsa.** Os conceitos estão **invertidos**: **utilidade** é a **funcionalidade** oferecida (o que o serviço faz — *fitness for purpose*); **garantia** é a **confiança** de que vai funcionar — disponibilidade, capacidade, continuidade e segurança (*fitness for use*). A banca troca os dois constantemente.
- **Afirmativa IV é verdadeira.** Na ITIL, incidentes de **segurança** são tratados pela **mesma gestão de incidentes** (registro, classificação, restauração) — o que muda é a atenção adicional aos impactos sobre a **tríade CID** (confidencialidade, integridade e disponibilidade). Não existe um "processo separado" para incidentes de segurança.

**Análise das alternativas:**
- **A (I e III):** errada — inclui III (falsa).
- **B (II e IV):** errada — omite I, que também é verdadeira.
- **C (I, II e III):** errada — inclui III (falsa).
- **D (I, III e IV):** errada — inclui III (falsa).
- **E (I, II e IV):** correta — reúne exatamente as afirmativas verdadeiras.

**Pegadinha:** Duas armadilhas clássicas da FGV aparecem aqui. A afirmativa III **inverte utilidade e garantia** — a mais cobrada em ITIL: quem lê rápido associa "garantia" a "garantir que funciona" e erra; na verdade, garantia é a confiabilidade, e utilidade é a funcionalidade. A afirmativa IV explora a pegadinha apontada pela própria ementa (ITIL × Segurança): a banca sugere que incidentes de segurança exigem prática própria — **falso**, eles seguem a gestão de incidentes, com atenção à tríade CID. De brinde, não confunda com a gestão de mudanças, cujas categorias (padrão, normal e urgente) têm fluxos distintos — mudanças urgentes seguem processo acelerado.

---

## Questão 03 — COBIT 2019 (governança × gestão, domínios, princípios e relação com ITIL)

**id:** GOV-003
**disciplina:** Gestão e Governança de TI
**tópico:** COBIT 2019
**subtópico:** Governança × gestão, domínios (EDM, APO, BAI, DSS, MEA), princípios orientadores, relação COBIT × ITIL
**origem:** autoral
**habilidade cognitiva:** análise
**dificuldade:** média
**conhecimento avaliado:** responsabilidade e funções da governança vs. gestão de TI; posição dos domínios EDM e APO/BAI/DSS/MEA; princípio das partes interessadas; relação COBIT × ITIL (níveis diferentes, complementares)

A diretoria da DATAPREV está implementando o COBIT 2019 como framework de governança e gestão de TI. Considere as afirmativas abaixo:

I. No COBIT 2019, a governança de TI é responsabilidade do conselho de administração e da alta direção, que avaliam, dirigem e monitoram a utilização da TI para assegurar o alinhamento aos objetivos estratégicos do negócio.

II. No COBIT 2019, os objetivos de governança estão distribuídos nos domínios de gestão APO, BAI, DSS e MEA, enquanto o domínio EDM (Avaliar, Dirigir e Monitorar) concentra os objetivos de gestão.

III. A ITIL v4 é um framework de governança de TI que substitui o COBIT 2019, pois ambos atuam na mesma camada estratégica da organização.

IV. Um dos princípios orientadores do COBIT é atender às necessidades das partes interessadas, buscando equilibrar os interesses de acionistas, reguladores, clientes e demais envolvidos — e não apenas de um único grupo.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I e II
B) II e III
C) I e IV
D) I, II e IV
E) II, III e IV

---

**Gabarito:** C

### Comentário

**Raciocínio:** A questão testa as duas distinções mais cobradas do COBIT 2019: **governança × gestão** e **COBIT × ITIL**, além de um princípio orientador. É preciso identificar qual afirmativa inverte os papéis e qual atribui o papel errado a cada framework.

**Palavra-chave:** governança = avaliar, dirigir, monitorar (conselho/alta direção); gestão = planejar, construir, executar (gestores de TI); EDM = único domínio de governança; APO/BAI/DSS/MEA = domínios de gestão; ITIL = gestão de serviços (não é governança); COBIT = guarda-chuva estratégico; princípio: partes interessadas

**Conceito:**
- **Afirmativa I é verdadeira.** A **governança** responde a *"para onde ir?"* e *"estamos no caminho certo?"*: é função do **conselho de administração e da alta direção**, que **avaliam, dirigem e monitoram** a TI. A **gestão**, por sua vez, responde a *"como chegar lá?"* e é executada pelos **gestores e profissionais de TI** (planejar, construir, executar, monitorar).
- **Afirmativa II é falsa.** A estrutura está **invertida**. O **EDM** (*Evaluate, Direct and Monitor* — Avaliar, Dirigir e Monitorar) é o **único domínio de governança**; os domínios **APO** (Alinhar, Planejar e Organizar), **BAI** (Construir, Adquirir e Implementar), **DSS** (Entregar, Serviço e Suporte) e **MEA** (Monitorar, Avaliar e Analisar) são os **quatro domínios de gestão**. No total, são 40 objetivos: 5 de governança (EDM) e 35 de gestão.
- **Afirmativa III é falsa.** A **ITIL v4** é um framework de **gestão de serviços** (incidentes, problemas, mudanças, continuidade) — **não é governança**. E **não substitui** o COBIT: os dois são **complementares** e atuam em **níveis diferentes** — COBIT no topo (estratégia e controle) e ITIL na base operacional (entrega e operação de serviços).
- **Afirmativa IV é verdadeira.** O primeiro princípio orientador do COBIT é **atender às necessidades das partes interessadas**: a governança deve equilibrar acionistas, reguladores, clientes, colaboradores e parceiros — não existe governança eficaz que atenda apenas a um grupo.

**Análise das alternativas:**
- **A (I e II):** errada — inclui II (falsa).
- **B (II e III):** errada — ambas falsas.
- **C (I e IV):** correta — reúne exatamente as afirmativas verdadeiras.
- **D (I, II e IV):** errada — inclui II (falsa).
- **E (II, III e IV):** errada — inclui II e III (falsas).

**Pegadinha:** Três inversões rentáveis em uma questão. A afirmativa II **troca EDM por APO** — o EDM é o único domínio de governança, e a banca adora colocá-lo como domínio de gestão. A afirmativa III **promove a ITIL a framework de governança e a substituta do COBIT** — na verdade, ITIL é gestão de serviços e os dois se complementam. E, de fundo, a afirmativa I testa a pegadinha de **atribuir governança ao CIO**: governança é do conselho/alta direção; o CIO participa da gestão. Se a questão mencionar "conselho de administração" ou "direção estratégica", a resposta é governança.

---

## Questão 04 — BPMN (notação, subprocesso, gateways, fluxos e BPMN × UML)

**id:** GOV-004
**disciplina:** Gestão e Governança de TI
**tópico:** BPMN
**subtópico:** Notação (eventos, atividades, gateways, fluxo de sequência), subprocessos, pools/lanes, diferença BPMN × UML
**origem:** autoral
**habilidade cognitiva:** aplicação e compreensão
**dificuldade:** fácil-média
**conhecimento avaliado:** reconhecimento de subprocesso (marcador "+"); diferença entre fluxo de sequência e fluxo de mensagem; lógica do gateway exclusivo; finalidades distintas de BPMN e UML

Durante a modelagem do processo de concessão de benefícios, um analista de negócio da DATAPREV elabora um diagrama BPMN. Considere as afirmativas abaixo:

I. No BPMN, um subprocesso é uma atividade composta, representada por um retângulo de cantos arredondados com um sinal de "+" no centro inferior, indicando que a atividade possui fluxo interno detalhado em outro nível do modelo.

II. O fluxo de sequência é representado por uma linha tracejada com círculo vazio na origem e é o objeto de conexão utilizado para ligar atividades de pools diferentes.

III. Em um gateway exclusivo (XOR), somente um dos caminhos de saída é seguido, conforme a condição avaliada — por exemplo, em um processo de concessão de benefícios, "deferir" ou "indeferir".

IV. BPMN e UML têm a mesma finalidade: ambos modelam a estrutura e o comportamento de sistemas de software orientados a objetos, sendo o BPMN a versão mais recente da UML.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I e II
B) I e III
C) II e IV
D) I, II e III
E) III e IV

---

**Gabarito:** B

### Comentário

**Raciocínio:** A questão cobra a alfabetização visual do BPMN: diferenciar tarefa de subprocesso, fluxo de sequência de fluxo de mensagem, compreender a lógica do gateway exclusivo e não confundir BPMN com UML. Cada afirmativa testa um elemento da notação.

**Palavra-chave:** subprocesso = retângulo arredondado com "+" (atividade composta); fluxo de sequência = seta cheia (interno ao pool); fluxo de mensagem = tracejada com círculo vazio (entre pools); gateway exclusivo (XOR) = um único caminho; BPMN = processo de negócio; UML = software/sistema

**Conceito:**
- **Afirmativa I é verdadeira.** A **tarefa** é uma atividade **atômica** (retângulo arredondado sem marcação); o **subprocesso** é uma atividade **composta**, identificado pelo **"+" no centro inferior**, pois possui um fluxo interno próprio, detalhado em outro nível (versão colapsada) ou desenhado dentro da própria caixa (expandida).
- **Afirmativa II é falsa.** A descrição é do **fluxo de mensagem** (linha **tracejada** com **círculo vazio** na origem), usado para conectar **participantes distintos (pools)**. O **fluxo de sequência** é a **seta de linha contínua (cheia)**, que liga as atividades **dentro do mesmo processo (pool)** — ele **nunca cruza a fronteira de um pool**.
- **Afirmativa III é verdadeira.** O **gateway exclusivo (XOR)** é o losango com "X" (ou vazio): **apenas um** caminho de saída é seguido, segundo a condição avaliada. É o elemento mais cobrado pela FGV em BPMN — decisões como "conceder ou negar", "conforme ou não conforme" usam exatamente esse gateway. Alternativas: gateway **paralelo (AND, "+")** aciona **todos** os caminhos; **inclusivo (OR, "O")** aciona **um ou mais**.
- **Afirmativa IV é falsa.** BPMN e UML são **ambos padrões da OMG**, mas com **finalidades diferentes**: **BPMN** modela **processos de negócio e fluxos de trabalho** (quem-quando-como, com pools, lanes, mensagens); **UML** modela **software e sistemas** orientados a objetos (classes, componentes, casos de uso etc.). O diagrama UML mais próximo em aparência é o **diagrama de atividades** — e mesmo ele descreve o fluxo de controle do sistema, não o processo de negócio.

**Análise das alternativas:**
- **A (I e II):** errada — inclui II (falsa).
- **B (I e III):** correta — reúne exatamente as afirmativas verdadeiras.
- **C (II e IV):** errada — ambas falsas.
- **D (I, II e III):** errada — inclui II (falsa).
- **E (III e IV):** errada — inclui IV (falsa).

**Pegadinha:** A afirmativa II é a inversão mais cobrada: **fluxo de sequência não cruza pool** — quem conecta pools é o **fluxo de mensagem** (tracejada com círculo vazio). A afirmativa IV inverte o par clássico **BPMN × UML**: BPMN é de **negócio/processo**; UML é de **software/sistema**. E a afirmativa I testa o "**+**" do subprocesso — a banca costuma chamar um retângulo com "+" de "tarefa", mas tarefa é a atividade atômica, **sem "+"**. Na prova, responda pelo **desenho**: se o gateway exclusivo mostra os rótulos "deferir" e "indeferir", apenas um caminho ocorre — mesmo que o texto do enunciado sugira o contrário.

---

## Padrões de cobrança utilizados

As questões autorais acima foram inspiradas nos seguintes padrões de cobrança identificados nas questões reais FGV e nas orientações pedagógicas da ementa:

1. **BPMN — gateway exclusivo (DATAPREV 2024, TCE PE 2025, AMAZUL 2026):** decisão com base em condições/regras de negócio → gateway exclusivo (XOR). O elemento mais cobrado de BPMN pela FGV. Inspiração direta para GOV-004 (afirmativa III).
2. **V/F combinando frameworks (CNS014 FGV — governança × gestão):** julgamento de afirmativas em que cada item testa um framework (COBIT, ITIL); a fronteira conceitual governança × gestão é o alvo. Inspiração para GOV-002 e GOV-003. Nota: a questão real da CNS014 mencionava a **ISO/IEC 38500:2024**, norma **fora do edital 2026** — por isso foi deliberadamente **excluída** das questões autorais.
3. **Troca de definições (padrão geral FGV):** atribuir ao framework o papel errado — "ITIL é governança", "COBIT substitui o ITIL", "EDM é domínio de gestão". Inspiração para GOV-003.
4. **BPMN × UML e elementos de conexão (padrão recorrente FGV):** inverter finalidades (negócio × sistema) e inverter fluxo de sequência × fluxo de mensagem. Inspiração para GOV-004.
5. **EVM — CPI/SPI (ementa BLoco 6.2 — métricas EVM):** fórmulas exatas e regra "> 1 é bom"; a armadilha de inverter CPI por SPI é a pegadinha mais rentável do tópico. Inspiração para GOV-001 (afirmativa III).
6. **WBS por entregáveis × por fases (padrão PMI/PMBOK, reforçado na ementa):** distinção entre escopo e cronograma. Inspiração para GOV-001 (afirmativa II).
7. **Julgamento de afirmativas (V/F) com uma ou duas falsas sutis** — formato FGV clássico, replicado em todas as quatro questões, no mesmo registro das questões autorais de Java/Spring e Metodologias já aprovadas no vault.

---