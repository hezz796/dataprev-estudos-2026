# Fundamentos Web

> [!info] Metadados
> **Disciplina:** Tecnologias e Práticas Frontend Web
> **Bloco:** 5.1 — Tecnologias e Práticas Frontend Web (FASE 5 — Frontend e Interfaces)
> **Tópico:** 1. Fundamentos Web
> **Subtópicos:** HTML5 (semântica, forms, acessibilidade básica) · CSS3 (seletores, box model, flexbox, grid, responsividade) · UX (princípios básicos de usabilidade, heurísticas de Nielsen) · Ajax (requisições assíncronas, API calls do navegador)
> **Pré-requisitos:** [[JavaScript]] (sintaxe, ES6+, assincronia com Promises/async-await) · [[Padroes-de-Projeto-e-Arquitetura|APIs RESTful]] (verbos HTTP, status codes, recursos) · [[Testes-Automatizados|Selenium]] (testes de UI web — conceito)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-31

---

## 1. Por que estudar fundamentos web?

Até aqui você dominou o **backend** (Java, Spring, APIs RESTful) e a **lógica de programação** (JavaScript, assincronia, Promises). Mas existe uma questão que toda aplicação web precisa responder: *como o usuário final vê e interage com o sistema?* É isso que o **frontend** resolve — e os fundamentos web são a base de qualquer interface web, desde o portal do Meu INSS até os sistemas internos de gestão de benefícios da DATAPREV.

Por que isso importa na prática? Porque o **portal gov.br**, o **Meu INSS** e dezenas de sistemas corporativos da seguridade social são, em sua essência, **aplicações web**. Milhões de cidadãos acessam esses sistemas todos os dias — em celulares, tablets e computadores — e a experiência deles depende diretamente de como o HTML está estruturado, de como o CSS organiza o layout, e de como o JavaScript comunica com o backend. Um formulário de requerimento de benefício mal estruturado pode causar erros de dados; um layout que não se adapta ao celular exclui uma parcela enorme de usuários.

> [!question] Pergunta orientadora
> Se o backend é a "cozinha" onde os dados são processados, o que é a "fachada" que o cliente enxerga? E se o cliente é um idoso tentando acessar o Meu INSS pelo celular — o que acontece se a página não for responsiva ou se o formulário não validar dados antes do envio?

Este bloco se apoia diretamente no que você já estudou no [[JavaScript|Bloco 4.1 — JavaScript]]: **assincronia**, **Promises**, **async/await** e **fetch**. Também retoma as [[Padroes-de-Projeto-e-Arquitetura|APIs RESTful]] (verbos HTTP, status codes) que o frontend precisa consumir. E se conecta ao [[Testes-Automatizados|Selenium]], que você viu nos testes automatizados — o Selenium testa exatamente a **interface web** que você vai aprender a construir agora.

---

## 2. HTML5 — a estrutura semântica da web

### 2.1 O que é HTML e por que a semântica importa

**HTML (HyperText Markup Language)** é a linguagem de marcação que define a **estrutura e o conteúdo** de uma página web. Ela não é uma linguagem de programação — não tem variáveis, loops nem funções. Ela **descreve** o que cada elemento *é* e *significa*: um título, um parágrafo, uma imagem, um formulário.

O **HTML5** — a versão atual — trouxe uma mudança fundamental: **tags semânticas**. Antes do HTML5, tudo era `<div>` — um "caixa genérica" sem significado. O HTML5 introduziu tags que **comunicam o significado do conteúdo** para o navegador, para leitores de tela, e para mecanismos de busca.

> [!important] Por que semântica importa — o triplo benefício
> Tags semânticas beneficiam três públicos: **(1)** desenvolvedores que mantenham o código (legibilidade); **(2)** **mecanismos de busca** como Google (SEO — o buscador entende melhor a estrutura); **(3)** **leitores de tela** para pessoas com deficiência visual (acessibilidade — o leitor anuncia "navegação principal" em vez de "div número 3"). A FGV cobra esse triplo benefício.

