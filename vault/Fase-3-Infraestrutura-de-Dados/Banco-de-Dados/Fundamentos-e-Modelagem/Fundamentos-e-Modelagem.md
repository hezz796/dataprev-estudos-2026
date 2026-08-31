# Fundamentos e Modelagem

> [!info] Metadados
> **Disciplina:** Banco de Dados
> **Bloco:** 3.1 — Banco de Dados (FASE 3 — Infraestrutura de Dados)
> **Tópico:** 1. Fundamentos e Modelagem
> **Subtópicos:** Conceito de banco de dados e SGBD · Abordagens (hierárquica, rede, relacional, orientada a objetos) · Modelagem conceitual (entidade, atributo, relacionamento, cardinalidade) · Modelagem lógica (modelo relacional, chaves primárias e estrangeiras) · Modelagem física (indexação, particionamento, tablespaces)
> **Pré-requisitos:** [[Raciocinio-Matematico-Aplicado|Raciocínio Lógico Matemático]] (modelagem, conjuntos, funções) e [[LGPD-Lei-Geral-de-Protecao-de-Dados|Legislação/Segurança]] (privacidade, dados sensíveis)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-28

---

## 1. Por que estudar banco de dados?

Esta nota abre a FASE 3 — Infraestrutura de Dados, e com ela começamos a percorrer a **corrente de dados** do edital: do banco de dados, o conhecimento seguirá para o desenvolvimento de sistemas, para a arquitetura avançada e para a segurança da informação. Tudo o que uma aplicação faz, em última instância, é **produzir, armazenar, recuperar e transformar dados**. Quem projeta sistemas sem entender onde e como os dados vivem constrói software frágil.

O contexto do seu cargo torna isso ainda mais concreto. A DATAPREV é uma empresa de tecnologia que presta serviços de processamento de dados para a seguridade social brasileira. Sistemas como o CNIS (Cadastro Nacional de Informações Sociais) trabalham com dezenas de milhões de registros de cidadãos: vínculos de trabalho, contribuições, benefícios. Boa parte desses registros é composta por **dados pessoais** — e uma fração deles, por **dados sensíveis** (informações de saúde, por exemplo). A [[LGPD-Lei-Geral-de-Protecao-de-Dados|LGPD]] impõe a quem armazena e processa esses dados um dever de segurança, de confidencialidade e de qualidade. O lugar onde esse dever se materializa tecnicamente é o banco de dados.

E por que o [[Raciocinio-Matematico-Aplicado|Raciocínio Lógico Matemático]] da Fase 1 é pré-requisito? Porque **modelar dados é descrever conjuntos e relações**. Uma entidade é um conjunto de "coisas" do mundo real; um relacionamento liga elementos de um conjunto a elementos de outro; a cardinalidade diz *quantos* elementos de um lado se conectam a *quantos* do outro. É a mesma matemática de conjuntos e funções que você já domina, agora aplicada a clientes, pedidos e produtos. A lógica também volta: a consistência de um banco de dados será constantemente descrita em termos de regras do tipo "se... então" — exatamente o que você treinou na Fase 1.

> [!question] Pergunta orientadora
> Se uma aplicação precisa apenas guardar informações e consultá-las depois, por que não usar simplesmente arquivos de texto? A resposta desta pergunta explica a existência dos bancos de dados — e a seção 2 a responde.

---

## 2. Conceito de banco de dados e SGBD

### 2.1 Dado, informação e banco de dados

Antes de definir banco de dados, é preciso distinguir **dado** de **informação** — distinção clássica de prova. **Dado** é um fato bruto, sem interpretação: o número "320,00", a sigla "PE", a data "2026-08-10". **Informação** é o dado processado, contextualizado, com significado: "o valor médio dos pedidos de agosto foi R$ 320,00". O mesmo dado pode alimentar várias informações; a interpretação é que transforma um no outro.

