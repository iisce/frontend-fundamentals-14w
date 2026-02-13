# Week 10 — ES6+, Async JavaScript & Mini Project 2

> _"Modern JavaScript and fetching data from the web."_

This capstone week for the JavaScript phase introduces modern ES6+ syntax, asynchronous programming with Promises and async/await, the Fetch API for working with web APIs, and culminates in building a complete interactive application that combines everything learned in Weeks 07–09.

---

## Overview

-   **Focus:** Modern ES6+ features, asynchronous JavaScript, Fetch API, and building a complete interactive app
-   **Prerequisites:** Weeks 07–09 (variables, functions, arrays, objects, DOM, events)
-   **Outcomes by end of week:**
    -   Use modern ES6+ syntax confidently (arrow functions, destructuring, modules, spread/rest)
    -   Understand synchronous vs asynchronous execution
    -   Work with Promises and async/await
    -   Fetch data from public APIs and display it dynamically
    -   Handle errors gracefully in async code
    -   Build and present a complete interactive JavaScript application

---

## Sessions

### Session 28 — Modern ES6+ Features (90 min)

**Learning Objectives:**
-   Use arrow functions in all their forms (concise body, block body, implicit return)
-   Apply destructuring in practical scenarios (function params, API responses)
-   Use spread/rest operators for arrays and objects effectively
-   Understand JavaScript modules (`import`/`export`)
-   Apply shorthand property and method syntax
-   Use optional chaining (`?.`) and nullish coalescing (`??`)

**Topics Covered:**

| Topic | Duration | Details |
|-------|----------|---------|
| Arrow Functions Deep Dive | 15 min | Concise vs block body, implicit return, no own `this`, when NOT to use arrows (methods, constructors), array method callbacks |
| Destructuring Patterns | 15 min | Nested object destructuring, array swap, function parameter destructuring, rest in destructuring, practical API response parsing |
| Spread & Rest Mastery | 10 min | Cloning arrays/objects, merging, function arguments, converting iterables, immutable updates |
| Template Literals Advanced | 5 min | Tagged templates, multi-line, expression evaluation, nesting |
| Shorthand Syntax | 5 min | Property shorthand, method shorthand, computed property names |
| Optional Chaining & Nullish Coalescing | 10 min | `?.` for safe property access, `??` vs `\|\|`, chaining with methods `?.()` and bracket `?.[]` |
| JavaScript Modules | 15 min | `export default`, named exports, `import { } from`, module scope, organizing code into modules, `<script type="module">` |
| Lab: Refactor to ES6+ | 15 min | Take pre-ES6 code and refactor using modern features |

**Key Code Examples:**

```javascript
// Arrow function patterns
const numbers = [1, 2, 3, 4, 5];

// Single param, implicit return
const doubled = numbers.map(n => n * 2);

// Multiple params
const add = (a, b) => a + b;

// Block body (explicit return needed)
const getGrade = (score) => {
  if (score >= 90) return "A";
  if (score >= 80) return "B";
  if (score >= 70) return "C";
  return "F";
};

// Returning an object (wrap in parentheses)
const makeUser = (name, age) => ({ name, age, id: Date.now() });

// Advanced destructuring
const apiResponse = {
  data: {
    user: {
      name: "Alice",
      address: {
        city: "Lagos",
        country: "Nigeria"
      }
    },
    posts: [
      { id: 1, title: "First Post" },
      { id: 2, title: "Second Post" }
    ]
  },
  status: 200
};

// Nested destructuring
const { 
  data: { 
    user: { name, address: { city } },
    posts: [firstPost, ...otherPosts]
  }, 
  status 
} = apiResponse;

console.log(name);        // "Alice"
console.log(city);        // "Lagos"
console.log(firstPost);   // { id: 1, title: "First Post" }
console.log(otherPosts);  // [{ id: 2, title: "Second Post" }]

// Optional chaining
const user = { profile: { avatar: null } };
console.log(user.profile?.avatar?.url);     // undefined (no error!)
console.log(user.settings?.theme);           // undefined (no error!)

// Nullish coalescing
const config = { timeout: 0, retries: null };
const timeout = config.timeout ?? 3000;   // 0 (preserves falsy 0)
const retries = config.retries ?? 3;      // 3 (null/undefined fallback)

// Spread — immutable updates
const original = { name: "Alice", age: 25, role: "student" };
const updated = { ...original, age: 26, email: "alice@example.com" };
// original is unchanged!

// Modules (in separate files)
// utils.js
export const formatDate = (date) => date.toLocaleDateString();
export const capitalize = (str) => str.charAt(0).toUpperCase() + str.slice(1);
export default function logger(msg) {
  console.log(`[LOG] ${msg}`);
}

// app.js
// import logger, { formatDate, capitalize } from './utils.js';
```

