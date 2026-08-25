# How my page centres itself — and the bug that wasn't there

FlyRank AI Internship · Week 5 · **Explain It Like You Built It**

I picked the smallest-looking piece of my site: the four lines of CSS that put my name in
the middle of the screen. I picked it because it is where I got something wrong, and
because "centre a box" turns out to have a real mechanism underneath it that I did not
understand when I wrote it.

Explaining it to someone who has never built a site.

---

## What the browser is actually doing

A web page is a stack of boxes. Every heading, paragraph and link is a box, and the
browser's whole job on layout is deciding how wide each box is and where it sits.

My page has one box that matters — `<main>` — holding my name, my one-line claim, and two
links. Everything else is inside it. The CSS says:

```css
body {
  display: grid;
  place-items: center;
  padding: 2rem;
}
main { max-width: 34rem; width: 100%; }
```

In plain words: *make the page a grid, put its contents in the middle both ways, keep a
2rem gap at the edges, and don't let the inner box get wider than 34rem.*

`display: grid` turns `<body>` into a container that arranges children in rows and
columns. I only have one child, so there is one cell. `place-items: center` centres that
child inside its cell, horizontally and vertically at once. `max-width: 34rem` stops the
text lines getting so long they become hard to read — around 65 characters is comfortable,
and 34rem lands near that.

That is the part I thought I understood. Here is the part I didn't.

## The bit I had to be taught

**A grid column has a width, and by default that width is decided by the content.**

I had not thought about the column at all. I assumed `<main>` sat directly inside the
page and `max-width` capped it. But there is a column in between, and because I never
declared one, the browser created an implicit column sized `auto` — which means *as wide
as the widest thing inside it needs to be*.

So the chain is: my longest line wants some width → the column grows to fit it → `<main>`
is `width: 100%` *of that column*. On a wide screen this never shows, because the column
is comfortably narrower than the window. On a narrow phone, the column can end up wider
than the screen, and then the text runs off the right edge.

The fix is one line, and it only makes sense once you know a column exists:

```css
grid-template-columns: minmax(0, 1fr);
```

`1fr` means "one share of the available space" — so the column takes the width the page
actually has, rather than the width the content wants. `minmax(0, ...)` is the important
half: it sets the column's *minimum* to zero, giving it permission to shrink smaller than
its contents. Without that, a grid column silently refuses to go below its own content
width, which is exactly the trap.

## The part I got wrong

I found this because my page *looked* broken on a phone. I took a screenshot at 390 pixels
wide, saw my claim and my footer clipped at the right edge, decided I had a responsive
bug, wrote a fix, and pushed it with a commit message saying it fixed a mobile overflow.

It hadn't, because there was no overflow.

What gave it away was that three genuinely different versions of the CSS produced
**byte-identical** screenshots — 24,917 bytes, three times. That cannot happen if the CSS
is being applied. So I stopped looking at pictures and measured instead, in a real browser
at a real phone width:

```
viewport width      375
body.scrollWidth    375     ← equal, so nothing overflows
main width          311     ← 375 minus 2rem padding on each side

element     left  right   overflows?
h1           32    343     no
p.claim      32    343     no
footer       32    343     no
```

Every element sat inside the screen. The page had been fine the whole time. The broken
thing was my screenshot method: the headless-browser flag I used to set the window size
does not set the *layout* viewport, so the browser laid the page out wide and then cropped
the image to 390 pixels — which looks exactly like clipped text.

I went back and corrected the commit message rather than leaving a fix in the history for
a bug that never existed. I kept the `minmax(0, 1fr)` line, because an auto-sized column
genuinely can be pushed past its container by something unbreakable like a long URL — but
the commit now calls it hardening, not a fix.

## What I actually learned

Two things, and the second one is the one I will reuse.

The mechanism: `place-items: center` centres a box inside its grid cell, and the cell is
not automatically the width of the page. If you want it to be, you have to say so.

The habit: **a screenshot is evidence about your screenshot tool as much as about your
page.** One measurement — does `scrollWidth` equal the viewport — answered in a second
what I had already spent two commits guessing at. When something looks wrong, measuring
the thing beats looking at a picture of the thing.
