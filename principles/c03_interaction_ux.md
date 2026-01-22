# Interaction & Chinese UX Polish

## Overview

Chinese B-End users have unique expectations shaped by:

* **WeChat/Alipay** (mobile-first, instant feedback)
* **Taobao/JD.com** (high information density on small screens)
* **Government systems** (formal tone, explicit confirmations)

This document covers interaction patterns and typography optimizations for Simplified Chinese interfaces.

---

## 1. Chinese Typography (微排版)

### Font Stack

 **Principle** : Use Western fonts for numbers/English, Chinese fonts for Chinese text.

**Recommended Stack:**

```css
font-family:
  Inter,                    /* Numbers, English UI */
  -apple-system,            /* macOS San Francisco */
  BlinkMacSystemFont,       /* Chrome on macOS */
  "Segoe UI",               /* Windows */
  "PingFang SC",            /* macOS Chinese (Simplified) */
  "Microsoft YaHei",        /* Windows Chinese */
  "Helvetica Neue",         /* Fallback */
  Arial,
  sans-serif;
```

**Tailwind Config:**

```javascript
// tailwind.config.js
fontFamily: {
  sans: ['Inter', 'PingFang SC', 'Microsoft YaHei', 'sans-serif'],
  mono: ['JetBrains Mono', 'Menlo', 'monospace'],
}
```

### Italics Are Forbidden

 **Rule** : NEVER use italic for Chinese text.

 **Reason** : Italic rendering is broken for CJK fonts (斜体字体显示异常).

**Alternative:**

* Use color to emphasize: `text-blue-600`
* Use background to highlight: `bg-yellow-50`
* Use bold sparingly: `font-semibold`

### Line Height for Mixed Content

Chinese characters are denser than Latin letters. Adjust `line-height` based on content type:

| Content Type                  | Line Height | Tailwind Class                    | Reason                     |
| ----------------------------- | ----------- | --------------------------------- | -------------------------- |
| Pure Chinese Text (≥3 lines) | 1.75-2      | `leading-7`or `leading-loose` | Prevent crowding           |
| Mixed Chinese + Numbers       | 1.5         | `leading-6`                     | Standard balance           |
| Short Labels (<10 chars)      | 1.25        | `leading-tight`                 | Compact for UI labels      |
| Code/Monospace                | 1.6         | `leading-relaxed`               | Readability in code blocks |

### Alignment Rules

| Content Type      | Alignment | Tailwind Class              | Reason                  |
| ----------------- | --------- | --------------------------- | ----------------------- |
| Chinese Text      | Left      | `text-left`               | Natural reading flow    |
| Numbers (in text) | Left      | `text-left tabular-nums`  | Consistency with text   |
| Numbers in Tables | Right     | `text-right tabular-nums` | Critical for comparison |
| Currency          | Right     | `text-right tabular-nums` | Financial standards     |
| Badges/Status     | Center    | `text-center`             | Visual balance          |
| Timestamps        | Left      | `text-left`               | Part of description     |

**Example: Table Number Alignment**

```html
<table>
  <tr>
    <td class="text-left">Product Name</td>  <!-- Left -->
    <td class="text-right tabular-nums">¥1,234</td>  <!-- Right -->
    <td class="text-center"><span class="badge">Active</span></td>  <!-- Center -->
  </tr>
</table>
```

### Unit Separation (单位分离)

 **Anti-Pattern** : Uniform styling for number and unit

❌ `<span class="text-2xl">1024MB</span>`

 **Best Practice** : Visually separate number from unit

✅

```html
<span class="text-2xl font-semibold tabular-nums">1,024</span>
<span class="text-sm text-gray-400 ml-1">MB</span>
```

**Why?**

* Reduces visual noise
* Numbers are scannable
* Units are contextual (lower priority)

---

## 2. Noise Reduction (降噪设计)

### Progressive Disclosure

 **Principle** : Don't show everything at once. Hide L3/L4 details until needed.

**Rule: Truncate Long Text**

* If text > 2 lines → Truncate with `truncate` + Tooltip on hover
* If list > 5 items → Show top 3 + "View All (12)" button

**Example: Long Description**

```html
<p class="text-sm text-gray-600 line-clamp-2" title="Full text on hover">
  This is a very long description that may span multiple lines and should be truncated...
</p>
```

**Tailwind Plugin Required:**

```javascript
// Install @tailwindcss/line-clamp
// Or use CSS: display: -webkit-box; -webkit-line-clamp: 2;
```

### Rule: Collapse Sections

* Use `<details>` for optional information
* Use accordions for long forms

**Example: Collapsible Section**

