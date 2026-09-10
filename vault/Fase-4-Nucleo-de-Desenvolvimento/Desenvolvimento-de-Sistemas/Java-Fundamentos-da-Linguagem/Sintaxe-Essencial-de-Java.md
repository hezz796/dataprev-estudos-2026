# Sintaxe Essencial de Java

> [!info] Metadados
> **Disciplina:** Desenvolvimento de Sistemas
> **Bloco:** 4.1 — Desenvolvimento de Sistemas (FASE 4 — Núcleo de Desenvolvimento)
> **Tópico:** 1. Java — Fundamentos da Linguagem — Sintaxe essencial
> **Subtópicos:** Estrutura de um programa (a classe como recipiente: `class`, `main`, campos) · Variáveis · Operadores · Controle de fluxo (if/else, for, while) · Entrada/saída básica
> **Pré-requisitos:** [[Raciocinio-Matematico-Aplicado|Raciocínio Lógico Matemático]] (lógica de programação) e [[SQL-DDL-e-DML|SQL/Banco de Dados]] (estruturas de dados e consultas) — SEM POO
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-09-09

---

## 1. Por que estudar a sintaxe essencial?

Esta nota é o primeiro tijolo da sequência de programação da Fase 4. Ela parte exatamente de onde você já chegou: na Fase 3, você modelou e consultou dados — um `Beneficiario` virou uma linha na tabela `beneficiario`, e o SQL trouxe essa linha de volta com filtros como `WHERE idade >= 18 AND renda_mensal > 0`; na Fase 1, você treinou a lógica que decide e repete, com condicionais e tabelas-verdade. Agora vem o ponto de encontro: **escrever um programa Java que pega esses dados, decide caminhos e repete operações** — o mesmo raciocínio do RLM e a mesma disciplina de dados do SQL, agora em código executável.

No contexto DATAPREV, isso é concreto: a empresa processa dados da seguridade social — o **CNIS**, o INSS digital, os sistemas de **benefícios** e de **consignação** — e o analista escreve código que guarda o valor de um benefício em uma variável, compara a renda do beneficiário com um limite, decide se a margem consignável permite o desconto e repete o processamento para milhares de registros. Tudo isso é a **sintaxe** da linguagem. Um aviso importante antes de começar: o foco aqui é a **forma** da língua. Você vai escrever a classe como recipiente do código — a forma `class` com seus campos — porque todo programa Java precisa dela para dar estrutura ao código. Mas o *porquê* do paradigma orientado a objetos e o comportamento do objeto (o `new`, o construtor, o `this`, os métodos) é o **tópico 2**, a nota [[Paradigma-Orientado-a-Objetos]]. Nesta subnota, a classe é ferramenta; na próxima, ela vira filosofia de design.

> [!question] Pergunta orientadora
> Você já sabe filtrar linhas com `WHERE` e combinar condições com `AND`, `OR`, `NOT` no SQL — e sabe que "se chover, levo guarda-chuva" é uma condicional do RLM. O que falta para transformar essa lógica em um programa que a DATAPREV executa milhões de vezes por dia? Falta a **sintaxe** — as regras da língua Java. É exatamente isso que esta nota constrói.

---

## 2. Estrutura de um programa: o ponto de entrada

Um programa Java não executa sozinho: ele precisa de um **ponto de entrada** — o lugar exato onde a máquina virtual (a JVM, que roda o código) começa a executar instruções. Em Java esse ponto é sempre o mesmo, com o mesmo nome — e a FGV já pediu o nome literalmente:

```java
public class MeuPrograma {
    public static void main(String[] args) {
        System.out.println("Olá, DATAPREV!");
    }
}
```

Repare na organização: todo código vive dentro de uma **classe** — por enquanto, trate-a como o "arquivo organizador" do código; o significado profundo das classes (por que existem, como se relacionam) é assunto do tópico 2. Dentro da classe, o método `main` é o ponto de entrada, e cada palavra tem um papel — as bancas gostam de explorar cada uma:

