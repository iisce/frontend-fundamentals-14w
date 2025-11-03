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

## 2) Headings and paragraphs (15 minutes)

-   One `<h1>` per page; subsequent sections use `<h2>`/`<h3>`
-   Keep paragraphs short and meaningful

## 3) Lists and emphasis (20 minutes)

-   `<ul>` vs `<ol>`; nesting lists
-   `<em>` and `<strong>` for meaning (not just visual styling)

## 4) Links (15 minutes)

-   Absolute URLs vs relative paths
-   Descriptive link text; avoid "click here"

## 5) Images (15 minutes)

-   `<img src="..." alt="...">` basics
-   When to use empty alt (decorative images only)
-   Image formats and sizing tips

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
