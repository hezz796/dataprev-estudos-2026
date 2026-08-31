# SQL — DDL e DML

> [!info] Metadados
> **Disciplina:** Banco de Dados
> **Bloco:** 3.1 — Banco de Dados (FASE 3 — Infraestrutura de Dados)
> **Tópico:** 3. SQL — DDL e DML
> **Subtópicos:** DDL (CREATE, ALTER, DROP, TRUNCATE) · DML (SELECT, INSERT, UPDATE, DELETE) · JOINs (INNER, LEFT, RIGHT, FULL, CROSS) · Subconsultas, agrupamento (GROUP BY, HAVING), ordenação · Funções de agregação (COUNT, SUM, AVG, MIN, MAX) · Views, triggers, stored procedures (conceito)
> **Pré-requisitos:** [[Fundamentos-e-Modelagem]] (modelo relacional, chaves primárias e estrangeiras, integridade referencial), [[Normalizacao]] (esquema sem anomalias), [[Raciocinio-Matematico-Aplicado|Raciocínio Lógico Matemático]] (lógica proposicional, conjuntos e operações entre conjuntos) e [[LGPD-Lei-Geral-de-Protecao-de-Dados|Legislação/Segurança]] (dados pessoais e sensíveis, auditoria)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-28

---

## 1. Por que estudar SQL?

Nas duas notas anteriores do Bloco 3.1, você trabalhou no **papel**: na [[Fundamentos-e-Modelagem]], transformou o mundo real em tabelas, chaves e relacionamentos; na [[Normalizacao]], submeteu essas tabelas ao crivo das formas normais. O resultado é um esquema limpo — mas que ainda não roda em lugar nenhum. Falta a ponte entre o desenho e o sistema vivo: **SQL** — a *Structured Query Language*, a linguagem padrão para definir e manipular dados em bancos relacionais.

A ementa do DATAPREV é explícita: *"SQL é o tópico mais prático — montar queries complexas é essencial."* A FGV não cobra SQL por decoreba; ela apresenta um esquema (ou um trecho de código) e pergunta qual consulta produz determinado resultado, qual comando fez tal alteração, ou qual afirmativa sobre um JOIN está correta. Por isso, esta nota é diferente das anteriores: **cada conceito vem com um comando executável, e você deve reproduzir os exemplos sozinho** — de preferência em um SGBD real de estudos (PostgreSQL, MySQL), mas pelo menos no papel, prevendo o resultado antes de ver a explicação.

Há também duas pontes com a Fase 1 que vamos usar o tempo todo:

- o [[Raciocinio-Matematico-Aplicado|RLM]]: uma condição `WHERE` é uma **proposição lógica** aplicada linha a linha — `AND`, `OR`, `NOT` funcionam exatamente como na tabela verdade; e o `JOIN` e o `UNION` são **operações entre conjuntos** (produto cartesiano, união, interseção) com os dados no papel de conjuntos;
- a [[LGPD-Lei-Geral-de-Protecao-de-Dados|LGPD]]: profissionais que manipulam dados pessoais e sensíveis precisam saber **o que cada comando faz com os dados** — um `DELETE` mal escrito apaga registros de cidadãos; um `TRUNCATE` não deixa rastro linha a linha; um `UPDATE` sem `WHERE` altera a base inteira. Na DATAPREV, que processa dados previdenciários de milhões de brasileiros, esse cuidado é literalmente dever legal.

> [!question] Pergunta orientadora
> Você tem 27 clientes cadastrados e precisa descobrir quantos pedidos cada um fez no último mês. *Sem SQL*, quanto tempo leva? A resposta — e a agilidade com que você escreve essa consulta — é exatamente o que este tópico desenvolve.

---

## 2. SQL e suas sublinguagens

O SQL não é uma linguagem única: ele se divide em **famílias de comandos**, cada uma com um papel. A primeira classificação que a banca cobra é entre **DDL** e **DML** — e muitas questões morrem ou nascem nessa distinção.

| Família | O que faz | Comandos | Palavra-chave |
|---|---|---|---|
| **DDL** (Data Definition Language) | Define a **estrutura** (o "esqueleto" do banco) | `CREATE`, `ALTER`, `DROP`, `TRUNCATE` | estrutura |
| **DML** (Data Manipulation Language) | Manipula os **dados** (o "conteúdo") | `SELECT`, `INSERT`, `UPDATE`, `DELETE` | conteúdo |
| **DQL** (Data Query Language) | Consulta (alguns autores separam da DML) | `SELECT` | consulta |
| **DCL** (Data Control Language) | Controla **permissões** | `GRANT`, `REVOKE` | permissões |
| **TCL** (Transaction Control Language) | Controla **transações** | `BEGIN`, `COMMIT`, `ROLLBACK` | transações |

Duas observações de prova: a classificação oficial mais comum trata o `SELECT` como parte da DML (a DQL é uma subdivisão didática — guarde as duas leituras), e o `TRUNCATE` costuma ser classificado como **DDL**, porque ele lida com a estrutura da tabela (esvaziar a tabela é "redefinir" seu estado), não com linhas individuais. A seção 3.4 explora essa pegadinha.

> [!note] Palavras-chave desta seção
> **DDL** (estrutura), **DML** (dados), comando `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `CREATE`, `ALTER`, `DROP`, `TRUNCATE`. Na prova: "qual destes é um comando DDL?" — a resposta é aquele que **altera a definição da tabela**, não os dados.

---

## 3. DDL — construindo o esqueleto do banco

### 3.1 CREATE — criar objetos

O `CREATE` é o comando que **cria** objetos: bancos (`CREATE DATABASE`), tabelas (`CREATE TABLE`), índices (`CREATE INDEX`), views (seção 9). O `CREATE TABLE` é o mais cobrado — e é onde reaparecem, agora em código, os conceitos de chave e integridade que você estudou na modelagem.

Vamos materializar o esquema normalizado da loja das notas anteriores. Repare como cada decisão de projeto vira uma **restrição**:

```sql
CREATE TABLE cliente (
    cod_cliente INTEGER PRIMARY KEY,          -- chave primária
    nome        VARCHAR(100) NOT NULL,        -- não pode ser nulo
    email       VARCHAR(100) UNIQUE,          -- não admite duplicados
    cidade      VARCHAR(60)
);

