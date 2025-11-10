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

## Part 1: Understanding Form Basics (25 minutes)

### What Is a Form?

An HTML form is a section of a document that contains interactive controls for submitting information. Every form you've ever filled out online—whether creating an account, searching Google, or leaving a comment—uses HTML forms.

**Forms are made up of:**

-   The `<form>` element (the container)
-   Input controls (text boxes, checkboxes, buttons, etc.)
-   Labels (text that describes each control)
-   Submit buttons (to send the data)

### Your First Form: Step by Step

Let's build a form from scratch. We'll start with the absolute minimum and add complexity gradually.

#### Step 1: Create the Form Container

Every form starts with a `<form>` element:

```html
<form>
	<!-- Form controls will go here -->
</form>
```

That's it! A form is just a container. Now let's add controls.

#### Step 2: Add a Text Input

A text input is the most basic form control:

```html
<form>
	<input type="text" />
</form>
```

Try this in your browser. You'll see a text box, but there's a problem: **there's no label!** Users (and screen readers) won't know what this field is for.

#### Step 3: Add a Label

Labels tell users what each field is for. Here's the **wrong** way and the **right** way:

**❌ Wrong: No connection between label and input**

```html
<form>
	<label>Name</label>
	<input type="text" />
</form>
```

**✅ Right: Label connected via `for` and `id`**

```html
<form>
	<label for="name">Name</label>
	<input
		id="name"
		type="text"
	/>
</form>
```

**Why this matters:** When you click on the label text "Name", the input field gets focus. This makes forms easier to use, especially on mobile devices. Screen readers also announce the label when the field is focused.

> **The Golden Rule:** The `for` attribute on the `<label>` must **exactly match** the `id` attribute on the input.

#### Step 4: Add the `name` Attribute

The `name` attribute is what gets sent to the server when the form is submitted:

```html
<form>
	<label for="name">Name</label>
	<input
		id="name"
		name="name"
		type="text"
	/>
</form>
```

**Understanding `id` vs `name`:**

-   `id` — Used to connect the label to the input (accessibility)
-   `name` — Used to identify the data when the form is submitted (functionality)

They often have the same value, but they serve different purposes!

#### Step 5: Build a Complete Contact Form

Now let's put it all together with multiple fields:

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

**What's happening here:**

1. Each field is wrapped in a `<div>` for organization (you could also use `<p>` or just line breaks)
2. Each `<label>` has a `for` attribute matching its input's `id`
3. Each input has a `name` (this is what gets submitted)
4. We use `type="email"` for the email field (gives us mobile keyboard optimization and basic validation)
5. `<textarea>` is used for multi-line text (messages, comments, etc.)
6. The submit button has `type="submit"` (this is the default, but being explicit is good practice)

### Common Input Types

Here are the most common input types you'll use:

| Type       | Purpose               | Example             |
| ---------- | --------------------- | ------------------- |
| `text`     | Single-line text      | Name, username      |
| `email`    | Email addresses       | user@example.com    |
| `password` | Password (hides text) | •••••••••           |
| `tel`      | Phone numbers         | (555) 123-4567      |
| `number`   | Numeric input         | Age, quantity       |
| `date`     | Date picker           | 2025-11-10          |
| `url`      | Website URLs          | https://example.com |
| `search`   | Search queries        | "Find products..."  |

### The Placeholder Trap ⚠️

You might be tempted to use placeholders instead of labels:

**❌ DON'T DO THIS:**

```html
<input
	type="text"
	placeholder="Enter your name"
/>
<!-- No label! Bad for accessibility! -->
```

**✅ DO THIS INSTEAD:**

```html
<label for="name">Name</label>
<input
	id="name"
	name="name"
	type="text"
	placeholder="e.g., Jane Smith"
/>
<!-- Label + placeholder is fine -->
```

**Why placeholders alone are bad:**

-   They disappear when you start typing
-   They're often too low-contrast to read
-   Screen readers might not announce them
-   They're not a replacement for proper labels

> **Rule:** Always use a visible `<label>`. Placeholders can provide examples, but they're optional extras.

---

### 🎯 Quick Practice 1

Create a simple login form with:

