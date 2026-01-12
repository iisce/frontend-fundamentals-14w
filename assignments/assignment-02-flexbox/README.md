# Assignment 02 — Flexbox

**Topic:** CSS Flexbox layouts (navigation, toolbars, cards, responsive patterns)

## Learning goals

By completing this assignment, you will be able to:

-   Build layouts using `display: flex` and understand **main axis vs cross axis**.
-   Use `justify-content`, `align-items`, `align-content`, `gap`, and `flex-wrap` effectively.
-   Control sizing with `flex: grow shrink basis` and patterns like `flex: 1`.
-   Create common UI layouts: header nav, toolbar, card rows, sidebar + content.
-   Keep layouts responsive without relying on fixed widths everywhere.

## Files in this folder

-   `practice.md` — warm-up flexbox tasks
-   `starter/` — student starter project
-   `solution/` — one possible solution

## Rules

-   HTML + CSS only.
-   No frameworks, no CSS libraries.
-   Do not change the HTML structure in `starter/index.html`.
-   Use Flexbox for layout in this assignment (Grid is not allowed for the main layouts).

## Your task (comprehensive assignment)

You are styling a small “product dashboard” page using Flexbox.

The page includes:

-   a header with brand + nav + profile action
-   a toolbar with filters and actions
-   a responsive set of cards
-   a two-column layout (sidebar + main)
-   a footer

### Part A — Base styling (required)

1. Global styles

    - Apply a readable font stack.
    - Add consistent page spacing.
    - Set a consistent `line-height`.

2. Focus and keyboard accessibility
    - Add visible focus styling for interactive elements using `:focus-visible`.
    - Keep good contrast and don’t remove outlines.

### Part B — Header layout (required)

Use Flexbox to:

-   Place the brand on the left, nav in the middle, and profile button on the right.
-   Allow the nav to wrap on small screens.
-   Add spacing between nav links using `gap`.

Required Flexbox properties in this part:

-   `display: flex`
-   `gap`
-   `flex-wrap`

### Part C — Toolbar layout (required)

The toolbar contains:

-   a search input
-   a status select
-   an “Add item” button

Use Flexbox to:

-   Align items nicely on one row.
-   On small screens, stack the controls.
-   Make the search input grow to take available space (hint: `flex: 1`).

Required Flexbox properties in this part:

-   `flex` (shorthand)
-   `align-items`
-   responsive `flex-direction`

### Part D — Card row (required)

Cards are `.card` elements inside `.card-row`.

Use Flexbox to:

-   Create a responsive row of cards that wraps.
-   Make each card have a consistent minimum size.
-   Keep consistent spacing using `gap`.
-   Make each card’s footer actions stick to the bottom (hint: `flex-direction: column` on the card).

Required Flexbox properties in this part:

-   `flex-wrap`
-   `gap`
-   `flex-basis` (directly or via shorthand)

### Part E — Sidebar layout (required)

The `.layout` section contains a sidebar and main content.

Use Flexbox to:

-   Make sidebar a fixed-ish width.
-   Make the main content fill the remaining space.
-   On narrow screens, stack sidebar above content.

Required Flexbox properties in this part:

-   `flex` sizing (grow/shrink/basis)
-   responsive `flex-direction`

### Part F — Flexbox patterns (required)

Implement at least **three** of these patterns:

-   Use `margin-left: auto` to push one item to the far end.
-   Use `order` to change the visual order for small screens.
-   Use `align-self` to override a single item’s alignment.
-   Use `justify-content: space-between` in a safe place (not for general spacing when `gap` is better).

## Deliverables

Submit either:

-   a folder named `assignment-02-your-name/` containing `index.html` + `styles.css`

OR

-   a GitHub repository link with:
    -   `index.html`
    -   `styles.css`
    -   a short `README.md` explaining your flexbox decisions

## Rubric (100 points)

-   Flexbox used correctly for all layouts (30)
-   Responsiveness (wrap + stacking) (20)
-   Accessibility: focus-visible, readable UI, labels intact (20)
-   Spacing & alignment quality (gap, axes reasoning) (15)
-   Maintainability: clean CSS, minimal hacks, no `!important` (15)

## Extension (optional)

-   Add a “compact mode” using `[data-density="compact"]` on `body`.
-   Use `prefers-reduced-motion` to reduce transitions.

## How to start

1. Open `starter/index.html` in your browser.
2. Edit `starter/styles.css`.
3. Compare with `solution/` only after you’ve tried.