CREATE TABLE produto (
    cod_produto    INTEGER PRIMARY KEY,
    descricao      VARCHAR(100) NOT NULL,
    preco_unitario NUMERIC(10,2) NOT NULL
);

CREATE TABLE pedido (
    num_pedido  INTEGER PRIMARY KEY,
    data_venda  DATE NOT NULL,
    cod_cliente INTEGER NOT NULL,
    CONSTRAINT fk_pedido_cliente
        FOREIGN KEY (cod_cliente) REFERENCES cliente (cod_cliente)
);

CREATE TABLE pedido_produto (
    num_pedido  INTEGER NOT NULL,
    cod_produto INTEGER NOT NULL,
    quantidade  INTEGER NOT NULL CHECK (quantidade > 0),
    PRIMARY KEY (num_pedido, cod_produto),   -- chave composta
    FOREIGN KEY (num_pedido)  REFERENCES pedido  (num_pedido),
    FOREIGN KEY (cod_produto) REFERENCES produto (cod_produto)
);
```

Veja o que cada restrição significa:

- **`PRIMARY KEY`**: implementa a **integridade de entidade** — não aceita valores nulos nem repetidos;
- **`FOREIGN KEY ... REFERENCES`**: implementa a **integridade referencial** — a FGV adora perguntar "o que impede um pedido de apontar para um cliente inexistente?"; a resposta é a `FOREIGN KEY`;
- **`NOT NULL`**: exige presença de valor;
- **`UNIQUE`**: impede duplicados (a chave primária já é única; `UNIQUE` serve para os demais atributos, como o e-mail);
- **`CHECK`**: valida uma condição por linha — aqui, `quantidade > 0`.

> [!tip] Sintaxe varia entre SGBDs — fique no padrão
> Esta nota usa **SQL padrão, alinhado ao PostgreSQL**. Em prova, a FGV quase sempre cobra a *lógica* do comando, não o dialeto. Quando a sintaxe variar muito (ex.: `ALTER TABLE ... ALTER COLUMN` no PostgreSQL vs. `MODIFY` no Oracle/MySQL), aviso em um callout como este.
>
> Para chaves autoincrementadas: `SERIAL` (PostgreSQL), `AUTO_INCREMENT` (MySQL), `IDENTITY` (SQL Server) — mesmo conceito, nomes diferentes. No padrão puro, você insere a chave manualmente.

### 3.2 ALTER — mudar o esqueleto

O `ALTER` **modifica a estrutura** de um objeto já existente: adicionar/remover colunas, alterar tipos, incluir restrições.

```sql
-- Adicionar uma coluna
ALTER TABLE cliente ADD COLUMN telefone VARCHAR(20);

-- Alterar o tipo de uma coluna (PostgreSQL)
ALTER TABLE cliente ALTER COLUMN telefone TYPE VARCHAR(25);

-- Em Oracle/MySQL, a mesma ideia aparece com MODIFY
ALTER TABLE cliente MODIFY telefone VARCHAR(25);

-- Adicionar uma restrição
ALTER TABLE pedido
    ADD CONSTRAINT fk_pedido_cliente2
    FOREIGN KEY (cod_cliente) REFERENCES cliente (cod_cliente);
```

Preste atenção à pegadinha recorrente: `ALTER` **não mexe nos dados** — ele mexe na *definição*. "Alterar o nome de um cliente para 'Ana' em todos os pedidos" é `UPDATE` (DML); "adicionar uma coluna 'desconto'" é `ALTER` (DDL).

### 3.3 DROP — derrubar o esqueleto

O `DROP` **remove o objeto inteiro** — estrutura **e** dados. É irreversível na prática (sem backup, sem recuperação):

```sql
DROP TABLE pedido_produto;   -- remove a tabela e os dados
DROP TABLE cliente;          -- em ordem: as "filhas" antes das "mães"
```

Por causa da integridade referencial, muitos SGBDs **recusam** dropar uma tabela que é referenciada por outra. Duas saídas: dropar as tabelas na ordem inversa das dependências, ou usar `DROP TABLE ... CASCADE` (que remove também as restrições dependentes). A pegadinha da banca: `DROP` não é "apagar as linhas" — é **extinguir a tabela**; para apagar só as linhas, os candidatos são `DELETE` e `TRUNCATE`.

### 3.4 TRUNCATE — esvaziar de uma vez

O `TRUNCATE TABLE` **remove todas as linhas** de uma tabela, mas **mantém a estrutura** (as colunas e restrições continuam existindo). É rápido porque não gera log linha a linha na maioria dos SGBDs. E aqui mora a pegadinha mais clássica do tópico:

> [!warning] PEGADINHA — TRUNCATE vs. DELETE
> | | `TRUNCATE TABLE` | `DELETE FROM` |
> |---|---|---|
> | O que remove | **todas** as linhas, de uma vez | linhas selecionadas pelo `WHERE` |
> | Aceita `WHERE` | **não** | sim |
> | Mantém a estrutura | sim | sim |
> | Pode ser revertido com `ROLLBACK`? | em geral **não** (comporta-se como DDL; há exceções em alguns SGBDs) | sim, se ainda não houve `COMMIT` |
> | Dispara triggers de linha | em geral **não** | sim |
> | Classificação usual | **DDL** | **DML** |
>
> Frases clássicas de prova: "o comando que elimina todas as linhas de uma tabela sem condições e sem disparar triggers é o `TRUNCATE`"; "o comando que permite apagar apenas algumas linhas mediante condição é o `DELETE`". O `TRUNCATE` **não aceita** `WHERE` — se você viu um `TRUNCATE` com filtro, está vendo um erro.

---

## 4. DML — dando vida aos dados

### 4.1 INSERT — inserir dados

```sql
-- Inserindo um registro por vez
INSERT INTO cliente (cod_cliente, nome, email, cidade)
VALUES (1, 'Ana Souza', 'ana@email.com', 'Recife');

