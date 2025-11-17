# Week 02 — HTML Extras: Additional Topics

**Navigation:**
← [Week 02 Index](README.md) | [Learning Plan](../learning-plan.md)

---

## 📚 Overview

This document covers additional HTML topics that complement the main Week 02 sessions but aren't required for the core curriculum. These are useful features you may encounter or need in real-world projects.

**Topics Covered:**

-   Select Dropdowns, Radio Buttons & Checkboxes
-   Multimedia Elements (Audio, Video, Picture)
-   Embedded Content (iframe, embed, object)
-   Data Lists and Advanced Form Controls
-   Meta Tags and SEO Basics
-   Special Characters and Entities
-   Definition Lists
-   Details and Summary Elements
-   Semantic Text Elements

---

## 1) Select Dropdowns, Radio Buttons & Checkboxes (35 minutes)

### The `<select>` Element

The `<select>` element creates a dropdown menu with options.

**Basic Dropdown:**

```html
<div>
	<label for="country">Country:</label>
	<select
		id="country"
		name="country"
	>
		<option value="">-- Select a country --</option>
		<option value="us">United States</option>
		<option value="uk">United Kingdom</option>
		<option value="ca">Canada</option>
		<option value="au">Australia</option>
	</select>
</div>
```

**Key Attributes:**

| Attribute  | Purpose                   | Example             |
| ---------- | ------------------------- | ------------------- |
| `id`       | Connects to label         | `id="country"`      |
| `name`     | Data sent to server       | `name="country"`    |
| `required` | Must select an option     | `<select required>` |
| `multiple` | Allow multiple selections | `<select multiple>` |
| `size`     | Number of visible options | `<select size="5">` |
| `disabled` | Cannot be changed         | `<select disabled>` |

**Individual Option Attributes:**

| Attribute  | Purpose                  | Example               |
| ---------- | ------------------------ | --------------------- |
| `value`    | Value sent when selected | `<option value="us">` |
| `selected` | Pre-selected by default  | `<option selected>`   |
| `disabled` | Cannot be selected       | `<option disabled>`   |

### The `<optgroup>` Element

Group related options together with a visible label.

```html
<label for="vehicle">Choose a vehicle:</label>
<select
	id="vehicle"
	name="vehicle"
>
	<option value="">-- Select a vehicle --</option>

	<optgroup label="Cars">
		<option value="sedan">Sedan</option>
		<option value="suv">SUV</option>
		<option value="coupe">Coupe</option>
	</optgroup>

	<optgroup label="Motorcycles">
		<option value="cruiser">Cruiser</option>
		<option value="sport">Sport Bike</option>
		<option value="touring">Touring</option>
	</optgroup>

	<optgroup label="Trucks">
		<option value="pickup">Pickup</option>
		<option value="semi">Semi Truck</option>
	</optgroup>
</select>
```

**Visual appearance:**

```
-- Select a vehicle --
Cars
  Sedan
  SUV
  Coupe
Motorcycles
  Cruiser
  Sport Bike
  Touring
Trucks
  Pickup
  Semi Truck
```

### Radio Buttons

Radio buttons allow users to select **one option** from a group.

**Basic Radio Group:**

```html
<fieldset>
	<legend>Choose your preferred contact method:</legend>

	<div>
		<input
			type="radio"
			id="contact-email"
			name="contact-method"
			value="email"
			checked
		/>
		<label for="contact-email">Email</label>
	</div>

	<div>
		<input
			type="radio"
			id="contact-phone"
			name="contact-method"
			value="phone"
		/>
		<label for="contact-phone">Phone</label>
	</div>

	<div>
		<input
			type="radio"
			id="contact-mail"
			name="contact-method"
			value="mail"
		/>
		<label for="contact-mail">Mail</label>
	</div>
</fieldset>
```

**Critical Rules for Radio Buttons:**

1. **Same `name` attribute**: All radio buttons in a group must have the **same** `name`
2. **Different `id` attributes**: Each radio button needs a **unique** `id`
3. **Different `value` attributes**: Each option should have a distinct `value`
4. **Use `<fieldset>` and `<legend>`**: Group related radio buttons semantically

**Why same `name`?**

-   Ensures only one option can be selected at a time
-   Groups the options together for form submission

**Example showing correct vs incorrect:**

