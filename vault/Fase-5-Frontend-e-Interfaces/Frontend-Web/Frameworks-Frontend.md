# Frameworks Frontend

> [!info] Metadados
> **Disciplina:** Tecnologias e Práticas Frontend Web
> **Bloco:** 5.1 — Tecnologias e Práticas Frontend Web (FASE 5 — Frontend e Interfaces)
> **Tópico:** 2. Frameworks Frontend
> **Subtópicos:** VueJS (componentes, reatividade, Vue Router, Vuex/Pinia) · Angular (componentes, diretivas, serviços, RxJS, Angular CLI) · React (componentes, hooks, JSX, React Router, Context API)
> **Pré-requisitos:** [[JavaScript]] (ES6+, assincronia, closures, prototypes) · [[Fundamentos-Web|Fundamentos Web]] (HTML, CSS, DOM, fetch/Ajax) · [[Metodologias-Ageis|Padrões de Desenvolvimento e Reuso]] (componentização e modularização)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-31

---

## 1. Por que estudar frameworks frontend?

No tópico anterior, você aprendeu os **fundamentos web**: HTML semântico para estruturar, CSS para estilizar, JavaScript para dar comportamento, e `fetch` para comunicar com o backend. Mas imagine uma aplicação real — o **Meu INSS**, por exemplo — com dezenas de telas, formulários complexos, atualizações dinâmicas de dados, navegação entre páginas sem recarregar, e estado do usuário que precisa ser mantido. Escrever tudo em JavaScript puro, manipulando o DOM diretamente com `document.getElementById()`, rapidamente se torna um pesadelo de manutenção.

É aqui que entram os **frameworks e bibliotecas frontend**. Eles resolvem problemas específicos que surgem em aplicações complexas:

- **Componentização:** dividir a interface em **peças reutilizáveis** (como cards, formulários, tabelas) que encapsulam HTML + CSS + JS em um único módulo;
- **Reatividade:** quando os dados mudam, a interface **atualiza automaticamente** — sem precisar manipular o DOM manualmente;
- **Gerenciamento de estado:** manter uma "fonte única da verdade" para os dados que circulam pela aplicação;
- **Roteamento:** navegar entre "páginas" sem recarregar o navegador (SPA — veremos no próximo tópico).

> [!question] Pergunta orientadora
> Se você já viu [[Frameworks-Java|Spring]] no backend, lembre-se: o Spring resolve a complexidade de um backend Java com injeção de dependência, convention over configuration, e componentização via beans. Os frameworks frontend fazem algo análogo para o frontend: organizam o código, reduzem repetição, e permitem que o desenvolvedor foque na **lógica da aplicação** em vez de na manipulação manual do DOM.

A ementa exige que você conheça os **três principais**: **Vue.js**, **Angular** e **React**. A prova **não cobra detalhes de API** de nenhum deles — cobra **diferenças conceituais**, **classificações**, e **características fundamentais**. Focaremos exatamente nisso.

---

## 2. Framework vs. Biblioteca — a distinção que a banca adora testar

Antes de mergulhar em cada tecnologia, é crucial entender a diferença entre **framework** e **biblioteca** — uma distinção que é alvo recorrente de questões.

| Conceito | Definição | Analogia |
|---|---|---|
| **Biblioteca** | Um conjunto de ferramentas que o programador **chama** quando precisa — ele mantém o controle do fluxo | Você contrata um encanador: liga quando precisa, manda ele embora quando termina |
| **Framework** | Uma estrutura que **chama o código do programador** — o framework mantém o controle do fluxo (Inversão de Controle) | A construtora constrói a casa e pede que você preencha as paredes — quem define o fluxo é a construtora |

No mundo backend, você já viu essa distinção: a [[Frameworks-Java|javax.servlet]] é uma biblioteca (você chama); o **Spring** é um framework (ele chama seu código via `@Controller`, `@Service` — Inversão de Controle/IoC).

No frontend:

