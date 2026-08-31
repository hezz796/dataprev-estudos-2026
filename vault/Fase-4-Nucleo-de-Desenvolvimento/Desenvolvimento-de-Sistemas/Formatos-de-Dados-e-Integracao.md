# Formatos de Dados e Integração

> [!info] Metadados
> **Disciplina:** Desenvolvimento de Sistemas
> **Bloco:** 4.1 — Desenvolvimento de Sistemas (FASE 4 — Núcleo de Desenvolvimento)
> **Tópico:** 6. Formatos de Dados e Integração
> **Subtópicos:** XML (sintaxe, namespaces, validação XSD) · XSLT (transformação de XML) · JSON (sintaxe, parsing, serialização) · UDDI (registro e descoberta de serviços)
> **Pré-requisitos:** [[Padroes-de-Projeto-e-Arquitetura|Padrões de Projeto e Arquitetura]] (SOAP, REST, Web Services) e [[Java-e-Ecossistema-JVM|Java/JVM]] (serialização, integração)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-31

---

## 1. Por que estudar formatos de dados e integração?

No tópico anterior, você aprendeu **como** os sistemas se integram — via **SOAP** (que troca mensagens **XML**) e via **REST** (que, tipicamente, troca **JSON**). Agora vamos estudar **o que exatamente viaja** por esses canais: os **formatos de dados** — **XML** e **JSON** — e as ferramentas que os acompanham (**XSLT** para transformação, **XSD** para validação, e **UDDI** para descoberta de serviços).

Para a DATAPREV, isso é fundamental: a troca de dados com o INSS, bancos, órgãos públicos e seguradoras depende de **formatos padronizados**. Um sistema que envia a folha de benefícios de milhares de cidadãos precisa que o destinatário **entenda exatamente** a estrutura recebida — e é para garantir esse entendimento que existem os **esquemas de validação** (XSD) e os **formatos** (XML/JSON).

> [!note] A conexão com o banco de dados
> Assim como o **banco relacional** [[SQL-DDL-e-DML|valida seus dados]] com restrições (chaves, `NOT NULL`, `CHECK`), o **XML** valida sua estrutura com o **XSD** (o "schema"). E, do mesmo modo que o JSON e o XML representam *dados estruturados* para troca entre sistemas, o banco os representa para armazenamento. São visões complementares do mesmo desejo: **dados bem definidos e consistentes**.

> [!question] Pergunta orientadora
> Dois sistemas diferentes (um em Java, outro em .NET) precisam trocar informações. Como garantir que ambos "entendam" o mesmo documento — a mesma hierarquia, os mesmos nomes de campos, os mesmos tipos de dado? Sem uma **validação formal**, um erro de estrutura passaria despercebido. É exatamente para isso que serve o **XSD** validando o **XML** — e para isso que o **JSON**, embora mais simples, obedece a uma **sintaxe rigorosa**.

---

## 2. XML — eXtensible Markup Language

### 2.1 O que é XML

O **XML (eXtensible Markup Language)** é uma **linguagem de marcação** criada para **representar e transportar dados estruturados** de forma legível por humanos e máquinas. Diferente do HTML (que define *apresentação*), o XML define *estrutura e conteúdo* — as tags são **definidas pelo autor** (por isso "extensible": extensível).

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beneficiario>
    <nome>Ana Souza</nome>
    <cpf>123.456.789-00</cpf>
    <status>ATIVO</status>
    <dependentes>
        <dependente nome="João" parentesco="FILHO"/>
    </dependentes>
