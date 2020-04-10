# linux指令

## 查询类

- **在指定的日志中列出包含指定关键字**：`grep  -rn 关键字 xxx.log`
- **linux 下查看消耗 CPU 的线程**：
    1. `top` 命令，查看消耗 cpu 的进程，假设 PID = 2864
    2. `ps -mp 2864 -o THREAD,tid,time`，查看当前进程 2864 下的消耗 cpu 的线程，假设线程 TID = 2888
    3. `printf "%x\n" 2888`，将线程 ID 转为 16 进制，这里得到的值为：b48
    4. `jstack 2864 |grep b48 -A 30`，查看堆栈信


## 操作类

- **java 命令启动某个 jar 应用**：
    - 以控制台方式启动，关闭控制台应用会停止：`java -jar -Dserver.port=9350 -Dspring.profiles.active=dev demo.jar`
    - 以后台方式启动某应用，并且不输出日志：`java -jar -Dserver.port=9350 -Dspring.profiles.active=dev demo.jar > /dev/null 2>&1 &`
    - 以后台方式启动某应用，并且将日志输出到当前目录 out.log 文件：`java -jar -Dserver.port=9350 -Dspring.profiles.active=dev demo.jar > out.log &`
    - 配置项介绍：
        - `-Dserver.port=9350`：启动端口
        - `-Dspring.profiles.active=dev`：启动环境
- **eureka 强制下线指定的服务**：
    - `http://ip:端口/eureka/apps/应用名称/实例名称/status?value=OUT_OF_SERVICE`，请求方式 PUT
        - value 的值有：UP（上线）、DOWN（临时下线）、STARTING、OUT_OF_SERVICE（永久下线）、UNKNOWN
    - 示例：`http://192.168.3.100:9406/eureka/apps/DEMO-SERVICE/localhost:demo-service:9401/status?value=OUT_OF_SERVICE`

- **maven 私服上传第三方 jar 命令**：`mvn deploy:deploy-file -DgroupId=com.leeyom -DartifactId=leeyom_api_sdk -Dversion=2.4.0 -Dpackaging=jar -Dfile=/Users/leeyom/Downloads/leeyom_api_sdk_2.4.0.jar -Durl=http://192.168.31.21:8081/repository/thirdparty/ -DrepositoryId=thirdparty`
    - `DgroupId=com.leeyom`：jar 所属组织名称
    - `DartifactId=leeyom_api_sdk`：：jar 的名称
    - `Dversion=2.4.0`：版本号
    - `Dpackaging=jar`：上传的类型是jar类型
    - `Dfile=/Users/leeyom/Downloads/leeyom_api_sdk_2.4.0.jar`：jar的本地磁盘位置
    - `Durl=http://192.168.31.21:8081/repository/thirdparty/`：maven私服仓库地址，我这里上传到 thirdparty 仓库
    - `DrepositoryId=thirdparty`：上传的仓库名称
    - 如果执行命令出现：`Return code is: 401, ReasonPhrase: Unauthorized.`异常提示，需要在 maven 的 settings.xml 文件中增加该仓库（我这里是 thirdparty ）的权限：

```
<server>
    <id>thirdparty</id>
    <username>admin</username>
    <password>admin</password>
</server>
```