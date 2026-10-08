# Self-Healing Communities Fund — Website Handoff

**Client:** Laura Porter, ACE Interface, LLC (Self-Healing Communities Fund)
**Prepared by:** Gabriel Linares · Awesomic
**Handoff date:** October 8, 2026
**Live site:** https://hero-versions.vercel.app

This repository holds everything for the Self-Healing Communities Fund (SHCF) landing page:
the production site, earlier concepts, project documentation, the full client conversation,
brand assets and reference material.

---

## Start here

1. **See the live site:** https://hero-versions.vercel.app
2. **Read the overview docs**, in this order:
   - [`briefing.md`](briefing.md): the original brief and goals
   - [`docs/content-guidelines.md`](docs/content-guidelines.md): how the client defines "Self-Healing Communities"; **all copy follows it**
   - [`docs/site-architecture.md`](docs/site-architecture.md): what each section does and how it is built
   - [`docs/open-items.md`](docs/open-items.md): what is still pending with the client
3. **Run it locally:** see [`hero-versions/README.md`](hero-versions/README.md)

---

## What's in the repo

| Path | Contents |
|---|---|
| [`hero-versions/`](hero-versions/) | **The site, deployed from this folder.** `index.html` (homepage) and `approach.html` (Approach page) are live. `home.html`, `landing.html`, `banner-options.html` and `ia-sitemap.html` are earlier concepts and the approved sitemap, not live. |
| [`docs/`](docs/) | Design system, content guidelines, site architecture, open items. |
| [`backlog.md`](backlog.md) | **The decision log**, §1–§17 in date order, with the client quote behind each decision. Code comments cite its section numbers. |
| [`briefing.md`](briefing.md) | The original project brief. |
| `client-feedback*.md`, `backlog-oct01-laura.md`, `meeting-2025-06-01.md`, [`client-docs/`](client-docs/) | Client feedback and meeting notes. |
| `client-response-*.md`, `message-to-*.md` | Every message sent back to the client. |
| `Self Healing Communities Fund logos/` | SHCF logos (SVG and PNG, every colourway). |
| `ACE interface.pdf`, `Flyer_…jpg` | ACE Interface brand reference, SHCF flyer. |
| `assets/photos/`, `image.png`, `image (8).png`, `hero-versions/assets/reference/` | Original photo downloads and screenshots the client sent with feedback (excluded from deploys). |
| [`hero-versions/assets/CREDITS.md`](hero-versions/assets/CREDITS.md) | Image sources and licence notes. |

---

## Project status

- **Homepage: approved and live.** Laura's last response (Oct 7): *"I love it!"*
- The latest round (Oct 5–7) is built and deployed: opening sentence under the logo, the book and
  "It begins with seeing differently" arriving together, the "Expand the Circle of Leadership" ring
  around the spiral, connector lines on the spiral steps, the caption under the spiral, and the
  footer credit wording.
- A performance and accessibility pass shipped Oct 7. On the live site, mobile Lighthouse went
  **50 → 82**, accessibility **96 → 100**.
- **Pending with the client:** see [`docs/open-items.md`](docs/open-items.md). Most
  important: the *Resilience* film clip, the wording for "Building a model that can work in
  practice", and confirming licences for the stock photography before launch.

---

## Key people

| Who | Role |
|---|---|
| Laura Porter | Client. Co-founder of ACE Interface, LLC; final approver on all copy and design |
| Dr. Robert Anda | Co-founder of ACE Interface, LLC |
| Gabriel Linares | Designer and developer, Awesomic |

---

## Related links

- **Design canvas** (spiral positioning, used Oct 6 to set the circle and spiral layout):
  https://claude.ai/artifact/D3gMekgUyBuzHgNRoYHGgk (private until shared from its Share menu)
- **Hosting:** Vercel. The production alias is `hero-versions.vercel.app`. Account access has to
  be transferred separately; this repo contains no credentials.
