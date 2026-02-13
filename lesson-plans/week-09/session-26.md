# Week 09 — Session 26: DOM Manipulation & Styling

**Navigation:**
← [Session 25](session-25.md) | [Week 09 Index](../week-09.md) | [Session 27](session-27.md) →

---

**Session Length:** 90 minutes

## 📋 Pre-Class Checklist

Before starting this session, make sure you have:

- ✅ Completed Session 25 (DOM selection & traversal)
- ✅ Comfortable with `querySelector`, `querySelectorAll`, and DOM traversal
- ✅ Have `dom-basics.html` from Session 25
- ✅ Create a new file: `dom-manipulation.js`

## 🎯 Learning Objectives

By the end of this session, you will be able to:

- Create new DOM elements with `createElement`
- Add elements to the page with `append`, `prepend`, `before`, `after`
- Remove elements from the DOM
- Modify element content, attributes, and data attributes
- Manipulate CSS classes with `classList`
- Change inline styles dynamically
- Clone elements and work with document fragments for performance

## 📦 Files for This Session

- `session-26.md` — This tutorial (you're reading it!)
- Create: `dom-manipulation.html`, `dom-manipulation.js`

## 🔑 Key Terms

**createElement**, **append**, **prepend**, **before**, **after**, **remove**, **replaceWith**, **cloneNode**, **innerHTML**, **textContent**, **setAttribute**, **classList**, **toggle**, **DocumentFragment**, **template**, **insertAdjacentHTML**

## 🏗️ What You Will Build

- A dynamic to-do list (add, delete, toggle items)
- A card generator that creates cards from data
- A theme switcher with dynamic styling

---

## Part 1: Creating Elements (15 minutes)

### `document.createElement()`

```javascript
// Create a new element (exists in memory, not on page yet!)
const newDiv = document.createElement('div');
const newParagraph = document.createElement('p');
const newButton = document.createElement('button');

// Set content
newParagraph.textContent = 'This paragraph was created by JavaScript!';
newButton.textContent = 'Click Me';

// Set attributes
newDiv.id = 'dynamic-content';
newDiv.className = 'card';
newButton.setAttribute('type', 'button');
newButton.dataset.action = 'submit';

// Set styles
newDiv.style.padding = '16px';
newDiv.style.border = '2px solid blue';
newDiv.style.borderRadius = '8px';
```

### Adding Elements to the Page

```javascript
const container = document.querySelector('#content');

// append — add to END of element's children
container.append(newDiv);

// prepend — add to BEGINNING of element's children
container.prepend(newParagraph);

// before — add BEFORE the element (as sibling)
const firstCard = document.querySelector('.card');
firstCard.before(newButton);

// after — add AFTER the element (as sibling)
firstCard.after(newParagraph);

// appendChild (older, still works) — only takes one node
container.appendChild(newDiv);
```

### Building Complex Elements

```javascript
function createCard(title, text, category) {
	const card = document.createElement('div');
	card.className = 'card';
	card.dataset.category = category;

	const heading = document.createElement('h2');
	heading.textContent = title;

	const paragraph = document.createElement('p');
	paragraph.textContent = text;

	const badge = document.createElement('span');
	badge.className = 'badge';
	badge.textContent = category;

	// Assemble the card
	card.append(heading, paragraph, badge);

	return card;
}

// Use it
const container = document.querySelector('#content');
const card = createCard('New Topic', 'Created dynamically!', 'dynamic');
container.append(card);
```

### Using `innerHTML` (Quick but Risky)

```javascript
// innerHTML — set HTML content as a string
const container = document.querySelector('#output');

container.innerHTML = `
  <div class="card">
    <h2>Quick Card</h2>
    <p>Created with innerHTML</p>
  </div>
`;

// ⚠️ WARNING: Never use innerHTML with user input!
const userInput = '<img src="x" onerror="alert(\'hacked!\')">';
// container.innerHTML = userInput; // ❌ XSS vulnerability!
// container.textContent = userInput; // ✅ Safe — treats as text
```

### `insertAdjacentHTML()` — Best of Both Worlds

```javascript
const card = document.querySelector('.card');

// Position options:
// "beforebegin" — before the element
// "afterbegin"  — inside, before first child
// "beforeend"   — inside, after last child
// "afterend"    — after the element

card.insertAdjacentHTML(
	'beforeend',
	`
  <footer class="card-footer">
    <small>Added dynamically</small>
  </footer>
`,
);
```

<details>
<summary>💡 Knowledge Check #1</summary>

**Question:** What is the difference between `append()` and `appendChild()`?

**Answer:**
| Feature | `append()` | `appendChild()` |
|---------|-----------|-----------------|
| Accepts strings | ✅ Yes | ❌ No (nodes only) |
| Multiple items | ✅ Yes | ❌ One at a time |
| Return value | `undefined` | The appended node |
| Modern | ✅ ES6+ | Older API |

```javascript
// append can take multiple items and strings
container.append(heading, paragraph, 'Some text');

// appendChild takes only one node
container.appendChild(heading);
```

</details>

---

## Part 2: Removing & Replacing Elements (10 minutes)

### Removing Elements

```javascript
// Modern: element.remove()
const card = document.querySelector('.card');
card.remove(); // gone from the DOM!

// Older: parent.removeChild(child)
const list = document.querySelector('#nav-list');
const firstItem = list.firstElementChild;
list.removeChild(firstItem);

// Remove all children
const container = document.querySelector('#content');
container.innerHTML = ''; // quick but destroys event listeners

// Better: remove children one by one
while (container.firstChild) {
	container.removeChild(container.firstChild);
}

// Modern: replaceChildren() — clear or replace all children
container.replaceChildren(); // clear all
container.replaceChildren(newElement1, newElement2); // replace with new
```

### Replacing Elements

```javascript
const oldCard = document.querySelector('.card');

const newCard = document.createElement('div');
newCard.className = 'card updated';
newCard.innerHTML = "<h2>Replacement Card</h2><p>I'm new here!</p>";

// replaceWith — replace with a new element
oldCard.replaceWith(newCard);

// Older: parent.replaceChild(new, old)
// parent.replaceChild(newCard, oldCard);
```

---

## Part 3: Working with Classes (10 minutes)

### `classList` API

```javascript
const card = document.querySelector('.card');

// Add classes
card.classList.add('featured');
card.classList.add('animated', 'fade-in'); // multiple at once

// Remove classes
card.classList.remove('fade-in');

// Toggle — add if missing, remove if present
card.classList.toggle('active'); // adds "active"
card.classList.toggle('active'); // removes "active"

// Toggle with condition
const isDark = true;
card.classList.toggle('dark-mode', isDark); // adds if isDark is true

// Check if class exists
console.log(card.classList.contains('featured')); // true
console.log(card.classList.contains('hidden')); // false

// Replace a class
card.classList.replace('featured', 'standard');

// Get all classes as an array
const classes = [...card.classList];
console.log(classes); // ["card", "standard", "animated"]
```

### Practical: Theme Switcher

```javascript
function toggleTheme() {
	document.body.classList.toggle('dark-theme');

	const isDark = document.body.classList.contains('dark-theme');
	localStorage.setItem('theme', isDark ? 'dark' : 'light');
}

// Load saved theme on startup
const savedTheme = localStorage.getItem('theme');
if (savedTheme === 'dark') {
	document.body.classList.add('dark-theme');
}
```

### Practical: Tab Navigation

```javascript
function activateTab(clickedTab) {
	// Remove active from all tabs
	document.querySelectorAll('.tab').forEach((tab) => {
		tab.classList.remove('active');
	});

	// Add active to clicked tab
	clickedTab.classList.add('active');
}
```

<details>
<summary>💡 Knowledge Check #2</summary>

**Question:** What does `classList.toggle("active")` do?

**Answer:**

- If the element **does NOT** have the class `"active"` → it **adds** it
- If the element **already has** the class `"active"` → it **removes** it
- Returns `true` if the class was added, `false` if removed

It's like a light switch — on/off each time you call it.

</details>

---

## Part 4: Dynamic Styling (10 minutes)

### Inline Styles with `style` Property

```javascript
const card = document.querySelector('.card');

// Set individual styles
card.style.backgroundColor = '#f0f0f0';
card.style.padding = '20px';
card.style.borderRadius = '12px';
card.style.boxShadow = '0 4px 6px rgba(0, 0, 0, 0.1)';

// CSS property names are camelCase in JS!
// background-color → backgroundColor
// font-size → fontSize
// border-radius → borderRadius
// z-index → zIndex

// Remove an inline style
card.style.boxShadow = ''; // set to empty string

// Set multiple styles at once with cssText
card.style.cssText = `
  background-color: #f0f0f0;
  padding: 20px;
  border-radius: 12px;
  transition: transform 0.3s ease;
`;
```

### CSS Custom Properties (Variables) via JS

```javascript
// Set a CSS variable on the root
document.documentElement.style.setProperty('--primary-color', '#3498db');
document.documentElement.style.setProperty('--font-size', '18px');

// Read a CSS variable
const primaryColor = getComputedStyle(
	document.documentElement,
).getPropertyValue('--primary-color');
console.log(primaryColor); // "#3498db"
```

### When to Use Classes vs Inline Styles

| Use Case                                     | Approach                         |
| -------------------------------------------- | -------------------------------- |
| Toggle visual states (active, hidden, error) | `classList.add/remove/toggle` ✅ |
| Apply a theme or variant                     | `classList` + CSS classes ✅     |
| Dynamic values (position, size from JS)      | `style.property` ✅              |
| User-chosen colors/fonts                     | CSS variables via JS ✅          |
| Animations and transitions                   | CSS classes ✅                   |

> 💡 **Rule of thumb:** Prefer CSS classes over inline styles. Classes are reusable, cacheable, and easier to maintain.

---

## Part 5: Cloning & Document Fragments (5 minutes)

### Cloning Elements

```javascript
const originalCard = document.querySelector('.card');

// Shallow clone (element only, no children)
const shallowClone = originalCard.cloneNode(false);

// Deep clone (element + all children)
const deepClone = originalCard.cloneNode(true);
deepClone.querySelector('h2').textContent = 'Cloned Card';

document.querySelector('#content').append(deepClone);
```

### Document Fragments (Performance)

When adding many elements, use a fragment to avoid multiple reflows:

```javascript
const data = ['Apple', 'Banana', 'Cherry', 'Date', 'Elderberry'];

// ❌ Slow — each append triggers a DOM reflow
// data.forEach(item => {
//   const li = document.createElement("li");
//   li.textContent = item;
//   list.append(li);
// });

// ✅ Fast — batch with DocumentFragment
const fragment = document.createDocumentFragment();

data.forEach((item) => {
	const li = document.createElement('li');
	li.textContent = item;
	fragment.append(li);
});

document.querySelector('ul').append(fragment); // single DOM update!
```

---

## Part 6: Lab — Dynamic To-Do List (20 minutes)

### Challenge: Build a To-Do List

Create `dom-manipulation.html` with a to-do list that supports:

1. Adding new items
2. Marking items as complete (strikethrough)
3. Deleting items
4. Counting remaining items

**HTML Setup:**

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<title>To-Do List</title>
		<style>
			body {
				font-family: Arial, sans-serif;
				max-width: 500px;
				margin: 40px auto;
				padding: 0 20px;
			}
			h1 {
				text-align: center;
			}
			.input-group {
				display: flex;
				gap: 8px;
				margin-bottom: 16px;
			}
			.input-group input {
				flex: 1;
				padding: 8px 12px;
				font-size: 16px;
				border: 2px solid #ddd;
				border-radius: 6px;
			}
			.input-group button {
				padding: 8px 16px;
				background: #3498db;
				color: white;
				border: none;
				border-radius: 6px;
				cursor: pointer;
				font-size: 16px;
			}
			#todo-list {
				list-style: none;
				padding: 0;
			}
			.todo-item {
				display: flex;
				align-items: center;
				gap: 12px;
				padding: 12px;
				border-bottom: 1px solid #eee;
			}
			.todo-item.completed span {
				text-decoration: line-through;
				color: #999;
			}
			.todo-item span {
				flex: 1;
			}
			.delete-btn {
				background: #e74c3c;
				color: white;
				border: none;
				padding: 4px 10px;
				border-radius: 4px;
				cursor: pointer;
			}
			.status {
				text-align: center;
				color: #666;
				margin-top: 16px;
			}
		</style>
	</head>
	<body>
		<h1>📝 To-Do List</h1>
		<div class="input-group">
			<input
				type="text"
				id="todo-input"
				placeholder="What needs to be done?"
			/>
			<button id="add-btn">Add</button>
		</div>
		<ul id="todo-list"></ul>
		<p
			class="status"
			id="status"
		></p>

		<script src="dom-manipulation.js"></script>
	</body>
