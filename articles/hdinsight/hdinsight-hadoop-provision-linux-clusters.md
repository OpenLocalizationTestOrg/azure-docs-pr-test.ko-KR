---
title: "Hadoop, Spark, Kafka, HBase, 또는 R 서버-Azure HDInsight에 대 한 aaaCluster 설치 | Microsoft Docs"
description: "브라우저, hello Azure CLI, Azure PowerShell, REST, 또는 SDK에서 HDInsight Hadoop, Kafka, Spark, HBase, R 서버 또는 Storm 클러스터를 설정 합니다."
keywords: "hadoop 클러스터 설정, kafka 클러스터 설정, spark 클러스터 설정, hadoop에서 클러스터란"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 23a01938-3fe5-4e2e-8e8b-3368e1bbe2ca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/06/2017
ms.author: jgao
ms.openlocfilehash: 80ec59d8a39f7fccb940503fd2dc3ae5afee6bcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-clusters-in-hdinsight-with-hadoop-spark-kafka-and-more"></a><span data-ttu-id="410d3-104">Hadoop, Spark, Kafka 등으로 HDInsight에서 클러스터를 설정</span><span class="sxs-lookup"><span data-stu-id="410d3-104">Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="410d3-105">자세한 방법을 tooset 및 HDInsight Hadoop, Spark, Kafka, 대화형 하이브, HBase, R 서버 또는 Storm의에서 클러스터를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-105">Learn how tooset up and configure clusters in HDInsight with Hadoop, Spark, Kafka, Interactive Hive, HBase, R Server, or Storm.</span></span> <span data-ttu-id="410d3-106">또한 toocustomize 클러스터 방법을 알아보고 tooa 도메인을 조인 하 여 보안을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-106">Also, learn how toocustomize clusters and add security by joining them tooa domain.</span></span>

<span data-ttu-id="410d3-107">Hadoop 클러스터는 작업의 분산 처리에 사용되는 여러 가상 컴퓨터(노드)로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-107">A Hadoop cluster consists of several virtual machines (nodes) that are used for distributed processing of tasks.</span></span> <span data-ttu-id="410d3-108">Azure HDInsight 되므로 tooprovide 일반 구성 정보를 하나만 설치의 구현 세부 정보 및 구성의 개별 노드를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-108">Azure HDInsight handles implementation details of installation and configuration of individual nodes, so you only have tooprovide general configuration information.</span></span> 

> [!IMPORTANT]
><span data-ttu-id="410d3-109">HDInsight 클러스터 결제 클러스터 만들어지고 hello 클러스터를 삭제할 때 중지 되 면 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-109">HDInsight cluster billing starts once a cluster is created and stops when hello cluster is deleted.</span></span> <span data-ttu-id="410d3-110">분 단위로 청구되므로 더 이상 사용하지 않으면 항상 클러스터를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-110">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span> <span data-ttu-id="410d3-111">너무 방법에 대해 알아봅니다[클러스터를 삭제 합니다.](hdinsight-delete-cluster.md)</span><span class="sxs-lookup"><span data-stu-id="410d3-111">Learn how too[delete a cluster.](hdinsight-delete-cluster.md)</span></span>
>

## <a name="cluster-setup-methods"></a><span data-ttu-id="410d3-112">클러스터 설정 방법</span><span class="sxs-lookup"><span data-stu-id="410d3-112">Cluster setup methods</span></span>
<span data-ttu-id="410d3-113">hello 다음 표에 다양 한 방법을 hello tooset HDInsight 클러스터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-113">hello following table shows hello different methods you can use tooset up an HDInsight cluster.</span></span>

| <span data-ttu-id="410d3-114">다음을 사용하여 만든 클러스터</span><span class="sxs-lookup"><span data-stu-id="410d3-114">Clusters created with</span></span> | <span data-ttu-id="410d3-115">웹 브라우저 사용</span><span class="sxs-lookup"><span data-stu-id="410d3-115">Web browser</span></span> | <span data-ttu-id="410d3-116">명령 줄</span><span class="sxs-lookup"><span data-stu-id="410d3-116">Command line</span></span> | <span data-ttu-id="410d3-117">REST API</span><span class="sxs-lookup"><span data-stu-id="410d3-117">REST API</span></span> | <span data-ttu-id="410d3-118">SDK)</span><span class="sxs-lookup"><span data-stu-id="410d3-118">SDK</span></span> | 
| --- |:---:|:---:|:---:|:---:|
| [<span data-ttu-id="410d3-119">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="410d3-119">Azure portal</span></span>](hdinsight-hadoop-create-linux-clusters-portal.md) |<span data-ttu-id="410d3-120">✔</span><span class="sxs-lookup"><span data-stu-id="410d3-120">✔</span></span> |&nbsp; |&nbsp; |&nbsp; |
| [<span data-ttu-id="410d3-121">Azure 데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="410d3-121">Azure Data Factory</span></span>](hdinsight-hadoop-create-linux-clusters-adf.md) |<span data-ttu-id="410d3-122">✔</span><span class="sxs-lookup"><span data-stu-id="410d3-122">✔</span></span> |<span data-ttu-id="410d3-123">✔</span><span class="sxs-lookup"><span data-stu-id="410d3-123">✔</span></span> |<span data-ttu-id="410d3-124">✔</span><span class="sxs-lookup"><span data-stu-id="410d3-124">✔</span></span> |<span data-ttu-id="410d3-125">✔</span><span class="sxs-lookup"><span data-stu-id="410d3-125">✔</span></span> |
| [<span data-ttu-id="410d3-126">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="410d3-126">Azure CLI</span></span>](hdinsight-hadoop-create-linux-clusters-azure-cli.md) |&nbsp; |<span data-ttu-id="410d3-127">✔</span><span class="sxs-lookup"><span data-stu-id="410d3-127">✔</span></span> |&nbsp; |&nbsp; |
| [<span data-ttu-id="410d3-128">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="410d3-128">Azure PowerShell</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md) |&nbsp; |<span data-ttu-id="410d3-129">✔</span><span class="sxs-lookup"><span data-stu-id="410d3-129">✔</span></span> |&nbsp; |&nbsp; |
| [<span data-ttu-id="410d3-130">cURL</span><span class="sxs-lookup"><span data-stu-id="410d3-130">cURL</span></span>](hdinsight-hadoop-create-linux-clusters-curl-rest.md) |&nbsp; |<span data-ttu-id="410d3-131">✔</span><span class="sxs-lookup"><span data-stu-id="410d3-131">✔</span></span> |<span data-ttu-id="410d3-132">✔</span><span class="sxs-lookup"><span data-stu-id="410d3-132">✔</span></span> |&nbsp; |
| [<span data-ttu-id="410d3-133">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="410d3-133">.NET SDK</span></span>](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md) |&nbsp; |&nbsp; |&nbsp; |<span data-ttu-id="410d3-134">✔</span><span class="sxs-lookup"><span data-stu-id="410d3-134">✔</span></span> |
| [<span data-ttu-id="410d3-135">Azure 리소스 관리자 템플릿</span><span class="sxs-lookup"><span data-stu-id="410d3-135">Azure Resource Manager templates</span></span>](hdinsight-hadoop-create-linux-clusters-arm-templates.md) |&nbsp; |<span data-ttu-id="410d3-136">✔</span><span class="sxs-lookup"><span data-stu-id="410d3-136">✔</span></span> |&nbsp; |&nbsp; |