- `public` — o método pode ser acessado de fora da classe (os modificadores de acesso serão detalhados no tópico 2; aqui, guarde apenas a ideia de "visível");
- `static` — o método pertence à **classe**, e não a um objeto; por isso a JVM consegue chamá-lo **sem criar nenhum objeto antes**;
- `void` — o método **não devolve nenhum valor**; ele executa e termina;
- `main` — o nome **obrigatório** do ponto de entrada; a JVM procura exatamente por esse nome;
- `String[] args` — os **parâmetros** recebidos da linha de comando (um conjunto de textos; a palavra `String` é uma **classe** do Java, não um tipo primitivo — detalhes em [[Tipos-Primitivos-e-Wrappers]]);
- cada instrução do corpo termina com `;` — o **ponto e vírgula encerra um comando**, e esquecê-lo é erro de compilação. E uma convenção que também cai em prova: o nome do **arquivo** deve ser igual ao nome da **classe pública** (`public class MeuPrograma` vive no arquivo `MeuPrograma.java`) — nome diferente gera erro de compilação.

Quanto à **forma da classe**, guarde três detalhes: a palavra-chave é `class`, **sempre em minúsculo**; o nome da classe segue o **PascalCase** (`MeuPrograma`, `Beneficiario`); e a classe pode guardar **campos** — variáveis declaradas dentro dela, com o tipo antes do nome, a mesma sintaxe de variável da Seção 3 (`String nome;`, `double rendaMensal;`). Além de campos, a classe costuma declarar **métodos** (o que ela sabe fazer) e um **construtor** (o que roda quando um objeto é criado). Essas partes e o objeto criado por `new` — como o `new Scanner(System.in)` da Seção 6 — pertencem ao **tópico 2 — [[Paradigma-Orientado-a-Objetos]]**; aqui basta reconhecer a forma.

> [!warning] PEGADINHA — o nome do ponto de entrada é fixo
> Se você renomear `main` para `start` ou `inicio`, o programa **compila** (é um método comum), mas **não executa**: a JVM procura por `public static void main(String[] args)` e não encontra. A banca gosta de apresentar um código sem `main` e perguntar o que acontece — a resposta correta é "não é um executável Java", muito mais do que "dá erro de compilação".

---

## 3. Declaração de variáveis: o tipo antes do nome

Uma **variável** é um espaço nomeado na memória que guarda um valor. O Java é uma linguagem **fortemente tipada**: antes de usar uma variável, você precisa declarar de que **tipo** ela é — e a ordem é sempre a mesma: **o tipo vem primeiro, depois o nome**, e opcionalmente um valor inicial:

```java
int idade = 32;
double salario = 4250.75;
boolean ativo = true;
String nome = "Maria";
```

Consegue ver a disciplina do SQL aqui? Na modelagem, cada coluna da tabela `beneficiario` tinha um tipo (`INTEGER`, `VARCHAR`, `NUMERIC`) definido no `CREATE TABLE`. No Java é a mesma ideia: `idade` tem que ser `int`; `salario`, um número com casas decimais (`double`); `ativo`, um `boolean` — o tipo **fixa** o que a variável pode guardar, e o compilador barra o uso errado. As regras que caem em prova: **o tipo vem antes do nome** (`int idade`, jamais `idade int`); o nome segue o padrão **camelCase** — `rendaMensal`, `cpf`, `dataNascimento`, `margemConsignavel`; Java é **sensível a maiúsculas** (`idade`, `Idade` e `IDADE` são três identificadores diferentes — declarar `int idade` e usar `Idade` é erro de compilação); e toda variável precisa ser **declarada antes de ser usada** — não existe "usar primeiro, declarar depois".

Faça um teste mental: `double 2salario = 5000;` compila? Não — **nenhum identificador pode começar com dígito**. O nome começa com letra, `_` ou `$` e não pode ser palavra reservada (`int`, `class`, `public`...) — pegadinha clássica de compilação.

---

## 4. Operadores: a máquina lógica do programa

Os operadores são a ponte direta entre a aritmética do [[Raciocinio-Matematico-Aplicado|RLM]] e a lógica das [[Logica-Sentencial|tabelas-verdade]]. Eles se organizam em quatro famílias.

### 4.1 Aritméticos

