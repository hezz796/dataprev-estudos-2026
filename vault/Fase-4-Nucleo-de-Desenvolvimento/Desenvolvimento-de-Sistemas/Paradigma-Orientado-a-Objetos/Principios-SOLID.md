# Princípios SOLID

> [!info] Metadados
> **Disciplina:** Desenvolvimento de Sistemas
> **Bloco:** 4.1 — Desenvolvimento de Sistemas (FASE 4 — Núcleo de Desenvolvimento)
> **Tópico:** 2. Paradigma Orientado a Objetos — Princípios SOLID
> **Subtópicos:** SOLID (princípios básicos — S, O, L, I, D)
> **Pré-requisitos:** [[Quatro-Pilares-do-POO]] (polimorfismo, herança, encapsulamento) e [[Clean-Code]] (qualidade de código)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-09-17

---

## 1. Por que estudar SOLID?

SOLID é um acrônimo mnemônico que agrupa cinco princípios de design orientado a objetos, introduzidos originalmente por Robert C. Martin ("Uncle Bob") e consolidados ao longo de décadas de prática de engenharia de software. Esses cinco princípios orientam a construção de código **coeso, desacoplado, extensível e fácil de manter** — exatamente o tipo de código que sistemas críticos exigem.

O edital da DATAPREV pede os "princípios básicos" do SOLID. A expressão "básicos" não é casual: a banca espera que você conheça a **definição** de cada letra, saiba **distingui-las** (especialmente as que se confundem — S, D, L) e reconheça quando o código viola algum princípio. Não se trata de decorar casos extremos, mas de dominar o conceito central de cada um.

> [!question] Pergunta orientadora
> Se um sistema previdenciário precisa evoluir para atender uma nova legislação — digamos, uma nova regra de cálculo de benefício — mas qualquer alteração no código quebra funcionalidades existentes, o que está errado? Os princípios SOLID existem justamente para evitar esse cenário. Um código bem projetado permite **adicionar** funcionalidade **sem modificar** a que já funciona — e cada princípio SOLID contribui com uma peça desse quebra-cabeça.

Pense no contexto DATAPREV: sistemas de benefícios, consignação, folha de pagamento, CNIS. São sistemas que precisam **evoluir continuamente** (nova legislação, novas regras, novos canais de atendimento) sem que cada mudança arrisque quebrar o que já está rodando. SOLID é o conjunto de princípios que mantém esses sistemas saudáveis ao longo do tempo.

---

## 2. S — Single Responsibility Principle (SRP, Princípio da Responsabilidade Única)

> [!important] Definição
> **Uma classe deve ter um único motivo para mudar** — ou seja, deve possuir **uma única responsabilidade**.

A ideia central é a seguinte: quando uma classe acumula duas ou mais responsabilidades distintas, qualquer mudança em uma delas força alterações nessa mesma classe — o que aumenta o risco de introduzir bugs em funcionalidades que não tinham nada a ver com a mudança. SRP é, antes de tudo, um princípio de **manutenibilidade**: ao garantir que uma classe tenha um único motivo para ser alterada, você reduz o risco de efeitos colaterais.

Pense assim: se você é responsável por duas tarefas — digamos, calcular impostos e enviar relatórios por e-mail —, qualquer mudança na fórmula de imposto força você a mexer no mesmo código que envia e-mail. Dois códigos-fonte distintos, dois motivos diferentes para mudar, compartilhando o mesmo espaço. Isso é ruim porque uma mudança pode acidentalmente quebrar a outra.

### Violação e correção

```java
// VIOLAÇÃO — a classe cuida do cálculo E do envio de email (duas responsabilidades)
public class Beneficio {
    public double calcularValor(double renda, double margem) { ... }
    public void enviarEmail(Beneficiario b, double valor) { ... }   // responsabilidade alheia
}

// CORREÇÃO — cada responsabilidade em sua classe
public class CalculoBeneficio {
    public double calcular(double renda, double margem) { ... }
}

public class NotificacaoBeneficio {
    public void enviar(Beneficiario b, double valor) { ... }
}
```

