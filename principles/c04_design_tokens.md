# Design Tokens (Tailwind Preset)

## Overview

This document defines the **Design Tokens** (design variables) for Chinese B-End interfaces using Tailwind CSS utilities.

These tokens are aligned with:

* **Ant Design** color system
* **Arco Design** spacing scale
* **TDesign** shadow specifications

---

## 1. Color System

### Functional Colors (Business Logic)

| Token Name              | Tailwind Class | Hex Value   | Use Case                             |
| ----------------------- | -------------- | ----------- | ------------------------------------ |
| **primary**       | `blue-600`   | `#2563eb` | Primary actions, links, focus states |
| **primary-hover** | `blue-700`   | `#1d4ed8` | Hover state for primary actions      |
| **primary-light** | `blue-50`    | `#eff6ff` | Light background for info sections   |
| **success**       | `green-600`  | `#16a34a` | Success states, positive metrics     |
| **success-bg**    | `green-50`   | `#f0fdf4` | Success alert backgrounds            |
| **warning**       | `orange-600` | `#ea580c` | Warning states, attention needed     |
| **warning-bg**    | `orange-50`  | `#fff7ed` | Warning alert backgrounds            |
| **critical**      | `red-600`    | `#dc2626` | Error states, critical alerts        |
| **critical-bg**   | `red-50`     | `#fef2f2` | Error alert backgrounds              |
| **processing**    | `blue-500`   | `#3b82f6` | Loading, in-progress states          |
| **disabled**      | `gray-300`   | `#d1d5db` | Disabled elements                    |

### Neutral Colors (UI Structure)

| Token Name              | Tailwind Class | Hex Value   | Use Case              |
| ----------------------- | -------------- | ----------- | --------------------- |
| **surface**       | `white`      | `#ffffff` | Card backgrounds      |
| **background**    | `gray-50`    | `#f9fafb` | App canvas background |
| **divider**       | `gray-100`   | `#f3f4f6` | Subtle separators     |
| **border**        | `gray-200`   | `#e5e7eb` | Standard borders      |
| **border-strong** | `gray-300`   | `#d1d5db` | Emphasized borders    |

### Text Colors

| Token Name                 | Tailwind Class | Hex Value   | Use Case                     | WCAG AA                  |
| -------------------------- | -------------- | ----------- | ---------------------------- | ------------------------ |
| **text-primary**     | `gray-900`   | `#111827` | Headings, key content        | ✅                       |
| **text-secondary**   | `gray-600`   | `#4b5563` | Body text, descriptions      | ✅                       |
| **text-tertiary**    | `gray-500`   | `#6b7280` | Labels, helper text          | ⚠️ Use for ≥14px only |
| **text-placeholder** | `gray-400`   | `#9ca3af` | Input placeholders, inactive | ⚠️ Large text only     |
| **text-disabled**    | `gray-300`   | `#d1d5db` | Disabled text                | ❌ Use with care         |

---

## 2. Spacing System (4px Grid)

### Spacing Scale

All spacing follows a  **4px base unit** :

| Token         | Tailwind Class | Pixels | Use Case                             |
| ------------- | -------------- | ------ | ------------------------------------ |
| **xs**  | `1`          | 4px    | Icon padding, tight inline spacing   |
| **sm**  | `2`          | 8px    | Button icon-to-text gap              |
| **md**  | `4`          | 16px   | Card internal padding (standard)     |
| **lg**  | `6`          | 24px   | Between cards                        |
| **xl**  | `8`          | 32px   | Section spacing                      |
| **2xl** | `12`         | 48px   | Major section breaks (rare in B-End) |

### Common Spacing Patterns

| Context                 | Property   | Tailwind Class | Pixels | Note                    |
| ----------------------- | ---------- | -------------- | ------ | ----------------------- |
| Card padding (standard) | padding    | `p-4`        | 16px   | Most common             |
| Card padding (compact)  | padding    | `p-3`        | 12px   | High-density dashboards |
| Gap between cards       | gap        | `gap-4`      | 16px   | Grid layouts            |
| Label to value          | gap        | `gap-1`      | 4px    | DescriptionList         |
| Button icon to text     | gap        | `gap-2`      | 8px    | Icon buttons            |
| Form field spacing      | gap        | `gap-4`      | 16px   | Vertical form fields    |
| Section divider         | margin-top | `mt-6`       | 24px   | Between major sections  |

---

## 3. Typography Scale

### Font Sizes

