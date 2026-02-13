# Week 07 — Session 21: Operators, Expressions & Control Flow

**Navigation:**
← [Session 20](session-20.md) | [Week 07 Index](../week-07.md) | [Session 22](../week-08/session-22.md) →

---

**Session Length:** 90 minutes

## 📋 Pre-Class Checklist

Before starting this session, make sure you have:

- ✅ Completed Sessions 19–20 (JS setup, variables, data types)
- ✅ Understand `let`, `const`, and primitive data types
- ✅ Comfortable using `console.log()` and `prompt()`
- ✅ Create a new file: `control-flow.js`

## 🎯 Learning Objectives

By the end of this session, you will be able to:

- Use arithmetic, comparison, logical, and assignment operators
- Write expressions using template literals for string interpolation
- Identify truthy and falsy values in JavaScript
- Write conditional logic using `if`, `else if`, `else`
- Use `switch` statements for multi-case branching
- Apply the ternary operator for concise conditionals
- Combine operators and conditionals to build decision-making programs

## 📦 Files for This Session

- `session-21.md` — This tutorial (you're reading it!)
- Create: `control-flow.js`, `calculator.js`, `grade-calculator.js`

## 🔑 Key Terms

**operator**, **operand**, **expression**, **arithmetic operator**, **comparison operator**, **logical operator**, **assignment operator**, **template literal**, **interpolation**, **truthy**, **falsy**, **conditional**, **if/else**, **switch**, **ternary operator**, **short-circuit evaluation**, **nullish coalescing**

## 🏗️ What You Will Build

- A grade calculator with letter grades and feedback
- A simple calculator (add, subtract, multiply, divide)
- A "Magic 8-Ball" random response generator

---

## Part 1: Arithmetic Operators (10 minutes)

### Basic Math Operators

```javascript
const a = 10;
const b = 3;

console.log(a + b); // 13   Addition
console.log(a - b); // 7    Subtraction
console.log(a * b); // 30   Multiplication
console.log(a / b); // 3.33 Division
console.log(a % b); // 1    Modulo (remainder)
console.log(a ** b); // 1000 Exponentiation (10³)
```

### Modulo (`%`) — The Remainder Operator

This is incredibly useful for many programming patterns:

```javascript
// Check if a number is even or odd
console.log(10 % 2); // 0 → even
console.log(7 % 2); // 1 → odd

// Wrap around (cycle through values)
console.log(0 % 3); // 0
console.log(1 % 3); // 1
console.log(2 % 3); // 2
console.log(3 % 3); // 0 ← wraps back!
console.log(4 % 3); // 1

// Check divisibility
const year = 2024;
const isLeapYear = (year % 4 === 0 && year % 100 !== 0) || year % 400 === 0;
console.log(isLeapYear); // true
```

### Increment & Decrement

```javascript
let count = 0;

count++; // count is now 1 (post-increment)
count++; // count is now 2
count--; // count is now 1 (post-decrement)

// Pre vs Post (subtle difference)
let x = 5;
console.log(x++); // 5 (returns THEN increments)
console.log(x); // 6
console.log(++x); // 7 (increments THEN returns)
```

### Operator Precedence

JavaScript follows standard math order (PEMDAS/BODMAS):

```javascript
console.log(2 + 3 * 4); // 14 (not 20! multiplication first)
console.log((2 + 3) * 4); // 20 (parentheses override)
console.log(10 - 2 ** 2); // 6  (exponent first: 10 - 4)
```

> 💡 When in doubt, use **parentheses** to make your intent clear!

<details>
<summary>💡 Knowledge Check #1</summary>

**Question:** What does `17 % 5` return, and why is the modulo operator useful?

**Answer:**

- `17 % 5` returns `2` (17 ÷ 5 = 3 remainder 2)
- Modulo is useful for:
    - Checking even/odd (`n % 2`)
    - Cycling through values (carousel/slider indexes)
    - Checking divisibility (`n % 3 === 0`)
    - Clock arithmetic (hours, minutes)

</details>

---

## Part 2: Comparison Operators (10 minutes)

Comparison operators compare two values and return a **boolean** (`true` or `false`):

```javascript
const age = 25;

// Equality
console.log(age === 25); // true  (strict equal — same type AND value)
console.log(age === '25'); // false (different types!)
console.log(age !== 30); // true  (strict not equal)

// Greater/Less than
console.log(age > 18); // true
console.log(age < 18); // false
console.log(age >= 25); // true  (greater than OR equal)
console.log(age <= 24); // false

// String comparison (alphabetical/Unicode order)
console.log('apple' < 'banana'); // true (a comes before b)
console.log('a' < 'A'); // false (lowercase > uppercase in Unicode)
console.log('10' < '9'); // true! (string comparison: "1" < "9")
```

### Strict vs Loose Comparison (Reminder)

```javascript
// ALWAYS use strict (===)
console.log(5 === 5); // true ✅
console.log(5 === '5'); // false ✅ (different types)

// NEVER use loose (==)
console.log(5 == '5'); // true ❌ (coercion hides bugs)
console.log(0 == false); // true ❌
console.log('' == false); // true ❌
console.log(null == undefined); // true ❌
```

---

## Part 3: Logical Operators (10 minutes)

Logical operators combine boolean expressions:

### AND (`&&`) — Both must be true

```javascript
const age = 25;
const hasTicket = true;

// Both conditions must be true
console.log(age >= 18 && hasTicket); // true (both true)
console.log(age >= 18 && !hasTicket); // false (second is false)

// Practical example: login validation
const username = 'admin';
const password = 'secret123';
const isValid = username === 'admin' && password === 'secret123';
console.log('Login valid:', isValid); // true
```

### OR (`||`) — At least one must be true

```javascript
const isWeekend = true;
const isHoliday = false;

// At least one must be true
console.log(isWeekend || isHoliday); // true

// Practical example: can access premium content
const isPremiumUser = false;
const hasFreeTrial = true;
const canAccess = isPremiumUser || hasFreeTrial;
console.log('Can access:', canAccess); // true
```

### NOT (`!`) — Flips the boolean

```javascript
console.log(!true); // false
console.log(!false); // true
console.log(!0); // true  (0 is falsy → !falsy = true)
console.log(!''); // true  ("" is falsy)
console.log(!'hello'); // false ("hello" is truthy)
```

### Short-Circuit Evaluation

JavaScript stops evaluating as soon as the result is determined:

```javascript
// && — stops at first falsy value
console.log(false && 'hello'); // false (stopped at false)
console.log(true && 'hello'); // "hello" (passed, returns last value)

// || — stops at first truthy value
console.log('Alice' || 'default'); // "Alice" (already truthy, stop)
console.log('' || 'default'); // "default" (empty string is falsy)
console.log(null || 'fallback'); // "fallback"

// Practical: default values
const input = prompt('Enter name:'); // might be empty
const name = input || 'Guest'; // use "Guest" if input is empty
console.log('Hello,', name);
```

### Nullish Coalescing (`??`)

Similar to `||` but only treats `null` and `undefined` as "empty":

```javascript
// || treats ALL falsy values as "empty"
console.log(0 || 'default'); // "default" (0 is falsy)
console.log('' || 'default'); // "default" ("" is falsy)

// ?? only treats null/undefined as "empty"
console.log(0 ?? 'default'); // 0 (0 is not null/undefined!)
console.log('' ?? 'default'); // "" (empty string is not null/undefined!)
console.log(null ?? 'default'); // "default" ✅
console.log(undefined ?? 'default'); // "default" ✅
```

<details>
<summary>💡 Knowledge Check #2</summary>

**Question:** What is the difference between `||` and `??`?

**Answer:**

- `||` — Returns the right side if the left side is **any falsy value** (`false`, `0`, `""`, `null`, `undefined`, `NaN`)
- `??` — Returns the right side **only** if the left side is `null` or `undefined`

Use `??` when `0` or `""` are valid values you want to keep:

```javascript
const volume = 0;
console.log(volume || 50); // 50 (wrong! 0 is a valid volume)
console.log(volume ?? 50); // 0 (correct! 0 is not null/undefined)
```

</details>

---

## Part 4: Assignment Operators (5 minutes)

Shorthand for updating variables:

```javascript
let score = 100;

score += 10; // score = score + 10   → 110
score -= 5; // score = score - 5    → 105
score *= 2; // score = score * 2    → 210
score /= 3; // score = score / 3    → 70
score %= 4; // score = score % 4    → 2
score **= 3; // score = score ** 3   → 8

// String concatenation with +=
let message = 'Hello';
message += ' World'; // "Hello World"
message += '!'; // "Hello World!"
```

---

## Part 5: Template Literals (10 minutes)

### String Concatenation (Old Way)

```javascript
const name = 'Alice';
const age = 25;

// Messy with + concatenation
const message =
	'Hello, my name is ' + name + ' and I am ' + age + ' years old.';
console.log(message);
```

### Template Literals (Modern Way ✅)

Use backticks `` ` `` and `${expression}`:

```javascript
const name = 'Alice';
const age = 25;

// Clean and readable
const message = `Hello, my name is ${name} and I am ${age} years old.`;
console.log(message);

// Expressions inside ${}
console.log(`In 5 years, I'll be ${age + 5}.`);
console.log(`Is adult: ${age >= 18}`);
console.log(`Name uppercase: ${name.toUpperCase()}`);

// Multi-line strings (no \n needed!)
const card = `
╔══════════════════╗
║  Name: ${name.padEnd(10)}║
║  Age:  ${String(age).padEnd(10)}║
╚══════════════════╝`;
console.log(card);

// Building HTML strings
const productHTML = `
  <div class="product">
    <h3>${name}'s Widget</h3>
    <p>Price: $${(29.99).toFixed(2)}</p>
    <p>In stock: ${true ? 'Yes' : 'No'}</p>
  </div>
`;
console.log(productHTML);
```

<details>
<summary>💡 Knowledge Check #3</summary>

**Question:** Rewrite this string concatenation using a template literal:

```javascript
const item = 'Book';
const price = 15.99;
const qty = 3;
const output =
	'You ordered ' + qty + ' x ' + item + ' for $' + (price * qty).toFixed(2);
```

**Answer:**

```javascript
const output = `You ordered ${qty} x ${item} for $${(price * qty).toFixed(2)}`;
```

</details>

---

## Part 6: Truthy & Falsy Values (10 minutes)

In JavaScript, every value can be treated as either `true` or `false` in a boolean context (like an `if` statement).

### Falsy Values (Only 6!)

These are the ONLY values that are considered `false`:

```javascript
if (false) {
} // false
if (0) {
} // 0
if ('') {
} // empty string
if (null) {
} // null
if (undefined) {
} // undefined
if (NaN) {
} // NaN

// Everything else is TRUTHY
```

### Truthy Values (Everything Else)

```javascript
if (true) {
	console.log('truthy');
} // ✅
if (42) {
	console.log('truthy');
} // ✅ any non-zero number
if ('hello') {
	console.log('truthy');
} // ✅ any non-empty string
if ('false') {
	console.log('truthy');
} // ✅ the STRING "false" is truthy!
if ('0') {
	console.log('truthy');
} // ✅ the STRING "0" is truthy!
if ([]) {
	console.log('truthy');
} // ✅ empty array is truthy!
if ({}) {
	console.log('truthy');
} // ✅ empty object is truthy!
if (-1) {
	console.log('truthy');
} // ✅ negative numbers are truthy
```

### Practical Use: Checking for Input

```javascript
const userInput = prompt('Enter your name:');

if (userInput) {
	// Runs if userInput is NOT empty, null, or undefined
	console.log(`Welcome, ${userInput}!`);
} else {
	// Runs if userInput is empty string or null (clicked Cancel)
	console.log('No name entered.');
}
```

---

## Part 7: Conditional Statements (15 minutes)

### `if` / `else if` / `else`

The most common way to make decisions:

```javascript
const temperature = 32;

if (temperature >= 35) {
	console.log("🔥 It's very hot! Stay hydrated.");
} else if (temperature >= 25) {
	console.log('☀️ Nice and warm.');
} else if (temperature >= 15) {
	console.log('🌤️ A bit cool. Wear a jacket.');
} else if (temperature >= 0) {
	console.log("🥶 It's cold! Bundle up.");
} else {
	console.log('❄️ Freezing! Stay inside.');
}
```

### Nested Conditionals

```javascript
const age = 20;
const hasLicense = true;

if (age >= 18) {
	if (hasLicense) {
		console.log('You can drive! 🚗');
	} else {
		console.log("You're old enough but need a license first.");
	}
} else {
	console.log('You must be at least 18 to drive.');
}

// Better: combine with && (flatter, more readable)
if (age >= 18 && hasLicense) {
	console.log('You can drive! 🚗');
} else if (age >= 18 && !hasLicense) {
	console.log('Get a license first.');
} else {
	console.log('Too young to drive.');
}
```

### `switch` Statement

Best for comparing a single value against many options:

```javascript
const fruit = prompt('Enter a fruit:').toLowerCase();

switch (fruit) {
	case 'apple':
		console.log('🍎 Apples are $1.50/lb');
		break;
	case 'banana':
		console.log('🍌 Bananas are $0.75/lb');
		break;
	case 'orange':
		console.log('🍊 Oranges are $2.00/lb');
		break;
	case 'grape':
	case 'grapes':
		console.log('🍇 Grapes are $3.00/lb');
		break; // handles both "grape" and "grapes"
	default:
		console.log(`Sorry, we don't carry ${fruit}.`);
}
```

> ⚠️ Don't forget `break`! Without it, execution "falls through" to the next case.

### Ternary Operator

A concise shorthand for simple `if/else`:

```javascript
// Syntax: condition ? valueIfTrue : valueIfFalse

const age = 20;
const status = age >= 18 ? 'adult' : 'minor';
console.log(status); // "adult"

// Practical examples
const score = 85;
const grade =
	score >= 90 ? 'A'
	: score >= 80 ? 'B'
	: score >= 70 ? 'C'
	: 'F';

const greeting = `Good ${new Date().getHours() < 12 ? 'morning' : 'afternoon'}!`;

// Use in template literals
const items = 5;
console.log(`You have ${items} item${items !== 1 ? 's' : ''} in your cart.`);
```

> 💡 Use ternary for simple cases. If you're nesting ternaries, use `if/else` instead for readability.

<details>
<summary>💡 Knowledge Check #4</summary>

**Question:** Rewrite this `if/else` using a ternary operator:

```javascript
let access;
if (age >= 18 && hasTicket) {
	access = 'granted';
} else {
	access = 'denied';
}
```

**Answer:**

```javascript
const access = age >= 18 && hasTicket ? 'granted' : 'denied';
```

</details>

---

## Part 8: Lab — Grade Calculator (20 minutes)

### Challenge: Build a Grade Calculator

Create `grade-calculator.js` that:

1. Asks the user for their score (0–100) using `prompt()`
2. Converts the input to a number
3. Validates the input (must be a number between 0 and 100)
4. Calculates a letter grade:
    - 90–100: A (Excellent!)
    - 80–89: B (Good job!)
    - 70–79: C (Satisfactory)
    - 60–69: D (Needs improvement)
    - 0–59: F (Please see instructor)
5. Displays the result using `alert()` and `console.log()`
6. Updates the page with the result

**Starter Code:**

```javascript
// Grade Calculator

// Step 1: Get input
const input = prompt('Enter your score (0-100):');
const score = Number(input);

// Step 2: Validate
if (isNaN(score) || score < 0 || score > 100) {
	alert('Invalid score! Please enter a number between 0 and 100.');
	// TODO: Handle invalid input
}

// Step 3: Calculate grade
let grade;
let feedback;
let emoji;

// TODO: Use if/else if/else to determine grade, feedback, and emoji

// Step 4: Display result
const result = `Score: ${score} | Grade: ${grade} ${emoji}\n${feedback}`;
alert(result);
console.log(result);

// Step 5: Update the page
document.getElementById('output').innerHTML = `
  <div class="result">
    <h2>${emoji} Grade: ${grade}</h2>
    <p>Score: ${score}/100</p>
    <p>${feedback}</p>
  </div>
`;
```

<details>
<summary>✅ Solution</summary>

```javascript
const input = prompt('Enter your score (0-100):');
const score = Number(input);

if (isNaN(score) || score < 0 || score > 100) {
	alert('Invalid score! Please enter a number between 0 and 100.');
} else {
	let grade;
	let feedback;
	let emoji;

	if (score >= 90) {
		grade = 'A';
		feedback = "Excellent work! You've mastered the material.";
		emoji = '🌟';
	} else if (score >= 80) {
		grade = 'B';
		feedback = 'Good job! You have a solid understanding.';
		emoji = '👍';
	} else if (score >= 70) {
		grade = 'C';
		feedback = 'Satisfactory. Review the challenging topics.';
		emoji = '📖';
	} else if (score >= 60) {
		grade = 'D';
		feedback = 'Needs improvement. Please seek extra help.';
		emoji = '⚠️';
	} else {
		grade = 'F';
		feedback = 'Please see the instructor for additional support.';
		emoji = '❗';
	}

	const result = `Score: ${score} | Grade: ${grade} ${emoji}\n${feedback}`;
	alert(result);
	console.log(result);

	document.getElementById('output').innerHTML = `
    <div class="result">
      <h2>${emoji} Grade: ${grade}</h2>
      <p>Score: ${score}/100</p>
      <p>${feedback}</p>
    </div>
  `;
}
```

</details>

---

## ⚠️ Common Mistakes

| Mistake                         | Problem                          | Fix                                  |
| ------------------------------- | -------------------------------- | ------------------------------------ | --- | --- | -------------------------- | --------------------------------- |
| `=` instead of `===`            | Assignment instead of comparison | `if (x === 5)` not `if (x = 5)`      |
| Missing `break` in switch       | Fall-through to next case        | Add `break` after each case block    |
| Chaining ternaries              | Hard to read and debug           | Use `if/else` for complex conditions |
| Not converting `prompt()` input | String math: `"5" + 3 = "53"`    | Convert with `Number()` first        |
| Using `                         |                                  | `when you mean`??`                   | `0  |     | "default"`gives`"default"` | Use `??` to preserve `0` and `""` |

---

## 📝 Session Summary

In this session, you learned:

1. **Arithmetic operators** — `+`, `-`, `*`, `/`, `%`, `**`, `++`, `--`
2. **Comparison operators** — `===`, `!==`, `>`, `<`, `>=`, `<=`
3. **Logical operators** — `&&`, `||`, `!`, `??`
4. **Assignment operators** — `=`, `+=`, `-=`, `*=`, `/=`
5. **Template literals** — Backtick strings with `${expression}` interpolation
6. **Truthy/Falsy** — 6 falsy values, everything else is truthy
7. **Conditionals** — `if/else if/else`, `switch`, ternary `? :`
8. **Short-circuit evaluation** — `||` for defaults, `&&` for guards

---

## 🏠 Homework

### Task 1: Simple Calculator

Build a calculator that:

1. Asks for the first number
2. Asks for the operator (+, -, \*, /)
3. Asks for the second number
4. Displays the result
5. Handles division by zero

### Task 2: Day of the Week

Use `switch` to display a message based on `new Date().getDay()` (0 = Sunday, 6 = Saturday). Include whether it's a weekday or weekend.

### Task 3: Magic 8-Ball

1. Generate a random number: `Math.floor(Math.random() * 8)`
2. Map each number to a response (e.g., "Yes", "No", "Ask again later", etc.)
3. Ask the user a yes/no question with `prompt()`
4. Display the Magic 8-Ball response with `alert()`

### Bonus Challenge: Ticket Price Calculator

Calculate ticket prices based on:

- Age: under 5 = free, 5-12 = $5, 13-64 = $12, 65+ = $8
- Day: weekends are $3 extra
- 3D movie: add $4
  Display a detailed receipt with all line items using template literals.

---

## 📚 Resources

- [MDN: Expressions and Operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_operators)
- [MDN: Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)
- [MDN: if...else](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else)
- [MDN: switch](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch)
- [JavaScript.info: Comparisons](https://javascript.info/comparison)
- [JavaScript.info: Logical Operators](https://javascript.info/logical-operators)
- [JavaScript.info: Conditional Branching](https://javascript.info/ifelse)

---

**Next:** [Session 22 — Functions & Scope](../week-08/session-22.md) →
