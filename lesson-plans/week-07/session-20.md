# Week 07 — Session 20: Variables, Constants & Data Types

**Navigation:**
← [Session 19](session-19.md) | [Week 07 Index](../week-07.md) | [Session 21](session-21.md) →

---

**Session Length:** 90 minutes

## 📋 Pre-Class Checklist

Before starting this session, make sure you have:

- ✅ Completed Session 19 (Introduction to JavaScript)
- ✅ Your `week-07-js-basics` project folder open in VS Code
- ✅ Browser DevTools Console accessible (F12)
- ✅ Understand how to link an external `.js` file to HTML

## 🎯 Learning Objectives

By the end of this session, you will be able to:

- Declare variables using `let` and constants using `const`
- Explain why `var` exists and why we prefer `let`/`const`
- Identify and use all 7 primitive data types in JavaScript
- Use `typeof` to check data types at runtime
- Understand implicit type coercion and avoid its pitfalls
- Explicitly convert between data types
- Explain the difference between `==` and `===`

## 📦 Files for This Session

- `session-20.md` — This tutorial (you're reading it!)
- Create a new file: `variables.js`

## 🔑 Key Terms

**variable**, **constant**, **`let`**, **`const`**, **`var`**, **declaration**, **assignment**, **reassignment**, **primitive**, **string**, **number**, **boolean**, **null**, **undefined**, **symbol**, **BigInt**, **`typeof`**, **type coercion**, **type conversion**, **strict equality**, **loose equality**, **hoisting**, **temporal dead zone**

---

## Part 1: Variables with `let` (15 minutes)

### What is a Variable?

A variable is a **named container** that stores a value. Think of it like a labeled box:

```
┌──────────────┐
│  age  →  25  │   A box labeled "age" containing the value 25
└──────────────┘
```

### Declaring and Assigning Variables

```javascript
// Declaration: create the box
let age;
console.log(age); // undefined — the box exists but is empty

// Assignment: put a value in the box
age = 25;
console.log(age); // 25

// Declaration + Assignment in one step (most common)
let name = 'Alice';
console.log(name); // "Alice"

// Reassignment: change the value in the box
name = 'Bob';
console.log(name); // "Bob"
```

### Variable Naming Rules

JavaScript has strict rules for variable names:

| Rule                                  | Valid ✅                   | Invalid ❌                        |
| ------------------------------------- | -------------------------- | --------------------------------- |
| Must start with a letter, `$`, or `_` | `name`, `$price`, `_count` | `1name`, `@value`                 |
| Can contain letters, digits, `$`, `_` | `item1`, `total_price`     | `my-var`, `my var`                |
| Case-sensitive                        | `Name` ≠ `name` ≠ `NAME`   | —                                 |
| Cannot be reserved words              | `myClass`, `letValue`      | `let`, `const`, `class`, `return` |

### Naming Conventions

```javascript
// ✅ camelCase (JavaScript standard)
let firstName = 'Alice';
let totalPrice = 29.99;
let isLoggedIn = true;
let numberOfStudents = 30;

// ❌ Avoid these styles in JavaScript
let first_name = 'Alice'; // snake_case (Python style)
let FirstName = 'Alice'; // PascalCase (for classes only)
let FIRSTNAME = 'Alice'; // SCREAMING_CASE (for true constants only)
```

> 💡 **Best practice:** Use descriptive, camelCase names. `studentAge` is better than `a` or `x`.

### Multiple Declarations

```javascript
// Declare multiple variables (each on its own line for readability)
let city = 'Lagos';
let country = 'Nigeria';
let population = 16000000;

// You CAN declare on one line (less readable)
let x = 1,
	y = 2,
	z = 3;
```

<details>
<summary>💡 Knowledge Check #1</summary>

**Question:** Which of these are valid variable names?

```javascript
let 2fast = "car";
let _private = true;
let my-name = "Alice";
let $price = 9.99;
let class = "math";
let firstName = "Bob";
```

**Answer:**

- `2fast` — ❌ Cannot start with a digit
- `_private` — ✅ Can start with underscore
- `my-name` — ❌ Hyphens are not allowed
- `$price` — ✅ Can start with dollar sign
- `class` — ❌ `class` is a reserved keyword
- `firstName` — ✅ Valid camelCase name

</details>

---

## Part 2: Constants with `const` (10 minutes)

### What is a Constant?

A **constant** is a variable whose value **cannot be reassigned** after initialization.

```javascript
const PI = 3.14159;
const SITE_NAME = 'Frontend Fundamentals';
const MAX_STUDENTS = 30;

// This will throw an error:
PI = 3.14; // ❌ TypeError: Assignment to constant variable
```

### When to Use `const` vs `let`

```javascript
// Use const when the value won't change (DEFAULT CHOICE)
const birthday = '1999-05-15';
const username = 'alice_dev';
const apiUrl = 'https://api.example.com';

// Use let when the value WILL change
let score = 0;
score = score + 10; // ✅ Reassignment is fine

let isGameOver = false;
isGameOver = true; // ✅ State changes

let counter = 1;
counter++; // ✅ Incrementing
```

> 🏆 **Best practice:** Default to `const`. Only use `let` when you know the value needs to change. Never use `var` in new code.

### `const` with Objects and Arrays (Preview)

A subtle but important point — `const` prevents **reassignment**, not **mutation**:

```javascript
const colors = ['red', 'green', 'blue'];
colors.push('yellow'); // ✅ This works! (modifying the array)
console.log(colors); // ["red", "green", "blue", "yellow"]

colors = ['pink', 'gold']; // ❌ TypeError! (reassigning the variable)

const user = { name: 'Alice', age: 25 };
user.age = 26; // ✅ This works! (modifying a property)
user = { name: 'Bob' }; // ❌ TypeError! (reassigning the variable)
```

> Think of `const` as: "I will always point to the **same box**, but the contents of the box can change."

<details>
<summary>💡 Knowledge Check #2</summary>

**Question:** What will happen when this code runs?

```javascript
const greeting = 'Hello';
greeting = 'Hi';
console.log(greeting);
```

**Answer:** A `TypeError: Assignment to constant variable` will be thrown on line 2. The `console.log` never runs. `const` prevents reassignment.

</details>

---

## Part 3: Legacy `var` and Hoisting (10 minutes)

### Why Does `var` Still Exist?

Before ES6 (2015), `var` was the only way to declare variables. You'll see it in older code, tutorials, and Stack Overflow answers. Understanding it helps you read existing code and avoid bugs.

### Key Differences: `var` vs `let`/`const`

| Feature       | `var`                         | `let` / `const`      |
| ------------- | ----------------------------- | -------------------- |
| Scope         | Function scope                | Block scope `{ }`    |
| Redeclare     | ✅ Allowed                    | ❌ Error             |
| Hoisting      | Hoisted (value = `undefined`) | Hoisted (but in TDZ) |
| Global object | Adds to `window`              | Does not             |

### Scope Difference (The Big One)

```javascript
// var — function scoped (ignores blocks)
if (true) {
	var x = 10;
}
console.log(x); // 10 — var "leaks" out of the block! 😱

// let — block scoped (stays inside the block)
if (true) {
	let y = 20;
}
console.log(y); // ❌ ReferenceError: y is not defined ✅ (expected!)
```

### Hoisting

**Hoisting** means JavaScript moves declarations to the top of their scope before running the code:

```javascript
// What you write:
console.log(a); // undefined (not an error!)
var a = 5;

// What JavaScript sees:
var a; // Declaration hoisted to top
console.log(a); // undefined
a = 5; // Assignment stays in place

// With let:
console.log(b); // ❌ ReferenceError: Cannot access 'b' before initialization
let b = 5;
```

> `let` and `const` are hoisted too, but they sit in a **Temporal Dead Zone (TDZ)** until their declaration is reached — accessing them before that throws an error, which is actually **safer** behavior.

### The Problem with `var` in Loops

```javascript
// Classic var bug
for (var i = 0; i < 3; i++) {
	setTimeout(() => console.log(i), 100);
}
// Prints: 3, 3, 3 (not 0, 1, 2!)

// Fixed with let
for (let j = 0; j < 3; j++) {
	setTimeout(() => console.log(j), 100);
}
// Prints: 0, 1, 2 ✅
```

> 🚫 **Rule:** Never use `var` in new code. Always use `const` (default) or `let` (when reassignment is needed).

<details>
<summary>💡 Knowledge Check #3</summary>

**Question:** What does "hoisting" mean, and how does it behave differently with `var` vs `let`?

**Answer:**

- **Hoisting** = JavaScript moves variable declarations to the top of their scope before execution
- **`var`** — Hoisted and initialized to `undefined`. You can access it before declaration (but the value is `undefined`)
- **`let`/`const`** — Hoisted but placed in the **Temporal Dead Zone (TDZ)**. Accessing before declaration throws a `ReferenceError`, which is safer because it reveals bugs

</details>

---

## Part 4: Primitive Data Types (20 minutes)

JavaScript has **7 primitive data types** — these are the basic building blocks of all data.

### 1. String — Text Data

Strings hold text. You can create them with single quotes, double quotes, or backticks:

```javascript
const single = 'Hello'; // Single quotes
const double = 'World'; // Double quotes
const backtick = `Hello World`; // Template literal (backtick)

// Strings have useful properties and methods
console.log(single.length); // 5
console.log(double.toUpperCase()); // "WORLD"
console.log(backtick.includes('World')); // true

// Escape characters
const quote = 'She said "hello"'; // Mixed quotes
const escaped = 'She said "hello"'; // Escape with backslash
const newLine = 'Line 1\nLine 2'; // \n = new line
const tab = 'Col1\tCol2'; // \t = tab
```

### 2. Number — Numeric Data

JavaScript has a single `number` type for both integers and decimals:

```javascript
const integer = 42;
const decimal = 3.14;
const negative = -10;

// Special numeric values
const infinity = Infinity;
const negInfinity = -Infinity;
const notANumber = NaN; // "Not a Number"

// Math operations
console.log(10 / 3); // 3.3333...
console.log(10 % 3); // 1 (remainder/modulo)
console.log(2 ** 10); // 1024 (exponentiation)

// Checking for special values
console.log(isNaN('hello' * 2)); // true
console.log(isFinite(100)); // true
console.log(isFinite(Infinity)); // false
```

### 3. Boolean — True/False

```javascript
const isStudent = true;
const hasGraduated = false;

// Booleans are the result of comparisons
console.log(10 > 5); // true
console.log(10 === 5); // false
console.log('a' < 'b'); // true (alphabetical)
```

### 4. Null — Intentional Absence

`null` means "I explicitly set this to nothing":

```javascript
let selectedUser = null; // No user selected yet
console.log(selectedUser); // null

// Later...
selectedUser = { name: 'Alice' }; // Now we have a user
```

### 5. Undefined — Not Yet Assigned

`undefined` means "this exists but has no value yet":

```javascript
let score;
console.log(score); // undefined — declared but not assigned

function greet() {
	// no return statement
}
console.log(greet()); // undefined — functions return undefined by default
```

### 6. Symbol — Unique Identifier (Advanced)

```javascript
const id1 = Symbol('id');
const id2 = Symbol('id');
console.log(id1 === id2); // false — every Symbol is unique!
```

> 💡 Symbols are rarely used in beginner code. Just know they exist.

### 7. BigInt — Very Large Numbers

```javascript
const huge = 9007199254740991n; // Add 'n' suffix
const also = BigInt('9007199254740991');
console.log(huge + 1n); // 9007199254740992n
```

> 💡 BigInt is for numbers larger than `Number.MAX_SAFE_INTEGER`. You probably won't need it often.

### Quick Reference Table

| Type      | Example         | `typeof` Result | Description         |
| --------- | --------------- | --------------- | ------------------- |
| String    | `"hello"`       | `"string"`      | Text data           |
| Number    | `42`, `3.14`    | `"number"`      | Numeric data        |
| Boolean   | `true`, `false` | `"boolean"`     | Logical values      |
| Null      | `null`          | `"object"` ⚠️   | Intentional absence |
| Undefined | `undefined`     | `"undefined"`   | Not assigned        |
| Symbol    | `Symbol("x")`   | `"symbol"`      | Unique identifier   |
| BigInt    | `42n`           | `"bigint"`      | Large integers      |

> ⚠️ `typeof null === "object"` is a famous JavaScript bug from 1995 that was never fixed for backward compatibility!

<details>
<summary>💡 Knowledge Check #4</summary>

**Question:** What is the difference between `null` and `undefined`?

**Answer:**

- **`null`** — Intentionally assigned by the developer to mean "empty" or "no value." It's a deliberate choice.
- **`undefined`** — The default value automatically assigned by JavaScript when a variable is declared but not initialized.

```javascript
let a; // undefined (JS assigned it)
let b = null; // null (developer assigned it)
```

</details>

---

## Part 5: Type Checking with `typeof` (10 minutes)

### Using `typeof`

The `typeof` operator tells you what type a value is:

```javascript
console.log(typeof 'hello'); // "string"
console.log(typeof 42); // "number"
console.log(typeof true); // "boolean"
console.log(typeof undefined); // "undefined"
console.log(typeof null); // "object" (⚠️ historical bug!)
console.log(typeof Symbol('x')); // "symbol"
console.log(typeof 42n); // "bigint"

// Practical use: checking before operations
const input = prompt('Enter a number:');
console.log(typeof input); // "string" (always!)
```

### Practical Example: Type-Safe Input

```javascript
function processAge(input) {
	console.log('Raw input:', input, 'Type:', typeof input);

	if (typeof input !== 'string') {
		console.error('Expected a string input');
		return;
	}

	const age = Number(input);

	if (isNaN(age)) {
		console.error("That's not a valid number!");
		return;
	}

	console.log('Your age is:', age, 'Type:', typeof age);
}

processAge(prompt('Enter your age:'));
```

---

## Part 6: Type Coercion & Conversion (15 minutes)

### Implicit Coercion (Automatic)

JavaScript automatically converts types in certain situations. This is called **type coercion**:

```javascript
// String + Number → String (concatenation wins)
console.log('5' + 3); // "53" 😱 (string concatenation)
console.log('Hello' + 42); // "Hello42"

// String - Number → Number (math wins)
console.log('10' - 3); // 7
console.log('10' * 2); // 20
console.log('10' / 5); // 2

// Boolean in math context
console.log(true + 1); // 2 (true → 1)
console.log(false + 1); // 1 (false → 0)

// Comparison coercion
console.log('5' == 5); // true (loose comparison, coerces types)
console.log('5' === 5); // false (strict comparison, no coercion)
```

### The `==` vs `===` Trap

```javascript
// == (loose equality) — converts types before comparing
console.log(0 == false); // true  (0 → false)
console.log('' == false); // true  ("" → false)
console.log(null == undefined); // true  (special rule)
console.log('1' == 1); // true  ("1" → 1)

// === (strict equality) — no conversion, must be same type AND value
console.log(0 === false); // false (number vs boolean)
console.log('' === false); // false (string vs boolean)
console.log('1' === 1); // false (string vs number)
console.log(1 === 1); // true  ✅
```

> 🏆 **Rule:** Always use `===` and `!==` (strict). Forget that `==` exists.

### Explicit Conversion (Manual)

Convert types intentionally using built-in functions:

```javascript
// To Number
console.log(Number('42')); // 42
console.log(Number('3.14')); // 3.14
console.log(Number('hello')); // NaN
console.log(Number(true)); // 1
console.log(Number(false)); // 0
console.log(Number(null)); // 0
console.log(Number(undefined)); // NaN

console.log(parseInt('42px')); // 42 (stops at first non-digit)
console.log(parseFloat('3.14em')); // 3.14

// To String
console.log(String(42)); // "42"
console.log(String(true)); // "true"
console.log(String(null)); // "null"
console.log((42).toString()); // "42"

// To Boolean
console.log(Boolean(0)); // false
console.log(Boolean('')); // false
console.log(Boolean(null)); // false
console.log(Boolean(undefined)); // false
console.log(Boolean(NaN)); // false

console.log(Boolean(1)); // true
console.log(Boolean('hello')); // true
console.log(Boolean(42)); // true
console.log(Boolean('false')); // true! ⚠️ (non-empty string)
console.log(Boolean([])); // true! ⚠️ (empty array is truthy)
```

<details>
<summary>💡 Knowledge Check #5</summary>

**Question:** What is the output of each line?

```javascript
console.log('5' + 3);
console.log('5' - 3);
console.log(Boolean(''));
console.log(Boolean('false'));
console.log(0 === false);
```

**Answer:**

- `"5" + 3` → `"53"` (string concatenation, `+` with string converts to string)
- `"5" - 3` → `2` (subtraction forces numeric conversion)
- `Boolean("")` → `false` (empty string is falsy)
- `Boolean("false")` → `true` (non-empty string is truthy — the word "false" is still a string!)
- `0 === false` → `false` (strict equality, different types: number vs boolean)

</details>

---

## Part 7: Lab — Variable Explorer (10 minutes)

### Challenge: Type Detective

Create a file called `type-detective.js` and complete these exercises:

```javascript
// === Variable Explorer Lab ===

// 1. Declare a variable of EVERY primitive type
let myString = ______;
let myNumber = ______;
let myBoolean = ______;
let myNull = ______;
let myUndefined; // don't assign anything
const mySymbol = Symbol('test');
const myBigInt = ______;

// 2. Log each with its type
console.log('String:', myString, '→', typeof myString);
console.log('Number:', myNumber, '→', typeof myNumber);
console.log('Boolean:', myBoolean, '→', typeof myBoolean);
console.log('Null:', myNull, '→', typeof myNull, '(⚠️ bug!)');
console.log('Undefined:', myUndefined, '→', typeof myUndefined);
console.log('Symbol:', mySymbol, '→', typeof mySymbol);
console.log('BigInt:', myBigInt, '→', typeof myBigInt);

// 3. Coercion challenges — predict the output BEFORE running!
console.log('--- Coercion Challenges ---');
console.log('10' + 5); // Predict: ______
console.log('10' - 5); // Predict: ______
console.log(true + true); // Predict: ______
console.log('5' * '3'); // Predict: ______
console.log(null + 1); // Predict: ______
console.log(undefined + 1); // Predict: ______

// 4. Conversion practice
const userInput = '42.5px';
const parsed = parseFloat(userInput);
console.log('Parsed:', parsed, typeof parsed);
```

<details>
<summary>✅ Solution</summary>

```javascript
let myString = 'Hello, JavaScript!';
let myNumber = 42;
let myBoolean = true;
let myNull = null;
let myUndefined;
const mySymbol = Symbol('test');
const myBigInt = 9007199254740991n;

// Coercion answers:
console.log('10' + 5); // "105" (string concatenation)
console.log('10' - 5); // 5 (numeric subtraction)
console.log(true + true); // 2 (1 + 1)
console.log('5' * '3'); // 15 (both convert to numbers)
console.log(null + 1); // 1 (null → 0)
console.log(undefined + 1); // NaN (undefined → NaN)
```

</details>

---

## ⚠️ Common Mistakes

| Mistake                                 | Problem                                 | Fix                                     |
| --------------------------------------- | --------------------------------------- | --------------------------------------- |
| Using `var` instead of `let`/`const`    | Scope leaks, hoisting bugs              | Always use `const` (default) or `let`   |
| Using `==` instead of `===`             | Unexpected type coercion in comparisons | Always use strict equality `===`        |
| Expecting `prompt()` to return a number | It always returns a string              | Convert with `Number()` or `parseInt()` |
| `typeof null === "object"` confusion    | Historical bug, null IS a primitive     | Check explicitly: `value === null`      |
| Not initializing `const`                | `const x;` → SyntaxError                | Always assign: `const x = value;`       |
| Concatenating when you want to add      | `"5" + 3 = "53"` not `8`                | Convert first: `Number("5") + 3`        |

---

## 📝 Session Summary

In this session, you learned:

1. **`let`** — Declare variables that can be reassigned, block-scoped
2. **`const`** — Declare constants that cannot be reassigned, block-scoped (default choice)
3. **`var`** — Legacy keyword, function-scoped, avoid in new code
4. **7 Primitive Types** — string, number, boolean, null, undefined, symbol, BigInt
5. **`typeof`** — Operator to check data types at runtime
6. **Type Coercion** — JavaScript auto-converts types (beware `+` with strings!)
7. **Type Conversion** — Manual conversion with `Number()`, `String()`, `Boolean()`, `parseInt()`
8. **Strict Equality** — Always use `===` over `==`

---

## 🏠 Homework

### Task 1: Person Profile

Create variables for a person's profile using appropriate types and `const`/`let`:

- Full name (string)
- Age (number)
- Email (string)
- Is student? (boolean)
- GPA (number)
- Graduation date (null — hasn't graduated yet)

Log each with its `typeof` result.

### Task 2: Temperature Converter

Write a program that:

1. Uses `prompt()` to ask for a temperature in Fahrenheit
2. Converts the input to a number using `Number()`
3. Calculates Celsius: `(F - 32) × 5/9`
4. Displays the result using `alert()` and `console.log()`

### Task 3: Type Coercion Quiz

For each expression, predict the output, then verify in the console:

```javascript
'' + 1 + 0;
'' - 1 + 0;
true + false;
'2' * '3';
4 + 5 + 'px';
'$' + 4 + 5;
'4' - 2;
'4px' - 2;
null + 1;
undefined + 1;
```

### Bonus Challenge: Type Checker Function

Write a function called `describeType(value)` that takes any value and logs:

- The value itself
- Its `typeof` result
- Whether it's truthy or falsy
- A human-readable description

---

## 📚 Resources

- [MDN: let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
- [MDN: const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)
- [MDN: Data Types and Data Structures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)
- [MDN: typeof](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof)
- [JavaScript.info: Data Types](https://javascript.info/types)
- [JavaScript.info: Type Conversions](https://javascript.info/type-conversions)

---

**Next:** [Session 21 — Operators, Expressions & Control Flow](session-21.md) →
