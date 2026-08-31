# Gramática Inglesa Aplicada

> [!info] Metadados
> **Disciplina:** Língua Inglesa
> **Bloco:** 2.1 — Língua Inglesa (FASE 2 — Linguagens e Acesso)
> **Tópico:** 2. Gramática inglesa aplicada
> **Subtópicos:** Tempos verbais · Condicionais · Voz passiva · Reported Speech · Modais · Conectivos acadêmicos e técnicos
> **Pré-requisitos:** Língua Portuguesa (estrutura morfossintática, classes de palavras) + Tópico 1 — Compreensão de textos em inglês
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-28

---

## 1. Gramática a serviço do sentido

A ementa é explícita: *"itens gramaticais relevantes para o entendimento dos sentidos dos textos"*. Essa frase é o seu mapa. Você não vai memorizar regras de gramática inglesa como quem decora uma lista telefônica. Você vai aprender aquelas estruturas que, quando aparecem num texto técnico, **mudam o que o texto diz**.

Pense na diferença entre as frases:

- *"The system **worked**."*
- *"The system **has worked**."*
- *"The system **is working**."*
- *"The system **was working**."*
- *"The system **had worked**."*

Todas falam de algo relacionado a "trabalhar", mas cada uma conta uma história diferente sobre **quando** a ação acontece e **como ela se relaciona com o momento presente**. É esse "quando e como" que a FGV testa — não porque quer gramáticos, mas porque o tempo verbal carrega sentido.

> [!important] A pergunta que define a nota
> Por que duas frases com as mesmas palavras — *"He **has lived** in São Paulo"* e *"He **lived** in São Paulo"* — significam coisas diferentes? Porque o tempo verbal **não é decoração**: ele é a máquina que marca *se* a ação terminou, *se* continua, *se* afeta o presente. Quem não entende essa máquina lê errado. Esta nota é sobre destravar essa máquina para ler e interpretar.

A boa notícia: você já estudou, na Fase 1, como os tempos verbais afetam a coerência narrativa em português — em [[Estrutura-Morfossintatica|Estrutura Morfossintática]] e [[Coesao-Textual|Coesão Textual]]. O raciocínio do "aspecto verbal" é o mesmo; o que muda é a forma. Vamos aproveitar essa base.

---

## 2. Os tempos verbais que mudam o sentido

### 2.1 Simple Present — o presente "verdade geral"

O *simple present* descreve **fatos, verdades gerais, hábitos e estados permanentes**: *"The application **runs** on a Java Virtual Machine."* (a aplicação roda — fato, não ação em andamento agora).

A pegadinha típica é confundi-lo com o *present continuous*. Repare:

- *"The server **processes** requests."* → afirmação permanente: o servidor (por função) processa requisições.
- *"The server **is processing** the requests."* → ação em andamento **agora**: o servidor está processando, neste momento.

> [!warning] Simple Present × Present Continuous
> O *simple present* fala de hábito/verdade geral ("o sistema faz isso"); o *present continuous* (verbo *to be* + verbo-ing) fala de ação em andamento ("está fazendo agora"). Em textos técnicos, o contínuo costuma indicar um **processo temporário ou em execução no momento**. Confundir os dois equivale a confundir "o sistema roda" com "o sistema está rodando" — sentidos bem diferentes.

Forma do contínuo: *subject + am/is/are + verb-ing*. Atenção ao verbo *to be*: ele é o auxiliar do contínuo — uma pista visual importante em prova.

### 2.2 Simple Past × Present Perfect — a fronteira que mais derruba

Este é um dos pares mais cobrados, porque **não existe correspondência perfeita no português** — nós usamos "pretérito perfeito" para ambos.

- **Simple Past** (*worked*): ação **terminada em um tempo definido no passado**. Costuma vir com marcadores: *yesterday, last week, in 2019, when*. *"The team **fixed** the bug yesterday."* (corrigiu ontem — tempo definido.)
- **Present Perfect** (*has/have + particípio*): ação do passado **com relevância ou conexão com o presente** — geralmente: acabou de acontecer (*just*), aconteceu num tempo indeterminado (*ever, never*), ou ainda **continua até agora** (*for, since*). *"The team **has fixed** the bug."* (corrigiu — e isso importa agora; resultado presente.)

> [!example] O contraste de sentido
> - *"I **tested** the module."* → testei (em algum momento passado específico; a ação pertence ao passado).
> - *"I **have tested** the module."* → testei (e o resultado disso é relevante agora — por exemplo, posso afirmar que ele funciona).
>
> Em prova, quando a banca quer que a **conexão com o presente** fique clara, usa *present perfect*; quando quer simplesmente *"o que aconteceu antes"*, usa *simple past*. Marcadores resolvem: *yesterday/last/ago* → past; *since/for/just/already/ever/never* → perfect.

