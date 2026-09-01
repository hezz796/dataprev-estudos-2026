# Segurança da Informação — Questões Autorais Comentadas

> **Disciplina:** Segurança da Informação · **Bloco:** 6.1 — Segurança da Informação (FASE 6 — Segurança e Governança)
> **Banca de referência:** FGV · **Formato:** alternativas A–E
> **Origem:** autoral (todas) · **Não são questões oficiais de banca.**

**Tópicos cobertos:** (a) Fundamentos de Segurança — tríade CID e ISO 27001/27002; (b) Autenticação e Autorização — OAuth2, OpenID Connect e JWT; (c) Gestão de Riscos — avaliação, matriz probabilidade × impacto e planos de contingência; (d) Segurança no Desenvolvimento — SDL, OWASP Top 10 e SAST/DAST; (e) Governança de segurança — SGSI, política de segurança e LGPD em contexto de incidentes.

---

## Questão 01 — Fundamentos da Segurança (Tríade CID e ISO 27001/27002)

**id:** SEG-001
**disciplina:** Segurança da Informação
**tópico:** Fundamentos de Segurança
**subtópico:** Tríade CID; ISO 27001/27002 (estrutura, controles); classificação da informação
**origem:** autoral
**habilidade cognitiva:** análise
**dificuldade:** fácil-média
**conhecimento avaliado:** composição exata da tríade CID; diferença estrutural entre ISO 27001 (requisitos/SGSI/certificável) e ISO 27002 (código de práticas/controles); classificação da informação como etapa anterior às proteções

Em uma auditoria de segurança do sistema de benefícios, um analista da DATAPREV revisa os conceitos fundamentais de segurança da informação. Considere as afirmativas abaixo:

I. Na tríade CID, os três pilares fundamentais da segurança da informação são Confidencialidade, Autenticidade e Disponibilidade.

II. A ISO/IEC 27002 é um código de práticas que detalha os controles de segurança da informação, servindo de guia para a implementação dos controles que a ISO/IEC 27001 referencia em seu Anexo A.

III. A ISO/IEC 27001 especifica requisitos para estabelecer, implementar, manter e melhorar continuamente um Sistema de Gestão da Segurança da Informação (SGSI), sendo a norma passível de certificação.

IV. A classificação da informação precede a definição das proteções: o nível adequado de confidencialidade, integridade e disponibilidade só pode ser decidido depois de conhecer a sensibilidade do dado.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I e II
B) I, II e III
C) III e IV
D) II, III e IV
E) Apenas I

---

**Gabarito:** D

### Comentário

**Raciocínio:** A questão combina as duas pegadinhas estruturais mais repetidas da FGV em fundamentos: a composição exata da tríade CID e a diferença entre ISO 27001 e ISO 27002. É preciso avaliar cada afirmativa com precisão terminológica — e lembrar que o edital grafa "Confiabilidade, Integridade e Disponibilidade", mas o termo técnico correto é **Confidencialidade**.

**Palavra-chave:** tríade CID = Confidencialidade, **Integridade**, Disponibilidade; ISO 27001 = requisitos/SGSI/certificável; ISO 27002 = controles/código de práticas (Anexo A); classificação antes das proteções

**Conceito:**
- **Afirmativa I é falsa.** O segundo pilar da tríade é **Integridade**, não Autenticidade. Autenticidade (e não repúdio) são complementos que alguns autores agregam à tríade — mas a ementa e a FGV cobram a tríade clássica: **Confidencialidade, Integridade e Disponibilidade**.
- **Afirmativa II é verdadeira.** A **ISO/IEC 27002** é o **código de práticas** para controles de segurança: detalha o objetivo e as diretrizes de implementação de cada controle, servindo de apoio para aplicar os controles que a 27001 referencia (sem detalhar) no **Anexo A**. Não é certificável.
- **Afirmativa III é verdadeira.** A **ISO/IEC 27001** é a norma de **requisitos do SGSI** (Sistema de Gestão da Segurança da Informação), opera em ciclo **PDCA** de melhoria contínua e é a norma **certificável** — por um organismo acreditado.
- **Afirmativa IV é verdadeira.** A **classificação da informação** (rotular dados por sensibilidade/impacto) é **pré-requisito** para definir quem acessa e que proteção aplicar: sem saber o quão sensível é o dado, não se decide a intensidade da confidencialidade, integridade e disponibilidade exigida.

