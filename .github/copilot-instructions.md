# Copilot Instructions for Session Development

This document provides guidance on how to effectively use GitHub Copilot when creating course materials for the Frontend Fundamentals course.

## 🎯 General Guidelines

### When Creating Session Materials

**DO:**
- Follow the structure defined in `session-instructions.md`
- Create all 6 components for each session (tutorial, cheat sheet, template, solution, visual guide, README updates)
- Maintain consistency with existing sessions
- Use progressive complexity (basic → intermediate → advanced)
- Include accessibility features in all examples
- Test all code examples before including them
- Provide complete, working solutions
- Use realistic, practical examples

**DON'T:**
- Skip any of the required components
- Create incomplete or toy examples
- Assume students have knowledge not covered in prerequisites
- Use external dependencies unless absolutely necessary
- Create sessions without clear learning objectives
- Forget to update the week's README file

## 📝 Prompt Engineering for Session Creation

### Initial Request Format

When requesting a new session or tutorial transformation:

```
Transform session-XX.md into a self-guided tutorial following these requirements:
- Duration: [80-90] minutes
- Topic: [specific topic]
- Prerequisites: [list prerequisites]
- Create all supporting files: cheat sheet, template, solution, visual guide
- Follow the structure in session-instructions.md
- Include accessibility examples throughout
- Add interactive quizzes with expandable answers
- Provide troubleshooting section
```

### Iterative Development

Break complex requests into steps:

1. **First:** "Create the main tutorial structure for session-XX on [topic]"
2. **Second:** "Create the cheat sheet reference guide"
3. **Third:** "Create the template and solution files"
4. **Fourth:** "Create the visual anatomy guide"
5. **Fifth:** "Update the README with all new materials"

### Specific Component Requests

**For tutorials:**
```
Create session-XX.md on [topic] with:
- Welcome section listing learning objectives and files
- Part 1: [concept] (30 min) with 3 quiz questions
- Part 2: [concept] (25 min) with 3 quiz questions
- Part 3: [concept] (20 min) with 3 quiz questions
- Part 4: Hands-on practice (40 min)
- Common mistakes section
- Homework challenge
- External resources
```

**For cheat sheets:**
```
Create [topic]-cheat-sheet.md with:
- Complete syntax table for [elements/attributes]
- Common patterns with code examples
- Accessibility considerations
- Common mistakes to avoid
- Quick troubleshooting tips
```

**For templates:**
```
Create [topic]-template.html with:
- Basic HTML structure
- Embedded CSS styling
- TODO comments for students
- Instructions box listing tasks
- [specific framework/structure needed]
```

**For solutions:**
```
Create [topic]-solution.html with:
- Complete working implementation of [feature]
- All accessibility features (ARIA, semantic HTML)
- Explanatory comments
- Best practices demonstrated
- Visual styling for demonstration
```

**For visual guides:**
```
Create [topic]-anatomy-visual.html with:
- Color-coded visualization of [concept]
- Legend explaining color scheme
- Interactive examples
- Visual arrows showing relationships
- Self-contained (inline CSS)
```

## 🔧 Working with Existing Sessions

### Updating Session Content

When requesting updates:
```
Update session-XX.md to add:
- [Specific content]
- Maintain existing structure
- Update time estimates if needed
- Add to appropriate part/section
```

### Maintaining Consistency

Reference existing sessions:
```
Create session-XX following the same structure and style as session-04:
- Same heading levels
- Similar quiz format
- Consistent emoji usage
- Similar timing breakdown
```

### README Updates

Always request README updates after creating files:
```
Update week-XX/README.md to include:
- Session XX as self-guided tutorial
- All new files in inventory table
- Learning materials section
- Practice files section
- Step-by-step learning path
- File descriptions table
- Help section updates
```

## 💡 Best Practices for Copilot Collaboration

### Provide Context

**Good:**
```
I'm creating session-07 on CSS selectors for a 14-week frontend course.
Students have completed HTML basics (sessions 01-03) and HTML tables/forms (sessions 04-06).
Create a self-guided tutorial following session-instructions.md structure.
Include specificity, inheritance, and cascade concepts.
```

