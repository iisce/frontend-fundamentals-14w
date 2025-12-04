# Week 05 — Session 15: Mini Project 1 — Responsive Webpage

**Navigation:**
← [Week 05 Session 14](session-14.md) | [Week 05 Index](../week-05.md) | [Week 06](../week-06.md) →

---

**Project Duration:** Full session (90 minutes) + homework time
**Completion Time:** 1 week (due end of Week 05)

## 📋 Pre-Project Checklist

Before starting this mini project, make sure you have:

-   ✅ Completed Sessions 01-14 (Weeks 01-05)
-   ✅ Understanding of HTML structure and semantic elements
-   ✅ Proficiency with CSS Box Model, positioning, and spacing
-   ✅ Mastery of Flexbox container and item properties
-   ✅ Experience with responsive design principles
-   ✅ Code editor (VS Code) ready with Live Server
-   ✅ Browser Developer Tools familiarity
-   ✅ Create project folder: `mini-project-1-responsive-webpage`

## 🎯 Project Objectives

By the end of this mini project, you will have:

-   Built a complete, multi-section responsive landing page
-   Applied HTML5 semantic structure throughout
-   Implemented responsive navigation with mobile menu
-   Created flexible layouts using Flexbox
-   Designed mobile-first with progressive enhancement
-   Tested across multiple screen sizes
-   Written clean, well-commented code
-   Deployed a live, functional webpage

## 🏆 What You Will Build

**Project:** A responsive landing page for a fictional product/service of your choice.

**Examples:**

-   Tech startup landing page
-   Coffee shop website
-   Fitness studio homepage
-   Portfolio showcase
-   Online course platform
-   Restaurant website

**Required Sections:**

1. **Header with Navigation**

    - Logo
    - Responsive navigation menu
    - Mobile hamburger menu (optional but encouraged)

2. **Hero Section**

    - Eye-catching headline
    - Subheadline/description
    - Call-to-action button
    - Background image or gradient

3. **Features Section**

    - 3-4 feature cards in a flexible grid
    - Icons or images
    - Equal-height cards

4. **About/Services Section**

    - Text content with image
    - Two-column layout (desktop)
    - Single column (mobile)

5. **Testimonials/Pricing Section** (choose one)

    - Customer testimonials with avatars, OR
    - Pricing cards with featured option

6. **Footer**
    - Contact information
    - Social media links
    - Copyright notice

## 📐 Project Structure

### File Organization

```
mini-project-1-responsive-webpage/
│
├── index.html           ← Main HTML file
├── styles.css           ← External CSS file
├── README.md            ← Project documentation
│
└── images/              ← Image assets
    ├── logo.png
    ├── hero-bg.jpg
    ├── feature-1.jpg
    └── ...
```

### Recommended Workflow

**Phase 1: Planning (10 minutes)**

1. Choose your website theme
2. Sketch layout on paper
3. Identify semantic HTML structure
4. Plan color scheme and typography

**Phase 2: HTML Structure (15 minutes)**

1. Create semantic HTML skeleton
2. Add all content sections
3. Include placeholder text/images
4. Validate HTML

**Phase 3: CSS Foundation (15 minutes)**

1. CSS reset and base styles
2. Typography and color variables
3. Layout container styles
4. Mobile-first base styles

**Phase 4: Desktop Layout (25 minutes)**

1. Header and navigation
2. Hero section
3. Features grid with Flexbox
4. Content sections
5. Footer

**Phase 5: Responsive Design (15 minutes)**

1. Test at different screen sizes
2. Add media queries for tablets
3. Refine mobile experience
4. Test navigation on mobile

**Phase 6: Polish & Testing (10 minutes)**

1. Add hover effects
2. Check accessibility
3. Validate HTML/CSS
4. Cross-browser testing

---

## 🛠️ Step-by-Step Guide

### Step 1: Set Up Project Files

Create your project structure:

```bash
mkdir mini-project-1-responsive-webpage
cd mini-project-1-responsive-webpage
mkdir images
touch index.html styles.css README.md
```

### Step 2: HTML Foundation

