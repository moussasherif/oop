# Course study website: instructions for Claude

You are maintaining my course study website: a single file, `index.html`, in this folder. It is hosted on GitHub Pages, so loading libraries and fonts from the internet is fine.

When I ask you to add a lecture, your job that session is to add ONE new lecture to it, following everything below.

## INPUTS

I will give you these at the start of the session:

- Lecture file: [LECTURE FILE NAME, e.g. lec05.pdf]
- Tutorial / assignment file (optional): [FILE NAME or "none"]
- Course: [COURSE NAME]
- Lecture number and title: [e.g. Lecture 5 - Decision Trees]
- Style reference: `style-reference.png` in this folder (match it exactly: colors, fonts, spacing, card shapes, header style, overall feel)

If any input is missing, ask me before starting.

## STEP 0 - CHECK THE CURRENT STATE

- If `index.html` does not exist, build the full site shell first (see SITE STRUCTURE), then add the lecture.
- If it exists, read it fully. Do NOT rewrite or restyle existing lectures. Only insert new content at the marked places and update the summary page.

## STEP 1 - READ THE LECTURE COMPLETELY

- Read every slide/page of the lecture file, including image-only slides. Note each slide number.
- Make an internal checklist of every concept, definition, formula, example, diagram, table, code snippet, and note.
- Nothing from the lecture may be dropped. Before finishing, go through the checklist and confirm every item appears in the page.
- If a tutorial or assignment file is provided, read it completely too.

## SITE STRUCTURE (one HTML file, CSS and JS inline)

- Sidebar/top nav grouped by course, listing every lecture, plus a "Summary & Exam Review" page.
- Each lecture is its own view (hash routing, e.g. `#course-lec05`), only one view visible at a time.
- Use clear insertion markers so future sessions can add content safely:
  ```
  <!-- NAV:[course-id]:END -->
  <!-- LECTURES:END -->
  <!-- SUMMARY:[course-id]:END -->
  ```
  If a course is new, create its nav group and summary block with these markers.
- Responsive on mobile, supports light and dark mode.
- Use any CDN libraries that help (e.g. KaTeX for math, highlight.js for code, Mermaid for diagrams), pinned to exact versions.

## LECTURE PAGE RULES

- Simple English. Short sentences. Explain every technical term the first time it appears. Use everyday analogies to explain hard ideas.
- Follow the lecture's order. One section per topic.
- Each section contains:
  1. A short plain-language explanation
  2. The original definitions, formulas, and examples, kept accurate (rebuild diagrams as SVG or Mermaid, tables as HTML tables)
  3. An analogy or "think of it like..." box when the idea is abstract
  4. A small slide reference tag, e.g. "📄 Slides 12-15", so I can go back to the original file
- Make it interactive and dynamic:
  - Collapsible "show more detail" blocks for long material
  - Flip cards for key terms (term on front, definition on back)
  - Step-by-step reveal for algorithms, derivations, or worked examples
  - Reading progress bar and a "mark as done" toggle per section
  - Smooth but subtle animations, nothing distracting
- End of each lecture page: "Lecture Recap" with key points, key formulas, and common exam traps.

## QUESTIONS RULE

- Do NOT write any questions, quizzes, or practice problems on your own.
- Only if a tutorial or assignment file is provided: add a "Practice" section at the end of the lecture page using those questions. Keep the original wording, show the solution hidden until clicked, link each question to the lecture section it tests, and add the tutorial/assignment question number as a reference.
- If no tutorial or assignment is provided, the lecture page has no questions at all.

## SUMMARY & EXAM REVIEW PAGE

- Append this lecture's block to its course section inside the summary page (do not touch other lectures' blocks).
- Each block contains:
  - Lecture title + link to the full lecture page
  - 5-10 must-know points
  - All formulas and definitions in a compact reference table
  - Slide references for each point
  - Practice questions only if they came from a provided tutorial or assignment (solutions hidden until clicked)
- Keep the summary page printable (clean print stylesheet).

## FINAL CHECKS BEFORE YOU FINISH

