# Tipos de Codificação

> [!info] Metadados
> **Disciplina:** Metodologias e Engenharia de Software
> **Bloco:** 4.2 — Metodologias e Engenharia de Software (FASE 4 — Núcleo de Desenvolvimento)
> **Tópico:** 3. Tipos de Codificação
> **Subtópicos:** Sistemas transacionais (CRUD, integração, regras de negócio) · Analíticos (relatórios, dashboards, processamento de dados) · Mobile (nativo, híbrido, responsividade) · API (desenvolvimento e versionamento)
> **Pré-requisitos:** [[Desenvolvimento-de-Sistemas]] (Java, Spring, APIs RESTful, mobile) e [[Banco-de-Dados|Banco de Dados]], com os conceitos de OLTP/OLAP sendo INTRODUZIDOS nesta nota (a modelagem dimensional e o ETL são aprofundados no bloco posterior de BI/Data Warehouse)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-31

---

## 1. Por que estudar tipos de codificação?

Até aqui você aprendeu *como* programar (POO, Java, JavaScript), *como* entregar (DevOps, Git), *como* organizar o trabalho (Scrum, Kanban) e *como* reutilizar soluções (padrões, frameworks). Mas **em que contextos** o código é produzido? O tipo de sistema que você vai desenvolver determina **arquitetura, ferramentas, padrões e até a forma como os dados são tratados**.

A DATAPREV trabalha com **todos** esses tipos: o **Meu INSS** é um app mobile; o **sistema de cálculo de benefícios** é um sistema transacional; os **relatórios gerenciais** são sistemas analíticos; e as **integrações entre órgãos** são APIs. Um analista de TI precisa reconhecer qual tipo de sistema está lidando e escolher a abordagem certa.

> [!question] Pergunta orientadora
> Pense em dois cenários: (1) um usuário consulta seu benefício no app e recebe a resposta em segundos — isso é **transacional** (operação pontual e rápida). (2) Um gerente solicita um relatório consolidado de todos os benefícios pagos no último trimestre — isso é **analítico** (processamento de grandes volumes para análise). A mesma DATAPREV precisa dos dois. O que diferencia um do outro? A resposta envolve **tipo de operação, volume de dados e objetivo** — e determina completamente como o software deve ser construído.

---

## 2. Sistemas transacionais (OLTP)

### 2.1 O que são

Um **sistema transacional** processa **operações pontuais e rápidas** — cada operação (transação) é uma unidade atômica de trabalho. O foco é **capturar, atualizar e consultar dados em tempo real**, com alta disponibilidade e integridade.

O nome técnico é **OLTP — Online Transaction Processing**. A sigla oposta é OLAP (Online Analytical Processing), que veremos na seção 3.

> [!note] Conexão com Banco de Dados
> O conceito de **transação e ACID** (Atomicidade, Consistência, Isolamento, Durabilidade) que você estudou no [[Banco-de-Dados|Bloco 3.1]] é o fundamento dos sistemas transacionais. Cada operação de CRUD é uma transação que precisa respeitar as propriedades ACID — especialmente em sistemas governamentais onde a integridade dos dados é crítica.

### 2.2 CRUD — o ciclo básico

A maioria dos sistemas transacionais se baseia em quatro operações fundamentais, conhecidas pela sigla **CRUD**:

| Letra | Operação | SQL equivalente | Exemplo na DATAPREV |
|---|---|---|---|
| **C** | **Create** (criar) | `INSERT` | Cadastrar um novo beneficiário |
| **R** | **Read** (ler/consultar) | `SELECT` | Consultar o status de um benefício |
| **U** | **Update** (atualizar) | `UPDATE` | Alterar o endereço de um beneficiário |
| **D** | **Delete** (remover) | `DELETE` | Cancelar uma solicitação duplicada |

A ligação entre CRUD e verbos HTTP (que você viu no [[Padroes-de-Projeto-e-Arquitetura|Bloco 4.1]]) é direta:

| CRUD | Verbo HTTP | Ação |
|---|---|---|
| Create | POST | criar recurso |
| Read | GET | consultar recurso |
| Update | PUT/PATCH | atualizar recurso |
| Delete | DELETE | remover recurso |

> [!warning] PEGADINHA — CRUD não é "fazer tudo"
> CRUD define as quatro operações **básicas** sobre dados. Um sistema transacional pode ter regras de negócio complexas *além* do CRUD (validações, cálculos, integrações) — mas o CRUD é a **base**. A banca pode perguntar: "Qual operação SQL corresponde ao Update?" → `UPDATE`. Ou: "Qual verbo HTTP corresponde ao Create?" → `POST`.

