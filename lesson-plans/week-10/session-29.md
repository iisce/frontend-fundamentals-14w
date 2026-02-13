# Week 10 — Session 29: Async JavaScript & Fetch API

**Navigation:**
← [Session 28](session-28.md) | [Week 10 Index](../week-10.md) | [Session 30](session-30.md) →

---

**Session Length:** 90 minutes

## 📋 Pre-Class Checklist

Before starting this session, make sure you have:

- ✅ Completed Session 28 (ES6+ features)
- ✅ Understand callbacks, arrow functions, and Promises concept
- ✅ Comfortable with DOM manipulation and events
- ✅ Create: `async-demo.html` and `async-demo.js`

## 🎯 Learning Objectives

By the end of this session, you will be able to:

- Explain synchronous vs asynchronous JavaScript
- Use callbacks and understand callback limitations
- Create and consume Promises
- Write clean async code with `async`/`await`
- Fetch data from APIs using the Fetch API
- Handle loading states, errors, and edge cases
- Use `try/catch` for error handling in async code
- Process and display API data in the DOM

## 📦 Files for This Session

- `session-29.md` — This tutorial (you're reading it!)
- Create: `async-demo.html`, `async-demo.js`

## 🔑 Key Terms

**synchronous**, **asynchronous**, **callback**, **callback hell**, **Promise**, **pending**, **fulfilled**, **rejected**, **then**, **catch**, **finally**, **async**, **await**, **Fetch API**, **JSON**, **REST API**, **HTTP methods**, **status codes**, **try/catch**, **Promise.all**, **Promise.race**

## 🏗️ What You Will Build

- A user profile card fetched from an API
- A weather dashboard with loading states
- A searchable user directory

---

## Part 1: Synchronous vs Asynchronous (10 minutes)

### Synchronous Code (Default)

Code runs line by line, each line waits for the previous one:

```javascript
console.log('1. Start');
console.log('2. Middle');
console.log('3. End');
// Output: 1, 2, 3 (in order, immediately)
```

### Asynchronous Code

Some operations take time (network requests, timers, file reading). JavaScript doesn't wait — it moves on:

```javascript
console.log('1. Start');

setTimeout(() => {
	console.log('2. This runs after 2 seconds');
}, 2000);

console.log('3. This runs immediately!');

// Output: 1, 3, (2 seconds later) 2
```

### Why Async?

- **Network requests** — Fetching data from a server takes time
- **Timers** — `setTimeout`, `setInterval`
- **User interactions** — Waiting for clicks, typing
- **File operations** — Reading/writing files
- **Animations** — requestAnimationFrame

> 💡 JavaScript is **single-threaded** but uses an **event loop** to handle async operations without blocking.

### `setTimeout` and `setInterval`

```javascript
// setTimeout — run once after a delay
const timerId = setTimeout(() => {
	console.log('Delayed message!');
}, 3000); // 3 seconds

// Cancel a timeout
clearTimeout(timerId);

// setInterval — run repeatedly
let count = 0;
const intervalId = setInterval(() => {
	count++;
	console.log(`Tick ${count}`);
	if (count >= 5) {
		clearInterval(intervalId); // stop after 5 ticks
	}
}, 1000);
```

<details>
<summary>💡 Knowledge Check #1</summary>

**Question:** What will this code output and in what order?

```javascript
console.log('A');
setTimeout(() => console.log('B'), 0);
console.log('C');
```

**Answer:**

```
A
C
B
```

Even with a 0ms delay, `setTimeout` is **asynchronous** — it goes to the task queue and waits until the current synchronous code finishes. So "A" and "C" run first, then "B" runs from the queue.

</details>

---

## Part 2: Callbacks & Their Problems (10 minutes)

### Callbacks

A callback is a function passed to another function to be called later:

```javascript
function fetchData(url, callback) {
	setTimeout(() => {
		const data = { name: 'Alice', age: 25 };
		callback(data);
	}, 1000);
}

fetchData('/api/user', (data) => {
	console.log('Got data:', data);
});
```

### Callback Hell (The Problem)

Nested callbacks become unreadable quickly:

```javascript
// ❌ Callback Hell — "Pyramid of Doom"
getUser(userId, (user) => {
	getOrders(user.id, (orders) => {
		getOrderDetails(orders[0].id, (details) => {
			getShippingInfo(details.shippingId, (shipping) => {
				console.log('Shipping:', shipping);
				// 4 levels deep, hard to read, hard to handle errors
			});
		});
	});
});
```

---

## Part 3: Promises (15 minutes)

### What Is a Promise?

A Promise is an object representing the eventual result of an async operation:

```javascript
// Creating a Promise
const myPromise = new Promise((resolve, reject) => {
	const success = true;

	setTimeout(() => {
		if (success) {
			resolve({ name: 'Alice', age: 25 }); // fulfilled!
		} else {
			reject(new Error('Something went wrong')); // rejected!
		}
	}, 1000);
});

// Consuming a Promise
myPromise
	.then((data) => {
		console.log('Success:', data);
	})
	.catch((error) => {
		console.error('Error:', error.message);
	})
	.finally(() => {
		console.log('Done (runs either way)');
	});
```

### Promise States

| State         | Description                                       |
| ------------- | ------------------------------------------------- |
| **Pending**   | Initial state — not yet fulfilled or rejected     |
| **Fulfilled** | Operation completed successfully (`.then()` runs) |
| **Rejected**  | Operation failed (`.catch()` runs)                |

### Chaining Promises

```javascript
function fetchUser(id) {
	return new Promise((resolve) => {
		setTimeout(() => resolve({ id, name: 'Alice' }), 500);
	});
}

function fetchOrders(userId) {
	return new Promise((resolve) => {
		setTimeout(() => resolve([{ id: 1, item: 'Laptop' }]), 500);
	});
}

// ✅ Promise chain — flat and readable!
fetchUser(1)
	.then((user) => {
		console.log('User:', user.name);
		return fetchOrders(user.id);
	})
	.then((orders) => {
		console.log('Orders:', orders);
	})
	.catch((error) => {
		console.error('Error:', error.message);
	});
```

### `Promise.all()` — Run in Parallel

```javascript
// Run multiple promises at the same time
const promise1 = fetch('/api/users').then((r) => r.json());
const promise2 = fetch('/api/posts').then((r) => r.json());
const promise3 = fetch('/api/comments').then((r) => r.json());

Promise.all([promise1, promise2, promise3])
	.then(([users, posts, comments]) => {
		console.log('Users:', users.length);
		console.log('Posts:', posts.length);
		console.log('Comments:', comments.length);
	})
	.catch((error) => {
		console.error('One failed:', error);
	});

// Promise.allSettled — doesn't fail if one rejects
Promise.allSettled([promise1, promise2, promise3]).then((results) => {
	results.forEach((result) => {
		if (result.status === 'fulfilled') {
			console.log('Success:', result.value);
		} else {
			console.log('Failed:', result.reason);
		}
	});
});
```

<details>
<summary>💡 Knowledge Check #2</summary>

**Question:** What is the difference between `Promise.all()` and `Promise.allSettled()`?

**Answer:**

- `Promise.all()` — Waits for ALL promises to resolve. If **any one** rejects, the entire `Promise.all` rejects immediately ("fail fast").
- `Promise.allSettled()` — Waits for ALL promises to finish (resolve or reject). Returns results for **each** promise with `status: "fulfilled"` or `status: "rejected"`. Never rejects.

Use `Promise.all` when you need ALL results or none. Use `Promise.allSettled` when you want to process whatever succeeds.

</details>

---

## Part 4: Async/Await (15 minutes)

### The Modern Way

`async`/`await` is syntactic sugar over Promises — same behavior, cleaner syntax:

```javascript
// With Promises
function getUser() {
	return fetch('https://jsonplaceholder.typicode.com/users/1')
		.then((response) => response.json())
		.then((user) => {
			console.log(user.name);
			return user;
		});
}

// With async/await — reads like synchronous code!
async function getUser() {
	const response = await fetch(
		'https://jsonplaceholder.typicode.com/users/1',
	);
	const user = await response.json();
	console.log(user.name);
	return user;
}
```

### Rules of async/await

```javascript
// 1. 'await' can only be used inside an 'async' function
async function getData() {
	const result = await somePromise; // ✅
}

// 2. async functions always return a Promise
async function greet() {
	return 'Hello'; // automatically wrapped in Promise.resolve("Hello")
}
greet().then((msg) => console.log(msg)); // "Hello"

// 3. Top-level await (in modules only)
// <script type="module">
//   const data = await fetch("/api/data").then(r => r.json());
// </script>
```

### Error Handling with try/catch

```javascript
async function fetchUserSafely(id) {
	try {
		const response = await fetch(
			`https://jsonplaceholder.typicode.com/users/${id}`,
		);

		if (!response.ok) {
			throw new Error(`HTTP error! Status: ${response.status}`);
		}

		const user = await response.json();
		console.log('User:', user.name);
		return user;
	} catch (error) {
		console.error('Failed to fetch user:', error.message);
		return null; // return a fallback value
	} finally {
		console.log('Fetch attempt complete');
		// cleanup code (hide loading spinner, etc.)
	}
}

