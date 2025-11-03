# Week 02 — Session 06: Forms II — Validation & Accessibility

Navigation

-   Back to Learning Plan: ../learning-plan.md
-   Week 02 Index: ../week-02.md
-   Prev: session-05.md
-   Next: ../week-03/session-07.md

Session length: 90 minutes

Pre-class checklist

-   Open your Session 05 contact form
-   Skim MDN’s client-side form validation guide (links below)

Learning objectives

-   Use built-in HTML validation attributes (`required`, `min`, `max`, `minlength`, `maxlength`, `pattern`)
-   Provide helpful error messages and instructions
-   Ensure forms are keyboard and screen-reader friendly

Materials

-   MDN: Client-side form validation — [MDN Validation](https://developer.mozilla.org/docs/Learn/Forms/Form_validation)
-   WAI: Labels and instructions — [WAI Forms Labels](https://www.w3.org/WAI/tutorials/forms/labels/)

Key terms

-   constraint validation, required, pattern, minlength, aria-describedby, invalid, help text

You will build

-   An enhanced contact form with built-in validation and associated help/error text

## 1) HTML validation (25m)

Start by layering constraints on existing fields.

```html
<form>
	<label for="name">Name</label>
	<input
		id="name"
		name="name"
		type="text"
		required
		minlength="2"
	/>

	<label for="email">Email</label>
	<input
		id="email"
		name="email"
		type="email"
		required
	/>

	<label for="phone">Phone (optional)</label>
	<input
		id="phone"
		name="phone"
		type="tel"
		pattern="^[0-9\-\s\(\)]+$"
		title="Use digits, spaces, parentheses, and dashes only"
	/>

	<button type="submit">Send</button>
</form>
```

Notes

-   Browsers provide default messages; you can customize with `title` and help text
-   Use appropriate `type` (e.g., `email`) to get free validation and better mobile keyboards

## 2) Error UX and help text (15m)

Associate instructions and errors with inputs via `aria-describedby`.

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

Notes

-   Keep help text visible by default; reserve `aria-live` regions for dynamic error/status updates
-   Ensure the described elements have unique `id`s and are referenced on the input

## 3) Guided lab (40m)

Goal: Enhance the Session 05 contact form with validation and help text.

Steps

1. Make `name` and `email` required; set sensible length limits
2. Use `type="email"` for email; consider a basic `pattern` for telephone if you added it
3. Add help text beneath each input, and connect via `aria-describedby`
4. Add a brief instruction near the submit button (e.g., required fields note)

Checklist

-   [ ] Required fields are marked with `required`
-   [ ] Inputs use the most specific `type` available
-   [ ] Help text and/or error text is associated via `aria-describedby`
-   [ ] Title or pattern messages are user-friendly (no regex-only messages)

Knowledge checks

-   Q: What are the pros/cons of `pattern` compared to appropriate input `type`?
-   Q: How does `aria-describedby` improve the screen reader experience?

Common pitfalls

-   Overly strict `pattern` that blocks valid input
-   Missing `name` attributes (the form may look fine but sends nothing)
-   Help text present but not referenced (not read by screen readers)

Homework (30–45 minutes)

-   Exercise: Add validation to your feedback form from Session 05.
-   Acceptance criteria:
    -   [ ] Required fields marked and enforced by the browser
    -   [ ] Helpful instructions (help text) for at least two fields
    -   [ ] Inputs use specific types and constraints (`type`, `minlength`, `maxlength`, `pattern` when reasonable)
    -   [ ] Help text is connected via `aria-describedby`

Troubleshooting

-   Browser messages differ? That’s normal; supplement with clear help text via `aria-describedby` and `title`
-   Screen reader doesn’t announce the help/error? Verify the `aria-describedby` IDs match

Navigation

-   Back: ../learning-plan.md
-   Week 02 Index: ../week-02.md
-   Prev: session-05.md
-   Next: ../week-03/session-07.md
