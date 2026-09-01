# Frontend Web — Questões Autorais Comentadas

> **Disciplina:** Tecnologias e Práticas Frontend Web · **Bloco:** 5.1 — Tecnologias e Práticas Frontend Web
> **Banca de referência:** FGV · **Formato:** alternativas A–E
> **Origem:** autoral (todas) · **Não são questões oficiais de banca.**

---

## Questão 01 — Fundamentos Web (HTML5 e CSS3)

**id:** FRONT-001
**disciplina:** Tecnologias e Práticas Frontend Web
**tópico:** Fundamentos Web
**subtópico:** HTML5 (semântica, forms, acessibilidade básica) e CSS3 (box model, flexbox, grid, responsividade)
**origem:** autoral
**habilidade cognitiva:** análise
**dificuldade:** média
**conhecimento avaliado:** tags semânticas e por que usá-las; responsabilidade HTML vs. CSS vs. JS; flexbox (1 dimensão) vs. grid (2 dimensões); responsividade via media queries

A equipe da DATAPREV está reestruturando o portal de consulta de benefícios. Considere as afirmativas abaixo:

I. A tag `<nav>` deve ser usada para agrupar o bloco de navegação (menu), porque comunica a função do conteúdo ao navegador, aos leitores de tela e aos mecanismos de busca — diferentemente de um `<div>` genérico.

II. O CSS é a tecnologia responsável por definir a posição e o layout dos elementos na página, como organizar itens em uma única linha por meio da propriedade `display: grid`.

III. O CSS Grid é indicado quando o layout exige organização simultânea em linhas e colunas, enquanto o Flexbox organiza itens em uma única direção (linha ou coluna).

IV. Uma página totalmente responsiva, que se adapta a diferentes tamanhos de tela, pode ser alcançada somente com CSS, usando-se, entre outras técnicas, media queries.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I e II
B) II e IV
C) I, III e IV
D) I e III
E) III e IV

---

**Gabarito:** C

### Comentário

**Raciocínio:** A questão exige avaliar cada afirmação sobre HTML semântico e CSS. É preciso separar as responsabilidades das tecnologias (HTML = estrutura; CSS = apresentação) e distinguir Flexbox de Grid.

**Palavra-chave:** `<nav>` = navegação semântica; HTML = estrutura · CSS = apresentação · JS = comportamento; Flexbox = 1 dimensão; Grid = 2 dimensões; media queries = responsividade

**Conceito:**
- **Afirmativa I é verdadeira.** A tag `<nav>` é uma tag semântica que indica o bloco de navegação — beneficia o código (legibilidade), o SEO (o buscador entende a estrutura) e a acessibilidade (o leitor de tela anuncia "navegação principal"). O `<div>` é uma caixa genérica sem significado.
- **Afirmativa II é falsa.** A primeira parte está correta (o CSS define layout), mas o exemplo está errado: organizar itens em **uma única linha** é função do **Flexbox** (`display: flex`), não do Grid. O **Grid** é para **duas dimensões** simultâneas.
- **Afirmativa III é verdadeira.** Essa é a distinção essencial: **Flexbox** = 1 dimensão (row ou column); **Grid** = 2 dimensões (linhas **e** colunas).
- **Afirmativa IV é verdadeira.** Responsividade é alcançada **com CSS puro** — principalmente via media queries (`@media (min-width: ...)`), combinadas com Flexbox e Grid. JavaScript pode complementar, mas não é necessário.

**Análise das alternativas:**
- **A (I e II):** errada — inclui II (falsa).
- **B (II e IV):** errada — inclui II (falsa).
- **C (I, III e IV):** correta.
- **D (I e III):** errada — não inclui IV (verdadeira).
- **E (III e IV):** errada — não inclui I (verdadeira).

