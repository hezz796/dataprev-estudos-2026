# JavaScript

> [!info] Metadados
> **Disciplina:** Desenvolvimento de Sistemas
> **Bloco:** 4.1 — Desenvolvimento de Sistemas (FASE 4 — Núcleo de Desenvolvimento)
> **Tópico:** 3. JavaScript
> **Subtópicos:** Sintaxe básica e tipos · Funções, closures, escopo · Prototype e cadeia de protótipos · Async/Await, Promises · ES6+ (let/const, arrow functions, destructuring, spread/rest)
> **Pré-requisitos:** [[Raciocinio-Matematico-Aplicado|Raciocínio Lógico Matemático]] (lógica de programação, condicionais) e [[Compreensao-e-Interpretacao-de-Textos|Língua Portuguesa]] (leitura de código e documentação técnica)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-31

---

## 1. Por que estudar JavaScript?

O JavaScript nasceu no navegador, mas hoje é muito mais: é uma das linguagens mais difundidas do mundo, roda no servidor (Node.js), no aplicativo (React Native), e é a base de todo o **frontend web** — que será detalhado na fase posterior do edital. Por isso, a ementa o coloca aqui, no **Núcleo de Desenvolvimento**, como uma das três linguagens principais do cargo (com Java e o JavaScript do frontend).

A FGV cobrará JavaScript com um viés **conceitual e de comportamento**: escopo, closures, protótipos, assincronia — os pontos em que o JavaScript mais se diferencia de outras linguagens e onde estão as pegadinhas. É bem menos sobre "escrever um CRUD em JS" e bem mais sobre **entender como a linguagem se comporta**, porque é isso que separa quem sabe programar de quem apenas copia código.

> [!question] Pergunta orientadora
> Numa linguagem tradicional como Java, os tipos são fixos e o escopo é "previsível". No JavaScript, porém, coisas surpreendentes acontecem: uma variável declarada com `var` dentro de um `if` "vaza" para fora; um `console.log` antes da declaração não dá erro; e chamadas assíncronas não esperam na ordem em que foram escritas. Por que o JavaScript se comporta assim? Entender *por quê* é o coração deste tópico.

---

## 2. Tipagem dinâmica e tipos básicos

### 2.1 A tipagem dinâmica

O JavaScript é **dinamicamente tipado**: uma variável pode mudar de tipo ao longo da execução, e o tipo é determinado em **tempo de execução**, não em tempo de compilação.

```javascript
let valor = "Recife";   // string
valor = 10;             // agora é número — sem erro
valor = true;           // agora é boolean
```

Isso difere frontalmente do Java ([[Java-e-Ecossistema-JVM|estaticamente tipado]]), onde o tipo é fixo em compilação. A pegadinha da banca: a declaração "JavaScript é uma linguagem **estaticamente tipada**" é **falsa**; é **dinamicamente tipada**.

### 2.2 Tipos primitivos e tipos de referência

O JavaScript tem **7 tipos primitivos** (`string`, `number`, `boolean`, `null`, `undefined`, `symbol`, `bigint`) e **objetos** como tipo de referência. Dois pontos de prova:

- **`number`:** cobre tanto inteiros quanto decimais (não há `int` vs. `double` como no Java). O `NaN` (Not a Number) é o resultado de operações inválidas (ex.: `10 / "abc"` → `NaN`).
- **`null` vs. `undefined`:** a distinção favorita da banca:
  - **`undefined`:** a variável foi declarada, mas **nunca recebeu valor** (não inicializada), ou o acesso a propriedade inexistente.
  - **`null`:** um **valor explícito** que representa "vazio/nada" **atribuído** pelo programador.

```javascript
let a;                    // a === undefined (declarada sem valor)
let b = null;             // b é null (valor explícito de "nada")
typeof a;   // "undefined"
typeof b;   // "object"  (curiosidade: typeof null retorna "object"!)
```

> [!warning] PEGADINHA — `typeof null` retorna "object"
> Apesar de `null` ser um tipo **primitivo**, `typeof null` retorna `"object"` — um erro histórico mantido no JavaScript por compatibilidade. A banca cobra isso para ver se você sabe diferenciar "tipo primitivo" de "retorno do `typeof`". Lembre: `null` é primitivo, mas o `typeof` diz `"object"`.

---

## 3. Escopo: global, função e bloco

**Escopo** é a região do código onde uma variável é acessível. Entender o escopo em JavaScript exige conhecer os três níveis e como cada palavra-chave (`var`, `let`, `const`) se comporta.

