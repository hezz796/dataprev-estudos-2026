# DevOps e Controle de Versão

> [!info] Metadados
> **Disciplina:** Desenvolvimento de Sistemas
> **Bloco:** 4.1 — Desenvolvimento de Sistemas (FASE 4 — Núcleo de Desenvolvimento)
> **Tópico:** 8. DevOps e Controle de Versão
> **Subtópicos:** Git (init, add, commit, branch, merge, rebase, pull request) · CI/CD (conceito, Jenkins, GitHub Actions — conceito) · Containerização (Docker — conceito básico) · Ambientes (Internet, intranet, portal)
> **Pré-requisitos:** [[Raciocinio-Matematico-Aplicado|Raciocínio Lógico Matemático]] (raciocínio de processos e sequências) e [[Paradigma-Orientado-a-Objetos|POO/Desenvolvimento]] (contexto do código versionado)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-31

---

## 1. Por que estudar DevOps e controle de versão?

Chegamos à última nota do **Núcleo de Desenvolvimento**. Todo o código produzido até aqui — Java, JavaScript, apps mobile — precisa ser **versionado, construído, testado e entregue** de forma confiável e repetível. É exatamente isso que o **DevOps** (integração entre desenvolvimento e operações) e o **controle de versão** (Git) fazem: transformam o "código que funciona na minha máquina" em um **software que chega ao usuário com qualidade**.

Na DATAPREV, que entrega sistemas críticos da seguridade social, uma entrega mal feita pode impactar milhões de cidadãos. Por isso, o controle de versão, o pipeline de CI/CD e a padronização de ambientes são mais do que conveniência — são **exigência operacional**. E há uma conexão com o raciocínio: pensar em **branches, merges e pipelines** é pensar em **processos e dependências** — a mesma lógica de sequência e condição que você treinou na Fase 1.

> [!question] Pergunta orientadora
> Vários desenvolvedores editam o mesmo código ao mesmo tempo. Sem um sistema de controle de versão, um sobrescreveria o trabalho do outro. Como garantir que todas as mudanças convivam, que dê para voltar a qualquer versão anterior e que o histórico seja preservado? A resposta é o **Git** — ainda que o conceito de "commit", "branch" e "merge" pareça abstrato à primeira vista, a lógica por trás é simples e poderosa.

---

## 2. Git — o sistema de controle de versão

### 2.1 Os três "estágios" da área de trabalho

O Git organiza o trabalho em **três áreas/estágios**, cuja compreensão é a base de tudo:

```
Working Directory (área de trabalho)
        │ git add
        ▼
Staging Area / Index (área de preparação)
        │ git commit
        ▼
Repository (repositório / histórico)
```

- **Working Directory (área de trabalho):** onde os arquivos existem e você **edita**.
- **Staging Area / Index (área de preparação):** onde você **seleciona** (marca) quais alterações entrarão no próximo commit (via `git add`).
- **Repository (repositório):** o **histórico de commits** já salvos (via `git commit`).

> [!important] add → commit
> O **`git add`** move alterações da área de trabalho para a **staging area** (prepara/empilha). O **`git commit`** grava as alterações **preparadas** no **histórico do repositório**. A pegadinha clássica: apenas o `git commit` registra permanentemente no histórico; o `git add` apenas *prepara* (marca) o que será registrado.

### 2.2 Os comandos essenciais

| Comando | O que faz |
|---|---|
| `git init` | **inicializa** um repositório Git num diretório |
| `git add <arquivo>` | move alterações para a **staging area** |
| `git commit -m "mensagem"` | grava as alterações preparadas no **histórico** |
| `git branch <nome>` | **cria** uma nova branch (ramo) |
| `git checkout <branch>` / `git switch` | **troca** para uma branch |
| `git merge <branch>` | **integra** uma branch na branch atual |
| `git rebase <branch>` | **rebaseia**: reaplica commits sobre outra base |
| `git pull` | busca e **integra** alterações do repositório remoto |
| `git push` | **envia** os commits locais para o repositório remoto |
| `git status` | mostra o **estado** (arquivos modificados, na staging etc.) |
| `git log` | mostra o **histórico** de commits |

```bash
# Fluxo básico
git init                      # cria o repositório
git add .                     # prepara todas as alterações (staging)
git commit -m "Implementa cálculo do benefício"   # grava no histórico
git push origin main          # envia para o repositório remoto
```

> [!warning] PEGADINHA — o `git add .` não é um commit
> O `git add .` **apenas prepara** todas as alterações na **staging area** — **não** cria commit, **não** envia para o remoto. Para realmente registrar no histórico é preciso o `git commit`; para enviar ao remoto, o `git push`. A banca adora dizer "git add registra permanentemente" — **falso**; quem registra é o `commit`.

