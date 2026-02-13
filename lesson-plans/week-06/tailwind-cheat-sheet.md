# Tailwind CSS Utility Classes Cheat Sheet

A quick reference for the Tailwind-like utility classes available in `tailwind-utilities.css`.

---

## 📐 Layout & Display

| Class | CSS Property |
|-------|-------------|
| `.block` | `display: block` |
| `.inline-block` | `display: inline-block` |
| `.inline` | `display: inline` |
| `.flex` | `display: flex` |
| `.inline-flex` | `display: inline-flex` |
| `.grid` | `display: grid` |
| `.hidden` | `display: none` |

---

## 📦 Flexbox

### Direction
| Class | Effect |
|-------|--------|
| `.flex-row` | Items flow left to right |
| `.flex-row-reverse` | Items flow right to left |
| `.flex-col` | Items stack top to bottom |
| `.flex-col-reverse` | Items stack bottom to top |

### Wrap
| Class | Effect |
|-------|--------|
| `.flex-wrap` | Items wrap to next line |
| `.flex-nowrap` | Items stay on one line |
| `.flex-wrap-reverse` | Items wrap in reverse |

### Grow & Shrink
| Class | CSS | Use Case |
|-------|-----|----------|
| `.flex-1` | `flex: 1 1 0%` | Equal distribution |
| `.flex-auto` | `flex: 1 1 auto` | Grow based on content |
| `.flex-none` | `flex: none` | Fixed size |
| `.grow` | `flex-grow: 1` | Allow growing |
| `.shrink-0` | `flex-shrink: 0` | Prevent shrinking |

---

## 🔲 Grid

### Grid Columns
| Class | Columns |
|-------|---------|
| `.grid-cols-1` | 1 column |
| `.grid-cols-2` | 2 equal columns |
| `.grid-cols-3` | 3 equal columns |
| `.grid-cols-4` | 4 equal columns |
| `.grid-cols-6` | 6 equal columns |
| `.grid-cols-12` | 12-column system |

### Column Span
| Class | Spans |
|-------|-------|
| `.col-span-2` | Spans 2 columns |
| `.col-span-3` | Spans 3 columns |
| `.col-span-6` | Spans 6 columns (half in 12-col) |
| `.col-span-full` | Spans entire row |

---

## 📏 Gap (Spacing Between Items)

**Formula:** `gap-{n}` where `n × 0.25rem` = actual size

| Class | Size |
|-------|------|
| `.gap-0` | 0 |
| `.gap-1` | 0.25rem (4px) |
| `.gap-2` | 0.5rem (8px) |
| `.gap-4` | 1rem (16px) |
| `.gap-6` | 1.5rem (24px) |
| `.gap-8` | 2rem (32px) |

**Axis-specific:** `.gap-x-4` (horizontal), `.gap-y-4` (vertical)

---

## ↔️ Justify Content (Main Axis)

| Class | Alignment |
|-------|-----------|
| `.justify-start` | Items at start |
| `.justify-end` | Items at end |
| `.justify-center` | Items centered |
| `.justify-between` | Space between items |
| `.justify-around` | Space around items |
| `.justify-evenly` | Equal space |

---

## ↕️ Align Items (Cross Axis)

| Class | Alignment |
|-------|-----------|
| `.items-start` | Items at top |
| `.items-end` | Items at bottom |
| `.items-center` | Items centered |
| `.items-baseline` | Text baselines align |
| `.items-stretch` | Items fill height |

---

## 📐 Width & Height

### Width Scale

| Class | Width |
|-------|-------|
| `.w-4` | 1rem (16px) |
| `.w-8` | 2rem (32px) |
| `.w-16` | 4rem (64px) |
| `.w-32` | 8rem (128px) |
| `.w-64` | 16rem (256px) |
| `.w-1/2` | 50% |
| `.w-1/3` | 33.33% |
| `.w-2/3` | 66.67% |
| `.w-full` | 100% |
| `.w-screen` | 100vw |

### Height Scale

| Class | Height |
|-------|--------|
| `.h-4` | 1rem (16px) |
| `.h-8` | 2rem (32px) |
| `.h-16` | 4rem (64px) |
| `.h-32` | 8rem (128px) |
| `.h-64` | 16rem (256px) |
| `.h-full` | 100% |
| `.h-screen` | 100vh |

### Max Width
| Class | Max Width |
|-------|-----------|
| `.max-w-sm` | 24rem (384px) |
| `.max-w-md` | 28rem (448px) |
| `.max-w-lg` | 32rem (512px) |
| `.max-w-xl` | 36rem (576px) |
| `.max-w-2xl` | 42rem (672px) |
| `.max-w-4xl` | 56rem (896px) |

---

## 🔳 Padding

**Formula:** `p{side}-{n}` where `n × 0.25rem` = actual size

| Prefix | Sides |
|--------|-------|
| `p-` | All sides |
| `px-` | Left + Right |
| `py-` | Top + Bottom |
| `pt-`, `pr-`, `pb-`, `pl-` | Individual sides |

