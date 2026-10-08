# hero-versions · The website

This folder is deployed to **https://hero-versions.vercel.app**. Only `index.html` and `approach.html` are live; `home.html`, `landing.html`, `banner-options.html` and `ia-sitemap.html` are earlier concepts kept for context.

## Files

| File | What it is |
|---|---|
| `index.html` | The homepage. Each page is self-contained: all CSS and JS are inline. |
| `approach.html` | "A Different Way of Working": the Approach page (thesis + value sections). Not linked from the homepage nav at present. |
| `logo.svg`, `favicon.svg` | Logo (deep emerald, for light backgrounds) and favicon |
| `assets/` | Photography (AVIF/WebP with JPEG fallbacks), `logo-white.svg`, `symbol-emerald.svg`, the compare-slider path illustrations, the social share card |
| `assets/CREDITS.md` | Image sources and licence notes, **read before launch** |
| `.vercelignore` | Keeps `assets/reference/` (client screenshots) out of the deployment |

A few files in `assets/` are not used by the current pages (`elderhood`, `parenthood`, `eyes.jpg`,
`face.png`). They are kept for the life-course options discussed with the client.

## Run locally

No build step and no dependencies. Serve the folder with any static server:

```bash
cd hero-versions
python3 -m http.server 4611
# open http://localhost:4611
```

Opening `index.html` straight from the file system mostly works, but use a server: some
browsers block parts of the page on `file://`.

## Deploy

The site is a plain static Vercel project.

```bash
cd hero-versions
vercel link        # once, to your team's Vercel project
vercel --prod      # deploy to production
```

⚠ Use `--prod`. Plain `vercel` creates a *preview* deploy, and the production URL keeps serving the
old build. That caused a "my changes aren't live" mix-up once during the project (decision log §13).

## Tech notes for whoever edits this next

- **Fonts:** Archivo (variable, Google Fonts) for everything; Fraunces italic only for quoted voices.
- **Images:** every photo is set as `background-image` with `image-set()` (AVIF/WebP + JPEG).
  Photos below the opening carry `data-bg` and load after the page (performance, §17).
- **AVIF images must have even width and height**, or they render blank in Chrome and Safari. Don't
  resize with `sips -Z`.
- **Scroll-driven sections** (the opening book, the river) use a sticky child inside a tall
  scroll area. Size stickies in `svh` and measure the element itself. Never mix CSS `vh` with
  `window.innerHeight`: on iOS they differ by about 85px, and that caused three separate iPhone bugs.
- **The spiral's geometry** (step positions, circle centre and radius) is a set of constants at the
  top of the spiral script, each with a comment explaining why it has that value. Read the comments
  before changing a number.
- Every non-obvious decision is commented in the code where it lives, and logged with its reason in
  `../backlog.md`.
