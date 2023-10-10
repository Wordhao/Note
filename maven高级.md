##### *分模块开发与设计（重点）*

- ssm_pojo
- ssm_dao
- 

##### *聚合*

```xml
 <!--定义该工程用于进行构建管理-->
    <packaging>pom</packaging>
    <!-- 默认打jar包，war是web工程，pom是专门做聚合工程用 -->

    <!--管理的工程列表-->
    <modules>
        <!--具体的工程名称-->
        <module>../ssm_controller</module>
        <module>../ssm_service</module>
        <module>../ssm_dao</module>
        <module>../ssm_pojo</module>
    </modules>
```





##### *继承*

在pom文件中创建依赖，进行依赖管理

###### 父工程中添加 依赖管理声明:

```xml
<!--声明此处进行依赖管理-->
    <dependencyManagement>
        <!--具体的依赖-->
        <dependencies>
            <!--添加自己的工程模块依赖-->
            <dependency>
                <groupId>com.itheima</groupId>
                <artifactId>ssm_pojo</artifactId>
                <version>1.0-SNAPSHOT</version>
            </dependency>
        </dependencies>
    </dependencyManagement>
```

```xml
 <pluginManagement>
            <!--设置插件-->
            <plugins>
                <!--具体的插件配置-->
                <plugin>
                    <groupId>org.apache.tomcat.maven</groupId>
                    <artifactId>tomcat7-maven-plugin</artifactId>
                    <version>2.1</version>
                    <configuration>
                        <port>80</port>
                        <path>/</path>
                    </configuration>
                </plugin>
            </plugins>
        </pluginManagement>
```



###### 子工程中添加：

```xml
 <!--定义该工程的父工程-->
    <parent>
        <groupId>com.itheima</groupId>
        <artifactId>ssm</artifactId>
        <version>1.0-SNAPSHOT</version>
        <!--填写父工程的pom文件， 相对路径-->
        <relativePath>../ssm/pom.xml</relativePath>
    </parent>
```



##### ***属性***

###### 自定义属性

```xml
<!-- 定义自定义属性 -->
    <properties>
        <spring.version>5.1.9.RELEASE</spring.version>
        <junit.version>4.12</junit.version>
    </properties>
```



```xml
<!-- 调用格式-->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>${spring.version}</version>
    </dependency>
```



###### 内置属性

###### java系统属性



##### 版本管理

##### 资源配置

##### 多环境开发配置

###### 定义多环境

```xml
<!-- 创建多环境 -->
    <profiles>
        <!-- 定义具体的环境：生产环境 -->
        <profile>
            <!--定义环境对应的唯一名称-->
            <id>produce_env</id>
            <!--定义环境中专用的属性值-->
            <properties>
                <jdbc.url>jdbc:mysql://127.1.1.1:3306/ssm_db</jdbc.url>
            </properties>
        </profile>

        <!-- 定义具体的环境：开发环境 -->
        <profile>
            <id>dep_env</id>
            <properties>
                <jdbc.url>jdbc:mysql://127.2.2.2:3306/ssm_db</jdbc.url>
            </properties>
        </profile>
    </profiles>
```



###### 使用多环境

执行命令

```java
install -P dep_env(多环境id)
```





##### 跳过测试

##### *私服*