**Análise das alternativas:**
- **A (I e II):** errada — inclui I (falsa).
- **B (I, II e III):** errada — inclui I (falsa).
- **C (III e IV):** errada — II também é verdadeira.
- **D (II, III e IV):** correta — apenas I é falsa.
- **E (Apenas I):** errada — I é falsa e II, III e IV são verdadeiras.

**Pegadinha:** A afirmativa I é a armadilha clássica: trocar **Integridade** por **Autenticidade** dá um ar de "conceito avançado" que parece plausível — mas é falso. Atenção também à grafia do edital ("Confiabilidade"): na prova, o termo técnico é **Confidencialidade** (evidência FGV/AMAZUL 2026). E, quando a questão mencionar **SGSI** ou **certificação**, a resposta é **27001**; quando mencionar **controles** ou **boas práticas de implementação**, é **27002** — inverteu, errou.

---

## Questão 02 — Autenticação e Autorização (OAuth2, OpenID Connect e JWT)

**id:** SEG-002
**disciplina:** Segurança da Informação
**tópico:** Autenticação e Autorização
**subtópico:** OAuth2 (Authorization Code + PKCE, Client Credentials); OpenID Connect; JWT (estrutura e assinatura)
**origem:** autoral
**habilidade cognitiva:** análise
**dificuldade:** média-alta
**conhecimento avaliado:** fluxos do OAuth2 (papel do authorization code e do back-channel; PKCE; Client Credentials como M2M); OAuth2 × OpenID Connect (autorização × autenticação); estrutura do JWT (payload legível em Base64Url; assinatura garante integridade, não confidencialidade)

Um portal de consulta de benefícios precisa integrar-se a uma API do INSS em nome dos cidadãos. A equipe avalia os protocolos e formatos de token a adotar. Considere as afirmativas abaixo:

I. No fluxo Authorization Code do OAuth2, o access token não trafega pelo navegador do usuário: o client troca o authorization code pelo token por meio de um canal de servidor para servidor (back-channel); para aplicações mobile e SPAs, o fluxo é reforçado com PKCE, que impede o uso do code interceptado sem o code verifier.

II. No fluxo Client Credentials, um usuário final precisa autenticar e autorizar o client antes de ele obter o access token para acessar recursos em seu nome.

III. O OpenID Connect é uma camada de identidade construída sobre o OAuth2, que acrescenta um ID Token, em geral um JWT, com informações do usuário autenticado — enquanto o OAuth2 autoriza, o OpenID Connect autentica.

IV. Como o payload do JWT é assinado e codificado em Base64Url, o conteúdo das claims fica criptografado, de modo que somente o servidor que emitiu o token pode lê-lo.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I e II
B) I e III
C) II e III
D) I, II e III
E) II e IV

---

**Gabarito:** B

### Comentário

**Raciocínio:** A questão testa os dois pontos que a ementa exige em OAuth2 — a diferença entre os fluxos Authorization Code e Client Credentials —, além da relação OAuth2 × OpenID Connect e da natureza do JWT. Cada afirmativa deve ser julgada pela função de cada protocolo: **autorizar** (OAuth2) ou **autenticar** (OIDC).

**Palavra-chave:** Authorization Code = code → token em back-channel; PKCE = code verifier; Client Credentials = máquina a máquina, sem usuário; OIDC = camada de identidade sobre OAuth2 (ID Token); JWT = Base64Url não é criptografia

**Conceito:**
- **Afirmativa I é verdadeira.** No **Authorization Code**, o `authorization code` (curta duração) é entregue ao client via navegador, mas a troca por **access token** ocorre em **back-channel** (servidor para servidor) — o token nunca passa pelo navegador. O **PKCE** (code verifier/code challenge) protege principalmente **mobile e SPAs**, que não conseguem guardar um segredo de client.
- **Afirmativa II é falsa.** O **Client Credentials** é o fluxo **máquina a máquina (M2M)**: o client apresenta as **próprias credenciais** (client id + client secret) e recebe o token **sem qualquer usuário final** — não há redirecionamento nem autorização de usuário. A descrição de "usuário que autentica e autoriza" é do **Authorization Code**.
- **Afirmativa III é verdadeira.** O **OpenID Connect** constrói uma camada de **identidade sobre o OAuth2**: além do access token, entrega um **ID Token** (em geral JWT) com dados do usuário autenticado. OAuth2 **autoriza**; autenticação (identidade) é papel do **OIDC**.
- **Afirmativa IV é falsa.** O JWT é **ASSINADO, não criptografado**: header e payload são apenas codificados em **Base64Url**, codificação **reversível** — qualquer um pode **decodificar e ler** as claims. A assinatura garante **integridade e autenticidade** (o token não foi alterado e veio de quem o assinou), **não confidencialidade**. Para confidencialidade, usar-se-ia **JWE** (JSON Web Encryption).

