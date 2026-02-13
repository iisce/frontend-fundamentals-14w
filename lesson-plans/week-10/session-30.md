# Week 10 — Session 30: Mini Project 2 — Interactive Web App

**Navigation:**
← [Session 29](session-29.md) | [Week 10 Index](../week-10.md) | [Phase 3: Integration →](../week-11.md)

---

**Session Length:** 90 minutes

## 📋 Pre-Class Checklist

Before starting this session, make sure you have:

- ✅ Completed Sessions 19–29 (all JavaScript fundamentals)
- ✅ Comfortable with DOM manipulation and events
- ✅ Understand async/await and Fetch API
- ✅ Create a project folder: `mini-project-2/`
- ✅ Inside it, create: `index.html`, `style.css`, `app.js`

## 🎯 Learning Objectives

By the end of this session, you will be able to:

- Plan and scope a front-end JavaScript project
- Structure HTML, CSS, and JS files for a multi-feature app
- Implement CRUD-like functionality using arrays and objects
- Handle user input with forms and validation
- Fetch and display data from an external API
- Apply ES6+ features in a real project
- Polish, test, and present a working application

## 📦 Files for This Session

- `session-30.md` — This tutorial (you're reading it!)
- Create a project folder: `mini-project-2/`
    - `index.html` — page structure
    - `style.css` — styling
    - `app.js` — all application logic

## 🔑 Key Terms

**project planning**, **user stories**, **MVP**, **CRUD**, **state management**, **separation of concerns**, **event delegation**, **localStorage**, **API integration**, **deployment**, **code review**

## 🏗️ What You Will Build

An **Interactive Recipe Finder** — a single-page app that lets users:

- Search for recipes from an API
- View recipe details (ingredients, instructions)
- Save favorite recipes to a personal collection (localStorage)
- Remove favorites
- Filter favorites by category
- Responsive, polished UI with loading and error states

> 💡 This project brings together **everything** you've learned: HTML structure, CSS styling, DOM manipulation, events, arrays/objects, async/await, and Fetch API.

---

## Part 1: Project Planning & Structure (10 minutes)

### Step 1: Define Your Features (User Stories)

Write down what the app should do:

| #   | User Story                                        | Priority     |
| --- | ------------------------------------------------- | ------------ |
| 1   | As a user, I can search for recipes by keyword    | Must Have    |
| 2   | As a user, I can see recipe results as cards      | Must Have    |
| 3   | As a user, I can click a card to see full details | Must Have    |
| 4   | As a user, I can save recipes to favorites        | Must Have    |
| 5   | As a user, I can view my saved favorites          | Must Have    |
| 6   | As a user, I can remove a recipe from favorites   | Must Have    |
| 7   | As a user, I can filter favorites by category     | Nice to Have |
| 8   | As a user, my favorites persist on page reload    | Nice to Have |

### Step 2: Choose an API

We'll use the free [TheMealDB API](https://www.themealdb.com/api.php):

- **Search meals:** `https://www.themealdb.com/api/json/v1/1/search.php?s=chicken`
- **Meal by ID:** `https://www.themealdb.com/api/json/v1/1/lookup.php?i=52772`
- **Random meal:** `https://www.themealdb.com/api/json/v1/1/random.php`
- **Categories:** `https://www.themealdb.com/api/json/v1/1/categories.php`
- No API key required!

### Step 3: Plan File Structure

```
mini-project-2/
├── index.html      ← Structure & layout
├── style.css       ← All styling
└── app.js          ← Application logic
```

<details>
<summary>💡 Knowledge Check #1</summary>

**Question:** What does MVP stand for, and why is it important for project planning?

**Answer:**
**MVP** = **Minimum Viable Product**. It's the simplest version of your project that still works and delivers value. Start with "Must Have" features, get them working, then add "Nice to Have" features. This prevents wasting time on polish before core features work.

</details>

---

## Part 2: HTML Structure (10 minutes)

Create the page layout with all the sections your app needs:

**`index.html`:**

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta
			name="viewport"
			content="width=device-width, initial-scale=1.0"
		/>
		<title>🍽️ Recipe Finder</title>
		<link
			rel="stylesheet"
			href="style.css"
		/>
	</head>
	<body>
		<!-- Header -->
		<header class="header">
			<h1>🍽️ Recipe Finder</h1>
			<nav class="nav-tabs">
				<button
					class="tab active"
					data-tab="search"
				>
					Search
				</button>
				<button
					class="tab"
					data-tab="favorites"
				>
					Favorites <span id="fav-count">(0)</span>
				</button>
			</nav>
		</header>

		<main class="container">
			<!-- Search Section -->
			<section
				id="search-section"
				class="section"
			>
				<form
					id="search-form"
					class="search-bar"
				>
					<input
						type="text"
						id="search-input"
						placeholder="Search for a recipe... (e.g., chicken, pasta, salad)"
						aria-label="Search recipes"
						required
					/>
					<button type="submit">Search</button>
				</form>

				<div
					id="search-results"
					class="grid"
				>
					<!-- Recipe cards will be rendered here -->
				</div>
			</section>

			<!-- Favorites Section (hidden by default) -->
			<section
				id="favorites-section"
				class="section hidden"
			>
				<div class="favorites-header">
					<h2>My Favorite Recipes</h2>
					<select
						id="category-filter"
						aria-label="Filter by category"
					>
						<option value="all">All Categories</option>
					</select>
				</div>

				<div
					id="favorites-list"
					class="grid"
				>
					<!-- Favorite recipe cards here -->
				</div>
			</section>

			<!-- Recipe Detail Modal -->
			<div
				id="modal"
				class="modal hidden"
				role="dialog"
				aria-modal="true"
			>
				<div class="modal-content">
					<button
						class="modal-close"
						aria-label="Close"
					>
						&times;
					</button>
					<div id="modal-body">
						<!-- Recipe details here -->
					</div>
				</div>
			</div>

			<!-- Loading Overlay -->
			<div
				id="loading"
				class="loading hidden"
			>
				<div class="spinner"></div>
				<p>Searching recipes...</p>
			</div>
		</main>

		<footer class="footer">
			<p>
				Powered by
				<a
					href="https://www.themealdb.com/"
					target="_blank"
					>TheMealDB</a
				>
				| Mini Project 2
			</p>
		</footer>

		<script src="app.js"></script>
	</body>
</html>
```

---

## Part 3: CSS Styling (10 minutes)

Style the app with a clean, responsive layout:

**`style.css`:**

```css
/* ===== Reset & Base ===== */
*,
*::before,
*::after {
	box-sizing: border-box;
	margin: 0;
	padding: 0;
}

body {
	font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
	background: #f0f2f5;
	color: #333;
	min-height: 100vh;
	display: flex;
	flex-direction: column;
}

/* ===== Header ===== */
.header {
	background: linear-gradient(135deg, #e74c3c, #c0392b);
	color: white;
	padding: 20px;
	text-align: center;
}

.header h1 {
	font-size: 2rem;
	margin-bottom: 16px;
}

.nav-tabs {
	display: flex;
	justify-content: center;
	gap: 8px;
}

.tab {
	padding: 10px 24px;
	border: 2px solid white;
	background: transparent;
	color: white;
	border-radius: 25px;
	cursor: pointer;
	font-size: 14px;
	font-weight: 600;
	transition: all 0.3s;
}

.tab:hover,
.tab.active {
	background: white;
	color: #e74c3c;
}

/* ===== Main Content ===== */
.container {
	max-width: 1100px;
	margin: 0 auto;
	padding: 20px;
	flex: 1;
	width: 100%;
}

/* ===== Search Bar ===== */
.search-bar {
	display: flex;
	gap: 8px;
	margin-bottom: 24px;
}

.search-bar input {
	flex: 1;
	padding: 14px 20px;
	border: 2px solid #ddd;
	border-radius: 8px;
	font-size: 16px;
	transition: border-color 0.3s;
}

.search-bar input:focus {
	outline: none;
	border-color: #e74c3c;
}

.search-bar button {
	padding: 14px 28px;
	background: #e74c3c;
	color: white;
	border: none;
	border-radius: 8px;
	cursor: pointer;
	font-size: 16px;
	font-weight: 600;
	transition: background 0.3s;
}

.search-bar button:hover {
	background: #c0392b;
}

/* ===== Grid ===== */
.grid {
	display: grid;
	grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
	gap: 20px;
}

/* ===== Recipe Card ===== */
.recipe-card {
	background: white;
	border-radius: 12px;
	overflow: hidden;
	box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
	cursor: pointer;
	transition:
		transform 0.3s,
		box-shadow 0.3s;
}

.recipe-card:hover {
	transform: translateY(-4px);
	box-shadow: 0 8px 24px rgba(0, 0, 0, 0.15);
}

.recipe-card img {
	width: 100%;
	height: 200px;
	object-fit: cover;
}

.recipe-card .card-body {
	padding: 16px;
}

.recipe-card h3 {
	font-size: 1rem;
	margin-bottom: 8px;
	color: #333;
}

.recipe-card .category {
	display: inline-block;
	background: #ffeaa7;
	color: #d63031;
	padding: 4px 10px;
	border-radius: 12px;
	font-size: 12px;
	font-weight: 600;
}

.fav-btn {
	margin-top: 8px;
	padding: 6px 12px;
	border: 1px solid #e74c3c;
	background: transparent;
	color: #e74c3c;
	border-radius: 6px;
	cursor: pointer;
	font-size: 13px;
	transition: all 0.3s;
}

.fav-btn:hover,
.fav-btn.saved {
	background: #e74c3c;
	color: white;
}

/* ===== Modal ===== */
.modal {
	position: fixed;
	inset: 0;
	background: rgba(0, 0, 0, 0.6);
	display: flex;
	justify-content: center;
	align-items: center;
	z-index: 1000;
	padding: 20px;
}

.modal-content {
	background: white;
	border-radius: 12px;
	max-width: 700px;
	width: 100%;
	max-height: 85vh;
	overflow-y: auto;
	padding: 32px;
	position: relative;
}

.modal-close {
	position: absolute;
	top: 12px;
	right: 16px;
	font-size: 28px;
	background: none;
	border: none;
	cursor: pointer;
	color: #999;
}

.modal-close:hover {
	color: #333;
}

#modal-body img {
	width: 100%;
	border-radius: 8px;
	margin-bottom: 16px;
}

#modal-body h2 {
	margin-bottom: 8px;
}
#modal-body .detail-category {
	color: #e74c3c;
	font-weight: 600;
	margin-bottom: 16px;
}
#modal-body h3 {
	margin: 16px 0 8px;
	color: #e74c3c;
}
#modal-body ul {
	padding-left: 24px;
	margin-bottom: 16px;
}
#modal-body li {
	margin-bottom: 4px;
}
#modal-body p {
	line-height: 1.7;
}

