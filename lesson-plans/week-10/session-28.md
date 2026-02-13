# Week 10 — Session 28: Modern ES6+ Features

**Navigation:**
← [Session 27](../week-09/session-27.md) | [Week 10 Index](../week-10.md) | [Session 29](session-29.md) →

---

**Session Length:** 90 minutes

## 📋 Pre-Class Checklist

Before starting this session, make sure you have:

- ✅ Completed Weeks 07–09 (JS fundamentals, DOM, events)
- ✅ Comfortable with functions, arrays, objects, and the DOM
- ✅ Understand callbacks, closures, and event handling
- ✅ Create a new file: `es6-features.js`

## 🎯 Learning Objectives

By the end of this session, you will be able to:

- Use enhanced object literals and shorthand properties
- Apply destructuring in advanced scenarios
- Use the rest and spread operators fluently
- Work with `for...of` loops and iterables
- Understand and use ES6 modules (`import`/`export`)
- Apply `Map`, `Set`, and their use cases
- Use optional chaining and nullish coalescing in real code
- Write cleaner code with modern JavaScript patterns

## 📦 Files for This Session

- `session-28.md` — This tutorial (you're reading it!)
- Create: `es6-features.js`, `utils.js`

## 🔑 Key Terms

**ES6**, **ECMAScript 2015**, **module**, **import**, **export**, **default export**, **named export**, **Map**, **Set**, **Symbol**, **for...of**, **rest parameters**, **spread syntax**, **enhanced object literals**, **computed property names**, **tagged template literals**, **optional chaining**, **nullish coalescing**

## 🏗️ What You Will Build

- A modular utility library using ES6 modules
- A unique value filter using Sets
- A word frequency counter using Maps
- A data processing pipeline using chained modern methods

---

## Part 1: Advanced Destructuring & Spread (10 minutes)

### Nested Destructuring

```javascript
const response = {
	status: 200,
	data: {
		user: {
			id: 1,
			name: 'Alice',
			preferences: {
				theme: 'dark',
				language: 'en',
			},
		},
		posts: [
			{ id: 101, title: 'Hello World' },
			{ id: 102, title: 'ES6 Features' },
		],
	},
};

// Deep destructuring with renaming and defaults
const {
	status,
	data: {
		user: {
			name,
			preferences: { theme = 'light' },
		},
		posts: [firstPost, ...otherPosts],
	},
} = response;

console.log(name); // "Alice"
console.log(theme); // "dark"
console.log(firstPost); // { id: 101, title: "Hello World" }
console.log(otherPosts); // [{ id: 102, title: "ES6 Features" }]
```

### Rest Parameters

```javascript
// Rest parameters — collect remaining arguments into an array
function sum(...numbers) {
	return numbers.reduce((total, n) => total + n, 0);
}

console.log(sum(1, 2, 3)); // 6
console.log(sum(10, 20, 30, 40)); // 100

// Combine with regular parameters
function log(level, ...messages) {
	const prefix =
		level === 'error' ? '❌'
		: level === 'warn' ? '⚠️'
		: 'ℹ️';
	messages.forEach((msg) => console.log(`${prefix} ${msg}`));
}

log('error', 'File not found', 'Please check the path');
log('info', 'Server started');
```

### Advanced Spread Patterns

```javascript
// Conditional spread
const isDev = true;
const config = {
	host: 'localhost',
	port: 3000,
	...(isDev && { debug: true, verbose: true }),
};

// Merging with override
function createUser(overrides) {
	const defaults = {
		role: 'user',
		active: true,
		createdAt: new Date().toISOString(),
	};
	return { ...defaults, ...overrides };
}

const admin = createUser({ name: 'Alice', role: 'admin' });
console.log(admin); // { role: "admin", active: true, createdAt: "...", name: "Alice" }

// Removing properties with destructuring + rest
const { password, ...safeUser } = {
	name: 'Alice',
	email: 'a@b.com',
	password: 'secret',
};
console.log(safeUser); // { name: "Alice", email: "a@b.com" }
```

<details>
<summary>💡 Knowledge Check #1</summary>

**Question:** What does `const { a, ...rest } = { a: 1, b: 2, c: 3 }` produce?

**Answer:**

- `a` = `1`
- `rest` = `{ b: 2, c: 3 }`

The rest pattern (`...rest`) collects all remaining properties into a new object. This is useful for extracting specific properties while keeping the rest intact.

</details>

---

## Part 2: Enhanced Object Literals (10 minutes)

### Shorthand Properties & Methods

```javascript
const name = 'Alice';
const age = 25;
const role = 'developer';

// ❌ Old way
const user1 = { name: name, age: age, role: role };

// ✅ Shorthand (when variable name matches property name)
const user2 = { name, age, role };

// ❌ Old method syntax
const calc1 = {
	add: function (a, b) {
		return a + b;
	},
};

// ✅ Method shorthand
const calc2 = {
	add(a, b) {
		return a + b;
	},
	subtract(a, b) {
		return a - b;
	},
};
```

### Computed Property Names

```javascript
const field = 'email';
const value = 'alice@example.com';

// Dynamic keys using [expression]
const user = {
	name: 'Alice',
	[field]: value,
	[`${field}Verified`]: true,
	[`get${field.charAt(0).toUpperCase() + field.slice(1)}`]() {
		return this[field];
	},
};

console.log(user.email); // "alice@example.com"
console.log(user.emailVerified); // true
console.log(user.getEmail()); // "alice@example.com"

// Practical: object from array of key-value pairs
const entries = [
	['name', 'Alice'],
	['age', 25],
	['role', 'admin'],
];
const fromEntries = Object.fromEntries(entries);
console.log(fromEntries); // { name: "Alice", age: 25, role: "admin" }
```

### Tagged Template Literals

```javascript
// Tag functions process template literal parts
function highlight(strings, ...values) {
	return strings.reduce((result, str, i) => {
		const value =
			values[i] !== undefined ? `<mark>${values[i]}</mark>` : '';
		return result + str + value;
	}, '');
}

const name = 'Alice';
const score = 95;
const html = highlight`Student ${name} scored ${score} points!`;
console.log(html);
// "Student <mark>Alice</mark> scored <mark>95</mark> points!"

// Practical: SQL-safe queries (concept)
function sql(strings, ...values) {
	const sanitized = values.map((v) =>
		typeof v === 'string' ? v.replace(/'/g, "''") : v,
	);
	return strings.reduce(
		(result, str, i) => result + str + (sanitized[i] ?? ''),
		'',
	);
}
```

---

## Part 3: Map & Set (15 minutes)

### `Set` — Unique Values

A Set stores only unique values (no duplicates):

```javascript
// Creating a Set
const uniqueNums = new Set([1, 2, 3, 2, 1, 4, 3, 5]);
console.log(uniqueNums); // Set { 1, 2, 3, 4, 5 }
console.log(uniqueNums.size); // 5

// Methods
uniqueNums.add(6); // add a value
uniqueNums.add(3); // ignored — already exists!
uniqueNums.has(4); // true — check membership
uniqueNums.delete(1); // remove a value
uniqueNums.clear(); // remove all values

// Convert to array
const arr = [...uniqueNums];
// or: Array.from(uniqueNums)

// Practical: Remove duplicates from array
const names = ['Alice', 'Bob', 'Alice', 'Charlie', 'Bob'];
const uniqueNames = [...new Set(names)];
console.log(uniqueNames); // ["Alice", "Bob", "Charlie"]

// Set operations
const setA = new Set([1, 2, 3, 4]);
const setB = new Set([3, 4, 5, 6]);

// Union
const union = new Set([...setA, ...setB]); // {1, 2, 3, 4, 5, 6}

// Intersection
const intersection = new Set([...setA].filter((x) => setB.has(x))); // {3, 4}

// Difference
const difference = new Set([...setA].filter((x) => !setB.has(x))); // {1, 2}
```

### `Map` — Any-Type Keys

A Map is like an object but with any type as keys and maintains insertion order:

```javascript
// Creating a Map
const userRoles = new Map();

// Set key-value pairs (any type as key!)
userRoles.set('alice', 'admin');
userRoles.set('bob', 'editor');
userRoles.set(42, 'special user'); // number key
userRoles.set(true, 'boolean key'); // boolean key

// Get values
console.log(userRoles.get('alice')); // "admin"
console.log(userRoles.get(42)); // "special user"

// Check & delete
console.log(userRoles.has('bob')); // true
userRoles.delete('bob');
console.log(userRoles.size); // 3

// Iterate
userRoles.forEach((value, key) => {
	console.log(`${key} → ${value}`);
});

for (const [key, value] of userRoles) {
	console.log(`${key}: ${value}`);
}

// Convert from/to Object
const obj = { a: 1, b: 2, c: 3 };
const map = new Map(Object.entries(obj));
const backToObj = Object.fromEntries(map);
```

### When to Use Map vs Object

| Feature                           | Object                    | Map                |
| --------------------------------- | ------------------------- | ------------------ |
| Key types                         | Strings/Symbols only      | Any type           |
| Key order                         | Not guaranteed            | Insertion order    |
| Size                              | `Object.keys(obj).length` | `map.size`         |
| Iteration                         | `Object.entries()`        | Built-in           |
| Performance (frequent add/delete) | Slower                    | Faster             |
| JSON support                      | `JSON.stringify` works    | Must convert first |

### Practical: Word Frequency Counter with Map

```javascript
function wordFrequency(text) {
	const counts = new Map();
	const words = text.toLowerCase().split(/\s+/);

	for (const word of words) {
		counts.set(word, (counts.get(word) || 0) + 1);
	}

	// Sort by frequency (most common first)
	return new Map([...counts.entries()].sort((a, b) => b[1] - a[1]));
}

const freq = wordFrequency('the cat sat on the mat the cat ate the hat');
for (const [word, count] of freq) {
	console.log(`${word}: ${count}`);
}
// the: 4, cat: 2, sat: 1, on: 1, mat: 1, ate: 1, hat: 1
```

<details>
<summary>💡 Knowledge Check #2</summary>

**Question:** How do you remove duplicate values from an array using a Set?

**Answer:**

```javascript
const arr = [1, 2, 3, 2, 1, 4, 3];
const unique = [...new Set(arr)];
console.log(unique); // [1, 2, 3, 4]
```

1. `new Set(arr)` creates a Set with only unique values
2. `[...set]` (spread) converts the Set back to an array

</details>

---

## Part 4: ES6 Modules (15 minutes)

### Why Modules?

- Split code into separate files
- Explicit dependencies (import what you need)
- Avoid global scope pollution
- Reusable across projects

### Named Exports & Imports

```javascript
// utils.js — EXPORTING
export function capitalize(str) {
	return str.charAt(0).toUpperCase() + str.slice(1);
}

export function slugify(str) {
	return str.toLowerCase().replace(/\s+/g, '-');
}

export const PI = 3.14159;

// Can also export at the end
function helper() {
	/* ... */
}
export { helper };
```

```javascript
// main.js — IMPORTING
import { capitalize, slugify, PI } from './utils.js';

console.log(capitalize('hello')); // "Hello"
console.log(slugify('Hello World')); // "hello-world"
console.log(PI); // 3.14159

// Rename on import
import { capitalize as cap } from './utils.js';

// Import everything
import * as utils from './utils.js';
console.log(utils.capitalize('hi')); // "Hi"
```

### Default Exports

```javascript
// User.js — one default export per file
export default class User {
	constructor(name, email) {
		this.name = name;
		this.email = email;
	}

	greet() {
		return `Hi, I'm ${this.name}!`;
	}
}
```

```javascript
// main.js — import default (no curly braces, any name)
import User from './User.js';
// or: import MyUser from "./User.js"; // any name works!

