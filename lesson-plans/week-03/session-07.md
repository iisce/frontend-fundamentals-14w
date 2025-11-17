# Week 03 — Session 07: Introduction to CSS

**Navigation:**
← [Week 02 Session 06](../week-02/session-06.md) | [Week 03 Index](../week-03.md) | [Session 08](session-08.md) →

---

**Session Length:** 90 minutes

## 📋 Pre-Class Checklist

Before starting this session, make sure you have:

-   ✅ Completed HTML fundamentals (Weeks 01-02)
-   ✅ Code editor (VS Code) installed with Live Server extension
-   ✅ A browser with Developer Tools (Chrome, Firefox, or Edge)
-   ✅ Create a new folder: `week-03-css-basics`

## 🎯 Learning Objectives

By the end of this session, you will be able to:

-   Understand what CSS is and how it works with HTML
-   Write CSS using three different methods (inline, internal, external)
-   Use basic CSS selectors (element, class, ID)
-   Apply colors using different formats (names, hex, RGB)
-   Style text with fonts, sizes, and formatting
-   Understand and debug CSS using Developer Tools

## 📦 Files for This Session

-   `session-07.md` — This tutorial (you're reading it!)
-   `css-basics-template.html` — Starter file for practice
-   `css-basics-solution.html` — Complete working example
-   `css-basics-cheat-sheet.md` — Quick reference guide

## 🔑 Key Terms

**CSS** (Cascading Style Sheets), **selector**, **property**, **value**, **declaration**, **rule**, **class**, **id**, **inline style**, **internal style**, **external stylesheet**, **hex color**, **RGB**, **font-family**, **Developer Tools**

## 🏗️ What You Will Build

-   A styled personal profile card
-   A formatted article with typography
-   A color palette showcase

---

## Part 1: What is CSS? (20 minutes)

### What is CSS?

**CSS (Cascading Style Sheets)** is the language used to style and layout web pages. While HTML provides the structure and content, CSS controls the visual presentation.

**Think of it like building a house:**

-   **HTML** = The structure (walls, rooms, doors)
-   **CSS** = The decoration (paint colors, furniture, lighting)
-   **JavaScript** = The functionality (lights turning on, doors opening) — we'll learn this later!

### What Can CSS Do?

CSS controls:

✅ **Colors** — Text color, background color, borders
✅ **Typography** — Font family, size, weight, line height
✅ **Spacing** — Margins, padding, gaps between elements
✅ **Layout** — Positioning, alignment, responsive design
✅ **Effects** — Shadows, transitions, animations
✅ **Visibility** — Show/hide elements, opacity

### CSS Syntax

Every CSS rule has the same structure:

```css
selector {
	property: value;
	property: value;
}
```

**Example:**

```css
p {
	color: blue;
	font-size: 16px;
}
```

**Breaking it down:**

-   `p` — **Selector** (what to style)
-   `{ }` — **Declaration block** (contains all styling)
-   `color: blue;` — **Declaration** (one style rule)
-   `color` — **Property** (what aspect to style)
-   `blue` — **Value** (how to style it)
-   `;` — **Semicolon** (ends each declaration)

<details>
<summary>💡 Knowledge Check #1</summary>

**Question:** In the CSS rule `h1 { color: red; font-size: 24px; }`, identify:

-   What is the selector?
-   How many declarations are there?
-   What are the properties?

**Answer:**

-   **Selector:** `h1`
-   **Declarations:** 2 (`color: red;` and `font-size: 24px;`)
-   **Properties:** `color` and `font-size`

</details>

### Quick Practice: Read CSS

Look at this CSS code:

```css
h2 {
	color: green;
	font-size: 20px;
	text-align: center;
}
```

**What does it do?**

Answer: It makes all `<h2>` headings green, 20 pixels tall, and centered.

---

## Part 2: Three Ways to Add CSS (25 minutes)

There are three methods to add CSS to your HTML:

### Method 1: Inline CSS

Add CSS directly to an HTML element using the `style` attribute.

```html
<p style="color: red; font-size: 18px;">This is a red paragraph.</p>
```

**Pros:**

-   ✅ Quick for single elements
-   ✅ Highest priority (overrides other styles)

**Cons:**

-   ❌ Not reusable
-   ❌ Hard to maintain
-   ❌ Mixes content with presentation

**When to use:** Rarely. Only for quick tests or email HTML.

### Method 2: Internal CSS

Add CSS in the `<head>` section using `<style>` tags.

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<title>My Page</title>
		<style>
			p {
				color: blue;
				font-size: 16px;
			}

			h1 {
				color: navy;
				text-align: center;
			}
		</style>
	</head>
	<body>
		<h1>Welcome</h1>
		<p>This is a blue paragraph.</p>
	</body>
</html>
```

**Pros:**

-   ✅ Affects entire page
-   ✅ Keeps everything in one file
-   ✅ Good for single-page sites

**Cons:**

-   ❌ Not reusable across pages
-   ❌ Makes HTML file longer

**When to use:** Small websites, prototypes, or email templates.

### Method 3: External CSS (BEST PRACTICE)

Create a separate `.css` file and link it to your HTML.

**File: `styles.css`**

```css
p {
	color: blue;
	font-size: 16px;
}

h1 {
	color: navy;
	text-align: center;
}
```

**File: `index.html`**

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<title>My Page</title>
		<link
			rel="stylesheet"
			href="styles.css"
		/>
	</head>
	<body>
		<h1>Welcome</h1>
		<p>This is a blue paragraph.</p>
	</body>
</html>
```

**Breaking down the `<link>` tag:**

-   `rel="stylesheet"` — Relationship: this file is a stylesheet
-   `href="styles.css"` — Path to the CSS file

**Pros:**

-   ✅ Reusable across multiple pages
-   ✅ Separates content from presentation
-   ✅ Easier to maintain
-   ✅ Browser caches it (faster loading)

**Cons:**

-   ❌ Requires separate file

**When to use:** Almost always. This is the industry standard.

<details>
<summary>💡 Knowledge Check #2</summary>

**Question:** Which method should you use for a 10-page website, and why?

**Answer:** External CSS. All 10 pages can share one stylesheet, making it easier to update styles across the entire site. If you change the stylesheet, all pages automatically get the update.

</details>

### Quick Practice: Create External CSS

**Try this:**

1. Create a new folder called `css-practice`
2. Inside, create two files:
    - `index.html`
    - `style.css`
3. In `index.html`, add basic HTML structure and link to `style.css`
4. In `style.css`, add a rule to make all paragraphs purple
5. Open `index.html` in Live Server to test

---

## Part 3: CSS Selectors (25 minutes)

Selectors tell CSS **which elements** to style.

### Element Selector

Targets all elements of a specific type.

```css
p {
	color: darkgreen;
}

h1 {
	color: navy;
}

a {
	color: blue;
	text-decoration: none;
}
```

**Use when:** You want all elements of that type to look the same.

### Class Selector

Targets elements with a specific `class` attribute. Classes are reusable.

**HTML:**

```html
<p class="highlight">This paragraph is highlighted.</p>
<p>This one is not.</p>
<p class="highlight">This one is highlighted too!</p>
```

**CSS:**

```css
.highlight {
	background-color: yellow;
	font-weight: bold;
}
```

**Key points:**

-   Start with a dot (`.`) in CSS
-   Can be applied to multiple elements
-   One element can have multiple classes
-   Use descriptive names: `.error`, `.success`, `.btn-primary`

**Multiple classes example:**

```html
<button class="btn btn-large btn-primary">Click Me</button>
```

```css
.btn {
	padding: 10px 20px;
	border: none;
	cursor: pointer;
}

.btn-large {
	font-size: 18px;
}

.btn-primary {
	background-color: blue;
	color: white;
}
```

### ID Selector

Targets a single unique element with a specific `id` attribute.

**HTML:**

```html
<header id="main-header">
	<h1>My Website</h1>
</header>
```

**CSS:**

```css
#main-header {
	background-color: #333;
	color: white;
	padding: 20px;
}
```

**Key points:**

-   Start with a hash (#) in CSS
-   Each ID must be unique on the page
-   Use for unique elements: `#header`, `#footer`, `#logo`

### Class vs. ID: When to Use Each

| Feature              | Class          | ID                          |
| -------------------- | -------------- | --------------------------- |
| CSS prefix           | `.` (dot)      | `#` (hash)                  |
| Reusable             | ✅ Yes         | ❌ No (unique)              |
| Multiple per element | ✅ Yes         | ❌ Only one ID              |
| Best for             | Styling groups | Unique elements, JS targets |

**Rule of thumb:** Use classes for styling, IDs sparingly (mainly for JavaScript or page anchors).

<details>
<summary>💡 Knowledge Check #3</summary>

**Question:** What's wrong with this code?

```html
<p id="intro">First paragraph</p>
<p id="intro">Second paragraph</p>
```

**Answer:** IDs must be unique! You can't use the same ID twice on the same page. This should use a class instead:

```html
<p class="intro">First paragraph</p>
<p class="intro">Second paragraph</p>
```

</details>

### Grouping Selectors

Apply the same styles to multiple selectors.

```css
h1,
h2,
h3 {
	color: navy;
	font-family: Arial, sans-serif;
}

.btn-primary,
.btn-secondary {
	padding: 10px 20px;
	border-radius: 5px;
}
```

**Use commas** to separate selectors.

### Quick Practice: Selectors

Create an HTML page with:

-   An `<h1>` with `id="page-title"`
-   Three `<p>` tags, two with `class="important"`
-   A `<footer>` tag

Then write CSS to:

-   Make the `#page-title` blue and centered
-   Make `.important` paragraphs bold with yellow background
-   Make the `footer` have a gray background

---

## Part 4: Colors in CSS (20 minutes)

CSS supports multiple color formats.

### Color Names

CSS recognizes 140 color names.

```css
p {
	color: red;
	background-color: lightblue;
}

h1 {
	color: navy;
}

.warning {
	color: orange;
}
```

**Common colors:** `red`, `blue`, `green`, `yellow`, `orange`, `purple`, `pink`, `gray`, `black`, `white`

**Extended colors:** `lightblue`, `darkgreen`, `crimson`, `coral`, `turquoise`, `gold`

### Hexadecimal Colors (Hex)

Most common format in web design. Uses base-16 numbering.

```css
h1 {
	color: #ff0000; /* Red */
}

p {
	color: #0000ff; /* Blue */
}

.box {
	background-color: #00ff00; /* Green */
}
```

**Format:** `#RRGGBB`

-   **RR** = Red (00-FF)
-   **GG** = Green (00-FF)
-   **BB** = Blue (00-FF)

**Shorthand:**

```css
/* Full form */
color: #ff0000;

/* Shorthand (when pairs match) */
color: #f00;
```

**Popular hex colors:**

```css
#FFFFFF  /* White */
#000000  /* Black */
#808080  /* Gray */
#FF0000  /* Red */
#00FF00  /* Green */
#0000FF  /* Blue */
#FFFF00  /* Yellow */
#FFA500  /* Orange */
#800080  /* Purple */
```

### RGB Colors

Specify colors using Red, Green, Blue values (0-255).

```css
p {
	color: rgb(255, 0, 0); /* Red */
}

h1 {
	color: rgb(0, 0, 255); /* Blue */
}

.box {
	background-color: rgb(255, 255, 0); /* Yellow */
}
```

### RGBA Colors (with transparency)

Same as RGB, but with an **alpha channel** for transparency (0-1).

```css
.overlay {
	background-color: rgba(0, 0, 0, 0.5); /* Black with 50% opacity */
}

.banner {
	background-color: rgba(255, 0, 0, 0.3); /* Red with 30% opacity */
}
```

**Alpha values:**

-   `0` = Fully transparent
-   `0.5` = 50% transparent
-   `1` = Fully opaque (no transparency)

### Which Color Format to Use?

| Format | Best For                                   | Example                           |
| ------ | ------------------------------------------ | --------------------------------- |
| Names  | Quick prototypes, common colors            | `color: red;`                     |
| Hex    | Most web projects, design systems          | `color: #FF5733;`                 |
| RGB    | When you have RGB values from design tools | `color: rgb(255, 87, 51);`        |
| RGBA   | When you need transparency                 | `background: rgba(0, 0, 0, 0.5);` |

<details>
<summary>💡 Knowledge Check #4</summary>

**Question:** What's the difference between these two?

```css
background-color: rgb(0, 0, 0);
background-color: rgba(0, 0, 0, 0.5);
```

**Answer:**

-   First one is solid black
-   Second one is black with 50% transparency (semi-transparent)

</details>

### Quick Practice: Colors

Create a div with:

-   Background: light blue (`#ADD8E6` or `lightblue`)
-   Text color: dark blue (`#00008B` or `navy`)
-   Border: 2px solid with 50% transparent black

---

## Part 5: Text Styling (Homework/Practice)

You'll explore these CSS properties on your own:

### Font Properties

```css
p {
	font-family: Arial, sans-serif;
	font-size: 16px;
	font-weight: bold; /* or 100-900 */
	font-style: italic;
}
```

### Text Properties

```css
h1 {
	text-align: center; /* left, right, center, justify */
	text-decoration: underline; /* none, underline, line-through */
	text-transform: uppercase; /* lowercase, capitalize */
	letter-spacing: 2px;
	line-height: 1.5;
}
```

### Complete Example

```css
.article-title {
	font-family: Georgia, serif;
	font-size: 32px;
	font-weight: bold;
	color: #333;
	text-align: center;
	line-height: 1.2;
	margin-bottom: 20px;
}

.article-text {
	font-family: Arial, sans-serif;
	font-size: 16px;
	color: #555;
	line-height: 1.6;
	text-align: justify;
}
```

---

## 🛠️ Hands-On Practice (Remaining Time)

### Exercise 1: Profile Card (15 minutes)

Create a personal profile card with:

**Requirements:**

-   Use external CSS
-   Include a profile photo (can use placeholder: `https://via.placeholder.com/150`)
-   Name as `<h1>` (blue, centered)
-   Job title as `<h2>` (gray, centered)
-   Bio paragraph (left-aligned, dark gray text)
-   Background color for the card
-   Padding and border

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
		<link
			rel="stylesheet"
			href="profile.css"
		/>
	</head>
	<body>
		<div class="profile-card">
			<img
				src="https://via.placeholder.com/150"
				alt="Profile photo"
			/>
			<h1>Your Name</h1>
			<h2>Job Title</h2>
			<p class="bio">Write a short bio about yourself...</p>
		</div>
	</body>
</html>
```

**Your Task:** Create `profile.css` and style it!

<details>
<summary>💡 Solution</summary>

**profile.css:**

```css
body {
	font-family: Arial, sans-serif;
	background-color: #f0f0f0;
	padding: 20px;
}

.profile-card {
	background-color: white;
	max-width: 400px;
	margin: 0 auto;
	padding: 30px;
	border: 1px solid #ddd;
	text-align: center;
}

.profile-card img {
	border-radius: 50%;
	width: 150px;
	height: 150px;
}

.profile-card h1 {
	color: #0066cc;
	font-size: 28px;
	margin: 15px 0 5px 0;
}

.profile-card h2 {
	color: #666;
	font-size: 18px;
	font-weight: normal;
	margin: 0 0 20px 0;
}

.bio {
	color: #333;
	line-height: 1.6;
	text-align: left;
}
```

</details>

### Exercise 2: Styled Article (15 minutes)

Create an article page with proper typography:

**Requirements:**

-   Article title (large, bold, centered, dark color)
-   Author and date (smaller, gray, italicized)
-   Multiple paragraphs with good line height
-   Highlighted quote (different background, larger text)
-   Use classes effectively

**Try it yourself, then check the solution!**

<details>
<summary>💡 Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<title>Article</title>
		<link
			rel="stylesheet"
			href="article.css"
		/>
	</head>
	<body>
		<article>
			<h1 class="article-title">The Future of Web Development</h1>
			<p class="article-meta">By Jane Doe | November 17, 2025</p>

			<p>Web development continues to evolve at a rapid pace...</p>

			<blockquote class="highlight">
				"The best way to predict the future is to create it."
			</blockquote>

			<p>As we look ahead, several trends are emerging...</p>
		</article>
	</body>
</html>
```

```css
body {
	font-family: Georgia, serif;
	max-width: 700px;
	margin: 40px auto;
	padding: 20px;
	background-color: #fafafa;
	color: #333;
}

.article-title {
	font-size: 36px;
	color: #1a1a1a;
	text-align: center;
	margin-bottom: 10px;
}

.article-meta {
	text-align: center;
	color: #777;
	font-style: italic;
	font-size: 14px;
	margin-bottom: 30px;
}

article p {
	font-size: 18px;
	line-height: 1.8;
	margin-bottom: 20px;
}

.highlight {
	background-color: #fff3cd;
	border-left: 4px solid #ffc107;
	padding: 20px;
	font-size: 20px;
	font-style: italic;
	margin: 30px 0;
	color: #856404;
}
```

</details>

---

## 🐛 Common Mistakes & Troubleshooting

### Mistake 1: Forgetting the Semicolon

```css
/* ❌ WRONG */
p {
  color: blue
  font-size: 16px;
}

/* ✅ CORRECT */
p {
  color: blue;
  font-size: 16px;
}
```

### Mistake 2: Missing Dot for Classes

```css
/* ❌ WRONG */
highlight {
	background-color: yellow;
}

/* ✅ CORRECT */
.highlight {
	background-color: yellow;
}
```

### Mistake 3: Wrong File Path

```html
<!-- ❌ WRONG - file is actually in a 'css' folder -->
<link
	rel="stylesheet"
	href="styles.css"
/>

<!-- ✅ CORRECT -->
<link
	rel="stylesheet"
	href="css/styles.css"
/>
```

### Mistake 4: Typos in Color Names

```css
/* ❌ WRONG */
color: blu;
color: ligt-blue;

/* ✅ CORRECT */
color: blue;
color: lightblue;
```

### Debugging Tips

1. **Use Developer Tools** (F12 or Right-click → Inspect)

    - See which styles are applied
    - Test changes live
    - View computed styles

2. **Check for typos** in property names and values

3. **Verify file paths** for external stylesheets

4. **Use color** to test if CSS is working:

    ```css
    * {
    	border: 1px solid red;
    }
    ```

5. **Comment out code** to isolate problems:
    ```css
    /* p {
      color: blue;
    } */
    ```

---

## 📝 Homework Assignment

Create a **"My Favorite Things" webpage** with:

**Content requirements:**

-   Page title (h1)
-   Introduction paragraph
-   Three sections (use h2 for section titles):
    -   Favorite books (unordered list)
    -   Favorite movies (unordered list)
    -   Favorite hobbies (unordered list)
-   Footer with your name and date

**Styling requirements:**

-   Use external CSS
-   Use at least 3 different color formats (name, hex, RGB)
-   Style headings with custom colors and fonts
-   Use classes for styling list items
-   Add background color to sections
-   Style the footer differently
-   Use at least 5 different CSS properties

**Bonus challenges:**

-   Add hover effects (links change color when hovered)
-   Use RGBA for semi-transparent backgrounds
-   Create a color scheme that looks professional

---

## 🔍 What We Covered

✅ What CSS is and its role in web development
✅ CSS syntax (selectors, properties, values)
✅ Three ways to add CSS (inline, internal, external)
✅ Basic selectors (element, class, ID)
✅ Color formats (names, hex, RGB, RGBA)
✅ Text styling basics (fonts, sizes, alignment)
✅ Using Developer Tools to debug CSS

---

## 📚 Additional Resources

**Official Documentation:**

-   [MDN: CSS Basics](https://developer.mozilla.org/docs/Learn/Getting_started_with_the_web/CSS_basics)
-   [MDN: CSS Selectors](https://developer.mozilla.org/docs/Web/CSS/CSS_Selectors)
-   [MDN: Color Values](https://developer.mozilla.org/docs/Web/CSS/color_value)

**Tools:**

-   [Color Picker](https://htmlcolorcodes.com/)
-   [Google Fonts](https://fonts.google.com/)
-   [Can I Use](https://caniuse.com/) - Check browser support

**Practice:**

-   [CSS Diner](https://flukeout.github.io/) - Selector practice game
-   [Codecademy CSS Course](https://www.codecademy.com/learn/learn-css)

---

## 🎯 Next Session Preview

In **Session 08: The CSS Box Model**, you'll learn:

-   How every element is a rectangular box
-   Margin, border, padding, and content
-   Width and height properties
-   Box-sizing property
-   Creating layouts with the box model

**Preparation:** Make sure you're comfortable with selectors and colors before moving on!

---

**Navigation:**
← [Week 02 Session 06](../week-02/session-06.md) | [Week 03 Index](../week-03.md) | [Session 08](session-08.md) →