/* ===== Favorites Header ===== */
.favorites-header {
	display: flex;
	justify-content: space-between;
	align-items: center;
	margin-bottom: 20px;
	flex-wrap: wrap;
	gap: 12px;
}

.favorites-header select {
	padding: 8px 16px;
	border: 2px solid #ddd;
	border-radius: 8px;
	font-size: 14px;
}

/* ===== Loading Spinner ===== */
.loading {
	position: fixed;
	inset: 0;
	background: rgba(255, 255, 255, 0.9);
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
	z-index: 999;
}

.spinner {
	width: 50px;
	height: 50px;
	border: 5px solid #ddd;
	border-top-color: #e74c3c;
	border-radius: 50%;
	animation: spin 0.8s linear infinite;
	margin-bottom: 16px;
}

@keyframes spin {
	to {
		transform: rotate(360deg);
	}
}

/* ===== Utilities ===== */
.hidden {
	display: none !important;
}

.no-results {
	grid-column: 1 / -1;
	text-align: center;
	padding: 60px 20px;
	color: #999;
	font-size: 18px;
}

/* ===== Footer ===== */
.footer {
	text-align: center;
	padding: 16px;
	color: #999;
	font-size: 13px;
}

.footer a {
	color: #e74c3c;
}

/* ===== Responsive ===== */
@media (max-width: 600px) {
	.header h1 {
		font-size: 1.5rem;
	}
	.search-bar {
		flex-direction: column;
	}
	.grid {
		grid-template-columns: 1fr;
	}
}
```

---

## Part 4: JavaScript — Core Logic (25 minutes)

Now build the application logic step by step.

**`app.js`:**

```javascript
// ===== DOM Elements =====
const searchForm = document.querySelector('#search-form');
const searchInput = document.querySelector('#search-input');
const searchResults = document.querySelector('#search-results');
const favoritesSection = document.querySelector('#favorites-section');
const searchSection = document.querySelector('#search-section');
const favoritesList = document.querySelector('#favorites-list');
const favCount = document.querySelector('#fav-count');
const categoryFilter = document.querySelector('#category-filter');
const modal = document.querySelector('#modal');
const modalBody = document.querySelector('#modal-body');
const modalClose = document.querySelector('.modal-close');
const loading = document.querySelector('#loading');
const tabs = document.querySelectorAll('.tab');

