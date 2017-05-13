
## lesson2 构建 Docker 镜像

使用 `Dockerfile` 构建镜像。`Dockerfile` 是一个文本文件，它记述了 `Docker` 构建一个镜像所需要的过程，包括安装软件包、创建文件夹、定义环境变量以及其他一些操作。

### `FROM` 指定基础镜像

以一个镜像为基础，在其上进行定制。`Dockerfile` 中 `FROM` 是必备的指令，并且必须是第一条指令。

`scratch` 它表示一个空白的镜像。直接 `FROM scratch` 会让镜像体积更加小巧。

```
FROM scratch
```

### `RUN` 执行命令
`RUN` 指令在定制镜像时是最常用的指令之一。
每一个 `RUN` 的行为，在其上执行这些命令，执行结束后，commit 这一层的修改，构成新的镜像。
仅仅使用一个 `RUN` 指令，并使用 `&&` 将各个所需命令串联起来，简化为一层修改。

```
RUN apt-get update
```

 * `docker build` 镜像构建。在 Dockerfile 文件所在目录执行

```
# . 指定 context 目录
docker build -t nginx:v3 .
```

将 `Dockerfile` 置于一个空目录下，或者项目根目录下。如果该目录下没有所需文件，那么应该把所需文件复制一份过来。如果目录下有些东西确实不希望构建时传给 `Docker` 引擎，那么可以用 `.gitignore` 一样的语法写一个 `.dockerignore`，该文件是用于剔除不需要作为上下文传递给 `Docker` 引擎的。

 * `COPY` 复制文件 `COPY <源路径>... <目标路径>`
 * `ADD` 与 `COPY` 的格式和性质基本一致。如果 `<源路径>` 为一个 `tar` 压缩文件的话，压缩格式为 `gzip`, `bzip2` 以及 `xz` 的情况下，`ADD` 指令将会自动解压缩这个压缩文件到 `<目标路径>` 去。
 * `CMD` 容器启动命令。指令的格式和 `RUN` 相似
 * `ENTRYPOINT` 入口点
 * `ENV` 设置环境变量 格式：`ENV <key1>=<value1> <key2>=<value2>`
 * `ARG` 构建参数 格式：`ARG <参数名>[=<默认值>]`
 * `VOLUME` 定义匿名卷 格式：`VOLUME ["<路径1>", "<路径2>"...]`
 * `EXPOSE` 声明端口 格式：`EXPOSE <端口1> [<端口2>...]`
 * `WORKDIR` 指定工作目录 格式：`WORKDIR <工作目录路径>`
 * `USER` 指定当前用户 格式：`USER <用户名>`
 * `HEALTHCHECK` 健康检查 `HEALTHCHECK [选项] CMD <命令>` 设置检查容器健康状况的命令。用这行命令来判断容器主进程的服务状态是否还正常，从而比较真实的反应容器实际状态
 * `ONBUILD` 为他人做嫁衣裳
