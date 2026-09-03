<!-- Título: escopo curto + imperativo. Ex: "broadcast: corrige timezone na tela de saída" -->

## O que muda e por quê

<!-- O problema ou a necessidade, e a abordagem escolhida. Linke a issue: Closes #123 -->

## Como testei

<!-- Passos, breakpoints checados (mobile + desktop se toca UI), dados usados -->

## Checklist

- [ ] `npm run lint` passa (boundaries + regra de cor)
- [ ] `npm run typecheck` passa
- [ ] `npm run test` passa; teste unitário cobre o `service` novo/alterado
- [ ] `npm run build` passa (se for core ou plugin)
- [ ] Sem valor de cor/raio/espaçamento hardcoded; `src/components/ui/**` não editado direto
- [ ] Fluxo de camadas respeitado (`handler → service → store`), `OperationResult<T>` em `handler`/`service`
- [ ] Se toca schema: migration via `drizzle-kit generate`, contagem de migrations confere
- [ ] Se cruza mais de um domínio de dado: teste de integração incluído
- [ ] UI nova/alterada é responsiva mobile-first, verificada em ao menos um breakpoint mobile e um desktop
