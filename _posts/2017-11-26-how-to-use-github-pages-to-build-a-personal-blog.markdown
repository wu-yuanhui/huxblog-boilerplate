---
layout:     post
title:      "使用 Github pages 搭建个人博客简易教程"
subtitle:   "来撸一个自己的专属博客吧~"
date:       2017-11-26 16:00:00
author:     "伍源辉"
header-img: "img/2017-11-26.jpg"
tags:
    - 博客
    - 教程
    - 域名
    - 主机
    - Github Pages
    - Git
    - Jekyll
    - Markdown
    - Ruby
---

# 基础

## 注册 Github 帐号
https://github.com/

## 安装 Git 软件
https://git-for-windows.github.io/

## 设置 Git 的用户名和邮箱
```
$ git config --global user.name "{username}"          // 用你的用户名替换{username}
$ git config --global user.email "{name@site.com}"    // 用你的邮箱替换{name@site.com}
```

## 生成本地电脑的 SSH key
```
$ ssh-keygen -t rsa -C "{name@site.com}"              // 用你的邮箱替换{name@site.com}
cat C:\Users\{your_computer_name}\.ssh\id_rsa.pub     // 打印输出 SSH key 公钥
```

## 添加本机 SSH key 到 Github
依次点击：用户头像 - Settings - SSH and GPG keys - New SSH key

## 通过 hello world 例子学习 Github 的使用
https://guides.github.com/activities/hello-world/

> 学习完之后可以在当前仓库的 `Settings` 标签页的最下方点击 `Delete this repository` 删除仓库

## 跟着 GitHub Pages 教程搭建个人博客项目
https://pages.github.com/

## 访问你的个人博客
http://{username}.github.io

---

# 进阶

## 了解 Jekyll
英文文档：https://jekyllrb.com/
中文文档：http://jekyll.com.cn/
中文文档：http://jekyllcn.com/

## 使用 Jekyll 搭建博客
https://jekyllrb.com/docs/quickstart/

## 挑选博客模版
https://github.com/jekyll/jekyll/wiki/sites

## 使用博客模版
依次点击：Fork - Settings - Repository name - {username}.github.io - Rename

## 购买域名（可选）
https://wanwang.aliyun.com/

## 设置 DNS 解析（可选）
https://www.dnspod.cn/

## 自定义博客域名
https://help.github.com/articles/using-a-custom-domain-with-github-pages/
https://help.github.com/articles/troubleshooting-custom-domains/
依次点击：CNAME file - Edit - Change or Delete Content - Commit

---

# 开始写作

## Clone 博客到本机
```
$ git clone https://github.com/{username}/{username}.github.io.git     // 用你的Github用户名替换{username}
```

## 安装 Ruby
http://rubyinstaller.org/downloads/
Remember to check "Add Ruby executables to your PATH"

## 安装 RubyGems
https://rubygems.org/pages/download
> 下载 zip 版本，解压，Win+R，cmd，Enter

```
$ cd {unzip-path}  //如果你不是解压在C盘，windows的终端切换到其他盘需要写为 cd /d {unzip-path}
$ ruby setup.rb
```

## 安装 Jekyll
```
$ gem install jekyll
```

## 安装jekyll-paginate
```
$ gem install jekyll-paginate
```

## 修改 Ruby 源
https://gems.ruby-china.org/

## 实时预览
```
$ cd {local repository} // {local repository}替换成你的本地仓库的目录
$ jekyll serve
$ curl http://localhost:4000/
```

## 下载 MarkdownPad
http://markdownpad.com/download.html

## 了解 Markdown 语法
http://sspai.com/25137

## 撰写博文
```
$ cd _posts
$ cp 2016-03-03-hello-world.markdown 2017-07-07-hello-earth.markdown
```

## 发布到互联网
```
$ git status
$ git add .
$ git commit -m "my first post"
$ git push origin master
```

---

## 更多教程
https://help.github.com/categories/github-pages-basics/
https://help.github.com/articles/troubleshooting-github-pages-builds/

## 了解 GitHub 的工作流程
https://guides.github.com/introduction/flow/

## 参考：
http://playingfingers.com/2016/03/26/build-a-blog/

