---
title: docker管理mysql
date: 2018-05-14 15:59:00
tags: [Docker]
---

{% cq %}
docker管理mysql
{% endcq %}

<!-- more -->

## Advantage

    Use Docker can easily install mysql in same enviroment.

## Install 

1. docker 创建并运行mysql, 配置初始化密码

```zsh
docker run --name some-mysql \
-e MYSQL_ROOT_PASSWORD=mypwd123 \
-p 3306:3306 \
-v $PWD/mysql:/var/lib/mysql \
-d mysql
```

``MYSQL_ROOT_PASSWORD``为用户密码, 用户名``root``

2. 尝试登陆

```zsh
# 进入docker内部
docker exec -it container-id /bin/bash
# 登陆
mysql -uroot -p
``` 

3. connect mysql(例如:navicat)

ip: 服务器ip
端口号: 3306
用户名: root
密码: mypwd123(刚刚设置的)