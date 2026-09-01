# Banco de Dados — Questões Autorais Comentadas

> **Disciplina:** Banco de Dados · **Bloco:** 3.1 — Banco de Dados (FASE 3 — Infraestrutura de Dados)
> **Banca de referência:** FGV · **Formato:** alternativas A–E
> **Origem:** autoral (todas) · **Não são questões oficiais de banca.**

---

## Questão 01 — Fundamentos e Modelagem: cardinalidade e mapeamento conceitual → lógico

**id:** BD-001
**disciplina:** Banco de Dados
**tópico:** Fundamentos e Modelagem
**subtópico:** Modelagem conceitual e lógica (entidade, relacionamento, cardinalidade, chaves PK/FK)
**origem:** autoral
**habilidade cognitiva:** análise e aplicação
**dificuldade:** média
**conhecimento avaliado:** leitura de cardinalidade 1:1/1:N/N:M pelos dois lados do relacionamento; mapeamento N:M para tabela associativa; chave primária composta e chaves estrangeiras; distinção entre entidade fraca e relacionamento com atributos

Ao modelar um sistema de atendimento de um consultório, o analista levantou as seguintes regras de negócio:

- cada médico atende vários pacientes;
- cada paciente pode ser atendido por vários médicos;
- de cada consulta, é necessário guardar a data e o valor cobrado.

Assinale a opção que descreve corretamente a modelagem conceitual e lógica desse cenário.

A) A cardinalidade entre MÉDICO e PACIENTE é 1:N, pois um médico atende vários pacientes; no modelo lógico, a chave primária de MÉDICO entra como chave estrangeira em PACIENTE.

B) A cardinalidade entre MÉDICO e PACIENTE é N:M; no modelo lógico, o relacionamento é implementado por uma tabela associativa CONSULTA(cod_medico, cod_paciente, data, valor), cuja chave primária é composta pelas chaves das duas entidades, e a data e o valor entram como colunas dessa tabela.

C) A cardinalidade entre MÉDICO e PACIENTE é 1:1, pois cada consulta envolve exatamente um médico e um paciente; no modelo lógico, a chave primária de uma das entidades é transformada em chave estrangeira da outra.

D) No modelo conceitual, CONSULTA deve ser representada como uma entidade fraca dependente de MÉDICO, porque a data e o valor de uma consulta não podem existir sem o médico.

E) A cardinalidade entre MÉDICO e PACIENTE é N:M; no modelo lógico, o relacionamento é implementado adicionando-se a chave primária de PACIENTE como coluna em MÉDICO e a chave primária de MÉDICO como coluna em PACIENTE.

---

**Gabarito:** B

### Comentário

**Raciocínio:** A questão pede traduzir um texto de regras de negócio em modelo conceitual (cardinalidade) e em modelo lógico (tabelas e chaves). O primeiro passo é ler a cardinalidade **dos dois lados**: pergunte "quantas consultas um médico tem?" e "quantos médicos um paciente tem?". Só depois de responder às duas perguntas é possível decidir entre 1:1, 1:N e N:M — e então aplicar a regra de mapeamento correta.

**Palavra-chave:** "vários médicos" + "vários pacientes" = N:M; N:M → tabela associativa com chave composta; atributos do relacionamento entram na associativa.

**Conceito:**
- **Cardinalidade:** o relacionamento MÉDICO–PACIENTE é **N:M**, porque um médico se associa a vários pacientes **e** um paciente se associa a vários médicos. Quem lê apenas um lado ("um médico atende vários pacientes") conclui 1:N e cai na pegadinha.
- **Mapeamento N:M:** no modelo lógico, todo relacionamento N:M vira uma **tabela associativa** cuja chave primária é **composta** pelas chaves primárias das duas entidades — que são, ao mesmo tempo, **chaves estrangeiras** para MÉDICO e PACIENTE.
- **Atributos do relacionamento:** `data` e `valor` não pertencem nem ao médico nem ao paciente — pertencem à associação *consulta*. Por isso entram como colunas da tabela associativa, exatamente como a opção B descreve.
- **Entidade fraca:** só existe em função de outra (ex.: DEPENDENTE em relação a FUNCIONÁRIO) e tem chave parcial. CONSULTA aqui é um **relacionamento com atributos**, não uma entidade fraca.