// ===== State =====
const API_BASE = 'https://www.themealdb.com/api/json/v1/1';
let favorites = JSON.parse(localStorage.getItem('favorites')) || [];

// ===== API Functions =====

async function searchMeals(query) {
	showLoading();
	try {
		const response = await fetch(
			`${API_BASE}/search.php?s=${encodeURIComponent(query)}`,
		);
		if (!response.ok) throw new Error('Network error');
		const data = await response.json();
		return data.meals || [];
	} catch (error) {
		console.error('Search failed:', error);
		return [];
	} finally {
		hideLoading();
	}
}

async function getMealById(id) {
	try {
		const response = await fetch(`${API_BASE}/lookup.php?i=${id}`);
		if (!response.ok) throw new Error('Network error');
		const data = await response.json();
		return data.meals ? data.meals[0] : null;
	} catch (error) {
		console.error('Lookup failed:', error);
		return null;
	}
}

// ===== Render Functions =====

function createRecipeCard(meal, isFavorite = false) {
	const saved = favorites.some((f) => f.idMeal === meal.idMeal);

	return `
    <article class="recipe-card" data-id="${meal.idMeal}">
      <img src="${meal.strMealThumb}" alt="${meal.strMeal}" loading="lazy">
      <div class="card-body">
        <h3>${meal.strMeal}</h3>
        <span class="category">${meal.strCategory || 'Uncategorized'}</span>
        <button class="fav-btn ${saved ? 'saved' : ''}"
                data-id="${meal.idMeal}"
                onclick="event.stopPropagation(); toggleFavorite('${meal.idMeal}')">
          ${saved ? '★ Saved' : '☆ Save'}
        </button>
      </div>
    </article>
  `;
}