1. A label and input for "Username" (text type)
2. A label and input for "Password" (password type)
3. A submit button that says "Log In"

Make sure each input has an `id`, `name`, and is connected to its label!

<details>
<summary>Click to see solution</summary>

```html
<form>
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

	<button type="submit">Log In</button>
</form>
```

</details>

---

## Part 2: Organizing Forms with Fieldsets (15 minutes)

### Why Group Form Fields?

As forms get longer, they become harder to use. Grouping related fields helps users understand the form's structure and makes it more accessible.

**Example:** A registration form might have:

-   Personal information (name, age, gender)
-   Contact details (email, phone, address)
-   Account settings (username, password)

Each of these is a logical group!

### Enter `<fieldset>` and `<legend>`

The `<fieldset>` element groups related controls, and `<legend>` provides a title for the group.

**Basic structure:**

```html
<fieldset>
	<legend>Group Title</legend>
	<!-- Related form controls go here -->
</fieldset>
```

**Visual benefit:** Browsers usually draw a border around fieldsets, making the grouping visible.

**Accessibility benefit:** Screen readers announce the legend when entering the fieldset, providing context for all controls inside.

### Example: Registration Form with Fieldsets

Let's organize a registration form into logical sections:

```html
<form>
	<fieldset>
		<legend>Personal Information</legend>

		<div>
			<label for="first-name">First name</label>
			<input
				id="first-name"
				name="first_name"
				type="text"
			/>
		</div>

		<div>
			<label for="last-name">Last name</label>
			<input
				id="last-name"
				name="last_name"
				type="text"
			/>
		</div>

		<div>
			<label for="birth-date">Date of birth</label>
			<input
				id="birth-date"
				name="birth_date"
				type="date"
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

	<fieldset>
		<legend>Account Setup</legend>

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
	</fieldset>

	<button type="submit">Create Account</button>
</form>
```

**Notice:**

-   Each `<fieldset>` groups related information
-   Each `<legend>` clearly describes what the group contains
-   All the label/input patterns we learned earlier still apply inside fieldsets

### When to Use Fieldsets

**✅ Use fieldsets for:**

