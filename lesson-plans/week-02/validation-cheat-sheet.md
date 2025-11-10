# HTML Form Validation Cheat Sheet

Quick reference for HTML5 validation attributes and ARIA for accessible error handling.

---

## 📋 HTML5 Validation Attributes

### Basic Validation

| Attribute   | Purpose                    | Example                               | Notes                                |
| ----------- | -------------------------- | ------------------------------------- | ------------------------------------ |
| `required`  | Field must be filled       | `<input required>`                    | Works on text, email, checkbox, etc. |
| `minlength` | Minimum character count    | `<input minlength="3">`               | Text inputs only                     |
| `maxlength` | Maximum character count    | `<input maxlength="100">`             | Text inputs only                     |
| `min`       | Minimum numeric value      | `<input type="number" min="0">`       | Number, date, range inputs           |
| `max`       | Maximum numeric value      | `<input type="number" max="100">`     | Number, date, range inputs           |
| `pattern`   | Custom regex validation    | `<input pattern="[0-9]{3}-[0-9]{4}">` | Must match entire value              |
| `type`      | Built-in format validation | `<input type="email">`                | email, url, tel, number, date, etc.  |

### Common Input Types with Built-in Validation

| Type     | Validates For             | Mobile Keyboard        |
| -------- | ------------------------- | ---------------------- |
| `email`  | Email format (includes @) | Email keyboard with @  |
| `url`    | URL format (http://)      | URL keyboard with .com |
| `tel`    | Phone numbers             | Numeric keyboard       |
| `number` | Numeric values            | Numeric keyboard       |
| `date`   | Date format               | Date picker            |
| `time`   | Time format               | Time picker            |
| `color`  | Color hex values          | Color picker           |

---

## 🎯 Pattern Examples

### Common Patterns

```html
<!-- US Phone: (123) 456-7890 or 123-456-7890 -->
<input pattern="[\(]?[0-9]{3}[\)]?[\s\-]?[0-9]{3}[\s\-]?[0-9]{4}" />

<!-- ZIP Code: 12345 or 12345-6789 -->
<input pattern="[0-9]{5}(-[0-9]{4})?" />

<!-- Username: letters, numbers, underscore, 3-16 chars -->
<input pattern="[a-zA-Z0-9_]{3,16}" />

<!-- Hex Color: #fff or #ffffff -->
<input pattern="#[0-9a-fA-F]{3}([0-9a-fA-F]{3})?" />

<!-- Credit Card: 16 digits with optional spaces/dashes -->
<input pattern="[0-9]{4}[\s\-]?[0-9]{4}[\s\-]?[0-9]{4}[\s\-]?[0-9]{4}" />
```

### Pattern Tips

-   Always include a `title` attribute to explain the pattern
-   Patterns must match the **entire** value (implicit `^` and `$`)
-   Use `\s` for whitespace, `\d` for digits (but `[0-9]` is safer)
-   Test patterns thoroughly—overly strict patterns frustrate users

---

## ♿ ARIA Attributes for Accessible Validation

### Essential ARIA Attributes

| Attribute          | Purpose                        | Example                                                 |
| ------------------ | ------------------------------ | ------------------------------------------------------- |
| `aria-describedby` | Links help/error text to input | `<input aria-describedby="email-help email-error">`     |
| `aria-invalid`     | Marks field as having an error | `<input aria-invalid="true">`                           |
| `aria-live`        | Announces dynamic changes      | `<div aria-live="polite" id="error"></div>`             |
| `aria-required`    | Indicates required field       | `<input aria-required="true">` (use `required` instead) |

### How to Use aria-describedby

```html
<label for="email">Email Address</label>
<input
	id="email"
	name="email"
	type="email"
	required
	aria-describedby="email-help email-error"
/>
<small id="email-help">We'll never share your email.</small>
<small
	id="email-error"
	aria-live="polite"
></small>
```

**What happens:**

-   Screen reader announces: "Email Address, required, edit text, We'll never share your email"
-   If error appears, it's announced due to `aria-live="polite"`
-   User understands the field's purpose and constraints

---

## ✅ Complete Validated Field Example

```html
<div class="form-field">
	<label for="username">Username</label>
	<input
		id="username"
		name="username"
		type="text"
		required
		minlength="3"
		maxlength="16"
		pattern="[a-zA-Z0-9_]+"
		title="Letters, numbers, and underscores only"
		aria-describedby="username-help username-error"
	/>
	<small id="username-help">
		3-16 characters, letters, numbers, and underscores only
	</small>
	<small
		id="username-error"
		aria-live="polite"
		role="alert"
	></small>
</div>
```

---

## 🎨 Styling Validation States

### CSS Pseudo-classes

```css
/* Valid input */
input:valid {
	border-color: green;
}

/* Invalid input */
input:invalid {
	border-color: red;
}

/* Required input */
input:required {
	border-left: 3px solid orange;
}

/* Optional input */
input:optional {
	border-left: 3px solid lightgray;
}

/* Only show invalid state after user interaction */
input:not(:focus):invalid {
	border-color: red;
}
```

### Accessible Error Styling

```css
/* Error text */
.error-message {
	color: #c41e3a;
	font-size: 0.9em;
	display: none;
}

/* Show error when input is invalid */
input:invalid + .error-message {
	display: block;
}

/* Ensure sufficient color contrast */
.error-message {
	background: #fef6f6;
	padding: 0.5em;
	border-left: 3px solid #c41e3a;
}
```

---

## 🚫 Common Mistakes

### ❌ Don't Do This

```html
<!-- Missing aria-describedby -->
<input
	id="email"
	type="email"
	required
/>
<small id="email-help">Enter a valid email</small>

<!-- Pattern without title -->
<input pattern="[0-9]{5}" />

<!-- Using placeholder as label -->
<input
	placeholder="Email"
	type="email"
	required
/>

<!-- Error not connected -->
<input
	id="email"
	type="email"
/>
<span class="error">Invalid email!</span>
```

### ✅ Do This Instead

```html
<!-- Proper aria-describedby -->
<label for="email">Email</label>
<input
	id="email"
	type="email"
	required
	aria-describedby="email-help"
/>
<small id="email-help">Enter a valid email</small>

<!-- Pattern with helpful title -->
<label for="zip">ZIP Code</label>
<input
	id="zip"
	pattern="[0-9]{5}"
	title="5-digit ZIP code"
/>

<!-- Always use label, placeholder is extra -->
<label for="email">Email Address</label>
<input
	id="email"
	type="email"
	required
	placeholder="you@example.com"
/>

<!-- Error properly connected -->
<label for="email">Email</label>
<input
	id="email"
	type="email"
	aria-describedby="email-error"
	aria-invalid="true"
/>
<span
	id="email-error"
	role="alert"
	>Please enter a valid email</span
>
```

---

## 📚 Validation Checklist

Before submitting your form:

-   [ ] Every required field has `required` attribute
-   [ ] Text inputs have appropriate `minlength`/`maxlength`
-   [ ] Numeric inputs have appropriate `min`/`max`
-   [ ] Input types are as specific as possible (`email`, `tel`, `url`, etc.)
-   [ ] Patterns include helpful `title` attributes
-   [ ] Help text is connected via `aria-describedby`
-   [ ] Error messages have unique `id` attributes
-   [ ] Error regions use `aria-live="polite"` and `role="alert"`
-   [ ] Form works with keyboard only (Tab, Enter, Space)
-   [ ] Error messages are clear and actionable
-   [ ] Validation styling has sufficient color contrast

---

## 🔗 Additional Resources

-   [MDN: Client-side Form Validation](https://developer.mozilla.org/docs/Learn/Forms/Form_validation)
-   [MDN: Constraint Validation API](https://developer.mozilla.org/docs/Web/API/Constraint_validation)
-   [W3C: ARIA Authoring Practices - Forms](https://www.w3.org/WAI/ARIA/apg/patterns/)
-   [WebAIM: Creating Accessible Forms](https://webaim.org/techniques/forms/)
-   [Regex101](https://regex101.com/) - Test your patterns

---

## 💡 Quick Tips

1. **Start simple:** Use built-in types (`email`, `number`) before reaching for `pattern`
2. **Be forgiving:** Don't reject valid input (e.g., allow spaces in phone numbers)
3. **Test thoroughly:** Try your form with keyboard, screen reader, and mobile
4. **Provide context:** Always explain what format you expect
5. **Don't rely on color alone:** Use icons, text, or patterns for errors
6. **Server-side too:** Always validate on the server—client-side is just UX
