# Repro: `useSetI18nParams` params lost on a prerendered page opened with a query string or hash

[Open in StackBlitz](https://stackblitz.com/github/GlennBergmans/i18n-set-params-query-repro), then in its terminal:

```sh
pnpm generate
npx serve .output/public
```

(`nuxt preview` doesn't work for static output with this starter's `@nuxt/cli`, and the dev server
doesn't show the bug: it only happens on prerendered pages.)

Changes from the v10 starter: `app/pages/products/[slug].vue` sets its counterpart slugs with
`useSetI18nParams`, the index links to it, and `LangSwitcher` uses `<SwitchLocalePathLink>` (the
starter's `switchLocalePath()` in a `NuxtLink` renders before the page sets its params).

| Open | Language switcher after hydration | Expected |
|---|---|---|
| `/products/red-mug` | `/nl/products/rode-mok`, `/ja/products/akai-magu` | ✅ |
| `/products/red-mug?utm_source=x` | `/nl/products/red-mug?utm_source=x`, `/ja/products/red-mug?utm_source=x` | `/nl/products/rode-mok?…`, `/ja/products/akai-magu?…` |
| `/products/red-mug#top` | `/nl/products/red-mug#top`, `/ja/products/red-mug#top` | `/nl/products/rode-mok#top`, `/ja/products/akai-magu#top` |

The prerendered HTML is correct (view source); the links break during hydration. Served with SSR
instead (`pnpm build && node .output/server/index.mjs`), all three are correct.

---

# Nuxt 3 Minimal Starter with Nuxt I18n

Look at the [Nuxt 3 documentation](https://nuxt.com/docs/getting-started/introduction) to learn more.

## Setup

Make sure to install the dependencies:

```bash
# yarn
yarn install

# npm
npm install

# pnpm
pnpm install
```

## Development Server

Start the development server on http://localhost:3000

```bash
npm run dev
```

## Production

Build the application for production:

```bash
npm run build
```

Locally preview production build:

```bash
npm run preview
```

Check out the [deployment documentation](https://nuxt.com/docs/getting-started/deployment) for more information.
