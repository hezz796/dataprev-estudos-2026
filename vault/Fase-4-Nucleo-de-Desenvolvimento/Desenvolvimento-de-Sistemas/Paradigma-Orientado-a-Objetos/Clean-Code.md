# Clean Code — Código Limpo

> [!info] Metadados
> **Disciplina:** Desenvolvimento de Sistemas
> **Bloco:** 4.1 — Desenvolvimento de Sistemas (FASE 4 — Núcleo de Desenvolvimento)
> **Tópico:** 2. Paradigma Orientado a Objetos — Clean Code
> **Subtópicos:** Clean Code (nomes significativos, funções pequenas, comentários úteis)
> **Pré-requisitos:** [[Classe-e-Objeto]] e [[Quatro-Pilares-do-POO]] (encapsulamento, métodos, classes) e [[Java-Fundamentos-da-Linguagem|Java — Fundamentos da Linguagem]] (sintaxe)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-09-17

---

## 1. Por que estudar Clean Code?

O edital da DATAPREV cobra Clean Code de forma conceitual — a FGV não pede que você decore a biografia de Robert C. Martin, mas sim que entenda **por que** certas práticas de escrita de código tornam um sistema mais legível, manutenível e robusto. A pergunta subjacente é: *o que diferencia código profissional de código amador?*

A resposta começa com um fato simples: **código é lido muito mais vezes do que é escrito**. Um desenvolvedor dedica, em média, muito mais tempo entendendo código existente (seu ou de colegas) do que escrevendo código novo. Em um contexto como o da DATAPREV — onde sistemas legados de seguridade social possuem dezenas de milhares de linhas, são mantidos por múltiplas equipes ao longo de anos e passam por constantes manutenções e atualizações regulatórias — essa realidade se amplifica. Código difícil de ler vira custo: cada nova funcionalidade leva mais tempo, cada correção de bug arrisca quebrar algo em outro lugar, e cada novo integrante da equipe precisa de dias para "decifrar" o que o código anterior faz.

Clean Code é o conjunto de **princípios e práticas** que tornam o código **fácil de ler, fácil de modificar e fácil de confiar**. Não é uma norma oficial nem um padrão ISO — é um conjunto de orientações consagradas pela comunidade de desenvolvimento de software, aplicáveis a qualquer linguagem, mas particularmente relevantes em ecossistemas como o Java corporativo que a DATAPREV utiliza.

> [!question] Pergunta orientadora
> Se você herda um sistema de cálculo de benefícios previdenciários com 50 mil linhas de código e nenhum comentário, sem nomes descritivos e com funções que fazem dez coisas ao mesmo tempo — quanto tempo levaria para entender apenas o fluxo de cálculo de um benefício? E se o código fosse escrito com nomes claros, funções pequenas e bem delimitadas? A diferença entre os dois cenários é, em grande parte, a diferença entre código que ignora e código que segue os princípios de Clean Code.

---

## 2. Nomes significativos

### 2.1 A regra central: nomes devem revelar a intenção

O primeiro e mais fundamental princípio de Clean Code é que **nomes devem dizer o que representam**. Um nome bom dispensa comentários explicativos — quem lê o código entende o propósito sem precisar de uma anotação externa. Pense nisso como uma "autoexplicação": se o nome de uma variável ou método não deixa claro o que ela contém ou faz, o código falhou na comunicação.

O raciocínio é direto: se o código precisa de um comentário para explicar o que uma variável significa, o nome está ruim. Se o nome estivesse bom, o comentário seria desnecessário. É por isso que, nos exemplos abaixo, o código BOM **dispensa** qualquer explicação externa:

```java
// RUIM — nomes enigmáticos
int d;             // o que é d? dias?
double v;          // valor? de quê?

// BOM — nomes revelam a intenção
int diasDesdeUltimaConsulta;
double limiteDeMargemConsignavel;
```

Repare como `d` e `v` dizem absolutamente nada sobre o que representam. `diasDesdeUltimaConsulta` e `limiteDeMargemConsignavel`, por outro lado, comunicam exatamente o significado — qualquer desenvolvedor que leia esse código entende imediatamente o que cada variável guarda.

### 2.2 Regras de nomeação que a banca cobra

A FGV costuma cobrar Clean Code por asserções verdadeiras/falsas, o que torna importante conhecer as regras de nomeação com precisão:

**Métodos devem ser verbos.** Um método representa uma *ação*, então seu nome deve começar com um verbo que descreva essa ação. `calcularSalario()`, `emitirExtrato()`, `validarCpf()`, `processarBeneficio()` — todos são nomes claros porque descrevem o que o método *faz*. O nome do método já diz ao leitor o que esperar antes mesmo de ler o corpo da função.

**Classes devem ser substantivos.** Uma classe representa uma *coisa* (um molde, como você viu em [[Classe-e-Objeto]]), então seu nome deve ser um substantivo. `Beneficiario`, `EmprestimoConsignado`, `CalculoBeneficio` — todos nomeiam *o que a classe representa*, não *o que ela faz*. O que ela faz ficará nos métodos.

**Evite abreviações obscuras.** `calcSal()` pode parecer mais curto que `calcularSalario()`, mas quem lê pela primeira vez precisa adivinhar o que "calc" e "Sal" significam. Abreviações como `d`, `v`, `tmp`, `aux` são especialmente perigosas porque são ambíguas — `tmp` para quê? `aux` auxilia o quê? O custo de digitar mais alguns caracteres é infinitamente menor do que o custo de um bug causado por má compreensão.

**Use camelCase com consistência.** Em Java, a convenção para variáveis e métodos é `camelCase` (primeira palavra em minúscula, subsequentes com inicial maiúscula): `diasDesdeUltimaConsulta`, `calcularValorBeneficio()`. Para classes, `PascalCase` (cada palavra com inicial maiúscula): `Beneficiario`, `EmprestimoConsignado`. Essa convenção é parte do vocabulário técnico que aparece também na nota de [[Estrutura-Morfossintatica|Português]] quando se estuda terminologia de programação — e a banca pode testar se você conhece a convenção correta.

> [!warning] PEGADINHA — "nomes curtos são sempre melhores"
> **A armadilha:** a banca propõe que "nomes curtos são preferíveis a nomes longos porque reduzem a complexidade do código".
> **O raciocínio errado:** concordar que `x` é melhor que `diasDesdeUltimaConsulta` porque tem menos letras.
> **Como se proteger:** nomes **curtos** não são necessariamente **bons**. O critério é **significatividade**, não tamanho. `diasDesdeUltimaConsulta` é longo, mas diz exatamente o que é. `x` é curto, mas não diz nada. O nome ideal é **curto o suficiente para ser digitável e longo o suficiente para ser compreensível**. Se um nome preciso exige mais caracteres, use-os — a legibilidade vale mais que a economia de teclas.

### 2.3 Conectando com os pilares do POO

Nomes significativos não são apenas estética — eles se conectam com os conceitos de [[Quatro-Pilares-do-POO|encapsulamento e abstração]] que você já estudou. Quando uma classe se chama `Beneficiario` e tem um método `calcularMargemConsignavel()`, o nome já **abstrai** (modela só o essencial) e **encapsula** a intenção: quem usa sabe o que esperar sem precisar olhar o código interno. Nomes ruins quebram a promessa do encapsulamento — se `b1.proc()` significa "processar benefício do beneficiário" ou "calcular prazo de carência", o leitor fica perdido.

---

## 3. Funções pequenas

### 3.1 Uma função, uma coisa

O segundo princípio de Clean Code defende que **uma função deve fazer uma única coisa, e bem feita**. Funções gigantes que realizam dez operações diferentes são difíceis de entender (o leitor precisa manter múltiplas ideias na cabeça ao mesmo tempo), difíceis de testar (como testar isoladamente a validação se ela está misturada com o cálculo e com o envio de e-mail?) e difíceis de reutilizar (se você precisa apenas do cálculo, precisa copiar ou extrair toda a função).

O indicador prático é este: **se você precisa de um comentário para explicar o que uma parte da função faz, essa parte provavelmente deveria ser extraída para outra função**. Isso se chama **refatoração** — reestruturar o código sem alterar seu comportamento externo. Refatoração será aprofundada em notas de metodologias ágeis; aqui, basta entender o conceito como o mecanismo pelo qual funções grandes viram funções pequenas.

### 3.2 O exemplo da nota-fonte

Veja o contraste entre uma função que faz várias coisas e a mesma lógica decomposta:

```java
// RUIM — função que faz várias coisas
public void processarBeneficio(Beneficiario b) {
    // valida
    if (b.getCpf() == null) throw new IllegalArgumentException();
    // calcula
    double valor = b.getRendaMensal() * 0.30;
    // formata e envia
    String msg = "Seu benefício é " + formatar(valor);
    enviarEmail(b.getEmail(), msg);
}

// MELHOR — uma função, uma responsabilidade
public void processarBeneficio(Beneficiario b) {
    validar(b);
    double valor = calcularValor(b);
    notificar(b, valor);
}
```

