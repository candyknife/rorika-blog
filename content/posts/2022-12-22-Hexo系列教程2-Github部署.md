---
title: "Hexo 系列教程 2：Github 部署"
date: 2022-12-22
updated: 2023-06-06
categories: [技术]
tags: [Hexo]
---

## 配置 Git

打开 Windows Terminal 或者在菜单里搜索 Git Bash，取消 ssl 认证：

```bash
git config --global http.sslVerify false
```

设置 user.name 和 user.email 配置信息：

```bash
git config --global user.name "你的 GitHub 用户名"
git config --global user.email "你的 GitHub 注册邮箱"
```

生成 ssh 密钥文件：

```bash
ssh-keygen -t rsa -C "你的 GitHub 注册邮箱"
```

然后直接三个回车即可，默认不需要设置密码。你应该会看到如下输出：

```
Generating public/private rsa key pair.
Enter file in which to save the key (C:\Users\用户名/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in C:\Users\用户名/.ssh/id_rsa
Your public key has been saved in C:\Users\用户名/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:66taKe0S8vRMPMJnjCi/GaDgi+oEaPAJy71QEBFX7+Y
The key's randomart image is:
+---[RSA 3072]----+
| =+...           |
|  o   .          |
|o  .   .         |
|++o.  .          |
|*+o+ + oS        |
|B.+ B.X. .       |
|.=.=.O+E.        |
|o ooo+o.         |
|=oo..oo.o.       |
+----[SHA256]-----+
```

在 `C:\Users\用户名/.ssh/id_rsa.pub` 处找到生成的 `id_rsa.pub` 密钥，复制其中全部内容。

## 配置 Github

使用邮箱注册 GitHub 帐号并登录：[Github](https://github.com/)

点击右上角加号图标，选择 `New repository` 创建一个新仓库，仓库名为：**用户名.github.io**，该 **用户名** 使用自己的 GitHub 帐号名称代替。

打开 [GitHub_Settings_keys](https://github.com/settings/keys) 页面，点击 `New SSH key` 按钮，Title 处为本台计算机取一个名字，然后将刚刚复制的 `id_rsa.pub` 内容粘贴进去，最后点击 `Add SSH key`。

## 配置 Hexo

打开 blog 根目录里的 `_config.yml` 文件，也称为 **站点配置文件**。

在站点配置文件的最后，修改为如下形式并保存：

```yaml
deploy:
  type: git
  repo: https://用户名/用户名.github.io.git
  branch: main
```

打开 Windows Terminal 安装 Git 部署插件：

```bash
npm install hexo-deployer-git --save
```

## 部署博客到 Github Page

输入以下命令完成生成与部署：

```bash
hexo g
hexo d
```

完成后打开浏览器，在浏览器地址栏输入博客所在仓库的路径，即 "http://用户名.github.io"，即可通过互联网访问生成的博客。

> 更新于 2023-06-06
