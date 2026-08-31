# Desenvolvimento Mobile

> [!info] Metadados
> **Disciplina:** Desenvolvimento de Sistemas
> **Bloco:** 4.1 — Desenvolvimento de Sistemas (FASE 4 — Núcleo de Desenvolvimento)
> **Tópico:** 7. Desenvolvimento Mobile
> **Subtópicos:** Android (Activity, Fragment, Intent, RecyclerView, lifecycle) · iOS (UIKit, SwiftUI conceito, ciclo de vida) · Low-code e no-code (conceitos, plataformas, quando usar)
> **Pré-requisitos:** [[Paradigma-Orientado-a-Objetos|POO]] (objetos, ciclo de vida, estados) e [[Java-e-Ecossistema-JVM|Java]] (linguagem do Android nativo) e [[JavaScript|JavaScript]] (base para tecnologias híbridas/React Native)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-31

---

## 1. Por que estudar desenvolvimento mobile?

Ao lado do web, o **desenvolvimento mobile** é um dos principais vetores de entrega de software — e, para o DATAPREV e o setor público como um todo, os aplicativos (como o **Meu INSS**, aplicativo usado por milhões de brasileiros para consultar benefícios) são canais essenciais de serviço ao cidadão. Um analista de TI precisa entender o ciclo de vida, os componentes e as alternativas (nativo, híbrido, low-code) dos apps móveis.

Este tópico conecta:

- A [[Paradigma-Orientado-a-Objetos|nota de POO]]: as **Activities** e **Fragments** do Android são **objetos com ciclo de vida e estado** — exatamente a noção de *estado* e *comportamento* que você estudou. O ciclo de vida de uma Activity é um caso real de **estados transitando** sob controle do sistema.
- A [[Java-e-Ecossistema-JVM|nota de Java]] e a [[JavaScript|de JavaScript]]: o Android nativo é escrito **em Java/Kotlin**; e as soluções **híbridas** (como React Native) usam **JavaScript**. Você já domina as duas linguagens.

> [!question] Pergunta orientadora
> Quando você gira a tela do celular, o aplicativo Android "reinicia" — e isso é um comportamento *esperado*, não um bug. Por quê? Porque a plataforma controla o **ciclo de vida** das telas. Entender esse ciclo de vida (onCreate → ... → onDestroy) é entender como o sistema gerencia o estado de cada tela — o coração do Android. Vamos começar por aí.

---

## 2. Android — o ecossistema

### 2.1 Activity e o ciclo de vida

Uma **Activity** é um **componente de tela** do Android — cada tela do app é (geralmente) uma Activity. Ela representa **uma única interface com o usuário** e possui um **ciclo de vida** gerenciado pelo sistema. Os principais **métodos de callback** do ciclo de vida, em ordem:

```
onCreate()  → onStart()  → onResume()  → [app em execução/ativo]
              (repõe)                    (em primeiro plano)
onPause()   → onStop()   → onDestroy()
(outro ganha foco)  (não visível)  (destruição)
```

| Método | Quando é chamado | O que fazer |
|---|---|---|
| **`onCreate()`** | criação da Activity | inicializar recursos, inflar a interface |
| **`onStart()`** | Activity fica *visível* | preparar a interface para aparecer |
| **`onResume()`** | Activity fica *em primeiro plano* (adora interação) | retomar tarefas pausadas |
| **`onPause()`** | outra Activity ganha **foco** parcial (ex.: diálogo) | pausar tarefas leves, salvar estado |
| **`onStop()`** | Activity **não é mais visível** | liberar recursos mais pesados |
| **`onDestroy()`** | Activity é **destruída** | liberar recursos e referências |

> [!important] O estado "ativo" e "em loop"
> Quando a Activity está **em primeiro plano e recebe interação**, o ciclo vive entre `onResume()` e `onPause()`. Ao girar a tela, o sistema **destrói e recria** a Activity (`onPause` → `onStop` → `onDestroy` → `onCreate` → ...) — por isso o estado precisa ser **salvo** (ex.: em `onSaveInstanceState`) antes da destruição e **restaurado** no novo `onCreate`.