</html>
```

**Starter Code (`dom-manipulation.js`):**

```javascript
const input = document.querySelector('#todo-input');
const addBtn = document.querySelector('#add-btn');
const todoList = document.querySelector('#todo-list');
const status = document.querySelector('#status');

// TODO 1: Create a function to add a new to-do item
function addTodo() {
	const text = input.value.trim();
	if (!text) return;

	// Create <li> with class "todo-item"
	// Add a checkbox, text <span>, and delete button
	// Append to the list
	// Clear the input
	// Update the status count
}

// TODO 2: Create a function to toggle complete status
function toggleComplete(item) {
	// Toggle "completed" class on the todo-item
	// Update the status count
}

// TODO 3: Create a function to delete a to-do item
function deleteTodo(item) {
	// Remove the item from the list
	// Update the status count
}

// TODO 4: Create a function to update the remaining count
function updateStatus() {
	// Count items that don't have "completed" class
	// Update the status text
}

// TODO 5: Add event listeners
// - Click "Add" button → addTodo()
// - Press Enter in input → addTodo()

updateStatus();
```

<details>
<summary>✅ Solution</summary>

```javascript
const input = document.querySelector('#todo-input');
const addBtn = document.querySelector('#add-btn');
const todoList = document.querySelector('#todo-list');
const status = document.querySelector('#status');