-   Multi-section forms (registration, checkout, surveys)
-   Forms with distinct categories of information
-   Radio button groups (we'll cover these in Session 06)
-   Checkbox groups

**❌ Don't use fieldsets for:**

-   Very simple forms (1-3 fields)
-   Single-section forms
-   Every single field (over-grouping makes forms harder to scan)

### Example: Contact Form with Fieldsets

Here's a well-organized contact form:

```html
<form>
	<fieldset>
		<legend>Your Information</legend>

		<div>
			<label for="full-name">Full name</label>
			<input
				id="full-name"
				name="full_name"
				type="text"
			/>
		</div>

		<div>
			<label for="email">Email address</label>
			<input
				id="email"
				name="email"
				type="email"
			/>
		</div>
	</fieldset>

	<fieldset>
		<legend>Your Message</legend>

		<div>
			<label for="subject">Subject</label>
			<input
				id="subject"
				name="subject"
				type="text"
			/>
		</div>

		<div>
			<label for="message">Message</label>
			<textarea
				id="message"
				name="message"
				rows="5"
			></textarea>
		</div>
	</fieldset>

	<button type="submit">Send Message</button>
</form>
```

---

### 🎯 Quick Practice 2

Add fieldsets to organize this form into two groups: "Shipping Address" and "Payment Information":

```html
<form>
	<label for="street">Street address</label>
	<input
		id="street"
		name="street"
		type="text"
	/>

	<label for="city">City</label>
	<input
		id="city"
		name="city"
		type="text"
	/>

	<label for="card-number">Card number</label>
	<input
		id="card-number"
		name="card_number"
		type="text"
	/>

	<label for="cvv">CVV</label>
	<input
		id="cvv"
		name="cvv"
		type="text"
	/>

	<button type="submit">Complete Order</button>
</form>
```

<details>
<summary>Click to see solution</summary>

```html
<form>
	<fieldset>
		<legend>Shipping Address</legend>

		<div>
			<label for="street">Street address</label>
			<input
				id="street"
				name="street"
				type="text"
			/>
		</div>

		<div>
			<label for="city">City</label>
			<input
				id="city"
				name="city"
				type="text"
			/>
		</div>
	</fieldset>

	<fieldset>
		<legend>Payment Information</legend>

		<div>
			<label for="card-number">Card number</label>
			<input
				id="card-number"
				name="card_number"
				type="text"
			/>
		</div>

		<div>
			<label for="cvv">CVV</label>
			<input
				id="cvv"
				name="cvv"
				type="text"
			/>
		</div>
	</fieldset>

	<button type="submit">Complete Order</button>
</form>
```

</details>

---

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

## Homework Assignment (30–45 minutes)

### Project: Create a Feedback Form for Your Website

Add a feedback form to one of your HTML pages from Week 01 (or create a new page).

**Requirements:**

**Section 1: About You**

-   Your name (text input)
-   Your email (email input)

**Section 2: Feedback**

-   Rating (we'll keep it simple with a text input for now—we'll learn better options in Session 06)
-   Comments (textarea with at least 4 rows)

**Additional Requirements:**

-   [ ] Form has two fieldsets with appropriate legends
-   [ ] Every input has a visible label
-   [ ] All labels are connected using `for`/`id`
-   [ ] All inputs have `name` attributes
-   [ ] Submit button says "Submit Feedback"
-   [ ] No placeholder-only labels
-   [ ] Optional: Add some basic CSS to make it look nice

**Bonus challenges:**

-   Add a "Website URL" field using `type="url"`
-   Add a "Date of experience" field using `type="date"`
-   Include helpful placeholder text as examples (but keep the labels!)

### Submission

Save your file as `feedback-form.html`.

**Self-grading checklist:**

1. Does every field have a label?
2. Can you click each label to focus its input?
3. Do all fields have `name` attributes?
4. Are related fields grouped in fieldsets?
5. Is the form organized and easy to understand?

---

## Troubleshooting Guide

### Problem: Clicking the label doesn't focus the input

**Cause:** The `for` attribute doesn't match the `id`, or one is missing.

**Solution:**

```html
<!-- Check that these match EXACTLY -->
<label for="email">Email</label>
<input
	id="email"
	name="email"
	type="email"
/>
```

### Problem: Form submits but data is empty

**Cause:** Missing `name` attributes.

**Solution:** Add `name` to every input:

```html
<input
	id="username"
	name="username"
	type="text"
/>
<!--                   ^^^^^^^^^^^^^^ This is required! -->
```

### Problem: Screen reader doesn't announce the label

**Cause:** Either missing `for`/`id` connection or using placeholder instead of label.

**Solution:** Always use a proper label:

```html
<!-- ✅ Good -->
<label for="phone">Phone</label>
<input
	id="phone"
	name="phone"
	type="tel"
/>

<!-- ❌ Bad -->
<input
	type="tel"
	placeholder="Phone"
/>
```

### Problem: Fieldset border looks ugly

**Cause:** Default browser styling.

**Solution:** Add CSS to customize:

```css
fieldset {
	border: 1px solid #ddd;
	border-radius: 4px;
	padding: 15px;
	margin-bottom: 20px;
}

legend {
	font-weight: bold;
	padding: 0 10px;
}
```

---

## Congratulations! 🎉

You've completed Forms I! You now know:

✅ How to create accessible forms with proper labels
✅ The difference between `id` and `name`
✅ How to use different input types
✅ How to organize forms with fieldsets and legends
✅ Why placeholders aren't replacements for labels

**Next Steps:**

-   Practice by building different types of forms
-   Move on to Session 06: Forms II — Validation & Accessibility
-   Learn about radio buttons, checkboxes, and select menus

**Additional Learning Resources:**

-   [MDN: Your First Form](https://developer.mozilla.org/docs/Learn/Forms/Your_first_form)
-   [MDN: How to Structure a Form](https://developer.mozilla.org/docs/Learn/Forms/How_to_structure_a_web_form)
-   [WebAIM: Creating Accessible Forms](https://webaim.org/techniques/forms/)

---

Navigation

-   Back: ../learning-plan.md
-   Week 02 Index: ../week-02.md
-   Prev: session-04.md
-   Next: session-06.md
