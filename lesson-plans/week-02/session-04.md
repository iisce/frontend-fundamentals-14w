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

## Part 1: Understanding Tables (20 minutes)

### When Should You Use Tables?

**✅ USE tables for:**

-   Data that has a clear row/column relationship
-   Price comparisons
-   Sports scores or statistics
-   Course schedules
-   Product specifications
-   Financial reports

**❌ DON'T USE tables for:**

-   Page layout (use CSS Grid or Flexbox instead)
-   Visual alignment of non-tabular content
-   Creating multi-column layouts

> **Historical Note:** In the early days of the web (1990s–2000s), developers used tables for page layout because CSS wasn't powerful enough. This is now considered a bad practice because it makes pages inaccessible and hard to maintain.

### The Anatomy of an HTML Table

Let's build a table from the ground up. Here's the simplest possible table:

```html
<table>
	<tr>
		<td>Name</td>
		<td>Age</td>
	</tr>
	<tr>
		<td>Alice</td>
		<td>25</td>
	</tr>
</table>
```

**Let's break it down:**

-   `<table>` — The container for the entire table
-   `<tr>` — Table Row (each row of data)
-   `<td>` — Table Data (an individual cell)

But wait! This table is missing crucial accessibility features. Let's improve it step-by-step.

### Step 1: Add a Caption

A `<caption>` tells everyone (especially screen reader users) what the table is about:

```html
<table>
	<caption>
		User Information
	</caption>
	<tr>
		<td>Name</td>
		<td>Age</td>
	</tr>
	<tr>
		<td>Alice</td>
		<td>25</td>
	</tr>
</table>
```

### Step 2: Use Proper Headers

Replace `<td>` with `<th>` (table header) for the first row:

```html
<table>
	<caption>
		User Information
	</caption>
	<tr>
		<th>Name</th>
		<th>Age</th>
	</tr>
	<tr>
		<td>Alice</td>
		<td>25</td>
	</tr>
</table>
```

### Step 3: Add `scope` Attributes

The `scope` attribute tells screen readers whether a header applies to a column or row:

```html
<table>
	<caption>
		User Information
	</caption>
	<tr>
		<th scope="col">Name</th>
		<th scope="col">Age</th>
	</tr>
	<tr>
		<td>Alice</td>
		<td>25</td>
	</tr>
</table>
```

### Step 4: Structure with `<thead>` and `<tbody>`

Semantic sections make tables easier to style and understand:

```html
<table>
	<caption>
		User Information
	</caption>
	<thead>
		<tr>
			<th scope="col">Name</th>
			<th scope="col">Age</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>Alice</td>
			<td>25</td>
		</tr>
		<tr>
			<td>Bob</td>
			<td>30</td>
		</tr>
	</tbody>
</table>
```

### Full Example: Pricing Table

Now let's see a complete, professional example:

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

**Notice:**

-   `<th scope="col">` for column headers (Feature, Basic, Pro, Team)
-   `<th scope="row">` for row headers (Storage, Support, Price / mo)
-   `<tfoot>` for the footer row (optional but semantic)
-   Each row has the same number of cells (4 in this case)

> **Pro Tip:** Use `scope="col"` for headers that apply to columns (vertical), and `scope="row"` for headers that apply to rows (horizontal).

---

### 🎯 Quick Practice 1

Copy the pricing table above into your `tables-practice.html` file. Open it in a browser. Do you see a table? Great!

**Now modify it:**

1. Change the caption to something else
2. Add a fourth row in `<tbody>` for "Users" (e.g., 1, 5, Unlimited)
3. Save and refresh your browser

✅ **You've just created your first accessible table!**

---

## Part 2: Making Tables Accessible (20 minutes)

Accessibility isn't an afterthought—it's built into HTML tables from the start. Let's understand why each piece matters.

### Why Captions Matter

A `<caption>` is the first thing a screen reader announces. It provides context for the entire table.

**Good caption:**

```html
<caption>
	Course enrollment statistics for Fall 2025
</caption>
```

**Bad caption (too vague):**

```html
<caption>
	Table
</caption>
```

**Bad caption (redundant with nearby heading):**

```html
<h2>Course Enrollment Statistics for Fall 2025</h2>
<table>
	<caption>
		Course Enrollment Statistics for Fall 2025
	</caption>
	<!-- Don't repeat the exact heading -->
</table>
```

