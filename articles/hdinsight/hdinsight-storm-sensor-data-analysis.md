---
title: "Apache Storm 및 HBase를 사용 하 여 aaaAnalyze 센서 데이터 | Microsoft Docs"
description: "자세한 내용은 가상 네트워크와 tooconnect tooApache 스톰 방법입니다. Storm를 사용 하 여 이벤트 허브에서 HBase tooprocess 센서 데이터를 사용 하 고 D3.js로 시각화 합니다."
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
ms.openlocfilehash: e54fe9ffc720b0089f90e302b24a9438bd43999a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a><span data-ttu-id="3e9e9-104">HDInsight(Hadoop)에서 Apache Storm, 이벤트 허브 및 HBase를 사용하여 센서 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="3e9e9-104">Analyze sensor data with Apache Storm, Event Hub, and HBase in HDInsight (Hadoop)</span></span>

<span data-ttu-id="3e9e9-105">자세한 내용은 Azure 이벤트 허브의 HDInsight tooprocess 센서 데이터에 대해 toouse Apache Storm 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-105">Learn how toouse Apache Storm on HDInsight tooprocess sensor data from Azure Event Hub.</span></span> <span data-ttu-id="3e9e9-106">hello 데이터, HDInsight의 Apache HBase에 저장 됩니다 및 D3.js를 사용 하 여 시각화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-106">hello data is then stored into Apache HBase on HDInsight, and visualized using D3.js.</span></span>

<span data-ttu-id="3e9e9-107">이 문서에 사용 되는 hello Azure 리소스 관리자 템플릿을 보여 줍니다. 방법을 toocreate 리소스 그룹에 여러 Azure 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-107">hello Azure Resource Manager template used in this document demonstrates how toocreate multiple Azure resources in a resource group.</span></span> <span data-ttu-id="3e9e9-108">hello 템플릿은 Azure 가상 네트워크, 두 개의 HDInsight 클러스터 (스톰 및 HBase) 및 Azure 웹 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-108">hello template creates an Azure Virtual Network, two HDInsight clusters (Storm and HBase) and an Azure Web App.</span></span> <span data-ttu-id="3e9e9-109">실시간 웹 대시보드를 구현 하는 node.js 웹 응용 프로그램 배포가 자동으로 toohello입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-109">A node.js implementation of a real-time web dashboard is automatically deployed toohello web app.</span></span>

> [!NOTE]
> <span data-ttu-id="3e9e9-110">이 문서와이 문서에 대 한 예제에서 hello 정보 HDInsight 버전 3.6 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-110">hello information in this document and example in this document require HDInsight version 3.6.</span></span>
>
> <span data-ttu-id="3e9e9-111">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3e9e9-112">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e9e9-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3e9e9-113">Prerequisites</span></span>