Na versão corrigida, `CalculoBeneficio` tem um único motivo para mudar: a regra de cálculo. `NotificacaoBeneficio` tem outro motivo próprio: o canal ou formato de notificação. Se amanhã o e-mail for substituído por push notification, você altera apenas `NotificacaoBeneficio` — `CalculoBeneficio` nem precisa saber da mudança.

> [!warning] PEGADINHA — SRP não significa "uma classe com um único método"
> O SRP **não** significa "uma classe faz uma única coisa elementar" nem "uma classe tem um único método". Significa que ela tem **um único motivo para mudar** — uma única *responsabilidade* no sentido de *razão de ser alterada*. Uma classe `Beneficiario` pode ter dezenas de métodos (`calcularRegra()`, `validarCpf()`, `listarDependentes()`, `obterLotacao()`) e ainda assim ter responsabilidade única: **representar o beneficiário no sistema**. A pegadinha é reduzir o SRP a "uma função só". Quando a questão disser que uma classe com vários métodos viola SRP, pergunte-se: *esses métodos servem a uma mesma razão de existir ou a duas diferentes?*

### Como a FGV cobra o SRP

A banca troca definições entre letras. Uma alternativa pode dizer que o SRP "abre para extensão e fecha para modificação" — isso é OCP, não SRP. Outra pegadinha: afirmar que o SRP proíbe que uma classe tenha vários métodos. Preste atenção: a frase-chave é **"único motivo para mudar"**, não "único método".

---

## 3. O — Open/Closed Principle (OCP, Princípio Aberto/Fechado)

> [!important] Definição
> **As entidades devem estar abertas para extensão, mas fechadas para modificação.**

A tradução mais direta: você deve poder **adicionar** novos comportamentos **sem modificar** o código que já existe. O polimorfismo — que você estudou em [[Quatro-Pilares-do-POO]] — é o mecanismo que torna isso possível: ao definir uma interface comum e permitir que novas implementações sejam criadas, o código existente continua funcionando sem alterações.

A metáfora é simples: imagine um sistema que aceita plugins. Você instala um plugin novo sem tocar no sistema original. OCP diz: o código deveria funcionar assim — aberto a novos plugins (extensão), mas sem precisar reescrever o código-fonte (modificação).

### Violação e correção

```java
// VIOLAÇÃO — cada tipo novo exige um novo "if" e modifica a classe
public class Desconto {
    public double aplicar(double valor, String tipo) {
        if (tipo.equals("PIX")) return valor * 0.95;
        if (tipo.equals("CARTAO")) return valor * 1.03;
        // novo tipo => novo if => modificação da classe
        return valor;
    }
}
```

Nesse código, toda vez que surge um novo tipo de desconto (Boleto, Criptomoeda, etc.), alguém precisa abrir o arquivo `Desconto.java` e adicionar mais um `if`. A classe **não é fechada para modificação** — ela muda a cada novo tipo. Isso viola OCP.

```java
// CORREÇÃO — aberto para extensão via herança/polimorfismo
public interface RegraDesconto {
    double aplicar(double valor);
}

public class DescontoPix implements RegraDesconto {
    public double aplicar(double valor) { return valor * 0.95; }
}

public class DescontoCartao implements RegraDesconto {
    public double aplicar(double valor) { return valor * 1.03; }
}

// Para adicionar um novo tipo, basta criar uma nova classe que implementa
// RegraDesconto — sem tocar no código existente.
```

Agora `DescontoPix` e `DescontoCartao` são **extensões** que não modificam código existente. Se amanhã surgir `DescontoBoleto`, você cria a nova classe e pronto — o código que usa `RegraDesconto` continua funcionando sem alteração. A classe original está **fechada para modificação** e **aberta para extensão**.

### Como a FGV cobra o OCP

