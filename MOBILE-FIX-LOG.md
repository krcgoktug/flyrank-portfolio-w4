# Fix log — opening it on a phone

FlyRank AI Internship · **Open It on Your Phone**

Site: <https://krcgoktug.github.io>

I audited it at a 375×812 viewport by **measuring**, not by looking — after Week 4, where
I spent two commits fixing a mobile bug that turned out to be my screenshot tool rather
than the page. A number that comes back from the live DOM cannot be misread the way a
cropped PNG can.

Every figure below is from a real browser at phone width.

---

## What was actually broken

| # | Finding | Measured | Standard | Verdict |
| --- | --- | --- | --- | --- |
| 1 | Nav pills too small to tap reliably | **39 px** tall | 44 px | fix now |
| 2 | Smallest text below comfortable reading | **11.84 px** | ~12.8 px floor | fix now |
| 3 | No social share preview | no `og:image` | — | fix now |
| 4 | Example chips (added later) | 36 px | 44 px | fix now |
| 5 | Horizontal overflow | `scrollWidth` 375 = viewport 375 | no overflow | already fine |
| 6 | Colour contrast, dark mode | 6.22 – 17.51 | 4.5 | already fine |
| 7 | Colour contrast, light mode | 5.56 – 17.51 | 4.5 | already fine |
| 8 | Every outbound link | 9 links, all **200** | — | already fine |

Three of the eight were real. The other five I had assumed were problems and were not —
which is the reason for measuring rather than guessing.

## What I changed

**1 · Tap targets, 39 px → 45 px.** The nav pills were `padding: .4rem .85rem` on an
inline element, which gave a 39 px box. 44 px is the smallest target most people hit
reliably first try. Changed to `inline-flex` with `min-height: 44px`, which also centres
the label properly instead of relying on line-height.

```css
nav.links a {
  display: inline-flex; align-items: center; min-height: 44px;
  padding: .55rem 1rem;
}
```

Verified after deploy: GitHub 45, LinkedIn 45, View my CV 45, Book 20 minutes 45, Email 45.

**2 · Smallest text, 11.84 px → 12.8 px.** The `.tag` chips were `.74rem`. At arm's length
on a phone that is squinting territory. `.8rem` for tags and `.85rem` for the evidence
lines. Smallest font on the page is now 12.8 px, measured.

**3 · Social share preview.** A shared link rendered as a bare URL with no image or
description. Added `og:image`, `og:url`, `twitter:card`, a canonical link and a
`theme-color`, plus a real 1200×630 card generated from the identity kit —
[`site/social-card.png`](site/social-card.png), live and returning `200`
(`image/png`, 39,575 bytes).

**4 · Example chips, 36 px → 44 px.** These arrived with the live demo, after the first
pass. 36 px passes WCAG AA (24 px) so it was not a failure — but "tappable" was the whole
point of the audit, and there was no reason to keep a second size.

## What I did not change, and why

**Contrast.** I expected the muted grey to fail and it does not: `#646669` on `#FBFBF9` is
**5.56:1** and `#9A9CA0` on `#12161C` is **6.60:1**, against a 4.5:1 requirement for body
text. Measured in both colour schemes. No change needed, and inventing one would have been
worse than leaving it.

**Images.** There are none to compress. The site carries no screenshots — the evidence is
code and terminal output, which is text. The social card is the only image, and it is only
fetched by crawlers.

## Still open

- **Checked with a real phone viewport, not a physical device.** 375×812 with a mobile user
  agent, measured in the DOM. That is stronger than eyeballing a resized desktop window and
  weaker than holding a phone; it would not catch an iOS-specific rendering quirk.
- **No tablet-specific pass.** The layout is a single column with a `max-width`, so tablet
  is the desktop layout with more margin. Worth a look, not worth a claim.