### 2.3 Past × Past Continuous — ação concluída × ação em andamento

- **Simple Past:** ação concluída. *"The service **stopped** processing."*
- **Past Continuous** (*was/were + verb-ing*): ação que **estava em andamento** num momento do passado, geralmente interrompida ou pano de fundo. *"The service **was processing** data when the server crashed."* (estava processando quando o servidor caiu.)

A pegadinha clássica: a **interrupção**. A "ação que interrompe" costuma estar num simple past; a "ação que estava acontecendo" (e foi interrompida) fica no past continuous. *"She **was writing** the report **when** the system **failed**."* — *was writing* (em andamento) + *failed* (interrupção pontual).

### 2.4 Past Perfect — o "passado do passado"

O *past perfect* (*had + particípio*) marca uma ação que aconteceu **antes de outra ação passada**. É "o mais antigo dos passados".

- *"The system **had stored** the data **before** the failure occurred."* → os dados já haviam sido armazenados **antes** de a falha ocorrer.

Sem *past perfect*, a ordem temporal fica ambígua. Com ele, a frase garante: "X já tinha acontecido quando Y aconteceu". Em texto técnico, essa ordem é crucial para entender cronologia de eventos (logs, auditoria, sequência de operações).

### 2.5 Future: will × going to

Ambos expressam futuro, mas com **matizes de sentido** que a prova pode explorar:

- ***Will*:** decisão **no momento da fala**, previsão/opinião, promessa, ou futuro "neutro". *"The system **will** handle it."* (vai lidar com isso — afirmação futura.)
- ***Going to*:** intenção **planejada** ou futuro baseado em **evidência presente**. *"We **are going to** migrate the servers next month."* (nós **planejamos** migrar — há um plano.)

> [!example] Nuance de sentido
> - *"I **will** call you."* → decidido agora, no momento da fala.
> - *"I **am going to** call you."* → já era intenção planejada, havia um plano prévio.
>
> Em interpretação, o *going to* sugere **planejamento/decisão anterior**, enquanto o *will* sugere **decisão espontânea ou previsão**. A diferença é sutil, mas é exatamente o tipo de nuance que distingue a alternativa certa da errada.

---

## 3. Condicionais: os cinco mundos do "se"

As condicionais expressam relações entre uma condição e seu resultado. O **tempo verbal** dentro da *if-clause* e da *main clause* revela **quão provável ou possível** é o cenário. Esse é o coração da cobrança: **o tempo constrói o sentido de probabilidade**.

Na prática, lembre-se do valor central de cada tipo:

- **Zero conditional** (if + simple present, simple present): **verdade geral/fato científico**. *"If you save the file, the data **is** preserved."* (sempre que você salva, os dados são preservados — lei geral.)
- **First conditional** (if + simple present, will + base): **condição real e possível no futuro**. *"If the network **fails**, the app **will** retry."* (se a rede falhar — possível de fato acontecer —, o app vai tentar de novo.)
- **Second conditional** (if + simple past, would + base): **condição irreal/improvável ou hipotética, presente/futuro**. *"If I **knew** the password, I **would** log in."* (se eu soubesse — mas não sei —, logaria.)
- **Third conditional** (if + past perfect, would have + particípio): **condição irreal no passado** — impossível de mudar. *"If we **had backed up** the data, we **would have avoided** the loss."* (se tivéssemos feito backup — não fizemos —, teríamos evitado a perda.)
- **Mista (Mixed)**: combina passado e presente, quando a condição é do passado mas a consequência é do presente. *"If we **had hired** more staff, we **would not be** overloaded now."* (se tivéssemos contratado [passado/irreal], não estaríamos sobrecarregados agora [presente].)

> [!warning] Condicionais e o efeito de sentido
> Cada "mundo" da condicional comunica um **grau de certeza**. A FGV adora trocar o tempo para mudar o sentido: dizer "If the server fails, the app **would** retry" *(would* no lugar de *will*) transforma um fato provável num cenário hipotético. Repare sempre: **presente → provável; passado simples → irreal/improvável; past perfect → impossível/no passado**. O tempo é o sinal de certeza dentro da condicional.

---

## 4. Voz passiva: onipresente no texto técnico

Você estudou a transformação de voz em português na [[Reescrita-de-Frases-e-Paragrafos|reescrita de frases]]. Em inglês, o princípio é idêntico: na **voz ativa**, o sujeito pratica a ação (*"The team **deploys** the release"*); na **passiva**, o foco está no **receptor** da ação (*"The release **is deployed** by the team"*).

