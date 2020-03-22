## 安装 eureka

- 拉取镜像：`docker pull springcloud/eureka`
- 启动容器：`docker run --name eureka -d -p 8761:8761 springcloud/eureka`

## 安装 mysql

- 拉取镜像：`docker pull mysql`
- 启动容器：`docker run -itd --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql`
- 如果用 Navicat 连接 mysql 提示：`Authentication plugin 'caching_sha2_password' cannot be loaded: dlopen(/usr/local/mysql/lib/plugin/caching_sha2_password.so, 2): image not foun`
    - 进入 mysql 客户端，执行如下的命令：
        - 启动 bash：：`docker exec -it mysql /bin/bash`
        - 连接 mysql：`mysql -u root -h 127.0.0.1 -p`
        - 修改密码：`ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'newpassword';`
            - newpassword 就是新的密码
        - 刷新权限：`flush privileges;`
    - 之后便可以连接

## 安装 redis

- 拉取镜像：`docker pull redis`
- 启动容器：`docker run -itd --name redis -p 6379:6379 redis`