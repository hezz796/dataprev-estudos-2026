# NoSQL

> [!info] Metadados
> **Disciplina:** Banco de Dados
> **Bloco:** 3.1 — Banco de Dados (FASE 3 — Infraestrutura de Dados)
> **Tópico:** 5. NoSQL
> **Subtópicos:** Quando usar NoSQL vs. SQL · Tipos: document, key-value, column-family, graph · Exemplos: MongoDB, Redis, Cassandra, Neo4j · Eventual consistency vs. strong consistency
> **Pré-requisitos:** [[Transacoes-e-ACID]] (ACID, isolamento e a letra C — para contrapor com *eventual consistency*), [[SQL-DDL-e-DML]] (linguagem declarativa e JOINs), [[Fundamentos-e-Modelagem]] e [[Normalizacao]] (modelo relacional, esquema rígido, chaves e integridade), [[Raciocinio-Matematico-Aplicado|Raciocínio Lógico Matemático]] (conjuntos, funções, grafos, relações n-árias) e [[LGPD-Lei-Geral-de-Protecao-de-Dados|Legislação/Segurança]] (dados pessoais em larga escala, minimização, segurança)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-28

---

## 1. Por que estudar NoSQL?

Nas quatro notas anteriores você percorreu o lado "clássico" do banco de dados: modelamos entidades e relacionamentos ([[Fundamentos-e-Modelagem]]), normalizamos as tabelas ([[Normalizacao]]), consultamos com SQL ([[SQL-DDL-e-DML]]) e vimos como o ACID torna as transações confiáveis ([[Transacoes-e-ACID]]). Tudo isso responde muito bem a uma pergunta: *como guardar dados estruturados com integridade?* Mas o mundo real fez outra pergunta — e é dela que nasce esta nota.

No início dos anos 2000, empresas como Google e Amazon precisavam lidar com **bilhões de operações por dia**, dados cujo formato mudava a cada versão do produto e a exigência de funcionar 24/7. Um banco relacional único (ou poucos servidores muito potentes) não acompanhava esse ritmo — e, principalmente, o **esquema rígido** (todas as linhas da tabela com as mesmas colunas, definido antes de gravar qualquer coisa) atrapalhava quando o dado mudava de forma. Foi para cenários assim que surgiram os bancos **NoSQL**.

Sistemas como os da DATAPREV também convivem com os dois mundos: bases relacionais para cadastros e transações que exigem consistência forte, e soluções NoSQL para **cache, sessões, catálogos de serviços, filas e análises em larga escala**. Entender *quando* usar cada um é a habilidade que a FGV quer testar.

> [!question] Pergunta orientadora
> Se o modelo relacional é tão bom, por que alguém criaria bancos que **abrem mão** de partes do ACID — como a consistência forte? A pista está no próprio nome: *Not Only SQL* — "não somente SQL". NoSQL não é a ausência do relacional; é a resposta para problemas que o relacional não resolve bem.

---

## 2. Relacional × NoSQL — quando usar cada um

### 2.1 O nome e as duas leituras erradas

**NoSQL** significa **"Not Only SQL"** (não somente SQL). O termo foi popularizado em 2009 para designar uma família de bancos que **não seguem o modelo relacional**. Duas leituras erradas são clássicas de prova: "NoSQL = banco que não usa SQL" e "NoSQL = substituto do SQL". A primeira é falsa porque alguns bancos NoSQL oferecem linguagens parecidas com SQL; a segunda é falsa porque NoSQL e SQL são **complementares**, não concorrentes — um sistema grande usa os dois.

### 2.2 Comparando os dois mundos

| Critério | Relacional | NoSQL |
|---|---|---|
| Modelo de dados | Tabelas (relações) com linhas e colunas | Documentos, pares chave-valor, colunas, grafos |
| Esquema | **Fixo**, definido antes de gravar | **Flexível**: cada registro pode ter campos diferentes |
| Consultas | SQL declarativo, com **JOINs** | APIs próprias: por chave, por documento, por travessia de grafo |
| Consistência | ACID, consistência forte | Geralmente **consistência eventual** (ou forte, conforme configuração) |
| Escala | **Vertical** (servidor mais potente) | **Horizontal** (mais servidores, dados distribuídos) |
| Integridade | Chaves, FKs, constraints (o banco impõe) | Poucas garantias; regras ficam no código da aplicação |
| Uso típico | Transacional, financeiro, relatórios | Cache, sessão, catálogo, redes sociais, IoT, Big Data |

