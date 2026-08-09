# 已有项目接入与持续约束

## 目录

- [目标](#目标)
- [建立现状基线](#1-建立现状基线)
- [解决 Design 冲突](#2-解决-design-冲突)
- [生成差距矩阵](#3-生成差距矩阵)
- [渐进式改造顺序](#4-渐进式改造顺序)
- [建立唯一项目入口](#5-建立唯一项目入口)
- [后续变更协议](#6-后续变更协议)
- [规则演进](#7-规则演进)

## 目标

允许从功能原型、半成品网站或视觉不统一的现有产品开始，在不破坏产品行为的前提下逐步应用 Taste Pack。

Taste Pack 是外部审美来源，不天然高于项目已有 Design，也不是要求推倒重写的页面模板。接入后以已解决的项目规则为准。

## 1. 建立现状基线

在修改前记录：

- 页面和路由清单；
- 已有组件、共享布局和设计 token；
- 已有 Design 文档、品牌指南及其作用域；
- 已实现的交互与业务状态；
- 桌面、平板和移动截图；
- 当前测试和可访问性约束；
- 不得改变的功能、文案和数据流程；
- 视觉债务与不一致位置。

不要把视觉问题误判为需要重写业务逻辑。

## 2. 解决 Design 冲突

读取 `references/design-conflict-resolution.md`，生成现有设计摘要、冲突矩阵、权威策略和已解决规则。

默认使用 `harmonize`。未经用户明确授权，不把“视觉效果不好”解释为允许 `migrate`。只有基于 `integration/resolved-rules.json` 才能生成改造方案。

## 3. 生成差距矩阵

对每个页面或组件记录：

| 对象 | 当前状态 | 相关已解决规则 | 差距 | 风险 | 改造阶段 | 验证方式 |
|---|---|---|---|---|---|---|
| `Header` | [...] | `attention.*` | [...] | 低 | 2 | 三视口截图 |

将差距分为：

- `foundation`：字体、颜色角色、间距尺度、容器和基础动效；
- `shared`：导航、按钮、输入、卡片、媒体容器等共享组件；
- `page`：页面构图、信息密度和内容层级；
- `exception`：业务约束导致的合理例外。

## 4. 渐进式改造顺序

默认按以下顺序执行：

1. 固定字体决策和品牌边界；
2. 校准全局基础关系；
3. 改造高复用共享组件；
4. 改造高流量或高视觉权重页面；
5. 处理长尾页面和明确例外；
6. 执行跨页面一致性审查。

每阶段保持功能可用并保存前后截图。除非用户明确要求，不把视觉改造和业务重构混在同一阶段。

## 5. 建立唯一项目入口

将完整 Taste Pack 保存在项目内，例如：

```text
taste/<site-slug>/TASTE.md
```

`TASTE.md` 是捕获结果的唯一来源入口。完成项目接入后，`integration/authority-policy.md` 是项目设计入口，`integration/resolved-rules.json` 是实现和审查使用的最终规则。不要把这些完整内容复制到 `AGENTS.md`、`CLAUDE.md`、`GEMINI.md`、Copilot、Cursor 或其他平台文件，否则后续会产生版本漂移。

在项目已有的 Agent 指令文档中追加一个带标记的短入口。保留所有既有内容，只更新标记范围：

```markdown
<!-- capture-taste:start -->
## Design Taste Contract

For every frontend, styling, layout, motion, or component change:

1. Read `taste/<site-slug>/integration/authority-policy.md` before planning.
2. Use `taste/<site-slug>/integration/resolved-rules.json` as the executable design rules.
3. Read the relevant Existing Design and `TASTE.md` sources when the authority policy points to them.
4. Cite the applied resolved rule IDs in the implementation plan.
5. Preserve product behavior unless the task explicitly changes it.
6. For a new component, follow `taste/<site-slug>/transfer/component-creation-policy.md`.
7. Run `taste/<site-slug>/evaluation/change-checklist.md` after implementation.
8. Do not declare completion while a hard gate or unresolved conflict blocks the change.
<!-- capture-taste:end -->
```

处理平台入口：

1. 更新项目已经存在且覆盖当前目录的 Agent 指令文件；
2. 如果没有任何可识别入口，创建根级 `AGENTS.md`；
3. 同时生成 `transfer/agent-instruction-snippet.md`，供未知平台手动引用；
4. 在 manifest 中记录更新过的入口文件和相对路径。

无法保证所有 AI 产品自动发现同一种文件名。可移植性来自 Markdown/JSON 核心协议和可复制的短入口，而不是声称存在通用自动加载机制。

## 6. 后续变更协议

每次前端变更必须执行：

### 实现前

- 读取 `integration/authority-policy.md` 和 `integration/resolved-rules.json`；
- 按权威策略读取相关 Existing Design 与 `TASTE.md` 来源；
- 确定任务涉及的规则 ID；
- 标记功能约束和允许变化；
- 判断是复用、扩展还是创建组件。

### 实现后

- 在要求的视口截图；
- 执行 `evaluation/change-checklist.md`；
- 新组件执行组件评分；
- 报告失败项、修订和有意例外；
- 如果新模式被重复使用至少两次，考虑将其提升为正式组件配方。

## 7. 规则演进

不得为了让当前实现“通过”而静默降低 Taste 或已解决规则。

修改核心规则时必须记录：

- 修改原因；
- 新证据；
- 受影响页面和组件；
- 是否改变品牌边界或字体决策；
- 旧规则到新规则的迁移说明。

Existing Design 或 Taste Pack 更新后，必须重新检查受影响的冲突并递增 `resolved-rules.json` 版本。不得只更新其中一份引用而保留过期裁决。

产品自身逐渐形成的新设计模式应标为 `project-derived`，不要伪称来自源网站。
