# Classe e Objeto

> [!info] Metadados
> **Disciplina:** Desenvolvimento de Sistemas
> **Bloco:** 4.1 — Desenvolvimento de Sistemas (FASE 4 — Núcleo de Desenvolvimento)
> **Tópico:** 2. Paradigma Orientado a Objetos — Classe e Objeto
> **Subtópicos:** Conceitos (classe, objeto, instância, identidade, estado, comportamento) · Ponte com o banco de dados (tabela ↔ classe, linha ↔ objeto, coluna ↔ atributo)
> **Pré-requisitos:** [[Java-Fundamentos-da-Linguagem|Java — Fundamentos da Linguagem]] (sintaxe, `new`, classe como molde) e [[Raciocinio-Matematico-Aplicado|Raciocínio Lógico Matemático]] (lógica de programação) e [[Fundamentos-e-Modelagem|Banco de Dados]] (modelagem de entidades e relacionamentos)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-09-17

---

## 1. Por que estudar classe e objeto?

Na subnota anterior ([[Java-Fundamentos-da-Linguagem|Java — Fundamentos da Linguagem]]), você aprendeu a **sintaxe** da linguagem: variáveis, operadores, controle de fluxo e a forma básica de uma classe. Lá, a classe apareceu como um "recipiente" do código — algo que o compilador exige para organizar as instruções. O `new` apareceu de forma prática, como no `new Scanner(System.in)`, mas sem aprofundamento.

Agora é hora de entender **por que** aquela estrutura existe. A classe e o objeto não são apenas sintaxe — são o **modelo mental** sobre o qual quase todo software moderno é construído. O `new` que você viu na nota anterior não é apenas uma palavra-chave: ele **instancia** um objeto a partir de um molde, criando algo concreto com estado próprio, comportamento próprio e identidade própria.

Pense no contexto DATAPREV. A empresa processa dados da seguridade social: o **CNIS** (Cadastro Nacional de Informações Sociais), sistemas de **benefícios**, de **consignação**, de **folha de pagamento**. Nesses domínios, tratamos de cidadãos, vínculos empregatícios, contribuições, benefícios, órgãos concedentes. Cada uma dessas "coisas" do mundo real vira um **objeto** no software. E é exatamente aí que o paradigma orientado a objetos se conecta com aquilo que você já estudou.

Volte um instante à subnota anterior ([[Sintaxe-Essencial-de-Java|Sintaxe Essencial de Java]]). Quando você escreveu `Scanner leitor = new Scanner(System.in)`, o que era aquele `new`? Eram duas coisas ao mesmo tempo: você estava **criando um objeto** da classe `Scanner` (um leitor de dados ligado ao teclado) e guardando a referência a ele na variável `leitor`. Naquele momento, o `new` era apenas "a forma de criar um Scanner" — sem o conceito de molde por trás. Agora você verá que esse mesmo `new` é o verbo **instanciar**: aplicar o molde (classe) para gerar um exemplar concreto (objeto). Se você entendeu `new Scanner(System.in)`, entenderá `new Beneficiario(...)`, `new Vinculo(...)` e `new Contribuicao(...)` — a mesma mecânica, aplicada às entidades do domínio previdenciário.

> [!question] Pergunta orientadora
> Na modelagem conceitual de [[Fundamentos-e-Modelagem|Banco de Dados]], você desenhou entidades como CLIENTE, PEDIDO e PRODUTO, com atributos e relacionamentos. Será que existe uma forma de representar essas mesmas entidades no código Java, de modo que cada linha da tabela vire um objeto com comportamento? A resposta é sim — e essa ponte entre o mundo do banco e o mundo do código é uma das ideias centrais desta nota.

---

## 2. Objeto: a unidade do mundo real

Um **objeto** é a representação, no software, de uma *coisa* do mundo real (ou conceitual) que possui três características fundamentais: **estado**, **comportamento** e **identidade**.

