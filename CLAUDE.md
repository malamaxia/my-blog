# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目简介

MkDocs 静态博客（"麻虾的技术站"），使用 Material 主题，部署至 GitHub Pages。内容为 Markdown，配置为 YAML。

## 本地环境安装

```bash
pip install -r requirements.txt
```

## 常用命令

```bash
# 开发服务器（热重载，访问 http://127.0.0.1:8000）
mkdocs serve

# 生产构建 —— 有警告或死链时直接报错，输出到 site/
mkdocs build --strict

# 验证 YAML 语法
python -c "import yaml; yaml.safe_load(open('mkdocs.yml'))"
```

## 部署

推送到 `master` 分支 → GitHub Actions 自动执行 `mkdocs build --strict --site-dir _site` 并部署到 GitHub Pages。详见 `.github/workflows/deploy.yml`。

> 注意：CI 使用 `--site-dir _site`，本地默认输出到 `site/`，两者均不应提交到版本库。

## 项目结构

- `mkdocs.yml` — 站点名称、Material 主题、导航树、插件、Markdown 扩展
- `requirements.txt` — Python 依赖（mkdocs、mkdocs-material、pymdown-extensions）
- `docs/index.md` — 首页
- `docs/articles/` — 博客文章
- `docs/assets/images/` — 图片资源

## 新增文章

1. 创建 `docs/articles/your-title.md`（front matter 可选，推荐加上）：
   ```yaml
   ---
   title: 标题
   date: 2024-01-01
   tags: [标签1]
   ---
   ```
2. 在 `mkdocs.yml` 的 `nav:` 中手动注册该文件路径。

> 文件名中避免使用空格；若必须使用，`nav:` 中的路径同样需要带空格，且 `mkdocs build --strict` 可能对此敏感。

## 已启用的 Markdown 扩展

- `admonition` — 提示框（`!!! note`、`!!! warning` 等）
- `toc` — 自动生成目录，标题带永久链接
- `pymdownx.highlight` — 代码块语法高亮（行号锚点）
- `pymdownx.superfences` — 支持嵌套代码块、Mermaid 图表
- `pymdownx.tabbed` — 内容选项卡（`alternate_style: true`）
- `pymdownx.details` — 可折叠内容块（`???` 语法）
- `pymdownx.inlinehilite` — 行内代码高亮
- `pymdownx.snippets` — 文件片段引入
- `attr_list` / `md_in_html` — HTML 元素属性与 Markdown 嵌套

## 注意事项

- YAML 键名必须小写（用 `site_name`，不用 `siteName`）
- 文档间链接使用相对路径
- 推送前必须通过 `mkdocs build --strict`，警告即视为错误
