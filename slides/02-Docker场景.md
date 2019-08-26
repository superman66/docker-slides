<!-- sectionTitle: Dokcer 场景介绍 -->

## Docker 场景

---

## 开始介绍前，我们先来思考一个小 🌰

你一个人前后端全包，写了一个 Web 项目，俗称 **全干工程师**

**（这里手动@Doma 的小蓝晶项目）**

当你要部署项目到服务器的时候，大家可以思考下有哪些事情是需要做的？

<br />

- 下载并安装配置 `nginx`
- 后端服务、数据库服务、负载均衡服务等
- ...其他配置

<br />

当你在一台服务器上成功部署并运行后，
<br />
老板来了句，把这个项目再部署到其他几台服务器上？你该怎么做？

---

## 这时候 Docker 的作用就显而易见

接下来我们通过一个最小化的前端 + 后端 + 数据库的 Web 项目，来体验下 Docker 部署的便捷与高效。

```shell
$ git clone https://github.com/superman66/docker-demo
$ cd docker-demo
$ yarn
// 这里省去安装构建步骤...
$ docker-compose up -d
```
---

## Docker-compose 配置文件

通过这么一个文件，我们就能搞定一个 Web 项目的部署，而无需去手动安装管理各个服务。

```shell
version: '3'

services:
  web:
    # 开机总是启动
    restart: always
    image: nginx
    # 绑定端口
    ports:
      - '8084:80'
    # 挂载本地文件夹到容器内部文件夹
    volumes:
      - ./app/build:/usr/share/nginx/html/web_app
      - ./nginx/default.conf:/etc/nginx/conf.d/default.conf
  server:
    container_name: server
    build: ./server
    ports:
      - '3200:3200'
    links:
      - mongo
    depends_on:
      - mongo
  mongo:
    container_name: mongo
    image: mongo
    expose:
      - '27017'
    ports:
      - '27017:27017'
    volumes:
      - './db:/data/db'
```
