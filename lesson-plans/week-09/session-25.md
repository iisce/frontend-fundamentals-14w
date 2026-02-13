# Week 09 — Session 25: DOM Fundamentals & Selection

**Navigation:**
← [Session 24](../week-08/session-24.md) | [Week 09 Index](../week-09.md) | [Session 26](session-26.md) →

---

**Session Length:** 90 minutes

## 📋 Pre-Class Checklist

Before starting this session, make sure you have:

- ✅ Completed Weeks 07–08 (JS fundamentals)
- ✅ Comfortable with variables, functions, arrays, and objects
- ✅ Have an HTML file ready to work with
- ✅ Create: `dom-basics.html` and `dom-basics.js`

## 🎯 Learning Objectives

By the end of this session, you will be able to:

- Explain what the DOM is and how browsers build it
- Select single and multiple DOM elements using modern methods
- Traverse the DOM tree (parents, children, siblings)
- Read element properties (text, HTML, attributes, classes)
- Understand the relationship between HTML, CSS, and the DOM

## 📦 Files for This Session

- `session-25.md` — This tutorial (you're reading it!)
- Create: `dom-basics.html`, `dom-basics.js`

## 🔑 Key Terms

**DOM**, **Document Object Model**, **node**, **element**, **text node**, **document**, **querySelector**, **querySelectorAll**, **getElementById**, **getElementsByClassName**, **NodeList**, **HTMLCollection**, **parent**, **child**, **sibling**, **traversal**, **live collection**, **static collection**

## 🏗️ What You Will Build

- A DOM explorer that highlights and inspects elements
- An interactive page that responds to element selection
- A navigation highlighter tool

---

## Part 1: What Is the DOM? (10 minutes)

### The Browser's Model of Your Page

When the browser loads an HTML file, it creates a **Document Object Model** — a tree of objects representing every element on the page:

```
                    document
                       |
                     <html>
                    /      \
                <head>     <body>
                  |        /    \
               <title>  <h1>   <ul>
                  |       |    / | \
                "My Page" "Hello" <li> <li> <li>
```

### Why the DOM Matters

- JavaScript can't see your HTML file directly
- The DOM is JavaScript's interface to the page
- Every HTML element becomes a JavaScript **object** you can read and modify
- Changes to the DOM instantly update what the user sees

```javascript
// The 'document' object is your entry point to the DOM
console.log(document); // the entire page
console.log(document.title); // the <title> text
console.log(document.URL); // the page URL
console.log(document.body); // the <body> element
console.log(document.head); // the <head> element
console.log(document.documentElement); // the <html> element
```

### DOM Node Types

Everything in the DOM is a **node**. The most common node types:

| Node Type | Example                | `nodeType` |
| --------- | ---------------------- | ---------- |
| Element   | `<div>`, `<p>`, `<h1>` | 1          |
| Text      | `"Hello World"`        | 3          |
| Comment   | `<!-- comment -->`     | 8          |
| Document  | `document`             | 9          |

```javascript
const heading = document.querySelector('h1');
console.log(heading.nodeType); // 1 (Element)
console.log(heading.nodeName); // "H1"
console.log(heading.nodeValue); // null (elements don't have nodeValue)
```

<details>
<summary>💡 Knowledge Check #1</summary>

**Question:** What is the DOM, and why can't JavaScript directly read your HTML file?

**Answer:**
The DOM (Document Object Model) is a **tree-structured representation** of an HTML document created by the browser. JavaScript can't read the raw HTML file because:

1. The browser **parses** the HTML and creates objects in memory
2. JavaScript interacts with these **objects** (the DOM), not the text file
3. The DOM can be different from the source HTML (browser fixes errors, JavaScript modifies it)
4. The DOM is **live** — changes update the screen instantly

</details>

---

## Part 2: Selecting Elements (20 minutes)

### Setup HTML

Create `dom-basics.html`:

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<title>DOM Basics</title>
		<style>
			.highlight {
				background-color: yellow;
				padding: 2px 6px;
			}
			.active {
				color: blue;
				font-weight: bold;
			}
			.card {
				border: 1px solid #ccc;
				padding: 16px;
				margin: 8px;
				border-radius: 8px;
			}
		</style>
	</head>
	<body>
		<header>
			<h1 id="main-title">DOM Fundamentals</h1>
			<p class="subtitle">Learning to select and manipulate elements</p>
		</header>

		<nav>
			<ul id="nav-list">
				<li class="nav-item active"><a href="#home">Home</a></li>
				<li class="nav-item"><a href="#about">About</a></li>
				<li class="nav-item"><a href="#contact">Contact</a></li>
			</ul>
		</nav>

		<main>
			<section id="content">
				<div
					class="card"
					data-category="intro"
				>
					<h2>Introduction</h2>
					<p>Welcome to the DOM tutorial.</p>
				</div>
				<div
					class="card"
					data-category="basics"
				>
					<h2>Basics</h2>
					<p>Learn how to select elements.</p>
				</div>
				<div
					class="card"
					data-category="advanced"
				>
					<h2>Advanced</h2>
					<p>Master DOM manipulation techniques.</p>
				</div>
			</section>
		</main>

		<footer>
			<p>&copy; 2024 DOM Tutorial</p>
		</footer>

		<script src="dom-basics.js"></script>
	</body>
</html>
```

### `querySelector()` — Select ONE Element

Returns the **first** element matching a CSS selector:

```javascript
// By ID
const title = document.querySelector('#main-title');
console.log(title.textContent); // "DOM Fundamentals"

// By class
const subtitle = document.querySelector('.subtitle');
console.log(subtitle.textContent);

// By tag
const firstParagraph = document.querySelector('p');

// By attribute
const introCard = document.querySelector('[data-category="intro"]');

// Complex selectors (just like CSS!)
const firstNavLink = document.querySelector('nav .nav-item a');
const activeItem = document.querySelector('.nav-item.active');
```

### `querySelectorAll()` — Select ALL Matching Elements

Returns a **NodeList** (array-like) of all matching elements:

```javascript
// Select all cards
const cards = document.querySelectorAll('.card');
console.log(cards.length); // 3
console.log(cards[0]); // first card
console.log(cards[2]); // third card

// Iterate with forEach
cards.forEach((card, index) => {
	console.log(`Card ${index + 1}: ${card.querySelector('h2').textContent}`);
});

// Convert to array if needed
const cardArray = [...cards]; // or Array.from(cards)
const cardTexts = cardArray.map((card) => card.querySelector('h2').textContent);
console.log(cardTexts); // ["Introduction", "Basics", "Advanced"]
```

### Older Selection Methods (Still Valid)

```javascript
// getElementById — fast, returns single element
const title = document.getElementById('main-title');

// getElementsByClassName — returns LIVE HTMLCollection
const items = document.getElementsByClassName('nav-item');
console.log(items.length); // 3

// getElementsByTagName — returns LIVE HTMLCollection
const paragraphs = document.getElementsByTagName('p');
```

### Live vs Static Collections

```javascript
// querySelectorAll returns a STATIC NodeList (snapshot)
const staticItems = document.querySelectorAll('.nav-item');

// getElementsByClassName returns a LIVE HTMLCollection (auto-updates)
const liveItems = document.getElementsByClassName('nav-item');

// If you add a new .nav-item to the page:
// staticItems.length stays the same (snapshot!)
// liveItems.length increases automatically (live!)
```

> 💡 **Best practice:** Use `querySelector` and `querySelectorAll` for almost everything. They use CSS selectors you already know!

<details>
<summary>💡 Knowledge Check #2</summary>

**Question:** What is the difference between `querySelector` and `querySelectorAll`?

**Answer:**
| Feature | `querySelector` | `querySelectorAll` |
|---------|-----------------|-------------------|
| Returns | First matching element (or `null`) | All matching elements (NodeList) |
| Selector | Any CSS selector | Any CSS selector |
| Result type | Single Element | Static NodeList |
| If no match | `null` | Empty NodeList (length 0) |

</details>

---

## Part 3: Reading Element Properties (15 minutes)

### Text Content

```javascript
const title = document.querySelector('#main-title');

// textContent — all text (including hidden)
console.log(title.textContent); // "DOM Fundamentals"

// innerText — visible text only (affected by CSS)
console.log(title.innerText); // "DOM Fundamentals"

// innerHTML — raw HTML inside the element
const nav = document.querySelector('#nav-list');
console.log(nav.innerHTML);
// <li class="nav-item active"><a href="#home">Home</a></li>
// <li class="nav-item"><a href="#about">About</a></li>
// ...
```

### Attributes

```javascript
const link = document.querySelector('nav a');

// Get an attribute
console.log(link.getAttribute('href')); // "#home"

// Check if an attribute exists
console.log(link.hasAttribute('href')); // true
console.log(link.hasAttribute('target')); // false

// Common properties (direct access)
const img = document.querySelector('img'); // if one existed
// img.src, img.alt, img.width, img.height

// Data attributes
const card = document.querySelector('.card');
console.log(card.getAttribute('data-category')); // "intro"
console.log(card.dataset.category); // "intro" (modern!)
```

### Classes

```javascript
const item = document.querySelector('.nav-item');

// classList — the modern way to work with classes
console.log(item.classList); // DOMTokenList ["nav-item", "active"]
console.log(item.classList.contains('active')); // true
console.log(item.classList.contains('hidden')); // false

// className — the full class string
console.log(item.className); // "nav-item active"
```

### Styles

```javascript
const title = document.querySelector('#main-title');

// Inline styles (read/write)
console.log(title.style.color); // "" (no inline style set)
console.log(title.style.fontSize); // "" (no inline style set)

// Computed styles (actual rendered styles from CSS)
const computed = getComputedStyle(title);
console.log(computed.fontSize); // "32px" (from browser default or CSS)
console.log(computed.color); // "rgb(0, 0, 0)"
console.log(computed.fontFamily); // "Times New Roman" (or whatever)
```

### Element Dimensions & Position

```javascript
const card = document.querySelector('.card');

// Dimensions
console.log(card.offsetWidth); // width including padding + border
console.log(card.offsetHeight); // height including padding + border
console.log(card.clientWidth); // width including padding (no border)
console.log(card.clientHeight); // height including padding (no border)

// Position relative to viewport
const rect = card.getBoundingClientRect();
console.log(rect.top); // distance from viewport top
console.log(rect.left); // distance from viewport left
console.log(rect.width); // element width
console.log(rect.height); // element height
```

---

## Part 4: DOM Traversal (15 minutes)

### Parent, Children, Siblings

From any element, you can navigate to related elements:

```javascript
const activeItem = document.querySelector('.nav-item.active');

// PARENT
console.log(activeItem.parentElement); // <ul id="nav-list">
console.log(activeItem.parentElement.parentElement); // <nav>

// CHILDREN
const navList = document.querySelector('#nav-list');
console.log(navList.children); // HTMLCollection of <li> elements
console.log(navList.children.length); // 3
console.log(navList.children[0]); // first <li>
console.log(navList.firstElementChild); // first <li>
console.log(navList.lastElementChild); // last <li>

// SIBLINGS
console.log(activeItem.nextElementSibling); // second <li>
console.log(activeItem.previousElementSibling); // null (it's the first)

const secondItem = activeItem.nextElementSibling;
console.log(secondItem.nextElementSibling); // third <li>
console.log(secondItem.previousElementSibling); // first <li> (activeItem)
```

### Traversal Pattern: Walk the DOM

```javascript
// Find all siblings of an element
function getSiblings(element) {
	const siblings = [];
	let sibling = element.parentElement.firstElementChild;

	while (sibling) {
		if (sibling !== element) {
			siblings.push(sibling);
		}
		sibling = sibling.nextElementSibling;
	}

	return siblings;
}

const active = document.querySelector('.nav-item.active');
const siblings = getSiblings(active);
console.log(siblings.length); // 2
```

### `closest()` — Find Nearest Ancestor

```javascript
const link = document.querySelector('nav a');

// Find the closest ancestor matching a selector
const listItem = link.closest('li'); // parent <li>
const nav = link.closest('nav'); // grandparent <nav>
const body = link.closest('body'); // <body>
const card = link.closest('.card'); // null (not an ancestor)

// Very useful for event delegation (coming in Session 27)
```

<details>
<summary>💡 Knowledge Check #3</summary>

**Question:** Given the HTML `<ul><li>A</li><li>B</li><li>C</li></ul>`, how do you get the text of the last `<li>` using DOM traversal?

**Answer:**

```javascript
const ul = document.querySelector('ul');

// Option 1: lastElementChild
console.log(ul.lastElementChild.textContent); // "C"

// Option 2: children collection
console.log(ul.children[ul.children.length - 1].textContent); // "C"

// Option 3: querySelector
console.log(ul.querySelector('li:last-child').textContent); // "C"
```

</details>

---

## Part 5: Lab — DOM Explorer (20 minutes)

### Challenge: Build a DOM Explorer

Add the following to your `dom-basics.js` file:

1. Select and log the main title text
2. Count all `.card` elements and log the count
3. Get the category of each card using `dataset`
4. Find the `active` nav item and log its link text
5. Get all siblings of the active nav item
6. Log the parent chain from the first `<a>` tag up to `<body>`

**Starter Code:**

```javascript
// DOM Explorer

// 1. Log the main title
const title = document.querySelector('#main-title');
// TODO: Log the title's text content

// 2. Count cards
// TODO: Select all .card elements and log the count

// 3. Get categories from data attributes
// TODO: Loop through cards and log each data-category

// 4. Active nav item
// TODO: Find the active nav item and log the text of its <a> child

// 5. Siblings of active item
// TODO: Get and log the text of all siblings

// 6. Parent chain
// TODO: Starting from the first <a>, walk up using parentElement and log each tag name
```

<details>
<summary>✅ Solution</summary>

```javascript
// DOM Explorer

// 1. Log the main title
const title = document.querySelector('#main-title');
console.log('Title:', title.textContent);

// 2. Count cards
const cards = document.querySelectorAll('.card');
console.log('Number of cards:', cards.length);

// 3. Get categories from data attributes
cards.forEach((card) => {
	console.log('Category:', card.dataset.category);
});

// 4. Active nav item
const activeItem = document.querySelector('.nav-item.active');
const activeLink = activeItem.querySelector('a');
console.log('Active link:', activeLink.textContent);

// 5. Siblings of active item
let sibling = activeItem.nextElementSibling;
while (sibling) {
	console.log('Sibling:', sibling.querySelector('a').textContent);
	sibling = sibling.nextElementSibling;
}

// 6. Parent chain
let current = document.querySelector('a');
const chain = [];
while (current && current !== document.body) {
	chain.push(current.tagName);
	current = current.parentElement;
}
chain.push('BODY');
console.log('Parent chain:', chain.join(' → '));
// A → LI → UL → NAV → BODY
```

</details>

---

## ⚠️ Common Mistakes

| Mistake                              | Problem                                | Fix                                                  |
| ------------------------------------ | -------------------------------------- | ---------------------------------------------------- |
| Using `querySelector` on `null`      | Chaining on element that doesn't exist | Check for `null` first: `if (el) { ... }`            |
| Forgetting `#` or `.` in selectors   | ID needs `#`, class needs `.`          | `querySelector("#id")`, `querySelector(".class")`    |
| Using `innerHTML` when you want text | Security risk (XSS) if user data       | Use `textContent` for plain text                     |
| Treating NodeList as an Array        | `map`, `filter` won't work directly    | Convert: `[...nodeList]` or `Array.from(nodeList)`   |
| Script in `<head>` without `defer`   | DOM not ready when script runs         | Use `defer` attribute or put script before `</body>` |

---

## 📝 Session Summary

In this session, you learned:

1. **The DOM** — Browser's tree representation of HTML
2. **`querySelector/querySelectorAll`** — Modern element selection with CSS selectors
3. **Reading properties** — `textContent`, `innerHTML`, `getAttribute`, `dataset`, `classList`
4. **Computed styles** — `getComputedStyle()` for actual rendered values
5. **DOM traversal** — `parentElement`, `children`, `nextElementSibling`, `closest()`
6. **Element dimensions** — `getBoundingClientRect()`, `offsetWidth/Height`

---

## 🏠 Homework

### Task 1: Page Analyzer

Write a script that logs:

- Total number of elements on the page
- Number of each tag type (how many `div`s, `p`s, `a`s, etc.)
- The deepest nested element and its depth

### Task 2: Navigation Highlighter

Write a script that:

- Finds all navigation links
- Checks which one matches the current page URL
- Adds an `active` class to the matching link's parent `<li>`

### Task 3: Table of Contents Generator

Write a function that:

- Finds all `<h2>` and `<h3>` elements on the page
- Generates a nested list (table of contents) from them
- Logs the result as HTML

### Bonus: DOM Statistics Dashboard

Create a script that builds a "stats panel" showing:

- Page load time
- Number of DOM nodes
- Number of images (loaded vs broken)
- All external links on the page

---

## 📚 Resources

- [MDN: Introduction to the DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction)
- [MDN: Document.querySelector()](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)
- [MDN: Document.querySelectorAll()](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll)
- [MDN: Element.closest()](https://developer.mozilla.org/en-US/docs/Web/API/Element/closest)
- [JavaScript.info: DOM Tree](https://javascript.info/dom-nodes)
- [JavaScript.info: Searching: getElement*, querySelector*](https://javascript.info/searching-elements-dom)

---

**Next:** [Session 26 — DOM Manipulation & Styling](session-26.md) →
