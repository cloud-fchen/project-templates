
### User Guide 

#### 创建工程

我们可以通过下列命令来生成一个多个module的maven工程

```bash 
mvn -X -e org.apache.maven.plugins:maven-archetype-plugin:2.4:generate      \
        -DarchetypeGroupId=cloud.fchen                                      \
        -DarchetypeArtifactId=scala-multi-module                            \
        -DarchetypeVersion=1.0                                              \
        -DartifactId=example                                                \
        -DgroupId=cloud.fchen                                               \
        -DarchetypeCatalog=http://private-host-pository/nexus/content/groups/public \
        -DinteractiveMode=false
```

相关参数以及说明

|  参数   | 含义     |说明|
| --- | --- | --- |
|archetypeGroupId|模版的groupId |无需变动|
|archetypeArtifactId|模版的artifactId|无需变动|
|archetypeVersion|模版的Version||
|groupId|即将创建的工程的groupId||
|artifactId|即将创建的工程的artifactId|根据项目功能来命名|
|archetypeCatalog|模版的地址|如果在settings.xml中配置了maven私有仓库则无需配置|
|interactiveMode|false||

archetype可选参数说明 

|参数值|说明|
| --- | --- |
|scala-single-module|单模块maven工程|
|scala-multi-module|多模块maven工程|

> **NOTE:** 后续可以继续往该工程里添加所需的工程模版

运行之后我们会在当前目录生成一个名为`example`的maven多模块工程

一个单模块的maven工程模版生成脚本示例

```bash
mvn -X -e org.apache.maven.plugins:maven-archetype-plugin:2.4:generate      \
        -DarchetypeGroupId=cloud.fchen                                      \
        -DarchetypeArtifactId=scalak-single-module                          \
        -DarchetypeVersion=1.0                                              \
        -DartifactId=single-example                                         \
        -DgroupId=cloud.fchen                                               \
        -DinteractiveMode=false
```

### 打包

以多模块的maven工程模版为例

对bootstrap脚本赋予可执行权限
```bash
chmod a+x ./bootstrap.sh
```
并修改bootstrap脚本的`APP_NAME`和`APP_VERSION`

> **NOTE:** 现在需要手动修改，后续考虑增加到脚本自动化修改

```bash
./bootstrap.sh package
```

> 运行成功后会在工程根目录下生成一个${project}-bin-${version}.tgz的压缩包，包含启动所需的脚本/配置文件/依赖包

打包命令可以带上maven打包所需的参数，例如下列命令就可以将spark相关依赖打包到tgz包当中，默认不会将spark依赖打包到tgz包当中
```bash 
./bootstrap.sh package -Pwith-dependencies
```

### 运行

运行多模块模版工程的examples中的count例子

```bash
./bootstrap.sh run Test
```

> **NOTE:** 正式运行项目需要自己修改bootstrap，添加启动/停止函数

