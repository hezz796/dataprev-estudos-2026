# Transações e ACID

> [!info] Metadados
> **Disciplina:** Banco de Dados
> **Bloco:** 3.1 — Banco de Dados (FASE 3 — Infraestrutura de Dados)
> **Tópico:** 4. Transações e ACID
> **Subtópicos:** Propriedades ACID (Atomicidade, Consistência, Isolamento, Durabilidade) · Níveis de isolamento · Deadlocks (conceito e mecanismos de resolução)
> **Pré-requisitos:** [[SQL-DDL-e-DML]] (INSERT, UPDATE, DELETE, conceito de COMMIT/ROLLBACK), [[Fundamentos-e-Modelagem]] (chaves, integridade referencial, funções do SGBD), [[Normalizacao]] (consistência do esquema), [[Raciocinio-Matematico-Aplicado|Raciocínio Lógico Matemático]] (lógica, conjuntos, operações entre conjuntos) e [[LGPD-Lei-Geral-de-Protecao-de-Dados|Legislação/Segurança]] (privacidade e dados sensíveis — auditoria e logs de transações)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-28

---

## 1. Por que estudar transações?

Na nota anterior, você viu comandos como `UPDATE`, `DELETE` e `TRUNCATE` e, de passagem, os comandos `COMMIT` e `ROLLBACK`. Ficou no ar uma pergunta incômoda: *o que garante que, se o sistema cair no meio de uma operação, o banco não fique pela metade?* E outra, ainda mais prática em um sistema como o da DATAPREV: *o que impede duas pessoas de alterarem o mesmo benefício ao mesmo tempo e uma sobrescrever o trabalho da outra?*

Este tópico responde às duas. Uma **transação** é a **unidade lógica de trabalho** de um banco de dados: uma sequência de comandos tratada como **um bloco só**. As propriedades que fazem desse bloco algo confiável são as **ACID** — Atomicidade, Consistência, Isolamento e Durabilidade. O contexto deixa isso muito concreto: sistemas previdenciários processam **transferências de valores, concessões de benefícios, atualizações de vínculos** — operações que, interrompidas no meio, gerariam prejuízo direto ao cidadão. E como esses mesmos sistemas guardam **dados pessoais e sensíveis**, a [[LGPD-Lei-Geral-de-Protecao-de-Dados|LGPD]] cobra registros de auditoria — trilhas que dependem de saber exatamente **o que foi feito, quando e por quem**, o que nos remete aos logs de transação (seções 3.4 e 7).

> [!question] Pergunta orientadora
> Você transfere R$ 100,00 da sua conta para a de um amigo. O comando dá "débito na sua conta" e logo em seguida o servidor desliga, *antes* do crédito no amigo. O que aconteceu com os seus R$ 100,00? Existem três respostas possíveis (ficou consigo, foi para o amigo, ou sumiu) — e o **ACID** existe para garantir que a resposta seja sempre uma das duas primeiras, nunca a terceira.

---

## 2. O que é uma transação — COMMIT e ROLLBACK

Em SQL, abrimos uma transação com `BEGIN` (ou `START TRANSACTION`), executamos os comandos e a fechamos com um dos dois finais possíveis:

- **`COMMIT`** — confirma: torna **permanentes** todas as modificações da transação;
- **`ROLLBACK`** — desfaz: **descarta** todas as modificações, devolvendo o banco ao estado anterior à transação.

Veja o exemplo clássico, a transferência bancária — que vamos carregar pela nota inteira:

```sql
BEGIN;

UPDATE conta SET saldo = saldo - 100 WHERE cod_conta = 101;   -- débito
UPDATE conta SET saldo = saldo + 100 WHERE cod_conta = 202;   -- crédito

COMMIT;   -- os dois UPDATEs passam a valer juntos, permanentemente
```

O que aconteceria se o servidor caísse **entre** os dois `UPDATE`, antes do `COMMIT`? A resposta depende de um conceito que já passou por aqui ([[Fundamentos-e-Modelagem]]): **até o `COMMIT`, as modificações são temporárias** — podem ser desfeitas com `ROLLBACK` ou desfeitas automaticamente pelo SGBD em caso de falha. O débito sem o crédito **nunca** chega a ser persistido: ou a transação completa se confirma, ou nenhum dos dois comandos vale. É a **atomicidade** em ação — e ela será detalhada na seção 3.1.

