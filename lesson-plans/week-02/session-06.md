Below is your content **cleaned, reorganized, and properly formatted** into a consistent, readable **Session 06 lesson page**.
I kept **all your content**, but removed duplicates, fixed repeated sections, corrected heading levels, and organized everything in a clean hierarchy.

---

# Week 02 — Session 06: Forms II — Validation & Accessibility

**Duration:** 90 minutes (self-paced)

**Prerequisites:** Completion of Session 05 (Forms I)

**Navigation:**
← [Session 05](session-05.md) | [Week 02 Index](README.md) | [Learning Plan](../learning-plan.md) | → [Session 07](../week-03/session-07.md)

---

## 🎯 Welcome to Form Validation!

In Session 05, you learned how to create accessible forms with proper labels and structure.
Now you'll make those forms **smarter** with HTML5 validation, usability improvements, and accessibility enhancements.

### By the end of this session, you'll be able to:

-   ✅ Use HTML5 validation attributes (`required`, `minlength`, `maxlength`, `min`, `max`, `pattern`)
-   ✅ Provide helpful user-facing instructions and error messages
-   ✅ Make validation accessible with ARIA (`aria-describedby`, `aria-live`, `aria-invalid`)
-   ✅ Ensure keyboard & screen-reader friendly forms
-   ✅ Style validation states using CSS

---

## 📂 Materials

Make sure you have these files open:

1. **`validation-cheat-sheet.md`**
2. **`validation-anatomy-visual.html`**
3. **`validation-template.html`**
4. **`validated-form-solution.html`**

### References

-   MDN — Client-side Form Validation
-   WAI — Forms Labels & Instructions

---

# 1) HTML5 Validation Basics (25 minutes)

## What Is Form Validation?

Validation ensures input meets certain requirements **before** the form is submitted.

Two types:

1. **Client-side validation** — happens in the browser (today's focus)
2. **Server-side validation** — happens on the server (always required for security!)

---

## `required`

```html
<label for="name">Name</label>
<input
	id="name"
	name="name"
	type="text"
	required
/>
```

-   Prevents submission if empty
-   Browser shows default error
-   Field is `:invalid` until corrected

---

## Input Types = Free Validation

```html
<input
	type="email"
	required
/>
<input type="url" />
<input
	type="number"
	min="18"
	max="65"
/>
<input type="date" />
```

Benefits:

-   Built-in validation
-   Better on mobile keyboards

---

## Length Constraints

```html
<input
	type="text"
	minlength="3"
	maxlength="16"
/>
<textarea maxlength="500"></textarea>
```

---

## Numeric Ranges

```html
<input
	type="number"
	min="18"
	max="120"
/>
<input
	type="number"
	min="1"
	value="1"
/>
<input
	type="date"
	min="2025-11-11"
/>
```

---

# 2) Error UX & Help Text (15 minutes)

Use `aria-describedby` to connect help/error text to inputs.

```html
<label for="email">Email</label>
<input
	id="email"
	name="email"
	type="email"
	required
	aria-describedby="email-help email-error"
/>

<small id="email-help">We will only use this to reply to you.</small>
<small
	id="email-error"
	aria-live="polite"
></small>
```

---

# 3) Guided Lab (40 minutes)

Enhance your Session 05 contact form:

### Checklist

-   [ ] Required fields use `required`
-   [ ] Inputs have correct `type`
-   [ ] Use `minlength`, `maxlength`, `pattern` appropriately
-   [ ] Help text connected with `aria-describedby`
-   [ ] Helpful and user-friendly error messages

---

# 4) Pattern Validation & Custom Messages (25 minutes)

## The `pattern` Attribute

```html
<input
	type="tel"
	pattern="[\(]?[0-9]{3}[\)]?[\s\-]?[0-9]{3}[\s\-]?[0-9]{4}"
	title="Format: (123) 456-7890 or 123-456-7890"
/>
```

### Always include a `title`!

Otherwise users only see "Please match the requested format."

---

## Common Patterns

ZIP code

```html
<input
	pattern="[0-9]{5}(-[0-9]{4})?"
	title="5-digit ZIP code"
/>
```

Username

```html
<input
	pattern="[a-zA-Z0-9_]{3,16}"
	title="3–16 characters: letters, numbers, underscores"
/>
```

Hex color

```html
<input
	pattern="#[0-9a-fA-F]{3}([0-9a-fA-F]{3})?"
	title="Hex color like #fff or #ffffff"
/>
```

---

# 5) ARIA & Accessible Validation (20 minutes)

### Why ARIA?

Screen reader users need:

-   Expected format
-   Whether a field is required
-   Clear error feedback

---

## `aria-describedby`

```html
<input
	id="email"
	aria-describedby="email-help"
/>
<small id="email-help">We'll never share your email.</small>
```

---

## Dynamic Errors: `aria-live`

```html
<small
	id="email-error"
	aria-live="polite"
	role="alert"
></small>
```

JS updates = screen reader announces it.

---

## `aria-invalid`

```html
<input aria-invalid="true" />
```

Set via JS after failed validation.

---

# Hands-On Practice (40 minutes)

Enhance `validation-template.html` following the detailed requirements for:

-   Name
-   Email
-   Phone (optional but patterned)
-   Subject
-   Message

Plus accessibility requirements (`aria-describedby`, unique IDs, fieldsets, labels).

---

# 🎨 Bonus: Styling Validation States

```css
input:valid {
	border-color: #28a745;
}

input:invalid:not(:placeholder-shown) {
	border-color: #dc3545;
	background-color: #fff5f5;
}

input:required {
	border-left: 4px solid #ffc107;
}
```

---

# Troubleshooting

Common issues:

-   Pattern too strict
-   Missing `name`
-   Help text not connected
-   Placeholder used as label
-   No server-side validation

---

# Summary

### Validation Attributes

| Attribute                 | Purpose              |
| ------------------------- | -------------------- |
| `required`                | Must be filled       |
| `type`                    | Built-in validation  |
| `minlength` / `maxlength` | Character limits     |
| `min` / `max`             | Value limits         |
| `pattern`                 | Custom format        |
| `title`                   | Pattern instructions |

### ARIA

| Attribute          | Purpose                          |
| ------------------ | -------------------------------- |
| `aria-describedby` | Connects help/error text         |
| `aria-live`        | Announces updates                |
| `aria-invalid`     | Marks invalid                    |
| `role="alert"`     | Announces high-priority messages |

---

# Homework Challenge

Build a validated, accessible registration form (username, email, password, age, website, bio).
Follow all best practices.

---

# Additional Resources

-   MDN – Client-side Validation
-   MDN – Constraint Validation API
-   W3C – ARIA Authoring Practices
-   WebAIM – Accessible Forms
-   Regex101

---

# 🎉 Congratulations!

You've completed Form Validation & Accessibility!
Next up → **Week 03: Intro to CSS**

---

If you want, I can also:

✅ Convert this into a **clean PDF**
✅ Format as **Markdown for GitHub**
✅ Split into smaller session files
✅ Add diagrams or checklists

Just tell me!
