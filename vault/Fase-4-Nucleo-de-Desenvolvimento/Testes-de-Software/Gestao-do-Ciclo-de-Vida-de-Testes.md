# Gestão do Ciclo de Vida de Testes

> [!info] Metadados
> **Disciplina:** Testes de Software
> **Bloco:** 4.3 — Testes de Software (FASE 4 — Núcleo de Desenvolvimento)
> **Tópico:** 4. Gestão do Ciclo de Vida de Testes
> **Subtópicos:** Planejamento (plano de teste, casos de teste, dados de teste) · Execução (registro de defeitos, severidade e prioridade) · Relatórios (métricas: defeitos por fase, taxa de falha, MTBF)
> **Pré-requisitos:** [[Fundamentos-de-Teste|Fundamentos de Teste]] (níveis, tipos, estratégias) · [[Testes-Automatizados|Testes Automatizados]] (ferramentas, métricas de cobertura) · [[Metodologias-Ageis|Metodologias Ágeis]] (Scrum, sprints, processos)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-31

---

## 1. Por que estudar gestão do ciclo de vida de testes?

Você já domina os **fundamentos** ([[Fundamentos-de-Teste]]), os **métodos ágeis** ([[Testes-Ageis]]) e as **ferramentas** ([[Testes-Automatizados]]) de teste. Mas falta uma pergunta essencial: **como organizar todo esse conhecimento em um processo estruturado e gerenciável?**

Escrever testes sem gestão é como construir um prédio sem planta: cada pessoa faz o que quer, ninguém sabe o que já foi testado, e os defeitos escapam por falta de planejamento. A **gestão do ciclo de vida de testes** é o processo que transforma atividades isoladas de teste em um **sistema organizado, rastreável e mensurável**.

> [!question] Pergunta orientadora
> Se a DATAPREV precisa liberar uma nova regra de benefício para milhões de segurados, como você garante que os testes cobrem todos os cenários críticos? Como registra os defeitos encontrados? Como mede se o sistema está pronto para produção? A resposta está no **plano de teste**, no **registro de defeitos** e nas **métricas** — que são o coração deste tópico.

---

## 2. O processo de teste: as seis fases

O processo de teste segue uma sequência lógica de atividades, independentemente de ser ágil ou tradicional:

```mermaid
flowchart LR
    A["1. Planejamento\ndo Teste"] --> B["2. Análise e\nDesign"]
    B --> C["3. Implementação\ndos Casos"]
    C --> D["4. Execução\ndos Testes"]
    D --> E["5. Avaliação do\nCritério de Saída"]
    E --> F["6. Encerramento\ne Relatório"]
```

| Fase | O que acontece | Entregas principais |
|---|---|---|
| **1. Planejamento** | Define **escopo, estratégia, recursos e cronograma** dos testes | Plano de teste |
| **2. Análise e Design** | Analisa requisitos e **projeta** os casos de teste | Casos de teste, dados de teste |
| **3. Implementação** | **Codifica/automatiza** os casos de teste e prepara o ambiente | Scripts de teste, ambiente configurado |
| **4. Execução** | **Executa** os testes e registra resultados | Resultados, defeitos encontrados |
| **5. Avaliação do Critério de Saída** | Verifica se os **critérios de parada** foram atingidos | Decisão: liberar ou não |
| **6. Encerramento** | Produz o **relatório final**, lições aprendidas, encerra testes | Relatório de teste |

> [!question] Critérios de entrada vs. critérios de saída
> **Critérios de entrada** são as condições que devem ser verdadeiras **para começar** a testar (ex: "o módulo está implementado e os testes unitários passando"). **Critérios de saída** são as condições que devem ser verdadeiras **para parar** de testar e liberar (ex: "todos os testes críticos passando, nenhum defeito de severidade alta aberto, cobertura mínima de 80%"). A banca cobra a distinção: entrada = "posso começar?" · saída = "posso liberar?"

---

## 3. Plano de teste — o documento central

O **plano de teste** (test plan) é o documento que organiza **toda a estratégia de teste** de um projeto. Ele responde às perguntas: *o quê* testar, *como* testar, *quando* testar, *quem* testa, e *quando parar*.

### 3.1 Estrutura típica de um plano de teste