**Not as effective:**
```
Create a CSS selectors tutorial.
```

### Be Specific About Requirements

**Good:**
```
Create a contact form template with:
- Name field (text, required, minlength=2)
- Email field (email, required)
- Phone field (tel, pattern for xxx-xxx-xxxx format)
- Message field (textarea, required, minlength=10)
- Submit button
- Embedded CSS with modern styling
- ARIA labels and descriptions
- TODO comments for students
```

**Not as effective:**
```
Create a form template.
```

### Request Validation and Testing

**Include:**
```
After creating [files], verify:
- All code examples are syntactically correct
- HTML validates
- Accessibility features are properly implemented
- File references in README match actual files
- All links work correctly
```

### Iterative Refinement

If output needs adjustment:
```
The [component] needs these improvements:
1. Add more detailed comments
2. Include ARIA attributes for [specific elements]
3. Expand the troubleshooting section to cover [issue]
4. Add a visual example of [concept]
```

## 📊 Structuring Multi-File Requests

### Option 1: Sequential Creation

Request files one at a time for more control:

1. "Create session-XX.md tutorial"
2. Review and approve
3. "Create [topic]-cheat-sheet.md"
4. Review and approve
5. Continue for remaining files

### Option 2: Batch Creation

Request all files at once for efficiency:

```
Create complete materials for session-XX on [topic]:
1. session-XX.md (self-guided tutorial, 4 parts, 90 min)
2. [topic]-cheat-sheet.md (reference guide)
3. [topic]-template.html (starter file)
4. [topic]-solution.html (complete example)
5. [topic]-anatomy-visual.html (color-coded guide)
6. Update week-XX/README.md

Follow session-instructions.md structure.
Include accessibility throughout.
```

## 🎨 Content Generation Tips

### Code Examples

Request complete, realistic examples:
```
Create a complete accessible [element] example showing:
- Proper semantic HTML
- ARIA attributes with explanations
- Common use case
- Error handling
- Edge cases
- Comments explaining key concepts
```

### Quiz Questions

Specify question types:
```
Create 3 knowledge check questions about [topic]:
- 1 definition/concept question
- 1 code reading question
- 1 practical application question
Each with detailed explanations in expandable answers
```

### Troubleshooting Sections

Request comprehensive coverage:
```
Create troubleshooting section for [topic] covering:
- Common syntax errors and fixes
- Accessibility issues and solutions
- Browser compatibility problems
- Performance considerations
- Debugging tips
```

## ✅ Quality Assurance Prompts

### Pre-Completion Checklist

Request verification:
```
Before finalizing session-XX, verify:
- [ ] All learning objectives are addressed
- [ ] Time estimates total 80-90 minutes
- [ ] All code examples are complete and tested
- [ ] Quiz questions have expandable answers
- [ ] Accessibility features demonstrated throughout
- [ ] README accurately lists all files
- [ ] External resources are relevant and accessible
- [ ] Homework challenge extends learning appropriately
```

### Consistency Check

Compare with existing sessions:
```
Review session-XX against sessions 04-06 to ensure:
- Similar structure and organization
- Consistent heading hierarchy
- Matching file naming conventions
- Comparable depth and complexity
- Similar quiz format and quantity
- Consistent emoji usage for visual organization
```

## 🔄 Common Request Patterns

### Transforming Instructor-Led to Self-Guided

```
Transform session-XX.md from instructor-led to self-guided:
- Expand brief notes into complete explanations
- Add step-by-step instructions for all activities
- Include code examples for all concepts
- Create practice exercises with solutions
- Add knowledge check quizzes
- Include troubleshooting guidance
- Create all supporting files (template, solution, cheat sheet, visual guide)
```

### Creating Data Files

```
Create [data-file] for session-XX:
- [Specifications: columns, rows, data type]
- Realistic data relevant to [context]
- Format: [CSV/JSON/etc.]
- [X] rows of data
- Include headers
- Use for [specific exercise]
```

### Visual Guide Creation

