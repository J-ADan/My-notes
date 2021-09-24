# Maven

Maven项目对象模型(POM)，可以通过一小段描述信息来管理项目的构建，报告和[文档](https://baike.baidu.com/item/文档/1009768)的[项目管理工具](https://baike.baidu.com/item/项目管理工具/6854630)软件。

Maven 除了以程序构建能力为特色之外，还提供高级项目管理工具。由于 Maven 的缺省构建规则有较高的可重用性，所以常常用两三行 Maven 构建脚本就可以构建简单的项目。由于 Maven 的面向项目的方法，许多 Apache Jakarta 项目发文时使用 Maven，而且公司项目采用 Maven 的比例在持续增长。

Maven这个单词来自于意第绪语（犹太语），意为知识的积累，最初在Jakata Turbine项目中用来简化构建过程。当时有一些项目（有各自Ant build文件），仅有细微的差别，而JAR文件都由[CVS](https://baike.baidu.com/item/CVS)来维护。于是希望有一种标准化的方式构建项目，一个清晰的方式定义项目的组成，一个容易的方式发布项目的信息，以及一种简单的方式在多个项目中共享[JARs](https://baike.baidu.com/item/JARs)。



**为什么学习Maven：**

1. 在JavaWeb项目的开发中，需要大量的jar包，都需要手动导入
2. 我们需要一个东西帮助我们手动导入jar包，由此Maven诞生



## Maven 架构管理工具

在我们当下的学习使用中，就是来方便我们管理导入jar包的

**Maven 的核心思想：** **约定大于配置** （即有约定，有规范，不要去违反）

Maven会规定好如何去编写Java代码，必须按照规范来编写



Maven官网：https://maven.apache.org/

![image-20210813090624418](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813090624418.png)



## Maven 环境配置

![image-20210813091523916](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813091523916.png)

![image-20210813091539129](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813091539129.png)

![image-20210813091559476](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813091559476.png)

![image-20210813091655534](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813091655534.png)



## 阿里镜像配置

```bash
<mirror>
      <id>alimaven</id>
      <name>aliyun maven</name>
      <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
      <mirrorOf>central</mirrorOf>
</mirror>
```

![image-20210813092007017](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813092007017.png)

## 本地仓库配置

```html
<localRepository>G:\Java\Maven\apache-maven-3.8.1\maven-repo</localRepository>
```



## IDEA Maven 操作

**创建Maven项目**

![image-20210813093401698](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813093401698.png)

![image-20210813094444576](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813094444576.png)

![image-20210813093854674](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813093854674.png)

![image-20210813094738477](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813094738477.png)

**不报错即成功：**

![image-20210813095145191](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813095145191.png)

### IDEA MAVEN 配置

![image-20210813095748734](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813095748734.png)



### 标记文件夹功能

![image-20210813163048759](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813163048759.png)

![image-20210813163606693](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813163606693.png)



## 给项目配置Tomcat

![image-20210813164007898](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813164007898.png)

![image-20210813164117397](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813164117397.png)

![image-20210813164355113](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813164355113.png)

![image-20210813164523918](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813164523918.png)

**选择第一个即可，下面的名称可以不写，不写的默认路径为 localhost:8080，填入路径之后，访问路径为 localhost:8080/填入名称，这个过程叫做，虚拟路径映射**



## Maven 的 pom 文件

![image-20210813165157809](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813165157809.png)



pom.xml是Maven的核心配置文件。

```xml
<?xml version="1.0" encoding="UTF-8"?>

<!--Maven的版本和头文件-->
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

<!--  刚配置的GAV-->
  <groupId>com.sdut</groupId>
  <artifactId>JavaWeb-01-maven</artifactId>
  <version>1.0-SNAPSHOT</version>
<!--  项目的打包方式-->
  <packaging>war</packaging>

  <name>JavaWeb-01-maven Maven Webapp</name>
  <!-- FIXME change it to the project's website -->
  <url>http://www.example.com</url>

<!--  配置-->
  <properties>
<!--    项目的默认构建编码-->
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
<!--    编码的版本-->
    <maven.compiler.source>1.7</maven.compiler.source>
    <maven.compiler.target>1.7</maven.compiler.target>
  </properties>

  <dependencies>
<!--    具体依赖的jar包-->
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>
  </dependencies>

<!--  项目构建的东西-->
  <build>
    <finalName>JavaWeb-01-maven</finalName>
    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
      <plugins>
        <plugin>
          <artifactId>maven-clean-plugin</artifactId>
          <version>3.1.0</version>
        </plugin>
        <!-- see http://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_war_packaging -->
        <plugin>
          <artifactId>maven-resources-plugin</artifactId>
          <version>3.0.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.8.0</version>
        </plugin>
        <plugin>
          <artifactId>maven-surefire-plugin</artifactId>
          <version>2.22.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-war-plugin</artifactId>
          <version>3.2.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-install-plugin</artifactId>
          <version>2.5.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-deploy-plugin</artifactId>
          <version>2.8.2</version>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
</project>

```

![image-20210813170417252](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813170417252.png)



## 其他

![image-20210813171350330](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813171350330.png)

maven的jar包目录树



```xml
<!--    maven资源导出失败解决方案-->
    <build>
        <resources>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
            </resource>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>true</filtering>
            </resource>
        </resources>
    </build>
```



![image-20210813173303592](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813173303592.png)

将这里的webapp版本替换为跟tonncat一致

![image-20210813173452899](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813173452899.png)

打开全复制

![image-20210813173620108](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813173620108.png)

![image-20210813173645553](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813173645553.png)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                      http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0"
         metadata-complete="true">

  <display-name>Welcome to Tomcat</display-name>
  <description>
    Welcome to Tomcat
  </description>

</web-app>
```

