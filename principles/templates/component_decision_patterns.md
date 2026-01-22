# Component Decision Patterns

## Overview

This document provides decision-making patterns for selecting and designing components in Chinese B-End interfaces.

**Structure:**

* **Basic Components** - UI elements for data display and status
* **Data Display Components** - Complex structures for tables and grids
* **Chart Components (ECharts)** - Data visualization patterns

---

## Part 1: Basic Components

### 1.1 Badge / Status Indicator

#### When to Use

* **Data Type** : Enum values with ≤10 possible states
* **Semantic Intent** : Discrete status or category (not continuous values)
* **Character Length** : 1-10 characters (Chinese: 2-5 chars)

#### Decision Matrix

| Status Semantic      | Badge Style  | Tailwind Classes                                          | Icon           |
| -------------------- | ------------ | --------------------------------------------------------- | -------------- |
| **Critical**   | Red badge    | `bg-red-50 text-red-700 border border-red-100`          | X-Circle       |
| **Warning**    | Orange badge | `bg-orange-50 text-orange-700 border border-orange-100` | Alert-Triangle |
| **Success**    | Green badge  | `bg-green-50 text-green-700 border border-green-100`    | Check-Circle   |
| **Processing** | Blue badge   | `bg-blue-50 text-blue-700 border border-blue-100`       | Loader         |
| **Neutral**    | Gray badge   | `bg-gray-100 text-gray-500`                             | —             |

#### Design Recommendations

* **Padding** : `px-2 py-1` (compact) or `px-2.5 py-0.5` (standard)
* **Font Size** : `text-xs` (12px) for most cases
* **Border Radius** : `rounded` (4px) or `rounded-full` (pill shape)
* **Font Weight** : `font-medium` (500)
* **Placement** :
* In tables: Right-aligned in status columns
* In cards: Top-right corner or inline after title
* In lists: Left-aligned before item title

---

### 1.2 Tag (Multi-Category)

#### When to Use

* **Data Type** : Multiple categories applied to one object
* **Semantic Intent** : Filtering/grouping dimensions (not status)
* **Examples** : Skills, product tags, topic labels

#### vs Badge

* **Badge** : Single status (mutually exclusive)
* **Tag** : Multiple categories (can coexist)

#### Design Recommendations

* **Style** : `bg-gray-100 text-gray-700 text-xs px-2 py-1 rounded`
* **Hover** : If clickable → `hover:bg-gray-200 cursor-pointer`
* **Close Icon** : If removable → Add X icon with `hover:text-red-600`
* **Max Display** : Show 3-5 tags, hide rest behind "+N more"

---

### 1.3 DescriptionList (Key-Value Pairs)

#### When to Use

* **Data Type** : Structured attributes of a business object
* **Semantic Intent** : Present object metadata (not transactional data)
* **Examples** : User profile, order details, device specifications

#### Layout Options

**Option A: 2-Column Grid (Compact)**

* **Use Case** : Space-constrained cards, 5-10 attributes
* **Tailwind Structure** : `grid grid-cols-2 gap-4`

```
Label    Value
Label    Value
```

**Option B: Horizontal Inline (Dense)**

* **Use Case** : Single-row summaries, 2-4 attributes
* **Tailwind Structure** : `flex gap-6`

```
Label: Value  |  Label: Value
```

**Option C: Stacked (Spacious)**

* **Use Case** : Detail pages, emphasize readability
* **Tailwind Structure** : `space-y-3`

```
Label
Value

Label
Value
```

#### Design Recommendations