> [!warning] PEGADINHA — COMMIT vs. ROLLBACK
> O `COMMIT` **confirma** e torna permanente; o `ROLLBACK` **desfaz** e descarta. A FGV adora inverter a frase: "o `ROLLBACK` torna permanentes as alterações da transação" — **falso**. E a pegadinha do `TRUNCATE` (vista em [[SQL-DDL-e-DML]]): antes do `COMMIT`, um `DELETE` pode ser desfeito com `ROLLBACK`; um `TRUNCATE`, na maioria dos SGBDs, **não** — comporta-se como DDL e não participa da transação da mesma forma.

### 2.1 Por que agrupar comandos? — um mesmo benefício, duas linhas

Nem só de transferências vive o exemplo. Pense na concessão de um benefício previdenciário fictício no sistema da DATAPREV: o processo pode precisar (1) criar o registro do benefício, (2) atualizar o vínculo do segurado, (3) gerar a primeira parcela. Se o sistema falhar após o passo 1, teríamos um "benefício sem segurado" — um dado órfão. **É a atomicidade que impede isso**: os três passos entram na mesma transação e só são confirmados juntos; se um falhar, os três são desfeitos. Repare que não se trata apenas de SQL: transação é o **agrupamento lógico de operações que só fazem sentido em conjunto** — e a prova costuma descrever essa situação em linguagem natural ("operação de depósito que atualiza duas tabelas e precisa ser confirmada como um todo").

---

## 3. As propriedades ACID

O acrônimo **ACID** descreve quatro garantias de uma transação. A ordem não é arbitrária: cada letra responde a um medo diferente de quem usa o banco.

> [!note] Palavras-chave do ACID
> **Atomicidade** (tudo ou nada) · **Consistência** (de estado válido a estado válido) · **Isolamento** (transações concorrentes não interferem) · **Durabilidade** (depois do COMMIT, não se perde mais). A banca cobra as quatro definições — e, principalmente, **saber identificar qual propriedade está sendo violada no cenário descrito**.

### 3.1 Atomicidade (A) — tudo ou nada

A **atomicidade** garante que a transação é **indivisível**: ou **todos** os comandos são executados, ou **nenhum** deles vale. Não existe "transação pela metade".

No exemplo da transferência: o débito de 100 na conta 101 e o crédito de 100 na conta 202 são **um único átomo** — se o segundo `UPDATE` falhar (conta inexistente, restrição violada, queda de energia), o SGBD **desfaz o primeiro automaticamente**. Os R$ 100,00 não "somem": voltam ao estado original.

Como o SGBD implementa isso? Com **logs de transação** (o *write-ahead log* ou WAL, em muitos SGBDs): antes de aplicar uma modificação, o banco registra em disco **como desfazê-la** (log de *undo*) e como refazê-la (log de *redo*). Com o log, o SGBD consegue:

- **desfazer** (rollback) o que a transação fez até o ponto da falha;
- **refazer** (recovery) operações de transações que já tinham `COMMIT` mas cujos dados ainda não haviam sido gravados em disco quando o sistema caiu.

> [!warning] PEGADINHA — atomicidade não é "gravar tudo de uma vez"
> Atomicidade **não** significa que os comandos são executados simultaneamente, nem que "todos os dados ficam prontos no mesmo instante". Significa que o **efeito final** é o de um bloco único: o mundo externo enxerga o banco **antes** ou **depois** da transação inteira, nunca no meio. A frase "a transação é atômica porque todos os comandos são executados ao mesmo tempo" é falsa.

### 3.2 Consistência (C) — de estado válido a estado válido

A **consistência** garante que a transação leva o banco de um **estado válido** a outro **estado válido**: nenhuma regra de integridade pode ser violada, mesmo que temporariamente, no final da transação. "Estado válido" é todo aquele que respeita as **regras do negócio** — e aqui entra a ponte direta com a [[Fundamentos-e-Modelagem]]:

