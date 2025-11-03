# Week 02 — Session 05: Forms I — Inputs and Labels

Navigation

-   Back to Learning Plan: ../learning-plan.md
-   Week 02 Index: ../week-02.md
-   Prev: session-04.md
-   Next: session-06.md

Session length: 90 minutes

Pre-class checklist

-   Open your project in VS Code and start Live Server
-   Skim MDN’s forms overview (links below)

Learning objectives

-   Create forms with `<form>`, `<label>`, and common inputs
-   Associate labels using `for` and `id`
-   Group related controls with `<fieldset>` and `<legend>`

Materials

-   MDN: Your first form — [MDN Forms Overview](https://developer.mozilla.org/docs/Learn/Forms/Your_first_form)
-   MDN: `<label>` — [MDN label](https://developer.mozilla.org/docs/Web/HTML/Element/label)

Key terms

-   form, action, method, label, input, textarea, select, option, id, for, name, value, fieldset, legend, placeholder

You will build

-   A contact form with properly associated labels and grouped fields

## 1) Form basics (25m)

Start with a minimal form. Note the `for`/`id` link between `<label>` and the input, and the `name` that becomes the key when the form is submitted.

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
	<!-- No action/method yet; we focus on semantics first -->
	<!-- Avoid placeholder-only labels; placeholders are not accessible labels -->
</form>
```

Notes

-   Each control has a unique `id`, and its `<label>` uses `for` to reference it
-   `name` is required for successful form submission
-   Prefer visible labels; placeholders are not a substitute for labels

## 2) Fieldsets and semantics (15m)

Group related controls with `<fieldset>` and caption them with `<legend>`.

```html
<form>
	<fieldset>
		<legend>Contact details</legend>
		<label for="full-name">Full name</label>
		<input
			id="full-name"
			name="full_name"
			type="text"
		/>
		<label for="email">Email</label>
		<input
			id="email"
			name="email"
			type="email"
		/>
	</fieldset>
	<fieldset>
		<legend>Message</legend>
		<label for="subject">Subject</label>
		<input
			id="subject"
			name="subject"
			type="text"
		/>
		<label for="message">Message</label>
		<textarea
			id="message"
			name="message"
			rows="4"
		></textarea>
	</fieldset>
	<button type="submit">Send</button>
</form>
```

## 3) Guided lab (40m)

Goal: Build a contact form with labels and field grouping.

Requirements

-   At least four controls (name, email, subject, message)
-   Each control has a visible `<label>` tied to an `id`
-   Related controls grouped by `<fieldset>` with a meaningful `<legend>`

Checklist

-   [ ] Every input/textarea/select has a `<label>`
-   [ ] `for` and `id` match for each label/control pair
-   [ ] Every control has a `name`
-   [ ] Submit button present and descriptive

Knowledge checks

-   Q: Why is `name` required if we’re not submitting to a server yet?
-   Q: What’s the difference between a placeholder and a label?

Common pitfalls

-   Relying on placeholders instead of visible labels
-   Mismatched `for`/`id` values
-   Missing `name` attributes (data won’t submit)

Homework (30–45 minutes)

-   Exercise: Add a feedback form to your article page from Week 01.
-   Acceptance criteria:
    -   [ ] Includes name, email, and message
    -   [ ] All controls have labels associated via `for`/`id`
    -   [ ] Fields are grouped with fieldset/legend where appropriate
    -   [ ] No placeholder-only labels

Troubleshooting

-   Screen reader doesn’t announce the label? Ensure `for` exactly matches the control `id`.
-   Form submits empty values? Confirm each control has a `name`.

Navigation

-   Back: ../learning-plan.md
-   Week 02 Index: ../week-02.md
-   Prev: session-04.md
-   Next: session-06.md
