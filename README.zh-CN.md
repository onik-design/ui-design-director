# UI Design Director (UI 设计决策系统)

[English](README.md) | 中文文档

> 面向中国 B 端（企业级）界面设计的综合设计系统与知识库

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Documentation](https://img.shields.io/badge/docs-comprehensive-brightgreen.svg)](ui-design-director/SKILL.md)

## 项目概述

**UI Design Director** 是一个文档驱动的设计系统，为创建面向中国用户的数据密集型、效率优先的企业界面提供结构化指南、原则和决策模式。

这不是一个组件库或框架 - 而是一个**设计智能系统**，帮助你基于业务数据的语义分析，做出关于布局、组件和视觉层级的明智决策。

## 核心理念

**"效率与确定性"**

- **降低认知负荷**：通过语义优先的设计简化决策过程
- **最大化屏效比**：优化中国 B 端用户的信息密度
- **意图优于外观**：定义数据的含义，而非外观

## 核心特性

### 1. 语义优先设计（A2UI）
自动将业务意图映射到视觉组件。将数据定义为 `CriticalAlert`（严重告警）而非"红色文本" - 系统自动处理视觉呈现。

### 2. 针对中文 B 端优化
- F 型扫描流优化
- 高信息密度且不混乱
- 中文排版规则（禁止斜体、正确行高）
- 关键指标的黄金三角位置

### 3. Tailwind CSS 集成
所有视觉建议使用与 Ant Design/Arco Design 标准对齐的 Tailwind 工具类。

### 4. ECharts 图表模式
针对常见业务图表的预配置模式，带有语义颜色映射。

### 5. 决策模板
组件选择指南，提供在 Badge、Timeline、DescriptionList、Table 等组件之间选择的明确标准。

## 快速开始

### 1. 理解角色定位
阅读 [SKILL.md](ui-design-director/SKILL.md) 了解 3 步设计流程：
- **分析意图**（语义层）
- **组织布局**（架构层）
- **精化细节**（视觉层）

### 2. 探索设计原则
访问 `principles/` 目录：

| 文档 | 用途 |
|------|------|
| [c01_cn_b_end_layout.md](ui-design-director/principles/c01_cn_b_end_layout.md) | 布局模式、网格系统、F 型扫描 |
| [c02_semantic_a2ui.md](ui-design-director/principles/c02_semantic_a2ui.md) | 语义映射、意图驱动设计（A2UI）|
| [c03_interaction_ux.md](ui-design-director/principles/c03_interaction_ux.md) | 中文排版、微交互、用户体验优化 |
| [c04_design_tokens.md](ui-design-director/principles/c04_design_tokens.md) | Tailwind CSS 设计令牌、颜色系统、间距 |

### 3. 使用组件模式
参考 [component_decision_patterns.md](ui-design-director/templates/component_decision_patterns.md) 获取：
- 组件选择标准
- ECharts 配置示例
- 语义颜色映射
- 无障碍访问指南

## 设计原则速览

### 状态颜色系统
```
严重（Critical）：  bg-red-50 text-red-700      （致命错误、需立即处理）
警告（Warning）：   bg-orange-50 text-orange-700 （需注意、非阻塞）
成功（Success）：   bg-green-50 text-green-700   （已完成、正向结果）
处理中（Processing）：bg-blue-50 text-blue-700   （进行中、加载中）
中性（Neutral）：   bg-gray-100 text-gray-500    （未激活、待定）
```

### 组件语义
| 数据类型 | 组件 | 视觉模式 |
|---------|------|---------|
| 枚举/状态 | Badge（徽章） | 圆角胶囊，语义颜色 |
| 键值对 | DescriptionList（描述列表） | `dl/dt/dd` 结构 |
| 时序事件 | Timeline（时间轴） | 垂直线带时间戳 |
| 表格数据 | Table（表格） | 数字右对齐，文本左对齐 |
| 单一 KPI | KeyMetric Typography（关键指标排版） | `text-2xl font-semibold tabular-nums` |

### 中文排版规则
- **字体栈**：`Inter`（数字） + `PingFang SC`（中文） + `Microsoft YaHei`（微软雅黑）
- **绝对禁止使用斜体** 渲染中文（CJK 字体斜体渲染损坏）
- **行高**：纯中文文本 1.75-2，中英混排 1.5
- **字重**：避免 `font-bold`(700) - 最多使用 `font-semibold`(600)

## 使用示例

### 输入：业务数据
```json
{
  "orderStatus": "pending_payment",
  "totalAmount": 156800,
  "createdAt": "2025-01-20T10:30:00Z",
  "urgencyLevel": "high"
}
```

### 输出：设计建议

**语义分析：**
- `orderStatus`（订单状态）：处理中状态 → Badge 组件 → `bg-blue-50 text-blue-700`
- `totalAmount`（总金额）：关键指标 → 带单位分隔的排版 → `text-2xl tabular-nums`
- `createdAt`（创建时间）：时间戳 → 次要标签 → `text-sm text-gray-400`
- `urgencyLevel`（紧急程度）：警告指示器 → Badge 组件 → `bg-orange-50 text-orange-700`

**布局结构：**
```
┌────────────────────────────────────┐
│ 订单 #12345 [待支付]              │
├────────────────────────────────────┤
│ ¥1,568.00                   [高]   │
│ 创建时间：2025-01-20 10:30        │
└────────────────────────────────────┘
```

## 仓库结构

```
ui-design-director/
├── SKILL.md                    # 主入口 - 角色定义和工作流
├── principles/                 # 核心设计原则
│   ├── c01_cn_b_end_layout.md # 布局模式、网格系统、F 型扫描
│   ├── c02_semantic_a2ui.md   # 语义映射、意图驱动设计（A2UI）
│   ├── c03_interaction_ux.md  # 中文排版、微交互、用户体验优化
│   ├── c04_design_tokens.md   # Tailwind CSS 设计令牌、颜色系统、间距
│   └── templates/
│       └── component_decision_patterns.md
└── templates/
    └── component_decision_patterns.md  # 组件选择指南、ECharts 模式
```

## 技术约束

- **CSS 框架**：纯 Tailwind CSS（不使用 Ant Design 等组件库）
- **图表库**：ECharts（主要推荐）
- **无障碍访问**：最低 WCAG AA 合规
- **浏览器支持**：现代常青浏览器（Chrome/Edge/Firefox/Safari 最新 2 个版本）
- **设计目标**：桌面优先（最小可行宽度：1024px）
- **主要断点**：xl (1280px)

## 常见布局模式

### 仪表盘概览
```
┌────────────────────────────────────────┐
│ [顶栏：标题 + 日期选择器]             │
├────────────────────────────────────────┤
│ [KPI 行：4 个卡片 grid-cols-4]        │
├────────────────────────────────────────┤
│ [图表：2 个图表 grid-cols-2]          │
├────────────────────────────────────────┤
│ [表格：最近活动]                      │
└────────────────────────────────────────┘
```

### 详情页
```
┌────────────────────────────────────────┐
│ [面包屑 + 标题 + 操作按钮]            │
├─────────────────┬──────────────────────┤
│ [左侧：核心]    │ [右侧：时间轴]       │
│ - 状态          │ - 变更历史           │
│ - 关键属性      │ - 评论               │
└─────────────────┴──────────────────────┘
```

## 何时使用本系统

本系统针对**中国 B 端企业界面**优化。适用于：
- 仪表盘和数据可视化平台
- 管理面板和运营控制台
- 企业 SaaS 应用
- 监控和分析工具
- 商业智能界面

## 何时不使用

以下情况不要使用：
- 项目需要营销/品牌导向设计（非数据密集型）
- 设计需要大量留白或极简美学
- 深色模式是主要需求（本系统专注浅色模式）
- 用户需要 CSS-in-JS 或组件库集成

## 设计验证清单

审查设计或实现时：
- [ ] 布局是否优先展示可操作信息而非美学？
- [ ] 关键指标是否位于左上象限（黄金三角）？
- [ ] 状态颜色是否语义化使用（非装饰性）？
- [ ] 中文文本是否使用正确行高（段落 ≥1.75）？
- [ ] 表格中数字是否右对齐并使用 `tabular-nums`？
- [ ] 单位是否与数字视觉分离（`text-sm text-gray-400`）？
- [ ] 所有交互元素是否有悬浮状态？
- [ ] 正文对比度是否 ≥4.5:1？
- [ ] 卡片是否使用 `rounded-lg`(8px)，按钮使用 `rounded`(4px)？
- [ ] 间距是否遵循 4px 网格（无 13px 等奇数值）？

## 参考资源

- [Ant Design Pro](https://preview.pro.ant.design/) - 企业级 UI 模式
- [Arco Design Pro](https://pro.arco.design/) - 字节跳动设计系统
- [TDesign Starter](https://tdesign.tencent.com/starter/) - 腾讯设计系统
- [ECharts 示例](https://echarts.apache.org/examples/) - 图表模式
- [WCAG 对比度检查器](https://webaim.org/resources/contrastchecker/) - 无障碍验证

## 贡献指南

这是一个文档驱动的仓库。贡献应专注于：
1. 基于实际使用完善设计原则
2. 添加新的组件决策模式
3. 扩展图表配置示例
4. 改进无障碍访问指南

贡献时：
- 保持语义优先的方法
- 使用 Tailwind CSS 工具类（非原始 CSS）
- 确保 WCAG AA 合规
- 验证中文排版规则

## 许可证

MIT 许可证 - 欢迎在你的项目中使用本设计系统。

## 致谢

基于以下最佳实践构建：
- Ant Design / Ant Design Pro
- Arco Design / Arco Design Pro
- TDesign
- Alibaba Fusion Design
- ECharts 可视化库

---

**为中国 B 端开发者和设计师用心打造**
