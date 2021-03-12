# phoebus
<<<<<<< HEAD
=======
![GitHub Actions Status](https://github.com/ControlSystemStudio/phoebus/actions/workflows/build.yml/badge.svg)
>>>>>>> 8419f2b04be78fd2a0fc775148c4dcf294c0c58e

[![Build Status](https://travis-ci.com/haitao127/phoebus.svg?branch=master)](https://travis-ci.com/haitao127/phoebus)

Phoebus 是一个框架和一系列工具，用于监视和操作大型控制系统，例如加速器社区中的系统。 Phoebus 是 Control System Studio 工具集的更新，它删除了对 Eclipse RCP 和 SWT 的依赖。

详细信息：[https://phoebus-impics.readthedocs.io](https://phoebus-impics.readthedocs.io)

## 要求

-   [JDK11 或更高版本，建议使用 OpenJDK](http://jdk.java.net/12) 。
-   [Maven 2.x](https://maven.apache.org/) 或 [ant](http://ant.apache.org/)

## 目标平台

所有外部依赖项都应在 `dependencies/target/lib` 。可以通过从现有的构建设置扩展一个压缩的 Phoebus 目标来获得，也可以通过一个初步的 Maven 运行来获得它们：

```
mvn clean verify -f dependencies/pom.xml
```

## 使用Maven进行构建

定义JAVA_HOME环境变量，使其指向Java的安装目录。

Mac操作系统的用户应该使用如下所示的配置：
```
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk-11.0.5+10/Contents/Home
```
可以通过以下命令进行验证:
```
$JAVA_HOME/bin/java -version
```

请确保PATH环境变量包括了JAVA_HOME和Maven可执行程序的路径。

### 构建

构建整个 phoebus 堆栈

```
mvn clean install
```

### 单元测试

某些单元测试可能对本地化敏感，并且在以前未经测试的语言环境中执行时会失败。将环境变量 `LANG` 设置为 `en_US.UTF-8` 以在特定的语言环境中执行测试，或使用 `mvn -DskipTests ...` 进行构建以跳过测试。

### 运行 Phoebus 应用程序

运行jar程序：
```
cd phoebus-product/target
java -jar product-*-SNAPSHOT.jar
```

## 使用Ant进行构建

```
ant clean run
```

## 使用 Eclipse 开发

从 [http://download.eclipse.org/eclipse/downloads/](http://download.eclipse.org/eclipse/downloads/) 下载 Eclipse Oxygen 4.7.1a 或更高版本

像这样启动 Eclipse：

```
export JAVA_HOME=/path/to/your/jdk-9-or-later
export PATH="$JAVA_HOME/bin:$PATH"
eclipse/eclipse -consoleLog
```

检查 Eclipse 首选项：

-   Java，已安装的 JRE：默认为 JDK 9 或更高版本
-   Java，编译器：“JDK 符合性” 应为 “9” 或更高

### 使用简单的Java配置

使用文件-导入-常规-现有项目到工作区。 选择phoebus根目录，然后选中“搜索相关项目”选项。

默认情况下，应选择所有项目（“依赖项”，“核心框架”，……，“产品”）。

需要编辑文件 `dependencies/phoebus-target/.classpath` 列出所有 `phoebus-target/target/lib/javafx*.jar` 文件。

在包资源管理器中，选择 `product` 项目。从菜单中调用 `Run` ， `Run Configurations...` 在启动配置对话框中，选择 `Java Application` ，然后按 `New Configuration` 。请注意，该项目应预先设置为 `product` ，并且 Dependencies 选项卡应列出该产品的所有项目依赖项，即所有 `core-*` 和 `app-*` 项目。对于 Main 类，输入 `org.phoebus.product.Launcher` ，按 `Apply` ，然后按 `Run` 。

### 在 Eclipse 中使用 Maven 文件

在 “帮助 / Eclipse 市场” 中，搜索 “Maven Integration for Eclipse Luna 或更高版本”。

使用文件 / 导入 / Maven / 现有 Maven 项目导入 Phoebus 源代码。

可能存在编译器错误，因为程序包资源管理器中的 “JRE 系统库” 显示为 “\[J2SE-1.4\]”。右键单击受影响的项目（greeting-app，探针），“构建路径”，“配置构建路径”，“库”，“编辑 JRE 系统库” 以使用工作区默认值（jdk-9）。重新启动 Eclipse IDE。

现在可以启动 product /src/main /java/org.phoebus.product/ Launcher.java。

## 使用 Intellij IDEA 开发

首先，如上所述下载目标平台。

导入项目：

-   启动 Intellij
-   导入项目
-   选择 Phoebus 目录
-   从外部模型导入项目：Maven
-   接受默认选项，然后单击两次下一步。
-   确保 JDK 是版本 9 或更高版本
-   将项目名称更改为 Phoebus 并单击完成

要运行 Phoebus 应用程序：

-   运行编辑配置...
-   选择 + | 应用
-   搜索主类并键入 Launcher
-   使用模块的类路径：选择产品
-   将名称设置为 Phoebus
-   点击确定
-   在 IDE 的右上角，单击绿色的播放按钮

## 使用 NetBeans 开发

首先下载 [NetBeans 9](https://netbeans.apache.org/download/nb90/nb90.html) ，然后如上所述下载目标平台。运行 NetBeans 之后，选择 “ **工具** ➜Java **平台”** ，并确保将 Java 9 或 10 平台设置为默认平台。

要打开 Maven 项目，请选择 **File** **…Open Project…，** 然后选择 *phoebus* 根项目文件夹。

在 “ **项目”** 视图上，右键单击 “*phoebus（父级）”* 节点，然后选择 “ **清理并构建”** 菜单项。要在没有单元测试的情况下进行构建，请右键单击 *phoebus（父级）* 节点，然后选择 **“运行** *Maven➜* **跳过测试”** 。

要运行 Phoebus 应用程序：

-   打开 *phoebus（父级）* 项目和 “ *模块”* 节点，然后双击 *产品* 模块。
-   现在，右键单击打开的 *产品* 项目，然后选择 *“运行”* ；
-   将打开一个对话框，选择要运行的主类。验证是否已选择 `org.phoebus.product.Launcher` ，然后按 *Select Main Class* 按钮以启动应用程序。
-   您还可以选择 *“永久记住”，* 以允许 NetBeans 记住所选的类。
-   右键单击 *产品* 项目，还可以选择 *Set as Main Project* 。这样，只需按 *F6* 键，“ *运行主要项目”* 工具栏按钮或 “ *运行* ➜ *运行主要项目”* 菜单项即可启动 Phoebus 应用程序。

## 完整的分发，包括手动和自动更新

```
# Obtain sources
git clone https://github.com/ControlSystemStudio/phoebus.git

# Build the Javadoc, i.e. html files to be included in the manual
( cd phoebus/app/display/editor; ant -f javadoc.xml clean all )

# Building the manual will locate and include
# all ../phoebus/**/doc/index.rst and ../phoebus/**/doc/html
( cd phoebus/docs; make clean html )
# Windows: Use make.bat html

# Build Product

# Fetch dependencies
( cd phoebus; mvn clean verify -f dependencies/pom.xml )

# Create settings.ini for the product with current date
# and URL of your update site.
# Update site contains '$(arch)' which client will replace with
# its host OS (linux, mac, win).
# Note that this example replaces an existing product/settings.ini.
# If your product already contains settings.ini,
# consider using '>>' to append instead of replacing.
URL='https://controlssoftware.sns.ornl.gov/css_phoebus/nightly/phoebus-$(arch).zip'
( cd phoebus;
  app/update/mk_update_settings.sh $URL > phoebus-product/settings.ini
)

# Build product & bundle for distribution, including the documentation
( cd phoebus; ant clean dist )

# The files phoebus/phoebus-product/target/*.zip and
# services/*/target/*.zip can now be distributed,
# unzipped, launched
```

请注意，phoebus-product 取决于平台，您会根据构建平台获得 `phoebus-0.0.1-linux.zip` ， `phoebus-0.0.1-mac.zip` 或 `phoebus-0.0.1-win.zip` 。

## 跨平台构建

`dependencies` 包括与平台相关的 JavaFX 库，其针对 Linux，Mac 和 Windows 的内容不同。如上所述进行构建时，结果将是构建平台的可执行文件。要为其他平台进行构建，请通过以下方式之一创建 `dependencies` ：

```
# Either create the build platform for Linux..
( cd phoebus; mvn clean verify  -Djavafx.platform=linux  -f dependencies/pom.xml )

# or Mac OS X ..
( cd phoebus; mvn clean verify  -Djavafx.platform=mac    -f dependencies/pom.xml )

# or Windows:
( cd phoebus; mvn clean verify  -Djavafx.platform=win    -f dependencies/pom.xml )
```

其余构建是相同的，例如 `ant clean dist` 来构建发行版。

## 发布

有一个发布配置文件，可以帮助准备和部署 Phoebus 版本。

```
mvn -P release release:prepare
```

-   检查源中是否有未提交的更改
-   检查是否没有 SNAPSHOT 依赖项
-   将 POM 中的版本从 x-SNAPSHOT 更改为新版本（系统将提示您使用该版本）
-   在 POM 中转换 SCM 信息以包括标签的最终目的地
-   针对修改后的 POM 运行项目测试，以确认一切正常
-   提交修改后的 POM
-   用版本名称标记 SCM 中的代码（将提示输入）
-   将 POM 中的版本更改为新值 y-SNAPSHOT（还将提示输入这些值）
-   提交修改后的 POM

另外：

-   在提交更改之前，目标平台 `release_classpath.py` 有一个脚本将被执行。可以修改此脚本以更新.classpath 和其他在发行期间需要人工干预的文件。
