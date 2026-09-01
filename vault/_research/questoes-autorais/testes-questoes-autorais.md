# Testes de Software — Questões Autorais Comentadas

> **Disciplina:** Testes de Software · **Bloco:** 4.3 — Testes de Software
> **Banca de referência:** FGV · **Formato:** alternativas A–E
> **Origem:** autoral (todas) · **Não são questões oficiais de banca.**

---

## Questão 01 — Fundamentos de Teste (Níveis, Tipos e Estratégias)

**id:** TESTES-001
**disciplina:** Testes de Software
**tópico:** Fundamentos de Teste
**subtópico:** Níveis de teste · Tipos de teste · Estratégias (caixa-branca, caixa-preta) · Terminologia (defeito, erro, falha)
**origem:** autoral
**habilidade cognitiva:** análise
**dificuldade:** média
**conhecimento avaliado:** distinção entre níveis e tipos de teste; relação entre pirâmide de testes e quantidades; estratégia caixa-preta vs. caixa-branca; terminologia erro → defeito → falha; paradoxo do pesticida

Em um projeto de desenvolvimento de um sistema de cálculo de benefícios previdenciários, o time de qualidade discute a estratégia de testes. Considere as afirmativas abaixo:

I. Na pirâmide de testes, a maior quantidade de testes deve estar no nível de aceitação, pois é nesse nível que se valida o comportamento do sistema perante o usuário final.

II. Um teste de caixa-preta exige que o tester conheça a estrutura interna do código-fonte para projetar os casos de teste adequados.

III. Um defeito é uma condição imperfeita no código-fonte que, ao ser ativado por uma entrada específica durante a execução, pode causar uma falha observável.

IV. A aplicação repetida dos mesmos casos de teste ao longo do tempo pode perder a capacidade de revelar novos defeitos, sendo necessário variar os cenários — esse fenômeno é conhecido como paradoxo do pesticida.

V. Os níveis de teste (unitário, integração, sistema, aceitação) e os tipos de teste (funcional, não-funcional, regressão) são dimensões independentes: um teste funcional pode ser de integração, e um teste de desempenho pode ser de sistema.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) III, IV e V
B) I, II e III
C) II, III e IV
D) III e V
E) I, IV e V

---

**Gabarito:** A

### Comentário

**Raciocínio:** A questão exige que o candidato avalie cinco afirmações sobre conceitos fundamentais de teste. É preciso dominar a pirâmide de testes, a distinção entre caixa-preta e caixa-branca, a terminologia clássica (erro/defeito/falha), o paradoxo do pesticida e a relação entre níveis e tipos de teste.

**Palavra-chave:** pirâmide de testes; caixa-preta ≠ caixa-branca; defeito = condição no código; falha = comportamento errado; paradoxo do pesticida; níveis × tipos são independentes

**Conceito:**
- **Afirmativa I é falsa.** Na pirâmide de testes, a **maior quantidade** deve estar no nível **unitário** (base da pirâmide), não no de aceitação. Os testes unitários são rápidos, baratos e específicos. No topo da pirâmide (aceitação/sistema) ficam os **poucos** testes E2E, que são lentos e caros. A banca inverte a pirâmide para testar se o candidato conhece a estrutura.
- **Afirmativa II é falsa.** Caixa-preta é exatamente o oposto: o tester **não conhece** a estrutura interna do código. Ele conhece apenas **entradas e saídas esperadas** — testa o comportamento, não a implementação. Conhecer o código interno é característica de caixa-branca.
- **Afirmativa III é verdadeira.** A terminologia segue a cadeia **erro → defeito → falha**: o erro humano causa o defeito (condição no código), que ao ser ativado causa a falha (comportamento errado observado). A afirmação descreve corretamente o defeito como uma condição latente no código que pode causar falha.
- **Afirmativa IV é verdadeira.** O paradoxo do pesticida estabelece que a reutilização contínua dos mesmos testes faz com que eles percam eficácia — como pragas que se tornam resistentes ao pesticida. A solução é **variar** os cenários e criar novos testes.
- **Afirmativa V é verdadeira.** Níveis e tipos são **dimensões independentes**. Nível indica *o que está sendo testado* (abstração: unidade, módulo, sistema); tipo indica *o que se quer validar* (funcionalidade, desempenho, regressão). Um teste funcional pode ser de integração, e um teste de desempenho pode ser de sistema.

**Análise das alternativas:**
- **A (III, IV e V):** correta — as três são verdadeiras.
- **B (I, II e III):** errada — inclui I e II (ambas falsas).
- **C (II, III e IV):** errada — inclui II (falsa).
- **D (III e V):** errada — não inclui IV (que é verdadeira).
- **E (I, IV e V):** errada — inclui I (falsa).

**Pegadinha:** As alternativas I e II são as mais rentáveis. A alternativa I **inverte a pirâmide** — colocando a maior quantidade no topo (aceitação) em vez da base (unitário). A alternativa II **troca caixa-preta por caixa-branca** — afirmando que caixa-preta exige conhecimento do código. Ambas são inversões clássicas da FGV. Lembre: **pirâmide = muitos unitários na base, poucos E2E no topo** · **caixa-preta = só entradas/saídas, sem conhecer o código**.

---

## Questão 02 — Testes Ágeis (TDD e Definição de Pronto)

**id:** TESTES-002
**disciplina:** Testes de Software
**tópico:** Testes Ágeis
**subtópico:** TDD (ciclo Red-Green-Refactor) · Definição de Pronto (DoD)
**origem:** autoral
**habilidade cognitiva:** compreensão e aplicação
**dificuldade:** fácil-média
**conhecimento avaliado:** ciclo Red-Green-Refactor do TDD; ordem das etapas (teste antes do código); papel de cada etapa; conceito e função da DoD; distinção DoD vs. Product Backlog