### 2.3 O roteiro de decisão

Quando ficar com o **relacional**?

- Os dados têm **estrutura estável** e **relacionamentos ricos** (muitos N:M, consultas que cruzam várias tabelas);
- A operação exige **transação com consistência forte** — dinheiro, benefícios, débitos e créditos;
- Você precisa de **consultas ad-hoc** e relatórios (o SQL é imbatível nisso);
- Você valoriza maturidade da ferramenta e garantias de integridade impostas pelo banco.

Quando partir para o **NoSQL**?

- O **volume exige distribuição horizontal** com tolerância a partição;
- O **formato dos dados muda com frequência** (esquema flexível);
- A carga é de **escrita em altíssima vazão** (logs, eventos, sensores);
- A operação é **simples e por chave**, e precisa de latência mínima (cache, sessão);
- O dado é naturalmente um **documento** (JSON) ou um **grafo**;
- Você aceita **consistência eventual** em troca de disponibilidade e velocidade.

> [!warning] PEGADINHA — "substitui" ou "complementa"?
> A FGV adora as frases "o NoSQL substitui o banco relacional" e "o NoSQL dispensa a linguagem SQL" — ambas **falsas**. A prática moderna é a **persistência poliglota**: o mesmo sistema usa relacional (transações), document (catálogo), key-value (cache) e graph (relacionamentos) ao mesmo tempo, cada um no seu papel.

---

## 3. Os quatro tipos de NoSQL

O que a banca costuma chamar de "NoSQL" na verdade é um **guarda-chuva** com quatro modelos de dados bem diferentes. A escolha entre eles depende da resposta a uma pergunta simples.

> [!question] Pergunta orientadora
> Como você guardaria (1) um currículo que muda de formato a cada candidato, (2) uma sessão de login que precisa ser lida em milissegundos, (3) bilhões de eventos de sensores gravados sem parar e (4) o mapa de amizades de uma rede social? Cada item aponta para um dos quatro tipos de NoSQL.

### 3.1 Document — MongoDB

Ao contrário do relacional, que espalha um "pedido" por várias tabelas (cliente, pedido, item, produto) e o reconstitui com JOINs, o banco **de documentos** guarda o registro como uma unidade autônoma: um **documento**, geralmente em JSON. O documento é autossuficiente — traz consigo os campos que lhe pertencem — e, por isso, exige pouco ou nenhum JOIN. Em troca, aceita **redundância controlada** (denormalização): o nome do cliente pode repetir-se dentro do documento do pedido, para não precisar de busca em outra coleção.

Veja como ficaria um documento de "benefício" no **MongoDB**:

```json
{
  "cod_beneficio": "B-000123",
  "tipo": "aposentadoria",
  "situacao": "ativo",
  "segurado": { "nome": "Maria da Silva", "cidade": "Recife" },
  "dependentes": ["João", "Ana"]
}
```

Repare na flexibilidade: o próximo documento da mesma coleção pode simplesmente **não ter** o campo `dependentes` — não há schema fixo obrigatório. É o modelo ideal para catálogos, conteúdos e dados cuja estrutura varia. Consultas são por **campos do documento**, com índices.

### 3.2 Key-value — Redis

O modelo mais simples de todos: um **mapa** de pares **chave → valor**. Você já estudou funções no [[Raciocinio-Matematico-Aplicado|RLM]]: cada chave "aponta" para um valor, e o acesso é direto — busca por chave é instantânea. O valor é **opaco** para o banco: pode ser texto, número, lista, hash — o banco guarda e devolve, sem interpretar.

