# Assignment 01 — CSS Selector Combinations

**Topic:** CSS selector combinations (relationships + attributes + pseudo-classes)

## Learning goals

By completing this assignment, you will be able to:

-   Write precise selectors using **descendant**, **child (`>`)**, **adjacent sibling (`+`)**, and **general sibling (`~`)** combinators.
-   Use **attribute selectors** to style UI states without extra classes.
-   Use pseudo-classes like `:hover`, `:focus-visible`, `:checked`, `:first-child`, `:nth-child()`.
-   Keep styles maintainable by scoping selectors and controlling specificity.

## Files in this folder

-   `practice.md` — warm-up tasks and mini examples
-   `starter/` — student starter project
-   `solution/` — one possible solution

## Rules

-   HTML + CSS only.
-   No frameworks, no CSS libraries.
-   Do not change the HTML structure in `starter/index.html` (you may add **attributes** if a task specifically asks you to).
-   Prefer selector combinations over adding new classes everywhere.

## Your task (comprehensive assignment)

You’re styling a small “UI playground” page with:

-   a header navigation
-   alert panels
-   a card list
-   a settings form
-   a footer

Your goal is to make it look clean and usable **using selector combinations**, not by over-classing everything.

### Part A — Base styling (required)

1. Global styles

    - Use a readable font stack.
    - Add comfortable page spacing.
    - Set a consistent `line-height`.

2. Focus and keyboard accessibility

    - Add visible focus styling for interactive elements using `:focus-visible`.
    - Ensure focus rings are not removed.

3. Links & buttons
    - Create consistent hover styling for links.
    - Buttons should have clear hover/active styles.

### Part B — Navigation (required)

Using selector combinations:

-   Style only the navigation links inside the header nav (not the brand link).
-   Style the “current page” link using `[aria-current="page"]`.
-   Add spacing between nav items using selectors (no extra markup).

### Part C — Panels (required)

Panels are marked up as `.panel` with `data-variant`.

-   Give every `.panel` a border, padding, and rounded corners.
-   Use attribute selectors to create a different accent for:
    -   `data-variant="info"`
    -   `data-variant="warning"`
    -   `data-variant="success"`
-   Make the first paragraph after the `h2` in each panel italic using `+`.
-   Make the `.muted` paragraph smaller and lighter, but only inside panels.

### Part D — Cards (required)

Cards are `<article class="card" data-state="...">`.

-   Layout cards in a responsive grid.
-   Use attribute selectors to style states:
    -   `data-state="new"` (highlight)
    -   `data-state="active"` (strong border)
    -   `data-state="archived"` (reduce emphasis)
-   Style the card link, but only inside cards.
-   Add spacing between cards using the container (`.cards`) rather than adding margins to every card.

### Part E — Form (required)

The form contains labels, inputs, a select, and a hint paragraph.

-   Style only the inputs/selects inside `.settings`.
-   Add a subtle border and background.
-   Use `:required` to indicate required fields.
-   Use `:focus-visible` for input focus.
-   Style the hint text via `.settings .hint` but do not affect other `.hint` classes elsewhere.

### Part F — Specificity control (required)

-   Use at least **two** of these to keep specificity low and maintainable:
    -   `:where(...)`
    -   `:is(...)`
    -   scoped selectors (e.g. `.settings input`, `.cards > .card`)
-   Do not use `!important`.

## Deliverables

Submit either:

-   a folder named `assignment-01-your-name/` containing `index.html` + `styles.css`

OR

-   a GitHub repository link with:
    -   `index.html`
    -   `styles.css`
    -   a short `README.md` explaining your selector strategy

## Rubric (100 points)

-   Selector combinations used correctly (25)
-   Attribute selectors + state styling (20)
-   Accessibility: focus-visible, readable contrast, labels intact (20)
-   Layout + spacing: grid, consistent rhythm (20)
-   Maintainability: scoped selectors, low specificity, no `!important` (15)

## Extension (optional)

-   Add a light/dark theme using `[data-theme="dark"]` on `html`.
-   Use `prefers-reduced-motion` to reduce transitions.

## How to start

1. Open `starter/index.html` in your browser.
2. Edit `starter/styles.css`.
3. Compare with `solution/` only after you’ve tried.
