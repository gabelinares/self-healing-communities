# Site Architecture

The homepage is a sequence of views. The rule since Sept 25: **each view fits one screen** on a
laptop, and nothing inside a view scrolls on its own. Phones flow at natural height.

## Homepage (`index.html`)

| # | Section | Anchor | What it does |
|---|---|---|---|
| 1 | **Opening + the book** | `#why` | The logo, then the main sentence ("Building a new model…"), then a close-up of a child's eyes. Scrolling opens the photo into a book that slides aside as "It begins with seeing differently" appears beside it. Each further scroll turns one page; the copy on the left changes with each spread. |
| 2 | **Lives unfold / the river** | `#wayfinding` | Four life-stage photos (infancy → adulthood) beside the core message. Scattered terracotta dots gather into a flowing emerald stream as you scroll. Founder quote. On phones the photos swipe sideways. |
| 3 | **Old Way / New Way** | `#how` | "We don't work one problem at a time." A drag-to-compare slider over the same community network: tangled and red on one side, connected and green on the other. |
| 4 | **Flagship case** | `#flagship` | "Building a model that can work in practice." Two pillars: Intellectual groundwork; Governance & financing architecture. |
| 5 | **The cycle (spiral)** | `#cycle` | "SHCF brings evidence, community knowledge, learning, and financing together in a continuing cycle." See below. |
| 6 | **Get involved** | `#act` | "Each generation will leave the next stronger." One call to action (the briefing). Coloured dots orbit the centre ("gather around"). |
| — | Footer | | Credit line and links |

### The book (section 1)

| Spread | Copy title |
|---|---|
| Opening | It begins with seeing differently. |
| Page one | Risk can build over time. |
| Page two | ACE-related risk has outgrown the systems built to manage it. ("new normal" + paper link) |
| Page three | Our fragmented programmatic approach is too expensive. ($14.1 Trillion/Year) |
| Page four | Find where change has the greatest reach. (quote: Laura Porter, from *Resilience*) |

Each left-hand page carries a testimonial quote. Scroll timing is set by constants
(`OPEN`, `SETTLE`, `SHIFT`) at the top of the opening's script.

### The spiral (section 5)

- An Archimedean spiral drawn as a moving current of dots on a `<canvas>`, with five steps at fixed
  points on it and **Risk Stewardship** at the core.
- **Desktop:** hover, focus or click a step's oval. The path lights from the centre to that step, and
  its explanation appears in the panel on the left. The five ticks under the panel are a second way in.
- **Circle of leadership:** a stipple circle around the whole figure, with "Expand the circle of
  leadership" forming its top arc. Hovering the lettering lights the circle and the whole path, and
  shows Laura's text.
- **Phone:** the diagram pins to the top of the screen while the steps scroll underneath. Whichever
  step you're reading lights up on the diagram. The circle is the last entry in the list.
- The circle's centre, radius and the lettering's angle were set visually on a design canvas
  (Oct 6) and are constants in the code (`OX`, `OY`, `ringGeo.r`, `TEXT_A`).

## Approach page (`approach.html`)

"A Different Way of Working": a thesis section (photo + "SHCF is not another answer to the question,
'What should we fund upstream?'…") and "Success creates value in more than one way". Shares the
homepage's tokens and footer. **Not linked from the homepage nav yet.**

## Navigation

Fixed top nav: The Science · Our Approach · Community Stories · About · **Get Involved**. Hovering a
link shows a preview strip (an interaction the client liked from the Broad Institute site). Links
currently jump to sections on the homepage. Separate pages for Science, Community Stories and About
are in the approved sitemap but **not built** (see open items).

## Performance and accessibility (as of Oct 7)

- Mobile Lighthouse 82, desktop 91, accessibility 100, best practices 100, SEO 100.
- The opening photo is preloaded at high priority; off-screen photos load after the page.
- Animations pause off-screen, and the opening skips its frame work while the page is at rest.
- Real buttons and links throughout, keyboard reachable, `prefers-reduced-motion` respected.

## Where the reasoning lives

Every decision, with the client quote that prompted it, is in
[`../backlog.md`](../backlog.md) (§1–§17, in date order). The code comments name the same
section numbers.