- **chaves primárias** não podem duplicar nem ser nulas (integridade de entidade);
- **chaves estrangeiras** não podem apontar para registros inexistentes (integridade referencial) — um pedido não pode referenciar um cliente que não existe;
- restrições como `NOT NULL`, `UNIQUE` e `CHECK` (vistas em [[SQL-DDL-e-DML]]) também são regras de consistência;
- regras de negócio arbitrárias: "saldo não pode ficar negativo", "a soma dos valores de um pedido deve ser igual ao total".

O ponto fino — e o favorito da prova — é: **a consistência é uma propriedade que a transação ajuda a preservar, mas cujas regras pertencem ao banco** (definidas na modelagem). O SGBD não "adivinha" a regra do negócio: ela precisa estar declarada (chave, `CHECK`) ou implementada no código. Se a regra é "nunca deixar saldo negativo" e nenhuma restrição a declara, uma transação mal escrita pode violá-la mesmo dentro do ACID.

No exemplo da transferência: se a conta 101 tivesse apenas 50,00 e a transação tentasse debitar 100, um `CHECK (saldo >= 0)` faria o SGBD **rejeitar a transação inteira** — voltando ao estado válido anterior — em vez de deixar um saldo negativo de 50 (estado inválido).

> [!warning] PEGADINHA — Consistência ≠ "dados iguais"
> No ACID, **consistência** é sobre **regras e invariantes** (o banco respeita as restrições), **não** sobre "os dados são iguais em todas as cópias". O termo *consistency* com outro sentido (dados idênticos entre réplicas) aparece em bancos distribuídos e NoSQL — inclusive como *eventual consistency* — e será estudado no próximo tópico, NoSQL, como uma **consistência de replicação**, não a propriedade C do ACID. Guarde a distinção: no ACID, C = integridade das regras.

### 3.3 Isolamento (I) — transações concorrentes não interferem

O **isolamento** garante que transações executadas **ao mesmo tempo** (concorrentemente) produzam o mesmo resultado que se fossem executadas uma após a outra (serialmente). Em outras palavras: uma transação **não enxerga** as modificações não confirmadas de outra, e duas transações não devem atrapalhar uma às outras.

Volte à transferência: dois caixas, no mesmo instante, tentam movimentar a conta 101 — um deposita 50, outro deposita 100. Se o saldo atual é 200, o esperado ao final é 350. Sem isolamento, uma transação poderia ler o saldo enquanto a outra ainda não terminou, e ambas calcular "200 + o meu valor", gravando 250 e depois 300 — **perdendo** dinheiro. O isolamento escolhe **como** essas transações se comportam: se uma espera a outra terminar, ou se cada uma trabalha sobre uma cópia, etc. Depois, ele é medido em **graus** — os níveis de isolamento da seção 5.

A tensão fundamental que a banca sempre explora: **mais isolamento = mais segurança, menos concorrência** (as transações ficam mais lentas, esperando umas às outras); **menos isolamento = mais velocidade, mais risco de anomalias**. Não existe almoço grátis — o SGBD oferece níveis e o administrador escolhe o trade-off.

### 3.4 Durabilidade (D) — o que passou, passou

A **durabilidade** garante que, **após o `COMMIT`**, as modificações são **permanentes**: sobrevivem a falhas de energia, queda do SGBD, reinicialização do servidor. O mecanismo básico é a **gravação em log** (o *redo log*): quando a transação confirma, o SGBD garante que as informações necessárias para **refazê-la** já estão em disco — assim, mesmo que o dado ainda não tenha sido gravado na tabela (em disco), na recuperação o banco usa o log para **refazer** o que estava faltando.

Distinção de prova valiosa: **atomicidade** desfaz o que **não** foi confirmado; **durabilidade** preserva o que **já foi** confirmado. As duas trabalham com os logs — mas em direções opostas.

E a ponte com a [[LGPD-Lei-Geral-de-Protecao-de-Dados|LGPD]] é dupla: (1) a durabilidade protege dados de benefícios, contribuições e vínculos contra perda — um dever de **segurança** do art. 46 da LGPD; (2) os **logs de transação** são a matéria-prima das **trilhas de auditoria** — saber quem alterou um benefício, quando e de onde, é instrumento de **prestação de contas** e de resposta a incidentes (art. 48). A seção 7 fecha esse ponto.

---

## 4. Anomalias de concorrência — o que o isolamento impede