**Análise das alternativas:**
- **A (errada):** conclui 1:N olhando somente o lado do médico; ignora a regra "cada paciente pode ser atendido por vários médicos".
- **B (correta):** identifica N:M, usa a tabela associativa com chave composta e coloca `data` e `valor` como colunas dela.
- **C (errada):** a cardinalidade 1:1 não corresponde ao enunciado; cada entidade se relaciona com vários da outra.
- **D (errada):** confunde relacionamento com atributos e entidade fraca; uma entidade fraca depende de outra **entidade**, e sua identificação exige chave parcial, o que não é o caso.
- **E (errada):** diz N:M, mas propõe "espalhar" as chaves nas duas tabelas originais — isso duplicaria dados e violaria a modelagem; a forma correta é a tabela associativa.

**Pegadinha:** A opção A é a armadilha clássica: o enunciado afirma que "um médico atende vários pacientes" e o candidato conclui 1:N sem verificar o lado inverso. A leitura correta exige as **duas** perguntas de cardinalidade. Já a opção E acerta a cardinalidade e erra o mapeamento — quem conhece a regra N:M → tabela associativa elimina a alternativa sem hesitar.

---

## Questão 02 — Normalização: dependências funcionais, 2FN/3FN e decomposição

**id:** BD-002
**disciplina:** Banco de Dados
**tópico:** Normalização
**subtópico:** Formas normais (1FN, 2FN, 3FN), dependências funcionais, decomposição sem perda
**origem:** autoral
**habilidade cognitiva:** análise
**dificuldade:** média-alta
**conhecimento avaliado:** identificação de chave a partir das DFs; dependência parcial (2FN) vs. dependência transitiva (3FN); hierarquia das formas normais; decomposição correta a partir das dependências parciais

Considere a relação ALOCACAO(cod_funcionario, cod_projeto, nome_funcionario, nome_projeto, horas, uf_projeto) e as dependências funcionais:

- `cod_funcionario → nome_funcionario`
- `cod_projeto → nome_projeto`
- `cod_projeto → uf_projeto`
- `(cod_funcionario, cod_projeto) → horas`

Sobre a normalização dessa relação, analise as afirmativas a seguir:

I. A chave primária da relação é `(cod_funcionario, cod_projeto)`, e a relação está na 1FN, mas não na 2FN, porque `nome_funcionario` depende apenas de parte da chave.

II. A relação está na 3FN, pois nenhum atributo não chave depende de outro atributo não chave.

III. A dependência funcional `cod_projeto → uf_projeto` é uma dependência parcial, que impede a relação de estar na 2FN.

IV. Uma decomposição em FUNCIONARIO(cod_funcionario, nome_funcionario), PROJETO(cod_projeto, nome_projeto, uf_projeto) e ALOCACAO(cod_funcionario, cod_projeto, horas) elimina as dependências parciais, preserva as chaves e não perde informação.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I e II
B) I, III e IV
C) II e IV
D) I e III
E) III e IV

---

**Gabarito:** B

### Comentário

**Raciocínio:** Questão de normalização exige o roteiro: (1) listar as DFs; (2) achar a chave candidata — o conjunto mínimo que determina todos os atributos; (3) procurar não chave dependente de *parte* da chave (→ fora da 2FN) e não chave dependente de *outro não chave* (→ fora da 3FN); (4) verificar a decomposição proposta. O fecho de `(cod_funcionario, cod_projeto)` cobre todos os atributos, e nenhum dos dois isoladamente cobre: logo, essa é a chave composta.

**Palavra-chave:** chave composta; dependência **parcial** = não chave depende de parte da chave (2FN); 3FN exige 2FN; decompor = retirar cada porção da chave com seus dependentes.

**Conceito:**
- **Afirmativa I é verdadeira.** A chave é `(cod_funcionario, cod_projeto)`; `nome_funcionario` depende de `cod_funcionario` (parte da chave) — é uma **dependência parcial**, que viola a 2FN. A relação está na 1FN (valores atômicos, sem grupos repetitivos).
- **Afirmativa II é falsa.** A 3FN exige, como condição, estar na 2FN. Como existem dependências parciais, a relação **não está nem na 2FN**, logo não pode estar na 3FN — ainda que não haja cadeia transitiva entre atributos não chave.
- **Afirmativa III é verdadeira.** `cod_projeto → uf_projeto` depende apenas de uma parte da chave composta: é exatamente uma dependência parcial, a doença que impede a 2FN.
- **Afirmativa IV é verdadeira.** A decomposição separa cada "porção da chave" com seus dependentes (FUNCIONARIO e PROJETO) e mantém a relação central com a chave inteira (ALOCACAO). A decomposição é **sem perda**: a interseção entre FUNCIONARIO e ALOCACAO é `cod_funcionario` (chave de FUNCIONARIO), e a interseção entre PROJETO e ALOCACAO é `cod_projeto` (chave de PROJETO) — a junção devolve a relação original sem linhas espúrias.