**Pegadinha:** A alternativa II é a armadilha principal: ela acerta na primeira parte ("CSS define layout") para fazer o candidato "engolir" o erro no exemplo (`grid` para uma linha). A banca mistura a responsabilidade correta com a ferramenta errada. Lembre: **Grid = linhas E colunas ao mesmo tempo; Flexbox = uma direção.** E cuidado com outra inversão clássica: "HTML define o layout" é falso (é CSS) — responsabilidade e ferramenta são testadas como pegadinha.

---

## Questão 02 — Frameworks Frontend (VueJS, Angular, React)

**id:** FRONT-002
**disciplina:** Tecnologias e Práticas Frontend Web
**tópico:** Frameworks Frontend
**subtópico:** Diferenças conceituais entre VueJS, Angular e React (classificação, TypeScript, JSX/templates, Injeção de Dependência, Virtual DOM)
**origem:** autoral
**habilidade cognitiva:** análise
**dificuldade:** média-alta
**conhecimento avaliado:** React = biblioteca (não framework); Angular = framework completo com TypeScript obrigatório e DI nativa; Vue = framework progressivo; JSX vs. templates; Virtual DOM como técnica compartilhada

Um desenvolvedor está revisitando as diferenças entre os principais frameworks frontend usados pela DATAPREV. Considere as afirmativas abaixo:

I. O React é uma biblioteca, e não um framework, porque define como construir componentes de interface, mas não define a organização da aplicação como um todo — isso depende de bibliotecas complementares, como o React Router.

II. O Angular é um framework completo que exige TypeScript e possui um sistema de Injeção de Dependência nativo, conceitualmente análogo ao do Spring.

III. O uso de JSX no React significa escrever HTML dentro de JavaScript, sendo essa a principal razão de o React ser classificado como uma biblioteca.

IV. O Virtual DOM é uma técnica compartilhada por React e Vue, que atualiza no DOM real apenas as partes que mudaram — não sendo exclusividade de nenhum dos dois.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I e II
B) II e IV
C) I, II e IV
D) I e III
E) III e IV

---

**Gabarito:** C

### Comentário

**Raciocínio:** A questão testa as distinções conceituais que a FGV mais cobra neste bloco: classificação (biblioteca vs. framework), TypeScript no Angular, Injeção de Dependência, JSX e Virtual DOM. É preciso avaliar cada afirmação sem cair nas inversões clássicas.

**Palavra-chave:** React = biblioteca; Angular = framework completo + TypeScript + DI; Vue = framework progressivo; JSX = extensão sintática do JavaScript (não é HTML); Virtual DOM = técnica de React e Vue

**Conceito:**
- **Afirmativa I é verdadeira.** O **React é uma biblioteca** (não framework): ele entrega componentes de interface, mas o roteamento (React Router), estado global (Context API/Redux) e demais estruturas vêm de bibliotecas complementares. O Angular e o Vue, quando usados como framework, mantêm o controle do fluxo (IoC) e definem a estrutura da aplicação.
- **Afirmativa II é verdadeira.** O **Angular** é um framework completo e "opiniado", exige **TypeScript** e possui **Injeção de Dependência nativa** (`@Injectable`, construtor) — conceitualmente a mesma técnica do `@Service`/`@Autowired` do Spring. É o único dos três com sistema de DI nativo nesse sentido.
- **Afirmativa III é falsa.** O **JSX é uma extensão sintática do JavaScript** que "parece" HTML, mas é JavaScript — usa `className` (não `class`), `htmlFor` (não `for`), e é compilado para `React.createElement()`. Dizer que "é HTML dentro de JavaScript" é uma simplificação incorreta. Além disso, o motivo de o React ser biblioteca **não** é o JSX — é o fato de não definir a estrutura da aplicação como um todo.
- **Afirmativa IV é verdadeira.** O **Virtual DOM** é uma técnica (representação leve da árvore DOM em memória com diffing e atualização seletiva) usada tanto pelo **React** quanto pelo **Vue**. O Angular usa Change Detection com Zone.js, uma abordagem diferente. Não é exclusividade do React.

