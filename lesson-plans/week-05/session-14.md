# Week 05 — Session 14: Flexbox Deep Dive

**Navigation:**
← [Week 05 Session 13](session-13.md) | [Week 05 Index](../week-05.md) | [Session 15](session-15.md) →

---

**Session Length:** 90 minutes

## 📋 Pre-Class Checklist

Before starting this session, make sure you have:

-   ✅ Completed Session 13 (Introduction to Flexbox)
-   ✅ Understand flex container properties (`flex-direction`, `justify-content`, `align-items`)
-   ✅ Familiar with the main axis and cross axis concepts
-   ✅ Code editor (VS Code) with Live Server extension
-   ✅ Browser with Developer Tools (Chrome, Firefox, or Edge)
-   ✅ Create a new folder: `week-05-flexbox-deep`

## 🎯 Learning Objectives

By the end of this session, you will be able to:

-   Master flex item properties (`flex-grow`, `flex-shrink`, `flex-basis`)
-   Use the `flex` shorthand property effectively
-   Control individual item alignment with `align-self`
-   Change item display order with the `order` property
-   Build complex responsive layouts without media queries
-   Create common UI patterns (holy grail, sticky footer, equal height columns)
-   Understand when items grow, shrink, or maintain size
-   Debug Flexbox layouts using DevTools

## 📦 Files for This Session