Os cinco operadores aritméticos são `+`, `-`, `*`, `/` e `%`. Os quatro primeiros você conhece do RLM; o quinto merece atenção especial:

$$7 \div 3 = 2 \text{ com resto } 1$$

O `%` devolve o **resto** da divisão inteira: `7 % 3` vale `1`; `10 % 2` vale `0` (dez dividido por dois não deixa resto). Em sistemas previdenciários, o `%` aparece sempre que a pergunta é "quanto sobra?": descobrir se um número é par, separar dígitos de um documento, paginar registros.

> [!warning] PEGADINHA — o `%` NÃO é porcentagem
> `100 % 5` não é "5% de 100". **`%` é resto de divisão** — o resto de `100 % 5` é `0`, porque 100 é divisível por 5. Para calcular porcentagem, você multiplica: o desconto é `valor * 0.05` ou `valor * (5 / 100.0)`. E repare no segundo formato: `5 / 100.0` usa um decimal justamente para não cair na pegadinha abaixo.

E há uma segunda armadilha dentro dos aritméticos: a **divisão inteira**. Quando os dois operandos de `/` são inteiros, o Java **descarta a parte fracionária**:

```java
int a = 7, b = 2;
double r = a / b;   // r vale 3.0, e NÃO 3.5!
```

O `7 / 2` é calculado como divisão inteira (resulta `3`) e só depois convertido para `double`; para obter `3.5`, pelo menos um operando precisa ser decimal (`7 / 2.0` ou `(double) a / b`). É por isso que a porcentagem correta usa `percentual / 100.0` — com `percentual / 100` inteiro, o resultado seria `0` para quase todo percentual.

> [!tip] O `+` também concatena texto
> Quando um dos lados do `+` é uma `String`, ele **concatena** em vez de somar: `"Benefício: " + 123` produz `"Benefício: 123"`. A pegadinha clássica: `System.out.println(1 + 2 + "3")` imprime `"33"` — porque `1 + 2` soma primeiro (dá `3`) e só depois o `+` encontra a String e concatena.

### 4.2 Comparação

Os operadores de comparação são **==**, `!=`, `<`, `>`, `<=`, `>=`. Todos produzem um `boolean` — verdadeiro ou falso:

```java
int idade = 32;
boolean maior = idade >= 18;      // true
boolean diferente = idade != 30;  // true
```

> [!warning] PEGADINHA — **==** compara, **=** atribui
> Em Java, **=** é atribuição (guarda um valor na variável) e **==** é comparação (pergunta se dois valores são iguais):
>
> ```java
> if (idade = 18)   // ERRO de compilação: = atribui, não compara
> ```
>
> Em linguagens como C, essa confusão passa despercebida; no Java, o compilador impede. Em prova, desconfie sempre que a alternativa trocar **==** por **=** — isso quase nunca é "detalhe de digitação".

### 4.3 Lógicos: `&&`, `||`, `!` e a ponte com as tabelas-verdade

Aqui a lógica sentencial do RLM vira código. Na [[Logica-Sentencial]], os conectivos são $p \land q$ (conjunção), $p \lor q$ (disjunção) e $\neg p$ (negação). No Java, os mesmos três conectivos têm os nomes `&&` (e), `||` (ou) e `!` (não):

$$(p \land q) \text{ é verdadeiro somente quando } p \text{ e } q \text{ são verdadeiros} \iff (p \;\&\&\; q)$$

| $p$ | $q$ | $p \land q$ (`&&`) | $p \lor q$ (`\|\|`) | $\neg p$ (`!`) |
|:---:|:---:|:---:|:---:|:---:|
| V | V | V | V | F |
| V | F | F | V | F |
| F | V | F | V | V |
| F | F | F | F | V |

```java
boolean podeConsignar = (idade >= 18) && (rendaMensal > 0);
boolean temDireito = (tipo == 1) || (tipo == 2);   // aposentadoria ou pensão
boolean situacaoBloqueada = false;
boolean naoBloqueado = !situacaoBloqueada;         // true
```

