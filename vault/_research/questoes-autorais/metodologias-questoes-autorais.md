# Metodologias e Engenharia de Software — Questões Autorais Comentadas

> **Disciplina:** Metodologias e Engenharia de Software · **Bloco:** 4.2 — Metodologias e Engenharia de Software
> **Banca de referência:** FGV · **Formato:** alternativas A–E
> **Origem:** autoral (todas) · **Não são questões oficiais de banca.**

---

## Questão 07 — Scrum (Papéis e Eventos)

**id:** MET-ENG-001
**disciplina:** Metodologias e Engenharia de Software
**tópico:** Metodologias Ágeis
**subtópico:** Scrum (papéis: PO, SM, Dev Team; eventos: Daily Scrum)
**origem:** autoral
**habilidade cognitiva:** análise
**dificuldade:** fácil-média
**conhecimento avaliado:** papel do Product Owner vs. Scrum Master; função da Daily Scrum; incrementalidade do Scrum

Em um time Scrum da DATAPREV, o Scrum Master percebe que a equipe está enfrentando problemas de comunicação e de entendimento dos requisitos. Considere as afirmativas abaixo:

I. O Product Owner é responsável por definir o quê deve ser feito e em qual ordem de prioridade — ele representa os stakeholders e maximiza o valor do produto.

II. O Scrum Master é o chefe do time e atribui tarefas a cada membro do Dev Team durante a sprint.

III. A Daily Scrum é uma reunião de 15 minutos em que o Dev Team sincroniza o trabalho e identifica impedimentos — não é um reporte de status para gestores.

IV. A Sprint Review é o momento em que o time demonstra o incremento para os stakeholders e coleta feedback — é nessa reunião que se apresenta o software funcional produzido na sprint.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I, II e III
B) I, III e IV
C) II e IV
D) I e IV
E) Apenas I

---

**Gabarito:** B

### Comentário

**Raciocínio:** A questão testa os três papéis do Scrum e dois de seus cinco eventos. É uma das combinações mais cobradas pela FGV — e uma das que mais geram confusão.

**Palavra-chave:** Product Owner = o quê fazer; Scrum Master = garante o processo (facilitador); Daily Scrum = sincronização do time; Sprint Review = demo + feedback

**Conceito:**
- **Afirmativa I é verdadeira.** O **Product Owner (PO)** define o quê fazer, prioriza o Product Backlog, representa os stakeholders e maximiza o valor do produto. É a "voz do negócio".
- **Afirmativa II é falsa.** O **Scrum Master NÃO é chefe do time** — é um **facilitador/servo-líder**. Ele remove impedimentos e garante que o Scrum funcione. **Não atribui tarefas** — quem decide como fazer é o Dev Team (auto-organizado). Essa é a pegadinha mais clássica da FGV em Scrum.
- **Afirmativa III é verdadeira.** A **Daily Scrum** é uma reunião **do time, para o time** (15 min). Serve para sincronizar ("o que fiz ontem? o que farei hoje? há impedimentos?"). **Não é um reporte para gestores** — se o gestor quer saber o progresso, ele consulta o Sprint Backlog ou participa da Review.
- **Afirmativa IV é verdadeira.** A **Sprint Review** é a demo do incremento para stakeholders, com coleta de feedback. É aqui que se apresenta o software funcional produzido na sprint.

**Análise das alternativas:**
- **A (I, II e III):** errada — inclui II (falsa).
- **B (I, III e IV):** correta.
- **C (II e IV):** errada — inclui II (falsa).
- **D (I e IV):** errada — não inclui III (que é verdadeira).
- **E (Apenas I):** errada — III e IV também são verdadeiras.

**Pegadinha:** A alternativa II é a armadilha mais clássica: "Scrum Master é o chefe" — **falso**. O SM é facilitador, não gerente. E a alternativa III reforça que a Daily não é reporte — outra confusão frequente. Lembre: **PO decide o quê; SM garante o processo; Dev Team decide como e entrega.**

---

## Questão 08 — APF (Análise de Pontos de Função)