> [!warning] PEGADINHA — a ordem do ciclo de vida
> A ordem canônica é **onCreate → onStart → onResume → onPause → onStop → onDestroy**. Alternativas de prova costumam misturar (ex.: `onResume` antes de `onStart`, ou `onPause` depois de `onStop`). Memorize a sequência e o que cada fase significa (criada → visível → em primeiro plano → pausada → não visível → destruída). Outra pegadinha: **`onCreate` é o primeiro** e **`onDestroy` o último** da vida útil.

### 2.2 Activity vs. Fragment

Um **Fragment** é um **componente de interface reutilizável** que vive **dentro de uma Activity** — representa uma parte da tela, com seu próprio ciclo de vida (dependente do da Activity).

- **Activity:** a tela/cenário principal; um Fragment **pertence** a uma Activity.
- **Fragment:** um bloco reutilizável de UI que pode ser **adicionado, removido ou trocado** dentro de uma Activity — permitindo, por exemplo, layouts diferentes para celular e tablet.

```text
Activity (tela)
├── Fragment A  (parte da interface — ex.: lista)
└── Fragment B  (outra parte — ex.: detalhes)
```

> [!warning] PEGADINHA — Fragment não existe sem Activity
> O **Fragment sempre vive dentro de uma Activity** — não pode existir sozinho. A diferença essencial: a **Activity é a tela**; o **Fragment é uma parte reutilizável dentro dela** (o que viabiliza interfaces flexíveis, como dois painéis no tablet). Uma alternativa que diga "o Fragment é independente da Activity" está errada.

### 2.3 Intent — a "mensagem" entre componentes

Uma **Intent** é um **objeto de mensagem assíncrona** que descreve uma **operação a ser realizada** — usada para **navegar entre Activities/Fragments**, **iniciar serviços** e **comunicar componentes**. Há dois tipos principais:

- **Intent explícita:** nomeia **exatamente** o componente (a classe) que irá tratar a ação — usada para navegar **dentro do próprio app**.
- **Intent implícita:** descreve a **ação** (ex.: abrir uma URL, tirar foto, ligar) sem especificar o componente — o **sistema** decide qual app/componente atende (ex.: abrir no navegador padrão).

```java
// Intent explícita: aponta diretamente para a Activity de destino
Intent i = new Intent(this, DetalheActivity.class);
i.putExtra("cpf", "123");              // envia dado junto
startActivity(i);

// Intent implícita: só descreve a ação; o sistema escolhe o app
Intent abrirUrl = new Intent(Intent.ACTION_VIEW, Uri.parse("https://www.gov.br"));
startActivity(abrirUrl);
```

> [!important] Explícita vs. implícita
> **Intent explícita** = especifica a classe destino (navegação no próprio app). **Intent implícita** = descreve a *ação* e deixa o **sistema** resolver qual componente (ex.: "abra esta URL"). A pegadinha: implicitamente o Android "pergunta ao sistema" quem pode tratar; a explícita "já sabe" quem tratar.

### 2.4 RecyclerView

O **RecyclerView** é o **componente de lista** moderno do Android — usado para exibir **conjuntos de dados de forma eficiente**. Ele "recicla" (daí o nome) as *views* de itens que saem da tela para reutilizá-las, em vez de criar uma view nova para cada item — o que economiza memória em listas longas.

- **Adapter:** conecta os **dados** ao RecyclerView e cria as views dos itens.
- **LayoutManager:** define como os itens ficam dispostos (lista, grade).
- **ViewHolder:** armazena as referências das views de um item para reuso.

> [!note] Onde cai o RecyclerView
> O **RecyclerView** é o substituto moderno do antigo `ListView`, com ênfase em **eficiência/reciclagem** de views e em **flexibilidade** (listas e grades). A banca cobra o **conceito**: ele recicla views para listas grandes com bom desempenho; o **Adapter** é o elo entre o modelo (dados) e a apresentação.

---

## 3. iOS — UIKit e SwiftUI

### 3.1 UIKit

**UIKit** é o **framework de interface** tradicional do iOS para o desenvolvimento **nativo** (em **Swift** ou Objective-C). Ele fornece os **componentes visuais** (botões, tabelas, telas) e o ciclo de vida de **views e view controllers**.

### 3.2 O ciclo de vida do iOS

No iOS, o equivalente à Activity do Android é o **UIViewController**, que também tem um ciclo de vida de *view* (chamadas de callback):