- **Angular** é um **framework completo** — ele define a estrutura da aplicação, o ciclo de vida, o roteamento, e o programador preenche os componentes. Ele controla o fluxo.
- **Vue.js** é classificado como um **framework progressivo** — pode ser usado como biblioteca (só para reatividade) ou como framework completo (com roteamento e gerenciamento de estado). Mas quando se usa como framework, ele também controla o fluxo.
- **React** é uma **biblioteca** — ele fornece ferramentas para construir interfaces (componentes, JSX), mas não define sozinho a estrutura da aplicação. Você decide como organizar o roteamento, o estado, etc. (embora existam bibliotecas complementares como React Router).

> [!warning] PEGADINHA — React é BIBLIOTECA, não framework
> Essa é a pegadinha mais clássica do bloco. A banca pergunta: "React é um framework frontend?" — a resposta é **não, é uma biblioteca**. Angular e Vue são frameworks (ou framework progressivo). React é uma biblioteca. A razão: React define *como construir componentes de interface*, mas não define *como a aplicação como um todo se organiza* — isso depende de bibliotecas adicionais (React Router para rotas, Context API/Redux para estado). A banca troca as classificações propositadamente.

---

## 3. Vue.js — o framework progressivo

### 3.1 O que é o Vue

O **Vue.js** (ou simplesmente **Vue**) é um framework JavaScript **progressivo** — projetado para ser adotado incrementalmente. Você pode começar usando apenas a reatividade para uma parte de uma página e, gradualmente, escalar para uma aplicação completa com roteamento e gerenciamento de estado.

Sua filosofia é simplicidade: um template HTML familiar, JavaScript puro (sem TypeScript obrigatório), e reatividade baseada em **Proxy** ( Vue 3) — quando os dados mudam, a interface se atualiza automaticamente.

### 3.2 Componentes no Vue — Single-File Components

O Vue organiza a interface em **componentes** — e sua abordagem é o **Single-File Component (SFC)**: um único arquivo `.vue` que encapsula **template + lógica + estilos** de uma vez.

```html
<!-- BeneficiarioCard.vue -->
<template>
  <div class="card">
    <h3>{{ nome }}</h3>
    <p>CPF: {{ cpf }}</p>
    <span :class="status === 'ATIVO' ? 'badge-ativo' : 'badge-inativo'">
      {{ status }}
    </span>
  </div>
</template>

<script>
export default {
  props: ['nome', 'cpf', 'status']
}
</script>

<style scoped>
.card { border: 1px solid #ddd; padding: 16px; border-radius: 8px; }
.badge-ativo { color: green; font-weight: bold; }
.badge-inativo { color: red; }
</style>
```

> [!tip] Single-File Component do Vue
> O SFC do Vue é uma de suas características mais distintivas: tudo em um arquivo `.vue` — `<template>` para a estrutura HTML, `<script>` para a lógica JavaScript, e `<style>` para os estilos CSS. O `<style scoped>` garante que os estilos se apliquem **apenas** àquele componente, evitando conflitos. Essa organização é muito intuitive e é uma das razões da popularidade do Vue.

### 3.3 Reatividade

A **reatividade** é o conceito central: quando os dados do componente mudam (uma variável é atualizada), a interface se **atualiza automaticamente**. Não há necessidade de manipular o DOM manualmente com `document.getElementById()` — o Vue observa as mudanças e atualiza o que precisa.

No Vue 3, isso é implementado com **`ref()` e `reactive()`**:

```javascript
import { ref } from 'vue';

export default {
  setup() {
    const contador = ref(0);
    const incrementar = () => { contador.value++; };
    return { contador, incrementar };
  }
}
```

### 3.4 Vue Router e Vuex/Pinia

- **Vue Router:** gerencia a **navegação** entre "páginas" (componentes) sem recarregar o navegador — o equivalente ao Angular Router e ao React Router.
- **Vuex / Pinia:** gerencia o **estado global** da aplicação — o "banco de dados" do frontend. O Pinia é a versão moderna e recomendada (substituiu o Vuex no Vue 3).

---

## 4. Angular — o framework completo