```html
<!-- ✅ CORRECT: Same name, different IDs -->
<input
	type="radio"
	id="male"
	name="gender"
	value="male"
/>
<label for="male">Male</label>

<input
	type="radio"
	id="female"
	name="gender"
	value="female"
/>
<label for="female">Female</label>

<!-- ❌ WRONG: Different names - they won't work as a group! -->
<input
	type="radio"
	id="male"
	name="gender-male"
	value="male"
/>
<label for="male">Male</label>

<input
	type="radio"
	id="female"
	name="gender-female"
	value="female"
/>
<label for="female">Female</label>
```

**Attributes for Radio Buttons:**

| Attribute  | Purpose                       | Example                                |
| ---------- | ----------------------------- | -------------------------------------- |
| `type`     | Defines as radio button       | `type="radio"`                         |
| `id`       | Unique identifier for label   | `id="contact-email"`                   |
| `name`     | Groups radio buttons together | `name="contact-method"` (same for all) |
| `value`    | Value sent when selected      | `value="email"`                        |
| `checked`  | Pre-selected by default       | `checked`                              |
| `required` | At least one must be selected | `required` (on all in group)           |
| `disabled` | Cannot be selected            | `disabled`                             |

### Checkboxes

Checkboxes allow users to select **multiple options** or toggle a single option.

**Single Checkbox:**

```html
<div>
	<input
		type="checkbox"
		id="newsletter"
		name="newsletter"
		value="yes"
	/>
	<label for="newsletter">Subscribe to newsletter</label>
</div>
```

**Multiple Checkboxes (Related Group):**

```html
<fieldset>
	<legend>Select your interests:</legend>

	<div>
		<input
			type="checkbox"
			id="interest-tech"
			name="interests"
			value="technology"
		/>
		<label for="interest-tech">Technology</label>
	</div>

	<div>
		<input
			type="checkbox"
			id="interest-sports"
			name="interests"
			value="sports"
		/>
		<label for="interest-sports">Sports</label>
	</div>

	<div>
		<input
			type="checkbox"
			id="interest-music"
			name="interests"
			value="music"
		/>
		<label for="interest-music">Music</label>
	</div>

	<div>
		<input
			type="checkbox"
			id="interest-art"
			name="interests"
			value="art"
		/>
		<label for="interest-art">Art</label>
	</div>
</fieldset>
```

**Checkbox Attributes:**

| Attribute  | Purpose                     | Example                          |
| ---------- | --------------------------- | -------------------------------- |
| `type`     | Defines as checkbox         | `type="checkbox"`                |
| `id`       | Unique identifier for label | `id="interest-tech"`             |
| `name`     | Data identifier             | `name="interests"` (can be same) |
| `value`    | Value sent when checked     | `value="technology"`             |
| `checked`  | Pre-checked by default      | `checked`                        |
| `required` | Must be checked             | `required`                       |
| `disabled` | Cannot be changed           | `disabled`                       |

**Note:** Unlike radio buttons, checkboxes with the same `name` will submit multiple values.

### Radio vs. Checkbox: When to Use Each

| Use Radio Buttons                      | Use Checkboxes                             |
| -------------------------------------- | ------------------------------------------ |
| User must select **one** option        | User can select **multiple** options       |
| Options are mutually exclusive         | Options are independent                    |
| Examples: Gender, payment method, size | Examples: Interests, permissions, features |

### Complete Form Example with All Types

