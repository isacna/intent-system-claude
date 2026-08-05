# intent-system — Intent-Driven Development para Claude Code

Plugin do Claude Code que implementa o fluxo de **Intent-Driven Development (IDD)** usando
GitHub Issues como armazenamento: capture o *porquê* antes do código, fatie o trabalho em
contratos autossuficientes e conduza implementação, revisão e encerramento com labels como
máquina de estados.

Inspirado na metodologia de [intent-driven-development.com](https://www.intent-driven-development.com/)
e no [intent-system da J-Tech Japan](https://github.com/J-Tech-Japan/intent-system) — mas
autocontido: sem dependência de .NET nem do `intent-cli`. Requer apenas o [`gh` CLI](https://cli.github.com/) autenticado.

## Conceitos

```
Intent (porquê e o quê)  →  Packet (contrato de uma fatia)  →  Code (última milha)
```

- **Intent**: issue durável que registra propósito, resultado esperado, restrições e decisões.
- **Intent Storming**: entrevista estruturada — uma pergunta por vez, com opções, prós/contras e recomendação — que extrai e registra o intent.
- **Packet**: issue-contrato autossuficiente (Standalone Child Issue Contract). Quem implementa lê apenas a issue e o código do repositório.
- **Labels `intent:*`**: expressam o estado do fluxo (`ready → in-progress → in-review → done`).

## Instalação

```
/plugin marketplace add <url-ou-caminho-deste-repositório>
/plugin install intent-system
```

Para desenvolvimento local: `claude --plugin-dir <caminho-deste-repositório>`.

## Uso

| Comando | O que faz |
| --- | --- |
| `/intent-system:init` | Configura o repo: labels + issue raiz da árvore de intents |
| `/intent-system:storm [tópico]` | Intent Storming — entrevista estruturada que gera o intent |
| `/intent-system:new <descrição>` | Registra um intent rápido, sem entrevista longa |
| `/intent-system:slice [#intent]` | Corta o próximo packet e publica como issue pronta |
| `/intent-system:next` | Recomenda a próxima ação com base no estado das issues |
| `/intent-system:implement [#packet]` | Implementa um packet: branch, código, verificação, PR |
| `/intent-system:review [#pr]` | Revisa o PR estritamente contra o contrato do packet |
| `/intent-system:closeout [#pr]` | Encerra após o merge: labels, task-lists, próximo passo |
| `/intent-system:status` | Árvore de intents e estado de todos os packets |

### Fluxo típico

```
/intent-system:init
/intent-system:storm "portal de autoatendimento para clientes"
/intent-system:slice #12
/intent-system:implement #15
/intent-system:review 16        (após revisão aprovada, você faz o merge)
/intent-system:closeout 16
/intent-system:next
```

## Estrutura do plugin

```
.claude-plugin/           manifesto e marketplace
commands/                 os 9 slash commands
skills/intent-system/     skill com a metodologia + templates
  references/             intent-template, packet-template, question-format, labels
```

## Licença

Apache 2.0 — veja [LICENSE](LICENSE).
