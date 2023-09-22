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

其中newpasswd换成你的新密码，完成后重启容器

## TODO

- [ ] 使用docker-compose.yml的environment来修改VNC密码
- [ ] 能固化已登陆QQ的数据



