# Contribuindo com o Venore Docks

Vale para o core e para todos os repos `venore-plugin-*` / `venore-theme-*` da organização.

## Antes de abrir um PR

Rode, na raiz do repo:

```bash
npm run lint        # ESLint — inclui as regras de fronteira (boundaries) e a de cor
npm run typecheck   # tsc --noEmit
npm run test        # Vitest — testes unitários (*.test.ts, sem banco)
```

Se o repo tem `*.integration.test.ts`, rode também `npm run test:integration` com
`TEST_DATABASE_URL` apontando para um Postgres vazio (nunca o banco de desenvolvimento).

Em plugins e no core, `npm run build` (`next build`) também precisa passar — ele é o único
passo que pega um client component importando o barrel de um plugin por valor.

## Regras de arquitetura que o PR precisa respeitar

- **Fluxo de camadas.** Todo use case segue `handler.ts → service.ts → store.ts → view.ts /
  types.ts`, em arquivos separados. `handler` e `service` retornam `OperationResult<T>` e nunca
  lançam exception para erro de negócio esperado.
- **Fronteiras.** Um plugin só importa de `@venore/plugin-sdk` (ou, no monorepo, do barrel
  `index.ts` e de `contracts/` de um context) — nunca de `store`, `schema` ou `service` interno.
  Plugin não acessa internal de outro plugin. As regras têm enforcement em `npm run lint`.
- **Design tokens.** Nenhum valor de cor, raio, sombra, espaçamento ou tipografia hardcoded em
  componente. Só o vocabulário semântico do shadcn (`bg-card`, `text-muted-foreground`,
  `border-border`, …). Valor de design mora no `theme.css` de um tema, nunca em `globals.css`.
- **Mobile-first.** Classe responsiva escreve o estado mobile sem prefixo primeiro, depois
  `sm:` → `md:` → `lg:` → `xl:` → `2xl:` na mesma ordem.
- **Migrations.** Geradas com `drizzle-kit generate`, nunca editadas à mão. Migration de plugin
  roda no install, não no build.

O detalhamento completo está no `AGENTS.md` e no `docs/venore-docks.md` do core.

## Commits e PRs

- Mensagens no imperativo, escopo curto no início (`themes: …`, `broadcast: …`, `docs: …`).
- Um PR = uma mudança coesa. Descreva o *porquê*, não só o *o quê*.
- CI verde (`lint` + `typecheck` + `test`) é pré-requisito de review.

## Reportando bugs e pedindo features

Use os templates de issue. Para vulnerabilidades, siga o [`SECURITY.md`](SECURITY.md) — não
abra issue pública.
