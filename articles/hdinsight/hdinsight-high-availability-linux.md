---
title: "Hadoop-Azure HDInsight에 대 한 aaaHigh 가용성 | Microsoft Docs"
description: "HDInsight 클러스터에서 추가 헤드 노드를 사용하여 안정성과 가용성을 높이는 방법을 알아봅니다. 에 대해 알아봅니다 Ambari 하이브가 등의 Hadoop 서비스에 미치는 영향에 tooindividually SSH를 사용 하 여 tooeach 헤드 노드를 연결 하는 방식."
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
ms.openlocfilehash: 9ff62afe6b63b241cb984225233157219f8d7411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="b4d55-105">HDInsight에서 Hadoop 클러스터의 가용성 및 안정성</span><span class="sxs-lookup"><span data-stu-id="b4d55-105">Availability and reliability of Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="b4d55-106">HDInsight 클러스터에 두 개의 헤드 노드 tooincrease hello 가용성과 Hadoop 서비스와 실행 중인 작업의 안정성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-106">HDInsight clusters provide two head nodes tooincrease hello availability and reliability of Hadoop services and jobs running.</span></span>

<span data-ttu-id="b4d55-107">Hadoop은 클러스터의 여러 노드에서 서비스와 데이터를 복사하여 고가용성과 안정성을 달성합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-107">Hadoop achieves high availability and reliability by replicating services and data across multiple nodes in a cluster.</span></span> <span data-ttu-id="b4d55-108">그러나 Hadoop의 표준 배포에는 일반적으로 단일 헤드 노드만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-108">However standard distributions of Hadoop typically have only a single head node.</span></span> <span data-ttu-id="b4d55-109">모든 시간 동안 중단 hello 단일 헤드 노드는 hello 클러스터 toostop 작업을 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-109">Any outage of hello single head node can cause hello cluster toostop working.</span></span> <span data-ttu-id="b4d55-110">HDInsight 두 headnodes tooimprove Hadoop의 가용성 및 안정성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-110">HDInsight provides two headnodes tooimprove Hadoop's availability and reliability.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4d55-111">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b4d55-112">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4d55-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="availability-and-reliability-of-nodes"></a><span data-ttu-id="b4d55-113">노드의 가용성 및 안정성</span><span class="sxs-lookup"><span data-stu-id="b4d55-113">Availability and reliability of nodes</span></span>

<span data-ttu-id="b4d55-114">HDInsight 클러스터에 있는 노드는 Azure 가상 컴퓨터를 사용하여 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-114">Nodes in an HDInsight cluster are implemented using Azure Virtual Machines.</span></span> <span data-ttu-id="b4d55-115">hello 다음 섹션에서는 형식에 설명 hello 개별 노드 HDInsight 함께 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-115">hello following sections discuss hello individual node types used with HDInsight.</span></span> 

> [!NOTE]
> <span data-ttu-id="b4d55-116">일부 노드 유형은 클러스터 유형에 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-116">Not all node types are used for a cluster type.</span></span> <span data-ttu-id="b4d55-117">예를 들어 Hadoop 클러스터 유형에는 Nimbus 노드가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-117">For example, a Hadoop cluster type does not have any Nimbus nodes.</span></span> <span data-ttu-id="b4d55-118">HDInsight 클러스터 형식에서 사용 하는 노드에 대 한 자세한 내용은 hello의 hello 클러스터 유형 섹션을 참조 하십시오. [HDInsight 클러스터를 만드는 Linux 기반 Hadoop](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) 문서.</span><span class="sxs-lookup"><span data-stu-id="b4d55-118">For more information on nodes used by HDInsight cluster types, see hello Cluster types section of hello [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) document.</span></span>

### <a name="head-nodes"></a><span data-ttu-id="b4d55-119">헤드 노드</span><span class="sxs-lookup"><span data-stu-id="b4d55-119">Head nodes</span></span>

<span data-ttu-id="b4d55-120">HDInsight은 Hadoop 서비스의 고가용성을 tooensure, 두 헤드 노드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-120">tooensure high availability of Hadoop services, HDInsight provides two head nodes.</span></span> <span data-ttu-id="b4d55-121">두 헤드 노드가 모두 동시에 활성 상태이 고 hello HDInsight 클러스터 내에서 실행 중인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-121">Both head nodes are active and running within hello HDInsight cluster simultaneously.</span></span> <span data-ttu-id="b4d55-122">일부 서비스(예: HDFS 또는 YARN)는 항상 헤드 노드 하나에서만 '활성' 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-122">Some services, such as HDFS or YARN, are only 'active' on one head node at any given time.</span></span> <span data-ttu-id="b4d55-123">HiveServer2 또는 Hive MetaStore 같은 다른 서비스는 hello에서 헤드 노드 모두에서 활성 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-123">Other services such as HiveServer2 or Hive MetaStore are active on both head nodes at hello same time.</span></span>