**Estado** são os dados que o objeto guarda em um determinado momento — os seus **atributos**. No banco de dados, o estado de uma ocorrência corresponde aos valores das **colunas** daquela linha. Um beneficiário do INSS, por exemplo, tem estado definido por atributos como `nome`, `CPF`, `matrícula`, `rendaMensal` e `lotação`. Cada objeto carrega seus próprios valores para esses atributos — um beneficiário pode ter renda de R$ 3.200,00; outro, R$ 5.800,00.

**Comportamento** é o que o objeto *sabe fazer* — os seus **métodos**. Métodos são operações que podem consultar ou alterar o estado do objeto, ou produzir resultados. No caso do beneficiário do INSS, os métodos poderiam ser `calcularMargemConsignavel()`, `consultarBeneficio()`, `atualizarCadastro()`. Note a diferença essencial em relação à programação procedural: no modelo procedural, os dados ficavam em estruturas separadas e as funções operavam sobre elas *de fora*. No paradigma orientado a objetos, dados e comportamento vivem juntos, na mesma unidade.

Veja a diferença na prática. Na abordagem procedural, o dado e a operação vivem separados — a função calcula *de fora*, recebendo o dado como parâmetro:

```java
// Programação procedural: dados e funções separados
String nome = "José";
double rendaMensal = 3200.0;
double margem = calcularMargemConsignavel(rendaMensal, 30.0);  // função "de fora"
```

Na abordagem orientada a objetos, o objeto carrega **o dado e a operação juntos** — quem calcula a margem é o próprio objeto, usando seu próprio estado:

```java
// Orientação a objetos: o objeto reúne dado e comportamento
Beneficiario jose = new Beneficiario("José", "123.456.789-00", 3200.0);
double margem = jose.calcularMargemConsignavel(30.0);  // o próprio objeto sabe calcular
```

No primeiro caso, o programador precisa caçar `calcularMargemConsignavel` em algum lugar do código e lembrar-se de lhe passar os dados corretos. No segundo, o comportamento está **dentro** do conceito que ele representa: quem é beneficiário sabe (tem método para) calcular sua margem. É essa coesão — estado e comportamento na mesma unidade — que torna o paradigma orientado a objetos adequado para sistemas grandes e em constante evolução, como os da DATAPREV.

> [!question] Por que juntar dado e comportamento?
> Em um sistema com milhares de linhas de código procedural, como saber qual função opera sobre qual estrutura de dados? E quando a regra de negócio muda, quantos pontos precisam ser atualizados? O POO responde: o objeto é o ponto único onde o dado e suas regras convivem — a mudança de regra se concentra no método, e o dado nunca anda solto pelo sistema.

**Identidade** é o que torna o objeto único e distinguível dos demais da mesma categoria. Dois objetos podem ter o mesmo estado (mesmos valores nos atributos), mas ainda assim serem **objetos diferentes** — cada um ocupa uma posição distinta na memória e possui sua própria existência. No banco de dados, a identidade corresponde à **chave primária**: dois registros podem ter o mesmo nome, mas só um pode ter o CPF `123.456.789-00`.

Pense em dois beneficiários com o nome "Maria Souza". No mundo real, são duas pessoas distintas, mesmo que compartilhem o mesmo nome. No software, são dois objetos com a mesma classe (`Beneficiario`), mas com **identidade diferente** — um pode ter CPF `111.222.333-44` e outro `999.888.777-66`. É a identidade que garante que um não se confunde com o outro.

> [!tip] Resumo dos três pilares do objeto
> | Característica | O que é | No banco de dados |
> |---|---|---|
> | **Estado** | Valores dos atributos em um momento dado | Colunas da linha |
> | **Comportamento** | Métodos que o objeto sabe executar | Regras de negócio (constraints, triggers) |
> | **Identidade** | O que torna o objeto único, independente dos valores | Chave primária |

---

## 3. Classe: o molde

Se o objeto é a *peça concreta*, a **classe** é o *molde* — o template, a planta, a receita que define **quais** atributos e métodos os objetos daquela categoria terão. A classe não é um objeto em si; ela é a definição abstrata que permite **criar** objetos.