</beneficiario>
```

Elementos essenciais: as **tags** (`<tag>`), os **atributos** (`nome="João"`), o **texto** entre tags, e a **declaração** inicial (`<?xml ...?>`).

### 2.2 XML bem formado vs. XML válido

A distinção mais cobrada do XML:

- **XML bem formado (well-formed):** segue as **regras sintáticas** básicas do XML — tem **exatamente uma raiz**, todas as tags são **fechadas**, e os atributos são **entre aspas**.
- **XML válido (valid):** além de bem formado, **obedece a um esquema** (como o **XSD**) que define a estrutura, os tipos de dados e as restrições.

```text
XML bem formado = sintaxe correta (estrutura léxica)
XML válido      = bem formado + conforme ao schema (XSD)
```

> [!warning] PEGADINHA — bem formado ≠ válido
> A pegadinha mais clássica: "todo XML válido é bem formado, mas nem todo XML bem formado é válido." **Verdadeiro.** A validade **exige** o bem formado; o bem formado é apenas a base sintática, sem garantia de conformidade a um schema. Um XML bem formado pode **não** validar contra um XSD (estrutura errada, tipo errado) — ele é bem formado, mas **inválido**. E um XML que **fecha tags erradas** nem chega a ser bem formado.

Regras de bom (well-formed) — o que a banca repete:

- uma única **raiz** (elemento que contém todos os outros);
- **toda tag aberta é fechada** (ou é auto-fechada: `<br/>`);
- atributos sempre **entre aspas**;
- **sensibilidade a maiúsculas/minúsculas** (case-sensitive): `<Nome>` ≠ `<nome>`;
- **não se sobrepõem tags**: `<a><b></a></b>` é incorreto.

```xml
<!-- MAL formado: tags cruzadas (sobrepostas) -->
<a><b>texto</a></b>

<!-- Bem formado: tags corretamente aninhadas -->
<a><b>texto</b></a>
```

### 2.3 Namespaces

**Namespaces** (espaços de nomes) no XML resolvem um problema de **colisão de nomes** entre vocabulários diferentes: quando dois esquemas usam a mesma tag com significados diferentes, o **namespace** desambigua, associando um **prefixo** a uma **URI (Uniform Resource Identifier)**.

```xml
<!-- Namespace: associa o prefixo 'ps' à URI do padrão previdenciário -->
<ps:beneficiario xmlns:ps="http://www.dataprev.gov.br/padrao-previdencia">
    <ps:cpf>123</ps:cpf>
</ps:beneficiario>
```

Sem o namespace, não há como saber se `<cpf>` pertence ao vocabulário da previdência ou, digamos, ao da operadora de saúde. O **namespace** identifica **a qual vocabulário** um elemento pertence — evitando conflitos quando vários standards dividem o mesmo documento.

> [!note] O que é a "URI" no namespace?
> O namespace usa uma **URI** apenas como **identificador único** e globalmente exclusivo — não precisa ser um link que abre algo. Serve para dar **significado próprio** a um conjunto de elementos. A banca pode perguntar que o namespace evita **colisão de nomes** entre vocabulários.

### 2.4 Validação XSD — o schema do XML

**XSD (XML Schema Definition)** é a linguagem de **esquema** que define a **estrutura e os tipos** que um XML pode ter. É o "contrato" que torna um XML *válido*. O XSD define:

- os **elementos e atributos** permitidos;
- a **ordem e obrigatoriedade** deles;
- os **tipos de dados** (string, número, data etc.);
- as **restrições** (valores possíveis, intervalos, padrões).

```xml
<!-- Esquema XSD que valida a estrutura do XML de beneficiário -->
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:element name="beneficiario">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="nome" type="xs:string"/>
        <xs:element name="cpf" type="xs:string" minOccurs="1" maxOccurs="1"/>
        <xs:element name="status" type="xs:string"/>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
