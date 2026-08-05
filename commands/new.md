---
description: Registra um intent rapidamente, sem a entrevista completa do storm
argument-hint: <descrição curta do intent>
---

Registre um novo intent de forma rápida a partir de: $ARGUMENTS
(Se não houver argumento, peça uma descrição curta.)

Use o template de `${CLAUDE_PLUGIN_ROOT}/skills/intent-system/references/intent-template.md`.

Processo:

1. Localize a issue raiz (`gh issue list --label "intent:root" --state open`). Se não existir, oriente a rodar `/intent-system:init` e pare.

2. Preencha o que conseguir inferir da descrição e do código do repositório. Pergunte APENAS o essencial que não puder inferir — no máximo uma rodada de AskUserQuestion cobrindo: categoria, Purpose (por quê) e Outcome (resultado esperado). Não conduza entrevista longa; para isso existe `/intent-system:storm`.

3. Crie a issue com `gh issue create --title "[Intent] <nome>" --label "intent:node" --body-file <arquivo no scratchpad>`, com Parent apontando para a raiz, seções não discutidas preenchidas com o que for razoável e o restante marcado como Open Questions.

4. Adicione o intent à task-list da categoria correspondente na issue raiz (preservando o restante do corpo).

5. Informe número/URL e sugira: `/intent-system:storm` para aprofundar decisões, ou `/intent-system:slice #<n>` se já estiver claro o suficiente para fatiar.
