# Big Data

> [!info] Metadados
> **Disciplina:** Banco de Dados
> **Bloco:** 3.1 — Banco de Dados (FASE 3 — Infraestrutura de Dados)
> **Tópico:** 6. Big Data
> **Subtópicos:** Características: Volume, Velocidade, Variabilidade, Veracidade, Valor · Hadoop e MapReduce (conceito) · Apache Spark (conceito) · Data Lakes
> **Pré-requisitos:** [[NoSQL]] (modelos não relacionais e consistência eventual — base dos ecossistemas de larga escala), [[Transacoes-e-ACID]] (ACID e consistência — para contrapor com o modelo distribuído), [[Fundamentos-e-Modelagem]] (dado estruturado e modelo de dados), [[Raciocinio-Matematico-Aplicado|Raciocínio Lógico Matemático]] (conjuntos, estatística elementar, grafos) e [[LGPD-Lei-Geral-de-Protecao-de-Dados|Legislação/Segurança]] (grandes bases de dados pessoais, minimização, avaliação de risco)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-28

---

## 1. O que é Big Data?

Você acaba de fechar o estudo dos bancos de dados com o NoSQL — as ferramentas criadas para quando o relacional não escala. O Big Data é o passo seguinte da mesma história: o momento em que o **problema vira escala de outra natureza**. A nota pedagógica da ementa avisa: Big Data é **conceitual** neste edital — não vamos aprofundar implementação, mas entender o **ecossistema**: o que é, por que existe, quais as peças principais e como se relacionam.

**Big Data** é o termo para conjuntos de dados tão **grandes, rápidos e variados** que as ferramentas tradicionais de processamento (um SGBD relacional, uma planilha, um servidor único) não dão conta — exigindo **novas formas de armazenamento e processamento distribuído**. Não é um produto nem um software específico: é um **desafio** — e, para enfrentá-lo, surgiu um ecossistema inteiro de tecnologias.

O contexto ajuda a tornar isso concreto. A DATAPREV processa dados da seguridade social de dezenas de milhões de brasileiros: vínculos, contribuições, benefícios, atendimentos. São bases que crescem continuamente, chegam de fontes diferentes (órgãos públicos, empresas, sistemas internos), em formatos diversos, e precisam ser analisadas para pagamento correto, auditoria e combate a fraude. Esse é um cenário genuinamente Big Data.

> [!question] Pergunta orientadora
> Se bastasse "muita informação", um computador maior resolveria o problema, e Big Data nem teria nome próprio. O que faz dele um campo à parte? A resposta está nos **5 Vs** — e, em especial, num deles que nada tem a ver com tamanho.

> [!warning] PEGADINHA — Big Data não é só "grande quantidade"
> Se a afirmação diz "Big Data = dados em grande volume", falta metade da história. Volume é **um** dos Vs; o conceito inclui também velocidade, variedade, veracidade e valor. E não existe um número mágico de gigabytes que defina "Big": o limite é prático — **o ponto em que as ferramentas tradicionais param de funcionar**. O que é Big para uma farmácia de bairro não é para a DATAPREV.

---

## 2. Os 5 Vs

A forma mais conhecida de descrever Big Data é pela família dos **Vs**. Ela começou com os **3 Vs** do Gartner (2001) — **Volume, Velocidade e Variedade** — e depois ganhou **Veracidade** e **Valor**, formando os **5 Vs** mais citados na literatura: *Volume, Velocity, Variety, Veracity, Value*.

> [!note] Atenção à lista do edital
> A ementa da DATAPREV lista: **Volume, Velocidade, Variabilidade, Veracidade, Valor**. Repare na pequena variação: a família clássica usa **Variedade** no lugar de **Variabilidade**. As duas cobrem coisas diferentes — e a prova pode usar qualquer uma delas. Veja a seguir o significado de cada termo para acertar nas duas versões. (Algumas listas mais longas ainda acrescentam Visualização e outras variantes — o que importa é dominar os conceitos.)

### 2.1 Volume — a quantidade

**Volume** é o tamanho: bilhões de registros, terabytes e petabytes de dados. É o V mais óbvio — e o único que a maioria das pessoas lembra. Ele exige armazenamento distribuído: nenhum disco único comporta ou lê tudo em tempo útil. É o V que justifica tecnologias como o HDFS e os bancos NoSQL.

*Verbo-chave: "bilhões de registros", "petabytes", "dados demais para um servidor".*

### 2.2 Velocidade — a rapidez

