---
description: Encerra um packet após o merge do PR — labels, task-lists e próximo passo
argument-hint: [#PR ou #packet]
---

Faça o closeout de: $ARGUMENTS
(Se não houver argumento, procure PRs de packets recém-mesclados — `gh pr list --state merged --search "intent/" --limit 5` — e issues ainda em `intent:in-review`, e pergunte qual encerrar.)

Processo:

1. **Confirme o merge**: `gh pr view <pr> --json state,mergedAt,body`. Se o PR não estiver mesclado, informe o estado real e pare — closeout só após merge.

2. **Atualize o packet**:
   - Identifique a issue pelo `Closes #<n>` (o GitHub pode já tê-la fechado — tudo bem).
   - `gh issue edit <n> --remove-label "intent:in-review" --add-label "intent:done"`
   - Se ainda aberta: `gh issue close <n> --comment "Concluído via <URL do PR>."`

3. **Atualize o intent pai** (referenciado no cabeçalho do packet):
   - Marque `[x]` no item do packet na task-list da seção Packets (preserve o restante do corpo).
   - Avalie: o Outcome do intent foi totalmente alcançado?
     - **Sim** → proponha ao usuário fechar o intent; se aceito, feche com comentário resumindo os packets entregues e marque `[x]` na task-list da issue raiz.
     - **Não** → identifique o que falta.

4. **Relate e sugira o próximo passo**: packets restantes prontos (`/intent-system:implement`), próxima fatia a cortar (`/intent-system:slice #<intent>`), ou `/intent-system:next` para visão geral.
