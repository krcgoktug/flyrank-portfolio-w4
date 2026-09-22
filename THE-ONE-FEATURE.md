# The one thing my site actually does

FlyRank AI Internship · **Make It Do Something**

Live on <https://krcgoktug.github.io> — the section *"Try it: does this commit record a
mistake?"*

One feature, not several half-wired ones. You type a commit message and get an answer.

---

## What it is

It is the **keyword rule** out of my commit-triage service, ported to run in your browser,
shown next to what the **model** said about the same message.

That pairing is the whole point. The service exists because a keyword search for
`fix|wrong|revert` gets this job wrong in both directions, and the fastest way to show that
is to let someone try it themselves. Press *the false negative* and you get:

```
keyword rule : no mistake        ← wrong
model        : records a mistake  ← right
"They disagree — and the model is right."
```

That message — *"Stage 5: 60 clean records collected…"* — is the encoding bug from my
scraper. It contains no keyword at all, so a grep sails past it. Press *the false positive*
and both say "no mistake", because the keyword rule keeps a hand-written list of words like
`prefix` that only look like `fix`. That list is exactly the maintenance the model call
buys its way out of.

## What a backend is, in plain words

A **frontend** is what arrives in your browser: HTML, CSS, a bit of JavaScript. It runs on
*your* computer. Everyone who opens my site gets the same files.

A **backend** is a program running on a computer somewhere else, waiting for requests. You
need one when the work cannot happen on the visitor's machine — because it needs a secret
(an API key you must not ship to a browser), or data other people can't have, or something
too heavy to run on a phone.

My site is entirely frontend: static files on GitHub Pages, no server of mine involved.
That is why the page loads in 368 ms and why there is nothing to keep running.

## How the data flows

Two paths, and the difference between them is the honest part of this feature.

**The keyword rule — fully live, no backend:**

```
you type          →  an `input` event fires in your browser
                  →  keywordVerdict() runs, the same logic as judge.py's fallback
                  →  the verdict is written into the page
```

Nothing leaves your machine. No request, no server, no logging. It is instant because
there is no network in the loop at all.

**The model verdict — recorded, not live:**

```
earlier, on my machine:
  POST /classify   →  FastAPI  →  Ollama (qwen2.5:7b)  →  schema check  →  verdict
                                                              ↓
                                                 docs/test-cases.txt
                                                              ↓
                                          copied into the page as RECORDED[]
```

The model runs on my own machine. Putting it behind a public URL needs a hosting account,
and I would rather ship a page that is honest about the seam than one that pretends to a
live model it does not have.

So the page shows **"not recorded"** for any message outside the eight I actually ran. It
does not guess, and it does not quietly fall back to the keyword answer and present it as
the model's. That was a deliberate choice: a demo that invents an answer is worse than a
demo with a stated limit.

## Why this feature and not a contact form

A contact form is the default answer, and for most portfolios it is right. Mine already
has a working contact path — a `mailto:` link, and a booking link that pre-fills a subject
and body. Adding a form would mean a backend, a spam problem and a deliverability problem,
in exchange for something that already works.

The feature that earns its place is the one that demonstrates the claim at the top of the
page. Mine is *"I build backend services, and I can tell you how each one fails"* — so the
thing to put on the site is a failure you can reproduce yourself, in two clicks.

## What I would do next

Put the model behind a real endpoint so the second column is live too. That needs a free
host account and a cold-start budget, and it changes the honest label from "recorded" to
"live" — which is the only reason to bother.