fetchUserSafely(1);
fetchUserSafely(999); // will trigger error (user not found)
```

### Parallel Async/Await

```javascript
// ❌ Sequential — each waits for the previous (slow!)
async function loadSequential() {
	const users = await fetch('/api/users').then((r) => r.json()); // wait...
	const posts = await fetch('/api/posts').then((r) => r.json()); // then wait...
	const comments = await fetch('/api/comments').then((r) => r.json()); // then wait...
	return { users, posts, comments };
}

// ✅ Parallel — all start at once (fast!)
async function loadParallel() {
	const [users, posts, comments] = await Promise.all([
		fetch('/api/users').then((r) => r.json()),
		fetch('/api/posts').then((r) => r.json()),
		fetch('/api/comments').then((r) => r.json()),
	]);
	return { users, posts, comments };
}
```

---

## Part 5: Fetch API Deep Dive (10 minutes)

### GET Request (Default)

```javascript
async function getUsers() {
	const response = await fetch('https://jsonplaceholder.typicode.com/users');
	const users = await response.json();
	return users;
}
```

### POST Request

```javascript
async function createPost(title, body) {
	const response = await fetch('https://jsonplaceholder.typicode.com/posts', {
		method: 'POST',
		headers: {
			'Content-Type': 'application/json',
		},
		body: JSON.stringify({
			title,
			body,
			userId: 1,
		}),
	});

	const newPost = await response.json();
	console.log('Created:', newPost);
	return newPost;
}
```

### Handling Different Response Types

```javascript
async function fetchData(url) {
	const response = await fetch(url);

	// Check status
	console.log('Status:', response.status); // 200, 404, 500, etc.
	console.log('OK?:', response.ok); // true if 200-299
	console.log('Status text:', response.statusText); // "OK", "Not Found"

	// Different response formats
	const json = await response.json(); // Parse as JSON
	// const text = await response.text();  // Raw text
	// const blob = await response.blob();  // Binary data (images, files)

	return json;
}
```

### HTTP Status Codes to Know

| Code | Meaning                                |
| ---- | -------------------------------------- |
| 200  | OK — success                           |
| 201  | Created — resource created             |
| 204  | No Content — success but no body       |
| 400  | Bad Request — invalid data sent        |
| 401  | Unauthorized — not logged in           |
| 403  | Forbidden — no permission              |
| 404  | Not Found — resource doesn't exist     |
| 500  | Internal Server Error — server problem |

<details>
<summary>💡 Knowledge Check #3</summary>

**Question:** Why do we need TWO `await` calls when using `fetch`?

```javascript
const response = await fetch(url); // First await
const data = await response.json(); // Second await
```

**Answer:**

1. **First `await`** — Waits for the HTTP response headers to arrive. At this point, the response body hasn't been fully downloaded yet.
2. **Second `await`** — Waits for the response body to be fully downloaded and parsed as JSON.

`response.json()` returns a Promise because parsing a large response body is an async operation. The body comes as a stream that needs to be read completely before parsing.

</details>

---

## Part 6: Lab — User Directory (20 minutes)

### Challenge: Build a Searchable User Directory

Create a page that fetches users from an API and displays them as cards with search functionality.

**HTML Setup (`async-demo.html`):**

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<title>User Directory</title>
		<style>
			* {
				box-sizing: border-box;
				margin: 0;
				padding: 0;
			}
			body {
				font-family: Arial, sans-serif;
				max-width: 900px;
				margin: 0 auto;
				padding: 20px;
				background: #f5f5f5;
			}
			h1 {
				text-align: center;
				margin-bottom: 20px;
			}
			.search-box {
				width: 100%;
				padding: 12px 16px;
				font-size: 16px;
				border: 2px solid #ddd;
				border-radius: 8px;
				margin-bottom: 20px;
			}
			.loading {
				text-align: center;
				font-size: 18px;
				color: #666;
				padding: 40px;
			}
			.error {
				text-align: center;
				color: #e74c3c;
				padding: 20px;
				background: #ffeaea;
				border-radius: 8px;
			}
			.grid {
				display: grid;
				grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
				gap: 16px;
			}
			.user-card {
				background: white;
				border-radius: 12px;
				padding: 20px;
				box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
			}
			.user-card h2 {
				margin-bottom: 8px;
				color: #333;
			}
			.user-card p {
				color: #666;
				margin-bottom: 4px;
				font-size: 14px;
			}
			.user-card .company {
				color: #3498db;
				font-weight: bold;
			}
			.no-results {
				text-align: center;
				color: #999;
				padding: 40px;
			}
		</style>
	</head>
	<body>
		<h1>👥 User Directory</h1>
		<input
			type="text"
			class="search-box"
			id="search"
			placeholder="Search users by name, email, or company..."
		/>
		<div id="app">
			<div class="loading">Loading users...</div>
		</div>

		<script src="async-demo.js"></script>
	</body>
</html>
```