O **Redis** é o exemplo clássico e quase sempre cai junto com a palavra **em memória**: seus dados vivem majoritariamente na RAM dos servidores, por isso a latência é mínima. Usos típicos:

- **cache** de consultas (guardar o resultado de uma consulta SQL que é cara e repetida);
- **sessão de usuário** (`sessao:abc123 → {"usuario": "maria.silva", "perfil": "analista"}`);
- **contadores** (`curtidas:post_42 → 137`);
- filas e rate limiting.

> [!warning] PEGADINHA — acesso por chave, não por valor
> No key-value, a busca natural é **pela chave**. "Encontre todos os valores que contêm a palavra X" exige varrer tudo — não é o forte do modelo. Isso o diferencia do documento, que consulta por campos. Frase de prova: "o banco key-value permite consultar rapidamente os dados pelo seu conteúdo" — **falso**; a consulta é por chave.

### 3.3 Column-family — Cassandra

O modelo **column-family** (família de colunas) organiza os dados em colunas agrupadas em "famílias" — parece tabela, mas com liberdade: linhas da mesma família podem ter **colunas diferentes**, e os dados são ordenados pela **chave da linha**. O ponto forte está na **distribuição**: foi projetado para espalhar os dados por muitos servidores e **escrever com vazão altíssima**, sem parar.

O **Cassandra** é o exemplo que a banca cita: usado para **logs de eventos, séries temporais (time-series), mensagens e telemetria de IoT** — cargas de escrita massiva e contínua. Escala-se adicionando servidores (horizontal), e cada linha fica em um nó conforme a chave da linha (o conceito de *partition key* — suficiente saber que a distribuição é por chave).

> [!warning] PEGADINHA — column-family ≠ banco colunar
> "Column-family" **não é** a mesma coisa que "banco colunar" (column-oriented), aquele usado em BI para agregações analíticas rápidas. O Cassandra é distribuído e focado em **escrita horizontal**; o banco colunar é focado em **leitura analítica** — esse tema pertencente ao futuro bloco de BI/Data Warehouse. Se a prova disser que o Cassandra é "um banco orientado a colunas para análise OLAP", desconfie: a definição mais precisa do column-family é **família de colunas com distribuição por chave de linha**.

### 3.4 Graph — Neo4j

O modelo de **grafos** trata o **relacionamento como cidadão de primeira classe**: os dados são **nós** (entidades) e **arestas** (relacionamentos), ambos podendo ter propriedades. É exatamente o [[Raciocinio-Matematico-Aplicado|grafo]] que você viu no RLM — vértices e arestas, caminhos e ciclos — agora como estrutura de armazenamento.

No **Neo4j**, a consulta é uma **travessia**: "quem conhece quem", "qual o caminho mais curto entre duas contas", "existe ciclo de suspeitos?" No combate a fraude previdenciária, por exemplo, os nós podem ser cidadãos, empresas e contas; as arestas, "é sócio de", "é titular de", "fez transação com". O valor do dado está **nas relações** — e o modelo de grafos percorre relações sem JOINs em cascata.

> [!tip] Por que não fazer isso no relacional?
> No banco relacional, um relacionamento N:M exige tabela associativa; percorrer 5 níveis de relação ("amigo do amigo do amigo...") exige 5 JOINs, e o custo explode. No grafo, o relacionamento **já existe como dado** e a travessia segue as arestas diretamente. É a estrutura ideal quando a pergunta é sobre a **conexão**, não sobre o registro isolado.

### 3.5 Panorama dos quatro tipos

| Tipo | Unidade de dado | Estrutura típica | Exemplo | Caso de uso |
|---|---|---|---|---|
| Document | documento (JSON) | autossuficiente, campos flexíveis | **MongoDB** | catálogos, conteúdos, dados variáveis |
| Key-value | par chave-valor | mapa, acesso por chave | **Redis** | cache, sessão, contadores |
| Column-family | linha com colunas variáveis | distribuído por chave de linha | **Cassandra** | eventos, logs, IoT, escrita massiva |
| Graph | nó e aresta | grafo com propriedades | **Neo4j** | redes sociais, fraude, recomendação |

