# Mini Project 01: Personal Portfolio Website (Weeks 01-03)

**Coverage:** Sessions 01-09 (HTML & CSS Foundations)
**Duration:** 1 week (work outside class)
**Total Points:** 100

---

## 🎯 Project Overview

Build a **complete personal portfolio website** to showcase your HTML and CSS skills learned in the first three weeks. This project demonstrates your understanding of HTML structure, semantic markup, CSS styling, and basic layout techniques.

**What You'll Build:**

A multi-page portfolio website with:

-   Homepage with hero section, skills, and projects
-   About page with your background and experience
-   Contact page with a functional contact form
-   Consistent navigation and styling across all pages
-   Professional design with proper spacing and layout

**Skills Demonstrated:**

-   ✅ HTML5 semantic structure
-   ✅ Forms, tables, and lists
-   ✅ CSS selectors and styling
-   ✅ Box model and spacing
-   ✅ Layout and positioning
-   ✅ Typography and color schemes

---

## 📁 Project Setup

### File Structure

Create a project folder with the following structure:

```
portfolio-project/
├── index.html          (Homepage)
├── about.html          (About page)
├── contact.html        (Contact page)
├── css/
│   └── styles.css      (Main stylesheet)
├── images/             (Optional: for photos/icons)
│   └── profile.jpg
└── README.md           (Project documentation)
```

### Technical Requirements

-   **Pure HTML & CSS only** — No frameworks or libraries
-   **External CSS** — All styles in separate CSS file(s)
-   **Valid HTML5** — Use proper semantic markup
-   **Accessibility** — Include alt text, labels, and semantic elements
-   **Cross-browser** — Test in Chrome, Firefox, or Edge
-   **Clean code** — Proper indentation and comments

---

## 📄 Page 1: Homepage (index.html)

### Required Sections

**1. Header (Navigation)**

-   Site logo or your name
-   Navigation menu linking to all pages:
    -   Home (index.html)
    -   About (about.html)
    -   Contact (contact.html)

**2. Hero Section**

-   Large, eye-catching heading with your name or tagline
-   Subtitle describing who you are (e.g., "Web Developer | Designer | Creator")
-   Brief introduction paragraph (2-3 sentences)
-   Call-to-action button (e.g., "View My Work" or "Contact Me")

**3. Skills Section**

-   Section heading: "My Skills" or "What I Do"
-   Display your skills using:
    -   **Option A:** Unordered list with at least 6 skills
    -   **Option B:** Grid of skill cards with icons/emojis
-   Example skills: HTML, CSS, Design, Problem Solving, etc.

**4. Projects Section**

-   Section heading: "My Projects" or "Portfolio"
-   Create a **table** showcasing at least 3 projects:
    -   Columns: Project Name, Description, Technologies, Year/Status
    -   Style the table with borders, padding, and alternating row colors
-   **Alternative:** Create project cards instead of a table (bonus points!)

**5. Footer**

-   Copyright notice: "© 2025 Your Name. All rights reserved."
-   Social media links (GitHub, LinkedIn, Twitter, etc.) — can be placeholder links
-   Optional: Quick links to main pages

### Styling Requirements (Homepage)

-   Sticky or fixed navigation header
-   Hero section with background color or gradient
-   Consistent spacing using margins and padding
-   Professional color scheme (3-5 colors)
-   Hover effects on links and buttons

---

## 👤 Page 2: About Page (about.html)

### Required Content

**1. Header & Navigation**

-   Same header/navigation as homepage
-   Maintain consistency across pages

**2. About Me Section**

-   Page heading: "About Me"
-   Profile photo or placeholder image with:
    -   Proper `alt` attribute
    -   Styled with border-radius for rounded corners
    -   Max-width for responsive sizing
-   Personal introduction (150-200 words or lorem ipsum):
    -   Who you are
    -   Your background
    -   Your interests or goals

**3. Education/Experience Section**

-   Section heading: "Education" or "Experience"
-   Use an **ordered or unordered list** to display:
    -   Educational background (schools, courses, certifications)
    -   **OR** Work experience/projects
    -   **OR** Hobbies and interests
-   At least 3-4 list items

