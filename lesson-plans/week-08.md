# Week 08 — JavaScript Fundamentals II: Functions, Arrays & Objects

> _"Writing reusable code and working with collections of data."_

This week deepens your JavaScript skills by introducing functions for code reuse, arrays for ordered collections, and objects for structured data. These are the core building blocks you will use in every JavaScript project.

---

## Overview

-   **Focus:** Functions, scope, arrays, array methods, objects, destructuring, and JSON
-   **Prerequisites:** Week 07 (variables, data types, operators, control flow)
-   **Outcomes by end of week:**
    -   Write reusable functions using declarations, expressions, and arrow syntax
    -   Understand scope (global, function, block) and variable hoisting
    -   Create and manipulate arrays with built-in methods
    -   Iterate over arrays using loops and higher-order methods
    -   Create objects, access properties, and use methods
    -   Work with destructuring, spread/rest operators
    -   Parse and stringify JSON data

---

## Sessions

### Session 22 — Functions & Scope (90 min)

**Learning Objectives:**
-   Define functions using declarations, expressions, and arrow syntax
-   Use parameters, default parameters, and return values
-   Understand scope (global, local, block) and the scope chain
-   Explain hoisting behavior for functions and variables
-   Write pure functions and understand side effects

**Topics Covered:**

| Topic | Duration | Details |
|-------|----------|---------|
| Function Declarations | 15 min | Syntax, naming, calling functions, `return` keyword, functions without return (undefined) |
| Function Expressions & Arrow Functions | 15 min | Anonymous functions, `const fn = function() {}`, arrow syntax `() => {}`, implicit return, when to use each |
| Parameters & Arguments | 10 min | Positional params, default values, rest parameters `...args`, `arguments` object (legacy) |
| Return Values | 10 min | Single return, returning objects/arrays, early return pattern, multiple values via objects |
| Scope & Scope Chain | 20 min | Global scope, function scope, block scope, lexical scoping, scope chain lookup, closures preview |
| Hoisting | 10 min | Function declaration hoisting, `var` hoisting vs `let`/`const` TDZ, best practices to avoid issues |
| Lab: Function Toolkit | 10 min | Write utility functions: `calculateArea()`, `isEven()`, `capitalize()`, `getMax()` |

**Key Code Examples:**

```javascript
// Function declaration (hoisted)
function greet(name) {
  return `Hello, ${name}!`;
}

// Function expression (not hoisted)
const square = function(n) {
  return n * n;
};

// Arrow function (concise)
const double = (n) => n * 2;
const add = (a, b) => a + b;

// Default parameters
function createUser(name, role = "student") {
  return { name, role };
}
console.log(createUser("Alice"));         // { name: "Alice", role: "student" }
console.log(createUser("Bob", "admin"));  // { name: "Bob", role: "admin" }

// Rest parameters
function sum(...numbers) {
  let total = 0;
  for (const num of numbers) {
    total += num;
  }
  return total;
}
console.log(sum(1, 2, 3, 4, 5)); // 15

// Scope demonstration
let globalVar = "I'm global";

function outer() {
  let outerVar = "I'm in outer";
  
  function inner() {
    let innerVar = "I'm in inner";
    console.log(globalVar);  // ✅ accessible
    console.log(outerVar);   // ✅ accessible (scope chain)
    console.log(innerVar);   // ✅ accessible
  }
  
  inner();
  // console.log(innerVar); // ❌ ReferenceError
}

// Early return pattern
function getDiscount(age) {
  if (age < 0) return "Invalid age";
  if (age < 12) return 0.5;  // 50% discount
  if (age >= 65) return 0.3; // 30% discount
  return 0;                   // no discount
}
```

**Homework:**
-   Write a `calculateBMI(weight, height)` function that returns BMI and a category string
-   Create a `fizzBuzz(n)` function that returns the FizzBuzz result for any number
-   Build a `passwordStrength(password)` function that rates passwords as weak/medium/strong
-   Challenge: Write a `compose(f, g)` function that returns a new function applying `g` then `f`

---

### Session 23 — Arrays & Iteration (90 min)