Se duas transações rodam ao mesmo tempo e **nenhum controle** existe, aparecem as anomalias clássicas. Conhecê-las é pré-requisito para entender os níveis de isolamento: cada nível veda um subconjunto delas.

### 4.1 Dirty read — leitura suja

Uma transação T1 **escreve** um valor (sem confirmar); outra transação T2 **lê** esse valor **antes** do `COMMIT`; depois T1 **desfaz** (rollback). T2 trabalhou com um dado que **nunca existiu de verdade** — leu uma "sujeira".

> [!example] Exemplo
> T1 debita 100 da conta 101: saldo 300 → 200 (ainda **sem** COMMIT). T2 consulta o saldo, vê **200** e decide conceder uma operação baseada nesse valor. T1 então executa `ROLLBACK` — o saldo volta a 300. T2 tomou decisão com um dado fantasma.

O antídoto mínimo: **nenhuma transação lê dados não confirmados** — é a promessa do nível `READ COMMITTED` (seção 5).

### 4.2 Non-repeatable read — leitura não repetível

Dentro da **mesma** transação, T2 lê o mesmo registro **duas vezes** e obtém **valores diferentes**, porque outra transação T1 **alterou e confirmou** entre as duas leituras.

> [!example] Exemplo
> T2 consulta o saldo da conta 101 → 300. T1 (concorrente) retira 100 e dá `COMMIT` → saldo 200. T2 consulta de novo → 200. A T2 "não consegue repetir" a leitura: mesmo lendo o mesmo dado, obteve resultados diferentes dentro da mesma transação.

O antídoto: **uma transação lê sempre o mesmo valor enquanto durar** — a promessa do nível `REPEATABLE READ`.

### 4.3 Phantom read — leitura fantasma

Uma transação T2 executa **duas vezes a mesma consulta por conjunto** (ex.: "soma dos saldos acima de 100") e, entre as duas execuções, outra transação T1 **insere** novas linhas (e confirma) que se encaixam na consulta — o resultado muda **porque o conjunto de linhas mudou**. As linhas novas são os "fantasmas".

> [!example] Exemplo
> T2 calcula `SUM(saldo)` das contas com saldo > 100 → 1.500,00. T1 insere uma nova conta com saldo 400 e confirma. T2 recalcula → 1.900,00. Nenhuma linha existente mudou — apareceu uma **linha nova** (o fantasma) que muda o agregado.

O antídoto mais forte: **impedir que inserções aconteçam na faixa consultada enquanto a transação durar** — a promessa do nível `SERIALIZABLE`.

### 4.4 Lost update — atualização perdida

Duas transações leem o mesmo valor, cada uma calcula a partir dele, e **a última gravação sobrescreve a primeira** — um dos incrementos se perde. É o cenário dos dois caixas da seção 3.3: leem 200, calculam 250 e 300, gravam — o resultado final é 300 (ou 250), não 350. A atualização de um **sumiu**.

> [!note] Palavras-chave das anomalias (para a prova)
> **Dirty read** = leitura de dado **não confirmado** (depois desfeito) · **Non-repeatable read** = **mesma linha**, valores diferentes na mesma transação · **Phantom read** = **conjunto** muda por **inserção** durante a transação · **Lost update** = gravação de uma transação **sobrescreve** a de outra. A FGV descreve o cenário em prosa e pergunta o nome da anomalia — preste atenção no verbo: *lê não confirmado* → dirty; *relê e muda* → non-repeatable; *linha nova no conjunto* → phantom; *dois escrevem e um perde* → lost update.

| Anomalia | O que acontece | Verbo-chave |
|---|---|---|
| Dirty read | ler dado não confirmado que depois foi desfeito | lê + rollback alheio |
| Non-repeatable read | mesma linha lida duas vezes, valores diferentes | relê + UPDATE alheio |
| Phantom read | mesma consulta, conjunto diferente (linhas novas) | refaz + INSERT alheio |
| Lost update | duas gravações concorrentes, uma sobrescreve a outra | escreve sobre escrita |

---

## 5. Níveis de isolamento

O padrão SQL define **quatro níveis de isolamento**, do mais fraco ao mais forte. Cada nível é definido por **quais anomalias ele permite** — essa é a forma mais cobrada na prova: a tabela das anomalias.