**Homework:**
-   Refactor your Week 09 to-do list using ES6+ features (arrow functions, destructuring, spread)
-   Create a `utils.js` module with 5+ utility functions, import and use them in `app.js`
-   Practice optional chaining: safely access deeply nested API-like objects
-   Challenge: Build an immutable state manager using spread operator and pure functions

---

### Session 29 — Asynchronous JavaScript & Fetch API (90 min)

**Learning Objectives:**
-   Explain why JavaScript is single-threaded and what the event loop does
-   Understand callbacks and "callback hell"
-   Create and consume Promises
-   Use `async/await` for clean asynchronous code
-   Fetch data from public APIs using the Fetch API
-   Handle errors with `try/catch` in async functions
-   Display fetched data dynamically in the DOM

**Topics Covered:**

| Topic | Duration | Details |
|-------|----------|---------|
| Sync vs Async | 10 min | Blocking vs non-blocking, `setTimeout()`, `setInterval()`, the event loop (call stack, task queue, microtask queue) |
| Callbacks | 10 min | Functions as arguments, callback pattern, callback hell / pyramid of doom, why we need something better |
| Promises | 15 min | `new Promise((resolve, reject) => {})`, `.then()`, `.catch()`, `.finally()`, Promise states (pending, fulfilled, rejected), chaining |
| async/await | 15 min | `async` function keyword, `await` expression, sequential vs parallel (`Promise.all()`), `try/catch` for errors |
| Fetch API | 20 min | `fetch(url)`, response object, `response.json()`, GET request, query parameters, headers, status codes, error handling |
| Working with Public APIs | 10 min | Free APIs (JSONPlaceholder, OpenWeatherMap, PokéAPI, REST Countries), API keys, rate limiting, CORS basics |
| Lab: API Data Viewer | 10 min | Fetch and display data from JSONPlaceholder — show users, posts, or todos with loading/error states |

**Key Code Examples:**

```javascript
// setTimeout / setInterval (async foundations)
console.log("1. Start");
setTimeout(() => console.log("2. Timeout (2 seconds)"), 2000);
console.log("3. End");
// Output: 1. Start → 3. End → 2. Timeout (2 seconds)

// Promise creation
function wait(ms) {
  return new Promise((resolve) => {
    setTimeout(resolve, ms);
  });
}

wait(1000).then(() => console.log("1 second passed!"));

// Promise chain
function fetchUserData(userId) {
  return fetch(`https://jsonplaceholder.typicode.com/users/${userId}`)
    .then(response => {
      if (!response.ok) {
        throw new Error(`HTTP error! Status: ${response.status}`);
      }
      return response.json();
    })
    .then(user => {
      console.log(`User: ${user.name}`);
      return user;
    })
    .catch(error => {
      console.error("Failed to fetch user:", error.message);
    });
}

// async/await (cleaner syntax for the same thing)
async function fetchUser(userId) {
  try {
    const response = await fetch(
      `https://jsonplaceholder.typicode.com/users/${userId}`
    );
    
    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
    
    const user = await response.json();
    console.log(`User: ${user.name}, City: ${user.address.city}`);
    return user;
  } catch (error) {
    console.error("Failed to fetch user:", error.message);
  }
}

