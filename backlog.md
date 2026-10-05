# SHCF Homepage — Backlog

Source: client copy draft sent 2026-08-24 (`Web-landing-draft-SHCF-for-Awesomic-8-24-26...pdf`), reviewed 2026-08-26. Low-effort items from that round already shipped to `hero-versions.vercel.app` (see git log / commit history in `hero-versions/index.html`). Everything below is what's left.

## 1. Book content expansion (`#why` section)
The new draft turns the 3-leaf book into 4+ spreads and adds stat-heavy pages the current `.txtpage` layout (title + one quote + attribution) isn't built for. Needs a new page template before this can go in.

- **"Risk can build over time"** page — Dr. Robert Anda quote ("Every experience teaches the body and brain what to expect next...") + ACEs-discoveries paragraph.
- **"ACE-related risk has outgrown the systems built to manage it"** page — stat callouts (27% increase in average ACE score among adults 25–39 between 2009–2010 and 2023–2024; nearly 1 in 4 adults in that group now report 4+ ACEs, vs. ~1 in 6 a decade earlier) + Budget Director quote ("The bills show up in one place, the savings show up somewhere else...").
- **"Our fragmented programmatic approach is too expensive"** page — $14.1 trillion/year economic-burden stat (with footnote marker in source doc) + explanatory paragraph + State Legislator quote.

## 2. New "Flagship Case" section
Doesn't exist anywhere in the current site. Content: two bodies of work (intellectual groundwork for life-course/intergenerational risk; governance and financing architecture), reference to the ACE Study and the films "Paper Tigers" and "Resilience," and a community-member quote ("For years no one asked what my childhood was like. The first time someone did, my life finally made sense." — rural health clinic). Client's draft places it after the How/compare section.

## 3. Imagery
- Replace the abstract network-diagram images with the family/path-in-nature illustration style shown in the client's doc. Client flagged their own reference images as "just AI generated ideas" — final art still needed, not just a swap.
- Life-stage frame photos in the wayfinding section (`assets/infancy.jpg` → `elderhood.jpg`) are still placeholders per [[shcf-homepage]] hard constraints — need real contextual photography, not stock.

## 3b. Open from the Sept 16 round
- **Quote for book page four ("Good decisions require trustworthy evidence")** — asked Laura for one; every other spread pairs the argument with a named voice, so page four currently runs a visible `Placeholder — we need a quote here for parallelism` panel.
- **Image for the page-three/four spread** — placeholder panel reading `Image to come` is live in the book.
- **Wayfinding subhead now echoes its own headline.** The new client headline ends "…to restore them," and the line under it still reads "we can restore the conditions that let it." Flagged to Laura; awaiting her call on changing or cutting it.

## 4. Explicitly "future," not this round (per client)
- Pop-ups on key concepts (ACE, risk, other big ideas) triggered from within the page copy.
- A Laura self-quote in the Act/closing section — authority + how she approaches the work, introduces team members, note on outcomes/confidence that communities can turn the corner and reduce costs.

## 5. Process
- Get client confirmation the low-effort round (scroll speed, wayfinding/How/Act copy) reads correctly before starting the bigger pass above.
- Coordinate scope/timeline with Clara (account manager) — Laura already flagged to her that there's more work and info available.

## 6. Sept 2026 client feedback round (email via Laura's team, 2026-09-14)
Reference screenshots saved to `hero-versions/assets/reference/2026-09-14-client-feedback/`.