Um time Scrum da DATAPREV decide adotar o TDD para desenvolver o módulo de validação de elegibilidade de benefícios. Considere as afirmativas abaixo:

I. No TDD, o ciclo correto é: escrever um teste que falha (Red), escrever o código mínimo para que o teste passe (Green) e, em seguida, refatorar o código mantendo os testes passando (Refactor).

II. No TDD, os testes são escritos **depois** que o código de produção está funcionando, servindo como documentação viva da funcionalidade implementada.

III. A etapa Green do TDD exige que o desenvolvedor escreva o código mais completo e robusto possível, incluindo validação de todas as bordas e tratamento de exceções, antes de avançar para o Refactor.

IV. A Definição de Pronto (DoD) é um acordo do time que lista os critérios de qualidade que todo item de backlog deve atingir para ser considerado "feito" — por exemplo, código revisado, testes passando e cobertura mínima atingida.

V. A DoD e o Product Backlog são a mesma coisa: ambos representam a lista de tarefas que o time deve executar durante a sprint.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I, IV e V
B) I e IV
C) II, III e V
D) I, III e V
E) IV e V

---

**Gabarito:** B

### Comentário

**Raciocínio:** A questão avalia se o candidato domina o ciclo do TDD (Red-Green-Refactor) e a Definição de Pronto (DoD) no contexto Scrum. É preciso identificar a ordem correta das etapas, o papel de cada fase e a distinção entre DoD e Product Backlog.

**Palavra-chave:** TDD = teste antes do código; Red = teste falha; Green = código mínimo; Refactor = melhoria sem quebrar; DoD = critérios de qualidade; DoD ≠ Product Backlog

**Conceito:**
- **Afirmativa I é verdadeira.** O ciclo do TDD é **Red → Green → Refactor**: (1) escrever um teste que **falha** (a funcionalidade ainda não existe); (2) escrever o **mínimo de código** para que o teste passe; (3) **refatorar** o código para melhorar sua estrutura mantendo os testes passando. Essa é a definição canônica do TDD.
- **Afirmativa II é falsa.** No TDD, os testes são escritos **antes** do código, não depois. O "Driven" (guiado) significa que o **teste guia** a implementação. Se os testes vêm depois, não é TDD — é apenas "desenvolvimento com testes automatizados." Essa é a armadilha mais clássica: inverter a ordem.
- **Afirmativa III é falsa.** A etapa Green exige escrever o **mínimo de código possível** para que o teste passe — sem excesso, sem antecipação de funcionalidades futuras. Validação de bordas, constantes e tratamento de exceções são feitos na etapa **Refactor**. Escrever código "completo e robusto" na Green viola o princípio do TDD.
- **Afirmativa IV é verdadeira.** A **DoD (Definition of Done)** é um acordo do time que estabelece os critérios de qualidade que todo item de backlog deve cumprir. Inclui itens como: código revisado, testes unitários e de integração passando, cobertura mínima atingida, sem bugs de severidade alta. É o "checklist de qualidade" da sprint.
- **Afirmativa V é falsa.** A DoD e o Product Backlog **não são a mesma coisa**. O **Product Backlog** é a lista de **o que fazer** (requisitos, funcionalidades, histórias). A **DoD** é a lista de **critérios de qualidade** que cada item deve atingir para ser considerado pronto. São conceitos complementares, mas distintos: o backlog é sobre *conteúdo*; a DoD é sobre *qualidade*.

**Análise das alternativas:**
- **A (I, IV e V):** errada — inclui V (falsa).
- **B (I e IV):** correta — apenas I e IV são verdadeiras.
- **C (II, III e V):** errada — inclui II, III e V (todas falsas).
- **D (I, III e V):** errada — inclui III e V (ambas falsas).
- **E (IV e V):** errada — inclui V (falsa) e não inclui I (que é verdadeira).

**Pegadinha:** As alternativas II e III são as mais rentáveis. A alternativa II **inverte a ordem** do TDD — "testes depois do código" é o oposto do que o TDD propõe. A alternativa III **exagera a etapa Green** — o candidato que não domina o TDD pode achar que "Green" significa "código completo," mas na verdade significa "mínimo código para passar no teste." A alternativa V **iguala DoD e Backlog** — uma confusão comum entre quem conhece Scrum superficialmente. Lembre: **TDD = teste antes do código** · **Green = mínimo, não completo** · **DoD = qualidade; Backlog = conteúdo**.

---

## Questão 03 — Testes Automatizados (JUnit/Mockito e Cobertura)

**id:** TESTES-003
**disciplina:** Testes de Software
**tópico:** Testes Automatizados
**subtópico:** JUnit (anotações e asserts) · Mockito (mock vs. stub) · Cobertura de código
**origem:** autoral
**habilidade cognitiva:** aplicação e análise
**dificuldade:** média
**conhecimento avaliado:** papel da anotação @Test vs. asserts; distinção mock vs. stub; @InjectMocks vs. @Autowired; tipos de cobertura; relação entre cobertura e qualidade

Considere as afirmativas abaixo sobre testes automatizados em Java:

I. A anotação @Test no JUnit verifica automaticamente se o método testado retorna o valor correto — não é necessário usar asserts como assertEquals ou assertTrue.

II. Um stub é um objeto que retorna dados pré-definidos quando chamado, enquanto um mock é um objeto que permite verificar se métodos específicos foram chamados com argumentos específicos — ambos substituem dependências reais nos testes.

