---
title: "Java HBase 클라이언트 - Azure HDInsight | Microsoft Docs"
description: "Apache Maven을 사용하여 Java 기반 Apache HBase 응용 프로그램을 빌드한 다음 Azure HDInsight의 HBase에 배포하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: 
ms.assetid: 1d1ed180-e0f4-4d1c-b5ea-72e0eda643bc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 03c88397e36c0fc7f19410e49f6b6f1a607659f8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="build-java-applications-for-apache-hbase"></a><span data-ttu-id="3e26c-103">Apache HBase에 대한 Java 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="3e26c-103">Build Java applications for Apache HBase</span></span>

<span data-ttu-id="3e26c-104">Java에서 [Apache HBase](http://hbase.apache.org/) 응용 프로그램을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-104">Learn how to create an [Apache HBase](http://hbase.apache.org/) application in Java.</span></span> <span data-ttu-id="3e26c-105">그런 다음 Azure HDInsight의 HBase에서 응용 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-105">Then use the application with HBase on Azure HDInsight.</span></span>

<span data-ttu-id="3e26c-106">이 문서에 나온 단계는 [Maven](http://maven.apache.org/)을 사용하여 프로젝트를 만들고 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-106">The steps in this document use [Maven](http://maven.apache.org/) to create and build the project.</span></span> <span data-ttu-id="3e26c-107">Maven은 Java 프로젝트용 소프트웨어, 문서화 및 보고를 빌드할 수 있는 소프트웨어 프로젝트 관리 및 종합 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-107">Maven is a software project management and comprehension tool that allows you to build software, documentation, and reports for Java projects.</span></span>

> [!NOTE]
> <span data-ttu-id="3e26c-108">이 문서의 단계는 HDInsight 3.6에서 가장 최근에 테스트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-108">The steps in this document were most recently tested with HDInsight 3.6.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e26c-109">이 문서의 단계에는 Linux를 사용하는 HDInsight 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-109">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="3e26c-110">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3e26c-111">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e26c-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="3e26c-112">요구 사항</span><span class="sxs-lookup"><span data-stu-id="3e26c-112">Requirements</span></span>

* <span data-ttu-id="3e26c-113">[Java 플랫폼 JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 이상.</span><span class="sxs-lookup"><span data-stu-id="3e26c-113">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 or later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3e26c-114">HDInsight 3.5 이상에는 Java 8이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-114">HDInsight 3.5 and greater requires Java 8.</span></span> <span data-ttu-id="3e26c-115">이전 버전의 HDInsight를 사용하려면 Java 7이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-115">Earlier versions of HDInsight require Java 7.</span></span>

* [<span data-ttu-id="3e26c-116">Maven</span><span class="sxs-lookup"><span data-stu-id="3e26c-116">Maven</span></span>](http://maven.apache.org/)

* [<span data-ttu-id="3e26c-117">Linux 기반 Azure HDInsight 클러스터 및 HBase</span><span class="sxs-lookup"><span data-stu-id="3e26c-117">A Linux-based Azure HDInsight cluster with HBase</span></span>](hdinsight-hbase-tutorial-get-started-linux.md#create-hbase-cluster)

  > [!NOTE]
  > <span data-ttu-id="3e26c-118">이 문서의 단계는 HDInsight 클러스터 버전 3.4 및 3.5에서 테스트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-118">The steps in this document have been tested with HDInsight cluster versions 3.4 and 3.5.</span></span> <span data-ttu-id="3e26c-119">예제에 제공되는 기본값은 HDInsight 3.5 클러스터에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-119">The default values provided in examples are for a HDInsight 3.5 cluster.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="3e26c-120">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="3e26c-120">Create the project</span></span>

1. <span data-ttu-id="3e26c-121">개발 환경의 명령줄에서 프로젝트를 만들 위치(예: `cd code\hbase`)로 디렉터리를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-121">From the command line in your development environment, change directories to the location where you want to create the project, for example, `cd code\hbase`.</span></span>

2. <span data-ttu-id="3e26c-122">Maven과 함께 설치되는 **mvn** 명령을 사용하여 프로젝트용 스캐폴딩을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-122">Use the **mvn** command, which is installed with Maven, to generate the scaffolding for the project.</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

    > [!NOTE]
    > <span data-ttu-id="3e26c-123">PowerShell을 사용하는 경우 큰 따옴표로 `-D` 매개 변수를 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-123">If you are using PowerShell, you must enclose the `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=hbaseapp" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="3e26c-124">이 명령은 **artifactID** 매개 변수와 동일한 이름으로 디렉터리를 만듭니다(이 예제에서는 **hbaseapp**). 이 디렉터리에는 다음과 같은 항목이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-124">This command creates a directory with the same name as the **artifactID** parameter (**hbaseapp** in this example.) This directory contains the following items:</span></span>

   * <span data-ttu-id="3e26c-125">**pom.xml**: [프로젝트 개체 모델(POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)은 프로젝트를 빌드하는 데 사용된 정보 및 구성 세부 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-125">**pom.xml**:  The Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used to build the project.</span></span>
   * <span data-ttu-id="3e26c-126">**src**: **main/java/com/microsoft/examples** 디렉터리를 포함하는 디렉터리이며 여기서 응용 프로그램을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-126">**src**: The directory that contains the **main/java/com/microsoft/examples** directory, where you author the application.</span></span>

3. <span data-ttu-id="3e26c-127">`src/test/java/com/microsoft/examples/apptest.java` 파일을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-127">Delete the `src/test/java/com/microsoft/examples/apptest.java` file.</span></span> <span data-ttu-id="3e26c-128">이 예제에서는 사용되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-128">It is not be used in this example.</span></span>

## <a name="update-the-project-object-model"></a><span data-ttu-id="3e26c-129">프로젝트 개체 모델 업데이트</span><span class="sxs-lookup"><span data-stu-id="3e26c-129">Update the Project Object Model</span></span>

1. <span data-ttu-id="3e26c-130">`pom.xml` 파일을 편집하고 다음 코드를 `<dependencies>` 섹션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-130">Edit the `pom.xml` file and add the following code inside the `<dependencies>` section:</span></span>

   ```xml
    <dependency>
        <groupId>org.apache.hbase</groupId>
        <artifactId>hbase-client</artifactId>
        <version>1.1.2</version>
    </dependency>
    <dependency>
        <groupId>org.apache.phoenix</groupId>
        <artifactId>phoenix-core</artifactId>
        <version>4.4.0-HBase-1.1</version>
    </dependency>
   ```

    <span data-ttu-id="3e26c-131">이 섹션에서는 프로젝트에 **hbase-client** 및 **phoenix-core** 구성 요소가 필요하다는 점을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-131">This section indicates that the project needs **hbase-client** and **phoenix-core** components.</span></span> <span data-ttu-id="3e26c-132">컴파일 시 이러한 종속성이 기본 Maven 리포지토리에서 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-132">At compile time, these dependencies are downloaded from the default Maven repository.</span></span> <span data-ttu-id="3e26c-133">[Maven 중앙 리포지토리 검색](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar)을 사용하여 이 종속성에 대한 자세한 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-133">You can use the [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) to learn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="3e26c-134">hbase-client의 버전 번호는 HDInsight 클러스터와 함께 제공되는 HBase 버전과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-134">The version number of the hbase-client must match the version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="3e26c-135">다음 표를 사용하여 올바른 버전 번호를 찾으세요.</span><span class="sxs-lookup"><span data-stu-id="3e26c-135">Use the following table to find the correct version number.</span></span>

   | <span data-ttu-id="3e26c-136">HDInsight 클러스터 버전</span><span class="sxs-lookup"><span data-stu-id="3e26c-136">HDInsight cluster version</span></span> | <span data-ttu-id="3e26c-137">사용할 HBase 버전</span><span class="sxs-lookup"><span data-stu-id="3e26c-137">HBase version to use</span></span> |
   | --- | --- |
   | <span data-ttu-id="3e26c-138">3.2</span><span class="sxs-lookup"><span data-stu-id="3e26c-138">3.2</span></span> |<span data-ttu-id="3e26c-139">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="3e26c-139">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="3e26c-140">3.3, 3.4, 3.5 및 3.6</span><span class="sxs-lookup"><span data-stu-id="3e26c-140">3.3, 3.4, 3.5, and 3.6</span></span> |<span data-ttu-id="3e26c-141">1.1.2</span><span class="sxs-lookup"><span data-stu-id="3e26c-141">1.1.2</span></span> |

    <span data-ttu-id="3e26c-142">HDInsight 버전 및 구성 요소에 대한 자세한 내용은 [HDInsight에서 사용할 수 있는 다양한 Hadoop 구성 요소](hdinsight-component-versioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e26c-142">For more information on HDInsight versions and components, see [What are the different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>

3. <span data-ttu-id="3e26c-143">**pom.xml** 파일에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-143">Add the following code to the **pom.xml** file.</span></span> <span data-ttu-id="3e26c-144">이 텍스트는 파일의 `<project>...</project>` 태그 내에 있어야 합니다. 예를 들어 `</dependencies>`와 `</project>` 사이에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-144">This text must be inside the `<project>...</project>` tags in the file, for example, between `</dependencies>` and `</project>`.</span></span>

   ```xml
    <build>
        <sourceDirectory>src</sourceDirectory>
        <resources>
        <resource>
            <directory>${basedir}/conf</directory>
            <filtering>false</filtering>
            <includes>
            <include>hbase-site.xml</include>
            </includes>
        </resource>
        </resources>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
                    <version>3.3</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
            </configuration>
            </plugin>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
            <transformers>
                <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                </transformer>
            </transformers>
            </configuration>
            <executions>
            <execution>
                <phase>package</phase>
                <goals>
                <goal>shade</goal>
                </goals>
            </execution>
            </executions>
        </plugin>
        </plugins>
    </build>
   ```

    <span data-ttu-id="3e26c-145">이 섹션은 HBase에 대한 구성 정보를 포함하는 리소스(`conf/hbase-site.xml`)를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-145">This section configures a resource (`conf/hbase-site.xml`) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3e26c-146">또한 코드를 통해 구성 값을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-146">You can also set configuration values via code.</span></span> <span data-ttu-id="3e26c-147">`CreateTable` 예제에서 주석을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e26c-147">See the comments in the `CreateTable` example.</span></span>

    <span data-ttu-id="3e26c-148">또한 이 섹션에서는 [Maven 컴파일러 플러그 인](http://maven.apache.org/plugins/maven-compiler-plugin/) 및 [Maven 음영 플러그 인](http://maven.apache.org/plugins/maven-shade-plugin/)도 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-148">This section also configures the [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="3e26c-149">컴파일러 플러그 인은 토폴로지를 컴파일하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-149">The compiler plug-in is used to compile the topology.</span></span> <span data-ttu-id="3e26c-150">음영 플러그 인은 Maven으로 빌드된 JAR 패키지에서 라이선스 중복을 방지하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-150">The shade plug-in is used to prevent license duplication in the JAR package that is built by Maven.</span></span> <span data-ttu-id="3e26c-151">이 플러그 인은 HDInsight 클러스터에서 런타임에 "중복 라이선스 파일" 오류가 발생하지 않도록 하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-151">This plugin is used to prevent a "duplicate license files" error at run time on the HDInsight cluster.</span></span> <span data-ttu-id="3e26c-152">`ApacheLicenseResourceTransformer` 구현에서 maven-shade-plugin을 사용하면 이 오류가 방지됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-152">Using maven-shade-plugin with the `ApacheLicenseResourceTransformer` implementation prevents the error.</span></span>

    <span data-ttu-id="3e26c-153">또한 maven-shade-plugin은 응용 프로그램에 필요한 모든 종속성을 포함하는 uber jar도 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-153">The maven-shade-plugin also produces an uber jar that contains all the dependencies required by the application.</span></span>

4. <span data-ttu-id="3e26c-154">`pom.xml` 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-154">Save the `pom.xml` file.</span></span>

5. <span data-ttu-id="3e26c-155">`hbaseapp` 디렉터리에 `conf`라는 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-155">Create a directory named `conf` in the `hbaseapp` directory.</span></span> <span data-ttu-id="3e26c-156">이 디렉터리는 HBase에 연결하기 위한 구성 정보를 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-156">This directory is used to hold configuration information for connecting to HBase.</span></span>

6. <span data-ttu-id="3e26c-157">다음 명령을 사용하여 HBase 클러스터에서 `conf` 디렉터리로 HBase 구성을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-157">Use the following command to copy the HBase configuration from the HBase cluster to the `conf` directory.</span></span> <span data-ttu-id="3e26c-158">`USERNAME`을 SSH 로그인 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-158">Replace `USERNAME` with the name of your SSH login.</span></span> <span data-ttu-id="3e26c-159">`CLUSTERNAME`을 HDInsight 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-159">Replace `CLUSTERNAME` with your HDInsight cluster name:</span></span>

    ```bash
    scp USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml
    ```

   <span data-ttu-id="3e26c-160">`ssh` 및 `scp` 사용에 관한 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e26c-160">For more information on using `ssh` and `scp`, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-the-application"></a><span data-ttu-id="3e26c-161">응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="3e26c-161">Create the application</span></span>

1. <span data-ttu-id="3e26c-162">`hbaseapp/src/main/java/com/microsoft/examples` 디렉터리로 이동하여 app.java 파일 이름을 `CreateTable.java`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-162">Go to the `hbaseapp/src/main/java/com/microsoft/examples` directory and rename the app.java file to `CreateTable.java`.</span></span>

2. <span data-ttu-id="3e26c-163">`CreateTable.java` 파일을 열고 기존 콘텐츠를 다음 텍스트로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-163">Open the `CreateTable.java` file and replace the existing contents with the following text:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;
    import org.apache.hadoop.hbase.HTableDescriptor;
    import org.apache.hadoop.hbase.TableName;
    import org.apache.hadoop.hbase.HColumnDescriptor;
    import org.apache.hadoop.hbase.client.HTable;
    import org.apache.hadoop.hbase.client.Put;
    import org.apache.hadoop.hbase.util.Bytes;

    public class CreateTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Example of setting zookeeper values for HDInsight
        // in code instead of an hbase-site.xml file
        //
        // config.set("hbase.zookeeper.quorum",
        //            "zookeepernode0,zookeepernode1,zookeepernode2");
        //config.set("hbase.zookeeper.property.clientPort", "2181");
        //config.set("hbase.cluster.distributed", "true");
        //
        //NOTE: Actual zookeeper host names can be found using Ambari:
        //curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts"

        //Linux-based HDInsight clusters use /hbase-unsecure as the znode parent
        config.set("zookeeper.znode.parent","/hbase-unsecure");

        // create an admin object using the config
        HBaseAdmin admin = new HBaseAdmin(config);

        // create the table...
        HTableDescriptor tableDescriptor = new HTableDescriptor(TableName.valueOf("people"));
        // ... with two column families
        tableDescriptor.addFamily(new HColumnDescriptor("name"));
        tableDescriptor.addFamily(new HColumnDescriptor("contactinfo"));
        admin.createTable(tableDescriptor);

        // define some people
        String[][] people = {
            { "1", "Marcel", "Haddad", "marcel@fabrikam.com"},
            { "2", "Franklin", "Holtz", "franklin@contoso.com" },
            { "3", "Dwayne", "McKee", "dwayne@fabrikam.com" },
            { "4", "Rae", "Schroeder", "rae@contoso.com" },
            { "5", "Rosalie", "burton", "rosalie@fabrikam.com"},
            { "6", "Gabriela", "Ingram", "gabriela@contoso.com"} };

        HTable table = new HTable(config, "people");

        // Add each person to the table
        //   Use the `name` column family for the name
        //   Use the `contactinfo` column family for the email
        for (int i = 0; i< people.length; i++) {
            Put person = new Put(Bytes.toBytes(people[i][0]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("first"), Bytes.toBytes(people[i][1]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("last"), Bytes.toBytes(people[i][2]));
            person.add(Bytes.toBytes("contactinfo"), Bytes.toBytes("email"), Bytes.toBytes(people[i][3]));
            table.put(person);
        }
        // flush commits and close the table
        table.flushCommits();
        table.close();
        }
    }
   ```

    <span data-ttu-id="3e26c-164">이 코드는 **CreateTable** 클래스이며, **people**이라는 테이블을 만들고 미리 정의된 사용자로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-164">This code is the **CreateTable** class, which creates a table named **people** and populate it with some predefined users.</span></span>

3. <span data-ttu-id="3e26c-165">`CreateTable.java` 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-165">Save the `CreateTable.java` file.</span></span>

4. <span data-ttu-id="3e26c-166">`hbaseapp/src/main/java/com/microsoft/examples` 디렉터리에서 `SearchByEmail.java`라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-166">In the `hbaseapp/src/main/java/com/microsoft/examples` directory, create a file named `SearchByEmail.java`.</span></span> <span data-ttu-id="3e26c-167">이 파일의 내용으로 다음 텍스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-167">Use the following text as the contents of this file:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HTable;
    import org.apache.hadoop.hbase.client.Scan;
    import org.apache.hadoop.hbase.client.ResultScanner;
    import org.apache.hadoop.hbase.client.Result;
    import org.apache.hadoop.hbase.filter.RegexStringComparator;
    import org.apache.hadoop.hbase.filter.SingleColumnValueFilter;
    import org.apache.hadoop.hbase.filter.CompareFilter.CompareOp;
    import org.apache.hadoop.hbase.util.Bytes;
    import org.apache.hadoop.util.GenericOptionsParser;

    public class SearchByEmail {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Use GenericOptionsParser to get only the parameters to the class
        // and not all the parameters passed (when using WebHCat for example)
        String[] otherArgs = new GenericOptionsParser(config, args).getRemainingArgs();
        if (otherArgs.length != 1) {
            System.out.println("usage: [regular expression]");
            System.exit(-1);
        }

        // Open the table
        HTable table = new HTable(config, "people");

        // Define the family and qualifiers to be used
        byte[] contactFamily = Bytes.toBytes("contactinfo");
        byte[] emailQualifier = Bytes.toBytes("email");
        byte[] nameFamily = Bytes.toBytes("name");
        byte[] firstNameQualifier = Bytes.toBytes("first");
        byte[] lastNameQualifier = Bytes.toBytes("last");

        // Create a regex filter
        RegexStringComparator emailFilter = new RegexStringComparator(otherArgs[0]);
        // Attach the regex filter to a filter
        //   for the email column
        SingleColumnValueFilter filter = new SingleColumnValueFilter(
            contactFamily,
            emailQualifier,
            CompareOp.EQUAL,
            emailFilter
        );

        // Create a scan and set the filter
        Scan scan = new Scan();
        scan.setFilter(filter);

        // Get the results
        ResultScanner results = table.getScanner(scan);
        // Iterate over results and print  values
        for (Result result : results ) {
            String id = new String(result.getRow());
            byte[] firstNameObj = result.getValue(nameFamily, firstNameQualifier);
            String firstName = new String(firstNameObj);
            byte[] lastNameObj = result.getValue(nameFamily, lastNameQualifier);
            String lastName = new String(lastNameObj);
            System.out.println(firstName + " " + lastName + " - ID: " + id);
            byte[] emailObj = result.getValue(contactFamily, emailQualifier);
            String email = new String(emailObj);
            System.out.println(firstName + " " + lastName + " - " + email + " - ID: " + id);
        }
        results.close();
        table.close();
        }
    }
   ```

    <span data-ttu-id="3e26c-168">**SearchByEmail** 클래스를 사용하여 메일 주소로 행을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-168">The **SearchByEmail** class can be used to query for rows by email address.</span></span> <span data-ttu-id="3e26c-169">정규식 필터를 사용하므로, 이 클래스를 사용할 때 문자열 또는 정규식을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-169">Because it uses a regular expression filter, you can provide either a string or a regular expression when using the class.</span></span>

5. <span data-ttu-id="3e26c-170">`SearchByEmail.java` 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-170">Save the `SearchByEmail.java` file.</span></span>

6. <span data-ttu-id="3e26c-171">`hbaseapp/src/main/hava/com/microsoft/examples` 디렉터리에서 `DeleteTable.java`라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-171">In the `hbaseapp/src/main/hava/com/microsoft/examples` directory, create a file named `DeleteTable.java`.</span></span> <span data-ttu-id="3e26c-172">이 파일의 내용으로 다음 텍스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-172">Use the following text as the contents of this file:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;

    public class DeleteTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Create an admin object using the config
        HBaseAdmin admin = new HBaseAdmin(config);

        // Disable, and then delete the table
        admin.disableTable("people");
        admin.deleteTable("people");
        }
    }
   ```

    <span data-ttu-id="3e26c-173">이 클래스는 `CreateTable` 클래스에서 생성된 테이블을 비활성화하고 제거하여 이 예제에서 만든 HBase 테이블을 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-173">This class cleans up the HBase tables created in this example by disabling and dropping the table created by the `CreateTable` class.</span></span>

7. <span data-ttu-id="3e26c-174">`DeleteTable.java` 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-174">Save the `DeleteTable.java` file.</span></span>

## <a name="build-and-package-the-application"></a><span data-ttu-id="3e26c-175">응용 프로그램 빌드 및 패키지화</span><span class="sxs-lookup"><span data-stu-id="3e26c-175">Build and package the application</span></span>

1. <span data-ttu-id="3e26c-176">`hbaseapp` 디렉터리에서 다음 명령을 사용하여 응용 프로그램을 포함하는 JAR 파일을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-176">From the `hbaseapp` directory, use the following command to build a JAR file that contains the application:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="3e26c-177">이 명령은 .jar 파일에 응용 프로그램을 빌드하고 패키지합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-177">This command builds and packages the application into a .jar file.</span></span>

2. <span data-ttu-id="3e26c-178">명령이 완료되면 `hbaseapp/target` 디렉터리는 `hbaseapp-1.0-SNAPSHOT.jar`라는 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-178">When the command completes, the `hbaseapp/target` directory contains a file named `hbaseapp-1.0-SNAPSHOT.jar`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3e26c-179">`hbaseapp-1.0-SNAPSHOT.jar` 파일은 uber jar입니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-179">The `hbaseapp-1.0-SNAPSHOT.jar` file is an uber jar.</span></span> <span data-ttu-id="3e26c-180">응용 프로그램을 실행 는 데 필요한 모든 종속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-180">It contains all the dependencies required to run the application.</span></span>


## <a name="upload-the-jar-and-run-jobs-ssh"></a><span data-ttu-id="3e26c-181">JAR 업로드 및 작업 실행(SSH)</span><span class="sxs-lookup"><span data-stu-id="3e26c-181">Upload the JAR and run jobs (SSH)</span></span>

<span data-ttu-id="3e26c-182">다음 단계에서는 `scp`를 사용하여 HDInsight 클러스터에 있는 HBase의 기본 헤드 노드에 JAR을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-182">The following steps use `scp` to copy the JAR to the primary head node of your HBase on HDInsight cluster.</span></span> <span data-ttu-id="3e26c-183">그런 후 `ssh` 명령은 클러스터에 연결하고 헤드 노드에서 직접 예제를 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-183">The `ssh` command is then used to connect to the cluster and run the example directly on the head node.</span></span>

1. <span data-ttu-id="3e26c-184">jar을 클러스터에 업로드하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-184">To upload the jar to the cluster, use the following command:</span></span>

    ```bash
    scp ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="3e26c-185">`USERNAME`을 SSH 로그인 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-185">Replace `USERNAME` with the name of your SSH login.</span></span> <span data-ttu-id="3e26c-186">`CLUSTERNAME`을 HDInsight 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-186">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

2. <span data-ttu-id="3e26c-187">HBase 클러스터에 연결하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-187">To connect to the HBase cluster, use the following command:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="3e26c-188">`USERNAME`을 SSH 로그인 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-188">Replace `USERNAME` the name of your SSH login.</span></span> <span data-ttu-id="3e26c-189">`CLUSTERNAME`을 HDInsight 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-189">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

3. <span data-ttu-id="3e26c-190">Java 응용 프로그램을 사용하는 HBase 테이블을 만들려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-190">To create an HBase table using the Java application, use the following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.CreateTable
    ```

    <span data-ttu-id="3e26c-191">이 명령은 **people**이라는 HBase 테이블을 만들고 데이터로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-191">This command creates a HBase table named **people**, and populates it with data.</span></span>

4. <span data-ttu-id="3e26c-192">테이블에 저장된 이메일 주소를 검색하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-192">To search for email addresses stored in the table, use the following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.SearchByEmail contoso.com
    ```

    <span data-ttu-id="3e26c-193">다음과 같은 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-193">You receive the following results:</span></span>

        Franklin Holtz - ID: 2
        Franklin Holtz - franklin@contoso.com - ID: 2
        Rae Schroeder - ID: 4
        Rae Schroeder - rae@contoso.com - ID: 4
        Gabriela Ingram - ID: 6
        Gabriela Ingram - gabriela@contoso.com - ID: 6

5. <span data-ttu-id="3e26c-194">테이블을 삭제하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-194">To delete the table, use the following command:</span></span>

    

## <a name="upload-the-jar-and-run-jobs-powershell"></a><span data-ttu-id="3e26c-195">JAR 업로드 및 작업 실행(PowerShell)</span><span class="sxs-lookup"><span data-stu-id="3e26c-195">Upload the JAR and run jobs (PowerShell)</span></span>

<span data-ttu-id="3e26c-196">다음 단계는 Azure PowerShell을 사용하여 HBase 클러스터용 기본 저장소에 JAR을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-196">The following steps use Azure PowerShell to upload the JAR to the default storage for your HBase cluster.</span></span> <span data-ttu-id="3e26c-197">HDInsight cmdlet은 예제를 원격으로 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-197">HDInsight cmdlets are then used to run the examples remotely.</span></span>

1. <span data-ttu-id="3e26c-198">Azure PowerShell을 설치 및 구성한 후 `hbase-runner.psm1`이라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-198">After installing and configuring Azure PowerShell, create a file named `hbase-runner.psm1`.</span></span> <span data-ttu-id="3e26c-199">이 파일의 내용으로 다음 텍스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-199">Use the following text as the contents of this file:</span></span>

   ```powershell
    <#
    .SYNOPSIS
    Copies a file to the primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory to the blob container for
    the HDInsight cluster.
    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.CreateTable"
    -clusterName "MyHDInsightCluster"

    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
    -clusterName "MyHDInsightCluster"
    -emailRegex "contoso.com"

    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
    -clusterName "MyHDInsightCluster"
    -emailRegex "^r" -showErr
    #>

    function Start-HBaseExample {
    [CmdletBinding(SupportsShouldProcess = $true)]
    param(
    #The class to run
    [Parameter(Mandatory = $true)]
    [String]$className,

    #The name of the HDInsight cluster
    [Parameter(Mandatory = $true)]
    [String]$clusterName,

    #Only used when using SearchByEmail
    [Parameter(Mandatory = $false)]
    [String]$emailRegex,

    #Use if you want to see stderr output
    [Parameter(Mandatory = $false)]
    [Switch]$showErr
    )

    Set-StrictMode -Version 3

    # Is the Azure module installed?
    FindAzure

    # Get the login for the HDInsight cluster
    $creds=Get-Credential -Message "Enter the login for the cluster" -UserName "admin"

    # The JAR
    $jarFile = "wasb:///example/jars/hbaseapp-1.0-SNAPSHOT.jar"

    # The job definition
    $jobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
        -JarFile $jarFile `
        -ClassName $className `
        -Arguments $emailRegex

    # Get the job output
    $job = Start-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobDefinition $jobDefinition `
        -HttpCredential $creds
    Write-Host "Wait for the job to complete ..." -ForegroundColor Green
    Wait-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds
    if($showErr)
    {
    Write-Host "STDERR"
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds `
                -DisplayOutputType StandardError
    }
    Write-Host "Display the standard output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds
    }

    <#
    .SYNOPSIS
    Copies a file to the primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory to the blob container for
    the HDInsight cluster.
    .EXAMPLE
    Add-HDInsightFile -localPath "C:\temp\data.txt"
    -destinationPath "example/data/data.txt"
    -ClusterName "MyHDInsightCluster"
    .EXAMPLE
    Add-HDInsightFile -localPath "C:\temp\data.txt"
    -destinationPath "example/data/data.txt"
    -ClusterName "MyHDInsightCluster"
    -Container "MyContainer"
    #>

    function Add-HDInsightFile {
        [CmdletBinding(SupportsShouldProcess = $true)]
        param(
            #The path to the local file.
            [Parameter(Mandatory = $true)]
            [String]$localPath,

            #The destination path and file name, relative to the root of the container.
            [Parameter(Mandatory = $true)]
            [String]$destinationPath,

            #The name of the HDInsight cluster
            [Parameter(Mandatory = $true)]
            [String]$clusterName,

            #If specified, overwrites existing files without prompting
            [Parameter(Mandatory = $false)]
            [Switch]$force
        )

        Set-StrictMode -Version 3

        # Is the Azure module installed?
        FindAzure

        # Get authentication for the cluster
        $creds=Get-Credential

        # Does the local path exist?
        if (-not (Test-Path $localPath))
        {
            throw "Source path '$localPath' does not exist."
        }

        # Get the primary storage container
        $storage = GetStorage -clusterName $clusterName

        # Upload file to storage, overwriting existing files if -force was used.
        Set-AzureStorageBlobContent -File $localPath `
            -Blob $destinationPath `
            -force:$force `
            -Container $storage.container `
            -Context $storage.context
    }

    function FindAzure {
        # Is there an active Azure subscription?
        $sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
        if(-not($sub))
        {
            throw "No active Azure subscription found! If you have a subscription, use the Login-AzureRmAccount cmdlet to login to your subscription."
        }
    }

    function GetStorage {
        param(
            [Parameter(Mandatory = $true)]
            [String]$clusterName
        )
        $hdi = Get-AzureRmHDInsightCluster -ClusterName $clusterName
        # Does the cluster exist?
        if (!$hdi)
        {
            throw "HDInsight cluster '$clusterName' does not exist."
        }
        # Create a return object for context & container
        $return = @{}
        $storageAccounts = @{}

        # Get storage information
        $resourceGroup = $hdi.ResourceGroup
        $storageAccountName=$hdi.DefaultStorageAccount.split('.')[0]
        $container=$hdi.DefaultStorageContainer
        $storageAccountKey=(Get-AzureRmStorageAccountKey `
            -Name $storageAccountName `
        -ResourceGroupName $resourceGroup)[0].Value
        # Get the resource group, in case we need that
        $return.resourceGroup = $resourceGroup
        # Get the storage context, as we can't depend
        # on using the default storage context
        $return.context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        # Get the container, so we know where to
        # find/store blobs
        $return.container = $container
        # Return storage accounts to support finding all accounts for
        # a cluster
        $return.storageAccount = $storageAccountName
        $return.storageAccountKey = $storageAccountKey

        return $return
    }
    # Only export the verb-phrase things
    export-modulemember *-*
   ```

    <span data-ttu-id="3e26c-200">이 파일에는 다음 두 모듈이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-200">This file contains two modules:</span></span>

   * <span data-ttu-id="3e26c-201">**Add-HDInsightFile** - 클러스터에 파일을 업로드하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-201">**Add-HDInsightFile** - used to upload files to the cluster</span></span>
   * <span data-ttu-id="3e26c-202">**Start-HBaseExample** - 이전에 생성한 클래스를 실행하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-202">**Start-HBaseExample** - used to run the classes created earlier</span></span>

2. <span data-ttu-id="3e26c-203">`hbase-runner.psm1` 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-203">Save the `hbase-runner.psm1` file.</span></span>

3. <span data-ttu-id="3e26c-204">새 Azure PowerShell 창을 열고, 디렉터리를 `hbaseapp` 디렉터리로 변경한 후 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-204">Open a new Azure PowerShell window, change directories to the `hbaseapp` directory, and then run the following command:</span></span>

    ```powershell
    PS C:\ Import-Module c:\path\to\hbase-runner.psm1
    ```

    <span data-ttu-id="3e26c-205">이전에 만든 `hbase-runner.psm1` 파일의 위치로 경로를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-205">Change the path to the location of the `hbase-runner.psm1` file created earlier.</span></span> <span data-ttu-id="3e26c-206">이 명령은 Azure PowerShell에 모듈을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-206">This command registers the module with Azure PowerShell.</span></span>

4. <span data-ttu-id="3e26c-207">다음 명령을 사용하여 클러스터에 `hbaseapp-1.0-SNAPSHOT.jar`을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-207">Use the following command to upload the `hbaseapp-1.0-SNAPSHOT.jar` to your cluster.</span></span>

    ```powershell
    Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername
    ```

    <span data-ttu-id="3e26c-208">`hdinsightclustername`을 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-208">Replace `hdinsightclustername` with the name of your cluster.</span></span> <span data-ttu-id="3e26c-209">이 명령은 `hbaseapp-1.0-SNAPSHOT.jar`을 클러스터용 기본 저장소에서 `example/jars` 위치에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-209">The command uploads the `hbaseapp-1.0-SNAPSHOT.jar` to the `example/jars` location in the primary storage for your cluster.</span></span>

5. <span data-ttu-id="3e26c-210">`hbaseapp`을 사용하는 테이블을 만들려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-210">To create a table using the `hbaseapp`, use the following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername
    ```

    <span data-ttu-id="3e26c-211">`hdinsightclustername`을 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-211">Replace `hdinsightclustername` with the name of your cluster.</span></span>

    <span data-ttu-id="3e26c-212">이 명령은 HDInsight 클러스터에 HBase의 **people**이라는 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-212">This command creates a table named **people** in HBase on your HDInsight cluster.</span></span> <span data-ttu-id="3e26c-213">이 명령은 콘솔 창에 출력을 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-213">This command does not show any output in the console window.</span></span>

6. <span data-ttu-id="3e26c-214">테이블에서 항목을 검색하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-214">To search for entries in the table, use the following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com
    ```

    <span data-ttu-id="3e26c-215">`hdinsightclustername`을 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-215">Replace `hdinsightclustername` with the name of your cluster.</span></span>

    <span data-ttu-id="3e26c-216">이 명령은 `SearchByEmail` 클래스를 사용하여 `contactinformation` 열 패밀리 및 `email` 열에 `contoso.com` 문자열이 포함된 모든 행을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-216">This command uses the `SearchByEmail` class to search for any rows where the `contactinformation` column family and the `email` column, contains the string `contoso.com`.</span></span> <span data-ttu-id="3e26c-217">다음과 같은 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-217">You should receive the following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="3e26c-218">`-emailRegex` 값에 **fabrikam.com**을 사용하면 메일 필드에 **fabrikam.com**을 포함하는 사용자가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-218">Using **fabrikam.com** for the `-emailRegex` value returns the users that have **fabrikam.com** in the email field.</span></span> <span data-ttu-id="3e26c-219">검색 용어로 정규식을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-219">You can also use regular expressions as the search term.</span></span> <span data-ttu-id="3e26c-220">예를 들어, **^r**은 'r' 문자로 시작하는 전자 메일 주소를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-220">For example, **^r** returns email addresses that begin with the letter 'r'.</span></span>

### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="3e26c-221">Start-HBaseExample을 사용할 경우 결과가 없거나 예기치 않은 결과가 표시됨</span><span class="sxs-lookup"><span data-stu-id="3e26c-221">No results or unexpected results when using Start-HBaseExample</span></span>

<span data-ttu-id="3e26c-222">`-showErr` 매개 변수를 사용하여 작업을 실행하는 동안 생성된 표준 오류(STDERR)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-222">Use the `-showErr` parameter to view the standard error (STDERR) that is produced while running the job.</span></span>

## <a name="delete-the-table"></a><span data-ttu-id="3e26c-223">테이블 삭제</span><span class="sxs-lookup"><span data-stu-id="3e26c-223">Delete the table</span></span>

<span data-ttu-id="3e26c-224">예제를 완료하면 Azure PowerShell 세션에서 다음을 사용하여 이 예제에 사용된 **people** 테이블을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26c-224">When you are done with the example, use the following to delete the **people** table used in this example:</span></span>

<span data-ttu-id="3e26c-225">__`ssh` 세션에서__:</span><span class="sxs-lookup"><span data-stu-id="3e26c-225">__From an `ssh` session__:</span></span>

`yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.DeleteTable`

<span data-ttu-id="3e26c-226">__Azure PowerShell에서__:</span><span class="sxs-lookup"><span data-stu-id="3e26c-226">__From Azure PowerShell__:</span></span>

`Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername`

## <a name="next-steps"></a><span data-ttu-id="3e26c-227">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3e26c-227">Next steps</span></span>

[<span data-ttu-id="3e26c-228">HBase를 통해 SQuirreL SQL 사용 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="3e26c-228">Learn how to use SQuirreL SQL with HBase</span></span>](hdinsight-hbase-phoenix-squirrel-linux.md)
