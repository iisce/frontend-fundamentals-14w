# Assignment 02 — Flexbox (Practice)

Use this file as **warm-up practice** before you start the full assignment.

Goal: get comfortable with:

-   `display: flex` + main axis vs cross axis
-   `justify-content`, `align-items`, `align-content`
-   `gap`, `flex-wrap`
-   `flex: grow shrink basis` and common patterns

---

## How to use this practice

1. Create a scratch HTML file.
2. Paste the markup from each section.
3. Write CSS rules until the layout matches the instructions.
4. Use DevTools to toggle flex properties live.

---

## Practice 1 — Center a badge

**Markup**

```html
<div class="badge-row">
	<span class="badge">New</span>
</div>
```

**Tasks**

-   Make `.badge-row` a flex container.
-   Center `.badge` horizontally and vertically.
-   Add `min-height: 120px` to `.badge-row`.

---

## Practice 2 — Navigation that wraps

**Markup**

```html
<nav
	class="top-nav"
	aria-label="Practice nav"
>
	<a href="#">Home</a>
	<a href="#">Projects</a>
	<a href="#">Blog</a>
	<a href="#">Contact</a>
	<a href="#">Longer Link Example</a>
</nav>
```

**Tasks**

-   Make the links a row using flex.
-   Add spacing with `gap` (no margins).
-   Allow wrapping on narrow screens.
-   Align items vertically in the center.

---

## Practice 3 — Card row with equal-height cards

**Markup**

```html
<section
	class="row"
	aria-label="Cards"
>
	<article class="card">
		<h2>Card A</h2>
		<p>Short text.</p>
		<a href="#">Details</a>
	</article>

	<article class="card">
		<h2>Card B</h2>
		<p>This card has a longer description to force different heights.</p>
		<a href="#">Details</a>
	</article>

	<article class="card">
		<h2>Card C</h2>
		<p>Medium text length here.</p>
		<a href="#">Details</a>
	</article>
</section>
```

**Tasks**

-   Make `.row` a flex container.
-   Add a `gap`.
-   Make cards equal height.
-   Make each card take equal width.
-   Make the link stick to the bottom of each card (hint: flex column inside `.card`).

---

## Practice 4 — Sidebar layout

**Markup**

```html
<div class="layout">
	<aside class="sidebar">
		<h2>Filters</h2>
		<ul>
			<li><a href="#">All</a></li>
			<li><a href="#">Active</a></li>
			<li><a href="#">Archived</a></li>
		</ul>
	</aside>

	<main class="content">
		<h1>Results</h1>
		<p>Content goes here.</p>
	</main>
</div>
```

**Tasks**

-   Use flex so the sidebar is a fixed-ish width (e.g. `260px`).
-   Make content fill remaining space.
-   On narrow screens, stack sidebar on top (hint: media query + `flex-direction: column`).

---

## Practice 5 — `flex` shorthand

Answer in 1–2 sentences each:

1. What does `flex: 1;` expand to?
2. What’s the difference between `flex-basis: auto` and `flex-basis: 0`?
3. When would you use `justify-content: space-between` vs `gap`?

<details>
<summary>Suggested answers</summary>

1. `flex: 1` is commonly treated as `flex: 1 1 0%` (grow and shrink, basis 0).
2. `auto` bases sizing on content/width; `0` ignores content size so items share space more evenly.
3. `gap` adds consistent spacing; `space-between` pushes first/last to edges and distributes leftover space.

</details>
