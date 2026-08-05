---
description: Mostra a árvore de intents e o estado de todos os packets
---

Monte um panorama do Intent-System neste repositório.

1. **Colete** (em paralelo):
   - Issue raiz: `gh issue list --label "intent:root" --state open --json number,title,body`
   - Intents: `gh issue list --label "intent:node" --state all --json number,title,state,labels --limit 100`
   - Packets: `gh issue list --label "intent:packet" --state all --json number,title,state,labels,body --limit 100`
   - Clarifications: `gh issue list --label "intent:clarification" --state open --json number,title`
   - PRs: `gh pr list --state open --search "intent/" --json number,title,url`

   Se não houver issue raiz, informe que o repo não foi inicializado (`/intent-system:init`) e pare.

2. **Apresente como árvore**, agrupando packets sob seus intents (use o `Intent: #n` do corpo do packet) e intents por categoria (task-lists da raiz). Para cada packet, mostre o estado pela label (`ready` / `in-progress` / `in-review` / `done`) com um marcador visual (por ex. ○ ◐ ◑ ●). Liste clarifications abertas em destaque no final.

3. **Feche com um resumo**: contagem por estágio e a sugestão de `/intent-system:next` para a recomendação de próxima ação.