**Análise das alternativas:**
- **A (I e II):** errada — II é falsa (não há 3FN sem 2FN).
- **B (I, III e IV):** correta.
- **C (II e IV):** errada — II é falsa e I/III (verdadeiras) ficam de fora.
- **D (I e III):** errada — IV também é verdadeira.
- **E (III e IV):** errada — I também é verdadeira.

**Pegadinha:** A afirmativa II é a armadilha central: ela afirma que "não há transitividade, logo está na 3FN", ignorando que a 3FN **herda** a 2FN. A hierarquia é BCNF ⊂ 3FN ⊂ 2FN ⊂ 1FN — quem pula degraus erra. E a afirmativa III explora a confusão clássica entre **dependência parcial** (depende de parte da chave) e **transitiva** (depende de outro não chave): ambas impedem formas normais diferentes, e aqui o caso é parcial, pois o determinante `cod_projeto` é parte da chave.

---

## Questão 03 — SQL DDL e DML: JOIN, GROUP BY, HAVING e agregação

**id:** BD-003
**disciplina:** Banco de Dados
**tópico:** SQL — DDL e DML
**subtópico:** INNER JOIN, GROUP BY/HAVING, funções de agregação, ORDER BY
**origem:** autoral
**habilidade cognitiva:** aplicação (ler SQL e prever o resultado)
**dificuldade:** média
**conhecimento avaliado:** comportamento do INNER JOIN (linhas sem correspondência somem); diferença entre WHERE (filtra linhas) e HAVING (filtra grupos); SUM como agregação por grupo; ordem de exibição com ORDER BY DESC

Considere o esquema e os dados de um sistema de vendas:

```
cliente(cod_cliente, nome)
compra(num_compra, cod_cliente, valor_total)
```

| cod_cliente | nome |
|---|---|
| 1 | Ana |
| 2 | Bruno |
| 3 | Carla |
| 4 | Daniel |

| num_compra | cod_cliente | valor_total |
|---|---|---|
| 101 | 1 | 300,00 |
| 102 | 1 | 200,00 |
| 103 | 2 | 100,00 |
| 104 | 3 | 600,00 |

Considere a consulta:

```sql
SELECT c.nome, SUM(co.valor_total) AS total
FROM cliente c
INNER JOIN compra co ON co.cod_cliente = c.cod_cliente
GROUP BY c.cod_cliente, c.nome
HAVING SUM(co.valor_total) > 300
ORDER BY total DESC;
```

O resultado exibido por essa consulta, na ordem de exibição, é:

A) Carla – 600,00; Ana – 500,00
B) Ana – 500,00; Carla – 600,00
C) Carla – 600,00; Ana – 500,00; Bruno – 100,00
D) Ana – 500,00; Carla – 600,00; Bruno – 100,00
E) Carla – 600,00; Ana – 500,00; Daniel – NULL

---

**Gabarito:** A

### Comentário

**Raciocínio:** A questão cobra a habilidade de **simular a execução da consulta na ordem lógica do SQL**: `FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY`. Percorra os dados: (1) o `INNER JOIN` combina cada compra com seu cliente; (2) o `GROUP BY` forma um grupo por cliente; (3) o `SUM` calcula o total de cada grupo; (4) o `HAVING` descarta grupos com total ≤ 300; (5) o `ORDER BY total DESC` ordena do maior para o menor.

**Palavra-chave:** INNER JOIN (só o que casa); WHERE = filtra linhas, HAVING = filtra grupos; SUM por grupo; ORDER BY DESC.