Um **banco de dados** é uma **coleção integrada, organizada e persistente de dados relacionados**, que representa uma parte do mundo real — chamada de *mini-mundo* ou *universo de discurso* — e que atende a uma determinada comunidade de usuários e aplicações. Três palavras dessa definição são as favoritas da banca:

- **integrada:** os dados são tratados como um todo, com redundância controlada, em vez de arquivos isolados e repetidos;
- **organizada:** existe uma estrutura (um modelo) que descreve como os dados se relacionam — não é uma pilha de arquivos soltos;
- **persistente:** os dados sobrevivem ao término dos programas que os utilizam; ficam guardados de forma duradoura.

### 2.2 SGBD — o software por trás do banco

O **SGBD (Sistema Gerenciador de Banco de Dados)** é o **software** que define, armazena, recupera, atualiza e administra os dados do banco. Oracle, MySQL, PostgreSQL, SQL Server, MariaDB são exemplos de SGBDs. O banco de dados é o **dado**; o SGBD é o **programa** que o gerencia. Guarde essa separação com carinho: ela é uma das pegadinhas mais rentáveis do edital.

> [!warning] PEGADINHA — banco de dados ≠ SGBD
> A banca pergunta: "O MySQL é um banco de dados?" Tecnicamente, o MySQL é um **SGBD**; o banco de dados é a coleção de dados que o MySQL armazena e gerencia. Quando a FGV escreve "SGBD é o software que gerencia o banco de dados", a afirmativa está certa; quando escreve "banco de dados é o software", está errada. Na dúvida, pergunte-se: *é um programa?* Se sim, é SGBD (ou parte dele), não o banco.

Um SGBD oferece, tipicamente, as seguintes capacidades — e cada uma delas já caiu em prova:

- **catálogo ou dicionário de dados:** armazena os **metadados**, ou seja, os dados sobre os dados — o nome das tabelas, das colunas, dos tipos, das restrições. É o SGBD "sabendo" o que existe no banco;
- **controle de concorrência:** permite que vários usuários acessem e modifiquem dados ao mesmo tempo, de forma controlada;
- **controle de segurança e privacidade:** gerencia usuários, perfis e permissões de acesso;
- **controle de integridade:** aplica regras que mantêm os dados coerentes (como as chaves que veremos na seção 5);
- **backup e recuperação:** protege os dados contra falhas de software, hardware ou operacionais.

Vale a pena comparar com o mundo dos arquivos tradicionais: sem SGBD, cada programa precisa conhecer a estrutura física do arquivo, repetir a lógica de leitura e escrita, e administrar sozinho o acesso concorrente. Com o SGBD, o programa conversa com o banco em um nível **abstrato** — "dê-me os pedidos deste cliente" — e o SGBD resolve onde e como os dados estão guardados. Essa separação entre o que o programa enxerga e o que existe em disco chama-se **independência de dados**. Ela é a mãe dos três níveis de modelagem, que abrem a próxima seção.

### 2.3 Os três níveis: conceitual, lógico e físico

Construir um banco de dados é traduzir o mundo real em estrutura. Essa tradução acontece em **três níveis de abstração**, e esta nota inteira caminha por eles — por isso vale apresentá-los já:

| Nível | Pergunta que responde | Produto típico | Depende do SGBD? |
|---|---|---|---|
| **Conceitual** | O que o negócio precisa guardar? | Modelo entidade-relacionamento (DER) | Não |
| **Lógico** | Como estruturar no modelo escolhido (o relacional)? | Esquema relacional: tabelas, chaves | Depende do *modelo*, não do *produto* |
| **Físico** | Como armazenar em disco no SGBD escolhido? | Índices, partições, tablespaces | Sim |

O nível conceitual descreve o **quê**; o lógico, o **como estruturar**; o físico, o **como guardar**. A FGV adora misturar essas perguntas — e você vai perceber que saber dizer "isso é decisão de nível conceitual" ou "isso é decisão de nível físico" resolve meia questão.

---

## 3. Abordagens de banco de dados