<span data-ttu-id="b4d55-124">헤드 노드 (및 HDInsight의 다른 노드에) hello 노드의 hello hostname의 일환으로 숫자 값이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-124">Head nodes (and other nodes in HDInsight) have a numeric value as part of hello hostname of hello node.</span></span> <span data-ttu-id="b4d55-125">예를 들면 `hn0-CLUSTERNAME` 또는 `hn4-CLUSTERNAME`과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-125">For example, `hn0-CLUSTERNAME` or `hn4-CLUSTERNAME`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4d55-126">기본 또는 보조 노드 인지와 hello 숫자 값을 연결 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="b4d55-126">Do not associate hello numeric value with whether a node is primary or secondary.</span></span> <span data-ttu-id="b4d55-127">hello 숫자 값이 있는 tooprovide 각 노드에 대 한 고유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-127">hello numeric value is only present tooprovide a unique name for each node.</span></span>

### <a name="nimbus-nodes"></a><span data-ttu-id="b4d55-128">Nimbus 노드</span><span class="sxs-lookup"><span data-stu-id="b4d55-128">Nimbus Nodes</span></span>

<span data-ttu-id="b4d55-129">Nimbus 노드는 Storm 클러스터와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-129">Nimbus nodes are available with Storm clusters.</span></span> <span data-ttu-id="b4d55-130">hello Nimbus 노드를 배포 하 고 작업자 노드 간 처리를 모니터링 하 여 비슷한 기능 toohello Hadoop JobTracker를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-130">hello Nimbus nodes provide similar functionality toohello Hadoop JobTracker by distributing and monitoring processing across worker nodes.</span></span> <span data-ttu-id="b4d55-131">HDInsight는 Storm 클러스터에 두 개의 Nimbus 노드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-131">HDInsight provides two Nimbus nodes for Storm clusters</span></span>

### <a name="zookeeper-nodes"></a><span data-ttu-id="b4d55-132">Zookeeper 노드</span><span class="sxs-lookup"><span data-stu-id="b4d55-132">Zookeeper nodes</span></span>

