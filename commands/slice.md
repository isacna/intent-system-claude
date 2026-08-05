---
description: Corta o próximo packet (fatia de trabalho) de um intent e publica como issue pronta
argument-hint: [#issue do intent]
---

Corte a próxima fatia de trabalho do intent: $ARGUMENTS
(Se não houver argumento, liste os intents abertos — `gh issue list --label "intent:node" --state open` — e pergunte de qual fatiar.)

Siga o template e o checklist de validação de
`${CLAUDE_PLUGIN_ROOT}/skills/intent-system/references/packet-template.md`.

Processo:

1. **Leia o intent** (`gh issue view <n>`) e os packets já cortados dele. Verifique bloqueios:
   - Purpose/Outcome vazios → oriente a rodar `/intent-system:storm` primeiro e pare.
   - Clarifications abertas que afetam a próxima fatia → aponte-as e pare.

2. **Explore o código do repositório** o suficiente para dar Technical guidance concreta (arquivos prováveis, padrões existentes a seguir).

3. **Proponha a fatia**: a menor unidade que entrega valor verificável e cabe num PR revisável (~<400 linhas de diff). Descreva a proposta em 2–3 frases e confirme com o usuário antes de redigir o contrato (use AskUserQuestion se houver mais de um corte razoável, com sua recomendação primeiro).

4. **Redija o Standalone Child Issue Contract** com o template completo. Regra central: o corpo deve ser autossuficiente — copie para "Intent context (inline)" tudo que o implementador precisa; ele não lerá o intent nem outras issues.

5. **Valide** contra o checklist "standalone" do template. Só prossiga se todos os itens passarem; caso contrário, corrija o contrato ou volte ao passo 3.

6. **Publique**:
   - `gh issue create --title "[Packet] <verbo + objeto>" --label "intent:packet" --label "intent:ready" --body-file <arquivo no scratchpad>`
   - Adicione `- [ ] #<packet> — <nome>` na seção Packets do intent pai (preservando o restante do corpo).

7. Informe número/URL do packet e sugira `/intent-system:implement #<packet>`.