// Fetching and displaying in DOM
async function displayUsers() {
  const container = document.querySelector("#users");
  container.innerHTML = '<p class="loading">Loading users...</p>';
  
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/users");
    if (!response.ok) throw new Error("Failed to fetch");
    
    const users = await response.json();
    
    container.innerHTML = users.map(user => `
      <div class="user-card">
        <h3>${user.name}</h3>
        <p>��� ${user.email}</p>
        <p>���️ ${user.address.city}</p>
        <p>��� ${user.company.name}</p>
      </div>
    `).join("");
    
  } catch (error) {
    container.innerHTML = `
      <p class="error">❌ Error: ${error.message}. Please try again.</p>
    `;
  }
}

// Parallel requests with Promise.all
async function fetchDashboard(userId) {
  try {
    const [user, posts, todos] = await Promise.all([
      fetch(`https://jsonplaceholder.typicode.com/users/${userId}`).then(r => r.json()),
      fetch(`https://jsonplaceholder.typicode.com/posts?userId=${userId}`).then(r => r.json()),
      fetch(`https://jsonplaceholder.typicode.com/todos?userId=${userId}`).then(r => r.json()),
    ]);
    
    console.log(`${user.name} has ${posts.length} posts and ${todos.length} todos`);
    return { user, posts, todos };
  } catch (error) {
    console.error("Dashboard load failed:", error);
  }
}

// Search with debounce (real-world pattern)
let debounceTimer;
const searchInput = document.querySelector("#search");

searchInput.addEventListener("input", (event) => {
  clearTimeout(debounceTimer);
  debounceTimer = setTimeout(async () => {
    const query = event.target.value.trim();
    if (query.length < 2) return;
    
    const response = await fetch(
      `https://jsonplaceholder.typicode.com/users?name_like=${query}`
    );
    const results = await response.json();
    displayResults(results);
  }, 300);
});
```

**Homework:**
-   Build a **User Directory**: fetch all users from JSONPlaceholder, display as cards, add a search/filter
-   Add **loading states** (spinner/text) and **error handling** (user-friendly error messages)
-   Use `Promise.all()` to fetch users AND their posts simultaneously
-   Challenge: Build a country info app using the [REST Countries API](https://restcountries.com/) — search by name, display flag, population, capital, languages

---

### Session 30 — Mini Project 2: Interactive JavaScript App (90 min)

**Learning Objectives:**
-   Plan and build a complete interactive application from scratch
-   Combine DOM manipulation, events, ES6+, and Fetch API
-   Implement loading states, error handling, and user feedback
-   Write clean, modular, well-organized code

**Project Options (Choose One):**

| Project | Difficulty | API | Features |
|---------|-----------|-----|----------|
| Weather App | ⭐⭐ | OpenWeatherMap / wttr.in | Search city, display temp/conditions/forecast, location icon |
| Movie Search | ⭐⭐ | OMDb API / TMDb | Search movies, display posters/ratings/plot, favorites list |
| Quiz Game | ⭐⭐⭐ | Open Trivia DB | Category selection, timed questions, score tracking, leaderboard |
| Recipe Finder | ⭐⭐ | TheMealDB | Search recipes, display ingredients/instructions, save favorites |
| GitHub Profile Viewer | ⭐⭐ | GitHub API | Search users, display repos/bio/avatar, repo statistics |

**Project Requirements:**

```
✅ Required Features:
  □ HTML/CSS responsive layout (use skills from Weeks 01–06)
  □ JavaScript with ES6+ syntax throughout
  □ Fetch data from at least one public API
  □ DOM manipulation for dynamic content rendering
  □ Event handling for user interactions (search, click, submit)
  □ Loading state while data is being fetched
  □ Error handling with user-friendly messages
  □ At least one array method (map, filter, or reduce)

⭐ Bonus Features:
  □ Local storage for saving user preferences / favorites
  □ Multiple API endpoints
  □ Keyboard accessibility
  □ Dark mode toggle
  □ Responsive design (works on mobile)
