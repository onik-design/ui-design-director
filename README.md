# UI Design Director

[中文文档](README.zh-CN.md) | English

> A comprehensive design system and knowledge base for Chinese B-End (enterprise) interface design.

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Documentation](https://img.shields.io/badge/docs-comprehensive-brightgreen.svg)](ui-design-director/SKILL.md)

## Overview

**UI Design Director** is a documentation-first design system that provides structured guidelines, principles, and decision-making patterns for creating data-dense, efficiency-focused business interfaces optimized for Chinese users.

This is not a component library or framework - it's a **design intelligence system** that helps you make informed decisions about layout, components, and visual hierarchy based on semantic analysis of your business data.

## Core Philosophy

**"Efficiency & Certainty" (效率与确定性)**

- **Reduce Cognitive Load**: Simplify decision-making through semantic-first design
- **Maximize Screen Efficiency**: Optimize information density for Chinese B-End users
- **Intent Over Appearance**: Define what data means, not how it looks

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

## Quick Start

### 1. Understand the Role
Read [SKILL.md](ui-design-director/SKILL.md) to understand the 3-step design process:
- **Analyze Intent** (Semantic Layer)
- **Structure Layout** (Architecture Layer)
- **Refine Details** (Visual Layer)

### 2. Explore Design Principles
Navigate to the `principles/` directory:

| Document | Purpose |
|----------|---------|
| [c01_cn_b_end_layout.md](ui-design-director/principles/c01_cn_b_end_layout.md) | Layout patterns, grid system, F-pattern scanning |
| [c02_semantic_a2ui.md](ui-design-director/principles/c02_semantic_a2ui.md) | Semantic mapping, intent-based design (A2UI) |
| [c03_interaction_ux.md](ui-design-director/principles/c03_interaction_ux.md) | Chinese typography, micro-interactions, UX polish |
| [c04_design_tokens.md](ui-design-director/principles/c04_design_tokens.md) | Tailwind CSS tokens, color system, spacing |

### 3. Use Component Patterns
Refer to [component_decision_patterns.md](ui-design-director/templates/component_decision_patterns.md) for:
- Component selection criteria
- ECharts configuration examples
- Semantic color mapping
- Accessibility guidelines

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

## When to Use This System

This system is optimized for **Chinese B-End enterprise interfaces**. Ideal for:
- Dashboard and data visualization platforms
- Admin panels and operation consoles
- Enterprise SaaS applications
- Monitoring and analytics tools
- Business intelligence interfaces

## When NOT to Use

Do NOT use if:
- The project requires marketing/brand-focused design (not data-dense)
- The design needs extensive whitespace or minimal aesthetics
- Dark mode is a primary requirement (this focuses on light mode)
- The user needs CSS-in-JS or component library integration

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