| Nível de isolamento | Dirty read | Non-repeatable read | Phantom read |
|---|---|---|---|
| `READ UNCOMMITTED` | **pode** | pode | pode |
| `READ COMMITTED` | **impede** | pode | pode |
| `REPEATABLE READ` | impede | **impede** | pode |
| `SERIALIZABLE` | impede | impede | **impede** |

- **`READ UNCOMMITTED`** — o nível mais fraco: uma transação pode ler dados **não confirmados** de outra (permite dirty read). Praticamente não há isolamento; usado em cenários onde a exatidão não importa muito.
- **`READ COMMITTED`** — a transação só lê dados **já confirmados** (impede dirty read), mas duas leituras dentro da mesma transação podem divergir se outra transação confirmar no meio (permite non-repeatable read). É o padrão do PostgreSQL e da Oracle.
- **`REPEATABLE READ`** — dentro da mesma transação, uma linha lida **não muda** (impede non-repeatable read); leituras por **conjunto** ainda podem ganhar linhas novas (permite phantom read). É o padrão do MySQL/InnoDB.
- **`SERIALIZABLE`** — o mais forte: as transações comportam-se **como se fossem executadas em série** (uma após a outra), mesmo rodando em paralelo. Impede as três anomalias. O preço é a **concorrência**: transações que disputam os mesmos dados ficam esperando umas às outras — e o risco de deadlock (seção 6) cresce.

> [!tip] O padrão de cada SGBD (referência de prova)
> O **padrão SQL** é o que cai em prova, mas a FGV às vezes menciona o comportamento real: o **PostgreSQL** usa `READ COMMITTED` por padrão; o **MySQL** (InnoDB) usa `REPEATABLE READ`; a **Oracle** usa `READ COMMITTED` e **não suporta** `READ UNCOMMITTED`. O `SERIALIZABLE` existe em todos — com custo de desempenho.

```sql
-- Como definir o nível de isolamento
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;
-- (nos SGBDs modernos, também como opção de sessão:
--  SET SESSION CHARACTERISTICS AS TRANSACTION ISOLATION LEVEL ...)
BEGIN;
SELECT ...;
COMMIT;
```

> [!warning] PEGADINHA — a coluna que decide o nível
> Não decore a tabela inteira: decore a **coluna do dirty read** e a **coluna do phantom**. `READ COMMITTED` = "nada de sujeira"; `SERIALIZABLE` = "nada de fantasmas"; `REPEATABLE READ` fica no meio (impede dirty e non-repeatable, permite phantom). Frase clássica de prova: "no `READ UNCOMMITTED`, uma transação pode ler dados gravados por outra transação **antes do COMMIT**" — verdadeiro; "no `SERIALIZABLE`, transações concorrentes são executadas **simultaneamente sem espera**" — falso, é exatamente o oposto: são serializadas.

---

## 6. Deadlocks — quando as transações se trancam

### 6.1 Conceito

Um **deadlock** (impasse) acontece quando duas ou mais transações ficam **esperando, cada uma, por um recurso que a outra detém** — e nenhuma consegue avançar, porque a liberação do recurso depende justamente de quem está esperando. É uma **espera circular**: T1 espera o recurso de T2; T2 espera o recurso de T1; ninguém desiste; nada anda.

> [!example] Deadlock clássico — duas contas, duas transações
> T1 precisa atualizar a **conta A** e depois a **conta B**. T2 precisa atualizar a **conta B** e depois a **conta A**. O cronograma:
>
> 1. T1 bloqueia a conta A (ex.: `UPDATE conta SET saldo = saldo - 50 WHERE cod_conta = 'A';`);
> 2. T2 bloqueia a conta B (`UPDATE ... WHERE cod_conta = 'B';`);
> 3. T1 pede a conta B — **mas B está com T2** → T1 espera;
> 4. T2 pede a conta A — **mas A está com T1** → T2 espera.
>
> Pronto: espera circular. Nenhuma das duas termina sozinha; o sistema precisa intervir.

O mecanismo que cria o impasse é o **lock (bloqueio)**: para atualizar um dado, a transação "tranca" o registro; enquanto uma tranca, outra espera. Sempre que dois recursos são atualizados em **ordens diferentes** por transações concorrentes, o deadlock é possível.

