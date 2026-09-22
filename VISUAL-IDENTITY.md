# Consistency, not talent

FlyRank AI Internship · **Consistency, Not Talent (and Frame, Not Upstage)**

Site: <https://krcgoktug.github.io>

I did this one late and backwards. The identity was already on the site — I picked the
colours and the two typefaces back in Week 4 and never wrote them down. So instead of
describing what I *meant*, I measured what is actually rendering, and the measurement
found a real problem.

---

## The kit

Seven colour tokens, redefined once for dark mode. Two typefaces. Nothing else.

| Token | Light | Dark | What it is for |
| --- | --- | --- | --- |
| `--ink` | `#12161C` | `#FBFBF9` | body text |
| `--paper` | `#FBFBF9` | `#12161C` | page background |
| `--main` | `#1F4B6E` | `#7FB2D8` | links, the claim line, the primary button |
| `--accent` | `#B4531F` | `#E08A4E` | one warm colour, used sparingly |
| `--muted` | `#646669` | `#9A9CA0` | captions, secondary lines |
| `--rule` | `#E2E2DE` | `#262C35` | every border on the page |
| `--card` | `#FFFFFF` | `#171C24` | raised surfaces |

**Inter** for everything readable, **JetBrains Mono** for anything that is evidence — a
`curl` line, a tag, a raw verdict. That split is doing a job: mono means *this is output,
not my opinion*. Three weights only, 400 / 600 / 700.

Measured on the live page: lowest text contrast **6.6:1**, against a 4.5 requirement.
Highest 17.51:1.

## What measuring found

I counted what the browser actually computes, not what I thought I had written:

```
20 font-size declarations  →  15 distinct sizes on one page
 8 border-radius declarations →  5 distinct radii
```

The sizes included `.93rem`, `.94rem`, `.95rem` and `.96rem` — four steps inside 0.5px of
each other. Nobody can see that. All it proves is that no one chose it, which is precisely
the thing a portfolio's design is not supposed to say about the person who built it.

That is the whole lesson of this week in one grep. The page *looked* fine. Looking is how
you miss it.

## What I changed

A named scale, each step with a stated job, and every declaration pointing at a token:

```css
--t-xs:   .8rem;    /* 12.8px - mono chips, captions */
--t-sm:   .85rem;   /* 13.6px - footer, inline code */
--t-md:   .9rem;    /* 14.4px - notes under a heading */
--t-base: .95rem;   /* 15.2px - body copy inside cards, controls */
--t-lg:   1rem;     /* 16px   - the one answer line that must read first */
--t-xl:   1.1rem;   /* 17.6px - card titles */
--t-2xl:  1.35rem;  /* 21.6px - section headings */
--t-lede: clamp(1.05rem, 3.5vw, 1.25rem);
--t-hero: clamp(2rem, 6vw, 2.9rem);
```

and four radii instead of five — pill, card, control, chip — because 10px was sitting next
to 12px for no reason I could name once I looked at it.

Measured on the live site after deploy:

| | Before | After |
| --- | --- | --- |
| Distinct rendered text sizes | 15 | **10** |
| Distinct border radii | 5 | **4** |
| Smallest text | 12.8 px | **12.8 px** (floor held) |
| Lowest contrast | 6.6:1 | **6.6:1** |
| Tap targets | ≥44 px | **≥44 px** |
| Horizontal overflow | none | **none** |

Ten rather than nine because two of the steps are fluid `clamp()` values and land wherever
the viewport puts them, plus the 17px document base. I am not going to round that down to
make the table look better.

Nothing on the page moved by more than about a pixel. That is the point.

## Frame, not upstage — and the AI images

Here is where I diverge from what I think this assignment expects.

**The page contains zero images.** No `<img>`, no `<svg>`, no CSS background image.
Verified in the browser, not assumed. I generated none, and I rejected the idea of
generating any.

The reason is the proof statement at the top of the page: *"I build backend services, and
I can tell you how each one fails."* The evidence for that claim is a live classifier you
can type into, nine repo links, HTTP status codes and measured timings. A generated
illustration of, say, an abstract network graph would not support one word of it. It would
be decoration standing in front of the argument — the exact definition of the design
upstaging the work. For a backend portfolio, **a real terminal capture beats anything
generated**, and no capture at all beats a decorative one.

The one image that exists is the **social card**, and a crawler is the only thing that
fetches it:

- 1200×630, 39,575 bytes, served `200`
- built from the kit above — `#12161C` paper, `#FBFBF9` ink, `#7FB2D8` claim,
  a single `#E08A4E` rule, Inter for the name, JetBrains Mono for the stack line
- it is the homepage, cropped to a rectangle. That is deliberate: a share preview that
  does not look like the page it links to is a small broken promise.

So: images that belong together, by there being one, and it being made of the same seven
colours and two fonts as everything else.

## What I would still change

- **Self-host the two fonts.** They come from Google, which is four third-party requests
  and a privacy cost. Same limitation as in `WHERE-IT-BREAKS.md`; still not paid down.
- **The 17px body base sits oddly next to a rem scale** measured against a 16px root, so
  `--t-base` (15.2px) is smaller than body copy. It reads fine and I checked, but it is a
  seam I would tidy if I rebuilt the stylesheet.
- **No spacing scale.** I fixed type and radii. Margins and padding are still ad hoc, and
  if I ran the same count on them I expect I would find the same mess.