**Velocidade** é a taxa com que os dados são **gerados** e precisam ser **processados**. Dados podem chegar em lotes (batch) ou em fluxo contínuo (streaming): leituras de sensores, transações online, posts em redes sociais, logs de sistemas. Quando a resposta precisa sair em **tempo real** (fraude detectada na hora da tentativa), a velocidade domina o problema.

*Verbo-chave: "tempo real", "streaming", "milhões de eventos por segundo".*

### 2.3 Variedade — e Variabilidade

**Variedade** é a **diversidade de formatos e fontes**: dados estruturados (tabelas), semiestruturados (JSON, XML), não estruturados (texto, áudio, vídeo, imagem) — vindos de sistemas internos, órgãos públicos, redes sociais, sensores. É o V que mais diferencia Big Data dos bancos tradicionais, que só lidavam bem com dados estruturados. Toda a seção 3 existe por causa dele.

**Variabilidade** é o termo do edital — e dois sentidos: (1) a **variação da velocidade** do fluxo ao longo do tempo (picos, sazonalidade, eventos que multiplicam o volume de repente — como a carga de declarações no fim do ano); (2) a **mudança de significado/contexto** dos dados (a mesma palavra pode significar coisas diferentes em contextos diferentes). Se a prova usar "variabilidade", pense em **flutuação e mudança**; se usar "variedade", pense em **diversidade de formatos**.

### 2.4 Veracidade — a confiabilidade

**Veracidade** é a **qualidade e confiabilidade** dos dados. Fontes diferentes trazem dados imprecisos, incompletos, duplicados ou ruidosos; redes sociais e dados gerados por usuários são cheios de inconsistência. Decisões baseadas em dados ruins são decisões ruins — por isso, no Big Data, "limpar" e validar não é etapa opcional. A veracidade conecta-se ao [[Raciocinio-Matematico-Aplicado|RLM]]: avaliar se uma afirmação sobre os dados tem fundamento é, no fundo, lógica de argumentação.

*Verbo-chave: "dados duvidosos", "ruído", "qualidade dos dados", "confiabilidade".*

### 2.5 Valor — o objetivo final

**Valor** é o retorno: transformar os dados em **insight, decisão, economia ou receita**. Dados sem análise são apenas custo (armazenar e processar gasta dinheiro). O valor é a justificativa de todos os outros Vs — é a resposta à pergunta "para que gastar tudo isso?". Na DATAPREV: detectar fraudes, melhorar o atendimento, pagar benefícios corretos.

| V | Pergunta que responde | Exemplo |
|---|---|---|
| Volume | *quanto?* | bilhões de registros de contribuições previdenciárias |
| Velocidade | *com que rapidez?* | leitura de sensores e transações em tempo real |
| Variedade / Variabilidade | *quais formatos? como varia?* | textos, JSON, vídeo; picos sazonais de carga |
| Veracidade | *é confiável?* | dados de cadastros com inconsistências e duplicidades |
| Valor | *gera benefício?* | detecção de fraude, pagamento correto de benefícios |

> [!tip] Palavras-chave dos Vs (para a prova)
> A FGV descreve um cenário e pergunta qual V está em jogo. Anote o gatilho de cada um: **volume** = tamanho · **velocidade** = rapidez/tempo real · **variedade** = formatos diferentes · **variabilidade** = flutuação/mudança · **veracidade** = qualidade/confiança · **valor** = benefício/insight. Pegadinha clássica: "os Vs formam uma lista fixa e universal" — **falso**; há versões com 3, 5, 7 Vs e a banca pode citar qualquer combinação, desde que os conceitos estejam certos.

---

## 3. Dado estruturado, semiestruturado e não estruturado

Para entender a **variedade**, é preciso classificar os dados pelo **grau de organização** que possuem — distinção clássica de prova:

- **Estruturado:** tem **schema (estrutura) pré-definido**, organizado em linhas e colunas — tabelas relacionais, planilhas, arquivos CSV com cabeçalho rígido. É o território que você estudou em [[Fundamentos-e-Modelagem]]: chaves, tipos, constraints.
- **Semiestruturado:** possui certa **marcação ou organização interna**, mas **sem schema rígido** — JSON, XML, e-mails (com campos fixos + corpo livre), logs com formato padrão. É o formato típico de [[NoSQL]] do tipo documento e das APIs web.
- **Não estruturado:** **não possui estrutura reconhecível** pelo computador sem técnicas especiais — texto livre, áudio, vídeo, imagens, mensagens.

| Tipo | Há schema? | Exemplos | Onde é processado |
|---|---|---|---|
| Estruturado | Sim, fixo | tabelas, planilhas, CSV rígido | SGBD relacional ([[SQL-DDL-e-DML]]) |
| Semiestruturado | Parcial (tags/marcações) | JSON, XML, e-mail | NoSQL document, APIs |
| Não estruturado | Não | texto, áudio, vídeo, imagem | Big Data, ML, análise de texto |