```
viewDidLoad()  → viewWillAppear()  → viewDidAppear()  → [tela visível]
                                               ↓ atualizações
viewWillDisappear()  → viewDidDisappear()  → (destruição)
```

| Método (iOS) | Quando ocorre |
|---|---|
| `viewDidLoad()` | a view foi carregada na memória (equivalente ao `onCreate` do Android) |
| `viewWillAppear()` | a view está prestes a aparecer |
| `viewDidAppear()` | a view já apareceu |
| `viewWillDisappear()` | a view está prestes a sair da tela |
| `viewDidDisappear()` | a view já saiu da tela |

### 3.3 SwiftUI (conceito)

**SwiftUI** é o **framework declarativo moderno** da Apple (introduzido no iOS 13) para construir interfaces. A diferença-chave: no **UIKit** a interface é **imperativa** (você cria e controla as views passo a passo); no **SwiftUI** a interface é **declarativa** (você *descreve* como a interface deve ficar e o framework a renderiza), com **binding** automático de dados — a mesma ideia de *declarativa + realização automática* que inspira frameworks como React.

> [!warning] PEGADINHA — UIKit (imperativo) vs. SwiftUI (declarativo)
> O **UIKit** é **imperativo**: você instrui o sistema, passo a passo, como construir e atualizar a interface. O **SwiftUI** é **declarativo**: você *descreve o estado desejado* da interface, e o framework cuida de renderizá-la e atualizá-la. SwiftUI é a abordagem mais moderna; UIKit é o framework consolidado. A pegadinha inverte os termos: "SwiftUI é imperativo" ou "UIKit é declarativo" — ambos falsos.

> [!note] O edital pede SwiftUI como "conceito"
> A ementa pede SwiftUI **conceitualmente**. Guarde: é o framework de UI **declarativo** e moderno do iOS, que descreve a interface e sincroniza dados automaticamente, em contraste ao **UIKit imperativo**. O **ciclo de vida** do iOS é centrado no **UIViewController** (`viewDidLoad`, `viewWillAppear`, etc.).

---

## 4. Low-code e no-code

### 4.1 O que são

Ambos permitem construir aplicações com **menos escrita de código manual**, usando **interfaces visuais** (arrastar e soltar componentes, conectar dados). A distinção essencial:

- **Low-code:** ainda **envolve escrita de código**, mas em quantidade **reduzida** — para personalização, regras e integrações complexas. A plataforma fornece os componentes prontos; o desenvolvedor complementa com código quando necessário.
- **No-code:** **praticamente não escreve código** — a aplicação é construída **inteiramente com a ferramenta visual** (arrastar e soltar, configuração). Voltado a **não programadores**.

| | Low-code | No-code |
|---|---|---|
| Escrita de código | **pouca** (ainda há) | **nenhuma/ mínima** |
| Público-alvo | desenvolvedores que aceleram | **não programadores** |
| Complexidade permitida | maior (personalização) | menor (fluxos padrão) |
| Exemplos | OutSystems, Mendix, Power Apps | Bubble, Airtable (paradigma) |

> [!question] O que determina a escolha entre low-code e no-code?
> Se a aplicação precisa de **regras de negócio complexas, integrações profundas ou muito controle**, o **low-code** (com código sob demanda) é mais adequado. Se é um fluxo simples, interno, que um **analista de negócio** (não programador) precisa montar rápido, o **no-code** basta. A decisão depende da **complexidade** e de **quem** vai construir/manter.

### 4.2 Quando usar (e quando não usar)

Considerações-chave:

- **Quando usar:** prototipagem rápida, apps internos simples, formulários, dashboards, automação de fluxos de negócio; acelerar a entrega com time reduzido.
- **Cuidados/limitações:** menor controle sobre o código, possível **dependência da plataforma** (vendor lock-in), governança de dados e **segurança** (dados previdenciários sensíveis exigem controle rigoroso), e **dificuldade de escalar** soluções muito complexas.