Estrutura: **to be + particípio passado**, mantendo o tempo do verbo *to be* igual ao tempo da ativa:

- *"The system **processes** data."* (ativa, simple present) → *"Data **is processed** by the system."* (passiva)
- *"The company **released** the update."* (simple past) → *"The update **was released** by the company."* (passiva)
- *"The team **will support** the tool."* → *"The tool **will be supported** by the team."* (passiva futura)

Por que a passiva é tão comum em textos técnicos? Porque o agente muitas vezes **é irrelevante ou desconhecido** — o que importa é a ação e seu resultado: *"The error **was logged**."* (o erro foi registrado) — quem registrou não interessa. Esse uso é típico de manuais, relatórios de incidentes e documentação.

> [!important] O que muda na interpretação
> A passiva **desloca o foco**: o sujeito gramatical vira o **receptor** da ação. Se o texto diz *"The backup **was corrupted**"*, a mensagem é que o backup foi corrompido — não quem corrompeu. Uma alternativa que diga *"The hacker corrupted the backup"* inseriria um agente e uma ação que o texto não afirma. Reconstruir **quem fez o quê** (ou se o agente é omitido) é a habilidade que cai na prova.

---

## 5. Reported Speech: o "discurso indireto" e o backshift

**Reported speech** (ou *indirect speech*) é quando relatamos o que alguém disse, sem aspas. Em português: "ele disse que **ia** viajar" (reportando "vou viajar"). Em inglês, o fenômeno central é o **backshift** — o "recuo" do tempo verbal no relato.

Quando o verbo de relato está no passado (*said, told, asked*), os tempos normalmente "recuam um degrau":

| Discurso direto (o que foi dito) | Discurso indireto (o relato) |
|---|---|
| "I **am** working" | He said he **was** working |
| "I **work**" | He said he **worked** |
| "I **worked**" | He said he **had worked** |
| "I **have worked**" | He said he **had worked** |
| "I **will** work" | He said he **would** work |
| "I **can** help" | He said he **could** help |
| "I **may** go" | He said he **might** go |

O padrão do backshift é o "degrau para trás": *am/are → was/were; is → was; will → would; can → could; may → might; present → past; past → past perfect.*

> [!example] Por que isso muda o sentido
> *"The engineer said: 'The system **will** be ready.'"* → relato: *"The engineer said the system **would** be ready."*
> O *would* é apenas o "will do passado" no relato — **não** significa condicional nem "cortesia". Essa é a pegadinha: ver o *would* num relato e achar que há hipótese, quando na verdade é só o backshift do *will*.

Além dos tempos, há **deslocamentos de palavras que apontam para o aqui/agora**: *here → there; now → then; today → that day; tomorrow → the next day; yesterday → the day before; this → that; these → those.*

**Perguntas no reported speech** mudam a ordem e acrescentam *if/whether* (para perguntas sim/não) ou mantêm a *wh-* word (what, when, why...) sem inverter o sujeito:

- *"Are you ready?"* → *He asked **if** I **was** ready.*
- *"Where is the server?"* → *He asked **where the server was**.* (ordem direta: sujeito antes do verbo — sem "was the server").

> [!warning] Pegadinha do backshift
> A FGV pode apresentar um relato **sem** aplicar o backshift (ex.: "He said he **will** go" quando deveria ser "**would** go") e pedir para identificar o erro, ou então apresentar o backshift correto como resposta. Decore o "degrau para trás" — é a mecânica da questão.

---

## 6. Modais: o tom das possibilidades, obrigações e deduções

Os modais são pequenas palavras que **modificam o sentido do verbo** — expressam possibilidade, capacidade, obrigação, permissão, conselho, dedução. Em interpretação, o modal é a chave do **grau de certeza** do autor. Vamos percorrer os principais com foco no sentido.

| Modal | Sentido principal | Exemplo técnico |
|---|---|---|
| *can* | capacidade / possibilidade | "The tool **can** parse large files." (consegue/pode) |
| *could* | capacidade no passado / possibilidade / forma educada | "It **could** have been cached." (podia ter sido / talvez) |
| *may* | permissão / possibilidade (incerta) | "The request **may** be rejected." (pode ser — talvez) |
| *might* | possibilidade ainda mais remota/incerta | "It **might** fail." (talvez/pode ser que) |
| *must* | obrigação (forte) **ou dedução** | "You **must** configure the proxy." (deve/obrigação) |
| *should* | conselho / recomendação / dever moderado | "We **should** review the logs." (deveríamos) |
| *will* | futuro / determinação | "It **will** retry." (vai) |
| *would* | futuro no passado / condicional / cortesia | "It **would** work if..." (funcionaria) |

