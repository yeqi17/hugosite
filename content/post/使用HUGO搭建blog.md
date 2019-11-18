---
title: "使用 Hugo 搭建 Blog"
date: 2019-11-18T11:18:15+08:00
draft:true
weight: 70
keywords: ["hugo"]
description: "Hugo 安装与配置"
tags: ["hugo", "pages"]
categories: ["pages"]
author: "yeqi"
---
## 1.安装HOGO

环境:mac

安装:

```shell
brew install hugo
```

hugo常用指令:

- hugo new 命令用于为网站生成新的内容, 其后可以接上命令也可以接上路径.
- hugo server , 该命令应该在网站根目录下运行, 然后启动 hugo 服务, 便可以在浏览器中输入网址来浏览生成的网站了.

## 2.创建网站

```bash
hugo new site hugosite
```

- 下载主题到hugosite的theme目录
- 如何设置主题为站点主题

## 3.搭建blog

以 user.github.io 为例, 用户名为 user.

申请 github 账号,新建两个 repo:

- user.github.io

  这个 repo 用来存储 hugo 编译后的静态网站.

- hugosite

  这个 repo 用来存储静态网站的原始文件.

  - 在本地新建 hugosite 文件夹

  ```shell
  hugo new site hugosite
  ```

  - 进入该文件夹

  ```shell
  cd hugosite
  ```

  - 与远程 hugosite repo 关联

  ```shell
  git init .
  git remote add origin git@github.com:<username>/hugosite.git
  ```

  - 配置主题

  ```shell
  cd hugosite/themes
  git clone https://github.com/keichi/vienna
  ```

  - 修改 hugosite/config.toml 

  ```shell
  baseURL = "https://user.github.io/"
  languageCode = "en-us"
  theme = "vienna"
  title = "PIS"
  copyright = '&copy; Theme from <a href="https://themes.gohugo.io/vienna/">vienna</a> '
  [params]
      subtitle = "subtile"
      contact = "mailto:xxx@gmail.com"
      author = "author name"
      avatar = "/images/boy.jpg"
      bio = "your bio"
  ```

  - 新建文章

  ```shell
  hugo new post/article.md
  ```

  该文件存在于content/post/article.md里.

  - 配置 github

  github 用户名和邮箱

  ```shell
  git config user.name "user"
  git config user.email "xxx@gmail.com" # xxx@gmail.com 修改为为你的邮箱
  ```

  - 使用travis-ci来自动完成hugosite到.io的部署,具体设置有待补充.

  ```bash
  i=#!/bin/bash
  echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"
  
  msg="rebuilding site `date`"
  if [ $# -eq 1 ]
    then msg="$1"
  fi
  
  # Push Hugo content
  git add -A
  git commit -m "$msg"
  git push origin master
  ```

  - 添加执行权限

  ```shell
  chmod +x
  ```

  - 预览

  ```shell
  hugo server
  ```



  注:部分内容引用自<http://ahageek.com/writer/posts/hugo/index.html>