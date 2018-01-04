---
title: Hexo+Yilia+travis+github 个人博客 简洁至上
date: 2018-01-04 1:39:04
tags: [前端,CI]
---
<img width="600" height="600" src="/asserts/heox.png"/>

**[Demo](http://rogerabyss.top), 欢迎Star我**
[please star me!!](https://github.com/RogerAbyss/RogerAbyss.github.io)

我们准备用**hexo+yilia+travis** 搭建一个**简洁至上的个人博客**
**我们不需要域名, 不需要空间或者服务器, 只需要一个github账号**
我们只需要本地修改测试代码然后提交git, **使用travis CI自动上传到github**

<!--more-->

## 准备工作

- [x] 一颗想搞事的心
- [x] 一点点编程基础
- [x] node环境
- [x] git环境
- [x] hexo框架
- [x] 一个github账号
- [x] 一个文本编辑器
- [x] 主题yilia
- [x] travis CI

## 第一步 准备环境

**以下环境为MacOS的安装环境, 如果是Linux或者Windows系统请按步骤根据官方文档自己安装环境**

安装node环境, [homebrew官网](https://brew.sh/index_zh-cn.html)
```
# 如果你有homebrew, 跳过此步骤
# 安装homebrew, MacOS包管理软件
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

# 安装node
brew install node
```

安装git
```
brew install git
```

安装hexo, [hexo官网](https://hexo.io)
```
npm install hexo-cli -g
hexo
```

注册一个github账号, [github](https://github.com)
准备一个文本编辑器, 本人推荐**vscode**,**webstorm**

## 开始创建博客

**创建代码仓库**
在github上创建一个代码仓库, 名称``xxx.github.io``, 将来将会用这个地址打开博客。

**在哪里搞事情?**
就在桌面吧, 打开**Terminal**

```
# 进入桌面
cd ~/Desktop
# 创建一个文件夹 blog
mkdir blog && cd blog
# 克隆代码仓库
git clone https://{仓库地址}
# 创建博客模板
hexo init
# 生成静态文件
hexo g
# 启动node.js服务器
hexo s
```

打开http://localhost:4000/
看看我们的博客吧！

好像有哪里不对？
**对, 不好看！**

## 使用好看的yilia主题

**不喜欢也可以自己找其他主题**,[找主题](https://hexo.io/themes)

在刚刚创建的blog目录下,下载yilia
```
# 进入刚刚的目录
cd ~/Desktop/blog

# 下载yilia
git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia

# 删除.git, 这样才能提交
cd themes/yilia
rm -rf .git
```

修改根目录下的``_config.yml``,搜索``theme=``修改为``theme=yilia``
关于yilia目录内的``config.yml``, 可以参考[yilia](https://github.com/litten/hexo-theme-yilia)

大功告成！
```
# Ctrl+C 关闭之后进行下面的操作

# 清理缓存
hexo clean

# 重新运行
hexo g
hexo s
```

打开http://localhost:4000/
看看我们的博客吧！

## 如何使用hexo维护我们的博客

**授人以鱼不如授人以渔**

#### node.js

hexo是一个基于node.js的框架, 所以我们首先要有一点node.js的知识。
常用的使用npm,yarn的姿势应该要有。
node_modules里面就是node.js的包, ```npm install```重新安装依赖可以解决大部分问题。

附:
- [node.js中文网](http://nodejs.cn)

#### hexo - config.yml

配置文件``config.yml``, 管理了大部分功能。
可以参考我的博客``dev``分支, 我给了大部分config.yml的注释, 欢迎大家指正。

附:
- [我的博客源码](https://github.com/RogerAbyss/RogerAbyss.github.io/tree/dev)

#### hexo - _posts

位于``source/_posts``目录下就是我们的博文了。
博文是.md格式大家都知道了, 下面给大家讲讲简单的功能
``title: 标题``
``date:  日期``
``tags:  标签``
``<!--more--> 折叠文章``

#### hexo - 其他

我遇到过这样的情况, 因为整个博客都是约定好的theme。
如果我需要新建一个页面, 里面所有的css都是我自己重新构思的呢？
根目录``config.yml``里``skip_render:``设置, 可以跳过模板的渲染。

## 利用Travis C, 自动构建发布到web

**开通Github Pages**

我们将利用``github pages``充当空间存放我们的个人博客。
进入我们仓库的``setting``, 打开``GitHub Pages``。
![github-pages](/asserts/github-pages.png)
(可选)GitHub访问速度并不快, 我们可以申请一个域名, 指向一个CNAME。
在根目录source里面, 创建一个空文件, 输入``{你的域名}``。

**开通/配置Travis CI**

[Travis CI官网](https://travis-ci.org)

通过github账号可以开通Travis CI, 享受开源完全免费。

我们需要在``Github->setting->Developer settings->Personal access tokens``生成一个repo访问权限的token。
![github-toekn](/asserts/github-token.png)
然后在Travis CI, 里开启此仓库的开关, 并且设置环境变量, 毕竟你不想密码被别人看到吧。
![traivs-setting](/asserts/travis-setting.png)
在文件根目录, 创建Travis配置文件``.travis.yml``。

分支``dev2``出来并且清空``master``分支, 我们的目的是, dev分支负责开发, master分支只包含博客代码。
详情参考我dev2分支的travis CI, 我写了详细的注释, 更多姿势请移步[Travis CI官方文档](https://docs.travis-ci.com)。

**大功告成, 现在git commit&push, 收到一封ravis CI成功的邮件, 看看我们的网站吧**
                                           

<br>
---
**如果你有任何的问题, 可以email我, 有空的时候我会回复**
**如果你觉得对你有帮助, 可以点击支持我一杯咖啡, 我会继续更新一些有用的东西**
