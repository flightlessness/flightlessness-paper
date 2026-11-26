# flightlessness 后续计划与维护

更新：2026-11-27。站点结构与实现入口见 [PROJECT_MAP.md](PROJECT_MAP.md)，操作规范见 [AGENTS.md](../AGENTS.md)。

## 后续计划与未实现功能

- **中英双语阅读（规划中）**：网站界面以英文为默认（当前配置 `locale: en-US`），但绝大部分现有 Post 为中文；当前 HTML 文档语言声明与中文正文尚不一致，未来应为各语言页面正确标记 `lang`。未来每篇文章发布前由 AI 翻译和润色英文版，经作者确认，再一同发布中文原文和英文译文；文章详情页提供中英切换，并保持相互对应。设计时确定 Hugo multilingual 目录/Front Matter、默认 URL 与英文 URL、`hreflang`、sitemap、RSS、分类/标签翻译、未翻译文章回退、隐藏文章继承规则，确保现有中文文章 URL 不被破坏。当前仅改成英文 `locale`，**尚未提供双语切换或翻译自动化**。
- **404 导航体验（可选）**：现有 404 含 Back 的历史记录待实际浏览器复核；暂不新增模板。
- **已决定**：保留 `Hello, Hugo` 及现有隐藏规则；三个旧导航 SVG 已清理。首页 name 与 bio 暂不改动。

## 风险与维护重点

状态说明：已解决表示对应修复已实施并有构建或其他验证依据；待验证表示实现已提交，但仍需检查实际输出或交互；高、中、低表示尚未完成事项的维护优先级。

| 优先级 | 发现与可复验的证据 | 处理方向 |
| --- | --- | --- |
| 已解决 | 5 篇隐藏文章仍无详情页，分类页取消失效链接、前后篇跳过隐藏、sitemap 排除对应 URL，保留标题与 RSS。 | 维持网站不展示正文、仓库和 RSS 可以公开的约定。 |
| 已解决 | Paper 版本固定为 `f7ed52a1da04`，CI 停止自动升级，`go.sum` 已跟踪。 | 主题升级单独处理并验证生成 CSS 和模板差异。 |
| 已解决 | `languageCode` 已迁移为 `locale: en-US`，生产构建成功。 | 英文 UI 与中文文章现状保持；正式双语另行设计。 |
| 待视觉验证 | 本地五个补充工具类中 `gap-8` 暂无调用，`py-4` 优先级已修复。历史产物校验见 Git 记录，本轮未重新下载核验。 | 浏览器核验分类单/双列及间距。 |
| 待完整视觉验证 | 作者已确认 Back/提示 CSS 冲突修复；最新首页分类、日期与点击区域调整已构建部署成功（[Actions #45893625134](https://github.com/flightlessness/flightlessness-paper/actions/runs/45893625134)）。 | 实测桌面/移动端、浅深色、计算样式、Back、提示、键盘、分类点击、文章覆盖层、分页、隐藏输出及资源请求；本轮未完成浏览器回归。 |
| 已解决 | CI 修复 `961ea72`：checkout 完整历史、configure-pages v6、upload-pages-artifact v5；[Actions #45850622617](https://github.com/flightlessness/flightlessness-paper/actions/runs/45850622617) 成功，日志确认 fetch-depth 0、Go 缓存命中、Node.js 20 警告消失。 | 固定 Hugo/Go/Paper 版本，按需升级 Actions。 |
| 中 | 正式双语文章、逐篇 AI 翻译及语言切换尚未实现。 | 保留现有 URL，另行设计语言标记、翻译关联、切换、RSS、sitemap 和隐藏规则。 |
| 低 | 生产 404.html 已确认含 Back；尚未实测返回行为。 | 按需核验 404 交互，不另改模板。 |
| 已解决 | 三个旧导航 SVG 已清理；作者明确保留 Hello, Hugo，维持隐藏文章规则。 | 不删除测试文章。 |
| 已核验 | 作者提供 Pages 与 Environment 设置：GitHub Actions、默认域名、强制 HTTPS、公开站点；`github-pages` 仅允许 main、0 tags、无 secrets/variables，未见审批或等待规则。管理员绕过选项勾选状态未确认。 | 保持现状；新增域名或权限需求时再检查。 |
| 已核验 | 作者确认微博、B 站、腾讯游戏三个正文外链有效；此前网络工具未能读取。 | 保留原链接；未来按需复查。 |
