# Week 03 — Session 09: CSS Positioning & Basic Layout

**Navigation:**
← [Session 08](session-08.md) | [Week 03 Index](../week-03.md) | [Week 04 Session 10](../../week-04/session-10.md) →

---

**Session Length:** 90 minutes

## 📋 Pre-Class Checklist

Before starting this session, make sure you have:

-   ✅ Completed Sessions 07 and 08 (CSS basics and box model)
-   ✅ Understand the box model (margin, padding, border, content)
-   ✅ Know how to use CSS selectors and properties
-   ✅ Code editor (VS Code) with Live Server extension
-   ✅ Browser with Developer Tools (Chrome, Firefox, or Edge)
-   ✅ Create a new folder: `week-03-positioning`

## 🎯 Learning Objectives

By the end of this session, you will be able to:

-   Understand CSS positioning (static, relative, absolute, fixed, sticky)
-   Use the `display` property (block, inline, inline-block, none)
-   Control element flow with float and clear
-   Use z-index to layer elements
-   Create simple page layouts
-   Position elements precisely on the page
-   Build common UI patterns (sticky headers, overlays, tooltips)

## 📦 Files for This Session

-   `session-09.md` — This tutorial (you're reading it!)
-   `positioning-template.html` — Starter file for practice
-   `positioning-solution.html` — Complete working example
-   `positioning-cheat-sheet.md` — Quick reference guide
-   `positioning-visual.html` — Interactive positioning demonstration

## 🔑 Key Terms

**position**, **static**, **relative**, **absolute**, **fixed**, **sticky**, **display**, **block**, **inline**, **inline-block**, **float**, **clear**, **z-index**, **stacking context**, **top**, **right**, **bottom**, **left**, **overflow**

## 🏗️ What You Will Build

-   A sticky navigation header
-   A modal/dialog overlay
-   A card layout with positioned badges
-   A sidebar layout using float
-   A tooltip component

---

## Part 1: The Display Property (20 minutes)

### Understanding Display

The `display` property controls how an element is displayed and how it interacts with other elements.

### Block Elements

**Block-level elements:**

-   Take up the **full width** available
-   Always start on a **new line**
-   Can have width and height set
-   Stack vertically

**Default block elements:** `<div>`, `<p>`, `<h1>`-`<h6>`, `<ul>`, `<li>`, `<header>`, `<footer>`, `<section>`

```css
.block-element {
    display: block;
    width: 300px;
    height: 100px;
    background-color: lightblue;
    margin-bottom: 10px;
}
```

```html
<div class="block-element">Block 1</div>
<div class="block-element">Block 2</div>
<div class="block-element">Block 3</div>
<!-- Each takes full width and stacks vertically -->
```

### Inline Elements

**Inline elements:**

-   Take up only as much width as needed
-   Do **not** start on a new line
-   **Cannot** have width and height set
-   Flow horizontally with text

**Default inline elements:** `<span>`, `<a>`, `<strong>`, `<em>`, `<img>`, `<button>`

```css
.inline-element {
    display: inline;
    background-color: yellow;
    /* width and height are ignored! */
}
```

```html
<span class="inline-element">Inline 1</span>
<span class="inline-element">Inline 2</span>
<span class="inline-element">Inline 3</span>
<!-- They flow horizontally like words in a sentence -->
```

### Inline-Block (Best of Both Worlds)

**Inline-block elements:**

-   Flow horizontally like inline elements
-   **Can** have width and height like block elements
-   Useful for creating horizontal layouts

```css
.inline-block-element {
    display: inline-block;
    width: 150px;
    height: 100px;
    background-color: lightcoral;
    margin-right: 10px;
}
```

```html
<div class="inline-block-element">Box 1</div>
<div class="inline-block-element">Box 2</div>
<div class="inline-block-element">Box 3</div>
<!-- They sit side by side but you can set their dimensions -->
```

### Display: None

Completely removes the element from the page (doesn't take up space).

```css
.hidden {
    display: none;
}
```

**Comparison with `visibility: hidden`:**

```css
/* Takes up space but is invisible */
.invisible {
    visibility: hidden;
}

/* Doesn't take up space at all */
.hidden {
    display: none;
}
```

### Common Display Values Summary

| Value          | Behavior                                   | Width/Height | New Line |
|----------------|---------------------------------------------|--------------|----------|
| `block`        | Full width, stacks vertically               | ✅ Yes       | ✅ Yes   |
| `inline`       | Only content width, flows horizontally      | ❌ No        | ❌ No    |
| `inline-block` | Flows horizontally but can have dimensions  | ✅ Yes       | ❌ No    |
| `none`         | Hidden, takes no space                      | ❌ No        | N/A      |

<details>
<summary>💡 Knowledge Check #1</summary>

**Question:** You want three boxes to sit side by side, each with a specific width and height. Which display value should you use?

**Answer:** `display: inline-block;`

This allows elements to flow horizontally (like inline) while still accepting width and height (like block).

</details>

---

## Part 2: CSS Positioning Basics (25 minutes)

### The Position Property

The `position` property determines how an element is positioned in the document.

**Five position values:**

1. `static` (default)
2. `relative`
3. `absolute`
4. `fixed`
5. `sticky`

### Position: Static (Default)

Elements are positioned according to the normal document flow.

```css
.static-element {
    position: static;
    /* This is the default - usually not needed */
}
```

**Key points:**

-   Default positioning for all elements
-   `top`, `right`, `bottom`, `left`, and `z-index` have **no effect**
-   Elements appear in order in the document

### Position: Relative

Element is positioned **relative to its normal position**.

```css
.relative-box {
    position: relative;
    top: 20px;      /* Moves 20px DOWN from normal position */
    left: 30px;     /* Moves 30px RIGHT from normal position */
}
```

**Key points:**

-   Original space is **still reserved** (other elements don't move)
-   Use `top`, `right`, `bottom`, `left` to offset from normal position
-   Often used as a positioning context for absolute children

**Example:**

```html
<style>
    .box {
        width: 100px;
        height: 100px;
        background-color: lightblue;
        margin: 10px;
        display: inline-block;
    }
    
    .relative {
        position: relative;
        top: 20px;
        left: 20px;
        background-color: lightcoral;
    }
</style>

<div class="box">Box 1</div>
<div class="box relative">Box 2 (Relative)</div>
<div class="box">Box 3</div>
<!-- Box 2 shifts, but Box 3 stays in its original position -->
```

### Position: Absolute

Element is removed from normal document flow and positioned relative to its **nearest positioned ancestor** (any parent with `position` other than `static`).

```css
.container {
    position: relative;  /* Creates positioning context */
    width: 400px;
    height: 300px;
    background-color: lightgray;
}

.absolute-box {
    position: absolute;
    top: 20px;      /* 20px from top of .container */
    right: 20px;    /* 20px from right of .container */
    width: 100px;
    height: 100px;
    background-color: red;
}
```

**Key points:**

-   Removed from normal flow (other elements act like it doesn't exist)
-   Positioned relative to nearest positioned ancestor
-   If no positioned ancestor, positioned relative to `<body>`
-   Use `top`, `right`, `bottom`, `left` to position

**Common use cases:**

-   Dropdown menus
-   Tooltips
-   Badge notifications
-   Modal overlays
-   Image captions

**Example: Badge on a Card**

```html
<style>
    .card {
        position: relative;
        width: 300px;
        padding: 20px;
        border: 1px solid #ddd;
        border-radius: 8px;
    }
    
    .badge {
        position: absolute;
        top: 10px;
        right: 10px;
        background-color: red;
        color: white;
        padding: 5px 10px;
        border-radius: 12px;
        font-size: 12px;
    }
</style>

<div class="card">
    <div class="badge">NEW</div>
    <h3>Product Title</h3>
    <p>Product description goes here...</p>
</div>
```

<details>
<summary>💡 Knowledge Check #2</summary>

**Question:** You have a card with `position: relative` and a badge inside with `position: absolute; top: 0; right: 0;`. Where does the badge appear?

**Answer:** In the **top-right corner of the card**.

The badge is positioned absolutely relative to its nearest positioned ancestor (the card with `position: relative`).

</details>

### Position: Fixed

Element is positioned relative to the **viewport** (browser window). It stays in place when you scroll.

```css
.fixed-header {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    background-color: #333;
    color: white;
    padding: 20px;
    z-index: 1000;
}
```

**Key points:**

-   Removed from normal document flow
-   Positioned relative to viewport (browser window)
-   Stays in same position when scrolling
-   Use `top`, `right`, `bottom`, `left` to position

**Common use cases:**

-   Fixed navigation headers
-   "Back to top" buttons
-   Cookie consent banners
-   Chat widgets

**Example: Fixed Navigation**

```html
<style>
    body {
        margin: 0;
        padding-top: 60px; /* Space for fixed header */
    }
    
    .fixed-nav {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 60px;
        background-color: #333;
        color: white;
        display: flex;
        align-items: center;
        padding: 0 20px;
        z-index: 1000;
    }
    
    .content {
        height: 2000px; /* Long content to scroll */
    }
</style>

<nav class="fixed-nav">
    <h1>My Website</h1>
</nav>
<div class="content">
    <p>Scroll down and the header stays at the top!</p>
</div>
```

### Position: Sticky

A hybrid of `relative` and `fixed`. Element is relative until you scroll to a threshold, then it becomes fixed.

```css
.sticky-header {
    position: sticky;
    top: 0;  /* Stick to top when you scroll to it */
    background-color: white;
    padding: 10px;
    border-bottom: 2px solid #333;
}
```

**Key points:**

-   Acts like `relative` until scroll threshold is reached
-   Then acts like `fixed` within its container
-   Requires a threshold (`top`, `bottom`, etc.)
-   Stays within parent container

**Common use cases:**

-   Sticky table headers
-   Section headings that stick when scrolling
-   Sidebars that follow you partway down the page

**Example: Sticky Section Headers**

```html
<style>
    .section-header {
        position: sticky;
        top: 0;
        background-color: #f0f0f0;
        padding: 10px;
        font-weight: bold;
        border-bottom: 2px solid #333;
    }
    
    .section-content {
        height: 400px;
        padding: 20px;
    }
</style>

<div>
    <h2 class="section-header">Section 1</h2>
    <div class="section-content">Content for section 1...</div>
    
    <h2 class="section-header">Section 2</h2>
    <div class="section-content">Content for section 2...</div>
    
    <h2 class="section-header">Section 3</h2>
    <div class="section-content">Content for section 3...</div>
</div>
```

### Position Values Summary

| Value      | Flow          | Relative To                        | Scrolls | Common Use                |
|------------|---------------|------------------------------------|---------|---------------------------|
| `static`   | Normal        | Normal flow                        | ✅ Yes  | Default                   |
| `relative` | Normal (space reserved) | Its normal position     | ✅ Yes  | Minor adjustments, context|
| `absolute` | Removed       | Nearest positioned ancestor        | ✅ Yes  | Tooltips, badges, dropdowns|
| `fixed`    | Removed       | Viewport (browser window)          | ❌ No   | Fixed headers, modals     |
| `sticky`   | Hybrid        | Container + viewport               | Hybrid  | Sticky headers, sidebars  |

---

## Part 3: Positioning Properties and Z-Index (20 minutes)

### Top, Right, Bottom, Left

These properties work with `position: relative`, `absolute`, `fixed`, and `sticky`.

```css
.positioned {
    position: absolute;
    top: 20px;      /* Distance from top */
    right: 30px;    /* Distance from right */
    bottom: 40px;   /* Distance from bottom */
    left: 50px;     /* Distance from left */
}
```

**Important:** You typically use **either** `top` or `bottom`, **either** `left` or `right`, not both.

**Common patterns:**

```css
/* Top-right corner */
.top-right {
    position: absolute;
    top: 0;
    right: 0;
}

/* Bottom-left corner */
.bottom-left {
    position: absolute;
    bottom: 0;
    left: 0;
}

/* Centered (with transform) */
.centered {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}

/* Full coverage */
.overlay {
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    /* Or use: width: 100%; height: 100%; */
}
```

### Z-Index (Stacking Order)

Controls which elements appear on top when they overlap.

```css
.element1 {
    position: relative;
    z-index: 1;
}

.element2 {
    position: relative;
    z-index: 2;  /* This appears on top */
}

.element3 {
    position: relative;
    z-index: 3;  /* This appears on top of both */
}
```

**Key points:**

-   Only works on **positioned** elements (`position` other than `static`)
-   Higher number = on top
-   Can be negative
-   Default is `auto` (stacking order = order in HTML)

**Common z-index values:**

```css
/* Typical z-index scale */
.dropdown { z-index: 100; }
.modal-backdrop { z-index: 1000; }
.modal { z-index: 1001; }
.tooltip { z-index: 1500; }
.notification { z-index: 2000; }
```

**Example: Modal Overlay**

```html
<style>
    .modal-backdrop {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.5);
        z-index: 1000;
    }
    
    .modal {
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background-color: white;
        padding: 30px;
        border-radius: 8px;
        z-index: 1001; /* Above backdrop */
        box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
    }
</style>

<div class="modal-backdrop"></div>
<div class="modal">
    <h2>Modal Title</h2>
    <p>Modal content goes here...</p>
    <button>Close</button>
</div>
```

<details>
<summary>💡 Knowledge Check #3</summary>

**Question:** You have a dropdown menu (`z-index: 100`) and a modal (`z-index: 1000`). Which appears on top?

**Answer:** The modal appears on top because it has a higher z-index value (1000 > 100).

</details>

---

## Part 4: Float and Clear (15 minutes)

**Note:** Float is an older layout technique. Modern layouts use Flexbox or Grid, but you'll still see float in older code.

### Float Property

Makes an element float to the left or right, allowing text and inline elements to wrap around it.

```css
.float-left {
    float: left;
    width: 200px;
    margin-right: 20px;
}

.float-right {
    float: right;
    width: 200px;
    margin-left: 20px;
}
```

**Values:**

-   `left` — Float to the left
-   `right` — Float to the right
-   `none` — Default (no float)

**Example: Text Wrapping Around Image**

```html
<style>
    .article-image {
        float: left;
        width: 200px;
        margin: 0 20px 10px 0;
        border-radius: 8px;
    }
</style>

<article>
    <img src="image.jpg" class="article-image" alt="Article image">
    <p>This text wraps around the floated image on the left. 
    Lorem ipsum dolor sit amet, consectetur adipiscing elit...</p>
    <p>More text continues to wrap around the image...</p>
</article>
```

### Clear Property

Prevents elements from wrapping around floated elements.

```css
.clear-left {
    clear: left;   /* No floating elements on left */
}

.clear-right {
    clear: right;  /* No floating elements on right */
}

.clear-both {
    clear: both;   /* No floating elements on either side */
}
```

**Example:**

```html
<style>
    .float-box {
        float: left;
        width: 150px;
        height: 100px;
        background-color: lightblue;
        margin: 10px;
    }
    
    .clear {
        clear: both;
    }
</style>

<div class="float-box">Float 1</div>
<div class="float-box">Float 2</div>
<p class="clear">This paragraph starts below the floated boxes.</p>
```

### Clearfix (Fixing Container Collapse)

When all children are floated, the parent container collapses (height becomes 0).

**Problem:**

```html
<div class="container">
    <div style="float: left;">Floated content</div>
</div>
<!-- Container has height of 0! -->
```

**Solution: Clearfix**

```css
.clearfix::after {
    content: "";
    display: table;
    clear: both;
}
```

**Usage:**

```html
<div class="container clearfix">
    <div style="float: left;">Floated content</div>
</div>
<!-- Container now has proper height! -->
```

**Modern alternative:** Use Flexbox or Grid instead of float for layouts.

---

## Part 5: Common Layout Patterns (10 minutes)

### Pattern 1: Fixed Header + Content

```html
<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }
    
    .header {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 60px;
        background-color: #333;
        color: white;
        display: flex;
        align-items: center;
        padding: 0 20px;
        z-index: 1000;
    }
    
    .content {
        padding-top: 60px; /* Height of header */
    }
</style>

<header class="header">My Website</header>
<main class="content">
    <!-- Page content -->
</main>
```

### Pattern 2: Centered Container

```css
.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
}
```

### Pattern 3: Card with Badge

```html
<style>
    .card {
        position: relative;
        width: 300px;
        padding: 20px;
        border: 1px solid #ddd;
        border-radius: 8px;
    }
    
    .badge {
        position: absolute;
        top: -10px;
        right: -10px;
        background-color: red;
        color: white;
        width: 30px;
        height: 30px;
        border-radius: 50%;
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 12px;
        font-weight: bold;
    }
</style>

<div class="card">
    <div class="badge">5</div>
    <h3>Card Title</h3>
    <p>Card content...</p>
</div>
```

### Pattern 4: Sidebar Layout with Float

```html
<style>
    .sidebar {
        float: left;
        width: 250px;
        background-color: #f0f0f0;
        padding: 20px;
        min-height: 400px;
    }
    
    .main-content {
        margin-left: 270px; /* Sidebar width + gap */
        padding: 20px;
    }
    
    .container::after {
        content: "";
        display: table;
        clear: both;
    }
</style>

<div class="container">
    <aside class="sidebar">Sidebar content</aside>
    <main class="main-content">Main content</main>
</div>
```

---

## 🛠️ Hands-On Practice (Remaining Time)

### Exercise 1: Sticky Navigation (15 minutes)

Create a webpage with a sticky navigation that sticks to the top when you scroll.

**Requirements:**

-   Header section with hero content
-   Navigation bar that becomes sticky
-   Multiple sections of content to scroll through
-   "Back to top" button that's fixed in bottom-right corner

**Starter code:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Sticky Navigation</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: Arial, sans-serif;
        }
        
        /* Add your CSS here */
        
    </style>
</head>
<body>
    <header class="hero">
        <h1>Welcome to My Website</h1>
        <p>Scroll down to see the sticky navigation</p>
    </header>
    
    <nav class="sticky-nav">
        <a href="#section1">Section 1</a>
        <a href="#section2">Section 2</a>
        <a href="#section3">Section 3</a>
    </nav>
    
    <section id="section1">
        <h2>Section 1</h2>
        <p>Content for section 1...</p>
    </section>
    
    <section id="section2">
        <h2>Section 2</h2>
        <p>Content for section 2...</p>
    </section>
    
    <section id="section3">
        <h2>Section 3</h2>
        <p>Content for section 3...</p>
    </section>
    
    <a href="#top" class="back-to-top">↑</a>
</body>
</html>
```

<details>
<summary>💡 Solution</summary>

```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
}

.hero {
    height: 400px;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}

.hero h1 {
    font-size: 48px;
    margin-bottom: 10px;
}

.sticky-nav {
    position: sticky;
    top: 0;
    background-color: #333;
    padding: 15px 20px;
    display: flex;
    gap: 30px;
    z-index: 100;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.sticky-nav a {
    color: white;
    text-decoration: none;
    font-weight: bold;
}

.sticky-nav a:hover {
    color: #667eea;
}

section {
    padding: 80px 20px;
    min-height: 500px;
}

section:nth-child(even) {
    background-color: #f5f5f5;
}

section h2 {
    font-size: 32px;
    margin-bottom: 20px;
    color: #333;
}

.back-to-top {
    position: fixed;
    bottom: 30px;
    right: 30px;
    width: 50px;
    height: 50px;
    background-color: #667eea;
    color: white;
    text-decoration: none;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 24px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
    z-index: 1000;
}

.back-to-top:hover {
    background-color: #5568d3;
}
```

</details>

### Exercise 2: Product Card with Badges (15 minutes)

Create a product card with positioned badges and overlays.

**Requirements:**

-   Product image with "Sale" badge in top-left corner
-   "New" badge in top-right corner
-   Price at bottom with proper positioning
-   Hover effect that shows additional info overlay

<details>
<summary>💡 Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Product Card</title>
    <style>
        * {
            box-sizing: border-box;
        }
        
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            padding: 40px;
            display: flex;
            justify-content: center;
        }
        
        .product-card {
            position: relative;
            width: 300px;
            background-color: white;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
        
        .product-image {
            position: relative;
            width: 100%;
            height: 300px;
            background-color: #ddd;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 18px;
            color: #666;
        }
        
        .badge {
            position: absolute;
            padding: 5px 15px;
            color: white;
            font-size: 12px;
            font-weight: bold;
            border-radius: 4px;
        }
        
        .badge-sale {
            top: 10px;
            left: 10px;
            background-color: #e74c3c;
        }
        
        .badge-new {
            top: 10px;
            right: 10px;
            background-color: #3498db;
        }
        
        .product-info {
            padding: 20px;
        }
        
        .product-title {
            margin: 0 0 10px 0;
            font-size: 20px;
            color: #333;
        }
        
        .product-price {
            font-size: 24px;
            color: #e74c3c;
            font-weight: bold;
        }
        
        .product-overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(102, 126, 234, 0.95);
            color: white;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            opacity: 0;
            transition: opacity 0.3s;
        }
        
        .product-card:hover .product-overlay {
            opacity: 1;
        }
        
        .overlay-button {
            margin-top: 20px;
            padding: 10px 30px;
            background-color: white;
            color: #667eea;
            border: none;
            border-radius: 5px;
            font-weight: bold;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="product-card">
        <div class="product-image">
            <span class="badge badge-sale">SALE</span>
            <span class="badge badge-new">NEW</span>
            Product Image
            <div class="product-overlay">
                <h3>Quick View</h3>
                <p>Hover to see details</p>
                <button class="overlay-button">Add to Cart</button>
            </div>
        </div>
        <div class="product-info">
            <h3 class="product-title">Awesome Product</h3>
            <div class="product-price">$29.99</div>
        </div>
    </div>
</body>
</html>
```

</details>

---

## 🐛 Common Mistakes & Troubleshooting

### Mistake 1: Forgetting Position on Parent

```css
/* ❌ WRONG: absolute child without positioned parent */
.child {
    position: absolute;
    top: 20px;
    /* Will position relative to <body>! */
}

/* ✅ CORRECT: Set parent position */
.parent {
    position: relative;  /* Creates positioning context */
}

.child {
    position: absolute;
    top: 20px;  /* Now positions relative to .parent */
}
```

### Mistake 2: Z-Index Not Working

```css
/* ❌ WRONG: z-index on static element */
.element {
    z-index: 100;  /* Has no effect! */
}

/* ✅ CORRECT: Add position property */
.element {
    position: relative;  /* or absolute, fixed, sticky */
    z-index: 100;  /* Now it works! */
}
```

### Mistake 3: Fixed Element Not Full Width

```css
/* ❌ WRONG: Fixed header not full width */
.header {
    position: fixed;
    top: 0;
    /* Doesn't stretch across screen */
}

/* ✅ CORRECT: Set width and position */
.header {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
}
```

### Mistake 4: Forgetting Padding for Fixed Header

```css
/* ❌ WRONG: Content hidden behind fixed header */
.header {
    position: fixed;
    top: 0;
    height: 60px;
}
/* Content starts at top and is hidden */

/* ✅ CORRECT: Add padding to body */
body {
    padding-top: 60px;  /* Same as header height */
}
```

### Debugging Positioning Issues

**Use Developer Tools:**

1. Right-click element → Inspect
2. Look at **Computed** tab for final position values
3. Check **Layout** tab for visual box model
4. Toggle position properties to test
5. Check for parent positioning context

**Common checks:**

-   ✅ Is parent positioned (for absolute children)?
-   ✅ Is element positioned (for z-index)?
-   ✅ Are top/right/bottom/left values correct?
-   ✅ Is z-index high enough?
-   ✅ Is overflow: hidden on parent hiding the element?

---

## 📝 Homework Assignment

Create a **"Portfolio Landing Page"** with advanced positioning:

**Content requirements:**

-   Fixed navigation header at top
-   Hero section with large background image
-   "Scroll down" indicator (positioned at bottom of hero)
-   Three project cards with:
    -   "Featured" badge on one card
    -   Category badge on all cards
    -   Hover overlay with project details
-   Sticky section headers as you scroll
-   Fixed "Contact Me" button in bottom-right corner
-   Footer section

**Styling requirements:**

-   Use `position: fixed` for navigation
-   Use `position: absolute` for badges
-   Use `position: sticky` for section headers
-   Use z-index to layer overlays properly
-   Implement hover effects on cards
-   Use proper box model (box-sizing: border-box)
-   Create a professional color scheme

**Bonus challenges:**

-   Add smooth scroll behavior
-   Create a modal dialog (fixed overlay)
-   Add a tooltip on hover
-   Make the navigation hide on scroll down, show on scroll up (requires JavaScript preview)
-   Add animation to the scroll indicator

---

## 🔍 What We Covered

✅ Display property (block, inline, inline-block, none)
✅ CSS positioning (static, relative, absolute, fixed, sticky)
✅ Positioning properties (top, right, bottom, left)
✅ Z-index and stacking contexts
✅ Float and clear (legacy layout technique)
✅ Common layout patterns
✅ Debugging positioning issues with Developer Tools

---

## 📚 Additional Resources

**Official Documentation:**

-   [MDN: CSS Positioning](https://developer.mozilla.org/docs/Web/CSS/position)
-   [MDN: Display Property](https://developer.mozilla.org/docs/Web/CSS/display)
-   [MDN: Z-Index](https://developer.mozilla.org/docs/Web/CSS/z-index)
-   [MDN: Float and Clear](https://developer.mozilla.org/docs/Web/CSS/float)

**Interactive Learning:**

-   [Learn CSS Positioning](https://ishadeed.com/article/learn-css-positioning/)
-   [CSS Positioning Explained](https://www.freecodecamp.org/news/css-positioning-position-absolute-and-relative/)

**Visual Guides:**

-   [CSS Tricks: Position](https://css-tricks.com/almanac/properties/p/position/)
-   [Positioning Examples](https://cssreference.io/positioning/)

**Practice:**

-   Try recreating common UI patterns (modals, dropdowns, sticky headers)
-   Build a complete landing page using only positioning techniques
-   Experiment with z-index and layering

---

## 🎯 Next Session Preview

In **Week 04 Session 10**, you'll learn about:

-   Flexbox layout system
-   Creating flexible, responsive layouts
-   Alignment and distribution of items
-   Building common UI patterns with Flexbox

**Preparation:** Master positioning concepts — they're the foundation before learning modern layout systems like Flexbox and Grid!

---

**Navigation:**
← [Session 08](session-08.md) | [Week 03 Index](../week-03.md) | [Week 04 Session 10](../../week-04/session-10.md) →
