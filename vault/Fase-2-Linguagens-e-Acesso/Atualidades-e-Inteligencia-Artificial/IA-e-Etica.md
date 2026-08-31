# IA e Ética

> [!info] Metadados
> **Disciplina:** Atualidades e Inteligência Artificial
> **Bloco:** 2.2 — Atualidades e IA (FASE 2 — Linguagens e Acesso)
> **Tópico:** 3. IA e Ética
> **Subtópicos:** Viés algorítmico (bias) · Transparência e explicabilidade · Regulamentação de IA no Brasil e no mundo · IA generativa no contexto corporativo e público · Impacto da IA no mercado de trabalho de TI
> **Pré-requisitos:** [[Inteligencia-Artificial-Conceitos-Fundamentais|IA: Conceitos Fundamentais]], [[Raciocinio-Matematico-Aplicado|Raciocínio Lógico Matemático]] e [[LGPD-Lei-Geral-de-Protecao-de-Dados|Legislação/LGPD]]
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-28

---

## 1. Por que estudar ética de IA?

Na nota anterior, você aprendeu *o que* a IA é: uma máquina que aprende padrões a partir de dados, gera conteúdo e prevê resultados. Mas há uma pergunta que nenhum sistema responde sozinho: **devemos usar isso, e até onde?** Esse é o território da **ética de IA** — e, para um concurso, é onde a tecnologia encontra a **lei** e o **direito**.

Este módulo é o ponto de encontro de duas correntes que você já percorreu na Fase 1. Da [[LGPD-Lei-Geral-de-Protecao-de-Dados|LGPD]], você traz os princípios — sobretudo o da **não discriminação** e o direito à **revisão de decisões automatizadas** (art. 20). Do [[Raciocinio-Matematico-Aplicado|raciocínio matemático]], você traz o entendimento de que algoritmos são "matemática aplicada a dados" — portanto, **se os dados têm preconceitos, o algoritmo os aprende**. É exatamente essa matemática que cria o problema ético do **viés**.

> [!tip] Conexão com o pré-requisito
> Um algoritmo é tão bom (ou tão enviesado) quanto os **dados** com que foi treinado. Pense nisso como uma inferência indutiva (sua base de [[Logica-de-Argumentacao|Lógica de Argumentação]]): você conclui padrões a partir dos exemplos que viu. Se os exemplos históricos carregam discriminação, a "regra" que o sistema induz também carregará. **A ética de IA é, em grande parte, uma questão de dados e de projeto.**

---

## 2. Viés algorítmico (bias)

### 2.1 O que é

**Viés algorítmico (bias)** é a tendência de um sistema de IA a produzir resultados **sistematicamente distorcidos ou injustos** em relação a determinados grupos de pessoas. Não é um "erro aleatório" — é um *padrão* de erro que prejudica consistentemente um grupo com base em características como raça, gênero, idade ou condição socioeconômica.

> [!important] Por que "viés" não é só "erro"
> Um sistema que erra 5% das vezes para todo mundo está errando de forma **aleatória**. Um sistema que erra 2% para um grupo e 30% para outro está **enviesado** — o erro se concentra injustamente. Viés é sobre **distribuição desigual de erros/resultados** entre grupos.

### 2.2 Como o viés surge

O viés não é "mágica" nem "má intenção" necessariamente. Ele costuma nascer de duas fontes principais, e a banca adora explorar essa distinção:

1. **Dados enviesados de treinamento**: se os dados históricos usados refletem discriminações passadas, o modelo as reproduz. Ex.: se um banco só emprestou historicamente a um perfil, o modelo "aprende" que outros perfis são mais arriscados — sem que isso seja verdade.
2. **Decisões de projeto**: escolhas dos desenvolvedores — que dados incluir/ignorar, qual variável usar como alvo, como balancear as classes — podem introduzir ou amplificar o viés, mesmo sem intenção.

> [!question] Pergunta orientadora
> Se um sistema de recrutamento histórico foi treinado com currículos que favoreciam candidatos homens (porque os dados antigos de contratação eram assim), de onde vem o viés? **Dos dados de treinamento** — o sistema apenas replicou o padrão histórico. O algoritmo não "inventou" o preconceito; ele o herdou de dados enviesados.

### 2.3 Exemplos concretos