* <span data-ttu-id="3e9e9-114">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-114">An Azure subscription.</span></span>
* <span data-ttu-id="3e9e9-115">[Node.js](http://nodejs.org/): 개발 환경에서 로컬로 사용 되는 toopreview hello 웹 대시보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-115">[Node.js](http://nodejs.org/): Used toopreview hello web dashboard locally on your development environment.</span></span>
* <span data-ttu-id="3e9e9-116">[Java 및 hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): toodevelop hello 스톰 토폴로지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-116">[Java and hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): Used toodevelop hello Storm topology.</span></span>
* <span data-ttu-id="3e9e9-117">[Maven](http://maven.apache.org/what-is-maven.html): toobuild 및 컴파일 hello 프로젝트를 사용된 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-117">[Maven](http://maven.apache.org/what-is-maven.html): Used toobuild and compile hello project.</span></span>
* <span data-ttu-id="3e9e9-118">[Git](http://git-scm.com/): GitHub에서 사용 되는 toodownload hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-118">[Git](http://git-scm.com/): Used toodownload hello project from GitHub.</span></span>
* <span data-ttu-id="3e9e9-119">**SSH** 클라이언트: tooconnect toohello Linux 기반 HDInsight 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-119">An **SSH** client: Used tooconnect toohello Linux-based HDInsight clusters.</span></span> <span data-ttu-id="3e9e9-120">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-120">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="3e9e9-121">기존 HDInsight 클러스터가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-121">You do not need an existing HDInsight cluster.</span></span> <span data-ttu-id="3e9e9-122">이 문서의 단계 hello hello 다음 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-122">hello steps in this document create hello following resources:</span></span>
> 
> * <span data-ttu-id="3e9e9-123">Azure 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="3e9e9-123">An Azure Virtual Network</span></span>
> * <span data-ttu-id="3e9e9-124">HDInsight 클러스터의 Storm(Linux 기반, 작업자 노드 2개)</span><span class="sxs-lookup"><span data-stu-id="3e9e9-124">A Storm on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="3e9e9-125">HDInsight 클러스터의 HBase(Linux 기반, 작업자 노드 2개)</span><span class="sxs-lookup"><span data-stu-id="3e9e9-125">An HBase on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="3e9e9-126">Hello 웹 대시보드를 호스팅하는 Azure 웹 앱</span><span class="sxs-lookup"><span data-stu-id="3e9e9-126">An Azure Web App that hosts hello web dashboard</span></span>

## <a name="architecture"></a><span data-ttu-id="3e9e9-127">아키텍처</span><span class="sxs-lookup"><span data-stu-id="3e9e9-127">Architecture</span></span>

![아키텍처 다이어그램](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

<span data-ttu-id="3e9e9-129">이 예제에서는 다음과 같은 구성 요소가 hello 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-129">This example consists of hello following components:</span></span>

* <span data-ttu-id="3e9e9-130">**Azure 이벤트 허브**: 센서에서 수집된 데이터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-130">**Azure Event Hubs**: Contains data that is collected from sensors.</span></span>
* <span data-ttu-id="3e9e9-131">**HDInsight의 Storm**: 이벤트 허브의 데이터를 실시간으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-131">**Storm on HDInsight**: Provides real-time processing of data from Event Hub.</span></span>
* <span data-ttu-id="3e9e9-132">**HDInsight의 HBase**: Storm에서 처리된 후에 데이터에 대한 영구 NoSQL 데이터 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-132">**HBase on HDInsight**: Provides a persistent NoSQL data store for data after it has been processed by Storm.</span></span>
* <span data-ttu-id="3e9e9-133">**Azure 가상 네트워크 서비스**: HDInsight 클러스터에서 HDInsight의 Storm hello 및 HBase 간의 보안 통신을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-133">**Azure Virtual Network service**: Enables secure communications between hello Storm on HDInsight and HBase on HDInsight clusters.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="3e9e9-134">가상 네트워크는 hello HBase Java 클라이언트 API를 사용 하는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-134">A virtual network is required when using hello Java HBase client API.</span></span> <span data-ttu-id="3e9e9-135">HBase 클러스터에 대 한 hello 공용 게이트웨이 통해 노출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-135">It is not exposed over hello public gateway for HBase clusters.</span></span> <span data-ttu-id="3e9e9-136">동일한 가상 네트워크를 허용 하는 hello로 설치 HBase 및 Storm 클러스터 hello Storm 클러스터 (또는 hello 가상 네트워크에서 다른 시스템) toodirectly 클라이언트 API를 사용 하 여 HBase에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-136">Installing HBase and Storm clusters into hello same virtual network allows hello Storm cluster (or any other system on hello virtual network) toodirectly access HBase using client API.</span></span>

* <span data-ttu-id="3e9e9-137">**대시보드 웹 사이트**: 실시간으로 데이터 차트를 작성하는 예제 대시보드입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-137">**Dashboard website**: An example dashboard that charts data in real time.</span></span>
  
  * <span data-ttu-id="3e9e9-138">hello 웹 사이트는 Node.js에서 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-138">hello website is implemented in Node.js.</span></span>
  * <span data-ttu-id="3e9e9-139">[Socket.io](http://socket.io/) hello 웹 사이트와 hello 스톰 토폴로지 실시간 통신에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-139">[Socket.io](http://socket.io/) is used for real-time communication between hello Storm topology and hello website.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="3e9e9-140">통신에 Socket.io를 사용하는 것은 구현 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-140">Using Socket.io for communication is an implementation detail.</span></span> <span data-ttu-id="3e9e9-141">원시 WebSocket 또는 SignalR과 같은 모든 통신 프레임워크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-141">You can use any communications framework, such as raw WebSockets or SignalR.</span></span>

  * <span data-ttu-id="3e9e9-142">[D3.js](http://d3js.org/) toohello 웹 사이트에 전송 된 사용 되는 toograph hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-142">[D3.js](http://d3js.org/) is used toograph hello data that is sent toohello website.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e9e9-143">지원 되는 방법을 toocreate 하나 HDInsight 클러스터가 없습니다 스톰와 HBase 없기 때문에 두 개의 클러스터가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-143">Two clusters are required, as there is no supported method toocreate one HDInsight cluster for both Storm and HBase.</span></span>

<span data-ttu-id="3e9e9-144">hello 토폴로지 데이터 이벤트 허브에서 사용 하 여 읽고 hello [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) 집합과 hello를 사용 하 여 HBase에 데이터 쓰기 [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-144">hello topology reads data from Event Hub by using hello [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) class, and writes data into HBase using hello [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) class.</span></span> <span data-ttu-id="3e9e9-145">Hello 웹 사이트와 통신을 사용 하 여 수행 됩니다 [socket.io client.java](https://github.com/nkzawa/socket.io-client.java)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-145">Communication with hello website is accomplished by using [socket.io-client.java](https://github.com/nkzawa/socket.io-client.java).</span></span>

<span data-ttu-id="3e9e9-146">다음 다이어그램 hello hello 토폴로지의 hello 레이아웃을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-146">hello following diagram explains hello layout of hello topology:</span></span>

![토폴로지 다이어그램](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> <span data-ttu-id="3e9e9-148">이 다이어그램은 토폴로지 hello의 단순화 된 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-148">This diagram is a simplified view of hello topology.</span></span> <span data-ttu-id="3e9e9-149">Event Hub의 각 파티션에 대해 각 구성 요소의 인스턴스가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-149">An instance of each component is created for each partition in your Event Hub.</span></span> <span data-ttu-id="3e9e9-150">이러한 인스턴스는 hello hello 클러스터 노드를 통해 배포 되 고 다음과 같이 데이터 간에 전달 되:</span><span class="sxs-lookup"><span data-stu-id="3e9e9-150">These instances are distributed across hello nodes in hello cluster, and data is routed between them as follows:</span></span>
> 
> * <span data-ttu-id="3e9e9-151">Hello 배출구 toohello 파서 데이터는 부하 분산 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-151">Data from hello spout toohello parser is load balanced.</span></span>
> * <span data-ttu-id="3e9e9-152">장치 ID hello 파서 toohello 대시보드 및 HBase에서 데이터가 그룹화 되어, 메시지를 동일한 장치를 항상 hello 있도록 흐름 toohello 동일한 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-152">Data from hello parser toohello Dashboard and HBase is grouped by Device ID, so that messages from hello same device always flow toohello same component.</span></span>

### <a name="topology-components"></a><span data-ttu-id="3e9e9-153">토폴로지 구성 요소</span><span class="sxs-lookup"><span data-stu-id="3e9e9-153">Topology components</span></span>

* <span data-ttu-id="3e9e9-154">**이벤트 허브 Spout**: hello 배출구 0.10.0 Apache Storm 버전의 일부로 제공 되며 높은 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-154">**Event Hub Spout**: hello spout is provided as part of Apache Storm version 0.10.0 and higher.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="3e9e9-155">이 예에서 사용 된 hello 이벤트 허브 배출구 HDInsight 클러스터 버전이 3.5 또는 3.6에서 Storm이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-155">hello Event Hub spout used in this example requires a Storm on HDInsight cluster version 3.5 or 3.6.</span></span>

* <span data-ttu-id="3e9e9-156">**ParserBolt.java**: hello 배출구에서 내보내는 hello 데이터 원시 JSON 이며 한 번에 하나 이상의 경우에 따라 이벤트를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-156">**ParserBolt.java**: hello data that is emitted by hello spout is raw JSON, and occasionally more than one event is emitted at a time.</span></span> <span data-ttu-id="3e9e9-157">이 볼트 읽고 hello에서 내보내는 hello 데이터 spout hello JSON 메시지를 구문 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-157">This bolt reads hello data emitted by hello spout and parses hello JSON message.</span></span> <span data-ttu-id="3e9e9-158">hello 볼트 다음 여러 필드를 포함 하는 튜플로 서 hello 데이터를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-158">hello bolt then emits hello data as a tuple that contains multiple fields.</span></span>
* <span data-ttu-id="3e9e9-159">**DashboardBolt.java**:이 구성 요소 toouse toohello 웹 대시보드에 실시간으로 Java toosend 데이터에 대 한 클라이언트 라이브러리 Socket.io hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-159">**DashboardBolt.java**: This component demonstrates how toouse hello Socket.io client library for Java toosend data in real time toohello web dashboard.</span></span>
* <span data-ttu-id="3e9e9-160">**아니요 hbase.yaml**: hello 로컬 모드에서 실행할 때 사용 되는 토폴로지 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-160">**no-hbase.yaml**: hello topology definition used when running in local mode.</span></span> <span data-ttu-id="3e9e9-161">HBase 구성 요소를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-161">It does not use HBase components.</span></span>
* <span data-ttu-id="3e9e9-162">**hbase.yaml와**: hello hello 토폴로지 hello 클러스터에서 실행할 때 사용 되는 토폴로지 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-162">**with-hbase.yaml**: hello topology definition used when running hello topology on hello cluster.</span></span> <span data-ttu-id="3e9e9-163">HBase 구성 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-163">It does use HBase components.</span></span>
* <span data-ttu-id="3e9e9-164">**dev.properties**: hello hello 이벤트 허브 배출구, HBase 볼트 및 대시보드 구성 요소에 대 한 구성 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-164">**dev.properties**: hello configuration information for hello Event Hub spout, HBase bolt, and dashboard components.</span></span>

## <a name="prepare-your-environment"></a><span data-ttu-id="3e9e9-165">환경 준비</span><span class="sxs-lookup"><span data-stu-id="3e9e9-165">Prepare your environment</span></span>

<span data-ttu-id="3e9e9-166">이 예제를 사용 하기 전에 hello 스톰 토폴로지에서 읽고 Azure 이벤트 허브를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-166">Before you use this example, you must create an Azure Event Hub, which hello Storm topology reads from.</span></span>

### <a name="configure-event-hub"></a><span data-ttu-id="3e9e9-167">이벤트 허브 구성</span><span class="sxs-lookup"><span data-stu-id="3e9e9-167">Configure Event Hub</span></span>

<span data-ttu-id="3e9e9-168">이벤트 허브는이 예제에 대 한 hello 데이터 원본.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-168">Event Hub is hello data source for this example.</span></span> <span data-ttu-id="3e9e9-169">다음 단계 toocreate 이벤트 허브 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-169">Use hello following steps toocreate an Event Hub.</span></span>

1. <span data-ttu-id="3e9e9-170">Hello에서 [Azure 포털](https://portal.azure.com)선택, **+ 새로 만들기** -> **사물 인터넷** -> **이벤트 허브**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-170">From hello [Azure portal](https://portal.azure.com), select **+ New** -> **Internet of Things** -> **Event Hubs**.</span></span>
2. <span data-ttu-id="3e9e9-171">Hello에 **만들 Namespace** 섹션를 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-171">In hello **Create Namespace** section, perform hello following tasks:</span></span>
   
   1. <span data-ttu-id="3e9e9-172">입력 한 **이름** hello 네임 스페이스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-172">Enter a **Name** for hello namespace.</span></span>
   2. <span data-ttu-id="3e9e9-173">가격 책정 계층을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-173">Select a pricing tier.</span></span> <span data-ttu-id="3e9e9-174">**기본** 이면 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-174">**Basic** is sufficient for this example.</span></span>
   3. <span data-ttu-id="3e9e9-175">선택 hello Azure **구독** toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-175">Select hello Azure **Subscription** toouse.</span></span>
   4. <span data-ttu-id="3e9e9-176">기존 리소스 그룹을 선택하거나 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-176">Either select an existing resource group or create a new one.</span></span>
   5. <span data-ttu-id="3e9e9-177">선택 hello **위치** hello 이벤트 허브에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-177">Select hello **Location** for hello Event Hub.</span></span>
   6. <span data-ttu-id="3e9e9-178">선택 **Pin toodashboard**, 클릭 하 고 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-178">Select **Pin toodashboard**, and then click **Create**.</span></span>

3. <span data-ttu-id="3e9e9-179">Hello 생성 프로세스가 완료 되 면 hello 네임 스페이스에 대 한 이벤트 허브 정보 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-179">When hello creation process completes, hello Event Hubs information for your namespace is displayed.</span></span> <span data-ttu-id="3e9e9-180">여기에서 **+ Event Hub 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-180">From here, select **+ Add Event Hub**.</span></span> <span data-ttu-id="3e9e9-181">Hello에 **이벤트 허브 만들기** 섹션의 이름을 입력 합니다. **sensordata**를 선택한 후 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-181">In hello **Create Event Hub** section, enter a name of **sensordata**, and then select **Create**.</span></span> <span data-ttu-id="3e9e9-182">나머지 필드는 hello 기본값 hello를 둡니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-182">Leave hello other fields at hello default values.</span></span>
4. <span data-ttu-id="3e9e9-183">Hello 이벤트 허브에서 하 여 네임 스페이스 선택에 대 한 보기 **이벤트 허브**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-183">From hello Event Hubs view for your namespace, select **Event Hubs**.</span></span> <span data-ttu-id="3e9e9-184">선택 hello **sensordata** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-184">Select hello **sensordata** entry.</span></span>
5. <span data-ttu-id="3e9e9-185">Hello sensordata 이벤트 허브에서에서 선택 **공유 액세스 정책을**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-185">From hello sensordata Event Hub, select **Shared access policies**.</span></span> <span data-ttu-id="3e9e9-186">사용 하 여 hello **+ 추가** 다음 정책 링크 tooadd hello:</span><span class="sxs-lookup"><span data-stu-id="3e9e9-186">Use hello **+ Add** link tooadd hello following policies:</span></span>

    | <span data-ttu-id="3e9e9-187">정책 이름</span><span class="sxs-lookup"><span data-stu-id="3e9e9-187">Policy name</span></span> | <span data-ttu-id="3e9e9-188">클레임</span><span class="sxs-lookup"><span data-stu-id="3e9e9-188">Claims</span></span> |
    | ----- | ----- |
    | <span data-ttu-id="3e9e9-189">devices</span><span class="sxs-lookup"><span data-stu-id="3e9e9-189">devices</span></span> | <span data-ttu-id="3e9e9-190">보내기</span><span class="sxs-lookup"><span data-stu-id="3e9e9-190">Send</span></span> |
    | <span data-ttu-id="3e9e9-191">storm</span><span class="sxs-lookup"><span data-stu-id="3e9e9-191">storm</span></span> | <span data-ttu-id="3e9e9-192">수신 대기</span><span class="sxs-lookup"><span data-stu-id="3e9e9-192">Listen</span></span> |

1. <span data-ttu-id="3e9e9-193">두 정책을 모두 선택 하 고 hello 메모 **기본 키** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-193">Select both policies and make a note of hello **PRIMARY KEY** value.</span></span> <span data-ttu-id="3e9e9-194">Hello 값 이후 단계에서 두 정책을 모두 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-194">You need hello value for both policies in future steps.</span></span>

## <a name="download-and-configure-hello-project"></a><span data-ttu-id="3e9e9-195">다운로드 하 고 hello 프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="3e9e9-195">Download and configure hello project</span></span>

<span data-ttu-id="3e9e9-196">Hello toodownload hello 프로젝트 GitHub에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-196">Use hello following toodownload hello project from GitHub.</span></span>

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

<span data-ttu-id="3e9e9-197">Hello 명령이 완료 된 후에 디렉터리 구조를 다음 hello</span><span class="sxs-lookup"><span data-stu-id="3e9e9-197">After hello command completes, you have hello following directory structure:</span></span>

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains hello topology
            resources/
                log4j2.xml - set logging toominimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO toohello web dashboard.
        dashboard/nodejs/ - this is hello node.js web dashboard.
        SendEvents/ - utilities toosend fake sensor data.

> [!NOTE]
> <span data-ttu-id="3e9e9-198">이 문서는이 예제에 포함 된 hello 코드의 toofull 세부 정보에는 설명 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-198">This document does not go in toofull details of hello code included in this example.</span></span> <span data-ttu-id="3e9e9-199">그러나 hello 코드 주석 완벽 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-199">However, hello code is fully commented.</span></span>

<span data-ttu-id="3e9e9-200">이벤트 허브를 열고 hello에서 tooconfigure hello 프로젝트 tooread `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` 파일 및 줄을 다음에 이벤트 허브 정보 toohello 추가:</span><span class="sxs-lookup"><span data-stu-id="3e9e9-200">tooconfigure hello project tooread from Event Hub, open hello `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` file and add your Event Hub information toohello following lines:</span></span>

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a><span data-ttu-id="3e9e9-201">로컬로 컴파일 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3e9e9-201">Compile and test locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e9e9-202">로컬로 hello 토폴로지를 사용 하 여 작업 스톰 개발 환경 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-202">Using hello topology locally requires a working Storm development environment.</span></span> <span data-ttu-id="3e9e9-203">자세한 내용은 Apache.org에서 [Storm 개발 환경 설정](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-203">For more information, see [Setting up a Storm development environment](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) at Apache.org.</span></span>

> [!WARNING]
> <span data-ttu-id="3e9e9-204">Windows 개발 환경의 사용 하는 경우 발생할 수 있습니다는 `java.io.IOException` 때 hello 토폴로지를 로컬로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-204">If you are using a Windows development environment, you may receive a `java.io.IOException` when running hello topology locally.</span></span> <span data-ttu-id="3e9e9-205">이 경우 HDInsight의 toorunning hello 토폴로지 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-205">If so, move on toorunning hello topology on HDInsight.</span></span>

<span data-ttu-id="3e9e9-206">를 테스트 하기 전에 hello 토폴로지의 hello 대시보드 tooview hello 출력을 시작 하 고 이벤트 허브에 데이터 toostore를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-206">Before testing, you must start hello dashboard tooview hello output of hello topology and generate data toostore in Event Hub.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e9e9-207">이 토폴로지의 hello HBase 구성 요소가 로컬로 테스트할 때에 활성 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-207">hello HBase component of this topology is not active when testing locally.</span></span> <span data-ttu-id="3e9e9-208">Java API hello hello HBase 클러스터에 대 한 외부 hello hello 클러스터 포함 된 Azure 가상 네트워크에서에서 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-208">hello Java API for hello HBase cluster cannot be accessed from outside hello Azure Virtual Network that contains hello clusters.</span></span>

### <a name="start-hello-web-application"></a><span data-ttu-id="3e9e9-209">Hello 웹 응용 프로그램 시작</span><span class="sxs-lookup"><span data-stu-id="3e9e9-209">Start hello web application</span></span>

1. <span data-ttu-id="3e9e9-210">명령 프롬프트를 열고 디렉터리를 너무 변경`hdinsight-eventhub-example/dashboard`합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-210">Open a command prompt and change directories too`hdinsight-eventhub-example/dashboard`.</span></span> <span data-ttu-id="3e9e9-211">명령 tooinstall hello 종속성 hello 웹 응용 프로그램에 필요한 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-211">Use hello following command tooinstall hello dependencies needed by hello web application:</span></span>
   
    ```bash
    npm install
    ```

2. <span data-ttu-id="3e9e9-212">사용 하 여 hello 다음 명령 toostart hello 웹 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-212">Use hello following command toostart hello web application:</span></span>
   
    ```bash
    node server.js
    ```
   
    <span data-ttu-id="3e9e9-213">텍스트 다음 메시지와 비슷한 toohello를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-213">You see a message similar toohello following text:</span></span>
   
        Server listening at port 3000

3. <span data-ttu-id="3e9e9-214">웹 브라우저를 열고 다음을 입력 `http://localhost:3000/` hello 주소로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-214">Open a web browser and enter `http://localhost:3000/` as hello address.</span></span> <span data-ttu-id="3e9e9-215">다음 이미지는 페이지와 유사한 toohello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-215">A page similar toohello following image is displayed:</span></span>
   
    ![웹 대시보드](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    <span data-ttu-id="3e9e9-217">이 명령 프롬프트는 계속 열어 두세요.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-217">Leave this command prompt open.</span></span> <span data-ttu-id="3e9e9-218">테스트를 마친 후 Ctrl + C toostop hello 웹 서버를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-218">After testing, use Ctrl-C toostop hello web server.</span></span>

### <a name="generate-data"></a><span data-ttu-id="3e9e9-219">데이터 생성</span><span class="sxs-lookup"><span data-stu-id="3e9e9-219">Generate data</span></span>

> [!NOTE]
> <span data-ttu-id="3e9e9-220">hello이 섹션의 단계에 사용 하 여 Node.js 모든 플랫폼에서 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-220">hello steps in this section use Node.js so that they can be used on any platform.</span></span> <span data-ttu-id="3e9e9-221">다른 언어 예제를 보려면 hello `SendEvents` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-221">For other language examples, see hello `SendEvents` directory.</span></span>

1. <span data-ttu-id="3e9e9-222">새 프롬프트, 셸 또는 터미널을 열고 디렉터리를 너무 변경`hdinsight-eventhub-example/SendEvents/nodejs`합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-222">Open a new prompt, shell, or terminal, and change directories too`hdinsight-eventhub-example/SendEvents/nodejs`.</span></span> <span data-ttu-id="3e9e9-223">다음 명령을 사용 하 여 hello hello 응용 프로그램에 필요한 tooinstall hello 종속성:</span><span class="sxs-lookup"><span data-stu-id="3e9e9-223">tooinstall hello dependencies needed by hello application, use hello following command:</span></span>

    ```bash
    npm install
    ```

2. <span data-ttu-id="3e9e9-224">열기 hello `app.js` 텍스트 편집기에서 파일을 hello 이전에 가져온 이벤트 허브 정보를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-224">Open hello `app.js` file in a text editor and add hello Event Hub information you obtained earlier:</span></span>
   
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
   > <span data-ttu-id="3e9e9-225">이 예에서는 사용 했다고 가정 `sensordata` 이벤트 허브의 hello 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-225">This example assumes that you have used `sensordata` as hello name of your Event Hub.</span></span> <span data-ttu-id="3e9e9-226">해당 `devices` hello 정책에의 hello 이름으로는 `Send` 클레임입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-226">And that `devices` as hello name of hello policy that has a `Send` claim.</span></span>

3. <span data-ttu-id="3e9e9-227">이벤트 허브에서 명령 tooinsert 새 항목을 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-227">Use hello following command tooinsert new entries in Event Hub:</span></span>
   
    ```bash
    node app.js
    ```
   
    <span data-ttu-id="3e9e9-228">출력의 hello 데이터를 포함 하는 여러 줄 tooEvent 허브 전송 하는 것이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-228">You see several lines of output that contain hello data sent tooEvent Hub:</span></span>
   
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

### <a name="build-and-start-hello-topology"></a><span data-ttu-id="3e9e9-229">빌드하고 hello 토폴로지를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-229">Build and start hello topology</span></span>

1. <span data-ttu-id="3e9e9-230">새 명령 프롬프트를 열고 디렉터리를 너무 변경`hdinsight-eventhub-example/TemperatureMonitor`합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-230">Open a new command prompt and change directories too`hdinsight-eventhub-example/TemperatureMonitor`.</span></span> <span data-ttu-id="3e9e9-231">토폴로지 hello toobuild 및 패키지 다음 명령을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-231">toobuild and package hello topology, use hello following command:</span></span> 

    ```bash
    mvn clean package
    ```

2. <span data-ttu-id="3e9e9-232">로컬 모드에서는 다음 명령을 사용 하 여 hello toostart hello 토폴로지:</span><span class="sxs-lookup"><span data-stu-id="3e9e9-232">toostart hello topology in local mode, use hello following command:</span></span>

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * <span data-ttu-id="3e9e9-233">`--local`로컬 모드에서 hello 토폴로지를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-233">`--local` starts hello topology in local mode.</span></span>
    * <span data-ttu-id="3e9e9-234">`--filter`사용 하 여 hello `dev.properties` hello 토폴로지 정의에서 파일 toopopulate 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-234">`--filter` uses hello `dev.properties` file toopopulate parameters in hello topology definition.</span></span>
    * <span data-ttu-id="3e9e9-235">`resources/no-hbase.yaml`사용 하 여 hello `no-hbase.yaml` 토폴로지 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-235">`resources/no-hbase.yaml` uses hello `no-hbase.yaml` topology definition.</span></span>
 
   <span data-ttu-id="3e9e9-236">시작 되 면 hello 토폴로지 이벤트 허브에서 항목을 읽고 하 고 로컬 컴퓨터에서 실행 중인 toohello 대시보드 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-236">Once started, hello topology reads entries from Event Hub, and sends them toohello dashboard running on your local machine.</span></span> <span data-ttu-id="3e9e9-237">다음 이미지와 비슷한 toohello hello 웹 대시보드에 표시 되는 줄이 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-237">You should see lines appear in hello web dashboard, similar toohello following image:</span></span>
   
    ![데이터가 표시된 대시보드](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. <span data-ttu-id="3e9e9-239">Hello 대시보드를 실행 하는 동안 사용 하 여 hello `node app.js` 이전 hello에서 명령을 단계 toosend 새 데이터 tooEvent 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-239">While hello dashboard is running, use hello `node app.js` command from hello previous steps toosend new data tooEvent Hubs.</span></span> <span data-ttu-id="3e9e9-240">Hello 온도 값을 임의로 생성 하기 때문에 hello 그래프 tooshow 크게 변경 온도 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-240">Because hello temperature values are randomly generated, hello graph should update tooshow large changes in temperature.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3e9e9-241">Hello에 있어야 **hdinsight-eventhub-예/SendEvents/Nodejs** hello를 사용 하는 경우 디렉터리 `node app.js` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-241">You must be in hello **hdinsight-eventhub-example/SendEvents/Nodejs** directory when using hello `node app.js` command.</span></span>

3. <span data-ttu-id="3e9e9-242">Ctrl + C를 사용 하 여 중지 hello 토폴로지 hello 대시보드 해당 업데이트를 확인 한 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-242">After verifying that hello dashboard updates, stop hello topology using Ctrl+C.</span></span> <span data-ttu-id="3e9e9-243">또한 Ctrl + C toostop hello 로컬 웹 서버를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-243">You can use Ctrl+C toostop hello local web server also.</span></span>

## <a name="create-a-storm-and-hbase-cluster"></a><span data-ttu-id="3e9e9-244">Storm 및 HBase 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="3e9e9-244">Create a Storm and HBase cluster</span></span>

<span data-ttu-id="3e9e9-245">이 섹션 사용의 단계를 hello는 [Azure 리소스 관리자 템플릿](../azure-resource-manager/resource-group-template-deploy.md) toocreate hello 가상 네트워크에는 Azure 가상 네트워크 및 스톰 및 HBase 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-245">hello steps in this section use an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) toocreate an Azure Virtual Network and a Storm and HBase cluster on hello virtual network.</span></span> <span data-ttu-id="3e9e9-246">hello 템플릿 Azure 웹 앱도 만들고에 hello 대시보드의 복사본을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-246">hello template also creates an Azure Web App and deploys a copy of hello dashboard into it.</span></span>

> [!NOTE]
> <span data-ttu-id="3e9e9-247">가상 네트워크는 hello Storm 클러스터에서 실행 되는 hello 토폴로지 hello HBase Java API를 사용 하 여 hello HBase 클러스터와 직접 통신할 수 있도록 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-247">A virtual network is used so that hello topology running on hello Storm cluster can directly communicate with hello HBase cluster using hello HBase Java API.</span></span>

<span data-ttu-id="3e9e9-248">이 문서에 사용 되는 hello 리소스 관리자 템플릿을 공용 blob 컨테이너에에 위치한 **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-248">hello Resource Manager template used in this document is located in a public blob container at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span></span>

1. <span data-ttu-id="3e9e9-249">Hello tooAzure에서 단추 toosign와 hello Azure 포털에서에서 열기 hello 리소스 관리자 템플릿을 다음를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-249">Click hello following button toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="3e9e9-250">Hello에서 **사용자 지정 배포** 섹션에서 다음 값에는 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-250">From hello **Custom deployment** section, enter hello following values:</span></span>
   
    ![HDInsight 매개 변수](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * <span data-ttu-id="3e9e9-252">**기본 클러스터 이름을**:이 값 hello hello 스톰 및 HBase 클러스터에 대 한 기본 이름으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-252">**Base Cluster Name**: This value is used as hello base name for hello Storm and HBase clusters.</span></span> <span data-ttu-id="3e9e9-253">예를 들어 **abc**를 입력하면 **storm-abc**라는 Storm 클러스터와 **hbase-abc**라는 HBase 클러스터가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-253">For example, entering **abc** creates a Storm cluster named **storm-abc** and an HBase cluster named **hbase-abc**.</span></span>
   * <span data-ttu-id="3e9e9-254">**클러스터 로그인 사용자 이름**: hello 스톰 및 HBase 클러스터에 대 한 hello 관리자 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-254">**Cluster Login User Name**: hello admin user name for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="3e9e9-255">**로그인 암호 클러스터**: hello 스톰 및 HBase 클러스터에 대 한 hello 관리자 사용자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-255">**Cluster Login Password**: hello admin user password for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="3e9e9-256">**SSH 사용자 이름이**: hello 스톰 및 HBase 클러스터에 대 한 SSH 사용자 toocreate hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-256">**SSH User Name**: hello SSH user toocreate for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="3e9e9-257">**SSH 암호**: hello 스톰 및 HBase 클러스터에 대 한 SSH 사용자 hello에 대 한 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-257">**SSH Password**: hello password for hello SSH user for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="3e9e9-258">**위치**: hello 클러스터에 생성 되는 hello 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-258">**Location**: hello region that hello clusters are created in.</span></span>
     
     <span data-ttu-id="3e9e9-259">클릭 **확인** toosave hello 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-259">Click **OK** toosave hello parameters.</span></span>

3. <span data-ttu-id="3e9e9-260">사용 하 여 hello **기본 사항** toocreate 리소스 그룹 섹션 또는 기존 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-260">Use hello **Basics** section toocreate a resource group or select an existing one.</span></span>
4. <span data-ttu-id="3e9e9-261">Hello에 **리소스 그룹 위치** hello에 대 한 선택 드롭다운 메뉴에서 선택 hello 동일한 위치 **위치** hello에 대 한 매개 변수 **설정을** 섹션.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-261">In hello **Resource group location** dropdown menu, select hello same location as you selected for hello **Location** parameter in hello **Settings** section.</span></span>
5. <span data-ttu-id="3e9e9-262">Hello 사용 약관을 읽고 다음 선택 **toohello 약관 위에서 설명한 동의**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-262">Read hello terms and conditions, and then select **I agree toohello terms and conditions stated above**.</span></span>
6. <span data-ttu-id="3e9e9-263">마지막으로 확인 **Pin toodashboard** 선택한 후 **구매**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-263">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="3e9e9-264">Hello 클러스터 toocreate 약 20 분이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-264">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="3e9e9-265">Hello 리소스를 만든 후 hello 리소스 그룹에 대 한 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-265">Once hello resources have been created, information about hello resource group is displayed.</span></span>

![Hello vnet 및 클러스터 리소스 그룹](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="3e9e9-267">Hello HDInsight 클러스터의 이름이 hello **스톰 BASENAME** 및 **hbase BASENAME**, 여기서 BASENAME는 hello 이름이 toohello 서식 파일을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-267">Notice that hello names of hello HDInsight clusters are **storm-BASENAME** and **hbase-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="3e9e9-268">Toohello 클러스터를 연결 하는 경우 이후 단계에서 이러한 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-268">You use these names in a later step when connecting toohello clusters.</span></span> <span data-ttu-id="3e9e9-269">또한 hello hello 대시보드 사이트의 이름 메모는 **basename 대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-269">Also note that hello name of hello dashboard site is **basename-dashboard**.</span></span> <span data-ttu-id="3e9e9-270">이 값은 이 문서의 뒷부분에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-270">This value is used later in this document.</span></span>

## <a name="configure-hello-dashboard-bolt"></a><span data-ttu-id="3e9e9-271">Hello 대시보드 볼트 구성</span><span class="sxs-lookup"><span data-stu-id="3e9e9-271">Configure hello Dashboard bolt</span></span>

<span data-ttu-id="3e9e9-272">toosend 데이터 toohello 대시보드 웹 앱으로 배포를 hello 다음 hello에 줄을 수정 해야 `dev.properties`파일:</span><span class="sxs-lookup"><span data-stu-id="3e9e9-272">toosend data toohello dashboard deployed as a web app, you must modify hello following line in hello `dev.properties`file:</span></span>

```yaml
dashboard.uri: http://localhost:3000
```

<span data-ttu-id="3e9e9-273">변경 `http://localhost:3000` 너무`http://BASENAME-dashboard.azurewebsites.net` hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-273">Change `http://localhost:3000` too`http://BASENAME-dashboard.azurewebsites.net` and save hello file.</span></span> <span data-ttu-id="3e9e9-274">대체 **BASENAME** hello 이전 단계에서 제공한 hello 기본 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-274">Replace **BASENAME** with hello base name you provided in hello previous step.</span></span> <span data-ttu-id="3e9e9-275">또한 tooselect hello 대시보드 및 보기 hello URL 이전에 만든 hello 리소스 그룹을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-275">You can also use hello resource group created previously tooselect hello dashboard and view hello URL.</span></span>

## <a name="create-hello-hbase-table"></a><span data-ttu-id="3e9e9-276">Hello HBase 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="3e9e9-276">Create hello HBase table</span></span>

<span data-ttu-id="3e9e9-277">HBase의 데이터를 toostore, 테이블을 먼저 작성 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-277">toostore data in HBase, we must first create a table.</span></span> <span data-ttu-id="3e9e9-278">미리 스톰 toowrite를 필요로 하는 리소스를 만들기, toocreate 동일한 리소스 hello 여러 인스턴스 스톰 토폴로지 내에서 toocreate 리소스는 동안 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-278">Pre-create resources that Storm needs toowrite to, as trying toocreate resources from inside a Storm topology can result in multiple instances trying toocreate hello same resource.</span></span> <span data-ttu-id="3e9e9-279">Hello 토폴로지 외부 hello 리소스를 만들고 읽기/쓰기 및 분석에 대 한 스톰을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-279">Create hello resources outside hello topology and use Storm for reading/writing and analytics.</span></span>

1. <span data-ttu-id="3e9e9-280">SSH 사용자 hello 및 클러스터를 만드는 동안 toohello 서식 파일을 입력 한 암호를 사용 하 여 SSH tooconnect toohello HBase 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-280">Use SSH tooconnect toohello HBase cluster using hello SSH user and password you supplied toohello template during cluster creation.</span></span> <span data-ttu-id="3e9e9-281">예를 들어 hello를 사용 하 여 연결 `ssh` 명령 구문 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-281">For example, if connecting using hello `ssh` command, you would use hello following syntax:</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    <span data-ttu-id="3e9e9-282">대체 `sshuser` hello 클러스터를 만들 때 제공한 hello SSH 사용자 이름이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-282">Replace `sshuser` with hello SSH user name you provided when creating hello cluster.</span></span> <span data-ttu-id="3e9e9-283">대체 `clustername` hello HBase 클러스터 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-283">Replace `clustername` with hello HBase cluster name.</span></span>

2. <span data-ttu-id="3e9e9-284">Hello SSH 세션에서 hello HBase 셸을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-284">From hello SSH session, start hello HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="3e9e9-285">Hello 셸 로드 되 면 참조는 `hbase(main):001:0>` 프롬프트입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-285">Once hello shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="3e9e9-286">HBase 셸 hello에서 hello 명령 toocreate 테이블 toostore hello 센서 데이터를 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-286">From hello HBase shell, enter hello following command toocreate a table toostore hello sensor data:</span></span>
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. <span data-ttu-id="3e9e9-287">다음 명령을 hello를 사용 하 여 해당 hello 테이블 생성 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-287">Verify that hello table has been created by using hello following command:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="3e9e9-288">다음 예에서는, hello 테이블에 행이 0 개 나타내는 비슷한 toohello 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-288">This returns information similar toohello following example, indicating that there are 0 rows in hello table.</span></span>
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. <span data-ttu-id="3e9e9-289">입력 `exit` tooexit hello HBase 셸:</span><span class="sxs-lookup"><span data-stu-id="3e9e9-289">Enter `exit` tooexit hello HBase shell:</span></span>

## <a name="configure-hello-hbase-bolt"></a><span data-ttu-id="3e9e9-290">Hello HBase 볼트 구성</span><span class="sxs-lookup"><span data-stu-id="3e9e9-290">Configure hello HBase bolt</span></span>

<span data-ttu-id="3e9e9-291">hello Storm 클러스터에서 toowrite tooHBase, hello HBase 볼트 HBase 클러스터의 hello 구성 세부 정보를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-291">toowrite tooHBase from hello Storm cluster, you must provide hello HBase bolt with hello configuration details of your HBase cluster.</span></span>

1. <span data-ttu-id="3e9e9-292">Hello HBase 클러스터에 대 한 예제 tooretrieve hello 사육 쿼럼 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-292">Use one of hello following examples tooretrieve hello Zookeeper quorum for your HBase cluster:</span></span>

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > <span data-ttu-id="3e9e9-293">대체 `your_HDInsight_cluster_name` HDInsight 클러스터의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-293">Replace `your_HDInsight_cluster_name` with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="3e9e9-294">Hello를 설치 하는 방법에 대 한 자세한 내용은 `jq` 유틸리티 참조 [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-294">For more information on installing hello `jq` utility, see [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span></span>
    >
    > <span data-ttu-id="3e9e9-295">메시지가 표시 되 면 hello HDInsight 관리자 로그인에 대 한 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-295">When prompted, enter hello password for hello HDInsight admin login.</span></span>

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > <span data-ttu-id="3e9e9-296">대체 ' HDInsight 클러스터의 hello 이름의 your_HDInsight_cluster_name 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-296">Replace \`your_HDInsight_cluster_name with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="3e9e9-297">메시지가 표시 되 면 hello HDInsight 관리자 로그인에 대 한 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-297">When prompted, enter hello password for hello HDInsight admin login.</span></span>
    >
    > <span data-ttu-id="3e9e9-298">이 예제에서는 Azure PowerShell이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-298">This example requires Azure PowerShell.</span></span> <span data-ttu-id="3e9e9-299">Azure PowerShell 사용에 대한 자세한 내용은 [Azure PowerShell 시작](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-299">For more information on using Azure PowerShell, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span></span>

    <span data-ttu-id="3e9e9-300">이러한 예제에서 반환 하는 hello 정보는 텍스트 다음 유사한 toohello:</span><span class="sxs-lookup"><span data-stu-id="3e9e9-300">hello information returned by these examples is similar toohello following text:</span></span>

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    <span data-ttu-id="3e9e9-301">이 정보는 스톰 toocommunicate hello HBase 클러스터에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-301">This information is used by Storm toocommunicate with hello HBase cluster.</span></span>

2. <span data-ttu-id="3e9e9-302">Hello 수정 `dev.properties` 파일을 hello 사육 쿼럼 정보 toohello 다음 줄 추가:</span><span class="sxs-lookup"><span data-stu-id="3e9e9-302">Modify hello `dev.properties` file and add hello Zookeeper quorum information toohello following line:</span></span>

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-hello-solution-toohdinsight"></a><span data-ttu-id="3e9e9-303">패키지를 빌드 및 hello 솔루션 tooHDInsight 배포</span><span class="sxs-lookup"><span data-stu-id="3e9e9-303">Build, package, and deploy hello solution tooHDInsight</span></span>

<span data-ttu-id="3e9e9-304">개발 환경에서 다음 단계 toodeploy hello Storm 토폴로지 toohello storm 클러스터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-304">In your development environment, use hello following steps toodeploy hello Storm topology toohello storm cluster.</span></span>

1. <span data-ttu-id="3e9e9-305">Hello에서 `TemperatureMonitor` 디렉터리 사용 하 여 hello 다음 tooperform 새 빌드 명령 및 프로젝트에서 JAR 패키지 만들기:</span><span class="sxs-lookup"><span data-stu-id="3e9e9-305">From hello `TemperatureMonitor` directory, use hello following command tooperform a new build and create a JAR package from your project:</span></span>
   
        mvn clean package
   
    <span data-ttu-id="3e9e9-306">이 명령은 프로젝트의 대상 디렉터리에 `TemperatureMonitor-1.0-SNAPSHOT.jar in hello `라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-306">This command creates a file named `TemperatureMonitor-1.0-SNAPSHOT.jar in hello `target\` directory of your project.</span></span>

2. <span data-ttu-id="3e9e9-307">사용 하 여 scp tooupload hello `TemperatureMonitor-1.0-SNAPSHOT.jar` 및 `dev.properties` 파일 tooyour Storm 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-307">Use scp tooupload hello `TemperatureMonitor-1.0-SNAPSHOT.jar` and `dev.properties` files tooyour Storm cluster.</span></span> <span data-ttu-id="3e9e9-308">Hello에서 다음 예제에서는 대체 `sshuser` hello 클러스터를 만들 때 제공한 hello SSH 사용자와 및 `clustername` Storm 클러스터의 hello 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-308">In hello following example, replace `sshuser` with hello SSH user you provided when creating hello cluster, and `clustername` with hello name of your Storm cluster.</span></span> <span data-ttu-id="3e9e9-309">메시지가 표시 되 면 hello SSH 사용자에 대 한 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-309">When prompted, enter hello password for hello SSH user.</span></span>
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > <span data-ttu-id="3e9e9-310">Tooupload hello 파일 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-310">It may take several minutes tooupload hello files.</span></span>

    <span data-ttu-id="3e9e9-311">Hello를 사용 하 여 대 한 자세한 내용은 `scp` 및 `ssh` HDInsight 사용 하 여 명령을 참조 [SSH HDInsight를 사용](./hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="3e9e9-311">For more information on using hello `scp` and `ssh` commands with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

3. <span data-ttu-id="3e9e9-312">Hello 파일에 업로드 되 면 SSH를 사용 하 여 toohello Storm 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-312">Once hello file has been uploaded, connect toohello Storm cluster using SSH.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="3e9e9-313">대체 `sshuser` hello SSH 사용자 이름이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-313">Replace `sshuser` with hello SSH user name.</span></span> <span data-ttu-id="3e9e9-314">대체 `clustername` hello Storm 클러스터 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-314">Replace `clustername` with hello Storm cluster name.</span></span>

4. <span data-ttu-id="3e9e9-315">toostart는 토폴로지 hello, hello 다음 hello SSH 세션에서 명령을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="3e9e9-315">toostart hello topology, use hello following command from hello SSH session:</span></span>
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * <span data-ttu-id="3e9e9-316">`--remote`hello 토폴로지 toohello hello 클러스터의 toohello 감독자 노드를 배포 하는 Nimbus 서비스에 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-316">`--remote` submits hello topology toohello Nimbus service, which distributes it toohello supervisor nodes in hello cluster.</span></span>
    * <span data-ttu-id="3e9e9-317">`--filter`사용 하 여 hello `dev.properties` hello 토폴로지 정의에서 파일 toopopulate 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-317">`--filter` uses hello `dev.properties` file toopopulate parameters in hello topology definition.</span></span>
    * <span data-ttu-id="3e9e9-318">`-R /with-hbase.yaml`사용 하 여 hello `with-hbase.yaml` 토폴로지 hello 패키지에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-318">`-R /with-hbase.yaml` uses hello `with-hbase.yaml` topology included in hello package.</span></span>

5. <span data-ttu-id="3e9e9-319">Hello 토폴로지 시작 된 후에 다음 사용 하 여 hello Azure에 게시 된 브라우저 toohello 웹 사이트 열기 `node app.js` 명령 toosend 데이터 tooEvent 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-319">After hello topology has started, open a browser toohello website you published on Azure, then use hello `node app.js` command toosend data tooEvent Hub.</span></span> <span data-ttu-id="3e9e9-320">Hello 웹 대시보드 업데이트 toodisplay hello 정보를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-320">You should see hello web dashboard update toodisplay hello information.</span></span>
   
    ![dashboard](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a><span data-ttu-id="3e9e9-322">HBase 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="3e9e9-322">View HBase data</span></span>

<span data-ttu-id="3e9e9-323">다음 단계 tooconnect tooHBase hello를 사용 하 여 하 고 있는지 hello에 데이터가 기록 된 toohello 테이블을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-323">Use hello following steps tooconnect tooHBase and verify that hello data has been written toohello table:</span></span>

1. <span data-ttu-id="3e9e9-324">SSH tooconnect toohello HBase 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-324">Use SSH tooconnect toohello HBase cluster.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="3e9e9-325">대체 `sshuser` hello SSH 사용자 이름이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-325">Replace `sshuser` with hello SSH user name.</span></span> <span data-ttu-id="3e9e9-326">대체 `clustername` hello HBase 클러스터 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-326">Replace `clustername` with hello HBase cluster name.</span></span>

2. <span data-ttu-id="3e9e9-327">Hello SSH 세션에서 hello HBase 셸을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-327">From hello SSH session, start hello HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="3e9e9-328">Hello 셸 로드 되 면 참조는 `hbase(main):001:0>` 프롬프트입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-328">Once hello shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="3e9e9-329">Hello 테이블에서 행을 보기:</span><span class="sxs-lookup"><span data-stu-id="3e9e9-329">View rows from hello table:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="3e9e9-330">이 명령은 텍스트 다음, hello 테이블에 데이터를 나타내는 비슷한 toohello 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-330">This command returns information similar toohello following text, indicating that there is data in hello table.</span></span>
   
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
   > <span data-ttu-id="3e9e9-331">이 검색 작업 hello 테이블에서 최대 10 개의 행을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-331">This scan operation returns a maximum of 10 rows from hello table.</span></span>

## <a name="delete-your-clusters"></a><span data-ttu-id="3e9e9-332">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="3e9e9-332">Delete your clusters</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="3e9e9-333">toodelete hello 클러스터, 저장소 및 웹 응용 프로그램을 포함 하는 hello 리소스 그룹을 삭제 한 번에 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-333">toodelete hello clusters, storage, and web app at one time, delete hello resource group that contains them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e9e9-334">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3e9e9-334">Next steps</span></span>

<span data-ttu-id="3e9e9-335">HDInsight의 Storm 토폴로지에 대한 자세한 내용은 [HDInsight의 Storm에 대한 예제 토폴로지](hdinsight-storm-example-topology.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-335">For more examples of Storm topologies with HDInsight, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md)</span></span>

<span data-ttu-id="3e9e9-336">Apache Storm에 대 한 자세한 내용은 참조 hello [Apache Storm](https://storm.incubator.apache.org/) 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-336">For more information about Apache Storm, see hello [Apache Storm](https://storm.incubator.apache.org/) site.</span></span>

<span data-ttu-id="3e9e9-337">HDInsight에서 HBase에 대 한 자세한 내용은 참조 hello [개요를 HDInsight HBase](hdinsight-hbase-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-337">For more information about HBase on HDInsight, see hello [HBase with HDInsight Overview](hdinsight-hbase-overview.md).</span></span>

<span data-ttu-id="3e9e9-338">Socket.io에 대 한 자세한 내용은 참조 hello [socket.io](http://socket.io/) 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-338">For more information about Socket.io, see hello [socket.io](http://socket.io/) site.</span></span>

<span data-ttu-id="3e9e9-339">D3.js에 대한 자세한 내용은 [D3.js - 데이터 기반 문서](http://d3js.org/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-339">For more information about D3.js, see [D3.js - Data Driven Documents](http://d3js.org/).</span></span>

<span data-ttu-id="3e9e9-340">Java에서 토폴로지를 만들기에 대한 자세한 내용은 [HDInsight의 Apache Storm용 Java 토폴로지 개발](hdinsight-storm-develop-java-topology.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-340">For information about creating topologies in Java, see [Develop Java topologies for Apache Storm on HDInsight](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="3e9e9-341">.NET에서 토폴로지를 만들기에 대한 자세한 내용은 [Visual Studio를 사용하여 HDInsight의 Apache Storm용 C# 토폴로지 개발](hdinsight-storm-develop-csharp-visual-studio-topology.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e9e9-341">For information about creating topologies in .NET, see [Develop C# topologies for Apache Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

[azure-portal]: https://portal.azure.com
