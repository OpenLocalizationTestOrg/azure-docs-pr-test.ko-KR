---
title: "Azure HDInsight aaaApache 스톰 Java 토폴로지 예제-| Microsoft Docs"
description: "Java 예제 word 만들어 toocreate Apache Storm 토폴로지에 토폴로지를 계산 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 54fa9dc3c93ddad83ac861f3101f50f80117d804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-storm-topology-in-java"></a><span data-ttu-id="7bc21-104">Java에서 Apache Storm 토폴로지 만들기</span><span class="sxs-lookup"><span data-stu-id="7bc21-104">Create an Apache Storm topology in Java</span></span>

<span data-ttu-id="7bc21-105">자세한 내용은 방법 toocreate Apache Storm의 Java 기반 토폴로지입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-105">Learn how toocreate a Java-based topology for Apache Storm.</span></span> <span data-ttu-id="7bc21-106">단어 계산 응용 프로그램을 구현하는 Storm 토폴로지를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-106">You create a Storm topology that implements a word-count application.</span></span> <span data-ttu-id="7bc21-107">Maven toobuild 및 패키지 hello 프로젝트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-107">You use Maven toobuild and package hello project.</span></span> <span data-ttu-id="7bc21-108">그런 다음 어떻게 결정 프레임 워크를 사용 하 여 toodefine hello 토폴로지 hello 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-108">Then, you learn how toodefine hello topology using hello Flux framework.</span></span>

> [!NOTE]
> <span data-ttu-id="7bc21-109">hello 표적이 프레임 워크 이상 스톰 0.10.0에서에서 사용할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-109">hello Flux framework is available in Storm 0.10.0 or later.</span></span> <span data-ttu-id="7bc21-110">Storm 0.10.0은 HDInsight 3.3 및 3.4에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-110">Storm 0.10.0 is available with HDInsight 3.3 and 3.4.</span></span>