Chamamos de **abordagem** (ou **modelo de dados**) o paradigma usado para representar e organizar os dados. A história dos bancos de dados é a história dessas abordagens, e a banca costuma cobrar a relação entre cada uma e sua estrutura característica.

- **Modelo hierárquico:** organiza os dados em uma **árvore** — cada registro tem um único "pai" e pode ter vários "filhos". A navegação começa sempre pela raiz, seguindo os ponteiros pai-filho. Era rápido para consultas que seguiam a hierarquia natural, mas rígido: um relacionamento N:M exigia duplicar registros. O exemplo histórico mais famoso é o IMS, da IBM.
- **Modelo de rede:** substitui a árvore por um **grafo** — um registro pode participar de vários "conjuntos" e ter muitos relacionamentos, inclusive N:M, ligados por ponteiros. Foi padronizado pelo CODASYL. Mais flexível que o hierárquico, porém de navegação complexa: o programador precisava percorrer os ponteiros manualmente.
- **Modelo relacional:** proposto por **Edgar Codd** em 1970, organiza os dados em **tabelas (relações)** com linhas e colunas, e conecta as tabelas por **valores de chave** — não por ponteiros. Sua base matemática (a teoria de conjuntos e a lógica) permite consultas **declarativas**: o usuário diz *o que* quer, e o sistema descobre *como* obter. É o modelo dominante até hoje e o alicerce de todo o restante do Bloco 3.1.
- **Modelo orientado a objetos:** trata cada registro como um **objeto**, com identidade própria, atributos e comportamentos (métodos), e suporta conceitos como herança. Fez sentido para domínios complexos, mas não alcançou o domínio de mercado do relacional — e, na prática, o paradigma de objetos reaparece na Fase 4 sob a forma de **mapeamento objeto-relacional (ORM)**, tema que será estudado lá.

| Abordagem | Estrutura | Como liga os dados | Vantagem | Limitação | Exemplo típico |
|---|---|---|---|---|---|
| Hierárquica | Árvore (pai-filho) | Ponteiros | Consultas rápidas pela raiz | Rigidez; N:M exige duplicação | IMS (IBM) |
| Rede | Grafo (nós e arestas) | Ponteiros e conjuntos | N:M com liberdade | Navegação manual complexa | CODASYL / IDMS |
| Relacional | Tabelas (linhas e colunas) | Valores de chave (chave estrangeira) | Simplicidade, base matemática, independência | Consultas complexas podem exigir muitas junções | Oracle, MySQL, PostgreSQL, SQL Server |
| Orientada a objetos | Objetos (dados + métodos) | Identidade e referências | Modela domínios complexos | Mercado reduzido; integração difícil | SGBDs OO (conceitual) |

> [!note] Por que o resto do bloco é relacional?
> O edital do DATAPREV é, no seu núcleo, um edital de **banco relacional**: SQL, transações, normalização — tudo parte do modelo de Codd. As abordagens hierárquica, de rede e orientada a objetos aparecem em prova quase sempre em questões de **associação**: *"qual modelo organiza os dados em árvore?"* (hierárquico), *"qual modelo usa grafo?"* (rede). Memorize a estrutura-chave de cada uma e o modelo relacional será o seu ponto de retorno para todo o bloco.

---

## 4. Modelagem conceitual

### 4.1 O que é a modelagem conceitual

A **modelagem conceitual** é o primeiro nível da tradução: ela descreve, em linguagem próxima do usuário e do analista de negócio, **quais dados o negócio precisa guardar e como eles se relacionam** — sem nenhuma preocupação com tecnologia. Neste nível não existe "tabela", "coluna", "índice" nem "SGBD"; existe *cliente*, *pedido*, *produto*. O produto clássico dessa etapa é o **DER — Diagrama Entidade-Relacionamento** (ou o modelo entidade-relacionamento *MER*, que o DER desenha).