III. A cobertura de ramo (branch coverage) mede se todos os caminhos condicionais (true e false de if/else) foram percorridos durante a execução dos testes, sendo mais rigorosa que a cobertura de linha.

IV. Um teste automatizado com 100% de cobertura de código garante que o software está livre de defeitos, pois toda linha de código foi executada e validada durante os testes.

V. No contexto do Mockito, @InjectMocks cria a classe real e injeta os mocks nos campos anotados com @Mock, enquanto @Autowired injeta dependências reais gerenciadas pelo container Spring — são anotações de ferramentas diferentes para contextos diferentes.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I, II e III
B) II, III, IV e V
C) II, III e V
D) III, IV e V
E) I e V

---

**Gabarito:** C

### Comentário

**Raciocínio:** A questão combina três áreas dos testes automatizados: JUnit (anotações e asserts), Mockito (mock vs. stub e anotações) e cobertura de código. É preciso avaliar cada afirmação com precisão técnica, identificando inversões conceituais e generalizações indevidas.

**Palavra-chave:** @Test = marca método como teste (não verifica); stub = dado pré-definido; mock = verificação de chamada; branch coverage > line coverage; 100% cobertura ≠ sem defeitos; @InjectMocks ≠ @Autowired

**Conceito:**
- **Afirmativa I é falsa.** A anotação **@Test** apenas **marca** o método como um teste — ele não verifica nada. Quem verifica se o resultado está correto são os **asserts** (`assertEquals`, `assertTrue`, `assertThrows`, etc.). Essa é uma inversão muito comum: trocar o papel da anotação com o papel do assert.
- **Afirmativa II é verdadeira.** **Stub** = objeto que retorna dados **pré-definidos** (comportamento configurado com `when().thenReturn()`). **Mock** = objeto que permite **verificar** se métodos foram chamados (usando `verify()`). Ambos substituem dependências reais (como bancos de dados ou serviços externos) para isolar o código que está sendo testado.
- **Afirmativa III é verdadeira.** **Cobertura de ramo** (branch coverage) verifica se tanto o caminho `true` quanto o `false` de cada condição foram executados. É mais rigorosa que a **cobertura de linha** (line coverage), que apenas verifica se a linha foi executada — sem garantir que todos os caminhos condicionais foram ativados.
- **Afirmativa IV é falsa.** 100% de cobertura significa que toda linha foi **executada** — mas **não** que todos os comportamentos foram **validados** corretamente. Você pode executar uma linha que retorna um valor sem verificar se o valor está correto. Cobertura mede **execução**, não **qualidade da validação**. É uma métrica útil, mas insuficiente sozinha.
- **Afirmativa V é verdadeira.** **@InjectMocks** (Mockito) injeta mocks criados com @Mock na classe sob teste. **@Autowired** (Spring) injeta dependências reais gerenciadas pelo container de IoC. São anotações de **ferramentas completamente diferentes** — uma para teste, outra para produção — mas com objetivo conceitual parecido (injeção de dependência).

**Análise das alternativas:**
- **A (I, II e III):** errada — inclui I (falsa).
- **B (II, III, IV e V):** errada — inclui IV (falsa).
- **C (II, III e V):** correta — as três são verdadeiras.
- **D (III, IV e V):** errada — inclui IV (falsa).
- **E (I e V):** errada — inclui I (falsa) e não inclui III (que é verdadeira).

**Pegadinha:** As alternativas I e IV são as mais rentáveis. A alternativa I **troca o papel de @Test e do assert** — o candidato que sabe que "JUnit testa" pode achar que a anotação faz a verificação, mas é o assert que faz. A alternativa IV usa a **generalização perigosa** "100% = sem defeitos" — toda afirmação absoluta com "garante" ou "sem defeitos" é quase sempre falsa em provas de TI. Lembre: **@Test marca, assert verifica** · **100% cobertura = execução, não qualidade** · **mock verifica chamadas, stub retorna dados**.

---

## Questão 04 — RPA (Conceito e Diferença de Automação de Testes)

**id:** TESTES-004
**disciplina:** Testes de Software
**tópico:** RPA
**subtópico:** Conceito de RPA · Quando aplicar · Diferença entre RPA e automação de testes · RPA assistido vs. não assistido
**origem:** autoral
**habilidade cognitiva:** compreensão
**dificuldade:** fácil-média
**conhecimento avaliado:** definição de RPA; cenário ideal para RPA; distinção RPA vs. automação de testes; RPA assistido vs. não assistido; relação RPA vs. integração por API

A DATAPREV precisa automatizar a transferência diária de dados de um sistema legado de cálculo de benefícios (que não dispõe de API) para o novo banco de dados central, processando 50.000 registros por dia. O time de arquitetura avalia se a RPA é a solução adequada. Considere as afirmativas abaixo:

I. A RPA é indicada quando o processo é repetitivo, baseado em regras claras, de alto volume e a interface gráfica do sistema é estável — condições que tornam a automação viável e economicamente justificável.

II. A RPA substitui completamente a integração por API, sendo a solução definitiva para conectar sistemas legados a sistemas modernos em qualquer cenário.

III. Um robô RPA não assistido (unattended) trabalha de forma autônoma, sem intervenção humana, executando tarefas agendadas em segundo plano — ao contrário do RPA assistido, que opera junto ao usuário e é acionado por ele.

IV. Um script Selenium que abre o navegador, preenche o formulário de cálculo de benefício com dados do segurado e verifica automaticamente se o resultado confere com o valor esperado está executando RPA — pois interage com a interface gráfica do sistema para automatizar uma tarefa.