</xs:schema>
```

> [!important] XML bem formado x XSD
> O **XSD** é o instrumento que transforma um XML apenas *bem formado* em **válido**. Um validador: (1) verifica se é **bem formado** (sintaxe) e (2) verifica se é **válido** contra o XSD (conformidade ao contrato). É análogo às **restrições do banco** (`NOT NULL`, `CHECK`, chaves) que você viu em [[SQL-DDL-e-DML|SQL]].

---

## 3. XSLT — transformação de XML

**XSLT (eXtensible Stylesheet Language Transformations)** é uma linguagem para **transformar** um documento XML em **outro formato** — outro XML, HTML, texto, etc. O XSLT usa uma **folha de estilo** (stylesheet) que descreve, por regras, como transformar os elementos de entrada em elementos de saída.

```xslt
<!-- Folha XSLT: transforma a lista de beneficiários em uma tabela HTML -->
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
  <xsl:template match="/">
    <html>
      <body>
        <h2>Beneficiários</h2>
        <ul>
          <xsl:for-each select="//beneficiario">
            <li><xsl:value-of select="nome"/></li>
          </xsl:for-each>
        </ul>
      </body>
    </html>
  </xsl:template>
</xsl:stylesheet>
```

- **`<xsl:template>`:** define uma regra de transformação (com `match` indicando a que nós se aplica).
- **`<xsl:for-each>`:** itera sobre um conjunto de elementos (como um `foreach`).
- **`<xsl:value-of>`:** extrai o **valor** de um elemento/atributo.

> [!example] O fluxo do XSLT
> Entrada: **XML** (os dados) + **stylesheet XSLT** (as regras) → **transformador XSLT** → **saída** (HTML, XML, texto...). Só o **XML** é transformado; o XSLT é o "molde" que decide a forma final. Isso permite, por exemplo, exibir os mesmos dados previdenciários em um site web (HTML) a partir de um XML, sem mudar os dados de origem.

> [!warning] PEGADINHA — XSLT transforma, não valida nem armazena
> O **XSLT transforma XML em outro formato** (como HTML ou outro XML) — ele **não valida** (isso é papel do XSD) e **não armazena** (isso é papel do banco/aplicação). Uma alternativa que diga "o XSLT valida o XML" está errada: a validação é do **XSD**; a transformação é do **XSLT**.

---

## 4. JSON — JavaScript Object Notation

### 4.1 O que é JSON

O **JSON (JavaScript Object Notation)** é um **formato leve de intercâmbio de dados**, derivado da sintaxe de objetos do JavaScript, **legível por humanos** e **fácil de analisar para máquinas**. É o formato dominante nas APIs REST modernas.

```json
{
  "nome": "Ana Souza",
  "cpf": "123.456.789-00",
  "status": "ATIVO",
  "renda": 3200.50,
  "dependentes": [
    { "nome": "João", "parentesco": "FILHO" }
  ],
  "ativo": true
}
```

### 4.2 Estruturas JSON

O JSON suporta **dois tipos de estrutura** básicos — que a banca adora perguntar:

- **Objeto (`{ }`):** um conjunto de pares **"chave": valor** — análogo a um dicionário/mapa. As **chaves** são *strings* entre aspas.
- **Array (`[ ]`):** uma **lista ordenada** de valores — análogo a uma lista.

E os **tipos de valor**:
- **string** (entre aspas duplas);
- **number** (inteiro ou decimal);
- **boolean** (`true`/`false`);
- **null** (valor nulo);
- objeto ou array (aninhamento).

> [!question] Por que as chaves JSON precisam de aspas duplas?
> No JSON, **toda chave de objeto é uma string** e deve ser escrita **entre aspas duplas** — diferente do JavaScript puro (onde a chave pode ser um identificador sem aspas). Isso faz parte da **sintaxe rigorosa** do JSON: ele é um *formato de dados* independente de linguagem, e a rigidez garante que qualquer parser, em qualquer linguagem, interprete igual.

### 4.3 JSON vs. XML

O JSON costuma ser preferido nas APIs REST por ser mais **leve**, **legível** e **facilmente mapeado** para objetos de programação. A comparação:

| Critério | JSON | XML |
|---|---|---|
| Sintaxe | leve, `{}` e `[]` | verboso, tags |
| Legibilidade humana | alta | média/menor |
| Tipos de dados | nativos (number, boolean, null) | todos como texto (tipos definidos no XSD) |
| Validação formal | sem padrão tão consolidado como o XSD; usa schemas (JSON Schema) | **XSD** tradicional e robusto |
| Metadados/namespaces | não possui | suporta **namespaces** e atributos |
| Uso típico | APIs REST modernas | SOAP, documentos com metadados ricos e transformações |

> [!warning] PEGADINHA — JSON ainda "vem de JavaScript"
> Embora o JSON tenha nascido da sintaxe de objetos do **JavaScript**, ele é um **formato independente de linguagem** — qualquer linguagem (Java, Python, C#) pode produzir e consumir JSON. A frase "JSON só funciona com JavaScript" é **falsa**. É um formato de intercâmbio textual.

### 4.4 Parsing e serialização

Dois conceitos complementares, muito cobrados:

- **Serialização (serialization):** transformar um **objeto em memória** em **texto JSON** (por exemplo, para enviar numa requisição HTTP).
- **Parsing/deserialização (parsing/deserialization):** transformar o **texto JSON** de volta em **objeto em memória** (por exemplo, ao receber uma resposta HTTP).

```java
// Serialização: objeto Java -> JSON
ObjectMapper mapper = new ObjectMapper();
Beneficiario b = new Beneficiario("Ana", "123", 3200);
String json = mapper.writeValueAsString(b);   // {"nome":"Ana",...}