### 2.2 Tags semânticas principais

| Tag | Função | Quando usar |
|---|---|---|
| `<header>` | Cabeçalho de uma seção ou da página | Logo, título, menu de navegação |
| `<nav>` | Bloco de **navegação** | Menu principal, links de breadcrumbs |
| `<main>` | Conteúdo **principal** da página | A área onde está o conteúdo único e principal |
| `<section>` | Seção temática genérica | Dividir conteúdo em blocos temáticos |
| `<article>` | Conteúdo **independente e autocontido** | Post, notícia, comentário, card de benefício |
| `<aside>` | Conteúdo **complementar** (relacionado indiretamente) | Sidebar, links relacionados |
| `<footer>` | Rodapé de uma seção ou da página | Copyright, contatos, links auxiliares |
| `<figure>` + `<figcaption>` | Ilustração com legenda | Imagem com descrição (gráfico, foto, diagrama) |

### 2.3 Exemplo: HTML5 semântico aplicado

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Consulta de Benefícios — DATAPREV</title>
</head>
<body>
    <header>
        <h1>Sistema de Benefícios</h1>
        <nav aria-label="Menu principal">
            <ul>
                <li><a href="/consultar">Consultar</a></li>
                <li><a href="/requerer">Requerer</a></li>
                <li><a href="/acompanhar">Acompanhar</a></li>
            </ul>
        </nav>
    </header>

    <main>
        <article>
            <h2>Consulta por CPF</h2>
            <section>
                <p>Informe o CPF do beneficiário para consultar seus benefícios ativos.</p>
            </section>
            <section>
                <form action="/api/consulta" method="GET" role="search">
                    <label for="cpf">CPF:</label>
                    <input type="text" id="cpf" name="cpf"
                           placeholder="000.000.000-00"
                           pattern="\d{3}\.\d{3}\.\d{3}-\d{2}"
                           required
                           aria-describedby="cpf-ajuda">
                    <small id="cpf-ajuda">Formato: 000.000.000-00</small>
                    <button type="submit">Consultar</button>
                </form>
            </section>
        </article>
    </main>

    <footer>
        <p>&copy; 2026 DATAPREV — Todos os direitos reservados.</p>
    </footer>
</body>
</html>
```

Observe dois detalhes: o atributo `lang="pt-BR"` no `<html>` (fala ao navegador e aos leitores de tela que o conteúdo é em português brasileiro) e o atributo `aria-label` no `<nav>` (descreve a finalidade do bloco para tecnologias assistivas). Acessibilidade não é uma feature opcional — é uma **exigência legal** para sistemas governamentais.

### 2.4 Formulários HTML5

Os **formulários** são a porta de entrada de dados em qualquer aplicação web — e na DATAPREV, são exatamente os formulários que os cidadãos usam para requerer benefícios, atualizar dados e consultar informações. O HTML5 trouxe tipos de `<input>` nativos e **validação sem JavaScript**.

**Tipos de input importantes:**

| Tipo | Função | Validação nativa |
|---|---|---|
| `text` | Texto genérico | — |
| `email` | Endereço de e-mail | Valida formato de e-mail |
| `number` | Número | Aceita apenas numéricos, `min`/`max` |
| `date` | Data | Seletor de data nativo do navegador |
| `tel` | Telefone | Teclado numérico em dispositivos móveis |
| `password` | Senha | Mascara os caracteres |
| `search` | Campo de busca | Comportamento de busca |

**Atributos de validação nativos:**

| Atributo | Função |
|---|---|
| `required` | Campo obrigatório |
| `pattern` | Expressão regular que o valor deve seguir |
| `minlength` / `maxlength` | Tamanho mínimo/máximo |
| `min` / `max` | Valor mínimo/máximo (para `number`/`date`) |
| `placeholder` | Texto de exemplo (não substitui label!) |

```html
<form action="/api/beneficio" method="POST">
    <label for="cpf">CPF:</label>
    <input type="text" id="cpf" name="cpf"
           pattern="\d{3}\.\d{3}\.\d{3}-\d{2}"
           required>

    <label for="email">E-mail:</label>
    <input type="email" id="email" name="email" required>

    <label for="valor">Valor do benefício:</label>
    <input type="number" id="valor" name="valor"
           min="0" step="0.01" required>

    <button type="submit">Enviar</button>
