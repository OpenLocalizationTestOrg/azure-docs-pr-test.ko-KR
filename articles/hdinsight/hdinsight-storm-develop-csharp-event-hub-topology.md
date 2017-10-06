---
title: "Storm-Azure HDInsight으로 이벤트 허브에서 aaaProcess 이벤트 | Microsoft Docs"
description: "C# 스톰 토폴로지를 사용 하 여 Azure 이벤트 허브에서 tooprocess 데이터 만드는 방법 Visual Studio에서 hello를 사용 하 여 HDInsight tools for Visual Studio에 알아봅니다."
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 67f9d08c-eea0-401b-952b-db765655dad0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 30cd910d80eba066f283197bcbbaf11145bc5524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a><span data-ttu-id="6aeee-103">HDInsight의 Storm(C#)으로 Azure Event Hubs에서 이벤트 처리</span><span class="sxs-lookup"><span data-stu-id="6aeee-103">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>

<span data-ttu-id="6aeee-104">자세한 방법을 toowork HDInsight의 Apache Storm에서 Azure 이벤트 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-104">Learn how toowork with Azure Event Hubs from Apache Storm on HDInsight.</span></span> <span data-ttu-id="6aeee-105">이 문서에서는 Evbent 허브에서 C# 스톰 토폴로지 tooread 및 쓰기 데이터 사용</span><span class="sxs-lookup"><span data-stu-id="6aeee-105">This document uses a C# Storm topology tooread and write data from Evbent Hubs</span></span>

> [!NOTE]
> <span data-ttu-id="6aeee-106">이 프로젝트의 Java 버전은 [HDInsight의 Storm(Java)으로 Azure Event Hubs에서 이벤트 처리](hdinsight-storm-develop-java-event-hub-topology.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6aeee-106">For a Java version of this project, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="scpnet"></a><span data-ttu-id="6aeee-107">SCP.NET</span><span class="sxs-lookup"><span data-stu-id="6aeee-107">SCP.NET</span></span>

<span data-ttu-id="6aeee-108">이 문서의 단계 hello SCP.NET, NuGet 패키지를 사용 하면 쉽게 toocreate C# 토폴로지 및 스톰와 함께 사용할 구성 요소에 HDInsight를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-108">hello steps in this document use SCP.NET, a NuGet package that makes it easy toocreate C# topologies and components for use with Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6aeee-109">Hello이 문서의 단계 동안 Visual Studio와 함께 Windows 개발 환경에 의존, hello 컴파일된 프로젝트 Linux를 사용 하는 HDInsight 클러스터에 제출 된 tooa 스톰 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-109">While hello steps in this document rely on a Windows development environment with Visual Studio, hello compiled project can be submitted tooa Storm on HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="6aeee-110">2016년 10월 28일 이후에 만든 Linux 기반 클러스터만 SCP.NET 토폴로지를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-110">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="6aeee-111">HDInsight 3.4 및 큰 사용 모노 toorun C# 토폴로지입니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-111">HDInsight 3.4 and greater use Mono toorun C# topologies.</span></span> <span data-ttu-id="6aeee-112">이 문서에 사용 된 hello 예제 HDInsight 3.6 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-112">hello example used in this document works with HDInsight 3.6.</span></span> <span data-ttu-id="6aeee-113">HDInsight에 대 한.NET 솔루션을 만드는 방법에 하려는 경우 확인 hello [모노 호환성](http://www.mono-project.com/docs/about-mono/compatibility/) 잠재적인 호환성 문제에 대 한 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-113">If you plan on creating your own .NET solutions for HDInsight, check hello [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>

### <a name="cluster-versioning"></a><span data-ttu-id="6aeee-114">클러스터 버전 관리</span><span class="sxs-lookup"><span data-stu-id="6aeee-114">Cluster versioning</span></span>

<span data-ttu-id="6aeee-115">hello Microsoft.SCP.Net.SDK NuGet 패키지를 프로젝트에 사용할 HDInsight에 설치 된 Storm의 주 버전 hello 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-115">hello Microsoft.SCP.Net.SDK NuGet package you use for your project must match hello major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="6aeee-116">HDInsight 버전 3.5 및 3.6은 Storm 1.x를 사용하므로 이 클러스터와 함께 SCP.NET 버전 1.0.x.x를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-116">HDInsight versions 3.5 and 3.6 use Storm 1.x, so you must use SCP.NET version 1.0.x.x with these clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6aeee-117">이 문서에 hello 예제 HDInsight 3.5 또는 3.6 클러스터에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-117">hello example in this document expects an HDInsight 3.5 or 3.6 cluster.</span></span>
>
> <span data-ttu-id="6aeee-118">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-118">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6aeee-119">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6aeee-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="6aeee-120">C# 토폴로지도 .NET 4.5를 대상으로 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-120">C# topologies must also target .NET 4.5.</span></span>

## <a name="how-toowork-with-event-hubs"></a><span data-ttu-id="6aeee-121">어떻게 toowork 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="6aeee-121">How toowork with Event Hubs</span></span>

<span data-ttu-id="6aeee-122">Microsoft 스톰 토폴로지에서 이벤트 허브 사용된 toocommunicate 일 수 있는 Java 구성 요소 집합을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-122">Microsoft provides a set of Java components that can be used toocommunicate with Event Hubs from a Storm topology.</span></span> <span data-ttu-id="6aeee-123">HDInsight 3.6 호환 버전에서 이러한 구성 요소를 포함 하는 hello Java 보관 파일 (JAR) 파일을 찾을 수 [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar)합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-123">You can find hello Java archive (JAR) file that contains an HDInsight 3.6 compatible version of these components at [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6aeee-124">Hello 구성 요소는 Java로 작성 된 경우 C# 토폴로지에서 쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-124">While hello components are written in Java, you can easily use them from a C# topology.</span></span>

<span data-ttu-id="6aeee-125">이 예제에 다음과 같은 구성 요소가 hello 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-125">hello following components are used in this example:</span></span>

* <span data-ttu-id="6aeee-126">__EventHubSpout__: Event Hubs에서 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-126">__EventHubSpout__: Reads data from Event Hubs.</span></span>
* <span data-ttu-id="6aeee-127">__EventHubBolt__: tooEvent 데이터 허브를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-127">__EventHubBolt__: Writes data tooEvent Hubs.</span></span>
* <span data-ttu-id="6aeee-128">__EventHubSpoutConfig__: tooconfigure EventHubSpout를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-128">__EventHubSpoutConfig__: Used tooconfigure EventHubSpout.</span></span>
* <span data-ttu-id="6aeee-129">__EventHubBoltConfig__: tooconfigure EventHubBolt를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-129">__EventHubBoltConfig__: Used tooconfigure EventHubBolt.</span></span>

### <a name="example-spout-usage"></a><span data-ttu-id="6aeee-130">예제 Spout 사용</span><span class="sxs-lookup"><span data-stu-id="6aeee-130">Example spout usage</span></span>

<span data-ttu-id="6aeee-131">SCP.NET은 EventHubSpout tooyour 토폴로지를 추가 하기 위한 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-131">SCP.NET provides methods for adding an EventHubSpout tooyour topology.</span></span> <span data-ttu-id="6aeee-132">이러한 메서드는 Java 구성 요소를 추가 하기 위한 hello 제네릭 메서드를 사용 하 여 보다 쉽게 tooadd는 배출구 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-132">These methods make it easier tooadd a spout than using hello generic methods for adding a Java component.</span></span> <span data-ttu-id="6aeee-133">hello 다음 예제에서는 방법을 사용 하 여 배출구 toocreate hello __SetEventHubSpout__ 및 **EventHubSpoutConfig** SCP.NET에서 제공 하는 메서드:</span><span class="sxs-lookup"><span data-stu-id="6aeee-133">hello following example demonstrates how toocreate a spout by using hello __SetEventHubSpout__ and **EventHubSpoutConfig** methods provided by SCP.NET:</span></span>

```csharp
 topologyBuilder.SetEventHubSpout(
    "EventHubSpout",
    new EventHubSpoutConfig(
        ConfigurationManager.AppSettings["EventHubSharedAccessKeyName"],
        ConfigurationManager.AppSettings["EventHubSharedAccessKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        ConfigurationManager.AppSettings["EventHubEntityPath"],
        eventHubPartitions),
    eventHubPartitions);
```

<span data-ttu-id="6aeee-134">이전 예제 hello 라는 새 배출구 구성 요소를 만들고 __EventHubSpout__, 이벤트 허브 사용 toocommunicate을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-134">hello previous example creates a new spout component named __EventHubSpout__, and configures it toocommunicate with an event hub.</span></span> <span data-ttu-id="6aeee-135">hello 구성 요소에 대 한 병렬 처리 힌트 hello hello 이벤트 허브에 toohello 파티션 수가 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-135">hello parallelism hint for hello component is set toohello number of partitions in hello event hub.</span></span> <span data-ttu-id="6aeee-136">이 설정을 통해 스톰 toocreate 각 파티션에 대 한 hello 구성 요소의 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="6aeee-136">This setting allows Storm toocreate an instance of hello component for each partition.</span></span>

### <a name="example-bolt-usage"></a><span data-ttu-id="6aeee-137">예제 Bolt 사용</span><span class="sxs-lookup"><span data-stu-id="6aeee-137">Example bolt usage</span></span>

<span data-ttu-id="6aeee-138">사용 하 여 hello **JavaComponmentConstructor** 메서드 toocreate hello 볼트의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-138">Use hello **JavaComponmentConstructor** method toocreate an instance of hello bolt.</span></span> <span data-ttu-id="6aeee-139">hello 다음 예제에서는 어떻게 toocreate hello의 새 인스턴스를 구성 하 고 **EventHubBolt**:</span><span class="sxs-lookup"><span data-stu-id="6aeee-139">hello following example demonstrates how toocreate and configure a new instance of hello **EventHubBolt**:</span></span>

```csharp
// Java construcvtor for hello Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set hello bolt toosubscribe toodata from hello spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> <span data-ttu-id="6aeee-140">이 예에서는 사용 하는 대신 문자열로 전달 Clojure 식 **JavaComponentConstructor** toocreate는 **EventHubBoltConfig**hello 배출구 예제 때와 마찬가지로, 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-140">This example uses a Clojure expression passed as a string, instead of using **JavaComponentConstructor** toocreate an **EventHubBoltConfig**, as hello spout example did.</span></span> <span data-ttu-id="6aeee-141">어떤 방법이든 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-141">Either method works.</span></span> <span data-ttu-id="6aeee-142">최상의 tooyou 판단는 hello 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-142">Use hello method that feels best tooyou.</span></span>

## <a name="download-hello-completed-project"></a><span data-ttu-id="6aeee-143">완료 하는 hello 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="6aeee-143">Download hello completed project</span></span>

<span data-ttu-id="6aeee-144">이 자습서에서 만든 hello 프로젝트의 전체 버전을 다운로드할 수 있습니다 [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub)합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-144">You can download a complete version of hello project created in this tutorial from [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span> <span data-ttu-id="6aeee-145">그러나 보내야 tooprovide 구성 설정을이 자습서에서는 hello 단계에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-145">However, you still need tooprovide configuration settings by following hello steps in this tutorial.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="6aeee-146">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6aeee-146">Prerequisites</span></span>

* <span data-ttu-id="6aeee-147">[HDInsight 클러스터 버전 3.5 또는 3.6의 Apache Storm](hdinsight-apache-storm-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6aeee-147">An [Apache Storm on HDInsight cluster version 3.5 or 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span></span>

    > [!WARNING]
    > <span data-ttu-id="6aeee-148">이 문서에 사용 되는 hello 예제 스톰 HDInsight 버전 3.5 또는 3.6에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-148">hello example used in this document requires Storm on HDInsight version 3.5 or 3.6.</span></span> <span data-ttu-id="6aeee-149">기한 toobreaking 클래스 이름 변경, HDInsight의 이전 버전으로 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-149">This does not work with older versions of HDInsight, due toobreaking class name changes.</span></span> <span data-ttu-id="6aeee-150">이전 클러스터에서 작동하는 이 예제의 버전은 [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6aeee-150">For a version of this example that works with older clusters, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span></span>

* <span data-ttu-id="6aeee-151">[Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="6aeee-151">An [Azure event hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="6aeee-152">hello [Azure.NET SDK](http://azure.microsoft.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-152">hello [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>

* <span data-ttu-id="6aeee-153">hello [Visual Studio 용 HDInsight 도구](hdinsight-hadoop-visual-studio-tools-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-153">hello [HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="6aeee-154">개발 환경에서 Java JDK 1.8 이상.</span><span class="sxs-lookup"><span data-stu-id="6aeee-154">Java JDK 1.8 or later on your development environment.</span></span> <span data-ttu-id="6aeee-155">JDK 다운로드는 [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-155">JDK downloads are available from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>

  * <span data-ttu-id="6aeee-156">hello **JAVA_HOME** Java 포함 되어 있는 환경 변수 해야 지점 toohello 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-156">hello **JAVA_HOME** environment variable must point toohello directory that contains Java.</span></span>
  * <span data-ttu-id="6aeee-157">hello **%JAVA_HOME%/bin** 디렉터리 hello 경로에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-157">hello **%JAVA_HOME%/bin** directory must be in hello path.</span></span>

## <a name="download-hello-event-hubs-components"></a><span data-ttu-id="6aeee-158">Hello 이벤트 허브 구성 요소 다운로드</span><span class="sxs-lookup"><span data-stu-id="6aeee-158">Download hello Event Hubs components</span></span>

<span data-ttu-id="6aeee-159">다운로드 hello 이벤트 허브 spout 및 구성 요소에서 볼트 [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar)합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-159">Download hello Event Hubs spout and bolt component from [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

<span data-ttu-id="6aeee-160">라는 디렉터리를 만들고 `eventhubspout`, hello 디렉터리로 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-160">Create a directory named `eventhubspout`, and save hello file into hello directory.</span></span>

## <a name="configure-event-hubs"></a><span data-ttu-id="6aeee-161">Event Hubs 구성</span><span class="sxs-lookup"><span data-stu-id="6aeee-161">Configure Event Hubs</span></span>

<span data-ttu-id="6aeee-162">이벤트 허브는이 예제에 대 한 hello 데이터 원본.</span><span class="sxs-lookup"><span data-stu-id="6aeee-162">Event Hubs is hello data source for this example.</span></span> <span data-ttu-id="6aeee-163">Hello 정보를 사용 하 여의 hello "이벤트 허브 만들기" 섹션에 [이벤트 허브 시작](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-163">Use hello information in hello "Create an event hub" section of [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

1. <span data-ttu-id="6aeee-164">Hello 이벤트 허브를 만든 후 보기 hello **EventHub** hello Azure 포털에서 선택에 블레이드 **공유 액세스 정책을**합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-164">After hello event hub has been created, view hello **EventHub** blade in hello Azure portal, and select **Shared access policies**.</span></span> <span data-ttu-id="6aeee-165">선택 **+ 추가** tooadd hello 다음 정책:</span><span class="sxs-lookup"><span data-stu-id="6aeee-165">Select **+ Add** tooadd hello following policies:</span></span>

   | <span data-ttu-id="6aeee-166">이름</span><span class="sxs-lookup"><span data-stu-id="6aeee-166">Name</span></span> | <span data-ttu-id="6aeee-167">권한</span><span class="sxs-lookup"><span data-stu-id="6aeee-167">Permissions</span></span> |
   | --- | --- |
   | <span data-ttu-id="6aeee-168">기록기</span><span class="sxs-lookup"><span data-stu-id="6aeee-168">writer</span></span> |<span data-ttu-id="6aeee-169">보내기</span><span class="sxs-lookup"><span data-stu-id="6aeee-169">Send</span></span> |
   | <span data-ttu-id="6aeee-170">판독기</span><span class="sxs-lookup"><span data-stu-id="6aeee-170">reader</span></span> |<span data-ttu-id="6aeee-171">수신 대기</span><span class="sxs-lookup"><span data-stu-id="6aeee-171">Listen</span></span> |

    ![공유 액세스 정책 창의 스크린샷](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. <span data-ttu-id="6aeee-173">선택 hello **판독기** 및 **기록기** 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-173">Select hello **reader** and **writer** policies.</span></span> <span data-ttu-id="6aeee-174">복사 하 고 이러한 값은 나중에 사용 되는 두 정책 모두에 대 한 hello 기본 키 값을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-174">Copy and save hello primary key value for both policies, as these values are used later.</span></span>

## <a name="configure-hello-eventhubwriter"></a><span data-ttu-id="6aeee-175">Hello EventHubWriter 구성</span><span class="sxs-lookup"><span data-stu-id="6aeee-175">Configure hello EventHubWriter</span></span>

1. <span data-ttu-id="6aeee-176">Visual Studio 용 hello 최신 버전의 hello HDInsight 도구를 아직 설치 하지 있을 경우 참조 [Visual Studio 용 HDInsight 도구를 사용 하 여 시작](hdinsight-hadoop-visual-studio-tools-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-176">If you have not already installed hello latest version of hello HDInsight tools for Visual Studio, see [Get started using HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="6aeee-177">Hello 솔루션에서 다운로드 [eventhub-스톰-하이브리드](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub)합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-177">Download hello solution from [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

3. <span data-ttu-id="6aeee-178">Hello에 **EventHubWriter** 프로젝트, 열기 hello **App.config** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-178">In hello **EventHubWriter** project, open hello **App.config** file.</span></span> <span data-ttu-id="6aeee-179">Hello 키 다음에 대 한 hello 값에서 이전 toofill를 구성 하는 hello 이벤트 허브에서 hello 정보를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="6aeee-179">Use hello information from hello event hub that you configured earlier toofill in hello value for hello following keys:</span></span>

   | <span data-ttu-id="6aeee-180">키</span><span class="sxs-lookup"><span data-stu-id="6aeee-180">Key</span></span> | <span data-ttu-id="6aeee-181">값</span><span class="sxs-lookup"><span data-stu-id="6aeee-181">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="6aeee-182">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="6aeee-182">EventHubPolicyName</span></span> |<span data-ttu-id="6aeee-183">기록기 (hello 정책에 다른 이름을 사용 하는 경우 *보낼* 권한, 대신 사용 합니다.)</span><span class="sxs-lookup"><span data-stu-id="6aeee-183">writer (If you used a different name for hello policy with *Send* permission, use it instead.)</span></span> |
   | <span data-ttu-id="6aeee-184">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="6aeee-184">EventHubPolicyKey</span></span> |<span data-ttu-id="6aeee-185">hello 기록기 정책에 대 한 hello 키입니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-185">hello key for hello writer policy.</span></span> |
   | <span data-ttu-id="6aeee-186">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="6aeee-186">EventHubNamespace</span></span> |<span data-ttu-id="6aeee-187">이벤트 허브를 포함 하는 hello 네임 스페이스</span><span class="sxs-lookup"><span data-stu-id="6aeee-187">hello namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="6aeee-188">EventHubName</span><span class="sxs-lookup"><span data-stu-id="6aeee-188">EventHubName</span></span> |<span data-ttu-id="6aeee-189">이벤트 허브 이름</span><span class="sxs-lookup"><span data-stu-id="6aeee-189">Your event hub name.</span></span> |
   | <span data-ttu-id="6aeee-190">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="6aeee-190">EventHubPartitionCount</span></span> |<span data-ttu-id="6aeee-191">이벤트 허브에 대 한 파티션 hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-191">hello number of partitions in your event hub.</span></span> |

4. <span data-ttu-id="6aeee-192">저장 후 닫기 hello **App.config** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-192">Save and close hello **App.config** file.</span></span>

## <a name="configure-hello-eventhubreader"></a><span data-ttu-id="6aeee-193">Hello EventHubReader 구성</span><span class="sxs-lookup"><span data-stu-id="6aeee-193">Configure hello EventHubReader</span></span>

1. <span data-ttu-id="6aeee-194">열기 hello **EventHubReader** 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="6aeee-194">Open hello **EventHubReader** project.</span></span>

2. <span data-ttu-id="6aeee-195">열기 hello **App.config** hello에 대 한 파일 **EventHubReader**합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-195">Open hello **App.config** file for hello **EventHubReader**.</span></span> <span data-ttu-id="6aeee-196">Hello 키 다음에 대 한 hello 값에서 이전 toofill를 구성 하는 hello 이벤트 허브에서 hello 정보를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="6aeee-196">Use hello information from hello event hub that you configured earlier toofill in hello value for hello following keys:</span></span>

   | <span data-ttu-id="6aeee-197">키</span><span class="sxs-lookup"><span data-stu-id="6aeee-197">Key</span></span> | <span data-ttu-id="6aeee-198">값</span><span class="sxs-lookup"><span data-stu-id="6aeee-198">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="6aeee-199">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="6aeee-199">EventHubPolicyName</span></span> |<span data-ttu-id="6aeee-200">판독기 (hello 정책에 다른 이름을 사용 하는 경우 *수신* 권한, 대신 사용 합니다.)</span><span class="sxs-lookup"><span data-stu-id="6aeee-200">reader (If you used a different name for hello policy with *listen* permission, use it instead.)</span></span> |
   | <span data-ttu-id="6aeee-201">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="6aeee-201">EventHubPolicyKey</span></span> |<span data-ttu-id="6aeee-202">hello 판독기 정책에 대 한 hello 키입니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-202">hello key for hello reader policy.</span></span> |
   | <span data-ttu-id="6aeee-203">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="6aeee-203">EventHubNamespace</span></span> |<span data-ttu-id="6aeee-204">이벤트 허브를 포함 하는 hello 네임 스페이스</span><span class="sxs-lookup"><span data-stu-id="6aeee-204">hello namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="6aeee-205">EventHubName</span><span class="sxs-lookup"><span data-stu-id="6aeee-205">EventHubName</span></span> |<span data-ttu-id="6aeee-206">이벤트 허브 이름</span><span class="sxs-lookup"><span data-stu-id="6aeee-206">Your event hub name.</span></span> |
   | <span data-ttu-id="6aeee-207">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="6aeee-207">EventHubPartitionCount</span></span> |<span data-ttu-id="6aeee-208">이벤트 허브에 대 한 파티션 hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-208">hello number of partitions in your event hub.</span></span> |

3. <span data-ttu-id="6aeee-209">저장 후 닫기 hello **App.config** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-209">Save and close hello **App.config** file.</span></span>

## <a name="deploy-hello-topologies"></a><span data-ttu-id="6aeee-210">Hello 토폴로지를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-210">Deploy hello topologies</span></span>

1. <span data-ttu-id="6aeee-211">**솔루션 탐색기**, 마우스 오른쪽 단추로 클릭 hello **EventHubReader** 프로젝트를 마우스 선택 **HDInsight의 tooStorm 제출**합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-211">From **Solution Explorer**, right-click hello **EventHubReader** project, and select **Submit tooStorm on HDInsight**.</span></span>

    ![스크린샷의 솔루션 탐색기에서 강조 표시 하는 HDInsight의 전송 tooStorm와](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. <span data-ttu-id="6aeee-213">Hello에 **제출 토폴로지** 대화 상자를 선택 하면 **Storm 클러스터**합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-213">On hello **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="6aeee-214">확장 **추가 구성을**선택, **Java 파일 경로**선택, **...** , 및 이전에 다운로드 한 hello JAR 파일이 포함 된 select hello 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-214">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select hello directory that contains hello JAR file that you downloaded earlier.</span></span> <span data-ttu-id="6aeee-215">마지막으로 **제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-215">Finally, click **Submit**.</span></span>

    ![토폴로지 제출 대화 상자의 스크린샷](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. <span data-ttu-id="6aeee-217">Hello 토폴로지가 제출 될 때 hello **스톰 토폴로지 뷰어** 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-217">When hello topology has been submitted, hello **Storm Topologies Viewer** appears.</span></span> <span data-ttu-id="6aeee-218">hello 토폴로지를 선택 하는 hello에 대 한 정보 tooview **EventHubReader** hello 왼쪽된 창에는 토폴로지입니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-218">tooview information about hello topology, select hello **EventHubReader** topology in hello left pane.</span></span>

    ![Storm Topologies Viewer의 스크린샷](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. <span data-ttu-id="6aeee-220">**솔루션 탐색기**, 마우스 오른쪽 단추로 클릭 hello **EventHubWriter** 프로젝트를 마우스 선택 **HDInsight의 tooStorm 제출**합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-220">From **Solution Explorer**, right-click hello **EventHubWriter** project, and select **Submit tooStorm on HDInsight**.</span></span>

5. <span data-ttu-id="6aeee-221">Hello에 **제출 토폴로지** 대화 상자를 선택 하면 **Storm 클러스터**합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-221">On hello **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="6aeee-222">확장 **추가 구성을**선택, **Java 파일 경로**선택, **...** , hello JAR 파일이 포함 된 select hello 디렉터리 이전에 다운로드 한 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-222">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select hello directory that contains hello JAR file you downloaded earlier.</span></span> <span data-ttu-id="6aeee-223">마지막으로 **제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-223">Finally, click **Submit**.</span></span>

6. <span data-ttu-id="6aeee-224">Hello 토폴로지가 제출 될 때 hello에 hello 토폴로지 목록 새로 고침 **스톰 토폴로지 뷰어** tooverify 두 토폴로지 모두 hello 클러스터에서 실행 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-224">When hello topology has been submitted, refresh hello topology list in hello **Storm Topologies Viewer** tooverify that both topologies are running on hello cluster.</span></span>

7. <span data-ttu-id="6aeee-225">**스톰 토폴로지 뷰어**선택, hello **EventHubReader** 토폴로지입니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-225">In **Storm Topologies Viewer**, select hello **EventHubReader** topology.</span></span>

8. <span data-ttu-id="6aeee-226">hello 모양에 대 한 요약 tooopen hello 구성 요소를 두 번 클릭 hello **LogBolt** hello 다이어그램에서 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-226">tooopen hello component summary for hello bolt, double-click hello **LogBolt** component in hello diagram.</span></span>

9. <span data-ttu-id="6aeee-227">Hello에 **Executor** hello에서 hello 링크 중 하나를 선택 하십시오 섹션 **포트** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-227">In hello **Executors** section, select one of hello links in hello **Port** column.</span></span> <span data-ttu-id="6aeee-228">Hello 구성 요소에 의해 기록 된 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-228">This displays information logged by hello component.</span></span> <span data-ttu-id="6aeee-229">hello 기록 정보는 텍스트 다음 유사한 toohello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-229">hello logged information is similar toohello following text:</span></span>

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-hello-topologies"></a><span data-ttu-id="6aeee-230">Hello 토폴로지를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-230">Stop hello topologies</span></span>

<span data-ttu-id="6aeee-231">toostop hello 토폴로지 hello에서 각각의 토폴로지를 선택 **스톰 토폴로지 뷰어**, 클릭 **Kill**합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-231">toostop hello topologies, select each topology in hello **Storm Topology Viewer**, then click **Kill**.</span></span>

![종료 단추가 강조 표시된 Storm Topologies Viewer의 스크린샷](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="6aeee-233">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="6aeee-233">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="6aeee-234">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6aeee-234">Next steps</span></span>

<span data-ttu-id="6aeee-235">이 문서에서는 어떻게 toouse hello Java 이벤트 허브 spout 및 C# 토폴로지 toowork Azure 이벤트 허브의 데이터로에서 볼트 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-235">In this document, you have learned how toouse hello Java Event Hubs spout and bolt from a C# topology toowork with data in Azure Event Hubs.</span></span> <span data-ttu-id="6aeee-236">C# 토폴로지를 만들기에 대 한 더 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aeee-236">toolearn more about creating C# topologies, see hello following:</span></span>

* [<span data-ttu-id="6aeee-237">Visual Studio를 사용하여 HDInsight에서 Apache Storm에 대한 C# 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="6aeee-237">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="6aeee-238">SCP 프로그래밍 가이드</span><span class="sxs-lookup"><span data-stu-id="6aeee-238">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)
* [<span data-ttu-id="6aeee-239">HDInsight의 Storm에 대한 예제 토폴로지</span><span class="sxs-lookup"><span data-stu-id="6aeee-239">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
