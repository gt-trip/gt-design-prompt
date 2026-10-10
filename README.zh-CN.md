# 设计提示词词汇库

**把视觉设计想法，变成可以直接使用的提示词。**

面向 Web 与移动端界面的可视化词汇库与提示词组合工具。浏览 109 个设计词条，对照示意图理解含义，将风格、布局、材质、排版与配色组合成可复用的设计需求。

[English](README.md) · **简体中文**

[在线体验](https://gt-trip.github.io/gt-design-prompt/) · [反馈问题](https://github.com/gt-trip/gt-design-prompt/issues) · [部署状态](https://github.com/gt-trip/gt-design-prompt/actions/workflows/deploy-pages.yml)

## 为什么使用它？

“做得现代一点”留给执行者的解释空间太大。这个词汇库提供具体的设计语言，以及每个词对应的视觉参考，帮助你更准确地表达想要的效果。

你可以用它探索陌生的设计风格、整理设计需求，或为 AI 设计和编程工具准备提示词。从一个主风格开始，再补充项目真正需要的细节。

## 功能

- **可视化词汇**：八类共 109 个词条，包含英文关键词与中文解释。
- **文字 / 示意图切换**：支持全局切换与单个词条切换，切换时保留已选组合。
- **亮色 / 暗色模式**：工具栏可切换网页主题。未手动选择时跟随系统偏好，选择后通过 `localStorage` 记住主题。
- **提示词组合**：点击词条复制英文关键词，并按类别整理成完整提示词。
- **预设风格参考**：根据第一个选中的风格或氛围词，提供两组预设提示词模板。
- **响应式工作区**：宽屏使用右侧面板，小屏使用可展开的底部面板。
- **轻量图片资源**：WebP 照片采用懒加载与异步解码，结构示意图采用内联 SVG。
- **简单启动**：原生 HTML、CSS 与 JavaScript，无需安装依赖、构建工具、后端或 API Key。

应用当前使用中文界面与英文设计关键词。仓库默认展示[英文文档](README.md)，本页为中文入口。

## 词汇分类

| 分类 | 词条数 | 示例 |
| --- | ---: | --- |
| 风格锚点 | 24 | 玻璃拟态、便当盒布局、瑞士风格、日式北欧 |
| 布局结构 | 14 | 分屏、瀑布流、侧边栏后台 |
| 光效材质 | 16 | 极光、磨砂玻璃、胶片颗粒 |
| 排版气质 | 12 | 超大标题、衬线混搭、等宽数字 |
| 配色方案 | 12 | 莫兰迪、大地色、单色加点缀 |
| 氛围词 | 12 | 静奢、开发者工具、复古未来 |
| 移动端专属 | 10 | 底部导航、底部弹层、单手可达 |
| 负面清单 | 9 | 避免图库照片、图标堆砌与占位假文 |

应用还提供三个完整的组合范例，帮助你快速开始。

## 快速开始

直接打开[在线应用](https://gt-trip.github.io/gt-design-prompt/)，或使用 Python 3 在本地运行：

```bash
git clone https://github.com/gt-trip/gt-design-prompt.git
cd gt-design-prompt
python3 -m http.server 8000 --bind 127.0.0.1
```

访问[本地页面](http://localhost:8000/design-prompt-vocabulary.html)。按 `Ctrl+C` 停止服务。

建议通过 `localhost` 或 HTTPS 访问，并在浏览器提示时允许剪贴板权限，以便正常复制。

## 组合第一段提示词

1. 选择一个**风格锚点**；需要明确混搭时再添加第二个。
2. 补充所需的布局、材质、排版、配色与移动端模式。
3. 添加**负面清单**，说明结果应避免什么。
4. 在右侧或底部面板中查看组合结果，点击**复制整段**。
5. 将通用任务描述和参考图占位替换成实际产品、目标用户与参考图。

再次点击已选词条或面板中的标签即可移除，点击**清空**重新开始。顶部**文字 / 示意图**按钮可切换全部词条，每个词条也有独立切换按钮。

### 设计需求示例

下面是一段使用词汇库中术语编写的中文示例：

```text
设计一个移动端冥想 App，采用 Japandi 日式北欧极简风格与 SPA & wellness
疗愈氛围。使用奶油色与大地色配色、柔软的哑光黏土材质、衬线标题搭配
无衬线正文，以及充足留白。包含底部 Tab 导航，主要操作应单手可达。
不要图库照片，不要过多图标。参考附图中的氛围与材质。
```

## 工作原理

提示词由浏览器根据预定义规则组合，应用不调用 AI 服务。相似风格参考来自固定映射选择的预设模板。

已选词条保存在当前页面内存中，刷新后重置。浏览器的 `localStorage` 仅保存全局文字 / 示意图展示偏好。

颜色主题保存在 `localStorage` 的 `vocabulary-theme` 键中。如果没有已保存的主题，应用使用浏览器的 `prefers-color-scheme` 设置。

## 项目结构

```text
.
├── design-prompt-vocabulary.html   # 界面、样式、图例与应用逻辑
├── assets/                         # WebP 图片资源
├── .github/workflows/
│   └── deploy-pages.yml            # GitHub Pages 部署
├── README.md                       # 英文文档
└── README.zh-CN.md                 # 中文文档
```

### 自定义词汇库

编辑 `design-prompt-vocabulary.html`：

| 位置 | 用途 |
| --- | --- |
| `.chip` 元素 | 词条标题与解释；`data-copy` 提供英文关键词，`data-p` 指定对应图例 |
| `P` | 图例内容与说明 |
| `RECIPE` / `RNAME` | 预设提示词模板及名称 |
| `SIM` / `VSIM` | 风格与氛围词对应的相似模板映射 |
| `CAT` | 组合提示词使用的分类名称 |

位图统一使用 WebP，图片路径使用相对路径，以兼容 GitHub Pages 的仓库子路径。照片应作为独立文件保存，避免以 Base64 内嵌进 HTML。

## 部署自己的版本

仓库提供 [GitHub Pages 工作流](.github/workflows/deploy-pages.yml)。

1. Fork 本仓库，或将项目复制到自己的 GitHub 仓库。
2. 在 **Settings → Pages** 中，将 **Build and deployment → Source** 设置为 **GitHub Actions**。
3. 推送代码到 `main`，或在 **Actions** 中手动运行 **Deploy to GitHub Pages**。
4. 部署成功后，访问该次工作流 `github-pages` 环境显示的地址。

工作流将 HTML 同时发布为 `index.html` 与 `design-prompt-vocabulary.html`，并复制 `assets/`。README 文件作为仓库文档保留，不进入部署站点。

## 参与贡献

欢迎补充实用设计词汇、改进示意图、优化解释、修复无障碍问题，或完善文档。

- 通过 [Issue](https://github.com/gt-trip/gt-design-prompt/issues) 反馈问题或提出建议。界面问题请附上浏览器、视口尺寸与复现步骤。
- 每个改动聚焦一个问题，并在 Pull Request 中说明改进之处。
- 修改应用时，检查桌面和手机布局、两种展示模式，以及选择、移除、清空和复制功能。
- 修改文档所述行为时，同步维护[英文](README.md)和[中文](README.zh-CN.md)文档。
