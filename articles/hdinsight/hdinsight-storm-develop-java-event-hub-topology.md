---
title: "Java를 사용 하 여 HDInsight의 Storm으로 이벤트 허브에서 aaaProcess 이벤트 | Microsoft Docs"
description: "Java 스톰 토폴로지를 사용 하 여 이벤트 허브 데이터 tooprocess Maven을 사용 하 여 만든 하는 방법에 대해 알아봅니다."
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 453fa7b0-c8a6-413e-8747-3ac3b71bed86
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/13/2017
ms.author: larryfr
ms.openlocfilehash: 6506f5bc8f6ab0e29350c071a3f84433382038e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a><span data-ttu-id="7cc71-103">HDInsight의 Storm으로 Azure 이벤트 허브에서 이벤트 처리(Java)</span><span class="sxs-lookup"><span data-stu-id="7cc71-103">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>

<span data-ttu-id="7cc71-104">자세한 내용은 방법 toouse HDInsight의 Storm와 Azure 이벤트 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-104">Learn how toouse Azure Event Hubs with Storm on HDInsight.</span></span> <span data-ttu-id="7cc71-105">이 예제에서는 Azure 이벤트 허브의 Java 기반 구성 요소 데이터 tooread 및 쓰기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-105">This example uses Java-based components tooread and write data in Azure Event Hubs.</span></span>

<span data-ttu-id="7cc71-106">Azure 이벤트 허브는 대량의 웹 사이트, 앱 및 장치에서 데이터를 tooprocess 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-106">Azure Event Hubs allows you tooprocess massive amounts of data from websites, apps, and devices.</span></span> <span data-ttu-id="7cc71-107">hello 배출구 이벤트 허브를 사용 하면 쉽게 toouse Apache Storm HDInsight tooanalyze에이 데이터를 실시간으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-107">hello Event Hub spout makes it easy toouse Apache Storm on HDInsight tooanalyze this data in real time.</span></span> <span data-ttu-id="7cc71-108">이벤트 허브 볼트 hello를 사용 하 여 스톰에서 tooEvent 데이터 허브를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-108">You can also write data tooEvent Hubs from Storm by using hello Event Hubs bolt.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7cc71-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7cc71-109">Prerequisites</span></span>