### Common Values
| Class | Value |
|-------|-------|
| `.p-1` | 0.25rem (4px) |
| `.p-2` | 0.5rem (8px) |
| `.p-4` | 1rem (16px) |
| `.p-6` | 1.5rem (24px) |
| `.p-8` | 2rem (32px) |

---

## 📏 Margin

**Same pattern as padding, with `m` prefix**

| Prefix | Sides |
|--------|-------|
| `m-` | All sides |
| `mx-` | Left + Right |
| `my-` | Top + Bottom |
| `mt-`, `mr-`, `mb-`, `ml-` | Individual |

### Special Values
| Class | Use |
|-------|-----|
| `.mx-auto` | Center horizontally |
| `.ml-auto` | Push to right |
| `.mr-auto` | Push to left |
| `.mt-auto` | Push to bottom |
| `.-mt-4` | Negative margin (overlap) |

---

## 🔤 Typography

### Font Size
| Class | Size |
|-------|------|
| `.text-xs` | 0.75rem (12px) |
| `.text-sm` | 0.875rem (14px) |
| `.text-base` | 1rem (16px) |
| `.text-lg` | 1.125rem (18px) |
| `.text-xl` | 1.25rem (20px) |
| `.text-2xl` | 1.5rem (24px) |
| `.text-3xl` | 1.875rem (30px) |
| `.text-4xl` | 2.25rem (36px) |

### Font Weight
| Class | Weight |
|-------|--------|
| `.font-light` | 300 |
| `.font-normal` | 400 |
| `.font-medium` | 500 |
| `.font-semibold` | 600 |
| `.font-bold` | 700 |
| `.font-extrabold` | 800 |

### Text Alignment
| Class | Alignment |
|-------|-----------|
| `.text-left` | Left aligned |
| `.text-center` | Centered |
| `.text-right` | Right aligned |
| `.text-justify` | Justified |

### Text Transform
| Class | Transform |
|-------|-----------|
| `.uppercase` | UPPERCASE |
| `.lowercase` | lowercase |
| `.capitalize` | Capitalize Each |
| `.normal-case` | Normal |

### Text Decoration
| Class | Style |
|-------|-------|
| `.underline` | Underlined |
| `.line-through` | ~~Strikethrough~~ |
| `.no-underline` | Remove underline |

---

## 🎨 Colors

### Text Colors
```
.text-{color}-{shade}
```

| Base Colors | Shades Available |
|-------------|------------------|
| gray | 100-900 |
| red | 500, 600, 700 |
| green | 500, 600, 700 |
| blue | 500, 600, 700 |
| yellow | 500, 600 |
| purple | 500, 600 |

**Examples:**
- `.text-gray-700` - Dark gray text
- `.text-blue-500` - Blue text
- `.text-white` - White text
- `.text-black` - Black text

### Background Colors
```
.bg-{color}-{shade}
```

**Examples:**
- `.bg-gray-100` - Light gray background
- `.bg-blue-500` - Blue background
- `.bg-white` - White background
- `.bg-transparent` - Transparent

---

## 📦 Borders

### Border Width
| Class | Width |
|-------|-------|
| `.border` | 1px |
| `.border-2` | 2px |
| `.border-4` | 4px |
| `.border-0` | 0 (remove) |
| `.border-t` | Top only |
| `.border-b` | Bottom only |

### Border Radius
| Class | Radius |
|-------|--------|
| `.rounded-none` | 0 |
| `.rounded-sm` | 0.125rem |
| `.rounded` | 0.25rem |
| `.rounded-md` | 0.375rem |
| `.rounded-lg` | 0.5rem |
| `.rounded-xl` | 0.75rem |
| `.rounded-2xl` | 1rem |
| `.rounded-full` | 9999px (circle) |

### Border Colors
| Class | Color |
|-------|-------|
| `.border-gray-200` | Light gray |
| `.border-gray-300` | Gray |
| `.border-blue-500` | Blue |
| `.border-transparent` | Invisible |

---

## 🌑 Shadows

| Class | Effect |
|-------|--------|
| `.shadow-sm` | Subtle shadow |
| `.shadow` | Default shadow |
| `.shadow-md` | Medium shadow |
| `.shadow-lg` | Large shadow |
| `.shadow-xl` | Extra large |
| `.shadow-2xl` | Maximum shadow |
| `.shadow-none` | Remove shadow |

---

## 📍 Positioning

### Position Type
| Class | Position |
|-------|----------|
| `.static` | Default flow |
| `.relative` | Relative to self |
| `.absolute` | Relative to parent |
| `.fixed` | Relative to viewport |
| `.sticky` | Sticky on scroll |

### Placement
| Class | Placement |
|-------|-----------|
| `.top-0` | Top edge |
| `.right-0` | Right edge |
| `.bottom-0` | Bottom edge |
| `.left-0` | Left edge |
| `.inset-0` | All edges (full cover) |

### Z-Index
| Class | Z-Index |
|-------|---------|
| `.z-0` | 0 |
| `.z-10` | 10 |
| `.z-20` | 20 |
| `.z-50` | 50 |