<span data-ttu-id="b4d55-133">[ZooKeeper](http://zookeeper.apache.org/) 노드는 헤드 노드에서 마스터 서비스의 리더 선택에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-133">[ZooKeeper](http://zookeeper.apache.org/) nodes are used for leader election of master services on head nodes.</span></span> <span data-ttu-id="b4d55-134">사용 되는 tooinsure 서비스, 데이터 (작업자) 노드 및 게이트웨이 마스터 서비스에서 활성화 되어 있는 헤드 노드를 알고 있는 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-134">They are also used tooinsure that services, data (worker) nodes, and gateways know which head node a master service is active on.</span></span> <span data-ttu-id="b4d55-135">기본적으로 HDInsight는 3개의 ZooKeeper 노드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-135">By default, HDInsight provides three ZooKeeper nodes.</span></span>

### <a name="worker-nodes"></a><span data-ttu-id="b4d55-136">작업자 노드</span><span class="sxs-lookup"><span data-stu-id="b4d55-136">Worker nodes</span></span>

<span data-ttu-id="b4d55-137">작업자 노드는 작업을 제출 된 toohello 클러스터 hello 실제 데이터 분석을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-137">Worker nodes perform hello actual data analysis when a job is submitted toohello cluster.</span></span> <span data-ttu-id="b4d55-138">작업자 노드 실패 하면 수행 된 hello 작업은 제출 된 tooanother 작업자 노드입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-138">If a worker node fails, hello task that it was performing is submitted tooanother worker node.</span></span> <span data-ttu-id="b4d55-139">기본적으로 HDInsight는 네 개의 작업자 노드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-139">By default, HDInsight creates four worker nodes.</span></span> <span data-ttu-id="b4d55-140">및 클러스터를 만든 후 요구에 맞게가 숫자 toosuit을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-140">You can change this number toosuit your needs both during and after cluster creation.</span></span>

### <a name="edge-node"></a><span data-ttu-id="b4d55-141">에지 노드</span><span class="sxs-lookup"><span data-stu-id="b4d55-141">Edge node</span></span>

<span data-ttu-id="b4d55-142">가장자리 노드 hello 클러스터 내에서 분석 데이터에에서 적극적으로 참여 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-142">An edge node does not actively participate in data analysis within hello cluster.</span></span> <span data-ttu-id="b4d55-143">이는 개발자 또는 데이터 과학자가 Hadoop과 함께 작업하는 경우 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-143">It is used by developers or data scientists when working with Hadoop.</span></span> <span data-ttu-id="b4d55-144">hello 모서리 생활에서 노드 hello 클러스터의 다른 노드와 hello와 동일한 Azure 가상 네트워크를 hello 및 다른 모든 노드에서 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-144">hello edge node lives in hello same Azure Virtual Network as hello other nodes in hello cluster, and can directly access all other nodes.</span></span> <span data-ttu-id="b4d55-145">hello 가장자리 노드는 분석 작업 또는 중요 한 Hadoop 서비스 리소스를 차지 하지 않고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-145">hello edge node can be used without taking resources away from critical Hadoop services or analysis jobs.</span></span>

<span data-ttu-id="b4d55-146">현재 HDInsight에 R Server 가장자리 노드는 기본적으로 제공 하는 hello만 클러스터 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-146">Currently, R Server on HDInsight is hello only cluster type that provides an edge node by default.</span></span> <span data-ttu-id="b4d55-147">HDInsight의 R 서버용 hello 가장자리 노드 사용 되는 분산된 처리에 대 한 클러스터 toohello 제출 하기 전에 hello 노드에서 로컬로 테스트 R 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-147">For R Server on HDInsight, hello edge node is used test R code locally on hello node before submitting it toohello cluster for distributed processing.</span></span>

<span data-ttu-id="b4d55-148">가장자리 노드를 사용 하 여 R 서버가 아닌 다른 클러스터 형식에 대 한 내용은 hello 참조 [가장자리 노드를 사용 하 여 HDInsight의](hdinsight-apps-use-edge-node.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="b4d55-148">For information on using an edge node with cluster types other than R Server, see hello [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md) document.</span></span>

## <a name="accessing-hello-nodes"></a><span data-ttu-id="b4d55-149">Hello 노드에 액세스</span><span class="sxs-lookup"><span data-stu-id="b4d55-149">Accessing hello nodes</span></span>

<span data-ttu-id="b4d55-150">Hello 통해 액세스 toohello 클러스터 인터넷 공용 게이트웨이 통해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-150">Access toohello cluster over hello internet is provided through a public gateway.</span></span> <span data-ttu-id="b4d55-151">액세스 제한 tooconnecting toohello 헤드 노드에 사용 되며 (하는 경우 하나 존재) hello 가장자리 노드.</span><span class="sxs-lookup"><span data-stu-id="b4d55-151">Access is limited tooconnecting toohello head nodes and (if one exists) hello edge node.</span></span> <span data-ttu-id="b4d55-152">액세스 tooservices hello 헤드 노드에서 실행 하 여 여러 헤드 노드에 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-152">Access tooservices running on hello head nodes is not effected by having multiple head nodes.</span></span> <span data-ttu-id="b4d55-153">hello 공용 게이트웨이 경로 요청 toohello 헤드 노드 hello를 호스팅하는 서비스를 요청 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-153">hello public gateway routes requests toohello head node that hosts hello requested service.</span></span> <span data-ttu-id="b4d55-154">예를 들어 Ambari hello 보조 헤드 노드에서 현재 호스팅되면, hello 게이트웨이 Ambari toothat 노드에 대 한 들어오는 요청을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-154">For example, if Ambari is currently hosted on hello secondary head node, hello gateway routes incoming requests for Ambari toothat node.</span></span>

<span data-ttu-id="b4d55-155">Hello 공용 게이트웨이 통해 액세스가 제한 된 tooport 443 (HTTPS), 22, 및 23 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-155">Access over hello public gateway is limited tooport 443 (HTTPS), 22, and 23.</span></span>

* <span data-ttu-id="b4d55-156">포트 __443__ 사용 되는 tooaccess은 Ambari 오류 코드 및 기타 웹 UI 또는 hello 헤드 노드에 호스팅되는 REST Api입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-156">Port __443__ is used tooaccess Ambari and other web UI or REST APIs hosted on hello head nodes.</span></span>

* <span data-ttu-id="b4d55-157">포트 __22__ 가 사용 되는 tooaccess hello 기본 헤드 노드 또는 SSH 노드 가장자리입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-157">Port __22__ is used tooaccess hello primary head node or edge node with SSH.</span></span>

* <span data-ttu-id="b4d55-158">포트 __23__ 사용 되는 tooaccess hello 보조 헤드 노드의 SSH 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-158">Port __23__ is used tooaccess hello secondary head node with SSH.</span></span> <span data-ttu-id="b4d55-159">예를 들어 `ssh username@mycluster-ssh.azurehdinsight.net` toohello 기본 헤드 노드 라는 hello 클러스터의 연결 **mycluster**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-159">For example, `ssh username@mycluster-ssh.azurehdinsight.net` connects toohello primary head node of hello cluster named **mycluster**.</span></span>

<span data-ttu-id="b4d55-160">SSH를 사용 하 여에 대 한 자세한 내용은 참조 hello [SSH HDInsight를 사용](hdinsight-hadoop-linux-use-ssh-unix.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="b4d55-160">For more information on using SSH, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

### <a name="internal-fully-qualified-domain-names-fqdn"></a><span data-ttu-id="b4d55-161">내부 FQDN(정규화된 도메인 이름)</span><span class="sxs-lookup"><span data-stu-id="b4d55-161">Internal fully qualified domain names (FQDN)</span></span>

<span data-ttu-id="b4d55-162">HDInsight 클러스터의 노드 내부 IP 주소와 FQDN만 hello 클러스터에서 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-162">Nodes in an HDInsight cluster have an internal IP address and FQDN that can only be accessed from hello cluster.</span></span> <span data-ttu-id="b4d55-163">Hello 내부 FQDN 또는 IP 주소를 사용 하 여 hello 클러스터에서 서비스에 액세스할 때는 hello 서비스에 액세스할 때 Ambari tooverify hello IP 또는 FQDN toouse를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-163">When accessing services on hello cluster using hello internal FQDN or IP address, you should use Ambari tooverify hello IP or FQDN toouse when accessing hello service.</span></span>

<span data-ttu-id="b4d55-164">예를 들어, 헤드 노드 하나에서 서비스 에서만 실행할 수 Oozie hello 및 hello를 사용 하 여 `oozie` 대 한 SSH 세션에서 명령을 hello URL toohello 서비스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-164">For example, hello Oozie service can only run on one head node, and using hello `oozie` command from an SSH session requires hello URL toohello service.</span></span> <span data-ttu-id="b4d55-165">다음 명령을 hello를 사용 하 여 Ambari에서이 URL은 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-165">This URL can be retrieved from Ambari by using hello following command:</span></span>

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

<span data-ttu-id="b4d55-166">이 명령은 다음 hello 내부 URL toouse hello로 포함 된 명령을 값 비슷한 toohello 반환 `oozie` 명령:</span><span class="sxs-lookup"><span data-stu-id="b4d55-166">This command returns a value similar toohello following command, which contains hello internal URL toouse with hello `oozie` command:</span></span>

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

<span data-ttu-id="b4d55-167">Hello Ambari REST API를 사용한 작업에 대 한 자세한 내용은 참조 하십시오. [모니터 및 hello Ambari REST API를 사용 하 여 관리할 HDInsight](hdinsight-hadoop-manage-ambari-rest-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-167">For more information on working with hello Ambari REST API, see [Monitor and Manage HDInsight using hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

### <a name="accessing-other-node-types"></a><span data-ttu-id="b4d55-168">다른 노드 유형에 액세스</span><span class="sxs-lookup"><span data-stu-id="b4d55-168">Accessing other node types</span></span>

<span data-ttu-id="b4d55-169">액세스할 수 있는 조치 hello 다음 메서드를 사용 하 여 인터넷 hello 직접 않은 toonodes를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-169">You can connect toonodes that are not directly accessible over hello internet by using hello following methods:</span></span>

* <span data-ttu-id="b4d55-170">**SSH**: SSH를 사용 하 여 tooa 헤드 노드에 연결 되 면 hello 클러스터의 헤드 노드 tooconnect tooother 노드 hello에서에서 SSH를 사용 하 여 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-170">**SSH**: Once connected tooa head node using SSH, you can then use SSH from hello head node tooconnect tooother nodes in hello cluster.</span></span> <span data-ttu-id="b4d55-171">자세한 내용은 참조 hello [SSH HDInsight를 사용](hdinsight-hadoop-linux-use-ssh-unix.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="b4d55-171">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

* <span data-ttu-id="b4d55-172">**SSH 터널이**: toohello 노출 하지 않은 hello 노드 중 하나에서 호스팅되는 웹 서비스 tooaccess 해야 할 경우 인터넷에는 SSH 터널을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-172">**SSH Tunnel**: If you need tooaccess a web service hosted on one of hello nodes that is not exposed toohello internet, you must use an SSH tunnel.</span></span> <span data-ttu-id="b4d55-173">자세한 내용은 참조 hello [HDInsight와 SSH 터널을 사용 하 여](hdinsight-linux-ambari-ssh-tunnel.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="b4d55-173">For more information, see hello [Use an SSH tunnel with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

* <span data-ttu-id="b4d55-174">**Azure 가상 네트워크**: 경우 HDInsight 클러스터의 모든 리소스에 Azure 가상 네트워크의 일부인 hello 동일한 가상 네트워크 직접 액세스할 수 hello 클러스터의 모든 노드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-174">**Azure Virtual Network**: If your HDInsight cluster is part of an Azure Virtual Network, any resource on hello same Virtual Network can directly access all nodes in hello cluster.</span></span> <span data-ttu-id="b4d55-175">자세한 내용은 참조 hello [Azure 가상 네트워크를 사용 하 여 확장 HDInsight](hdinsight-extend-hadoop-virtual-network.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="b4d55-175">For more information, see hello [Extend HDInsight using Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

## <a name="how-toocheck-on-a-service-status"></a><span data-ttu-id="b4d55-176">어떻게 toocheck 서비스 상태에</span><span class="sxs-lookup"><span data-stu-id="b4d55-176">How toocheck on a service status</span></span>

<span data-ttu-id="b4d55-177">hello 헤드 노드에서 실행 되는 서비스의 toocheck hello 상태 hello Ambari 웹 UI를 사용 하 여 또는 Ambari REST API를 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-177">toocheck hello status of services that run on hello head nodes, use hello Ambari Web UI or hello Ambari REST API.</span></span>

### <a name="ambari-web-ui"></a><span data-ttu-id="b4d55-178">Ambari 웹 UI</span><span class="sxs-lookup"><span data-stu-id="b4d55-178">Ambari Web UI</span></span>

<span data-ttu-id="b4d55-179">hello Ambari 웹 UI https://CLUSTERNAME.azurehdinsight.net에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-179">hello Ambari Web UI is viewable at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="b4d55-180">대체 **CLUSTERNAME** 클러스터의 hello 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-180">Replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="b4d55-181">메시지가 표시 되 면 클러스터에 대 한 hello HTTP 사용자 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-181">If prompted, enter hello HTTP user credentials for your cluster.</span></span> <span data-ttu-id="b4d55-182">hello 기본 HTTP 사용자 이름은 **admin** hello 암호도 hello 클러스터를 만들 때 입력 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-182">hello default HTTP user name is **admin** and hello password is hello password you entered when creating hello cluster.</span></span>

<span data-ttu-id="b4d55-183">Hello Ambari 페이지에 도착 하면 hello 설치 된 서비스는 hello hello 페이지 왼쪽에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-183">When you arrive on hello Ambari page, hello installed services are listed on hello left of hello page.</span></span>

![설치된 서비스](./media/hdinsight-high-availability-linux/services.png)

<span data-ttu-id="b4d55-185">일련의 다음 tooa 서비스 tooindicate 상태 표시 될 수 있는 아이콘 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-185">There are a series of icons that may appear next tooa service tooindicate status.</span></span> <span data-ttu-id="b4d55-186">Tooa 서비스는 hello를 사용 하 여 볼 수 있습니다 하는 모든 경고와 관련 된 **경고** hello hello 페이지 맨 아래에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-186">Any alerts related tooa service can be viewed using hello **Alerts** link at hello top of hello page.</span></span> <span data-ttu-id="b4d55-187">자세한 내용은 각 서비스 tooview를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-187">You can select each service tooview more information on it.</span></span>

<span data-ttu-id="b4d55-188">Hello 서비스 페이지 hello 상태와 각 서비스의 구성 정보를 제공 하며, 헤드 노드 hello 서비스에서 실행 되는 정보를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-188">While hello service page provides information on hello status and configuration of each service, it does not provide information on which head node hello service is running on.</span></span> <span data-ttu-id="b4d55-189">tooview이 정보를 사용 하 여 hello **호스트** hello hello 페이지 맨 아래에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-189">tooview this information, use hello **Hosts** link at hello top of hello page.</span></span> <span data-ttu-id="b4d55-190">이 페이지는 hello 헤드 노드를 포함 하 여 hello 클러스터 내의 호스트를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-190">This page displays hosts within hello cluster, including hello head nodes.</span></span>

![호스트 목록](./media/hdinsight-high-availability-linux/hosts.png)

<span data-ttu-id="b4d55-192">Hello 헤드 노드 중 하나에 대 한 hello 링크를 선택 하는 hello 서비스와 해당 노드에서 실행 되는 구성 요소를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-192">Selecting hello link for one of hello head nodes displays hello services and components running on that node.</span></span>

![구성 요소 상태](./media/hdinsight-high-availability-linux/nodeservices.png)

<span data-ttu-id="b4d55-194">Ambari를 사용 하 여에 대 한 자세한 내용은 참조 하십시오. [모니터 HDInsight hello Ambari 웹 UI를 사용 하 여 관리 및](hdinsight-hadoop-manage-ambari.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-194">For more information on using Ambari, see [Monitor and manage HDInsight using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

### <a name="ambari-rest-api"></a><span data-ttu-id="b4d55-195">Ambari REST API</span><span class="sxs-lookup"><span data-stu-id="b4d55-195">Ambari REST API</span></span>

<span data-ttu-id="b4d55-196">hello Ambari REST API는 hello를 통해 사용할 수 있는 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-196">hello Ambari REST API is available over hello internet.</span></span> <span data-ttu-id="b4d55-197">hello HDInsight 공용 게이트웨이 라우팅 요청 toohello 헤드 노드 hello REST API를 현재 호스팅 중인를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-197">hello HDInsight public gateway handles routing requests toohello head node that is currently hosting hello REST API.</span></span>

<span data-ttu-id="b4d55-198">다음 명령 toocheck hello 상태 hello Ambari REST API를 통해 서비스의 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-198">You can use hello following command toocheck hello state of a service through hello Ambari REST API:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* <span data-ttu-id="b4d55-199">대체 **암호** hello HTTP 사용자 (관리자) 계정 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-199">Replace **PASSWORD** with hello HTTP user (admin) account password.</span></span>
* <span data-ttu-id="b4d55-200">대체 **CLUSTERNAME** hello 클러스터의 hello 이름을 가진 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-200">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
* <span data-ttu-id="b4d55-201">대체 **SERVICENAME** toocheck hello 상태의 hello 서비스의 hello 이름의 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-201">Replace **SERVICENAME** with hello name of hello service you want toocheck hello status of.</span></span>

<span data-ttu-id="b4d55-202">예를 들어 toocheck hello 상태의 hello **HDFS** 서비스 라는 클러스터에 **mycluster**, 암호는 **암호**, hello 다음 명령을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="b4d55-202">For example, toocheck hello status of hello **HDFS** service on a cluster named **mycluster**, with a password of **password**, you would use hello following command:</span></span>

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

<span data-ttu-id="b4d55-203">hello 응답은 JSON 다음 유사한 toohello입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-203">hello response is similar toohello following JSON:</span></span>

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

<span data-ttu-id="b4d55-204">hello URL 알려줍니다. 명명 된 헤드 노드에서 hello 서비스가 실행 중이 **hn0 CLUSTERNAME**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-204">hello URL tells us that hello service is currently running on a head node named **hn0-CLUSTERNAME**.</span></span>

<span data-ttu-id="b4d55-205">hello 상태를 알려줍니다. hello 서비스를 현재 실행 중인지 또는 **STARTED**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-205">hello state tells us that hello service is currently running, or **STARTED**.</span></span>

<span data-ttu-id="b4d55-206">Hello 클러스터에 설치 하는 서비스 잘 모르는 경우에 hello tooretrieve 명령 목록을 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-206">If you do not know what services are installed on hello cluster, you can use hello following command tooretrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

<span data-ttu-id="b4d55-207">Hello Ambari REST API를 사용한 작업에 대 한 자세한 내용은 참조 하십시오. [모니터 및 hello Ambari REST API를 사용 하 여 관리할 HDInsight](hdinsight-hadoop-manage-ambari-rest-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-207">For more information on working with hello Ambari REST API, see [Monitor and Manage HDInsight using hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

#### <a name="service-components"></a><span data-ttu-id="b4d55-208">서비스 구성 요소</span><span class="sxs-lookup"><span data-stu-id="b4d55-208">Service components</span></span>

<span data-ttu-id="b4d55-209">서비스의 toocheck hello 상태를 개별적으로 원하는 구성 요소를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-209">Services may contain components that you wish toocheck hello status of individually.</span></span> <span data-ttu-id="b4d55-210">예를 들어 HDFS hello NameNode 구성 요소를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-210">For example, HDFS contains hello NameNode component.</span></span> <span data-ttu-id="b4d55-211">구성 요소에 대 한 tooview 내용은 hello 명령이 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-211">tooview information on a component, hello command would be:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

<span data-ttu-id="b4d55-212">구성 요소는 서비스에서 제공 잘 모르는 경우에 hello tooretrieve 명령 목록을 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-212">If you do not know what components are provided by a service, you can use hello following command tooretrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-tooaccess-log-files-on-hello-head-nodes"></a><span data-ttu-id="b4d55-213">Tooaccess는 hello 헤드 노드에서 파일을 로그 하는 방법은</span><span class="sxs-lookup"><span data-stu-id="b4d55-213">How tooaccess log files on hello head nodes</span></span>

### <a name="ssh"></a><span data-ttu-id="b4d55-214">SSH</span><span class="sxs-lookup"><span data-stu-id="b4d55-214">SSH</span></span>

<span data-ttu-id="b4d55-215">SSH 통해 연결 된 tooa 헤드 노드는 동안 로그 파일을 찾을 수에서 **/var/로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-215">While connected tooa head node through SSH, log files can be found under **/var/log**.</span></span> <span data-ttu-id="b4d55-216">예를 들어 **/var/log/hadoop-yarn/yarn** 은 YARN에 대한 로그를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-216">For example, **/var/log/hadoop-yarn/yarn** contain logs for YARN.</span></span>

<span data-ttu-id="b4d55-217">각 헤드 노드 hello 모두에 로그를 확인 해야 하므로 고유한 로그 항목에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-217">Each head node can have unique log entries, so you should check hello logs on both.</span></span>

### <a name="sftp"></a><span data-ttu-id="b4d55-218">SFTP</span><span class="sxs-lookup"><span data-stu-id="b4d55-218">SFTP</span></span>

<span data-ttu-id="b4d55-219">파일 전송 프로토콜 SFTP (보안), 또는 hello SSH 파일 전송 프로토콜을 사용 하 여 toohello 헤드 노드를 연결 하 고 hello 로그 파일을 직접 다운로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-219">You can also connect toohello head node using hello SSH File Transfer Protocol or Secure File Transfer Protocol (SFTP), and download hello log files directly.</span></span>

<span data-ttu-id="b4d55-220">비슷한 toousing SSH 클라이언트를 제공 해야 toohello 클러스터를 연결할 때 SSH 사용자 계정 이름 및 hello SSH 주소 hello 클러스터의 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-220">Similar toousing an SSH client, when connecting toohello cluster you must provide hello SSH user account name and hello SSH address of hello cluster.</span></span> <span data-ttu-id="b4d55-221">예: `sftp username@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="b4d55-221">For example, `sftp username@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="b4d55-222">메시지가 표시 되 면 hello 계정에 대 한 hello 암호를 제공 하거나 hello를 사용 하 여 공개 키 제공 `-i` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-222">Provide hello password for hello account when prompted, or provide a public key using hello `-i` parameter.</span></span>

<span data-ttu-id="b4d55-223">연결되면 `sftp>` 프롬프트가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-223">Once connected, you are presented with a `sftp>` prompt.</span></span> <span data-ttu-id="b4d55-224">이 프롬프트에서 디렉터리를 변경하고 파일을 업로드 및 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-224">From this prompt, you can change directories, upload, and download files.</span></span> <span data-ttu-id="b4d55-225">다음 명령을 hello 디렉터리 toohello를 변경 하는 예를 들어 **/var/log/hadoop/hdfs** 디렉터리와 hello 디렉터리의 모든 파일 다음 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-225">For example, hello following commands change directories toohello **/var/log/hadoop/hdfs** directory and then download all files in hello directory.</span></span>

    cd /var/log/hadoop/hdfs
    get *

<span data-ttu-id="b4d55-226">사용할 수 있는 명령 목록에 대 한 입력 `help` hello에 `sftp>` 프롬프트입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-226">For a list of available commands, enter `help` at hello `sftp>` prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="b4d55-227">SFTP를 사용 하 여 연결 하는 경우 toovisualize hello 파일 시스템을 수 있는 그래픽 인터페이스도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-227">There are also graphical interfaces that allow you toovisualize hello file system when connected using SFTP.</span></span> <span data-ttu-id="b4d55-228">예를 들어 [MobaXTerm](http://mobaxterm.mobatek.net/) toobrowse hello 파일 시스템 인터페이스 비슷한 tooWindows 탐색기를 사용 하 여 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-228">For example, [MobaXTerm](http://mobaxterm.mobatek.net/) allows you toobrowse hello file system using an interface similar tooWindows Explorer.</span></span>

### <a name="ambari"></a><span data-ttu-id="b4d55-229">Ambari</span><span class="sxs-lookup"><span data-stu-id="b4d55-229">Ambari</span></span>

> [!NOTE]
> <span data-ttu-id="b4d55-230">tooaccess 로그 Ambari를 사용 하 여 파일, SSH 터널을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-230">tooaccess log files using Ambari, you must use an SSH tunnel.</span></span> <span data-ttu-id="b4d55-231">hello 개별 서비스에 대 한 hello 웹 인터페이스 hello 인터넷에서 공개적으로 노출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-231">hello web interfaces for hello individual services are not exposed publicly on hello Internet.</span></span> <span data-ttu-id="b4d55-232">SSH 터널을 사용 하는 방법은 참조 hello [사용 하 여 SSH 터널링](hdinsight-linux-ambari-ssh-tunnel.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="b4d55-232">For information on using an SSH tunnel, see hello [Use SSH Tunneling](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="b4d55-233">Hello Ambari 웹 UI에서에서 tooview 로그 (예를 들어 YARN)에 대 한 원하는 hello 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-233">From hello Ambari Web UI, select hello service you wish tooview logs for (for example, YARN).</span></span> <span data-ttu-id="b4d55-234">다음 사용 하 여 **빠른 링크** tooselect는 헤드 노드 tooview hello에 대 한 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-234">Then use **Quick Links** tooselect which head node tooview hello logs for.</span></span>

![Tooview 로그 링크 빠른을 사용 하 여](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-tooconfigure-hello-node-size"></a><span data-ttu-id="b4d55-236">Tooconfigure 노드 크기를 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="b4d55-236">How tooconfigure hello node size</span></span>

<span data-ttu-id="b4d55-237">hello 크기 노드 클러스터를 만드는 동안만 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-237">hello size of a node can only be selected during cluster creation.</span></span> <span data-ttu-id="b4d55-238">찾을 수 있습니다 hello 목록을 사용할 수 있는 다른 VM 크기 HDInsight에 대 한 hello [HDInsight 가격 책정 페이지](https://azure.microsoft.com/pricing/details/hdinsight/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-238">You can find a list of hello different VM sizes available for HDInsight on hello [HDInsight pricing page](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="b4d55-239">클러스터를 만들 때는 hello 노드의 hello 크기를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-239">When creating a cluster, you can specify hello size of hello nodes.</span></span> <span data-ttu-id="b4d55-240">hello 다음 정보에 지침을 제공 방법을 사용 하 여 toospecify hello 크기 hello [Azure 포털][preview-portal], [Azure PowerShell][azure-powershell], hello 및 [Azure CLI][azure-cli]:</span><span class="sxs-lookup"><span data-stu-id="b4d55-240">hello following information provides guidance on how toospecify hello size using hello [Azure portal][preview-portal], [Azure PowerShell][azure-powershell], and hello [Azure CLI][azure-cli]:</span></span>

* <span data-ttu-id="b4d55-241">**Azure 포털**: hello 클러스터에서 사용 하는 hello 노드의 hello 크기는 클러스터를 만들 때 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-241">**Azure portal**: When creating a cluster, you can set hello size of hello nodes used by hello cluster:</span></span>

    ![노드 크기 선택이 포함된 클러스터 만들기 마법사의 이미지](./media/hdinsight-high-availability-linux/headnodesize.png)

* <span data-ttu-id="b4d55-243">**Azure CLI**: hello를 사용 하는 경우 `azure hdinsight cluster create` 명령을 hello를 사용 하 여 hello h e a d, 작업자 및 사육 노드의 hello 크기를 설정할 수 있습니다 `--headNodeSize`, `--workerNodeSize`, 및 `--zookeeperNodeSize` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-243">**Azure CLI**: When using hello `azure hdinsight cluster create` command, you can set hello size of hello head, worker, and ZooKeeper nodes by using hello `--headNodeSize`, `--workerNodeSize`, and `--zookeeperNodeSize` parameters.</span></span>

* <span data-ttu-id="b4d55-244">**Azure PowerShell**: hello를 사용 하는 경우 `New-AzureRmHDInsightCluster` cmdlet hello를 사용 하 여 hello h e a d, 작업자 및 사육 노드의 hello 크기를 설정할 수 있습니다 `-HeadNodeVMSize`, `-WorkerNodeSize`, 및 `-ZookeeperNodeSize` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-244">**Azure PowerShell**: When using hello `New-AzureRmHDInsightCluster` cmdlet, you can set hello size of hello head, worker, and ZooKeeper nodes by using hello `-HeadNodeVMSize`, `-WorkerNodeSize`, and `-ZookeeperNodeSize` parameters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4d55-245">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b4d55-245">Next steps</span></span>

<span data-ttu-id="b4d55-246">이 문서에 설명 된 항목에 대 한 자세한 링크 toolearn 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-246">Use hello following links toolearn more about things mentioned in this document.</span></span>

* [<span data-ttu-id="b4d55-247">Ambari REST 참조</span><span class="sxs-lookup"><span data-stu-id="b4d55-247">Ambari REST Reference</span></span>](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [<span data-ttu-id="b4d55-248">설치 하 고 hello Azure CLI를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d55-248">Install and configure hello Azure CLI</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="b4d55-249">Azure PowerShell 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="b4d55-249">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="b4d55-250">Ambari를 사용하여 HDInsight 관리</span><span class="sxs-lookup"><span data-stu-id="b4d55-250">Manage HDInsight using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="b4d55-251">Linux 기반 HDInsight 클러스터 프로비전을</span><span class="sxs-lookup"><span data-stu-id="b4d55-251">Provision Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