</form>
```

> [!warning] PEGADINHA — validação HTML5 não substitui validação no backend
> A validação nativa do HTML5 é **apenas no cliente** — o navegador verifica antes de enviar. Mas ela pode ser **contornada** facilmente (desabilitando JavaScript ou usando ferramentas de desenvolvedor). Por isso, **toda validação de segurança deve ser feita também no servidor**. A banca adora colocar: "com HTML5, a validação de formulários no servidor torna-se desnecessária" — isso é **falso**. Validação client-side é conveniência, não segurança.

### 2.5 Acessibilidade básica no HTML

O termo **acessibilidade web** (muitas vezes abreviado como **a11y**, de "a" + 11 letras + "y") se refere a tornar a web utilizável por **todas as pessoas**, incluindo aquelas com deficiências visuais, motoras, cognitivas ou auditivas. No contexto de sistemas governamentais brasileiros, a acessibilidade é **obrigatória** — o Decreto 5.296/2004 e as diretrizes do e-MAG (Modelo de Acessibilidade em Governo Eletrônico) exigem conformidade.

O HTML semântico já dá o primeiro passo. Outras práticas básicas incluem:

- **Sempre usar `<label>`** associado a `<input>` (via `for`/`id`) — leitores de tela precisam saber o que cada campo significa;
- **Usar `alt` em imagens** — descreve o conteúdo da imagem para quem não pode vê-la;
- **Usar `aria-label` e `aria-describedby`** quando a semântica HTML não é suficiente;
- **Garantir navegação por teclado** — todos os elementos interativos devem ser acessíveis via `Tab`.

> [!note] Acessibilidade: fundamento aqui, aprofundamento no Bloco 5.2
> Este bloco cobre apenas os **fundamentos** de acessibilidade web — a relação com HTML semântico e atributos ARIA básicos. O aprofundamento (WCAG, testes de acessibilidade, leitores de tela, navegação por teclado em profundidade) será coberto no [[Fundamentos-Web|Bloco 5.2 — UX e Gestão de Conteúdo]], que é o próximo módulo dentro da Fase 5.

---

## 3. CSS3 — apresentação e layout

### 3.1 O papel do CSS

Se o HTML define **o que** cada elemento *é*, o CSS define **como** ele *aparece*. **CSS (Cascading Style Sheets)** é a linguagem de estilização que controla cores, fontes, espaçamento, posicionamento e layout. A separação de responsabilidades é um princípio fundamental:

| Responsabilidade | Tecnologia |
|---|---|
| **Estrutura e significado** | HTML |
| **Apresentação visual** | CSS |
| **Comportamento e interação** | JavaScript |

> [!warning] PEGADINHA — quem controla o layout: HTML, CSS ou JavaScript?
> A banca adora confundir: "o HTML controla o layout da página" — **falso**. O HTML define a **estrutura**; o CSS define o **layout**; o JavaScript define o **comportamento**. Se uma questão descreve algo como "definir a posição de um elemento na tela", a resposta é **CSS**, não HTML. Se descreve "tornar o layout responsivo com base no tamanho da tela", também é **CSS** (media queries).

### 3.2 Seletores CSS

**Seletores** indicam **a qual elemento** um estilo será aplicado. Os mais cobrados em concursos:

| Seletor | Exemplo | Seleciona |
|---|---|---|
| Elemento | `p` | Todos os parágrafos |
| Classe | `.card` | Elementos com `class="card"` |
| ID | `#menu` | O elemento com `id="menu"` |
| Descendente | `nav a` | Todos os `<a>` dentro de `<nav>` |
| Filho direto | `nav > a` | Apenas `<a>` filhos diretos de `<nav>` |
| Pseudo-classe | `a:hover`, `input:focus` | Estado do elemento (hover, foco, etc.) |

