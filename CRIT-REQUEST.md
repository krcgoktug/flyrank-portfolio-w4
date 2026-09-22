# Survive the Crit — the review pack

FlyRank AI Internship · **Survive the Crit** (Checkpoint 1)

Everything needed to run the review. The only step I cannot do myself is the one that
matters: someone else looking at the site.

Site under review: <https://krcgoktug.github.io>

---

## The proof statement the reviewer is judging it against

> **I build backend services, and I can tell you how each one fails.**

Audience: an engineering manager or a technical founder.
The one action the page asks for: **book a 20-minute technical conversation.**

Give the reviewer this statement *before* they look. The job is not "do you like it" —
it is "does the page deliver on that specific claim, to that specific person".

## The two questions, asked first — before any other feedback

Ask these while they still have a first impression, and ask them in this order. Once
someone has scrolled for two minutes they can no longer answer question 1 honestly.

1. **"You have ten seconds. What do I do?"**
2. **"Would you believe I am good at it?"** — and then: *why, or why not?*

Then stop talking and let them keep going. **Do not defend anything.** If they
misunderstood something, that is the finding. Write it down exactly as they said it,
including the parts that sting. "They just didn't read it properly" is not an outcome the
page gets to claim.

## The message to send

**Turkish — for a friend or classmate:**

> Selam! Portfolyo sitem için bir tasarım geri bildirimine ihtiyacım var, 10 dakikanı alır.
>
> Site: https://krcgoktug.github.io
>
> Sitenin iddiası şu: *"Backend servisler yazıyorum ve her birinin nerede bozulduğunu sana
> söyleyebilirim."* Hedef kitle bir mühendislik yöneticisi ya da teknik bir kurucu, ve
> sayfanın istediği tek şey 20 dakikalık teknik bir görüşme ayarlamak.
>
> Önce açmadan iki soruya cevap ver, açtıktan **10 saniye** sonra:
> 1. On saniyede: ben ne yapıyorum?
> 2. Bu işte iyi olduğuma inanır mısın? Neden / neden değil?
>
> Sonra istediğin kadar gez ve aklına ne geliyorsa söyle — kafa karıştıran, kırık, gereksiz,
> abartılı görünen her şey. Savunmaya geçmeyeceğim, söz. Acımasız olman benim için daha
> faydalı.
>
> Telefondan da bir bakabilirsen ayrıca iyi olur.

**English — if the reviewer is not a Turkish speaker:** same thing, shorter:

> I need ten minutes of design feedback on my portfolio: https://krcgoktug.github.io
>
> The claim it makes is *"I build backend services, and I can tell you how each one fails."*
> The audience is an engineering manager or technical founder, and the one thing the page
> asks for is a 20-minute conversation.
>
> Open it, count ten seconds, then answer: **what do I do**, and **would you believe I'm
> good at it?** After that, tell me anything confusing, broken or overclaimed. I won't
> defend it — brutal is more useful.

## Capture what comes back, here

Paste their words, not your summary of their words.

| # | What they said (verbatim) | must-fix / nice-to-have | Why |
| --- | --- | --- | --- |
| 1 | | | |
| 2 | | | |
| 3 | | | |

**must-fix** = confusing, broken, hurts the one action, or the proof does not land.
**nice-to-have** = everything else. Be strict; a list where everything is must-fix is a
list that has not been triaged.

Then fix the must-fixes, push, and reply to the reviewer with what changed. That reply is
part of the deliverable — the assignment grades the loop closing, not just the feedback
arriving.

## What the reviewer will be looking at

So you know what is already true when they open it, and are not surprised by a finding you
have already fixed:

- **The ten-second answer is the h1 plus the line under it** — name, then the claim, then
  three sentences of context. No hero image, no scroll-jacking, nothing between them and
  the sentence.
- **The one action is now the only filled button** in the header. It used to be one of five
  identical pills, which is the same as asking for five things equally. Fixed today;
  contrast 8.0:1, 45 px tall.
- **Four projects, each with a one-line failure mode**, and a measured evidence line under
  each — "18 tests · one idempotency key survives 12 concurrent retries", not "robust".
- **One interactive thing**: the live commit classifier, which is the claim demonstrated
  rather than asserted. It labels its own limit — anything outside the eight recorded
  messages says "not recorded" instead of inventing a verdict.
- **The capstone section is current** as of today. It used to say both capstones were "in
  review"; they were accepted weeks ago and the page had gone stale.
- **The credential badge is in the footer** and links to a verification page that will
  confirm it.

## Known weak points — do not lead with these, but do not hide them either

If the reviewer finds these, they are right, and the answer is "yes, here is why", not a
defence:

- **No case study pages.** Every project links straight to a GitHub README. For a reader
  who does not open GitHub, the site is a list of links. This is the single biggest gap
  and it is the thing the monthly case-study habit exists to close.
- **Two third-party font requests** to Google — flagged in `WHERE-IT-BREAKS.md`, not yet
  paid down.
- **The model column in the demo is recorded, not live.** Stated on the page, but a
  reviewer may still read "AI feature" and expect live.
- **No analytics yet**, so there is no data on whether anyone reaches the one action.
