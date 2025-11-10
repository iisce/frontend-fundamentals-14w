# HTML Forms Quick Reference

## Basic Form Structure

```html
<form>
	<fieldset>
		<legend>Section Title</legend>

		<div>
			<label for="fieldId">Field Label</label>
			<input
				id="fieldId"
				name="fieldName"
				type="text"
			/>
		</div>
	</fieldset>

	<button type="submit">Submit</button>
</form>
```

## Essential Elements

| Element      | Purpose                       | Required?                           |
| ------------ | ----------------------------- | ----------------------------------- |
| `<form>`     | Container for the form        | Yes                                 |
| `<label>`    | Describes what a field is for | Yes (for accessibility)             |
| `<input>`    | Single-line input field       | For most fields                     |
| `<textarea>` | Multi-line text input         | For long text                       |
| `<select>`   | Dropdown menu                 | For choices                         |
| `<button>`   | Submit or action button       | Yes                                 |
| `<fieldset>` | Groups related fields         | Recommended for multi-section forms |
| `<legend>`   | Title for a fieldset          | Required with `<fieldset>`          |

## Label-Input Connection

**The Golden Rule:** `for` must match `id`

```html
<label for="email">Email</label>
<input
	id="email"
	name="email"
	type="email"
/>
<!--       ↑                ↑                     -->
<!--   These MUST match exactly!                 -->
```

**Why both `id` and `name`?**

-   `id` — Connects the label (accessibility)
-   `name` — Identifies the data when submitted (functionality)

## Common Input Types

| Type       | Purpose            | Mobile Keyboard | Example             |
| ---------- | ------------------ | --------------- | ------------------- |
| `text`     | General text       | Standard        | Name, username      |
| `email`    | Email addresses    | @ symbol shown  | user@example.com    |
| `password` | Passwords (hidden) | Standard        | •••••••••           |
| `tel`      | Phone numbers      | Number pad      | (555) 123-4567      |
| `number`   | Numbers only       | Number pad      | 42                  |
| `date`     | Date picker        | Date picker     | 2025-11-10          |
| `url`      | Website URLs       | .com shown      | https://example.com |
| `search`   | Search queries     | Search button   | "Find..."           |

## Input Patterns

### Text Input

```html
<div>
	<label for="name">Name</label>
	<input
		id="name"
		name="name"
		type="text"
		placeholder="e.g., Jane Smith"
	/>
</div>
```

### Email Input

```html
<div>
	<label for="email">Email</label>
	<input
		id="email"
		name="email"
		type="email"
		placeholder="your.email@example.com"
	/>
</div>
```

### Password Input

```html
<div>
	<label for="password">Password</label>
	<input
		id="password"
		name="password"
		type="password"
	/>
</div>
```

### Textarea (Multi-line)

```html
<div>
	<label for="message">Message</label>
	<textarea
		id="message"
		name="message"
		rows="5"
		placeholder="Enter your message here..."
	></textarea>
</div>
```

### Date Input

```html
<div>
	<label for="birth-date">Date of Birth</label>
	<input
		id="birth-date"
		name="birth_date"
		type="date"
	/>
</div>
```

### Number Input

```html
<div>
	<label for="age">Age</label>
	<input
		id="age"
		name="age"
		type="number"
		min="0"
		max="120"
	/>
</div>
```

## Grouping with Fieldsets

### When to Use Fieldsets

**✅ Use for:**

-   Multi-section forms (registration, checkout)
-   Forms with distinct categories
-   Related fields that belong together

**❌ Don't use for:**

-   Very simple forms (1-3 fields)
-   Every single field

### Pattern: Two-Section Form

```html
<form>
	<fieldset>
		<legend>Personal Information</legend>

		<div>
			<label for="first-name">First Name</label>
			<input
				id="first-name"
				name="first_name"
				type="text"
			/>
		</div>

		<div>
			<label for="last-name">Last Name</label>
			<input
				id="last-name"
				name="last_name"
				type="text"
			/>
		</div>
	</fieldset>

	<fieldset>
		<legend>Contact Details</legend>

		<div>
			<label for="email">Email</label>
			<input
				id="email"
				name="email"
				type="email"
			/>
		</div>

		<div>
			<label for="phone">Phone</label>
			<input
				id="phone"
				name="phone"
				type="tel"
			/>
		</div>
	</fieldset>

	<button type="submit">Submit</button>
</form>
```

## Button Types

```html
<!-- Submit button (submits the form) -->
<button type="submit">Submit</button>

<!-- Reset button (clears all fields) - rarely used -->
<button type="reset">Reset</button>

<!-- Generic button (does nothing by default) -->
<button type="button">Click Me</button>
```

## Placeholders vs Labels

### ❌ WRONG: Placeholder Only

```html
<input
	type="text"
	placeholder="Enter your name"
/>
<!-- No label! Bad for accessibility! -->
```