A banca pode afirmar: "para adicionar um novo tipo de desconto, é necessário modificar a classe `Desconto`." Se o código viola OCP, isso é verdade — mas a banca espera que você reconheça a **violação**. A resposta correta geralmente aponta que o código deveria ser aberto para extensão. Outra forma: trocar a definição de OCP com a de SRP ou DIP — fique atento à palavra-chave "extensão/modificação" que é exclusiva do OCP.

---

## 4. L — Liskov Substitution Principle (LSP, Princípio da Substituição de Liskov)

> [!important] Definição
> **Se uma classe S é uma subclasse de T, então objetos de T devem poder ser substituídos por objetos de S sem quebrar o programa.**

Em outras palavras: a herança deve ser **genuína**. Se `PatoDeBorracha` é subclasse de `Pato`, então em qualquer lugar que o código espera um `Pato` (e acredita que ele nada), um `PatoDeBorracha` deveria funcionar da mesma forma. Se não funciona — se o `PatoDeBorracha` lança exceção ao nadar —, a herança é falsa e o LSP está violado.

O LSP protege o **contrato** entre superclasse e subclasses. A superclasse define um comportamento esperado; as subclasses devem honrar esse comportamento.

### Violação e correção

```java
// VIOLAÇÃO — o Pato de borracha "é um" Pato, mas não nada
public class Pato { public void nadar() { } }
public class PatoDeBorracha extends Pato {
    @Override
    public void nadar() { throw new UnsupportedOperationException(); }
}
// Quem confia que "todo Pato nada" quebra ao receber um PatoDeBorracha.
```

O problema é claro: o código que recebe um `Pato` e chama `nadar()` espera que isso funcione. Se recebe um `PatoDeBorracha`, lança exceção. A substituição falhou. O LSP diz: ou `PatoDeBorracha` nadar de verdade, ou a hierarquia está errada e deveria ser reavaliada.

> [!warning] PEGADINHA — retângulo e quadrado
> O exemplo clássico do LSP é o **retângulo/quadrado**: um Quadrado "é um" Retângulo (um quadrado é um retângulo com lados iguais), mas se você altera a largura do quadrado, a altura deveria mudar também para manter os lados iguais — o que **quebra o comportamento esperado** do Retângulo (onde largura e altura são independentes). Se o código espera um `Retangulo` e recebe um `Quadrado`, alterar a largura afeta a altura de forma inesperada. A substituição não preserva o comportamento correto, e o LSP é violado. A FGV adora cobrar esse cenário: "um Quadrado é um Retângulo — logo, pode substituí-lo em qualquer contexto" — **falso**, sob o ponto de vista de LSP.

### Como a FGV cobra o LSP

A banca pode inverter a definição e dizer que o LSP "permite que subclasse adicione comportamentos novos sem alterar a superclasse" — isso é confundir LSP com OCP. A frase-chave do LSP é **substituibilidade**: a subclasse deve poder substituir a superclasse **sem quebrar o comportamento correto do programa**.

---

## 5. I — Interface Segregation Principle (ISP, Princípio da Segregação de Interfaces)

> [!important] Definição
> **As interfaces devem ser específicas do cliente; nenhum cliente deve depender de métodos que não utiliza.**

A ideia é combater interfaces "gorduchas" — interfaces com tantos métodos que seus implementadores são forçados a implementar funcionalidades que não precisam. Quando isso acontece, o código acumula implementações vazias ou fictícias (`throw new UnsupportedOperationException()`), o que é sinal de má configuração de interfaces.

ISP diz: dividir em interfaces menores e mais focadas, de modo que cada classe implemente apenas o que realmente precisa.

### Violação e correção

```java
// VIOLAÇÃO — interface única e inchada
public interface Funcionario {
    void baterPonto();
    void programar();
    void gerenciarEquipe();
}
// Um programador precisaria implementar gerenciarEquipe (e vice-versa)
```