**Conceito:**
- **INNER JOIN:** retorna apenas os pares com correspondência nos dois lados. Daniel (cod_cliente 4) **não possui compra** — a linha dele jamais entra no agrupamento. Se fosse `LEFT JOIN`, Daniel apareceria com `total = NULL`.
- **GROUP BY c.cod_cliente, c.nome:** forma três grupos: Ana (compras 101 e 102 → 500,00), Bruno (compra 103 → 100,00) e Carla (compra 104 → 600,00).
- **HAVING SUM(co.valor_total) > 300:** filtra **grupos já agregados** — Bruno (100,00) é eliminado; Ana (500,00) e Carla (600,00) permanecem. O `HAVING` é o único lugar para filtrar com função de agregação; o `WHERE` rodaria antes do agrupamento e não poderia usar `SUM`.
- **ORDER BY total DESC:** Carla (600,00) vem antes de Ana (500,00).

**Análise das alternativas:**
- **A (correta):** Carla – 600,00; Ana – 500,00, nessa ordem.
- **B (errada):** inverte a ordem — esqueceu o `DESC`.
- **C (errada):** inclui Bruno — ignorou o `HAVING` (100,00 não é maior que 300,00).
- **D (errada):** inverte a ordem **e** inclui Bruno.
- **E (errada):** inclui Daniel com NULL — quem responde isso confundiu `INNER JOIN` com `LEFT JOIN` (no INNER, Daniel simplesmente não aparece) e esqueceu o `HAVING`.

**Pegadinha:** A questão combina as três armadilhas mais cobradas em SQL: (1) **INNER vs. LEFT JOIN** — o candidato que pensa "quero todos os clientes" troca o join e "ressuscita" Daniel com NULL; (2) **WHERE vs. HAVING** — filtrar o total com `HAVING` é obrigatório, pois a condição é sobre o grupo agregado; (3) **ordem do ORDER BY** — o `DESC` coloca Carla antes de Ana. Refaça a consulta no papel, grupo por grupo, antes de marcar.

---

## Questão 04 — Transações e ACID: propriedades, níveis de isolamento e deadlock

**id:** BD-004
**disciplina:** Banco de Dados
**tópico:** Transações e ACID
**subtópico:** Propriedades ACID; níveis de isolamento (READ COMMITTED, SERIALIZABLE); deadlock e mecanismos de resolução
**origem:** autoral
**habilidade cognitiva:** análise
**dificuldade:** média
**conhecimento avaliado:** definição exata de cada propriedade ACID (atomicidade vs. durabilidade); anomalias de concorrência por nível de isolamento; conceito de deadlock e resolução por detecção de ciclo no grafo de espera

Considere as afirmativas a seguir sobre transações em bancos de dados:

I. A atomicidade garante que, após o COMMIT, as alterações da transação são permanentes e sobrevivem a falhas de energia ou queda do servidor.

II. No nível de isolamento READ COMMITTED, uma transação não pode ler dados ainda não confirmados por outra transação (dirty read), mas pode ler a mesma linha com valores diferentes em duas consultas dentro da mesma transação (non-repeatable read).

III. No nível SERIALIZABLE, as transações concorrentes são executadas simultaneamente, sem espera umas pelas outras, o que maximiza o desempenho do banco.

IV. Um deadlock ocorre quando duas ou mais transações ficam em espera circular, cada uma aguardando um recurso retido por outra; o SGBD pode resolvê-lo detectando ciclos no grafo de espera e desfazendo (rollback) uma das transações, chamada vítima.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I e II
B) II e IV
C) III e IV
D) I, II e III
E) Apenas II

---

**Gabarito:** B

### Comentário

**Raciocínio:** A questão mistura os dois pontos mais cobrados do tópico: a **troca de definições entre propriedades ACID** e a **relação entre nível de isolamento e anomalias**. O roteiro é: (1) identificou "tudo ou nada" → atomicidade; (2) identificou "depois do COMMIT não se perde" → durabilidade; (3) para cada nível de isolamento, pergunte quais anomalias ele impede; (4) para deadlock, procure a espera circular com locks.

**Palavra-chave:** atomicidade = tudo ou nada; durabilidade = permanência após COMMIT; READ COMMITTED impede dirty read; SERIALIZABLE = execução como se fosse em série; deadlock = ciclo no grafo de espera.