| Token          | Tailwind Class | px / rem        | Line Height  | Use Case                                |
| -------------- | -------------- | --------------- | ------------ | --------------------------------------- |
| **xs**   | `text-xs`    | 12px / 0.75rem  | 16px (1.333) | Captions, helper text, units            |
| **sm**   | `text-sm`    | 14px / 0.875rem | 20px (1.429) | Body text, table cells, labels          |
| **base** | `text-base`  | 16px / 1rem     | 24px (1.5)   | Standard UI text (rarely used in B-End) |
| **lg**   | `text-lg`    | 18px / 1.125rem | 28px (1.556) | Card titles, section headers            |
| **xl**   | `text-xl`    | 20px / 1.25rem  | 28px (1.4)   | Page subtitles                          |
| **2xl**  | `text-2xl`   | 24px / 1.5rem   | 32px (1.333) | Key metrics, page titles                |
| **3xl**  | `text-3xl`   | 30px / 1.875rem | 36px (1.2)   | Hero metrics (rare)                     |

### Font Weights

| Token              | Tailwind Class    | Weight | Use Case                                  |
| ------------------ | ----------------- | ------ | ----------------------------------------- |
| **normal**   | `font-normal`   | 400    | Body text, descriptions                   |
| **medium**   | `font-medium`   | 500    | Labels, values in DescriptionList         |
| **semibold** | `font-semibold` | 600    | Headings, key metrics                     |
| **bold**     | `font-bold`     | 700    | Rarely used (too heavy for Chinese fonts) |

 **Note** : Avoid `font-bold` for Chinese text (中文粗体过重).

### Line Heights (for Chinese Text)

| Token             | Tailwind Class    | Value | Use Case                            |
| ----------------- | ----------------- | ----- | ----------------------------------- |
| **tight**   | `leading-tight` | 1.25  | Short labels (<10 chars)            |
| **normal**  | `leading-6`     | 1.5   | Mixed content (numbers + Chinese)   |
| **relaxed** | `leading-7`     | 1.75  | Pure Chinese paragraphs (≥3 lines) |
| **loose**   | `leading-loose` | 2     | Emphasis on readability (rare)      |

---

## 4. Shadows & Elevation

### Shadow Scale

Chinese B-End design prefers **subtle shadows** (not dramatic depth).

| Level             | Tailwind Class  | CSS Shadow                           | Use Case                    |
| ----------------- | --------------- | ------------------------------------ | --------------------------- |
| **none**    | `shadow-none` | `none`                             | Flat cards in dense layouts |
| **card**    | `shadow-sm`   | `0 1px 2px 0 rgba(0,0,0,0.05)`     | Standard card elevation     |
| **hover**   | `shadow`      | `0 1px 3px 0 rgba(0,0,0,0.1)`      | Card hover state            |
| **modal**   | `shadow-lg`   | `0 10px 15px -3px rgba(0,0,0,0.1)` | Modals, dropdowns           |
| **tooltip** | `shadow-md`   | `0 4px 6px -1px rgba(0,0,0,0.1)`   | Tooltips, popovers          |

 **Anti-Pattern** : Using `shadow-2xl` (too heavy for B-End).

---

## 5. Border Radius

### Radius Scale

| Token          | Tailwind Class   | Pixels | Use Case                        |
| -------------- | ---------------- | ------ | ------------------------------- |
| **none** | `rounded-none` | 0px    | Tables, strict layouts          |
| **sm**   | `rounded-sm`   | 2px    | Badges, tags (minimal rounding) |
| **base** | `rounded`      | 4px    | Standard buttons, inputs        |
| **md**   | `rounded-md`   | 6px    | Cards (rarely used)             |
| **lg**   | `rounded-lg`   | 8px    | Cards, modals (most common)     |
| **full** | `rounded-full` | 9999px | Circular badges, avatars        |

 **Standard Choice** : Use `rounded-lg` (8px) for cards, `rounded` (4px) for buttons/inputs.

---

## 6. Opacity & States

### Opacity Levels

| State                    | Tailwind Class     | Opacity | Use Case                 |
| ------------------------ | ------------------ | ------- | ------------------------ |
| **Disabled**       | `opacity-50`     | 50%     | Disabled buttons, inputs |
| **Loading**        | `opacity-70`     | 70%     | Content behind spinners  |
| **Hover overlay**  | `bg-gray-900/10` | 10%     | Dark overlay on hover    |
| **Modal backdrop** | `bg-black/50`    | 50%     | Modal background dimming |

---

## 7. Transitions

### Timing Functions

| Context                  | Tailwind Class                        | Duration | Easing      | Use Case                         |
| ------------------------ | ------------------------------------- | -------- | ----------- | -------------------------------- |
| **Color change**   | `transition-colors duration-150`    | 150ms    | ease-out    | Button hover, status change      |
| **Opacity**        | `transition-opacity duration-200`   | 200ms    | ease-in-out | Fade in/out                      |
| **Transform**      | `transition-transform duration-150` | 150ms    | ease-out    | Scale, translate                 |
| **All properties** | `transition-all duration-300`       | 300ms    | ease-in-out | ⚠️ Use sparingly (performance) |

 **Standard Choice** : `transition-colors` for most UI interactions.

