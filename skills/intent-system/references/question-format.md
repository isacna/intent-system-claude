# Formato de pergunta do Intent Storming

Toda pergunta do storm segue esta estrutura — **uma pergunta por vez**, nunca uma lista
de perguntas soltas. O objetivo é que o usuário decida rápido e bem informado.

## Estrutura

```markdown
**Entendimento atual**: <fatos já estabelecidos até aqui, em 1–2 frases>

**Contexto**: <por que esta decisão importa; o que ela trava/destrava adiante>

**Pergunta**: <UMA pergunta focada>

**Opções**:
1. **<Opção A>** — <descrição>. Prós: <...>. Contras: <...>.
2. **<Opção B>** — <descrição>. Prós: <...>. Contras: <...>.
3. (2 a 4 opções no total)

**Recomendação**: <opção preferida e o porquê, em 1–2 frases>

**Impacto**: <o que fica registrado/travado no intent quando o usuário decidir>
```

## Regras

- Se a ferramenta **AskUserQuestion** estiver disponível, use-a: a pergunta vai no campo
  `question` (inclua o contexto resumido), cada opção com prós/contras na `description`,
  e a recomendada primeiro com "(Recomendado)" no label. Agrupe no máximo 2–4 perguntas
  por chamada apenas quando forem independentes entre si.
- Se a resposta do usuário abrir uma nova dúvida, ela vira a próxima pergunta — não
  acumule perguntas pendentes em paralelo.
- Cada resposta é registrada imediatamente como decisão `D<n>` na seção Decisions do
  intent (pergunta, opções, escolha, porquê).
- O usuário pode responder "não sei / decidir depois": registre em Open Questions e,
  se bloquear o fatiamento, crie issue `intent:clarification`.
- Encerre o storm quando: Purpose e Outcome estiverem claros, as decisões estruturantes
  tomadas e nenhuma pergunta bloqueante restar — ou quando o usuário pedir para parar.
- Sinal de "packet-ready": você conseguiria escrever um packet autossuficiente agora.
