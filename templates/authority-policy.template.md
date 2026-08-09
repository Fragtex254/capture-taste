# 项目设计权威策略

## 状态

- 接入策略：`augment | harmonize | migrate`
- 策略确认者：
- 确认时间：
- Resolved Rules 版本：
- 未解决硬冲突数量：

## 权威顺序

1. 用户对当前任务的明确决定；
2. 法律、字体许可、安全、可访问性和不可改变的产品行为；
3. Existing Design 的品牌、系统级和硬约束；
4. `resolved-rules.json` 中已确认的项目规则；
5. 可迁移的 Taste 规则；
6. 当前实现；
7. Agent 自行偏好。

## 规范来源

- Existing Design 摘要：`existing-design-summary.md`
- 冲突矩阵：`conflict-matrix.md`
- 已解决规则：`resolved-rules.json`
- Taste 来源：`../TASTE.md`
- 其他原始 Design 文档：

## 策略解释

- 必须保留：
- 允许迁移：
- 需要映射：
- 已明确替换：
- 不在本次范围：

## 未解决冲突

- [...]

## 后续 Agent 指令

1. 实现和审查以 `resolved-rules.json` 为直接规则来源。
2. 根据来源引用读取相关 Existing Design 和 `TASTE.md` 证据。
3. 不得自行解决标记为 `pending` 或 `blocked` 的硬冲突。
4. 不得为了让当前实现通过而静默修改权威层级。
5. 规则来源更新后，重新运行冲突检查并递增版本。
