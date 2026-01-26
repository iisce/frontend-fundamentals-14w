# Week 06 — Session 17: CSS Grid Fundamentals

**Navigation:**
← [Session 16](session-16.md) | [Week 06 Index](../week-06.md) | [Session 18](session-18.md) →

---

**Session Length:** 90 minutes

## 📋 Pre-Class Checklist

Before starting this session, make sure you have:

-   ✅ Completed Session 16 (Responsive Design)
-   ✅ Comfortable with the concept of Flexbox (one-dimensional layout)
-   ✅ Code editor (VS Code)

## 🎯 Learning Objectives

By the end of this session, you will be able to:

-   Understand the CSS Grid layout model (two-dimensional)
-   Create a grid container and define rows and columns
-   Use the `fr` unit for flexible sizing
-   Position items using line-based placement
-   Create named grid areas with `grid-template-areas`
-   Understand the difference between explicit and implicit grids

## 🔑 Key Terms

**CSS Grid**, **Grid Container**, **Grid Items**, **Grid Lines**, **Grid Tracks**, **Grid Cells**, **Grid Areas**, **fr unit**, **Explicit Grid**, **Implicit Grid**, **Grid Gap**, **Alignment**, **auto-fill**, **auto-fit**

---

## Part 1: Introduction to CSS Grid (15 minutes)

### What is CSS Grid?

**CSS Grid Layout** is the most powerful layout system available in CSS. It is a **two-dimensional** system, meaning it can handle both columns and rows at the same time, unlike Flexbox which is largely a one-dimensional system.

### Grid vs. Flexbox

-   **Flexbox:** One-dimensional (Row OR Column). Best for small-scale layouts and components (like a nav bar or centering items).
-   **Grid:** Two-dimensional (Row AND Column). Best for large-scale page layouts and complex horizontal/vertical structures.

You will often use **Grid** for the main page structure and **Flexbox** for the components inside the grid cells.

---

## Part 2: Defining Rows and Columns (25 minutes)

### Activating the Grid

```css
.container {
    display: grid;
}
```

### Grid Tracks (Rows and Columns)

You define the tracks of your grid using `grid-template-columns` and `grid-template-rows`.

```css
.container {
    display: grid;
    grid-template-columns: 200px 1fr 150px; /* 3 columns */
    grid-template-rows: 100px auto 100px; /* 3 rows */
}
```

### The `fr` Unit

The `fr` (fractional) unit represents a fraction of the available space in the grid container. It's much more flexible than percentages because it accounts for gaps automatically.

```css
.container {
    display: grid;
    grid-template-columns: 1fr 2fr 1fr; /* Middle column takes 50% of space, others 25% */
}
```

### Repeat and Minmax

Useful functions for defining large grids:

```css
.container {
    /* 12 equal columns */
    grid-template-columns: repeat(12, 1fr);

    /* Columns that are at least 200px but can expand to fill space */
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
}
```

#### `auto-fill` vs `auto-fit`

These keywords are used with `repeat()` to create responsive layouts without media queries.

-   **`auto-fill`**: Fills the row with as many columns as it can fit. Even if the columns are empty, they will take up space.
-   **`auto-fit`**: Also fills the row with columns, but then **collapses** any empty columns, stretching the remaining items to fill the entire row.

---

## Part 3: Spacing and Alignment (20 minutes)

### Gaps (Spacing)

The `gap` property (shorthand for `row-gap` and `column-gap`) is the modern way to add space between grid items.

```css
.container {
    display: grid;
    gap: 20px; /* 20px between all rows and columns */
    /* OR */
    row-gap: 30px;
    column-gap: 10px;
}
```

Unlike margins, `gap` only adds space **between** items, not around the edges of the container.

### Alignment

Grid items can be aligned both horizontally and vertically.

#### Aligning Items (Within their cells)
-   `justify-items`: Aligns items along the **inline (horizontal)** axis. (start, end, center, stretch)
-   `align-items`: Aligns items along the **block (vertical)** axis. (start, end, center, stretch)