| Seção | Conteúdo |
|---|---|
| **Objetivo** | O que se pretende validar com os testes |
| **Escopo** | O que será testado (e o que **não** será) |
| **Estratégia** | Níveis e tipos de teste que serão aplicados |
| **Critérios de entrada** | Condições para começar a testar |
| **Critérios de saída** | Condições para liberar (ex: 0 defeitos altos, 80% cobertura) |
| **Recursos** | Ferramentas, ambiente, equipe |
| **Cronograma** | Datas e fases |
| **Riscos** | O que pode dar errado e como mitigar |
| **Entregas** | Relatórios, métricas, lições aprendidas |

> [!important] Plano de teste ≠ caso de teste
> O **plano de teste** é o documento **estratégico** — ele diz *como* o teste será organizado. O **caso de teste** é a especificação **tática** — ele diz *o que* exatamente será testado em um cenário específico. O plano contém centenas de casos de teste. É a diferença entre o "plano de campanha militar" e a "ordem de uma operação específica."

### 3.2 Dados de teste

Os **dados de teste** (test data) são os valores específicos usados para executar os casos de teste. Podem ser:

- **Dados reais** (extraídos de produção — cuidado com LGPD!);
- **Dados sintéticos** (gerados artificialmente);
- **Dados de borda** (boundary values) — valores nos limites aceitáveis;
- **Dados inválidos** — propositadamente incorretos para testar validação.

> [!note] Cuidado com dados reais em teste
> Em sistemas governamentais como os da DATAPREV, usar **dados reais de beneficiários** em ambiente de teste viola a [[LGPD|Lei Geral de Proteção de Dados]]. Por isso, os dados de teste devem ser **sintéticos** (fictícios, mas com formato válido). Essa restrição é um cenário real que a banca pode cobrar.

---

## 4. Caso de teste — a especificação detalhada

No [[Fundamentos-de-Teste|tópico 1]] introduzimos o conceito de caso de teste. Aqui, vamos detalhar sua **estrutura prática**:

### 4.1 Estrutura de um caso de teste

```text
Caso de Teste: CT-001
Título: Validar cálculo de benefício com tempo mínimo de contribuição
Objetivo: Verificar que o cálculo retorna o valor correto para 15 anos de contribuição
Pré-condições: Sistema inicializado, banco de dados com dados de teste
Dados de teste: AnosContribuicao = 15, SalarioBase = 2000.00
Passos:
  1. Acessar módulo de cálculo
  2. Informar 15 anos de contribuição
  3. Informar salário base de R$ 2.000,00
  4. Solicitar cálculo
Resultado esperado: Valor do benefício = R$ 30.000,00
Resultado real: [preenchido após execução]
Status: PASSOU / FALHOU / BLOQUEADO
```

### 4.2 Execução e registro

Após executar o caso de teste, o resultado é registrado:

| Status | Significado |
|---|---|
| **PASSOU (Pass)** | O resultado real **é igual** ao esperado |
| **FALHOU (Fail)** | O resultado real **é diferente** do esperado — **registrar defeito** |
| **BLOQUEADO (Blocked)** | O teste não pôde ser executado (dependência, ambiente, etc.) |
| **CANCELADO** | O teste não será mais executado (mudança de escopo) |

> [!question] O que fazer quando um teste falha?
> O primeiro passo é **registrar o defeito** (defect report) — documentar o que aconteceu, com detalhes suficientes para que o desenvolvedor consiga reproduzir e corrigir. É o que vamos ver agora.

---

## 5. Registro de defeitos (Defect Report)

Um **registro de defeito** (defect report / bug report) é o documento que descreve um defeito encontrado durante os testes. Deve ser **claro, completo e reprodutível**.

### 5.1 Estrutura de um defect report

| Campo | Conteúdo |
|---|---|
| **ID** | Identificador único (ex: BUG-042) |
| **Título** | Resumo do defeito (ex: "Cálculo de benefício retorna valor negativo") |
| **Descrição** | Detalhamento do problema |
| **Passos para reproduzir** | Sequência exata que gera o defeito |
| **Resultado esperado** | O que deveria acontecer |
| **Resultado obtido** | O que realmente aconteceu |
| **Severidade** | Impacto do defeito (ver seção 5.2) |
| **Prioridade** | Urgência de correção (ver seção 5.2) |
| **Ambiente** | SO, navegador, versão, configuração |
| **Evidência** | Prints, logs, capturas de tela |
| **Status** | Aberto → Em análise → Em correção → Resolvido → Fechado |
| **Responsável** | Quem irá corrigir |