**Learning Objectives:**
-   Create arrays and access elements by index
-   Use mutating methods: `push()`, `pop()`, `shift()`, `unshift()`, `splice()`
-   Use non-mutating methods: `slice()`, `concat()`, `includes()`, `indexOf()`
-   Iterate with `for`, `for...of`, `forEach()`
-   Transform data with `map()`, `filter()`, `find()`, `reduce()`

**Topics Covered:**

| Topic | Duration | Details |
|-------|----------|---------|
| Creating & Accessing Arrays | 10 min | Array literal `[]`, `new Array()`, zero-based indexing, `.length`, nested arrays |
| Mutating Methods | 15 min | `push()`, `pop()`, `shift()`, `unshift()`, `splice(index, deleteCount, ...items)`, `reverse()`, `sort()` |
| Non-Mutating Methods | 10 min | `slice(start, end)`, `concat()`, `includes()`, `indexOf()`, `join()`, spread to copy `[...arr]` |
| Loops for Arrays | 10 min | Classic `for` loop, `for...of` loop, `for...in` (and why to avoid it for arrays) |
| forEach() | 5 min | Syntax, callback parameters (element, index, array), no return value |
| map() & filter() | 15 min | Transforming arrays with `map()`, filtering with `filter()`, chaining methods |
| find(), findIndex() & reduce() | 15 min | Finding elements, accumulating values, practical `reduce()` examples (sum, grouping, flattening) |
| Lab: Array Challenges | 10 min | Filter even numbers, find max value, count word occurrences, flatten nested array |

**Key Code Examples:**

```javascript
// Creating and modifying arrays
const fruits = ["apple", "banana", "cherry"];
fruits.push("date");           // ["apple", "banana", "cherry", "date"]
fruits.pop();                  // ["apple", "banana", "cherry"]
fruits.splice(1, 1, "blueberry"); // ["apple", "blueberry", "cherry"]

// Copying arrays (never mutate the original when unnecessary)
const copy = [...fruits];          // spread operator
const slice = fruits.slice();      // slice without args

// Iterating
for (const fruit of fruits) {
  console.log(fruit);
}

fruits.forEach((fruit, index) => {
  console.log(`${index + 1}. ${fruit}`);
});

// Transforming with map
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(n => n * 2);        // [2, 4, 6, 8, 10]
const squared = numbers.map(n => n ** 2);       // [1, 4, 9, 16, 25]

// Filtering
const evens = numbers.filter(n => n % 2 === 0); // [2, 4]
const big = numbers.filter(n => n > 3);         // [4, 5]

// Finding
const found = numbers.find(n => n > 3);         // 4 (first match)
const index = numbers.findIndex(n => n > 3);    // 3

// Reducing
const total = numbers.reduce((sum, n) => sum + n, 0); // 15

// Chaining methods
const students = [
  { name: "Alice", grade: 92 },
  { name: "Bob", grade: 78 },
  { name: "Charlie", grade: 85 },
  { name: "Diana", grade: 95 },
];

const honors = students
  .filter(s => s.grade >= 90)
  .map(s => s.name);
// ["Alice", "Diana"]

// Sort (mutates — copy first if needed)
const sorted = [...students].sort((a, b) => b.grade - a.grade);
```

**Homework:**
-   Given an array of prices, use `filter()` to get items under $20, then `map()` to apply a 10% discount
-   Use `reduce()` to calculate a shopping cart total
-   Write a function `removeDuplicates(arr)` that returns a new array without duplicates
-   Challenge: Implement your own `myMap()` function that works like the built-in `.map()`

---

### Session 24 — Objects & JSON (90 min)

**Learning Objectives:**
-   Create objects using literal syntax and access properties
-   Add methods to objects and understand `this` keyword basics
-   Use destructuring to extract values from objects and arrays
-   Apply spread/rest operators with objects
-   Work with `Object.keys()`, `Object.values()`, `Object.entries()`
-   Parse JSON strings and stringify objects

**Topics Covered:**

