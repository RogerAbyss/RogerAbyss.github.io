---
title: docker管理mysql
date: 2018-05-14 15:59:00
tags: [Docker]
---

{% cq %}
Docker的妙用
{% endcq %}

<!-- more -->

## Advantage

    Use Docker can easily install mysql in same enviroment &
    learn basic usage of docker.

- [x] 如何使用docker管理mysql
- [x] docker的基础用法
- [x] docker搭建CI
- [ ] docker compose

## 如何使用docker管理mysql 

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


### docker的基础用法

```shell
# 拉取镜像
docker pull ${someimages}
# 查看本地镜像
docker images
# 删除本地镜像
docker rmi ${imageId}
# 运行Docker (-d 守护进程)
docker run -d
# 查看运行容器 (-a 所有的,包括已经停止的)
docker ps -a
# 进入容器调试
docker exec -it ${containerid} /bin/bash
# 删除容器 (需要停止 或者 -f强制)
docker rm ${containerid}
docker rm $(docker ps -a -q)
# 本地创建image
docker build -t ${user_name/image_name:version} . 
```

### docker搭建CI
[CI](https://github.com/RogerAbyss/docker-abyssci)
### docker compose