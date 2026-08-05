# Template: issue de Intent (`intent:node`)

**Título da issue**: `[Intent] <nome curto e descritivo>`

**Labels**: `intent:node` (+ `intent:clarification` se houver perguntas bloqueantes)

**Corpo**:

```markdown
> Categoria: <identity | product | features | technology | decisions | operations>
> Parent: #<número da issue pai — a raiz ou outro intent>

## Purpose (por quê)

<Por que este intent existe. Que problema ou oportunidade motiva o trabalho.
O raciocínio que deve sobreviver mesmo quando o código mudar.>

## Outcome (o que importa alcançar)

<Resultados observáveis que definem sucesso. O "o quê", não o "como".>

## User Context / Constraints

<Quem é afetado, restrições de negócio, técnicas, regulatórias ou de prazo
que condicionam as soluções aceitáveis.>

## Means (abordagem)

<Direção de solução acordada, em alto nível. Pode começar vazio e ser
preenchido conforme as decisões do storm.>

## Decisions

<Registro durável de Q&A do Intent Storming. Acrescente, nunca sobrescreva.>

### D1 — <título da decisão> (<data AAAA-MM-DD>)
- **Pergunta**: <a pergunta feita>
- **Opções consideradas**: <opção A — prós/contras resumidos; opção B — ...>
- **Decisão**: <opção escolhida>
- **Porquê**: <justificativa dada pelo usuário/recomendação aceita>

## Packets

<Task-list das fatias de trabalho cortadas deste intent.>

- [ ] #<número do packet> — <nome curto>

## Open Questions

<Perguntas ainda sem decisão. Se bloqueiam o fatiamento, crie issue
`intent:clarification` e linke aqui.>
```

## Regras de preenchimento

- Purpose e Outcome são obrigatórios antes de qualquer `slice`.
- Cada decisão do storm vira uma entrada `D<n>` na seção Decisions.
- Ao criar um packet, adicione-o à task-list da seção Packets e marque `[x]` no closeout.
- Ao criar o intent, adicione-o também à task-list da categoria correspondente na issue raiz.