-   `session-14.md` — This tutorial (you're reading it!)
-   `flex-items-template.html` — Starter file for practice
-   `flex-items-solution.html` — Complete working example
-   `flex-shorthand-cheat-sheet.md` — Quick reference guide
-   `flexbox-patterns.html` — Common layout patterns

## 🔑 Key Terms

**flex-grow**, **flex-shrink**, **flex-basis**, **flex shorthand**, **align-self**, **order**, **flex items**, **available space**, **positive free space**, **negative free space**, **flex factor**, **intrinsic size**, **automatic sizing**

## 🏗️ What You Will Build

-   A responsive dashboard layout
-   A holy grail layout with Flexbox
-   Equal-height card columns
-   A sticky footer layout
-   A pricing table with featured item
-   A media object pattern

---

## Part 1: Understanding Flex Item Properties (20 minutes)

### The Three Core Properties

Flex items have three fundamental properties that control their sizing:

| Property      | Description                           | Default |
| ------------- | ------------------------------------- | ------- |
| `flex-grow`   | How much item can grow to fill space  | `0`     |
| `flex-shrink` | How much item can shrink if needed    | `1`     |
| `flex-basis`  | Initial size before growing/shrinking | `auto`  |

**Together, these properties control how flex items distribute available space.**

### Flex-Basis: Setting Initial Size

**`flex-basis`** defines the initial main size of a flex item before space distribution.

**Syntax:**

```css
.item {
	flex-basis: auto; /* Default: use item's width/height */
	flex-basis: 200px; /* Fixed size */
	flex-basis: 50%; /* Percentage of container */
	flex-basis: 0; /* Zero size, item only uses grow/shrink */
	flex-basis: content; /* Size based on content */
}
```

**Example:**

```html
<div class="container">
	<div class="item item-1">Item 1</div>
	<div class="item item-2">Item 2</div>
	<div class="item item-3">Item 3</div>
</div>
```

```css
.container {
	display: flex;
	gap: 10px;
	background: lightgray;
	padding: 10px;
}

.item {
	background: coral;
	padding: 20px;
}

.item-1 {
	flex-basis: 100px;
} /* 100px initial size */
.item-2 {
	flex-basis: 200px;
} /* 200px initial size */
.item-3 {
	flex-basis: 150px;
} /* 150px initial size */
```

**Key points:**

-   `flex-basis: auto` — Uses the item's `width` (or `height` in column direction)
-   `flex-basis: 0` — Item starts with zero size, purely based on grow/shrink
-   When `flex-direction: row`, `flex-basis` controls width
-   When `flex-direction: column`, `flex-basis` controls height

### Flex-Grow: Expanding Items

**`flex-grow`** determines how much an item can grow relative to other items when there's **extra space**.

**Syntax:**

```css
.item {
	flex-grow: 0; /* Default: don't grow */
	flex-grow: 1; /* Can grow, equal share */
	flex-grow: 2; /* Grows twice as much as flex-grow: 1 */
}
```

**How it works:**

1. Browser calculates **available space** after placing all items
2. Distributes extra space based on `flex-grow` ratios
3. Items with `flex-grow: 0` don't expand

**Example:**

```html
<div class="grow-container">
	<div class="box box-1">Grow 0</div>
	<div class="box box-2">Grow 1</div>
	<div class="box box-3">Grow 2</div>
</div>
```

```css
.grow-container {
	display: flex;
	gap: 10px;
	width: 600px;
	background: lightgray;
	padding: 10px;
}

.box {
	background: skyblue;
	padding: 20px;
	flex-basis: 100px; /* All start at 100px */
}

.box-1 {
	flex-grow: 0;
} /* Stays 100px */
.box-2 {
	flex-grow: 1;
} /* Gets 1 share of extra space */
.box-3 {
	flex-grow: 2;
} /* Gets 2 shares of extra space */
```

**Calculation:**

-   Container: 600px
-   Used space: 100px + 100px + 100px = 300px
-   Available space: 600px - 300px = **300px**
-   Total grow factors: 0 + 1 + 2 = **3**
-   Each grow unit: 300px ÷ 3 = **100px**

**Final sizes:**

-   Box 1: 100px + (0 × 100px) = **100px**
-   Box 2: 100px + (1 × 100px) = **200px**
-   Box 3: 100px + (2 × 100px) = **300px**

### Flex-Shrink: Compressing Items

**`flex-shrink`** determines how much an item can shrink when there's **not enough space**.

**Syntax:**

```css
.item {
	flex-shrink: 1; /* Default: can shrink equally */
	flex-shrink: 0; /* Cannot shrink (maintains size) */
	flex-shrink: 2; /* Shrinks twice as much as flex-shrink: 1 */
}
```

**Example:**

```html
<div class="shrink-container">
	<div class="box box-1">No Shrink</div>
	<div class="box box-2">Shrink 1</div>
	<div class="box box-3">Shrink 2</div>
</div>
```

```css
.shrink-container {
	display: flex;
	gap: 10px;
	width: 400px; /* Smaller container */
	background: lightgray;
	padding: 10px;
}

.box {
	background: lightcoral;
	padding: 20px;
	flex-basis: 200px; /* All want to be 200px */
}

.box-1 {
	flex-shrink: 0;
} /* Won't shrink */
.box-2 {
	flex-shrink: 1;
} /* Normal shrinking */
.box-3 {
	flex-shrink: 2;
} /* Shrinks twice as much */
```

**Calculation:**

-   Container: 400px
-   Desired space: 200px + 200px + 200px = 600px
-   Overflow: 600px - 400px = **200px over**
-   Total shrink factors: 0 + 1 + 2 = **3**
-   Each shrink unit: 200px ÷ 3 = **66.67px**

**Final sizes:**

-   Box 1: 200px - (0 × 66.67px) = **200px** (maintains size!)
-   Box 2: 200px - (1 × 66.67px) = **133.33px**
-   Box 3: 200px - (2 × 66.67px) = **66.67px**

<details>
<summary>💡 Knowledge Check #1</summary>

**Question:** What's the difference between `flex-basis: 0` and `flex-basis: auto`?

**Answer:**

**`flex-basis: auto` (default):**

-   Uses the item's content size or explicit `width`/`height`
-   Item starts with its natural/specified size
-   Then grows or shrinks from that base

**Example:**

```css
.item {
	width: 200px;
	flex-basis: auto; /* Uses 200px as starting size */
	flex-grow: 1;
}
```

**`flex-basis: 0`:**

-   Item starts with **zero size**
-   Ignores content size and `width`/`height`
-   Size determined entirely by `flex-grow`
-   Creates truly equal-sized items when all have same `flex-grow`

**Example:**

```css
.item {
	width: 200px; /* Ignored! */
	flex-basis: 0; /* Starts at 0px */
	flex-grow: 1; /* Only grow determines size */
}
```

**Practical use case:**

```css
/* ❌ Unequal sizes (content affects final size) */
.item {
	flex: 1 1 auto; /* flex-basis: auto */
}

/* ✅ Perfectly equal sizes (content doesn't affect size) */
.item {
	flex: 1 1 0; /* flex-basis: 0 */
}
```

**Key takeaway:** Use `flex-basis: 0` with `flex-grow: 1` for truly equal-sized items, regardless of content.

</details>

---

## Part 2: The Flex Shorthand Property (15 minutes)

### Understanding the Flex Shorthand

The `flex` property is a shorthand for `flex-grow`, `flex-shrink`, and `flex-basis`.

**Syntax:**

```css
.item {
	flex: <grow> <shrink> <basis>;
}

/* Examples */
.item {
	flex: 0 1 auto; /* Default (same as no flex property) */
	flex: 1; /* Shorthand for: 1 1 0 */
	flex: 1 1 200px; /* grow: 1, shrink: 1, basis: 200px */
	flex: 0 0 250px; /* Fixed 250px, no grow or shrink */
}
```

### Common Flex Shorthand Values

| Shorthand         | Expansion   | Use Case                                          |
| ----------------- | ----------- | ------------------------------------------------- |
| `flex: initial`   | `0 1 auto`  | Default: don't grow, can shrink, based on content |
| `flex: auto`      | `1 1 auto`  | Flexible: can grow and shrink, based on content   |
| `flex: none`      | `0 0 auto`  | Inflexible: fixed size, can't grow or shrink      |
| `flex: 1`         | `1 1 0`     | Equal sizing: distribute space equally            |
| `flex: 2`         | `2 1 0`     | Double sizing: twice as much space as `flex: 1`   |
| `flex: 0 0 200px` | `0 0 200px` | Fixed size: exactly 200px                         |

### Practical Examples

**Equal-width columns:**

```css
.container {
	display: flex;
}

.column {
	flex: 1; /* Equal width columns */
}
```

**Sidebar with main content:**

```css
.container {
	display: flex;
}

.sidebar {
	flex: 0 0 250px; /* Fixed 250px sidebar */
}

.main {
	flex: 1; /* Main takes remaining space */
}
```

**Three-column layout (1:2:1 ratio):**

```css
.container {
	display: flex;
}

.left {
	flex: 1; /* 1 share */
}

.center {
	flex: 2; /* 2 shares (twice as wide) */
}

.right {
	flex: 1; /* 1 share */
}
```

**Fixed, flexible, and auto-width:**

```css
.container {
	display: flex;
}

.fixed {
	flex: 0 0 200px; /* Always 200px */
}

.flexible {
	flex: 1; /* Takes remaining space */
}

.auto {
	flex: 0 1 auto; /* Based on content, can shrink */
}
```

### Best Practices

**Do:**

```css
/* ✅ Use shorthand for clarity */
.item {
	flex: 1 1 0;
}

/* ✅ Use common keywords */
.item {
	flex: auto; /* Clear intent */
}
```

**Don't:**

```css
/* ❌ Avoid mixing shorthand and longhand */
.item {
	flex: 1;
	flex-basis: 200px; /* Confusing! */
}

/* ❌ Don't use inconsistent values */
.item-1 {
	flex: 1 1 auto;
}
.item-2 {
	flex: 1;
} /* Different basis! */
```

<details>
<summary>💡 Knowledge Check #2</summary>

**Question:** What's the difference between `flex: 1` and `flex: auto`?

**Answer:**

**`flex: 1`:**

-   Expands to: `flex: 1 1 0`
-   `flex-basis: 0` — starts with zero size
-   Size determined entirely by `flex-grow`
-   Creates **equal-sized items** regardless of content

**Visual:**

```
Container (600px):
┌────────────┬────────────┬────────────┐
│   Item 1   │   Item 2   │   Item 3   │ ← All 200px
│  (small)   │  (large)   │  (medium)  │   (equal!)
└────────────┴────────────┴────────────┘
```

**`flex: auto`:**

-   Expands to: `flex: 1 1 auto`
-   `flex-basis: auto` — starts with content/width size
-   Content size affects final size
-   Creates **flexible items** that can grow/shrink but respect content

**Visual:**

```
Container (600px):
┌──────┬──────────────────┬──────────┐
│ Item │     Item 2       │  Item 3  │ ← Unequal!
│  1   │  (large content) │          │   (content-based)
└──────┴──────────────────┴──────────┘
```

**When to use:**

**`flex: 1`:**

-   Equal-width columns
-   Card grids where all cards should be same size
-   Dashboard panels

**`flex: auto`:**

-   Navigation links (size based on text length)
-   Tabs (adapt to label width)
-   Buttons in a toolbar

**Example:**

```css
/* Equal-width cards */
.card {
	flex: 1; /* All cards same width */
}

/* Flexible navigation */
.nav-item {
	flex: auto; /* Adapt to content, but can grow */
}
```

</details>

---

## Part 3: Individual Item Control (20 minutes)

### Align-Self: Individual Alignment

**`align-self`** overrides the container's `align-items` for a specific item.

**Syntax:**

```css
.item {
	align-self: auto; /* Default: inherit from align-items */
	align-self: flex-start; /* Align to start of cross axis */
	align-self: flex-end; /* Align to end of cross axis */
	align-self: center; /* Center on cross axis */
	align-self: baseline; /* Align text baselines */
	align-self: stretch; /* Stretch to fill (default behavior) */
}
```

**Example:**

```html
<div class="container">
	<div class="box">Normal</div>
	<div class="box special">Centered</div>
	<div class="box">Normal</div>
</div>
```

```css
.container {
	display: flex;
	align-items: flex-start; /* All items align to top */
	height: 200px;
	background: lightgray;
	gap: 10px;
	padding: 10px;
}

.box {
	background: coral;
	padding: 20px;
}

.special {
	align-self: center; /* This one centers vertically */
	background: skyblue;
}
```

**Use cases:**

-   Highlighting a featured item
-   Different alignment for specific elements
-   Creating staggered layouts
-   Baseline-aligning text of different sizes

### Order: Changing Display Order

**`order`** controls the visual order of flex items without changing HTML.

**Syntax:**

```css
.item {
	order: 0; /* Default: display in source order */
	order: 1; /* Display after items with order: 0 */
	order: -1; /* Display before items with order: 0 */
}
```

**How it works:**

-   Items are sorted by `order` value (lowest to highest)
-   Items with the same `order` use source order
-   Default is `0`, so negative values appear first

**Example:**

```html
<div class="container">
	<div class="item item-1">First in HTML</div>
	<div class="item item-2">Second in HTML</div>
	<div class="item item-3">Third in HTML</div>
</div>
```

```css
.container {
	display: flex;
	gap: 10px;
}

.item {
	background: coral;
	padding: 20px;
}

.item-1 {
	order: 3;
} /* Displays last */
.item-2 {
	order: 1;
} /* Displays first */
.item-3 {
	order: 2;
} /* Displays middle */
```

**Visual result:**

```
HTML order: [1] [2] [3]
Display order: [2] [3] [1]
```

**Responsive reordering:**

```css
/* Desktop: sidebar on left */
.sidebar {
	order: 1;
}

.main {
	order: 2;
}

/* Mobile: main content first, sidebar after */
@media (max-width: 768px) {
	.container {
		flex-direction: column;
	}

	.sidebar {
		order: 2; /* Sidebar appears below */
	}

	.main {
		order: 1; /* Main content appears first */
	}
}
```

**Important accessibility note:**

⚠️ **`order` changes visual order only, not semantic order!**

-   Screen readers follow HTML source order
-   Keyboard navigation follows HTML source order
-   Use `order` for visual enhancement only
-   Don't use it to fix poor HTML structure

<details>
<summary>💡 Knowledge Check #3</summary>

**Question:** What happens when multiple items have the same `order` value?

**Answer:**

When multiple items have the same `order` value, they appear in **HTML source order** within that group.

**Example:**

```html
<div class="container">
	<div class="item a">A</div>
	<div class="item b">B</div>
	<div class="item c">C</div>
	<div class="item d">D</div>
</div>
```

```css
.a {
	order: 2;
}
.b {
	order: 1;
}
.c {
	order: 2;
}
.d {
	order: 1;
}
```

**Result:**

1. Items with `order: 1` → **B, D** (source order within group)
2. Items with `order: 2` → **A, C** (source order within group)

**Display order:** `[B] [D] [A] [C]`

**Grouping logic:**

-   Order groups: -1, 0, 1, 2, etc.
-   Within each group: HTML source order
-   Lower order numbers appear first

**Practical example:**

```css
/* Featured items first, normal items after */
.item {
	order: 0; /* Default: normal items */
}

.featured {
	order: -1; /* Featured items appear first */
}

/* Within featured items, they maintain HTML order */
```

</details>

---

## Part 4: Advanced Flexbox Patterns (25 minutes)

### Pattern 1: Holy Grail Layout with Flexbox

**Goal:** Header, footer, and three-column body (sidebar, main, sidebar).

```html
<div class="page">
	<header class="header">Header</header>

	<div class="content">
		<nav class="nav">Navigation</nav>
		<main class="main">Main Content</main>
		<aside class="aside">Sidebar</aside>
	</div>

	<footer class="footer">Footer</footer>
</div>
```

```css
.page {
	display: flex;
	flex-direction: column;
	min-height: 100vh;
}

.header,
.footer {
	flex: 0 0 auto; /* Fixed height based on content */
	background: #2c3e50;
	color: white;
	padding: 20px;
	text-align: center;
}

.content {
	flex: 1; /* Take remaining vertical space */
	display: flex; /* Nested flex container */
}

.nav {
	flex: 0 0 200px; /* Fixed 200px width */
	background: #ecf0f1;
	padding: 20px;
}

.main {
	flex: 1; /* Take remaining horizontal space */
	padding: 20px;
}

.aside {
	flex: 0 0 180px; /* Fixed 180px width */
	background: #fef5e7;
	padding: 20px;
}

/* Responsive: stack on mobile */
@media (max-width: 768px) {
	.content {
		flex-direction: column;
	}

	.nav,
	.aside {
		flex: 0 0 auto; /* Auto height on mobile */
		width: 100%;
	}

	.main {
		order: -1; /* Main content first on mobile */
	}
}
```

### Pattern 2: Sticky Footer

**Goal:** Footer always at bottom, even with little content.

```html
<div class="page-container">
	<header class="header">Header</header>
	<main class="main">Content (may be short)</main>
	<footer class="footer">Footer (always at bottom)</footer>
</div>
```

```css
.page-container {
	display: flex;
	flex-direction: column;
	min-height: 100vh; /* Full viewport height */
}

.header,
.footer {
	flex: 0 0 auto; /* Fixed size */
}

.header {
	background: #34495e;
	color: white;
	padding: 20px;
}

.main {
	flex: 1; /* Grows to fill available space */
	padding: 20px;
}

.footer {
	background: #2c3e50;
	color: white;
	padding: 20px;
	text-align: center;
}
```

**How it works:**

-   `min-height: 100vh` ensures container fills viewport
-   `flex: 1` on main makes it grow to push footer down
-   Footer always at bottom, even with minimal content

### Pattern 3: Equal Height Columns

**Goal:** Columns with different content but same height.

```html
<div class="card-container">
	<div class="card">
		<h3>Short Content</h3>
		<p>Brief text.</p>
	</div>
	<div class="card">
		<h3>Medium Content</h3>
		<p>
			This card has more content. Lorem ipsum dolor sit amet, consectetur
			adipiscing elit.
		</p>
	</div>
	<div class="card">
		<h3>Long Content</h3>
		<p>
			This card has the most content. Lorem ipsum dolor sit amet,
			consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut
			labore et dolore magna aliqua. Ut enim ad minim veniam.
		</p>
	</div>
</div>
```

```css
.card-container {
	display: flex;
	gap: 20px;
}

.card {
	flex: 1; /* Equal width */
	padding: 20px;
	background: white;
	border: 1px solid #ddd;
	border-radius: 8px;

	/* Flexbox stretches items by default (align-items: stretch) */
	/* All cards will have the same height! */
}
```

**With footer at bottom of each card:**

```css
.card {
	flex: 1;
	padding: 20px;
	background: white;
	border: 1px solid #ddd;
	border-radius: 8px;

	/* Make card a flex container */
	display: flex;
	flex-direction: column;
}

.card-content {
	flex: 1; /* Push footer to bottom */
}

.card-footer {
	flex: 0 0 auto; /* Fixed size */
	padding-top: 15px;
	border-top: 1px solid #eee;
	margin-top: 15px;
}
```

### Pattern 4: Media Object

**Goal:** Image on left, content on right (common pattern for comments, posts, etc.).

```html
<div class="media">
	<img
		src="avatar.jpg"
		alt="User avatar"
		class="media-image"
	/>
	<div class="media-content">
		<h4>John Doe</h4>
		<p>
			This is a comment or post content that appears next to the avatar
			image.
		</p>
	</div>
</div>
```

```css
.media {
	display: flex;
	gap: 15px;
	padding: 15px;
	border-bottom: 1px solid #eee;
}

.media-image {
	flex: 0 0 60px; /* Fixed 60px width */
	width: 60px;
	height: 60px;
	border-radius: 50%;
	object-fit: cover;
}

.media-content {
	flex: 1; /* Take remaining space */
}

.media-content h4 {
	margin: 0 0 5px 0;
	color: #2c3e50;
}

.media-content p {
	margin: 0;
	color: #7f8c8d;
}
```

### Pattern 5: Pricing Table with Featured Item

**Goal:** Three pricing plans with middle one featured/highlighted.

```html
<div class="pricing-container">
	<div class="pricing-card">
		<h3>Basic</h3>
		<div class="price">$9/mo</div>
		<ul>
			<li>Feature 1</li>
			<li>Feature 2</li>
		</ul>
		<button>Choose Plan</button>
	</div>

	<div class="pricing-card featured">
		<div class="badge">Popular</div>
		<h3>Pro</h3>
		<div class="price">$29/mo</div>
		<ul>
			<li>All Basic features</li>
			<li>Feature 3</li>
			<li>Feature 4</li>
		</ul>
		<button>Choose Plan</button>
	</div>

	<div class="pricing-card">
		<h3>Enterprise</h3>
		<div class="price">$99/mo</div>
		<ul>
			<li>All Pro features</li>
			<li>Feature 5</li>
			<li>Feature 6</li>
		</ul>
		<button>Choose Plan</button>
	</div>
</div>
```

```css
.pricing-container {
	display: flex;
	gap: 20px;
	align-items: flex-end; /* Align to bottom */
	padding: 40px;
}

.pricing-card {
	flex: 1; /* Equal width */
	padding: 30px;
	background: white;
	border: 2px solid #ddd;
	border-radius: 8px;
	text-align: center;

	/* Make each card a flex container */
	display: flex;
	flex-direction: column;
}

.pricing-card h3 {
	font-size: 1.5rem;
	margin-bottom: 10px;
}

.price {
	font-size: 2rem;
	font-weight: bold;
	color: #3498db;
	margin-bottom: 20px;
}

.pricing-card ul {
	flex: 1; /* Push button to bottom */
	list-style: none;
	padding: 0;
	margin-bottom: 20px;
}

.pricing-card li {
	padding: 8px 0;
	border-bottom: 1px solid #eee;
}

.pricing-card button {
	padding: 12px 30px;
	background: #3498db;
	color: white;
	border: none;
	border-radius: 5px;
	cursor: pointer;
	font-size: 1rem;
}

/* Featured card styling */
.pricing-card.featured {
	border-color: #3498db;
	box-shadow: 0 10px 40px rgba(52, 152, 219, 0.2);
	transform: scale(1.05); /* Slightly larger */
	position: relative;
}

.badge {
	position: absolute;
	top: -15px;
	left: 50%;
	transform: translateX(-50%);
	background: #e74c3c;
	color: white;
	padding: 5px 20px;
	border-radius: 15px;
	font-size: 0.85rem;
	font-weight: bold;
}

.pricing-card.featured button {
	background: #e74c3c;
}
```

### Pattern 6: Responsive Dashboard Grid

**Goal:** Flexible grid that adapts to available space.

```html
<div class="dashboard">
	<div class="widget">
		<h3>Widget 1</h3>
		<p>Content here</p>
	</div>
	<div class="widget">
		<h3>Widget 2</h3>
		<p>Content here</p>
	</div>
	<div class="widget">
		<h3>Widget 3</h3>
		<p>Content here</p>
	</div>
	<div class="widget">
		<h3>Widget 4</h3>
		<p>Content here</p>
	</div>
</div>
```

```css
.dashboard {
	display: flex;
	flex-wrap: wrap;
	gap: 20px;
	padding: 20px;
}

.widget {
	flex: 1 1 300px; /* Minimum 300px, can grow */
	padding: 20px;
	background: white;
	border: 1px solid #ddd;
	border-radius: 8px;
	box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

/* Result:
   - Wide screen: 4 columns (if space allows)
   - Medium screen: 2-3 columns
   - Narrow screen: 1-2 columns
   All without media queries!
*/
```

---

## Part 5: Hands-On Practice (10 minutes)

### Exercise: Build a Responsive Card Layout

**Goal:** Create a card layout with flexible sizing and a featured card.

**Requirements:**

1. Three cards in a row on desktop
2. Featured card is wider than others
3. Cards have equal height
4. "Read More" button at bottom of each card
5. Wraps to column on mobile

**Starter code:**

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta
			name="viewport"
			content="width=device-width, initial-scale=1.0"
		/>
		<title>Flexbox Card Layout</title>
		<style>
			* {
				margin: 0;
				padding: 0;
				box-sizing: border-box;
			}

			body {
				font-family: Arial, sans-serif;
				background: #f5f5f5;
				padding: 40px 20px;
			}

			/* TODO: Create flex container */
			.card-grid {
				/* Add flexbox properties */
			}

			/* TODO: Style cards with flex properties */
			.card {
				background: white;
				padding: 25px;
				border-radius: 8px;
				box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
				/* Add flex properties */
				/* Make card a flex container for content */
			}

			/* TODO: Make featured card wider */
			.card.featured {
				/* Add flex properties for 2x width */
				background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
				color: white;
			}

			.card h3 {
				margin-bottom: 15px;
			}

			/* TODO: Make card-content push button to bottom */
			.card-content {
				/* Add flex property */
			}

			.card-footer {
				margin-top: 20px;
			}

			.btn {
				display: inline-block;
				padding: 10px 20px;
				background: #3498db;
				color: white;
				text-decoration: none;
				border-radius: 5px;
			}

			.featured .btn {
				background: white;
				color: #667eea;
			}
		</style>
	</head>
	<body>
		<div class="card-grid">
			<div class="card">
				<h3>Regular Card</h3>
				<div class="card-content">
					<p>This is a regular card with some content.</p>
				</div>
				<div class="card-footer">
					<a
						href="#"
						class="btn"
						>Read More</a
					>
				</div>
			</div>

			<div class="card featured">
				<h3>Featured Card</h3>
				<div class="card-content">
					<p>
						This is the featured card with more prominence. It's
						wider than the other cards and has a gradient
						background.
					</p>
				</div>
				<div class="card-footer">
					<a
						href="#"
						class="btn"
						>Read More</a
					>
				</div>
			</div>

			<div class="card">
				<h3>Regular Card</h3>
				<div class="card-content">
					<p>Another regular card with some content.</p>
				</div>
				<div class="card-footer">
					<a
						href="#"
						class="btn"
						>Read More</a
					>
				</div>
			</div>
		</div>
	</body>
</html>
```

<details>
<summary>✅ Solution</summary>

```css
.card-grid {
	display: flex;
	gap: 20px;
	max-width: 1200px;
	margin: 0 auto;
}

.card {
	flex: 1 1 0; /* Equal width for regular cards */
	background: white;
	padding: 25px;
	border-radius: 8px;
	box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);

	/* Make card a flex container */
	display: flex;
	flex-direction: column;
}