```html
<form
	action="/submit"
	method="POST"
>
	<h2>Registration Form</h2>

	<!-- Dropdown -->
	<div>
		<label for="country">Country:</label>
		<select
			id="country"
			name="country"
			required
		>
			<option value="">-- Select your country --</option>
			<option value="us">United States</option>
			<option value="uk">United Kingdom</option>
			<option value="ca">Canada</option>
			<option value="au">Australia</option>
		</select>
	</div>

	<!-- Radio buttons -->
	<fieldset>
		<legend>Membership Level:</legend>

		<div>
			<input
				type="radio"
				id="level-basic"
				name="membership"
				value="basic"
				checked
			/>
			<label for="level-basic">Basic (Free)</label>
		</div>

		<div>
			<input
				type="radio"
				id="level-premium"
				name="membership"
				value="premium"
			/>
			<label for="level-premium">Premium ($9.99/mo)</label>
		</div>

		<div>
			<input
				type="radio"
				id="level-pro"
				name="membership"
				value="pro"
			/>
			<label for="level-pro">Pro ($19.99/mo)</label>
		</div>
	</fieldset>

	<!-- Checkboxes -->
	<fieldset>
		<legend>Communication Preferences:</legend>

		<div>
			<input
				type="checkbox"
				id="comm-email"
				name="communications"
				value="email"
				checked
			/>
			<label for="comm-email">Email updates</label>
		</div>

		<div>
			<input
				type="checkbox"
				id="comm-sms"
				name="communications"
				value="sms"
			/>
			<label for="comm-sms">SMS notifications</label>
		</div>

		<div>
			<input
				type="checkbox"
				id="comm-newsletter"
				name="communications"
				value="newsletter"
			/>
			<label for="comm-newsletter">Monthly newsletter</label>
		</div>
	</fieldset>

	<!-- Single required checkbox -->
	<div>
		<input
			type="checkbox"
			id="terms"
			name="terms"
			value="accepted"
			required
		/>
		<label for="terms">I agree to the Terms and Conditions *</label>
	</div>

	<button type="submit">Register</button>
</form>
```

### Accessibility Best Practices

**DO:**

✅ Always use `<label>` elements with matching `for`/`id`
✅ Group related radio buttons and checkboxes with `<fieldset>` and `<legend>`
✅ Use the same `name` for all radio buttons in a group
✅ Provide a default empty option for select dropdowns (`<option value="">Select...</option>`)
✅ Use `required` attribute when selection is mandatory
✅ Put label text **after** the input for radio/checkbox (better click target)

**DON'T:**

❌ Don't use different `name` attributes for radio buttons that should be grouped
❌ Don't rely on placeholder text for labels
❌ Don't forget to include the empty first option in dropdowns
❌ Don't use radio buttons when checkboxes are more appropriate (and vice versa)
❌ Don't nest labels inside inputs or vice versa

### Common Use Cases

**Select Dropdowns:**

-   Country/state selection
-   Category selection with many options
-   Date selection (month, year)
-   Sorting options
-   Language selection

**Radio Buttons:**

-   Gender selection
-   Payment method
-   Shipping speed (standard, express, overnight)
-   Yes/No questions
-   Multiple choice questions (only one answer)

**Checkboxes:**

-   Terms and conditions agreement
-   Newsletter subscription
-   Feature selection (multiple features)
-   Privacy settings
-   Filter options (can select multiple)

### Quick Practice

**Try creating:**

1. A survey form with:

    - Dropdown for age range (18-24, 25-34, 35-44, 45+)
    - Radio buttons for satisfaction level (Very Satisfied, Satisfied, Neutral, Dissatisfied)
    - Checkboxes for product features used (at least 4 options)

2. A pizza order form with:
    - Dropdown for pizza size (Small, Medium, Large, Extra Large)
    - Radio buttons for crust type (Thin, Regular, Thick, Stuffed)
    - Checkboxes for toppings (at least 6 options)

---

## 2) Multimedia Elements (30 minutes)

### The `<video>` Element

The `<video>` element embeds video content in your page.

**Basic syntax:**

```html
<video
	controls
	width="640"
	height="360"
>
	<source
		src="video.mp4"
		type="video/mp4"
	/>
	<source
		src="video.webm"
		type="video/webm"
	/>
	<p>
		Your browser doesn't support HTML5 video. Here is a
		<a href="video.mp4">link to the video</a> instead.
	</p>
</video>
```

**Key attributes:**

| Attribute  | Purpose                                      |
| ---------- | -------------------------------------------- |
| `controls` | Shows play/pause, volume, progress bar       |
| `autoplay` | Starts playing automatically (use sparingly) |
| `loop`     | Repeats the video when finished              |
| `muted`    | Starts muted (required for autoplay)         |
| `poster`   | Image to show before video plays             |
| `preload`  | How much to load: `none`, `metadata`, `auto` |

**Accessible video example:**

```html
<figure>
	<video
		controls
		width="640"
		height="360"
		poster="thumbnail.jpg"
	>
		<source
			src="tutorial.mp4"
			type="video/mp4"
		/>
		<source
			src="tutorial.webm"
			type="video/webm"
		/>
		<track
			kind="captions"
			src="captions-en.vtt"
			srclang="en"
			label="English"
			default
		/>
		<p>Your browser doesn't support HTML5 video.</p>
	</video>
	<figcaption>Tutorial: Building Your First HTML Page</figcaption>
</figure>
```

