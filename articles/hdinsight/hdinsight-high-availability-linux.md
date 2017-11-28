---
title: "Hadoop의 고가용성 - Azure HDInsight | Microsoft Docs"
description: "HDInsight 클러스터에서 추가 헤드 노드를 사용하여 안정성과 가용성을 높이는 방법을 알아봅니다. 이로 인해 Ambari 및 Hive와 같은 Hadoop 서비스에 미치는 영향과 SSH를 사용하여 각 헤드 노드에 개별적으로 연결하는 방법에 대해 알아봅니다."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
keywords: hadoop high availability
ms.assetid: 99c9f59c-cf6b-4529-99d1-bf060435e8d4
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 07/28/2017
ms.author: larryfr
ms.openlocfilehash: e66ba67a36fc48d1762ba302d708e060489fdc71
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="5cd36-105">HDInsight에서 Hadoop 클러스터의 가용성 및 안정성</span><span class="sxs-lookup"><span data-stu-id="5cd36-105">Availability and reliability of Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="5cd36-106">HDInsight 클러스터는 두 개의 헤드 노드를 제공하여 실행 중인 Hadoop 서비스와 작업의 안정성과 가용성을 높입니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-106">HDInsight clusters provide two head nodes to increase the availability and reliability of Hadoop services and jobs running.</span></span>

<span data-ttu-id="5cd36-107">Hadoop은 클러스터의 여러 노드에서 서비스와 데이터를 복사하여 고가용성과 안정성을 달성합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-107">Hadoop achieves high availability and reliability by replicating services and data across multiple nodes in a cluster.</span></span> <span data-ttu-id="5cd36-108">그러나 Hadoop의 표준 배포에는 일반적으로 단일 헤드 노드만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-108">However standard distributions of Hadoop typically have only a single head node.</span></span> <span data-ttu-id="5cd36-109">단일 헤드 노드의 가동 중단으로 인해 클러스터의 작동이 중지될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-109">Any outage of the single head node can cause the cluster to stop working.</span></span> <span data-ttu-id="5cd36-110">HDInsight는 Hadoop의 가용성 및 안정성을 향상시키기 위해 두 헤드 노드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-110">HDInsight provides two headnodes to improve Hadoop's availability and reliability.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5cd36-111">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5cd36-112">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5cd36-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="availability-and-reliability-of-nodes"></a><span data-ttu-id="5cd36-113">노드의 가용성 및 안정성</span><span class="sxs-lookup"><span data-stu-id="5cd36-113">Availability and reliability of nodes</span></span>

<span data-ttu-id="5cd36-114">HDInsight 클러스터에 있는 노드는 Azure 가상 컴퓨터를 사용하여 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-114">Nodes in an HDInsight cluster are implemented using Azure Virtual Machines.</span></span> <span data-ttu-id="5cd36-115">다음 섹션에서는 HDInsight와 함께 사용되는 개별 노드 유형을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-115">The following sections discuss the individual node types used with HDInsight.</span></span> 

> [!NOTE]
> <span data-ttu-id="5cd36-116">일부 노드 유형은 클러스터 유형에 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-116">Not all node types are used for a cluster type.</span></span> <span data-ttu-id="5cd36-117">예를 들어 Hadoop 클러스터 유형에는 Nimbus 노드가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-117">For example, a Hadoop cluster type does not have any Nimbus nodes.</span></span> <span data-ttu-id="5cd36-118">HDInsight 클러스터 유형에서 사용하는 노드에 대한 자세한 내용은 [HDInsight에서 Linux 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) 문서의 클러스터 유형 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5cd36-118">For more information on nodes used by HDInsight cluster types, see the Cluster types section of the [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) document.</span></span>

### <a name="head-nodes"></a><span data-ttu-id="5cd36-119">헤드 노드</span><span class="sxs-lookup"><span data-stu-id="5cd36-119">Head nodes</span></span>