> [!warning] PEGADINHA — semiestruturado não é "sem estrutura"
> "Dado semiestruturado é aquele que não possui nenhuma estrutura" — **falso**: sem estrutura é o **não estruturado**. "JSON é dado não estruturado" — **falso**: JSON tem organização (chaves e valores, hierarquia) — é **semiestruturado**. A ordem de "estruturação" é: estruturado → semiestruturado → não estruturado, do mais rígido ao mais livre.

---

## 4. O ecossistema de processamento distribuído

Processar Big Data exige **dividir o trabalho entre muitos computadores** (um *cluster*), tolerar a falha de máquinas individuais e executar em paralelo. Dois nomes dominam o entendimento conceitual: **Hadoop** e **Spark**. Como a ementa pede conceito, vamos às ideias — sem mergulhar em detalhes de implementação.

### 4.1 Hadoop — o framework e seus dois pilares

**Hadoop** é um **framework de código aberto** para armazenamento e processamento distribuído de grandes volumes de dados em clusters de servidores comuns. Seus dois pilares clássicos:

- **HDFS** (*Hadoop Distributed File System*): o **sistema de arquivos distribuído**. Arquivos grandes são divididos em **blocos** e **replicados** em vários servidores; se um servidor cai, outro guarda a cópia — é assim que se obtém tolerância a falhas. Pense no HDFS como o "disco distribuído" do cluster.
- **MapReduce**: o **modelo de processamento** (próxima seção).

O trio se completa com o **YARN**, o gerenciador de recursos do cluster — pode aparecer citado em prova, mas o par HDFS + MapReduce é o coração do entendimento.

> [!warning] PEGADINHA — Hadoop não é banco de dados
> "Hadoop é um banco de dados distribuído" — **falso**: é um **ecossistema/framework** de armazenamento e processamento. "Hadoop = HDFS" — **falso**: o HDFS é um **componente** (o armazenamento); o Hadoop é o ecossistema inteiro. E o detalhe histórico que a banca explora: o **conceito** de MapReduce veio do Google (artigo de 2004); o Hadoop, open-source, foi criado no projeto Apache por Doug Cutting, inspirado nesses artigos do Google.

### 4.2 MapReduce — o modelo de duas fases

**MapReduce** é um **modelo de programação** para processar dados em paralelo, dividido em duas fases:

- **Map** (mapear): transforma **cada** dado de entrada em pares **(chave, valor)**. A fase roda **em paralelo**, dividida entre os nós do cluster — cada nó processa a sua fatia;
- **Reduce** (reduzir): **agrupa** os valores pela chave e os **combina** (soma, conta, agrega), produzindo o resultado final.

O exemplo clássico, a **contagem de palavras** (*word count*), torna isso claro. Entrada: `gato cão gato peixe gato`.

1. **Map:** cada palavra vira um par (palavra, 1) → `(gato,1) (cão,1) (gato,1) (peixe,1) (gato,1)`
2. **Agrupamento:** valores por chave → `gato → [1,1,1]`, `cão → [1]`, `peixe → [1]`
3. **Reduce:** soma dos valores → `gato → 3`, `cão → 1`, `peixe → 1`

A mágica está na **escala**: com bilhões de palavras, o Map roda espalhado por milhares de máquinas — cada uma processando sua parte — e o Reduce junta os parciais.

> [!warning] PEGADINHA — MapReduce é conceito, não ferramenta
> "MapReduce é uma ferramenta/aplicativo que se instala" — **falso**: é um **modelo/paradigma de programação**. O **Hadoop** é uma **implementação** desse modelo. "O Map e o Reduce são executados em sequência em uma única máquina" — **falso** (na prática, o Map roda **em paralelo** nos nós do cluster).

### 4.3 Apache Spark — o motor in-memory

**Spark** é um **motor de processamento** (*engine*) que também roda distribuído, mas com uma diferença-chave: mantém os dados **em memória** (in-memory) **entre as etapas do processamento**, em vez de gravar no disco a cada passo, como fazia o MapReduce clássico do Hadoop. O resultado: **muito mais rápido** para algoritmos **iterativos** (que repetem passos sobre os mesmos dados, como os de aprendizado de máquina) e para consultas interativas.

O Spark é **unificado**: com a mesma engine, faz processamento em lote (batch), processamento em tempo real (streaming), consultas estilo SQL e bibliotecas de aprendizado de máquina. É o exemplo mais citado da geração pós-MapReduce.

