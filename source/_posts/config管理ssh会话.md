---
title: config管理ssh会话
date: 2018-05-14 15:17:00
tags: [Linux]
---

{% cq %}
利用ssh config无密码访问服务器
{% endcq %}

<!-- more -->

## Advantage

    Allow we use just a simple commands connect ours servers.
    On Linux, it`s especially useful without GUI.

#### whereis config
在``~/.ssh/``下配置config可以管理ssh会话
```zsh
 abyss@Proabyss-macbook-pro-3  ~  tree ~/.ssh/ -L 1
/Users/abyss/.ssh/
├── config
├── ecs.pem
├── id_rsa
├── id_rsa.pub
├── known_hosts
├── ppmatch-zgxl
├── ppmatch-zgxl.pub
├── zgxl-ci
├── zgxl-ci.pub
├── zgxl-gitlab
└── zgxl-gitlab.pub
```

#### simple commonds

**一行简短的命令访问服务器**
```zsh
 abyss@Proabyss-macbook-pro-3  ~  ssh ces
Last login: Fri May  4 09:02:23 2018 from 125.84.*.*

Welcome to Alibaba Cloud Elastic Compute Service !

[root@iZwz9ffj2n0qabqqile246Z ~]#
```

## Config 
如果没有, 生成一个``config``, 在``~/.ssh/``文件下
```
# 服务器别名, ssh server访问
Host server
    # ip地址
    HostName        192.168.3.*
    # ssh端口号
    Port	        22
    # 用户名
    User            root
    # 私钥位置
    IdentityFile    /Users/**/.ssh/id_rsa
```

## Config Server
服务器,需要配置有我们的公钥。


1. 生成公钥和私钥
```zsh
# 没有则mkdir ssh创建一个
cd ~/.ssh
# 生成公钥和私钥, 密码可以不设置  *私钥 *.pub公钥
ssh-keygen -t rsa
```

2.  将公钥上传到服务器, 生成authorized_keys
```zsh
scp ./*.pub user@216.194.70.*:~/.ssh/
cat *.pub >> authorized_keys
```

3. 管理文件权限
```zsh
chmod 700 ~/.ssh/
chmod 600 authorized_keys
```

4. 重启服务器sshd
```zsh
service sshd restart
```