function renderSearchResults(meals) {
	if (meals.length === 0) {
		searchResults.innerHTML =
			'<p class="no-results">No recipes found. Try a different search!</p>';
		return;
	}
	searchResults.innerHTML = meals
		.map((meal) => createRecipeCard(meal))
		.join('');
}

function renderFavorites() {
	const filter = categoryFilter.value;
	const filtered =
		filter === 'all' ? favorites : (
			favorites.filter((f) => f.strCategory === filter)
		);

	if (filtered.length === 0) {
		favoritesList.innerHTML =
			'<p class="no-results">No favorites yet. Search and save some recipes!</p>';
	} else {
		favoritesList.innerHTML = filtered
			.map((meal) => createRecipeCard(meal, true))
			.join('');
	}

	favCount.textContent = `(${favorites.length})`;
	updateCategoryFilter();
}

function updateCategoryFilter() {
	const categories = [
		...new Set(favorites.map((f) => f.strCategory).filter(Boolean)),
	];
	const current = categoryFilter.value;

	categoryFilter.innerHTML = '<option value="all">All Categories</option>';
	categories.sort().forEach((cat) => {
		categoryFilter.innerHTML += `<option value="${cat}" ${cat === current ? 'selected' : ''}>${cat}</option>`;
	});
}

// ===== Favorites Logic =====

