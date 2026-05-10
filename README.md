# Filamuze website (filamuze.com)

Everything that goes live at `filamuze.com` is in this folder. Three
landing pages + six legal pages + a screenshots subfolder. Static HTML,
no build step, no JS, no external CSS — drop the lot at the root of any
host and it works.

## Files

```
docs/website/
  index.html              ← https://filamuze.com/             (EN landing)
  index.ru.html           ← https://filamuze.com/index.ru.html (RU landing)
  index.he.html           ← https://filamuze.com/index.he.html (HE landing, RTL)
  privacy.html            ← https://filamuze.com/privacy.html  (EN privacy policy)
  privacy.ru.html         ← https://filamuze.com/privacy.ru.html
  privacy.he.html         ← https://filamuze.com/privacy.he.html
  terms.html              ← https://filamuze.com/terms.html    (EN terms of service)
  terms.ru.html           ← https://filamuze.com/terms.ru.html
  terms.he.html           ← https://filamuze.com/terms.he.html
  screenshots/            ← app screenshots referenced from index.* (optional)
```

The app's [Settings → About](../../src/screens/SettingsScreen.js) section
links directly to these URLs:

```js
function legalUrl(slug) {
  const lang = i18n.getLanguage();
  if (lang === 'en') return `https://filamuze.com/${slug}.html`;
  return `https://filamuze.com/${slug}.${lang}.html`;
}
```

If filamuze.com isn't reachable yet, those Privacy / Terms taps in the
app open a 404. Apple and Play Store reviewers click these — the URLs
must work before you submit.

## Deploy — pick one

All three options are free for the traffic Filamuze will see at the
Closed Test stage. Cloudflare is the recommended path because the EU
edge gives ~30 ms latency from Israel and from the EU at large.

### Option A — Cloudflare Pages (recommended)

1. Sign in to Cloudflare → **Workers & Pages** → **Create** → **Pages**.
2. **Connect to Git** → pick a repo containing this folder. Two ways:
   - This repo, with build output dir set to `docs/website`.
   - A new dedicated repo (`filamuze-com`) where you sync just this
     folder's contents to the repo root.
3. Build settings: **None** (it's plain HTML). Output directory:
   `docs/website` (or `/` if you used a dedicated repo).
4. **Save and deploy.** Cloudflare assigns a `*.pages.dev` URL — verify
   the EN landing renders correctly on it before pointing the domain.
5. **Custom domain:** Pages project → Custom domains → Set up
   `filamuze.com`. If your DNS is on Cloudflare, the CNAME is added
   automatically. If not, follow the prompt.
6. Push any change → Cloudflare auto-deploys in ~30 seconds.

### Option B — GitHub Pages

1. Create a repo `filamuze-com` (or use this one).
2. Copy the **contents** of `docs/website/` to the **repo root** (Pages
   doesn't serve from a subfolder unless you customize, and the simpler
   the better).
3. Repo Settings → Pages → Source: **Deploy from a branch** → main → `/`.
4. Custom domain → `filamuze.com`. GitHub serves `CNAME` config; point
   your DNS A records at GitHub Pages IPs (instructions in their docs).
5. Push → live in ~1 minute.

### Option C — Plain web host (FTP / cPanel / Netlify drag-drop)

Upload all eleven files (9 HTML + screenshots/* + this README is fine
to leave) to the document root. Done.

## Email — `support@filamuze.com`

The legal pages and the in-app **Settings → Email support** link both
point at `support@filamuze.com`. Set up either:

- **Cloudflare Email Routing** (free if your domain is on Cloudflare
  DNS) — forward to your real address.
- An MX record + alias on the domain registrar.
- Google Workspace / Fastmail — if you want it to be a real mailbox.

Without this, the in-app "Email support" button opens a `mailto:` that
will bounce.

## After deploy: verify

Walk through these in a private/incognito window before submitting to
any store:

- `https://filamuze.com/` — EN landing renders dark, hero card shows
  three demo spool rows, no console errors.
- `https://filamuze.com/index.ru.html` — Cyrillic copy correct.
- `https://filamuze.com/index.he.html` — RTL layout, Hebrew aligns to
  the right.
- All six legal URLs return 200 (not 404). Both EN/RU/HE versions of
  privacy and terms.
- Tap **Privacy Policy** and **Terms of Service** from inside the app
  in each of the three languages → opens the matching language file.
- Send a test mail to `support@filamuze.com` → lands somewhere you read.

## Updating

1. **Content edits** — edit the relevant HTML files (don't forget the
   other two language versions if the change is substantive). Bump the
   "Last updated" date in the header of each updated legal file.
2. **Screenshots** — drop new images into `screenshots/` keeping the
   filenames stable (the landing references them by exact name).
3. **Push** → Cloudflare/GitHub Pages auto-redeploys.

## Disclaimer

The legal pages were drafted by an LLM as a starting point for an indie
hobbyist app. They cover the standard requirements of the App Store and
Play Store privacy / legal sections, and reflect what Filamuze actually
does. For commercial launches, GDPR-heavy markets, or B2B contracts,
have an actual lawyer review them.