| Topic | Duration | Details |
|-------|----------|---------|
| Object Literals | 15 min | Creating objects, properties (key-value pairs), dot notation, bracket notation, computed property names |
| Object Methods & `this` | 10 min | Functions as values, `this` keyword in methods, method shorthand syntax |
| Destructuring | 15 min | Object destructuring, array destructuring, renaming, default values, nested destructuring, function parameter destructuring |
| Spread & Rest with Objects | 10 min | Copying objects `{...obj}`, merging objects, rest in destructuring, shallow vs deep copy |
| Object Utility Methods | 10 min | `Object.keys()`, `Object.values()`, `Object.entries()`, `Object.assign()`, `Object.freeze()` |
| JSON | 15 min | What is JSON, `JSON.stringify()`, `JSON.parse()`, JSON vs JS objects, storing data as JSON, fetching JSON (preview) |
| Lab: Student Records | 15 min | Build a student record system: create, update, list, filter, and export to JSON |

**Key Code Examples:**

```javascript
// Object creation
const student = {
  firstName: "Alice",
  lastName: "Johnson",
  age: 20,
  grades: [92, 88, 95, 91],
  isActive: true,
  
  // Method
  getFullName() {
    return `${this.firstName} ${this.lastName}`;
  },
  
  getAverage() {
    const sum = this.grades.reduce((a, b) => a + b, 0);
    return (sum / this.grades.length).toFixed(1);
  }
};

console.log(student.getFullName());  // "Alice Johnson"
console.log(student.getAverage());    // "91.5"

// Destructuring objects
const { firstName, lastName, age } = student;
console.log(`${firstName} is ${age}`); // "Alice is 20"

// Renaming during destructuring
const { firstName: fName, lastName: lName } = student;

// Destructuring with defaults
const { nickname = "N/A" } = student;

// Array destructuring
const [first, second, ...rest] = student.grades;
console.log(first);  // 92
console.log(rest);   // [95, 91]

// Spread operator for objects
const updatedStudent = { 
  ...student, 
  age: 21, 
  email: "alice@example.com" 
};

// Object utility methods
const keys = Object.keys(student);      // ["firstName", "lastName", ...]
const values = Object.values(student);   // ["Alice", "Johnson", ...]
const entries = Object.entries(student); // [["firstName", "Alice"], ...]

// Iterating over object entries
for (const [key, value] of Object.entries(student)) {
  console.log(`${key}: ${value}`);
}

// JSON
const jsonString = JSON.stringify(student, null, 2);
console.log(jsonString); // Pretty-printed JSON

const parsed = JSON.parse(jsonString);
console.log(parsed.firstName); // "Alice"

// Practical example: array of objects
const classroom = [
  { name: "Alice", grade: 92 },
  { name: "Bob", grade: 78 },
  { name: "Charlie", grade: 85 },
];

// Find top student
const topStudent = classroom.reduce((top, s) => 
  s.grade > top.grade ? s : top
);
console.log(`Top student: ${topStudent.name} (${topStudent.grade})`);
```

**Homework:**
-   Create a `library` array of book objects (title, author, year, isRead) with at least 5 books
-   Write functions: `getUnreadBooks()`, `getBooksByAuthor(author)`, `getNewestBook()`
-   Use `JSON.stringify()` to "save" the library and `JSON.parse()` to "load" it
-   Challenge: Build a simple contact book that stores contacts in an array of objects, with add, remove, search, and list-all functions

---

## Week 08 Summary

By the end of this week, students can:

| Skill | Status |
|-------|--------|
| Write functions (declaration, expression, arrow) | ✅ |
| Use parameters, defaults, and rest params | ✅ |
| Understand scope (global, function, block) | ✅ |
| Create and manipulate arrays | ✅ |
| Use higher-order methods (map, filter, reduce) | ✅ |
| Chain array methods for data transformations | ✅ |
| Create objects with properties and methods | ✅ |
| Use destructuring and spread/rest operators | ✅ |
| Work with JSON (stringify, parse) | ✅ |

## Resources

-   [MDN: Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions)
-   [MDN: Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
-   [MDN: Working with Objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_objects)
-   [MDN: Destructuring Assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
-   [JavaScript.info: Data Types](https://javascript.info/data-types)
-   [JSON.org](https://www.json.org/)