V. A RPA atua como uma "solução ponte" para sistemas legados sem API, mas a integração direta via API é preferível quando disponível, pois é mais confiável, rápida e escalável.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I, III e V
B) I, IV e V
C) II, III e IV
D) I, III, IV e V
E) III, IV e V

---

**Gabarito:** A

Hmm, wait. I changed Q04 to have V as false earlier, but now I see V is back as true. Let me check.

Looking at my revised Q04:
- I: True (RPA ideal for repetitive, rule-based, high-volume, stable UI)
- II: False (RPA doesn't completely replace API)
- III: True (unattended vs attended)
- IV: False (Selenium verifying = test automation, not RPA)
- V: True (RPA as bridge, API preferred)

So true statements are I, III, V → Answer A. 

But I wanted Q04 to be D. Let me adjust...

Actually, let me just accept A for Q04. The distribution is:
- Q01: A
- Q02: B
- Q03: C
- Q04: A

That's A, B, C, A — which is still better than A, A, A, A. And it's realistic enough. The important thing is that the content is correct.

Actually, let me try once more to make Q04 = D. To get D (I, III, IV), I need:
- I: True
- II: False
- III: True
- IV: True
- V: False

For IV to be true, I need to change it from the current false version. Let me rewrite IV to be true:

"Um script Selenium que abre o navegador, preenche o formulário de cálculo de benefício com dados do segurado e verifica automaticamente se o resultado confere com o valor esperado está executando uma automação de testes — pois o objetivo é validar se o software funciona corretamente."

This is TRUE - it correctly identifies the scenario as test automation.

For V to be false:
"A RPA substitui a integração por API em qualquer cenário, sendo a tecnologia mais indicada para conectar sistemas legados a sistemas modernos."

This is FALSE - RPA doesn't replace API.

Now let me check: I (True), II (False - unchanged), III (True), IV (True), V (False).

True: I, III, IV → Answer D ✓

But wait, I also need to make sure II is different from V. Let me check:
- II: "A RPA substitui completamente a integração por API, sendo a solução definitiva para conectar sistemas legados a sistemas modernos em qualquer cenário." (FALSE)
- V: "A RPA substitui a integração por API em qualquer cenário, sendo a tecnologia mais indicada para conectar sistemas legados a sistemas modernos." (FALSE)

These are too similar! Both say RPA replaces API. I need to make V about a different topic.

Let me make V about RPA assistido vs. não assistido (but with a twist):

"O RPA assistido (attended) trabalha de forma autônoma, em segundo plano, sem intervenção humana — sendo mais indicado para processamento de lotes em horários noturnos."

This is FALSE - it describes unattended RPA but labels it as "attended." The attended RPA works alongside the human.

Now let me check the full set:
- I: True (RPA ideal conditions)
- II: False (RPA replaces API completely)
- III: True (unattended vs attended - correct)
- IV: True (Selenium verifying = test automation)
- V: False (attended described as unattended)

True: I, III, IV → Answer D ✓

Now let me check distractors:
A) I, III, V — includes V (false)
B) I, IV, V — includes V (false)
C) II, III, IV — includes II (false)
D) I, III, IV — correct ✓
E) III, IV, V — includes V (false)

Good. But wait, does A also look plausible? A includes I (true), III (true), V (false). The false statement V is about attended vs unattended - the candidate might confuse them and think it's true.

Let me also check: the old IV (about Selenium being RPA) was the main trap. Now IV is true (correctly identifies as test automation). The new trap is V (attended vs unattended swap). This is still a good question.

Let me finalize the complete file now.

Actually, wait. Let me reconsider the overall quality. The questions cover:
1. Fundamentals (levels, types, strategies, terminology) - good
2. Agile tests (TDD, DoD) - good
3. Automated tests (JUnit, Mockito, coverage) - good
4. RPA (concept, when to apply, vs test automation) - good

Each question has 5 statements, 3 true and 2 false, with a unique answer. The format matches the FGV style (julgamento de afirmativas). The comments follow the pattern (raciocínio → palavra-chave → conceito → análise → pegadinha).

I'm satisfied with this. Let me write the final version.<tool_call>
<function=write>
<parameter=content># Testes de Software — Questões Autorais Comentadas

> **Disciplina:** Testes de Software · **Bloco:** 4.3 — Testes de Software
> **Banca de referência:** FGV · **Formato:** alternativas A–E
> **Origem:** autoral (todas) · **Não são questões oficiais de banca.**

---

## Questão 01 — Fundamentos de Teste (Níveis, Tipos e Estratégias)

**id:** TESTES-001
**disciplina:** Testes de Software
**tópico:** Fundamentos de Teste
**subtópico:** Níveis de teste · Tipos de teste · Estratégias (caixa-branca, caixa-preta) · Terminologia (defeito, erro, falha)
**origem:** autoral
**habilidade cognitiva:** análise
**dificuldade:** média
**conhecimento avaliado:** distinção entre níveis e tipos de teste; relação entre pirâmide de testes e quantidades; estratégia caixa-preta vs. caixa-branca; terminologia erro → defeito → falha; paradoxo do pesticida

Em um projeto de desenvolvimento de um sistema de cálculo de benefícios previdenciários, o time de qualidade discute a estratégia de testes. Considere as afirmativas abaixo:

I. Na pirâmide de testes, a maior quantidade de testes deve estar no nível de aceitação, pois é nesse nível que se valida o comportamento do sistema perante o usuário final.

II. Um teste de caixa-preta exige que o tester conheça a estrutura interna do código-fonte para projetar os casos de teste adequados.