### 5.2 Severidade vs. Prioridade — a pegadinha clássica

Essa é uma das **distinções mais cobradas** pela FGV:

| Conceito | O que mede | Exemplo |
|---|---|---|
| **Severidade** | O **impacto técnico** do defeito — o quanto ele afeta o sistema | Um bug que causa erro de 500 no servidor é **alta severidade** |
| **Prioridade** | A **urgência de correção** — o quanto o negócio pressiona por correção | Um erro de digitação no "Sobre" do sistema é **baixa prioridade** |

> [!warning] PEGADINHA — severidade ≠ prioridade
> Essa é a pegadinha mais clássica deste tópico. Um defeito pode ter **alta severidade** (causa crashes) mas **baixa prioridade** (ocorre em uma funcionalidade que ninguém usa — e será descontinuada). Outro pode ter **baixa severidade** (leve inconveniência) mas **alta prioridade** (afeta o processo de pagamento em massa no dia de pagamento de benefícios). **Severidade é técnica; prioridade é de negócio.** A banca troca os termos sistematicamente.

| Severidade | Descrição |
|---|---|
| **Crítica / Bloqueante** | Impede completamente o uso do sistema ou causa perda de dados |
| **Alta** | Funcionalidade principal afetada, sem workaround |
| **Média** | Funcionalidade secundária afetada, com workaround disponível |
| **Baixa** | Inconveniência menor, cosmético, sem impacto funcional |

| Prioridade | Descrição |
|---|---|
| **Urgente** | Corrigir imediatamente (bloqueia entrega ou produção) |
| **Alta** | Corrigir nesta sprint/ciclo |
| **Média** | Corrigir no próximo ciclo |
| **Baixa** | Corrigir quando houver tempo (não bloqueia nada) |

> [!question] cenário clássico da banca
> "Um bug causa erro 500 ao acessar uma página de ajuda pouco visitada. classifique a severidade e prioridade." Severidade: **Alta** (erro 500 = sistema indisponível naquela funcionalidade). Prioridade: **Baixa** (página de ajuda pouco visitada, não afeta negócio). Resposta: alta severidade, baixa prioridade.

---

## 6. Métricas e relatórios de teste

### 6.1 Métricas principais

| Métrica | O que mede | Como calcular |
|---|---|---|
| **Defeitos por fase** | Em que fase do ciclo o defeito foi introduzido | Rastrear o defeito até a fase onde o código foi escrito |
| **Taxa de falha (Failure Rate)** | Proporção de testes que falharam | `Falhas / Total de testes × 100` |
| **Densidade de defeitos** | Defeitos por unidade de tamanho (ex: por 1.000 linhas de código) | `Total de defeitos / (KLOC)` |
| **MTBF (Mean Time Between Failures)** | Tempo médio entre duas falhas consecutivas | `Tempo total de operação / Número de falhas` |
| **MTTR (Mean Time To Repair)** | Tempo médio para corrigir um defeito | `Tempo total de correção / Número de defeitos corrigidos` |
| **Cobertura de teste** | Percentual de requisitos/código coberto por testes | `Requisitos testados / Total de requisitos × 100` |
| **Taxa de reabertura** | Defeitos que retornam após terem sido corrigidos | `Defeitos reabertos / Total de defeitos corrigidos × 100` |

> [!note] MTBF e MTTR são mais comuns em governança
> MTBF e MTTR são frequentemente cobrados no contexto de [[Gestao-e-Governanca-de-TI|Gestão e Governança de TI]] (Bloco 6.2) e [[Seguranca-da-Informacao|Segurança da Informação]] (Bloco 6.1). Aqui, apresentamos as definições; a aplicação completa será vista nas fases futuras.

### 6.2 Relatório de teste

O **relatório de teste** (test summary report) é o documento que consolida os resultados de todos os testes executados. Ele inclui:

- **Resumo executivo** — visão geral (passou/falhou, defeitos encontrados);
- **Escopo dos testes** — o que foi testado e o que não foi;
- **Resultado por nível** — quantos testes unitários, integração, sistema e aceitação;
- **Defeitos encontrados** — total, por severidade, por fase;
- **Métricas** — cobertura, taxa de falha, MTBF;
- **Decisão** — o sistema está pronto para produção? (sim/não/com ressalvas);
- **Recomendações** — melhorias para os próximos ciclos.