A regra de ouro se preserva: `&&` só é verdadeiro quando **ambos** os lados são verdadeiros; `||` é verdadeiro quando **pelo menos um** é verdadeiro; `!` inverte — a mesma tabela da Fase 1, com outra notação. Um detalhe a mais que o Java tem: os operadores `&&` e `||` são **curto-circuitados** — se o primeiro operando já decide o resultado (`false` para `&&`, `true` para `||`), o segundo nem chega a ser avaliado. E quem internalizou a [[Logica-Sentencial]] não decora operadores: `!(p && q)` continua equivalente a `!p || !q`, aplicando De Morgan automaticamente.

### 4.4 Atribuição: **=** e os combinados

O **=** já apareceu: ele **guarda um valor** na variável. E o Java oferece os **combinados**, que economizam escrita: `+=`, `-=`, `*=`, `/=` (e `%=`):

```java
double margem = 800.00;
margem += 100.00;   // margem = margem + 100 → 900.00
margem -= 50.00;    // margem = margem - 50  → 850.00
```

`margem += 100` é açúcar sintático da forma expandida abaixo — a expressão **da direita usa o valor atual** da variável e o resultado volta para ela:

```java
margem = margem + 100;   // equivale a margem += 100;
```
No `for`, você verá ainda o **incremento** `i++`, que é o mesmo que `i = i + 1`.

---

## 5. Controle de fluxo: decidir e repetir

O Java oferece cinco estruturas para controlar o fluxo de execução — duas de **decisão** e três de **repetição**:

| Estrutura | Tipo | Quando usar |
|---|---|---|
| `if/else` | Decisão | Condições booleanas, intervalos, lógica combinada |
| `switch/case` | Decisão | Mesma variável testada contra valores fixos |
| `for` | Repetição | Número de iterações **conhecido** antes de começar |
| `while` | Repetição | Fim depende de condição que muda durante execução |
| `do-while` | Repetição | Corpo precisa rodar **pelo menos uma** vez |

> [!tip] A ponte entre SQL e Java
> Pense no `WHERE` do SQL como um `if` que roda automaticamente para cada linha da tabela. No Java, você controla explicitamente quando e quantas vezes a condição é testada.

A explicação completa com exemplos, pegadinhas da FGV e tabelas comparativas está na subnota dedicada:

👉 **[[Controle-de-Fluxo-Java]]**

---

## 6. Entrada e saída básica

Todo programa precisa se comunicar: receber dados (**entrada**) e mostrar resultados (**saída**). Nesta seção, você vai ver as duas faces dessa comunicação: como o Java mostra informações na tela e como ele recebe dados do usuário. A saída é o foco da prova; a entrada é o primeiro contato com a ideia de objeto — o aprofundamento virá no tópico 2.

### 6.1 Saída: `System.out.println` e `System.out.print`

A saída em Java usa a classe `System`. A cadeia `System.out.println(...)` tem três partes que funcionam como um encadeamento — cada parte acessa algo da anterior:

- `System` — uma classe especial do Java que fornece acesso ao sistema (entrada, saída e utilitários);
- `out` — um campo dentro de `System` que representa o **canal de saída padrão** (a tela do terminal);
- `println(...)` — um **método** que imprime o valor entre parênteses e em seguida **pula para a próxima linha** (o `ln` vem de *line*, "linha" em inglês).

O equivalente em inglês é: "`System`, canal da saída padrão, e imprima **com quebra de linha**." Se você trocar `println` por `print`, a única diferença é que **não há quebra de linha** — o cursor permanece no final do texto impresso, e a próxima impressão continua na mesma linha:

```java
System.out.println("Beneficiário cadastrado");   // imprime e pula linha
System.out.print("Renda: ");                     // imprime SEM pular linha
System.out.println(3200.00);                     // imprime na MESMA linha e pula
```

O resultado das três linhas acima:

```text
Beneficiário cadastrado
Renda: 3200.0
```

Repare no efeito: como `print("Renda: ")` não pula linha, o `println(3200.00)` continua imediatamente após os dois-pontos. Se a segunda linha fosse `println` em vez de `print`, o resultado seria diferente:

```text
Beneficiário cadastrado
Renda: 
3200.0
```

