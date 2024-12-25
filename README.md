# 发布jar包到maven中央仓库

## 准备账号

### 创建账号

https://central.sonatype.com/

右上角的“登录”链接，支持通过 Google 或 GitHub 进行社交登录。也可以选择注册自己的用户名和密码。我这里选择github进行登录。

![image](https://github.com/user-attachments/assets/f0b708b1-c111-4114-b4ac-3ef31cbcee16)


![image](https://github.com/user-attachments/assets/b74b2fe1-6580-47dc-ad50-f017f13668b9)


登录完之后是这样的：

![image](https://github.com/user-attachments/assets/3ae11958-c245-4538-bd56-55eaa12eada3)


### 新建命名空间

如果你使用 GitHub 登录的，该步骤可跳过。

![image](https://github.com/user-attachments/assets/9a4796bb-0924-4f7d-9239-52586cda5d32)


![image](https://github.com/user-attachments/assets/c394dab0-b1fa-48f3-a33d-165e8fe43d1e)


![image](https://github.com/user-attachments/assets/3408a7be-6457-453b-a3e3-0ed1b69daa2b)


如果你的代码存在 `GitHub` 上，你就需要把命名空间设置为`io.github.myusername`。这里的`myusername`是你的github地址，例如我的的是`https://github.com/``gwyg`所以我的命名空间是：`io.github.gwyg`

> 其他的仓库可以按照下面的要求来创建： **GitHub io.github.myusername** **GitLab io.gitlab.myusername** **Gitee io.gitee.myusername** **Bitbucket io.bitbucket.myusername**

### 验证命名空间

创建之后需要验证命名空间来依次证明这个命名空间是你独有的，需要在对应的地址创建一个[开源](https://edu.csdn.net/cloud/pm_summit?utm_source=blogglc&spm=1001.2101.3001.7020)的仓库，名称就是你点击`verify namespace`的名称，例如下面这样：

我这里是创建了gitee仓库的一个命名空间

![image](https://github.com/user-attachments/assets/5f602963-5c1a-494b-9acc-942eeeb0149d)


![image](https://github.com/user-attachments/assets/888ce439-459a-4465-a335-c1f3ddfdbcd0)


### 创建push的账号和密码

这一步抛弃了原来固定的username和password，选择了一个随机的username和password，这个username和password用来push你的jar包到中央仓库里面去，所以一定要保存好，以后都不会显示了，只有在创建成功的时候才会显示一次。

![image](https://github.com/user-attachments/assets/1de0d57e-a55a-4e7c-be75-120d415b9bec)


![image](https://github.com/user-attachments/assets/c1cdf579-1b5d-4498-934c-85614b2e34bd)


![image](https://github.com/user-attachments/assets/68dba56e-0f77-4dbe-bd9c-cee5325cc4c9)


![image](https://github.com/user-attachments/assets/16d6f305-e8b9-48e1-8d36-14818aeec7dc)


把他粘贴到maven的setting.xml 文件里面

这个`${server}`可以写成你自定义的id，待会会用到，记住。

```XML
<server>
        <id>${server}</id>
        <username>w2JL882q</username>
        <password>fwCP62XwRq3KiKFIHttKQK2RMRuDgxsoWenUBADyC5PP</password>
</server>
```

![image](https://github.com/user-attachments/assets/b952abec-ac7d-4467-a195-958d4fa8a742)


## GPG准备

### 下载GPG

GPG 用于创建asc文件用于验证你的文件的正确性和安全性，我们直接去官网下载：

https://gnupg.org/download/index.html

![image](https://github.com/user-attachments/assets/4b27e57d-b1e3-478e-9ddf-67e3abfd687d)


安装过程比较简单，这里就不单独截图来教学了，安装的时候可以把这些开发工具放在同一个地方，方便管理。

### 生成秘钥

![image](https://github.com/user-attachments/assets/c369cf95-eecd-410e-a9ef-31ba2c23435a)


安装好之后我有两个目录，进入 GnuPG\bin 这个目录下的cmd

输入`gpg --gen-key`回车

依次输入名称，邮箱地址，**名称输入你命名空间的名称（我这里使用的是github上的那个）**

然后在弹出的窗口设置一个密码，用来保护密钥对。

![image](https://github.com/user-attachments/assets/441d1413-cdba-4b07-ae68-f2a0a4896748)



### 发布秘钥

上面 067FBBE0CB587465FD81AF9C580E420B49E48996 就是密钥id

![image](https://github.com/user-attachments/assets/2bd11572-a5c4-42fa-81b3-d1aa4f974922)



```Bash
gpg --keyserver keyserver.ubuntu.com --send-keys 067FBBE0CB587465FD81AF9C580E420B49E48996
```

这里发布到`keyserver.ubuntu.com`服务器上，这样中央仓库也有你的密钥，所以它才能验证你的身份

> As SKS Keyserver Network is being deprecated we recommend the use an specific GPG keyserver. Current GPG Keyservers supported by Central Servers are: **keyserver.ubuntu.com keys.openpgp.org pgp.mit.edu**

如果发布失败开源用上面的其他两个地址

### 验证秘钥

验证秘钥是否发布成功：

```Bash
gpg --keyserver keyserver.ubuntu.com --recv-keys 067FBBE0CB587465FD81AF9C580E420B49E48996
```

出现下面内容则说明发布成功

                                                                                                            
                                                                                         ![image](https://github.com/user-attachments/assets/5549d619-48bc-4851-977f-6b0073bc97fa)




## 发布jar包

### 编辑pom文件

`dependencies`里面的内容是根据你的项目里面的实际情况写，其他的都都安装实际情况写。

```XML
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>


    <groupId>io.github.gwyg</groupId>
    <artifactId>hello-maven</artifactId>
    <version>0.0.1</version>
    <packaging>jar</packaging>
    <name>hello-maven</name>
    <description>hello-maven</description>
    <url>https://github.com/Gwyg/hello-maven</url>

    <licenses>
        <license>
            <name>The Apache Software License, Version 2.0</name>
            <url>http://www.apache.org/licenses/LICENSE-2.0.txt</url>
        </license>
    </licenses>


    <developers>
        <developer>
            <name>gwyg</name>
            <email>1773511271@qq.com</email>
            <!-- organization及相关信息，可选 -->
<!--            <organization>组织名称</organization>-->
<!--            <organizationUrl>组织官网</organizationUrl>-->
            <url>https://github.com/Gwyg/hello-maven</url>
            <timezone>+8</timezone>
        </developer>
    </developers>


  <!--  <scm>
        <connection>https://github.com/Gwyg/hello-maven.git</connection>
        <developerConnection>scm:git:ssh://git@github.com:Gwyg/hello-maven.git</developerConnection>
        <url>https://github.com/Gwyg/hello-maven</url>
    </scm>-->
    <scm>
        <!-- 项目URL -->
        <url>https://github.com/Gwyg/hello-maven</url>
        <!-- 项目URL.git -->
        <connection>scm:git:https://github.com/Gwyg/hello-maven.git</connection>
        <!-- 项目URL.git -->
        <developerConnection>scm:git:https://github.com/Gwyg/hello-maven.git</developerConnection>
    </scm>



    <properties>
        <java.version>1.8</java.version>
        <maven.compiler.source>${java.version}</maven.compiler.source>
        <maven.compiler.target>${java.version}</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
        <!-- 服务id 也就是setting.xml中的servers.server.id -->
        <serverId>gwyg</serverId>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>


    <build>
        <plugins>
            <!-- 编译插件，设置源码以及编译的jdk版本 -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>${maven.compiler.source}</source>
                    <target>${maven.compiler.target}</target>
                </configuration>
            </plugin>
            <!-- Source -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-source-plugin</artifactId>
                <version>2.2.1</version>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>jar-no-fork</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
            <!-- Javadoc -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-javadoc-plugin</artifactId>
                <version>2.9.1</version>
                <configuration>
                    <additionalparam>-Xdoclint:none</additionalparam>
                </configuration>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>jar</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
            <!-- Javadoc -->
            <!-- Gpg Signature -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-gpg-plugin</artifactId>
                <version>1.5</version>
                <executions>
                    <execution>
                        <phase>verify</phase>
                        <goals>
                            <goal>sign</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
            <!-- 新方式的配置，将组件部署到OSSRH并将其发布到Central Repository-->
            <plugin>
                <groupId>org.sonatype.central</groupId>
                <artifactId>central-publishing-maven-plugin</artifactId>
                <version>0.4.0</version>
                <extensions>true</extensions>
                <configuration>
                    <!-- 服务id 也就是setting.xml中的servers.server.id -->
                    <publishingServerId>gwyg</publishingServerId>
                    <tokenAuth>true</tokenAuth>
                </configuration>
            </plugin>
        </plugins>
    </build>

    <distributionManagement>
        <snapshotRepository>
            <id>${serverId}</id>
            <url>https://central.sonatype.com/</url>
        </snapshotRepository>
    </distributionManagement>

</project>
```

### 打包上传

**mvn** 先clean 后deploy

不要有中文路径

这个时候会让你输入你在开头设置的密码，输入成功开始打包上传。

![image](https://github.com/user-attachments/assets/c5a2ad61-d4b3-46c3-b2ad-6e672e48fd7b)



打包完成

![image](https://github.com/user-attachments/assets/f67e6375-e347-4401-bb28-250d8c3a16ff)


### 发布jar包

打包成功之后`Deployments`模块里面也有对应的步骤，刚刚我们在idea控制台看到的id是：`1ac77d8b-5abe-4458-ba2a-9d7484601370`也就对应这个页面里面的`Deployment ID`

这个时候我们点击`Publish`意思就是将我们的jar包发布了

发布之后需要等待通过。

![image](https://github.com/user-attachments/assets/53bc3a3b-df79-4a94-8cbd-a5fcd481005f)



![image](https://github.com/user-attachments/assets/88bbc55b-a59c-4cd6-a4b7-72534716d06a)



几分钟之后就能通过

### 搜索我们的jar包

搜索到就是成功了

![image](https://github.com/user-attachments/assets/99865a56-60f9-407e-8c8e-d4861a50610a)



## 测试jar包

在idea中就可以导入我们自己发布的jar包并使用了

```XML
<dependency>
    <groupId>io.github.gwyg</groupId>
    <artifactId>hello-maven</artifactId>
    <version>0.0.2</version>
</dependency>
```

导入我们上传的依赖

![image](https://github.com/user-attachments/assets/ce81871f-acb9-444b-8609-c5e0c3526896)



成功运行，到此就是完整的上传流程了

![image](https://github.com/user-attachments/assets/0937f597-9c18-4786-9f53-d9113de05788)