| Palavra-chave | Escopo | Hoisting | Pode reassignar? | Recomendada? |
|---|---|---|---|---|
| `var` | **função** (function scope) | sim (inicializa como `undefined`) | sim | não (legada) |
| `let` | **bloco** (block scope) | sim (mas fica em *temporal dead zone*) | sim | sim |
| `const` | **bloco** | sim (mas TDZ) | **não** | sim (preferida) |

> [!question] Por que `var` não é mais recomendado?
> Porque `var` ignora o **escopo de bloco**: uma variável declarada com `var` dentro de um `if` ou `for` "vaza" para fora do bloco (mas fica presa na função). Isso gera bugs difíceis de prever. O `let` e o `const` respeitam o **escopo de bloco** — são as escolhas modernas (ES6+).

### 3.1 Hoisting (elevação)

**Hoisting** é o comportamento em que as **declarações** são "elevadas" para o topo do escopo em tempo de interpretação. Para `var`, a **declaração** é elevada e inicializada com `undefined`; para `let`/`const`, a declaração é elevada, mas fica em **Temporal Dead Zone (TDZ)** — usar antes da declaração gera erro.

```javascript
console.log(x);   // undefined (var é elevado e inicializado como undefined)
var x = 10;

console.log(y);   // ReferenceError (let está em TDZ até a linha da declaração)
let y = 20;
```

> [!warning] PEGADINHA — hoisting do `var` vs. TDZ do `let`
> `var` elevado = `undefined` (não erro). `let`/`const` elevados, porém **não inicializados** = acionam **Temporal Dead Zone** → `ReferenceError` ao acessar antes da declaração. A distinção entre "undefined" (var) e "ReferenceError" (let/const na TDZ) é uma das pegadinhas mais clássicas do JS.

### 3.2 var vs. let vs. const — o resumo decisivo

Como funciona na prática:

```javascript
function exemplo() {
    var a = 1;        // function-scoped
    let b = 2;        // block-scoped
    const c = 3;      // block-scoped, não pode reassignar

    if (true) {
        var a = 10;   // reutiliza a MESMA variável a (vaza do if)
        let b = 20;   // nova variável b dentro do bloco (sombreia a de fora)
        // c não pode receber novo valor
    }
    console.log(a);   // 10 (var vazou do if)
    console.log(b);   // 2 (let de fora preservada)
}
```

> [!warning] PEGADINHA — `const` não é "constante em valor", é "constante em referência"
> Para **objetos e arrays**, `const` proíbe **reassociar a variável** a outro objeto, mas **permite modificar o conteúdo** do objeto/array. `const arr = [1, 2, 3]; arr = [4];` dá erro (reassociação), mas `arr.push(4);` funciona (modifica o conteúdo). A banca cobra: `const` impede a *reatribuição*, não a *mutação*.

---

## 4. Funções, closures e arrow functions

### 4.1 Funções: de primeira classe

Em JavaScript, **funções são valores de primeira classe**: podem ser atribuídas a variáveis, passadas como argumento e retornadas por outras funções. Isso é a base das `closures` e do padrão *callback*.

```javascript
// Declaração de função (function declaration) — é elevada
function somar(a, b) { return a + b; }

// Função anônima atribuída a uma variável (function expression)
const subtrair = function(a, b) { return a - b; };

// Passando função como argumento (callback)
function aplicar(fn, a, b) { return fn(a, b); }
aplicar(somar, 3, 4);   // 7
```

### 4.2 Escopo léxico e closures

Uma **closure** é uma função que **"lembra" o ambiente (escopo) onde foi criada**, mesmo depois de esse escopo ter terminado. Em outras palavras, a função interna guarda acesso à variável/escopo da função externa.

```javascript
function criarContador() {
    let contador = 0;              // variável do escopo externo
    return function() {            // closure: lembra do 'contador'
        contador++;
        return contador;
    };
}

const incrementar = criarContador();
incrementar();   // 1
incrementar();   // 2
incrementar();   // 3
// A variável 'contador' continua "viva" dentro da closure,
// mesmo após criarContador() ter terminado.
```

> [!important] A essência da closure
> A **closure** mantém viva a **referência ao escopo onde a função foi definida**, mesmo após esse escopo de criação ter retornado. É isso que permite *estado privado* e *encapsulamento* em JavaScript (uma noção que ecoa o **encapsulamento** do [[Paradigma-Orientado-a-Objetos|POO]]). Sem closure, cada chamada de `incrementar` usaria um estado zerado.

