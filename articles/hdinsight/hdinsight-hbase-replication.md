---
title: "가상 네트워크 내에서 HBase 클러스터 복제 구성 - Azure  | Microsoft Docs"
description: "부하 분산, 고가용성, 한 버전의 HDInsight에서 다른 버전으로의 무중단 마이그레이션/업데이트 및 재해 복구를 위해 HBase 복제를 구성하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 895709391486acb4a9d7a54ef046956539913f7b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a><span data-ttu-id="8376c-103">가상 네트워크 내에서 HBase 클러스터 복제 구성</span><span class="sxs-lookup"><span data-stu-id="8376c-103">Configure HBase cluster replication within virtual networks</span></span>

<span data-ttu-id="8376c-104">한 VNet(가상 네트워크) 내에 또는 두 VNet 간에 HBase 복제를 구성하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-104">Learn how to configure HBase replication within one virtual network (VNet) or between two virtual networks.</span></span>

<span data-ttu-id="8376c-105">클러스터 복제에서는 원본-푸시 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-105">Cluster replication uses a source-push methodology.</span></span> <span data-ttu-id="8376c-106">HBase 클러스터는 원본 또는 대상이 될 수도 있고, 한 번에 두 가지 역할을 모두 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-106">An HBase cluster can be a source or a destination, or it can fulfill both roles at once.</span></span> <span data-ttu-id="8376c-107">복제는 비동기이며 복제의 목적은 일관성을 유지하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-107">Replication is asynchronous, and the goal of replication is eventual consistency.</span></span> <span data-ttu-id="8376c-108">원본에서 복제를 사용할 수 있는 열 패밀리에 대한 편집 내용을 받은 경우 해당 편집 내용은 모든 대상 클러스터로 전파됩니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-108">When the source receives an edit to a column family with replication enabled, that edit is propagated to all destination clusters.</span></span> <span data-ttu-id="8376c-109">클러스터 간에 데이터를 복제하는 경우 복제 루프를 방지하기 위해 데이터를 이미 사용한 원본 클러스터 및 모든 클러스터가 추적됩니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-109">When data is replicated from one cluster to another, the source cluster and all clusters that have already consumed the data are tracked to prevent replication loops.</span></span>

