# Paradigma Orientado a Objetos — Índice

> [!info] Metadados
> **Disciplina:** Desenvolvimento de Sistemas
> **Bloco:** 4.1 — Desenvolvimento de Sistemas (FASE 4 — Núcleo de Desenvolvimento)
> **Tópico:** 2. Paradigma Orientado a Objetos
> **Subtópicos:** Conceitos (classe, objeto, herança, polimorfismo, encapsulamento, abstração) · SOLID (princípios básicos) · Clean Code (nomes significativos, funções pequenas, comentários úteis) · Análise estática de código e SonarQube
> **Pré-requisitos:** [[Java-Fundamentos-da-Linguagem|Java — Fundamentos da Linguagem]] (sintaxe da linguagem) e [[Raciocinio-Matematico-Aplicado|Raciocínio Lógico Matemático]] (lógica de programação, condicionais, estruturas de dados) e [[Fundamentos-e-Modelagem|Banco de Dados]] (modelagem de entidades e relacionamentos)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-09-17

Este é o **índice** do Tópico 2 — Paradigma Orientado a Objetos, o coração da Fase 4. A DATAPREV processa dados da seguridade social — o **CNIS**, o INSS digital, os sistemas de benefícios, a consignação — e cada "coisa" desse mundo real (cidadão, vínculo, contribuição, benefício) vira um **objeto** no software. É por isso que o edital trata o POO como o modelo mental sobre o qual quase todo sistema moderno é construído — inclusive praticamente tudo o que a DATAPREV desenvolve.

Você chega aqui já dominando as bases. Do **tópico 1 ([[Java-Fundamentos-da-Linguagem|Java — Fundamentos da Linguagem]])** vem a sintaxe: a classe como recipiente do código, o `new`, o construtor e o `this` que você viu nas coleções e nos exemplos. Do [[Raciocinio-Matematico-Aplicado|Raciocínio Lógico Matemático]] vem a lógica de programação: condicionais, repetições, estruturas de dados. Do [[Fundamentos-e-Modelagem|Banco de Dados]] vem a modelagem: entidades, atributos e relacionamentos. O POO costura esses três fios: o que era *sintaxe* vira *design*, e a *entidade* do banco vira *classe* no código.

Um aviso importante: por ser um conteúdo denso — conceitos, princípios e ferramentas — o tópico foi organizado em **cinco notas** dentro desta subpasta, seguindo a ordem pedagógica **do básico ao avançado**: primeiro o par fundamental (classe e objeto), depois os quatro pilares, então os princípios de escrita (Clean Code), a ferramenta que fiscaliza essa escrita (análise estática e SonarQube) e, por fim, os cinco princípios de design que amarram tudo (SOLID).

> [!question] Pergunta orientadora
> Depois de décadas de programação procedural (que segue uma lista de instruções), por que a indústria migrou para um modelo que "embrulha" dados e comportamentos juntos? E por que um órgão como o INSS — com milhões de beneficiários e regras complexas como a margem consignável — precisa de código que seja fácil de estender, testar e manter? As cinco notas deste tópico respondem a isso, começando pelo molde e a peça: classe e objeto.

## Sequência das notas

Navegue na ordem abaixo. Cada nota parte do que a anterior ensinou e termina apontando o que a próxima retoma.

| # | Nota | Conteúdo principal (subtópicos da ementa) |
|---|------|-------------------------------------------|
| 1 | [[Classe-e-Objeto]] | Objeto (estado, comportamento, identidade) · Classe (molde) · Instância (`new`, construtor) · Ponte com o banco de dados (tabela ↔ classe, linha ↔ objeto, coluna ↔ atributo) |
| 2 | [[Quatro-Pilares-do-POO]] | Abstração · Encapsulamento · Herança (é-um) vs composição (tem-um) · Classe abstrata (molde incompleto, método abstrato) · Polimorfismo (sobrescrita/sobrecarga) · Interface (contrato, implements) · Interface vs. classe abstrata (tabela comparativa) · Visibilidade dos membros (private, padrão, protected, public) |
| 3 | [[Clean-Code]] | Nomes significativos · Funções pequenas · Comentários úteis (o "porquê", não o óbvio) |
| 4 | [[Analise-Estatica-e-SonarQube]] | Análise estática vs dinâmica · Code smells · SonarQube · Quality Gate |
| 5 | [[Principios-SOLID]] | S (responsabilidade única) · O (aberto/fechado) · L (substituição de Liskov) · I (segregação de interfaces) · D (inversão de dependência) |

> [!tip] Roteiro de estudo sugerido
> Estude as notas **em ordem** (1 → 5). A cada nota, resolva os exemplos e as pegadinhas ao final antes de avançar. As notas 2 (pilares) e 5 (SOLID) concentram as pegadinhas mais frequentes da FGV — a distinção abstração/encapsulamento, herança/composição, sobrescrita/sobrecarga, a troca das características entre interface e classe abstrata e a troca das definições entre as letras do SOLID. A visibilidade (nota 2) também é clássica: `private` não é herdado e `protected` é visível no pacote.

## Mapa da unidade no bloco