O modal tem uma peculiaridade gramatical: é **seguido do verbo na forma base**, sem *to* (ex.: *must go*, não *must to go*; *can help*, não *can to help*). E não recebe *-s* na terceira pessoa (*he can run*, não *he cans run*).

> [!important] As duas pegadinhas mais graves dos modais
>
> **1) *must have + particípio* = dedução sobre o passado, NÃO obrigação.** *"The data **must have been deleted** by an automated job"* não significa que "os dados devem ser apagados" (obrigação), mas que "os dados **devem ter sido apagados**" (dedução: é muito provável que tenham sido). A FGV adora trocar dedução por obrigação — o sentido se distorce.
>
> **2) *can* × *may* — certeza diferente.** *"The update **can** break compatibility"* (pode quebrar — capacidade/permissão) vs. *"The update **may** break compatibility"* (pode quebrar — incerteza/possibilidade). Em interpretação, *can* tende a pendurar-se em "capacidade/dar para", *may/might* em "possibilidade/talvez". Confundi-los equivale a confundir "consegue" com "talvez".

> [!warning] Pegadinha *should have + particípio* × *must have + particípio*
> *"We **should have backed up** the data"* = "nós **deveríamos ter feito** backup" — reprovação sobre o passado (não fizemos, mas deveríamos). Já *"the file **must have been** corrupted"* = "o arquivo **deve ter sido corrompido**" — dedução sobre o passado. Dois usos "de passado" mas com naturezas muito diferentes: um é reprovação, o outro é conclusão.

**Modais na voz passiva** também aparecem muito em texto técnico: *"The payment **can be processed**"* (o pagamento pode ser processado), *"The service **must be restarted**"* (o serviço deve ser reiniciado). É a combinação modal + to be + particípio passado — e ela une os dois tópicos desta nota.

---

## 7. Conectivos acadêmicos e técnicos: o esqueleto do argumento

Você já viu parte disso na nota de [[Compreensao-de-Textos-em-Ingles|compreensão]]. Agora, no âmbito da gramática aplicada, vamos olhar o **efeito de sentido** de cada grupo — porque a FGV os testa perguntando qual conectivo **preserva a relação original** quando o enunciado pede para reescrever, ou qual valor lógico um conectivo expressa.

| Conectivo | Valor | Exemplo de uso no texto técnico |
|---|---|---|
| *however* | contraste (entre parágrafos/orações) | "The cloud scales well. **However**, costs can rise." |
| *nevertheless* / *nonetheless* | contraste que **mantém** a ideia anterior | "It is complex; **nevertheless**, it is worth it." |
| *although* / *even though* | concessão (dentro da mesma oração complexa) | "**Although** it is fast, it is complex." |
| *whereas* | contraste formal entre dois | "Python is interpreted, **whereas** Java is compiled." |
| *therefore* / *thus* / *hence* | conclusão | "The data is corrupt; **therefore**, we must restore it." |
| *consequently* / *as a result* | consequência | "The server crashed; **consequently**, users lost access." |
| *furthermore* / *moreover* / *in addition* | adição | "It is fast. **Furthermore**, it is secure." |
| *for instance* / *for example* | exemplificação | "Use caching; **for instance**, use Redis." |
| *in order to* | finalidade | "Compile **in order to** run the tests." |
| *due to* | causa (seguido de nome) | "The delay was **due to** a network issue." |
| *because* / *since* | causa (seguido de oração) | "It failed **because** the disk was full." |

> [!warning] *although* × *but* e a inversão da oração
> *Although* organiza a oração **concedida primeiro** e a oração principal depois: *"Although X, Y"* — e a ideia forte é Y. Já *but* conecta duas orações sem "rebaixar" nenhuma a concessão: *"X, but Y"*. Trocar um pelo outro **muda a hierarquia das ideias**. Se a FGV perguntar "qual conectivo preserva o sentido", confira qual das duas ideias o autor **queria destacar**.

> [!example] Causa e consequência na prática
> *"The application was slow **because** the database lacked indexes. **Consequently**, queries timed out."*
> *Because + oração* explica a **causa** (sem índices); *consequently* anuncia a **consequência** (consultas estouraram o tempo). A FGV pergunta isso de dois jeitos: ou "que relação expressa *consequently*?" (consequência), ou "reescreva mantendo a relação" — e aí *therefore*/"as a result" são equivalentes a *consequently*, enquanto *however* quebraria tudo.

---

