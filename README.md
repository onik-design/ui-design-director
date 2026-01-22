# UI Design Director

[中文文档](README.zh-CN.md) | English

> A comprehensive Skill for Chinese B-End (enterprise) interface design - Structured design knowledge base that guides AI to provide expert design recommendations.

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Skill](https://img.shields.io/badge/Type-Skill-7C3AED.svg)](ui-design-director/SKILL.md)
[![Documentation](https://img.shields.io/badge/docs-comprehensive-brightgreen.svg)](ui-design-director/SKILL.md)

## What is This?

**UI Design Director** is a **Skill** - a structured knowledge base that enables AI assistants to act as expert design advisors for Chinese B-End (enterprise) interfaces.

Unlike traditional component libraries or frameworks, this is a **documentation-first design system** that contains:
- Semantic design principles (A2UI methodology)
- Layout patterns optimized for Chinese user scanning behaviors
- Component decision templates with clear selection criteria
- Tailwind CSS token system aligned with Chinese design standards
- ECharts configuration patterns for business visualization

**Value Proposition**: Transform any AI assistant into a senior Chinese B-End UI/UX designer who can analyze your business data and provide structured, actionable design guidance.

## What You'll Get

When an AI assistant uses this skill, it will provide:

1. **Semantic Analysis** - Business context understanding and data classification
2. **Layout Recommendations** - Page structure and information hierarchy strategies
3. **Component Mapping** - Specific component choices with Tailwind CSS classes
4. **Chart Recommendations** - ECharts configuration guidance for business scenarios
5. **Critical Reminders** - Accessibility compliance and Chinese typography best practices

### Example Interaction

```
You: I have an order management dashboard with this data:
{
  "orderId": "ORD-2025-001",
  "status": "pending_payment",
  "amount": 156800,
  "customer": "Acme Corp",
  "createdAt": "2025-01-20T10:30:00Z",
  "urgencyLevel": "high"
}

How should I design this interface?

AI Assistant (with UI Design Director):
[Provides semantic analysis, layout recommendations, component mapping,
and Tailwind CSS implementation suggestions following the 3-step methodology]
```

## Core Design Philosophy

This skill is built on **"Efficiency & Certainty" (效率与确定性)**:

- **Reduce Cognitive Load**: Simplify decision-making through semantic-first design
- **Maximize Screen Efficiency**: Optimize information density for Chinese B-End users
- **Intent Over Appearance**: Define what data means, not how it looks

### The 3-Step Methodology

AI assistants using this skill follow a structured process:

1. **Analyze Intent** (Semantic Layer) - What does the data mean in business context?
2. **Structure Layout** (Architecture Layer) - How should information be organized?
3. **Refine Details** (Visual Layer) - What are the specific implementation details?

## Key Features

### 1. Semantic-First Design (A2UI)
Map business intent to visual components automatically. Define data as `CriticalAlert` instead of "red text" - the system handles visual representation.

### 2. Chinese B-End Optimized
- F-pattern scanning flow optimization
- High information density without chaos
- Chinese typography rules (no italics, correct line-height)
- Golden triangle placement for key metrics

### 3. Tailwind CSS Integration
All visual recommendations use Tailwind utility classes aligned with Ant Design/Arco Design standards.

### 4. ECharts Patterns
Pre-configured patterns for common business charts with semantic color mapping.

### 5. Decision Templates
Component selection guides with clear criteria for choosing between Badge, Timeline, DescriptionList, Table, and more.

## Real-World Example

**User Input:**
```
I need to design a server monitoring dashboard. Each server has:
- status (running/stopped/error)
- CPU usage percentage
- memory usage
- last heartbeat timestamp
- alert level
```

**AI Response (Powered by This Skill):**

```
1. Semantic Analysis
   - Business Context: Real-time monitoring dashboard requiring quick status identification
   - Key Metrics: CPU/Memory (quantitative KPIs)
   - Status Indicators: Server status, alert level (categorical states)
   - Supporting Data: Last heartbeat (timestamp)

2. Layout Recommendation
   - Page Structure: Card-based grid layout (grid-cols-3 xl:grid-cols-4)
   - F-Pattern optimization: Status badge in top-left corner
   - Visual Hierarchy: Status → Metrics → Timestamp

3. Component Mapping
   - status: Badge component
     - running → bg-green-50 text-green-700
     - stopped → bg-gray-100 text-gray-500
     - error → bg-red-50 text-red-700

   - CPU/Memory: Progress bar with percentage typography
     - Container: h-2 bg-gray-100 rounded-full
     - Fill: bg-blue-500 (safe) / bg-orange-500 (warning) / bg-red-500 (critical)
     - Text: text-2xl font-semibold tabular-nums

   - lastHeartbeat: Relative timestamp
     - Style: text-sm text-gray-400
     - Format: "2分钟前" (2 minutes ago)

   - alertLevel: Badge component (top-right corner)
     - high → bg-orange-50 text-orange-700 border-orange-100

4. Implementation Hint (Tailwind)
   <div class="grid grid-cols-3 gap-4">
     <div class="bg-white border border-gray-100 rounded-lg p-4">
       <div class="flex items-start justify-between mb-3">
         <span class="bg-green-50 text-green-700 px-2 py-1 rounded text-xs">运行中</span>
         <span class="bg-orange-50 text-orange-700 px-2 py-1 rounded text-xs">高负载</span>
       </div>
       <!-- Metrics here -->
     </div>
   </div>
```

## Skill Architecture

This skill is organized as a structured knowledge base:

### Core Documents
- **[SKILL.md](ui-design-director/SKILL.md)** - Role definition and workflow methodology
- **[CLAUDE.md](CLAUDE.md)** - Integration guide and usage instructions

### Design Principles (Knowledge Base)
| Document | Purpose |
|----------|---------|
| [c01_cn_b_end_layout.md](ui-design-director/principles/c01_cn_b_end_layout.md) | Layout patterns, grid system, F-pattern scanning |
| [c02_semantic_a2ui.md](ui-design-director/principles/c02_semantic_a2ui.md) | Semantic mapping, intent-based design (A2UI) |
| [c03_interaction_ux.md](ui-design-director/principles/c03_interaction_ux.md) | Chinese typography, micro-interactions, UX polish |
| [c04_design_tokens.md](ui-design-director/principles/c04_design_tokens.md) | Tailwind CSS tokens, color system, spacing |

### Decision Templates
- **[component_decision_patterns.md](ui-design-director/templates/component_decision_patterns.md)** - Component selection guide and ECharts patterns

## Design Principles at a Glance

### Status Color System
```
Critical:    bg-red-50 text-red-700      (fatal errors, immediate action)
Warning:     bg-orange-50 text-orange-700 (attention needed, non-blocking)
Success:     bg-green-50 text-green-700   (completed, positive result)
Processing:  bg-blue-50 text-blue-700     (in progress, loading)
Neutral:     bg-gray-100 text-gray-500    (inactive, pending)
```

### Component Semantics
| Data Type | Component | Visual Pattern |
|-----------|-----------|----------------|
| Enum/Status | Badge | Rounded pill with semantic color |
| Key-Value Pairs | DescriptionList | `dl/dt/dd` structure |
| Sequential Events | Timeline | Vertical line with timestamps |
| Tabular Data | Table | Right-align numbers, left-align text |
| Single KPI | KeyMetric Typography | `text-2xl font-semibold tabular-nums` |

### Chinese Typography Rules
- **Font Stack**: `Inter` (numbers) + `PingFang SC` (Chinese) + `Microsoft YaHei`
- **NEVER use italic** for Chinese text (rendering is broken for CJK fonts)
- **Line Height**: 1.75-2 for pure Chinese text, 1.5 for mixed content
- **Font Weight**: Avoid `font-bold` (700) - use `font-semibold` (600) maximum

## Usage Example

### Input: Business Data
```json
{
  "orderStatus": "pending_payment",
  "totalAmount": 156800,
  "createdAt": "2025-01-20T10:30:00Z",
  "urgencyLevel": "high"
}
```

### Output: Design Recommendation

**Semantic Analysis:**
- `orderStatus`: ProcessingState → Badge component → `bg-blue-50 text-blue-700`
- `totalAmount`: KeyMetric → Typography with unit separation → `text-2xl tabular-nums`
- `createdAt`: Timestamp → Secondary label → `text-sm text-gray-400`
- `urgencyLevel`: Warning indicator → Badge component → `bg-orange-50 text-orange-700`

**Layout Structure:**
```
┌────────────────────────────────────┐
│ Order #12345 [Pending Payment]    │
├────────────────────────────────────┤
│ ¥1,568.00                   [High] │
│ Created: 2025-01-20 10:30         │
└────────────────────────────────────┘
```

## Repository Structure

```
ui-design-director/
├── SKILL.md                    # Main entry point - role definition and workflow
├── principles/                 # Core design principles
│   ├── c01_cn_b_end_layout.md # Layout patterns, grid system, F-pattern scanning
│   ├── c02_semantic_a2ui.md   # Semantic mapping, intent-based design (A2UI)
│   ├── c03_interaction_ux.md  # Chinese typography, micro-interactions, UX polish
│   ├── c04_design_tokens.md   # Tailwind CSS tokens, color system, spacing
│   └── templates/
│       └── component_decision_patterns.md
└── templates/
    └── component_decision_patterns.md  # Component selection guide, ECharts patterns
```

## Technical Constraints

- **CSS Framework**: Pure Tailwind CSS (no component libraries like Ant Design)
- **Chart Library**: ECharts (primary recommendation)
- **Accessibility**: WCAG AA minimum compliance
- **Browser Support**: Modern evergreen browsers (Chrome/Edge/Firefox/Safari latest 2 versions)
- **Design Target**: Desktop-first (minimum viable width: 1024px)
- **Primary Breakpoint**: xl (1280px)

## Common Layout Patterns

### Dashboard Overview
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

### Detail Page
```
┌────────────────────────────────────────┐
│ [Breadcrumb + Title + Actions]        │
├─────────────────┬──────────────────────┤
│ [Left: Core]    │ [Right: Timeline]    │
│ - Status        │ - Change History     │
│ - Key Attrs     │ - Comments           │
└─────────────────┴──────────────────────┘
```

## Use Cases

This skill is optimized for **Chinese B-End enterprise interfaces**, including:
- Dashboard and data visualization platforms
- Admin panels and operation consoles
- Enterprise SaaS applications
- Monitoring and analytics tools
- Business intelligence interfaces
- Data-dense management systems

**Typical Design Scenarios:**
- Designing admin dashboard layouts with multiple KPIs
- Selecting appropriate components for status indicators
- Organizing complex data tables with Chinese text
- Configuring ECharts for time-series or categorical data
- Optimizing information density without creating visual chaos

## When NOT to Use

This skill may not be suitable if:
- The project requires marketing/brand-focused design (not data-dense)
- The design needs extensive whitespace or minimal aesthetics
- Dark mode is a primary requirement (this focuses on light mode)
- You need component library-specific implementation (Ant Design, Material-UI, etc.)

## Design Validation Checklist

When reviewing designs or implementations:
- [ ] Does the layout prioritize actionable information over aesthetics?
- [ ] Are key metrics placed in the top-left quadrant (golden triangle)?
- [ ] Are status colors used semantically (not decoratively)?
- [ ] Is Chinese text using correct line-height (≥1.75 for paragraphs)?
- [ ] Are numbers right-aligned in tables with `tabular-nums`?
- [ ] Are units visually separated from numbers (`text-sm text-gray-400`)?
- [ ] Do all interactive elements have hover states?
- [ ] Is contrast ratio ≥4.5:1 for body text?
- [ ] Are cards using `rounded-lg` (8px) and buttons using `rounded` (4px)?
- [ ] Is spacing following the 4px grid (no odd values like 13px)?

## References

- [Ant Design Pro](https://preview.pro.ant.design/) - Enterprise UI patterns
- [Arco Design Pro](https://pro.arco.design/) - ByteDance design system
- [TDesign Starter](https://tdesign.tencent.com/starter/) - Tencent design system
- [ECharts Examples](https://echarts.apache.org/examples/) - Chart patterns
- [WCAG Contrast Checker](https://webaim.org/resources/contrastchecker/) - Accessibility validation

## Contributing

This is a documentation-first repository. Contributions should focus on:
1. Refining design principles based on real-world usage
2. Adding new component decision patterns
3. Expanding chart configuration examples
4. Improving accessibility guidelines

When contributing:
- Maintain the semantic-first approach
- Use Tailwind CSS utility classes (not raw CSS)
- Ensure WCAG AA compliance
- Validate Chinese typography rules

## License

MIT License - Feel free to use this design system in your projects.

## Acknowledgments

Built on best practices from:
- Ant Design / Ant Design Pro
- Arco Design / Arco Design Pro
- TDesign
- Alibaba Fusion Design
- ECharts visualization library

---

**Made with ❤️ for Chinese B-End developers and designers**