> [!note] Palavras-chave dos tipos (para a prova)
> **Document** = JSON, esquema flexível (MongoDB) · **Key-value** = em memória, acesso por chave (Redis) · **Column-family** = escala de escrita, distribuído (Cassandra) · **Graph** = nós e arestas, travessia (Neo4j). A FGV costuma descrever o cenário ("sistema de recomendação que precisa percorrer relações") e pedir o modelo — o verbo-chave é "relação/travessia" → graph; "cache rápido" → key-value.

---

## 4. Eventual consistency vs. strong consistency

### 4.1 Um novo significado para "consistência"

Em [[Transacoes-e-ACID]], a letra **C** significava "regras de integridade respeitadas" (chaves, FKs, constraints). Em bancos distribuídos e NoSQL, a palavra **consistência** aparece com outro sentido: *as réplicas estão com o mesmo dado?* Quando o banco roda em vários servidores, cada escrita precisa se propagar para as cópias; o que o usuário lê depende de quanto a propagação já avançou. Não confunda os dois C's — esta é a pegadinha mais rentável do tópico:

> [!warning] PEGADINHA — a letra C do ACID ≠ a letra C do NoSQL
> No ACID, C = **integridade das regras** (o banco está num estado válido). No NoSQL, consistência = **igualdade entre réplicas** (todas as cópias com o mesmo valor). A frase "o C do ACID garante que os dados são iguais em todas as réplicas" é falsa — isso é o sentido distribuído, que veremos agora.

### 4.2 Strong consistency — consistência forte

Com **consistência forte**, após uma escrita **confirmada**, qualquer leitura subsequente enxerga o **novo valor** — como se existisse uma única cópia. Em bancos distribuídos, isso exige **coordenação entre os nós** antes de responder: o nó que recebeu a escrita precisa garantir que os demais já viram o valor, ou que responderão com o mais recente. Custa tempo (latência) e pode reduzir a disponibilidade — mas a leitura nunca é "velha".

### 4.3 Eventual consistency — consistência eventual

Com **consistência eventual**, as réplicas podem **divergir por um tempo**; se **nenhuma escrita nova** chegar, todas **convergem** para o mesmo valor — *eventualmente*. Uma leitura imediatamente após uma escrita pode retornar um dado **defasado** (o valor antigo). É a escolha típica de sistemas que priorizam **disponibilidade e velocidade**: cada réplica responde sozinha, sem esperar as outras — correndo o risco de responder "atrasado".

Compare os dois com casos do dia a dia:

| Cenário | Consistência necessária | Por quê? |
|---|---|---|
| Rede social: contador de "curtidas" de um post | **Eventual** | Ver 1.384 em vez de 1.385 por alguns segundos não afeta ninguém |
| Transação bancária: saque e saldo | **Forte** | Não se pode ler "saldo de R$ 200" depois de sacar R$ 100 e o sistema confirmar |
| DATAPREV: consulta de um benefício pelo cidadão | **Forte** | Informação errada/defasada sobre o próprio benefício gera dano direto |
| DATAPREV: notificação interna de atualização de cadastro | **Eventual** | O atraso de propagação é tolerável |

> [!warning] PEGADINHA — eventual ≠ inconsistente para sempre, e ≠ transacional
> Duas frases falsas clássicas: (1) "na consistência eventual, os dados ficam inconsistentes permanentemente" — **falso**: na ausência de novas escritas, as réplicas **convergem**; a divergência é temporária. (2) "consistência eventual equivale a uma transação" — **falso**: eventual consistency **relaxa** o ACID (não há isolamento nem atomicidade distribuída); é um mecanismo de replicação, não uma transação. E atenção: "consistência forte" também **não é** sinônimo de "ACID" — trata de réplicas; o ACID é um conjunto mais amplo, que vimos na nota anterior.

---

## 5. O Teorema CAP — consistência, disponibilidade e partições

### 5.1 As três letras

