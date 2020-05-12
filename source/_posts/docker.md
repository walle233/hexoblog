---
title: docker笔记
---

## docker 安装

略

## docker 使用

#### 启动一个镜像,输出 hello world

```
docker run ubuntu:15.10 /bin/echo "Hello world"
```

#### 运行交互式的容器

```
docker run -i -t ubuntu:15.10 /bin/bash
```

- -t:在新容器内指定一个伪终端或终端。
- -i:允许你对容器内的标准输入 (STDIN) 进行交互。

此时可以运行 exit 退出容器

启动容器（后台模式）

```
docker run -d ubuntu:15.10 /bin/sh -c "while true; do echo hello world; sleep 1; done"
```

查看正在运行的容器

```
docker ps

docker exec -it
```

停止容器

```
docker stop [options]
```

移除容器

```
docker rm [options]
```

<!-- ## 容器使用 -->

运行一个 web 应用

```
docker pull training/webapp
docker run -d -P training/webapp python app.py

docker run -d -p 5000:5000 training/webapp python app.py
```

查看 docker 容器内部进程

```
docker top
```

## docker 镜像

列出本地主机上的镜像

```
docker images
```

使用版本为 15.10 的 ubuntu 系统镜像来运行容器

```
docker run -t -i ubuntu:15.10 /bin/bash
```

获取一个新的镜像

```
docker pull ubuntu:13.10
```

查找镜像

```
docker search httpd
```

文件 挂载

docker run -v --rm -w

```
docker run -d -v $(pwd):/usr/share/nginx/html -p 8080:80 nginx

docker run -d -e MYSQL_ROOT_PASSWORD=abc123 --name mysql_db mysql:5.7

docker run -d -e WORDPRESS_DB_PASSWORD=abc123 -p 8080:80 --link mysql_db:mysql wordpress
```