## 8. Como a FGV cobra isto na prática (raciocínio passo a passo)

Diante de uma questão de gramática aplicada, siga uma rotina mental de eliminação:

1. **Identifique a estrutura testada.** O enunciado fala em passiva? reported speech? modal? tempo? condicional? conectivo? Essa primeira classificação restringe metade das alternativas.
2. **Traduza o sentido, não as palavras.** Pergunte: o que esta estrutura **comunica** sobre tempo, certeza, ordem ou foco?
3. **Teste cada alternativa preservando o sentido original.** A alternativa certa mantém tempo, modalidade e hierarquia das ideias — não os altera.
4. **Desconfie de "traduções" automáticas.** *Would* que é só backshift, *must have done* que é dedução, *can* que é capacidade: esses são os campeões de pegadinha.

> [!example] Um caso completo
> *"A manager said: 'We **will move** the database to the cloud.' — Which of the following correctly reports the statement?"*
>
> O verbo de relato *said* está no passado → backshift obrigatório: *will → would*. O relato correto: *"The manager said we **would move** the database to the cloud."* Alternativas que mantenham *will* ignoram o backshift; alternativas que usem *must* ou *may* mudam a modalidade. A única resposta que preserva tudo: o *would* como "will do passado".

---

## 9. Próximos passos

Você agora tem as ferramentas para **ler e interpretar** textos técnicos em inglês: compreensão estratégica (Tópico 1) e gramática aplicada ao sentido (Tópico 2). Com elas, a disciplina de Língua Inglesa do Bloco 2.1 está coberta. Na Fase 2, o próximo bloco é **Atualidades e Inteligência Artificial**, que usa a mesma habilidade de leitura crítica — agora aplicada a textos de atualidade e a conceitos de IA — e se conecta com o Raciocínio Lógico e a Legislação que você já estudou. Antes de partir, revise os itens a seguir e refaça os exemplos de memória: é assim que a gramática deixa de ser regra e vira reflexo de leitura.

---

## Palavras-chave que a banca cobra

- Tempos: *simple present, present continuous, simple past, past continuous, present perfect, past perfect, will, going to*
- Marcadores de tempo: *yesterday, last, ago, since, for, just, already, ever, never, when, before*
- Condicionais: *zero, first, second, third, mixed* e os verbos *if + would*
- Voz passiva: *be + past participle*, e o foco no receptor da ação
- Reported speech e **backshift**: *said/told/asked + recuo do tempo; if/whether;* *wh-* *questions (what, when, why, where)*
- Modais: *can, could, may, might, must, should, will, would* e *must have/could have/should have + particípio*
- Conectivos: *however, furthermore, consequently, in contrast, therefore, moreover, nevertheless, in addition, as a result, for instance, although, whereas, in order to, due to, based on*

## Pegadinhas mais comuns

> [!warning] Pegadinha 1 — Simple Past × Present Perfect
> *"I tested"* (ação pontual no passado) × *"I have tested"* (com resultado que importa no presente). Marcadores resolvem: *yesterday/last/ago* → past; *since/for/just* → perfect. A FGV troca um pelo outro para mudar a conexão com o presente.

> [!warning] Pegadinha 2 — Past × Past Continuous
> "Ação que estava em andamento" (contínuo) × "ação pontual/interrupção" (simple past). *"She was writing when the system failed"* — confundir os dois apaga a ideia de "em andamento interrompido".

> [!warning] Pegadinha 3 — *must have done* não é obrigação, é dedução
> *"The file must have been deleted"* = "**deve ter sido** apagado" (conclusão provável), e não "deve ser apagado" (obrigação). *Should have done* é reprovação; *must have done* é dedução.

> [!warning] Pegadinha 4 — *can* × *may*
> *can* pendura-se em "capacidade/dar para"; *may/might* em "possibilidade/talvez". Trocar um pelo outro muda o grau de certeza e o sentido da frase.

> [!warning] Pegadinha 5 — *would* que é só backshift
> Num relato com *said*, o *would* é o *will* do passado — não é condicional nem cortesia. Interpretar *would* como hipótese num reported speech leva à alternativa errada.

> [!warning] Pegadinha 6 — *although* × *but* e a hierarquia das ideias
> *Although* introduz a concessão e destaca a ideia seguinte; *but* apenas contrasta. Substituir um pelo outro reordena qual ideia o autor quer destacar.

> [!warning] Pegadinha 7 — conectivo com valor trocado
> *However* (contraste) por *therefore* (conclusão); *because* (causa) por *so* (consequência). Cada conectivo tem valor exato; a FGV mistura-os porque parecem "da mesma família".
