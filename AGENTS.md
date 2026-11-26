# AGENTS.md

## 项目与操作范围

- 这是 flightlessness 的中文个人博客。站点由 Hugo Extended 与 Paper 主题模块生成，通过 GitHub Actions 部署至 GitHub Pages。
- 目录、模板优先级和已知行为见 [PROJECT_MAP.md](project-docs/PROJECT_MAP.md)。按任务范围读取当前分支的相关文件。
- 分析请求使用只读操作。获得修改授权后，将改动限制在任务范围内。推送 `main` 会触发部署，按用户明确授权执行提交、推送或发布。
- 保留现有文章的文风、标题、标点、日期和 URL。诗歌行尾的两个空格是 Markdown 硬换行，批量格式化时保留。

## 项目文档与 Git 工作流

- 当前任务以用户在本次 ChatGPT 对话中的明确要求为准。同一任务有后续补充或更正时，按最新要求执行。GitHub `main` 上的本文件和 `project-docs/` 提供项目背景、默认工作方式及交接参考。文档与当前对话的明确要求冲突时，按当前对话执行。
- 改动功能、模板、配置或部署时，按需查阅项目地图，并搜索相关实现、调用方和模板覆盖。优先复用已有逻辑。功能、目录或依赖关系变化时，更新项目地图。
- 从当前 `main` 开始工作，先检查分支、工作区和远端 HEAD。跨模板、主题或部署的改动优先用短期分支和 PR。按用户授权提交或合并，避免覆盖他人的改动。提交前核对差异范围。
- 推送 `main` 会触发 Pages 部署，包括仅文档的提交。用户授权直接更新 `main` 时，用正常快进写入。提交后核对实际提交和 Actions 结果。远端在工作期间更新时，先读取新提交并重新核对差异。
- 仓库是公开的，纳入版本控制的管理文档也可以公开读取。项目文档使用根目录和 `project-docs/`，站点文章、页面和公开素材使用对应的 Hugo 源目录。

## 常见改动入口

| 任务 | 入口和联动检查 |
| --- | --- |
| 首页展示名和简介 | `hugo.yaml` 的 `params.name`、`params.bio`。首页正文元数据来自 `content/_index.md`，可视简介和文章列表由 `layouts/_default/list.html` 渲染。 |
| 修改 About | `content/about.md`。页面内容使用 Paper 的单页模板。 |
| 修改站名、菜单文字和顺序 | `hugo.yaml` 的 `title` 和 `menu.main`。文本菜单与图标共同由 `layouts/partials/header.html` 输出。 |
| 修改导航图标、移动端菜单或深色切换 | `layouts/partials/header.html`。Home、Categories、Tags 使用内联 SVG，当前与 RSS 分支绑定。 |
| 修改分类或标签 | 文章 Front Matter 和 `hugo.yaml` 的 `taxonomies`。当前版本下，`layouts/_default/terms.html` 渲染分类和标签总览，`layouts/_default/taxonomy.html` 渲染单个词条的文章列表。 |
| 修改样式 | 主题配色在 `hugo.yaml` 的 `params.color`。本地模板使用 Paper 的预编译 Tailwind CSS。新增工具类先查生成 CSS 是否包含对应选择器。需要自定义 CSS 时，可使用项目 `assets/custom.css` 覆盖 Paper 的同名占位资源，并检查生成的 CSS。 |
| 修改文章详情、页脚、元数据 | 先核对实际解析到的 Paper 模块版本及其单页、footer、head 模板，再按需求增加局部覆盖。 |
| 修改构建和部署 | `.github/workflows/hugo.yaml`、`hugo.yaml`、`go.mod`。保留项目子路径 `/flightlessness-paper/` 的验证。 |

## 写作与发布

- 新文放在 `content/posts/<slug>.md`，使用小写英文或拼音加连字符，可加数字系列后缀。日期放在 YAML Front Matter，沿用文章原有时区，有新日期时写明正确偏移量。
- 常用字段为 `title`、`date`、`draft`、`categories`，按需加 `tags`。正常发布时使用 `draft: false`，复用现有分类与标签拼写。
- 明确区分草稿与现有的「隐藏」约定。当前「隐藏」由 `categories: [隐藏, …]` 和 `build.render: link` 组合实现。标题仍在集合中，详情页会缺失，公开 RSS 仍可能输出正文摘录。使用保密内容前须考虑公开源码，草稿标志和模板过滤仅影响生成站点。
- 新增图片前核对需求和输出路径。仓库目前只有导航 SVG，没有文章图片惯例。采用文章专用资源时，可选 `content/posts/<slug>/index.md` 与同目录图片，使用相对 Markdown 链接。采用共享静态资源时，可选 `static/images/`，并验证 GitHub Pages 子路径和替代文字。迁移已有文章时保留原 URL 并验证。
- 普通文字 Post 只需读取目标文章或一篇同类样例，核对文件名是否冲突、Front Matter 和正文。用户明确要求发布即授权直接提交到 `main`，无需再次确认。构建验证由 GitHub Actions 执行，提交后查看部署结果。页面、分类、分页和订阅的联动检查用于涉及相应行为的改动。调整隐藏规则时，检查首页、Posts、分类与标签、前后篇、RSS、sitemap 和详情页的返回状态。

## 模板、样式、配置和部署改动的验证

- 以 `.github/workflows/hugo.yaml` 为当前构建工具版本来源。审计时为 Go 1.27.3 与 Hugo Extended 0.169.0。
- 本地预览用 `hugo server`，预览草稿时用 `hugo server -D`。验证部署行为时使用生产环境参数和 Pages baseURL。
- 在临时工作副本中复现 CI 的 `hugo mod get -u` 与生产构建。前者会解析或更新 Paper 模块，也可能写入 `go.mod` 和 `go.sum`。记录 `hugo mod graph` 输出中的实际主题版本。
- 生产构建命令为 `HUGO_ENVIRONMENT=production hugo --gc --minify --baseURL "https://flightlessness.github.io/flightlessness-paper/"`。检查 `public/` 中实际生成的 URL、资源、RSS 和 sitemap，确认 Git diff 中只有预期源文件变动。
- 验证导航或样式时覆盖首页与嵌套页面、桌面与移动端、浅色与深色，并检查键盘操作。通过 CI 或真实页面验证到的行为和仍缺失的验证应在交付中分开写明。