```
Create [topic]-anatomy-visual.html showing:
- [X] example elements with color coding
- Legend with color meanings
- Visual connections between related elements
- Hover states for interactivity
- Explanatory text for each component
- Self-contained with inline CSS
- Color scheme: [specify colors for concepts]
```

## 🐛 Handling Issues

### When Output Doesn't Match Expectations

**Clarify requirements:**
```
The [file] created doesn't include [expected feature].
Please update it to:
- Add [specific feature]
- Follow the pattern shown in [reference file]
- Ensure [specific requirement]
```

### When Code Has Errors

**Request fixes with context:**
```
The code in [file] has [specific error].
The [element/attribute] should [correct behavior].
Please fix and ensure:
- [Validation requirement]
- [Accessibility requirement]
- [Best practice requirement]
```

### When Structure Doesn't Match

**Reference the standard:**
```
The structure of [file] doesn't match session-instructions.md.
Please reorganize to:
- Follow the [section] structure exactly
- Include all required subsections
- Match heading hierarchy
- Use consistent formatting
```

## 📚 Reference Materials to Mention

When creating sessions, mention relevant standards:

**For HTML:**
```
Use MDN HTML reference for [topic]
Follow W3C HTML5 specifications
Include WAI-ARIA authoring practices
Reference WebAIM guidelines for accessibility
```

**For CSS:**
```
Reference MDN CSS documentation
Follow CSS specifications from W3C
Include browser compatibility notes
Show fallbacks for newer features
```

**For Accessibility:**
```
Follow WCAG 2.1 Level AA guidelines
Reference WAI tutorials
Include ARIA Authoring Practices Guide patterns
Test with screen reader examples
```

## 🎯 Session-Specific Prompts

### For HTML Topics

```
Create session on [HTML topic] including:
- Semantic HTML elements
- Accessibility considerations
- ARIA attributes where needed
- Browser compatibility notes
- Common use cases
- Anti-patterns to avoid
```

### For CSS Topics

```
Create session on [CSS topic] including:
- Syntax and property reference
- Visual examples showing effect
- Browser support information
- Common patterns and techniques
- Responsive considerations
- Performance implications
```

### For JavaScript Topics

```
Create session on [JS topic] including:
- ES6+ syntax
- Practical examples
- Browser API usage
- Error handling
- Debugging techniques
- Performance considerations
```

## 💼 Working Session Example

**Full session creation workflow:**

1. **Initial request:**
   ```
   I need to create session-07 on CSS Box Model for week-03.
   Students have completed HTML fundamentals (weeks 01-02).
   Duration: 90 minutes
   Topics: content, padding, border, margin, box-sizing
   Create self-guided tutorial with all supporting files.
   ```

2. **After tutorial creation:**
   ```
   Great! Now create the cheat sheet with:
   - Box model diagram
   - All box-sizing values
   - Margin/padding shorthand reference
   - Common spacing patterns
   - Debugging tips for layout issues
   ```

3. **For practice files:**
   ```
   Create template and solution for a card layout exercise:
   - 3 cards in a row
   - Equal spacing between cards
   - Padding inside cards
   - Border around each card
   - Demonstrate box-sizing: border-box
   Template: structural HTML with TODOs
   Solution: complete implementation
   ```

4. **For visual guide:**
   ```
   Create visual guide showing:
   - Content box vs border-box comparison
   - Color-coded layers (content, padding, border, margin)
   - Interactive hover to highlight each layer
   - Code examples for each box-sizing value
   ```

5. **Final update:**
   ```
   Update week-03/README.md to include session-07
   with all files, learning path, and help section.
   ```

---

## 🎓 Learning from Examples

When creating new sessions, reference completed sessions:

**"Create session-XX following the same pattern as session-04"**
- Copies successful structure
- Maintains consistency
- Learns from proven format

**"Use the quiz format from session-05"**
- Reuses effective patterns
- Ensures consistency
- Saves specification time

**"Follow the visual guide style from session-06"**
- Maintains visual consistency
- Reuses color schemes
- Applies successful interaction patterns

---

**Remember:** The more specific and contextual your requests, the better Copilot can assist in creating high-quality, consistent educational materials.