* **Label Style** : `text-xs text-gray-500` (uppercase optional)
* **Value Style** : `text-sm text-gray-900 font-medium`
* **Empty Values** : Hide the entire row (don't show "N/A")
* **Long Values** : Truncate with `truncate` + tooltip, or allow wrapping with `break-words`

---

### 1.4 Timeline (Sequential Events)

#### When to Use

* **Data Type** : Chronological events or change history
* **Semantic Intent** : Show "what happened when" (audit trail)
* **Examples** : Order status changes, approval workflow, system logs

#### Design Pattern

**Vertical Timeline (Standard for B-End):**

```
[Time]  [Icon]  [Title]
              [Description]
              [Metadata]
   |
   |
[Time]  [Icon]  [Title]
              ...
```

#### Decision Points

| Attribute                  | Options                | Recommendation                                                    |
| -------------------------- | ---------------------- | ----------------------------------------------------------------- |
| **Icon**             | Colored dots vs icons  | Use status-semantic icons (Check, Alert, X)                       |
| **Line Color**       | Gray vs status-colored | Gray (`border-gray-200`) for neutrality                         |
| **Timestamp Format** | Absolute vs relative   | Absolute for audit logs, relative for recent activity             |
| **Density**          | Compact vs spacious    | Compact (`gap-3`) for logs, spacious (`gap-4`) for milestones |

#### Design Recommendations

* **Time Style** : `text-xs text-gray-400` (right-aligned or above icon)
* **Title Style** : `text-sm font-medium text-gray-900`
* **Description Style** : `text-sm text-gray-600`
* **Icon Size** : `h-5 w-5` (20px)
* **Line Width** : `border-l-2` (2px)
* **Max Items** : Show latest 5-10, collapse rest behind "View All"

---

## Part 2: Data Display Components

### 2.1 Table (Complex Lists)

#### When to Use

* **Data Type** : Tabular data with ≥3 columns
* **Semantic Intent** : Compare, sort, filter multiple objects
* **Examples** : Order lists, user management, inventory

#### Design Recommendations

**Header Row**

```html
<th class="px-4 py-3 text-left text-xs text-gray-500 uppercase tracking-wide">
  Column Name
</th>
```

**Body Row**

```html
<td class="px-4 py-3 text-sm text-gray-900">Cell Content</td>
```

**Column Alignment**

* **Text** : Left-aligned (`text-left`)
* **Numbers** : Right-aligned (`text-right tabular-nums`)
* **Status Badges** : Center-aligned (`text-center`)
* **Actions** : Right-aligned (`text-right`)

**Row Actions**

* **Hover Reveal** : Show action buttons only on row hover
* **Overflow Menu** : Use "..." icon for 3+ actions
* **Inline Actions** : Primary action as text link (e.g., "View"), destructive as red text (e.g., "Delete")

**Empty State**

```html
<tr>
  <td colspan="5" class="px-4 py-8 text-center text-sm text-gray-500">
    No data available
  </td>
</tr>
```

---

### 2.2 Card Grid (KPI Dashboard)

#### When to Use

* **Data Type** : Key metrics (numbers + trends)
* **Semantic Intent** : Quick overview of performance indicators
* **Examples** : Sales dashboard, system health, user analytics

#### Layout Pattern

**4-Column Grid (≥1920px):**

```html
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
  ...
</div>
```

**Responsive Breakpoints:**

* `lg:grid-cols-4` (≥1024px: 4 columns)
* `md:grid-cols-2` (768-1023px: 2 columns)
* `grid-cols-1` (<768px: 1 column)

#### Card Structure

```
[Icon]  [Label]
        [Big Number]
        [Trend Indicator]
        [Helper Text]
```

#### Design Recommendations

1. **Card Container:**
   ```
    bg-white border border-gray-100 shadow-sm rounded-lg p-4
   ```
2. **Icon (Optional)** : `h-8 w-8 text-blue-600` (left or top-left)
3. **Label** : `text-xs text-gray-500 uppercase tracking-wide`
4. **Key Metric** : `text-2xl font-semibold text-gray-900 tabular-nums`
5. **Trend Indicator:**
   * Positive: `text-green-600 text-sm` + ↑ icon
   * Negative: `text-red-600 text-sm` + ↓ icon
   * Neutral: `text-gray-500 text-sm` + → icon
6. **Helper Text** : `text-xs text-gray-400`

---

## Part 3: Chart Components (ECharts)

### Overview

**ECharts** is the primary recommendation for Chinese B-End data visualization due to:

* Wide adoption in Chinese tech companies
* Rich configuration options for business scenarios
* Good Chinese localization
* Strong mobile responsiveness

**CDN Reference:**

```html
<script src="https://cdn.jsdelivr.net/npm/echarts@5/dist/echarts.min.js"></script>
```

---

### 3.1 Core KPI Display (Dashboard Hero)

#### Data Characteristics

* Single numeric value with optional trend
* **Business Scenario** : Homepage dashboard, executive summary
* **User Goal** : Quick health check (at-a-glance monitoring)

#### Recommended Approach

**Primary: Large Number + Mini Chart (Sparkline)**

**Visual Structure:**

```
[Label]
[Big Number]  [Mini Trend Line]
[% Change] [Time Period]
```

**ECharts Configuration (Sparkline):**

```javascript
option = {
  grid: { top: 0, right: 0, bottom: 0, left: 0 },  // No margins
  xAxis: { type: 'category', show: false },         // Hide axis
  yAxis: { type: 'value', show: false },
  series: [{
    type: 'line',
    data: [120, 200, 150, 80, 70, 110, 130],
    smooth: true,
    symbol: 'none',                                 // No data point markers
    lineStyle: { color: '#2563eb', width: 2 },
    areaStyle: { color: 'rgba(37, 99, 235, 0.1)' }, // Optional fill
  }]
}
```

 **Container** : `height: 60px` (compact)

---

### 3.2 Time Series Analysis (Trend Monitoring)

#### Data Characteristics

* Time-based data (daily/weekly/monthly metrics)
* **Business Scenario** : Sales trends, traffic analytics, system metrics
* **User Goal** : Identify patterns, detect anomalies

#### Recommended Chart Types

**A. Line Chart (Single Metric Over Time)**

 **Use When** : Focus on trend (growth/decline)

**ECharts Key Config:**

```javascript
option = {
  xAxis: {
    type: 'time',                      // Auto-format dates
    boundaryGap: false                 // Line starts at edge
  },
  yAxis: { type: 'value' },
  series: [{
    type: 'line',
    data: [[timestamp, value], ...],   // [Date, Number] pairs
    smooth: true,                      // Smooth curves
    lineStyle: { color: '#2563eb' },
    areaStyle: { color: 'rgba(37, 99, 235, 0.1)' }  // Optional fill
  }],
  tooltip: { trigger: 'axis' },        // Vertical crosshair
  dataZoom: [{ type: 'inside' }]       // Enable scroll zoom
}
```

**Style Hints:**

* Container: `bg-white p-4 rounded-lg`
* Height: `300px` (standard) or `400px` (emphasis)
* Color: Use `blue-600` for primary metric

**B. Multi-Line Chart (Compare Metrics)**

 **Use When** : Compare 2-3 related metrics (e.g., Revenue vs Cost vs Profit)

**ECharts Key Config:**

```javascript
series: [
  { type: 'line', name: 'Revenue', data: [...], lineStyle: { color: '#2563eb' } },
  { type: 'line', name: 'Cost', data: [...], lineStyle: { color: '#ea580c' } },
  { type: 'line', name: 'Profit', data: [...], lineStyle: { color: '#16a34a' } }
],
legend: {
  bottom: 0,                          // Place at bottom (not top)
  textStyle: { fontSize: 12 }
}
```

 **Rule** : Max 3 lines (more = use separate charts or filters)

---

### 3.3 Categorical Comparison (Performance Benchmarking)

#### Data Characteristics

* Multiple categories compared on same metric
* **Business Scenario** : Department sales, product rankings, regional performance
* **User Goal** : Identify best/worst performers

#### Recommended Chart Types

**A. Bar Chart (Horizontal Comparison)**

 **Use When** : 5-15 categories, long category names

**ECharts Key Config:**

```javascript
option = {
  xAxis: { type: 'value' },           // Numbers on X-axis
  yAxis: {
    type: 'category',
    data: ['Product A', 'Product B', ...],
    axisLabel: { fontSize: 12 }
  },
  series: [{
    type: 'bar',
    data: [120, 200, 150, ...],
    itemStyle: { color: '#2563eb' },
    label: {
      show: true,                     // Show values on bars
      position: 'right',
      fontSize: 12
    }
  }]
}
```

**Style Hints:**

* Use horizontal bars if category names > 6 characters (Chinese: >3 chars)
* Sort by value (descending) for rankings

**B. Column Chart (Vertical Comparison)**

 **Use When** : <10 categories, short category names

**ECharts Key Config:**

```javascript
option = {
  xAxis: {
    type: 'category',
    data: ['Mon', 'Tue', 'Wed', ...]
  },
  yAxis: { type: 'value' },
  series: [{
    type: 'bar',
    data: [120, 200, 150, ...],
    itemStyle: { color: '#2563eb' },
    label: { show: true, position: 'top' }  // Values above bars
  }]
}
```

**Style Hints:**

* Max bar width: `barMaxWidth: 60` (prevent overly wide bars)

**C. Grouped Bar Chart (Multi-Dimension Comparison)**

 **Use When** : Compare 2-3 metrics across categories (e.g., This Year vs Last Year)

**ECharts Key Config:**

```javascript
series: [
  { type: 'bar', name: '2023', data: [120, 200, 150] },
  { type: 'bar', name: '2024', data: [150, 220, 180] }
]
```

**Color Recommendation:**

* First metric: `blue-600`
* Second metric: `orange-500`
* Third metric: `green-500`

---

### 3.4 Part-to-Whole Analysis (Composition)

#### Data Characteristics

* Percentage or ratio data (parts add up to 100%)
* **Business Scenario** : Market share, traffic sources, budget allocation
* **User Goal** : Understand composition

#### Recommended Chart Types

**A. Pie Chart**

 **Use When** : ≤6 categories, simple composition

**ECharts Key Config:**

```javascript
series: [{
  type: 'pie',
  radius: '60%',                      // Size relative to container
  data: [
    { value: 335, name: 'Product A' },
    { value: 234, name: 'Product B' },
    ...
  ],
  label: {
    formatter: '{b}: {d}%'            // "Name: 25%"
  },
  emphasis: {                         // Hover effect
    itemStyle: {
      shadowBlur: 10,
      shadowColor: 'rgba(0, 0, 0, 0.5)'
    }
  }
}]
```

 **Anti-Pattern** : >6 slices (hard to distinguish)

**B. Donut Chart (Ring Chart)**

 **Use When** : Want to display a total in the center

**ECharts Key Config:**

```javascript
series: [{
  type: 'pie',
  radius: ['40%', '70%'],             // Inner & outer radius (creates ring)
  data: [...],
  label: { position: 'outside' }      // Labels outside ring
}]
```

 **Center Content** : Add total number or key metric as HTML overlay (absolute positioning)

---

### 3.5 Distribution & Correlation (Advanced Analytics)

#### A. Scatter Plot

 **Use When** : Show relationship between 2 variables (e.g., User Age vs Spending)

**ECharts Key Config:**

```javascript
xAxis: { type: 'value', name: 'Age' },
yAxis: { type: 'value', name: 'Spending' },
series: [{
  type: 'scatter',
  data: [[28, 120], [35, 200], ...],  // [X, Y] pairs
  symbolSize: 8,
  itemStyle: { color: '#2563eb' }
}]
```

#### B. Heatmap (Time-Based Patterns)

 **Use When** : Show activity intensity (e.g., Commit heatmap, sales by day/hour)

**ECharts Key Config:**

```javascript
xAxis: { type: 'category', data: ['Mon', 'Tue', ...] },
yAxis: { type: 'category', data: ['00:00', '01:00', ...] },
series: [{
  type: 'heatmap',
  data: [[0, 0, 5], [0, 1, 12], ...],  // [x, y, value]
  label: { show: true },
  itemStyle: {
    borderWidth: 1,
    borderColor: '#fff'
  }
}],
visualMap: {
  min: 0,
  max: 100,
  calculable: true,
  orient: 'horizontal',
  left: 'center',
  bottom: '0%',
  inRange: {
    color: ['#f0f9ff', '#2563eb']    // Light to dark blue
  }
}
```

#### C. Gauge Chart (Progress/KPI Meter)

 **Use When** : Show progress toward a target (e.g., Completion rate, risk score)

**ECharts Key Config:**

```javascript
series: [{
  type: 'gauge',
  data: [{ value: 75, name: 'Completion' }],
  detail: { formatter: '{value}%' },
  axisLine: {
    lineStyle: {
      color: [
        [0.3, '#16a34a'],             // Green: 0-30%
        [0.7, '#ea580c'],             // Orange: 30-70%
        [1, '#dc2626']                // Red: 70-100%
      ]
    }
  }
}]
```

---

### 3.6 Chart Design Best Practices

#### Color Palette

**Single-Series Charts (Line/Bar):**

* Primary: `#2563eb` (blue-600)

**Multi-Series Charts:**

* Series 1: `#2563eb` (Blue)
* Series 2: `#ea580c` (Orange)
* Series 3: `#16a34a` (Green)
* Series 4: `#8b5cf6` (Purple)
* Series 5: `#ec4899` (Pink)

**Status-Based Colors (Gauge/Heatmap):**

* Good: `#16a34a` (Green)
* Warning: `#ea580c` (Orange)
* Critical: `#dc2626` (Red)

#### Typography in Charts

**Title (if used):**

```javascript
title: {
  text: 'Revenue Trend',
  textStyle: { fontSize: 16, fontWeight: 500, color: '#111827' }
}
```

**Axis Labels:**

```javascript
axisLabel: { fontSize: 12, color: '#6b7280' }
```

**Tooltip:**

```javascript
tooltip: {
  textStyle: { fontSize: 12 },
  backgroundColor: 'rgba(0,0,0,0.8)',
  borderWidth: 0
}
```

#### Responsive Sizing

**Container Heights:**

* Mini Chart (Sparkline): `60px`
* Standard Chart: `300px`
* Emphasized Chart: `400px`
* Full-Height Chart: `calc(100vh - 200px)` (rare)

 **Responsive Width** : Always use `width: 100%` (fill parent container)

#### Accessibility

 **Tooltip** : Always enable to show exact values on hover

```javascript
tooltip: { trigger: 'axis' }  // For line/bar
tooltip: { trigger: 'item' }  // For pie/scatter
```

 **Data Labels** : Show labels for critical metrics

```javascript
label: { show: true, position: 'top', fontSize: 12 }
```

 **Legend** : Use text legends (not color-only)

```javascript
legend: {
  bottom: 0,
  textStyle: { fontSize: 12, color: '#374151' }
}
```

---

## Decision Flowchart for Chart Selection

```
Is the data time-based?
├─ Yes → Line Chart (single metric) or Multi-Line Chart (compare)
└─ No → Continue

Are you showing composition (parts of a whole)?
├─ Yes → Pie Chart (≤6 categories) or Donut Chart
└─ No → Continue

Are you comparing categories?
├─ Yes → Bar Chart (horizontal) or Column Chart (vertical)
└─ No → Continue

Are you showing distribution or correlation?
├─ Yes → Scatter Plot (correlation) or Heatmap (patterns)
└─ No → Continue

Are you showing progress toward a goal?
├─ Yes → Gauge Chart
└─ No → Consider a custom visualization or table
```

---

## When NOT to Use Charts

**Use Tables Instead when:**

* Users need exact values (not just trends)
* Data has >5 dimensions (too complex for chart)
* Data is non-numeric (textual attributes)

**Use Big Numbers + Sparklines when:**

* Only 1-3 metrics to display
* Screen space is limited (dashboard cards)
* Users care about current value more than history

---

## Chart Container Pattern (Standard)

**HTML Structure:**

```html
<div class="bg-white border border-gray-100 rounded-lg p-4">
  <!-- Chart Header (Optional) -->
  <div class="flex items-center justify-between mb-4">
    <h3 class="text-lg font-medium text-gray-900">Revenue Trend</h3>
    <div class="text-xs text-gray-400">Last 30 Days</div>
  </div>

  <!-- Chart Container -->
  <div id="chart" style="width: 100%; height: 300px;"></div>
</div>
```

**JavaScript Initialization:**

```javascript
const chartDom = document.getElementById('chart');
const myChart = echarts.init(chartDom);
myChart.setOption(option);

// Auto-resize on window resize
window.addEventListener('resize', () => myChart.resize());
```

---

## Minimal Code Example Request Policy

When user explicitly asks  **"Show me ECharts config for [chart type]"** :

✅  **Provide** : Minimal `option` object (10-15 lines)

❌  **Do NOT provide** : Full HTML page, complete initialization code, complex styling

**Example Response Format:**

```
Here's the minimal ECharts configuration:

[Code block with option object]

Key decisions:
- [Explain 2-3 critical config choices]

Container requirements:
- Height: 300px
- Background: white card with border
```

---

This completes the component decision patterns. Always cross-reference with:

* `principles/c02_semantic_a2ui.md` for semantic mappings
* `principles/c04_design_tokens.md` for Tailwind classes
