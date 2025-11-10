# Week 02 Session Files

This folder contains materials for Week 02 sessions covering HTML tables and forms (Sessions 04-06).

## 📑 Quick Navigation

-   **[Session 04: Tables and Tabular Data](#-session-04-tables-and-tabular-data)** - Self-guided tutorial
-   **[Session 05: Forms I — Inputs and Labels](#-session-05-forms-i--inputs-and-labels)** - Self-guided tutorial
-   **[Session 06: Forms II — Validation & Accessibility](#-session-06-forms-ii--validation--accessibility)** - Self-guided tutorial

## 📦 All Files in This Folder

| File                             | Type        | Related Session | Purpose                               |
| -------------------------------- | ----------- | --------------- | ------------------------------------- |
| `session-04.md`                  | Tutorial    | Session 04      | Self-guided HTML tables tutorial      |
| `session-05.md`                  | Tutorial    | Session 05      | Self-guided HTML forms tutorial       |
| `session-06.md`                  | Tutorial    | Session 06      | Self-guided form validation tutorial  |
| `table-cheat-sheet.md`           | Reference   | Session 04      | Quick table syntax reference          |
| `forms-cheat-sheet.md`           | Reference   | Session 05      | Quick form syntax reference           |
| `validation-cheat-sheet.md`      | Reference   | Session 06      | Quick validation syntax reference     |
| `table-anatomy-visual.html`      | Interactive | Session 04      | Visual guide to table structure       |
| `form-anatomy-visual.html`       | Interactive | Session 05      | Visual guide to form structure        |
| `validation-anatomy-visual.html` | Interactive | Session 06      | Visual guide to validation attributes |
| `table-template.html`            | Template    | Session 04      | Starter file for table practice       |
| `form-template.html`             | Template    | Session 05      | Starter file for form practice        |
| `validation-template.html`       | Template    | Session 06      | Starter file for validation practice  |
| `course-table-solution.html`     | Solution    | Session 04      | Complete table example                |
| `contact-form-solution.html`     | Solution    | Session 05      | Complete form example                 |
| `validated-form-solution.html`   | Solution    | Session 06      | Complete validated form example       |
| `sample-data.csv`                | Data        | Session 04      | Sample data for table exercises       |
| `README.md`                      | Index       | All             | This file—navigation guide            |

---

## 📚 Session 04: Tables and Tabular Data

### 📖 Learning Materials

1. **`session-04.md`** - Complete self-guided tutorial (start here!)
2. **`table-cheat-sheet.md`** - Quick reference guide for HTML tables
3. **`table-anatomy-visual.html`** - Interactive visual guide to table structure

### 💻 Practice Files

1. **`sample-data.csv`** - Sample course data for table exercises
2. **`table-template.html`** - Starter template with basic styling
3. **`course-table-solution.html`** - Complete solution example

### 🎯 How to Use These Files

**Step-by-step learning path:**

1. **Start:** Open `session-04.md` and read it from beginning to end
2. **Visualize:** Open `table-anatomy-visual.html` in your browser to see how tables are structured
3. **Practice:** When you reach exercises, use `table-template.html` as your starting point
4. **Reference:** Keep `table-cheat-sheet.md` open for quick lookups
5. **Verify:** Compare your work to `course-table-solution.html` after completing exercises

**Tips for success:**

-   ✅ Work through the tutorial in order—each section builds on the previous one
-   ✅ Type out the code examples yourself (don't just copy-paste)
-   ✅ Test your tables in a browser after each change
-   ✅ Try the practice exercises before looking at solutions
-   ✅ Use the cheat sheet when you forget syntax

### 🎨 What Each File Does

| File                         | Purpose                                         | When to Use                  |
| ---------------------------- | ----------------------------------------------- | ---------------------------- |
| `session-04.md`              | Main tutorial with explanations and exercises   | Primary learning material    |
| `table-anatomy-visual.html`  | Color-coded visual breakdown of table structure | Understanding table parts    |
| `table-cheat-sheet.md`       | Quick syntax reference                          | When you need a reminder     |
| `table-template.html`        | Pre-styled HTML file for practice               | Starting point for exercises |
| `sample-data.csv`            | Practice dataset                                | Converting CSV to HTML table |
| `course-table-solution.html` | Completed example                               | Checking your work           |

### 📝 Quick Reference

**Minimal accessible table:**

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
</table>
```

### 🔗 External Resources

-   [MDN: HTML Tables Basics](https://developer.mozilla.org/docs/Learn/HTML/Tables/Basics)
-   [W3C WAI: Tables Tutorial](https://www.w3.org/WAI/tutorials/tables/)
-   [WebAIM: Creating Accessible Tables](https://webaim.org/techniques/tables/)

### ✅ Learning Outcomes

By the end of Session 04, you should be able to:

-   Explain when to use tables vs. CSS for layout
-   Create properly structured tables with `<thead>`, `<tbody>`, and `<tfoot>`
-   Use `scope` attributes correctly for accessibility
-   Write descriptive captions
-   Convert tabular data (like CSV) into semantic HTML

---

## � Session 05: Forms I — Inputs and Labels

### 📖 Learning Materials

1. **`session-05.md`** - Complete self-guided tutorial on HTML forms (start here!)
2. **`forms-cheat-sheet.md`** - Quick reference guide for form elements and patterns
3. **`form-anatomy-visual.html`** - Interactive color-coded guide showing form structure

### 💻 Practice Files

1. **`form-template.html`** - Starter template with basic styling
2. **`contact-form-solution.html`** - Complete solution example with best practices

### 🎯 How to Use These Files

**Step-by-step learning path:**

1. **Start:** Open `session-05.md` and work through it section by section
2. **Practice:** Use `form-template.html` as your starting point for exercises
3. **Reference:** Keep `forms-cheat-sheet.md` open for quick syntax lookups
4. **Verify:** Compare your work to `contact-form-solution.html` after completing exercises

**Tips for success:**

-   ✅ Type out the code examples yourself—muscle memory helps!
-   ✅ Test forms in your browser frequently to see how they behave
-   ✅ Try clicking labels to ensure they're properly connected
-   ✅ Practice with different input types to understand their behavior
-   ✅ Complete all quiz questions to test your understanding

### 🎨 What Each File Does

| File                         | Purpose                                     | When to Use                  |
| ---------------------------- | ------------------------------------------- | ---------------------------- |
| `session-05.md`              | Main tutorial with explanations and quizzes | Primary learning material    |
| `forms-cheat-sheet.md`       | Quick syntax reference for form elements    | When you need a reminder     |
| `form-anatomy-visual.html`   | Interactive visual guide to form structure  | Understanding connections    |
| `form-template.html`         | Pre-styled HTML file for practice           | Starting point for exercises |
| `contact-form-solution.html` | Completed example with accessibility notes  | Checking your work           |

### 📝 Quick Reference

**Minimal accessible form:**

```html
<form>
	<fieldset>
		<legend>Section Title</legend>

		<div>
			<label for="name">Name</label>
			<input
				id="name"
				name="name"
				type="text"
			/>
		</div>

		<div>
			<label for="email">Email</label>
			<input
				id="email"
				name="email"
				type="email"
			/>
		</div>
	</fieldset>

	<button type="submit">Submit</button>
</form>
```

**Key rules:**

-   Every input needs a `<label>`
-   `for` attribute must match the input's `id`
-   Every input needs a `name` for form submission
-   Use appropriate `type` attributes (email, tel, date, etc.)
-   Group related fields with `<fieldset>` and `<legend>`

### 🔗 External Resources

-   [MDN: Your First Form](https://developer.mozilla.org/docs/Learn/Forms/Your_first_form)
-   [MDN: How to Structure a Form](https://developer.mozilla.org/docs/Learn/Forms/How_to_structure_a_web_form)
-   [WebAIM: Creating Accessible Forms](https://webaim.org/techniques/forms/)

### ✅ Learning Outcomes

By the end of Session 05, you should be able to:

-   Create accessible forms with proper label associations
-   Understand the difference between `id` and `name` attributes
-   Use different input types appropriately (text, email, password, etc.)
-   Organize forms with fieldsets and legends
-   Explain why placeholders aren't replacements for labels

---

## � Session 06: Forms II — Validation & Accessibility

### 📖 Learning Materials

1. **`session-06.md`** - Complete self-guided tutorial on form validation (start here!)
2. **`validation-cheat-sheet.md`** - Quick reference guide for HTML5 validation and ARIA
3. **`validation-anatomy-visual.html`** - Interactive color-coded guide to validation attributes

### 💻 Practice Files

1. **`validation-template.html`** - Starter template with form needing validation
2. **`validated-form-solution.html`** - Complete solution with validation and ARIA

### 🎯 How to Use These Files

**Step-by-step learning path:**

1. **Start:** Open `session-06.md` and work through it section by section
2. **Visualize:** Open `validation-anatomy-visual.html` in your browser to see validation attributes
3. **Practice:** Use `validation-template.html` as your starting point for exercises
4. **Reference:** Keep `validation-cheat-sheet.md` open for quick syntax lookups
5. **Verify:** Compare your work to `validated-form-solution.html` after completing exercises

**Tips for success:**

-   ✅ Complete Session 05 first—this builds on forms basics
-   ✅ Test validation by trying to submit invalid data
-   ✅ Use browser DevTools to inspect validation states
-   ✅ Test with keyboard navigation (Tab, Enter keys)
-   ✅ Try all quiz questions to solidify understanding

### 🎨 What Each File Does

| File                             | Purpose                                    | When to Use                   |
| -------------------------------- | ------------------------------------------ | ----------------------------- |
| `session-06.md`                  | Main tutorial with validation explanations | Primary learning material     |
| `validation-cheat-sheet.md`      | Quick syntax reference for validation/ARIA | When you need a reminder      |
| `validation-anatomy-visual.html` | Interactive visual guide with color coding | Understanding validation flow |
| `validation-template.html`       | Pre-styled form for adding validation      | Starting point for exercises  |
| `validated-form-solution.html`   | Completed example with all attributes      | Checking your work            |

### 📝 Quick Reference

**Common validation attributes:**

```html
<!-- Required field -->
<input
	id="name"
	name="name"
	type="text"
	required
/>

<!-- Length constraints -->
<input
	id="username"
	name="username"
	type="text"
	minlength="3"
	maxlength="20"
	required
/>

<!-- Email validation -->
<input
	id="email"
	name="email"
	type="email"
	required
/>

<!-- Pattern validation with help text -->
<input
	id="phone"
	name="phone"
	type="tel"
	pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}"
	title="Format: 123-456-7890"
	aria-describedby="phone-help"
	required
/>
<small id="phone-help">Format: 123-456-7890</small>
```

**Key validation attributes:**

-   `required` - Field must be filled
-   `minlength` / `maxlength` - Text length constraints
-   `min` / `max` - Numeric range constraints
-   `pattern` - Regular expression validation
-   `type` - Input type (email, url, tel, number, date, etc.)
-   `aria-describedby` - Associate help text with input
-   `aria-invalid` - Mark field as invalid (use with JavaScript)

### 🔗 External Resources

-   [MDN: Client-side Form Validation](https://developer.mozilla.org/docs/Learn/Forms/Form_validation)
-   [MDN: HTML5 Constraint Validation](https://developer.mozilla.org/docs/Web/HTML/Constraint_validation)
-   [WAI: Forms Tutorial](https://www.w3.org/WAI/tutorials/forms/)
-   [WebAIM: Creating Accessible Forms](https://webaim.org/techniques/forms/)

### ✅ Learning Outcomes

By the end of Session 06, you should be able to:

-   Apply HTML5 validation attributes (`required`, `minlength`, `pattern`, etc.)
-   Use `pattern` attribute with regular expressions
-   Provide helpful error messages with `title` attribute
-   Associate help text with inputs using `aria-describedby`
-   Understand the constraint validation API
-   Create accessible validated forms
-   Test validation with keyboard and different browsers

---

## 💡 Need Help?

**For Tables (Session 04):**

1. Check the `table-cheat-sheet.md` for syntax
2. Review the visual guide in `table-anatomy-visual.html`
3. Look at the solution in `course-table-solution.html`
4. Re-read the relevant section in `session-04.md`

**For Forms Basics (Session 05):**

1. Check the `forms-cheat-sheet.md` for syntax
2. Review the visual guide in `form-anatomy-visual.html`
3. Look at the solution in `contact-form-solution.html`
4. Re-read the relevant section in `session-05.md`
5. Test your form by clicking labels and using Tab to navigate

**For Form Validation (Session 06):**

1. Check the `validation-cheat-sheet.md` for syntax
2. Review the visual guide in `validation-anatomy-visual.html`
3. Look at the solution in `validated-form-solution.html`
4. Re-read the relevant section in `session-06.md`
5. Test validation by submitting invalid data
6. Inspect validation states using browser DevTools

**General:**

-   Search MDN documentation for detailed explanations
-   Use your browser's DevTools to inspect elements
-   Test with keyboard navigation (Tab, Enter keys)
-   Try forms in different browsers to see validation behavior
