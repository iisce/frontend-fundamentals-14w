# Week 07 — Session 19: Introduction to JavaScript & Developer Tools

**Navigation:**
← [Week 06 Session 18](../week-06/session-18.md) | [Week 07 Index](../week-07.md) | [Session 20](session-20.md) →

---

**Session Length:** 90 minutes

## 📋 Pre-Class Checklist

Before starting this session, make sure you have:

- ✅ Completed HTML & CSS fundamentals (Weeks 01–06)
- ✅ Code editor (VS Code) installed with Live Server extension
- ✅ A modern browser with Developer Tools (Chrome, Firefox, or Edge)
- ✅ Create a new folder: `week-07-js-basics`
- ✅ Inside that folder, create: `index.html` and `script.js`

## 🎯 Learning Objectives

By the end of this session, you will be able to:

- Explain what JavaScript is and its role alongside HTML and CSS
- Understand where JavaScript runs (browser engine, Node.js)
- Add JavaScript to HTML pages using three methods (inline, internal, external)
- Use browser developer tools effectively (Console, Sources tab)
- Write your first JavaScript statements using `console.log()`, `alert()`, and `prompt()`
- Understand script loading strategies (`defer`, `async`, placement)

## 📦 Files for This Session

- `session-19.md` — This tutorial (you're reading it!)
- Practice files you'll create during the session

## 🔑 Key Terms

**JavaScript**, **ECMAScript**, **script tag**, **console**, **REPL**, **`console.log()`**, **`alert()`**, **`prompt()`**, **`confirm()`**, **`defer`**, **`async`**, **Developer Tools**, **client-side**, **server-side**

## 🏗️ What You Will Build

- A page that greets users by name
- An interactive "About Me" generator
- A mini number guessing game using `prompt()` and `alert()`

---

## Part 1: What is JavaScript? (15 minutes)

### The Three Languages of the Web

Every website you visit is built with three core languages working together:

| Language       | Role                     | Analogy                           |
| -------------- | ------------------------ | --------------------------------- |
| **HTML**       | Structure & Content      | The skeleton and organs of a body |
| **CSS**        | Styling & Layout         | The clothes, hair, and appearance |
| **JavaScript** | Behavior & Interactivity | The muscles, reflexes, and brain  |

**Without JavaScript**, a website is like a beautiful poster — you can look at it, but you can't interact with it.

**With JavaScript**, you can:

- ✅ Respond to clicks, typing, scrolling
- ✅ Show/hide content dynamically
- ✅ Validate form input before submission
- ✅ Fetch data from servers (APIs)
- ✅ Build games, animations, and apps
- ✅ Update the page without reloading

### A Brief History

- **1995** — Brendan Eich created JavaScript at Netscape in just 10 days
- **1997** — Standardized as ECMAScript (ES1)
- **2009** — Node.js released — JavaScript can now run on servers
- **2015** — ES6 (ES2015) — Massive update that modernized the language
- **Today** — JavaScript is the most widely-used programming language in the world

### Where Does JavaScript Run?

```
┌─────────────────────────────────────────────┐
│              JavaScript Runs In:            │
├─────────────────┬───────────────────────────┤
│   🌐 Browser    │   🖥️ Server (Node.js)     │
│                 │                           │
│  - Chrome (V8)  │  - Web servers            │
│  - Firefox      │  - APIs                   │
│    (SpiderMon.) │  - Command-line tools     │
│  - Safari       │  - Desktop apps           │
│    (JavaScrCore)│    (Electron)             │
│  - Edge (V8)    │  - Mobile apps            │
│                 │    (React Native)         │
└─────────────────┴───────────────────────────┘
```

> ⚡ **For this course**, we focus on **client-side JavaScript** — code that runs in the browser.

<details>
<summary>💡 Knowledge Check #1</summary>

**Question:** What are the three core languages of the web, and what does each do?

**Answer:**

- **HTML** — Provides structure and content (headings, paragraphs, images, links)
- **CSS** — Controls visual presentation (colors, layout, fonts, spacing)
- **JavaScript** — Adds behavior and interactivity (responding to events, updating the page)

</details>

---

## Part 2: Adding JavaScript to HTML (15 minutes)

There are three ways to add JavaScript to a web page, just like CSS has inline, internal, and external methods.

### Method 1: Inline JavaScript (Avoid)

Add JavaScript directly on HTML elements using event attributes:

```html
<button onclick="alert('Hello!')">Click Me</button>
<a
	href="#"
	onmouseover="console.log('Hovered!')"
	>Hover Me</a
>
```

**Pros:**

- ✅ Quick for testing

**Cons:**

- ❌ Mixes HTML and JavaScript (hard to maintain)
- ❌ Can't reuse code
- ❌ Security concerns
- ❌ Difficult to debug

**When to use:** Almost never. Only for very quick tests.

### Method 2: Internal JavaScript

Add JavaScript inside `<script>` tags in your HTML file:

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta
			name="viewport"
			content="width=device-width, initial-scale=1.0"
		/>
		<title>Internal JS Example</title>
	</head>
	<body>
		<h1>My Page</h1>
		<p id="greeting">Hello!</p>

		<script>
			// JavaScript code goes here
			console.log('Page loaded successfully!');
			document.getElementById('greeting').textContent =
				'Hello from JavaScript!';
		</script>
	</body>
</html>
```

**Pros:**

- ✅ Everything in one file
- ✅ Good for small projects or examples

**Cons:**

- ❌ Not reusable across pages
- ❌ Makes HTML file longer

**When to use:** Small demos, prototypes, or learning exercises.

### Method 3: External JavaScript (Best Practice ✅)

Create a separate `.js` file and link it to your HTML:

**File: `script.js`**

```javascript
// This is an external JavaScript file
console.log('External script loaded!');
```

**File: `index.html`**

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta
			name="viewport"
			content="width=device-width, initial-scale=1.0"
		/>
		<title>External JS Example</title>
		<script
			src="script.js"
			defer
		></script>
	</head>
	<body>
		<h1>My Page</h1>
		<p id="output">Waiting for JavaScript...</p>
	</body>
</html>
```

**Pros:**

- ✅ Reusable across many pages
- ✅ Separates concerns (HTML vs JS)
- ✅ Easier to maintain and debug
- ✅ Browser can cache the file

**Cons:**

- ❌ Extra file to manage

**When to use:** Almost always. This is the industry standard.

### Script Loading: `defer` vs `async`

Where you place your `<script>` tag matters:

```html
<!-- Option A: At the end of <body> (traditional) -->
<body>
	<h1>Content loads first</h1>
	<script src="script.js"></script>
</body>

<!-- Option B: In <head> with defer (modern best practice) -->
<head>
	<script
		src="script.js"
		defer
	></script>
</head>

<!-- Option C: In <head> with async (for independent scripts) -->
<head>
	<script
		src="analytics.js"
		async
	></script>
</head>
```

| Attribute | HTML Parsing | Script Execution  | Order Guaranteed? |
| --------- | ------------ | ----------------- | ----------------- |
| (none)    | ⏸️ Pauses    | Immediately       | Yes               |
| `defer`   | ✅ Continues | After HTML parsed | Yes               |
| `async`   | ✅ Continues | When downloaded   | No                |

> 🏆 **Best practice:** Use `<script src="script.js" defer></script>` in the `<head>`.

<details>
<summary>💡 Knowledge Check #2</summary>

**Question:** Why is `defer` better than placing the script at the end of `<body>`?

**Answer:** With `defer`, the browser starts downloading the JavaScript file while parsing HTML (in parallel), but waits to execute it until after the HTML is fully parsed. This means faster page loads compared to placing the script at the end of `<body>`, where the download doesn't start until the browser reaches that point.

</details>

### Quick Practice: Set Up Your Project

1. Open your `week-07-js-basics` folder in VS Code
2. Create `index.html` with this starter:

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta
			name="viewport"
			content="width=device-width, initial-scale=1.0"
		/>
		<title>Week 07 — JavaScript Basics</title>
		<script
			src="script.js"
			defer
		></script>
	</head>
	<body>
		<h1>JavaScript Fundamentals</h1>
		<p id="output">Check the console!</p>
	</body>
</html>
```

3. Create `script.js` with:

```javascript
console.log('✅ script.js is connected!');
```

4. Open with Live Server and check the browser console (F12 → Console tab)

---

## Part 3: Browser Developer Tools (20 minutes)

The browser Developer Tools (DevTools) are your **best friend** for JavaScript development. You'll use them constantly.

### Opening DevTools

| Method      | Windows/Linux               | Mac                          |
| ----------- | --------------------------- | ---------------------------- |
| Keyboard    | `F12` or `Ctrl+Shift+I`     | `Cmd+Option+I`               |
| Right-click | Right-click → Inspect       | Right-click → Inspect        |
| Menu        | ☰ → More Tools → Dev Tools | View → Developer → Dev Tools |

### The Console Tab

The Console is an interactive **REPL** (Read-Eval-Print Loop) — you type JavaScript, it runs immediately.

**Try these in the Console:**

```javascript
// Basic math
2 + 2; // 4
10 * 5; // 50
100 / 3; // 33.333...

// Strings
'Hello' + ' ' + 'World'; // "Hello World"
'JavaScript'.length; // 10
'hello'.toUpperCase(); // "HELLO"

// Quick experiments
Math.random(); // random number 0–1
Math.floor(Math.random() * 6) + 1; // dice roll (1–6)
Date(); // current date/time
```

### Console Methods

Beyond `console.log()`, there are several useful methods:

```javascript
// Standard output
console.log('Regular message');

// Warning (yellow)
console.warn('This is a warning!');

// Error (red)
console.error('Something went wrong!');

// Informational
console.info('FYI: This is informational');

// Table format (great for arrays/objects)
console.table(['Apple', 'Banana', 'Cherry']);

// Grouping related logs
console.group('User Details');
console.log('Name: Alice');
console.log('Age: 25');
console.groupEnd();

// Timing
console.time('loop');
for (let i = 0; i < 1000000; i++) {} // do something
console.timeEnd('loop'); // "loop: 3.45ms"

// Clearing the console
console.clear();
```

### The Sources Tab

The Sources tab lets you:

- View your JavaScript files
- Set **breakpoints** (pause execution at a specific line)
- Step through code line by line
- Inspect variables at each step

> 💡 We'll use breakpoints more in later sessions. For now, focus on the Console.

<details>
<summary>💡 Knowledge Check #3</summary>

**Question:** What is the difference between `console.log()`, `console.warn()`, and `console.error()`?

**Answer:**

- `console.log()` — Standard output, white/default color
- `console.warn()` — Warning message, displayed in yellow with ⚠️ icon
- `console.error()` — Error message, displayed in red with ❌ icon

All three output to the Console, but with different visual styling to help you identify the severity of the message.

</details>

### Quick Practice: Console Exploration

Open the browser console and try each of these. Write down what each returns:

```javascript
// 1. String operations
'Frontend' + ' ' + 'Fundamentals';
'JavaScript'.includes('Script');
'hello world'.split(' ');

// 2. Math operations
Math.PI;
Math.max(10, 25, 3, 42, 18);
Math.round(4.7);

// 3. Fun experiments
typeof 42;
typeof 'hello';
typeof true;
typeof undefined;
```

---

## Part 4: Your First JavaScript Programs (25 minutes)

### `console.log()` — Output to the Console

The most important tool for learning and debugging:

```javascript
// Printing text
console.log('Hello, World!');

// Printing numbers
console.log(42);
console.log(3.14);

// Printing multiple values
console.log('Name:', 'Alice', 'Age:', 25);

// Printing expressions
console.log(2 + 3); // 5
console.log('Score: ' + 95); // "Score: 95"
```

### `alert()` — Pop-Up Message

Displays a message in a dialog box:

```javascript
alert('Welcome to our website!');
alert('Your order has been placed.');
```

> ⚠️ `alert()` **blocks** the page — the user must click OK before anything else happens. Use sparingly in real projects.

### `prompt()` — Ask for Input

Displays a dialog box asking the user for text input:

```javascript
// Basic prompt
const name = prompt('What is your name?');
console.log(name); // whatever the user typed

// Prompt with default value
const color = prompt('What is your favorite color?', 'blue');
console.log(color);
```

**Important:** `prompt()` **always returns a string** (or `null` if the user clicks Cancel).

```javascript
const age = prompt('How old are you?');
console.log(typeof age); // "string" — even if they type a number!
```

### `confirm()` — Yes/No Question

Displays a dialog box with OK and Cancel buttons. Returns `true` or `false`:

```javascript
const isSure = confirm('Are you sure you want to delete this?');

if (isSure) {
	console.log('Item deleted.');
} else {
	console.log('Deletion cancelled.');
}
```

### Combining Them Together

```javascript
// Interactive greeting program
const userName = prompt('What is your name?');
const userAge = prompt('How old are you?');

alert('Hello, ' + userName + '! You are ' + userAge + ' years old.');
console.log('User:', userName, 'Age:', userAge);
```

<details>
<summary>💡 Knowledge Check #4</summary>

**Question:** What data type does `prompt()` always return, and why is this important?

**Answer:** `prompt()` always returns a **string** (or `null` if cancelled). This is important because if you ask for a number and try to do math with it, you might get unexpected results:

```javascript
const age = prompt('Your age?'); // "25" (a string!)
console.log(age + 5); // "255" (string concatenation, NOT 30!)
console.log(Number(age) + 5); // 30 (correct — convert first!)
```

</details>

### Quick Practice: Build an "About Me" Generator

Add this to your `script.js`:

```javascript
// About Me Generator
const name = prompt('What is your name?');
const age = prompt('How old are you?');
const hobby = prompt('What is your favorite hobby?');
const city = prompt('What city do you live in?');

const aboutMe =
	'My name is ' +
	name +
	'. I am ' +
	age +
	' years old. I love ' +
	hobby +
	' and I live in ' +
	city +
	'.';

alert(aboutMe);
console.log(aboutMe);

// Also update the page!
document.getElementById('output').textContent = aboutMe;
```

---

## Part 5: Lab — Interactive Greeting Page (15 minutes)

### Challenge: Build a Personalized Greeting Page

Create a new file called `greeting.html` with an external `greeting.js` file.

**Requirements:**

1. Ask the user for their name using `prompt()`
2. Ask what time of day it is (morning, afternoon, evening)
3. Display an appropriate greeting:
    - Morning → "Good morning, [name]! ☀️"
    - Afternoon → "Good afternoon, [name]! 🌤️"
    - Evening → "Good evening, [name]! 🌙"
4. Display the greeting both as an `alert()` and on the page

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
		<title>Greeting Page</title>
		<link
			rel="stylesheet"
			href="style.css"
		/>
		<script
			src="greeting.js"
			defer
		></script>
	</head>
	<body>
		<div class="container">
			<h1 id="greeting-heading">Welcome!</h1>
			<p id="greeting-message">Loading your greeting...</p>
		</div>
	</body>
</html>
```

**Starter JavaScript (fill in the blanks):**

```javascript
// greeting.js

// Step 1: Get user input
const name = prompt('What is your name?');
const timeOfDay = prompt('Is it morning, afternoon, or evening?');

// Step 2: Create the greeting
let greeting;
let emoji;

// TODO: Use if/else to set greeting and emoji based on timeOfDay
// Hint: if (timeOfDay === "morning") { ... }

// Step 3: Display the greeting
const message = greeting + ', ' + name + '! ' + emoji;

alert(message);
document.getElementById('greeting-heading').textContent =
	greeting + '! ' + emoji;
document.getElementById('greeting-message').textContent =
	'Welcome, ' + name + '!';
```

<details>
<summary>✅ Solution</summary>

```javascript
const name = prompt('What is your name?');
const timeOfDay = prompt('Is it morning, afternoon, or evening?');

let greeting;
let emoji;

if (timeOfDay === 'morning') {
	greeting = 'Good morning';
	emoji = '☀️';
} else if (timeOfDay === 'afternoon') {
	greeting = 'Good afternoon';
	emoji = '🌤️';
} else if (timeOfDay === 'evening') {
	greeting = 'Good evening';
	emoji = '🌙';
} else {
	greeting = 'Hello';
	emoji = '👋';
}

const message = greeting + ', ' + name + '! ' + emoji;

alert(message);
document.getElementById('greeting-heading').textContent =
	greeting + '! ' + emoji;
document.getElementById('greeting-message').textContent =
	'Welcome, ' + name + '!';

console.log('Greeting created for:', name);
console.log('Time of day:', timeOfDay);
console.log('Message:', message);
```

</details>

---

## ⚠️ Common Mistakes

| Mistake                                | Problem                                | Fix                                        |
| -------------------------------------- | -------------------------------------- | ------------------------------------------ |
| Forgetting `defer` on external scripts | Script runs before HTML is ready       | Add `defer` to your `<script>` tag         |
| Misspelling `console.log`              | `consolee.log` → ReferenceError        | Double-check spelling, use autocomplete    |
| Missing quotes around strings          | `console.log(hello)` → ReferenceError  | Use `console.log("hello")` with quotes     |
| Forgetting semicolons                  | Usually works, but can cause rare bugs | Always end statements with `;`             |
| Not saving the file before testing     | Old code runs instead                  | Save (`Ctrl+S`) before refreshing          |
| Using `document.write()`               | Overwrites entire page                 | Use `console.log()` or DOM methods instead |

---

## 📝 Session Summary

In this session, you learned:

1. **What JavaScript is** — The programming language of the web, adding interactivity and behavior
2. **Where it runs** — In browsers (client-side) and on servers (Node.js)
3. **Three ways to add JS** — Inline (avoid), internal (`<script>`), external (`<script src="">` preferred)
4. **Script loading** — Use `defer` for guaranteed execution order after HTML parsing
5. **Developer Tools** — Console for testing, `console.log/warn/error/table` for output
6. **Input/Output** — `prompt()` for input, `alert()` for pop-ups, `console.log()` for debugging

---

## 🏠 Homework

### Task 1: Favorite Things Page

Create an HTML page with external JS that asks the user for:

- Favorite movie
- Favorite food
- Favorite music artist

Display all answers on the page using `document.getElementById().textContent`.

### Task 2: Simple Math Quiz

Use `prompt()` to ask 3 math questions. Use `alert()` to tell the user if each answer is correct or wrong. At the end, show their score (e.g., "You got 2 out of 3 correct!").

### Task 3: Console Exploration

Open the browser console and experiment with at least 10 different expressions. Take a screenshot of your experiments and save it for class.

### Bonus Challenge: Number Guessing Game

1. Generate a random number between 1 and 10: `Math.floor(Math.random() * 10) + 1`
2. Use `prompt()` to ask the user to guess
3. Use `alert()` to tell them if they were right, too high, or too low
4. Allow 3 guesses

---

## 📚 Resources

- [MDN: What is JavaScript?](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/What_is_JavaScript)
- [MDN: Developer Tools](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Tools_and_setup/What_are_browser_developer_tools)
- [JavaScript.info: Hello, world!](https://javascript.info/hello-world)
- [JavaScript.info: Developer Console](https://javascript.info/devtools)
- [W3Schools: JavaScript Output](https://www.w3schools.com/js/js_output.asp)

---

**Next:** [Session 20 — Variables, Constants & Data Types](session-20.md) →
