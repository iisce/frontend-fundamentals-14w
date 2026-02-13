# Week 08 — Session 23: Arrays & Iteration

**Navigation:**
← [Session 22](session-22.md) | [Week 08 Index](../week-08.md) | [Session 24](session-24.md) →

---

**Session Length:** 90 minutes

## 📋 Pre-Class Checklist

Before starting this session, make sure you have:

- ✅ Completed Session 22 (Functions & Scope)
- ✅ Understand function declarations, expressions, and arrow functions
- ✅ Comfortable with parameters, return values, and scope
- ✅ Create a new file: `arrays.js`

## 🎯 Learning Objectives

By the end of this session, you will be able to:

- Create and access arrays using index notation
- Add, remove, and modify array elements
- Iterate over arrays with `for`, `for...of`, and `forEach`
- Use essential array methods: `map`, `filter`, `find`, `reduce`
- Chain array methods for data transformations
- Apply spread operator and destructuring with arrays

## 📦 Files for This Session

- `session-23.md` — This tutorial (you're reading it!)
- Create: `arrays.js`, `student-grades.js`

## 🔑 Key Terms

**array**, **index**, **element**, **length**, **push**, **pop**, **shift**, **unshift**, **splice**, **slice**, **for loop**, **for...of**, **forEach**, **map**, **filter**, **find**, **findIndex**, **reduce**, **some**, **every**, **includes**, **spread operator**, **destructuring**

## 🏗️ What You Will Build

- A student grade management system
- A data processing pipeline with chained array methods
- A shopping list manager

---

## Part 1: Creating & Accessing Arrays (10 minutes)

### What Is an Array?

An ordered collection of values (elements), accessed by index (starting at 0):

```javascript
// Creating arrays
const fruits = ['apple', 'banana', 'cherry', 'date'];
const numbers = [10, 20, 30, 40, 50];
const mixed = ['hello', 42, true, null, [1, 2, 3]];
const empty = [];

// Accessing elements by index (0-based!)
console.log(fruits[0]); // "apple"   (first element)
console.log(fruits[1]); // "banana"  (second element)
console.log(fruits[3]); // "date"    (fourth element)
console.log(fruits[-1]); // undefined (no negative indexing in JS)

// Length property
console.log(fruits.length); // 4

// Last element
console.log(fruits[fruits.length - 1]); // "date"

// Check if something is an array
console.log(Array.isArray(fruits)); // true
console.log(Array.isArray('hello')); // false
```

### Modifying Elements

```javascript
const colors = ['red', 'green', 'blue'];

// Change an element
colors[1] = 'yellow';
console.log(colors); // ["red", "yellow", "blue"]

// Add at a specific index (can create gaps!)
colors[5] = 'purple';
console.log(colors); // ["red", "yellow", "blue", empty × 2, "purple"]
console.log(colors.length); // 6
```

> ⚠️ Avoid creating "sparse" arrays with gaps. Use `push()` to add elements instead.

<details>
<summary>💡 Knowledge Check #1</summary>

**Question:** Given `const items = ["a", "b", "c", "d", "e"]`, what does `items[items.length - 1]` return?

**Answer:**
`"e"` — `items.length` is 5, so `items[5 - 1]` = `items[4]` = `"e"` (the last element).

</details>

---

## Part 2: Adding & Removing Elements (10 minutes)

### End of Array: `push()` and `pop()`

```javascript
const stack = ['a', 'b', 'c'];

// push — add to END
stack.push('d');
console.log(stack); // ["a", "b", "c", "d"]

stack.push('e', 'f'); // add multiple
console.log(stack); // ["a", "b", "c", "d", "e", "f"]

// pop — remove from END (returns the removed element)
const last = stack.pop();
console.log(last); // "f"
console.log(stack); // ["a", "b", "c", "d", "e"]
```

### Beginning of Array: `unshift()` and `shift()`

```javascript
const queue = ['b', 'c', 'd'];

// unshift — add to BEGINNING
queue.unshift('a');
console.log(queue); // ["a", "b", "c", "d"]

// shift — remove from BEGINNING (returns the removed element)
const first = queue.shift();
console.log(first); // "a"
console.log(queue); // ["b", "c", "d"]
```

### Middle of Array: `splice()`

```javascript
const arr = ['a', 'b', 'c', 'd', 'e'];

// splice(startIndex, deleteCount, ...itemsToAdd)

// Delete 2 elements starting at index 1
const removed = arr.splice(1, 2);
console.log(removed); // ["b", "c"]
console.log(arr); // ["a", "d", "e"]

// Insert without deleting (deleteCount = 0)
arr.splice(1, 0, 'x', 'y');
console.log(arr); // ["a", "x", "y", "d", "e"]

// Replace: delete 1 and insert 1
arr.splice(2, 1, 'z');
console.log(arr); // ["a", "x", "z", "d", "e"]
```

### Non-Destructive: `slice()` and `concat()`

```javascript
const original = [1, 2, 3, 4, 5];

// slice — returns a COPY of a portion (does NOT modify original)
const portion = original.slice(1, 4); // from index 1 to 3 (end exclusive)
console.log(portion); // [2, 3, 4]
console.log(original); // [1, 2, 3, 4, 5] (unchanged!)

// concat — merges arrays (returns new array)
const a = [1, 2];
const b = [3, 4];
const c = a.concat(b, [5, 6]);
console.log(c); // [1, 2, 3, 4, 5, 6]
console.log(a); // [1, 2] (unchanged!)
```

### Quick Reference

| Method                   | Action                | Modifies Original? | Returns          |
| ------------------------ | --------------------- | ------------------ | ---------------- |
| `push(item)`             | Add to end            | ✅ Yes             | New length       |
| `pop()`                  | Remove from end       | ✅ Yes             | Removed element  |
| `unshift(item)`          | Add to beginning      | ✅ Yes             | New length       |
| `shift()`                | Remove from beginning | ✅ Yes             | Removed element  |
| `splice(i, n, ...items)` | Add/remove at index   | ✅ Yes             | Removed elements |
| `slice(start, end)`      | Copy portion          | ❌ No              | New array        |
| `concat(arr)`            | Merge arrays          | ❌ No              | New array        |

---

## Part 3: Iterating Over Arrays (15 minutes)

### Classic `for` Loop

```javascript
const fruits = ['apple', 'banana', 'cherry', 'date'];

for (let i = 0; i < fruits.length; i++) {
	console.log(`${i}: ${fruits[i]}`);
}
// 0: apple
// 1: banana
// 2: cherry
// 3: date
```

### `for...of` Loop (Cleaner!)

```javascript
const fruits = ['apple', 'banana', 'cherry', 'date'];

for (const fruit of fruits) {
	console.log(fruit);
}
// apple
// banana
// cherry
// date

// Need the index too? Use entries()
for (const [index, fruit] of fruits.entries()) {
	console.log(`${index}: ${fruit}`);
}
```

### `forEach` Method

```javascript
const fruits = ['apple', 'banana', 'cherry', 'date'];

fruits.forEach(function (fruit, index) {
	console.log(`${index}: ${fruit}`);
});

// With arrow function
fruits.forEach((fruit, index) => {
	console.log(`${index}: ${fruit}`);
});
```

### When to Use Which?

| Loop       | Best For                                      | Can `break`? |
| ---------- | --------------------------------------------- | ------------ |
| `for`      | Need index, complex logic, `break`/`continue` | ✅ Yes       |
| `for...of` | Simple iteration, readable code               | ✅ Yes       |
| `forEach`  | Running a function on each element            | ❌ No        |

<details>
<summary>💡 Knowledge Check #2</summary>

**Question:** What's wrong with this code?

```javascript
const names = ["Alice", "Bob", "Charlie"];
names.forEach(name => {
  if (name === "Bob") break;
  console.log(name);
});
```

**Answer:**
You can't use `break` inside `forEach`. It will throw a SyntaxError. Use a regular `for` loop or `for...of` if you need to break early:

```javascript
for (const name of names) {
	if (name === 'Bob') break;
	console.log(name);
}
```

</details>

---

## Part 4: Transforming Arrays — `map`, `filter`, `find` (15 minutes)

### `map()` — Transform Every Element

Creates a **new array** by applying a function to each element:

```javascript
const numbers = [1, 2, 3, 4, 5];

// Double every number
const doubled = numbers.map((n) => n * 2);
console.log(doubled); // [2, 4, 6, 8, 10]
console.log(numbers); // [1, 2, 3, 4, 5] (unchanged!)

// Convert to strings
const strings = numbers.map((n) => `Item ${n}`);
console.log(strings); // ["Item 1", "Item 2", ...]

// Extract a property from objects
const users = [
	{ name: 'Alice', age: 25 },
	{ name: 'Bob', age: 30 },
	{ name: 'Charlie', age: 35 },
];
const names = users.map((user) => user.name);
console.log(names); // ["Alice", "Bob", "Charlie"]
```

### `filter()` — Keep Elements That Pass a Test

Creates a **new array** with only elements where the callback returns `true`:

```javascript
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

const evens = numbers.filter((n) => n % 2 === 0);
console.log(evens); // [2, 4, 6, 8, 10]

const bigNumbers = numbers.filter((n) => n > 5);
console.log(bigNumbers); // [6, 7, 8, 9, 10]

// Filter objects
const users = [
	{ name: 'Alice', age: 17 },
	{ name: 'Bob', age: 25 },
	{ name: 'Charlie', age: 15 },
	{ name: 'Diana', age: 30 },
];
const adults = users.filter((user) => user.age >= 18);
console.log(adults); // [{ name: "Bob", ... }, { name: "Diana", ... }]
```

### `find()` — Get the First Match

Returns the **first element** that passes the test (or `undefined`):

```javascript
const numbers = [10, 20, 30, 40, 50];

const found = numbers.find((n) => n > 25);
console.log(found); // 30 (first match, not all matches)

const notFound = numbers.find((n) => n > 100);
console.log(notFound); // undefined

// findIndex — returns the INDEX of the first match
const index = numbers.findIndex((n) => n > 25);
console.log(index); // 2

// includes — check if value exists
console.log(numbers.includes(30)); // true
console.log(numbers.includes(35)); // false
```

### Chaining Methods

The real power comes from combining these methods:

```javascript
const products = [
	{ name: 'Laptop', price: 999, inStock: true },
	{ name: 'Phone', price: 699, inStock: false },
	{ name: 'Tablet', price: 499, inStock: true },
	{ name: 'Watch', price: 299, inStock: true },
	{ name: 'Headphones', price: 149, inStock: false },
];

// Get names of affordable in-stock products
const affordable = products
	.filter((p) => p.inStock) // keep only in-stock
	.filter((p) => p.price < 500) // keep only under $500
	.map((p) => p.name) // extract names
	.sort(); // sort alphabetically

console.log(affordable); // ["Tablet", "Watch"]
```

<details>
<summary>💡 Knowledge Check #3</summary>

**Question:** What is the difference between `map()`, `filter()`, and `find()`?

**Answer:**
| Method | Returns | Purpose |
|--------|---------|---------|
| `map()` | New array (same length) | Transform every element |
| `filter()` | New array (same or shorter) | Keep elements that pass a test |
| `find()` | Single element or `undefined` | Get the first match |

All three are **non-destructive** — they don't modify the original array.

</details>

---

## Part 5: `reduce()` — The Swiss Army Knife (10 minutes)

`reduce()` processes an array into a **single value**:

```javascript
// Syntax: array.reduce((accumulator, currentValue) => newAccumulator, initialValue)

const numbers = [1, 2, 3, 4, 5];

// Sum all numbers
const sum = numbers.reduce((total, n) => total + n, 0);
console.log(sum); // 15

// How it works step by step:
// Step 1: total = 0,  n = 1 → 0 + 1 = 1
// Step 2: total = 1,  n = 2 → 1 + 2 = 3
// Step 3: total = 3,  n = 3 → 3 + 3 = 6
// Step 4: total = 6,  n = 4 → 6 + 4 = 10
// Step 5: total = 10, n = 5 → 10 + 5 = 15

// Find the maximum
const max = numbers.reduce(
	(biggest, n) => (n > biggest ? n : biggest),
	numbers[0],
);
console.log(max); // 5

// Count occurrences
const fruits = ['apple', 'banana', 'apple', 'cherry', 'banana', 'apple'];
const counts = fruits.reduce((acc, fruit) => {
	acc[fruit] = (acc[fruit] || 0) + 1;
	return acc;
}, {});
console.log(counts); // { apple: 3, banana: 2, cherry: 1 }

// Group by property
const people = [
	{ name: 'Alice', dept: 'Engineering' },
	{ name: 'Bob', dept: 'Marketing' },
	{ name: 'Charlie', dept: 'Engineering' },
	{ name: 'Diana', dept: 'Marketing' },
];

const byDept = people.reduce((groups, person) => {
	const dept = person.dept;
	groups[dept] = groups[dept] || [];
	groups[dept].push(person.name);
	return groups;
}, {});
console.log(byDept);
// { Engineering: ["Alice", "Charlie"], Marketing: ["Bob", "Diana"] }
```

> 💡 **Tip:** `reduce` is powerful but can be hard to read. For simple operations (sum, max, min), use `reduce`. For complex transformations, consider using `map`/`filter` chains instead.

---

## Part 6: Spread & Destructuring (5 minutes)

### Spread Operator (`...`)

```javascript
// Copy an array
const original = [1, 2, 3];
const copy = [...original];
copy.push(4);
console.log(original); // [1, 2, 3] (unchanged!)
console.log(copy); // [1, 2, 3, 4]

// Merge arrays
const a = [1, 2];
const b = [3, 4];
const merged = [...a, ...b, 5, 6];
console.log(merged); // [1, 2, 3, 4, 5, 6]
```

### Array Destructuring

```javascript
const colors = ['red', 'green', 'blue', 'yellow'];

// Extract into variables
const [first, second, third] = colors;
console.log(first); // "red"
console.log(second); // "green"
console.log(third); // "blue"

// Skip elements
const [, , thirdColor] = colors;
console.log(thirdColor); // "blue"

// Rest pattern
const [head, ...rest] = colors;
console.log(head); // "red"
console.log(rest); // ["green", "blue", "yellow"]

// Swap variables
let x = 1,
	y = 2;
[x, y] = [y, x];
console.log(x, y); // 2, 1
```

---

## Part 7: Lab — Student Grade Manager (15 minutes)

### Challenge

Create `student-grades.js` that processes a student grade dataset:

**Starter Code:**

```javascript
const students = [
	{ name: 'Alice', grade: 92 },
	{ name: 'Bob', grade: 78 },
	{ name: 'Charlie', grade: 85 },
	{ name: 'Diana', grade: 95 },
	{ name: 'Eve', grade: 63 },
	{ name: 'Frank', grade: 88 },
	{ name: 'Grace', grade: 45 },
	{ name: 'Hank', grade: 71 },
];

// TODO 1: Get an array of just the student names
// Expected: ["Alice", "Bob", "Charlie", ...]

// TODO 2: Find all students with grade >= 80 (honor roll)
// Expected: [{ name: "Alice", ... }, { name: "Charlie", ... }, ...]

// TODO 3: Calculate the class average grade
// Expected: 77.125

// TODO 4: Find the student with the highest grade
// Expected: { name: "Diana", grade: 95 }

// TODO 5: Add a "status" property (pass/fail, threshold = 60)
// Expected: [{ name: "Alice", grade: 92, status: "pass" }, ...]

// TODO 6: Sort students by grade (highest first)
// Expected: [{ name: "Diana", ... }, { name: "Alice", ... }, ...]
```

<details>
<summary>✅ Solution</summary>

```javascript
const students = [
	{ name: 'Alice', grade: 92 },
	{ name: 'Bob', grade: 78 },
	{ name: 'Charlie', grade: 85 },
	{ name: 'Diana', grade: 95 },
	{ name: 'Eve', grade: 63 },
	{ name: 'Frank', grade: 88 },
	{ name: 'Grace', grade: 45 },
	{ name: 'Hank', grade: 71 },
];

// 1. Get names
const names = students.map((s) => s.name);
console.log('Names:', names);

// 2. Honor roll (grade >= 80)
const honorRoll = students.filter((s) => s.grade >= 80);
console.log('Honor Roll:', honorRoll);

// 3. Class average
const average = students.reduce((sum, s) => sum + s.grade, 0) / students.length;
console.log('Average:', average);

// 4. Highest grade
const topStudent = students.reduce((best, s) =>
	s.grade > best.grade ? s : best,
);
console.log('Top Student:', topStudent);

// 5. Add pass/fail status
const withStatus = students.map((s) => ({
	...s,
	status: s.grade >= 60 ? 'pass' : 'fail',
}));
console.log('With Status:', withStatus);

// 6. Sort by grade (highest first) — using spread to avoid mutating original
const sorted = [...students].sort((a, b) => b.grade - a.grade);
console.log('Sorted:', sorted);
```

</details>

---

## ⚠️ Common Mistakes

| Mistake                             | Problem                         | Fix                                        |
| ----------------------------------- | ------------------------------- | ------------------------------------------ |
| Forgetting arrays are 0-indexed     | `arr[1]` is the second element  | First element is `arr[0]`                  |
| `sort()` without compare function   | Sorts as strings: `[1, 10, 2]`  | Use `sort((a, b) => a - b)` for numbers    |
| Mutating when you shouldn't         | `splice()` changes the original | Use `slice()`, `map()`, `filter()` instead |
| Forgetting `return` in `reduce`     | Accumulator becomes `undefined` | Always return the accumulator              |
| Using `map` when you mean `forEach` | Creates an unused array         | Use `forEach` for side effects only        |

---

## 📝 Session Summary

In this session, you learned:

1. **Array basics** — Creating, accessing (0-indexed), modifying
2. **Mutating methods** — `push`, `pop`, `shift`, `unshift`, `splice`
3. **Non-mutating methods** — `slice`, `concat`, spread `[...]`
4. **Iteration** — `for`, `for...of`, `forEach`
5. **Transformation** — `map`, `filter`, `find`, `findIndex`, `includes`
6. **Aggregation** — `reduce` for sums, counts, grouping
7. **Modern syntax** — Spread operator, array destructuring

---

## 🏠 Homework

### Task 1: Shopping List Manager

Create a shopping list program that supports:

- Adding items (with quantity and price)
- Removing items by name
- Displaying the list with totals
- Finding the most expensive item

### Task 2: Data Pipeline

Given an array of numbers `[3, 7, 2, 9, 1, 5, 8, 4, 6, 10]`:

- Filter out odd numbers
- Double the remaining numbers
- Sort in descending order
- Calculate the sum
- Do it all in a single chain

### Task 3: Word Frequency Counter

Write a function that takes a sentence string and returns an object with word frequencies (case-insensitive):

```javascript
wordFrequency('The cat sat on the mat the cat');
// { the: 3, cat: 2, sat: 1, on: 1, mat: 1 }
```

### Bonus Challenge: Flatten & Deduplicate

Write a function that takes a nested array and returns a flat, unique, sorted array:

```javascript
flatUnique([
	[3, 1],
	[2, 3],
	[1, 4, 2],
]);
// [1, 2, 3, 4]
```

---

## 📚 Resources

- [MDN: Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
- [MDN: Array.prototype.map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
- [MDN: Array.prototype.filter()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
- [MDN: Array.prototype.reduce()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)
- [JavaScript.info: Arrays](https://javascript.info/array)
- [JavaScript.info: Array Methods](https://javascript.info/array-methods)

---

**Next:** [Session 24 — Objects & JSON](session-24.md) →