**Análise das alternativas:**
- **A (I e II):** errada — II é falsa.
- **B (I e III):** correta — apenas I e III são verdadeiras.
- **C (II e III):** errada — II é falsa.
- **D (I, II e III):** errada — inclui II (falsa).
- **E (II e IV):** errada — ambas falsas.

**Pegadinha:** Esta questão condensa três inversões clássicas da FGV: (1) **Client Credentials com usuário** — falso; fluxo com usuário interagindo é Authorization Code; (2) **OAuth2 como autenticação** — falso; é autorização, quem autentica é o OpenID Connect; (3) **JWT criptografado** — falso; Base64Url é codificação legível, a assinatura não esconde o conteúdo. Para o JWT, guarde: **decodificar ≠ descriptografar**.

---

## Questão 03 — Gestão de Riscos (Avaliação, Matriz e Planos)

**id:** SEG-003
**disciplina:** Segurança da Informação
**tópico:** Gestão de Riscos
**subtópico:** Identificação e avaliação de riscos; matriz probabilidade × impacto; tratamento de riscos; contingência e recuperação
**origem:** autoral
**habilidade cognitiva:** compreensão e análise
**dificuldade:** média
**conhecimento avaliado:** definição de risco (ameaça + vulnerabilidade + impacto); função da matriz de risco (classificar/priorizar); distinção entre mitigar e transferir; distinção entre plano de contingência e plano de recuperação

Uma equipe de segurança da DATAPREV está conduzindo o processo de gestão de riscos dos sistemas de benefícios. Considere as afirmativas abaixo:

I. Risco é a possibilidade de ocorrência de um evento indesejado com impacto sobre a informação; ele resulta da combinação de ameaça, vulnerabilidade e impacto, de modo que a existência isolada de uma vulnerabilidade não configura, por si só, risco relevante.

II. A matriz de risco cruza probabilidade e impacto para classificar e priorizar riscos; um risco com probabilidade alta e impacto alto ocupa a célula mais crítica e exige tratamento prioritário, normalmente por mitigação.

III. Transferir um risco significa reduzir a probabilidade de o evento ocorrer por meio da aplicação de controles técnicos, como criptografia e backups.

IV. O plano de contingência visa restaurar sistemas e dados ao estado normal após o incidente; já o plano de recuperação mantém as operações funcionando em modo reduzido durante a interrupção.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) II e III
B) I, II e IV
C) I e II
D) I, II e III
E) Apenas II

---

**Gabarito:** C

### Comentário

**Raciocínio:** A questão avalia o vocabulário central da gerência de riscos — o que é risco, o que a matriz faz, e as quatro estratégias de tratamento — e termina com a confusão clássica entre contingência e recuperação. A palavra-chave é identificar **quem faz o quê** em cada conceito.

**Palavra-chave:** risco = ameaça + vulnerabilidade + impacto; matriz = probabilidade × impacto; mitigar = reduzir (controles); transferir = deslocar responsabilidade (seguro); contingência = continuar operando; recuperação = restaurar ao normal

**Conceito:**
- **Afirmativa I é verdadeira.** **Risco** é a possibilidade de um evento indesejado causar impacto; ele depende da combinação de **ameaça** (fator externo), **vulnerabilidade** (fragilidade interna) e **impacto** (consequência). Uma vulnerabilidade que nenhuma ameaça alcança (ex.: sistema legado sem conexão externa) não gera risco relevante — **vulnerabilidade ≠ risco**.
- **Afirmativa II é verdadeira.** A **matriz de risco** organiza a avaliação cruzando **probabilidade × impacto**; a célula resultante indica o nível de risco (baixo, médio, alto, extremo) e orienta a **priorização**. Probabilidade alta + impacto alto = nível extremo = ação prioritária de mitigação.
- **Afirmativa III é falsa.** Aplicar controles (criptografia, backups) para reduzir probabilidade ou impacto é **mitigar**. **Transferir** é **deslocar a responsabilidade/consequência** para outra parte — o exemplo típico é o **seguro** de cibersegurança; não reduz a chance nem o dano.
- **Afirmativa IV é falsa.** Os termos estão **invertidos**: o **plano de contingência** mantém as operações **funcionando** (total ou parcialmente, em modo reduzido) durante a interrupção; o **plano de recuperação** (de desastres) **restaura** sistemas e dados ao estado normal **depois** do incidente.