```

**Session Structure:**

| Phase | Duration | Activity |
|-------|----------|----------|
| Planning | 15 min | Choose project, sketch UI, identify API endpoints, plan data flow |
| Setup | 10 min | Create files (HTML, CSS, JS), set up project structure, test API in console |
| Core Build | 40 min | Implement fetch, DOM rendering, event handlers, loading/error states |
| Polish & Debug | 15 min | Styling, edge cases, code cleanup, accessibility |
| Demo & Review | 10 min | Present work, peer feedback, discuss improvements |

**Example: Weather App Starter Structure**

```
weather-app/
├── index.html
├── style.css
├── app.js
└── README.md
```

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Weather App</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="app">
    <header>
      <h1>���️ Weather App</h1>
      <form id="search-form">
        <input type="text" id="city-input" placeholder="Enter city name..." 
               autocomplete="off" required>
        <button type="submit">Search</button>
      </form>
    </header>
    
    <main id="weather-display">
      <p class="placeholder">Search for a city to see the weather.</p>
    </main>
  </div>
  
  <script src="app.js" defer></script>
</body>
</html>
```

```javascript
// app.js — Weather App starter
const form = document.querySelector("#search-form");
const input = document.querySelector("#city-input");
const display = document.querySelector("#weather-display");

form.addEventListener("submit", async (event) => {
  event.preventDefault();
  const city = input.value.trim();
  if (!city) return;
  
  await fetchWeather(city);
  input.value = "";
});

async function fetchWeather(city) {
  showLoading();
  
  try {
    const response = await fetch(
      `https://wttr.in/${encodeURIComponent(city)}?format=j1`
    );
    
    if (!response.ok) throw new Error("City not found");
    
    const data = await response.json();
    renderWeather(data, city);
  } catch (error) {
    showError(error.message);
  }
}

function showLoading() {
  display.innerHTML = '<p class="loading">⏳ Fetching weather data...</p>';
}

function showError(message) {
  display.innerHTML = `<p class="error">❌ ${message}. Please try again.</p>`;
}

function renderWeather(data, city) {
  const current = data.current_condition[0];
  const { temp_C, temp_F, humidity, weatherDesc, windspeedKmph } = current;
  
  display.innerHTML = `
    <div class="weather-card">
      <h2>${city}</h2>
      <p class="temp">${temp_C}°C / ${temp_F}°F</p>
      <p class="desc">${weatherDesc[0].value}</p>
      <div class="details">
        <span>��� Humidity: ${humidity}%</span>
        <span>��� Wind: ${windspeedKmph} km/h</span>
      </div>
    </div>
  `;
}
```

**Deliverable:**
-   **Mini Project 2: Interactive JavaScript App** — due end of Week 10
-   Submit: GitHub repository link with README documenting features, API used, and how to run
-   Grading rubric: functionality (40%), code quality & ES6+ usage (25%), UI/UX (20%), error handling (15%)

---

## Week 10 Summary

By the end of this week, students can:

| Skill | Status |
|-------|--------|
| Use ES6+ syntax confidently | ✅ |
| Apply destructuring and spread/rest | ✅ |
| Use optional chaining and nullish coalescing | ✅ |
| Organize code with modules | ✅ |
| Understand async vs sync execution | ✅ |
| Work with Promises and async/await | ✅ |
| Fetch data from public APIs | ✅ |
| Handle errors in async code | ✅ |
| Display dynamic data in the DOM | ✅ |
| Build complete interactive applications | ✅ |

## 4-Week JavaScript Journey Complete! ���

After completing Weeks 07–10, students have a solid foundation in:

| Week | Core Skills Gained |
|------|-------------------|
| Week 07 | JS syntax, variables, types, operators, control flow |
| Week 08 | Functions, scope, arrays, objects, JSON |
| Week 09 | DOM selection/manipulation, events, forms, event delegation |
| Week 10 | ES6+ features, async/await, Fetch API, building complete apps |

Students are now ready for **Phase 3** (Weeks 11–14): web storage, API integration, accessibility, Git/GitHub, and the final capstone project.

## Resources

-   [MDN: Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
-   [MDN: Destructuring Assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
-   [MDN: Using Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)
-   [MDN: async function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)
-   [MDN: Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
-   [JavaScript.info: Async/Await](https://javascript.info/async-await)
-   [Public APIs List](https://github.com/public-apis/public-apis)
-   [JSONPlaceholder](https://jsonplaceholder.typicode.com/)
