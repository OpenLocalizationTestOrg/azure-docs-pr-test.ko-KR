---
title: "Apache Storm 및 HBase를 사용하여 센서 데이터 분석 | Microsoft Docs"
description: "가상 네트워크를 사용하여 Apache Storm에 연결하는 방법을 알아봅니다. HBase와 함께 Storm을 사용하여 이벤트 허브에서 센서 데이터를 처리하고 D3.js를 통해 이를 시각화합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a9a1ac8e-5708-4833-b965-e453815e671f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/09/2017
ms.author: larryfr
ms.openlocfilehash: 0d1cc959c87bd64ed728f8b56c9b9156fa492a8b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a><span data-ttu-id="24046-104">HDInsight(Hadoop)에서 Apache Storm, 이벤트 허브 및 HBase를 사용하여 센서 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="24046-104">Analyze sensor data with Apache Storm, Event Hub, and HBase in HDInsight (Hadoop)</span></span>

<span data-ttu-id="24046-105">HDInsight의 Apache Storm을 사용하여 Azure 이벤트 허브에서 센서 데이터를 처리하는 방법에 대해 알아보니다.</span><span class="sxs-lookup"><span data-stu-id="24046-105">Learn how to use Apache Storm on HDInsight to process sensor data from Azure Event Hub.</span></span> <span data-ttu-id="24046-106">데이터는 HDInsight의 Apache HBase에 저장되며 D3.js를 사용하여 시각화됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-106">The data is then stored into Apache HBase on HDInsight, and visualized using D3.js.</span></span>

<span data-ttu-id="24046-107">이 문서에 사용되는 Azure Resource Manager 템플릿은 리소스 그룹에 여러 Azure 리소스를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="24046-107">The Azure Resource Manager template used in this document demonstrates how to create multiple Azure resources in a resource group.</span></span> <span data-ttu-id="24046-108">템플릿은 Azure Virtual Network, 두 개의 HDInsight 클러스터(Storm 및 HBase) 및 Azure Web App을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24046-108">The template creates an Azure Virtual Network, two HDInsight clusters (Storm and HBase) and an Azure Web App.</span></span> <span data-ttu-id="24046-109">실시간 웹 대시보드의 node.js 구현은 웹앱에 자동으로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-109">A node.js implementation of a real-time web dashboard is automatically deployed to the web app.</span></span>

> [!NOTE]
> <span data-ttu-id="24046-110">이 문서의 정보와 이 문서의 예제에는 HDInsight 버전 3.6이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-110">The information in this document and example in this document require HDInsight version 3.6.</span></span>
>
> <span data-ttu-id="24046-111">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="24046-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="24046-112">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24046-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24046-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="24046-113">Prerequisites</span></span>