> [!question] Por que modelar antes de implementar?
> Porque a estrutura de um banco é cara de mudar depois que os dados começam a entrar. Corrigir uma tabela mal desenhada no início custa pouco; corrigi-la com dez anos de dados acumulados custa muito. A modelagem conceitual é o momento de acertar o desenho — e é também um dos assuntos mais cobrados pela FGV, porque exige interpretação de enunciado: a banca descreve as regras de negócio em texto e pede que você identifique entidades, atributos, relacionamentos e cardinalidades.

### 4.2 Entidade e atributo

**Entidade** é qualquer coisa (objeto, pessoa, conceito) do mundo real com **existência própria** e que interessa ao negócio. Pense nelas como **conjuntos**: a entidade CLIENTE é o conjunto de todos os clientes; a entidade PEDIDO, o conjunto de todos os pedidos. Uma **ocorrência** (instância) da entidade é um elemento desse conjunto — um cliente específico, um pedido específico.

Dois tipos de entidade aparecem em prova:

- **entidade forte:** existe por conta própria, sem depender de outra — CLIENTE, PRODUTO;
- **entidade fraca:** só existe em função de outra — DEPENDENTE só existe ligado a um FUNCIONÁRIO; ITEM_PEDIDO só existe ligado a um PEDIDO.

**Atributo** é uma propriedade da entidade: CLIENTE tem *nome*, *email*, *telefone*; PEDIDO tem *data*, *valor total*. A classificação clássica dos atributos:

| Tipo | Característica | Exemplo |
|---|---|---|
| Simples vs. composto | indivisível vs. decomposto em partes | `nome` (simples) vs. `endereço` = rua + número + bairro (composto) |
| Monovalorado vs. multivalorado | um único valor vs. vários valores | `cpf` (monovalorado) vs. `telefone` (multivalorado) |
| Derivado | calculado a partir de outros | `idade`, derivada de `data_nascimento` |

> [!note] Palavras-chave da modelagem conceitual
> O atributo **multivalorado** (ex.: "telefones" de um cliente) é um favorito da banca. No modelo conceitual ele é permitido; no modelo relacional ele será tratado — como você verá na nota de [[Normalizacao]], a **1FN** impedirá grupos repetitivos e transformará esse atributo em uma tabela própria. Guarde apenas a ponte por enquanto.

### 4.3 Relacionamento e cardinalidade

**Relacionamento** é a associação entre duas ou mais entidades — é o verbo do modelo: CLIENTE **realiza** PEDIDO; PEDIDO **contém** PRODUTO; FUNCIONÁRIO **trabalha em** DEPARTAMENTO. Um relacionamento pode ter **atributos próprios**: a associação entre PEDIDO e PRODUTO tem o atributo `quantidade` — não faz sentido dizer que a quantidade é "do pedido" nem "do produto"; ela é do relacionamento *contém*.

A **cardinalidade** de um relacionamento diz **quantas ocorrências de uma entidade podem se relacionar com quantas ocorrências da outra**. Ela é a informação mais cobrada da modelagem conceitual, e a forma de lê-la é sempre *de um lado, depois do outro*:

- **1:1 (um para um):** cada ocorrência de A se relaciona com no máximo uma de B, e vice-versa. Ex.: cada MEI tem um único CNPJ; cada CNPJ pertence a um único MEI.
- **1:N (um para muitos):** cada ocorrência de A se relaciona com várias de B, mas cada B se relaciona com **um único** A. Ex.: um CLIENTE realiza vários PEDIDOS, mas cada PEDIDO pertence a um único CLIENTE.
- **N:M (muitos para muitos):** cada A pode se relacionar com vários B e cada B com vários A. Ex.: um PEDIDO contém vários PRODUTOS e um PRODUTO aparece em vários PEDIDOS.

