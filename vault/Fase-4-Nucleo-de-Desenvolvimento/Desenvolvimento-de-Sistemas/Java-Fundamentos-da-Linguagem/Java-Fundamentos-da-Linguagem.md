# Java — Fundamentos da Linguagem — Índice

> [!info] Metadados
> **Disciplina:** Desenvolvimento de Sistemas
> **Bloco:** 4.1 — Desenvolvimento de Sistemas (FASE 4 — Núcleo de Desenvolvimento)
> **Tópico:** 1. Java — Fundamentos da Linguagem
> **Subtópicos:** Sintaxe essencial (estrutura de um programa, variáveis, operadores, controle de fluxo, entrada/saída) · Tipos primitivos e wrappers (autoboxing/unboxing) · Coleções (List, Set, Map) · Tratamento de exceções (checked/unchecked, try/catch/finally, throws/throw) · Generics
> **Pré-requisitos:** [[Raciocinio-Matematico-Aplicado|Raciocínio Lógico Matemático]] (lógica de programação) e [[SQL-DDL-e-DML|SQL/Banco de Dados]] (consultas, estruturas de dados)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-09-09

Este é o **índice** do Tópico 1 — Java — Fundamentos da Linguagem, o primeiro tópico da sequência de programação da Fase 4. Por ser o conteúdo mais denso do edital na parte técnica (*"Java é o tópico de maior profundidade — priorizar o ecossistema Spring, que é o mais cobrado"*), ele foi organizado em **cinco notas** dentro desta subpasta, seguindo a ordem pedagógica **do básico ao avançado**: primeiro a língua (sintaxe), depois os dados (tipos e wrappers), então as estruturas de dados (coleções), a robustez (exceções) e, por fim, a segurança de tipos (generics).

Você chega aqui dominando os dois pré-requisitos do tópico:

- Do [[Raciocinio-Matematico-Aplicado|Raciocínio Lógico Matemático]] vem a **lógica de programação**: condicionais (`se... então`), repetições, representação de conjuntos de dados. O Java transforma essa lógica em sintaxe concreta — `if`, `for`, `while`, operadores.
- Do [[SQL-DDL-e-DML|Banco de Dados]] vem a disciplina de **estruturas de dados e consultas**: listas, conjuntos e pares chave-valor — que, no Java, aparecem como **coleções** (`List`, `Set`, `Map`) — e a noção de que dados bem organizados são o alicerce de todo sistema.

Um aviso importante antes de começar: aqui o foco é a **linguagem** — sintaxe, tipos, coleções, exceções e generics. Você vai aprender a **classe como recipiente** do código (`class` + nome + chaves, com campos) como **sintaxe da linguagem** — todo programa Java vive dentro de uma classe. O **aprofundamento conceitual do paradigma orientado a objetos** — por que as classes existem, o que são objetos, herança, polimorfismo e encapsulamento, e o comportamento do objeto criado por `new` (construtor, `this`) — fica para o **tópico 2 ([[Paradigma-Orientado-a-Objetos|Paradigma Orientado a Objetos]])**. Neste tópico, a classe é ferramenta; no próximo, a classe é filosofia de design.

> [!question] Pergunta orientadora
> Todo sistema corporativo conversa com um banco relacional — como os que você modelou e [[SQL-DDL-e-DML|consultou com SQL]] na Fase 3. No Java, os dados do domínio (Beneficiario, Beneficio, CNIS) precisam ser representados em memória — listas, conjuntos, mapas — e manipulados com lógica. Como transformar a lógica treinada no RLM e a disciplina de dados do SQL em um programa Java que roda? É exatamente isso que este tópico constrói — começando pela sintaxe.

## Sequência das notas

Navegue na ordem abaixo. Cada nota parte do que a anterior ensinou e termina apontando o que a próxima retoma.

