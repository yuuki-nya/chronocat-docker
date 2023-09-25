# chronocat-docker

使用ubuntu22.04 + openbox + linuxqq 制作

## 使用

```bash
docker run -d --name chronocat-docker -p 16530:16530 -p 5900:5900 yuukinya/chronocat-docker
```

或者下载代码中的docker-compose.yml，然后执行

```bash
docker-compose up -d
```

### VNC登陆

使用VNC软件登陆`服务器IP:5900`，默认密码是`vncpasswd`

### 获取RED_PROTOCOL_TOKEN

```bash
docker exec chronocat-docker cat /home/user/BetterUniverse/QQNT/RED_PROTOCOL_TOKEN
```

### 修改VNC密码

```bash
docker exec chronocat-docker sh -c "x11vnc -storepasswd newpasswd /root/.vnc/passwd"
```

其中newpasswd换成你的新密码，立即生效，无需重启容器

## 已知问题

- 容器重启后，桌面的任务栏可能会消失，如果触发了请不要缩小或者点叉关闭，建议保持在聊天的界面，再关闭VNC远程
- 伪造转发暂不适配Linux QQ

## TODO

- [ ] 使用docker的environment来指定VNC密码
- [ ] 能固化已登陆QQ的数据（可能因为容器重随机生成设备ID而无法实现）



