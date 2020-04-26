---
title: 关于 hexo 博客搭建与 Next 主题优化——第一部分
tags:
- hexo
- Next
categories:
- 博客
- hexo
- Next
abbrlink: aa2b6a17
---

## 前言

把 hexo 博客搭建与 next 主题优化的过程记录下来，以便日后参考。

本文分为三个部分：

* Hexo 的搭建与部署
* Next 主题的基本设置
* Next 主题的深度美化

> 本文基于目前最新的 Next7 主题 7.8.0，其它版本仅做参考。

<!-- more -->

---

## Hexo 的搭建与部署

### 什么是 Hexo

Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 [Markdown](http://daringfireball.net/projects/markdown/)（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

### 环境搭建

在安装 hexo 框架之前，我们需要先安装该框架的依赖环境：

1. Node.js
2. Git

#### Node.js 安装

因为 Hexo 框架是基于 Node.js 渲染的，所以必须要安装 Node.js 环境。

Windows：

* 可以前往 [Node.js](https://nodejs.org/en/download/ "Node.js官网") 官网下载

* 也可以去 [淘宝 Node.js 镜像](https://npm.taobao.org/mirrors/node "淘宝 Node.js 镜像") 下载

关于版本：选择 LTS 版本即可。

#### Git 安装

Git 用于管理你的 hexo 博客文章，帮助我们部署到 Github Pages 静态仓库上。

Windows：

* 去 [Git官网](https://gitforwindows.org/ "Git官网") 下载

* 建议前往 [淘宝 Git for Windows 镜像](https://npm.taobao.org/mirrors/git-for-windows/ "淘宝 Git for Windows 镜像") 下载

#### 安装完成验证

在 Git Bash 中输入以下命令。

##### Node.js 验证

```
node -v
npm -v
```

##### Git 验证

```
git --version
```



### Hexo 安装

**本文安装环境是基于 Windows10，以下操作均以 Windows 操作系统下安装为例。**

> 注意事项：
>
> * 建议只是用 Git Bash 来执行命令，cmd 中部分命令可能会出现一些问题。
> * 由于使用 `npm` 安装速度慢，可以选择安装淘宝的源
> * 在 Git Bash 中输入以下命令
>
> ```
> npm install -g cnpm --registry=https://registry.npm.taobao.org
> ```
>
> > -g 全局安装
> >
> > registry 镜像源，指向淘宝
>
> * 安装完成后，可以使用命令 `cnpm`、`cnpm -v` 验证
> * **以下 `npm` 命令均可使用 `cnpm` 代替**



#### 安装 Hexo

在 Git Bash 中输入以下命令，等待安装完成。

```
npm install -g hexo-cli
```

安装完成后，可以使用 `hexo -v` 验证。



#### 初始化 hexo

##### 创建 hexo 博客根文件夹，并初始化

这个文件夹是你以后存放博客代码与文章的地方，如果搭建过程出现了什么错误把它删掉重来即可。

执行以下命令，hexo 会在你当前所在的路径创建你指定的文件夹。

```
hexo init (folder)
cd blog //进入博客根文件夹
npm install
```

`(folder)`为指定文件夹，如：`hexo init blog`

`hexo init (folder)`这个命令执行时间比较长，请耐心等待。如果初始化失败可以将这个文件夹删掉重试。

初始化完成后，打开这个文件夹，可以看到里面的目录如下：

> * `node_modules`: 依赖包
> * `public`：存放生成的页面
> * `scaffolds`：生成文章的一些模板
> * `source`：用来存放你的文章
> * `themes`：存放主题
> * <font color=red>**`_config.yml`: 站点配置文件**</font>

现在我们的 hexo 博客已经搭建成功了。在 git bash 输入以下命令

```
//进入 hexo 根目录
hexo g
hexo s
```

> hexo g：hexo generate 的缩写
>
> hexo s：hexo sever 的缩写

此时，我们可以打开浏览器，输入 `localhost:4000` ，可以看见出现了 hexo 的默认主题。

**输入 `ctrl + c` 可以结束服务。**



### 把 hexo 博客部署到 github page

> 为什么要把 hexo 部署到 GitHub 上？
>
> 1. 免费
> 2. 可以随意绑定自己的域名，不用备案
> 3. 可以一键开启 HTTPS
>
> 4. ......

#### 在 github 创建个人仓库

首先，你需要注册一个 GitHub 账号，可以前往 [GitHub 官网](https://github.com/) 注册。

#### 创建 GitHub 个人仓库

在 [GitHub 官网](https://github.com/) 上可以看见一个 New repository ,点击可以新建仓库。

注意：创建的**仓库名**必须为<font color=red> `GitHub 用户名.github.io` </font>，勾选公开 `Public` 状态，可以选择勾选 README 选项。

这样设置后，我们可以在不绑定域名的情况下，使用 `GitHub 用户名.github.io` 访问我们的博客。

#### 生成 SSH key

> 如果是第一次在自己的电脑上使用 git 上传到 GitHub，那么必须要配置 `SSH key`，表示 GitHub 允许这台机器有权限使用 git 上传代码到远端仓库。

可以使用命令 `cd ~/.ssh` 查看本机是否已存在 ssh 密钥，如果显示 `No such file or directory` 则表示不存在；如果不是的话，可以选择使用已经存在的密钥或者重新生成一份。

##### 设置 git 提交的用户信息 

使用 git bash，输入以下命令

```
git config --global user.name "GitHub 用户名"
git congit --global user.eamil "绑定 GitHub 的邮箱"
```

检查信息有没有输入正确可以使用以下指令

```
git config user.name
git config user.email
```

##### 创建 SSH key

```
ssh-keygen -t rsa -C "GitHub 邮箱"
```

之后连续回车，最终会在 C 盘生成一个 `.ssh` 文件夹。

在你的电脑里找到这个 `.ssh` 文件夹并打开，把 `id_rsa.pub` 里面的内容复制，然后打开 [GitHub 官网](https://github.com/) 打开 `Setting`，找到 `SSH and GPG keys` ，点击 `New SSH key`，把刚才从 `id_rsa.pub` 复制的内容粘贴进去。

> `id_rsa` 是你的电脑的私人密钥，不能给别人看，`id_rsa_pub` 是公共密钥，可以随便给别人看。
>
> 把公钥放在 GitHub 上后，当你连接自己的账户时，他会根据公钥匹配匹配你的私钥，如果相互匹配，才能通过 git 上传你的文件到 GitHub 上。

##### 检查是否成功

在 git bash 中输入以下命令查看是否成功

```
ssh -T git@github.com
```

如果提示 `You've successfully authenticated, but GitHub does not provide shell access.` 说明 SSH 配置成功了。

#### 把 hexo 部署到 GitHub

这一步，我们可以将 hexo 与 GitHub 关联起来，将 hexo 生成的静态网页部署到 GitHub 上。

进入 hexo 根目录，打开站点配置文件 `_config.yml`，找到 deploy ，修改成以下配置

```
deploy:
  type: git
  repository: https://github.com/GitHub 用户名/GitHub 用户名.github.io.git 
  branch: master
```

此时，我们还需要安装一个插件 `hexo-deployer-git` ，才能使用部署的命令。

在 git bash 中输入以下命令

```
//进入 hexo 博客根目录
npm install hexo-deployer-git --save
```

然后，我们可以使用以下命令一键部署到 GitHub 上

```
hexo clean && hexo g && hexo d
```

> hexo clean 即清除你之前生成的东西，可以不加。
>
> hexo g 即 hexo generate 的缩写，生成静态文件
>
> hexo d 即 hexo deploy 的缩写，部署文章

## 参考

* [Hexo博客+Next主题深度优化与定制](https://bestzuo.cn/posts/blog-establish.html#主题自带样式代码块高亮)

* [hexo史上最全搭建教程](https://blog.csdn.net/sinat_37781304/article/details/82729029?depth_1-)