-- Inserindo vários registros de uma vez (multi-VALUES)
INSERT INTO cliente (cod_cliente, nome, email, cidade) VALUES
(2, 'Bruno Lima',    'bruno@email.com', 'Olinda'),
(3, 'Carla Dias',    'carla@email.com', 'Recife'),
(4, 'Daniel Melo',   'daniel@email.com', 'Paulista');

INSERT INTO produto (cod_produto, descricao, preco_unitario) VALUES
(7,  'Teclado mecânico',     320.00),
(9,  'Mouse sem fio',         95.00),
(15, 'Monitor 24 polegadas', 850.00),
(21, 'Webcam Full HD',       150.00);

INSERT INTO pedido (num_pedido, data_venda, cod_cliente) VALUES
(1001, '2026-08-10', 1),
(1002, '2026-08-11', 2),
(1003, '2026-08-12', 1),
(1004, '2026-08-15', 3);

INSERT INTO pedido_produto (num_pedido, cod_produto, quantidade) VALUES
(1001, 7,  1),
(1002, 9,  2),
(1002, 7,  1),
(1003, 9,  1),
(1004, 15, 1),
(1004, 7,  2);
```

> [!tip] Multi-VALUES ≠ Oracle
> A inserção múltipla com `VALUES (...), (...), (...)`, mostrada acima, é padrão no PostgreSQL e no MySQL. No **Oracle**, o comando clássico é `INSERT ALL` ou um `INSERT` por linha. Em prova, o raciocínio não muda: o que `INSERT` faz é **adicionar tuplas** — e cada tupla deve respeitar as restrições (PK não duplicada, FK existente, `NOT NULL` preenchido).

Dois detalhes que a banca explora: **violar a `FOREIGN KEY`** (inserir um pedido com `cod_cliente = 99` que não existe) gera erro — a integridade referencial impede; e **omitir a lista de colunas** (`INSERT INTO cliente VALUES (...)`) exige valores para *todas* as colunas, na ordem do `CREATE TABLE` — frágil e rejeitado se faltar alguma obrigatória.

### 4.2 UPDATE — alterar dados

```sql
UPDATE produto
SET preco_unitario = 300.00
WHERE descricao = 'Teclado mecânico';
```

> [!warning] PEGADINHA — UPDATE sem WHERE
> O `UPDATE` **sem `WHERE`** atualiza **todas** as linhas da tabela. `UPDATE produto SET preco_unitario = 300.00;` rebaixaria o preço de *todos* os produtos — e, sem `COMMIT`, um `ROLLBACK` ainda poderia salvar o dia (mas o próximo tópico, Transações e ACID, entra nesse detalhe). Sempre leia a questão procurando o `WHERE`: ele é o filtro que limita o alcance.

### 4.3 DELETE — apagar dados

```sql
DELETE FROM pedido_produto WHERE num_pedido = 1003;
```

O `DELETE` **remove linhas** da tabela, mantendo a estrutura (diferente do `DROP`, seção 3.3). Sem `WHERE`, remove todas as linhas (diferente do `TRUNCATE`, que é mais rápido mas não filtra e não dispara triggers). A hierarquia que você deve ter na cabeça:

- **`DROP TABLE`** → some a tabela inteira (estrutura + dados);
- **`TRUNCATE`** → esvazia todas as linhas (mantém estrutura; sem filtro; DDL);
- **`DELETE`** → apaga linhas, com ou sem filtro (mantém estrutura; DML);
- **`UPDATE`** → não apaga; altera valores.

### 4.4 SELECT — consultar

Aqui começa o coração do tópico. O `SELECT` **projeta** colunas e **filtra** linhas; depois veremos como ele **agrega**, **ordena** e **junta** tabelas.

```sql
-- Todas as colunas de todos os clientes
SELECT * FROM cliente;

-- Projeção: apenas algumas colunas
SELECT nome, cidade FROM cliente;

-- Com apelido de coluna (alias)
SELECT nome AS cliente, cidade AS uf FROM cliente;

-- Sem duplicatas
SELECT DISTINCT cidade FROM cliente;
```

> [!question] O que o * faz?
> O `SELECT *` ("selecionar tudo") devolve **todas as colunas** da tabela. Não confunda com "todas as linhas": *linhas* são controladas pelo `WHERE`; *colunas* são controladas pela lista após o `SELECT`. Essa distinção é cobrada em frases do tipo "o `SELECT * FROM cliente` retorna todas as linhas" — verdadeiro, mas o motivo é que não há `WHERE`, não porque o `*` filtra linhas.

---

## 5. WHERE, operadores lógicos e ORDER BY

### 5.1 O WHERE é uma proposição lógica

O `WHERE` recebe uma **condição** e devolve apenas as linhas em que ela é **verdadeira**. É aqui que a lógica proposicional da Fase 1 entra em campo: cada condição é uma proposição avaliada por linha; `AND`, `OR` e `NOT` seguem exatamente a tabela verdade que você estudou em [[Raciocinio-Matematico-Aplicado|RLM]].

```sql
-- Comparação simples
SELECT nome, cidade FROM cliente WHERE cidade = 'Recife';

