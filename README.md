## config
##### config-server说明：
* 注册到服务中心后，其他微服务可以通过该微服务获取配置
* 配置文件放置本地
* 配置文件放置在版本控制器，比如github
* 可通过将自己注册成服务中心从而达到高可用
***
#### 步骤：
* 引入config-server依赖
* 启动类配置@EnableConfigServer注解
****
###### 本地配置：
* 配置为本地获取配置：
```
server:
  port: 7003

eureka:
  client:
    registerWithEureka: true
    fetchRegistry: true
    serviceUrl:
      defaultZone: http://gaochao:8810/eureka
  instance:
    prefer-ip-address: true

spring:
  application:
    name: qbgc-test-config
  profiles:
    active: native
  cloud:
    config:
      server:
        native:
          search-locations: F:/IDEAWorkspace/config
```
* 将qbgc-admin-service 0.0.1_issues_#1版本作为config-client进行测试
    * 首先引入config依赖
    * 配置项获取配置的方式：
    ```
    spring:
      application:
        name: qbgc-admin-service
      profiles:
        active: dev
      cloud:
        config:
          name: qbgc-admin-service
          discovery:
            enabled: true
            service-id: qbgc-test-config
    ```
    * 创建一个配置POJO类，并用@ConfigurationProperties(prefix = "gcconfig")注入
    * 创建service类，controller类获取
***
###### git获取：
* 不谈了，有兴趣自己去查吧
