# Week 02 — Session 06: Forms II — Validation & Accessibility# Week 02 — Session 06: Forms II — Validation & Accessibility

**Duration:** 90 minutes (self-paced) Navigation

**Prerequisites:** Completion of Session 05 (Forms I)

-   Back to Learning Plan: ../learning-plan.md

**Navigation:** [← Session 05](session-05.md) | [Week 02 Index](README.md) | [Learning Plan](../learning-plan.md)- Week 02 Index: ../week-02.md

-   Prev: session-05.md

---- Next: ../week-03/session-07.md

## 🎯 Welcome to Form Validation!Session length: 90 minutes

In Session 05, you learned how to create accessible forms with proper labels and structure. Now you'll make those forms **smarter** by adding validation—ensuring users provide the right data in the right format **before** the form is submitted.Pre-class checklist

### What You'll Learn Today- Open your Session 05 contact form

-   Skim MDN’s client-side form validation guide (links below)

By the end of this session, you'll be able to:

Learning objectives

-   ✅ Use HTML5 validation attributes (`required`, `minlength`, `maxlength`, `min`, `max`, `pattern`)

-   ✅ Provide helpful error messages and instructions- Use built-in HTML validation attributes (`required`, `min`, `max`, `minlength`, `maxlength`, `pattern`)

-   ✅ Connect help text to form fields using ARIA attributes- Provide helpful error messages and instructions

-   ✅ Create keyboard and screen-reader friendly validated forms- Ensure forms are keyboard and screen-reader friendly

-   ✅ Style validation states with CSS

Materials

### Files You'll Need

