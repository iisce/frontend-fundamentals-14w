# Week 08 — Session 24: Objects & JSON

**Navigation:**
← [Session 23](session-23.md) | [Week 08 Index](../week-08.md) | [Session 25](../week-09/session-25.md) →

---

**Session Length:** 90 minutes

## 📋 Pre-Class Checklist

Before starting this session, make sure you have:

- ✅ Completed Session 23 (Arrays & Iteration)
- ✅ Comfortable with array methods (`map`, `filter`, `reduce`)
- ✅ Understand functions and scope
- ✅ Create a new file: `objects.js`

## 🎯 Learning Objectives

By the end of this session, you will be able to:

- Create objects using object literals and access properties
- Add, modify, and delete object properties
- Use dot notation vs bracket notation appropriately
- Iterate over object properties with `for...in` and `Object.keys/values/entries`
- Nest objects and arrays within objects
- Understand and work with JSON (parse and stringify)
- Apply destructuring and spread with objects
- Use `this` keyword in object methods

## 📦 Files for This Session

- `session-24.md` — This tutorial (you're reading it!)
- Create: `objects.js`, `contact-book.js`

## 🔑 Key Terms

**object**, **property**, **key**, **value**, **method**, **dot notation**, **bracket notation**, **nested object**, **JSON**, **JSON.parse()**, **JSON.stringify()**, **destructuring**, **spread operator**, **this**, **computed property**, **shorthand property**, **optional chaining**

## 🏗️ What You Will Build

- A contact book application with CRUD operations
- A student record system with nested data
- A JSON data processor

---

## Part 1: Creating & Accessing Objects (15 minutes)

### Object Literals

Objects store data as **key-value pairs**:

```javascript
// Creating an object
const person = {
	firstName: 'Alice',
	lastName: 'Johnson',
	age: 28,
	isStudent: false,
	hobbies: ['reading', 'coding', 'hiking'],
	address: {
		street: '123 Main St',
		city: 'Lagos',
		country: 'Nigeria',
	},
};
```

### Accessing Properties

```javascript
// Dot notation (preferred when key is known)
console.log(person.firstName); // "Alice"
console.log(person.age); // 28
console.log(person.address.city); // "Lagos"
console.log(person.hobbies[0]); // "reading"

// Bracket notation (required for dynamic keys or special characters)
console.log(person['firstName']); // "Alice"
console.log(person['last' + 'Name']); // "Johnson" (dynamic key)

const key = 'age';
console.log(person[key]); // 28 (variable as key)

// When you MUST use bracket notation:
const weird = {
	'full name': 'Alice Johnson', // space in key
	'2fast': true, // starts with number
	'background-color': '#ff0000', // hyphen in key
};
console.log(weird['full name']); // "Alice Johnson"
console.log(weird['background-color']); // "#ff0000"
```

### Modifying Objects

```javascript
const car = {
	make: 'Toyota',
	model: 'Camry',
	year: 2020,
};

// Update a property
car.year = 2024;

// Add a new property
car.color = 'blue';
car.mileage = 15000;

// Delete a property
delete car.mileage;

console.log(car); // { make: "Toyota", model: "Camry", year: 2024, color: "blue" }

// Check if a property exists
console.log('color' in car); // true
console.log('mileage' in car); // false
console.log(car.hasOwnProperty('make')); // true
```

### Optional Chaining (`?.`)

Safely access nested properties without errors:

```javascript
const user = {
	name: 'Alice',
	address: {
		city: 'Lagos',
	},
};

// Without optional chaining — crashes!
// console.log(user.profile.avatar); // ❌ TypeError: Cannot read properties of undefined

// With optional chaining — returns undefined safely
console.log(user.profile?.avatar); // undefined (no error!)
console.log(user.address?.city); // "Lagos"
console.log(user.address?.zipCode); // undefined
console.log(user.getProfile?.()); // undefined (safe method call)
```

<details>
<summary>💡 Knowledge Check #1</summary>

**Question:** When must you use bracket notation instead of dot notation?

**Answer:**
You must use bracket notation when:

1. The property name contains **spaces** or **special characters** (`"full name"`, `"background-color"`)
2. The property name **starts with a number** (`"2fast"`)
3. The property name is stored in a **variable** (`const key = "name"; obj[key]`)
4. The property name is **computed dynamically** (`obj["prop" + num]`)

</details>

---

## Part 2: Object Methods (10 minutes)

### Methods — Functions Inside Objects

```javascript
const calculator = {
	// Method shorthand (ES6)
	add(a, b) {
		return a + b;
	},

	subtract(a, b) {
		return a - b;
	},

	multiply(a, b) {
		return a * b;
	},
};

console.log(calculator.add(5, 3)); // 8
console.log(calculator.subtract(10, 4)); // 6
console.log(calculator.multiply(3, 7)); // 21
```

### The `this` Keyword

`this` refers to the object the method is called on:

```javascript
const student = {
	name: 'Bob',
	grades: [85, 92, 78, 95, 88],

	getAverage() {
		const sum = this.grades.reduce((total, g) => total + g, 0);
		return sum / this.grades.length;
	},

	getSummary() {
		return `${this.name}'s average: ${this.getAverage().toFixed(1)}`;
	},
};

