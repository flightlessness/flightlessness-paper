# AGENTS.md

## 项目与操作范围

- 这是 flightlessness 的中文个人博客。站点由 Hugo Extended 与 Paper 主题模块生成，通过 GitHub Actions 部署至 GitHub Pages。
- 目录、模板优先级和已知行为见 [PROJECT_MAP.md](project-docs/PROJECT_MAP.md)。按任务范围读取当前分支的相关文件。
- 分析请求使用只读操作。获得修改授权后，将改动限制在任务范围内。推送 `main` 会触发部署，按用户明确授权执行提交、推送或发布。
- 保留现有文章的文风、标题、标点、日期和 URL。诗歌行尾的两个空格是 Markdown 硬换行，批量格式化时保留。

## 项目文档与 Git 工作流

- 当前任务以用户在本次 ChatGPT 对话中的明确要求为准。同一任务有后续补充或更正时，按最新要求执行。GitHub `main` 上的本文件和 `project-docs/` 提供项目背景、默认工作方式及交接参考。文档与当前对话的明确要求冲突时，按当前对话执行。
- 改动功能、模板、配置或部署时，按需查阅项目地图，并搜索相关实现、调用方和模板覆盖。优先复用已有逻辑。功能、目录或依赖关系变化时，更新项目地图。用户提出但尚未实施的功能需求，记录到 [project-docs/ROADMAP.md](project-docs/ROADMAP.md) 的后续计划，注明目标、状态和未定设计；不要把设想写成已实现。AI 主动提出的每个网站功能建议也须同步写入 ROADMAP，标为候选或暂缓，合并重复事项；记录不等于实施授权。
- 从当前 `main` 开始工作，先检查分支、工作区和远端 HEAD。跨模板、主题或部署的改动优先用短期分支和 PR。按用户授权提交或合并，避免覆盖他人的改动。提交前核对差异范围。
- 推送 `main` 会触发 Pages 部署，包括仅文档的提交。用户授权直接更新 `main` 时，用正常快进写入。提交后核对实际提交和 Actions 结果。远端在工作期间更新时，先读取新提交并重新核对差异。
- 仓库是公开的，纳入版本控制的管理文档也可以公开读取。项目文档使用根目录和 `project-docs/`，站点文章、页面和公开素材使用对应的 Hugo 源目录。

## 常见改动入口

| 任务 | 入口和联动检查 |
| --- | --- |
| 首页展示名和简介 | `hugo.yaml` 的 `params.name`、`params.bio`。首页正文元数据来自 `content/_index.md`，可视简介和文章列表由 `layouts/_default/list.html` 渲染。 |
| 修改 About | `content/about.md`。页面内容使用 Paper 的单页模板。 |
| 修改站名、菜单文字和顺序 | `hugo.yaml` 的 `title` 和 `layouts/partials/header.html` 的纯图标导航。 |
| 修改导航图标、移动端菜单或深色切换 | `layouts/partials/header.html`。Home、Categories、Tags、About 使用独立内联 SVG；GitHub/RSS 使用 Paper 背景图标。Posts 页面保留但不在导航栏。 |
| 修改分类或标签 | 文章 Front Matter 和 `hugo.yaml` 的 `taxonomies`。当前版本下，`layouts/_default/terms.html` 渲染分类和标签总览，`layouts/_default/taxonomy.html` 渲染单个词条的文章列表。 |
| 修改样式 | 主题配色在 `hugo.yaml` 的 `params.color`。本地模板使用 Paper 的预编译 Tailwind CSS。新增工具类先查生成 CSS 是否包含对应选择器。需要自定义 CSS 时，可使用项目 `assets/custom.css` 覆盖 Paper 的同名占位资源，并检查生成的 CSS。 |
| 修改文章详情、页脚、元数据 | 先核对实际解析到的 Paper 模块版本及其单页、footer、head 模板，再按需求增加局部覆盖。 |
| 修改构建和部署 | `.github/workflows/hugo.yaml`、`hugo.yaml`、`go.mod`。保留项目子路径 `/flightlessness-paper/` 的验证。 |

## 写作与发布