- **Recrutamento**: IA que filtra currículos acaba penalizando grupos sub-representados nos dados históricos de contratação.
- **Crédito**: sistemas de análise de crédito que negam empréstimos a certos grupos com base em correlações enviesadas.
- **Reconhecimento facial**: taxas de erro mais altas para rostos de determinados grupos étnicos, quando os dados de treino não eram representativos — com consequências graves em segurança pública, inclusive com risco de prisões injustas.

### 2.4 Por que é perigoso e a relação com a LGPD

O perigo não é apenas o "erro técnico": é a **discriminação em escala**. Uma decisão enviesada automatizada pode afetar milhares de pessoas de uma vez, de forma opaca e difícil de contestar. É aqui que a ética se conecta com a lei.

A [[LGPD-Lei-Geral-de-Protecao-de-Dados|LGPD]] traz o **princípio da não discriminação** (art. 6º, IX): o tratamento de dados não pode ser realizado para fins discriminatórios ilícitos ou abusivos. E o **art. 20** garante ao titular o direito de solicitar a **revisão de decisões automatizadas** que afetem seus interesses. Ou seja: a lei não proíbe usar IA, mas **proíbe que ela discrimine ilicitamente** e **garante revisão humana** para decisões automáticas. Um sistema enviesado que decide crédito ou seleção pode violar a não discriminação e acionar o direito à revisão.

> [!example] Raciocínio de prova
> Uma questão pode perguntar: "que princípio da LGPD é diretamente ameaçado por um algoritmo que sistematicamente prejudica um grupo étnico?" Resposta: o **princípio da não discriminação** (art. 6º, IX), complementado pelo direito à revisão de decisões automatizadas (art. 20).

---

## 3. Transparência e explicabilidade

### 3.1 Caixa-preta × caixa-branca

Quando um sistema toma uma decisão, *conseguimos dizer por quê?* Essa questão divide os modelos em dois tipos conceituais:

- **Caixa-preta (black box)**: o sistema produz um resultado, mas **não conseguimos enxergar facilmente** como os fatores internos (os pesos, as camadas) chegaram àquela decisão. Redes neurais profundas tendem a ser caixas-pretas: são precisas, porém opacas.
- **Caixa-branca (white box)**: o modelo, ou o processo, permite **entender a lógica** da decisão. Modelos mais simples (como certas árvores de decisão ou regressões) são mais "brancos" — cada decisão pode ser rastreada.

> [!tip] Palavras-chave
> **caixa-preta (opacidade)** · **caixa-branca (transparência)** · **explicabilidade** · **interpretabilidade**.

### 3.2 Explicabilidade: como "abrir" a caixa-preta

Aqui surge um termo técnico importante: **explicabilidade**. Como um modelo de caixa-preta pode ser *preciso* mas *opaco*, desenvolveu-se um campo para **explicar** suas decisões *a posteriori*. Duas ferramentas conceituais que a banca pode citar:

- **Feature importance (importância das características/atributos)**: indica *quais variáveis de entrada mais influenciam* a decisão. "Este resultado foi puxado principalmente por renda e histórico de crédito."
- **LIME e SHAP**: métodos para gerar explicações locais — *por que o modelo decidiu assim para ESTE caso específico?* Não é preciso aprofundar a matemática; basta reconhecer que servem para **explicar decisões** de modelos complexos.

> [!note] O que basta saber
> A prova pede reconhecimento conceitual: explicabilidade = capacidade de explicar por que o modelo decidiu. Feature importance, LIME e SHAP são **mecanismos** dessa explicação. Não memorize fórmulas.

### 3.3 O direito à explicação e o art. 20 da LGPD

Do conceito técnico passamos ao **direito**. Se um humano pode ser prejudicado por uma decisão automática, ele tem o direito de **entender e contestar** essa decisão. A [[LGPD-Lei-Geral-de-Protecao-de-Dados|LGPD]] concretiza isso no **art. 20**:

> [!important] Art. 20 da LGPD — revisão de decisões automatizadas
> O titular tem o direito de solicitar a **revisão de decisões** tomadas **unicamente com base em tratamento automatizado** de dados pessoais que afetem seus interesses — incluindo decisões de **perfilamento** (profissional, consumo, crédito). A revisão deve ser feita por **pessoa natural** — ou seja, por **um ser humano**, não por outro algoritmo. A banca costuma testar justamente essa exigência: "decisões automatizadas são irrevisáveis?" — **não**, a LGPD garante a revisão humana.

