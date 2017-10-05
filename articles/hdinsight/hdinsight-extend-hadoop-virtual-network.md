---
title: "Virtual Network로 HDInsight 확장 - Azure | Microsoft Docs"
description: "Azure Virtual Network를 사용하여 HDInsight 다른 클라우드 리소스 또는 데이터 센터에서 리소스에 연결하는 방법을 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 37b9b600-d7f8-4cb1-a04a-0b3a827c6dcc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: 380423ec42ad4905c73fcd57501102e9f7062e81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a><span data-ttu-id="b871f-103">Azure Virtual Network를 사용하여 Azure HDInsight 확장</span><span class="sxs-lookup"><span data-stu-id="b871f-103">Extend Azure HDInsight using an Azure Virtual Network</span></span>

<span data-ttu-id="b871f-104">[Azure Virtual Network](../virtual-network/virtual-networks-overview.md)에 HDInsight를 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-104">Learn how to use HDInsight with an [Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="b871f-105">Azure Virtual Network를 사용하면 다음 시나리오가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-105">Using an Azure Virtual Network enables the following scenarios:</span></span>

* <span data-ttu-id="b871f-106">온-프레미스 네트워크에서 HDInsight에 직접 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-106">Connecting to HDInsight directly from an on-premises network.</span></span>

* <span data-ttu-id="b871f-107">Azure Virtual Network에서 데이터 저장소에 HDInsight를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-107">Connecting HDInsight to data stores in an Azure Virtual network.</span></span>

* <span data-ttu-id="b871f-108">인터넷을 통해 공개적으로 사용할 수 없는 Hadoop 서비스에 직접 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-108">Directly accessing Hadoop services that are not available publicly over the internet.</span></span> <span data-ttu-id="b871f-109">예를 들어 Kafka API 또는 HBase Java API.</span><span class="sxs-lookup"><span data-stu-id="b871f-109">For example, Kafka APIs or the HBase Java API.</span></span>

> [!WARNING]
> <span data-ttu-id="b871f-110">이 문서의 정보를 이해하려면 TCP/IP 네트워킹에 대한 사전 지식이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-110">The information in this document requires an understanding of TCP/IP networking.</span></span> <span data-ttu-id="b871f-111">TCP/IP 네트워킹에 대해 잘 모르는 경우 이전에 프로덕션 네트워크를 수정한 사람과 협력하여 작업해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-111">If you are not familiar with TCP/IP networking, you should partner with someone who is before making modifications to production networks.</span></span>

## <a name="planning"></a><span data-ttu-id="b871f-112">계획</span><span class="sxs-lookup"><span data-stu-id="b871f-112">Planning</span></span>

<span data-ttu-id="b871f-113">다음은 가상 네트워크에 HDInsight를 설치하려고 할 때 대답해야 하는 질문입니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-113">The following are the questions that you must answer when planning to install HDInsight in a virtual network:</span></span>

