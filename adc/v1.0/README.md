ArteryDevloperCommunity（Artery6版）
==========================
[Artery开发者社区](http://artery.thunisoft.com)源码（Artery6版）


## 运行环境要求
* Jdk1.8
* Elasticsearch6.7.2
* Mysql 5.7

## 如何启动
- 启动Mysql    
  第一次启动应执行初始化脚本：`sql/init.sql`  

- 启动ES

  在docker容器内可参考`es/Dockerfile`构建一个镜像并在docker内部署es

  本地开发可自行启动es服务，符合运行环境的es版本要求

- 启动应用

  在应用程序中修改连接配置，包括修改数据库的访问地址、用户名密码、es的cluster名称、访问地址等

  ```yml
  spring:
    datasource:
      driver-class-name: com.mysql.jdbc.Driver
      url: jdbc:mysql://${DB_ADDR}:${DB_PORT}/${DB_DATABASE}
      username: ${DB_USERNAME}
      password: ${DB_PASSWORD}
    data:
      elasticsearch:
        cluster-name: ${ES_CLUSTER}
        cluster-nodes: ${ES_IP}:${ES_PORT}
  ```
  以spring boot启动方式启动应用

## 常见问题

### 登录出错

通过登录页面输入用户名面登录出错，查看后台报错`could not be authenticated by any configured realms...`，此问题是用户名密码错误导致，adc用户登录时应使用cocall的用户名和密码（注意不是域账户密码），确认密码是否正确。

*关于源码中登录的处理可参见`com.thunisoft.adc.login`包*