Na versão ruim, o método `processarBeneficio` faz **três coisas**: valida o CPF, calcula o valor e envia o e-mail. Se amanhã a regra de validação mudar, o desenvolvedor precisa mexer nessa mesma função que também calcula e envia — risco de quebrar o que não deveria ser tocado. Se alguém precisar reaproveitar apenas o cálculo, não pode — o cálculo está "preso" dentro de uma função que também valida e notifica.

Na versão melhor, cada operação está isolada em sua própria função. `validar(b)` faz uma coisa: valida. `calcularValor(b)` faz uma coisa: calcula. `notificar(b, valor)` faz uma coisa: notifica. Se a validação mudar, você mexe só em `validar`. Se alguém precisar reaproveitar o cálculo em outro contexto, basta chamar `calcularValor` diretamente. As funções pequenas também comunicam a **estrutura** do código: basta ler `processarBeneficio` para entender o fluxo (validar, calcular, notificar) sem precisar ler o corpo de cada passo.

> [!question] Como identificar que uma função precisa ser dividida?
> Pergunte a si mesmo: esta função faz mais de uma coisa? Se sim, divida. Uma técnica simples: se você consegue colocar um "e" entre as operações da função ("valida **e** calcula **e** notifica"), são múltiplas responsabilidades. Se a função faz apenas uma coisa ("calcula"), ela está coesa.

### 3.3 Coesão: o conceito que conecta tudo

Funções pequenas estão relacionadas ao conceito de **coesão** — que também aparece como palavra-chave na cobrança da FGV sobre Clean Code. Coesão é o grau em que os elementos de uma unidade de código (classe ou função) estão relacionados entre si e convergem para um único propósito. Uma função coesa faz uma coisa só; uma classe coesa reúne atributos e métodos que juntos representam uma única responsabilidade. Coesão é o antônimo de "fazer tudo no mesmo lugar".

---

## 4. Comentários úteis

### 4.1 O princípio: código bem nomeado dispensa comentários

O terceiro pilar de Clean Code diz que o **código bem nomeado não precisa de comentários explicativos** — o código deve se explicar sozinho. Se uma variável se chama `diasDesdeUltimaConsulta`, não faz sentido colocar um comentário `// dias que passaram desde a última consulta do usuário`. O nome já diz isso.

```java
// RUIM — comenta o óbvio (o código já diz isso)
int x = 0;      // seta x para zero

// ÚTIL — explica o "porquê", que o código não revela
// Margem consignável de 30% conforme Resolução INSS nº 100/2021
final double MARGEM_CONSIGNAVEL = 0.30;
```

O primeiro caso é inútil: `// seta x para zero` não agrega informação ao código, porque `x = 0` já comunica isso. O segundo caso é útil: o valor `0.30` sozinho não revela de onde veio — o comentário explica a **origem normativa** (Resolução INSS), informação que o código não carrega.

### 4.2 Quando o comentário é útil

Comentários úteis explicam o **porquê**, não o **o quê**. Existe uma distinção fundamental:

- **Comentário inútil (o quê):** repete em palavras o que o código já diz. `i++ // incrementa i`. `return resultado; // retorna o resultado`. São comentários que ocupam espaço sem agregar informação.

- **Comentário útil (porquê):** explica uma decisão de negócio, um número mágico, uma limitação técnica ou o contexto de um trecho complexo. São comentários que **não poderiam ser expressos** apenas pelo nome de variáveis ou funções.

Os cenários mais comuns onde comentários são úteis são:

**Regras de negócio com fundamento normativo.** O código precisa calcular a margem consignável em 30%, mas de onde vem esse 30%? Vem de uma Resolução do INSS. O comentário documenta a **fonte da regra** — algo que o nome da variável ou o valor numérico não transmitem.

**Números mágicos.** Um `0.30` solto no meio de uma expressão de cálculo levanta a pergunta: "de onde veio esse valor?". Sem o comentário, o leitor precisa ir atrás da documentação ou da legislação para entender. Com o comentário, o contexto está ali.

**Decisões de design.** Por que esta classe não herda de outra, mesmo que a relação pareça "é-um"? Por que este método lança exceção em vez de retornar null? Comentários de design documentam as **razões por trás das decisões** — o "porquê" arquitetural.

### 4.3 A pegadinha que a FGV adora