* <span data-ttu-id="b871f-114">기존 가상 네트워크에 HDInsight 설치해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="b871f-114">Do you need to install HDInsight into an existing virtual network?</span></span> <span data-ttu-id="b871f-115">아니면 새 네트워크를 만드나요?</span><span class="sxs-lookup"><span data-stu-id="b871f-115">Or are you creating a new network?</span></span>

    <span data-ttu-id="b871f-116">기존 가상 네트워크를 사용하는 경우 HDInsight를 설치하기 전에 네트워크 구성을 수정해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-116">If you are using an existing virtual network, you may need to modify the network configuration before you can install HDInsight.</span></span> <span data-ttu-id="b871f-117">자세한 내용은 [기존 가상 네트워크에 HDInsight 추가](#existingvnet) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-117">For more information, see the [add HDInsight to an existing virtual network](#existingvnet) section.</span></span>

* <span data-ttu-id="b871f-118">HDInsight가 들어 있는 가상 네트워크를 다른 가상 네트워크 또는 온-프레미스 네트워크에 연결하시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="b871f-118">Do you want to connect the virtual network containing HDInsight to another virtual network or your on-premises network?</span></span>

    <span data-ttu-id="b871f-119">네트워크 간의 리소스로 쉽게 작업하려면 사용자 지정 DNS를 만들고 DNS 전달을 구성해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-119">To easily work with resources across networks, you may need to create a custom DNS and configure DNS forwarding.</span></span> <span data-ttu-id="b871f-120">자세한 내용은 [다중 네트워크 연결](#multinet) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-120">For more information, see the [connecting multiple networks](#multinet) section.</span></span>

* <span data-ttu-id="b871f-121">HDInsight로의 인바운드 또는 아웃바운드 트래픽을 제한/리디렉션하시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="b871f-121">Do you want to restrict/redirect inbound or outbound traffic to HDInsight?</span></span>

    <span data-ttu-id="b871f-122">HDInsight는 Azure 데이터 센터에서 특정 IP 주소와 무제한 통신을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-122">HDInsight must have unrestricted communication with specific IP addresses in the Azure data center.</span></span> <span data-ttu-id="b871f-123">또한 클라이언트 통신에 방화벽을 통해 허용해야 하는 여러 포트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-123">There are also several ports that must be allowed through firewalls for client communication.</span></span> <span data-ttu-id="b871f-124">자세한 내용은 [네트워크 트래픽 제어](#networktraffic) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-124">For more information, see the [controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="b871f-125"><a id="existingvnet"></a>기존 가상 네트워크에 HDInsight 추가</span><span class="sxs-lookup"><span data-stu-id="b871f-125"><a id="existingvnet"></a>Add HDInsight to an existing virtual network</span></span>

<span data-ttu-id="b871f-126">이 섹션의 단계를 사용하여 새 HDInsight를 기존 Azure Virtual Network에 추가하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-126">Use the steps in this section to discover how to add a new HDInsight to an existing Azure Virtual Network.</span></span>

> [!NOTE]
> <span data-ttu-id="b871f-127">기존 HDInsight 클러스터를 가상 네트워크에 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-127">You cannot add an existing HDInsight cluster into a virtual network.</span></span>

1. <span data-ttu-id="b871f-128">가상 네트워크에 클래식 또는 리소스 관리자 배포 모델을 사용하나요?</span><span class="sxs-lookup"><span data-stu-id="b871f-128">Are you using a classic or Resource Manager deployment model for the virtual network?</span></span>

    <span data-ttu-id="b871f-129">HDInsight 3.4 이상에는 리소스 관리자 가상 네트워크가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-129">HDInsight 3.4 and greater requires a Resource Manager virtual network.</span></span> <span data-ttu-id="b871f-130">이전 버전의 HDInsightㅇ는 클래식 가상 네트워크가 필요했습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-130">Earlier versions of HDInsight required a classic virtual network.</span></span>

    <span data-ttu-id="b871f-131">기존 네트워크가 클래식 가상 네트워크인 경우 리소스 관리자 가상 네트워크를 만든 후 둘을 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-131">If your existing network is a classic virtual network, then you must create a Resource Manager virtual network and then connect the two.</span></span> <span data-ttu-id="b871f-132">[새 VNet에 클래식 VNet 연결](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b871f-132">[Connecting classic VNets to new VNets](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span></span>

    <span data-ttu-id="b871f-133">조인된 후 리소스 관리자 네트워크에 설치된 HDInsight는 클래식 네트워크의 리소스와 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-133">Once joined, HDInsight installed in the Resource Manager network can interact with resources in the classic network.</span></span>

2. <span data-ttu-id="b871f-134">강제 터널링을 사용하나요?</span><span class="sxs-lookup"><span data-stu-id="b871f-134">Do you use forced tunneling?</span></span> <span data-ttu-id="b871f-135">강제 터널링은 검사 및 로깅을 위해 장치에 아웃바운드 인터넷 트래픽을 적용하는 서브넷 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-135">Forced tunneling is a subnet setting that forces outbound Internet traffic to a device for inspection and logging.</span></span> <span data-ttu-id="b871f-136">HDInsight는 강제 터널링을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-136">HDInsight does not support forced tunneling.</span></span> <span data-ttu-id="b871f-137">서브넷에 HDInsight를 설치하기 전에 강제 터널링을 제거하거나 HDInsight에 대해 새 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-137">Either remove forced tunneling before installing HDInsight into a subnet, or create a new subnet for HDInsight.</span></span>

3. <span data-ttu-id="b871f-138">가상 네트워크 내부 또는 외부로 트래픽을 제한하기 위해 네트워크 보안 그룹, 사용자 정의 경로 또는 Virtual Network 어플라이언스를 사용하나요?</span><span class="sxs-lookup"><span data-stu-id="b871f-138">Do you use network security groups, user-defined routes, or Virtual Network Appliances to restrict traffic into or out of the virtual network?</span></span>

    <span data-ttu-id="b871f-139">관리 서비스로 HDInsight를 사용하려면 Azure 데이터 센터에서 여러 IP 주소에 대한 무제한 액세스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-139">As a managed service, HDInsight requires unrestricted access to several IP addresses in the Azure data center.</span></span> <span data-ttu-id="b871f-140">이러한 IP 주소와의 통신을 허용하려면 기존의 모든 네트워크 보안 그룹 또는 사용자 정의 경로를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-140">To allow communication with these IP addresses, update any existing network security groups or user-defined routes.</span></span>

    <span data-ttu-id="b871f-141">HDInsight는 다양한 포트를 사용하는 여러 서비스를 호스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-141">HDInsight  hosts multiple services, which use a variety of ports.</span></span> <span data-ttu-id="b871f-142">이 포트로의 트래픽을 차단하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-142">Do not block traffic to these ports.</span></span> <span data-ttu-id="b871f-143">가상 어플라이언스 방화벽을 통과하도록 허용할 포트 목록은 [보안](#security) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-143">For a list of ports to allow through virtual appliance firewalls, see the [Security](#security) section.</span></span>

    <span data-ttu-id="b871f-144">기존 보안 구성을 찾으려면 다음 Azure PowerShell 또는 Azure CLI 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-144">To find your existing security configuration, use the following Azure PowerShell or Azure CLI commands:</span></span>

    * <span data-ttu-id="b871f-145">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="b871f-145">Network security groups</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="b871f-146">자세한 내용은 [네트워크 보안 그룹 문제 해결](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-146">For more information, see the [Troubleshoot network security groups](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) document.</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="b871f-147">네트워크 보안 그룹 규칙은 규칙 우선 순위에 따라 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-147">Network security group rules are applied in order based on rule priority.</span></span> <span data-ttu-id="b871f-148">트래픽 패턴과 일치하는 첫 번째 규칙이 적용되고 해당 트래픽에 대해서는 다른 규칙이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-148">The first rule that matches the traffic pattern is applied, and no others are applied for that traffic.</span></span> <span data-ttu-id="b871f-149">가장 허용적인 것부터 가장 허용적이지 않은 것 순서로 규칙을 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-149">Order rules from most permissive to least permissive.</span></span> <span data-ttu-id="b871f-150">자세한 내용은 [네트워크 보안 그룹을 사용하여 네트워크 트래픽 필터링](../virtual-network/virtual-networks-nsg.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-150">For more information, see the [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    * <span data-ttu-id="b871f-151">사용자 정의 경로</span><span class="sxs-lookup"><span data-stu-id="b871f-151">User-defined routes</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="b871f-152">자세한 내용은 [문제 해결 경로](../virtual-network/virtual-network-routes-troubleshoot-portal.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-152">For more information, see the [Troubleshoot routes](../virtual-network/virtual-network-routes-troubleshoot-portal.md) document.</span></span>

4. <span data-ttu-id="b871f-153">HDInsight 클러스터를 만들고 구성 중 Azure Virtual Network를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-153">Create an HDInsight cluster and select the Azure Virtual Network during configuration.</span></span> <span data-ttu-id="b871f-154">클러스터 만들기 프로세스를 이해하려면 다음 문서의 단계를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-154">Use the steps in the following documents to understand the cluster creation process:</span></span>

    * [<span data-ttu-id="b871f-155">Azure Portal을 사용하여 HDInsight 만들기</span><span class="sxs-lookup"><span data-stu-id="b871f-155">Create HDInsight using the Azure portal</span></span>](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [<span data-ttu-id="b871f-156">Azure PowerShell을 사용하여 HDInsight 만들기</span><span class="sxs-lookup"><span data-stu-id="b871f-156">Create HDInsight using Azure PowerShell</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
    * [<span data-ttu-id="b871f-157">Azure CLI 1.0을 사용하여 HDInsight 만들기</span><span class="sxs-lookup"><span data-stu-id="b871f-157">Create HDInsight using Azure CLI 1.0</span></span>](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [<span data-ttu-id="b871f-158">Azure Resource Manager 템플릿을 사용하여 HDInsight 만들기</span><span class="sxs-lookup"><span data-stu-id="b871f-158">Create HDInsight using an Azure Resource Manager template</span></span>](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > <span data-ttu-id="b871f-159">가상 네트워크에 HDInsight 추가하기는 선택적 구성 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-159">Adding HDInsight to a virtual network is an optional configuration step.</span></span> <span data-ttu-id="b871f-160">클러스터를 구성할 때 가상 네트워크를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-160">Be sure to select the virtual network when configuring the cluster.</span></span>

## <span data-ttu-id="b871f-161"><a id="multinet"></a>다중 네트워크 연결</span><span class="sxs-lookup"><span data-stu-id="b871f-161"><a id="multinet"></a>Connecting multiple networks</span></span>

<span data-ttu-id="b871f-162">다중 네트워크 구성에서 가장 큰 문제는 네트워크 간 이름 확인입니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-162">The biggest challenge with a multi-network configuration is name resolution between the networks.</span></span>

<span data-ttu-id="b871f-163">Azure는 가상 네트워크에 설치된 Azure 서비스에 대한 이름 확인을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-163">Azure provides name resolution for Azure services that are installed in a virtual network.</span></span> <span data-ttu-id="b871f-164">기본 제공 이름 확인을 통해 HDInsight는 FQDN(정규화된 도메인 이름)을 사용하여 다음 리소스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-164">This built-in name resolution allows HDInsight to connect to the following resources by using a fully qualified domain name (FQDN):</span></span>

* <span data-ttu-id="b871f-165">인터넷에서 사용할 수 있는 모든 리소스.</span><span class="sxs-lookup"><span data-stu-id="b871f-165">Any resource that is available on the internet.</span></span> <span data-ttu-id="b871f-166">예를 들어, microsoft.com, google.com.</span><span class="sxs-lookup"><span data-stu-id="b871f-166">For example, microsoft.com, google.com.</span></span>

* <span data-ttu-id="b871f-167">리소스의 __내부 DNS 이름__을 사용하여 동일한 Azure Virtual Network에 있는 모든 리소스.</span><span class="sxs-lookup"><span data-stu-id="b871f-167">Any resource that is in the same Azure Virtual Network, by using the __internal DNS name__ of the resource.</span></span> <span data-ttu-id="b871f-168">예를 들어 기본 이름 확인 기능을 사용할 경우, 다음은 HDInsight 작업자 노드에 할당된 내부 DNS 이름에 대한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-168">For example, when using the default name resolution, the following are example internal DNS names assigned to HDInsight worker nodes:</span></span>

    * <span data-ttu-id="b871f-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="b871f-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>
    * <span data-ttu-id="b871f-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="b871f-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>

    <span data-ttu-id="b871f-171">이러한 두 노드는 내부 DNS 이름을 사용하여 서로 직접 통신하고 HDInsight의 다른 노드와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-171">Both these nodes can communicate directly with each other, and other nodes in HDInsight, by using internal DNS names.</span></span>

<span data-ttu-id="b871f-172">기본 이름 확인에서는 HDInsight가 가상 네트워크에 조인된 네트워크에 있는 리소스 이름을 확인하도록 허용하지 __않습니다__.</span><span class="sxs-lookup"><span data-stu-id="b871f-172">The default name resolution does __not__ allow HDInsight to resolve the names of resources in networks that are joined to the virtual network.</span></span> <span data-ttu-id="b871f-173">예를 들어 온-프레미스 네트워크를 가상 네트워크에 조인하는 것이 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-173">For example, it is common to join your on-premises network to the virtual network.</span></span> <span data-ttu-id="b871f-174">기본 이름 확인만으로는, HDInsight가 이름으로 온-프레미스 네트워크의 리소스에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-174">With only the default name resolution, HDInsight cannot access resources in the on-premises network by name.</span></span> <span data-ttu-id="b871f-175">반대도 마찬가지입니다. 온-프레미스 네트워크의 리소스는 이름으로 가상 네트워크의 리소스에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-175">The opposite is also true, resources in your on-premises network cannot access resources in the virtual network by name.</span></span>

> [!WARNING]
> <span data-ttu-id="b871f-176">사용자 지정 DNS 서버를 만들고 이 서버를 사용하도록 가상 네트워크를 구성한 후 HDInsight 클러스터를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-176">You must create the custom DNS server and configure the virtual network to use it before creating the HDInsight cluster.</span></span>

<span data-ttu-id="b871f-177">가상 네트워크 및 조인된 네트워크의 리소스 간에 이름 확인을 사용하려면 다음 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-177">To enable name resolution between the virtual network and resources in joined networks, you must perform the following actions:</span></span>

1. <span data-ttu-id="b871f-178">HDInsight를 설치할 계획인 Azure Virtual Network에서 사용자 지정 DNS 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-178">Create a custom DNS server in the Azure Virtual Network where you plan to install HDInsight.</span></span>

2. <span data-ttu-id="b871f-179">사용자 지정 DNS 서버를 사용하도록 가상 네트워크를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-179">Configure the virtual network to use the custom DNS server.</span></span>

3. <span data-ttu-id="b871f-180">가상 네트워크에 대해 Azure에서 할당한 DNS 접미사를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-180">Find the Azure assigned DNS suffix for your virtual network.</span></span> <span data-ttu-id="b871f-181">이 값은 `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-181">This value is similar to `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span></span> <span data-ttu-id="b871f-182">DNS 접미사를 찾는 방법에 대한 자세한 내용은 [예제: 사용자 지정 DNS](#example-dns) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-182">For information on finding the DNS suffix, see the [Example: Custom DNS](#example-dns) section.</span></span>

4. <span data-ttu-id="b871f-183">DNS 서버 간에 전달을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-183">Configure forwarding between the DNS servers.</span></span> <span data-ttu-id="b871f-184">구성은 원격 네트워크의 유형에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-184">The configuration depends on the type of remote network.</span></span>

    * <span data-ttu-id="b871f-185">원격 네트워크가 온-프레미스 네트워크인 경우 다음과 같이 DNS를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-185">If the remote network is an on-premises network, configure DNS as follows:</span></span>
        
        * <span data-ttu-id="b871f-186">__사용자 지정 DNS(가상 네트워크에서)__:</span><span class="sxs-lookup"><span data-stu-id="b871f-186">__Custom DNS__ (in the virtual network):</span></span>

            * <span data-ttu-id="b871f-187">가상 네트워크의 DNS 접미사에 대한 요청을 Azure 재귀 확인자(168.63.129.16)에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-187">Forward requests for the DNS suffix of the virtual network to the Azure recursive resolver (168.63.129.16).</span></span> <span data-ttu-id="b871f-188">Azure에서 가상 네트워크의 리소스에 대한 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-188">Azure handles requests for resources in the virtual network</span></span>

            * <span data-ttu-id="b871f-189">다른 모든 요청을 온-프레미스 DNS 서버에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-189">Forward all other requests to the on-premises DNS server.</span></span> <span data-ttu-id="b871f-190">온-프레미스 DNS가 Microsoft.com과 같은 인터넷 리소스에 대한 요청을 비롯한 기타 모든 이름 확인 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-190">The on-premises DNS handles all other name resolution requests, even requests for internet resources such as Microsoft.com.</span></span>

        * <span data-ttu-id="b871f-191">__온-프레미스 DNS__: 가상 네트워크 DNS 접미사에 대한 요청을 사용자 지정 DNS 서버에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-191">__On-premises DNS__: Forward requests for the virtual network DNS suffix to the custom DNS server.</span></span> <span data-ttu-id="b871f-192">그러면 사용자 지정 DNS 서버에서 Azure 재귀 확인자로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-192">The custom DNS server then forwards to the Azure recursive resolver.</span></span>

        <span data-ttu-id="b871f-193">이 구성은 가상 네트워크에 대한 DNS 접미사를 포함하는 정규화된 도메인 이름 요청을 사용자 지정 DNS 서버로 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-193">This configuration routes requests for fully qualified domain names that contain the DNS suffix of the virtual network to the custom DNS server.</span></span> <span data-ttu-id="b871f-194">공용 인터넷 주소를 포함한 모든 다른 요청은 온-프레미스 DNS 서버에서 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-194">All other requests (even for public internet addresses) are handled by the on-premises DNS server.</span></span>

    * <span data-ttu-id="b871f-195">원격 네트워크가 다른 Azure Virtual Network인 경우 다음과 같이 DNS를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-195">If the remote network is another Azure Virtual Network, configure DNS as follows:</span></span>

        * <span data-ttu-id="b871f-196">__사용자 지정 DNS(각 가상 네트워크에서)__:</span><span class="sxs-lookup"><span data-stu-id="b871f-196">__Custom DNS__ (in each virtual network):</span></span>

            * <span data-ttu-id="b871f-197">가상 네트워크 DNS 접미사에 대한 요청은 사용자 지정 DNS 서버에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-197">Requests for the DNS suffix of the virtual networks are forwarded to the custom DNS servers.</span></span> <span data-ttu-id="b871f-198">각 가상 네트워크에 있는 DNS는 해당 네트워크 내에서 리소스를 확인하는 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-198">The DNS in each virtual network is responsible for resolving resources within its network.</span></span>

            * <span data-ttu-id="b871f-199">다른 모든 요청은 Azure 재귀 확인자에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-199">Forward all other requests to the Azure recursive resolver.</span></span> <span data-ttu-id="b871f-200">재귀 확인자는 로컬 및 인터넷 리소스를 확인하는 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-200">The recursive resolver is responsible for resolving local and internet resources.</span></span>

        <span data-ttu-id="b871f-201">각 네트워크의 DNS 서버는 DNS 접미사에 따라 요청을 다른 곳으로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-201">The DNS server for each network forwards requests to the other, based on DNS suffix.</span></span> <span data-ttu-id="b871f-202">다른 요청은 Azure 재귀 확인자를 사용하여 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-202">Other requests are resolved using the Azure recursive resolver.</span></span>

    <span data-ttu-id="b871f-203">각 구성에 대한 예는 [예제: 사용자 지정 DNS](#example-dns) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-203">For an example of each configuration, see the [Example: Custom DNS](#example-dns) section.</span></span>

<span data-ttu-id="b871f-204">자세한 내용은 [VM 및 역할 인스턴스의 이름 확인](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-204">For more information, see the [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) document.</span></span>

## <a name="directly-connect-to-hadoop-services"></a><span data-ttu-id="b871f-205">Hadoop 서비스에 직접 연결</span><span class="sxs-lookup"><span data-stu-id="b871f-205">Directly connect to Hadoop services</span></span>

<span data-ttu-id="b871f-206">HDInsight에 대한 대부분의 설명서는 인터넷을 통해 클러스터에 액세스할 수 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-206">Most documentation on HDInsight assumes that you have access to the cluster over the internet.</span></span> <span data-ttu-id="b871f-207">예를 들어 https://CLUSTERNAME.azurehdinsight.net에서 클러스터에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-207">For example, that you can connect to the cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="b871f-208">이 주소는 인터넷에서 액세스를 제한하는 데 NSG 또는 UDR을 사용한 경우에는 사용할 수 없는 공용 게이트웨이를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-208">This address uses the public gateway, which is not available if you have used NSGs or UDRs to restrict access from the internet.</span></span>

<span data-ttu-id="b871f-209">가상 네트워크를 통해 Ambari 및 다른 웹 페이지에 연결하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-209">To connect to Ambari and other web pages through the virtual network, use the following steps:</span></span>

1. <span data-ttu-id="b871f-210">HDInsight 클러스터 노드의 내부 FQDN(정규화된 도메인 이름)을 검색하려면 다음 방법 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-210">To discover the internal fully qualified domain names (FQDN) of the HDInsight cluster nodes, use one of the following methods:</span></span>

    ```powershell
    $resourceGroupName = "The resource group that contains the virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

    <span data-ttu-id="b871f-211">반환된 노드 목록에서 헤드 노드에 대한 FQDN을 찾아 Ambari 및 기타 웹 서비스에 연결하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-211">In the list of nodes returned, find the FQDN for the head nodes and use the FQDNs to connect to Ambari and other web services.</span></span> <span data-ttu-id="b871f-212">예를 들어 `http://<headnode-fqdn>:8080`을 사용하여 Ambari에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-212">For example, use `http://<headnode-fqdn>:8080` to access Ambari.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b871f-213">헤드 노드에서 호스팅되는 일부 서비스는 한 번에 한 노드에서만 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-213">Some services hosted on the head nodes are only active on one node at a time.</span></span> <span data-ttu-id="b871f-214">한 헤드 노드에서 서비스에 액세스하려고 하고 404 오류가 반환되면 다른 헤드 노드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-214">If you try accessing a service on one head node and it returns a 404 error, switch to the other head node.</span></span>

2. <span data-ttu-id="b871f-215">서비스가 제공되는 노드 및 포트를 확인하려면 [HDInsight의 Hadoop 서비스에서 사용하는 포트](./hdinsight-hadoop-port-settings-for-services.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-215">To determine the node and port that a service is available on, see the [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

## <span data-ttu-id="b871f-216"><a id="networktraffic"></a> 네트워크 트래픽 제어</span><span class="sxs-lookup"><span data-stu-id="b871f-216"><a id="networktraffic"></a> Controlling network traffic</span></span>

<span data-ttu-id="b871f-217">Azure Virtual Networks의 네트워크 트래픽은 다음 방법을 사용하여 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-217">Network traffic in an Azure Virtual Networks can be controlled using the following methods:</span></span>

* <span data-ttu-id="b871f-218">**NSG(네트워크 보안 그룹)**를 통해 네트워크로의 인바운드 및 아웃바운드 트래픽을 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-218">**Network security groups** (NSG) allow you to filter inbound and outbound traffic to the network.</span></span> <span data-ttu-id="b871f-219">자세한 내용은 [네트워크 보안 그룹을 사용하여 네트워크 트래픽 필터링](../virtual-network/virtual-networks-nsg.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-219">For more information, see the [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    > [!WARNING]
    > <span data-ttu-id="b871f-220">HDInsight는 아웃바운드 트래픽을 제한하도록 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-220">HDInsight does not support restricting outbound traffic.</span></span>

* <span data-ttu-id="b871f-221">**UDR(사용자 정의 경로)**은 네트워크에 있는 리소스 간에 트래픽이 흐르는 방식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-221">**User-defined routes** (UDR) define how traffic flows between resources in the network.</span></span> <span data-ttu-id="b871f-222">자세한 내용은 [사용자 정의 경로 및 IP 전달](../virtual-network/virtual-networks-udr-overview.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-222">For more information, see the [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md) document.</span></span>

* <span data-ttu-id="b871f-223">**네트워크 가상 어플라이언스**는 방화벽 및 라우터와 같은 장치 기능을 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-223">**Network virtual appliances** replicate the functionality of devices such as firewalls and routers.</span></span> <span data-ttu-id="b871f-224">자세한 내용은 [네트워크 어플라이언스](https://azure.microsoft.com/solutions/network-appliances) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-224">For more information, see the [Network Appliances](https://azure.microsoft.com/solutions/network-appliances) document.</span></span>

<span data-ttu-id="b871f-225">관리 서비스로 HDInsight를 사용하려면 Azure 클라우드에서 Azure 상태 및 관리 서비스에 대한 무제한 액세스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-225">As a managed service, HDInsight requires unrestricted access to Azure health and management services in the Azure cloud.</span></span> <span data-ttu-id="b871f-226">NSG 및 UDR을 사용할 때는 이러한 서비스에서 HDInsight와 계속 통신할 수 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-226">When using NSGs and UDRs, you must ensure that HDInsight these services can still communicate with HDInsight.</span></span>

<span data-ttu-id="b871f-227">HDInsight는 여러 포트에서 서비스를 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-227">HDInsight exposes services on several ports.</span></span> <span data-ttu-id="b871f-228">가상 어플라이언스 방화벽을 사용할 경우 이러한 서비스에 사용된 포트에서 트래픽을 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-228">When using a virtual appliance firewall, you must allow traffic on the ports used for these services.</span></span> <span data-ttu-id="b871f-229">자세한 내용은 [필수 포트] 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-229">For more information, see the [Required ports] section.</span></span>

### <span data-ttu-id="b871f-230"><a id="hdinsight-ip"></a> 네트워크 보안 그룹 및 사용자 정의 경로가 있는 HDInsight</span><span class="sxs-lookup"><span data-stu-id="b871f-230"><a id="hdinsight-ip"></a> HDInsight with network security groups and user-defined routes</span></span>

<span data-ttu-id="b871f-231">네트워크 트래픽을 제어하는 데 **네트워크 보안 그룹** 또는 **사용자 정의 경로**를 사용할 계획인 경우 HDInsight를 설치하기 전에 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-231">If you plan on using **network security groups** or **user-defined routes** to control network traffic, perform the following actions before installing HDInsight:</span></span>

1. <span data-ttu-id="b871f-232">HDInsight에 대해 사용할 Azure 지역을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-232">Identify the Azure region that you plan to use for HDInsight.</span></span>

2. <span data-ttu-id="b871f-233">HDInsight에 필요한 IP 주소를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-233">Identify the IP addresses required by HDInsight.</span></span> <span data-ttu-id="b871f-234">자세한 내용은 [HDInsight에 필요한 IP 주소](#hdinsight-ip) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-234">For more information, see the [IP Addresses required by HDInsight](#hdinsight-ip) section.</span></span>

3. <span data-ttu-id="b871f-235">HDInsight을 설치하려는 서브넷에 대한 사용자 정의 경로 또는 네트워크 보안 그룹을 만들거나 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-235">Create or modify the network security groups or user-defined routes for the subnet that you plan to install HDInsight into.</span></span>

    * <span data-ttu-id="b871f-236">__네트워크 보안 그룹__: IP 주소에서 포트 __443__에 __인바운드__ 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-236">__Network security groups__: allow __inbound__ traffic on port __443__ from the IP addresses.</span></span>
    * <span data-ttu-id="b871f-237">__사용자 정의 경로__: 각 IP 주소에 대한 경로를 만들고 __다음 홉 유형__을 __인터넷__으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-237">__User-defined routes__: create a route to each IP address and set the __Next hop type__ to __Internet__.</span></span>

<span data-ttu-id="b871f-238">네트워크 보안 그룹 또는 사용자 정의 경로에 대한 자세한 내용은 다음 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-238">For more information on network security groups or user-defined routes, see the following documentation:</span></span>

* [<span data-ttu-id="b871f-239">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="b871f-239">Network security group</span></span>](../virtual-network/virtual-networks-nsg.md)

* [<span data-ttu-id="b871f-240">사용자 정의 경로</span><span class="sxs-lookup"><span data-stu-id="b871f-240">User-defined routes</span></span>](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a><span data-ttu-id="b871f-241">강제 터널링</span><span class="sxs-lookup"><span data-stu-id="b871f-241">Forced tunneling</span></span>

<span data-ttu-id="b871f-242">강제 터널링은 서브넷의 모든 트래픽이 특정 네트워크 또는 위치(예: 온-프레미스 네트워크)로 적용되는 사용자 정의 라우팅 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-242">Forced tunneling is a user-defined routing configuration where all traffic from a subnet is forced to a specific network or location, such as your on-premises network.</span></span> <span data-ttu-id="b871f-243">HDInsight는 강제 터널링을 지원하지 __않습니다.__</span><span class="sxs-lookup"><span data-stu-id="b871f-243">HDInsight does __not__ support forced tunneling.</span></span>

## <span data-ttu-id="b871f-244"><a id="hdinsight-ip"></a> 필수 IP 주소</span><span class="sxs-lookup"><span data-stu-id="b871f-244"><a id="hdinsight-ip"></a> Required IP addresses</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b871f-245">Azure 상태 및 관리 서비스는 HDInsight와 통신할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-245">The Azure health and management services must be able to communicate with HDInsight.</span></span> <span data-ttu-id="b871f-246">네트워크 보안 그룹 또는 사용자 정의 경로를 사용하는 경우 이러한 서비스의 IP 주소에서 HDInsight로 트래픽이 전송되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-246">If you use network security groups or user-defined routes, allow traffic from the IP addresses for these services to reach HDInsight.</span></span>
>
> <span data-ttu-id="b871f-247">트래픽을 제어하는 네트워크 보안 그룹 또는 사용자 정의 경로를 사용하지 않는 경우 이 섹션을 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-247">If you do not use network security groups or user-defined routes to control traffic, you can ignore this section.</span></span>

<span data-ttu-id="b871f-248">네트워크 보안 그룹 또는 사용자 정의 경로를 사용하는 경우 Azure 상태 및 관리 서비스의 트래픽이 HDInsight에 도달하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-248">If you use network security groups or user-defined routes, you must allow traffic from the Azure health and management services to reach HDInsight.</span></span> <span data-ttu-id="b871f-249">다음 단계를 사용하여 다음을 허용해야 하는 IP 주소를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-249">Use the following steps to find the IP addresses that must be allowed:</span></span>

1. <span data-ttu-id="b871f-250">다음 IP 주소에서 트래픽을 항상 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-250">You must always allow traffic from the following IP addresses:</span></span>

    | <span data-ttu-id="b871f-251">IP 주소</span><span class="sxs-lookup"><span data-stu-id="b871f-251">IP address</span></span> | <span data-ttu-id="b871f-252">허용되는 포트</span><span class="sxs-lookup"><span data-stu-id="b871f-252">Allowed port</span></span> | <span data-ttu-id="b871f-253">방향</span><span class="sxs-lookup"><span data-stu-id="b871f-253">Direction</span></span> |
    | ---- | ----- | ----- |
    | <span data-ttu-id="b871f-254">168.61.49.99</span><span class="sxs-lookup"><span data-stu-id="b871f-254">168.61.49.99</span></span> | <span data-ttu-id="b871f-255">443</span><span class="sxs-lookup"><span data-stu-id="b871f-255">443</span></span> | <span data-ttu-id="b871f-256">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-256">Inbound</span></span> |
    | <span data-ttu-id="b871f-257">23.99.5.239</span><span class="sxs-lookup"><span data-stu-id="b871f-257">23.99.5.239</span></span> | <span data-ttu-id="b871f-258">443</span><span class="sxs-lookup"><span data-stu-id="b871f-258">443</span></span> | <span data-ttu-id="b871f-259">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-259">Inbound</span></span> |
    | <span data-ttu-id="b871f-260">168.61.48.131</span><span class="sxs-lookup"><span data-stu-id="b871f-260">168.61.48.131</span></span> | <span data-ttu-id="b871f-261">443</span><span class="sxs-lookup"><span data-stu-id="b871f-261">443</span></span> | <span data-ttu-id="b871f-262">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-262">Inbound</span></span> |
    | <span data-ttu-id="b871f-263">138.91.141.162</span><span class="sxs-lookup"><span data-stu-id="b871f-263">138.91.141.162</span></span> | <span data-ttu-id="b871f-264">443</span><span class="sxs-lookup"><span data-stu-id="b871f-264">443</span></span> | <span data-ttu-id="b871f-265">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-265">Inbound</span></span> |

2. <span data-ttu-id="b871f-266">HDInsight 클러스터가 다음 지역 중에 있으면 해당 지역에 대해 나열된 IP 주소에서 트래픽을 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-266">If your HDInsight cluster is in one of the following regions, then you must allow traffic from the IP addresses listed for the region:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b871f-267">사용하는 Azure 지역이 나열되지 않으면 1단계의 4가지 IP 주소만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-267">If the Azure region you are using is not listed, then only use the four IP addresses from step 1.</span></span>

    | <span data-ttu-id="b871f-268">국가</span><span class="sxs-lookup"><span data-stu-id="b871f-268">Country</span></span> | <span data-ttu-id="b871f-269">지역</span><span class="sxs-lookup"><span data-stu-id="b871f-269">Region</span></span> | <span data-ttu-id="b871f-270">허용된 IP 주소</span><span class="sxs-lookup"><span data-stu-id="b871f-270">Allowed IP addresses</span></span> | <span data-ttu-id="b871f-271">허용되는 포트</span><span class="sxs-lookup"><span data-stu-id="b871f-271">Allowed port</span></span> | <span data-ttu-id="b871f-272">방향</span><span class="sxs-lookup"><span data-stu-id="b871f-272">Direction</span></span> |
    | ---- | ---- | ---- | ---- | ----- |
    | <span data-ttu-id="b871f-273">아시아</span><span class="sxs-lookup"><span data-stu-id="b871f-273">Asia</span></span> | <span data-ttu-id="b871f-274">동아시아</span><span class="sxs-lookup"><span data-stu-id="b871f-274">East Asia</span></span> | <span data-ttu-id="b871f-275">23.102.235.122</span><span class="sxs-lookup"><span data-stu-id="b871f-275">23.102.235.122</span></span></br><span data-ttu-id="b871f-276">52.175.38.134</span><span class="sxs-lookup"><span data-stu-id="b871f-276">52.175.38.134</span></span> | <span data-ttu-id="b871f-277">443</span><span class="sxs-lookup"><span data-stu-id="b871f-277">443</span></span> | <span data-ttu-id="b871f-278">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-278">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="b871f-279">동남아시아</span><span class="sxs-lookup"><span data-stu-id="b871f-279">Southeast Asia</span></span> | <span data-ttu-id="b871f-280">13.76.245.160</span><span class="sxs-lookup"><span data-stu-id="b871f-280">13.76.245.160</span></span></br><span data-ttu-id="b871f-281">13.76.136.249</span><span class="sxs-lookup"><span data-stu-id="b871f-281">13.76.136.249</span></span> | <span data-ttu-id="b871f-282">443</span><span class="sxs-lookup"><span data-stu-id="b871f-282">443</span></span> | <span data-ttu-id="b871f-283">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-283">Inbound</span></span> |
    | <span data-ttu-id="b871f-284">오스트레일리아</span><span class="sxs-lookup"><span data-stu-id="b871f-284">Australia</span></span> | <span data-ttu-id="b871f-285">오스트레일리아 동부</span><span class="sxs-lookup"><span data-stu-id="b871f-285">Australia East</span></span> | <span data-ttu-id="b871f-286">104.210.84.115</span><span class="sxs-lookup"><span data-stu-id="b871f-286">104.210.84.115</span></span></br><span data-ttu-id="b871f-287">13.75.152.195</span><span class="sxs-lookup"><span data-stu-id="b871f-287">13.75.152.195</span></span> | <span data-ttu-id="b871f-288">443</span><span class="sxs-lookup"><span data-stu-id="b871f-288">443</span></span> | <span data-ttu-id="b871f-289">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-289">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="b871f-290">오스트레일리아 남동부</span><span class="sxs-lookup"><span data-stu-id="b871f-290">Australia Southeast</span></span> | <span data-ttu-id="b871f-291">13.77.2.56</span><span class="sxs-lookup"><span data-stu-id="b871f-291">13.77.2.56</span></span></br><span data-ttu-id="b871f-292">13.77.2.94</span><span class="sxs-lookup"><span data-stu-id="b871f-292">13.77.2.94</span></span> | <span data-ttu-id="b871f-293">443</span><span class="sxs-lookup"><span data-stu-id="b871f-293">443</span></span> | <span data-ttu-id="b871f-294">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-294">Inbound</span></span> |
    | <span data-ttu-id="b871f-295">브라질</span><span class="sxs-lookup"><span data-stu-id="b871f-295">Brazil</span></span> | <span data-ttu-id="b871f-296">브라질 남부</span><span class="sxs-lookup"><span data-stu-id="b871f-296">Brazil South</span></span> | <span data-ttu-id="b871f-297">191.235.84.104</span><span class="sxs-lookup"><span data-stu-id="b871f-297">191.235.84.104</span></span></br><span data-ttu-id="b871f-298">191.235.87.113</span><span class="sxs-lookup"><span data-stu-id="b871f-298">191.235.87.113</span></span> | <span data-ttu-id="b871f-299">443</span><span class="sxs-lookup"><span data-stu-id="b871f-299">443</span></span> | <span data-ttu-id="b871f-300">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-300">Inbound</span></span> |
    | <span data-ttu-id="b871f-301">캐나다</span><span class="sxs-lookup"><span data-stu-id="b871f-301">Canada</span></span> | <span data-ttu-id="b871f-302">캐나다 동부</span><span class="sxs-lookup"><span data-stu-id="b871f-302">Canada East</span></span> | <span data-ttu-id="b871f-303">52.229.127.96</span><span class="sxs-lookup"><span data-stu-id="b871f-303">52.229.127.96</span></span></br><span data-ttu-id="b871f-304">52.229.123.172</span><span class="sxs-lookup"><span data-stu-id="b871f-304">52.229.123.172</span></span> | <span data-ttu-id="b871f-305">443</span><span class="sxs-lookup"><span data-stu-id="b871f-305">443</span></span> | <span data-ttu-id="b871f-306">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-306">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="b871f-307">캐나다 중부</span><span class="sxs-lookup"><span data-stu-id="b871f-307">Canada Central</span></span> | <span data-ttu-id="b871f-308">52.228.37.66</span><span class="sxs-lookup"><span data-stu-id="b871f-308">52.228.37.66</span></span></br><span data-ttu-id="b871f-309">52.228.45.222</span><span class="sxs-lookup"><span data-stu-id="b871f-309">52.228.45.222</span></span> | <span data-ttu-id="b871f-310">443</span><span class="sxs-lookup"><span data-stu-id="b871f-310">443</span></span> | <span data-ttu-id="b871f-311">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-311">Inbound</span></span> |
    | <span data-ttu-id="b871f-312">중국</span><span class="sxs-lookup"><span data-stu-id="b871f-312">China</span></span> | <span data-ttu-id="b871f-313">중국 북부</span><span class="sxs-lookup"><span data-stu-id="b871f-313">China North</span></span> | <span data-ttu-id="b871f-314">42.159.96.170</span><span class="sxs-lookup"><span data-stu-id="b871f-314">42.159.96.170</span></span></br><span data-ttu-id="b871f-315">139.217.2.219</span><span class="sxs-lookup"><span data-stu-id="b871f-315">139.217.2.219</span></span> | <span data-ttu-id="b871f-316">443</span><span class="sxs-lookup"><span data-stu-id="b871f-316">443</span></span> | <span data-ttu-id="b871f-317">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-317">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="b871f-318">중국 동부</span><span class="sxs-lookup"><span data-stu-id="b871f-318">China East</span></span> | <span data-ttu-id="b871f-319">42.159.198.178</span><span class="sxs-lookup"><span data-stu-id="b871f-319">42.159.198.178</span></span></br><span data-ttu-id="b871f-320">42.159.234.157</span><span class="sxs-lookup"><span data-stu-id="b871f-320">42.159.234.157</span></span> | <span data-ttu-id="b871f-321">443</span><span class="sxs-lookup"><span data-stu-id="b871f-321">443</span></span> | <span data-ttu-id="b871f-322">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-322">Inbound</span></span> |
    | <span data-ttu-id="b871f-323">유럽</span><span class="sxs-lookup"><span data-stu-id="b871f-323">Europe</span></span> | <span data-ttu-id="b871f-324">북유럽</span><span class="sxs-lookup"><span data-stu-id="b871f-324">North Europe</span></span> | <span data-ttu-id="b871f-325">52.164.210.96</span><span class="sxs-lookup"><span data-stu-id="b871f-325">52.164.210.96</span></span></br><span data-ttu-id="b871f-326">13.74.153.132</span><span class="sxs-lookup"><span data-stu-id="b871f-326">13.74.153.132</span></span> | <span data-ttu-id="b871f-327">443</span><span class="sxs-lookup"><span data-stu-id="b871f-327">443</span></span> | <span data-ttu-id="b871f-328">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-328">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="b871f-329">서유럽</span><span class="sxs-lookup"><span data-stu-id="b871f-329">West Europe</span></span>| <span data-ttu-id="b871f-330">52.166.243.90</span><span class="sxs-lookup"><span data-stu-id="b871f-330">52.166.243.90</span></span></br><span data-ttu-id="b871f-331">52.174.36.244</span><span class="sxs-lookup"><span data-stu-id="b871f-331">52.174.36.244</span></span> | <span data-ttu-id="b871f-332">443</span><span class="sxs-lookup"><span data-stu-id="b871f-332">443</span></span> | <span data-ttu-id="b871f-333">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-333">Inbound</span></span> |
    | <span data-ttu-id="b871f-334">독일</span><span class="sxs-lookup"><span data-stu-id="b871f-334">Germany</span></span> | <span data-ttu-id="b871f-335">독일 중부</span><span class="sxs-lookup"><span data-stu-id="b871f-335">Germany Central</span></span> | <span data-ttu-id="b871f-336">51.4.146.68</span><span class="sxs-lookup"><span data-stu-id="b871f-336">51.4.146.68</span></span></br><span data-ttu-id="b871f-337">51.4.146.80</span><span class="sxs-lookup"><span data-stu-id="b871f-337">51.4.146.80</span></span> | <span data-ttu-id="b871f-338">443</span><span class="sxs-lookup"><span data-stu-id="b871f-338">443</span></span> | <span data-ttu-id="b871f-339">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-339">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="b871f-340">독일 북동부</span><span class="sxs-lookup"><span data-stu-id="b871f-340">Germany Northeast</span></span> | <span data-ttu-id="b871f-341">51.5.150.132</span><span class="sxs-lookup"><span data-stu-id="b871f-341">51.5.150.132</span></span></br><span data-ttu-id="b871f-342">51.5.144.101</span><span class="sxs-lookup"><span data-stu-id="b871f-342">51.5.144.101</span></span> | <span data-ttu-id="b871f-343">443</span><span class="sxs-lookup"><span data-stu-id="b871f-343">443</span></span> | <span data-ttu-id="b871f-344">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-344">Inbound</span></span> |
    | <span data-ttu-id="b871f-345">인도</span><span class="sxs-lookup"><span data-stu-id="b871f-345">India</span></span> | <span data-ttu-id="b871f-346">인도 중부</span><span class="sxs-lookup"><span data-stu-id="b871f-346">Central India</span></span> | <span data-ttu-id="b871f-347">52.172.153.209</span><span class="sxs-lookup"><span data-stu-id="b871f-347">52.172.153.209</span></span></br><span data-ttu-id="b871f-348">52.172.152.49</span><span class="sxs-lookup"><span data-stu-id="b871f-348">52.172.152.49</span></span> | <span data-ttu-id="b871f-349">443</span><span class="sxs-lookup"><span data-stu-id="b871f-349">443</span></span> | <span data-ttu-id="b871f-350">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-350">Inbound</span></span> |
    | <span data-ttu-id="b871f-351">일본</span><span class="sxs-lookup"><span data-stu-id="b871f-351">Japan</span></span> | <span data-ttu-id="b871f-352">일본 동부</span><span class="sxs-lookup"><span data-stu-id="b871f-352">Japan East</span></span> | <span data-ttu-id="b871f-353">13.78.125.90</span><span class="sxs-lookup"><span data-stu-id="b871f-353">13.78.125.90</span></span></br><span data-ttu-id="b871f-354">13.78.89.60</span><span class="sxs-lookup"><span data-stu-id="b871f-354">13.78.89.60</span></span> | <span data-ttu-id="b871f-355">443</span><span class="sxs-lookup"><span data-stu-id="b871f-355">443</span></span> | <span data-ttu-id="b871f-356">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-356">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="b871f-357">일본 서부</span><span class="sxs-lookup"><span data-stu-id="b871f-357">Japan West</span></span> | <span data-ttu-id="b871f-358">40.74.125.69</span><span class="sxs-lookup"><span data-stu-id="b871f-358">40.74.125.69</span></span></br><span data-ttu-id="b871f-359">138.91.29.150</span><span class="sxs-lookup"><span data-stu-id="b871f-359">138.91.29.150</span></span> | <span data-ttu-id="b871f-360">443</span><span class="sxs-lookup"><span data-stu-id="b871f-360">443</span></span> | <span data-ttu-id="b871f-361">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-361">Inbound</span></span> |
    | <span data-ttu-id="b871f-362">한국</span><span class="sxs-lookup"><span data-stu-id="b871f-362">Korea</span></span> | <span data-ttu-id="b871f-363">한국 중부</span><span class="sxs-lookup"><span data-stu-id="b871f-363">Korea Central</span></span> | <span data-ttu-id="b871f-364">52.231.39.142</span><span class="sxs-lookup"><span data-stu-id="b871f-364">52.231.39.142</span></span></br><span data-ttu-id="b871f-365">52.231.36.209</span><span class="sxs-lookup"><span data-stu-id="b871f-365">52.231.36.209</span></span> | <span data-ttu-id="b871f-366">433</span><span class="sxs-lookup"><span data-stu-id="b871f-366">433</span></span> | <span data-ttu-id="b871f-367">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-367">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="b871f-368">한국 남부</span><span class="sxs-lookup"><span data-stu-id="b871f-368">Korea South</span></span> | <span data-ttu-id="b871f-369">52.231.203.16</span><span class="sxs-lookup"><span data-stu-id="b871f-369">52.231.203.16</span></span></br><span data-ttu-id="b871f-370">52.231.205.214</span><span class="sxs-lookup"><span data-stu-id="b871f-370">52.231.205.214</span></span> | <span data-ttu-id="b871f-371">443</span><span class="sxs-lookup"><span data-stu-id="b871f-371">443</span></span> | <span data-ttu-id="b871f-372">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-372">Inbound</span></span>
    | <span data-ttu-id="b871f-373">영국</span><span class="sxs-lookup"><span data-stu-id="b871f-373">United Kingdom</span></span> | <span data-ttu-id="b871f-374">영국 서부</span><span class="sxs-lookup"><span data-stu-id="b871f-374">UK West</span></span> | <span data-ttu-id="b871f-375">51.141.13.110</span><span class="sxs-lookup"><span data-stu-id="b871f-375">51.141.13.110</span></span></br><span data-ttu-id="b871f-376">51.141.7.20</span><span class="sxs-lookup"><span data-stu-id="b871f-376">51.141.7.20</span></span> | <span data-ttu-id="b871f-377">443</span><span class="sxs-lookup"><span data-stu-id="b871f-377">443</span></span> | <span data-ttu-id="b871f-378">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-378">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="b871f-379">영국 남부</span><span class="sxs-lookup"><span data-stu-id="b871f-379">UK South</span></span> | <span data-ttu-id="b871f-380">51.140.47.39</span><span class="sxs-lookup"><span data-stu-id="b871f-380">51.140.47.39</span></span></br><span data-ttu-id="b871f-381">51.140.52.16</span><span class="sxs-lookup"><span data-stu-id="b871f-381">51.140.52.16</span></span> | <span data-ttu-id="b871f-382">443</span><span class="sxs-lookup"><span data-stu-id="b871f-382">443</span></span> | <span data-ttu-id="b871f-383">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-383">Inbound</span></span> |
    | <span data-ttu-id="b871f-384">미국</span><span class="sxs-lookup"><span data-stu-id="b871f-384">United States</span></span> | <span data-ttu-id="b871f-385">미국 중부</span><span class="sxs-lookup"><span data-stu-id="b871f-385">Central US</span></span> | <span data-ttu-id="b871f-386">13.67.223.215</span><span class="sxs-lookup"><span data-stu-id="b871f-386">13.67.223.215</span></span></br><span data-ttu-id="b871f-387">40.86.83.253</span><span class="sxs-lookup"><span data-stu-id="b871f-387">40.86.83.253</span></span> | <span data-ttu-id="b871f-388">443</span><span class="sxs-lookup"><span data-stu-id="b871f-388">443</span></span> | <span data-ttu-id="b871f-389">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-389">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="b871f-390">미국 중북부</span><span class="sxs-lookup"><span data-stu-id="b871f-390">North Central US</span></span> | <span data-ttu-id="b871f-391">157.56.8.38</span><span class="sxs-lookup"><span data-stu-id="b871f-391">157.56.8.38</span></span></br><span data-ttu-id="b871f-392">157.55.213.99</span><span class="sxs-lookup"><span data-stu-id="b871f-392">157.55.213.99</span></span> | <span data-ttu-id="b871f-393">443</span><span class="sxs-lookup"><span data-stu-id="b871f-393">443</span></span> | <span data-ttu-id="b871f-394">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-394">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="b871f-395">미국 중서부</span><span class="sxs-lookup"><span data-stu-id="b871f-395">West Central US</span></span> | <span data-ttu-id="b871f-396">52.161.23.15</span><span class="sxs-lookup"><span data-stu-id="b871f-396">52.161.23.15</span></span></br><span data-ttu-id="b871f-397">52.161.10.167</span><span class="sxs-lookup"><span data-stu-id="b871f-397">52.161.10.167</span></span> | <span data-ttu-id="b871f-398">443</span><span class="sxs-lookup"><span data-stu-id="b871f-398">443</span></span> | <span data-ttu-id="b871f-399">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-399">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="b871f-400">미국 서부 2</span><span class="sxs-lookup"><span data-stu-id="b871f-400">West US 2</span></span> | <span data-ttu-id="b871f-401">52.175.211.210</span><span class="sxs-lookup"><span data-stu-id="b871f-401">52.175.211.210</span></span></br><span data-ttu-id="b871f-402">52.175.222.222</span><span class="sxs-lookup"><span data-stu-id="b871f-402">52.175.222.222</span></span> | <span data-ttu-id="b871f-403">443</span><span class="sxs-lookup"><span data-stu-id="b871f-403">443</span></span> | <span data-ttu-id="b871f-404">인바운드</span><span class="sxs-lookup"><span data-stu-id="b871f-404">Inbound</span></span> |

    <span data-ttu-id="b871f-405">Azure Government에 사용할 IP 주소에 대한 자세한 내용은 [Azure Government 인텔리전스 + 분석](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-405">For information on the IP addresses to use for Azure Government, see the [Azure Government Intelligence + Analytics](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) document.</span></span>

3. <span data-ttu-id="b871f-406">가상 네트워크에서 사용자 지정 DNS 서버를 사용하는 경우 __168.63.129.16__에서의 액세스도 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-406">If you use a custom DNS server with your virtual network, you must also allow access from __168.63.129.16__.</span></span> <span data-ttu-id="b871f-407">이 주소는 Azure 재귀 확인자입니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-407">This address is Azure's recursive resolver.</span></span> <span data-ttu-id="b871f-408">자세한 내용은 [VM 및 역할 인스턴스의 이름 확인](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-408">For more information, see the [Name resolution for VMs and Role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) document.</span></span>

<span data-ttu-id="b871f-409">자세한 내용은 [네트워크 트래픽 제어](#networktraffic) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-409">For more information, see the [Controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="b871f-410"><a id="hdinsight-ports"></a> 필수 포트</span><span class="sxs-lookup"><span data-stu-id="b871f-410"><a id="hdinsight-ports"></a> Required ports</span></span>

<span data-ttu-id="b871f-411">네트워크 **가상 어플라이언스 방화벽**을 사용하여 가상 네트워크를 보호할 계획인 경우 다음 포트에서 아웃바운드 트래픽을 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-411">If you plan on using a network **virtual appliance firewall** to secure the virtual network, you must allow outbound traffic on the following ports:</span></span>

* <span data-ttu-id="b871f-412">53</span><span class="sxs-lookup"><span data-stu-id="b871f-412">53</span></span>
* <span data-ttu-id="b871f-413">443</span><span class="sxs-lookup"><span data-stu-id="b871f-413">443</span></span>
* <span data-ttu-id="b871f-414">1433</span><span class="sxs-lookup"><span data-stu-id="b871f-414">1433</span></span>
* <span data-ttu-id="b871f-415">11000-11999</span><span class="sxs-lookup"><span data-stu-id="b871f-415">11000-11999</span></span>
* <span data-ttu-id="b871f-416">14000-14999</span><span class="sxs-lookup"><span data-stu-id="b871f-416">14000-14999</span></span>

<span data-ttu-id="b871f-417">특정 서비스에 대한 포트 목록은 [HDInsight의 Hadoop 서비스에서 사용하는 포트](hdinsight-hadoop-port-settings-for-services.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-417">For a list of ports for specific services, see the [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

<span data-ttu-id="b871f-418">가상 어플라이언스의 방화벽 규칙에 대한 자세한 내용은 [가상 어플라이언스 시나리오](../virtual-network/virtual-network-scenario-udr-gw-nva.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-418">For more information on firewall rules for virtual appliances, see the [virtual appliance scenario](../virtual-network/virtual-network-scenario-udr-gw-nva.md) document.</span></span>

## <span data-ttu-id="b871f-419"><a id="hdinsight-nsg"></a>예제: HDInsight에서 네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="b871f-419"><a id="hdinsight-nsg"></a>Example: network security groups with HDInsight</span></span>

<span data-ttu-id="b871f-420">이 섹션의 예제는 HDInsight가 Azure 관리 서비스와 통신할 수 있도록 하는 네트워크 보안 그룹 규칙을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-420">The examples in this section demonstrate how to create network security group rules that allow HDInsight to communicate with the Azure management services.</span></span> <span data-ttu-id="b871f-421">예제를 사용하기 전에 사용 중인 Azure 지역과 일치하도록 IP 주소를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-421">Before using the examples, adjust the IP addresses to match the ones for the Azure region you are using.</span></span> <span data-ttu-id="b871f-422">이 정보는 [네트워크 보안 그룹 및 사용자 정의 경로가 있는 HDInsight](#hdinsight-ip) 섹션에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-422">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-resource-management-template"></a><span data-ttu-id="b871f-423">Azure Resource Management 템플릿</span><span class="sxs-lookup"><span data-stu-id="b871f-423">Azure Resource Management template</span></span>

<span data-ttu-id="b871f-424">다음 리소스 관리 템플릿은 인바운드 트래픽을 제한하지만 HDInsight에 필요한 IP 주소에서의 트래픽은 허용하는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-424">The following Resource Management template creates a virtual network that restricts inbound traffic, but allows traffic from the IP addresses required by HDInsight.</span></span> <span data-ttu-id="b871f-425">또한 이 템플릿은 가상 네트워크에 HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-425">This template also creates an HDInsight cluster in the virtual network.</span></span>

* [<span data-ttu-id="b871f-426">보안 Azure Virtual Network 및 HDInsight Hadoop 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="b871f-426">Deploy a secured Azure Virtual Network and an HDInsight Hadoop cluster</span></span>](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

> [!IMPORTANT]
> <span data-ttu-id="b871f-427">이 예제에 사용된 IP 주소를 사용 중인 Azure 지역에 맞게 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-427">Change the IP addresses used in this example to match the Azure region you are using.</span></span> <span data-ttu-id="b871f-428">이 정보는 [네트워크 보안 그룹 및 사용자 정의 경로가 있는 HDInsight](#hdinsight-ip) 섹션에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-428">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="b871f-429">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b871f-429">Azure PowerShell</span></span>

<span data-ttu-id="b871f-430">다음 PowerShell 스크립트를 사용하여 인바운드 트래픽을 제한하며 북유럽 지역의 IP 주소에서 전송되는 트래픽을 허용하는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-430">Use the following PowerShell script to create a virtual network that restricts inbound traffic and allows traffic from the IP addresses for the North Europe region.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b871f-431">이 예제에 사용된 IP 주소를 사용 중인 Azure 지역에 맞게 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-431">Change the IP addresses used in this example to match the Azure region you are using.</span></span> <span data-ttu-id="b871f-432">이 정보는 [네트워크 보안 그룹 및 사용자 정의 경로가 있는 HDInsight](#hdinsight-ip) 섹션에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-432">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with the resource group the virtual network is in"
$subnetName = "Replace with the name of the subnet that you plan to use for HDInsight"
# Get the Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get the region the Virtual network is in.
$location = $vnet.Location
# Get the subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for the HDInsight health and management services.
$nsg = New-AzureRmNetworkSecurityGroup `
    -Name "hdisecure" `
    -ResourceGroupName $resourceGroupName `
    -Location $location `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -name "hdirule1" `
        -Description "HDI health and management address 52.164.210.96" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "52.164.210.96" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 300 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 13.74.153.132" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "13.74.153.132" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 301 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.49.99" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.49.99" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 302 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 23.99.5.239" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "23.99.5.239" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 303 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.48.131" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.48.131" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 304 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 138.91.141.162" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "138.91.141.162" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 305 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "blockeverything" `
        -Description "Block everything else" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "*" `
        -SourceAddressPrefix "Internet" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Deny `
        -Priority 500 `
        -Direction Inbound
# Set the changes to the security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply the NSG to the subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> <span data-ttu-id="b871f-433">이 예제에서는 필요한 IP 주소에서 인바운드 트래픽을 허용하도록 규칙을 추가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-433">This example demonstrates how to add rules to allow inbound traffic on the required IP addresses.</span></span> <span data-ttu-id="b871f-434">다른 소스에서 인바운드 액세스를 제한하는 규칙은 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-434">It does not contain a rule to restrict inbound access from other sources.</span></span>
>
> <span data-ttu-id="b871f-435">다음 예제는 인터넷에서 SSH 액세스를 사용 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-435">The following example demonstrates how to enable SSH access from the Internet:</span></span>
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a><span data-ttu-id="b871f-436">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b871f-436">Azure CLI</span></span>

<span data-ttu-id="b871f-437">다음 단계에 따라 인바운드 트래픽을 제한하지만 HDInsight에 필요한 IP 주소에서의 트래픽은 허용하는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-437">Use the following steps to create a virtual network that restricts inbound traffic, but allows traffic from the IP addresses required by HDInsight.</span></span>

1. <span data-ttu-id="b871f-438">다음 명령을 사용하여 `hdisecure`이라는 새 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-438">Use the following command to create a new network security group named `hdisecure`.</span></span> <span data-ttu-id="b871f-439">**RESOURCEGROUPNAME**을 Azure Virtual Network를 포함하는 리소스 그룹으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-439">Replace **RESOURCEGROUPNAME** with the resource group that contains the Azure Virtual Network.</span></span> <span data-ttu-id="b871f-440">**LOCATION**을 그룹이 만들어진 위치(지역)로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-440">Replace **LOCATION** with the location (region) that the group was created in.</span></span>

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    <span data-ttu-id="b871f-441">그룹을 만들면 새 그룹에 대한 정보를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-441">Once the group has been created, you receive information on the new group.</span></span>

2. <span data-ttu-id="b871f-442">다음을 사용하여 Azure HDInsight 상태 및 관리 서비스에서 포트 443에 대한 인바운드 통신을 허용하는 새 네트워크 보안 그룹에 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-442">Use the following to add rules to the new network security group that allow inbound communication on port 443 from the Azure HDInsight health and management service.</span></span> <span data-ttu-id="b871f-443">**RESOURCEGROUPNAME** 을 Azure Virtual Network를 포함하는 리소스 그룹 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-443">Replace **RESOURCEGROUPNAME** with the name of the resource group that contains the Azure Virtual Network.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b871f-444">이 예제에 사용된 IP 주소를 사용 중인 Azure 지역에 맞게 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-444">Change the IP addresses used in this example to match the Azure region you are using.</span></span> <span data-ttu-id="b871f-445">이 정보는 [네트워크 보안 그룹 및 사용자 정의 경로가 있는 HDInsight](#hdinsight-ip) 섹션에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-445">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. <span data-ttu-id="b871f-446">이 네트워크 보안 그룹에 대한 고유 식별자를 검색하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-446">To retrieve the unique identifier for this network security group, use the following command:</span></span>

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    <span data-ttu-id="b871f-447">이 명령은 다음 텍스트와 유사한 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-447">This command returns a value similar to the following text:</span></span>

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    <span data-ttu-id="b871f-448">예상된 결과를 얻지 못한 경우 명령에서 id에 따옴표를 넣어 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-448">Use double-quotes around id in the command if you don't get the expected results.</span></span>

4. <span data-ttu-id="b871f-449">다음 명령을 사용하여 네트워크 보안 그룹을 서브넷에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-449">Use the following command to apply the network security group to a subnet.</span></span> <span data-ttu-id="b871f-450">__GUID__ 및 __RESOURCEGROUPNAME__ 값을 이전 단계에서 반환된 값으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-450">Replace the __GUID__ and __RESOURCEGROUPNAME__ values with the ones returned from the previous step.</span></span> <span data-ttu-id="b871f-451">__VNETNAME__ 및 __SUBNETNAME__을 만들려는 가상 네트워크 이름 및 서브넷 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-451">Replace __VNETNAME__ and __SUBNETNAME__ with the virtual network name and subnet name that you want to create.</span></span>

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    <span data-ttu-id="b871f-452">이 명령이 완료되면 Virtual Network에 HDInsight를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-452">Once this command completes, you can install HDInsight into the Virtual Network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b871f-453">이러한 단계를 사용하면 Azure 클라우드의 HDInsight 상태 및 관리 서비스에 대한 액세스만 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-453">These steps only open access to the HDInsight health and management service on the Azure cloud.</span></span> <span data-ttu-id="b871f-454">Virtual Network 외부에서 HDInsight 클러스터에 대한 기타 액세스는 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-454">Any other access to the HDInsight cluster from outside the Virtual Network is blocked.</span></span> <span data-ttu-id="b871f-455">가상 네트워크 외부에서 액세스할 수 있도록 하려는 경우 네트워크 보안 그룹 규칙을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-455">To enable access from outside the virtual network, you must add additional Network Security Group rules.</span></span>
>
> <span data-ttu-id="b871f-456">다음 예제는 인터넷에서 SSH 액세스를 사용 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-456">The following example demonstrates how to enable SSH access from the Internet:</span></span>
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <span data-ttu-id="b871f-457"><a id="example-dns"></a> 예제: DNS 구성</span><span class="sxs-lookup"><span data-stu-id="b871f-457"><a id="example-dns"></a> Example: DNS configuration</span></span>

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a><span data-ttu-id="b871f-458">가상 네트워크와 연결된 온-프레미스 네트워크 간에 이름 확인</span><span class="sxs-lookup"><span data-stu-id="b871f-458">Name resolution between a virtual network and a connected on-premises network</span></span>

<span data-ttu-id="b871f-459">이 예제에서는 다음과 같이 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-459">This example makes the following assumptions:</span></span>

* <span data-ttu-id="b871f-460">VPN 게이트웨이를 사용하여 온-프레미스 네트워크에 연결된 Azure Virtual Network가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-460">You have an Azure Virtual Network that is connected to an on-premises network using a VPN gateway.</span></span>

* <span data-ttu-id="b871f-461">가상 네트워크의 사용자 지정 DNS 서버는 운영 체제로 Linux 또는 Unix 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-461">The custom DNS server in the virtual network is running Linux or Unix as the operating system.</span></span>

* <span data-ttu-id="b871f-462">[바인딩](https://www.isc.org/downloads/bind/)이 사용자 지정 DNS 서버에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-462">[Bind](https://www.isc.org/downloads/bind/) is installed on the custom DNS server.</span></span>

<span data-ttu-id="b871f-463">가상 네트워크의 사용자 지정 DNS 서버에서:</span><span class="sxs-lookup"><span data-stu-id="b871f-463">On the custom DNS server in the virtual network:</span></span>

1. <span data-ttu-id="b871f-464">Azure PowerShell 또는 Azure CLI를 사용하여 가상 네트워크의 DNS 접미사를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-464">Use either Azure PowerShell or Azure CLI to find the DNS suffix of the virtual network:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="b871f-465">가상 네트워크에 대한 사용자 지정 DNS 서버에서 `/etc/bind/named.conf.local` 파일의 내용으로 다음 텍스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-465">On the custom DNS server for the virtual network, use the following text as the contents of the `/etc/bind/named.conf.local` file:</span></span>

    ```
    // Forward requests for the virtual network suffix to Azure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    <span data-ttu-id="b871f-466">`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` 값을 가상 네트워크의 DNS 접미사로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-466">Replace the `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with the DNS suffix of your virtual network.</span></span>

    <span data-ttu-id="b871f-467">이 구성은 가상 네트워크의 DNS 접미사에 대한 모든 DNS 요청을 Azure 재귀 확인자에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-467">This configuration routes all DNS requests for the DNS suffix of the virtual network to the Azure recursive resolver.</span></span>

2. <span data-ttu-id="b871f-468">가상 네트워크에 대한 사용자 지정 DNS 서버에서 `/etc/bind/named.conf.options` 파일의 내용으로 다음 텍스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-468">On the custom DNS server for the virtual network, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients to accept requests from
    // TODO: Add the IP range of the joined network to this list
    acl goodclients {
        10.0.0.0/16; # IP address range of the virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent to the following
            forwarders {
                192.168.0.1; # Replace with the IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform to RFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="b871f-469">`10.0.0.0/16` 값을 가상 네트워크의 IP 주소 범위로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-469">Replace the `10.0.0.0/16` value with the IP address range of your virtual network.</span></span> <span data-ttu-id="b871f-470">이 항목으로 이 범위 내의 주소로 이름 확인 요청이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-470">This entry allows name resolution requests addresses within this range.</span></span>

    * <span data-ttu-id="b871f-471">온-프레미스 네트워크의 IP 주소 범위를 `acl goodclients { ... }` 섹션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-471">Add the IP address range of the on-premises network to the `acl goodclients { ... }` section.</span></span>  <span data-ttu-id="b871f-472">이 항목으로 온-프레미스 네트워크의 리소스에서 이름 확인 요청이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-472">entry allows name resolution requests from resources in the on-premises network.</span></span>
    
    * <span data-ttu-id="b871f-473">`192.168.0.1` 값을 온-프레미스 DNS 서버의 IP 주소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-473">Replace the value `192.168.0.1` with the IP address of your on-premises DNS server.</span></span> <span data-ttu-id="b871f-474">이 항목은 다른 모든 DNS 요청을 온-프레미스 DNS 서버에 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-474">This entry routes all other DNS requests to the on-premises DNS server.</span></span>

3. <span data-ttu-id="b871f-475">구성을 사용하려면 바인딩을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-475">To use the configuration, restart Bind.</span></span> <span data-ttu-id="b871f-476">예: `sudo service bind9 restart`</span><span class="sxs-lookup"><span data-stu-id="b871f-476">For example, `sudo service bind9 restart`.</span></span>

4. <span data-ttu-id="b871f-477">온-프레미스 DNS 서버에 조건부 전달자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-477">Add a conditional forwarder to the on-premises DNS server.</span></span> <span data-ttu-id="b871f-478">1단계에서 DNS 접미사에 대한 요청을 사용자 지정 DNS 서버에 보내도록 조건부 전달자를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-478">Configure the conditional forwarder to send requests for the DNS suffix from step 1 to the custom DNS server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b871f-479">조건부 전달자를 추가하는 방법에 대한 구체적인 정보는 DNS 소프트웨어에 대한 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-479">Consult the documentation for your DNS software for specifics on how to add a conditional forwarder.</span></span>

<span data-ttu-id="b871f-480">다음 단계를 완료한 후 FQDN(정규화된 도메인 이름)을 사용하여 네트워크의 리소스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-480">After completing these steps, you can connect to resources in either network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="b871f-481">이제 HDInsight를 가상 네트워크에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-481">You can now install HDInsight into the virtual network.</span></span>

### <a name="name-resolution-between-two-connected-virtual-networks"></a><span data-ttu-id="b871f-482">두 개의 연결된 가상 네트워크 간의 이름 확인</span><span class="sxs-lookup"><span data-stu-id="b871f-482">Name resolution between two connected virtual networks</span></span>

<span data-ttu-id="b871f-483">이 예제에서는 다음과 같이 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-483">This example makes the following assumptions:</span></span>

* <span data-ttu-id="b871f-484">VPN 게이트웨이 또는 피어링을 사용하여 연결된 두 Azure Virtual Networks가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-484">You have two Azure Virtual Networks that are connected using either a VPN gateway or peering.</span></span>

* <span data-ttu-id="b871f-485">두 네트워크의 사용자 지정 DNS 서버는 운영 체제로 Linux 또는 Unix를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-485">The custom DNS server in both networks is running Linux or Unix as the operating system.</span></span>

* <span data-ttu-id="b871f-486">[바인딩](https://www.isc.org/downloads/bind/)이 사용자 지정 DNS 서버에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-486">[Bind](https://www.isc.org/downloads/bind/) is installed on the custom DNS servers.</span></span>

1. <span data-ttu-id="b871f-487">Azure PowerShell 또는 Azure CLI를 사용하여 두 가상 네트워크의 DNS 접미사를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-487">Use either Azure PowerShell or Azure CLI to find the DNS suffix of both virtual networks:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="b871f-488">사용자 지정 DNS 서버에서 `/etc/bind/named.config.local` 파일의 내용으로 다음 텍스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-488">Use the following text as the contents of the `/etc/bind/named.config.local` file on the custom DNS server.</span></span> <span data-ttu-id="b871f-489">두 가상 네트워크의 사용자 지정 DNS 서버에서 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-489">Make this change on the custom DNS server in both virtual networks.</span></span>

    ```
    // Forward requests for the virtual network suffix to Azure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # The IP address of the DNS server in the other virtual network
    };
    ```

    <span data-ttu-id="b871f-490">`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` 값을 __다른__ 가상 네트워크의 DNS 접미사로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-490">Replace the `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with the DNS suffix of the __other__ virtual network.</span></span> <span data-ttu-id="b871f-491">이 항목은 원격 네트워크의 DNS 접미사 요청을 해당 네트워크의 사용자 지정 DNS로 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-491">This entry routes requests for the DNS suffix of the remote network to the custom DNS in that network.</span></span>

3. <span data-ttu-id="b871f-492">두 가상 네트워크의 사용자 지정 DNS 서버에서 `/etc/bind/named.conf.options` 파일의 내용으로 다음 텍스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-492">On the custom DNS servers in both virtual networks, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients to accept requests from
    acl goodclients {
        10.1.0.0/16; # The IP address range of one virtual network
        10.0.0.0/16; # The IP address range of the other virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            forwarders {
            168.63.129.16;   # Azure recursive resolver         
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform to RFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="b871f-493">`10.0.0.0/16` 및 `10.1.0.0/16` 값을 가상 네트워크의 IP 주소 범위로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-493">Replace the `10.0.0.0/16` and `10.1.0.0/16` values with the IP address ranges of your virtual networks.</span></span> <span data-ttu-id="b871f-494">이 항목으로 각 네트워크의 리소스가 DNS 서버에 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-494">This entry allows resources in each network to make requests of the DNS servers.</span></span>

    <span data-ttu-id="b871f-495">가상 네트워크의 DNS 접미사에 해당하지 않는 모든 요청(예: microsoft.com)은 Azure 재귀 확인자에 의해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-495">Any requests that are not for the DNS suffixes of the virtual networks (for example, microsoft.com) is handled by the Azure recursive resolver.</span></span>

4. <span data-ttu-id="b871f-496">구성을 사용하려면 바인딩을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-496">To use the configuration, restart Bind.</span></span> <span data-ttu-id="b871f-497">예를 들어, 두 DNS 서버에서 `sudo service bind9 restart`입니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-497">For example, `sudo service bind9 restart` on both DNS servers.</span></span>

<span data-ttu-id="b871f-498">다음 단계를 완료한 후 FQDN(정규화된 도메인 이름)을 사용하여 가상 네트워크의 리소스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-498">After completing these steps, you can connect to resources in the virtual network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="b871f-499">이제 HDInsight를 가상 네트워크에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b871f-499">You can now install HDInsight into the virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b871f-500">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b871f-500">Next steps</span></span>

* <span data-ttu-id="b871f-501">온-프레미스 네트워크에 연결하기 위해 HDInsight를 구성하는 종단 간 예제는 [HDInsight를 온-프레미스 네트워크에 연결](./connect-on-premises-network.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-501">For an end-to-end example of configuring HDInsight to connect to an on-premises network, see [Connect HDInsight to an on-premises network](./connect-on-premises-network.md).</span></span>

* <span data-ttu-id="b871f-502">Azure 가상 네트워크에 대한 자세한 내용은 [Azure Virtual Network 개요](../virtual-network/virtual-networks-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-502">For more information on Azure virtual networks, see the [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="b871f-503">네트워크 보안 그룹에 대한 자세한 내용은 [네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-503">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="b871f-504">사용자 정의 경로에 대한 자세한 내용은 [사용자 정의 경로 및 IP 전달](../virtual-network/virtual-networks-udr-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b871f-504">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>