> [!warning] O ponto preciso do art. 20
> A revisão é para decisões tomadas **unicamente** com base em tratamento **automatizado**. Se um humano já participou da decisão, não se aplica o "unicamente automatizado" da mesma forma. E a revisão deve ser feita **por pessoa natural**. Estes dois detalhes ("unicamente" e "pessoa natural") são alvos frequentes de pegadinha.

---

## 4. Regulamentação de IA no Brasil e no mundo

### 4.1 O panorama mundial: três grandes abordagens

Não existe uma única lei global de IA. Cada grande ator adotou um caminho, e a banca gosta de contrastá-los.

| Jurisdição | Abordagem | Marca |
|:--|:--|:--|
| **União Europeia** | **Regulamentação abrangente, baseada em risco** | **EU AI Act** — primeiro marco regulatório abrangente do mundo |
| **Brasil** | Projeto de lei ("Marco Legal da IA") em tramitação | **PL 2338/2023** |
| **Estados Unidos** | **Setorial e estadual**, sem lei federal única | regulamentos pontuais + leis de estados |
| **China** | Regras específicas e intervenção estatal forte | regulamentação por domínio (recomendação, deepfake, etc.) |

> [!question] Pergunta orientadora
> Por que a UE adotou um caminho diferente dos EUA? Porque a UE optou por um **modelo baseado em risco** — em vez de uma lei para cada aplicação, ela regula *um mesmo conjunto de regras* que variam conforme o **nível de risco** da aplicação de IA. Os EUA preferiram uma abordagem mais fragmentada, sem uma legislação federal única e abrangente. Cada modelo tem prós e contras; o ponto para a prova é reconhecer qual é qual.

### 4.2 O EU AI Act (União Europeia)

O **EU AI Act** — formalmente o **Regulamento (UE) 2024/1689** — é o **primeiro marco regulatório abrangente de IA do mundo**. Ele entrou em vigor de forma **gradual** (as obrigações se aplicam por faixas de datas). Sua grande inovação estrutural é a abordagem **baseada em risco**: quanto maior o risco de uma aplicação de IA, mais pesadas as obrigações.

As categorias de risco, em ordem decrescente de severidade:

- **Riscos inaceitáveis → PROIBIDOS**: aplicações que violam direitos fundamentais ou valores da UE (ex.: *social scoring* — pontuação social generalizada — e certas formas de manipulação). São banidas.
- **Alto risco → obrigações rigorosas**: sistemas usados em áreas sensíveis (saúde, educação, emprego, infraestrutura crítica, justiça) devem cumprir exigências de governança, documentação, supervisão humana e rastreabilidade.
- **Risco limitado → transparência**: por exemplo, chatbots e *deepfakes* devem informar que o conteúdo é gerado por IA.
- **Risco mínimo → sem obrigações específicas**: a maioria das aplicações de baixo risco.

> [!important] Como a FGV pode cobrar
> Guarde as palavras-chave: **Regulamento (UE) 2024/1689** · **primeiro marco abrangente** · **baseado em risco** · **risco inaceitável = proibido** · **alto risco = obrigações** · **vigência gradual**. A pegadinha mais comum é inverter a lógica: achar que "risco alto vira proibição" — não; **proibidos são os de risco inaceitável**, enquanto os de alto risco são permitidos com obrigações.

### 4.3 O Brasil: o PL 2338/2023 e o "Marco Legal da IA"

No Brasil, o principal instrumento em discussão é o **Projeto de Lei 2338/2023**, o chamado **"Marco Legal da IA"**, de autoria do **Senador Rodrigo Pacheco**. Ele também adota, em linhas gerais, uma lógica **baseada em risco**, inspirada no EU AI Act.

O status legislativo é o ponto que exige **máxima atenção**:

> [!warning] STATUS DE 2026 — CONFIRME ANTES DA PROVA
> Este é um **retrato de 2026**, não um fato permanente. O **PL 2338/2023** foi **aprovado pelo Senado em dezembro de 2024** e **enviado à Câmara dos Deputados em 2025**. **Até meados de 2026, ele ainda NÃO tinha virado lei** — seguia **em tramitação na Câmara**. **NÃO afirme que ele se tornou lei.** Como a tramitação é dinâmica, **confira o status oficial mais próximo da prova** (pelo site do Congresso Nacional / Câmara) e atualize esta nota. Se, à época da prova, o PL já tiver virado lei com outro número, é esse o dado CORRETO a usar.

