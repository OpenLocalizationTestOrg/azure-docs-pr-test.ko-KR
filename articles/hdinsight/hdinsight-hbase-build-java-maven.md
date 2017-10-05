---
title: "Windows 기반 Azure HDInsight용 Java HBase 응용 프로그램 빌드 | Microsoft Docs"
description: "Apache Maven을 사용하여 Java 기반 Apache HBase 응용 프로그램을 빌드한 다음 Windows 기반 Azure HDInsight 클러스터에 배포하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7f4a4e02-45ab-40dd-842b-3ec034f256c9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 59c9af5a91b107e68a676f02fe5a936f955b22fa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-maven-to-build-java-applications-that-use-hbase-with-windows-based-hdinsight-hadoop"></a><span data-ttu-id="063a7-103">Maven을 사용하여 Windows 기반 HDInsight(Hadoop)에서 HBase를 사용하는 Java 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="063a7-103">Use Maven to build Java applications that use HBase with Windows-based HDInsight (Hadoop)</span></span>
<span data-ttu-id="063a7-104">Apache Maven을 사용하여 Java로 [Apache HBase](http://hbase.apache.org/) 응용 프로그램을 만들어 빌드하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-104">Learn how to create and build an [Apache HBase](http://hbase.apache.org/) application in Java by using Apache Maven.</span></span> <span data-ttu-id="063a7-105">그런 다음 Azure HDInsight(Hadoop)에서 응용 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-105">Then use the application with Azure HDInsight (Hadoop).</span></span>

<span data-ttu-id="063a7-106">[Maven](http://maven.apache.org/) 은 Java 프로젝트용 소프트웨어, 문서화 및 보고를 빌드할 수 있는 소프트웨어 프로젝트 관리 및 종합 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-106">[Maven](http://maven.apache.org/) is a software project management and comprehension tool that allows you to build software, documentation, and reports for Java projects.</span></span> <span data-ttu-id="063a7-107">이 문서에서는 Maven을 사용하여 Azure HDInsight 클러스터에서 HBase 테이블을 만들고, 쿼리하고, 삭제하는 기본 Java 응용 프로그램을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-107">In this article, you learn how to use it to create a basic Java application that that creates, queries, and deletes an HBase table on an Azure HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="063a7-108">이 문서의 단계에는 Windows를 사용하는 HDInsight 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-108">The steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="063a7-109">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="063a7-110">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="063a7-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="063a7-111">요구 사항</span><span class="sxs-lookup"><span data-stu-id="063a7-111">Requirements</span></span>
* <span data-ttu-id="063a7-112">[Java 플랫폼 JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 이상</span><span class="sxs-lookup"><span data-stu-id="063a7-112">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 or later</span></span>
* [<span data-ttu-id="063a7-113">Maven</span><span class="sxs-lookup"><span data-stu-id="063a7-113">Maven</span></span>](http://maven.apache.org/)
* <span data-ttu-id="063a7-114">Windows 기반 HDInsight 클러스터 및 HBase</span><span class="sxs-lookup"><span data-stu-id="063a7-114">A Windows-based HDInsight cluster with HBase</span></span>

    > [!NOTE]
    > <span data-ttu-id="063a7-115">이 문서의 단계는 HDInsight 클러스터 버전 3.2 및 3.3으로 테스트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-115">The steps in this document have been tested with HDInsight cluster versions 3.2 and 3.3.</span></span> <span data-ttu-id="063a7-116">예제에 제공되는 기본값은 HDInsight 3.3 클러스터에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-116">The default values provided in examples are for a HDInsight 3.3 cluster.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="063a7-117">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="063a7-117">Create the project</span></span>
1. <span data-ttu-id="063a7-118">개발 환경의 명령줄에서 프로젝트를 만들 위치(예: `cd code\hdinsight`)로 디렉터리를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-118">From the command line in your development environment, change directories to the location where you want to create the project, for example, `cd code\hdinsight`.</span></span>
2. <span data-ttu-id="063a7-119">Maven과 함께 설치되는 **mvn** 명령을 사용하여 프로젝트용 스캐폴딩을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-119">Use the **mvn** command, which is installed with Maven, to generate the scaffolding for the project.</span></span>

        mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

    <span data-ttu-id="063a7-120">이 명령은 현재 위치에 디렉터리를 만들며, 이름은 **artifactID** 매개 변수로 지정됩니다(이 예제에서는 **hbaseapp**). 이 디렉터리에는 다음과 같은 항목이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-120">This command creates a directory in the current location, with the name specified by the **artifactID** parameter (**hbaseapp** in this example.) This directory contains the following items:</span></span>

   * <span data-ttu-id="063a7-121">**pom.xml**: [프로젝트 개체 모델(POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)은 프로젝트를 빌드하는 데 사용된 정보 및 구성 세부 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-121">**pom.xml**:  The Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used to build the project.</span></span>
   * <span data-ttu-id="063a7-122">**src**: **main\java\com\microsoft\examples** 디렉터리를 포함하는 디렉터리이며 여기서 응용 프로그램을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-122">**src**: The directory that contains the **main\java\com\microsoft\examples** directory, where you will author the application.</span></span>
3. <span data-ttu-id="063a7-123">**src\test\java\com\microsoft\examples\apptest.java** 파일은 이 예제에서 사용되지 않으므로 이 파일을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-123">Delete the **src\test\java\com\microsoft\examples\apptest.java** file because it is not used in this example.</span></span>

## <a name="update-the-project-object-model"></a><span data-ttu-id="063a7-124">프로젝트 개체 모델 업데이트</span><span class="sxs-lookup"><span data-stu-id="063a7-124">Update the Project Object Model</span></span>
1. <span data-ttu-id="063a7-125">**pom.xml** 파일을 편집하고 `<dependencies>` 섹션 안에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-125">Edit the **pom.xml** file and add the following code inside the `<dependencies>` section:</span></span>

        <dependency>
          <groupId>org.apache.hbase</groupId>
          <artifactId>hbase-client</artifactId>
          <version>1.1.2</version>
        </dependency>

    <span data-ttu-id="063a7-126">이 섹션을 통해 Maven은 프로젝트에 **hbase-client** 버전 **1.1.2**가 필요하다는 것을 인식합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-126">This section tells Maven that the project requires **hbase-client** version **1.1.2**.</span></span> <span data-ttu-id="063a7-127">컴파일 시간에 이 종속성이 기본 Maven 리포지토리에서 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-127">At compile time, this dependency is downloaded from the default Maven repository.</span></span> <span data-ttu-id="063a7-128">[Maven 중앙 리포지토리 검색](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) 을 사용하여 이 종속성에 대한 자세한 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-128">You can use the [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) to learn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="063a7-129">버전 번호는 HDInsight 클러스터와 함께 제공되는 HBase 버전과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-129">The version number must match the version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="063a7-130">다음 표를 사용하여 올바른 버전 번호를 찾으세요.</span><span class="sxs-lookup"><span data-stu-id="063a7-130">Use the following table to find the correct version number.</span></span>
   >
   >

   | <span data-ttu-id="063a7-131">HDInsight 클러스터 버전</span><span class="sxs-lookup"><span data-stu-id="063a7-131">HDInsight cluster version</span></span> | <span data-ttu-id="063a7-132">사용할 HBase 버전</span><span class="sxs-lookup"><span data-stu-id="063a7-132">HBase version to use</span></span> |
   | --- | --- |
   | <span data-ttu-id="063a7-133">3.2</span><span class="sxs-lookup"><span data-stu-id="063a7-133">3.2</span></span> |<span data-ttu-id="063a7-134">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="063a7-134">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="063a7-135">3.3</span><span class="sxs-lookup"><span data-stu-id="063a7-135">3.3</span></span> |<span data-ttu-id="063a7-136">1.1.2</span><span class="sxs-lookup"><span data-stu-id="063a7-136">1.1.2</span></span> |

    <span data-ttu-id="063a7-137">HDInsight 버전 및 구성 요소에 대한 자세한 내용은 [HDInsight에서 사용할 수 있는 다양한 Hadoop 구성 요소](hdinsight-component-versioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="063a7-137">For more information on HDInsight versions and components, see [What are the different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>
2. <span data-ttu-id="063a7-138">HDInsight 3.3 클러스터를 사용하는 경우 `<dependencies>` 섹션에 다음을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-138">If you are using an HDInsight 3.3 cluster, you must also add the following to the `<dependencies>` section:</span></span>

        <dependency>
            <groupId>org.apache.phoenix</groupId>
            <artifactId>phoenix-core</artifactId>
            <version>4.4.0-HBase-1.1</version>
        </dependency>

    <span data-ttu-id="063a7-139">이 종속성에 따라 Hbase 버전 1.1.x에서 사용되는 phoenix-core 구성 요소가 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-139">This dependency will load the phoenix-core components, which are used by Hbase version 1.1.x.</span></span>
3. <span data-ttu-id="063a7-140">**pom.xml** 파일에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-140">Add the following code to the **pom.xml** file.</span></span> <span data-ttu-id="063a7-141">이 섹션은 파일의 `<project>...</project>` 태그 내에 있어야 합니다. 예를 들어`</dependencies>`과 `</project>` 사이에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-141">This section must be inside the `<project>...</project>` tags in the file, for example, between `</dependencies>` and `</project>`.</span></span>

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
                    <source>1.7</source>
                    <target>1.7</target>
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

    <span data-ttu-id="063a7-142">`<resources>` 섹션은 HBase에 대한 구성 정보를 포함하는 리소스(**conf\hbase-site.xml**)를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-142">The `<resources>` section configures a resource (**conf\hbase-site.xml**) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="063a7-143">또한 코드를 통해 구성 값을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-143">You can also set configuration values via code.</span></span> <span data-ttu-id="063a7-144">작업 방법은 뒤에 나오는 **CreateTable** 예제의 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="063a7-144">See the comments in the **CreateTable** example that follows for how to do this.</span></span>
   >
   >

    <span data-ttu-id="063a7-145">이 `<plugins>` 섹션에서는 [Maven 컴파일러 플러그 인](http://maven.apache.org/plugins/maven-compiler-plugin/) 및 [Maven 음영 플러그 인](http://maven.apache.org/plugins/maven-shade-plugin/)도 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-145">This `<plugins>` section configures the [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="063a7-146">컴파일러 플러그 인은 토폴로지를 컴파일하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-146">The compiler plug-in is used to compile the topology.</span></span> <span data-ttu-id="063a7-147">음영 플러그 인은 Maven으로 빌드된 JAR 패키지에서 라이선스 중복을 방지하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-147">The shade plug-in is used to prevent license duplication in the JAR package that is built by Maven.</span></span> <span data-ttu-id="063a7-148">이 플러그 인을 사용하는 이유는 중복 라이선스 파일이 HDInsight 클러스터에서 런타임으로 오류를 일으키기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-148">The reason this is used is that the duplicate license files cause an error at run time on the HDInsight cluster.</span></span> <span data-ttu-id="063a7-149">`ApacheLicenseResourceTransformer` 구현에서 maven-shade-plugin을 사용하면 이 오류가 방지됩니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-149">Using maven-shade-plugin with the `ApacheLicenseResourceTransformer` implementation prevents this error.</span></span>

    <span data-ttu-id="063a7-150">또한 maven-shade-plugin은 응용 프로그램에 필요한 모든 종속성을 포함하는 uber jar(또는 fat jar)도 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-150">The maven-shade-plugin also produces an uber jar (or fat jar) that contains all the dependencies required by the application.</span></span>
4. <span data-ttu-id="063a7-151">**pom.xml** 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-151">Save the **pom.xml** file.</span></span>
5. <span data-ttu-id="063a7-152">**hbaseapp** 디렉터리에 **conf**이라는 새 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-152">Create a new directory named **conf** in the **hbaseapp** directory.</span></span> <span data-ttu-id="063a7-153">**conf** 디렉터리에 **hbase-site.xml**이라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-153">In the **conf** directory, create a file named **hbase-site.xml**.</span></span> <span data-ttu-id="063a7-154">파일 내용으로 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-154">Use the following as the contents of the file:</span></span>

        <?xml version="1.0"?>
        <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
        <!--
        /**
          * Copyright 2010 The Apache Software Foundation
          *
          * Licensed to the Apache Software Foundation (ASF) under one
          * or more contributor license agreements.  See the NOTICE file
          * distributed with this work for additional information
          * regarding copyright ownership.  The ASF licenses this file
          * to you under the Apache License, Version 2.0 (the
          * "License"); you may not use this file except in compliance
          * with the License.  You may obtain a copy of the License at
          *
          *     http://www.apache.org/licenses/LICENSE-2.0
          *
          * Unless required by applicable law or agreed to in writing, software
          * distributed under the License is distributed on an "AS IS" BASIS,
          * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
          * See the License for the specific language governing permissions and
          * limitations under the License.
          */
        -->
        <configuration>
          <property>
            <name>hbase.cluster.distributed</name>
            <value>true</value>
          </property>
          <property>
            <name>hbase.zookeeper.quorum</name>
            <value>zookeeper0,zookeeper1,zookeeper2</value>
          </property>
          <property>
            <name>hbase.zookeeper.property.clientPort</name>
            <value>2181</value>
          </property>
        </configuration>

    <span data-ttu-id="063a7-155">이 파일은 HDInsight 클러스터용 HBase 구성을 로드하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-155">This file will be used to load the HBase configuration for an HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="063a7-156">이 파일은 최소 크기의 hbase-site.xml 파일로, HDInsight 클러스터용 완전한 최소 설정을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-156">This is a minimal hbase-site.xml file, and it contains the bare minimum settings for the HDInsight cluster.</span></span>

6. <span data-ttu-id="063a7-157">**hbase-site.xml** 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-157">Save the **hbase-site.xml** file.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="063a7-158">응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="063a7-158">Create the application</span></span>
1. <span data-ttu-id="063a7-159">**hbaseapp\src\main\java\com\microsoft\examples** 디렉터리로 이동하여 app.java 파일 이름을 **CreateTable.java**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-159">Go to the **hbaseapp\src\main\java\com\microsoft\examples** directory and rename the app.java file to **CreateTable.java**.</span></span>
2. <span data-ttu-id="063a7-160">**CreateTable.java** 파일을 열고 기존 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-160">Open the **CreateTable.java** file and replace the existing contents with the following code:</span></span>

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
            // The following sets the znode root for Linux-based HDInsight
            //config.set("zookeeper.znode.parent","/hbase-unsecure");

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

    <span data-ttu-id="063a7-161">이 코드는 **CreateTable** 클래스이며, **people**이라는 테이블을 만들고 미리 정의된 사용자로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-161">This is the **CreateTable** class, which will create a table named **people** and populate it with some predefined users.</span></span>
3. <span data-ttu-id="063a7-162">**CreateTable.java** 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-162">Save the **CreateTable.java** file.</span></span>
4. <span data-ttu-id="063a7-163">**hbaseapp\src\main\java\com\microsoft\examples** 디렉터리에서 **SearchByEmail.java**라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-163">In the **hbaseapp\src\main\java\com\microsoft\examples** directory, create a new file named **SearchByEmail.java**.</span></span> <span data-ttu-id="063a7-164">이 파일의 내용으로 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-164">Use the following code as the contents of this file:</span></span>

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

            // Create a new regex filter
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

    <span data-ttu-id="063a7-165">**SearchByEmail** 클래스를 사용하여 메일 주소로 행을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-165">The **SearchByEmail** class can be used to query for rows by email address.</span></span> <span data-ttu-id="063a7-166">정규식 필터를 사용하므로, 이 클래스를 사용할 때 문자열 또는 정규식을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-166">Because it uses a regular expression filter, you can provide either a string or a regular expression when using the class.</span></span>
5. <span data-ttu-id="063a7-167">**SearchByEmail.java** 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-167">Save the **SearchByEmail.java** file.</span></span>
6. <span data-ttu-id="063a7-168">**hbaseapp\src\main\hava\com\microsoft\examples** 디렉터리에서 **DeleteTable.java**라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-168">In the **hbaseapp\src\main\hava\com\microsoft\examples** directory, create a new file named **DeleteTable.java**.</span></span> <span data-ttu-id="063a7-169">이 파일의 내용으로 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-169">Use the following code as the contents of this file:</span></span>

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

    <span data-ttu-id="063a7-170">이 클래스는 **CreateTable** 클래스로 생성된 테이블을 비활성화하고 제거하여 이 예제를 정리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-170">This class is for cleaning up this example by disabling and dropping the table created by the **CreateTable** class.</span></span>
7. <span data-ttu-id="063a7-171">**DeleteTable.java** 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-171">Save the **DeleteTable.java** file.</span></span>

## <a name="build-and-package-the-application"></a><span data-ttu-id="063a7-172">응용 프로그램 빌드 및 패키지화</span><span class="sxs-lookup"><span data-stu-id="063a7-172">Build and package the application</span></span>
1. <span data-ttu-id="063a7-173">명령 프롬프트를 열고 **hbaseapp** 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-173">Open a command prompt and change directories to the **hbaseapp** directory.</span></span>
2. <span data-ttu-id="063a7-174">다음 명령을 사용하여 응용 프로그램을 포함하는 JAR 파일을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-174">Use the following command to build a JAR file that contains the application:</span></span>

        mvn clean package

    <span data-ttu-id="063a7-175">이 코드는 이전 빌드 아티팩트를 정리하고, 아직 설치되지 않은 모든 종속성을 다운로드한 후 응용 프로그램을 빌드 및 패키지화합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-175">This cleans any previous build artifacts, downloads any dependencies that have not already been installed, then builds and packages the application.</span></span>
3. <span data-ttu-id="063a7-176">명령이 완료되면 **hbaseapp\target** 디렉터리에 **hbaseapp-1.0-SNAPSHOT.jar**이라는 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-176">When the command completes, the **hbaseapp\target** directory contains a file named **hbaseapp-1.0-SNAPSHOT.jar**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="063a7-177">**hbaseapp-1.0-SNAPSHOT.jar** 파일은 응용 프로그램을 실행하는 데 필요한 모든 종속성을 포함하는 uber jar(fat jar라고도 함)입니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-177">The **hbaseapp-1.0-SNAPSHOT.jar** file is an uber jar (sometimes called a fat jar,) which contains all the dependencies required to run the application.</span></span>

## <a name="upload-the-jar-file-and-start-a-job"></a><span data-ttu-id="063a7-178">JAR 파일 업로드 및 작업 시작</span><span class="sxs-lookup"><span data-stu-id="063a7-178">Upload the JAR file and start a job</span></span>
<span data-ttu-id="063a7-179">[HDInsight에서 Hadoop 작업용 데이터 업로드](hdinsight-upload-data.md)에서 설명한 대로 HDInsight 클러스터에 파일을 업로드하는 방법은 많습니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-179">There are many ways to upload a file to your HDInsight cluster, as described in [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span> <span data-ttu-id="063a7-180">다음 단계에서는 Azure PowerShell을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-180">The following steps use Azure PowerShell.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

1. <span data-ttu-id="063a7-181">Azure PowerShell을 설치 및 구성한 후 **hbase-runner.psm1**이라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-181">After installing and configuring Azure PowerShell, create a new file named **hbase-runner.psm1**.</span></span> <span data-ttu-id="063a7-182">이 파일의 내용으로 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-182">Use the following as the contents of this file:</span></span>

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

    <span data-ttu-id="063a7-183">이 파일에는 다음 두 모듈이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-183">This file contains two modules:</span></span>

   * <span data-ttu-id="063a7-184">**Add-HDInsightFile** - HDInsight에 파일을 업로드하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-184">**Add-HDInsightFile** - used to upload files to HDInsight</span></span>
   * <span data-ttu-id="063a7-185">**Start-HBaseExample** - 이전에 생성한 클래스를 실행하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-185">**Start-HBaseExample** - used to run the classes created earlier</span></span>
2. <span data-ttu-id="063a7-186">**hbase-runner.psm1** 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-186">Save the **hbase-runner.psm1** file.</span></span>
3. <span data-ttu-id="063a7-187">새 Azure PowerShell 창을 열고, **hbaseapp** 디렉터리로 이동한 후 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-187">Open a new Azure PowerShell window, change directories to the **hbaseapp** directory, and then run the following command.</span></span>

        PS C:\ Import-Module c:\path\to\hbase-runner.psm1

    <span data-ttu-id="063a7-188">이전에 만든 **hbase-runner.psm1** 파일의 위치로 경로를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-188">Change the path to the location of the **hbase-runner.psm1** file created earlier.</span></span> <span data-ttu-id="063a7-189">그러면 이 Azure PowerShell 세션에 대한 모듈이 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-189">This registers the module for this Azure PowerShell session.</span></span>
4. <span data-ttu-id="063a7-190">다음 명령을 사용하여 HDInsight 클러스터에 **hbaseapp-1.0-SNAPSHOT.jar**을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-190">Use the following command to upload the **hbaseapp-1.0-SNAPSHOT.jar** to your HDInsight cluster.</span></span>

        Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername

    <span data-ttu-id="063a7-191">**hdinsightclustername**을 HDInsight 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-191">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span></span> <span data-ttu-id="063a7-192">이 명령은 HDInsight 클러스터용 기본 저장소의 **example/jars** 위치로 **hbaseapp-1.0-SNAPSHOT.jar**을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-192">The command uploads the **hbaseapp-1.0-SNAPSHOT.jar** to the **example/jars** location in the primary storage for your HDInsight cluster.</span></span>
5. <span data-ttu-id="063a7-193">파일을 업로드한 후 다음 코드를 사용하여 **hbaseapp**으로 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-193">After the files are uploaded, use the following code to create a table using the **hbaseapp**:</span></span>

        Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername

    <span data-ttu-id="063a7-194">**hdinsightclustername**을 HDInsight 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-194">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="063a7-195">이 명령은 HDInsight 클러스터에 **people**이라는 새 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-195">This command creates a new table named **people** in your HDInsight cluster.</span></span> <span data-ttu-id="063a7-196">이 명령은 콘솔 창에 출력을 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-196">This command does not show any output in the console window.</span></span>
6. <span data-ttu-id="063a7-197">테이블에서 항목을 검색하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-197">To search for entries in the table, use the following command:</span></span>

        Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com

    <span data-ttu-id="063a7-198">**hdinsightclustername**을 HDInsight 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-198">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="063a7-199">이 명령은 **SearchByEmail** 클래스를 사용하여 **contactinformation** 열 패밀리 및 **email** 열에 **contoso.com** 문자열이 포함된 모든 행을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-199">This command uses the **SearchByEmail** class to search for any rows where the **contactinformation** column family and the **email** column, contains the string **contoso.com**.</span></span> <span data-ttu-id="063a7-200">다음과 같은 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-200">You should receive the following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="063a7-201">`-emailRegex` 값에 **fabrikam.com**을 사용하면 메일 필드에 **fabrikam.com**을 포함하는 사용자가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-201">Using **fabrikam.com** for the `-emailRegex` value returns the users that have **fabrikam.com** in the email field.</span></span> <span data-ttu-id="063a7-202">이 검색은 정규식 기반 필터를 사용하여 구현되므로, **^r**과 같은 정규식을 입력할 수 있습니다. 이 정규식은 메일이 'r' 문자로 시작하는 항목을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-202">Since this search is implemented by using a regular expression-based filter, you can also enter regular expressions, such as **^r**, which returns entries where the email begins with the letter 'r'.</span></span>

## <a name="delete-the-table"></a><span data-ttu-id="063a7-203">테이블 삭제</span><span class="sxs-lookup"><span data-stu-id="063a7-203">Delete the table</span></span>
<span data-ttu-id="063a7-204">예제를 완료하면 Azure PowerShell 세션에서 다음 명령을 사용하여 이 예제에 사용된 **people** 테이블을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-204">When you are done with the example, use the following command from the Azure PowerShell session to delete the **people** table used in this example:</span></span>

    Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername

<span data-ttu-id="063a7-205">**hdinsightclustername**을 HDInsight 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-205">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="063a7-206">문제 해결</span><span class="sxs-lookup"><span data-stu-id="063a7-206">Troubleshooting</span></span>
### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="063a7-207">Start-HBaseExample을 사용할 경우 결과가 없거나 예기치 않은 결과가 표시됨</span><span class="sxs-lookup"><span data-stu-id="063a7-207">No results or unexpected results when using Start-HBaseExample</span></span>
<span data-ttu-id="063a7-208">`-showErr` 매개 변수를 사용하여 작업을 실행하는 동안 생성된 표준 오류(STDERR)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="063a7-208">Use the `-showErr` parameter to view the standard error (STDERR) that is produced while running the job.</span></span>