**Starter Code (`async-demo.js`):**

```javascript
const app = document.querySelector('#app');
const searchInput = document.querySelector('#search');
let allUsers = [];

// TODO 1: Fetch users from https://jsonplaceholder.typicode.com/users
async function fetchUsers() {
	// Show loading state
	// Fetch data with error handling
	// Store in allUsers
	// Render the users
}

// TODO 2: Render user cards
function renderUsers(users) {
	// If no users, show "no results" message
	// Create cards for each user with: name, email, phone, company, city
	// Use template literals and innerHTML or createElement
}

// TODO 3: Filter users based on search input
function filterUsers(query) {
	// Filter allUsers by name, email, or company name
	// Case-insensitive search
	// Render the filtered results
}

// TODO 4: Set up search event listener with debounce
// TODO 5: Call fetchUsers to initialize
```

<details>
<summary>✅ Solution</summary>

```javascript
const app = document.querySelector('#app');
const searchInput = document.querySelector('#search');
let allUsers = [];

async function fetchUsers() {
	app.innerHTML = '<div class="loading">⏳ Loading users...</div>';

	try {
		const response = await fetch(
			'https://jsonplaceholder.typicode.com/users',
		);

		if (!response.ok) {
			throw new Error(`HTTP error! Status: ${response.status}`);
		}

		allUsers = await response.json();
		renderUsers(allUsers);
	} catch (error) {
		app.innerHTML = `
      <div class="error">
        <p>❌ Failed to load users: ${error.message}</p>
        <button onclick="fetchUsers()">Try Again</button>
      </div>
    `;
	}
}

function renderUsers(users) {
	if (users.length === 0) {
		app.innerHTML =
			'<div class="no-results">No users found matching your search.</div>';
		return;
	}

	app.innerHTML = `
    <div class="grid">
      ${users
			.map(
				(user) => `
        <div class="user-card">
          <h2>${user.name}</h2>
          <p>📧 ${user.email.toLowerCase()}</p>
          <p>📞 ${user.phone}</p>
          <p>📍 ${user.address.city}</p>
          <p class="company">🏢 ${user.company.name}</p>
        </div>
      `,
			)
			.join('')}
    </div>
  `;
}

function filterUsers(query) {
	const q = query.toLowerCase().trim();

	if (!q) {
		renderUsers(allUsers);
		return;
	}

	const filtered = allUsers.filter(
		(user) =>
			user.name.toLowerCase().includes(q) ||
			user.email.toLowerCase().includes(q) ||
			user.company.name.toLowerCase().includes(q),
	);

	renderUsers(filtered);
}

// Debounce helper
function debounce(fn, delay) {
	let timer;
	return (...args) => {
		clearTimeout(timer);
		timer = setTimeout(() => fn(...args), delay);
	};
}

searchInput.addEventListener(
	'input',
	debounce((e) => {
		filterUsers(e.target.value);
	}, 300),
);

fetchUsers();
```

