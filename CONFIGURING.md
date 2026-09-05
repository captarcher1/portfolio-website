# Configuring your site

This guide assumes no coding background beyond editing a text file. If
something here doesn't work, open an issue — that's a bug in this guide, not
a mistake on your part.

## 1. Get the project running

```bash
npm install
npm run dev
```

Then open [http://localhost:3000](http://localhost:3000) in your browser. You
should see a fictional example portfolio — that's expected, and it's safe to
leave running while you edit.

## 2. Find your config file

Open `config/site.ts` in a text editor (it was created for you automatically
by step 1, from `config/site.example.ts`). This one file controls everything
on the page. Save it, and your browser tab will update automatically.

## 3. Edit your identity

At the top of `config/site.ts`:

```ts
name: "Your Name",
role: "Your Role / Title",
headshot: "/images/your-photo.jpg", // see step 4
metaTitle: "Your Name | Your Role",
metaDescription: "One sentence describing you, for search engines and link previews.",
social: {
  email: "you@example.com",
  linkedin: "https://www.linkedin.com/in/yourprofile",
  github: "https://github.com/yourusername",
  calendarBookingUrl: "https://calendar.app.google/yourlink", // optional
},
```

Leave any `social` field out entirely if you don't want that icon to appear —
it's optional, not required.

## 4. Add your photo

Put your photo in `public/images/` (any filename, e.g. `my-photo.jpg`), then
set `headshot: "/images/my-photo.jpg"` (note the leading `/`). If you skip
this, your initials will show instead — that's an intentional fallback, not a
bug.

## 5. Edit each section

Scroll down to the `sections` array. Each entry is one block on your page.
You can:

- **Change text** — edit any string inside `data: { ... }`.
- **Hide a section** — set `enabled: false`.
- **Reorder sections** — cut and paste a whole `{ ... }` block to a different
  position in the array.
- **Remove a section** — delete its whole `{ ... }` block.
- **Rename a section's heading** — change its `heading` field.
- **Rename a section's nav label** — change its `navLabel` field.

See the [README's section-type table](./README.md#section-types) for exactly
what fields each section type expects.

## 6. Turn on the contact form (optional)

1. Create a free account at [web3forms.com](https://web3forms.com) and get an
   access key.
2. Copy `.env.example` to a new file named `.env.local`.
3. Paste your key: `NEXT_PUBLIC_WEB3FORMS_ACCESS_KEY=your-key-here`.
4. Restart `npm run dev`.

Without this step, the contact section shows a plain "email me" link instead
— that works fine too, it's just not a form.

## 7. Deploy

Push your repo to GitHub, then connect it at [vercel.com](https://vercel.com)
— it will detect this as a Next.js project automatically. If you set up the
contact form (step 6), add `NEXT_PUBLIC_WEB3FORMS_ACCESS_KEY` again in
Vercel's project environment variables — `.env.local` only applies locally,
it doesn't get deployed with your code.

## Troubleshooting

- **"Invalid site config in config/site.ts"** at startup — the error message
  lists exactly which field is wrong and why. Fix that field and save again.
- **A broken image icon** — check the path starts with `/` and the file
  actually exists in `public/images/`.
- **Still stuck** — open an issue on this repo.