-- Duas condições verdadeiras ao mesmo tempo (AND)
SELECT * FROM pedido
WHERE cod_cliente = 1 AND data_venda >= '2026-08-11';

-- Pelo menos uma verdadeira (OR)
SELECT * FROM produto
WHERE descricao LIKE 'Mouse%' OR preco_unitario < 100;

-- Negação (NOT)
SELECT * FROM cliente WHERE NOT cidade = 'Recife';
```

Operadores que a banca ama:

- comparação: `=`, `<>` (diferente), `>`, `<`, `>=`, `<=`;
- `BETWEEN a AND b` — intervalo **inclusivo** (equivale a `>= a AND <= b`);
- `IN (lista)` — pertence ao conjunto (equivale a vários `OR`); `NOT IN` é o complemento;
- `LIKE` — casamento de padrão: `%` casa qualquer sequência, `_` casa um caractere. `LIKE 'Mo%'` casa "Mouse", "Monitor"...; `LIKE '_ata'` casa "Data" (um caractere + "ata");
- `IS NULL` / `IS NOT NULL` — **nunca** use `= NULL`; `NULL` não é um valor, é a ausência de valor, e qualquer comparação com `NULL` resulta em *desconhecido*, não em verdadeiro ou falso.

> [!warning] PEGADINHA — NULL na condição
> `WHERE preco_unitario <> 300.00` **não retorna** as linhas em que `preco_unitario` é `NULL` — porque `NULL <> 300` é *desconhecido*, e o `WHERE` exige *verdadeiro*. É a famosa **lógica de três valores** (verdadeiro, falso, desconhecido). Para pegar os nulos, é obrigatório `WHERE preco_unitario IS NULL`. A FGV cobra essa armadilha com frequência — inclusive nas funções de agregação (seção 6.2).

### 5.2 ORDER BY — ordenar

```sql
SELECT nome, cidade FROM cliente ORDER BY nome;

SELECT num_pedido, data_venda, cod_cliente
FROM pedido
ORDER BY data_venda DESC, num_pedido ASC;
```

O `ORDER BY` ordena o resultado — `ASC` (crescente, padrão) ou `DESC` (decrescente) — e aceita **várias colunas**: a primeira é o critério principal; as seguintes desempatam. Na ordem lógica de execução (seção 5.3), o `ORDER BY` é **o último** passo — por isso ele consegue ordenar por colunas calculadas no `SELECT`, como `ORDER BY faturamento DESC`.

### 5.3 A ordem lógica de execução — a chave para entender SQL

O SQL **não** executa as cláusulas na ordem em que você as escreve. A ordem **lógica** (a que o SGBD segue, conceitualmente) é esta:

1. `FROM` — escolhe as tabelas (e aplica JOINs);
2. `WHERE` — filtra **linhas**;
3. `GROUP BY` — forma os **grupos**;
4. `HAVING` — filtra **grupos**;
5. `SELECT` — calcula projeções e agregações;
6. `ORDER BY` — ordena o resultado final.

Guarde essa sequência: ela explica as duas pegadinhas mais rentáveis do SQL — por que `WHERE` não pode usar funções de agregação (o agrupamento ainda não aconteceu quando o `WHERE` roda) e por que `HAVING` existe (é o filtro *depois* do `GROUP BY`).

---

## 6. Funções de agregação, GROUP BY e HAVING

### 6.1 As cinco funções de agregação

As funções de agregação resumem um conjunto de linhas em **um único valor**:

| Função | O que calcula | Atenção |
|---|---|---|
| `COUNT(*)` | número de **linhas** | conta inclusive linhas com nulos |
| `COUNT(coluna)` | número de valores **não nulos** da coluna | ignora `NULL` |
| `SUM(coluna)` | soma dos valores | ignora `NULL`; só numérica |
| `AVG(coluna)` | média aritmética = $\text{SUM} / \text{COUNT(nao nulos)}$ | ignora `NULL` no denominador |
| `MIN(coluna)` / `MAX(coluna)` | menor / maior valor | ignora `NULL`; serve para texto (ordem alfabética) também |

```sql
SELECT COUNT(*)            AS total_produtos,
       COUNT(preco_unitario) AS com_preco,
       SUM(preco_unitario) AS soma_precos,
       AVG(preco_unitario) AS media_precos,
       MIN(preco_unitario) AS mais_barato,
       MAX(preco_unitario) AS mais_caro
FROM produto;
```

### 6.2 A pegadinha do COUNT(*)

> [!warning] PEGADINHA — `COUNT(*)` vs. `COUNT(coluna)`
> Considere `produto` com 10 registros, dos quais 3 têm `preco_unitario` nulo. Então `COUNT(*)` = **10** (conta linhas), mas `COUNT(preco_unitario)` = **7** (conta valores não nulos). Mais sutil ainda: `AVG(preco_unitario)` soma os 7 valores e divide **por 7**, não por 10. Se a prova pergunta "qual a média dos preços considerando que 3 são desconhecidos?", a resposta correta é a média dos 7 conhecidos — salvo se o enunciado disser explicitamente "considere nulos como zero".

### 6.3 GROUP BY — formando grupos

O `GROUP BY` agrupa as linhas que têm o **mesmo valor** nas colunas listadas. Toda coluna do `SELECT` que **não** estiver dentro de uma função de agregação precisa estar no `GROUP BY` — regra de ouro.

```sql
-- Quantos clientes há em cada cidade?
SELECT cidade, COUNT(*) AS total_clientes
FROM cliente
GROUP BY cidade;