**Better approach:**

```html
<h2>Course Enrollment Statistics</h2>
<table>
	<caption>
		Fall 2025 semester enrollment data
	</caption>
	<!-- Caption adds context, doesn't repeat -->
</table>
```

### Understanding `scope`

When a screen reader user navigates to a cell, it announces the associated headers. The `scope` attribute creates these associations.

**Example:** In our pricing table, when a screen reader focuses on "50 GB", it should announce:

> "Storage, Pro, 50 GB"

This happens because:

-   "Storage" has `scope="row"` (applies to the whole row)
-   "Pro" has `scope="col"` (applies to the whole column)

**Rule of thumb:**

-   `scope="col"` → Header applies to everything **below** it (in the same column)
-   `scope="row"` → Header applies to everything **to the right** of it (in the same row)

### Avoiding Merged Cells

You can merge cells with `colspan` and `rowspan`, but **avoid it unless absolutely necessary**. Merged cells make tables harder to navigate with assistive technology.

**Example of unnecessary merging:**

```html
<!-- ❌ Overly complex -->
<tr>
	<th colspan="2">Personal Info</th>
	<th colspan="2">Contact</th>
</tr>
```

**Better approach:**

```html
<!-- ✅ Keep it simple -->
<tr>
	<th scope="col">First Name</th>
	<th scope="col">Last Name</th>
	<th scope="col">Email</th>
	<th scope="col">Phone</th>
</tr>
```

### Keep Headers Concise

**Good header text:**

-   Short and descriptive
-   No full sentences
-   Clear abbreviations (with `<abbr>` if needed)

**Example:**

```html
<th scope="col">Duration<br />(weeks)</th>
<!-- Or -->
<th scope="col"><abbr title="Duration in weeks">Duration</abbr></th>
```

### Avoid Empty Cells in Headers

**Bad:**

```html
<tr>
	<th scope="col"></th>
	<!-- Empty! -->
	<th scope="col">Monday</th>
	<th scope="col">Tuesday</th>
</tr>
```

**Good:**

```html
<tr>
	<th scope="col">Time</th>
	<th scope="col">Monday</th>
	<th scope="col">Tuesday</th>
</tr>
```

---

### 🎯 Quick Practice 2

**Accessibility Check:** Review the pricing table you created. Answer these questions:

1. Does your caption describe what the table shows (not just "Table")?
2. Do all column headers have `scope="col"`?
3. Do all row headers have `scope="row"`?
4. Are there any empty header cells?

Fix any issues you find!

---

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

## Homework Assignment (30–45 minutes)

### Project: Build a Restaurant Menu Table

Create an HTML table for a restaurant menu with the following specifications:

**Data to include:**

-   At least 4 menu items
-   Columns: Item Name, Description, Price, Calories, Dietary Info

**Example data:**
| Item Name | Description | Price | Calories | Dietary |
|-----------|-------------|-------|----------|---------|
| Caesar Salad | Romaine lettuce, parmesan, croutons | $8.99 | 350 | Vegetarian |
| Grilled Chicken | Herb-marinated chicken breast with vegetables | $14.99 | 420 | Gluten-Free |
| Margherita Pizza | Fresh mozzarella, basil, tomato sauce | $12.99 | 680 | Vegetarian |
| Fish Tacos | Grilled fish, cabbage slaw, chipotle mayo | $11.99 | 520 | - |

### Requirements Checklist

Your submission must include:

-   [ ] A complete HTML file (with `<!DOCTYPE html>`, `<head>`, `<body>`)
-   [ ] A descriptive `<caption>` (e.g., "Lunch menu for [Restaurant Name]")
-   [ ] Column headers using `<th scope="col">`
-   [ ] Row headers (Item Name) using `<th scope="row">`
-   [ ] Properly structured with `<thead>` and `<tbody>`
-   [ ] At least 4 menu items (rows of data)
-   [ ] All rows have the same number of cells
-   [ ] No empty header cells
-   [ ] Optional: Basic CSS for readability

### Submission

Save your file as `menu-table.html` and test it in your browser.

**Self-grading questions:**

1. Can you understand the table without looking at the visual layout?
2. Would a screen reader user know what each cell represents?
3. Are all your headers properly marked up with `<th>` and `scope`?

---

## Bonus Assignment: Class Schedule Table (30–45 minutes)

