# Week 04 — Session 12: Multi-Column Layouts

**Navigation:**
← [Week 04 Session 11](session-11.md) | [Week 04 Index](../week-04.md) | [Week 05 Session 13](../week-05/session-13.md) →

---

**Session Length:** 90 minutes

## 📋 Pre-Class Checklist

Before starting this session, make sure you have:

-   ✅ Completed Session 11 (Positioning and Layering)
-   ✅ Understand the CSS box model, spacing, and positioning
-   ✅ Familiar with `float`, `clear`, and basic layout concepts
-   ✅ Code editor (VS Code) with Live Server extension
-   ✅ Browser with Developer Tools (Chrome, Firefox, or Edge)
-   ✅ Create a new folder: `week-04-multicolumn`

## 🎯 Learning Objectives

By the end of this session, you will be able to:

-   Create multi-column layouts using CSS floats
-   Understand and apply clearing techniques
-   Use the `clearfix` hack for float containment
-   Build traditional multi-column page layouts (2-column, 3-column)
-   Understand the limitations of float-based layouts
-   Explore modern alternatives (CSS Grid, Flexbox preview)
-   Create newspaper-style columns with CSS Multi-Column Layout
-   Build responsive column layouts

## 📦 Files for This Session

-   `session-12.md` — This tutorial (you're reading it!)
-   `multicolumn-template.html` — Starter file for practice
-   `multicolumn-solution.html` — Complete working example
-   `float-cheat-sheet.md` — Quick reference guide
-   `multicolumn-visual.html` — Interactive layout demo

## 🔑 Key Terms

**float**, **clear**, **clearfix**, **float containment**, **float collapse**, **multi-column layout**, **sidebar**, **main content**, **CSS columns**, `column-count`, `column-gap`, `column-rule`, **layout patterns**, **holy grail layout**, **newspaper columns**

## 🏗️ What You Will Build

-   A 2-column blog layout (sidebar + main content)
-   A 3-column card grid
-   A newspaper-style multi-column article
-   A responsive layout that adapts to screen sizes
-   A classic "Holy Grail" layout

---

## Part 1: Understanding Float Basics (15 minutes)

### What is Float?

**Float** was originally designed for wrapping text around images (magazine-style layouts), but became the primary tool for multi-column layouts before Flexbox and Grid.

**How float works:**

-   Removes element from normal document flow
-   Pushes element to the left or right of its container
-   Allows content to flow around the floated element
-   Affects following elements, not preceding ones

### Float Values

```css
.element {
	float: none; /* Default - element in normal flow */
	float: left; /* Float to the left */
	float: right; /* Float to the right */
	float: inherit; /* Inherit from parent */
}
```

### Basic Float Example

**Text wrapping around an image:**

```html
<article>
	<img
		src="photo.jpg"
		alt="Article photo"
		class="article-image"
	/>
	<p>
		Lorem ipsum dolor sit amet, consectetur adipiscing elit. The image
		floats to the left, and this text wraps around it naturally.
	</p>
	<p>
		This paragraph also wraps around the floated image, creating a classic
		magazine-style layout.
	</p>
</article>
```

```css
.article-image {
	float: left;
	width: 300px;
	margin: 0 20px 20px 0; /* Right and bottom margins create space */
	border-radius: 8px;
}

article {
	max-width: 800px;
	line-height: 1.6;
}
```

**Result:** Image floats left, text flows around the right side.

**Visual representation:**

```
Before float (normal flow):
┌─────────────────────────────┐
│ ┌───────────────────────┐   │
│ │       Image           │   │
│ └───────────────────────┘   │
│                             │
│ Text starts here and        │
│ continues below the image.  │
└─────────────────────────────┘

After float: left:
┌─────────────────────────────┐
│ ┌─────────┐ Text wraps      │
│ │ Image   │ around the      │
│ │ (float) │ floated image   │
│ └─────────┘ and continues   │
│             on multiple     │
│             lines naturally.│
└─────────────────────────────┘
```

### Float for Column Layouts

**Creating two columns:**

```html
<div class="container">
	<div class="column left">Left Column</div>
	<div class="column right">Right Column</div>
</div>
```

```css
.container {
	width: 100%;
	max-width: 1200px;
	margin: 0 auto;
}

.column {
	width: 48%;
	padding: 20px;
	background: lightblue;
	box-sizing: border-box;
}

.left {
	float: left;
}

.right {
	float: right;
}
```

**Important notes:**

-   Total width should be less than 100% to account for rounding/gaps
-   Use `box-sizing: border-box` for predictable sizing
-   Floated elements are removed from normal flow

<details>
<summary>💡 Knowledge Check #1</summary>

**Question:** What happens to the height of a parent container when all its child elements are floated?

**Answer:**

The parent container **collapses to zero height** (or height of any non-floated content). This is called **"float collapse"**.

**Why it happens:**

-   Floated elements are removed from normal document flow
-   Parent doesn't "see" floated children when calculating height
-   Can break layouts if not handled properly

**Visual example:**

```html
<div class="parent">
	<div class="child float-left">Floated</div>
</div>
<div class="next">Next element</div>
```

```css
.parent {
	background: lightgray;
	/* Height collapses! */
}

.child {
	float: left;
	width: 200px;
	height: 100px;
	background: coral;
}
```

**Result:** Parent has 0 height, and `.next` element slides up behind floated child.

**Solution:** Use clearing techniques (covered in Part 2).

</details>

### Real-World Use Cases for Floats

**1. Article Images (Original Purpose)**

```css
/* Magazine-style article layout */
.article-content img.pull-left {
	float: left;
	max-width: 40%;
	margin: 0 20px 15px 0;
}

.article-content img.pull-right {
	float: right;
	max-width: 40%;
	margin: 0 0 15px 20px;
}
```

**Use when:** Adding images to blog posts, articles, or editorial content.

**2. Navigation Menus**

```css
/* Horizontal navigation with logo */
.header-nav .logo {
	float: left;
}

.header-nav .menu {
	float: right;
}

.header-nav::after {
	content: '';
	display: table;
	clear: both;
}
```

**Use when:** Creating horizontal layouts where items need to be on opposite sides.

**3. Legacy Browser Support**

```css
/* Fallback for older browsers that don't support Flexbox */
.column {
	float: left;
	width: 50%;
}

/* Modern browsers override with Flexbox */
@supports (display: flex) {
	.container {
		display: flex;
	}
	.column {
		float: none;
		flex: 1;
	}
}
```

**Use when:** Supporting IE9 or maintaining legacy projects.

### Browser DevTools Tips for Debugging Floats

**Tip 1: Visualize the float**

1. Open DevTools (F12)
2. Select the floated element
3. Look for the computed dimensions
4. Check if parent has height: 0

**Tip 2: Check for clearfix**

```javascript
// Run in console to check if clearfix is applied
getComputedStyle(
	document.querySelector('.container'),
	'::after'
).getPropertyValue('clear');
// Should return 'both' if clearfix is present
```

**Tip 3: Highlight layout issues**

```css
/* Temporary debugging CSS */
.container {
	outline: 2px solid red; /* Shows container boundary */
}

.floated {
	outline: 2px solid blue; /* Shows floated element */
}
```

---

## Part 2: Clearing Floats (20 minutes)

### The Problem: Float Collapse

When all children are floated, the parent container collapses:

```html
<div class="container">
	<div class="box float-left">Box 1</div>
	<div class="box float-left">Box 2</div>
	<div class="box float-left">Box 3</div>
</div>
<footer>Footer appears too high!</footer>
```

```css
.container {
	background: lightgray;
	/* Height = 0! */
}

.box {
	float: left;
	width: 200px;
	height: 150px;
	margin: 10px;
	background: coral;
}
```

**Problem:** Footer slides up and overlaps the floated boxes.

### Solution 1: The `clear` Property

**Clear** forces an element to move below floated elements.

```css
.element {
	clear: none; /* Default - allows floating elements */
	clear: left; /* Clear left-floated elements */
	clear: right; /* Clear right-floated elements */
	clear: both; /* Clear both left and right floats */
}
```

**Using clear on the next element:**

```html
<div class="container">
	<div class="box float-left">Box 1</div>
	<div class="box float-left">Box 2</div>
	<div class="box float-left">Box 3</div>
</div>
<footer class="clear-floats">Footer now appears below boxes</footer>
```

```css
.clear-floats {
	clear: both; /* Moves below all floated elements */
}
```

**Limitation:** This only fixes the element that follows, not the collapsed parent.

### Solution 2: Empty Clearing Div (Old Method)

**Adding an empty div inside the container:**

```html
<div class="container">
	<div class="box float-left">Box 1</div>
	<div class="box float-left">Box 2</div>
	<div class="box float-left">Box 3</div>
	<div class="clear"></div>
	<!-- Empty clearing div -->
</div>
```

```css
.clear {
	clear: both;
}
```

**Problems:**

-   ❌ Adds non-semantic HTML
-   ❌ Clutters markup
-   ❌ Not maintainable
-   ❌ Not recommended anymore

### Solution 3: The Clearfix Hack (Best Practice)

**The modern clearfix** uses a pseudo-element to clear floats without extra HTML:

```css
/* Modern clearfix */
.clearfix::after {
	content: '';
	display: table;
	clear: both;
}

/* Alternative version */
.clearfix::after {
	content: '';
	display: block;
	clear: both;
}
```

**Usage:**

```html
<div class="container clearfix">
	<div class="box float-left">Box 1</div>
	<div class="box float-left">Box 2</div>
	<div class="box float-left">Box 3</div>
</div>
```

**How it works:**

1. `::after` creates a pseudo-element after the content
2. `content: ""` makes it exist (even if empty)
3. `display: table` or `display: block` makes it a block-level element
4. `clear: both` forces it below floated elements
5. Parent now contains the pseudo-element, so height is restored

### Solution 4: `overflow` Property

**Using overflow to contain floats:**

```css
.container {
	overflow: auto; /* or overflow: hidden; */
}
```

**How it works:**

-   Creates a **Block Formatting Context (BFC)**
-   BFC contains floated children
-   Parent height expands to contain floats

**Example:**

```html
<div class="container">
	<div class="box float-left">Box 1</div>
	<div class="box float-left">Box 2</div>
</div>
```

```css
.container {
	overflow: auto; /* Contains floats */
	background: lightgray;
	padding: 10px;
}

.box {
	float: left;
	width: 200px;
	height: 150px;
	margin: 10px;
	background: coral;
}
```

**Pros:**

-   ✅ Simple one-line solution
-   ✅ No extra markup or pseudo-elements

**Cons:**

-   ❌ May cause scrollbars with `overflow: auto`
-   ❌ May hide content with `overflow: hidden`
-   ❌ Side effects in certain scenarios

### Comparison of Clearing Methods

| Method                  | Pros                   | Cons                        | Use When                              |
| ----------------------- | ---------------------- | --------------------------- | ------------------------------------- |
| `clear` on next element | Simple                 | Doesn't fix parent collapse | Quick fix for following elements      |
| Empty div               | Works everywhere       | Non-semantic, adds markup   | Never (outdated)                      |
| Clearfix hack           | Clean, no side effects | Requires extra class        | Best practice for float layouts       |
| `overflow`              | Simple, one line       | Potential side effects      | Simple containers, no overflow needed |

**Recommended:** Use **clearfix** for float-based layouts.

### Troubleshooting Flowchart

```
Float Layout Issue?
        │
        ▼
Is parent collapsed?
   ├─ YES ─▶ Add clearfix to parent
   │         OR use overflow: auto
   │
   └─ NO ──▶ Is footer overlapping?
              ├─ YES ─▶ Add clear: both to footer
              │
              └─ NO ──▶ Are widths exceeding 100%?
                         ├─ YES ─▶ Use box-sizing: border-box
                         │         AND reduce total width
                         │
                         └─ NO ──▶ Check DevTools for
                                   computed dimensions
```

### Performance Considerations

**Floats vs Modern Alternatives:**

| Aspect                   | Floats                     | Flexbox           | CSS Grid                 |
| ------------------------ | -------------------------- | ----------------- | ------------------------ |
| **Render Performance**   | ⚡ Fast                    | ⚡ Fast           | ⚡ Fast                  |
| **Layout Recalculation** | ⚠️ Can trigger reflows     | ✅ Optimized      | ✅ Optimized             |
| **Browser Support**      | ✅ Universal (IE6+)        | ✅ Modern (IE11+) | ⚠️ Modern (IE11 partial) |
| **Code Complexity**      | ⚠️ Requires clearfix hacks | ✅ Simple         | ✅ Simple                |
| **Maintenance**          | ❌ Difficult               | ✅ Easy           | ✅ Easy                  |

**When floats might still be preferable:**

-   Supporting very old browsers (IE8, IE9)
-   Text wrapping around images (original use case)
-   Very simple left/right layouts
-   Legacy codebases

**Recommendation:** Use Flexbox or Grid for new projects.

<details>
<summary>💡 Knowledge Check #2</summary>

**Question:** What does the `::after` pseudo-element in the clearfix hack do?

**Answer:**

The `::after` pseudo-element:

1. **Creates a virtual element** after the container's content
2. **Acts as the last child** of the container
3. **Clears the floats** with `clear: both`
4. **Forces the parent to expand** to contain the floated children

**Step-by-step visualization:**

```html
<!-- HTML -->
<div class="container clearfix">
	<div class="box float-left">Box 1</div>
	<div class="box float-left">Box 2</div>
</div>
```

**Browser renders as if it were:**

```html
<div class="container clearfix">
	<div class="box float-left">Box 1</div>
	<div class="box float-left">Box 2</div>
	<!-- Invisible pseudo-element here -->
	<div style="clear: both; display: block; content: '';"></div>
</div>
```

**Result:** Parent height expands to contain both the floated boxes and the clearing pseudo-element.

</details>

---

## Part 3: Multi-Column Layout Patterns (25 minutes)

### Pattern 1: Two-Column Layout (Sidebar + Main)

**Classic blog/article layout:**

```html
<div class="page-container clearfix">
	<aside class="sidebar">
		<h3>Sidebar</h3>
		<ul>
			<li><a href="#">Category 1</a></li>
			<li><a href="#">Category 2</a></li>
			<li><a href="#">Category 3</a></li>
		</ul>
	</aside>

	<main class="main-content">
		<h1>Main Content</h1>
		<p>
			This is the main content area where articles, blog posts, or primary
			information is displayed.
		</p>
	</main>
</div>
```

```css
.page-container {
	max-width: 1200px;
	margin: 0 auto;
	padding: 20px;
}

.sidebar {
	float: left;
	width: 25%;
	padding: 20px;
	background: #f5f5f5;
	box-sizing: border-box;
}

.main-content {
	float: right;
	width: 72%;
	padding: 20px;
	background: white;
	box-sizing: border-box;
}

/* Clearfix */
.clearfix::after {
	content: '';
	display: table;
	clear: both;
}
```

**Key points:**

-   Sidebar: 25% width
-   Main content: 72% width
-   3% gap between columns (100% - 25% - 72% = 3%)
-   Use `box-sizing: border-box` for easier width calculations

### Pattern 2: Three-Column Layout

**Dashboard or complex layout:**

```html
<div class="three-column-container clearfix">
	<div class="column left-sidebar">
		<h3>Left Sidebar</h3>
		<p>Navigation or filters</p>
	</div>

	<div class="column main">
		<h2>Main Content</h2>
		<p>Primary content area</p>
	</div>

	<div class="column right-sidebar">
		<h3>Right Sidebar</h3>
		<p>Ads or related content</p>
	</div>
</div>
```

```css
.three-column-container {
	max-width: 1200px;
	margin: 0 auto;
}

.column {
	float: left;
	padding: 20px;
	box-sizing: border-box;
	min-height: 400px;
}

.left-sidebar {
	width: 20%;
	background: #e8f4f8;
}

.main {
	width: 55%;
	background: white;
	margin: 0 2.5%; /* Creates gaps on both sides */
}

.right-sidebar {
	width: 20%;
	background: #fff3e0;
}

.clearfix::after {
	content: '';
	display: table;
	clear: both;
}
```

**Width calculation:**

-   Left: 20%
-   Main: 55% + 5% margins = 60%
-   Right: 20%
-   Total: 20% + 60% + 20% = 100%

### Pattern 3: Holy Grail Layout

**Classic 5-section layout (header, footer, 3 columns):**

```html
<div class="holy-grail">
	<header class="header">Header</header>

	<div class="container clearfix">
		<nav class="left-nav">
			<h3>Navigation</h3>
			<ul>
				<li><a href="#">Link 1</a></li>
				<li><a href="#">Link 2</a></li>
			</ul>
		</nav>

		<main class="content">
			<h1>Main Content</h1>
			<p>The primary content area that takes up the most space.</p>
		</main>

		<aside class="right-ads">
			<h3>Advertisements</h3>
			<div class="ad-box">Ad 1</div>
			<div class="ad-box">Ad 2</div>
		</aside>
	</div>

	<footer class="footer">Footer</footer>
</div>
```

```css
.holy-grail {
	max-width: 1200px;
	margin: 0 auto;
}

.header,
.footer {
	background: #2c3e50;
	color: white;
	padding: 20px;
	text-align: center;
}

.container {
	padding: 20px 0;
}

.left-nav {
	float: left;
	width: 20%;
	padding: 20px;
	background: #ecf0f1;
	box-sizing: border-box;
}

.content {
	float: left;
	width: 55%;
	padding: 20px;
	margin: 0 2.5%;
	background: white;
	box-sizing: border-box;
}

.right-ads {
	float: right;
	width: 20%;
	padding: 20px;
	background: #fef5e7;
	box-sizing: border-box;
}

.clearfix::after {
	content: '';
	display: table;
	clear: both;
}
```

### Pattern 4: Card Grid Layout

**Equal-width cards using float:**

```html
<div class="card-grid clearfix">
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
.card-grid {
	max-width: 1200px;
	margin: 0 auto;
	padding: 20px;
}

.card {
	float: left;
	width: 23%; /* 4 cards per row */
	margin: 1%; /* Gap between cards */
	padding: 20px;
	background: white;
	border: 1px solid #ddd;
	border-radius: 8px;
	box-sizing: border-box;
}

/* For 3 cards per row */
.card-three {
	width: 31.33%;
	margin: 1%;
}

.clearfix::after {
	content: '';
	display: table;
	clear: both;
}
```

**Width calculation for 4 columns:**

-   Card width: 23%
-   Margin: 1% × 2 sides = 2%
-   Total per card: 23% + 2% = 25%
-   4 cards: 25% × 4 = 100%

### Advanced Float Techniques

**Technique 1: Negative Margins for Gutterless Grids**

```css
/* Container with negative margin */
.row {
	margin-left: -10px;
	margin-right: -10px;
}

.row::after {
	content: '';
	display: table;
	clear: both;
}

/* Columns with positive padding */
.col {
	float: left;
	width: 33.333%;
	padding-left: 10px;
	padding-right: 10px;
	box-sizing: border-box;
}
```

**Why this works:**

-   Negative margins pull the row outward
-   Column padding creates the gutter
-   First and last columns align with container edges

**Technique 2: Centering Floated Elements**

```css
/* Float wrapper that centers itself */
.centered-float {
	float: left;
	position: relative;
	left: 50%;
}

.centered-float-inner {
	float: left;
	position: relative;
	left: -50%;
}
```

```html
<div class="centered-float">
	<div class="centered-float-inner">
		<nav>
			<a href="#">Link 1</a>
			<a href="#">Link 2</a>
			<a href="#">Link 3</a>
		</nav>
	</div>
</div>
```

**Technique 3: Equal Height Columns with Faux Columns**

```css
/* Parent with background image */
.columns-wrapper {
	background: url('column-bg.png') repeat-y;
	background-size: 50% 100%; /* Two columns */
}

.column {
	float: left;
	width: 50%;
	padding-bottom: 9999px; /* Fake height */
	margin-bottom: -9999px; /* Negative margin */
}

.columns-wrapper {
	overflow: hidden; /* Clip the padding */
}
```

**Note:** This is a hack. Use Flexbox (`display: flex`) for real equal-height columns.

### Responsive Float Layouts

**Mobile-First Approach:**

```css
/* Mobile: Stacked (no floats) */
.column {
	width: 100%;
	margin-bottom: 20px;
	padding: 15px;
}

/* Tablet: 2 columns */
@media (min-width: 768px) {
	.column {
		float: left;
		width: 48%;
		margin-right: 4%;
	}

	.column:nth-child(2n) {
		margin-right: 0; /* Remove margin from every 2nd item */
	}
}

/* Desktop: 4 columns */
@media (min-width: 1024px) {
	.column {
		width: 23%;
		margin-right: 2.666%;
	}

	.column:nth-child(2n) {
		margin-right: 2.666%; /* Restore margin */
	}

	.column:nth-child(4n) {
		margin-right: 0; /* Remove margin from every 4th item */
	}
}
```

**Desktop-First Approach:**

```css
/* Desktop: 4 columns (default) */
.column {
	float: left;
	width: 23%;
	margin-right: 2.666%;
	box-sizing: border-box;
}

.column:nth-child(4n) {
	margin-right: 0;
}

/* Tablet: 2 columns */
@media (max-width: 1023px) {
	.column {
		width: 48%;
		margin-right: 4%;
	}

	.column:nth-child(4n) {
		margin-right: 4%; /* Reset */
	}

	.column:nth-child(2n) {
		margin-right: 0;
	}
}

/* Mobile: Stacked */
@media (max-width: 767px) {
	.column {
		float: none;
		width: 100%;
		margin-right: 0;
		margin-bottom: 20px;
	}
}
```

<details>
<summary>💡 Knowledge Check #3</summary>

**Question:** Why is it important to use `box-sizing: border-box` in float-based layouts?

**Answer:**

**Without `box-sizing: border-box` (default `content-box`):**

```css
.column {
	width: 50%;
	padding: 20px;
	border: 2px solid black;
	/* Total width = 50% + 40px padding + 4px border */
	/* This breaks the layout! */
}
```

**Calculation:**

-   Specified width: 50%
-   Padding: 20px × 2 = 40px
-   Border: 2px × 2 = 4px
-   **Total width: 50% + 44px** (exceeds container!)

**With `box-sizing: border-box`:**

```css
.column {
	box-sizing: border-box;
	width: 50%;
	padding: 20px;
	border: 2px solid black;
	/* Total width = 50% (padding and border INCLUDED) */
	/* Layout works perfectly! */
}
```

**Calculation:**

-   Total width: 50% (as specified)
-   Content width: 50% - 40px - 4px
-   Everything stays within the specified width

**Benefits:**

-   ✅ Predictable sizing
-   ✅ Easier percentage calculations
-   ✅ Padding/borders don't break layout
-   ✅ Industry standard practice

**Best practice:**

```css
/* Apply to all elements */
*,
*::before,
*::after {
	box-sizing: border-box;
}
```

</details>

---

## Part 4: CSS Multi-Column Layout (15 minutes)

### Introduction to CSS Columns

**CSS Multi-Column Layout** allows content to flow into multiple columns, like a newspaper.

**Key difference from floats:**

-   Floats: Create structural columns (sidebars, layout sections)
-   CSS Columns: Create text flow columns (newspaper, magazine articles)

### Basic Column Properties

```css
.article {
	column-count: 3; /* Number of columns */
	column-gap: 30px; /* Space between columns */
	column-rule: 1px solid #ccc; /* Line between columns */
}
```

### Column Count

**Setting the number of columns:**

```css
/* Exactly 2 columns */
.two-columns {
	column-count: 2;
}

/* Exactly 3 columns */
.three-columns {
	column-count: 3;
}
```

**Example:**

```html
<article class="newspaper">
	<h2>Article Title</h2>
	<p>
		Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod
		tempor incididunt ut labore et dolore magna aliqua. Content flows
		naturally across columns...
	</p>
	<p>
		More content continues here and automatically flows into the next
		column...
	</p>
</article>
```

```css
.newspaper {
	column-count: 3;
	column-gap: 40px;
	max-width: 1200px;
	margin: 0 auto;
	padding: 20px;
	line-height: 1.6;
}
```

### Column Width

**Setting optimal column width (browser determines count):**

```css
.responsive-columns {
	column-width: 250px; /* Ideal width per column */
	column-gap: 30px;
}
```

**How it works:**

-   Browser creates as many columns as fit
-   Each column is at least 250px wide
-   Responsive without media queries!

**Example:**

-   1200px container: ~4 columns (250px each + gaps)
-   600px container: ~2 columns
-   300px container: 1 column

### Column Gap and Rule

**Styling the space between columns:**

```css
.styled-columns {
	column-count: 3;
	column-gap: 50px; /* Gap between columns */
	column-rule: 2px solid #3498db; /* Vertical line between */
	column-rule-style: dashed; /* Can be: solid, dashed, dotted, etc. */
	column-rule-width: 3px;
	column-rule-color: crimson;
}

/* Shorthand */
.styled-columns {
	column-rule: 3px dashed crimson;
}
```

### Spanning Columns

**Making an element span across all columns:**

```css
.article h2 {
	column-span: all; /* Span across all columns */
	background: #f5f5f5;
	padding: 20px;
	margin-bottom: 20px;
}

.article img {
	column-span: all; /* Image spans full width */
	width: 100%;
	margin: 20px 0;
}
```

**Example:**

```html
<article class="magazine">
	<h2>Breaking News: Major Discovery</h2>
	<p>This paragraph flows in columns...</p>
	<img
		src="photo.jpg"
		alt="News photo"
		class="full-width"
	/>
	<p>More text continues in columns after the image...</p>
</article>
```

```css
.magazine {
	column-count: 2;
	column-gap: 40px;
}

.magazine h2,
.magazine .full-width {
	column-span: all;
}
```

### Controlling Column Breaks

**Preventing awkward breaks:**

```css
/* Prevent breaks inside an element */
.keep-together {
	break-inside: avoid; /* Don't break this element across columns */
	page-break-inside: avoid; /* Older browsers */
}

/* Force break before element */
.new-column {
	break-before: column;
}

/* Force break after element */
.break-after {
	break-after: column;
}
```

**Example:**

```css
.article h3 {
	break-after: avoid; /* Keep heading with next paragraph */
	break-inside: avoid;
}

.article figure {
	break-inside: avoid; /* Keep image and caption together */
	margin: 20px 0;
}
```

### Complete Multi-Column Example

```html
<article class="feature-article">
	<h1>The Art of Web Design</h1>

	<div class="intro">
		<p class="lead">
			A comprehensive guide to modern web design principles and practices.
		</p>
	</div>

	<div class="article-body">
		<h2>Introduction</h2>
		<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit...</p>

		<figure class="image-break">
			<img
				src="design.jpg"
				alt="Web design example"
			/>
			<figcaption>Figure 1: Modern web design layout</figcaption>
		</figure>

		<h2>Core Principles</h2>
		<p>More content continues here...</p>
		<p>Additional paragraphs flow naturally across columns...</p>
	</div>
</article>
```

```css
.feature-article {
	max-width: 1200px;
	margin: 0 auto;
	padding: 40px;
}

.feature-article h1 {
	font-size: 2.5rem;
	margin-bottom: 20px;
	color: #2c3e50;
	text-align: center;
}

.intro {
	margin-bottom: 30px;
	padding: 20px;
	background: #f8f9fa;
	border-left: 4px solid #3498db;
}

.intro .lead {
	font-size: 1.2rem;
	line-height: 1.6;
}

.article-body {
	column-count: 2;
	column-gap: 60px;
	column-rule: 1px solid #ddd;
	text-align: justify;
	line-height: 1.8;
}

.article-body h2 {
	column-span: all;
	margin-top: 40px;
	margin-bottom: 20px;
	padding-bottom: 10px;
	border-bottom: 2px solid #3498db;
	color: #2c3e50;
}

.article-body figure {
	column-span: all;
	break-inside: avoid;
	margin: 30px 0;
	text-align: center;
}

.article-body figure img {
	max-width: 100%;
	border-radius: 8px;
}

.article-body figcaption {
	margin-top: 10px;
	font-style: italic;
	color: #666;
}
```

<details>
<summary>💡 Knowledge Check #4</summary>

**Question:** What's the difference between `column-count` and `column-width`?

**Answer:**

**`column-count`:**

-   **Fixed number** of columns
-   Browser adjusts column width to fit
-   Columns may become very narrow on small screens
-   Use when you want exact column count

**Example:**

```css
.fixed-columns {
	column-count: 3; /* Always 3 columns, no matter the width */
}
```

**Result:**

-   1200px wide: 3 × 400px columns
-   600px wide: 3 × 200px columns (very narrow!)
-   300px wide: 3 × 100px columns (unreadable!)

**`column-width`:**

-   **Ideal minimum** width per column
-   Browser determines how many columns fit
-   Automatically responsive
-   Use for flexible, readable layouts

**Example:**

```css
.flexible-columns {
	column-width: 250px; /* Minimum ~250px per column */
}
```

**Result:**

-   1200px wide: ~4 columns (4 × 250px + gaps)
-   600px wide: ~2 columns
-   300px wide: 1 column (maintains readability!)

**Best practice:**

```css
/* Responsive columns without media queries */
.article {
	column-width: 300px; /* Ideal minimum */
	column-gap: 40px;
}

/* Or combine both for more control */
.article-combined {
	column-width: 250px; /* Minimum width */
	column-count: 3; /* Maximum columns */
}
```

</details>

---

## Part 5: Hands-On Practice (15 minutes)

### Exercise: Blog Layout with Sidebar

**Goal:** Create a classic blog layout with floating sidebar and main content area.

**Requirements:**

1. Header across full width
2. Left sidebar (25% width) with navigation
3. Main content area (70% width) with article
4. Footer across full width
5. Proper clearing to prevent collapse
6. Responsive spacing and padding

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
		<title>Blog Layout</title>
		<style>
			* {
				margin: 0;
				padding: 0;
				box-sizing: border-box;
			}

			body {
				font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
				line-height: 1.6;
				background: #f5f5f5;
			}

			/* TODO: Style the container */
			.container {
				max-width: 1200px;
				margin: 0 auto;
				background: white;
			}

			/* TODO: Style the header */
			.header {
				background: #2c3e50;
				color: white;
				padding: 20px;
				text-align: center;
			}

			/* TODO: Create the layout wrapper with clearfix */
			.layout {
				/* Add clearfix here */
			}

			/* TODO: Style the sidebar (25% width, float left) */
			.sidebar {
				/* Add float and width */
				background: #ecf0f1;
				padding: 20px;
			}

			/* TODO: Style the main content (70% width, float right) */
			.main-content {
				/* Add float and width */
				padding: 20px;
			}

			/* TODO: Style the footer */
			.footer {
				background: #34495e;
				color: white;
				padding: 20px;
				text-align: center;
			}

			/* Clearfix */
			.clearfix::after {
				content: '';
				display: table;
				clear: both;
			}

			/* Additional styling */
			.sidebar nav ul {
				list-style: none;
			}

			.sidebar nav a {
				display: block;
				padding: 10px;
				color: #2c3e50;
				text-decoration: none;
				border-bottom: 1px solid #ddd;
			}

			.sidebar nav a:hover {
				background: #d5dbdd;
			}

			.article h2 {
				color: #2c3e50;
				margin-bottom: 15px;
			}

			.article p {
				margin-bottom: 15px;
			}
		</style>
	</head>
	<body>
		<div class="container">
			<header class="header">
				<h1>My Awesome Blog</h1>
				<p>Web Development Tutorials and Tips</p>
			</header>

			<div class="layout">
				<aside class="sidebar">
					<h3>Categories</h3>
					<nav>
						<ul>
							<li><a href="#">HTML & CSS</a></li>
							<li><a href="#">JavaScript</a></li>
							<li><a href="#">Web Design</a></li>
							<li><a href="#">Tutorials</a></li>
							<li><a href="#">Resources</a></li>
						</ul>
					</nav>
				</aside>

				<main class="main-content">
					<article class="article">
						<h2>Understanding CSS Float Layouts</h2>
						<p class="meta">
							Published on December 4, 2025 | By Jane Doe
						</p>

						<p>
							Lorem ipsum dolor sit amet, consectetur adipiscing
							elit. Float-based layouts have been a cornerstone of
							web design for many years, allowing developers to
							create multi-column layouts before Flexbox and Grid
							were available.
						</p>

						<p>
							While modern layout techniques like Flexbox and CSS
							Grid are now preferred, understanding floats is
							still important for maintaining legacy code and
							understanding CSS fundamentals.
						</p>

						<p>
							In this article, we'll explore how floats work,
							common patterns, and best practices for clearing
							floats to prevent layout issues.
						</p>

						<h3>Key Concepts</h3>
						<p>
							Floats remove elements from the normal document flow
							and allow text and inline elements to wrap around
							them. This behavior was originally designed for
							magazine-style layouts but became the primary tool
							for creating column-based layouts.
						</p>
					</article>
				</main>
			</div>

			<footer class="footer">
				<p>&copy; 2025 My Awesome Blog. All rights reserved.</p>
			</footer>
		</div>
	</body>
</html>
```

**Tasks:**

1. Add clearfix class to `.layout`
2. Float `.sidebar` to the left with 25% width
3. Float `.main-content` to the right with 70% width
4. Ensure proper spacing and box-sizing
5. Test that footer appears below both columns

<details>
<summary>✅ Solution</summary>

```css
.container {
	max-width: 1200px;
	margin: 0 auto;
	background: white;
	box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.header {
	background: #2c3e50;
	color: white;
	padding: 30px 20px;
	text-align: center;
}

.header h1 {
	margin-bottom: 5px;
}

.layout {
	min-height: 500px;
}

.layout::after {
	content: '';
	display: table;
	clear: both;
}

.sidebar {
	float: left;
	width: 25%;
	background: #ecf0f1;
	padding: 20px;
	box-sizing: border-box;
}

.main-content {
	float: right;
	width: 72%;
	padding: 30px;
	box-sizing: border-box;
}

.footer {
	background: #34495e;
	color: white;
	padding: 20px;
	text-align: center;
	clear: both; /* Extra safety */
}

/* Additional enhancements */
.meta {
	color: #7f8c8d;
	font-size: 0.9rem;
	margin-bottom: 20px;
	padding-bottom: 10px;
	border-bottom: 1px solid #eee;
}

.article h3 {
	color: #34495e;
	margin-top: 25px;
	margin-bottom: 10px;
}
```

</details>

---

## 🐛 Common Mistakes and Troubleshooting

### Mistake 1: Parent Collapsing

**Problem:**

```css
/* ❌ Floated children, no clearfix */
.container {
	background: gray;
	/* Height = 0! */
}

.box {
	float: left;
	width: 200px;
}
```

**Solution:**

```css
/* ✅ Add clearfix */
.container::after {
	content: '';
	display: table;
	clear: both;
}
```

### Mistake 2: Widths Don't Add Up

**Problem:**

```css
/* ❌ Total exceeds 100% */
.sidebar {
	float: left;
	width: 30%;
	padding: 20px; /* Adds to width! */
}

.main {
	float: right;
	width: 70%;
	padding: 20px; /* Breaks layout! */
}
```

**Solution:**

```css
/* ✅ Use box-sizing */
.sidebar,
.main {
	box-sizing: border-box;
}
```

### Mistake 3: Forgetting to Clear

**Problem:**

```css
/* ❌ Footer slides up */
.content {
	float: left;
}

.footer {
	/* Overlaps floated content */
}
```

**Solution:**

```css
/* ✅ Clear the footer */
.footer {
	clear: both;
}
```

### Mistake 4: Pixel Widths with Percentage Columns

**Problem:**

```css
/* ❌ Mixing units causes issues */
.sidebar {
	float: left;
	width: 300px; /* Fixed */
}

.main {
	float: right;
	width: 70%; /* Percentage */
	/* Unpredictable on different screen sizes */
}
```

**Solution:**

```css
/* ✅ Use consistent units */
.sidebar {
	float: left;
	width: 25%;
}

.main {
	float: right;
	width: 72%;
}
```

### Mistake 5: Not Using Modern Alternatives

**Problem:** Using floats for everything when better options exist.

**Solution:**

```css
/* ✅ Use Flexbox or Grid for layout */
.container {
	display: flex;
	gap: 20px;
}

.sidebar {
	flex: 0 0 25%;
}

.main {
	flex: 1;
}

/* Much simpler than floats! */
```

---

## 🔄 Modern Alternatives to Floats

### Why Move Beyond Floats?

**Limitations of float-based layouts:**

-   ❌ Requires clearfix hacks
-   ❌ Parent collapse issues
-   ❌ Hard to vertically center
-   ❌ Complex responsive behavior
-   ❌ Not designed for layout (hack repurposed from text wrapping)

**Modern solutions:**

✅ **Flexbox** — One-dimensional layouts (rows or columns)
✅ **CSS Grid** — Two-dimensional layouts (rows and columns)
✅ **CSS Multi-Column** — Newspaper-style text flow

### Quick Flexbox Comparison

**Same layout with Flexbox:**

```css
/* Float version (old) */
.container-float {
	/* Needs clearfix */
}

.sidebar-float {
	float: left;
	width: 25%;
}

.main-float {
	float: right;
	width: 72%;
}

/* Flexbox version (modern) */
.container-flex {
	display: flex;
	gap: 20px; /* Easy gaps! */
}

.sidebar-flex {
	flex: 0 0 25%; /* Or just: width: 25% */
}

.main-flex {
	flex: 1; /* Takes remaining space */
}
```

**Benefits:**

-   No clearfix needed
-   No collapse issues
-   Easier to center
-   Built-in gap property
-   More intuitive

**Preview:** We'll learn Flexbox in detail next week (Session 13-14)!

### CSS Grid Quick Preview

**Same layout with CSS Grid:**

```css
/* Float version (old - complex) */
.container-float {
	max-width: 1200px;
	margin: 0 auto;
}

.sidebar-float {
	float: left;
	width: 25%;
	box-sizing: border-box;
}

.main-float {
	float: right;
	width: 72%;
	box-sizing: border-box;
}

.container-float::after {
	content: '';
	display: table;
	clear: both;
}

/* Grid version (modern - simple) */
.container-grid {
	display: grid;
	grid-template-columns: 1fr 3fr; /* 1:3 ratio */
	gap: 20px;
	max-width: 1200px;
	margin: 0 auto;
}

/* No need for width, float, or clearfix! */
```

**Benefits:**

-   Two-dimensional layouts (rows AND columns)
-   No clearfix needed
-   Gap property for spacing
-   Easier responsive design
-   Better alignment control

**Preview:** We'll learn CSS Grid in Week 06!

### Browser Compatibility Notes

**Float Property Support:**

| Browser | Version | Support |
| ------- | ------- | ------- |
| Chrome  | All     | ✅ Full |
| Firefox | All     | ✅ Full |
| Safari  | All     | ✅ Full |
| Edge    | All     | ✅ Full |
| IE      | 6+      | ✅ Full |

**CSS Multi-Column Support:**

| Property       | Chrome | Firefox | Safari | Edge | IE  |
| -------------- | ------ | ------- | ------ | ---- | --- |
| `column-count` | 50+    | 52+     | 9+     | 12+  | 10+ |
| `column-gap`   | 50+    | 52+     | 9+     | 12+  | 10+ |
| `column-rule`  | 50+    | 52+     | 9+     | 12+  | 10+ |
| `column-span`  | 50+    | 71+     | 9+     | 12+  | 10+ |
| `break-inside` | 50+    | 65+     | 10+    | 12+  | 10+ |

**Vendor Prefixes (for older browsers):**

```css
/* Include prefixes for broader support */
.newspaper {
	-webkit-column-count: 3; /* Chrome, Safari */
	-moz-column-count: 3; /* Firefox */
	column-count: 3; /* Standard */

	-webkit-column-gap: 40px;
	-moz-column-gap: 40px;
	column-gap: 40px;

	-webkit-column-rule: 1px solid #ccc;
	-moz-column-rule: 1px solid #ccc;
	column-rule: 1px solid #ccc;
}
```

**Modern approach (2025):** Vendor prefixes are rarely needed for floats and basic columns.

---

## 🏡 Homework Assignment

**Create a Multi-Column Magazine Layout**

Build a magazine-style article page that combines float layouts and CSS columns.

**Requirements:**

1. **Header** with site logo and navigation (full width)
2. **Hero section** with featured image and title
3. **Three-column section** with latest articles (using floats)
4. **Main article** with newspaper-style columns (using CSS columns)
5. **Sidebar** with "Related Articles" (float layout)
6. **Footer** with contact info and copyright

**Technical requirements:**

-   Use floats for structural layout (3-column articles, sidebar)
-   Use CSS columns for main article text
-   Apply clearfix where needed
-   Use `box-sizing: border-box` throughout
-   Ensure all sections have proper spacing
-   No parent collapse issues

**Bonus challenges:**

-   Add column rules to the main article
-   Make headings span across all columns
-   Prevent images from breaking across columns
-   Add hover effects to article cards
-   Create a sticky header

**Deliverables:**

-   `magazine-layout.html` — Complete HTML structure
-   Inline or external CSS with all layouts
-   Comments explaining float usage and clearing
-   At least 5 article cards in the three-column section

**Submission:** Create a folder `session-12-homework` with your files.

**Evaluation Criteria:**

| Criteria              | Points | Description                       |
| --------------------- | ------ | --------------------------------- |
| **HTML Structure**    | 15     | Semantic elements, proper nesting |
| **Float Layouts**     | 25     | Correct use of floats for columns |
| **Clearfix Applied**  | 15     | No parent collapse issues         |
| **CSS Columns**       | 20     | Proper newspaper-style article    |
| **Responsive Design** | 10     | Works on mobile and desktop       |
| **Code Quality**      | 10     | Clean, commented, organized       |
| **Design/Polish**     | 5      | Professional appearance           |
| **Total**             | 100    |                                   |
| **Bonus**             | +15    | Sticky header, animations, etc.   |

**Timeline:**

-   Start: End of Session 12
-   Due: Before Session 13 (Week 05)
-   Time needed: 2-3 hours

---

## 📚 Additional Resources

### Documentation

-   [MDN: float](https://developer.mozilla.org/en-US/docs/Web/CSS/float)
-   [MDN: clear](https://developer.mozilla.org/en-US/docs/Web/CSS/clear)
-   [MDN: CSS Columns](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_multicol_layout)
-   [CSS Tricks: All About Floats](https://css-tricks.com/all-about-floats/)
-   [CSS Tricks: The Clearfix](https://css-tricks.com/snippets/css/clear-fix/)

### Tutorials

-   [Learn CSS Float & Clear](https://www.freecodecamp.org/news/css-floats-explained-by-riding-an-escalator/)
-   [CSS Multi-Column Layout Guide](https://www.smashingmagazine.com/2019/01/css-multiple-column-layout-multicol/)
-   [Understanding Float Layouts](https://www.joshwcomeau.com/css/understanding-layout-algorithms/)

### Historical Context

-   [The Evolution of CSS Layouts](https://www.youtube.com/watch?v=qOUtkN6M52M)
-   [From Floats to Flexbox to Grid](https://chenhuijing.com/blog/from-floats-to-flexbox-to-grid/)

### Tools & Generators

-   [CSS Layout Generator](https://csslayout.io/) — Common layout patterns
-   [Gridulator](http://gridulator.com/) — Calculate grid percentages
-   [Float Layout Calculator](https://www.responsivegridsystem.com/) — Responsive grid generator

### Practice Exercises

-   [CSS Diner](https://flukeout.github.io/) — CSS selector game
-   [Flexbox Froggy](https://flexboxfroggy.com/) — Learn Flexbox (next week preview)
-   [Grid Garden](https://cssgridgarden.com/) — Learn CSS Grid (Week 06 preview)

### Video Tutorials

-   [CSS Floats Explained](https://www.youtube.com/watch?v=xara4Z1b18I) — Visual explanation
-   [The Clearfix Explained](https://www.youtube.com/watch?v=2tC4PIlEz_o) — Deep dive
-   [CSS Multi-Column Layout](https://www.youtube.com/watch?v=qOUtkN6M52M) — Practical examples

---

## 🎉 Session Summary

Congratulations! You've completed the CSS Layout I week. You can now:

✅ Create multi-column layouts using CSS floats
✅ Apply proper clearing techniques (clearfix, overflow, clear property)
✅ Build classic layout patterns (2-column, 3-column, Holy Grail)
✅ Use CSS Multi-Column Layout for newspaper-style text flow
✅ Understand the limitations of floats and when to use alternatives
✅ Debug and fix float collapse issues
✅ Calculate column widths and gaps correctly

**Looking ahead:**

**Week 05** introduces **Flexbox**, the modern solution for one-dimensional layouts. You'll find that many tasks you struggled with using floats become trivially easy with Flexbox!

**What you've learned this week:**

-   **Session 10:** Box model and spacing fundamentals
-   **Session 11:** Positioning schemes and z-index layering
-   **Session 12:** Multi-column layouts with floats and CSS columns

**Next week (Week 05):**

-   **Session 13:** Introduction to Flexbox
-   **Session 14:** Flexbox deep dive
-   **Session 15:** Mini Project 1 — Responsive Webpage

Keep practicing, and get ready to discover how much easier layouts become with modern CSS! 🚀

---

**Navigation:**
← [Week 04 Session 11](session-11.md) | [Week 04 Index](../week-04.md) | [Week 05 Session 13](../week-05/session-13.md) →
