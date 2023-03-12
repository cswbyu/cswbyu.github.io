---
title: A Blog Is All You Need
index_img: img/post_cover/20230312-A-Blog-Is-All-You-Need.jpg
date: 2023-03-12 14:58:07
tags:
- 技术经验
categories:
- 技术经验
- 博客管理
---

本文主要介绍如何快速搭建一个私人博客（以发布一个在线网页为目标）。

<!-- more -->

# 搭建的技术方案

该博客在搭建过程中用到的技术有 `GitHub Pages` 、 `Hexo` 、 `Fluid` 。与它们相关的网络资源如下：

- `GitHub Pages` 的[官方主页](https://pages.github.com/)；
- `Hexo` 的[官方中文文档](https://hexo.io/zh-cn/docs/)；
- `Fluid` 的[中文用户手册](https://hexo.fluid-dev.com/docs/)。

在正式开始搭建之前，需要确保以下工作已经完成：

- 成功注册一个 `GitHub` 账号；
- 下载并安装好 `Node.js` ；
- 下载并安装好 `Git` 。

# 搭建步骤——以发布一个在线网页为目标

接下来的一系列步骤以最终能发布一个在线网页为目标，更细节、个性化的操作可以参考[前面介绍的官方文档](#搭建的技术方案)完成。

## 本地静态网站的搭建

### 准备工作

首先确保前面提到的 `Node.js` 以及 `Git` 都已正确安装。在终端分别输入命令 `node -v` 以及命令 `git -v` ，如果上述两者都已安装成功，那么会正确显示版本号。

### 安装 `Hexo`

该步骤非常简单，只需要在终端输入命令 `npm install hexo-cli -g` 。安装完毕后同样可以在终端输入命令 `hexo -v` 进行检测，如果正确输出版本号，则说明安装成功。

### 生成博客文件夹

随便挑选一个希望存放博客文件夹的目录（比如D盘），在该目录下打开 `Git Bash` 并输入命令

```bash
$ hexo init my_new_blog
```

新建一个名为 `my_new_blog` 的博客文件夹，再使用 `cd my_new_blog` 进入该文件夹。

### 访问本地静态网站

进入该博客文件夹后，输入命令 `npm install` 安装所依赖的库，然后输入命令 `hexo s` 即可在本地生成预览网页。

在浏览器中输入地址 `localhost:4000` 并访问，即可看到生成的本地预览网页。

## 切换主题为 `Fluid`

通过前面步骤所生成的网页默认使用 `landscape` 主题，接下来将介绍如何将其修改为 `Fluid` 主题。

直接在博客目录下执行命令 `npm install --save hexo-theme-fluid` 安装主题，然后删除目录下原有的 `_config.landscape.yml` 文件，新建一个 `_config.fluid.yml` 文件，并将[Fluid官方远程仓库的_config.yml文件](https://github.com/fluid-dev/hexo-theme-fluid/blob/master/_config.yml)的内容全部复制到 `_config.fluid.yml` 中去。

打开本地目录的 `_config.yml` 文件，并进行如下修改：

```yaml
theme: fluid  # 指定主题

language: zh-CN  # 指定语言，会影响主题显示的语言，按需修改
```

重新输入命令 `hexo s` 并访问 `localhost:4000` ，即可看到修改完主题后的静态网页。值得注意的是，文件 `_config.fluid.yml` 是主题 `Fluid` 的配置文件，注释详尽，可以结合用户手册的[配置指南](https://hexo.fluid-dev.com/docs/guide/)对其进行修改，实现网站风格的个性化定制。

## 将本地静态网站发布到 `GitHub` 上

首先登陆自己的 `GitHub` 账号，新建一个仓库，仓库名必须按照 `GitHub用户名.github.io` 的方式命名，否则会发布不成功。

然后建立当前主机与自己 `GitHub` 账号的 `SSH` 连接，具体可参考 `GitHub` 关于这一部分的[官方文档](https://docs.github.com/cn/authentication/connecting-to-github-with-ssh)。

修改博客目录下 `_config.yml` 文件的参数：

- `# URL` 部分
  - 修改 `url:` 的值为 `https://GitHub用户名.github.io` ；
- `# Deployment` 部分
  - 修改 `type:` 的值为 `git` ；
  - 修改 `repo:` 的值为 `https://github.com/GitHub用户名/GitHub用户名.github.io` ；
  - 修改 `branch:` 的值为 `main` 。

现在，在我们正式发布到 `GitHub` 之前，可以先使用命令 `hexo new "网页名"` 创建一个全新的网页。在博客目录下的 `source/_posts` 中，找到这个网页对应的 `.md` 文件，修改 `.md` 文件，就能修改网页内容。

然后，执行命令 `npm install hexo-deployer-git --save` 安装 `hexo-deployer-git` ，再依次执行命令 `hexo cl` 、 `hexo g` 、 `hexo d` ，从而完成缓存清除、生成博客文件、提交网站到远程仓库的操作。

最后，访问地址 `https://GitHub用户名.github.io` ，将会看到所创建的博客网站已经被顺利发布，包括刚刚新创建的网页也被一同提交到了线上。

至此，本文已经顺利完成任务——发布一个在线网页。要实现更丰富更酷炫的功能，可以进一步阅读[前面介绍的官方文档](#搭建的技术方案)。
