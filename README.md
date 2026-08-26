# Week 4–5 · picking a stack, shipping it live, and explaining it

FlyRank AI Internship · General AI Fluency. Three assignments, one thread: choose how to
build, get something on a real URL, then prove you understand what you shipped.

| Assignment | Deliverable |
| --- | --- |
| **Three Roads: Choose Your Stack with AI** | [STACK-DECISION.md](STACK-DECISION.md) |
| **Empty but Live: Ship a Blank Page** | **<https://krcgoktug.github.io>** + [docs/live-check.txt](docs/live-check.txt) |
| **Explain It Like You Built It** | [EXPLAIN-ONE-PIECE.md](EXPLAIN-ONE-PIECE.md) |
| **Personal Website Live** (PF-04) | the same URL, now a real one-pager + [DNS-WALKTHROUGH.md](DNS-WALKTHROUGH.md) |

The site's source is in [`site/`](site) here and deployed from
[krcgoktug/krcgoktug.github.io](https://github.com/krcgoktug/krcgoktug.github.io).

---

## The short version

**Stack:** plain HTML and CSS on GitHub Pages. Not because frameworks are bad — because my
evidence is terminal output and status codes, a no-code builder renders that as
screenshots of text, and a framework would charge maintenance rent for templating that
four static pages do not need. Full reasoning, including the two roads I rejected and the
"can I maintain this" answer, is in [STACK-DECISION.md](STACK-DECISION.md).

**Live:** <https://krcgoktug.github.io> — HTTP 200, checked at a phone viewport with
measurements rather than eyeballing. The submitted visual evidence is
[`docs/mobile-live-375x812.png`](docs/mobile-live-375x812.png); the exact layout
measurements are in [`docs/live-check.txt`](docs/live-check.txt).

**The piece I explained:** the four lines of CSS that centre the page, and the grid column
underneath them that I did not know existed. That write-up also contains the mistake I
made this week, which is the more useful half.

---

## What I got wrong this week

I thought I had a mobile layout bug. I had a screenshot bug.

My first phone check used headless Chrome with `--window-size=390,844`, and the image
showed the claim and the footer clipped at the right edge. I wrote a fix, pushed it, and
described it in the commit message as fixing a mobile overflow.

The tell that something was off: three genuinely different versions of the CSS produced
**byte-identical** PNGs — 24,917 bytes, every time. That cannot happen if the CSS is being
applied. So I measured in a real browser instead:

```
viewport width      375
body.scrollWidth    375     ← equal, so nothing overflows
main width          311
h1 / claim / footer  32 → 343 px, all inside the screen
```

The page had been fine the whole time. `--window-size` does not set the layout viewport in
headless-new, so Chrome laid out wide and cropped the screenshot — which looks exactly
like clipped text.

I corrected the commit message rather than leaving a fix in the history for a bug that
never existed. The CSS change stayed, relabelled as hardening: an auto-sized grid column
genuinely can be pushed past its container by an unbreakable line, so it is cheap
insurance — just not a fix for anything that was happening.

---

## Deliberate limits

- **The CV link reuses my existing public resume page.** The private portal upload stays
  private; the portfolio points at `goktugkaraca.com/resume`, which was already public.
- **Booking is email-based.** The working booking link opens a message with the subject
  and requested time fields prepared. There is no extra calendar account to maintain.
- **The Writing section is empty**, and says so on the page. The process for filling it is
  written down and a monthly reminder is set; if it is still empty in three months, the
  honest move is to delete the section rather than leave it aspirational.