**4. Optional: Timeline or Journey**

-   Visual representation of your journey
-   Can use styled divs with positioning

**5. Footer**

-   Same footer as homepage

### Styling Requirements (About Page)

-   Image styling with box-shadow or border
-   Two-column layout for text and image (optional, but recommended)
-   Proper spacing and readability for text content
-   Section dividers or backgrounds

---

## 📧 Page 3: Contact Page (contact.html)

### Required Content

**1. Header & Navigation**

-   Same header/navigation as other pages

**2. Contact Form**

Create a contact form with the following fields:

**Required Form Fields:**

-   **Name** (text input)
    -   Label: "Your Name"
    -   Required attribute
    -   Placeholder text
-   **Email** (email input)
    -   Label: "Your Email"
    -   Required attribute
    -   Proper email validation
-   **Subject** (text input)
    -   Label: "Subject"
    -   Optional
-   **Message** (textarea)
    -   Label: "Your Message"
    -   Required attribute
    -   Minimum 5 rows
-   **Submit Button**
    -   Text: "Send Message" or "Submit"

**Form Best Practices:**

-   Use `<label>` elements properly associated with inputs
-   Use appropriate input types (`type="email"`, etc.)
-   Include `name` attributes for all inputs
-   Add `required` attributes where needed
-   Group related fields using `<fieldset>` (optional bonus)

**3. Contact Information (Optional)**

-   Display alternative contact methods:
    -   Email address
    -   Phone number
    -   Location/Address
    -   Social media links

**4. Footer**

-   Same footer as other pages

### Styling Requirements (Contact Page)

-   Form fields styled with:
    -   Padding and borders
    -   Full width or fixed width
    -   Focus states (`:focus` pseudo-class)
-   Submit button styled with:
    -   Background color and text color
    -   Padding and border-radius
    -   Hover effects
-   Vertical stacking of form elements
-   Proper spacing between fields
-   Form centered or in a card/container

---

## 🎨 Overall CSS Requirements

Apply these styling rules across all pages:

### 1. CSS Reset & Box Model

```css
*,
*::before,
*::after {
	box-sizing: border-box;
}

body {
	margin: 0;
	padding: 0;
	font-family: Arial, sans-serif;
}
```

### 2. Typography

-   Choose a readable font family (can use system fonts)
-   Set font sizes: h1 (32-48px), h2 (24-32px), h3 (18-24px), body (16-18px)
-   Line height: at least 1.5 for body text
-   Letter spacing for headings (optional)

### 3. Color Scheme

Choose a professional color palette:

-   Primary color (brand/accent)
-   Secondary color (complementary)
-   Text color (dark gray or black)
-   Background colors (white, light gray)
-   At least 3-5 colors total

### 4. Layout & Spacing

-   Centered container: max-width 1200px, centered with `margin: 0 auto`
-   Consistent section padding (e.g., 60px vertical, 20px horizontal)
-   Margins between elements (16px, 24px, 32px system)
-   Use of whitespace for visual breathing room

### 5. Navigation

-   Horizontal navigation menu
-   Remove default list styling
-   Links styled with:
    -   Color change on hover
    -   Smooth transitions
    -   Active page indicator (optional)

### 6. Responsive Elements

-   Images: `max-width: 100%; height: auto;`
-   Container padding on small screens
-   Readable text on all screen sizes

---

## 🌟 Bonus Challenges (Optional)

Earn extra points by implementing these advanced features:

### Design Enhancements (+5 points)

-   [ ] Custom 404 error page
-   [ ] Favicon for the website
-   [ ] CSS animations (fade-in, slide-in effects)
-   [ ] Gradient backgrounds
-   [ ] Box shadows and depth

### Layout Techniques (+5 points)

-   [ ] Sticky header that stays at top when scrolling
-   [ ] "Back to top" button (fixed position)
-   [ ] Multi-column layout on about page
-   [ ] Card-based project display instead of table
-   [ ] Sidebar layout

### Interactive Elements (+5 points)

-   [ ] CSS-only dropdown menu
-   [ ] Smooth scroll behavior
-   [ ] Form validation styling (valid/invalid states)
-   [ ] Tooltips on hover
-   [ ] Modal/lightbox effect (CSS only)