### 3.3 Box Model — o modelo de caixa

Todo elemento HTML é uma **caixa retangular** composta por, de dentro para fora:

1. **Content (conteúdo):** onde o texto ou imagem aparece (largura × altura definidas por `width`/`height`);
2. **Padding (preenchimento):** espaço entre o conteúdo e a borda;
3. **Border (borda):** a borda da caixa;
4. **Margin (margem):** espaço externo entre essa caixa e as vizinhas.

```
┌─────────────────── margin ───────────────────┐
│  ┌──────────────── border ────────────────┐  │
│  │  ┌──────────── padding ───────────┐    │  │
│  │  │  ┌─────── content ─────────┐   │    │  │
│  │  │  │                         │   │    │  │
│  │  │  │      Texto ou imagem    │   │    │  │
│  │  │  │                         │   │    │  │
│  │  │  └─────────────────────────┘   │    │  │
│  │  └────────────────────────────────┘    │  │
│  └────────────────────────────────────────┘  │
└──────────────────────────────────────────────┘
```

> [!tip] `box-sizing: border-box`
> Por padrão (`content-box`), o `width` define apenas o **conteúdo** — padding e border são somados ao tamanho total. Com `box-sizing: border-box`, o `width` inclui **conteúdo + padding + border** — tornando o cálculo de layouts muito mais previsível. Na prática, quase todo projeto moderno aplica `* { box-sizing: border-box; }` globalmente.

### 3.4 Flexbox — layout em uma dimensão

O **Flexbox** (Display Flex) é um modelo de layout que organiza itens em uma **única direção** — horizontal ou vertical — com controle preciso de alinhamento, espaçamento e distribuição.

```css
.container {
    display: flex;
    justify-content: space-between; /* distribui no eixo principal */
    align-items: center;            /* centraliza no eixo transversal */
    gap: 16px;                      /* espaço entre os itens */
}
```

**Propriedades principais do Flexbox:**

| Propriedade | Efeito |
|---|---|
| `flex-direction` | Direção: `row` (horizontal), `column` (vertical) |
| `justify-content` | Alinhamento no **eixo principal** (espaço, centro, início, fim) |
| `align-items` | Alinhamento no **eixo transversal** |
| `flex-wrap` | Permite que itens "quebrem" para a próxima linha |
| `gap` | Espaço entre os itens |

O Flexbox é perfeito para **arranjos lineares** — uma barra de navegação, uma lista de cards em linha, centralizar um formulário na tela.

### 3.5 Grid — layout em duas dimensões

O **CSS Grid** (Display Grid) é um modelo de layout que organiza itens em **duas dimensões** simultaneamente — linhas **e** colunas. É ideal para layouts de página inteira, dashboards e grids de conteúdo.

```css
.dashboard {
    display: grid;
    grid-template-columns: 250px 1fr 1fr;  /* 3 colunas */
    grid-template-rows: auto 1fr auto;      /* 3 linhas */
    gap: 16px;
}

/* Áreas nomeadas */
.header  { grid-column: 1 / -1; }          /* ocupa todas as colunas */
.sidebar { grid-row: 2 / 4; }              /* ocupa linhas 2 e 3 */
```