<span data-ttu-id="8376c-110">이 자습서에서는 원본-대상 복제를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-110">In this tutorial, you will configure a source-destination replication.</span></span> <span data-ttu-id="8376c-111">다른 클러스터 토폴로지는 [Apache HBase 참조 가이드](http://hbase.apache.org/book.html#_cluster_replication)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8376c-111">For other cluster topologies, see [Apache HBase Reference Guide](http://hbase.apache.org/book.html#_cluster_replication).</span></span>

<span data-ttu-id="8376c-112">단일 가상 네트워크에 대한 HBase 복제 사용 사례:</span><span class="sxs-lookup"><span data-stu-id="8376c-112">HBase replication usage cases for a single virtual network:</span></span>

* <span data-ttu-id="8376c-113">부하 분산 - 예를 들어 대상 클러스터에서 스캔 또는 MapReduce 작업을 실행하고 원본 클러스터에서 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-113">Load balancing--for example, running scans or MapReduce jobs on the destination cluster and ingesting data on the source cluster</span></span>
* <span data-ttu-id="8376c-114">고가용성</span><span class="sxs-lookup"><span data-stu-id="8376c-114">High availability</span></span>
* <span data-ttu-id="8376c-115">하나의 HBase 클러스터에서 다른 HBase 클러스터로 데이터 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="8376c-115">Migrating data from one HBase cluster to another</span></span>
* <span data-ttu-id="8376c-116">한 버전에서 다른 버전으로 Azure HDInsight 클러스터 업그레이드</span><span class="sxs-lookup"><span data-stu-id="8376c-116">Upgrading an Azure HDInsight cluster from one version to another</span></span>

<span data-ttu-id="8376c-117">두 가상 네트워크에 대한 HBase 복제 사용 사례:</span><span class="sxs-lookup"><span data-stu-id="8376c-117">HBase replication usage cases for two virtual networks:</span></span>

* <span data-ttu-id="8376c-118">재해 복구</span><span class="sxs-lookup"><span data-stu-id="8376c-118">Disaster recovery</span></span>
* <span data-ttu-id="8376c-119">응용 프로그램 부하 분산 및 분할</span><span class="sxs-lookup"><span data-stu-id="8376c-119">Load balancing and partitioning the application</span></span>
* <span data-ttu-id="8376c-120">고가용성</span><span class="sxs-lookup"><span data-stu-id="8376c-120">High availability</span></span>

<span data-ttu-id="8376c-121">[GitHub](https://github.com/Azure/hbase-utils/tree/master/replication)에 있는 [스크립트 동작](hdinsight-hadoop-customize-cluster-linux.md) 스크립트를 사용하여 클러스터를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-121">You replicate clusters by using [script action](hdinsight-hadoop-customize-cluster-linux.md) scripts located at [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8376c-122">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8376c-122">Prerequisites</span></span>
<span data-ttu-id="8376c-123">이 자습서를 시작하기 전에 Azure 구독이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-123">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="8376c-124">[Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8376c-124">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="configure-the-environments"></a><span data-ttu-id="8376c-125">환경 구성</span><span class="sxs-lookup"><span data-stu-id="8376c-125">Configure the environments</span></span>

<span data-ttu-id="8376c-126">다음과 같이 세 가지 가능한 구성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-126">There are three possible configurations:</span></span>

- <span data-ttu-id="8376c-127">1개 Azure 가상 네트워크에 2개 HBase 클러스터 구성</span><span class="sxs-lookup"><span data-stu-id="8376c-127">Two HBase clusters in one Azure virtual network</span></span>
- <span data-ttu-id="8376c-128">동일한 지역에 있는 별도의 2개 가상 네트워크에 2개 HBase 클러스터 구성</span><span class="sxs-lookup"><span data-stu-id="8376c-128">Two HBase clusters in two different virtual networks in the same region</span></span>
- <span data-ttu-id="8376c-129">별도의 2개 지역에 있는 2개 다른 가상 네트워크에 2개 HBase 클러스터 구성(지리적 복제)</span><span class="sxs-lookup"><span data-stu-id="8376c-129">Two HBase clusters in two different virtual networks in two different regions (geo-replication)</span></span>

<span data-ttu-id="8376c-130">환경을 쉽게 구성할 수 있도록 몇 가지 [Azure Resource Manager 템플릿](../azure-resource-manager/resource-group-overview.md)을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-130">To make it easier to configure the environments, we have created some [Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="8376c-131">다른 방법을 사용하여 환경을 구성하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8376c-131">If you prefer to configure the environments by using other methods, see:</span></span>

- [<span data-ttu-id="8376c-132">HDInsight에서 Linux 기반 Hadoop 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="8376c-132">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
- [<span data-ttu-id="8376c-133">Azure Virtual Network에 HBase 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="8376c-133">Create HBase clusters in Azure Virtual Network</span></span>](hdinsight-hbase-provision-vnet.md)

### <a name="configure-one-virtual-network"></a><span data-ttu-id="8376c-134">1개 가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="8376c-134">Configure one virtual network</span></span>

<span data-ttu-id="8376c-135">다음 이미지를 클릭하면 동일한 가상 네트워크에서 두 개의 HBase 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-135">Click the following image to create two HBase clusters in the same virtual network.</span></span> <span data-ttu-id="8376c-136">템플릿은 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/)에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-136">The template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy to Azure"></a>

### <a name="configure-two-virtual-networks-in-the-same-region"></a><span data-ttu-id="8376c-137">동일한 지역에 2개 가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="8376c-137">Configure two virtual networks in the same region</span></span>

<span data-ttu-id="8376c-138">다음 이미지를 클릭하면 동일한 지역에 VNet 피어링과 두 개의 HBase 클러스터가 있는 두 개의 가상 네트워크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-138">Click the following image to create two virtual networks with VNet peering and two HBase clusters in the same region.</span></span> <span data-ttu-id="8376c-139">템플릿은 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/)에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-139">The template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy to Azure"></a>



<span data-ttu-id="8376c-140">이 시나리오에는 [VNet 피어링](../virtual-network/virtual-network-peering-overview.md)이 필요하며,</span><span class="sxs-lookup"><span data-stu-id="8376c-140">This scenario requires [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> <span data-ttu-id="8376c-141">템플릿은 VNet 피어링을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-141">The template enables VNet peering.</span></span>   

<span data-ttu-id="8376c-142">HBase 복제는 ZooKeeper VM의 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-142">HBase replication uses IP addresses of the ZooKeeper VMs.</span></span> <span data-ttu-id="8376c-143">대상 HBase ZooKeeper 노드에 대해 고정 IP 주소를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-143">You must configure static IP addresses for the destination HBase ZooKeeper nodes.</span></span>

<span data-ttu-id="8376c-144">**고정 IP 주소를 구성 하려면**</span><span class="sxs-lookup"><span data-stu-id="8376c-144">**To configure static IP addresses**</span></span>

1. <span data-ttu-id="8376c-145">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-145">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8376c-146">왼쪽 메뉴에서 **리소스 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-146">From the left menu, click **Resource Groups**.</span></span>
3. <span data-ttu-id="8376c-147">대상 HBase 클러스터가 포함된 리소스 그룹을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-147">Click your resource group that contains the destination HBase cluster.</span></span> <span data-ttu-id="8376c-148">이 그룹은 Resource Manager 템플릿을 사용하여 환경을 만들 때 지정한 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-148">This is the resource group that you specified when you used the Resource Manager template to create the environment.</span></span> <span data-ttu-id="8376c-149">필터를 사용하여 목록의 범위를 좁힐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-149">You can use the filter to narrow down the list.</span></span> <span data-ttu-id="8376c-150">두 개의 가상 네트워크가 포함된 리소스 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-150">You can see a list of resources that contains the two virtual networks.</span></span>
4. <span data-ttu-id="8376c-151">대상 HBase 클러스터가 포함된 가상 네트워크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-151">Click the virtual network that contains the destination HBase cluster.</span></span> <span data-ttu-id="8376c-152">예를 들어 **xxxx-vnet2**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-152">For example, click **xxxx-vnet2**.</span></span> <span data-ttu-id="8376c-153">**nic-zookeepermode-**로 시작하는 이름을 가진 세 개의 장치를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-153">You can see three devices with names that start with **nic-zookeepermode-**.</span></span> <span data-ttu-id="8376c-154">이러한 장치는 세 개의 ZooKeeper VM입니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-154">Those devices are the three ZooKeeper VMs.</span></span>
5. <span data-ttu-id="8376c-155">ZooKeeper VM 중 하나를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-155">Click one of the ZooKeeper VMs.</span></span>
6. <span data-ttu-id="8376c-156">**IP 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-156">Click **IP configurations**.</span></span>
7. <span data-ttu-id="8376c-157">목록에서 **ipConfig1**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-157">Click **ipConfig1** from the list.</span></span>
8. <span data-ttu-id="8376c-158">**고정**을 클릭하고 실제 IP 주소를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-158">Click **Static**, and write down the actual IP address.</span></span> <span data-ttu-id="8376c-159">스크립트 동작을 실행하여 복제를 사용하도록 설정할 때 IP 주소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-159">You will need the IP address when you run the script action to enable replication.</span></span>

  ![HDInsight HBase 복제 ZooKeeper 고정 IP](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. <span data-ttu-id="8376c-161">6단계를 반복하여 다른 두 ZooKeeper 노드의 고정 IP 주소를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-161">Repeat step 6 to set the static IP address for the other two ZooKeeper nodes.</span></span>

<span data-ttu-id="8376c-162">VNet 간 시나리오의 경우 **hdi_enable_replication.sh** 스크립트 작업 호출 시 **-ip** 스위치를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-162">For the cross-VNet scenario, you must use the **-ip** switch when calling the **hdi_enable_replication.sh** script action.</span></span>

### <a name="configure-two-virtual-networks-in-two-different-regions"></a><span data-ttu-id="8376c-163">별도의 2개 지역에 2개 가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="8376c-163">Configure two virtual networks in two different regions</span></span>

<span data-ttu-id="8376c-164">다음 이미지를 클릭하면 두 개의 다른 지역에 두 개의 가상 네트워크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-164">Click the following image to create two virtual networks in two different regions.</span></span> <span data-ttu-id="8376c-165">템플릿은 공용 Azure Blob 컨테이너에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-165">The template is stored in a public Azure Blob container.</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy to Azure"></a>

<span data-ttu-id="8376c-166">두 개의 가상 네트워크 간에 VPN 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-166">Create a VPN gateway between the two virtual networks.</span></span> <span data-ttu-id="8376c-167">지침은 [사이트 간 연결로 VNet 만들기](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8376c-167">For instructions, see [Create a VNet with a site-to-site connection](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span></span>

<span data-ttu-id="8376c-168">HBase 복제는 ZooKeeper VM의 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-168">HBase replication uses IP addresses of the ZooKeeper VMs.</span></span> <span data-ttu-id="8376c-169">대상 HBase ZooKeeper 노드에 대해 고정 IP 주소를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-169">You must configure static IP addresses for the destination HBase ZooKeeper nodes.</span></span> <span data-ttu-id="8376c-170">고정 IP를 구성하려면 이 문서의 "동일한 지역에 2개 가상 네트워크 구성" 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8376c-170">To configure static IP, see the "Configure two virtual networks in the same region" section in this article.</span></span>

<span data-ttu-id="8376c-171">VNet 간 시나리오의 경우 **hdi_enable_replication.sh** 스크립트 작업 호출 시 **-ip** 스위치를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-171">For the cross-VNet scenario, you must use the **-ip** switch when calling the **hdi_enable_replication.sh** script action.</span></span>

## <a name="load-test-data"></a><span data-ttu-id="8376c-172">테스트 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="8376c-172">Load test data</span></span>

<span data-ttu-id="8376c-173">클러스터를 복제할 때 복제할 테이블을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-173">When you replicate a cluster, you must specify the tables to replicate.</span></span> <span data-ttu-id="8376c-174">이 섹션에서는 일부 데이터를 원본 클러스터에 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-174">In this section, you will load some data into the source cluster.</span></span> <span data-ttu-id="8376c-175">다음 섹션에서는 두 클러스터 간에 복제를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-175">In the next section, you will enable replication between the two clusters.</span></span>

<span data-ttu-id="8376c-176">[HBase 자습서: HDInsight에서 Linux 기반 Hadoop을 통해 Apache HBase 사용 시작](hdinsight-hbase-tutorial-get-started-linux.md)의 지침에 따라 **연락처** 테이블을 만들고 이 테이블에 데이터를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-176">Follow the instructions in [HBase tutorial: Get started using Apache HBase with Linux-based Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) to create a **Contacts** table and insert some data into the table.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="8376c-177">복제 사용</span><span class="sxs-lookup"><span data-stu-id="8376c-177">Enable replication</span></span>

<span data-ttu-id="8376c-178">다음 단계에서는 Azure Portal에서 스크립트 동작 스크립트를 호출하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-178">The following steps show how to call the script action script from the Azure portal.</span></span> <span data-ttu-id="8376c-179">Azure PowerShell과 Azure CLI(명령줄 인터페이스)를 사용하여 스크립트 동작을 실행하려면 [스크립트 동작을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8376c-179">For running a script action by using Azure PowerShell and the Azure command-line interface (CLI), see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="8376c-180">**Azure Portal에서 HBase 복제를 사용하도록 설정하려면**</span><span class="sxs-lookup"><span data-stu-id="8376c-180">**To enable HBase replication from the Azure portal**</span></span>

1. <span data-ttu-id="8376c-181">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-181">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8376c-182">원본 HBase 클러스터를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-182">Open the source HBase cluster.</span></span>
3. <span data-ttu-id="8376c-183">클러스터 메뉴에서 **스크립트 동작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-183">From the cluster menu, click **Script Actions**.</span></span>
4. <span data-ttu-id="8376c-184">블레이드 위쪽에서 **새로운 항목 제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-184">Click **Submit New** from the top of the blade.</span></span>
5. <span data-ttu-id="8376c-185">다음 정보를 선택하거나 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-185">Select or enter the following information:</span></span>

  - <span data-ttu-id="8376c-186">**이름**: **복제 사용**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-186">**Name**: Enter **Enable replication**.</span></span>
  - <span data-ttu-id="8376c-187">**Bash 스크립트 URL**: **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-187">**Bash Script URL**: Enter **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span></span>
  - <span data-ttu-id="8376c-188">**헤드**: 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-188">**Head**: Selected.</span></span> <span data-ttu-id="8376c-189">다른 노드 형식은 선택 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-189">Clear the other node types.</span></span>
  - <span data-ttu-id="8376c-190">**매개 변수**: 다음 샘플 매개 변수를 사용하면 기존의 모든 테이블을 복제하도록 설정하고 모든 데이터를 원본 클러스터에서 대상 클러스터로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-190">**Parameters**: The following sample parameters enable replication for all the existing tables and copy all the data from the source cluster to the destination cluster:</span></span>

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. <span data-ttu-id="8376c-191">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-191">Click **Create**.</span></span> <span data-ttu-id="8376c-192">특히 -copydata 인수를 사용하는 경우 스크립트 실행에서 시간이 좀 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-192">The script can take some time, especially when the -copydata argument is used.</span></span>

<span data-ttu-id="8376c-193">필수 인수:</span><span class="sxs-lookup"><span data-stu-id="8376c-193">Required arguments:</span></span>

|<span data-ttu-id="8376c-194">이름</span><span class="sxs-lookup"><span data-stu-id="8376c-194">Name</span></span>|<span data-ttu-id="8376c-195">설명</span><span class="sxs-lookup"><span data-stu-id="8376c-195">Description</span></span>|
|----|-----------|
|<span data-ttu-id="8376c-196">-s, --src-cluster</span><span class="sxs-lookup"><span data-stu-id="8376c-196">-s, --src-cluster</span></span> | <span data-ttu-id="8376c-197">원본 HBase 클러스터의 DNS 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-197">Specify the DNS name of the source HBase cluster.</span></span> <span data-ttu-id="8376c-198">예: -s hbsrccluster, --src-cluster=hbsrccluster</span><span class="sxs-lookup"><span data-stu-id="8376c-198">For example: -s hbsrccluster, --src-cluster=hbsrccluster</span></span> |
|<span data-ttu-id="8376c-199">-d, --dst-cluster</span><span class="sxs-lookup"><span data-stu-id="8376c-199">-d, --dst-cluster</span></span> | <span data-ttu-id="8376c-200">대상(복제본) HBase 클러스터의 DNS 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-200">Specify the DNS name of the destination (replica) HBase cluster.</span></span> <span data-ttu-id="8376c-201">예: -s dsthbcluster, --src-cluster=dsthbcluster</span><span class="sxs-lookup"><span data-stu-id="8376c-201">For example: -s dsthbcluster, --src-cluster=dsthbcluster</span></span> |
|<span data-ttu-id="8376c-202">-sp, --src-ambari-password</span><span class="sxs-lookup"><span data-stu-id="8376c-202">-sp, --src-ambari-password</span></span> | <span data-ttu-id="8376c-203">원본 HBase 클러스터에서 Ambari의 관리자 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-203">Specify the admin password for Ambari on the source HBase cluster.</span></span> |
|<span data-ttu-id="8376c-204">-dp, --dst-ambari-password</span><span class="sxs-lookup"><span data-stu-id="8376c-204">-dp, --dst-ambari-password</span></span> | <span data-ttu-id="8376c-205">대상 HBase 클러스터에서 Ambari의 관리자 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-205">Specify the admin password for Ambari on the destination HBase cluster.</span></span>|

<span data-ttu-id="8376c-206">선택적 인수:</span><span class="sxs-lookup"><span data-stu-id="8376c-206">Optional arguments:</span></span>

|<span data-ttu-id="8376c-207">이름</span><span class="sxs-lookup"><span data-stu-id="8376c-207">Name</span></span>|<span data-ttu-id="8376c-208">설명</span><span class="sxs-lookup"><span data-stu-id="8376c-208">Description</span></span>|
|----|-----------|
|<span data-ttu-id="8376c-209">-su, --src-ambari-user</span><span class="sxs-lookup"><span data-stu-id="8376c-209">-su, --src-ambari-user</span></span> | <span data-ttu-id="8376c-210">원본 HBase 클러스터에서 Ambari의 관리자 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-210">Specify the admin username for Ambari on the source HBase cluster.</span></span> <span data-ttu-id="8376c-211">기본값은 **admin**입니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-211">The default value is **admin**.</span></span> |
|<span data-ttu-id="8376c-212">-du, --dst-ambari-user</span><span class="sxs-lookup"><span data-stu-id="8376c-212">-du, --dst-ambari-user</span></span> | <span data-ttu-id="8376c-213">대상 HBase 클러스터에서 Ambari의 관리자 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-213">Specify the admin username for Ambari on the destination HBase cluster.</span></span> <span data-ttu-id="8376c-214">기본값은 **admin**입니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-214">The default value is **admin**.</span></span> |
|<span data-ttu-id="8376c-215">-t, --table-list</span><span class="sxs-lookup"><span data-stu-id="8376c-215">-t, --table-list</span></span> | <span data-ttu-id="8376c-216">복제할 테이블을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-216">Specify the tables to be replicated.</span></span> <span data-ttu-id="8376c-217">예: --table-list="table1;table2;table3".</span><span class="sxs-lookup"><span data-stu-id="8376c-217">For example: --table-list="table1;table2;table3".</span></span> <span data-ttu-id="8376c-218">테이블을 지정하지 않으면 기존의 모든 HBase 테이블을 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-218">If you don't specify tables, all existing HBase tables are replicated.</span></span>|
|<span data-ttu-id="8376c-219">-m, --machine</span><span class="sxs-lookup"><span data-stu-id="8376c-219">-m, --machine</span></span> | <span data-ttu-id="8376c-220">스크립트 동작이 실행될 헤드 노드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-220">Specify the head node where the script action will run.</span></span> <span data-ttu-id="8376c-221">값은 hn1 또는 hn0입니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-221">The value is either hn1 or hn0.</span></span> <span data-ttu-id="8376c-222">대개 hn0이 더 바쁘기 때문에 hn1을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-222">Because hn0 is usually busier, we recommend using hn1.</span></span> <span data-ttu-id="8376c-223">HDInsight 포털 또는 Azure PowerShell에서 $0 스크립트를 스크립트 동작으로 실행하는 경우 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-223">You use this option when you're running the $0 script as a script action from the HDInsight portal or Azure PowerShell.</span></span>|
|<span data-ttu-id="8376c-224">-ip</span><span class="sxs-lookup"><span data-stu-id="8376c-224">-ip</span></span> | <span data-ttu-id="8376c-225">이 인수는 두 개의 가상 네트워크 간에 복제를 사용할 때 필요하며,</span><span class="sxs-lookup"><span data-stu-id="8376c-225">This argument is required when you're enabling replication between two virtual networks.</span></span> <span data-ttu-id="8376c-226">FQDN 이름 대신 복제본 클러스터에서 ZooKeeper 노드의 고정 IP를 사용하는 스위치 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-226">This argument acts as a switch to use the static IPs of ZooKeeper nodes from replica clusters instead of FQDN names.</span></span> <span data-ttu-id="8376c-227">고정 IP는 복제를 사용하도록 설정하기 전에 미리 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-227">The static IPs need to be preconfigured before you enable replication.</span></span> |
|<span data-ttu-id="8376c-228">-cp, -copydata</span><span class="sxs-lookup"><span data-stu-id="8376c-228">-cp, -copydata</span></span> | <span data-ttu-id="8376c-229">복제가 사용되는 테이블에서 기존 데이터의 마이그레이션을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-229">Enable the migration of existing data on the tables where replication is enabled.</span></span> |
|<span data-ttu-id="8376c-230">-rpm, -replicate-phoenix-meta</span><span class="sxs-lookup"><span data-stu-id="8376c-230">-rpm, -replicate-phoenix-meta</span></span> | <span data-ttu-id="8376c-231">Phoenix 시스템 테이블에서 복제를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-231">Enable replication on Phoenix system tables.</span></span> <br><br><span data-ttu-id="8376c-232">*이 옵션은 주의해서 사용해야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="8376c-232">*Use this option with caution.*</span></span> <span data-ttu-id="8376c-233">이 스크립트를 사용하기 전에 복제본 클러스터에서 Phoenix 테이블을 다시 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-233">We recommend that you re-create Phoenix tables on replica clusters before you use this script.</span></span> |
|<span data-ttu-id="8376c-234">-h, --help</span><span class="sxs-lookup"><span data-stu-id="8376c-234">-h, --help</span></span> | <span data-ttu-id="8376c-235">사용 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-235">Display usage information.</span></span> |

<span data-ttu-id="8376c-236">[스크립트](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh)의 print_usage() 섹션은 매개 변수에 대한 자세한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-236">The print_usage() section of the [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) provides a detailed explanation of parameters.</span></span>

<span data-ttu-id="8376c-237">스크립트 동작이 성공적으로 배포된 후에 SSH를 사용하면 대상 HBase 클러스터에 연결하고 데이터가 복제되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-237">After the script action is successfully deployed, you can use SSH to connect to the destination HBase cluster, and verify the data has been replicated.</span></span>

### <a name="replication-scenarios"></a><span data-ttu-id="8376c-238">복제 시나리오</span><span class="sxs-lookup"><span data-stu-id="8376c-238">Replication scenarios</span></span>

<span data-ttu-id="8376c-239">다음 목록에서는 일반적인 사용 사례 및 해당 매개 변수 설정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-239">The following list shows you some general usage cases and their parameter settings:</span></span>

- <span data-ttu-id="8376c-240">**두 클러스터 간의 모든 테이블에서 복제를 사용하도록 설정** -</span><span class="sxs-lookup"><span data-stu-id="8376c-240">**Enable replication on all tables between the two clusters**.</span></span> <span data-ttu-id="8376c-241">이 시나리오에서는 기존 데이터를 테이블에 복사/마이그레이션할 필요가 없으며 Phoenix 테이블을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-241">This scenario does not require the copy/migration of existing data on the tables, and it does not use Phoenix tables.</span></span> <span data-ttu-id="8376c-242">다음 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-242">Use the following parameters:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- <span data-ttu-id="8376c-243">**특정 테이블에서 복제를 사용하도록 설정** -</span><span class="sxs-lookup"><span data-stu-id="8376c-243">**Enable replication on specific tables**.</span></span> <span data-ttu-id="8376c-244">table1, table2 및 table3에서 복제를 사용하도록 설정하려면 다음 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-244">Use the following parameters to enable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- <span data-ttu-id="8376c-245">**특정 테이블에서 복제를 사용하도록 설정 및 기존 데이터 복사** -</span><span class="sxs-lookup"><span data-stu-id="8376c-245">**Enable replication on specific tables and copy the existing data**.</span></span> <span data-ttu-id="8376c-246">table1, table2 및 table3에서 복제를 사용하도록 설정하려면 다음 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-246">Use the following parameters to enable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- <span data-ttu-id="8376c-247">**원본에서 대상으로 phoenix 메타데이터를 복제하여 모든 테이블에서 복제를 사용하도록 설정** -</span><span class="sxs-lookup"><span data-stu-id="8376c-247">**Enable replication on all tables with replicating phoenix metadata from source to destination**.</span></span> <span data-ttu-id="8376c-248">Phoenix 메타데이터 복제는 완벽하지 않으므로 주의해서 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-248">Phoenix metadata replication is not perfect and should be enabled with caution.</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a><span data-ttu-id="8376c-249">데이터 복사 및 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="8376c-249">Copy and migrate data</span></span>

<span data-ttu-id="8376c-250">복제를 사용하도록 설정한 후에 데이터를 복사/마이그레이션하기 위한 두 개의 스크립트 동작 스크립트가 별도로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-250">There are two separate script action scripts for copying/migrating data after replication is enabled:</span></span>

- <span data-ttu-id="8376c-251">[소형 테이블용 스크립트](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) - 수 GB 크기, 전체 복사 완료에 1시간 이내 소요</span><span class="sxs-lookup"><span data-stu-id="8376c-251">[Script for small tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (a few gigabytes in size, and overall copy is expected to finish in less than one hour)</span></span>

- <span data-ttu-id="8376c-252">[대형 테이블용 스크립트](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) - 복사 완료에 1시간 이상 소요</span><span class="sxs-lookup"><span data-stu-id="8376c-252">[Script for large tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (expected to take longer than one hour to copy)</span></span>

<span data-ttu-id="8376c-253">[복제 사용](#enable-replication)과 동일한 절차에 따라 다음 매개 변수를 사용하여 스크립트 동작을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-253">You can follow the same procedure in [Enable replication](#enable-replication) to call the script action with the following parameters:</span></span>

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

<span data-ttu-id="8376c-254">[스크립트](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh)의 print_usage() 섹션은 매개 변수에 대한 자세한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-254">The print_usage() section of the [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) provides a detailed description of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="8376c-255">시나리오</span><span class="sxs-lookup"><span data-stu-id="8376c-255">Scenarios</span></span>

- <span data-ttu-id="8376c-256">**지금(현재 타임스탬프)까지 편집된 모든 행에 대한 특정 테이블(test1, test2 및 test3) 복사**:</span><span class="sxs-lookup"><span data-stu-id="8376c-256">**Copy specific tables (test1, test2, and test3) for all rows edited till now (current time stamp)**:</span></span>

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  <span data-ttu-id="8376c-257">또는</span><span class="sxs-lookup"><span data-stu-id="8376c-257">or</span></span>

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- <span data-ttu-id="8376c-258">**지정된 시간 범위의 특정 테이블 복사**:</span><span class="sxs-lookup"><span data-stu-id="8376c-258">**Copy specific tables with specified time range**:</span></span>

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a><span data-ttu-id="8376c-259">복제 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="8376c-259">Disable replication</span></span>

<span data-ttu-id="8376c-260">복제를 사용하지 않도록 설정하려면 [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh)에 있는 다른 스크립트 동작 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-260">To disable replication, you use another script action script located at [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span></span> <span data-ttu-id="8376c-261">[복제 사용](#enable-replication)과 동일한 절차에 따라 다음 매개 변수를 사용하여 스크립트 동작을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-261">You can follow the same procedure in [Enable replication](#enable-replication) to call the script action with the following parameters:</span></span>

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

<span data-ttu-id="8376c-262">[스크립트](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh)의 print_usage() 섹션은 매개 변수에 대한 자세한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-262">The print_usage() section of the [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) provides a detailed explanation of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="8376c-263">시나리오</span><span class="sxs-lookup"><span data-stu-id="8376c-263">Scenarios</span></span>

- <span data-ttu-id="8376c-264">**모든 테이블에서 복제를 사용하지 않도록 설정**:</span><span class="sxs-lookup"><span data-stu-id="8376c-264">**Disable replication on all tables**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  <span data-ttu-id="8376c-265">또는</span><span class="sxs-lookup"><span data-stu-id="8376c-265">or</span></span>

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- <span data-ttu-id="8376c-266">**지정된 테이블(table1, table2 및 table3)에서 복제를 사용하지 않도록 설정**:</span><span class="sxs-lookup"><span data-stu-id="8376c-266">**Disable replication on specified tables (table1, table2, and table3)**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a><span data-ttu-id="8376c-267">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8376c-267">Next steps</span></span>

<span data-ttu-id="8376c-268">이 자습서에서는 두 데이터 센터에서 HBase 복제를 구성하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="8376c-268">In this tutorial, you learned how to configure HBase replication across two datacenters.</span></span> <span data-ttu-id="8376c-269">HDInsight 및 HBase에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8376c-269">To learn more about HDInsight and HBase, see:</span></span>

* <span data-ttu-id="8376c-270">[HDInsight에서 Apache HBase 시작][hdinsight-hbase-get-started]</span><span class="sxs-lookup"><span data-stu-id="8376c-270">[Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started]</span></span>
* <span data-ttu-id="8376c-271">[HDInsight HBase 개요][hdinsight-hbase-overview]</span><span class="sxs-lookup"><span data-stu-id="8376c-271">[HDInsight HBase overview][hdinsight-hbase-overview]</span></span>
* <span data-ttu-id="8376c-272">[Azure Virtual Network에 HBase 클러스터 만들기][hdinsight-hbase-provision-vnet]</span><span class="sxs-lookup"><span data-stu-id="8376c-272">[Create HBase clusters in Azure Virtual Network][hdinsight-hbase-provision-vnet]</span></span>
* <span data-ttu-id="8376c-273">[HBase를 사용하여 Twitter 데이터 실시간 분석][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="8376c-273">[Analyze real-time Twitter sentiment with HBase][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="8376c-274">[HDInsight(Hadoop)에서 Apache Storm 및 HBase를 사용하여 센서 데이터 분석][hdinsight-sensor-data]</span><span class="sxs-lookup"><span data-stu-id="8376c-274">[Analyzing sensor data with Storm and HBase in HDInsight (Hadoop)][hdinsight-sensor-data]</span></span>

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