- **Before/after path images (`#how` comparison section)**: client picked two path/subway-style diagrams — `path-before-ref.png` (add gaps in the pathways: interruptions in supports, confusion about where help leads) and `path-after-ref.png` (as-is). Confirmed direction: yes, rebuild this section with them. Client floated animating the SVG eventually — **explicitly future scope**, not this round.
  - **Artwork DONE 2026-09-14** → `hero-versions/assets/path-friction.svg` and `path-flow.svg` (66K/53K gzipped). Built from the licensed stock EPS pair Gabriel downloaded; scripts that produced them are in the session scratchpad (`recolor.py`, `add_gaps.py`) — rerun those to re-tune rather than hand-editing the SVGs.
    - *Colour*: the stock art is flattened (7 line colours × a grid-shadow variant × hand-set darker crossings = 66 colours), so it was remapped algorithmically in HSL — hue retargeted per colour family, lightness preserved so crossings stay dark. Friction → terracotta band (hue 3–38°, capped at 38 because past that it reads mustard); flow → emerald band (hue 150–184°). Lightness pulled down hard on the flow side: brand emerald lives at L 17–43% and the stock art at 55–65% read neon.
    - *Background removed* (Gabriel, 2026-09-14): the squared paper ground and its grid are stripped — arrows only, on transparency. Two traps this exposed, both handled in `recolor.py`: (1) the grid is baked into the art twice, as a uniformly darker duplicate of every line *and* as a copy blended toward the paper where a grid line crosses a stroke — both fold back into their base colour or they show as plaid inside the strokes; (2) the art is sliced into tiles along the grid, so with no paper behind them the antialiased seams read as hairlines — each tile is grown by a 2-unit stroke in its own colour to close them.
    - *Placement*: stock "before" left its right 30% empty. Each viewBox is now tight to its own artwork (friction 1868×1700, flow 2426×1700) so the arrows run right off the edge with no built-in padding, and the two share a viewBox *height* so stroke weights still match across the wipe. Flow is flush to the bottom of its box; friction fills its own. Display with `contain`, not `cover` — cover crops arrows off.
    - *Gaps*: 8 cuts via an SVG mask, placed by detecting clean straight single-line runs (rejects junctions, dots and diagonal arrowheads). Sized 2.0 stroke widths along the line and only 1.2 across — wider than that and the rect bites dots and arrowheads passing close to the line, which reads as a broken mask rather than a break. Each candidate is also validated along the cut's full length plus margin: if the perpendicular width changes anywhere in that span (a dot, a crossing, an arrowhead) the position is rejected. Each cut fully severs its segment — the point is that lines read as *disconnected*, with some arrowheads left detached from their stems. Watch the mask coordinate space: it sits on an untransformed wrapper group around the translated artwork, because putting it on the transformed group itself applies the centring offset twice and the cuts land beside their lines as edge notches instead of breaks.
  - **INTEGRATED 2026-09-14.** Panels stay dark (Gabriel's call — a light-panel variant was tried and rejected). The two `<canvas>` node-webs and their ~68 lines of `drawNet` code are gone, replaced by `<img class="cbg">` layers.
    - Each artwork is mirrored (`transform:scaleX(-1)`) and anchored flush to the bottom and to the edge *opposite* its panel's copy, so the arrows run off that edge and never sit under the text. Note `object-position` is set to the **opposite** side of where the art should land, because `scaleX` flips the element after it is placed — friction uses `left bottom` to end up right, flow uses `right bottom` to end up left.
    - `.cpanel.friction .cbg` is scaled to `height:110%`. Its composition is near-square, so at the 50% rest position a flush-right placement sat entirely inside the clipped half and the panel looked empty. The extra scale brings it into view and crops its sparse top rather than any arrowheads. The flow art is wide enough not to need this. **If either composition is ever re-cropped, re-check both the 50% rest state and a dragged state** — that interaction is where this breaks.
- **Brighter orange reintroduced**: client's original site orange, sampled from their reference swatch = `#C36938` (current site terracotta `#C9442F` is more brick-red/muted by comparison). Added as `--terracotta-bright` in `hero-versions/index.html`. Decision: use it in exactly one place rather than scattering it, so it reads as deliberate. Landed it in the wayfinding section (see below) as that one place — flag to client explicitly when sharing the preview, since "one place" wasned't pinned to a location in the original feedback.
- **Wayfinding section "doesn't stand out"**: shipped a first pass to test direction — `.lc-frame` enlarged 300px→340px desktop (196px→216px mobile), and the river-dot color at full gather changed from bright emerald to `--terracotta-bright` (was an emerald pop; now a warm one, echoing the "gather around" section's warm-tones treatment the client already loves). Not yet deployed/sent — Gabriel to preview and confirm the color transition still reads well (start color is already a muted terracotta, so the scatter→gather contrast is now more subtle than the old red→green swap) before sending to client as a direction check.

## 7. Sept 2026 typography + Flagship round (Laura, 2026-09-18)

Two separate deliverables from the same message. Reference screenshot of the type
direction Laura wants to "play with": her own page-three layout (heavy condensed
sans headline with the closing clause in a second colour, big warm stat, serif
italic quote with a rule and an oversized mark, letterspaced caps attribution).

### 7a. Flagship section — SHIPPED into `index.html` (and carried into the type version)
Laura: *"feels a little plain compared with the rest because there aren't any photos or
much color. I don't think it needs photos, but maybe we could bring some color into the
background or the two boxes."* No photos added. Colour came from three places:
- **The section field**: a cool wash from the top and a warm one from the bottom-left over
  the cream→paper gradient, plus the shared `.grain-tex`. It sits between the dark compare
  widget and the dark Act band, so it stays a light breather — going fully dark would have
  put three heavy sections in a row.
- **The arch**, which was a 2px hairline at .5 opacity and effectively invisible. Now a
  drawn form: a 3px stroke on an emerald→terracotta gradient, over a tinted field that is
  **masked to fade downward**. Without that mask the field terminated hard at the card tops
  and read as a grey wedge in the gap between them.
- **The two cards**, tinted rather than cream — cool for the intellectual body of work, warm
  for governance/financing — each with a 5px accent cap, an accent number badge, an accent
  rule under the heading, and a large arc in its own colour echoing the arch. A first pass
  used an oversized cropped numeral there instead; it read as a rendering slip, not a mark.
- The section eyebrow moved off "Flagship case" to "The work underway", because the apex
  pill already says Flagship Case and the two sat one above the other.
- The community quote picked up the reference treatment (rule, oversized mark, ranged left).

### 7b. Version B — a new typographic identity: `index-type.html` + `approach-type.html`
Built as a **separate version so Laura can compare**, not as a replacement. A version
switcher (`.vswitch`, bottom-left, marked `<!-- version switch -->` in both homepages)
flips between them; **delete that block and its CSS once a direction is chosen.**

The identity is a straight inversion of the current one. Today: Fraunces serif display +
Inter body. Version B: **Archivo** (variable, `wdth` + `wght`) carries everything —
display, body, UI — and **Fraunces survives in italic only, for quoted voices**. That is
exactly the split in Laura's reference, and it keeps the warmth of the book spreads and
the pull-quotes, which she has already approved, while the argument type gets louder.

- Display is set from two custom properties, `--disp-wdth` (90) and `--disp-wght` (700),
  so the whole voice retunes from one place. Leading ~1.0, tracking -.03em.
- **`em` inside a headline stops being an italic and becomes a colour break**, and
  `em::before{content:"\A"}` forces it onto its own line so the shape holds at every
  width rather than depending on where the text happens to wrap. `em` colours are
  per-surface: emerald on paper, `--emerald-bright` on the flow panel, `#FFC9B4` on
  friction, `--emerald-bright` on the Act band. Headlines that had no `em` got one.
- Stats are now Archivo 800 in `--terracotta-bright`, not Fraunces in emerald. Page three
  of the book got a `.wc-stats.solo` treatment so `$14.1 Trillion/Year` is the headline act
  of its own page with the sentence under it as a subhead — i.e. Laura's reference, rebuilt.
- **The canvas hero title**: `ctx.font` accepts `font-stretch` in the shorthand (Chrome
  narrows the glyphs even though `ctx.font` reads back without it), so the emphasis line is
  set `700 semi-condensed` to hold the same width axis as the CSS headlines. Without it the
  one headline rendered in canvas sits visibly wider than every other headline on the site.

### 7c. Approach page hero rebuilt (both versions)
Gabriel, 2026-09-21: the spiral was below the fold and its copy below *that*, so the
diagram and the words explaining it could never be seen together. Four changes:

- **The spiral moved into the hero.** `.ap-hero` is now one `100svh` two-column grid —
  headline and step copy left, spiral right — so nothing about the cycle needs a scroll.
  An `.ap-more` cue at the bottom says there is more page below.
- **The step labels stopped being tilted.** They were SVG `<text>` rotated to the spiral's
  tangent (clamped to ±30° so they never stood on end). They are now **HTML buttons
  absolutely positioned over the SVG**, converting viewBox units to stage percentages
  (`(v+560)/1120`). Horizontal at every position, and they can carry a border, shadow and
  hover state instead of the `paint-order:stroke` halo the SVG text needed to stay legible.
  - *Placement trap*: a chip is far wider than it is tall, so centring it on a radial
    offset lays it across the spiral. Each chip anchors its **inner edge** to its dot and
    runs outward (`translate(0,-50%)` right side, `translate(-100%,-50%)` left). Near the
    top and bottom of the circle there is no "outward" horizontally, so when
    `|x| < r*0.42` the chip centres and is pushed clear vertically instead.
  - The hover/active scale has to compose with that anchoring transform, so the anchor is
    stored in `--sp-t` and every transform is written `var(--sp-t) scale(1.05)`.
  - *Muting trap (Laura/Gabriel, 2026-09-21)*: dimming the unselected chips with
    `opacity:.4` fades the **fill** along with the ink, so the spiral showed straight
    through them. The fill is now flat `--cream` (the backdrop-blur went with it, being
    pointless behind an opaque fill) and the recede happens in the ink, border and shadow
    instead. Keep it that way — the curve has to terminate cleanly at a chip's edge.
- **The copy appears in place.** `.ap-panel` sits in the left column with a fixed
  `min-height`, so swapping steps never reflows the page. The six `.sp-ticks` are pinned to
  its bottom edge — they read as position-in-set *and* work as a second way in for anyone
  who never thinks to point at the diagram.
- **It now looks interactive.** Chips are real `<button>`s with pill/border/shadow and a
  pointer cursor; the dots gained an expanding halo on select; the resting panel shows a
  pinging cue dot plus "Pick a step"; and until the first hover, focus or tap the chips
  **breathe in sequence** (`.sp-stage.idle`, staggered via `--sp-d`), which stops for good
  on first interaction so the hint never fights the user. All of it is off under
  `prefers-reduced-motion`.

- **A pulse runs the spiral every few seconds**, so the diagram is visibly alive before
  anyone touches it. Built as four bands that all *end* on the same leading edge and get
  progressively shorter and brighter (`LAYERS`, driven off one shared `strokeDashoffset`),
  which tapers the light behind the head. A single dash would be as bright at its tail as
  at its head, and a linear gradient cannot follow a spiral — stacking the bands is what
  makes the falloff track the curve. The widest band is blurred through `#spGlowF` for the
  halo; a small circle rides the leading edge via `getPointAtLength`.
  - Travel eases as `1-(1-u)^2.4` (out of the core fast, dissipating slow) over 2.9s, then
    rests 5.4s **plus up to 3.6s of jitter** so it never feels metronomic. Opacity ramps in
    over the first 14% and out over the last 24% rather than popping at either end.
  - It **stands down whenever a step is open** — `armed` is lerped, not switched, so
    hovering a chip doesn't cut the light dead — and it is off entirely under
    `prefers-reduced-motion` (the elements are never created). An IntersectionObserver
    parks the loop when the spiral is scrolled past; rAF already handles a hidden tab.
  - Measured at 121fps during travel with the pulse and the six chips both live.

Verified on both versions at 1440x900, 1280x700 and 390x844: hero fits the viewport, zero
rotated chips, tick clicks and keyboard focus both drive the panel, no console errors.
Below 980px the chips and panel hide and the existing straight-read `.sp-steps` list takes
over, as before.

### 7d. A/B parity audit (2026-09-21)
After the approach-page rebuild, checked that the two versions still differ in typography
and nothing else. Diffing them with the cross-links normalised leaves only the `--disp`
token block and the `em::before` rule — structure and JS are byte-identical. Two real gaps
were found and closed:

- **The chip numeral broke version A's own identity.** Every other small numeral on that
  page is Fraunces (`.sp-detail-n`, `.fs-num`, the `.sp-steps` counter), but `.sp-chip .n`
  had no `font-family` and fell through to Inter — so the same "01" rendered in two faces
  at once, on the chip and in the panel beside it. A now sets it in Fraunces; B was already
  on `var(--disp)`.
- **The version switcher only existed on the two homepages.** Following "See our approach"
  from version B landed on `approach-type.html` with no way back to A. Both approach pages
  now carry it, pointing at each other (`approach.html` <-> `approach-type.html`) so
  switching keeps you on the page you are reading.

Computed styles confirmed per element — A: Fraunces display + Inter UI; B: Archivo
throughout. `em::before` stays B-only by design; it is part of that identity, not a bug.

### Open / not done in this round
- **Deploy**: the Sept 18 round (7a + 7b) is live on `hero-versions.vercel.app`. The Sept 21
  approach-page rebuild (7c/7d) is **not deployed yet**.
- **The approach page's return cards never got the flagship card treatment.** `.fs-pillar`
  and `.fs-num` are shared class names but have diverged: on the homepage they are the
  redesigned Flagship cards (tinted fills, accent caps, badge numerals, arc motif), on the
  approach page they are still plain cream cards with a bare numeral. Consistent between A
  and B, so it is not a parity bug — but it is a visible inconsistency between the two
  pages of the same site, and worth a decision before this goes to the client.
- **Pre-existing bug, both versions**: on phones the drag-to-compare panels overlap — the
  friction panel is clipped at 50% while the flow panel's right-ranged copy shows through,
  so the two headlines collide. Present on the current live design too, not a regression
  from this round. Needs a decision: stack the panels below ~720px, or keep the drag and
  move each panel's copy out of the other's half.

See project memory `shcf-aug24-copy-round`, `shcf-sep14-feedback`, `shcf-homepage`, `shcf-todo-jun16` for full design/interaction context behind these.

---

## 8 · Sept 22 — Laura's consolidated feedback round (`Feedback-to-Awesomic-9-21-26.docx`)

Laura spent the weekend merging her team's conflicting feedback into one document. It
contains nine images: two screenshots of the compare section, one of the closing paragraph,
one of page four, the Awesomic illustrator's hand-drawn cascade slide, and three watermarked
Getty comps. She also chose **version B** ("more color and variety in the font").

I triaged the document into what could be built exactly as specified versus what is design
exploration, and did the first group. **8a–8e below are done. 8f–8i are not started.**

### 8a · The green box now carries her five conditions
`index.html` / `index-type.html`. Was four items; "Health and connection flow" is gone,
"Earlier action, less crisis" and "Learning and adapting together" are in. The green panel
now has one more item than the red one — the two are absolutely positioned in the same box
and sized by the taller of the two, so this does not clip on desktop or phone (checked).

### 8b · The closing paragraph under the compare panels
Her replacement text, verbatim. Two notes: it says "SHCF" where the old line said "The
Fund", and it drops "make sure what works is what is done" — a phrase she wrote herself in
an earlier round, so the new version is taken as superseding it. The `<b>` emphasis follows
the old rhythm: the opening concept, then the closing claim.

### 8c · Page four of the book, including the quote we had been waiting for
`#why` article four: new headline `Find where change has <em>the greatest reach.</em>` and
her two paragraphs. The Laura Porter quote from *Resilience: The Biology of Stress and the
Science of Hope* replaces the `q-ph` placeholder on leaf 3 — that placeholder had been
sitting in the book since Sept 16 precisely so the gap stayed visible.

The film title needed a treatment that was not there before: `.q-attr .q-src` sets it in
Fraunces italic under the speaker, in both versions. B keeps Fraunces for quoted voices, so
this is the same rule in both files rather than a divergence.

**The `ph-face` "Image to come" on the recto of that leaf is still there** — that is the gap
Laura's three Getty comps are meant for.

### 8d · The particle river reads much harder now
Her note: "can you make more contrast so the dots/flow shows up more? We like that feeling
a lot." Five changes in `tickWf`: density `/2400` → `/1950`, radius `2.8+1.4` → `3.2+1.8`,
alpha `(0.42+0.5p)` → `(0.55+0.45p)` so it reaches full strength instead of topping out at
.92, and the readability scrim under the copy softened from .97/.86/.50 to .94/.78/.38.

The fifth is the one that mattered most: **the dots used to lighten as they gathered**
(201,68,47 → 195,105,56), so the flow state — the thing the section is about — was the
least visible thing on screen. They now deepen instead (→ 170,78,38).

### 8e · The spiral: five steps, her copy, her centre
Six steps → five, with her names and descriptions and `RISK STEWARDSHIP` in the core.

**Geometry.** Five steps advancing 144° land exactly 72° apart, because 144×5 is two whole
turns — the set closes on itself. `TMAX` moved 23.570 → 21.991, which is not cosmetic: it
puts the *last* step (furthest out, so the one whose chip has least room) at the bottom of
the stage, where the chip is centred and pushed clear vertically. At the old `TMAX` it
landed dead-left and drove a 196px chip straight through the copy column.

**Her copy is 3–5× longer than what it replaced** (up to 400 characters against one short
sentence), and the whole point of the Sept 21 rebuild was the hero fitting on one screen
with no scroll. Four changes absorb it without breaking that: panel `min-height`
`clamp(258px,33vh,304px)` with `padding-bottom:20px` so the text can never reach the ticks,
step heading capped by `3vh` as well as `2.2vw`, body `clamp(14px,1.65vh,15.2px)`, measure
50ch. Verified: hero fits at 1440×760, 1280×800, 1440×900 and 1680×1050, and the longest
step (02) does not overflow the panel at any of them.

**Chips wrap now.** "Learn continuously across investments" is 36 characters; on one line it
ran off the stage. `white-space:nowrap` is gone, `max-width:168px`. That value is load-
bearing in both directions — wider and chip 03 collides with the step copy, narrower and the
chips turn into four-line blocks. Measured ink clearance between the copy and every chip is
positive at all four viewports (tightest: 18px).

### 8f–8i · Not started *(superseded — 8f, 8g and 8h are done in 8m below; 8i still blocked on Laura)*
- **8f · "EXPAND THE CIRCLE OF LEADERSHIP"** on the outer edge of the widening spiral,
  visually distinct from the five steps so it does not read as a sixth. Her own idea and the
  best note in the document. Text on an SVG path along the outer arc; expect iteration.
- **8g · A river/stream variant of the compare graphic.** She asked for it *without losing
  the current one*, so this is a third option, not a replacement.
- **8h · The spiral built from clustered dots that densify outward.** Her idea, tying the
  spiral to the wave section she likes. Keep the path for geometry and render dots along it
  so hover, trail and pulse all still work. Prototype before promising it.
- **8i · The Getty photos.** Watermarked comps, so nothing to implement. They are also
  corporate stock meeting rooms against a site of documentary portraits — worth saying
  before she spends money.

**Cannot do: the hand-drawn cascade illustration.** That is the Awesomic illustrator's work
and it lands the idea better than vector would. Either she sends the source, the illustrator
finishes it, or it is skipped — not something to approximate.

### Still open from round 7
The approach page's return cards never got the flagship treatment (§7), and the phone
drag-to-compare overlap is still there (§7). Neither is touched by this round.

### 8j · Collapsed to version B (done)
Laura picked B, so the A/B comparison is over. `index-type.html` and `approach-type.html`
are now `index.html` and `approach.html`; the originals are deleted, the `-type` suffix is
gone from every internal link, and the `.vswitch` stylesheet block and markup — both tagged
`REVIEW ONLY` for exactly this moment — are removed.

The site is now four files' worth of work in two: Archivo carries display and body, Fraunces
survives italic only for quoted voices (the book pages, the wayfinding quote, the Laura
Porter film citation). The `em::before` colour-break rule is no longer a B-only divergence —
it is simply the house rule.

Version A as it stood at the moment of the switch is archived in the session scratchpad as
`versionA-index-final.html` / `versionA-approach-final.html`. `index.html` also has its
pre-round-7 state in git history; `approach.html` never had a commit, so the scratchpad copy
is the only record of version A's approach page. Worth a commit if that matters.

Everything in §7d (the parity audit) is now moot — there is nothing left to keep parallel.

### 8k · Clockwise reading order (done)
The numbering did not follow the eye. With a 144-degree advance the five steps were evenly
spaced and easy to fit, but the set wound twice round before closing, so sweeping the
diagram clockwise met them **1 4 2 5 3**. Now it is 1 2 3 4 5 from any starting point.

Getting there is not a matter of moving dots. A 72-degree advance is the only spacing that
gives clockwise order, and five steps at 72 degrees occupy **exactly one turn** — which is
the whole difficulty, because one turn inside a fixed radius cannot show the line passing
inside itself. Two intermediate attempts are worth recording so they are not retried:

- **K 46.26, TMAX 9.77** (steps spread 223 -> 456, line stopping at step 05). Clockwise, all
  clearances fine, but with only 1.55 turns and the core fade hiding the lead-in it read as
  a plain circle. Pulling the fade in from 118/224 units to 31/123 barely helped — at that K
  the whole lead-in is packed into the masked centre.
- **K 25.90, TMAX 17.45** (line continuing 280 degrees past 05). Two full turns, a proper
  spiral — but the steps compressed into r 199..329 and sat crowded against the centre
  label with a bare outer ring.

**Superseded by 8l — see below. Was: K 29.855, TMAX 15.140, STEP_T [6.7735, 8.0301, 9.2867,
10.5434, 11.8000].** The
line runs ~190 degrees past step 05. That buys 1.78 visible turns (so it reads as a spiral)
while keeping the steps spread over r 206..356.

Parameters were chosen by sweeping `t5` and the overshoot against **real chip boxes**
measured from the page, not estimates — chip widths, the centre label's true ink extents
(144.6 x 82 units, much narrower than its 36% box) and the copy column's right edge. The
chosen point sits in a feasible window 0.33 wide rather than on an edge. Verified at
1280x800, 1440x760, 1440x900, 1680x1050 and 1920x1080: clockwise order `12345` at every
size, radii strictly increasing, no chip overlaps, 54-147px of ink clearance to the copy
(was 18px at its tightest before), hero still fits, trail lights progressively 0.21 -> 0.62,
pulse running, no console errors.

**Two useful side effects.** Hovering step 05 now lights only ~62% of the line, so the
diagram visibly has somewhere left to go — and that unlit outer sweep is exactly where
"EXPAND THE CIRCLE OF LEADERSHIP" belongs (§8f). It is the one part of the figure that is
not a step, which is what the client asked for.

Also in this round: the core fade now reveals from 123 units instead of 224 (it must clear
the label ink, which the curve only crosses below ~118), and the track ribbon widens harder
from hairline to 3.4 units, since a single-turn form has to carry the unfurl by thickness
rather than by wrapping.

### 8l · Step 01 rotated to centre-left (done, supersedes 8k's parameters)
Step 01 was at 298 degrees — top-right — so the eye came off the headline on the left and had
to travel across the diagram to find where the sequence began. It now sits at **192 degrees**,
centre-left, level with the core label, and the rest follow clockwise from it.

**Shipped: K 36.545, TMAX 12.368, STEP_T [4.9218, 6.1785, 7.4351, 8.6917, 9.9484].**
Bearings 192 / 264 / 336 / 48 / 120. The line still runs ~140 degrees past step 05.

The brief was "01 should be where the 5 is" (226 degrees). **That specific bearing has no
solution.** The five bearings are locked 72 degrees apart, so fixing 01 fixes all of them, and
putting 01 at 226 puts 05 — the largest radius, and so the widest chip — at 154 degrees, hard
left, straight through the copy column. Every overshoot value from 0 to 360 degrees was swept:
the copy-column gap is negative or single-digit throughout. 192 degrees is the closest the
geometry allows to centre-left, and the feasible band runs 168..205 degrees, so it is not
balanced on an edge.

This is a better layout than 8k on every measure, not just the requested one: the steps now
spread over r 184..368 (span 184, was 150) and the nearest chip ink is 133-263px from the
copy (was 54-147). Verified at five viewport sizes: clockwise `12345`, radii strictly
increasing, no chip collisions, hero fits, trail lights 0.18 -> 0.66, pulse running, no errors.

---

## 8m · The flow, the outer band, and the two deferred decisions (Sept 23)

Gabriel: *"for the river/stream variant, you can keep the spiral, just change the line to
nice organic circles moving outwards and fading on a stream that goes back to the center
from below."* That folds 8g and 8h into one change and does it on the spiral rather than on
the compare graphic.

### The line is a current now
`.sp-track` — the filled ribbon — is gone. The spiral is drawn as ~1050 dots running outward
from the core, widening and deepening as the radius grows, on a **canvas** under the SVG.
Canvas rather than SVG because 1050 nodes at four attribute writes each per frame janks a
mid laptop; on canvas it is one fill. Measured 115–122fps at 1440x900.

The SVG keeps what needs to stay crisp and interactive: the hover trail, the step markers,
the chips and the band.

### The return
It surfaces rather than loops. Two routes were built and thrown away first:

- **Around the outside of the frame.** The stage has ~100 units of margin past the spiral and
  the chips occupy most of it, so half the stream sat behind a chip.
- **A wide off-canvas sweep** from the spiral's end all the way round. Nearly half the dots
  were then drawing something nobody could see, which starved the spiral itself — that is why
  the first render looked sparse and clumpy.

Shipped 09-22: the current fades out where the spiral ends, and a separate short stream rises
from below the bottom edge into the core.

**Removed 2026-09-23** (Gabriel, on a screenshot with the stream boxed in red: "this part is
weird, remove the dots on that path"). On the page the short return read as a stray dotted
tail hanging off the centre label and down out of the frame, competing with the spiral's own
line. There is no drawn way back now: a dot dissolves at the end of the sweep and surfaces in
the core under the label's fade. The whole journey between is underground. `RET_*` and `bez`
are gone from `approach.html`; `SPIRAL_U` is 1; `NDOT` went 1050 → 820, since about a fifth
of the dots had been spent on the leg, so the spiral's density is unchanged. Verified: no
console errors, the swell still runs the sweep, the outer band unchanged.

### The pulse became the swell
The old pulse was its own set of SVG bands riding the line. With the line gone it read as a
green smear. It is now a brightening that travels **along the current** — same event, same
cadence and stand-down behaviour, carried by the water instead of drawn over it. Only the
crest reaches `--emerald-bright`; the rest lifts to `--emerald`.

### 8f · The outer band
`EXPAND THE CIRCLE OF LEADERSHIP` follows the spiral's own curve, offset 38 units outward,
extended past where the line stops so the words sit **across the top of the stage where they
read horizontally**. The client asked for this to follow the widening edge; she also asked,
earlier, that step names never tilt. Both hold, because this is not a step — it is the label
on the sweep the steps produce. It mutes when a step is open.

### Two decisions that had been sitting open since §7
- **The approach page's return cards** now use the Flagship card treatment. They had been
  sharing the `.fs-pillar` class name while looking nothing alike. Three returns rather than
  two, so there is a third tint — deep forest — which keeps the trio in palette.
- **The phone compare panels** stack below 720px. The drag needs each panel to be wide enough
  that its clipped half is still a readable column; at 326px both headlines and every bullet
  were cut through the middle of a word and the two halves collided. Measured six text
  collisions before, zero after. The handle, the hint and the drag JS all stand down.

### Still open
8i — the Getty photos and the cascade illustration — is blocked on Laura, not on us.

### 8n · Core kicker, dot spread, and a full-bleed figure for the thesis band (Sept 23)
- **"At the centre" removed.** The core says its own name. Its bottom margin had been
  pushing "Risk Stewardship" low in the circle; without it the label centres properly.
- **Wider dot spread**, skewed small: roughly 0.5x-2.1x (was 0.7x-1.45x), weighted toward the
  fine end so the current reads as many small drops with the occasional coarse one.
- **The thesis band was centred copy in a full-width strip** — a lot of empty paper either
  side and no reason for the section to be as tall as it was. It is now a two-column band:
  a large placeholder figure running off the **left edge of the screen with no margin**, and
  the words in the column beside it, their right edge aligned to the page wrap. The column
  gives the prose its measure, so no text here carries a width of its own — see the standing
  rule in memory `no-text-width-caps`.

That figure is a real gap, not decoration: it is one of the places Laura's photo choice can
land, and it uses the same "Image to come" placeholder language as the book's page four.

### 8o · Stand-in photography for the two open image gaps (Sept 24)
Both placeholders are filled so the pages read as finished:
- **Book, page four recto** — `gathering.jpg`, a group sitting together in a park in low sun.
  It faces the Porter quote about getting the science "into the hands of the general
  population," which is what the picture shows.
- **Approach, the thesis band** — `deliberation.jpg`, a diverse group working a problem out
  at a flipchart, one of them a wheelchair user. On message for "answering harder questions
  together."

Both StockSnap, CC0, commercial use, no attribution. Details in `assets/CREDITS.md`.

**These are stand-ins and the reasons matter.** CC0 covers the photographer, not a model
release, and both show identifiable people — which is exactly the release Getty sells and the
real argument for Laura buying. They are also 960px on the long edge, the most StockSnap
serves, against 1600px for the rest of `assets/`.

And the honest note: the free CC0 pools have no community-deliberation documentary
photography, so `deliberation.jpg` is a meeting-room picture — the same objection raised
about Laura's own Getty shortlist. It strengthens rather than weakens the case for her
choosing properly.

The `ph-face` / `ph-mark` placeholder CSS is removed; it has no user left.

---

## 9 · The cycle joins the landing sequence, and every view fits one screen (Sept 25)

Two notes arrived together.

**Laura:** *"I like the new draft of the approach page. I think the spiral could be more
dominant because it catches the eye and is helpful for conveying our cyclic way of working.
I wasn't thinking of this as a separate approach page. I was thinking of it as the second to
last view in the landing page sequence. Then, the approach page could be a document or an
interview or a video."*

**Her colleague:** *"I'd like to see the last two sections ... each fit within one screen, as
the other two sections do ... you know how we stop everything on the screen while we scroll?
do the same with the fit, but without the scroll."*

### 9a · The spiral moved, and grew
The whole cycle view — copy column, step panel, ticks, spiral, flow canvas, outer band — moved
out of `approach.html` and into `index.html` as `<section class="cycle" id="cycle">`, sitting
between the Flagship case and Get Involved. Scope was confirmed as **the spiral view only**:
the thesis band and the three returns stay on `approach.html`, which is now the stub for the
document, interview or video she has in mind.

It is `.cycle` rather than `.ap-hero` now, because it is no longer a hero. All JS references
were already by id, so nothing in the behaviour had to change.

**Dominance.** The stage went from 560px to **756px at 1440x900** — 35% wider — by giving the
copy column less of the grid (`.88fr` -> `.56fr`) and letting this one view run wider than the
page wrap (1180 -> 1320). Ink clearance between the chips and the copy actually *improved*,
from 265px to 344-436px, because the copy column narrowed faster than the chips moved out.

Links: nav, footer and the compare section's hand-off now point at `#cycle`. `approach.html`
has no inbound links from the landing page and no self-links; it is reachable by URL only,
which is what a page awaiting new content should be.

### 9b · One screen per view
`.how`, `.flagship` and `.act` are each `min-height:100svh` with their contents centred. **Not**
scroll-jacked: the book and the river get their full-screen feel from a sticky child inside a
tall scroll-area, and the colleague explicitly asked for the fit without the scroll.

Every internal measurement is now capped against viewport **height** as well as width, so on a
short laptop the contents shrink rather than overflow. Verified at 1440x760, 1440x900 and
1680x1050: all four views are exactly one viewport tall, and every section head clears the
fixed nav (tightest: 11px on Flagship at 760).

`.act` was not in the brief but was the one section left breaking the rhythm — 842px against a
760px viewport — so it got the same treatment.

**Two traps worth recording.**
- A flex item with `margin:0 auto` shrink-wraps to its content. Making these sections flex
  columns silently cut `.wrap` from 1180px to 607px and took the compare box down with it.
  Fixed with `width:100%` on the direct `.wrap` children.
- The padding could not simply be reduced to make room. The nav is fixed and ~65px tall, so
  landing on a view put its eyebrow underneath it. The padding was *moved* to the top rather
  than trimmed, and the difference clawed back from the compare height and the arch.

Below 820px none of this applies — a phone screen cannot hold either section, and pretending
otherwise only crops the content, so they flow at their natural height again.

### 9c · "Flagship Case" renamed (Sept 28)
Laura: *"several people are concerned with the heading 'Flagship Case'"*. The heading is now
**Building a model that can work in practice**, followed by her sentence about the detailed
implementation case.

Two judgment calls worth knowing about:
- **Sentence case, not her Title Case.** Every other heading on the site is sentence case with
  a full stop; hers would have been the only one in caps. Her words, house typography. Easy to
  put back.
- **The arch pill said "Flagship Case" too.** Changing the heading while leaving the phrase on
  the pill directly under it would have defeated the point, so it now reads "Implementation
  case". She only asked about the heading, so this one is flagged to her.

Her sentence is half as long again as the line it replaced, which broke the one-screen fit from
§9b (flagship went to 925px against 900). It buys the room back across rather than down — the
head runs to 840px and the lede is uncapped inside it, so the sentence sets in two lines rather
than four. All four views are one viewport again at 760, 900 and 1050.

The `.flagship` class and `#flagship` id are unchanged — internal names, not visible, and
renaming them is churn with no benefit to her.

---

## 10 · The phone pass (Sept 29)

Gabriel, with six screenshots off an iPhone: the hero's text sat on the photograph, the
margins and gaps were wrong, the book's pages flickered and showed the wrong pictures, the
life-course caption was cut off and its card ran under the nav, the Gather Around dots sat on
the words, and "the spiral is weird. I don't know what to do. Do you have any suggestions?"

### 10a · One root cause under three of them: `vh` is not `innerHeight`
`#why .sticky` and `#wayfinding .sticky` were `height:100vh`, and every JS placement inside
them — the clip box, the book, the copy column, the intro paragraph — was computed from
`window.innerHeight`. On iOS Safari those are **two different numbers**: `vh` means the
viewport with the URL bar hidden, `innerHeight` means the viewport as it is right now. With
the bar showing they differ by ~85px, so the whole opening was laid out for a frame taller
than the one on screen. The intro paragraph landed on the photograph, the bottom was cropped,
and the life-course card was pushed up under the fixed nav.

Both stickies are `100svh` now — the small viewport, which never changes as the bar comes and
goes — and the script reads `stickyH()`, the measured element, never `innerHeight` again.
`progressOf` takes the pinned child's height for the same reason. **Do not put `vh` back.**

### 10b · The headline ran off both edges of a phone
Two faults stacked. The size was measured on a **detached** probe canvas: a canvas in the page
inherits `font-variation-settings:'wdth' 100` from `body`, which overrides the `semi-condensed`
in the canvas font shorthand, but a detached one inherits nothing and keeps the condensation —
so the probe reported a string 12% narrower than the one actually painted. And the measuring
happened before Archivo had loaded at all, because the webfont stylesheet is deliberately lazy
(`media="print"` then swapped) and `fonts.ready` can resolve before it is even requested.

Now measured on `titleCtx` itself, twice (a variable font's advance is not linear in size), and
only after an explicit `document.fonts.load()` for the two weights the headline draws in.
The phone side margin went 0.94 -> 0.88 of the canvas, which matches the photo box's 6vw.

The resting frame also moved: `curBox()` on a phone was `t:44,b:31`, which left a dead band the
depth of the photograph between the headline and the picture. Now `t:37,b:28`.

### 10c · The book showed two pictures at once
`backface-visibility:hidden` is not reliable on iOS inside a `preserve-3d` subtree that is
itself being scaled — and `book-zoom` is scaled every frame. Sometimes the verso bled through
the recto; sometimes the recto was culled at 0deg and you saw straight past the leaf to the
page beneath, which is why page one showed the base photographs instead of its quote.

`backface-visibility` is **gone**. Which face is showing is decided in `tickWhy` from the angle
we already have, written only when the side actually changes. Verified across the turn: exactly
one face visible per leaf at every sampled position, sides advancing cleanly 1 -> 4.

### 10d · The life-course card
Caption overflowed its frame by 27px on the longest stage name. The label is its own element
now and stacks above the name on a phone, with the separator dropped.

The card also grew in both directions as the life unfolded, so it climbed under the nav (top
went 47 -> 7 against a 61px bar). On a phone the **height is fixed and only the width moves**,
which is what Gabriel asked for — there is no vertical room to spend. The travel widened to
180 -> 300px to compensate. `--navh` is published from the real nav height and the view pads
itself clear of it. Top is now a constant 89 at every stage.

### 10e · Gather Around
The orbits are sized from the SHORT side of the section, so on a phone all three rings ran
straight through the copy. The dots are not moved: they fade over the copy's measured box and
come back on the other side, so the gathering still reads as a gathering. On narrow screens
the rings are also sized from the long side so they orbit around the column rather than sit on
it.

### 10f · The spiral at phone size — what it became
The desktop diagram does not survive being shrunk. 820 dots across a 300px stage read as grain
rather than a current; the labelled chips have nowhere to go so they are hidden; what was left
was five unlabelled rings over a list with no visible connection to them. Decoration — when the
client's whole reason for wanting it bigger was that it "conveys our cyclic way of working".

Same geometry, different instrument below 980px:
- the curve is **drawn** (`.sp-base`), one continuous line, instead of implied by moving dots;
- every step is **numbered on the curve**, set outward of its node and knocked out of the line
  behind it, so the clockwise 01-05 order is readable standing still — which is the entire
  reason the 72-degree spacing was fought for in §8k;
- the diagram **sticks** while the five steps scroll under it, and the step being read lights
  its own node and the arc leading to it. Same gesture as the desktop hover, carried by the one
  input a phone always has.

The steps stay below the diagram — Gabriel: "I like the idea of letting the text below".

Two things that had to change to make it work:
- `.cycle` is `overflow:clip`, not `hidden`, on a phone. `hidden` makes the section its own
  scroll container and a sticky child of a box that never scrolls never sticks.
- The core label kept its share of the width when shrunk, so relative to the figure it GREW
  until it sat on top of steps 01-03. It is a caption at this size (46% / 14px), not a headline.
  This was a large part of why the diagram read as a tangle.

The `<ol>` moved inside `.wrap` so the pinned stage has a parent tall enough to stick against,
and `.ap-grid` is `display:contents` on a phone. Desktop is untouched — verified: chips, dot
current, hover trail and ticks all unchanged, and the four one-screen views are still exactly
one viewport at 900 and 760.

### 10g · Also found
The footer links overran a 360px screen by 14px and broke across words. They wrap now, with
each label whole. Fixed on both pages.

### 10h · Corrections after the second phone pass (same day)
Gabriel, on a screenshot of 10f: *"text being cut, and you lost completely the dots flowing,
everything that is nice. adjust the size to make the dots bigger. besides, the text below dont
need to fade, all of them can be normal colors"*. Three things, all fair:

- **The current is back.** Replacing it with a plain drawn line threw out the best thing about
  the figure. The real problem was never the dots, it was their SIZE: a dot's radius is in
  viewBox units, so on a 310px stage the same dots that draw 0.3-3.9px on a 760px desktop stage
  drew a third of a pixel and vanished into grain. `sizeBoost()` scales them back to roughly
  their desktop apparent size (capped at 2.6x). `.sp-base` survives only as a very faint thread
  at .16 alpha, holding the form together between the dots.
- **No fading of the steps.** Every step reads in its normal colour. Which one you are on is
  carried entirely by the lit node and the path drawn to it on the diagram above — greying out
  four fifths of the copy to say the same thing was too heavy a hand.
- **The sticky band had a hard top edge**, which sliced the headline clean through while the
  stage was still in flow, before it had pinned. It fades at both ends now and only reaches
  26px above the stage: once pinned the stage sits at navh+8 and the nav covers the rest.

### 10i · One tone behind the diagram (Sept 29)
Gabriel: *"can you change the background color of the spiral to match the background color
below?"* Measured: the pinned band was `#F7EFDE` (247,239,222) and the paper the steps sit on
was `#E8D6B8` (232,214,184) — a 15-point step.

The cause is that `.cycle` carries a radial gradient sized to the SECTION, and on a phone the
section is ~1690px tall, so the gradient has already reached its last stop long before you get
to the diagram. Matching the band to a moving gradient would mean recolouring it on scroll, so
the section is simply **flat `#E8D6B8` at phone widths** and the band and the numerals' knockout
stroke use the same value. Sampled top to bottom afterwards: uniformly (232,214,184), +/-1 from
the grain. The band is no longer visible as a band — text just fades as it passes behind the
diagram. Desktop keeps its gradient, where there is no band at all.

**If you retune any one of these three, retune all three:** `.cycle` background, `.sp-stage::after`
and `.sp-num`'s stroke.

### 10j · The book, second attempt (Sept 29)
Gabriel: *"the book bugs on mobile are still happening, the images changes abruptly and the
images are wrong sometimes, make sure this doesnt happen"*. §10c had only hidden the back face
by hand; it had not removed the reasons the mechanism was fragile. Three separate defects:

**1. `container-type:inline-size` on `.leaf` — dead code that cancels the 3D context.**
Nothing in this file uses an `@container` query or a `cq` unit; it was left behind. But
containment removes the preserve-3d rendering context a page-turn depends on, so
`backface-visibility` had nothing to cull against. Chrome tolerated it (verified in an isolated
test — both faces render correctly at 0deg with and without it), which is exactly why it only
ever showed on a handset. **Removed. Do not put it back.** With a real 3D context,
`backface-visibility:hidden` is correct again and is back as a second guard.

**2. The face state was cached on the element.** §10c only wrote visibility when the side
changed. If one style write were ever dropped — a recomposite, a frame lost to a momentum
scroll — that leaf stayed wrong permanently, showing the other page's picture. It is written
every frame now; the same value twice is a no-op for the style system, so it costs nothing.
Verified across the whole scroll range on a touch-emulated device: **204 leaf states sampled,
exactly one face visible per leaf at every one, always the geometrically correct one.**

**3. The easing was the "abrupt" part.** `whySmooth` chases the scroll with `lerp(...,0.14)`.
That smooths a mouse wheel's coarse steps, but on iOS requestAnimationFrame can be starved
during a momentum flick: the target runs away while `whySmooth` sits still, and when frames
resume the book races through several page-turns at once. A finger already supplies the
smoothing, so on a coarse pointer the book now tracks the scroll exactly, and `scroll` — which
keeps firing through a flick where rAF does not — drives the tick as well as rAF.

Measured, jumping from 30% to 80% of the opening in one step:

| | frames until the book settles |
|---|---|
| touch (before) | never settles inside 40 |
| touch (after) | **1** |
| pointer (after) | 27 — the wheel easing is unchanged |

Note for testing: `html` has `scroll-behavior:smooth`, so `scrollTo(0,y)` in a probe animates
the scroll and hides exactly this measurement. Use `scrollTo({top:y,behavior:'instant'})`.

### Not verified on a real device
All of the above is verified in Chrome at 1440/820/390/360 and by measurement. The iOS-specific
faults (10a, 10c) are fixed **by construction** — by removing the dependency on the browser
behaviour that differs — rather than by reproducing them here. Worth one pass on a real handset.

---

## 11 · Housekeeping the substantive backlog left behind (Sept 30)

Everything from Laura's September document is built and the rest is blocked on her, so this is
the two things that were still genuinely missing rather than invented work.

### 11a · The link had no share preview
Neither page carried a single `og:`, `twitter:` or `description` tag. Pasted into an email,
Slack or a post, `hero-versions.vercel.app` rendered as a bare grey URL — and Laura is
circulating it (her Sept 28 note, "several people are concerned with the heading", is a person
forwarding a link). That bare URL was the first thing a board member saw.

Both pages now carry a description, canonical, theme-colour, the full Open Graph set and
`twitter:card=summary_large_image`.

The card itself is generated, not a photograph: `assets/share-card.jpg`, 1200x630, built from
the site's own gradient, logo, fonts and headline so the preview and the page are obviously the
same object. The source is `scratchpad/card.html` — **regenerate it from there if the headline
ever changes**, rather than editing the JPEG.

**⚠ Four hard-coded absolute URLs.** `og:image` will not resolve a relative path — scrapers do
not run the page — so the domain is written out in `canonical`, `og:url` and `og:image` on both
pages. All four need changing the day this moves off the preview domain.

### 11b · Half a megabyte arriving before anything that needed it
Measured on a throttled phone connection (4 Mbps, 150ms RTT): 1.74 MB over 20 requests, load
event at 3.69s. The two heaviest items were `path-flow.svg` (241 KB) and `path-friction.svg`
(223 KB) — the drag-compare artwork, which lives in the third section and cannot be seen for a
long scroll. They are `<img>`, so `loading="lazy" decoding="async"` was the whole fix. Same for
the footer mark on both pages.

**1.74 MB -> 1.24 MB, 3.69s -> 2.67s.** First contentful paint was already 300ms and is
unchanged; this is the tail, not the opening.

Not deferred: the life-course photographs and the book's pages. They are needed within the
first scroll and popping in would be worse than arriving early.

---

## 12 · Laura's Oct 1 round — part one (Oct 1)

Her list ran to 18 items; these eleven were confirmed to build. The spiral work (step names on
phone, the double loop, moving the diagram and its explanation together), the opening headline,
"new normal" and the film clip are not in this pass.

### 12a · Copy, straightforward
- **"public"** added: "We keep treating and financing connected **public** problems as separate
  ones."
- **Both water references deleted** from the river view — the eyebrow "Like water finding its
  way" and the line "We can't force a river to flow; we can restore the conditions that let it."
  She considers the rest of that view strong and the metaphor a distraction. This also closes the
  subhead-echo question that had been open since §8i.
- **The founder quote** now ends "…but now **the whole community is working to solve the problem
  together**", putting the community at the centre rather than the Fund.
- **Closing view**: Stewardship for impact leads the three lines; "A short read · no obligation ·
  unsubscribe anytime" and the "Gather around" eyebrow are gone (the ring of dots already says it).

### 12b · "Old Way" / "New Way"
The two compare panels carried an eyebrow AND a display headline ("One fix at a time" + "Leaning
on constant rescue"). Both are replaced by a single two-word label. The friction panel is the one
clipped from the left, so the drag reads left-to-right as old -> new.

Her reason was that it "would put the lists below in a more dominant place — and we like those
lists", so this is not only a deletion: the heading drops from clamp(24,…,50) to
clamp(22,…,38) and the list rises from clamp(13.5,…,18) to clamp(15,…,22) with the gaps opened
out. `.ctag` and its three colour rules are deleted; nothing used them.

### 12c · The life course is a grid, not a sequence
*"two reviewers still find it difficult to do the scrolling and seeing the change"* — so the
scroll-driven sequence is gone. Four stages (infancy, childhood, adolescence, adulthood) sit
side by side and the comparison is simply there to be looked at. All of its state —
`lcImgs/lcFrame/lcStage/lcBar/STAGES/lcWidth`, the growth curve, the per-stage progress bar —
is deleted. **The river's own scroll (scatter -> flow) is untouched**; only the photographs
changed. Parenthood and elderhood are no longer used on the page.

On a phone they slide sideways rather than stacking (Gabriel's call): a 2x2 grid at 390px makes
each stage too small to read a face in, and four stacked eats the whole view. The next tile stays
half in frame, which is what says it scrolls.

**⚠ `min-width:0` on both `.lc-grid` and `.lc-rail`.** Without it the flex rail's content width
(814px) wins the `1fr` column's auto minimum, the column grows to fit, and the copy is shoved off
the side of the screen. That is exactly what happened on the first attempt.

### 12d · "It begins with seeing differently" leads
*"can you open with the left side so the first thing that people read is 'It begins with seeing
differently'… that would be consistent with the other page turning."* **This instruction is
ambiguous and the reading here is a judgement call** — that line is already the first copy in the
book, so it cannot be about ordering. What it was not doing is being read *first*: it came up at
the very end of the book's slide (esh 0.6..1), by which time the book had landed and taken the eye.

It now rises during the slide and is at full strength the moment the book clears the copy column
(measured: esh 0.86, book left 545 against a column ending at 541). The words are read, then the
book settles in beside them.

It cannot start earlier than that. The book's path crosses this column, so bringing the text up
sooner just prints it under the photograph — which is what the first attempt at this did.
**If Laura meant something else, this is one constant.**

---

## 13 · Recovering work done on another machine (Oct 5)

Gabriel: *"i have done a lot of changes on the current website but with other computer locally,
i think its deployed on vercel but its not here"*.

**Why nothing came across: this repo has no git remote.** `git remote -v` is empty, so the two
machines share nothing. The only copy of that work was the build output sitting on Vercel.

**And it was never live.** Those deploys went to **Preview**, not Production — `vercel` without
`--prod`. `hero-versions.vercel.app` was still serving the Oct 1 build, so the client never saw
any of it. Two previews, both Oct 2:

| | |
|---|---|
| `self-healing-communities-qlpwcfpou` | earlier — everything below **plus** the double-loop arc |
| `self-healing-communities-gb4wdo5xu` | later — the same, with the double loop taken back out |

Recovered from the later one, which is the latest intent. It is built on top of the Oct 1 commit,
so it is a clean superset — five diff hunks, four of them real, the fifth Vercel's injected
`vercel.live/feedback` preview script, which was stripped. `approach.html` and every asset are
byte-identical, so all of it is in `index.html`.

### What it contains
- **Laura's item 1** — the large opening headline is retired. `paintTitleMask` and
  `paintTitleSolid` are now empty; the opening is the logo, then the lede. `titleLayout()` still
  reserves the headline's space so the logo keeps its position — **which leaves a visible gap**
  of ~225px at 1440x900 and ~270px on a phone between the logo and the photograph. Flagged to
  Gabriel; not changed here, because the reservation looks deliberate.
- **Laura's item 15** — "new normal", placed on the page about ACE-related risk outgrowing the
  systems built to manage it, which is where the rising-prevalence figures are. Reads: "…than the
  generation before them — this is essentially a new normal that invites a healing-centered
  approach to systems change." followed by a "Read the paper →" link to
  `https://www.mdpi.com/2076-328X/16/9/1687`. New `.wc-src` rule for the link.
- **A crash guard** in `buildTitle`: `if(!tcw||!tch){titleParts=[];return;}`. Measuring the page
  while hidden gives a zero-size canvas, and `getImageData` then throws and halts the rest of the
  script. Worth keeping.

### Laura's item 16 was tried and withdrawn
The earlier preview drew the double loop — the outer sweep carrying on past "expand the circle of
leadership" and back in to step 03, learning, with an arrowhead. It is not in the later preview,
so it was deliberately backed out. **The code is preserved in
`hero-versions/_double-loop-attempt.txt`** rather than lost with the preview.

### To stop this recurring
Either give this repo a remote both machines push to, or always deploy with `--prod`. The second
only fixes the symptom.
