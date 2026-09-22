# Launch checklist — Plant Your Flag

FlyRank AI Internship · **Plant Your Flag: Domain + Badge**

Site: <https://krcgoktug.github.io>

Four things this assignment asks for. Three are done and measured. One needs an account
I have to create myself, and it is the only thing standing between this and a submission.

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

## 4 · Analytics — **not done, and this is what is blocking the submission**

Every free analytics option worth installing — GoatCounter, Cloudflare Web Analytics,
Umami Cloud, Plausible's free tier — requires creating an account. That is a step I have
to take myself.

It is about ten lines of work once the account exists. GoatCounter is the one I would
pick: no cookies, no consent banner needed, and the free tier is free at rest rather than
free-for-now, which is the same test I applied to the hosting in `STACK-DECISION.md`.

```html
<!-- immediately before </body> in index.html -->
<script data-goatcounter="https://YOURCODE.goatcounter.com/count"
        async src="//gc.zgo.at/count.js"></script>
```

Then: commit, push, wait for Pages, load the site once, and confirm the hit appears in the
dashboard. That last step is the one the assignment actually grades — "installed **and
working**" — so a screenshot of a real recorded visit is the evidence, not the snippet.

Until that is real, this assignment is three-quarters done and I would rather say so than
submit it and call the missing quarter an oversight.
