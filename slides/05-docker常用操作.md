<!-- sectionTitle: Docker 基本操作 -->

## Docker 基本操作

---
## 镜像基本操作

**拉取镜像**

```bash
docker pull nginx
```

也可以指定 tag

```bash
docker pull nginx:latest
```

**列出镜像**

```bash
docker image ls [option]
```

**删除本地镜像**

```bash
docker image rm [options] 
```

---
## 容器基本操作

前面说过容器是有生命周期的，可以被
- 创建
- 启动
- 停止
- 删除

<br />

**启动容器**

启动容器有两种方式，一种是**基于镜像新建一个容器并启动**。另外一种是**将处于终止状态下的容器重新启动**。

由于 Docker 实在是太轻量级了，所以大部分情况都是随用随创建，不用就删掉。

```bash
docker run nginx-demo -P
```

run 有一些常用的参数：

* `-P` 参数表示随机端口映射。用于映射容器内部端口到主机的端口
* `-p` 指定端口映射。格式为：`主机端口:容器端口`。比如 `8083:80`。
* `-d` 后台运行容器。
* `--name` 指定容器名称。

当使用 `docker run` 命令去创建容器时，Docker 后台运行的操作是：

* 检查本地是否存在指定的镜像，不存在就从公有仓库下载
* 利用镜像创建并启动一个容器
* 分配一个文件系统，并在只读的镜像层外面挂载一层可读写层
* 从宿主主机配置的网桥接口中桥接一个虚拟接口到容器中去
* 从地址池配置一个ip地址给容器
* 执行用户指定的应用程序
* 执行完毕后容器被终止



**查看容器**

```shell
docker ps 				// 查看当前运行的容器
docker ps -a			// 查看所有容器，包含已终止的容器
```



**终止容器**

```shell
docker contaier stop containerid
```


**启动容器**

可以对已经终止的容器进行重新启动

```bash
docker container start containerid
```



**删除容器**

```bash
docker container [name] rm  [-f]
```

上面是删除单个容器，也可以删除全部处于终止状态的容器

```bash
docker container prune
```

---

### 又是一个例子
讲了上面的一些基本操作，我们就可以来看一个简单的 nginx 例子。

起一个 名为 mynginx 的 nginx 容器

```bash
docker run --name mynginx -d -P nginx
```

这就是最简单的一个例子了。

那问题来了？如果我们要更改 nginx 的配置呢？

这就要说到 Docker 数据管理了。


---
## Docker 数据管理

* 数据卷（volumes）
* 挂载主机目录

---

## 数据卷

数据卷是一个可供一个或者多个容器使用的特殊目录。他具有以下的特征

* 在容器之间共享和重用
* 对数据卷的修改会立马生效
* 对数据卷的更新不会影响容器
* 数据卷默认一直存在，即使容器被删除。


---

### 数据卷操作

**创建数据卷**
```bash
docker volume create my-local-vol		// 创建数据卷
docker volume ls	// 查看所有数据卷
```



**查看数据卷**

```bash
docker volume inspect my-local-vol
```

创建完数据卷后，就可以在启动容器的时候使用 `--mount` 将其挂载到容器里。

以前面 nginx 为例：

```bash
docker run --name mynginx -d -P --mount source=my-local-vol,target=/test nginx 
```


---
## 挂载主机目录

无需创建数据卷，直接将本地主机的目录挂载到容器里。

```bash
docker run --name mynginx -d -P --mount type=bind,source=./nginx/default.conf,target=/etc/nginx/conf.d/default.conf nginx 
```

上面命令就会启动一个挂载了本地nginx.conf 配置文件的 nginx 容器。