### Advanced Styling (+5 points)

-   [ ] Dark mode toggle (CSS variables)
-   [ ] Custom styled table
-   [ ] Progress bars for skills
-   [ ] Social media icon fonts or SVGs
-   [ ] Responsive navigation (hamburger menu concept)

---

## ✅ Grading Rubric

| Category           | Points | Criteria                                                                |
| ------------------ | ------ | ----------------------------------------------------------------------- |
| **HTML Structure** | 25     | Valid HTML5, semantic elements, proper hierarchy, all required sections |
| **CSS Styling**    | 25     | Professional design, consistent spacing, color scheme, typography       |
| **Homepage**       | 15     | Complete with all required sections and proper styling                  |
| **About Page**     | 15     | Complete content, image, list, proper layout                            |
| **Contact Page**   | 15     | Functional form with all fields, labels, and styling                    |
| **Code Quality**   | 5      | Clean, indented, commented, valid code                                  |
| **Bonus Features** | +20    | Extra credit for advanced implementations                               |
| **Total**          | 100    | (+20 bonus possible)                                                    |

### Detailed Breakdown

**HTML Structure (25 points):**

-   Valid HTML5 doctype and structure (5 pts)
-   Proper use of semantic elements (5 pts)
-   Heading hierarchy maintained (3 pts)
-   All required attributes present (alt, href, etc.) (4 pts)
-   Forms with proper labels and input types (4 pts)
-   Links working between pages (4 pts)

**CSS Styling (25 points):**

-   External stylesheet properly linked (3 pts)
-   Box model and spacing (6 pts)
-   Typography and readability (5 pts)
-   Color scheme and design consistency (5 pts)
-   Navigation styling with hover effects (3 pts)
-   Form styling (3 pts)

**Code Quality (5 points):**

-   Proper indentation (2 pts)
-   Meaningful class names (1 pt)
-   Comments where needed (1 pt)
-   No broken links or errors (1 pt)

---

## 📋 Submission Requirements

### What to Submit

1. **Complete project folder** containing:

    - All HTML files (index.html, about.html, contact.html)
    - CSS folder with styles.css
    - Images folder (if you used images)
    - README.md file (optional but recommended)

2. **README.md** should include:

    - Project title and description
    - Technologies used (HTML5, CSS3)
    - Features implemented
    - Any bonus features completed
    - Challenges faced and how you solved them
    - Screenshots (optional)

3. **Submission format:**
    - ZIP file named: `miniproject01-yourname.zip`
    - Or GitHub repository link (if using version control)

### Submission Checklist

Before submitting, verify:

-   [ ] All three HTML pages are complete
-   [ ] Navigation links work between all pages
-   [ ] Contact form has all required fields with proper labels
-   [ ] CSS file is linked and styles are applied
-   [ ] All images have alt attributes
-   [ ] Code is properly indented and formatted
-   [ ] No broken links or missing files
-   [ ] Tested in a modern browser (Chrome, Firefox, or Edge)
-   [ ] HTML validates (use [W3C Validator](https://validator.w3.org/))
-   [ ] Project folder is properly organized
-   [ ] README.md included (optional)

---

## 💡 Development Tips

### Getting Started

1. **Plan first:** Sketch your layout on paper or wireframe tool
2. **Start with HTML:** Build structure before styling
3. **One page at a time:** Complete index.html, then about, then contact
4. **Test frequently:** Open in browser after each section
5. **Use placeholders:** Lorem ipsum, placeholder images are fine

### Best Practices

-   **Semantic HTML:** Use `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`
-   **Meaningful names:** Use descriptive class names (`.hero-section`, not `.div1`)
-   **DRY principle:** Don't repeat styles—use classes for reusable styles
-   **Mobile-first thinking:** Even without media queries, think about smaller screens
-   **Comments:** Add comments to organize your CSS sections

### Debugging Tips

-   **Use DevTools:** Right-click → Inspect to debug CSS
-   **Border trick:** Add `border: 1px solid red;` to see element boundaries
-   **Validate:** Use W3C HTML and CSS validators
-   **Console:** Check browser console for errors
-   **Live Server:** Use VS Code Live Server extension for auto-refresh

### Time Management

**Suggested timeline (1 week):**

-   **Day 1-2:** Plan and build HTML structure for all pages
-   **Day 3-4:** Create and apply CSS styling
-   **Day 5:** Refine design, add polish
-   **Day 6:** Test, fix bugs, validate code
-   **Day 7:** Final review and submit

---

## 📚 Resources & References

### Course Materials

Review these sessions:

-   **Session 01-03:** HTML fundamentals, links, images
-   **Session 04:** HTML tables
-   **Session 05-06:** HTML forms
-   **Session 07:** CSS basics and selectors
-   **Session 08:** CSS box model
-   **Session 09:** CSS positioning and layout

### External Resources

**Documentation:**

-   [MDN HTML Reference](https://developer.mozilla.org/en-US/docs/Web/HTML)
-   [MDN CSS Reference](https://developer.mozilla.org/en-US/docs/Web/CSS)
-   [W3Schools HTML Tutorial](https://www.w3schools.com/html/)
-   [W3Schools CSS Tutorial](https://www.w3schools.com/css/)

**Tools:**

-   [W3C HTML Validator](https://validator.w3.org/)
-   [W3C CSS Validator](https://jigsaw.w3.org/css-validator/)
-   [Can I Use](https://caniuse.com/) — Browser compatibility
-   [Google Fonts](https://fonts.google.com/) — Free web fonts
-   [Coolors](https://coolors.co/) — Color scheme generator

**Placeholder Content:**

-   [Lorem Ipsum Generator](https://www.lipsum.com/)
-   [Placeholder Images](https://placeholder.com/)
-   [Unsplash](https://unsplash.com/) — Free photos

---

## 🎓 Learning Objectives Assessment

This project demonstrates your ability to:

✅ **Create valid HTML5 documents** with proper structure
✅ **Use semantic HTML elements** appropriately
✅ **Build forms** with proper labels and input types
✅ **Create tables** with headers and data cells
✅ **Apply CSS styling** using selectors and properties
✅ **Implement the box model** with margins, padding, borders
✅ **Create layouts** using positioning and display properties
✅ **Design with typography** and color schemes
✅ **Link multiple pages** together with navigation
✅ **Write clean, organized code** with proper formatting

---

## ⚠️ Important Notes

### Academic Integrity

-   This is an **individual project**
-   Write your own code from scratch
-   You may reference course materials and documentation
-   You may use placeholder images and lorem ipsum text
-   Do not copy entire designs or code from other students or websites
-   Inspiration is fine, but the code should be yours

### What You CAN Use

-   Course materials and examples
-   MDN, W3Schools, and other documentation
-   Google Fonts
-   Free stock photos (Unsplash, Pexels, etc.)
-   Lorem ipsum generators
-   Color palette generators
-   Your own creativity!

### What You CANNOT Use

-   CSS frameworks (Bootstrap, Tailwind, etc.)
-   JavaScript libraries or frameworks
-   Code copied from CodePen, GitHub, or other sources
-   Templates or themes
-   AI-generated code (unless you fully understand and modify it)

---

## 🆘 Getting Help

### When You're Stuck

1. **Review session materials** — Look at examples and exercises
2. **Check documentation** — MDN and W3Schools are your friends
3. **Use DevTools** — Inspect element to debug CSS
4. **Ask specific questions** — "My navigation won't center" not "My code doesn't work"
5. **Break it down** — Solve one small problem at a time

### Office Hours & Support

-   Attend office hours for help
-   Post questions in class discussion forum
-   Review with study group (but write your own code!)
-   Use online validators to find errors

---

## 🎉 Final Thoughts

This project is your opportunity to:

-   **Showcase what you've learned** in the first three weeks
-   **Build something you can be proud of** and add to your portfolio
-   **Practice real-world web development** skills
-   **Develop good coding habits** early in your journey

**Remember:**

-   Focus on meeting requirements first, then enhance
-   Clean, simple design is better than complex, broken design
-   Code quality matters as much as visual design
-   This is a learning project—mistakes are part of the process!

**You've got this! 🚀**

Good luck and have fun building your portfolio website!