Nesse cenário, um desenvolvedor que implementa `Funcionario` é obrigado a escrever `gerenciarEquipe()` — algo que ele não faz. E um gestor que implementa `Funcionario` é obrigado a escrever `programar()` — algo que ele também não faz. Ambos implementam código que não precisa existir.

```java
// CORREÇÃO — interfaces específicas
public interface RegistroPonto { void baterPonto(); }
public interface Desenvolvedor { void programar(); }
public interface Gestor { void gerenciarEquipe(); }
```

Agora cada classe implementa exatamente o que precisa. Um desenvolvedor implementa `Desenvolvedor`; um gestor implementa `Gestor`. Ninguém é forçado a implementar métodos irrelevantes.

### Como a FGV cobra o ISP

A banca pode trocar a definição de ISP com SRP: "cada classe deve ter uma única responsabilidade" é SRP; "cada interface deve ser específica do cliente" é ISP. A palavra-chave que distingue ISP é **interfaces** e **cliente** — se a frase fala em interfaces inchadas e métodos que clientes não utilizam, é ISP.

---

## 6. D — Dependency Inversion Principle (DIP, Princípio da Inversão de Dependência)

> [!important] Definição
> **Módulos de alto nível não devem depender de módulos de baixo nível; ambos devem depender de abstrações. Abstrações não devem depender de detalhes; detalhes devem depender de abstrações.**

Em termos simples: o código deve depender de **interfaces/abstrações** (o "contrato"), e não de **implementações concretas** (o "como"). Isso permite trocar a implementação sem mexer em quem a usa.

Pense assim: se um relatório depende diretamente do banco PostgreSQL, trocar o banco exige alterar o código do relatório. Mas se o relatório depende de uma interface `RepositorioDados`, basta criar uma nova classe que implemente essa interface para o banco diferente — o relatório nem fica sabendo da troca.

### Violação e correção

```java
// VIOLAÇÃO — a classe alta depende diretamente de uma implementação concreta
public class EmissorRelatorio {
    private BancoPostgres banco = new BancoPostgres();   // acoplamento rígido
}
```

Aqui `EmissorRelatorio` (módulo de alto nível — a regra de negócio) depende diretamente de `BancoPostgres` (módulo de baixo nível — detalhe de implementação). Se amanhã o banco for Oracle ou um cache in-memory, é preciso alterar `EmissorRelatorio`.

```java
// CORREÇÃO — depende de uma abstração (interface)
public interface RepositorioDados { List<Registro> buscar(); }

public class RepositorioPostgres implements RepositorioDados { ... }
public class RepositorioCache implements RepositorioDados { ... }

public class EmissorRelatorio {
    private RepositorioDados repositorio;   // depende da abstração
    public EmissorRelatorio(RepositorioDados r) { this.repositorio = r; }
}
```

Agora `EmissorRelatorio` depende de `RepositorioDados` — uma abstração. A implementação concreta (`RepositorioPostgres`, `RepositorioCache`) é injetada externamente (construtor). Para trocar a fonte de dados, basta passar outra implementação — o relatório não muda. Esse padrão de "receber a dependência de fora" é a base da **Injeção de Dependência**, que será explorada nos tópicos de Spring (tópico 5).

> [!note] Conexão com o Spring
> DIP é o princípio que fundamenta a **Injeção de Dependência** e o **IoC Container** do Spring Framework. Quando você usar `@Autowired` no tópico 5, estará aplicando DIP na prática — a classe depende de uma abstração (interface), e o container fornece a implementação concreta. Não se aprofunde agora; apenas registre a conexão.

### Como a FGV cobra o DIP

A banca troca definições entre DIP e SRP: "dependa de abstrações, não de detalhes" é DIP; "um único motivo para mudar" é SRP. Outra pegadinha: afirmar que DIP significa "as classes de alto nível devem depender de classes de baixo nível" — o oposto exato do princípio. A frase-chave é **dependa de abstrações** e **inversão** (a dependência é invertida: o módulo alto não depende do baixo, e sim de uma abstração compartilhada).

