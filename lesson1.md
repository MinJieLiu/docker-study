# docker 学习笔记

## lesson1 入门

 * `docker ps` 列出所有运行中的容器。 `-a` 参数显示额外已经停止的的容器；`-q`参数只返回容器 `id`
 * `docker create xxx` 创建一个容器
 * `docker kill xxx` 停止该容器
 * `docker rm xxx` 删除指定容器
 * `docker images` 列出镜像信息。 `-a` 参数列出包含中间层镜像； `-f` 过滤镜像，如`since=mongo:3.2`；`-q`参数只返回镜像 `id`
 * `docker rmi xxx` 删除指定镜像
 * `docker run xxx` 运行 xxx 镜像。 `-t -i` 参数获得一个交互式会话；`-d` 参数以后台服务运行镜像，可以通过运行 `exec` 启动 bash shell

example:

```
# 运行 busybox 镜像
docker run busybox echo hello world

# 查看容器的镜像列表
docker ps -a

# 将已停止的容器列表删除
docker rm $(docker ps -a -q)

# 过滤镜像
docker images -f before=mongo:3.2

#自定义条件（Go模板语法）查看镜像
docker images --format "{{.ID}}: {{.Repository}}"
```
