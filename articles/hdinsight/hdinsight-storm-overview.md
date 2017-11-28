---
title: "aaaWhat Apache Storm-Azure HDInsight는 | Microsoft Docs"
description: "Apache Storm tooprocess 실시간으로 데이터 스트림이 있습니다. Azure HDInsight 있습니다 tooeasily hello Azure 클라우드에서 Storm 클러스터를 만듭니다. Visual Studio와 함께 C#을 사용 하 여 스톰 솔루션을 만들 수 있으며 다음 tooyour HDInsight Storm 클러스터를 배포 키를 누릅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "Apache Storm 사용 사례, Storm 클러스터, Apache Storm이란?"
ms.assetid: 72d54080-1e48-4a5e-aa50-cce4ffc85077
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 6c6b2925ef3e5666dfecc3fb3c835bb362902c51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-storm-on-azure-hdinsight"></a><span data-ttu-id="bfa76-106">Azure HDInsight의 Apache Storm이란?</span><span class="sxs-lookup"><span data-stu-id="bfa76-106">What is Apache Storm on Azure HDInsight?</span></span>

<span data-ttu-id="bfa76-107">[Apache Storm](http://storm.apache.org/)은 내결함성이 있는 분산형 오픈 소스 계산 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-107">[Apache Storm](http://storm.apache.org/) is a distributed, fault-tolerant, open-source computation system.</span></span> <span data-ttu-id="bfa76-108">Hadoop으로 스톰 tooprocess 스트림을 실시간으로 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-108">You can use Storm tooprocess streams of data in real time with Hadoop.</span></span> <span data-ttu-id="bfa76-109">스톰 솔루션이 데이터의 보장 된 처리를 제공할 수도 있습니다, 그리고 hello 기능 tooreplay 성공적으로 했던 데이터를 처리 hello 처음으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-109">Storm solutions can also provide guaranteed processing of data, with hello ability tooreplay data that was not successfully processed hello first time.</span></span>

<span data-ttu-id="bfa76-110">HDInsight의 storm hello를 주요 이점은 다음을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-110">Storm on HDInsight provides hello following key benefits:</span></span>

* <span data-ttu-id="bfa76-111">가동 시간 99.9%의 SLA를 사용하여 관리되는 서비스로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-111">Performs as a managed service with an SLA of 99.9 percent uptime.</span></span>

* <span data-ttu-id="bfa76-112">생성 중 또는 생성 후에 Storm 클러스터에 대해 스크립트를 실행하여 손쉬운 사용자 지정을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-112">Supports easy customization by running scripts against a Storm cluster during or after creation.</span></span> <span data-ttu-id="bfa76-113">자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bfa76-113">For more information, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

* <span data-ttu-id="bfa76-114">다양한 언어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-114">Uses various languages.</span></span> <span data-ttu-id="bfa76-115">Hello 언어를 선택, Java, C#, 및 Python 등의 Storm 구성 요소를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-115">You can write Storm components in hello language of your choice, such as Java, C#, and Python.</span></span>

    * <span data-ttu-id="bfa76-116">HDInsight와 hello 개발, 관리 및 C# 토폴로지에 대 한 모니터링을 위한 Visual Studio를 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-116">Integrates Visual Studio with HDInsight for hello development, management, and monitoring of C# topologies.</span></span> <span data-ttu-id="bfa76-117">자세한 내용은 참조 [hello HDInsight Tools for Visual Studio로 개발 C# 스톰 토폴로지](hdinsight-storm-develop-csharp-visual-studio-topology.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-117">For more information, see [Develop C# Storm topologies with hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

    * <span data-ttu-id="bfa76-118">Hello Trident Java 인터페이스를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-118">Supports hello Trident Java interface.</span></span> <span data-ttu-id="bfa76-119">정확히 한 번의 메시지 처리, 트랜잭션 데이터 저장소 지속성 및 일반 Stream Analytics 작업 집합을 지원하는 Storm 토폴로지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-119">You can create Storm topologies that support exactly once processing of messages, transactional datastore persistence, and a set of common stream analytics operations.</span></span>

*  <span data-ttu-id="bfa76-120">Storm 클러스터의 크기를 쉽게 확장하거나 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-120">Easily scale Storm clusters up and down.</span></span> <span data-ttu-id="bfa76-121">추가 하거나 없는 영향 toorunning 스톰 토폴로지에 작업자 노드를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-121">You can add or remove worker nodes with no impact toorunning Storm topologies.</span></span>

* <span data-ttu-id="bfa76-122">Azure 서비스를 수행 하는 hello와 통합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-122">Integrates with hello following Azure services:</span></span>

    * <span data-ttu-id="bfa76-123">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="bfa76-123">Azure Event Hubs</span></span>

    * <span data-ttu-id="bfa76-124">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="bfa76-124">Azure Virtual Network</span></span>

    * <span data-ttu-id="bfa76-125">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="bfa76-125">Azure SQL Database</span></span>

    * <span data-ttu-id="bfa76-126">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="bfa76-126">Azure Storage</span></span>

    * <span data-ttu-id="bfa76-127">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bfa76-127">Azure Cosmos DB</span></span>

* <span data-ttu-id="bfa76-128">가상 네트워크를 사용 하 여 여러 HDInsight 클러스터의 hello 기능을 안전 하 게 결합 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-128">Securely combines hello capabilities of multiple HDInsight clusters by using Virtual Network.</span></span> <span data-ttu-id="bfa76-129">Storm, Kafka, Spark, HBase 또는 Hadoop 클러스터를 사용하는 분석 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-129">You can create analytic pipelines that use Storm, Kafka, Spark, HBase, or Hadoop clusters.</span></span>

<span data-ttu-id="bfa76-130">실시간 분석 솔루션에 Apache Storm을 사용하는 회사 목록은 [Apache Storm을 사용하는 회사](https://storm.apache.org/documentation/Powered-By.html)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bfa76-130">For a list of companies that are using Apache Storm for their real-time analytics solutions, see [Companies using Apache Storm](https://storm.apache.org/documentation/Powered-By.html).</span></span>

<span data-ttu-id="bfa76-131">사용 하 여 시작 tooget 참조 [HDInsight의 Storm 시작][gettingstarted]합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-131">tooget started using Storm, see [Get started with Storm on HDInsight][gettingstarted].</span></span>

## <a name="how-does-storm-work"></a><span data-ttu-id="bfa76-132">Storm 작동 방법</span><span class="sxs-lookup"><span data-stu-id="bfa76-132">How does Storm work</span></span>

<span data-ttu-id="bfa76-133">스톰에 잘 알고 있을 수 있다는 MapReduce 작업 hello 대신 토폴로지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-133">Storm runs topologies instead of hello MapReduce jobs that you might be familiar with.</span></span> <span data-ttu-id="bfa76-134">Storm 토폴로지는 DAG(방향성 비순환 그래프)에서 정렬된 여러 구성 요소로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-134">Storm topologies are composed of multiple components that are arranged in a directed acyclic graph (DAG).</span></span> <span data-ttu-id="bfa76-135">데이터가는 hello 그래프의 hello 구성 요소 간에 흐릅니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-135">Data flows between hello components in hello graph.</span></span> <span data-ttu-id="bfa76-136">각 구성 요소는 하나 이상의 데이터 스트림을 사용하며, 선택적으로 하나 이상의 스트림을 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-136">Each component consumes one or more data streams, and can optionally emit one or more streams.</span></span> <span data-ttu-id="bfa76-137">다음 다이어그램 hello 기본 단어 개수 토폴로지의 구성 요소 간 데이터 흐름 방식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-137">hello following diagram illustrates how data flows between components in a basic word-count topology:</span></span>

![Storm 토폴로지에서 구성 요소 정렬 방법의 예제](./media/hdinsight-storm-overview/example-apache-storm-topology-diagram.png)

* <span data-ttu-id="bfa76-139">Spout 구성 요소는 데이터를 토폴로지로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-139">Spout components bring data into a topology.</span></span> <span data-ttu-id="bfa76-140">스트림을 하나 이상 hello 토폴로지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-140">They emit one or more streams into hello topology.</span></span>

* <span data-ttu-id="bfa76-141">Bolt 구성 요소는 Spout 또는 다른 Bolt에서 내보낸 스트림을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-141">Bolt components consume streams emitted from spouts or other bolts.</span></span> <span data-ttu-id="bfa76-142">필요에 따라 볼트 hello 토폴로지에 스트림을 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-142">Bolts might optionally emit streams into hello topology.</span></span> <span data-ttu-id="bfa76-143">볼트는 데이터 tooexternal 서비스 또는 HDFS, Kafka, 또는 HBase 같은 저장소에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-143">Bolts are also responsible for writing data tooexternal services or storage, such as HDFS, Kafka, or HBase.</span></span>

## <a name="ease-of-creation"></a><span data-ttu-id="bfa76-144">만들기 편의성</span><span class="sxs-lookup"><span data-stu-id="bfa76-144">Ease of creation</span></span>

<span data-ttu-id="bfa76-145">HDInsight에서 새 Storm 클러스터를 몇 분 내에 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-145">You can provision a new Storm cluster on HDInsight in minutes.</span></span> <span data-ttu-id="bfa76-146">Storm 클러스터를 만드는 방법에 대한 자세한 내용은 [HDInsight에서 Storm 시작](hdinsight-apache-storm-tutorial-get-started-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bfa76-146">For more information on creating a Storm cluster, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

## <a name="ease-of-use"></a><span data-ttu-id="bfa76-147">사용 편의성</span><span class="sxs-lookup"><span data-stu-id="bfa76-147">Ease of use</span></span>

* <span data-ttu-id="bfa76-148">__SSH 연결을 보호__: SSH를 사용 하 여 hello Storm 클러스터의 헤드 노드에 hello 인터넷을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-148">__Secure Shell (SSH) connectivity__: You can access hello head nodes of your Storm cluster over hello Internet by using SSH.</span></span> <span data-ttu-id="bfa76-149">SSH를 사용하여 클러스터에서 명령을 직접 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-149">You can run commands directly on your cluster by using SSH.</span></span>

  <span data-ttu-id="bfa76-150">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bfa76-150">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="bfa76-151">__웹 연결__: 모든 HDInsight 클러스터 hello Ambari web UI를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-151">__Web connectivity__: All HDInsight clusters provide hello Ambari web UI.</span></span> <span data-ttu-id="bfa76-152">있습니다 수 쉽게 모니터링, 구성 및 hello Ambari web UI를 사용 하 여 클러스터에서 서비스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-152">You can easily monitor, configure, and manage services on your cluster by using hello Ambari web UI.</span></span> <span data-ttu-id="bfa76-153">또한 storm 클러스터 hello 스톰 UI를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-153">Storm clusters also provide hello Storm UI.</span></span> <span data-ttu-id="bfa76-154">모니터링 하 고 hello 스톰 UI를 사용 하 여 브라우저에서 실행 중인 스톰 토폴로지를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-154">You can monitor and manage running Storm topologies from your browser by using hello Storm UI.</span></span>

  <span data-ttu-id="bfa76-155">자세한 내용은 참조 hello [Ambari 웹 UI hello 관리할 HDInsight를 사용 하 여](hdinsight-hadoop-manage-ambari.md) 및 [모니터 hello 스톰 UI를 사용 하 여 관리 하 고](hdinsight-storm-deploy-monitor-topology-linux.md#monitor-and-manage-storm-ui) 문서.</span><span class="sxs-lookup"><span data-stu-id="bfa76-155">For more information, see hello [Manage HDInsight using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md) and [Monitor and manage using hello Storm UI](hdinsight-storm-deploy-monitor-topology-linux.md#monitor-and-manage-storm-ui) documents.</span></span>

* <span data-ttu-id="bfa76-156">__Azure PowerShell 및 Azure CLI__: PowerShell 및 CLI 둘 다 HDInsight 및 다른 Azure 서비스와 클라이언트 시스템 toowork 프로그램에서 사용할 수 있는 명령줄 유틸리티를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-156">__Azure PowerShell and Azure CLI__: PowerShell and CLI both provide command-line utilities that you can use from your client system toowork with HDInsight and other Azure services.</span></span>

* <span data-ttu-id="bfa76-157">__Visual Studio 통합__: Azure 데이터 레이크 Tools for Visual Studio에는 hello SCP.Net 프레임 워크를 사용 하 여 C# 스톰 토폴로지를 만들기 위한 프로젝트 템플릿이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-157">__Visual Studio integration__: Azure Data Lake Tools for Visual Studio include project templates for creating C# Storm topologies by using hello SCP.Net framework.</span></span> <span data-ttu-id="bfa76-158">또한 데이터 레이크 도구 제공 도구 toodeploy 모니터링 하며 HDInsight의 Storm 사용 하 여 솔루션을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-158">Data Lake Tools also provide tools toodeploy, monitor, and manage solutions with Storm on HDInsight.</span></span>

  <span data-ttu-id="bfa76-159">자세한 내용은 참조 [hello HDInsight Tools for Visual Studio로 개발 C# 스톰 토폴로지](hdinsight-storm-develop-csharp-visual-studio-topology.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-159">For more information, see [Develop C# Storm topologies with hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="integration-with-other-azure-services"></a><span data-ttu-id="bfa76-160">다른 Azure 서비스와 통합</span><span class="sxs-lookup"><span data-stu-id="bfa76-160">Integration with other Azure services</span></span>

* <span data-ttu-id="bfa76-161">__Azure Data Lake Store__: Storm 클러스터에서 Data Lake Store를 사용하는 예제는 [HDInsight의 Apache Storm에서 Azure Data Lake Store 사용](hdinsight-storm-write-data-lake-store.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bfa76-161">__Azure Data Lake Store__: For an example of using Data Lake Store with a Storm cluster, see [Use Azure Data Lake Store with Apache Storm on HDInsight](hdinsight-storm-write-data-lake-store.md).</span></span>

* <span data-ttu-id="bfa76-162">__이벤트 허브__: Storm 클러스터를 이벤트 허브를 사용 하는 예제를 보려면 다음 문서는 hello:</span><span class="sxs-lookup"><span data-stu-id="bfa76-162">__Event Hubs__: For an example of using Event Hubs with a Storm cluster, see hello following documents:</span></span>

    * [<span data-ttu-id="bfa76-163">HDInsight의 Storm에 대한 Java 기반 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="bfa76-163">Develop a Java-based topology for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)

    * [<span data-ttu-id="bfa76-164">HDInsight의 Storm(C#)에서 Azure Event Hubs의 이벤트 처리</span><span class="sxs-lookup"><span data-stu-id="bfa76-164">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>](hdinsight-storm-develop-csharp-event-hub-topology.md)

* <span data-ttu-id="bfa76-165">__SQL 데이터베이스__, __Cosmos DB__, __이벤트 허브__, 및 __HBase__: Visual Studio에 대 한 서식 파일 예제 hello 데이터 레이크 도구에에서 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-165">__SQL Database__, __Cosmos DB__, __Event Hubs__, and __HBase__: Template examples are included in hello Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="bfa76-166">자세한 내용은 [HDInsight의 Storm에 대한 C# 토폴로지 개발](hdinsight-storm-develop-csharp-visual-studio-topology.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bfa76-166">For more information, see [Develop a C# topology for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="reliability"></a><span data-ttu-id="bfa76-167">안정성</span><span class="sxs-lookup"><span data-stu-id="bfa76-167">Reliability</span></span>

<span data-ttu-id="bfa76-168">Apache Storm 들어오는 각 메시지는 항상 완전히 처리 하, 수백 개의 노드에 걸쳐 hello 데이터 분석 하는 경우에 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-168">Apache Storm guarantees that each incoming message is always fully processed, even when hello data analysis is spread over hundreds of nodes.</span></span>

<span data-ttu-id="bfa76-169">hello Nimbus 노드 기능 비슷한 toohello Hadoop JobTracker 하며 tooother 노드 사육을 통해 클러스터에서 작업에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-169">hello Nimbus node provides functionality similar toohello Hadoop JobTracker, and it assigns tasks tooother nodes in a cluster through Zookeeper.</span></span> <span data-ttu-id="bfa76-170">사육 노드가 클러스터에 대 한 조정 제공 하 고 Nimbus와 hello hello 작업자 노드에서 감독자 프로세스 간의 통신을 용이 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-170">Zookeeper nodes provide coordination for a cluster and facilitate communication between Nimbus and hello Supervisor process on hello worker nodes.</span></span> <span data-ttu-id="bfa76-171">하나의 처리 노드가 다운 되 면 hello Nimbus 노드 정보를 얻으려면 및 hello 작업과 연결 된 데이터 tooanother 노드에 자동으로 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-171">If one processing node goes down, hello Nimbus node is informed, and it assigns hello task and associated data tooanother node.</span></span>

<span data-ttu-id="bfa76-172">Apache Storm 클러스터에 대 한 기본 구성 hello는 toohave 하나만 Nimbus 노드입니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-172">hello default configuration for Apache Storm clusters is toohave only one Nimbus node.</span></span> <span data-ttu-id="bfa76-173">HDInsight의 Storm은 두 개의 Nimbus 노드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-173">Storm on HDInsight provides two Nimbus nodes.</span></span> <span data-ttu-id="bfa76-174">Hello 주 노드에 장애가 hello 주 노드를 복구 하는 동안 hello Storm 클러스터 toohello 보조 노드를 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-174">If hello primary node fails, hello Storm cluster switches toohello secondary node while hello primary node is recovered.</span></span> <span data-ttu-id="bfa76-175">hello 다음 다이어그램에서는 HDInsight의 Storm의 hello 작업 흐름 구성을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-175">hello following diagram illustrates hello task flow configuration for Storm on HDInsight:</span></span>

![nimbus, zookeeper 및 감독자 다이어그램](./media/hdinsight-storm-overview/nimbus.png)

## <a name="scale"></a><span data-ttu-id="bfa76-177">크기 조정</span><span class="sxs-lookup"><span data-stu-id="bfa76-177">Scale</span></span>

<span data-ttu-id="bfa76-178">작업자 노드를 추가하거나 제거하여 HDInsight 클러스터의 크기를 동적으로 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-178">HDInsight clusters can be dynamically scaled by adding or removing worker nodes.</span></span> <span data-ttu-id="bfa76-179">이 작업은 데이터를 처리하는 동안 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-179">This operation can be performed while processing data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bfa76-180">새 노드 tootake 활용 toorebalance 스톰 토폴로지 hello 클러스터 크기를 증가 하기 전에 시작 해야 크기 조정을 통해 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-180">tootake advantage of new nodes added through scaling, you need toorebalance Storm topologies started before hello cluster size was increased.</span></span>

## <a name="support"></a><span data-ttu-id="bfa76-181">지원</span><span class="sxs-lookup"><span data-stu-id="bfa76-181">Support</span></span>

<span data-ttu-id="bfa76-182">HDInsight의 Storm에는 완전한 엔터프라이즈 수준의 연속 지원이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-182">Storm on HDInsight comes with full enterprise-level continuous support.</span></span> <span data-ttu-id="bfa76-183">HDInsight의 Storm에는 99.9%의 SLA도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-183">Storm on HDInsight also has an SLA of 99.9 percent.</span></span> <span data-ttu-id="bfa76-184">즉, Storm 클러스터 연결 되어 있는지 외부 hello 시간의 99.9% 이상 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-184">That means we guarantee that a Storm cluster has external connectivity at least 99.9 percent of hello time.</span></span>

<span data-ttu-id="bfa76-185">자세한 내용은 [Azure 지원](https://azure.microsoft.com/support/options/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bfa76-185">For more information, see [Azure support](https://azure.microsoft.com/support/options/).</span></span>

## <a name="apache-storm-use-cases"></a><span data-ttu-id="bfa76-186">Apache Storm 사용 사례</span><span class="sxs-lookup"><span data-stu-id="bfa76-186">Apache Storm use cases</span></span>

<span data-ttu-id="bfa76-187">hello 다음은 몇 가지 일반적인 시나리오를 위해 HDInsight의 Storm를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-187">hello following are some common scenarios for which you might use Storm on HDInsight:</span></span>

* <span data-ttu-id="bfa76-188">IoT(사물 인터넷)</span><span class="sxs-lookup"><span data-stu-id="bfa76-188">Internet of Things (IoT)</span></span>
* <span data-ttu-id="bfa76-189">부정 행위 감지</span><span class="sxs-lookup"><span data-stu-id="bfa76-189">Fraud detection</span></span>
* <span data-ttu-id="bfa76-190">소셜 분석</span><span class="sxs-lookup"><span data-stu-id="bfa76-190">Social analytics</span></span>
* <span data-ttu-id="bfa76-191">추출, 변환 및 로드(ETL)</span><span class="sxs-lookup"><span data-stu-id="bfa76-191">Extraction, transformation, and loading (ETL)</span></span>
* <span data-ttu-id="bfa76-192">네트워크 모니터링</span><span class="sxs-lookup"><span data-stu-id="bfa76-192">Network monitoring</span></span>
* <span data-ttu-id="bfa76-193">검색</span><span class="sxs-lookup"><span data-stu-id="bfa76-193">Search</span></span>
* <span data-ttu-id="bfa76-194">모바일 고객 관리</span><span class="sxs-lookup"><span data-stu-id="bfa76-194">Mobile engagement</span></span>

<span data-ttu-id="bfa76-195">실제 시나리오에 대 한 정보를 참조 hello [회사 스톰 사용 하는 방식과](https://storm.apache.org/documentation/Powered-By.html) 문서.</span><span class="sxs-lookup"><span data-stu-id="bfa76-195">For information about real-world scenarios, see hello [How companies are using Storm](https://storm.apache.org/documentation/Powered-By.html) document.</span></span>

## <a name="development"></a><span data-ttu-id="bfa76-196">개발</span><span class="sxs-lookup"><span data-stu-id="bfa76-196">Development</span></span>

<span data-ttu-id="bfa76-197">Data Lake Tools for Visual Studio를 사용하면 .NET 개발자는 C#으로 토폴로지를 디자인하고 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-197">.NET developers can design and implement topologies in C# by using Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="bfa76-198">또한 Java 및 C# 구성 요소를 사용하는 하이브리드 토폴로지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-198">You can also create hybrid topologies that use Java and C# components.</span></span>

<span data-ttu-id="bfa76-199">자세한 내용은 [Visual Studio를 사용하여 HDInsight에서 Storm에 대한 C# 토폴로지 개발](hdinsight-storm-develop-csharp-visual-studio-topology.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bfa76-199">For more information, see [Develop C# topologies for Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="bfa76-200">또한 사용자가 선택한 IDE hello를 사용 하 여 Java 솔루션을 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-200">You can also develop Java solutions by using hello IDE of your choice.</span></span> <span data-ttu-id="bfa76-201">자세한 내용은 [HDInsight의 Storm에 대한 Java 토폴로지 개발](hdinsight-storm-develop-java-topology.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bfa76-201">For more information, see [Develop Java topologies for Storm on HDInsight](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="bfa76-202">Python에서 사용 되는 toodevelop Storm 구성 요소를 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-202">Python can also be used toodevelop Storm components.</span></span> <span data-ttu-id="bfa76-203">자세한 내용은 [HDInsight에서 Python을 사용하여 Storm 토폴로지 개발](hdinsight-storm-develop-python-topology.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bfa76-203">For more information, see [Develop Storm topologies using Python on HDInsight](hdinsight-storm-develop-python-topology.md).</span></span>

## <a name="common-development-patterns"></a><span data-ttu-id="bfa76-204">일반적인 개발 패턴</span><span class="sxs-lookup"><span data-stu-id="bfa76-204">Common development patterns</span></span>

### <a name="guaranteed-message-processing"></a><span data-ttu-id="bfa76-205">메시지 처리 보장</span><span class="sxs-lookup"><span data-stu-id="bfa76-205">Guaranteed message processing</span></span>

<span data-ttu-id="bfa76-206">Apache Storm은 다양한 수준의 보장된 메시지 처리를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-206">Apache Storm can provide different levels of guaranteed message processing.</span></span> <span data-ttu-id="bfa76-207">예를 들어 기본적인 Storm 응용 프로그램은 최소한 한 번 처리를 보장할 수 있고 Trident는 정확히 한 번 처리를 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-207">For example, a basic Storm application can guarantee at-least-once processing, and Trident can guarantee exactly once processing.</span></span>

<span data-ttu-id="bfa76-208">자세한 내용은 apache.org에서 [데이터 처리 보장](https://storm.apache.org/about/guarantees-data-processing.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bfa76-208">For more information, see [Guarantees on data processing](https://storm.apache.org/about/guarantees-data-processing.html) at apache.org.</span></span>

### <a name="ibasicbolt"></a><span data-ttu-id="bfa76-209">IBasicBolt</span><span class="sxs-lookup"><span data-stu-id="bfa76-209">IBasicBolt</span></span>

<span data-ttu-id="bfa76-210">0 개 이상의 튜플로 구성 내보내기 입력된 튜플과 읽을 패턴 hello을 hello의 hello 끝에 즉시 응답 hello 입력된 튜플 메서드를 실행 하는 다음이 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-210">hello pattern of reading an input tuple, emitting zero or more tuples, and then acking hello input tuple immediately at hello end of hello execute method is common.</span></span> <span data-ttu-id="bfa76-211">Storm 제공 hello [IBasicBolt](https://storm.apache.org/releases/1.0.3/javadocs/org/apache/storm/topology/IBasicBolt.html) 인터페이스 tooautomate이이 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-211">Storm provides hello [IBasicBolt](https://storm.apache.org/releases/1.0.3/javadocs/org/apache/storm/topology/IBasicBolt.html) interface tooautomate this pattern.</span></span>

### <a name="joins"></a><span data-ttu-id="bfa76-212">조인</span><span class="sxs-lookup"><span data-stu-id="bfa76-212">Joins</span></span>

<span data-ttu-id="bfa76-213">데이터 스트림이 조인되는 방식은 응용 프로그램마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-213">How data streams are joined varies between applications.</span></span> <span data-ttu-id="bfa76-214">예를 들어 여러 스트림의 각 튜플을 새 스트림 하나에 조인할 수도 있고 특정 창에 대한 튜플 배치만 조인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-214">For example, you can join each tuple from multiple streams into one new stream, or you can join only batches of tuples for a specific window.</span></span> <span data-ttu-id="bfa76-215">어떤 방법을 사용하든 [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-)을 통해 조인을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-215">Either way, joining can be accomplished by using [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-).</span></span> <span data-ttu-id="bfa76-216">그룹화 필드는 방법은 튜플 라우트된 toobolts는 하는 방법을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-216">Field grouping is a way of defining how tuples are routed toobolts.</span></span>

<span data-ttu-id="bfa76-217">다음 예에서는 Java hello, fieldsGrouping toohello MyJoiner 볼트 "1", "2", "3" 구성 요소에서에서 생성 되는 사용 되는 tooroute 튜플입니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-217">In hello following Java example, fieldsGrouping is used tooroute tuples that originate from components "1", "2", and "3" toohello MyJoiner bolt:</span></span>

    builder.setBolt("join", new MyJoiner(), parallelism) .fieldsGrouping("1", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("2", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("3", new Fields("joinfield1", "joinfield2"));

### <a name="batches"></a><span data-ttu-id="bfa76-218">일괄 처리</span><span class="sxs-lookup"><span data-stu-id="bfa76-218">Batches</span></span>

<span data-ttu-id="bfa76-219">Apache Storm은 "틱 튜플(tick tuple)"이라고 하는 내부 타이밍 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-219">Apache Storm provides an internal timing mechanism known as a "tick tuple."</span></span> <span data-ttu-id="bfa76-220">토폴로지에서 틱 튜플을 내보내는 빈도를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-220">You can set how often a tick tuple is emitted in your topology.</span></span>

<span data-ttu-id="bfa76-221">C# 구성 요소에서 틱 튜플을 사용하는 예제는 [PartialBoltCount.cs](https://github.com/hdinsight/hdinsight-storm-examples/blob/3b2c960549cac122e8874931df4801f0934fffa7/EventCountExample/EventCountTopology/src/main/java/com/microsoft/hdinsight/storm/examples/PartialCountBolt.java)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bfa76-221">For an example of using a tick tuple from a C# component, see [PartialBoltCount.cs](https://github.com/hdinsight/hdinsight-storm-examples/blob/3b2c960549cac122e8874931df4801f0934fffa7/EventCountExample/EventCountTopology/src/main/java/com/microsoft/hdinsight/storm/examples/PartialCountBolt.java).</span></span>

### <a name="caches"></a><span data-ttu-id="bfa76-222">캐시</span><span class="sxs-lookup"><span data-stu-id="bfa76-222">Caches</span></span>

<span data-ttu-id="bfa76-223">메모리 내 캐싱은 자주 사용되는 자산을 메모리에 저장하므로 처리 속도를 높이기 위한 메커니즘으로 사용되는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-223">In-memory caching is often used as a mechanism for speeding up processing because it keeps frequently used assets in memory.</span></span> <span data-ttu-id="bfa76-224">토폴로지는 여러 노드 및 각 노드 내의 여러 프로세스로 분산되므로 [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-)을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-224">Because a topology is distributed across multiple nodes, and multiple processes within each node, you should consider using [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-).</span></span> <span data-ttu-id="bfa76-225">사용 하 여 `fieldsGrouping` tooensure 캐시 조회에 사용 되는 hello 필드를 포함 하는 튜플이 라우트된 toohello는 항상 동일한 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-225">Use `fieldsGrouping` tooensure that tuples containing hello fields that are used for cache lookup are always routed toohello same process.</span></span> <span data-ttu-id="bfa76-226">이 그룹화 기능으로 프로세스 간 캐시 항목 중복을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-226">This grouping functionality avoids duplication of cache entries across processes.</span></span>

### <a name="stream-top-n"></a><span data-ttu-id="bfa76-227">스트림 “상위 N”</span><span class="sxs-lookup"><span data-stu-id="bfa76-227">Stream "top N"</span></span>

<span data-ttu-id="bfa76-228">토폴로지에 상위 n 개 값을 계산에 따라 달라 집니다 때 병렬로 hello 상위 n 개 값을 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-228">When your topology depends on calculating a top N value, calculate hello top N value in parallel.</span></span> <span data-ttu-id="bfa76-229">다음 전역 값에 해당 계산에서 출력 hello를 병합 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-229">Then merge hello output from those calculations into a global value.</span></span> <span data-ttu-id="bfa76-230">사용 하 여이 작업을 수행할 수 [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-) 필드 병렬 처리에 의해 tooroute 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-230">This operation can be done by using [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-) tooroute by field for parallel processing.</span></span> <span data-ttu-id="bfa76-231">그런 다음 전역 hello 상위 n 개 값을 결정 하는 tooa 볼트를 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-231">Then you can route tooa bolt that globally determines hello top N value.</span></span>

<span data-ttu-id="bfa76-232">상위 n 개 값을 계산한 다음의 예를 들어 참조 hello [RollingTopWords](https://github.com/apache/storm/blob/master/examples/storm-starter/src/jvm/org/apache/storm/starter/RollingTopWords.java) 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-232">For an example of calculating a top N value, see hello [RollingTopWords](https://github.com/apache/storm/blob/master/examples/storm-starter/src/jvm/org/apache/storm/starter/RollingTopWords.java) example.</span></span>

## <a name="logging"></a><span data-ttu-id="bfa76-233">로깅</span><span class="sxs-lookup"><span data-stu-id="bfa76-233">Logging</span></span>

<span data-ttu-id="bfa76-234">Storm은 Apache Log4j toolog 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-234">Storm uses Apache Log4j toolog information.</span></span> <span data-ttu-id="bfa76-235">기본적으로 많은 양의 데이터가 기록 되 고 hello 정보를 통해 어려운 toosort 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-235">By default, a large amount of data is logged, and it can be difficult toosort through hello information.</span></span> <span data-ttu-id="bfa76-236">Storm 토폴로지 toocontrol 로깅 동작의 일부로 로깅 구성 파일을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-236">You can include a logging configuration file as part of your Storm topology toocontrol logging behavior.</span></span>

<span data-ttu-id="bfa76-237">보여 주는 토폴로지 예제에 대 한 로깅 tooconfigure 참조 하는 방법을 [Java 기반 WordCount](hdinsight-storm-develop-java-topology.md) HDInsight의 Storm의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-237">For an example topology that demonstrates how tooconfigure logging, see [Java-based WordCount](hdinsight-storm-develop-java-topology.md) example for Storm on HDInsight.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfa76-238">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bfa76-238">Next steps</span></span>

<span data-ttu-id="bfa76-239">HDInsight의 Storm을 사용한 실시간 분석 솔루션에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="bfa76-239">Learn more about real-time analytics solutions with Storm on HDInsight:</span></span>

* <span data-ttu-id="bfa76-240">[HDInsight의 Apache Storm 시작][gettingstarted]</span><span class="sxs-lookup"><span data-stu-id="bfa76-240">[Get started with Apache Storm on HDInsight][gettingstarted]</span></span>
* [<span data-ttu-id="bfa76-241">HDInsight의 Apache Storm에 대한 예제 토폴로지</span><span class="sxs-lookup"><span data-stu-id="bfa76-241">Example topologies for Apache Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

[stormtrident]: https://storm.apache.org/documentation/Trident-API-Overview.html
[samoa]: http://yahooeng.tumblr.com/post/65453012905/introducing-samoa-an-open-source-platform-for-mining
[apachetutorial]: https://storm.apache.org/documentation/Tutorial.html
[gettingstarted]: hdinsight-apache-storm-tutorial-get-started-linux.md