const alice = new User('Alice', 'alice@example.com');
console.log(alice.greet()); // "Hi, I'm Alice!"
```

### Using Modules in HTML

```html
<!-- type="module" enables ES6 imports -->
<script
	type="module"
	src="main.js"
></script>

<!-- Modules are deferred by default (no need for defer attribute) -->
<!-- Modules have their own scope (no global pollution) -->
<!-- Modules run in strict mode automatically -->
```

### Module Patterns

```javascript
// Re-exporting (barrel file)
// index.js
export { capitalize, slugify } from './string-utils.js';
export { formatDate, parseDate } from './date-utils.js';
export { default as User } from './User.js';

// Then import from one place
import { capitalize, formatDate, User } from './index.js';
```

<details>
<summary>💡 Knowledge Check #3</summary>

**Question:** What is the difference between a named export and a default export?

**Answer:**
| Feature | Named Export | Default Export |
|---------|-------------|----------------|
| Syntax (export) | `export function foo()` | `export default function()` |
| Syntax (import) | `import { foo }` (braces) | `import foo` (no braces) |
| Per file | Multiple allowed | Only ONE |
| Name required? | Must use same name (or rename with `as`) | Can use any name |
| Use case | Multiple utilities from one file | Main export of a module |

</details>

---

## Part 5: Optional Chaining & Useful Patterns (10 minutes)

### Optional Chaining (`?.`) Deep Dive

```javascript
const user = {
	name: 'Alice',
	address: {
		street: '123 Main St',
	},
};