> [!question] Flexbox ou Grid — qual usar?
> A regra prática: se o layout é **linear** (uma direção — linha ou coluna), use **Flexbox**. Se o layout é **bidimensional** (linhas e colunas ao mesmo tempo), use **Grid**. Na FGV, quando a questão descreve "organizar itens em uma única linha" → Flexbox; "organizar conteúdo em áreas de uma página" → Grid. Na prática, os dois se complementam — muitos projetos usam Grid para a estrutura da página e Flexbox para componentes internos.

### 3.6 Responsividade — Media Queries

A **responsividade** (ou *responsive design*) é a capacidade de uma página se **adaptar** a diferentes tamanhos de tela — desktop, tablet, celular. A técnica fundamental são as **media queries**: blocos CSS que só se aplicam quando uma condição de viewport é atendida.

```css
/* Estilo base (mobile-first) */
.card {
    padding: 16px;
    font-size: 14px;
}

/* A partir de 768px (tablet) */
@media (min-width: 768px) {
    .card {
        padding: 24px;
        font-size: 16px;
    }
}

/* A partir de 1024px (desktop) */
@media (min-width: 1024px) {
    .card {
        padding: 32px;
    }
}
```

O **approach mobile-first** é o padrão moderno: você escreve os estilos para o menor tamanho primeiro e vai **adicionando** media queries conforme a tela cresce. Isso garante que o site funcione bem no celular (onde a maioria dos cidadãos acessa o Meu INSS) e melhora a performance em conexões lentas.

> [!warning] PEGADINHA — responsividade é CSS, não JavaScript
> "O JavaScript é necessário para tornar uma página responsiva" — **falso**. Responsividade é alcança com **CSS puro** (media queries, flexbox, grid). JavaScript pode *complementar* (ex.: detecção de dispositivo), mas a técnica fundamental é CSS. A banca testa se você sabe separar responsabilidades.

---

## 4. UX — princípios básicos de usabilidade

### 4.1 O que é UX?

**UX (User Experience)** é a **experiência completa** que um usuário tem ao interagir com um produto — não é apenas "bonito" (isso seria UI/Design Visual). UX envolve **usabilidade** (facilidade de uso), **acessibilidade** (utilizável por todos), **eficiência** (o usuário atinge seu objetivo com mínimo esforço) e **satisfação** (a experiência é agradável).

> [!note] UX vs. UI — distinção essencial
> **UX (User Experience Design):** como o usuário **se sente** e **se comporta** ao usar o produto — fluxos, jornadas, facilidade. **UI (User Interface Design):** como o produto **aparece visualmente** — cores, tipografia, ícones, botões. UX é sobre **funcionar bem**; UI é sobre **parecer bem**. Uma pode existir sem a outra: um sistema pode ter UI bonita mas UX péssima (difícil de usar) ou UX boa com UI simples (funcional, sem luxo).

### 4.2 Heurísticas de Nielsen — as 10 regras da usabilidade

As **Heurísticas de Nielsen** são um conjunto de **10 princípios de usabilidade** formulados pelo pesquisador Jakob Nielsen. Elas funcionam como um **checklist** para avaliar se uma interface é usável. São amplamente usadas em avaliações de usabilidade e **muito cobradas em concursos**.

> [!note] Heurísticas de Nielsen: fundamentos aqui, aprofundamento no Bloco 5.2
> Neste bloco, apresentamos as 10 heurísticas em nível conceitual — o suficiente para reconhecê-las e aplicar em questões básicas. O aprofundamento (como avaliar interfaces com base nas heurísticas, testes de usabilidade, wireframes, prototipação) será coberto no Bloco 5.2 — UX e Gestão de Conteúdo.

As 10 heurísticas, em linguagem simples:

| # | Heurística | Essência | Exemplo no contexto gov.br |
|---|---|---|---|
| 1 | **Status do sistema** | O usuário deve saber o que está acontecendo a qualquer momento | Barra de progresso ao enviar um requerimento |
| 2 | **Linguagem do mundo real** | Usar termos familiares ao usuário, não jargão técnico | Dizer ".Nome completo" em vez de "field_nome_completo" |
| 3 | **Controle e liberdade** | O usuário deve poder desfazer erros facilmente | Botão "Voltar" ou "Cancelar" no formulário |
| 4 | **Consistência e padrões** | Seguir convenções — não inventar comportamentos | Botões "Salvar" sempre na mesma posição |
| 5 | **Prevenção de erros** | Evitar que erros aconteçam, não apenas tratá-los | Desabilitar botão "Enviar" enquanto dados obrigatórios estiverem vazios |
| 6 | **Reconhecimento em vez de memória** | Tornar opções visíveis, não exigir que o usuário lembre | Mostrar opções de benefício em vez de pedir para digitar o código |
| 7 | **Flexibilidade e eficiência** | Atalhos para usuários avançados, caminho simples para iniciantes | Busca avançada e busca simples lado a lado |
| 8 | **Estética e design minimalista** | Interface limpa — apenas o necessário | Formulário com apenas os campos essenciais na primeira tela |
| 9 | **Ajuda para reconhecer, diagnosticar e recuperar erros** | Mensagens de erro claras e úteis | "CPF inválido — verifique se digitou corretamente" em vez de "Erro 422" |
| 10 | **Ajuda e documentação** | Facilitar acesso a ajuda quando necessário | Link "Precisa de ajuda?" ao lado de campos complexos |

> [!tip] Como a banca cobra as heurísticas
> A FGV costuma apresentar um **cenário** (ex.: "O formulário não mostra se o dados foram salvos") e perguntar **qual heurística foi violada**. Para resolver, identifique a **essência do problema** e encontre a heurística correspondente na tabela acima. A dica é: leia a heurística como uma **pergunta** — se o cenário viola essa pergunta, é a heurística certa. Por exemplo: "O sistema não informa que a operação foi concluída" → a pergunta "o usuário sabe o que está acontecendo?" (Heurística 1) é violada.

---

## 5. Ajax — requisições assíncronas do navegador

### 5.1 O que é Ajax

**Ajax (Asynchronous JavaScript and XML)** é uma técnica que permite ao navegador **enviar e receber dados do servidor em segundo plano**, sem recarregar a página inteira. Embora o nome original mencione XML, hoje o formato mais usado é o **JSON** — mas o conceito permanece: **comunicação assíncrona entre frontend e backend**.

É exatamente o que acontece quando você digita um CEP em um formulário e a cidade/estado aparecem automaticamente — sem apertar "Enviar". O JavaScript envia a requisição ao servidor, recebe a resposta, e atualiza apenas aquele trecho da página.

> [!question] Pergunta orientadora
> Quando você estudou [[JavaScript|Promises e async/await]], aprendemos que operações assíncronas não bloqueiam o navegador. E quando estudamos as [[Padroes-de-Projeto-e-Arquitetura|APIs RESTful]], vimos que o backend expõe recursos via verbos HTTP (GET, POST, etc.). A pergunta é: **como o frontend faz essas chamadas REST ao backend, de forma assíncrona, sem recarregar a página?** A resposta é o **fetch API** — a forma moderna de fazer Ajax.

### 5.2 XMLHttpRequest vs. fetch

Há duas formas de fazer requisições Ajax no navegador:

**XMLHttpRequest (XHR):** a abordagem antiga, baseada em eventos. Funcional, mas verbosa e difícil de ler.

**Fetch API:** a abordagem moderna, baseada em **Promises** — mais limpa, mais legível, e se integra perfeitamente com `async/await` que você já dominou no [[JavaScript]].

> [!important] A banca foca no `fetch`
> O `XMLHttpRequest` é mais cobrado como "conceito histórico" — a banca pode perguntar que o Ajax originalmente usava XHR. Mas código prático e questões modernas focam no **fetch API**. Domine o fetch; conheça o XHR apenas conceitualmente.

### 5.3 Fetch API — a forma moderna