<span data-ttu-id="5cd36-120">Hadoop 서비스의 고가용성을 보장하기 위해 HDInsight는 두 개의 헤드 노드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-120">To ensure high availability of Hadoop services, HDInsight provides two head nodes.</span></span> <span data-ttu-id="5cd36-121">두 헤드 노드가 모두 활성화되어 HDInsight 클러스터 내에서 동시에 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-121">Both head nodes are active and running within the HDInsight cluster simultaneously.</span></span> <span data-ttu-id="5cd36-122">일부 서비스(예: HDFS 또는 YARN)는 항상 헤드 노드 하나에서만 '활성' 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-122">Some services, such as HDFS or YARN, are only 'active' on one head node at any given time.</span></span> <span data-ttu-id="5cd36-123">다른 서비스(예: HiveServer2 또는 Hive MetaStore)는 두 헤드 노드에서 동시에 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-123">Other services such as HiveServer2 or Hive MetaStore are active on both head nodes at the same time.</span></span>

<span data-ttu-id="5cd36-124">헤드 노드(및 HDInsight의 다른 노드)에는 노드의 호스트 이름의 일부인 숫자 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-124">Head nodes (and other nodes in HDInsight) have a numeric value as part of the hostname of the node.</span></span> <span data-ttu-id="5cd36-125">예를 들면 `hn0-CLUSTERNAME` 또는 `hn4-CLUSTERNAME`과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-125">For example, `hn0-CLUSTERNAME` or `hn4-CLUSTERNAME`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5cd36-126">숫자 값을 노드가 기본 또는 보조 노드와 연결하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5cd36-126">Do not associate the numeric value with whether a node is primary or secondary.</span></span> <span data-ttu-id="5cd36-127">숫자 값은 각 노드에 대해 고유한 이름을 제공하기 위해 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-127">The numeric value is only present to provide a unique name for each node.</span></span>

### <a name="nimbus-nodes"></a><span data-ttu-id="5cd36-128">Nimbus 노드</span><span class="sxs-lookup"><span data-stu-id="5cd36-128">Nimbus Nodes</span></span>

<span data-ttu-id="5cd36-129">Nimbus 노드는 Storm 클러스터와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-129">Nimbus nodes are available with Storm clusters.</span></span> <span data-ttu-id="5cd36-130">Nimbus 노드는 작업자 노드에 대한 프로세싱을 배포하고 모니터링하여 Hadoop JobTracker에 유사한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-130">The Nimbus nodes provide similar functionality to the Hadoop JobTracker by distributing and monitoring processing across worker nodes.</span></span> <span data-ttu-id="5cd36-131">HDInsight는 Storm 클러스터에 두 개의 Nimbus 노드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-131">HDInsight provides two Nimbus nodes for Storm clusters</span></span>

### <a name="zookeeper-nodes"></a><span data-ttu-id="5cd36-132">Zookeeper 노드</span><span class="sxs-lookup"><span data-stu-id="5cd36-132">Zookeeper nodes</span></span>