**Análise das alternativas:**
- **A (I e II):** errada — não inclui IV (verdadeira).
- **B (II e IV):** errada — não inclui I (verdadeira).
- **C (I, II e IV):** correta.
- **D (I e III):** errada — inclui III (falsa) e exclui II e IV (verdadeiras).
- **E (III e IV):** errada — inclui III (falsa).

**Pegadinha:** A alternativa III condensa duas armadilhas: (1) **JSX não é HTML** — é extensão sintática de JavaScript; (2) a razão de o React ser biblioteca é a não definição da estrutura da aplicação, não o JSX. A alternativa II conecta a Injeção de Dependência do Angular com o Spring, uma ponte que a FGV explora (DI é nativa só no Angular; React usa Context, que não é DI). E a IV derruba o mito de que Virtual DOM é exclusivo do React — **Vue também usa**.

---

## Questão 03 — Arquiteturas de Apresentação (SPA, PWA, SSR/CSR)

**id:** FRONT-003
**disciplina:** Tecnologias e Práticas Frontend Web
**tópico:** Arquiteturas de Apresentação
**subtópico:** SPA vs. MPA vs. PWA; SSR vs. CSR (quem renderiza); Service Worker e manifest
**origem:** autoral
**habilidade cognitiva:** análise
**dificuldade:** média
**conhecimento avaliado:** SPA = arquitetura (uma página); PWA = tecnologia de capacidades nativas (Service Worker, manifest, HTTPS); CSR/SSR = modelo de renderização; distinção SPA ≠ CSR e SSR ≠ MPA

A DATAPREV está decidindo a arquitetura de apresentação de um novo portal de serviços. Considere as afirmativas abaixo:

I. Em uma SPA, o navegador recarrega a página inteira a cada navegação, pois cada mudança de rota corresponde a uma nova requisição de HTML completo ao servidor.

II. O Service Worker é um script que roda em segundo plano, separado da página, e atua como intermediário de rede — permitindo o funcionamento offline por meio do uso de cache.

III. CSR (Client-Side Rendering) é o nome da arquitetura em que a aplicação possui uma única página; já a expressão SSR (Server-Side Rendering) designa uma aplicação com múltiplas páginas.

IV. Uma SPA pode, em determinados cenários, utilizar SSR — pois SPA diz respeito à estrutura da aplicação (uma página), enquanto SSR diz respeito a quem monta o HTML (o servidor). São conceitos de camadas diferentes e podem se combinar.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I e II
B) II e IV
C) I, III e IV
D) II e III
E) Apenas II

---

**Gabarito:** B

### Comentário

**Raciocínio:** A questão pede distinguir três conceitos de camadas diferentes: SPA (arquitetura), PWA (capacidades) e SSR/CSR (renderização). Cada afirmação testa uma das pegadinhas clássicas da FGV.

**Palavra-chave:** SPA = uma página, JS intercepta o clique (sem recarregar); PWA = Service Worker + manifest + HTTPS (offline/instalável); CSR = cliente monta; SSR = servidor monta; SPA ≠ CSR; SSR ≠ MPA

**Conceito:**
- **Afirmativa I é falsa.** Em uma **SPA**, a navegação **não recarrega a página inteira**. O navegador carrega um único `index.html` + JS e, ao clicar em um link, o **JavaScript intercepta** o clique, busca os dados via fetch/Ajax e atualiza **apenas a parte modificada**. O que faz esse recarregamento é a **MPA (Multi-Page Application)**, em que cada navegação pede um HTML completo ao servidor.
- **Afirmativa II é verdadeira.** O **Service Worker** é um script JavaScript que roda **em segundo plano**, separado da página, atuando como **proxy de rede** — intercepta requisições, armazena respostas em cache e pode **servir conteúdo offline**. É um dos pilares da PWA (junto com o manifest e o HTTPS).
- **Afirmativa III é falsa.** **CSR não é arquitetura de uma página** — é um **modelo de renderização**: o navegador (cliente) monta o HTML via JavaScript. E **SSR não significa múltiplas páginas** — é o modelo em que o **servidor** monta o HTML completo. A afirmação troca os planos: SPA/MPA é sobre estrutura; CSR/SSR é sobre renderização.
- **Afirmativa IV é verdadeira.** SPA (arquitetura) e SSR (renderização) são **conceitos de camadas diferentes** e **podem se combinar** — por exemplo, frameworks híbridos (Next.js para React, Nuxt.js para Vue, Angular Universal) renderizam no servidor uma aplicação de página única. Derivado normal disso: **CSR não é sinônimo de SPA**, nem **SSR de MPA**.