O `fetch()` retorna uma **Promise** que resolve para um objeto `Response`. Veja a conexão direta com o [[JavaScript]]: tudo que você aprendeu sobre `async`/`await` e `.then()`/.`catch()` se aplica aqui.

```javascript
// Requisição GET simples — consultar um beneficiário por CPF
async function consultarBeneficio(cpf) {
    try {
        const resposta = await fetch(`/api/beneficiarios/${cpf}`);
        
        if (!resposta.ok) {
            throw new Error(`Erro HTTP: ${resposta.status}`);
        }
        
        const dados = await resposta.json();  // parse do JSON
        console.log(dados.nome, dados.status);
    } catch (erro) {
        console.error("Falha na consulta:", erro.message);
    }
}
```

**Requisição POST — criar um novo registro:**

```javascript
async function criarRequerimento(dados) {
    try {
        const resposta = await fetch("/api/requerimentos", {
            method: "POST",
            headers: {
                "Content-Type": "application/json"
            },
            body: JSON.stringify(dados)
        });

        if (resposta.status === 201) {       // 201 Created
            const resultado = await resposta.json();
            console.log("Requerimento criado:", resultado.id);
        } else {
            const erro = await resposta.json();
            console.error("Erro:", erro.mensagem);
        }
    } catch (erro) {
        console.error("Falha na requisição:", erro.message);
    }
}

// Uso
criarRequerimento({
    cpf: "123.456.789-00",
    tipoBeneficio: "APOSENTADORIA",
    dataInicio: "2026-09-01"
});
```

Observe a conexão com as [[Padroes-de-Projeto-e-Arquitetura|APIs RESTful]]: o método `GET` para consultar (status 200), o método `POST` para criar (status 201), e o `Content-Type: application/json` indicando que o corpo é JSON. O `response.ok` verifica se o status está na faixa 200-299 (sucesso).

### 5.4 Tratamento de erros em chamadas Ajax

O `fetch` tem uma particularidade que é uma **pegadinha clássica**: ele **não rejeita a Promise** em caso de erro HTTP (como 404 ou 500). A Promise só é rejeitada se houver falha de **rede** (servidor offline, sem internet). Por isso, é necessário checar `response.ok` manualmente.

```javascript
// Erro de rede → Promise rejeitada (entra no catch)
await fetch("http://servidor-inexistente.com/api");

// Erro HTTP (404, 500) → Promise RESOLVIDA (não entra no catch!)
const resp = await fetch("/api/rota-inexistente");
console.log(resp.ok);     // false
console.log(resp.status); // 404
// O catch NÃO é acionado — precisa checar resp.ok manualmente
```

> [!warning] PEGADINHA — fetch não rejeita em erro HTTP
> Essa é uma das armadilhas mais rentáveis da FGV sobre Ajax: "fetch() rejeita a Promise quando o servidor retorna status 404" — **falso**. O fetch só rejeita em falha de **rede**. Erros HTTP (4xx, 5xx) resolvem normalmente — você precisa checar `response.ok` ou `response.status` para detectá-los. Essa distinção é cobrada justamente porque é contraintuitiva.

---

## 6. Como a FGV cobra este tópico

- **HTML semântico:** qual tag usar em cada contexto (ex.: `<nav>` para navegação, `<article>` para conteúdo independente) — e *por que* (acessibilidade, SEO).
- **Responsabilidade HTML vs. CSS:** HTML = estrutura; CSS = apresentação; JavaScript = comportamento. A banca mistura as responsabilidades para confundir.
- **Box Model:** a ordem content → padding → border → margin; a diferença entre `content-box` e `border-box`.
- **Flexbox vs. Grid:** Flexbox = 1 dimensão (linha OU coluna); Grid = 2 dimensões (linhas E colunas).
- **Media queries:** responsividade é CSS, não JavaScript.
- **Heurísticas de Nielsen:** reconhecer qual heurística foi violada em um cenário descrito (foco na Heurística 1 — status do sistema, e Heurística 9 — mensagens de erro).
- **Fetch API:** `fetch()` retorna Promise; `fetch` não rejeita em erro HTTP (apenas em falha de rede); `response.ok` é necessário para verificar sucesso.
- **XHR vs. fetch:** XHR é legado, fetch é moderno e baseado em Promise.