> [!question] Relatório ≠ Plano de teste
> O **plano** é **antes** dos testes (define a estratégia). O **relatório** é **depois** dos testes (consolida resultados). São complementares: o plano diz "vamos testar assim"; o relatório diz "o resultado foi esse."

---

## 7. Defeitos por fase — a regra do custo crescente

Uma das métricas mais importantes (e cobradas) é a relação entre **fase em que o defeito é introduzido** e **fase em que é detectado**:

| Fase de introdução | Custo relativo de correção |
|---|---|
| Requisitos | 1x (barato — basta atualizar o documento) |
| Design | 5x |
| Codificação | 10x |
| Teste | 20x |
| Produção | 50x – 200x (caríssimo — correção + retrabalho + impacto ao usuário) |

> [!important] Por que testar cedo é mais barato
> Essa tabela é a justificativa para o princípio "teste precoce" do [[Fundamentos-de-Teste]]. Se um defeito de requisitos é detectado na fase de codificação, o custo é 10x maior. Se é detectado em produção (onde o INSS está pagando benefícios errados), o custo pode ser 200x — incluindo prejuízo financeiro, retrabalho e impacto à imagem da DATAPREV.

---

## 8. Como a FGV cobra gestão de testes

- **Severidade vs. prioridade** é o alvo mais rentável — sempre em cenários que exigem distinguir impacto técnico de urgência de negócio.
- **Plano de teste vs. caso de teste** aparece em questões que trocam os conceitos.
- **Critérios de entrada vs. saída** cai em perguntas sobre "quando começar/parar de testar."
- **Métricas (MTBF, taxa de falha)** aparecem em questões conceituais e de cálculo simples.
- **Custo crescente de defeitos** é cobrado como justificativa para testes precoces.

> [!warning] PEGADINHA — as cinco armadilhas mais rentáveis
> (1) **Severidade ≠ prioridade** — severidade é impacto técnico; prioridade é urgência de negócio. (2) **Caso de teste ≠ plano de teste** — caso é específico; plano é estratégico. (3) **Critério de saída ≠ critério de entrada** — saída = quando parar; entrada = quando começar. (4) **MTBF é tempo entre falhas, não tempo de falha** — não confunda com MTTR. (5) **Relatório é posterior; plano é anterior** — não troque os documentos.

---

## 9. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **Processo de teste:** planejamento → análise/design → implementação → execução → avaliação do critério de saída → encerramento
> - [ ] **Plano de teste:** documento estratégico (escopo, estratégia, recursos, cronograma, critérios de entrada/saída)
> - [ ] **Caso de teste:** especificação detalhada (ID, pré-condições, passos, resultado esperado/real, status)
> - [ ] **Dados de teste:** sintéticos (não reais, por LGPD) · incluem dados de borda e dados inválidos
> - [ ] **Defect report:** ID, título, descrição, passos para reproduzir, severidade, prioridade, evidências, status
> - [ ] **Severidade = impacto técnico** · **Prioridade = urgência de negócio** — NÃO são a mesma coisa
> - [ ] **Métricas:** defeitos por fase · taxa de falha · MTBF · MTTR · cobertura · densidade de defeitos
> - [ ] **Custo crescente:** defeito em produção = 50x–200x mais caro que em requisitos
> - [ ] **Plano ≠ caso ≠ relatório** — documentos com funções completamente diferentes

> [!question] Revise mentalmente
> Um defeito causa um erro visual na tela de boas-vindas do portal — mas não afeta nenhuma funcionalidade de cálculo de benefício. Qual a severidade e qual a prioridade? *(Resposta: Severidade Baixa (impacto cosmético); Prioridade Baixa (não afeta negócio). Mas se a página de boas-vindas for o primeiro contato com milhões de usuários e a imagem da empresa, a prioridade pode subir para Média — dependendo do contexto de negócio.)*

---

## 10. Próximos passos

Você agora domina o **processo** de teste: como planejar, executar, registrar e reportar. No próximo tópico — e último deste bloco — vamos estudar um tema que complementa a automação de testes mas tem objetivo diferente: a **RPA (Robotic Process Automation)** — robôs que automatizam processos de negócio, não testes de software. Veremos as diferenças fundamentais entre RPA e automação de testes.
