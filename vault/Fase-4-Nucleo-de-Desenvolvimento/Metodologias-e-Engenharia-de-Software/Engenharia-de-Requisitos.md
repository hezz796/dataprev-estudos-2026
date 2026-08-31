# Engenharia de Requisitos

> [!info] Metadados
> **Disciplina:** Metodologias e Engenharia de Software
> **Bloco:** 4.2 — Metodologias e Engenharia de Software (FASE 4 — Núcleo de Desenvolvimento)
> **Tópico:** 5. Engenharia de Requisitos
> **Subtópicos:** Elicitação (entrevistas, questionários, observação, workshops) · Documentação (User Stories, casos de uso, especificações) · Gerenciamento de requisitos (rastreabilidade, priorização MoSCoW e Kano) · Validação e verificação de requisitos
> **Pré-requisitos:** [[Desenvolvimento-de-Sistemas]] (tipos de sistemas, APIs, conceitos de arquitetura) e [[Metodologias-Ageis|Metodologias Ágeis]] (Scrum, User Stories no contexto ágil)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-31

---

## 1. Por que estudar engenharia de requisitos?

Toda a cadeia de desenvolvimento que você estudou — POO, Spring, APIs, Scrum, estimativas — parte de uma pergunta fundamental: **o que o sistema deve fazer?** Antes de escrever uma linha de código, de estimar Pontos de Função ou de montar uma sprint, alguém precisa **descobrir, entender e documentar** o que o usuário precisa. É exatamente isso que a **Engenharia de Requisitos** faz: ela é o **elo entre o usuário (negócio) e o desenvolvedor (tecnologia)**.

Na DATAPREV, onde sistemas críticos atendem milhões de cidadãos e órgãos públicos, requisitos mal capturados podem significar **benefícios calculados incorretamente**, **integrações quebradas** ou **sistemas que não atendem à legislação**. Por isso, a engenharia de requisitos não é burocracia — é **investimento em qualidade**.

> [!question] Pergunta orientadora
> Se o INSS solicita um sistema de cálculo de aposentadoria e o time desenvolve algo que calcula corretamente, mas não gera o relatório que a auditoria exige — o sistema está "errado"? O código está correto, mas o **requisito** (gerar relatório para auditoria) não foi capturado. O problema não foi de programação, foi de **engenharia de requisitos**. É disso que se trata este tópico.

---

## 2. Classificação de requisitos

Antes de estudar o processo, é fundamental entender **o que** está sendo requisitado. Os requisitos se dividem em duas grandes categorias:

### 2.1 Requisitos funcionais

**Requisitos funcionais** descrevem **o que o sistema deve fazer** — as funcionalidades, comportamentos e serviços que ele precisa oferecer. São as "funcionalidades visíveis" ao usuário.

Exemplos:
- "O sistema deve permitir o cadastro de beneficiários com CPF, nome e data de nascimento."
- "O sistema deve calcular o valor da aposentadoria com base nas regras vigentes."
- "O sistema deve gerar um relatório mensal de benefícios pagos."

> [!note] Conexão com APF
> Os requisitos funcionais são a base para a **contagem de Pontos de Função**: cada funcionalidade identificada no APF (ILF, EIF, EI, EO, EQ) corresponde a um ou mais requisitos funcionais.

### 2.2 Requisitos não-funcionais

**Requisitos não-funcionais** descrevem **como** o sistema deve operar — as restrições, atributos de qualidade e condições técnicas que o sistema deve atender, mesmo que o usuário não veja diretamente.

Exemplos:
- "O tempo de resposta para consultas deve ser inferior a 2 segundos."
- "O sistema deve suportar 10.000 usuários simultâneos."
- "Os dados devem ser criptografados em trânsito e em repouso (conforme LGPD)."
- "O sistema deve estar disponível 99,9% do tempo (SLA)."

| Tipo | O que descreve | Exemplo |
|---|---|---|
| **Funcional** | **o que** o sistema faz | cadastrar beneficiário, calcular benefício |
| **Não-funcional** | **como** o sistema opera | performance, segurança, disponibilidade, usabilidade |

> [!warning] PEGADINHA — requisitos não-funcionais são tão importantes quanto os funcionais
> A banca pode sugerir que "requisitos não-funcionais são secundários" — **falso**. Um sistema que cadastra corretamente mas leva 30 segundos para responder (violação de performance) ou que expõe dados pessoais (violação de segurança/LGPD) é um **sistema falho** — mesmo que os requisitos funcionais estejam todos implementados.

---

## 3. Processo de Engenharia de Requisitos