> [!warning] PEGADINHA — o que Clean Code diz sobre comentários
> **A armadilha:** a banca pergunta: "o Clean Code recomenda eliminar todos os comentários do código?"
> **O raciocínio errado:** concordar, porque "Clean Code prega que o código se explica sozinho".
> **Como se proteger:** **não.** Clean Code **não** recomenda eliminar todos os comentários. Ele recomenda que os **comentários dispensáveis** (os que repetem o código ou explicam o óbvio) sejam removidos, e que o código seja **expressivo o bastante para reduzir** a dependência de comentários. Comentários que explicam **regras de negócio**, **origens normativas** ou **decisões de design** são bem-vindos. A pegadinha consiste em transformar a recomendação (remover o dispensável) em proibição absoluta (remover todos). Se a banca oferece "Clean Code elimina todos os comentários" como alternativa, ela está errada.

---

## 5. Como a FGV cobra este tópico

### 5.1 Palavras-chave e expressões de referência

| Palavra-chave / Expressão | O que sinaliza |
|---|---|
| **Clean Code / código limpo** | Questão conceitual sobre princípios gerais |
| **Nomes significativos** | Princípio de que nomes devem revelar intenção |
| **Funções pequenas** | Princípio de uma função, uma responsabilidade |
| **Comentários úteis** | Comentários que explicam o "porquê", não o "como" óbvio |
| **Refatoração** | Reestruturar código sem alterar comportamento externo |
| **Intenção** | Nome que comunica propósito (intenção do autor) |
| **Coesão** | Grau de relacionamento entre elementos de uma unidade de código |
| **Código limpo** | Sinônimo de Clean Code — não é conceito diferente |

### 5.2 O padrão "armadilha → raciocínio errado → proteção"

> [!warning] Pegadinha 1 — "Clean Code elimina todos os comentários"
> **A armadilha:** alternativa que diz que "Clean Code determina que nenhum comentário deve existir no código-fonte".
> **O raciocínio errado:** aceitar porque "o código se autoexplica com nomes e funções pequenas".
> **Como se proteger:** Clean Code elimina comentários **dispensáveis**, não todos. Comentários de regra de negócio e decisão de design são úteis e bem-vindos. A pegadinha transforma recomendação em proibição absoluta.

> [!warning] Pegadinha 2 — "funções pequenas significam funções que retornam valor único"
> **A armadilha:** alternativa que define funções pequenas como "funções que retornam apenas um valor".
> **O raciocínio errado:** confundir "uma única responsabilidade" com "um único retorno".
> **Como se proteger:** "função pequena" significa **uma única responsabilidade** (faz uma coisa só), não necessariamente que retorna um único valor. Uma função pode ter vários caminhos de retorno e ainda assim ser coesa, desde que todas as rotas estejam ligadas à mesma responsabilidade.

> [!warning] Pegadinha 3 — "nomes curtos são sempre preferíveis"
> **A armadilha:** alternativa que diz que "nomes curtos são sempre superiores a nomes longos em Clean Code".
> **O raciocínio errado:** achar que concisão é o mesmo que significatividade.
> **Como se proteger:** o critério é **significatividade**, não tamanho. `x` é curto mas nada diz. `diasDesdeUltimaConsulta` é longo mas comunica exatamente o propósito. Nomes são sobre **clareza**, não sobre comprimento.

> [!warning] Pegadinha 4 — "Clean Code se aplica apenas a Java"
> **A armadilha:** afirmar que Clean Code é exclusivo de uma linguagem ou paradigma.
> **O raciocínio errado:** assumir que, como o edital cobra Java, Clean Code só vale para Java.
> **Como se proteger:** Clean Code é um conjunto de princípios **genéricos** de escrita de código, aplicáveis a qualquer linguagem e paradigma. A FGV cobra o conceito, não a implementação em uma linguagem específica.

---

## 6. Questões-modelo (pegada FGV)

> [!example] Questão 1
> Considere o trecho de código abaixo:
> ```java
> public void proc(Beneficiario b) {
>     // valida CPF
>     if (b.getCpf() == null) throw new IllegalArgumentException();
>     // calcula valor
>     double v = b.getRendaMensal() * 0.30;
>     // envia email
>     String m = "Benefício: " + v;
>     enviarEmail(b.getEmail(), m);
> }
> ```
> De acordo com os princípios de Clean Code, quais problemas estão presentes nesse código?
>
> **(A)** O código não utiliza generics e, portanto, não oferece segurança de tipos.
> **(B)** Os nomes das variáveis e do método não revelam a intenção, e a função faz mais de uma coisa.
> **(C)** O código viola o princípio da substituição de Liskov por não usar herança.
> **(D)** O uso de literais numéricos (0.30) é proibido por Clean Code em qualquer circunstância.
> **(E)** O método deveria ser abstrato, pois representa uma operação conceitual.

