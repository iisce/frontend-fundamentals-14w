# HTML Tables Quick Reference

## Basic Structure

```html
<table>
	<caption>
		Description of the table
	</caption>
	<thead>
		<tr>
			<th scope="col">Header 1</th>
			<th scope="col">Header 2</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th scope="row">Row Header</th>
			<td>Data</td>
		</tr>
	</tbody>
	<tfoot>
		<tr>
			<th scope="row">Footer Header</th>
			<td>Footer Data</td>
		</tr>
	</tfoot>
</table>
```

## Essential Elements

| Element     | Purpose                    | Required?          |
| ----------- | -------------------------- | ------------------ |
| `<table>`   | Container for entire table | Yes                |
| `<caption>` | Describes table's purpose  | Highly recommended |
| `<thead>`   | Groups header rows         | Recommended        |
| `<tbody>`   | Groups data rows           | Recommended        |
| `<tfoot>`   | Groups footer rows         | Optional           |
| `<tr>`      | Table row                  | Yes                |
| `<th>`      | Header cell                | For headers        |
| `<td>`      | Data cell                  | For data           |

## The `scope` Attribute

Use `scope` on `<th>` elements to define what the header applies to:

-   `scope="col"` → Header applies to the column below it
-   `scope="row"` → Header applies to the row to its right
-   `scope="colgroup"` → Header applies to a group of columns (advanced)
-   `scope="rowgroup"` → Header applies to a group of rows (advanced)

### Example: Column Headers

```html
<thead>
	<tr>
		<th scope="col">Product</th>
		<th scope="col">Price</th>
		<th scope="col">Stock</th>
	</tr>
</thead>
```

### Example: Row Headers

```html
<tbody>
	<tr>
		<th scope="row">Laptop</th>
		<td>$999</td>
		<td>15</td>
	</tr>
	<tr>
		<th scope="row">Mouse</th>
		<td>$29</td>
		<td>47</td>
	</tr>
</tbody>
```

## Common Patterns

### Pattern 1: Simple Data Table

```html
<table>
	<caption>
		Employee Directory
	</caption>
	<thead>
		<tr>
			<th scope="col">Name</th>
			<th scope="col">Department</th>
			<th scope="col">Email</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>Alice Chen</td>
			<td>Engineering</td>
			<td>alice@example.com</td>
		</tr>
		<!-- More rows... -->
	</tbody>
</table>
```

### Pattern 2: Table with Row and Column Headers

```html
<table>
	<caption>
		Q3 Sales by Region
	</caption>
	<thead>
		<tr>
			<th scope="col">Region</th>
			<th scope="col">July</th>
			<th scope="col">August</th>
			<th scope="col">September</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th scope="row">North</th>
			<td>$45,000</td>
			<td>$52,000</td>
			<td>$48,000</td>
		</tr>
		<tr>
			<th scope="row">South</th>
			<td>$38,000</td>
			<td>$41,000</td>
			<td>$44,000</td>
		</tr>
	</tbody>
</table>
```

### Pattern 3: Table with Footer

```html
<table>
	<caption>
		Monthly Expenses
	</caption>
	<thead>
		<tr>
			<th scope="col">Category</th>
			<th scope="col">Amount</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th scope="row">Rent</th>
			<td>$1,200</td>
		</tr>
		<tr>
			<th scope="row">Utilities</th>
			<td>$150</td>
		</tr>
	</tbody>
	<tfoot>
		<tr>
			<th scope="row">Total</th>
			<td>$1,350</td>
		</tr>
	</tfoot>
</table>
```

## Accessibility Checklist

✅ **DO:**

-   Use `<caption>` to describe the table
-   Use `<th>` for all headers (not `<td>`)
-   Add `scope` attribute to all `<th>` elements
-   Structure with `<thead>`, `<tbody>`, `<tfoot>`
-   Keep headers concise and descriptive
-   Ensure each row has the same number of cells
-   Use tables only for tabular data

❌ **DON'T:**

-   Use tables for page layout
-   Leave captions blank or vague
-   Use `<td>` for headers
-   Merge cells unnecessarily (`colspan`, `rowspan`)
-   Create empty header cells
-   Nest tables inside tables (rarely needed)

## Basic Styling (CSS)

```css
/* Make table easier to read */
table {
	border-collapse: collapse;
	width: 100%;
}

th,
td {
	border: 1px solid #ddd;
	padding: 8px;
	text-align: left;
}

/* Style headers */
thead {
	background-color: #f2f2f2;
	font-weight: bold;
}

/* Alternate row colors */
tbody tr:nth-child(even) {
	background-color: #f9f9f9;
}

/* Hover effect */
tbody tr:hover {
	background-color: #e9e9e9;
}

/* Caption styling */
caption {
	font-weight: bold;
	margin-bottom: 10px;
	text-align: left;
}
```

## When to Use Tables

### ✅ Good Uses

-   Spreadsheet-like data
-   Comparison charts (products, prices, features)
-   Schedules and timetables
-   Statistical data
-   Financial reports
-   Sports scores/standings

### ❌ Bad Uses (Use CSS Instead)

-   Multi-column page layouts
-   Image galleries
-   Navigation menus
-   Form layouts
-   Card/grid displays

## Common Mistakes

### Mistake 1: Missing Caption

```html
<!-- ❌ Bad -->
<table>
	<thead>
		...
	</thead>
</table>

<!-- ✅ Good -->
<table>
	<caption>
		User List
	</caption>
	<thead>
		...
	</thead>
</table>
```

### Mistake 2: Using `<td>` for Headers

```html
<!-- ❌ Bad -->
<tr>
	<td>Name</td>
	<td>Age</td>
</tr>

<!-- ✅ Good -->
<tr>
	<th scope="col">Name</th>
	<th scope="col">Age</th>
</tr>
```

### Mistake 3: Inconsistent Cell Count

```html
<!-- ❌ Bad -->
<tr>
	<th scope="col">A</th>
	<th scope="col">B</th>
	<th scope="col">C</th>
</tr>
<tr>
	<td>1</td>
	<td>2</td>
	<!-- Missing third cell! -->
</tr>

<!-- ✅ Good -->
<tr>
	<td>1</td>
	<td>2</td>
	<td>3</td>
</tr>
```

## Resources

-   [MDN: HTML Tables](https://developer.mozilla.org/docs/Learn/HTML/Tables)
-   [W3C: Tables Tutorial](https://www.w3.org/WAI/tutorials/tables/)
-   [WebAIM: Creating Accessible Tables](https://webaim.org/techniques/tables/)

---

**Quick Test:** Can you create a table with 3 columns and 4 rows, including proper headers and a caption? Try it!
