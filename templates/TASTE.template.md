# 核心设计品味

## 一句话定义

[通过具体视觉原因描述这套设计语言。]

## 设计性格

- [特征]：[形成该特征的视觉原因]
- [特征]：[形成该特征的视觉原因]
- [特征]：[形成该特征的视觉原因]

## 最高优先级规则

1. [...]
2. [...]
3. [...]
4. [...]
5. [...]

## 必须保持稳定的关系

- [...]
- [...]

## 可以改变的变量

- [...]
- [...]

## 字体决策

- 策略：`ask | preserve | substitute | auto`
- 标题字体：
- 正文字体：
- 是否允许自动安装：
- 字体不可用时的回退：
- 详细决策：`transfer/font-decision.md`

## 必须替换的品牌元素

- [...]
- [...]

## 禁止走的捷径

- [...]
- [...]

## 常见失败模式

- [...]
- [...]

## 可用组件配方

- `recipes/...`

## 新组件创建约束

- 项目策略：`transfer/component-creation-policy.md`
- 评分卡：`evaluation/component-scorecard.md`
- 变更检查：`evaluation/change-checklist.md`

## 后续建议读取顺序

1. `rules/design-rules.json`
2. `transfer/brand-boundaries.md`
3. `transfer/font-decision.md`
4. 当前任务相关的组件配方
5. `evaluation/acceptance-tests.md`

## 必须执行的应用流程

1. 理解新产品。
2. 选择适用规则。
3. 编写 `DESIGN_PLAN.md`。
4. 实现页面。
5. 执行审美验收。
6. 修正失败项。

## 项目接入状态

- 模式：`capture | integrate | apply | audit | continue`
- Existing Design 接入策略：`not-integrated | augment | harmonize | migrate`
- 项目设计入口：`integration/authority-policy.md`
- 最终项目规则：`integration/resolved-rules.json`
- 未解决硬冲突：
- 项目入口文件：
- 渐进式改造计划：`transfer/retrofit-plan.md`

完成接入后，后续实现以 `integration/resolved-rules.json` 为准；本文件继续保存 Taste 来源，不覆盖 Existing Design 或冲突裁决。
