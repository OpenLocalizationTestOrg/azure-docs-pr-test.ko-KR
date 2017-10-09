---
title: "VNet: 클래식: Azure Portal 사이의 연결 만들기 | Microsoft Docs"
description: "어떻게 함께 tooconnect Azure 가상 네트워크 및 PowerShell을 사용 하 여 hello Azure 클래식 포털입니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: f29c3c091d049ff96cf59f4c28ab86a100bcb5fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-connection-classic"></a><span data-ttu-id="7505f-103">VNet-VNet 연결(클래식) 구성</span><span class="sxs-lookup"><span data-stu-id="7505f-103">Configure a VNet-to-VNet connection (classic)</span></span>

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

<span data-ttu-id="7505f-104">이 문서에서는 어떻게 toocreate 가상 네트워크 간의 VPN 게이트웨이 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-104">This article shows you how toocreate a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="7505f-105">hello 가상 네트워크 수 같거나 다른 지역 hello와에서 동일 hello 또는 서로 다른 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-105">hello virtual networks can be in hello same or different regions, and from hello same or different subscriptions.</span></span> <span data-ttu-id="7505f-106">이 문서의 단계 hello toohello 클래식 배포 모델 및 hello Azure 포털에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-106">hello steps in this article apply toohello classic deployment model and hello Azure portal.</span></span> <span data-ttu-id="7505f-107">또한 서로 다른 배포 도구 또는 배포 모델을 사용 하 여 hello 다음 목록에서에서 다른 옵션을 선택 하 여이 구성을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7505f-108">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="7505f-108">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="7505f-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7505f-109">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="7505f-110">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7505f-110">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="7505f-111">Azure Portal(클래식)</span><span class="sxs-lookup"><span data-stu-id="7505f-111">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="7505f-112">다양한 배포 모델 간 연결 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7505f-112">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="7505f-113">다양한 배포 모델 간 연결 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="7505f-113">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![TooVNet VNet 연결 다이어그램](./media/vpn-gateway-howto-vnet-vnet-portal-classic/v2vclassic.png)

## <a name="about-vnet-to-vnet-connections"></a><span data-ttu-id="7505f-115">VNet 간 연결 정보</span><span class="sxs-lookup"><span data-stu-id="7505f-115">About VNet-to-VNet connections</span></span>

<span data-ttu-id="7505f-116">가상 네트워크 tooanother 가상 네트워크 (VNet 대 VNet) VPN 게이트웨이 사용 하 여 hello 클래식 배포 모델에 연결 하는 유사한 tooconnecting 가상 네트워크 tooan 온-프레미스 사이트 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-116">Connecting a virtual network tooanother virtual network (VNet-to-VNet) in hello classic deployment model using a VPN gateway is similar tooconnecting a virtual network tooan on-premises site location.</span></span> <span data-ttu-id="7505f-117">두 연결 유형에서는 VPN 게이트웨이 tooprovide IPsec/IKE를 사용 하 여 보안 터널을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-117">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span>

<span data-ttu-id="7505f-118">다른 구독 및 지역 hello Vnet에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-118">hello VNets you connect can be in different subscriptions and different regions.</span></span> <span data-ttu-id="7505f-119">다중 사이트 구성과 VNet tooVNet 통신을 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-119">You can combine VNet tooVNet communication with multi-site configurations.</span></span> <span data-ttu-id="7505f-120">이렇게 하면 프레미스 간 연결을 가상 네트워크 간 연결과 결합하는 네트워크 토폴로지를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-120">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity.</span></span>

![VNet tooVNet 연결](./media/vpn-gateway-howto-vnet-vnet-portal-classic/aboutconnections.png)

### <span data-ttu-id="7505f-122"><a name="why"></a>가상 네트워크에 연결하는 이유</span><span class="sxs-lookup"><span data-stu-id="7505f-122"><a name="why"></a>Why connect virtual networks?</span></span>

<span data-ttu-id="7505f-123">다음 이유로 hello에 대 한 tooconnect 가상 네트워크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-123">You may want tooconnect virtual networks for hello following reasons:</span></span>

* <span data-ttu-id="7505f-124">**지역 간 지리적 중복 및 지리적 상태**</span><span class="sxs-lookup"><span data-stu-id="7505f-124">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="7505f-125">인터넷 연결 끝점으로 이동하지 않고도 보안 연결을 통해 지역에서 복제 또는 동기화를 직접 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-125">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="7505f-126">Azure 부하 분산 장치 및 Microsoft 또는 타사 클러스터링 기술을 사용하여 여러 Azure 지역 간의 지리적 중복을 통해 워크로드의 가용성을 높게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-126">With Azure Load Balancer and Microsoft or third-party clustering technology, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="7505f-127">한 가지 중요 한 예는 SQL Always On 가용성 그룹이 여러 Azure 지역에 분산을 tooset 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-127">One important example is tooset up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="7505f-128">**분리 경계가 뚜렷한 지역별 다중 계층 응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="7505f-128">**Regional multi-tier applications with strong isolation boundary**</span></span>

  * <span data-ttu-id="7505f-129">내 동일한 hello 영역 강력한 격리 및 보안 계층 간 통신을 함께 연결 된 여러 Vnet으로 다중 계층 응용 프로그램을 설치할 수 없다.</span><span class="sxs-lookup"><span data-stu-id="7505f-129">Within hello same region, you can set up multi-tier applications with multiple VNets connected together with strong isolation and secure inter-tier communication.</span></span>
* <span data-ttu-id="7505f-130">**Azure의 구독 간/조직 간 통신**</span><span class="sxs-lookup"><span data-stu-id="7505f-130">**Cross subscription, inter-organization communication in Azure**</span></span>

  * <span data-ttu-id="7505f-131">Azure 구독이 여러 개인 경우 이제 가상 네트워크 간에 여러 구독의 작업을 안전하게 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-131">If you have multiple Azure subscriptions, you can connect workloads from different subscriptions together securely between virtual networks.</span></span>
  * <span data-ttu-id="7505f-132">엔터프라이즈 또는 서비스 공급자의 경우 이제 Azure 내의 보안 VPN 기술을 사용하여 조직 간 통신을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-132">For enterprises or service providers, you can enable cross-organization communication with secure VPN technology within Azure.</span></span>

