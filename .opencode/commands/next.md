---
description: "Identifica e executa a próxima etapa pedagógica válida."
agent: coordinator
---

Determine qual é a próxima etapa válida da produção pedagógica.

Não peça ao usuário informações que possam ser obtidas a partir dos artefatos existentes.

Analise:

1. ementa;
2. disciplinas;
3. tópicos;
4. subtópicos;
5. notas existentes;
6. pré-requisitos;
7. auditorias;
8. questões e simulados quando relevantes.

Determine:

```text
último ponto concluído
→ dependências satisfeitas
→ próxima unidade válida
→ agente responsável
```

Depois:

1. execute a próxima etapa;
2. mantenha a ordem pedagógica;
3. não recrie conteúdo existente;
4. não ultrapasse pré-requisitos;
5. salve o resultado no vault;
6. valide o resultado quando necessário.

Se a próxima etapa exigir intervenção do usuário, pare e explique o motivo.

Ao final, informe:

- o que foi executado;
- quais arquivos foram criados ou alterados;
- estado da etapa;
- próxima etapa disponível.