-- Quantos pedidos cada cliente realizou?
SELECT cod_cliente, COUNT(*) AS total_pedidos
FROM pedido
GROUP BY cod_cliente;
```

Lendo o segundo exemplo com a ordem lógica: o `FROM pedido` traz as 4 linhas; o `GROUP BY cod_cliente` forma 3 grupos (1, 2, 3); o `COUNT(*)` conta 2, 1 e 1 respectivamente.

### 6.4 HAVING — filtrando grupos (e a pegadinha WHERE vs. HAVING)

O `WHERE` filtra **linhas antes do agrupamento**. O `HAVING` filtra **grupos depois do agrupamento**. Essa é a distinção mais cobrada do SQL:

```sql
-- ERRADO: WHERE não pode usar função de agregação
SELECT cod_cliente, COUNT(*) AS total
FROM pedido
WHERE COUNT(*) > 1
GROUP BY cod_cliente;

-- CERTO: HAVING filtra o grupo após a agregação
SELECT cod_cliente, COUNT(*) AS total
FROM pedido
GROUP BY cod_cliente
HAVING COUNT(*) > 1;
```

> [!warning] PEGADINHA — WHERE vs. HAVING
> "Filtrar linhas antes de agrupar" = `WHERE`; "filtrar grupos após agrupar" = `HAVING`. A FGV mistura os dois em alternativas: a consulta correta para "clientes com **mais de um** pedido" usa `HAVING COUNT(*) > 1`; a consulta para "pedidos **do dia 10**" usa `WHERE data_venda = '2026-08-10'` (filtro de linha, antes de agrupar). Se você vir `WHERE COUNT(...)` — erro; se vir condição sobre uma coluna comum dentro do `HAVING` — funciona, mas é estilo ruim que a banca pode explorar.

E o exemplo clássico que combina tudo — agregação, agrupamento, filtro de grupo e ordenação:

```sql
-- Faturamento por cliente, apenas para quem faturou acima de 500,00
SELECT c.nome,
       SUM(pp.quantidade * p.preco_unitario) AS faturamento
FROM cliente c
JOIN pedido pd       ON pd.cod_cliente = c.cod_cliente
JOIN pedido_produto pp ON pp.num_pedido = pd.num_pedido
JOIN produto p       ON p.cod_produto = pp.cod_produto
GROUP BY c.cod_cliente, c.nome
HAVING SUM(pp.quantidade * p.preco_unitario) > 500
ORDER BY faturamento DESC;
```

Resultado com a nossa base: **Carla Dias** fatura 1490,00 (monitor 850 + 2 teclados 640) e **Bruno Lima** fatura 510,00 (2 mouses 190 + 1 teclado 320); Ana Souza (415,00) fica de fora pelo `HAVING`.

---

## 7. JOINs — juntando tabelas

### 7.1 O JOIN é uma operação entre conjuntos

No modelo relacional, as tabelas se conectam por **valores de chave** ([[Fundamentos-e-Modelagem]]). O `JOIN` materializa essa conexão: ele combina linhas de duas tabelas conforme uma **condição de junção** — normalmente a igualdade entre a chave estrangeira e a chave primária. Do ponto de vista do [[Raciocinio-Matematico-Aplicado|RLM]], pensamos em conjuntos: o `JOIN` seleciona pares segundo uma regra; o `CROSS JOIN` é o **produto cartesiano**; o `UNION` é a **união** de conjuntos; o `INTERSECT`, a **interseção**.

### 7.2 INNER JOIN — só o que casa

O `INNER JOIN` retorna apenas as linhas em que a condição de junção é satisfeita **nos dois lados**: linhas sem correspondência **somem**.

```sql
-- Clientes e seus pedidos (apenas clientes com pedido)
SELECT c.nome, p.num_pedido, p.data_venda
FROM cliente c
INNER JOIN pedido p ON p.cod_cliente = c.cod_cliente
ORDER BY c.nome;
```

Na nossa base, esse `INNER JOIN` retorna os 4 pedidos — e **Daniel**, que não tem pedido, não aparece.

### 7.3 LEFT JOIN — tudo do lado esquerdo

O `LEFT JOIN` retorna **todas** as linhas da tabela à esquerda do `JOIN`, mesmo sem correspondência; para as que não casam, as colunas da direita vêm **nulas**.

```sql
-- Todos os clientes, com ou sem pedido
SELECT c.nome, p.num_pedido
FROM cliente c
LEFT JOIN pedido p ON p.cod_cliente = c.cod_cliente
ORDER BY c.nome;
```

Agora **Daniel** aparece com `num_pedido = NULL` — e é exatamente assim que se descobre "quem nunca pediu":

```sql
SELECT c.nome
FROM cliente c
LEFT JOIN pedido p ON p.cod_cliente = c.cod_cliente
WHERE p.num_pedido IS NULL;
```

> [!warning] PEGADINHA — INNER vs. LEFT JOIN
> "Retornar todos os clientes, **inclusive os que nunca fizeram pedido**" exige `LEFT JOIN` — o `INNER JOIN` descartaria Daniel. A pegadinha inversa: "retornar apenas clientes **com** pedido" pode ser feita com `INNER JOIN` **ou** com `LEFT JOIN ... WHERE p.num_pedido IS NOT NULL` — a banca gosta de afirmar que "só o INNER serve", o que é falso. E o detalhe da ordem: em `A LEFT JOIN B`, todo `A` sobrevive; inverta os lados e o comportamento inverte junto.

### 7.4 RIGHT JOIN, FULL JOIN e CROSS JOIN

O `RIGHT JOIN` é o espelho do `LEFT`: preserva **todas** as linhas da tabela à **direita**. O `FULL OUTER JOIN` preserva **as duas**: clientes sem pedido **e** produtos sem venda aparecem com nulos no lado que falta.

```sql
-- Todos os produtos, com as quantidades vendidas (nulo se nunca vendido)
SELECT pr.descricao, pp.quantidade
FROM produto pr
LEFT JOIN pedido_produto pp ON pp.cod_produto = pr.cod_produto
ORDER BY pr.descricao;
```

Aqui, a **Webcam Full HD** (sem nenhuma venda) aparece com `quantidade = NULL`. O `FULL JOIN` faria o mesmo para os dois lados ao mesmo tempo.

O `CROSS JOIN` não usa condição: combina **cada linha de uma tabela com cada linha da outra** — o produto cartesiano.

```sql
-- Exemplo didático: 4 clientes × 4 produtos = 16 combinações
SELECT c.nome, pr.descricao
FROM cliente c
CROSS JOIN produto pr;
```

> [!warning] PEGADINHA — CROSS JOIN e produtos cartesianos
> O `CROSS JOIN` **não possui condição de junção** — e por isso, em bases reais, quase sempre gera resultado sem sentido (é o produto cartesiano que o [[Raciocinio-Matematico-Aplicado|RLM]] chama de $A \times B$). Cuidado com duas pegadinhas: (1) se você escrever um `INNER JOIN` **sem** o `ON`, alguns SGBDs o tratam implicitamente como produto cartesiano; (2) números de questão do tipo "qual o total de linhas do resultado?" pedem a **multiplicação** das cardinalidades: $4 \times 4 = 16$ linhas.

### 7.5 UNION, INTERSECT, EXCEPT — operações entre consultas

Fechando a ponte com conjuntos, o SQL também combina **resultados de consultas**, não tabelas:

- `UNION` — união (deduplica); `UNION ALL` — união mantendo duplicados (mais rápido);
- `INTERSECT` — elementos presentes nas duas;
- `EXCEPT` (ou `MINUS` no Oracle) — elementos da primeira que não estão na segunda.

```sql
-- Cidades onde há clientes OU produtos... (ilustrativo: as consultas
-- devem ter o mesmo número de colunas e tipos compatíveis)
SELECT cidade FROM cliente
UNION
SELECT 'loja virtual' FROM produto;
```

Na prova, as pegadinhas de `UNION` são: colunas em **número e tipo iguais** nas duas consultas; e `UNION` (com deduplicação) vs. `UNION ALL` (sem deduplicação).

---

## 8. Subconsultas — consulta dentro de consulta

Uma **subconsulta** é um `SELECT` interno usado dentro de outro comando — no `WHERE`, no `FROM` (como se fosse uma tabela derivada) ou até no `SELECT` (subconsulta escalar). A pegadinha mais cobrada: **quantas linhas a subconsulta pode retornar?**

- **Subconsulta escalar:** retorna **um único valor** (linha e coluna) — pode ser usada com `=`, `>`, `<`;
- **Subconsulta com `IN` / `NOT IN`:** retorna uma **lista** de valores — aí o `=` não funciona;
- **`EXISTS` / `NOT EXISTS`:** testa se a subconsulta retorna **ao menos uma linha** — não importa o conteúdo, só a existência. Por isso o padrão `SELECT 1` aparece dentro do `EXISTS`.

```sql
-- Quem comprou a partir de 2026-08-12? (com IN)
SELECT nome, email
FROM cliente
WHERE cod_cliente IN (
    SELECT cod_cliente
    FROM pedido
    WHERE data_venda >= '2026-08-12'
);