A analogia clássica que costuma cair em prova é da receita de bolo: a **classe** é a receita (o molde); o **objeto** é o bolo de fato assado com ela. Uma mesma receita pode produzir milhares de bolos diferentes — cada bolo com sua cor, sabor e tamanho próprios (os valores dos atributos). Mas todos seguiram a mesma receita (a mesma classe).

No Java, a classe define:
- os **atributos** (quais dados os objetos terão);
- os **métodos** (quais operações os objetos saberão executar);
- o **construtor** (o "mecanismo de fabricação" que roda quando o objeto é criado).

O operador `new` é o comando que **instancia** a classe — ou seja, cria um objeto concreto a partir do molde. Cada chamada de `new` gera um novo objeto com seu próprio estado.

Considere o exemplo de uma classe `Beneficiario`, que modela um beneficiário de benefício previdenciário (como o auxílio-doença ou aposentadoria):

```java
// Classe (molde) — define quais atributos e métodos existirão
public class Beneficiario {
    // atributos (estado)
    private String nome;
    private String cpf;
    private double rendaMensal;

    // construtor: cria (instancia) o objeto preenchendo o estado
    public Beneficiario(String nome, String cpf, double rendaMensal) {
        this.nome = nome;
        this.cpf = cpf;
        this.rendaMensal = rendaMensal;
    }

    // método (comportamento)
    public double calcularMargemConsignavel(double margem) {
        return this.rendaMensal * (margem / 100.0);
    }
}

// Uso: criar (instanciar) dois objetos a partir da mesma classe
Beneficiario jose = new Beneficiario("José da Silva", "123.456.789-00", 3200.00);
Beneficiario maria = new Beneficiario("Maria Souza", "987.654.321-00", 4100.00);
```

O que acontece aqui? A classe `Beneficiario` é o molde: ela diz que todo beneficiário terá `nome`, `cpf` e `rendaMensal`, e saberá calcular a margem consignável. Cada chamada de `new Beneficiario(...)` cria um **objeto distinto** — o `jose` tem renda de R$ 3.200,00; a `maria`, R$ 4.100,00. Mesmo que dois objetos tenham exatamente os mesmos valores, eles continuam sendo objetos diferentes (identidade distinta).

Repare em dois detalhes do código que caem em prova:

### O construtor

Um método especial com o mesmo nome da classe (`public Beneficiario(...)`), que não tem tipo de retorno e roda automaticamente no momento do `new`. Ele existe para **preencher o estado inicial** do objeto — é o "molde sendo preenchido" no instante da criação.

### O `this`

Dentro de métodos de instância e construtores, `this` é uma referência que aponta para o **objeto que está executando aquele código naquele momento**. Não é um objeto novo, nem uma variável especial que o compilador cria — é o próprio objeto corrente, acessado pelo nome.

Para entender na prática, acompanhe as duas chamadas de método:

```java
jose.calcularMargemConsignavel(30.0);   // ← this É o jose
maria.calcularMargemConsignavel(30.0);  // ← this É a maria
```

O código-fonte do método é **o mesmo** para ambos. Mas, dentro de cada chamada, `this` aponta para um objeto diferente:

| Chamada | `this` dentro do método | `this.rendaMensal` |
|---|---|---|
| `jose.calcularMargemConsignavel(30.0)` | `jose` | 3200.00 |
| `maria.calcularMargemConsignavel(30.0)` | `maria` | 4100.00 |

É por isso que o mesmo método retorna valores diferentes: o molde (classe) é idêntico; o que muda são os valores que cada objeto carrega em seus atributos — acessados via `this`.

Agora decomponha a linha do construtor, parte por parte:

```java
this.nome = nome;
// ──────   ─────
// atributo   parâmetro recebido
```