// Safe property access
console.log(user?.address?.street); // "123 Main St"
console.log(user?.address?.zip); // undefined
console.log(user?.phone?.number); // undefined (no crash!)

// Safe method calls
const arr = [1, 2, 3];
console.log(arr?.map?.((x) => x * 2)); // [2, 4, 6]
console.log(null?.map?.((x) => x * 2)); // undefined

// With bracket notation
const key = 'address';
console.log(user?.[key]?.street); // "123 Main St"

// Combine with nullish coalescing
const city = user?.address?.city ?? 'Unknown';
console.log(city); // "Unknown"
```

### Logical Assignment Operators (ES2021)

```javascript
// ||= assigns if the left side is falsy
let name = '';
name ||= 'Guest'; // name = "Guest" (empty string is falsy)

// ??= assigns if the left side is null/undefined
let count = 0;
count ??= 10; // count stays 0 (0 is not null/undefined)

let missing = null;
missing ??= 'default'; // missing = "default"

// &&= assigns if the left side is truthy
let user = { name: 'Alice' };
user.name &&= user.name.toUpperCase(); // "ALICE"
```

### `Object.assign()` vs Spread

```javascript
// Both merge objects, but spread is newer & preferred
const a = { x: 1 };
const b = { y: 2 };

const merged1 = Object.assign({}, a, b); // { x: 1, y: 2 }
const merged2 = { ...a, ...b }; // { x: 1, y: 2 }

