---
title: "가상 네트워크-Azure 내에서 HBase 클러스터 복제 aaaConfigure | Microsoft Docs"
description: "자세한 내용은 어떻게 부하 분산, 고가용성, 0-가동 중지 시간 마이그레이션/업데이트에서 하나의 HDInsight 버전 tooanother 및 재해 복구에 대 한 tooconfigure HBase 복제 합니다."
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ba1c44f26b7cbf4a7a88159b12b3e064ea9f9a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a><span data-ttu-id="94421-103">가상 네트워크 내에서 HBase 클러스터 복제 구성</span><span class="sxs-lookup"><span data-stu-id="94421-103">Configure HBase cluster replication within virtual networks</span></span>

<span data-ttu-id="94421-104">자세한 방법을 하나의 가상 네트워크 (VNet) 내에서 또는 두 개의 가상 네트워크 간에 tooconfigure HBase 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-104">Learn how tooconfigure HBase replication within one virtual network (VNet) or between two virtual networks.</span></span>

<span data-ttu-id="94421-105">클러스터 복제에서는 원본-푸시 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-105">Cluster replication uses a source-push methodology.</span></span> <span data-ttu-id="94421-106">HBase 클러스터는 원본 또는 대상이 될 수도 있고, 한 번에 두 가지 역할을 모두 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94421-106">An HBase cluster can be a source or a destination, or it can fulfill both roles at once.</span></span> <span data-ttu-id="94421-107">복제는 비동기적 이며 및 hello 복제 ´ ֲ 결과적 일관성.</span><span class="sxs-lookup"><span data-stu-id="94421-107">Replication is asynchronous, and hello goal of replication is eventual consistency.</span></span> <span data-ttu-id="94421-108">Hello 소스 편집 tooa 열 제품군 사용 하도록 설정 하는 복제를 받을 때 편집은 전파 tooall 대상 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="94421-108">When hello source receives an edit tooa column family with replication enabled, that edit is propagated tooall destination clusters.</span></span> <span data-ttu-id="94421-109">하나의 클러스터 tooanother에서 데이터가 복제 되므로 hello 원본 클러스터와 hello 데이터 이미 있는 모든 클러스터 추적된 tooprevent 복제 루프 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94421-109">When data is replicated from one cluster tooanother, hello source cluster and all clusters that have already consumed hello data are tracked tooprevent replication loops.</span></span>

<span data-ttu-id="94421-110">이 자습서에서는 원본-대상 복제를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-110">In this tutorial, you will configure a source-destination replication.</span></span> <span data-ttu-id="94421-111">다른 클러스터 토폴로지는 [Apache HBase 참조 가이드](http://hbase.apache.org/book.html#_cluster_replication)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="94421-111">For other cluster topologies, see [Apache HBase Reference Guide](http://hbase.apache.org/book.html#_cluster_replication).</span></span>

<span data-ttu-id="94421-112">단일 가상 네트워크에 대한 HBase 복제 사용 사례:</span><span class="sxs-lookup"><span data-stu-id="94421-112">HBase replication usage cases for a single virtual network:</span></span>

* <span data-ttu-id="94421-113">부하 분산-예를 들어 검색 또는 MapReduce 작업 hello 대상 클러스터에서 실행 중 이며 hello 원본 클러스터에서 데이터를 수집 하는 방법</span><span class="sxs-lookup"><span data-stu-id="94421-113">Load balancing--for example, running scans or MapReduce jobs on hello destination cluster and ingesting data on hello source cluster</span></span>
* <span data-ttu-id="94421-114">고가용성</span><span class="sxs-lookup"><span data-stu-id="94421-114">High availability</span></span>
* <span data-ttu-id="94421-115">하나의 HBase 클러스터 tooanother에서 데이터 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="94421-115">Migrating data from one HBase cluster tooanother</span></span>
* <span data-ttu-id="94421-116">한 버전 tooanother에서 Azure HDInsight 클러스터를 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-116">Upgrading an Azure HDInsight cluster from one version tooanother</span></span>

<span data-ttu-id="94421-117">두 가상 네트워크에 대한 HBase 복제 사용 사례:</span><span class="sxs-lookup"><span data-stu-id="94421-117">HBase replication usage cases for two virtual networks:</span></span>

* <span data-ttu-id="94421-118">재해 복구</span><span class="sxs-lookup"><span data-stu-id="94421-118">Disaster recovery</span></span>
* <span data-ttu-id="94421-119">부하 분산 및 분할 hello 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="94421-119">Load balancing and partitioning hello application</span></span>
* <span data-ttu-id="94421-120">고가용성</span><span class="sxs-lookup"><span data-stu-id="94421-120">High availability</span></span>