**Análise das alternativas:**
- **A (I e II):** errada — inclui I (falsa).
- **B (II e IV):** correta.
- **C (I, III e IV):** errada — inclui I e III (falsas).
- **D (II e III):** errada — inclui III (falsa).
- **E (Apenas II):** errada — IV também é verdadeira.

**Pegadinha:** Esta questão condensa as três trocas mais rentáveis do bloco: (1) **SPA = recarrega a página** (é o contrário — a SPA não recarrega); (2) **CSR = arquitetura de uma página** e **SSR = múltiplas páginas** (na verdade é sobre *quem renderiza*, não sobre *quantas páginas*); (3) tratar SPA e CSR como sinônimos. Guarde o recurso mnemônico da nota: **SPA = "uma página" (estrutura)** · **PWA = "app web" (capacidades)** · **CSR/SSR = "quem pinta" (renderização)**.

---

## Questão 04 — UX Básica (Heurísticas de Nielsen)

**id:** FRONT-004
**disciplina:** Tecnologias e Práticas Frontend Web
**tópico:** Fundamentos Web / UX
**subtópico:** Heurísticas de Nielsen (conceito, reconhecimento de qual heurística foi violada em cenário)
**origem:** autoral
**habilidade cognitiva:** compreensão e aplicação (reconhecer violação)
**dificuldade:** fácil-média
**conhecimento avaliado:** aplicar as heurísticas de Nielsen a um cenário de uso; distinguir status do sistema (1), prevenção de erros (5) e ajuda/reconhecimento de erros (9)

Durante a avaliação de usabilidade de um formulário de requerimento de benefícios da DATAPREV, foram observados os seguintes problemas:

1. Ao enviar o formulário, o cidadão não recebe nenhuma indicação se o envio foi concluído ou se ainda está em andamento.
2. O formulário não possui nenhuma orientação para corrigir um campo preenchido incorretamente — o sistema apenas rejeita o envio com a mensagem genérica "Erro interno".

Considerando as Heurísticas de Nielsen, os problemas **1** e **2** violam, respectivamente, as heurísticas:

A) Prevenção de erros e Estética e design minimalista
B) Status do sistema e Ajuda para reconhecer, diagnosticar e recuperar de erros
C) Reconhecimento em vez de memória e Consistência e padrões
D) Status do sistema e Prevenção de erros
E) Flexibilidade e eficiência de uso e Ajuda e documentação

---

**Gabarito:** B

### Comentário

**Raciocínio:** A questão descreve dois cenários e pede para identificar qual heurística de Nielsen foi violada. A chave é ler cada heurística como uma pergunta e ver se o cenário responde "não".

**Palavra-chave:** heurística 1 = status do sistema (informar o que está acontecendo); heurística 9 = ajudar a reconhecer, diagnosticar e recuperar de erros (mensagem clara); heurística 5 = prevenção de erros (evitar antes); heurística 3 = controle e liberdade (desfazer)

