# Week 08 — Session 22: Functions & Scope

**Navigation:**
← [Session 21](../week-07/session-21.md) | [Week 08 Index](../week-08.md) | [Session 23](session-23.md) →

---

**Session Length:** 90 minutes

## 📋 Pre-Class Checklist

Before starting this session, make sure you have:

- ✅ Completed Week 07 (Sessions 19–21)
- ✅ Comfortable with variables, data types, operators, and conditionals
- ✅ Understand template literals and `if/else`
- ✅ Create a new file: `functions.js`

## 🎯 Learning Objectives

By the end of this session, you will be able to:

- Declare and invoke functions using function declarations, expressions, and arrow functions
- Define parameters, default parameters, and use return values
- Understand global, function, and block scope
- Explain hoisting and how it affects function declarations vs expressions
- Use closures for data privacy and state management
- Apply the DRY (Don't Repeat Yourself) principle with reusable functions

## 📦 Files for This Session

- `session-22.md` — This tutorial (you're reading it!)
- Create: `functions.js`, `utility-functions.js`

## 🔑 Key Terms

**function**, **declaration**, **expression**, **arrow function**, **parameter**, **argument**, **default parameter**, **return value**, **scope**, **global scope**, **function scope**, **block scope**, **hoisting**, **closure**, **callback**, **DRY principle**, **pure function**, **side effect**

## 🏗️ What You Will Build

- A utility library with reusable helper functions
- A tip calculator with multiple functions
- A simple counter using closures

---

## Part 1: Function Declarations (15 minutes)

### Why Functions?

Functions let you write code once and use it many times:

```javascript
// ❌ Without functions — repetition everywhere
console.log('Hello, Alice! Welcome to JavaScript.');
console.log('Hello, Bob! Welcome to JavaScript.');
console.log('Hello, Charlie! Welcome to JavaScript.');

// ✅ With a function — write once, use many times
function greet(name) {
	console.log(`Hello, ${name}! Welcome to JavaScript.`);
}

greet('Alice');
greet('Bob');
greet('Charlie');
```

### Function Declaration Syntax

```javascript
// Defining a function
function functionName(param1, param2) {
	// function body — code to execute
	return result; // optional return value
}

// Calling (invoking) a function
functionName(arg1, arg2);
```

### Parameters vs Arguments

```javascript
//                  parameters (placeholders)
//                       ↓     ↓
function add(a, b) {
	return a + b;
}

//          arguments (actual values)
//               ↓  ↓
const sum = add(5, 3); // 8
```

### Return Values

```javascript
// Functions without return → return undefined
function sayHello(name) {
	console.log(`Hello, ${name}!`);
	// no return → returns undefined
}

const result1 = sayHello('Alice'); // logs "Hello, Alice!"
console.log(result1); // undefined

// Functions with return → return a value
function calculateArea(width, height) {
	return width * height;
}

const area = calculateArea(10, 5);
console.log(`Area: ${area}`); // Area: 50

// return stops execution
function checkAge(age) {
	if (age < 0) {
		return 'Invalid age'; // exits here if negative
	}
	return age >= 18 ? 'Adult' : 'Minor';
}
```

### Multiple Parameters & Default Values

```javascript
// Default parameters — use when argument is not provided
function greetUser(name = 'Guest', greeting = 'Hello') {
	return `${greeting}, ${name}!`;
}

console.log(greetUser('Alice', 'Hi')); // "Hi, Alice!"
console.log(greetUser('Bob')); // "Hello, Bob!"
console.log(greetUser()); // "Hello, Guest!"
```

<details>
<summary>💡 Knowledge Check #1</summary>

**Question:** What is the difference between a parameter and an argument?

**Answer:**

- **Parameter** — A variable listed in the function definition (a placeholder). Like a label on a parking spot.
- **Argument** — The actual value passed to the function when calling it. Like the car that parks in the spot.

```javascript
function greet(name) { ... }   // 'name' is a parameter
greet("Alice");                 // "Alice" is an argument
```

</details>

---

## Part 2: Function Expressions & Arrow Functions (15 minutes)

### Function Expression

A function stored in a variable:

```javascript
// Function Expression
const multiply = function (a, b) {
	return a * b;
};

console.log(multiply(4, 5)); // 20

// Named function expression (useful for debugging)
const divide = function divideNumbers(a, b) {
	if (b === 0) return 'Cannot divide by zero';
	return a / b;
};
```

### Arrow Functions (ES6+)

A shorter syntax for writing functions:

```javascript
// Regular function
function add(a, b) {
	return a + b;
}

// Arrow function
const addArrow = (a, b) => {
	return a + b;
};

// Arrow function — concise body (implicit return)
const addShort = (a, b) => a + b;

// One parameter — parentheses optional
const double = (n) => n * 2;

// No parameters — empty parentheses required
const getTimestamp = () => Date.now();

// Returning an object — wrap in parentheses
const createUser = (name, age) => ({ name, age });
```

### When to Use Each

```javascript
// Function declarations — general-purpose, hoisted
function calculateTax(amount, rate) {
	return amount * rate;
}

// Arrow functions — callbacks, short operations
const prices = [10, 20, 30];
const withTax = prices.map((price) => price * 1.1);
console.log(withTax); // [11, 22, 33]

// Arrow functions — event handlers (coming in Week 09)
// button.addEventListener("click", () => { ... });
```

### Comparison Table

| Feature        | Declaration          | Expression                   | Arrow                   |
| -------------- | -------------------- | ---------------------------- | ----------------------- |
| Syntax         | `function name() {}` | `const name = function() {}` | `const name = () => {}` |
| Hoisted?       | ✅ Yes               | ❌ No                        | ❌ No                   |
| `this` binding | Dynamic              | Dynamic                      | Lexical (inherits)      |
| Best for       | General purpose      | Callbacks                    | Short callbacks         |

<details>
<summary>💡 Knowledge Check #2</summary>

**Question:** Convert this function declaration to an arrow function with implicit return:

```javascript
function square(n) {
	return n * n;
}
```

**Answer:**

```javascript
const square = (n) => n * n;
```

</details>

---

## Part 3: Scope (15 minutes)

### What Is Scope?

Scope determines where variables are accessible in your code.

### Global Scope

Variables declared outside any function or block:

```javascript
const appName = 'My App'; // global — accessible everywhere

function showApp() {
	console.log(appName); // ✅ accessible inside functions
}

if (true) {
	console.log(appName); // ✅ accessible inside blocks
}

showApp();
```

### Function Scope

Variables declared inside a function are only accessible within that function:

```javascript
function calculateTotal(price, qty) {
	const total = price * qty; // function scope
	const tax = total * 0.1; // function scope
	return total + tax;
}

calculateTotal(10, 3);
// console.log(total); // ❌ ReferenceError: total is not defined
// console.log(tax);   // ❌ ReferenceError: tax is not defined
```

### Block Scope (`let` and `const`)

Variables declared with `let` or `const` inside `{}` are only accessible within that block:

```javascript
if (true) {
	const blockVar = "I'm inside a block";
	let anotherBlock = 'Me too';
	console.log(blockVar); // ✅ works inside the block
}

// console.log(blockVar);     // ❌ ReferenceError
// console.log(anotherBlock); // ❌ ReferenceError

// var ignores block scope! (another reason to avoid var)
if (true) {
	var leaky = 'I escape blocks!';
}
console.log(leaky); // "I escape blocks!" — this is a bug!
```

### Scope Chain

Inner scopes can access outer scopes, but not vice versa:

```javascript
const outerVar = 'outer';

function outer() {
	const middleVar = 'middle';

	function inner() {
		const innerVar = 'inner';
		console.log(innerVar); // ✅ own scope
		console.log(middleVar); // ✅ parent scope
		console.log(outerVar); // ✅ grandparent (global) scope
	}

	inner();
	// console.log(innerVar); // ❌ can't access child scope
}

outer();
```

### Variable Shadowing

An inner variable with the same name "shadows" (hides) the outer one:

```javascript
const color = 'blue';

function paint() {
	const color = 'red'; // shadows the global 'color'
	console.log(color); // "red"
}

paint();
console.log(color); // "blue" (global unchanged)
```

<details>
<summary>💡 Knowledge Check #3</summary>

**Question:** What will this code output and why?

```javascript
let x = 10;

function test() {
	let x = 20;
	if (true) {
		let x = 30;
		console.log('Block:', x);
	}
	console.log('Function:', x);
}

test();
console.log('Global:', x);
```

**Answer:**

```
Block: 30
Function: 20
Global: 10
```

Each `let x` creates a NEW variable in its own scope. They don't affect each other. This is variable shadowing — the innermost `x` shadows the outer ones within its block.

</details>

---

## Part 4: Hoisting (10 minutes)

### What Is Hoisting?

JavaScript "moves" declarations to the top of their scope before execution:

```javascript
// Function declarations ARE hoisted (fully available before definition)
sayHi(); // ✅ Works!
function sayHi() {
	console.log('Hi!');
}

// Function expressions are NOT hoisted
// greet(); // ❌ ReferenceError: Cannot access 'greet' before initialization
const greet = function () {
	console.log('Hello!');
};
greet(); // ✅ Works here (after definition)

// Arrow functions are NOT hoisted
// add(2, 3); // ❌ ReferenceError
const add = (a, b) => a + b;
add(2, 3); // ✅ Works here
```

### Variable Hoisting

```javascript
// var is hoisted but initialized to undefined
console.log(a); // undefined (not an error!)
var a = 5;

// let/const are hoisted but NOT initialized (TDZ)
// console.log(b); // ❌ ReferenceError: Cannot access 'b' before initialization
let b = 10;

// const behaves the same
// console.log(c); // ❌ ReferenceError
const c = 15;
```

> 💡 **Best practice:** Always declare variables and functions before using them. Don't rely on hoisting.

---

## Part 5: Closures (10 minutes)

### What Is a Closure?

A closure is a function that "remembers" variables from its parent scope even after the parent function has finished:

```javascript
function createGreeter(greeting) {
	// 'greeting' is "closed over" — remembered by the inner function
	return function (name) {
		return `${greeting}, ${name}!`;
	};
}

const sayHello = createGreeter('Hello');
const sayHi = createGreeter('Hi');

console.log(sayHello('Alice')); // "Hello, Alice!"
console.log(sayHi('Bob')); // "Hi, Bob!"
// 'greeting' variable persists even though createGreeter() finished!
```

### Practical Closure: Counter

```javascript
function createCounter(start = 0) {
	let count = start; // private variable — can't be accessed from outside

	return {
		increment: () => ++count,
		decrement: () => --count,
		getCount: () => count,
		reset: () => {
			count = start;
		},
	};
}

const counter = createCounter();
console.log(counter.increment()); // 1
console.log(counter.increment()); // 2
console.log(counter.increment()); // 3
console.log(counter.decrement()); // 2
console.log(counter.getCount()); // 2
counter.reset();
console.log(counter.getCount()); // 0

// count is truly private
// console.log(counter.count); // undefined — can't access directly!
```

### Practical Closure: Rate Limiter

```javascript
function createRateLimiter(maxCalls, timeWindow) {
	let callCount = 0;

	setInterval(() => {
		callCount = 0;
	}, timeWindow);

	return function () {
		if (callCount < maxCalls) {
			callCount++;
			return true; // allowed
		}
		return false; // rate limited
	};
}

const canCall = createRateLimiter(3, 5000); // 3 calls per 5 seconds
console.log(canCall()); // true
console.log(canCall()); // true
console.log(canCall()); // true
console.log(canCall()); // false — rate limited!
```

<details>
<summary>💡 Knowledge Check #4</summary>

**Question:** What is a closure, and why are they useful?

**Answer:**
A closure is a function that retains access to variables from its outer (enclosing) function's scope, even after the outer function has returned.

**Useful for:**

- **Data privacy** — variables can't be accessed from outside
- **State management** — maintaining state between function calls
- **Factory functions** — creating customized functions
- **Callbacks** — preserving context in async operations

</details>

---

## Part 6: Lab — Utility Function Library (15 minutes)

### Challenge: Build a Utility Library

Create `utility-functions.js` with these helper functions:

1. `capitalize(str)` — Capitalizes the first letter of a string
2. `clamp(value, min, max)` — Restricts a number within a range
3. `randomInt(min, max)` — Returns a random integer between min and max (inclusive)
4. `formatCurrency(amount, currency)` — Formats a number as currency
5. `createCounter(start)` — Returns a counter object (using closures)

**Starter Code:**

```javascript
// Utility Function Library

// 1. Capitalize first letter
function capitalize(str) {
	// TODO: Return string with first letter uppercase, rest lowercase
}

// 2. Clamp a number within a range
function clamp(value, min, max) {
	// TODO: Return value if within range, otherwise return min or max
}

// 3. Random integer between min and max (inclusive)
function randomInt(min, max) {
	// TODO: Use Math.random(), Math.floor()
}

// 4. Format as currency
function formatCurrency(amount, currency = '$') {
	// TODO: Return formatted string like "$12.50"
}

// 5. Create a counter (closure)
function createCounter(start = 0) {
	// TODO: Return object with increment, decrement, getCount, reset
}

// Test your functions!
console.log(capitalize('hello')); // "Hello"
console.log(clamp(15, 0, 10)); // 10
console.log(randomInt(1, 6)); // random 1-6
console.log(formatCurrency(9.5)); // "$9.50"

const counter = createCounter(10);
console.log(counter.increment()); // 11
console.log(counter.getCount()); // 11
```

<details>
<summary>✅ Solution</summary>

```javascript
function capitalize(str) {
	if (!str) return '';
	return str.charAt(0).toUpperCase() + str.slice(1).toLowerCase();
}

function clamp(value, min, max) {
	return Math.min(Math.max(value, min), max);
}

function randomInt(min, max) {
	return Math.floor(Math.random() * (max - min + 1)) + min;
}

function formatCurrency(amount, currency = '$') {
	return `${currency}${amount.toFixed(2)}`;
}

function createCounter(start = 0) {
	let count = start;
	return {
		increment: () => ++count,
		decrement: () => --count,
		getCount: () => count,
		reset: () => {
			count = start;
		},
	};
}

// Tests
console.log(capitalize('hello')); // "Hello"
console.log(capitalize('jAVASCRIPT')); // "Javascript"
console.log(clamp(15, 0, 10)); // 10
console.log(clamp(-5, 0, 10)); // 0
console.log(clamp(5, 0, 10)); // 5
console.log(randomInt(1, 6)); // random 1-6
console.log(formatCurrency(9.5)); // "$9.50"
console.log(formatCurrency(1234, '€')); // "€1234.00"

const counter = createCounter(10);
console.log(counter.increment()); // 11
console.log(counter.increment()); // 12
console.log(counter.decrement()); // 11
console.log(counter.getCount()); // 11
counter.reset();
console.log(counter.getCount()); // 10
```

</details>

---

## ⚠️ Common Mistakes

| Mistake                                     | Problem                                          | Fix                                           |
| ------------------------------------------- | ------------------------------------------------ | --------------------------------------------- |
| Forgetting `return`                         | Function returns `undefined`                     | Always add `return` for computed values       |
| Calling without `()`                        | References the function, doesn't run it          | `greet()` not `greet`                         |
| Modifying global variables inside functions | Creates hidden side effects                      | Pass values as parameters, return results     |
| Using `var` in loops                        | Variable leaks out of loop scope                 | Always use `let` or `const`                   |
| Arrow function returning object             | `() => { key: value }` is a block, not an object | Wrap in parentheses: `() => ({ key: value })` |

---

## 📝 Session Summary

In this session, you learned:

1. **Function declarations** — Hoisted, available before definition
2. **Function expressions** — Stored in variables, not hoisted
3. **Arrow functions** — Concise syntax, implicit return, lexical `this`
4. **Parameters & defaults** — Placeholders with fallback values
5. **Return values** — Functions produce output via `return`
6. **Scope** — Global, function, and block scope with `let`/`const`
7. **Hoisting** — Declarations are "moved" to the top of scope
8. **Closures** — Functions that remember their outer scope

---

## 🏠 Homework

### Task 1: Tip Calculator

Write functions:

- `calculateTip(bill, tipPercent)` — returns tip amount
- `calculateTotal(bill, tipPercent)` — returns bill + tip
- `splitBill(total, numPeople)` — returns amount per person
- Use `prompt()` to get inputs, display results with `alert()`

### Task 2: Temperature Converter

Create two functions:

- `celsiusToFahrenheit(c)` — converts C to F (`F = C * 9/5 + 32`)
- `fahrenheitToCelsius(f)` — converts F to C (`C = (F - 32) * 5/9`)
- Ask the user which conversion they want and the value
- Display the formatted result with 1 decimal place

### Task 3: Password Validator

Create `validatePassword(password)` that checks:

- At least 8 characters
- Contains at least one uppercase letter
- Contains at least one lowercase letter
- Contains at least one number
- Return an object: `{ isValid: true/false, errors: [...] }`

### Bonus Challenge: Function Composition

Create a `compose()` function that takes multiple functions and returns a new function that applies them in sequence (right to left):

```javascript
const add1 = (n) => n + 1;
const double = (n) => n * 2;
const square = (n) => n * n;

const transform = compose(add1, double, square);
console.log(transform(3)); // add1(double(square(3))) = add1(double(9)) = add1(18) = 19
```

---

## 📚 Resources

- [MDN: Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions)
- [MDN: Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
- [MDN: Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)
- [JavaScript.info: Functions](https://javascript.info/function-basics)
- [JavaScript.info: Function Expressions](https://javascript.info/function-expressions)
- [JavaScript.info: Arrow Functions](https://javascript.info/arrow-functions-basics)
- [JavaScript.info: Closure](https://javascript.info/closure)

---

**Next:** [Session 23 — Arrays & Iteration](session-23.md) →