### Project: Build a Weekly Class Schedule

Create an HTML table that displays a weekly class schedule with the following specifications:

**Data to include:**

-   At least 5 time slots (e.g., 9:00 AM, 10:00 AM, 11:00 AM, etc.)
-   Columns for Monday through Friday
-   Class names with room numbers

**Example data:**
| Time | Monday | Tuesday | Wednesday | Thursday | Friday |
|----------|-------------|-------------|-------------|-------------|-------------|
| 9:00 AM | Math 101<br>Room 204 | Chemistry<br>Lab A | Math 101<br>Room 204 | Chemistry<br>Lab A | Free |
| 10:00 AM | English<br>Room 115 | Free | English<br>Room 115 | Free | Computer Lab |
| 11:00 AM | Physics<br>Room 301 | History<br>Room 220 | Physics<br>Room 301 | History<br>Room 220 | Free |

### Requirements Checklist

Your submission must include:

-   [ ] A complete HTML file with proper document structure
-   [ ] A descriptive `<caption>` (e.g., "Fall 2025 Weekly Class Schedule")
-   [ ] Column headers for each day using `<th scope="col">`
-   [ ] Row headers for time slots using `<th scope="row">`
-   [ ] Properly structured with `<thead>` and `<tbody>`
-   [ ] At least 5 time slots (rows)
-   [ ] All 5 weekdays represented (columns)
-   [ ] Use `<br>` tags to separate class name and room number within cells
-   [ ] Indicate "Free" or "Break" for empty time slots (no blank cells)
-   [ ] Optional: Use `<tfoot>` for a summary row (e.g., "Total classes: 12")

### Submission

Save your file as `class-schedule.html` and test it in your browser.

**Self-grading questions:**

1. Does your table clearly show when and where each class meets?
2. Are time slots properly marked as row headers with `scope="row"`?
3. Are weekday names properly marked as column headers with `scope="col"`?
4. Would a screen reader user be able to understand "Physics at 11:00 AM on Monday in Room 301"?

### Bonus Challenge (Optional)

-   Add a `<tfoot>` section showing total hours of class per day
-   Style the table with CSS to use different background colors for different subjects
-   Use `colspan` to show a lunch break that spans all weekdays (e.g., 12:00 PM - 1:00 PM)

---

## Troubleshooting Guide

### Problem: Headers aren't visually distinct

**Cause:** Browsers apply minimal default styling.

**Solution:** Add CSS to make headers bold and add background color:

```css
th {
	font-weight: bold;
	background-color: #f0f0f0;
}
```

### Problem: Screen reader doesn't announce headers

**Cause:** You're using `<td>` instead of `<th>`, or missing `scope` attribute.

**Solution:**

1. Check that header cells use `<th>`, not `<td>`
2. Add `scope="col"` or `scope="row"` to all `<th>` elements

### Problem: Table cells are misaligned

**Cause:** Rows have different numbers of cells.

**Solution:** Count the cells in each row. They should all have the same number. If you have 5 column headers, every row should have 5 cells.

### Problem: Table is too wide for mobile screens

**Cause:** Tables with many columns can overflow on small screens.

**Solution (advanced):**

-   Use CSS to make the table scrollable: `overflow-x: auto;`
-   Or consider a responsive design pattern (beyond this lesson's scope)

---

## Congratulations! 🎉

You've completed the Tables and Tabular Data tutorial! You now know:

✅ When to use tables (and when to avoid them)
✅ How to structure tables with semantic HTML
✅ How to make tables accessible with `scope`, headers, and captions
✅ Best practices for creating usable tables

**Next Steps:**

-   Practice by creating tables from real-world data
-   Move on to Session 05: Forms I — Inputs and Labels
-   Explore advanced table features like `<colgroup>` and complex headers

**Additional Learning Resources:**

-   [MDN: Advanced Tables](https://developer.mozilla.org/docs/Learn/HTML/Tables/Advanced)
-   [WebAIM: Creating Accessible Tables](https://webaim.org/techniques/tables/)
-   [A11ycasts: Accessible Tables](https://www.youtube.com/watch?v=RKmmaDp-Cu8)

---

Navigation

-   Back: ../learning-plan.md
-   Week 02 Index: ../week-02.md
-   Prev: ../week-01/session-03.md
-   Next: session-05.md