A banca às vezes cita as **quatro condições** necessárias para o deadlock (consulte a referência de sistemas operacionais, mas no contexto de banco): exclusão mútua (o recurso é usado por um de cada vez), posse e espera (a transação segura um recurso enquanto espera outro), não preempção (o recurso não é tirado à força) e **espera circular**. O mais útil em prova é reconhecer o **padrão de espera circular com bloqueios** na descrição do cenário.

### 6.2 Mecanismos de resolução

Como o SGBD resolve um deadlock? Três famílias de resposta:

**1. Timeout (tempo máximo de espera).** Cada transação tem um prazo para obter o recurso; se estourar, ela é desfeita (rollback) e pode tentar de novo. Simples, mas arbitrário: mata transações legítimas que apenas demoram.

**2. Detecção do deadlock e escolha de vítima.** O SGBD mantém um **grafo de espera** (quem espera quem) e procura **ciclos**. Ao encontrar, escolhe uma transação para ser **vítima** — desfaz (rollback) a vítima, liberando os recursos para as outras avançarem. O critério de escolha costuma ser o custo (a mais "barata" de desfazer, a mais antiga ou mais nova, a que menos caminhou). É a abordagem mais sofisticada e a mais citada em prova.

**3. Prevenção (evitar que o deadlock aconteça).** A técnica clássica é a **ordenação global dos recursos**: todas as transações acessam os recursos na **mesma ordem** — ex.: primeiro a conta de menor código, depois a de maior. Se T1 e T2 acessam A antes de B sempre, nunca haverá espera circular (quem pegar A primeiro também pegará B primeiro; o segundo espera na fila). Outras variantes teóricas: *wait-die* e *wound-wait* — quando uma transação mais nova pede recurso de uma mais velha, ela espera ou morre, respectivamente —, mas a ordenação é o exemplo que a FGV costuma cobrar.

> [!example] Resolução por ordenação — aplicada ao exemplo
> Regra: **atualizar sempre a conta de menor código primeiro**. T1 (que precisa de A=101 e B=202) e T2 (que precisa de B=202 e A=101) passam ambas a tocar **101 antes de 202**. Quem chegar primeiro bloqueia 101 e, em seguida, 202; a segunda espera na fila desde o primeiro lock — sem cruzar, sem ciclo, sem deadlock. A espera continua existindo (uma transação ainda espera a outra), mas ela **sempre termina**: deadlock, não.

> [!warning] PEGADINHA — deadlock ≠ starveção e ≠ wait
> **Deadlock** é espera **circular** (nenhuma avança). **Waiting** (espera) normal ocorre quando uma transação espera outra por um instante — mas a outra **progride** e libera o recurso; não há ciclo. **Starvation** é quando uma transação espera **indefinidamente** por falta de oportunidade (e não por ciclo) — ex.: o escalonador vive escolhendo outras. A banca mistura os três: o cenário "T1 espera T2, T2 espera T1" é **deadlock**; "uma transação nunca consegue obter o recurso porque outras sempre são priorizadas" é **starvation**.

A conexão com o [[Raciocinio-Matematico-Aplicado|RLM]] aqui é elegante: o deadlock é um **ciclo** no grafo de espera — o tipo de estrutura que você estudou em conjuntos e grafos. "Detectar deadlock" é **detectar ciclo**. Por isso a resolução por ordenação funciona: ela **impede a formação do ciclo** na estrutura, não apenas o detecta.

---

## 7. ACID, LGPD e auditoria — a ponte com a Fase 1

A [[LGPD-Lei-Geral-de-Protecao-de-Dados|LGPD]] não cita "ACID" — mas as garantias do ACID são a infraestrutura técnica de vários deveres legais:

- **Segurança** (art. 46): proteger dados pessoais de perda, alteração ou acesso não autorizado. A **durabilidade** (dados confirmados não se perdem) e a **atomicidade** (nada fica pela metade) são camadas dessa proteção.
- **Integridade e confidencialidade**: a **consistência** (regras de integridade referencial, `CHECK`) mantém os dados coerentes — inclusive dados sensíveis, como informações de saúde presentes em sistemas previdenciários.
- **Prestação de contas e auditoria**: o art. 37 exige registros das operações de tratamento. As **trilhas de auditoria** — Tabela de Ações de Tratamento, logs de acesso e de transação — dependem de um banco que **registre o que foi feito** (triggers de auditoria, vistas em [[SQL-DDL-e-DML]]) e que **preserve esses registros** (durabilidade).
- **Resposta a incidentes** (art. 48): para comunicar um incidente à ANPD com precisão, é preciso saber **o que aconteceu** — e os logs de transação, junto com os backups (função do SGBD vista em [[Fundamentos-e-Modelagem]]), são a fonte dessa informação.