function addTodo() {
	const text = input.value.trim();
	if (!text) return;

	const li = document.createElement('li');
	li.className = 'todo-item';

	const checkbox = document.createElement('input');
	checkbox.type = 'checkbox';
	checkbox.addEventListener('change', () => toggleComplete(li));

	const span = document.createElement('span');
	span.textContent = text;

	const deleteBtn = document.createElement('button');
	deleteBtn.className = 'delete-btn';
	deleteBtn.textContent = '✕';
	deleteBtn.addEventListener('click', () => deleteTodo(li));

	li.append(checkbox, span, deleteBtn);
	todoList.append(li);

	input.value = '';
	input.focus();
	updateStatus();
}

function toggleComplete(item) {
	item.classList.toggle('completed');
	const checkbox = item.querySelector('input[type="checkbox"]');
	checkbox.checked = item.classList.contains('completed');
	updateStatus();
}

function deleteTodo(item) {
	item.remove();
	updateStatus();
}

function updateStatus() {
	const total = todoList.children.length;
	const completed = todoList.querySelectorAll('.completed').length;
	const remaining = total - completed;

	if (total === 0) {
		status.textContent = 'No tasks yet. Add one above!';
	} else {
		status.textContent = `${remaining} of ${total} task${total !== 1 ? 's' : ''} remaining`;
	}
}