function toggleFavorite(mealId) {
	const index = favorites.findIndex((f) => f.idMeal === mealId);

	if (index > -1) {
		// Remove from favorites
		favorites.splice(index, 1);
	} else {
		// Need to find the meal data — check search results or fetch
		const card = document.querySelector(
			`.recipe-card[data-id="${mealId}"]`,
		);
		if (card) {
			const meal = {
				idMeal: mealId,
				strMeal: card.querySelector('h3').textContent,
				strMealThumb: card.querySelector('img').src,
				strCategory: card.querySelector('.category').textContent,
			};
			favorites.push(meal);
		}
	}

	saveFavorites();
	renderFavorites();
	refreshCards();
}

function saveFavorites() {
	localStorage.setItem('favorites', JSON.stringify(favorites));
}

function refreshCards() {
	document.querySelectorAll('.fav-btn').forEach((btn) => {
		const id = btn.dataset.id;
		const saved = favorites.some((f) => f.idMeal === id);
		btn.classList.toggle('saved', saved);
		btn.textContent = saved ? '★ Saved' : '☆ Save';
	});
}

// ===== Modal (Recipe Detail) =====

function getIngredients(meal) {
	const ingredients = [];
	for (let i = 1; i <= 20; i++) {
		const ingredient = meal[`strIngredient${i}`];
		const measure = meal[`strMeasure${i}`];
		if (ingredient && ingredient.trim()) {
			ingredients.push(
				`${measure ? measure.trim() : ''} ${ingredient.trim()}`,
			);
		}
	}
	return ingredients;
}

async function showRecipeDetail(mealId) {
	showLoading();
	const meal = await getMealById(mealId);
	hideLoading();

	if (!meal) {
		alert('Could not load recipe details.');
		return;
	}

	const ingredients = getIngredients(meal);
	const saved = favorites.some((f) => f.idMeal === meal.idMeal);

	modalBody.innerHTML = `
    <img src="${meal.strMealThumb}" alt="${meal.strMeal}">
    <h2>${meal.strMeal}</h2>
    <p class="detail-category">${meal.strCategory} · ${meal.strArea || 'Unknown'}</p>

    <button class="fav-btn ${saved ? 'saved' : ''}"
            data-id="${meal.idMeal}"
            onclick="toggleFavorite('${meal.idMeal}'); this.classList.toggle('saved'); this.textContent = this.classList.contains('saved') ? '★ Saved' : '☆ Save';">
      ${saved ? '★ Saved' : '☆ Save'}
    </button>

    <h3>🧾 Ingredients</h3>
    <ul>
      ${ingredients.map((ing) => `<li>${ing}</li>`).join('')}
    </ul>

    <h3>📝 Instructions</h3>
    <p>${meal.strInstructions.replace(/\n/g, '<br>')}</p>

    ${meal.strYoutube ? `<h3>🎬 Video</h3><a href="${meal.strYoutube}" target="_blank">Watch on YouTube</a>` : ''}
  `;

	modal.classList.remove('hidden');
}

function closeModal() {
	modal.classList.add('hidden');
	modalBody.innerHTML = '';
}

// ===== Tab Navigation =====

function switchTab(tabName) {
	tabs.forEach((t) => t.classList.remove('active'));
	document.querySelector(`[data-tab="${tabName}"]`).classList.add('active');

	if (tabName === 'search') {
		searchSection.classList.remove('hidden');
		favoritesSection.classList.add('hidden');
	} else {
		searchSection.classList.add('hidden');
		favoritesSection.classList.remove('hidden');
		renderFavorites();
	}
}

