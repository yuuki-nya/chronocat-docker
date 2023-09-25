# chronocat-docker

使用ubuntu22.04 + openbox + linuxqq 制作

## 使用

### 快速运行

容器重建会丢失已登陆QQ数据

```bash
docker run -d --name chronocat-docker -p 16530:16530 -p 5900:5900 -v ${PWD}/config:/root/.chronocat/config yuukinya/chronocat-docker
```

或者下载代码中的docker-compose.yml，然后执行

```bash
docker-compose up -d
```

### QQ登陆数据固化（可选）

先完成上面的`快速运行`，保证容器在运行状态

```bash
# 进入项目目录
mkdir data
# 复制数据到data目录
docker cp chronocat-docker:/root/.config/QQ ./data
```

如果之前是docker run运行的，执行

```bash
docker rm -f chronocat-docker && run -d --name chronocat-docker -p 16530:16530 -p 5900:5900 -v ${PWD}/config:/root/.chronocat/config -v ${PWD}/data/QQ:/root/.config/QQ yuukinya/chronocat-docker
```

如果之前是docker-compose运行的，编辑docker-compose.yml，把volumes下两行的开头注释去掉，保存，再执行

```bash
docker-compose up -d
```

### VNC登陆

使用VNC软件登陆`服务器IP:5900`，默认密码是`vncpasswd`

### 修改chronocat配置

修改当前目录/config/chronocat.yml，修改后重启容器即可

### 修改VNC密码

```bash
docker exec chronocat-docker sh -c "x11vnc -storepasswd newpasswd /root/.vnc/passwd"
```

其中newpasswd换成你的新密码，立即生效，无需重启容器

## 已知问题

- 容器重启后，桌面的任务栏可能会消失，如果触发了请不要缩小或者点叉关闭，建议保持在聊天的界面，再关闭VNC远程
- 伪造转发暂不适配Linux QQ

## TODO

- [x] 能固化已登陆QQ的数据
- [ ] 使用docker的environment来指定VNC密码

## 更新日志

### 2023-9-25

- 更新chronocat至0.0.46
- 修改chronocat配置映射至宿主机
- 固化已登陆QQ数据

### 2023-9-22

- 初始版本