| Aspecto | Hadoop (MapReduce) | Spark |
|---|---|---|
| Armazenamento | **HDFS** (próprio) | usa HDFS, S3 e outros |
| Processamento | em **disco**, etapa a etapa | **em memória** (in-memory) |
| Velocidade | mais lento em algoritmos iterativos | mais rápido em algoritmos iterativos |
| Escopo | foco em lote (batch) | lote, streaming, SQL, aprendizado de máquina |

> [!warning] PEGADINHA — Spark não "substitui" o Hadoop completamente
> "O Spark substitui o Hadoop integralmente" — **falso**: o Spark é um **motor de processamento** e pode usar o **HDFS** do Hadoop como armazenamento — os dois **coexistem**. "O Spark é a implementação do MapReduce" — **falso**: o MapReduce é um modelo (implementado pelo Hadoop); o Spark é outro **motor**, que aplica ideias semelhantes com arquitetura própria (in-memory). A palavra-chave do Spark na prova é **memória**.

---

## 5. Data Lakes

### 5.1 O conceito de lago de dados

**Data Lake** é um **repositório central** que armazena dados **no seu formato original (bruto)**, em qualquer escala — estruturados, semiestruturados e não estruturados — **antes** de se saber exatamente como serão usados. É a estratégia "guarda tudo como veio, decide depois": a estrutura é definida no momento da **leitura** (*schema-on-read*), e não no momento da gravação, como faz o banco relacional (*schema-on-write*, que exige saber a estrutura antes de gravar — o que você viu em [[Fundamentos-e-Modelagem]]).

### 5.2 A distinção essencial: Data Lake × Data Warehouse

A banca cobra o contraste. Enquanto o **Data Warehouse** armazena dados **processados, limpos e modelados** para análise e relatórios (o "estoque organizado"), o **Data Lake** armazena dados **brutos, como foram recebidos** (o "reservatório"). O Data Warehouse pertence ao mundo do BI — e o aprofundamento dele (modelagem dimensional, ETL, OLAP) ficará para o bloco seguinte da trilha, de **BI/Data Warehouse**. Aqui, a ementa cobra apenas o Data Lake, com o conceito essencial:

| Data Lake | Data Warehouse |
|---|---|
| Dados **brutos**, formato original | Dados **processados e modelados** |
| Todos os tipos: estruturado, semiestruturado, não estruturado | Geralmente estruturado |
| Esquema definido na **leitura** | Esquema definido na **escrita** |
| Flexível: qualquer uso futuro | Otimizado para análise e relatórios |
| Risco: virar "pântano" (*data swamp*) sem governança | Mais organizado, porém menos flexível |

> [!note] Data Lake está no edital do Bloco 3.1
> Repare no detalhe: **Data Lake** é item **deste** tópico — por isso o contraste com o Data Warehouse precisa ficar claro aqui. O **Data Warehouse**, com ETL, OLAP e modelagem dimensional, será estudado a fundo no bloco de BI/Data Warehouse (próximo na trilha); aqui basta a distinção: **bruto e flexível** (lake) versus **processado e modelado** (warehouse).

> [!warning] PEGADINHA — Data Lake não é um software
> "Data Lake é a tecnologia Hadoop" — **falso**: o Data Lake é um **conceito de repositório**; o Hadoop (e outras plataformas) são **tecnologias usadas para construí-lo**. "O Data Lake garante dados confiáveis" — **falso**: sem **governança** (catálogo, controle de qualidade, segurança), o lago vira um **pântano de dados** (*data swamp*) — dados acumulados que ninguém sabe onde estão nem se podem ser usados. Governança não é luxo: é o que separa o lago do pântano — e é onde a LGPD entra.

---

## 6. Big Data, RLM, IA e LGPD — pontes com as Fases 1 e 2

### 6.1 RLM: o raciocínio por trás dos dados

Os Vs só geram **valor** com raciocínio quantitativo — a matéria que você treinou no [[Raciocinio-Matematico-Aplicado|RLM]]: porcentagens, médias, amostragem, conjuntos e grafos. Duas aplicações diretas: (1) interpretar análises de Big Data exige ler estatísticas com senso crítico — de onde vieram, qual a amostra, qual a margem de erro; (2) a **veracidade** dos dados é uma questão de **argumentação**: a afirmação "correlação = causa" é falácia, e desconfiar dela é lógica de argumentação aplicada a dados.

### 6.2 IA: dados alimentam modelos