**Best practices:**

-   ✅ Always include `controls` for accessibility
-   ✅ Provide multiple formats for browser compatibility
-   ✅ Include captions using `<track>` for accessibility
-   ✅ Add a fallback message for older browsers
-   ⚠️ Avoid `autoplay` unless muted (annoying user experience)
-   ⚠️ Use `poster` to show a meaningful thumbnail

### The `<audio>` Element

The `<audio>` element embeds sound content.

**Basic syntax:**

```html
<audio controls>
	<source
		src="podcast.mp3"
		type="audio/mpeg"
	/>
	<source
		src="podcast.ogg"
		type="audio/ogg"
	/>
	<p>Your browser doesn't support the audio element.</p>
</audio>
```

**Complete example with description:**

```html
<figure>
	<figcaption>Episode 5: Introduction to HTML Forms</figcaption>
	<audio
		controls
		preload="metadata"
	>
		<source
			src="episode-05.mp3"
			type="audio/mpeg"
		/>
		<source
			src="episode-05.ogg"
			type="audio/ogg"
		/>
		<p>
			Your browser doesn't support audio playback.
			<a href="episode-05.mp3">Download the episode</a> instead.
		</p>
	</audio>
	<p>Duration: 23 minutes | Published: November 15, 2025</p>
</figure>
```

### The `<picture>` Element

The `<picture>` element provides responsive images with different sources for different screen sizes or formats.

**Basic syntax:**

```html
<picture>
	<source
		media="(min-width: 800px)"
		srcset="large.jpg"
	/>
	<source
		media="(min-width: 400px)"
		srcset="medium.jpg"
	/>
	<img
		src="small.jpg"
		alt="Description"
	/>
</picture>
```

**Modern format support with fallback:**

```html
<picture>
	<!-- WebP for modern browsers -->
	<source
		srcset="image.webp"
		type="image/webp"
	/>
	<!-- AVIF for even better compression -->
	<source
		srcset="image.avif"
		type="image/avif"
	/>
	<!-- Fallback to JPEG -->
	<img
		src="image.jpg"
		alt="Scenic mountain landscape"
	/>
</picture>
```

**Art direction example (different crops for different sizes):**

```html
<picture>
	<!-- Wide crop for desktop -->
	<source
		media="(min-width: 1024px)"
		srcset="hero-wide.jpg"
	/>
	<!-- Square crop for tablet -->
	<source
		media="(min-width: 768px)"
		srcset="hero-square.jpg"
	/>
	<!-- Vertical crop for mobile -->
	<img
		src="hero-vertical.jpg"
		alt="Team collaboration at the office"
	/>
</picture>
```

**When to use `<picture>` vs `<img srcset>`:**

-   Use `<picture>` when:
    -   Different image crops for different screen sizes (art direction)
    -   Serving modern formats with fallbacks (WebP, AVIF)
-   Use `<img srcset>` when:
    -   Same image at different resolutions (1x, 2x, 3x)
    -   Simple responsive sizing

---

## 3) Embedded Content (iframe, embed, object) (20 minutes)

### The `<iframe>` Element

`<iframe>` embeds another HTML page within your page.

**Basic syntax:**

```html
<iframe
	src="https://example.com"
	width="800"
	height="600"
	title="Embedded content description"
>
</iframe>
```

**Common use cases:**

**Embedding a YouTube video:**

```html
<iframe
	width="560"
	height="315"
	src="https://www.youtube.com/embed/dQw4w9WgXcQ"
	title="YouTube video player"
	frameborder="0"
	allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
	allowfullscreen
></iframe>
```

**Embedding a Google Map:**

```html
<iframe
	src="https://www.google.com/maps/embed?pb=!1m18!..."
	width="600"
	height="450"
	style="border:0;"
	allowfullscreen=""
	loading="lazy"
	referrerpolicy="no-referrer-when-downgrade"
	title="Map showing our office location"
></iframe>
```

**Security considerations:**

```html
<!-- Add sandbox attribute for untrusted content -->
<iframe
	src="https://untrusted-site.com"
	sandbox="allow-scripts allow-same-origin"
	title="Embedded third-party content"
></iframe>
```

**Accessibility requirements:**

-   ✅ Always include a `title` attribute describing the iframe content
-   ✅ Ensure embedded content is keyboard accessible
-   ✅ Consider providing an alternative for users who can't access iframes

