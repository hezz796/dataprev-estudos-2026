# RPA (Robotic Process Automation)

> [!info] Metadados
> **Disciplina:** Testes de Software
> **Bloco:** 4.3 — Testes de Software (FASE 4 — Núcleo de Desenvolvimento)
> **Tópico:** 5. RPA
> **Subtópicos:** Conceito e quando aplicar · Diferença entre RPA e automação de testes · Ferramentas (UiPath, Automation Anywhere — conceito) · RPA assistido vs. não assistido
> **Pré-requisitos:** [[Fundamentos-de-Teste|Fundamentos de Teste]] (conceito de automação de testes) · [[Testes-Automatizados|Testes Automatizados]] (Selenium, automação de UI) · [[Tipos-de-Codificacao|Tipos de Codificação]] (sistemas transacionais, fluxos de negócio)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-31

---

## 1. Por que estudar RPA?

No [[Testes-Automatizados|tópico anterior]] vimos o **Selenium** — uma ferramenta que **automatiza um navegador** para testar se o software funciona. Mas e se o objetivo **não for testar** o software, e sim **executar uma tarefa de negócio repetitiva** na interface de um sistema? Por exemplo: um servidor do INSS precisa transferir dados de um sistema legado para uma planilha, todo dia, 200 vezes. Isso não é um teste — é uma **tarefa de negócio** que poderia ser feita por um "robô digital."

É aqui que entra a **RPA (Robotic Process Automation)** — robôs de software que **automatizam processos de negócio** interagindo com a interface de sistemas existentes, **sem modificar** esses sistemas. O RPA é um tema conceitual no edital da DATAPREV, mas a banca cobra a **distinção entre RPA e automação de testes** — que é a pegadinha mais clássica deste tópico.

> [!question] Pergunta orientadora
> Se o Selenium abre o navegador para **verificar** se o login funciona, e o robô RPA abre o navegador para **executar** uma tarefa de negócio (transferir dados, preencher formulários, gerar relatórios) — a ferramenta é parecida, mas o **objetivo** é completamente diferente. O Selenium **valida o software**; o RPA **usa o software** para realizar um trabalho. Entender essa distinção é o suficiente para a banca.

---

## 2. O que é RPA?

**RPA (Robotic Process Automation)** é uma tecnologia que cria **"robôs" de software** (bots) capazes de executar **tarefas repetitivas, baseadas em regras e de alto volume** — interagindo diretamente com a **interface dos sistemas** existentes (como se fosse um humano usando o sistema), sem precisar modificar a infraestrutura subjacente.

> [!important] "Robô" não significa hardware
> O "robô" da RPA é **software** — não é um robô físico. É um programa que simula as ações de um humano na interface gráfica: clica em botões, preenche campos, copia e cola dados, navega entre telas. A palavra "robô" é uma metáfora — mas a banca pode testar se você sabe disso.

### 2.1 Características do cenário ideal para RPA

| Característica | Por que é bom para RPA |
|---|---|
| **Repetitivo** | A tarefa é feita da mesma forma muitas vezes — o robô não cansa |
| **Baseado em regras** | Tem regras claras e determinísticas (não exige julgamento humano) |
| **Alto volume** | A quantidade de execuções justifica o investimento em automação |
| **Estável** | A interface do sistema não muda frequentemente |
| **Estruturado** | Os dados têm formato previsível |

> [!question] Quando NÃO aplicar RPA?
> RPA **não é adequado** quando: o processo exige **julgamento humano** (decisões subjetivas), a interface do sistema é **altamente instável** (muda toda semana), o volume é **baixo** (não justifica o custo da automação), ou o processo não é **estruturado** (dados não padronizados). Nesses casos, é melhor investir em **integração via API** (conectando sistemas diretamente) do que em RPA (que simula a interface humana).

---

## 3. RPA vs. Automação de Testes — a distinção crítica

Essa é a **pegadinha mais cobrada** deste tópico:

| Aspecto | RPA | Automação de Testes |
|---|---|---|
| **Objetivo** | **Executar** uma tarefa de negócio | **Validar** se o software funciona |
| **Pergunta que responde** | "O robô fez o que deveria?" | "O software está correto?" |
| **Resultado** | Tarefa concluída (dados transferidos, formulário preenchido) | Relatório: passou/falhou |
| **Quem se beneficia** | Operação / negócio (redução de trabalho manual) | Qualidade / engenharia (redução de defeitos) |
| **Ferramenta típica** | UiPath, Automation Anywhere, Blue Prism | JUnit, Selenium, Postman |
| **Quando roda** | Contínuo (executa a tarefa repetidamente) | Durante o ciclo de desenvolvimento/regressão |