// Parsing (deserialização): JSON -> objeto Java
Beneficiario b2 = mapper.readValue(json, Beneficiario.class);
```

> [!important] Serialização vs. Parsing — direções opostas
> **Serialização** = objeto → texto JSON (para fora). **Parsing/deserialização** = texto JSON → objeto (para dentro). São a **mesma ponte** vista em direções opostas. Em Java, a biblioteca **Jackson** (`ObjectMapper`) faz ambos. A banca cobra a direção: "transformar objeto em JSON" é **serializar**; "transformar JSON em objeto" é **fazer parsing (deserializar)**.

---

## 5. UDDI — registro e descoberta de serviços

O **UDDI (Universal Description, Discovery and Integration)** é um **registro/diretório padronizado** de **Web Services** — o mecanismo de **descoberta** dentro do contexto de **SOA** (que você viu no tópico anterior). Pense nele como uma "lista telefônica" ou "Páginas Amarelas" dos serviços web.

O papel do UDDI no ciclo SOA é permitir que um consumidor:

1. **descreva** um serviço (o que ele faz);
2. **publique** a sua existência e localização;
3. **descubra** um serviço adequado às suas necessidades e obtenha como acessá-lo.

```
Provedor de serviço
      │ publica (publish)
      ▼
    [UDDI Registry]  ← catálogo central
      │ descoberta (find)
      ▼
