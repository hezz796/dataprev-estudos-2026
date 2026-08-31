# Padrões de Desenvolvimento e Reuso

> [!info] Metadados
> **Disciplina:** Metodologias e Engenharia de Software
> **Bloco:** 4.2 — Metodologias e Engenharia de Software (FASE 4 — Núcleo de Desenvolvimento)
> **Tópico:** 2. Padrões de Desenvolvimento e Reuso
> **Subtópicos:** Padrões de projeto aplicados ao desenvolvimento · Componentização e modularização · Bibliotecas e frameworks como formas de reuso
> **Pré-requisitos:** [[Padroes-de-Projeto-e-Arquitetura|Padrões de Projeto e Arquitetura]] (GoF, MVC, SOA) e [[Paradigma-Orientado-a-Objetos|POO]] (encapsulamento, herança, polimorfismo)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-31

---

## 1. Por que estudar padrões de desenvolvimento e reuso?

Você já conhece os **padrões GoF** (Singleton, Factory, Strategy, Observer) e as **arquiteturas** (MVC, SOA) do [[Padroes-de-Projeto-e-Arquitetura|Bloco 4.1]]. Mas conhecer um padrão é diferente de **aplicá-lo como forma de reuso**. Este tópico muda o olhar: em vez de estudar cada padrão isoladamente, vamos pensar em como eles — junto com **bibliotecas, frameworks e componentes** — formam um sistema de **reutilização de soluções** que acelera o desenvolvimento e reduz erros.

Na DATAPREV, o reuso é uma questão de **eficiência e padronização**: se dezenas de sistemas precisam autenticar usuários, consultar benefícios e gerar relatórios, faz sentido **reutilizar** soluções testadas em vez de reescrevê-las a cada projeto. O reuso é o que permite que o tempo gasto em um projeto beneficie todos os outros.

> [!question] Pergunta orientadora
> Se você já implementou o padrão Strategy para calcular descontos em um sistema de pedidos, por que reescrevê-lo em outro sistema que precisa da mesma flexibilidade? A resposta óbvia é "reutilize" — mas *como* reutilizar? É exatamente isso que vamos entender: os **níveis de reuso** e como cada um se manifesta no desenvolvimento real.

---

## 2. O que é reuso de software?

**Reuso** é o ato de utilizar artefatos, soluções ou componentes já existentes — em vez de criá-los do zero — para resolver um problema similar. O reuso se dá em diferentes **níveis**:

| Nível de reuso | O que é reutilizado | Exemplo |
|---|---|---|
| **Reuso de código** | Trechos de código, funções, classes | Copiar uma função de validação de CPF para outro projeto |
| **Reuso de design (solução)** | **Padrões de projeto** — a *solução* para um problema recorrente | Aplicar o padrão Factory para criar diferentes tipos de relatório |
| **Reuso de componente** | Módulo/componente **independente e reutilizável** | Biblioteca de componentes de UI (botões, formulários) |
| **Reuso de framework** | Um **framework** que estrutura toda a aplicação | Usar Spring Boot para criar uma API RESTful em vez de montar tudo manualmente |

> [!important] Reuso de código ≠ reuso de design
> Essa é uma distinção que a banca cobra. O **reuso de código** é copiar/colar ou importar trechos de código — é o nível mais baixo e mais frágil (se o código original mudar, você precisa atualizar todas as cópias). O **reuso de design** é aplicar uma **solução consagrada** (um padrão) que resolve o problema de forma genérica e flexível — mesmo que o código concreto seja diferente. A **Factory Method**, por exemplo, é um reuso de *design*: cada implementação concreta tem código diferente, mas a *solução* (deslocar a criação para um método) é reutilizada.

---

## 3. Padrões de projeto como instrumento de reuso

Os **padrões GoF** são, por natureza, **soluções reutilizáveis**. Cada padrão descreve um *template* de solução que pode ser aplicado a diferentes contextos — é reuso no nível de **design**.

Vamos revisitar os padrões mais cobrados sob a ótica do reuso:

### 3.1 Strategy — reuso de comportamento

O **Strategy** permite definir uma **família de algoritmos** e trocá-los em tempo de execução. Cada vez que você precisa de **flexibilidade no algoritmo**, está reaproveitando o mesmo *design*:

- No sistema de benefícios: Strategy para calcular diferentes tipos de aposentadoria.
- No sistema de pagamentos: Strategy para diferentes meios de pagamento (PIX, cartão, boleto).
- O **código-base** (a classe de contexto) é o mesmo; apenas as **estratégias concretas** mudam.

