# Week 03 — Session 08: CSS Box Model & Styling

**Navigation:**
← [Session 07](session-07.md) | [Week 03 Index](../week-03.md) | [Session 09](session-09.md) →

---

**Session Length:** 90 minutes

## 📋 Pre-Class Checklist

Before starting this session, make sure you have:

-   ✅ Completed Session 07 (Introduction to CSS)
-   ✅ Understand CSS selectors (element, class, ID)
-   ✅ Know how to link external CSS files
-   ✅ Code editor (VS Code) with Live Server extension
-   ✅ Browser with Developer Tools (Chrome, Firefox, or Edge)
-   ✅ Create a new folder: `week-03-box-model`

## 🎯 Learning Objectives

By the end of this session, you will be able to:

-   Understand the CSS Box Model (content, padding, border, margin)
-   Apply width and height properties to elements
-   Use the `box-sizing` property effectively
-   Style backgrounds with colors, images, and gradients
-   Create and customize borders
-   Control spacing with margin and padding
-   Debug layout issues using Developer Tools

## 📦 Files for This Session

-   `session-08.md` — This tutorial (you're reading it!)
-   `box-model-template.html` — Starter file for practice
-   `box-model-solution.html` — Complete working example
-   `box-model-cheat-sheet.md` — Quick reference guide
-   `box-model-visual.html` — Interactive box model visualization

## 🔑 Key Terms

**Box Model**, **content**, **padding**, **border**, **margin**, **width**, **height**, **box-sizing**, **content-box**, **border-box**, **background**, **background-image**, **border-radius**, **spacing**, **Developer Tools**

## 🏗️ What You Will Build

-   A styled card component with proper spacing
-   A profile card with images and borders
-   A pricing table with box model principles
-   A button collection showcasing different styles

---

## Part 1: Understanding the Box Model (25 minutes)

### What is the Box Model?

Every HTML element is a **rectangular box**. The CSS Box Model describes how these boxes are structured and how space is calculated around them.

**The Four Parts of the Box Model:**

```
┌─────────────────────────────────────┐
│           MARGIN (transparent)       │
│  ┌───────────────────────────────┐  │
│  │     BORDER                    │  │
│  │  ┌─────────────────────────┐  │  │
│  │  │   PADDING               │  │  │
│  │  │  ┌───────────────────┐  │  │  │
│  │  │  │    CONTENT        │  │  │  │
│  │  │  │  (text, images)   │  │  │  │
│  │  │  └───────────────────┘  │  │  │
│  │  └─────────────────────────┘  │  │
│  └───────────────────────────────┘  │
└─────────────────────────────────────┘
```

**1. Content** — The actual content (text, images, etc.)
**2. Padding** — Space between content and border (transparent)
**3. Border** — Line around the padding and content
**4. Margin** — Space outside the border (transparent, pushes other elements away)

### Visualizing the Box Model

Let's create a simple example:

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<title>Box Model Demo</title>
		<style>
			.box {
				width: 200px;
				height: 100px;
				padding: 20px;
				border: 5px solid red;
				margin: 30px;
				background-color: lightblue;
			}
		</style>
	</head>
	<body>
		<div class="box">Content Area</div>
	</body>
</html>
```

**What's the total width of this box?**

-   Content: 200px
-   Padding: 20px × 2 (left + right) = 40px
-   Border: 5px × 2 (left + right) = 10px
-   **Total visible width: 250px**
-   Margin: 30px on each side (but doesn't count toward element width)

### Seeing the Box Model in Developer Tools

**Try this:**

1. Open the HTML above in your browser
2. Right-click the box and select "Inspect"
3. In Developer Tools, find the **Box Model diagram** (usually at the bottom)
4. Hover over different parts to see them highlighted

**You'll see:**

-   Blue = Content
-   Green = Padding
-   Yellow/Brown = Border
-   Orange = Margin

<details>
<summary>💡 Knowledge Check #1</summary>

**Question:** If an element has `width: 300px`, `padding: 10px`, and `border: 5px solid black`, what is the total width the element occupies?

**Answer:**

-   Content: 300px
-   Padding: 10px × 2 = 20px
-   Border: 5px × 2 = 10px
-   **Total: 330px**

(Margin doesn't count toward the element's width, it creates space around it)

</details>

### Box Model Properties Overview

```css
.element {
	/* Content area */
	width: 200px;
	height: 100px;

	/* Padding (space inside, around content) */
	padding: 20px;

	/* Border (line around padding and content) */
	border: 2px solid black;

	/* Margin (space outside, around element) */
	margin: 10px;

	/* Background (shows in content + padding) */
	background-color: lightgray;
}
```

**Important:** Background color/image shows in the **content + padding** area, but NOT in the margin.

---

## Part 2: Width, Height, and Box-Sizing (20 minutes)

### Width and Height

Set the size of the **content area**.

```css
.box {
	width: 300px;
	height: 200px;
}
```

**Units you can use:**

-   `px` — Pixels (fixed size)
-   `%` — Percentage of parent element
-   `em` — Relative to font size
-   `rem` — Relative to root font size
-   `vh/vw` — Viewport height/width
-   `auto` — Automatic (default)

**Examples:**

```css
.full-width {
	width: 100%; /* Takes full width of parent */
}

.half-height {
	height: 50vh; /* 50% of viewport height */
}

.fixed {
	width: 400px;
	height: 300px;
}
```

### Min and Max Dimensions

Control size boundaries:

```css
.responsive-box {
	width: 80%;
	max-width: 600px; /* Won't grow beyond 600px */
	min-width: 300px; /* Won't shrink below 300px */
}

.flexible-height {
	min-height: 200px; /* At least 200px tall */
	max-height: 500px; /* Won't grow beyond 500px */
}
```

**Use case:** Responsive design — element scales but has limits.

### The Box-Sizing Property

**Problem:** Calculating total width is confusing!

```css
.box {
	width: 300px;
	padding: 20px;
	border: 5px solid black;
	/* Total width = 300 + 20 + 20 + 5 + 5 = 350px */
}
```

**Solution:** Use `box-sizing: border-box`!

```css
.box {
	box-sizing: border-box;
	width: 300px;
	padding: 20px;
	border: 5px solid black;
	/* Total width = 300px (padding and border included!) */
}
```

### Content-Box vs. Border-Box

**`box-sizing: content-box` (default):**

-   Width/height applies to **content only**
-   Padding and border are **added** to the total size
-   Math is harder!

**`box-sizing: border-box` (recommended):**

-   Width/height includes **content + padding + border**
-   Total size is exactly what you specify
-   Math is easier!

**Visual comparison:**

```css
/* Both have width: 200px */

.content-box {
	box-sizing: content-box;
	width: 200px;
	padding: 20px;
	border: 10px solid black;
	/* Total width: 200 + 40 + 20 = 260px */
}

.border-box {
	box-sizing: border-box;
	width: 200px;
	padding: 20px;
	border: 10px solid black;
	/* Total width: 200px (includes everything!) */
}
```

### Best Practice: Apply to All Elements

Many developers use this at the start of their CSS:

```css
* {
	box-sizing: border-box;
}
```

Or more specifically:

```css
*,
*::before,
*::after {
	box-sizing: border-box;
}
```

<details>
<summary>💡 Knowledge Check #2</summary>

**Question:** You want a button that's exactly 150px wide including padding and border. Which box-sizing should you use?

**Answer:** `box-sizing: border-box;`

This way, when you set `width: 150px`, the total width including padding and border will be exactly 150px.

</details>

---

## Part 3: Padding and Margin (25 minutes)

### Padding Syntax

**Padding** creates space **inside** the element, between content and border.

**Individual sides:**

```css
.box {
	padding-top: 10px;
	padding-right: 20px;
	padding-bottom: 10px;
	padding-left: 20px;
}
```

**Shorthand (clockwise from top):**

```css
/* All sides */
padding: 20px;

/* Vertical | Horizontal */
padding: 10px 20px;

/* Top | Horizontal | Bottom */
padding: 10px 20px 15px;

/* Top | Right | Bottom | Left (clockwise) */
padding: 10px 20px 15px 25px;
```

**Memory trick:** TRouBLe (Top, Right, Bottom, Left) — goes clockwise!

**Common patterns:**

```css
/* Equal all around */
padding: 20px;

/* More top/bottom than sides */
padding: 20px 10px;

/* Different on each side */
padding: 10px 15px 20px 15px;
```

### Margin Syntax

**Margin** creates space **outside** the element, pushing other elements away.

**Same syntax as padding:**

```css
/* All sides */
margin: 20px;

/* Vertical | Horizontal */
margin: 10px 20px;

/* Top | Right | Bottom | Left */
margin: 10px 20px 15px 25px;
```

**Centering with auto:**

```css
.centered {
	width: 600px;
	margin: 0 auto; /* Top/bottom: 0, Left/right: auto */
	/* This centers the element horizontally! */
}
```

### Padding vs. Margin: When to Use Which?

| Use Padding When...                     | Use Margin When...                  |
| --------------------------------------- | ----------------------------------- |
| Creating space inside an element        | Creating space between elements     |
| Expanding clickable area                | Separating elements from each other |
| Adding space around content             | Centering elements                  |
| Background should extend into the space | Creating gaps in layouts            |

**Example showing the difference:**

```html
<style>
	.with-padding {
		background-color: lightblue;
		padding: 20px;
		/* Background extends into padding */
	}

	.with-margin {
		background-color: lightcoral;
		margin: 20px;
		/* Background doesn't extend into margin */
	}
</style>

<div class="with-padding">I have padding (blue extends)</div>
<div class="with-margin">I have margin (coral doesn't extend)</div>
```

### Margin Collapse

**Important concept:** Vertical margins between elements **collapse**!

```html
<style>
	.box1 {
		margin-bottom: 30px;
	}

	.box2 {
		margin-top: 20px;
	}
</style>

<div class="box1">First box</div>
<div class="box2">Second box</div>
<!-- Gap between them is 30px, NOT 50px! -->
<!-- The larger margin "wins" -->
```

**Key points:**

-   Only **vertical** margins collapse (not horizontal)
-   The **larger** margin value is used
-   Padding does NOT collapse

<details>
<summary>💡 Knowledge Check #3</summary>

**Question:** Two paragraphs have `margin-bottom: 20px` and `margin-top: 20px`. How much space is between them?

**Answer:** 20px, not 40px! Vertical margins collapse, so the larger value (both are 20px) is used.

</details>

### Negative Margins

You can use negative values to pull elements closer or overlap them:

```css
.overlap {
	margin-top: -20px; /* Pulls element up */
}

.pull-left {
	margin-left: -10px; /* Pulls element left */
}
```

**Use carefully** — can create overlapping content!

---

## Part 4: Borders (15 minutes)

### Border Basics

Borders go around padding and content.

**Full syntax:**

```css
border: width style color;
```

**Example:**

```css
.box {
	border: 2px solid black;
}
```

### Border Width

```css
border-width: 1px;
border-width: thin; /* Predefined value */
border-width: medium; /* Predefined value */
border-width: thick; /* Predefined value */
```

### Border Style

**Required property** — without it, border won't show!

```css
border-style: solid;
border-style: dashed;
border-style: dotted;
border-style: double;
border-style: groove;
border-style: ridge;
border-style: inset;
border-style: outset;
border-style: none;
border-style: hidden;
```

**Visual examples:**

```css
.solid {
	border: 3px solid black;
}
.dashed {
	border: 3px dashed black;
}
.dotted {
	border: 3px dotted black;
}
.double {
	border: 5px double black;
}
```

### Border Color

```css
border-color: red;
border-color: #333;
border-color: rgb(100, 100, 100);
border-color: rgba(0, 0, 0, 0.5); /* Semi-transparent */
```

### Individual Sides

```css
/* Individual properties */
border-top: 2px solid red;
border-right: 1px dashed blue;
border-bottom: 3px dotted green;
border-left: 2px solid black;

/* Or specific aspects */
border-top-width: 3px;
border-right-style: dashed;
border-bottom-color: red;
```

### Border Radius (Rounded Corners)

Make corners rounded:

```css
/* All corners */
border-radius: 10px;

/* Oval/ellipse */
border-radius: 50px / 25px;

/* Individual corners */
border-radius: 10px 20px 30px 40px;

/* Circle */
border-radius: 50%;
```

**Common uses:**

```css
/* Subtle rounding */
.card {
	border-radius: 5px;
}

/* Pills/buttons */
.button {
	border-radius: 25px;
}

/* Circle (for square elements) */
.avatar {
	width: 100px;
	height: 100px;
	border-radius: 50%;
}
```

<details>
<summary>💡 Knowledge Check #4</summary>

**Question:** What's wrong with this CSS?

```css
.box {
	border-width: 2px;
	border-color: red;
}
```

**Answer:** It's missing `border-style`! Without a style, the border won't appear. Should add: `border-style: solid;`

</details>

---

## Part 5: Backgrounds (20 minutes)

### Background Color

```css
.box {
	background-color: lightblue;
	background-color: #f0f0f0;
	background-color: rgb(240, 240, 240);
	background-color: rgba(0, 0, 0, 0.1); /* Semi-transparent */
}
```

### Background Image

```css
.hero {
	background-image: url('images/background.jpg');
}
```

### Background Properties

**Complete control over background images:**

```css
.element {
	background-image: url('pattern.png');
	background-repeat: no-repeat; /* no-repeat, repeat, repeat-x, repeat-y */
	background-position: center center; /* horizontal vertical */
	background-size: cover; /* cover, contain, 100px 200px, 50% */
	background-attachment: fixed; /* scroll, fixed */
}
```

**Shorthand:**

```css
background: color image repeat position / size;

/* Example */
background: lightblue url('bg.jpg') no-repeat center / cover;
```

### Background Size

```css
/* Keywords */
background-size: cover; /* Covers entire area, may crop */
background-size: contain; /* Fits entire image, may have empty space */

/* Specific values */
background-size: 100px 200px; /* Width height */
background-size: 50%; /* Percentage of container */
```

**`cover` vs `contain`:**

-   **`cover`** — Image fills entire container, may be cropped
-   **`contain`** — Entire image is visible, may have empty space

### Background Position

Position the background image:

```css
/* Keywords */
background-position: top left;
background-position: center center;
background-position: bottom right;

/* Percentages */
background-position: 50% 50%; /* Center */

/* Pixels */
background-position: 20px 40px;

/* Mix */
background-position: center 20px; /* Centered horizontally, 20px from top */
```

### Multiple Backgrounds

Layer multiple backgrounds:

```css
.element {
	background: url('foreground.png') no-repeat center, url('background.jpg')
			no-repeat center / cover;
}
```

### Gradient Backgrounds

Create color gradients:

```css
/* Linear gradient */
background: linear-gradient(to right, red, yellow);
background: linear-gradient(45deg, #667eea 0%, #764ba2 100%);

/* Radial gradient */
background: radial-gradient(circle, red, yellow);
```

**Common gradient patterns:**

```css
/* Top to bottom */
background: linear-gradient(to bottom, #667eea, #764ba2);

/* Diagonal */
background: linear-gradient(135deg, #667eea, #764ba2);

/* Multiple colors */
background: linear-gradient(to right, red, yellow, green, blue);

/* With color stops */
background: linear-gradient(to right, red 0%, yellow 33%, green 66%, blue 100%);
```

---

## 🛠️ Hands-On Practice (Remaining Time)

### Exercise 1: Profile Card (20 minutes)

Create a profile card demonstrating the box model:

**Requirements:**

-   Card container with padding, border, and margin
-   Background color for the card
-   Profile image (use border-radius to make it circular)
-   Name and title with appropriate spacing
-   Social media buttons with padding and borders
-   Use `box-sizing: border-box`

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
		<title>Profile Card</title>
		<style>
			* {
				box-sizing: border-box;
			}

			body {
				font-family: Arial, sans-serif;
				background-color: #f0f0f0;
				padding: 40px;
			}

			/* Add your CSS here */
		</style>
	</head>
	<body>
		<div class="profile-card">
			<img
				src="https://via.placeholder.com/150"
				alt="Profile"
				class="profile-img"
			/>
			<h2 class="name">Jane Doe</h2>
			<p class="title">Web Developer</p>
			<p class="bio">
				Passionate about creating beautiful and functional websites.
			</p>
			<div class="social-buttons">
				<button class="btn">Twitter</button>
				<button class="btn">LinkedIn</button>
				<button class="btn">GitHub</button>
			</div>
		</div>
	</body>
</html>
```

**Your task:** Add CSS to style the profile card!

<details>
<summary>💡 Solution</summary>

```css
* {
	box-sizing: border-box;
}

body {
	font-family: Arial, sans-serif;
	background-color: #f0f0f0;
	padding: 40px;
}

.profile-card {
	max-width: 400px;
	margin: 0 auto;
	background-color: white;
	padding: 30px;
	border: 1px solid #ddd;
	border-radius: 10px;
	text-align: center;
	box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.profile-img {
	width: 150px;
	height: 150px;
	border-radius: 50%;
	border: 5px solid #667eea;
	margin-bottom: 20px;
}

.name {
	margin: 0 0 5px 0;
	color: #333;
	font-size: 24px;
}

.title {
	margin: 0 0 15px 0;
	color: #666;
	font-size: 16px;
	font-style: italic;
}

.bio {
	margin: 0 0 25px 0;
	color: #555;
	line-height: 1.6;
}

.social-buttons {
	display: flex;
	gap: 10px;
	justify-content: center;
}

.btn {
	padding: 10px 20px;
	background-color: #667eea;
	color: white;
	border: none;
	border-radius: 5px;
	cursor: pointer;
	font-size: 14px;
}

.btn:hover {
	background-color: #5568d3;
}
```

</details>

### Exercise 2: Pricing Cards (20 minutes)

Create three pricing cards side by side:

**Requirements:**

-   Three cards: Basic, Pro, Premium
-   Each card has padding, border, and background
-   Different border colors for each tier
-   Highlight the "Pro" card (different background, larger, etc.)
-   Price in large text
-   List of features
-   "Sign Up" button with padding and border-radius

<details>
<summary>💡 Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<title>Pricing Cards</title>
		<style>
			* {
				box-sizing: border-box;
			}

			body {
				font-family: Arial, sans-serif;
				background-color: #f5f5f5;
				padding: 40px;
			}

			.pricing-container {
				max-width: 1000px;
				margin: 0 auto;
				display: flex;
				gap: 20px;
				justify-content: center;
			}

			.pricing-card {
				flex: 1;
				background-color: white;
				padding: 30px;
				border: 2px solid #ddd;
				border-radius: 8px;
				text-align: center;
			}

			.pricing-card.featured {
				border-color: #667eea;
				background-color: #f8f9ff;
				transform: scale(1.05);
				box-shadow: 0 4px 20px rgba(102, 126, 234, 0.2);
			}

			.plan-name {
				margin: 0 0 10px 0;
				font-size: 24px;
				color: #333;
			}

			.price {
				font-size: 48px;
				font-weight: bold;
				color: #667eea;
				margin: 20px 0;
			}

			.price span {
				font-size: 18px;
				color: #666;
			}

			.features {
				list-style: none;
				padding: 0;
				margin: 20px 0;
			}

			.features li {
				padding: 10px 0;
				border-bottom: 1px solid #eee;
			}

			.signup-btn {
				width: 100%;
				padding: 15px;
				background-color: #667eea;
				color: white;
				border: none;
				border-radius: 5px;
				font-size: 16px;
				cursor: pointer;
				margin-top: 20px;
			}

			.signup-btn:hover {
				background-color: #5568d3;
			}
		</style>
	</head>
	<body>
		<div class="pricing-container">
			<div class="pricing-card">
				<h3 class="plan-name">Basic</h3>
				<div class="price">$9<span>/mo</span></div>
				<ul class="features">
					<li>10 Projects</li>
					<li>5GB Storage</li>
					<li>Email Support</li>
					<li>Basic Features</li>
				</ul>
				<button class="signup-btn">Sign Up</button>
			</div>

			<div class="pricing-card featured">
				<h3 class="plan-name">Pro</h3>
				<div class="price">$29<span>/mo</span></div>
				<ul class="features">
					<li>Unlimited Projects</li>
					<li>50GB Storage</li>
					<li>Priority Support</li>
					<li>Advanced Features</li>
				</ul>
				<button class="signup-btn">Sign Up</button>
			</div>

			<div class="pricing-card">
				<h3 class="plan-name">Premium</h3>
				<div class="price">$99<span>/mo</span></div>
				<ul class="features">
					<li>Unlimited Everything</li>
					<li>500GB Storage</li>
					<li>24/7 Phone Support</li>
					<li>All Features</li>
				</ul>
				<button class="signup-btn">Sign Up</button>
			</div>
		</div>
	</body>
</html>
```

</details>

---

## 🐛 Common Mistakes & Troubleshooting

### Mistake 1: Forgetting Box-Sizing

```css
/* ❌ PROBLEM: Element is wider than expected */
.box {
	width: 300px;
	padding: 20px;
	border: 5px solid black;
	/* Total width: 350px! */
}

/* ✅ SOLUTION: Use border-box */
.box {
	box-sizing: border-box;
	width: 300px;
	padding: 20px;
	border: 5px solid black;
	/* Total width: 300px */
}
```

### Mistake 2: Confusing Padding and Margin

```css
/* ❌ WRONG: Using margin when you want background color to extend */
.button {
	background-color: blue;
	margin: 20px; /* Background won't extend into margin! */
}

/* ✅ CORRECT: Use padding for space inside */
.button {
	background-color: blue;
	padding: 20px; /* Background extends into padding */
}
```

### Mistake 3: Missing Border Style

```css
/* ❌ WRONG: Border won't show */
.box {
	border-width: 2px;
	border-color: red;
}

/* ✅ CORRECT: Include style */
.box {
	border: 2px solid red;
}
```

### Mistake 4: Margin Auto on Inline Elements

```css
/* ❌ WRONG: Won't center */
span {
	margin: 0 auto; /* Doesn't work on inline elements */
}

/* ✅ CORRECT: Make it block or inline-block first */
span {
	display: block; /* or inline-block */
	margin: 0 auto;
}
```

### Debugging with Developer Tools

**Steps to debug box model issues:**

1. Right-click element → Inspect
2. Look at the **Box Model** diagram (usually bottom-right)
3. Check each layer: margin, border, padding, content
4. Hover over the diagram to see each layer highlighted
5. Edit values in DevTools to test fixes

**Common issues to check:**

-   ✅ Is `box-sizing` set correctly?
-   ✅ Are margins collapsing unexpectedly?
-   ✅ Is padding adding unexpected width?
-   ✅ Is `border-style` set?

---

## 📝 Homework Assignment

Create a **"Product Showcase Page"** with three product cards:

**Content requirements:**

-   Page header with title and description
-   Three product cards side by side:
    -   Product image (use placeholder images)
    -   Product name
    -   Price
    -   Short description
    -   "Add to Cart" button
-   Footer with copyright information

**Styling requirements:**

-   Use `box-sizing: border-box` for all elements
-   Each card should have:
    -   Padding around content
    -   Border with border-radius
    -   Background color
    -   Margin between cards
-   Images should be circular or have rounded corners
-   Buttons should have padding, border-radius, and hover effects
-   Use consistent spacing throughout
-   Add a subtle background color to the page

**Bonus challenges:**

-   Add a "featured" card that stands out (different border, shadow, etc.)
-   Use a background gradient on one element
-   Add a semi-transparent overlay on images
-   Create a "sale badge" using absolute positioning (preview for next session!)

---

## 🔍 What We Covered

✅ The CSS Box Model (content, padding, border, margin)
✅ Width and height properties
✅ Box-sizing property (content-box vs border-box)
✅ Padding and margin syntax and usage
✅ Margin collapse behavior
✅ Border styles, widths, colors, and border-radius
✅ Background colors, images, and gradients
✅ Using Developer Tools to debug layout issues

---

## 📚 Additional Resources

**Official Documentation:**

-   [MDN: The Box Model](https://developer.mozilla.org/docs/Learn/CSS/Building_blocks/The_box_model)
-   [MDN: Box-sizing](https://developer.mozilla.org/docs/Web/CSS/box-sizing)
-   [MDN: Backgrounds and Borders](https://developer.mozilla.org/docs/Learn/CSS/Building_blocks/Backgrounds_and_borders)

**Interactive Learning:**

-   [CSS Box Model Interactive](https://www.w3schools.com/css/css_boxmodel.asp)
-   [Box-sizing Explained](https://css-tricks.com/box-sizing/)

**Tools:**

-   [CSS Border Radius Generator](https://border-radius.com/)
-   [Gradient Generator](https://cssgradient.io/)
-   Browser Developer Tools (F12)

**Practice:**

-   [Flexbox Froggy](https://flexboxfroggy.com/) - While focused on flexbox, it reinforces box model concepts
-   [CSS Diner](https://flukeout.github.io/) - Selector practice

---

## 🎯 Next Session Preview

In **Session 09: CSS Positioning & Basic Layout**, you'll learn:

-   CSS positioning (static, relative, absolute, fixed, sticky)
-   Display properties (block, inline, inline-block)
-   Float and clear
-   Creating simple layouts
-   Z-index and stacking contexts

**Preparation:** Make sure you understand the box model thoroughly — it's the foundation for positioning and layout!

---

**Navigation:**
← [Session 07](session-07.md) | [Week 03 Index](../week-03.md) | [Session 09](session-09.md) →
