# 技术与设计决策

本文件记录已确认的项目约定和当前已经采用的实现。它关联 [项目地图](PROJECT_MAP.md) 和 [任务台账](TASKS.md)。某项决定替换既有约定时，记录新选择、原因和受影响范围。

## GitHub 主分支是项目文档的权威版本

**依据** 用户于 2026-11-26 明确指定。

根目录保存 `AGENTS.md`。项目地图、路线图、决策台账和任务台账保存在 `project-docs/`。跨对话交接以 GitHub `main` 最新内容为准。文档与站点源码共用版本历史，便于把文档变化关联到对应提交。

## 使用 Hugo 与 Paper 构建静态博客

**依据** 已实现，见 [hugo.yaml](../hugo.yaml)、[go.mod](../go.mod) 和 [README.md](../README.md)。

站点内容保存在 Markdown，Hugo 读取 YAML Front Matter，Paper 作为 Hugo Module 提供基础模板与资源。项目层已有首页和 Posts 列表、分类和标签模板及页头覆盖。主题配色为 `linen`，页头提供深色切换。当前 CI 使用 Hugo Extended 0.169.0 和 Go 1.27.3。审计中的 Paper 版本是部署事实，模块固定方案仍见任务台账。

## 通过 GitHub Actions 发布到 GitHub Pages

**依据** 已实现，见 [部署 workflow](../.github/workflows/hugo.yaml)。

推送 `main` 或手动触发构建。Actions 获取项目 baseURL，构建到 `public/` 并部署到 Pages。网站路径保留 `/flightlessness-paper/`。导航、资源和生产构建的验收以该子路径为基准。

## 文章 URL、分类和标签沿用当前结构

**依据** 已实现，见 [文章源目录](../content/posts/) 和 [站点配置](../hugo.yaml)。

现有文章集中在 `content/posts/`，文件名由小写英文或拼音、连字符和可选数字组成。正常发布时已有 URL 由文件名决定，分类和标签由 Front Matter 驱动。文章正文保留作者的写作格式，尤其是诗歌硬换行。图片目录策略留待首个实际需求。

## 待确认的议题

- 「隐藏」目前是已有实现，作者期望的可见范围仍待确认。先确定详情页、列表、RSS、sitemap 和公开源码各自允许公开的内容，再选择实现。
- Paper 固定版本方案、样式修复方式和中文文案范围由对应执行任务验证后记录。候选方案和任务状态见 [TASKS.md](TASKS.md)。