* <span data-ttu-id="24046-114">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="24046-114">An Azure subscription.</span></span>
* <span data-ttu-id="24046-115">[Node.js](http://nodejs.org/): 개발 환경에서 로컬로 웹 대시보드를 미리 보는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-115">[Node.js](http://nodejs.org/): Used to preview the web dashboard locally on your development environment.</span></span>
* <span data-ttu-id="24046-116">[Java 및 JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): Storm 토폴로지를 개발하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-116">[Java and the JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): Used to develop the Storm topology.</span></span>
* <span data-ttu-id="24046-117">[Maven](http://maven.apache.org/what-is-maven.html): 프로젝트를 빌드하고 컴파일하고 하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-117">[Maven](http://maven.apache.org/what-is-maven.html): Used to build and compile the project.</span></span>
* <span data-ttu-id="24046-118">[Git](http://git-scm.com/): GitHub에서 프로젝트를 다운로드하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-118">[Git](http://git-scm.com/): Used to download the project from GitHub.</span></span>
* <span data-ttu-id="24046-119">**SSH** 클라이언트: Linux 기반 HDInsight 클러스터에 연결하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-119">An **SSH** client: Used to connect to the Linux-based HDInsight clusters.</span></span> <span data-ttu-id="24046-120">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24046-120">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="24046-121">기존 HDInsight 클러스터가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="24046-121">You do not need an existing HDInsight cluster.</span></span> <span data-ttu-id="24046-122">이 문서의 단계는 다음 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24046-122">The steps in this document create the following resources:</span></span>
> 
> * <span data-ttu-id="24046-123">Azure 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="24046-123">An Azure Virtual Network</span></span>
> * <span data-ttu-id="24046-124">HDInsight 클러스터의 Storm(Linux 기반, 작업자 노드 2개)</span><span class="sxs-lookup"><span data-stu-id="24046-124">A Storm on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="24046-125">HDInsight 클러스터의 HBase(Linux 기반, 작업자 노드 2개)</span><span class="sxs-lookup"><span data-stu-id="24046-125">An HBase on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="24046-126">웹 대시보드를 호스트하는 Azure 웹앱</span><span class="sxs-lookup"><span data-stu-id="24046-126">An Azure Web App that hosts the web dashboard</span></span>

## <a name="architecture"></a><span data-ttu-id="24046-127">아키텍처</span><span class="sxs-lookup"><span data-stu-id="24046-127">Architecture</span></span>

![아키텍처 다이어그램](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

<span data-ttu-id="24046-129">이 예제는 다음 구성 요소로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-129">This example consists of the following components:</span></span>

* <span data-ttu-id="24046-130">**Azure 이벤트 허브**: 센서에서 수집된 데이터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-130">**Azure Event Hubs**: Contains data that is collected from sensors.</span></span>
* <span data-ttu-id="24046-131">**HDInsight의 Storm**: 이벤트 허브의 데이터를 실시간으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-131">**Storm on HDInsight**: Provides real-time processing of data from Event Hub.</span></span>
* <span data-ttu-id="24046-132">**HDInsight의 HBase**: Storm에서 처리된 후에 데이터에 대한 영구 NoSQL 데이터 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-132">**HBase on HDInsight**: Provides a persistent NoSQL data store for data after it has been processed by Storm.</span></span>
* <span data-ttu-id="24046-133">**Azure 가상 네트워크 서비스**: HDInsight의 Storm 클러스터와 HDInsight의 HBase 클러스터 간 보안 통신을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-133">**Azure Virtual Network service**: Enables secure communications between the Storm on HDInsight and HBase on HDInsight clusters.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="24046-134">Java HBase 클라이언트 API를 사용하는 경우에 가상 네트워크가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-134">A virtual network is required when using the Java HBase client API.</span></span> <span data-ttu-id="24046-135">HBase 클러스터에 대한 공용 게이트웨이를 통해 노출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="24046-135">It is not exposed over the public gateway for HBase clusters.</span></span> <span data-ttu-id="24046-136">HBase 및 Storm 클러스터를 동일한 가상 네트워크에 설치하면 Storm 클러스터(또는 가상 네트워크의 다른 시스템)에서 클라이언트 API를 사용하여 HBase에 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24046-136">Installing HBase and Storm clusters into the same virtual network allows the Storm cluster (or any other system on the virtual network) to directly access HBase using client API.</span></span>

* <span data-ttu-id="24046-137">**대시보드 웹 사이트**: 실시간으로 데이터 차트를 작성하는 예제 대시보드입니다.</span><span class="sxs-lookup"><span data-stu-id="24046-137">**Dashboard website**: An example dashboard that charts data in real time.</span></span>
  
  * <span data-ttu-id="24046-138">웹 사이트는 Node.js로 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-138">The website is implemented in Node.js.</span></span>
  * <span data-ttu-id="24046-139">[Socket.io](http://socket.io/) 는 Storm 토폴로지와 웹 사이트 간의 실시간 통신에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-139">[Socket.io](http://socket.io/) is used for real-time communication between the Storm topology and the website.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="24046-140">통신에 Socket.io를 사용하는 것은 구현 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="24046-140">Using Socket.io for communication is an implementation detail.</span></span> <span data-ttu-id="24046-141">원시 WebSocket 또는 SignalR과 같은 모든 통신 프레임워크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24046-141">You can use any communications framework, such as raw WebSockets or SignalR.</span></span>

  * <span data-ttu-id="24046-142">[D3.js](http://d3js.org/) 는 웹 사이트로 전송되는 데이터의 그래프를 작성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-142">[D3.js](http://d3js.org/) is used to graph the data that is sent to the website.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="24046-143">Storm 및 HBase 모두에 대해 하나의 HDInsight 클러스터를 만드는 지원 방법이 없으므로 두 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-143">Two clusters are required, as there is no supported method to create one HDInsight cluster for both Storm and HBase.</span></span>

<span data-ttu-id="24046-144">이 토폴로지는 [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) 클래스를 사용하여 이벤트 허브에서 데이터를 읽고 [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) 클래스를 사용하여 HBase에 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="24046-144">The topology reads data from Event Hub by using the [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) class, and writes data into HBase using the [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) class.</span></span> <span data-ttu-id="24046-145">웹 사이트와의 통신은 [socket.io-client.java](https://github.com/nkzawa/socket.io-client.java)를 사용하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-145">Communication with the website is accomplished by using [socket.io-client.java](https://github.com/nkzawa/socket.io-client.java).</span></span>

<span data-ttu-id="24046-146">다음 다이어그램은 토폴로지 레이아웃을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-146">The following diagram explains the layout of the topology:</span></span>

![토폴로지 다이어그램](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> <span data-ttu-id="24046-148">이 다이어그램은 토폴로지를 단순화한 그림입니다.</span><span class="sxs-lookup"><span data-stu-id="24046-148">This diagram is a simplified view of the topology.</span></span> <span data-ttu-id="24046-149">Event Hub의 각 파티션에 대해 각 구성 요소의 인스턴스가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="24046-149">An instance of each component is created for each partition in your Event Hub.</span></span> <span data-ttu-id="24046-150">이러한 인스턴스는 클러스터의 노드에 분산되며 노드 간에 다음과 같이 데이터가 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-150">These instances are distributed across the nodes in the cluster, and data is routed between them as follows:</span></span>
> 
> * <span data-ttu-id="24046-151">Spout에서 파서로 전송되는 데이터는 부하 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-151">Data from the spout to the parser is load balanced.</span></span>
> * <span data-ttu-id="24046-152">파서에서 대시보드 및 HBase로 전송되는 데이터는 장치 ID별로 그룹화되므로 같은 장치의 메시지는 항상 동일한 구성 요소로 흐릅니다.</span><span class="sxs-lookup"><span data-stu-id="24046-152">Data from the parser to the Dashboard and HBase is grouped by Device ID, so that messages from the same device always flow to the same component.</span></span>

### <a name="topology-components"></a><span data-ttu-id="24046-153">토폴로지 구성 요소</span><span class="sxs-lookup"><span data-stu-id="24046-153">Topology components</span></span>

* <span data-ttu-id="24046-154">**Event Hub Spout**: Spout는 Apache Storm 버전 0.10.0 이상의 일부로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-154">**Event Hub Spout**: The spout is provided as part of Apache Storm version 0.10.0 and higher.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="24046-155">이 예제에서 사용되는 Event Hub Spout에는 HDInsight 클러스터 버전 3.5 또는 3.6에 대한 Storm이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-155">The Event Hub spout used in this example requires a Storm on HDInsight cluster version 3.5 or 3.6.</span></span>

* <span data-ttu-id="24046-156">**ParserBolt.java**: Spout에서 내보내는 데이터는 원시 JSON이며, 한 번에 둘 이상의 이벤트를 내보낼 때도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24046-156">**ParserBolt.java**: The data that is emitted by the spout is raw JSON, and occasionally more than one event is emitted at a time.</span></span> <span data-ttu-id="24046-157">이 Bolt는 Spout에서 내보내는 데이터를 읽고 JSON 메시지를 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-157">This bolt reads the data emitted by the spout and parses the JSON message.</span></span> <span data-ttu-id="24046-158">그런 다음 Bolt는 여러 필드를 포함하는 튜플로써 데이터를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="24046-158">The bolt then emits the data as a tuple that contains multiple fields.</span></span>
* <span data-ttu-id="24046-159">**DashboardBolt.java**: 이 구성 요소는 Java용 Socket.io 클라이언트 라이브러리를 사용하여 웹 대시보드로 데이터를 실시간으로 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="24046-159">**DashboardBolt.java**: This component demonstrates how to use the Socket.io client library for Java to send data in real time to the web dashboard.</span></span>
* <span data-ttu-id="24046-160">**no-hbase.yaml**: 로컬 모드에서 실행할 때 사용되는 토폴로지 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="24046-160">**no-hbase.yaml**: The topology definition used when running in local mode.</span></span> <span data-ttu-id="24046-161">HBase 구성 요소를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="24046-161">It does not use HBase components.</span></span>
* <span data-ttu-id="24046-162">**with-hbase.yaml**: 클러스터에서 토폴로지를 실행할 때 사용되는 토폴로지 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="24046-162">**with-hbase.yaml**: The topology definition used when running the topology on the cluster.</span></span> <span data-ttu-id="24046-163">HBase 구성 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-163">It does use HBase components.</span></span>
* <span data-ttu-id="24046-164">**dev.properties**: Event Hub Spout, HBase Bolt 및 대시보드 구성 요소에 대한 구성 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="24046-164">**dev.properties**: The configuration information for the Event Hub spout, HBase bolt, and dashboard components.</span></span>

## <a name="prepare-your-environment"></a><span data-ttu-id="24046-165">환경 준비</span><span class="sxs-lookup"><span data-stu-id="24046-165">Prepare your environment</span></span>

<span data-ttu-id="24046-166">이 예제를 사용하려면 먼저 Storm 토폴로지에서 읽을 Azure 이벤트 허브를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-166">Before you use this example, you must create an Azure Event Hub, which the Storm topology reads from.</span></span>

### <a name="configure-event-hub"></a><span data-ttu-id="24046-167">이벤트 허브 구성</span><span class="sxs-lookup"><span data-stu-id="24046-167">Configure Event Hub</span></span>

<span data-ttu-id="24046-168">이벤트 허브는 이 예제의 데이터 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="24046-168">Event Hub is the data source for this example.</span></span> <span data-ttu-id="24046-169">다음 단계에 따라 이벤트 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24046-169">Use the following steps to create an Event Hub.</span></span>

1. <span data-ttu-id="24046-170">[Azure Portal](https://portal.azure.com)에서 **+ 새로 만들기** -> **사물 인터넷** -> **Event Hubs**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-170">From the [Azure portal](https://portal.azure.com), select **+ New** -> **Internet of Things** -> **Event Hubs**.</span></span>
2. <span data-ttu-id="24046-171">**네임스페이스 만들기** 섹션에서 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-171">In the **Create Namespace** section, perform the following tasks:</span></span>
   
   1. <span data-ttu-id="24046-172">네임스페이스의 **이름** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-172">Enter a **Name** for the namespace.</span></span>
   2. <span data-ttu-id="24046-173">가격 책정 계층을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-173">Select a pricing tier.</span></span> <span data-ttu-id="24046-174">**기본** 이면 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-174">**Basic** is sufficient for this example.</span></span>
   3. <span data-ttu-id="24046-175">사용할 Azure **구독** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-175">Select the Azure **Subscription** to use.</span></span>
   4. <span data-ttu-id="24046-176">기존 리소스 그룹을 선택하거나 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24046-176">Either select an existing resource group or create a new one.</span></span>
   5. <span data-ttu-id="24046-177">Event Hub의 **위치** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-177">Select the **Location** for the Event Hub.</span></span>
   6. <span data-ttu-id="24046-178">**대시보드에 고정**을 선택하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-178">Select **Pin to dashboard**, and then click **Create**.</span></span>

3. <span data-ttu-id="24046-179">만들기 프로세스가 완료되면 네임스페이스에 대한 Event Hubs 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-179">When the creation process completes, the Event Hubs information for your namespace is displayed.</span></span> <span data-ttu-id="24046-180">여기에서 **+ Event Hub 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-180">From here, select **+ Add Event Hub**.</span></span> <span data-ttu-id="24046-181">**Event Hub 만들기** 섹션에서 **sensordata**의 이름을 입력한 다음 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-181">In the **Create Event Hub** section, enter a name of **sensordata**, and then select **Create**.</span></span> <span data-ttu-id="24046-182">다른 필드는 기본값으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="24046-182">Leave the other fields at the default values.</span></span>
4. <span data-ttu-id="24046-183">네임스페이스에 대한 Event Hubs 보기에서 **Event Hubs**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-183">From the Event Hubs view for your namespace, select **Event Hubs**.</span></span> <span data-ttu-id="24046-184">**sensordata** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-184">Select the **sensordata** entry.</span></span>
5. <span data-ttu-id="24046-185">sensordata Event Hub에서 **공유 액세스 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-185">From the sensordata Event Hub, select **Shared access policies**.</span></span> <span data-ttu-id="24046-186">**+ 추가** 링크를 사용하여 다음 정책에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-186">Use the **+ Add** link to add the following policies:</span></span>

    | <span data-ttu-id="24046-187">정책 이름</span><span class="sxs-lookup"><span data-stu-id="24046-187">Policy name</span></span> | <span data-ttu-id="24046-188">클레임</span><span class="sxs-lookup"><span data-stu-id="24046-188">Claims</span></span> |
    | ----- | ----- |
    | <span data-ttu-id="24046-189">devices</span><span class="sxs-lookup"><span data-stu-id="24046-189">devices</span></span> | <span data-ttu-id="24046-190">보내기</span><span class="sxs-lookup"><span data-stu-id="24046-190">Send</span></span> |
    | <span data-ttu-id="24046-191">storm</span><span class="sxs-lookup"><span data-stu-id="24046-191">storm</span></span> | <span data-ttu-id="24046-192">수신 대기</span><span class="sxs-lookup"><span data-stu-id="24046-192">Listen</span></span> |

1. <span data-ttu-id="24046-193">두 정책을 모두 선택하고 **기본 키** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="24046-193">Select both policies and make a note of the **PRIMARY KEY** value.</span></span> <span data-ttu-id="24046-194">이후 단계에서 두 정책에 대한 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-194">You need the value for both policies in future steps.</span></span>

## <a name="download-and-configure-the-project"></a><span data-ttu-id="24046-195">프로젝트 다운로드 및 구성</span><span class="sxs-lookup"><span data-stu-id="24046-195">Download and configure the project</span></span>

<span data-ttu-id="24046-196">다음을 사용하여 GitHub에서 프로젝트를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-196">Use the following to download the project from GitHub.</span></span>

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

<span data-ttu-id="24046-197">명령이 완료되면 다음 디렉터리 구조가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-197">After the command completes, you have the following directory structure:</span></span>

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains the topology
            resources/
                log4j2.xml - set logging to minimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO to the web dashboard.
        dashboard/nodejs/ - this is the node.js web dashboard.
        SendEvents/ - utilities to send fake sensor data.

> [!NOTE]
> <span data-ttu-id="24046-198">이 문서에서는 이 예제에 포함된 코드에 대해 자세히 알아보지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="24046-198">This document does not go in to full details of the code included in this example.</span></span> <span data-ttu-id="24046-199">그러나 코드는 완전히 주석 처리되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24046-199">However, the code is fully commented.</span></span>

<span data-ttu-id="24046-200">Event Hub에서 읽는 프로젝트를 구성하려면 `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` 파일을 열고 다음 줄에 Event Hub 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-200">To configure the project to read from Event Hub, open the `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` file and add your Event Hub information to the following lines:</span></span>

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a><span data-ttu-id="24046-201">로컬로 컴파일 및 테스트</span><span class="sxs-lookup"><span data-stu-id="24046-201">Compile and test locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="24046-202">토폴로지를 로컬로 사용하려면 작동 가능한 Storm 개발 환경이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-202">Using the topology locally requires a working Storm development environment.</span></span> <span data-ttu-id="24046-203">자세한 내용은 Apache.org에서 [Storm 개발 환경 설정](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24046-203">For more information, see [Setting up a Storm development environment](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) at Apache.org.</span></span>

> [!WARNING]
> <span data-ttu-id="24046-204">Windows 개발 환경을 사용하는 경우 토폴로지를 로컬로 실행할 때 `java.io.IOException`을 수신할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24046-204">If you are using a Windows development environment, you may receive a `java.io.IOException` when running the topology locally.</span></span> <span data-ttu-id="24046-205">이 경우 HDInsight에서 토폴로지를 실행하기 위해 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-205">If so, move on to running the topology on HDInsight.</span></span>

<span data-ttu-id="24046-206">테스트하기 전에 대시보드를 시작하여 토폴로지의 출력을 확인하고 이벤트 허브에 저장할 데이터를 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-206">Before testing, you must start the dashboard to view the output of the topology and generate data to store in Event Hub.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="24046-207">이 토폴로지의 HBase 구성 요소는 로컬로 테스트하는 경우에 활성화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="24046-207">The HBase component of this topology is not active when testing locally.</span></span> <span data-ttu-id="24046-208">HBase 클러스터의 Java API는 클러스터를 포함하는 Azure Virtual Network 외부에서 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="24046-208">The Java API for the HBase cluster cannot be accessed from outside the Azure Virtual Network that contains the clusters.</span></span>

### <a name="start-the-web-application"></a><span data-ttu-id="24046-209">웹 응용 프로그램 시작</span><span class="sxs-lookup"><span data-stu-id="24046-209">Start the web application</span></span>

1. <span data-ttu-id="24046-210">명령 프롬프트를 열고 디렉터리를 `hdinsight-eventhub-example/dashboard`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-210">Open a command prompt and change directories to `hdinsight-eventhub-example/dashboard`.</span></span> <span data-ttu-id="24046-211">다음 명령을 사용하여 웹 응용 프로그램에서 필요한 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-211">Use the following command to install the dependencies needed by the web application:</span></span>
   
    ```bash
    npm install
    ```

2. <span data-ttu-id="24046-212">다음 명령을 사용하여 웹 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-212">Use the following command to start the web application:</span></span>
   
    ```bash
    node server.js
    ```
   
    <span data-ttu-id="24046-213">다음 텍스트와 유사한 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-213">You see a message similar to the following text:</span></span>
   
        Server listening at port 3000

3. <span data-ttu-id="24046-214">웹 브라우저를 열고 주소로 `http://localhost:3000/`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-214">Open a web browser and enter `http://localhost:3000/` as the address.</span></span> <span data-ttu-id="24046-215">다음 이미지와 유사한 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-215">A page similar to the following image is displayed:</span></span>
   
    ![웹 대시보드](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    <span data-ttu-id="24046-217">이 명령 프롬프트는 계속 열어 두세요.</span><span class="sxs-lookup"><span data-stu-id="24046-217">Leave this command prompt open.</span></span> <span data-ttu-id="24046-218">테스트 후 Ctrl+C를 사용하여 웹 서버를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-218">After testing, use Ctrl-C to stop the web server.</span></span>

### <a name="generate-data"></a><span data-ttu-id="24046-219">데이터 생성</span><span class="sxs-lookup"><span data-stu-id="24046-219">Generate data</span></span>

> [!NOTE]
> <span data-ttu-id="24046-220">이 섹션의 단계에서는 모든 플랫폼에서 사용할 수 있도록 Node.js를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-220">The steps in this section use Node.js so that they can be used on any platform.</span></span> <span data-ttu-id="24046-221">다른 언어 예제는 `SendEvents` 디렉터리를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24046-221">For other language examples, see the `SendEvents` directory.</span></span>

1. <span data-ttu-id="24046-222">새 프롬프트, 셸 또는 터미널을 열고 디렉터리를 `hdinsight-eventhub-example/SendEvents/nodejs`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-222">Open a new prompt, shell, or terminal, and change directories to `hdinsight-eventhub-example/SendEvents/nodejs`.</span></span> <span data-ttu-id="24046-223">응용 프로그램에서 필요한 종속성을 설치하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-223">To install the dependencies needed by the application, use the following command:</span></span>

    ```bash
    npm install
    ```

2. <span data-ttu-id="24046-224">텍스트 편집기에서 `app.js` 파일을 열고 이전에 가져온 Event Hub 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-224">Open the `app.js` file in a text editor and add the Event Hub information you obtained earlier:</span></span>
   
    ```javascript
    // ServiceBus Namespace
    var namespace = 'YourNamespace';
    // Event Hub Name
    var hubname ='sensordata';
    // Shared access Policy name and key (from Event Hub configuration)
    var my_key_name = 'devices';
    var my_key = 'YourKey';
    ```
   
   > [!NOTE]
   > <span data-ttu-id="24046-225">이 예제에서는 Event Hub의 이름으로 `sensordata`를 사용했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-225">This example assumes that you have used `sensordata` as the name of your Event Hub.</span></span> <span data-ttu-id="24046-226">해당 `devices`는 `Send` 클레임을 갖는 정책의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="24046-226">And that `devices` as the name of the policy that has a `Send` claim.</span></span>

3. <span data-ttu-id="24046-227">다음 명령을 사용하여 이벤트 허브에 새 항목을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-227">Use the following command to insert new entries in Event Hub:</span></span>
   
    ```bash
    node app.js
    ```
   
    <span data-ttu-id="24046-228">Event Hub로 전송된 데이터가 포함된 여러 줄의 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-228">You see several lines of output that contain the data sent to Event Hub:</span></span>
   
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"0","Temperature":7}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"1","Temperature":39}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"2","Temperature":86}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"3","Temperature":29}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"4","Temperature":30}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"5","Temperature":5}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"6","Temperature":24}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"7","Temperature":40}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"8","Temperature":43}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"9","Temperature":84}