<span data-ttu-id="7bc21-111">이 문서의 hello 단계를 완료 한 후 hello 토폴로지 tooApache 스톰 HDInsight에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-111">After completing hello steps in this document, you can deploy hello topology tooApache Storm on HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="7bc21-112">이 문서에서 만든 hello 스톰 토폴로지 예제의 전체 버전에서 제공 됩니다. [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-112">A completed version of hello Storm topology examples created in this document is available at [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7bc21-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7bc21-113">Prerequisites</span></span>

* [<span data-ttu-id="7bc21-114">JDK(Java Developer Kit) 버전 7</span><span class="sxs-lookup"><span data-stu-id="7bc21-114">Java Developer Kit (JDK) version 7</span></span>](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* <span data-ttu-id="7bc21-115">[Maven(https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Java 프로젝트를 위한 프로젝트 빌드 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="7bc21-116">텍스트 편집기 또는 IDE</span><span class="sxs-lookup"><span data-stu-id="7bc21-116">A text editor or IDE.</span></span>

## <a name="configure-environment-variables"></a><span data-ttu-id="7bc21-117">환경 변수 구성</span><span class="sxs-lookup"><span data-stu-id="7bc21-117">Configure environment variables</span></span>

<span data-ttu-id="7bc21-118">hello 다음과 같은 환경 변수 설정 되어 있습니다 Java 및 hello JDK 설치.</span><span class="sxs-lookup"><span data-stu-id="7bc21-118">hello following environment variables may be set when you install Java and hello JDK.</span></span> <span data-ttu-id="7bc21-119">그러나 시스템에 대 한 올바른 값 hello를 포함 하 고 있는 것을 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-119">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="7bc21-120">**JAVA_HOME** -toohello hello Java runtime environment (JRE)가 설치 디렉터리를 가리켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-120">**JAVA_HOME** - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="7bc21-121">예를 들어, Unix 또는 Linux 배포 없어야과 유사한 값 너무`/usr/lib/jvm/java-7-oracle`합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-121">For example, in a Unix or Linux distribution, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="7bc21-122">Windows에서 동일 하 게과 유사한 값 너무`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="7bc21-122">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="7bc21-123">**경로** -hello 다음 경로 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-123">**PATH** - should contain hello following paths:</span></span>

  * <span data-ttu-id="7bc21-124">**JAVA_HOME** (또는 hello 해당 하는 경로)</span><span class="sxs-lookup"><span data-stu-id="7bc21-124">**JAVA_HOME** (or hello equivalent path)</span></span>

  * <span data-ttu-id="7bc21-125">**JAVA_HOME\bin** (또는 hello 해당 하는 경로)</span><span class="sxs-lookup"><span data-stu-id="7bc21-125">**JAVA_HOME\bin** (or hello equivalent path)</span></span>

  * <span data-ttu-id="7bc21-126">Maven 설치 되어 있는 hello 디렉터리</span><span class="sxs-lookup"><span data-stu-id="7bc21-126">hello directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="7bc21-127">Maven 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="7bc21-127">Create a Maven project</span></span>

<span data-ttu-id="7bc21-128">Hello 명령줄에서 사용 하 여 hello 다음 명령은 toocreate 라는 Maven 프로젝트가 **WordCount**:</span><span class="sxs-lookup"><span data-stu-id="7bc21-128">From hello command line, use hello following command toocreate a Maven project named **WordCount**:</span></span>

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> <span data-ttu-id="7bc21-129">PowerShell을 사용하는 경우 큰 따옴표로 `-D` 매개 변수를 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-129">If you are using PowerShell, you must surround the`-D` parameters with double quotes.</span></span>
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

<span data-ttu-id="7bc21-130">이 명령은 라는 디렉터리를 만듭니다. `WordCount` 기본 Maven 프로젝트를 포함 하는 hello 현재 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-130">This command creates a directory named `WordCount` at hello current location, which contains a basic Maven project.</span></span> <span data-ttu-id="7bc21-131">hello `WordCount` hello 다음 항목을 포함 하는 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="7bc21-131">hello `WordCount` directory contains hello following items:</span></span>

* <span data-ttu-id="7bc21-132">`pom.xml`: Hello Maven 프로젝트에 대 한 설정을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-132">`pom.xml`: Contains settings for hello Maven project.</span></span>
* <span data-ttu-id="7bc21-133">`src\main\java\com\microsoft\example`: 응용 프로그램 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-133">`src\main\java\com\microsoft\example`: Contains your application code.</span></span>
* <span data-ttu-id="7bc21-134">`src\test\java\com\microsoft\example`: 응용 프로그램에 대한 테스트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-134">`src\test\java\com\microsoft\example`: Contains tests for your application.</span></span> 

### <a name="remove-hello-generated-example-code"></a><span data-ttu-id="7bc21-135">예제 코드를 생성 하는 hello 제거</span><span class="sxs-lookup"><span data-stu-id="7bc21-135">Remove hello generated example code</span></span>

<span data-ttu-id="7bc21-136">생성 된 hello 테스트 및 hello 응용 프로그램 파일을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-136">Delete hello generated test and hello application files:</span></span>

* <span data-ttu-id="7bc21-137">**src\test\java\com\microsoft\example\AppTest.java**</span><span class="sxs-lookup"><span data-stu-id="7bc21-137">**src\test\java\com\microsoft\example\AppTest.java**</span></span>
* <span data-ttu-id="7bc21-138">**src\main\java\com\microsoft\example\App.java**</span><span class="sxs-lookup"><span data-stu-id="7bc21-138">**src\main\java\com\microsoft\example\App.java**</span></span>

## <a name="add-maven-repositories"></a><span data-ttu-id="7bc21-139">Maven 리포지토리 추가</span><span class="sxs-lookup"><span data-stu-id="7bc21-139">Add Maven repositories</span></span>

<span data-ttu-id="7bc21-140">HDInsight는 hello Hortonworks Data Platform (HDP)에 기반 하므로 Apache Storm 프로젝트에 대 한 hello Hortonworks 리포지토리 toodownload 종속성을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-140">HDInsight is based on hello Hortonworks Data Platform (HDP), so we recommend using hello Hortonworks repository toodownload dependencies for your Apache Storm projects.</span></span> <span data-ttu-id="7bc21-141">Hello에 __pom.xml__ 파일에서 다음과 같은 XML hello 후 hello 추가 `<url>http://maven.apache.org</url>` 줄:</span><span class="sxs-lookup"><span data-stu-id="7bc21-141">In hello __pom.xml__ file, add hello following XML after hello `<url>http://maven.apache.org</url>` line:</span></span>

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

## <a name="add-properties"></a><span data-ttu-id="7bc21-142">속성 추가</span><span class="sxs-lookup"><span data-stu-id="7bc21-142">Add properties</span></span>

<span data-ttu-id="7bc21-143">Maven 속성 이라는 toodefine 프로젝트 수준 값을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-143">Maven allows you toodefine project-level values called properties.</span></span> <span data-ttu-id="7bc21-144">Hello에 __pom.xml__, hello 텍스트 hello 후 다음 추가 `</repositories>` 줄:</span><span class="sxs-lookup"><span data-stu-id="7bc21-144">In hello __pom.xml__, add hello following text after hello `</repositories>` line:</span></span>

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from hello Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

<span data-ttu-id="7bc21-145">이제 hello의 다른 섹션에서이 값을 사용할 수 `pom.xml`합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-145">You can now use this value in other sections of hello `pom.xml`.</span></span> <span data-ttu-id="7bc21-146">예를 들어 hello 버전의 Storm 구성 요소를 지정할 때는 사용할 수 있습니다 `${storm.version}` 하드 코딩 된 값 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-146">For example, when specifying hello version of Storm components, you can use `${storm.version}` instead of hard coding a value.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="7bc21-147">종속성 추가</span><span class="sxs-lookup"><span data-stu-id="7bc21-147">Add dependencies</span></span>

<span data-ttu-id="7bc21-148">Storm 구성 요소에 대한 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-148">Add a dependency for Storm components.</span></span> <span data-ttu-id="7bc21-149">열기 hello `pom.xml` 파일 및 코드 hello에 다음 hello 추가 `<dependencies>` 섹션:</span><span class="sxs-lookup"><span data-stu-id="7bc21-149">Open hello `pom.xml` file and add hello following code in hello `<dependencies>` section:</span></span>

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of hello jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

<span data-ttu-id="7bc21-150">컴파일 타임에 Maven 소진이 정보 toolook `storm-core` hello Maven 리포지토리에 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-150">At compile time, Maven uses this information toolook up `storm-core` in hello Maven repository.</span></span> <span data-ttu-id="7bc21-151">먼저 로컬 컴퓨터에 대 한 hello 리포지토리에 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-151">It first looks in hello repository on your local computer.</span></span> <span data-ttu-id="7bc21-152">Hello 파일 반영 되지 않을, Maven hello 공개 Maven 저장소에서 다운로드 hello 로컬 저장소에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-152">If hello files aren't there, Maven downloads them from hello public Maven repository and stores them in hello local repository.</span></span>

> [!NOTE]
> <span data-ttu-id="7bc21-153">공지 hello `<scope>provided</scope>` 줄이이 섹션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-153">Notice hello `<scope>provided</scope>` line in this section.</span></span> <span data-ttu-id="7bc21-154">이 설정은 Maven tooexclude를 알려 줍니다. **스톰 코어** hello 시스템에서 제공 되기 때문에 생성 된 JAR 파일에서입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-154">This setting tells Maven tooexclude **storm-core** from any JAR files that are created, because it is provided by hello system.</span></span>

## <a name="build-configuration"></a><span data-ttu-id="7bc21-155">빌드 구성</span><span class="sxs-lookup"><span data-stu-id="7bc21-155">Build configuration</span></span>

<span data-ttu-id="7bc21-156">Maven 플러그 인을 사용 하면 hello 프로젝트의 toocustomize hello 빌드 단계 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-156">Maven plug-ins allow you toocustomize hello build stages of hello project.</span></span> <span data-ttu-id="7bc21-157">Hello 프로젝트 컴파일 방식을 예를 들어 방식이 나 toopackage JAR 파일을 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-157">For example, how hello project is compiled or how toopackage it into a JAR file.</span></span> <span data-ttu-id="7bc21-158">열기 hello `pom.xml` 파일 및 코드 hello 바로 위에 다음 hello 추가 `</project>` 선입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-158">Open hello `pom.xml` file and add hello following code directly above hello `</project>` line.</span></span>

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

<span data-ttu-id="7bc21-159">이 섹션에 사용 되는 tooadd 플러그 인, 리소스 및 기타 빌드 구성 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-159">This section is used tooadd plug-ins, resources, and other build configuration options.</span></span> <span data-ttu-id="7bc21-160">전체 참조의 hello **pom.xml** 파일, 참조 [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-160">For a full reference of hello **pom.xml** file, see [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span></span>

### <a name="add-plug-ins"></a><span data-ttu-id="7bc21-161">플러그 인 추가</span><span class="sxs-lookup"><span data-stu-id="7bc21-161">Add plug-ins</span></span>

<span data-ttu-id="7bc21-162">Java에서 구현 되는 Apache Storm 토폴로지, hello [Exec Maven 플러그 인](http://www.mojohaus.org/exec-maven-plugin/) tooeasily 개발 환경에서 hello 토폴로지를 로컬로 실행할 수 있기 때문에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-162">For Apache Storm topologies implemented in Java, hello [Exec Maven Plugin](http://www.mojohaus.org/exec-maven-plugin/) is useful because it allows you tooeasily run hello topology locally in your development environment.</span></span> <span data-ttu-id="7bc21-163">Hello toohello 다음 추가 `<plugins>` hello 섹션 `pom.xml` tooinclude hello Exec Maven 플러그 인 파일:</span><span class="sxs-lookup"><span data-stu-id="7bc21-163">Add hello following toohello `<plugins>` section of hello `pom.xml` file tooinclude hello Exec Maven plugin:</span></span>

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

<span data-ttu-id="7bc21-164">유용한 다른 플러그 인은 hello [Apache Maven 컴파일러 플러그 인](http://maven.apache.org/plugins/maven-compiler-plugin/), 어떤가 사용 되는 toochange 컴파일 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-164">Another useful plug-in is hello [Apache Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/), which is used toochange compilation options.</span></span> <span data-ttu-id="7bc21-165">hello 변경 hello Maven hello 원본과 응용 프로그램에 대 한 대상에 대 한 사용 하는 Java 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-165">hello changes hello Java version that Maven uses for hello source and target for your application.</span></span>

* <span data-ttu-id="7bc21-166">HDInsight에 대 한 __3.4 또는 이전 버전__hello 소스 설정, 및 Java 버전 too__1.7__ 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-166">For HDInsight __3.4 or earlier__, set hello source and target Java version too__1.7__.</span></span>

* <span data-ttu-id="7bc21-167">HDInsight에 대 한 __3.5__hello 소스 설정, 및 Java 버전 too__1.8__ 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-167">For HDInsight __3.5__, set hello source and target Java version too__1.8__.</span></span>

<span data-ttu-id="7bc21-168">Hello hello에서 텍스트 다음 추가 `<plugins>` hello 섹션 `pom.xml` tooinclude hello Apache Maven 컴파일러 플러그 인 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-168">Add hello following text in hello `<plugins>` section of hello `pom.xml` file tooinclude hello Apache Maven Compiler plugin.</span></span> <span data-ttu-id="7bc21-169">이 예에서는 hello 대상 HDInsight 버전은 3.5 1.8을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-169">This example specifies 1.8, so hello target HDInsight version is 3.5.</span></span>

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

### <a name="configure-resources"></a><span data-ttu-id="7bc21-170">리소스 구성</span><span class="sxs-lookup"><span data-stu-id="7bc21-170">Configure resources</span></span>

<span data-ttu-id="7bc21-171">hello 리소스 섹션 hello 토폴로지의 구성 요소에 필요한 구성 파일과 같은 tooinclude 비 코드 리소스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-171">hello resources section allows you tooinclude non-code resources such as configuration files needed by components in hello topology.</span></span> <span data-ttu-id="7bc21-172">예를 들어 hello hello에서 텍스트 다음 추가 `<resources>` hello 섹션 ' pom.xml 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-172">For this example, add hello following text in hello `<resources>` section of hello \`pom.xml file.</span></span>

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

<span data-ttu-id="7bc21-173">Hello 프로젝트의 hello 루트에서 hello resources 디렉터리를 추가 하는이 예제 (`${basedir}`) 리소스를 포함 하 고 라는 hello 파일을 포함 한 위치로 `log4j2.xml`합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-173">This example adds hello resources directory in hello root of hello project (`${basedir}`) as a location that contains resources, and includes hello file named `log4j2.xml`.</span></span> <span data-ttu-id="7bc21-174">이 파일은 hello 토폴로지에서 정보를 기록 하는 사용 되는 tooconfigure 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-174">This file is used tooconfigure what information is logged by hello topology.</span></span>

## <a name="create-hello-topology"></a><span data-ttu-id="7bc21-175">Hello 토폴로지 만들기</span><span class="sxs-lookup"><span data-stu-id="7bc21-175">Create hello topology</span></span>

<span data-ttu-id="7bc21-176">Java 기반 Apache Storm 토폴로지는 사용자가 작성자이거나 종속성으로 참조되는 세 개의 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-176">A Java-based Apache Storm topology consists of three components that you must author (or reference) as a dependency.</span></span>

* <span data-ttu-id="7bc21-177">**Spouts**: 외부에서 데이터 원본 및 데이터 스트림을 hello 토폴로지 내보냅니다 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-177">**Spouts**: Reads data from external sources and emits streams of data into hello topology.</span></span>

* <span data-ttu-id="7bc21-178">**Bolt**: Spout 또는 다른 Bolt가 내보낸 스트림에서 처리를 수행하고 하나 이상의 스트림을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-178">**Bolts**: Performs processing on streams emitted by spouts or other bolts, and emits one or more streams.</span></span>

* <span data-ttu-id="7bc21-179">**토폴로지**: 및 방법을 정의 hello spouts 볼트 정리 되 고 hello 토폴로지에 대 한 hello 진입점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-179">**Topology**: Defines how hello spouts and bolts are arranged, and provides hello entry point for hello topology.</span></span>

### <a name="create-hello-spout"></a><span data-ttu-id="7bc21-180">Hello 배출구 만들기</span><span class="sxs-lookup"><span data-stu-id="7bc21-180">Create hello spout</span></span>

<span data-ttu-id="7bc21-181">다음 외부 데이터 소스를 설정 하기 위한 요구 사항 tooreduce hello 배출구 단순히 임의의 문장을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-181">tooreduce requirements for setting up external data sources, hello following spout simply emits random sentences.</span></span> <span data-ttu-id="7bc21-182">Hello로 제공 되는 배출구의 수정 된 버전이 [스톰 스타터 예제](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-182">It is a modified version of a spout that is provided with hello [Storm-Starter examples](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span></span>

> [!NOTE]
> <span data-ttu-id="7bc21-183">외부 데이터 원본에서 읽는 배출구의 예 예제 따르는 hello 중 하나를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-183">For an example of a spout that reads from an external data source, see one of hello following examples:</span></span>
>
> * <span data-ttu-id="7bc21-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): Twitter에서 읽는 예제 Spout</span><span class="sxs-lookup"><span data-stu-id="7bc21-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): An example spout that reads from Twitter</span></span>
> * <span data-ttu-id="7bc21-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): Kafka에서 읽는 Spout</span><span class="sxs-lookup"><span data-stu-id="7bc21-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): A spout that reads from Kafka</span></span>

<span data-ttu-id="7bc21-186">Hello 배출구 라는 파일을 만들 `RandomSentenceSpout.java` hello에 `src\main\java\com\microsoft\example` Java 코드를 hello 내용으로 다음 디렉터리 및 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="7bc21-186">For hello spout, create a file named `RandomSentenceSpout.java` in hello `src\main\java\com\microsoft\example` directory and use hello following Java code as hello contents:</span></span>

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
  //Collector used tooemit output
  SpoutOutputCollector _collector;
  //Used toogenerate a random number
  Random _rand;

  //Open is called when an instance of hello class is created
  @Override
  public void open(Map conf, TopologyContext context, SpoutOutputCollector collector) {
  //Set hello instance collector toohello one passed in
    _collector = collector;
    //For randomness
    _rand = new Random();
  }

  //Emit data toohello stream
  @Override
  public void nextTuple() {
  //Sleep for a bit
    Utils.sleep(100);
    //hello sentences that are randomly emitted
    String[] sentences = new String[]{ "hello cow jumped over hello moon", "an apple a day keeps hello doctor away",
        "four score and seven years ago", "snow white and hello seven dwarfs", "i am at two with nature" };
    //Randomly pick a sentence
    String sentence = sentences[_rand.nextInt(sentences.length)];
    //Emit hello sentence
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

  //Declare hello output fields. In this case, an sentence
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("sentence"));
  }
}
```

> [!NOTE]
> <span data-ttu-id="7bc21-187">이 토폴로지 하나만 배출구를 사용 하지만 다른 hello 토폴로지에 서로 다른 원본의 데이터를 공급 하는 몇 가지 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-187">Although this topology uses only one spout, others may have several that feed data from different sources into hello topology.</span></span>

### <a name="create-hello-bolts"></a><span data-ttu-id="7bc21-188">Hello 볼트 만들기</span><span class="sxs-lookup"><span data-stu-id="7bc21-188">Create hello bolts</span></span>

<span data-ttu-id="7bc21-189">볼트 hello 데이터 처리를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-189">Bolts handle hello data processing.</span></span> <span data-ttu-id="7bc21-190">이 토폴로지는 두 개의 bolt를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-190">This topology uses two bolts:</span></span>

* <span data-ttu-id="7bc21-191">**SplitSentence**: hello 문장에서 내보낸 분할 **RandomSentenceSpout** 개별 단어로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-191">**SplitSentence**: Splits hello sentences emitted by **RandomSentenceSpout** into individual words.</span></span>

* <span data-ttu-id="7bc21-192">**WordCount**: 각각의 단어가 발생한 횟수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-192">**WordCount**: Counts how many times each word has occurred.</span></span>

> [!NOTE]
> <span data-ttu-id="7bc21-193">볼트 것, 예를 들어, 계산, 저장, 또는 tooexternal 구성 요소와 통신 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-193">Bolts can do anything, for example, computation, persistence, or talking tooexternal components.</span></span>

<span data-ttu-id="7bc21-194">두 개의 새 파일 만들기 `SplitSentence.java` 및 `WordCount.java` hello에 `src\main\java\com\microsoft\example` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-194">Create two new files, `SplitSentence.java` and `WordCount.java` in hello `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="7bc21-195">Hello 콘텐츠로 사용 hello 파일에 대 한 텍스트를 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-195">Use hello following text as hello contents for hello files:</span></span>

#### <a name="splitsentence"></a><span data-ttu-id="7bc21-196">SplitSentence</span><span class="sxs-lookup"><span data-stu-id="7bc21-196">SplitSentence</span></span>

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

  //Execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //Get hello sentence content from hello tuple
    String sentence = tuple.getString(0);
    //An iterator tooget each word
    BreakIterator boundary=BreakIterator.getWordInstance();
    //Give hello iterator hello sentence
    boundary.setText(sentence);
    //Find hello beginning first word
    int start=boundary.first();
    //Iterate over each word and emit it toohello output stream
    for (int end=boundary.next(); end != BreakIterator.DONE; start=end, end=boundary.next()) {
      //get hello word
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

#### <a name="wordcount"></a><span data-ttu-id="7bc21-197">WordCount</span><span class="sxs-lookup"><span data-stu-id="7bc21-197">WordCount</span></span>

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
  //How often tooemit a count of words
  private Integer emitFrequency;

  // Default constructor
  public WordCount() {
      emitFrequency=5; // Default too60 seconds
  }

  // Constructor that sets emit frequency
  public WordCount(Integer frequency) {
      emitFrequency=frequency;
  }

  //Configure frequency of tick tuples for this bolt
  //This delivers a 'tick' tuple on a specific interval,
  //which is used tootrigger certain actions
  @Override
  public Map<String, Object> getComponentConfiguration() {
      Config conf = new Config();
      conf.put(Config.TOPOLOGY_TICK_TUPLE_FREQ_SECS, emitFrequency);
      return conf;
  }

  //execute is called tooprocess tuples
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
      //Get hello word contents from hello tuple
      String word = tuple.getString(0);
      //Have we counted any already?
      Integer count = counts.get(word);
      if (count == null)
        count = 0;
      //Increment hello count and store it
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

### <a name="define-hello-topology"></a><span data-ttu-id="7bc21-198">Hello 토폴로지 정의</span><span class="sxs-lookup"><span data-stu-id="7bc21-198">Define hello topology</span></span>

<span data-ttu-id="7bc21-199">hello 토폴로지 hello spouts 연결 및 hello 구성 요소 간 데이터 흐름 방식을 정의 하는 그래프로 함께 쐐기 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-199">hello topology ties hello spouts and bolts together into a graph, which defines how data flows between hello components.</span></span> <span data-ttu-id="7bc21-200">또한 스톰 hello 클러스터 내에서 hello 구성 요소의 인스턴스를 만들 때 사용 되는 병렬 처리 수준 힌트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-200">It also provides parallelism hints that Storm uses when creating instances of hello components within hello cluster.</span></span>

<span data-ttu-id="7bc21-201">hello 다음 그림은이 토폴로지에 대 한 구성 요소의 hello 그래프의 기본 다이어그램.</span><span class="sxs-lookup"><span data-stu-id="7bc21-201">hello following image is a basic diagram of hello graph of components for this topology.</span></span>

![다이어그램 보여 주는 hello spouts 및 쐐기 정렬](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

<span data-ttu-id="7bc21-203">tooimplement 토폴로지 hello, 라는 파일을 만들어 `WordCountTopology.java` hello에 `src\main\java\com\microsoft\example` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-203">tooimplement hello topology, create a file named `WordCountTopology.java` in hello `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="7bc21-204">Hello 파일의 내용을 hello로 Java 코드를 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-204">Use hello following Java code as hello contents of hello file:</span></span>

```java
package com.microsoft.example;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.StormSubmitter;
import org.apache.storm.topology.TopologyBuilder;
import org.apache.storm.tuple.Fields;

import com.microsoft.example.RandomSentenceSpout;

public class WordCountTopology {

  //Entry point for hello topology
  public static void main(String[] args) throws Exception {
  //Used toobuild hello topology
    TopologyBuilder builder = new TopologyBuilder();
    //Add hello spout, with a name of 'spout'
    //and parallelism hint of 5 executors
    builder.setSpout("spout", new RandomSentenceSpout(), 5);
    //Add hello SplitSentence bolt, with a name of 'split'
    //and parallelism hint of 8 executors
    //shufflegrouping subscribes toohello spout, and equally distributes
    //tuples (sentences) across instances of hello SplitSentence bolt
    builder.setBolt("split", new SplitSentence(), 8).shuffleGrouping("spout");
    //Add hello counter, with a name of 'count'
    //and parallelism hint of 12 executors
    //fieldsgrouping subscribes toohello split bolt, and
    //ensures that hello same word is sent toohello same instance (group by field 'word')
    builder.setBolt("count", new WordCount(), 12).fieldsGrouping("split", new Fields("word"));

    //new configuration
    Config conf = new Config();
    //Set toofalse toodisable debug information when
    // running in production on a cluster
    conf.setDebug(false);

    //If there are arguments, we are running on a cluster
    if (args != null && args.length > 0) {
      //parallelism hint tooset hello number of workers
      conf.setNumWorkers(3);
      //submit hello topology
      StormSubmitter.submitTopology(args[0], conf, builder.createTopology());
    }
    //Otherwise, we are running locally
    else {
      //Cap hello maximum number of executors that can be spawned
      //for a component too3
      conf.setMaxTaskParallelism(3);
      //LocalCluster is used toorun locally
      LocalCluster cluster = new LocalCluster();
      //submit hello topology
      cluster.submitTopology("word-count", conf, builder.createTopology());
      //sleep
      Thread.sleep(10000);
      //shut down hello cluster
      cluster.shutdown();
    }
  }
}
```

### <a name="configure-logging"></a><span data-ttu-id="7bc21-205">로깅 구성</span><span class="sxs-lookup"><span data-stu-id="7bc21-205">Configure logging</span></span>

<span data-ttu-id="7bc21-206">Storm은 Apache Log4j toolog 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-206">Storm uses Apache Log4j toolog information.</span></span> <span data-ttu-id="7bc21-207">로깅을 구성 하지 않으면 hello 토폴로지 진단 정보를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-207">If you do not configure logging, hello topology emits diagnostic information.</span></span> <span data-ttu-id="7bc21-208">기록 된 값, toocontrol 라는 파일을 만들어 `log4j2.xml` hello에 `resources` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-208">toocontrol what is logged, create a file named `log4j2.xml` in hello `resources` directory.</span></span> <span data-ttu-id="7bc21-209">Hello hello 파일의 내용을 hello로 다음과 같은 XML을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-209">Use hello following XML as hello contents of hello file.</span></span>

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

<span data-ttu-id="7bc21-210">이 XML 구성 hello에 대 한 새로운 로거가 `com.microsoft.example` 토폴로지가 예제에 hello 구성 요소를 포함 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-210">This XML configures a new logger for hello `com.microsoft.example` class, which includes hello components in this example topology.</span></span> <span data-ttu-id="7bc21-211">hello 수준은이 토폴로지의 구성 요소에서 내보낸 모든 로깅 정보를 캡처하고이 거에 대 한 tootrace를 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-211">hello level is set tootrace for this logger, which captures any logging information emitted by components in this topology.</span></span>

<span data-ttu-id="7bc21-212">hello `<Root level="error">` 섹션 hello 루트 수준의 로깅 구성 (모든 항목에 속하지 않은 `com.microsoft.example`) tooonly 로그 오류 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-212">hello `<Root level="error">` section configures hello root level of logging (everything not in `com.microsoft.example`) tooonly log error information.</span></span>

<span data-ttu-id="7bc21-213">Log4j에 대한 로깅 구성과 관련된 자세한 내용은 [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7bc21-213">For more information on configuring logging for Log4j, see [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span></span>

> [!NOTE]
> <span data-ttu-id="7bc21-214">Storm 버전 0.10.0 이상은 Log4j 2.x를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-214">Storm version 0.10.0 and higher use Log4j 2.x.</span></span> <span data-ttu-id="7bc21-215">이전 버전의 Storm은 로그 구성에 다른 형식을 사용하는 Log4j 1.x를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-215">Older versions of storm used Log4j 1.x, which used a different format for log configuration.</span></span> <span data-ttu-id="7bc21-216">Hello 오래 된 구성에 대 한 자세한 내용은 참조 하십시오. [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-216">For information on hello older configuration, see [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span></span>

## <a name="test-hello-topology-locally"></a><span data-ttu-id="7bc21-217">로컬로 테스트 hello 토폴로지</span><span class="sxs-lookup"><span data-stu-id="7bc21-217">Test hello topology locally</span></span>

<span data-ttu-id="7bc21-218">Hello 파일을 저장 한 후 다음 명령을 로컬로 토폴로지 tootest hello hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-218">After you save hello files, use hello following command tootest hello topology locally.</span></span>

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

<span data-ttu-id="7bc21-219">이 실행 될 때 hello 토폴로지 시작 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-219">As it runs, hello topology displays startup information.</span></span> <span data-ttu-id="7bc21-220">hello 다음 텍스트는 hello 단어 개수 출력 예입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-220">hello following text is an example of hello word count output:</span></span>

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

<span data-ttu-id="7bc21-221">이 예에서는 로그 hello 단어 ' 나타내고 ' 113 번 내보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-221">This example log indicates that hello word 'and' has been emitted 113 times.</span></span> <span data-ttu-id="7bc21-222">hello 수가 계속 해 서 toogo를 hello 배출구 hello를 지속적으로 내보내는 hello 토폴로지 실행으로 같은 문장입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-222">hello count continues toogo up as long as hello topology runs because hello spout continuously emits hello same sentences.</span></span>

<span data-ttu-id="7bc21-223">단어 내보내기와 개수 사이에는 5초의 간격이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-223">There is a 5-second interval between emission of words and counts.</span></span> <span data-ttu-id="7bc21-224">hello **WordCount** 구성 요소가 구성 되어 tooonly 눈금 튜플 도착할 때 정보를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-224">hello **WordCount** component is configured tooonly emit information when a tick tuple arrives.</span></span> <span data-ttu-id="7bc21-225">틱 튜플은 5초마다 배달되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-225">It requests that tick tuples are only delivered every five seconds.</span></span>

## <a name="convert-hello-topology-tooflux"></a><span data-ttu-id="7bc21-226">Hello 토폴로지 tooFlux 변환</span><span class="sxs-lookup"><span data-stu-id="7bc21-226">Convert hello topology tooFlux</span></span>

<span data-ttu-id="7bc21-227">결정은 새 프레임 워크 스톰 0.10.0 사용할 수 있는 이상 구현에서 tooseparate 구성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-227">Flux is a new framework available with Storm 0.10.0 and higher, which allows you tooseparate configuration from implementation.</span></span> <span data-ttu-id="7bc21-228">구성 요소 Java에 여전히 정의 되어 있지만 YAML 파일을 사용 하 여 hello 토폴로지를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-228">Your components are still defined in Java, but hello topology is defined using a YAML file.</span></span> <span data-ttu-id="7bc21-229">프로젝트에서 기본 토폴로지 정의 패키지 하거나 hello 토폴로지를 전송할 때 독립 실행형 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-229">You can package a default topology definition with your project, or use a standalone file when submitting hello topology.</span></span> <span data-ttu-id="7bc21-230">Hello 토폴로지 tooStorm를 전송할 때 hello YAML 토폴로지 정의의 환경 변수 또는 구성 파일 toopopulate 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-230">When submitting hello topology tooStorm, you can use environment variables or configuration files toopopulate values in hello YAML topology definition.</span></span>

<span data-ttu-id="7bc21-231">hello YAML 파일 hello 토폴로지 및 서로 hello 데이터 흐름에 대 한 구성 요소 toouse hello를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-231">hello YAML file defines hello components toouse for hello topology and hello data flow between them.</span></span> <span data-ttu-id="7bc21-232">Hello jar 파일의 일부로 YAML 파일을 포함할 수 있습니다 또는 외부 YAML 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-232">You can include a YAML file as part of hello jar file or you can use an external YAML file.</span></span>

<span data-ttu-id="7bc21-233">Flux에 대한 자세한 내용은 [Flux 프레임워크(https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7bc21-233">For more information on Flux, see [Flux framework (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

> [!WARNING]
> <span data-ttu-id="7bc21-234">기한 tooa [버그 (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) 1.0.1 스톰 tooinstall을 할 수 있습니다는 [스톰 개발 환경](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) toorun 표적이 토폴로지 로컬로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-234">Due tooa [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) with Storm 1.0.1, you may need tooinstall a [Storm development environment](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) toorun Flux topologies locally.</span></span>

1. <span data-ttu-id="7bc21-235">Hello 이동 `WordCountTopology.java` hello 프로젝트에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-235">Move hello `WordCountTopology.java` file out of hello project.</span></span> <span data-ttu-id="7bc21-236">이전에이 파일 hello 토폴로지 정의 되지만 결정으로 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-236">Previously, this file defined hello topology, but isn't needed with Flux.</span></span>

2. <span data-ttu-id="7bc21-237">Hello에 `resources` 디렉터리 라는 파일을 만들어 `topology.yaml`합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-237">In hello `resources` directory, create a file named `topology.yaml`.</span></span> <span data-ttu-id="7bc21-238">이 파일의 내용에 hello 텍스트를 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-238">Use hello following text as hello contents of this file.</span></span>

        name: "wordcount"       # friendly name for hello topology
        
        config:                 # Topology configuration
        topology.workers: 1     # Hint for hello number of workers toocreate
        
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
            from: "sentence-spout"       # hello stream emitter
            to: "splitter-bolt"          # hello stream consumer
            grouping:                    # Grouping type
                type: SHUFFLE
          
            - name: "Splitter -> Counter"
            from: "splitter-bolt"
            to: "counter-bolt"
            grouping:
            type: FIELDS
                args: ["word"]           # field(s) toogroup on

3. <span data-ttu-id="7bc21-239">다음 변경 내용을 toohello hello 확인 `pom.xml` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-239">Make hello following changes toohello `pom.xml` file.</span></span>
   
   * <span data-ttu-id="7bc21-240">Hello에 대 한 새 종속성을 따라 hello 추가 `<dependencies>` 섹션:</span><span class="sxs-lookup"><span data-stu-id="7bc21-240">Add hello following new dependency in hello `<dependencies>` section:</span></span>
     
        ```xml
        <!-- Add a dependency on hello Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * <span data-ttu-id="7bc21-241">플러그 인 toohello 다음 hello 추가 `<plugins>` 섹션.</span><span class="sxs-lookup"><span data-stu-id="7bc21-241">Add hello following plugin toohello `<plugins>` section.</span></span> <span data-ttu-id="7bc21-242">이 플러그 인 hello 프로젝트에 대 한 패키지 (jar 파일)의 hello 생성을 처리 하 고 hello 패키지를 만들 때 일부 변환 특정 tooFlux를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-242">This plugin handles hello creation of a package (jar file) for hello project, and applies some transformations specific tooFlux when creating hello package.</span></span>
     
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
                    <!-- We're using Flux, so refer tooit as main -->
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

   * <span data-ttu-id="7bc21-243">Hello에 **플러그 인 maven-exec-** `<configuration>` 섹션에 대 한 hello 값을 변경 하세요 `<mainClass>` 너무`org.apache.storm.flux.Flux`합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-243">In hello **exec-maven-plugin** `<configuration>` section, change hello value for `<mainClass>` too`org.apache.storm.flux.Flux`.</span></span> <span data-ttu-id="7bc21-244">이 설정을 통해 결정 toohandle 개발에서 hello 토폴로지를 로컬로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-244">This setting allows Flux toohandle running hello topology locally in development.</span></span>

   * <span data-ttu-id="7bc21-245">Hello에 `<resources>` 섹션을 따라 toohello hello 추가 `<includes>`합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-245">In hello `<resources>` section, add hello following toohello `<includes>`.</span></span> <span data-ttu-id="7bc21-246">이 XML hello 프로젝트의 일부로 hello 토폴로지를 정의 하는 hello YAML 파일에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-246">This XML includes hello YAML file that defines hello topology as part of hello project.</span></span>

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-hello-flux-topology-locally"></a><span data-ttu-id="7bc21-247">로컬로 hello 표적이 토폴로지를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-247">Test hello flux topology locally</span></span>

1. <span data-ttu-id="7bc21-248">다음 toocompile hello를 사용 하 고 Maven을 사용 하 여 hello 표적이 토폴로지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-248">Use hello following toocompile and execute hello Flux topology using Maven:</span></span>

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    <span data-ttu-id="7bc21-249">PowerShell을 사용 하는 경우 다음 명령을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-249">If you are using PowerShell, use hello following command:</span></span>

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > <span data-ttu-id="7bc21-250">토폴로지가 Storm 1.0.1 비트를 사용하는 경우 이 명령은 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-250">If your topology uses Storm 1.0.1 bits, this command fails.</span></span> <span data-ttu-id="7bc21-251">이 문제는 [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055)로 인해 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-251">This failure is caused by [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span></span> <span data-ttu-id="7bc21-252">대신, [스톰 개발 환경에서 설치](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) 다음 정보를 사용 하 여 hello 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-252">Instead, [install Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) and use hello following information.</span></span>

    <span data-ttu-id="7bc21-253">있는 경우 [스톰 개발 환경에 설치](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), hello 명령 대신 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-253">If you have [installed Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), you can use hello following commands instead:</span></span>

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    <span data-ttu-id="7bc21-254">hello `--local` 매개 변수 개발 환경에서 로컬 모드에서 hello 토폴로지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-254">hello `--local` parameter runs hello topology in local mode on your development environment.</span></span> <span data-ttu-id="7bc21-255">hello `-R /topology.yaml` hello를 사용 하는 매개 변수 `topology.yaml` hello jar 파일 toodefine hello 토폴로지에서 리소스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-255">hello `-R /topology.yaml` parameter uses hello `topology.yaml` file resource from hello jar file toodefine hello topology.</span></span>

    <span data-ttu-id="7bc21-256">이 실행 될 때 hello 토폴로지 시작 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-256">As it runs, hello topology displays startup information.</span></span> <span data-ttu-id="7bc21-257">hello 텍스트 다음은 hello 출력의 예:</span><span class="sxs-lookup"><span data-stu-id="7bc21-257">hello following text is an example of hello output:</span></span>

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    <span data-ttu-id="7bc21-258">기록된 정보 배치 간에 10초의 지연이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-258">There is a 10-second delay between batches of logged information.</span></span>

2. <span data-ttu-id="7bc21-259">Hello의 사본을 `topology.yaml` hello 프로젝트에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-259">Make a copy of hello `topology.yaml` file from hello project.</span></span> <span data-ttu-id="7bc21-260">새 파일 이름 hello `newtopology.yaml`합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-260">Name hello new file `newtopology.yaml`.</span></span> <span data-ttu-id="7bc21-261">Hello에 `newtopology.yaml` 파일을 찾아 hello 다음 섹션의 값을 hello 변경 `10` 너무`5`합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-261">In hello `newtopology.yaml` file, find hello following section and change hello value of `10` too`5`.</span></span> <span data-ttu-id="7bc21-262">10 초 too5에서이 수정 변경 내용을 hello 간격 표시 하 고 word의 일괄 처리 사이 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-262">This modification changes hello interval between emitting batches of word counts from 10 seconds too5.</span></span>

    ```yaml
    - id: "counter-bolt"
    className: "com.microsoft.example.WordCount"
    constructorArgs:
    - 5
    parallelism: 1
    ```yaml

3. toorun hello topology, use hello following command:

    ```bash
    mvn exec:java -Dexec.args="--local /path/to/newtopology.yaml"
    ```

    <span data-ttu-id="7bc21-263">또는 개발 환경에서 Storm을 설치한 경우:</span><span class="sxs-lookup"><span data-stu-id="7bc21-263">Or, if you have Storm on your development environment:</span></span>

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    <span data-ttu-id="7bc21-264">변경 hello `/path/to/newtopology.yaml` hello 이전 단계에서 만든 toohello 경로 toohello newtopology.yaml 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-264">Change hello `/path/to/newtopology.yaml` toohello path toohello newtopology.yaml file you created in hello previous step.</span></span> <span data-ttu-id="7bc21-265">이 명령은 hello 토폴로지 정의를 hello newtopology.yaml를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-265">This command uses hello newtopology.yaml as hello topology definition.</span></span> <span data-ttu-id="7bc21-266">Hello 포함 되지 이후 `compile` 매개 변수를 Maven 이전 단계에서 빌드한 hello 프로젝트의 hello 버전을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-266">Since we didn't include hello `compile` parameter, Maven uses hello version of hello project built in previous steps.</span></span>

    <span data-ttu-id="7bc21-267">Hello 한 번 시작 되는 토폴로지를 내보낸된 일괄 처리 간격 hello newtopology.yaml tooreflect hello 값이 변경 되었음을 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-267">Once hello topology starts, you should notice that hello time between emitted batches has changed tooreflect hello value in newtopology.yaml.</span></span> <span data-ttu-id="7bc21-268">따라서 toorecompile hello 토폴로지 필요 없이 구성의 변경할 YAML 파일을 통해 수 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-268">So you can see that you can change your configuration through a YAML file without having toorecompile hello topology.</span></span>

<span data-ttu-id="7bc21-269">이러한 기술 및 hello 표적이 framework의 기타 기능에 대 한 자세한 내용은 참조 하십시오. [표적이 (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-269">For more information on these and other features of hello Flux framework, see [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

## <a name="trident"></a><span data-ttu-id="7bc21-270">Trident</span><span class="sxs-lookup"><span data-stu-id="7bc21-270">Trident</span></span>

<span data-ttu-id="7bc21-271">Trident는 Storm에서 제공하는 높은 수준의 추상화이며</span><span class="sxs-lookup"><span data-stu-id="7bc21-271">Trident is a high-level abstraction that is provided by Storm.</span></span> <span data-ttu-id="7bc21-272">상태 저장 처리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-272">It supports stateful processing.</span></span> <span data-ttu-id="7bc21-273">hello Trident의 주요 이점은 hello 토폴로지가 입력 하는 모든 메시지가 한 번만 처리는 보장할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-273">hello primary advantage of Trident is that it can guarantee that every message that enters hello topology is processed only once.</span></span> <span data-ttu-id="7bc21-274">Trident를 사용하지 않으면 토폴로지는 메시지가 최소한 한 번은 처리된다는 것만 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-274">Without using Trident, your topology can only guarantee that messages are processed at least once.</span></span> <span data-ttu-id="7bc21-275">Bolt를 만드는 대신 사용할 수 있는 기본 제공 구성 요소와 같은 다른 차이점도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-275">There are also other differences, such as built-in components that can be used instead of creating bolts.</span></span> <span data-ttu-id="7bc21-276">사실 Bolt는 필터, 프로젝션 및 함수와 같이 덜 일반적인 구성 요소로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-276">In fact, bolts are replaced by less-generic components, such as filters, projections, and functions.</span></span>

<span data-ttu-id="7bc21-277">Trident 응용 프로그램은 Maven 프로젝트를 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-277">Trident applications can be created by using Maven projects.</span></span> <span data-ttu-id="7bc21-278">Hello를 사용 하 여이 문서의 앞부분에 제공 된 대로 동일한 기본 단계-hello 코드는 다른만 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-278">You use hello same basic steps as presented earlier in this article—only hello code is different.</span></span> <span data-ttu-id="7bc21-279">Trident 수 없습니다 (현재) 함께 사용할 수도 hello 표적이 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-279">Trident also cannot (currently) be used with hello Flux framework.</span></span>

<span data-ttu-id="7bc21-280">Trident에 대 한 자세한 내용은 참조 hello [Trident API 개요](http://storm.apache.org/documentation/Trident-API-Overview.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-280">For more information about Trident, see hello [Trident API Overview](http://storm.apache.org/documentation/Trident-API-Overview.html).</span></span>

<span data-ttu-id="7bc21-281">Trident 응용 프로그램 예제는 [HDInsight에서 Apache Storm을 사용하는 Twitter 추세 항목](hdinsight-storm-twitter-trending.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7bc21-281">For an example of a Trident application, see [Twitter trending topics with Apache Storm on HDInsight](hdinsight-storm-twitter-trending.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7bc21-282">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7bc21-282">Next Steps</span></span>

<span data-ttu-id="7bc21-283">배웠습니다 어떻게 toocreate Java를 사용 하 여 스톰 토폴로지입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-283">You have learned how toocreate a Storm topology by using Java.</span></span> <span data-ttu-id="7bc21-284">이제 다음으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc21-284">Now learn how to:</span></span>

* [<span data-ttu-id="7bc21-285">HDInsight에서 Apache Storm 토폴로지 배포 및 관리</span><span class="sxs-lookup"><span data-stu-id="7bc21-285">Deploy and manage Apache Storm topologies on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)

* [<span data-ttu-id="7bc21-286">Visual Studio를 사용하여 HDInsight에서 Apache Storm에 대한 C# 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="7bc21-286">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="7bc21-287">Storm 토폴로지에 대한 추가 예제는 [HDInsight의 Storm에 대한 예제 토폴로지](hdinsight-storm-example-topology.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7bc21-287">You can find more example Storm topologies by visiting [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