<span data-ttu-id="7505f-133">VNet 대 VNet 연결에 대 한 자세한 내용은 참조 [VNet 대 VNet 고려 사항](#faq) hello이이 문서의 뒷부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-133">For more information about VNet-to-VNet connections, see [VNet-to-VNet considerations](#faq) at hello end of this article.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="7505f-134">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="7505f-134">Before you begin</span></span>

<span data-ttu-id="7505f-135">이 연습을 시작 하기 전에 다운로드 하 여 hello hello Azure 서비스 관리 (SM) PowerShell cmdlet의 최신 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-135">Before beginning this exercise, download and install hello latest version of hello Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="7505f-136">자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-136">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="7505f-137">대부분의 hello 단계를 위해 hello 포털을 사용 하지만 hello Vnet 간의 PowerShell toocreate hello 연결을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-137">We use hello portal for most of hello steps, but you must use PowerShell toocreate hello connections between hello VNets.</span></span> <span data-ttu-id="7505f-138">Azure 포털 hello를 사용 하 여 hello 연결을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-138">You can't create hello connections using hello Azure portal.</span></span>

## <span data-ttu-id="7505f-139"><a name="plan"></a>1단계 - IP 주소 범위 계획</span><span class="sxs-lookup"><span data-stu-id="7505f-139"><a name="plan"></a>Step 1 - Plan your IP address ranges</span></span>

<span data-ttu-id="7505f-140">것은 중요 한 toodecide hello 범위 수를 사용 하는 tooconfigure 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-140">It’s important toodecide hello ranges that you’ll use tooconfigure your virtual networks.</span></span> <span data-ttu-id="7505f-141">이 구성에 대 한 서로 또는 로컬 네트워크에 연결 하는 hello 사용 하 여 겹치는 VNet 범위 중 선택 되어 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-141">For this configuration, you must make sure that none of your VNet ranges overlap with each other, or with any of hello local networks that they connect to.</span></span>

<span data-ttu-id="7505f-142">hello 다음 표에서 방법의 예 toodefine Vnet입니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-142">hello following table shows an example of how toodefine your VNets.</span></span> <span data-ttu-id="7505f-143">지침 으로만 참고 hello 범위를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-143">Use hello ranges as a guideline only.</span></span> <span data-ttu-id="7505f-144">가상 네트워크에 대 한 hello 범위를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-144">Write down hello ranges for your virtual networks.</span></span> <span data-ttu-id="7505f-145">이 정보는 이후 단계에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-145">You need this information for later steps.</span></span>

<span data-ttu-id="7505f-146">**예제**</span><span class="sxs-lookup"><span data-stu-id="7505f-146">**Example**</span></span>

| <span data-ttu-id="7505f-147">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="7505f-147">Virtual Network</span></span> | <span data-ttu-id="7505f-148">주소 공간</span><span class="sxs-lookup"><span data-stu-id="7505f-148">Address Space</span></span> | <span data-ttu-id="7505f-149">지역</span><span class="sxs-lookup"><span data-stu-id="7505f-149">Region</span></span> | <span data-ttu-id="7505f-150">Toolocal 네트워크 사이트에 연결</span><span class="sxs-lookup"><span data-stu-id="7505f-150">Connects toolocal network site</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7505f-151">TestVNet1</span><span class="sxs-lookup"><span data-stu-id="7505f-151">TestVNet1</span></span> |<span data-ttu-id="7505f-152">TestVNet1</span><span class="sxs-lookup"><span data-stu-id="7505f-152">TestVNet1</span></span><br><span data-ttu-id="7505f-153">(10.11.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="7505f-153">(10.11.0.0/16)</span></span><br><span data-ttu-id="7505f-154">(10.12.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="7505f-154">(10.12.0.0/16)</span></span> |<span data-ttu-id="7505f-155">미국 동부</span><span class="sxs-lookup"><span data-stu-id="7505f-155">East US</span></span> |<span data-ttu-id="7505f-156">VNet4Local</span><span class="sxs-lookup"><span data-stu-id="7505f-156">VNet4Local</span></span><br><span data-ttu-id="7505f-157">(10.41.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="7505f-157">(10.41.0.0/16)</span></span><br><span data-ttu-id="7505f-158">(10.42.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="7505f-158">(10.42.0.0/16)</span></span> |
| <span data-ttu-id="7505f-159">TestVNet4</span><span class="sxs-lookup"><span data-stu-id="7505f-159">TestVNet4</span></span> |<span data-ttu-id="7505f-160">TestVNet4</span><span class="sxs-lookup"><span data-stu-id="7505f-160">TestVNet4</span></span><br><span data-ttu-id="7505f-161">(10.41.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="7505f-161">(10.41.0.0/16)</span></span><br><span data-ttu-id="7505f-162">(10.42.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="7505f-162">(10.42.0.0/16)</span></span> |<span data-ttu-id="7505f-163">미국 서부</span><span class="sxs-lookup"><span data-stu-id="7505f-163">West US</span></span> |<span data-ttu-id="7505f-164">VNet1Local</span><span class="sxs-lookup"><span data-stu-id="7505f-164">VNet1Local</span></span><br><span data-ttu-id="7505f-165">(10.11.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="7505f-165">(10.11.0.0/16)</span></span><br><span data-ttu-id="7505f-166">(10.12.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="7505f-166">(10.12.0.0/16)</span></span> |

## <span data-ttu-id="7505f-167"><a name="vnetvalues"></a>2 단계-hello 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="7505f-167"><a name="vnetvalues"></a>Step 2 - Create hello virtual networks</span></span>

<span data-ttu-id="7505f-168">두 개의 가상 네트워크를에서 만들고 hello [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-168">Create two virtual networks in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7505f-169">Hello 단계 toocreate 클래식 가상 네트워크에 대 한 참조 [클래식 가상 네트워크 만들기](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-169">For hello steps toocreate classic virtual networks, see [Create a classic virtual network](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span></span> 

<span data-ttu-id="7505f-170">Hello 포털 toocreate 클래식 가상 네트워크를 사용할 때는 hello hello 옵션 toocreate 클래식 가상 네트워크 나타나지 않으면 그렇지 않으면 다음 단계를 사용 하 여 toohello 가상 네트워크 블레이드를 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-170">When using hello portal toocreate a classic virtual network, you must navigate toohello virtual network blade by using hello following steps, otherwise hello option toocreate a classic virtual network does not appear:</span></span>

1. <span data-ttu-id="7505f-171">Hello 클릭 tooopen hello 'New' 블레이드 '+'.</span><span class="sxs-lookup"><span data-stu-id="7505f-171">Click hello '+' tooopen hello 'New' blade.</span></span>
2. <span data-ttu-id="7505f-172">' 가상 네트워크 ' hello 'hello 마켓플레이스' 필드에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-172">In hello 'Search hello marketplace' field, type 'Virtual Network'.</span></span> <span data-ttu-id="7505f-173">네트워킹을 대신 선택-> 가상 네트워크를 가져올 수 없습니다 hello 옵션 toocreate 클래식 VNet 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-173">If you instead, select Networking -> Virtual Network, you will not get hello option toocreate a classic VNet.</span></span>
3. <span data-ttu-id="7505f-174">' 가상 네트워크 ' hello 반환 된 목록에서에서 찾은 tooopen hello 가상 네트워크 블레이드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-174">Locate 'Virtual Network' from hello returned list and click it tooopen hello Virtual Network blade.</span></span> 
4. <span data-ttu-id="7505f-175">가상 네트워크 블레이드에서 hello '클래식' toocreate 클래식 VNet을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-175">On hello virtual network blade, select 'Classic' toocreate a classic VNet.</span></span> 

<span data-ttu-id="7505f-176">이 문서의 연습으로을 사용 하는 경우 다음 예제에서는 값에는 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-176">If you are using this article as an exercise, you can use hello following example values:</span></span>

<span data-ttu-id="7505f-177">**TestVNet1에 대한 값**</span><span class="sxs-lookup"><span data-stu-id="7505f-177">**Values for TestVNet1**</span></span>

<span data-ttu-id="7505f-178">이름: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="7505f-178">Name: TestVNet1</span></span><br>
<span data-ttu-id="7505f-179">주소 공간: 10.11.0.0/16, 10.12.0.0/16(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="7505f-179">Address space: 10.11.0.0/16, 10.12.0.0/16 (optional)</span></span><br>
<span data-ttu-id="7505f-180">서브넷 이름: 기본값</span><span class="sxs-lookup"><span data-stu-id="7505f-180">Subnet name: default</span></span><br>
<span data-ttu-id="7505f-181">서브넷 주소 범위: 10.11.0.1/24</span><span class="sxs-lookup"><span data-stu-id="7505f-181">Subnet address range: 10.11.0.1/24</span></span><br>
<span data-ttu-id="7505f-182">리소스 그룹: ClassicRG</span><span class="sxs-lookup"><span data-stu-id="7505f-182">Resource group: ClassicRG</span></span><br>
<span data-ttu-id="7505f-183">위치: 미국 동부</span><span class="sxs-lookup"><span data-stu-id="7505f-183">Location: East US</span></span><br>
<span data-ttu-id="7505f-184">게이트웨이 서브넷: 10.11.1.0/27</span><span class="sxs-lookup"><span data-stu-id="7505f-184">GatewaySubnet: 10.11.1.0/27</span></span>

<span data-ttu-id="7505f-185">**TestVNet4에 대한 값**</span><span class="sxs-lookup"><span data-stu-id="7505f-185">**Values for TestVNet4**</span></span>

<span data-ttu-id="7505f-186">이름: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="7505f-186">Name: TestVNet4</span></span><br>
<span data-ttu-id="7505f-187">주소 공간: 10.41.0.0/16, 10.42.0.0/16(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="7505f-187">Address space: 10.41.0.0/16, 10.42.0.0/16 (optional)</span></span><br>
<span data-ttu-id="7505f-188">서브넷 이름: 기본값</span><span class="sxs-lookup"><span data-stu-id="7505f-188">Subnet name: default</span></span><br>
<span data-ttu-id="7505f-189">서브넷 주소 범위: 10.41.0.1/24</span><span class="sxs-lookup"><span data-stu-id="7505f-189">Subnet address range: 10.41.0.1/24</span></span><br>
<span data-ttu-id="7505f-190">리소스 그룹: ClassicRG</span><span class="sxs-lookup"><span data-stu-id="7505f-190">Resource group: ClassicRG</span></span><br>
<span data-ttu-id="7505f-191">위치: 미국 서부</span><span class="sxs-lookup"><span data-stu-id="7505f-191">Location: West US</span></span><br>
<span data-ttu-id="7505f-192">게이트웨이 서브넷: 10.41.1.0/27</span><span class="sxs-lookup"><span data-stu-id="7505f-192">GatewaySubnet: 10.41.1.0/27</span></span>

<span data-ttu-id="7505f-193">**Vnet을 만들 때 주의 hello 설정을 다음에 유의 하십시오.**</span><span class="sxs-lookup"><span data-stu-id="7505f-193">**When creating your VNets, keep in mind hello following settings:**</span></span>

* <span data-ttu-id="7505f-194">**가상 네트워크 주소 공간** – hello 가상 네트워크 주소 공간 페이지에서 가상 네트워크에 대 한 toouse 되도록 hello 주소 범위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-194">**Virtual Network Address Spaces** – On hello Virtual Network Address Spaces page, specify hello address range that you want toouse for your virtual network.</span></span> <span data-ttu-id="7505f-195">이들은 toohello Vm 및 toothis 가상 네트워크를 배포 하는 다른 역할 인스턴스에 할당할 수 있는 hello 동적 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-195">These are hello dynamic IP addresses that will be assigned toohello VMs and other role instances that you deploy toothis virtual network.</span></span><br><span data-ttu-id="7505f-196">이 VNet에 연결 하는 다른 Vnet 또는 온-프레미스 위치 hello 하는 hello 주소 공간 선택에 대 한 hello 주소 공간과 겹칠 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-196">hello address spaces you select cannot overlap with hello address spaces for any of hello other VNets or on-premises locations that this VNet will connect to.</span></span>

* <span data-ttu-id="7505f-197">**위치** – 가상 네트워크를 만들 때 Azure 위치(지역)와 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-197">**Location** – When you create a virtual network, you associate it with an Azure location (region).</span></span> <span data-ttu-id="7505f-198">예를 들어 있는 Vm에 배포 tooyour 가상 네트워크 toobe West US에 물리적으로 배치 하려면 해당 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-198">For example, if you want your VMs that are deployed tooyour virtual network toobe physically located in West US, select that location.</span></span> <span data-ttu-id="7505f-199">만든 후 가상 네트워크와 연결 된 hello 위치를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-199">You can’t change hello location associated with your virtual network after you create it.</span></span>

<span data-ttu-id="7505f-200">**Vnet을 만든 후에 다음 설정을 hello를 추가할 수 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="7505f-200">**After creating your VNets, you can add hello following settings:**</span></span>

* <span data-ttu-id="7505f-201">**주소 공간** – 추가 주소 공간이이 구성에 필요 하지 않습니다. 하지만 hello VNet을 만든 후 다른 주소 공간을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-201">**Address space** – Additional address space is not required for this configuration, but you can add additional address space after creating hello VNet.</span></span>

* <span data-ttu-id="7505f-202">**서브넷** – 추가 서브넷이이 구성에 필요 하지 않습니다. 하지만 다른 역할 인스턴스와 별도의 서브넷에 Vm toohave를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-202">**Subnets** – Additional subnets are not required for this configuration, but you might want toohave your VMs in a subnet that is separate from your other role instances.</span></span>

* <span data-ttu-id="7505f-203">**DNS 서버** – hello DNS 서버 이름 및 IP 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-203">**DNS servers** – Enter hello DNS server name and IP address.</span></span> <span data-ttu-id="7505f-204">이 설정은 DNS 서버를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-204">This setting does not create a DNS server.</span></span> <span data-ttu-id="7505f-205">이 가상 네트워크에 대 한 이름 확인을 위해 toouse 되도록 toospecify hello DNS 서버가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-205">It allows you toospecify hello DNS servers that you want toouse for name resolution for this virtual network.</span></span>

<span data-ttu-id="7505f-206">이 섹션에서는 hello 연결 유형, hello 로컬 사이트를 구성 하 고 hello 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-206">In this section, you configure hello connection type, hello local site, and create hello gateway.</span></span>

## <span data-ttu-id="7505f-207"><a name="localsite"></a>3 단계-hello 로컬 사이트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-207"><a name="localsite"></a>Step 3 - Configure hello local site</span></span>

<span data-ttu-id="7505f-208">Hello Vnet 간의 tooroute 트래픽이 하는 방법을 각 로컬 네트워크 사이트 toodetermine에 지정 된 hello 설정을 azure 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-208">Azure uses hello settings specified in each local network site toodetermine how tooroute traffic between hello VNets.</span></span> <span data-ttu-id="7505f-209">각 VNet toohello 각 로컬 네트워크에 대 한 트래픽을 tooroute 원하는 가리켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-209">Each VNet must point toohello respective local network that you want tooroute traffic to.</span></span> <span data-ttu-id="7505f-210">Toouse toorefer tooeach 로컬 네트워크 사이트를 원하는 hello 이름을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-210">You determine hello name you want toouse toorefer tooeach local network site.</span></span> <span data-ttu-id="7505f-211">것이 가장 좋은 toouse 다른 설명적인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-211">It's best toouse something descriptive.</span></span>

<span data-ttu-id="7505f-212">예를 들어 TestVNet1 tooa 로컬 네트워크 사이트를 만들면 'VNet4Local' 라는 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-212">For example, TestVNet1 connects tooa local network site that you create named 'VNet4Local'.</span></span> <span data-ttu-id="7505f-213">VNet4Local에 대 한 hello 설정을 TestVNet4에 대 한 hello 주소 접두사를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-213">hello settings for VNet4Local contain hello address prefixes for TestVNet4.</span></span>

<span data-ttu-id="7505f-214">hello 로컬 각 VNet은 다른 VNet을 hello에 대 한 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-214">hello local site for each VNet is hello other VNet.</span></span> <span data-ttu-id="7505f-215">다음 예에서는 값에는 hello에서는 구성에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-215">hello following example values are used for our configuration:</span></span>

| <span data-ttu-id="7505f-216">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="7505f-216">Virtual Network</span></span> | <span data-ttu-id="7505f-217">주소 공간</span><span class="sxs-lookup"><span data-stu-id="7505f-217">Address Space</span></span> | <span data-ttu-id="7505f-218">지역</span><span class="sxs-lookup"><span data-stu-id="7505f-218">Region</span></span> | <span data-ttu-id="7505f-219">Toolocal 네트워크 사이트에 연결</span><span class="sxs-lookup"><span data-stu-id="7505f-219">Connects toolocal network site</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7505f-220">TestVNet1</span><span class="sxs-lookup"><span data-stu-id="7505f-220">TestVNet1</span></span> |<span data-ttu-id="7505f-221">TestVNet1</span><span class="sxs-lookup"><span data-stu-id="7505f-221">TestVNet1</span></span><br><span data-ttu-id="7505f-222">(10.11.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="7505f-222">(10.11.0.0/16)</span></span><br><span data-ttu-id="7505f-223">(10.12.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="7505f-223">(10.12.0.0/16)</span></span> |<span data-ttu-id="7505f-224">미국 동부</span><span class="sxs-lookup"><span data-stu-id="7505f-224">East US</span></span> |<span data-ttu-id="7505f-225">VNet4Local</span><span class="sxs-lookup"><span data-stu-id="7505f-225">VNet4Local</span></span><br><span data-ttu-id="7505f-226">(10.41.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="7505f-226">(10.41.0.0/16)</span></span><br><span data-ttu-id="7505f-227">(10.42.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="7505f-227">(10.42.0.0/16)</span></span> |
| <span data-ttu-id="7505f-228">TestVNet4</span><span class="sxs-lookup"><span data-stu-id="7505f-228">TestVNet4</span></span> |<span data-ttu-id="7505f-229">TestVNet4</span><span class="sxs-lookup"><span data-stu-id="7505f-229">TestVNet4</span></span><br><span data-ttu-id="7505f-230">(10.41.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="7505f-230">(10.41.0.0/16)</span></span><br><span data-ttu-id="7505f-231">(10.42.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="7505f-231">(10.42.0.0/16)</span></span> |<span data-ttu-id="7505f-232">미국 서부</span><span class="sxs-lookup"><span data-stu-id="7505f-232">West US</span></span> |<span data-ttu-id="7505f-233">VNet1Local</span><span class="sxs-lookup"><span data-stu-id="7505f-233">VNet1Local</span></span><br><span data-ttu-id="7505f-234">(10.11.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="7505f-234">(10.11.0.0/16)</span></span><br><span data-ttu-id="7505f-235">(10.12.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="7505f-235">(10.12.0.0/16)</span></span> |

1. <span data-ttu-id="7505f-236">Hello Azure 포털에서에서 TestVNet1를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-236">Locate TestVNet1 in hello Azure portal.</span></span> <span data-ttu-id="7505f-237">Hello에 **VPN 연결** 섹션 hello 블레이드의 클릭 **게이트웨이**합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-237">In hello **VPN connections** section of hello blade, click **Gateway**.</span></span>

    ![게이트웨이 없음](./media/vpn-gateway-howto-vnet-vnet-portal-classic/nogateway.png)
2. <span data-ttu-id="7505f-239">Hello에 **새 VPN 연결** 페이지에서 **사이트 간**합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-239">On hello **New VPN Connection** page, select **Site-to-Site**.</span></span>
3. <span data-ttu-id="7505f-240">클릭 **로컬 사이트** tooopen 로컬 사이트 페이지 hello 및 hello 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-240">Click **Local site** tooopen hello Local site page and configure hello settings.</span></span>
4. <span data-ttu-id="7505f-241">Hello에 **로컬 사이트** 페이지에서 로컬 사이트 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-241">On hello **Local site** page, name your local site.</span></span> <span data-ttu-id="7505f-242">예제에서는 이름을 hello 로컬 사이트 'VNet4Local' 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-242">In our example, we name hello local site 'VNet4Local'.</span></span>
5. <span data-ttu-id="7505f-243">**VPN 게이트웨이 IP 주소**의 경우 IP 주소가 올바른 형식이기만 하면 무엇이든 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-243">For **VPN gateway IP address**, you can use any IP address that you want, as long as it's in a valid format.</span></span> <span data-ttu-id="7505f-244">일반적으로 VPN 장치에 대 한 hello 실제 외부 IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-244">Typically, you’d use hello actual external IP address for a VPN device.</span></span> <span data-ttu-id="7505f-245">하지만 클래식 VNet 대 VNet 구성의 경우 toohello 게이트웨이 VNet에 대 한 할당 된 hello 공용 IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-245">But, for a classic VNet-to-VNet configuration, you use hello public IP address that is assigned toohello gateway for your VNet.</span></span> <span data-ttu-id="7505f-246">아직 hello 가상 네트워크 게이트웨이 만든 있다고 가정 자리 표시자로 모든 유효한 공용 IP 주소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-246">Given that you’ve not yet created hello virtual network gateway, you specify any valid public IP address as a placeholder.</span></span><br><span data-ttu-id="7505f-247">이 구성에서는 선택 사항이 아니므로 이 항목은 비워두면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-247">Don't leave this blank - it's not optional for this configuration.</span></span> <span data-ttu-id="7505f-248">이후 단계에서이 설정으로 다시 이동 하 고 Azure에서 생성 되 면 hello 해당 가상 네트워크 게이트웨이 IP 주소와 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-248">In a later step, you go back into these settings and configure them with hello corresponding virtual network gateway IP addresses once Azure generates it.</span></span>
6. <span data-ttu-id="7505f-249">에 대 한 **클라이언트 주소 공간**, 다른 VNet의 hello hello 주소 공간을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-249">For **Client Address Space**, use hello address space of hello other VNet.</span></span> <span data-ttu-id="7505f-250">Tooyour 계획 예를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7505f-250">Refer tooyour planning example.</span></span> <span data-ttu-id="7505f-251">클릭 **확인** toosave 설정 및 반환 백 toohello **새 VPN 연결** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-251">Click **OK** toosave your settings and return back toohello **New VPN Connection** blade.</span></span>

    ![로컬 사이트](./media/vpn-gateway-howto-vnet-vnet-portal-classic/localsite.png)

## <span data-ttu-id="7505f-253"><a name="gw"></a>4 단계-hello 가상 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="7505f-253"><a name="gw"></a>Step 4 - Create hello virtual network gateway</span></span>

<span data-ttu-id="7505f-254">각 가상 네트워크에는 가상 네트워크 게이트웨이가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-254">Each virtual network must have a virtual network gateway.</span></span> <span data-ttu-id="7505f-255">hello 가상 네트워크 게이트웨이 라우팅하고 트래픽을 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-255">hello virtual network gateway routes and encrypts traffic.</span></span>

1. <span data-ttu-id="7505f-256">Hello에 **새 VPN 연결** 블레이드, 확인란 선택 hello **게이트웨이 즉시 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-256">On hello **New VPN Connection** blade, select hello checkbox **Create gateway immediately**.</span></span>
2. <span data-ttu-id="7505f-257">**서브넷, 크기 및 라우팅 유형**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-257">Click **Subnet, size and routing type**.</span></span> <span data-ttu-id="7505f-258">Hello에 **게이트웨이 구성** 블레이드에서 클릭 **서브넷**합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-258">On hello **Gateway configuration** blade, click **Subnet**.</span></span>
3. <span data-ttu-id="7505f-259">hello 게이트웨이 서브넷 이름이 자동으로 채워집니다 'GatewaySubnet' hello 필요한 이름을 가진 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-259">hello gateway subnet name is filled in automatically with hello required name 'GatewaySubnet'.</span></span> <span data-ttu-id="7505f-260">hello **주소 범위** toohello VPN 게이트웨이 서비스에 할당 되는 hello IP 주소가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-260">hello **Address range** contains hello IP addresses that are allocated toohello VPN gateway services.</span></span> <span data-ttu-id="7505f-261">일부 구성은/27 또는 / 28/29, 하지만 최상의 toouse의 게이트웨이 서브넷을 허용 tooaccommodate 이후 구성을 hello 게이트웨이 서비스에 대 한 더 많은 IP 주소를 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-261">Some configurations allow a gateway subnet of /29, but it's best toouse a /28 or /27 tooaccommodate future configurations that may require more IP addresses for hello gateway services.</span></span> <span data-ttu-id="7505f-262">여기의 예제에서는 10.11.1.0/27을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-262">In our example settings, we use 10.11.1.0/27.</span></span> <span data-ttu-id="7505f-263">Hello 주소 공간을 조정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-263">Adjust hello address space, then click **OK**.</span></span>
4. <span data-ttu-id="7505f-264">Hello 구성 **게이트웨이 크기**합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-264">Configure hello **Gateway Size**.</span></span> <span data-ttu-id="7505f-265">이 설정은 참조 toohello [게이트웨이 SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku)합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-265">This setting refers toohello [Gateway SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>
5. <span data-ttu-id="7505f-266">Hello 구성 **라우팅 유형**합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-266">Configure hello **Routing Type**.</span></span> <span data-ttu-id="7505f-267">이 구성에 대해 라우팅 유형을 hello **동적**합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-267">hello routing type for this configuration must be **Dynamic**.</span></span> <span data-ttu-id="7505f-268">Hello 게이트웨이 종료 하 고 새로 만들 하지 않으면 hello 라우팅 유형을 나중에 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-268">You can't change hello routing type later unless you tear down hello gateway and create a new one.</span></span>
6. <span data-ttu-id="7505f-269">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-269">Click **OK**.</span></span>
7. <span data-ttu-id="7505f-270">Hello에 **새 VPN 연결** 블레이드에서 클릭 **확인** toobegin hello 가상 네트워크 게이트웨이 만들기.</span><span class="sxs-lookup"><span data-stu-id="7505f-270">On hello **New VPN Connection** blade, click **OK** toobegin creating hello virtual network gateway.</span></span> <span data-ttu-id="7505f-271">게이트웨이 만들기 45 분에 따라 이상 hello 선택한 게이트웨이 SKU 종종 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-271">Creating a gateway can often take 45 minutes or more, depending on hello selected gateway SKU.</span></span>

## <span data-ttu-id="7505f-272"><a name="vnet4settings"></a>5단계 - TestVNet4 설정 구성</span><span class="sxs-lookup"><span data-stu-id="7505f-272"><a name="vnet4settings"></a>Step 5 - Configure TestVNet4 settings</span></span>

<span data-ttu-id="7505f-273"> ° ט hello 너무[로컬 사이트를 만들](#localsite) 및 [hello 가상 네트워크 게이트웨이 만들기](#gw) tooconfigure TestVNet4, 필요한 경우 hello 값으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-273">Repeat hello steps too[Create a local site](#localsite) and [Create hello virtual network gateway](#gw) tooconfigure TestVNet4, substituting hello values when necessary.</span></span> <span data-ttu-id="7505f-274">이렇게 하는 연습으로, 하는 경우 사용 하 여 hello [예제 값](#vnetvalues)합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-274">If you are doing this as an exercise, use hello [Example values](#vnetvalues).</span></span>

## <span data-ttu-id="7505f-275"><a name="updatelocal"></a>6 단계-hello 로컬 사이트 업데이트</span><span class="sxs-lookup"><span data-stu-id="7505f-275"><a name="updatelocal"></a>Step 6 - Update hello local sites</span></span>

<span data-ttu-id="7505f-276">Hello 로컬 사이트를 조정 해야 두 Vnet에 대 한 가상 네트워크 게이트웨이 만든 후 **VPN 게이트웨이 IP 주소** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-276">After your virtual network gateways have been created for both VNets, you must adjust hello local sites **VPN gateway IP address** values.</span></span>

|<span data-ttu-id="7505f-277">VNet 이름</span><span class="sxs-lookup"><span data-stu-id="7505f-277">VNet name</span></span>|<span data-ttu-id="7505f-278">연결된 사이트</span><span class="sxs-lookup"><span data-stu-id="7505f-278">Connected site</span></span>|<span data-ttu-id="7505f-279">게이트웨이 IP 주소</span><span class="sxs-lookup"><span data-stu-id="7505f-279">Gateway IP address</span></span>|
|:--- |:--- |:--- |
|<span data-ttu-id="7505f-280">TestVNet1</span><span class="sxs-lookup"><span data-stu-id="7505f-280">TestVNet1</span></span>|<span data-ttu-id="7505f-281">VNet4Local</span><span class="sxs-lookup"><span data-stu-id="7505f-281">VNet4Local</span></span>|<span data-ttu-id="7505f-282">TestVNet4의 VPN 게이트웨이 IP 주소</span><span class="sxs-lookup"><span data-stu-id="7505f-282">VPN gateway IP address for TestVNet4</span></span>|
|<span data-ttu-id="7505f-283">TestVNet4</span><span class="sxs-lookup"><span data-stu-id="7505f-283">TestVNet4</span></span>|<span data-ttu-id="7505f-284">VNet1Local</span><span class="sxs-lookup"><span data-stu-id="7505f-284">VNet1Local</span></span>|<span data-ttu-id="7505f-285">TestVNet1의 VPN 게이트웨이 IP 주소</span><span class="sxs-lookup"><span data-stu-id="7505f-285">VPN gateway IP address for TestVNet1</span></span>|

### <a name="part-1---get-hello-virtual-network-gateway-public-ip-address"></a><span data-ttu-id="7505f-286">-1 부 Get hello 가상 네트워크 게이트웨이 공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="7505f-286">Part 1 - Get hello virtual network gateway public IP address</span></span>

1. <span data-ttu-id="7505f-287">Hello Azure 포털에서에서 가상 네트워크를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-287">Locate your virtual network in hello Azure portal.</span></span>
2. <span data-ttu-id="7505f-288">Tooopen hello VNet 클릭 **개요** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-288">Click tooopen hello VNet **Overview** blade.</span></span> <span data-ttu-id="7505f-289">Hello 블레이드에서 **VPN 연결**, 가상 네트워크 게이트웨이에 대 한 hello IP 주소를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-289">On hello blade, in **VPN connections**, you can view hello IP address for your virtual network gateway.</span></span>

  ![공용 IP](./media/vpn-gateway-howto-vnet-vnet-portal-classic/publicIP.png)
3. <span data-ttu-id="7505f-291">Hello IP 주소를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-291">Copy hello IP address.</span></span> <span data-ttu-id="7505f-292">Hello 다음 섹션에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-292">You will use it in hello next section.</span></span>
4. <span data-ttu-id="7505f-293">TestVNet4에 대해 이들 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-293">Repeat these steps for TestVNet4</span></span>

### <a name="part-2---modify-hello-local-sites"></a><span data-ttu-id="7505f-294">2 부-hello 로컬 사이트 수정</span><span class="sxs-lookup"><span data-stu-id="7505f-294">Part 2 - Modify hello local sites</span></span>

1. <span data-ttu-id="7505f-295">Hello Azure 포털에서에서 가상 네트워크를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-295">Locate your virtual network in hello Azure portal.</span></span>
2. <span data-ttu-id="7505f-296">Hello VNet에 **개요** 블레이드에서 hello 로컬 사이트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-296">On hello VNet **Overview** blade, click hello local site.</span></span>

  ![생성된 로컬 사이트](./media/vpn-gateway-howto-vnet-vnet-portal-classic/local.png)
3. <span data-ttu-id="7505f-298">Hello에 **사이트 간 VPN 연결** 블레이드에서 원하는 toomodify hello 로컬 사이트의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-298">On hello **Site-to-Site VPN Connections** blade, click hello name of hello local site that you want toomodify.</span></span>

  ![로컬 사이트 열기](./media/vpn-gateway-howto-vnet-vnet-portal-classic/openlocal.png)
4. <span data-ttu-id="7505f-300">Hello 클릭 **로컬 사이트** toomodify 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-300">Click hello **Local site** that you want toomodify.</span></span>

  ![사이트 수정](./media/vpn-gateway-howto-vnet-vnet-portal-classic/connections.png)
5. <span data-ttu-id="7505f-302">업데이트 hello **VPN 게이트웨이 IP 주소** 클릭 **확인** toosave hello 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-302">Update hello **VPN gateway IP address** and click **OK** toosave hello settings.</span></span>

  ![게이트웨이 IP](./media/vpn-gateway-howto-vnet-vnet-portal-classic/gwupdate.png)
6. <span data-ttu-id="7505f-304">다른 블레이드를 닫고 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-304">Close hello other blades.</span></span>
7. <span data-ttu-id="7505f-305">TestVNet4에 대해 이들 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-305">Repeat these steps for TestVNet4.</span></span>

## <span data-ttu-id="7505f-306"><a name="getvalues"></a>단계 7-hello 네트워크 구성 파일에서 값 검색</span><span class="sxs-lookup"><span data-stu-id="7505f-306"><a name="getvalues"></a>Step 7 - Retrieve values from hello network configuration file</span></span>

<span data-ttu-id="7505f-307">Hello Azure 포털에서에서 기존 Vnet을 만들 때 볼 수 있는 hello 이름은 PowerShell을 사용 하는 hello 전체 이름이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-307">When you create classic VNets in hello Azure portal, hello name that you view is not hello full name that you use for PowerShell.</span></span> <span data-ttu-id="7505f-308">예를 들어 라는 toobe 나타나는 VNet **TestVNet1** hello 포털에 있을 수는 훨씬 더 긴 이름을 hello 네트워크 구성 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-308">For example, a VNet that appears toobe named **TestVNet1** in hello portal, may have a much longer name in hello network configuration file.</span></span> <span data-ttu-id="7505f-309">hello 이름이 같을 수 있습니다: **그룹 ClassicRG TestVNet1**합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-309">hello name might look something like: **Group ClassicRG TestVNet1**.</span></span> <span data-ttu-id="7505f-310">사용자 연결을 만드는 경우는 hello 네트워크 구성 파일에서 볼 수 있는 중요 한 toouse hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-310">When you create your connections, it's important toouse hello values that you see in hello network configuration file.</span></span>

<span data-ttu-id="7505f-311">단계를 수행 하는 hello, tooyour Azure 계정을 연결 하는 데 하 고 다운로드 및 hello 네트워크 구성 파일 tooobtain hello 있는 값이 보기는 연결에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-311">In hello following steps, you will connect tooyour Azure account and download and view hello network configuration file tooobtain hello values that are required for your connections.</span></span>

1. <span data-ttu-id="7505f-312">다운로드 하 여 hello hello Azure 서비스 관리 (SM) PowerShell cmdlet의 최신 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-312">Download and install hello latest version of hello Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="7505f-313">자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-313">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

2. <span data-ttu-id="7505f-314">관리자 권한으로 PowerShell 콘솔을 열고 및 tooyour 계정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-314">Open your PowerShell console with elevated rights and connect tooyour account.</span></span> <span data-ttu-id="7505f-315">다음 예제에서는 toohelp 연결한 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-315">Use hello following example toohelp you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="7505f-316">Hello 계정에 대 한 hello 구독을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-316">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="7505f-317">둘 이상의 구독을 보유 하는 경우 toouse hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-317">If you have more than one subscription, select hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
  ```

  <span data-ttu-id="7505f-318">를 사용 하 여 다음 cmdlet tooadd hello Azure 구독 tooPowerShell hello 클래식 배포 모델에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-318">Next, use hello following cmdlet tooadd your Azure subscription tooPowerShell for hello classic deployment model.</span></span>

  ```powershell
  Add-AzureAccount
  ```
3. <span data-ttu-id="7505f-319">내보낸 hello 네트워크 구성 파일을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-319">Export and view hello network configuration file.</span></span> <span data-ttu-id="7505f-320">컴퓨터에 디렉터리를 만들고 hello 네트워크 구성 파일 toohello 디렉터리를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-320">Create a directory on your computer and then export hello network configuration file toohello directory.</span></span> <span data-ttu-id="7505f-321">이 예제에서는 hello 네트워크 구성 파일을 내보내려면 너무**C:\AzureNet**합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-321">In this example, hello network configuration file is exported too**C:\AzureNet**.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
4. <span data-ttu-id="7505f-322">표시 되는 텍스트 편집기 및 보기 hello 이름이 Vnet 및 사이트에 대 한 hello 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-322">Open hello file with a text editor and view hello names for your VNets and sites.</span></span> <span data-ttu-id="7505f-323">이러한 연결을 만들 때 사용 하는 hello 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-323">These will be hello name you use when you create your connections.</span></span><br><span data-ttu-id="7505f-324">VNet 이름은 **VirtualNetworkSite name =**으로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-324">VNet names are listed as **VirtualNetworkSite name =**</span></span><br><span data-ttu-id="7505f-325">사이트 이름은 **LocalNetworkSiteRef name =**으로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-325">Site names are listed as **LocalNetworkSiteRef name =**</span></span>

## <span data-ttu-id="7505f-326"><a name="createconnections"></a>8 단계-hello VPN 게이트웨이 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="7505f-326"><a name="createconnections"></a>Step 8 - Create hello VPN gateway connections</span></span>

<span data-ttu-id="7505f-327">Hello 위의 모든 단계를 모두 완료 되 면 hello IPsec/IKE 사전 공유 키를 설정할 수 있으며 hello 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-327">When all hello previous steps have been completed, you can set hello IPsec/IKE pre-shared keys and create hello connection.</span></span> <span data-ttu-id="7505f-328">이번 단계에서는 PowerShell을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-328">This set of steps uses PowerShell.</span></span> <span data-ttu-id="7505f-329">VNet 대 VNet 연결 hello 클래식 배포 모델에 대 한 hello Azure 포털에서에서 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-329">VNet-to-VNet connections for hello classic deployment model cannot be configured in hello Azure portal.</span></span>

<span data-ttu-id="7505f-330">Hello 예에서 hello 공유 키에 정확 하 게 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-330">In hello examples, notice that hello shared key is exactly hello same.</span></span> <span data-ttu-id="7505f-331">공유 키 hello 항상 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-331">hello shared key must always match.</span></span> <span data-ttu-id="7505f-332">있는지 tooreplace hello Vnet 및 로컬 네트워크 사이트에 대 한 정확한 이름으로 이러한 예에서 hello 값 수입니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-332">Be sure tooreplace hello values in these examples with hello exact names for your VNets and Local Network Sites.</span></span>

1. <span data-ttu-id="7505f-333">Hello TestVNet1 tooTestVNet4 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-333">Create hello TestVNet1 tooTestVNet4 connection.</span></span>

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet1' `
  -LocalNetworkSiteName '17BE5E2C_VNet4Local' -SharedKey A1b2C3D4
  ```
2. <span data-ttu-id="7505f-334">Hello TestVNet4 tooTestVNet1 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-334">Create hello TestVNet4 tooTestVNet1 connection.</span></span>

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet4' `
  -LocalNetworkSiteName 'F7F7BFC7_VNet1Local' -SharedKey A1b2C3D4
  ```
3. <span data-ttu-id="7505f-335">Hello 연결 tooinitialize 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-335">Wait for hello connections tooinitialize.</span></span> <span data-ttu-id="7505f-336">Hello 게이트웨이 초기화 되 면 hello 상태는 '성공'입니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-336">Once hello gateway has initialized, hello Status is 'Successful'.</span></span>

  ```
  Error          :
  HttpStatusCode : OK
  Id             :
  Status         : Successful
  RequestId      :
  StatusCode     : OK
  ```

## <span data-ttu-id="7505f-337"><a name="faq"></a>클래식 VNet에 대한 VNet-VNet 고려 사항</span><span class="sxs-lookup"><span data-stu-id="7505f-337"><a name="faq"></a>VNet-to-VNet considerations for classic VNets</span></span>
* <span data-ttu-id="7505f-338">hello에 hello 가상 네트워크 수 동일 하거나 다른 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-338">hello virtual networks can be in hello same or different subscriptions.</span></span>
* <span data-ttu-id="7505f-339">hello에 hello 가상 네트워크 수 같거나 다른 Azure 지역 (위치).</span><span class="sxs-lookup"><span data-stu-id="7505f-339">hello virtual networks can be in hello same or different Azure regions (locations).</span></span>
* <span data-ttu-id="7505f-340">클라우드 서비스 또는 부하 분산 끝점은 연결되어 있더라도 여러 가상 네트워크에 분산될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-340">A cloud service or a load balancing endpoint can't span across virtual networks, even if they are connected together.</span></span>
* <span data-ttu-id="7505f-341">여러 가상 네트워크를 연결할 때 VPN 장치는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-341">Connecting multiple virtual networks together doesn't require any VPN devices.</span></span>
* <span data-ttu-id="7505f-342">VNet 간 연결은 Azure 가상 네트워크 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-342">VNet-to-VNet supports connecting Azure Virtual Networks.</span></span> <span data-ttu-id="7505f-343">가상 컴퓨터 연결을 지원 하지 않습니다 또는 tooa 가상 네트워크를 배포 하지 않은 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-343">It does not support connecting virtual machines or cloud services that are not deployed tooa virtual network.</span></span>
* <span data-ttu-id="7505f-344">VNet-VNet을 위해서는 동적 라우팅 게이트웨이가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-344">VNet-to-VNet requires dynamic routing gateways.</span></span> <span data-ttu-id="7505f-345">Azure 정적 라우팅 게이트웨이는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-345">Azure static routing gateways are not supported.</span></span>
* <span data-ttu-id="7505f-346">가상 네트워크 연결을 다중 사이트 VPN과 동시에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-346">Virtual network connectivity can be used simultaneously with multi-site VPNs.</span></span> <span data-ttu-id="7505f-347">10 개의 VPN 터널이 다른 가상 네트워크 또는 온-프레미스 사이트 tooeither를 연결할 가상 네트워크 VPN 게이트웨이 최대가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-347">There is a maximum of 10 VPN tunnels for a virtual network VPN gateway connecting tooeither other virtual networks, or on-premises sites.</span></span>
* <span data-ttu-id="7505f-348">hello 주소 공간 hello 가상 네트워크와 온-프레미스 로컬 네트워크 사이트는 겹치지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-348">hello address spaces of hello virtual networks and on-premises local network sites must not overlap.</span></span> <span data-ttu-id="7505f-349">겹치는 주소 공간의 가상 네트워크 또는 업로드 netcfg 구성 파일 toofail hello 작성을 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-349">Overlapping address spaces will cause hello creation of virtual networks or uploading netcfg configuration files toofail.</span></span>
* <span data-ttu-id="7505f-350">가상 네트워크 한 쌍 간의 중복 터널은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-350">Redundant tunnels between a pair of virtual networks are not supported.</span></span>
* <span data-ttu-id="7505f-351">VPN 터널 hello P2S Vpn을 포함 하 여 VNet에 대 한 모든 hello VPN 게이트웨이에 대 한 사용 가능한 대역폭 hello를 공유 하며 Azure에서 동일한 VPN 게이트웨이 작동 시간 SLA hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-351">All VPN tunnels for hello VNet, including P2S VPNs, share hello available bandwidth for hello VPN gateway, and hello same VPN gateway uptime SLA in Azure.</span></span>
* <span data-ttu-id="7505f-352">VNet 대 VNet 트래픽이 hello Azure backbone 통과 합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-352">VNet-to-VNet traffic travels across hello Azure backbone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7505f-353">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7505f-353">Next steps</span></span>
<span data-ttu-id="7505f-354">연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7505f-354">Verify your connections.</span></span> <span data-ttu-id="7505f-355">[VPN Gateway 연결 확인](vpn-gateway-verify-connection-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7505f-355">See [Verify a VPN Gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>
