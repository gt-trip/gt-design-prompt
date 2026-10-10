# Design Prompt Vocabulary

**Turn visual design ideas into a prompt you can use.**

A visual vocabulary and prompt builder for web and mobile interfaces. Explore 109 design terms, compare their diagrams, and combine styles, layouts, textures, typography, and colors into a reusable design brief.

**English** · [简体中文](README.zh-CN.md)

[Try the app](https://gt-trip.github.io/gt-design-prompt/) · [Report an issue](https://github.com/gt-trip/gt-design-prompt/issues) · [Deployment status](https://github.com/gt-trip/gt-design-prompt/actions/workflows/deploy-pages.yml)

## Why use it?

“Make it modern” leaves a lot to interpretation. This library gives you specific design language—and a visual reference for each term—so you can describe what you want with more precision.

Use it to explore unfamiliar styles, prepare a design brief, or build a prompt for an AI design or coding tool. Start with one style anchor, then add the details that matter to your project.

## Features

- **Visual vocabulary:** 109 terms across eight categories, with English keywords and Chinese explanations.
- **Text or diagrams:** switch every item at once or change individual items. Your selected terms stay in place when you switch views.
- **Prompt builder:** select terms to copy their English keywords and assemble a prompt organized by category.
- **Curated references:** get two preset prompt templates based on your first selected style or atmosphere term.
- **Responsive workspace:** a side panel on wide screens and an expandable bottom panel on smaller screens.
- **Lightweight assets:** WebP photos with lazy loading and asynchronous decoding, plus inline SVG diagrams.
- **Simple setup:** plain HTML, CSS, and JavaScript. No package installation, build step, backend, or API key required.

The app currently uses a Chinese interface with English design keywords. This README is the default English documentation; [Chinese documentation](README.zh-CN.md) is also available.

## Explore the vocabulary

| Category | Terms | Examples |
| --- | ---: | --- |
| Style anchors | 24 | Glassmorphism, Bento Grid, Swiss Style, Japandi |
| Layout | 14 | Split screen, masonry, sidebar dashboard |
| Light & texture | 16 | Aurora glow, frosted glass, film grain |
| Typography | 12 | Display headlines, serif pairing, tabular numbers |
| Color | 12 | Morandi, earth tones, monochrome with an accent |
| Atmosphere | 12 | Quiet luxury, developer tools, retro-futurism |
| Mobile patterns | 10 | Bottom tabs, bottom sheets, thumb-friendly actions |
| Negative constraints | 9 | Avoid stock photos, icon overload, placeholder content |

The app also includes three complete prompt examples to help you get started.

## Quick start

Open the [hosted app](https://gt-trip.github.io/gt-design-prompt/), or run it locally with Python 3:

```bash
git clone https://github.com/gt-trip/gt-design-prompt.git
cd gt-design-prompt
python3 -m http.server 8000 --bind 127.0.0.1
```

Visit [localhost:8000/design-prompt-vocabulary.html](http://localhost:8000/design-prompt-vocabulary.html). Press `Ctrl+C` to stop the server.

Use `localhost` or HTTPS and allow clipboard access when prompted for reliable copying.

## Build your first prompt

1. Choose one **style anchor**. Add a second only if you want a deliberate blend.
2. Select the layout, textures, typography, colors, and mobile patterns you need.
3. Add **negative constraints** to describe what the result should avoid.
4. Review the assembled prompt in the side or bottom panel and choose **复制整段** (Copy full prompt).
5. Replace the generic task description and reference-image placeholder with your actual product, audience, and reference.

Click a selected item or its tag again to remove it. Use **清空** (Clear) to start over. The **文字 / 示意图** controls switch between text and diagrams; each item has its own view toggle too.

### Example design brief

The following is an English example written using terms from the library:

```text
Design a mobile meditation app with a Japandi minimal style and a calming
SPA & wellness atmosphere. Use a cream and earth-tone palette, soft clay
surfaces, serif headlines paired with sans-serif body text, and generous
whitespace. Include bottom tab navigation and thumb-friendly primary actions.
Avoid stock photos and excessive icons. Use the attached reference image
for the intended mood and materials.
```

## How it works

Prompt assembly runs entirely in your browser using predefined rules. The app does not call an AI service. Similar-style references are curated templates selected through fixed mappings.

Selected terms are kept in memory and reset when you reload the page. Only your global text/diagram preference is saved in the browser's `localStorage`.

## Project structure

```text
.
├── design-prompt-vocabulary.html   # UI, styles, diagrams, and app logic
├── assets/                         # WebP image resources
├── .github/workflows/
│   └── deploy-pages.yml            # GitHub Pages deployment
├── README.md                       # English documentation
└── README.zh-CN.md                 # Chinese documentation
```

### Customize the library

Edit `design-prompt-vocabulary.html`:

| Source | Purpose |
| --- | --- |
| `.chip` elements | Term title and explanation; `data-copy` supplies the keyword and `data-p` identifies its diagram |
| `P` | Diagram markup and captions |
| `RECIPE` / `RNAME` | Preset prompt templates and their names |
| `SIM` / `VSIM` | Style and atmosphere mappings for related templates |
| `CAT` | Category names used in assembled prompts |

Use WebP for raster images and relative asset paths so the app works under a GitHub Pages repository subpath. Keep photos as separate files instead of embedding them as Base64.

## Deploy your own copy

The repository includes a [GitHub Pages workflow](.github/workflows/deploy-pages.yml).

1. Fork the repository or copy it into your own GitHub repository.
2. In **Settings → Pages**, set **Build and deployment → Source** to **GitHub Actions**.
3. Push to `main`, or run **Deploy to GitHub Pages** manually from the **Actions** tab.
4. Open the URL shown in the workflow's `github-pages` environment after deployment succeeds.

The workflow publishes the HTML as both `index.html` and `design-prompt-vocabulary.html`, together with `assets/`. README files remain repository documentation and are not included in the deployed site.

## Contributing

Contributions are welcome: add useful design terms, improve diagrams, refine explanations, fix accessibility issues, or improve the documentation.

- Open an [issue](https://github.com/gt-trip/gt-design-prompt/issues) for a bug or a proposed change. For UI bugs, include your browser, viewport size, and reproduction steps.
- Keep changes focused and describe what they improve in your pull request.
- For app changes, check desktop and mobile layouts, both display modes, term selection, removal, clearing, and clipboard behavior.
- Keep the [English](README.md) and [Chinese](README.zh-CN.md) documentation aligned when changing documented behavior.
