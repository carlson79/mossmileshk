# Moss & Miles 苔径 — 网站维护指南（SITE-GUIDE）

> 任何对话、任何人维护本站前，先读完本文件。内容现状一律以本仓库为准，其他地方的副本（Kimi 项目文件、本地文件）仅作参考。

## 1. 站点与仓库

- 线上地址：https://mossmiles.hk （GitHub Pages + CNAME，推送到 main 后自动重建，约 1 分钟生效）
- 仓库：`carlson79/mossmileshk`，默认分支 `main`
- 纯静态 HTML/CSS，无构建流程，含 `.nojekyll`
- 旧站仓库：`carlson79/mossmiles`（内有 music.html 波士顿音乐节小提琴页，尚未迁移）

## 2. 网站结构

首页 `index.html`：hero（Moss & Miles / 苔径 / "Run long distances. Notice small things."）→ 四栏目导航卡（`.cats`）→ Field Notes 文章列表（`.essays`，按栏目分组 `.group-label`，**组内新文章排在最前**）→ About → footer。

| 栏目 | class | 标签色 | 内容 |
|---|---|---|---|
| Macro Ecology 宏观生态 | `macro` | `.tag.gold`（沙色） | 赛事随笔、戈壁、赛道与沿途观察 |
| Micro World 微观世界 | `micro` | `.tag.green`（苔色） | 苔藓观察、微距摄影 |
| Investment Notes 投资笔记 | `invest` | `.tag.deep`（深苔） | 论文阅读笔记（当前为占位卡 `.card.soon`） |
| Nature & Humanities 自然与人文 | `hum` | `.tag.bronze`（铜色） | 唐宋苔诗、俳句、音乐 |

## 3. 设计规范

### 首页
- 字体：Georgia/Times 正文 + 'Songti SC'/'Noto Serif SC' 中文；无衬线点缀用 'Segoe UI'
- 色板：`--moss-deep:#1e3a24` `--moss:#3e6b3f` `--moss-light:#7fa86b` `--moss-pale:#e9f2e3` `--sand:#9a6b2f` `--sand-light:#d9b380` `--bronze:#b08d57` `--ink:#26312a` `--paper:#f7f8f3` `--grey:#75806f`
- 文章卡 `.card`：`grid-template-columns:220px 1fr`，`.thumb` 用背景图，`.body` 内依次为 `.tag`（栏目色 · 子标签）、`h3` 标题、`.desc` 摘要、`.meta`（日期 · 地点）

### 文章页（模板参照 `gobi20.html`、`changsha.html`）
- 沙色系：`--sand-deep:#2b2118` `--sand:#9a6b2f` `--sand-light:#d9b380` `--paper:#faf6ee` `--ink:#3a2e1e` `--grey:#8a8070`
- 中文宋体，`line-height:2`，正文 `max-width:780px`
- 结构顺序：固定 nav 返回链接 → hero（`.bg` 背景图 opacity .6 + `.veil` 底部压暗渐变 + `.kicker` / `h1` / `.sub`）→ `.stats` 数据带（可选，赛事类文章用）→ main → footer `.sig`（日期落款 + 返回首页链接）
- 正文构件：首段 drop-cap（`p:first-of-type::first-letter`）、分幕标题 `h2.act`（`<span class="no">Act I</span>标题`）、金句 `.pull`、图片 `figure` / 竖图 `figure.tall`（max-width 420px，`figcaption` 用 `<b>01 ·</b>` 编号）、收尾句 `.fin`

## 4. 图片规范

- 目录 `images/`，命名 `{文章slug}-{用途}.jpg`（如 `changsha-medal.jpg`）
- 压缩：横图宽 ≤1600px、竖图宽 ≤1200px，JPEG 质量 76–82，单张控制在 500KB 以内
- hero 用横图；竖图放文中用 `figure.tall`

## 5. 发布工作流（AI 与用户的分工）

1. **AI**：撰写文章页 HTML、更新首页卡片、压缩图片到 `images/`
2. **AI**：文字文件用 GitHub MCP `push_files` 推到 main（MCP 无法推二进制）；**推送前先 `list_tags` 报告现有 tag**
3. **用户**：图片在 GitHub 网页 Add file → Upload files 上传到 `images/`
4. **用户**：图片就位后打新 tag（git CLI `git tag -a` 或网页 Releases）
5. **AI**：验证——列 `images/` 目录核对字节数、curl 检查 mossmiles.hk 各页面与图片返回 200、截图核对渲染，然后汇报 commit sha 与线上状态
6. 文章源稿（md/docx）一并提交仓库根目录存档

## 6. 内容硬性规则

- 赛事成绩一律以官方成绩证书的**净成绩**为准，不用手表或 APP 数据
- 全马距离写标准里程 **42.195km**，不用手表记录的实际跑动距离
- 文章页与首页卡片上的年份、日期、成绩、距离必须完全一致
- 卡片摘要 `.desc` 一两句话，提炼文章的内核，不罗列情节
- 文章页署名落款写实际写作时间地点

## 7. 待办 / 想法池

- [ ] music.html（波士顿音乐节小提琴）从旧仓库 `carlson79/mossmiles` 迁移到 Nature & Humanities —— 待决定
- [ ] Investment Notes 第一篇论文阅读笔记 —— 占位中
