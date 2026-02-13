# Week 07 — JavaScript Fundamentals I: Syntax, Variables & Data Types

> _"Your first lines of JavaScript — understanding the language from the ground up."_

This week marks the beginning of your JavaScript journey. You will learn what JavaScript is, how to run it in the browser, and master the building blocks of the language: variables, data types, operators, and control flow.

---

## Overview

-   **Focus:** Introduction to JavaScript, variables, data types, operators, and control flow
-   **Prerequisites:** Weeks 01–06 (HTML & CSS fundamentals complete)
-   **Outcomes by end of week:**
    -   Understand JavaScript's role in modern web development
    -   Add JavaScript to HTML pages using inline, internal, and external methods
    -   Use browser developer tools (Console, Sources, Debugger)
    -   Declare variables with `let`, `const`, and understand legacy `var`
    -   Work with all primitive data types and understand type coercion
    -   Write conditional logic and use operators effectively
    -   Build simple interactive programs using `prompt()`, `alert()`, and `console.log()`

---

## Sessions

### Session 19 — Introduction to JavaScript & Developer Tools (90 min)

**Learning Objectives:**
-   Explain what JavaScript is and its role in the web (HTML = structure, CSS = style, JS = behavior)
-   Understand where JavaScript runs (browser engine, Node.js)
-   Add JavaScript to HTML pages (inline, `<script>` tag, external `.js` file)
-   Use browser developer tools (Console tab, Sources tab)
-   Write first JavaScript statements using `console.log()`, `alert()`, and `prompt()`

**Topics Covered:**

| Topic | Duration | Details |
|-------|----------|---------|
| What is JavaScript? | 15 min | History (Brendan Eich, 1995), ECMAScript standard, client-side vs server-side, JS ecosystem overview |
| Adding JS to HTML | 15 min | Inline `onclick`, internal `<script>`, external `<script src="">`, `defer` vs `async` attributes, script placement (head vs body) |
| Browser Developer Tools | 20 min | Opening DevTools (F12 / Ctrl+Shift+I), Console tab (REPL), Sources tab, clearing console, multi-line input |
| First JavaScript Programs | 25 min | `console.log("Hello, World!")`, `alert("Welcome!")`, `prompt("What is your name?")`, `confirm()`, string concatenation basics |
| Lab: Interactive Greeting | 15 min | Build a page that asks the user's name with `prompt()` and displays a personalized greeting with `alert()` |

**Key Code Examples:**

```html
<!-- Three ways to add JavaScript -->

<!-- 1. Inline (avoid in production) -->
<button onclick="alert('Clicked!')">Click Me</button>

<!-- 2. Internal script -->
<script>
  console.log("Page loaded!");
</script>

<!-- 3. External script (recommended) -->
<script src="script.js" defer></script>
```

```javascript
// script.js — First interactive program
const userName = prompt("What is your name?");
console.log("Hello, " + userName + "!");
alert("Welcome to JavaScript, " + userName + "!");
```

**Homework:**
-   Create an HTML page with an external JS file
-   Use `prompt()` to ask for the user's favorite color
-   Display the response using both `console.log()` and `alert()`
-   Experiment with the browser console: try typing expressions like `2 + 2`, `"hello".toUpperCase()`, `Math.random()`

---

### Session 20 — Variables, Constants & Data Types (90 min)

**Learning Objectives:**
-   Declare variables using `let` and constants using `const`
-   Understand why `var` exists and why we prefer `let`/`const`
-   Identify and use all 7 primitive data types
-   Use `typeof` to check data types at runtime
-   Understand type coercion and conversion

**Topics Covered:**

| Topic | Duration | Details |
|-------|----------|---------|
| Variables with `let` | 15 min | Declaration, assignment, reassignment, naming rules (camelCase, no reserved words, start with letter/$/_), meaningful names |
| Constants with `const` | 10 min | Immutable bindings, when to use `const` (default choice), `const` with objects/arrays (reference vs value) |
| Legacy `var` and Hoisting | 10 min | `var` function scope vs `let`/`const` block scope, hoisting behavior, why `var` causes bugs, temporal dead zone |
| Primitive Data Types | 20 min | `string` (single/double/backtick quotes), `number` (integers, floats, `Infinity`, `NaN`), `boolean` (`true`/`false`), `null`, `undefined`, `symbol`, `BigInt` |
| Type Checking with `typeof` | 10 min | `typeof` operator, common results, quirks (`typeof null === "object"`), practical uses |
| Type Coercion & Conversion | 15 min | Implicit coercion (`"5" + 3` vs `"5" - 3`), explicit conversion (`Number()`, `String()`, `Boolean()`, `parseInt()`, `parseFloat()`), strict equality `===` vs loose `==` |
| Lab: Variable Explorer | 10 min | Create variables of every type, log them with `typeof`, test coercion edge cases |

**Key Code Examples:**