O processo de engenharia de requisitos é uma sequência de atividades que transformam as **necessidades vagas** do usuário em **requisitos documentados, validados e gerenciados**. As quatro atividades principais são:

### 3.1 Elicitação de requisitos

**Elicitação** é o processo de **descobrir e extrair** os requisitos das partes interessadas (stakeholders). É a fase mais desafiadora porque envolve **comunicação com humanos** — e humanos frequentemente não sabem exatamente o que querem, ou dão informações incompletas.

As principais técnicas de elicitação:

| Técnica | Como funciona | Quando usar |
|---|---|---|
| **Entrevistas** | conversa estruturada ou semi-estruturada com stakeholders | quando há acesso direto aos usuários-chave |
| **Questionários** | formulário com perguntas fechadas/abertas distribuído a vários stakeholders | quando há muitos usuários ou estão geograficamente dispersos |
| **Observação (Shadowing)** | observar o usuário **no seu ambiente de trabalho**, executando suas tarefas | quando os usuários têm dificuldade em articular seus processos |
| **Workshops (JAD)** | reunião colaborativa com múltiplos stakeholders para definir requisitos em grupo | quando há consenso a ser alcançado entre áreas diferentes |
| **Prototipação** | criar protótipos visuais para validar requisitos com o usuário | quando o usuário tem dificuldade de imaginar o sistema |

> [!question] Por que não basta perguntar "o que você precisa?"
> Usuários frequentemente **não conseguem expressar** tudo que precisam — ou dão respostas vagas ("preciso de um relatório"). A elicitação combina **múltiplas técnicas** para triangulgar os requisitos reais: a entrevista traz a visão do usuário, a observação revela o que ele *realmente faz* (que pode ser diferente do que *diz* que faz), e o protótipo valida se o que foi entendido está correto.

### 3.2 Análise e especificação de requisitos

Após elicitar, os requisitos precisam ser **analisados** (verificar completude, consistência e prioridade) e **especificados** (documentar de forma clara e não ambígua).

As principais formas de documentação:

#### User Stories (histórias de usuário)

As **User Stories** são a forma de documentação predominante em metodologias ágeis. Têm o formato:

> **Como** [tipo de usuário], **eu quero** [funcionalidade], **para que** [benefício/objetivo].

Exemplo: **"Como** servidor do INSS, **eu quero** consultar o histórico de benefícios de um segurado, **para que** eu possa orientá-lo corretamente."

As User Stories são deliberadamente **simples e curtas** — elas são o "lembrete de conversa", não a documentação completa. Os **critérios de aceitação** complementam a User Story, definindo *quando* ela está implementada:

```text
Cenário: Consulta de histórico
  Dado que o servidor informou o CPF de um segurado
  Quando ele solicita o histórico de benefícios
  Então o sistema exibe a lista de benefícios com data, tipo e valor
  E a consulta é concluída em menos de 2 segundos
```

#### Casos de uso (Use Cases)

Os **casos de uso** são uma forma mais **estruturada e detalhada** de documentação, comum em abordagens tradicionais e em UML. Um caso de uso descreve uma **interação completa** entre um ator (usuário ou sistema externo) e o sistema, incluindo o fluxo principal e alternativas.

Elementos de um caso de uso:
- **Nome:** o que está sendo feito (ex.: "Cadastrar Beneficiário")
- **Ator:** quem inicia a ação (ex.: "Analista de Benefícios")
- **Pré-condições:** o que precisa ser verdade antes (ex.: "analista está autenticado")
- **Fluxo principal:** a sequência de passos bem-sucedidos
- **Fluxos alternativos/ exceções:** o que acontece quando algo sai do esperado
- **Pós-condições:** o estado do sistema após a conclusão

> [!note] User Stories vs. Casos de Uso
> **User Stories** são **breves** ("lembr de conversa"), usadas no ágil, e incentivam o **diálogo** entre time e usuário. **Casos de uso** são **detalhados e formais**, documentam fluxos completos e são mais comuns em projetos com requisitos estabelecidos. Ambos são formas válidas de documentar — a escolha depende da metodologia (Scrum usa User Stories; projetos tradicionais usam casos de uso).

#### Especificações de requisitos

Em projetos maiores ou regulados (como sistemas governamentais), os requisitos são documentados em **documentos formais** de especificação, que incluem descrição detalhada, prioridade, dependências e critérios de validação.

### 3.3 Validação e verificação de requisitos

Essa é uma das áreas mais cobradas — e mais confundidas. **Validação** e **verificação** são atividades **distintas**:

| Conceito | Pergunta-chave | O que verifica |
|---|---|---|
| **Verificação** | "Estamos construindo o produto **direito**?" | se os requisitos estão **corretos, completos, consistentes e não ambíguos** |
| **Validação** | "Estamos construindo o **produto certo**?" | se os requisitos **atendem realmente às necessidades do usuário** |

> [!warning] PEGADINHA — validação ≠ verificação
> Essa é uma das distinções mais cobradas em concursos. **Verificação** olha para o **produto** (está conforme a especificação?); **Validação** olha para o **usuário** (atende ao que ele realmente precisa?). Um sistema pode passar em todas as verificações (está 100% conforme a especificação) e mesmo assim **falhar na validação** (porque a especificação estava errada — não era isso que o usuário queria).
>
> Mnemônico: **V**erificação = "re**V**iso o documento/spec" · **V**alidação = "o usuário **V**alida/aceita?"

Exemplos de técnicas:
- **Verificação:** revisão de requisitos por especialistas, inspeções formais, verificação de consistência e completude.
- **Validação:** prototipação e demonstração ao usuário, testes de aceitação, revisão com stakeholders.

### 3.4 Gerenciamento de requisitos

Após elicitar, documentar e validar, os requisitos precisam ser **gerenciados** ao longo do projeto — porque eles **mudam**.

#### Rastreabilidade (Traceability)

A **rastreabilidade** é a capacidade de **rastrear** cada requisito ao longo de todo o ciclo de vida: de onde ele veio (stakeholder/documento original), para que ele foi implementado (código), como ele foi testado (caso de teste) e para que item do contrato ele corresponde.

A **matriz de rastreabilidade** liga:

```text
Requisito → Design → Código → Teste → Contrato
```

> [!question] Por que rastrear requisitos?
> Se um requisito muda (o INSS altera uma regra de cálculo), a rastreabilidade permite saber **exatamente** quais partes do código, quais testes e quais itens contratuais são afetados — sem precisar revirar todo o projeto. É a base do **controle de mudanças**.

#### Priorização: MoSCoW e Kano

Quando há mais requisitos do que tempo/recursos disponíveis, é preciso **priorizar**. Dois métodos são muito cobrados:

**MoSCoW** — classifica requisitos em quatro categorias:

| Categoria | Significado | Exemplo |
|---|---|---|
| **Must have** | essencial — o sem isso, o sistema não funciona | cálculo correto do benefício |
| **Should have** | importante, mas o sistema funciona sem | notificação por email ao beneficiário |
| **Could have** | desejável — melhora a experiência, mas pode ser cortado | dashboard visual no painel administrativo |
| **Won't have (this time)** | **não será implementado** nesta versão | integração com chatbot de atendimento |

> [!note] MoSCoW é um acrônimo
> **M**ust · **S**hould · **C**ould · **W**on't — é assim que se memoriza.

**Modelo de Kano** — classifica os requisitos com base no **grau de satisfação** do usuário:

| Categoria | Efeito de ter | Efeito de não ter | Exemplo |
|---|---|---|---|
| **Básicos (Must-be)** | não aumenta satisfação (é esperado) | **gera grande insatisfação** | sistema que calcula corretamente o benefício |
| **Performance (One-dimensional)** | aumento proporcional da satisfação | diminuição proporcional da insatisfação | tempo de resposta mais rápido |
| **Excitantes (Attractive)** | **grande aumento** da satisfação | não gera insatisfação (não é esperado) | notificação proativa de novo benefício disponível |
| **Indiferentes** | não afeta satisfação | não afeta insatisfação | cor do fundo da tela |
| **Inversores** | **causa insatisfação** | pode causar satisfação (paradoxo) | notificação excessiva (spambot) |

> [!warning] PEGADINHA — MoSCoW vs. Kano
> **MoSCoW** é um método de **priorização** (o que implementar primeiro). **Kano** é um modelo de **classificação** (como o requisito impacta a satisfação do usuário). A banca pode trocar: "o Kano é um método de priorização" — não exatamente; ele **classifica** os requisitos quanto ao impacto na satisfação, e a partir disso você pode priorizar. E o MoSCoW classifica em Must/Should/Could/Won't — e não há "Could have" no Kano.

---

## 4. Requisitos e o ciclo de vida — a ponte com Scrum e APF

Os requisitos são o ponto de partida de tudo:

- **Estimativas (APF):** cada funcionalidade contada como ILF, EIF, EI, EO ou EQ **nasce de um requisito funcional**. Sem requisitos claros, a contagem de PF é imprecisa.
- **Scrum:** o **Product Backlog** é uma lista de **requisitos** (expressos como User Stories) priorizados pelo Product Owner. Cada sprint seleciona um subconjunto de requisitos para implementar.
- **Tipos de codificação:** os requisitos determinam se o sistema é **transacional** (CRUD), **analítico** (relatórios), **mobile** ou **API**.

