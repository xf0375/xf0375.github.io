# Xiao Fei Fei Blog

基于 `Hexo + NexT + GitHub Pages` 搭建的个人博客源码仓库。

线上地址：`https://xf0375.github.io`

## 1. 项目定位

这个博客目前主要承载 3 类内容：

- 学习笔记
- 周报 / 复盘
- 项目总结

首页以文章列表为主，额外保留 `About` 和 `Projects` 两个固定页面，方便后续做个人介绍和作品展示。

## 2. 技术架构

这套博客的核心链路可以理解成下面这几层：

```text
Markdown 内容
  -> source/
  -> Hexo 渲染
  -> public/ 静态文件
  -> hexo deploy
  -> gh-pages 分支
  -> GitHub Pages
  -> https://xf0375.github.io
```

当前技术栈：

- 博客框架：`Hexo 8`
- 主题：`NexT 8`
- 部署方式：`hexo-deployer-git`
- 托管平台：`GitHub Pages`
- 源码分支：`main`
- 发布分支：`gh-pages`

职责拆分如下：

- `main` 分支保存博客源码、配置、Markdown 内容
- `gh-pages` 分支保存生成后的静态站点文件
- GitHub Pages 从 `gh-pages / (root)` 发布线上页面

## 3. 目录结构

当前仓库的核心目录如下：

```text
blog/
├─ .github/                 # 仓库自动化配置（当前有 dependabot）
├─ .deploy_git/             # hexo deploy 生成的临时部署仓库
├─ node_modules/            # 项目依赖
├─ public/                  # hexo generate 输出的静态文件
├─ scaffolds/               # 新建文章 / 页面时使用的模板
├─ source/                  # 站点内容源文件
│  ├─ _posts/               # 博客文章
│  ├─ about/                # 关于页面
│  ├─ projects/             # 项目页面
│  ├─ tags/                 # 标签页
│  └─ categories/           # 分类页
├─ _config.yml              # Hexo 主配置
├─ _config.next.yml         # NexT 主题覆盖配置
├─ db.json                  # Hexo 缓存数据
├─ package.json             # 依赖与常用脚本
└─ README.md                # 当前说明文档
```

几个最重要的文件说明：

- `_config.yml`
  负责站点标题、作者、URL、文章链接格式、部署仓库等全局配置
- `_config.next.yml`
  负责菜单、社交链接等主题层配置
- `source/_posts/*.md`
  日常写文章主要就在这里
- `source/about/index.md`
  维护个人介绍页面
- `source/projects/index.md`
  维护项目展示页面

## 4. 本地开发环境

建议环境：

- `Node.js 18+`
- `Git`

当前仓库使用的依赖版本以 `package-lock.json` 为准。

首次进入项目：

```bash
npm install
```

本地启动预览：

```bash
npm run server
```

默认访问：

```text
http://localhost:4000
```

## 5. 常用命令

`package.json` 里已经整理好了常用脚本：

```bash
npm run clean    # 清理缓存和 public 输出
npm run build    # 生成静态文件
npm run server   # 本地启动预览
npm run deploy   # 部署到 gh-pages
```

如果你习惯直接用 Hexo 命令，也可以：

```bash
npx hexo clean
npx hexo generate
npx hexo server
npx hexo deploy
```

## 6. Blog 日常使用

### 6.1 新建文章

新建一篇文章：

```bash
npx hexo new post "my-first-post"
```

生成后的文件会放到：

```text
source/_posts/my-first-post.md
```

当前文章模板来自 `scaffolds/post.md`，默认结构是：

```md
---
title: 标题
date: 2026-04-19 10:00:00
tags:
---
```

建议你平时补全成下面这种写法：

```md
---
title: Java 并发学习记录
date: 2026-04-19 10:00:00
categories:
  - study-notes
tags:
  - Java
  - Concurrency
  - JVM
---
```

### 6.2 新建页面

如果后面要增加独立页面，比如 `friends` 或 `resume`：

```bash
npx hexo new page "friends"
```

会生成：

```text
source/friends/index.md
```

然后你可以再去 `_config.next.yml` 里补导航菜单。

### 6.3 修改 About 页面

直接编辑：

```text
source/about/index.md
```

适合放：

- 个人介绍
- 学习方向
- 联系方式
- 当前目标

### 6.4 修改 Projects 页面

直接编辑：

```text
source/projects/index.md
```

适合放：

- 项目名称
- 你的角色
- 技术栈
- 项目链接 / 仓库链接

### 6.5 本地预览内容

写完内容后先本地看效果：

```bash
npm run server
```

如果页面样式或内容没有刷新干净，可以先清理再重启：

```bash
npm run clean
npm run server
```

### 6.6 发布到线上

发布前建议先本地生成一次，确认没有报错：

```bash
npm run clean
npm run build
```

确认没问题后部署：

```bash
npm run deploy
```

这一步会把 `public/` 里的静态文件推到远程 `gh-pages` 分支，然后由 GitHub Pages 发布到线上。

## 7. 推荐发布流程

平时写完一篇文章，推荐按这个顺序走：

1. 编辑 `source/_posts/*.md`
2. 本地执行 `npm run server` 预览
3. 检查文章标题、分类、标签、排版
4. 执行 `npm run clean && npm run build`
5. 执行 `npm run deploy`
6. 打开 `https://xf0375.github.io` 检查线上效果

如果你也想把源码同步到 GitHub：

```bash
git add .
git commit -m "docs: add new post"
git push origin main
```

## 8. 配置说明

当前关键配置如下：

- 站点标题：`Xiao Fei Fei`
- 站点副标题：`Notes, weekly reviews, and project summaries`
- 站点语言：`zh-CN`
- 时区：`Asia/Shanghai`
- 主题：`next`
- 部署仓库：`https://github.com/xf0375/xf0375.github.io.git`
- 发布分支：`gh-pages`

导航菜单当前包含：

- 首页
- 归档
- 分类
- 标签
- 关于
- projects

## 9. 维护约定

下面这些约定很重要，能避免后面把站点弄乱：

- 不要手动编辑 `public/` 里的文件，它们是生成产物
- 不要手动编辑 `.deploy_git/`，它是部署临时目录
- 日常内容维护主要集中在 `source/`
- 站点行为和部署配置主要看 `_config.yml`
- 菜单和社交链接主要看 `_config.next.yml`
- 改完配置后，优先执行一次 `npm run clean`

## 10. 常见问题

### 10.1 为什么本地改了内容，线上没变？

通常是因为只改了源码，但还没有执行：

```bash
npm run deploy
```

### 10.2 为什么 GitHub Pages 打开是 404？

重点检查：

- 仓库名是否为 `xf0375.github.io`
- 仓库是否为 `Public`
- GitHub Pages 是否设置为从 `gh-pages / (root)` 发布
- 是否已经成功执行 `npm run deploy`

### 10.3 哪些文件是我最常改的？

一般就是这几个：

- `source/_posts/*.md`
- `source/about/index.md`
- `source/projects/index.md`
- `_config.next.yml`

## 11. 后续可扩展方向

当前这版站点已经适合稳定写作和上线，后面如果要增强，可以继续加：

- 评论系统
- 访问统计
- 自定义域名
- 更完整的项目展示页
- 自动化部署工作流