**Best practices:**

-   Use `loading="lazy"` for iframes below the fold
-   Set explicit `width` and `height` to prevent layout shift
-   Use `sandbox` attribute for untrusted content
-   Always provide a meaningful `title`

---

## 4) Advanced Form Controls (25 minutes)

### The `<datalist>` Element

`<datalist>` provides autocomplete suggestions for an input field.

**Basic example:**

```html
<label for="browser">Choose your browser:</label>
<input
	list="browsers"
	id="browser"
	name="browser"
/>

<datalist id="browsers">
	<option value="Chrome"></option>
	<option value="Firefox"></option>
	<option value="Safari"></option>
	<option value="Edge"></option>
	<option value="Opera"></option>
</datalist>
```

**With descriptions:**

```html
<label for="country">Country:</label>
<input
	list="countries"
	id="country"
	name="country"
/>

<datalist id="countries">
	<option value="United States">USA</option>
	<option value="United Kingdom">UK</option>
	<option value="Canada">CA</option>
	<option value="Australia">AU</option>
</datalist>
```

**Use cases:**

-   Product search with suggestions
-   Location/city selection
-   Category selection with many options
-   Browser autocomplete enhancements

### The `<output>` Element

Represents the result of a calculation or user action.

```html
<form oninput="result.value = parseInt(a.value) + parseInt(b.value)">
	<label for="a">Number 1:</label>
	<input
		type="number"
		id="a"
		name="a"
		value="0"
	/>
	+
	<label for="b">Number 2:</label>
	<input
		type="number"
		id="b"
		name="b"
		value="0"
	/>
	=
	<output
		name="result"
		for="a b"
		>0</output
	>
</form>
```

**Range slider with output:**

```html
<form>
	<label for="volume">Volume:</label>
	<input
		type="range"
		id="volume"
		name="volume"
		min="0"
		max="100"
		value="50"
		oninput="volumeOutput.value = volume.value"
	/>
	<output
		id="volumeOutput"
		name="volumeOutput"
		for="volume"
		>50</output
	>%
</form>
```

### The `<meter>` Element

Represents a scalar measurement within a known range.

```html
<label for="disk-usage">Disk usage:</label>
<meter
	id="disk-usage"
	min="0"
	max="100"
	low="33"
	high="66"
	optimum="20"
	value="75"
>
	75% used
</meter>
```

**Example: Test score meter:**

```html
<p>Test Score:</p>
<meter
	min="0"
	max="100"
	low="40"
	high="80"
	optimum="90"
	value="85"
>
	85 out of 100
</meter>
```

**Attributes:**

-   `value` — Current value
-   `min` / `max` — Range boundaries
-   `low` / `high` — Low and high thresholds
-   `optimum` — Optimal value (affects color in some browsers)

### The `<progress>` Element

Represents task completion progress.

```html
<label for="file-upload">Uploading file:</label>
<progress
	id="file-upload"
	value="32"
	max="100"
>
	32%
</progress>
```

**Indeterminate progress (unknown duration):**

```html
<p>Processing...</p>
<progress></progress>
<!-- No value attribute = indeterminate -->
```

---

## 5) Meta Tags and SEO Basics (25 minutes)

### Essential Meta Tags

Meta tags provide information about your HTML document.

**Basic meta tags:**

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta
			name="viewport"
			content="width=device-width, initial-scale=1.0"
		/>
		<meta
			name="description"
			content="Learn HTML fundamentals with hands-on tutorials and examples. Perfect for beginners."
		/>
		<meta
			name="keywords"
			content="HTML, web development, tutorial, beginner"
		/>
		<meta
			name="author"
			content="Your Name"
		/>
		<title>HTML Fundamentals Course</title>
	</head>
	<body>
		<!-- Content -->
	</body>
</html>
```

### Open Graph Tags (for social media)

Make your pages look good when shared on Facebook, LinkedIn, etc.

```html
<head>
	<!-- Open Graph / Facebook -->
	<meta
		property="og:type"
		content="website"
	/>
	<meta
		property="og:url"
		content="https://example.com/page"
	/>
	<meta
		property="og:title"
		content="Your Page Title"
	/>
	<meta
		property="og:description"
		content="Description for social media"
	/>
	<meta
		property="og:image"
		content="https://example.com/image.jpg"
	/>

	<!-- Twitter -->
	<meta
		name="twitter:card"
		content="summary_large_image"
	/>
	<meta
		name="twitter:url"
		content="https://example.com/page"
	/>
	<meta
		name="twitter:title"
		content="Your Page Title"
	/>
	<meta
		name="twitter:description"
		content="Description for Twitter"
	/>
	<meta
		name="twitter:image"
		content="https://example.com/image.jpg"
	/>