> [!warning] PEGADINHA — low-code ≠ ausência de desenvolvedores
> O **low-code reduz** o código manual, mas **não elimina** o papel do programador — ele complementa quando necessário; o **no-code** é que se aproxima de "sem código", voltado a não programadores. Uma alternativa que diga "no low-code não há nenhum código" ou "no no-code ainda existe muito código" troca os conceitos. E ambos **não eliminam** a necessidade de cuidado com dados sensíveis — sob a [[LGPD-Lei-Geral-de-Protecao-de-Dados|LGPD]], a proteção vale nas plataformas low-code/no-code também.

### 4.3 A ponte com o edital

O edital pede low-code/no-code **conceitualmente** — é preciso entender **o que são**, **as diferenças** e **quando aplicar**, não dominar plataformas específicas. Para o contexto DATAPREV, surgem como alternativa **rápida** para determinadas necessidades internas (formulários, workflow), respeitando as exigências de segurança e dados.

---

## 5. Como a FGV cobra este tópico

- **Ciclo de vida Android:** a ordem `onCreate → onStart → onResume → onPause → onStop → onDestroy` e o que ocorre em cada fase (criada → visível → em primeiro plano → pausada → não visível → destruída).
- **Activity vs. Fragment:** a Activity é a tela; o Fragment é uma parte reutilizável dentro dela (não existe sem Activity).
- **Intent:** explícita (nomeia a classe destino) vs. implícita (descreve a ação, o sistema resolve).
- **RecyclerView:** reciclagem de views para listas eficientes; Adapter liga dados à lista.
- **iOS:** UIKit (imperativo/consolidado) vs. SwiftUI (declarativo/moderno); ciclo de vida do `UIViewController`.
- **Low-code vs. no-code:** low envolve pouca escrita de código (ainda há); no não escreve (para não programadores); a escolha depende de complexidade e público.

> [!warning] PEGADINHA — as distinções mais prováveis
> (1) **onCreate é o primeiro; onDestroy o último** — e a ordem correta das fases. (2) **Fragment sempre vive numa Activity**. (3) **Intent explícita** (classe definida) vs. **implícita** (ação, sistema resolve). (4) **UIKit imperativo vs. SwiftUI declarativo**. (5) **low-code** (pouco código) vs. **no-code** (sem código p/ não programadores).

---

## 6. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **Activity:** componente de tela com ciclo de vida gerenciado pelo sistema
> - [ ] **Ciclo de vida Android:** onCreate → onStart → onResume → onPause → onStop → onDestroy
> - [ ] **Fragment:** parte reutilizável de UI dentro de uma Activity (depende dela)
> - [ ] **Intent explícita** (classe destino) vs. **implícita** (ação; sistema resolve)
> - [ ] **RecyclerView:** lista eficiente; recicla views; Adapter liga dados à UI
> - [ ] **iOS UIKit:** framework **imperativo** e consolidado; ciclo de vida do `UIViewController` (viewDidLoad etc.)
> - [ ] **iOS SwiftUI:** framework **declarativo** moderno; descreve a interface, sincroniza dados
> - [ ] **Low-code:** pouca escrita de código (ainda há); **No-code:** sem código, para não programadores
> - [ ] Quando usar low/no-code: prototipagem rápida e apps simples; cuidado com dados sensíveis (LGPD)

> [!warning] O erro mais comum em prova
> Trocar a **ordem do ciclo de vida Android** e confundir **UIKit (imperativo) com SwiftUI (declarativo)**. E inverter **low-code (pouco código) com no-code (sem código)**. Na questão, pergunte: *qual fase vem antes de qual?* e *imperativo (instrui passo a passo) ou declarativo (descreve o estado)?*

---

## 7. Próximos passos

Você entendeu como o POO, o Java e o JavaScript se materializam no **mobile**: as Activities e Fragments (Android), o UIKit e o SwiftUI (iOS), além do panorama de **low-code/no-code**. Isso completa a visão dos "dois mundos principais" de entrega de software — web e mobile — que um analista de TI precisa conhecer.

A última nota do **Núcleo de Desenvolvimento** é o **DevOps e Controle de Versão**: como o código que você produz (em Java, JavaScript, mobile) é **versionado** (Git), **construído e entregue continuamente** (CI/CD), **empacotado em containers** (Docker) e **disponibilizado em ambientes** (internet, intranet, portal). Ou seja: fechamos o ciclo do desenvolvimento com a **entrega** — o ponto em que o código vira produto.
