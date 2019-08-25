<!-- sectionTitle: Docker Compose -->
## Docker Compose 

---
## Docker Compose

Docker Compose 属于 Docker 三剑客中的一个。负责实现对 Docker 容器集群**快速编排**。

就像一开始说的最小化 Web 项目，用的就是 Docker Compose 进行编排的。
<br/>
一个项目通常是需要多个容器相互配合。比如Web项目，除了需要 nginx 容器本身，还需要后端运行的容器、数据库容器、甚至是负载均衡容器。

如果不通过 Docker Compose 的话，你就需要手动去管理各个容器之间的关联，这样不高效也不方便。

Compose 恰好满足这样的需求，它允许用户通过一个单独的 `docker-compose.yml` 模板文件来定义一组相关联的应用容器为一个项目（project）.

--- 

## Docker Compose 最重要的两个概念

- 服务 service：一个应用的容器。比如一个 nginx 容器就是一个 service
- 项目 project：由一组关联的应用容器组成的一个完整业务单元。比如前面演示的那个项目，就是属于 Project，下面掌管着多个 service，nginx service，node service, mongodb servce。