Sem o `this`, o Java veria `nome = nome` — um parâmetro sendo atribuído a ele mesmo. O atributo do objeto ficaria sem valor. O `this` resolve essa ambiguidade dizendo ao compilador: *"à esquerda está o meu atributo; à direita está o valor que recebi"*.

> [!warning] PEGADINHA — o que `this` realmente faz
> **A armadilha:** afirmar que "`this` é um objeto criado pelo construtor", "`this` é uma variável global" ou "`this` é o molde da classe".
> **O raciocínio errado:** tratar `this` como algo separado do objeto.
> **Como se proteger:** `this` é o **próprio objeto em execução** — ele só aparece dentro de métodos de instância e construtores. Regra prática: onde houver `this`, há um objeto concreto sendo manipulado, nunca a classe como um todo.

> [!question] O que muda entre um objeto e outro?
> Se `jose` e `maria` vêm da mesma classe, por que `jose.calcularMargemConsignavel(30.0)` e `maria.calcularMargemConsignavel(30.0)` podem retornar valores diferentes? Porque o método usa `this.rendaMensal` — o estado de cada objeto. A classe fornece o molde do método; o objeto fornece os valores. É por isso que dizemos que a classe é a **abstração** (a definição, sem valores próprios) e o objeto é o **exemplar concreto** (com valores).

> [!important] Classe vs. objeto — a armadilha favorita da FGV
> A banca adora inverter os papéis. A alternativa mais perigosa diz que "o objeto é o molde da classe" ou que "a classe é a instância de um objeto". **Sempre pergunte: é a definição abstrata (classe) ou é um exemplar concreto com valores (objeto)?**
> - **Classe** = molde, definição, abstrato, "uma só por categoria"
> - **Objeto** = instância, peça concreta, com valores, "vários possíveis"
>
> Se a alternativa inverter "molde" e "instância", ela está errada — marque e siga em frente.

---

## 4. A ponte com o banco de dados

Na [[Fundamentos-e-Modelagem|modelagem conceitual]] que você estudou na Fase 3, você desenhou entidades (como CLIENTE, PEDIDO, PRODUTO) com atributos e relacionamentos. O POO constrói a aplicação com a mesma visão, mas no código. A entidade do banco (uma tabela) e a classe do POO (um molde) são **leituras do mesmo mundo real**.

Essa ponte é fundamental porque, na prática, os sistemas da DATAPREV funcionam com bancos de dados relacionais: os dados vivem em tabelas; as regras de integridade são impostas por constraints e triggers; e os dados são consultados com SQL. Mas o código que processa esses dados é escrito em Java, no paradigma orientado a objetos. É preciso traduzir entre os dois mundos.

A tabela abaixo compara os conceitos lado a lado:

| Mundo do banco (Fundamentos e Modelagem) | Mundo do POO (código Java) | Exemplo DATAPREV |
|---|---|---|
| **Entidade** (conceitual) / **tabela** (lógico) | **Classe** | `Beneficiario` (classe) ↔ tabela `beneficiario` |
| **Ocorrência** / **tupla** (linha) | **Objeto** | Um beneficiário com CPF `123.456.789-00` ↔ uma linha na tabela |
| **Coluna** | **Atributo** | Coluna `renda_mensal` ↔ atributo `rendaMensal` |
| **Chave primária** | **Identidade** (e campo `id`) | `cpf` como PK ↔ o que distingue cada objeto |
| **Relacionamento 1:N / N:M** | **Referência entre objetos** / coleções | Um órgão concedente tem vários benefícios ↔ uma lista de objetos `Beneficio` dentro de `OrgaoConcedente` |
| **Regra de negócio** (constraint / trigger) | **Regra nos métodos** da classe | `CHECK (renda > 0)` ↔ validação no construtor |

Note o padrão: no banco, a integridade é imposta por estruturas externas (constraints, triggers, chaves estrangeiras). No POO, a integridade é imposta **dentro do próprio objeto**, via métodos controlados (encapsulamento — assunto que será detalhado nos [[Quatro-Pilares-do-POO|Quatro Pilares do POO]]). Os dois caminhos chegam ao mesmo resultado — dados consistentes e regras de negócio respeitadas — mas por vias diferentes.