| # | Nota | Conteúdo principal (subtópicos da ementa) |
|---|------|-------------------------------------------|
| 1 | [[Sintaxe-Essencial-de-Java\|Sintaxe Essencial de Java]] | Estrutura de um programa (a classe como recipiente: `class`, `main`, campos) · Variáveis · Operadores · Controle de fluxo (if/else, for, while) · Entrada/saída |
| 2 | [[Tipos-Primitivos-e-Wrappers\|Tipos Primitivos e Wrappers]] | Os 8 tipos primitivos · Wrappers (Integer, Long, Double...) · Autoboxing/unboxing · Casting · Igualdade (**==**) vs `equals()` · `null` |
| 3 | [[Colecoes-Java\|Coleções Java]] | `List` (ArrayList, LinkedList) · `Set` (HashSet, LinkedHashSet, TreeSet) · `Map` (HashMap, LinkedHashMap, TreeMap) · Map não é Collection |
| 4 | [[Tratamento-de-Excecoes\|Tratamento de Exceções]] | Hierarquia (Throwable, Error, Exception) · Checked vs unchecked · try/catch/finally · throws vs throw · Multi-catch e try-with-resources |
| 5 | [[Generics\|Generics]] | Tipos parametrizados · Segurança de tipos em compilação · Eliminação de casts · Diamond operator (`<>`) · Classes e métodos genéricos (menção) |

> [!tip] Roteiro de estudo sugerido
> Estude as notas **em ordem** (1 → 5). A cada nota, resolva os exemplos e as pegadinhas ao final antes de avançar. As notas 2 (tipos/wrappers) e 4 (exceções) concentram as pegadinhas mais frequentes da FGV — o cache de `Integer`, o `null` no unboxing e o comportamento do `finally` são armadilhas clássicas.

## Mapa da unidade no bloco

```text
Tópicos anteriores (bases)
  RLM (lógica de programação)  →  Banco de Dados (SQL)
                          ↓
TÓPICO 1 — JAVA — FUNDAMENTOS DA LINGUAGEM (este índice)
   1. Sintaxe Essencial de Java
      ↓
   2. Tipos Primitivos e Wrappers
      ↓
   3. Coleções Java
      ↓
   4. Tratamento de Exceções
      ↓
   5. Generics
      ↓
Próximo tópico
   2. Paradigma Orientado a Objetos (classe vira design)
```

## Antes de estudar — palavras-chave do tópico

As **palavras-chave** que você deve reconhecer nas questões deste tópico são:

- **Sintaxe:** `public static void main(String[] args)`, `;`, `camelCase`, `if/else`, `for`, `while`, `System.out.println`/`print`, classe (recipiente), campo, `class`.
- **Tipos:** primitivo, wrapper, autoboxing, unboxing, sufixo `L`/`f`, cast, `null`, `equals()`.
- **Coleções:** Collection, `List`, `Set`, `Map`, ArrayList, LinkedList, HashSet, TreeSet, HashMap, duplicados, ordem, índice, chave.
- **Exceções:** Throwable, Error, Exception, RuntimeException, checked, unchecked, try, catch, finally, throws, throw, SQLException, IOException, NullPointerException.
- **Generics:** tipo parametrizado, segurança de tipos, compilação, cast, ClassCastException, diamond `<>`.

> [!warning] Cuidado com as pegadinhas recorrentes
> Bancas misturam conceitos próximos em uma mesma alternativa: `print` vs `println`, primitivo vs wrapper, `List` vs `Set`, `throw` vs `throws`, checked vs unchecked. Cada nota detalha a distinção com exemplos e questões-modelo na pegada da FGV.

## Revisão rápida do bloco

Ao terminar as cinco notas, você deve ser capaz de:

1. Escrever e interpretar um programa Java mínimo: ponto de entrada `main`, declaração de variáveis, operadores, `if/else`, `for`, `while`, entrada/saída e a classe como recipiente (`class`, `main`, campos);
2. Distinguir os 8 tipos primitivos dos wrappers, aplicar autoboxing/unboxing e identificar as pegadinhas de sufixo, cast e `null`;
3. Escolher a estrutura de dados certa entre `List` (ordem e duplicados), `Set` (unicidade) e `Map` (chave → valor), inclusive as implementações (ArrayList vs LinkedList, HashSet vs TreeSet, HashMap vs TreeMap);
4. Classificar exceções em checked/unchecked, usar `try`/`catch`/`finally` corretamente e diferenciar `throws` de `throw`;
5. Aplicar generics para ganhar segurança de tipos em tempo de compilação e eliminar casts manuais.

Se você domina esses pontos, está pronto para avançar ao **Tópico 2 — [[Paradigma-Orientado-a-Objetos|Paradigma Orientado a Objetos]]**: lá a classe deixa de ser apenas sintaxe e vira o coração do design — objeto, herança, polimorfismo, encapsulamento, abstração, SOLID e Clean Code. Se o Java é a *língua*, o POO é a *gramática de design* que organiza essa língua em sistemas bem construídos.