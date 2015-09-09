
所有maven工程的parent都是此pom,主要用于统一各个工程依赖版本。


maven settiing.xml 配置：

```
<?xml version="1.0" encoding="UTF-8"?>

<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">

  <!-- 自定义本地仓库地址,其默认值为~/.m2/repository -->
  <localRepository>~/.m2/repository</localRepository>

  <servers>
    <server>
        <id>mdsh</id>
        <username>deployment</username>
        <password>admin123</password>
    </server>
  </servers>

  <mirrors>
    <mirror>
        <id>mdsh</id>
        <name>internal nexus repository</name>
        <url>http://192.168.11.111:8081/nexus/content/groups/public/</url>
        <mirrorOf>central</mirrorOf>
    </mirror>
  </mirrors>

    <profiles>
        <profile>
            <id>mdsh-profile</id>
            <repositories>
                <repository>
                    <id>mdsh-nexus</id>
                    <name>mdsh</name>
                    <url>http://192.168.11.111:8081/nexus/content/groups/public/</url>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                    <snapshots>
                        <enabled>true</enabled>
                        <updatePolicy>interval:10</updatePolicy>
                    </snapshots>
                </repository>
            </repositories>
        </profile>
    </profiles>
    <activeProfiles>
        <activeProfile>mdsh-profile</activeProfile>
    </activeProfiles>

</settings>
```

maven 工程pom文件添加parent依赖

```
        <parent>
            <groupId>com.mdsh</groupId>
            <artifactId>mdsh-root-pom</artifactId>
	  	    <version>1.0-SNAPSHOT</version>
        </parent> 

```


工程实例：

```

https://git.coding.net/woowo/mdsh_order_java.git

```