**id:** MET-ENG-002
**disciplina:** Metodologias e Engenharia de Software
**tópico:** Estimativas
**subtópico:** APF — funções de dados e transação, independência de tecnologia
**origem:** autoral
**habilidade cognitiva:** compreensão e aplicação
**dificuldade:** média
**conhecimento avaliado:** classificação de funções APF (ILF, EIF, EI, EO, EQ); independência de tecnologia; distinção EO vs. EQ

Um analista de APF está avaliando um sistema de benefícios da DATAPREV. Considere as afirmativas abaixo:

I. Um sistema escrito em Java e um sistema em Python que implementam as mesmas funcionalidades devem ter o mesmo número de Pontos de Função, porque o APF é independente da tecnologia.

II. Um relatório que apresenta o total de benefícios pagos no trimestre, incluindo o cálculo da média e o cruzamento por região, seria classificado como EQ (External Inquiry), pois é apenas uma consulta de dados.

III. A tabela de beneficiários do sistema — dados mantidos e atualizados pelo próprio sistema — é classificada como ILF (Internal Logical File).

IV. O fator de ajuste (VAF) sempre aumenta o PF bruto, pois seus 14 fatores de influência são multiplicativos.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I e II
B) II e IV
C) I e III
D) I, III e IV
E) III e IV

---

**Gabarito:** C

### Comentário

**Raciocínio:** A questão combina conceitos fundamentais do APF: independência de tecnologia, classificação de funções (ILF, EIF, EI, EO, EQ) e o comportamento do fator de ajuste. Cada afirmação precisa ser avaliada com atenção ao detalhe.

**Palavra-chave:** APF independente de tecnologia; ILF = dados internos mantidos; EO = saída com lógica derivada; EQ = saída sem lógica derivada; VAF varia de 0.65 a 1.35

**Conceito:**
- **Afirmativa I é verdadeira.** O APF mede **tamanho funcional do ponto de vista do usuário** — o que o sistema faz, não como foi implementado. Dois sistemas com as mesmas funcionalidades, independentemente da linguagem, devem ter o mesmo PF. Essa é a característica mais importante do APF.
- **Afirmativa II é falsa.** O relatório **calcula média e cruza dados por região** — há **lógica derivada** (processamento adicional além da simples recuperação). Portanto, é **EO** (External Output), não EQ. EQ é para consultas simples, sem processamento.
- **Afirmativa III é verdadeira.** O ILF (Internal Logical File) representa **dados lógicos internos mantidos pelo sistema**. Uma tabela de beneficiários, que o sistema cadastra, atualiza e mantém, é um ILF clássico.
- **Afirmativa IV é falsa.** O VAF varia de **0.65** (todos os fatores = 0) a **1.35** (todos = 5). Quando o VAF é menor que 1.0, ele **reduz** o PF bruto; quando é maior que 1.0, aumenta. Portanto, o fator de ajuste **pode aumentar ou diminuir** o PF bruto — não "sempre aumenta".

**Análise das alternativas:**
- **A (I e II):** errada — II é falsa.
- **B (II e IV):** errada — ambas falsas.
- **C (I e III):** correta.
- **D (I, III e IV):** errada — IV é falsa.
- **E (III e IV):** errada — IV é falsa.

**Pegadinha:** A alternativa II é a mais rentável — o cenário parece ser uma "consulta simples" (EQ), mas o cálculo de média e cruzamento por região configura **lógica derivada** (EO). Pergunte sempre: *há processamento/cálculo além da simples recuperação?* Se sim → EO. Se não → EQ. A alternativa IV usa a palavra "sempre" — e quase toda afirmação absoluta com "sempre" ou "nunca" é falsa em provas.

---

## Questão 09 — Engenharia de Requisitos (Validação vs. Verificação)

**id:** MET-ENG-003
**disciplina:** Metodologias e Engenharia de Software
**tópico:** Engenharia de Requisitos
**subtópico:** Validação e verificação de requisitos; classificação de requisitos
**origem:** autoral
**habilidade cognitiva:** compreensão e análise
**dificuldade:** média
**conhecimento avaliado:** distinção validação vs. verificação; requisitos funcionais vs. não-funcionais; User Stories

Em um projeto de desenvolvimento de um sistema de cálculo de aposentadoria para a DATAPREV, os seguintes requisitos foram levantados:

**Requisito R1:** "O sistema deve calcular corretamente o valor da aposentadoria conforme as regras da legislação vigente."

**Requisito R2:** "O tempo de resposta para consultas ao histórico de contribuições deve ser inferior a 2 segundos."

**Requisito R3:** "Como analista do INSS, eu quero consultar o histórico de contribuições de um segurado para que eu possa orientá-lo sobre sua elegibilidade."

Considere as afirmativas abaixo:

I. O Requisito R2 é um requisito funcional porque descreve uma funcionalidade que o sistema deve oferecer ao usuário.

II. A atividade de verificar se R1 está completo, consistente e não ambíguo responde à pergunta "Estamos construindo o produto certo?"

III. O Requisito R3 está no formato de User Story ("Como… eu quero… para que…").

IV. Validar R2 com os stakeholders significa confirmar que "2 segundos" atende efetivamente à necessidade real de uso do sistema.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I e II
B) III e IV
C) I, III e IV
D) II e III
E) Apenas III

---

**Gabarito:** B

### Comentário

**Raciocínio:** A questão combina três conceitos de Engenharia de Requisitos: classificação funcional/não-funcional, validação vs. verificação, e o formato de User Stories. É preciso avaliar cada afirmação com precisão terminológica.

**Palavra-chave:** Verificação = "produto direito?" (conforme spec); Validação = "produto certo?" (atende ao usuário); funcional = o que o sistema faz; não-funcional = como opera; User Story = "Como… eu quero… para que…"

**Conceito:**
- **Afirmativa I é falsa.** R2 ("tempo de resposta inferior a 2 segundos") descreve uma **restrição de performance** — é um **requisito não-funcional**. Requisitos funcionais descrevem *o que* o sistema faz (funcionalidades); não-funcionais descrevem *como* opera (performance, segurança, disponibilidade).
- **Afirmativa II é falsa.** Verificar se o requisito está completo, consistente e não ambíguo responde à pergunta "Estamos construindo o **produto direito**?" (conforme a especificação). A pergunta "Estamos construindo o **produto certo**?" é da **validação** (se atende ao que o usuário realmente precisa). A banca troca os dois constantemente.
- **Afirmativa III é verdadeira.** R3 segue exatamente o formato de User Story: "Como [tipo de usuário], eu quero [funcionalidade], para que [benefício]".
- **Afirmativa IV é verdadeira.** **Validação** confirma com os stakeholders se o requisito atende à **necessidade real** — se "2 segundos" é suficiente para o uso do sistema. É a pergunta "produto certo?".

**Análise das alternativas:**
- **A (I e II):** errada — ambas falsas.
- **B (III e IV):** correta.
- **C (I, III e IV):** errada — I é falsa.
- **D (II e III):** errada — II é falsa.
- **E (Apenas III):** errada — IV também é verdadeira.

**Pegadinha:** As alternativas I e II condensam as duas confusões mais cobradas neste bloco: (1) tratar requisito não-funcional como funcional; (2) trocar validação por verificação. Mnemônico: **Verificação** = "re**V**iso a spec" · **Validação** = "o usuário **V**alida/aceita?".

---

## Questão 10 — Kanban e XP (Práticas Complementares)

**id:** MET-ENG-004
**disciplina:** Metodologias e Engenharia de Software
**tópico:** Metodologias Ágeis
**subtópico:** Kanban (WIP limits, fluxo contínuo) e XP (TDD, programação em par)
**origem:** autoral
**habilidade cognitiva:** compreensão e aplicação
**dificuldade:** fácil-média
**conhecimento avaliado:** WIP limits como característica definidora do Kanban; natureza relativa dos Story Points; ciclo Red-Green-Refactor do TDD; relação Scrum/XP

Considere as afirmativas abaixo sobre práticas ágeis:

I. O Kanban se caracteriza por sprints fixas de 1 a 4 semanas e pela definição de papéis formais (PO, SM, Dev Team).

II. Um quadro Kanban sem WIP limits (limites de trabalho em progresso) não é verdadeiramente Kanban — é apenas um quadro visual.

III. No TDD (Test-Driven Development), o ciclo correto é: escrever um teste que falha (Red), escrever o código mínimo para passar (Green), refatorar (Refactor).