- 新文放在 `content/posts/<slug>.md`，使用小写英文或拼音加连字符，可加数字系列后缀。日期放在 YAML Front Matter，沿用文章原有时区，有新日期时写明正确偏移量。
- 常用字段为 `title`、`date`、`draft`、`categories`，按需加 `tags`。正常发布时使用 `draft: false`，复用现有分类与标签拼写。
- 明确区分草稿与现有的「隐藏」约定。当前「隐藏」由 `categories: [隐藏, …]` 和 `build.render: link` 组合实现。标题仍在集合中，详情页会缺失，公开 RSS 仍可能输出正文摘录。使用保密内容前须考虑公开源码，草稿标志和模板过滤仅影响生成站点。
- 新增图片前核对需求和输出路径。旧导航 SVG 已清理，尚无文章图片惯例。采用文章专用资源时，可选 `content/posts/<slug>/index.md` 与同目录图片，使用相对 Markdown 链接。采用共享静态资源时，可选 `static/images/`，并验证 GitHub Pages 子路径和替代文字。迁移已有文章时保留原 URL 并验证。
- 普通文字 Post 只需读取目标文章或一篇同类样例，核对文件名是否冲突、Front Matter 和正文。用户明确要求发布即授权直接提交到 `main`，无需再次确认。构建验证由 GitHub Actions 执行，提交后查看部署结果。页面、分类、分页和订阅的联动检查用于涉及相应行为的改动。调整隐藏规则时，检查首页、Posts、分类与标签、前后篇、RSS、sitemap 和详情页的返回状态。

## 模板、样式、配置和部署改动的验证

- 以 `.github/workflows/hugo.yaml` 为当前构建工具版本来源。审计时为 Go 1.27.3 与 Hugo Extended 0.169.0。
- 本地预览用 `hugo server`，预览草稿时用 `hugo server -D`。验证部署行为时使用生产环境参数和 Pages baseURL。
- CI 使用 `go mod download github.com/nanxiaobei/hugo-paper` 下载 `go.mod` 中固定的 Paper 版本，`go.sum` 纳入版本控制。复现生产构建时不得自动执行 `hugo mod get -u`；主题升级需要明确任务、修改依赖与校验文件，并检查生成产物。记录 `hugo mod graph` 中的实际版本。
- 生产构建命令为 `HUGO_ENVIRONMENT=production hugo --gc --minify --baseURL "https://flightlessness.github.io/flightlessness-paper/"`。检查 `public/` 中实际生成的 URL、资源、RSS 和 sitemap，确认 Git diff 中只有预期源文件变动。
- 验证导航或样式时覆盖首页与嵌套页面、桌面与移动端、浅色与深色，并检查键盘操作。通过 CI 或真实页面验证到的行为和仍缺失的验证应在交付中分开写明。

## CSS 冲突排查与视觉验证

- 修改样式前，核对目标元素实际 HTML、锁定 Paper 版本的预编译 `assets/main.css` 与本地 `assets/custom.css`，检查选择器优先级、层叠顺序、媒体查询和深色/交互状态。Paper 当前使用 `:not(#\#)` 提升选择器优先级（全局重置有两个 ID 级权重，工具类及组件可能更高）；后加载的普通选择器不一定能覆盖它。
- 优先采用局部且足够的选择器优先级，必要时沿用 Paper 的 `:not(#\#)` 机制；保持桌面/移动端、深色及 hover/focus 变体之间的层叠关系。避免无差别提高权重或使用 `!important`，不为解决局部冲突修改上游主题。
- 如果线上样式未变化，不继续盲目调整数值。先确认部署提交及实际 HTML 引用的指纹 CSS，检查资源加载、缓存和目标规则；再用浏览器 DevTools 的 Styles / Computed 找到最终生效值及覆盖来源。修复后核对相关断点、配色和交互状态，必要时强制刷新。
- CI 成功只证明构建/部署结果，不代表视觉效果正确。能访问实际浏览器时验证最终计算样式与视觉表现；工具不能完成时明确标记待验证，不宣称视觉验证通过。用户实际确认可记录为用户视觉验收。参见 CSS 优先级修复提交 `866369f`。
