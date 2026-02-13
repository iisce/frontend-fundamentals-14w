# Week 09 — The DOM & Event-Driven Programming

> _"Making web pages alive — selecting, changing, and responding to user actions."_

This is where JavaScript meets the browser. You will learn to select HTML elements, change their content and styles dynamically, create and remove elements on the fly, and respond to user interactions like clicks, typing, and form submissions.

---

## Overview

-   **Focus:** DOM selection, manipulation, traversal, event handling, event delegation, and form interaction
-   **Prerequisites:** Weeks 07–08 (variables, functions, arrays, objects)
-   **Outcomes by end of week:**
    -   Understand the DOM tree structure and how browsers build it
    -   Select elements using `getElementById`, `querySelector`, and `querySelectorAll`
    -   Traverse the DOM tree using parent, child, and sibling properties
    -   Modify content, attributes, classes, and styles dynamically
    -   Create, insert, and remove DOM elements programmatically
    -   Attach event listeners and handle user interactions
    -   Understand event bubbling, capturing, and delegation
    -   Build interactive, event-driven web applications

---

## Sessions

### Session 25 — DOM Fundamentals & Selection (90 min)

**Learning Objectives:**
-   Explain what the DOM is and how the browser constructs it
-   Select single and multiple elements using various methods
-   Traverse the DOM tree using relationship properties
-   Read element content, attributes, and properties

**Topics Covered:**

| Topic | Duration | Details |
|-------|----------|---------|
| What Is the DOM? | 15 min | Document Object Model, browser parsing HTML → DOM tree, `document` object, DOM vs HTML source, live vs static node lists |
| Selecting Single Elements | 15 min | `document.getElementById("id")`, `document.querySelector("css-selector")`, returns first match or null, using compound selectors |
| Selecting Multiple Elements | 15 min | `document.querySelectorAll("selector")` returns a static NodeList, `document.getElementsByClassName()`, `document.getElementsByTagName()`, iterating NodeLists |
| DOM Traversal | 15 min | `parentElement`, `children`, `firstElementChild`, `lastElementChild`, `nextElementSibling`, `previousElementSibling`, `closest()` |
| Reading Element Data | 15 min | `textContent` vs `innerText` vs `innerHTML`, `getAttribute()`, `dataset` (data-* attributes), `id`, `className`, `classList` |
| Lab: DOM Explorer | 15 min | Build a page, select elements in the console, traverse the tree, read content and attributes |

**Key Code Examples:**

```html
<!-- Sample HTML for DOM practice -->
<div id="app">
  <header class="site-header">
    <h1>My Website</h1>
    <nav>
      <ul id="nav-list">
        <li class="nav-item active"><a href="#">Home</a></li>
        <li class="nav-item"><a href="#">About</a></li>
        <li class="nav-item"><a href="#">Contact</a></li>
      </ul>
    </nav>
  </header>
  <main>
    <section class="hero" data-page="home">
      <h2>Welcome!</h2>
      <p id="hero-text">This is a dynamic page.</p>
    </section>
  </main>
</div>
```

```javascript
// Selecting elements
const heading = document.getElementById("hero-text");
const navItems = document.querySelectorAll(".nav-item");
const firstLink = document.querySelector("nav a");
const hero = document.querySelector("[data-page='home']");

// Reading content
console.log(heading.textContent);      // "This is a dynamic page."
console.log(hero.dataset.page);        // "home"
console.log(firstLink.getAttribute("href")); // "#"

// Traversal
const navList = document.getElementById("nav-list");
console.log(navList.children);             // HTMLCollection of 3 <li> elements
console.log(navList.firstElementChild);    // first <li>
console.log(navList.lastElementChild);     // last <li>

const aboutItem = navItems[1];
console.log(aboutItem.parentElement);          // <ul>
console.log(aboutItem.previousElementSibling); // first <li>
console.log(aboutItem.nextElementSibling);     // last <li>

// closest() — find nearest ancestor matching selector
const link = document.querySelector("nav a");
const closestList = link.closest("ul"); // <ul id="nav-list">

// Iterating NodeLists
navItems.forEach((item, index) => {
  console.log(`Item ${index}: ${item.textContent}`);
});
```

**Homework:**
-   Create an HTML page with a navigation bar, hero section, and a list of cards
-   Write a JS file that selects and logs: all nav links, the hero heading, card count
-   Use traversal to find the parent of a specific card, its siblings, and its first child
-   Challenge: Write a function `findAllByText(text)` that returns all elements containing that text

---

### Session 26 — DOM Manipulation & Styling (90 min)