</head>
```

### Favicon

Add an icon for browser tabs and bookmarks:

```html
<head>
	<!-- Modern approach -->
	<link
		rel="icon"
		type="image/png"
		sizes="32x32"
		href="/favicon-32x32.png"
	/>
	<link
		rel="icon"
		type="image/png"
		sizes="16x16"
		href="/favicon-16x16.png"
	/>
	<link
		rel="apple-touch-icon"
		sizes="180x180"
		href="/apple-touch-icon.png"
	/>

	<!-- For older browsers -->
	<link
		rel="icon"
		href="/favicon.ico"
	/>
</head>
```

---

## 6) HTML Character Entities (15 minutes)

### HTML Character Entities

Some characters have special meaning in HTML and must be escaped.

**Essential entities:**

| Character | Entity     | Name         | Use Case                  |
| --------- | ---------- | ------------ | ------------------------- |
| `<`       | `&lt;`     | Less than    | Display code examples     |
| `>`       | `&gt;`     | Greater than | Display code examples     |
| `&`       | `&amp;`    | Ampersand    | URLs, text with &         |
| `"`       | `&quot;`   | Quote        | Inside attribute values   |
| `'`       | `&apos;`   | Apostrophe   | Inside attribute values   |
| ` `       | `&nbsp;`   | Non-breaking | Prevent line breaks       |
| `©`       | `&copy;`   | Copyright    | Copyright symbol          |
| `®`       | `&reg;`    | Registered   | Trademark symbol          |
| `™`       | `&trade;`  | Trademark    | Trademark symbol          |
| `€`       | `&euro;`   | Euro         | Currency                  |
| `£`       | `&pound;`  | Pound        | Currency                  |
| `¥`       | `&yen;`    | Yen          | Currency                  |
| `—`       | `&mdash;`  | Em dash      | Typography                |
| `–`       | `&ndash;`  | En dash      | Typography (ranges: 1–10) |
| `×`       | `&times;`  | Multiply     | Math: 5 × 3               |
| `÷`       | `&divide;` | Divide       | Math: 10 ÷ 2              |
| `°`       | `&deg;`    | Degree       | Temperature: 25°C         |
| `←`       | `&larr;`   | Left arrow   | Directions                |
| `→`       | `&rarr;`   | Right arrow  | Directions                |
| `↑`       | `&uarr;`   | Up arrow     | Directions                |
| `↓`       | `&darr;`   | Down arrow   | Directions                |

**Examples:**

```html
<!-- Displaying HTML code -->
<p>Use <code>&lt;p&gt;</code> for paragraphs.</p>

<!-- Copyright notice -->
<footer>
	<p>&copy; 2025 My Company. All rights reserved.</p>
</footer>

<!-- Non-breaking space (keeps words together) -->
<p>The price is&nbsp;$99.99</p>

<!-- Mathematical expression -->
<p>The area is 5&nbsp;&times;&nbsp;3&nbsp;=&nbsp;15&nbsp;cm&sup2;</p>

<!-- Temperature -->
<p>Today's high: 25&deg;C (77&deg;F)</p>

<!-- Em dash for parenthetical statements -->
<p>HTML—the foundation of the web—is easy to learn.</p>
```

---

## 7) Definition Lists (10 minutes)

### The `<dl>`, `<dt>`, and `<dd>` Elements

Definition lists are for term/description pairs.

**Basic structure:**

```html
<dl>
	<dt>HTML</dt>
	<dd>HyperText Markup Language</dd>

	<dt>CSS</dt>
	<dd>Cascading Style Sheets</dd>

	<dt>JavaScript</dt>
	<dd>Programming language for web interactivity</dd>
</dl>
```

**Multiple descriptions per term:**

```html
<dl>
	<dt>Firefox</dt>
	<dd>A free, open-source web browser</dd>
	<dd>Developed by Mozilla Foundation</dd>
	<dd>Available on Windows, macOS, Linux, Android, iOS</dd>
</dl>
```

