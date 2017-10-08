---
title: "가상 네트워크-Azure HDInsight aaaExtend | Microsoft Docs"
description: "어떻게 toouse Azure 가상 네트워크 tooconnect HDInsight tooother 클라우드 리소스 또는 데이터 센터의 리소스에 알아봅니다"
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
ms.openlocfilehash: ba80be4d9f280c6c62fa8acc996ef5f921acdbbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a><span data-ttu-id="4042f-103">Azure Virtual Network를 사용하여 Azure HDInsight 확장</span><span class="sxs-lookup"><span data-stu-id="4042f-103">Extend Azure HDInsight using an Azure Virtual Network</span></span>

<span data-ttu-id="4042f-104">자세한 내용은 방법 toouse HDInsight와는 [Azure 가상 네트워크](../virtual-network/virtual-networks-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-104">Learn how toouse HDInsight with an [Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="4042f-105">Azure 가상 네트워크를 사용 하 여 다음 시나리오는 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-105">Using an Azure Virtual Network enables hello following scenarios:</span></span>

* <span data-ttu-id="4042f-106">온-프레미스 네트워크에서 직접 tooHDInsight를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-106">Connecting tooHDInsight directly from an on-premises network.</span></span>

* <span data-ttu-id="4042f-107">HDInsight toodata 연결 된 Azure 가상 네트워크에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-107">Connecting HDInsight toodata stores in an Azure Virtual network.</span></span>

* <span data-ttu-id="4042f-108">직접 넘는 공개적으로 사용할 수 없는 Hadoop 서비스 액세스 방법에 인터넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-108">Directly accessing Hadoop services that are not available publicly over hello internet.</span></span> <span data-ttu-id="4042f-109">예를 들어 Kafka Api 또는 hello HBase Java API입니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-109">For example, Kafka APIs or hello HBase Java API.</span></span>

> [!WARNING]
> <span data-ttu-id="4042f-110">hello이이 문서의 정보에에서는 TCP/IP 네트워킹 이해를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-110">hello information in this document requires an understanding of TCP/IP networking.</span></span> <span data-ttu-id="4042f-111">TCP/IP 네트워킹 잘 모르는 경우 tooproduction 네트워크 수정 하기 전에 장애가 있는 사용자와 파트너가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-111">If you are not familiar with TCP/IP networking, you should partner with someone who is before making modifications tooproduction networks.</span></span>

## <a name="planning"></a><span data-ttu-id="4042f-112">계획</span><span class="sxs-lookup"><span data-stu-id="4042f-112">Planning</span></span>

<span data-ttu-id="4042f-113">hello 다음은 가상 네트워크의 tooinstall HDInsight를 계획할 때 대답 해야 하는 hello 질문입니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-113">hello following are hello questions that you must answer when planning tooinstall HDInsight in a virtual network:</span></span>

* <span data-ttu-id="4042f-114">기존 가상 네트워크에 HDInsight tooinstall 필요 한가요?</span><span class="sxs-lookup"><span data-stu-id="4042f-114">Do you need tooinstall HDInsight into an existing virtual network?</span></span> <span data-ttu-id="4042f-115">아니면 새 네트워크를 만드나요?</span><span class="sxs-lookup"><span data-stu-id="4042f-115">Or are you creating a new network?</span></span>

    <span data-ttu-id="4042f-116">기존 가상 네트워크를 사용 하는 경우 HDInsight를 설치 하기 전에 toomodify hello 네트워크 구성을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-116">If you are using an existing virtual network, you may need toomodify hello network configuration before you can install HDInsight.</span></span> <span data-ttu-id="4042f-117">자세한 내용은 참조 hello [HDInsight tooan 기존 가상 네트워크 추가](#existingvnet) 섹션.</span><span class="sxs-lookup"><span data-stu-id="4042f-117">For more information, see hello [add HDInsight tooan existing virtual network](#existingvnet) section.</span></span>

* <span data-ttu-id="4042f-118">온-프레미스 네트워크 또는 tooconnect hello 가상 네트워크 HDInsight tooanother 가상 네트워크를 포함 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="4042f-118">Do you want tooconnect hello virtual network containing HDInsight tooanother virtual network or your on-premises network?</span></span>

    <span data-ttu-id="4042f-119">tooeasily 작업 네트워크를 통해 리소스를 리소스와 필요한 사용자 지정 DNS toocreate 및 DNS 전달 구성 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-119">tooeasily work with resources across networks, you may need toocreate a custom DNS and configure DNS forwarding.</span></span> <span data-ttu-id="4042f-120">자세한 내용은 참조 hello [여러 네트워크 연결](#multinet) 섹션.</span><span class="sxs-lookup"><span data-stu-id="4042f-120">For more information, see hello [connecting multiple networks](#multinet) section.</span></span>

* <span data-ttu-id="4042f-121">Toorestrict/리디렉션 원하는 인바운드 또는 아웃 바운드 트래픽 tooHDInsight?</span><span class="sxs-lookup"><span data-stu-id="4042f-121">Do you want toorestrict/redirect inbound or outbound traffic tooHDInsight?</span></span>

    <span data-ttu-id="4042f-122">HDInsight은 hello Azure 데이터 센터에서 특정 IP 주소와 통신을 제한 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-122">HDInsight must have unrestricted communication with specific IP addresses in hello Azure data center.</span></span> <span data-ttu-id="4042f-123">또한 클라이언트 통신에 방화벽을 통해 허용해야 하는 여러 포트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-123">There are also several ports that must be allowed through firewalls for client communication.</span></span> <span data-ttu-id="4042f-124">자세한 내용은 참조 hello [네트워크 트래픽을 제어](#networktraffic) 섹션.</span><span class="sxs-lookup"><span data-stu-id="4042f-124">For more information, see hello [controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="4042f-125"><a id="existingvnet"></a>HDInsight tooan 기존 가상 네트워크 추가</span><span class="sxs-lookup"><span data-stu-id="4042f-125"><a id="existingvnet"></a>Add HDInsight tooan existing virtual network</span></span>

<span data-ttu-id="4042f-126">이 섹션 toodiscover을 어떻게 hello 단계를 사용 하 여 Azure 가상 네트워크를 기존 새 HDInsight tooan tooadd 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-126">Use hello steps in this section toodiscover how tooadd a new HDInsight tooan existing Azure Virtual Network.</span></span>

> [!NOTE]
> <span data-ttu-id="4042f-127">기존 HDInsight 클러스터를 가상 네트워크에 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-127">You cannot add an existing HDInsight cluster into a virtual network.</span></span>

1. <span data-ttu-id="4042f-128">사용 하는 기본 리소스 관리자 배포 모델 hello 가상 네트워크에 대 한?</span><span class="sxs-lookup"><span data-stu-id="4042f-128">Are you using a classic or Resource Manager deployment model for hello virtual network?</span></span>

    <span data-ttu-id="4042f-129">HDInsight 3.4 이상에는 리소스 관리자 가상 네트워크가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-129">HDInsight 3.4 and greater requires a Resource Manager virtual network.</span></span> <span data-ttu-id="4042f-130">이전 버전의 HDInsightㅇ는 클래식 가상 네트워크가 필요했습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-130">Earlier versions of HDInsight required a classic virtual network.</span></span>

    <span data-ttu-id="4042f-131">기존 네트워크 클래식 가상 네트워크 인 경우 다음 리소스 관리자 가상 네트워크를 만들고 해야 다음 두 hello를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-131">If your existing network is a classic virtual network, then you must create a Resource Manager virtual network and then connect hello two.</span></span> <span data-ttu-id="4042f-132">[클래식 Vnet toonew Vnet 연결](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-132">[Connecting classic VNets toonew VNets](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span></span>

    <span data-ttu-id="4042f-133">조인, hello 리소스 관리자 네트워크에 설치 하는 HDInsight hello 클래식 네트워크 리소스와 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-133">Once joined, HDInsight installed in hello Resource Manager network can interact with resources in hello classic network.</span></span>

2. <span data-ttu-id="4042f-134">강제 터널링을 사용하나요?</span><span class="sxs-lookup"><span data-stu-id="4042f-134">Do you use forced tunneling?</span></span> <span data-ttu-id="4042f-135">강제 터널링 하는 것은 검사에 대 한 아웃 바운드 인터넷 트래픽을 tooa 장치를 강제로 수행 하는 서브넷 설정 및 로깅입니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-135">Forced tunneling is a subnet setting that forces outbound Internet traffic tooa device for inspection and logging.</span></span> <span data-ttu-id="4042f-136">HDInsight는 강제 터널링을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-136">HDInsight does not support forced tunneling.</span></span> <span data-ttu-id="4042f-137">서브넷에 HDInsight를 설치하기 전에 강제 터널링을 제거하거나 HDInsight에 대해 새 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-137">Either remove forced tunneling before installing HDInsight into a subnet, or create a new subnet for HDInsight.</span></span>

3. <span data-ttu-id="4042f-138">사용 합니까 네트워크 보안 그룹, 사용자 정의 경로 또는 가상 네트워크 어플라이언스에 toorestrict 트래픽 내부 또는 외부로 가상 네트워크 hello?</span><span class="sxs-lookup"><span data-stu-id="4042f-138">Do you use network security groups, user-defined routes, or Virtual Network Appliances toorestrict traffic into or out of hello virtual network?</span></span>

    <span data-ttu-id="4042f-139">관리 되는 서비스로 HDInsight hello Azure 데이터 센터에 대 한 무제한 액세스 tooseveral IP 주소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-139">As a managed service, HDInsight requires unrestricted access tooseveral IP addresses in hello Azure data center.</span></span> <span data-ttu-id="4042f-140">이러한 IP 주소와 통신을 tooallow 모든 기존 네트워크 보안 그룹 또는 사용자 정의 경로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-140">tooallow communication with these IP addresses, update any existing network security groups or user-defined routes.</span></span>

    <span data-ttu-id="4042f-141">HDInsight는 다양한 포트를 사용하는 여러 서비스를 호스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-141">HDInsight  hosts multiple services, which use a variety of ports.</span></span> <span data-ttu-id="4042f-142">트래픽이 toothese 포트를 차단 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-142">Do not block traffic toothese ports.</span></span> <span data-ttu-id="4042f-143">가상 어플라이언스 방화벽을 통해 포트 tooallow 목록이 참조 hello [보안](#security) 섹션.</span><span class="sxs-lookup"><span data-stu-id="4042f-143">For a list of ports tooallow through virtual appliance firewalls, see hello [Security](#security) section.</span></span>

    <span data-ttu-id="4042f-144">toofind 기존 보안 구성에 따라 Azure PowerShell 또는 Azure CLI 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="4042f-144">toofind your existing security configuration, use hello following Azure PowerShell or Azure CLI commands:</span></span>

    * <span data-ttu-id="4042f-145">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="4042f-145">Network security groups</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="4042f-146">자세한 내용은 참조 hello [네트워크 보안 그룹 문제 해결](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="4042f-146">For more information, see hello [Troubleshoot network security groups](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) document.</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="4042f-147">네트워크 보안 그룹 규칙은 규칙 우선 순위에 따라 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-147">Network security group rules are applied in order based on rule priority.</span></span> <span data-ttu-id="4042f-148">hello 트래픽 패턴과 일치 하는 hello 첫 번째 규칙을 적용 하 고 해당 트래픽을 에서만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-148">hello first rule that matches hello traffic pattern is applied, and no others are applied for that traffic.</span></span> <span data-ttu-id="4042f-149">순서에서 가장 높은 tooleast 허용 되는 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-149">Order rules from most permissive tooleast permissive.</span></span> <span data-ttu-id="4042f-150">자세한 내용은 참조 hello [네트워크 보안 그룹과 네트워크 트래픽 필터](../virtual-network/virtual-networks-nsg.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="4042f-150">For more information, see hello [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    * <span data-ttu-id="4042f-151">사용자 정의 경로</span><span class="sxs-lookup"><span data-stu-id="4042f-151">User-defined routes</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="4042f-152">자세한 내용은 참조 hello [경로 문제를 해결](../virtual-network/virtual-network-routes-troubleshoot-portal.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="4042f-152">For more information, see hello [Troubleshoot routes](../virtual-network/virtual-network-routes-troubleshoot-portal.md) document.</span></span>

4. <span data-ttu-id="4042f-153">HDInsight 클러스터를 만들고 구성 하는 동안 hello Azure 가상 네트워크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-153">Create an HDInsight cluster and select hello Azure Virtual Network during configuration.</span></span> <span data-ttu-id="4042f-154">Hello 문서 toounderstand hello 클러스터 만들기 프로세스의 단계를 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="4042f-154">Use hello steps in hello following documents toounderstand hello cluster creation process:</span></span>

    * [<span data-ttu-id="4042f-155">HDInsight hello Azure 포털을 사용 하 여 만들기</span><span class="sxs-lookup"><span data-stu-id="4042f-155">Create HDInsight using hello Azure portal</span></span>](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [<span data-ttu-id="4042f-156">Azure PowerShell을 사용하여 HDInsight 만들기</span><span class="sxs-lookup"><span data-stu-id="4042f-156">Create HDInsight using Azure PowerShell</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
    * [<span data-ttu-id="4042f-157">Azure CLI 1.0을 사용하여 HDInsight 만들기</span><span class="sxs-lookup"><span data-stu-id="4042f-157">Create HDInsight using Azure CLI 1.0</span></span>](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [<span data-ttu-id="4042f-158">Azure Resource Manager 템플릿을 사용하여 HDInsight 만들기</span><span class="sxs-lookup"><span data-stu-id="4042f-158">Create HDInsight using an Azure Resource Manager template</span></span>](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > <span data-ttu-id="4042f-159">옵션 구성 단계를 tooa 가상 네트워크는 HDInsight를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-159">Adding HDInsight tooa virtual network is an optional configuration step.</span></span> <span data-ttu-id="4042f-160">Hello 클러스터를 구성할 때 있는지 tooselect hello 가상 네트워크를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-160">Be sure tooselect hello virtual network when configuring hello cluster.</span></span>

## <span data-ttu-id="4042f-161"><a id="multinet"></a>다중 네트워크 연결</span><span class="sxs-lookup"><span data-stu-id="4042f-161"><a id="multinet"></a>Connecting multiple networks</span></span>

<span data-ttu-id="4042f-162">hello 다중 네트워크 구성이 포함 된 가장 큰 문제는 hello 네트워크 간에 이름 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-162">hello biggest challenge with a multi-network configuration is name resolution between hello networks.</span></span>

<span data-ttu-id="4042f-163">Azure는 가상 네트워크에 설치된 Azure 서비스에 대한 이름 확인을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-163">Azure provides name resolution for Azure services that are installed in a virtual network.</span></span> <span data-ttu-id="4042f-164">기본 제공 이름 확인이 정규화 된 도메인 이름 (FQDN)을 사용 하 여 리소스를 다음 HDInsight tooconnect toohello를 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-164">This built-in name resolution allows HDInsight tooconnect toohello following resources by using a fully qualified domain name (FQDN):</span></span>

* <span data-ttu-id="4042f-165">사용할 수 있는 모든 리소스에는 인터넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-165">Any resource that is available on hello internet.</span></span> <span data-ttu-id="4042f-166">예를 들어, microsoft.com, google.com.</span><span class="sxs-lookup"><span data-stu-id="4042f-166">For example, microsoft.com, google.com.</span></span>

* <span data-ttu-id="4042f-167">에 hello 동일한 Azure 가상 네트워크에서 hello를 사용 하 여 모든 리소스 __내부 DNS 이름을__ hello 리소스의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-167">Any resource that is in hello same Azure Virtual Network, by using hello __internal DNS name__ of hello resource.</span></span> <span data-ttu-id="4042f-168">예를 들어 hello 기본 이름 확인을 사용할 경우 hello 다음은 예제 내부 DNS 이름이 할당된 tooHDInsight 작업자 노드.</span><span class="sxs-lookup"><span data-stu-id="4042f-168">For example, when using hello default name resolution, hello following are example internal DNS names assigned tooHDInsight worker nodes:</span></span>

    * <span data-ttu-id="4042f-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="4042f-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>
    * <span data-ttu-id="4042f-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="4042f-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>

    <span data-ttu-id="4042f-171">이러한 두 노드는 내부 DNS 이름을 사용하여 서로 직접 통신하고 HDInsight의 다른 노드와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-171">Both these nodes can communicate directly with each other, and other nodes in HDInsight, by using internal DNS names.</span></span>

<span data-ttu-id="4042f-172">기본 이름 확인 기능 hello 않습니다 __하지__ 조인된 toohello 가상 네트워크에 있는 네트워크에 HDInsight tooresolve hello 리소스 이름에 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-172">hello default name resolution does __not__ allow HDInsight tooresolve hello names of resources in networks that are joined toohello virtual network.</span></span> <span data-ttu-id="4042f-173">예를 들어, 일반적인 toojoin는 온-프레미스 네트워크 toohello 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-173">For example, it is common toojoin your on-premises network toohello virtual network.</span></span> <span data-ttu-id="4042f-174">만 hello 기본 이름 확인을 HDInsight 이름별 hello 온-프레미스 네트워크의 리소스를 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-174">With only hello default name resolution, HDInsight cannot access resources in hello on-premises network by name.</span></span> <span data-ttu-id="4042f-175">hello 반대도 온-프레미스 네트워크의 리소스 이름으로 hello 가상 네트워크의 리소스에 액세스할 수 없습니다 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-175">hello opposite is also true, resources in your on-premises network cannot access resources in hello virtual network by name.</span></span>

> [!WARNING]
> <span data-ttu-id="4042f-176">사용자 지정 DNS 서버 hello을 만들고 가상 네트워크 toouse hello를 구성 해야 HDInsight 클러스터를 hello를 만들기 전에 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-176">You must create hello custom DNS server and configure hello virtual network toouse it before creating hello HDInsight cluster.</span></span>

<span data-ttu-id="4042f-177">tooenable hello 가상 네트워크와 조인 된 네트워크의 리소스 간에 이름 확인을 hello 다음 작업을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-177">tooenable name resolution between hello virtual network and resources in joined networks, you must perform hello following actions:</span></span>

1. <span data-ttu-id="4042f-178">Hello tooinstall HDInsight을 계획 하는 Azure 가상 네트워크에서에서 사용자 지정 DNS 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-178">Create a custom DNS server in hello Azure Virtual Network where you plan tooinstall HDInsight.</span></span>

2. <span data-ttu-id="4042f-179">Hello 가상 네트워크 toouse hello 사용자 지정 DNS 서버를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-179">Configure hello virtual network toouse hello custom DNS server.</span></span>

3. <span data-ttu-id="4042f-180">Azure 가상 네트워크에 대 한 DNS 접미사를 할당 하는 hello를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-180">Find hello Azure assigned DNS suffix for your virtual network.</span></span> <span data-ttu-id="4042f-181">이 값이 너무 유사`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-181">This value is similar too`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span></span> <span data-ttu-id="4042f-182">Hello DNS 접미사를 찾는 방법에 대 한 정보를 참조 hello [예제: 사용자 지정 DNS](#example-dns) 섹션.</span><span class="sxs-lookup"><span data-stu-id="4042f-182">For information on finding hello DNS suffix, see hello [Example: Custom DNS](#example-dns) section.</span></span>

4. <span data-ttu-id="4042f-183">Hello DNS 서버 간에 전달을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-183">Configure forwarding between hello DNS servers.</span></span> <span data-ttu-id="4042f-184">hello 구성 hello 유형의 원격 네트워크에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-184">hello configuration depends on hello type of remote network.</span></span>

    * <span data-ttu-id="4042f-185">Hello 원격 네트워크는 온-프레미스 네트워크를 DNS를 다음과 같이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-185">If hello remote network is an on-premises network, configure DNS as follows:</span></span>
        
        * <span data-ttu-id="4042f-186">__사용자 지정 DNS__ hello 가상 네트워크) (에:</span><span class="sxs-lookup"><span data-stu-id="4042f-186">__Custom DNS__ (in hello virtual network):</span></span>

            * <span data-ttu-id="4042f-187">Hello 가상 네트워크 toohello Azure 재귀 확인자 (168.63.129.16)의 hello DNS 접미사에 대 한 요청을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-187">Forward requests for hello DNS suffix of hello virtual network toohello Azure recursive resolver (168.63.129.16).</span></span> <span data-ttu-id="4042f-188">Azure는 hello 가상 네트워크의 리소스에 대 한 요청 처리</span><span class="sxs-lookup"><span data-stu-id="4042f-188">Azure handles requests for resources in hello virtual network</span></span>

            * <span data-ttu-id="4042f-189">모든 다른 요청 toohello 온-프레미스 DNS 서버를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-189">Forward all other requests toohello on-premises DNS server.</span></span> <span data-ttu-id="4042f-190">hello 온-프레미스 DNS 처리 다른 모든 이름 확인 요청을 Microsoft.com 같은 인터넷 리소스에 대 한 요청을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-190">hello on-premises DNS handles all other name resolution requests, even requests for internet resources such as Microsoft.com.</span></span>

        * <span data-ttu-id="4042f-191">__온-프레미스 DNS__: hello 가상 네트워크 DNS 접미사 toohello 사용자 지정 DNS 서버에 대 한 요청을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-191">__On-premises DNS__: Forward requests for hello virtual network DNS suffix toohello custom DNS server.</span></span> <span data-ttu-id="4042f-192">사용자 지정 DNS 서버 hello toohello Azure 재귀 확인자를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-192">hello custom DNS server then forwards toohello Azure recursive resolver.</span></span>

        <span data-ttu-id="4042f-193">이 구성 경로 요청에 대 한 정규화 된 도메인 이름 hello 가상 네트워크 toohello 사용자 지정 DNS 서버 hello DNS 접미사를 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-193">This configuration routes requests for fully qualified domain names that contain hello DNS suffix of hello virtual network toohello custom DNS server.</span></span> <span data-ttu-id="4042f-194">(공용 인터넷 주소)에 다른 모든 요청은 hello 온-프레미스 DNS 서버에서 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-194">All other requests (even for public internet addresses) are handled by hello on-premises DNS server.</span></span>

    * <span data-ttu-id="4042f-195">Hello 원격 네트워크는 다른 Azure 가상 네트워크를 DNS를 다음과 같이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-195">If hello remote network is another Azure Virtual Network, configure DNS as follows:</span></span>

        * <span data-ttu-id="4042f-196">__사용자 지정 DNS(각 가상 네트워크에서)__:</span><span class="sxs-lookup"><span data-stu-id="4042f-196">__Custom DNS__ (in each virtual network):</span></span>

            * <span data-ttu-id="4042f-197">Hello 가상 네트워크의 DNS 접미사 hello에 대 한 요청 toohello 사용자 지정 DNS 서버에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-197">Requests for hello DNS suffix of hello virtual networks are forwarded toohello custom DNS servers.</span></span> <span data-ttu-id="4042f-198">각 가상 네트워크에 DNS hello는 해당 네트워크 내에서 리소스를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-198">hello DNS in each virtual network is responsible for resolving resources within its network.</span></span>

            * <span data-ttu-id="4042f-199">다른 모든 요청 toohello Azure 재귀 확인자를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-199">Forward all other requests toohello Azure recursive resolver.</span></span> <span data-ttu-id="4042f-200">hello 재귀 확인자는 로컬 해결 하 고 인터넷 리소스 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-200">hello recursive resolver is responsible for resolving local and internet resources.</span></span>

        <span data-ttu-id="4042f-201">각 네트워크에 대 한 hello DNS 서버, DNS 접미사에 따라 요청 toohello를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-201">hello DNS server for each network forwards requests toohello other, based on DNS suffix.</span></span> <span data-ttu-id="4042f-202">다른 요청 hello Azure 재귀 확인자를 사용 하 여 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-202">Other requests are resolved using hello Azure recursive resolver.</span></span>

    <span data-ttu-id="4042f-203">예를 보려면 각 구성 참조 hello [예제: 사용자 지정 DNS](#example-dns) 섹션.</span><span class="sxs-lookup"><span data-stu-id="4042f-203">For an example of each configuration, see hello [Example: Custom DNS](#example-dns) section.</span></span>

<span data-ttu-id="4042f-204">자세한 내용은 참조 hello [Vm 및 역할 인스턴스에 대 한 이름 확인](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) 문서.</span><span class="sxs-lookup"><span data-stu-id="4042f-204">For more information, see hello [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) document.</span></span>

## <a name="directly-connect-toohadoop-services"></a><span data-ttu-id="4042f-205">TooHadoop 서비스에 직접 연결</span><span class="sxs-lookup"><span data-stu-id="4042f-205">Directly connect tooHadoop services</span></span>

<span data-ttu-id="4042f-206">HDInsight에 대 한 대부분 설명서 hello를 통해 액세스 toohello 클러스터 있다고 가정 합니다. 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-206">Most documentation on HDInsight assumes that you have access toohello cluster over hello internet.</span></span> <span data-ttu-id="4042f-207">예를 들어, https://CLUSTERNAME.azurehdinsight.net에 toohello 클러스터를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-207">For example, that you can connect toohello cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="4042f-208">이 주소에서 UDRs toorestrict 액세스 hello 인터넷 또는 Nsg를 사용 하는 경우에 사용할 수 없는 hello 공용 게이트웨이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-208">This address uses hello public gateway, which is not available if you have used NSGs or UDRs toorestrict access from hello internet.</span></span>

<span data-ttu-id="4042f-209">tooconnect tooAmbari 및 hello 가상 네트워크를 통해 다른 웹 페이지 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-209">tooconnect tooAmbari and other web pages through hello virtual network, use hello following steps:</span></span>

1. <span data-ttu-id="4042f-210">hello HDInsight 클러스터 노드의 toodiscover hello 내부 정규화 된 도메인 이름 (FQDN) hello 메서드를 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-210">toodiscover hello internal fully qualified domain names (FQDN) of hello HDInsight cluster nodes, use one of hello following methods:</span></span>

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

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

    <span data-ttu-id="4042f-211">반환 되는 노드 hello 목록의 hello FQDN hello에 대 한 헤드 노드 찾아 hello Fqdn tooconnect tooAmbari 및 기타 웹 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-211">In hello list of nodes returned, find hello FQDN for hello head nodes and use hello FQDNs tooconnect tooAmbari and other web services.</span></span> <span data-ttu-id="4042f-212">사용 예를 들어 `http://<headnode-fqdn>:8080` tooaccess Ambari 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-212">For example, use `http://<headnode-fqdn>:8080` tooaccess Ambari.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4042f-213">일부 서비스의 hello 헤드 노드에 호스팅되 한 번에 한 노드에서 활성화만 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-213">Some services hosted on hello head nodes are only active on one node at a time.</span></span> <span data-ttu-id="4042f-214">헤드 노드 하나에서 서비스에 액세스 하면 404 오류를 반환 하는 경우 toohello 다른 헤드 노드를 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-214">If you try accessing a service on one head node and it returns a 404 error, switch toohello other head node.</span></span>

2. <span data-ttu-id="4042f-215">toodetermine hello 노드 및 서비스를 사용할 수 있는 포트 참조 hello [HDInsight의 Hadoop 서비스에 의해 사용 되는 포트](./hdinsight-hadoop-port-settings-for-services.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="4042f-215">toodetermine hello node and port that a service is available on, see hello [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

## <span data-ttu-id="4042f-216"><a id="networktraffic"></a> 네트워크 트래픽 제어</span><span class="sxs-lookup"><span data-stu-id="4042f-216"><a id="networktraffic"></a> Controlling network traffic</span></span>

<span data-ttu-id="4042f-217">메서드를 다음 hello를 사용 하 여 Azure 가상 네트워크에서 네트워크 트래픽을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-217">Network traffic in an Azure Virtual Networks can be controlled using hello following methods:</span></span>

* <span data-ttu-id="4042f-218">**네트워크 보안 그룹** (NSG) toofilter 인바운드 및 아웃 바운드 트래픽을 toohello 네트워크를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-218">**Network security groups** (NSG) allow you toofilter inbound and outbound traffic toohello network.</span></span> <span data-ttu-id="4042f-219">자세한 내용은 참조 hello [네트워크 보안 그룹과 네트워크 트래픽 필터](../virtual-network/virtual-networks-nsg.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="4042f-219">For more information, see hello [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    > [!WARNING]
    > <span data-ttu-id="4042f-220">HDInsight는 아웃바운드 트래픽을 제한하도록 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-220">HDInsight does not support restricting outbound traffic.</span></span>

* <span data-ttu-id="4042f-221">**사용자 정의 경로** (UDR) hello 네트워크의 리소스 간의 트래픽 흐름 방식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-221">**User-defined routes** (UDR) define how traffic flows between resources in hello network.</span></span> <span data-ttu-id="4042f-222">자세한 내용은 참조 hello [사용자 정의 경로 및 IP 전달](../virtual-network/virtual-networks-udr-overview.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="4042f-222">For more information, see hello [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md) document.</span></span>

* <span data-ttu-id="4042f-223">**네트워크 가상 어플라이언스** 방화벽, 라우터 등과 같은 장치의 기능을 hello를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-223">**Network virtual appliances** replicate hello functionality of devices such as firewalls and routers.</span></span> <span data-ttu-id="4042f-224">자세한 내용은 참조 hello [네트워크 어플라이언스에](https://azure.microsoft.com/solutions/network-appliances) 문서.</span><span class="sxs-lookup"><span data-stu-id="4042f-224">For more information, see hello [Network Appliances](https://azure.microsoft.com/solutions/network-appliances) document.</span></span>

<span data-ttu-id="4042f-225">HDInsight 관리 되는 서비스로 Azure 클라우드 hello에 대 한 무제한 액세스 tooAzure 상태 및 관리 서비스를 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-225">As a managed service, HDInsight requires unrestricted access tooAzure health and management services in hello Azure cloud.</span></span> <span data-ttu-id="4042f-226">NSG 및 UDR을 사용할 때는 이러한 서비스에서 HDInsight와 계속 통신할 수 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-226">When using NSGs and UDRs, you must ensure that HDInsight these services can still communicate with HDInsight.</span></span>

<span data-ttu-id="4042f-227">HDInsight는 여러 포트에서 서비스를 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-227">HDInsight exposes services on several ports.</span></span> <span data-ttu-id="4042f-228">가상 기기 방화벽을 사용 하는 경우에 이러한 서비스에 사용 되는 포트를 hello의 트래픽을 허용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-228">When using a virtual appliance firewall, you must allow traffic on hello ports used for these services.</span></span> <span data-ttu-id="4042f-229">자세한 내용은 hello [필요한 포트] 섹션을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-229">For more information, see hello [Required ports] section.</span></span>

### <span data-ttu-id="4042f-230"><a id="hdinsight-ip"></a> 네트워크 보안 그룹 및 사용자 정의 경로가 있는 HDInsight</span><span class="sxs-lookup"><span data-stu-id="4042f-230"><a id="hdinsight-ip"></a> HDInsight with network security groups and user-defined routes</span></span>

<span data-ttu-id="4042f-231">사용 하려는 경우 **네트워크 보안 그룹** 또는 **사용자 정의 경로** toocontrol 네트워크 트래픽 hello 동작 HDInsight를 설치 하기 전에 다음을 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4042f-231">If you plan on using **network security groups** or **user-defined routes** toocontrol network traffic, perform hello following actions before installing HDInsight:</span></span>

1. <span data-ttu-id="4042f-232">Hello Azure 지역 toouse HDInsight에 대 한 계획을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-232">Identify hello Azure region that you plan toouse for HDInsight.</span></span>

2. <span data-ttu-id="4042f-233">HDInsight에서 요구 하는 hello IP 주소를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-233">Identify hello IP addresses required by HDInsight.</span></span> <span data-ttu-id="4042f-234">자세한 내용은 참조 hello [HDInsight에 필요한 IP 주소](#hdinsight-ip) 섹션.</span><span class="sxs-lookup"><span data-stu-id="4042f-234">For more information, see hello [IP Addresses required by HDInsight](#hdinsight-ip) section.</span></span>

3. <span data-ttu-id="4042f-235">만들기 또는 수정 hello 네트워크 보안 그룹 또는 tooinstall HDInsight를 계획 하는 hello 서브넷에 대 한 사용자 정의 경로에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-235">Create or modify hello network security groups or user-defined routes for hello subnet that you plan tooinstall HDInsight into.</span></span>

    * <span data-ttu-id="4042f-236">__네트워크 보안 그룹__: 허용 __인바운드__ 포트에서 트래픽을 __443__ hello IP 주소의 기능과 동일에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-236">__Network security groups__: allow __inbound__ traffic on port __443__ from hello IP addresses.</span></span>
    * <span data-ttu-id="4042f-237">__사용자 정의 경로__: 경로 tooeach IP 주소를 만들고 hello 설정 __다음 홉 형식__ too__Internet__ 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-237">__User-defined routes__: create a route tooeach IP address and set hello __Next hop type__ too__Internet__.</span></span>

<span data-ttu-id="4042f-238">네트워크 보안 그룹 또는 사용자 정의 된 경로에 대 한 자세한 내용은 hello 설명서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="4042f-238">For more information on network security groups or user-defined routes, see hello following documentation:</span></span>

* [<span data-ttu-id="4042f-239">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="4042f-239">Network security group</span></span>](../virtual-network/virtual-networks-nsg.md)

* [<span data-ttu-id="4042f-240">사용자 정의 경로</span><span class="sxs-lookup"><span data-stu-id="4042f-240">User-defined routes</span></span>](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a><span data-ttu-id="4042f-241">강제 터널링</span><span class="sxs-lookup"><span data-stu-id="4042f-241">Forced tunneling</span></span>

<span data-ttu-id="4042f-242">강제 터널링은 하나의 사용자 정의 라우팅 구성 강제 tooa 특정 네트워크 또는 온-프레미스 네트워크와 같은 위치에서 서브넷의에서 모든 트래픽이입니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-242">Forced tunneling is a user-defined routing configuration where all traffic from a subnet is forced tooa specific network or location, such as your on-premises network.</span></span> <span data-ttu-id="4042f-243">HDInsight는 강제 터널링을 지원하지 __않습니다.__</span><span class="sxs-lookup"><span data-stu-id="4042f-243">HDInsight does __not__ support forced tunneling.</span></span>

## <span data-ttu-id="4042f-244"><a id="hdinsight-ip"></a> 필수 IP 주소</span><span class="sxs-lookup"><span data-stu-id="4042f-244"><a id="hdinsight-ip"></a> Required IP addresses</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4042f-245">Azure health hello 및 관리 서비스 수 toocommunicate HDInsight와 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-245">hello Azure health and management services must be able toocommunicate with HDInsight.</span></span> <span data-ttu-id="4042f-246">네트워크 보안 그룹 또는 사용자 정의 경로 사용 하는 경우 트래픽을 hello에서 이러한 서비스 tooreach HDInsight에 대 한 IP 주소를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-246">If you use network security groups or user-defined routes, allow traffic from hello IP addresses for these services tooreach HDInsight.</span></span>
>
> <span data-ttu-id="4042f-247">네트워크 보안 그룹 또는 사용자 정의 경로 toocontrol 트래픽을 사용 하지 않는 경우에이 섹션을 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-247">If you do not use network security groups or user-defined routes toocontrol traffic, you can ignore this section.</span></span>

<span data-ttu-id="4042f-248">네트워크 보안 그룹 또는 사용자 정의 경로 사용 하는 경우에 hello Azure 상태 및 관리 서비스 tooreach HDInsight에서 트래픽을 허용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-248">If you use network security groups or user-defined routes, you must allow traffic from hello Azure health and management services tooreach HDInsight.</span></span> <span data-ttu-id="4042f-249">사용 하 여 hello 다음 단계 toofind hello IP 주소를 허용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-249">Use hello following steps toofind hello IP addresses that must be allowed:</span></span>

1. <span data-ttu-id="4042f-250">항상 트래픽을 hello 다음 IP 주소를 허용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-250">You must always allow traffic from hello following IP addresses:</span></span>

    | <span data-ttu-id="4042f-251">IP 주소</span><span class="sxs-lookup"><span data-stu-id="4042f-251">IP address</span></span> | <span data-ttu-id="4042f-252">허용되는 포트</span><span class="sxs-lookup"><span data-stu-id="4042f-252">Allowed port</span></span> | <span data-ttu-id="4042f-253">방향</span><span class="sxs-lookup"><span data-stu-id="4042f-253">Direction</span></span> |
    | ---- | ----- | ----- |
    | <span data-ttu-id="4042f-254">168.61.49.99</span><span class="sxs-lookup"><span data-stu-id="4042f-254">168.61.49.99</span></span> | <span data-ttu-id="4042f-255">443</span><span class="sxs-lookup"><span data-stu-id="4042f-255">443</span></span> | <span data-ttu-id="4042f-256">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-256">Inbound</span></span> |
    | <span data-ttu-id="4042f-257">23.99.5.239</span><span class="sxs-lookup"><span data-stu-id="4042f-257">23.99.5.239</span></span> | <span data-ttu-id="4042f-258">443</span><span class="sxs-lookup"><span data-stu-id="4042f-258">443</span></span> | <span data-ttu-id="4042f-259">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-259">Inbound</span></span> |
    | <span data-ttu-id="4042f-260">168.61.48.131</span><span class="sxs-lookup"><span data-stu-id="4042f-260">168.61.48.131</span></span> | <span data-ttu-id="4042f-261">443</span><span class="sxs-lookup"><span data-stu-id="4042f-261">443</span></span> | <span data-ttu-id="4042f-262">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-262">Inbound</span></span> |
    | <span data-ttu-id="4042f-263">138.91.141.162</span><span class="sxs-lookup"><span data-stu-id="4042f-263">138.91.141.162</span></span> | <span data-ttu-id="4042f-264">443</span><span class="sxs-lookup"><span data-stu-id="4042f-264">443</span></span> | <span data-ttu-id="4042f-265">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-265">Inbound</span></span> |

2. <span data-ttu-id="4042f-266">HDInsight 클러스터에 hello 영역을 다음 중 하나에 있으면 hello 지역에 대해 나열 된 hello IP 주소에서 트래픽을 허용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-266">If your HDInsight cluster is in one of hello following regions, then you must allow traffic from hello IP addresses listed for hello region:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4042f-267">사용 하는 Azure 지역 hello 나열 되지 않으면 사용만 hello 1 단계에서 네 개의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-267">If hello Azure region you are using is not listed, then only use hello four IP addresses from step 1.</span></span>

    | <span data-ttu-id="4042f-268">국가</span><span class="sxs-lookup"><span data-stu-id="4042f-268">Country</span></span> | <span data-ttu-id="4042f-269">지역</span><span class="sxs-lookup"><span data-stu-id="4042f-269">Region</span></span> | <span data-ttu-id="4042f-270">허용된 IP 주소</span><span class="sxs-lookup"><span data-stu-id="4042f-270">Allowed IP addresses</span></span> | <span data-ttu-id="4042f-271">허용되는 포트</span><span class="sxs-lookup"><span data-stu-id="4042f-271">Allowed port</span></span> | <span data-ttu-id="4042f-272">방향</span><span class="sxs-lookup"><span data-stu-id="4042f-272">Direction</span></span> |
    | ---- | ---- | ---- | ---- | ----- |
    | <span data-ttu-id="4042f-273">아시아</span><span class="sxs-lookup"><span data-stu-id="4042f-273">Asia</span></span> | <span data-ttu-id="4042f-274">동아시아</span><span class="sxs-lookup"><span data-stu-id="4042f-274">East Asia</span></span> | <span data-ttu-id="4042f-275">23.102.235.122</span><span class="sxs-lookup"><span data-stu-id="4042f-275">23.102.235.122</span></span></br><span data-ttu-id="4042f-276">52.175.38.134</span><span class="sxs-lookup"><span data-stu-id="4042f-276">52.175.38.134</span></span> | <span data-ttu-id="4042f-277">443</span><span class="sxs-lookup"><span data-stu-id="4042f-277">443</span></span> | <span data-ttu-id="4042f-278">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-278">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="4042f-279">동남아시아</span><span class="sxs-lookup"><span data-stu-id="4042f-279">Southeast Asia</span></span> | <span data-ttu-id="4042f-280">13.76.245.160</span><span class="sxs-lookup"><span data-stu-id="4042f-280">13.76.245.160</span></span></br><span data-ttu-id="4042f-281">13.76.136.249</span><span class="sxs-lookup"><span data-stu-id="4042f-281">13.76.136.249</span></span> | <span data-ttu-id="4042f-282">443</span><span class="sxs-lookup"><span data-stu-id="4042f-282">443</span></span> | <span data-ttu-id="4042f-283">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-283">Inbound</span></span> |
    | <span data-ttu-id="4042f-284">오스트레일리아</span><span class="sxs-lookup"><span data-stu-id="4042f-284">Australia</span></span> | <span data-ttu-id="4042f-285">오스트레일리아 동부</span><span class="sxs-lookup"><span data-stu-id="4042f-285">Australia East</span></span> | <span data-ttu-id="4042f-286">104.210.84.115</span><span class="sxs-lookup"><span data-stu-id="4042f-286">104.210.84.115</span></span></br><span data-ttu-id="4042f-287">13.75.152.195</span><span class="sxs-lookup"><span data-stu-id="4042f-287">13.75.152.195</span></span> | <span data-ttu-id="4042f-288">443</span><span class="sxs-lookup"><span data-stu-id="4042f-288">443</span></span> | <span data-ttu-id="4042f-289">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-289">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="4042f-290">오스트레일리아 남동부</span><span class="sxs-lookup"><span data-stu-id="4042f-290">Australia Southeast</span></span> | <span data-ttu-id="4042f-291">13.77.2.56</span><span class="sxs-lookup"><span data-stu-id="4042f-291">13.77.2.56</span></span></br><span data-ttu-id="4042f-292">13.77.2.94</span><span class="sxs-lookup"><span data-stu-id="4042f-292">13.77.2.94</span></span> | <span data-ttu-id="4042f-293">443</span><span class="sxs-lookup"><span data-stu-id="4042f-293">443</span></span> | <span data-ttu-id="4042f-294">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-294">Inbound</span></span> |
    | <span data-ttu-id="4042f-295">브라질</span><span class="sxs-lookup"><span data-stu-id="4042f-295">Brazil</span></span> | <span data-ttu-id="4042f-296">브라질 남부</span><span class="sxs-lookup"><span data-stu-id="4042f-296">Brazil South</span></span> | <span data-ttu-id="4042f-297">191.235.84.104</span><span class="sxs-lookup"><span data-stu-id="4042f-297">191.235.84.104</span></span></br><span data-ttu-id="4042f-298">191.235.87.113</span><span class="sxs-lookup"><span data-stu-id="4042f-298">191.235.87.113</span></span> | <span data-ttu-id="4042f-299">443</span><span class="sxs-lookup"><span data-stu-id="4042f-299">443</span></span> | <span data-ttu-id="4042f-300">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-300">Inbound</span></span> |
    | <span data-ttu-id="4042f-301">캐나다</span><span class="sxs-lookup"><span data-stu-id="4042f-301">Canada</span></span> | <span data-ttu-id="4042f-302">캐나다 동부</span><span class="sxs-lookup"><span data-stu-id="4042f-302">Canada East</span></span> | <span data-ttu-id="4042f-303">52.229.127.96</span><span class="sxs-lookup"><span data-stu-id="4042f-303">52.229.127.96</span></span></br><span data-ttu-id="4042f-304">52.229.123.172</span><span class="sxs-lookup"><span data-stu-id="4042f-304">52.229.123.172</span></span> | <span data-ttu-id="4042f-305">443</span><span class="sxs-lookup"><span data-stu-id="4042f-305">443</span></span> | <span data-ttu-id="4042f-306">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-306">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="4042f-307">캐나다 중부</span><span class="sxs-lookup"><span data-stu-id="4042f-307">Canada Central</span></span> | <span data-ttu-id="4042f-308">52.228.37.66</span><span class="sxs-lookup"><span data-stu-id="4042f-308">52.228.37.66</span></span></br><span data-ttu-id="4042f-309">52.228.45.222</span><span class="sxs-lookup"><span data-stu-id="4042f-309">52.228.45.222</span></span> | <span data-ttu-id="4042f-310">443</span><span class="sxs-lookup"><span data-stu-id="4042f-310">443</span></span> | <span data-ttu-id="4042f-311">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-311">Inbound</span></span> |
    | <span data-ttu-id="4042f-312">중국</span><span class="sxs-lookup"><span data-stu-id="4042f-312">China</span></span> | <span data-ttu-id="4042f-313">중국 북부</span><span class="sxs-lookup"><span data-stu-id="4042f-313">China North</span></span> | <span data-ttu-id="4042f-314">42.159.96.170</span><span class="sxs-lookup"><span data-stu-id="4042f-314">42.159.96.170</span></span></br><span data-ttu-id="4042f-315">139.217.2.219</span><span class="sxs-lookup"><span data-stu-id="4042f-315">139.217.2.219</span></span> | <span data-ttu-id="4042f-316">443</span><span class="sxs-lookup"><span data-stu-id="4042f-316">443</span></span> | <span data-ttu-id="4042f-317">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-317">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="4042f-318">중국 동부</span><span class="sxs-lookup"><span data-stu-id="4042f-318">China East</span></span> | <span data-ttu-id="4042f-319">42.159.198.178</span><span class="sxs-lookup"><span data-stu-id="4042f-319">42.159.198.178</span></span></br><span data-ttu-id="4042f-320">42.159.234.157</span><span class="sxs-lookup"><span data-stu-id="4042f-320">42.159.234.157</span></span> | <span data-ttu-id="4042f-321">443</span><span class="sxs-lookup"><span data-stu-id="4042f-321">443</span></span> | <span data-ttu-id="4042f-322">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-322">Inbound</span></span> |
    | <span data-ttu-id="4042f-323">유럽</span><span class="sxs-lookup"><span data-stu-id="4042f-323">Europe</span></span> | <span data-ttu-id="4042f-324">북유럽</span><span class="sxs-lookup"><span data-stu-id="4042f-324">North Europe</span></span> | <span data-ttu-id="4042f-325">52.164.210.96</span><span class="sxs-lookup"><span data-stu-id="4042f-325">52.164.210.96</span></span></br><span data-ttu-id="4042f-326">13.74.153.132</span><span class="sxs-lookup"><span data-stu-id="4042f-326">13.74.153.132</span></span> | <span data-ttu-id="4042f-327">443</span><span class="sxs-lookup"><span data-stu-id="4042f-327">443</span></span> | <span data-ttu-id="4042f-328">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-328">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="4042f-329">서유럽</span><span class="sxs-lookup"><span data-stu-id="4042f-329">West Europe</span></span>| <span data-ttu-id="4042f-330">52.166.243.90</span><span class="sxs-lookup"><span data-stu-id="4042f-330">52.166.243.90</span></span></br><span data-ttu-id="4042f-331">52.174.36.244</span><span class="sxs-lookup"><span data-stu-id="4042f-331">52.174.36.244</span></span> | <span data-ttu-id="4042f-332">443</span><span class="sxs-lookup"><span data-stu-id="4042f-332">443</span></span> | <span data-ttu-id="4042f-333">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-333">Inbound</span></span> |
    | <span data-ttu-id="4042f-334">독일</span><span class="sxs-lookup"><span data-stu-id="4042f-334">Germany</span></span> | <span data-ttu-id="4042f-335">독일 중부</span><span class="sxs-lookup"><span data-stu-id="4042f-335">Germany Central</span></span> | <span data-ttu-id="4042f-336">51.4.146.68</span><span class="sxs-lookup"><span data-stu-id="4042f-336">51.4.146.68</span></span></br><span data-ttu-id="4042f-337">51.4.146.80</span><span class="sxs-lookup"><span data-stu-id="4042f-337">51.4.146.80</span></span> | <span data-ttu-id="4042f-338">443</span><span class="sxs-lookup"><span data-stu-id="4042f-338">443</span></span> | <span data-ttu-id="4042f-339">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-339">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="4042f-340">독일 북동부</span><span class="sxs-lookup"><span data-stu-id="4042f-340">Germany Northeast</span></span> | <span data-ttu-id="4042f-341">51.5.150.132</span><span class="sxs-lookup"><span data-stu-id="4042f-341">51.5.150.132</span></span></br><span data-ttu-id="4042f-342">51.5.144.101</span><span class="sxs-lookup"><span data-stu-id="4042f-342">51.5.144.101</span></span> | <span data-ttu-id="4042f-343">443</span><span class="sxs-lookup"><span data-stu-id="4042f-343">443</span></span> | <span data-ttu-id="4042f-344">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-344">Inbound</span></span> |
    | <span data-ttu-id="4042f-345">인도</span><span class="sxs-lookup"><span data-stu-id="4042f-345">India</span></span> | <span data-ttu-id="4042f-346">인도 중부</span><span class="sxs-lookup"><span data-stu-id="4042f-346">Central India</span></span> | <span data-ttu-id="4042f-347">52.172.153.209</span><span class="sxs-lookup"><span data-stu-id="4042f-347">52.172.153.209</span></span></br><span data-ttu-id="4042f-348">52.172.152.49</span><span class="sxs-lookup"><span data-stu-id="4042f-348">52.172.152.49</span></span> | <span data-ttu-id="4042f-349">443</span><span class="sxs-lookup"><span data-stu-id="4042f-349">443</span></span> | <span data-ttu-id="4042f-350">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-350">Inbound</span></span> |
    | <span data-ttu-id="4042f-351">일본</span><span class="sxs-lookup"><span data-stu-id="4042f-351">Japan</span></span> | <span data-ttu-id="4042f-352">일본 동부</span><span class="sxs-lookup"><span data-stu-id="4042f-352">Japan East</span></span> | <span data-ttu-id="4042f-353">13.78.125.90</span><span class="sxs-lookup"><span data-stu-id="4042f-353">13.78.125.90</span></span></br><span data-ttu-id="4042f-354">13.78.89.60</span><span class="sxs-lookup"><span data-stu-id="4042f-354">13.78.89.60</span></span> | <span data-ttu-id="4042f-355">443</span><span class="sxs-lookup"><span data-stu-id="4042f-355">443</span></span> | <span data-ttu-id="4042f-356">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-356">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="4042f-357">일본 서부</span><span class="sxs-lookup"><span data-stu-id="4042f-357">Japan West</span></span> | <span data-ttu-id="4042f-358">40.74.125.69</span><span class="sxs-lookup"><span data-stu-id="4042f-358">40.74.125.69</span></span></br><span data-ttu-id="4042f-359">138.91.29.150</span><span class="sxs-lookup"><span data-stu-id="4042f-359">138.91.29.150</span></span> | <span data-ttu-id="4042f-360">443</span><span class="sxs-lookup"><span data-stu-id="4042f-360">443</span></span> | <span data-ttu-id="4042f-361">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-361">Inbound</span></span> |
    | <span data-ttu-id="4042f-362">한국</span><span class="sxs-lookup"><span data-stu-id="4042f-362">Korea</span></span> | <span data-ttu-id="4042f-363">한국 중부</span><span class="sxs-lookup"><span data-stu-id="4042f-363">Korea Central</span></span> | <span data-ttu-id="4042f-364">52.231.39.142</span><span class="sxs-lookup"><span data-stu-id="4042f-364">52.231.39.142</span></span></br><span data-ttu-id="4042f-365">52.231.36.209</span><span class="sxs-lookup"><span data-stu-id="4042f-365">52.231.36.209</span></span> | <span data-ttu-id="4042f-366">433</span><span class="sxs-lookup"><span data-stu-id="4042f-366">433</span></span> | <span data-ttu-id="4042f-367">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-367">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="4042f-368">한국 남부</span><span class="sxs-lookup"><span data-stu-id="4042f-368">Korea South</span></span> | <span data-ttu-id="4042f-369">52.231.203.16</span><span class="sxs-lookup"><span data-stu-id="4042f-369">52.231.203.16</span></span></br><span data-ttu-id="4042f-370">52.231.205.214</span><span class="sxs-lookup"><span data-stu-id="4042f-370">52.231.205.214</span></span> | <span data-ttu-id="4042f-371">443</span><span class="sxs-lookup"><span data-stu-id="4042f-371">443</span></span> | <span data-ttu-id="4042f-372">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-372">Inbound</span></span>
    | <span data-ttu-id="4042f-373">영국</span><span class="sxs-lookup"><span data-stu-id="4042f-373">United Kingdom</span></span> | <span data-ttu-id="4042f-374">영국 서부</span><span class="sxs-lookup"><span data-stu-id="4042f-374">UK West</span></span> | <span data-ttu-id="4042f-375">51.141.13.110</span><span class="sxs-lookup"><span data-stu-id="4042f-375">51.141.13.110</span></span></br><span data-ttu-id="4042f-376">51.141.7.20</span><span class="sxs-lookup"><span data-stu-id="4042f-376">51.141.7.20</span></span> | <span data-ttu-id="4042f-377">443</span><span class="sxs-lookup"><span data-stu-id="4042f-377">443</span></span> | <span data-ttu-id="4042f-378">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-378">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="4042f-379">영국 남부</span><span class="sxs-lookup"><span data-stu-id="4042f-379">UK South</span></span> | <span data-ttu-id="4042f-380">51.140.47.39</span><span class="sxs-lookup"><span data-stu-id="4042f-380">51.140.47.39</span></span></br><span data-ttu-id="4042f-381">51.140.52.16</span><span class="sxs-lookup"><span data-stu-id="4042f-381">51.140.52.16</span></span> | <span data-ttu-id="4042f-382">443</span><span class="sxs-lookup"><span data-stu-id="4042f-382">443</span></span> | <span data-ttu-id="4042f-383">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-383">Inbound</span></span> |
    | <span data-ttu-id="4042f-384">미국</span><span class="sxs-lookup"><span data-stu-id="4042f-384">United States</span></span> | <span data-ttu-id="4042f-385">미국 중부</span><span class="sxs-lookup"><span data-stu-id="4042f-385">Central US</span></span> | <span data-ttu-id="4042f-386">13.67.223.215</span><span class="sxs-lookup"><span data-stu-id="4042f-386">13.67.223.215</span></span></br><span data-ttu-id="4042f-387">40.86.83.253</span><span class="sxs-lookup"><span data-stu-id="4042f-387">40.86.83.253</span></span> | <span data-ttu-id="4042f-388">443</span><span class="sxs-lookup"><span data-stu-id="4042f-388">443</span></span> | <span data-ttu-id="4042f-389">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-389">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="4042f-390">미국 중북부</span><span class="sxs-lookup"><span data-stu-id="4042f-390">North Central US</span></span> | <span data-ttu-id="4042f-391">157.56.8.38</span><span class="sxs-lookup"><span data-stu-id="4042f-391">157.56.8.38</span></span></br><span data-ttu-id="4042f-392">157.55.213.99</span><span class="sxs-lookup"><span data-stu-id="4042f-392">157.55.213.99</span></span> | <span data-ttu-id="4042f-393">443</span><span class="sxs-lookup"><span data-stu-id="4042f-393">443</span></span> | <span data-ttu-id="4042f-394">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-394">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="4042f-395">미국 중서부</span><span class="sxs-lookup"><span data-stu-id="4042f-395">West Central US</span></span> | <span data-ttu-id="4042f-396">52.161.23.15</span><span class="sxs-lookup"><span data-stu-id="4042f-396">52.161.23.15</span></span></br><span data-ttu-id="4042f-397">52.161.10.167</span><span class="sxs-lookup"><span data-stu-id="4042f-397">52.161.10.167</span></span> | <span data-ttu-id="4042f-398">443</span><span class="sxs-lookup"><span data-stu-id="4042f-398">443</span></span> | <span data-ttu-id="4042f-399">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-399">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="4042f-400">미국 서부 2</span><span class="sxs-lookup"><span data-stu-id="4042f-400">West US 2</span></span> | <span data-ttu-id="4042f-401">52.175.211.210</span><span class="sxs-lookup"><span data-stu-id="4042f-401">52.175.211.210</span></span></br><span data-ttu-id="4042f-402">52.175.222.222</span><span class="sxs-lookup"><span data-stu-id="4042f-402">52.175.222.222</span></span> | <span data-ttu-id="4042f-403">443</span><span class="sxs-lookup"><span data-stu-id="4042f-403">443</span></span> | <span data-ttu-id="4042f-404">인바운드</span><span class="sxs-lookup"><span data-stu-id="4042f-404">Inbound</span></span> |

    <span data-ttu-id="4042f-405">Hello IP에 대 한 정보에 대 한 Azure Government toouse 주소에 대 한 참조 hello [Azure Government Intelligence + 분석](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) 문서.</span><span class="sxs-lookup"><span data-stu-id="4042f-405">For information on hello IP addresses toouse for Azure Government, see hello [Azure Government Intelligence + Analytics](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) document.</span></span>

3. <span data-ttu-id="4042f-406">가상 네트워크에서 사용자 지정 DNS 서버를 사용하는 경우 __168.63.129.16__에서의 액세스도 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-406">If you use a custom DNS server with your virtual network, you must also allow access from __168.63.129.16__.</span></span> <span data-ttu-id="4042f-407">이 주소는 Azure 재귀 확인자입니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-407">This address is Azure's recursive resolver.</span></span> <span data-ttu-id="4042f-408">자세한 내용은 참조 hello [Vm 및 역할에 대 한 이름 확인 인스턴스](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="4042f-408">For more information, see hello [Name resolution for VMs and Role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) document.</span></span>

<span data-ttu-id="4042f-409">자세한 내용은 참조 hello [네트워크 트래픽을 제어](#networktraffic) 섹션.</span><span class="sxs-lookup"><span data-stu-id="4042f-409">For more information, see hello [Controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="4042f-410"><a id="hdinsight-ports"></a> 필수 포트</span><span class="sxs-lookup"><span data-stu-id="4042f-410"><a id="hdinsight-ports"></a> Required ports</span></span>

<span data-ttu-id="4042f-411">네트워크를 사용 하려는 경우 **가상 어플라이언스 방화벽** toosecure hello 가상 네트워크 포트를 수행 하는 hello에 아웃 바운드 트래픽을 허용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-411">If you plan on using a network **virtual appliance firewall** toosecure hello virtual network, you must allow outbound traffic on hello following ports:</span></span>

* <span data-ttu-id="4042f-412">53</span><span class="sxs-lookup"><span data-stu-id="4042f-412">53</span></span>
* <span data-ttu-id="4042f-413">443</span><span class="sxs-lookup"><span data-stu-id="4042f-413">443</span></span>
* <span data-ttu-id="4042f-414">1433</span><span class="sxs-lookup"><span data-stu-id="4042f-414">1433</span></span>
* <span data-ttu-id="4042f-415">11000-11999</span><span class="sxs-lookup"><span data-stu-id="4042f-415">11000-11999</span></span>
* <span data-ttu-id="4042f-416">14000-14999</span><span class="sxs-lookup"><span data-stu-id="4042f-416">14000-14999</span></span>

<span data-ttu-id="4042f-417">특정 서비스에 대 한 포트 목록이 참조 hello [HDInsight의 Hadoop 서비스에 의해 사용 되는 포트](hdinsight-hadoop-port-settings-for-services.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="4042f-417">For a list of ports for specific services, see hello [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

<span data-ttu-id="4042f-418">가상 어플라이언스에 대 한 방화벽 규칙에 대 한 자세한 내용은 참조 hello [가상 어플라이언스 시나리오](../virtual-network/virtual-network-scenario-udr-gw-nva.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="4042f-418">For more information on firewall rules for virtual appliances, see hello [virtual appliance scenario](../virtual-network/virtual-network-scenario-udr-gw-nva.md) document.</span></span>

## <span data-ttu-id="4042f-419"><a id="hdinsight-nsg"></a>예제: HDInsight에서 네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="4042f-419"><a id="hdinsight-nsg"></a>Example: network security groups with HDInsight</span></span>

<span data-ttu-id="4042f-420">이 섹션의 예제 hello hello로 HDInsight toocommunicate를 허용 하는 Azure 관리 서비스 toocreate 네트워크 보안 그룹을 규칙 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-420">hello examples in this section demonstrate how toocreate network security group rules that allow HDInsight toocommunicate with hello Azure management services.</span></span> <span data-ttu-id="4042f-421">Hello 예제를 사용 하기 전에 hello 사용 하는 Azure 지역에 대 한 hello IP 주소 toomatch hello 것을 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-421">Before using hello examples, adjust hello IP addresses toomatch hello ones for hello Azure region you are using.</span></span> <span data-ttu-id="4042f-422">Hello에서이 정보를 찾을 수 있습니다 [네트워크 보안 그룹 및 사용자 정의 경로 포함 하는 HDInsight](#hdinsight-ip) 섹션.</span><span class="sxs-lookup"><span data-stu-id="4042f-422">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-resource-management-template"></a><span data-ttu-id="4042f-423">Azure Resource Management 템플릿</span><span class="sxs-lookup"><span data-stu-id="4042f-423">Azure Resource Management template</span></span>

<span data-ttu-id="4042f-424">hello 다음 리소스 관리 템플릿을 만듭니다 인바운드 트래픽을 제한 하지만 HDInsight에 필요한 hello IP 주소에서의 트래픽을 허용 하는 가상 네트워크.</span><span class="sxs-lookup"><span data-stu-id="4042f-424">hello following Resource Management template creates a virtual network that restricts inbound traffic, but allows traffic from hello IP addresses required by HDInsight.</span></span> <span data-ttu-id="4042f-425">또한이 템플릿은 hello 가상 네트워크에는 HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-425">This template also creates an HDInsight cluster in hello virtual network.</span></span>

* [<span data-ttu-id="4042f-426">보안 Azure Virtual Network 및 HDInsight Hadoop 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="4042f-426">Deploy a secured Azure Virtual Network and an HDInsight Hadoop cluster</span></span>](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

> [!IMPORTANT]
> <span data-ttu-id="4042f-427">이 예제에서는 toomatch hello 사용 하는 Azure 지역에서에서 사용 하는 hello IP 주소를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-427">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="4042f-428">Hello에서이 정보를 찾을 수 있습니다 [네트워크 보안 그룹 및 사용자 정의 경로 포함 하는 HDInsight](#hdinsight-ip) 섹션.</span><span class="sxs-lookup"><span data-stu-id="4042f-428">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="4042f-429">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4042f-429">Azure PowerShell</span></span>

<span data-ttu-id="4042f-430">다음 PowerShell 스크립트 toocreate 인바운드 트래픽을 제한 하 고 hello 트래픽을 hello 유럽 북부 지역에 대 한 IP 주소를 허용 하는 가상 네트워크는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-430">Use hello following PowerShell script toocreate a virtual network that restricts inbound traffic and allows traffic from hello IP addresses for hello North Europe region.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4042f-431">이 예제에서는 toomatch hello 사용 하는 Azure 지역에서에서 사용 하는 hello IP 주소를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-431">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="4042f-432">Hello에서이 정보를 찾을 수 있습니다 [네트워크 보안 그룹 및 사용자 정의 경로 포함 하는 HDInsight](#hdinsight-ip) 섹션.</span><span class="sxs-lookup"><span data-stu-id="4042f-432">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with hello resource group hello virtual network is in"
$subnetName = "Replace with hello name of hello subnet that you plan toouse for HDInsight"
# Get hello Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get hello region hello Virtual network is in.
$location = $vnet.Location
# Get hello subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for hello HDInsight health and management services.
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
# Set hello changes toohello security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply hello NSG toohello subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> <span data-ttu-id="4042f-433">이 예제에서는 tooadd 규칙 tooallow hello 필요한 IP 주소에서 트래픽을 인바운드 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-433">This example demonstrates how tooadd rules tooallow inbound traffic on hello required IP addresses.</span></span> <span data-ttu-id="4042f-434">규칙 toorestrict 포함 하지 않으므로 다른 소스에서 인바운드 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-434">It does not contain a rule toorestrict inbound access from other sources.</span></span>
>
> <span data-ttu-id="4042f-435">다음 예제는 hello tooenable SSH hello 인터넷에서에서 액세스 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-435">hello following example demonstrates how tooenable SSH access from hello Internet:</span></span>
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a><span data-ttu-id="4042f-436">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4042f-436">Azure CLI</span></span>

<span data-ttu-id="4042f-437">다음 단계 toocreate 인바운드 트래픽을 제한 하지만 HDInsight에 필요한 hello IP 주소에서의 트래픽을 허용 하는 가상 네트워크는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-437">Use hello following steps toocreate a virtual network that restricts inbound traffic, but allows traffic from hello IP addresses required by HDInsight.</span></span>

1. <span data-ttu-id="4042f-438">새 네트워크 보안 그룹 이라는 명령 toocreate 다음 사용 하 여 hello `hdisecure`합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-438">Use hello following command toocreate a new network security group named `hdisecure`.</span></span> <span data-ttu-id="4042f-439">대체 **RESOURCEGROUPNAME** hello Azure 가상 네트워크를 포함 하는 hello 리소스 그룹을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-439">Replace **RESOURCEGROUPNAME** with hello resource group that contains hello Azure Virtual Network.</span></span> <span data-ttu-id="4042f-440">대체 **위치** hello 위치 (지역)와 해당 hello 그룹에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-440">Replace **LOCATION** with hello location (region) that hello group was created in.</span></span>

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    <span data-ttu-id="4042f-441">Hello 그룹을 만든 후 hello 새 그룹에 정보가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-441">Once hello group has been created, you receive information on hello new group.</span></span>

2. <span data-ttu-id="4042f-442">Hello tooadd 규칙 toohello 새 네트워크 보안 그룹 hello Azure HDInsight 상태 및 관리 서비스에서에서 포트 443에서 인바운드 통신을 허용 하는 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-442">Use hello following tooadd rules toohello new network security group that allow inbound communication on port 443 from hello Azure HDInsight health and management service.</span></span> <span data-ttu-id="4042f-443">대체 **RESOURCEGROUPNAME** hello Azure 가상 네트워크를 포함 하는 hello 리소스 그룹의 hello 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-443">Replace **RESOURCEGROUPNAME** with hello name of hello resource group that contains hello Azure Virtual Network.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4042f-444">이 예제에서는 toomatch hello 사용 하는 Azure 지역에서에서 사용 하는 hello IP 주소를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-444">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="4042f-445">Hello에서이 정보를 찾을 수 있습니다 [네트워크 보안 그룹 및 사용자 정의 경로 포함 하는 HDInsight](#hdinsight-ip) 섹션.</span><span class="sxs-lookup"><span data-stu-id="4042f-445">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. <span data-ttu-id="4042f-446">이 네트워크 보안 그룹을 다음 명령을 사용 하 여 hello에 대 한 tooretrieve hello의 고유 식별자:</span><span class="sxs-lookup"><span data-stu-id="4042f-446">tooretrieve hello unique identifier for this network security group, use hello following command:</span></span>

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    <span data-ttu-id="4042f-447">이 명령은 텍스트 다음 값 비슷한 toohello를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-447">This command returns a value similar toohello following text:</span></span>

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    <span data-ttu-id="4042f-448">Hello 예상 결과 얻지 못할 경우 hello 명령에서 id 주위 큰따옴표를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-448">Use double-quotes around id in hello command if you don't get hello expected results.</span></span>

4. <span data-ttu-id="4042f-449">다음 명령은 tooapply hello 네트워크 보안 그룹 tooa 서브넷 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-449">Use hello following command tooapply hello network security group tooa subnet.</span></span> <span data-ttu-id="4042f-450">Hello 대체 __GUID__ 및 __RESOURCEGROUPNAME__ hello 이전 단계에서 반환 된 것과 hello 사용 하 여 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-450">Replace hello __GUID__ and __RESOURCEGROUPNAME__ values with hello ones returned from hello previous step.</span></span> <span data-ttu-id="4042f-451">대체 __VNETNAME__ 및 __SUBNETNAME__ hello 가상 네트워크 이름 및 toocreate 서브넷 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-451">Replace __VNETNAME__ and __SUBNETNAME__ with hello virtual network name and subnet name that you want toocreate.</span></span>

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    <span data-ttu-id="4042f-452">이 명령은 완료 되 면 hello 가상 네트워크에 HDInsight를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-452">Once this command completes, you can install HDInsight into hello Virtual Network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4042f-453">이러한 단계는 access toohello HDInsight 상태 및 관리 서비스에 hello Azure 클라우드만 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-453">These steps only open access toohello HDInsight health and management service on hello Azure cloud.</span></span> <span data-ttu-id="4042f-454">모든 다른 액세스 toohello HDInsight 클러스터에서 가상 네트워크 외부 hello 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-454">Any other access toohello HDInsight cluster from outside hello Virtual Network is blocked.</span></span> <span data-ttu-id="4042f-455">tooenable 액세스 hello 가상 네트워크 외부에서 추가 네트워크 보안 그룹 규칙을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-455">tooenable access from outside hello virtual network, you must add additional Network Security Group rules.</span></span>
>
> <span data-ttu-id="4042f-456">다음 예제는 hello tooenable SSH hello 인터넷에서에서 액세스 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-456">hello following example demonstrates how tooenable SSH access from hello Internet:</span></span>
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <span data-ttu-id="4042f-457"><a id="example-dns"></a> 예제: DNS 구성</span><span class="sxs-lookup"><span data-stu-id="4042f-457"><a id="example-dns"></a> Example: DNS configuration</span></span>

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a><span data-ttu-id="4042f-458">가상 네트워크와 연결된 온-프레미스 네트워크 간에 이름 확인</span><span class="sxs-lookup"><span data-stu-id="4042f-458">Name resolution between a virtual network and a connected on-premises network</span></span>

<span data-ttu-id="4042f-459">이 예제에서는 다음 가정을 hello:</span><span class="sxs-lookup"><span data-stu-id="4042f-459">This example makes hello following assumptions:</span></span>

* <span data-ttu-id="4042f-460">Azure 가상 네트워크 VPN 게이트웨이 사용 하 여 연결 된 tooan 온-프레미스 네트워크를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-460">You have an Azure Virtual Network that is connected tooan on-premises network using a VPN gateway.</span></span>

* <span data-ttu-id="4042f-461">hello 가상 네트워크의 사용자 지정 DNS 서버 hello hello 운영 체제로 Linux 또는 Unix 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-461">hello custom DNS server in hello virtual network is running Linux or Unix as hello operating system.</span></span>

* <span data-ttu-id="4042f-462">[바인딩](https://www.isc.org/downloads/bind/) hello 사용자 지정 DNS 서버에 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-462">[Bind](https://www.isc.org/downloads/bind/) is installed on hello custom DNS server.</span></span>

<span data-ttu-id="4042f-463">Hello 사용자 지정 DNS 서버 hello 가상 네트워크에서:</span><span class="sxs-lookup"><span data-stu-id="4042f-463">On hello custom DNS server in hello virtual network:</span></span>

1. <span data-ttu-id="4042f-464">Hello 가상 네트워크의 Azure PowerShell 또는 Azure CLI toofind hello DNS 접미사를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-464">Use either Azure PowerShell or Azure CLI toofind hello DNS suffix of hello virtual network:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="4042f-465">Hello 사용자 지정 DNS 서버에서 가상 네트워크 hello에 대 한 hello의 hello 콘텐츠로 텍스트를 다음 hello를 사용 하 여 `/etc/bind/named.conf.local` 파일:</span><span class="sxs-lookup"><span data-stu-id="4042f-465">On hello custom DNS server for hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.local` file:</span></span>

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    <span data-ttu-id="4042f-466">Hello 대체 `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` 가상 네트워크의 DNS 접미사 hello 사용 하 여 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-466">Replace hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with hello DNS suffix of your virtual network.</span></span>

    <span data-ttu-id="4042f-467">이 구성은 Azure 재귀 해결 프로그램을 toohello hello 가상 네트워크의 DNS 접미사 hello에 대 한 모든 DNS 요청을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-467">This configuration routes all DNS requests for hello DNS suffix of hello virtual network toohello Azure recursive resolver.</span></span>

2. <span data-ttu-id="4042f-468">Hello 사용자 지정 DNS 서버에서 가상 네트워크 hello에 대 한 hello의 hello 콘텐츠로 텍스트를 다음 hello를 사용 하 여 `/etc/bind/named.conf.options` 파일:</span><span class="sxs-lookup"><span data-stu-id="4042f-468">On hello custom DNS server for hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients tooaccept requests from
    // TODO: Add hello IP range of hello joined network toothis list
    acl goodclients {
        10.0.0.0/16; # IP address range of hello virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent toohello following
            forwarders {
                192.168.0.1; # Replace with hello IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="4042f-469">Hello 대체 `10.0.0.0/16` 가상 네트워크의 IP 주소 범위 hello 사용 하 여 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-469">Replace hello `10.0.0.0/16` value with hello IP address range of your virtual network.</span></span> <span data-ttu-id="4042f-470">이 항목으로 이 범위 내의 주소로 이름 확인 요청이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-470">This entry allows name resolution requests addresses within this range.</span></span>

    * <span data-ttu-id="4042f-471">Hello 온-프레미스 네트워크 toohello의 hello IP 주소 범위 추가 `acl goodclients { ... }` 섹션.</span><span class="sxs-lookup"><span data-stu-id="4042f-471">Add hello IP address range of hello on-premises network toohello `acl goodclients { ... }` section.</span></span>  <span data-ttu-id="4042f-472">항목은 hello 온-프레미스 네트워크에 리소스에서 이름 확인 요청을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-472">entry allows name resolution requests from resources in hello on-premises network.</span></span>
    
    * <span data-ttu-id="4042f-473">Hello 값을 대체 `192.168.0.1` 온-프레미스 DNS 서버의 hello IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-473">Replace hello value `192.168.0.1` with hello IP address of your on-premises DNS server.</span></span> <span data-ttu-id="4042f-474">이 항목에는 모든 DNS 요청 toohello 온-프레미스 DNS 서버를 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-474">This entry routes all other DNS requests toohello on-premises DNS server.</span></span>

3. <span data-ttu-id="4042f-475">toouse hello 구성 바인딩을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-475">toouse hello configuration, restart Bind.</span></span> <span data-ttu-id="4042f-476">예: `sudo service bind9 restart`.</span><span class="sxs-lookup"><span data-stu-id="4042f-476">For example, `sudo service bind9 restart`.</span></span>

4. <span data-ttu-id="4042f-477">조건부 전달자 toohello 온-프레미스 DNS 서버를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-477">Add a conditional forwarder toohello on-premises DNS server.</span></span> <span data-ttu-id="4042f-478">단계 1 toohello 사용자 지정 DNS 서버에서 DNS 접미사 hello에 대 한 hello 조건 전달자 toosend 요청을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-478">Configure hello conditional forwarder toosend requests for hello DNS suffix from step 1 toohello custom DNS server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4042f-479">방법에 대 한 구체적인 정보에 대 한 DNS 소프트웨어에 대 한 hello 설명서를 참조 하십시오. tooadd 조건 전달자 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-479">Consult hello documentation for your DNS software for specifics on how tooadd a conditional forwarder.</span></span>

<span data-ttu-id="4042f-480">다음이 단계를 완료 한 후 tooresources 정규화 된 도메인 이름 (FQDN)을 사용 하 여 두 네트워크에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-480">After completing these steps, you can connect tooresources in either network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="4042f-481">이제 hello 가상 네트워크로 HDInsight를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-481">You can now install HDInsight into hello virtual network.</span></span>

### <a name="name-resolution-between-two-connected-virtual-networks"></a><span data-ttu-id="4042f-482">두 개의 연결된 가상 네트워크 간의 이름 확인</span><span class="sxs-lookup"><span data-stu-id="4042f-482">Name resolution between two connected virtual networks</span></span>

<span data-ttu-id="4042f-483">이 예제에서는 다음 가정을 hello:</span><span class="sxs-lookup"><span data-stu-id="4042f-483">This example makes hello following assumptions:</span></span>

* <span data-ttu-id="4042f-484">VPN 게이트웨이 또는 피어링을 사용하여 연결된 두 Azure Virtual Networks가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-484">You have two Azure Virtual Networks that are connected using either a VPN gateway or peering.</span></span>

* <span data-ttu-id="4042f-485">두 네트워크에에서 사용자 지정 DNS 서버 hello hello 운영 체제로 Linux 또는 Unix 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-485">hello custom DNS server in both networks is running Linux or Unix as hello operating system.</span></span>

* <span data-ttu-id="4042f-486">[바인딩](https://www.isc.org/downloads/bind/) hello 사용자 지정 DNS 서버에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-486">[Bind](https://www.isc.org/downloads/bind/) is installed on hello custom DNS servers.</span></span>

1. <span data-ttu-id="4042f-487">두 가상 네트워크의 Azure PowerShell 또는 Azure CLI toofind hello DNS 접미사를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-487">Use either Azure PowerShell or Azure CLI toofind hello DNS suffix of both virtual networks:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="4042f-488">콘텐츠로 사용 hello hello 텍스트를 다음으로 사용 하 여 hello `/etc/bind/named.config.local` hello 사용자 지정 DNS 서버에는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-488">Use hello following text as hello contents of hello `/etc/bind/named.config.local` file on hello custom DNS server.</span></span> <span data-ttu-id="4042f-489">두 가상 네트워크에서 사용자 지정 DNS 서버 hello에 이와 같이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-489">Make this change on hello custom DNS server in both virtual networks.</span></span>

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello IP address of hello DNS server in hello other virtual network
    };
    ```

    <span data-ttu-id="4042f-490">Hello 대체 `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` hello의 hello DNS 접미사를 사용 하 여 값 __다른__ 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-490">Replace hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with hello DNS suffix of hello __other__ virtual network.</span></span> <span data-ttu-id="4042f-491">이 항목의 hello 원격 네트워크 toohello hello DNS 접미사에 대 한 요청을 라우팅하는 네트워크에 있는 사용자 지정 DNS 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-491">This entry routes requests for hello DNS suffix of hello remote network toohello custom DNS in that network.</span></span>

3. <span data-ttu-id="4042f-492">콘텐츠로 사용 hello hello 텍스트를 다음 hello를 사용 하 여 hello 사용자 지정 DNS 서버에서 두 가상 네트워크에 `/etc/bind/named.conf.options` 파일:</span><span class="sxs-lookup"><span data-stu-id="4042f-492">On hello custom DNS servers in both virtual networks, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients tooaccept requests from
    acl goodclients {
        10.1.0.0/16; # hello IP address range of one virtual network
        10.0.0.0/16; # hello IP address range of hello other virtual network
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

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="4042f-493">Hello 대체 `10.0.0.0/16` 및 `10.1.0.0/16` 값 hello ip 주소 범위가 가상 네트워크의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-493">Replace hello `10.0.0.0/16` and `10.1.0.0/16` values with hello IP address ranges of your virtual networks.</span></span> <span data-ttu-id="4042f-494">이 항목을 사용 하면 각 네트워크의 리소스의 DNS 서버 hello toomake 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-494">This entry allows resources in each network toomake requests of hello DNS servers.</span></span>

    <span data-ttu-id="4042f-495">Hello 가상 네트워크 (예를 들어, microsoft.com) hello DNS 접미사에 대 한 하지 않은 모든 요청은 hello Azure 재귀 확인자에 의해 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-495">Any requests that are not for hello DNS suffixes of hello virtual networks (for example, microsoft.com) is handled by hello Azure recursive resolver.</span></span>

4. <span data-ttu-id="4042f-496">toouse hello 구성 바인딩을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-496">toouse hello configuration, restart Bind.</span></span> <span data-ttu-id="4042f-497">예를 들어, 두 DNS 서버에서 `sudo service bind9 restart`입니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-497">For example, `sudo service bind9 restart` on both DNS servers.</span></span>

<span data-ttu-id="4042f-498">다음이 단계를 완료 한 후 tooresources 정규화 된 도메인 이름 (FQDN)을 사용 하 여 hello 가상 네트워크에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-498">After completing these steps, you can connect tooresources in hello virtual network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="4042f-499">이제 hello 가상 네트워크로 HDInsight를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-499">You can now install HDInsight into hello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4042f-500">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4042f-500">Next steps</span></span>

* <span data-ttu-id="4042f-501">HDInsight tooconnect tooan 온-프레미스 네트워크 구성의 종단 간 예제를 참조 하십시오. [HDInsight 연결 tooan 온-프레미스 네트워크](./connect-on-premises-network.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-501">For an end-to-end example of configuring HDInsight tooconnect tooan on-premises network, see [Connect HDInsight tooan on-premises network](./connect-on-premises-network.md).</span></span>

* <span data-ttu-id="4042f-502">Azure 가상 네트워크에 대 한 자세한 내용은 참조 hello [Azure 가상 네트워크 개요](../virtual-network/virtual-networks-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4042f-502">For more information on Azure virtual networks, see hello [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="4042f-503">네트워크 보안 그룹에 대한 자세한 내용은 [네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4042f-503">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="4042f-504">사용자 정의 경로에 대한 자세한 내용은 [사용자 정의 경로 및 IP 전달](../virtual-network/virtual-networks-udr-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4042f-504">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>