- Every checklist item from the lecture file is covered. List any item you were unsure about.
- Every section has a slide reference.
- No invented questions anywhere.
- Old lectures still render and navigate correctly.
- No console errors. Open the file and verify.
- Report back briefly: sections added, whether a tutorial/assignment was used, and any slide content that was unclear or unreadable.

## Notes about this repo (current state)

The site shell is in place. Lectures so far (course id `oop`):

| View | Lecture | Notes |
|---|---|---|
| `#oop-lec01` | Lecture 1 - Introduction to OOP | Older page with its own script; its 9 parts are paged with Back/Next |
| `#oop-lec01p2` | Lecture 1 (Part 2) - Introduction to Java Basics | Uses the shared components below; Lab 1 notes and practice at the end |
| `#summary` | Summary & Exam Review | One `.sum-block` per lecture |

**Where things go in `index.html`:**
- Nav: a new lecture's `<a class="navi" href="#oop-lecNN" data-view="oop-lecNN">` plus an empty `<div class="subnav" data-for="oop-lecNN"></div>`, just before `<!-- NAV:oop:END -->`. A new course gets its own `<div class="course">` before `<!-- NAV:COURSES:END -->`.
- Lecture: `<article class="view lecture" data-view="oop-lecNN" data-title="…" data-short="…" hidden>` just before `<!-- LECTURES:END -->`.
- Summary: a `<div class="sum-block" id="sum-oop-lecNN">` just before `<!-- SUMMARY:oop:END -->`. A new course gets a `<section class="sum-course">` before `<!-- SUMMARY:COURSES:END -->`.
- Links: `#<view>` opens a view, and `#<view>:<section>` opens it and scrolls to the element with id `<view>-<section>`.

**Shared components (no extra JavaScript needed; see `#oop-lec01p2` for working examples):**
- Section: `<section class="lec-sec" id="oop-lecNN-topic" data-nav="Short label">` with a `.kicker`, an `<h2>` (key words in `<span class="hl">`), then `<div class="sec-head"><span class="slide-tag">📄 Slides 12–15</span></div>`. The "mark as done" button, sidebar sub-link, scroll highlight and progress bar are added automatically. Use `data-num="R"` (or similar) for non-numbered sections.
- Analogy box: `<div class="callout"><p><b>Think of it like…</b> …</p></div>`. Warning box: `.heads`.
- More detail: `<details class="more"><summary>Show more detail: …</summary><div class="more-in">…</div></details>`. Solutions use `details.sol`.
- Flip cards: `.flips > button.flip > .flip-in > .flip-f (term) + .flip-b (definition)`.
- Step-by-step reveal: `<div class="reveal card" data-reveal><ol class="rv-steps"><li>…</li></ol></div>` (buttons are added automatically).
- Code: `<pre class="code" data-java>` is colored automatically (escape `<` as `&lt;` and `&` as `&amp;`). Console output: `<pre class="out">`.
- Code anatomy: `[data-anat]` with `.part[data-part]` spans in the code and one `<template data-part data-label>` per explanation.
- Lab or tutorial pages: `<span class="slide-tag lab">🧪 Lab 1 · p. 25</span>`. Lab 1 references use PDF page numbers (the number printed on each lab slide is one higher).
- A lecture's own widgets go in one inline `<script>` at the end of its `<article>`. It can use the helpers defined in the `<head>` script: `$`, `$$`, `esc`, `store`, `hlj`. Do not redeclare them.

**Things to know:**
- Lecture 1 has a 10-question "Test yourself" quiz that was written before the questions rule. Leave it as it is unless I say to remove it, and do not copy it into the summary page.
- Lecture 1's 31 slide images are embedded as base64 in the `SLIDES` object, all on one very long line (about 2.6 MB). Skip that line when reading the file. Do not print it or try to edit it by hand.
- The CSS matches `style-reference.png`: color tokens on `:root` (with dark mode versions), the dark sidebar, `.kicker` labels, `.hl` blue key words, and white `.card` boxes with a `.card-h` header. Reuse these instead of writing new styles.
- `java` and `javac` are usually available: run the lecture's code examples to check every output you show.
