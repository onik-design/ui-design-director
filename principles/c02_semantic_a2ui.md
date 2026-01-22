# Semantic Hints & Usage Mapping (A2UI Core)

## Philosophy: Intent Over Appearance

 **A2UI Principle** : Designers should define **what data means** (semantic intent), not **how it looks** (visual attributes).

Instead of saying:

❌ "Make this text red and 14px"

Say:

✅ "This is a CriticalAlert status"

The design system then maps `CriticalAlert` → `bg-red-50 text-red-700 border-red-100 text-sm`.

---

## 1. Status & Feedback Semantics

### The Traffic Light Logic

Chinese users are conditioned to the "red-yellow-green" mental model from traffic signals, warning labels, and industrial systems.

### Semantic Mapping Table

| Semantic Type        | Meaning                                         | Visual Mapping                                     | Icon                          | Use Case                                                    |
| -------------------- | ----------------------------------------------- | -------------------------------------------------- | ----------------------------- | ----------------------------------------------------------- |
| **Critical**   | Fatal error, blocker, immediate action required | `bg-red-50 text-red-700 border-red-100`          | X-Circle / Alert-Octagon      | "Server Down", "Payment Failed", "Risk Score > 80"          |
| **Warning**    | Risk present, attention needed, non-blocking    | `bg-orange-50 text-orange-700 border-orange-100` | Alert-Triangle                | "Approaching Deadline", "Low Inventory", "Risk Score 50-79" |
| **Success**    | Target met, task completed, positive result     | `bg-green-50 text-green-700 border-green-100`    | Check-Circle / Shield-Check   | "Order Delivered", "Test Passed", "Under Budget"            |
| **Processing** | Active task, in progress, awaiting result       | `bg-blue-50 text-blue-700 border-blue-100`       | Loader (animate-spin) / Clock | "Uploading File", "Processing Payment", "Running Job"       |
| **Info**       | Neutral information, informational notice       | `bg-blue-50 text-blue-600`                       | Info-Circle                   | "System Maintenance Scheduled", "New Feature Available"     |
| **Neutral**    | Inactive, pending, not applicable               | `bg-gray-100 text-gray-500`                      | Minus-Circle / Pause          | "Draft", "Pending Review", "Offline"                        |
| **Disabled**   | Cannot be interacted with                       | `bg-gray-50 text-gray-300 cursor-not-allowed`    | —                            | Inactive buttons, read-only fields                          |

### Contextual Usage

**Example: Order Status**

* **Critical** : "Cancelled", "Payment Failed"
* **Warning** : "Delayed", "Partially Shipped"
* **Success** : "Delivered", "Completed"
* **Processing** : "In Transit", "Processing"
* **Neutral** : "Draft", "Pending Payment"

**Example: Risk Assessment**

* **Critical** : Risk Score 80-100
* **Warning** : Risk Score 50-79
* **Success** : Risk Score 0-29
* **Info** : Risk Score 30-49

---

## 2. Typography Semantics

### Hierarchy Through Intent

Do not think in "font sizes" first. Think in  **information roles** .

| Semantic Type          | Role                                       | Style                                                                | Example                         |
| ---------------------- | ------------------------------------------ | -------------------------------------------------------------------- | ------------------------------- |
| **KeyMetric**    | The most important number on the page/card | `text-2xl font-semibold tracking-tight tabular-nums text-gray-900` | "¥1,234,567" (monthly revenue) |
| **Metric**       | Secondary important number                 | `text-xl font-medium tabular-nums text-gray-800`                   | "87%" (completion rate)         |
| **Label**        | Attribute name, field label                | `text-xs text-gray-500 font-normal uppercase tracking-wide`        | "STATUS:", "CREATED AT:"        |
| **Value**        | Attribute data, field value                | `text-sm text-gray-900 font-medium`                                | "Active", "2024-01-15"          |
| **HelperText**   | Explanation, hint, footnote                | `text-xs text-gray-400`                                            | "Last synced 5 minutes ago"     |
| **Emphasized**   | Important inline text (not a metric)       | `text-sm text-gray-900 font-semibold`                              | User names, critical keywords   |
| **Deemphasized** | Low-priority information                   | `text-xs text-gray-400`                                            | Metadata, timestamps in lists   |

### Number Formatting

Use `tabular-nums` for all numeric data to ensure alignment in tables/lists.

**Unit Separation:**

❌  **Bad** : `<span class="text-2xl">1024MB</span>` (unit same size as number)

✅  **Good** : `<span class="text-2xl font-semibold">1024</span><span class="text-sm text-gray-400 ml-1">MB</span>`

---

## 3. Component Semantics

### When to Use Each Component

| Component                 | Semantic Intent                              | Visual Form                        | When to Use                                           |
| ------------------------- | -------------------------------------------- | ---------------------------------- | ----------------------------------------------------- |
| **Badge**           | Discrete state or category (1-2 words)       | Rounded pill with background color | Enum values: "Active", "Pending", "Critical"          |
| **Tag**             | Multiple categories (can have many)          | Smaller rounded pill, often gray   | Filter tags, skill labels, multi-select categories    |
| **DescriptionList** | Key-value pairs (structured attributes)      | Label + Value in `dl/dt/dd`      | User profile, order details, config settings          |
| **Timeline**        | Sequential events (chronological order)      | Vertical line with timestamps      | Change history, audit logs, status transitions        |
| **Alert**           | Contextual notification (page/section level) | Colored banner with icon           | Error messages, warnings, success confirmations       |
| **Tooltip**         | Supplementary explanation (low priority)     | Hover/focus overlay                | Help text, full timestamps, truncated content         |
| **Popover**         | Interactive details (requires user action)   | Click/hover panel                  | Filters, quick actions, extra info without navigation |

---