Start with semantic HTML structure:

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
			content="Your website description here"
		/>
		<title>Your Project Title | Tagline</title>
		<link
			rel="stylesheet"
			href="styles.css"
		/>
	</head>
	<body>
		<!-- Header with Navigation -->
		<header class="header">
			<div class="container">
				<nav class="nav">
					<div class="logo">Your Logo</div>
					<ul class="nav-menu">
						<li><a href="#home">Home</a></li>
						<li><a href="#features">Features</a></li>
						<li><a href="#about">About</a></li>
						<li><a href="#contact">Contact</a></li>
					</ul>
				</nav>
			</div>
		</header>

		<!-- Hero Section -->
		<section
			class="hero"
			id="home"
		>
			<div class="container">
				<div class="hero-content">
					<h1>Your Compelling Headline</h1>
					<p class="hero-subtitle">
						A clear, concise description of what you offer
					</p>
					<a
						href="#features"
						class="btn btn-primary"
						>Get Started</a
					>
				</div>
			</div>
		</section>

		<!-- Features Section -->
		<section
			class="features"
			id="features"
		>
			<div class="container">
				<h2 class="section-title">Amazing Features</h2>
				<div class="features-grid">
					<div class="feature-card">
						<div class="feature-icon">🚀</div>
						<h3>Fast Performance</h3>
						<p>
							Lightning-fast load times and smooth user
							experience.
						</p>
					</div>
					<div class="feature-card">
						<div class="feature-icon">🎨</div>
						<h3>Beautiful Design</h3>
						<p>Modern, clean interface that users love.</p>
					</div>
					<div class="feature-card">
						<div class="feature-icon">🔒</div>
						<h3>Secure & Reliable</h3>
						<p>Your data is safe with enterprise-grade security.</p>
					</div>
					<div class="feature-card">
						<div class="feature-icon">💡</div>
						<h3>Smart Features</h3>
						<p>Intelligent tools that make your work easier.</p>
					</div>
				</div>
			</div>
		</section>

		<!-- About Section -->
		<section
			class="about"
			id="about"
		>
			<div class="container">
				<div class="about-content">
					<div class="about-text">
						<h2>About Our Product</h2>
						<p>
							Tell your story here. Explain what makes your
							product or service unique and why customers should
							choose you.
						</p>
						<p>
							Add more compelling information that builds trust
							and showcases your expertise.
						</p>
						<a
							href="#contact"
							class="btn btn-secondary"
							>Learn More</a
						>
					</div>
					<div class="about-image">
						<img
							src="images/about.jpg"
							alt="About us"
						/>
					</div>
				</div>
			</div>
		</section>

		<!-- Footer -->
		<footer class="footer">
			<div class="container">
				<div class="footer-content">
					<div class="footer-section">
						<h3>Your Company</h3>
						<p>Building amazing products since 2025.</p>
					</div>
					<div class="footer-section">
						<h3>Quick Links</h3>
						<ul>
							<li><a href="#home">Home</a></li>
							<li><a href="#features">Features</a></li>
							<li><a href="#about">About</a></li>
						</ul>
					</div>
					<div class="footer-section">
						<h3>Connect</h3>
						<div class="social-links">
							<a href="#">Twitter</a>
							<a href="#">LinkedIn</a>
							<a href="#">GitHub</a>
						</div>
					</div>
				</div>
				<div class="footer-bottom">
					<p>&copy; 2025 Your Company. All rights reserved.</p>
				</div>
			</div>
		</footer>
	</body>
</html>
```

### Step 3: CSS Foundation (Mobile-First)

Set up your CSS with variables and base styles:

```css
/* ===================================
   CSS Reset & Base Styles
   =================================== */

* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}

html {
	scroll-behavior: smooth;
}

body {
	font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
		Ubuntu, Cantarell, sans-serif;
	line-height: 1.6;
	color: #333;
}

/* ===================================
   CSS Variables
   =================================== */