-   MDN: Client-side form validation — [MDN Validation](https://developer.mozilla.org/docs/Learn/Forms/Form_validation)

Before you start, make sure you have these files open:- WAI: Labels and instructions — [WAI Forms Labels](https://www.w3.org/WAI/tutorials/forms/labels/)

1. **`validation-cheat-sheet.md`** - Quick reference for validation attributesKey terms

2. **`validation-anatomy-visual.html`** - Interactive visual guide (open in browser)

3. **`validation-template.html`** - Practice template- constraint validation, required, pattern, minlength, aria-describedby, invalid, help text

4. **`validated-form-solution.html`** - Complete solution example

You will build

### Key Terms

-   An enhanced contact form with built-in validation and associated help/error text

-   **constraint validation** - Browser's built-in validation system

-   **required** - Field must be filled before submission## 1) HTML validation (25m)

-   **pattern** - Custom regex validation for specific formats

-   **aria-describedby** - Links help text to inputs for screen readersStart by layering constraints on existing fields.

-   **help text** - Instructions that guide users on what to enter

````html

---<form>

	<label for="name">Name</label>

## Part 1: HTML5 Validation Basics (30 minutes)	<input

		id="name"

### What is Form Validation?		name="name"

		type="text"

**Validation** ensures that user input meets certain requirements before being processed. There are two types:		required

		minlength="2"

1. **Client-side validation** (what we're learning today) - Happens in the browser before submission	/>

2. **Server-side validation** (covered later) - Happens on the server after submission

	<label for="email">Email</label>

> ⚠️ **Important:** Always validate on the server too! Client-side validation is for UX, not security.	<input

		id="email"

### The `required` Attribute		name="email"

		type="email"

The simplest validation: make a field mandatory.		required

	/>

```html

<label for="name">Name</label>	<label for="phone">Phone (optional)</label>

<input id="name" name="name" type="text" required />	<input

```		id="phone"

		name="phone"

**What happens:**		type="tel"

- User cannot submit the form if this field is empty		pattern="^[0-9\-\s\(\)]+$"

- Browser shows a default error message: "Please fill out this field"		title="Use digits, spaces, parentheses, and dashes only"

- Field is marked as `:invalid` until filled in	/>



### Input Type Validation	<button type="submit">Send</button>

</form>

Using specific input types gives you free validation:```



```htmlNotes

<!-- Email validation (checks for @ and domain) -->

<label for="email">Email</label>-   Browsers provide default messages; you can customize with `title` and help text

<input id="email" name="email" type="email" required />-   Use appropriate `type` (e.g., `email`) to get free validation and better mobile keyboards



<!-- URL validation (checks for http:// or https://) -->## 2) Error UX and help text (15m)

<label for="website">Website</label>

<input id="website" name="website" type="url" />Associate instructions and errors with inputs via `aria-describedby`.



<!-- Number validation (only allows numbers) -->```html

<label for="age">Age</label><label for="email">Email</label>

<input id="age" name="age" type="number" min="18" max="120" /><input

	id="email"

<!-- Date validation (ensures valid date format) -->	name="email"

<label for="birthday">Birthday</label>	type="email"

<input id="birthday" name="birthday" type="date" />	required

```	aria-describedby="email-help email-error"

/>

**Bonus:** Mobile devices show appropriate keyboards (email keyboard has @, number keyboard is numeric, etc.)<small id="email-help">We will only use this to reply to you.</small>

<small

### Length Constraints	id="email-error"

	aria-live="polite"

Control how much text users can enter:></small>

````

````html
<!-- Username: 3-16 characters -->Notes

<label for="username">Username</label>

<input - Keep help text visible by default; reserve `aria-live` regions for
dynamic error/status updates id="username" - Ensure the described elements have
unique `id`s and are referenced on the input name="username" type="text"## 3)
Guided lab (40m) required minlength="3"Goal: Enhance the Session 05 contact form
with validation and help text. maxlength="16" />Steps

<!-- Comment: max 500 characters -->1. Make `name` and `email` required; set
sensible length limits

<label for="comment">Comment</label>2. Use `type="email"` for email; consider a
basic `pattern` for telephone if you added it

<textarea
	3.
	Add
	help
	text
	beneath
	each
	input,
	and
	connect
	via
	`aria-describedby`
	id="comment"
	4.
	Add
	a
	brief
	instruction
	near
	the
	submit
	button
	(e.g.,
	required
	fields
	note)
	name="comment"
	maxlength="500"
	Checklist
></textarea>

```- [ ] Required fields are marked with `required` - [ ] Inputs use the most
specific `type` available ### Numeric Ranges- [ ] Help text and/or error text is
associated via `aria-describedby` - [ ] Title or pattern messages are
user-friendly (no regex-only messages) For number, date, and range inputs:
Knowledge checks ```html

<!-- Age must be 18-120 -->- Q: What are the pros/cons of `pattern` compared to
appropriate input `type`?

<input
	type="number"
	min="18"
	max="120"
/>- Q: How does `aria-describedby` improve the screen reader experience?

<!-- Quantity must be at least 1 -->Common pitfalls

<input
	type="number"
	min="1"
	value="1"
/>

- Overly strict `pattern` that blocks valid input

<!-- Date must be in the future -->- Missing `name` attributes (the form may
look fine but sends nothing)

<input
	type="date"
	min="2025-11-11"
/>- Help text present but not referenced (not read by screen readers)
````

Homework (30–45 minutes)

### ✏️ Quick Practice 1

-   Exercise: Add validation to your feedback form from Session 05.

Open `validation-template.html` in your code editor. Try these tasks:- Acceptance criteria:

    -   [ ] Required fields marked and enforced by the browser

1. Add `required` to the name, email, and message fields - [ ] Helpful instructions (help text) for at least two fields

2. Change the email input's `type` from `"text"` to `"email"` - [ ] Inputs use specific types and constraints (`type`, `minlength`, `maxlength`, `pattern` when reasonable)

3. Add `minlength="2"` and `maxlength="50"` to the name field - [ ] Help text is connected via `aria-describedby`

4. Add `minlength="10"` to the message textarea

Troubleshooting

Save and test in your browser. Try submitting with empty fields!

-   Browser messages differ? That’s normal; supplement with clear help text via `aria-describedby` and `title`

<details>-   Screen reader doesn’t announce the help/error? Verify the `aria-describedby` IDs match

<summary>📖 Show Solution</summary>

Navigation

```html
<div class="form-field">
	- Back: ../learning-plan.md

	<label for="name">Full Name</label>- Week 02 Index: ../week-02.md <input -
	Prev: session-05.md id="name" - Next: ../week-03/session-07.md name="name"
	type="text" required minlength="2" maxlength="50" />
</div>

<div class="form-field">
	<label for="email">Email Address</label>
	<input
		id="email"
		name="email"
		type="email"
		required
	/>
</div>

<div class="form-field">
	<label for="message">Message</label>
	<textarea
		id="message"
		name="message"
		required
		minlength="10"
	></textarea>
</div>
```

</details>

### 🧠 Knowledge Check 1

<details>
<summary>Q1: What's the difference between <code>minlength</code> and <code>min</code>?</summary>

**Answer:**

-   `minlength` - Minimum number of **characters** for text inputs
-   `min` - Minimum **value** for number/date/range inputs

Examples:

-   `minlength="5"` - Text must be at least 5 characters long
-   `min="18"` - Number must be at least 18

</details>

<details>
<summary>Q2: If I use <code>type="email"</code>, do I still need <code>required</code>?</summary>

**Answer:**
It depends!

-   `type="email"` validates the **format** (checks for @ symbol)
-   `required` makes the field **mandatory**

If the email is optional but must be valid when provided, use only `type="email"`.
If the email is required, use **both** `type="email"` and `required`.

</details>

<details>
<summary>Q3: Can users bypass client-side validation?</summary>

**Answer:**
Yes! Users can:

-   Disable JavaScript
-   Edit HTML in DevTools
-   Submit forms directly via API

That's why you **must** always validate on the server too. Client-side validation is for **user experience**, not **security**.

</details>

---

## Part 2: Pattern Validation & Custom Messages (25 minutes)

### The `pattern` Attribute

For custom validation beyond built-in types, use `pattern` with regex:

```html
<!-- US Phone: (123) 456-7890 or 123-456-7890 -->
<label for="phone">Phone Number</label>
<input
	id="phone"
	name="phone"
	type="tel"
	pattern="[\(]?[0-9]{3}[\)]?[\s\-]?[0-9]{3}[\s\-]?[0-9]{4}"
	title="Format: (123) 456-7890 or 123-456-7890"
/>
```

**Important:** Always include a `title` attribute! It shows users what format you expect.

### Common Pattern Examples

```html
<!-- ZIP Code: 12345 or 12345-6789 -->
<input
	pattern="[0-9]{5}(-[0-9]{4})?"
	title="5-digit ZIP code"
/>

<!-- Username: letters, numbers, underscore only, 3-16 chars -->
<input
	pattern="[a-zA-Z0-9_]{3,16}"
	title="3-16 characters, letters, numbers, and underscores only"
/>

<!-- Hex color: #fff or #ffffff -->
<input
	pattern="#[0-9a-fA-F]{3}([0-9a-fA-F]{3})?"
	title="Hex color like #fff or #ffffff"
/>
```

### Pattern Tips

✅ **Do:**

-   Keep patterns simple and forgiving
-   Always include helpful `title` text
-   Test thoroughly with real user input
-   Allow reasonable variations (spaces, dashes, etc.)

❌ **Don't:**

-   Make patterns too strict (rejects valid input)
-   Use regex-only error messages
-   Forget to test edge cases
-   Use patterns when built-in types work (`type="email"` instead of email pattern)

### The `title` Attribute

The `title` attribute does two things:

1. Shows as a tooltip when hovering over the field
2. Displays in the browser's validation error message

```html
<!-- Without title: unhelpful error -->
<input pattern="[0-9]{3}-[0-9]{4}" />
<!-- Error: "Please match the requested format" -->

<!-- With title: helpful error -->
<input
	pattern="[0-9]{3}-[0-9]{4}"
	title="Format: 123-4567"
/>
<!-- Error: "Please match the requested format: Format: 123-4567" -->
```

### ✏️ Quick Practice 2

In `validation-template.html`, add pattern validation to the phone field:

1. Add this pattern: `[\(]?[0-9]{3}[\)]?[\s\-]?[0-9]{3}[\s\-]?[0-9]{4}`
2. Add a helpful `title` attribute
3. Test with different phone formats: (123) 456-7890, 123-456-7890, 1234567890

<details>
<summary>📖 Show Solution</summary>

```html
<div class="form-field">
	<label for="phone">Phone Number (Optional)</label>
	<input
		id="phone"
		name="phone"
		type="tel"
		pattern="[\(]?[0-9]{3}[\)]?[\s\-]?[0-9]{3}[\s\-]?[0-9]{4}"
		title="Format: (123) 456-7890 or 123-456-7890"
		placeholder="(123) 456-7890"
	/>
</div>
```

</details>

### 🧠 Knowledge Check 2

<details>
<summary>Q1: When should I use <code>pattern</code> vs. specific input types?</summary>

**Answer:**

**Use built-in types first:**

-   `type="email"` for emails (better than email pattern)
-   `type="url"` for URLs
-   `type="tel"` for phone numbers (even without pattern)
-   `type="number"` for numbers

**Use pattern when:**

-   You need a specific format (ZIP codes, product codes)
-   Built-in validation isn't strict enough
-   You're validating text patterns (usernames, IDs)

Built-in types give you mobile keyboard improvements for free!

</details>

<details>
<summary>Q2: What regex characters need escaping in patterns?</summary>

**Answer:**

Common characters that need escaping with backslash `\`:

-   `\(` and `\)` - Parentheses
-   `\[` and `\]` - Square brackets
-   `\.` - Period/dot
-   `\-` - Dash (in some contexts)

Example:

```html
<!-- Phone with parentheses and dashes -->
<input pattern="[\(]?[0-9]{3}[\)]?[\-]?[0-9]{3}[\-]?[0-9]{4}" />
```

</details>

<details>
<summary>Q3: How can I make a pattern case-insensitive?</summary>

**Answer:**

Include both uppercase and lowercase in your pattern:

```html
<!-- Case-insensitive letters -->
<input pattern="[a-zA-Z]+" />

<!-- Or for specific words -->
<input pattern="[Yy][Ee][Ss]|[Nn][Oo]" />
```

HTML patterns don't support regex flags like `/i`, so you must include both cases explicitly.

</details>

---

## Part 3: ARIA & Accessible Validation (20 minutes)

### Why ARIA for Validation?

HTML validation works, but screen reader users need **context**:

-   What format is expected?
-   Is this field required?
-   What went wrong if there's an error?

ARIA (Accessible Rich Internet Applications) attributes help communicate this.

### The `aria-describedby` Attribute

Connects help text to an input so screen readers announce it:

```html
<label for="email">Email Address</label>
<input
	id="email"
	name="email"
	type="email"
	required
	aria-describedby="email-help"
/>
<small id="email-help">We'll never share your email with anyone</small>
```

**What screen readers announce:**
"Email Address, required, edit text, We'll never share your email with anyone"

### Multiple Descriptions

You can reference multiple help elements:

```html
<label for="password">Password</label>
<input
	id="password"
	name="password"
	type="password"
	required
	minlength="8"
	aria-describedby="password-help password-requirements"
/>
<small id="password-help">Choose a strong password</small>
<small id="password-requirements">
	At least 8 characters with letters and numbers
</small>
```

### Error Messages with `aria-live`

For dynamic error messages that appear after validation:

```html
<label for="email">Email</label>
<input
	id="email"
	name="email"
	type="email"
	required
	aria-describedby="email-help email-error"
/>
<small id="email-help">Enter a valid email address</small>
<small
	id="email-error"
	aria-live="polite"
	role="alert"
></small>
```

When an error appears, JavaScript can update `email-error`, and it will be announced:

```javascript
// After validation fails
document.getElementById('email-error').textContent =
	'Please enter a valid email address with an @ symbol';
```

**Key ARIA attributes:**

-   `aria-live="polite"` - Announces changes when user is idle
-   `role="alert"` - Marks this as an important message
-   Both together ensure screen readers announce errors

### Visual Indicators with `aria-invalid`

Mark fields as invalid (usually done with JavaScript):

```html
<input
	id="email"
	type="email"
	aria-invalid="true"
	aria-describedby="email-error"
/>
```

This tells assistive tech that the field has an error.

### ✏️ Quick Practice 3

In `validation-template.html`, add `aria-describedby` to connect help text:

1. Add `aria-describedby="name-help"` to the name input
2. Add `aria-describedby="email-help"` to the email input
3. Add `aria-describedby="phone-help"` to the phone input
4. Add `aria-describedby="message-help"` to the message textarea

<details>
<summary>📖 Show Solution</summary>

```html
<div class="form-field">
	<label for="name">Full Name</label>
	<input
		id="name"
		name="name"
		type="text"
		required
		minlength="2"
		maxlength="50"
		aria-describedby="name-help"
	/>
	<small
		id="name-help"
		class="help-text"
	>
		Please enter your first and last name (2-50 characters)
	</small>
</div>

<div class="form-field">
	<label for="email">Email Address</label>
	<input
		id="email"
		name="email"
		type="email"
		required
		aria-describedby="email-help"
	/>
	<small
		id="email-help"
		class="help-text"
	>
		We'll never share your email with anyone
	</small>
</div>
```

</details>

### 🧠 Knowledge Check 3

<details>
<summary>Q1: What's the difference between <code>aria-describedby</code> and <code>aria-labelledby</code>?</summary>

**Answer:**

-   **`aria-labelledby`** - Provides the field's **label** (alternative to `<label>`)
-   **`aria-describedby`** - Provides **additional description/help text**

Use `<label>` for labels (better for accessibility).
Use `aria-describedby` for help text and error messages.

```html
<!-- Good: label element + description -->
<label for="email">Email</label>
<input
	id="email"
	aria-describedby="email-help"
/>
<small id="email-help">Help text here</small>
```

</details>

<details>
<summary>Q2: Why use <code>aria-live="polite"</code> instead of <code>"assertive"</code>?</summary>

**Answer:**

-   **`polite`** - Waits until user is idle, then announces
-   **`assertive`** - Interrupts immediately

Use `polite` for most errors—it's less disruptive. Only use `assertive` for critical alerts (like "Session expiring in 1 minute").

Form validation errors should be `polite` so they don't interrupt while the user is typing.

</details>

<details>
<summary>Q3: Is placeholder text announced by screen readers?</summary>

**Answer:**

**No!** Placeholder text is NOT reliable for accessibility:

-   Some screen readers ignore it
-   It disappears when typing starts
-   Low contrast makes it hard to read

**Always use `<label>` and `aria-describedby` for important information.**

```html
<!-- Bad: placeholder only -->
<input placeholder="Enter your email" />

<!-- Good: label + help text + placeholder -->
<label for="email">Email</label>
<input
	id="email"
	placeholder="you@example.com"
	aria-describedby="email-help"
/>
<small id="email-help">We'll never share your email</small>
```

</details>

---

## Part 4: Hands-On Practice (40 minutes)

### Practice Exercise: Validate a Contact Form

**Your mission:** Enhance the contact form in `validation-template.html` with complete validation.

#### Requirements:

**Contact Information Fieldset:**

1. ✅ Name: Required, 2-50 characters
2. ✅ Email: Required, email type
3. ✅ Phone: Optional, pattern for (123) 456-7890 format

**Your Message Fieldset:**

4. ✅ Subject: Optional, max 100 characters
5. ✅ Message: Required, minimum 10 characters

**Accessibility:**

6. ✅ All fields have `aria-describedby` connecting to help text
7. ✅ All help text has unique `id` attributes
8. ✅ Required fields are clearly marked

**Testing:**

9. ✅ Form works with keyboard only (Tab, Enter, Space)
10. ✅ Validation errors are clear and helpful

### Step-by-Step Guide

**Step 1:** Add validation attributes to name field

```html
<input
	id="name"
	name="name"
	type="text"
	required
	minlength="2"
	maxlength="50"
	aria-describedby="name-help"
/>
```

**Step 2:** Add email validation

```html
<input
	id="email"
	name="email"
	type="email"
	required
	aria-describedby="email-help"
/>
```

**Step 3:** Add phone pattern (optional field)

```html
<input
	id="phone"
	name="phone"
	type="tel"
	pattern="[\(]?[0-9]{3}[\)]?[\s\-]?[0-9]{3}[\s\-]?[0-9]{4}"
	title="Format: (123) 456-7890 or 123-456-7890"
	aria-describedby="phone-help"
/>
```

**Step 4:** Add subject constraints

```html
<input
	id="subject"
	name="subject"
	type="text"
	maxlength="100"
	aria-describedby="subject-help"
/>
```

**Step 5:** Add message validation

```html
<textarea
	id="message"
	name="message"
	required
	minlength="10"
	maxlength="1000"
	aria-describedby="message-help"
></textarea>
```

**Step 6:** Test your form!

1. Try submitting with empty required fields → Should show error
2. Enter "test" in email → Should reject invalid format
3. Enter valid data → Should submit successfully
4. Use Tab key to navigate → All fields should be reachable
5. Click labels → Should focus corresponding inputs

### Compare with Solution

Open `validated-form-solution.html` in your browser to see a complete working example. Compare your code with the solution.

**Key differences to look for:**

-   Are all validation attributes present?
-   Is `aria-describedby` on every field?
-   Do all help text elements have unique IDs?
-   Are required fields marked visually?

---

## 🎨 Bonus: Styling Validation States

Want to add visual feedback? Use CSS pseudo-classes:

```css
/* Valid input - green border */
input:valid {
	border-color: #28a745;
}

/* Invalid input - red border (only after interaction) */
input:invalid:not(:placeholder-shown) {
	border-color: #dc3545;
	background-color: #fff5f5;
}

/* Required fields - orange left border */
input:required {
	border-left: 4px solid #ffc107;
}

/* Focus state */
input:focus {
	outline: none;
	box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
}
```

**Note:** The `:not(:placeholder-shown)` prevents showing errors before the user types anything.

---

## 🚨 Common Mistakes & Troubleshooting

### Mistake 1: Pattern Without Title

```html
<!-- ❌ Bad: No explanation -->
<input pattern="[0-9]{5}" />

<!-- ✅ Good: Helpful title -->
<input
	pattern="[0-9]{5}"
	title="5-digit ZIP code"
/>
```

### Mistake 2: Missing `aria-describedby`

```html
<!-- ❌ Bad: Help text not connected -->
<input
	id="email"
	type="email"
/>
<small id="email-help">Enter valid email</small>

<!-- ✅ Good: Connected with aria-describedby -->
<input
	id="email"
	type="email"
	aria-describedby="email-help"
/>
<small id="email-help">Enter valid email</small>
```

### Mistake 3: Using Placeholder as Label

```html
<!-- ❌ Bad: No visible label -->
<input
	placeholder="Email"
	type="email"
/>

<!-- ✅ Good: Label + placeholder -->
<label for="email">Email</label>
<input
	id="email"
	type="email"
	placeholder="you@example.com"
/>
```

### Mistake 4: Too Strict Patterns

```html
<!-- ❌ Bad: Rejects valid phone numbers with spaces -->
<input
	pattern="[0-9]{10}"
	title="Phone number"
/>

<!-- ✅ Good: Allows multiple formats -->
<input
	pattern="[\(]?[0-9]{3}[\)]?[\s\-]?[0-9]{3}[\s\-]?[0-9]{4}"
	title="Format: (123) 456-7890 or 123-456-7890"
/>
```

### Mistake 5: Forgetting Server Validation

```html
<!-- Client-side validation can be bypassed! -->
<!-- Always validate on the server too -->
```

### Debugging Tips

1. **Validation not working?**

    - Check if `type`, `pattern`, `required` are spelled correctly
    - Verify pattern regex is valid
    - Look for typos in attribute names

2. **Screen reader not announcing help text?**

    - Verify `aria-describedby` matches the help element's `id`
    - Check that help element actually has an `id`
    - Ensure IDs are unique

3. **Pattern always failing?**

    - Test your regex at [regex101.com](https://regex101.com/)
    - Remember: patterns must match the ENTIRE value
    - Check for special characters that need escaping

4. **Form submits despite errors?**
    - Ensure `<button type="submit">` (not just `<button>`)
    - Check if JavaScript is preventing default behavior
    - Verify inputs are inside the `<form>` tag

---

## 📚 Summary & Key Takeaways

### Validation Attributes You Learned

| Attribute      | Purpose                       | Example                           |
| -------------- | ----------------------------- | --------------------------------- |
| `required`     | Field must be filled          | `<input required>`                |
| `type="email"` | Email format validation       | `<input type="email">`            |
| `minlength`    | Minimum characters            | `<input minlength="3">`           |
| `maxlength`    | Maximum characters            | `<input maxlength="50">`          |
| `min`          | Minimum value (numbers/dates) | `<input type="number" min="18">`  |
| `max`          | Maximum value (numbers/dates) | `<input type="number" max="120">` |
| `pattern`      | Custom regex validation       | `<input pattern="[0-9]{5}">`      |
| `title`        | Help text for pattern         | `<input title="5-digit ZIP">`     |

### ARIA Attributes You Learned

| Attribute            | Purpose                   | Example                           |
| -------------------- | ------------------------- | --------------------------------- |
| `aria-describedby`   | Connects help text        | `<input aria-describedby="help">` |
| `aria-live="polite"` | Announces dynamic changes | `<div aria-live="polite">`        |
| `aria-invalid`       | Marks field as invalid    | `<input aria-invalid="true">`     |
| `role="alert"`       | Marks important message   | `<div role="alert">`              |

### Best Practices Checklist

-   ✅ Use specific input types (`email`, `tel`, `url`, `number`)
-   ✅ Provide helpful `title` attributes for patterns
-   ✅ Connect help text with `aria-describedby`
-   ✅ Mark required fields visually (\*, red border, etc.)
-   ✅ Show clear, actionable error messages
-   ✅ Test with keyboard navigation
-   ✅ Test with screen readers (if possible)
-   ✅ Always validate on the server too!

---

## 🎯 Homework Challenge (30-45 minutes)

Create a registration form with the following validated fields:

### Required Fields:

1. **Username**

    - Required
    - 3-16 characters
    - Pattern: letters, numbers, and underscores only
    - Help text: "Choose a unique username (3-16 characters, letters, numbers, \_ only)"

2. **Email**

    - Required
    - Email type
    - Help text: "We'll send a confirmation to this address"

3. **Password**

    - Required
    - Minimum 8 characters
    - Help text: "At least 8 characters recommended"

4. **Age**
    - Required
    - Number type
    - Min: 13, Max: 120
    - Help text: "You must be 13 or older to register"

### Optional Fields:

5. **Website**

    - Optional
    - URL type
    - Help text: "Personal website or portfolio (optional)"

6. **Bio**
    - Optional
    - Textarea
    - Max 500 characters
    - Help text: "Tell us about yourself (max 500 characters)"

### Requirements:

-   ✅ All fields have proper labels with `for`/`id` connection
-   ✅ All fields have help text connected via `aria-describedby`
-   ✅ Username pattern includes helpful `title` attribute
-   ✅ Required fields marked visually with \* or color
-   ✅ Form uses fieldsets to group related fields
-   ✅ Submit button present
-   ✅ Works with keyboard navigation

### Bonus Challenges:

-   Add CSS styling for `:valid` and `:invalid` states
-   Add custom JavaScript validation messages
-   Create a "password strength" indicator
-   Add a "Confirm Password" field that matches the password

---

## 📖 Additional Resources

### Documentation

-   [MDN: Client-side Form Validation](https://developer.mozilla.org/docs/Learn/Forms/Form_validation)
-   [MDN: Constraint Validation API](https://developer.mozilla.org/docs/Web/API/Constraint_validation)
-   [W3C: ARIA Authoring Practices - Forms](https://www.w3.org/WAI/ARIA/apg/patterns/)
-   [WebAIM: Creating Accessible Forms](https://webaim.org/techniques/forms/)

### Tools

-   [Regex101](https://regex101.com/) - Test your patterns
-   [WAVE Browser Extension](https://wave.webaim.org/extension/) - Check accessibility
-   [HTML Validator](https://validator.w3.org/) - Validate your HTML

### Cheat Sheets

-   **In this folder:** `validation-cheat-sheet.md`
-   **Previous sessions:** `forms-cheat-sheet.md`, `table-cheat-sheet.md`

---

## 🎉 Congratulations!

You've completed Form Validation! You can now:

-   ✅ Add HTML5 validation to any form
-   ✅ Use patterns for custom validation
-   ✅ Make forms accessible with ARIA
-   ✅ Provide helpful error messages
-   ✅ Create keyboard-friendly validated forms

### What's Next?

-   **Week 03:** Introduction to CSS and styling
-   **Future sessions:** JavaScript form validation, Ajax submissions, and more!

Keep practicing, and remember: **always validate on the server too!**

---

**Navigation:** [← Session 05](session-05.md) | [Week 02 Index](README.md) | [Week 03 →](../week-03/session-07.md)
