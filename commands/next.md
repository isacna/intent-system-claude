---
description: Analisa o estado do fluxo e recomenda a próxima ação
---

Analise o estado do fluxo Intent-System neste repositório e recomende a próxima ação.

1. **Colete o estado** (em paralelo):
   - `gh issue list --label "intent:clarification" --state open --json number,title`
   - `gh issue list --label "intent:in-review" --state open --json number,title`
   - `gh issue list --label "intent:in-progress" --state open --json number,title`
   - `gh issue list --label "intent:ready" --state open --json number,title`
   - `gh issue list --label "intent:node" --state open --json number,title`
   - `gh pr list --state open --search "intent/" --json number,title,url`

   Se a issue raiz não existir, recomende `/intent-system:init` e pare.

2. **Recomende pela prioridade** (a primeira condição verdadeira define a recomendação principal; mencione as demais como pendências):
   1. Clarifications abertas → resolvê-las bloqueia o resto: proponha decidir agora (ofereça conduzir com o formato do storm).
   2. PRs `intent:in-review` → `/intent-system:review <pr>` (ou merge + `/intent-system:closeout` se já aprovado).
   3. Packets `intent:in-progress` sem PR aberto → retomar ou destravar a implementação.
   4. Packets `intent:ready` → `/intent-system:implement #<n>`.
   5. Intents sem packets abertos → `/intent-system:slice #<n>`.
   6. Nada aberto → `/intent-system:storm` para capturar o próximo intent.

3. **Responda** com um resumo curto do estado (contagens por estágio) e UMA recomendação principal com o comando pronto para copiar.