// Object.assign mutates the first argument
const target = { x: 1 };
Object.assign(target, { y: 2 }); // target is now { x: 1, y: 2 }

// Spread always creates a new object (non-mutating)
```

---

## Part 6: Lab — Modular Data Processor (10 minutes)

### Challenge

Build a data processing pipeline using modern ES6+ features:

```javascript
// Given this data:
const salesData = [
	{
		product: 'Laptop',
		category: 'Electronics',
		price: 999,
		qty: 5,
		date: '2024-01-15',
	},
	{
		product: 'Phone',
		category: 'Electronics',
		price: 699,
		qty: 12,
		date: '2024-01-16',
	},
	{
		product: 'Desk',
		category: 'Furniture',
		price: 350,
		qty: 3,
		date: '2024-01-15',
	},
	{
		product: 'Chair',
		category: 'Furniture',
		price: 250,
		qty: 8,
		date: '2024-01-16',
	},
	{
		product: 'Laptop',
		category: 'Electronics',
		price: 999,
		qty: 3,
		date: '2024-01-17',
	},
	{
		product: 'Monitor',
		category: 'Electronics',
		price: 450,
		qty: 6,
		date: '2024-01-17',
	},
	{
		product: 'Desk',
		category: 'Furniture',
		price: 350,
		qty: 2,
		date: '2024-01-17',
	},
];

// TODO 1: Get unique product names using Set

// TODO 2: Get unique categories using Set

// TODO 3: Group sales by category using Map or reduce

// TODO 4: Calculate total revenue per category

// TODO 5: Find the best-selling product (highest total qty)

// TODO 6: Create a summary object using destructuring and spread
```

<details>
<summary>✅ Solution</summary>

```javascript
// 1. Unique products
const uniqueProducts = [...new Set(salesData.map((s) => s.product))];
console.log('Products:', uniqueProducts);

// 2. Unique categories
const categories = [...new Set(salesData.map((s) => s.category))];
console.log('Categories:', categories);

// 3. Group by category
const byCategory = new Map();
for (const sale of salesData) {
	const existing = byCategory.get(sale.category) ?? [];
	byCategory.set(sale.category, [...existing, sale]);
}
console.log('Grouped:', byCategory);

