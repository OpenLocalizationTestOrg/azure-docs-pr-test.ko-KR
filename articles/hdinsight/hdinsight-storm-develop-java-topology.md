---
title: "Apache Storm 예제 Java 토폴로지 - Azure HDInsight | Microsoft Docs"
description: "예제 단어 개수 토폴로지를 만들어 Java에서 Apache Storm 토폴로지를 만드는 방법에 대해 배웁니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: apache storm,apache storm example,storm java,storm topology example
ms.assetid: a8838f29-9c08-4fd9-99ef-26655d1bf6d7
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 36285fbaf1da3c566d338bd5612eebad327eaf50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-apache-storm-topology-in-java"></a><span data-ttu-id="501b8-104">Java에서 Apache Storm 토폴로지 만들기</span><span class="sxs-lookup"><span data-stu-id="501b8-104">Create an Apache Storm topology in Java</span></span>

<span data-ttu-id="501b8-105">Apache Storm에 대한 Java 기반 토폴로지를 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-105">Learn how to create a Java-based topology for Apache Storm.</span></span> <span data-ttu-id="501b8-106">단어 계산 응용 프로그램을 구현하는 Storm 토폴로지를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-106">You create a Storm topology that implements a word-count application.</span></span> <span data-ttu-id="501b8-107">Maven을 사용하여 프로젝트를 빌드하고 패키징합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-107">You use Maven to build and package the project.</span></span> <span data-ttu-id="501b8-108">그런 다음 Flux 프레임워크를 사용하여 토폴로지를 정의하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-108">Then, you learn how to define the topology using the Flux framework.</span></span>

> [!NOTE]
> <span data-ttu-id="501b8-109">Flux 프레임워크는 Storm 0.10.0 이상에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-109">The Flux framework is available in Storm 0.10.0 or later.</span></span> <span data-ttu-id="501b8-110">Storm 0.10.0은 HDInsight 3.3 및 3.4에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-110">Storm 0.10.0 is available with HDInsight 3.3 and 3.4.</span></span>