<span data-ttu-id="94421-121">[GitHub](https://github.com/Azure/hbase-utils/tree/master/replication)에 있는 [스크립트 동작](hdinsight-hadoop-customize-cluster-linux.md) 스크립트를 사용하여 클러스터를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-121">You replicate clusters by using [script action](hdinsight-hadoop-customize-cluster-linux.md) scripts located at [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94421-122">필수 조건</span><span class="sxs-lookup"><span data-stu-id="94421-122">Prerequisites</span></span>
<span data-ttu-id="94421-123">이 자습서를 시작하기 전에 Azure 구독이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-123">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="94421-124">[Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="94421-124">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="configure-hello-environments"></a><span data-ttu-id="94421-125">Hello 환경 구성</span><span class="sxs-lookup"><span data-stu-id="94421-125">Configure hello environments</span></span>

<span data-ttu-id="94421-126">다음과 같이 세 가지 가능한 구성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94421-126">There are three possible configurations:</span></span>

- <span data-ttu-id="94421-127">1개 Azure 가상 네트워크에 2개 HBase 클러스터 구성</span><span class="sxs-lookup"><span data-stu-id="94421-127">Two HBase clusters in one Azure virtual network</span></span>
- <span data-ttu-id="94421-128">서로 다른 두 개의 가상 네트워크에 두 개의 HBase 클러스터 hello 동일한 지역</span><span class="sxs-lookup"><span data-stu-id="94421-128">Two HBase clusters in two different virtual networks in hello same region</span></span>
- <span data-ttu-id="94421-129">별도의 2개 지역에 있는 2개 다른 가상 네트워크에 2개 HBase 클러스터 구성(지리적 복제)</span><span class="sxs-lookup"><span data-stu-id="94421-129">Two HBase clusters in two different virtual networks in two different regions (geo-replication)</span></span>

<span data-ttu-id="94421-130">toomake 것 보다 쉽게 tooconfigure hello 환경에서 만든 일부 [Azure 리소스 관리자 템플릿을](../azure-resource-manager/resource-group-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-130">toomake it easier tooconfigure hello environments, we have created some [Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="94421-131">다른 방법을 사용 하 여 tooconfigure hello 환경을 선호 하는 경우 참조:</span><span class="sxs-lookup"><span data-stu-id="94421-131">If you prefer tooconfigure hello environments by using other methods, see:</span></span>

- [<span data-ttu-id="94421-132">HDInsight에서 Linux 기반 Hadoop 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="94421-132">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
- [<span data-ttu-id="94421-133">Azure Virtual Network에 HBase 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="94421-133">Create HBase clusters in Azure Virtual Network</span></span>](hdinsight-hbase-provision-vnet.md)

### <a name="configure-one-virtual-network"></a><span data-ttu-id="94421-134">1개 가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="94421-134">Configure one virtual network</span></span>

<span data-ttu-id="94421-135">Hello 다음 hello에 이미지 toocreate 두 HBase 클러스터를 클릭 합니다. 동일한 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="94421-135">Click hello following image toocreate two HBase clusters in hello same virtual network.</span></span> <span data-ttu-id="94421-136">hello 서식 파일에 저장 된 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/)합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-136">hello template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

### <a name="configure-two-virtual-networks-in-hello-same-region"></a><span data-ttu-id="94421-137">Hello에 두 개의 가상 네트워크를 구성 합니다. 동일한 지역</span><span class="sxs-lookup"><span data-stu-id="94421-137">Configure two virtual networks in hello same region</span></span>

<span data-ttu-id="94421-138">다음 이미지 toocreate 두 가상 네트워크 VNet 피어 링 및 두 개의 HBase 클러스터 hello에서 사용 하 여 hello를 클릭 합니다. 동일한 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="94421-138">Click hello following image toocreate two virtual networks with VNet peering and two HBase clusters in hello same region.</span></span> <span data-ttu-id="94421-139">hello 서식 파일에 저장 된 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/)합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-139">hello template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>



<span data-ttu-id="94421-140">이 시나리오에는 [VNet 피어링](../virtual-network/virtual-network-peering-overview.md)이 필요하며,</span><span class="sxs-lookup"><span data-stu-id="94421-140">This scenario requires [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> <span data-ttu-id="94421-141">hello 템플릿 VNet 피어 링 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94421-141">hello template enables VNet peering.</span></span>   

<span data-ttu-id="94421-142">HBase 복제 hello 사육 Vm의 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-142">HBase replication uses IP addresses of hello ZooKeeper VMs.</span></span> <span data-ttu-id="94421-143">Hello 대상 HBase 사육 노드에 대 한 고정 IP 주소를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-143">You must configure static IP addresses for hello destination HBase ZooKeeper nodes.</span></span>

<span data-ttu-id="94421-144">**tooconfigure 고정 IP 주소**</span><span class="sxs-lookup"><span data-stu-id="94421-144">**tooconfigure static IP addresses**</span></span>

1. <span data-ttu-id="94421-145">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-145">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="94421-146">Hello 왼쪽된 메뉴에서 클릭 **리소스 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-146">From hello left menu, click **Resource Groups**.</span></span>
3. <span data-ttu-id="94421-147">Hello 대상 HBase 클러스터를 포함 하 여 리소스 그룹을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-147">Click your resource group that contains hello destination HBase cluster.</span></span> <span data-ttu-id="94421-148">리소스 관리자 템플릿 toocreate hello 환경 hello를 사용 하는 때를 지정 하는 hello 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="94421-148">This is hello resource group that you specified when you used hello Resource Manager template toocreate hello environment.</span></span> <span data-ttu-id="94421-149">Hello 목록 아래로 hello 필터 toonarrow를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94421-149">You can use hello filter toonarrow down hello list.</span></span> <span data-ttu-id="94421-150">Hello 두 가상 네트워크를 포함 하는 리소스의 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94421-150">You can see a list of resources that contains hello two virtual networks.</span></span>
4. <span data-ttu-id="94421-151">Hello 대상 HBase 클러스터를 포함 하는 hello 가상 네트워크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-151">Click hello virtual network that contains hello destination HBase cluster.</span></span> <span data-ttu-id="94421-152">예를 들어 **xxxx-vnet2**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-152">For example, click **xxxx-vnet2**.</span></span> <span data-ttu-id="94421-153">**nic-zookeepermode-**로 시작하는 이름을 가진 세 개의 장치를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94421-153">You can see three devices with names that start with **nic-zookeepermode-**.</span></span> <span data-ttu-id="94421-154">이러한 장치는 hello 3 사육 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="94421-154">Those devices are hello three ZooKeeper VMs.</span></span>
5. <span data-ttu-id="94421-155">Hello 사육 Vm 중 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-155">Click one of hello ZooKeeper VMs.</span></span>
6. <span data-ttu-id="94421-156">**IP 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-156">Click **IP configurations**.</span></span>
7. <span data-ttu-id="94421-157">클릭 **ipConfig1** hello 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-157">Click **ipConfig1** from hello list.</span></span>
8. <span data-ttu-id="94421-158">클릭 **정적**, hello 실제 IP 주소를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="94421-158">Click **Static**, and write down hello actual IP address.</span></span> <span data-ttu-id="94421-159">Hello 스크립트 동작 tooenable 복제를 실행할 때 hello IP 주소가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-159">You will need hello IP address when you run hello script action tooenable replication.</span></span>

  ![HDInsight HBase 복제 ZooKeeper 고정 IP](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. <span data-ttu-id="94421-161">다른 두 사육 노드 hello에 대 한 단계 6 tooset hello 고정 IP 주소를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-161">Repeat step 6 tooset hello static IP address for hello other two ZooKeeper nodes.</span></span>

<span data-ttu-id="94421-162">Hello VNet 간 시나리오에 대 한 hello를 사용 해야 **ip** hello를 호출할 때 전환 **hdi_enable_replication.sh** 작업을 스크립팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-162">For hello cross-VNet scenario, you must use hello **-ip** switch when calling hello **hdi_enable_replication.sh** script action.</span></span>

### <a name="configure-two-virtual-networks-in-two-different-regions"></a><span data-ttu-id="94421-163">별도의 2개 지역에 2개 가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="94421-163">Configure two virtual networks in two different regions</span></span>

<span data-ttu-id="94421-164">다음 이미지 toocreate 두 가상 네트워크에 두 개의 서로 다른 지역 hello를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-164">Click hello following image toocreate two virtual networks in two different regions.</span></span> <span data-ttu-id="94421-165">hello 템플릿은 공용 Azure Blob 컨테이너에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94421-165">hello template is stored in a public Azure Blob container.</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

<span data-ttu-id="94421-166">Hello 두 가상 네트워크 간의 VPN 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94421-166">Create a VPN gateway between hello two virtual networks.</span></span> <span data-ttu-id="94421-167">지침은 [사이트 간 연결로 VNet 만들기](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="94421-167">For instructions, see [Create a VNet with a site-to-site connection](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span></span>

<span data-ttu-id="94421-168">HBase 복제 hello 사육 Vm의 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-168">HBase replication uses IP addresses of hello ZooKeeper VMs.</span></span> <span data-ttu-id="94421-169">Hello 대상 HBase 사육 노드에 대 한 고정 IP 주소를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-169">You must configure static IP addresses for hello destination HBase ZooKeeper nodes.</span></span> <span data-ttu-id="94421-170">tooconfigure 고정 IP이 문서의 hello "에서 구성 두 가상 네트워크는 동일한 지역 hello" 섹션을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="94421-170">tooconfigure static IP, see hello "Configure two virtual networks in hello same region" section in this article.</span></span>

<span data-ttu-id="94421-171">Hello VNet 간 시나리오에 대 한 hello를 사용 해야 **ip** hello를 호출할 때 전환 **hdi_enable_replication.sh** 작업을 스크립팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-171">For hello cross-VNet scenario, you must use hello **-ip** switch when calling hello **hdi_enable_replication.sh** script action.</span></span>

## <a name="load-test-data"></a><span data-ttu-id="94421-172">테스트 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="94421-172">Load test data</span></span>

<span data-ttu-id="94421-173">클러스터를 복제 하면 테이블 tooreplicate hello를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-173">When you replicate a cluster, you must specify hello tables tooreplicate.</span></span> <span data-ttu-id="94421-174">이 섹션에서는 hello 원본 클러스터로 일부 데이터를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-174">In this section, you will load some data into hello source cluster.</span></span> <span data-ttu-id="94421-175">다음 섹션인 hello hello 두 클러스터 간 복제를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-175">In hello next section, you will enable replication between hello two clusters.</span></span>

<span data-ttu-id="94421-176">Hello 지침에 따라 [HBase 자습서: HDInsight에서 Linux 기반 Hadoop으로 HBase Apache를 사용 하 여 시작](hdinsight-hbase-tutorial-get-started-linux.md) toocreate는 **연락처** 테이블 및 일부 데이터 hello 테이블에 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-176">Follow hello instructions in [HBase tutorial: Get started using Apache HBase with Linux-based Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) toocreate a **Contacts** table and insert some data into hello table.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="94421-177">복제 활성화</span><span class="sxs-lookup"><span data-stu-id="94421-177">Enable replication</span></span>

<span data-ttu-id="94421-178">단계를 수행 하는 hello toocall hello Azure 포털에서에서 스크립트 동작 스크립트 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="94421-178">hello following steps show how toocall hello script action script from hello Azure portal.</span></span> <span data-ttu-id="94421-179">Azure PowerShell을 hello Azure CLI (명령줄 인터페이스)를 사용 하 여 스크립트 작업을 실행 하는 것에 대 한 참조 [스크립트 동작을 사용 하 여 사용자 지정 하는 Linux 기반 HDInsight 클러스터](hdinsight-hadoop-customize-cluster-linux.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-179">For running a script action by using Azure PowerShell and hello Azure command-line interface (CLI), see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="94421-180">**hello Azure 포털에서에서 tooenable HBase 복제**</span><span class="sxs-lookup"><span data-stu-id="94421-180">**tooenable HBase replication from hello Azure portal**</span></span>

1. <span data-ttu-id="94421-181">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-181">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="94421-182">Hello 원본 HBase 클러스터를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="94421-182">Open hello source HBase cluster.</span></span>
3. <span data-ttu-id="94421-183">Hello 클러스터 메뉴에서 클릭 **스크립트 동작**합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-183">From hello cluster menu, click **Script Actions**.</span></span>
4. <span data-ttu-id="94421-184">클릭 **새 제출** hello hello 블레이드 맨 위에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-184">Click **Submit New** from hello top of hello blade.</span></span>
5. <span data-ttu-id="94421-185">선택 하거나 hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-185">Select or enter hello following information:</span></span>

  - <span data-ttu-id="94421-186">**이름**: **복제 사용**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-186">**Name**: Enter **Enable replication**.</span></span>
  - <span data-ttu-id="94421-187">**Bash 스크립트 URL**: **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-187">**Bash Script URL**: Enter **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span></span>
  - <span data-ttu-id="94421-188">**헤드**: 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-188">**Head**: Selected.</span></span> <span data-ttu-id="94421-189">다른 노드 형식 hello 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-189">Clear hello other node types.</span></span>
  - <span data-ttu-id="94421-190">**매개 변수**: hello 다음 hello 원본 클러스터 toohello 대상 클러스터에서 모든 hello 데이터를 복사 및 매개 변수 hello 기존의 모든 테이블에 대 한 복제를 사용 하는 샘플:</span><span class="sxs-lookup"><span data-stu-id="94421-190">**Parameters**: hello following sample parameters enable replication for all hello existing tables and copy all hello data from hello source cluster toohello destination cluster:</span></span>

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. <span data-ttu-id="94421-191">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-191">Click **Create**.</span></span> <span data-ttu-id="94421-192">hello 스크립트에는 다소 시간이 걸릴 수 hello-copydata 인수를 사용 하는 경우에 특히 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-192">hello script can take some time, especially when hello -copydata argument is used.</span></span>

<span data-ttu-id="94421-193">필수 인수:</span><span class="sxs-lookup"><span data-stu-id="94421-193">Required arguments:</span></span>

|<span data-ttu-id="94421-194">이름</span><span class="sxs-lookup"><span data-stu-id="94421-194">Name</span></span>|<span data-ttu-id="94421-195">설명</span><span class="sxs-lookup"><span data-stu-id="94421-195">Description</span></span>|
|----|-----------|
|<span data-ttu-id="94421-196">-s, --src-cluster</span><span class="sxs-lookup"><span data-stu-id="94421-196">-s, --src-cluster</span></span> | <span data-ttu-id="94421-197">Hello hello 원본 HBase 클러스터 DNS 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-197">Specify hello DNS name of hello source HBase cluster.</span></span> <span data-ttu-id="94421-198">예: -s hbsrccluster, --src-cluster=hbsrccluster</span><span class="sxs-lookup"><span data-stu-id="94421-198">For example: -s hbsrccluster, --src-cluster=hbsrccluster</span></span> |
|<span data-ttu-id="94421-199">-d, --dst-cluster</span><span class="sxs-lookup"><span data-stu-id="94421-199">-d, --dst-cluster</span></span> | <span data-ttu-id="94421-200">Hello hello 대상 (복제본) HBase 클러스터 DNS 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-200">Specify hello DNS name of hello destination (replica) HBase cluster.</span></span> <span data-ttu-id="94421-201">예: -s dsthbcluster, --src-cluster=dsthbcluster</span><span class="sxs-lookup"><span data-stu-id="94421-201">For example: -s dsthbcluster, --src-cluster=dsthbcluster</span></span> |
|<span data-ttu-id="94421-202">-sp, --src-ambari-password</span><span class="sxs-lookup"><span data-stu-id="94421-202">-sp, --src-ambari-password</span></span> | <span data-ttu-id="94421-203">Hello 소스 HBase 클러스터에서 Ambari에 대 한 hello 관리자 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-203">Specify hello admin password for Ambari on hello source HBase cluster.</span></span> |
|<span data-ttu-id="94421-204">-dp, --dst-ambari-password</span><span class="sxs-lookup"><span data-stu-id="94421-204">-dp, --dst-ambari-password</span></span> | <span data-ttu-id="94421-205">Ambari에 대 한 hello 대상 HBase 클러스터에 hello 관리자 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-205">Specify hello admin password for Ambari on hello destination HBase cluster.</span></span>|

<span data-ttu-id="94421-206">선택적 인수:</span><span class="sxs-lookup"><span data-stu-id="94421-206">Optional arguments:</span></span>

|<span data-ttu-id="94421-207">이름</span><span class="sxs-lookup"><span data-stu-id="94421-207">Name</span></span>|<span data-ttu-id="94421-208">설명</span><span class="sxs-lookup"><span data-stu-id="94421-208">Description</span></span>|
|----|-----------|
|<span data-ttu-id="94421-209">-su, --src-ambari-user</span><span class="sxs-lookup"><span data-stu-id="94421-209">-su, --src-ambari-user</span></span> | <span data-ttu-id="94421-210">Ambari에 대 한 hello 원본 HBase 클러스터에 hello 관리자 권한을 가진 사용자를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-210">Specify hello admin username for Ambari on hello source HBase cluster.</span></span> <span data-ttu-id="94421-211">hello 기본값은 **admin**합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-211">hello default value is **admin**.</span></span> |
|<span data-ttu-id="94421-212">-du, --dst-ambari-user</span><span class="sxs-lookup"><span data-stu-id="94421-212">-du, --dst-ambari-user</span></span> | <span data-ttu-id="94421-213">Ambari에 대 한 hello 대상 HBase 클러스터에 hello 관리자 권한을 가진 사용자를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-213">Specify hello admin username for Ambari on hello destination HBase cluster.</span></span> <span data-ttu-id="94421-214">hello 기본값은 **admin**합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-214">hello default value is **admin**.</span></span> |
|<span data-ttu-id="94421-215">-t, --table-list</span><span class="sxs-lookup"><span data-stu-id="94421-215">-t, --table-list</span></span> | <span data-ttu-id="94421-216">Hello 테이블 toobe 복제를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-216">Specify hello tables toobe replicated.</span></span> <span data-ttu-id="94421-217">예: --table-list="table1;table2;table3".</span><span class="sxs-lookup"><span data-stu-id="94421-217">For example: --table-list="table1;table2;table3".</span></span> <span data-ttu-id="94421-218">테이블을 지정하지 않으면 기존의 모든 HBase 테이블을 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-218">If you don't specify tables, all existing HBase tables are replicated.</span></span>|
|<span data-ttu-id="94421-219">-m, --machine</span><span class="sxs-lookup"><span data-stu-id="94421-219">-m, --machine</span></span> | <span data-ttu-id="94421-220">Hello 헤드 노드 hello 스크립트 동작 실행 될 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-220">Specify hello head node where hello script action will run.</span></span> <span data-ttu-id="94421-221">hello 값은 hn1 또는 hn0 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-221">hello value is either hn1 or hn0.</span></span> <span data-ttu-id="94421-222">대개 hn0이 더 바쁘기 때문에 hn1을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="94421-222">Because hn0 is usually busier, we recommend using hn1.</span></span> <span data-ttu-id="94421-223">Hello HDInsight 포털 또는 Azure PowerShell에서 스크립트 동작으로 hello $0 스크립트를 실행 하는 경우이 옵션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-223">You use this option when you're running hello $0 script as a script action from hello HDInsight portal or Azure PowerShell.</span></span>|
|<span data-ttu-id="94421-224">-ip</span><span class="sxs-lookup"><span data-stu-id="94421-224">-ip</span></span> | <span data-ttu-id="94421-225">이 인수는 두 개의 가상 네트워크 간에 복제를 사용할 때 필요하며,</span><span class="sxs-lookup"><span data-stu-id="94421-225">This argument is required when you're enabling replication between two virtual networks.</span></span> <span data-ttu-id="94421-226">이 인수는 스위치 toouse hello 정적 Ip의 사육 노드 클러스터를 복제본 클러스터 FQDN 이름 대신 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-226">This argument acts as a switch toouse hello static IPs of ZooKeeper nodes from replica clusters instead of FQDN names.</span></span> <span data-ttu-id="94421-227">hello 정적 Ip toobe 복제를 활성화 하기 전에 미리 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-227">hello static IPs need toobe preconfigured before you enable replication.</span></span> |
|<span data-ttu-id="94421-228">-cp, -copydata</span><span class="sxs-lookup"><span data-stu-id="94421-228">-cp, -copydata</span></span> | <span data-ttu-id="94421-229">복제를 사용 하는 hello 테이블에서 기존 데이터의 hello 마이그레이션을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-229">Enable hello migration of existing data on hello tables where replication is enabled.</span></span> |
|<span data-ttu-id="94421-230">-rpm, -replicate-phoenix-meta</span><span class="sxs-lookup"><span data-stu-id="94421-230">-rpm, -replicate-phoenix-meta</span></span> | <span data-ttu-id="94421-231">Phoenix 시스템 테이블에서 복제를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-231">Enable replication on Phoenix system tables.</span></span> <br><br><span data-ttu-id="94421-232">*이 옵션은 주의해서 사용해야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="94421-232">*Use this option with caution.*</span></span> <span data-ttu-id="94421-233">이 스크립트를 사용하기 전에 복제본 클러스터에서 Phoenix 테이블을 다시 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="94421-233">We recommend that you re-create Phoenix tables on replica clusters before you use this script.</span></span> |
|<span data-ttu-id="94421-234">-h, --help</span><span class="sxs-lookup"><span data-stu-id="94421-234">-h, --help</span></span> | <span data-ttu-id="94421-235">사용 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-235">Display usage information.</span></span> |

<span data-ttu-id="94421-236">hello print_usage() 섹션 hello [스크립트](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) 매개 변수를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-236">hello print_usage() section of hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) provides a detailed explanation of parameters.</span></span>

<span data-ttu-id="94421-237">Hello 스크립트 작업을 성공적으로 후 배포 SSH tooconnect toohello 대상 HBase 클러스터를 사용 하 여 있고 hello 데이터 복제 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-237">After hello script action is successfully deployed, you can use SSH tooconnect toohello destination HBase cluster, and verify hello data has been replicated.</span></span>

### <a name="replication-scenarios"></a><span data-ttu-id="94421-238">복제 시나리오</span><span class="sxs-lookup"><span data-stu-id="94421-238">Replication scenarios</span></span>

<span data-ttu-id="94421-239">hello 다음 목록을 보면 몇 가지 일반 사용 사례 및 해당 매개 변수 설정:</span><span class="sxs-lookup"><span data-stu-id="94421-239">hello following list shows you some general usage cases and their parameter settings:</span></span>

- <span data-ttu-id="94421-240">**Hello 두 클러스터 간의 모든 테이블에서 복제 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-240">**Enable replication on all tables between hello two clusters**.</span></span> <span data-ttu-id="94421-241">이 시나리오 hello 복사/hello 테이블에서 기존 데이터의 마이그레이션에 필요 하지 및 피닉스 테이블을 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="94421-241">This scenario does not require hello copy/migration of existing data on hello tables, and it does not use Phoenix tables.</span></span> <span data-ttu-id="94421-242">매개 변수 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-242">Use hello following parameters:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- <span data-ttu-id="94421-243">**특정 테이블에서 복제를 사용하도록 설정** -</span><span class="sxs-lookup"><span data-stu-id="94421-243">**Enable replication on specific tables**.</span></span> <span data-ttu-id="94421-244">Hello 매개 변수 tooenable 복제 table1, table2 및 표 3에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-244">Use hello following parameters tooenable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- <span data-ttu-id="94421-245">**특정 테이블에서 복제를 사용 하도록 설정 하 고 hello 기존 데이터를 복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-245">**Enable replication on specific tables and copy hello existing data**.</span></span> <span data-ttu-id="94421-246">Hello 매개 변수 tooenable 복제 table1, table2 및 표 3에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-246">Use hello following parameters tooenable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- <span data-ttu-id="94421-247">**소스 toodestination에서 피닉스 메타 데이터를 복제 된 모든 테이블에서 복제 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-247">**Enable replication on all tables with replicating phoenix metadata from source toodestination**.</span></span> <span data-ttu-id="94421-248">Phoenix 메타데이터 복제는 완벽하지 않으므로 주의해서 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-248">Phoenix metadata replication is not perfect and should be enabled with caution.</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a><span data-ttu-id="94421-249">데이터 복사 및 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="94421-249">Copy and migrate data</span></span>

<span data-ttu-id="94421-250">복제를 사용하도록 설정한 후에 데이터를 복사/마이그레이션하기 위한 두 개의 스크립트 동작 스크립트가 별도로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94421-250">There are two separate script action scripts for copying/migrating data after replication is enabled:</span></span>

- <span data-ttu-id="94421-251">[작은 테이블에 대 한 스크립트](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (몇 기가바이트 크기 및 전반적인 복사본에서 1 시간 안에 예상된 toofinish를가 하는 데 사용)</span><span class="sxs-lookup"><span data-stu-id="94421-251">[Script for small tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (a few gigabytes in size, and overall copy is expected toofinish in less than one hour)</span></span>

- <span data-ttu-id="94421-252">[대형 테이블에 대 한 스크립트](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (1 시간 toocopy 보다 긴 tootake 예상)</span><span class="sxs-lookup"><span data-stu-id="94421-252">[Script for large tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (expected tootake longer than one hour toocopy)</span></span>

<span data-ttu-id="94421-253">따를 수 있습니다에 같은 프로시저 hello [복제 사용](#enable-replication) toocall hello 스크립트 동작 매개 변수 뒤 hello로:</span><span class="sxs-lookup"><span data-stu-id="94421-253">You can follow hello same procedure in [Enable replication](#enable-replication) toocall hello script action with hello following parameters:</span></span>

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

<span data-ttu-id="94421-254">hello print_usage() 섹션 hello [스크립트](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) 매개 변수에 대 한 자세한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-254">hello print_usage() section of hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) provides a detailed description of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="94421-255">시나리오</span><span class="sxs-lookup"><span data-stu-id="94421-255">Scenarios</span></span>

- <span data-ttu-id="94421-256">**지금(현재 타임스탬프)까지 편집된 모든 행에 대한 특정 테이블(test1, test2 및 test3) 복사**:</span><span class="sxs-lookup"><span data-stu-id="94421-256">**Copy specific tables (test1, test2, and test3) for all rows edited till now (current time stamp)**:</span></span>

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  <span data-ttu-id="94421-257">또는</span><span class="sxs-lookup"><span data-stu-id="94421-257">or</span></span>

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- <span data-ttu-id="94421-258">**지정된 시간 범위의 특정 테이블 복사**:</span><span class="sxs-lookup"><span data-stu-id="94421-258">**Copy specific tables with specified time range**:</span></span>

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a><span data-ttu-id="94421-259">복제 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="94421-259">Disable replication</span></span>

<span data-ttu-id="94421-260">에 있는 다른 스크립트 동작 스크립트 사용 toodisable 복제 [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh)합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-260">toodisable replication, you use another script action script located at [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span></span> <span data-ttu-id="94421-261">따를 수 있습니다에 같은 프로시저 hello [복제 사용](#enable-replication) toocall hello 스크립트 동작 매개 변수 뒤 hello로:</span><span class="sxs-lookup"><span data-stu-id="94421-261">You can follow hello same procedure in [Enable replication](#enable-replication) toocall hello script action with hello following parameters:</span></span>

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

<span data-ttu-id="94421-262">hello print_usage() 섹션 hello [스크립트](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) 매개 변수를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-262">hello print_usage() section of hello [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) provides a detailed explanation of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="94421-263">시나리오</span><span class="sxs-lookup"><span data-stu-id="94421-263">Scenarios</span></span>

- <span data-ttu-id="94421-264">**모든 테이블에서 복제를 사용하지 않도록 설정**:</span><span class="sxs-lookup"><span data-stu-id="94421-264">**Disable replication on all tables**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  <span data-ttu-id="94421-265">또는</span><span class="sxs-lookup"><span data-stu-id="94421-265">or</span></span>

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- <span data-ttu-id="94421-266">**지정된 테이블(table1, table2 및 table3)에서 복제를 사용하지 않도록 설정**:</span><span class="sxs-lookup"><span data-stu-id="94421-266">**Disable replication on specified tables (table1, table2, and table3)**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a><span data-ttu-id="94421-267">다음 단계</span><span class="sxs-lookup"><span data-stu-id="94421-267">Next steps</span></span>

<span data-ttu-id="94421-268">이 자습서에서는 방법에 대해 배웠습니다 두 데이터 센터에서 tooconfigure HBase 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="94421-268">In this tutorial, you learned how tooconfigure HBase replication across two datacenters.</span></span> <span data-ttu-id="94421-269">toolearn 더 및에 대 한 HDInsight HBase를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="94421-269">toolearn more about HDInsight and HBase, see:</span></span>

* <span data-ttu-id="94421-270">[HDInsight에서 Apache HBase 시작][hdinsight-hbase-get-started]</span><span class="sxs-lookup"><span data-stu-id="94421-270">[Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started]</span></span>
* <span data-ttu-id="94421-271">[HDInsight HBase 개요][hdinsight-hbase-overview]</span><span class="sxs-lookup"><span data-stu-id="94421-271">[HDInsight HBase overview][hdinsight-hbase-overview]</span></span>
* <span data-ttu-id="94421-272">[Azure Virtual Network에 HBase 클러스터 만들기][hdinsight-hbase-provision-vnet]</span><span class="sxs-lookup"><span data-stu-id="94421-272">[Create HBase clusters in Azure Virtual Network][hdinsight-hbase-provision-vnet]</span></span>
* <span data-ttu-id="94421-273">[HBase를 사용하여 Twitter 데이터 실시간 분석][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="94421-273">[Analyze real-time Twitter sentiment with HBase][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="94421-274">[HDInsight(Hadoop)에서 Apache Storm 및 HBase를 사용하여 센서 데이터 분석][hdinsight-sensor-data]</span><span class="sxs-lookup"><span data-stu-id="94421-274">[Analyzing sensor data with Storm and HBase in HDInsight (Hadoop)][hdinsight-sensor-data]</span></span>

[hdinsight-hbase-geo-replication-vnet]: hdinsight-hbase-geo-replication-configure-vnets.md
[hdinsight-hbase-geo-replication-dns]: ../hdinsight-hbase-geo-replication-configure-VNet.md


[img-vnet-diagram]: ./media/hdinsight-hbase-geo-replication/HDInsight.HBase.Replication.Network.diagram.png

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[hdinsight-sensor-data]: hdinsight-storm-sensor-data-analysis.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
