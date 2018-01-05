---
title: Hexo+Yilia+travis+github 个人博客 简洁至上
date: 2018-01-05 1:39:04
tags: [前端,CI]
---
<img width="400" height="350" src="/asserts/heox.png"/>

不需要域名, 不需要租用空间或者服务器
**全免费**搭建简洁至上的个人博客。

<!--more-->  

**观看博客[Demo](http://rogerabyss.top)**
**你觉得不错,保存并且[Star Me!](https://github.com/RogerAbyss/RogerAbyss.github.io)**

<br>
# 准备工作

- 一颗想搞事的心和一点点编程基础
- 环境: node, git
- 框架: hexo
- 服务商: github, travis
- 工具: 文本编辑器
- 其他: yilia

**本文章所有操作在Macos系统下完成, 其他系统请参考步骤自己动手!!**
<br>

<br>
### 开始安装环境

**你可能需要安装homebrew**
```
# 如果你有homebrew, 跳过此步骤
# 安装homebrew, MacOS包管理软件
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

**1.安装node环境**
```
# 安装node
brew install node
```

**2.安装git环境**
```
# 安装node
brew install git
```

**3.安装hexo环境**
```
npm install hexo-cli -g
hexo
```

<br>
### 附录

- 科学上网-[如何科学上网](https://www.textarea.com/ExpectoPatronum/shiyong-shadowsocks-kexue-shangwang-265)
- MacOS包管理器-[homebrew官网](https://brew.sh/index_zh-cn.html)
- 搭建微型服务器-[node.js官网](https://nodejs.org/zh-cn)
- 版本控制-[git官网](https://git-scm.com)
- 好用的博客框架-[hexo官网](https://hexo.io)
- 来注册一个-[github官网](https://github.com)
- 我推荐的编辑器-[vscode官网](https://code.visualstudio.com)
- 我推荐的IDE-[webstorm官网](https://www.jetbrains.com/webstorm)
<br>

<br>
# 用hexo创建博客

<br>
### github创建代码仓库

在github上创建一个代码仓库, 如果你想取名:``xxx``,
建议名称:``xxx.github.io``,将来将会用这个地址打开博客。

将仓库到克隆到本地, 你可以使用``版本管理工具``, 也可以直接
```
# 进入桌面,创建目录并且进入目录
cd ~/Desktop && mkdir blog && cd blog
# 克隆代码仓库
git clone https://{仓库地址}
```

<br>
### 创建博客 

在仓库的根目录``hexo init``初始化博客。

- 生成静态web页面 ``hexo g``
- 运行服务器 ``hexo s``
- 清理缓存 ``hexo clean``

<br>
运行过``hexo g && hexo s``, 
**打开http://localhost:4000/ 看看我们的博客吧!**

<br>
是不是有哪里不对?
和我宣传的效果有点不一样对吧？
因为这只是hexo默认的主题。

<br>
**不要忘记``git add . && git commit && git push``提交仓库哦**

<br>
### 附录

- 我推荐的版本管理工具-[SourceTree](https://www.sourcetreeapp.com)
- node的包管理工具-[npm](https://www.npmjs.com.cn)
<br>

<br>
# 使用yilia主题

**如果不喜欢Yilia, 可以在附录找其他主题**

<br>
### 安装Yilia主题

在仓库的根目录下,下载yilia
```
git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia
```

git clone下来需要删除``.git``文件夹, 才能正确的进入仓库的git版本管理
```
cd themes/yilia
rm -rf .git
```

<br>
这样子根目录结构如下
```
.
├── _config.yml             # 配置文件
├── db.json
├── node_modules            # npm管理的项目依赖包
├── package-lock.json       # npm依赖列包环境的lock
├── package.json            # npm依赖包列表
├── public                  # web页面
├── scaffolds           
├── source                  # 资源文件等的文件存放
├── themes                  # 主题
└── yarn.lock
```

<br>
### 配置项目

修改根目录下的``_config.yml``配置文件

- 使用yilia主题，``theme: yilia``
- 修改网页名字, ``title: {title}``
- 修改副标题, ``subtitle: {subtitle}``
- 署上你的大名, ``author: {author}``
- 修改语言, ``language: zh-Hans``
- 修改时区, ``timezone: Asia/Chongqing``

**更多配置, 移步附录查看我的项目(有详细的注释哦！)**

<br>
**大功告成！打开http://localhost:4000/ 看看我们的博客吧!**


<br>
### 附录

- hexo-config.yml配置, [我的配置](https://github.com/RogerAbyss/RogerAbyss.github.io/blob/dev2/_config.yml)
- yilia-config.yml配置, [我的配置](https://github.com/RogerAbyss/RogerAbyss.github.io/blob/dev2/themes/yilia/_config.yml)

<br>
# 集成Travis CI


根目录下创建``.travis.yml``配置文件。

- 设置node.js语言, ``language: node_js``
- 设置依赖包环境, 
```
install:
    - npm install
```
- 设置脚本, 
```
script:
  - hexo g
```
- 设置分支, 只在``dev2``分支生效,``dev2``开发->推送到``master``
```
branches:
  only:
    - dev2
```
- 设置环境变量${REPO}
```
env:
 global:
   - REPO: github.com/RogerAbyss/RogerAbyss.github.io.git
```
- Github生成访问repo的token, 在travis里设置token的环境变量${TOKEN}
- 设置提交脚本, git通过${TOEKN},${REPO}提交到master分支
```
  - cd ./public
  - git init
  - git config user.name "RogerAbyss"
  - git config user.email "roger_ren@qq.com"
  - git add .
  - git commit -m "Travis automatic update"
  - git push --force --quiet "https://${TOKEN}@${REPO}" master:master
```

<br>
**大功告成, 等待travis CI运行完毕看看我们的网站吧``https://xxx.github.io``**

<br>
### 附录

- Travis-[Travis CI官网]()
- Travis CI教程-[如何配置Travis CI]()
- 我的.travis.yml-[for docker]()
- 我的.travis.yml-[for node]()
- 我的.travis.yml-[for oc]()

<br>
# 其他问题

- 如何写文章? 答: markdown
- 文章日期,分类,标签怎么来? 答: 看文档
```
---
title: ${title}         # 标题
date: ${date}           # 日期
tags: [tag1,tag2]       # 标签
---
```
- 如何控制打开全文在哪里? 答: ``<!--more-->``标签
- 图片不能控制大小? 答: markdown不能, 使用html标签
- 部分页面不想套用主题怎么办? 答: 根目录下``config.yml``下的``skip_render:``


<br>
### 附录

- markdown语法-[如何使用markdown?](http://wowubuntu.com/markdown/#list)
- 优雅的配置文件yaml语法-[yaml官网](http://www.yaml.org)

<br>
<br>
---

**你看到了结尾, 说明我的文章对你是有帮助的！我感到非常荣幸。**
**如果你有任何的问题, 可以email我, 有空的时候我会回复**
**如果你觉得对你有帮助, 可以点击支持我一杯咖啡, 我会继续更新一些有用的东西**