<span data-ttu-id="501b8-111">이 문서의 단계를 완료한 후에 HDInsight에서 Apache Storm에 토폴로지를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-111">After completing the steps in this document, you can deploy the topology to Apache Storm on HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="501b8-112">이 문서에서 만든 Storm 토폴로지의 완료된 버전은 [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-112">A completed version of the Storm topology examples created in this document is available at [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="501b8-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="501b8-113">Prerequisites</span></span>

* [<span data-ttu-id="501b8-114">JDK(Java Developer Kit) 버전 7</span><span class="sxs-lookup"><span data-stu-id="501b8-114">Java Developer Kit (JDK) version 7</span></span>](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* <span data-ttu-id="501b8-115">[Maven(https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Java 프로젝트를 위한 프로젝트 빌드 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="501b8-116">텍스트 편집기 또는 IDE</span><span class="sxs-lookup"><span data-stu-id="501b8-116">A text editor or IDE.</span></span>

## <a name="configure-environment-variables"></a><span data-ttu-id="501b8-117">환경 변수 구성</span><span class="sxs-lookup"><span data-stu-id="501b8-117">Configure environment variables</span></span>

<span data-ttu-id="501b8-118">Java 및 JDK를 설치할 때 다음 환경 변수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-118">The following environment variables may be set when you install Java and the JDK.</span></span> <span data-ttu-id="501b8-119">하지만 변수가 존재하며 시스템에 대한 올바른 값을 포함하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-119">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="501b8-120">**JAVA_HOME** - JRE(Java runtime environment)가 설치된 디렉터리를 가리켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-120">**JAVA_HOME** - should point to the directory where the Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="501b8-121">예를 들어 Unix 또는 Linux 배포에서는 `/usr/lib/jvm/java-7-oracle`과 유사한 값이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-121">For example, in a Unix or Linux distribution, it should have a value similar to `/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="501b8-122">Windows에서는 `c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="501b8-122">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="501b8-123">**PATH** - 다음 경로를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-123">**PATH** - should contain the following paths:</span></span>

  * <span data-ttu-id="501b8-124">**JAVA_HOME** 또는 그와 동등한 경로</span><span class="sxs-lookup"><span data-stu-id="501b8-124">**JAVA_HOME** (or the equivalent path)</span></span>

  * <span data-ttu-id="501b8-125">**JAVA_HOME\bin** 또는 그와 동등한 경로</span><span class="sxs-lookup"><span data-stu-id="501b8-125">**JAVA_HOME\bin** (or the equivalent path)</span></span>

  * <span data-ttu-id="501b8-126">Maven이 설치된 디렉터리</span><span class="sxs-lookup"><span data-stu-id="501b8-126">The directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="501b8-127">Maven 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="501b8-127">Create a Maven project</span></span>

<span data-ttu-id="501b8-128">명령줄에서 다음 명령을 사용하여 **WordCount**라는 Maven 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-128">From the command line, use the following command to create a Maven project named **WordCount**:</span></span>

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> <span data-ttu-id="501b8-129">PowerShell을 사용하는 경우 큰 따옴표로 `-D` 매개 변수를 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-129">If you are using PowerShell, you must surround the`-D` parameters with double quotes.</span></span>
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

<span data-ttu-id="501b8-130">이 명령은 기본 Maven 프로젝트를 포함하는 현재 위치에 `WordCount`라는 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-130">This command creates a directory named `WordCount` at the current location, which contains a basic Maven project.</span></span> <span data-ttu-id="501b8-131">`WordCount` 디렉터리에는 다음과 같은 항목이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-131">The `WordCount` directory contains the following items:</span></span>

* <span data-ttu-id="501b8-132">`pom.xml`: Maven 프로젝트에 대한 설정을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-132">`pom.xml`: Contains settings for the Maven project.</span></span>
* <span data-ttu-id="501b8-133">`src\main\java\com\microsoft\example`: 응용 프로그램 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-133">`src\main\java\com\microsoft\example`: Contains your application code.</span></span>
* <span data-ttu-id="501b8-134">`src\test\java\com\microsoft\example`: 응용 프로그램에 대한 테스트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-134">`src\test\java\com\microsoft\example`: Contains tests for your application.</span></span> 

### <a name="remove-the-generated-example-code"></a><span data-ttu-id="501b8-135">생성된 예제 코드 제거</span><span class="sxs-lookup"><span data-stu-id="501b8-135">Remove the generated example code</span></span>

<span data-ttu-id="501b8-136">생성된 테스트 및 응용 프로그램 파일을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-136">Delete the generated test and the application files:</span></span>

* <span data-ttu-id="501b8-137">**src\test\java\com\microsoft\example\AppTest.java**</span><span class="sxs-lookup"><span data-stu-id="501b8-137">**src\test\java\com\microsoft\example\AppTest.java**</span></span>
* <span data-ttu-id="501b8-138">**src\main\java\com\microsoft\example\App.java**</span><span class="sxs-lookup"><span data-stu-id="501b8-138">**src\main\java\com\microsoft\example\App.java**</span></span>

## <a name="add-maven-repositories"></a><span data-ttu-id="501b8-139">Maven 리포지토리 추가</span><span class="sxs-lookup"><span data-stu-id="501b8-139">Add Maven repositories</span></span>

<span data-ttu-id="501b8-140">HDInsight는 HDP(Hortonworks Data Platform)를 기반으로 하므로 Hortonworks 리포지토리를 사용하여 Apache Storm 프로젝트에 대한 종속성을 다운로드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-140">HDInsight is based on the Hortonworks Data Platform (HDP), so we recommend using the Hortonworks repository to download dependencies for your Apache Storm projects.</span></span> <span data-ttu-id="501b8-141">__pom.xml__ 파일에서 `<url>http://maven.apache.org</url>` 줄 뒤에 다음 XML을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-141">In the __pom.xml__ file, add the following XML after the `<url>http://maven.apache.org</url>` line:</span></span>

```xml
<repositories>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPReleases</id>
        <name>HDP Releases</name>
        <url>http://repo.hortonworks.com/content/repositories/releases/</url>
        <layout>default</layout>
    </repository>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPJetty</id>
        <name>Hadoop Jetty</name>
        <url>http://repo.hortonworks.com/content/repositories/jetty-hadoop/</url>
        <layout>default</layout>
    </repository>
</repositories>
```

## <a name="add-properties"></a><span data-ttu-id="501b8-142">속성 추가</span><span class="sxs-lookup"><span data-stu-id="501b8-142">Add properties</span></span>

<span data-ttu-id="501b8-143">Maven을 사용하면 속성이라고 하는 프로젝트 수준 값을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-143">Maven allows you to define project-level values called properties.</span></span> <span data-ttu-id="501b8-144">__pom.xml__에서 `</repositories>` 줄 뒤에 다음 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-144">In the __pom.xml__, add the following text after the `</repositories>` line:</span></span>

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from the Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

<span data-ttu-id="501b8-145">이제 `pom.xml`의 다른 섹션에서 이 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-145">You can now use this value in other sections of the `pom.xml`.</span></span> <span data-ttu-id="501b8-146">예를 들어 Storm 구성 요소의 버전을 지정할 때 값을 하드 코딩하는 대신 `${storm.version}`을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-146">For example, when specifying the version of Storm components, you can use `${storm.version}` instead of hard coding a value.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="501b8-147">종속성 추가</span><span class="sxs-lookup"><span data-stu-id="501b8-147">Add dependencies</span></span>

<span data-ttu-id="501b8-148">Storm 구성 요소에 대한 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-148">Add a dependency for Storm components.</span></span> <span data-ttu-id="501b8-149">`<dependencies>` 섹션에서 `pom.xml` 파일을 열고 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-149">Open the `pom.xml` file and add the following code in the `<dependencies>` section:</span></span>

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of the jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

<span data-ttu-id="501b8-150">컴파일 시간에 Maven은 이 정보를 사용하여 Maven 리포지토리에서 `storm-core`를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-150">At compile time, Maven uses this information to look up `storm-core` in the Maven repository.</span></span> <span data-ttu-id="501b8-151">먼저 로컬 컴퓨터의 리포지토리에서 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-151">It first looks in the repository on your local computer.</span></span> <span data-ttu-id="501b8-152">파일이 없으면 Maven은 공개 Maven 리포지토리에서 파일을 다운로드하여 로컬 리포지토리에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-152">If the files aren't there, Maven downloads them from the public Maven repository and stores them in the local repository.</span></span>

> [!NOTE]
> <span data-ttu-id="501b8-153">이 섹션에서 `<scope>provided</scope>` 줄을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-153">Notice the `<scope>provided</scope>` line in this section.</span></span> <span data-ttu-id="501b8-154">이 설정은 Maven이 만든 JAR 파일에서 **storm-core**를 제외하도록 요청합니다. 시스템을 통해 제공되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-154">This setting tells Maven to exclude **storm-core** from any JAR files that are created, because it is provided by the system.</span></span>

## <a name="build-configuration"></a><span data-ttu-id="501b8-155">빌드 구성</span><span class="sxs-lookup"><span data-stu-id="501b8-155">Build configuration</span></span>

<span data-ttu-id="501b8-156">Maven 플러그 인을 사용하면 프로젝트의 빌드 단계를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-156">Maven plug-ins allow you to customize the build stages of the project.</span></span> <span data-ttu-id="501b8-157">예를 들어 프로젝트 컴파일 방법 또는 JAR 파일로 패키지하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-157">For example, how the project is compiled or how to package it into a JAR file.</span></span> <span data-ttu-id="501b8-158">`pom.xml` 파일을 열고 `</project>` 줄 바로 위에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-158">Open the `pom.xml` file and add the following code directly above the `</project>` line.</span></span>

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

<span data-ttu-id="501b8-159">이 섹션은 플러그 인, 리소스 및 다른 빌드 구성 옵션을 추가하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-159">This section is used to add plug-ins, resources, and other build configuration options.</span></span> <span data-ttu-id="501b8-160">**pom.xml** 파일에 대한 전체 참조는 [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="501b8-160">For a full reference of the **pom.xml** file, see [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span></span>

### <a name="add-plug-ins"></a><span data-ttu-id="501b8-161">플러그 인 추가</span><span class="sxs-lookup"><span data-stu-id="501b8-161">Add plug-ins</span></span>

<span data-ttu-id="501b8-162">Java에서 구현된 Apache Storm 토폴로지의 경우 [Exec Maven 플러그 인](http://www.mojohaus.org/exec-maven-plugin/)을 사용하면 개발 환경에서 토폴로지를 로컬에서 쉽게 실행할 수 있어 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-162">For Apache Storm topologies implemented in Java, the [Exec Maven Plugin](http://www.mojohaus.org/exec-maven-plugin/) is useful because it allows you to easily run the topology locally in your development environment.</span></span> <span data-ttu-id="501b8-163">Exec Maven 플러그 인을 추가하려면 `pom.xml` 파일의 `<plugins>` 섹션에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-163">Add the following to the `<plugins>` section of the `pom.xml` file to include the Exec Maven plugin:</span></span>

```xml
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>exec-maven-plugin</artifactId>
    <version>1.4.0</version>
    <executions>
    <execution>
    <goals>
        <goal>exec</goal>
    </goals>
    </execution>
    </executions>
    <configuration>
    <executable>java</executable>
    <includeProjectDependencies>true</includeProjectDependencies>
    <includePluginDependencies>false</includePluginDependencies>
    <classpathScope>compile</classpathScope>
    <mainClass>${storm.topology}</mainClass>
    <cleanupDaemonThreads>false</cleanupDaemonThreads> 
    </configuration>
</plugin>
```

<span data-ttu-id="501b8-164">다른 유용한 플러그 인은 컴파일 옵션을 변경하는 데 사용되는 [Apache Maven 컴파일러 플러그 인](http://maven.apache.org/plugins/maven-compiler-plugin/)입니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-164">Another useful plug-in is the [Apache Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/), which is used to change compilation options.</span></span> <span data-ttu-id="501b8-165">사용자의 응용 프로그램에 대한 원본 및 대상에 Maven이 사용하는 Java 버전이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-165">The changes the Java version that Maven uses for the source and target for your application.</span></span>

* <span data-ttu-id="501b8-166">HDInsight __3.4 이하__의 경우 원본과 대상의 Java 버전을 __1.7__로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-166">For HDInsight __3.4 or earlier__, set the source and target Java version to __1.7__.</span></span>

* <span data-ttu-id="501b8-167">HDInsight __3.5__의 경우 원본과 대상의 Java 버전을 __1.8__로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-167">For HDInsight __3.5__, set the source and target Java version to __1.8__.</span></span>

<span data-ttu-id="501b8-168">Apache Maven Compiler 플러그 인을 포함하려면 `pom.xml` 파일의 `<plugins>` 섹션에 다음 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-168">Add the following text in the `<plugins>` section of the `pom.xml` file to include the Apache Maven Compiler plugin.</span></span> <span data-ttu-id="501b8-169">이 예에서는 1.8을 지정하므로 대상 HDInsight 버전은 3.5가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-169">This example specifies 1.8, so the target HDInsight version is 3.5.</span></span>

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.3</version>
    <configuration>
    <source>1.8</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

### <a name="configure-resources"></a><span data-ttu-id="501b8-170">리소스 구성</span><span class="sxs-lookup"><span data-stu-id="501b8-170">Configure resources</span></span>

<span data-ttu-id="501b8-171">리소스 섹션을 사용하면 토폴로지에 구성 요소에 필요한 구성 파일과 같은 비코드 리소스를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-171">The resources section allows you to include non-code resources such as configuration files needed by components in the topology.</span></span> <span data-ttu-id="501b8-172">이 예제에서는 `pom.xml 파일의 `<resources>\` 섹션 내에 다음 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-172">For this example, add the following text in the `<resources>` section of the \`pom.xml file.</span></span>

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

<span data-ttu-id="501b8-173">이 예제는 프로젝트의 루트에 있는 리소스 디렉터리(`${basedir}`)를 리소스를 포함하는 위치로 추가하고 `log4j2.xml`이라는 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-173">This example adds the resources directory in the root of the project (`${basedir}`) as a location that contains resources, and includes the file named `log4j2.xml`.</span></span> <span data-ttu-id="501b8-174">이 파일은 토폴로지에서 기록하는 정보를 구성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-174">This file is used to configure what information is logged by the topology.</span></span>

## <a name="create-the-topology"></a><span data-ttu-id="501b8-175">토폴로지 만들기</span><span class="sxs-lookup"><span data-stu-id="501b8-175">Create the topology</span></span>

<span data-ttu-id="501b8-176">Java 기반 Apache Storm 토폴로지는 사용자가 작성자이거나 종속성으로 참조되는 세 개의 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-176">A Java-based Apache Storm topology consists of three components that you must author (or reference) as a dependency.</span></span>

* <span data-ttu-id="501b8-177">**Spout**: 외부 소스에서 데이터를 읽고 데이터의 스트림을 토폴로지로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-177">**Spouts**: Reads data from external sources and emits streams of data into the topology.</span></span>

* <span data-ttu-id="501b8-178">**Bolt**: Spout 또는 다른 Bolt가 내보낸 스트림에서 처리를 수행하고 하나 이상의 스트림을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-178">**Bolts**: Performs processing on streams emitted by spouts or other bolts, and emits one or more streams.</span></span>

* <span data-ttu-id="501b8-179">**토폴로지**: Spout 및 Bolt 배열 방식을 정의하고 토폴로지에 대한 진입점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-179">**Topology**: Defines how the spouts and bolts are arranged, and provides the entry point for the topology.</span></span>

### <a name="create-the-spout"></a><span data-ttu-id="501b8-180">Spout 만들기</span><span class="sxs-lookup"><span data-stu-id="501b8-180">Create the spout</span></span>

<span data-ttu-id="501b8-181">외부 데이터 소스 설정에 대한 요구를 줄이기 위해 다음 spout가 임의의 문장을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-181">To reduce requirements for setting up external data sources, the following spout simply emits random sentences.</span></span> <span data-ttu-id="501b8-182">이는 [Storm-Starter 예제](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter)와 함께 제공된 Spout의 수정된 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-182">It is a modified version of a spout that is provided with the [Storm-Starter examples](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span></span>

> [!NOTE]
> <span data-ttu-id="501b8-183">외부 데이터 소스에서 읽는 Spout의 예는 다음 예제 중 하나를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="501b8-183">For an example of a spout that reads from an external data source, see one of the following examples:</span></span>
>
> * <span data-ttu-id="501b8-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): Twitter에서 읽는 예제 Spout</span><span class="sxs-lookup"><span data-stu-id="501b8-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): An example spout that reads from Twitter</span></span>
> * <span data-ttu-id="501b8-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): Kafka에서 읽는 Spout</span><span class="sxs-lookup"><span data-stu-id="501b8-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): A spout that reads from Kafka</span></span>

<span data-ttu-id="501b8-186">Spout의 경우 `src\main\java\com\microsoft\example` 디렉터리에 `RandomSentenceSpout.java`라는 파일을 만들고 다음 Java 코드를 그 콘텐츠로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-186">For the spout, create a file named `RandomSentenceSpout.java` in the `src\main\java\com\microsoft\example` directory and use the following Java code as the contents:</span></span>

```java
package com.microsoft.example;

import org.apache.storm.spout.SpoutOutputCollector;
import org.apache.storm.task.TopologyContext;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseRichSpout;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Values;
import org.apache.storm.utils.Utils;

import java.util.Map;
import java.util.Random;

//This spout randomly emits sentences
public class RandomSentenceSpout extends BaseRichSpout {
  //Collector used to emit output
  SpoutOutputCollector _collector;
  //Used to generate a random number
  Random _rand;

  //Open is called when an instance of the class is created
  @Override
  public void open(Map conf, TopologyContext context, SpoutOutputCollector collector) {
  //Set the instance collector to the one passed in
    _collector = collector;
    //For randomness
    _rand = new Random();
  }

  //Emit data to the stream
  @Override
  public void nextTuple() {
  //Sleep for a bit
    Utils.sleep(100);
    //The sentences that are randomly emitted
    String[] sentences = new String[]{ "the cow jumped over the moon", "an apple a day keeps the doctor away",
        "four score and seven years ago", "snow white and the seven dwarfs", "i am at two with nature" };
    //Randomly pick a sentence
    String sentence = sentences[_rand.nextInt(sentences.length)];
    //Emit the sentence
    _collector.emit(new Values(sentence));
  }

  //Ack is not implemented since this is a basic example
  @Override
  public void ack(Object id) {
  }

  //Fail is not implemented since this is a basic example
  @Override
  public void fail(Object id) {
  }

  //Declare the output fields. In this case, an sentence
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("sentence"));
  }
}
```

> [!NOTE]
> <span data-ttu-id="501b8-187">이 토폴로지는 하나의 spout만 사용하지만 다른 토폴로지는 다른 소스에서 해당 토폴로지로 데이터를 피드하는 여러 spout를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-187">Although this topology uses only one spout, others may have several that feed data from different sources into the topology.</span></span>

### <a name="create-the-bolts"></a><span data-ttu-id="501b8-188">Bolt 만들기</span><span class="sxs-lookup"><span data-stu-id="501b8-188">Create the bolts</span></span>

<span data-ttu-id="501b8-189">Bolt는 데이터 처리를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-189">Bolts handle the data processing.</span></span> <span data-ttu-id="501b8-190">이 토폴로지는 두 개의 bolt를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-190">This topology uses two bolts:</span></span>

* <span data-ttu-id="501b8-191">**SplitSentence**: **RandomSentenceSpout**를 통해 내보낸 문장을 개별 단어로 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-191">**SplitSentence**: Splits the sentences emitted by **RandomSentenceSpout** into individual words.</span></span>

* <span data-ttu-id="501b8-192">**WordCount**: 각각의 단어가 발생한 횟수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-192">**WordCount**: Counts how many times each word has occurred.</span></span>

> [!NOTE]
> <span data-ttu-id="501b8-193">Bolt는 계산, 지속성, 외부 구성 요소에 말하기 등 모든 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-193">Bolts can do anything, for example, computation, persistence, or talking to external components.</span></span>

<span data-ttu-id="501b8-194">`src\main\java\com\microsoft\example` 디렉터리에서 두 개의 새 파일인 `SplitSentence.java` 및 `WordCount.java`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-194">Create two new files, `SplitSentence.java` and `WordCount.java` in the `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="501b8-195">파일 내용으로 다음 텍스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-195">Use the following text as the contents for the files:</span></span>

#### <a name="splitsentence"></a><span data-ttu-id="501b8-196">SplitSentence</span><span class="sxs-lookup"><span data-stu-id="501b8-196">SplitSentence</span></span>

```java
package com.microsoft.example;

import java.text.BreakIterator;

import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class SplitSentence extends BaseBasicBolt {

  //Execute is called to process tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //Get the sentence content from the tuple
    String sentence = tuple.getString(0);
    //An iterator to get each word
    BreakIterator boundary=BreakIterator.getWordInstance();
    //Give the iterator the sentence
    boundary.setText(sentence);
    //Find the beginning first word
    int start=boundary.first();
    //Iterate over each word and emit it to the output stream
    for (int end=boundary.next(); end != BreakIterator.DONE; start=end, end=boundary.next()) {
      //get the word
      String word=sentence.substring(start,end);
      //If a word is whitespace characters, replace it with empty
      word=word.replaceAll("\\s+","");
      //if it's an actual word, emit it
      if (!word.equals("")) {
        collector.emit(new Values(word));
      }
    }
  }

  //Declare that emitted tuples contain a word field
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word"));
  }
}
```

#### <a name="wordcount"></a><span data-ttu-id="501b8-197">WordCount</span><span class="sxs-lookup"><span data-stu-id="501b8-197">WordCount</span></span>

```java
package com.microsoft.example;

import java.util.HashMap;
import java.util.Map;
import java.util.Iterator;

import org.apache.storm.Constants;
import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;
import org.apache.storm.Config;

// For logging
import org.apache.logging.log4j.Logger;
import org.apache.logging.log4j.LogManager;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class WordCount extends BaseBasicBolt {
  //Create logger for this class
  private static final Logger logger = LogManager.getLogger(WordCount.class);
  //For holding words and counts
  Map<String, Integer> counts = new HashMap<String, Integer>();
  //How often to emit a count of words
  private Integer emitFrequency;

  // Default constructor
  public WordCount() {
      emitFrequency=5; // Default to 60 seconds
  }

  // Constructor that sets emit frequency
  public WordCount(Integer frequency) {
      emitFrequency=frequency;
  }

  //Configure frequency of tick tuples for this bolt
  //This delivers a 'tick' tuple on a specific interval,
  //which is used to trigger certain actions
  @Override
  public Map<String, Object> getComponentConfiguration() {
      Config conf = new Config();
      conf.put(Config.TOPOLOGY_TICK_TUPLE_FREQ_SECS, emitFrequency);
      return conf;
  }

  //execute is called to process tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //If it's a tick tuple, emit all words and counts
    if(tuple.getSourceComponent().equals(Constants.SYSTEM_COMPONENT_ID)
            && tuple.getSourceStreamId().equals(Constants.SYSTEM_TICK_STREAM_ID)) {
      for(String word : counts.keySet()) {
        Integer count = counts.get(word);
        collector.emit(new Values(word, count));
        logger.info("Emitting a count of " + count + " for word " + word);
      }
    } else {
      //Get the word contents from the tuple
      String word = tuple.getString(0);
      //Have we counted any already?
      Integer count = counts.get(word);
      if (count == null)
        count = 0;
      //Increment the count and store it
      count++;
      counts.put(word, count);
    }
  }

  //Declare that this emits a tuple containing two fields; word and count
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word", "count"));
  }
}
```

### <a name="define-the-topology"></a><span data-ttu-id="501b8-198">토폴로지 정의</span><span class="sxs-lookup"><span data-stu-id="501b8-198">Define the topology</span></span>

<span data-ttu-id="501b8-199">토폴로지는 spout 및 bolt를 그래프로 묶습니다. 이 그래프는 구성 요소 사이의 데이터 흐름 방식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-199">The topology ties the spouts and bolts together into a graph, which defines how data flows between the components.</span></span> <span data-ttu-id="501b8-200">Storm이 클러스터 내에서 구성 요소의 인스턴스를 만들 대 사용하는 병렬 처리 힌트도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-200">It also provides parallelism hints that Storm uses when creating instances of the components within the cluster.</span></span>

<span data-ttu-id="501b8-201">다음 이미지는 이 토폴로지에 대한 구성 요소 그래프의 기본 다이어그램입니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-201">The following image is a basic diagram of the graph of components for this topology.</span></span>

![Spout 및 Bolt 배열을 보여 주는 다이어그램](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

<span data-ttu-id="501b8-203">토폴로지를 구현하려면 `src\main\java\com\microsoft\example` 디렉터리에서 `WordCountTopology.java`라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-203">To implement the topology, create a file named `WordCountTopology.java` in the `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="501b8-204">파일의 콘텐츠로 다음 Java 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-204">Use the following Java code as the contents of the file:</span></span>

```java
package com.microsoft.example;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.StormSubmitter;
import org.apache.storm.topology.TopologyBuilder;
import org.apache.storm.tuple.Fields;

import com.microsoft.example.RandomSentenceSpout;

public class WordCountTopology {

  //Entry point for the topology
  public static void main(String[] args) throws Exception {
  //Used to build the topology
    TopologyBuilder builder = new TopologyBuilder();
    //Add the spout, with a name of 'spout'
    //and parallelism hint of 5 executors
    builder.setSpout("spout", new RandomSentenceSpout(), 5);
    //Add the SplitSentence bolt, with a name of 'split'
    //and parallelism hint of 8 executors
    //shufflegrouping subscribes to the spout, and equally distributes
    //tuples (sentences) across instances of the SplitSentence bolt
    builder.setBolt("split", new SplitSentence(), 8).shuffleGrouping("spout");
    //Add the counter, with a name of 'count'
    //and parallelism hint of 12 executors
    //fieldsgrouping subscribes to the split bolt, and
    //ensures that the same word is sent to the same instance (group by field 'word')
    builder.setBolt("count", new WordCount(), 12).fieldsGrouping("split", new Fields("word"));

    //new configuration
    Config conf = new Config();
    //Set to false to disable debug information when
    // running in production on a cluster
    conf.setDebug(false);

    //If there are arguments, we are running on a cluster
    if (args != null && args.length > 0) {
      //parallelism hint to set the number of workers
      conf.setNumWorkers(3);
      //submit the topology
      StormSubmitter.submitTopology(args[0], conf, builder.createTopology());
    }
    //Otherwise, we are running locally
    else {
      //Cap the maximum number of executors that can be spawned
      //for a component to 3
      conf.setMaxTaskParallelism(3);
      //LocalCluster is used to run locally
      LocalCluster cluster = new LocalCluster();
      //submit the topology
      cluster.submitTopology("word-count", conf, builder.createTopology());
      //sleep
      Thread.sleep(10000);
      //shut down the cluster
      cluster.shutdown();
    }
  }
}
```

### <a name="configure-logging"></a><span data-ttu-id="501b8-205">로깅 구성</span><span class="sxs-lookup"><span data-stu-id="501b8-205">Configure logging</span></span>

<span data-ttu-id="501b8-206">Storm은 Apache Log4j를 사용하여 정보를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-206">Storm uses Apache Log4j to log information.</span></span> <span data-ttu-id="501b8-207">로깅을 구성하지 않으면 토폴로지는 진단 정보를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-207">If you do not configure logging, the topology emits diagnostic information.</span></span> <span data-ttu-id="501b8-208">로깅되는 내용을 제어하려면 `resources` 디렉터리에서 `log4j2.xml`이라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-208">To control what is logged, create a file named `log4j2.xml` in the `resources` directory.</span></span> <span data-ttu-id="501b8-209">파일 콘텐츠로 다음 XML을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-209">Use the following XML as the contents of the file.</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration>
<Appenders>
    <Console name="STDOUT" target="SYSTEM_OUT">
        <PatternLayout pattern="%d{HH:mm:ss} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
</Appenders>
<Loggers>
    <Logger name="com.microsoft.example" level="trace" additivity="false">
        <AppenderRef ref="STDOUT"/>
    </Logger>
    <Root level="error">
        <Appender-Ref ref="STDOUT"/>
    </Root>
</Loggers>
</Configuration>
```

<span data-ttu-id="501b8-210">이 XML은 이 예제 토폴로지의 구성 요소를 포함하는 `com.microsoft.example` 클래스에 대한 새 로거를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-210">This XML configures a new logger for the `com.microsoft.example` class, which includes the components in this example topology.</span></span> <span data-ttu-id="501b8-211">수준은 이 로거에 대한 추적으로 설정되며, 이 토폴로지의 구성 요소에서 내보낸 모든 로깅 정보가 캡처됩니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-211">The level is set to trace for this logger, which captures any logging information emitted by components in this topology.</span></span>

<span data-ttu-id="501b8-212">`<Root level="error">` 섹션은 루트 수준의 로깅(모든 항목이 `com.microsoft.example`에 있지는 않음)을 오류 정보를 기록하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-212">The `<Root level="error">` section configures the root level of logging (everything not in `com.microsoft.example`) to only log error information.</span></span>

<span data-ttu-id="501b8-213">Log4j에 대한 로깅 구성과 관련된 자세한 내용은 [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="501b8-213">For more information on configuring logging for Log4j, see [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span></span>

> [!NOTE]
> <span data-ttu-id="501b8-214">Storm 버전 0.10.0 이상은 Log4j 2.x를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-214">Storm version 0.10.0 and higher use Log4j 2.x.</span></span> <span data-ttu-id="501b8-215">이전 버전의 Storm은 로그 구성에 다른 형식을 사용하는 Log4j 1.x를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-215">Older versions of storm used Log4j 1.x, which used a different format for log configuration.</span></span> <span data-ttu-id="501b8-216">이전 구성에 대한 자세한 내용은 [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="501b8-216">For information on the older configuration, see [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span></span>

## <a name="test-the-topology-locally"></a><span data-ttu-id="501b8-217">로컬에서 토폴로지 테스트</span><span class="sxs-lookup"><span data-stu-id="501b8-217">Test the topology locally</span></span>

<span data-ttu-id="501b8-218">파일을 저장한 후 다음 명령을 사용하여 토폴로지를 로컬로 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-218">After you save the files, use the following command to test the topology locally.</span></span>

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

<span data-ttu-id="501b8-219">실행할 때 토폴로지가 시작 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-219">As it runs, the topology displays startup information.</span></span> <span data-ttu-id="501b8-220">다음 텍스트는 단어 개수 출력의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-220">The following text is an example of the word count output:</span></span>

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

<span data-ttu-id="501b8-221">이 예제 로그는 단어 ‘and’가 113번 내보내졌음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-221">This example log indicates that the word 'and' has been emitted 113 times.</span></span> <span data-ttu-id="501b8-222">Spout가 계속해서 동일한 문장을 내보내기 때문에 토폴로지를 실행하면 개수는 계속 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-222">The count continues to go up as long as the topology runs because the spout continuously emits the same sentences.</span></span>

<span data-ttu-id="501b8-223">단어 내보내기와 개수 사이에는 5초의 간격이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-223">There is a 5-second interval between emission of words and counts.</span></span> <span data-ttu-id="501b8-224">**WordCount** 구성 요소는 틱 튜플이 도착할 때 정보만 내보내도록 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-224">The **WordCount** component is configured to only emit information when a tick tuple arrives.</span></span> <span data-ttu-id="501b8-225">틱 튜플은 5초마다 배달되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-225">It requests that tick tuples are only delivered every five seconds.</span></span>

## <a name="convert-the-topology-to-flux"></a><span data-ttu-id="501b8-226">토폴로지를 Flux로 변환</span><span class="sxs-lookup"><span data-stu-id="501b8-226">Convert the topology to Flux</span></span>

<span data-ttu-id="501b8-227">Flux는 Storm 0.10.0 이상에서 사용할 수 있는 새로운 프레임워크로서 구성을 구현과 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-227">Flux is a new framework available with Storm 0.10.0 and higher, which allows you to separate configuration from implementation.</span></span> <span data-ttu-id="501b8-228">구성 요소가 여전히 Java로 정의되지만 토폴로지는 YAML 파일을 사용하여 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-228">Your components are still defined in Java, but the topology is defined using a YAML file.</span></span> <span data-ttu-id="501b8-229">프로젝트를 통해 기본 토폴로지 정의를 패키지하거나 토폴로지를 제출할 때 독립 실행형 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-229">You can package a default topology definition with your project, or use a standalone file when submitting the topology.</span></span> <span data-ttu-id="501b8-230">Storm에 토폴로지를 제출할 때 환경 변수 또는 구성 파일을 사용하여 YAML 토폴로지 정의에서 값을 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-230">When submitting the topology to Storm, you can use environment variables or configuration files to populate values in the YAML topology definition.</span></span>

<span data-ttu-id="501b8-231">YAML 파일은 토폴로지 및 구성 요소 간 데이터 흐름에 사용할 구성 요소를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-231">The YAML file defines the components to use for the topology and the data flow between them.</span></span> <span data-ttu-id="501b8-232">jar 파일의 일부로 YAML 파일을 포함하거나 외부 YAML 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-232">You can include a YAML file as part of the jar file or you can use an external YAML file.</span></span>

<span data-ttu-id="501b8-233">Flux에 대한 자세한 내용은 [Flux 프레임워크(https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="501b8-233">For more information on Flux, see [Flux framework (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

> [!WARNING]
> <span data-ttu-id="501b8-234">Storm 1.0.1의 [버그(https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055)로 인해 [Storm 개발 환경](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)을 설치하여 Flux 토폴로지를 로컬로 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-234">Due to a [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) with Storm 1.0.1, you may need to install a [Storm development environment](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) to run Flux topologies locally.</span></span>

1. <span data-ttu-id="501b8-235">`WordCountTopology.java` 파일을 프로젝트에서 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-235">Move the `WordCountTopology.java` file out of the project.</span></span> <span data-ttu-id="501b8-236">이전에 이 파일은 토폴로지를 정의했지만 Flux에는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-236">Previously, this file defined the topology, but isn't needed with Flux.</span></span>

2. <span data-ttu-id="501b8-237">`resources` 디렉터리에서 `topology.yaml`라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-237">In the `resources` directory, create a file named `topology.yaml`.</span></span> <span data-ttu-id="501b8-238">이 파일의 내용으로 다음 텍스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-238">Use the following text as the contents of this file.</span></span>

        name: "wordcount"       # friendly name for the topology
        
        config:                 # Topology configuration
        topology.workers: 1     # Hint for the number of workers to create
        
        spouts:                 # Spout definitions
        - id: "sentence-spout"
            className: "com.microsoft.example.RandomSentenceSpout"
            parallelism: 1      # parallelism hint
        
        bolts:                  # Bolt definitions
        - id: "splitter-bolt"
            className: "com.microsoft.example.SplitSentence"
            parallelism: 1
         
        - id: "counter-bolt"
            className: "com.microsoft.example.WordCount"
            constructorArgs:
                - 10
            parallelism: 1
        
        streams:                # Stream definitions
            - name: "Spout --> Splitter" # name isn't used (placeholder for logging, UI, etc.)
            from: "sentence-spout"       # The stream emitter
            to: "splitter-bolt"          # The stream consumer
            grouping:                    # Grouping type
                type: SHUFFLE
          
            - name: "Splitter -> Counter"
            from: "splitter-bolt"
            to: "counter-bolt"
            grouping:
            type: FIELDS
                args: ["word"]           # field(s) to group on

3. <span data-ttu-id="501b8-239">`pom.xml` 파일을 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-239">Make the following changes to the `pom.xml` file.</span></span>
   
   * <span data-ttu-id="501b8-240">`<dependencies>` 섹션에서 다음 새 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-240">Add the following new dependency in the `<dependencies>` section:</span></span>
     
        ```xml
        <!-- Add a dependency on the Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * <span data-ttu-id="501b8-241">`<plugins>` 섹션에 다음 플러그 인을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-241">Add the following plugin to the `<plugins>` section.</span></span> <span data-ttu-id="501b8-242">이 플러그 인은 프로젝트에 대한 패키지(jar 파일)를 만들도록 처리하고 패키지를 만들 때 Flux에 특정된 일부 변환을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-242">This plugin handles the creation of a package (jar file) for the project, and applies some transformations specific to Flux when creating the package.</span></span>
     
        ```xml
        <!-- build an uber jar -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
                <transformers>
                    <!-- Keep us from getting a "can't overwrite file error" -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer" />
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer" />
                    <!-- We're using Flux, so refer to it as main -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                        <mainClass>org.apache.storm.flux.Flux</mainClass>
                    </transformer>
                </transformers>
                <!-- Keep us from getting a bad signature error -->
                <filters>
                    <filter>
                        <artifact>*:*</artifact>
                        <excludes>
                            <exclude>META-INF/*.SF</exclude>
                            <exclude>META-INF/*.DSA</exclude>
                            <exclude>META-INF/*.RSA</exclude>
                        </excludes>
                    </filter>
                </filters>
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
        ```

   * <span data-ttu-id="501b8-243">**exec-maven-plugin** `<configuration>` 섹션에서 `<mainClass>` 값을 `org.apache.storm.flux.Flux`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-243">In the **exec-maven-plugin** `<configuration>` section, change the value for `<mainClass>` to `org.apache.storm.flux.Flux`.</span></span> <span data-ttu-id="501b8-244">이 설정을 통해 Flux가 개발 중에 로컬로 토폴로지 실행을 처리하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-244">This setting allows Flux to handle running the topology locally in development.</span></span>

   * <span data-ttu-id="501b8-245">`<resources>` 섹션의 `<includes>`에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-245">In the `<resources>` section, add the following to the `<includes>`.</span></span> <span data-ttu-id="501b8-246">이 XML에는 토폴로지를 프로젝트의 일환으로 정의하는 YAML 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-246">This XML includes the YAML file that defines the topology as part of the project.</span></span>

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-the-flux-topology-locally"></a><span data-ttu-id="501b8-247">로컬에서 Flux 토폴로지 테스트</span><span class="sxs-lookup"><span data-stu-id="501b8-247">Test the flux topology locally</span></span>

1. <span data-ttu-id="501b8-248">Maven을 사용하여 Flux 토폴로지를 컴파일하고 실행하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-248">Use the following to compile and execute the Flux topology using Maven:</span></span>

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    <span data-ttu-id="501b8-249">PowerShell을 사용하는 경우 다음 명령을 대신 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-249">If you are using PowerShell, use the following command:</span></span>

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > <span data-ttu-id="501b8-250">토폴로지가 Storm 1.0.1 비트를 사용하는 경우 이 명령은 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-250">If your topology uses Storm 1.0.1 bits, this command fails.</span></span> <span data-ttu-id="501b8-251">이 문제는 [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055)로 인해 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-251">This failure is caused by [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span></span> <span data-ttu-id="501b8-252">대신, [개발 환경에서 Storm을 설치](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html)하고 다음 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-252">Instead, [install Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) and use the following information.</span></span>

    <span data-ttu-id="501b8-253">[개발 환경에서 Storm을 설치](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html)한 경우 다음 명령을 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-253">If you have [installed Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), you can use the following commands instead:</span></span>

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    <span data-ttu-id="501b8-254">`--local` 매개 변수는 개발 환경에서 토폴로지를 로컬 모드로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-254">The `--local` parameter runs the topology in local mode on your development environment.</span></span> <span data-ttu-id="501b8-255">`-R /topology.yaml` 매개 변수는 jar 파일에서 `topology.yaml` 파일 리소스를 사용하여 토폴로지를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-255">The `-R /topology.yaml` parameter uses the `topology.yaml` file resource from the jar file to define the topology.</span></span>

    <span data-ttu-id="501b8-256">실행할 때 토폴로지가 시작 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-256">As it runs, the topology displays startup information.</span></span> <span data-ttu-id="501b8-257">다음 텍스트는 출력의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-257">The following text is an example of the output:</span></span>

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    <span data-ttu-id="501b8-258">기록된 정보 배치 간에 10초의 지연이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-258">There is a 10-second delay between batches of logged information.</span></span>

2. <span data-ttu-id="501b8-259">프로젝트에서 `topology.yaml` 파일의 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-259">Make a copy of the `topology.yaml` file from the project.</span></span> <span data-ttu-id="501b8-260">새 파일의 이름을 `newtopology.yaml`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-260">Name the new file `newtopology.yaml`.</span></span> <span data-ttu-id="501b8-261">`newtopology.yaml` 파일에서 다음 섹션을 찾고 `10` 값을 `5`으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-261">In the `newtopology.yaml` file, find the following section and change the value of `10` to `5`.</span></span> <span data-ttu-id="501b8-262">이렇게 수정하면 단어 수의 배치를 내보내는 간격이 10초에서 5초로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-262">This modification changes the interval between emitting batches of word counts from 10 seconds to 5.</span></span>

    ```yaml
    - id: "counter-bolt"
    className: "com.microsoft.example.WordCount"
    constructorArgs:
    - 5
    parallelism: 1
    ```yaml

3. To run the topology, use the following command:

    ```bash
    mvn exec:java -Dexec.args="--local /path/to/newtopology.yaml"
    ```

    <span data-ttu-id="501b8-263">또는 개발 환경에서 Storm을 설치한 경우:</span><span class="sxs-lookup"><span data-stu-id="501b8-263">Or, if you have Storm on your development environment:</span></span>

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    <span data-ttu-id="501b8-264">`/path/to/newtopology.yaml`을 이전 단계에서 만든 newtopology.yaml 파일의 경로로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-264">Change the `/path/to/newtopology.yaml` to the path to the newtopology.yaml file you created in the previous step.</span></span> <span data-ttu-id="501b8-265">이 명령은 newtopology.yaml을 토폴로지 정의로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-265">This command uses the newtopology.yaml as the topology definition.</span></span> <span data-ttu-id="501b8-266">`compile` 매개 변수를 포함하지 않았기 때문에 Maven은 이전 단계에서 빌드한 프로젝트의 버전을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-266">Since we didn't include the `compile` parameter, Maven uses the version of the project built in previous steps.</span></span>

    <span data-ttu-id="501b8-267">토폴로지가 시작되면 내보낸 배치 간의 간격이 newtopology.yaml에 있는 값을 반영하도록 변경되었다는 점에 유의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-267">Once the topology starts, you should notice that the time between emitted batches has changed to reflect the value in newtopology.yaml.</span></span> <span data-ttu-id="501b8-268">따라서 토폴로지를 다시 컴파일하지 않고도 YAML 파일을 통해 구성을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-268">So you can see that you can change your configuration through a YAML file without having to recompile the topology.</span></span>

<span data-ttu-id="501b8-269">Flux 프레임워크의 다른 기능에 대한 자세한 내용은 [Flux(https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="501b8-269">For more information on these and other features of the Flux framework, see [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

## <a name="trident"></a><span data-ttu-id="501b8-270">Trident</span><span class="sxs-lookup"><span data-stu-id="501b8-270">Trident</span></span>

<span data-ttu-id="501b8-271">Trident는 Storm에서 제공하는 높은 수준의 추상화이며</span><span class="sxs-lookup"><span data-stu-id="501b8-271">Trident is a high-level abstraction that is provided by Storm.</span></span> <span data-ttu-id="501b8-272">상태 저장 처리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-272">It supports stateful processing.</span></span> <span data-ttu-id="501b8-273">Trident의 주요 이점은 토폴로지가 입력하는 모든 메시지가 한 번만 처리된다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-273">The primary advantage of Trident is that it can guarantee that every message that enters the topology is processed only once.</span></span> <span data-ttu-id="501b8-274">Trident를 사용하지 않으면 토폴로지는 메시지가 최소한 한 번은 처리된다는 것만 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-274">Without using Trident, your topology can only guarantee that messages are processed at least once.</span></span> <span data-ttu-id="501b8-275">Bolt를 만드는 대신 사용할 수 있는 기본 제공 구성 요소와 같은 다른 차이점도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-275">There are also other differences, such as built-in components that can be used instead of creating bolts.</span></span> <span data-ttu-id="501b8-276">사실 Bolt는 필터, 프로젝션 및 함수와 같이 덜 일반적인 구성 요소로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-276">In fact, bolts are replaced by less-generic components, such as filters, projections, and functions.</span></span>

<span data-ttu-id="501b8-277">Trident 응용 프로그램은 Maven 프로젝트를 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-277">Trident applications can be created by using Maven projects.</span></span> <span data-ttu-id="501b8-278">이 문서의 앞부분에 제공된 것과 동일한 기본 단계를 거치며 코드만 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-278">You use the same basic steps as presented earlier in this article—only the code is different.</span></span> <span data-ttu-id="501b8-279">Trident도 현재 Flux 프레임워크에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-279">Trident also cannot (currently) be used with the Flux framework.</span></span>

<span data-ttu-id="501b8-280">Trident에 대한 자세한 내용은 [Trident API 개요](http://storm.apache.org/documentation/Trident-API-Overview.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="501b8-280">For more information about Trident, see the [Trident API Overview](http://storm.apache.org/documentation/Trident-API-Overview.html).</span></span>

<span data-ttu-id="501b8-281">Trident 응용 프로그램 예제는 [HDInsight에서 Apache Storm을 사용하는 Twitter 추세 항목](hdinsight-storm-twitter-trending.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="501b8-281">For an example of a Trident application, see [Twitter trending topics with Apache Storm on HDInsight](hdinsight-storm-twitter-trending.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="501b8-282">다음 단계</span><span class="sxs-lookup"><span data-stu-id="501b8-282">Next Steps</span></span>

<span data-ttu-id="501b8-283">Java를 사용하여 Storm 토폴로지를 만드는 방법을 배웠으므로</span><span class="sxs-lookup"><span data-stu-id="501b8-283">You have learned how to create a Storm topology by using Java.</span></span> <span data-ttu-id="501b8-284">이제 다음으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="501b8-284">Now learn how to:</span></span>

* [<span data-ttu-id="501b8-285">HDInsight에서 Apache Storm 토폴로지 배포 및 관리</span><span class="sxs-lookup"><span data-stu-id="501b8-285">Deploy and manage Apache Storm topologies on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)

* [<span data-ttu-id="501b8-286">Visual Studio를 사용하여 HDInsight에서 Apache Storm에 대한 C# 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="501b8-286">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="501b8-287">Storm 토폴로지에 대한 추가 예제는 [HDInsight의 Storm에 대한 예제 토폴로지](hdinsight-storm-example-topology.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="501b8-287">You can find more example Storm topologies by visiting [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