Big Data e inteligência artificial andam juntos — e a ponte com a [[IA-e-Etica|Fase 2]] é natural: modelos de IA **aprendem com dados**. Se os dados são incompletos, tendenciosos ou sujos (pouca veracidade), o modelo herda esses defeitos — é a raiz do **viés algorítmico** que você estudou em IA e Ética. Veracidade, portanto, não é só uma preocupação técnica: é **pré-condição para uma IA justa e transparente**.

### 6.3 LGPD: grandes bases de dados pessoais

O cenário Big Data da DATAPREV é feito de **dados pessoais** — e muitos **sensíveis** (informações de saúde, por exemplo). A [[LGPD-Lei-Geral-de-Protecao-de-Dados|LGPD]] impõe limites a "guardar tudo e decidir depois":

- **Minimização** (princípio da necessidade): reter só o que for preciso para a finalidade — um Data Lake sem critério de retenção viola isso;
- **Finalidade**: o dado bruto só pode ser usado para fins compatíveis com os informados ao titular;
- **Relatório de Impacto (RIPD)**: tratamentos em **larga escala** de dados pessoais podem exigir avaliação de riscos documentada — o retrato exato de um projeto Big Data;
- **Segurança** (art. 46): criptografia, controle de acesso e trilhas valem em todo o ecossistema — inclusive nos lagos de dados.

> [!important] O raciocínio para a prova
> Questão que mistura Big Data e LGPD quase sempre aponta para: **minimização** (não reter tudo), **avaliação de risco** (RIPD para larga escala), **anonimização** quando possível e **governança** (catálogo, retenção, segurança). O fato de o dado ser "big" não o dispensa da lei — pelo contrário.

---

## 7. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **Big Data** = dados que as ferramentas tradicionais não processam; não é só "muito volume" nem um software
> - [ ] **5 Vs do edital:** Volume (tamanho) · Velocidade (rapidez/tempo real) · **Variabilidade** (= flutuação/mudança; a família clássica diz **Variedade** = formatos diversos) · Veracidade (qualidade/confiança) · Valor (benefício/insight)
> - [ ] **Dados:** estruturado (schema fixo) · semiestruturado (JSON/XML) · não estruturado (texto, áudio, vídeo)
> - [ ] **Hadoop = ecossistema** distribuído: **HDFS** (armazenamento em blocos replicados) + **MapReduce** (processamento) + YARN (gerenciamento de recursos)
> - [ ] **MapReduce = modelo** de programação: **Map** (gera pares chave-valor em paralelo) → **Reduce** (agrupa e agrega)
> - [ ] **Spark = motor** de processamento **in-memory**; mais rápido para algoritmos iterativos; coexiste com o Hadoop (pode usar o HDFS)
> - [ ] **Data Lake = repositório de dados brutos**, schema-on-read; contraste com **Data Warehouse** (processado/modelado) — item do edital deste bloco
> - [ ] **Governança** separa o Data Lake do "pântano de dados"; **LGPD** exige minimização, RIPD e segurança em larga escala

> [!warning] O erro mais comum em prova
> Trocar conceito por implementação. Roteiro rápido: (1) "modelo de duas fases map/reduce" → **MapReduce é o conceito**; (2) "ecossistema com HDFS" → **Hadoop**; (3) "processa em memória, mais rápido" → **Spark**; (4) "guardar bruto, esquema na leitura" → **Data Lake**; (5) "dado sem estrutura nenhuma" → **não estruturado** (semiestruturado ainda tem organização); (6) "só tamanho define Big Data" → **falso**, são os Vs.

---

## 8. Próximos passos

Com esta nota, você fecha o **Bloco 3.1 — Banco de Dados** do seu plano de estudos. O percurso foi completo: modelagem e normalização ([[Fundamentos-e-Modelagem]], [[Normalizacao]]), SQL ([[SQL-DDL-e-DML]]), transações e ACID ([[Transacoes-e-ACID]]), NoSQL ([[NoSQL]]) e, agora, o ecossistema Big Data. Você saiu do banco de uma planilha imaginária até os lagos de dados — e sabe *por que* cada tecnologia existe.

A trilha da **Fase 3** aponta para o bloco de **BI e Data Warehouse** (ETL, OLAP e modelagem dimensional — o aprofundamento do Data Warehouse que aqui ficou apenas anunciado) e, na sequência didática, para a **Fase 4 — Desenvolvimento de Sistemas**: Java, Spring e JPA, que usarão, na prática, o banco relacional que você aprendeu a modelar. Mais adiante, na **Arquitetura Avançada**, o NoSQL e o CAP voltam ao palco com transações distribuídas em microsserviços.

Por ora, respire: o núcleo de dados do edital está completo. Um bom momento para revisar o bloco inteiro antes de seguir para o desenvolvimento de software.