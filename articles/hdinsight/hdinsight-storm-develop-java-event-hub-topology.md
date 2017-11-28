---
title: "Java를 사용하여 HDInsight의 Storm으로 Event Hub에서 이벤트 처리 | Microsoft Docs"
description: "Maven으로 만든 Java Storm 토폴로지를 사용하여 이벤트 허브 데이터를 처리하는 방법을 알아봅니다."
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
ms.openlocfilehash: 2e8ebbdab2be7bed224a67facec798820615bb22
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a><span data-ttu-id="90ea6-103">HDInsight의 Storm으로 Azure 이벤트 허브에서 이벤트 처리(Java)</span><span class="sxs-lookup"><span data-stu-id="90ea6-103">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>

<span data-ttu-id="90ea6-104">HDInsight의 Storm에서 Azure Event Hubs를 사용하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-104">Learn how to use Azure Event Hubs with Storm on HDInsight.</span></span> <span data-ttu-id="90ea6-105">이 예제는 Azure Event Hubs에서 데이터를 읽고 는 Java 기반 구성 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-105">This example uses Java-based components to read and write data in Azure Event Hubs.</span></span>

<span data-ttu-id="90ea6-106">Azure 이벤트 허브를 사용하면 웹 사이트, 앱 및 장치에서 대량의 데이터를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-106">Azure Event Hubs allows you to process massive amounts of data from websites, apps, and devices.</span></span> <span data-ttu-id="90ea6-107">Event Hub spout를 사용하면 HDInsight에서 Apache Storm을 사용하여 이 데이터를 실시간으로 쉽게 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-107">The Event Hub spout makes it easy to use Apache Storm on HDInsight to analyze this data in real time.</span></span> <span data-ttu-id="90ea6-108">또한 이벤트 허브 Bolt를 사용하여 Storm에서 이벤트 허브에 데이터를 기록할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-108">You can also write data to Event Hubs from Storm by using the Event Hubs bolt.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90ea6-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="90ea6-109">Prerequisites</span></span>