console.log(student.getAverage()); // 87.6
console.log(student.getSummary()); // "Bob's average: 87.6"
```

> ⚠️ Arrow functions do NOT have their own `this`. When writing object methods that need `this`, use the shorthand syntax or regular functions.

```javascript
const timer = {
	seconds: 0,

	// ✅ Correct — regular method
	start() {
		console.log(`Timer at ${this.seconds}s`);
	},

	// ❌ Wrong — arrow function has no `this`
	startBroken: () => {
		console.log(`Timer at ${this.seconds}s`); // `this` is NOT the timer object!
	},
};
```

---

## Part 3: Iterating Over Objects (10 minutes)

### `for...in` Loop

```javascript
const scores = {
	math: 95,
	english: 88,
	science: 92,
	history: 85,
};

for (const subject in scores) {
	console.log(`${subject}: ${scores[subject]}`);
}
// math: 95
// english: 88
// science: 92
// history: 85
```

### `Object.keys()`, `Object.values()`, `Object.entries()`

```javascript
const product = {
	name: 'Laptop',
	price: 999,
	inStock: true,
};

// Get all keys as an array
console.log(Object.keys(product)); // ["name", "price", "inStock"]

// Get all values as an array
console.log(Object.values(product)); // ["Laptop", 999, true]

// Get key-value pairs as an array of arrays
console.log(Object.entries(product));
// [["name", "Laptop"], ["price", 999], ["inStock", true]]

// Use with array methods!
const priceList = {
	apple: 1.5,
	banana: 0.75,
	cherry: 3.0,
	date: 5.0,
};

// Find most expensive fruit
const mostExpensive = Object.entries(priceList).reduce((max, [fruit, price]) =>
	price > max[1] ? [fruit, price] : max,
);
console.log(`${mostExpensive[0]}: $${mostExpensive[1]}`); // "date: $5"

// Filter to affordable items
const affordable = Object.fromEntries(
	Object.entries(priceList).filter(([, price]) => price < 2),
);
console.log(affordable); // { apple: 1.5, banana: 0.75 }
```

<details>
<summary>💡 Knowledge Check #2</summary>

**Question:** What is the difference between `for...in` and `for...of`?

**Answer:**

- `for...in` — Iterates over **property keys** (strings) of an object. Works on objects and arrays (but not recommended for arrays).
- `for...of` — Iterates over **values** of an iterable (arrays, strings, Maps, Sets). Does NOT work on regular objects.

```javascript
const obj = { a: 1, b: 2 };
for (const key in obj) console.log(key); // "a", "b"

const arr = [10, 20, 30];
for (const val of arr) console.log(val); // 10, 20, 30
```

</details>

---

## Part 4: Destructuring & Spread (10 minutes)

### Object Destructuring

Extract properties into variables:

```javascript
const user = {
	name: 'Alice',
	email: 'alice@example.com',
	age: 25,
	role: 'admin',
};

