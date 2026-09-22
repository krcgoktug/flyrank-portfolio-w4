# Where it breaks

FlyRank AI Internship · **Break Your Own Site**

Site: <https://krcgoktug.github.io>

I tried to break my own site on purpose: hostile input into the one interactive feature,
every link clicked, a speed measurement, and a look at what a shared link renders as.
Everything below is a result, not an intention.

---

## What I threw at it

The site has one interactive thing — the live commit classifier — so that is where the
attack surface is. Ten inputs, each one a way a real user or a bored attacker breaks a form.

| Input | What happened | Verdict |
| --- | --- | --- |
| Empty string | Shows `—`, "waiting for input" | fine |
| Only whitespace `"     "` | Same as empty; does not classify blank as a result | fine |
| `<img src=x onerror=alert(1)>` | Treated as text. **`alert` never fired** | fine |
| `<script>window.__pwned=1</script>` | Treated as text. `window.__pwned` is `undefined` | fine |
| 16,000 characters (`"fix "` × 4000) | Still classifies, no freeze, `scrollWidth` stays 375 | fine |
| Emoji, Arabic script, newlines | Handled; no layout break | fine |
| `PREFIX ekle` (uppercase) | Correctly "no mistake" — the matcher lowercases first | fine |
| `!@#$%^&*()` | "no mistake", no crash | fine |
| A message nobody recorded | Says **"not recorded"** rather than inventing a verdict | fine |
| Every outbound link (9) | All **HTTP 200** | fine |

**Why the injection did not work**, verified by reading the code and not just by the alert
not firing: user input never reaches `innerHTML`. There are exactly three `innerHTML`
writes on the page and all three concatenate only my own literal strings — the typed text
is used as a *condition* (`text.trim() ? … : …`), never as content. Everything that does
echo input goes through `textContent`.

## Speed and findability

Measured from the network, uncached:

| | |
| --- | --- |
| HTML | **17,510 bytes** |
| Time to first byte | **359 ms** |
| Total load | **368 ms** |
| DOMContentLoaded (warm) | **216 ms** |
| Social card | 39,575 bytes, fetched only by crawlers |
| JS frameworks | none |
| Build step | none |

Meta added this week: `og:title`, `og:description`, `og:image` (a real 1200×630 card),
`og:url`, `twitter:card`, `canonical`, `theme-color`. Before this, a shared link rendered
as a bare URL.

## Fix now — done

1. **Tap targets 39 px → 45 px**, and the example chips 36 px → 44 px.
2. **Smallest text 11.84 px → 12.8 px.**
3. **No social preview → a real card**, live and returning `200`.

All three verified after deploy by measuring the live DOM, not by looking at it. Details
in [MOBILE-FIX-LOG.md](MOBILE-FIX-LOG.md).

## Known limitations — not fixed, and why

- **Two third-party requests.** The page pulls Inter and JetBrains Mono from
  `fonts.googleapis.com` and `fonts.gstatic.com`. That is four requests to Google and a
  privacy cost I have not paid down. Self-hosting the two fonts would remove it; I have
  not, and the honest reason is that I have not got to it rather than that I decided
  against it.
- **The model half of the demo is recorded, not live.** The classifier's keyword rule runs
  in your browser for real. The model verdicts beside it are copied from actual runs,
  because the model runs on my machine and putting it behind a public endpoint needs a
  host account I do not have. The page says "not recorded" for anything outside that set
  rather than guessing — which is the honest failure mode, but it is still a limitation.
- **No contact form.** The contact path is `mailto:`. A form means a backend, a spam
  problem and a deliverability problem, to replace something `mailto:` already does. This
  is a decision, not a gap.
- **No analytics, so "search your own name" is unmeasurable from here.** The site went up
  days ago and is not yet indexed; I can confirm the meta tags are correct and cannot
  confirm a search ranking. Claiming one would be inventing a number.
- **Tested at a phone viewport, not on a physical handset.** 375×812 with a mobile user
  agent, measured in the DOM. Stronger than eyeballing a resized window, weaker than
  holding a phone.

## The one that is still open

**Nobody else has reviewed this site.** The *Survive the Crit* assignment asks for a real
second pair of eyes — a fellow student or a friend — and for their feedback sorted into
must-fix and nice-to-have. I have not had that review yet, so there is nothing to report,
and a reviewer I invented would be worth less than an empty section.
