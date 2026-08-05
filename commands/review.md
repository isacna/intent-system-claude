---
description: Revisa um PR estritamente contra o contrato do packet
argument-hint: [#PR]
---

Revise o pull request: $ARGUMENTS
(Se não houver argumento, liste PRs abertos de packets — `gh pr list --search "intent/" --state open` e issues `intent:in-review` — e pergunte qual revisar.)

Processo:

1. **Recupere o contrato**: pelo `Closes #<n>` no corpo do PR (`gh pr view <pr> --json body,title,url`), abra a issue do packet. A revisão é SEMPRE contra o contrato — acceptance criteria, escopo e constraints — não contra preferências pessoais.

2. **Analise o diff** (`gh pr diff <pr>`) verificando, nesta ordem:
   - **Acceptance criteria**: cada critério do packet foi atendido? Aponte evidência no diff.
   - **Escopo**: há mudanças fora do escopo declarado (scope creep)? Itens "NÃO inclui" foram respeitados?
   - **Constraints**: os limites operacionais do contrato foram respeitados?
   - **Correção**: bugs, casos de borda quebrados, regressões prováveis.
   - **Verificação**: o PR descreve como foi verificado? Os Verification steps do contrato são reproduzíveis? Se possível, execute-os localmente (`gh pr checkout <pr>`).

3. **Emita o veredito**:
   - Tudo atendido → `gh pr review <pr> --approve --body "<resumo: critérios verificados, evidências>"`
   - Problemas → `gh pr review <pr> --request-changes --body "<lista objetiva: critério/escopo violado + o que corrigir>"` (o packet permanece `intent:in-review`).

4. Informe o resultado real e o próximo passo: merge + `/intent-system:closeout` se aprovado; corrigir e re-revisar se não. NÃO faça merge por conta própria — o merge é decisão do usuário.
