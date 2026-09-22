# Launch checklist — Plant Your Flag

FlyRank AI Internship · **Plant Your Flag: Domain + Badge**

Site: <https://krcgoktug.github.io>

Four things this assignment asks for. All four are done and measured.

---

## 1 · Address and HTTPS — done, with a choice I want to defend

The brief allows "a clean free subdomain … only if budget is truly zero". That is the
option I took, and it is a decision rather than a surrender.

`krcgoktug.github.io` is the account's own GitHub Pages domain: HTTPS by default with a
certificate I do not renew, no registrar to forget, no DNS to expire, and no yearly cost
that quietly turns my portfolio off eighteen months from now when I am not looking. A
`.com` costs little, but its failure mode — silent expiry — is worse than the thing it
buys me, which is a slightly shorter address.

I did learn the mechanism rather than skipping it: [DNS-WALKTHROUGH.md](DNS-WALKTHROUGH.md)
is the plain-language version of what pointing a custom domain here would actually
involve, written so I could explain it rather than click through it.

Verified live: `200`, HTTPS, no mixed content.

## 2 · Launch hygiene — done and measured

| | Status |
| --- | --- |
| `<title>` | `Göktuğ Karaca — backend engineer` |
| Meta description | present |
| `og:title` / `og:description` / `og:url` | present |
| `og:image` | 1200×630, live, `200`, `image/png` |
| `twitter:card` | `summary_large_image` |
| Canonical | present |
| **Favicon** | **added this pass** — `favicon.svg`, `200`, `image/svg+xml` |
| **Apple touch icon** | **added this pass** — `icon-180.png`, `200`, `image/png` |

The favicon was the real gap. There was none at all, which means a blank page icon in
every tab and every bookmark — one of those things you stop seeing on your own site. The
icon is drawn from the same palette as the social card: `#12161C` ground, `#FBFBF9` mark,
one `#E08A4E` rule.

Phone check, measured at 375×812 in a real browser (not a screenshot — see
`MOBILE-FIX-LOG.md` for why that distinction cost me two commits): `body.scrollWidth` 375
equals the viewport, no horizontal overflow, badge 335 px wide and inside the fold.

## 3 · The badge — done

In the footer, linking to FlyRank's public verification page, printing the credential
reference `FR-D1-02C09-C281E` so it is a claim someone can actually check rather than an
image anybody could have made in an editor.

Styled quiet on purpose — muted colour, mono face, the same treatment every other piece of
evidence on the page gets. 44 px minimum height, because it is a link on a phone.

It also wraps as one run of prose. The first version had the reference as its own flex
item, so at 375 px it sat in a separate right-hand column while the label wrapped in the
left one. Same sentence, so it should wrap like one.

## 4 · Analytics — done, and verified by a real recorded visit

**GoatCounter**, at `krcgoktug.goatcounter.com`. No cookies, so the page still needs no
consent banner — that is the reason it is this and not Google Analytics — and the free
tier is free at rest rather than free-for-now, the same test I applied to the hosting in
`STACK-DECISION.md`.

One line, immediately before `</body>`:

```html
<script data-goatcounter="https://krcgoktug.goatcounter.com/count"
        async src="//gc.zgo.at/count.js"></script>
```

**Working, not just installed.** The dashboard has stopped saying *"No data received"* and
shows:

| | |
| --- | --- |
| Visits | **1** |
| Page | `/` — "Göktuğ Karaca — backend engineer" |
| Browser | Chrome |
| System | Windows |
| Location | Turkey |

I also confirmed on the live page that `window.goatcounter` is defined and
`goatcounter.count` is a function, and that the `/count` endpoint accepts the beacon. But
the claim is the recorded visit. A snippet sitting in the source is not evidence that
anything is being counted, and this assignment grades the second thing.

### What I tried first, so nobody repeats the search

I wanted to avoid the signup entirely. It cannot be done:

| Option | Result |
| --- | --- |
| CountAPI (`api.countapi.xyz`) | dead — connection refused |
| CounterAPI v1 | `410 Gone`, deprecated |
| CounterAPI v2 | `404 Workspace not found` — needs an account |
| hits.sh | `404` on any key I do not own, and the host answers as `Apache/2.4.38 (Win64)` from 2019 — not somewhere I am pointing a beacon from a live site |
| GoatCounter / Cloudflare / Umami / Plausible | all work, all require signing up |

So it was one free account and about two minutes.

### The cost, written down rather than absorbed

This is now the **third third-party request** on a page whose own `WHERE-IT-BREAKS.md`
complains about the two Google Fonts ones. That comment sits next to the snippet in
`index.html`. Self-hosting the fonts would take the page back to one; I still have not
done it, and the honest reason is that I have not got to it rather than that I decided
against it.

I briefly had a better idea and discarded it: `goktugkaraca.com` is already mine, on
Vercel, where Web Analytics is one toggle on an account I already have — and Speed
Insights is in fact already enabled there. But every other assignment this term — *Make It
Do Something*, *Open It on Your Phone*, *Break Your Own Site* — was submitted against
`krcgoktug.github.io`, and quietly changing which site "my portfolio" means at the last
checkpoint would make those submissions inconsistent. The free subdomain stays, and the
trade-off is stated rather than hidden.