<span data-ttu-id="5cd36-133">[ZooKeeper](http://zookeeper.apache.org/) 노드는 헤드 노드에서 마스터 서비스의 리더 선택에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-133">[ZooKeeper](http://zookeeper.apache.org/) nodes are used for leader election of master services on head nodes.</span></span> <span data-ttu-id="5cd36-134">서비스, 데이터(작업자) 노드 및 게이트웨이에서 어떤 헤드 노드의 마스터 서비스가 활성화되어 있는지 파악하도록 하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-134">They are also used to insure that services, data (worker) nodes, and gateways know which head node a master service is active on.</span></span> <span data-ttu-id="5cd36-135">기본적으로 HDInsight는 3개의 ZooKeeper 노드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-135">By default, HDInsight provides three ZooKeeper nodes.</span></span>

### <a name="worker-nodes"></a><span data-ttu-id="5cd36-136">작업자 노드</span><span class="sxs-lookup"><span data-stu-id="5cd36-136">Worker nodes</span></span>

<span data-ttu-id="5cd36-137">작업자 노드는 클러스터에 작업이 제출될 경우 실제 데이터 분석을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-137">Worker nodes perform the actual data analysis when a job is submitted to the cluster.</span></span> <span data-ttu-id="5cd36-138">작업자 노드가 실패하면 수행 중인 작업이 다른 작업자 노드에 제출됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-138">If a worker node fails, the task that it was performing is submitted to another worker node.</span></span> <span data-ttu-id="5cd36-139">기본적으로 HDInsight는 네 개의 작업자 노드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-139">By default, HDInsight creates four worker nodes.</span></span> <span data-ttu-id="5cd36-140">이 숫자는 클러스터를 만드는 중에 그리고 만든 후에 필요에 따라 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-140">You can change this number to suit your needs both during and after cluster creation.</span></span>

### <a name="edge-node"></a><span data-ttu-id="5cd36-141">에지 노드</span><span class="sxs-lookup"><span data-stu-id="5cd36-141">Edge node</span></span>

<span data-ttu-id="5cd36-142">에지 노드는 클러스터 내에서 데이터 분석에 적극적으로 참가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-142">An edge node does not actively participate in data analysis within the cluster.</span></span> <span data-ttu-id="5cd36-143">이는 개발자 또는 데이터 과학자가 Hadoop과 함께 작업하는 경우 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-143">It is used by developers or data scientists when working with Hadoop.</span></span> <span data-ttu-id="5cd36-144">에지 노드는 클러스터의 다른 노드와 동일한 Azure 가상 네트워크에 있으며 다른 모든 노드에 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-144">The edge node lives in the same Azure Virtual Network as the other nodes in the cluster, and can directly access all other nodes.</span></span> <span data-ttu-id="5cd36-145">에지 노드는 중요한 Hadoop 서비스 또는 분석 작업에서 리소스를 가져오지 않으면서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-145">The edge node can be used without taking resources away from critical Hadoop services or analysis jobs.</span></span>

<span data-ttu-id="5cd36-146">현재 HDInsight의 R 서버는 기본적으로 에지 노드를 제공하는 유일한 클러스터 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-146">Currently, R Server on HDInsight is the only cluster type that provides an edge node by default.</span></span> <span data-ttu-id="5cd36-147">HDInsight의 R 서버의 경우 에지 노드는 분산된 처리를 위해 클러스터에 제출하기 전에 노드에서 로컬로 R 코드를 테스트하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-147">For R Server on HDInsight, the edge node is used test R code locally on the node before submitting it to the cluster for distributed processing.</span></span>

<span data-ttu-id="5cd36-148">R Server 이외의 클러스터 유형으로 에지 노드를 사용하는 방법에 대한 내용은 [HDInsight에서 에지 노드 사용](hdinsight-apps-use-edge-node.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5cd36-148">For information on using an edge node with cluster types other than R Server, see the [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md) document.</span></span>

## <a name="accessing-the-nodes"></a><span data-ttu-id="5cd36-149">노드 액세스</span><span class="sxs-lookup"><span data-stu-id="5cd36-149">Accessing the nodes</span></span>

<span data-ttu-id="5cd36-150">인터넷을 통한 클러스터 액세스는 공용 게이트웨이를 통해 제공되며,</span><span class="sxs-lookup"><span data-stu-id="5cd36-150">Access to the cluster over the internet is provided through a public gateway.</span></span> <span data-ttu-id="5cd36-151">액세스는 헤드 노드와 에지 노드(하나가 있는 경우)에 연결하는 것으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-151">Access is limited to connecting to the head nodes and (if one exists) the edge node.</span></span> <span data-ttu-id="5cd36-152">여러 헤드 노드가 있는 경우 헤드 노드에서 실행되는 서비스에 대한 액세스는 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-152">Access to services running on the head nodes is not effected by having multiple head nodes.</span></span> <span data-ttu-id="5cd36-153">공용 게이트웨이는 요청된 서비스를 호스팅하는 헤드 노드로 요청을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-153">The public gateway routes requests to the head node that hosts the requested service.</span></span> <span data-ttu-id="5cd36-154">예를 들어 현재 Ambari가 보조 헤드 노드에서 호스팅되는 경우 게이트웨이는 Ambari에 들어오는 요청을 해당 노드로 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-154">For example, if Ambari is currently hosted on the secondary head node, the gateway routes incoming requests for Ambari to that node.</span></span>

<span data-ttu-id="5cd36-155">공용 게이트웨이를 통한 액세스는 443(HTTPS), 22 및 23 포트로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-155">Access over the public gateway is limited to port 443 (HTTPS), 22, and 23.</span></span>

* <span data-ttu-id="5cd36-156">__443__ 포트는 헤드 노드에 호스팅된 Ambari 및 기타 웹 UI 또는 REST API에 액세스하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-156">Port __443__ is used to access Ambari and other web UI or REST APIs hosted on the head nodes.</span></span>

* <span data-ttu-id="5cd36-157">__22__ 포트는 SSH가 있는 기본 헤드 노드 또는 에지 노드에 액세스하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-157">Port __22__ is used to access the primary head node or edge node with SSH.</span></span>

* <span data-ttu-id="5cd36-158">__23__ 포트는 SSH가 있는 보조 헤드 노드에 액세스하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-158">Port __23__ is used to access the secondary head node with SSH.</span></span> <span data-ttu-id="5cd36-159">예를 들어 `ssh username@mycluster-ssh.azurehdinsight.net`은 **mycluster**라는 클러스터의 기본 헤드 노드에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-159">For example, `ssh username@mycluster-ssh.azurehdinsight.net` connects to the primary head node of the cluster named **mycluster**.</span></span>

<span data-ttu-id="5cd36-160">SSH 사용에 대한 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5cd36-160">For more information on using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

### <a name="internal-fully-qualified-domain-names-fqdn"></a><span data-ttu-id="5cd36-161">내부 FQDN(정규화된 도메인 이름)</span><span class="sxs-lookup"><span data-stu-id="5cd36-161">Internal fully qualified domain names (FQDN)</span></span>

<span data-ttu-id="5cd36-162">HDInsight 클러스터의 노드에는 클러스터에서만 액세스할 수 있는 내부 IP 주소와 FQDN이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-162">Nodes in an HDInsight cluster have an internal IP address and FQDN that can only be accessed from the cluster.</span></span> <span data-ttu-id="5cd36-163">내부 FQDN 또는 IP 주소를 사용하여 클러스터의 서비스에 액세스할 경우, Ambari를 사용하여 서비스 액세스 시 사용할 IP 또는 FQDN을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-163">When accessing services on the cluster using the internal FQDN or IP address, you should use Ambari to verify the IP or FQDN to use when accessing the service.</span></span>

<span data-ttu-id="5cd36-164">예를 들어 Oozie 서비스는 헤드 노드에서만 실행될 수 있으며, SSH 세션에서 `oozie` 명령을 사용하려면 서비스에 대한 URL이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-164">For example, the Oozie service can only run on one head node, and using the `oozie` command from an SSH session requires the URL to the service.</span></span> <span data-ttu-id="5cd36-165">이 URL은 다음 명령을 사용하여 Ambari에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-165">This URL can be retrieved from Ambari by using the following command:</span></span>

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

<span data-ttu-id="5cd36-166">이 명령은 `oozie` 명령과 함께 사용할 내부 URL을 포함하는 다음 명령과 비슷한 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-166">This command returns a value similar to the following command, which contains the internal URL to use with the `oozie` command:</span></span>

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

<span data-ttu-id="5cd36-167">Ambari REST API 작업에 대한 자세한 내용은 [Ambari REST API를 사용하여 HDInsight 모니터링 및 관리](hdinsight-hadoop-manage-ambari-rest-api.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5cd36-167">For more information on working with the Ambari REST API, see [Monitor and Manage HDInsight using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

### <a name="accessing-other-node-types"></a><span data-ttu-id="5cd36-168">다른 노드 유형에 액세스</span><span class="sxs-lookup"><span data-stu-id="5cd36-168">Accessing other node types</span></span>

<span data-ttu-id="5cd36-169">다음 방법을 사용하여 인터넷을 통해 직접 액세스할 수 없는 노드에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-169">You can connect to nodes that are not directly accessible over the internet by using the following methods:</span></span>

* <span data-ttu-id="5cd36-170">**SSH**: SSH를 사용하여 헤드 노드에 연결되면 SSH를 사용하여 헤드 노드에서 클러스터의 다른 노드에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-170">**SSH**: Once connected to a head node using SSH, you can then use SSH from the head node to connect to other nodes in the cluster.</span></span> <span data-ttu-id="5cd36-171">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5cd36-171">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

* <span data-ttu-id="5cd36-172">**SSH 터널**: 인터넷에 노출되지 않는 노드 중 하나에서 호스팅되는 웹 서비스에 액세스해야 하는 경우 SSH 터널을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-172">**SSH Tunnel**: If you need to access a web service hosted on one of the nodes that is not exposed to the internet, you must use an SSH tunnel.</span></span> <span data-ttu-id="5cd36-173">자세한 내용은 [HDInsight와 SSH 터널 사용](hdinsight-linux-ambari-ssh-tunnel.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5cd36-173">For more information, see the [Use an SSH tunnel with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

* <span data-ttu-id="5cd36-174">**Azure 가상 네트워크**: HDInsight 클러스터가 Azure 가상 네트워크의 일부인 경우 동일한 가상 네트워크의 리소스는 클러스터의 모든 노드에 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-174">**Azure Virtual Network**: If your HDInsight cluster is part of an Azure Virtual Network, any resource on the same Virtual Network can directly access all nodes in the cluster.</span></span> <span data-ttu-id="5cd36-175">자세한 내용은 [Azure 가상 네트워크를 사용하여 HDInsight 기능 확장](hdinsight-extend-hadoop-virtual-network.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5cd36-175">For more information, see the [Extend HDInsight using Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

## <a name="how-to-check-on-a-service-status"></a><span data-ttu-id="5cd36-176">서비스 상태를 확인하는 방법</span><span class="sxs-lookup"><span data-stu-id="5cd36-176">How to check on a service status</span></span>

<span data-ttu-id="5cd36-177">헤드 노드에서 실행되는 서비스의 상태를 확인하려면 Ambari 웹 UI 또는 Ambari REST API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-177">To check the status of services that run on the head nodes, use the Ambari Web UI or the Ambari REST API.</span></span>

### <a name="ambari-web-ui"></a><span data-ttu-id="5cd36-178">Ambari 웹 UI</span><span class="sxs-lookup"><span data-stu-id="5cd36-178">Ambari Web UI</span></span>

<span data-ttu-id="5cd36-179">Ambari 웹 UI는 https://CLUSTERNAME.azurehdinsight.net에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-179">The Ambari Web UI is viewable at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="5cd36-180">**CLUSTERNAME** 을 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-180">Replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="5cd36-181">메시지가 표시되면 클러스터의 HTTP 사용자 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-181">If prompted, enter the HTTP user credentials for your cluster.</span></span> <span data-ttu-id="5cd36-182">기본 HTTP 사용자 이름은 **admin** 이고 암호는 클러스터를 만들 때 입력한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-182">The default HTTP user name is **admin** and the password is the password you entered when creating the cluster.</span></span>

<span data-ttu-id="5cd36-183">Ambari 페이지로 이동하면 설치된 서비스가 페이지 왼쪽에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-183">When you arrive on the Ambari page, the installed services are listed on the left of the page.</span></span>

![설치된 서비스](./media/hdinsight-high-availability-linux/services.png)

<span data-ttu-id="5cd36-185">서비스 옆에 상태를 나타내는 여러 아이콘이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-185">There are a series of icons that may appear next to a service to indicate status.</span></span> <span data-ttu-id="5cd36-186">서비스와 관련된 모든 경고는 페이지 위쪽의 **Alert(경고)** 링크를 사용하여 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-186">Any alerts related to a service can be viewed using the **Alerts** link at the top of the page.</span></span> <span data-ttu-id="5cd36-187">각 서비스를 선택하여 해당 서비스에 대한 자세한 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-187">You can select each service to view more information on it.</span></span>

<span data-ttu-id="5cd36-188">서비스 페이지에서는 각 서비스의 상태 및 구성에 대한 정보를 제공하지만 서비스가 실행되고 있는 헤드 노드에 대한 정보는 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-188">While the service page provides information on the status and configuration of each service, it does not provide information on which head node the service is running on.</span></span> <span data-ttu-id="5cd36-189">이 정보를 보려면 페이지 위쪽의 **Hosts(호스트)** 링크를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="5cd36-189">To view this information, use the **Hosts** link at the top of the page.</span></span> <span data-ttu-id="5cd36-190">이 페이지에는 헤드 노드를 포함하여 클러스터 내의 호스트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-190">This page displays hosts within the cluster, including the head nodes.</span></span>

![호스트 목록](./media/hdinsight-high-availability-linux/hosts.png)

<span data-ttu-id="5cd36-192">헤드 노드 중 하나에 대한 링크를 선택하면 해당 노드에서 실행 중인 서비스와 구성 요소가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-192">Selecting the link for one of the head nodes displays the services and components running on that node.</span></span>

![구성 요소 상태](./media/hdinsight-high-availability-linux/nodeservices.png)

<span data-ttu-id="5cd36-194">Ambari 사용에 대한 자세한 내용은 [Ambari 웹 UI를 사용하여 HDInsight 모니터링 및 관리](hdinsight-hadoop-manage-ambari.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5cd36-194">For more information on using Ambari, see [Monitor and manage HDInsight using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

### <a name="ambari-rest-api"></a><span data-ttu-id="5cd36-195">Ambari REST API</span><span class="sxs-lookup"><span data-stu-id="5cd36-195">Ambari REST API</span></span>

<span data-ttu-id="5cd36-196">Ambari REST API는 인터넷을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-196">The Ambari REST API is available over the internet.</span></span> <span data-ttu-id="5cd36-197">HDInsight 공용 게이트웨이는 REST API를 현재 호스팅하는 헤드 노드에 라우팅 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-197">The HDInsight public gateway handles routing requests to the head node that is currently hosting the REST API.</span></span>

<span data-ttu-id="5cd36-198">다음 명령을 사용하여 Ambari REST API를 통해 서비스의 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-198">You can use the following command to check the state of a service through the Ambari REST API:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* <span data-ttu-id="5cd36-199">**PASSWORD**를 HTTP 사용자(관리자) 계정 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-199">Replace **PASSWORD** with the HTTP user (admin) account password.</span></span>
* <span data-ttu-id="5cd36-200">**CLUSTERNAME**은 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-200">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
* <span data-ttu-id="5cd36-201">**SERVICENAME**을 상태를 확인할 서비스의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-201">Replace **SERVICENAME** with the name of the service you want to check the status of.</span></span>

<span data-ttu-id="5cd36-202">예를 들어 **password** 암호를 사용하여 **mycluster**라는 클러스터의 **HDFS** 서비스 상태를 확인하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-202">For example, to check the status of the **HDFS** service on a cluster named **mycluster**, with a password of **password**, you would use the following command:</span></span>

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

<span data-ttu-id="5cd36-203">응답은 다음 JSON과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-203">The response is similar to the following JSON:</span></span>

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

<span data-ttu-id="5cd36-204">URL은 현재 서비스가 **hn0-CLUSTERNAME**라는 헤드 노드에서 실행되고 있음을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-204">The URL tells us that the service is currently running on a head node named **hn0-CLUSTERNAME**.</span></span>

<span data-ttu-id="5cd36-205">상태는 현재 서비스가 실행되고 있음( **STARTED**)을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-205">The state tells us that the service is currently running, or **STARTED**.</span></span>

<span data-ttu-id="5cd36-206">클러스터에 설치된 서비스를 모르는 경우 다음 명령을 사용하여 목록을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-206">If you do not know what services are installed on the cluster, you can use the following command to retrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

<span data-ttu-id="5cd36-207">Ambari REST API 작업에 대한 자세한 내용은 [Ambari REST API를 사용하여 HDInsight 모니터링 및 관리](hdinsight-hadoop-manage-ambari-rest-api.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5cd36-207">For more information on working with the Ambari REST API, see [Monitor and Manage HDInsight using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

#### <a name="service-components"></a><span data-ttu-id="5cd36-208">서비스 구성 요소</span><span class="sxs-lookup"><span data-stu-id="5cd36-208">Service components</span></span>

<span data-ttu-id="5cd36-209">서비스는 개별적으로 상태를 확인하려는 구성 요소를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-209">Services may contain components that you wish to check the status of individually.</span></span> <span data-ttu-id="5cd36-210">예를 들어 HDFS는 NameNode 구성 요소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-210">For example, HDFS contains the NameNode component.</span></span> <span data-ttu-id="5cd36-211">구성 요소에 대한 정보를 보려면 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-211">To view information on a component, the command would be:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

<span data-ttu-id="5cd36-212">서비스에서 제공하는 구성 요소를 모르는 경우 다음 명령을 사용하여 목록을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-212">If you do not know what components are provided by a service, you can use the following command to retrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-to-access-log-files-on-the-head-nodes"></a><span data-ttu-id="5cd36-213">헤드 노드의 로그 파일에 액세스하는 방법</span><span class="sxs-lookup"><span data-stu-id="5cd36-213">How to access log files on the head nodes</span></span>

### <a name="ssh"></a><span data-ttu-id="5cd36-214">SSH</span><span class="sxs-lookup"><span data-stu-id="5cd36-214">SSH</span></span>

<span data-ttu-id="5cd36-215">SSH를 통해 헤드 노드에 연결된 동안에는 **/var/log**에서 로그 파일을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-215">While connected to a head node through SSH, log files can be found under **/var/log**.</span></span> <span data-ttu-id="5cd36-216">예를 들어 **/var/log/hadoop-yarn/yarn** 은 YARN에 대한 로그를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-216">For example, **/var/log/hadoop-yarn/yarn** contain logs for YARN.</span></span>

<span data-ttu-id="5cd36-217">각 헤드 노드는 고유한 로그 항목을 포함할 수 있으므로 두 가지 다에서 로그를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-217">Each head node can have unique log entries, so you should check the logs on both.</span></span>

### <a name="sftp"></a><span data-ttu-id="5cd36-218">SFTP</span><span class="sxs-lookup"><span data-stu-id="5cd36-218">SFTP</span></span>

<span data-ttu-id="5cd36-219">또한 SSH 파일 전송 프로토콜 또는 SFTP(보안 파일 전송 프로토콜)을 사용하여 헤드 노드에 연결하고 로그 파일을 직접 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-219">You can also connect to the head node using the SSH File Transfer Protocol or Secure File Transfer Protocol (SFTP), and download the log files directly.</span></span>

<span data-ttu-id="5cd36-220">클러스터의 SSH 사용자 계정 이름 및 SSH 주소를 제공해야 하는 클러스터에 연결하는 경우 SSH 클라이언트를 사용하는 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-220">Similar to using an SSH client, when connecting to the cluster you must provide the SSH user account name and the SSH address of the cluster.</span></span> <span data-ttu-id="5cd36-221">예: `sftp username@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="5cd36-221">For example, `sftp username@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="5cd36-222">메시지가 표시되면 계정에 대한 암호를 제공하거나 `-i` 매개 변수를 사용하여 공개 키를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-222">Provide the password for the account when prompted, or provide a public key using the `-i` parameter.</span></span>

<span data-ttu-id="5cd36-223">연결되면 `sftp>` 프롬프트가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-223">Once connected, you are presented with a `sftp>` prompt.</span></span> <span data-ttu-id="5cd36-224">이 프롬프트에서 디렉터리를 변경하고 파일을 업로드 및 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-224">From this prompt, you can change directories, upload, and download files.</span></span> <span data-ttu-id="5cd36-225">예를 들어 다음 명령은 디렉터리를 **/var/log/hadoop/hdfs** 디렉터리고 변경하고 디렉터리에 있는 모든 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-225">For example, the following commands change directories to the **/var/log/hadoop/hdfs** directory and then download all files in the directory.</span></span>

    cd /var/log/hadoop/hdfs
    get *

<span data-ttu-id="5cd36-226">사용 가능한 명령 목록의 경우 `sftp>` 프롬프트에 `help`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-226">For a list of available commands, enter `help` at the `sftp>` prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="5cd36-227">또한 SFTP를 사용하여 연결하는 경우 파일 시스템을 시각화할 수 있는 그래픽 인터페이스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-227">There are also graphical interfaces that allow you to visualize the file system when connected using SFTP.</span></span> <span data-ttu-id="5cd36-228">예를 들어 [MobaXTerm](http://mobaxterm.mobatek.net/)을 사용하면 Windows 탐색기와 비슷한 인터페이스를 사용하는 파일 시스템을 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-228">For example, [MobaXTerm](http://mobaxterm.mobatek.net/) allows you to browse the file system using an interface similar to Windows Explorer.</span></span>

### <a name="ambari"></a><span data-ttu-id="5cd36-229">Ambari</span><span class="sxs-lookup"><span data-stu-id="5cd36-229">Ambari</span></span>

> [!NOTE]
> <span data-ttu-id="5cd36-230">Ambari를 사용하여 로그 파일에 액세스하려면 SSH 터널을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-230">To access log files using Ambari, you must use an SSH tunnel.</span></span> <span data-ttu-id="5cd36-231">개별 서비스의 웹 인터페이스는 인터넷에 공개적으로 노출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-231">The web interfaces for the individual services are not exposed publicly on the Internet.</span></span> <span data-ttu-id="5cd36-232">SSH 터널 사용에 대한 내용은 [SSH 터널 사용](hdinsight-linux-ambari-ssh-tunnel.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5cd36-232">For information on using an SSH tunnel, see the [Use SSH Tunneling](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="5cd36-233">Ambari 웹 UI에서 로그를 보려는 서비스(예: YARN)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-233">From the Ambari Web UI, select the service you wish to view logs for (for example, YARN).</span></span> <span data-ttu-id="5cd36-234">그런 다음 **빠른 링크**를 사용하여 로그를 볼 헤드 노드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-234">Then use **Quick Links** to select which head node to view the logs for.</span></span>

![빠른 연결을 사용하여 로그 보기](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-to-configure-the-node-size"></a><span data-ttu-id="5cd36-236">노드 크기를 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="5cd36-236">How to configure the node size</span></span>

<span data-ttu-id="5cd36-237">노드의 크기는 클러스터를 만드는 동안에만 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-237">The size of a node can only be selected during cluster creation.</span></span> <span data-ttu-id="5cd36-238">[HDInsight 가격 책정 페이지](https://azure.microsoft.com/pricing/details/hdinsight/)에서 HDInsight에 사용할 수 있는 다양한 VM 크기의 목록을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-238">You can find a list of the different VM sizes available for HDInsight on the [HDInsight pricing page](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="5cd36-239">클러스터를 만들 때 노드 크기를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-239">When creating a cluster, you can specify the size of the nodes.</span></span> <span data-ttu-id="5cd36-240">다음 정보는 [Azure Portal][preview-portal], [Azure PowerShell][azure-powershell] 및 [Azure CLI][azure-cli]를 사용하여 크기를 지정하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-240">The following information provides guidance on how to specify the size using the [Azure portal][preview-portal], [Azure PowerShell][azure-powershell], and the [Azure CLI][azure-cli]:</span></span>

* <span data-ttu-id="5cd36-241">**Azure Portal**: 클러스터를 만들 때 클러스터에서 사용하는 노드의 크기를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-241">**Azure portal**: When creating a cluster, you can set the size of the nodes used by the cluster:</span></span>

    ![노드 크기 선택이 포함된 클러스터 만들기 마법사의 이미지](./media/hdinsight-high-availability-linux/headnodesize.png)

* <span data-ttu-id="5cd36-243">**Azure CLI**: `azure hdinsight cluster create` 명령을 사용하는 경우 `--headNodeSize`, `--workerNodeSize` 및 `--zookeeperNodeSize` 매개 변수를 사용하여 헤드 노드의 크기, 작업자 및 ZooKeeper 노드를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-243">**Azure CLI**: When using the `azure hdinsight cluster create` command, you can set the size of the head, worker, and ZooKeeper nodes by using the `--headNodeSize`, `--workerNodeSize`, and `--zookeeperNodeSize` parameters.</span></span>

* <span data-ttu-id="5cd36-244">**Azure PowerShell**: `New-AzureRmHDInsightCluster` cmdlet을 사용하는 경우 `-HeadNodeVMSize`, `-WorkerNodeSize` 및 `-ZookeeperNodeSize` 매개 변수를 사용하여 헤드 노드의 크기, 작업자 및 ZooKeeper 노드를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd36-244">**Azure PowerShell**: When using the `New-AzureRmHDInsightCluster` cmdlet, you can set the size of the head, worker, and ZooKeeper nodes by using the `-HeadNodeVMSize`, `-WorkerNodeSize`, and `-ZookeeperNodeSize` parameters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5cd36-245">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5cd36-245">Next steps</span></span>

<span data-ttu-id="5cd36-246">이 문서에서 설명된 항목에 대해 자세히 알아보려면 다음 링크를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="5cd36-246">Use the following links to learn more about things mentioned in this document.</span></span>

* [<span data-ttu-id="5cd36-247">Ambari REST 참조</span><span class="sxs-lookup"><span data-stu-id="5cd36-247">Ambari REST Reference</span></span>](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [<span data-ttu-id="5cd36-248">Azure CLI 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="5cd36-248">Install and configure the Azure CLI</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="5cd36-249">Azure PowerShell 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="5cd36-249">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="5cd36-250">Ambari를 사용하여 HDInsight 관리</span><span class="sxs-lookup"><span data-stu-id="5cd36-250">Manage HDInsight using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="5cd36-251">Linux 기반 HDInsight 클러스터 프로비전을</span><span class="sxs-lookup"><span data-stu-id="5cd36-251">Provision Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
