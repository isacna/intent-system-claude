---
description: Intent Storming — entrevista estruturada para extrair e registrar um intent
argument-hint: [tópico ou ideia a explorar]
---

Conduza uma sessão de **Intent Storming** sobre: $ARGUMENTS
(Se não houver argumento, pergunte primeiro qual ideia/problema o usuário quer explorar.)

Siga estritamente o formato de pergunta definido em
`${CLAUDE_PLUGIN_ROOT}/skills/intent-system/references/question-format.md` e o template de intent em
`${CLAUDE_PLUGIN_ROOT}/skills/intent-system/references/intent-template.md`.

Processo:

1. **Preparação**: localize a issue raiz (`gh issue list --label "intent:root" --state open`).
   Se não existir, oriente a rodar `/intent-system:init` primeiro e pare.
   Verifique se já existe um intent aberto sobre o mesmo tópico (`gh issue list --label "intent:node" --search "<tópico>"`) — se existir, pergunte se o usuário quer continuar o storm daquele intent em vez de criar um novo.

2. **Entrevista** — UMA pergunta por vez, no formato estruturado (entendimento atual → contexto → pergunta → 2–4 opções com prós/contras → recomendação → impacto). Use AskUserQuestion quando disponível, com a opção recomendada primeiro e "(Recomendado)" no label. Comece pelo que destrava mais: propósito/problema, depois resultado esperado, depois restrições, depois decisões estruturantes de abordagem. Tipicamente 3 a 7 perguntas — pare quando Purpose e Outcome estiverem claros e nenhuma dúvida bloqueante restar, ou quando o usuário pedir.

3. **Consolidação**: monte o corpo do intent com o template (Categoria, Parent = issue raiz, Purpose, Outcome, User Context/Constraints, Means, Decisions com uma entrada D<n> por resposta dada — pergunta, opções, decisão, porquê —, Packets vazio, Open Questions). Mostre o resumo ao usuário antes de publicar.

4. **Publicação**:
   - `gh issue create --title "[Intent] <nome>" --label "intent:node" --body-file <arquivo temporário>` (escreva o corpo num arquivo no scratchpad para preservar a formatação).
   - Adicione `- [ ] #<n> — <nome>` na task-list da categoria correspondente na issue raiz (`gh issue edit`  no corpo da raiz — preserve o restante do corpo intacto).
   - Perguntas sem decisão que bloqueiam avanço: crie issues `intent:clarification` linkando o intent.

5. **Encerramento**: informe número/URL do intent criado e sugira o próximo passo — normalmente `/intent-system:slice #<n>` se o intent estiver packet-ready, ou resolver as clarifications.