// Basic destructuring
const { name, email, age } = user;
console.log(name); // "Alice"
console.log(email); // "alice@example.com"

// Rename variables
const { name: userName, role: userRole } = user;
console.log(userName); // "Alice"
console.log(userRole); // "admin"

// Default values
const { name: n, phone = 'N/A' } = user;
console.log(phone); // "N/A" (doesn't exist on user)

// Nested destructuring
const order = {
	id: 123,
	customer: {
		name: 'Bob',
		address: { city: 'Lagos', zip: '100001' },
	},
};

const {
	customer: {
		name: customerName,
		address: { city },
	},
} = order;
console.log(customerName); // "Bob"
console.log(city); // "Lagos"

// Rest pattern
const { name: n2, ...rest } = user;
console.log(rest); // { email: "alice@example.com", age: 25, role: "admin" }
```

### Destructuring in Function Parameters

```javascript
// Without destructuring
function greet(user) {
	return `Hello, ${user.name}! You are ${user.age}.`;
}

// With destructuring — cleaner!
function greet({ name, age }) {
	return `Hello, ${name}! You are ${age}.`;
}

const user = { name: 'Alice', age: 25, email: 'a@b.com' };
console.log(greet(user)); // "Hello, Alice! You are 25."
```

### Object Spread (`...`)

```javascript
// Copy an object
const original = { a: 1, b: 2 };
const copy = { ...original };

// Merge objects
const defaults = { theme: 'light', lang: 'en', fontSize: 14 };
const userPrefs = { theme: 'dark', fontSize: 18 };
const settings = { ...defaults, ...userPrefs }; // later values override
console.log(settings); // { theme: "dark", lang: "en", fontSize: 18 }

// Add/update properties immutably
const user = { name: 'Alice', age: 25 };
const updated = { ...user, age: 26, role: 'admin' };
console.log(updated); // { name: "Alice", age: 26, role: "admin" }
console.log(user); // { name: "Alice", age: 25 } (unchanged!)
```

### Shorthand Properties & Computed Keys

```javascript
// Shorthand — when variable name matches property name
const name = 'Alice';
const age = 25;

// Old way
const user1 = { name: name, age: age };
// Shorthand
const user2 = { name, age };
console.log(user2); // { name: "Alice", age: 25 }

// Computed property names
const field = 'email';
const obj = {
	[field]: 'alice@example.com',
	[`${field}Verified`]: true,
};
console.log(obj); // { email: "alice@example.com", emailVerified: true }
```

---

## Part 5: JSON — JavaScript Object Notation (10 minutes)

### What Is JSON?

JSON is a text format for storing and exchanging data. It looks like JavaScript objects but with stricter rules:

```json
{
	"name": "Alice",
	"age": 25,
	"isStudent": true,
	"courses": ["Math", "CS"],
	"address": {
		"city": "Lagos"
	}
}
```

### JSON Rules

- Keys MUST be double-quoted strings: `"name"` not `name`
- Strings MUST use double quotes: `"hello"` not `'hello'`
- No trailing commas
- No comments
- No `undefined`, functions, or `Date` objects

### Converting Between JSON and Objects

```javascript
// JavaScript Object → JSON String
const user = {
	name: 'Alice',
	age: 25,
	hobbies: ['reading', 'coding'],
};

const jsonString = JSON.stringify(user);
console.log(jsonString);
// '{"name":"Alice","age":25,"hobbies":["reading","coding"]}'
console.log(typeof jsonString); // "string"

// Pretty-print JSON
const pretty = JSON.stringify(user, null, 2);
console.log(pretty);
// {
//   "name": "Alice",
//   "age": 25,
//   "hobbies": [
//     "reading",
//     "coding"
//   ]
// }

// JSON String → JavaScript Object
const parsed = JSON.parse(jsonString);
console.log(parsed.name); // "Alice"
console.log(parsed.hobbies[0]); // "reading"
console.log(typeof parsed); // "object"
```

### Practical Use: Local Storage

```javascript
// Save data to localStorage
const settings = { theme: 'dark', fontSize: 16 };
localStorage.setItem('settings', JSON.stringify(settings));