### 2.3 Branch — o ramo

Uma **branch (ramo)** é uma **linha independente de desenvolvimento** que parte do histórico. Ela permite trabalhar em uma funcionalidade nova **sem interferir** na branch principal (geralmente `main`/`master`). Cada lista de commits de um ramo é uma branch.

```bash
git branch feature/consignacao   # cria um ramo
git checkout feature/consignacao # entra nele
# ... desenvolve e commita ...
git checkout main                # volta à principal
git merge feature/consignacao    # integra as mudanças do ramo na principal
```

### 2.4 Merge vs. Rebase

Dois comandos para **integrar** uma branch na outra — com filosofias diferentes:

- **`git merge`:** cria um **commit de mesclagem** que junta os históricos das duas branches, **preservando o histórico** de ambas. O histórico fica com ramificações.

- **`git rebase`:** **reaplica (rebaseia) os commits de uma branch sobre a outra**, resultando em um histórico **linear** (sem os pontos de ramificação). Reescreve o histórico dos commits rebaseados.

```text
MERGE (mantém bifurcação/commit de merge):
    A---B---C---D (main)
         \       /
          X---Y  (feature, mesclada)

REBASE (histórico linear):
    A---B---X'---Y'    (commits X,Y reaplicados sobre B)
```

> [!warning] PEGADINHA — merge preserva; rebase lineariza/reescreve
> O **merge** preserva o histórico das duas branches (gera um commit de integração). O **rebase** reescreve/lineariza o histórico (reaplica os commits sobre uma nova base, sem o "nó" de merge). A pegadinha: "o rebase criou um commit de merge" — **falso**, o rebase é que **evita** o commit de merge ao linearizar.

### 2.5 Pull Request

A **Pull Request (PR)** é um **pedido de revisão e integração** de uma branch em outra (geralmente na principal). Não é um comando Git em si, mas um **recurso das plataformas** (GitHub, GitLab): o desenvolvedor sobe sua branch (`push`) e abre uma **PR** para que outros **revisem** o código antes do **merge**. É o mecanismo de **revisão de código** e de **colaboração controlada**.

> [!note] Pull request = revisão antes de integrar
> Uma **Pull Request** promove o **controle de qualidade**: antes de a branch ser mesclada na principal, ela passa por **revisão** (código) e, muitas vezes, pela **CI** (veremos na seção 3). Serve para **discutir, revisar e aprovar** a mudança. A pegadinha: a PR **não é** o mesmo que o `merge` automático — ela é o *pedido* para integrar, que depende de **aprovação**.

---

## 3. CI/CD — Integração e Entrega Contínuas

### 3.1 O conceito

**CI/CD** é uma combinação de práticas para **automatizar** a entrega de software:

- **CI (Continuous Integration — Integração Contínua):** integrar o código **frequentemente** (várias vezes ao dia) e **automatizar a verificação** — compilar, rodar testes automaticamente sempre que um código novo é enviado. O objetivo é **detectar erros cedo**.
- **CD (Continuous Delivery/Deployment — Entrega/Implantação Contínua):** após a CI passar, **automatizar a entrega/implantação** do software nos ambientes. *Continuous **Delivery*** (Entrega Contínua): o software fica pronto para ir a produção com um clique; *Continuous **Deployment*** (Implantação Contínua): a implantação em produção acontece automaticamente.

```
código → build (compilar) → testar → empacotar → implantar (CD) → produzir
               └─────────────── CI ───────────────┘
```

> [!question] Por que automatizar o teste a cada envio de código?
> Se o código só for testado no final, os erros surgem tarde, misturados, difíceis de localizar. Com a **CI**, cada `push` dispara automaticamente um **build + testes** — se algo quebrar, o time descobre **na hora** e **onde**. A **CD** estende isso ao empacotamento e à implantação, tornando a entrega **repetível e confiável** (a mesma receita toda vez).

### 3.2 Jenkins

O **Jenkins** é uma das **ferramentas de CI/CD** mais usadas e tradicionais, de **código aberto**. Ele permite **automatizar o pipeline** — a sequência de etapas (build → teste → empacotar → publicar). Configura-se **jobs/pipelines** que disparam ao **detectar mudanças** no repositório.

- **Pipeline:** a **sequência de etapas automatizadas** (ex.: compilar, rodar JUnit, empacotar JAR, publicar).
- **Jenkins:** o **servidor/ferramenta** que executa esses pipelines, disparado por eventos (ex.: novo commit no Git).

