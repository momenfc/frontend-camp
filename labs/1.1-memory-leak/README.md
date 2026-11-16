# Lab 1.1 — Leaky Notes

A tiny vanilla-JS page. Each panel holds 20,000 notes. Opening and closing a panel should
leave memory where it started. It doesn't: on a reference run, every open/close cycle keeps
about 3.6 MB alive, and the heap climbs from ~5 MB to ~55 MB after 14 cycles.

## Setup

1. Copy this folder into your `camp` repo as `labs/1.1-memory-leak/`.
2. Open `index.html` in Chrome (double-click works, or `npx serve .`). Use an Incognito window.
3. Commit the untouched version first, so your fix is one clean diff.

## Rules

- Write the fixes by hand. No AI for this one: the point is that you can read a retainer chain.
- Don't rewrite the app. Keep all four features working: the resize label, the live clock,
  the "recent" counter in the header, and the render cache.
- Fix one leak at a time, and take numbers after each fix.

## Steps

1. **Prove it.** Performance panel, tick *Memory*, record while you click "Open + close x7" twice.
   Screenshot the JS heap line (staircase, not sawtooth).
2. **Find it.** Memory panel: warm up (open + close once), Snapshot 1, click "x7", Snapshot 2,
   click "x7", Snapshot 3. Snapshot 3 → *Comparison* vs Snapshot 1, sort by `# Delta`.
   Filter `Detached`. For each suspicious object, read the Retainers down to the root.
3. **Fix it.** There is more than one leak. For each one, write down the retainer chain you saw,
   then fix it.
4. **Prove the fix.** Repeat step 2. Target: no `Detached` nodes from panels, no `NotesPanel`
   instances left after closing, and the heap after GC back within ~1 MB of the warm-up baseline.

## Report (fill this in, commit it as REPORT.md)

| Leak | Retainer chain (root → object) | Fix | Heap after 14 cycles |
| --- | --- | --- | --- |
| baseline (no fixes) | — | — | ___ MB |
| 1 | | | ___ MB |
| 2 | | | ___ MB |
| ... | | | ___ MB |

Also answer in 2–3 lines each:

- Which leak was the hardest to see, and why?
- Why does a detached `<span>` keep the whole panel's DOM alive?
- The "recent" counter needed a design decision to fix. What did you choose and what did it cost?