### 4.1 O que é o Angular

O **Angular** é um framework **completo e opiniado** (batteries-included) desenvolvido e mantido pelo Google. Diferente do Vue e do React, o Angular exige **TypeScript** (uma superset de JavaScript com tipagem estática), e vem com praticamente tudo pronto: roteamento, formulários, HTTP client, testes, e injeção de dependência.

### 4.2 Componentes no Angular

O Angular também é baseado em **componentes**, mas sua organização é diferente: cada componente tem **quatro arquivos** separados (TypeScript, HTML, CSS, e spec de teste):

```
beneficiario-card/
├── beneficiario-card.component.ts      (lógica)
├── beneficiario-card.component.html    (template)
├── beneficiario-card.component.css     (estilos)
└── beneficiario-card.component.spec.ts (testes)
```

### 4.3 Diretivas

As **diretivas** são marcadores no template que adicionam comportamento. As mais usadas:

| Diretiva | Função | Exemplo |
|---|---|---|
| `*ngIf` | Renderiza condicionalmente | `<div *ngIf="usuario">Olá {{ usuario.nome }}</div>` |
| `*ngFor` | Itera sobre uma lista | `<li *ngFor="let b of beneficiarios">{{ b.nome }}</li>` |
| `[ngClass]` | Aplica classes condicionalmente | `[ngClass]="{'ativo': b.status === 'ATIVO'}"` |
| `[(ngModel)]` | Binding bidirecional de dados | `<input [(ngModel)]="nome">` |

### 4.4 Serviços e Injeção de Dependência

Aqui está uma das conexões mais diretas com o que você já estudou. No Angular, a lógica de negócio e o acesso a dados ficam em **serviços** — classes injetadas nos componentes via **Injeção de Dependência (DI)**. O mecanismo é conceitualmente idêntico ao que você viu no [[Frameworks-Java|Spring]]:

| Angular | Spring |
|---|---|
| `@Injectable()` | `@Service` / `@Component` |
| `@Component` | `@Controller` / `@RestController` |
| Injetor de dependência (DI Container) | Container IoC do Spring |
| `constructor(private servico: MeuServico)` | `@Autowired MeuServico servico;` |

A diferença é que o Angular usa **TypeScript** (com tipos), e o Spring usa **Java** — mas o **princípio** (Inversão de Controle, Injeção de Dependência) é o mesmo. Se você entendeu DI no Spring, entende DI no Angular.

> [!tip] Conexão com DI do Spring
> Quando você estudou [[Frameworks-Java|Injeção de Dependência no Spring]], aprendeu que o container cria os objetos e os injeta onde são necessários — sem que a classe precise `new`-ar suas dependências. O Angular faz **exatamente a mesma coisa** no frontend: o `Angular DI Container` cria instâncias de serviços e as injeta nos componentes via construtor. A prova pode testar essa conexão conceitual: "O mecanismo de Injeção de Dependência do Angular é análogo ao de qual framework Java?" → **Spring**.

### 4.5 RxJS e Observables

O **Angular** usa **RxJS** (Reactive Extensions for JavaScript) para lidar com operações assíncronas — chamadas HTTP, eventos, e fluxos de dados contínuos. O conceito central é o **Observable**: um padrão que emite valores ao longo do tempo (diferente de uma Promise, que resolve uma única vez).

```typescript
// Chamada HTTP no Angular retorna um Observable
this.http.get<Beneficiario[]>('/api/beneficiarios')
  .subscribe({
    next: (dados) => this.beneficiarios = dados,
    error: (erro) => console.error(erro)
  });
```

> [!note] RxJS: conceito neste bloco, não aprofundamento
> O RxJS é extenso e poderoso (operators como `map`, `filter`, `switchMap`, `mergeMap`). Neste bloco, basta saber que o Angular usa **Observables** (e não Promises) para operações assíncronas, e que o `.subscribe()` é o equivalente ao `.then()`. O aprofundamento em reatividade e operators não é cobrado nesta prova.

### 4.6 Angular CLI

