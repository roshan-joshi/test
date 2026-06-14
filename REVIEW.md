# 📋 Prototype Review Log — Systemboom Photo Timeline

Single source of truth for review feedback on the photo prototype (`photo.html`).
Reviewers (coworkers) **and** the build agent (Claude) both read and update this file,
so nothing has to be re-pasted in chat — just "re-read REVIEW.md".

---

## How this file works (read me first)

**Reviewers — to add feedback**
1. Add each issue under **🔴 Open Issues** with the next free ID (`R-06`, `R-07`, …).
2. Fill in: severity, area, what's wrong, and (if you know it) the suggested fix.
3. Save the file. If you use git: `git commit -am "review: <date>"` then push.
   - One issue = one entry. Don't overwrite someone else's entry.

**Build agent (Claude) — to work an issue**
1. Pick an Open issue → set its status to 🟡 *In progress*.
2. After implementing **and** verifying → set 🟢 *Fixed (pending confirm)* and note exactly what was done.

**Closing the loop — keep history, never delete**
3. When a reviewer **confirms** a fix, MOVE that entry from *Open Issues* down to the
   **✅ Resolved Log** (bottom), keeping its ID, the fix summary, and the confirm date.
   - The Open list stays short (only live issues); the Resolved Log is the permanent audit trail.
   - "Removed/won't-fix" issues also move to the Resolved Log, marked `WON'T FIX` with a one-line reason — so there's still a record.

**Severity:** 🟥 Critical · 🟧 Important · 🟨 Nice-to-have
**Status:** 🔴 Open · 🟡 In progress · 🟢 Fixed (pending confirm) · ✅ Confirmed (moved to Resolved Log)

---

## 🔴 Open Issues (at a glance)

| ID | Sev | Area | Issue | Status |
|----|-----|------|-------|--------|
| R-01 | 🟥 Critical | Mobile nav | No mobile navigation menu (nav is desktop-only) | 🟢 Fixed (pending confirm) |
| R-02 | 🟧 Important | Ruler | Drag-handle needs a ≥44px invisible hit-area | 🟢 Fixed (pending confirm) |
| R-03 | 🟧 Important | Forms | Inputs <16px → iOS Safari auto-zooms on focus | 🟢 Fixed (pending confirm) |
| R-04 | 🟧 Important | Touch targets | Several controls <44px (cramped, invites mis-taps) | 🟢 Fixed (pending confirm) |
| R-05 | 🟨 Nice-to-have | Mobile polish | Persistent mobile "Add memory" + one-time ruler touch hint | 🔴 Open |

> ⚠️ Seeded from a **partial screenshot** of "Prototype UI review" (the top CRITICAL items were above the fold; the review showed "6 of 6"). Reviewer: please paste/confirm the exact wording for R-01 and add any item I missed.

### R-01 · 🟥 Critical — Mobile navigation missing
- **Area:** Header / global navigation
- **Raised by:** Coworker — "Prototype UI review" · 2026-06-14
- **Details:** The top nav (Home / About / Dashboard / Friends / Profile) is `lg:flex` — hidden below 1024px with no hamburger or menu, so phones have **no way to navigate**. Reviewer's bottom line: *"mobile navigation is the #1 fix."*
- **Suggested fix:** Add a mobile menu — hamburger button → slide-out drawer / bottom sheet with the nav links.
- ⚠️ *Exact wording was above the screenshot fold — confirm.*
- 🟢 **Fix (pending confirm) — 2026-06-14:** Added a **hamburger** (`#navToggle`, shown `lg:hidden`) → a **dropdown menu** with all 5 links (Home/About/Dashboard/Friends/Profile), icons, **45px-tall rows** (≥44px touch target). Closes on select, outside-click, and Esc. Verified on a 390px phone viewport; desktop nav unchanged. *(Files: `photo.html` + `index.html` + `photo-v2.html`.)*