### 3.3 GitHub Actions (conceito)

**GitHub Actions** é o serviço de **CI/CD nativo do GitHub**: você define **workflows** em arquivos (`.github/workflows/*.yml`) com **jobs e steps**; o GitHub executa esses workflows automaticamente em resposta a eventos (push, pull request etc.). É o "Jenkins", mas **integrado ao GitHub** (sem servidor próprio tão configurado).

```yaml
# Conceito de workflow do GitHub Actions (arquivo YAML)
name: CI
on: [push]              # dispara a cada push
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: mvn test   # roda os testes automaticamente
```

> [!warning] PEGADINHA — distinguir a ferramenta do conceito
> O **conceito** é o **pipeline de CI/CD** (a sequência automatizada build→teste→entrega). O **Jenkins** e o **GitHub Actions** são **ferramentas/plataformas** que executam esses pipelines. Uma alternativa que trate "Jenkins" como sinônimo de "conceito de CI/CD" ou que diga "GitHub Actions não automatiza nada" está mal formulada — ambos *automatizam* o pipeline; a diferença é onde/como.

---

## 4. Containerização — Docker

### 4.1 Imagem vs. Container

A **containerização** empacota uma **aplicação e suas dependências** numa unidade isolada e portátil (o **container**), que roda **igual** em qualquer ambiente. O **Docker** é a ferramenta mais famosa. A distinção central:

- **Imagem (image):** o **modelo/template** imutável com tudo que a aplicação precisa (código, runtime, bibliotecas, configuração). É a "receita".
- **Container:** a **instância executável** criada a partir da imagem — o "bolo assado", rodando. Você pode criar **vários containers** da mesma imagem.

> [!important] Imagem é o molde; container é a instância
> A **imagem** é o **template imutável** de onde partem os containers; o **container** é a **instância em execução**. A mesma imagem serve de base para **muitos containers** independentes. Essa relação **imagem ↔ container** ecoa a de **classe ↔ objeto** que você viu no [[Paradigma-Orientado-a-Objetos|POO]]: um "molde" e suas "peças".

```text
Imagem Docker (template)  ──run──►  Container 1 (executando)
        │                            Container 2 (executando)
        └──(modelo imutável)         Container 3 (executando)
```

### 4.2 Por que containers?

- **Portabilidade:** roda igual em qualquer lugar (dev, teste, produção) porque leva o ambiente junto.
- **Isolamento:** cada container é isolado dos demais (processos, sistema de arquivos).
- **Consistência:** elimina o "na minha máquina funciona" — o ambiente acompanha a aplicação.
- **Leveza:** comparados às **máquinas virtuais (VMs)**, os containers são mais **leves** (compartilham o **kernel** do sistema operacional hospedeiro; as VMs precisam de um SO completo).

> [!warning] PEGADINHA — container vs. máquina virtual
> O **container** compartilha o **kernel do host** (é mais leve, inicia mais rápido). A **máquina virtual (VM)** inclui um **sistema operacional convidado completo** (é mais pesada, usa mais recursos). A pegadinha: "o container inclui um sistema operacional completo" — **falso**; ele isola a aplicação e as dependências, mas reutiliza o kernel do hospedeiro.

---

## 5. Ambientes: Internet, intranet e portal

A entrega do software acontece em **ambientes de rede** com níveis de acesso distintos, e o edital pede a distinção:

- **Internet:** a rede **pública mundial** — acesso irrestrito de qualquer lugar. É onde ficam os **serviços públicos acessíveis a todos** (ex.: o site de consulta pública de benefícios).
- **Intranet:** a rede **privada interna** de uma organização — acessível apenas a membros da organização (ex.: os sistemas internos administrativos da DATAPREV). Não é acessível ao público.
- **Portal:** um **ponto único de entrada/agregação de serviços e informações** — normalmente na web (pode ser público ou corporativo), que **reúne** vários serviços/aplicações num lugar só para o usuário (ex.: um portal do servidor que centraliza benefícios, contracheque, solicitações).

| Ambiente | Acesso | Exemplo |
|---|---|---|
| **Internet** | público, mundial | site público de consulta |
| **Intranet** | privado, interno à organização | sistema administrativo interno |
| **Extranet** | privado, mas **estendido a parceiros** (bancos, órgãos) | integração com bancos parceiros |
| **Portal** | ponto único de entrada (pode ser público ou interno) | portal que centraliza serviços |

