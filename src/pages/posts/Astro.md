---
layout: '../../layouts/MarkdownPost.astro'
title: '搭建一个有果味的静态博客-Astro'
pubDate: 2023-02-23
description: ''
author: 'Steve'
cover:
    url: 'https://cdn.staticaly.com/gh/zxfccmm/image@master/20230223/7.6zducpj8j5w0.webp'
    square: 'https://cdn.staticaly.com/gh/zxfccmm/image@master/20230223/7.6zducpj8j5w0.webp'
    alt: 'cover'
tags: ["Steve 分享", "Blog", "Astro"]
theme: 'dark'
featured: false

---

## 前言

偶然在推上看到  **Austin aka 驭风** [@austin2035](https://github.com/austin2035)  大佬写的 Astro 博客这个项目,一时间觉得颜值耐打,还有一股熟悉的果味,很不错.想着就自己来搭建一个自己的博客.

## 预览

Steve : [https://blog.Steveee.me](https://blog.Steveee.me)

## 开始搭建

1.先去大佬的 github 上 Fork 一下该项目.  项目地址: https://github.com/austin2035/astro-air-blog

![Fork](https://cdn.staticaly.com/gh/zxfccmm/image@master/20230223/1.3idxttw527o0.webp)

2.把项目名称改为 xxx.github.io 其实 xxx 为你的用户名,如下图,用户名为 zxfccmm 即改为 zxfccmm.github.io 

之后点击创建.

![Name](https://cdn.staticaly.com/gh/zxfccmm/image@master/20230223/2.76qm28zxb180.webp)

3.接着就会到下面这个界面,我们新建一个文件点击 Add file - Create new file 

![Create new file](https://cdn.staticaly.com/gh/zxfccmm/image@master/20230223/3.4a6tqv87u4a0.webp)

在你的项目中的 `.github/workflows/` 目录创建一个新文件 `deploy.yml`，并粘贴以下 YAML 配置信息。

``` .github/workflows/deploy.yml ```

```yml
name: Github Pages Astro CI

on:
  # 每次推送到 `main` 分支时触发这个“工作流程”
  # 如果你使用了别的分支名，请按需将 `main` 替换成你的分支名
  push:
    branches: [ main ]
  # 允许你在 GitHub 上的 Actions 标签中手动触发此“工作流程”
  workflow_dispatch:
  
# 允许 job 克隆 repo 并创建一个 page deployment
permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout your repository using git
        uses: actions/checkout@v3
      - name: Install, build, and upload your site
        uses: withastro/action@v0

  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v1
```

4.接着我们点击 Settings - Pages - Source 选择 **Github Actions**



静等一会儿后会出现以下画面,使用 https://zxfccmm.github.io 即可访问博客主页

![GithubPages](https://cdn.staticaly.com/gh/zxfccmm/image@master/20230223/4.3m2yq27n7540.webp)

当然你也可以设置自己的域名,在 Custom domain 里面 设置自己的域名,别忘了在您的域名DNS CNAME 到 

xxx(你的用户名).github.io

![CNAME](https://cdn.staticaly.com/gh/zxfccmm/image@master/20230223/5.2sgaxz8owu20.webp)

还需要在下图位置添加 CNAME 文件

![CNAME](https://cdn.staticaly.com/gh/zxfccmm/image@master/20230223/CNAME.1fiago55cjr4.webp)

5.接着我们便可以得到以下的博客主页,他已经是可用的状态了.

## 使用其他方式部署

可以参考官方的教程十分详细：
**[部署教程](https://docs.astro.build/zh-cn/guides/deploy/)**

## 自定义成你的博客

```
|-- README.md
|-- astro.config.mjs
|-- package.json
|-- public
|   |-- favicon.svg
|   `-- static
|-- src
|   |-- components
|   |   |-- BaseHead.astro // common <head> tags
|   |   |-- Footer.astro
|   |   |-- Header.astro
|   |   `-- Navigation.astro
|   |-- consts.js
|   |-- env.d.ts
|   |-- layouts
|   |   |-- BaseLayout.astro
|   |   |-- MarkdownPost.astro
|   |   |-- MoreTile.astro
|   |   `-- Tile.astro
|   |-- pages
|   |   |-- about.astro
|   |   |-- archive.astro
|   |   |-- index.astro
|   |   |-- posts 
|   |   |   |-- some markdown post.md  // 这里写文章
|   |   |-- rss.xml.js // RSS feed
|   |   `-- tags
|   |       `-- [tag].astro // dynamic route of all posts with a given tag
|   |-- styles
|   |   `-- global.css // global styles
|   `-- utils.js
```



上面是博客的文件结构

### 发布文章

需要在 Posts 上上传 Markdown 文件

### 自定义博客

路径为``zxfccmm/zxfccmm.github.io/tree/main/src/pages/``

**archive.astro** 我们可以修改文章的标签

**about.astro**  设置您的关于页面

路径为``zxfccmm/zxfccmm.github.io/tree/main/src/consts.js/``

```js
export const SITE_TITLE = `Austin's Blog`;    
export const SITE_DESCRIPTION = 'Austin Site Description';
export const SITE_EMAIL = 'no.sql@qq.com'
export const SITE_NAME = 'astro-blog.qum.cc';
export const SITE_URL = "https://astro-blog.qum.cc";
```

路径为``zxfccmm/zxfccmm.github.io/tree/main/src/components/``

**Footer.astro**  可以修改页脚

到这一步,已经是一个可以用的博客了.

![Blog](https://cdn.staticaly.com/gh/zxfccmm/image@master/20230223/7.6zducpj8j5w0.webp)



![Blog2](https://cdn.staticaly.com/gh/zxfccmm/image@master/20230223/8.80po0irc580.webp)