// Load data from localStorage
const saved = localStorage.getItem('settings');
const loaded = saved ? JSON.parse(saved) : { theme: 'light', fontSize: 14 };
console.log(loaded.theme); // "dark"
```

### Deep Clone with JSON

```javascript
const original = {
	name: 'Alice',
	scores: [90, 85, 95],
	address: { city: 'Lagos' },
};

// Shallow copy — nested objects are still shared!
const shallow = { ...original };
shallow.scores.push(100);
console.log(original.scores); // [90, 85, 95, 100] ← Bug! Original modified!

// Deep clone with JSON
const deep = JSON.parse(JSON.stringify(original));
deep.scores.push(100);
console.log(original.scores); // [90, 85, 95] ← Original unchanged ✅

// Modern: structuredClone (built-in)
const deep2 = structuredClone(original);
```

<details>
<summary>💡 Knowledge Check #3</summary>

**Question:** What happens if you try to `JSON.stringify` a function or `undefined`?

**Answer:**

- **Functions** — Silently omitted from the output
- **`undefined`** — Silently omitted from objects, converted to `null` in arrays

```javascript
const obj = {
	name: 'Alice',
	greet: function () {
		return 'Hi';
	},
	value: undefined,
};

console.log(JSON.stringify(obj));
// '{"name":"Alice"}' — greet and value are gone!

const arr = [1, undefined, 3];
console.log(JSON.stringify(arr));
// '[1,null,3]' — undefined becomes null in arrays
```

</details>

---

## Part 6: Lab — Contact Book (20 minutes)

### Challenge: Build a Contact Book

Create `contact-book.js` with the following functionality:

**Starter Code:**

```javascript
const contacts = [];

// TODO 1: addContact(name, phone, email) — adds a contact object to the array
function addContact(name, phone, email) {
	// Create contact with id, name, phone, email, createdAt
}

// TODO 2: findContact(name) — finds a contact by name (case-insensitive)
function findContact(name) {
	// Return the contact or undefined
}

// TODO 3: updateContact(name, updates) — updates fields of an existing contact
function updateContact(name, updates) {
	// Find the contact and apply updates using spread
}

// TODO 4: deleteContact(name) — removes a contact by name
function deleteContact(name) {
	// Remove from array
}

// TODO 5: listContacts() — returns a formatted string of all contacts
function listContacts() {
	// Return formatted list
}

// TODO 6: exportContacts() — returns contacts as a JSON string
function exportContacts() {
	// Return pretty-printed JSON
}

// Test your contact book!
addContact('Alice Johnson', '555-0101', 'alice@example.com');
addContact('Bob Smith', '555-0202', 'bob@example.com');
addContact('Charlie Brown', '555-0303', 'charlie@example.com');

console.log(findContact('alice'));
updateContact('Bob Smith', { phone: '555-9999' });
console.log(listContacts());
deleteContact('Charlie Brown');
console.log(exportContacts());
```

<details>
<summary>✅ Solution</summary>

```javascript
const contacts = [];
let nextId = 1;

function addContact(name, phone, email) {
	const contact = {
		id: nextId++,
		name,
		phone,
		email,
		createdAt: new Date().toISOString(),
	};
	contacts.push(contact);
	console.log(`✅ Added: ${name}`);
	return contact;
}

function findContact(name) {
	return contacts.find((c) =>
		c.name.toLowerCase().includes(name.toLowerCase()),
	);
}

function updateContact(name, updates) {
	const index = contacts.findIndex(
		(c) => c.name.toLowerCase() === name.toLowerCase(),
	);
	if (index === -1) {
		console.log(`❌ Contact "${name}" not found.`);
		return null;
	}
	contacts[index] = { ...contacts[index], ...updates };
	console.log(`✅ Updated: ${name}`);
	return contacts[index];
}