Observe também a **tradução de nomes**. No banco relacional, a convenção usual é *snake_case*: `renda_mensal`, `data_nascimento`, `numero_beneficio`. No Java, a convenção é *camelCase*: `rendaMensal`, `dataNascimento`, `numeroBeneficio`. Não é apenas estética: quando a aplicação precisa conversar com o banco, alguém precisa traduzir `rendaMensal` ↔ `renda_mensal`, `Beneficiario` ↔ `beneficiario`. Essa tradução é feita manualmente por quem escreve o SQL ou automaticamente pelo framework de persistência — como você verá no tópico 3.

> [!question] Se banco e POO são a mesma visão, por que precisamos de um "tradutor"?
> Se a tabela e a classe descrevem a mesma entidade, bastaria "ligar uma na outra", não? O problema é que os dois mundos têm convenções diferentes: nomes diferentes (snake_case vs. camelCase), tipos diferentes (o banco usa `NUMERIC`, o Java usa `double`), e formas diferentes de representar relacionamentos (chaves estrangeiras vs. referências a objetos). Alguém precisa fazer essa tradução. No [[Java-Corporativo-JavaEE-JPA-Hibernate|Java Corporativo (tópico 3)]], o **JPA/Hibernate** automatizará exatamente essa ponte — por isso ela vale a pena ser fixada aqui.

> [!tip] Essa ponte é o mapa para o JPA/Hibernate
> No tópico 3 da fase ([[Java-Corporativo-JavaEE-JPA-Hibernate|JavaEE, JakartaEE, JPA e Hibernate]]), você verá como essa ponte é automatizada com anotações de mapeamento: cada *classe Java* vira uma *tabela*; cada *objeto* vira uma *linha*. Por enquanto, basta entender a analogia: se você desenhou uma entidade `Beneficiario` com colunas `nome`, `cpf` e `renda_mensal`, a classe Java correspondente terá os atributos `nome`, `cpf` e `rendaMensal`. A tradução é quase direta.

---

## 5. Como a FGV cobra

A FGV costuma apresentar este subtópico de duas formas: por **asserções verdadeiras/falsas** ("é correto afirmar que...") e por **questões de definição** ("assinale a afirmativa correta sobre classe e objeto"). Nos dois casos, o jogo é o mesmo: a banca oferece alternativas que **espelham** o conceito correto com uma palavra trocada. Se a definição correta diz "a classe é o molde que define atributos e métodos", as alternativas erradas dirão "molde que define valores", "instância que define métodos", e assim por diante. A estratégia é decorar os pares conceituais e testar cada alternativa contra eles.

### 5.1 Palavras-chave

Quando você encontrar uma questão sobre classe e objeto, fique atento a esses termos:

| Palavra-chave | O que sinaliza na prova |
|---|---|
| **classe** | Molde, definição, template — é a planta, não o produto final |
| **objeto** | Instância concreta de uma classe — tem valores, ocupa memória |
| **instância** | Sinônimo de objeto; instanciar = criar um objeto com `new` |
| **molde** | Sinônimo de classe — a receita, não o bolo |
| **estado** | Valores dos atributos em um momento dado |
| **comportamento** | Métodos que o objeto sabe executar |
| **identidade** | O que torna o objeto único, mesmo com mesmos valores (chave primária) |
| **construtor** | Método especial que inicializa o objeto no momento do `new` |
| **this** | Referência ao objeto corrente — desfaz ambiguidade entre atributo e parâmetro |

### 5.2 As pegadinhas no padrão "armadilha → raciocínio errado → proteção"

> [!warning] Pegadinha 1 — "o objeto é o molde da classe"
> **A armadilha:** a alternativa afirma que "o objeto é o molde a partir do qual a classe é criada" ou expressão equivalente que inverte a relação.
> **O raciocínio errado:** confundir a direção: pensar que o objeto é anterior à classe.
> **Como se proteger:** a **classe** é o molde; o **objeto** é o que sai do molde. Sempre pergunte: *estou falando da definição (classe) ou do exemplar concreto (objeto)?*