</details>

---

## ⚠️ Common Mistakes

| Mistake                                | Problem                               | Fix                                                    |
| -------------------------------------- | ------------------------------------- | ------------------------------------------------------ |
| Not checking `response.ok`             | 404/500 errors aren't thrown by fetch | `if (!response.ok) throw new Error(...)`               |
| Forgetting `await` before `fetch`      | Gets a Promise object, not data       | `const data = await fetch(url)`                        |
| Calling `.json()` twice                | Stream already consumed               | Store the result: `const data = await response.json()` |
| Sequential fetches when parallel works | Slow performance                      | Use `Promise.all()` for independent requests           |
| No loading/error states in UI          | Poor user experience                  | Show loading before fetch, error on catch              |
| Not wrapping async code in try/catch   | Unhandled promise rejections          | Always use try/catch with async/await                  |

---

## 📝 Session Summary

In this session, you learned:

1. **Sync vs Async** — JavaScript event loop, non-blocking behavior
2. **Callbacks** — Functions called later, callback hell problem
3. **Promises** — `new Promise`, `.then()`, `.catch()`, `.finally()`
4. **Promise utilities** — `Promise.all()`, `Promise.allSettled()`, `Promise.race()`
5. **Async/Await** — Clean async syntax, `try/catch` error handling
6. **Fetch API** — GET, POST requests, response handling, status codes
7. **UI patterns** — Loading states, error handling, search with debounce

