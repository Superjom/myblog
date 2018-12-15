---
title: "Hugo 博客使用日志"
date: 2018-10-14T22:20:19+08:00
draft: true
tags: [hugo, blog]
categories: [blog, tools]

---

记录 Hugo 博客使用的一些经验

# Quick-start

```bash
# Create a new blog
hugo new site <blog-directory-name>

cd <blog-name>
git init
# Install a theme
git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke

# Create a new blog post
hugo new posts/<post-file-name>

# Start web service
hugo server -D
```

# Tag 和 Category 支持

在 `config.toml` 中添加

```sh
[taxonomies]
   tag = "tags"
   category = "categories"
```



在文章中按需增加 header comments 类似如下内容

```
categories: [development, publishing]
tags: [hugo,content,static site generator]
```