O **Teorema CAP** (também chamado de teorema de Brewer, por Eric Brewer, 2000) responde à pergunta que todo sistema distribuído enfrenta: *o que fazemos quando a rede se parte?* As três letras são:

- **C — Consistency (Consistência):** toda leitura vê a escrita mais recente; todas as réplicas têm o mesmo dado no mesmo instante;
- **A — Availability (Disponibilidade):** toda requisição recebe uma resposta (de sucesso ou de falha), sem que o sistema fique esperando indefinidamente;
- **P — Partition tolerance (Tolerância a partição):** o sistema continua operando mesmo quando a rede se **divide** em partes que não se comunicam (partição) ou mensagens se perdem.

### 5.2 O raciocínio do teorema

Imagine dois servidores com o dado $D$. A rede se parte: o servidor 1 fica isolado do servidor 2. Uma escrita chega ao servidor 1 e altera $D$; logo depois, uma leitura chega ao servidor 2.

O que o servidor 2 responde?

- Se responder com o **valor antigo**, mantém a disponibilidade (A) — mas viola a consistência (C);
- Se **recusar a responder** (ou responder "não sei"), preserva a consistência (C) — mas viola a disponibilidade (A);
- A única forma de ter C e A juntos seria o sistema **parar de operar com a partição** — ou seja, abrir mão do P.

Por isso o teorema afirma: **em um sistema distribuído, é impossível garantir simultaneamente os três — escolha dois**.

### 5.3 As combinações

| Combinação | O que faz | Exemplo típico |
|---|---|---|
| **CA** | consistência + disponibilidade, **sem** tolerância a partição | banco relacional tradicional em **nó único** |
| **CP** | consistência forte; durante a partição, **sacrifica a disponibilidade** | MongoDB (com escrita majoritária), HBase |
| **AP** | disponibilidade; aceita **consistência eventual** | Cassandra, DynamoDB |

> [!tip] A leitura moderna do teorema
> Em redes reais, **partições acontecem** — logo, P não é uma escolha, é uma **condição do ambiente**. A decisão prática é entre **C ou A durante a partição**. Por isso: a dupla "CA" só existe em sistemas que não se particionam (na prática, nó único); sistemas distribuídos de verdade são **CP** ou **AP**. E a ponte com a seção 4: sistemas **AP** costumam usar **consistência eventual**; sistemas **CP**, **consistência forte**.

> [!warning] PEGADINHA — só 2 de 3
> "Em um sistema distribuído, o CAP permite garantir consistência, disponibilidade e tolerância a partição simultaneamente" — **falso**: no máximo **dois** dos três. "Um sistema CA distribui os dados e continua consistente e disponível durante a partição" — **falso**: CA não tolera partição; com a rede partida, ele para. E não confunda siglas: **CAP** (teorema de sistemas distribuídos) ≠ **ACID** (propriedades de transação) — o C de cada um tem significados diferentes, como vimos na seção 4.1.

---

## 6. NoSQL, RLM e LGPD — pontes com a Fase 1

### 6.1 O RLM dentro dos modelos NoSQL

A matemática que você treinou na Fase 1 reaparece aqui com roupagem de banco de dados:

- o **conjunto** é a base do modelo relacional (uma relação é um subconjunto de um produto cartesiano — você viu isso em [[Fundamentos-e-Modelagem]]);
- o **key-value** é uma **função**: cada chave do domínio aponta para exatamente um valor do contradomínio;
- o **graph** é o **grafo do RLM**: vértices, arestas, caminhos e ciclos — a mesma estrutura que causava deadlock em [[Transacoes-e-ACID]] agora é o modelo de dados de redes sociais e detecção de fraude;
- a **relação n-ária** do modelo relacional, que exige normalização ([[Normalizacao]]), é o que o NoSQL desnormaliza: em vez de quebrar em várias tabelas, ele guarda o registro inteiro como documento ou linha espalhada.

### 6.2 LGPD: escala grande, responsabilidade grande

Quanto mais dados pessoais armazenados e replicados, mais exposição. Eis as pontes com a [[LGPD-Lei-Geral-de-Protecao-de-Dados|LGPD]]:

- **Minimização** (princípio da necessidade): o NoSQL incentiva guardar tudo — mas a LGPD manda coletar e reter **somente o necessário** para a finalidade. Documentos com redundância controlada não podem virar acúmulo de dados pessoais desnecessários;
- **Réplicas multiplicam cópias**: cada nó que guarda uma cópia é um ponto de exposição. Criptografia, controle de acesso e trilhas de auditoria (art. 46) precisam valer em **todos** os nós, não só no servidor principal;
- **Consistência eventual em dado sensível é perigosa**: informações de saúde, por exemplo, não podem ser lidas "defasadas" — a escolha entre eventual e forte tem implicação de **qualidade dos dados** (art. 6);
- **Tratamento em larga escala**: operações com muitos dados pessoais podem exigir **Relatório de Impacto à Proteção de Dados (RIPD)** e avaliação de risco — exatamente o cenário de quem adota NoSQL em grande escala.

> [!important] O raciocínio para a prova
> Questão que mistura NoSQL e LGPD quase sempre trava em "dados pessoais em larga escala". A resposta técnica aponta para: **minimização** (guardar só o necessário), **segurança em cada nó** (criptografia, controle de acesso) e **consistência adequada ao risco** (não usar consistência eventual para dado sensível crítico).

---

## 7. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **NoSQL = Not Only SQL** — complementa, não substitui o relacional
> - [ ] **Quando usar:** relacional = estrutura estável, relacionamentos, ACID, SQL; NoSQL = escala horizontal, esquema flexível, escrita massiva, cache
> - [ ] **4 tipos:** document (MongoDB, JSON) · key-value (Redis, em memória) · column-family (Cassandra, escrita distribuída) · graph (Neo4j, nós e arestas)
> - [ ] **Consistência forte** = leitura sempre vê a escrita mais recente (réplicas coordenadas)
> - [ ] **Consistência eventual** = réplicas divergem e **convergem**; leitura pode ser defasada
> - [ ] **C do ACID (regras)** ≠ **C do NoSQL (réplicas)** — não confundir
> - [ ] **CAP:** sistema distribuído garante no máximo **2 de 3** (C, A, P); na prática, escolha C ou A durante a partição (CP ou AP)
> - [ ] Aplicação prática: rede social → eventual; transação bancária/benefício → forte
> - [ ] **LGPD:** minimização, segurança em todos os nós, consistência adequada ao risco

> [!warning] O erro mais comum em prova
> Confundir os quatro tipos entre si e confundir os dois C's. Roteiro rápido: (1) "documento JSON" → document; (2) "acesso por chave, em memória" → key-value; (3) "escrita em larga escala distribuída" → column-family; (4) "percorre relações" → graph; (5) "réplicas convergem depois" → eventual consistency; (6) "todo sistema distribuído garante C, A e P" → falso, só 2 de 3.

---

## 8. Próximos passos

Você fechou o penúltimo tópico do Bloco 3.1. A comparação que faltava — relacional com suas garantias ACID versus NoSQL com flexibilidade e escala — está feita, e agora você sabe que a escolha de banco é uma **decisão de arquitetura**, não de moda.

O próximo e **último tópico do bloco** é **Big Data** ([[Big-Data]]): lá você verá o ambiente onde o NoSQL mais brilha — volumes gigantescos, velocidade, variedade — e o ecossistema de processamento distribuído (Hadoop, Spark) e os Data Lakes. A ponte é imediata: o Cassandra que você estudou aqui é um dos armazenamentos preferidos de ecossistemas Big Data, e a discussão de consistência retorna com mais força.

O que fica anunciado para **depois**, sem ensinar agora: o bloco de **BI/Data Warehouse** (modelagem dimensional, ETL e OLAP) aprofundará o lado analítico dos dados; e, na **Arquitetura Avançada**, o **Teorema CAP** e as transações distribuídas voltam — agora com protocolos como Two-Phase Commit e Saga em sistemas de microsserviços. Por ora, respire: o alvo imediato é a nota de Big Data, que encerra o seu Bloco 3.1.