> [!question] E se o requisito mudar no meio da sprint?
> Em Scrum, **requisitos não podem ser adicionados** no meio de uma sprint — mas podem ser **repriorizados** no Product Backlog entre sprints. Se o requisito muda drasticamente, o time pode cancelar a sprint (raro) e replanejar. A mudança é **bem-vinda** no ágil — desde que aconteça no momento certo (entre sprints, não no meio).

---

## 5. Como a FGV cobra este tópico

- **Validação vs. Verificação:** a distinção clássica — "produto certo" (validação) vs. "produto direito" (verificação). Muito cobrada e muito confundida.
- **Requisitos funcionais vs. não-funcionais:** a banca cria cenários e pede para classificar.
- **Técnicas de elicitação:** entrevista, questionário, observação, workshop, protótipo — e quando usar cada uma.
- **MoSCoW:** Must/Should/Could/Won't — classificar requisitos em cenários.
- **Kano:** Básicos, Performance, Excitantes — e a relação com satisfação do usuário.
- **User Stories vs. Casos de Uso:** formato simples vs. documentação detalhada.
- **Rastreabilidade:** matriz que liga requisito → código → teste.

> [!warning] PEGADINHA — as armadilhas mais rentáveis
> (1) **Validação** (usuário aceita? = "produto certo") ≠ **Verificação** (está conforme spec? = "produto direito"). (2) **Requisitos não-funcionais** (performance, segurança) são tão críticos quanto os funcionais — não são "extras". (3) **MoSCoW** tem Must/Should/Could/Won't — e o "Won't" não é "nunca", é "nesta versão". (4) **Kano não é MoSCoW** — um classifica quanto à satisfação, o outro prioriza para implementação. (5) **User Stories são lembretes de conversa**, não documentação completa — os critérios de aceitação complementam.

---

## 6. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **Funcional:** o que o sistema faz (cadastrar, calcular, gerar)
> - [ ] **Não-funcional:** como opera (performance, segurança, disponibilidade)
> - [ ] **Elicitação:** entrevistas, questionários, observação, workshops, prototipação
> - [ ] **User Story:** "Como [usuário], eu quero [funcionalidade], para que [benefício]"
> - [ ] **Caso de uso:** ator, fluxo principal, fluxos alternativos, pré/pós-condições
> - [ ] **Verificação:** "estamos construindo o produto **direito**?" (conforme spec)
> - [ ] **Validação:** "estamos construindo o **produto certo**?" (atende ao usuário)
> - [ ] **Rastreabilidade:** ligar requisito → código → teste → contrato
> - [ ] **MoSCoW:** Must · Should · Could · Won't (priorização)
> - [ ] **Kano:** Básicos (esperado) · Performance (proporcional) · Excitantes (surpresa positiva)

> [!warning] O erro mais comum em prova
> Confundir **validação com verificação** — o erro mais clássico. Na questão, pergunte: *estamos verificando se o documento/spec está correto (verificação)? ou estamos validando com o usuário se atende à necessidade dele (validação)?* E não subestime os **requisitos não-funcionais** — eles são frequentemente o motivo de um sistema ser rejeitado em produção.

---

## 7. Fecho do Bloco 4.2 — Metodologias e Engenharia de Software

Com esta nota, você fecha o **Bloco 4.2 — Metodologias e Engenharia de Software**. Recapitule o caminho:

1. **[[Metodologias-Ageis|Metodologias Ágeis]]** — Scrum, Kanban e XP organizam o trabalho e o código;
2. **[[Padroes-de-Desenvolvimento-e-Reuso|Padrões e Reuso]]** — bibliotecas, frameworks e componentes reaproveitam soluções;
3. **[[Tipos-de-Codificacao|Tipos de Codificação]]** — transacional (OLTP), analítico (OLAP), mobile e APIs;
4. **[[Estimativas|Estimativas]]** — APF (pontos de função) e Story Points medem tamanho e esforço;
5. **Engenharia de Requisitos** (esta nota) — descobrir, documentar, validar e gerenciar o que o sistema deve fazer.

A ementa indica que o próximo bloco é o **Bloco 4.3 — Testes de Software**, que depende tanto de Desenvolvimento de Sistemas quanto deste bloco. O TDD que você viu no XP será aprofundado — e novos conceitos (JMockit, Selenium, BDD) serão introduzidos. Prepare-se para entrar na **garantia de qualidade** do software.
