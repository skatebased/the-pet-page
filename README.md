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
template.html           The page template — the example layout, annotated
partners.html           Partner kit and fixed rates for other newspapers
playbook.html           Video production playbook
data/targets.json       Newspaper prospecting list near Mars US sites
assets/press/           Press-ready PDF proofs and the Word prospectus
```

## The template

`template.html` is the whole partner-facing system now — no software, just the page itself, annotated. Every month The Middleburg Page sends the right-hand story and the strip advertisement; the partner paper adds its rescue story and photograph, in the template arrangement or any layout it prefers. Two elements are fixed: the story we send, and the Mars strip across the bottom. Papers email their story and photograph back and receive the finished vertical video for their social accounts.

The example on the page is set with the print CSS the sample issue uses — optical sizes, real kerning, justified newspaper measure — so what an editor sees is what the pressroom gets.

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
