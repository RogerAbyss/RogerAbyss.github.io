---
title: 玩转MacOS包管理器Homebrew
---

Homebrew 是一款MacOS的包管理器, 它几乎包含了所有你需要的一切环境和优秀的软件。
本文主要带大家深入了解和使用Homebrew。
<!-- more -->

**什么样的人需要Homebrew？**

* 首先, 你是一个MacOS玩家
* 你有轻微强迫症, 希望电脑所有文件保持整洁、条理
* 你是一个开发者
* 你习惯使用Linux, 并且更喜欢使用命令行

**任中满足一条或一条以上, 你都应该拥有Homebrew**
---

## Install (安装)
#### 1.普通安装
参考[Homebrew官网](https://brew.sh)
#### 2.镜像安装
如果你是国内玩家, 你可能会发现下载相当慢。就算下载好了, 以后安装东西也会很慢。
所以, 我们需要通过**镜像安装**。

1. 下载官方安装脚本``brew_install``, 放在桌面
```
cd ~/Desktop
 curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install >> brew_install
```

2. 修改镜像,``BREW_REPO``与``CORE_TAP_REPO``两项(你可以双击文件修改, 也可以使用vim等工具)
```
#BREW_REPO = "https://github.com/Homebrew/brew".freeze
BREW_REPO = "git://mirrors.ustc.edu.cn/brew.git".freeze
#CORE_TAP_REPO = "https://github.com/Homebrew/homebrew-core".freeze
CORE_TAP_REPO = "git://mirrors.ustc.edu.cn/homebrew-core.git".freeze
```

3. 运行脚本安装
```
/usr/bin/ruby ~/Desktop/brew_install
```

4. 替换源并且设置镜像
```

// 设置brew镜像
cd "$(brew --repo)"
git remote set-url origin git://mirrors.ustc.edu.cn/brew.git

// 修改core源
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin git://mirrors.ustc.edu.cn/homebrew-core.git

// 修改bottles源
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.bash_profile

// 使其生效
source ~/.bash_profile
```
**觉得速度不稳定可以考虑Coding,七牛等其他的镜像点**

5. (如果你有稳定的ss)设置sock5
```
// 创建一个.curlrc文件 写入
vim ~/.curlrc

// 写入这一句
socks5 = "127.0.0.1:1086"
```

## Usage (使用)
参考[Homebrew官网](https://brew.sh)

![brew help](/src/brew.png)

**常用命令**

1. brew upgrade
> 升级环境, 你所安装的一切环境如果有需要更新的就用这个命令
2. brew search something
> 搜索, 查看库是否存在以及依赖情况
3. brew instll something
> 安装, 安装库与相应依赖
4. brew leaves
> 查看所有的库, 与list不同的是, 不包括依赖环境
5. brew service star something
> 启动服务
6. brew doctor
> 自检
7. brew info something
> 查看库信息, 一般忘了怎么设置库, 或者查看依赖环境

## Leaves（我的清单）

```
Abyss:~ abyss$ brew leaves
activemq
coreutils
flow
gcovr
git
git-lfs
gnupg
infer
jenkins
maven
mysql
ncdu
nginx
perl
postgresql
python
redis
ruby
sonar-scanner
sonarqube
thefuck
tomcat
tree
vim
watchman
wget
yarn
zookeeper
```
http://localhost:4000/2017/08/04/Homebrew/src/brew.png
http://localhost:4000/backend/syso_files/con1-bg1.png
## 进阶玩法

### LaunchRocket

![brew rocket](/src/brewRocket.png)
[下载地址](https://github.com/jimbojsb/launchrocket)

**使用xcode运行安装**

### Cakebrew

Cakebrew是一款图形化管理homebrew的软件, 我没有用。大家可以自己找找。