# 现有 Design 与 Taste 冲突解决

## 目录

- [基本定义](#基本定义)
- [权威层级](#权威层级)
- [接入策略](#接入策略)
- [发现现有规范](#发现现有规范)
- [冲突分类](#冲突分类)
- [裁决方法](#裁决方法)
- [最终产物](#最终产物)
- [后续 Agent 读取顺序](#后续-agent-读取顺序)

## 基本定义

- **Existing Design**：项目已经声明的品牌规范、设计系统、token、组件规范和设计决策。
- **Taste Pack**：从外部来源提取的审美语法，不天然拥有项目最高优先级。
- **Current Implementation**：现状证据，不自动等于规范；实现可能已经偏离 Existing Design。
- **Resolved Rules**：经过冲突检查和接入决策后，当前项目真正可执行的规则。

不要直接让 Taste 覆盖 Existing Design，也不要因为项目已有 Design 文档就拒绝所有 Taste 改善。

## 权威层级

按以下顺序裁决：

1. 用户对当前任务的明确决定；
2. 法律、字体许可、安全、可访问性和不可改变的产品行为；
3. Existing Design 中标记为品牌级、系统级或硬约束的规则；
4. `integration/resolved-rules.json` 中已经确认的项目规则；
5. 可迁移的 Taste 规则；
6. Current Implementation；
7. Agent 自行偏好。

较高层级只在相同作用域发生真实冲突时覆盖较低层级。不要用全局品牌规则错误覆盖与其无关的局部布局规则。

## 接入策略

### `augment`

Existing Design 为主。Taste 只填补没有定义的审美关系，不能改变已有规则。

适用于成熟、稳定的设计系统。

### `harmonize`

默认策略。保留 Existing Design 的品牌、语义、功能和硬约束；使用 Taste 改善注意力、密度、空间、材质和动效，并对直接冲突进行映射或限定作用域。

适用于已有规范但最终效果仍不协调的项目。

### `migrate`

Taste 成为新的视觉方向。Existing Design 只保留法律、品牌、功能、可访问性和用户明确指定的约束。

只有用户明确授权重新设计或替换现有视觉系统时才能使用。页面“看起来不好”不能自动视为迁移授权。

## 发现现有规范

检查项目中已有的：

- Agent 指令和设计说明；
- 品牌指南、设计系统文档、Figma 导出说明；
- CSS 变量、主题、token 文件和 Tailwind 等配置；
- 共享组件与 Storybook；
- 字体、图标、颜色和动效约定；
- 测试、可访问性和产品状态约束。

分别记录 `declared` 和 `implemented`。当文档与实现不一致时，不擅自把实现提升为规则；将其标为现有设计债务。

## 冲突分类

- `compatible`：两套规则可以同时满足。
- `gap`：Existing Design 未定义，可采用 Taste。
- `soft-conflict`：可通过映射、缩放、限定组件或页面范围融合。
- `hard-conflict`：同一作用域的要求互斥，必须裁决。
- `internal-conflict`：Existing Design 自身的文档、token 或实现互相矛盾。

每项冲突记录作用域、双方规则 ID、证据、建议、风险和最终决定。

## 裁决方法

对 `compatible` 直接合并。对 `gap` 按接入策略决定是否采用 Taste。对 `soft-conflict` 生成明确映射，例如：

- 保留品牌色，迁移强调色面积比例；
- 保留品牌字体，迁移字号反差、行宽和换行节奏；
- 保留组件语义与 API，调整内部空间和视觉层级；
- 将 Taste 的大圆角限制在媒体容器，而不改变表单控件。

对影响品牌、字体、全局 token、共享组件 API 或大量页面的 `hard-conflict`，先提出建议并请求用户决定。等待期间可以处理不冲突的规则，但不得实施冲突部分。

对 `internal-conflict` 不替项目猜测真实规范；报告矛盾，并让用户选择来源或批准整理方案。

## 最终产物

生成：

```text
integration/
├── existing-design-summary.md
├── conflict-matrix.md
├── authority-policy.md
└── resolved-rules.json
```

`authority-policy.md` 是已接入项目的设计入口。它声明策略、权威层级、原始规范位置和未解决冲突。

`resolved-rules.json` 是后续实现、组件创建和评分使用的机器可读规则。每条规则必须记录：

- 最终约束；
- 作用域；
- 来源规则 ID；
- 来源类型；
- 解决方式；
- 覆盖或保留的内容；
- 用户决定或推导依据；
- 状态与版本。

不要修改或删除原始 Taste 证据来制造一致。不要静默改写 Existing Design 文档。需要正式迁移规范时，把它作为后续明确任务执行。

## 后续 Agent 读取顺序

项目已经接入时：

1. `integration/authority-policy.md`；
2. `integration/resolved-rules.json`；
3. 原 Existing Design 文档中与当前任务相关的部分；
4. `TASTE.md` 及其证据；
5. 当前任务相关的组件配方和验收标准。

如果不存在 `integration/authority-policy.md`，说明尚未完成接入，不得假设 Taste 已成为项目规范。