### <a name="build-and-start-the-topology"></a><span data-ttu-id="24046-229">토폴로지 빌드 및 시작</span><span class="sxs-lookup"><span data-stu-id="24046-229">Build and start the topology</span></span>

1. <span data-ttu-id="24046-230">새 명령 프롬프트를 열고 디렉터리를 `hdinsight-eventhub-example/TemperatureMonitor`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-230">Open a new command prompt and change directories to `hdinsight-eventhub-example/TemperatureMonitor`.</span></span> <span data-ttu-id="24046-231">토폴로지를 빌드하고 패키지하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-231">To build and package the topology, use the following command:</span></span> 

    ```bash
    mvn clean package
    ```

2. <span data-ttu-id="24046-232">토폴로지를 로컬 모드로 시작하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-232">To start the topology in local mode, use the following command:</span></span>

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * <span data-ttu-id="24046-233">`--local`은 토폴로지를 로컬 모드로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-233">`--local` starts the topology in local mode.</span></span>
    * <span data-ttu-id="24046-234">`--filter`는 `dev.properties` 파일을 사용하여 토폴로지 정의의 매개 변수를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="24046-234">`--filter` uses the `dev.properties` file to populate parameters in the topology definition.</span></span>
    * <span data-ttu-id="24046-235">`resources/no-hbase.yaml`은 `no-hbase.yaml` 토폴로지 정의를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-235">`resources/no-hbase.yaml` uses the `no-hbase.yaml` topology definition.</span></span>
 
   <span data-ttu-id="24046-236">일단 시작되면 토폴로지는 Event Hub에서 항목을 읽고 로컬 컴퓨터에서 실행되는 대시보드에 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-236">Once started, the topology reads entries from Event Hub, and sends them to the dashboard running on your local machine.</span></span> <span data-ttu-id="24046-237">웹 대시보드에 다음 이미지와 유사한 줄이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-237">You should see lines appear in the web dashboard, similar to the following image:</span></span>
   
    ![데이터가 표시된 대시보드](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. <span data-ttu-id="24046-239">이벤트 허브가 실행 중인 동안 이전 단계의 `node app.js` 명령을 사용하여 새 데이터를 대시보드로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="24046-239">While the dashboard is running, use the `node app.js` command from the previous steps to send new data to Event Hubs.</span></span> <span data-ttu-id="24046-240">온도 값은 임의로 생성되기 때문에 큰 온도 변화를 표시하도록 그래프가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-240">Because the temperature values are randomly generated, the graph should update to show large changes in temperature.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="24046-241">`node app.js` 명령을 사용할 때 **hdinsight-eventhub-example/SendEvents/Nodejs** 디렉터리에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-241">You must be in the **hdinsight-eventhub-example/SendEvents/Nodejs** directory when using the `node app.js` command.</span></span>

3. <span data-ttu-id="24046-242">대시보드가 업데이트되는지 확인한 후에 Ctrl+C를 사용하여 토폴로지를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-242">After verifying that the dashboard updates, stop the topology using Ctrl+C.</span></span> <span data-ttu-id="24046-243">Ctrl+C를 사용하여 로컬 웹 서버를 중지할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24046-243">You can use Ctrl+C to stop the local web server also.</span></span>

## <a name="create-a-storm-and-hbase-cluster"></a><span data-ttu-id="24046-244">Storm 및 HBase 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="24046-244">Create a Storm and HBase cluster</span></span>

<span data-ttu-id="24046-245">이 섹션의 단계에서는 [Azure Resource Manager 템플릿](../azure-resource-manager/resource-group-template-deploy.md)을 사용하여 Azure Virtual Network를 만들고 해당 가상 네트워크에서 Storm 및 HBase 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24046-245">The steps in this section use an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) to create an Azure Virtual Network and a Storm and HBase cluster on the virtual network.</span></span> <span data-ttu-id="24046-246">또한 이 템플릿은 Azure 웹앱을 만들고 대시보드의 복사본을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-246">The template also creates an Azure Web App and deploys a copy of the dashboard into it.</span></span>

> [!NOTE]
> <span data-ttu-id="24046-247">가상 네트워크는 Storm 클러스터에서 실행되는 토폴로지가 HBase Java API를 사용하여 HBase 클러스터와 직접 통신할 수 있도록 하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-247">A virtual network is used so that the topology running on the Storm cluster can directly communicate with the HBase cluster using the HBase Java API.</span></span>

<span data-ttu-id="24046-248">이 문서에 사용되는 Resource Manager 템플릿은 **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**의 공용 Blob 컨테이너에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24046-248">The Resource Manager template used in this document is located in a public blob container at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span></span>

1. <span data-ttu-id="24046-249">Azure에 로그인하고 Azure Portal에서 Azure Resource Manager 템플릿을 열려면 다음 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-249">Click the following button to sign in to Azure and open the Resource Manager template in the Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. <span data-ttu-id="24046-250">**사용자 지정 배포** 섹션에서 다음 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-250">From the **Custom deployment** section, enter the following values:</span></span>
   
    ![HDInsight 매개 변수](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * <span data-ttu-id="24046-252">**기본 클러스터 이름**: 이 값은 Storm 및 HBase 클러스터의 기본 이름으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-252">**Base Cluster Name**: This value is used as the base name for the Storm and HBase clusters.</span></span> <span data-ttu-id="24046-253">예를 들어 **abc**를 입력하면 **storm-abc**라는 Storm 클러스터와 **hbase-abc**라는 HBase 클러스터가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-253">For example, entering **abc** creates a Storm cluster named **storm-abc** and an HBase cluster named **hbase-abc**.</span></span>
   * <span data-ttu-id="24046-254">**클러스터 로그인 사용자 이름**: Storm 및 HBase 클러스터의 관리자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="24046-254">**Cluster Login User Name**: The admin user name for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="24046-255">**클러스터 로그인 암호**: Storm 및 HBase 클러스터의 관리자 사용자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="24046-255">**Cluster Login Password**: The admin user password for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="24046-256">**SSH 사용자 이름**: Storm 및 HBase 클러스터를 만들기 위한 SSH 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="24046-256">**SSH User Name**: The SSH user to create for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="24046-257">**SSH 암호**: Storm 및 HBase 클러스터에 대한 SSH 사용자의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="24046-257">**SSH Password**: The password for the SSH user for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="24046-258">**위치**: 클러스터가 만들어지는 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="24046-258">**Location**: The region that the clusters are created in.</span></span>
     
     <span data-ttu-id="24046-259">**확인** 을 클릭하여 매개 변수를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-259">Click **OK** to save the parameters.</span></span>

3. <span data-ttu-id="24046-260">**기본** 섹션에서 리소스 그룹을 만들거나 기존 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-260">Use the **Basics** section to create a resource group or select an existing one.</span></span>
4. <span data-ttu-id="24046-261">**리소스 그룹 위치** 드롭다운 메뉴에서 **설정** 섹션의 **위치** 매개 변수에 대해 선택한 것과 동일한 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-261">In the **Resource group location** dropdown menu, select the same location as you selected for the **Location** parameter in the **Settings** section.</span></span>
5. <span data-ttu-id="24046-262">사용 약관을 읽은 다음 **위에 명시된 사용 약관에 동의함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-262">Read the terms and conditions, and then select **I agree to the terms and conditions stated above**.</span></span>
6. <span data-ttu-id="24046-263">마지막으로 **대시보드에 고정**을 선택한 다음 **구매**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-263">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="24046-264">클러스터를 만드는 데 약 20분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="24046-264">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="24046-265">리소스를 만들었으면 리소스 그룹에 대한 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-265">Once the resources have been created, information about the resource group is displayed.</span></span>

![vnet 및 클러스터에 대한 리소스 그룹](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="24046-267">HDInsight 클러스터의 이름은 **storm-BASENAME** 및 **hbase-BASENAME**입니다. 여기서 BASENAME은 템플릿에 제공된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="24046-267">Notice that the names of the HDInsight clusters are **storm-BASENAME** and **hbase-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="24046-268">이후 단계에서 클러스터에 연결할 때 이러한 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-268">You use these names in a later step when connecting to the clusters.</span></span> <span data-ttu-id="24046-269">또한 대시보드 사이트의 이름은 **basename-dashboard**입니다.</span><span class="sxs-lookup"><span data-stu-id="24046-269">Also note that the name of the dashboard site is **basename-dashboard**.</span></span> <span data-ttu-id="24046-270">이 값은 이 문서의 뒷부분에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-270">This value is used later in this document.</span></span>

## <a name="configure-the-dashboard-bolt"></a><span data-ttu-id="24046-271">대시보드 bolt 구성</span><span class="sxs-lookup"><span data-stu-id="24046-271">Configure the Dashboard bolt</span></span>

<span data-ttu-id="24046-272">웹앱으로 배포된 대시보드에 데이터를 보내려면 `dev.properties` 파일에서 다음 줄을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-272">To send data to the dashboard deployed as a web app, you must modify the following line in the `dev.properties`file:</span></span>

```yaml
dashboard.uri: http://localhost:3000
```

<span data-ttu-id="24046-273">`http://localhost:3000`을 `http://BASENAME-dashboard.azurewebsites.net`으로 변경하고 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-273">Change `http://localhost:3000` to `http://BASENAME-dashboard.azurewebsites.net` and save the file.</span></span> <span data-ttu-id="24046-274">**BASENAME** 을 이전 단계에서 제공한 기본 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="24046-274">Replace **BASENAME** with the base name you provided in the previous step.</span></span> <span data-ttu-id="24046-275">또한 이전에 만든 리소스 그룹을 사용하여 대시보드를 선택하고 URL을 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24046-275">You can also use the resource group created previously to select the dashboard and view the URL.</span></span>

## <a name="create-the-hbase-table"></a><span data-ttu-id="24046-276">HBase 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="24046-276">Create the HBase table</span></span>

<span data-ttu-id="24046-277">HBase에 데이터를 저장하려면 먼저 테이블을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-277">To store data in HBase, we must first create a table.</span></span> <span data-ttu-id="24046-278">Storm 토폴로지 내에서 리소스를 만들려고 하면 여러 인스턴스가 동일한 리소스를 만들려고 할 수 있으므로 Storm이 데이터를 써야 하는 리소스를 미리 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24046-278">Pre-create resources that Storm needs to write to, as trying to create resources from inside a Storm topology can result in multiple instances trying to create the same resource.</span></span> <span data-ttu-id="24046-279">토폴로지 외부에 리소스를 만들고 읽기/쓰기 및 분석에 Storm을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-279">Create the resources outside the topology and use Storm for reading/writing and analytics.</span></span>

1. <span data-ttu-id="24046-280">SSH를 사용하여 클러스터 생성 중에 템플릿에 제공한 SSH 사용자 이름 및 암호를 사용하여 HBase 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-280">Use SSH to connect to the HBase cluster using the SSH user and password you supplied to the template during cluster creation.</span></span> <span data-ttu-id="24046-281">예를 들어 `ssh` 명령을 사용하여 연결하는 경우 다음 구문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-281">For example, if connecting using the `ssh` command, you would use the following syntax:</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    <span data-ttu-id="24046-282">`sshuser`를 클러스터를 만들 때 제공했던 SSH 사용자 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="24046-282">Replace `sshuser` with the SSH user name you provided when creating the cluster.</span></span> <span data-ttu-id="24046-283">`clustername`을 HBase 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="24046-283">Replace `clustername` with the HBase cluster name.</span></span>

2. <span data-ttu-id="24046-284">SSH 세션에서 HBase 셸을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-284">From the SSH session, start the HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="24046-285">셸이 로드되면 `hbase(main):001:0>` 프롬프트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-285">Once the shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="24046-286">HBase 셸에서 다음 명령을 입력하여 센서 데이터를 저장할 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24046-286">From the HBase shell, enter the following command to create a table to store the sensor data:</span></span>
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. <span data-ttu-id="24046-287">다음 명령을 사용하여 테이블이 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-287">Verify that the table has been created by using the following command:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="24046-288">이렇게 하면 테이블에 0개의 행이 있음을 나타내는 다음 예제와 비슷한 정보가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-288">This returns information similar to the following example, indicating that there are 0 rows in the table.</span></span>
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. <span data-ttu-id="24046-289">`exit`를 눌러 HBase 셸을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-289">Enter `exit` to exit the HBase shell:</span></span>

## <a name="configure-the-hbase-bolt"></a><span data-ttu-id="24046-290">HBase bolt 구성</span><span class="sxs-lookup"><span data-stu-id="24046-290">Configure the HBase bolt</span></span>

<span data-ttu-id="24046-291">Storm 클러스터에서 HBase에 쓰려면 HBase 클러스터의 구성 세부 정보를 HBase bolt에 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-291">To write to HBase from the Storm cluster, you must provide the HBase bolt with the configuration details of your HBase cluster.</span></span>

1. <span data-ttu-id="24046-292">다음 예제 중 하나를 사용하여 HBase 클러스터에 대한 Zookeeper 쿼럼을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-292">Use one of the following examples to retrieve the Zookeeper quorum for your HBase cluster:</span></span>

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > <span data-ttu-id="24046-293">`your_HDInsight_cluster_name` 을 HDInsight 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="24046-293">Replace `your_HDInsight_cluster_name` with the name of your HDInsight cluster.</span></span> <span data-ttu-id="24046-294">`jq` 유틸리티 설치에 대한 자세한 내용은 [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-294">For more information on installing the `jq` utility, see [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span></span>
    >
    > <span data-ttu-id="24046-295">메시지가 표시되면 HDInsight 관리자 로그인의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-295">When prompted, enter the password for the HDInsight admin login.</span></span>

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > <span data-ttu-id="24046-296">‘your_HDInsight_cluster_name’을 HDInsight 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="24046-296">Replace \`your_HDInsight_cluster_name with the name of your HDInsight cluster.</span></span> <span data-ttu-id="24046-297">메시지가 표시되면 HDInsight 관리자 로그인의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-297">When prompted, enter the password for the HDInsight admin login.</span></span>
    >
    > <span data-ttu-id="24046-298">이 예제에서는 Azure PowerShell이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-298">This example requires Azure PowerShell.</span></span> <span data-ttu-id="24046-299">Azure PowerShell 사용에 대한 자세한 내용은 [Azure PowerShell 시작](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24046-299">For more information on using Azure PowerShell, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span></span>

    <span data-ttu-id="24046-300">이러한 예제에서 반환되는 정보는 다음 텍스트와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-300">The information returned by these examples is similar to the following text:</span></span>

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    <span data-ttu-id="24046-301">이 정보는 HBase 클러스터와 통신하기 위해 Storm에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-301">This information is used by Storm to communicate with the HBase cluster.</span></span>

2. <span data-ttu-id="24046-302">`dev.properties` 파일을 수정하고 다음 줄에 Zookeeper 쿼럼 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-302">Modify the `dev.properties` file and add the Zookeeper quorum information to the following line:</span></span>

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-the-solution-to-hdinsight"></a><span data-ttu-id="24046-303">솔루션을 빌드, 패키지하여 HDInsight에 배포</span><span class="sxs-lookup"><span data-stu-id="24046-303">Build, package, and deploy the solution to HDInsight</span></span>

<span data-ttu-id="24046-304">개발 환경에서 다음 단계를 수행하여 Storm 토폴로지를 Storm 클러스터에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-304">In your development environment, use the following steps to deploy the Storm topology to the storm cluster.</span></span>

1. <span data-ttu-id="24046-305">`TemperatureMonitor` 디렉터리에서 다음 명령을 사용하여 새 빌드를 수행하고 프로젝트에서 JAR 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24046-305">From the `TemperatureMonitor` directory, use the following command to perform a new build and create a JAR package from your project:</span></span>
   
        mvn clean package
   
    <span data-ttu-id="24046-306">이 명령은 프로젝트의 대상 디렉터리에 `TemperatureMonitor-1.0-SNAPSHOT.jar in the `라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24046-306">This command creates a file named `TemperatureMonitor-1.0-SNAPSHOT.jar in the `target\` directory of your project.</span></span>

2. <span data-ttu-id="24046-307">Scp를 사용하여 `TemperatureMonitor-1.0-SNAPSHOT.jar` 및 `dev.properties` 파일을 Storm 클러스터에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-307">Use scp to upload the `TemperatureMonitor-1.0-SNAPSHOT.jar` and `dev.properties` files to your Storm cluster.</span></span> <span data-ttu-id="24046-308">다음 예제에서 `sshuser`를 클러스터를 만들 때 제공한 SSH 사용자로 바꾸고 `clustername`을 Storm 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="24046-308">In the following example, replace `sshuser` with the SSH user you provided when creating the cluster, and `clustername` with the name of your Storm cluster.</span></span> <span data-ttu-id="24046-309">확인 메시지가 표시되면 SSH 사용자의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-309">When prompted, enter the password for the SSH user.</span></span>
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > <span data-ttu-id="24046-310">파일을 업로드하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24046-310">It may take several minutes to upload the files.</span></span>

    <span data-ttu-id="24046-311">HDInsight에서 `scp` 및 `ssh` 명령 사용에 대한 자세한 내용은 [HDInsight에서 SSH 사용](./hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24046-311">For more information on using the `scp` and `ssh` commands with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

3. <span data-ttu-id="24046-312">파일이 업로드되면 SSH를 사용하여 Storm 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-312">Once the file has been uploaded, connect to the Storm cluster using SSH.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="24046-313">`sshuser`를 SSH 사용자 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="24046-313">Replace `sshuser` with the SSH user name.</span></span> <span data-ttu-id="24046-314">`clustername`을 Storm 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="24046-314">Replace `clustername` with the Storm cluster name.</span></span>

4. <span data-ttu-id="24046-315">토폴로지를 시작하려면 SSH 세션에서 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-315">To start the topology, use the following command from the SSH session:</span></span>
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * <span data-ttu-id="24046-316">`--remote`는 Nimbus 서비스에 토폴로지를 제출합니다. 그러면 클러스터의 감독자 노드에서 토폴로지가 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-316">`--remote` submits the topology to the Nimbus service, which distributes it to the supervisor nodes in the cluster.</span></span>
    * <span data-ttu-id="24046-317">`--filter`는 `dev.properties` 파일을 사용하여 토폴로지 정의의 매개 변수를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="24046-317">`--filter` uses the `dev.properties` file to populate parameters in the topology definition.</span></span>
    * <span data-ttu-id="24046-318">`-R /with-hbase.yaml`은 패키지에 포함되는 `with-hbase.yaml` 토폴로지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-318">`-R /with-hbase.yaml` uses the `with-hbase.yaml` topology included in the package.</span></span>

5. <span data-ttu-id="24046-319">토폴로지가 시작되면 브라우저에서 Azure에 게시한 웹 사이트를 열고 `node app.js` 명령을 사용하여 이벤트 허브로 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="24046-319">After the topology has started, open a browser to the website you published on Azure, then use the `node app.js` command to send data to Event Hub.</span></span> <span data-ttu-id="24046-320">정보를 표시하기 위해 웹 대시보드가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-320">You should see the web dashboard update to display the information.</span></span>
   
    ![dashboard](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a><span data-ttu-id="24046-322">HBase 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="24046-322">View HBase data</span></span>

<span data-ttu-id="24046-323">다음 단계를 사용하여 HBase에 연결하며 데이터가 테이블에 기록되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-323">Use the following steps to connect to HBase and verify that the data has been written to the table:</span></span>

1. <span data-ttu-id="24046-324">SSH를 사용하여 HBase 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-324">Use SSH to connect to the HBase cluster.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="24046-325">`sshuser`를 SSH 사용자 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="24046-325">Replace `sshuser` with the SSH user name.</span></span> <span data-ttu-id="24046-326">`clustername`을 HBase 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="24046-326">Replace `clustername` with the HBase cluster name.</span></span>

2. <span data-ttu-id="24046-327">SSH 세션에서 HBase 셸을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-327">From the SSH session, start the HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="24046-328">셸이 로드되면 `hbase(main):001:0>` 프롬프트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="24046-328">Once the shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="24046-329">테이블의 행 보기:</span><span class="sxs-lookup"><span data-stu-id="24046-329">View rows from the table:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="24046-330">이 명령은 테이블에 데이터가 있음을 나타내는 다음 텍스트와 비슷한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-330">This command returns information similar to the following text, indicating that there is data in the table.</span></span>
   
        hbase(main):002:0> scan 'SensorData'
        ROW                             COLUMN+CELL
        \x00\x00\x00\x00               column=cf:temperature, timestamp=1467290788277, value=\x00\x00\x00\x04
        \x00\x00\x00\x00               column=cf:timestamp, timestamp=1467290788277, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x01               column=cf:temperature, timestamp=1467290788348, value=\x00\x00\x00M
        \x00\x00\x00\x01               column=cf:timestamp, timestamp=1467290788348, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x02               column=cf:temperature, timestamp=1467290788268, value=\x00\x00\x00R
        \x00\x00\x00\x02               column=cf:timestamp, timestamp=1467290788268, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x03               column=cf:temperature, timestamp=1467290788269, value=\x00\x00\x00#
        \x00\x00\x00\x03               column=cf:timestamp, timestamp=1467290788269, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x04               column=cf:temperature, timestamp=1467290788356, value=\x00\x00\x00>
        \x00\x00\x00\x04               column=cf:timestamp, timestamp=1467290788356, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x05               column=cf:temperature, timestamp=1467290788326, value=\x00\x00\x00\x0D
        \x00\x00\x00\x05               column=cf:timestamp, timestamp=1467290788326, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x06               column=cf:temperature, timestamp=1467290788253, value=\x00\x00\x009
        \x00\x00\x00\x06               column=cf:timestamp, timestamp=1467290788253, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x07               column=cf:temperature, timestamp=1467290788229, value=\x00\x00\x00\x12
        \x00\x00\x00\x07               column=cf:timestamp, timestamp=1467290788229, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x08               column=cf:temperature, timestamp=1467290788336, value=\x00\x00\x00\x16
        \x00\x00\x00\x08               column=cf:timestamp, timestamp=1467290788336, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x09               column=cf:temperature, timestamp=1467290788246, value=\x00\x00\x001
        \x00\x00\x00\x09               column=cf:timestamp, timestamp=1467290788246, value=2015-02-10T14:43.05.00320Z
        10 row(s) in 0.1800 seconds
   
   > [!NOTE]
   > <span data-ttu-id="24046-331">이 검색 작업은 테이블에서 최대 10개의 행을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-331">This scan operation returns a maximum of 10 rows from the table.</span></span>

## <a name="delete-your-clusters"></a><span data-ttu-id="24046-332">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="24046-332">Delete your clusters</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="24046-333">클러스터, 저장소, 웹앱을 한꺼번에 삭제하려면 해당 항목을 포함하는 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="24046-333">To delete the clusters, storage, and web app at one time, delete the resource group that contains them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24046-334">다음 단계</span><span class="sxs-lookup"><span data-stu-id="24046-334">Next steps</span></span>

<span data-ttu-id="24046-335">HDInsight의 Storm 토폴로지에 대한 자세한 내용은 [HDInsight의 Storm에 대한 예제 토폴로지](hdinsight-storm-example-topology.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24046-335">For more examples of Storm topologies with HDInsight, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md)</span></span>

<span data-ttu-id="24046-336">Apache Storm에 대한 자세한 내용은 [Apache Storm](https://storm.incubator.apache.org/) 사이트를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24046-336">For more information about Apache Storm, see the [Apache Storm](https://storm.incubator.apache.org/) site.</span></span>

<span data-ttu-id="24046-337">HDInsight의 HBase에 대한 자세한 내용은 [HDInsight HBase 개요](hdinsight-hbase-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24046-337">For more information about HBase on HDInsight, see the [HBase with HDInsight Overview](hdinsight-hbase-overview.md).</span></span>

<span data-ttu-id="24046-338">Socket.io에 대한 자세한 내용은 [socket.io](http://socket.io/) 사이트를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24046-338">For more information about Socket.io, see the [socket.io](http://socket.io/) site.</span></span>

<span data-ttu-id="24046-339">D3.js에 대한 자세한 내용은 [D3.js - 데이터 기반 문서](http://d3js.org/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24046-339">For more information about D3.js, see [D3.js - Data Driven Documents](http://d3js.org/).</span></span>

<span data-ttu-id="24046-340">Java에서 토폴로지를 만들기에 대한 자세한 내용은 [HDInsight의 Apache Storm용 Java 토폴로지 개발](hdinsight-storm-develop-java-topology.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24046-340">For information about creating topologies in Java, see [Develop Java topologies for Apache Storm on HDInsight](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="24046-341">.NET에서 토폴로지를 만들기에 대한 자세한 내용은 [Visual Studio를 사용하여 HDInsight의 Apache Storm용 C# 토폴로지 개발](hdinsight-storm-develop-csharp-visual-studio-topology.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24046-341">For information about creating topologies in .NET, see [Develop C# topologies for Apache Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

[azure-portal]: https://portal.azure.com