### 4.3 Arrow functions (ES6)

As **arrow functions** (`=>`) são uma sintaxe concisa de função. Diferenças-chave vs. funções tradicionais:

- **`this` léxico:** arrow functions **não têm seu próprio `this`** — herdam o `this` do escopo onde foram definidas. Funções tradicionais têm `this` dinâmico (quem chamou).
- **Não têm `arguments`** próprio (nem podem ser usadas como construtora com `new`).

```javascript
// Sintaxe concisa
const dobrar = (x) => x * 2;
const saudar = nome => `Olá, ${nome}`;    // parênteses opcionais com 1 parâmetro

// this léxico: a arrow herda o this de fora
function Timer() {
    this.valor = 0;
    setInterval(() => { this.valor++; }, 1000);   // arrow: this = Timer
}
```

> [!warning] PEGADINHA — `this` na arrow function
> A **arrow function não tem `this` próprio**; ela usa o `this` do escopo externo (é um `this` **léxico**). Já a função tradicional tem `this` **dinâmico** (depende de quem a invocou, por exemplo, o elemento num evento). A banca cobra essa diferença: numa função de callback tradicional num objeto, o `this` pode não ser o objeto esperado; com arrow, o `this` é o do escopo que a criou.

---

## 5. Prototype e a cadeia de protótipos

O JavaScript **não é class-based clássico** — ele é baseado em **protótipos**. Diferentemente do Java, onde a herança é por **classes** (`extends`), no JS a herança acontece por **cadeia de protótipos**: cada **objeto** tem um **protótipo** (outro objeto) e, ao buscar uma propriedade, o motor percorre a cadeia até encontrá-la.

```javascript
// Um objeto "pai"
const animal = { respirar() { return "respirando"; } };

// Um objeto que usa 'animal' como protótipo
const cao = Object.create(animal);
cao.latir = function() { return "au!"; };

console.log(cao.latir());      // "au!"  (propriedade própria)
console.log(cao.respirar());   // "respirando"  (encontrada no protótipo!)
```

Quando o JS não encontra `respirar` em `cao`, ele sobe (procura em `animal`, que é seu protótipo). Se o protótipo do protótipo também não tiver, continua subindo até chegar a `Object.prototype` e, no fim, `null` — **a cadeia de protótipos**.

> [!question] Por que a cadeia de protótipos importa?
> Porque ela é o mecanismo de **herança** do JavaScript. Um objeto "herda" propriedades de seus protótipos simplesmente por referência na cadeia. Isso é conceitualmente diferente da herança por classes do [[Paradigma-Orientado-a-Objetos|POO clássico]] — embora o ES6 tenha introduzido a sintaxe `class`/`extends`, que é um *açúcar sintático* sobre o mesmo mecanismo de protótipos subjacente.

> [!warning] PEGADINHA — `class` ES6 não é herança clássica de verdade
> O `class` do ES6 **parece** classes do Java, mas por baixo **continua usando protótipos**. A afirmativa "o JavaScript ES6 possui herança orientada a objetos clássica" pode ser considerada simplista/cuidadosa pela banca: na prática, `class`/`extends` são **açúcar sintático sobre a cadeia de protótipos**. Se a prova perguntar "qual é o mecanismo fundamental de herança do JavaScript?", a resposta é **protótipos**.

---

## 6. Assincronia: Event Loop, Promises e async/await

### 6.1 O JavaScript é single-threaded e assíncrono

Uma das características mais desafiadoras é que o JavaScript é **single-threaded** (executa uma coisa por vez na thread principal) mas **assíncrono** — ele não bloqueia esperando operações lentas (I/O, rede). Isso é possível graças ao **Event Loop**.

### 6.2 O Event Loop e as microtasks

Quando uma operação assíncrona é iniciada, ela é enviada para ser processada; quando termina, seu *callback* entra numa fila. O **Event Loop** coleta essas tarefas pendentes e as executa quando a pilha principal está livre. Há duas filas distintas — e a prioridade entre elas é cobrada:

- **Microtasks** (ex.: resolução de `Promise.then`): executam **antes** das macrotasks.
- **Macrotasks** (ex.: `setTimeout`, `setInterval`, eventos): executam depois das microtasks.

```javascript
console.log("1");
setTimeout(() => console.log("2"), 0);   // macrotask — executa por último
Promise.resolve().then(() => console.log("3"));  // microtask
console.log("4");
// Saída: 1, 4, 3, 2
// (o console.log 4 roda imediatamente; a microtask 3 roda antes do setTimeout 2)
```