A conexão com o [[Raciocinio-Matematico-Aplicado|RLM]] é direta e poderosa: entidades são conjuntos; o relacionamento associa elementos de um conjunto a elementos de outro; e a cardinalidade descreve *quantos elementos* se correspondem. Um relacionamento **1:N** se comporta como uma **função** do conjunto dos N para o conjunto dos 1 — cada elemento do lado N tem exatamente um correspondente do lado 1. Você já sabe, da Fase 1, que funções não admitem um mesmo elemento do domínio com duas imagens diferentes: é exatamente essa a "regra do negócio" que o 1:N impõe.

> [!example] Modelando uma loja — o exemplo que vamos carregar pela nota
> Uma loja deseja registrar clientes, pedidos e produtos. As regras de negócio:
> - cada cliente pode fazer **vários** pedidos; cada pedido pertence a **um único** cliente;
> - cada pedido pode conter **vários** produtos; cada produto pode aparecer em **vários** pedidos;
> - de cada produto em um pedido, interessa a **quantidade**.
>
> O modelo conceitual fica assim:
>
> ```text
> CLIENTE (cod_cliente, nome, email, telefone)
>   │ 1
>   │
>   │ N
> PEDIDO (num_pedido, data_venda, valor_total)
>   │ N
>   │ M
> PRODUTO (cod_produto, descricao, preco_unitario)
>   com atributo QUANTIDADE no relacionamento PEDIDO-PRODUTO
> ```
>
> CLIENTE–PEDIDO é **1:N** (um cliente, muitos pedidos); PEDIDO–PRODUTO é **N:M** (muitos para muitos). Já dá para antever a consequência: N:M pedirá uma tabela extra no modelo lógico (seção 5.3).

> [!tip] Como ler a cardinalidade sem errar
> Leia sempre a frase completa, do ponto de vista de cada entidade: "cada CLIENTE realiza **quantos** PEDIDOS?" e "cada PEDIDO pertence a **quantos** CLIENTES?" A pegadinha da banca é inverter o lado: dizer que "cada pedido tem vários clientes" quando a regra é "cada pedido tem um único cliente". Escreva as duas perguntas no papel antes de marcar a resposta.

### 4.4 Participação: opcional vs. obrigatória

Além da quantidade, o modelo conceitual costuma registrar se a participação é **obrigatória** ou **opcional**. Se todo pedido precisa ter um cliente, a participação do pedido no relacionamento é *total* (obrigatória); se um cliente pode existir sem nunca ter feito pedido, a participação do cliente é *parcial* (opcional). A banca explora isso com palavras como "todo", "nenhum", "pode", "deve" — a mesma semântica de quantificadores que você estudou na lógica. "**Todo** pedido pertence a um cliente" é um "todo" universal de verdade.

---

## 5. Modelagem lógica: o modelo relacional

### 5.1 Relação, tupla, domínio

A **modelagem lógica** traduz o modelo conceitual para o modelo escolhido — no nosso caso, o **modelo relacional**. Aqui nascem as **tabelas**. A terminologia formal, herdada da matemática, é cobrada com frequência:

| Termo formal | Termo popular | Significado |
|---|---|---|
| Relação | Tabela | O conjunto de dados estruturado em linhas e colunas |
| Tupla | Linha, registro | Uma ocorrência da relação |
| Atributo | Coluna, campo | Uma propriedade da relação |
| Domínio | Tipo, conjunto de valores válidos | O "universo" de valores que um atributo pode assumir |
| Grau | — | A quantidade de atributos (colunas) da relação |

> [!warning] PEGADINHA — dois sentidos de "cardinalidade"
> No modelo conceitual, "cardinalidade" é a quantidade de associações de um relacionamento (**1:1, 1:N, N:M**). No modelo relacional, o mesmo termo pode aparecer com outro sentido: a **cardinalidade de uma relação** é o **número de tuplas (linhas)** — chamada também de *cardinalidade do conjunto*. A banca testa exatamente essa ambiguidade: leia o contexto antes de responder.

### 5.2 Chaves: o coração do modelo relacional

