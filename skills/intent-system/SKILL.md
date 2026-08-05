---
name: intent-system
description: >-
  Intent-Driven Development (IDD) com GitHub Issues. Use quando o usuário falar
  de intent, intents, intent storming, IDD, packet, fatiar trabalho, child issue,
  contrato de implementação, ou quiser capturar o "porquê" de uma feature antes
  de codificar, cortar a próxima fatia de trabalho, implementar/revisar um packet
  ou perguntar qual o próximo passo do fluxo de intents.
---

# Intent-System — Intent-Driven Development no Claude Code

## A metodologia em uma frase

O IDD move a fonte da verdade uma camada acima do código: **Intent (porquê e o quê) → Spec (como) → Code (última milha)**. Intents são artefatos duráveis curados por humanos; o código é derivado deles.

## Onde tudo vive

Todo o estado fica em **GitHub Issues do próprio repositório**, manipuladas via `gh` CLI. Não há banco de dados nem arquivos de metadata locais.

- Uma **issue raiz** (`intent:root`) mantém a árvore de intents em task-lists, organizada por categorias: identity, product, features, technology, decisions, operations.
- Cada **intent** é uma issue `intent:node` seguindo `references/intent-template.md`.
- Cada **packet** é uma issue `intent:packet` seguindo `references/packet-template.md` — um **Standalone Child Issue Contract**.
- O estado do fluxo é expresso por labels — ver `references/labels.md`.

## Roteamento: objetivo → comando

| Objetivo do usuário | Comando |
| --- | --- |
| Configurar o repo pela primeira vez | `/intent-system:init` |
| Explorar/clarificar uma ideia antes de codificar | `/intent-system:storm` |
| Registrar um intent rapidamente, sem entrevista longa | `/intent-system:new` |
| Cortar a próxima fatia de trabalho de um intent | `/intent-system:slice` |
| Saber o que fazer agora | `/intent-system:next` |
| Implementar um packet pronto | `/intent-system:implement` |
| Revisar um PR contra o contrato do packet | `/intent-system:review` |
| Encerrar um PR mesclado | `/intent-system:closeout` |
| Ver o estado geral da árvore | `/intent-system:status` |

Se o usuário pedir algo relacionado a intents que não mapeia diretamente, escolha o comando mais próximo e explique a escolha.

## Regras invioláveis

1. **Uma pergunta por vez** no Intent Storming, sempre no formato de `references/question-format.md` (entendimento atual → contexto → pergunta → 2–4 opções com prós/contras → recomendação → impacto). Prefira a ferramenta AskUserQuestion quando disponível.
2. **Packet é contrato autossuficiente**: o corpo da issue do packet deve conter TODO o contexto necessário. O implementador lê apenas a issue e o código do repositório — nunca outras issues, nem a árvore de intents.
3. **Labels só transicionam pelos comandos** do fluxo (`ready → in-progress → in-review → done`). Não altere labels manualmente fora do comando correspondente.
4. **Decisões são duráveis**: toda decisão tomada no storm é registrada na seção Decisions do intent (pergunta, opções consideradas, escolha e porquê). Nunca sobrescreva decisões antigas — acrescente.
5. **Humano decide, agente executa**: recomendações são sempre oferecidas, mas escolhas de produto/arquitetura são do usuário.
6. **Reporte saída real** dos comandos `gh` (números de issue, URLs), não interpretações.

## Convenções

- Labels usam o prefixo `intent:` (namespace) — taxonomia completa em `references/labels.md`.
- Branches de implementação: `intent/<número-do-packet>-<slug-curto>`.
- PRs de packet incluem `Closes #<packet>` no corpo.
- Hierarquia: intents referenciam o pai com `Parent: #N` no corpo; a issue raiz e cada intent mantêm task-lists (`- [ ] #N`) dos filhos.
- Idioma das issues: siga o idioma do usuário/repositório.
