# Week 09 — Session 27: Events, Forms & User Interaction

**Navigation:**
← [Session 26](session-26.md) | [Week 09 Index](../week-09.md) | [Session 28](../week-10/session-28.md) →

---

**Session Length:** 90 minutes

## 📋 Pre-Class Checklist

Before starting this session, make sure you have:

- ✅ Completed Sessions 25–26 (DOM selection & manipulation)
- ✅ Comfortable creating, modifying, and removing DOM elements
- ✅ Understand classList and dynamic styling
- ✅ Create: `events.html` and `events.js`

## 🎯 Learning Objectives

By the end of this session, you will be able to:

- Attach event listeners with `addEventListener`
- Handle mouse, keyboard, and form events
- Use the event object to access event details
- Explain event bubbling, capturing, and propagation
- Implement event delegation for dynamic content
- Validate and process form data with JavaScript
- Prevent default browser behavior

## 📦 Files for This Session

- `session-27.md` — This tutorial (you're reading it!)
- Create: `events.html`, `events.js`, `form-validation.html`

## 🔑 Key Terms

**event**, **event listener**, **event handler**, **addEventListener**, **removeEventListener**, **event object**, **event.target**, **event.currentTarget**, **bubbling**, **capturing**, **stopPropagation**, **preventDefault**, **event delegation**, **submit event**, **input event**, **change event**, **keydown**, **click**, **DOMContentLoaded**

## 🏗️ What You Will Build

- An interactive button with multiple event types
- A real-time form validator
- An image gallery with event delegation

---

## Part 1: Event Listeners (15 minutes)

### What Are Events?

Events are things that happen on the page — clicks, key presses, form submissions, page loads, mouse movements, and more.

### Adding Event Listeners

```javascript
const button = document.querySelector('#myButton');

// addEventListener(eventType, handlerFunction)
button.addEventListener('click', function () {
	console.log('Button clicked!');
});

// With a named function (reusable, removable)
function handleClick() {
	console.log('Button clicked!');
}
button.addEventListener('click', handleClick);

// With arrow function
button.addEventListener('click', () => {
	console.log('Button clicked!');
});
```

### Removing Event Listeners

```javascript
function handleClick() {
	console.log('Clicked!');
}

// Add
button.addEventListener('click', handleClick);

// Remove (must reference the SAME function!)
button.removeEventListener('click', handleClick);

// ❌ This WON'T work — anonymous functions can't be removed
button.addEventListener('click', () => console.log('Hi'));
// button.removeEventListener("click", () => console.log("Hi")); // different function!

// One-time listener
button.addEventListener('click', handleClick, { once: true });
// Automatically removed after first trigger
```

### Common Event Types

| Category      | Events                                                                               |
| ------------- | ------------------------------------------------------------------------------------ |
| **Mouse**     | `click`, `dblclick`, `mouseenter`, `mouseleave`, `mousemove`, `mousedown`, `mouseup` |
| **Keyboard**  | `keydown`, `keyup`, `keypress` (deprecated)                                          |
| **Form**      | `submit`, `input`, `change`, `focus`, `blur`, `reset`                                |
| **Window**    | `load`, `DOMContentLoaded`, `resize`, `scroll`                                       |
| **Touch**     | `touchstart`, `touchend`, `touchmove`                                                |
| **Clipboard** | `copy`, `paste`, `cut`                                                               |
| **Drag**      | `dragstart`, `dragend`, `dragover`, `drop`                                           |

<details>
<summary>💡 Knowledge Check #1</summary>

**Question:** Why should you use named functions instead of anonymous functions when you need to remove an event listener?

**Answer:**
`removeEventListener` requires a reference to the **exact same function** that was passed to `addEventListener`. Anonymous functions create a new function reference each time, so there's no way to reference the original one to remove it:

```javascript
// ✅ Works — same reference
function handler() {
	console.log('Hi');
}
button.addEventListener('click', handler);
button.removeEventListener('click', handler); // Same reference!

// ❌ Fails — different references
button.addEventListener('click', () => console.log('Hi'));
button.removeEventListener('click', () => console.log('Hi')); // Different function!
```

</details>

---

## Part 2: The Event Object (15 minutes)

Every event handler receives an **event object** with details about what happened:

### Mouse Events

```javascript
document.addEventListener('click', (event) => {
	// event (often abbreviated as 'e')
	console.log('Type:', event.type); // "click"
	console.log('Target:', event.target); // element that was clicked
	console.log('X:', event.clientX); // mouse X position (viewport)
	console.log('Y:', event.clientY); // mouse Y position (viewport)
	console.log('Page X:', event.pageX); // mouse X position (page)
	console.log('Page Y:', event.pageY); // mouse Y position (page)
	console.log('Button:', event.button); // 0=left, 1=middle, 2=right
	console.log('Ctrl?:', event.ctrlKey); // was Ctrl held?
	console.log('Shift?:', event.shiftKey); // was Shift held?
});
```

### Keyboard Events

```javascript
document.addEventListener('keydown', (e) => {
	console.log('Key:', e.key); // "a", "Enter", "ArrowUp", etc.
	console.log('Code:', e.code); // "KeyA", "Enter", "ArrowUp"
	console.log('Ctrl:', e.ctrlKey);
	console.log('Alt:', e.altKey);
	console.log('Shift:', e.shiftKey);
	console.log('Meta:', e.metaKey); // Cmd on Mac, Win on Windows

	// Common shortcuts
	if (e.ctrlKey && e.key === 's') {
		e.preventDefault(); // stop browser's save dialog
		console.log('Custom save!');
	}

	if (e.key === 'Escape') {
		console.log('Close modal or menu');
	}
});
```

### `event.target` vs `event.currentTarget`

```javascript
// target — the element that TRIGGERED the event
// currentTarget — the element the listener is ATTACHED to

document.querySelector('ul').addEventListener('click', (e) => {
	console.log('target:', e.target); // <li> or <a> that was clicked
	console.log('currentTarget:', e.currentTarget); // <ul> (where listener is)
});
```

### Preventing Default Behavior

```javascript
// Prevent link navigation
const link = document.querySelector('a');
link.addEventListener('click', (e) => {
	e.preventDefault(); // link won't navigate
	console.log('Link click intercepted!');
});

// Prevent form submission
const form = document.querySelector('form');
form.addEventListener('submit', (e) => {
	e.preventDefault(); // page won't reload
	console.log('Form handled by JavaScript!');
});

// Prevent right-click menu
document.addEventListener('contextmenu', (e) => {
	e.preventDefault();
	console.log('Custom context menu could go here');
});
```

<details>
<summary>💡 Knowledge Check #2</summary>

**Question:** What is the difference between `event.target` and `event.currentTarget`?

**Answer:**

- `event.target` — The **actual element** that triggered the event (the one the user clicked/typed on). Could be a child of the element with the listener.
- `event.currentTarget` — The **element the event listener is attached to**. Always the same for a given listener.

Example: If you attach a click listener to a `<ul>` and click on a `<li>` inside it:

- `event.target` = the `<li>` (what was clicked)
- `event.currentTarget` = the `<ul>` (where the listener is)

</details>

---

## Part 3: Event Bubbling & Delegation (15 minutes)

### Event Bubbling

When an event occurs, it "bubbles" up from the target element through its ancestors:

```html
<div id="outer">
	<div id="inner">
		<button id="btn">Click Me</button>
	</div>
</div>
```

```javascript
document.querySelector('#outer').addEventListener('click', () => {
	console.log('Outer clicked');
});

document.querySelector('#inner').addEventListener('click', () => {
	console.log('Inner clicked');
});

document.querySelector('#btn').addEventListener('click', () => {
	console.log('Button clicked');
});

// Clicking the button logs:
// "Button clicked"  (target)
// "Inner clicked"   (bubbles up)
// "Outer clicked"   (bubbles up more)
```

### Stopping Propagation

```javascript
document.querySelector('#btn').addEventListener('click', (e) => {
	e.stopPropagation(); // stops bubbling here
	console.log('Button clicked — stopped propagation');
});
// Now clicking the button only logs the button's handler
```

### Event Delegation

Instead of adding listeners to many elements, add ONE listener to the parent:

```javascript
// ❌ Inefficient — listener on EACH item
document.querySelectorAll('.nav-item').forEach((item) => {
	item.addEventListener('click', () => {
		console.log(item.textContent);
	});
});

// ✅ Efficient — ONE listener on the parent
document.querySelector('#nav-list').addEventListener('click', (e) => {
	const item = e.target.closest('.nav-item');
	if (!item) return; // clicked somewhere else in the list

	console.log(item.textContent);

	// Remove active from all, add to clicked
	document
		.querySelectorAll('.nav-item')
		.forEach((i) => i.classList.remove('active'));
	item.classList.add('active');
});
```

### Why Event Delegation?

1. **Works with dynamic content** — new elements added later are automatically handled
2. **Better performance** — one listener instead of hundreds
3. **Less memory** — fewer function references in memory
4. **Simpler management** — one place to add/remove the listener

```javascript
// Dynamic content example — delegation handles items that don't exist yet!
const list = document.querySelector('#todo-list');

list.addEventListener('click', (e) => {
	// Handle delete button clicks on any item (even future ones)
	if (e.target.classList.contains('delete-btn')) {
		e.target.closest('.todo-item').remove();
	}

	// Handle toggle clicks
	if (e.target.type === 'checkbox') {
		e.target.closest('.todo-item').classList.toggle('completed');
	}
});

// Adding new items after the listener — they're automatically handled!
function addItem(text) {
	list.insertAdjacentHTML(
		'beforeend',
		`
    <li class="todo-item">
      <input type="checkbox">
      <span>${text}</span>
      <button class="delete-btn">✕</button>
    </li>
  `,
	);
}
```

<details>
<summary>💡 Knowledge Check #3</summary>

**Question:** What is event delegation and why would you use it?

**Answer:**
Event delegation is a pattern where you attach a **single event listener to a parent element** instead of individual listeners on each child. It works because of event bubbling — clicks "bubble up" to the parent.

**Benefits:**

1. Handles **dynamic content** (new elements work automatically)
2. **Better performance** (1 listener vs 100+)
3. Less memory usage
4. Cleaner code (one handler, not many)

**Pattern:**

```javascript
parent.addEventListener('click', (e) => {
	const target = e.target.closest('.child-selector');
	if (!target) return;
	// handle the event
});
```

</details>

---

## Part 4: Form Events & Validation (15 minutes)

### Form Event Types

```javascript
const form = document.querySelector('form');
const emailInput = document.querySelector('#email');

// submit — when form is submitted
form.addEventListener('submit', (e) => {
	e.preventDefault();
	const formData = new FormData(form);
	console.log('Email:', formData.get('email'));
});

// input — fires on EVERY keystroke/change
emailInput.addEventListener('input', (e) => {
	console.log('Current value:', e.target.value);
});

// change — fires when value changes AND element loses focus
emailInput.addEventListener('change', (e) => {
	console.log('Final value:', e.target.value);
});

// focus — element receives focus
emailInput.addEventListener('focus', () => {
	emailInput.classList.add('focused');
});

// blur — element loses focus
emailInput.addEventListener('blur', () => {
	emailInput.classList.remove('focused');
	// Validate on blur
	validateEmail(emailInput.value);
});
```

### Reading Form Data

```javascript
form.addEventListener('submit', (e) => {
	e.preventDefault();

	// Method 1: Access fields directly
	const name = document.querySelector('#name').value;
	const email = document.querySelector('#email').value;

	// Method 2: FormData API
	const formData = new FormData(form);
	const data = Object.fromEntries(formData);
	console.log(data); // { name: "Alice", email: "alice@..." }

	// Method 3: form.elements
	console.log(form.elements.name.value);
	console.log(form.elements.email.value);
});
```

### Real-Time Validation

```javascript
function validateField(input, validationFn, errorMsg) {
	const errorEl = input.nextElementSibling; // <span class="error"> after input

	input.addEventListener('input', () => {
		if (validationFn(input.value)) {
			input.classList.remove('invalid');
			input.classList.add('valid');
			if (errorEl) errorEl.textContent = '';
		} else {
			input.classList.remove('valid');
			input.classList.add('invalid');
			if (errorEl) errorEl.textContent = errorMsg;
		}
	});
}

// Usage
const nameInput = document.querySelector('#name');
validateField(
	nameInput,
	(value) => value.trim().length >= 2,
	'Name must be at least 2 characters',
);

const emailInput = document.querySelector('#email');
validateField(
	emailInput,
	(value) => /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(value),
	'Please enter a valid email address',
);

const passwordInput = document.querySelector('#password');
validateField(
	passwordInput,
	(value) => value.length >= 8,
	'Password must be at least 8 characters',
);
```

### Complete Form Validation on Submit

```javascript
form.addEventListener('submit', (e) => {
	e.preventDefault();

	const errors = [];
	const name = form.elements.name.value.trim();
	const email = form.elements.email.value.trim();
	const password = form.elements.password.value;

	if (name.length < 2) errors.push('Name must be at least 2 characters');
	if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)) errors.push('Invalid email');
	if (password.length < 8) errors.push('Password must be 8+ characters');

	if (errors.length > 0) {
		const errorList = document.querySelector('#errors');
		errorList.innerHTML = errors.map((e) => `<li>${e}</li>`).join('');
		return;
	}

	// All valid — process the form
	console.log('Form submitted!', { name, email, password });
	form.reset();
});
```

---

## Part 5: Page Load & Timing Events (5 minutes)

### DOMContentLoaded vs load

```javascript
// DOMContentLoaded — DOM is ready (HTML parsed, scripts loaded)
// Fires BEFORE images and stylesheets finish loading
document.addEventListener('DOMContentLoaded', () => {
	console.log('DOM ready!');
	// Safe to select elements here
});

// load — EVERYTHING is loaded (images, stylesheets, iframes)
window.addEventListener('load', () => {
	console.log('Everything loaded!');
});

// If script has `defer` attribute, DOM is already ready — no need for DOMContentLoaded
```

### Scroll & Resize

```javascript
// Scroll — fires frequently! Use throttling in production
window.addEventListener('scroll', () => {
	const scrollY = window.scrollY;
	const header = document.querySelector('header');

	if (scrollY > 100) {
		header.classList.add('scrolled');
	} else {
		header.classList.remove('scrolled');
	}
});

// Resize
window.addEventListener('resize', () => {
	console.log(`Window: ${window.innerWidth}x${window.innerHeight}`);
});
```

---

## Part 6: Lab — Interactive Image Gallery (15 minutes)

### Challenge

Build a simple image gallery with:

1. Thumbnail images that enlarge when clicked
2. A modal/lightbox overlay
3. Keyboard navigation (Escape to close, Arrow keys to navigate)
4. Event delegation for thumbnails

**Starter Code:**

```javascript
// Image Gallery with Event Delegation

const images = [
	{ src: 'https://picsum.photos/id/10/600/400', alt: 'Forest' },
	{ src: 'https://picsum.photos/id/20/600/400', alt: 'Mountains' },
	{ src: 'https://picsum.photos/id/30/600/400', alt: 'Ocean' },
	{ src: 'https://picsum.photos/id/40/600/400', alt: 'Desert' },
	{ src: 'https://picsum.photos/id/50/600/400', alt: 'City' },
	{ src: 'https://picsum.photos/id/60/600/400', alt: 'Sunset' },
];

let currentIndex = 0;

// TODO 1: Generate gallery thumbnails from the images array

// TODO 2: Create a modal overlay element dynamically

// TODO 3: Use event delegation on the gallery container for thumbnail clicks

// TODO 4: Show the modal with the full-size image

// TODO 5: Close modal on Escape key and overlay click

// TODO 6: Navigate with Arrow keys when modal is open
```

<details>
<summary>✅ Solution</summary>

```javascript
const images = [
	{ src: 'https://picsum.photos/id/10/600/400', alt: 'Forest' },
	{ src: 'https://picsum.photos/id/20/600/400', alt: 'Mountains' },
	{ src: 'https://picsum.photos/id/30/600/400', alt: 'Ocean' },
	{ src: 'https://picsum.photos/id/40/600/400', alt: 'Desert' },
	{ src: 'https://picsum.photos/id/50/600/400', alt: 'City' },
	{ src: 'https://picsum.photos/id/60/600/400', alt: 'Sunset' },
];

let currentIndex = 0;

// 1. Generate thumbnails
const gallery = document.querySelector('#gallery');
images.forEach((img, i) => {
	gallery.insertAdjacentHTML(
		'beforeend',
		`
    <img src="${img.src}" alt="${img.alt}" class="thumbnail" data-index="${i}"
         style="width:150px; height:100px; object-fit:cover; cursor:pointer; border-radius:8px;">
  `,
	);
});

// 2. Create modal
const modal = document.createElement('div');
modal.id = 'modal';
modal.style.cssText = `
  display:none; position:fixed; top:0; left:0; width:100%; height:100%;
  background:rgba(0,0,0,0.9); justify-content:center; align-items:center;
  z-index:1000; cursor:pointer;
`;
modal.innerHTML = `<img id="modal-img" style="max-width:90%; max-height:90%; border-radius:8px;">`;
document.body.append(modal);

const modalImg = document.querySelector('#modal-img');

// 3. Event delegation for thumbnails
gallery.addEventListener('click', (e) => {
	const thumb = e.target.closest('.thumbnail');
	if (!thumb) return;

	currentIndex = parseInt(thumb.dataset.index);
	showModal(currentIndex);
});

// 4. Show modal
function showModal(index) {
	modalImg.src = images[index].src;
	modalImg.alt = images[index].alt;
	modal.style.display = 'flex';
}

function closeModal() {
	modal.style.display = 'none';
}

// 5. Close on click and Escape
modal.addEventListener('click', (e) => {
	if (e.target === modal) closeModal();
});

document.addEventListener('keydown', (e) => {
	if (modal.style.display !== 'flex') return;

	if (e.key === 'Escape') closeModal();
	if (e.key === 'ArrowRight') {
		currentIndex = (currentIndex + 1) % images.length;
		showModal(currentIndex);
	}
	if (e.key === 'ArrowLeft') {
		currentIndex = (currentIndex - 1 + images.length) % images.length;
		showModal(currentIndex);
	}
});
```

</details>

---

## ⚠️ Common Mistakes

| Mistake                                     | Problem                         | Fix                                                 |
| ------------------------------------------- | ------------------------------- | --------------------------------------------------- |
| Forgetting `e.preventDefault()` on forms    | Page reloads on submit          | Always call it in submit handlers                   |
| Anonymous functions for removable listeners | Can't remove them               | Use named functions                                 |
| Not checking `e.target` in delegation       | Handler runs for any click      | Use `e.target.closest(".selector")` with null check |
| Attaching listeners inside loops            | Creates duplicates on re-render | Use delegation or track listeners                   |
| Not debouncing `scroll`/`resize`            | Performance issues              | Throttle or debounce rapid-fire events              |

---

## 📝 Session Summary

In this session, you learned:

1. **addEventListener** — Attach handlers for any event type
2. **Event object** — `target`, `currentTarget`, `key`, `preventDefault()`
3. **Bubbling & capturing** — Events propagate up through the DOM tree
4. **Event delegation** — One parent listener instead of many child listeners
5. **Form events** — `submit`, `input`, `change`, `focus`, `blur`
6. **Form validation** — Real-time validation with visual feedback
7. **Keyboard events** — `keydown`, modifier keys, keyboard shortcuts

---

## 🏠 Homework

### Task 1: Interactive Quiz

Build a multiple-choice quiz with:

- Questions displayed one at a time
- Radio button answers
- Next/Previous navigation
- Score calculation and display at the end
- Use event delegation for answer selection

### Task 2: Live Search Filter

Create a search box that filters a list of items in real-time:

- Highlight matching text
- Show "no results" message when nothing matches
- Debounce the input event (wait 300ms after typing stops)

### Task 3: Form Wizard

Build a multi-step form with:

- Step 1: Personal info (name, email)
- Step 2: Preferences (checkboxes, radio buttons)
- Step 3: Review & submit
- Validate each step before allowing progression
- Show a progress indicator

### Bonus: Custom Dropdown

Build a custom dropdown/select component from scratch:

- Click to open/close
- Keyboard navigation (Arrow keys, Enter, Escape)
- Close when clicking outside
- Custom styling (unlike native `<select>`)

---

## 📚 Resources

- [MDN: Introduction to Events](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events)
- [MDN: addEventListener](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)
- [MDN: Event Reference](https://developer.mozilla.org/en-US/docs/Web/Events)
- [MDN: FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData)
- [JavaScript.info: Introduction to Browser Events](https://javascript.info/introduction-browser-events)
- [JavaScript.info: Bubbling and Capturing](https://javascript.info/bubbling-and-capturing)
- [JavaScript.info: Event Delegation](https://javascript.info/event-delegation)

---

**Next:** [Session 28 — Modern ES6+ Features](../week-10/session-28.md) →
