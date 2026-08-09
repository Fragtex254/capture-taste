# Taste 审查与继续工作流

只在 `audit` 或 `continue` 模式读取本文件。

## 1. 确定设计入口

按以下顺序定位项目规范：

1. 如果存在 `integration/authority-policy.md`，先读取它；
2. 按权威策略读取 `integration/resolved-rules.json`；
3. 只读取当前任务引用的 Existing Design、Taste 证据和组件配方；
4. 如果项目未接入 Existing Design，读取 `TASTE.md` 和当前任务需要的规则；
5. 如果同时存在 Existing Design 和 Taste、但没有接入产物，先切换到 `integrate`，不要自行决定优先级。

不要批量读取整个 Taste Pack。

## 2. 确定审查范围

记录：

- 页面、组件或变更；
- 必须保持的产品行为；
- 适用的 Resolved Rule ID；
- 相关硬性门槛和例外；
- 需要检查的视口与状态；
- 未解决冲突是否影响当前任务。

如果相关硬冲突仍为 `pending` 或 `blocked`，可以审查不冲突部分，但不得实现或通过受影响部分。

## 3. 选择附加模块

- 创建新组件：此时读取 `references/component-governance.md`。
- 改变字体：此时读取 `references/font-policy.md`。
- 重新观察源 URL：返回 `capture`，并在访问前读取 `references/url-trust.md`。
- 只修改已有组件：不读取上述模块，直接使用项目规则和变更检查。

## 4. 执行前检查

使用当前项目的 `evaluation/change-checklist.md`，只读取与变更相关的规则。实现计划列出 Resolved Rule ID、来源、允许变化、功能约束和有意例外。

`audit` 只报告发现，不修改实现。`continue` 只有在用户要求修改时才实施。

## 5. 证据与判定

根据任务风险获取桌面、移动和必要状态截图；影响平板布局时增加平板。对每个发现记录：

- 规则 ID；
- 视觉或实现证据；
- 影响范围；
- 严重度；
- 修订建议；
- `pass | revise | reject | unverified`。

新组件还必须完成组件评分卡。硬性门槛失败不能被平均分抵消。

## 6. 完成报告

报告设计入口、接入策略、审查范围、采用的规则、通过项、失败项、未验证状态、未解决冲突、完成的修订、剩余限制和证据路径。

不得为了让当前实现通过而静默修改 Taste、Existing Design、权威层级或评分标准。