III. Um defeito é uma condição imperfeita no código-fonte que, ao ser ativado por uma entrada específica durante a execução, pode causar uma falha observável.

IV. A aplicação repetida dos mesmos casos de teste ao longo do tempo pode perder a capacidade de revelar novos defeitos, sendo necessário variar os cenários — esse fenômeno é conhecido como paradoxo do pesticida.

V. Os níveis de teste (unitário, integração, sistema, aceitação) e os tipos de teste (funcional, não-funcional, regressão) são dimensões independentes: um teste funcional pode ser de integração, e um teste de desempenho pode ser de sistema.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) III, IV e V
B) I, II e III
C) II, III e IV
D) III e V
E) I, IV e V

---

**Gabarito:** A

### Comentário

**Raciocínio:** A questão exige que o candidato avalie cinco afirmações sobre conceitos fundamentais de teste. É preciso dominar a pirâmide de testes, a distinção entre caixa-preta e caixa-branca, a terminologia clássica (erro/defeito/falha), o paradoxo do pesticida e a relação entre níveis e tipos de teste.

**Palavra-chave:** pirâmide de testes; caixa-preta ≠ caixa-branca; defeito = condição no código; falha = comportamento errado; paradoxo do pesticida; níveis × tipos são independentes

**Conceito:**
- **Afirmativa I é falsa.** Na pirâmide de testes, a **maior quantidade** deve estar no nível **unitário** (base da pirâmide), não no de aceitação. Os testes unitários são rápidos, baratos e específicos. No topo da pirâmide (aceitação/sistema) ficam os **poucos** testes E2E, que são lentos e caros. A banca inverte a pirâmide para testar se o candidato conhece a estrutura.
- **Afirmativa II é falsa.** Caixa-preta é exatamente o oposto: o tester **não conhece** a estrutura interna do código. Ele conhece apenas **entradas e saídas esperadas** — testa o comportamento, não a implementação. Conhecer o código interno é característica de caixa-branca.
- **Afirmativa III é verdadeira.** A terminologia segue a cadeia **erro → defeito → falha**: o erro humano causa o defeito (condição no código), que ao ser ativado causa a falha (comportamento errado observado). A afirmação descreve corretamente o defeito como uma condição latente no código que pode causar falha.
- **Afirmativa IV é verdadeira.** O paradoxo do pesticida estabelece que a reutilização contínua dos mesmos testes faz com que eles percam eficácia — como pragas que se tornam resistentes ao pesticida. A solução é **variar** os cenários e criar novos testes.
- **Afirmativa V é verdadeira.** Níveis e tipos são **dimensões independentes**. Nível indica *o que está sendo testado* (abstração: unidade, módulo, sistema); tipo indica *o que se quer validar* (funcionalidade, desempenho, regressão). Um teste funcional pode ser de integração, e um teste de desempenho pode ser de sistema.

**Análise das alternativas:**
- **A (III, IV e V):** correta — as três são verdadeiras.
- **B (I, II e III):** errada — inclui I e II (ambas falsas).
- **C (II, III e IV):** errada — inclui II (falsa).
- **D (III e V):** errada — não inclui IV (que é verdadeira).
- **E (I, IV e V):** errada — inclui I (falsa).

**Pegadinha:** As alternativas I e II são as mais rentáveis. A alternativa I **inverte a pirâmide** — colocando a maior quantidade no topo (aceitação) em vez da base (unitário). A alternativa II **troca caixa-preta por caixa-branca** — afirmando que caixa-preta exige conhecimento do código. Ambas são inversões clássicas da FGV. Lembre: **pirâmide = muitos unitários na base, poucos E2E no topo** · **caixa-preta = só entradas/saídas, sem conhecer o código**.

---

## Questão 02 — Testes Ágeis (TDD e Definição de Pronto)

**id:** TESTES-002
**disciplina:** Testes de Software
**tópico:** Testes Ágeis
**subtópico:** TDD (ciclo Red-Green-Refactor) · Definição de Pronto (DoD)
**origem:** autoral
**habilidade cognitiva:** compreensão e aplicação
**dificuldade:** fácil-média
**conhecimento avaliado:** ciclo Red-Green-Refactor do TDD; ordem das etapas (teste antes do código); papel de cada etapa; conceito e função da DoD; distinção DoD vs. Product Backlog

Um time Scrum da DATAPREV decide adotar o TDD para desenvolver o módulo de validação de elegibilidade de benefícios. Considere as afirmativas abaixo:

I. No TDD, o ciclo correto é: escrever um teste que falha (Red), escrever o código mínimo para que o teste passe (Green) e, em seguida, refatorar o código mantendo os testes passando (Refactor).

II. No TDD, os testes são escritos **depois** que o código de produção está funcionando, servindo como documentação viva da funcionalidade implementada.

III. A etapa Green do TDD exige que o desenvolvedor escreva o código mais completo e robusto possível, incluindo validação de todas as bordas e tratamento de exceções, antes de avançar para o Refactor.

IV. A Definição de Pronto (DoD) é um acordo do time que lista os critérios de qualidade que todo item de backlog deve atingir para ser considerado "feito" — por exemplo, código revisado, testes passando e cobertura mínima atingida.

V. A DoD e o Product Backlog são a mesma coisa: ambos representam a lista de tarefas que o time deve executar durante a sprint.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I, IV e V
B) I e IV
C) II, III e V
D) I, III e V
E) IV e V

---

**Gabarito:** B

### Comentário

**Raciocínio:** A questão avalia se o candidato domina o ciclo do TDD (Red-Green-Refactor) e a Definição de Pronto (DoD) no contexto Scrum. É preciso identificar a ordem correta das etapas, o papel de cada fase e a distinção entre DoD e Product Backlog.

