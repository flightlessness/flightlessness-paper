# flightlessness-paper 项目地图

审计范围为 2026-11-26 读取的 `main`，提交 `af477a9dbc7e5556b7a4f81be139bda149d5d1e9`。递归目录结果完整，26 个跟踪文件均已读取，包括 12 篇文章全文、3 个 SVG、站点配置、模板和部署脚本。另读了最近一次部署的 build 和 deploy 日志，以及该部署解析到的 Paper 模块的关键模板、CSS 入口和工具配置。此次分析保持 GitHub 仓库只读。

[仓库快照](https://github.com/flightlessness/flightlessness-paper/tree/af477a9dbc7e5556b7a4f81be139bda149d5d1e9) · [部署 #62](https://github.com/flightlessness/flightlessness-paper/actions/runs/44914085196) · [线上站点](https://flightlessness.github.io/flightlessness-paper/)

## 项目管理文档

根目录的 [AGENTS.md](../AGENTS.md) 记录 AI 操作规范和 Git 流程。本文件记录已有功能、文件关系及实现入口。下文的构建证据使用上面的审计快照，动手前对照 GitHub `main` 上的最新源码。

## 当前改动与最近新增

| 状态 | 内容 |
| --- | --- |
| 已完成 · 隐藏文章 | 隐藏文章导航修复：分类词条页保留标题但取消不可达链接；公开文章的前后篇跳过隐藏文章；5 篇隐藏文章通过 Front Matter 的 `sitemap.disable: true` 不再列入 sitemap。涉及 `layouts/_default/{taxonomy,single}.html` 与 5 篇隐藏文章的元数据；RSS、正文和首页/Posts 展示保持不变。提交 [`f6b3584`](https://github.com/flightlessness/flightlessness-paper/commit/f6b35846f64d055d431c318e8f18e3f1b425d9f5)，Actions [#45838661569](https://github.com/flightlessness/flightlessness-paper/actions/runs/45838661569) 构建及部署成功。 |
| 本轮站点维护 | 固定 Paper 主题至 `f7ed52a1da04`、准备跟踪 Go 模块校验文件，修补本地布局 CSS，改善菜单/深色切换的键盘可用性与社交图标路径，将配置键改为 `locale: en-US`。 |
| 最近完成 | 将项目管理文档精简为两份，并在 README 集中链接。详见 [`f173548`](https://github.com/flightlessness/flightlessness-paper/commit/f17354811cf09790a67cca3f2110d7c7c93594fe)。 |
| 最近的站点变更 | 调整《忏悔录 2》的发布时间。详见 [`af477a9`](https://github.com/flightlessness/flightlessness-paper/commit/af477a9dbc7e5556b7a4f81be139bda149d5d1e9)。 |
| 站点功能开发 | 截至本次核对，近期提交中未见新增站点功能，GitHub 上也没有开放的 PR。 |

后续开始需要跨对话接手的工作时，简要记录正在改什么和涉及的文件。功能合并后，将对应条目改为已完成，补上一句用户能看到的变化和提交或 PR 链接。这里保留当前工作和最近几项变化，较早的记录从 Git 历史查阅。

## 目录与技术栈

| 路径 | 读取后确认的用途 |
| --- | --- |
| `README.md` | 说明 Markdown 写作、提交 main 后自动部署，以及 `hugo server` 预览。 |
| `hugo.yaml` | 定义 Pages baseURL、`en-US`（界面默认 locale）、站名、robots.txt、Git 信息、分类和标签、Posts/About 菜单、Paper 配色与简介、GitHub/RSS 图标、代码高亮和前后篇开关。 |
| `go.mod` / `go.sum` | 站点依赖声明与校验文件。`go.mod` 固定 Paper 主题提交 `f7ed52a1da04`，CI 只下载固定版本，升级需明确修改版本并检查产物。 |
| `.gitignore` | 忽略构建输出 `public/`、`resources/_gen/` 和 `.hugo_build.lock`，不再忽略 `go.sum`。 |
| `content/_index.md` | 首页标题和两段欢迎文案。模板没有把文案插入首页主体，生产 HTML 的 Open Graph、Twitter 和 Schema 描述使用了这段文案。 |
| `content/about.md` | About 的标题和 Markdown 正文，走 Paper 单页模板。 |
| `content/posts/` | 12 篇平铺的 Markdown 文件。目录没有自己的 `_index.md`，Hugo 自动生成 Posts 区段页。 |
| `layouts/_default/single.html` | 覆盖 Paper 单篇文章模板，前后篇导航跳过隐藏文章，其余渲染沿用 Paper。 |
| `layouts/_default/list.html` | 首页与 Posts 列表。筛选首页文章集合，渲染简介、标题、日期和分页，并按「隐藏」分类决定是否输出卡片链接。 |
| `layouts/_default/terms.html` | 分类、标签总览，按 `.Data.Terms.Alphabetical` 列出词条名称及数量。 |
| `layouts/_default/taxonomy.html` | 单个分类或标签词条页，按 `.Pages.ByDate.Reverse` 倒序输出文章卡片；隐藏文章只显示标题和日期，不输出失效链接。 |
| `assets/custom.css` | 补充本地模板需要、而 Paper 预编译样式未包含的 CSS 工具类。 |
| `layouts/partials/header.html` | 本地页头覆盖层。合并文字菜单、页头图标、移动端菜单和深色切换逻辑。 |
| `static/{home,categories,tags}.svg` | 三个同名公共静态 SVG。当前页头重画为内联 SVG，这三个文件没有在本地模板或已读文章中被引用。 |
| `.github/workflows/hugo.yaml` | Hugo 构建与 GitHub Pages 部署的唯一仓库 workflow。 |

Hugo 将 Markdown 和 YAML Front Matter 转换为静态页面。模板使用 Hugo 的 Go 模板语法。Paper 以 Hugo Module 引入，实际部署 #62 解析到 `v0.0.0-20261026221338-f7ed52a1da04`。上游该提交的 `package.json` 标记 6.31.0，README 显示 6.30，所以排查生成结果时优先使用部署中的提交标识。站点仓库无 `package.json`、`themes/`、`assets/`、Git 子模块和自建后端。Paper 用 Bun、PostCSS、Tailwind 4.1.18 和 Typography 插件开发主题 CSS，本站 CI 直接消费 Paper 的预编译 `assets/main.css`。代码高亮脚本来自 Paper 的静态资源。当前站点配置没有启用主题提供的评论服务或数学排版选项。当前界面优先使用英文，中文文章不会因为 locale 变更而自动翻译。

[Paper 实际版本的源码](https://github.com/nanxiaobei/hugo-paper/tree/f7ed52a1da04aa2c536a9c075354191dc10152f8) · [Paper 前端依赖](https://github.com/nanxiaobei/hugo-paper/blob/f7ed52a1da04aa2c536a9c075354191dc10152f8/package.json)

## 页面怎样生成

| 线上相对路径 | 内容、模板与行为 |
| --- | --- |
| `/` | 本地 `list.html` 取 `site.RegularPages` 中属于 `site.Params.mainSections` 的内容。配置未显式指定 `mainSections`，当前有效主区段为 `posts`。首页第一页第一条记录之前显示配置中的名字和简介，当前未配置头像。 |
| `/posts/` | 同一列表模板，分页集合由当前区段的 `.RegularPages` 与 `.Sections` 合并。首页和 Posts 在线上当前均为 10 + 2 条。 |
| `/about/` | `content/about.md` → Paper `single.html` → 正文 `.Content`。 |
| `/posts/<slug>/` | Markdown 和 Front Matter → Paper `single.html`，渲染标题、日期、正文、标签与前后篇。前后篇同样从主区段的 `site.RegularPages` 取数据。 |
| `/categories/` 与 `/tags/` | 本地 `terms.html` 输出所有词条及数量。 |
| `/categories/<词条>/` 与 `/tags/<词条>/` | 本地 `taxonomy.html` 用词条的 `.Pages` 输出文章链接。当前 `INFP` 的输出路径为 `/tags/infp/`。 |
| `/index.xml`、`/posts/index.xml`、词条 RSS、`/sitemap.xml`、`/robots.txt` | 使用 Hugo 内置输出。可见性与 HTML 列表模板各自计算。Paper 在生产环境为页面加 canonical、可用的 RSS 链接和社交元数据。 |

Paper 的 `baseof.html` 设置背景、头像和社交图标 Scratch 值，再依次调用 `head.html`、项目覆盖的 `header.html`、当前页面的 `main` block 及主题 `footer.html`。Paper 的 `head.html` 把 `assets/main.css` 和 `assets/custom.css` 合并、压缩、计算指纹并输出带完整性校验的样式链接。

页头文字取 `site.Menus.main`。已验证生成的 Posts/About 链接包含 `/flightlessness-paper/`。Home/Categories/Tags 由页头通过 `absURL` 输出，并与 RSS 项共用一次分支。Paper 用 `isset` 判定 `rss` 等键是否存在。如果将 `rss` 键整个移除，三个额外图标也会消失。单纯设为 `false` 仍保留该键。页头脚本控制移动菜单、系统配色和保存在 `localStorage` 的深色状态。

当前 taxonomy 文件名沿用旧布局的语义。Hugo 0.169.0 的线上输出已确认其分工。若将来迁移到新版布局目录，应明确使用 `layouts/taxonomy.html` 做总览，`layouts/term.html` 做单个词条，并回归检查两级页面。

[Hugo 模板迁移说明](https://discourse.gohugo.io/t/migrating-templates-to-the-new-template-system-v0-146-0-and-later/57770)

## 文章约定

- 文件名使用小写英文或拼音、连字符和可选数字。12 篇文章均未显式设置 `slug`、`url` 或 `aliases`，已发布文章使用 `/posts/<文件名>/`。重命名时需要处理旧链接。
- 全部使用 `---` 包住 YAML，包含 `title`、带时区的 `date`、`draft: false` 和 `categories`。时区存在 `+08:00`、`-08:00`、`+00:00` 三种，排版变更时保留原始语义。5 篇使用 `tags`。隐藏文章另设 `sitemap.disable: true` 以排除无效详情 URL。分类可重叠，线上计数为「诗」9、「随笔」3、「隐藏」5。
- 诗歌常用行尾两个空格保留换行。有 4 篇在正文后用横线分隔外部链接。读取到的外链指向微博、B 站短链和腾讯纪念碑谷资讯。
- 本次审计的 12 篇文章均无 Markdown 图片、正文 HTML 图片或图片 shortcode。站点仅三份本地导航 SVG，暂无文章图片管理约定。新增图片可按项目需求选择文章包内的同目录图片或共享 `static/images/`，并验证实际输出 URL。

| 文件名（省略 .md） | 分类 | 标签 | 独立 HTML |
| --- | --- | --- | --- |
| `blue-planet-celebration` | 诗 | — | 有 |
| `chan-hui-lu-1` | 随笔、隐藏 | — | 404 |
| `chan-hui-lu-2` | 随笔、隐藏 | — | 404 |
| `chang-da` | 随笔、隐藏 | — | 404 |
| `hello-world` | 隐藏、诗 | — | 404 |
| `infp-late` | 诗 | INFP | 有 |
| `monument-valley-2` | 诗 | — | 有 |
| `moonlight-background` | 诗 | 后知 | 有 |
| `shanhe-weiyang` | 诗 | 国庆 | 有 |
| `shi-hou` | 诗 | 风月 | 有 |
| `si-ren-yi-wang-qian-xiao-yi-ran` | 隐藏、诗 | — | 404 |
| `yogurt-spoiled` | 诗 | 爱情 | 有 |

## 构建与发布

1. 推送 `main` 或手动运行触发 workflow。并发组为 `pages`，`cancel-in-progress: false`。仓库的 workflow 未设置 pull request 预检触发。
2. Build job 在 `ubuntu-latest` 上运行 `actions/checkout@v6`、`actions/setup-go@v6`，安装 Go 1.27.3，并从 Hugo release 下载安装 Hugo Extended 0.169.0 的 Linux amd64 包。
3. `actions/configure-pages@v5` 提供 `base_url`。`hugo mod download` 下载锁定主题，`HUGO_ENVIRONMENT=production hugo --gc --minify --baseURL "${{ steps.pages.outputs.base_url }}/"` 构建到 `public/`。
4. `actions/upload-pages-artifact@v4` 上传 `public/`。Deploy job 依赖 build，使用 `actions/deploy-pages@v5` 在 `github-pages` 环境部署。权限包括 `contents: read`、`pages: write` 和 `id-token: write`。
5. #62 为 2026-11-21 的 main push。日志确认 build、上传和 deploy 成功，构建报告为 35 个 Pages、2 个分页页面、16 个静态文件和 0 张处理图片，部署目标为 `https://flightlessness.github.io/flightlessness-paper/`。这次审计没有触发远程构建或部署。另用相同版本的 Go 和 Hugo Extended 在独立浅克隆中重跑模块解析和生产构建，得到相同的主题提交和构建计数。产出的指纹 CSS 与线上文件逐字节一致。

## 后续计划与未实现功能

- **中英双语阅读（规划中）**：网站界面以英文为默认；绝大部分现有 Post 为中文。未来每篇文章发布前由 AI 翻译和润色英文版，经作者确认，再一同发布中文原文和英文译文；文章详情页提供中英切换，并保持相互对应。设计时确定 Hugo multilingual 目录/Front Matter、默认 URL 与英文 URL、`hreflang`、sitemap、RSS、分类/标签翻译、未翻译文章回退、隐藏文章继承规则，确保现有中文文章 URL 不被破坏。当前仅改成英文 `locale`，**尚未提供双语切换或翻译自动化**。
- **404 导航体验（可选）**：旧书签或手动访问失效 URL 时，可在通用 404 模板中加入返回上一页及返回 Posts；与隐藏文章当前不可访问的约定区分。
- **保留待定**：`Hello, Hugo` 测试文章是否长期保留、三个无模板引用的 `static/{home,categories,tags}.svg` 是否删除，由以后单独决定。

## 风险与维护重点

| 优先级 | 发现与可复验的证据 | 处理方向 |
| --- | --- | --- |
| 已解决 | 5 篇隐藏文章仍无详情页，但分类页移除失效链接、前后篇跳过隐藏、sitemap 排除对应 URL，保留标题与 RSS。 | 维持现有“网站不展示正文、仓库和 RSS 可以公开”的约定。 |
| 本轮处理 | 主题版本漂移：固定 `go.mod` 的 Paper 版本，停止 CI 自动升级，并跟踪 `go.sum`。 | 如需主题升级，单独修改依赖，验证生成 CSS 和模板差异。 |
| 本轮处理 | 本地分类/页头模板引用了 Paper 预编译 CSS 中不存在的工具类。 | 在 `assets/custom.css` 补齐五个类并以构建产物验证。 |
| 本轮处理 | 旧键 `languageCode` 已弃用。网站以英文 UI 为默认，Post 仍以中文为主。 | 采用 `locale: en-US`；正式双语站点另行设计真实语言标记和逐篇翻译。 |
| 本轮处理 | 菜单/深色按钮缺少键盘事件和状态属性；社交图标依赖相对路径。 | 增加 Enter/Space 键支持、状态 ARIA 属性和站点绝对资源 URL。 |
| 低 | `static/` 三个项目图标均可在线访问，但页头使用内联版本。Hello, Hugo 为初始测试文章，现继续出现在列表、分类和订阅输出。 | 确认没有外部引用后再考虑静态文件清理。测试文章是否留作历史记录由作者决定。 |
| 低 | 最新 CI 已出现 Node.js 20 action 运行时兼容提示及 Go 模块缓存路径缺失提示。浅克隆默认深度配合 `enableGitInfo` 可能限制历史元数据的完整性。 | 下次维护 CI 时核验 action 新版本、缓存和 Git 历史深度。当前 #62 的构建与部署成功。 |

[隐藏分类](https://flightlessness.github.io/flightlessness-paper/categories/%E9%9A%90%E8%97%8F/) · [站点订阅](https://flightlessness.github.io/flightlessness-paper/index.xml) · [站点地图](https://flightlessness.github.io/flightlessness-paper/sitemap.xml) · [Hugo 构建选项](https://gohugo.io/content-management/build-options/)

## 未覆盖的部分

- GitHub Pages 管理页面、环境保护、私有变量和自定义域设置未读取。实际部署模式和 URL 来自已成功的 Actions 记录。
- #62 的原始构建产物压缩包已不可获取。公开 URL、HTML、RSS、sitemap 和 CSS 已抽查，并复现了本地生产构建。未逐个检查所有外链、浏览器视觉与移动端交互，也未审阅主题仓库全部上游文件。