**Multiple terms with same description:**

```html
<dl>
	<dt>HTML</dt>
	<dt>HyperText Markup Language</dt>
	<dd>The standard language for creating web pages</dd>
</dl>
```

**Real-world use case: FAQ:**

```html
<h2>Frequently Asked Questions</h2>

<dl>
	<dt>What is HTML?</dt>
	<dd>
		HTML stands for HyperText Markup Language. It's the standard language
		used to create web pages.
	</dd>

	<dt>Do I need to know programming to learn HTML?</dt>
	<dd>
		No! HTML is a markup language, not a programming language. It's designed
		to be easy to learn, even for complete beginners.
	</dd>

	<dt>What's the difference between HTML and HTML5?</dt>
	<dd>
		HTML5 is the latest version of HTML. It includes new semantic elements,
		multimedia support, and improved accessibility features.
	</dd>
</dl>
```

**Styling definition lists:**

```css
dl {
	margin: 20px 0;
}

dt {
	font-weight: bold;
	margin-top: 15px;
	color: #333;
}

dd {
	margin-left: 20px;
	margin-bottom: 10px;
	color: #666;
}
```

---

## 8) Details and Summary Elements (15 minutes)

### The `<details>` and `<summary>` Elements

Create collapsible content without JavaScript!

**Basic syntax:**

```html
<details>
	<summary>Click to expand</summary>
	<p>This content is hidden until you click the summary.</p>
</details>
```

**Real-world example: FAQ accordion:**

```html
<h2>Frequently Asked Questions</h2>

<details>
	<summary>How do I create my first HTML page?</summary>
	<p>
		Start by creating a new file with a <code>.html</code> extension. Add
		the basic HTML structure with <code>&lt;!DOCTYPE html&gt;</code>,
		<code>&lt;html&gt;</code>, <code>&lt;head&gt;</code>, and
		<code>&lt;body&gt;</code> tags.
	</p>
</details>

<details>
	<summary>What text editor should I use?</summary>
	<p>
		We recommend VS Code, but you can use any text editor like Sublime Text,
		Atom, or even Notepad. The important thing is that you save files with
		the
		<code>.html</code> extension.
	</p>
</details>

<details open>
	<summary>Is HTML hard to learn?</summary>
	<p>
		No! HTML is one of the easiest languages to learn. It has a simple
		syntax and you can see results immediately in your browser.
	</p>
</details>
<!-- 'open' attribute makes it expanded by default -->
```

**Nested details:**

```html
<details>
	<summary>Web Technologies</summary>

	<details>
		<summary>Frontend</summary>
		<ul>
			<li>HTML</li>
			<li>CSS</li>
			<li>JavaScript</li>
		</ul>
	</details>

	<details>
		<summary>Backend</summary>
		<ul>
			<li>Node.js</li>
			<li>Python</li>
			<li>PHP</li>
		</ul>
	</details>
</details>
```

**Styled details/summary:**

```css
details {
	border: 1px solid #ddd;
	border-radius: 4px;
	padding: 10px;
	margin-bottom: 10px;
	background: #f9f9f9;
}

summary {
	font-weight: bold;
	cursor: pointer;
	padding: 5px;
	user-select: none; /* Prevent text selection when clicking */
}

summary:hover {
	background: #e9e9e9;
}

details[open] summary {
	margin-bottom: 10px;
	border-bottom: 1px solid #ddd;
}

/* Hide default marker and add custom icon */
summary {
	list-style: none;
}

summary::before {
	content: '▶ ';
	transition: transform 0.2s;
	display: inline-block;
}

details[open] summary::before {
	transform: rotate(90deg);
}
```

**Accessibility note:**

The `<details>` element is keyboard accessible by default:

-   Press `Tab` to focus the summary
-   Press `Enter` or `Space` to expand/collapse

---

## 9) Semantic Text Elements (20 minutes)

### The `<abbr>` Element

Marks abbreviations and acronyms:

```html
<p><abbr title="World Wide Web Consortium">W3C</abbr> sets web standards.</p>

<p>
	The <abbr title="HyperText Markup Language">HTML</abbr> specification is
	maintained by
	<abbr title="Web Hypertext Application Technology Working Group"
		>WHATWG</abbr
	>.
</p>
```

### The `<mark>` Element

Highlights text (like a highlighter pen):

