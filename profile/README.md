# Venore

**Venore Docks** é um boilerplate de site institucional + CMS construído sobre Next.js
(App Router). O core entrega autenticação, RBAC, observabilidade, gestão de conteúdo e mídia,
banco PostgreSQL e temas trocáveis em runtime. Tudo que é específico de um site chega por
**plugins** e **temas** instaláveis — cada um no seu próprio repositório.

## Como as peças se encaixam

- **Core** — `venore-docks` (privado). A plataforma. Cada site é um fork que acompanha o core
  via `git merge upstream/main` e nunca edita `core/` diretamente.
- **`@venore/plugin-sdk`** — o contrato versionado core → plugin. Um plugin importa só o SDK,
  declara no manifesto o que contribui (permissions, navegação, rotas, blocos, seeds) e roda
  suas próprias migrations no momento do install, nunca no build.
- **Plugins** — `venore-plugin-*`. Capacidades de site. Uma instância traz só os que quer via
  `VENORE_PLUGINS` + `npm run sync:plugins`; `git pull` no core não arrasta plugin nenhum.
- **Temas** — pacotes `@venore/theme-*` descobertos pelas deps do `package.json`. Cada tema
  exporta um `Shell` e redeclara o vocabulário de design tokens sob seu `[data-theme="…"]`. O
  `venore-slime` é o fallback obrigatório e vive dentro do core.

## Repositórios

### Plugins

| Repo | O que faz |
| --- | --- |
| [venore-plugin-academy](https://github.com/venore-docks/venore-plugin-academy) | Cursos e trilhas de aprendizado — editor de aulas, blocos interativos, bundles de curso importáveis |
| [venore-plugin-broadcast](https://github.com/venore-docks/venore-plugin-broadcast) | Switcher de cenas e camadas estilo OBS para telão e TV em rede local |
| [venore-plugin-birthdays](https://github.com/venore-docks/venore-plugin-birthdays) | Mural e registro de aniversariantes do mês, com bloco de página e tela de TV |

### Temas

`@venore/theme-*` — instaláveis via git-dependency, um repositório cada:
[nite](https://github.com/venore-docks/venore-theme-nite) ·
[knights](https://github.com/venore-docks/venore-theme-knights) ·
[paladins](https://github.com/venore-docks/venore-theme-paladins) ·
[sorcerers](https://github.com/venore-docks/venore-theme-sorcerers) ·
[druids](https://github.com/venore-docks/venore-theme-druids) ·
[academy](https://github.com/venore-docks/venore-theme-academy) ·
[fearless](https://github.com/venore-docks/venore-theme-fearless)

## Stack

Next.js · React · Tailwind CSS v4 · shadcn/ui · Auth.js · Drizzle ORM + PostgreSQL · Vitest