```css
.container {
    justify-items: center;
    align-items: center;
}
```

> [!TIP]
> **Super Centering:** To perfectly center an item inside its grid cell (or the whole grid if it's the only item), use the shorthand:
> `place-items: center;`

#### Aligning Tracks (Within the container)
If your grid tracks are smaller than the container, you can align the tracks themselves using `justify-content` and `align-content`.

---

## Part 4: Grid Template Areas (20 minutes)

One of the most intuitive ways to use Grid is by naming areas and "drawing" the layout.

### Step 1: Name the Items
```css
.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.content { grid-area: content; }
.footer { grid-area: footer; }
```

### Step 2: Draw the Grid in the Container
```css
.container {
    display: grid;
    grid-template-columns: 200px 1fr;
    grid-template-rows: auto 1fr auto;
    grid-template-areas:
        "header header"
        "sidebar content"
        "footer footer";
    height: 100vh;
}
```

**This creates a layout where the header and footer span full width, while the sidebar and content sit side-by-side in the middle.**

---

## Part 4: Positioning Items (20 minutes)

You can also position items using the grid lines.

### Line-Based Placement

```css
.item {
    grid-column-start: 1;
    grid-column-end: 3; /* Spans across 2 columns */
    grid-row-start: 2;
    grid-row-end: 4; /* Spans across 2 rows */
}

/* Shorthand */
.item {
    grid-column: 1 / 3;
    grid-row: 2 / 4;
}

/* Span Keyword */
.item {
    grid-column: 1 / span 2;
}
```

---

## Part 6: Explicit vs. Implicit Grid (10 minutes)

-   **Explicit Grid:** The tracks you define manually using `grid-template-columns` and `grid-template-rows`.
-   **Implicit Grid:** Tracks created automatically by the browser when there are more items than defined cells.

You can control the sizing of these automatic tracks:

```css
.container {
    grid-auto-rows: 100px; /* Any automatically created row will be 100px tall */
    grid-auto-flow: row; /* Default: item fills rows. Can be 'column' */
}
```

---

## Part 7: Grid DevTools (5 minutes)

Modern browsers (Chrome, Firefox, Edge) have excellent Grid inspectors.
1.  Open **Developer Tools (F12)**.
2.  In the **Elements** panel, find your grid container.
3.  Click the small **"grid" badge** next to the element.
4.  This will overlay the grid lines, area names, and gaps directly on your website.

---

## 🎨 Hands-On Exercise: Simple Website Layout

**Goal:** Create a 2-column layout with a header and footer using `grid-template-areas`.

**Starter Code:**
```html
<div class="page-layout">
  <header>Header</header>
  <aside>Sidebar</aside>
  <main>Main Content</main>
  <footer>Footer</footer>
</div>
```

**Instruction:** Set up the Grid CSS.

<details>
<summary>✅ Solution</summary>

```css
.page-layout {
    display: grid;
    grid-template-columns: 250px 1fr;
    grid-template-rows: auto 1fr auto;
    grid-template-areas:
        "nav nav"
        "aside content"
        "foot foot";
    gap: 15px;
    min-height: 100vh;
}

header {
    grid-area: nav;
    background: #34495e;
    color: white;
    display: grid;
    place-items: center; /* Center header text */
}

aside {
    grid-area: aside;
    background: #ecf0f1;
    padding: 20px;
}

main {
    grid-area: content;
    background: #fff;
    padding: 30px;
}

footer {
    grid-area: foot;
    background: #2c3e50;
    color: white;
    padding: 10px;
    text-align: center;
}
```
</details>

---

## 🏡 Homework Assignment

**Create a Multi-Section Layout**

Build a layout that includes:
- A full-width header.
- A hero section.
- A 3-column features section.
- A main content area with a sidebar.
- A full-width footer.

**Rules:**
- Use `display: grid` for the main layout.
- Use `grid-template-areas` for at least one part of the layout.
- Use `gap` to separate sections.

---

**Navigation:**
← [Session 16](session-16.md) | [Week 06 Index](../week-06.md) | [Session 18](session-18.md) →