* <span data-ttu-id="7cc71-110">HDInsight 클러스터 버전 3.6의 Apache Storm</span><span class="sxs-lookup"><span data-stu-id="7cc71-110">An Apache Storm on HDInsight cluster version 3.6.</span></span> <span data-ttu-id="7cc71-111">자세한 내용은 [HDInsight 클러스터에서 Storm 시작](hdinsight-apache-storm-tutorial-get-started-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7cc71-111">For more information, see [Get started with Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="7cc71-112">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-112">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7cc71-113">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7cc71-113">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="7cc71-114">[Azure 이벤트 허브](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="7cc71-114">An [Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="7cc71-115">[OpenJDK](http://openjdk.java.net/)와 같은 [Oracle JDK(Java 개발자 키트) 버전 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 또는 그와 동등</span><span class="sxs-lookup"><span data-stu-id="7cc71-115">[Oracle Java Developer Kit (JDK) version 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or equivalent, such as [OpenJDK](http://openjdk.java.net/).</span></span>

* <span data-ttu-id="7cc71-116">[Maven](https://maven.apache.org/download.cgi): Maven은 Java 프로젝트용 프로젝트 빌드 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-116">[Maven](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="7cc71-117">텍스트 편집기 또는 통합 개발 환경(IDE)입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-117">A text editor or integrated development environment (IDE).</span></span>

    > [!NOTE]
    > <span data-ttu-id="7cc71-118">편집기 또는 IDE에 이 문서에서 다루지 않은 Maven과 함께 동작하는 특정 기능이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-118">Your editor or IDE may have specific functionality for working with Maven that is not addressed in this document.</span></span> <span data-ttu-id="7cc71-119">편집 환경의 hello 기능에 대 한 정보를 사용 하는 hello 제품에 대 한 hello 설명서를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-119">For information about hello capabilities of your editing environment, see hello documentation for hello product you are using.</span></span>

    * <span data-ttu-id="7cc71-120">SSH 클라이언트.</span><span class="sxs-lookup"><span data-stu-id="7cc71-120">An SSH client.</span></span> <span data-ttu-id="7cc71-121">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7cc71-121">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="7cc71-122">hello `ssh` 및 `scp` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-122">hello `ssh` and `scp` commands.</span></span> <span data-ttu-id="7cc71-123">이들은 사용된 toocopy 파일 toohello HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-123">These are used toocopy files toohello HDInsight cluster.</span></span> <span data-ttu-id="7cc71-124">Windows의 경우 Windows 10의 Bash를 통해 이러한 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-124">On Windows, you can get these through Bash on Windows 10.</span></span>

## <a name="understanding-hello-example"></a><span data-ttu-id="7cc71-125">이해 hello 예제</span><span class="sxs-lookup"><span data-stu-id="7cc71-125">Understanding hello example</span></span>

<span data-ttu-id="7cc71-126">hello [java 스톰 eventhub hdinsight](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) 예제에는 두 가지 토폴로지:</span><span class="sxs-lookup"><span data-stu-id="7cc71-126">hello [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) example contains two topologies:</span></span>

<span data-ttu-id="7cc71-127">hello `resources/writer.yaml` 토폴로지 임의의 데이터 tooan Azure 이벤트 허브를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-127">hello `resources/writer.yaml` topology writes random data tooan Azure Event Hub.</span></span> <span data-ttu-id="7cc71-128">hello hello 데이터를 생성 `DeviceSpout` 구성 요소는 임의 장치 ID와 장치 값 이며 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-128">hello data is generated by hello `DeviceSpout` component, and is a random device ID and device value.</span></span> <span data-ttu-id="7cc71-129">따라서 문자열 ID 및 숫자 값을 내보내는 하드웨어 일부를 시뮬레이션 중입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-129">So it's simulating some hardware that emits a string ID and a numeric value.</span></span>

<span data-ttu-id="7cc71-130">3 개 `resources/reader.yaml` 토폴로지 hello JSON 데이터를 구문 분석 하 고 hello를 로그 하는 이벤트 허브 (EventHubWriter를 통해 작성 된 hello 데이터)에서 데이터를 읽고 `deviceId` 및 `deviceValue` 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-130">Thee `resources/reader.yaml` topology reads data from Event Hub (hello data written by EventHubWriter,) parses hello JSON data, and then logs hello `deviceId` and `deviceValue` data.</span></span>

<span data-ttu-id="7cc71-131">hello 데이터 형식이 JSON द tooEvent 허브에 기록 되 고 hello 판독기가 읽을 때 전에 구문 분석 되어야 JSON를 튜플 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-131">hello data is formatted as a JSON document before it is written tooEvent Hub, and when read by hello reader it is parsed out of JSON and into tuples.</span></span> <span data-ttu-id="7cc71-132">hello JSON 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-132">hello JSON format is as follows:</span></span>

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a><span data-ttu-id="7cc71-133">프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="7cc71-133">Project configuration</span></span>

<span data-ttu-id="7cc71-134">hello `POM.xml` 파일이 Maven 프로젝트에 대 한 구성 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-134">hello `POM.xml` file contains configuration information for this Maven project.</span></span> <span data-ttu-id="7cc71-135">hello 흥미로운 부분에는</span><span class="sxs-lookup"><span data-stu-id="7cc71-135">hello interesting pieces are:</span></span>

#### <a name="event-hub-components"></a><span data-ttu-id="7cc71-136">Event Hub 구성 요소</span><span class="sxs-lookup"><span data-stu-id="7cc71-136">Event Hub components</span></span>

<span data-ttu-id="7cc71-137">hello 구성 요소를 읽고 쓰는 tooAzure 이벤트 허브 hello에 위치한 [HDInsight 리포지토리](https://github.com/hdinsight/mvn-rep)합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-137">hello component that reads and writes tooAzure Event Hubs is located in hello [HDInsight repository](https://github.com/hdinsight/mvn-rep).</span></span> <span data-ttu-id="7cc71-138">hello의 섹션에서는 다음 hello `POM.xml` 이 리포지토리의 파일 부하 hello 구성 요소</span><span class="sxs-lookup"><span data-stu-id="7cc71-138">hello following sections in hello `POM.xml` file load hello components from this repository</span></span>

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="hello-eventhubs-storm-spout-dependency"></a><span data-ttu-id="7cc71-139">hello EventHubs 스톰 Spout 종속성</span><span class="sxs-lookup"><span data-stu-id="7cc71-139">hello EventHubs Storm Spout dependency</span></span>

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

<span data-ttu-id="7cc71-140">이 xml 이벤트 허브에서 읽기 위해 배출구 tooit 작성 하기 위한 볼트 모두 들어 있는 hello eventhubs 패키지에 대 한 종속성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-140">This xml defines a dependency for hello eventhubs package, which contains both a spout for reading from Event Hubs, and a bolt for writing tooit.</span></span>

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

<span data-ttu-id="7cc71-141">이 xml 이상 HDInsight 3.5에서 사용 되는 Java 8에 대 한 hello 프로젝트 toogenerate 출력을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-141">This xml configures hello project toogenerate output for Java 8, which is used by HDInsight 3.5 or higher.</span></span>

#### <a name="hello-maven-shade-plugin"></a><span data-ttu-id="7cc71-142">hello maven-음영-플러그 인</span><span class="sxs-lookup"><span data-stu-id="7cc71-142">hello maven-shade-plugin</span></span>

```xml
<!-- build an uber jar -->
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-shade-plugin</artifactId>
<version>2.3</version>
<configuration>
    <transformers>
    <!-- Keep us from getting a can't overwrite file error -->
    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer"/>
    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer"/>
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

<span data-ttu-id="7cc71-143">이 xml uber jar에 hello 솔루션 toopackage hello 출력을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-143">This xml configures hello solution toopackage hello output into an uber jar.</span></span> <span data-ttu-id="7cc71-144">hello jar hello 프로젝트 코드와 필요한 종속성을 모두 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-144">hello jar contains both hello project code and required dependencies.</span></span> <span data-ttu-id="7cc71-145">다음에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-145">It is also used to:</span></span>

* <span data-ttu-id="7cc71-146">Hello 종속성에 대 한 라이선스 파일을 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-146">Rename license files for hello dependencies.</span></span>
* <span data-ttu-id="7cc71-147">보안/서명을 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-147">Exclude security/signatures.</span></span>
* <span data-ttu-id="7cc71-148">여러 번 구현 hello 동일 있는지 확인 한 항목으로 병합 하는 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-148">Ensure that multiple implementations of hello same interface are merged into one entry.</span></span>

<span data-ttu-id="7cc71-149">이러한 구성 설정은 런타임 시 오류를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-149">These configuration settings prevent errors at runtime.</span></span>

#### <a name="topology-definitions"></a><span data-ttu-id="7cc71-150">토폴로지 정의</span><span class="sxs-lookup"><span data-stu-id="7cc71-150">Topology definitions</span></span>

<span data-ttu-id="7cc71-151">이 예에서는 hello [표적이](https://storm.apache.org/releases/1.1.0/flux.html) 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-151">This example uses hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span></span> <span data-ttu-id="7cc71-152">이 프레임 워크 YAML toodefine hello 토폴로지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-152">This framework uses YAML toodefine hello topologies.</span></span> <span data-ttu-id="7cc71-153">hello 기본 이점은 하드 코딩 hello 토폴로지 Java 코드를 주는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-153">hello primary benefit is that you aren't hard coding hello topology in Java code.</span></span> <span data-ttu-id="7cc71-154">Hello 정의 YAML 이기 때문에 모든 toorecompile 필요 없이 hello 토폴로지를 전송 하기 전에 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-154">Since hello definition is YAML, you can change it before submitting hello topology, without having toorecompile everything.</span></span>

<span data-ttu-id="7cc71-155">__writer.yaml__:</span><span class="sxs-lookup"><span data-stu-id="7cc71-155">__writer.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubwriter"

components:
  # Configure hello Event Hub spout
  - id: "eventhubbolt-config"
    className: "org.apache.storm.eventhubs.bolt.EventHubBoltConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.write.policy.name}"
      - "${eventhub.write.policy.key}"
      - "${eventhub.namespace}"
      - "servicebus.windows.net"
      - "${eventhub.name}"

spouts:
  - id: "device-emulator-spout"
    className: "com.microsoft.example.DeviceSpout"
    parallelism: ${eventhub.partitions}

bolts:
  - id: "eventhub-bolt"
    className: "org.apache.storm.eventhubs.bolt.EventHubBolt"
    constructorArgs:
      - ref: "eventhubbolt-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

# How data flows through hello components
streams:
  - name: "spout -> eventhub" # just a string used for logging
    from: "device-emulator-spout"
    to: "eventhub-bolt"
    grouping:
        type: SHUFFLE

  - name: "spout -> logger"
    from: "device-emulator-spout"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

<span data-ttu-id="7cc71-156">__reader.yaml__:</span><span class="sxs-lookup"><span data-stu-id="7cc71-156">__reader.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubreader"

components:
  # Configure hello Event Hub spout
  - id: "eventhubspout-config"
    className: "org.apache.storm.eventhubs.spout.EventHubSpoutConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.read.policy.name}"
      - "${eventhub.read.policy.key}"
      - "${eventhub.namespace}"
      - "${eventhub.name}"
      - ${eventhub.partitions}

spouts:
  - id: "eventhub-spout"
    className: "org.apache.storm.eventhubs.spout.EventHubSpout"
    constructorArgs:
      - ref: "eventhubspout-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

bolts:
  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

  # Parses from JSON into tuples
  - id: "parser-bolt"
    className: "com.microsoft.example.ParserBolt"
    parallelism: ${eventhub.partitions}

# How data flows through hello components
streams:
  - name: "spout -> parser" # just a string used for logging
    from: "eventhub-spout"
    to: "parser-bolt"
    grouping:
        type: SHUFFLE

  - name: "parser -> log-bolt"
    from: "parser-bolt"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

#### <a name="tell-hello-topology-about-event-hub"></a><span data-ttu-id="7cc71-157">이벤트 허브에 대해 어떤 hello 토폴로지</span><span class="sxs-lookup"><span data-stu-id="7cc71-157">Tell hello topology about Event Hub</span></span>

<span data-ttu-id="7cc71-158">런타임 시 hello `dev.properties` 파일은 사용 되는 toopass hello 이벤트 허브 구성 toohello 토폴로지입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-158">At run time, hello `dev.properties` file is used toopass hello Event Hub configuration toohello topology.</span></span> <span data-ttu-id="7cc71-159">hello 다음 예제는 hello 파일의 기본 내용 hello:</span><span class="sxs-lookup"><span data-stu-id="7cc71-159">hello following example is hello default contents of hello file:</span></span>

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a><span data-ttu-id="7cc71-160">환경 변수 구성</span><span class="sxs-lookup"><span data-stu-id="7cc71-160">Configure environment variables</span></span>

<span data-ttu-id="7cc71-161">hello 다음과 같은 환경 변수 설정 되어 있습니다 Java와 hello JDK 개발용 워크스테이션에 설치 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="7cc71-161">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="7cc71-162">그러나 시스템에 대 한 올바른 값 hello를 포함 하 고 있는 것을 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-162">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="7cc71-163">**JAVA_HOME** -toohello hello Java runtime environment (JRE)가 설치 디렉터리를 가리켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-163">**JAVA_HOME** - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="7cc71-164">예를 들어, Unix 또는 Linux 배포 없어야과 유사한 값 너무`/usr/lib/jvm/java-7-oracle`합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-164">For example, in a Unix or Linux distribution, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="7cc71-165">Windows에서 동일 하 게과 유사한 값 너무`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="7cc71-165">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>
* <span data-ttu-id="7cc71-166">**경로** -hello 다음 경로 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-166">**PATH** - should contain hello following paths:</span></span>

  * <span data-ttu-id="7cc71-167">**JAVA_HOME** (또는 hello 해당 하는 경로)</span><span class="sxs-lookup"><span data-stu-id="7cc71-167">**JAVA_HOME** (or hello equivalent path)</span></span>
  * <span data-ttu-id="7cc71-168">**JAVA_HOME\bin** (또는 hello 해당 하는 경로)</span><span class="sxs-lookup"><span data-stu-id="7cc71-168">**JAVA_HOME\bin** (or hello equivalent path)</span></span>
  * <span data-ttu-id="7cc71-169">Maven 설치 되어 있는 hello 디렉터리</span><span class="sxs-lookup"><span data-stu-id="7cc71-169">hello directory where Maven is installed</span></span>

## <a name="configure-event-hub"></a><span data-ttu-id="7cc71-170">이벤트 허브 구성</span><span class="sxs-lookup"><span data-stu-id="7cc71-170">Configure Event Hub</span></span>

<span data-ttu-id="7cc71-171">이벤트 허브는이 예제에 대 한 hello 데이터 원본.</span><span class="sxs-lookup"><span data-stu-id="7cc71-171">Event Hubs is hello data source for this example.</span></span> <span data-ttu-id="7cc71-172">다음 단계 toocreate 이벤트 허브를 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-172">Use hello following steps toocreate a Event Hub.</span></span>

1. <span data-ttu-id="7cc71-173">Hello에서 [Azure 클래식 포털](https://manage.windowsazure.com)선택, **새로** > **서비스 버스** > **이벤트 허브**  >  **사용자 지정 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-173">From hello [Azure Classic Portal](https://manage.windowsazure.com), select **NEW** > **Service Bus** > **Event Hub** > **Custom Create**.</span></span>

2. <span data-ttu-id="7cc71-174">Hello에 **새 이벤트 허브 추가** 화면에서 입력 한 **이벤트 허브 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-174">On hello **Add a new Event Hub** screen, enter an **Event Hub Name**.</span></span> <span data-ttu-id="7cc71-175">선택 hello **지역** toocreate hello 허브에서는 다음 네임 스페이스를 만들거나 기존 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-175">Select hello **Region** toocreate hello hub in, and then create a namespace or select an existing one.</span></span> <span data-ttu-id="7cc71-176">마지막으로 hello 클릭 **화살표** toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-176">Finally, click hello **Arrow** toocontinue.</span></span>

    ![마법사 페이지 1](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > <span data-ttu-id="7cc71-178">동일한 select hello **위치** HDInsight 서버 tooreduce 대기 시간 및 비용에 프로그램 스톰으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-178">Select hello same **Location** as your Storm on HDInsight server tooreduce latency and costs.</span></span>

3. <span data-ttu-id="7cc71-179">Hello에 **이벤트 허브 구성** 화면에서 입력 하는 hello **count 파티션** 및 **메시지 보존** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-179">On hello **Configure Event Hub** screen, enter hello **Partition count** and **Message Retention** values.</span></span> <span data-ttu-id="7cc71-180">이 예에서는 파티션 개수로 10을, 메시지 보존으로는 1을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-180">For this example, use a partition count of 10 and a message retention of 1.</span></span> <span data-ttu-id="7cc71-181">이 값을 나중에 필요 하기 때문에 hello 파티션 수를 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-181">Note hello partition count because you need this value later.</span></span>

    ![마법사 페이지 2](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. <span data-ttu-id="7cc71-183">Hello 이벤트 허브에 대 한 생성을 선택 하는 hello 네임 스페이스를 수행한 후에 선택 **이벤트 허브**, 한 다음 이전에 만든 hello 이벤트 허브를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-183">After hello event hub has been created, select hello namespace, select **Event Hubs**, and then select hello event hub that you created earlier.</span></span>
5. <span data-ttu-id="7cc71-184">선택 **구성**, 다음 두 가지 새로운 액세스 정책을 hello 다음 정보를 사용 하 여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-184">Select **Configure**, then create two new access policies by using hello following information:</span></span>

    <table>
    <tr><th><span data-ttu-id="7cc71-185">이름</span><span class="sxs-lookup"><span data-stu-id="7cc71-185">Name</span></span></th><th><span data-ttu-id="7cc71-186">권한</span><span class="sxs-lookup"><span data-stu-id="7cc71-186">Permissions</span></span></th></tr>
    <tr><td><span data-ttu-id="7cc71-187">기록기</span><span class="sxs-lookup"><span data-stu-id="7cc71-187">Writer</span></span></td><td><span data-ttu-id="7cc71-188">보내기</span><span class="sxs-lookup"><span data-stu-id="7cc71-188">Send</span></span></td></tr>
    <tr><td><span data-ttu-id="7cc71-189">읽기 권한자</span><span class="sxs-lookup"><span data-stu-id="7cc71-189">Reader</span></span></td><td><span data-ttu-id="7cc71-190">수신 대기</span><span class="sxs-lookup"><span data-stu-id="7cc71-190">Listen</span></span></td></tr>
    </table>

    <span data-ttu-id="7cc71-191">Hello 사용 권한을 만든 후 선택 hello **저장** hello hello 페이지 맨 위에 있는 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-191">After You create hello permissions, select hello **Save** icon at hello bottom of hello page.</span></span> <span data-ttu-id="7cc71-192">이러한 공유 액세스 정책은 사용 되는 tooread 있으며 tooEvent 허브를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-192">These shared access policies are used tooread and write tooEvent Hub.</span></span>

    ![정책](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. <span data-ttu-id="7cc71-194">Hello를 사용 하 여 hello 정책을 저장 한 후 **공유 액세스 키 생성기** hello에 대 한 hello 페이지 tooretrieve hello 키 hello 맨 아래에 **기록기** 및 **판독기** 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-194">After you save hello policies, use hello **Shared access key generator** at hello bottom of hello page tooretrieve hello key for hello **writer** and **reader** policies.</span></span> <span data-ttu-id="7cc71-195">이러한 키를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-195">Save these keys.</span></span>

## <a name="download-and-build-hello-project"></a><span data-ttu-id="7cc71-196">다운로드 하 고 hello 프로젝트 빌드</span><span class="sxs-lookup"><span data-stu-id="7cc71-196">Download and build hello project</span></span>

1. <span data-ttu-id="7cc71-197">GitHub에서 hello 프로젝트를 다운로드: [java 스톰 eventhub hdinsight](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub)합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-197">Download hello project from GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span></span> <span data-ttu-id="7cc71-198">Zip 보관 파일로 hello 패키지를 다운로드 하거나 사용할 [git](https://git-scm.com/) 로컬로 tooclone hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="7cc71-198">You can either download hello package as a zip archive, or use [git](https://git-scm.com/) tooclone hello project locally.</span></span>

2. <span data-ttu-id="7cc71-199">Hello 수정 `dev.properties` 이벤트 허브에 대 한 hello 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-199">Modify hello `dev.properties` file with hello configuration for your Event Hub.</span></span>

3. <span data-ttu-id="7cc71-200">다음 toobuild 및 패키지 hello 프로젝트 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-200">Use hello following toobuild and package hello project:</span></span>

        mvn package

    <span data-ttu-id="7cc71-201">이 명령은 빌드에 필요한 종속성을 다운로드 한 다음 패키지 hello 프로젝트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-201">This command downloads required dependencies, builds, and then packages hello project.</span></span> <span data-ttu-id="7cc71-202">hello 출력이 hello에 저장 됩니다 **/대상** 으로 디렉터리 **EventHubExample-1.0-SNAPSHOT.jar**합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-202">hello output is stored in hello **/target** directory as **EventHubExample-1.0-SNAPSHOT.jar**.</span></span>

## <a name="test-locally"></a><span data-ttu-id="7cc71-203">로컬에서 테스트</span><span class="sxs-lookup"><span data-stu-id="7cc71-203">Test locally</span></span>

<span data-ttu-id="7cc71-204">이러한 토폴로지가 바로 읽고 쓰는 tooEvent 허브, 이후 테스트할 수 있습니다 있는 경우에 로컬로 [스톰 개발 환경](http://storm.apache.org/releases/current/Setting-up-development-environment.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-204">Since these topologies just read and write tooEvent Hubs, you can test them locally if you have a [Storm development environment](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span></span> <span data-ttu-id="7cc71-205">Hello 개발 환경에서 로컬로 toorun 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-205">Use hello following steps toorun locally in hello dev environment:</span></span>

1. <span data-ttu-id="7cc71-206">Hello 기록기를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-206">Run hello writer:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. <span data-ttu-id="7cc71-207">Hello 판독기를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-207">Run hello reader:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * <span data-ttu-id="7cc71-208">`--local`: Hello 토폴로지 모드에서 실행 로컬 (비 배포).</span><span class="sxs-lookup"><span data-stu-id="7cc71-208">`--local`: Run hello topology in local mode (non-distributed).</span></span>
> * <span data-ttu-id="7cc71-209">`-R /writer.yaml`: Hello에서 hello 토폴로지 정의 로드 합니다. `resources` hello jar에 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-209">`-R /writer.yaml`: Load hello topology definition from hello `resources` packaged in hello jar.</span></span> <span data-ttu-id="7cc71-210">Hello 토폴로지는 hello 로컬 파일 시스템에 파일을 대신 hello 경로 tooit hello 마지막 매개 변수로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-210">If hello topology is a file on hello local file system, specify hello path tooit as hello last parameter instead.</span></span>
> * <span data-ttu-id="7cc71-211">`--filter dev.properties`: 사용 하 여 hello 내용의 `dev.properties` toofill hello 토폴로지 정의에 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-211">`--filter dev.properties`: Use hello contents of `dev.properties` toofill in hello values in hello topology definitions.</span></span> <span data-ttu-id="7cc71-212">예: `${eventhub.read.policy.name}`.</span><span class="sxs-lookup"><span data-stu-id="7cc71-212">For example, `${eventhub.read.policy.name}`.</span></span>

<span data-ttu-id="7cc71-213">출력은 로컬로 실행 하는 경우 로깅된 toohello 콘솔입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-213">Output is logged toohello console when running locally.</span></span> <span data-ttu-id="7cc71-214">사용 하 여 __Ctrl + C__ toostop hello 토폴로지입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-214">Use __Ctrl+C__ toostop hello topology.</span></span>

## <a name="deploy-hello-topologies"></a><span data-ttu-id="7cc71-215">Hello 토폴로지를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-215">Deploy hello topologies</span></span>

1. <span data-ttu-id="7cc71-216">SCP toocopy hello jar 패키지 tooyour HDInsight 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-216">Use SCP toocopy hello jar package tooyour HDInsight cluster.</span></span> <span data-ttu-id="7cc71-217">클러스터에 대 한 hello SSH 사용자와 사용자 이름을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-217">Replace USERNAME with hello SSH user for your cluster.</span></span> <span data-ttu-id="7cc71-218">CLUSTERNAME를 HDInsight 클러스터의 hello 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-218">Replace CLUSTERNAME with hello name of your HDInsight cluster:</span></span>

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    <span data-ttu-id="7cc71-219">SSH 계정에 대 한 암호를 사용 하는 경우 메시지 표시 tooenter hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-219">If you used a password for your SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="7cc71-220">SSH 키를 사용 하는 hello 계정과 toouse hello를 할 수 있습니다 `-i` 매개 변수 toospecify hello 경로 toohello 키 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-220">If you used an SSH key with hello account, you may need toouse hello `-i` parameter toospecify hello path toohello key file.</span></span> <span data-ttu-id="7cc71-221">예를 들어 `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span><span class="sxs-lookup"><span data-stu-id="7cc71-221">For example, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span></span>

    <span data-ttu-id="7cc71-222">이 명령은 hello 파일 toohello hello 클러스터에 대 한 SSH 사용자의 홈 디렉터리에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-222">This command copies hello file toohello home directory of your SSH user on hello cluster.</span></span>

2. <span data-ttu-id="7cc71-223">Hello 파일 업로드 완료 되 면 SSH tooconnect toohello HDInsight 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-223">Once hello file has finished uploading, use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="7cc71-224">대체 **USERNAME** hello 이름 SSH 로그인입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-224">Replace **USERNAME** hello name of your SSH login.</span></span> <span data-ttu-id="7cc71-225">**CLUSTERNAME** 을 HDInsight 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-225">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > <span data-ttu-id="7cc71-226">SSH 계정에 대 한 암호를 사용 하는 경우 메시지 표시 tooenter hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-226">If you used a password for your SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="7cc71-227">SSH 키를 사용 하는 hello 계정과 toouse hello를 할 수 있습니다 `-i` 매개 변수 toospecify hello 경로 toohello 키 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-227">If you used an SSH key with hello account, you may need toouse hello `-i` parameter toospecify hello path toohello key file.</span></span> <span data-ttu-id="7cc71-228">hello 다음 예제에서는 로드에서 개인 키 hello `~/.ssh/id_rsa`:</span><span class="sxs-lookup"><span data-stu-id="7cc71-228">hello following example loads hello private key from `~/.ssh/id_rsa`:</span></span>
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. <span data-ttu-id="7cc71-229">다음 명령 toostart hello 토폴로지 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-229">Use hello following command toostart hello topologies:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * <span data-ttu-id="7cc71-230">`--remote`: Hello 토폴로지 toohello hello 클러스터의 작업자 노드 hello에 시작 Nimbus 서비스에 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-230">`--remote`: Submits hello topology toohello Nimbus service, which starts it on hello worker nodes in hello cluster.</span></span>

4. <span data-ttu-id="7cc71-231">tooview hello 기록 데이터를 이동 toohttps://CLUSTERNAME.azurehdinsight.net/stormui, 여기서 __CLUSTERNAME__ HDInsight 클러스터의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-231">tooview hello logged data, go toohttps://CLUSTERNAME.azurehdinsight.net/stormui, where __CLUSTERNAME__ is hello name of your HDInsight cluster.</span></span> <span data-ttu-id="7cc71-232">Hello 토폴로지를 선택 하 고 드릴 다운 toohello 구성 요소.</span><span class="sxs-lookup"><span data-stu-id="7cc71-232">Select hello topologies and drill down toohello components.</span></span> <span data-ttu-id="7cc71-233">선택 hello __포트__ 항목 구성 요소 tooview의 인스턴스에 대 한 정보를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-233">Select hello __port__ entry for an instance of a component tooview logged information.</span></span>

5. <span data-ttu-id="7cc71-234">사용 하 여 hello 다음 명령 toostop hello 토폴로지:</span><span class="sxs-lookup"><span data-stu-id="7cc71-234">Use hello following commands toostop hello topologies:</span></span>

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a><span data-ttu-id="7cc71-235">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="7cc71-235">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="7cc71-236">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7cc71-236">Next steps</span></span>

* [<span data-ttu-id="7cc71-237">HDInsight의 Storm에 대한 예제 토폴로지</span><span class="sxs-lookup"><span data-stu-id="7cc71-237">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
