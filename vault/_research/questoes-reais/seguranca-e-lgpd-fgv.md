# Segurança da Informação e LGPD — Questões Reais FGV

> Disciplinas: Segurança da Informação (Módulo II) e Legislação — Segurança da Informação e Proteção de Dados (Módulo I, 5 questões) · Banca: FGV · Evidências FGV 2024–2026.

> **Atenção (aderência ao edital 2026):** a seção de Segurança prevê políticas; procedimentos; ISO/IEC 27001:2022 e 27002:2022; tríade CID; mecanismos de segurança (controle de acesso, **OAuth2**, **SSO**); gerência de riscos; **SDL**; **OWASP Top 10**; **SAST/DAST**. Em Arquitetura Avançada constam **HTTPS, SSL/TLS**. VPN, FDE, TDE, rate limiting e JWT **não são citados** no edital — são relacionados, não explícitos.

## Questões reais localizadas

Classificação: **real** (todas as linhas abaixo). Sinalização: ✅ dentro · ⚠️ relacionado, não explícito · ❌ fora do programa.

| Ano | Concurso | Cargo | Tópico | Assunto cobrado | Edital 2026 | Referência |
|---|---|---|---|---|---|---|
| 2026 | MPE-ES | Engenheiro de Dados / Analista de Sistema | Segurança de APIs | Proteção de APIs com OAuth 2.0/JWT: token **não dispensa autorização**; medida adequada é **validação e saneamento de entradas**; rate limiting | ✅ Dentro (OAuth2 e controle de acesso previstos) | Questões Estratégicas — questão 22 / Gran Q4626557 |
| 2024 | INPE | Tecnologista Júnior — Ambientes Críticos TI | Protocolos | **TLS**: chave simétrica para confidencialidade + MAC para integridade | ✅ Dentro (HTTPS, SSL/TLS previstos) | Questões Estratégicas — questão 28 |
| 2024 | TCE PA | Auditor de Controle Externo — Analista de Sistemas | OWASP | OWASP: relacionar riscos × exemplos (Broken Access Control, Injection, Cryptographic Failures, Identification and Authentication Failures) | ✅ Dentro (OWASP Top 10) | Gran Questões — Q3379999 |
| 2026 | MPE-ES | Analista — Segurança da Informação | OWASP | OWASP Top 10:2025 — reconhecer técnica de exploração `../../etc/passwd` → **LFI** | ✅ Dentro (OWASP Top 10) | Gran Questões — Q4628833 |
| 2025 | AL-AM | Analista Legislativo Programador | Protocolos | Suporte a SSL 3.0/TLS 1.0/1.1 obsoletos → exposição a **POODLE e BEAST** — **B** | ✅ Dentro (SSL/TLS previstos; ataques derivam do tópico) | Questões Estratégicas — questão 58 |
| 2025 | — | — | OWASP | OWASP Top 10 (2021) — medidas contra injeção: APIs seguras parametrizadas, validação positiva no servidor (cláusula UNIQUE **não** é defesa) | ✅ Dentro (OWASP Top 10) | ResolvaMais — Q1842018 (FGV 2025) |
| 2026 | MPE-ES | Engenheiro de Dados | Criptografia | Estado dos dados: **repouso** (FDE, TDE, criptografia de disco) versus **trânsito** (HTTPS, VPN) — **B** | ⚠️ Relacionado (termos FDE/TDE/VPN não citados; deriva de mecanismos de segurança e SSL/TLS) | Questões Estratégicas — questão 32 |
| 2025 | TCE RR | Analista de TI — Banco de Dados | LGPD | Dados sensíveis e tratamento sem consentimento | ✅ Dentro (LGPD prevista na Legislação) | Gran Questões — FGV TCE RR 2025 |
| 2026 | AMAZUL | Analista de TI — Infraestrutura | ISO/IEC 27002 | Três pilares que formam a base da proteção de dados segundo a ISO/IEC 27002 → tríade **Confidencialidade, Integridade e Disponibilidade** | ✅ Dentro (27002 e CID previstos) | Magna Concursos — Q4024224 |
| — | FGV — CNS005 | Analista de TI — Segurança Cibernética e Proteção de Dados | ISO/IEC 27002 | Controle **organizacional** — preparação e planejamento de incidentes: propósito é garantir rapidez, eficácia, consistência e respostas ordenadas, incluindo comunicação (**E**) | ✅ Dentro | Prova oficial FGV — `ati-seguranca-cibernetica-e-protecao-de-dados-cns005-tipo-02.pdf`, questão 47 |
| — | FGV — CNS014 | Analista de Gestão de TI | ISO 27001/27002 × LGPD/GDPR | V/F sobre as normas + LGPD/GDPR (dados de saúde): I **inverte** as duas normas (falsa); II e III corretas — SGSI demonstra conformidade (**E**) | ✅ Dentro (27001/27002 e LGPD previstos) | Prova oficial FGV — `analista-de-gestao-tecnologia-da-informacaocns014-tipo-1.pdf`, questão 64 |
| 2024 | TJ RR | Analista — Área Cibersegurança | ISO 27001/27002/27005 | V/F: 27001 = requisitos do SGSI (V); 27002 orienta no cumprimento da **27001** (não da 27005); 27005 **não** estabelece requisitos de SGSI (é guia de riscos) | ✅ Dentro | Gran Questões — Q3517586 |
| 2024 | TJ RR | Analista — Gestão e Governança de TI | ISO 27002 | 93 controles em 4 temas (organizacionais, pessoas, físicos, tecnológicos); reconhecer os controles **organizacionais** | ✅ Dentro | Gran Questões — Q3517349 |
| 2026 | MPE-ES | Agente Técnico — TI | Controles físicos × lógicos | Classificação de controles na 27002:2022 — tokens **FIDO2** = controle lógico/tecnológico; **CFTV** = físico; senha é controle lógico; firewall é lógico — **E** | ✅ Dentro | Questões Estratégicas — questão 35 |
| 2026 | MPE-ES | Agente Técnico — Analista de Segurança | IAM / SSO / ABAC | V/F: provisionamento automatizado de acessos (V); **SSO não dispensa** auditoria e rastreabilidade (F); ABAC usa atributos como localização, horário, perfil e dispositivo (V) — **E** | ✅ Dentro (SSO e controle de acesso previstos) | Questões Estratégicas — questão 38 |
| 2025 | CGE SP | Auditor Estadual — Controle TI | SGSI / OIDC / continuidade | V/F: escopo do SGSI considera contexto e partes interessadas (V); RPO define perda de dados aceitável (⚠️ continuidade não explícita); **OIDC** = camada de identidade sobre **OAuth 2.0** (V) | ⚠️ Parcial (RPO não explícito) | Questões Estratégicas — prova CGE SP 2025 |

