# Week 02 — Session 04: Tables and Tabular Data

Navigation

-   Back to Learning Plan: ../learning-plan.md
-   Week 02 Index: ../week-02.md
-   Prev: ../week-01/session-03.md
-   Next: session-05.md

Session length: 90 minutes

Pre-class checklist

-   Skim MDN’s table guide (links below)
-   Bring a small CSV-like dataset (3–5 columns, ~5–10 rows)

Learning objectives

-   Structure tabular data with `<table>`, `<caption>`, `<thead>`, `<tbody>`, `<tfoot>`
-   Use `<th scope>` and captions for accessible tables
-   Decide when not to use tables (layout belongs to CSS)

Materials

-   MDN: HTML tables — [MDN Tables Basics](https://developer.mozilla.org/docs/Learn/HTML/Tables/Basics)
-   WAI: Tables — [WAI Tables Tutorial](https://www.w3.org/WAI/tutorials/tables/)

Key terms

-   table, caption, thead, tbody, tfoot, tr, th, td, scope, colgroup, col

You will build

-   A pricing/features table with row and column headers, and a clear caption

## 1) Tables 101 (20m)

-   When to use a table: only for data with a row/column relationship
-   Avoid using tables for page layout; use CSS instead
-   Anatomy and minimal semantic example:

```html
<table>
	<caption>
		Pricing plans comparison
	</caption>
	<thead>
		<tr>
			<th scope="col">Feature</th>
			<th scope="col">Basic</th>
			<th scope="col">Pro</th>
			<th scope="col">Team</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th scope="row">Storage</th>
			<td>5 GB</td>
			<td>50 GB</td>
			<td>200 GB</td>
		</tr>
		<tr>
			<th scope="row">Support</th>
			<td>Email</td>
			<td>Email + Chat</td>
			<td>Priority</td>
		</tr>
	</tbody>
	<tfoot>
		<tr>
			<th scope="row">Price / mo</th>
			<td>$0</td>
			<td>$9</td>
			<td>$29</td>
		</tr>
	</tfoot>
</table>
```

Notes

-   Use `<th scope="col">` for column headers and `<th scope="row">` for row headers.
-   Prefer `scope` for simple tables; for highly complex tables, use the `id`/`headers` technique.

## 2) Accessibility in tables (20m)

-   Captions provide context for the whole table (don’t repeat the surrounding heading verbatim)
-   Don’t merge cells unless necessary; merged cells complicate associations
-   Keep header text concise and descriptive; avoid empty cells in header rows/columns

## 3) Guided lab (40m)

Goal: Build a 3×4 pricing table with a caption and proper headers.

Steps

1. Create a `<table>` with `<caption>Pricing plans comparison</caption>`
2. Add a header row with plan names using `<th scope="col">`
3. Add at least three feature rows with `<th scope="row">`
4. Fill in cells with realistic values
5. Add a footer row showing the monthly price

Deliverable: an HTML snippet (no CSS required yet) that renders a readable, accessible table.

Checklist

-   [ ] Has `<caption>` describing the table’s purpose
-   [ ] Uses `<th scope="col">` and `<th scope="row">` correctly
-   [ ] No layout misuse (table is for data, not page layout)
-   [ ] Reasonable text content (no placeholder lorem)

Knowledge checks

-   Q: When do you use `scope="row"` vs `scope="col"`?
-   Q: Why do we add a `<caption>` even if a nearby heading describes the section?

Common pitfalls

-   Using `<td>` for headers (screen readers won’t treat them as headers)
-   Leaving off `<caption>` and relying only on visual context
-   Overusing merged cells, which harms navigability

Homework (30–45 minutes)

-   Exercise: Convert a CSV-like list into an accessible HTML table.
-   Acceptance criteria:
    -   [ ] Includes `<caption>` that describes the dataset
    -   [ ] First row uses `<th scope="col">`
    -   [ ] First cell in each data row uses `<th scope="row">`
    -   [ ] No tables for layout; only to present tabular data

Troubleshooting

-   Headers not announced? Check that you used `<th>` with the correct `scope`.
-   Misaligned cells? Ensure each row has the same number of cells and consistent structure.

Navigation

-   Back: ../learning-plan.md
-   Week 02 Index: ../week-02.md
-   Prev: ../week-01/session-03.md
-   Next: session-05.md