### R-02 · 🟧 Important — Ruler drag-handle hit-area too small
- **Area:** Timeline ruler (playhead handle)
- **Raised by:** Coworker — "Prototype UI review" · 2026-06-14
- **Details:** *"…with a thumb. Mitigated (not solved) by the large tappable year ticks (54×58) and keyboard nudge."* The new ↔ grip is visible but its tappable area is small.
- **Suggested fix:** Give the grip a **≥44px invisible hit-area**.
- **Link:** Follow-up to **R-00** (timeline discoverability, already fixed).
- 🟢 **Fix (pending confirm) — 2026-06-14:** Grip is now a **real draggable handle** (`pointer-events:auto`) with a **48×46 invisible hit-pad** (`::before`, ≥44px) and a larger visible body (40×18). It shares the exact rail scrub logic, so dragging the grip scrubs the timeline — and the full-ruler drag still works (verified both, no regression). *(Files: `photo.html` + mirrors.)*

### R-03 · 🟧 Important — Form inputs trigger iOS auto-zoom
- **Area:** "Add a memory" modal (form inputs)
- **Raised by:** Coworker — "Prototype UI review" · 2026-06-14
- **Details:** Input font is 12–14px; below 16px, Safari **zooms the page on focus**. Modal structure itself is fine (progressive disclosure + native date picker).
- **Suggested fix:** Set form inputs to **≥16px** font-size.
- 🟢 **Fix (pending confirm) — 2026-06-14:** All entry fields in `#uploadModal` (+ the memory modal, share, and nav search) are now **16px** font-size, so Safari no longer zooms on focus. Verified: caption/place/date/feeling/story/search all report 16px.

### R-04 · 🟧 Important — Touch targets under 44px
- **Area:** Filter chips, "Play all", ruler arrows, top-bar icons
- **Raised by:** Coworker — "Prototype UI review" · 2026-06-14
- **Details:** Measured: filter chips 82×34, "Play all" 92×36, ruler arrows 42×42, top-bar icons 40×40. All tappable but cramped; the filter row invites mis-taps.
- **Suggested fix:** Raise to **≥44px tall** with spacing.
- 🟢 **Fix (pending confirm) — 2026-06-14:** On phones/tablets (`@media max-width:1023px`), filter chips, "Play all", ruler arrows, and top-bar icons are now **≥44px**. Verified at 360/390px: filter chip 44, Play all 44, ruler arrow 44, top-bar icon 44. Desktop mouse left compact (chips 34, arrows 42, icons 40) on purpose.

### R-05 · 🟨 Nice-to-have — Mobile polish
- **Area:** Mobile add-flow + ruler
- **Raised by:** Coworker — "Prototype UI review" · 2026-06-14
- **Details:** A persistent mobile **"Add memory"** button and a **one-time touch hint** for the ruler. Responsiveness base is solid (correct viewport meta, mobile-first `flex-col → sm:flex-row`, `prefers-reduced-motion` respected, no real horizontal overflow).
- ⚠️ *May already be implemented locally (persistent ruler "+" add button + one-time hint/wiggle exist in the current build). Verify against the live build the reviewer saw — the review notes it reviewed an unchanged build.*

---

## ✅ Resolved Log (history — do not delete)

| ID | Area | Fix | Fixed | Confirmed |
|----|------|-----|-------|-----------|
| R-00 | Ruler | Timeline made discoverable — ↔ drag handle on the playhead + one-time wiggle + grab cursor + hint | 2026-06-14 | ⏳ pending |

### R-00 · Timeline interaction not discoverable → 🟢 Fixed (pending confirm)
- **Reported:** original "issue #1".
- **Fix:** Added a slider-style **↔ handle** on the playhead (always visible, desktop + mobile) + a **one-time wiggle** of the playhead/date-pill on load that stops on first interaction; kept the grab cursor and the "✦ Drag the ruler" hint. Dragging behavior unchanged (handle is decorative; the track still receives the drag).
- **Follow-up from reviewer:** grip needs a ≥44px invisible hit-area → tracked as **R-02**.

---

*Last updated: 2026-06-14 (build agent). Reviewer source: "Prototype UI review".*
