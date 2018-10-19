---
title: "Hugo笔记"
date: 2018-10-17T19:43:12+08:00
showDate: true
draft: false
categories: ["Code"]
tags: ["Hugo"]
---

## GitHub Repository

New repostory > Repostory name: \<yourusername>

## SSH Key

```
$ cd ~/.ssh
$ ssh-keygen -t rsa -C <youremail>
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/your_user_directory/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): <passphrase>
Enter same passphrase again: <passphrase>
```

这步做完我才发现文件夹里不知道为什么有个去年生成的key……算了。

把id_rsa.pub文件里的内容添加到Account Settings > SSH Public keys > add another public keys

```
git config user.name <username>
git config user.email <email>
```

多账号千万不要瞎用`--global`……\
`git config --list`可以检查当前账号。

## Hugo

下载[Hugo](https://github.com/gohugoio/hugo/releases)，添加到环境变量。

```bash
hugo new site <yoursitefolder>
cd <yoursitefolder>
git init
git remote add origin git@github.com:sekhet-aaru/sekhet-aaru.github.io.git
```

### 添加模板

```bash
git submodule add https://github.com/vickylai/hugo-theme-sam.git themes/sam
```

模板可以用clone。添加为submodule利于更新。

### 基本设置

`params`是模板参数。

```toml
baseURL = "https://sekhet-aaru.github.io/"
languageCode = "zh-CN"
defaultContentLanguage = "zh-CN"
title = "苇原"
theme = "sam"
hasCJKLanguage = true
enableEmoji = true
enableRobotsTXT = true

[params]
    author = "lanee"
    description = "杂学阅读笔记"
    homepage = "Home"
    footerText = "© lanee 2018 | Powered by [Hugo](https://gohugo.io/) | Theme based on [Sam](https://github.com/vickylai/hugo-theme-sam)"

[permalinks]
    post = "/:title/"

[blackfriday]
    hrefTargetBlank = true

[[params.mainMenu]]
    link = "/posts"
    text = "Notes"

[[params.mainMenu]]
    link = "/code"
    text = "Code"

[[params.mainMenu]]
    link = "/about"
    text = "About"
```

Hugo markdown的hard line breaks问题一箩筐，被迫关闭。我至今没见过没有坑的markdown parser，我竟然还没有被劝退。

### 新建页面

```bash
hugo new about.md
hugo new posts/post-title.md
```

### Front Matter

```toml
title: "Hugo笔记"
date: 2018-10-17T19:43:12+08:00
showDate: false
draft: false
tags: ["",""]
categories: ["",""]
keywords: ["",""]
```

### 本地预览

```bash
hugo server
```
基本上是即时预览，有时候会出现不同程度的延迟，原因不明。

### 生成页面

```bash
hugo
```

生成内容在public文件夹下。

总而言之关于Hugo的部分多看几遍官方文档，很烦我知道。


## 提交

把public下的内容提交到GitHub。cd错了请清空重来。

```bash
git submodule add -b master git@github.com:sekhet-aaru/sekhet-aaru.github.io.git public
cd public
git add .
git commit -m <必填>
git push origin master
```
也可以用GitHub Desktop clone到本地，然后把public下内容复制过去再GitHub Desktop同步。但我觉得这太多此一举了。

于是在git commit和git push上栽了一个小时。

---

参考列表：

1. [如何搭建一个独立博客——简明 GitHub Pages与 jekyll 教程](http://www.cnfeat.com/blog/2014/05/11/how-to-build-a-blog/)
2. [GitHub IO配合HuGo搭建个人静态博客](https://mikoto10032.github.io/post/程序员那些事/github-io配合hugo搭建个人静态博客/)
3. [使用Hugo+Github Pages建置Blog](https://www.jianshu.com/p/58c644011f7d)
4. [Hugo 从入门到会用](https://blog.olowolo.com/post/hugo-quick-start/)