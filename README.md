# Lab 02 - HTML & CSS: build and style the Sudoku

This is the first of three labs in which you'll build a **Sudoku** web app:

| Lab | You add | Topic |
|-----|---------|-------|
| 02 | **HTML + CSS** | semantic markup, tables, the box model, Flexbox, responsive layout |
| 04 | basic JavaScript | game logic + tests |
| 05 | DOM + tooling | making it actually playable |

So this week is **structure + style**: semantic, valid, accessible HTML, then hand-written CSS to make it look like the screenshots. **No JavaScript yet** - we'll do that in subsequent labs.

## What you'll build

Two pages that share one header:

1. **`index.html`** - the game page: a 9×9 Sudoku **board** with starting clues, and a **palette** of the digits 1–9 plus an undo icon.
2. **`high_scores.html`** - a table of past games (date + duration).

Open `documentation_images/game_page_desktop.png`, `game_page_mobile.png`, and the two `high_scores_page_*.png` to see the target - both the desktop **and** the narrow-screen layout.

## Getting your copy of the starter repo

The starter for this lab is a **template repository** on GitHub (the link is on Canvas). Make your own copy of it - work in *your* copy, never in the template:

1. Open the template repo and click **Use this template → Create a new repository**.
2. Name it `csci3230u-lab-02-<your-github-username>`, set the visibility to **Private**, and create it.
3. Add your **lab instructor (TA)** and the **course instructor** as collaborators (**Settings → Collaborators and teams → Add people**) - your work cannot be marked if they cannot see it.
4. Clone your new copy and work there:

   ```bash
   git clone <your-repo-url>
   cd <your-repo-dir>
   ```

## The starter repo

| File / folder | Purpose |
|---------------|---------|
| `index.html` | the game page - `TODO` comments where your markup goes; already links the stylesheet |
| `high_scores.html` | the high-scores page - same |
| `styles/sudoku.css` | a stylesheet pre-filled with the **colour tokens** and section headings - you write the rules |
| `images/` | `logo.gif` (brand logo) and `undo.png` (the palette's undo icon) |
| `documentation_images/` | the target screenshots, for reference |

---

## Phase 1 - Structure (HTML)

### Part 1 - The shared site header

On **both** pages, build a `<header class="site-header">` containing:

- an `<a class="brand">` with the logo (`images/logo.gif`) and the brand text **Sudoku Centre**;
- a `<nav>` with two links: **Play Game** → `index.html`, and **High Scores** → `high_scores.html`.

You will literally copy this header into both files. We'll identify how to eliminate this kind of duplication in future labs.

### Part 2 - The board (`index.html`)

> **New to HTML tables?** They aren't in the lecture demos - [MDN: HTML tables](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/table) is a quick primer on `<table>`, `<tr>`, `<td>`, `<th>`, and `<thead>`/`<tbody>`.

A 9×9 grid is a **table**. Build a `<table id="board">` with 9 rows of 9 cells. Fill in the starting clues exactly as below (a `.` means an empty cell - leave that `<td>` empty):

```
 .  1  . | .  .  . | .  9  .
 .  .  4 | .  .  . | 2  .  .
 .  .  8 | .  .  5 | .  .  .
---------+---------+---------
 .  .  . | .  .  . | .  3  .
 2  .  . | .  4  . | 1  .  .
 .  .  . | .  .  . | .  .  .
---------+---------+---------
 .  .  1 | 8  .  . | 6  .  .
 .  3  . | .  .  . | .  8  .
 .  .  6 | .  .  . | .  .  .
```

(The `+`/`-`/`|` lines just show the 3×3 blocks - the *borders* come from CSS in Part 2.)

### Part 3 - The palette (`index.html`)

Below the board, a `<table id="palette" class="palette">` with a **single row**: the digits **1–9**, then a final cell holding the undo image (`images/undo.png`).

### Part 4 - The high-scores page (`high_scores.html`)

A table with a header row (**Date**, **Duration**) and these five rows. Use real table structure - `<thead>`/`<tbody>`, and `<th scope="col">` for the header cells:

| Date | Duration |
|------|----------|
| 2021/01/17 | 3:41 |
| 2021/01/21 | 4:01 |
| 2021/02/01 | 2:52 |
| 2021/02/17 | 3:08 |
| 2021/03/02 | 2:51 |

---

## Phase 2 - Style (CSS)

`styles/sudoku.css` is already linked from both pages and includes **colour tokens** (`:root`) and section headings. Write the rules under each heading so the pages match the screenshots. This is **native CSS only**.

### Part 5 - The board

- `border-collapse` the table; give each cell a fixed size and centre the digit.
- **Thin** lines between cells, and a **thick** line around each **3×3 block**. Hint: target every third column and row with `td:nth-child(3n)` and `tr:nth-child(3n) td`.
- A hover colour on cells (the `--color-hover` token).
- Add rules for `.user-input` and `.error` cells now - the JavaScript in Lab 05 switches these classes on.

### Part 6 - The palette

- Size and border the cells like a smaller board; a hover colour; and an `.active` style for the selected digit (used in later lab).

### Part 7 - The header (responsive)

- Lay the header out with **Flexbox**; push the nav to the right (`margin-left: auto`).
- Add `flex-wrap: wrap` so that on a narrow screen the nav drops below the brand. Check it against `game_page_mobile.png`.

### Part 8 - The high-scores table

- Comfortable padding, left-aligned headings, and an underline under the header row.

---

## Quality bar

- **Valid HTML** - paste each page into the [W3C validator](https://validator.w3.org/nu/) and fix any errors.
- **Semantic** - exactly one `<h1>` per page; `<header>`, `<nav>`, `<main>`; tables for tabular data only.
- **Accessible** - every `<img>` has a sensible `alt` (decorative logo → `alt=""`; the undo icon → `alt="Undo"`); links have real text; usable with the **Tab** key alone.
- **Responsive** - no horizontal scrolling on a phone: the board fits and the nav wraps (match the `*_mobile.png` screenshots).

## How to view it

Plain HTML + CSS, no scripts - just **double-click `index.html`** (or drag it into your browser). No server needed this week; that changes in later labs.

## How you're graded

- **Automated:** both pages pass the W3C validator with no errors.
- **By rubric:** semantic structure; correct board/palette/scores markup; the CSS (board cells + 3×3 block borders + hover + the state classes, the responsive Flexbox header, the scores table); accessibility; and the header appearing correctly on both pages.

There's nothing to "run" and nothing to upload - your **repository is your submission**.

## How to submit

Commit your work and **push to `origin`** before the deadline (use the Git workflow from Lab 01 - a branch + PR is good practice, though not required here). The graded state is whatever is on `main`.  Show your resulting pages to your lab instructor for proof of completion.

However, since lab marks do sometimes go missing, I would encourage everyone to submit the URL of their repository to Canvas as the submission for this lab assignment (and for all other labs).  If there are any lab mark discrepancies, at least we have your submission to re-mark it.

> **AI policy:** this lab is **hand-coded**. You may ask an AI assistant to *explain* a concept or *interpret* a failing test, but write the logic yourself. (A later lab is explicitly about coding *with* AI tools.) See `project/ai-policy.md`.