---

## 🏠 Homework

### Task 1: Weather Dashboard

Use the [Open-Meteo API](https://open-meteo.com/en/docs) (free, no API key) to:

- Fetch weather for a city
- Display temperature, wind speed, and conditions
- Show a loading spinner while fetching
- Handle errors gracefully

### Task 2: GitHub Profile Viewer

Using the GitHub API (`https://api.github.com/users/{username}`):

- Prompt the user for a GitHub username
- Fetch and display their profile (avatar, name, bio, repos count)
- Show their recent repos (`/users/{username}/repos?sort=updated`)
- Handle 404 (user not found) gracefully

### Task 3: Multi-API Dashboard

Fetch data from multiple endpoints simultaneously:

- Users from JSONPlaceholder
- A random quote from a quotes API
- Display all data on a single dashboard
- Use `Promise.all()` for parallel fetching

### Bonus: Retry Logic

Create a `fetchWithRetry(url, maxRetries)` function that:

- Attempts to fetch the URL
- If it fails, waits 1 second and retries
- Doubles the wait time each retry (exponential backoff)
- Gives up after `maxRetries` attempts

---

## 📚 Resources

- [MDN: Using Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)
- [MDN: Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- [MDN: async/await](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Promises)
- [JavaScript.info: Fetch](https://javascript.info/fetch)
- [JavaScript.info: Async/Await](https://javascript.info/async-await)
- [JavaScript.info: Promise API](https://javascript.info/promise-api)
- [JSONPlaceholder](https://jsonplaceholder.typicode.com/) — Free fake API for testing

---

**Next:** [Session 30 — Mini Project 2: Interactive Web App](session-30.md) →
