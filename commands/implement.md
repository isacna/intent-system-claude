---
description: Implementa um packet pronto — branch, código, verificação e PR
argument-hint: [#issue do packet]
---

Implemente o packet: $ARGUMENTS
(Se não houver argumento, liste os prontos — `gh issue list --label "intent:ready" --state open` — e pergunte qual implementar; se houver só um, proponha-o.)

Máquina de estados em `${CLAUDE_PLUGIN_ROOT}/skills/intent-system/references/labels.md`.

**Regra central do IDD**: durante a implementação, sua única fonte de verdade é o corpo da issue do packet + o código do repositório. NÃO leia o intent pai, a issue raiz nem outras issues — se o contrato for insuficiente, isso é um defeito do packet: pare, reporte o que falta e sugira corrigir o contrato via novo `/intent-system:slice`.

Processo:

1. **Pegue o contrato**: `gh issue view <n>` — confirme que tem label `intent:ready`. Se não tiver, explique o estado atual e pare.

2. **Assuma o trabalho**:
   - `gh issue edit <n> --remove-label "intent:ready" --add-label "intent:in-progress"`
   - Crie o branch a partir do branch padrão atualizado: `git checkout -b intent/<n>-<slug-curto>`

3. **Implemente** seguindo Scope, Technical guidance e Constraints do contrato. Respeite o que está marcado como fora de escopo. Siga os padrões do código existente.

4. **Verifique**: execute os Verification steps do contrato e confira cada Acceptance criterion. Se algum falhar, corrija antes de prosseguir. Reporte resultados reais.

5. **Abra o PR**:
   - Commits com mensagens claras; `git push -u origin <branch>`
   - `gh pr create` com título espelhando o packet e corpo contendo: resumo do que foi feito, checklist dos acceptance criteria (marcados), como foi verificado, e `Closes #<n>`.
   - `gh issue edit <n> --remove-label "intent:in-progress" --add-label "intent:in-review"`

6. Informe a URL do PR e sugira `/intent-system:review <pr>`.