---

## 7. Os cinco em uma frase — revisão rápida

> [!note] Mnemônico SOLID
> **S** = uma responsabilidade por classe · **O** = aberto a extensão, fechado a modificação · **L** = superclasse substituível pela subclasse · **I** = interfaces específicas, não inchadas · **D** = dependa de abstrações, não de concretos.

A tabela abaixo consolida os cinco princípios com frase-chave e a pegadinha mais comum em cada um:

| Letra | Nome | Frase-chave | Pegadinha típica da banca |
|:---:|---|---|---|
| **S** | SRP — Responsabilidade Única | Um único motivo para mudar | Trocar com definição de OCP ou ISP; afirmar que SRP proíbe vários métodos |
| **O** | OCP — Aberto/Fechado | Aberto para extensão, fechado para modificação | Trocar com definição de SRP; afirmar que modificar classe existente é "extensão" |
| **L** | LSP — Substituição de Liskov | Subclasse deve substituir superclasse sem quebrar | Trocar com OCP; afirmar que Quadrado substitui Retângulo em qualquer contexto |
| **I** | ISP — Segregação de Interfaces | Interfaces específicas; cliente não depende do que não usa | Trocar com SRP; afirmar que ISP se refere a classes, não interfaces |
| **D** | DIP — Inversão de Dependência | Dependa de abstrações, não de implementações concretas | Trocar com SRP; afirmar que módulos de alto nível devem depender de módulos de baixo nível |

---

## 8. Como a FGV cobra SOLID

### 8.1 Palavras-chave

A banca costuma apresentar os termos abaixo nas alternativas. Quando você os vir, identifique imediatamente a que princípio pertencem:

| Palavra-chave / Expressão | Princípio associado |
|---|---|
| **Responsabilidade Única / único motivo para mudar** | SRP |
| **Aberto/fechado / extensão sem modificação** | OCP |
| **Substituição de Liskov / subclasse substituível** | LSP |
| **Segregação de Interfaces / interfaces específicas** | ISP |
| **Inversão de Dependência / depender de abstrações** | DIP |
| **Injeção de Dependência** | DIP (consequência prática) |
| **Abstração / contrato** | DIP (mecanismo) |
| **SOLID** | Todos os cinco — a banca pode trocar definições entre alternativas |

### 8.2 O padrão "armadilha → raciocínio errado → proteção"

> [!warning] Pegadinha 1 — Trocar definições entre letras
> **A armadilha:** a questão apresenta uma definição de um princípio e atribui a letra errada (por exemplo, diz que "aberto para extensão, fechado para modificação" é o SRP).
> **O raciocínio errado:** aceitar a definição sem verificar se a letra corresponde.
> **Como se proteger:** decore cada letra com sua frase-chave. SRP = "único motivo para mudar"; OCP = "aberto/fechado"; LSP = "substituível"; ISP = "interfaces específicas"; DIP = "abstrações". Se a letra na alternativa não bate com a frase, está errada — mesmo que a definição pareça bonita.

> [!warning] Pegadinha 2 — SRP proíbe vários métodos
> **A armadilha:** "uma classe com vários métodos viola SRP."
> **O raciocínio errado:** confundir "responsabilidade" com "método".
> **Como se proteger:** SRP fala em **motivo para mudar**, não em número de métodos. Uma classe com 20 métodos pode ter responsabilidade única se todos servem ao mesmo propósito. Pergunte: *qual a razão de ser alterada?* Se há apenas uma razão, SRP está satisfeito.

> [!warning] Pegadinha 3 — DIP significa depender de classes concretas
> **A armadilha:** "módulos de alto nível devem depender de módulos de baixo nível."
> **O raciocínio errado:** aceitar a frase como verdadeira, porque soa plausível.
> **Como se proteger:** o DIP diz **exatamente o oposto**: módulos de alto nível **não** devem depender de módulos de baixo nível — ambos devem depender de **abstrações**. Se a alternativa sugere dependência direta entre alto e baixo nível, é violação de DIP, não definição.