```javascript
// Variables and constants
let age = 25;                    // can be reassigned
const PI = 3.14159;              // cannot be reassigned
const name = "Alice";            // strings are immutable anyway

// All 7 primitive types
let str = "Hello";               // string
let num = 42;                    // number
let float = 3.14;               // number (no separate float type)
let bool = true;                 // boolean
let nothing = null;              // null (intentional absence)
let notDefined;                  // undefined (not yet assigned)
let id = Symbol("unique");      // symbol
let bigNum = 9007199254740991n; // BigInt

// typeof checks
console.log(typeof str);        // "string"
console.log(typeof num);        // "number"
console.log(typeof bool);       // "boolean"
console.log(typeof nothing);    // "object" (famous JS quirk!)
console.log(typeof notDefined); // "undefined"

// Type coercion gotchas
console.log("5" + 3);           // "53" (string concatenation)
console.log("5" - 3);           // 2   (numeric subtraction)
console.log("5" === 5);         // false (strict equality)
console.log("5" == 5);          // true  (loose equality — avoid!)

// Explicit conversion
let input = prompt("Enter a number:");  // always returns a string
let parsed = Number(input);              // convert to number
console.log(parsed + 10);               // now math works correctly
```

**Homework:**
-   Declare variables for a person's profile: name, age, email, isStudent, gpa
-   Use `typeof` on each and log the results
-   Experiment: What happens with `Number("hello")`? `Boolean(0)`? `Boolean("")`? `Boolean("false")`?
-   Write a program that converts temperature from Fahrenheit to Celsius using `prompt()` and `Number()`

---

### Session 21 — Operators, Expressions & Control Flow (90 min)

**Learning Objectives:**
-   Use arithmetic, comparison, logical, and assignment operators
-   Understand truthy and falsy values in JavaScript
-   Write conditional logic with `if`, `else if`, `else`, `switch`, and ternary operator
-   Use template literals for string interpolation
-   Combine operators and control flow to build decision-making programs

**Topics Covered:**

| Topic | Duration | Details |
|-------|----------|---------|
| Arithmetic Operators | 10 min | `+`, `-`, `*`, `/`, `%` (modulo), `**` (exponent), `++`, `--`, operator precedence |
| Comparison Operators | 10 min | `===`, `!==`, `>`, `<`, `>=`, `<=`, strict vs loose comparison, comparing different types |
| Logical Operators | 10 min | `&&` (AND), `\|\|` (OR), `!` (NOT), short-circuit evaluation, nullish coalescing `??` |
| Assignment Operators | 5 min | `=`, `+=`, `-=`, `*=`, `/=`, `%=` |
| Template Literals | 10 min | Backtick syntax, `${expression}` interpolation, multi-line strings, tagged templates (intro) |
| Truthy & Falsy Values | 10 min | Falsy values: `false`, `0`, `""`, `null`, `undefined`, `NaN`; everything else is truthy |
| Conditional Statements | 15 min | `if`, `else if`, `else`, nesting, `switch/case/default/break`, ternary `condition ? a : b` |
| Lab: Grade Calculator | 20 min | Build a program that takes a score via `prompt()`, converts it, and outputs a letter grade with feedback |

**Key Code Examples:**

```javascript
// Template literals
const name = "Alice";
const age = 25;
console.log(`Hello, ${name}! You are ${age} years old.`);
console.log(`In 5 years, you'll be ${age + 5}.`);

// Multi-line strings
const html = `
  <div class="card">
    <h2>${name}</h2>
    <p>Age: ${age}</p>
  </div>
`;

// Conditional statements
const score = Number(prompt("Enter your score (0-100):"));

if (score >= 90) {
  console.log("Grade: A — Excellent!");
} else if (score >= 80) {
  console.log("Grade: B — Good job!");
} else if (score >= 70) {
  console.log("Grade: C — Satisfactory");
} else if (score >= 60) {
  console.log("Grade: D — Needs improvement");
} else {
  console.log("Grade: F — Please see instructor");
}

// Ternary operator
const status = age >= 18 ? "adult" : "minor";
console.log(`${name} is an ${status}.`);

// Switch statement
const day = new Date().getDay();
switch (day) {
  case 0: console.log("Sunday");    break;
  case 1: console.log("Monday");    break;
  case 2: console.log("Tuesday");   break;
  case 3: console.log("Wednesday"); break;
  case 4: console.log("Thursday");  break;
  case 5: console.log("Friday");    break;
  case 6: console.log("Saturday");  break;
  default: console.log("Invalid day");
}

// Logical operators and short-circuit
const user = null;
const displayName = user ?? "Guest";  // "Guest" (nullish coalescing)
console.log(`Welcome, ${displayName}`);
```

**Homework:**
-   Build a **Temperature Converter** that asks "Convert to (C)elsius or (F)ahrenheit?" and performs the right conversion
-   Build a **Simple Calculator** that asks for two numbers and an operator (+, -, *, /), then displays the result
-   Challenge: Build a "Magic 8-Ball" that gives random responses using `Math.random()` and `Math.floor()`

---

## Week 07 Summary

By the end of this week, students can:

| Skill | Status |
|-------|--------|
| Add JavaScript to HTML pages | ✅ |
| Use browser developer tools | ✅ |
| Declare variables with `let` and `const` | ✅ |
| Work with all primitive data types | ✅ |
| Use `typeof` and understand type coercion | ✅ |
| Write expressions with all operator types | ✅ |
| Use template literals for string interpolation | ✅ |
| Write conditional logic (if/else, switch, ternary) | ✅ |
| Build simple interactive programs | ✅ |

## Resources

-   [MDN: JavaScript First Steps](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps)
-   [MDN: JavaScript Building Blocks](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks)
-   [JavaScript.info: The Fundamentals](https://javascript.info/first-steps)
-   [W3Schools: JavaScript Tutorial](https://www.w3schools.com/js/)