// 4. Revenue per category
const revenueByCategory = Object.fromEntries(
	[...byCategory.entries()].map(([cat, sales]) => [
		cat,
		sales.reduce((sum, s) => sum + s.price * s.qty, 0),
	]),
);
console.log('Revenue:', revenueByCategory);

// 5. Best-selling product
const qtyByProduct = salesData.reduce((acc, { product, qty }) => {
	acc.set(product, (acc.get(product) ?? 0) + qty);
	return acc;
}, new Map());

const [bestProduct, bestQty] = [...qtyByProduct.entries()].reduce(
	(max, entry) => (entry[1] > max[1] ? entry : max),
);
console.log(`Best seller: ${bestProduct} (${bestQty} units)`);

// 6. Summary
const summary = {
	totalProducts: uniqueProducts.length,
	categories: categories.length,
	totalRevenue: salesData.reduce((sum, s) => sum + s.price * s.qty, 0),
	revenueByCategory,
	bestSeller: { product: bestProduct, totalQty: bestQty },
	dateRange: {
		start: salesData.reduce(
			(min, s) => (s.date < min ? s.date : min),
			salesData[0].date,
		),
		end: salesData.reduce(
			(max, s) => (s.date > max ? s.date : max),
			salesData[0].date,
		),
	},
};
console.log('Summary:', JSON.stringify(summary, null, 2));
```

</details>

---

## ⚠️ Common Mistakes

| Mistake                          | Problem                            | Fix                                    |
| -------------------------------- | ---------------------------------- | -------------------------------------- |
| Circular imports                 | Module A imports B which imports A | Restructure to avoid circular deps     |
| Missing `type="module"` in HTML  | `import` syntax error in browser   | Add `type="module"` to script tag      |
| Using `??` when you mean `\|\|`  | `0 ?? fallback` keeps 0            | Use `\|\|` when 0 should be falsy      |
| Mutating Map/Set while iterating | Unpredictable behavior             | Create a copy first or collect deletes |
| Forgetting `.js` in import paths | Module not found in browsers       | Always include file extension          |

---

## 📝 Session Summary

In this session, you learned:

1. **Advanced destructuring** — Nested, renamed, defaults, rest patterns
2. **Enhanced objects** — Shorthand properties, computed keys, method shorthand
3. **Set** — Unique values, deduplication, set operations
4. **Map** — Any-type keys, ordered, better for dynamic key-value storage
5. **ES6 Modules** — `import`/`export`, named vs default, organizing code
6. **Optional chaining & nullish coalescing** — Safe property access
7. **Logical assignment** — `||=`, `??=`, `&&=`

---

## 🏠 Homework

### Task 1: Module Refactor

Take your utility functions from Session 22 and refactor them into ES6 modules:

- `string-utils.js` (capitalize, slugify, truncate)
- `math-utils.js` (clamp, randomInt, average)
- `array-utils.js` (unique, chunk, flatten)
- `index.js` (re-export everything)

### Task 2: Unique Tags Counter

Given an array of blog post objects (each with a `tags` array), use Sets and Maps to:

- Find all unique tags
- Count how many posts each tag appears in
- Find the most popular tag

### Task 3: Config Manager with Optional Chaining

Build a configuration manager that:

- Loads nested config from a JSON string
- Uses optional chaining for safe deep access
- Uses nullish coalescing for default values
- Supports setting values at deep paths

### Bonus: Simple Build Pipeline

Create a simple text processing pipeline using function composition with ES6 features:

```javascript
const pipeline = compose(
	(text) => text.trim(),
	(text) => text.toLowerCase(),
	(text) => text.replace(/\s+/g, ' '),
	(text) => text.split(' '),
	(words) => [...new Set(words)],
	(words) => words.sort(),
);
```

---

## 📚 Resources

- [MDN: JavaScript Modules](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)
- [MDN: Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)
- [MDN: Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)
- [MDN: Optional Chaining](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)
- [JavaScript.info: Modules](https://javascript.info/modules-intro)
- [JavaScript.info: Map and Set](https://javascript.info/map-set)

---

**Next:** [Session 29 — Async JavaScript & Fetch API](session-29.md) →
