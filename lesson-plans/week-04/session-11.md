# Week 04 — Session 11: Positioning and Layering

**Navigation:**
← [Week 04 Session 10](session-10.md) | [Week 04 Index](../week-04.md) | [Session 12](session-12.md) →

---

**Session Length:** 90 minutes

## 📋 Pre-Class Checklist

Before starting this session, make sure you have:

-   ✅ Completed Session 10 (Box Model and Spacing)
-   ✅ Understand the CSS box model and spacing
-   ✅ Familiar with basic CSS selectors and properties
-   ✅ Code editor (VS Code) with Live Server extension
-   ✅ Browser with Developer Tools (Chrome, Firefox, or Edge)
-   ✅ Create a new folder: `week-04-positioning`

## 🎯 Learning Objectives

By the end of this session, you will be able to:

-   Understand CSS positioning schemes and their differences
-   Use `position: static`, `relative`, `absolute`, `fixed`, and `sticky`
-   Create layered designs with `z-index` and stacking contexts
-   Build common UI patterns (modals, tooltips, sticky headers)
-   Control element stacking order and overlapping
-   Implement practical positioning techniques
-   Debug positioning issues with DevTools

## 📦 Files for This Session

-   `session-11.md` — This tutorial (you're reading it!)
-   `positioning-template.html` — Starter file for practice
-   `positioning-solution.html` — Complete working example
-   `positioning-cheat-sheet.md` — Quick reference guide
-   `positioning-visual.html` — Interactive positioning demo

## 🔑 Key Terms

**positioning**, **position property**, **static**, **relative**, **absolute**, **fixed**, **sticky**, **z-index**, **stacking context**, **containing block**, **offset properties** (`top`, `right`, `bottom`, `left`), **overlay**, **modal**, **tooltip**, **layers**

## 🏗️ What You Will Build

-   A sticky navigation header
-   A modal dialog overlay
-   Tooltip notifications
-   A layered card design
-   A "back to top" button

---

## Part 1: Understanding Positioning Schemes (20 minutes)

### The Five Position Values

CSS provides five positioning schemes, each behaving differently:

| Position Value | Description                                        | Use Cases                                     |
| -------------- | -------------------------------------------------- | --------------------------------------------- |
| `static`       | Default; normal flow                               | Most elements (default)                       |
| `relative`     | Positioned relative to its normal position         | Nudging elements, creating containing blocks  |
| `absolute`     | Positioned relative to nearest positioned ancestor | Overlays, tooltips, badges, dropdowns         |
| `fixed`        | Positioned relative to the viewport                | Sticky headers, "back to top" buttons, modals |
| `sticky`       | Toggles between relative and fixed                 | Sticky headers, table headers, sidebars       |

### Position: Static (Default)

**What it does:** Element flows normally in the document.

**Characteristics:**

-   Default positioning for all elements
-   `top`, `right`, `bottom`, `left`, and `z-index` have **no effect**
-   Elements stack vertically (block) or horizontally (inline)

```css
/* This is the default - you rarely need to write it */
.normal-element {
	position: static;
}
```

**Example:**

```html
<div class="box">I'm in normal flow</div>
<div class="box">Me too!</div>
<div class="box">All of us!</div>
```

```css
.box {
	/* position: static is implicit */
	background: lightblue;
	padding: 20px;
	margin-bottom: 10px;
}
```

### Position: Relative

**What it does:** Positioned relative to where it **would normally be**.

**Characteristics:**

-   Element **still occupies its original space** in normal flow
-   Can be offset using `top`, `right`, `bottom`, `left`
-   Creates a **containing block** for absolutely positioned children
-   Other elements don't move to fill the gap

```css
.relative-box {
	position: relative;
	top: 20px; /* Move down 20px from normal position */
	left: 30px; /* Move right 30px from normal position */
}
```

**Visual representation:**

```
Normal flow:
┌─────┐
│ Box │
└─────┘

With position: relative; top: 20px; left: 30px;
┌─────┐ (ghost - original space reserved)
│     │
    ┌─────┐
    │ Box │ (moved, but space still reserved above)
    └─────┘
```

**Example:**

```html
<div class="container">
	<div class="box box-1">Box 1</div>
	<div class="box box-2">Box 2 (shifted)</div>
	<div class="box box-3">Box 3</div>
</div>
```

```css
.box {
	background: coral;
	padding: 20px;
	margin-bottom: 10px;
}

.box-2 {
	position: relative;
	top: 15px;
	left: 40px;
	background: skyblue;
}
```

**Result:** Box 2 moves down and right, but Boxes 1 and 3 stay in their original positions.

<details>
<summary>💡 Knowledge Check #1</summary>

**Question:** If an element has `position: relative; top: 10px;`, which direction does it move?

**Answer:**

It moves **down** by 10px. The `top` property means "offset from the top edge," so a positive value pushes the element down. Similarly:

-   `top: -10px` moves it **up**
-   `left: 10px` moves it **right**
-   `left: -10px` moves it **left**

The offset properties can be confusing because they specify where the edge should be positioned, not the direction of movement.

</details>

### Position: Absolute

**What it does:** Positioned relative to the **nearest positioned ancestor** (or viewport if none exists).

**Characteristics:**

-   **Removed from normal flow** — doesn't occupy space
-   Other elements behave as if it doesn't exist
-   Positioned using `top`, `right`, `bottom`, `left`
-   "Positioned ancestor" = any ancestor with `position: relative`, `absolute`, `fixed`, or `sticky`

**Finding the containing block:**

1. Look for the nearest ancestor with `position: relative` (most common)
2. If none, look for `absolute`, `fixed`, or `sticky` ancestor
3. If still none, positioned relative to the `<html>` element (viewport)

```css
.parent {
	position: relative; /* Creates containing block */
	width: 300px;
	height: 200px;
	background: lightgray;
}

.child {
	position: absolute;
	top: 20px; /* 20px from parent's top edge */
	right: 20px; /* 20px from parent's right edge */
	background: coral;
	padding: 10px;
}
```

**Example: Badge on a card**

```html
<div class="card">
	<span class="badge">New</span>
	<h3>Product Title</h3>
	<p>Product description goes here.</p>
</div>
```

```css
.card {
	position: relative; /* Containing block for badge */
	width: 300px;
	padding: 20px;
	border: 1px solid #ddd;
	border-radius: 8px;
}

.badge {
	position: absolute;
	top: 10px;
	right: 10px;
	background: crimson;
	color: white;
	padding: 5px 10px;
	border-radius: 12px;
	font-size: 12px;
	font-weight: bold;
}
```

**Result:** Badge appears in the top-right corner of the card, regardless of content flow.

### Position: Fixed

**What it does:** Positioned relative to the **viewport** (browser window).

**Characteristics:**

-   **Removed from normal flow**
-   Stays in the same position even when scrolling
-   Always positioned relative to viewport (ignores ancestors)
-   Perfect for sticky headers, modals, "back to top" buttons

```css
.fixed-header {
	position: fixed;
	top: 0;
	left: 0;
	right: 0; /* Stretch full width */
	background: #333;
	color: white;
	padding: 15px;
	z-index: 1000; /* Stay on top of other content */
}
```

**Example: Fixed navigation bar**

```html
<nav class="navbar">
	<h1>My Site</h1>
	<ul>
		<li><a href="#home">Home</a></li>
		<li><a href="#about">About</a></li>
		<li><a href="#contact">Contact</a></li>
	</ul>
</nav>

<main class="content">
	<!-- Long content that scrolls -->
</main>
```

```css
.navbar {
	position: fixed;
	top: 0;
	left: 0;
	right: 0;
	background: #2c3e50;
	color: white;
	padding: 1rem;
	z-index: 100;
	box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.content {
	margin-top: 60px; /* Prevent content from hiding under fixed navbar */
	padding: 20px;
}
```

### Position: Sticky

**What it does:** Toggles between `relative` and `fixed` based on scroll position.

**Characteristics:**

-   Acts like `relative` until a scroll threshold is reached
-   Then becomes `fixed` within its parent container
-   Requires at least one offset value (`top`, `bottom`, etc.)
-   Parent must have sufficient height to scroll

```css
.sticky-header {
	position: sticky;
	top: 0; /* Stick when scrolled to top of viewport */
	background: white;
	z-index: 10;
}
```

**Example: Sticky section headers**

```html
<section>
	<h2 class="sticky-heading">Chapter 1</h2>
	<p>Content for chapter 1...</p>
	<p>More content...</p>
</section>

<section>
	<h2 class="sticky-heading">Chapter 2</h2>
	<p>Content for chapter 2...</p>
	<p>More content...</p>
</section>
```

```css
.sticky-heading {
	position: sticky;
	top: 0;
	background: #f0f0f0;
	padding: 15px;
	margin: 0;
	border-bottom: 2px solid #333;
	z-index: 10;
}

section {
	min-height: 100vh; /* Ensure enough height to scroll */
}
```

**Result:** Each chapter heading sticks to the top when scrolling until the next heading pushes it away.

<details>
<summary>💡 Knowledge Check #2</summary>

**Question:** What's the main difference between `position: fixed` and `position: sticky`?

**Answer:**

**`fixed`:**

-   Always positioned relative to the viewport
-   Stays in the same position regardless of scrolling
-   Removed from normal flow immediately

**`sticky`:**

-   Acts as `relative` initially (in normal flow)
-   Becomes `fixed` when reaching the scroll threshold (e.g., `top: 0`)
-   Only sticks within its parent container
-   Returns to normal flow when parent scrolls out of view

**Example use cases:**

-   `fixed`: Global navigation, "back to top" button, chat widget
-   `sticky`: Table headers, section headers, sidebar that sticks while scrolling

</details>

---

## Part 2: Offset Properties and Centering (15 minutes)

### The Offset Properties

When using positioned elements (except `static`), you control placement with:

| Property | Description                   | Example       |
| -------- | ----------------------------- | ------------- |
| `top`    | Distance from the top edge    | `top: 20px;`  |
| `right`  | Distance from the right edge  | `right: 10%;` |
| `bottom` | Distance from the bottom edge | `bottom: 0;`  |
| `left`   | Distance from the left edge   | `left: 50px;` |

**Values can be:**

-   Pixels: `top: 20px;`
-   Percentages: `left: 50%;` (relative to containing block)
-   `auto` (default): Browser calculates automatically
-   Negative values: `top: -10px;` (moves in opposite direction)

### Combining Offset Properties

You can use multiple offsets together:

**Stretch to fill parent:**

```css
.overlay {
	position: absolute;
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;
	/* Equivalent to: width: 100%; height: 100%; */
}
```

**Position in specific corner:**

```css
/* Top-right corner */
.top-right {
	position: absolute;
	top: 10px;
	right: 10px;
}

/* Bottom-left corner */
.bottom-left {
	position: absolute;
	bottom: 10px;
	left: 10px;
}
```

### Centering with Absolute Positioning

**Method 1: 50% + negative margin (old school)**

```css
.centered-old {
	position: absolute;
	top: 50%;
	left: 50%;
	width: 200px;
	height: 100px;
	margin-top: -50px; /* Half of height */
	margin-left: -100px; /* Half of width */
}
```

**Method 2: 50% + transform (modern)**

```css
.centered-modern {
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
	/* No need to know width/height! */
}
```

**Method 3: Using inset and margin (newest)**

```css
.centered-newest {
	position: absolute;
	inset: 0; /* Shorthand for top: 0; right: 0; bottom: 0; left: 0; */
	margin: auto;
	width: 300px; /* Must specify dimensions */
	height: 200px;
}
```

**Example: Centered modal dialog**

```html
<div class="modal-backdrop">
	<div class="modal">
		<h2>Welcome!</h2>
		<p>This is a centered modal dialog.</p>
		<button>Close</button>
	</div>
</div>
```

```css
.modal-backdrop {
	position: fixed;
	inset: 0; /* Cover entire viewport */
	background: rgba(0, 0, 0, 0.5);
	display: flex; /* Alternative centering method */
	align-items: center;
	justify-content: center;
}

/* Or using absolute positioning */
.modal {
	position: relative; /* If using flex on parent */
	/* OR */
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);

	background: white;
	padding: 30px;
	border-radius: 8px;
	max-width: 500px;
	box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
}
```

### The `inset` Shorthand Property

**New shorthand for offset properties:**

```css
/* Longhand */
.element {
	top: 10px;
	right: 20px;
	bottom: 10px;
	left: 20px;
}

/* Shorthand (same as above) */
.element {
	inset: 10px 20px 10px 20px; /* top right bottom left */
}

/* All sides equal */
.element {
	inset: 0; /* Same as: top: 0; right: 0; bottom: 0; left: 0; */
}

/* Vertical and horizontal */
.element {
	inset: 10px 20px; /* top/bottom left/right */
}
```

<details>
<summary>💡 Knowledge Check #3</summary>

**Question:** Why is `transform: translate(-50%, -50%)` preferred over negative margins for centering?

**Answer:**

**Advantages of `transform: translate(-50%, -50%)`:**

1. **No need to know dimensions**: Works without knowing width/height
2. **Responsive**: Automatically adjusts if content size changes
3. **Cleaner code**: No calculations needed
4. **More flexible**: Works with dynamic content

**Negative margin method requires:**

-   Fixed/known width and height
-   Manual calculation of half the dimensions
-   Updates if size changes

**Example:**

```css
/* ❌ Old way - must know size */
.modal {
	position: absolute;
	top: 50%;
	left: 50%;
	width: 400px;
	height: 300px;
	margin-top: -150px; /* Half of 300px */
	margin-left: -200px; /* Half of 400px */
}

/* ✅ Modern way - size agnostic */
.modal {
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
	/* Width and height can be anything or dynamic! */
}
```

</details>

---

## Part 3: Z-Index and Stacking Contexts (20 minutes)

### Understanding Z-Index

The `z-index` property controls the **stacking order** of positioned elements (the 3D layer).

**Key rules:**

1. **Only works on positioned elements** (not `static`)
2. Higher values stack on top of lower values
3. Default value is `auto` (same as `0`)
4. Can be positive or negative integers
5. Creates a stacking context

**Basic example:**

```css
.layer-1 {
	position: relative;
	z-index: 1;
	background: blue;
}

.layer-2 {
	position: relative;
	z-index: 2;
	background: red;
}

.layer-3 {
	position: relative;
	z-index: 3;
	background: green;
}
```

**Result:** Layer 3 (green) appears on top, then layer 2 (red), then layer 1 (blue).

### Stacking Contexts

A **stacking context** is a 3D layer in which child elements are stacked.

**What creates a stacking context:**

-   Root element (`<html>`)
-   Positioned elements with `z-index` other than `auto`
-   Elements with `opacity` less than 1
-   Elements with `transform`, `filter`, `perspective`
-   Elements with `position: fixed` or `position: sticky`
-   Flex/grid items with `z-index` other than `auto`

**Important rule:**

**Child elements can only compete with siblings in the same stacking context.**

**Example of nested stacking:**

```html
<div class="parent-1">
	<div class="child-1">Child 1 (z-index: 999)</div>
</div>

<div class="parent-2">
	<div class="child-2">Child 2 (z-index: 1)</div>
</div>
```

```css
.parent-1 {
	position: relative;
	z-index: 1; /* Creates stacking context */
}

.child-1 {
	position: relative;
	z-index: 999; /* High value, but trapped in parent-1's context! */
	background: blue;
}

.parent-2 {
	position: relative;
	z-index: 2; /* Higher than parent-1 */
}

.child-2 {
	position: relative;
	z-index: 1;
	background: red;
}
```

**Result:** Child 2 appears on top, even though child-1 has `z-index: 999`!

**Why?** Parent-2's stacking context (z-index: 2) is higher than parent-1's (z-index: 1).

### Common Z-Index Values

**Standard scale for UI elements:**

```css
/* Background elements */
.background {
	z-index: -1;
}

/* Normal content */
.content {
	z-index: 0;
} /* or auto */

/* Floating elements */
.dropdown {
	z-index: 10;
}
.tooltip {
	z-index: 20;
}

/* Overlays */
.overlay {
	z-index: 100;
}

/* Modals */
.modal {
	z-index: 1000;
}

/* Notifications/Toasts */
.notification {
	z-index: 5000;
}

/* Critical UI (e.g., cookie consent) */
.critical {
	z-index: 9999;
}
```

**Best practices:**

-   Use a **consistent scale** (e.g., increments of 10 or 100)
-   Document your z-index values in CSS comments
-   Avoid arbitrarily high values (like 999999)
-   Use CSS custom properties for z-index management

**Example: Z-index system**

```css
:root {
	--z-base: 0;
	--z-dropdown: 10;
	--z-sticky: 100;
	--z-overlay: 1000;
	--z-modal: 2000;
	--z-tooltip: 3000;
	--z-notification: 5000;
}

.modal {
	position: fixed;
	z-index: var(--z-modal);
}

.tooltip {
	position: absolute;
	z-index: var(--z-tooltip);
}
```

### Debugging Stacking Issues

**Common problems and solutions:**

**Problem 1: Element not responding to z-index**

```css
/* ❌ Won't work - element is static */
.element {
	z-index: 10;
}

/* ✅ Fixed - add positioning */
.element {
	position: relative;
	z-index: 10;
}
```

**Problem 2: Child can't stack above unrelated element**

```css
/* ❌ Child trapped in parent's stacking context */
.parent {
	position: relative;
	z-index: 1;
}

.child {
	position: absolute;
	z-index: 999; /* Can't escape parent's context */
}

/* ✅ Solution: increase parent's z-index or remove it */
.parent {
	position: relative;
	/* Remove z-index, or increase it */
}
```

**Problem 3: Transform creates unexpected stacking context**

```css
/* ❌ Transform creates stacking context */
.parent {
	transform: translateX(0); /* Creates stacking context! */
}

.child {
	position: absolute;
	z-index: 999; /* Trapped in parent's context */
}
```

<details>
<summary>💡 Knowledge Check #4</summary>

**Question:** Will `<div class="child">` appear above `<div class="other">`? Why or why not?

```html
<div
	class="parent"
	style="position: relative; z-index: 5;"
>
	<div
		class="child"
		style="position: absolute; z-index: 100;"
	>
		Child
	</div>
</div>
<div
	class="other"
	style="position: relative; z-index: 10;"
>
	Other
</div>
```

**Answer:**

**No**, the child will **not** appear above "Other."

**Explanation:**

1. The `.parent` has `z-index: 5`, creating a stacking context
2. The `.child` has `z-index: 100`, but it only competes within `.parent`'s stacking context
3. The `.other` has `z-index: 10` and exists in the root stacking context
4. At the root level: `.other` (z-index: 10) > `.parent` (z-index: 5)
5. Therefore, `.other` and all its contents appear above `.parent` and all its contents

**Key principle:** Child elements cannot escape their parent's stacking context to compete with elements outside it.

</details>

---

## Part 4: Hands-On Practice (35 minutes)

### Exercise 1: Sticky Navigation Header (15 minutes)

**Goal:** Create a navigation header that sticks to the top when scrolling.

**Requirements:**

1. Create an HTML page with a header and long content
2. Header should contain logo and navigation links
3. Header sticks to the top when scrolling
4. Add smooth shadow when stuck
5. Content should not jump when header becomes sticky

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
		<title>Sticky Navigation</title>
		<style>
			* {
				margin: 0;
				padding: 0;
				box-sizing: border-box;
			}

			body {
				font-family: Arial, sans-serif;
				line-height: 1.6;
			}

			/* TODO: Style the header */
			.header {
				/* Add sticky positioning here */
				background: #2c3e50;
				color: white;
				padding: 1rem 2rem;
			}

			.header nav {
				display: flex;
				justify-content: space-between;
				align-items: center;
			}

			.header ul {
				list-style: none;
				display: flex;
				gap: 2rem;
			}

			.header a {
				color: white;
				text-decoration: none;
			}

			.content {
				padding: 2rem;
				max-width: 800px;
				margin: 0 auto;
			}

			.content section {
				margin-bottom: 3rem;
				min-height: 60vh;
			}

			.content h2 {
				margin-bottom: 1rem;
				color: #2c3e50;
			}
		</style>
	</head>
	<body>
		<header class="header">
			<nav>
				<h1>My Website</h1>
				<ul>
					<li><a href="#home">Home</a></li>
					<li><a href="#about">About</a></li>
					<li><a href="#services">Services</a></li>
					<li><a href="#contact">Contact</a></li>
				</ul>
			</nav>
		</header>

		<main class="content">
			<section id="home">
				<h2>Home</h2>
				<p>
					Welcome to our website. Scroll down to see the sticky
					navigation in action.
				</p>
				<p>
					Lorem ipsum dolor sit amet, consectetur adipiscing elit.
					Nullam euismod, nisl eget ultricies aliquam, nunc nisl
					aliquet nunc, quis aliquam nisl nunc quis nisl.
				</p>
			</section>

			<section id="about">
				<h2>About Us</h2>
				<p>Learn more about our company and mission.</p>
				<p>
					Lorem ipsum dolor sit amet, consectetur adipiscing elit.
					Nullam euismod, nisl eget ultricies aliquam, nunc nisl
					aliquet nunc, quis aliquam nisl nunc quis nisl.
				</p>
			</section>

			<section id="services">
				<h2>Our Services</h2>
				<p>Discover the services we offer to our clients.</p>
				<p>
					Lorem ipsum dolor sit amet, consectetur adipiscing elit.
					Nullam euismod, nisl eget ultricies aliquam, nunc nisl
					aliquet nunc, quis aliquam nisl nunc quis nisl.
				</p>
			</section>

			<section id="contact">
				<h2>Contact</h2>
				<p>Get in touch with us today.</p>
				<p>
					Lorem ipsum dolor sit amet, consectetur adipiscing elit.
					Nullam euismod, nisl eget ultricies aliquam, nunc nisl
					aliquet nunc, quis aliquam nisl nunc quis nisl.
				</p>
			</section>
		</main>
	</body>
</html>
```

**Tasks:**

1. Add `position: sticky` to the header with `top: 0`
2. Add `z-index` to ensure it stays on top of content
3. Add a box-shadow for depth when sticky
4. Test by scrolling the page

<details>
<summary>✅ Solution</summary>

```css
.header {
	position: sticky;
	top: 0;
	background: #2c3e50;
	color: white;
	padding: 1rem 2rem;
	z-index: 100;
	box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

/* Optional: Add hover effects to links */
.header a:hover {
	color: #3498db;
	transition: color 0.3s ease;
}
```

**Enhanced version with scroll-triggered shadow:**

```html
<!-- Add this script before closing </body> tag -->
<script>
	const header = document.querySelector('.header');

	window.addEventListener('scroll', () => {
		if (window.scrollY > 0) {
			header.style.boxShadow = '0 2px 10px rgba(0, 0, 0, 0.2)';
		} else {
			header.style.boxShadow = 'none';
		}
	});
</script>
```

</details>

### Exercise 2: Modal Dialog Overlay (20 minutes)

**Goal:** Create a modal dialog that appears centered on the screen with a backdrop overlay.

**Requirements:**

1. Modal should be centered both horizontally and vertically
2. Backdrop should cover the entire viewport with semi-transparent background
3. Modal should appear above all other content
4. Include a close button
5. Use proper z-index layering

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
		<title>Modal Dialog</title>
		<style>
			* {
				margin: 0;
				padding: 0;
				box-sizing: border-box;
			}

			body {
				font-family: Arial, sans-serif;
				padding: 2rem;
			}

			/* TODO: Style the modal backdrop */
			.modal-backdrop {
				/* Add positioning and styling here */
				display: none; /* Hidden by default */
			}

			.modal-backdrop.active {
				display: block;
			}

			/* TODO: Style the modal */
			.modal {
				/* Add centering and styling here */
				background: white;
				padding: 2rem;
				border-radius: 8px;
				max-width: 500px;
				width: 90%;
			}

			.modal-header {
				display: flex;
				justify-content: space-between;
				align-items: center;
				margin-bottom: 1rem;
				padding-bottom: 1rem;
				border-bottom: 1px solid #eee;
			}

			.modal-header h2 {
				margin: 0;
				color: #2c3e50;
			}

			.close-btn {
				background: none;
				border: none;
				font-size: 1.5rem;
				cursor: pointer;
				color: #999;
				padding: 0;
				width: 30px;
				height: 30px;
				display: flex;
				align-items: center;
				justify-content: center;
				border-radius: 4px;
			}

			.close-btn:hover {
				background: #f0f0f0;
				color: #333;
			}

			.modal-body {
				margin-bottom: 1.5rem;
			}

			.modal-footer {
				display: flex;
				justify-content: flex-end;
				gap: 1rem;
			}

			.btn {
				padding: 0.5rem 1.5rem;
				border: none;
				border-radius: 4px;
				cursor: pointer;
				font-size: 1rem;
			}

			.btn-primary {
				background: #3498db;
				color: white;
			}

			.btn-secondary {
				background: #95a5a6;
				color: white;
			}

			.open-modal-btn {
				padding: 1rem 2rem;
				background: #2ecc71;
				color: white;
				border: none;
				border-radius: 4px;
				font-size: 1rem;
				cursor: pointer;
			}

			.open-modal-btn:hover {
				background: #27ae60;
			}
		</style>
	</head>
	<body>
		<h1>Modal Dialog Example</h1>
		<p>Click the button below to open the modal dialog.</p>
		<button
			class="open-modal-btn"
			onclick="openModal()"
		>
			Open Modal
		</button>

		<!-- Modal Structure -->
		<div
			class="modal-backdrop"
			id="modalBackdrop"
		>
			<div class="modal">
				<div class="modal-header">
					<h2>Confirm Action</h2>
					<button
						class="close-btn"
						onclick="closeModal()"
					>
						&times;
					</button>
				</div>
				<div class="modal-body">
					<p>
						Are you sure you want to perform this action? This
						cannot be undone.
					</p>
					<p>
						Please review the details carefully before confirming.
					</p>
				</div>
				<div class="modal-footer">
					<button
						class="btn btn-secondary"
						onclick="closeModal()"
					>
						Cancel
					</button>
					<button
						class="btn btn-primary"
						onclick="confirmAction()"
					>
						Confirm
					</button>
				</div>
			</div>
		</div>

		<script>
			function openModal() {
				document
					.getElementById('modalBackdrop')
					.classList.add('active');
			}

			function closeModal() {
				document
					.getElementById('modalBackdrop')
					.classList.remove('active');
			}

			function confirmAction() {
				alert('Action confirmed!');
				closeModal();
			}

			// Close modal when clicking on backdrop
			document
				.getElementById('modalBackdrop')
				.addEventListener('click', function (e) {
					if (e.target === this) {
						closeModal();
					}
				});
		</script>
	</body>
</html>
```

**Tasks:**

1. Make the backdrop cover the full viewport using `fixed` positioning
2. Center the modal using absolute positioning and transform
3. Add semi-transparent background to backdrop
4. Set appropriate z-index values
5. Test opening and closing the modal

<details>
<summary>✅ Solution</summary>

```css
/* Modal Backdrop */
.modal-backdrop {
	position: fixed;
	inset: 0; /* Cover entire viewport: top: 0; right: 0; bottom: 0; left: 0; */
	background: rgba(0, 0, 0, 0.5); /* Semi-transparent black */
	z-index: 1000; /* Above normal content */
	display: none;

	/* Optional: Smooth fade-in */
	animation: fadeIn 0.3s ease;
}

.modal-backdrop.active {
	display: flex; /* Use flex for easier centering */
	align-items: center;
	justify-content: center;
}

/* Modal */
.modal {
	/* Using flex centering from parent */
	background: white;
	padding: 2rem;
	border-radius: 8px;
	max-width: 500px;
	width: 90%;
	box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
	z-index: 1001; /* Above backdrop */

	/* Optional: Smooth scale-in */
	animation: scaleIn 0.3s ease;
}

/* Alternative centering method using absolute positioning */
.modal-alternative {
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
	background: white;
	padding: 2rem;
	border-radius: 8px;
	max-width: 500px;
	width: 90%;
	box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
}

/* Optional animations */
@keyframes fadeIn {
	from {
		opacity: 0;
	}
	to {
		opacity: 1;
	}
}

@keyframes scaleIn {
	from {
		transform: scale(0.9);
		opacity: 0;
	}
	to {
		transform: scale(1);
		opacity: 1;
	}
}
```

**Enhanced version with better accessibility:**

```html
<!-- Add role and aria attributes -->
<div
	class="modal-backdrop"
	id="modalBackdrop"
	role="dialog"
	aria-modal="true"
	aria-labelledby="modalTitle"
>
	<div class="modal">
		<div class="modal-header">
			<h2 id="modalTitle">Confirm Action</h2>
			<button
				class="close-btn"
				onclick="closeModal()"
				aria-label="Close modal"
			>
				&times;
			</button>
		</div>
		<!-- Rest of modal content -->
	</div>
</div>
```

</details>

---

## 📚 Common Positioning Patterns

### Pattern 1: Tooltip

```css
.tooltip-container {
	position: relative;
	display: inline-block;
}

.tooltip {
	position: absolute;
	bottom: 100%; /* Position above the element */
	left: 50%;
	transform: translateX(-50%);
	background: #333;
	color: white;
	padding: 8px 12px;
	border-radius: 4px;
	white-space: nowrap;
	opacity: 0;
	pointer-events: none;
	transition: opacity 0.3s;
	margin-bottom: 8px;
}

/* Arrow */
.tooltip::after {
	content: '';
	position: absolute;
	top: 100%;
	left: 50%;
	transform: translateX(-50%);
	border: 6px solid transparent;
	border-top-color: #333;
}

.tooltip-container:hover .tooltip {
	opacity: 1;
}
```

### Pattern 2: Badge on Button

```css
.button-container {
	position: relative;
	display: inline-block;
}

.badge {
	position: absolute;
	top: -8px;
	right: -8px;
	background: crimson;
	color: white;
	border-radius: 50%;
	width: 24px;
	height: 24px;
	display: flex;
	align-items: center;
	justify-content: center;
	font-size: 12px;
	font-weight: bold;
}
```

### Pattern 3: Back to Top Button

```css
.back-to-top {
	position: fixed;
	bottom: 30px;
	right: 30px;
	width: 50px;
	height: 50px;
	background: #3498db;
	color: white;
	border: none;
	border-radius: 50%;
	font-size: 24px;
	cursor: pointer;
	opacity: 0;
	pointer-events: none;
	transition: opacity 0.3s, background 0.3s;
	z-index: 1000;
}

.back-to-top.visible {
	opacity: 1;
	pointer-events: auto;
}

.back-to-top:hover {
	background: #2980b9;
}
```

### Pattern 4: Dropdown Menu

```css
.dropdown {
	position: relative;
	display: inline-block;
}

.dropdown-menu {
	position: absolute;
	top: 100%;
	left: 0;
	background: white;
	border: 1px solid #ddd;
	border-radius: 4px;
	min-width: 200px;
	box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
	opacity: 0;
	visibility: hidden;
	transform: translateY(-10px);
	transition: all 0.3s ease;
	z-index: 10;
}

.dropdown:hover .dropdown-menu {
	opacity: 1;
	visibility: visible;
	transform: translateY(0);
}
```

---

## 🐛 Common Mistakes and Troubleshooting

### Mistake 1: Forgetting to Position the Parent

**Problem:**

```css
/* ❌ Child won't position correctly */
.parent {
	/* No position set */
}

.child {
	position: absolute;
	top: 20px;
	left: 20px;
}
```

**Solution:**

```css
/* ✅ Parent creates containing block */
.parent {
	position: relative; /* Now child positions relative to parent */
}

.child {
	position: absolute;
	top: 20px;
	left: 20px;
}
```

### Mistake 2: Z-Index Not Working

**Problem:**

```css
/* ❌ Element is static */
.element {
	z-index: 999; /* Won't work! */
}
```

**Solution:**

```css
/* ✅ Add positioning */
.element {
	position: relative; /* or absolute, fixed, sticky */
	z-index: 999;
}
```

### Mistake 3: Fixed Element Not Staying Fixed

**Problem:**

```css
/* ❌ Parent with transform creates new containing block */
.parent {
	transform: translateX(0);
}

.child {
	position: fixed; /* Will be fixed to parent, not viewport! */
}
```

**Solution:**

```css
/* ✅ Remove transform from parent or move fixed element outside */
.parent {
	/* Don't use transform if child needs to be fixed to viewport */
}

/* Or restructure HTML to move fixed element outside transformed parent */
```

### Mistake 4: Content Jumping with Sticky

**Problem:** Content jumps when element becomes sticky because space is removed.

**Solution:**

```css
/* ✅ Add padding to parent or use placeholder */
.sticky-header {
	position: sticky;
	top: 0;
	/* Header has height of 60px */
}

/* Add padding to next element */
.content {
	padding-top: 60px; /* Match header height */
}
```

### Mistake 5: Absolute Element Overflowing Parent

**Problem:**

```css
.parent {
	position: relative;
	width: 300px;
	height: 200px;
}

.child {
	position: absolute;
	top: 0;
	left: 0;
	width: 400px; /* Wider than parent! */
}
```

**Solution:**

```css
.parent {
	position: relative;
	width: 300px;
	height: 200px;
	overflow: hidden; /* Clip overflowing content */
	/* Or use overflow: auto for scrollbars */
}
```

---

## 🏡 Homework Assignment

**Create a Landing Page with Layered Elements**

Build a landing page that demonstrates all positioning techniques learned:

**Requirements:**

1. **Fixed header navigation** that stays at top when scrolling
2. **Hero section** with absolutely positioned badge/tag in corner
3. **Sticky section headers** that stick while scrolling their section
4. **Tooltip** that appears on hover over certain text
5. **Back to top button** (fixed position, bottom-right)
6. **Modal dialog** that can be triggered by a button
7. Proper **z-index hierarchy** for all layered elements

**Bonus challenges:**

-   Add smooth scroll behavior
-   Animate modal entrance/exit
-   Create a notification badge on navigation
-   Implement a dropdown menu

**Deliverables:**

-   `landing-page.html` — Complete HTML structure
-   Inline or external CSS with all positioning styles
-   Comments explaining positioning choices
-   Test all interactive elements (modal, tooltips, etc.)

**Submission:** Create a folder `session-11-homework` with your files.

---

## 📚 Additional Resources

### Documentation

-   [MDN: position](https://developer.mozilla.org/en-US/docs/Web/CSS/position)
-   [MDN: z-index](https://developer.mozilla.org/en-US/docs/Web/CSS/z-index)
-   [MDN: Stacking Context](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_positioned_layout/Understanding_z-index/Stacking_context)
-   [CSS Tricks: position](https://css-tricks.com/almanac/properties/p/position/)
-   [CSS Tricks: Z-Index](https://css-tricks.com/almanac/properties/z/z-index/)

### Tutorials

-   [Learn CSS Positioning](https://ishadeed.com/article/learn-css-positioning/)
-   [CSS Position Sticky - How It Really Works!](https://www.youtube.com/watch?v=NzjU1GmKosQ)
-   [Understanding Z-Index](https://www.joshwcomeau.com/css/stacking-contexts/)

### Interactive Tools

-   [CSS Position Playground](https://codepen.io/search/pens?q=css+position+playground)
-   [Z-Index Visualizer](https://thirumanikandan.com/projects/z-index-visualizer)

---

## 🎉 Session Summary

Congratulations! You've mastered CSS positioning and layering. You can now:

✅ Use all five positioning values (`static`, `relative`, `absolute`, `fixed`, `sticky`)
✅ Position elements using offset properties (`top`, `right`, `bottom`, `left`)
✅ Center elements using multiple techniques
✅ Control stacking order with `z-index`
✅ Understand and work with stacking contexts
✅ Build common UI patterns (modals, tooltips, sticky headers)
✅ Debug positioning issues effectively

**Next session:** We'll explore multi-column layouts with floats and modern alternatives, building on your positioning knowledge to create complete page layouts!

---

**Navigation:**
← [Week 04 Session 10](session-10.md) | [Week 04 Index](../week-04.md) | [Session 12](session-12.md) →