> [!warning] PEGADINHA — intranet vs. extranet vs. internet
> **Internet** = rede pública mundial. **Intranet** = rede **privada interna** da organização (só membros internos). **Extranet** = extensão da intranet **a parceiros externos autorizados** (ex.: bancos acessando um serviço de consignação). A banca troca: "a intranet é acessível ao público" — **falso**; "a extranet só é usada internamente" — **falso** (a extranet serve aos parceiros externos). E o **portal** é um **ponto de entrada/agregação**, não uma classificação de rede como as anteriores.

> [!note] O contexto DATAPREV
> A DATAPREV opera em rede, com sistemas internos na **intranet**, serviços de consulta pública na **internet**, integrações com bancos e órgãos via **extranet**, e **portais** (como o Meu INSS) que centralizam serviços para o cidadão e para o servidor. Saber em qual ambiente cada tipo de sistema vive é conhecimento prático de prova.

---

## 6. Como a FGV cobra este tópico

- **Gestão: os três estágios do Git:** working directory (edita) → staging (prepara via `git add`) → repository (grava via `git commit`).
- **Comandos:** `git init` (inicializa), `git add` (prepara), `git commit` (grava no histórico), `git push` (envia ao remoto), `git merge`/`git rebase` (integra), `git branch` (cria ramo).
- **Merge vs. rebase:** merge preserva histórico (commit de merge); rebase lineariza/reescreve.
- **Pull Request:** pedido de revisão e integração antes do merge.
- **CI/CD:** conceito de pipeline automatizado; Jenkins e GitHub Actions como ferramentas.
- **Docker:** imagem = template imutável; container = instância executável; container não inclui SO completo.
- **Ambientes:** internet (pública), intranet (privada interna), extranet (estendida a parceiros), portal (ponto de entrada).

> [!warning] PEGADINHA — as distinções que definem a nota
> (1) **git add** (prepara na staging) ≠ **git commit** (grava no histórico) ≠ **git push** (envia ao remoto). (2) **merge** (preserva/commit de merge) vs. **rebase** (lineariza/reescreve). (3) **imagem** (molde) vs. **container** (instância); container **não** tem SO completo. (4) **intranet** (interna) vs. **extranet** (parceiros) vs. **internet** (pública).

---

## 7. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **Git:** working directory → staging (`add`) → repository (`commit`)
> - [ ] `git init` (cria repositório), `git commit` (grava histórico), `git push` (envia remoto), `git pull` (traz remoto)
> - [ ] **Branch:** linha independente de desenvolvimento; `git branch` cria, `checkout/switch` troca
> - [ ] **Merge** (preserva histórico, commit de merge) vs. **Rebase** (histórico linear, reescreve)
> - [ ] **Pull Request:** pedido de revisão e integração
> - [ ] **CI/CD:** pipeline automatizado (build → teste → entrega); **Jenkins** e **GitHub Actions** = ferramentas
> - [ ] **Docker:** imagem (molde imutável) vs. container (instância executável); container compartilha o kernel, não tem SO completo
> - [ ] **Ambientes:** internet (pública) · intranet (privada interna) · extranet (parceiros) · portal (ponto de entrada)

> [!warning] O erro mais comum em prova
> Confundir **git add / commit / push** e confundir **merge / rebase**. E trocar **imagem por container** (ou achar que o container leva um SO completo). Na questão, pergunte: *essa ação prepara (add), registra (commit), envia (push) ou integra (merge/rebase)?* e *estou olhando para o modelo (imagem) ou para a instância rodando (container)?*

---

## 8. Fecho do Núcleo de Desenvolvimento

Com esta nota, você fecha a **FASE 4 — Núcleo de Desenvolvimento** do edital. Revisite o caminho percorrido: começamos no **POO** (os pilares, SOLID e Clean Code), passamos pelo **Java** e o ecossistema JVM, pelo **JavaScript** e as **frameworks Java** (Spring, Spring Boot, Spring Cloud, JSF, PrimeFaces), pelos **padrões de projeto e arquitetura** (GoF, MVC, SOA, Web Services, RESTful, OpenAPI), pelos **formatos de dados** (XML, XSD, XSLT, JSON, UDDI), pelo **mobile** (Android, iOS, low-code/no-code) e encerramos com o **DevOps e controle de versão** (Git, CI/CD, Docker, ambientes).

A ementa indica que os próximos blocos (**Metodologias** e **Testes de Software**) dependem deste. Para o estudo continuar no ritmo certo, lembre-se: o DevOps, o CI/CD e o controle de versão que você acabou de estudar são o **elo entre escrever código e entregar software** — e é exatamente sobre como esse processo é **gerenciado** (Scrum, Kanban, XP) que os blocos seguintes tratarão, já usando o vocabulário que você construiu aqui.
