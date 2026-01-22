# Chinese B-End Layout Principles

## Overview

Chinese enterprise users have distinct preferences compared to Western SaaS products:

* **Higher information density** (more data per screen)
* **Faster scanning patterns** (F-shaped eye tracking)
* **Function-first aesthetics** (clarity over visual polish)

These principles are derived from industry leaders like Ant Design (Alibaba), Arco Design (ByteDance), and TDesign (Tencent).

---

## 1. High Density & Screen Efficiency (高屏效)

### Core Concept

**屏效比 (Screen Efficiency Ratio) = Useful Information / Screen Area**

Chinese B-End users prioritize seeing more actionable data without scrolling. Excessive whitespace is perceived as "wasted space."

### Grid System

* **Standard** : 12-column grid for responsive layouts
* **Dense Layouts** : 24-column grid for complex dashboards
* **Gutter** : `gap-4` (16px) between columns

### Spacing Guidelines

| Element      | Spacing | Tailwind Class | Use Case                               |
| ------------ | ------- | -------------- | -------------------------------------- |
| Card Padding | 16px    | `p-4`        | Standard density                       |
| Compact Card | 12px    | `p-3`        | High-density dashboards                |
| Loose Card   | 24px    | `p-6`        | Marketing pages (rarely used in B-End) |
| Section Gap  | 16px    | `gap-4`      | Between cards                          |
| Inner Gap    | 12px    | `gap-3`      | Inside card sections                   |

### Anti-Pattern

* ❌ Large hero sections with single CTAs (这是 C 端思维)
* ❌ Full-screen empty states with illustrations
* ❌ Excessive padding (>24px) unless for visual separation

---

## 2. The "F-Pattern" & "Golden Triangle" (视觉动线)

### F-Pattern Scanning

Users scan content in an F-shaped pattern:

1. Horizontal scan along the top (header/title)
2. Vertical scan down the left side (labels/categories)
3. Horizontal scan midway through content

**Layout Implication:**

* **Top-Left Corner** : Most critical information (page title, primary status)
* **Top Row** : Summary metrics (KPI cards)
* **Left Column** : Navigation or category filters
* **Center/Right** : Detailed content (tables, charts)

### Golden Triangle

The top-left 1/4 of the screen forms a "golden triangle" where users' eyes land first.

**Placement Strategy:**

```
┌─────────────────────────────────┐
│ [Golden Triangle]               │  ← Place:
│  - Page Title                   │     - Critical alerts
│  - Primary Status Badge         │     - Key action buttons
│  - Core Metric (Big Number)     │     - Primary KPI
├─────────────────────────────────┤
│ [Supporting Content]            │  ← Place:
│  - Data tables                  │     - Detailed lists
│  - Secondary charts             │     - Historical logs
└─────────────────────────────────┘
```

---

## 3. Container Strategy (Bento Box Metaphor)

### Card-Based Architecture

All content MUST live inside visual containers (cards) to create clear boundaries.

**Base Card Style:**

```
bg-white shadow-sm border border-gray-100 rounded-lg
```

### Internal Partitioning

Use subtle backgrounds to separate sections within a single card:

```html
<!-- Example: Card with 2 sections -->
<div class="bg-white border border-gray-100 rounded-lg p-4">
  <!-- Section 1: Current Status -->
  <div class="bg-gray-50 p-3 rounded mb-3">
    <h3>Current Status</h3>
    <p>Active</p>
  </div>

  <!-- Section 2: History -->
  <div>
    <h3>Recent Changes</h3>
    <ul>...</ul>
  </div>
</div>
```

### When to Split into Multiple Cards

* Different business objects (e.g., "Order Info"vs "Customer Info")
* Different time contexts (e.g., "Today's Stats" vs "This Month")
* Different user goals (e.g., "Monitor" vs "Configure")

---

## 4. Responsive Logic (Adaptability)

### Breakpoint Philosophy

B-End interfaces are  **desktop-first** . Mobile responsiveness is secondary.

**Minimum Viable Width: 1024px**

Below this, allow horizontal scrolling for tables rather than breaking layouts.

### Sidebar-Aware Layouts

Assumption: A left sidebar (200-250px) exists in most B-End apps.

**Content Area Width Calculation:**

```
Available Width = Viewport Width - Sidebar Width - Padding
```

**Responsive Card Grid:**

* ≥1920px: 4 columns (`grid-cols-4`)
* 1440-1919px: 3 columns (`grid-cols-3`)
* 1024-1439px: 2 columns (`grid-cols-2`)
* <1024px: Single column + horizontal scroll for tables

---

## 5. Vertical Rhythm & Hierarchy

### Content Blocks

Organize content into distinct "swim lanes":

1. **Header Zone (Sticky)** : Page title + breadcrumbs + primary actions
2. **Summary Zone** : KPI cards in a horizontal row
3. **Detail Zone** : Tables, charts, logs (scrollable)
4. **Footer Zone (Optional)** : Pagination or bulk actions

### Hierarchy Through Contrast

Use size + weight + color to create levels:

| Level              | Style                                    | Example                    |
| ------------------ | ---------------------------------------- | -------------------------- |
| L1 (Page Title)    | `text-2xl font-semibold text-gray-900` | "Order Management"         |
| L2 (Section Title) | `text-lg font-medium text-gray-800`    | "Recent Orders"            |
| L3 (Card Title)    | `text-base font-medium text-gray-700`  | "Order #12345"             |
| L4 (Label)         | `text-sm text-gray-500`                | "Status:"                  |
| L5 (Helper)        | `text-xs text-gray-400`                | "Last updated 2 hours ago" |

---

## 6. Common Layout Patterns

### Pattern A: Dashboard Overview

```
┌────────────────────────────────────────┐
│ [Header: Title + Date Picker]         │
├────────────────────────────────────────┤
│ [KPI Row: 4 Cards in grid-cols-4]     │
├────────────────────────────────────────┤
│ [Charts: 2 Charts in grid-cols-2]     │
├────────────────────────────────────────┤
│ [Table: Recent Activity]               │
└────────────────────────────────────────┘
```

### Pattern B: Detail Page

```
┌────────────────────────────────────────┐
│ [Breadcrumb + Title + Actions]        │
├─────────────────┬──────────────────────┤
│ [Left: Core]    │ [Right: Timeline]    │
│ - Status        │ - Change History     │
│ - Key Attrs     │ - Comments           │
└─────────────────┴──────────────────────┘
```

### Pattern C: List/Table Page

```
┌────────────────────────────────────────┐
│ [Search Bar + Filters]                 │
├────────────────────────────────────────┤
│ [Stats: 3 Metric Cards]                │
├────────────────────────────────────────┤
│ [Data Table with Row Actions]         │
├────────────────────────────────────────┤
│ [Pagination]                           │
└────────────────────────────────────────┘
```

---

## Decision Checklist

When designing a B-End layout, ask:

* [ ] Does the layout prioritize actionable information over aesthetics?
* [ ] Can users find the most critical data in the top-left quadrant?
* [ ] Are cards used to create clear boundaries between business objects?
* [ ] Is the information density appropriate? (Not too sparse, not cluttered)
* [ ] Does the design accommodate a left sidebar?
* [ ] Are tables allowed to scroll horizontally on smaller screens?

---

## Reference Examples

* **Ant Design Pro** : [https://preview.pro.ant.design/](https://preview.pro.ant.design/)
* **Arco Design Pro** : [https://pro.arco.design/](https://pro.arco.design/)
* **TDesign Starter** : [https://tdesign.tencent.com/starter/](https://tdesign.tencent.com/starter/)

Study how these systems balance density, clarity, and hierarchy.
