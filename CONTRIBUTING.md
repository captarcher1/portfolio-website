# Contributing

Thanks for considering a contribution. This is a personal-site template
maintained on a best-effort basis, not a funded open-source project — please
keep that in mind when opening issues or PRs.

## Reporting a bug

Open an issue with: what you expected, what happened instead, and your
Node.js version. A minimal `config/site.ts` snippet that reproduces the issue
helps a lot.

## Proposing a change

- **New section type** — open an issue first to discuss the design before
  writing code; adding a type touches `config/types.ts`,
  `components/layout/SectionRenderer.tsx`, a new file under
  `components/sections/`, and the README's section-type table.
- **Bug fix / small improvement** — a PR is welcome directly.
- **New dependency** — please explain why an existing one (Next.js, Tailwind,
  zod, lucide-react) can't cover it. This template intentionally stays light.

## Development

```bash
npm install
npm run dev        # local dev server
npm run typecheck  # tsc --noEmit
npm run lint        # eslint
npm run build       # production build — this is what CI runs
```

All four are expected to pass before a PR is merged (see
`.github/workflows/ci.yml`).

## Scope

Out of scope for this template (see the README and the original planning
doc): a CMS or hosted admin UI, multi-language support, and role-specific
theme presets. If you need one of these, a fork is the right approach rather
than a PR here.