> [!warning] Pegadinha 4 — LSP e o retângulo/quadrado
> **A armadilha:** "um Quadrado é um Retângulo, logo pode substituí-lo sem problemas."
> **O raciocínio errado:** confundir a relação conceitual ("quadrado é um retângulo") com o contrato de comportamento esperado pelo código.
> **Como se proteger:** LSP não é sobre classificação lógica — é sobre **comportamento observável**. Se o código espera que `Retangulo.setLargura(10)` não altere a altura, e o `Quadrado` viola essa expectativa, a substituição falha. LSP pergunta: *o comportamento é preservado?* — não *a relação conceitual faz sentido?*

---

## 9. Questões-modelo (pegada FGV)

> [!example] Questão 1 — Troca de definições entre letras
> Considere as afirmações sobre os princípios SOLID:
>
> **I.** O SRP determina que uma classe deve ter um único motivo para mudar.
> **II.** O OCP afirma que entidades devem ser fechadas para extensão e abertas para modificação.
> **III.** O LSP determina que uma subclasse deve poder substituir sua superclasse sem quebrar o programa.
> **IV.** O ISP afirma que interfaces devem ser específicas para cada cliente.
> **V.** O DIP determina que módulos de alto nível devem depender de módulos de baixo nível.
>
> Quais estão corretas?
>
> **(A)** Apenas I, III e IV.
> **(B)** Apenas II e V.
> **(C)** Apenas I, III, IV e V.
> **(D)** Apenas I e III.
> **(E)** Apenas I, II, III e IV.

> [!note] Gabarito e comentário — Questão 1
> **Resposta: (A)**
> Afirmação I está correta — SRP é "único motivo para mudar". Afirmação II está **incorreta** — o OCP diz "abertas para extensão, **fechadas** para modificação", e não o inverso. Afirmação III está correta — LSP é substituibilidade. Afirmação IV está correta — ISP é interfaces específicas por cliente. Afirmação V está **incorreta** — o DIP diz que módulos de alto nível **não** devem depender de módulos de baixo nível; ambos devem depender de abstrações. A banca trocou OCP (inverteu "aberto/fechado") e DIP (inverteu a direção da dependência). As alternativas B, C e E incluem pelo menos uma afirmação incorreta. A resposta é (A).

> [!example] Questão 2 — DIP e Injeção de Dependência
> Um sistema previdenciário possui a classe `CalculadoraBeneficio`, que precisa acessar dados de beneficiários. Atualmente, a classe instancia diretamente `BancoPostgres` no construtor. Para aplicar o princípio da inversão de dependência, qual alternativa representa a refatoração correta?
>
> **(A)** Tornar `CalculadoraBeneficio` uma classe abstrata para que `BancoPostgres` herde dela.
> **(B)** Deixar `CalculadoraBeneficio` como está, mas tornar `BancoPostgres` uma interface.
> **(C)** Criar uma interface `RepositorioBeneficiario` e fazer `CalculadoraBeneficio` depender dessa interface, recebendo a implementação via construtor.
> **(D)** Mover todos os métodos de `BancoPostgres` para `CalculadoraBeneficio` para eliminar a dependência externa.
> **(E)** Criar uma classe `CalculadoraBeneficioPostgres` que herde de `CalculadoraBeneficio`.

> [!note] Gabarito e comentário — Questão 2
> **Resposta: (C)**
> O DIP diz: módulos de alto nível devem depender de abstrações, não de implementações concretas. A refatoração correta é criar uma interface (`RepositorioBeneficiario`) que represente o contrato, e fazer `CalculadoraBeneficio` depender dela — recebendo a implementação concreta via construtor (injeção de dependência). (A) não resolve — herança não elimina a dependência de `BancoPostgres`. (B) confunde: `BancoPostgres` não deveria virar interface — a interface é um contrato novo, abstraindo o acesso a dados. (D) piora o acoplamento — agora `CalculadoraBeneficio` faz tudo. (E) cria hierarquia desnecessária e não resolve a dependência concreta.

