# Week 01 — Session 01: Introduction + HTML Basics

Navigation
- Back to Learning Plan: ../learning-plan.md
- Week 01 Index: ../week-01.md
- Next: session-02.md

Session length: 90 minutes

Pre-class checklist
- Install VS Code, Node.js LTS, Git (see ../../resources/setup.md)
- Open templates/project-scaffold/index.html with Live Server

Learning objectives
- Understand how the web works at a high level (request/response, files)
- Author a minimal, valid HTML5 document
- Use core content tags: headings, paragraphs, lists, links

Key terms
- Client, server, HTTP, HTML, head, body, semantic, element, attribute

You will build
- A simple “Hello, Web!” page with headings, lists, and links

1) The web in 10 minutes
- A browser (client) requests a document from a server (via HTTP)
- The server returns HTML; the browser parses HTML and loads linked assets (CSS, JS, images)
- Files and paths matter: relative vs absolute URLs, folder structure

2) Start a minimal HTML document
Create index.html if it doesn’t exist. Use this skeleton:

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>Hello, Web!</title>
  </head>
  <body>
    <h1>Hello, Web!</h1>
    <p>This is my first page.</p>
  </body>
</html>
```

3) Content fundamentals
- Headings: h1 is the page title; use h2–h3 for sections and subsections.
- Paragraphs: wrap text in <p>.
- Lists: use <ul>/<ol> with <li> items.
- Emphasis: <em> and <strong> convey meaning to assistive tech.

Add content step-by-step:

```html
<h2>About this site</h2>
<p>I'm learning front-end development.</p>

<h2>Links</h2>
<ul>
  <li><a href="https://developer.mozilla.org/">MDN Web Docs</a></li>
  <li><a href="#contact">Contact me</a></li>
</ul>

<h2 id="contact">Contact</h2>
<p>Email me at <a href="mailto:you@example.com">you@example.com</a></p>
```

4) Links and paths
- Absolute URL: starts with https:// and points anywhere on the web.
- Relative path: points to a file in your project, e.g., ./images/logo.png
- Hash link: jumps to an element with a matching id on the same page.

5) DevTools quick tour
- Right-click → Inspect → Elements panel
- Edit text live; see how the DOM reflects your HTML

Guided lab (25–30 minutes)
Goal: Build a one-page personal intro with:
- Title (h1), section headings (h2), paragraphs, a list of links
- One internal hash link (e.g., “Back to top”)
- A mailto link

Checklist
- [ ] Single h1
- [ ] Logical heading order
- [ ] At least one list
- [ ] At least two links (one absolute, one mailto or hash)

Knowledge checks
- Q: What belongs in <head> vs <body>?
- Q: Why is semantic structure better than “just styling” text?

Common pitfalls
- Multiple h1s without need, missing meta viewport, missing lang attribute
- Unclear link text like “click here”—prefer descriptive text

Homework (30–60 minutes)
- Exercise: Recreate a short article page (headings, paragraphs, links). Use the scaffold in ../../templates/project-scaffold/.
- Acceptance criteria:
  - [ ] Valid HTML5 structure with lang and meta viewport
  - [ ] Meaningful headings and link text
  - [ ] No empty links or placeholder “#” unless it’s an intentional in-page jump
- Reading: MDN “HTML: HyperText Markup Language” overview

Stretch goals (optional)
- Add a small nav section at the top linking to the page sections
- Add a footer with the current year

Troubleshooting
- If Live Server doesn’t reload, ensure the file is saved and the server points to the correct folder.
- If links fail, check your paths: use ./ for current folder; ../ to go up one level.

Navigation
- Back: ../learning-plan.md
- Next: session-02.md