```html
<details class="border border-gray-200 rounded p-3">
  <summary class="cursor-pointer font-medium text-gray-700">
    Advanced Settings (Optional)
  </summary>
  <div class="mt-3 text-sm text-gray-600">
    <!-- Hidden content -->
  </div>
</details>
```

### Visual Hierarchy: 3 Levels Maximum

* **Level 1 (Primary)** : High contrast, large text, bold
* **Level 2 (Secondary)** : Medium contrast, normal text
* **Level 3 (Tertiary)** : Low contrast, small text

 **Beyond L3** : Hide in tooltips, popovers, or separate pages.

**Example: Card with 3 Levels**

```html
<div class="card">
  <!-- L1: Key Metric -->
  <div class="text-2xl font-semibold text-gray-900">¥1,234,567</div>

  <!-- L2: Label -->
  <div class="text-sm text-gray-600">Total Revenue</div>

  <!-- L3: Helper Text -->
  <div class="text-xs text-gray-400">Last updated 5 min ago</div>
</div>
```

### Conditional Display

 **Rule** : If a field is empty/null, don't show "N/A" or "—". Hide the entire row.

**Anti-Pattern:**

❌ `<dt>Phone</dt><dd>N/A</dd>`
❌ `<dt>Address</dt><dd>—</dd>`

**Best Practice:**

✅

```javascript
<!-- Only render if data exists -->
{phone && <><dt>Phone</dt><dd>{phone}</dd></>}
```

---

## 3. Operation Affordance (操作可供性)

### Hover Feedback

 **Rule** : ALL interactive elements MUST have hover states.

| Element              | Hover Style       | Tailwind Classes                                      |
| -------------------- | ----------------- | ----------------------------------------------------- |
| Card/Row (clickable) | Light background  | `hover:bg-gray-50 transition-colors cursor-pointer` |
| Button (primary)     | Darker background | `hover:bg-blue-700`                                 |
| Button (secondary)   | Light background  | `hover:bg-gray-50`                                  |
| Link                 | Underline         | `hover:underline`                                   |
| Icon Button          | Background circle | `hover:bg-gray-100 rounded-full`                    |

**Example: Interactive Table Row**

```html
<tr class="hover:bg-gray-50 transition-colors cursor-pointer">
  <td>Order #12345</td>
  <td>Pending</td>
</tr>
```

### Action Button Hierarchy

 **Rule** : One page = One primary action.

| Priority              | Visual Style                    | Use Case                                                  |
| --------------------- | ------------------------------- | --------------------------------------------------------- |
| **Primary**     | Solid blue/black, high contrast | `bg-blue-600 text-white hover:bg-blue-700`              |
| **Secondary**   | Outline, neutral                | `border border-gray-300 text-gray-700 hover:bg-gray-50` |
| **Tertiary**    | Text link, blue                 | `text-blue-600 hover:underline`                         |
| **Destructive** | Red text (NOT red button)       | `text-red-600 hover:text-red-700`                       |

 **Anti-Pattern** : Red buttons for destructive actions (too aggressive).

 **Best Practice** : Use text links until confirmation modal:

```html
<!-- In list view -->
<button class="text-red-600 hover:text-red-700">Delete</button>

<!-- In confirmation modal -->
<button class="bg-red-600 text-white hover:bg-red-700">Confirm Delete</button>
```

### Loading States

 **Rule** : All async operations MUST show loading feedback.

| Operation     | Feedback                  | Implementation                        |
| ------------- | ------------------------- | ------------------------------------- |
| Button click  | Button disabled + spinner | `disabled:opacity-50`+ spinner icon |
| Data fetch    | Skeleton screen           | Gray boxes with `animate-pulse`     |
| Inline update | Spinner next to content   | Small spinner icon                    |
| Page load     | Full-page loader          | Center-aligned spinner                |

**Example: Button Loading State**

```html
<button class="btn-primary disabled:opacity-50 disabled:cursor-not-allowed" disabled>
  <svg class="animate-spin h-4 w-4 mr-2" ... >...</svg>
  Processing...
</button>
```

---

## 4. Empty States (情感化空状态)

### Positive Reinforcement

 **Rule** : When "no data" is a GOOD thing (e.g., "No Risks"), show positive feedback.

 **Anti-Pattern** : Blank space or "No data"

**Best Practice:**

```html
<div class="flex flex-col items-center justify-center py-8">
  <svg class="h-12 w-12 text-green-500" ...><!-- Check icon --></svg>
  <p class="mt-3 text-sm font-medium text-gray-900">Everything Looks Good</p>
  <p class="mt-1 text-xs text-gray-500">No risks detected in the past 7 days</p>
</div>
```

### Actionable Empty States

 **Rule** : If "no data" requires user action, provide a CTA.

**Example: No Orders**

