# flightlessness 后续计划与维护

更新：2026-11-27。站点结构与实现入口见 [PROJECT_MAP.md](PROJECT_MAP.md)，操作规范见 [AGENTS.md](../AGENTS.md)。

## 后续计划与待验证

状态说明：候选、待决定、完善和暂缓均为计划或建议，不代表已授权实施；观察中和未覆盖不等于已通过。时间均为 UTC+8；提交、部署和浏览器验证时间分别记录。

| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;状态&nbsp;/&nbsp;优先级&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 事项与现状 | 处理方向 | 解决 / 核验时间 |
| :---: | --- | --- | --- |
| 已实现&nbsp;·&nbsp;待验证 | 复制文章链接、返回顶部、阅读进度条 | 公开文章详情页已添加；验证剪贴板及失败回退、滚动阈值、进度、浅深色、键盘及窄屏。 | — |
| 已实现&nbsp;·&nbsp;待验证 | 面包屑导航、分类和标签下划线调整 | 核验各级链接、项目子路径、404、手机换行及最终计算样式。 | — |
| 高&nbsp;·&nbsp;候选 | 时间归档（Archives） | 按年/月组织文章，设计入口和隐藏文章规则。 | — |
| 高&nbsp;·&nbsp;候选 | 随机文章（Random Post） | 随机打开公开文章，排除隐藏及草稿。 | — |
| 暂缓&nbsp;·&nbsp;候选 | 站内搜索（Search） | 标题、正文、分类和标签索引；排除隐藏正文，文章增多后再设计。 | — |
| 暂缓&nbsp;·&nbsp;候选 | 相关文章（Related Posts） | 按共同标签推荐公开文章，与前后篇导航协调。 | — |
| 中&nbsp;·&nbsp;候选 | Featured（精选文章） | 已有 Weight > 0 的 Featured 标记；规划精选规则、排序和显示方式，排除隐藏文章。 | — |
| 中&nbsp;·&nbsp;候选 | Series（文章系列） | 新增 series 分类维度、系列总览及系列内顺序和导航；与普通分类、标签区分。 | — |
| 待决定 | 个人头像 Avatar / Gravatar / 自定义头像 CDN | Paper 头像入口未使用；三种表述归并为一项，选择本地或远程头像及隐私、加载策略。 | — |
| 待决定 | 单色深色模式切换图标 | 主题 monoDarkIcon 未启用；比较现有图标与单色样式。 | — |
| 中&nbsp;·&nbsp;候选 | 自定义 Favicon 与 Apple Touch Icon | 设计浏览器标签页及 iOS 主屏幕图标，核验项目子路径和缓存。 | — |
| 中&nbsp;·&nbsp;候选 | Collapse 折叠内容 / 写在这首诗之后 | 评估 Paper 折叠 shortcode，在诗歌正文之后放创作背景、后记或延伸材料；默认折叠，不改正文。 | — |
| 低&nbsp;·&nbsp;候选 | Mermaid 图表 | 已有主题入口，按文章需要启用；核验渲染和深色模式。 | — |
| 中&nbsp;·&nbsp;候选 | 引用、脚注及诗后链接规范 | 当前《蓝星庆典》《纪念碑谷 2》《迟到》《酸奶坏了》在正文后用 Markdown 横线与行内链接 [URL](URL)；规划引用说明、脚注、来源链接文字与展示风格，不直接改旧文。 | — |
| 中&nbsp;·&nbsp;完善 | SEO 页面描述 | 已有基础支持；完善首页、文章描述及中英版本。 | — |
| 低&nbsp;·&nbsp;完善 | Open Graph 分享卡片、Twitter Cards | 已支持；按需设计分享图和摘要、核验元数据。 | — |
| 低&nbsp;·&nbsp;完善 | Schema 结构化数据、Canonical 标准网址 | 已支持；未来双语和模板改动时核验。 | — |
| 低&nbsp;·&nbsp;完善 | RSS 订阅 | 已使用；评估订阅体验、双语输出，维持当前隐藏规则。 | — |
| 待决定 | Google Analytics | 主题预留，未启用；先决定是否需要统计及隐私策略。 | — |
| 低&nbsp;·&nbsp;候选 | 自定义版权声明 | 未配置；确认文案、位置及授权含义。 | — |
| 低&nbsp;·&nbsp;候选 | 文章独立作者署名 | 模板已有 author 支持；按需设置 Front Matter 与显示规则。 | — |
| 中&nbsp;·&nbsp;规划中 | 多语言界面翻译 | Paper 已有 21 种界面翻译资源（此前审计记录）；并入中英双语阅读设计，不等同于文章语言切换。 | — |
| 暂缓&nbsp;·&nbsp;候选 | RTL 从右向左排版 | 主题支持，暂无需求；新增相关语言时再验证。 | — |
| 低&nbsp;·&nbsp;候选 | 文章目录 TOC | 长篇文章按标题生成目录，短诗不显示。 | — |
| 低&nbsp;·&nbsp;候选 | 阅读时长 | 估算中文及英文阅读时间，短诗是否展示待定。 | — |
| 中&nbsp;·&nbsp;候选 | 图片画廊、点击放大 | 设计文章图片组织、响应式画廊、放大与键盘关闭。 | — |
| 待决定 | 阅读量统计 | 需额外统计服务或实现；与 Analytics 需求协调。 | — |
| 暂缓&nbsp;·&nbsp;候选 | 独立访客留言板 | 需要额外服务或实现；评估审核、隐私及维护。 | — |
| 暂缓&nbsp;·&nbsp;候选 | 音乐播放器 | 需要额外实现；评估音源授权、播放控制与移动端体验。 | — |
| 观察中 | 前轮 WebKit 390px 深色首页点击一次超时，随后20次独立复测未重现；本轮主矩阵及同组合20次点击亦未重现。 | 未针对该偶发项修改代码；保留原始截图和超时记录，继续观察，不标记已修复。 | 2026-11-27 05:38（复测观察） |
| 未覆盖 | iOS 真机 Safari、触摸与动态工具栏；未提供历史设计图或截图基线。 | Playwright WebKit/视口测试不替代真机或历史逐像素验收，保持未验证。 | — |
| 中&nbsp;/&nbsp;规划中 | 中英双语阅读：界面默认 `locale: en-US`，绝大部分 Post 为中文，HTML `lang` 与正文尚不一致；尚未提供双语切换或翻译自动化。 | 每篇文章发布前由 AI 翻译和润色英文版，经作者确认后与中文原文一同发布；详情页提供中英切换。设计 Hugo multilingual 目录及 Front Matter、翻译关联、默认与英文 URL、各语言 `lang`、`hreflang`、sitemap、RSS、分类/标签翻译、未翻译文章回退及隐藏规则，保留现有中文 URL。 | — |

## 已完成与已决定

| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;状态&nbsp;/&nbsp;优先级&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 事项与现状 | 处理方向 / 证据 | 解决 / 核验时间 |
| :---: | --- | --- | --- |
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
