# 设计提示词词汇库

面向 Web 与移动端设计的中英双语提示词工具。通过可视化词条选择风格、布局、光效、排版与配色，组合出可直接复制使用的设计提示词。

[在线访问](https://gt-trip.github.io/gt-design-prompt/) · [部署记录](https://github.com/gt-trip/gt-design-prompt/actions/workflows/deploy-pages.yml)

> 在线地址在首次 GitHub Pages 部署成功后生效。

## 功能

- **分类词汇**：风格锚点、布局结构、光效材质、排版气质、配色方案、氛围词、移动端专属、负面清单，以及组合范例。
- **图例预览**：鼠标悬停词条查看对应效果；点击词条也会短暂显示图例。
- **关键词复制**：点击词条复制英文关键词，同时加入或移出当前组合。
- **提示词组合**：底部面板按类别整理已选词条，支持复制整段、清空和展开查看。
- **相似风格参考**：根据所选风格或氛围，提供两组预设提示词模板。

页面使用原生 HTML、CSS 和 JavaScript，无需安装依赖、构建工具或后端。提示词组合在浏览器中按规则生成，未调用 AI 服务；已选词条仅保留在当前页面，刷新后重置。

## 本地预览

在项目目录运行（需要 Python 3）：

```bash
python3 -m http.server 8000 --bind 127.0.0.1
```

浏览器打开 [本地页面](http://localhost:8000/design-prompt-vocabulary.html)。按 `Ctrl+C` 停止服务。

复制功能需要浏览器允许访问剪贴板，推荐通过 `localhost` 或 HTTPS 打开页面。

## 使用方式

1. 先选择一个风格锚点，再补充布局、光效、排版、配色等词条。
2. 点击底部「展开提示词」或顶部「我的提示词组合」，查看组合与相似风格模板。
3. 点击「复制整段」，按实际需求替换任务描述与「参考图 X」。
4. 再次点击已选词条可移除；点击「清空」重置组合。

## GitHub Pages 自动部署

仓库已提供 [部署工作流](.github/workflows/deploy-pages.yml)。推送到 `main` 会自动部署，也支持在 Actions 页面手动运行。

### 首次启用

1. 将本项目及工作流提交并推送至 GitHub 仓库 `gt-trip/gt-design-prompt`。
2. 打开仓库 [Settings → Pages](https://github.com/gt-trip/gt-design-prompt/settings/pages)，将 **Build and deployment → Source** 设为 **GitHub Actions**。
3. 若此前的推送尚未成功部署，打开 [Actions](https://github.com/gt-trip/gt-design-prompt/actions/workflows/deploy-pages.yml)，选择 **Deploy to GitHub Pages → Run workflow → main**。
4. 等待工作流成功，访问 <https://gt-trip.github.io/gt-design-prompt/>。实际地址也会显示在该次运行的 `github-pages` 环境中。

启用 Pages 需要仓库设置权限，仓库也需要满足当前 GitHub 套餐的 Pages 使用条件。工作流使用自动提供的 `GITHUB_TOKEN`，无需配置个人访问令牌或额外 Secrets。

### 发布内容

工作流将 `design-prompt-vocabulary.html` 复制为发布目录 `_site/index.html`，同时保留原文件名入口，并复制 `assets/` 图片资源。两种地址均可访问：

- 首页：<https://gt-trip.github.io/gt-design-prompt/>
- 原文件入口：<https://gt-trip.github.io/gt-design-prompt/design-prompt-vocabulary.html>

发布目录包含 `.nojekyll`，按静态文件发布；README、工作流配置和本地工作记录不进入网站，图片目录中的 `.DS_Store` 也会被排除。

之后修改页面或图片，提交并推送到 `main` 即可自动更新网站。若部署失败，查看 Actions 中的失败步骤，并确认 Pages 的发布来源和仓库 Actions 权限。

参考：[GitHub 官方自定义 Pages 工作流说明](https://docs.github.com/zh/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages)。

## 项目结构

```text
.
├── design-prompt-vocabulary.html   # 页面、样式、图例与交互逻辑
├── assets/                         # 图片资源
├── .github/workflows/
│   └── deploy-pages.yml            # GitHub Pages 自动部署
├── .gitignore
└── README.md
```

维护词条时，在 HTML 中修改 `.chip` 元素；`data-copy` 是复制与组合使用的英文关键词，`data-p` 对应脚本中的图例键。图例、预设组合和相似风格映射分别位于 `P`、`RECIPE`、`SIM` 与 `VSIM` 中。图片路径应使用相对路径，以兼容 GitHub Pages 的仓库子路径。