.card.featured {
	flex: 2 1 0; /* 2x width of regular cards */
	background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
	color: white;
}

.card h3 {
	margin-bottom: 15px;
}

.card-content {
	flex: 1; /* Pushes footer to bottom */
	margin-bottom: 15px;
}

.card-footer {
	margin-top: auto; /* Alternative to flex: 1 on content */
}

.btn {
	display: inline-block;
	padding: 10px 20px;
	background: #3498db;
	color: white;
	text-decoration: none;
	border-radius: 5px;
	transition: background 0.3s;
}

.btn:hover {
	background: #2980b9;
}

.featured .btn {
	background: white;
	color: #667eea;
}

.featured .btn:hover {
	background: #f0f0f0;
}

/* Responsive: stack on mobile */
@media (max-width: 768px) {
	.card-grid {
		flex-direction: column;
	}

	.card,
	.card.featured {
		flex: 1 1 auto; /* Reset flex properties */
	}
}
```

</details>

---

## 🐛 Common Mistakes and Troubleshooting

### Mistake 1: Forgetting Flex Basis with Flex Shorthand

**Problem:**

```css
/* ❌ Items may not be equal */
.item {
	flex-grow: 1;
	/* Missing flex-shrink and flex-basis */
}
```

**Solution:**

```css
/* ✅ Use complete shorthand */
.item {
	flex: 1 1 0; /* Or just: flex: 1 */
}
```

### Mistake 2: Using Width Instead of Flex-Basis

**Problem:**

```css
/* ❌ Mixing width with flex can cause conflicts */
.item {
	flex: 1;
	width: 300px; /* May be ignored or cause issues */
}
```

**Solution:**

```css
/* ✅ Use flex-basis */
.item {
	flex: 1 1 300px;
	/* Or separate: */
	flex-grow: 1;
	flex-shrink: 1;
	flex-basis: 300px;
}
```

### Mistake 3: Not Understanding Flex: 1 vs Flex: Auto

**Problem:**

```css
/* Different items with different flex values */
.item-1 {
	flex: 1;
} /* flex-basis: 0 */
.item-2 {
	flex: auto;
} /* flex-basis: auto */
/* Items won't be sized consistently */
```

**Solution:**

```css
/* ✅ Use consistent flex values */
.item {
	flex: 1; /* All items use flex-basis: 0 */
}
```

### Mistake 4: Min-Width/Max-Width Issues

**Problem:**

```css
/* ❌ Item won't shrink below content size */
.item {
	flex: 1;
	/* Default min-width: auto prevents shrinking below content */
}
```

**Solution:**

```css
/* ✅ Override min-width if needed */
.item {
	flex: 1;
	min-width: 0; /* Allow shrinking below content size */
}
```

### Mistake 5: Nested Flexbox Height Issues

**Problem:**

```css
/* ❌ Child flex container won't fill parent */
.parent {
	display: flex;
	height: 500px;
}

