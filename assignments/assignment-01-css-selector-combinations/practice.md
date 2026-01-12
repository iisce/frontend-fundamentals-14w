# Assignment 01 — CSS Selector Combinations (Practice)

Use this file as **warm-up practice** before you start the full assignment.

Goal: get comfortable combining selectors to target elements **precisely** without adding extra classes everywhere.

---

## How to use this practice

1. Open the starter HTML (you can copy/paste snippets into a scratch `index.html`).
2. Write your CSS.
3. Confirm you can explain _why_ your selector matches (or doesn’t match).

Tip: When you get stuck, add temporary outlines:

```css
* {
	outline: 1px solid rgba(255, 0, 0, 0.15);
}
```

---

## Mini Markup (use for all questions)

Paste this into a scratch HTML file:

```html
<header class="site-header">
	<a
		class="brand"
		href="#"
		>Acme</a
	>
	<nav aria-label="Primary">
		<ul class="nav">
			<li>
				<a
					href="#"
					aria-current="page"
					>Home</a
				>
			</li>
			<li><a href="#">Work</a></li>
			<li><a href="#">Contact</a></li>
		</ul>
	</nav>
</header>

<main>
	<section
		class="panel"
		data-variant="info"
	>
		<h2>Info panel</h2>
		<p>Read this first.</p>
		<p class="muted">Extra details.</p>
		<a href="#">Learn more</a>
	</section>

	<section
		class="panel"
		data-variant="warning"
	>
		<h2>Warning panel</h2>
		<p>Pay attention.</p>
		<p class="muted">More context.</p>
		<a href="#">Resolve</a>
	</section>

	<section
		class="panel"
		data-variant="success"
	>
		<h2>Success panel</h2>
		<p>Nice work.</p>
		<p class="muted">You did it.</p>
		<a href="#">Share</a>
	</section>

	<section
		class="cards"
		aria-label="Examples"
	>
		<article
			class="card"
			data-state="new"
		>
			<h3>Card A</h3>
			<p>First card.</p>
			<a href="#">Details</a>
		</article>

		<article
			class="card"
			data-state="active"
		>
			<h3>Card B</h3>
			<p>Second card.</p>
			<a href="#">Details</a>
		</article>

		<article
			class="card"
			data-state="archived"
		>
			<h3>Card C</h3>
			<p>Third card.</p>
			<a href="#">Details</a>
		</article>
	</section>

	<form
		class="signup"
		aria-label="Newsletter signup"
	>
		<h2>Newsletter</h2>

		<label>
			Email
			<input
				type="email"
				name="email"
				required
				placeholder="you@example.com"
			/>
		</label>

		<label>
			Role
			<select name="role">
				<option value="student">Student</option>
				<option value="teacher">Teacher</option>
			</select>
		</label>

		<button type="submit">Sign up</button>
		<p class="hint">We’ll never share your email.</p>
	</form>
</main>

<footer class="site-footer">
	<p>© 2026</p>
	<nav aria-label="Footer">
		<a href="#">Privacy</a>
		<a href="#">Terms</a>
	</nav>
</footer>
```

---

## Practice tasks (write the selector + the rule)

### 1) Descendant vs child

1. Make ONLY the links inside the header nav bold.
2. Make ONLY the direct children `<a>` of `.site-footer nav` use `text-decoration: underline`.

<details>
<summary>Check your thinking</summary>

-   Header links: `.site-header nav a { font-weight: 700; }`
-   Footer direct children: `.site-footer nav > a { text-decoration: underline; }`

</details>

---

### 2) Grouping and scope

Set the same `line-height` for:

-   all `.panel p`
-   all `.card p`

But do NOT affect the footer paragraph.

<details>
<summary>One possible answer</summary>

```css
.panel p,
.card p {
	line-height: 1.6;
}
```

</details>

---

### 3) Attribute selectors

1. Give panels with `data-variant="warning"` a yellow-ish border.
2. Give cards with `data-state="archived"` reduced opacity.

<details>
<summary>One possible answer</summary>

```css
.panel[data-variant='warning'] {
	border: 2px solid #d4a000;
}

.card[data-state='archived'] {
	opacity: 0.65;
}
```

</details>

---

### 4) Adjacent sibling `+`

Make the paragraph right after any `h2` inside `.panel` italic.

<details>
<summary>One possible answer</summary>

```css
.panel h2 + p {
	font-style: italic;
}
```

</details>

---

### 5) General sibling `~`

In each `.panel`, style ALL paragraphs that come after the `h2` with a slightly lighter text color.

<details>
<summary>One possible answer</summary>

```css
.panel h2 ~ p {
	color: #444;
}
```

</details>

---

### 6) Pseudo-classes

1. Add a strong focus ring to links and buttons using `:focus-visible`.
2. Style the “current page” nav link using `[aria-current="page"]`.

<details>
<summary>One possible answer</summary>

```css
:where(a, button):focus-visible {
	outline: 3px solid #1d4ed8;
	outline-offset: 3px;
}

.site-header nav a[aria-current='page'] {
	text-decoration: underline;
}
```

</details>

---

### 7) Negation `:not()`

Style `.panel a` as buttons, but NOT the links in the header or footer.

Hint: constrain your selector to `.panel`.

<details>
<summary>One possible answer</summary>

```css
.panel a:not(.brand) {
	display: inline-block;
	padding: 0.5rem 0.75rem;
	border-radius: 0.5rem;
	background: #111827;
	color: white;
	text-decoration: none;
}
```

</details>

---

### 8) Specificity check (short answer)

Which selector is more specific?

A) `.panel p.muted`
B) `.panel [class="muted"]`

<details>
<summary>Answer</summary>

A is more specific because it has **two class selectors** (0,2,0) versus B has **one class + one attribute** (0,2,0) — actually _they tie_ at (0,2,0). In a tie, the later rule in the stylesheet wins.

</details>

---

## Optional challenge

Write a selector that targets:

-   the **first** card in `.cards`
-   but only if it has `data-state="new"`

<details>
<summary>One possible answer</summary>

```css
.cards > .card:first-child[data-state='new'] {
	border: 2px dashed #16a34a;
}
```

</details>