> [!tip] O que você pode afirmar com segurança (independente do status final)
> O **PL 2338/2023** é o principal texto em debate no Brasil sobre **regulação de IA**; segue a tendência de uma **abordagem baseada em risco**, com **obrigações mais severas para sistemas de alto risco** e proibições para usos considerados inaceitáveis; propõe também a **governança de IA** envolvendo órgãos como a **ANPD** ([[LGPD-Lei-Geral-de-Protecao-de-Dados|ANPD, que você já conhece]]) e, em tese, um **órgão regulador de IA**. Como está em tramitação, prefira frases como "o projeto prevê..." em vez de "a lei determina...".

### 4.4 China e EUA: comparação breve

- **China**: optou por **regulamentações específicas por domínio** e forte intervenção estatal (ex.: regras sobre sistemas de recomendação, *deepfakes* e geração de conteúdo sintético). Não há uma única lei "geral" de IA como o EU AI Act.
- **EUA**: seguem uma abordagem **setorial e estadual** — várias leis estaduais e regulamentos setoriais, **sem uma lei federal única e abrangente** de IA. A discussão envolve também diretrizes e ordens executivas, mas não um marco federal coeso.

> [!warning] PEGADINHA transversal de regulamentação
> Não confunda: **UE** → EU AI Act (abrangente, baseado em risco). **Brasil** → PL 2338/2023 em tramitação. **EUA** → setorial/estadual, sem lei federal única. **China** → regras por domínio com forte controle estatal. Trocar qual país tem lei federal única — ou afirmar que a do Brasil "já é lei" — são os erros mais comuns.

---

## 5. IA generativa no contexto corporativo e público

### 5.1 Usos

A **IA generativa** (que você estudou em [[Inteligencia-Artificial-Conceitos-Fundamentais|IA: Conceitos Fundamentais]] — modelos que *criam* texto, imagem, áudio e código) transformou o uso de IA em empresas e órgãos públicos. Exemplos:

- **Assistentes e atendimento**: chatbots e assistentes virtuais de atendimento ao cidadão/cliente;
- **Automação**: geração de documentos, resumos, minutas e relatórios;
- **Código**: assistentes que geram ou sugerem código para desenvolvedores;
- **Gestão de dados e conhecimento**: busca e síntese em grandes bases documentais.

Para o **setor público** — e para a **DATAPREV**, que desenvolve sistemas para a Previdência Social e o poder público — isso significa **serviços digitais**, **atendimento 24h**, **automação de processos** e melhor **gestão de dados**. É um caminho natural de transformação digital.

### 5.2 Riscos: alucinação e vazamento de dados

O uso de IA generativa, sobretudo LLMs, traz riscos que a ética e a segurança precisam conter:

- **Alucinação**: o modelo gera conteúdo **falso, porém plausível**, com total confiança. Em um contexto público, uma minuta de decisão "alucinada" pode ter consequências graves se não for revista por humano.
- **Vazamento de dados**: quando informações sensíveis são enviadas como *prompt* a um modelo externo, há risco de **exposição de dados pessoais** — o que evoca diretamente a [[LGPD-Lei-Geral-de-Protecao-de-Dados|LGPD]] e seus princípios de **segurança** e **minimização** (não tratar mais dados que o necessário).

### 5.3 Governança: a resposta organizacional

Por isso, o uso corporativo/público de IA passa a exigir **governança**: políticas claras de uso, **supervisão humana**, **controle sobre quais dados podem ser alimentados** nos modelos, **avaliação de risco e de impacto**, auditoria e documentação. A governança é o que transforma "usar IA" em "usar IA com responsabilidade".

> [!example] Raciocínio de prova
> Uma questão pode descrever um órgão público que usa um LLM para gerar respostas a cidadãos, mas um funcionário questiona que o sistema às vezes "inventa" informações. O fenômeno e a mitigação corretos são: **alucinação**, mitigada por **supervisão humana** e verificação, com **política de governança** definindo o que pode ser automatizado.

---

## 6. Impacto da IA no mercado de trabalho de TI

### 6.1 Automação de tarefas × criação de papéis

A pergunta que todo profissional de TI (e todo candidato) faz: *a IA vai me substituir?* A resposta equilibrada, e a mais alinhada à ementa, tem duas faces:

