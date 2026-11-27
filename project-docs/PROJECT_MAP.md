# flightlessness-paper 项目地图

审计范围为 2026-11-26 读取的 `main`，提交 `af477a9dbc7e5556b7a4f81be139bda149d5d1e9`。递归目录结果完整，26 个跟踪文件均已读取，包括 12 篇文章全文、3 个 SVG、站点配置、模板和部署脚本。另读了最近一次部署的 build 和 deploy 日志，以及该部署解析到的 Paper 模块的关键模板、CSS 入口和工具配置。此次分析保持 GitHub 仓库只读。

[仓库快照](https://github.com/flightlessness/flightlessness-paper/tree/af477a9dbc7e5556b7a4f81be139bda149d5d1e9) · [部署 #62](https://github.com/flightlessness/flightlessness-paper/actions/runs/44914085196) · [线上站点](https://flightlessness.github.io/flightlessness-paper/)

## 项目管理文档

根目录的 [AGENTS.md](../AGENTS.md) 记录 AI 操作规范和 Git 流程。本文件记录已有功能、文件关系及实现入口。历史审计快照保留作参考；当前实现更新至 2026-11-27 的 `378f16e`，后续计划与维护见 [ROADMAP.md](ROADMAP.md)。动手前对照 GitHub `main` 最新源码。

## 当前改动与最近新增

| 状态 | 内容 |
| --- | --- |
| 阅读辅助 · 待验证 | 公开 Post 的 `single.html` 添加日期旁复制链接、页面顶部 2px 阅读进度条、滚动 300px 后显示返回顶部；`custom.css` 负责样式。剪贴板失败提供手动复制，减少动态效果偏好下即时返回顶部；About、隐藏文章及列表不添加。待构建及浏览器验证。 |
| 面包屑导航 · 待验证 | `header.html` 在非首页 Back 右侧生成 home / 上级 / 当前 URL 路径，文章使用 slug，404 当前项不可点击；`custom.css` 设置 14px 灰色、24px 间距、悬停/焦点下划线和窄屏换行。保留 Back 行为与实际 URL；待构建和浏览器核验。 |
| 已完成 · 网格与菜单定向修复 | [378f16e](https://github.com/flightlessness/flightlessness-paper/commit/378f16eaf3599886eefde7e6f6a9617744506684)：补齐 `.grid`，恢复 Categories、Tags 和词条页 <640px 单列、≥640px 双列及 16px 行列间距；关闭的移动导航由 `inert`/`aria-hidden` 隔离，按 64rem 断点同步桌面可访问性；Escape 关闭并将焦点返回 Menu，`aria-expanded` 同步。保留无边框、字号、下划线与对齐；Paper 未升级。[部署 45898987742](https://github.com/flightlessness/flightlessness-paper/actions/runs/45898987742)构建及部署成功（2026-11-27 05:34:27，UTC+8）。 |
| 已核验 · 完整浏览器回归与 CSS | 2026-11-27 05:38（UTC+8）完成 Chromium 159.0.8154.6 / WebKit 27.2 × 375/390/639/640/768/1023/1024/1440px × 浅深色。Hugo Extended 0.169.0 本地构建成功，本地 4568/4568、线上 6184/6184 断言通过；覆盖计算样式/优先级、资源与 CSS SRI、主题刷新保留、导航/提示/键盘/Back、首页命中区域、分页、公开文章前后篇与首尾 Home、隐藏列表/404/RSS/sitemap、溢出/重叠。0 Console/请求异常；51 个线上发布文件与本地生产构建逐字节一致。构建成功与浏览器通过分别核验。 |
| 首页分类与日期 · 已验证 | 首页标题 24px、日期 14px、分类 18px；标题/日期覆盖层限定左列，与分类相隔 24px，分类实际点击不被覆盖；隐藏文章无详情链接，Posts 保持原行为。最初实现 `590c847`，已纳入本轮完整矩阵验证。 |
| 分类与标签 · 已验证 | 总览词条名称及篇数取消下划线；针对作者反馈的残留下划线，使用 site-term-link 局部覆盖 Paper 四 ID 权重的 Typography 链接规则（待线上复验）；具体标签页文章标题和日期无下划线（本次修改待浏览器验证），分类详情页不变；无边框、名称 18px、篇数/词条日期保持原实际 16px、内边距 16px 20px；网格及真实间距已验证。`py-4`、Back 和提示的局部高优先级覆盖实际生效；`gap-8` 仍无调用，未作无关清理。 |
| 导航及文章 · 已验证 | 顺序 Home、Categories、Tags、About、GitHub、RSS；手机六宫格居中、桌面图标与键盘提示通过。Back 20px/400、浅色 #999/深色 #aaa；桌面提示 14px、10px 16px、延迟 150ms。全部公开文章的前后篇跳过隐藏文章，序列首尾 Home 返回首页；404 页头/Back 已复核。 |
| 继续观察 / 未覆盖 | WebKit 390px 深色首页曾偶发点击超时；本轮主矩阵及同组合 20 次独立点击未重现，未针对其修改代码、不标记已修复。iOS 真机 Safari、触摸/动态工具栏及无历史截图基线的逐像素验收仍未覆盖，见 ROADMAP。 |
| 导航栏调整 | [`90cdaaa`](https://github.com/flightlessness/flightlessness-paper/commit/90cdaaad781967e2775109093ce1f8b49475c5dc)：自定义图标独立于 RSS，GitHub 移至 Tags 与 RSS 之间，深色反色仅用于原生背景图标。 |
| 已完成 · 隐藏文章 | 隐藏文章导航修复：分类词条页保留标题但取消不可达链接；公开文章的前后篇跳过隐藏文章；5 篇隐藏文章通过 Front Matter 的 `sitemap.disable: true` 不再列入 sitemap。涉及 `layouts/_default/{taxonomy,single}.html` 与 5 篇隐藏文章的元数据；RSS、正文和首页/Posts 展示保持不变。提交 [`f6b3584`](https://github.com/flightlessness/flightlessness-paper/commit/f6b35846f64d055d431c318e8f18e3f1b425d9f5)，Actions [#45838661569](https://github.com/flightlessness/flightlessness-paper/actions/runs/45838661569) 构建及部署成功。 |
| 本轮完成 | 将 Paper 固定至 `f7ed52a1da04` 并提交双校验项 `go.sum`，CI 停止自动升级；为本地分类与页头补充 CSS；改善键盘操作、状态 ARIA 与图标绝对路径；将 `languageCode` 迁移为 `locale: en-US`。变更见 [`206a31c`](https://github.com/flightlessness/flightlessness-paper/commit/206a31c6071dce0e5d17e3e4e7a089cb31c79a10) 及后续修复，生产构建 [#45840480016](https://github.com/flightlessness/flightlessness-paper/actions/runs/45840480016) 已成功。 |
| 最近完成 | 曾将项目管理文档精简为两份，并在 README 集中链接。详见 [`f173548`](https://github.com/flightlessness/flightlessness-paper/commit/f17354811cf09790a67cca3f2110d7c7c93594fe)。 |
| 最近的站点变更 | 调整《忏悔录 2》的发布时间。详见 [`af477a9`](https://github.com/flightlessness/flightlessness-paper/commit/af477a9dbc7e5556b7a4f81be139bda149d5d1e9)。 |

测试证据保存在本轮仓库外的证据包 `flightlessness-fix-2026-11-27`：`local/summary.json`、`online/summary.json`、`online/artifacts-fix.json`、`online/fix-results/` 截图及可重跑脚本；未将测试依赖或脚本纳入博客仓库。

后续开始需要跨对话接手的工作时，简要记录正在改什么和涉及的文件。功能合并后，将对应条目改为已完成，补上一句用户能看到的变化和提交或 PR 链接。这里保留当前工作和最近几项变化，较早的记录从 Git 历史查阅。

## 目录与技术栈

| 路径 | 读取后确认的用途 |
| --- | --- |
| `README.md` | 博客简介、站点链接与项目文档入口。 |
| `hugo.yaml` | 定义 Pages baseURL、`en-US`（界面默认 locale）、站名、robots.txt、Git 信息、分类和标签、纯图标导航（页头模板）、Paper 配色与简介、GitHub/RSS 图标、代码高亮和前后篇开关。 |
| `go.mod` / `go.sum` | 站点依赖声明与校验文件。`go.mod` 固定 Paper 主题提交 `f7ed52a1da04`，`go.sum` 记录模块及其 go.mod 校验码，CI 只下载固定版本，升级需明确修改版本并检查产物。 |
| `.gitignore` | 忽略构建输出 `public/`、`resources/_gen/` 和 `.hugo_build.lock`，不再忽略 `go.sum`。 |
| `content/_index.md` | 首页标题和两段欢迎文案。模板没有把文案插入首页主体，生产 HTML 的 Open Graph、Twitter 和 Schema 描述使用了这段文案。 |
| `content/about.md` | About 的标题和 Markdown 正文，走本地覆盖的单页模板。 |
| `content/posts/` | 12 篇平铺的 Markdown 文件。目录没有自己的 `_index.md`，Hugo 自动生成 Posts 区段页。 |
| `layouts/_default/single.html` | 覆盖 Paper 单篇文章模板，前后篇导航跳过隐藏文章，其余渲染沿用 Paper。 |
| `layouts/_default/list.html` | 首页与 Posts 列表。筛选首页文章集合，渲染简介、标题、日期和分页，首页额外显示非隐藏分类链接，按「隐藏」分类决定是否输出文章链接。 |
| `layouts/_default/terms.html` | 分类、标签总览，按 `.Data.Terms.Alphabetical` 列出词条名称及数量，名称及篇数均无下划线。 |
| `layouts/_default/taxonomy.html` | 单个分类或标签词条页，按 `.Pages.ByDate.Reverse` 倒序输出文章卡片；隐藏文章只显示标题和日期，不输出失效链接。 |
| `assets/custom.css` | 补充本地模板需要、而 Paper 预编译样式未包含的 CSS 工具类。 |
| `layouts/partials/header.html` | 本地页头覆盖层。合并文字菜单、页头图标、移动端菜单和深色切换逻辑。 |
| `static/` | 三个旧导航 SVG 经源码与产物引用核验后清理；页头继续使用内联 SVG。 |
| `.github/workflows/hugo.yaml` | Hugo 构建与 GitHub Pages 部署的唯一仓库 workflow。 |

Hugo 将 Markdown 和 YAML Front Matter 转换为静态页面。模板使用 Hugo 的 Go 模板语法。Paper 以 Hugo Module 引入，实际部署 #62 解析到 `v0.0.0-20261026221338-f7ed52a1da04`。上游该提交的 `package.json` 标记 6.31.0，README 显示 6.30，所以排查生成结果时优先使用部署中的提交标识。站点仓库无 `package.json`、`themes/`、Git 子模块和自建后端。Paper 用 Bun、PostCSS、Tailwind 4.1.18 和 Typography 插件开发主题 CSS，本站 CI 直接消费 Paper 的预编译 `assets/main.css`。代码高亮脚本来自 Paper 的静态资源。当前站点配置没有启用主题提供的评论服务或数学排版选项。当前界面优先使用英文，中文文章不会因为 locale 变更而自动翻译。

[Paper 实际版本的源码](https://github.com/nanxiaobei/hugo-paper/tree/f7ed52a1da04aa2c536a9c075354191dc10152f8) · [Paper 前端依赖](https://github.com/nanxiaobei/hugo-paper/blob/f7ed52a1da04aa2c536a9c075354191dc10152f8/package.json)

## 页面怎样生成

| 线上相对路径 | 内容、模板与行为 |
| --- | --- |
| `/` | 本地 `list.html` 取 `site.RegularPages` 中属于 `site.Params.mainSections` 的内容。配置未显式指定 `mainSections`，当前有效主区段为 `posts`。首页第一页第一条记录之前显示配置中的名字和简介，当前未配置头像。 |
| `/posts/` | 同一列表模板，分页集合由当前区段的 `.RegularPages` 与 `.Sections` 合并。首页和 Posts 在线上当前均为 10 + 2 条。 |
| `/about/` | `content/about.md` → 本地 `single.html` → 正文 `.Content`。 |
| `/posts/<slug>/` | Markdown 和 Front Matter → Paper `single.html`，渲染标题、日期、正文、标签与前后篇。前后篇同样从主区段的 `site.RegularPages` 取数据。 |
| `/categories/` 与 `/tags/` | 本地 `terms.html` 输出所有词条及数量。 |
| `/categories/<词条>/` 与 `/tags/<词条>/` | 本地 `taxonomy.html` 用词条的 `.Pages` 输出文章链接。当前 `INFP` 的输出路径为 `/tags/infp/`。 |
| `/index.xml`、`/posts/index.xml`、词条 RSS、`/sitemap.xml`、`/robots.txt` | 使用 Hugo 内置输出。可见性与 HTML 列表模板各自计算。Paper 在生产环境为页面加 canonical、可用的 RSS 链接和社交元数据。 |

Paper 的 `baseof.html` 设置背景、头像和社交图标 Scratch 值，再依次调用 `head.html`、项目覆盖的 `header.html`、当前页面的 `main` block 及主题 `footer.html`。Paper 的 `head.html` 把 `assets/main.css` 和 `assets/custom.css` 合并、压缩、计算指纹并输出带完整性校验的样式链接。

页头不再输出文字菜单；Posts 页面保留，About 使用内联信息图标。Home/Categories/Tags 由页头通过 `absURL` 独立输出，不再依赖 RSS 分支；内联 SVG 使用 `currentColor`，仅原生社交背景图标使用 `dark:invert`。当前顺序为 Home、Categories、Tags、About、GitHub、RSS。Paper 用 `isset` 判定社交配置键是否存在。页头脚本控制移动菜单、系统配色和保存在 `localStorage` 的深色状态。菜单状态统一同步 `inert`、`aria-hidden`、`aria-expanded`；关闭移动菜单时链接不可聚焦，桌面导航始终可访问；Escape 返回菜单按钮，断点切换清理移动 open 状态。

当前 taxonomy 文件名沿用旧布局的语义。Hugo 0.169.0 的线上输出已确认其分工。若将来迁移到新版布局目录，应明确使用 `layouts/taxonomy.html` 做总览，`layouts/term.html` 做单个词条，并回归检查两级页面。

[Hugo 模板迁移说明](https://discourse.gohugo.io/t/migrating-templates-to-the-new-template-system-v0-146-0-and-later/57770)

## 文章约定

- 文件名使用小写英文或拼音、连字符和可选数字。12 篇文章均未显式设置 `slug`、`url` 或 `aliases`，已发布文章使用 `/posts/<文件名>/`。重命名时需要处理旧链接。
- 全部使用 `---` 包住 YAML，包含 `title`、带时区的 `date`、`draft: false` 和 `categories`。时区存在 `+08:00`、`-08:00`、`+00:00` 三种，排版变更时保留原始语义。4 篇使用 `tags`。隐藏文章另设 `sitemap.disable: true` 以排除无效详情 URL。分类可重叠，线上计数为「诗」9、「随笔」3、「隐藏」5。
- 诗歌常用行尾两个空格保留换行。有 4 篇在正文后用横线分隔外部链接。读取到的外链指向微博、B 站短链和腾讯纪念碑谷资讯。
- 本次审计的 12 篇文章均无 Markdown 图片、正文 HTML 图片或图片 shortcode。旧导航 SVG 已清理，暂无文章图片管理约定。新增图片可按项目需求选择文章包内的同目录图片或共享 `static/images/`，并验证实际输出 URL。

| 文件名（省略 .md） | 分类 | 标签 | 独立 HTML |
| --- | --- | --- | --- |
| `blue-planet-celebration` | 诗 | — | 有 |
| `chan-hui-lu-1` | 随笔、隐藏 | — | 404 |
| `chan-hui-lu-2` | 随笔、隐藏 | — | 404 |
| `chang-da` | 随笔、隐藏 | — | 404 |
| `hello-world` | 隐藏、诗 | — | 404 |
| `infp-late` | 诗 | INFP | 有 |
| `monument-valley-2` | 诗 | — | 有 |
| `moonlight-background` | 诗 | — | 有 |
| `shanhe-weiyang` | 诗 | 国庆 | 有 |
| `shi-hou` | 诗 | 风月 | 有 |
| `si-ren-yi-wang-qian-xiao-yi-ran` | 隐藏、诗 | — | 404 |
| `yogurt-spoiled` | 诗 | 爱情 | 有 |

## 构建与发布

1. 推送 `main` 或手动运行触发 workflow。并发组为 `pages`，`cancel-in-progress: false`。仓库的 workflow 未设置 pull request 预检触发。
2. Build job 在 `ubuntu-latest` 上运行 `actions/checkout@v6`（fetch-depth: 0）、`actions/setup-go@v6`，安装 Go 1.27.3，并从 Hugo release 下载安装 Hugo Extended 0.169.0 的 Linux amd64 包。
3. `actions/configure-pages@v6` 提供 `base_url`。`go mod download github.com/nanxiaobei/hugo-paper` 下载锁定主题，`HUGO_ENVIRONMENT=production hugo --gc --minify --baseURL "${{ steps.pages.outputs.base_url }}/"` 构建到 `public/`。
4. `actions/upload-pages-artifact@v5` 上传 `public/`。Deploy job 依赖 build，使用 `actions/deploy-pages@v5` 在 `github-pages` 环境部署。权限包括 `contents: read`、`pages: write` 和 `id-token: write`。
5. #62 为 2026-11-21 的 main push。日志确认 build、上传和 deploy 成功，构建报告为 35 个 Pages、2 个分页页面、16 个静态文件和 0 张处理图片，部署目标为 `https://flightlessness.github.io/flightlessness-paper/`。这次审计没有触发远程构建或部署。另用相同版本的 Go 和 Hugo Extended 在独立浅克隆中重跑模块解析和生产构建，得到相同的主题提交和构建计数。产出的指纹 CSS 与线上文件逐字节一致。

## 后续计划与维护

已迁移至 [ROADMAP.md](ROADMAP.md)，统一记录未实现功能、风险、维护优先级与验证状态。

[隐藏分类](https://flightlessness.github.io/flightlessness-paper/categories/%E9%9A%90%E8%97%8F/) · [站点订阅](https://flightlessness.github.io/flightlessness-paper/index.xml) · [站点地图](https://flightlessness.github.io/flightlessness-paper/sitemap.xml) · [Hugo 构建选项](https://gohugo.io/content-management/build-options/)
