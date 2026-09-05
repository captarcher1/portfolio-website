# portfolio-website

A reusable, config-driven personal portfolio site built with Next.js and
Tailwind CSS. Fork it, edit one config file, deploy — no JSX editing required
to rename a section, reorder your page, or swap out your content.

This is a personal-site template, not a maintained product — issues and PRs
are welcome, but there's no support SLA. A CI check (lint + typecheck + build,
see `.github/workflows/ci.yml`) runs on every PR — the only "quality signal"
this repo makes. Once this repo has a permanent home on GitHub, add a status
badge here: `![CI](https://github.com/<owner>/<repo>/actions/workflows/ci.yml/badge.svg)`.

## Quick start

1. **Fork or clone this repo.**
2. **Install dependencies** — this also copies `config/site.example.ts` to
   `config/site.ts` for you automatically:
   ```bash
   npm install
   ```
3. **Edit `config/site.ts`** with your own name, role, sections, and content.
   It's git-ignored, so your real content never gets committed here. See
   [CONFIGURING.md](./CONFIGURING.md) for a field-by-field, non-engineer-friendly
   walkthrough.
4. **Swap your photo and any logos** into `public/images/`, and point
   `headshot` / section `logo` fields at them.
5. **Run it locally:**
   ```bash
   npm run dev
   ```
   Open [http://localhost:3000](http://localhost:3000).
6. **Deploy to Vercel** — see [Deploy your own](#deploy-your-own) below.

## How content works

Every visible section of the page — Hero, Work, Certifications, Contact, and
so on — is one entry in the `sections` array in `config/site.ts`. Each entry
has:

- `id` — used as the section's anchor (`#work`, `#about`, …).
- `type` — one of the 9 section types below; determines what renders.
- `heading` — optional; the visible `<h2>` for that section.
- `navLabel` — optional; if set, the section gets a link in the navbar.
- `enabled` — set to `false` to hide a section without deleting it.
- `data` — the content itself, shaped per the type's schema below.

Add, remove, reorder, or rename a section by editing this array — never by
editing component code. The navbar is generated from the same array, so it
can never fall out of sync with what's actually on the page. A section left
with an empty `data` array is automatically skipped, in both the page and the
nav.

### Section types

| Type | Renders | Data shape |
|---|---|---|
| `hero` | Name, role, eyebrow, headline, photo, socials, CTAs | `{ eyebrow?, headline, supportingCopy?, primaryCta?, secondaryCta? }` |
| `metrics` | Stat tiles on a dark band | `[{ value, label }]` |
| `cardGrid` | Grid of cards — image-led (if `image` is set) or icon-led otherwise | `[{ title, description, tagline?, icon?, image?, badge?, chips?, href?, linkLabel? }]` |
| `processSteps` | Numbered steps with connecting arrows | `[{ step, copy, icon? }]` |
| `topicGrid` | Icon + topic + one-line angle, no link required | `[{ topic, angle, icon? }]` |
| `logoCredentials` | Issuer logo, title, verify link | `{ items: [{ issuer, title, href?, logo? }], moreLink? }` |
| `chipGroups` | Grouped skill/tech chip clusters | `[{ group, chips: string[] }]` |
| `textAndTimeline` | Bio paragraphs + chronological entries | `{ paragraphs: string[], timeline?: [{ organization, role, dates, description? }] }` |
| `contactForm` | Web3Forms-backed form, or a `mailto:` fallback | `{ heading, supportingCopy?, socialLink?, privacyNote? }` |

`icon` fields take a name from `components/icons/iconMap.ts` (a small starter
set of [lucide-react](https://lucide.dev/icons) icons — add more there as
needed).

Full working example: [`config/site.example.ts`](./config/site.example.ts) —
every field above, populated with fictional content.

### Graceful fallbacks

A fresh fork should never look broken:

- No `headshot` configured → renders your initials as an avatar instead of a
  broken image.
- No credential `logo` → renders the issuer's initials as a badge instead.
- No `NEXT_PUBLIC_WEB3FORMS_ACCESS_KEY` set → the contact section renders a
  plain "email me" link instead of a non-functional form.
- A section with an empty `data` array → excluded from both the page and the
  nav automatically.

### Contact form

The contact form posts to [Web3Forms](https://web3forms.com) (a free tier is
available). To enable it:

1. Get an access key from web3forms.com.
2. Copy `.env.example` to `.env.local` and set
   `NEXT_PUBLIC_WEB3FORMS_ACCESS_KEY=<your key>`.
3. `.env.local` is git-ignored — your key never gets committed.

Without a key set, the section falls back to a `mailto:` link automatically.

## Deploy your own

The easiest path is [Vercel](https://vercel.com) (zero-config for Next.js).
After connecting your fork, add `NEXT_PUBLIC_WEB3FORMS_ACCESS_KEY` as an
environment variable in the Vercel project settings if you want the contact
form enabled in production.

## Tech stack

Next.js (App Router) + TypeScript + Tailwind CSS v4, content validated with
[zod](https://zod.dev). No database, no CMS — this stays a "clone it, edit a
config file, redeploy" template, not a hosted product.

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md).

## License

[MIT](./LICENSE)
