# Week 06 — Session 16: Responsive Design & Media Queries

**Navigation:**
← [Week 05 Session 15](../week-05/session-15.md) | [Week 06 Index](../week-06.md) | [Session 17](session-17.md) →

---

**Session Length:** 90 minutes

## 📋 Pre-Class Checklist

Before starting this session, make sure you have:

-   ✅ Completed Week 05 (Flexbox and Mini Project 1)
-   ✅ Basic understanding of CSS layout
-   ✅ Browser with Developer Tools
-   ✅ Code editor (VS Code)

## 🎯 Learning Objectives

By the end of this session, you will be able to:

-   Understand the core principles of Responsive Web Design (RWD)
-   Use the viewport meta tag correctly
-   Write media queries to target different screen sizes
-   Implement mobile-first and desktop-first design strategies
-   Identify and use common device breakpoints

## 🔑 Key Terms

**Responsive Design**, **Viewport**, **Media Queries**, **Breakpoints**, **Mobile-First**, **Desktop-First**, **Fluid Layouts**, **Flexible Images**

---

## Part 1: Introduction to Responsive Design (15 minutes)

### What is Responsive Web Design (RWD)?

**Responsive Web Design** is an approach to web development that makes web pages render well on a variety of devices and window or screen sizes.

**The three core ingredients of RWD:**

1.  **Fluid Grids:** Using relative units like `%`, `vh`, `vw`, or `fr` instead of fixed units like `px`.
2.  **Flexible Images:** Ensuring images don't overflow their containers (e.g., `max-width: 100%`).
3.  **Media Queries:** Applying different styles based on the device's characteristics (like screen width).

### Why do we need it?

In the early days of the web, designers built sites for a fixed width (usually 960px). Today, users access the web from smartphones, tablets, laptops, and massive 4K monitors. A single, fixed-width design cannot provide a good experience on all these devices.

---

## Part 2: The Viewport Meta Tag (10 minutes)

To make a website responsive, you **must** include the viewport meta tag in the `<head>` of your HTML.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

**What it does:**
-   `width=device-width`: Sets the width of the page to follow the screen-width of the device.
-   `initial-scale=1.0`: Sets the initial zoom level when the page is first loaded.

**Without this tag, mobile browsers will assume the page is a desktop-sized site and try to "zoom out" to fit it all on the screen, making the text tiny and unreadable.**

---

## Part 3: Media Queries Fundamentals (25 minutes)

Media queries allow you to apply CSS only when certain conditions are met.

### Syntax

```css
@media media-type and (media-feature) {
	/* CSS rules go here */
}
```

-   **media-type:** Usually `screen`, `print`, or `all`.
-   **media-feature:** The condition to check (e.g., `max-width: 600px`).

### Common Examples

```css
/* Apply styles when the screen is 768px wide or SMALLER */
@media screen and (max-width: 768px) {
	.container {
		flex-direction: column;
	}
}

/* Apply styles when the screen is 1024px wide or LARGER */
@media screen and (min-width: 1024px) {
	.header {
		padding: 40px;
	}
}
```

### Logical Operators

-   `and`: Combines multiple conditions (e.g., `(min-width: 600px) and (max-width: 900px)`).
-   `not`: Negates a condition.
-   `,`: Acts like an `OR` operator.

---

## Part 4: Design Strategies (20 minutes)

### Mobile-First vs. Desktop-First

#### 1. Mobile-First (Recommended)
You write styles for the smallest screens first (natural CSS), then use `min-width` media queries to add complexity for larger screens.

```css
/* Base styles (Mobile) */
.nav {
	display: none; /* Hide nav by default on mobile */
}

/* Desktop Styles */
@media screen and (min-width: 768px) {
	.nav {
		display: flex; /* Show nav as flexbox on tablets/desktops */
	}
}
```

#### 2. Desktop-First
You write styles for large screens first, then use `max-width` media queries to "fix" or simplify the layout for smaller screens.

```css
/* Base styles (Desktop) */
.nav {
	display: flex;
}

/* Mobile Styles */
@media screen and (max-width: 767px) {
	.nav {
		display: none;
	}
}
```

**Why Mobile-First is better:**
-   Encourages simpler, cleaner code.
-   Better performance (mobile devices don't download desktop-heavy CSS).
-   Forces you to prioritize content.

### Common Breakpoints

While you should design based on your content, these are common industry standards:
-   **Mobile:** 0 - 480px
-   **Tablets:** 481px - 768px
-   **Laptops:** 769px - 1024px
-   **Desktops:** 1025px - 1200px
-   **Large Screens:** 1201px+

---

## 🎨 Hands-On Exercise: Responsive Card Layout

**Goal:** Create a grid of cards that shows 1 column on mobile, 2 on tablet, and 3 on desktop.

**Starter Code:**
```html
<div class="card-grid">
  <div class="card">1</div>
  <div class="card">2</div>
  <div class="card">3</div>
  <div class="card">4</div>
  <div class="card">5</div>
  <div class="card">6</div>
</div>
```

**Instruction:** Fill in the CSS using a **Mobile-First** approach.

<details>
<summary>✅ Solution</summary>

```css
/* Mobile-First Base Styles */
.card-grid {
    display: grid;
    grid-template-columns: 1fr; /* 1 column */
    gap: 20px;
    padding: 20px;
}

/* Tablet (min-width 600px) */
@media screen and (min-width: 600px) {
    .card-grid {
        grid-template-columns: 1fr 1fr; /* 2 columns */
    }
}

/* Desktop (min-width 1024px) */
@media screen and (min-width: 1024px) {
    .card-grid {
        grid-template-columns: 1fr 1fr 1fr; /* 3 columns */
    }
}

.card {
    background: #f0f0f0;
    padding: 40px;
    text-align: center;
    border-radius: 8px;
    font-size: 2rem;
}
```
</details>

---

## 🏡 Homework Assignment

**Make Your Portfolio Responsive**

Take the portfolio we've been building and:
1.  Add the viewport meta tag.
2.  Use a Mobile-First approach.
3.  Ensure your navigation turns into a "hamburger menu" (styled-only, no JS needed yet) or a simplified list on mobile.
4.  Ensure your features/skills/projects sections use flexible grids.

---

**Navigation:**
← [Week 05 Session 15](../week-05/session-15.md) | [Week 06 Index](../week-06.md) | [Session 17](session-17.md) →