> [!tip] Anote a regra no rascunho
> Em prova, desenhe uma pequena **linha imaginária** para cada `print`/`println`. Cada `println` fecha a linha e desenha uma nova; cada `print` continua na linha atual. Esse truque evita o erro mais comum: confundir onde uma linha termina e outra começa.

`println` aceita **qualquer tipo** entre parênteses — `String`, `int`, `double`, `boolean` — e o imprime como texto. `println(3200.00)` mostra `3200.0` (um `double`); `println(true)` mostra `true`; `println(" texto ")` mantém os espaços. O `+` dentro de `System.out.println` funciona como **concatenação** quando um dos lados é `String` (como visto na Seção 4):

```java
String nome = "Maria";
double renda = 3200.00;
System.out.println("Nome: " + nome + " — R$" + renda);
// Saída: Nome: Maria — R$3200.0
```

### 6.2 Entrada: `Scanner`

Para **receber** dados (entrada), o Java oferece a classe `Scanner`, que faz a leitura de dados que o usuário digita. Por enquanto, o que interessa para a prova é reconhecer o **padrão** e saber o que cada parte faz — o conceito de objeto (o `new`, o construtor) será detalhado no tópico 2.

```java
import java.util.Scanner;                // importa a classe Scanner do pacote java.util

Scanner leitor = new Scanner(System.in);  // cria o leitor ligado ao teclado
System.out.print("Digite sua renda: ");   // pergunta ao usuário
double renda = leitor.nextDouble();       // lê um decimal (ex.: 3200.00)
System.out.println("Renda lida: " + renda);  // mostra o que foi lido
```

Cada linha tem um papel:

| Linha | O que faz | Por que é assim |
|---|---|---|
| `import java.util.Scanner;` | Disponibiliza a classe `Scanner` no programa | `Scanner` vive no pacote `java.util`; sem o `import`, o compilador não a encontra — **erro de compilação** |
| `Scanner leitor = new Scanner(System.in);` | Cria um leitor de dados ligado ao teclado | `System.in` é o **canal de entrada padrão** (o teclado); `new` cria o objeto (tópico 2); `leitor` é o nome da variável que guarda o leitor |
| `leitor.nextDouble()` | Lê um número decimal digitado pelo usuário | Outros métodos: `nextLine()` (linha inteira), `nextInt()` (inteiro) — a prova pede reconhecimento, não memorização |

> [!warning] O `Scanner` precisa de `import`
> Ao contrário de `System` (que está no pacote padrão e sempre está disponível), `Scanner` vive em `java.util`. Se você esquecer o `import java.util.Scanner;`, o compilador gera erro. Em prova, se a alternativa usa `Scanner` sem `import`, verifique se é a intenção da questão — geralmente o `import` é omitido por simplificação, mas em código completo ele é obrigatório.

> [!tip] O padrão que cai em prova
> A FGV não costuma pedir `Scanner` em profundidade neste nível. O que aparece é o **reconhecimento**: `new Scanner(System.in)` significa "criar um leitor de dados do teclado"; `nextLine()` significa "ler uma linha inteira"; `nextDouble()` significa "ler um número decimal". Se a questão mistura entrada e saída, trace o fluxo: o que entra pelo `Scanner` → o que o programa faz com os dados → o que sai pelo `System.out.println`.

---

## 7. Como a FGV cobra

### 7.1 Palavras-chave

| Palavra/expressão | O que sinaliza na prova |
|---|---|
| `public static void main(String[] args)` | Ponto de entrada; `public` = visível, `static` = pertence à classe, `void` = sem retorno |
| `main` | Nome **obrigatório**; renomear → compila mas não executa |
| `String[] args` | Parâmetros da linha de comando; `args.length` = quantidade de argumentos |
| camelCase | Padrão de nomes: `rendaMensal`, `dataNascimento`, `margemConsignavel` |
| `;` | Toda instrução termina com ponto e vírgula; esquecer → erro de compilação |
| `System.out.println` vs `System.out.print` | Com quebra de linha vs sem quebra — muda o texto de saída |
| `%` | Resto da divisão inteira, **não** porcentagem |
| Classe (recipiente) | `class` minúsculo, PascalCase, arquivo = classe; campos = variáveis dentro da classe | Aprofundar objeto (`new`, construtor, `this`) — isso é o tópico 2 |

