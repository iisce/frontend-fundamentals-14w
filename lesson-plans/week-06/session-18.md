# Week 06 — Session 18: Combining Flexbox & Grid

**Navigation:**
← [Session 17](session-17.md) | [Week 06 Index](../week-06.md) | [Week 07 Index](../week-07.md) →

---

**Session Length:** 90 minutes

## 📋 Pre-Class Checklist

Before starting this session, make sure you have:

-   ✅ Completed Session 17 (CSS Grid Fundamentals)
-   ✅ Solid understanding of both Flexbox and CSS Grid
-   ✅ Code editor (VS Code)

## 🎯 Learning Objectives

By the end of this session, you will be able to:

-   Determine when to use Flexbox vs. CSS Grid
-   Combine Flexbox and Grid effectively in a single layout
-   Build complex, real-world page structures
-   Implement common UI patterns using both systems
-   Understand layout best practices for modern web development

## 🔑 Key Terms

**Hybrid Layout**, **Layout Strategy**, **Component-Based Layout**, **Page Structure**, **Flex vs. Grid Decision Matrix**

---

## Part 1: Flexbox vs. Grid — When to use what? (20 minutes)

One of the most common questions in modern CSS is: "Should I use Flexbox or Grid?"

### The Decision Matrix

| Feature | Flexbox | CSS Grid |
| :--- | :--- | :--- |
| **Dimension** | One-dimensional (Row OR Column) | Two-dimensional (Row AND Column) |
| **Alignment** | Content-based (items flow naturally) | Container-based (items follow a predefined grid) |
| **Overlap** | Hard to overlap items | Easy to overlap items in cells |
| **Gaps** | `gap` works well | `gap` works well |
| **Best For** | Components, small-scale alignment | Page layout, complex grids |

### Rule of Thumb:
- Use **Grid** for the **"Skeleton"** of your page (the overall layout).
- Use **Flexbox** for the **"Muscles"** inside the blocks (the content alignment).

---

## Part 2: Nesting Flexbox in Grid (25 minutes)

This is the most common pattern in professional web development.

### Scenario: A Website Header
You might use **Grid** to define the header area in the overall page, but inside the header, you use **Flexbox** to spread out the logo, menu links, and search bar.

```css
/* Page Skeleton (Grid) */
.page-container {
    display: grid;
    grid-template-areas:
        "header"
        "main"
        "footer";
}

/* Header Component (Flexbox) */
header {
    grid-area: header;
    display: flex; /* This element is a Grid item AND a Flex container */
    justify-content: space-between;
    align-items: center;
}
```

### Scenario: A Card Component
You might use **Grid** to create a 3-column list of cards, but each card uses **Flexbox** to vertically align its title, image, and "Read More" button.

```css
/* Grid for the list */
.card-list {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
}

/* Flexbox for the card content */
.card {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}
```

---

## Part 3: Building a Complete Page Layout (25 minutes)

### The "Dashboard" Pattern
Dashboards often have a fixed sidebar and a header that stay in place while the content scrolls or changes.

1.  **Grid** defines the Sidebar (left) and Viewport (right).
2.  **Grid** defines the Header (top) and Content (bottom) within the Viewport.
3.  **Flexbox** handles the navigation links in the Sidebar.
4.  **Flexbox** handles the user profile dropdown in the Header.

---

## Part 4: Real-World Patterns (20 minutes)

### Responsive Hybrid Strategies
Combining media queries with Flexbox and Grid allows for powerful transitions.

- **On Mobile:** Change Grid from 2-columns to 1-column.
- **On Desktop:** Use Flexbox `row` for navigation; switch to `column` for mobile.

---

## 🎨 Hands-On Exercise: The Profile Page

**Goal:** Create a simple profile layout.
- The page has a Header (full width).
- Below the header, a Sidebar (left) and Profile Details (right).
- Inside Profile Details, a grid of "Achievement" badges.

**Starter HTML:**
```html
<div class="layout">
  <header>Logo & Search</header>
  <aside>Navigation</aside>
  <main>
    <section class="details">
      <h2>User Profile</h2>
      <div class="badges">
        <div class="badge">A</div>
        <div class="badge">B</div>
        <div class="badge">C</div>
      </div>
    </section>
  </main>
</div>
```

**Instruction:** Apply both Flexbox and Grid.

<details>
<summary>✅ Solution</summary>

```css
.layout {
    display: grid;
    grid-template-areas:
        "head head"
        "nav content";
    grid-template-columns: 200px 1fr;
    min-height: 100vh;
}

header {
    grid-area: head;
    display: flex;
    justify-content: space-between;
    padding: 20px;
    background: #333;
    color: white;
}

aside {
    grid-area: nav;
    background: #f4f4f4;
}

main {
    grid-area: content;
    padding: 20px;
}

.badges {
    display: flex; /* Flexbox for horizontal badges */
    gap: 10px;
    margin-top: 20px;
}

.badge {
    background: gold;
    padding: 10px 20px;
    border-radius: 20px;
}
```
</details>

---

## 🏡 Homework Assignment

**The "Z-Pattern" Landing Page**

Build a landing page section that alternates images and text blocks:
- Row 1: Text Left | Image Right
- Row 2: Image Left | Text Right
- Row 3: Text Left | Image Right

**Requirements:**
1. Use **Grid** for the 2-column sections.
2. Use **Flexbox** inside the text blocks to center headings and buttons vertically.
3. Use a **Media Query** so that on screens smaller than 768px, all sections stack (Image Top | Text Bottom).

---

**Navigation:**
← [Session 17](session-17.md) | [Week 06 Index](../week-06.md) | [Week 07 Index](../week-07.md) →