**Learning Objectives:**
-   Change element content using `textContent` and `innerHTML`
-   Modify attributes and classes dynamically
-   Create new elements and insert them into the DOM
-   Remove elements from the DOM
-   Change styles programmatically

**Topics Covered:**

| Topic | Duration | Details |
|-------|----------|---------|
| Changing Content | 10 min | `textContent` (plain text), `innerHTML` (parsed HTML), XSS security warning with innerHTML |
| Modifying Attributes | 10 min | `setAttribute()`, `removeAttribute()`, `id`, `src`, `href`, `alt`, `data-*` attributes |
| Working with Classes | 15 min | `classList.add()`, `classList.remove()`, `classList.toggle()`, `classList.contains()`, `classList.replace()`, toggling UI states |
| Creating Elements | 15 min | `document.createElement("tag")`, setting properties before inserting, `append()`, `prepend()`, `before()`, `after()`, `insertAdjacentHTML()` |
| Removing Elements | 10 min | `element.remove()`, `parent.removeChild(child)`, removing all children |
| Dynamic Styling | 15 min | `element.style.property` (camelCase), `getComputedStyle()`, CSS custom properties with JS, toggling themes |
| Lab: Dynamic List Builder | 15 min | Build a dynamic list where users can add items, remove items, and toggle a "completed" state |

**Key Code Examples:**

```javascript
// Changing content
const heading = document.querySelector("h2");
heading.textContent = "Updated Heading!";

// Modifying classes — toggling dark mode
const body = document.body;
body.classList.toggle("dark-mode");

// Creating and inserting elements
function addCard(title, description) {
  const card = document.createElement("div");
  card.classList.add("card");
  
  const h3 = document.createElement("h3");
  h3.textContent = title;
  
  const p = document.createElement("p");
  p.textContent = description;
  
  const deleteBtn = document.createElement("button");
  deleteBtn.textContent = "Delete";
  deleteBtn.classList.add("btn-delete");
  
  card.append(h3, p, deleteBtn);
  document.querySelector(".card-container").append(card);
  
  return card;
}

addCard("JavaScript", "Learn DOM manipulation");
addCard("CSS", "Master responsive layouts");

// Removing elements
const removeBtn = document.querySelector(".btn-delete");
removeBtn.addEventListener("click", () => {
  removeBtn.closest(".card").remove();
});

// Dynamic styling
const hero = document.querySelector(".hero");
hero.style.backgroundColor = "#1a1a2e";
hero.style.color = "#eee";
hero.style.padding = "2rem";
hero.style.borderRadius = "12px";

// Toggling theme with CSS custom properties
function setTheme(theme) {
  const root = document.documentElement;
  if (theme === "dark") {
    root.style.setProperty("--bg-color", "#1a1a2e");
    root.style.setProperty("--text-color", "#eee");
  } else {
    root.style.setProperty("--bg-color", "#ffffff");
    root.style.setProperty("--text-color", "#333");
  }
}

// Building a list dynamically from data
const tasks = ["Learn HTML", "Master CSS", "Study JavaScript"];
const ul = document.createElement("ul");

tasks.forEach(task => {
  const li = document.createElement("li");
  li.textContent = task;
  ul.append(li);
});

document.querySelector("main").append(ul);
```

**Homework:**
-   Build a **Color Palette Generator**: create 5 random colored boxes, display hex codes, click to copy
-   Build a **Dynamic Card List**: add cards from a form, each card has a delete button
-   Use `classList.toggle()` to implement a dark/light theme switch
-   Challenge: Implement an "Edit in place" feature — click text to turn it into an input, press Enter to save

---

### Session 27 — Events, Forms & User Interaction (90 min)

**Learning Objectives:**
-   Attach event listeners using `addEventListener()`
-   Use the event object and its properties
-   Prevent default browser behavior with `event.preventDefault()`
-   Understand event bubbling, capturing, and delegation
-   Handle keyboard, mouse, and form events
-   Validate form input using JavaScript

**Topics Covered:**

| Topic | Duration | Details |
|-------|----------|---------|
| addEventListener() | 10 min | Syntax, event types (`click`, `input`, `submit`, `keydown`), removing listeners, the `once` option |
| The Event Object | 10 min | `event.target`, `event.currentTarget`, `event.type`, `event.key`, `event.clientX/Y`, `event.detail` |
| preventDefault() | 10 min | Stopping form submission, stopping link navigation, when and why to use it |
| Event Bubbling & Capturing | 15 min | Bubble phase (default), capture phase, `event.stopPropagation()`, event flow diagram |
| Event Delegation | 10 min | Attaching one listener to a parent, checking `event.target`, dynamic elements benefit, performance advantage |
| Form Events & Validation | 20 min | `submit` event, `input` event, `change` event, `FormData`, real-time validation, providing feedback |
| Lab: Interactive To-Do List | 15 min | Build a to-do list: add tasks from a form, mark as complete (toggle), delete tasks, count remaining |