**Análise das alternativas:**
- **A (II e III):** errada — III é falsa.
- **B (I, II e IV):** errada — IV é falsa.
- **C (I e II):** correta — apenas I e II são verdadeiras.
- **D (I, II e III):** errada — inclui III (falsa).
- **E (Apenas II):** errada — I também é verdadeira.

**Pegadinha:** As afirmativas III e IV trazem as duas trocas mais cobradas da FGV neste tópico: **transferir ≠ mitigar** (transferir desloca a consequência, não reduz o risco) e **contingência ≠ recuperação** (operar durante × restaurar depois). Guarde também: **aceitar** não é ignorar — é decisão documentada de conviver com risco (geralmente baixo); **evitar** é eliminar a atividade de risco.

---

## Questão 04 — Segurança no Desenvolvimento (SDL, OWASP e SAST/DAST)

**id:** SEG-004
**disciplina:** Segurança da Informação
**tópico:** Segurança no Desenvolvimento
**subtópico:** SDL (Security Development Lifecycle); OWASP Top 10 (Injection, XSS); SAST × DAST
**origem:** autoral
**habilidade cognitiva:** análise
**dificuldade:** média
**conhecimento avaliado:** SDL e princípio de shift-left; distinção SAST (estático, sem executar, usa código-fonte) × DAST (dinâmico, em execução, caixa-preta); SQL Injection e sua defesa; distinção Injection × XSS

Um desenvolvedor da DATAPREV está revisando o ciclo de desenvolvimento de uma aplicação web que consulta dados previdenciários. Considere as afirmativas abaixo:

I. O SDL (Security Development Lifecycle) distribui atividades de segurança ao longo de todas as fases do desenvolvimento — do design à operação —, materializando a ideia de shift-left, isto é, antecipar a segurança para as etapas iniciais do ciclo.

II. O SAST analisa o código-fonte sem executar a aplicação e costuma ser aplicado durante o desenvolvimento; o DAST testa a aplicação em execução, de fora (caixa-preta), sem depender do código-fonte.

III. A SQL Injection ocorre quando dados fornecidos pelo usuário são interpretados como código pela aplicação, como na concatenação direta de strings em consultas SQL; a defesa clássica é o uso de consultas parametrizadas (prepared statements).

IV. O XSS (Cross-Site Scripting) ocorre quando a entrada fornecida pelo usuário é interpretada como comando no banco de dados; já a SQL Injection executa scripts maliciosos no navegador da vítima.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I, II e III
B) I e II
C) II, III e IV
D) I, II e IV
E) Apenas III

---

**Gabarito:** A

### Comentário

**Raciocínio:** A questão combina o ciclo de desenvolvimento seguro (SDL), a comparação SAST × DAST — a "pegadinha estrutural" mais clássica do tópico — e duas vulnerabilidades do OWASP Top 10 que a FGV adora diferenciar: Injection e XSS. A chave está em associar cada ataque ao **local do efeito**.

**Palavra-chave:** SDL = segurança em todas as fases + shift-left; SAST = estático/sem executar/código-fonte; DAST = dinâmico/em execução/caixa-preta; SQL Injection = banco/servidor; XSS = navegador da vítima

**Conceito:**
- **Afirmativa I é verdadeira.** O **SDL** insere práticas de segurança em **todas as fases** (requisitos/design → codificação → testes → implantação → pós-lançamento), em vez de tratar segurança como etapa final. O **shift-left** é exatamente isso: mover a segurança (e testes) para o **início** do ciclo.
- **Afirmativa II é verdadeira.** **SAST** (*Static* Application Security Testing) analisa o **código-fonte sem executar** — típico do desenvolvimento/CI, perspectiva "de dentro" (caixa-branca). **DAST** (*Dynamic* Application Security Testing) ataca a aplicação **em execução**, de fora, como um atacante (caixa-preta), **sem precisar do código-fonte**.
- **Afirmativa III é verdadeira.** **SQL Injection**: a entrada do usuário é tratada como **código SQL** pela aplicação (ex.: concatenação de strings), permitindo ler/alterar dados do banco. A defesa clássica é **consultas parametrizadas** (prepared statements), que separam dados de comando.
- **Afirmativa IV é falsa.** Os efeitos estão **invertidos**: o **XSS** ocorre quando a aplicação insere **conteúdo do usuário sem sanitização** em uma página, permitindo executar **JavaScript no navegador da vítima** (roubo de sessão, cookies). A **SQL Injection** age no **banco/servidor**, não no navegador.