> [!warning] PEGADINHA — ordem: síncrono → microtask → macrotask
> A ordem de execução é: **código síncrono em execução** → **microtasks** (`.then` de Promises) → **macrotasks** (`setTimeout`). Um `setTimeout(..., 0)` **não** executa antes de uma `.then` pendente, mesmo com delay 0 — as microtasks têm prioridade. A banca adora pedir a ordem de saída de um código com `console.log`, `setTimeout` e `Promise.then`.

### 6.3 Promises

Uma **Promise** é um objeto que representa **uma operação assíncrona que pode ter três estados**:

- **pending (pendente):** operação em andamento;
- **fulfilled (resolvida):** concluída com sucesso;
- **rejected (rejeitada):** concluída com erro.

Uma Promise é criada com um executor e tratada com `.then` (sucesso), `.catch` (erro) e `.finally` (sempre).

```javascript
function buscarBeneficio(cpf) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            if (cpf) resolve({ cpf, status: "ativo" });
            else reject(new Error("CPF inválido"));
        }, 500);
    });
}

buscarBeneficio("123")
    .then(ben => console.log(ben.status))   // "ativo"
    .catch(erro => console.log("Erro:", erro.message))
    .finally(() => console.log("finalizado"));
```

### 6.4 async/await

O **`async`/`await`** (ES8) é uma sintaxe que permite escrever código assíncrono de forma mais **síncrona e legível**, por cima das Promises.

- **`async`** antes de uma função faz ela retornar **sempre uma Promise**;
- **`await`** pausa a execução da função `async` até a Promise resolver (ou rejeitar), sem bloquear o Event Loop.

```javascript
async function processar() {
    try {
        const ben = await buscarBeneficio("123");  // espera a Promise resolver
        console.log(ben.status);
    } catch (erro) {
        console.log("Erro:", erro.message);        // tratamento com try/catch
    }
}
processar();
```

> [!important] `await` só funciona dentro de função `async`
> O `await` **só pode ser usado dentro de uma função declarada como `async`** (ou no top-level module). Tentar usar `await` fora de uma função `async` gera erro de sintaxe. E dentro de uma `async` function, o `try/catch` é a forma natural de capturar rejeições.

> [!warning] PEGADINHA — async sempre retorna Promise
> Uma função marcada com **`async` sempre retorna uma Promise** — mesmo que internamente retorne um valor simples. `async function f() { return 5; }` retorna uma Promise que resolve para `5`, não o número `5` diretamente. A banca adora testar se você sabe que `await f()` (ou `.then`) é necessário para obter o valor.

---

## 7. Sintaxe ES6+ moderna

O **ES6 (ECMAScript 2015)** e versões posteriores trouxeram uma série de açúcares sintáticos que você já viu (arrow functions, `let`/`const`) e que agora completamos: **destructuring**, **spread/rest**, e o **template literal**.

### 7.1 Destructuring (desestruturação)

O **destructuring** extrai valores de **objetos** ou **arrays** para variáveis de forma concisa.

```javascript
// Destructuring de objeto
const beneficiario = { nome: "Ana", cpf: "123", renda: 3200 };
const { nome, cpf } = beneficiario;
console.log(nome, cpf);   // Ana 123

// Destructuring de array
const [primeiro, segundo] = ["a", "b", "c"];
console.log(primeiro, segundo);   // a b

// Destructuring com renomeação
const { nome: nomeCompleto } = beneficiario;
console.log(nomeCompleto);        // Ana
```

### 7.2 Spread e Rest

- **Spread (`...`):** "espalha" os elementos de um iterável (array/objeto) em outro lugar.
- **Rest (`...`):** "recolhe" múltiplos valores em um agrupamento.

```javascript
// SPREAD — espalha elementos
const numeros = [1, 2, 3];
const copia = [...numeros, 4, 5];   // [1, 2, 3, 4, 5]
const obj = { a: 1, b: 2 };
const copiaObj = { ...obj, c: 3 };  // { a:1, b:2, c:3 }

// REST — recolhe parâmetros variáveis
function somarTudo(...valores) {     // rest: vira um array
    return valores.reduce((acc, v) => acc + v, 0);
}
somarTudo(1, 2, 3, 4);   // 10
```