> [!example] Questão 3 — OCP e extensão
> Considere o trecho abaixo:
> ```java
> public class CalculadoraImposto {
>     public double calcular(double valor, String tipo) {
>         if (tipo.equals("IRPF")) return valor * 0.275;
>         if (tipo.equals("IOF")) return valor * 0.01;
>         return 0;
>     }
> }
> ```
> Para que esse código atenda ao princípio aberto/fechado (OCP), a alternativa mais adequada é:
>
> **(A)** Adicionar mais parâmetros ao método `calcular` para cobrir todos os impostos.
> **(B)** Transformar os `if` em `switch-case` para facilitar a leitura.
> **(C)** Criar uma interface `RegraImposto` com um método `calcular()`, e criar classes separadas para cada tipo de imposto que implementem essa interface.
> **(D)** Tornar a classe `CalculadoraImposto` abstrata e criar subclasses para cada imposto.
> **(E)** Inverter a ordem dos `if` para que IOF seja verificado primeiro.

> [!note] Gabarito e comentário — Questão 3
> **Resposta: (C)**
> O OCP exige que o código seja **aberto para extensão** (novo tipo de imposto = nova classe) e **fechado para modificação** (nenhum `if` existente é alterado). A interface `RegraImposto` define o contrato; cada imposto tem sua implementação. (A) e (B) mantêm a estrutura de `if` — qualquer novo imposto ainda exige modificar `CalculadoraImposto`, violando OCP. (D) pode parecer plausível, mas herança sem interface não é o mecanismo canônico de OCP — o polimorfismo via interface é a abordagem recomendada. (E) é irrelevante para OCP.

---

## 10. Revisão rápida

| Princípio | Sigla | Frase-chave | Exemplo do dia a dia |
|---|:---:|---|---|
| Responsabilidade Única | SRP | Um único motivo para mudar | Separar cálculo de benefício de notificação por e-mail |
| Aberto/Fechado | OCP | Aberto para extensão, fechado para modificação | Criar nova classe de desconto sem modificar a existente |
| Substituição de Liskov | LSP | Subclasse substituível sem quebrar contrato | Quadrado não deve quebrar comportamento esperado de Retângulo |
| Segregação de Interfaces | ISP | Interfaces específicas por cliente | Separar `Desenvolvedor` de `Gestor` em vez de interface única |
| Inversão de Dependência | DIP | Dependa de abstrações, não de concretos | `EmissorRelatorio` depende de `RepositorioDados`, não de `BancoPostgres` |

> [!tip] Resumo em uma frase
> SOLID é um conjunto de cinco princípios que, juntos, garantem que o código seja fácil de estender, difícil de quebrar e simples de manter — o tipo de qualidade que sistemas previdenciários críticos como os da DATAPREV exigem.

---

## 11. Próximos passos

O DIP é a porta de entrada para um dos mecanismos mais importantes do ecossistema Java corporativo: a **Injeção de Dependência**. Quando você usar `@Autowired` ou `@Qualifier` no Spring, estará aplicando DIP na prática — a classe depende de uma abstração (interface), e o container do [[Frameworks-Java|Spring]] fornece a implementação concreta. Não se aprofunde agora; registre apenas que DIP e Injeção de Dependência são conceitos ligados.

Além disso, os princípios SOLID alimentam diretamente os [[Padroes-de-Projeto-e-Arquitetura|Padrões de Projeto]] (tópico 6): Strategy, Factory, Dependency Injection, Observer — todos são soluções concretas que aplicam um ou mais princípios SOLID. Conhecer SOLID é entender o *porquê* por trás dos padrões.

Para revisar o contexto completo do tópico, consulte o índice [[Paradigma-Orientado-a-Objetos]].