**Análise das alternativas:**
- **A (I, II e III):** correta — apenas IV é falsa.
- **B (I e II):** errada — III também é verdadeira.
- **C (II, III e IV):** errada — IV é falsa.
- **D (I, II e IV):** errada — IV é falsa.
- **E (Apenas III):** errada — I e II também são verdadeiras.

**Pegadinha:** A afirmativa IV é a armadilha mais rentável: inverte **Injection** e **XSS**. Aliado à comparação SAST × DAST, o candidato precisa de dois mnemônicos: **S**tático → **S**ource (código); **D**inâmico → em execução. E para os ataques: **Injection = servidor/banco**; **XSS = navegador da vítima**. Observação pedagógica: a afirmativa sobre Broken Auth/Access Control (acessar painel administrativo alterando a URL) e o CSRF não foram incluídas nesta questão por priorização — CSRF ainda não consta das notas estudadas do tópico, e o princípio do projeto é não avaliar conhecimento antes de o aluno ter condições de estudá-lo.

---

## Questão 05 — Governança de Segurança (SGSI, Política de Segurança e LGPD em Incidentes)

**id:** SEG-005
**disciplina:** Segurança da Informação
**tópico:** Governança de segurança
**subtópico:** SGSI (ISO 27001); Política de Segurança da Informação (conceito); LGPD em contexto de incidentes
**origem:** autoral
**habilidade cognitiva:** compreensão e análise
**dificuldade:** média
**conhecimento avaliado:** papel estratégico da Política de Segurança da Informação; caráter contínuo do SGSI (PDCA e melhoria contínua); dever de comunicação de incidentes à ANPD e aos titulares (LGPD); certificação ISO 27001 como evidência, não substituta das obrigações de segurança

Em uma reunião de governança, a diretoria da DATAPREV discute o alinhamento entre a gestão de segurança e a proteção de dados pessoais. Considere as afirmativas abaixo:

I. A Política de Segurança da Informação (PSI) é o documento de nível estratégico, aprovado pela alta direção, que expressa as intenções e as diretrizes gerais da organização quanto à segurança da informação; normas e procedimentos operacionais derivam dela.

II. O SGSI estabelecido conforme a ISO 27001 opera em ciclo de melhoria contínua e tem como ponto de partida a análise de riscos, que orienta a seleção dos controles aplicáveis; após a certificação, o processo se encerra.

III. No contexto da LGPD, quando ocorre incidente de segurança que possa acarretar risco ou dano relevante aos titulares, o controlador deve comunicar o incidente à ANPD e aos titulares.

IV. A obtenção de certificação ISO 27001 dispensa a organização de adotar medidas de segurança para o tratamento de dados pessoais, pois o selo substitui as obrigações técnicas previstas na LGPD.

Está(ão) correta(s) apenas a(s) afirmativa(s):

A) I e II
B) I e III
C) III e IV
D) I, III e IV
E) II, III e IV

---

**Gabarito:** B

### Comentário

**Raciocínio:** A questão fecha o bloco com o nível de governança: o papel da política de segurança, o funcionamento do SGSI e a ponte entre a norma ISO e a LGPD quando um incidente ocorre. O fio condutor é: **a certificação é evidência de conformidade, nunca substituta das obrigações legais.**

**Palavra-chave:** PSI = estratégico/alta direção; SGSI = PDCA contínuo (análise de riscos); LGPD = comunicação de incidente à ANPD e titulares; ISO 27001 = evidência, não dispensa

**Conceito:**
- **Afirmativa I é verdadeira.** A **Política de Segurança da Informação (PSI)** é o documento **mais estratégico**, aprovado pela **alta direção**, com intenções e diretrizes gerais (quem acessa o quê, responsabilidades, tratamento de dados sensíveis). Normas (regras obrigatórias), procedimentos (passo a passo) e ferramentas derivam dela — sem a política, as demais camadas ficam sem direção.
- **Afirmativa II é falsa.** A **análise de riscos** (que já era o ponto de partida da ISO 27001) e o **ciclo PDCA** (Planejar–Fazer–Verificar–Agir) mostram que o SGSI é um processo **contínuo e realimentado**: a certificação atesta conformidade em um momento, mas **não encerra** o ciclo — o SGSI deve ser **mantido e melhorado continuamente**.
- **Afirmativa III é verdadeira.** A LGPD impõe, em caso de incidente de segurança que possa acarretar **risco ou dano relevante** aos titulares, a **comunicação à ANPD e aos titulares** pelo **controlador** — além das medidas de mitigação/remediação. É o elo direto entre segurança técnica e obrigação legal que o edital explora.
- **Afirmativa IV é falsa.** A certificação **ISO 27001/27002** é uma forte **evidência** de que a organização adota medidas de segurança (útil perante a ANPD e em auditorias), mas a LGPD **não prescreve tecnologia nem admite "substituição"** das obrigações por selos — o padrão "dispensar um mecanismo porque outro existe" é quase sempre falso na FGV.