O modelo relacional conecta tabelas por **valores**, não por ponteiros. Essa conexão é feita por **chaves** — e conhecer os tipos de chave é obrigatório:

- **Superchave:** qualquer conjunto de atributos que identifica **unicamente** uma tupla. Pode conter atributos "a mais" (ex.: `cod_cliente` + `nome` também identifica, mas `nome` é desnecessário).
- **Chave candidata:** uma superchave **mínima** — nenhum subconjunto próprio dela ainda identifica a tupla. Uma relação pode ter várias.
- **Chave primária (PK):** a chave candidata **escolhida** para identificar oficialmente as tuplas.
- **Chave alternativa:** as chaves candidatas que **não** foram escolhidas como primária.
- **Chave composta:** chave formada por **mais de um atributo** (ex.: `(num_pedido, cod_produto)` na tabela de itens).
- **Chave estrangeira (FK):** atributo (ou conjunto) de uma relação que **referencia a chave primária de outra relação** — ou da mesma. É a FK que materializa, em valores, o relacionamento do modelo conceitual.

Duas regras de integridade sustentam o modelo relacional — decore-as como os dois pilares:

- **Integridade de entidade:** a chave primária **não pode ser nula** (NULL). Se uma tupla não tem chave, ela não pode ser identificada — e não faz sentido no modelo.
- **Integridade referencial:** todo valor de **chave estrangeira** deve existir como chave primária na relação referenciada (ou ser nulo, se a participação for opcional). Não se pode ter um pedido apontando para um cliente que não existe.

> [!note] Palavras-chave da modelagem lógica
> **Chave primária**, **chave estrangeira**, **chave candidata**, **chave alternativa**, **chave composta**, **superchave**, **integridade de entidade**, **integridade referencial**. A FGV cobra principalmente: (1) a definição de cada uma; (2) a diferença entre chave candidata e primária (escolha!); (3) qual chave resolve o relacionamento 1:N (a do lado 1 vira FK no lado N).

### 5.3 Mapeando o modelo conceitual para o relacional

As regras de transformação são o "ponto a ponto" entre as seções 4 e 5:

- **entidade → tabela;** atributo → coluna; atributo multivalorado → tabela à parte (tema da normalização, [[Normalizacao]]);
- **relacionamento 1:N:** a chave primária do lado **1** entra como **chave estrangeira** na tabela do lado **N**. CLIENTE (1) — (N) PEDIDO vira: `PEDIDO` ganha a coluna `cod_cliente`, que referencia `CLIENTE.cod_cliente`;
- **relacionamento N:M:** cria-se uma **tabela associativa** (de ligação), cuja chave primária é composta pelas chaves das duas entidades. PEDIDO (N) — (M) PRODUTO vira `PEDIDO_PRODUTO(num_pedido, cod_produto, quantidade)`, com as duas colunas servindo de chave composta e de chaves estrangeiras ao mesmo tempo; o atributo do relacionamento (quantidade) entra nela;
- **relacionamento 1:1:** a chave de um dos lados entra como FK no outro (escolha que segue a participação obrigatória/opcional).

> [!example] O modelo lógico da loja — com dados
> Aplicando as regras ao exemplo da seção 4.3:
>
> **CLIENTE** (PK: `cod_cliente`)
>
> | cod_cliente | nome | email | cidade |
> |---|---|---|---|
> | 1 | Ana Souza | ana@email.com | Recife |
> | 2 | Bruno Lima | bruno@email.com | Olinda |
>
> **PEDIDO** (PK: `num_pedido`; FK: `cod_cliente` → CLIENTE)
>
> | num_pedido | data_venda | cod_cliente |
> |---|---|---|
> | 1001 | 2026-08-10 | 1 |
> | 1002 | 2026-08-11 | 2 |
> | 1003 | 2026-08-12 | 1 |
>
> **PRODUTO** (PK: `cod_produto`)
>
> | cod_produto | descricao | preco_unitario |
> |---|---|---|
> | 7 | Teclado mecânico | 320,00 |
> | 9 | Mouse sem fio | 95,00 |
>
> **PEDIDO_PRODUTO** (PK composta: `num_pedido` + `cod_produto`; FKs para PEDIDO e PRODUTO)
>
> | num_pedido | cod_produto | quantidade |
> |---|---|---|
> | 1001 | 7 | 1 |
> | 1002 | 9 | 2 |
> | 1002 | 7 | 1 |
>
> Repare na beleza do modelo: o relacionamento N:M virou a tabela associativa; `quantidade`, que era atributo do relacionamento, virou coluna dela; e a integridade referencial garante que nenhum pedido aponte para um cliente ou produto inexistente. Essa estrutura será a matéria-prima da próxima nota: será que ela está bem projetada? (Eis o assunto da [[Normalizacao]].)

