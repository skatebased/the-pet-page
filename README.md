# The Pet Page

A monthly newspaper page pairing local animal rescue stories with pet care journalism — funded by the readers whose dogs appear on it.

A partnership between **Mars Petcare**, **The Middleburg Page**, the **Fauquier Times** and **The Georgetowner**, with the **Middleburg Humane Foundation**.

---

## The idea

Every community in America has a local newspaper, a local animal shelter, and people who are irrationally devoted to their pets. Almost nowhere are those three connected in a way that produces money.

One half of the page is a reported rescue story from the local shelter. The other half explains how Mars makes its pet food and the science behind it. Along the bottom runs a row of eight reader-submitted pet photographs, each paid for by the family whose pet appears — which is why the page doesn't depend on a national advertiser renewing.

## The architecture

**The printed page is not the source.** A broadsheet PDF is unreadable on a phone, so the story is authored once as structured content and every output is a render of it:

| Render | Specification | Purpose |
|---|---|---|
| Print page | 9.5 × 10.5 in live space (configurable), strip ad 9.5 × 1.25 in, 600–1200 DPI | The page of record |
| Phone | Single column, mobile-first | Where most readers actually read it — **carries the complete story** |
| Web | Responsive, two columns above 900 px | The jump page — **carries the complete story**, and the only render producing hard traffic numbers |
| Postcard | 6 × 4.25 in trim, 0.125 in bleed, 0.25 in safe zone | Pet-store counter hand-outs and USPS direct mail |
| Video | 1080 × 1920 (9:16), platform safe zones marked | Reels and Shorts |

Print is space-limited and hands off to the web. Phone and web always carry the full text.

## Site map

```
index.html              Home
about.html              The partnership prospectus — partners, Mars science, editorial standards
issues/index.html       Issue archive
issues/001-tanner.html  Issue 1, all five renders (press 1–5 or use the tabs)
composer.html           The Composer — the intake and auto-composition engine
partners.html           Partner kit and fixed rates for other newspapers
playbook.html           Video production playbook
data/targets.json       Newspaper prospecting list near Mars US sites
assets/press/           Press-ready PDF proofs and the Word prospectus
```

## The Composer

`composer.html` is the working system. A partner newspaper:

1. Pastes its rescue story and byline
2. Drops in the animal's photograph
3. Names the eight reader-funded pet slots
4. **Sets its own print specification** — page size, margins, column count, gutter, strip height — if it differs from the default
5. Gets all five renders composed live, and prints its page at its own trim

Story packages save and load as JSON, which is the interchange format between a partner paper and the syndicator.

### Typography

The Composer enables the professional typesetting controls a browser actually supports, most of which are off by default on the web:

- `font-optical-sizing` — Newsreader and Source Serif 4 carry an optical-size axis, so 8pt body and 34pt masthead render from differently *drawn* designs rather than one design scaled. The single biggest quality win.
- `font-kerning` — the font's own GPOS kern table
- A true **optical kerning pass** on display type, measured from the rendered glyphs at runtime: every pair of the display face is rasterised on a canvas, the visual gap between the facing ink profiles is compared with the face's own straight-stem rhythm (nn · no · on · oo), and the difference is applied as a per-pair correction — tightening boldly, opening timidly. Because it measures what the browser actually renders, it is correct for any face, including a paper's own licensed one. Strength is adjustable and it never touches body copy, where metric kerning is already correct.
- A **copy-edit pass** at render time — curly quotes, en dashes in numeric ranges, thin-spaced em dashes, true ellipses, non-breaking abbreviations, and widow-proofed paragraph endings. The writer's input is never altered; only the render is.
- **Cap-height trimming** (`text-box: trim-both cap alphabetic`) so display type is measured cap to baseline the way a compositor measures it, **optically aligned drop caps** whose ink — not their advance box — sits flush to the margin, and a **size-graded tracking curve**: tighter as type grows, a touch open at agate sizes.
- Paragraph-level line breaking (`text-wrap: pretty`), balanced headlines, hyphenation limits (`6 3 3`), hanging punctuation, old-style figures in text and lining figures in display, ligatures and contextual alternates, widow and orphan control.

A paper using its own licensed face types the family name into the typography panel.

**What a browser still cannot do:** Adobe's multi-line paragraph composer (which kills rivers in justified columns) and strict baseline-grid locking. For that last step of press quality the two routes are **PrinceXML** as a drop-in rendering upgrade, or an **InDesign bridge** driving a template from the JSON package via tagged-XML import.

## Editorial standard

Printed on every page, in the same size type as everything else:

> Mars Petcare funds this page and reviews only its own company content. The Middleburg Page retains full editorial control of all rescue reporting.

Mars approves its own content. It sees the rescue reporting when readers do — no review, no approval, no notes. Any newspaper adopting this model adopts the standard with it; it is a condition of the syndication, not a suggestion.

## Running locally

Static site, no build step:

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

## Deploying

Works on GitHub Pages as-is. Settings → Pages → deploy from branch `main`, folder `/ (root)`. A `.nojekyll` file is included so directories beginning with an underscore are served correctly.

## A note on the logos

The partner marks in `assets/img/` are typographic placeholders set for layout. Final artwork should be supplied by each partner — in particular, Mars brand assets and their permitted usage must come from Mars and be applied per Mars brand guidelines before publication.

---

**The Middleburg Page** · Leland Schwartz, Publisher · The Plains, Virginia · editor@themiddleburgpage.com