> [!warning] Pegadinha 2 — "classe e objeto são a mesma coisa"
> **A armadilha:** a alternativa trata classe e objeto como sinônimos — "classe e objeto significam a mesma coisa em POO".
> **O raciocínio errado:** achar que, porque ambos são conceitos relacionados, são intercambiáveis.
> **Como se proteger:** são conceitos **distintos** e complementares. A classe é a definição (uma por categoria); o objeto é a instância (vários possíveis). A relação entre eles é de **generação**: a classe gera (instancia) objetos. Não confunda "se relacionam" com "são iguais".

> [!warning] Pegadinha 3 — "a classe é a instância"
> **A armadilha:** a alternativa diz que "a classe é a instância concreta de um objeto".
> **O raciocínio errado:** trocar os termos — pensar que a classe é o que tem valores concretos.
> **Como se proteger:** a **instância** é o objeto; a classe é o **molde**. A classe não tem valores concretos — ela apenas define quais atributos existirão. Quem tem valores é o objeto.

> [!warning] Pegadinha 4 — identidade vs. igualdade de estado
> **A armadilha:** a alternativa afirma que "dois objetos com os mesmos atributos são o mesmo objeto".
> **O raciocínio errado:** confundir igualdade de estado (mesmos valores) com identidade (mesmo objeto na memória).
> **Como se proteger:** dois objetos podem ter o mesmo nome, o mesmo CPF e a mesma renda — e ainda assim serem **objetos diferentes**, cada um com sua identidade (sua posição na memória). A identidade é o que distingue um do outro, independentemente dos valores.

---

## 6. Questões-modelo (pegada FGV)

> [!example] Questão 1 — classe e objeto: conceitos fundamentais
> Sobre classe e objeto no paradigma orientado a objetos, assinale a alternativa correta:
> (A) Uma classe é um objeto concreto que ocupa memória na JVM.
> (B) Um objeto é o molde a partir do qual classes são criadas.
> (C) Uma classe define os atributos e métodos que os objetos daquela categoria terão.
> (D) Dois objetos com os mesmos valores nos atributos são necessariamente o mesmo objeto.
> (E) A identidade de um objeto é determinada exclusivamente pelo valor do seu primeiro atributo.
>
> **Gabarito comentado:** (C). A classe é o molde que define quais atributos e métodos existirão; os objetos são as instâncias concretas criadas a partir desse molde. (A) é falso: a classe é uma definição abstrata — quem ocupa memória é o objeto. (B) inverte a relação: é a classe que gera objetos, e não o contrário. (D) confunde igualdade de estado com identidade — dois objetos com mesmos valores podem ser distintos. (E) inventa uma regra: a identidade é inerente ao objeto e não depende de um atributo específico.

> [!example] Questão 2 — ponte com o banco de dados
> Considere uma tabela `beneficiario` no banco de dados relacional com as colunas `id` (chave primária), `nome`, `cpf` e `renda_mensal`. Qual a correspondência correta entre os conceitos do banco e do paradigma orientado a objetos?
> (A) Tabela ↔ Objeto; Coluna ↔ Método; Chave primária ↔ Construtor.
> (B) Tabela ↔ Classe; Linha ↔ Objeto; Coluna ↔ Atributo.
> (C) Tabela ↔ Atributo; Linha ↔ Classe; Coluna ↔ Objeto.
> (D) Tabela ↔ Método; Linha ↔ Atributo; Coluna ↔ Classe.
> (E) Tabela ↔ Classe; Linha ↔ Classe; Coluna ↔ Objeto.
>
> **Gabarito comentado:** (B). A tabela corresponde à classe (o molde que define a estrutura); cada linha (tupla) é um objeto (uma instância concreta com valores); cada coluna é um atributo do objeto. (A) troca quase tudo; (C) e (D) embaralham os termos de forma absurda; (E) erra ao dizer que linha é classe — a linha é o objeto, não o molde.