## Análise das questões principais

- **ISO 27001 × 27002 é o "pêndulo" da FGV (AMAZUL, CNS005, CNS014, TJ RR):** a 27001 especifica **requisitos do SGSI** (certificável); a 27002 é o **código de práticas com 93 controles** em 4 temas (organizacionais, pessoas, físicos, tecnológicos). Pegadinha clássica: **inverter** as duas ou atribuir à 27005 os requisitos do SGSI.
- **Tríade CID (AMAZUL 2026):** cobrada de forma literal a partir da ISO/IEC 27002 — Confidencialidade, Integridade e Disponibilidade. Cuidado: o edital grafa "Confiabilidade, Integridade e Disponibilidade" — na prova, o termo técnico é **Confidencialidade**.
- **IAM/SSO/ABAC (MPE-ES 2026):** pegadinha "SSO **dispensa** auditoria/rastreabilidade" é **falsa** — SSO centraliza a autenticação, mas auditoria continua obrigatória. ABAC autoriza por atributos (localização, horário, perfil, dispositivo).
- **Segurança de APIs (MPE-ES 2026):** alternativas que "dispensam" um mecanismo porque outro existe (OAuth/JWT dispensa autorização; tokens de longa duração; dispensar rate limiting) são **falsas**. Resposta tecnicamente correta: validação/saneamento de entradas.
- **OWASP:** a FGV cobra o Top 10 tanto por **relação risco × exemplo** quanto por **reconhecimento de técnica** (LFI com path traversal, SQLi, XSS).
- **TLS:** criptografia **simétrica** (confidencialidade) + **MAC** (integridade); chave pública apenas na troca de chaves/autenticação; SSL 3.0/TLS 1.0/1.1 → POODLE/BEAST.
- **Criptografia e estado dos dados:** HTTPS e VPN protegem **trânsito**; FDE (disco) e TDE (banco) protegem **repouso**. Pegadinha: "HTTPS protege dados em repouso" é falsa. Tema ⚠️ — termos não citados, conceito deriva de "mecanismos de segurança".
- **LGPD (TCE RR 2025) e ISO × LGPD/GDPR (CNS014):** base legal, dados sensíveis e a demonstração de conformidade por SGSI — ponte com as 5 questões de Legislação do Módulo I.

## Padrões de cobrança (observação)

1. **ISO 27001 × 27002** é o tema estrutural mais repetido (AMAZUL 2026, TJ RR 2024, CNS005, CNS014) e está **previsto no edital** — dominar a diferença (SGSI/requisitos × controles/código de práticas) e os 4 temas da 27002:2022.
2. **OWASP Top 10** (2021 e 2025) é frequente e **previsto** — relação risco × exemplo e reconhecimento de técnica de ataque.
3. Pegadinha recorrente: **alternativa que "dispensa" um controle de segurança** — quase sempre errada na FGV (SSO não dispensa auditoria; token não dispensa autorização).
4. **Mecanismos de segurança** (OAuth2, SSO, controle de acesso) com formato V/F sobre IAM — tópico expresso no edital.
5. **Protocolos e versões** (TLS/SSL) com ataques específicos (POODLE, BEAST) — previsto em Arquitetura Avançada.
6. **ISO × LGPD/GDPR:** a FGV conecta as normas de segurança à LGPD (dados de saúde, conformidade) — ponte direta com o Módulo I.
7. **Criptografia: estado dos dados (repouso/trânsito/uso)** é formato repetido (INPE e MPE-ES) — manter como apoio, por não estar explícito no edital.

> Lacuna de evidência restante (sugestão de pesquisa futura): tópicos do edital ainda sem questão completa localizada — **SDL** (Security Development Lifecycle) e **SAST/DAST** (aparecem no edital, sem enunciado FGV mapeado até aqui). A tríade CID, SSO, ISO 27001/27002 e OWASP agora têm evidência.

## Ligações com as notas

[[Fundamentos-de-Seguranca]] · [[Autenticacao-e-Autorizacao]] · [[Seguranca-de-Comunicacoes]] · [[Seguranca-no-Desenvolvimento]] · [[Gestao-de-Riscos]] · [[LGPD-Lei-Geral-de-Protecao-de-Dados]] · [[Lei-Carolina-Dieckmann]] · [[Marco-Civil-da-Internet]] · [[Lei-de-Acesso-a-Informacao-LAI]]