Isso é reuso de design aplicado: o padrão garante que, ao adicionar uma nova estratégia, você não altera o código existente — apenas cria uma nova classe concreta e a injeta no contexto.

### 3.2 Observer — reuso de notificação

O **Observer** implementa a notificação automática um-para-muitos. Ele é reutilizado sempre que múltiplos componentes precisam **reagir à mudança de estado** de outro:

- Mudou o status de um benefício → notifica o módulo de email, o de extrato e o de auditoria.
- Chegou um novo evento de integração → reagem os consumidores interessados.

O padrão Observer é reutilizado como *design* em bibliotecas de eventos, frameworks de mensageria e até no [[Padroes-de-Projeto-e-Arquitetura|padrão de mensageria]] que você estudou.

### 3.3 Singleton — reuso de instância única

O **Singleton** garante uma única instância e é reutilizado sempre que um **recurso global compartilhado** é necessário:

- Configuração global do sistema.
- Pool de conexões com o banco de dados.
- Cache compartilhado.

> [!warning] PEGADINHA — reuso não é cópia
> A banca pode tentar confundir: "reuso de software significa copiar e colar código de um projeto para outro". **Não necessariamente.** Reuso pode ser **aplicar um padrão**, **usar uma biblioteca**, **importar um framework** — nenhum dos quais envolve copiar e colar. O reuso de *design* é o mais valioso porque é **flexível e adaptável**.

---

## 4. Componentização e modularização

### 4.1 Modularização

**Modularização** é o processo de dividir um sistema em **módulos** — partes independentes que implementam funcionalidades específicas e se comunicam por **interfaces bem definidas**. Um módulo encapsula sua lógica interna e expõe apenas o que é necessário.

O princípio é simples: um módulo deve ter **responsabilidade única** e poder ser desenvolvido, testado e mantido **independentemente** dos demais.

> [!question] Por que modularizar?
> Se um sistema monolítico tem toda a lógica misturada, uma mudança na regra de cálculo de benefícios pode quebrar o módulo de relatórios. Com módulos bem definidos e interfaces claras, a mudança fica **isolada** — o módulo de cálculo é alterado sem afetar outros. É o **princípio da responsabilidade única** (S do SOLID) aplicado à arquitetura do sistema.

### 4.2 Componentização

A **componentização** é um passo além da modularização: ela leva a ideia de módulo para a **interface do usuário** e para **pedaços autocontidos** de software que encapsulam lógica, apresentação e estado.

No contexto de interfaces (web e mobile), um **componente** é uma unidade reutilizável de UI que pode ser combinada para construir telas complexas:

- **Web:** no Angular, React e Vue (que você verá na Fase 5), toda a interface é construída com **componentes**.
- **Mobile:** no Android, um **Fragment** (que você estudou no [[Desenvolvimento-Mobile|Bloco 4.1]]) é um componente reutilizável de tela.
- **Backend:** componentização também se aplica a **serviços** e **módulos de lógica de negócio** reutilizáveis.

> [!note] A relação com o SOLID
> A modularização e a componentização são a **materialização arquitetural** do **SOLID**: cada módulo/componente tem uma **responsabilidade única** (SRP), depende de **abstrações** em vez de implementações concretas (DIP), e pode ser **estendido** sem ser modificado (OCP).

---

## 5. Bibliotecas e frameworks como formas de reuso

### 5.1 Biblioteca (Library)

Uma **biblioteca** é um conjunto de código **reutilizável** que você **chama** (importa e usa) quando precisa. O controle do fluxo permanece com o seu código — a biblioteca é uma "ferramenta" que você invoca.

Exemplos:
- **Apache Commons** (Java): utilitários gerais (validação, coleções, IO).
- **JUnit** (Java): biblioteca de testes.
- **jQuery** (JavaScript): manipulação do DOM.

> A diferença-chave: **você chama a biblioteca** — o fluxo do programa é controlado pelo seu código.

### 5.2 Framework

Um **framework** é mais poderoso que uma biblioteca: ele fornece a **estrutura** da aplicação e **inverte o controle** — o framework chama o seu código, e não o contrário. É o conceito de **Inversão de Controle (IoC)**, que você já viu no [[Frameworks-Java|Spring]]: o container do Spring gerencia os seus beans, chama os seus controllers e executa os seus interceptadores — você apenas escreve o código que o framework orquestra.