// ===== Loading =====

function showLoading() {
	loading.classList.remove('hidden');
}
function hideLoading() {
	loading.classList.add('hidden');
}

// ===== Event Listeners =====

// Search form
searchForm.addEventListener('submit', async (e) => {
	e.preventDefault();
	const query = searchInput.value.trim();
	if (!query) return;

	const meals = await searchMeals(query);
	renderSearchResults(meals);
});

// Tab navigation
tabs.forEach((tab) => {
	tab.addEventListener('click', () => switchTab(tab.dataset.tab));
});

// Click on recipe card to show details (event delegation)
searchResults.addEventListener('click', (e) => {
	const card = e.target.closest('.recipe-card');
	if (card && !e.target.classList.contains('fav-btn')) {
		showRecipeDetail(card.dataset.id);
	}
});

favoritesList.addEventListener('click', (e) => {
	const card = e.target.closest('.recipe-card');
	if (card && !e.target.classList.contains('fav-btn')) {
		showRecipeDetail(card.dataset.id);
	}
});

// Close modal
modalClose.addEventListener('click', closeModal);
modal.addEventListener('click', (e) => {
	if (e.target === modal) closeModal();
});
document.addEventListener('keydown', (e) => {
	if (e.key === 'Escape') closeModal();
});

// Category filter
categoryFilter.addEventListener('change', renderFavorites);

// ===== Initialize =====
renderFavorites();
```

<details>
<summary>💡 Knowledge Check #2</summary>

**Question:** Why do we use `event.stopPropagation()` on the favorite button's click handler?

**Answer:**
The recipe card itself has a click handler (via event delegation) that opens the recipe detail modal. The favorite button is **inside** the card. Without `stopPropagation()`, clicking the favorite button would:

1. Toggle the favorite (button handler)
2. **Also** open the modal (card handler via bubbling)

`stopPropagation()` prevents the click from bubbling up to the card, so only the favorite toggle runs.

</details>

---

## Part 5: Testing & Polish (10 minutes)

### Test Checklist

Go through each feature and verify it works:

| Feature       | Test                                                  | ✅  |
| ------------- | ----------------------------------------------------- | --- |
| Search        | Type "chicken" and submit                             | ☐   |
| Results       | Cards show with image, name, category                 | ☐   |
| Details       | Click a card — modal shows ingredients + instructions | ☐   |
| Save          | Click "☆ Save" — button changes to "★ Saved"          | ☐   |
| Favorites tab | Switch to Favorites — saved recipes appear            | ☐   |
| Remove        | Click "★ Saved" again — recipe removed                | ☐   |
| Persistence   | Refresh page — favorites still there                  | ☐   |
| Filter        | Filter favorites by category                          | ☐   |
| Modal close   | Press Escape or click outside modal                   | ☐   |
| Empty state   | No favorites shows helpful message                    | ☐   |
| Error         | Disconnect internet, try searching — no crash         | ☐   |
| Responsive    | Resize browser — layout adapts                        | ☐   |

### Common Issues to Debug

```javascript
// ❌ Problem: "Cannot read property of null"
// Fix: Check that your DOM elements exist
console.log(searchForm); // Should not be null

// ❌ Problem: Favorites disappear on reload
// Fix: Check localStorage
console.log(JSON.parse(localStorage.getItem('favorites')));

// ❌ Problem: Search returns nothing
// Fix: Check the API URL and network tab
console.log(`${API_BASE}/search.php?s=chicken`);