-- Clientes que fizeram pedido após 2026-08-15 (com EXISTS)
SELECT nome
FROM cliente c
WHERE EXISTS (
    SELECT 1
    FROM pedido p
    WHERE p.cod_cliente = c.cod_cliente
      AND p.data_venda >= '2026-08-15'
);

-- Total de pedidos de cada cliente (subconsulta escalar no SELECT)
SELECT c.nome,
       (SELECT COUNT(*)
        FROM pedido p
        WHERE p.cod_cliente = c.cod_cliente) AS total_pedidos
FROM cliente c;
```

> [!warning] PEGADINHA — `=` com subconsulta multilinha
> Quando a subconsulta pode retornar **mais de uma linha**, o `=` gera erro ("subconsulta retornou mais de um registro"). Para listas, use `IN`; para quantificar, `ANY`/`ALL` (ex.: `preco > ALL (SELECT ...)`), que a banca às vezes cita em alternativas: `> ALL` significa "maior que **todos**", `> ANY` significa "maior que **pelo menos um**".

---

## 9. Views, triggers e stored procedures

Os três objetos encerram o tópico no nível **conceito** (a ementa pede conceito) — mas cada um aparece em prova com cara de aplicação.

### 9.1 View — a tabela virtual

Uma **view** é uma **consulta armazenada** que se usa como se fosse uma tabela. Ela **não guarda dados** (na maioria dos casos — existem *materialized views*, que guardam, mas o conceito padrão é o de visão lógica): ao consultá-la, o SGBD executa o `SELECT` por trás dela.

```sql
CREATE VIEW v_faturamento_cliente AS
SELECT c.cod_cliente, c.nome,
       SUM(pp.quantidade * p.preco_unitario) AS faturamento
FROM cliente c
LEFT JOIN pedido pd       ON pd.cod_cliente = c.cod_cliente
LEFT JOIN pedido_produto pp ON pp.num_pedido = pd.num_pedido
LEFT JOIN produto p       ON p.cod_produto = pp.cod_produto
GROUP BY c.cod_cliente, c.nome;

