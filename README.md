# chronocat-docker

本仓库是学习docker的打包与自动化构建，请下载后24小时内删除

## 使用

### 快速运行

```bash
docker run -d --name chronocat-docker -e VNC_PASSWD=vncpasswd -p 5500:5500 -p 5900:5900 -p 6081:6081 -p 16530:16530 -v ${PWD}/config:/root/.chronocat/config yuukinya/chronocat-docker
```

其中vncpasswd换成你的VNC密码

或者下载代码中的docker-compose.yml，然后执行

```bash
docker-compose up -d
```

### 数据固化（可选）

先完成上面的`快速运行`，保证容器在运行状态

```bash
# 进入项目目录
mkdir data
# 复制数据到data目录
docker cp chronocat-docker:/root/.config/QQ ./data
```

如果之前是docker run运行的，执行

```bash
docker run -d --name chronocat-docker -e VNC_PASSWD=vncpasswd -p 5500:5500 -p 5900:5900 -p 6081:6081 -p 16530:16530 -v ${PWD}/config:/root/.chronocat/config -v ${PWD}/data/QQ:/root/.config/QQ yuukinya/chronocat-docker
```

如果之前是docker-compose运行的，编辑docker-compose.yml，把volumes下两行的开头注释去掉，保存，再执行

```bash
docker-compose up -d
```

### noVNC登陆

浏览器访问`http://服务器IP:6081`，默认密码是`vncpasswd`

### VNC登陆

使用VNC软件登陆`服务器IP:5900`，默认密码是`vncpasswd`

### 修改chronocat配置

修改当前目录/config/chronocat.yml，修改后重启容器即可

### 修改VNC密码

```bash
docker exec chronocat-docker sh -c "x11vnc -storepasswd newpasswd /root/.vnc/passwd"
```

其中newpasswd换成你的新密码，立即生效，无需重启容器

## 如何更新

本镜像一般不会只更新chronocat，如果需要只更新chronocat可以使用LiteLoaderQQNT自行更新

1. 更新前请做好数据备份，比如数据固化

2. 删除容器并删除镜像，下面是代码示例

   ```bash
   docker rm -f chronocat-docker && docker rmi yuukinya/chronocat-docker
   ```

3. 重新pull最近镜像

   ```bash
   docker pull yuukinya/chronocat-docker
   ```

4. 按照前面的使用教程操作

## 已知问题

- 容器重启后，桌面的任务栏可能会消失，如果触发了请不要缩小或者点叉关闭，建议保持在聊天的界面，再关闭VNC远程
- 合并转发不可用在Linux版本

## TODO

- [x] 能固化已登陆的数据
- [x] 使用docker的environment来指定VNC密码

## 更新日志

### 2023-10-1

- 更新chronocat至0.0.54

### 2023-10-17

- 更新chronocat至0.0.53

### 2023-10-13

- 更新chronocat至0.0.52
- 新增satori默认端口
### 2023-10-3

- 更新chronocat至0.0.48
- 使用docker的environment来指定VNC密码 [Issue #2](https://github.com/yuuki-nya/chronocat-docker/issues/2)
- 新增noVNC，使用浏览器来登陆VNC [Issue #2](https://github.com/yuuki-nya/chronocat-docker/issues/2)

感谢 [ZGLinus](https://github.com/ZGLinus)提供的思路和代码

### 2023-9-25

- 更新chronocat至0.0.46
- 修改chronocat配置映射至宿主机
- 固化已登陆数据 [Issue #1](https://github.com/yuuki-nya/chronocat-docker/issues/1)

### 2023-9-22

- 初始版本