Consumidor de serviço → (obtém o WSDL) → chama o serviço
```

> [!note] O trio da SOA e onde entra o UDDI
> Na SOA, o ciclo clássico é: **publish** (publicar), **find** (descobrir/achar) e **bind** (vincular/chamar). O **UDDI** cuida do **publish** e do **find** — é o diretório que registra os serviços e permite que sejam achados. Após descobrir no UDDI, o consumidor obtém o **WSDL** (o contrato) e faz o **bind** (chama o serviço, geralmente SOAP). O **WSDL** descreve *como* chamar; o **UDDI** informa *onde existe* e *o que é*.

> [!warning] PEGADINHA — UDDI é para descoberta, não para execução
> O **UDDI** é um **diretório/registro** para **descrever, publicar e descobrir** serviços — ele **não executa** o serviço nem transporta as mensagens. Executar/transportar é papel do **protocolo** (SOAP sobre HTTP). A pegadinha: "o UDDI executa o Web Service" — **falso**, ele apenas **registra e localiza**. O **WSDL** descreve o contrato; o **SOAP** transporta a mensagem; o **UDDI** descobre o serviço.

---

## 6. Como a FGV cobra este tópico

- **XML bem formado vs. válido:** o bem formado é a sintaxe; o válido exige conformidade ao **XSD**. O válido é subconjunto do bem formado (mas o inverso não é verdadeiro).
- **Namespaces:** evitar **colisão de nomes** entre vocabulários, usando prefixos ligados a URIs.
- **XSD:** o esquema que **valida** a estrutura e tipos do XML.
- **XSLT:** transforma XML em outro formato (HTML, XML, texto).
- **JSON:** formato leve; objetos `{}` e arrays `[]`; chaves com aspas duplas; **independente de linguagem**.
- **Serialização vs. parsing:** objeto → JSON (serializar) vs. JSON → objeto (parsear).
- **UDDI:** diretório/registro para **descrever, publicar e descobrir** serviços (find/publish); não executa.
- **Integração:** JSON domina REST; XML domina SOAP; XSD valida; XSLT transforma; UDDI descobre.

> [!warning] PEGADINHA — as distinções que definem a nota
> (1) **bem formado** (sintaxe) vs. **válido** (sintaxe + schema). (2) **XSD valida**, **XSLT transforma**. (3) **serializar** (objeto→JSON) vs. **parsear** (JSON→objeto). (4) **UDDI descobre/publica**, **não executa**. Cada uma dessas quatro trocas de papel é uma armadilha de prova clássica.

---

## 7. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **XML:** linguagem de marcação para transportar dados estruturados; tags definidas pelo autor (extensible)
> - [ ] **Bem formado:** sintaxe correta (uma raiz, tags fechadas, aspas nos atributos, case-sensitive)
> - [ ] **Válido:** bem formado **+** conforme ao **XSD**; o válido é subconjunto do bem formado
> - [ ] **Namespaces:** prefixos ligados a URIs para **evitar colisão de nomes**
> - [ ] **XSD:** esquema que define estrutura, tipos e restrições (validação)
> - [ ] **XSLT:** transforma XML em HTML/XML/texto (regras `template`, `for-each`, `value-of`)
> - [ ] **JSON:** leve, `{}` objetos / `[]` arrays; chaves com aspas duplas; **independente de linguagem**
> - [ ] **Serialização** (objeto→JSON) vs. **Parsing/deserialização** (JSON→objeto)
> - [ ] **UDDI:** diretório para **descrever, publicar e descobrir** serviços (find/publish); não executa
> - [ ] Integração: JSON em REST, XML em SOAP; XSD valida, XSLT transforma

> [!warning] O erro mais comum em prova
> Confundir os **papéis**: acreditar que o **XSD transforma** (na verdade valida) ou que o **XSLT valida** (na verdade transforma), e achar que o **UDDI executa** serviços (na verdade registra/descobre). E trocar **bem formado por válido** — na dúvida, lembre: *válido = bem formado + schema*.

---

## 8. Próximos passos

Você agora sabe como os sistemas se **comunicam** (SOAP/REST, do tópico anterior) e **o que** viaja por esses canais (XML, XSLT, JSON e o UDDI para descoberta). Essa é a fundação de qualquer **integração entre sistemas** — exatamente o que a DATAPREV faz ao conectar os sistemas de benefícios aos órgãos e bancos.

Nas próximas duas notas, a ementa explora dois outros mundos do desenvolvimento. O **Desenvolvimento Mobile** mostra como o POO, o Java e o JavaScript que você estudou se aplicam aos apps Android (Activity, Fragment, Intent, RecyclerView) e iOS (UIKit, SwiftUI), além dos conceitos de **low-code/no-code**. E o **DevOps e Controle de Versão** (Git, CI/CD, Docker e ambientes) cuida de **como o código produzido é versionado, construído e entregue**. São os dois caminhos que fecham o Núcleo de Desenvolvimento.