---

## 🎭 Transitions & Transforms

### Transitions
| Class | Transition |
|-------|------------|
| `.transition` | All properties |
| `.transition-colors` | Color changes |
| `.transition-opacity` | Fade effects |
| `.transition-transform` | Movement/scale |

### Duration
| Class | Time |
|-------|------|
| `.duration-150` | 150ms |
| `.duration-200` | 200ms |
| `.duration-300` | 300ms |
| `.duration-500` | 500ms |

### Transforms
| Class | Effect |
|-------|--------|
| `.scale-95` | 95% size |
| `.scale-100` | Normal size |
| `.scale-105` | 105% size |
| `.scale-110` | 110% size |
| `.rotate-45` | Rotate 45° |
| `.rotate-90` | Rotate 90° |
| `.rotate-180` | Rotate 180° |

---

## 🖱️ Interactive States

### Hover States
Add `hover:` prefix to activate on hover:
```html
<button class="bg-blue-500 hover:bg-blue-600">
  Hover Me
</button>
```

| Class | Effect |
|-------|--------|
| `.hover\:bg-gray-100` | Gray background on hover |
| `.hover\:text-blue-500` | Blue text on hover |
| `.hover\:underline` | Underline on hover |
| `.hover\:scale-105` | Slightly larger on hover |
| `.hover\:shadow-lg` | Shadow on hover |

### Focus States
| Class | Effect |
|-------|--------|
| `.focus\:outline-none` | Remove outline |
| `.focus\:ring-2` | Ring effect |
| `.focus\:border-blue-500` | Blue border |

### Active States
| Class | Effect |
|-------|--------|
| `.active\:bg-blue-700` | Darker on click |
| `.active\:scale-95` | Slightly smaller when pressed |

---

## 🎯 Common Patterns

### Centering Content
```html
<!-- Flex center -->
<div class="flex items-center justify-center">
  Centered
</div>

<!-- Grid center -->
<div class="grid place-items-center">
  Centered
</div>
```

### Card Component
```html
<div class="bg-white rounded-lg shadow-md p-6">
  <h3 class="text-xl font-bold text-gray-900">Card Title</h3>
  <p class="text-gray-600 mt-2">Card content here.</p>
</div>
```

### Button
```html
<button class="btn btn-primary">
  Click Me
</button>

<!-- Or build from scratch -->
<button class="bg-blue-500 hover:bg-blue-600 text-white font-medium py-2 px-4 rounded-md transition">
  Click Me
</button>
```

### Navigation Bar
```html
<nav class="flex items-center justify-between bg-gray-800 text-white px-6 py-4">
  <div class="text-xl font-bold">Logo</div>
  <div class="flex gap-6">
    <a href="#" class="hover:text-blue-400 transition-colors">Home</a>
    <a href="#" class="hover:text-blue-400 transition-colors">About</a>
    <a href="#" class="hover:text-blue-400 transition-colors">Contact</a>
  </div>
</nav>
```

### Grid Layout
```html
<div class="grid grid-cols-3 gap-4">
  <div class="col-span-1">Sidebar</div>
  <div class="col-span-2">Main Content</div>
</div>
```

---

## 🔤 Naming Convention

Tailwind uses a consistent naming pattern:

```
{property}-{side?}-{size/value}
```

**Examples:**
- `p-4` → padding: 1rem
- `pt-4` → padding-top: 1rem
- `px-4` → padding-left & padding-right: 1rem
- `m-auto` → margin: auto
- `text-lg` → font-size: 1.125rem


## 📚 Size Scale Reference

| Number | rem | pixels |
|--------|-----|--------|
| 0 | 0 | 0 |
| 1 | 0.25rem | 4px |
| 2 | 0.5rem | 8px |
| 3 | 0.75rem | 12px |
| 4 | 1rem | 16px |
| 5 | 1.25rem | 20px |
| 6 | 1.5rem | 24px |
| 8 | 2rem | 32px |
| 10 | 2.5rem | 40px |
| 12 | 3rem | 48px |
| 16 | 4rem | 64px |
| 20 | 5rem | 80px |
| 24 | 6rem | 96px |
| 32 | 8rem | 128px |
| 40 | 10rem | 160px |
| 48 | 12rem | 192px |
| 64 | 16rem | 256px |

---

## 💡 Tips

1. **Combine classes** for complex styles:
   ```html
   <div class="flex items-center justify-between p-4 bg-white rounded-lg shadow-md">
   ```

2. **Use semantic class names** in addition to utilities for readability

3. **Remember the formula**: most spacing uses `value × 0.25rem`

4. **Order doesn't matter**: `p-4 m-2 bg-blue-500` = `bg-blue-500 m-2 p-4`

5. **Group related utilities** for readability:
   ```html
   <!-- Layout → Spacing → Appearance → Effects -->
   <div class="flex flex-col gap-4 | p-6 | bg-white rounded-lg | shadow-md transition">
   ```