**Análise das alternativas:**
- **A (I e II):** errada — II é falsa.
- **B (I e III):** correta — apenas I e III são verdadeiras.
- **C (III e IV):** errada — IV é falsa.
- **D (I, III e IV):** errada — IV é falsa.
- **E (II, III e IV):** errada — II e IV são falsas.

**Pegadinha:** Duas armadilhas: (1) "o SGSI se **encerra** após a certificação" — falso; o ciclo PDCA é contínuo, e a análise de riscos realimenta o processo; (2) "certificação ISO **dispensa** medidas/obrigações LGPD" — falso; a norma é caminho de evidência, não atalho que elimine deveres legais. Lembre: **política é estratégica; norma é obrigatória; procedimento é passo a passo — e certificação não substitui lei.**

---

## Padrões de cobrança utilizados

As questões autorais acima foram inspiradas nos seguintes padrões de cobrança identificados nas questões reais FGV (sem copiá-las):

1. **Julgamento de afirmativas (V/F)** — formato clássico da FGV em segurança, com uma ou duas falsas sutis (TJ RR 2024, CNS014, MPE-ES 2026). Inspiração estrutural para todas as questões.
2. **ISO 27001 × 27002 como "pêndulo" estrutural** — a 27001 é requisitos/SGSI/certificável; a 27002 é código de práticas/controles (AMAZUL 2026, TJ RR 2024, CNS005, CNS014). Inspiração para SEG-001 e SEG-005.
3. **Tríade CID cobrada de forma literal** — composição exata Confidencialidade, Integridade e Disponibilidade; pegadinha de trocar o segundo pilar (AMAZUL 2026; edital grafa "Confiabilidade"). Inspiração para SEG-001.
4. **OAuth2 com foco nos fluxos** — Authorization Code (com usuário, code → token) × Client Credentials (máquina a máquina, sem usuário); PKCE para mobile/SPA (ênfase explícita da ementa; evidências FGV 2026 em IAM/segurança de APIs). Inspiração para SEG-002.
5. **OAuth2 × OpenID Connect** — autorização × autenticação; OIDC como camada de identidade sobre OAuth2 (CGE SP 2025). Inspiração para SEG-002.
6. **JWT não é criptografia** — payload legível em Base64Url; assinatura dá integridade/autenticidade, não confidencialidade (padrão recorrente FGV em segurança de APIs; JWT consta da ementa do Bloco 6.1). Inspiração para SEG-002.
7. **Matriz probabilidade × impacto e tratamento de riscos** — mitigar/transferir/aceitar/evitar; contingência × recuperação — padrão conceitual FGV em gerência de riscos. Inspiração para SEG-003.
8. **OWASP Top 10 — relação risco × exemplo** — reconhecimento de ataques pela descrição (TCE PA 2024, FGV 2025, AL-AM 2025); e **SDL/SAST/DAST** previstos no edital (nota de pesquisa: ainda sem enunciado FGV mapeado — lacuna de evidência). Inspiração para SEG-004.
9. **Alternativa "dispensa um controle porque outro existe" quase sempre falsa** — "SSO dispensa auditoria", "token dispensa autorização" (MPE-ES 2026; padrão transversal da banca). Inspiração para SEG-005.
10. **ISO × LGPD** — SGSI como evidência de conformidade com o dever de segurança da LGPD (CNS014). Inspiração para SEG-005.

**Exclusões deliberadas:** VPN/FDE/TDE são ⚠️ relacionados no edital — não cobrados. CSRF ainda não consta das notas estudadas do tópico de Segurança no Desenvolvimento — não avaliado, por princípio pedagógico (não cobrar antes de estudar). Legislação em profundidade (LGPD) não foi cobrada; apenas o contexto de incidentes, que é ponte direta entre o Bloco 6.1 e o Módulo I.