### ✅ RIGHT: Label + Optional Placeholder

```html
<label for="name">Name</label>
<input
	id="name"
	name="name"
	type="text"
	placeholder="e.g., Jane Smith"
/>
```

**Why?**

-   Placeholders disappear when typing
-   Placeholders are often too low contrast
-   Screen readers might not announce placeholders
-   Labels are always visible and accessible

## Complete Form Examples

### Example 1: Simple Contact Form

```html
<form>
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

	<div>
		<label for="message">Message</label>
		<textarea
			id="message"
			name="message"
			rows="4"
		></textarea>
	</div>

	<button type="submit">Send</button>
</form>
```

### Example 2: Registration Form with Fieldsets

```html
<form>
	<fieldset>
		<legend>Account Information</legend>

		<div>
			<label for="username">Username</label>
			<input
				id="username"
				name="username"
				type="text"
			/>
		</div>

		<div>
			<label for="password">Password</label>
			<input
				id="password"
				name="password"
				type="password"
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

	<fieldset>
		<legend>Personal Details</legend>

		<div>
			<label for="full-name">Full Name</label>
			<input
				id="full-name"
				name="full_name"
				type="text"
			/>
		</div>

		<div>
			<label for="birth-date">Date of Birth</label>
			<input
				id="birth-date"
				name="birth_date"
				type="date"
			/>
		</div>
	</fieldset>

	<button type="submit">Create Account</button>
</form>
```

## Accessibility Checklist

✅ **DO:**

-   Use a `<label>` for every input
-   Connect labels with `for`/`id`
-   Add `name` to all inputs
-   Use appropriate `type` attributes
-   Group related fields with `<fieldset>`
-   Use descriptive button text
-   Test with keyboard navigation (Tab key)

❌ **DON'T:**

-   Use placeholders instead of labels
-   Leave `for`/`id` mismatched
-   Forget `name` attributes
-   Use `type="text"` for everything
-   Over-group with unnecessary fieldsets
-   Use vague button text like "Click Here"

## Common Mistakes

### Mistake 1: No Label

```html
<!-- ❌ Bad -->
<input type="text" />

<!-- ✅ Good -->
<label for="name">Name</label>
<input
	id="name"
	name="name"
	type="text"
/>
```

### Mistake 2: Mismatched for/id

```html
<!-- ❌ Bad -->
<label for="email">Email</label>
<input
	id="email-address"
	name="email"
	type="email"
/>

<!-- ✅ Good -->
<label for="email">Email</label>
<input
	id="email"
	name="email"
	type="email"
/>
```

### Mistake 3: Missing name

```html
<!-- ❌ Bad -->
<input
	id="username"
	type="text"
/>

<!-- ✅ Good -->
<input
	id="username"
	name="username"
	type="text"
/>
```

### Mistake 4: Fieldset without Legend

```html
<!-- ❌ Bad -->
<fieldset>
	<label for="name">Name</label>
	<input
		id="name"
		name="name"
		type="text"
	/>
</fieldset>

<!-- ✅ Good -->
<fieldset>
	<legend>Personal Information</legend>
	<label for="name">Name</label>
	<input
		id="name"
		name="name"
		type="text"
	/>
</fieldset>
```

## Quick Styling (CSS)

```css
/* Form container */
form {
	max-width: 600px;
	margin: 0 auto;
}

/* Fieldsets */
fieldset {
	border: 2px solid #ddd;
	border-radius: 4px;
	padding: 15px;
	margin-bottom: 20px;
}

legend {
	font-weight: bold;
	padding: 0 10px;
}

/* Field containers */
div {
	margin-bottom: 15px;
}

/* Labels */
label {
	display: block;
	font-weight: 600;
	margin-bottom: 5px;
}

/* Inputs */
input,
textarea {
	width: 100%;
	padding: 8px 12px;
	border: 1px solid #ccc;
	border-radius: 4px;
	font-size: 1em;
}

input:focus,
textarea:focus {
	outline: none;
	border-color: #007bff;
	box-shadow: 0 0 0 3px rgba(0, 123, 255, 0.1);
}

/* Buttons */
button {
	background-color: #007bff;
	color: white;
	padding: 10px 20px;
	border: none;
	border-radius: 4px;
	font-size: 1em;
	cursor: pointer;
}

button:hover {
	background-color: #0056b3;
}
```

## Resources

-   [MDN: Your First Form](https://developer.mozilla.org/docs/Learn/Forms/Your_first_form)
-   [MDN: How to Structure a Form](https://developer.mozilla.org/docs/Learn/Forms/How_to_structure_a_web_form)
-   [WebAIM: Creating Accessible Forms](https://webaim.org/techniques/forms/)

---

**Quick Test:** Can you create a form with name, email, and message fields, all properly labeled and grouped in a fieldset? Try it!