**Key Code Examples:**

```javascript
// Basic event listener
const button = document.querySelector("#myBtn");
button.addEventListener("click", (event) => {
  console.log("Button clicked!");
  console.log("Target:", event.target);
  console.log("Mouse position:", event.clientX, event.clientY);
});

// Form handling with preventDefault
const form = document.querySelector("#contact-form");
form.addEventListener("submit", (event) => {
  event.preventDefault(); // Stop page reload
  
  const formData = new FormData(form);
  const data = Object.fromEntries(formData);
  console.log("Form data:", data);
  
  // Validate
  if (!data.name || data.name.trim().length < 2) {
    showError("name", "Name must be at least 2 characters");
    return;
  }
  
  if (!data.email || !data.email.includes("@")) {
    showError("email", "Please enter a valid email");
    return;
  }
  
  console.log("Form is valid! Submitting...", data);
  form.reset();
});

// Real-time validation on input
const emailInput = document.querySelector("#email");
emailInput.addEventListener("input", (event) => {
  const value = event.target.value;
  const feedback = document.querySelector("#email-feedback");
  
  if (value && !value.includes("@")) {
    feedback.textContent = "Please include an @ symbol";
    feedback.style.color = "red";
  } else {
    feedback.textContent = "Looks good!";
    feedback.style.color = "green";
  }
});

// Event delegation — handle clicks on dynamic list items
const todoList = document.querySelector("#todo-list");

todoList.addEventListener("click", (event) => {
  const target = event.target;
  
  // Handle delete button clicks
  if (target.classList.contains("delete-btn")) {
    target.closest("li").remove();
    updateCount();
    return;
  }
  
  // Handle clicking on list item to toggle complete
  if (target.tagName === "LI" || target.closest("li")) {
    const li = target.closest("li");
    li.classList.toggle("completed");
    updateCount();
  }
});

// Keyboard events
document.addEventListener("keydown", (event) => {
  console.log(`Key pressed: ${event.key}, Code: ${event.code}`);
  
  // Keyboard shortcuts
  if (event.ctrlKey && event.key === "s") {
    event.preventDefault();
    console.log("Custom save action!");
  }
});

// Complete To-Do App example
function addTodo(text) {
  const li = document.createElement("li");
  li.innerHTML = `
    <span class="todo-text">${text}</span>
    <button class="delete-btn" aria-label="Delete ${text}">×</button>
  `;
  todoList.append(li);
  updateCount();
}

function updateCount() {
  const total = todoList.children.length;
  const completed = todoList.querySelectorAll(".completed").length;
  const remaining = total - completed;
  document.querySelector("#todo-count").textContent = 
    `${remaining} task${remaining !== 1 ? "s" : ""} remaining`;
}

// Add todo from form
const todoForm = document.querySelector("#todo-form");
todoForm.addEventListener("submit", (event) => {
  event.preventDefault();
  const input = todoForm.querySelector("input");
  const text = input.value.trim();
  if (text) {
    addTodo(text);
    input.value = "";
    input.focus();
  }
});
```

**Homework:**
-   Complete the **Interactive To-Do List** with add, delete, toggle complete, and remaining count
-   Build a **Form Validator** with real-time feedback (check name length, email format, password strength)
-   Add keyboard navigation: pressing Enter in the input adds a todo, pressing Escape clears input
-   Challenge: Implement drag-and-drop reordering of todo items using mouse events

---

## Week 09 Summary

By the end of this week, students can:

| Skill | Status |
|-------|--------|
| Select DOM elements with querySelector/All | ✅ |
| Traverse the DOM tree | ✅ |
| Modify content, attributes, and classes | ✅ |
| Create and remove elements dynamically | ✅ |
| Change styles programmatically | ✅ |
| Attach and remove event listeners | ✅ |
| Use the event object and preventDefault | ✅ |
| Implement event delegation | ✅ |
| Handle form submissions with validation | ✅ |
| Build complete interactive applications | ✅ |

## Resources

-   [MDN: Introduction to the DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction)
-   [MDN: Document.querySelector()](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)
-   [MDN: EventTarget.addEventListener()](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)
-   [MDN: Event Bubbling and Capturing](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#event_bubbling)
-   [JavaScript.info: Document](https://javascript.info/document)
-   [JavaScript.info: Events](https://javascript.info/events)
