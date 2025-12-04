# Week 05 — Session 13: Introduction to Flexbox

**Navigation:**
← [Week 04 Session 12](../week-04/session-12.md) | [Week 05 Index](../week-05.md) | [Session 14](session-14.md) →

---

**Session Length:** 90 minutes

## 📋 Pre-Class Checklist

Before starting this session, make sure you have:

-   ✅ Completed Week 04 (CSS Layout I with floats and positioning)
-   ✅ Understand the CSS box model and spacing
-   ✅ Familiar with traditional layout challenges (float collapse, clearfix)
-   ✅ Code editor (VS Code) with Live Server extension
-   ✅ Browser with Developer Tools (Chrome, Firefox, or Edge)
-   ✅ Create a new folder: `week-05-flexbox`

## 🎯 Learning Objectives

By the end of this session, you will be able to:

-   Understand the Flexbox layout model and when to use it
-   Create flex containers and control flex items
-   Master the main axis and cross axis concepts
-   Use `flex-direction` to control layout direction
-   Align items with `justify-content` and `align-items`
-   Control spacing with `gap` property
-   Wrap flex items with `flex-wrap`
-   Build common UI patterns (navigation, cards, centering)
-   Compare Flexbox advantages over float-based layouts

## 📦 Files for This Session

-   `session-13.md` — This tutorial (you're reading it!)
-   `flexbox-template.html` — Starter file for practice
-   `flexbox-solution.html` — Complete working example
-   `flexbox-cheat-sheet.md` — Quick reference guide
-   `flexbox-visual.html` — Interactive Flexbox playground

## 🔑 Key Terms

**Flexbox**, **flex container**, **flex items**, **main axis**, **cross axis**, **flex-direction**, **justify-content**, **align-items**, **align-content**, **flex-wrap**, **gap**, **one-dimensional layout**, **flex model**

## 🏗️ What You Will Build

-   A responsive navigation bar
-   A centered hero section
-   A flexible card grid
-   A horizontal list of tags/badges
-   A vertical sidebar layout

---

## Part 1: Understanding Flexbox (15 minutes)

### What is Flexbox?

**Flexbox (Flexible Box Layout)** is a modern CSS layout module designed for creating **one-dimensional layouts** (either rows or columns).

**Key concept:** Flexbox layouts work along a **single axis** at a time:

-   Horizontal (row) OR
-   Vertical (column)

**For two-dimensional layouts** (rows AND columns simultaneously), use **CSS Grid** (covered later).

### Why Flexbox?

**Problems Flexbox solves:**

❌ **Float layouts:**

-   Parent collapse issues
-   Require clearfix hacks
-   Hard to vertically center
-   Complex spacing

✅ **Flexbox advantages:**

-   No parent collapse
-   Easy alignment (horizontal and vertical)
-   Built-in spacing with `gap`
-   Flexible sizing and distribution
-   Responsive by design
-   Cleaner, more intuitive code

### Flexbox vs. Floats Comparison

**Same layout, different approaches:**

```css
/* Float approach (old) */
.container-float::after {
	content: '';
	display: table;
	clear: both;
}

.item-float {
	float: left;
	width: 33.33%;
	box-sizing: border-box;
}

/* Flexbox approach (modern) */
.container-flex {
	display: flex;
	gap: 20px; /* Easy spacing! */
}

.item-flex {
	flex: 1; /* Equal width, automatically */
}
```

**Result:** Same visual output, but Flexbox is:

-   Fewer lines of code
-   No clearfix needed
-   Easier to read and maintain
-   More flexible and responsive

### The Flexbox Model

**Two types of elements in Flexbox:**

1. **Flex Container** (parent) — Element with `display: flex`
2. **Flex Items** (children) — Direct children of the flex container

```html
<div class="flex-container">
	<!-- Flex Container -->
	<div class="item">Item 1</div>
	<!-- Flex Item -->
	<div class="item">Item 2</div>
	<!-- Flex Item -->
	<div class="item">Item 3</div>
	<!-- Flex Item -->
</div>
```

```css
.flex-container {
	display: flex; /* Activates Flexbox */
}
```

**What happens:**

-   `.flex-container` becomes a flex container
-   `.item` elements become flex items
-   Items arrange horizontally by default (in a row)
-   Items stretch to fill container height

### Main Axis vs. Cross Axis

**Flexbox has two axes:**

```
flex-direction: row (default)
┌─────────────────────────────────────┐
│                                     │ ↑
│  [Item 1] [Item 2] [Item 3]        │ │ Cross Axis
│  ─────────────────────────→        │ │
│         Main Axis                   │ ↓
└─────────────────────────────────────┘

flex-direction: column
┌──────────────┐
│   [Item 1]   │ ↓
│   [Item 2]   │ │
│   [Item 3]   │ │ Main Axis
│      ↓       │ │
└──────────────┘ ↓
 ← Cross Axis →
```

**Key concepts:**

-   **Main Axis:** Primary direction items flow (row = horizontal, column = vertical)
-   **Cross Axis:** Perpendicular to main axis
-   `justify-content`: Aligns along **main axis**
-   `align-items`: Aligns along **cross axis**

<details>
<summary>💡 Knowledge Check #1</summary>

**Question:** If `flex-direction: row`, which direction is the main axis and cross axis?

**Answer:**

**With `flex-direction: row` (default):**

-   **Main Axis:** Horizontal (left to right) →
-   **Cross Axis:** Vertical (top to bottom) ↓

**This means:**

-   `justify-content` controls horizontal alignment
-   `align-items` controls vertical alignment

**With `flex-direction: column`:**

-   **Main Axis:** Vertical (top to bottom) ↓
-   **Cross Axis:** Horizontal (left to right) →

**This means:**

-   `justify-content` controls vertical alignment
-   `align-items` controls horizontal alignment

**Key principle:** The axes change based on `flex-direction`, but `justify-content` always controls the **main axis** and `align-items` always controls the **cross axis**.

</details>

---

## Part 2: Flex Container Properties (25 minutes)

### Creating a Flex Container

**Activate Flexbox:**

```css
.container {
	display: flex; /* Block-level flex container */
}

/* Or */
.container {
	display: inline-flex; /* Inline-level flex container */
}
```

**Example:**

```html
<div class="flex-container">
	<div class="box">1</div>
	<div class="box">2</div>
	<div class="box">3</div>
</div>
```

```css
.flex-container {
	display: flex;
	background: lightgray;
	padding: 10px;
}

.box {
	background: coral;
	padding: 20px;
	margin: 5px;
	color: white;
	font-weight: bold;
}
```

**Default behavior:**

-   Items arrange in a row (horizontal)
-   Items start from the left
-   Items stretch to fill container height
-   Items don't wrap to new lines

### Flex-Direction: Controlling Flow

**Syntax:**

```css
.container {
	flex-direction: row; /* Default: left to right */
	flex-direction: row-reverse; /* Right to left */
	flex-direction: column; /* Top to bottom */
	flex-direction: column-reverse; /* Bottom to top */
}
```

**Examples:**

```css
/* Horizontal flow (default) */
.row-container {
	display: flex;
	flex-direction: row;
}
/* Result: [1] [2] [3] */

/* Reverse horizontal */
.row-reverse-container {
	display: flex;
	flex-direction: row-reverse;
}
/* Result: [3] [2] [1] */

/* Vertical flow */
.column-container {
	display: flex;
	flex-direction: column;
}
/* Result:
   [1]
   [2]
   [3]
*/

/* Reverse vertical */
.column-reverse-container {
	display: flex;
	flex-direction: column-reverse;
}
/* Result:
   [3]
   [2]
   [1]
*/
```

**Use cases:**

-   `row`: Horizontal navigation, card grids, toolbars
-   `row-reverse`: RTL languages, reversed priority display
-   `column`: Vertical navigation, sidebars, mobile layouts
-   `column-reverse`: Footer-first layouts, chat messages

### Justify-Content: Main Axis Alignment

**Controls spacing along the main axis:**

```css
.container {
	justify-content: flex-start; /* Default: items at start */
	justify-content: flex-end; /* Items at end */
	justify-content: center; /* Items centered */
	justify-content: space-between; /* Space between items */
	justify-content: space-around; /* Space around items */
	justify-content: space-evenly; /* Equal space everywhere */
}
```

**Visual representation (flex-direction: row):**

```
flex-start (default):
[1][2][3]___________________

flex-end:
___________________[1][2][3]

center:
_________[1][2][3]_________

space-between:
[1]_________[2]_________[3]

space-around:
___[1]______[2]______[3]___

space-evenly:
____[1]____[2]____[3]____
```

**Code examples:**

```html
<div class="container">
	<div class="item">Item 1</div>
	<div class="item">Item 2</div>
	<div class="item">Item 3</div>
</div>
```

```css
/* Center all items */
.container-center {
	display: flex;
	justify-content: center;
}

/* Push items to opposite ends */
.container-between {
	display: flex;
	justify-content: space-between;
}

/* Equal space distribution */
.container-evenly {
	display: flex;
	justify-content: space-evenly;
}
```

**Common use cases:**

| Value           | Use Case                                 |
| --------------- | ---------------------------------------- |
| `flex-start`    | Left-aligned content (default)           |
| `flex-end`      | Right-aligned content (e.g., navigation) |
| `center`        | Centered content (hero sections, modals) |
| `space-between` | Navigation with logo left, links right   |
| `space-around`  | Equal spacing around items               |
| `space-evenly`  | Card grids with perfect spacing          |

### Align-Items: Cross Axis Alignment

**Controls alignment along the cross axis:**

```css
.container {
	align-items: stretch; /* Default: fill container height */
	align-items: flex-start; /* Align to top */
	align-items: flex-end; /* Align to bottom */
	align-items: center; /* Vertically center */
	align-items: baseline; /* Align text baselines */
}
```

**Visual representation (flex-direction: row):**

```
stretch (default):
┌─────────────────────┐
│ [  Item 1  ]        │
│ [  Item 2  ]        │
│ [  Item 3  ]        │
└─────────────────────┘

flex-start:
┌─────────────────────┐
│ [Item 1] [Item 2]   │
│                     │
│                     │
└─────────────────────┘

flex-end:
┌─────────────────────┐
│                     │
│                     │
│ [Item 1] [Item 2]   │
└─────────────────────┘

center:
┌─────────────────────┐
│                     │
│ [Item 1] [Item 2]   │
│                     │
└─────────────────────┘
```

**Example:**

```css
/* Vertically center items */
.container-vcenter {
	display: flex;
	align-items: center;
	height: 300px; /* Container needs height */
}

/* Align to bottom */
.container-bottom {
	display: flex;
	align-items: flex-end;
	height: 300px;
}

/* Baseline alignment (for text) */
.container-baseline {
	display: flex;
	align-items: baseline;
}
```

### Perfect Centering with Flexbox

**Horizontal AND vertical centering (finally easy!):**

```css
.perfect-center {
	display: flex;
	justify-content: center; /* Horizontal center */
	align-items: center; /* Vertical center */
	height: 100vh; /* Full viewport height */
}
```

```html
<div class="perfect-center">
	<div class="centered-content">
		<h1>Perfectly Centered!</h1>
		<p>Both horizontally and vertically</p>
	</div>
</div>
```

**This was a nightmare with floats and positioning, but trivial with Flexbox!**

<details>
<summary>💡 Knowledge Check #2</summary>

**Question:** What's the difference between `justify-content: space-between` and `space-evenly`?

**Answer:**

**`space-between`:**

-   **First item** flush with the start
-   **Last item** flush with the end
-   **Equal space** between items
-   **No space** at the edges

**Visual:**

```
Container edges
↓                      ↓
[Item 1]    [Item 2]    [Item 3]
        ↑           ↑
    Equal space   Equal space
```

**`space-evenly`:**

-   **Equal space** everywhere
-   **Same space** at edges as between items
-   Items "float" in the container

**Visual:**

```
Container edges
↓                          ↓
   [Item 1]   [Item 2]   [Item 3]
  ↑       ↑           ↑           ↑
Space   Space       Space       Space
(all equal)
```

**When to use:**

-   **`space-between`:** Navigation with logo at left, links at right
-   **`space-evenly`:** Card grids where you want equal spacing all around

**Example:**

```css
/* Logo left, nav right */
.navbar {
	display: flex;
	justify-content: space-between;
}

/* Equal spacing card grid */
.card-grid {
	display: flex;
	justify-content: space-evenly;
}
```

</details>

### Flex-Wrap: Controlling Wrapping

**By default, flex items stay on one line. `flex-wrap` controls wrapping:**

```css
.container {
	flex-wrap: nowrap; /* Default: all items on one line */
	flex-wrap: wrap; /* Wrap to multiple lines */
	flex-wrap: wrap-reverse; /* Wrap in reverse order */
}
```

**Example:**

```html
<div class="flex-container">
	<div class="item">Item 1</div>
	<div class="item">Item 2</div>
	<div class="item">Item 3</div>
	<div class="item">Item 4</div>
	<div class="item">Item 5</div>
	<div class="item">Item 6</div>
</div>
```

```css
/* No wrapping (default) - items shrink to fit */
.no-wrap {
	display: flex;
	flex-wrap: nowrap; /* Items may overflow or shrink */
}

/* With wrapping - items wrap to next line */
.with-wrap {
	display: flex;
	flex-wrap: wrap;
}

.item {
	width: 200px;
	padding: 20px;
	margin: 10px;
	background: coral;
}
```

**Result with wrap:**

```
Container (600px wide):
[Item 1] [Item 2] [Item 3]
[Item 4] [Item 5] [Item 6]
```

### Gap: Spacing Between Items

**Modern spacing solution (no more margin hacks!):**

```css
.container {
	display: flex;
	gap: 20px; /* Equal gap all around */
	gap: 20px 40px; /* row-gap column-gap */
	row-gap: 20px; /* Vertical gap only */
	column-gap: 40px; /* Horizontal gap only */
}
```

**Example:**

```css
/* Equal 20px gap between all items */
.card-grid {
	display: flex;
	flex-wrap: wrap;
	gap: 20px;
}

/* Different vertical and horizontal gaps */
.custom-grid {
	display: flex;
	flex-wrap: wrap;
	gap: 30px 20px; /* 30px vertical, 20px horizontal */
}
```

**Before `gap` (old way):**

```css
/* ❌ Required margin hacks */
.item {
	margin: 10px; /* Spacing, but adds to edges too */
}

.container {
	margin: -10px; /* Negative margin to compensate */
}
```

**With `gap` (modern way):**

```css
/* ✅ Clean and simple */
.container {
	display: flex;
	gap: 20px; /* Perfect spacing, no hacks */
}
```

### Align-Content: Multi-Line Alignment

**Controls space between wrapped lines (only works with `flex-wrap: wrap`):**

```css
.container {
	align-content: stretch; /* Default: lines stretch to fill */
	align-content: flex-start; /* Lines at top */
	align-content: flex-end; /* Lines at bottom */
	align-content: center; /* Lines centered */
	align-content: space-between; /* Space between lines */
	align-content: space-around; /* Space around lines */
	align-content: space-evenly; /* Equal space everywhere */
}
```

**Important:** Only has an effect when:

1. `flex-wrap: wrap` is set
2. There are multiple lines of items
3. Container has extra vertical space

**Example:**

```css
.multi-line-container {
	display: flex;
	flex-wrap: wrap;
	align-content: space-between; /* Space between wrapped lines */
	height: 500px; /* Needs fixed height to see effect */
}
```

<details>
<summary>💡 Knowledge Check #3</summary>

**Question:** What's the difference between `align-items` and `align-content`?

**Answer:**

**`align-items`:**

-   Controls alignment of items **within each line**
-   Works on **single-line** and **multi-line** containers
-   Aligns items on the **cross axis**
-   Think: "How should items align in their line?"

**Example:**

```css
.container {
	display: flex;
	align-items: center; /* Center items vertically in their line */
}
```

**`align-content`:**

-   Controls alignment of **lines themselves**
-   Only works with **multi-line** containers (`flex-wrap: wrap`)
-   Distributes space **between lines**
-   Think: "How should the lines be spaced?"

**Example:**

```css
.container {
	display: flex;
	flex-wrap: wrap;
	align-content: space-between; /* Space between wrapped lines */
}
```

**Visual comparison:**

```
align-items: center (single line)
┌──────────────────────┐
│                      │
│  [Item] [Item] [Item]│
│                      │
└──────────────────────┘

align-content: space-between (multi-line)
┌──────────────────────┐
│ [Item] [Item] [Item] │ ← Line 1
│                      │
│                      │ ← Space
│                      │
│ [Item] [Item] [Item] │ ← Line 2
└──────────────────────┘
```

**Rule of thumb:**

-   **`align-items`:** Use for single-line layouts or to align items within lines
-   **`align-content`:** Use for multi-line layouts to control spacing between lines

</details>

---

## Part 3: Common Flexbox Patterns (25 minutes)

### Pattern 1: Horizontal Navigation Bar

**Goal:** Logo on left, navigation links on right.

```html
<nav class="navbar">
	<div class="logo">My Website</div>
	<ul class="nav-links">
		<li><a href="#home">Home</a></li>
		<li><a href="#about">About</a></li>
		<li><a href="#services">Services</a></li>
		<li><a href="#contact">Contact</a></li>
	</ul>
</nav>
```

```css
.navbar {
	display: flex;
	justify-content: space-between; /* Logo left, links right */
	align-items: center; /* Vertically center */
	background: #2c3e50;
	padding: 1rem 2rem;
}

.logo {
	font-size: 1.5rem;
	font-weight: bold;
	color: white;
}

.nav-links {
	display: flex; /* Make list horizontal */
	list-style: none;
	gap: 2rem; /* Space between links */
	margin: 0;
	padding: 0;
}

.nav-links a {
	color: white;
	text-decoration: none;
}

.nav-links a:hover {
	color: #3498db;
}
```

**Result:** Professional navigation bar with perfect spacing!

### Pattern 2: Centered Hero Section

**Goal:** Center content both horizontally and vertically.

```html
<section class="hero">
	<div class="hero-content">
		<h1>Welcome to Our Website</h1>
		<p>Discover amazing content and services</p>
		<button class="cta-button">Get Started</button>
	</div>
</section>
```

```css
.hero {
	display: flex;
	justify-content: center; /* Horizontal center */
	align-items: center; /* Vertical center */
	min-height: 100vh; /* Full viewport height */
	background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
	color: white;
	text-align: center;
}

.hero-content h1 {
	font-size: 3rem;
	margin-bottom: 1rem;
}

.hero-content p {
	font-size: 1.2rem;
	margin-bottom: 2rem;
}

.cta-button {
	padding: 1rem 2rem;
	font-size: 1rem;
	background: white;
	color: #667eea;
	border: none;
	border-radius: 5px;
	cursor: pointer;
	font-weight: bold;
}
```

**Result:** Perfectly centered hero section!

### Pattern 3: Flexible Card Grid

**Goal:** Equal-width cards that wrap to multiple rows.

```html
<div class="card-container">
	<div class="card">
		<h3>Card 1</h3>
		<p>Card content goes here</p>
	</div>
	<div class="card">
		<h3>Card 2</h3>
		<p>Card content goes here</p>
	</div>
	<div class="card">
		<h3>Card 3</h3>
		<p>Card content goes here</p>
	</div>
	<div class="card">
		<h3>Card 4</h3>
		<p>Card content goes here</p>
	</div>
</div>
```

```css
.card-container {
	display: flex;
	flex-wrap: wrap; /* Allow wrapping */
	gap: 20px; /* Space between cards */
	padding: 20px;
}

.card {
	flex: 1 1 300px; /* Grow, shrink, base 300px */
	/* This means:
       - flex-grow: 1 (can grow)
       - flex-shrink: 1 (can shrink)
       - flex-basis: 300px (minimum width)
    */
	padding: 20px;
	background: white;
	border: 1px solid #ddd;
	border-radius: 8px;
	box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.card h3 {
	color: #2c3e50;
	margin-bottom: 10px;
}
```

**Result:** Responsive card grid that automatically adjusts columns based on screen width!

### Pattern 4: Vertical Sidebar Layout

**Goal:** Sidebar on left, main content on right.

```html
<div class="app-layout">
	<aside class="sidebar">
		<h3>Sidebar</h3>
		<nav>
			<ul>
				<li><a href="#">Dashboard</a></li>
				<li><a href="#">Profile</a></li>
				<li><a href="#">Settings</a></li>
			</ul>
		</nav>
	</aside>

	<main class="main-content">
		<h1>Main Content</h1>
		<p>This is the main content area.</p>
	</main>
</div>
```

```css
.app-layout {
	display: flex; /* Horizontal layout */
	min-height: 100vh;
}

.sidebar {
	flex: 0 0 250px; /* Fixed 250px width */
	background: #2c3e50;
	color: white;
	padding: 20px;
}

.sidebar nav ul {
	list-style: none;
	padding: 0;
}

.sidebar nav a {
	display: block;
	color: white;
	text-decoration: none;
	padding: 10px;
	border-radius: 4px;
}

.sidebar nav a:hover {
	background: #34495e;
}

.main-content {
	flex: 1; /* Take remaining space */
	padding: 20px;
	background: #ecf0f1;
}
```

**Result:** Clean app layout with fixed sidebar and flexible main content!

### Pattern 5: Tag/Badge List

**Goal:** Horizontal list of tags that wraps naturally.

```html
<div class="tag-container">
	<span class="tag">JavaScript</span>
	<span class="tag">CSS</span>
	<span class="tag">HTML</span>
	<span class="tag">React</span>
	<span class="tag">Node.js</span>
	<span class="tag">MongoDB</span>
</div>
```

```css
.tag-container {
	display: flex;
	flex-wrap: wrap; /* Wrap tags to new line if needed */
	gap: 10px; /* Space between tags */
}

.tag {
	padding: 5px 15px;
	background: #3498db;
	color: white;
	border-radius: 20px;
	font-size: 0.9rem;
	white-space: nowrap; /* Don't break tag text */
}
```

**Result:** Tags flow horizontally and wrap naturally!

---

## Part 4: Hands-On Practice (25 minutes)

### Exercise: Build a Responsive Navigation

**Goal:** Create a navigation bar with logo, links, and search box.

**Requirements:**

1. Logo on the far left
2. Navigation links in the center
3. Search box on the far right
4. All items vertically centered
5. Proper spacing and styling

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
		<title>Flexbox Navigation</title>
		<style>
			* {
				margin: 0;
				padding: 0;
				box-sizing: border-box;
			}

			body {
				font-family: Arial, sans-serif;
			}

			/* TODO: Style the navigation */
			.navbar {
				background: #34495e;
				padding: 1rem 2rem;
				/* Add Flexbox properties here */
			}

			.logo {
				font-size: 1.5rem;
				font-weight: bold;
				color: #ecf0f1;
			}

			/* TODO: Make nav-links horizontal */
			.nav-links {
				list-style: none;
				/* Add Flexbox properties here */
			}

			.nav-links a {
				color: #ecf0f1;
				text-decoration: none;
				padding: 0.5rem 1rem;
				border-radius: 4px;
				transition: background 0.3s;
			}

			.nav-links a:hover {
				background: #2c3e50;
			}

			.search-box {
				/* Add styling here */
			}

			.search-box input {
				padding: 0.5rem 1rem;
				border: none;
				border-radius: 4px;
				width: 200px;
			}
		</style>
	</head>
	<body>
		<nav class="navbar">
			<div class="logo">MyLogo</div>

			<ul class="nav-links">
				<li><a href="#home">Home</a></li>
				<li><a href="#about">About</a></li>
				<li><a href="#services">Services</a></li>
				<li><a href="#portfolio">Portfolio</a></li>
				<li><a href="#contact">Contact</a></li>
			</ul>

			<div class="search-box">
				<input
					type="search"
					placeholder="Search..."
				/>
			</div>
		</nav>

		<main style="padding: 2rem;">
			<h1>Welcome to My Website</h1>
			<p>This is a demo page with a Flexbox navigation bar.</p>
		</main>
	</body>
</html>
```

**Tasks:**

1. Make `.navbar` a flex container
2. Distribute items: logo left, links center, search right
3. Make `.nav-links` a flex container for horizontal links
4. Add `gap` for spacing
5. Vertically center all items

<details>
<summary>✅ Solution</summary>

```css
.navbar {
	background: #34495e;
	padding: 1rem 2rem;
	display: flex;
	justify-content: space-between; /* Logo left, search right */
	align-items: center; /* Vertical center */
	gap: 2rem;
}

.logo {
	font-size: 1.5rem;
	font-weight: bold;
	color: #ecf0f1;
}

.nav-links {
	list-style: none;
	display: flex; /* Make horizontal */
	gap: 0.5rem; /* Space between links */
	margin: 0;
}

.nav-links a {
	color: #ecf0f1;
	text-decoration: none;
	padding: 0.5rem 1rem;
	border-radius: 4px;
	transition: background 0.3s;
}

.nav-links a:hover {
	background: #2c3e50;
}

.search-box input {
	padding: 0.5rem 1rem;
	border: none;
	border-radius: 4px;
	width: 200px;
	outline: none;
}

.search-box input:focus {
	box-shadow: 0 0 0 2px #3498db;
}
```

**Enhanced version with better centering:**

```css
/* Alternative: Center nav-links, push search to right */
.navbar {
	display: flex;
	align-items: center;
	background: #34495e;
	padding: 1rem 2rem;
	gap: 2rem;
}

.logo {
	margin-right: auto; /* Push nav-links to center */
}

.nav-links {
	display: flex;
	gap: 0.5rem;
	list-style: none;
	margin: 0 auto; /* Center in remaining space */
}

.search-box {
	margin-left: auto; /* Stay on right */
}
```

</details>

---

## 🐛 Common Mistakes and Troubleshooting

### Mistake 1: Forgetting `display: flex`

**Problem:**

```css
/* ❌ justify-content won't work */
.container {
	justify-content: center; /* No effect without display: flex */
}
```

**Solution:**

```css
/* ✅ Always set display first */
.container {
	display: flex;
	justify-content: center;
}
```

### Mistake 2: Confusing Axes

**Problem:**

```css
/* ❌ Trying to vertically center with justify-content */
.container {
	display: flex;
	flex-direction: row; /* Main axis = horizontal */
	justify-content: center; /* This centers HORIZONTALLY, not vertically */
}
```

**Solution:**

```css
/* ✅ Use align-items for vertical centering in row direction */
.container {
	display: flex;
	flex-direction: row;
	justify-content: center; /* Horizontal center */
	align-items: center; /* Vertical center */
}
```

### Mistake 3: Items Not Wrapping

**Problem:**

```css
/* ❌ Items overflow container */
.container {
	display: flex;
	/* flex-wrap: nowrap is default */
}
```

**Solution:**

```css
/* ✅ Allow wrapping */
.container {
	display: flex;
	flex-wrap: wrap;
}
```

### Mistake 4: Gaps at Edges

**Problem:**

```css
/* ❌ Using margins creates gaps at edges */
.item {
	margin: 10px; /* Creates unwanted space at container edges */
}
```

**Solution:**

```css
/* ✅ Use gap property instead */
.container {
	display: flex;
	gap: 20px; /* Perfect spacing, no edge gaps */
}

.item {
	/* No margin needed */
}
```

### Mistake 5: Height Not Working for Vertical Centering

**Problem:**

```css
/* ❌ Container has no height */
.container {
	display: flex;
	align-items: center; /* Won't center if container has no height */
}
```

**Solution:**

```css
/* ✅ Give container explicit height */
.container {
	display: flex;
	align-items: center;
	min-height: 400px; /* Or 100vh, or any fixed height */
}
```

---

## 🏡 Homework Assignment

**Build a Flexbox Landing Page**

Create a landing page that demonstrates all Flexbox concepts learned.

**Requirements:**

1. **Header Navigation**

    - Logo on left
    - Navigation links centered or right
    - Sticky/fixed positioning (bonus)

2. **Hero Section**

    - Centered content (both axes)
    - Full viewport height
    - Heading, subheading, and CTA button

3. **Features Section**

    - 3 feature cards in a row
    - Equal width with gap spacing
    - Icons or images (can use emojis)

4. **Testimonials Section**

    - 2 testimonials side-by-side
    - Flexible layout that wraps on small screens

5. **Footer**
    - Three columns: About, Links, Contact
    - Centered copyright text below

**Technical requirements:**

-   Use `display: flex` for all layouts
-   Use `gap` for spacing (no margin hacks)
-   Use `justify-content` and `align-items` appropriately
-   Implement at least one `flex-wrap` section
-   No floats or positioning for layout (only for decoration if needed)

**Bonus challenges:**

-   Add smooth hover effects
-   Make navigation responsive (mobile menu concept)
-   Use `flex-direction: column` for mobile layout
-   Add subtle animations with transitions

**Deliverables:**

-   `flexbox-landing.html` — Complete HTML structure
-   Inline or external CSS with Flexbox layouts
-   Comments explaining Flexbox usage
-   Clean, semantic HTML

**Submission:** Create a folder `session-13-homework` with your files.

---

## 📚 Additional Resources

### Documentation

-   [MDN: Flexbox](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox)
-   [MDN: Flex Container](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_flexible_box_layout/Basic_concepts_of_flexbox)
-   [CSS Tricks: A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

### Interactive Learning

-   [Flexbox Froggy](https://flexboxfroggy.com/) — Game to learn Flexbox
-   [Flexbox Defense](http://www.flexboxdefense.com/) — Tower defense game
-   [Flexbox Zombies](https://mastery.games/flexboxzombies/) — Story-based learning

### Visual Tools

-   [Flexbox Playground](https://codepen.io/enxaneta/pen/adLPwv)
-   [Flexbox Cheatsheet](https://yoksel.github.io/flex-cheatsheet/)

### Video Tutorials

-   [Flexbox CSS In 20 Minutes](https://www.youtube.com/watch?v=JJSoEo8JSnc)
-   [Flexbox Tutorial by Wes Bos](https://flexbox.io/)

---

## 🎉 Session Summary

Congratulations! You've learned the fundamentals of Flexbox. You can now:

✅ Understand the Flexbox layout model and when to use it
✅ Create flex containers with `display: flex`
✅ Control layout direction with `flex-direction`
✅ Align items along the main axis with `justify-content`
✅ Align items along the cross axis with `align-items`
✅ Create wrapping layouts with `flex-wrap`
✅ Add spacing with the `gap` property
✅ Build common UI patterns (navigation, cards, centering)
✅ Understand advantages over float-based layouts

**Key takeaway:** Flexbox makes layout tasks that were complex with floats incredibly simple and intuitive!

**Next session:** We'll dive deeper into **Flex Item Properties** (`flex-grow`, `flex-shrink`, `flex-basis`) and learn advanced Flexbox patterns!

---

**Navigation:**
← [Week 04 Session 12](../week-04/session-12.md) | [Week 05 Index](../week-05.md) | [Session 14](session-14.md) →
