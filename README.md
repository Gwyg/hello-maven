# 发布jar包到maven中央仓库

## 准备账号

### 创建账号

https://central.sonatype.com/

右上角的“登录”链接，支持通过 Google 或 GitHub 进行社交登录。也可以选择注册自己的用户名和密码。我这里选择github进行登录。

![img](https://lanshanteam.feishu.cn/space/api/box/stream/download/asynccode/?code=YWQ3OGJmZjhhYjcwNTk5Njg5MDg4MGMwNjkwYmViM2ZfRzllNjB1a2hmS2I4MW45TXhTVmUweXJjQWY5YzdyUk1fVG9rZW46TGIyT2JBbU1Fb253dlV4ek5semNDbVJ4bmJkXzE3MzMxNDc4Mjg6MTczMzE1MTQyOF9WNA)

![img](https://lanshanteam.feishu.cn/space/api/box/stream/download/asynccode/?code=YWYyNzQ1ZWU5ZjcyMmVhOGE5YWFkNzFjMTUzYTNhZjlfT09yd2llcHo3UGYzdFF4em5uZFJTSWlVT3Nydll0aU5fVG9rZW46THJLRGJTUXFub0VtQjV4TExNUWMwREFpbjhmXzE3MzMxNDc4Mjg6MTczMzE1MTQyOF9WNA)

登录完之后是这样的：

![img](https://lanshanteam.feishu.cn/space/api/box/stream/download/asynccode/?code=NTE2NmIwOGRiNmI4ZWYxMDBjYWU0YTA1NjVlNmFiNGJfRG1mZGJuR1luTGJiTHVsRlJsSW1RRmxMbXhROHJqVDVfVG9rZW46TERiRWJSMkhOb1Brakd4aXlmcmNNd3ZkblJmXzE3MzMxNDc4Mjg6MTczMzE1MTQyOF9WNA)

### 新建命名空间

如果你使用 GitHub 登录的，该步骤可跳过。

![img](https://lanshanteam.feishu.cn/space/api/box/stream/download/asynccode/?code=N2Q0ZmQ5NTI4MmQ5NTI4NmI3ODA5OTc1MTAzMDBjZWFfWDdCOHNFT2I2QUo2anN2ekY4SmpSZFduT2FqbzhUbWhfVG9rZW46SXFBTGI2Q0xCbzFTS254VGRUY2N1cjZPblZnXzE3MzMxNDc4Mjg6MTczMzE1MTQyOF9WNA)

![img](https://lanshanteam.feishu.cn/space/api/box/stream/download/asynccode/?code=NDU3N2MyY2E1ZjVmYjVmNGQ1YjdhODg1OTYwODcxOTJfRkE5QW9pemxYbk8wZ3doRjBzWklqWjBITk5FTUF3WjVfVG9rZW46UUNpcmJDdGd3b3NkYVZ4ZDV6b2NCVWNsblJtXzE3MzMxNDc4Mjg6MTczMzE1MTQyOF9WNA)

![img](https://lanshanteam.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjA4MzQ0YzcyM2VlMzRiNmE4MDA2YWFlNjVjZTQwMTBfUnFPNFlsZkNWdHppaVg0bnFtT2NmaHJYdmxJM1QzaUtfVG9rZW46TGEyRmJVYldNb0R0aGV4TzVVeGNTQjhrbjJlXzE3MzMxNDc4Mjg6MTczMzE1MTQyOF9WNA)

如果你的代码存在 `GitHub` 上，你就需要把命名空间设置为`io.gitee.myusername`。这里的`myusername`是你的github地址，例如我的的是`https://github.com/``gwyg`所以我的命名空间是：`io.github.gwyg`

> 其他的仓库可以按照下面的要求来创建： **GitHub io.github.myusername** **GitLab io.gitlab.myusername** **Gitee io.gitee.myusername** **Bitbucket io.bitbucket.myusername**

### 验证命名空间

创建之后需要验证命名空间来依次证明这个命名空间是你独有的，需要在对应的地址创建一个[开源](https://edu.csdn.net/cloud/pm_summit?utm_source=blogglc&spm=1001.2101.3001.7020)的仓库，名称就是你点击`verify namespace`的名称，例如下面这样：

我这里是创建了gitee仓库的一个命名空间

![img](https://lanshanteam.feishu.cn/space/api/box/stream/download/asynccode/?code=ZmIzNDI2NjY2MjVjMzJmNmQ5YmUzOTk0MDFhYjNmOGFfb0ZyOHRFTFRoak5acXdvckJBY1BpeFJHZVRaM041UFBfVG9rZW46Q2hON2JMd2xsb0dXWmd4NFpRaGNqazNMbjN5XzE3MzMxNDc4Mjg6MTczMzE1MTQyOF9WNA)

![img](https://lanshanteam.feishu.cn/space/api/box/stream/download/asynccode/?code=YjIwNzM0YTNlOGJiZTRlYmFiMmMxODk4YWNkYTk3NTRfRk03SzZwUkRqR3BmMkFxT1FuQTA2SmhBNEVObzNPYmJfVG9rZW46UVd0S2JaOVZLb2xGYUZ4SnptRGNBWWMzbkZkXzE3MzMxNDc4Mjg6MTczMzE1MTQyOF9WNA)

### 创建push的账号和密码

这一步抛弃了原来固定的username和password，选择了一个随机的username和password，这个username和password用来push你的jar包到中央仓库里面去，所以一定要保存好，以后都不会显示了，只有在创建成功的时候才会显示一次。

![img](https://lanshanteam.feishu.cn/space/api/box/stream/download/asynccode/?code=N2E5NWNjNjRmMGFiYmViYTg3ZWFhNmU3NDM0ZTlhMGRfOE9NcGRoV0hsQXYzcE42RUlCR1NZYzJGYkZwUWY1Y1ZfVG9rZW46TVJGVWIxdGlJb0lRVUN4OEFUcWMxWHU4bkFnXzE3MzMxNDc4Mjg6MTczMzE1MTQyOF9WNA)

![img](https://lanshanteam.feishu.cn/space/api/box/stream/download/asynccode/?code=OTY3YzU0OGE2MDg4OTAyNWJiOGQ2YTNiODI4MTdjNjZfeG12TnR3U3NXWjIxMGR3dllnMVk4QVlDbHduQWNpWjZfVG9rZW46SkF1a2J4RFVPb3d5V1R4bEZUdmNNZkJ2blBoXzE3MzMxNDc4Mjg6MTczMzE1MTQyOF9WNA)

![img](https://lanshanteam.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjNhYjJkY2FlOGIyMDEyZTMyZWEyYTgxMTM0Yzk3MWJfcm9oVjhha29KdUhyYmJRUFJaclAza0RtMms2aVlKaWFfVG9rZW46R0JneWIxeEJDb1kyRVl4ZUhoa2NSc1Rmbm5oXzE3MzMxNDc4Mjg6MTczMzE1MTQyOF9WNA)

![img](https://lanshanteam.feishu.cn/space/api/box/stream/download/asynccode/?code=YTE5MWY5YTU4ODQ3YzA1M2QyMGZmMzZlOTk4NGM0ZGVfRVM4am5LRWVDRGFlWGM4TUJBSGJoaDE2V1lqWlg3RFBfVG9rZW46RlN5c2JHaHc2b3p4T2x4MFNuSWNaaWNobk5ZXzE3MzMxNDc4Mjg6MTczMzE1MTQyOF9WNA)

把他粘贴到maven的setting.xml 文件里面

这个`${server}`可以写成你自定义的id，待会会用到，记住。

```XML
<server>
        <id>${server}</id>
        <username>w2JL882q</username>
        <password>fwCP62XwRq3KiKFIHttKQK2RMRuDgxsoWenUBADyC5PP</password>
</server>
```

![img](https://lanshanteam.feishu.cn/space/api/box/stream/download/asynccode/?code=MjY1ZGY0YTI1M2YwYjRhYzQxMzJhYzlkMGViNWExNzlfSUFWNXlDUVkyYTFkekN6UGQ3bkQwNUpHaHRTZ2lYNmJfVG9rZW46WGI0V2JmS3FWb0JLR054YlJDQmNkZ1BFbldmXzE3MzMxNDc4Mjg6MTczMzE1MTQyOF9WNA)

## GPG准备

### 下载GPG

GPG 用于创建asc文件用于验证你的文件的正确性和安全性，我们直接去官网下载：

https://gnupg.org/download/index.html

![img](https://lanshanteam.feishu.cn/space/api/box/stream/download/asynccode/?code=M2ZiNzU2NjQyODgzNjk2NTJhNzU0OTM0ZTExNTJkMjVfUWNEbEQ5R1AzMWNweFZ1a21EODdMbmxRY0c2bkdua2pfVG9rZW46RVFMd2JmSVRob0gwU0Z4ZlFSVWN6Vll2bmgzXzE3MzMxNDc4Mjg6MTczMzE1MTQyOF9WNA)

安装过程比较简单，这里就不单独截图来教学了，安装的时候可以把这些开发工具放在同一个地方，方便管理。

### 生成秘钥

![img](https://lanshanteam.feishu.cn/space/api/box/stream/download/asynccode/?code=YWYwMzQ0YzJjZjM4NWM4NGVkNGUyN2E3NzEyZjZjMzhfNVB4VWVaNmlybWpHWVdoSWNubjZnVEJjUVdXemJiZ0xfVG9rZW46WGpsRWJVeHQzb1p2VEp4bDFSeGNwY2hmblBoXzE3MzMxNDc4Mjg6MTczMzE1MTQyOF9WNA)

安装好之后我有两个目录，进入 GnuPG\bin 这个目录下的cmd

输入`gpg --gen-key`回车

依次输入名称，邮箱地址，**名称输入你命名空间的名称（我这里使用的是github上的那个）**

然后在弹出的窗口设置一个密码，用来保护密钥对。

![img](https://lanshanteam.feishu.cn/space/api/box/stream/download/asynccode/?code=NmQ3ZTk4ZjQ5MjEzMjkzYjYzNmEzYzdjNTI4NmJjNWVfaW0xQU5Sa21BcmZkWW1IQWlHWE9DcWVTNVEyTmdQVXdfVG9rZW46QVpJMWJMQUFrb3B6b014UG5aWWNmZTl5bndoXzE3MzMxNDc4Mjg6MTczMzE1MTQyOF9WNA)

### 发布秘钥

上面 067FBBE0CB587465FD81AF9C580E420B49E48996 就是密钥id

![img](https://lanshanteam.feishu.cn/space/api/box/stream/download/asynccode/?code=YmQ1NTA5NDEzMjlmZWQ2OGE1ZDlkNjI3NzI2YzZiMTlfMHBpbEFvQWlhZE9kNDY4dXhaVFUzd3gxZ0xtemRWQklfVG9rZW46SENSTmJxWGx6b1VpUVB4cDlEa2M3dXBtblhlXzE3MzMxNDc4Mjg6MTczMzE1MTQyOF9WNA)

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

![img](https://lanshanteam.feishu.cn/space/api/box/stream/download/asynccode/?code=MzgwMDBkMzNjNmFkMWMxMWUwYzUzYjEyNzhiOGU0M2NfYkJtUDdKRndORzlXR0pFMlFMRXBMVmJXdzF3TkJVc0tfVG9rZW46UTY5MGIyaVZ6b3J5WWp4cEczMmN3MFJ6bmxjXzE3MzMxNDc4Mjg6MTczMzE1MTQyOF9WNA)

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

![img](https://lanshanteam.feishu.cn/space/api/box/stream/download/asynccode/?code=ZmU2NzdiN2Q5Y2MwMmIwYTk0MjkxNTA2YjlkYjhiMDZfc0g4ZFhiT01VMk9QMmRJSTA3YXlTQWpYZzlOQk9QOVRfVG9rZW46QmFNdWJXRmEyb1hRU2J4dUxDdWM4WkF1bmVmXzE3MzMxNDc4Mjg6MTczMzE1MTQyOF9WNA)

打包完成

![img](https://lanshanteam.feishu.cn/space/api/box/stream/download/asynccode/?code=MjVmNTIyZGVkZjgxYjM1NDliZjQzMWQ5NmYxNTg1NTdfQlMzVEdKbmh5bDBZYjdaYURqYVc5VUlqeUQ1OThheFFfVG9rZW46U0tUdGJwZWd2b3pGdDV4UXFhY2NZWkZjbnNnXzE3MzMxNDc4Mjg6MTczMzE1MTQyOF9WNA)

### 发布jar包

打包成功之后`Deployments`模块里面也有对应的步骤，刚刚我们在idea控制台看到的id是：`1ac77d8b-5abe-4458-ba2a-9d7484601370`也就对应这个页面里面的`Deployment ID`

这个时候我们点击`Publish`意思就是将我们的jar包发布了

发布之后需要等待通过。

![img](https://lanshanteam.feishu.cn/space/api/box/stream/download/asynccode/?code=OTE4YzQ0ZDZhMmQxNjNiOTliY2I5NmI0ZWFjNTc1NThfU25KQk1qeDBCUTBYeENxRDJSd21sdmVYakhCQ2prRldfVG9rZW46UXRLcGIyYXR1bzRic0p4MVBSOGN5UDlQblFoXzE3MzMxNDc4Mjg6MTczMzE1MTQyOF9WNA)

![img](https://lanshanteam.feishu.cn/space/api/box/stream/download/asynccode/?code=YjNhM2Y5NjdkMTAxNGE1NDUzM2JkOTA0NGYyMmNlZjFfMnNWbUNsbk9UTkNpb2ZrQTA5QVZUd2Rlb0JBTUREcVRfVG9rZW46Vk01aWJBd1Ywb2dLU0x4bnB0eWNIbGhIbldlXzE3MzMxNDc4Mjg6MTczMzE1MTQyOF9WNA)

几分钟之后就能通过

### 搜索我们的jar包

搜索到就是成功了

![img](https://lanshanteam.feishu.cn/space/api/box/stream/download/asynccode/?code=ZWZjNTVhNDgwZTFiYWM2NDM1ODgzNGIyMjZiNDAzMjJfR3RJeXdXRERHZUFJczJGazhWdmh6aEZJTm1STkJCSFRfVG9rZW46VVZmYWJGdnJYb3c0YlR4Y2NoeWNsY1lZbkJmXzE3MzMxNDc4Mjg6MTczMzE1MTQyOF9WNA)

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

![img](https://lanshanteam.feishu.cn/space/api/box/stream/download/asynccode/?code=NjNhMWY0YzVkNTU1MzQ3ODBjZGI1ZDdiY2ViYjU5NzFfRzVGN2I0SmRrdTlMY0RyZkhET0I0Vlo1RGFtTkFlU2tfVG9rZW46S2JCbWI0YUR4b25WUzR4TlYyWGNBcVVqbm5iXzE3MzMxNDc4Mjg6MTczMzE1MTQyOF9WNA)

成功运行，到此就是完整的上传流程了

![img](https://lanshanteam.feishu.cn/space/api/box/stream/download/asynccode/?code=NjZjMzc3ZWFjNTQ5Yzk5ZjY2YTgxZDMwZjZkYjk4OTBfazg4ZU5BZWtBeG90SDRhSUsxa3pwbzVucUZ1dDFvbGdfVG9rZW46UkpMd2JqR1lTb0VEVnR4MEJyeWNyYUFwbktkXzE3MzMxNDc4Mjg6MTczMzE1MTQyOF9WNA)