// ❌ Problem: Modal doesn't close
// Fix: Check event listeners and class toggling
modal.classList.contains('hidden'); // should be true after close
```

---

## Part 6: Stretch Goals & Extensions (5 minutes)

If you finish early, try adding these features:

### 1. Random Recipe Button

```javascript
async function getRandomMeal() {
	showLoading();
	try {
		const response = await fetch(`${API_BASE}/random.php`);
		const data = await response.json();
		if (data.meals) {
			showRecipeDetail(data.meals[0].idMeal);
		}
	} catch (error) {
		console.error('Random meal failed:', error);
	} finally {
		hideLoading();
	}
}
```

### 2. Recipe of the Day

```javascript
// Show a random recipe when the page loads
document.addEventListener('DOMContentLoaded', async () => {
	const meals = await searchMeals('popular');
	if (meals.length > 0) {
		renderSearchResults(meals);
	}
});
```

### 3. Print/Share Recipe

```javascript
function printRecipe() {
	window.print();
}
```

### 4. Dark Mode Toggle

```javascript
function toggleDarkMode() {
	document.body.classList.toggle('dark-mode');
	localStorage.setItem(
		'darkMode',
		document.body.classList.contains('dark-mode'),
	);
}
```

---

## ⚠️ Common Mistakes

| Mistake                                   | Problem                          | Fix                                                  |
| ----------------------------------------- | -------------------------------- | ---------------------------------------------------- |
| Not encoding search query                 | Special characters break URL     | Use `encodeURIComponent(query)`                      |
| Storing full API response in localStorage | Storage limit exceeded           | Store only needed fields (id, name, image, category) |
| Not handling empty API responses          | `data.meals` is `null`, not `[]` | Check `data.meals \|\| []`                           |
| innerHTML with user data                  | XSS vulnerability                | Sanitize or use createElement                        |
| Not debouncing search                     | Fires on every keystroke         | Add debounce for real-time search                    |
| Forgetting `loading="lazy"` on images     | Slow page load                   | Add `loading="lazy"` to `<img>` tags                 |

---

## 📝 Session Summary

In this session, you built a complete interactive web app using:

1. **Project Planning** — User stories, MVP approach, file structure
2. **HTML** — Semantic structure, accessibility attributes, modal
3. **CSS** — Grid layout, animations, responsive design, custom properties
4. **DOM Manipulation** — Dynamic rendering, innerHTML, event delegation
5. **Events** — Form submit, click, keyboard, bubbling/delegation
6. **Async/Fetch** — API calls, loading/error states, data parsing
7. **Arrays & Objects** — Filter, map, find, splice, spread
8. **localStorage** — Persistent data across page reloads
9. **ES6+ Features** — Arrow functions, template literals, destructuring, modules

---

## 🏠 Homework

### Task 1: Add Your Own Feature

Choose one stretch goal from Part 6 and implement it fully.

### Task 2: Style Improvements

- Add a transition/animation when cards are added or removed
- Improve the mobile experience
- Add a color theme customizer

### Task 3: Code Review

Review your own code and answer:

- Are variable and function names descriptive?
- Is there repeated code that could be a reusable function?
- Are all edge cases handled (empty search, network error, no results)?
- Is the code well-commented?

### Bonus: Deploy Your App

- Push your project to GitHub
- Enable GitHub Pages in your repository settings
- Share the live URL!

---

## 📚 Resources

- [TheMealDB API Documentation](https://www.themealdb.com/api.php)
- [MDN: Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
- [MDN: localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)
- [MDN: Event Delegation](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Event_bubbling)
- [JavaScript.info: Fetch](https://javascript.info/fetch)
- [CSS-Tricks: A Complete Guide to Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)

---

## 🎉 Congratulations!

You've completed **Phase 2: JavaScript Fundamentals!**

Over the last 4 weeks (Sessions 19–30), you've gone from zero JavaScript knowledge to building a fully interactive web application with:

- DOM manipulation & events
- API integration with async/await
- State management with localStorage
- Clean, modular code with ES6+ features

**Next up:** Phase 3 (Weeks 11-14) — Integration, advanced patterns, and your Capstone Project!

---

**Next:** [Week 11 — Phase 3: Integration & Advanced Topics](../week-11.md) →
