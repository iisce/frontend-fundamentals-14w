# Week 01 — Session 03: Structure and Semantics

Navigation

-   Back to Learning Plan: ../learning-plan.md
-   Week 01 Index: ../week-01.md
-   Prev: session-02.md
-   Next: ../week-01.md (end of week)

Session length: 90 minutes

Materials

-   Project scaffold: ../../templates/project-scaffold/index.html
-   Setup guide: ../../resources/setup.md

Pre-class checklist

-   Open your article page from Session 02
-   Ensure Live Server is running

Learning objectives

-   Apply semantic HTML5 layout elements (header, nav, main, section, article, aside, footer)
-   Understand basic accessibility concepts and landmarks
-   Use DevTools to inspect structure and landmarks

Key terms

-   Landmarks, semantics, accessibility, headings outline, ARIA (at a glance)

You will build

-   A structured blog-style homepage using semantic layout elements

Success criteria (what “good” looks like)

-   One and only one `<main>` landmark on the page
-   Logical heading outline (one `<h1>`, nested `<h2>`/`<h3>` with no skipped levels)
-   Primary navigation inside `<nav>`; links have descriptive text
-   Content grouped in `<section>` and standalone posts in `<article>`
-   An `<aside>` contains supplementary content only

## 1) Semantic Layout Elements (25 minutes)

Semantic elements describe their meaning to both the browser and the developer. They act as a blueprint for your page, making it more accessible and easier to maintain. These elements are called **landmarks**, which allow assistive technologies (like screen readers) to navigate your page efficiently.

-   **`<header>`**: The introductory content for a page or a section. It often contains the site logo, title, and main navigation.
-   **`<nav>`**: Contains major navigation links. It's for the primary ways a user will move around your site.
-   **`<main>`**: The main, unique content of the page. There should only be **one** `<main>` element per page.
-   **`<section>`**: A thematic grouping of content. Think of it as a chapter in a book. It should almost always have a heading.
-   **`<article>`**: A self-contained piece of content that could be distributed on its own (e.g., a blog post, a news story, a forum comment).
-   **`<aside>`**: For supplementary content that is related to the main content but can be considered separate (e.g., a sidebar with related links, an author bio).
-   **`<footer>`**: The closing content for a page or section. It typically contains copyright info, contact details, or secondary navigation.

**When to use `<section>` vs. `<article>`?**

-   Use `<article>` if the content makes sense on its own (like a blog post).
-   Use `<section>` to group related parts of a page (like "Latest Posts" or "Contact Information"). An `<article>` can contain `<section>`s, and a `<section>` can contain `<article>`s.

**Example:**

```html
<body>
	<header>
		<h1>My Awesome Blog</h1>
		<nav>
			<ul>
				<li><a href="/">Home</a></li>
				<li><a href="/about">About</a></li>
			</ul>
		</nav>
	</header>

	<main>
		<article>
			<h2>My First Blog Post</h2>
			<p>This is the content of my post...</p>
			<section>
				<h3>Comments</h3>
				<p>This is a comment.</p>
			</section>
		</article>
	</main>

	<aside>
		<h3>Related Posts</h3>
		<ul>
			<li><a href="/post-2">Another Post</a></li>
		</ul>
	</aside>

	<footer>
		<p>&copy; 2025 My Awesome Blog</p>
	</footer>
</body>
```

## 2) Accessibility Basics (20 minutes)

Accessibility (often shortened to a11y) is the practice of making your websites usable by as many people as possible, including those with disabilities.

-   Landmarks: Semantic elements like `<main>`, `<nav>`, and `<footer>` create landmarks. Screen reader users can jump directly between landmarks.
-   Headings outline: A logical heading structure (`<h1>` → `<h2>` → `<h3>`) acts like a table of contents. Never skip heading levels.
-   Meaningful links: Link text should make sense out of context (avoid “Click here”).
-   Keyboard navigation: Ensure users can tab through links and controls in a logical order. Visible focus styles help everyone.

Skip link (improves keyboard navigation)

```html
<!-- Put this as the first focusable element inside <body> -->
<a
	href="#main-content"
	class="visually-hidden-focusable"
	>Skip to main content</a
>

<main id="main-content">
	<!-- Main content -->
</main>
```

```css
/* In your CSS */
.visually-hidden-focusable {
	position: absolute;
	left: -9999px;
	top: auto;
	width: 1px;
	height: 1px;
	overflow: hidden;
}
.visually-hidden-focusable:focus {
	left: 1rem;
	top: 1rem;
	width: auto;
	height: auto;
	padding: 0.5rem 0.75rem;
	background: #000;
	color: #fff;
	z-index: 1000;
}
```

## 3) DevTools Elements Panel Tour (10 minutes)

Do a quick pass to validate structure and landmarks:

1. Open DevTools (F12) → Elements.
2. Hover elements to see layout regions; confirm only one `<main>`.
3. Right-click a node → Inspect Accessibility Properties (or use the Accessibility pane) to view:
    - Role (e.g., navigation, main, contentinfo)
    - Name (e.g., from a heading or aria-label)
    - Keyboard focus order
4. Edit text/content live to try alternative headings and confirm outline impact.

Guided lab (25–30 minutes)

Goal: Add semantic structure to your article page and validate it with DevTools.

Step-by-step

1. Wrap existing content in a `<main id="main-content">` and add a `<header>` and `<footer>`.
2. Add a `<nav>` with links to page sections (e.g., `#latest`, `#about`).
3. Group related content into `<section>`; use `<article>` for standalone content (e.g., posts).
4. Add an `<aside>` with supplementary info (e.g., author bio or related links).
5. Add a skip link to jump to `#main-content`.
6. Open DevTools → Accessibility to confirm landmarks and headings.

Starter skeleton

```html
<body>
	<header>
		<h1>My Blog</h1>
		<nav>
			<a href="#latest">Latest</a>
			<a href="#about">About</a>
		</nav>
	</header>
	<a
		href="#main-content"
		class="visually-hidden-focusable"
		>Skip to main content</a
	>
	<main id="main-content">
		<section id="latest">
			<article>
				<h2>Post title</h2>
				<p>...</p>
			</article>
		</section>
		<aside>
			<h2>About the author</h2>
			<p>...</p>
		</aside>
	</main>
	<footer>
		<small>&copy; <span id="year"></span></small>
	</footer>
</body>
```

Acceptance criteria

-   One `<main>`; `<header>`, `<nav>`, `<footer>` present and correctly placed
-   Headings meaningful and ordered (no skipped levels)
-   At least one in-page nav link; skip link present and works
-   Landmarks appear correctly in DevTools Accessibility pane

Rubric (self-check)

-   2 pts: Correct landmarks and structure
-   2 pts: Clear, accessible headings and link text
-   1 pt: Skip link implemented and focusable
-   1 pt: DevTools verification notes (1–2 sentences)

Knowledge checks

-   Q: When should you use `<section>` vs `<article>`?
-   Q: Why are landmarks helpful for assistive technologies?

Homework (30–60 minutes)

-   Exercise: Add semantic structure to your article page from Session 02.
-   Acceptance criteria:
    -   [ ] One `<main>`; appropriate use of header/nav/section/article/aside/footer
    -   [ ] Headings are meaningful and ordered
    -   [ ] At least one in-page nav link; optional skip link

Stretch goals (optional)

-   Add a visually hidden “Skip to content” link that targets `#main-content`

Troubleshooting

-   If landmarks don’t appear in the accessibility pane, validate your HTML structure
-   Heading jumps (e.g., h1 → h4) indicate outline issues — adjust levels

Navigation

-   Prev: session-02.md
-   Next: ../week-01.md