-- Usar a view é como usar uma tabela
SELECT * FROM v_faturamento_cliente WHERE faturamento > 500;
```

As duas razões clássicas para views, ambas cobradas: **segurança** (expor apenas colunas permitidas — crucial sob a [[LGPD-Lei-Geral-de-Protecao-de-Dados|LGPD]], quando se quer liberar uma consulta de `nome` sem liberar `email` ou dados sensíveis) e **simplificação** (esconder a complexidade do JOIN de quem só precisa do resultado).

> [!warning] PEGADINHA — a view não é uma cópia
> "A view armazena uma cópia dos dados" — **falso** no conceito padrão. A view é uma *definição*: os dados continuam nas tabelas de origem. Se as tabelas originais mudam, a view reflete a mudança na próxima consulta. (A exceção é a *materialized view*, que guarda resultado físico — memória de prova para quando a banca quiser diferenciar.)

### 9.2 Trigger — a reação automática

Um **trigger** é um trecho de código que o SGBD executa **automaticamente** quando ocorre um evento: `INSERT`, `UPDATE` ou `DELETE` (antes ou depois da operação). O uso mais relevante para o contexto — e para a [[LGPD-Lei-Geral-de-Protecao-de-Dados|LGPD]] — é a **auditoria**: registrar quem alterou o quê e quando, sem depender da aplicação lembrar de fazer isso.

```sql
-- Conceito (o dialeto varia muito entre SGBDs)
CREATE TRIGGER trg_auditoria_pedido
AFTER INSERT ON pedido
FOR EACH ROW
    INSERT INTO log_auditoria (tabela, acao, id_registro, data_hora)
    VALUES ('pedido', 'INSERT', NEW.num_pedido, CURRENT_TIMESTAMP);
```

Raciocínio de prova: triggers **não são invocados manualmente** — uma questão que diz "o comando disparado automaticamente após um INSERT" está falando de trigger; e triggers servem para **automatizar regras** (auditoria, validação, sincronização), não para consultas.

### 9.3 Stored procedure — o programa dentro do banco

Uma **stored procedure** é um **conjunto de comandos SQL armazenado no banco**, com nome, parâmetros e lógica própria — o "programa" que vive dentro do SGBD. Vantagens que a banca cobra: **reuso** (várias aplicações chamam a mesma lógica), **desempenho** (menos tráfego entre aplicação e banco), **centralização da regra de negócio** e **segurança** (o usuário executa a procedure sem ganhar acesso direto às tabelas — sob a LGPD, um controle de acesso desejável).

```sql
-- Conceito (pseudocódigo; o dialeto varia)
CREATE PROCEDURE atualizar_preco (
    p_cod_produto INTEGER,
    p_novo_preco  NUMERIC(10,2)
) AS
BEGIN
    UPDATE produto
    SET preco_unitario = p_novo_preco
    WHERE cod_produto = p_cod_produto;