## <a name="quick-create-basic-cluster-setup"></a><span data-ttu-id="410d3-137">빨리 만들기: 기본 클러스터 설정</span><span class="sxs-lookup"><span data-stu-id="410d3-137">Quick create: Basic cluster setup</span></span>
<span data-ttu-id="410d3-138">이 문서에서는 hello에 대 한 설치 프로그램을 통해 [Azure 포털](https://portal.azure.com)사용 하 여 HDInsight 클러스터를 만들 수 있습니다, *빨리 만들기* 또는 *사용자 지정*합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-138">This article walks you through setup in hello [Azure portal](https://portal.azure.com), where you can create an HDInsight cluster using *Quick create* or *Custom*.</span></span> 

<span data-ttu-id="410d3-139">Hello 화면 toodo 기본 클러스터 설치 프로그램에 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-139">Follow instructions on hello screen toodo a basic cluster setup.</span></span> <span data-ttu-id="410d3-140">다음 사항에 대한 세부 정보가 아래에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-140">Details are provided below for:</span></span>

* [<span data-ttu-id="410d3-141">리소스 그룹 이름</span><span class="sxs-lookup"><span data-stu-id="410d3-141">Resource group name</span></span>](#resource-group-name)
* [<span data-ttu-id="410d3-142">클러스터 유형 및 구성</span><span class="sxs-lookup"><span data-stu-id="410d3-142">Cluster types and configuration</span></span>](#cluster-types) 
* [<span data-ttu-id="410d3-143">클러스터 로그인 및 SSH 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="410d3-143">Cluster login and SSH username</span></span>](#cluster-login-and-ssh-username)
* [<span data-ttu-id="410d3-144">위치</span><span class="sxs-lookup"><span data-stu-id="410d3-144">Location</span></span>](#location)

> [!IMPORTANT]
> <span data-ttu-id="410d3-145">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-145">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="410d3-146">자세한 내용은 [HDInsight 3.3 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="410d3-146">For more information, see [HDInsight 3.3 retirement](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>

## <a name="resource-group-name"></a><span data-ttu-id="410d3-147">리소스 그룹 이름</span><span class="sxs-lookup"><span data-stu-id="410d3-147">Resource group name</span></span> 

<span data-ttu-id="410d3-148">[Azure 리소스 관리자](../azure-resource-manager/resource-group-overview.md) 작업할 hello 리소스 그룹, 참조 tooas로 응용 프로그램에 Azure 리소스 그룹은 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-148">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) helps you work with hello resources in your application as a group, referred tooas an Azure resource group.</span></span> <span data-ttu-id="410d3-149">배포 업데이트 하거나 모니터링 조정 된 단일 작업에서 응용 프로그램에 대 한 모든 hello 리소스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-149">You can deploy, update, monitor, or delete all hello resources for your application in a single coordinated operation.</span></span>

## <span data-ttu-id="410d3-150"><a name="cluster-types"></a> 클러스터 유형 및 구성</span><span class="sxs-lookup"><span data-stu-id="410d3-150"><a name="cluster-types"></a> Cluster types and configuration</span></span>
<span data-ttu-id="410d3-151">Azure HDInsight는 현재 hello 다음 클러스터 종류의 구성 요소 tooprovide 집합을 가진 특정 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-151">Azure HDInsight currently provides hello following cluster types, each with a set of components tooprovide certain functionalities.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="410d3-152">HDInsight 클러스터는 각 단일 워크로드 또는 기술에 다양한 유형으로 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-152">HDInsight clusters are available in various types, each for a single workload or technology.</span></span> <span data-ttu-id="410d3-153">Storm 및 한 개의 클러스터에서 HBase 같은 여러 형식을 결합 하는 클러스터는 지원 되는 방법은 toocreate 없습니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-153">There is no supported method toocreate a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span> <span data-ttu-id="410d3-154">솔루션에 여러 HDInsight 클러스터 형식 간에 분산 되어 있는 기술 요구 하는 경우는 [Azure 가상 네트워크](https://docs.microsoft.com/azure/virtual-network) hello 필요한 클러스터 종류를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-154">If your solution requires technologies that are spread across multiple HDInsight cluster types, an [Azure virtual network](https://docs.microsoft.com/azure/virtual-network) can connect hello required cluster types.</span></span> 
>
>

| <span data-ttu-id="410d3-155">클러스터 유형</span><span class="sxs-lookup"><span data-stu-id="410d3-155">Cluster type</span></span> | <span data-ttu-id="410d3-156">기능</span><span class="sxs-lookup"><span data-stu-id="410d3-156">Functionality</span></span> |
| --- | --- |
| [<span data-ttu-id="410d3-157">Hadoop</span><span class="sxs-lookup"><span data-stu-id="410d3-157">Hadoop</span></span>](hdinsight-hadoop-introduction.md) |<span data-ttu-id="410d3-158">저장된 데이터의 일괄 처리 쿼리 및 분석</span><span class="sxs-lookup"><span data-stu-id="410d3-158">Batch query and analysis of stored data</span></span> |
| [<span data-ttu-id="410d3-159">HBase</span><span class="sxs-lookup"><span data-stu-id="410d3-159">HBase</span></span>](hdinsight-hbase-overview.md) |<span data-ttu-id="410d3-160">많은 양의 스키마 없는 NoSQL 데이터에 대한 처리</span><span class="sxs-lookup"><span data-stu-id="410d3-160">Processing for large amounts of schemaless, NoSQL data</span></span> |
| [<span data-ttu-id="410d3-161">Storm</span><span class="sxs-lookup"><span data-stu-id="410d3-161">Storm</span></span>](hdinsight-storm-overview.md) |<span data-ttu-id="410d3-162">실시간 이벤트 처리</span><span class="sxs-lookup"><span data-stu-id="410d3-162">Real-time event processing</span></span> |
| [<span data-ttu-id="410d3-163">Spark</span><span class="sxs-lookup"><span data-stu-id="410d3-163">Spark</span></span>](hdinsight-apache-spark-overview.md) |<span data-ttu-id="410d3-164">메모리 내 처리, 대화형 쿼리, 마이크로 배치 스트림 처리</span><span class="sxs-lookup"><span data-stu-id="410d3-164">In-memory processing, interactive queries, micro-batch stream processing</span></span> |
| [<span data-ttu-id="410d3-165">Kafka (미리 보기)</span><span class="sxs-lookup"><span data-stu-id="410d3-165">Kafka (Preview)</span></span>](hdinsight-apache-kafka-introduction.md) | <span data-ttu-id="410d3-166">사용 되는 toobuild 실시간 스트리밍 데이터 파이프라인 및 응용 프로그램 일 수 있는 분산된 스트리밍 플랫폼</span><span class="sxs-lookup"><span data-stu-id="410d3-166">A distributed streaming platform that can be used toobuild real-time streaming data pipelines and applications</span></span> |
| [<span data-ttu-id="410d3-167">R Server</span><span class="sxs-lookup"><span data-stu-id="410d3-167">R Server</span></span>](hdinsight-hadoop-r-server-overview.md) |<span data-ttu-id="410d3-168">다양한 빅 데이터 통계, 예측 모델링 및 기계 학습 기능</span><span class="sxs-lookup"><span data-stu-id="410d3-168">Various big data statistics, predictive modeling, and machine learning capabilities</span></span> |
| [<span data-ttu-id="410d3-169">대화형 Hive(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="410d3-169">Interactive Hive (Preview)</span></span>](hdinsight-hadoop-use-interactive-hive.md) |<span data-ttu-id="410d3-170">대화형 및 더 빠른 Hive 쿼리에 대한 메모리 내 캐싱</span><span class="sxs-lookup"><span data-stu-id="410d3-170">In-memory caching for interactive and faster Hive queries</span></span> |

### <a name="number-of-nodes-for-each-cluster-type"></a><span data-ttu-id="410d3-171">각 클러스터 유형에 대한 노드 수</span><span class="sxs-lookup"><span data-stu-id="410d3-171">Number of nodes for each cluster type</span></span>
<span data-ttu-id="410d3-172">각 클러스터 유형에는 자체 노드 수, 노드에 대한 용어 및 기본 VM 크기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-172">Each cluster type has its own number of nodes, terminology for nodes, and default VM size.</span></span> <span data-ttu-id="410d3-173">다음 표에서 hello, 각 노드 형식에 대 한 노드 수 hello 괄호 안의 항목은 합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-173">In hello following table, hello number of nodes for each node type is in parentheses.</span></span>

| <span data-ttu-id="410d3-174">형식</span><span class="sxs-lookup"><span data-stu-id="410d3-174">Type</span></span> | <span data-ttu-id="410d3-175">노드</span><span class="sxs-lookup"><span data-stu-id="410d3-175">Nodes</span></span> | <span data-ttu-id="410d3-176">다이어그램</span><span class="sxs-lookup"><span data-stu-id="410d3-176">Diagram</span></span> |
| --- | --- | --- |
| <span data-ttu-id="410d3-177">Hadoop은</span><span class="sxs-lookup"><span data-stu-id="410d3-177">Hadoop</span></span> |<span data-ttu-id="410d3-178">헤드 노드(2), 데이터 노드(1+)</span><span class="sxs-lookup"><span data-stu-id="410d3-178">Head node (2), data node (1+)</span></span> |![HDInsight Hadoop 클러스터 노드](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hadoop-cluster-type-nodes.png) |
| <span data-ttu-id="410d3-180">HBase</span><span class="sxs-lookup"><span data-stu-id="410d3-180">HBase</span></span> |<span data-ttu-id="410d3-181">헤드 서버(2), 지역 서버(1+), 마스터/ZooKeeper 노드(3)</span><span class="sxs-lookup"><span data-stu-id="410d3-181">Head server (2), region server (1+), master/ZooKeeper node (3)</span></span> |![HDInsight HBase 클러스터 노드](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hbase-cluster-type-setup.png) |
| <span data-ttu-id="410d3-183">Storm</span><span class="sxs-lookup"><span data-stu-id="410d3-183">Storm</span></span> |<span data-ttu-id="410d3-184">Nimbus 노드(2), 감독자 서버(1+), ZooKeeper 노드(3)</span><span class="sxs-lookup"><span data-stu-id="410d3-184">Nimbus node (2), supervisor server (1+), ZooKeeper node (3)</span></span> |![HDInsight Storm 클러스터 노드](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-storm-cluster-type-setup.png) |
| <span data-ttu-id="410d3-186">Spark</span><span class="sxs-lookup"><span data-stu-id="410d3-186">Spark</span></span> |<span data-ttu-id="410d3-187">헤드 노드(2), 작업자 노드(1+), ZooKeeper 노드(3)(A1 ZooKeeper VM 크기의 경우 무료)</span><span class="sxs-lookup"><span data-stu-id="410d3-187">Head node (2), worker node (1+), ZooKeeper node (3) (free for A1 ZooKeeper VM size)</span></span> |![HDInsight Spark 클러스터 노드](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-spark-cluster-type-setup.png) |

<span data-ttu-id="410d3-189">자세한 내용은 참조 [기본 클러스터 노드 구성 및 가상 컴퓨터 크기](hdinsight-component-versioning.md#default-node-configuration-and-virtual-machine-sizes-for-clusters) 에 "hello Hadoop 구성 요소 및 HDInsight의 버전이 무엇 인가요?"</span><span class="sxs-lookup"><span data-stu-id="410d3-189">For more information, see [Default node configuration and virtual machine sizes for clusters](hdinsight-component-versioning.md#default-node-configuration-and-virtual-machine-sizes-for-clusters) in "What are hello Hadoop components and versions in HDInsight?"</span></span>

### <a name="hdinsight-version"></a><span data-ttu-id="410d3-190">HDInsight 버전</span><span class="sxs-lookup"><span data-stu-id="410d3-190">HDInsight version</span></span>
<span data-ttu-id="410d3-191">이 클러스터에 대 한 HDInsight hello 버전을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-191">Choose hello version of HDInsight for this cluster.</span></span> <span data-ttu-id="410d3-192">자세한 내용은 [지원되는 HDInsight 버전](hdinsight-component-versioning.md#supported-hdinsight-versions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="410d3-192">For more information, see [Supported HDInsight versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>

### <span data-ttu-id="410d3-193"><a name="cluster-tiers"></a>클러스터 계층: HDInsight 서비스 계층</span><span class="sxs-lookup"><span data-stu-id="410d3-193"><a name="cluster-tiers"></a>Cluster tier: HDInsight service tiers</span></span>

<span data-ttu-id="410d3-194">Azure HDInsight hello 빅 데이터 클라우드 서비스의 두 가지 서비스 계층을 제공: Standard 및 Premium입니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-194">Azure HDInsight provides hello big data cloud offerings in two service tiers: Standard and Premium.</span></span>  <span data-ttu-id="410d3-195">자세한 내용은 [HDInsight Standard 및 HDInsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="410d3-195">For more information, see [HDInsight Standard and HDInsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium).</span></span>

<span data-ttu-id="410d3-196">hello 다음 스크린샷은 hello 클러스터 종류를 선택 하기 위한 Azure 포털 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-196">hello following screenshot shows hello Azure portal information for choosing cluster types.</span></span>

![HDInsight 프리미엄 구성](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-type-configuration.png)


## <a name="cluster-login-and-ssh-user-name"></a><span data-ttu-id="410d3-198">클러스터 로그인 및 SSH 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="410d3-198">Cluster login and SSH user name</span></span>
<span data-ttu-id="410d3-199">HDInsight 클러스터를 사용하면 클러스터 생성 중에 다음과 같은 두 개의 사용자 계정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-199">With HDInsight clusters, you can configure two user accounts during cluster creation:</span></span>

* <span data-ttu-id="410d3-200">HTTP 사용자: hello 기본 사용자 이름인 *admin*합니다. Hello Azure 포털에서 기본 구성을 hello를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-200">HTTP user: hello default user name is *admin*. It uses hello basic configuration on hello Azure portal.</span></span> <span data-ttu-id="410d3-201">경우에 따라 "클러스터 사용자"라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-201">Sometimes it is called "Cluster user."</span></span>
* <span data-ttu-id="410d3-202">SSH 사용자 (Linux 클러스터): SSH 통해 사용 되는 tooconnect toohello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-202">SSH user (Linux clusters): Used tooconnect toohello cluster through SSH.</span></span> <span data-ttu-id="410d3-203">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="410d3-203">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="410d3-204"><a name="location"></a>클러스터 및 저장소 위치(영역)</span><span class="sxs-lookup"><span data-stu-id="410d3-204"><a name="location"></a>Location (regions) for clusters and storage</span></span>

<span data-ttu-id="410d3-205">Toospecify hello 클러스터 위치를 명시적으로 필요 하지 않습니다: hello 클러스터가 hello에 있고 동일한 hello 기본 저장소 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-205">You don't need toospecify hello cluster location explicitly: hello cluster is in hello same location as hello default storage.</span></span> <span data-ttu-id="410d3-206">지원 되는 지역 목록은 hello 클릭 **지역** 드롭 다운 목록에서 [HDInsight 가격](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409)합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-206">For a list of supported regions, click hello **Region** drop-down list on [HDInsight pricing](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409).</span></span>

## <a name="storage-endpoints-for-clusters"></a><span data-ttu-id="410d3-207">클러스터에 대한 저장소 끝점</span><span class="sxs-lookup"><span data-stu-id="410d3-207">Storage endpoints for clusters</span></span>

<span data-ttu-id="410d3-208">Hadoop의 온-프레미스 설치에서는 hello 클러스터에서 저장소를 Hadoop 분산 파일 시스템 (HDFS) hello 하지만 hello에서 클라우드 저장소 끝점을 사용 하 여 toocluster을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-208">Although an on-premises installation of Hadoop uses hello Hadoop Distributed File System (HDFS) for storage on hello cluster, in hello cloud you use storage endpoints connected toocluster.</span></span> <span data-ttu-id="410d3-209">HDInsight 클러스터는 [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) 또는 [Azure Storage의 Blob](hdinsight-hadoop-use-blob-storage.md)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-209">HDInsight clusters use either [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) or [blobs in Azure Storage](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="410d3-210">Azure 저장소 서비스 또는 데이터 레이크 저장소를 사용 하 여 데이터를 유지 하면서 계산을 위해 사용 하는 hello HDInsight 클러스터를 삭제 해도 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-210">Using Azure Storage or Data Lake Store means you can safely delete hello HDInsight clusters used for computation while still retaining your data.</span></span> 

> [!WARNING]
> <span data-ttu-id="410d3-211">추가 저장소 계정을 사용 하 여 hello HDInsight 클러스터에서 다른 위치에 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-211">Using an additional storage account in a different location from hello HDInsight cluster is not supported.</span></span>

<span data-ttu-id="410d3-212">구성 하는 동안 hello 기본 저장소 끝점을 지정할 수는 Azure 저장소 계정 또는 데이터 레이크 저장소의 blob 컨테이너 있습니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-212">During configuration, for hello default storage endpoint you specify a blob container of an Azure Storage account or a Data Lake Store.</span></span> <span data-ttu-id="410d3-213">hello 기본 저장소에 응용 프로그램 및 시스템 로그 합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-213">hello default storage contains application and system logs.</span></span> <span data-ttu-id="410d3-214">필요에 따라 추가 연결 된 Azure 저장소 계정과 클러스터 hello Data Lake 저장소 계정에 액세스할 수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-214">Optionally, you can specify additional linked Azure Storage accounts and Data Lake Store accounts that hello cluster can access.</span></span> <span data-ttu-id="410d3-215">hello HDInsight 클러스터와 hello 종속 저장소 계정에 있어야 합니다. hello 동일한 Azure 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-215">hello HDInsight cluster and hello dependent storage accounts must be in hello same Azure location.</span></span>

![클러스터 저장소 설정: HDFS 호환 저장소 끝점](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-creation-storage.png)

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


### <a name="optional-metastores"></a><span data-ttu-id="410d3-217">선택적 Metastore</span><span class="sxs-lookup"><span data-stu-id="410d3-217">Optional metastores</span></span>
<span data-ttu-id="410d3-218">선택적 하이브 또는 Oozie Metastore를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-218">You can create optional Hive or Oozie metastores.</span></span> <span data-ttu-id="410d3-219">그러나 일부 클러스터 형식은 Metastore를 지원하지 않으며, Azure SQL Data Warehouse는 Metastore와 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-219">However, not all cluster types support metastores, and Azure SQL Data Warehouse isn't compatible with metastores.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="410d3-220">사용자 지정 metastore를 만들 때에 대시, 하이픈 또는 hello 데이터베이스 이름에 공백이 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="410d3-220">When you create a custom metastore, don't use dashes, hyphens, or spaces in hello database name.</span></span> <span data-ttu-id="410d3-221">이 인해 hello 클러스터 만들기 프로세스 toofail 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-221">This can cause hello cluster creation process toofail.</span></span>

### <span data-ttu-id="410d3-222"><a name="use-hiveoozie-metastore"></a>Hive metastore</span><span class="sxs-lookup"><span data-stu-id="410d3-222"><a name="use-hiveoozie-metastore"></a>Hive metastore</span></span>

<span data-ttu-id="410d3-223">원할 경우 tooretain 하이브 테이블 HDInsight 클러스터를 삭제 한 후 사용자 지정 metastore를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-223">If you want tooretain your Hive tables after you delete an HDInsight cluster, use a custom metastore.</span></span> <span data-ttu-id="410d3-224">그런 다음 hello metastore tooanother HDInsight 클러스터를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-224">You can then attach hello metastore tooanother HDInsight cluster.</span></span>

<span data-ttu-id="410d3-225">특정 HDInsight 클러스터 버전에 대해 만든 HDInsight metastore는 여러 다른 HDInsight 클러스터 버전 간에 공유할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-225">An HDInsight metastore that is created for one HDInsight cluster version cannot be shared across different HDInsight cluster versions.</span></span> <span data-ttu-id="410d3-226">HDInsight 버전 목록은 [지원되는 HDInsight 버전](hdinsight-component-versioning.md#supported-hdinsight-versions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="410d3-226">For a list of HDInsight versions, see [Supported HDInsight versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>

### <a name="oozie-metastore"></a><span data-ttu-id="410d3-227">Oozie Metastore</span><span class="sxs-lookup"><span data-stu-id="410d3-227">Oozie metastore</span></span>

<span data-ttu-id="410d3-228">tooincrease 성능 Oozie를 사용 하는 경우 사용자 지정 metastore를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-228">tooincrease performance when using Oozie, use a custom metastore.</span></span> <span data-ttu-id="410d3-229">Metastore는 클러스터를 삭제 한 후 tooOozie 작업 데이터에 액세스를 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-229">A metastore can also provide access tooOozie job data after you delete your cluster.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="410d3-230">사용자 지정 Oozie Metastore는 다시 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-230">You cannot reuse a custom Oozie metastore.</span></span> <span data-ttu-id="410d3-231">사용자 지정 Oozie metastore toouse hello HDInsight 클러스터를 만들 때 빈 Azure SQL 데이터베이스를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-231">toouse a custom Oozie metastore, you must provide an empty Azure SQL Database when creating hello HDInsight cluster.</span></span>

## <a name="configure-cluster-size"></a><span data-ttu-id="410d3-232">클러스터 크기 구성</span><span class="sxs-lookup"><span data-stu-id="410d3-232">Configure cluster size</span></span>

<span data-ttu-id="410d3-233">존재 하는 hello 클러스터 노드 사용량에 대 한 요금이 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-233">You are billed for node usage for as long as hello cluster exists.</span></span> <span data-ttu-id="410d3-234">클러스터를 만들면 청구 시작 되 고 중지 hello 클러스터 삭제 될 때입니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-234">Billing starts when a cluster is created and stops when hello cluster is deleted.</span></span> <span data-ttu-id="410d3-235">클러스터의 경우 할당을 취소하거나 보류할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-235">Clusters can’t be de-allocated or put on hold.</span></span>

<span data-ttu-id="410d3-236">hello 비용 HDInsight 클러스터의 노드 및 노드 hello에 대 한 hello 가상 컴퓨터 크기의 hello 수로 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-236">hello cost of HDInsight clusters is determined by hello number of nodes and hello virtual machines sizes for hello nodes.</span></span> 

<span data-ttu-id="410d3-237">클러스터 유형마다 서로 다른 노드 유형, 노드 수 및 노드 크기를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-237">Different cluster types have different node types, numbers of nodes, and node sizes:</span></span>
* <span data-ttu-id="410d3-238">Hadoop 클러스터 유형 기본값:</span><span class="sxs-lookup"><span data-stu-id="410d3-238">Hadoop cluster type default:</span></span> 
    * <span data-ttu-id="410d3-239">*헤드 노드* 2개</span><span class="sxs-lookup"><span data-stu-id="410d3-239">Two *head nodes*</span></span>  
    * <span data-ttu-id="410d3-240">*데이터 노드* 4개</span><span class="sxs-lookup"><span data-stu-id="410d3-240">Four *data nodes*</span></span>
* <span data-ttu-id="410d3-241">Storm 클러스터 유형 기본값:</span><span class="sxs-lookup"><span data-stu-id="410d3-241">Storm cluster type default:</span></span> 
    * <span data-ttu-id="410d3-242">*Nimbus 노드* 2개</span><span class="sxs-lookup"><span data-stu-id="410d3-242">Two *Nimbus nodes*</span></span>
    * <span data-ttu-id="410d3-243">*ZooKeeper 노드* 3개</span><span class="sxs-lookup"><span data-stu-id="410d3-243">Three *ZooKeeper nodes*</span></span>
    * <span data-ttu-id="410d3-244">*감독자 노드* 4개</span><span class="sxs-lookup"><span data-stu-id="410d3-244">Four *supervisor nodes*</span></span> 

<span data-ttu-id="410d3-245">HDInsight만 사용하려는 경우, 하나의 데이터 노드를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-245">If you are just trying out HDInsight, we recommend you use one data node.</span></span> <span data-ttu-id="410d3-246">HDInsight 가격에 대한 자세한 내용은 [HDInsight 가격](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="410d3-246">For more information about HDInsight pricing, see [HDInsight pricing](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409).</span></span>

> [!NOTE]
> <span data-ttu-id="410d3-247">hello 클러스터 크기 한도 Azure 구독 마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-247">hello cluster size limit varies among Azure subscriptions.</span></span> <span data-ttu-id="410d3-248">연락처 [Azure 청구 지원](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) tooincrease hello 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-248">Contact [Azure billing support](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) tooincrease hello limit.</span></span>
>

<span data-ttu-id="410d3-249">Hello 노드 크기 hello를 통해 사용할 수는 hello Azure 포털 tooconfigure hello 클러스터를 사용할 때는 **노드 가격 책정 계층** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-249">When you use hello Azure portal tooconfigure hello cluster, hello node size is available through hello **Node Pricing Tiers** blade.</span></span> <span data-ttu-id="410d3-250">Hello 포털에서 확인할 수 있습니다 hello hello 다양 한 노드 크기와 관련 된 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-250">In hello portal, you can also see hello cost associated with hello different node sizes.</span></span> 

![HDInsight VM 노드 크기](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-node-sizes.png)

### <a name="virtual-machine-sizes"></a><span data-ttu-id="410d3-252">가상 컴퓨터 크기</span><span class="sxs-lookup"><span data-stu-id="410d3-252">Virtual machine sizes</span></span> 
<span data-ttu-id="410d3-253">클러스터를 배포 하는 경우 선택 기반 계산 리소스 hello 솔루션 toodeploy 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-253">When you deploy clusters, choose compute resources based on hello solution you plan toodeploy.</span></span> <span data-ttu-id="410d3-254">hello 다음 Vm은 HDInsight 클러스터에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-254">hello following VMs are used for HDInsight clusters:</span></span>
* <span data-ttu-id="410d3-255">A 및 D1-4 시리즈 VM: [범용 Linux VM 크기](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-general)</span><span class="sxs-lookup"><span data-stu-id="410d3-255">A and D1-4 series VMs: [General-purpose Linux VM sizes](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-general)</span></span>
* <span data-ttu-id="410d3-256">D11-14 시리즈 VM: [메모리 최적화 Linux VM 크기](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-memory)</span><span class="sxs-lookup"><span data-stu-id="410d3-256">D11-14 series VM: [Memory-optimized Linux VM sizes](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-memory)</span></span>

<span data-ttu-id="410d3-257">값 초과 toofind toospecify VM 크기를 사용 하 여 클러스터를 만드는 동안 다양 한 Sdk hello 또는 Azure PowerShell을 사용 하는 동안 참조를 사용 해야 [VM의 크기를 조정 하는 HDInsight 클러스터에 대 한 toouse](../cloud-services/cloud-services-sizes-specs.md#size-tables)합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-257">toofind out what value you should use toospecify a VM size while creating a cluster using hello different SDKs or while using Azure PowerShell, see [VM sizes toouse for HDInsight clusters](../cloud-services/cloud-services-sizes-specs.md#size-tables).</span></span> <span data-ttu-id="410d3-258">이 연결 된 문서에서 값을 사용할 hello hello **크기** hello 테이블의 열입니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-258">From this linked article, use hello value in hello **Size** column of hello tables.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="410d3-259">클러스터에 필요한 작업자 노드 수가 32개를 초과하는 경우 최소한 코어 8개와 14GB RAM을 가진 헤드 노드 크기를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-259">If you need more than 32 worker nodes in a cluster, you must select a head node size with at least 8 cores and 14 GB of RAM.</span></span>
>
>

<span data-ttu-id="410d3-260">자세한 내용은 [가상 컴퓨터의 크기](../virtual-machines/windows/sizes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="410d3-260">For more information, see [Sizes for virtual machines](../virtual-machines/windows/sizes.md).</span></span> <span data-ttu-id="410d3-261">다양 한 크기의 hello 가격에 대 한 정보를 참조 하십시오. [HDInsight 가격](https://azure.microsoft.com/pricing/details/hdinsight)합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-261">For information about pricing of hello various sizes, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight).</span></span>   

## <a name="custom-cluster-setup"></a><span data-ttu-id="410d3-262">사용자 지정 클러스터 설정</span><span class="sxs-lookup"><span data-stu-id="410d3-262">Custom cluster setup</span></span>
<span data-ttu-id="410d3-263">빠른 hello에 사용자 지정 클러스터 설치 빌드 설정을 만들고 hello 다음 옵션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-263">Custom cluster setup builds on hello Quick create settings, and adds hello following options:</span></span>
- [<span data-ttu-id="410d3-264">HDInsight 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="410d3-264">HDInsight applications</span></span>](#hdinsight-applications)
- <span data-ttu-id="410d3-265">[클러스터 크기](#cluster-size):</span><span class="sxs-lookup"><span data-stu-id="410d3-265">[Cluster size](#cluster-size)</span></span>
- <span data-ttu-id="410d3-266">고급 설정</span><span class="sxs-lookup"><span data-stu-id="410d3-266">Advanced settings</span></span>
  - [<span data-ttu-id="410d3-267">스크립트 동작</span><span class="sxs-lookup"><span data-stu-id="410d3-267">Script actions</span></span>](#customize-clusters-using-script-action)
  - [<span data-ttu-id="410d3-268">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="410d3-268">Virtual network</span></span>](#use-virtual-network)

## <a name="install-hdinsight-applications-on-clusters"></a><span data-ttu-id="410d3-269">클러스터에 HDInsight 응용 프로그램 설치</span><span class="sxs-lookup"><span data-stu-id="410d3-269">Install HDInsight applications on clusters</span></span>

<span data-ttu-id="410d3-270">HDInsight 응용 프로그램은 Linux 기반 HDInsight 클러스터에 사용자가 설치할 수 있는 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-270">An HDInsight application is an application that users can install on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="410d3-271">Microsoft, 타사에서 제공하거나 또는 직접 개발한 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-271">You can use applications provided by Microsoft, third parties, or that you develop yourself.</span></span> <span data-ttu-id="410d3-272">자세한 내용은 [Azure HDInsight에 타사 Hadoop 응용 프로그램 설치](hdinsight-apps-install-applications.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="410d3-272">For more information, see [Install third-party Hadoop applications on Azure HDInsight](hdinsight-apps-install-applications.md).</span></span>

<span data-ttu-id="410d3-273">빈 가장자리 노드에 대부분의 hello HDInsight 응용 프로그램이 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-273">Most of hello HDInsight applications are installed on an empty edge node.</span></span>  <span data-ttu-id="410d3-274">빈 가장자리 노드는 동일한 클라이언트 도구 설치 및 헤드 노드 hello와 같이 구성 hello로 Linux 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="410d3-274">An empty edge node is a Linux virtual machine with hello same client tools installed and configured as in hello head node.</span></span> <span data-ttu-id="410d3-275">Hello 클러스터에 액세스, 클라이언트 응용 프로그램을 테스트 하 고, 클라이언트 응용 프로그램을 호스팅하기 위한 hello 가장자리 노드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-275">You can use hello edge node for accessing hello cluster, testing your client applications, and hosting your client applications.</span></span> <span data-ttu-id="410d3-276">자세한 내용은 [HDInsight에서 빈 에지 노드 사용](hdinsight-apps-use-edge-node.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="410d3-276">For more information, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>

## <a name="advanced-settings-script-actions"></a><span data-ttu-id="410d3-277">고급 설정: 스크립트 작업</span><span class="sxs-lookup"><span data-stu-id="410d3-277">Advanced settings: Script actions</span></span>

<span data-ttu-id="410d3-278">만드는 동안 스크립트를 사용하여 추가 구성 요소를 설치하거나 클러스터 구성을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-278">You can install additional components or customize cluster configuration by using scripts during creation.</span></span> <span data-ttu-id="410d3-279">이러한 스크립트를 통해 호출 되는 **스크립트 동작**, hello Azure 포털, HDInsight Windows PowerShell cmdlet 또는 hello HDInsight.NET SDK에서 사용할 수 있는 구성 옵션은입니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-279">Such scripts are invoked via **Script Action**, which is a configuration option that can be used from hello Azure portal, HDInsight Windows PowerShell cmdlets, or hello HDInsight .NET SDK.</span></span> <span data-ttu-id="410d3-280">자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="410d3-280">For more information, see [Customize HDInsight cluster using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="410d3-281">Mahout 및 Cascading와 같은 일부 네이티브 Java 구성 요소가 JAR (Java Archive) 파일로 hello 클러스터에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-281">Some native Java components, like Mahout and Cascading, can be run on hello cluster as Java Archive (JAR) files.</span></span> <span data-ttu-id="410d3-282">이러한 JAR 파일 분산된 tooAzure 저장 될 수 있습니다 및 tooHDInsight 클러스터 Hadoop 작업 전송 메커니즘으로 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-282">These JAR files can be distributed tooAzure Storage and submitted tooHDInsight clusters with Hadoop job submission mechanisms.</span></span> <span data-ttu-id="410d3-283">자세한 내용은 [프로그래밍 방식으로 Hadoop 작업 제출](hdinsight-submit-hadoop-jobs-programmatically.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="410d3-283">For more information, see [Submit Hadoop jobs programmatically](hdinsight-submit-hadoop-jobs-programmatically.md).</span></span>

> [!NOTE]
> <span data-ttu-id="410d3-284">JAR 파일 tooHDInsight 클러스터 배포 문제 또는 문의 HDInsight 클러스터에서 JAR 파일을 호출할 경우 [Microsoft 지원](https://azure.microsoft.com/support/options/)합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-284">If you have issues deploying JAR files tooHDInsight clusters, or calling JAR files on HDInsight clusters, contact [Microsoft Support](https://azure.microsoft.com/support/options/).</span></span>
>
> <span data-ttu-id="410d3-285">Cascading은 HDInsight에서 지원되지 않으며 Microsoft 지원 대상이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-285">Cascading is not supported by HDInsight and is not eligible for Microsoft Support.</span></span> <span data-ttu-id="410d3-286">지원 되는 구성의 목록에 대 한 참조 [HDInsight에서 제공 하는 hello 클러스터 버전의 새로운 기능](hdinsight-component-versioning.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-286">For lists of supported components, see [What's new in hello cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
>
>

<span data-ttu-id="410d3-287">경우에 따라 원하는 hello 만드는 프로세스 동안 구성 파일을 다음 tooconfigure hello:</span><span class="sxs-lookup"><span data-stu-id="410d3-287">Sometimes, you want tooconfigure hello following configuration files during hello creation process:</span></span>

* <span data-ttu-id="410d3-288">clusterIdentity.xml</span><span class="sxs-lookup"><span data-stu-id="410d3-288">clusterIdentity.xml</span></span>
* <span data-ttu-id="410d3-289">core-site.xml</span><span class="sxs-lookup"><span data-stu-id="410d3-289">core-site.xml</span></span>
* <span data-ttu-id="410d3-290">gateway.xml</span><span class="sxs-lookup"><span data-stu-id="410d3-290">gateway.xml</span></span>
* <span data-ttu-id="410d3-291">hbase-env.xml</span><span class="sxs-lookup"><span data-stu-id="410d3-291">hbase-env.xml</span></span>
* <span data-ttu-id="410d3-292">hbase-site.xml</span><span class="sxs-lookup"><span data-stu-id="410d3-292">hbase-site.xml</span></span>
* <span data-ttu-id="410d3-293">hdfs-site.xml</span><span class="sxs-lookup"><span data-stu-id="410d3-293">hdfs-site.xml</span></span>
* <span data-ttu-id="410d3-294">hive-env.xml</span><span class="sxs-lookup"><span data-stu-id="410d3-294">hive-env.xml</span></span>
* <span data-ttu-id="410d3-295">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="410d3-295">hive-site.xml</span></span>
* <span data-ttu-id="410d3-296">mapred-site</span><span class="sxs-lookup"><span data-stu-id="410d3-296">mapred-site</span></span>
* <span data-ttu-id="410d3-297">oozie-site.xml</span><span class="sxs-lookup"><span data-stu-id="410d3-297">oozie-site.xml</span></span>
* <span data-ttu-id="410d3-298">oozie-env.xml</span><span class="sxs-lookup"><span data-stu-id="410d3-298">oozie-env.xml</span></span>
* <span data-ttu-id="410d3-299">storm-site.xml</span><span class="sxs-lookup"><span data-stu-id="410d3-299">storm-site.xml</span></span>
* <span data-ttu-id="410d3-300">tez-site.xml</span><span class="sxs-lookup"><span data-stu-id="410d3-300">tez-site.xml</span></span>
* <span data-ttu-id="410d3-301">webhcat-site.xml</span><span class="sxs-lookup"><span data-stu-id="410d3-301">webhcat-site.xml</span></span>
* <span data-ttu-id="410d3-302">yarn-site.xml</span><span class="sxs-lookup"><span data-stu-id="410d3-302">yarn-site.xml</span></span>

<span data-ttu-id="410d3-303">자세한 내용은 [부트스트랩을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-bootstrap.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="410d3-303">For more information, see [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md).</span></span>

## <a name="advanced-settings-extend-clusters-with-a-virtual-network"></a><span data-ttu-id="410d3-304">고급 설정: 가상 네트워크를 사용하여 클러스터 확장</span><span class="sxs-lookup"><span data-stu-id="410d3-304">Advanced settings: Extend clusters with a virtual network</span></span>
<span data-ttu-id="410d3-305">솔루션에 여러 HDInsight 클러스터 형식 간에 분산 되어 있는 기술 요구 하는 경우는 [Azure 가상 네트워크](https://docs.microsoft.com/azure/virtual-network) hello 필요한 클러스터 종류를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-305">If your solution requires technologies that are spread across multiple HDInsight cluster types, an [Azure virtual network](https://docs.microsoft.com/azure/virtual-network) can connect hello required cluster types.</span></span> <span data-ttu-id="410d3-306">Toodirectly 서로 통신이 구성에서는 hello 클러스터 및 toothem 배포한 모든 코드를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-306">This configuration allows hello clusters, and any code you deploy toothem, toodirectly communicate with each other.</span></span>

<span data-ttu-id="410d3-307">HDInsight와 함께 Azure Virtual Network를 사용하는 방법에 대한 자세한 내용은 [Azure Virtual Network를 사용하여 HDInsight 확장](hdinsight-extend-hadoop-virtual-network.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="410d3-307">For more information on using an Azure virtual network with HDInsight, see [Extend HDInsight with Azure virtual networks](hdinsight-extend-hadoop-virtual-network.md).</span></span>

<span data-ttu-id="410d3-308">Azure Virtual Network 내에서 두 개의 클러스터 유형을 사용하는 예제는 [Storm 및 HBase의 센서 데이터 분석](hdinsight-storm-sensor-data-analysis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="410d3-308">For an example of using two cluster types within an Azure virtual network, see [Analyze sensor data with Storm and HBase](hdinsight-storm-sensor-data-analysis.md).</span></span> <span data-ttu-id="410d3-309">HDInsight를 사용 하 여 hello 가상 네트워크에 대 한 특정 구성 요구 사항을 포함 하 여 가상 네트워크에 대 한 자세한 내용은 참조 하십시오. [Azure 가상 네트워크를 사용 하 여 HDInsight 확장 기능](hdinsight-extend-hadoop-virtual-network.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="410d3-309">For more information about using HDInsight with a virtual network, including specific configuration requirements for hello virtual network, see [Extend HDInsight capabilities by using Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <a name="troubleshoot-access-control-issues"></a><span data-ttu-id="410d3-310">액세스 제어 문제 해결</span><span class="sxs-lookup"><span data-stu-id="410d3-310">Troubleshoot access control issues</span></span>

<span data-ttu-id="410d3-311">HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="410d3-311">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="410d3-312">다음 단계</span><span class="sxs-lookup"><span data-stu-id="410d3-312">Next steps</span></span>

- [<span data-ttu-id="410d3-313">HDInsight, hello Hadoop 에코 시스템 및 Hadoop 클러스터는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="410d3-313">What are HDInsight, hello Hadoop ecosystem, and Hadoop clusters?</span></span>](hdinsight-hadoop-introduction.md)
- [<span data-ttu-id="410d3-314">HDInsight에서 Hadoop 사용 시작</span><span class="sxs-lookup"><span data-stu-id="410d3-314">Get started using Hadoop in HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
- [<span data-ttu-id="410d3-315">Windows PC에서 HDInsight의 Hadoop 작업</span><span class="sxs-lookup"><span data-stu-id="410d3-315">Work in Hadoop on HDInsight from a Windows PC</span></span>](hdinsight-hadoop-windows-tools.md)