---

## 7. Revisão rápida

| Conceito | Ponto-chave | Erro mais comum em prova |
|---|---|---|
| **Classe** | Molde/definição que define atributos e métodos | Confundir com "instância" ou "objeto concreto" |
| **Objeto** | Instância concreta de uma classe; tem valores e identidade | Dizer que "o objeto é o molde" |
| **Instância** | Sinônimo de objeto; criar instância = usar `new` | Trocar com "classe" |
| **Estado** | Valores dos atributos em um momento dado | Confundir estado (valores) com identidade (o que é único) |
| **Comportamento** | Métodos que o objeto sabe executar | Achar que comportamento são apenas os atributos |
| **Identidade** | O que torna o objeto único, mesmo com mesmos valores | Confundir com igualdade de atributos |
| **Tabela ↔ Classe** | Tabela = molde; linha = objeto; coluna = atributo | Inverter: dizer que tabela é objeto |
| **Chave primária ↔ Identidade** | A PK é a manifestação da identidade no banco | Achar que identidade é um atributo qualquer |

> [!tip] O erro que mais derruba na prova
> É a **inversão dos papéis**: chamar a classe de "instância" e o objeto de "molde". Sempre que a questão mencionar os dois conceitos, faça o teste de uma frase só — *"esta frase está falando da definição (classe) ou de um exemplar concreto com valores (objeto)?"*. Se a resposta for "definição", a palavra certa é **classe**; se for "exemplar concreto", é **objeto/instância**. Esse único teste resolve a maior parte das alternativas erradas.

> [!note] Três frases para levar para a prova
> 1. A **classe** é o molde — define *quais* atributos e métodos existirão; não tem valores.
> 2. O **objeto** é a instância concreta — tem *quais valores* cada atributo recebeu e existe de forma única (identidade).
> 3. No banco: **tabela ↔ classe**, **linha ↔ objeto**, **coluna ↔ atributo**, **chave primária ↔ identidade**.

---

## 8. Próximos passos

Com a classe como molde e o objeto como instância concreta estabelecidos, o próximo passo natural é entender os **quatro pilares do paradigma orientado a objetos**: abstração, encapsulamento, herança e polimorfismo — os princípios que definem *como* a classe deve ser projetada para produzir código coeso, desacoplado e extensível.

Dois conceitos que complementam a classe — **interface** (contrato de comportamento) e **classe abstrata** (molde incompleto que não pode ser instanciado) — fazem sentido pleno ao lado de herança e polimorfismo. Por isso, eles serão ensinados na subnota 2 ([[Quatro-Pilares-do-POO]]), imediatamente após a herança e o polimorfismo, respectivamente. Lá você verá que a herança é a base da classe abstrata (`extends` liga subclasse à superclasse abstrata) e que o polimorfismo ganha efetividade quando operamos por meio de interfaces comuns.

Esses mecanismos também serão **exemplificados** no [[Principios-SOLID]] — especialmente no OCP (extensão sem modificação), no ISP (segregação de interfaces) e no DIP (depender de abstrações, não de implementações concretas). Não se adiante agora; apenas registre a conexão: o vocabulário de "contrato" e "molde incompleto" será usado lá com nomes de princípios.

Lembre-se: esta subnota é parte do índice [[Paradigma-Orientado-a-Objetos]], que reúne todos os conceitos do tópico 2 — da classe e do objeto (aqui) aos quatro pilares, ao SOLID, ao Clean Code e à análise estática com SonarQube. Cada subnota constrói sobre a anterior, e o vocabulário definido aqui será usado em todos os tópicos seguintes — especialmente no [[Java-Corporativo-JavaEE-JPA-Hibernate|Java Corporativo (tópico 3)]], onde a ponte entre classe e tabela será automatizada com JPA e Hibernate.