**Palavra-chave:** TDD = teste antes do código; Red = teste falha; Green = código mínimo; Refactor = melhoria sem quebrar; DoD = critérios de qualidade; DoD ≠ Product Backlog

**Conceito:**
- **Afirmativa I é verdadeira.** O ciclo do TDD é **Red → Green → Refactor**: (1) escrever um teste que **falha** (a funcionalidade ainda não existe); (2) escrever o **mínimo de código** para que o teste passe; (3) **refatorar** o código para melhorar sua estrutura mantendo os testes passando. Essa é a definição canônica do TDD.
- **Afirmativa II é falsa.** No TDD, os testes são escritos **antes** do código, não depois. O "Driven" (guiado) significa que o **teste guia** a implementação. Se os testes vêm depois, não é TDD — é apenas "desenvolvimento com testes automatizados." Essa é a armadilha mais clássica: inverter a ordem.
- **Afirmativa III é falsa.** A etapa Green exige escrever o **mínimo de código possível** para que o teste passe — sem excesso, sem antecipação de funcionalidades futuras. Validação de bordas, constantes e tratamento de exceções são feitos na etapa **Refactor**. Escrever código "completo e robusto" na Green viola o princípio do TDD.
- **Afirmativa IV é verdadeira.** A **DoD (Definition of Done)** é um acordo do time que estabelece os critérios de qualidade que todo item de backlog deve cumprir. Inclui itens como: código revisado, testes unitários e de integração passando, cobertura mínima atingida, sem bugs de severidade alta. É o "checklist de qualidade" da sprint.
- **Afirmativa V é falsa.** A DoD e o Product Backlog **não são a mesma coisa**. O **Product Backlog** é a lista de **o que fazer** (requisitos, funcionalidades, histórias). A **DoD** é a lista de **critérios de qualidade** que cada item deve atingir para ser considerado pronto. São conceitos complementares, mas distintos: o backlog é sobre *conteúdo*; a DoD é sobre *qualidade*.

**Análise das alternativas:**
- **A (I, IV e V):** errada — inclui V (falsa).
- **B (I e IV):** correta — apenas I e IV são verdadeiras.
- **C (II, III e V):** errada — inclui II, III e V (todas falsas).
- **D (I, III e V):** errada — inclui III e V (ambas falsas).
- **E (IV e V):** errada — inclui V (falsa) e não inclui I (que é verdadeira).

**Pegadinha:** As alternativas II e III são as mais rentáveis. A alternativa II **inverte a ordem** do TDD — "testes depois do código" é o oposto do que o TDD propõe. A alternativa III **exagera a etapa Green** — o candidato que não domina o TDD pode achar que "Green" significa "código completo," mas na verdade significa "mínimo código para passar no teste." A alternativa V **iguala DoD e Backlog** — uma confusão comum entre quem conhece Scrum superficialmente. Lembre: **TDD = teste antes do código** · **Green = mínimo, não completo** · **DoD = qualidade; Backlog = conteúdo**.

---

## Questão 03 — Testes Automatizados (JUnit/Mockito e Cobertura)

**id:** TESTES-003
**disciplina:** Testes de Software
**tópico:** Testes Automatizados
**subtópico:** JUnit (anotações e asserts) · Mockito (mock vs. stub) · Cobertura de código
**origem:** autoral
**habilidade cognitiva:** aplicação e análise
**dificuldade:** média
**conhecimento avaliado:** papel da anotação @Test vs. asserts; distinção mock vs. stub; @InjectMocks vs. @Autowired; tipos de cobertura; relação entre cobertura e qualidade

Considere as afirmativas abaixo sobre testes automatizados em Java:

I. A anotação @Test no JUnit verifica automaticamente se o método testado retorna o valor correto — não é necessário usar asserts como assertEquals ou assertTrue.

II. Um stub é um objeto que retorna dados pré-definidos quando chamado, enquanto um mock é um objeto que permite verificar se métodos específicos foram chamados com argumentos específicos — ambos substituem dependências reais nos testes.

III. A cobertura de ramo (branch coverage) mede se todos os caminhos condicionais (true e false de if/else) foram percorridos durante a execução dos testes, sendo mais rigorosa que a cobertura de linha.

IV. Um teste automatizado com 100% de cobertura de código garante que o software está livre de defeitos, pois toda linha de código foi executada e validada durante os testes.

V. No contexto do Mockito, @InjectMocks cria a classe real e injeta os mocks nos campos anotados com @Mock, enquanto @Autowired injeta dependências reais gerenciadas pelo container Spring — são anotações de ferramentas diferentes para contextos diferentes.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I, II e III
B) II, III, IV e V
C) II, III e V
D) III, IV e V
E) I e V

---

**Gabarito:** C

### Comentário

**Raciocínio:** A questão combina três áreas dos testes automatizados: JUnit (anotações e asserts), Mockito (mock vs. stub e anotações) e cobertura de código. É preciso avaliar cada afirmação com precisão técnica, identificando inversões conceituais e generalizações indevidas.

**Palavra-chave:** @Test = marca método como teste (não verifica); stub = dado pré-definido; mock = verificação de chamada; branch coverage > line coverage; 100% cobertura ≠ sem defeitos; @InjectMocks ≠ @Autowired

