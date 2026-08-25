# Three roads: how I chose the stack

FlyRank AI Internship · Week 4 · **Three Roads: Choose Your Stack with AI**

The point of this assignment is not to get a stack recommended. It is to give AI real
constraints, make it lay out options with trade-offs, and then decide myself. So the
constraints came first, and they are the reason the answer is boring.

---

## My four constraints

| | |
| --- | --- |
| **Budget** | Free only. Not "free tier that expires" — free at rest, forever. |
| **Skill level** | Comfortable with Python, FastAPI, SQL, Docker, git. Not a front-end developer. I can read HTML and CSS; I have never fought a JS build pipeline and would like to keep it that way. |
| **What the site must do** | Four pages from my Week 1 sitemap: Home / Case Studies / About / Contact. Static. No login, no CMS, no database. |
| **How my work must be shown** | This is the constraint that actually decides it. My evidence is **code and terminal output**: repo links, `curl` sessions with status codes, test output, a Swagger screenshot. I need readable long-form with **syntax-highlighted code blocks** and links that go to GitHub. I do **not** need image galleries, and I have no video. |

**Does anything need to be dynamic at launch?** No. The contact page is an email address
and a LinkedIn link. A contact *form* would mean a backend, a spam problem, and a
deliverability problem, to replace something `mailto:` already does. Not yet — and
"not yet" is the honest answer rather than the humble-sounding one.

---

## The three roads

### 1. No-code builder (Carrd, Framer, Canva Sites)

**How I'd build it.** Pick a template, drag blocks, publish. An afternoon.
**Hosting.** Included, on their subdomain.
**Backend?** No.
**How well it shows my work.** *Badly.* These tools are built for images and marketing
copy. Getting a monospaced, syntax-highlighted `curl` session with response headers into
one means an embed or a screenshot of text — and a screenshot of text is unreadable on a
phone and invisible to search.
**The real trade-off.** Fastest to publish, worst at the one thing my portfolio has to do.
Also: my content lives inside someone's editor. Exporting later means retyping.

### 2. Plain HTML + CSS on a free static host

**How I'd build it.** Four hand-written HTML files, one CSS file with the Week 3 identity
kit as custom properties. No build step, no dependencies, no `node_modules`.
**Hosting.** GitHub Pages (Netlify, Cloudflare Pages and Vercel are equivalent here).
**Backend?** No.
**How well it shows my work.** Best of the three. `<pre><code>` is exactly the right
element for terminal output, it is readable on a phone, and it costs nothing to render.
The repo sitting next to the site is itself part of the evidence for a backend developer.
**The real trade-off.** I write the HTML. Four pages of it is genuinely small; forty would
not be, and at that point the lack of templating starts to hurt.

### 3. A framework (Next.js / Astro on Vercel)

**How I'd build it.** `create-next-app`, components, MDX for the cases, deploy on push.
**Hosting.** Vercel free tier.
**Backend?** Not required, but it invites one.
**How well it shows my work.** Well — MDX plus a highlighter is genuinely nice for code.
**The real trade-off.** I would be maintaining a dependency tree to publish four static
pages. Node majors move, `next` majors move, and a build that works today breaks in eight
months when I have not touched it. That is a real cost paid in exchange for templating I
do not need at four pages.

---

## What I chose, and why

**Road 2: plain HTML and CSS on GitHub Pages.**

The deciding constraint was *how my work must be shown*. My evidence is text — status
codes, test output, terminal sessions. Road 1 is actively bad at that, and Road 3 is good
at it but charges maintenance rent for templating I do not need yet.

**Why not Road 1.** It would have been done faster. But a portfolio whose whole claim is
"here is the evidence" cannot render its evidence as screenshots of text.

**Why not Road 3.** Not because frameworks are bad — because this site has four static
pages. Bringing a build pipeline to that is the bulldozer-for-a-flower mistake the brief
warns about, and the cost lands later, on the version of me who has not opened the repo in
six months.

**Can I maintain this?** Yes, and this is the part I actually thought about rather than
asserted. There is nothing to maintain: no dependencies to update, no build to break, no
account that expires. Adding a case study is copying an HTML file and editing the text —
which is exactly the process my [AI Fluency capstone note](https://github.com/krcgoktug/flyrank-capstone-fluency)
commits me to, and that note stays true only if adding a page is genuinely this cheap. If
I had chosen Road 3, "add the next case" would sometimes mean "first fix the build," and
that is how portfolios go stale.

**Why GitHub Pages over Netlify** (the program's recommendation): I already have the
GitHub account the rest of my work lives in, so this adds no new account, and the site
deploys from the same repo the evidence links point at. Netlify drag-and-drop is genuinely
faster for a first deploy; the cost is that the site then lives outside version control
unless I wire it up again.

**What would make me switch.** If I add more than ~15 case pages and start copy-pasting
the same header into each one, the lack of templating stops being free. Astro would be the
move then — it outputs static HTML, so nothing about the hosting or the URLs changes. The
switching cost is deliberately low, and knowing that is part of why picking the small
option now is safe.
