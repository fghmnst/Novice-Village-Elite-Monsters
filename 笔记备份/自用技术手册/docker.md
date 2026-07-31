# docker

以Ubuntu24.04且部署在大陆以外的服务器为例，介绍最新最潮的下载安装
[Install Docker Engine on Ubuntu | Docker Docs](https://docs.docker.com/engine/install/ubuntu/)

> 国内服务器折腾起来十分麻烦，但依旧有解，这里挖一个坑

**下载：**

```shell
sudo apt remove $(dpkg --get-selections docker.io docker-compose docker-compose-v2 docker-doc podman-docker containerd runc | cut -f1)

# Add Docker's official GPG key:
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF

sudo apt update

sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

如果网络环境正常的话，理论上这一路下来可以十分爽快地复制粘贴，接下来设置sudo组，免得搞个docker回回得输入sudo。
>*现在是2026年7月31日，我在配置syncplay服务端的时候得知这种情况最好单独给软件设置一个用户`sudo useradd -r syncplay`，`-r`（或 `--system`）：将用户创建为系统用户（System User）*
>*这么做据说更规范点，因为可以做到更好的权限隔离，由于系统用户无法使用su命令进入，接下来要么使用命令`sudo -u syncplay -s`进入syncplay特有权限shell终端；要么在命令前都加上`sudo -u syncplay`；要么在最后修改权限`sudo chown -R syncplay:syncplay /opt/syncplay`*

```shell
# 1. 创建 docker 用户组（如果已存在会提示，无影响）
sudo groupadd docker

# 2. 将当前用户加入 docker 用户组
sudo usermod -aG docker $USER

# 3. 刷新用户组权限（或直接退出终端重新登录）
newgrp docker
```

ojbk。接下来是docker常见指令：

> 见尚硅谷的docker速通教程
> [Docker教程，3小时速通，docker部署到实战！_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Zn4y1X7AZ?spm_id_from=333.788.videopod.sections&vd_source=aec394c063dc8df9e287dfd78e682b5f)
> 这个教程我用edge开不知为何会卡得飞起，用chrome就没这个问题了。为什么呢？
> 是啊，为什么。

**镜像操作：**

1. 检索：`docker search`
2. 下载：`docker pull`
3. 列表：`docker images`
4. 删除镜像：`docker rmi`

**容器操作：**

1. 删除容器：`docker rm`
2. 创建并启动新容器：`docker run`
3. 启动已有容器：`docker start`
4. 查看：`docker ps`
5. 停止：`docker stop`
6. 重启：`docker restart`
7. 状态：`docker stats
8. 日志：`docker logs`
9. 进入：`docker exec`
> 加上`--help`可查看帮助
   >

**run 细节：**

1. `docker run -d`后台启动
2. `docker run -d --name aaa bbb`以aaa名称后台启动镜像bbb