:root {
	/* Colors */
	--primary-color: #3498db;
	--secondary-color: #2ecc71;
	--dark-color: #2c3e50;
	--light-color: #ecf0f1;
	--white: #ffffff;
	--gray: #7f8c8d;

	/* Spacing */
	--spacing-xs: 0.5rem;
	--spacing-sm: 1rem;
	--spacing-md: 2rem;
	--spacing-lg: 3rem;
	--spacing-xl: 4rem;

	/* Typography */
	--font-size-base: 1rem;
	--font-size-lg: 1.25rem;
	--font-size-xl: 1.5rem;
	--font-size-2xl: 2rem;
	--font-size-3xl: 2.5rem;

	/* Layout */
	--max-width: 1200px;
	--border-radius: 8px;
	--box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

/* ===================================
   Utility Classes
   =================================== */

.container {
	max-width: var(--max-width);
	margin: 0 auto;
	padding: 0 var(--spacing-sm);
}

.section-title {
	text-align: center;
	font-size: var(--font-size-2xl);
	margin-bottom: var(--spacing-lg);
	color: var(--dark-color);
}

/* ===================================
   Buttons
   =================================== */

.btn {
	display: inline-block;
	padding: 12px 30px;
	text-decoration: none;
	border-radius: var(--border-radius);
	font-weight: 600;
	transition: all 0.3s ease;
	cursor: pointer;
	border: none;
	font-size: var(--font-size-base);
}

.btn-primary {
	background: var(--primary-color);
	color: var(--white);
}

.btn-primary:hover {
	background: #2980b9;
	transform: translateY(-2px);
	box-shadow: 0 4px 15px rgba(52, 152, 219, 0.3);
}

.btn-secondary {
	background: transparent;
	color: var(--primary-color);
	border: 2px solid var(--primary-color);
}

.btn-secondary:hover {
	background: var(--primary-color);
	color: var(--white);
}

/* ===================================
   Header & Navigation
   =================================== */

.header {
	background: var(--white);
	box-shadow: var(--box-shadow);
	position: sticky;
	top: 0;
	z-index: 1000;
}

.nav {
	display: flex;
	justify-content: space-between;
	align-items: center;
	padding: var(--spacing-sm) 0;
}

.logo {
	font-size: var(--font-size-xl);
	font-weight: bold;
	color: var(--primary-color);
}

.nav-menu {
	display: flex;
	list-style: none;
	gap: var(--spacing-md);
}

.nav-menu a {
	text-decoration: none;
	color: var(--dark-color);
	font-weight: 500;
	transition: color 0.3s ease;
}

.nav-menu a:hover {
	color: var(--primary-color);
}

/* Mobile Navigation (stacked by default) */
@media (max-width: 768px) {
	.nav-menu {
		flex-direction: column;
		gap: var(--spacing-sm);
		display: none; /* You can add JavaScript to toggle this */
	}

	/* Add hamburger menu styles here if implementing */
}

/* ===================================
   Hero Section
   =================================== */

.hero {
	background: linear-gradient(
		135deg,
		var(--primary-color),
		var(--secondary-color)
	);
	color: var(--white);
	padding: var(--spacing-xl) 0;
	text-align: center;
}

.hero-content {
	max-width: 800px;
	margin: 0 auto;
}

.hero h1 {
	font-size: var(--font-size-3xl);
	margin-bottom: var(--spacing-md);
	line-height: 1.2;
}

.hero-subtitle {
	font-size: var(--font-size-lg);
	margin-bottom: var(--spacing-lg);
	opacity: 0.95;
}

/* ===================================
   Features Section
   =================================== */

.features {
	padding: var(--spacing-xl) 0;
	background: var(--light-color);
}

.features-grid {
	display: flex;
	flex-wrap: wrap;
	gap: var(--spacing-md);
}

.feature-card {
	flex: 1 1 250px; /* Flexible cards, minimum 250px */
	background: var(--white);
	padding: var(--spacing-lg);
	border-radius: var(--border-radius);
	box-shadow: var(--box-shadow);
	text-align: center;
	transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.feature-card:hover {
	transform: translateY(-5px);
	box-shadow: 0 5px 20px rgba(0, 0, 0, 0.15);
}

.feature-icon {
	font-size: 3rem;
	margin-bottom: var(--spacing-sm);
}

.feature-card h3 {
	color: var(--dark-color);
	margin-bottom: var(--spacing-sm);
}

.feature-card p {
	color: var(--gray);
	line-height: 1.7;
}

/* ===================================
   About Section
   =================================== */

.about {
	padding: var(--spacing-xl) 0;
}

.about-content {
	display: flex;
	flex-direction: column;
	gap: var(--spacing-lg);
	align-items: center;
}

.about-text {
	flex: 1;
}

.about-text h2 {
	color: var(--dark-color);
	margin-bottom: var(--spacing-md);
	font-size: var(--font-size-2xl);
}

.about-text p {
	margin-bottom: var(--spacing-md);
	color: var(--gray);
	line-height: 1.8;
}

.about-image {
	flex: 1;
	width: 100%;
}

.about-image img {
	width: 100%;
	height: auto;
	border-radius: var(--border-radius);
	box-shadow: var(--box-shadow);
}

/* Desktop: side-by-side layout */
@media (min-width: 768px) {
	.about-content {
		flex-direction: row;
	}
}

/* ===================================
   Footer
   =================================== */

.footer {
	background: var(--dark-color);
	color: var(--white);
	padding: var(--spacing-lg) 0 var(--spacing-md);
}

.footer-content {
	display: flex;
	flex-wrap: wrap;
	gap: var(--spacing-lg);
	margin-bottom: var(--spacing-md);
}

.footer-section {
	flex: 1 1 200px;
}

.footer-section h3 {
	margin-bottom: var(--spacing-sm);
	color: var(--white);
}

.footer-section p,
.footer-section a {
	color: var(--light-color);
}

.footer-section ul {
	list-style: none;
}

.footer-section ul li {
	margin-bottom: var(--spacing-xs);
}

.footer-section a {
	text-decoration: none;
	transition: color 0.3s ease;
}

.footer-section a:hover {
	color: var(--primary-color);
}

.social-links {
	display: flex;
	gap: var(--spacing-sm);
}

.footer-bottom {
	text-align: center;
	padding-top: var(--spacing-md);
	border-top: 1px solid rgba(255, 255, 255, 0.1);
	color: var(--light-color);
}
```

### Step 4: Responsive Enhancements

Add media queries for better tablet/desktop experience:

```css
/* ===================================
   Responsive Media Queries
   =================================== */

/* Tablet and up (768px+) */
@media (min-width: 768px) {
	:root {
		--font-size-3xl: 3rem;
	}

	.container {
		padding: 0 var(--spacing-md);
	}

	.hero {
		padding: 6rem 0;
	}

	.hero h1 {
		font-size: var(--font-size-3xl);
	}
}

/* Desktop and up (1024px+) */
@media (min-width: 1024px) {
	:root {
		--font-size-3xl: 3.5rem;
	}

	.features-grid {
		gap: var(--spacing-lg);
	}

	.feature-card {
		flex: 1 1 calc(25% - var(--spacing-lg)); /* 4 columns */
	}
}
```

---

## 🎨 Design Guidelines

### Color Scheme

Choose a cohesive color palette:

**Option 1: Modern Blue**

-   Primary: `#3498db` (Blue)
-   Secondary: `#2ecc71` (Green)
-   Dark: `#2c3e50`
-   Light: `#ecf0f1`

**Option 2: Professional Purple**

-   Primary: `#9b59b6` (Purple)
-   Secondary: `#e74c3c` (Red)
-   Dark: `#34495e`
-   Light: `#ecf0f1`

**Option 3: Warm Orange**

-   Primary: `#e67e22` (Orange)
-   Secondary: `#f39c12` (Yellow)
-   Dark: `#2c3e50`
-   Light: `#ecf0f1`

### Typography

**Recommended font pairings:**

```css
/* Option 1: System Fonts (fastest) */
font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
	Ubuntu, Cantarell, sans-serif;

/* Option 2: Google Fonts */
/* Add to <head>: */
/* <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet"> */
font-family: 'Inter', sans-serif;

/* Option 3: Classic */
font-family: 'Georgia', serif; /* Headings */
font-family: 'Arial', sans-serif; /* Body */
```

### Spacing System

Use consistent spacing throughout:

```css
/* Use spacing variables */
--spacing-xs: 0.5rem; /* 8px */
--spacing-sm: 1rem; /* 16px */
--spacing-md: 2rem; /* 32px */
--spacing-lg: 3rem; /* 48px */
--spacing-xl: 4rem; /* 64px */
```

---

## ✅ Project Requirements Checklist

### HTML Structure (20 points)

-   [ ] Valid HTML5 document structure
-   [ ] Proper semantic elements (`<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`)
-   [ ] All images have `alt` attributes
-   [ ] Headings follow logical hierarchy (h1 → h2 → h3)
-   [ ] External CSS file linked correctly

### CSS Implementation (40 points)

-   [ ] External stylesheet used (no inline styles)
-   [ ] CSS variables for colors and spacing
-   [ ] Flexbox used for layouts
-   [ ] Mobile-first approach with media queries
-   [ ] Responsive navigation
-   [ ] Hover effects on interactive elements
-   [ ] No CSS errors (validate with W3C)

### Responsive Design (20 points)

-   [ ] Works on mobile (320px - 767px)
-   [ ] Works on tablet (768px - 1023px)
-   [ ] Works on desktop (1024px+)
-   [ ] Smooth breakpoint transitions
-   [ ] Images scale appropriately

### Code Quality (10 points)

-   [ ] Code is well-organized and indented
-   [ ] Meaningful class names (BEM or similar)
-   [ ] Comments explain complex sections
-   [ ] No unused CSS or HTML
-   [ ] Consistent naming conventions

### Design & Polish (10 points)

-   [ ] Cohesive color scheme
-   [ ] Readable typography
-   [ ] Good contrast ratios
-   [ ] Visual hierarchy is clear
-   [ ] Professional appearance

**Total: 100 points**

---

## 🎁 Bonus Challenges (+20 points)

Want to go above and beyond? Try these:

### Bonus 1: Animated Hero Section (+5 points)

Add CSS animations to hero content:

```css
@keyframes fadeInUp {
	from {
		opacity: 0;
		transform: translateY(30px);
	}
	to {
		opacity: 1;
		transform: translateY(0);
	}
}

.hero h1 {
	animation: fadeInUp 1s ease-out;
}

.hero-subtitle {
	animation: fadeInUp 1s ease-out 0.2s backwards;
}

.btn-primary {
	animation: fadeInUp 1s ease-out 0.4s backwards;
}
```

### Bonus 2: Hamburger Menu with JavaScript (+10 points)

Implement a working mobile menu:

```html
<!-- Add to nav -->
<button
	class="hamburger"
	aria-label="Menu"
>
	<span></span>
	<span></span>
	<span></span>
</button>
```

```css
.hamburger {
	display: none;
	flex-direction: column;
	gap: 4px;
	background: none;
	border: none;
	cursor: pointer;
}

.hamburger span {
	width: 25px;
	height: 3px;
	background: var(--dark-color);
	transition: 0.3s;
}

@media (max-width: 768px) {
	.hamburger {
		display: flex;
	}

	.nav-menu {
		display: none;
	}

	.nav-menu.active {
		display: flex;
	}
}
```

```javascript
// Add before </body>
<script>
    const hamburger = document.querySelector('.hamburger');
    const navMenu = document.querySelector('.nav-menu');

    hamburger.addEventListener('click', () => {
        navMenu.classList.toggle('active');
    });
</script>
```

### Bonus 3: Dark Mode Toggle (+5 points)

Add a theme switcher:

```css
[data-theme='dark'] {
	--dark-color: #ecf0f1;
	--white: #2c3e50;
	--light-color: #34495e;
}
```

```javascript
const themeToggle = document.querySelector('.theme-toggle');
themeToggle.addEventListener('click', () => {
	document.documentElement.dataset.theme =
		document.documentElement.dataset.theme === 'dark' ? 'light' : 'dark';
});
```

---

## 🐛 Common Issues & Solutions

### Issue 1: Images Not Displaying

**Problem:** Images show as broken links.

**Solutions:**

-   Check file path is correct: `images/filename.jpg`
-   Verify image file actually exists in `images/` folder
-   Check file extension matches (`.jpg` vs `.jpeg`)
-   Use placeholder services: `https://via.placeholder.com/600x400`

### Issue 2: Flexbox Not Working

**Problem:** Items not arranging as expected.

**Solutions:**

-   Verify parent has `display: flex`
-   Check if `flex-wrap: wrap` is needed
-   Review `flex-direction` (row vs column)
-   Use browser DevTools to inspect flex container

### Issue 3: Mobile Menu Not Hiding

**Problem:** Navigation shows all items on mobile.

**Solutions:**

-   Add media query: `@media (max-width: 768px)`
-   Use `flex-direction: column` for mobile
-   Consider `display: none` for mobile nav initially
-   Add JavaScript for toggle functionality

### Issue 4: Sticky Header Not Working

**Problem:** Header doesn't stay at top when scrolling.

**Solutions:**

-   Use `position: sticky` with `top: 0`
-   Add `z-index: 1000` to stay above content
-   Ensure no parent has `overflow: hidden`

### Issue 5: Content Overflow on Small Screens

**Problem:** Content extends beyond viewport width.

**Solutions:**

-   Add `max-width: 100%` to images
-   Use `overflow-wrap: break-word` for long text
-   Check for fixed widths that exceed screen size
-   Test with browser DevTools responsive mode

---

## 📝 Project Documentation (README.md)

Create a README for your project:

```markdown
# Mini Project 1: Responsive Webpage

A fully responsive landing page built with HTML5 and CSS3 Flexbox.

## Project Description

[Describe your website theme and purpose]

## Features

-   Responsive design (mobile, tablet, desktop)
-   Flexible Flexbox layouts
-   Modern CSS with custom properties
-   Smooth scrolling navigation
-   Hover effects and transitions

## Technologies Used

-   HTML5 (Semantic markup)
-   CSS3 (Flexbox, Custom Properties, Media Queries)
-   [Any additional tools/libraries]

## Design Decisions

[Explain your color scheme choice, typography, layout decisions]

## Challenges & Solutions

[Describe any problems you encountered and how you solved them]

## Future Improvements

-   [ ] Add hamburger menu functionality
-   [ ] Implement smooth scroll behavior
-   [ ] Add more animations
-   [ ] Improve accessibility

## Screenshots

[Add screenshots of mobile, tablet, and desktop views]

## Live Demo

[Link to live site if deployed]

## Author

Your Name - [Your GitHub Profile]
```

---

## 🚀 Submission Guidelines

### What to Submit

1. **Project folder** containing:

    - `index.html`
    - `styles.css`
    - `README.md`
    - `images/` folder (if using local images)

2. **Validation reports:**

    - HTML validation: [W3C HTML Validator](https://validator.w3.org/)
    - CSS validation: [W3C CSS Validator](https://jigsaw.w3.org/css-validator/)

3. **Screenshots** (3 required):
    - Mobile view (375px width)
    - Tablet view (768px width)
    - Desktop view (1440px width)

### Submission Format

**Option 1: GitHub Repository (Recommended)**

1. Create a new GitHub repository
2. Push your project files
3. Enable GitHub Pages for live demo
4. Submit repository URL

**Option 2: ZIP File**

1. Compress project folder
2. Name: `yourname-mini-project-1.zip`
3. Submit via course platform

### Deadline

**Due:** End of Week 05 (Sunday, 11:59 PM)

**Late submissions:** -10% per day

---

## 🎓 Evaluation Criteria

Your project will be evaluated on:

### Functionality (30%)

-   All required sections present
-   Responsive on all screen sizes
-   Navigation works correctly
-   All links functional

### Design (25%)

-   Professional appearance
-   Cohesive color scheme
-   Good typography
-   Visual hierarchy

### Code Quality (25%)

-   Clean, organized code
-   Proper indentation
-   Meaningful names
-   Good comments

### Responsiveness (15%)

-   Mobile-first approach
-   Smooth breakpoints
-   Content adapts well
-   No horizontal scrolling

### Documentation (5%)

-   Complete README
-   Clear explanations
-   Validation reports

---

## 💡 Tips for Success

### Do's ✅

-   **Start with mobile layout first** — Mobile-first is easier
-   **Use semantic HTML** — Proper structure matters
-   **Test frequently** — Check each section as you build
-   **Keep it simple** — Clean design beats complexity
-   **Comment your code** — Explain complex sections
-   **Use browser DevTools** — Test responsive views
-   **Validate your code** — Catch errors early
-   **Get feedback** — Show others for fresh perspective

### Don'ts ❌

-   **Don't use floats** — Use Flexbox instead
-   **Don't use `!important`** — Fix specificity issues properly
-   **Don't ignore mobile** — Mobile traffic is significant
-   **Don't copy entire templates** — Build it yourself to learn
-   **Don't forget accessibility** — Alt text, semantic HTML
-   **Don't use inline styles** — Keep CSS in external file
-   **Don't use lorem ipsum** — Use real, relevant content
-   **Don't skip testing** — Test on multiple devices/browsers

---

## 📚 Resources for This Project

### Design Inspiration

-   [Dribbble](https://dribbble.com/search/landing-page) — Landing page designs
-   [Awwwards](https://www.awwwards.com/) — Award-winning websites
-   [Land-book](https://land-book.com/) — Landing page gallery
-   [One Page Love](https://onepagelove.com/) — One-page website showcase

### Free Images

-   [Unsplash](https://unsplash.com/) — High-quality free photos
-   [Pexels](https://www.pexels.com/) — Free stock photos
-   [Pixabay](https://pixabay.com/) — Free images and videos

### Icons

-   [Font Awesome](https://fontawesome.com/) — Icon library (CDN)
-   [Heroicons](https://heroicons.com/) — SVG icons
-   [Feather Icons](https://feathericons.com/) — Simple icons

### Color Tools

-   [Coolors](https://coolors.co/) — Color scheme generator
-   [Adobe Color](https://color.adobe.com/) — Color wheel and schemes
-   [Color Hunt](https://colorhunt.co/) — Curated color palettes

### CSS Tools

-   [Can I Use](https://caniuse.com/) — Browser support tables
-   [CSS Gradient](https://cssgradient.io/) — Gradient generator
-   [Box Shadow Generator](https://cssgenerator.org/box-shadow-css-generator.html)

### Validation & Testing

-   [W3C HTML Validator](https://validator.w3.org/)
-   [W3C CSS Validator](https://jigsaw.w3.org/css-validator/)
-   [Wave Accessibility Tool](https://wave.webaim.org/)

---

## 🎉 Mini Project Summary

Congratulations on reaching Mini Project 1! This is your opportunity to:

✅ Apply everything learned in Weeks 01-05
✅ Build a complete, professional webpage from scratch
✅ Practice responsive design with Flexbox
✅ Create a portfolio piece to showcase your skills
✅ Experience real-world web development workflow
✅ Gain confidence in HTML & CSS fundamentals

**This project demonstrates your ability to:**

-   Write semantic, valid HTML
-   Style with modern CSS techniques
-   Create responsive layouts
-   Organize and document code professionally
-   Problem-solve and debug independently

**Take your time, be creative, and make it your own!**

---

## 🚦 Next Steps

After completing Mini Project 1:

1. **Review your code** — Look for improvements
2. **Get feedback** — Share with peers or instructor
3. **Iterate** — Make refinements based on feedback
4. **Deploy** — Put it live with GitHub Pages or Netlify
5. **Document** — Update README with final notes
6. **Celebrate** — You've built a real webpage! 🎉

**Week 06 Preview:** Responsive Design & CSS Grid fundamentals

---

**Navigation:**
← [Week 05 Session 14](session-14.md) | [Week 05 Index](../week-05.md) | [Week 06](../week-06.md) →