```html
<div class="flex flex-col items-center justify-center py-12">
  <svg class="h-16 w-16 text-gray-300" ...><!-- Empty box icon --></svg>
  <p class="mt-4 text-base font-medium text-gray-900">No Orders Yet</p>
  <p class="mt-1 text-sm text-gray-500">Create your first order to get started</p>
  <button class="mt-4 btn-primary">Create Order</button>
</div>
```

---

## 5. Form Interaction

### Input Focus States

 **Rule** : Focused inputs MUST have visual feedback.

**Tailwind Classes:**

```
focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none
```

**Example:**

```html
<input
  type="text"
  class="w-full px-3 py-2 border border-gray-300 rounded
         focus:ring-2 focus:ring-blue-500 focus:border-blue-500
         outline-none transition"
>
```

### Validation Feedback

 **Rule** : Show validation errors AFTER blur (not on every keystroke).

**States:**

* **Default** : `border-gray-300`
* **Focus** : `border-blue-500 ring-2 ring-blue-500`
* **Error** : `border-red-500 ring-2 ring-red-500`
* **Success** : `border-green-500 ring-2 ring-green-500`

**Example: Error State**

```html
<div>
  <input
    type="email"
    class="w-full px-3 py-2 border border-red-500 rounded
           focus:ring-2 focus:ring-red-500"
  >
  <p class="mt-1 text-sm text-red-600">Please enter a valid email</p>
</div>
```

### Required Field Indicators

 **Rule** : Use `*` for required fields, placed AFTER the label.

**Example:**

```html
<label class="text-sm font-medium text-gray-700">
  Email <span class="text-red-500">*</span>
</label>
```

---

## 6. Responsive Interaction

### Touch Target Size (Mobile/Tablet)

 **Rule** : Minimum touch target = 44×44px (Apple HIG) or 48×48px (Material Design).

Desktop: 32×32px is acceptable for mouse-only interfaces.

**Tailwind Helper:**

```
min-h-[44px] min-w-[44px]  /* Mobile */
min-h-[32px] min-w-[32px]  /* Desktop */
```

### Keyboard Navigation

 **Rule** : All interactive elements MUST be keyboard-accessible.

**Checklist:**

* [ ] Use `<button>` and `<a>` (not `<div onclick>`)
* [ ] Maintain logical tab order
* [ ] Visible focus states (`:focus ring`)
* [ ] Support Enter/Space for activation
* [ ] Support Escape for closing modals

**Example: Accessible Button**

```html
<button
  class="btn focus:ring-2 focus:ring-blue-500 focus:outline-none"
  aria-label="Close dialog"
>
  Close
</button>
```

---

## 7. Micro-Interactions

### Transition Timing

Use consistent timing for all transitions:

| Animation Type    | Duration | Easing      | Tailwind Class                    |
| ----------------- | -------- | ----------- | --------------------------------- |
| Color change      | 150ms    | ease-out    | `transition-colors`             |
| Opacity           | 200ms    | ease-in-out | `transition-opacity`            |
| Transform (scale) | 150ms    | ease-out    | `transition-transform`          |
| Layout (height)   | 300ms    | ease-in-out | `transition-all`(use sparingly) |

**Example: Hover Color Transition**

```html
<button class="bg-blue-600 hover:bg-blue-700 transition-colors duration-150">
  Click Me
</button>
```

### Success Feedback

 **Rule** : After successful actions (save, delete, create), show feedback for 2-3 seconds.

**Options:**

* Toast/Snackbar (top-right corner)
* Inline message (above affected area)
* Temporary badge (next to button)

**Example: Toast**

```html
<div class="fixed top-4 right-4 bg-green-50 border border-green-200 rounded-lg p-4 shadow-lg">
  <div class="flex items-center">
    <svg class="h-5 w-5 text-green-500"><!-- Check icon --></svg>
    <p class="ml-3 text-sm font-medium text-green-800">Order created successfully</p>
  </div>
</div>
```

---

## Decision Checklist

When designing interactions, ask:

* [ ] Are all hover states defined?
* [ ] Is there visual feedback for loading states?
* [ ] Are empty states informative (not just "No data")?
* [ ] Are long texts truncated with progressive disclosure?
* [ ] Do numbers in tables align right?
* [ ] Are units visually separated from numbers?
* [ ] Is Chinese text using correct line-height (1.75+)?
* [ ] Are focus states visible for keyboard navigation?
* [ ] Are touch targets ≥44px for mobile?
* [ ] Are all interactive elements using semantic HTML (`<button>`, `<a>`)?

---

## Reference

* **Chinese Typography** : Ant Design Typography
* **Interaction Patterns** : Arco Design Interaction
* **Accessibility** : WCAG 2.1 Guidelines