### 2.3 Integração e regras de negócio

Sistemas transacionais na DATAPREV não operam isolados — eles se **integram** com outros sistemas (bancos, INSS, órgãos públicos) via **APIs RESTful**, **Web Services SOAP** ou **mensageria**. E contêm **regras de negócio** complexas: cálculos de benefícios, validações de elegibilidade, regras de consignação.

> [!question] Como o backend Spring se encaixa aqui?
> O [[Frameworks-Java|Spring Boot]] que você estudou é a ferramenta natural para construir sistemas transacionais: ele fornece **REST Controllers** (para CRUD via HTTP), **Services** (para regras de negócio), **Repositories** (para acesso a dados via JPA) e **transações** gerenciadas automaticamente. É a materialização do **MVC** no backend.

---

## 3. Sistemas analíticos (OLAP)

### 3.1 O que são

Um **sistema analítico** processa **grandes volumes de dados** para produzir **informações consolidadas** que auxiliam na tomada de decisão. Não se trata de operações pontuais (como consultar um benefício), mas de **agregar, cruzar e analisar** dados históricos.

O nome técnico é **OLAP — Online Analytical Processing**.

| Critério | OLTP (transacional) | OLAP (analítico) |
|---|---|---|
| **Objetivo** | operações do dia a dia (CRUD) | análise e tomada de decisão |
| **Volume** | operações pontuais, muitas por segundo | grandes volumes, processamento em lote |
| **Dados** | dados atuais e em tempo real | dados históricos e consolidados |
| **Modelo** | normalizado (3FN) | **desnormalizado** (star schema, snowflake) |
| **Exemplo** | cadastrar beneficiário | relatório de benefícios pagos por região no último ano |
| **Acesso** | muitas leituras e escritas rápidas | poucas consultas pesadas (agregações) |
| **Banco** | banco transacional (PostgreSQL, Oracle) | **Data Warehouse**, Data Lake |

> [!note] Sugestão de leitura da tabela
> Os termos **star schema**, **snowflake**, **Data Warehouse** e **Data Lake** aparecem aqui apenas como **contraste** para mostrar a diferença entre OLTP e OLAP. Você **não precisa dominá-los ainda** — são conceitos do **bloco posterior de BI/Data Warehouse**.

### 3.2 Relatórios e dashboards

Os principais produtos de um sistema analítico são:

- **Relatórios:** documentos estruturados que apresentam dados consolidados (ex.: relatório mensal de benefícios pagos por tipo e região).
- **Dashboards:** painéis visuais interativos que mostram **métricas em tempo real ou quase-real** (ex.: painel de acompanhamento do fluxo de benefícios).

> [!note] Conexão com Banco de Dados
> A distinção entre **OLTP** (transacional, normalizado) e **OLAP** (analítico, desnormalizado) é **introduzida aqui**, nesta nota. Enquanto o [[Banco-de-Dados|Bloco 3.1]] estudou a normalização relacional tradicional (OLTP), a **modelagem dimensional** — como os **star schema** e **snowflake**, que separam **fatos** (dados numéricos mensuráveis) de **dimensões** (contexto: tempo, região, tipo) — é o que leva a dados **desnormalizados** para OLAP. Esse aprofundamento (star schema, snowflake, fatos, dimensões, ETL) será estudado no **bloco posterior de BI/Data Warehouse**, que você ainda não viu.

### 3.3 Processamento de dados

Sistemas analíticos também envolvem **processamento de dados em lote**: ETL (*Extract, Transform, Load*), que extrai dados de fontes transacionais, transforma (limpa, agrega, cruza) e carrega em um Data Warehouse para análise. Na DATAPREV, isso é essencial para gerar indicadores do Programa de Benefícios, dashboards gerenciais e relatórios para órgãos de controle. Por ora, basta entender a **ideia** de ETL e de Data Warehouse; o **aprofundamento** — modelagem dimensional, fatos/dimensões, ETL detalhado e as tecnologias de Data Warehouse — é tema do **bloco posterior de BI/Data Warehouse**, que você ainda vai estudar.

> [!warning] PEGADINHA — OLTP não é OLAP
> A armadilha mais comum: tratar OLTP e OLAP como sinônimos ou inverter as características. **OLTP** = operações pontuais, dados atuais, normalizado. **OLAP** = análise de grandes volumes, dados históricos, desnormalizado. Na questão, identifique: *estamos fazendo uma operação pontual (OLTP) ou analisando dados consolidados (OLAP)?*