**Conceito:**
- **Problema 1 — Status do sistema (Heurística 1).** O usuário não sabe se o envio foi concluído ou está em andamento. Essa heurística exige que o **sistema sempre informe o que está acontecendo** (ex.: barra de progresso, confirmação "requerimento enviado com sucesso"). Como o sistema não informa o andamento, viola a **Heurística 1**.
- **Problema 2 — Ajuda para reconhecer, diagnosticar e recuperar de erros (Heurística 9).** O formulário rejeita o envio com uma mensagem genérica ("Erro interno") sem dizer o que há de errado nem como corrigir. Essa heurística exige **mensagens de erro claras e acionáveis** (ex.: "CPF inválido — digite apenas números"). Como a mensagem não ajuda a diagnosticar nem a recuperar, viola a **Heurística 9**.

**Análise das alternativas:**
- **A (Prevenção de erros / Estética e design minimalista):** errada — não há, nos cenários, foco em evitar que o erro ocorra (5) nem em minimalismo (8).
- **B (Status do sistema / Ajuda para reconhecer, diagnosticar e recuperar de erros):** correta.
- **C (Reconhecimento em vez de memória / Consistência e padrões):** errada — os cenários não envolvem exigir lembrança de opções (6) nem padrões inconsistentes (4).
- **D (Status do sistema / Prevenção de erros):** errada — para o problema 2, o foco é **recuperar do erro com mensagem clara** (9), não **evitar/prevenir** (5). O erro já ocorreu.
- **E (Flexibilidade e eficiência / Ajuda e documentação):** errada — o problema 2 é sobre a **mensagem de erro**, não sobre atalhos para avançados (7) nem acesso a documentação de ajuda (10).

**Pegadinha:** A alternativa **D** é a armadilha mais rentável — ela troca a **Heurística 9** (ajudar a **recuperar** do erro com mensagem clara) pela **Heurística 5** (prevenção de erros). A diferença é crucial: a **prevenção (5)** age **antes** do erro (desabilitar botão enquanto dados inválidos); a **recuperação (9)** age **depois** (mensagem clara explicando o erro e como corrigir). Aqui o erro já aconteceu ("rejeita o envio"), então é a **9**, não a 5. Regra prática da nota: informar o **andamento** → 1; **evitar** o erro → 5; **mensagem clara após** o erro → 9.

---

## Padrões de cobrança utilizados

As questões autorais acima foram inspiradas nos seguintes padrões de cobrança identificados nas questões reais FGV e nas observações do `padroes-gerais-fgv.md`:

1. **Formato de julgamento de afirmativas (V/F) sobre conceitos com inversões sutis** — formato FGV clássico: múltiplas afirmações com uma ou duas falsas escondidas em trocas de definição. Inspiração para Q01, Q02 e Q03.
2. **Troca de definições / categorias** (observação FGV recorrente, `padroes-gerais-fgv.md`): o padrão mais eficiente da banca é inverter pares conceituais — Flexbox/Grid, biblioteca/framework, SPA/CSR, status do sistema/prevenção de erros. Inspirado em todas as questões.
3. **Cenário prático e "qual foi violado?"** (padrão FGV em UX, indicado nas notas Fundamentos-Web e Conceitos-de-UX): a banca descreve um cenário e pede para reconhecer a heurística de Nielsen violada. Inspiração para Q04.
4. **Conceito aplicado a um sistema público** (contextualização FGV, `padroes-gerais-fgv.md` — enunciados contextualizados): todos os cenários foram situados em um contexto de portal de benefícios, seguindo a prática da banca de não cobrar decoreba puro.
5. **Conexão entre blocos** (nota Frameworks-Frontend): a Injeção de Dependência do Angular foi comparada ao Spring (DI nativa), ponte que a banca explora para testar integração de conhecimento — inspiração para Q02.
6. **Orientação das observações pedagógicas da ementa** (Fase 5.1): "a prova cobra as diferenças conceituais e não detalhes de API" — todas as questões mantêm foco conceitual, sem APIs internas de frameworks.

> **Nota de categoria:** todas as questões são **autorais**, inspiradas em padrões de cobrança, mas **não são** questões oficiais de banca e **não reproduzem** itens reais.