```text
Tópicos anteriores (bases)
  RLM (lógica)  →  Banco de Dados (modelagem)  →  Java (sintaxe)
                           ↓
TÓPICO 2 — PARADIGMA ORIENTADO A OBJETOS (este índice)
   1. Classe e Objeto
      ↓
   2. Quatro Pilares do POO
      ↓
   3. Clean Code
      ↓
   4. Análise Estática e SonarQube
      ↓
   5. Princípios SOLID
      ↓
Próximo tópico
   3. Java Corporativo (JPA/Hibernate — o POO encontra o banco)
```

## Antes de estudar — palavras-chave do tópico

As **palavras-chave** que você deve reconhecer nas questões deste tópico são:

- **Conceitos (nota 1):** classe, objeto, instância, molde, estado, comportamento, identidade, `new`, construtor, `this`.
- **Pilares e mecanismos (nota 2):** abstração, encapsulamento, herança, composição, polimorfismo, sobrescrita (override), sobrecarga (overload), visibilidade, private, protected, public, classe abstrata, método abstrato, `abstract`, interface, contrato, `implements`, `extends`, default method.
- **Clean Code e análise estática:** Clean Code, nomes significativos, funções pequenas, comentários úteis, análise estática, análise dinâmica, SonarQube, code smell, quality gate.
- **SOLID:** responsabilidade única, aberto/fechado, substituição de Liskov, segregação de interfaces, inversão de dependência.

> [!warning] Cuidado com as pegadinhas recorrentes
> A banca adora inverter conceitos próximos em uma mesma alternativa. As mais frequentes: **abstração** (simplificar o modelo) vs **encapsulamento** (proteger/esconder dados); **herança** ("é-um") vs **composição** ("tem-um" — e o conselho moderno é *prefira composição a herança*); **SRP** não significa "uma classe com um único método"; **`private` não é herdado** pela subclasse; **SonarQube é análise estática**, não dinâmica; **Clean Code não proíbe todos os comentários** — elimina os dispensáveis e valoriza os que explicam o "porquê"; e o **POO não elimina a lógica condicional** — apenas a organiza e pode reduzi-la via polimorfismo. Cada nota detalha a distinção com exemplos na pegada da FGV.

## Revisão rápida do bloco

Ao terminar as cinco notas, você deve ser capaz de:

1. Distinguir **classe** (molde, definição) de **objeto** (instância concreta com valores), descrever as três dimensões do objeto — estado (atributos), comportamento (métodos) e identidade — e estabelecer a ponte com o banco: tabela ↔ classe, linha ↔ objeto, coluna ↔ atributo;
2. Explicar os **quatro pilares** — abstração, encapsulamento, herança e polimorfismo — e diferenciar os pares que se confundem (abstração vs encapsulamento, herança vs composição, sobrescrita vs sobrecarga), **diferenciar interface** (contrato de comportamento, não instanciável, ligada por `implements`) **de classe abstrata** (molde incompleto, não instanciável, ligada por `extends`), além dos quatro níveis de visibilidade (private, padrão, protected, public) e da regra de que `private` não é herdado;
3. Aplicar os princípios de **Clean Code**: nomes que revelam a intenção, funções pequenas (uma coisa por função), comentários que explicam o "porquê" — e reconhecer o que NÃO é Clean Code;
4. Distinguir **análise estática** (examina o código sem executá-lo) de **análise dinâmica** (observa a execução), identificar o **SonarQube** como ferramenta estática que detecta code smells, bugs e duplicação e explicar o papel do **Quality Gate** como limite mínimo aceitável de qualidade;
5. Definir cada princípio do **SOLID** sem trocar as letras entre si — S (responsabilidade única), O (aberto para extensão, fechado para modificação), L (substituição de Liskov), I (segregação de interfaces), D (inversão de dependência) — e reconhecer o polimorfismo como o mecanismo por trás do O.

Se você domina esses pontos, está pronto para avançar ao **Tópico 3 — [[Java-Corporativo-JavaEE-JPA-Hibernate|Java Corporativo (JavaEE, JakartaEE, JPA e Hibernate)]]**: é lá que o POO se materializa no banco de dados — as classes viram **entidades JPA** e a ponte tabela ↔ classe, linha ↔ objeto, coluna ↔ atributo vira código com anotações.

## Próximos passos

A sintaxe Java foi consolidada no **tópico 1 ([[Java-Fundamentos-da-Linguagem|Java — Fundamentos da Linguagem]])**; este tópico construiu o que está *acima* da sintaxe — o **paradigma**: classe e objeto, os quatro pilares, Clean Code, análise estática com SonarQube e SOLID. Esse vocabulário será usado em todos os tópicos seguintes: no **ecossistema Spring (tópico 5)**, que materializa em escala a inversão de dependência (o D do SOLID), e nos **padrões de projeto (tópico 6)**, que são soluções prontas construídas sobre esses princípios.

O próximo tópico da ementa é o **Java Corporativo (tópico 3 — [[Java-Corporativo-JavaEE-JPA-Hibernate|JavaEE, JakartaEE, JPA e Hibernate]])**, onde o POO conversa com o banco relacional que você estudou na Fase 3: as **entidades JPA** automatizam a ponte construída aqui — *classe* vira *tabela*, *objeto* vira *linha*, *atributo* vira *coluna* — e o **Hibernate** implementa esse mapeamento. Se o Java é a *língua*, o POO é a *gramática de design*; no Java Corporativo, essa gramática encontra o mundo dos dados.