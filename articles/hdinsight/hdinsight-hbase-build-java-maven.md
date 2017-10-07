---
title: "Windows 기반 Azure HDInsight에 대 한 Java HBase 응용 프로그램 aaaBuild | Microsoft Docs"
description: "자세한 내용은 방법 toouse Apache Maven Java 기반 toobuild Apache HBase 응용 프로그램에 배포 tooa Windows 기반 Azure HDInsight 클러스터입니다."
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
ms.openlocfilehash: 33c2f3d12cb6a17b5406817e8bcd3accff239517
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-maven-toobuild-java-applications-that-use-hbase-with-windows-based-hdinsight-hadoop"></a><span data-ttu-id="fd474-103">Windows 기반 HDInsight (Hadoop)와 HBase를 사용 하는 Maven toobuild Java 응용 프로그램을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="fd474-103">Use Maven toobuild Java applications that use HBase with Windows-based HDInsight (Hadoop)</span></span>
<span data-ttu-id="fd474-104">자세한 내용은 어떻게 toocreate 및 빌드는 [Apache HBase](http://hbase.apache.org/) Apache Maven을 사용 하 여 java에서 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-104">Learn how toocreate and build an [Apache HBase](http://hbase.apache.org/) application in Java by using Apache Maven.</span></span> <span data-ttu-id="fd474-105">다음 hello 응용 프로그램을 사용 하 여 Azure HDInsight (Hadoop) 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-105">Then use hello application with Azure HDInsight (Hadoop).</span></span>

<span data-ttu-id="fd474-106">[Maven](http://maven.apache.org/) 는 소프트웨어 프로젝트 관리 및 이해 도구 toobuild 소프트웨어, 설명서 및 Java 프로젝트에 대 한 보고서 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-106">[Maven](http://maven.apache.org/) is a software project management and comprehension tool that allows you toobuild software, documentation, and reports for Java projects.</span></span> <span data-ttu-id="fd474-107">이 문서에서는 설명 어떻게 toouse 것 toocreate를 만들고, 쿼리 및 삭제는 HBase 테이블 Azure HDInsight 클러스터에는 기본 Java 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-107">In this article, you learn how toouse it toocreate a basic Java application that that creates, queries, and deletes an HBase table on an Azure HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fd474-108">이 문서의 단계 hello 창을 사용 하 여 HDInsight 클러스터를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-108">hello steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="fd474-109">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="fd474-110">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fd474-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="fd474-111">요구 사항</span><span class="sxs-lookup"><span data-stu-id="fd474-111">Requirements</span></span>
* <span data-ttu-id="fd474-112">[Java 플랫폼 JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 이상</span><span class="sxs-lookup"><span data-stu-id="fd474-112">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 or later</span></span>
* [<span data-ttu-id="fd474-113">Maven</span><span class="sxs-lookup"><span data-stu-id="fd474-113">Maven</span></span>](http://maven.apache.org/)
* <span data-ttu-id="fd474-114">Windows 기반 HDInsight 클러스터 및 HBase</span><span class="sxs-lookup"><span data-stu-id="fd474-114">A Windows-based HDInsight cluster with HBase</span></span>

    > [!NOTE]
    > <span data-ttu-id="fd474-115">이 문서의 단계 hello HDInsight 클러스터 버전 3.2 및 3.3으로 테스트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-115">hello steps in this document have been tested with HDInsight cluster versions 3.2 and 3.3.</span></span> <span data-ttu-id="fd474-116">3.3 HDInsight 클러스터에 대 한 예제에 제공 된 hello 기본값 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-116">hello default values provided in examples are for a HDInsight 3.3 cluster.</span></span>

## <a name="create-hello-project"></a><span data-ttu-id="fd474-117">Hello 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="fd474-117">Create hello project</span></span>
1. <span data-ttu-id="fd474-118">Hello 명령줄에서 개발 환경에서 디렉터리 toohello 저장할 위치 toocreate hello 프로젝트 예를 들어 변경 `cd code\hdinsight`합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-118">From hello command line in your development environment, change directories toohello location where you want toocreate hello project, for example, `cd code\hdinsight`.</span></span>
2. <span data-ttu-id="fd474-119">사용 하 여 hello **mvn** Maven에서 hello 프로젝트에 대 한 스 캐 폴딩 toogenerate hello 함께 설치 된 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-119">Use hello **mvn** command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

        mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

    <span data-ttu-id="fd474-120">이 명령은 hello 지정 된 이름의 hello hello 현재 위치에 디렉터리를 만듭니다 **의 artifactID** 매개 변수 (**hbaseapp** 이 예에서.) 이 디렉터리는 다음 항목 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-120">This command creates a directory in hello current location, with hello name specified by hello **artifactID** parameter (**hbaseapp** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="fd474-121">**pom.xml**: hello Project 개체 모델 ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) 정보 및 구성 사용 세부 정보 toobuild hello 프로젝트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-121">**pom.xml**:  hello Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used toobuild hello project.</span></span>
   * <span data-ttu-id="fd474-122">**src**: hello를 포함 하는 hello 디렉터리 **main\java\com\microsoft\examples** 디렉터리, hello 응용 프로그램을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-122">**src**: hello directory that contains hello **main\java\com\microsoft\examples** directory, where you will author hello application.</span></span>
3. <span data-ttu-id="fd474-123">Hello 삭제 **src\test\java\com\microsoft\examples\apptest.java** 파일 때문에이 예에서는 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-123">Delete hello **src\test\java\com\microsoft\examples\apptest.java** file because it is not used in this example.</span></span>

## <a name="update-hello-project-object-model"></a><span data-ttu-id="fd474-124">업데이트 hello Project 개체 모델</span><span class="sxs-lookup"><span data-stu-id="fd474-124">Update hello Project Object Model</span></span>
1. <span data-ttu-id="fd474-125">Hello 편집 **pom.xml** 파일을 hello hello 내부에서 코드를 다음 추가 `<dependencies>` 섹션:</span><span class="sxs-lookup"><span data-stu-id="fd474-125">Edit hello **pom.xml** file and add hello following code inside hello `<dependencies>` section:</span></span>

        <dependency>
          <groupId>org.apache.hbase</groupId>
          <artifactId>hbase-client</artifactId>
          <version>1.1.2</version>
        </dependency>

    <span data-ttu-id="fd474-126">이 섹션에서는 프로젝트 hello Maven 필요 설명 **hbase 클라이언트** 버전 **1.1.2**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-126">This section tells Maven that hello project requires **hbase-client** version **1.1.2**.</span></span> <span data-ttu-id="fd474-127">컴파일 타임에이 종속성 hello 기본 Maven 저장소에서 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-127">At compile time, this dependency is downloaded from hello default Maven repository.</span></span> <span data-ttu-id="fd474-128">Hello를 사용할 수 있습니다 [Maven 중앙 리포지토리 검색](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn이이 종속성에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-128">You can use hello [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="fd474-129">hello 버전 번호는 HDInsight 클러스터와 함께 제공 되는 HBase의 hello 버전과 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-129">hello version number must match hello version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="fd474-130">다음 테이블 toofind hello 올바른 버전 번호는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-130">Use hello following table toofind hello correct version number.</span></span>
   >
   >

   | <span data-ttu-id="fd474-131">HDInsight 클러스터 버전</span><span class="sxs-lookup"><span data-stu-id="fd474-131">HDInsight cluster version</span></span> | <span data-ttu-id="fd474-132">HBase 버전 toouse</span><span class="sxs-lookup"><span data-stu-id="fd474-132">HBase version toouse</span></span> |
   | --- | --- |
   | <span data-ttu-id="fd474-133">3.2</span><span class="sxs-lookup"><span data-stu-id="fd474-133">3.2</span></span> |<span data-ttu-id="fd474-134">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="fd474-134">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="fd474-135">3.3</span><span class="sxs-lookup"><span data-stu-id="fd474-135">3.3</span></span> |<span data-ttu-id="fd474-136">1.1.2</span><span class="sxs-lookup"><span data-stu-id="fd474-136">1.1.2</span></span> |

    <span data-ttu-id="fd474-137">HDInsight 버전 및 구성 요소에 대 한 자세한 내용은 참조 하십시오. [hello 다른 Hadoop 구성 요소 HDInsight를 사용할 수 있는](hdinsight-component-versioning.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-137">For more information on HDInsight versions and components, see [What are hello different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>
2. <span data-ttu-id="fd474-138">다음 toohello hello 3.3 HDInsight 클러스터를 사용 하는 경우도 추가 해야 `<dependencies>` 섹션:</span><span class="sxs-lookup"><span data-stu-id="fd474-138">If you are using an HDInsight 3.3 cluster, you must also add hello following toohello `<dependencies>` section:</span></span>

        <dependency>
            <groupId>org.apache.phoenix</groupId>
            <artifactId>phoenix-core</artifactId>
            <version>4.4.0-HBase-1.1</version>
        </dependency>

    <span data-ttu-id="fd474-139">이 종속성 Hbase 버전에서 사용 되는 hello 피닉스 핵심 구성 요소를 로드 합니다 1.1.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-139">This dependency will load hello phoenix-core components, which are used by Hbase version 1.1.x.</span></span>
3. <span data-ttu-id="fd474-140">다음 코드 toohello hello 추가 **pom.xml** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-140">Add hello following code toohello **pom.xml** file.</span></span> <span data-ttu-id="fd474-141">이 섹션은 hello 내부에 있어야 합니다. `<project>...</project>` 사이 hello에 태그 파일 예를 들어, `</dependencies>` 및 `</project>`합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-141">This section must be inside hello `<project>...</project>` tags in hello file, for example, between `</dependencies>` and `</project>`.</span></span>

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

    <span data-ttu-id="fd474-142">hello `<resources>` 섹션에는 리소스 구성 (**conf\hbase site.xml**) HBase에 대 한 구성 정보를 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-142">hello `<resources>` section configures a resource (**conf\hbase-site.xml**) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fd474-143">또한 코드를 통해 구성 값을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-143">You can also set configuration values via code.</span></span> <span data-ttu-id="fd474-144">Hello에 hello 메모를 참조 하십시오. **CreateTable** 방법에 대 한 다음에 나오는 예제 toodo이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-144">See hello comments in hello **CreateTable** example that follows for how toodo this.</span></span>
   >
   >

    <span data-ttu-id="fd474-145">이 `<plugins>` 섹션 구성 hello [Maven 컴파일러 플러그 인](http://maven.apache.org/plugins/maven-compiler-plugin/) 및 [Maven 음영 플러그 인](http://maven.apache.org/plugins/maven-shade-plugin/)합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-145">This `<plugins>` section configures hello [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="fd474-146">hello 컴파일러 플러그 인에 사용 되는 toocompile hello 토폴로지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-146">hello compiler plug-in is used toocompile hello topology.</span></span> <span data-ttu-id="fd474-147">플러그 인 hello 음영 Maven에 의해 빌드되는 hello JAR 패키지에서 사용 되는 tooprevent 라이선스 중복입니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-147">hello shade plug-in is used tooprevent license duplication in hello JAR package that is built by Maven.</span></span> <span data-ttu-id="fd474-148">이 옵션은 사용 하는 hello 이유 hello 중복 라이선스 파일 hello HDInsight 클러스터에서 실행 시 오류가 발생 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-148">hello reason this is used is that hello duplicate license files cause an error at run time on hello HDInsight cluster.</span></span> <span data-ttu-id="fd474-149">Maven-음영-플러그 인을 사용 하 여 hello로 `ApacheLicenseResourceTransformer` 구현이이 오류를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-149">Using maven-shade-plugin with hello `ApacheLicenseResourceTransformer` implementation prevents this error.</span></span>

    <span data-ttu-id="fd474-150">hello maven-음영-플러그인도 생성 uber jar (또는 fat jar) hello 응용 프로그램에 필요한 모든 hello 종속성을 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-150">hello maven-shade-plugin also produces an uber jar (or fat jar) that contains all hello dependencies required by hello application.</span></span>
4. <span data-ttu-id="fd474-151">Hello 저장 **pom.xml** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-151">Save hello **pom.xml** file.</span></span>
5. <span data-ttu-id="fd474-152">라는 새 디렉터리를 만들고 **conf** hello에 **hbaseapp** 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-152">Create a new directory named **conf** in hello **hbaseapp** directory.</span></span> <span data-ttu-id="fd474-153">Hello에 **conf** 디렉터리 라는 파일을 만들어 **hbase-site.xml**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-153">In hello **conf** directory, create a file named **hbase-site.xml**.</span></span> <span data-ttu-id="fd474-154">Hello 다음 hello 파일의 내용을 hello 사용:</span><span class="sxs-lookup"><span data-stu-id="fd474-154">Use hello following as hello contents of hello file:</span></span>

        <?xml version="1.0"?>
        <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
        <!--
        /**
          * Copyright 2010 hello Apache Software Foundation
          *
          * Licensed toohello Apache Software Foundation (ASF) under one
          * or more contributor license agreements.  See hello NOTICE file
          * distributed with this work for additional information
          * regarding copyright ownership.  hello ASF licenses this file
          * tooyou under hello Apache License, Version 2.0 (the
          * "License"); you may not use this file except in compliance
          * with hello License.  You may obtain a copy of hello License at
          *
          *     http://www.apache.org/licenses/LICENSE-2.0
          *
          * Unless required by applicable law or agreed tooin writing, software
          * distributed under hello License is distributed on an "AS IS" BASIS,
          * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
          * See hello License for hello specific language governing permissions and
          * limitations under hello License.
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

    <span data-ttu-id="fd474-155">이 파일에는 HDInsight 클러스터에 대 한 사용된 tooload hello HBase 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-155">This file will be used tooload hello HBase configuration for an HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fd474-156">최소 hbase-site.xml 파일 이며 hello HDInsight 클러스터에 대 한 hello 완전 최소 설정을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-156">This is a minimal hbase-site.xml file, and it contains hello bare minimum settings for hello HDInsight cluster.</span></span>

6. <span data-ttu-id="fd474-157">Hello 저장 **hbase-site.xml** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-157">Save hello **hbase-site.xml** file.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="fd474-158">Hello 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="fd474-158">Create hello application</span></span>
1. <span data-ttu-id="fd474-159">Toohello 이동 **hbaseapp\src\main\java\com\microsoft\examples** 디렉터리 및 이름 바꾸기 hello app.java 파일 너무**CreateTable.java**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-159">Go toohello **hbaseapp\src\main\java\com\microsoft\examples** directory and rename hello app.java file too**CreateTable.java**.</span></span>
2. <span data-ttu-id="fd474-160">열기 hello **CreateTable.java** 파일 및 코드 다음 hello hello 기존 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-160">Open hello **CreateTable.java** file and replace hello existing contents with hello following code:</span></span>

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
            // hello following sets hello znode root for Linux-based HDInsight
            //config.set("zookeeper.znode.parent","/hbase-unsecure");

            // create an admin object using hello config
            HBaseAdmin admin = new HBaseAdmin(config);

            // create hello table...
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

            // Add each person toohello table
            //   Use hello `name` column family for hello name
            //   Use hello `contactinfo` column family for hello email
            for (int i = 0; i< people.length; i++) {
              Put person = new Put(Bytes.toBytes(people[i][0]));
              person.add(Bytes.toBytes("name"), Bytes.toBytes("first"), Bytes.toBytes(people[i][1]));
              person.add(Bytes.toBytes("name"), Bytes.toBytes("last"), Bytes.toBytes(people[i][2]));
              person.add(Bytes.toBytes("contactinfo"), Bytes.toBytes("email"), Bytes.toBytes(people[i][3]));
              table.put(person);
            }
            // flush commits and close hello table
            table.flushCommits();
            table.close();
          }
        }

    <span data-ttu-id="fd474-161">이 hello **CreateTable** 클래스 이라는 테이블이 생성 됩니다 **사람** 미리 정의 된 사용자로 구성 된 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-161">This is hello **CreateTable** class, which will create a table named **people** and populate it with some predefined users.</span></span>
3. <span data-ttu-id="fd474-162">Hello 저장 **CreateTable.java** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-162">Save hello **CreateTable.java** file.</span></span>
4. <span data-ttu-id="fd474-163">Hello에 **hbaseapp\src\main\java\com\microsoft\examples** 디렉터리 라는 새 파일을 만들어 **SearchByEmail.java**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-163">In hello **hbaseapp\src\main\java\com\microsoft\examples** directory, create a new file named **SearchByEmail.java**.</span></span> <span data-ttu-id="fd474-164">이 파일의 내용을 hello로 코드를 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-164">Use hello following code as hello contents of this file:</span></span>

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

            // Use GenericOptionsParser tooget only hello parameters toohello class
            // and not all hello parameters passed (when using WebHCat for example)
            String[] otherArgs = new GenericOptionsParser(config, args).getRemainingArgs();
            if (otherArgs.length != 1) {
              System.out.println("usage: [regular expression]");
              System.exit(-1);
            }

            // Open hello table
            HTable table = new HTable(config, "people");

            // Define hello family and qualifiers toobe used
            byte[] contactFamily = Bytes.toBytes("contactinfo");
            byte[] emailQualifier = Bytes.toBytes("email");
            byte[] nameFamily = Bytes.toBytes("name");
            byte[] firstNameQualifier = Bytes.toBytes("first");
            byte[] lastNameQualifier = Bytes.toBytes("last");

            // Create a new regex filter
            RegexStringComparator emailFilter = new RegexStringComparator(otherArgs[0]);
            // Attach hello regex filter tooa filter
            //   for hello email column
            SingleColumnValueFilter filter = new SingleColumnValueFilter(
              contactFamily,
              emailQualifier,
              CompareOp.EQUAL,
              emailFilter
            );

            // Create a scan and set hello filter
            Scan scan = new Scan();
            scan.setFilter(filter);

            // Get hello results
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

    <span data-ttu-id="fd474-165">hello **SearchByEmail** 클래스에는 전자 메일 주소로 행에 대 한 사용된 tooquery 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-165">hello **SearchByEmail** class can be used tooquery for rows by email address.</span></span> <span data-ttu-id="fd474-166">정규식 필터를 사용 하기 때문에 hello 클래스를 사용 하는 경우 문자열이 나 정규식을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-166">Because it uses a regular expression filter, you can provide either a string or a regular expression when using hello class.</span></span>
5. <span data-ttu-id="fd474-167">Hello 저장 **SearchByEmail.java** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-167">Save hello **SearchByEmail.java** file.</span></span>
6. <span data-ttu-id="fd474-168">Hello에 **hbaseapp\src\main\hava\com\microsoft\examples** 디렉터리 라는 새 파일을 만들어 **DeleteTable.java**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-168">In hello **hbaseapp\src\main\hava\com\microsoft\examples** directory, create a new file named **DeleteTable.java**.</span></span> <span data-ttu-id="fd474-169">이 파일의 내용을 hello로 코드를 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-169">Use hello following code as hello contents of this file:</span></span>

        package com.microsoft.examples;
        import java.io.IOException;

        import org.apache.hadoop.conf.Configuration;
        import org.apache.hadoop.hbase.HBaseConfiguration;
        import org.apache.hadoop.hbase.client.HBaseAdmin;

        public class DeleteTable {
          public static void main(String[] args) throws IOException {
            Configuration config = HBaseConfiguration.create();

            // Create an admin object using hello config
            HBaseAdmin admin = new HBaseAdmin(config);

            // Disable, and then delete hello table
            admin.disableTable("people");
            admin.deleteTable("people");
          }
        }

    <span data-ttu-id="fd474-170">이 클래스는 사용 하지 않도록 설정 하 여이 예제를 정리 하는 hello에서 만든 hello 테이블 삭제 및 **CreateTable** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-170">This class is for cleaning up this example by disabling and dropping hello table created by hello **CreateTable** class.</span></span>
7. <span data-ttu-id="fd474-171">Hello 저장 **DeleteTable.java** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-171">Save hello **DeleteTable.java** file.</span></span>

## <a name="build-and-package-hello-application"></a><span data-ttu-id="fd474-172">Hello 응용 프로그램을 빌드 및 패키지</span><span class="sxs-lookup"><span data-stu-id="fd474-172">Build and package hello application</span></span>
1. <span data-ttu-id="fd474-173">명령 프롬프트를 열고 디렉터리 toohello 변경 **hbaseapp** 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-173">Open a command prompt and change directories toohello **hbaseapp** directory.</span></span>
2. <span data-ttu-id="fd474-174">다음 명령 toobuild hello 응용 프로그램을 포함 하는 JAR 파일 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-174">Use hello following command toobuild a JAR file that contains hello application:</span></span>

        mvn clean package

    <span data-ttu-id="fd474-175">그러면 모든 이전 빌드 아티팩트를 정리, 아직 설치 하지 않은 모든 종속성을 다운로드, 다음 빌드되고 hello 응용 프로그램을 패키지.</span><span class="sxs-lookup"><span data-stu-id="fd474-175">This cleans any previous build artifacts, downloads any dependencies that have not already been installed, then builds and packages hello application.</span></span>
3. <span data-ttu-id="fd474-176">Hello 명령이 완료 되 면 hello **hbaseapp\target** 라는 파일을 포함 하는 디렉터리 **hbaseapp-1.0-SNAPSHOT.jar**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-176">When hello command completes, hello **hbaseapp\target** directory contains a file named **hbaseapp-1.0-SNAPSHOT.jar**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fd474-177">hello **hbaseapp-1.0-SNAPSHOT.jar** 파일은 한 uber 모든 hello 종속성을 포함 하는 jar (fat jar 라고도 함) toorun hello 응용 프로그램을 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-177">hello **hbaseapp-1.0-SNAPSHOT.jar** file is an uber jar (sometimes called a fat jar,) which contains all hello dependencies required toorun hello application.</span></span>

## <a name="upload-hello-jar-file-and-start-a-job"></a><span data-ttu-id="fd474-178">Hello JAR 파일을 업로드 하 고 작업 시작</span><span class="sxs-lookup"><span data-stu-id="fd474-178">Upload hello JAR file and start a job</span></span>
<span data-ttu-id="fd474-179">여러 방법으로 tooupload 파일 tooyour HDInsight 클러스터에 설명 된 대로 [HDInsight에서 Hadoop 작업에 대 한 데이터 업로드](hdinsight-upload-data.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-179">There are many ways tooupload a file tooyour HDInsight cluster, as described in [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span> <span data-ttu-id="fd474-180">hello 다음 단계 Azure PowerShell을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-180">hello following steps use Azure PowerShell.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

1. <span data-ttu-id="fd474-181">Azure PowerShell을 설치 및 구성한 후 **hbase-runner.psm1**이라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-181">After installing and configuring Azure PowerShell, create a new file named **hbase-runner.psm1**.</span></span> <span data-ttu-id="fd474-182">Hello 다음이이 파일의 내용을 hello 사용:</span><span class="sxs-lookup"><span data-stu-id="fd474-182">Use hello following as hello contents of this file:</span></span>

        <#
        .SYNOPSIS
        Copies a file toohello primary storage of an HDInsight cluster.
        .DESCRIPTION
        Copies a file from a local directory toohello blob container for
        hello HDInsight cluster.
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
        #hello class toorun
        [Parameter(Mandatory = $true)]
        [String]$className,

        #hello name of hello HDInsight cluster
        [Parameter(Mandatory = $true)]
        [String]$clusterName,

        #Only used when using SearchByEmail
        [Parameter(Mandatory = $false)]
        [String]$emailRegex,

        #Use if you want toosee stderr output
        [Parameter(Mandatory = $false)]
        [Switch]$showErr
        )

        Set-StrictMode -Version 3

        # Is hello Azure module installed?
        FindAzure

        # Get hello login for hello HDInsight cluster
        $creds=Get-Credential -Message "Enter hello login for hello cluster" -UserName "admin"

        # hello JAR
        $jarFile = "wasb:///example/jars/hbaseapp-1.0-SNAPSHOT.jar"

        # hello job definition
        $jobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
            -JarFile $jarFile `
            -ClassName $className `
            -Arguments $emailRegex

        # Get hello job output
        $job = Start-AzureRmHDInsightJob `
            -ClusterName $clusterName `
            -JobDefinition $jobDefinition `
            -HttpCredential $creds
        Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
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
        Write-Host "Display hello standard output ..." -ForegroundColor Green
        Get-AzureRmHDInsightJobOutput `
                    -Clustername $clusterName `
                    -JobId $job.JobId `
                    -HttpCredential $creds
        }

        <#
        .SYNOPSIS
        Copies a file toohello primary storage of an HDInsight cluster.
        .DESCRIPTION
        Copies a file from a local directory toohello blob container for
        hello HDInsight cluster.
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
                #hello path toohello local file.
                [Parameter(Mandatory = $true)]
                [String]$localPath,

                #hello destination path and file name, relative toohello root of hello container.
                [Parameter(Mandatory = $true)]
                [String]$destinationPath,

                #hello name of hello HDInsight cluster
                [Parameter(Mandatory = $true)]
                [String]$clusterName,

                #If specified, overwrites existing files without prompting
                [Parameter(Mandatory = $false)]
                [Switch]$force
            )

            Set-StrictMode -Version 3

            # Is hello Azure module installed?
            FindAzure

            # Get authentication for hello cluster
            $creds=Get-Credential

            # Does hello local path exist?
            if (-not (Test-Path $localPath))
            {
                throw "Source path '$localPath' does not exist."
            }

            # Get hello primary storage container
            $storage = GetStorage -clusterName $clusterName

            # Upload file toostorage, overwriting existing files if -force was used.
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
                throw "No active Azure subscription found! If you have a subscription, use hello Login-AzureRmAccount cmdlet toologin tooyour subscription."
            }
        }

        function GetStorage {
            param(
                [Parameter(Mandatory = $true)]
                [String]$clusterName
            )
            $hdi = Get-AzureRmHDInsightCluster -ClusterName $clusterName
            # Does hello cluster exist?
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
            # Get hello resource group, in case we need that
            $return.resourceGroup = $resourceGroup
            # Get hello storage context, as we can't depend
            # on using hello default storage context
            $return.context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
            # Get hello container, so we know where to
            # find/store blobs
            $return.container = $container
            # Return storage accounts toosupport finding all accounts for
            # a cluster
            $return.storageAccount = $storageAccountName
            $return.storageAccountKey = $storageAccountKey

            return $return
        }
        # Only export hello verb-phrase things
        export-modulemember *-*

    <span data-ttu-id="fd474-183">이 파일에는 다음 두 모듈이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-183">This file contains two modules:</span></span>

   * <span data-ttu-id="fd474-184">**추가 HDInsightFile** -tooupload 파일 tooHDInsight 사용</span><span class="sxs-lookup"><span data-stu-id="fd474-184">**Add-HDInsightFile** - used tooupload files tooHDInsight</span></span>
   * <span data-ttu-id="fd474-185">**시작 HBaseExample** -사용 되는 이전에 만든 toorun hello 클래스</span><span class="sxs-lookup"><span data-stu-id="fd474-185">**Start-HBaseExample** - used toorun hello classes created earlier</span></span>
2. <span data-ttu-id="fd474-186">Hello 저장 **hbase runner.psm1** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-186">Save hello **hbase-runner.psm1** file.</span></span>
3. <span data-ttu-id="fd474-187">새 Azure PowerShell 창을 열고, 디렉터리 toohello 변경 **hbaseapp** 디렉터리 누른 실행된 hello 다음 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-187">Open a new Azure PowerShell window, change directories toohello **hbaseapp** directory, and then run hello following command.</span></span>

        PS C:\ Import-Module c:\path\to\hbase-runner.psm1

    <span data-ttu-id="fd474-188">Hello의 hello 경로 toohello 위치 변경 **hbase runner.psm1** 앞에서 만든 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-188">Change hello path toohello location of hello **hbase-runner.psm1** file created earlier.</span></span> <span data-ttu-id="fd474-189">이 Azure PowerShell 세션에 대 한 hello 모듈을 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-189">This registers hello module for this Azure PowerShell session.</span></span>
4. <span data-ttu-id="fd474-190">사용 하 여 hello 다음 명령은 tooupload hello **hbaseapp-1.0-SNAPSHOT.jar** tooyour HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-190">Use hello following command tooupload hello **hbaseapp-1.0-SNAPSHOT.jar** tooyour HDInsight cluster.</span></span>

        Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername

    <span data-ttu-id="fd474-191">대체 **hdinsightclustername** HDInsight 클러스터의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-191">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="fd474-192">hello 명령 업로드 hello **hbaseapp-1.0-SNAPSHOT.jar** toohello **예제/jar** hello HDInsight 클러스터에 대 한 기본 저장소에 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-192">hello command uploads hello **hbaseapp-1.0-SNAPSHOT.jar** toohello **example/jars** location in hello primary storage for your HDInsight cluster.</span></span>
5. <span data-ttu-id="fd474-193">사용 하 여 hello 다음 코드 hello를 사용 하는 테이블 toocreate hello 파일을 업로드 한 후 **hbaseapp**:</span><span class="sxs-lookup"><span data-stu-id="fd474-193">After hello files are uploaded, use hello following code toocreate a table using hello **hbaseapp**:</span></span>

        Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername

    <span data-ttu-id="fd474-194">대체 **hdinsightclustername** HDInsight 클러스터의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-194">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="fd474-195">이 명령은 HDInsight 클러스터에 **people**이라는 새 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-195">This command creates a new table named **people** in your HDInsight cluster.</span></span> <span data-ttu-id="fd474-196">이 명령은 hello 콘솔 창에서 어떠한 출력도 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-196">This command does not show any output in hello console window.</span></span>
6. <span data-ttu-id="fd474-197">다음 명령을 사용 하 여 hello hello 테이블의 엔터티에 대 한 toosearch:</span><span class="sxs-lookup"><span data-stu-id="fd474-197">toosearch for entries in hello table, use hello following command:</span></span>

        Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com

    <span data-ttu-id="fd474-198">대체 **hdinsightclustername** HDInsight 클러스터의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-198">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="fd474-199">이 명령은 hello를 사용 하 여 **SearchByEmail** 여기서 hello toosearch 모든 행에 대 한 클래스 **contactinformation** 열 제품군 및 hello **전자 메일** hello 문자열을 포함 하는 열 **contoso.com**합니다. 결과 다음 hello을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-199">This command uses hello **SearchByEmail** class toosearch for any rows where hello **contactinformation** column family and hello **email** column, contains hello string **contoso.com**. You should receive hello following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="fd474-200">사용 하 여 **fabrikam.com** hello에 대 한 `-emailRegex` 값이 있는 hello 사용자가 반환 **fabrikam.com** hello 전자 메일 필드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-200">Using **fabrikam.com** for hello `-emailRegex` value returns hello users that have **fabrikam.com** in hello email field.</span></span> <span data-ttu-id="fd474-201">정규식,이 검색은 일반 식 기반 필터를 사용 하 여 구현, 되므로 같은 입력할 수도 있습니다 **^ r**, hello 전자 메일에서 hello 문자 'r'로 시작 되는 반환 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-201">Since this search is implemented by using a regular expression-based filter, you can also enter regular expressions, such as **^r**, which returns entries where hello email begins with hello letter 'r'.</span></span>

## <a name="delete-hello-table"></a><span data-ttu-id="fd474-202">Hello 테이블 삭제</span><span class="sxs-lookup"><span data-stu-id="fd474-202">Delete hello table</span></span>
<span data-ttu-id="fd474-203">Hello Azure PowerShell 세션 toodelete hello에서 사용 하 여 hello 다음 명령은 hello 예제 끝나면 **사람** 이 예에서 사용 된 테이블:</span><span class="sxs-lookup"><span data-stu-id="fd474-203">When you are done with hello example, use hello following command from hello Azure PowerShell session toodelete hello **people** table used in this example:</span></span>

    Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername

<span data-ttu-id="fd474-204">대체 **hdinsightclustername** HDInsight 클러스터의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-204">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="fd474-205">문제 해결</span><span class="sxs-lookup"><span data-stu-id="fd474-205">Troubleshooting</span></span>
### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="fd474-206">Start-HBaseExample을 사용할 경우 결과가 없거나 예기치 않은 결과가 표시됨</span><span class="sxs-lookup"><span data-stu-id="fd474-206">No results or unexpected results when using Start-HBaseExample</span></span>
<span data-ttu-id="fd474-207">사용 하 여 hello `-showErr` 매개 변수 tooview hello 표준 오류 (STDERR) 실행 중인 hello 작업 하는 동안 생성 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd474-207">Use hello `-showErr` parameter tooview hello standard error (STDERR) that is produced while running hello job.</span></span>