## 4. Data Type to Component Mapping

### Enum/Status → Badge

 **Data** : `status = "critical"`

 **Semantic** : `CriticalAlert`

 **Component** : `<Badge variant="critical">Critical</Badge>`

---

### Number/KPI → KeyMetric Typography

 **Data** : `revenue = 1234567`

 **Semantic** : `KeyMetric`

 **Component** :

```html
<div class="text-2xl font-semibold tabular-nums text-gray-900">
  ¥1,234,567
</div>
```

---

### Attributes → DescriptionList

 **Data** : `{ name: "John", email: "john@example.com", role: "Admin" }`

 **Semantic** : `BusinessObjectAttributes`

 **Component** :

```html
<dl>
  <dt class="text-xs text-gray-500 uppercase">Name</dt>
  <dd class="text-sm text-gray-900 font-medium">John</dd>

  <dt class="text-xs text-gray-500 uppercase">Email</dt>
  <dd class="text-sm text-gray-900 font-medium">john@example.com</dd>

  <dt class="text-xs text-gray-500 uppercase">Role</dt>
  <dd class="text-sm text-gray-900 font-medium">Admin</dd>
</dl>
```

---

### Change History → Timeline

 **Data** : `[{ time: "2024-01-15 10:30", action: "Created", user: "Alice" }, ...]`

 **Semantic** : `SequentialEvents`

 **Component** : Vertical timeline with timestamp + icon + description

---

## 5. Interaction Affordance Semantics

### Clickable Elements

| Semantic Type               | Visual Style                                                              | Use Case                                    |
| --------------------------- | ------------------------------------------------------------------------- | ------------------------------------------- |
| **PrimaryAction**     | `bg-blue-600 text-white hover:bg-blue-700`(solid button)                | Main CTA per page: "Submit", "Create Order" |
| **SecondaryAction**   | `border border-gray-300 text-gray-700 hover:bg-gray-50`(outline button) | Alternative actions: "Cancel", "Save Draft" |
| **DestructiveAction** | `text-red-600 hover:text-red-700`(text/link style, NOT red button)      | "Delete", "Remove", "Revoke"                |
| **TertiaryAction**    | `text-blue-600 hover:text-blue-700 hover:underline`(link style)         | Navigation, "View Details", "Learn More"    |

 **Rule** : Only **ONE** PrimaryAction per screen/modal.

### Hover States

Interactive rows/cards MUST have hover feedback:

```
hover:bg-gray-50 transition-colors cursor-pointer
```

Disabled elements MUST indicate non-interactivity:

```
opacity-50 cursor-not-allowed pointer-events-none
```

---

## 6. Layout Semantics

### Container Types

| Semantic Type     | Purpose                     | Style                                                              |
| ----------------- | --------------------------- | ------------------------------------------------------------------ |
| **Surface** | Primary background (canvas) | `bg-gray-50`                                                     |
| **Card**    | Content container           | `bg-white border border-gray-100 shadow-sm rounded-lg`           |
| **Well**    | Nested section within card  | `bg-gray-50 border border-gray-200 rounded p-3`                  |
| **Divider** | Visual separation           | `border-t border-gray-100`(horizontal) or `border-l`(vertical) |

---

## 7. Accessibility Semantics (WCAG AA)

### Color Contrast Requirements

**Normal Text (14-18px):**

* Contrast ratio ≥ 4.5:1
* `text-gray-900` on `bg-white` ✅
* `text-gray-500` on `bg-white` ⚠️ (Use for labels only, not body text)

**Large Text (≥18px or ≥14px bold):**

* Contrast ratio ≥ 3:1
* `text-gray-600` on `bg-white` ✅

**Status Colors:**

* Red: `text-red-700` on `bg-red-50` ✅
* Orange: `text-orange-700` on `bg-orange-50` ✅
* Green: `text-green-700` on `bg-green-50` ✅

### Semantic HTML

Always use proper HTML5 semantics:

* Use `<button>` for actions (not `<div onclick>`)
* Use `<a>` for navigation (with `href`)
* Use `<dl>`, `<dt>`, `<dd>` for key-value pairs
* Use `<table>` for tabular data (not CSS grids mimicking tables)

---

## 8. Decision Workflow

When analyzing a data field, follow this process:

1. **Identify Intent** : What does this data represent? (Status? Metric? Attribute? Event?)
2. **Classify Semantic Type** : Map to one of the types above (CriticalAlert, KeyMetric, etc.)
3. **Select Component** : Choose the appropriate component based on semantic type
4. **Apply Visual Mapping** : Use predefined Tailwind classes from the semantic type definition
5. **Verify Accessibility** : Ensure contrast ratios and semantic HTML are correct

---

## Quick Reference Cheatsheet

```
Critical Alert     → bg-red-50 text-red-700 border-red-100
Warning           → bg-orange-50 text-orange-700 border-orange-100
Success           → bg-green-50 text-green-700 border-green-100
Processing        → bg-blue-50 text-blue-700 border-blue-100
Neutral/Disabled  → bg-gray-100 text-gray-500

KeyMetric         → text-2xl font-semibold tabular-nums
Label             → text-xs text-gray-500 uppercase
Value             → text-sm text-gray-900 font-medium

Enum/Status       → Badge (rounded pill)
Attributes        → DescriptionList (dl/dt/dd)
History           → Timeline (vertical)
Action (Primary)  → Solid Blue Button
Action (Destroy)  → Red Text Link
```

---

## Common Anti-Patterns

* ❌ Using color alone to convey status (missing icons/labels)
* ❌ Mixing visual styles for the same semantic type (inconsistent badge colors)
* ❌ Using `<div>` with click handlers instead of `<button>`
* ❌ Same font size for metric and unit label
* ❌ Multiple primary actions on one page (causes decision paralysis)