END;
```

> [!tip] View × Trigger × Procedure — como diferenciar na prova
> A **view** responde a **consultas** (é uma tabela virtual); o **trigger** reage a **eventos** (é automático); a **procedure** executa **lógica sob demanda** (é um programa chamado quando se quer). Se a frase fala em "chamar quando necessário" → procedure; "disparar automaticamente" → trigger; "consultar como tabela sem guardar dados" → view.

---

## 10. Como a FGV cobra — estratégia de leitura

- **Classifique o comando primeiro:** DDL (estrutura) ou DML (dados)? Isso elimina alternativas antes de qualquer análise de sintaxe.
- **Procure o `WHERE`:** ausência de `WHERE` em `UPDATE`/`DELETE` = operação em todas as linhas. Ausência de `WHERE` ao lado de `COUNT` = todas as linhas entram na conta.
- **Conte a ordem lógica:** `FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY`. Uma alternativa que usa `COUNT` no `WHERE` está errada; uma que usa condição comum no `HAVING` está mal escrita.
- **Desenhe o JOIN:** pergunte "quem deve sobreviver? Esquerda, direita ou os dois?" → `LEFT`, `RIGHT` ou `FULL`. "Apenas o que casa?" → `INNER`.
- **Cuidado com NULL:** `= NULL` não funciona; `COUNT(coluna)` ignora nulos; `LEFT JOIN` sem correspondência gera nulos — e nulos viram matéria-prima para descobrir "quem não tem filho".

---

## 11. Questões-modelo (na pegada da FGV)

> [!example] Questão-modelo 1 — GROUP BY, HAVING e a ordem dos filtros
> Considere a tabela `pedido(num_pedido, data_venda, cod_cliente)`. Um mesmo cliente pode ter vários pedidos. A consulta correta para retornar **os códigos dos clientes que fizeram mais de um pedido** é:
>
> A) `SELECT cod_cliente FROM pedido WHERE COUNT(*) > 1 GROUP BY cod_cliente;`
> B) `SELECT cod_cliente FROM pedido GROUP BY cod_cliente HAVING COUNT(*) > 1;`
> C) `SELECT cod_cliente FROM pedido HAVING COUNT(*) > 1 GROUP BY cod_cliente;`
> D) `SELECT cod_cliente, COUNT(*) FROM pedido WHERE COUNT(*) > 1;`
> E) `SELECT DISTINCT cod_cliente FROM pedido WHERE COUNT(*) > 1;`
>
> **Gabarito: B.** Nas alternativas A, D e E o `WHERE` tenta filtrar com função de agregação — impossível, pois o `WHERE` roda **antes** do agrupamento (ordem lógica da seção 5.3). Na C, a ordem sintática está invertida: o `HAVING` vem **depois** do `GROUP BY` (embora no nível conceitual a FGV considere a C incorreta por sintaxe — a gramática do SQL exige `GROUP BY` antes de `HAVING`). A B está correta: agrupa por cliente, conta os pedidos de cada grupo e filtra os grupos com contagem maior que 1.

> [!example] Questão-modelo 2 — TRUNCATE, DELETE e a classificação DDL/DML
> Um administrador de banco precisa **eliminar todas as linhas** de uma tabela de logs temporários, **sem registrar a exclusão linha a linha** e **sem disparar triggers** de auditoria. Mantendo a estrutura da tabela para uso futuro. O comando adequado é:
>
> A) `DROP TABLE logs_temporarios;`
> B) `DELETE FROM logs_temporarios;`
> C) `TRUNCATE TABLE logs_temporarios;`
> D) `ALTER TABLE logs_temporarios DELETE;`
> E) `UPDATE logs_temporarios SET excluido = 1;`
>
> **Gabarito: C.** O `TRUNCATE` esvazia a tabela mantendo a estrutura, não aceita `WHERE` e, na maioria dos SGBDs, não dispara triggers de linha — exatamente o que o enunciado pede. O `DROP` (A) eliminaria a tabela inteira (estrutura + dados); o `DELETE` (B) apaga linha a linha e dispararia triggers; a D mistura comandos que não existem; a E não apaga nada. Pegadinha clássica: o enunciado que pede "apenas algumas linhas" muda o gabarito para `DELETE ... WHERE`.

> [!example] Questão-modelo 3 — COUNT(*) vs. COUNT(coluna) com NULL
> A tabela `produto` possui 10 registros. Em 3 deles, a coluna `preco_unitario` é `NULL`; nos demais, os preços são 10,00, 20,00, 30,00, 40,00, 50,00, 60,00 e 70,00 (soma 280,00). Sobre `SELECT COUNT(*), COUNT(preco_unitario), SUM(preco_unitario), AVG(preco_unitario) FROM produto;`, o resultado correto é:
>
> A) 10 · 10 · 280 · 28
> B) 7 · 7 · 280 · 28
> C) 10 · 7 · 280 · 40
> D) 10 · 7 · 280 · 28
> E) 7 · 10 · 280 · 40
>
> **Gabarito: D.** `COUNT(*)` conta **linhas**: 10. `COUNT(preco_unitario)` conta **valores não nulos**: 7. `SUM(preco_unitario)` soma os não nulos: 280. E `AVG(preco_unitario)` divide a soma **pelo número de não nulos**: 280 / 7 = 40. As alternativas C e E trocam o denominador; a A conta os nulos como se fossem valores; a B confunde `COUNT(*)` com `COUNT(coluna)`.

---

## 12. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **DDL** = estrutura: `CREATE`, `ALTER`, `DROP`, `TRUNCATE`; **DML** = dados: `SELECT`, `INSERT`, `UPDATE`, `DELETE`
> - [ ] **Restrições**: `PRIMARY KEY` (integridade de entidade), `FOREIGN KEY` (integridade referencial), `NOT NULL`, `UNIQUE`, `CHECK`
> - [ ] **TRUNCATE** remove todas as linhas, mantém estrutura, sem `WHERE`, sem triggers; **DELETE** pode filtrar por `WHERE` e pode ser revertido; **DROP** extingue a tabela
> - [ ] **UPDATE/DELETE sem WHERE** = opera em todas as linhas — armadilha clássica
> - [ ] **WHERE** = condição por linha; comparações, `BETWEEN`, `IN`, `LIKE`, `IS NULL`; **nunca `= NULL`**
> - [ ] **Ordem lógica**: FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY
> - [ ] **`WHERE` filtra linhas antes de agrupar; `HAVING` filtra grupos depois de agrupar** — `COUNT` no `WHERE` é erro
> - [ ] **`COUNT(*)`** conta linhas; **`COUNT(coluna)`** conta não nulos; `AVG` divide pelos não nulos
> - [ ] **INNER** = só correspondências; **LEFT** = preserva a esquerda; **RIGHT** = preserva a direita; **FULL** = preserva ambos; **CROSS** = produto cartesiano, sem condição
> - [ ] **Subconsultas**: escalar com `=`, lista com `IN`, existência com `EXISTS`; `=` com multilinha gera erro
> - [ ] **View** = tabela virtual (não guarda dados); **Trigger** = reação automática a evento (auditoria); **Procedure** = lógica armazenada, chamada sob demanda
> - [ ] **LGPD**: `DELETE`/`UPDATE` mal escritos comprometem dados pessoais; views restringem acesso; triggers geram trilhas de auditoria

> [!warning] O erro mais comum em prova
> Aplicar filtro de grupo com `WHERE` e filtro de linha com `HAVING`, simultaneamente. Na hora da questão, pergunte: *isso é condição sobre a linha (WHERE) ou sobre o grupo já agregado (HAVING)?* E a segunda armadilha em frequência: esquecer que o `LEFT JOIN` gera `NULL` nas colunas da direita e que é esse `NULL` que permite encontrar "quem não tem correspondência".

---

## 13. Próximos passos

Você acabou de transformar o esquema das notas anteriores em **código executável**: sabe criar tabelas, inserir dados, consultar com filtros, agrupar, agregar, juntar tabelas e organizar consultas com views, triggers e procedures. Esse é o vocabulário que a FASE 4 (Desenvolvimento) vai exigir na prática, quando a aplicação conversar com o banco — mas isso vem depois.

O próximo tópico da ementa, dentro do próprio Bloco 3.1, é **Transações e ACID**: você já viu aqui os comandos `COMMIT` e `ROLLBACK` pairando nas discussões sobre `UPDATE` e `TRUNCATE` — o próximo passo é estudar exatamente como o SGBD garante que uma sequência de comandos seja tratada como uma **unidade indivisível**, o que é **isolamento** entre operações concorrentes e o que acontece quando duas transações **entram em deadlock**. Logo depois, o bloco fecha com **NoSQL** (onde a consistência estrita do ACID abre espaço para *eventual consistency*) e **Big Data** — tópicos que você já pode antecipar mentalmente como os "primos" do relacional.

Enquanto isso, a recomendação da ementa vale ouro: **pratique SQL**. Refaça os exemplos desta nota em um SGBD de estudos; mude os filtros, inverta os JOINs, acrescente um `HAVING` e veja o resultado mudar. Uma hora de prática aqui vale mais do que três de leitura — e a FGV sabe disso.