O **Angular CLI** (`@angular/cli`) é a ferramenta de linha de comando para criar, desenvolver e buildar projetos Angular. Comandos típicos:

```
ng new meu-projeto        # cria um novo projeto
ng generate component X   # gera um componente
ng serve                  # inicia o servidor de desenvolvimento
ng build                  # gera o build de produção
```

---

## 5. React — a biblioteca de interface

### 5.1 O que é o React

O **React** é uma **biblioteca** (não framework) desenvolvida pelo Meta (Facebook) para construir interfaces de componentes. Sua filosofia é minimalista: ele foca em **como construir componentes de interface** e deixa escolhas de roteamento, estado global e outros aspectos para bibliotecas complementares.

### 5.2 JSX — JavaScript + XML

O React usa **JSX** — uma extensão de sintaxe que combina JavaScript com algo parecido com HTML dentro do código JS. O JSX é **compilado** para chamadas `React.createElement()`.

```jsx
// Isso é JSX — parece HTML, mas é JavaScript
function BeneficiarioCard({ nome, cpf, status }) {
  return (
    <div className="card">
      <h3>{nome}</h3>
      <p>CPF: {cpf}</p>
      <span className={status === 'ATIVO' ? 'ativo' : 'inativo'}>
        {status}
      </span>
    </div>
  );
}
```

> [!warning] PEGADINHA — JSX não é HTML
> O JSX **parece** HTML, mas é JavaScript. Por isso: usa `className` (não `class`), usa `htmlFor` (não `for`), e as expressões dentro de `{}` são JavaScript puro. A banca troca: "JSX é HTML dentro de JavaScript" — é uma simplificação excessiva; JSX é uma **extensão sintática do JavaScript** que se transforma em chamadas de função.

### 5.3 Componentes, Props e State

O React organiza a interface em **componentes** — funções (ou classes) que recebem dados (**props**) e retornam JSX (a representação visual).

- **Props (propriedades):** dados **passados de fora** para o componente — imutáveis (o componente não deve alterá-las). São como parâmetros de função.
- **State (estado):** dados **internos** do componente que podem **mudar** ao longo do tempo — quando mudam, o componente é **re-renderizado**.

```jsx
import { useState } from 'react';

function ContadorBeneficios() {
  const [total, setTotal] = useState(0); // state inicial: 0

  return (
    <div>
      <p>Total de benefícios: {total}</p>
      <button onClick={() => setTotal(total + 1)}>
        Adicionar
      </button>
    </div>
  );
}
```

### 5.4 Hooks — useState e useEffect

Os **Hooks** são funções especiais que "conectam" componentes funcionais a recursos do React (estado, efeitos colaterais, contexto). Os dois mais importantes:

| Hook | Função | Quando usar |
|---|---|---|
| `useState` | Gerencia **estado** local do componente | Contadores, campos de formulário, toggle |
| `useEffect` | Executa **efeitos colaterais** (chamadas HTTP, timers, subscriptions) | Buscar dados ao montar o componente, inscrever-se em eventos |

```jsx
import { useState, useEffect } from 'react';

function ListaBeneficiarios() {
  const [beneficiarios, setBeneficiarios] = useState([]);
  const [carregando, setCarregando] = useState(true);

  useEffect(() => {
    fetch('/api/beneficiarios')
      .then(resp => resp.json())
      .then(dados => {
        setBeneficiarios(dados);
        setCarregando(false);
      });
  }, []); // array vazio = executar apenas uma vez (mount)

  if (carregando) return <p>Carregando...</p>;

  return (
    <ul>
      {beneficiarios.map(b => (
        <li key={b.cpf}>{b.nome} — {b.status}</li>
      ))}
    </ul>
  );
}
```

> [!note] React Router e Context API
> Assim como o Vue Router e o Angular Router, o **React Router** gerencia a navegação entre "páginas" sem recarregar. O **Context API** é o mecanismo nativo do React para compartilhar estado entre componentes (uma alternativa leve ao Redux). Ambos são conceitos que o edital cobra como componentes do ecossistema React.