- **Automação de tarefas**: a IA certamente **automatiza tarefas específicas** — geração de código repetitivo, testes iniciais, documentação, inspeção básica. Não é uma substituição do profissional como um todo, mas uma reconfiguração do *que o profissional faz*.
- **Criação de novos papéis**: a IA **cria novas funções e especialidades** — engenharia de prompt, curadoria de dados, avaliação de modelos, governança de IA, auditoria de algoritmos, revisão de conteúdo gerado.

> [!important] A síntese correta
> A IA **muda o trabalho, não (necessariamente) elimina o profissional**. O profissional que *apenas* executa tarefas automatizáveis fica mais exposto; o profissional que **usa a IA como ferramenta** e agrega **crítica, supervisão e ética** se valoriza. Esse é o posicionamento que a FGV tende a considerar correto.

### 6.2 O que muda para o profissional de desenvolvimento

Conectando ao seu futuro (sem antecipar conteúdo de Fases 3+, apenas como visão):

- **Revisão de código gerado**: quem programa passa a **validar** código produzido por IA — precisa entender o código para confiar nele;
- **Engenharia de prompt**: saber formular boas instruções vira habilidade prática (você já aprendeu o básico);
- **Curadoria de dados**: a qualidade da IA depende dos dados — saber selecionar, limpar e avaliar dados é crítico;
- **Ética e responsabilidade**: entender viés, explicabilidade e regulamentação se torna parte do trabalho.

### 6.3 Habilidades que valorizam

- Pensamento crítico para **avaliar** resultados de IA;
- **Conhecimento da área de domínio** (não basta o modelo, é preciso entender o problema);
- **Leitura de código e revisão** (para confiar no código gerado);
- **Comunicação** para formular prompts e explicar decisões;
- **Noções de ética e legislação** (LGPD, regulamentação de IA) — exatamente o que este módulo constrói.

> [!tip] Posicionamento para a prova
> A FGV valoriza a visão **realista e crítica**: IA é ferramenta poderosa, mas com riscos (viés, alucinação, vazamento) e sujeita a regulação; o profissional de TI evolui de "executor" para "supervisor/intérprete" da IA. Evite tanto o alarmismo ("vai acabar com todos os empregos") quanto o entusiasmo ingênuo ("a IA faz tudo sozinha e perfeita").

---

## 7. Questões-modelo comentadas (estilo FGV)

### Questão 1

> [!example] Questão-modelo 1
> Um banco utiliza um sistema de IA para decidir, automaticamente, a concessão de crédito. Um cliente, negado, recorre e questiona o motivo. No âmbito da [[LGPD-Lei-Geral-de-Protecao-de-Dados|LGPD]] (art. 20), o cliente tem:
>
> (A) a garantia de que nenhuma decisão automatizada pode ser usada para crédito.
> (B) o direito a que a decisão seja **revisada por pessoa natural (humano)**.
> (C) o direito a que a IA seja totalmente proibida no setor financeiro.
> (D) o direito a exigir que o algoritmo seja substituído por outro idêntico.
> (E) nenhuma proteção, pois decisões automatizadas são irrevisáveis.

> [!example] Raciocínio comentado
> A alternativa **B** é a correta: o art. 20 garante a revisão de decisões **unicamente automatizadas** que afetem interesses, **por pessoa natural**. (A) erra: a LGPD não proíbe decisões automatizadas — regula-as. (C) erra: não há proibição geral de IA. (E) erra frontalmente: decisões automatizadas **são** revisáveis. (D) é sem sentido técnico/jurídico.

### Questão 2

> [!example] Questão-modelo 2
> Considerando a regulação de IA no cenário 2025-2026, assinale a alternativa correta:
>
> (A) Os Estados Unidos adotaram, desde 2024, uma lei federal única e abrangente sobre IA.
> (B) A União Europeia, por meio do EU AI Act (Regulamento (UE) 2024/1689), adotou uma abordagem **baseada em risco**, proibindo as aplicações de risco inaceitável.
> (C) A China não possui qualquer regra sobre conteúdo gerado por IA.
> (D) O Brasil já sancionou definitivamente o Marco Legal da IA como lei em vigor.
> (E) O EU AI Act trata igualmente todas as aplicações de IA, independentemente do risco.

