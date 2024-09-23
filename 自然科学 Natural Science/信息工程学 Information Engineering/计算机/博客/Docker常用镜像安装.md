## docker 常用参数
```
-d: 后台运行容器，并打印容器ID。

--name: 为容器指定一个名称。

-p: 发布容器的端口到主机。

-v: 将主机目录挂载到容器内部。

--rm: 当容器停止时自动删除容器。

-e: 设置环境变量。

-it: 允许你交互式地运行容器。

# 运行一个后台容器，名为 my-nginx
docker run -d --name my-nginx -p 8080:80 nginx
 
# 运行一个交互式容器
docker run -it ubuntu bash
 
# 发布本地目录到容器内部，并命名容器
docker run -d --name my-app -v /my/local/path:/path/in/container -p 8080:80 my-app-image
 
# 设置环境变量并运行容器
docker run -d --name my-app -e "ENV_VAR_NAME=value" my-app-image
 
# 当容器停止时自动删除
docker run --rm -d --name my-temp-container ubuntu

```

## 1、Mysql

```
docker pull mysql # 拉取最新版mysql镜像
```

```
duso docker run -p 3306:3306 --name mysql \
-v /usr/local/docker/mysql/conf:/etc/mysql \
-v /usr/local/docker/mysql/logs:/var/log/mysql \
-v /usr/local/docker/mysql/data:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=123456 \
-d mysql

```

配置外网访问

```
sudo docker exec -it mysql bash
mysql -uroot -p123456
mysql> update user set host='%' where user ='root';
mysql> flush privileges;
mysql> ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'root';
mysql> alter user 'root'@'%' identified by '123456';
mysql> flush privileges;
```

## 2、Sql Server 


```
docker pull mcr.microsoft.com/mssql/server:2019-latest
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=dev@123" -p 14330:1433 --name sqlserver2019 -v /hd2/sqlserver2019_data:/var/opt/mssql  -d mcr.microsoft.com/mssql/server:2019-latest
```

## 3、Redis

```
docker pull redis:lastest
docker run -p 6379:6379 --name myredis -v /root/docker/redis/redis.conf:/etc/redis/redis.conf  -v /root/docker/redis/data:/data -d redis redis-server /etc/redis/redis.conf --appendonly yes
# redis-server /etc/redis/redis.conf  ：这个是关键配置，让redis不是无配置启动，而是按照这个redis.conf的配置启动
# -appendonly yes：redis启动后数据持久化
```

## 4、Nginx

```
docker pull nginx

mkdir -p /home/nginx/www /home/nginx/logs /home/nginx/conf
# www: 目录将映射为 nginx 容器配置的虚拟目录。

# logs: 目录将映射为 nginx 容器的日志目录。

# conf: 目录里的配置文件将映射为 nginx 容器的配置文件。
```

```
docker run -p 8080:80 --name nginx-test-web \ -v /home/nginx/www:/usr/share/nginx/html \ -v /home/nginx/conf/nginx.conf:/etc/nginx/nginx.conf \ -v /home/nginx/logs:/var/log/nginx \ -d nginx
```