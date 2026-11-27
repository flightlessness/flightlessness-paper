# flightlessness 后续计划与维护

更新：2026-11-27。站点结构与实现入口见 [PROJECT_MAP.md](PROJECT_MAP.md)，操作规范见 [AGENTS.md](../AGENTS.md)。

## 后续计划与待验证

状态说明：观察中和未覆盖不等于已通过。时间均为 UTC+8；提交、部署和浏览器验证时间分别记录。

| 状态&nbsp;/&nbsp;优先级&nbsp;&nbsp;&nbsp;&nbsp; | 事项与现状 | 处理方向 | 解决 / 核验时间 |
| --- | --- | --- | --- |
| 已实现 · 待验证 | 复制文章链接、返回顶部、阅读进度条 | 公开文章详情页已添加；验证剪贴板及失败回退、滚动阈值、进度、浅深色、键盘及窄屏。 | — |
| 已实现 · 待验证 | 面包屑导航、分类和标签下划线调整 | 核验各级链接、项目子路径、404、手机换行及最终计算样式。 | — |
| 高 · 候选 | 时间归档（Archives） | 按年/月组织文章，设计入口和隐藏文章规则。 | — |
| 高 · 候选 | 随机文章（Random Post） | 随机打开公开文章，排除隐藏及草稿。 | — |
| 暂缓 · 候选 | 站内搜索（Search） | 标题、正文、分类和标签索引；排除隐藏正文，文章增多后再设计。 | — |
| 暂缓 · 候选 | 相关文章（Related Posts） | 按共同标签推荐公开文章，与前后篇导航协调。 | — |
| 观察中 | 前轮 WebKit 390px 深色首页点击一次超时，随后20次独立复测未重现；本轮主矩阵及同组合20次点击亦未重现。 | 未针对该偶发项修改代码；保留原始截图和超时记录，继续观察，不标记已修复。 | 2026-11-27 05:38（复测观察） |
| 未覆盖 | iOS 真机 Safari、触摸与动态工具栏；未提供历史设计图或截图基线。 | Playwright WebKit/视口测试不替代真机或历史逐像素验收，保持未验证。 | — |
| 中&nbsp;/&nbsp;规划中 | 中英双语阅读：界面默认 `locale: en-US`，绝大部分 Post 为中文，HTML `lang` 与正文尚不一致；尚未提供双语切换或翻译自动化。 | 每篇文章发布前由 AI 翻译和润色英文版，经作者确认后与中文原文一同发布；详情页提供中英切换。设计 Hugo multilingual 目录及 Front Matter、翻译关联、默认与英文 URL、各语言 `lang`、`hreflang`、sitemap、RSS、分类/标签翻译、未翻译文章回退及隐藏规则，保留现有中文 URL。 | — |

## 已完成与已决定

| 状态&nbsp;/&nbsp;优先级&nbsp;&nbsp;&nbsp;&nbsp; | 事项与现状 | 处理方向 / 证据 | 解决 / 核验时间 |
| --- | --- | --- | --- |
| 已解决&nbsp;/&nbsp;已核验 | [378f16e](https://github.com/flightlessness/flightlessness-paper/commit/378f16eaf3599886eefde7e6f6a9617744506684) 补齐网格、隔离关闭菜单焦点、支持 Escape 与焦点返回；此前待验证的浏览器回归和 CSS 事项已合并核验。 | 本地 Hugo Extended 0.169.0 构建成功，Paper仍锁定f7ed52a1da04；本地4568/4568、线上6184/6184断言通过：Chromium/WebKit × 8宽度 × 浅深色，含640px单/双列16px实际间距、1023↔1024px菜单状态、Back/提示/键盘、首页字体与点击、分页/文章首尾、隐藏/RSS/sitemap、CSS SRI及请求。0 Console/请求异常；51个生产文件字节一致。[部署 45898987742](https://github.com/flightlessness/flightlessness-paper/actions/runs/45898987742)成功（05:34:27），Playwright独立验证。证据在仓库外包 `flightlessness-fix-2026-11-27` 的 local/online summary、artifacts及fix-results截图；测试脚本/依赖未入仓库。 | 2026-11-27 05:38（浏览器完成；修复已部署） |
| 已解决 | 404 页面：Paper 原生模板继承本地页头与 Back；作者确认问题已解决。 | 保持现有模板；已纳入 2026-11-27 双内核线上回归，404 导航与 Back 通过。 | 2026-11-27（作者确认） |
| 已决定 | 首页 name 与 bio 保持现状，暂不解除模板中的显示绑定。 | 不修改 `hugo.yaml` 或首页模板。 | 2026-11-27（作者决定） |
| 已核验 | 作者提供 Pages 与 Environment 设置：GitHub Actions、默认域名、强制 HTTPS、公开站点；`github-pages` 仅允许 main、0 tags、无 secrets/variables，未见审批或等待规则。管理员绕过选项勾选状态未确认。 | 保持现状；新增域名或权限需求时再检查。 | 2026-11-27（作者核验） |
| 已核验 | 作者确认微博、B 站、腾讯游戏三个正文外链有效；此前网络工具未能读取。 | 保留原链接；未来按需复查。 | 2026-11-27（此前作者确认） |
| 已解决 | 三个旧导航 SVG 已清理；作者明确保留 Hello, Hugo，维持隐藏文章规则。 | 不删除测试文章。 | 2026-11-27（确认保留；SVG 11-26 清理） |
| 已解决 | CI 修复 `961ea72`：checkout 完整历史、configure-pages v6、upload-pages-artifact v5；[Actions #45850622617](https://github.com/flightlessness/flightlessness-paper/actions/runs/45850622617) 成功，日志确认 fetch-depth 0、Go 缓存命中、Node.js 20 警告消失。 | 固定 Hugo/Go/Paper 版本，按需升级 Actions。 | 2026-11-26 23:35（修复提交） |
| 已解决 | Paper 版本固定为 `f7ed52a1da04`，CI 停止自动升级，`go.sum` 已跟踪。 | 主题升级单独处理并验证生成 CSS 和模板差异。 | 2026-11-26 22:36（校验提交） |
| 已解决 | `languageCode` 已迁移为 `locale: en-US`，生产构建成功。 | 英文 UI 与中文文章现状保持；正式双语另行设计。 | 2026-11-26 22:33（修复提交） |
| 已解决 | 5 篇隐藏文章仍无详情页，分类页取消失效链接、前后篇跳过隐藏、sitemap 排除对应 URL，保留标题与 RSS。 | 维持网站不展示正文、仓库和 RSS 可以公开的约定。 | 2026-11-26 22:24（修复提交） |