### 7.2 As pegadinhas no padrão "armadilha → raciocínio errado → proteção"

> [!warning] Pegadinha 1 — esquecer o `;`
> **A armadilha:** o código termina uma instrução sem `;` e a alternativa afirma "o programa roda, mas ignora a linha".
> **O raciocínio errado:** "se faltou o ponto e vírgula, o Java apenas continua na linha seguinte."
> **Como se proteger:** cada instrução Java **termina com `;`**. Faltou → **erro de compilação**; o programa nunca chega a rodar. Não existe "linha ignorada".

> [!warning] Pegadinha 2 — `println` vs `print`
> **A armadilha:** a questão pergunta qual é a saída exata de um código com `System.out.print` e `System.out.println` intercalados.
> **O raciocínio errado:** "tanto faz — os dois imprimem o texto."
> **Como se proteger:** teste linha por linha: `print` deixa o cursor **na mesma linha**; `println` joga para a linha seguinte. Em prova, anote no rascunho a saída **exatamente como o texto ficaria na tela**.

> [!warning] Pegadinha 3 — a forma da classe
> **A armadilha:** uma alternativa escreve `Class` com maiúscula, ou coloca código Java fora de uma classe, ou usa um nome de arquivo diferente do nome da classe pública.
> **O raciocínio errado:** "a classe é só um detalhe de organização; o que importa é o que o programa faz."
> **Como se proteger:** em Java, **todo** código executável vive dentro de uma classe; a palavra-chave é `class`, **sempre minúscula**; e o arquivo `.java` tem o **mesmo nome** da classe pública (`Principal.java` → `public class Principal`). Qualquer alternativa que quebre essas três regras é invenção.

> [!warning] Pegadinha 4 — `%`, **==** e divisão inteira
> **A armadilha:** o código calcula `7 % 3`, divide `a / b` com inteiros ou compara com **=**, e a alternativa troca o resultado.
> **O raciocínio errado:** "o `%` calcula porcentagem"; "divisão de inteiro sempre dá decimal"; "**=** compara valores."
> **Como se proteger:** `%` é **resto**; divisão entre inteiros **trunca** (`7 / 2 = 3`); **==** compara, **=** atribui. Na dúvida, simule a expressão com números pequenos no rascunho.

---

## 8. Questões-modelo (pegada FGV)

> [!example] Questão 1 — estrutura do programa e saída
> Considere o arquivo `Principal.java`:
> ```java
> public class Principal {
>     public static void main(String[] args) {
>         System.out.print("INSS");
>         System.out.println("BENEFICIOS");
>     }
> }
> ```
> A execução desse programa produzirá:
> (A) `INSSBENEFICIOS` em uma única linha;
> (B) `INSS` e `BENEFICIOS` em linhas separadas;
> (C) `BENEFICIOSINSS` em uma única linha;
> (D) `INSS BENEFICIOS` em uma única linha, com espaço entre as palavras;
> (E) erro de compilação, pois `print` e `println` não podem ser usados no mesmo método.
>
> **Gabarito comentado:** (A). O `print` imprime `INSS` sem quebrar a linha; o `println` imprime `BENEFICIOS` logo em seguida e só então quebra. O resultado é uma única linha `INSSBENEFICIOS`. A alternativa (B) é a pegadinha clássica de quem supõe que todo `System.out...` quebra linha; (C) inverte a ordem; (D) inventa um espaço que não existe no código; (E) é absurda — os dois métodos convivem normalmente.

> [!example] Questão 2 — operadores, `%` e divisão inteira
> Considere o trecho:
> ```java
> int a = 7, b = 2;
> boolean r1 = (a % b == 1) && (a / b == 3);
> boolean r2 = (a > b) || (a == b);
> System.out.println(r1 + " " + r2);
> ```
> O programa imprime:
> (A) `true true`
> (B) `true false`
> (C) `false true`
> (D) `false false`
> (E) erro de compilação, pois `a / b` não é permitido para inteiros.
>
> **Gabarito comentado:** (A). `7 % 2 = 1`, logo `(a % b == 1)` é `true`; `7 / 2` em inteiros vale `3` (a fração é descartada), logo `(a / b == 3)` é `true`; pela tabela da conjunção, `true && true = true`. Em `r2`, `7 > 2` é `true`, e na disjunção basta um verdadeiro → `true`. Repare nas duas pegadinhas embutidas: o `%` como **resto** e a **divisão inteira** (`a / b` vale `3`, não `3.5`) — exatamente o padrão da FGV.