---

## 4. Mobile — nativo, híbrido e responsividade

Você já estudou o [[Desenvolvimento-Mobile|desenvolvimento mobile no Bloco 4.1]] (Android, iOS, low-code/no-code). Aqui, o tópico reforça a **classificação das abordagens** sob a ótica de Engenharia de Software:

| Abordagem | O que é | Exemplo | Vantagem |
|---|---|---|---|
| **Nativo** | desenvolvido para **uma plataforma específica** usando suas linguagens/SDKs | Android (Java/Kotlin), iOS (Swift) | máximo desempenho e acesso a APIs nativas |
| **Híbrido** | desenvolvido com tecnologia **web** (HTML, CSS, JS) que roda dentro de um container nativo | React Native, Flutter, Ionic | **um único código** para Android e iOS |
| **Responsividade (web)** | site web que se adapta ao tamanho da tela do dispositivo | HTML + CSS (media queries) | sem instalação; funciona em qualquer navegador |

> [!question] Quando escolher nativo vs. híbrido?
> Se o app precisa de **alto desempenho** (jogos, realidade aumentada) ou acesso profundo a APIs do dispositivo, o **nativo** é melhor. Se o foco é **agilidade de desenvolvimento** e o app não depende pesadamente de APIs nativas, o **híbrido** economiza tempo e recurso. Na DATAPREV, apps como o Meu INSS usam abordagens que equilibram acesso nativo e reuso de código (React Native, por exemplo).

> [!warning] PEGADINHA — híbrido ≠ responsivo
> Um app **híbrido** é um app que usa tecnologia web (JS/HTML/CSS) mas é **empacotado como um app nativo** (tem .apk, aparece na loja). Um site **responsivo** é um site web que se adapta ao tamanho da tela — mas continua sendo um **site no navegador**, não um app instalável. A banca troca: "um site responsivo é um app híbrido" — **falso**.

---

## 5. API — desenvolvimento e versionamento

### 5.1 APIs como tipo de codificação

Desenvolver uma **API** é um tipo específico de codificação: em vez de criar uma interface visual para humanos, você cria uma **interface para outros softwares**. APIs são o mecanismo de **integração** entre sistemas — e na DATAPREV, onde dezenas de órgãos e sistemas precisam conversar, elas são a espinha dorsal da infraestrutura.

No [[Padroes-de-Projeto-e-Arquitetura|Bloco 4.1]], você estudou APIs RESTful (verbos HTTP, status codes, OpenAPI/Swagger). Aqui, adicionamos o conceito de **versionamento**.

### 5.2 Versionamento de APIs

Quando uma API evolui (novos campos, novas funcionalidades, mudanças de estrutura), os clientes que já a consomem precisam continuar funcionando. O **versionamento** é o mecanismo de garantir **compatibilidade retroativa**.

Os principais formatos de versionamento:

| Método | Como funciona | Exemplo |
|---|---|---|
| **Via URL (path)** | a versão faz parte da URL | `/api/v1/beneficiarios` vs. `/api/v2/beneficiarios` |
| **Via query parameter** | versão como parâmetro de query | `/api/beneficiarios?version=1` |
| **Via header HTTP** | versão no cabeçalho da requisição | `Accept: application/vnd.api.v1+json` |
| **Semantic versioning (SemVer)** | versão estruturada: `MAJOR.MINOR.PATCH` | `2.3.1` |

### 5.3 Semantic Versioning (SemVer)

O **Semantic Versioning** é o padrão mais utilizado para versionamento de software e APIs. Ele segue a estrutura:

$$
\text{Versão} = MAJOR.MINOR.PATCH
$$

| Componente | Muda quando... | Exemplo |
|---|---|---|
| **MAJOR** | há **mudanças incompatíveis** com versões anteriores (breaking changes) | `1.x.x → 2.0.0` |
| **MINOR** | há **novas funcionalidades** compatíveis com versões anteriores | `1.1.x → 1.2.0` |
| **PATCH** | há **correções de bugs** compatíveis | `1.2.0 → 1.2.1` |

> [!example] Exemplo na DATAPREV
> Uma API de consulta de benefícios está na versão `1.3.2`. Se você **adiciona** um novo campo na resposta (compatível), a versão vai para `1.4.0`. Se você **remove** um campo ou muda o formato da resposta (breaking change), vai para `2.0.0`. Se você **corrige** um bug de formatação, vai para `1.3.3`.