---

## 6. Modelagem física

### 6.1 Do lógico ao físico

O **modelo físico** descreve **como** os dados serão realmente armazenados no SGBD escolhido: em que arquivos, com que organização, com que índices, em que espaços. Aqui — e somente aqui — entram as decisões dependentes do produto: Oracle, PostgreSQL ou SQL Server guardam a mesma tabela lógica de formas diferentes. A independência de dados é exatamente o que permite mudar o nível físico sem reescrever os programas.

| | Conceitual | Lógico | Físico |
|---|---|---|---|
| Cidade do cliente | atributo da entidade CLIENTE | coluna `cidade` em CLIENTE (ou FK para CIDADE) | `cidade VARCHAR2(50)` com índice, em determinado tablespace |

> [!warning] PEGADINHA — misturar os níveis
> "O modelo físico é igual para qualquer SGBD" — **falso**; o físico é o nível mais dependente do produto. "O modelo conceitual define índices" — **falso**; índices são decisão física. A FGV oferece alternativas que misturam os níveis justamente para testar se você sabe onde cada decisão mora. Pergunte sempre: *o que decide isso — o negócio (conceitual), a estrutura (lógico) ou o disco (físico)?*

### 6.2 Indexação

Um **índice** é uma estrutura auxiliar de dados (tipicamente uma árvore, como a **B-tree**) que acelera a localização de linhas por valor de uma ou mais colunas — o equivalente ao índice remissivo de um livro: em vez de folhear página por página, você vai direto ao trecho. Sem índice, o SGBD precisa examinar todas as linhas da tabela (varredura completa); com índice, ele encontra os endereços rapidamente.

O que a banca cobra sobre índices:

- **trade-off:** o índice acelera **leituras**, mas custa **espaço em disco** e torna **inserções/atualizações mais lentas** (o índice precisa ser mantido a cada mudança). Por isso, não se cria índice para toda coluna;
- **índice único:** garante que não haja valores repetidos na coluna indexada — a chave primária, por definição, recebe um índice único automaticamente;
- **clusterizado (clustered) vs. não clusterizado:** no índice **clusterizado**, a ordem física das linhas no disco segue a ordem do índice (só um por tabela); no **não clusterizado**, o índice é uma estrutura separada que aponta para as linhas. É um conceito que a FGV costuma cobrar em distinção direta.

### 6.3 Particionamento

**Particionamento** é a divisão de uma tabela grande em **partes menores** (partições), mantendo a visão lógica de uma única tabela. As duas formas clássicas:

- **particionamento horizontal:** divide por **linhas** — ex.: tabela de benefícios particionada por ano (dados de 2024 em uma partição, 2025 em outra, 2026 em outra). Melhora consultas que filtram por faixa e facilita arquivar ou descartar dados antigos;
- **particionamento vertical:** divide por **colunas** — ex.: separar colunas de grande volume (textos longos) das colunas mais consultadas, se o SGBD distribuir o armazenamento.

O particionamento é uma decisão **física** pura: o modelo lógico continua enxergando uma única tabela; quem sente a divisão é o disco (e o desempenho).

### 6.4 Tablespaces