.child {
	display: flex;
	flex-direction: column;
	/* Height not specified */
}
```

**Solution:**

```css
/* ✅ Make child flex to fill parent */
.parent {
	display: flex;
	height: 500px;
}

.child {
	flex: 1; /* Fill parent height */
	display: flex;
	flex-direction: column;
}
```

---

## 🏡 Homework Assignment

**Build a Complete Dashboard Layout**

Create a responsive dashboard using all Flexbox concepts learned.

**Requirements:**

1. **Header** (fixed height)

    - Logo on left
    - User profile on right
    - Navigation in center

2. **Main Layout** (flex container)

    - Sidebar (fixed width, 250px)
    - Content area (remaining space)

3. **Content Area** (nested flex)

    - Stats cards (3 cards, equal width)
    - Featured widget (2x width of regular)
    - Activity feed

4. **Footer** (sticky at bottom)
    - Copyright and links

**Technical requirements:**

-   Use `flex` shorthand consistently
-   Implement `align-self` on at least one item
-   Use `order` for responsive reordering
-   Equal-height cards with buttons at bottom
-   Responsive: sidebar becomes top nav on mobile
-   No floats or positioning for layout

**Bonus challenges:**

-   Add a collapsible sidebar
-   Implement dark mode toggle
-   Add smooth transitions
-   Create a notification badge using absolute positioning within flex items

**Deliverables:**

-   `dashboard.html` — Complete HTML structure
-   External CSS file or inline styles
-   Comments explaining flex property choices
-   Responsive behavior without excessive media queries

**Submission:** Create a folder `session-14-homework` with your files.

---

## 📚 Additional Resources

### Documentation

-   [MDN: Flex](https://developer.mozilla.org/en-US/docs/Web/CSS/flex)
-   [MDN: flex-grow](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-grow)
-   [MDN: flex-shrink](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-shrink)
-   [MDN: flex-basis](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-basis)
-   [CSS Tricks: Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

### Deep Dives

-   [Understanding flex-grow, flex-shrink, and flex-basis](https://css-tricks.com/understanding-flex-grow-flex-shrink-and-flex-basis/)
-   [The Difference Between Width and Flex Basis](https://gedd.ski/post/the-difference-between-width-and-flex-basis/)
-   [Flexbox Holy Albatross](https://heydonworks.com/article/the-flexbox-holy-albatross/)

### Tools

-   [Flexbox Playground](https://flexbox.tech/)
-   [Flex Cheatsheet](https://yoksel.github.io/flex-cheatsheet/)

---

## 🎉 Session Summary

Congratulations! You've mastered advanced Flexbox concepts. You can now:

✅ Control item sizing with `flex-grow`, `flex-shrink`, and `flex-basis`
✅ Use the `flex` shorthand property effectively
✅ Understand the difference between `flex: 1`, `flex: auto`, and other values
✅ Align individual items with `align-self`
✅ Reorder items visually with the `order` property
✅ Build complex layouts (holy grail, sticky footer, equal-height columns)
✅ Create responsive designs without excessive media queries
✅ Debug flex layouts using DevTools

**Next session:** **Mini Project 1** — You'll apply all your Flexbox knowledge to build a complete responsive webpage from scratch!

---

**Navigation:**
← [Week 05 Session 13](session-13.md) | [Week 05 Index](../week-05.md) | [Session 15](session-15.md) →