### 5.5 React Router e Context API

- **React Router:** biblioteca para roteamento — define "rotas" (URLs) que renderizam componentes diferentes.
- **Context API:** mecanismo nativo para **compartilhar dados** entre componentes sem precisar passar props manualmente em cada nível (evita o "prop drilling").

```jsx
// Context API — compartilhar tema entre componentes
import { createContext, useContext, useState } from 'react';

const TemaContext = createContext();

function App() {
  const [tema, setTema] = useState('claro');
  return (
    <TemaContext.Provider value={{ tema, setTema }}>
      <Pagina />
    </TemaContext.Provider>
  );
}

// Em qualquer componente descendente:
const { tema } = useContext(TemaContext);
```

---

## 6. Tabela comparativa — Vue vs. Angular vs. React

Essa tabela é o **coração da prova** — memorize as diferenças.

| Aspecto | Vue.js | Angular | React |
|---|---|---|---|
| **Tipo** | Framework progressivo | Framework completo | **Biblioteca** |
| **Criador** | Evan You (comunidade) | Google | Meta (Facebook) |
| **Linguagem** | JavaScript/TypeScript (opcional) | **TypeScript obrigatório** | JavaScript/TypeScript (JSX) |
| **Template** | HTML com diretivas (`v-if`, `v-for`) | HTML com diretivas (`*ngIf`, `*ngFor`) | **JSX** (JavaScript + HTML-like) |
| **Reatividade** | Proxy (Vue 3) / Object.defineProperty (Vue 2) | Zone.js + Change Detection | State + re-render |
| **Estado global** | **Pinia** (ou Vuex) | Services + RxJS | **Context API** (ou Redux) |
| **Roteamento** | Vue Router | Angular Router | React Router |
| **DI (Injeção de Dep.)** | Não nativa (provide/inject simples) | **Sistema de DI completo** | Não nativa (Context) |
| **Curva de aprendizado** | Baixa | **Alta** | Média |
| **Filosofia** | Progressivo, incremental | Opiniado, completo | Minimalista, flexível |

### 6.1 O que a FGV mais cobra na tabela

> [!tip] As três distinções que mais caem em prova
> **(1) Classificação:** React = biblioteca; Angular = framework completo; Vue = framework progressivo. (2) **Linguagem:** Angular exige TypeScript; os outros aceitam JS puro. (3) **Template:** React usa JSX; Angular e Vue usam templates HTML com diretivas. Guarde essas três e você elimina metade das questões.

### 6.2 Virtual DOM

Uma característica compartilhada por **React e Vue** (mas não originalmente pelo Angular antigo) é o **Virtual DOM**: uma representação leve da árvore DOM em memória. Quando os dados mudam, o framework cria uma nova árvore virtual, **compara** com a anterior (diffing), e atualiza no DOM real **apenas as partes que mudaram** — em vez de re-renderizar a página inteira.

> [!warning] PEGADINHA — Virtual DOM não é exclusivo de um framework
> A banca pode afirmar: "O Virtual DOM é uma característica exclusiva do React" — **falso**. O Vue também usa Virtual DOM (desde sua primeira versão). O Angular, por sua vez, usa **Change Detection** com Zone.js (abordagem diferente). Virtual DOM é uma **técnica**, não propriedade de um framework.

---

## 7. Conexões com a ementa e com blocos anteriores

### 7.1 Componentização e reuso

Quando você estudou [[Metodologias-Ageis|Padrões de Desenvolvimento e Reuso]] no Bloco 4.2, aprendeu que a **componentização** é uma das formas mais eficazes de reutilizar código. Os frameworks frontend levam esse princípio ao extremo: cada componente é uma **unidade independente** que encapsula estrutura (HTML), apresentação (CSS) e comportamento (JS). Isso é a materialização frontend dos princípios de **baixo acoplamento** e **alta coesão** que você viu no [[Paradigma-Orientado-a-Objetos|POO]].

### 7.2 Injeção de dependência

