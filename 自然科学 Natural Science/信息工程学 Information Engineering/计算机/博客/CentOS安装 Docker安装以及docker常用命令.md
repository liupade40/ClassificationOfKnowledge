## 1、安装命令

```
yum install docker-ce -y
systemctl restart docker
systemctl enable docker
```

## 2、常用命令

```
docker -v 查看版本
docker info 查看宿主机上的容器的状态
docker search centos 搜索镜像
docker pull  [镜像名称] 拉取镜像
docker images 查看本地镜像
docker rmi [镜像名称] 
docker ps 查看运行的容器
docker run 创建并且运行容器
docker start/restart [容器名称] 启动容器
docker stop [容器名称]
docker rm [容器名称] 删除容器
docker logs [容器名称] 查看容器日志
docker inspect [容器名称] 获取容器元数据 
docker exec -it [容器名称] bash 进入容器
docker top [容器名称] 查看容器中运行的进程信息
```
