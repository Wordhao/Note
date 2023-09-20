#### Maven 项目管理工具 项目对象模型（POM）Project Object Model

##### Maven核心：

![image-20230915141336972](C:\Users\wordhao\AppData\Roaming\Typora\typora-user-images\image-20230915141336972.png)



##### Maven的作用：

- 项目构建
- 依赖管理
- 统一开发结构



##### Maven基本概念：

- 仓库：本地仓库、远程仓库
- 坐标：定位仓库中资源位置，Maven坐标主要组成groupId（组织名）、artifactId（项目名）、version（版本号）

```xml
<!-- https://mvnrepository.com/artifact/log4j/log4j -->
<dependency>
    <!--groupId组织名 -->
    <groupId>log4j</groupId>
    <!--artifactId项目名 -->
    <artifactId>log4j</artifactId>
    <!--version版本号 -->
    <version>1.2.17</version>
</dependency>

```



镜像仓库的配置：

```xml
 <mirror>
      <!-- 镜像的唯一标识符，用来区分不同的mirror元素 -->
      <id>nexus-aliyun</id>
      <!-- 对哪种仓库进行镜像，替代哪个仓库-->
      <mirrorOf>central</mirrorOf>
      <!-- 镜像名称，可省略 -->
      <name>Nexus aliyun</name>
      <!-- 镜像URL -->
      <url>http://maven.aliyun.com/nexus/content/groups/public</url>
    </mirror>

```



##### mvn指令

###### mvn compile 构建target编译目录

###### mvn clean 清除target目录

###### mvn test 测试

###### mvn package 打包（只打包源程序）

###### mvn install 安装到本地仓库



##### 依赖传递

###### 直接依赖

###### 间接依赖



##### 依赖传递冲突问题

![image-20230920105545387](C:\Users\wordhao\AppData\Roaming\Typora\typora-user-images\image-20230920105545387.png)

###### 路劲优先：层级越深优先级越低，反之

###### 声明优先：相同层级被依赖时，配置顺序考前的覆盖配置顺序靠后的

###### 特殊优先：同级配置了相同资源的不同版本，后配置的覆盖先配置的



##### 可选依赖

```xml
<dependency>
    <groupId>log4j</groupId>
    <artifactId>log4j</artifactId>
    <version>1.2.17</version>
    <!-- true——使对外不可传递 false——对外可传递 -->
    <optional>true</optional>
</dependency>
```



##### 排除依赖

```xml
<dependency>
    <groupId>log4j</groupId>
    <artifactId>log4j</artifactId>
    <version>1.2.17</version>
    <!-- 排除依赖 -->
    <exclusions>
        <exclusion>
            <groupId>com.itextpdf</groupId>
            <artifactId>itextpdf</artifactId>
            <!-- 不需要版本号 -->
        </exclusion>
    </exclusions>
</dependency>
```



##### 依赖范围

###### 依赖的jar默认情况可以在任何地方使用，通过scope标签设定作用范围

###### 作用范围

- 主程序范围有效（main文件夹范围）

- 测试程序范围有效（test文件夹范围）

- 是否参与打包（package指令范围）

  

```xml
<dependency>
    <groupId>log4j</groupId>
    <artifactId>log4j</artifactId>
    <version>1.2.17</version>
    <scope>compile/test/provided/runtime</scope>
</dependency>
```



![image-20230920202213912](C:\Users\wordhao\AppData\Roaming\Typora\typora-user-images\image-20230920202213912.png)



##### 生命周期与插件



