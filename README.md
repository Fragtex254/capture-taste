# Capture Taste

版本：`1.0.0` · 许可证：[MIT](LICENSE)

这是一个平台中立的网站设计品味提取与治理 Skill。

输入任意公开网站 URL，输出可供后续 AI Coding Agent 使用的 Taste Pack。

它不会复刻网站，也不会生成前端代码。

核心协议只使用 Markdown 和 JSON，不依赖 `$ARGUMENTS`、斜杠命令或某个 Agent 的专属工具名。不同 Agent 可以直接阅读 `SKILL.md`，也可以通过各自项目指令文件中的短入口引用生成的 `TASTE.md`。

## 渐进式加载

`SKILL.md` 只负责识别模式和路由，不要求一次读取全部内容。复杂能力拆成平台中立的按需模块，而不是依赖特定 Agent 才能发现的嵌套子 Skill：

- 捕获 URL 时才读取 `capture-workflow.md`、URL 授权和观察模块；
- 接入已有项目时才读取项目接入和 Design 冲突模块；
- 创建新组件时才读取组件治理模块；
- 审查或继续现有项目时才读取 `audit-workflow.md`；
- 字体、产物契约和模板只在对应阶段读取。

所有模块都由根级 `SKILL.md` 直接链接，因此不依赖某个平台的嵌套 Skill 发现机制。

目录：

- `SKILL.md`：主调度逻辑；
- `references/`：分析方法、浏览器观察规范、产物约定；
- `templates/`：Taste Pack、设计规则、组件配方、设计方案和验收模板。

安装：

```bash
git clone https://github.com/Fragtex254/capture-taste.git
```

将克隆目录注册为当前 Agent 可读取的 Skill，或让 Agent 直接从 `SKILL.md` 开始。平台不支持 Skill 注册时，也可以把仓库作为项目上下文提供给 Agent。

请求示例：

```text
分析 https://careers.kimi.com 的设计品味，使用 standard 深度。
```

在完整检查菜单、Tab、Focus、点击等交互前，Skill 会要求用户明确确认是否信任当前 URL。未授权时只进行静态和被动观察。

对于已有或半成品项目，可以请求：

```text
捕获 https://example.com 的设计品味，把 Taste Pack 接入当前项目，并按渐进式计划优化现有页面。
```

后续 Agent 通过项目指令文档中的短入口读取设计规范：未接入 Existing Design 时从 `TASTE.md` 开始；完成接入后从 `integration/authority-policy.md` 和 `resolved-rules.json` 开始。新组件必须经过规则映射、视觉证据、100 分评分和硬性门槛审查。

如果项目已经有 Design 文档或设计系统，Taste 不会自动覆盖它。Skill 默认使用 `harmonize` 策略，生成 Existing Design 摘要、冲突矩阵、权威策略和 `resolved-rules.json`。后续实现以已解决规则为准；使用 Taste 替换现有视觉系统的 `migrate` 策略必须由用户明确授权。


## 字体策略

支持策略：

```text
--font-policy ask|preserve|substitute|auto
```

默认使用 `auto`。用户明确要求字体选择时，可以使用 `ask`；无法交互时退化为 `auto`。

## 安全边界

- 在完整检查交互前确认用户是否信任当前 URL 和页面范围；
- 未授权时只执行静态与被动观察；
- URL 信任不自动授权登录、提交、支付、下载或改变外部状态；
- 不复制源网站品牌身份或许可不明的字体文件。

## 开发与验证

测试场景见 `TEST_PLAN.md`。发布前使用兼容的 Skill 校验器检查 `SKILL.md`，并验证 `templates/` 中的 JSON 文件。

## License

MIT © 2026 hcds