```html
<p>
	Search results for "HTML": The <mark>HTML</mark> element represents the root
	of an <mark>HTML</mark> document.
</p>
```

### The `<time>` Element

Represents dates and times in a machine-readable format:

```html
<p>
	The course starts on
	<time datetime="2025-11-17">November 17, 2025</time>.
</p>

<p>
	Published <time datetime="2025-11-17T14:30:00">2:30 PM</time> on
	<time datetime="2025-11-17">November 17</time>.
</p>

<!-- Relative time -->
<p>Posted <time datetime="2025-11-16">yesterday</time>.</p>
```

### The `<kbd>` Element

Represents keyboard input:

```html
<p>Press <kbd>Ctrl</kbd> + <kbd>S</kbd> to save your file.</p>

<p>
	To refresh the page, press <kbd>F5</kbd> or <kbd>Ctrl</kbd> + <kbd>R</kbd>.
</p>
```

### The `<samp>` Element

Represents sample output from a program:

```html
<p>If the file is not found, you'll see:</p>
<samp>Error: File not found (404)</samp>
```

### The `<var>` Element

Represents a variable in math or programming:

```html
<p>The area of a rectangle is <var>width</var> × <var>height</var>.</p>

<p>
	To calculate speed: <var>speed</var> = <var>distance</var> / <var>time</var>
</p>
```

### The `<code>` Element

Represents inline code:

```html
<p>Use the <code>&lt;a&gt;</code> element to create links.</p>

<p>
	The <code>console.log()</code> function outputs messages to the browser
	console.
</p>
```

### The `<pre>` Element

Preserves formatting (whitespace, line breaks):

```html
<pre>
function greet(name) {
    console.log("Hello, " + name);
}

greet("World");
</pre>
```

**Combining `<pre>` and `<code>` for code blocks:**

```html
<pre><code>
&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
    &lt;meta charset="UTF-8"&gt;
    &lt;title&gt;My Page&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;h1&gt;Hello, World!&lt;/h1&gt;
&lt;/body&gt;
&lt;/html&gt;
</code></pre>
```

---

## 9) Practice Exercises

### Exercise 1: Multimedia Gallery

Create a page with:

-   At least one video with controls and captions
-   At least one audio element
-   A responsive image using `<picture>`

### Exercise 2: Interactive FAQ

Build an FAQ page using:

-   `<details>` and `<summary>` for collapsible answers
-   `<dl>`, `<dt>`, and `<dd>` for structured Q&A
-   Proper semantic markup

### Exercise 3: Enhanced Form

Create a form that includes:

-   A `<datalist>` for autocomplete suggestions
-   A `<meter>` showing password strength
-   A `<progress>` bar (can be static for now)
-   Proper labels and accessibility

---

## 10) Resources

### Documentation

-   [MDN: HTML Elements Reference](https://developer.mozilla.org/docs/Web/HTML/Element)
-   [MDN: Video and Audio Content](https://developer.mozilla.org/docs/Learn/HTML/Multimedia_and_embedding/Video_and_audio_content)
-   [MDN: Responsive Images](https://developer.mozilla.org/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images)
-   [HTML5 Doctor](http://html5doctor.com/)

### Tools

-   [Can I Use](https://caniuse.com/) — Browser compatibility checker
-   [HTML5 Validator](https://validator.w3.org/)
-   [WebVTT Validator](https://w3c.github.io/webvtt.js/parser.html) — For video captions

### Additional Reading

-   [HTML: The Living Standard](https://html.spec.whatwg.org/)
-   [Web Fundamentals: Media](https://developers.google.com/web/fundamentals/media)

---

## Summary

These extras expand your HTML toolkit beyond the core curriculum:

✅ **Multimedia** — Embed video, audio, and responsive images
✅ **Embedded Content** — Use iframes responsibly
✅ **Advanced Forms** — Datalists, meters, progress bars
✅ **Meta Tags** — SEO and social media optimization
✅ **Entities** — Display special characters correctly
✅ **Definition Lists** — Semantic term/description pairs
✅ **Details/Summary** — No-JavaScript collapsible content
✅ **Semantic Elements** — `<abbr>`, `<time>`, `<kbd>`, `<code>`, etc.

While not required for the main course, these elements are commonly used in production websites and will make your HTML more powerful and semantic.

---

**Navigation:**
← [Week 02 Index](README.md) | [Learning Plan](../learning-plan.md)