> [!warning] PEGADINHA — spread vs. rest — são o mesmo símbolo com papéis opostos
> O operador **`...`** faz **spread** quando **desempacota** (espalha) e **rest** quando **empacota** (recolhe) — o papel depende do **contexto**. Em `[...array]` ele espalha; em `(...valores)` no parâmetro ele recolhe. A banca cobra essa dualidade: mesma sintaxe, função oposta conforme o uso.

### 7.3 Template literals

Os **template literals** (crases `` ` ``) permitem interpolar variáveis com `${}` e texto multilinha.

```javascript
const nome = "Maria";
const mensagem = `Olá, ${nome}! 
Seu benefício será creditado na conta de número 12345-6.`;
```

---

## 8. Como a FGV cobra este tópico

- **Tipagem dinâmica:** "JavaScript é estaticamente tipado" → falso.
- **`undefined` vs. `null`:** a variável não inicializada (`undefined`) vs. valor explícito de vazio (`null`); o `typeof null === "object"`.
- **var vs. let vs. const:** escopo (função vs. bloco), hoisting (var → `undefined`; let/const → TDZ → `ReferenceError`), e `const` que impede reatribuição, não mutação.
- **Closures:** a função que "lembra" o escopo onde foi criada.
- **Cadeia de protótipos:** o mecanismo de herança; `class` é açúcar sobre protótipos.
- **Event Loop / Promises / async-await:** a ordem síncrono → microtask → macrotask; os três estados da Promise; `async` sempre retorna Promise; `await` só em função `async`.
- **ES6+:** arrow functions (sem `this` próprio), destructuring, spread/rest.

> [!warning] PEGADINHA — o "default" que confunde
> Frase "O JavaScript implementa herança por classes como o Java" é, na leitura exigida pela banca, **contradita pelo mecanismo de protótipos** — mesmo com `class`/`extends` no ES6, o fundamento é a **cadeia de protótipos**, não uma herança de classes clássica. E "arrow functions possuem seu próprio `this`" é **falso** — elas herdam o `this` léxico.

---

## 9. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **Tipagem dinâmica** (tipo em tempo de execução, pode mudar)
> - [ ] Primitivos: `string`, `number`, `boolean`, `null`, `undefined`, `symbol`, `bigint`; `typeof null` → `"object"` (erro histórico)
> - [ ] **Escopo:** `var` (função, hoisting → `undefined`), `let`/`const` (bloco, TDZ → `ReferenceError`)
> - [ ] **`const`** impede reatribuição, **não mutação** (pode `push` em array const)
> - [ ] **Closure:** função que lembra o escopo de criação, mesmo após ele terminar
> - [ ] **Arrow functions:** sem `this` próprio (léxico), sem `arguments`, não são construtoras
> - [ ] **Protótipos:** herança por cadeia de protótipos; `class`/`extends` é açúcar sobre protótipos
> - [ ] **Event Loop:** síncrono → microtasks (`.then`) → macrotasks (`setTimeout`)
> - [ ] **Promise:** pending/fulfilled/rejected; `.then`/`.catch`/`.finally`
> - [ ] **async/await:** `async` sempre retorna Promise; `await` só em função `async`; `try/catch` para erros
> - [ ] **ES6+:** destructuring, spread (espalha) vs. rest (recolhe), template literals

> [!warning] O erro mais comum em prova
> Confundir a **ordem de execução assíncrona** (microtask antes de macrotask) e confundir **hoisting do `var`** (que retorna `undefined`) com o **TDZ do `let`/`const`** (que retorna erro). Na questão, pergunte: *é um valor indefinido (`undefined`) ou um erro (`ReferenceError`)?*

---

## 10. Próximos passos

Você entendeu o comportamento do JavaScript: a tipagem dinâmica, o escopo e o hoisting, as closures, os protótipos e a assincronia com Promises/async-await, além da sintaxe moderna do ES6+. Esse é exatamente o vocabulário que o **frontend web** (bloco posterior) vai usar com os frameworks Vue, Angular e React — mas ali o foco estará nas diferenças conceituais entre os frameworks, não na sintaxe básica que você acabou de dominar.

Antes disso, porém, a ementa devolve você ao **mundo Java**: o próximo tópico é **Frameworks Java** — Spring, Spring Boot, Spring Cloud, JSF e PrimeFaces. Ou seja, consolidamos três linguagens (Java, JavaScript e o POO) e agora vamos ver como o **Java organiza aplicações corporativas** com injeção de dependência, autoconfiguração e seus padrões — a ponte natural com os **padrões de projeto** do tópico 5.
