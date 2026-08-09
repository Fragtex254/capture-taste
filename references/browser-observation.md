# 浏览器观察规范

## 目录

- [必须检查的视口](#必须检查的视口)
- [截图要求](#截图要求)
- [交互扫描](#交互扫描)
- [时间状态](#时间状态)
- [代表性提取对象](#代表性提取对象)
- [证据格式](#证据格式)

开始前必须读取 `references/url-trust.md`，并根据 `passive` 或 `trusted-interactive` 授权决定观察范围。本文列出的交互检查项不是自动授权。

## 必须检查的视口

- 桌面端：`1440×900`
- 平板端：`768×1024`
- 移动端：`390×844`

## 截图要求

每个已分析页面都应包含：

- 完整页面截图；
- 首屏截图；
- 每个主要区块截图；
- 代表性的移动端截图；
- 关键交互状态截图。

## 交互扫描

在 `passive` 模式下，只记录通过加载、等待、调整视口和滚动可以确认的状态。将其他状态标为 `not_observed_due_to_authorization`。

只有处于 `trusted-interactive` 且操作属于无副作用的展示型交互时，才检查：

检查：

- 导航；
- 按钮和链接；
- 卡片；
- Tab 和 Accordion；
- 菜单；
- 表单；
- 轮播；
- Sticky 区域；
- 滚动驱动区域；
- 跟随指针的元素。

不要在判断交互模型之前直接点击。

先观察它是否由滚动驱动。

交互触发分类：

- 点击；
- Hover；
- Focus；
- 滚动；
- 时间；
- 指针位置；
- 视口进入；
- 混合。

## 时间状态

在相关场景下观察：

- 初始加载；
- 加载后约 500ms；
- 加载后约 1500ms；
- 25%、50%、75% 滚动位置；
- 元素进入视口；
- 元素完全可见；
- 元素离开视口。

## 代表性提取对象

优先提取：

- 页面容器；
- 导航；
- Hero；
- 展示标题；
- 区块标题；
- 正文；
- 标签；
- 主要行动；
- 次要行动；
- 卡片；
- 媒体容器；
- 分隔线；
- 覆盖层；
- Footer；
- 重复出现的装饰元素。

提取：

- 字体；
- 色彩；
- 间距和布局；
- 几何与材质；
- 动效；
- 响应式变化。

不要无差别导出所有计算样式。

## 证据格式

每条观察建议使用：

```json
{
  "id": "obs-home-hero-title-desktop-initial",
  "location": "homepage:hero:title",
  "page_url": "https://example.com/",
  "viewport": "desktop",
  "state": "initial",
  "observation_status": "observed",
  "evidence_file": "evidence/home/desktop/hero-initial.png",
  "measurement_method": "computed-style",
  "observation": "标题占据两行，宽度约为内容区域的一半。",
  "measurements": {
    "fontSize": "88px",
    "lineHeight": "0.96",
    "maxWidth": "720px"
  },
  "interpretation": "首屏保护了一个具有统治力的阅读焦点。",
  "confidence": 0.91
}
```

事实和解释必须明确区分。

规则文件使用 `id` 引用观察，不使用无法定位的笼统字符串。未经授权或工具能力不足时，将 `observation_status` 写成 `not_observed_due_to_authorization` 或 `not_observed_due_to_tooling`，并说明缺失影响。
