---
name: text-quality-review
description: "Define critérios para detectar e corrigir erros ortográficos, caracteres indevidos e corrupção textual em materiais Markdown."
---

# Text Quality Review

## Objetivo

Garantir a integridade linguística e textual dos arquivos produzidos pelo OpenCode.

## Verificações

Procure:

- ortografia;
- acentuação;
- pontuação;
- palavras deformadas;
- caracteres asiáticos inesperados;
- caracteres Unicode estranhos;
- palavras truncadas;
- duplicações;
- problemas de espaçamento;
- Markdown quebrado.

## Caracteres suspeitos

O idioma padrão do vault é português brasileiro.

Caracteres de outros sistemas de escrita somente devem permanecer quando forem semanticamente necessários.

Nunca remova automaticamente um caractere apenas por pertencer a outro alfabeto.

## Preservação

Não altere:

- significado;
- conteúdo técnico;
- estrutura pedagógica;
- Wiki Links;
- callouts;
- fluxogramas;
- código;
- frontmatter.

## Correção mínima

Prefira:

```text
correção pontual
```

em vez de:

```text
reescrita completa
```

## Resultado

O texto final deve parecer produzido originalmente em português brasileiro, sem sinais evidentes de corrupção ou geração textual defeituosa.