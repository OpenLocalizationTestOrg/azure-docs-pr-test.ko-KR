---
title: "Apache Storm이란? - Azure HDInsight | Microsoft Docs"
description: "Apache Storm을 사용하면 데이터 스트림을 실시간으로 처리할 수 있습니다. Azure HDInsight를 사용하면 Azure 클라우드에 Storm 클러스터를 쉽게 만들 수 있습니다. Visual Studio를 사용하면 C#을 사용하여 Storm 솔루션을 만든 다음 HDInsight Storm 클러스터에 배포할 수 있습니다."
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
ms.openlocfilehash: 073672f1223313938baedee027072cb96062294b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="what-is-apache-storm-on-azure-hdinsight"></a><span data-ttu-id="defe8-106">Azure HDInsight의 Apache Storm이란?</span><span class="sxs-lookup"><span data-stu-id="defe8-106">What is Apache Storm on Azure HDInsight?</span></span>

<span data-ttu-id="defe8-107">[Apache Storm](http://storm.apache.org/)은 내결함성이 있는 분산형 오픈 소스 계산 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-107">[Apache Storm](http://storm.apache.org/) is a distributed, fault-tolerant, open-source computation system.</span></span> <span data-ttu-id="defe8-108">Storm을 사용하여 Hadoop에서 실시간으로 데이터 스트림을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-108">You can use Storm to process streams of data in real time with Hadoop.</span></span> <span data-ttu-id="defe8-109">또한 Storm 솔루션은 처음에 정상적으로 처리되지 않은 데이터를 재생하는 기능을 통해 데이터 처리를 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-109">Storm solutions can also provide guaranteed processing of data, with the ability to replay data that was not successfully processed the first time.</span></span>

<span data-ttu-id="defe8-110">HDInsight의 Storm은 다음과 같은 주요 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-110">Storm on HDInsight provides the following key benefits:</span></span>

* <span data-ttu-id="defe8-111">가동 시간 99.9%의 SLA를 사용하여 관리되는 서비스로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-111">Performs as a managed service with an SLA of 99.9 percent uptime.</span></span>

* <span data-ttu-id="defe8-112">생성 중 또는 생성 후에 Storm 클러스터에 대해 스크립트를 실행하여 손쉬운 사용자 지정을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-112">Supports easy customization by running scripts against a Storm cluster during or after creation.</span></span> <span data-ttu-id="defe8-113">자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="defe8-113">For more information, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

* <span data-ttu-id="defe8-114">다양한 언어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-114">Uses various languages.</span></span> <span data-ttu-id="defe8-115">Java, C# 및 Python과 같은 사용자가 선택한 언어로 Storm 구성 요소를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-115">You can write Storm components in the language of your choice, such as Java, C#, and Python.</span></span>

    * <span data-ttu-id="defe8-116">C# 토폴로지의 개발, 관리 및 모니터링을 위해 HDInsight와 Visual Studio를 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-116">Integrates Visual Studio with HDInsight for the development, management, and monitoring of C# topologies.</span></span> <span data-ttu-id="defe8-117">자세한 내용은 [Visual Studio용 HDInsight를 사용하여 C# Storm 토폴로지 개발](hdinsight-storm-develop-csharp-visual-studio-topology.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="defe8-117">For more information, see [Develop C# Storm topologies with the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

    * <span data-ttu-id="defe8-118">Trident Java 인터페이스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-118">Supports the Trident Java interface.</span></span> <span data-ttu-id="defe8-119">정확히 한 번의 메시지 처리, 트랜잭션 데이터 저장소 지속성 및 일반 Stream Analytics 작업 집합을 지원하는 Storm 토폴로지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-119">You can create Storm topologies that support exactly once processing of messages, transactional datastore persistence, and a set of common stream analytics operations.</span></span>

*  <span data-ttu-id="defe8-120">Storm 클러스터의 크기를 쉽게 확장하거나 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-120">Easily scale Storm clusters up and down.</span></span> <span data-ttu-id="defe8-121">실행 중인 Storm 토폴로지에 영향을 주지 않고 작업자 노드를 추가하거나 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-121">You can add or remove worker nodes with no impact to running Storm topologies.</span></span>

* <span data-ttu-id="defe8-122">다음 Azure 서비스와의 통합:</span><span class="sxs-lookup"><span data-stu-id="defe8-122">Integrates with the following Azure services:</span></span>

    * <span data-ttu-id="defe8-123">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="defe8-123">Azure Event Hubs</span></span>

    * <span data-ttu-id="defe8-124">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="defe8-124">Azure Virtual Network</span></span>

    * <span data-ttu-id="defe8-125">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="defe8-125">Azure SQL Database</span></span>

    * <span data-ttu-id="defe8-126">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="defe8-126">Azure Storage</span></span>

    * <span data-ttu-id="defe8-127">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="defe8-127">Azure Cosmos DB</span></span>

* <span data-ttu-id="defe8-128">Virtual Network를 사용하여 여러 HDInsight 클러스터의 기능을 안전하게 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-128">Securely combines the capabilities of multiple HDInsight clusters by using Virtual Network.</span></span> <span data-ttu-id="defe8-129">Storm, Kafka, Spark, HBase 또는 Hadoop 클러스터를 사용하는 분석 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-129">You can create analytic pipelines that use Storm, Kafka, Spark, HBase, or Hadoop clusters.</span></span>

<span data-ttu-id="defe8-130">실시간 분석 솔루션에 Apache Storm을 사용하는 회사 목록은 [Apache Storm을 사용하는 회사](https://storm.apache.org/documentation/Powered-By.html)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="defe8-130">For a list of companies that are using Apache Storm for their real-time analytics solutions, see [Companies using Apache Storm](https://storm.apache.org/documentation/Powered-By.html).</span></span>

<span data-ttu-id="defe8-131">Storm 사용을 시작하려면 [HDInsight에서 Storm 시작][gettingstarted]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="defe8-131">To get started using Storm, see [Get started with Storm on HDInsight][gettingstarted].</span></span>

## <a name="how-does-storm-work"></a><span data-ttu-id="defe8-132">Storm 작동 방법</span><span class="sxs-lookup"><span data-stu-id="defe8-132">How does Storm work</span></span>

<span data-ttu-id="defe8-133">Storm에서는 친숙한 MapReduce 작업 대신 토폴로지를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-133">Storm runs topologies instead of the MapReduce jobs that you might be familiar with.</span></span> <span data-ttu-id="defe8-134">Storm 토폴로지는 DAG(방향성 비순환 그래프)에서 정렬된 여러 구성 요소로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-134">Storm topologies are composed of multiple components that are arranged in a directed acyclic graph (DAG).</span></span> <span data-ttu-id="defe8-135">그래프의 구성 요소 간에 데이터가 흐릅니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-135">Data flows between the components in the graph.</span></span> <span data-ttu-id="defe8-136">각 구성 요소는 하나 이상의 데이터 스트림을 사용하며, 선택적으로 하나 이상의 스트림을 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-136">Each component consumes one or more data streams, and can optionally emit one or more streams.</span></span> <span data-ttu-id="defe8-137">다음 다이어그램은 기본 단어 개수 토폴로지에 있는 구성 요소 간에 데이터가 흐르는 방식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-137">The following diagram illustrates how data flows between components in a basic word-count topology:</span></span>

![Storm 토폴로지에서 구성 요소 정렬 방법의 예제](./media/hdinsight-storm-overview/example-apache-storm-topology-diagram.png)

* <span data-ttu-id="defe8-139">Spout 구성 요소는 데이터를 토폴로지로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-139">Spout components bring data into a topology.</span></span> <span data-ttu-id="defe8-140">하나 이상의 스트림을 토폴로지에 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-140">They emit one or more streams into the topology.</span></span>

* <span data-ttu-id="defe8-141">Bolt 구성 요소는 Spout 또는 다른 Bolt에서 내보낸 스트림을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-141">Bolt components consume streams emitted from spouts or other bolts.</span></span> <span data-ttu-id="defe8-142">Bolt는 필요에 따라 스트림을 토폴로지로 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-142">Bolts might optionally emit streams into the topology.</span></span> <span data-ttu-id="defe8-143">또한 Bolt는 HDFS, Kafka 또는 HBase와 같은 외부 서비스 또는 저장소에 데이터를 쓰는 역할을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-143">Bolts are also responsible for writing data to external services or storage, such as HDFS, Kafka, or HBase.</span></span>

## <a name="ease-of-creation"></a><span data-ttu-id="defe8-144">만들기 편의성</span><span class="sxs-lookup"><span data-stu-id="defe8-144">Ease of creation</span></span>

<span data-ttu-id="defe8-145">HDInsight에서 새 Storm 클러스터를 몇 분 내에 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-145">You can provision a new Storm cluster on HDInsight in minutes.</span></span> <span data-ttu-id="defe8-146">Storm 클러스터를 만드는 방법에 대한 자세한 내용은 [HDInsight에서 Storm 시작](hdinsight-apache-storm-tutorial-get-started-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="defe8-146">For more information on creating a Storm cluster, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

## <a name="ease-of-use"></a><span data-ttu-id="defe8-147">사용 편의성</span><span class="sxs-lookup"><span data-stu-id="defe8-147">Ease of use</span></span>

* <span data-ttu-id="defe8-148">__SSH(보안 셸) 연결__: SSH를 사용하여 인터넷을 통해 Storm 클러스터의 헤드 노드에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-148">__Secure Shell (SSH) connectivity__: You can access the head nodes of your Storm cluster over the Internet by using SSH.</span></span> <span data-ttu-id="defe8-149">SSH를 사용하여 클러스터에서 명령을 직접 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-149">You can run commands directly on your cluster by using SSH.</span></span>

  <span data-ttu-id="defe8-150">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="defe8-150">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="defe8-151">__웹 연결__: 모든 HDInsight 클러스터는 Ambari 웹 UI를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-151">__Web connectivity__: All HDInsight clusters provide the Ambari web UI.</span></span> <span data-ttu-id="defe8-152">Ambari 웹 UI를 사용하여 클러스터에서 서비스를 쉽게 모니터링, 구성 및 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-152">You can easily monitor, configure, and manage services on your cluster by using the Ambari web UI.</span></span> <span data-ttu-id="defe8-153">또한 Storm 클러스터는 Storm UI도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-153">Storm clusters also provide the Storm UI.</span></span> <span data-ttu-id="defe8-154">Storm UI를 사용하여 브라우저에서 실행 중인 Storm 토폴로지를 모니터링 및 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-154">You can monitor and manage running Storm topologies from your browser by using the Storm UI.</span></span>

  <span data-ttu-id="defe8-155">자세한 내용은 [Ambari 웹 UI를 사용하여 HDInsight 관리](hdinsight-hadoop-manage-ambari.md) 및 [Storm UI를 사용하여 모니터링 및 관리](hdinsight-storm-deploy-monitor-topology-linux.md#monitor-and-manage-storm-ui) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="defe8-155">For more information, see the [Manage HDInsight using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md) and [Monitor and manage using the Storm UI](hdinsight-storm-deploy-monitor-topology-linux.md#monitor-and-manage-storm-ui) documents.</span></span>

* <span data-ttu-id="defe8-156">__Azure PowerShell 및 Azure CLI__: PowerShell 및 CLI는 HDInsight 및 다른 Azure 서비스를 사용하는 클라이언트 시스템에서 사용할 수 있는 명령줄 유틸리티를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-156">__Azure PowerShell and Azure CLI__: PowerShell and CLI both provide command-line utilities that you can use from your client system to work with HDInsight and other Azure services.</span></span>

* <span data-ttu-id="defe8-157">__Visual Studio 통합__: Azure Data Lake Tools for Visual Studio에는 SCP.Net Framework를 사용하여 C# Storm 토폴로지를 만드는 프로젝트 템플릿이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-157">__Visual Studio integration__: Azure Data Lake Tools for Visual Studio include project templates for creating C# Storm topologies by using the SCP.Net framework.</span></span> <span data-ttu-id="defe8-158">또한 Data Lake 도구는 HDInsight의 Storm을 사용하여 솔루션을 배포, 모니터링 및 관리하는 도구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-158">Data Lake Tools also provide tools to deploy, monitor, and manage solutions with Storm on HDInsight.</span></span>

  <span data-ttu-id="defe8-159">자세한 내용은 [Visual Studio용 HDInsight를 사용하여 C# Storm 토폴로지 개발](hdinsight-storm-develop-csharp-visual-studio-topology.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="defe8-159">For more information, see [Develop C# Storm topologies with the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="integration-with-other-azure-services"></a><span data-ttu-id="defe8-160">다른 Azure 서비스와 통합</span><span class="sxs-lookup"><span data-stu-id="defe8-160">Integration with other Azure services</span></span>

* <span data-ttu-id="defe8-161">__Azure Data Lake Store__: Storm 클러스터에서 Data Lake Store를 사용하는 예제는 [HDInsight의 Apache Storm에서 Azure Data Lake Store 사용](hdinsight-storm-write-data-lake-store.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="defe8-161">__Azure Data Lake Store__: For an example of using Data Lake Store with a Storm cluster, see [Use Azure Data Lake Store with Apache Storm on HDInsight](hdinsight-storm-write-data-lake-store.md).</span></span>

* <span data-ttu-id="defe8-162">__Event Hubs__: Storm 클러스터에서 Event Hubs를 사용하는 예제는 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="defe8-162">__Event Hubs__: For an example of using Event Hubs with a Storm cluster, see the following documents:</span></span>

    * [<span data-ttu-id="defe8-163">HDInsight의 Storm에 대한 Java 기반 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="defe8-163">Develop a Java-based topology for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)

    * [<span data-ttu-id="defe8-164">HDInsight의 Storm(C#)에서 Azure Event Hubs의 이벤트 처리</span><span class="sxs-lookup"><span data-stu-id="defe8-164">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>](hdinsight-storm-develop-csharp-event-hub-topology.md)

* <span data-ttu-id="defe8-165">__SQL Database__, __Cosmos DB__, __Event Hubs__ 및 __HBase__: 템플릿 예제는 Data Lake Tools for Visual Studio에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-165">__SQL Database__, __Cosmos DB__, __Event Hubs__, and __HBase__: Template examples are included in the Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="defe8-166">자세한 내용은 [HDInsight의 Storm에 대한 C# 토폴로지 개발](hdinsight-storm-develop-csharp-visual-studio-topology.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="defe8-166">For more information, see [Develop a C# topology for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="reliability"></a><span data-ttu-id="defe8-167">안정성</span><span class="sxs-lookup"><span data-stu-id="defe8-167">Reliability</span></span>

<span data-ttu-id="defe8-168">Apache Storm은 데이터 분석이 수백 개의 노드에 분산되어 있는 경우에도 들어오는 각 메시지를 항상 완전히 처리하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-168">Apache Storm guarantees that each incoming message is always fully processed, even when the data analysis is spread over hundreds of nodes.</span></span>

<span data-ttu-id="defe8-169">Nimbus 노드는 Hadoop JobTracker와 유사한 기능을 제공하며 Zookeeper를 통해 클러스터의 다른 노드에 태스크를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-169">The Nimbus node provides functionality similar to the Hadoop JobTracker, and it assigns tasks to other nodes in a cluster through Zookeeper.</span></span> <span data-ttu-id="defe8-170">Zookeeper 노드는 클러스터에 대한 조정을 제공하며, Nimbus와 작업자 노드의 감독자 프로세스 간의 통신을 용이하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-170">Zookeeper nodes provide coordination for a cluster and facilitate communication between Nimbus and the Supervisor process on the worker nodes.</span></span> <span data-ttu-id="defe8-171">하나의 처리 노드가 작동이 중지되면 Nimbus 노드에 알림이 제공되고 이 노드에서 작업 및 관련 데이터를 다른 노드에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-171">If one processing node goes down, the Nimbus node is informed, and it assigns the task and associated data to another node.</span></span>

<span data-ttu-id="defe8-172">Apache Storm 클러스터의 기본 구성에는 Nimbus 노드 하나만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-172">The default configuration for Apache Storm clusters is to have only one Nimbus node.</span></span> <span data-ttu-id="defe8-173">HDInsight의 Storm은 두 개의 Nimbus 노드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-173">Storm on HDInsight provides two Nimbus nodes.</span></span> <span data-ttu-id="defe8-174">주 노드에 장애가 발생하면 주 노드가 복구되는 동안 Storm 클러스터에서 보조 노드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-174">If the primary node fails, the Storm cluster switches to the secondary node while the primary node is recovered.</span></span> <span data-ttu-id="defe8-175">다음 다이어그램은 HDInsight에서 Storm에 대한 작업 흐름 구성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-175">The following diagram illustrates the task flow configuration for Storm on HDInsight:</span></span>

![nimbus, zookeeper 및 감독자 다이어그램](./media/hdinsight-storm-overview/nimbus.png)

## <a name="scale"></a><span data-ttu-id="defe8-177">크기 조정</span><span class="sxs-lookup"><span data-stu-id="defe8-177">Scale</span></span>

<span data-ttu-id="defe8-178">작업자 노드를 추가하거나 제거하여 HDInsight 클러스터의 크기를 동적으로 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-178">HDInsight clusters can be dynamically scaled by adding or removing worker nodes.</span></span> <span data-ttu-id="defe8-179">이 작업은 데이터를 처리하는 동안 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-179">This operation can be performed while processing data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="defe8-180">크기 조정을 통해 추가된 새 노드를 활용하려면 클러스터 크기를 늘리기 전에 시작된 Storm 토폴로지의 균형을 다시 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-180">To take advantage of new nodes added through scaling, you need to rebalance Storm topologies started before the cluster size was increased.</span></span>

## <a name="support"></a><span data-ttu-id="defe8-181">지원</span><span class="sxs-lookup"><span data-stu-id="defe8-181">Support</span></span>

<span data-ttu-id="defe8-182">HDInsight의 Storm에는 완전한 엔터프라이즈 수준의 연속 지원이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-182">Storm on HDInsight comes with full enterprise-level continuous support.</span></span> <span data-ttu-id="defe8-183">HDInsight의 Storm에는 99.9%의 SLA도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-183">Storm on HDInsight also has an SLA of 99.9 percent.</span></span> <span data-ttu-id="defe8-184">즉 Storm 클러스터에서 적어도 99.9%의 외부 연결을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-184">That means we guarantee that a Storm cluster has external connectivity at least 99.9 percent of the time.</span></span>

<span data-ttu-id="defe8-185">자세한 내용은 [Azure 지원](https://azure.microsoft.com/support/options/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="defe8-185">For more information, see [Azure support](https://azure.microsoft.com/support/options/).</span></span>

## <a name="apache-storm-use-cases"></a><span data-ttu-id="defe8-186">Apache Storm 사용 사례</span><span class="sxs-lookup"><span data-stu-id="defe8-186">Apache Storm use cases</span></span>

<span data-ttu-id="defe8-187">다음은 HDInsight의 Storm을 사용할 수 있는 몇 가지 일반적인 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-187">The following are some common scenarios for which you might use Storm on HDInsight:</span></span>

* <span data-ttu-id="defe8-188">IoT(사물 인터넷)</span><span class="sxs-lookup"><span data-stu-id="defe8-188">Internet of Things (IoT)</span></span>
* <span data-ttu-id="defe8-189">부정 행위 감지</span><span class="sxs-lookup"><span data-stu-id="defe8-189">Fraud detection</span></span>
* <span data-ttu-id="defe8-190">소셜 분석</span><span class="sxs-lookup"><span data-stu-id="defe8-190">Social analytics</span></span>
* <span data-ttu-id="defe8-191">추출, 변환 및 로드(ETL)</span><span class="sxs-lookup"><span data-stu-id="defe8-191">Extraction, transformation, and loading (ETL)</span></span>
* <span data-ttu-id="defe8-192">네트워크 모니터링</span><span class="sxs-lookup"><span data-stu-id="defe8-192">Network monitoring</span></span>
* <span data-ttu-id="defe8-193">검색</span><span class="sxs-lookup"><span data-stu-id="defe8-193">Search</span></span>
* <span data-ttu-id="defe8-194">모바일 고객 관리</span><span class="sxs-lookup"><span data-stu-id="defe8-194">Mobile engagement</span></span>

<span data-ttu-id="defe8-195">실제 시나리오에 대한 자세한 내용은 [기업에서 Storm을 사용하는 방식](https://storm.apache.org/documentation/Powered-By.html) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="defe8-195">For information about real-world scenarios, see the [How companies are using Storm](https://storm.apache.org/documentation/Powered-By.html) document.</span></span>

## <a name="development"></a><span data-ttu-id="defe8-196">개발</span><span class="sxs-lookup"><span data-stu-id="defe8-196">Development</span></span>

<span data-ttu-id="defe8-197">Data Lake Tools for Visual Studio를 사용하면 .NET 개발자는 C#으로 토폴로지를 디자인하고 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-197">.NET developers can design and implement topologies in C# by using Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="defe8-198">또한 Java 및 C# 구성 요소를 사용하는 하이브리드 토폴로지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-198">You can also create hybrid topologies that use Java and C# components.</span></span>

<span data-ttu-id="defe8-199">자세한 내용은 [Visual Studio를 사용하여 HDInsight에서 Storm에 대한 C# 토폴로지 개발](hdinsight-storm-develop-csharp-visual-studio-topology.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="defe8-199">For more information, see [Develop C# topologies for Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="defe8-200">선택한 IDE를 사용하여 Java 솔루션을 개발할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-200">You can also develop Java solutions by using the IDE of your choice.</span></span> <span data-ttu-id="defe8-201">자세한 내용은 [HDInsight의 Storm에 대한 Java 토폴로지 개발](hdinsight-storm-develop-java-topology.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="defe8-201">For more information, see [Develop Java topologies for Storm on HDInsight](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="defe8-202">Python은 Storm 구성 요소를 개발하는 데에도 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-202">Python can also be used to develop Storm components.</span></span> <span data-ttu-id="defe8-203">자세한 내용은 [HDInsight에서 Python을 사용하여 Storm 토폴로지 개발](hdinsight-storm-develop-python-topology.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="defe8-203">For more information, see [Develop Storm topologies using Python on HDInsight](hdinsight-storm-develop-python-topology.md).</span></span>

## <a name="common-development-patterns"></a><span data-ttu-id="defe8-204">일반적인 개발 패턴</span><span class="sxs-lookup"><span data-stu-id="defe8-204">Common development patterns</span></span>

### <a name="guaranteed-message-processing"></a><span data-ttu-id="defe8-205">메시지 처리 보장</span><span class="sxs-lookup"><span data-stu-id="defe8-205">Guaranteed message processing</span></span>

<span data-ttu-id="defe8-206">Apache Storm은 다양한 수준의 보장된 메시지 처리를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-206">Apache Storm can provide different levels of guaranteed message processing.</span></span> <span data-ttu-id="defe8-207">예를 들어 기본적인 Storm 응용 프로그램은 최소한 한 번 처리를 보장할 수 있고 Trident는 정확히 한 번 처리를 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-207">For example, a basic Storm application can guarantee at-least-once processing, and Trident can guarantee exactly once processing.</span></span>

<span data-ttu-id="defe8-208">자세한 내용은 apache.org에서 [데이터 처리 보장](https://storm.apache.org/about/guarantees-data-processing.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="defe8-208">For more information, see [Guarantees on data processing](https://storm.apache.org/about/guarantees-data-processing.html) at apache.org.</span></span>

### <a name="ibasicbolt"></a><span data-ttu-id="defe8-209">IBasicBolt</span><span class="sxs-lookup"><span data-stu-id="defe8-209">IBasicBolt</span></span>

<span data-ttu-id="defe8-210">입력 튜플을 읽고 튜플을 내보내지 않거나 하나 이상 내보낸 다음 실행 메서드 끝에서 입력 튜플을 즉시 승인하는 패턴은 매우 흔히 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-210">The pattern of reading an input tuple, emitting zero or more tuples, and then acking the input tuple immediately at the end of the execute method is common.</span></span> <span data-ttu-id="defe8-211">Storm은 이 패턴을 자동화하는 [IBasicBolt](https://storm.apache.org/releases/1.0.3/javadocs/org/apache/storm/topology/IBasicBolt.html) 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-211">Storm provides the [IBasicBolt](https://storm.apache.org/releases/1.0.3/javadocs/org/apache/storm/topology/IBasicBolt.html) interface to automate this pattern.</span></span>

### <a name="joins"></a><span data-ttu-id="defe8-212">조인</span><span class="sxs-lookup"><span data-stu-id="defe8-212">Joins</span></span>

<span data-ttu-id="defe8-213">데이터 스트림이 조인되는 방식은 응용 프로그램마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-213">How data streams are joined varies between applications.</span></span> <span data-ttu-id="defe8-214">예를 들어 여러 스트림의 각 튜플을 새 스트림 하나에 조인할 수도 있고 특정 창에 대한 튜플 배치만 조인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-214">For example, you can join each tuple from multiple streams into one new stream, or you can join only batches of tuples for a specific window.</span></span> <span data-ttu-id="defe8-215">어떤 방법을 사용하든 [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-)을 통해 조인을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-215">Either way, joining can be accomplished by using [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-).</span></span> <span data-ttu-id="defe8-216">필드 그룹화는 튜플을 Bolt로 라우팅하는 방식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-216">Field grouping is a way of defining how tuples are routed to bolts.</span></span>

<span data-ttu-id="defe8-217">다음 Java 예제에서는 fieldsGrouping을 사용하여 구성 요소 "1", "2", "3"에서 생성된 튜플을 MyJoiner Bolt로 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-217">In the following Java example, fieldsGrouping is used to route tuples that originate from components "1", "2", and "3" to the MyJoiner bolt:</span></span>

    builder.setBolt("join", new MyJoiner(), parallelism) .fieldsGrouping("1", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("2", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("3", new Fields("joinfield1", "joinfield2"));

### <a name="batches"></a><span data-ttu-id="defe8-218">일괄 처리</span><span class="sxs-lookup"><span data-stu-id="defe8-218">Batches</span></span>

<span data-ttu-id="defe8-219">Apache Storm은 "틱 튜플(tick tuple)"이라고 하는 내부 타이밍 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-219">Apache Storm provides an internal timing mechanism known as a "tick tuple."</span></span> <span data-ttu-id="defe8-220">토폴로지에서 틱 튜플을 내보내는 빈도를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-220">You can set how often a tick tuple is emitted in your topology.</span></span>

<span data-ttu-id="defe8-221">C# 구성 요소에서 틱 튜플을 사용하는 예제는 [PartialBoltCount.cs](https://github.com/hdinsight/hdinsight-storm-examples/blob/3b2c960549cac122e8874931df4801f0934fffa7/EventCountExample/EventCountTopology/src/main/java/com/microsoft/hdinsight/storm/examples/PartialCountBolt.java)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="defe8-221">For an example of using a tick tuple from a C# component, see [PartialBoltCount.cs](https://github.com/hdinsight/hdinsight-storm-examples/blob/3b2c960549cac122e8874931df4801f0934fffa7/EventCountExample/EventCountTopology/src/main/java/com/microsoft/hdinsight/storm/examples/PartialCountBolt.java).</span></span>

### <a name="caches"></a><span data-ttu-id="defe8-222">캐시</span><span class="sxs-lookup"><span data-stu-id="defe8-222">Caches</span></span>

<span data-ttu-id="defe8-223">메모리 내 캐싱은 자주 사용되는 자산을 메모리에 저장하므로 처리 속도를 높이기 위한 메커니즘으로 사용되는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-223">In-memory caching is often used as a mechanism for speeding up processing because it keeps frequently used assets in memory.</span></span> <span data-ttu-id="defe8-224">토폴로지는 여러 노드 및 각 노드 내의 여러 프로세스로 분산되므로 [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-)을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-224">Because a topology is distributed across multiple nodes, and multiple processes within each node, you should consider using [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-).</span></span> <span data-ttu-id="defe8-225">`fieldsGrouping`을 사용하여 캐시 조회에 사용되는 필드가 포함된 튜플은 항상 같은 프로세스로 라우팅될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-225">Use `fieldsGrouping` to ensure that tuples containing the fields that are used for cache lookup are always routed to the same process.</span></span> <span data-ttu-id="defe8-226">이 그룹화 기능으로 프로세스 간 캐시 항목 중복을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-226">This grouping functionality avoids duplication of cache entries across processes.</span></span>

### <a name="stream-top-n"></a><span data-ttu-id="defe8-227">스트림 “상위 N”</span><span class="sxs-lookup"><span data-stu-id="defe8-227">Stream "top N"</span></span>

<span data-ttu-id="defe8-228">토폴로지가 상위 N 값 계산에 따라 다른 경우 상위 N 값을 병렬로 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-228">When your topology depends on calculating a top N value, calculate the top N value in parallel.</span></span> <span data-ttu-id="defe8-229">그런 다음 해당 계산의 출력을 전역 값으로 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-229">Then merge the output from those calculations into a global value.</span></span> <span data-ttu-id="defe8-230">이 작업은 병렬 처리를 위해 필드별로 라우팅하도록 [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-)을 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-230">This operation can be done by using [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-) to route by field for parallel processing.</span></span> <span data-ttu-id="defe8-231">그런 다음 상위 N 값을 전역적으로 결정하는 Bolt로 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-231">Then you can route to a bolt that globally determines the top N value.</span></span>

<span data-ttu-id="defe8-232">상위 N 값을 계산하는 예제는 [RollingTopWords](https://github.com/apache/storm/blob/master/examples/storm-starter/src/jvm/org/apache/storm/starter/RollingTopWords.java) 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="defe8-232">For an example of calculating a top N value, see the [RollingTopWords](https://github.com/apache/storm/blob/master/examples/storm-starter/src/jvm/org/apache/storm/starter/RollingTopWords.java) example.</span></span>

## <a name="logging"></a><span data-ttu-id="defe8-233">로깅</span><span class="sxs-lookup"><span data-stu-id="defe8-233">Logging</span></span>

<span data-ttu-id="defe8-234">Storm은 Apache Log4j를 사용하여 정보를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-234">Storm uses Apache Log4j to log information.</span></span> <span data-ttu-id="defe8-235">기본적으로 많은 양의 데이터를 기록하면 정보를 정렬하기가 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-235">By default, a large amount of data is logged, and it can be difficult to sort through the information.</span></span> <span data-ttu-id="defe8-236">Storm 토폴로지의 일부로 로깅 구성 파일을 포함하여 로깅 동작을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-236">You can include a logging configuration file as part of your Storm topology to control logging behavior.</span></span>

<span data-ttu-id="defe8-237">로깅을 구성하는 방법을 보여 주는 예제 토폴로지는 HDInsight에서 Storm에 대한 [Java 기반 WordCount](hdinsight-storm-develop-java-topology.md) 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="defe8-237">For an example topology that demonstrates how to configure logging, see [Java-based WordCount](hdinsight-storm-develop-java-topology.md) example for Storm on HDInsight.</span></span>

## <a name="next-steps"></a><span data-ttu-id="defe8-238">다음 단계</span><span class="sxs-lookup"><span data-stu-id="defe8-238">Next steps</span></span>

<span data-ttu-id="defe8-239">HDInsight의 Storm을 사용한 실시간 분석 솔루션에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="defe8-239">Learn more about real-time analytics solutions with Storm on HDInsight:</span></span>

* <span data-ttu-id="defe8-240">[HDInsight의 Apache Storm 시작][gettingstarted]</span><span class="sxs-lookup"><span data-stu-id="defe8-240">[Get started with Apache Storm on HDInsight][gettingstarted]</span></span>
* [<span data-ttu-id="defe8-241">HDInsight의 Apache Storm에 대한 예제 토폴로지</span><span class="sxs-lookup"><span data-stu-id="defe8-241">Example topologies for Apache Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

[stormtrident]: https://storm.apache.org/documentation/Trident-API-Overview.html
[samoa]: http://yahooeng.tumblr.com/post/65453012905/introducing-samoa-an-open-source-platform-for-mining
[apachetutorial]: https://storm.apache.org/documentation/Tutorial.html
[gettingstarted]: hdinsight-apache-storm-tutorial-get-started-linux.md
