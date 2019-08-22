# Registry

Docker Registry 就是类似 Github 的一个服务，你可以把你在本地生成的镜像推送上去。这样就可以在其他服务器直接该镜像进行使用，也可以把镜像公开，让别人也使用。

一个 Docker Registry 中可以包含多个 仓库 （Repository）；每个仓库可以包含多个标签 Tag；每个标签对应一个镜像。

每个镜像可以用 tag 来指定具体版本的镜像。不打 `tag` 则默认 `latest`


同样的，Docker 官方提供了私有 Registry 服务，也可以搭建私有 Registry 服务。

像我们公司，生产环境所用的 Docker 镜像，就是从搭建的私有 Registry 上拉取的。