> [!warning] PEGADINHA — as três armadilhas mais rentáveis
> (1) **Responsabilidade:** "HTML define o layout" → **falso** (é CSS). "JavaScript é necessário para responsividade" → **falso** (é CSS). (2) **Fetch e erros:** "fetch() rejeita a Promise em status 404" → **falso** (só em falha de rede). (3) **Heurísticas:** confundir Heurística 1 (status do sistema = informar o que está acontecendo) com Heurística 6 (memória = mostrar opções em vez de exigir lembrete). A banca adora trocar essas duas.

---

## 7. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **HTML5 semântico:** `header`, `nav`, `main`, `section`, `article`, `footer` — cada qual com sua função
> - [ ] **Formulários HTML5:** tipos de input (`email`, `number`, `tel`), validação nativa (`required`, `pattern`, `min/max`)
> - [ ] **Acessibilidade:** `<label>` com `for`/`id`, `alt` em imagens, `aria-label`, `lang="pt-BR"` — fundamento aqui, WCAG no Bloco 5.2
> - [ ] **Responsabilidade:** HTML = estrutura · CSS = apresentação · JS = comportamento
> - [ ] **Box Model:** content → padding → border → margin; `box-sizing: border-box`
> - [ ] **Flexbox:** 1 dimensão; `display: flex`, `justify-content`, `align-items`, `gap`
> - [ ] **Grid:** 2 dimensões; `display: grid`, `grid-template-columns`, `grid-template-rows`
> - [ ] **Responsividade:** media queries (`@media (min-width: ...)`) — mobile-first
> - [ ] **UX vs. UI:** UX = experiência/funcionalidade · UI = aparência visual
> - [ ] **Heurísticas de Nielsen:** 10 princípios — memorize as essências (especialmente 1, 4, 5, 9)
> - [ ] **Fetch API:** `fetch()` retorna Promise; `response.ok` para verificar sucesso; **não rejeita em erro HTTP**
> - [ ] **XMLHttpRequest:** conceito legado; fetch é a forma moderna

> [!warning] O erro mais comum em prova
> Confundir **responsabilidades** (dizer que HTML define layout ou que JavaScript faz responsividade) e **subestimar o fetch** (achar que ele rejeita automaticamente em erro HTTP — quando na verdade precisa checar `response.ok`). E nas heurísticas, confundir **status do sistema** (informar o que acontece) com **prevenção de erros** (evitar que o erro ocorra) — são heurísticas diferentes mas parecidas em português.

---

## 8. Próximos passos

Você agora domina os fundamentos da web: a **estrutura** (HTML5 semântico), a **apresentação** (CSS3 com flexbox e grid), os **princípios de usabilidade** (UX e Heurísticas de Nielsen) e a **comunicação assíncrona** com o backend (Ajax via fetch). Essa é a base sobre a qual se constroem as aplicações web modernas.

O próximo tópico mergulha em como os **frameworks e bibliotecas frontend** organizam e simplificam esse trabalho: **Vue.js, Angular e React** — as três tecnologias mais usadas no mercado e cobradas pela FGV. A questão que o próximo bloco responde é: *"se o JavaScript puro já consegue manipular o DOM e fazer requisições Ajax, por que precisamos de frameworks?"* A resposta tem a ver com **componentização**, **reatividade** e **gerenciamento de estado** — temas que conectam diretamente com o que você já viu sobre [[Metodologias-Ageis|reuso e componentização]] no Bloco 4.2.