**Conceito:**
- **Afirmativa I é falsa.** A descrição é da **durabilidade** (após o COMMIT, nada se perde). A **atomicidade** garante que a transação é indivisível — ou todos os comandos valem, ou nenhum; se uma falha interrompe a transação antes do COMMIT, tudo é desfeito. A FGV adora apresentar a definição de uma propriedade no lugar de outra.
- **Afirmativa II é verdadeira.** O `READ COMMITTED` impede **dirty reads** (só lê dados confirmados), mas permite **non-repeatable reads**: entre duas leituras da mesma linha, outra transação pode alterar e confirmar o valor. É o nível padrão do PostgreSQL e da Oracle.
- **Afirmativa III é falsa.** No `SERIALIZABLE`, as transações se comportam **como se fossem executadas em série** — há espera e maior disputa por locks; o desempenho **cai**, não melhora. "Executadas simultaneamente sem espera" é o oposto do que o nível garante.
- **Afirmativa IV é verdadeira.** Deadlock é a **espera circular**: T1 espera recurso de T2, T2 espera recurso de T1. A resolução sofisticada é a **detecção** — o SGBD mantém o grafo de espera, encontra o **ciclo** e escolhe uma **vítima**, que é desfeita com rollback, liberando os recursos.

**Análise das alternativas:**
- **A (I e II):** errada — I é falsa (troca atomicidade por durabilidade).
- **B (II e IV):** correta.
- **C (III e IV):** errada — III é falsa (SERIALIZABLE não elimina a espera).
- **D (I, II e III):** errada — I e III são falsas.
- **E (Apenas II):** errada — IV também é verdadeira.

**Pegadinha:** Duas inversões clássicas: (1) na afirmativa I, a definição de **durabilidade** é atribuída à **atomicidade** — o candidato que decorou "A = tudo ou nada" reconhece a troca; (2) na afirmativa III, o `SERIALIZABLE` é descrito como "simultâneo e sem espera" — na verdade ele **serializa** as transações, trocando velocidade por isolamento. Para deadlock, lembre do padrão: **T1 espera T2, T2 espera T1** → ciclo → deadlock; resolver o ciclo escolhendo uma vítima é detecção, não prevenção (que usaria, por exemplo, ordenação global dos recursos).

---

## Questão 05 — NoSQL: tipos de bancos e consistência eventual vs. forte

**id:** BD-005
**disciplina:** Banco de Dados
**tópico:** NoSQL
**subtópico:** Tipos de NoSQL (document, key-value, column-family); eventual consistency vs. strong consistency
**origem:** autoral
**habilidade cognitiva:** compreensão e análise
**dificuldade:** fácil-média
**conhecimento avaliado:** características dos tipos document (MongoDB), key-value (Redis) e column-family (Cassandra); significado de consistência eventual vs. consistência forte em sistemas distribuídos

Considere as afirmativas a seguir sobre bancos NoSQL:

I. No MongoDB, exemplo de banco de documentos, cada registro é armazenado como um documento (tipicamente em formato JSON), e a coleção não exige esquema fixo: um documento pode ter campos que outro não possui.

II. No Redis, exemplo de banco key-value em memória, a operação natural de leitura é pela chave; localizar registros pelo conteúdo armazenado no valor exige varredura e não é eficiente.

III. O Cassandra é um banco do tipo column-family, projetado para escrita em altíssima vazão, distribuída horizontalmente pela adição de novos servidores.

IV. Na consistência eventual (eventual consistency), após uma escrita confirmada, toda leitura subsequente em qualquer réplica enxerga imediatamente o novo valor.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I, II e III
B) I, II e IV
C) II, III e IV
D) I, II, III e IV
E) Apenas I e II

---

**Gabarito:** A

### Comentário

**Raciocínio:** A questão combina as características concretas dos quatro tipos de NoSQL com a distinção entre consistência eventual e forte. Avalie cada afirmativa contra o que cada modelo realmente faz: documento = JSON com esquema flexível; key-value = acesso por chave (o valor é opaco); column-family = escrita distribuída em larga escala; consistência eventual = réplicas divergem e **convergem** — a leitura logo após a escrita **pode** estar defasada.

**Palavra-chave:** MongoDB = document (JSON, esquema flexível); Redis = key-value em memória (acesso por chave); Cassandra = column-family (escrita massiva distribuída); consistência eventual = convergência posterior (leitura pode ser defasada).

