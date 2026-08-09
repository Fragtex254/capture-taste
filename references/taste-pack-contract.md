# Taste Pack 产物规范

## 目录

- [后续 Agent 的读取顺序](#后续-agent-的读取顺序)
- [TASTE.md](#tastemd)
- [机器可读规则](#机器可读规则)
- [组件配方](#组件配方)
- [应用约定](#应用约定)
- [验收](#验收)
- [已有项目接入](#已有项目接入)
- [字体决策](#字体决策)

完整的可选结构如下；根据深度与工作模式裁剪，不创建与当前任务无关的空文件：

```text
taste/<site-slug>/
├── TASTE.md
├── taste.manifest.json
├── SOURCE_MANIFEST.json
├── rules/
│   ├── design-rules.json
│   ├── tokens.json
│   ├── attention.md
│   ├── typography.md
│   ├── layout.md
│   ├── color.md
│   ├── geometry.md
│   ├── motion.md
│   └── restraint.md
├── recipes/
├── evaluation/
│   ├── acceptance-tests.md
│   ├── change-checklist.md
│   ├── component-scorecard.md
│   ├── failure-patterns.md
│   └── audit-prompt.md
├── transfer/
│   ├── brand-boundaries.md
│   ├── transfer-guide.md
│   ├── font-decision.md
│   ├── retrofit-plan.md
│   ├── component-creation-policy.md
│   ├── agent-instruction-snippet.md
│   └── agent-application-prompt.md
├── integration/
│   ├── existing-design-summary.md
│   ├── conflict-matrix.md
│   ├── authority-policy.md
│   └── resolved-rules.json
├── references/
└── evidence/
```

`quick` 至少生成 `TASTE.md`、`SOURCE_MANIFEST.json`、`taste.manifest.json`、`rules/design-rules.json`、`rules/typography.md`、`rules/restraint.md`、`transfer/brand-boundaries.md`、`transfer/font-decision.md` 和 `evaluation/acceptance-tests.md`。

只有 `integrate`、`apply` 或首次 `continue` 必须生成 `integration/`、`retrofit-plan.md`、`component-creation-policy.md`、`agent-instruction-snippet.md` 和 `change-checklist.md`。`capture` 模式可以预生成通用组件治理文件，但不得声称已经接入某个项目。

使用 `templates/SOURCE_MANIFEST.template.json` 记录来源和授权，使用 `templates/observation.template.json` 保存可追溯观察。规则中的 `evidence` 必须引用观察 ID。

## 后续 Agent 的读取顺序

尚未接入项目时：

1. `TASTE.md`
2. `rules/design-rules.json`
3. `transfer/brand-boundaries.md`
4. `transfer/font-decision.md`
5. 当前任务相关的组件配方
6. `evaluation/acceptance-tests.md`
7. 可选读取详细规则和视觉参考

已经接入项目时：

1. `integration/authority-policy.md`
2. `integration/resolved-rules.json`
3. 当前任务相关的 Existing Design 来源
4. `TASTE.md` 及相关证据
5. 当前任务相关的组件配方
6. `evaluation/change-checklist.md`

不要要求后续 Agent 在规划前读取全部文件。

## TASTE.md

使用：

`templates/TASTE.template.md`

它必须总结：

- 设计定义；
- 最高优先级规则；
- 必须保持稳定的关系；
- 可以改变的变量；
- 品牌排除项；
- 字体决策；
- 禁止走的捷径；
- 常见失败模式；
- 可用组件配方；
- 必须执行的应用流程。

## 机器可读规则

使用：

`templates/design-rule.template.json`

规则必须包含：

- 设计意图；
- 约束；
- 允许变化；
- 失败信号；
- 证据；
- 例外；
- 置信度。

## 组件配方

使用：

`templates/component-recipe.template.md`

源网站观察得到的配方标记为 `source-observed`，例如：

- Hero；
- Navigation；
- 内容区块；
- 媒体区块；
- Card；
- CTA。

产品后来需要、但源网站不存在的组件也可以生成配方，但必须标记为 `project-derived`，列出推导所依据的全局规则 ID，并通过组件评分。

组件配方描述设计关系，不复制原组件，也不得把 `project-derived` 模式伪称为源网站证据。

## 应用约定

后续 Coding Agent 必须：

1. 阅读 `TASTE.md`；
2. 理解新产品与用户；
3. 选择适用规则；
4. 先写 `DESIGN_PLAN.md`；
5. 解释规则如何迁移；
6. 替换所有源网站品牌身份；
7. 实现新界面；
8. 执行审美验收；
9. 修正失败项；
10. 报告无法完全满足的部分。

使用：

`templates/DESIGN_PLAN.template.md`

## 验收

使用：

`templates/acceptance-tests.template.md`

验收对象是新页面是否遵守 Taste Pack，而不是是否像素级接近源网站。

每次前端变更使用：

`templates/change-checklist.template.md`

创建源网站没有的新组件时，同时使用：

- `templates/component-scorecard.template.md`
- `references/component-governance.md`

组件必须保存规则映射、视觉证据、分项评分、硬性门槛和最终判定。

## 已有项目接入

`integrate` 和 `apply` 模式额外生成：

- `transfer/retrofit-plan.md`：现状基线、差距矩阵、分阶段改造计划；
- `transfer/component-creation-policy.md`：将组件治理规范转化为当前项目约束；
- `transfer/agent-instruction-snippet.md`：供不同 Agent 入口引用的短指令；
- `evaluation/change-checklist.md`：后续修改的固定验收门槛。
- `integration/existing-design-summary.md`：现有规范、实现和内部矛盾；
- `integration/conflict-matrix.md`：Existing Design 与 Taste 的逐项冲突；
- `integration/authority-policy.md`：接入策略和项目权威入口；
- `integration/resolved-rules.json`：后续实现与评分使用的最终规则。

按照 `references/design-conflict-resolution.md` 解决冲突，再按照 `references/project-integration.md` 更新项目已有 Agent 指令入口。平台入口文档只保存相对链接和执行要求。

完成接入时，将 `taste.manifest.json` 的 `project_entry` 设置为 `integration/authority-policy.md`，记录接入策略、Resolved Rules 版本和未解决硬冲突数量。未接入时保持 `project_entry: null`。


## 字体决策

字体不属于默认品牌隔离项。

必须按照 `references/font-policy.md` 生成：

`transfer/font-decision.md`

`TASTE.md` 必须明确告诉后续 Agent：

- 是否沿用目标字体；
- 字体是否允许自动安装；
- 字体文件是否允许进入仓库；
- 字体不可用时的替代顺序；
- 换字体后需要重新校准的排版参数。

`taste.manifest.json` 必须将 `transfer/font-decision.md` 放入必要读取顺序。