> [!warning] PEGADINHA — RPA ≠ automação de testes
> A banca descreve um cenário e pergunta: "Isso é RPA ou automação de testes?" A chave: se o objetivo é **executar um processo de negócio** (copiar dados de A para B, preencher formulário, gerar relatório) → é **RPA**. Se o objetivo é **verificar se o software funciona** (clicar no botão e ver se abre a tela correta) → é **automação de testes**. A **ação** (abrir navegador, clicar, digitar) pode ser igual — o **propósito** é diferente.

> [!question] Um robô Selenium que clica no botão "Calcular Benefício" e verifica se o resultado é 30.000 — isso é RPA ou automação de testes?
> Resposta: **automação de testes** — porque o objetivo é **validar** o cálculo. Se o mesmo robô clicasse no botão, preenchesse os dados e **enviasse o resultado para uma planilha** (sem verificar se está correto), aí seria **RPA** — porque o objetivo é **executar** uma tarefa, não testar.

---

## 4. Arquitetura da RPA — como funciona

O fluxo básico de uma automação RPA é:

1. **Trigger (gatilho):** o robô é acionado (por horário, por evento, por fila de trabalho);
2. **Leitura de dados:** o robô lê dados de uma fonte (planilha, banco, sistema);
3. **Processamento:** o robô aplica regras (validação, transformação, cálculo);
4. **Interação com sistemas:** o robô abre sistemas, preenche campos, clica em botões;
5. **Saída:** o robô grava o resultado (banco de dados, planilha, outro sistema);
6. **Log/relatório:** o robô registra o que fez (para auditoria).

> [!note] RPA não substitui integração por API
> Uma pergunta comum: "Por que não integrar os sistemas diretamente via API, em vez de usar RPA?" Porque muitos sistemas legados (como os da DATAPREV) **não possuem API** — são sistemas antigos, desenvolvidos décadas atrás, que só têm interface gráfica. A RPA é uma "solução de ponte" — automatiza o que não pode ser integrado de outra forma. Mas a integração via API é **preferível** quando possível (é mais confiável, rápida e escalável).

---

## 5. RPA Assistido vs. Não Assistido

| Tipo | O que é | Exemplo |
|---|---|---|
| **RPA Assistido (Attended)** | O robô trabalha **ao lado do humano**, acionado por ele — como um "assistente digital" | O servidor clica em um botão e o robô preenche os campos restantes do formulário |
| **RPA Não Assistido (Unattended)** | O robô trabalha **sozinho**, sem intervenção humana — em segundo plano, em horário agendado | O robô roda à noite, transfere dados entre sistemas e gera relatório |

> [!question] Qual a diferença prática?
> O **assistido** é interativo — o humano inicia e supervisiona. O **não assistido** é autônomo — roda em servidores, sem tela visível, processando lotes. Em ambientes governamentais (como a DATAPREV), o não assistido é mais comum para tarefas de alto volume (processamento de lotes de benefícios, migração de dados).

---

## 6. Ferramentas de RPA

| Ferramenta | Características | Contexto |
|---|---|---|
| **UiPath** | Plataforma líder, interface visual (drag-and-drop), comunidade ativa, orçamento para empresas públicas | Usado em grandes empresas e governo |
| **Automation Anywhere** | Plataforma baseada em nuvem, IA integrada, escala enterprise | Foco em automatização de processos complexos |
| **Blue Prism** | Foco em segurança e governança, usado em setor financeiro | Forte em ambientes regulados |

> [!note] A banca cobra conceito, não ferramenta
> O edital menciona "UiPath, Automation Anywhere — conceito". Isso significa que você deve saber **o que são** e **quando usar**, não dominar a interface. Para a prova, basta saber: são plataformas de RPA que permitem criar robôs de software para automatizar processos de negócio repetitivos.

---

## 7. RPA e o contexto DATAPREV

A DATAPREV é um cenário ideal para RPA por vários motivos:

- **Sistemas legados** que não possuem APIs modernas;
- **Processos de alto volume** (milhões de beneficiários);
- **Tarefas repetitivas** (transferência de dados entre sistemas, geração de relatórios);
- **Necessidade de integração** entre sistemas que foram desenvolvidos em épocas diferentes.

> [!question] Se a DATAPREV usa RPA para transferir dados entre sistemas, isso resolve o problema de integração?
> Parcialmente. A RPA é uma **solução temporária** — funciona, mas é **frágil** (depende da interface gráfica), **lenta** (simula interações humanas) e **difícil de escalar** (cada robô consome recursos como um "usuário virtual"). A solução definitiva é **integração via API** — mas quando os sistemas não têm API (legado antigo), a RPA é a ponte viável. A banca cobra essa nuance: RPA como solução ponte, não como arquitetura permanente.

---

## 8. Como a FGV cobra RPA

- **Conceitual:** a banca pergunta "O que é RPA?" e espera resposta sobre automação de processos de negócio via robôs de software.
- **RPA vs. automação de testes:** a distinção mais cobrada — sempre em cenários onde a ação é parecida mas o objetivo é diferente.
- **Assistido vs. não assistido:** pode cair em questões que descrevem cenários (robô junto ao usuário vs. robô sozinho em servidor).
- **Quando aplicar:** cenários com processos repetitivos, baseados em regras, alto volume.

> [!warning] PEGADINHA — as três armadilhas mais rentáveis
> (1) **RPA ≠ automação de testes** — RPA executa processos de negócio; automação de testes valida software. (2) **RPA não substitui integração por API** — RPA é ponte para sistemas legados; API é preferível quando disponível. (3) **"Robô" da RPA é software** — não é hardware/robô físico.

---

## 9. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **RPA:** robôs de software que automatizam **processos de negócio** (não testes) na interface de sistemas existentes
> - [ ] **Cenário ideal:** repetitivo + baseado em regras + alto volume + sistema estável + dados estruturados
> - [ ] **Quando NÃO usar:** julgamento humano necessário, interface instável, volume baixo, processo não estruturado
> - [ ] **RPA ≠ automação de testes** — RPA = executa tarefa de negócio · automação de testes = valida software
> - [ ] **RPA ≠ integração por API** — RPA é ponte para legado; API é preferível quando disponível
> - [ ] **Assistido (Attended):** junto ao humano, acionado por ele
> - [ ] **Não Assistido (Unattended):** sozinho, em segundo plano, horário agendado
> - [ ] **Ferramentas:** UiPath, Automation Anywhere, Blue Prism (conceito, não interface)

> [!question] Revise mentalmente
> A DATAPREV precisa transferir dados de um sistema legado (sem API) para um novo banco de dados, todo dia, com 50.000 registros. Isso é RPA ou automação de testes? Qual tipo (assistido ou não assistido)? *(Resposta: RPA — porque o objetivo é executar uma tarefa de negócio (transferência de dados), não validar software. Tipo não assistido — porque é um processo diário de alto volume que não precisa de intervenção humana.)*

---

## 10. Fim do Bloco 4.3 — Testes de Software

Parabéns! Você completou o Bloco 4.3 — Testes de Software. Neste bloco, você aprendeu:

1. **[[Fundamentos-de-Teste]]** — níveis, tipos, estratégias e princípios de teste;
2. **[[Testes-Ageis]]** — TDD (ciclo Red-Green-Refactor aprofundado), BDD (Gherkin/Cucumber), DoD e pirâmide de testes;
3. **[[Testes-Automatizados]]** — JUnit 5, Mockito (mock/stub/fake), Selenium (WebDriver), cobertura de código (JaCoCo);
4. **[[Gestao-do-Ciclo-de-Vida-de-Testes]]** — plano de teste, registro de defeitos, severidade vs. prioridade, métricas;
5. **[[RPA]]** — conceito, RPA vs. automação de testes, assistido vs. não assistido.

Com isso, você fecha o **Núcleo de Desenvolvimento** (Fase 4): [[Java-e-Ecossistema-JVM|Java]], [[Frameworks-Java|Spring]], [[Metodologias-Ageis|Metodologias Ágeis]] e agora **Testes de Software**. Você tem a base sólida para avançar para a **Fase 5 — Frontend e Interfaces**, onde verá Vue, Angular, React e Arquitetura de Software Avançada.