Um **tablespace** é uma **área lógica de armazenamento** que agrupa objetos do banco (tabelas, índices) e os associa a **arquivos físicos** em disco. É a "gaveta organizadora" do SGBD: você pode colocar os dados em um tablespace e os índices em outro, em discos diferentes, para distribuir I/O; ou manter tabelas críticas em um tablespace com backup mais frequente. Quando o DBA "cria um tablespace e um usuário que o utiliza", ele está tomando decisões de modelagem física.

> [!tip] Os três níveis na prática — um mesmo dado, três decisões
> Para a cidade do cliente: no **conceitual**, decidimos que CLIENTE tem um atributo *cidade* (e que ela indica a UF, como veremos na normalização); no **lógico**, decidimos que *cidade* é uma coluna e se ela é FK para uma tabela CIDADE; no **físico**, decidimos o tipo exato (`VARCHAR2(50)`), se há índice, se a tabela é particionada e em qual tablespace mora. Cada decisão em seu nível — e é assim que a banca separa os candidatos.

---

## 7. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **Dado** é fato bruto; **informação** é dado interpretado
> - [ ] **Banco de dados** = coleção integrada, organizada e persistente de dados relacionados (o *dado*)
> - [ ] **SGBD** = software que gerencia o banco (o *programa*); MySQL é SGBD, não banco
> - [ ] Funções do SGBD: catálogo/metadados, concorrência, segurança, integridade, backup
> - [ ] Abordagens: **hierárquica** (árvore), **rede** (grafo), **relacional** (tabelas e chaves), **OO** (objetos)
> - [ ] Conceitual: o **quê**; entidade (conjunto), atributo, relacionamento (verbo), cardinalidade (1:1, 1:N, N:M)
> - [ ] Atributos: simples/composto, monovalorado/multivalorado, derivado; entidade forte/fraca
> - [ ] Lógico: relação/tupla/atributo/domínio; chaves (primária, estrangeira, candidata, alternativa, composta)
> - [ ] Integridade de **entidade** (PK não nula) e integridade **referencial** (FK válida)
> - [ ] Mapeamento: 1:N → FK no lado N; N:M → tabela associativa; atributo do relacionamento entra na associativa
> - [ ] Físico: o **como guardar**; índices (B-tree, único, clusterizado), particionamento (horizontal/vertical), tablespaces

> [!warning] O erro mais comum em prova
> Confundir **banco de dados com SGBD** e confundir os **três níveis de modelagem**. Antes de marcar qualquer questão, faça duas perguntas: *"isto é dado ou software?"* e *"isto é decisão de negócio (conceitual), de estrutura (lógico) ou de armazenamento (físico)?"* — essas duas perguntas eliminam a maioria das alternativas erradas.

---

## 8. Próximos passos

Você acabou de construir o alicerce do Bloco 3.1: sabe o que é um banco de dados, conhece as abordagens históricas e domina os três níveis de modelagem. Agora é hora de colocar as tabelas que criamos na seção 5.3 sob suspeita — o próximo tópico, [[Normalizacao]], vai ensinar como **avaliar e melhorar o projeto lógico** para eliminar repetição e inconsistência, usando dependências funcionais e as formas normais (1FN, 2FN, 3FN e BCNF).

Depois da normalização, o bloco segue na ordem da ementa: **SQL** (criar e consultar tabelas já bem desenhadas), **Transações e ACID** (a garantia de que operações concorrentes não corrompem dados), **NoSQL** (quando o modelo relacional não é a melhor resposta) e **Big Data** (volume, velocidade e variedade em escala). Mais adiante na FASE 3, o conteúdo destas notas será reaproveitado no estudo de **BI e Data Warehouse** — quando você entenderá como os bancos operacionais alimentam os ambientes analíticos. Por enquanto, a ordem é uma coisa de cada vez: a missão imediata é deixar o modelo lógico impecável — e esse é exatamente o trabalho da [[Normalizacao]].