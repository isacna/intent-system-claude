# Taxonomia de labels do Intent-System

Todas as labels usam o prefixo `intent:` para não colidir com labels existentes do repositório.

## Labels de tipo (permanentes na issue)

| Label | Cor sugerida | Aplica-se a | Significado |
| --- | --- | --- | --- |
| `intent:root` | `#1D76DB` | Issue raiz (única por repo) | Árvore de intents do repositório |
| `intent:node` | `#0E8A16` | Issues de intent | Intent (nó da árvore — porquê e o quê) |
| `intent:packet` | `#5319E7` | Issues de packet | Standalone Child Issue Contract |
| `intent:clarification` | `#FBCA04` | Issues de pergunta | Decisão em aberto aguardando o humano |

## Labels de estado (exclusivas entre si; apenas em packets)

| Label | Cor sugerida | Significado |
| --- | --- | --- |
| `intent:ready` | `#0052CC` | Packet validado, pronto para implementação |
| `intent:in-progress` | `#D93F0B` | Em implementação (branch criado) |
| `intent:in-review` | `#C2E0C6` | PR aberto aguardando revisão |
| `intent:done` | `#2EA44F` | Mesclado e com closeout concluído |

## Máquina de estados do packet

```
slice → [intent:packet + intent:ready]
implement (início) → remove intent:ready, adiciona intent:in-progress
implement (PR aberto) → remove intent:in-progress, adiciona intent:in-review
review (mudanças solicitadas) → permanece intent:in-review
closeout (após merge) → remove intent:in-review, adiciona intent:done, fecha a issue
```

Regras:
- Um packet tem **exatamente uma** label de estado por vez.
- Transições só acontecem pelos comandos do fluxo — nunca edite estados manualmente.
- Ao mudar estado: `gh issue edit <n> --remove-label "<antiga>" --add-label "<nova>"`.

## Criação (feita pelo /intent-system:init)

```bash
gh label create "intent:root" --color "1D76DB" --description "Árvore de intents do repositório" --force
gh label create "intent:node" --color "0E8A16" --description "Intent (porquê e o quê)" --force
gh label create "intent:packet" --color "5319E7" --description "Standalone Child Issue Contract" --force
gh label create "intent:clarification" --color "FBCA04" --description "Decisão em aberto" --force
gh label create "intent:ready" --color "0052CC" --description "Packet pronto para implementação" --force
gh label create "intent:in-progress" --color "D93F0B" --description "Packet em implementação" --force
gh label create "intent:in-review" --color "C2E0C6" --description "PR aguardando revisão" --force
gh label create "intent:done" --color "2EA44F" --description "Packet concluído" --force
```