function deleteContact(name) {
	const index = contacts.findIndex(
		(c) => c.name.toLowerCase() === name.toLowerCase(),
	);
	if (index === -1) {
		console.log(`❌ Contact "${name}" not found.`);
		return false;
	}
	const removed = contacts.splice(index, 1)[0];
	console.log(`🗑️ Deleted: ${removed.name}`);
	return true;
}

function listContacts() {
	if (contacts.length === 0) return 'No contacts found.';
	return contacts
		.map((c) => `[${c.id}] ${c.name} | 📞 ${c.phone} | 📧 ${c.email}`)
		.join('\n');
}

function exportContacts() {
	return JSON.stringify(contacts, null, 2);
}

// Test
addContact('Alice Johnson', '555-0101', 'alice@example.com');
addContact('Bob Smith', '555-0202', 'bob@example.com');
addContact('Charlie Brown', '555-0303', 'charlie@example.com');

console.log('\n--- Find ---');
console.log(findContact('alice'));

console.log('\n--- Update ---');
updateContact('Bob Smith', { phone: '555-9999' });

console.log('\n--- List ---');
console.log(listContacts());

console.log('\n--- Delete ---');
deleteContact('Charlie Brown');

console.log('\n--- Export ---');
console.log(exportContacts());
```

</details>

---

## ⚠️ Common Mistakes

| Mistake                                | Problem                                        | Fix                                               |
| -------------------------------------- | ---------------------------------------------- | ------------------------------------------------- |
| Mutating objects unintentionally       | Changing shared references                     | Use `{ ...obj }` or `structuredClone()`           |
| Arrow functions with `this`            | `this` doesn't bind to the object              | Use regular method syntax                         |
| `JSON.parse()` on invalid JSON         | Throws `SyntaxError`                           | Wrap in try/catch                                 |
| Confusing `for...in` and `for...of`    | `for...in` gives keys, `for...of` gives values | Use `for...in` for objects, `for...of` for arrays |
| Forgetting JSON requires double quotes | `{name: "Alice"}` is NOT valid JSON            | Keys must be `"name"`                             |

---

## 📝 Session Summary

In this session, you learned:

1. **Object literals** — Key-value pairs, nested objects
2. **Property access** — Dot vs bracket notation, optional chaining (`?.`)
3. **Object methods** — Functions inside objects, `this` keyword
4. **Iteration** — `for...in`, `Object.keys/values/entries`
5. **Destructuring** — Extract properties, rename, defaults, rest pattern
6. **Spread operator** — Copy, merge, immutable updates
7. **JSON** — `stringify`, `parse`, deep clone, localStorage

---

## 🏠 Homework

### Task 1: Inventory System

Create an inventory with products (name, price, quantity, category). Implement:

- `addProduct()`, `removeProduct()`, `updateStock()`
- `getByCategory(category)` — filter by category
- `getTotal()` — total value of all inventory

### Task 2: Student Report Card

Given student data (name, subjects with grades), write functions to:

- Calculate average grade per student
- Find the best student overall
- Generate a formatted report card string

### Task 3: JSON Config Manager

Build a config manager that:

- Loads settings from a JSON string
- Allows getting/setting nested values by dot-path (e.g., `"display.theme"`)
- Exports the config back to JSON

### Bonus Challenge: Object Diff

Write a `diff(objA, objB)` function that returns the differences between two objects:

```javascript
diff({ a: 1, b: 2, c: 3 }, { a: 1, b: 5, d: 4 });
// { changed: { b: { from: 2, to: 5 } }, added: { d: 4 }, removed: { c: 3 } }
```

---

## 📚 Resources

- [MDN: Working with Objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_objects)
- [MDN: JSON](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON)
- [MDN: Destructuring Assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
- [MDN: Optional Chaining](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)
- [JavaScript.info: Objects](https://javascript.info/object)
- [JavaScript.info: Object Methods, "this"](https://javascript.info/object-methods)
- [JavaScript.info: JSON Methods](https://javascript.info/json)

---

**Next:** [Session 25 — DOM Fundamentals & Selection](../week-09/session-25.md) →