| Característica | Biblioteca | Framework |
|---|---|---|
| **Controle de fluxo** | **seu código** chama a lib | **o framework** chama seu código |
| **Inversão de controle** | não há | sim (IoC) |
| **Estrutura** | você define | o framework define |
| **Exemplos** | JUnit, Apache Commons, jQuery | **Spring**, Angular, React, Django |
| **O que você faz** | importa e usa funções/classes | implementa pontos de extensão |

> [!warning] PEGADINHA — biblioteca vs. framework
> A armadilha clássica: "uma biblioteca inverte o controle" — **falso**. Na biblioteca, **você** chama a lib. No framework, **o framework** chama seu código. E o **Spring** é um framework (ele gerencia o ciclo de vida dos beans e chama seus controllers); o **JUnit** é uma biblioteca (você escreve os testes e o JUnit os executa — mas o controle do que testar é seu).

### 5.3 A cadeia de reuso na prática

Quando um time usa o **Spring Boot** para criar uma API, ele está reaproveitando:

1. **Framework** (Spring Boot) → estrutura, configuração, IoC;
2. **Bibliotecas** (Spring Data, Hibernate, Jackson) → funcionalidades reutilizáveis;
3. **Padrões de projeto** (MVC no Spring MVC, Repository no Spring Data, Strategy em interceptadores) → soluções consagradas;
4. **Componentes** (beans, serviços, repositórios) → módulos reutilizáveis dentro do projeto.

Tudo isso é **reuso em camadas** — do design ao código, passando por bibliotecas e frameworks.

---

## 6. Reuso e metodologia — a ponte com Scrum e XP

As metodologias ágeis estimulam o reuso de formas específicas:

- **XP:** a prática de *refatoração* melhora o código para que seja mais **reutilizável** e menos duplicado. *Design Simples* evita abstrações desnecessárias, mas não proíbe reuso quando ele é genuinamente útil.
- **Scrum:** a **Sprint Review** pode revelar que uma funcionalidade entregue em um sprint pode ser reaproveitada em outra parte do produto — o reuso é identificado e planejado incrementalmente.
- **Kanban:** o fluxo contínuo permite identificar padrões de trabalho repetitivo que podem ser transformados em **componentes reutilizáveis**.

---

## 7. Como a FGV cobra este tópico

- **Reuso de código vs. reuso de design:** a banca distingue copiar código de aplicar um padrão.
- **Biblioteca vs. framework:** quem chama quem? Biblioteca = seu código chama a lib; Framework = o framework chama seu código.
- **Componentização:** módulo = parte independente com interface bem definida; componente = unidade autocontida (geralmente de UI).
- **Frameworks como reuso:** o Spring é um framework (IoC, estrutura); o JUnit é uma biblioteca.

> [!warning] PEGADINHA — as distinções mais prováveis
> (1) **Biblioteca** = você chama · **Framework** = chama você (IoC). (2) **Reuso de código** = copiar trechos · **Reuso de design** = aplicar um padrão. (3) **Modularização** = divisão em módulos lógicos · **Componentização** = unidades autocontidas de UI/lógica. (4) O **Spring** é framework; o **JUnit** é biblioteca.

---

## 8. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **Reuso:** código (copiar trechos), design (aplicar padrão), componente (módulo reutilizável), framework (estrutura completa)
> - [ ] **Reuso de design ≠ reuso de código** — o design é mais valioso e flexível
> - [ ] **Modularização:** divisão em módulos com interfaces claras; responsabilidade única
> - [ ] **Componentização:** unidades autocontidas (UI e lógica); base dos frameworks modernos
> - [ ] **Biblioteca:** seu código chama a lib · **Framework:** o framework chama seu código (IoC)
> - [ ] O **Spring** é framework (IoC, estrutura); **JUnit** é biblioteca (você usa suas funções)
> - [ ] GoF (Strategy, Observer, Singleton, Factory) são **reuso de design** — soluções reutilizáveis para problemas recorrentes

> [!warning] O erro mais comum em prova
> Confundir **biblioteca com framework** (quem chama quem?) e confundir **reuso de código com reuso de design**. Na questão, pergunte: *estou copiando código (reuso de código) ou aplicando uma solução consagrada (reuso de design)?* e *meu código chama a ferramenta (biblioteca) ou a ferramenta chama meu código (framework)?*

---

## 9. Próximos passos

Você agora entende como as soluções são **reutilizadas** — de padrões de projeto a frameworks e componentes. No próximo tópico, vamos estudar como o código se **materializa** em diferentes contextos de desenvolvimento: **sistemas transacionais** (CRUD, integração), **analíticos** (relatórios, dashboards), **mobile** e **APIs** — os **tipos de codificação** que um analista de TI vai encontrar na DATAPREV.
