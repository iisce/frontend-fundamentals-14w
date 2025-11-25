# Week 04 — Session 10: Box Model and Spacing

**Navigation:**
← [Week 03 Session 09](../week-03/session-09.md) | [Week 04 Index](../week-04.md) | [Session 11](session-11.md) →

---

**Session Length:** 90 minutes

## 📋 Pre-Class Checklist

Before starting this session, make sure you have:

-   ✅ Completed Week 03 (CSS Foundations I)
-   ✅ Understand basic CSS selectors and properties
-   ✅ Familiar with the box model concept (content, padding, border, margin)
-   ✅ Code editor (VS Code) with Live Server extension
-   ✅ Browser with Developer Tools (Chrome, Firefox, or Edge)
-   ✅ Create a new folder: `week-04-layout`

## 🎯 Learning Objectives

By the end of this session, you will be able to:

-   Master the CSS box model anatomy and calculations
-   Control spacing effectively with margin and padding
-   Use margin collapsing to your advantage
-   Apply `box-sizing` for predictable layouts
-   Visualize and debug layout boundaries
-   Create consistent spacing systems
-   Build real-world card and container layouts

## 📦 Files for This Session

-   `session-10.md` — This tutorial (you're reading it!)
-   `box-model-template.html` — Starter file for practice
-   `box-model-solution.html` — Complete working example
-   `spacing-cheat-sheet.md` — Quick reference guide
-   `box-model-visual.html` — Interactive visualization tool

## 🔑 Key Terms

**box model**, **content-box**, **border-box**, **margin**, **padding**, **border**, **margin collapse**, **auto margins**, **spacing system**, **CSS custom properties**, **calc()**, **min-content**, **max-content**, **fit-content**

## 🏗️ What You Will Build

-   A card grid with consistent spacing
-   A centered page layout container
-   A spacing system using CSS variables
-   A responsive content container

---

## Part 1: Box Model Deep Dive (20 minutes)

### Review: The Box Model Anatomy

Every HTML element is a rectangular box with four layers:

```
┌─────────────────────────────────────────────────────────┐
│                      MARGIN                             │
│    ┌───────────────────────────────────────────────┐    │
│    │                 BORDER                        │    │
│    │    ┌─────────────────────────────────────┐    │    │
│    │    │            PADDING                  │    │    │
│    │    │    ┌───────────────────────────┐    │    │    │
│    │    │    │         CONTENT           │    │    │    │
│    │    │    │    (width × height)       │    │    │    │
│    │    │    └───────────────────────────┘    │    │    │
│    │    └─────────────────────────────────────┘    │    │
│    └───────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────┘
```

**The layers from inside out:**

1. **Content** — The actual content (text, images, etc.)
2. **Padding** — Space between content and border (has background color)
3. **Border** — The visible boundary line
4. **Margin** — Space outside the border (transparent, creates gaps)

### Calculating Total Element Size

**With `box-sizing: content-box` (default):**

```css
.box {
	width: 300px;
	height: 200px;
	padding: 20px;
	border: 5px solid black;
	margin: 10px;
}
```

**Total calculations:**

-   **Total width** = width + padding-left + padding-right + border-left + border-right
-   **Total width** = 300 + 20 + 20 + 5 + 5 = **350px**
-   **Total height** = 200 + 20 + 20 + 5 + 5 = **250px**
-   **Space occupied** = Total width + margin-left + margin-right = 350 + 10 + 10 = **370px**

### The Box-Sizing Solution

**`box-sizing: border-box`** makes width/height include padding and border:

```css
.box {
	box-sizing: border-box;
	width: 300px;
	height: 200px;
	padding: 20px;
	border: 5px solid black;
}
```

**Now:**

-   **Total width** = 300px (padding and border are included!)
-   **Content width** = 300 - 20 - 20 - 5 - 5 = **250px**

### Universal Box-Sizing Reset

**Best practice:** Apply border-box to all elements:

```css
/* Modern reset */
*,
*::before,
*::after {
	box-sizing: border-box;
}
```

**Why this matters:**

-   Predictable sizing
-   Easier calculations
-   Works better with percentages
-   Industry standard practice

<details>
<summary>💡 Knowledge Check #1</summary>

**Question:** With `box-sizing: border-box`, if an element has `width: 400px`, `padding: 30px`, and `border: 10px solid black`, what is the content area width?

**Answer:**

Content width = Total width - padding-left - padding-right - border-left - border-right
Content width = 400 - 30 - 30 - 10 - 10 = **320px**

</details>

---

## Part 2: Mastering Margin (25 minutes)

### Margin Syntax

**Individual properties:**

```css
.element {
	margin-top: 20px;
	margin-right: 15px;
	margin-bottom: 20px;
	margin-left: 15px;
}
```

**Shorthand (clockwise from top — TRouBLe):**

```css
/* All sides */
margin: 20px;

/* Vertical | Horizontal */
margin: 20px 15px;

/* Top | Horizontal | Bottom */
margin: 10px 15px 20px;

/* Top | Right | Bottom | Left */
margin: 10px 15px 20px 25px;
```

### Centering with Auto Margins

**Horizontal centering** (for block elements with defined width):

```css
.container {
	width: 800px;
	max-width: 100%;
	margin-left: auto;
	margin-right: auto;
	/* Or shorthand: */
	margin: 0 auto;
}
```

**How it works:**

-   `auto` distributes available space equally
-   Left and right auto = centered horizontally
-   Only works on block elements with a set width

**Example: Centered Page Container**

```html
<style>
	body {
		margin: 0;
		background-color: #f5f5f5;
	}

	.page-container {
		width: 1200px;
		max-width: 100%; /* Responsive! */
		margin: 0 auto;
		padding: 0 20px;
		background-color: white;
		min-height: 100vh;
	}
</style>

<body>
	<div class="page-container">
		<h1>Centered Content</h1>
		<p>This container is centered on the page.</p>
	</div>
</body>
```

### Margin Collapse (Critical Concept!)

**What is margin collapse?**

When vertical margins of adjacent elements meet, they **collapse** into a single margin (the larger one wins).

**Example:**

```html
<style>
	.box1 {
		margin-bottom: 30px;
		background-color: lightblue;
		padding: 20px;
	}

	.box2 {
		margin-top: 20px;
		background-color: lightcoral;
		padding: 20px;
	}
</style>

<div class="box1">Box 1 (margin-bottom: 30px)</div>
<div class="box2">Box 2 (margin-top: 20px)</div>

<!-- Gap between them is 30px, NOT 50px! -->
```

### When Margins Collapse

Margins collapse in these situations:

1. **Adjacent siblings** — Vertical margins between sibling elements
2. **Parent and first/last child** — If no padding, border, or content separates them
3. **Empty elements** — Top and bottom margins of empty elements

**Adjacent siblings:**

```css
p {
	margin: 20px 0;
}
/* Gap between paragraphs is 20px, not 40px */
```

**Parent and child:**

```html
<style>
	.parent {
		margin-top: 0;
		background: lightgray;
	}

	.child {
		margin-top: 30px; /* This collapses with parent! */
	}
</style>

<div class="parent">
	<div class="child">Child element</div>
</div>
<!-- The 30px margin appears OUTSIDE the parent! -->
```

### Preventing Margin Collapse

**Methods to prevent collapse:**

```css
/* 1. Add padding to parent */
.parent {
	padding-top: 1px; /* Even 1px prevents collapse */
}

/* 2. Add border to parent */
.parent {
	border-top: 1px solid transparent;
}

/* 3. Use overflow (creates new formatting context) */
.parent {
	overflow: auto; /* or hidden */
}

/* 4. Use display: flow-root (modern) */
.parent {
	display: flow-root;
}

/* 5. Use flexbox or grid (no margin collapse!) */
.parent {
	display: flex;
	flex-direction: column;
}
```

<details>
<summary>💡 Knowledge Check #2</summary>

**Question:** Two adjacent `<div>` elements have `margin-bottom: 25px` and `margin-top: 35px` respectively. What is the actual gap between them?

**Answer:** **35px** — The larger margin wins when vertical margins collapse.

</details>

### Negative Margins

Pull elements closer or create overlaps:

```css
.overlap-up {
	margin-top: -20px; /* Pulls element up */
}

.expand-sides {
	margin-left: -20px;
	margin-right: -20px;
	/* Element extends beyond parent padding */
}
```

**Use case: Full-width element inside padded container**

```css
.container {
	padding: 0 40px;
}

.full-width-image {
	margin-left: -40px;
	margin-right: -40px;
	width: calc(100% + 80px);
}
```

---

## Part 3: Mastering Padding (15 minutes)

### Padding Syntax

Same syntax as margin:

```css
/* All sides */
padding: 20px;

/* Vertical | Horizontal */
padding: 20px 40px;

/* Top | Right | Bottom | Left */
padding: 10px 20px 30px 40px;
```

### Padding vs. Margin: Decision Guide

| Situation                          | Use Padding | Use Margin |
| ---------------------------------- | ----------- | ---------- |
| Space around text inside a box     | ✅          |            |
| Gap between two elements           |             | ✅         |
| Clickable/touchable area expansion | ✅          |            |
| Background color should extend     | ✅          |            |
| Centering elements                 |             | ✅ (auto)  |
| Creating rhythm between sections   |             | ✅         |

### Common Padding Patterns

**Button padding:**

```css
.button {
	/* More horizontal than vertical for better proportions */
	padding: 12px 24px;
}

.button-small {
	padding: 8px 16px;
}

.button-large {
	padding: 16px 32px;
}
```

**Card padding:**

```css
.card {
	padding: 24px;
}

.card-compact {
	padding: 16px;
}

.card-spacious {
	padding: 32px;
}
```

**Section padding:**

```css
.section {
	/* More vertical space for visual breathing room */
	padding: 60px 20px;
}

.section-hero {
	padding: 100px 20px;
}
```

### Percentage Padding

**Important:** Percentage padding is always relative to the **width** of the parent, even for top/bottom!

```css
.aspect-ratio-box {
	width: 100%;
	padding-top: 56.25%; /* 16:9 aspect ratio */
	position: relative;
}

.aspect-ratio-box > * {
	position: absolute;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
}
```

**Use case:** Responsive video containers, image placeholders

---

## Part 4: Building a Spacing System (15 minutes)

### Why Use a Spacing System?

-   **Consistency** — Same spacing values throughout
-   **Maintainability** — Change once, update everywhere
-   **Scalability** — Easy to add responsive variations
-   **Design harmony** — Visual rhythm and balance

### Creating a Spacing Scale

**Using CSS Custom Properties (Variables):**

```css
:root {
	/* Base unit: 4px or 8px */
	--space-unit: 8px;

	/* Spacing scale */
	--space-xs: calc(var(--space-unit) * 0.5); /* 4px */
	--space-sm: var(--space-unit); /* 8px */
	--space-md: calc(var(--space-unit) * 2); /* 16px */
	--space-lg: calc(var(--space-unit) * 3); /* 24px */
	--space-xl: calc(var(--space-unit) * 4); /* 32px */
	--space-2xl: calc(var(--space-unit) * 6); /* 48px */
	--space-3xl: calc(var(--space-unit) * 8); /* 64px */
}
```

**Using the spacing system:**

```css
.card {
	padding: var(--space-lg);
	margin-bottom: var(--space-xl);
}

.card-title {
	margin-bottom: var(--space-sm);
}

.card-text {
	margin-bottom: var(--space-md);
}

.section {
	padding: var(--space-3xl) var(--space-lg);
}
```

### Utility Classes for Spacing

Create reusable spacing utilities:

```css
/* Margin utilities */
.mt-sm {
	margin-top: var(--space-sm);
}
.mt-md {
	margin-top: var(--space-md);
}
.mt-lg {
	margin-top: var(--space-lg);
}
.mt-xl {
	margin-top: var(--space-xl);
}

.mb-sm {
	margin-bottom: var(--space-sm);
}
.mb-md {
	margin-bottom: var(--space-md);
}
.mb-lg {
	margin-bottom: var(--space-lg);
}
.mb-xl {
	margin-bottom: var(--space-xl);
}

/* Padding utilities */
.p-sm {
	padding: var(--space-sm);
}
.p-md {
	padding: var(--space-md);
}
.p-lg {
	padding: var(--space-lg);
}
.p-xl {
	padding: var(--space-xl);
}

/* Gap utility (for flex/grid) */
.gap-sm {
	gap: var(--space-sm);
}
.gap-md {
	gap: var(--space-md);
}
.gap-lg {
	gap: var(--space-lg);
}
```

**Usage:**

```html
<div class="card p-lg mb-xl">
	<h2 class="mb-sm">Card Title</h2>
	<p class="mb-md">Card content goes here.</p>
	<button>Action</button>
</div>
```

<details>
<summary>💡 Knowledge Check #3</summary>

**Question:** Why would you use CSS custom properties (variables) for spacing instead of hardcoding pixel values?

**Answer:**

1. **Consistency** — Same values used everywhere
2. **Easy updates** — Change the variable once, updates everywhere
3. **Responsive design** — Can change variable values at different breakpoints
4. **Design system alignment** — Matches design tokens from design tools
5. **Self-documenting** — Semantic names like `--space-lg` are clearer than `24px`

</details>

---

## Part 5: Debugging and Visualization (15 minutes)

### Visualizing Boxes with Outlines

**Debug technique:** Add outlines to see all boxes:

```css
/* See all element boxes */
* {
	outline: 1px solid red;
}

/* Or more specific */
.debug * {
	outline: 1px solid rgba(255, 0, 0, 0.3);
}

/* Color-coded by element type */
header {
	outline: 2px solid blue;
}
main {
	outline: 2px solid green;
}
section {
	outline: 2px solid orange;
}
div {
	outline: 1px solid red;
}
```

**Why outlines instead of borders?**

-   Outlines don't affect layout (no added width)
-   Don't trigger box model recalculations
-   Can overlap other elements

### Using Browser DevTools

**Steps to inspect box model:**

1. Right-click element → Inspect
2. Look at the **Computed** tab or **Layout** panel
3. Find the **Box Model** diagram
4. Hover over each section to see it highlighted

**DevTools features:**

-   **Live editing** — Change values and see results instantly
-   **Computed values** — See final calculated sizes
-   **Inherited values** — Track where styles come from
-   **Box model diagram** — Visual representation with exact pixel values

### Common Layout Debugging Issues

**Issue 1: Unexpected horizontal scrollbar**

```css
/* Problem: Element wider than viewport */
.element {
	width: 100%;
	padding: 20px; /* Adds to width! */
}

/* Solution: Use border-box */
* {
	box-sizing: border-box;
}
```

**Issue 2: Margin outside parent**

```css
/* Problem: Child margin collapses with parent */
.parent {
	background: gray;
}
.child {
	margin-top: 20px; /* Appears outside parent! */
}

/* Solution: Add padding or border to parent */
.parent {
	padding-top: 1px;
	/* Or: overflow: auto; */
	/* Or: display: flow-root; */
}
```

**Issue 3: Inconsistent spacing**

```css
/* Problem: Hard to maintain */
.card1 {
	margin: 15px;
}
.card2 {
	margin: 20px;
}
.card3 {
	margin: 18px;
}

/* Solution: Use spacing system */
.card {
	margin: var(--space-md);
}
```

---

## 🛠️ Hands-On Practice

### Exercise 1: Card Grid Layout (20 minutes)

Create a responsive card grid using proper spacing techniques.

**Requirements:**

-   Use `box-sizing: border-box` universally
-   Implement a spacing system with CSS variables
-   Create 3 cards in a row
-   Consistent gaps between cards
-   Proper padding inside cards
-   Centered container on the page

**Starter HTML:**

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta
			name="viewport"
			content="width=device-width, initial-scale=1.0"
		/>
		<title>Card Grid</title>
		<style>
			/* Reset */
			*,
			*::before,
			*::after {
				box-sizing: border-box;
				margin: 0;
				padding: 0;
			}

			/* Spacing System */
			:root {
				--space-xs: 4px;
				--space-sm: 8px;
				--space-md: 16px;
				--space-lg: 24px;
				--space-xl: 32px;
				--space-2xl: 48px;
			}

			body {
				font-family: Arial, sans-serif;
				background-color: #f0f0f0;
				line-height: 1.6;
			}

			/* Add your CSS here */
		</style>
	</head>
	<body>
		<div class="container">
			<h1 class="page-title">Our Services</h1>

			<div class="card-grid">
				<div class="card">
					<div class="card-icon">🎨</div>
					<h2 class="card-title">Design</h2>
					<p class="card-text">
						Beautiful, user-centered designs that engage and
						convert.
					</p>
					<button class="card-button">Learn More</button>
				</div>

				<div class="card">
					<div class="card-icon">💻</div>
					<h2 class="card-title">Development</h2>
					<p class="card-text">
						Clean, efficient code that brings designs to life.
					</p>
					<button class="card-button">Learn More</button>
				</div>

				<div class="card">
					<div class="card-icon">🚀</div>
					<h2 class="card-title">Launch</h2>
					<p class="card-text">
						Deployment and optimization for peak performance.
					</p>
					<button class="card-button">Learn More</button>
				</div>
			</div>
		</div>
	</body>
</html>
```

<details>
<summary>💡 Solution</summary>

```css
/* Reset */
*,
*::before,
*::after {
	box-sizing: border-box;
	margin: 0;
	padding: 0;
}

/* Spacing System */
:root {
	--space-xs: 4px;
	--space-sm: 8px;
	--space-md: 16px;
	--space-lg: 24px;
	--space-xl: 32px;
	--space-2xl: 48px;
}

body {
	font-family: Arial, sans-serif;
	background-color: #f0f0f0;
	line-height: 1.6;
	padding: var(--space-xl);
}

.container {
	max-width: 1200px;
	margin: 0 auto;
}

.page-title {
	text-align: center;
	margin-bottom: var(--space-2xl);
	color: #333;
}

.card-grid {
	display: flex;
	gap: var(--space-lg);
	justify-content: center;
}

.card {
	flex: 1;
	max-width: 350px;
	background-color: white;
	padding: var(--space-xl);
	border-radius: 8px;
	box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
	text-align: center;
}

.card-icon {
	font-size: 48px;
	margin-bottom: var(--space-md);
}

.card-title {
	margin-bottom: var(--space-sm);
	color: #333;
}

.card-text {
	margin-bottom: var(--space-lg);
	color: #666;
}

.card-button {
	padding: var(--space-sm) var(--space-lg);
	background-color: #667eea;
	color: white;
	border: none;
	border-radius: 4px;
	cursor: pointer;
	font-size: 16px;
}

.card-button:hover {
	background-color: #5a6fd6;
}
```

</details>

### Exercise 2: Centered Content Container (15 minutes)

Create a reusable centered container with proper responsive behavior.

**Requirements:**

-   Max-width of 1200px
-   Centered with auto margins
-   Side padding for small screens
-   Nested content with proper spacing

<details>
<summary>💡 Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta
			name="viewport"
			content="width=device-width, initial-scale=1.0"
		/>
		<title>Centered Container</title>
		<style>
			*,
			*::before,
			*::after {
				box-sizing: border-box;
				margin: 0;
				padding: 0;
			}

			:root {
				--space-md: 16px;
				--space-lg: 24px;
				--space-xl: 32px;
				--space-2xl: 48px;
				--container-max: 1200px;
				--container-padding: var(--space-lg);
			}

			body {
				font-family: Georgia, serif;
				line-height: 1.8;
				color: #333;
			}

			/* Reusable container */
			.container {
				width: 100%;
				max-width: var(--container-max);
				margin-left: auto;
				margin-right: auto;
				padding-left: var(--container-padding);
				padding-right: var(--container-padding);
			}

			/* Narrow container for text */
			.container--narrow {
				max-width: 800px;
			}

			.hero {
				background: linear-gradient(135deg, #667eea, #764ba2);
				color: white;
				padding: var(--space-2xl) 0;
			}

			.hero h1 {
				font-size: 48px;
				margin-bottom: var(--space-md);
			}

			.content-section {
				padding: var(--space-2xl) 0;
			}

			.content-section h2 {
				margin-bottom: var(--space-lg);
			}

			.content-section p {
				margin-bottom: var(--space-md);
			}

			.content-section p:last-child {
				margin-bottom: 0;
			}
		</style>
	</head>
	<body>
		<header class="hero">
			<div class="container">
				<h1>Welcome to Our Site</h1>
				<p>Building amazing web experiences with proper spacing.</p>
			</div>
		</header>

		<main>
			<section class="content-section">
				<div class="container container--narrow">
					<h2>About Our Approach</h2>
					<p>
						We believe in creating clean, well-spaced layouts that
						are easy to read and navigate. Good spacing isn't just
						about aesthetics—it's about usability.
					</p>
					<p>
						By using a consistent spacing system, we ensure visual
						harmony throughout the entire website while making
						maintenance much easier.
					</p>
					<p>
						Notice how this text container is narrower than the hero
						section above. This improves readability for longer text
						content.
					</p>
				</div>
			</section>
		</main>
	</body>
</html>
```

</details>

---

## 🐛 Common Mistakes & Troubleshooting

### Mistake 1: Forgetting Box-Sizing Reset

```css
/* ❌ WRONG: Inconsistent sizing */
.box {
	width: 100%;
	padding: 20px;
	/* Total width is now 100% + 40px! */
}

/* ✅ CORRECT: Apply border-box universally */
*,
*::before,
*::after {
	box-sizing: border-box;
}

.box {
	width: 100%;
	padding: 20px;
	/* Total width stays at 100% */
}
```

### Mistake 2: Not Accounting for Margin Collapse

```css
/* ❌ WRONG: Expecting 40px gap */
.section {
	margin-bottom: 20px;
}

.section + .section {
	margin-top: 20px;
}
/* Actual gap: 20px (collapsed) */

/* ✅ CORRECT: Use only one margin direction */
.section {
	margin-bottom: 40px;
}

.section:last-child {
	margin-bottom: 0;
}
```

### Mistake 3: Inconsistent Spacing Values

```css
/* ❌ WRONG: Random values */
.card {
	padding: 18px;
}
.button {
	padding: 11px 23px;
}
.section {
	margin: 47px 0;
}

/* ✅ CORRECT: Use spacing system */
.card {
	padding: var(--space-lg);
} /* 24px */
.button {
	padding: var(--space-sm) var(--space-lg);
} /* 8px 24px */
.section {
	margin: var(--space-2xl) 0;
} /* 48px 0 */
```

### Mistake 4: Using Margin for Internal Spacing

```css
/* ❌ WRONG: Margin for space inside container */
.container {
	background: gray;
}
.container > * {
	margin: 20px;
	/* First child's top margin collapses out! */
}

/* ✅ CORRECT: Use padding for internal space */
.container {
	background: gray;
	padding: 20px;
}
```

### Debugging Checklist

When spacing looks wrong:

1. ✅ Is `box-sizing: border-box` applied?
2. ✅ Are margins collapsing unexpectedly?
3. ✅ Is the parent using padding or margin correctly?
4. ✅ Are percentage values calculated correctly?
5. ✅ Check DevTools Box Model diagram
6. ✅ Add temporary outlines to visualize boxes

---

## 📝 Homework Assignment

Create a **"Team Members"** page with proper spacing:

**Content requirements:**

-   Page header with title and subtitle
-   Grid of 4 team member cards (2×2)
-   Each card includes:
    -   Profile image (use placeholder)
    -   Name
    -   Job title
    -   Short bio
    -   Social media links
-   Footer with company info

**Spacing requirements:**

-   Create a CSS spacing system using custom properties
-   Use `box-sizing: border-box` universally
-   Consistent margins and padding throughout
-   Centered page container (max-width: 1000px)
-   Proper spacing between all elements
-   Cards should have equal spacing between them

**Technical requirements:**

-   External CSS file
-   No margin collapse issues
-   Use only your spacing system variables (no random pixel values)
-   Comment your spacing system in the CSS

**Bonus challenges:**

-   Add hover effects on cards
-   Create utility classes for spacing
-   Make the grid responsive (stack on mobile)
-   Add a "featured" team member with different styling

---

## 🔍 What We Covered

✅ Box model anatomy and calculations
✅ `box-sizing: content-box` vs `border-box`
✅ Margin syntax and auto centering
✅ Margin collapse behavior and prevention
✅ Padding patterns and percentage padding
✅ Building a spacing system with CSS variables
✅ Debugging and visualizing layout boundaries
✅ Common spacing mistakes and solutions

---

## 📚 Additional Resources

**Official Documentation:**

-   [MDN: The Box Model](https://developer.mozilla.org/docs/Learn/CSS/Building_blocks/The_box_model)
-   [MDN: Mastering Margin Collapsing](https://developer.mozilla.org/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing)
-   [MDN: box-sizing](https://developer.mozilla.org/docs/Web/CSS/box-sizing)
-   [MDN: CSS Custom Properties](https://developer.mozilla.org/docs/Web/CSS/Using_CSS_custom_properties)

**Articles:**

-   [CSS Tricks: The Box Model](https://css-tricks.com/the-css-box-model/)
-   [Spacing in CSS](https://ishadeed.com/article/spacing-in-css/)
-   [Building a Spacing System](https://medium.com/eightshapes-llc/space-in-design-systems-188bcbae0d62)

**Tools:**

-   Browser DevTools Box Model Inspector
-   [CSS Box Model Visualizer](https://codepen.io/carolineartz/pen/ogVXZj)

---

## 🎯 Next Session Preview

In **Session 11: Positioning and Layering**, you'll learn:

-   CSS positioning schemes in depth (static, relative, absolute, fixed, sticky)
-   Z-index and stacking contexts
-   Creating layered designs
-   Building modals, tooltips, and sticky headers
-   Complex positioning patterns

**Preparation:** Make sure you understand the box model thoroughly — positioning builds directly on these concepts!

---

**Navigation:**
← [Week 03 Session 09](../week-03/session-09.md) | [Week 04 Index](../week-04.md) | [Session 11](session-11.md) →