> [!example] Questão 3 — a forma da classe
> Considere o arquivo `Beneficiario.java`:
> ```java
> public class Beneficiario {
>     String nome;
>     double rendaMensal;
> }
> ```
> Assinale a afirmativa correta:
> (A) A palavra-chave pode ser escrita `Class`, com maiúscula, sem diferença para o compilador.
> (B) Esse código não compila, pois o nome do arquivo deve ser diferente do nome da classe.
> (C) `nome` e `rendaMensal` são **campos**, declarados dentro da classe como variáveis.
> (D) Métodos devem obrigatoriamente vir antes dos campos dentro da classe.
> (E) Código executável pode ser escrito fora de qualquer classe em um arquivo `.java`.
>
> **Gabarito comentado:** (C). Os campos usam a mesma sintaxe de variável vista na Seção 3 — tipo antes do nome, `;` ao final. (A) é falsa: a palavra-chave é `class`, minúscula. (B) e (E) são falsas: o arquivo deve ter o **mesmo nome** da classe pública e todo código Java vive **dentro** de uma classe. (D) é inventada: não existe ordem obrigatória entre campos e métodos.

---

## 9. Revisão rápida

| Conceito | Ponto-chave | Erro mais comum em prova |
|---|---|---|
| Ponto de entrada | `public static void main(String[] args)` | Renomear `main` e achar que ainda executa |
| Comando | Termina com `;` | Esquecer o `;` e achar que "roda mesmo assim" |
| Variável | Tipo **antes** do nome; camelCase; case-sensitive | Tratar `idade` e `Idade` como iguais |
| `%` | Resto da divisão inteira (`7 % 3` deixa resto `1`) | Tratar como porcentagem |
| `&&` / `\|\|` / `!` | Tabelas-verdade ([[Logica-Sentencial]]) | Achar que `&&` aceita "quase verdadeiro" |
| **==** | Compara valores | Confundir com **=** (atribuição) |
| Divisão inteira | `7 / 2 = 3` (descarta a fração) | Esperar `3.5` |
| `println` × `print` | Com/sem quebra de linha | Ignorar a diferença no texto de saída |
| Classe (recipiente) | `class` minúsculo + PascalCase + `{}`; campos = variáveis na classe | Escrever `Class` com maiúscula ou código fora da classe |

> [!tip] O erro que mais derruba na prova
> Misturar os pares parecidos da linguagem: **=** com **==**, `print` com `println`, e `class` (palavra-chave) com `Class` (maiúscula). Esses pares têm funções diferentes, e a FGV os explora justamente porque são os pontos em que o candidato que "decora por cima" erra.

---

## 10. Próximos passos

Você agora sabe a forma da língua: como um programa Java se organiza, como declarar variáveis, operar, decidir, repetir, comunicar e escrever o molde da classe. Antes de coleções, exceções e generics, falta um subtópico que aparece em quase todo código: os **tipos primitivos e seus wrappers** — por que `int` não aceita `null` e `Integer` aceita; por que `float x = 0.5;` não compila; o que é autoboxing e unboxing. É exatamente o que a subnota [[Tipos-Primitivos-e-Wrappers]] desenvolve. E lembre-se do mapa do tópico: esta subnota é o primeiro degrau do índice [[Java-Fundamentos-da-Linguagem]], que reúne a sintaxe essencial (aqui), os [[Tipos-Primitivos-e-Wrappers]], as [[Colecoes-Java]], o [[Tratamento-de-Excecoes]] e os [[Generics]]. Depois de dominar a forma, o próximo degrau é o [[Paradigma-Orientado-a-Objetos]] — onde a classe deixa de ser sintaxe e vira o modelo mental de design.