> [!warning] PEGADINHA — versionamento via URL é o mais visual, mas não o único
> A banca pode perguntar "qual é o método de versionamento mais comum?" — a resposta é **via URL** (`/v1/`, `/v2/`) por ser o mais simples e visual. Mas todos os métodos são válidos. O Semantic Versioning é o padrão para **versionamento do software/da API em si**, enquanto os métodos anteriores são para **versionamento do endpoint HTTP** — são níveis diferentes.

> [!note] Conexão com o que você já sabe
> O versionamento se conecta diretamente com as [[Padroes-de-Projeto-e-Arquitetura|APIs RESTful]] do Bloco 4.1. Quando uma API RESTful atinge muitos consumidores (como a API do INSS consumida por bancos), o versionamento garante que mudanças não quebrem os clientes existentes. E o **OpenAPI/Swagger** pode documentar múltiplas versões da mesma API.

---

## 6. Resumo comparativo dos tipos

| Tipo | Objetivo principal | Exemplo DATAPREV | Tecnologias associadas |
|---|---|---|---|
| **Transacional (OLTP)** | operações CRUD em tempo real | consulta/cadastro de benefícios | Spring, JPA, SQL, REST |
| **Analítico (OLAP)** | análise de grandes volumes | relatórios gerenciais | Data Warehouse, ETL, dashboards |
| **Mobile** | apps para dispositivos móveis | Meu INSS | Android, iOS, React Native |
| **API** | integração entre sistemas | integração INSS-bancos | REST, versionamento, OpenAPI |

---

## 7. Como a FGV cobra este tópico

- **OLTP vs. OLAP:** a banca adora inverter as características. OLTP = operações pontuais, normalizado, dados atuais. OLAP = análise consolidada, desnormalizado, dados históricos.
- **CRUD:** associar cada operação ao SQL e ao verbo HTTP correspondente.
- **Mobile:** nativo (plataforma específica) vs. híbrido (tecnologia web empacotada) vs. responsivo (site adaptativo, não é app).
- **Versionamento:** Semantic Versioning (MAJOR.MINOR.PATCH) — MAJOR = breaking change, MINOR = nova feature compatível, PATCH = correção.
- **APIs:** reforço do que foi visto no Bloco 4.1, com foco no versionamento.

> [!warning] PEGADINHA — as distinções mais prováveis
> (1) **OLTP** (transacional, CRUD, normalizado) ≠ **OLAP** (analítico, agregação, desnormalizado). (2) **App híbrido** (empacotado, instalável) ≠ **site responsivo** (adapta tela, mas continua no navegador). (3) **MAJOR** = breaking change · **MINOR** = feature compatível · **PATCH** = correção. (4) **CRUD** = Create, Read, Update, Delete — associar ao SQL e ao HTTP.

---

## 8. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **OLTP (transacional):** CRUD, operações pontuais, dados atuais, normalizado, alta disponibilidade
> - [ ] **OLAP (analítico):** relatórios, dashboards, grandes volumes, dados históricos, desnormalizado
> - [ ] **CRUD:** Create (POST/INSERT), Read (GET/SELECT), Update (PUT/UPDATE), Delete (DELETE)
> - [ ] **Mobile:** nativo (desempenho, plataforma específica) · híbrido (código único, empacotado) · responsivo (site adaptativo, não é app)
> - [ ] **Versionamento de API:** URL (`/v1/`), query param, header, Semantic Versioning
> - [ ] **SemVer:** MAJOR (breaking) · MINOR (feature compatível) · PATCH (correção)
> - [ ] **APIs:** tipo de codificação voltado para integração entre sistemas

> [!warning] O erro mais comum em prova
> Confundir **OLTP com OLAP** (inverter normalizado/desnormalizado) e confundir **app híbrido com site responsivo**. Na questão, pergunte: *estamos fazendo operações pontuais (OLTP/CRUD) ou analisando dados consolidados (OLAP)?* e *o resultado é instalável como app (híbrido) ou é um site no navegador (responsivo)?*

---

## 9. Próximos passos

Você agora reconhece os **quatro grandes contextos** de codificação: transacional, analítico, mobile e API. No próximo tópico, vamos estudar como **estimar o tamanho e o esforço** desses projetos: **Pontos de Função (APF)** para sistemas transacionais e analíticos, e **Story Points** para estimativas ágeis. É uma área **muito cobrada** em concursos públicos — e uma das mais práticas.