---

## 8. Z-Index Layers

### Stacking Order

| Layer                   | Z-Index Value | Use Case                |
| ----------------------- | ------------- | ----------------------- |
| **Base**          | 0             | Default content         |
| **Dropdown**      | 10            | Select menus, dropdowns |
| **Sticky Header** | 20            | Fixed headers           |
| **Overlay**       | 30            | Modal backdrops         |
| **Modal**         | 40            | Modals, dialogs         |
| **Tooltip**       | 50            | Tooltips, popovers      |
| **Notification**  | 60            | Toast notifications     |

 **Tailwind Classes** : `z-10`, `z-20`, `z-30`, `z-40`, `z-50`

---

## 9. Grid & Layout

### Container Widths

| Breakpoint    | Screen Width | Container Max-Width | Tailwind Class       |
| ------------- | ------------ | ------------------- | -------------------- |
| **sm**  | ≥640px      | 640px               | `max-w-screen-sm`  |
| **md**  | ≥768px      | 768px               | `max-w-screen-md`  |
| **lg**  | ≥1024px     | 1024px              | `max-w-screen-lg`  |
| **xl**  | ≥1280px     | 1280px              | `max-w-screen-xl`  |
| **2xl** | ≥1536px     | 1536px              | `max-w-screen-2xl` |

 **B-End Standard** : Design for **xl (1280px)** as the primary breakpoint.

### Grid Columns

| Density                | Grid Columns | Tailwind Class   | Use Case                                    |
| ---------------------- | ------------ | ---------------- | ------------------------------------------- |
| **Standard**     | 12 columns   | `grid-cols-12` | General layouts                             |
| **High Density** | 24 columns   | `grid-cols-24` | Complex dashboards (requires custom config) |

---

## 10. Tailwind Config Preset

**Recommended `tailwind.config.js` for Chinese B-End:**

```javascript
module.exports = {
  theme: {
    extend: {
      colors: {
        primary: {
          DEFAULT: '#2563eb',
          light: '#eff6ff',
          dark: '#1d4ed8',
        },
      },
      fontFamily: {
        sans: ['Inter', 'PingFang SC', 'Microsoft YaHei', 'sans-serif'],
      },
      boxShadow: {
        card: '0 1px 2px 0 rgba(0,0,0,0.05)',
      },
      spacing: {
        // Already defined by default (4px base)
      },
      gridTemplateColumns: {
        '24': 'repeat(24, minmax(0, 1fr))',  // For high-density layouts
      },
    },
  },
  plugins: [
    require('@tailwindcss/forms'),       // Better form styles
    require('@tailwindcss/line-clamp'),  // Multi-line truncation
  ],
}
```

---

## Quick Reference Cheatsheet

### Common Patterns

**Standard Card:**

```
bg-white border border-gray-100 shadow-sm rounded-lg p-4
```

**Compact Card:**

```
bg-white border border-gray-100 rounded-lg p-3
```

**Section Background:**

```
bg-gray-50 border border-gray-200 rounded p-3
```

**Primary Button:**

```
bg-blue-600 text-white hover:bg-blue-700 px-4 py-2 rounded transition-colors
```

**Secondary Button:**

```
border border-gray-300 text-gray-700 hover:bg-gray-50 px-4 py-2 rounded transition-colors
```

**Destructive Link:**

```
text-red-600 hover:text-red-700 hover:underline text-sm
```

**Key Metric:**

```
text-2xl font-semibold text-gray-900 tabular-nums
```

**Label:**

```
text-xs text-gray-500 uppercase tracking-wide
```

**Helper Text:**

```
text-xs text-gray-400
```

---

## Validation Checklist

When using these tokens, verify:

* [ ] Text colors meet WCAG AA contrast ratio (4.5:1 for normal text)
* [ ] Spacing follows 4px grid (no odd values like 13px)
* [ ] Font weights for Chinese text ≤ 600 (semibold)
* [ ] Shadows are subtle (no `shadow-2xl`)
* [ ] Border radius is consistent (cards = 8px, buttons = 4px)
* [ ] Transitions use appropriate duration (150-300ms)

---

## Reference

* **Ant Design Colors** : [https://ant.design/docs/spec/colors](https://ant.design/docs/spec/colors)
* **Tailwind Palette** : [https://tailwindcss.com/docs/customizing-colors](https://tailwindcss.com/docs/customizing-colors)
* **WCAG Contrast Checker** : [https://webaim.org/resources/contrastchecker/](https://webaim.org/resources/contrastchecker/)
