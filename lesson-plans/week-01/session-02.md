# Week 01 — Session 02: Text and Media

Navigation

-   Back to Learning Plan: ../learning-plan.md
-   Week 01 Index: ../week-01.md
-   Prev: session-01.md
-   Next: session-03.md

Session length: 90 minutes

Materials

-   Project scaffold: ../../templates/project-scaffold/index.html
-   Setup guide: ../../resources/setup.md

Pre-class checklist

-   Open your project scaffold at: ../../templates/project-scaffold/index.html
-   Ensure Live Server is running

Learning objectives

-   Use headings, paragraphs, emphasis, and links correctly
-   Create lists (ordered and unordered) with semantic structure
-   Embed images with meaningful alt text and understand file paths

Key terms

-   Relative vs absolute paths, alt text, semantic, anchor, list item

You will build

-   A content-rich article page with headings, lists, links, and images

## 1) Review (10 minutes)

-   Check setup, discuss homework highlights, clarify questions

## 2) Headings and Paragraphs (15 minutes)

Headings structure your content, acting like a table of contents for the page. Search engines and screen readers use them to understand your document's organization.

-   **`<h1>`**: The main title of your page. You should only have **one** `<h1>` per page for accessibility and SEO.
-   **`<h2>` to `<h6>`**: Subheadings for sections and sub-sections. Always use them in order without skipping levels (e.g., `<h2>` -> `<h3>`, not `<h2>` -> `<h4>`).

Paragraphs (`<p>`) are for blocks of text. Browsers automatically add space before and after paragraphs, making text easier to read.

**Example:**

```html
<h1>My Awesome Article</h1>
<p>
	This is the introduction to my article. It gives a brief overview of what I
	will discuss.
</p>

<h2>Section 1: The Beginning</h2>
<p>
	Here is the content for the first section. It's wrapped in a paragraph tag.
</p>

<h3>Subsection 1.1</h3>
<p>More detailed information goes here, also in a paragraph.</p>
```

## 3) Lists and Emphasis (20 minutes)

Lists are perfect for grouping related items, and HTML gives us a few types.

-   **`<ul>` (Unordered List)**: Use for items where the order doesn't matter. It creates a bulleted list.
-   **`</ol><ol>` (Ordered List)**: Use when the sequence is important, like steps in a recipe. It creates a numbered list.
-   **`<li>` (List Item)**: The tag for each item inside a `<ul>` or `<ol>`.

**Emphasis** tags add meaning to your text, not just style.

-   **`<strong>`**: Indicates that the text is important (e.g., a warning). Browsers display this as bold by default.
-   **`<em>`**: Adds stress emphasis to a word or phrase, changing the meaning of the sentence. Browsers display this as italic by default.

**Example:**

```html
<h2>My Grocery List</h2>
<ul>
	<li>Milk</li>
	<li>Bread</li>
	<li>Cheese</li>
</ul>

<h2>How to Make Tea</h2>
<ol>
	<li>Boil water.</li>
	<li>Place tea bag in cup.</li>
	<li>Pour boiling water into cup.</li>
</ol>

<p>
	<strong>Warning:</strong> Do not touch the hot stove. You <em>must</em> be
	careful.
</p>
```

## 4) Links (15 minutes)

Links (`<a>`, for "anchor") are what connect the web. A link needs an `href` attribute to know where to go.

-   **Absolute URLs**: A full web address to another site (e.g., `https://www.google.com`). Use this for external links.
-   **Relative Paths**: A path to a file within your own project. It's "relative" to the current file's location.
    -   `./contact.html`: Links to `contact.html` in the same folder.
    -   `../images/photo.jpg`: Goes up one folder, then into the `images` folder.
-   **Hash Links**: A link to another section on the same page. It points to an element's `id`.

**Link Text**: The text inside the `<a>` tag should be descriptive. Avoid "click here" because it's not accessible to screen reader users.

**Example:**

```html
<!-- Absolute URL -->
<p>
	Visit the <a href="https://developer.mozilla.org/">MDN Web Docs</a> for more
	info.
</p>

<!-- Relative Path -->
<p>Check out our <a href="./pages/about.html">About Us</a> page.</p>

<!-- Hash Link -->
<p><a href="#top">Back to top</a></p>
```

## 5) Images (15 minutes)

Images (`<img>`) bring life to your page. They are self-closing and require two main attributes:

-   **`src` (Source)**: The path to the image file. This can be a relative path or an absolute URL.
-   **`alt` (Alternative Text)**: A description of the image. This is crucial for accessibility (for screen readers) and for SEO. It also displays if the image fails to load.

**When should `alt` be empty?**
If an image is purely decorative and adds no meaning, you can use an empty `alt=""`. This tells screen readers to ignore it.

**Example:**

```html
<!-- Image with meaningful alt text -->
<img
	src="../images/dog.jpg"
	alt="A golden retriever puppy playing in a field."
/>

<!-- Decorative image -->
<img
	src="../images/blue-line-divider.png"
	alt=""
/>
```

Guided lab (25–30 minutes)

Goal: Convert a plain-text article into HTML with:

-   Title and section headings
-   At least one unordered list and one ordered list
-   3+ links (1 absolute, 1 relative, 1 hash link)
-   1+ image with meaningful alt text

Starter snippet

```html
<h1>The Joy of Learning the Web</h1>
<p>...</p>
<h2>Why HTML Matters</h2>
<p>...</p>
<h2 id="resources">Resources</h2>
<ul>
	<li><a href="https://developer.mozilla.org/">MDN Web Docs</a></li>
	<li><a href="#top">Back to top</a></li>
</ul>
```

Checklist

-   [ ] Single `<h1>` and logical heading order
-   [ ] Lists are valid (`<ul>/<ol>` with `<li>`) and nested correctly
-   [ ] Links have descriptive text; paths verified
-   [ ] Images include meaningful alt text

Knowledge checks

-   Q: When should alt be empty?
-   Q: What is the difference between relative and absolute paths?

Homework (30–60 minutes)

-   Exercise: Convert a text document into HTML with headings, lists, links, and images. Use the scaffold in ../../templates/project-scaffold/.
-   Acceptance criteria:
    -   [ ] Valid HTML5 structure
    -   [ ] At least two lists
    -   [ ] At least three links (absolute, relative/hash)
    -   [ ] At least one image with non-empty alt text (unless decorative)

Troubleshooting

-   Broken images: check file paths and file extensions
-   Link paths: use `./` for same folder and `../` to go up one level

Navigation

-   Prev: session-01.md
-   Next: session-03.md