> [!note] Gabarito e comentário — Questão 1
> **Resposta: (B)**
> O método `proc` tem nome enigmático (não revela intenção), as variáveis `v` e `m` são abreviações obscuras, e o método faz três coisas distintas: valida, calcula e envia. Essas violações correspondem aos dois primeiros pilares de Clean Code (nomes significativos e funções pequenas). A alternativa (A) é irrelevante — generics não têm a ver com Clean Code nesse contexto. (C) é incorreta — não há herança violada aqui. (D) é incorreta — o literal `0.30` seria aceitável se tivesse um nome constante descritivo (como `MARGEM_CONSIGNAVEL`), mas o problema não é o literal em si, e sim a falta de nome significativo. (E) é incorreta — não há relação com abstração nesse contexto.

> [!example] Questão 2
> Qual das afirmativas abaixo está **CORRETA** sobre o princípio de comentários úteis no Clean Code?
>
> **(A)** Clean Code determina que todos os comentários devem ser removidos do código-fonte.
> **(B)** Comentários que explicam regras de negócio e decisões de design são úteis e devem ser mantidos.
> **(C)** Comentários explicativos são sempre preferíveis a nomes descritivos de variáveis.
> **(D)** O uso de comentários substitui a necessidade de nomes significativos em métodos.
> **(E)** Comentários só são úteis quando documentam APIs públicas, não código interno.

> [!note] Gabarito e comentário — Questão 2
> **Resposta: (B)**
> Comentários que documentam regras de negócio (como "margem de 30% conforme Resolução INSS") ou decisões de design são exatamente o tipo de comentário que Clean Code considera útil. A alternativa (A) é a pegadinha clássica — Clean Code não proíbe todos os comentários, apenas os dispensáveis. (C) inverte a recomendação: nomes significativos devem *reduzir* a necessidade de comentários, não o contrário. (D) é a mesma inversão: comentários e nomes bons se complementam, não se substituem. (E) é restritiva demais — comentários internos de regra de negócio são igualmente úteis.

---

## 7. Revisão rápida

| Conceito | Ponto-chave | Erro mais comum em prova |
|---|---|---|
| **Nomes significativos** | Nomes devem revelar intenção; método = verbo, classe = substantivo | Confundir "curto" com "significativo" |
| **Funções pequenas** | Uma função, uma responsabilidade; indicador: precisa de comentário = divida | Confundir com "função que retorna valor único" |
| **Comentários úteis** | Explicam o "porquê" (regra de negócio, número mágico, decisão de design) | Achar que Clean Code proíbe todos os comentários |
| **Refatoração** | Reestruturar código sem alterar comportamento externo | Confundir com reescrita completa |
| **Coesão** | Elementos de uma unidade convergem para um único propósito | Confundir com acoplamento |
| **Clean Code** | Princípios genéricos de escrita de código, não exclusivos de Java | Achar que é restrito a uma linguagem |

> [!tip] Resumo em uma frase
> Clean Code é sobre escrever código que outro ser humano (ou você mesmo daqui a seis meses) consiga **entender, confiar e modificar** com segurança — e a FGV cobra se você sabe distinguir os princípios reais das distorções da banca.

---

## 8. Próximos passos

Os princípios de Clean Code que você acabou de estudar são, na prática, **orientações manuais** para escrever código limpo. Mas como garantir que um time inteiro, com dezenas de milhares de linhas de código, realmente segue esses princípios? A resposta é a **análise estática de código** — ferramentas que verificam automaticamente se o código atende a essas práticas, sem precisar executá-lo. Você verá isso na subnota seguinte: [[Analise-Estatica-e-SonarQube]].

Já os princípios de **design orientado a objetos** — coesão, baixo acoplamento, responsabilidade única — são o aprofundamento natural de Clean Code em escala de classes e arquitetura. O próximo bloco de estudo nessa trilha é o [[Principios-SOLID]], que formaliza esses princípios em cinco regras concretas.

Consulte sempre o [[Paradigma-Orientado-a-Objetos|índice do tópico 2]] para navegar entre as subnotas e revisar qualquer conceito antes de avançar.