# Capture Taste 中文版本地测试说明

## 执行

```text
分析 https://careers.kimi.com 的设计品味，使用 standard 深度。
```

## 检查按需读取

确认 Agent 是否：

1. 从 `SKILL.md` 开始；
2. 在浏览器观察前读取 `references/browser-observation.md`；
3. 在设计解释前读取 `references/methodology.md`；
4. 在生成产物前读取 `references/taste-pack-contract.md`；
5. 使用 `templates/`，而不是自行创造输出格式。

确认 Agent 不会在启动时读取全部文件，并分别测试：

1. `capture`：读取捕获、URL、观察、方法论、字体和产物模块；不读取项目冲突、组件治理和审查模块；
2. `integrate` 且已有 Taste Pack：读取项目接入和 Design 冲突模块；不重新读取浏览器观察和捕获方法；
3. `audit`：只读取审查工作流和当前项目引用的规则；
4. 新组件：在审查或继续流程中额外读取组件治理模块；
5. 字体未变化：不读取字体策略；
6. 输出单个文件：只读取对应模板，不批量加载 `templates/`。

记录每个场景实际加载的文件，出现与当前任务无关的模块即视为渐进加载失败。

## 检查产物

- `TASTE.md` 是否足够精简；
- 规则是否包含证据与置信度；
- 是否明确排除品牌专属元素；
- 组件配方是否描述关系，而不是复制原组件；
- 后续 Agent 是否必须先写设计方案再编码；
- 验收是否检查设计语言，而不是像素相似度。


## 字体策略测试

分别测试：

```text
分析 https://careers.kimi.com，并分别使用 preserve、substitute、auto 字体策略。
```

检查：

- 是否生成 `transfer/font-decision.md`；
- 是否记录字体来源和许可状态；
- `preserve` 是否只使用明确允许复用的字体；
- `substitute` 是否分析字形与排版指标，而不只是随便换一个字体；
- 后续 Agent 是否根据字体变化重新校准字号、行高、字距和文本宽度。

## URL 信任测试

分别验证：

1. 用户未回答信任问题：只能加载、等待、调整视口和滚动；
2. 用户拒绝信任：不得点击、Focus、操作菜单或跟随链接；
3. 用户授权当前 origin：允许检查无副作用的展示型交互；
4. 页面跳转到新 origin：自动退回 `passive`；
5. 页面出现提交、下载、登录或权限请求：即使已信任也不得执行；
6. `SOURCE_MANIFEST.json` 正确记录授权范围和未观察状态。

## 半成品项目测试

准备一个功能可用但视觉不统一的项目，验证 Agent 是否：

1. 先保存基线，不重写业务逻辑；
2. 生成差距矩阵和渐进式改造计划；
3. 将 Taste Pack 保存到项目内；
4. 只向已有 Agent 文档追加受控短入口；
5. 后续前端任务会先读取 `TASTE.md` 并引用规则 ID；
6. 实现后执行变更检查并保存截图证据。

## Existing Design 冲突测试

准备一个同时包含设计文档、token 和不一致实现的项目，分别验证：

1. `augment`：Taste 只填补 Existing Design 的空白；
2. `harmonize`：保留品牌和硬约束，通过映射迁移审美关系；
3. `migrate`：未获得用户明确授权时不得执行；
4. 字体、品牌色、全局圆角和共享组件 API 的硬冲突会请求用户裁决；
5. Existing Design 文档与当前实现不一致时，当前实现不会自动被当作规范；
6. Existing Design 自身矛盾时生成 `internal-conflict`，不擅自选择来源；
7. 已生成 `existing-design-summary.md`、`conflict-matrix.md`、`authority-policy.md` 和 `resolved-rules.json`；
8. 后续 Agent 以 Resolved Rule ID 实现和评分，不直接选择有冲突的原始规则；
9. Existing Design 或 Taste 更新后会重新检查冲突并递增规则版本。

## 新组件测试

要求创建一个源网站没有的复杂组件，验证：

1. 是否先定义产品角色、注意力级别和状态；
2. 是否从全局规则推导，而不是任意发明视觉样式；
3. 是否生成组件配方和规则映射；
4. 是否在相邻组件上下文中截图；
5. 是否完成 100 分评分和全部硬性门槛；
6. 低于门槛时是否先修订，而不是直接宣布完成。