O Angular tem um sistema de DI que é **conceitualmente idêntico** ao do [[Frameworks-Java|Spring]]. Se a banca perguntar "qual framework frontend possui Injeção de Dependência nativa análoga ao Spring?", a resposta é **Angular**. O React usa Context API (que não é DI); o Vue usa provide/inject (uma versão simples).

### 7.3 Componentes e testes

O [[Testes-Automatizados|Selenium]] que você estudou testa a **interface web final** (caixa-preta). Os frameworks frontend complementam com testes de **componentes** unitários — o Angular CLI gera arquivos `.spec.ts` para testes com Jasmine/Karma; o React usa Jest + React Testing Library; o Vue usa Vitest ou Jest.

---

## 8. Como a FGV cobra este tópico

- **Classificação:** React é biblioteca (não framework); Angular é framework completo; Vue é framework progressivo.
- **Angular = TypeScript:** é o único que exige TypeScript. Se a questão diz "framework frontend que utiliza tipagem estática obrigatória" → Angular.
- **JSX:** React usa JSX (não templates HTML). Vue e Angular usam templates com diretivas.
- **Injeção de Dependência:** Angular tem DI nativa (análoga ao Spring). React e Vue não têm DI no mesmo sentido.
- **Virtual DOM:** técnica compartilhada por React e Vue (não exclusiva de nenhum). Angular usa Change Detection.
- **Ecosistemas:** Vue Router / Pinia (Vue) · Angular Router / Services / RxJS (Angular) · React Router / Context API (React).

> [!warning] PEGADINHA — as quatro armadilhas mais rentáveis
> (1) **React é biblioteca**, não framework. (2) **Angular exige TypeScript** — os outros não. (3) **JSX é sintaxe do React**, não HTML. (4) **DI nativa é só do Angular** — React usa Context (não é DI); Vue usa provide/inject (simples). Decore essas quatro distinções e você resolve qualquer questão conceitual deste bloco.

---

## 9. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **Biblioteca vs. Framework:** biblioteca = programador controla; framework = controla (IoC)
> - [ ] **React = biblioteca** · Angular = framework completo · Vue = framework progressivo
> - [ ] **Angular:** TypeScript obrigatório, DI nativa, RxJS/Observables, templates com `*ngIf`/`*ngFor`
> - [ ] **Vue:** SFC (`.vue`), reatividade via `ref()`/`reactive()`, progressivo, template HTML
> - [ ] **React:** JSX, componentes via funções, hooks (`useState`/`useEffect`), React Router, Context API
> - [ ] **Virtual DOM:** React e Vue usam; Angular usa Change Detection
> - [ ] **Angular DI ≈ Spring DI:** `@Injectable()` ↔ `@Service`; construtor ↔ `@Autowired`
> - [ ] **A banca foca diferenças conceituais**, não detalhes de API
> - [ ] **Estado global:** Pinia (Vue) · Services/RxJS (Angular) · Context API/Redux (React)

> [!warning] O erro mais comum em prova
> Classificar o React como framework (é biblioteca) e esquecer que o Angular é o único que exige TypeScript e possui Injeção de Dependência nativa. Na questão, pergunte: *é biblioteca (React) ou framework (Angular/Vue)? · usa TypeScript obrigatoriamente (Angular)? · tem DI nativa (Angular)? · usa JSX (React) ou template HTML (Vue/Angular)?*

---

## 10. Próximos passos

Você agora conhece os três principais frameworks/bibliotecas frontend: Vue.js, Angular e React — suas classificações, diferenças conceituais, e componentes fundamentais. Essa visão comparativa é o que a FGV mais cobra neste bloco.

O próximo tópico fecha a Fase 5 ao explorar as **arquiteturas de apresentação**: como as aplicações frontend se estruturam e se entregam ao usuário — **SPA** (Single Page Application), **PWA** (Progressive Web App), e a distinção entre **SSR** e **CSR**. Esses conceitos são a "camada de arquitetura" dos frameworks que você acabou de conhecer — eles explicam como o Angular, Vue e React organizam suas aplicações no mundo real.
