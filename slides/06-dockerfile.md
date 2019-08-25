<!-- sectionTitle: Dockerfile -->
## Dockerfile

---
## Dockerfile 是什么

前面说到镜像可以从 Docker Hub 中拉取。还有一种方式也可以构建镜像：Dockerfile。

Dockerfile 就是一个文本文件，**包含了一条条的指令，用于描述如何构建镜像**。

---

## Dockerfile 实例
下面是我之前写的一个 node 小服务的 Dockerfile: [wakatime-sync Dockerfile](https://github.com/superman66/wakatime-sync/blob/master/Dockerfile)

```dockerfile
FROM node:carbon
COPY . /wakatime-sync
WORKDIR /wakatime-sync
RUN npm install \
&& npm install pm2 -g \
&& npm run build
CMD ["pm2-runtime", "start", "pm2.json"]		
```

* `FROM` 用于指定基础镜像
* `COPY source target` 复制文件。将当前目录所有文件复制到 容器内 `/wakatime-sync` 这个目录。如果目标路径不存在，会自动创建
* `WORKDIR` 指定工作目录，指的就是当前目录。如果当前目录不存在，会自动创建。
* `RUN` 用于执行命令行命令。这里我们用于执行 npm 命令。
* `CMD` 用于启动容器的命令。前面说过，容器是进程。既然是进程，就需要指定所运行的程序及参数。这里是指定 pm2 作为容器的运行程序

<br/>
通过这么一个 Dockerfile，我就可以构建该node服务的镜像，并上传到 Docker Hub。
<br/>

以后需要部署该服务，只需要去Docker hub 拉取该镜像，直接启动容器即可，无需关心任何的环境配置问题。

---


## Dockerfile 其他指令

- ADD 高级的复制文件

- ENV 设置环境变量

- VOLUME 定义数据卷
- EXPOSE 暴露端口
- CMD 容器启动命令
- WORKDIR 指定工作目录

---

## Dockerfile 最佳实践
更多 Dockerfile 用法可以查阅官方提供的 [Dockerfile最佳实践](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/) 