IV. 1 Story Point equivale a 4 horas de trabalho, permitindo calcular o tempo exato de cada sprint com base nos pontos estimados.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I e III
B) II e III
C) I, II e III
D) II, III e IV
E) Apenas II

---

**Gabarito:** B

### Comentário

**Raciocínio:** A questão combina características do Kanban, do XP e dos Story Points. É preciso identificar as confusões clássicas entre esses frameworks e práticas.

**Palavra-chave:** Kanban = WIP limits + fluxo contínuo (sem sprints); TDD = Red-Green-Refactor; Story Points = relativos (não são horas); XP = práticas de código

**Conceito:**
- **Afirmativa I é falsa.** Sprints fixas e papéis formais (PO, SM, Dev Team) são características do **Scrum**, não do Kanban. O Kanban trabalha com **fluxo contínuo** (sem sprints), **não prescreve papéis** e foca no **tabuleiro visual + WIP limits**. A banca troca características de Scrum e Kanban o tempo todo.
- **Afirmativa II é verdadeira.** O Kanban **só é Kanban** quando há **WIP limits** e **gestão do fluxo** (medir lead time, identificar gargalos). Um quadro de post-its sem limites é apenas um quadro — a definição do Kanban é o controle do fluxo via limites de trabalho em progresso.
- **Afirmativa III é verdadeira.** O ciclo do TDD é **Red-Green-Refactor**: (1) escrever um teste que **falha** (vermelho); (2) escrever o **código mínimo** para que o teste passe (verde); (3) **refatorar** o código mantendo os testes passando. É uma prática do XP.
- **Afirmativa IV é falsa.** Story Points são **unidades abstratas e relativas** — não têm correspondência fixa com horas. 1 Story Point ≠ 4 horas (nem nenhuma outra quantidade fixa). A conversão para tempo depende da **velocity** do time, que é calculada a posteriori. A banca adora criar alternativas com "1 SP = X horas" — todas são falsas.

**Análise das alternativas:**
- **A (I e III):** errada — I é falsa.
- **B (II e III):** correta.
- **C (I, II e III):** errada — I é falsa.
- **D (II, III e IV):** errada — IV é falsa.
- **E (Apenas II):** errada — III também é verdadeira.

**Pegadinha:** As alternativas I e IV são as mais rentáveis: I troca características de Scrum por Kanban (sprints + papéis); IV atribui unidade de tempo a Story Points (que são relativos). Lembre: **Kanban = fluxo + WIP limits (sem sprints)** · **Story Points = relativos (não são horas)** · **TDD = Red → Green → Refactor**.

---

## Padrões de cobrança utilizados

As questões autorais acima foram inspiradas nos seguintes padrões de cobrança identificados nas questões reais FGV:

1. **Scrum — papéis e eventos** (CGE SP, TJ RR, INPE, DATAPREV 2024): distinção PO vs. SM, função da Daily Scrum, incrementalidade. Inspiração para Q07.
2. **APF — independência de tecnologia e classificação de funções** (BANESTES, SES, SEAD-AP, ResolvaMais, BADESC): APF independente da tecnologia; EO vs. EQ com lógica derivada; fator de ajuste. Inspiração para Q08.
3. **Validação vs. Verificação** (padrão recorrente FGV em Engenharia de Requisitos): troca das definições. Inspiração para Q09.
4. **Manifesto Ágil e práticas** (DATAPREV 2024): metodologias ágeis, distinção Scrum/Kanban/XP. Inspiração para Q10.
5. **Kanban sem WIP limits não é Kanban** (padrão recorrente FGV): distinção de quadro visual vs. Kanban real. Inspiração para Q10.
6. **Story Points não são horas** (FGV 2025): natureza relativa e não temporal dos Story Points. Inspiração para Q10.
7. **Julgamento de afirmativas (V/F)** — formato FGV clássico: múltiplas afirmações com uma ou duas falsas sutis. Inspiração para todas as questões de julgamento.
8. **TDD — ciclo Red-Green-Refactor** (padrão recorrente FGV, ligação com XP): ciclo de desenvolvimento orientado a testes. Inspiração para Q10.