* <span data-ttu-id="90ea6-110">HDInsight 클러스터 버전 3.6의 Apache Storm</span><span class="sxs-lookup"><span data-stu-id="90ea6-110">An Apache Storm on HDInsight cluster version 3.6.</span></span> <span data-ttu-id="90ea6-111">자세한 내용은 [HDInsight 클러스터에서 Storm 시작](hdinsight-apache-storm-tutorial-get-started-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90ea6-111">For more information, see [Get started with Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="90ea6-112">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-112">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="90ea6-113">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90ea6-113">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="90ea6-114">[Azure 이벤트 허브](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="90ea6-114">An [Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="90ea6-115">[OpenJDK](http://openjdk.java.net/)와 같은 [Oracle JDK(Java 개발자 키트) 버전 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 또는 그와 동등</span><span class="sxs-lookup"><span data-stu-id="90ea6-115">[Oracle Java Developer Kit (JDK) version 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or equivalent, such as [OpenJDK](http://openjdk.java.net/).</span></span>

* <span data-ttu-id="90ea6-116">[Maven](https://maven.apache.org/download.cgi): Maven은 Java 프로젝트용 프로젝트 빌드 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-116">[Maven](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="90ea6-117">텍스트 편집기 또는 통합 개발 환경(IDE)입니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-117">A text editor or integrated development environment (IDE).</span></span>

    > [!NOTE]
    > <span data-ttu-id="90ea6-118">편집기 또는 IDE에 이 문서에서 다루지 않은 Maven과 함께 동작하는 특정 기능이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-118">Your editor or IDE may have specific functionality for working with Maven that is not addressed in this document.</span></span> <span data-ttu-id="90ea6-119">편집 환경 기능에 대한 내용은 사용 중인 제품의 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90ea6-119">For information about the capabilities of your editing environment, see the documentation for the product you are using.</span></span>

    * <span data-ttu-id="90ea6-120">SSH 클라이언트.</span><span class="sxs-lookup"><span data-stu-id="90ea6-120">An SSH client.</span></span> <span data-ttu-id="90ea6-121">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90ea6-121">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="90ea6-122">`ssh` 및 `scp` 명령.</span><span class="sxs-lookup"><span data-stu-id="90ea6-122">The `ssh` and `scp` commands.</span></span> <span data-ttu-id="90ea6-123">이러한 명령은 파일을 HDInsight 클러스터에 복사하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-123">These are used to copy files to the HDInsight cluster.</span></span> <span data-ttu-id="90ea6-124">Windows의 경우 Windows 10의 Bash를 통해 이러한 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-124">On Windows, you can get these through Bash on Windows 10.</span></span>

## <a name="understanding-the-example"></a><span data-ttu-id="90ea6-125">예제 이해</span><span class="sxs-lookup"><span data-stu-id="90ea6-125">Understanding the example</span></span>

<span data-ttu-id="90ea6-126">[hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) 예제는 두 토폴로지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-126">The [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) example contains two topologies:</span></span>

<span data-ttu-id="90ea6-127">`resources/writer.yaml` 토폴로지는 임의 데이터를 Azure Event Hub에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-127">The `resources/writer.yaml` topology writes random data to an Azure Event Hub.</span></span> <span data-ttu-id="90ea6-128">데이터는 `DeviceSpout` 구성 요소에서 생성되는 임의 장치 ID 및 장치 값입니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-128">The data is generated by the `DeviceSpout` component, and is a random device ID and device value.</span></span> <span data-ttu-id="90ea6-129">따라서 문자열 ID 및 숫자 값을 내보내는 하드웨어 일부를 시뮬레이션 중입니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-129">So it's simulating some hardware that emits a string ID and a numeric value.</span></span>

<span data-ttu-id="90ea6-130">`resources/reader.yaml` 토폴로지는 Event Hub에서 데이터(EventHubWriter에서 작성한 데이터)를 읽고 JSON 데이터를 구문 분석한 다음 `deviceId` 및 `deviceValue` 데이터를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-130">Thee `resources/reader.yaml` topology reads data from Event Hub (the data written by EventHubWriter,) parses the JSON data, and then logs the `deviceId` and `deviceValue` data.</span></span>

<span data-ttu-id="90ea6-131">데이터는 이벤트 허브에 기록되기 전에 JSON 문서로 형식이 지정되고 판독기에서 읽을 때 JSON에서 튜플로 구문이 분석됩니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-131">The data is formatted as a JSON document before it is written to Event Hub, and when read by the reader it is parsed out of JSON and into tuples.</span></span> <span data-ttu-id="90ea6-132">JSON 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-132">The JSON format is as follows:</span></span>

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a><span data-ttu-id="90ea6-133">프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="90ea6-133">Project configuration</span></span>

<span data-ttu-id="90ea6-134">`POM.xml` 파일은 이 Maven 프로젝트에 대한 구성 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-134">The `POM.xml` file contains configuration information for this Maven project.</span></span> <span data-ttu-id="90ea6-135">흥미로운 부분은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-135">The interesting pieces are:</span></span>

#### <a name="event-hub-components"></a><span data-ttu-id="90ea6-136">Event Hub 구성 요소</span><span class="sxs-lookup"><span data-stu-id="90ea6-136">Event Hub components</span></span>

<span data-ttu-id="90ea6-137">Azure Event Hubs를 읽고 Azure Event Hubs에 쓰는 구성 요소는 [HDInsight 리포지토리](https://github.com/hdinsight/mvn-rep)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-137">The component that reads and writes to Azure Event Hubs is located in the [HDInsight repository](https://github.com/hdinsight/mvn-rep).</span></span> <span data-ttu-id="90ea6-138">`POM.xml` 파일의 다음 섹션은 이 리포지토리에서 구성 요소를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-138">The following sections in the `POM.xml` file load the components from this repository</span></span>

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="the-eventhubs-storm-spout-dependency"></a><span data-ttu-id="90ea6-139">EventHubs Storm Spout 종속성</span><span class="sxs-lookup"><span data-stu-id="90ea6-139">The EventHubs Storm Spout dependency</span></span>

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

<span data-ttu-id="90ea6-140">이 xml은 eventhubs 패키지에 대한 종속성을 추가하며 이는 Event Hubs에서 읽기의 경우 Spout 및 쓰기의 경우 Bolt를 모두 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-140">This xml defines a dependency for the eventhubs package, which contains both a spout for reading from Event Hubs, and a bolt for writing to it.</span></span>

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

<span data-ttu-id="90ea6-141">이 xml은 HDInsight 3.5 이상에서 사용되는 Java 8에 대한 출력을 생성하는 프로젝트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-141">This xml configures the project to generate output for Java 8, which is used by HDInsight 3.5 or higher.</span></span>

#### <a name="the-maven-shade-plugin"></a><span data-ttu-id="90ea6-142">maven-shade-plugin</span><span class="sxs-lookup"><span data-stu-id="90ea6-142">The maven-shade-plugin</span></span>

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

<span data-ttu-id="90ea6-143">이 xml은 uber jar에 출력을 패키지하는 솔루션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-143">This xml configures the solution to package the output into an uber jar.</span></span> <span data-ttu-id="90ea6-144">jar은 프로젝트 코드와 필수 종속성을 모두 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-144">The jar contains both the project code and required dependencies.</span></span> <span data-ttu-id="90ea6-145">다음에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-145">It is also used to:</span></span>

* <span data-ttu-id="90ea6-146">종속성에 대한 라이선스 파일의 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-146">Rename license files for the dependencies.</span></span>
* <span data-ttu-id="90ea6-147">보안/서명을 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-147">Exclude security/signatures.</span></span>
* <span data-ttu-id="90ea6-148">동일한 인터페이스의 여러 구현이 하나의 항목으로 병합됩니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-148">Ensure that multiple implementations of the same interface are merged into one entry.</span></span>

<span data-ttu-id="90ea6-149">이러한 구성 설정은 런타임 시 오류를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-149">These configuration settings prevent errors at runtime.</span></span>

#### <a name="topology-definitions"></a><span data-ttu-id="90ea6-150">토폴로지 정의</span><span class="sxs-lookup"><span data-stu-id="90ea6-150">Topology definitions</span></span>

<span data-ttu-id="90ea6-151">이 예제에서는 [Flux](https://storm.apache.org/releases/1.1.0/flux.html) 프레임워크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-151">This example uses the [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span></span> <span data-ttu-id="90ea6-152">이 프레임워크에서는 YAML을 사용하여 토폴로지를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-152">This framework uses YAML to define the topologies.</span></span> <span data-ttu-id="90ea6-153">주요 이점은 Java 코드로 토폴로지를 하드 코드하지 않는다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-153">The primary benefit is that you aren't hard coding the topology in Java code.</span></span> <span data-ttu-id="90ea6-154">정의가 YAML이므로 모든 항목을 다시 컴파일할 필요 없이 토폴로지를 제출하기 전에 정의를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-154">Since the definition is YAML, you can change it before submitting the topology, without having to recompile everything.</span></span>

<span data-ttu-id="90ea6-155">__writer.yaml__:</span><span class="sxs-lookup"><span data-stu-id="90ea6-155">__writer.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubwriter"

components:
  # Configure the Event Hub spout
  - id: "eventhubbolt-config"
    className: "org.apache.storm.eventhubs.bolt.EventHubBoltConfig"
    constructorArgs:
      # These are populated from the .properties file when the topology is started
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
    # parallelism hint. This should be the same as the number of partitions for your Event Hub, so we read it from the dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

# How data flows through the components
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

<span data-ttu-id="90ea6-156">__reader.yaml__:</span><span class="sxs-lookup"><span data-stu-id="90ea6-156">__reader.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubreader"

components:
  # Configure the Event Hub spout
  - id: "eventhubspout-config"
    className: "org.apache.storm.eventhubs.spout.EventHubSpoutConfig"
    constructorArgs:
      # These are populated from the .properties file when the topology is started
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
    # parallelism hint. This should be the same as the number of partitions for your Event Hub, so we read it from the dev.properties file passed at run time.
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

# How data flows through the components
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

#### <a name="tell-the-topology-about-event-hub"></a><span data-ttu-id="90ea6-157">Event Hub에 대한 토폴로지 알리기</span><span class="sxs-lookup"><span data-stu-id="90ea6-157">Tell the topology about Event Hub</span></span>

<span data-ttu-id="90ea6-158">런타임에 `dev.properties` 파일은 Event Hub 구성을 토폴로지에 전달하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-158">At run time, the `dev.properties` file is used to pass the Event Hub configuration to the topology.</span></span> <span data-ttu-id="90ea6-159">다음 예제는 파일의 기본 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-159">The following example is the default contents of the file:</span></span>

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a><span data-ttu-id="90ea6-160">환경 변수 구성</span><span class="sxs-lookup"><span data-stu-id="90ea6-160">Configure environment variables</span></span>

<span data-ttu-id="90ea6-161">Java 및 JDK를 설치할 때 사용자의 개발 워크스테이션에 다음 환경 변수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-161">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="90ea6-162">하지만 변수가 존재하며 시스템에 대한 올바른 값을 포함하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-162">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="90ea6-163">**JAVA_HOME** - JRE(Java runtime environment)가 설치된 디렉터리를 가리켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-163">**JAVA_HOME** - should point to the directory where the Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="90ea6-164">예를 들어 Unix 또는 Linux 배포에서는 `/usr/lib/jvm/java-7-oracle`과 유사한 값이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-164">For example, in a Unix or Linux distribution, it should have a value similar to `/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="90ea6-165">Windows에서는 `c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="90ea6-165">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.7`</span></span>
* <span data-ttu-id="90ea6-166">**PATH** - 다음 경로를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-166">**PATH** - should contain the following paths:</span></span>

  * <span data-ttu-id="90ea6-167">**JAVA_HOME** 또는 그와 동등한 경로</span><span class="sxs-lookup"><span data-stu-id="90ea6-167">**JAVA_HOME** (or the equivalent path)</span></span>
  * <span data-ttu-id="90ea6-168">**JAVA_HOME\bin** 또는 그와 동등한 경로</span><span class="sxs-lookup"><span data-stu-id="90ea6-168">**JAVA_HOME\bin** (or the equivalent path)</span></span>
  * <span data-ttu-id="90ea6-169">Maven이 설치된 디렉터리</span><span class="sxs-lookup"><span data-stu-id="90ea6-169">The directory where Maven is installed</span></span>

## <a name="configure-event-hub"></a><span data-ttu-id="90ea6-170">이벤트 허브 구성</span><span class="sxs-lookup"><span data-stu-id="90ea6-170">Configure Event Hub</span></span>

<span data-ttu-id="90ea6-171">이벤트 허브는 이 예제의 데이터 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-171">Event Hubs is the data source for this example.</span></span> <span data-ttu-id="90ea6-172">다음 단계에 따라 Event Hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-172">Use the following steps to create a Event Hub.</span></span>

1. <span data-ttu-id="90ea6-173">[Azure 클래식 포털](https://manage.windowsazure.com)에서 **새로 만들기** > **Service Bus** > **이벤트 허브** > **사용자 지정 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-173">From the [Azure Classic Portal](https://manage.windowsazure.com), select **NEW** > **Service Bus** > **Event Hub** > **Custom Create**.</span></span>

2. <span data-ttu-id="90ea6-174">**새 Event Hub 추가** 화면에서 **Event Hub 이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-174">On the **Add a new Event Hub** screen, enter an **Event Hub Name**.</span></span> <span data-ttu-id="90ea6-175">**지역**을 선택하여 허브를 만든 다음 네임스페이스를 만들거나 기존 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-175">Select the **Region** to create the hub in, and then create a namespace or select an existing one.</span></span> <span data-ttu-id="90ea6-176">마지막으로 **화살표**를 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-176">Finally, click the **Arrow** to continue.</span></span>

    ![마법사 페이지 1](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > <span data-ttu-id="90ea6-178">대기 시간 및 비용을 줄이려면 HDInsight 서버의 Storm과 동일한 **위치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-178">Select the same **Location** as your Storm on HDInsight server to reduce latency and costs.</span></span>

3. <span data-ttu-id="90ea6-179">**이벤트 허브 구성** 화면에서 **파티션 개수** 및 **메시지 보존** 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-179">On the **Configure Event Hub** screen, enter the **Partition count** and **Message Retention** values.</span></span> <span data-ttu-id="90ea6-180">이 예에서는 파티션 개수로 10을, 메시지 보존으로는 1을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-180">For this example, use a partition count of 10 and a message retention of 1.</span></span> <span data-ttu-id="90ea6-181">파티션 개수 값은 나중에 필요하므로 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-181">Note the partition count because you need this value later.</span></span>

    ![마법사 페이지 2](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. <span data-ttu-id="90ea6-183">이벤트 허브를 만든 후 네임스페이스를 선택하고 **이벤트 허브**를 선택한 다음 앞에서 만든 이벤트 허브를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-183">After the event hub has been created, select the namespace, select **Event Hubs**, and then select the event hub that you created earlier.</span></span>
5. <span data-ttu-id="90ea6-184">**구성**을 선택하고 다음 정보를 사용하여 새 액세스 정책 두 개를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-184">Select **Configure**, then create two new access policies by using the following information:</span></span>

    <table>
    <tr><th><span data-ttu-id="90ea6-185">이름</span><span class="sxs-lookup"><span data-stu-id="90ea6-185">Name</span></span></th><th><span data-ttu-id="90ea6-186">권한</span><span class="sxs-lookup"><span data-stu-id="90ea6-186">Permissions</span></span></th></tr>
    <tr><td><span data-ttu-id="90ea6-187">기록기</span><span class="sxs-lookup"><span data-stu-id="90ea6-187">Writer</span></span></td><td><span data-ttu-id="90ea6-188">보내기</span><span class="sxs-lookup"><span data-stu-id="90ea6-188">Send</span></span></td></tr>
    <tr><td><span data-ttu-id="90ea6-189">읽기 권한자</span><span class="sxs-lookup"><span data-stu-id="90ea6-189">Reader</span></span></td><td><span data-ttu-id="90ea6-190">수신 대기</span><span class="sxs-lookup"><span data-stu-id="90ea6-190">Listen</span></span></td></tr>
    </table>

    <span data-ttu-id="90ea6-191">권한을 만든 후 페이지 아래쪽의 **저장** 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-191">After You create the permissions, select the **Save** icon at the bottom of the page.</span></span> <span data-ttu-id="90ea6-192">이러한 공유 액세스 정책은 Event Hub에 대한 읽기 및 쓰기에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-192">These shared access policies are used to read and write to Event Hub.</span></span>

    ![정책](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. <span data-ttu-id="90ea6-194">정책을 저장한 후 페이지 아래쪽의 **공유 액세스 키 생성기**를 사용하여 **기록기** 및 **판독기** 정책에 대한 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-194">After you save the policies, use the **Shared access key generator** at the bottom of the page to retrieve the key for the **writer** and **reader** policies.</span></span> <span data-ttu-id="90ea6-195">이러한 키를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-195">Save these keys.</span></span>

## <a name="download-and-build-the-project"></a><span data-ttu-id="90ea6-196">프로젝트 다운로드 및 빌드</span><span class="sxs-lookup"><span data-stu-id="90ea6-196">Download and build the project</span></span>

1. <span data-ttu-id="90ea6-197">GitHub에서 프로젝트 다운로드: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub)입니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-197">Download the project from GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span></span> <span data-ttu-id="90ea6-198">zip 아카이브로 패키지를 다운로드하거나 [git](https://git-scm.com/) 를 사용하여 프로젝트를 로컬로 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-198">You can either download the package as a zip archive, or use [git](https://git-scm.com/) to clone the project locally.</span></span>

2. <span data-ttu-id="90ea6-199">해당 Event Hub에 대한 구성으로 `dev.properties` 파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-199">Modify the `dev.properties` file with the configuration for your Event Hub.</span></span>

3. <span data-ttu-id="90ea6-200">다음을 사용하여 프로젝트를 빌드하고 패키징합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-200">Use the following to build and package the project:</span></span>

        mvn package

    <span data-ttu-id="90ea6-201">이 명령은 필수 종속성을 다운로드하고 프로젝트를 빌드한 다음 패키징합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-201">This command downloads required dependencies, builds, and then packages the project.</span></span> <span data-ttu-id="90ea6-202">출력은 **/target** 디렉터리에 **EventHubExample-1.0-SNAPSHOT.jar**로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-202">The output is stored in the **/target** directory as **EventHubExample-1.0-SNAPSHOT.jar**.</span></span>

## <a name="test-locally"></a><span data-ttu-id="90ea6-203">로컬에서 테스트</span><span class="sxs-lookup"><span data-stu-id="90ea6-203">Test locally</span></span>

<span data-ttu-id="90ea6-204">이러한 토폴로지는 Event Hubs를 읽고 Event Hubs에 쓸 뿐이므로 [Storm 개발 환경](http://storm.apache.org/releases/current/Setting-up-development-environment.html)이 있는 경우 로컬에서 이러한 토폴로지를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-204">Since these topologies just read and write to Event Hubs, you can test them locally if you have a [Storm development environment](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span></span> <span data-ttu-id="90ea6-205">다음 단계를 사용하여 개발 환경에서 로컬로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-205">Use the following steps to run locally in the dev environment:</span></span>

1. <span data-ttu-id="90ea6-206">기록기를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-206">Run the writer:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. <span data-ttu-id="90ea6-207">판독기를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-207">Run the reader:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * <span data-ttu-id="90ea6-208">`--local`: 로컬 모드(비분산)에서 토폴로지를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-208">`--local`: Run the topology in local mode (non-distributed).</span></span>
> * <span data-ttu-id="90ea6-209">`-R /writer.yaml`: jar에 패키지된 `resources`에서 토폴로지 정의를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-209">`-R /writer.yaml`: Load the topology definition from the `resources` packaged in the jar.</span></span> <span data-ttu-id="90ea6-210">토폴로지가 로컬 파일 시스템의 파일인 경우 대신에 해당 파일 경로를 마지막 매개 변수로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-210">If the topology is a file on the local file system, specify the path to it as the last parameter instead.</span></span>
> * <span data-ttu-id="90ea6-211">`--filter dev.properties`: `dev.properties` 내용을 사용하여 토폴로지 정의의 값을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-211">`--filter dev.properties`: Use the contents of `dev.properties` to fill in the values in the topology definitions.</span></span> <span data-ttu-id="90ea6-212">예: `${eventhub.read.policy.name}`</span><span class="sxs-lookup"><span data-stu-id="90ea6-212">For example, `${eventhub.read.policy.name}`.</span></span>

<span data-ttu-id="90ea6-213">로컬로 실행할 때 출력은 콘솔에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-213">Output is logged to the console when running locally.</span></span> <span data-ttu-id="90ea6-214">__Ctrl+C__를 사용하여 토폴로지를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-214">Use __Ctrl+C__ to stop the topology.</span></span>

## <a name="deploy-the-topologies"></a><span data-ttu-id="90ea6-215">토폴로지 배포</span><span class="sxs-lookup"><span data-stu-id="90ea6-215">Deploy the topologies</span></span>

1. <span data-ttu-id="90ea6-216">SCP를 사용하여 HDInsight 클러스터에 jar 패키지를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-216">Use SCP to copy the jar package to your HDInsight cluster.</span></span> <span data-ttu-id="90ea6-217">클러스터에 SSH 사용자로 사용자 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-217">Replace USERNAME with the SSH user for your cluster.</span></span> <span data-ttu-id="90ea6-218">CLUSTERNAME을 HDInsight 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-218">Replace CLUSTERNAME with the name of your HDInsight cluster:</span></span>

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    <span data-ttu-id="90ea6-219">SSH 계정에 암호를 사용한 경우 암호를 입력하라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-219">If you used a password for your SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="90ea6-220">계정에서 SSH 키를 사용한 경우 `-i` 매개 변수를 사용하여 키 파일에 대한 경로를 지정해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-220">If you used an SSH key with the account, you may need to use the `-i` parameter to specify the path to the key file.</span></span> <span data-ttu-id="90ea6-221">예를 들어 `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span><span class="sxs-lookup"><span data-stu-id="90ea6-221">For example, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span></span>

    <span data-ttu-id="90ea6-222">이 명령은 클러스터에 있는 SSH 사용자의 홈 디렉터리에 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-222">This command copies the file to the home directory of your SSH user on the cluster.</span></span>

2. <span data-ttu-id="90ea6-223">파일 업로드가 완료되면 SSH를 사용하여 HDInsight 클러스터에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-223">Once the file has finished uploading, use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="90ea6-224">**USERNAME**을 SSH 로그인의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-224">Replace **USERNAME** the name of your SSH login.</span></span> <span data-ttu-id="90ea6-225">**CLUSTERNAME** 을 HDInsight 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-225">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > <span data-ttu-id="90ea6-226">SSH 계정에 암호를 사용한 경우 암호를 입력하라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-226">If you used a password for your SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="90ea6-227">계정에서 SSH 키를 사용한 경우 `-i` 매개 변수를 사용하여 키 파일에 대한 경로를 지정해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-227">If you used an SSH key with the account, you may need to use the `-i` parameter to specify the path to the key file.</span></span> <span data-ttu-id="90ea6-228">다음 예제에서는 `~/.ssh/id_rsa`에서 개인 키를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-228">The following example loads the private key from `~/.ssh/id_rsa`:</span></span>
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. <span data-ttu-id="90ea6-229">다음 명령을 사용하여 토폴로지를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-229">Use the following command to start the topologies:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * <span data-ttu-id="90ea6-230">`--remote`: Nimbus 서비스에 토폴로지를 제출합니다. 그러면 클러스터의 작업자 노드에서 토폴로지가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-230">`--remote`: Submits the topology to the Nimbus service, which starts it on the worker nodes in the cluster.</span></span>

4. <span data-ttu-id="90ea6-231">기록된 데이터를 보려면 https://CLUSTERNAME.azurehdinsight.net/stormui로 이동합니다. 여기서 __CLUSTERNAME__은 HDInsight 클러스터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-231">To view the logged data, go to https://CLUSTERNAME.azurehdinsight.net/stormui, where __CLUSTERNAME__ is the name of your HDInsight cluster.</span></span> <span data-ttu-id="90ea6-232">토폴로지를 선택하고 구성 요소로 드릴다운합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-232">Select the topologies and drill down to the components.</span></span> <span data-ttu-id="90ea6-233">기록된 정보를 볼 구성 요소의 인스턴스에 대한 __port__ 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-233">Select the __port__ entry for an instance of a component to view logged information.</span></span>

5. <span data-ttu-id="90ea6-234">다음 명령을 사용하여 토폴로지를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="90ea6-234">Use the following commands to stop the topologies:</span></span>

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a><span data-ttu-id="90ea6-235">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="90ea6-235">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="90ea6-236">다음 단계</span><span class="sxs-lookup"><span data-stu-id="90ea6-236">Next steps</span></span>

* [<span data-ttu-id="90ea6-237">HDInsight의 Storm에 대한 예제 토폴로지</span><span class="sxs-lookup"><span data-stu-id="90ea6-237">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