> [!example] Raciocínio comentado
> A alternativa **B** é a correta: o EU AI Act é baseado em risco e **proíbe** aplicações de **risco inaceitável**, impõe obrigações ao alto risco e transparência ao risco limitado. (A) erra: os EUA não têm lei federal única. (C) erra: a China regula por domínio. (D) erra: no cenário de referência, o PL 2338/2023 **ainda não era lei** (estava na Câmara). (E) erra: a lógica é justamente **graduar** as regras pelo risco.

---

## 8. Palavras-chave que a banca cobra

> [!important] Caixa de ferramentas de ética de IA
> **viés algorítmico (bias)** · **não discriminação (art. 6º, IX, LGPD)** · **dados de treinamento enviesados** · **decisões de projeto** · **reconhecimento facial** · **caixa-preta × caixa-branca** · **explicabilidade** · **feature importance** · **LIME · SHAP** · **revisão de decisões automatizadas (art. 20 LGPD)** · **pessoa natural** · **perfilamento** · **EU AI Act (Regulamento (UE) 2024/1689)** · **abordagem baseada em risco** · **risco inaceitável = proibido** · **PL 2338/2023 (Marco Legal da IA)** · **ANPD** · **alucinação** · **vazamento de dados** · **governança de IA** · **supervisão humana** · **engenharia de prompt** · **curadoria de dados**.

---

## 9. Pegadinhas mais comuns

> [!warning] PEGADINHA 1 — "decisões automatizadas são irrevisáveis"
> É **falso**. O art. 20 da LGPD garante a revisão por **pessoa natural**, quando a decisão for **unicamente automatizada** e afetar interesses. A banca testa justamente esse mito.

> [!warning] PEGADINHA 2 — inverter a lógica de risco no EU AI Act
> **Risco inaceitável = proibido**; **alto risco = obrigações** (não proibição). Uma questão que diz "alto risco é proibido" está errada.

> [!warning] PEGADINHA 3 — afirmar que o Marco Legal da IA já é lei
> No retrato de 2026, o PL 2338/2023 **ainda não era lei** (aprovado no Senado em 2024, enviado à Câmara em 2025, em tramitação). **Confirme o status na data da prova.** Não presuma que virou lei.

> [!warning] PEGADINHA 4 — atribuir lei federal única aos EUA
> Os EUA usam abordagem **setorial/estadual, sem lei federal única**. Quem tem marco abrangente é a **UE** (EU AI Act). Não troque os dois.

> [!warning] PEGADINHA 5 — confundir viés com erro aleatório
> Viés não é "errar um pouco para todos" — é erro que **se concentra** desigualmente em grupos. A própria definição frequentemente aparece errada na alternativa e serve de distrator.

> [!warning] PEGADINHA 6 — confundir explicabilidade com transparência total do modelo
> Explicabilidade ≠ necessariamente "modelo simples". Um modelo de caixa-preta preciso pode ser **explicado a posteriori** (LIME/SHAP). Não caia em "só existe transparência se o modelo for simples".

> [!warning] PEGADINHA 7 — alarmismo vs. otimismo ingênuo sobre o mercado de TI
> A resposta correta costuma ser a intermediária crítica: IA **automatiza tarefas e cria novos papéis**; o profissional evolui para **supervisor/intérprete**, não é simplesmente "substituído" nem "insubstituível".

---

## 10. Próximos passos

Você acaba de fechar o **Bloco 2.2 — Atualidades e Inteligência Artificial**: primeiro o método de atualidades, depois os conceitos de IA, e agora a ética, a regulação e o impacto no trabalho de TI — sempre conectados à [[LGPD-Lei-Geral-de-Protecao-de-Dados|LGPD]] e ao seu futuro profissional. Com isso, você encerra a **Fase 2 (Linguagens e Acesso)**.

A próxima etapa é a **Fase 3 — Banco de Dados**, que também tem como pré-requisitos o [[Raciocinio-Matematico-Aplicado|raciocínio lógico-matemático]] e a [[LGPD-Lei-Geral-de-Protecao-de-Dados|legislação]] que você já domina. Lá você aprenderá modelagem, SQL, normalização (usando bastante a lógica que você já estudou) — e começará a construir a base técnica que sustentará todo o núcleo de desenvolvimento. Antes disso, faça uma revisão agora: atualize os retratos de atualidades e **confirme o status do Marco Legal da IA** com a fonte mais recente próxima da prova.
