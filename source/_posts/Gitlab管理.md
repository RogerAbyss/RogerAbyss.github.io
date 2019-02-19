---
title: Gitlab的管理与维护
date: 2019-2-19 10:10:00
tags: [Linux]
---

{% cq %}
Gitlab的管理与维护
{% endcq %}

<!-- more -->
- [x] gitlab 日常操作
- [ ] gitlab 备份与升级
- [ ] gitlab runner安装与配置


### gitlab日常操作

```shell
# 启动
sudo gitlab-ctl start
# 停止
sudo gitlab-ctl stop
# 重启
sudo gitlab-ctl restart
# 修改配置
vim /etc/gitlab/gitlab.rb
# 重新配置生效
sudo gitlab-ctl reconfigure
# 查看服务器状态
sudo gitlab-ctl status
# 修改管理员密码
sudo gitlab-rails console production
user = User.where(id: 1).first
user.password = '新密码'
user.password_confirmation = '新密码'
user.save!
###########
# 日志相关
###########
# 检查redis的日志
sudo gitlab-ctl tail redis
# 检查postgresql的日志
sudo gitlab-ctl tail postgresql
# 检查gitlab-workhorse的日志
sudo gitlab-ctl tail gitlab-workhorse
# 检查logrotate的日志
sudo gitlab-ctl tail logrotate
# 检查nginx的日志
sudo gitlab-ctl tail nginx
# 检查sidekiq的日志
sudo gitlab-ctl tail sidekiq
# 检查unicorn的日志
sudo gitlab-ctl tail unicorn
```

### gitlab 备份与升级
### gitlab runner安装与配置
```shell
# gitlab-runner每次都拉取docke image的解决方法
# pull_policy --> if-not-present
vim /srv/gitlab-runner/config/config.toml
volumes = ["/cache", "{$PATH}"]
pull_policy = "if-not-present"

# Docker开机启动
systemctl enable docker
usermod -aG docker ${your_username}
```