**Conceito:**
- **Afirmativa I é verdadeira.** O banco de **documentos** guarda cada registro como um documento autossuficiente, geralmente JSON, sem schema fixo — a flexibilidade de estrutura é a marca do modelo.
- **Afirmativa II é verdadeira.** No **key-value**, a busca natural é **pela chave**; o valor é opaco para o banco, e encontrar valores por conteúdo exigiria varrer todos os registros. É o modelo do Redis, que opera majoritariamente em memória (baixa latência).
- **Afirmativa III é verdadeira.** O **Cassandra** (column-family) foi projetado para distribuição horizontal e escrita com altíssima vazão — o caso clássico de logs, eventos e séries temporais. (Cuidado: isso **não** é o mesmo que banco colunar para análise OLAP, do bloco de BI.)
- **Afirmativa IV é falsa.** A descrição é da **consistência forte (strong consistency)**: leitura sempre vê a escrita mais recente, com réplicas coordenadas. Na **consistência eventual**, as réplicas podem **divergir temporariamente**; uma leitura imediatamente após a escrita pode retornar dado **defasado**, e, na ausência de novas escritas, as réplicas **convergem** para o mesmo valor.

**Análise das alternativas:**
- **A (I, II e III):** correta — IV é falsa.
- **B (I, II e IV):** errada — IV descreve consistência forte, não eventual.
- **C (II, III e IV):** errada — inclui IV (falsa) e exclui I (verdadeira).
- **D (I, II, III e IV):** errada — quem confunde eventual com forte marca todas.
- **E (Apenas I e II):** errada — III também é verdadeira.

**Pegadinha:** A afirmativa IV inverte eventual e forte — o espelho da pegadinha dos "dois C's": no ACID, C significa integridade das regras; em bancos distribuídos, consistência diz respeito à **igualdade entre réplicas**. Na consistência eventual, "divergir por um tempo e depois convergir" é a regra, não a exceção; a frase "leitura imediatamente enxerga o novo valor" descreve a consistência **forte**. Outra armadilha latente: associar Cassandra ao banco colunar de BI — o column-family é de escrita distribuída, não de análise OLAP.

---

## Padrões de cobrança utilizados

As questões autorais acima foram inspiradas nos seguintes padrões de cobrança identificados nas questões reais FGV:

1. **Esquema real em SQL + prever resultado/propriedades** (DATAPREV 2024 — Analista Engenharia e Sustentação): habilidade de ler DDL/DML e simular mentalmente a execução, com atenção a agrupamento, agregação e ordenação. Inspiração para BD-003.
2. **Leitura de cardinalidade em cenário textual + mapeamento conceitual → lógico** (padrão FGV em modelagem): entidades, relacionamentos, cardinalidade 1:1/1:N/N:M, chaves primárias e estrangeiras; as alternativas misturam os níveis de modelagem. Inspiração para BD-001.
3. **Normalização com dependências funcionais** (FGV CNS402 e DATAPREV 2024 — 1FN/2FN/3FN, superchave mínima): achar a chave a partir das DFs, identificar dependência parcial vs. transitiva e avaliar decomposição. Inspiração para BD-002.
4. **ACID com definições trocadas** (FGV CNS402): apresentar a definição de uma propriedade no lugar de outra — a "pegadinha das definições trocadas" é padrão recorrente da FGV. Inspiração para BD-004.
5. **Níveis de isolamento e anomalias de concorrência** (padrão FGV em transações): tabela de anomalias por nível; SERIALIZABLE descrito como execução serial, com custo de desempenho. Inspiração para BD-004.
6. **Deadlock: espera circular e mecanismos de resolução** (padrão FGV em transações): detecção de ciclo no grafo de espera e escolha de vítima; distinção entre detecção, timeout e prevenção. Inspiração para BD-004.
7. **NoSQL: características concretas de tipos e produtos** (FGV CNS402 — MongoDB/BSON): diferenças entre document, key-value, column-family e graph; complementaridade com o relacional. Inspiração para BD-005.
8. **Eventual consistency vs. strong consistency** (padrão FGV em NoSQL): divergência temporária entre réplicas, convergência e leitura defasada; relação com sistemas distribuídos. Inspiração para BD-005.
9. **Julgamento de afirmativas (V/F)** — formato FGV clássico: múltiplas afirmações com uma ou duas falsas sutis, alternativas com combinações tecnicamente próximas. Inspiração para BD-002, BD-004 e BD-005.
10. **Alternativas tecnicamente próximas** (observação do Gran sobre FGV/DATAPREV): distratores construídos sobre erros comuns (troca de ordens, inversão de níveis, confusão de propriedades) e não sobre absurdos fáceis de eliminar. Aplicado em todas as questões.