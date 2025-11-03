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

## 1) Semantic layout elements (25 minutes)

-   `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>`, `<footer>`
-   When to use section vs article; nesting rules and headings

## 2) Accessibility basics (20 minutes)

-   Landmarks and keyboard navigation
-   Meaningful headings and label relationships
-   Color contrast and link focus styles (preview only; deeper later)

## 3) DevTools Elements panel tour (10 minutes)

-   Inspect elements; view accessibility tree
-   Quick edits and structure validation

Guided lab (25–30 minutes)

Goal: Add semantic structure to your article page:

-   Wrap content with `<main>` and add a `<header>` and `<footer>`
-   Add a `<nav>` with in-page links
-   Group related content into `<section>`; use `<article>` for standalone content
-   Include an `<aside>` for supplementary content (e.g., author bio)

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

Checklist

-   [ ] Proper landmarks with one `<main>` per page
-   [ ] Logical heading outline (one `<h1>`, nested `<h2>`/`<h3>`)
-   [ ] Navigation links work and are descriptive
-   [ ] Optional: Skip link to main content

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
