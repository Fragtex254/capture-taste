---
name: capture-taste
description: 从公开 URL 捕获可迁移的设计品味并生成平台中立的 Taste Pack；也可将其接入已有或半成品前端项目，解决 Existing Design 与外部 Taste 的冲突，持续约束页面改造、新组件创建、评分和审查。用于风格提取、视觉优化、Taste 接入、设计冲突处理和既有 Taste 审计；不用于像素级复刻、复制品牌身份或未经授权遍历交互。
---

# Capture Taste

把本文件作为轻量路由器。先判断任务类型，只读取当前阶段需要的模块；不要在开始时加载全部 `references/` 或 `templates/`。

核心协议使用 Markdown 和 JSON，不依赖某个平台的斜杠命令、参数占位符或工具名称。

## 选择模式

- `capture`：分析 URL，生成 Taste Pack，不修改产品。
- `integrate`：将 Taste 接入已有项目，解决现有 Design 冲突并生成改造计划。
- `apply`：先完成 `capture → integrate`，再按用户要求修改项目。
- `audit`：用项目已有规则审查页面、变更或组件。
- `continue`：在已有设计权威下继续执行前端任务。

未指定时按用户目标自动判断；默认 `capture`。只有用户明确要求实施修改时才能使用 `apply`。

## 按需读取路由

不要预读未命中的模块。

| 当前任务或阶段 | 此时读取 | 不需要读取 |
|---|---|---|
| 需要访问 URL | `references/url-trust.md` | 项目接入、组件治理 |
| 开始捕获设计 | `references/capture-workflow.md` | 项目冲突模块 |
| 开始浏览器观察 | `references/browser-observation.md` | 产物契约 |
| 开始提炼设计规则 | `references/methodology.md` | 项目接入模块 |
| 处理字体 | `references/font-policy.md` | 组件治理 |
| 即将生成 Taste Pack | `references/taste-pack-contract.md` | 不相关模板 |
| 接入已有项目 | `references/project-integration.md` 与 `references/design-conflict-resolution.md` | 浏览器观察；除非同时 capture |
| 创建源网站没有的新组件 | `references/component-governance.md` | 捕获方法论；除非需要重新捕获 |
| 审查或继续已有项目 | `references/audit-workflow.md` | URL、字体和捕获模块；除非任务涉及它们 |

模板也按需读取：只打开 `templates/` 中当前要生成的那个文件，不批量加载模板目录。

## 不可省略的门槛

### URL 授权

访问 URL 前必须读取 `references/url-trust.md` 并确认信任范围。未获得 `trusted-interactive` 授权时，只进行静态和被动观察。URL 信任不自动授权登录、提交、购买、下载、发送消息或其他外部状态变更。

### 设计权威

Taste 不自动高于已有 Design。已有项目默认使用 `harmonize`；只有用户明确授权替换视觉系统时使用 `migrate`。完成接入后，以 `integration/authority-policy.md` 为项目入口，以 `integration/resolved-rules.json` 为实现和评分规则。不得实施仍未裁决的相关硬冲突。

### 品牌与许可

不得迁移 Logo、品牌名称、原始文案、专属素材、商标化图形或其他品牌身份。不得把网页可加载字体等同于允许安装、商用或再分发。

### 实现边界

`capture` 阶段不得生成产品实现代码。现有项目默认渐进改造并保留产品行为，不因视觉问题擅自重写业务逻辑。

## 最小执行协议

1. 确定模式、目标 URL、项目位置、深度和字体策略。
2. 按路由表读取当前模块并执行；进入新阶段时再读取下一模块。
3. 为观察、原始规则、Existing Design 和 Resolved Rules 保留独立来源 ID。
4. 将完整规则保存在 Taste Pack；Agent 指令文档只添加受控短入口，不复制规则正文。
5. 实现前声明采用的 Resolved Rule ID，实施后运行对应检查和评分。
6. 报告授权范围、规则来源、未解决冲突、失败项、已知限制和产物路径。

如果模块文件不存在或无法读取，停止该模块涉及的操作并报告缺失；不要凭常识重建安全门槛、权威策略或评分规则。