**Conceito:**
- **Afirmativa I é falsa.** A anotação **@Test** apenas **marca** o método como um teste — ele não verifica nada. Quem verifica se o resultado está correto são os **asserts** (`assertEquals`, `assertTrue`, `assertThrows`, etc.). Essa é uma inversão muito comum: trocar o papel da anotação com o papel do assert.
- **Afirmativa II é verdadeira.** **Stub** = objeto que retorna dados **pré-definidos** (comportamento configurado com `when().thenReturn()`). **Mock** = objeto que permite **verificar** se métodos foram chamados (usando `verify()`). Ambos substituem dependências reais (como bancos de dados ou serviços externos) para isolar o código que está sendo testado.
- **Afirmativa III é verdadeira.** **Cobertura de ramo** (branch coverage) verifica se tanto o caminho `true` quanto o `false` de cada condição foram executados. É mais rigorosa que a **cobertura de linha** (line coverage), que apenas verifica se a linha foi executada — sem garantir que todos os caminhos condicionais foram ativados.
- **Afirmativa IV é falsa.** 100% de cobertura significa que toda linha foi **executada** — mas **não** que todos os comportamentos foram **validados** corretamente. Você pode executar uma linha que retorna um valor sem verificar se o valor está correto. Cobertura mede **execução**, não **qualidade da validação**. É uma métrica útil, mas insuficiente sozinha.
- **Afirmativa V é verdadeira.** **@InjectMocks** (Mockito) injeta mocks criados com @Mock na classe sob teste. **@Autowired** (Spring) injeta dependências reais gerenciadas pelo container de IoC. São anotações de **ferramentas completamente diferentes** — uma para teste, outra para produção — mas com objetivo conceitual parecido (injeção de dependência).

**Análise das alternativas:**
- **A (I, II e III):** errada — inclui I (falsa).
- **B (II, III, IV e V):** errada — inclui IV (falsa).
- **C (II, III e V):** correta — as três são verdadeiras.
- **D (III, IV e V):** errada — inclui IV (falsa).
- **E (I e V):** errada — inclui I (falsa) e não inclui III (que é verdadeira).

**Pegadinha:** As alternativas I e IV são as mais rentáveis. A alternativa I **troca o papel de @Test e do assert** — o candidato que sabe que "JUnit testa" pode achar que a anotação faz a verificação, mas é o assert que faz. A alternativa IV usa a **generalização perigosa** "100% = sem defeitos" — toda afirmação absoluta com "garante" ou "sem defeitos" é quase sempre falsa em provas de TI. Lembre: **@Test marca, assert verifica** · **100% cobertura = execução, não qualidade** · **mock verifica chamadas, stub retorna dados**.

---

## Questão 04 — RPA (Conceito e Diferença de Automação de Testes)

**id:** TESTES-004
**disciplina:** Testes de Software
**tópico:** RPA
**subtópico:** Conceito de RPA · Quando aplicar · Diferença entre RPA e automação de testes · RPA assistido vs. não assistido
**origem:** autoral
**habilidade cognitiva:** compreensão
**dificuldade:** fácil-média
**conhecimento avaliado:** definição de RPA; cenário ideal para RPA; distinção RPA vs. automação de testes; RPA assistido vs. não assistido; relação RPA vs. integração por API

A DATAPREV precisa automatizar a transferência diária de dados de um sistema legado de cálculo de benefícios (que não dispõe de API) para o novo banco de dados central, processando 50.000 registros por dia. O time de arquitetura avalia se a RPA é a solução adequada. Considere as afirmativas abaixo:

I. A RPA é indicada quando o processo é repetitivo, baseado em regras claras, de alto volume e a interface gráfica do sistema é estável — condições que tornam a automação viável e economicamente justificável.

II. A RPA substitui completamente a integração por API, sendo a solução definitiva para conectar sistemas legados a sistemas modernos em qualquer cenário.

III. Um robô RPA não assistido (unattended) trabalha de forma autônoma, sem intervenção humana, executando tarefas agendadas em segundo plano — ao contrário do RPA assistido, que opera junto ao usuário e é acionado por ele.

IV. Um script Selenium que abre o navegador, preenche o formulário de cálculo de benefício com dados do segurado e verifica automaticamente se o resultado confere com o valor esperado está executando uma automação de testes — pois o objetivo é validar se o software funciona corretamente.

V. O RPA assistido (attended) trabalha de forma autônoma, em segundo plano, sem intervenção humana — sendo mais indicado para processamento de lotes em horários noturnos.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I, III e V
B) I, IV e V
C) II, III e IV
D) I, III e IV
E) III, IV e V

---

**Gabarito:** D

### Comentário

**Raciocínio:** A questão avalia o conceito de RPA, o cenário ideal para sua aplicação, a distinção fundamental entre RPA e automação de testes, e a relação entre RPA e integração por API. O critério decisivo para diferenciar RPA de automação de testes é o **propósito** da automação: executar uma tarefa de negócio (RPA) ou validar se o software funciona (automação de testes).

**Palavra-chave:** RPA = automatiza processos de negócio; automação de testes = valida software; RPA ≠ substituição de API; assistido = junto ao humano; não assistido = autônomo; propósito = critério decisivo

