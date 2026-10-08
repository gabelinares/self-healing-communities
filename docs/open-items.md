# Open Items

As of October 8, 2026.

## Waiting on the client

| Item | Notes |
|---|---|
| **The *Resilience* film clip** | Laura to send. Goes with the page-four quote in the book. |
| **"Building a model that can work in practice"** | Final wording for the Flagship case section. |
| **Phone step list numbering** | On phones the spiral's steps also appear as a list under the diagram, still numbered. Asked Laura (Oct 6) whether to drop the numbers there too. |
| **Parenthood in the life course** | The "Lives unfold" strip stops at adulthood, but the site's argument is that risk carries into the next generation. Asked whether to swap one stage for parenthood (Oct 5). `parenthood` and `elderhood` images are already in `assets/`. |

## Before launch

| Item | Notes |
|---|---|
| **Getty licence tier** | `gathering` and `deliberation` came from Getty *comp* files supplied by SHCF. Confirm the licensed files replace them. See `hero-versions/assets/CREDITS.md`. |
| **Life-stage photography** | The four life-course photos are still stock placeholders. The brief asks for real contextual photography. |
| **Testimonial quotes** | Check that every quote in the book is real and approved (some were placeholders early on). |
| **Real-device test** | All iPhone fixes were verified in browser emulation and by construction, not on a physical iPhone. One pass on a real phone is worth doing. |
| **Domain** | The site runs on `hero-versions.vercel.app`. A production domain hasn't been set up. |

## Not built yet (from the approved sitemap)

- Separate pages for **The Science**, **Community Stories**, **Who We Work With**, **About** and
  **Get Involved**. The nav currently jumps to homepage sections.
- `approach.html` exists but isn't linked from the nav.
- The client marked a brand video ("Phase 2") as future work. It should follow this site's visual
  direction.

## Small technical notes

- A small layout shift on desktop (Lighthouse CLS 0.056, under the 0.1 threshold). Existed before
  the Oct 7 pass.
- Unused images in `assets/` (`elderhood`, `parenthood`, `eyes.jpg`, `face.png`) can be removed if
  the life-course question above is settled without them.
