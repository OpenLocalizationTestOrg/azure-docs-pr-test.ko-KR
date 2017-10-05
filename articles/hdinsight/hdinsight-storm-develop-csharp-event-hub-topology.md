---
title: "Storm으로 Event Hubs에서 이벤트 처리 - Azure HDInsight | Microsoft Docs"
description: "HDInsight Tools for Visual Studio를 사용하여 Visual Studio에서 만든 C# Storm 토폴로지로 Azure Event Hubs의 데이터를 처리하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 4b6fd87b057d93175d3ef284238d77be3bdde61d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a><span data-ttu-id="e8c9f-103">HDInsight의 Storm(C#)으로 Azure Event Hubs에서 이벤트 처리</span><span class="sxs-lookup"><span data-stu-id="e8c9f-103">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>

<span data-ttu-id="e8c9f-104">HDInsight의 Apache Storm에서 Azure Event Hubs를 사용하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-104">Learn how to work with Azure Event Hubs from Apache Storm on HDInsight.</span></span> <span data-ttu-id="e8c9f-105">이 문서는 C# Storm 토폴로지를 사용하여 Evbent Hubs에서 데이터를 읽고 씁니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-105">This document uses a C# Storm topology to read and write data from Evbent Hubs</span></span>

> [!NOTE]
> <span data-ttu-id="e8c9f-106">이 프로젝트의 Java 버전은 [HDInsight의 Storm(Java)으로 Azure Event Hubs에서 이벤트 처리](hdinsight-storm-develop-java-event-hub-topology.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-106">For a Java version of this project, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="scpnet"></a><span data-ttu-id="e8c9f-107">SCP.NET</span><span class="sxs-lookup"><span data-stu-id="e8c9f-107">SCP.NET</span></span>

<span data-ttu-id="e8c9f-108">이 문서의 단계에서는 NuGet 패키지인 SCP.NET을 사용하여 HDInsight에서 Storm과 함께 사용할 C# 토폴로지 및 구성 요소를 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-108">The steps in this document use SCP.NET, a NuGet package that makes it easy to create C# topologies and components for use with Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8c9f-109">이 문서의 단계에서는 Visual Studio를 사용하는 Windows 개발 환경을 사용하지만 컴파일된 프로젝트는 Linux를 사용하는 HDInsight 클러스터의 Storm에 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-109">While the steps in this document rely on a Windows development environment with Visual Studio, the compiled project can be submitted to a Storm on HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="e8c9f-110">2016년 10월 28일 이후에 만든 Linux 기반 클러스터만 SCP.NET 토폴로지를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-110">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="e8c9f-111">HDInsight 3.4 이상은 Mono를 사용하여 C# 토폴로지를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-111">HDInsight 3.4 and greater use Mono to run C# topologies.</span></span> <span data-ttu-id="e8c9f-112">이 문서에 사용된 예제는 HDInsight 3.6에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-112">The example used in this document works with HDInsight 3.6.</span></span> <span data-ttu-id="e8c9f-113">HDInsight용 .NET 솔루션을 만들 계획인 경우 [Mono 호환성](http://www.mono-project.com/docs/about-mono/compatibility/) 문서에서 잠재적인 비호환성을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-113">If you plan on creating your own .NET solutions for HDInsight, check the [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>

### <a name="cluster-versioning"></a><span data-ttu-id="e8c9f-114">클러스터 버전 관리</span><span class="sxs-lookup"><span data-stu-id="e8c9f-114">Cluster versioning</span></span>

<span data-ttu-id="e8c9f-115">프로젝트에 사용하는 Microsoft.SCP.Net.SDK NuGet 패키지는 HDInsight에 설치된 Storm의 주 버전과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-115">The Microsoft.SCP.Net.SDK NuGet package you use for your project must match the major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="e8c9f-116">HDInsight 버전 3.5 및 3.6은 Storm 1.x를 사용하므로 이 클러스터와 함께 SCP.NET 버전 1.0.x.x를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-116">HDInsight versions 3.5 and 3.6 use Storm 1.x, so you must use SCP.NET version 1.0.x.x with these clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8c9f-117">이 문서의 예제는 HDInsight 3.5 또는 3.6 클러스터를 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-117">The example in this document expects an HDInsight 3.5 or 3.6 cluster.</span></span>
>
> <span data-ttu-id="e8c9f-118">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-118">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e8c9f-119">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="e8c9f-120">C# 토폴로지도 .NET 4.5를 대상으로 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-120">C# topologies must also target .NET 4.5.</span></span>

## <a name="how-to-work-with-event-hubs"></a><span data-ttu-id="e8c9f-121">Event Hubs 작동 방법</span><span class="sxs-lookup"><span data-stu-id="e8c9f-121">How to work with Event Hubs</span></span>

<span data-ttu-id="e8c9f-122">Microsoft는 Storm 토폴로지의 Event Hubs와 통신하는 데 사용할 수 있는 Java 구성 요소 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-122">Microsoft provides a set of Java components that can be used to communicate with Event Hubs from a Storm topology.</span></span> <span data-ttu-id="e8c9f-123">이러한 구성 요소의 HDInsight 3.6 호환 버전이 포함된 Java 아카이브(JAR) 파일을 [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-123">You can find the Java archive (JAR) file that contains an HDInsight 3.6 compatible version of these components at [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8c9f-124">구성 요소는 Java로 작성되지만 C# 토폴로지에서 쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-124">While the components are written in Java, you can easily use them from a C# topology.</span></span>

<span data-ttu-id="e8c9f-125">이 예제에서는 다음 구성 요소가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-125">The following components are used in this example:</span></span>

* <span data-ttu-id="e8c9f-126">__EventHubSpout__: Event Hubs에서 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-126">__EventHubSpout__: Reads data from Event Hubs.</span></span>
* <span data-ttu-id="e8c9f-127">__EventHubBolt__: Event Hubs에 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-127">__EventHubBolt__: Writes data to Event Hubs.</span></span>
* <span data-ttu-id="e8c9f-128">__EventHubSpoutConfig__: EventHubSpout를 구성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-128">__EventHubSpoutConfig__: Used to configure EventHubSpout.</span></span>
* <span data-ttu-id="e8c9f-129">__EventHubBoltConfig__: EventHubBolt를 구성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-129">__EventHubBoltConfig__: Used to configure EventHubBolt.</span></span>

### <a name="example-spout-usage"></a><span data-ttu-id="e8c9f-130">예제 Spout 사용</span><span class="sxs-lookup"><span data-stu-id="e8c9f-130">Example spout usage</span></span>

<span data-ttu-id="e8c9f-131">SCP.NET은 토폴로지에 EventHubSpout를 추가하기 위한 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-131">SCP.NET provides methods for adding an EventHubSpout to your topology.</span></span> <span data-ttu-id="e8c9f-132">이러한 메서드를 사용하면 Java 구성 요소를 추가하기 위한 제네릭 메서드를 사용하는 것보다 더 쉽게 Spout를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-132">These methods make it easier to add a spout than using the generic methods for adding a Java component.</span></span> <span data-ttu-id="e8c9f-133">다음 예제에서는 SCP.NET에서 제공하는 __SetEventHubSpout__ 및 **EventHubSpoutConfig**를 사용하여 Spout를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-133">The following example demonstrates how to create a spout by using the __SetEventHubSpout__ and **EventHubSpoutConfig** methods provided by SCP.NET:</span></span>

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

<span data-ttu-id="e8c9f-134">앞의 예제에서는 __EventHubSpout__라는 새 Spout 구성 요소를 만들고 이벤트 허브와 통신하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-134">The previous example creates a new spout component named __EventHubSpout__, and configures it to communicate with an event hub.</span></span> <span data-ttu-id="e8c9f-135">구성 요소에 대한 병렬 처리 힌트는 이벤트 허브의 파티션 수로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-135">The parallelism hint for the component is set to the number of partitions in the event hub.</span></span> <span data-ttu-id="e8c9f-136">이 설정을 통해 Storm은 각 파티션에 대한 구성 요소의 인스턴스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-136">This setting allows Storm to create an instance of the component for each partition.</span></span>

### <a name="example-bolt-usage"></a><span data-ttu-id="e8c9f-137">예제 Bolt 사용</span><span class="sxs-lookup"><span data-stu-id="e8c9f-137">Example bolt usage</span></span>

<span data-ttu-id="e8c9f-138">**JavaComponmentConstructor** 메서드를 사용하여 Bolt의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-138">Use the **JavaComponmentConstructor** method to create an instance of the bolt.</span></span> <span data-ttu-id="e8c9f-139">다음 예제에서는 **EventHubBolt**의 새 인스턴스를 만들고 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-139">The following example demonstrates how to create and configure a new instance of the **EventHubBolt**:</span></span>

```csharp
// Java construcvtor for the Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set the bolt to subscribe to data from the spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> <span data-ttu-id="e8c9f-140">이 예제에서는 Spout 예제와 같이 **JavaComponentConstructor**를 사용하여 **EventHubBoltConfig**를 만드는 대신 문자열로 전달되는 Clojure 식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-140">This example uses a Clojure expression passed as a string, instead of using **JavaComponentConstructor** to create an **EventHubBoltConfig**, as the spout example did.</span></span> <span data-ttu-id="e8c9f-141">어떤 방법이든 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-141">Either method works.</span></span> <span data-ttu-id="e8c9f-142">자신에게 가장 좋은 것을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-142">Use the method that feels best to you.</span></span>

## <a name="download-the-completed-project"></a><span data-ttu-id="e8c9f-143">완성된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="e8c9f-143">Download the completed project</span></span>

<span data-ttu-id="e8c9f-144">이 자습서에서 만든 프로젝트의 전체 버전은 [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-144">You can download a complete version of the project created in this tutorial from [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span> <span data-ttu-id="e8c9f-145">그러나 이 자습서의 단계에 따라 구성 설정을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-145">However, you still need to provide configuration settings by following the steps in this tutorial.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e8c9f-146">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e8c9f-146">Prerequisites</span></span>

* <span data-ttu-id="e8c9f-147">[HDInsight 클러스터 버전 3.5 또는 3.6의 Apache Storm](hdinsight-apache-storm-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e8c9f-147">An [Apache Storm on HDInsight cluster version 3.5 or 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span></span>

    > [!WARNING]
    > <span data-ttu-id="e8c9f-148">이 문서에서 사용되는 예제에는 HDInsight 버전 3.5 또는 3.6에서 Storm이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-148">The example used in this document requires Storm on HDInsight version 3.5 or 3.6.</span></span> <span data-ttu-id="e8c9f-149">이 내용은 주요 클래스 이름 변경 때문에 이전 버전의 HDInsight에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-149">This does not work with older versions of HDInsight, due to breaking class name changes.</span></span> <span data-ttu-id="e8c9f-150">이전 클러스터에서 작동하는 이 예제의 버전은 [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-150">For a version of this example that works with older clusters, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span></span>

* <span data-ttu-id="e8c9f-151">[Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="e8c9f-151">An [Azure event hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="e8c9f-152">[Azure .NET SDK](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="e8c9f-152">The [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>

* <span data-ttu-id="e8c9f-153">[HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="e8c9f-153">The [HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="e8c9f-154">개발 환경에서 Java JDK 1.8 이상.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-154">Java JDK 1.8 or later on your development environment.</span></span> <span data-ttu-id="e8c9f-155">JDK 다운로드는 [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-155">JDK downloads are available from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>

  * <span data-ttu-id="e8c9f-156">**JAVA_HOME** 환경 변수가 Java를 포함하고 있는 디렉터리를 가리켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-156">The **JAVA_HOME** environment variable must point to the directory that contains Java.</span></span>
  * <span data-ttu-id="e8c9f-157">**%JAVA_HOME%/bin** 디렉터리가 경로에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-157">The **%JAVA_HOME%/bin** directory must be in the path.</span></span>

## <a name="download-the-event-hubs-components"></a><span data-ttu-id="e8c9f-158">Event Hubs 구성 요소 다운로드</span><span class="sxs-lookup"><span data-stu-id="e8c9f-158">Download the Event Hubs components</span></span>

<span data-ttu-id="e8c9f-159">Event Hubs Spout 및 Bolt 구성 요소를 [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar)에서 다운로드하세요.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-159">Download the Event Hubs spout and bolt component from [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

<span data-ttu-id="e8c9f-160">`eventhubspout`라는 디렉터리를 만들고 이 디렉터리에 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-160">Create a directory named `eventhubspout`, and save the file into the directory.</span></span>

## <a name="configure-event-hubs"></a><span data-ttu-id="e8c9f-161">Event Hubs 구성</span><span class="sxs-lookup"><span data-stu-id="e8c9f-161">Configure Event Hubs</span></span>

<span data-ttu-id="e8c9f-162">Event Hubs는 이 예제의 데이터 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-162">Event Hubs is the data source for this example.</span></span> <span data-ttu-id="e8c9f-163">[Event Hubs 시작](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)의 "이벤트 허브 만들기" 섹션에 있는 정보를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-163">Use the information in the "Create an event hub" section of [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

1. <span data-ttu-id="e8c9f-164">이벤트 허브가 생성된 후에는 Azure Portal에서 **EventHub** 블레이드를 보고 **공유 액세스 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-164">After the event hub has been created, view the **EventHub** blade in the Azure portal, and select **Shared access policies**.</span></span> <span data-ttu-id="e8c9f-165">**+ 추가**를 선택하여 다음 정책을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-165">Select **+ Add** to add the following policies:</span></span>

   | <span data-ttu-id="e8c9f-166">이름</span><span class="sxs-lookup"><span data-stu-id="e8c9f-166">Name</span></span> | <span data-ttu-id="e8c9f-167">권한</span><span class="sxs-lookup"><span data-stu-id="e8c9f-167">Permissions</span></span> |
   | --- | --- |
   | <span data-ttu-id="e8c9f-168">기록기</span><span class="sxs-lookup"><span data-stu-id="e8c9f-168">writer</span></span> |<span data-ttu-id="e8c9f-169">보내기</span><span class="sxs-lookup"><span data-stu-id="e8c9f-169">Send</span></span> |
   | <span data-ttu-id="e8c9f-170">판독기</span><span class="sxs-lookup"><span data-stu-id="e8c9f-170">reader</span></span> |<span data-ttu-id="e8c9f-171">수신 대기</span><span class="sxs-lookup"><span data-stu-id="e8c9f-171">Listen</span></span> |

    ![공유 액세스 정책 창의 스크린샷](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. <span data-ttu-id="e8c9f-173">**판독기** 및 **기록기** 정책을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-173">Select the **reader** and **writer** policies.</span></span> <span data-ttu-id="e8c9f-174">이러한 값은 나중에 사용되므로 두 정책에 대한 기본 키 값을 복사 및 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-174">Copy and save the primary key value for both policies, as these values are used later.</span></span>

## <a name="configure-the-eventhubwriter"></a><span data-ttu-id="e8c9f-175">EventHubWriter 구성</span><span class="sxs-lookup"><span data-stu-id="e8c9f-175">Configure the EventHubWriter</span></span>

1. <span data-ttu-id="e8c9f-176">최신 버전의 HDInsight Tools for Visual Studio를 아직 설치하지 않은 경우 [HDInsight Tools for Visual Studio 사용 시작](hdinsight-hadoop-visual-studio-tools-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-176">If you have not already installed the latest version of the HDInsight tools for Visual Studio, see [Get started using HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="e8c9f-177">[eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub)에서 솔루션을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-177">Download the solution from [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

3. <span data-ttu-id="e8c9f-178">**EventHubWriter** 프로젝트에서 **App.config** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-178">In the **EventHubWriter** project, open the **App.config** file.</span></span> <span data-ttu-id="e8c9f-179">앞에서 구성한 이벤트 허브에 대한 정보를 다음 키에 대한 값에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-179">Use the information from the event hub that you configured earlier to fill in the value for the following keys:</span></span>

   | <span data-ttu-id="e8c9f-180">키</span><span class="sxs-lookup"><span data-stu-id="e8c9f-180">Key</span></span> | <span data-ttu-id="e8c9f-181">값</span><span class="sxs-lookup"><span data-stu-id="e8c9f-181">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="e8c9f-182">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="e8c9f-182">EventHubPolicyName</span></span> |<span data-ttu-id="e8c9f-183">기록기(*보내기* 권한이 있는 정책에 다른 이름을 사용한 경우 대신 사용)</span><span class="sxs-lookup"><span data-stu-id="e8c9f-183">writer (If you used a different name for the policy with *Send* permission, use it instead.)</span></span> |
   | <span data-ttu-id="e8c9f-184">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="e8c9f-184">EventHubPolicyKey</span></span> |<span data-ttu-id="e8c9f-185">기록기 정책에 대한 키</span><span class="sxs-lookup"><span data-stu-id="e8c9f-185">The key for the writer policy.</span></span> |
   | <span data-ttu-id="e8c9f-186">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="e8c9f-186">EventHubNamespace</span></span> |<span data-ttu-id="e8c9f-187">이벤트 허브가 포함된 네임스페이스</span><span class="sxs-lookup"><span data-stu-id="e8c9f-187">The namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="e8c9f-188">EventHubName</span><span class="sxs-lookup"><span data-stu-id="e8c9f-188">EventHubName</span></span> |<span data-ttu-id="e8c9f-189">이벤트 허브 이름</span><span class="sxs-lookup"><span data-stu-id="e8c9f-189">Your event hub name.</span></span> |
   | <span data-ttu-id="e8c9f-190">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="e8c9f-190">EventHubPartitionCount</span></span> |<span data-ttu-id="e8c9f-191">이벤트 허브의 파티션 수</span><span class="sxs-lookup"><span data-stu-id="e8c9f-191">The number of partitions in your event hub.</span></span> |

4. <span data-ttu-id="e8c9f-192">**App.config** 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-192">Save and close the **App.config** file.</span></span>

## <a name="configure-the-eventhubreader"></a><span data-ttu-id="e8c9f-193">EventHubReader 구성</span><span class="sxs-lookup"><span data-stu-id="e8c9f-193">Configure the EventHubReader</span></span>

1. <span data-ttu-id="e8c9f-194">**EventHubReader** 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-194">Open the **EventHubReader** project.</span></span>

2. <span data-ttu-id="e8c9f-195">**EventHubReader**에 대한 **App.config** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-195">Open the **App.config** file for the **EventHubReader**.</span></span> <span data-ttu-id="e8c9f-196">앞에서 구성한 이벤트 허브에 대한 정보를 다음 키에 대한 값에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-196">Use the information from the event hub that you configured earlier to fill in the value for the following keys:</span></span>

   | <span data-ttu-id="e8c9f-197">키</span><span class="sxs-lookup"><span data-stu-id="e8c9f-197">Key</span></span> | <span data-ttu-id="e8c9f-198">값</span><span class="sxs-lookup"><span data-stu-id="e8c9f-198">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="e8c9f-199">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="e8c9f-199">EventHubPolicyName</span></span> |<span data-ttu-id="e8c9f-200">판독기(*수신 대기* 권한이 있는 정책에 다른 이름을 사용한 경우 대신 사용)</span><span class="sxs-lookup"><span data-stu-id="e8c9f-200">reader (If you used a different name for the policy with *listen* permission, use it instead.)</span></span> |
   | <span data-ttu-id="e8c9f-201">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="e8c9f-201">EventHubPolicyKey</span></span> |<span data-ttu-id="e8c9f-202">판독기 정책에 대한 키</span><span class="sxs-lookup"><span data-stu-id="e8c9f-202">The key for the reader policy.</span></span> |
   | <span data-ttu-id="e8c9f-203">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="e8c9f-203">EventHubNamespace</span></span> |<span data-ttu-id="e8c9f-204">이벤트 허브가 포함된 네임스페이스</span><span class="sxs-lookup"><span data-stu-id="e8c9f-204">The namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="e8c9f-205">EventHubName</span><span class="sxs-lookup"><span data-stu-id="e8c9f-205">EventHubName</span></span> |<span data-ttu-id="e8c9f-206">이벤트 허브 이름</span><span class="sxs-lookup"><span data-stu-id="e8c9f-206">Your event hub name.</span></span> |
   | <span data-ttu-id="e8c9f-207">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="e8c9f-207">EventHubPartitionCount</span></span> |<span data-ttu-id="e8c9f-208">이벤트 허브의 파티션 수</span><span class="sxs-lookup"><span data-stu-id="e8c9f-208">The number of partitions in your event hub.</span></span> |

3. <span data-ttu-id="e8c9f-209">**App.config** 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-209">Save and close the **App.config** file.</span></span>

## <a name="deploy-the-topologies"></a><span data-ttu-id="e8c9f-210">토폴로지 배포</span><span class="sxs-lookup"><span data-stu-id="e8c9f-210">Deploy the topologies</span></span>

1. <span data-ttu-id="e8c9f-211">**솔루션 탐색기**에서 **EventHubReader** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **HDInsight의 Storm에 제출**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-211">From **Solution Explorer**, right-click the **EventHubReader** project, and select **Submit to Storm on HDInsight**.</span></span>

    ![HDInsight의 Storm에 제출이 강조 표시된 솔루션 탐색기 스크린샷](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. <span data-ttu-id="e8c9f-213">**토폴로지 제출** 대화 상자에서 **Storm 클러스터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-213">On the **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="e8c9f-214">**추가 구성**을 확장하고 **Java 파일 경로**, **...**을 차례로 선택한 다음 이전에 다운로드한 JAR 파일이 포함된 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-214">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select the directory that contains the JAR file that you downloaded earlier.</span></span> <span data-ttu-id="e8c9f-215">마지막으로 **제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-215">Finally, click **Submit**.</span></span>

    ![토폴로지 제출 대화 상자의 스크린샷](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. <span data-ttu-id="e8c9f-217">토폴로지가 제출되었으면 **Storm Topologies Viewer** 가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-217">When the topology has been submitted, the **Storm Topologies Viewer** appears.</span></span> <span data-ttu-id="e8c9f-218">토폴로지 정보를 보려면 왼쪽 창에서 **EventHubReader** 토폴로지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-218">To view information about the topology, select the **EventHubReader** topology in the left pane.</span></span>

    ![Storm Topologies Viewer의 스크린샷](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. <span data-ttu-id="e8c9f-220">**솔루션 탐색기**에서 **EventHubWriter** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **HDInsight의 Storm에 제출**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-220">From **Solution Explorer**, right-click the **EventHubWriter** project, and select **Submit to Storm on HDInsight**.</span></span>

5. <span data-ttu-id="e8c9f-221">**토폴로지 제출** 대화 상자에서 **Storm 클러스터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-221">On the **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="e8c9f-222">**추가 구성**을 확장하고 **Java 파일 경로**, **...**을 차례로 선택한 다음 이전에 다운로드한 JAR 파일이 포함된 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-222">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select the directory that contains the JAR file you downloaded earlier.</span></span> <span data-ttu-id="e8c9f-223">마지막으로 **제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-223">Finally, click **Submit**.</span></span>

6. <span data-ttu-id="e8c9f-224">토폴로지가 제출되었으면 **Storm Topologies Viewer** 에서 토폴로지 목록을 새로 고쳐 두 토폴로지 모두 클러스터에서 실행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-224">When the topology has been submitted, refresh the topology list in the **Storm Topologies Viewer** to verify that both topologies are running on the cluster.</span></span>

7. <span data-ttu-id="e8c9f-225">**Storm Topologies Viewer**에서 **EventHubReader** 토폴로지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-225">In **Storm Topologies Viewer**, select the **EventHubReader** topology.</span></span>

8. <span data-ttu-id="e8c9f-226">Bolt에 대한 구성 요소 요약을 열려면 다이어그램에서 **LogBolt** 구성 요소를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-226">To open the component summary for the bolt, double-click the **LogBolt** component in the diagram.</span></span>

9. <span data-ttu-id="e8c9f-227">**Executors** 섹션에서 **Port** 열의 링크 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-227">In the **Executors** section, select one of the links in the **Port** column.</span></span> <span data-ttu-id="e8c9f-228">그러면 구성 요소가 기록한 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-228">This displays information logged by the component.</span></span> <span data-ttu-id="e8c9f-229">기록된 정보는 다음 텍스트와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-229">The logged information is similar to the following text:</span></span>

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-the-topologies"></a><span data-ttu-id="e8c9f-230">토폴로지 중지</span><span class="sxs-lookup"><span data-stu-id="e8c9f-230">Stop the topologies</span></span>

<span data-ttu-id="e8c9f-231">토폴로지를 중지하려면 **Storm Topology Viewer**에서 각 토폴로지를 선택한 다음 **중단**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-231">To stop the topologies, select each topology in the **Storm Topology Viewer**, then click **Kill**.</span></span>

![종료 단추가 강조 표시된 Storm Topologies Viewer의 스크린샷](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="e8c9f-233">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="e8c9f-233">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="e8c9f-234">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e8c9f-234">Next steps</span></span>

<span data-ttu-id="e8c9f-235">이 문서에서는 C# 토폴로지에서 Java Event Hubs Spout 및 Bolt를 사용하여 Azure Event Hubs의 데이터로 작업하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-235">In this document, you have learned how to use the Java Event Hubs spout and bolt from a C# topology to work with data in Azure Event Hubs.</span></span> <span data-ttu-id="e8c9f-236">C# 토폴로지 만들기에 대해 자세히 알아보려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-236">To learn more about creating C# topologies, see the following:</span></span>

* [<span data-ttu-id="e8c9f-237">Visual Studio를 사용하여 HDInsight에서 Apache Storm에 대한 C# 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="e8c9f-237">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="e8c9f-238">SCP 프로그래밍 가이드</span><span class="sxs-lookup"><span data-stu-id="e8c9f-238">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)
* [<span data-ttu-id="e8c9f-239">HDInsight의 Storm에 대한 예제 토폴로지</span><span class="sxs-lookup"><span data-stu-id="e8c9f-239">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
