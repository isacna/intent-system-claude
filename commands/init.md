---
description: Configura o repositório atual para Intent-Driven Development (labels + issue raiz)
---

Configure o repositório atual para o fluxo Intent-System. Leia antes a taxonomia em
`${CLAUDE_PLUGIN_ROOT}/skills/intent-system/references/labels.md`.

Passos:

1. **Pré-verificações**:
   - `gh auth status` — se não autenticado, oriente o usuário a rodar `! gh auth login` e pare.
   - `gh repo view --json nameWithOwner` — confirme que o diretório atual é um repo GitHub. Se não for, explique e pare.
   - `gh issue list --label "intent:root" --state open --json number,title` — se já existir issue raiz, informe o número e pare (repo já inicializado; não duplique).

2. **Criar labels**: execute os comandos `gh label create ... --force` exatamente como listados em labels.md.

3. **Criar a issue raiz** com label `intent:root`, título `[Intent Root] Árvore de intents`, e corpo com uma seção (task-list vazia) por categoria:

   ```markdown
   Árvore de intents deste repositório (Intent-Driven Development).
   Gerenciada pelos comandos /intent-system:* — não edite manualmente.

   ## identity
   ## product
   ## features
   ## technology
   ## decisions
   ## operations
   ```

4. **Relatório final**: informe o número/URL da issue raiz, as labels criadas, e o próximo passo sugerido: `/intent-system:storm <tópico>` para capturar o primeiro intent.

Reporte a saída real dos comandos (números, URLs), não interpretações.
