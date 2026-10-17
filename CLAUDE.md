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

- `index.html` currently holds one lecture: **OOP, Lecture 1 - Introduction to OOP** (course id: `oop`). It was built before these rules, so it has **no insertion markers, no hash routing and no summary page**. Its 9 parts are switched by the `show()` function with Back/Next buttons.
- **The first time you add a lecture**, convert the file into the site shell described above, once: put Lecture 1 in an OOP nav group as view `#oop-lec01`, add the markers, and create the Summary & Exam Review page with a block for Lecture 1 too. Keep Lecture 1's text, interactive parts and look the same. Only move it into the new structure.
- Lecture 1 has a 10-question "Test yourself" quiz that was written before the questions rule. Leave it as it is unless I say to remove it, and do not copy it into the summary page.
- Lecture 1's 31 slide images are embedded as base64 in the `SLIDES` object, all on one very long line (about 2.6 MB). Skip that line when reading the file. Do not print it or try to edit it by hand.
- The current CSS already matches `style-reference.png`: color tokens on `:root` (with dark mode versions), the dark sidebar (`.side`, `.navi`, `.gs`), `.kicker` labels above titles, `.hl` for blue key words, and white `.card` boxes with a `.card-h` header. Reuse these for new lectures instead of writing new styles.