> [!important] O raciocínio para a prova
> Questões que misturam banco e LGPD costumam usar palavras como "trilha de auditoria", "logs", "dados sensíveis", "confidencialidade". A resposta técnica quase sempre aponta para: **controle de acesso** (quem pode executar transações), **auditoria** (registrar as transações) e **durabilidade/backup** (preservar os registros). Propriedade ACID não é "privacidade" — mas é o que torna a privacidade auditável.

---

## 8. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **Transação** = unidade lógica de trabalho; `BEGIN` → comandos → `COMMIT` (confirma) ou `ROLLBACK` (desfaz)
> - [ ] **Atomicidade**: tudo ou nada — falha no meio desfaz a transação inteira (logs de undo/redo)
> - [ ] **Consistência**: de estado válido a estado válido — chaves, FKs ([[Fundamentos-e-Modelagem]]), `CHECK`; a regra precisa estar declarada no banco
> - [ ] **Isolamento**: transações concorrentes não interferem — mais isolamento, menos concorrência
> - [ ] **Durabilidade**: após `COMMIT`, nada se perde — gravação em log de redo
> - [ ] **Atomicidade desfaz o não confirmado; durabilidade preserva o confirmado**
> - [ ] **Anomalias**: dirty read (lê não confirmado) · non-repeatable read (relê e muda) · phantom read (conjunto muda por INSERT) · lost update (gravação sobrescreve a outra)
> - [ ] **Níveis**: `READ UNCOMMITTED` (permite tudo) → `READ COMMITTED` (impede dirty) → `REPEATABLE READ` (impede non-repeatable) → `SERIALIZABLE` (impede phantoms; tudo serializado)
> - [ ] **Deadlock** = espera circular com locks; resolve-se com **timeout**, **detecção + vítima** (grafo de espera, ciclo) ou **prevenção por ordenação de recursos**
> - [ ] **LGPD**: trilha de auditoria, logs de transação, integridade e segurança dos dados pessoais/sensíveis

> [!warning] O erro mais comum em prova
> Aplicar o ACID na ordem errada do raciocínio. Na hora da questão, siga o roteiro: (1) identificou "tudo ou nada" ou "falhou no meio" → **atomicidade**; (2) identificou "regra de negócio/chave violada" → **consistência**; (3) identificou "duas transações ao mesmo tempo" → **isolamento** (e pergunte *qual anomalia*); (4) identificou "caiu o servidor depois do COMMIT" → **durabilidade**. Essa sequência de quatro perguntas resolve a maioria das alternativas.

---

## 9. Próximos passos

Você fechou o núcleo relacional do Bloco 3.1: nas notas anteriores desenhou e normalizou o banco ([[Fundamentos-e-Modelagem]], [[Normalizacao]]), escreveu SQL ([[SQL-DDL-e-DML]]) e agora sabe como o SGBD garante confiabilidade sob concorrência com o ACID.

O próximo tópico da ementa é **NoSQL** — e a ponte é imediata: lá você verá a *eventual consistency* (consistência eventual), um conceito que **relaxa** o C e o I do ACID em troca de disponibilidade e escala. Você saberá comparar porque agora conhece o lado "forte" da balança. Em seguida, **Big Data** fecha o bloco com os desafios de volume, velocidade, variedade, veracidade e valor — onde as garantias transacionais do modelo relacional precisam ser repensadas em escala.

Mais adiante na ementa — na fase avançada, em **Arquitetura Avançada** — a conexão entre **ACID e transações distribuídas** será retomada: quando o banco não é um só, mas uma rede de servidores, a atomicidade ganha o nome de *transação distribuída* e exige protocolos próprios (você verá isso no momento certo). Por ora, o alvo imediato é comparar o modelo ACID com o que o NoSQL oferece — e você já está armado para essa comparação.