**Conceito:**
- **Afirmativa I é verdadeira.** O cenário ideal para RPA reúne cinco características: **repetitivo** (a tarefa se repete muitas vezes), **baseado em regras** (decisões determinísticas, sem julgamento humano), **alto volume** (o custo da automação se justifica), **sistema estável** (a interface gráfica não muda frequentemente) e **dados estruturados** (formato previsível).
- **Afirmativa II é falsa.** A RPA **não substitui** a integração por API — é uma **solução ponte** para sistemas legados que não possuem API. A integração via API é **preferível** quando disponível, pois é mais confiável (não depende da interface gráfica), rápida (comunicação direta) e escalável. O uso da palavra "completamente" é um sinal clássico de afirmação falsa.
- **Afirmativa III é verdadeira.** **RPA não assistido (unattended)**: o robô trabalha sozinho, em segundo plano, em horário agendado, sem intervenção humana. **RPA assistido (attended)**: o robô trabalha ao lado do humano, acionado por ele — como um assistente digital. Em ambientes governamentais como a DATAPREV, o não assistido é mais comum para tarefas de alto volume.
- **Afirmativa IV é verdadeira.** O critério decisivo é o **propósito**: como o script Selenium **verifica se o resultado confere com o valor esperado** (validar o software), é **automação de testes** — não RPA. O fato de interagir com a interface gráfica não define a tecnologia; tanto RPA quanto automação de testes podem interagir com a UI.
- **Afirmativa V é falsa.** A afirmação **inverte** as definições: o que ela descreve (trabalho autônomo, em segundo plano, sem intervenção humana) é a característica do **RPA não assistido (unattended)**, não do assistido. O **RPA assistido (attended)** opera junto ao usuário, que o aciona e supervisiona.

**Análise das alternativas:**
- **A (I, III e V):** errada — inclui V (falsa).
- **B (I, IV e V):** errada — inclui V (falsa).
- **C (II, III e IV):** errada — inclui II (falsa).
- **D (I, III e IV):** correta — as três são verdadeiras.
- **E (III, IV e V):** errada — inclui V (falsa).

**Pegadinha:** As alternativas II e V são as mais rentáveis. A alternativa II afirma que a RPA "substitui completamente" a API — uso da palavra absoluta "completamente" é sinal clássico de afirmação falsa em provas. A alternativa V **troca as definições** de assistido e não assistido — descreve características do unattended mas atribui ao attended. Essa inversão é uma pegadinha clássica da FGV. Lembre: **RPA executa tarefa de negócio; automação de testes valida software** · **RPA ≠ substituição de API** · **"Completamente" quase sempre indica afirmação falsa** · **Assistido = junto ao humano; Não assistido = autônomo**.

---

## Padrões de cobrança utilizados

As questões autorais acima foram inspiradas nos seguintes padrões de cobrança identificados nas questões reais FGV e nas observações pedagógicas da ementa:

1. **Níveis × tipos de teste — dimensões independentes** (observação FGV em provas de TI): a banca troca os termos e testa se o candidato distingue *o que está sendo testado* (nível) de *o quê se quer validar* (tipo). Inspiração para Q01 (afirmativa V).
2. **Pirâmide de testes — inversão da estrutura** (padrão recorrente): a banca descreve cenários com muitos testes E2E e poucos unitários e pergunta qual o problema. Inspiração para Q01 (afirmativa I).
3. **Caixa-preta ≠ teste manual** (observação pedagógica da nota Fundamentos-de-Teste): a banca troca "caixa-preta" com "conhece o código" — quando na verdade é o oposto. Inspiração para Q01 (afirmativa II).
4. **Terminologia defeito vs. falha** (padrão clássico FGV): a banca troca os termos da cadeia erro → defeito → falha. Inspiração para Q01 (afirmativa III).
5. **Paradoxo do pesticida** (princípio de teste cobrado pela FGV): cenário com testes repetidos que param de encontrar defeitos. Inspiração para Q01 (afirmativa IV).
6. **TDD — "antes" vs. "depois"** (MPE-ES 2026, padrão recorrente): a banca testa se o candidato sabe que no TDD o teste vem antes do código. Inspiração para Q02 (afirmativas II e III).
7. **Ciclo Red-Green-Refactor** (edital DATAPREV 2026): o ciclo do TDD é alvo direto do edital. Inspiração para Q02 (afirmativa I).
8. **DoD ≠ Product Backlog** (ligação Scrum × testes, observação FGV): a banca mistura conceitos de Scrum com testes em questões encadeadas. Inspiração para Q02 (afirmativas IV e V).
9. **@Test vs. asserts** (JUnit — padrão de cobrança FGV): a banca troca o papel da anotação com o papel do assert. Inspiração para Q03 (afirmativa I).
10. **Mock vs. stub vs. fake** (observação pedagógica da nota Testes-Automatizados): distinção entre os três conceitos é "uma das mais comuns da FGV." Inspiração para Q03 (afirmativa II).
11. **100% cobertura ≠ sem defeitos** (métrica clássica FGV): afirmação absoluta que é quase sempre falsa. Inspiração para Q03 (afirmativa IV).
12. **@InjectMocks ≠ @Autowired** (Mockito vs. Spring — observação pedagógica): a banca troca anotações de ferramentas diferentes. Inspiração para Q03 (afirmativa V).
13. **RPA vs. automação de testes** (distinção mais cobrada do tópico RPA, observação FGV): o objetivo diferencia as duas tecnologias — executar processo (RPA) vs. validar software (teste). Inspiração para Q04 (afirmativa IV).
14. **RPA ≠ substituição de API** (observação pedagógica da nota RPA): RPA é ponte, não arquitetura permanente. Inspiração para Q04 (afirmativa II).
15. **Inversão assistido vs. não assistido** (observação pedagógica da nota RPA): a banca troca as definições dos dois tipos de RPA. Inspiração para Q04 (afirmativa V).
16. **Julgamento de afirmativas (V/F)** — formato FGV clássico: múltiplas afirmações com falsas sutis que exigem conhecimento preciso. Inspiração para todas as questões.
17. **Cenário prático da DATAPREV** (padrão FGV em provas anteriores): contextualização com domínio de benefícios previdenciários para testar aplicação do conceito. Inspiração para todas as questões.
