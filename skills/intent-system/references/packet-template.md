# Template: issue de Packet — Standalone Child Issue Contract (`intent:packet`)

**Título da issue**: `[Packet] <verbo + objeto — fatia fina e revisável>`

**Labels**: `intent:packet` + `intent:ready`

**Princípio central**: o corpo desta issue é um **contrato autossuficiente**. O implementador
(humano ou agente) lê APENAS esta issue e o código do repositório. Se ele precisar abrir
outra issue ou perguntar contexto, o contrato falhou a validação.

**Corpo**:

```markdown
> Intent: #<número do intent pai> (referência apenas para rastreio — o conteúdo necessário está inline abaixo)

## Objective

<Uma frase: o que este packet entrega quando concluído.>

## Intent context (inline)

<Resumo AUTOSSUFICIENTE do porquê e das decisões relevantes do intent pai.
Copie para cá tudo que o implementador precisa saber — ele não lerá o intent.>

## Scope

**Inclui:**
- <item concreto>

**NÃO inclui (fora de escopo):**
- <item explicitamente excluído — evita scope creep>

## Technical guidance

<Direção técnica: arquivos/módulos prováveis, padrões do repo a seguir,
APIs/contratos a respeitar, armadilhas conhecidas.>

## Acceptance criteria

<Critérios verificáveis, cada um testável de forma objetiva.>

- [ ] <critério 1>
- [ ] <critério 2>

## Verification steps

<Como provar que os critérios foram atendidos: comandos de teste, fluxo manual
a exercitar, saídas esperadas.>

1. <passo>

## Constraints

<Limites operacionais: não tocar em X, manter compatibilidade com Y,
tamanho máximo do diff, exigências de migração, etc. Escreva "Nenhuma" se vazio.>
```

## Checklist de validação "standalone" (antes de publicar)

Rode este checklist no texto do packet; só publique com `intent:ready` se TODOS passarem:

- [ ] Um leitor sem acesso a nenhuma outra issue entende o que fazer e por quê?
- [ ] A fatia é fina o suficiente para um PR revisável (idealmente < ~400 linhas de diff)?
- [ ] Todos os acceptance criteria são objetivamente verificáveis?
- [ ] Verification steps são executáveis no repo como está?
- [ ] O que está fora de escopo está explícito?
- [ ] Nenhuma decisão em aberto (`intent:clarification`) bloqueia esta fatia?