addBtn.addEventListener('click', addTodo);
input.addEventListener('keydown', (e) => {
	if (e.key === 'Enter') addTodo();
});

updateStatus();
```

</details>

---

## ⚠️ Common Mistakes

| Mistake                            | Problem                             | Fix                                         |
| ---------------------------------- | ----------------------------------- | ------------------------------------------- |
| Using `innerHTML` with user input  | XSS security vulnerability          | Use `textContent` or `createElement`        |
| Forgetting `camelCase` for styles  | `card.style.font-size` doesn't work | Use `card.style.fontSize`                   |
| Adding elements inside a loop      | Multiple reflows = slow             | Use `DocumentFragment` or build then append |
| Not clearing inputs after use      | User has to manually clear          | `input.value = ""` after processing         |
| Removing elements that don't exist | `null.remove()` crashes             | Check `if (element)` before removing        |

---

## 📝 Session Summary

In this session, you learned:

1. **Creating elements** — `createElement`, setting properties, assembling
2. **Adding to DOM** — `append`, `prepend`, `before`, `after`, `insertAdjacentHTML`
3. **Removing elements** — `remove()`, `replaceWith()`, `replaceChildren()`
4. **classList API** — `add`, `remove`, `toggle`, `contains`, `replace`
5. **Dynamic styling** — `style` property, CSS variables, computed styles
6. **Performance** — `DocumentFragment`, `cloneNode`, batch operations

---

## 🏠 Homework

### Task 1: Card Generator

Create a page with a form (title, description, color picker). When submitted, generate a styled card and add it to a grid. Cards should have a delete button.

### Task 2: Dynamic Table Builder

Build a function that takes an array of objects and generates an HTML table with headers and rows. Add the ability to sort by clicking column headers.

### Task 3: Theme Customizer

Create a theme customizer panel with options for:

- Background color (color picker)
- Font size (range slider)
- Font family (dropdown)
- Save preferences to `localStorage`
- Load and apply on page load

### Bonus: Drag and Drop Reorder

Implement drag-and-drop list reordering using only native DOM events (no libraries).

---

## 📚 Resources

- [MDN: Document.createElement()](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement)
- [MDN: Element.classList](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList)
- [MDN: Element.insertAdjacentHTML()](https://developer.mozilla.org/en-US/docs/Web/API/Element/insertAdjacentHTML)
- [MDN: DocumentFragment](https://developer.mozilla.org/en-US/docs/Web/API/DocumentFragment)
- [JavaScript.info: Modifying the Document](https://javascript.info/modifying-document)
- [JavaScript.info: Styles and Classes](https://javascript.info/styles-and-classes)

---

**Next:** [Session 27 — Events, Forms & User Interaction](session-27.md) →
