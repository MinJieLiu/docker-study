
## lesson2 构建 `Docker` 镜像

使用 Dockerfile 构建镜像。Dockerfile 是一个文本文件，它记述了 Docker 构建一个镜像所需要的过程，包括安装软件包、创建文件夹、定义环境变量以及其他一些操作。

### FROM 指定基础镜像

以一个镜像为基础，在其上进行定制。Dockerfile 中 FROM 是必备的指令，并且必须是第一条指令。

`scratch` 它表示一个空白的镜像。直接 `FROM scratch` 会让镜像体积更加小巧。

```
FROM scratch
```

### RUN 执行命令

RUN 指令是用来执行命令行命令的。由于命令行的强大能力，RUN 指令在定制镜像时是最常用的指令之一。
每一个 RUN 的行为，在其上执行这些命令，执行结束后，commit 这一层的修改，构成新的镜像。

```
RUN apt-get update
```

 * `docker build` 镜像构建。在 Dockerfile 文件所在目录执行

```
# . 指定 context 目录
docker build -t nginx:v3 .
```
