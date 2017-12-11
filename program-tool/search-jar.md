# 搜索jar文件的X种方法

> 以 struts 2.3.20 为例实验各种搜索方法

## 百度搜索
* 关键词 `struts.jar 2.3.20`: 会引导到 CSDN 对应的下载地址
* 关键词 `struts 2.3.20`: 会直接定位到 Apache Struts 的官网文件索引地址

## 网站
* [官网](http://struts.apache.org/): [download页面](http://struts.apache.org/download.cgi#struts2514.1)
   * 一般会提供最新的版本下载
   * 指定版本可以到 [archive 列表](https://archive.apache.org/dist/struts/) 中找到
* [CSDN](http://download.csdn.net): 搜索 `struts 2.3.20`
* [盘多多](http://www.panduoduo.net/): 在网盘中搜索 `struts 2.3.20`
* [mvnrepository](http://mvnrepository.com/): 搜索 `struts 2.3.20`
   * 在结果中选择对应的分类及版本
   * 点 jar 链接可以直接下载
   * 也可以根据项目类型添加依赖

### Maven
在 pom.xml 中添加依赖

```xml
<!-- https://mvnrepository.com/artifact/org.apache.struts/struts2-core -->
<dependency>
    <groupId>org.apache.struts</groupId>
    <artifactId>struts2-core</artifactId>
    <version>2.3.20</version>
</dependency>
```

### Gradle

```xml
// https://mvnrepository.com/artifact/org.apache.struts/struts2-core
compile group: 'org.apache.struts', name: 'struts2-core', version: '2.3.20'
```

### SBT

```xml
// https://mvnrepository.com/artifact/org.apache.struts/struts2-core
libraryDependencies += "org.apache.struts" % "struts2-core" % "2.3.20"
```

### Ivy

```xml
<!-- https://mvnrepository.com/artifact/org.apache.struts/struts2-core -->
<dependency org="org.apache.struts" name="struts2-core" rev="2.3.20"/>
```

### Grape

```xml
// https://mvnrepository.com/artifact/org.apache.struts/struts2-core
@Grapes(
    @Grab(group='org.apache.struts', module='struts2-core', version='2.3.20')
)
```

### Leiningen

```xml
;; https://mvnrepository.com/artifact/org.apache.struts/struts2-core
[org.apache.struts/struts2-core "2.3.20"]
```

### Buildr

```xml
# https://mvnrepository.com/artifact/org.apache.struts/struts2-core
'org.apache.struts:struts2-core:jar:2.3.20'
```
