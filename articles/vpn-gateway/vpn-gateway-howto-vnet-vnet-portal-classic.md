---
title: "VNet: 클래식: Azure Portal 사이의 연결 만들기 | Microsoft Docs"
description: "PowerShell 및 Azure 클래식 포털을 사용하여 Azure 가상 네트워크를 함께 연결하는 방법에 대해 설명합니다."
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
ms.openlocfilehash: 77097d59077cd8e199acdb5dc0d8427369565eea
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-a-vnet-to-vnet-connection-classic"></a><span data-ttu-id="b750e-103">VNet-VNet 연결(클래식) 구성</span><span class="sxs-lookup"><span data-stu-id="b750e-103">Configure a VNet-to-VNet connection (classic)</span></span>

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

<span data-ttu-id="b750e-104">이 문서에서는 가상 네트워크 간에 VPN Gateway 연결을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-104">This article shows you how to create a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="b750e-105">가상 네트워크는 같은 또는 다른 구독의 같은 지역에 있을 수도 있고 다른 지역에 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-105">The virtual networks can be in the same or different regions, and from the same or different subscriptions.</span></span> <span data-ttu-id="b750e-106">이 문서의 단계는 클래식 배포 모델 및 Azure Portal에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-106">The steps in this article apply to the classic deployment model and the Azure portal.</span></span> <span data-ttu-id="b750e-107">다른 배포 도구 또는 배포 모델을 사용하는 경우 다음 목록에서 별도의 옵션을 선택하여 이 구성을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b750e-108">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b750e-108">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="b750e-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b750e-109">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="b750e-110">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b750e-110">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="b750e-111">Azure Portal(클래식)</span><span class="sxs-lookup"><span data-stu-id="b750e-111">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="b750e-112">다양한 배포 모델 간 연결 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b750e-112">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="b750e-113">다양한 배포 모델 간 연결 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="b750e-113">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![VNet 간 연결 다이어그램](./media/vpn-gateway-howto-vnet-vnet-portal-classic/v2vclassic.png)

## <a name="about-vnet-to-vnet-connections"></a><span data-ttu-id="b750e-115">VNet 간 연결 정보</span><span class="sxs-lookup"><span data-stu-id="b750e-115">About VNet-to-VNet connections</span></span>

<span data-ttu-id="b750e-116">VPN 게이트웨이를 사용하여 클래식 배포 모델에서 가상 네트워크를 다른 가상 네트워크(VNet-VNet)에 연결하는 것은 가상 네트워크를 온-프레미스 사이트 위치에 연결하는 것과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-116">Connecting a virtual network to another virtual network (VNet-to-VNet) in the classic deployment model using a VPN gateway is similar to connecting a virtual network to an on-premises site location.</span></span> <span data-ttu-id="b750e-117">두 연결 유형 모두 VPN 게이트웨이를 사용하여 IPsec/IKE를 통한 보안 터널을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-117">Both connectivity types use a VPN gateway to provide a secure tunnel using IPsec/IKE.</span></span>

<span data-ttu-id="b750e-118">연결하는 VNet은 서로 다른 구독 및 지역에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-118">The VNets you connect can be in different subscriptions and different regions.</span></span> <span data-ttu-id="b750e-119">VNet 간 통신을 다중 사이트 구성과 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-119">You can combine VNet to VNet communication with multi-site configurations.</span></span> <span data-ttu-id="b750e-120">이렇게 하면 프레미스 간 연결을 가상 네트워크 간 연결과 결합하는 네트워크 토폴로지를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-120">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity.</span></span>

![VNet 간 연결](./media/vpn-gateway-howto-vnet-vnet-portal-classic/aboutconnections.png)

### <span data-ttu-id="b750e-122"><a name="why"></a>가상 네트워크에 연결하는 이유</span><span class="sxs-lookup"><span data-stu-id="b750e-122"><a name="why"></a>Why connect virtual networks?</span></span>

<span data-ttu-id="b750e-123">다음과 같은 이유로 가상 네트워크에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-123">You may want to connect virtual networks for the following reasons:</span></span>

* <span data-ttu-id="b750e-124">**지역 간 지리적 중복 및 지리적 상태**</span><span class="sxs-lookup"><span data-stu-id="b750e-124">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="b750e-125">인터넷 연결 끝점으로 이동하지 않고도 보안 연결을 통해 지역에서 복제 또는 동기화를 직접 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-125">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="b750e-126">Azure 부하 분산 장치 및 Microsoft 또는 타사 클러스터링 기술을 사용하여 여러 Azure 지역 간의 지리적 중복을 통해 워크로드의 가용성을 높게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-126">With Azure Load Balancer and Microsoft or third-party clustering technology, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="b750e-127">이러한 작업의 한 가지 주요 예는 여러 Azure 지역에 분산된 가용성 그룹을 사용하여 SQL AlwaysOn을 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-127">One important example is to set up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="b750e-128">**분리 경계가 뚜렷한 지역별 다중 계층 응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="b750e-128">**Regional multi-tier applications with strong isolation boundary**</span></span>

  * <span data-ttu-id="b750e-129">같은 지역 내에서 뚜렷한 경계를 적용해 여러 VNet이 함께 연결된 다중 계층 응용 프로그램을 설정하고 계층 간 통신을 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-129">Within the same region, you can set up multi-tier applications with multiple VNets connected together with strong isolation and secure inter-tier communication.</span></span>
* <span data-ttu-id="b750e-130">**Azure의 구독 간/조직 간 통신**</span><span class="sxs-lookup"><span data-stu-id="b750e-130">**Cross subscription, inter-organization communication in Azure**</span></span>

  * <span data-ttu-id="b750e-131">Azure 구독이 여러 개인 경우 이제 가상 네트워크 간에 여러 구독의 작업을 안전하게 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-131">If you have multiple Azure subscriptions, you can connect workloads from different subscriptions together securely between virtual networks.</span></span>
  * <span data-ttu-id="b750e-132">엔터프라이즈 또는 서비스 공급자의 경우 이제 Azure 내의 보안 VPN 기술을 사용하여 조직 간 통신을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-132">For enterprises or service providers, you can enable cross-organization communication with secure VPN technology within Azure.</span></span>

<span data-ttu-id="b750e-133">VNet 간 연결에 대한 자세한 내용은 이 문서의 끝에 있는 [VNet 간 고려 사항](#faq)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b750e-133">For more information about VNet-to-VNet connections, see [VNet-to-VNet considerations](#faq) at the end of this article.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="b750e-134">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="b750e-134">Before you begin</span></span>

<span data-ttu-id="b750e-135">이 연습을 시작하기 전에 최신 버전의 Azure SM(Service Management) PowerShell cmdlet을 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-135">Before beginning this exercise, download and install the latest version of the Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="b750e-136">자세한 내용은 [Azure PowerShell 설치 및 구성하는 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b750e-136">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="b750e-137">대부분의 단계에서 포털을 사용하지만 PowerShell을 사용하여 VNet 간의 연결을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-137">We use the portal for most of the steps, but you must use PowerShell to create the connections between the VNets.</span></span> <span data-ttu-id="b750e-138">Azure Portal을 사용하여 연결을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-138">You can't create the connections using the Azure portal.</span></span>

## <span data-ttu-id="b750e-139"><a name="plan"></a>1단계 - IP 주소 범위 계획</span><span class="sxs-lookup"><span data-stu-id="b750e-139"><a name="plan"></a>Step 1 - Plan your IP address ranges</span></span>

<span data-ttu-id="b750e-140">가상 네트워크를 구성하는 데 사용할 범위를 결정하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-140">It’s important to decide the ranges that you’ll use to configure your virtual networks.</span></span> <span data-ttu-id="b750e-141">이 구성의 경우 VNet 범위가 서로 간에 또는 연결된 로컬 네트워크와 겹치지 않는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-141">For this configuration, you must make sure that none of your VNet ranges overlap with each other, or with any of the local networks that they connect to.</span></span>

<span data-ttu-id="b750e-142">다음 테이블에는 VNet을 정의하는 방법의 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-142">The following table shows an example of how to define your VNets.</span></span> <span data-ttu-id="b750e-143">범위는 지침으로만 참고하고,</span><span class="sxs-lookup"><span data-stu-id="b750e-143">Use the ranges as a guideline only.</span></span> <span data-ttu-id="b750e-144">실제 가상 네트워크에 사용할 범위를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-144">Write down the ranges for your virtual networks.</span></span> <span data-ttu-id="b750e-145">이 정보는 이후 단계에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-145">You need this information for later steps.</span></span>

<span data-ttu-id="b750e-146">**예제**</span><span class="sxs-lookup"><span data-stu-id="b750e-146">**Example**</span></span>

| <span data-ttu-id="b750e-147">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="b750e-147">Virtual Network</span></span> | <span data-ttu-id="b750e-148">주소 공간</span><span class="sxs-lookup"><span data-stu-id="b750e-148">Address Space</span></span> | <span data-ttu-id="b750e-149">지역</span><span class="sxs-lookup"><span data-stu-id="b750e-149">Region</span></span> | <span data-ttu-id="b750e-150">로컬 네트워크 사이트에 연결</span><span class="sxs-lookup"><span data-stu-id="b750e-150">Connects to local network site</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b750e-151">TestVNet1</span><span class="sxs-lookup"><span data-stu-id="b750e-151">TestVNet1</span></span> |<span data-ttu-id="b750e-152">TestVNet1</span><span class="sxs-lookup"><span data-stu-id="b750e-152">TestVNet1</span></span><br><span data-ttu-id="b750e-153">(10.11.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="b750e-153">(10.11.0.0/16)</span></span><br><span data-ttu-id="b750e-154">(10.12.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="b750e-154">(10.12.0.0/16)</span></span> |<span data-ttu-id="b750e-155">미국 동부</span><span class="sxs-lookup"><span data-stu-id="b750e-155">East US</span></span> |<span data-ttu-id="b750e-156">VNet4Local</span><span class="sxs-lookup"><span data-stu-id="b750e-156">VNet4Local</span></span><br><span data-ttu-id="b750e-157">(10.41.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="b750e-157">(10.41.0.0/16)</span></span><br><span data-ttu-id="b750e-158">(10.42.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="b750e-158">(10.42.0.0/16)</span></span> |
| <span data-ttu-id="b750e-159">TestVNet4</span><span class="sxs-lookup"><span data-stu-id="b750e-159">TestVNet4</span></span> |<span data-ttu-id="b750e-160">TestVNet4</span><span class="sxs-lookup"><span data-stu-id="b750e-160">TestVNet4</span></span><br><span data-ttu-id="b750e-161">(10.41.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="b750e-161">(10.41.0.0/16)</span></span><br><span data-ttu-id="b750e-162">(10.42.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="b750e-162">(10.42.0.0/16)</span></span> |<span data-ttu-id="b750e-163">미국 서부</span><span class="sxs-lookup"><span data-stu-id="b750e-163">West US</span></span> |<span data-ttu-id="b750e-164">VNet1Local</span><span class="sxs-lookup"><span data-stu-id="b750e-164">VNet1Local</span></span><br><span data-ttu-id="b750e-165">(10.11.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="b750e-165">(10.11.0.0/16)</span></span><br><span data-ttu-id="b750e-166">(10.12.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="b750e-166">(10.12.0.0/16)</span></span> |

## <span data-ttu-id="b750e-167"><a name="vnetvalues"></a>2단계 - 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="b750e-167"><a name="vnetvalues"></a>Step 2 - Create the virtual networks</span></span>

<span data-ttu-id="b750e-168">[Azure Portal](https://portal.azure.com)에서 두 개의 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-168">Create two virtual networks in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b750e-169">클래식 가상 네트워크를 만드는 단계는 [클래식 가상 네트워크 만들기](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b750e-169">For the steps to create classic virtual networks, see [Create a classic virtual network](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span></span> 

<span data-ttu-id="b750e-170">포털을 사용하여 클래식 가상 네트워크를 만들 때 다음 단계를 사용하여 가상 네트워크 블레이드로 이동해야 합니다. 그렇지 않으면 가상 네트워크를 만드는 옵션이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-170">When using the portal to create a classic virtual network, you must navigate to the virtual network blade by using the following steps, otherwise the option to create a classic virtual network does not appear:</span></span>

1. <span data-ttu-id="b750e-171">'+'를 클릭하여 '새로 만들기' 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-171">Click the '+' to open the 'New' blade.</span></span>
2. <span data-ttu-id="b750e-172">‘Marketplace 검색’ 필드에 ‘가상 네트워크’를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-172">In the 'Search the marketplace' field, type 'Virtual Network'.</span></span> <span data-ttu-id="b750e-173">대신, 네트워킹 -> 가상 네트워크를 선택한 경우 클래식 VNet을 만드는 옵션이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-173">If you instead, select Networking -> Virtual Network, you will not get the option to create a classic VNet.</span></span>
3. <span data-ttu-id="b750e-174">반환된 목록에서 ‘가상 네트워크’를 찾아서 클릭하여 가상 네트워크 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-174">Locate 'Virtual Network' from the returned list and click it to open the Virtual Network blade.</span></span> 
4. <span data-ttu-id="b750e-175">가상 네트워크 블레이드에서 '클래식'을 선택하여 클래식 VNet을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-175">On the virtual network blade, select 'Classic' to create a classic VNet.</span></span> 

<span data-ttu-id="b750e-176">이 문서를 연습으로 사용하는 경우 다음 예제 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-176">If you are using this article as an exercise, you can use the following example values:</span></span>

<span data-ttu-id="b750e-177">**TestVNet1에 대한 값**</span><span class="sxs-lookup"><span data-stu-id="b750e-177">**Values for TestVNet1**</span></span>

<span data-ttu-id="b750e-178">이름: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="b750e-178">Name: TestVNet1</span></span><br>
<span data-ttu-id="b750e-179">주소 공간: 10.11.0.0/16, 10.12.0.0/16(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="b750e-179">Address space: 10.11.0.0/16, 10.12.0.0/16 (optional)</span></span><br>
<span data-ttu-id="b750e-180">서브넷 이름: 기본값</span><span class="sxs-lookup"><span data-stu-id="b750e-180">Subnet name: default</span></span><br>
<span data-ttu-id="b750e-181">서브넷 주소 범위: 10.11.0.1/24</span><span class="sxs-lookup"><span data-stu-id="b750e-181">Subnet address range: 10.11.0.1/24</span></span><br>
<span data-ttu-id="b750e-182">리소스 그룹: ClassicRG</span><span class="sxs-lookup"><span data-stu-id="b750e-182">Resource group: ClassicRG</span></span><br>
<span data-ttu-id="b750e-183">위치: 미국 동부</span><span class="sxs-lookup"><span data-stu-id="b750e-183">Location: East US</span></span><br>
<span data-ttu-id="b750e-184">게이트웨이 서브넷: 10.11.1.0/27</span><span class="sxs-lookup"><span data-stu-id="b750e-184">GatewaySubnet: 10.11.1.0/27</span></span>

<span data-ttu-id="b750e-185">**TestVNet4에 대한 값**</span><span class="sxs-lookup"><span data-stu-id="b750e-185">**Values for TestVNet4**</span></span>

<span data-ttu-id="b750e-186">이름: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="b750e-186">Name: TestVNet4</span></span><br>
<span data-ttu-id="b750e-187">주소 공간: 10.41.0.0/16, 10.42.0.0/16(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="b750e-187">Address space: 10.41.0.0/16, 10.42.0.0/16 (optional)</span></span><br>
<span data-ttu-id="b750e-188">서브넷 이름: 기본값</span><span class="sxs-lookup"><span data-stu-id="b750e-188">Subnet name: default</span></span><br>
<span data-ttu-id="b750e-189">서브넷 주소 범위: 10.41.0.1/24</span><span class="sxs-lookup"><span data-stu-id="b750e-189">Subnet address range: 10.41.0.1/24</span></span><br>
<span data-ttu-id="b750e-190">리소스 그룹: ClassicRG</span><span class="sxs-lookup"><span data-stu-id="b750e-190">Resource group: ClassicRG</span></span><br>
<span data-ttu-id="b750e-191">위치: 미국 서부</span><span class="sxs-lookup"><span data-stu-id="b750e-191">Location: West US</span></span><br>
<span data-ttu-id="b750e-192">게이트웨이 서브넷: 10.41.1.0/27</span><span class="sxs-lookup"><span data-stu-id="b750e-192">GatewaySubnet: 10.41.1.0/27</span></span>

<span data-ttu-id="b750e-193">**VNet을 만드는 경우 다음 설정에 유념하세요.**</span><span class="sxs-lookup"><span data-stu-id="b750e-193">**When creating your VNets, keep in mind the following settings:**</span></span>

* <span data-ttu-id="b750e-194">**가상 네트워크 주소 공간** – 가상 네트워크 주소 공간 페이지에서 가상 네트워크에 사용할 주소 범위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-194">**Virtual Network Address Spaces** – On the Virtual Network Address Spaces page, specify the address range that you want to use for your virtual network.</span></span> <span data-ttu-id="b750e-195">가상 네트워크에 배포하는 VM 및 다른 역할 인스턴스에 할당될 동적 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-195">These are the dynamic IP addresses that will be assigned to the VMs and other role instances that you deploy to this virtual network.</span></span><br><span data-ttu-id="b750e-196">선택하는 주소 공간은 이 VNet이 연결될 다른 VNet 또는 온-프레미스 위치의 주소 공간과 겹칠 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-196">The address spaces you select cannot overlap with the address spaces for any of the other VNets or on-premises locations that this VNet will connect to.</span></span>

* <span data-ttu-id="b750e-197">**위치** – 가상 네트워크를 만들 때 Azure 위치(지역)와 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-197">**Location** – When you create a virtual network, you associate it with an Azure location (region).</span></span> <span data-ttu-id="b750e-198">예를 들어 실제로 West US에 배치할 가상 네트워크에 VM을 배포하려는 경우 해당 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-198">For example, if you want your VMs that are deployed to your virtual network to be physically located in West US, select that location.</span></span> <span data-ttu-id="b750e-199">가상 네트워크를 만든 후에는 가상 네트워크에 연결된 위치를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-199">You can’t change the location associated with your virtual network after you create it.</span></span>

<span data-ttu-id="b750e-200">**VNet을 만든 후에는 다음 설정을 추가할 수 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="b750e-200">**After creating your VNets, you can add the following settings:**</span></span>

* <span data-ttu-id="b750e-201">**주소 공간** – 이 구성에는 주소 공간이 더 필요하지 않지만 VNet을 만든 후 주소 공간을 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-201">**Address space** – Additional address space is not required for this configuration, but you can add additional address space after creating the VNet.</span></span>

* <span data-ttu-id="b750e-202">**서브넷** – 이 구성에는 서브넷이 더 필요하지 않지만 다른 역할 인스턴스와 분리된 서브넷에 VM을 두려는 경우가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-202">**Subnets** – Additional subnets are not required for this configuration, but you might want to have your VMs in a subnet that is separate from your other role instances.</span></span>

* <span data-ttu-id="b750e-203">**DNS 서버** – DNS 서버 이름 및 IP 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-203">**DNS servers** – Enter the DNS server name and IP address.</span></span> <span data-ttu-id="b750e-204">이 설정은 DNS 서버를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-204">This setting does not create a DNS server.</span></span> <span data-ttu-id="b750e-205">이렇게 하면 이 가상 네트워크에 대한 이름 확인에 사용하려는 DNS 서버를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-205">It allows you to specify the DNS servers that you want to use for name resolution for this virtual network.</span></span>

<span data-ttu-id="b750e-206">이 섹션에서는 연결 형식, 로컬 사이트를 구성하고 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-206">In this section, you configure the connection type, the local site, and create the gateway.</span></span>

## <span data-ttu-id="b750e-207"><a name="localsite"></a>3단계 - 로컬 사이트 구성</span><span class="sxs-lookup"><span data-stu-id="b750e-207"><a name="localsite"></a>Step 3 - Configure the local site</span></span>

<span data-ttu-id="b750e-208">Azure는 각 로컬 네트워크 사이트에 지정된 설정을 사용하여 VNet 간에 트래픽을 라우팅하는 방법을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-208">Azure uses the settings specified in each local network site to determine how to route traffic between the VNets.</span></span> <span data-ttu-id="b750e-209">각 VNet은 트래픽을 라우팅하려는 각 로컬 네트워크를 가리켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-209">Each VNet must point to the respective local network that you want to route traffic to.</span></span> <span data-ttu-id="b750e-210">각 로컬 네트워크 사이트를 참조하는 데 사용할 이름을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-210">You determine the name you want to use to refer to each local network site.</span></span> <span data-ttu-id="b750e-211">설명이 포함된 이름을 사용하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-211">It's best to use something descriptive.</span></span>

<span data-ttu-id="b750e-212">예를 들어 TestVNet1은 'VNet4Local'이라는 이름으로 만든 로컬 네트워크 사이트에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-212">For example, TestVNet1 connects to a local network site that you create named 'VNet4Local'.</span></span> <span data-ttu-id="b750e-213">VNet4Local에 대한 설정에는 TestVNet4의 주소 접두사가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-213">The settings for VNet4Local contain the address prefixes for TestVNet4.</span></span>

<span data-ttu-id="b750e-214">각 VNet의 로컬 사이트는 다른 VNet입니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-214">The local site for each VNet is the other VNet.</span></span> <span data-ttu-id="b750e-215">다음 예제 값은 여기의 구성에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-215">The following example values are used for our configuration:</span></span>

| <span data-ttu-id="b750e-216">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="b750e-216">Virtual Network</span></span> | <span data-ttu-id="b750e-217">주소 공간</span><span class="sxs-lookup"><span data-stu-id="b750e-217">Address Space</span></span> | <span data-ttu-id="b750e-218">지역</span><span class="sxs-lookup"><span data-stu-id="b750e-218">Region</span></span> | <span data-ttu-id="b750e-219">로컬 네트워크 사이트에 연결</span><span class="sxs-lookup"><span data-stu-id="b750e-219">Connects to local network site</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b750e-220">TestVNet1</span><span class="sxs-lookup"><span data-stu-id="b750e-220">TestVNet1</span></span> |<span data-ttu-id="b750e-221">TestVNet1</span><span class="sxs-lookup"><span data-stu-id="b750e-221">TestVNet1</span></span><br><span data-ttu-id="b750e-222">(10.11.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="b750e-222">(10.11.0.0/16)</span></span><br><span data-ttu-id="b750e-223">(10.12.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="b750e-223">(10.12.0.0/16)</span></span> |<span data-ttu-id="b750e-224">미국 동부</span><span class="sxs-lookup"><span data-stu-id="b750e-224">East US</span></span> |<span data-ttu-id="b750e-225">VNet4Local</span><span class="sxs-lookup"><span data-stu-id="b750e-225">VNet4Local</span></span><br><span data-ttu-id="b750e-226">(10.41.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="b750e-226">(10.41.0.0/16)</span></span><br><span data-ttu-id="b750e-227">(10.42.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="b750e-227">(10.42.0.0/16)</span></span> |
| <span data-ttu-id="b750e-228">TestVNet4</span><span class="sxs-lookup"><span data-stu-id="b750e-228">TestVNet4</span></span> |<span data-ttu-id="b750e-229">TestVNet4</span><span class="sxs-lookup"><span data-stu-id="b750e-229">TestVNet4</span></span><br><span data-ttu-id="b750e-230">(10.41.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="b750e-230">(10.41.0.0/16)</span></span><br><span data-ttu-id="b750e-231">(10.42.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="b750e-231">(10.42.0.0/16)</span></span> |<span data-ttu-id="b750e-232">미국 서부</span><span class="sxs-lookup"><span data-stu-id="b750e-232">West US</span></span> |<span data-ttu-id="b750e-233">VNet1Local</span><span class="sxs-lookup"><span data-stu-id="b750e-233">VNet1Local</span></span><br><span data-ttu-id="b750e-234">(10.11.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="b750e-234">(10.11.0.0/16)</span></span><br><span data-ttu-id="b750e-235">(10.12.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="b750e-235">(10.12.0.0/16)</span></span> |

1. <span data-ttu-id="b750e-236">Azure Portal에서 TestVNet1을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-236">Locate TestVNet1 in the Azure portal.</span></span> <span data-ttu-id="b750e-237">블레이드의 **VPN 연결** 섹션에서 **게이트웨이**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-237">In the **VPN connections** section of the blade, click **Gateway**.</span></span>

    ![게이트웨이 없음](./media/vpn-gateway-howto-vnet-vnet-portal-classic/nogateway.png)
2. <span data-ttu-id="b750e-239">**새 VPN 연결** 페이지에서 **사이트 간**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-239">On the **New VPN Connection** page, select **Site-to-Site**.</span></span>
3. <span data-ttu-id="b750e-240">**로컬 사이트**를 클릭하여 로컬 사이트 페이지를 열고 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-240">Click **Local site** to open the Local site page and configure the settings.</span></span>
4. <span data-ttu-id="b750e-241">**로컬 사이트** 페이지에서 로컬 사이트 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-241">On the **Local site** page, name your local site.</span></span> <span data-ttu-id="b750e-242">예제의 경우 로컬 사이트 이름을 'VNet4Local'이라고 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-242">In our example, we name the local site 'VNet4Local'.</span></span>
5. <span data-ttu-id="b750e-243">**VPN 게이트웨이 IP 주소**의 경우 IP 주소가 올바른 형식이기만 하면 무엇이든 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-243">For **VPN gateway IP address**, you can use any IP address that you want, as long as it's in a valid format.</span></span> <span data-ttu-id="b750e-244">일반적으로는 VPN 장치의 실제 외부 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-244">Typically, you’d use the actual external IP address for a VPN device.</span></span> <span data-ttu-id="b750e-245">하지만 클래식 VNet-VNet 구성의 경우 VNet의 게이트웨이에 할당된 공용 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-245">But, for a classic VNet-to-VNet configuration, you use the public IP address that is assigned to the gateway for your VNet.</span></span> <span data-ttu-id="b750e-246">가상 네트워크 게이트웨이를 아직 만들지 않은 경우 유효한 공용 IP 주소라면 무엇이든 자리 표시자로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-246">Given that you’ve not yet created the virtual network gateway, you specify any valid public IP address as a placeholder.</span></span><br><span data-ttu-id="b750e-247">이 구성에서는 선택 사항이 아니므로 이 항목은 비워두면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-247">Don't leave this blank - it's not optional for this configuration.</span></span> <span data-ttu-id="b750e-248">이후 단계에서 Azure가 해당하는 가상 네트워크 게이트웨이 IP 주소를 생성하고 나면 이 설정으로 돌아와서 IP 주소를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-248">In a later step, you go back into these settings and configure them with the corresponding virtual network gateway IP addresses once Azure generates it.</span></span>
6. <span data-ttu-id="b750e-249">**클라이언트 주소 공간**의 경우 다른 VNet의 주소 공간을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-249">For **Client Address Space**, use the address space of the other VNet.</span></span> <span data-ttu-id="b750e-250">계획 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b750e-250">Refer to your planning example.</span></span> <span data-ttu-id="b750e-251">**확인**을 클릭하여 설정을 저장하고 **새 VPN 연결** 블레이드로 다시 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-251">Click **OK** to save your settings and return back to the **New VPN Connection** blade.</span></span>

    ![로컬 사이트](./media/vpn-gateway-howto-vnet-vnet-portal-classic/localsite.png)

## <span data-ttu-id="b750e-253"><a name="gw"></a>4단계 - 가상 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="b750e-253"><a name="gw"></a>Step 4 - Create the virtual network gateway</span></span>

<span data-ttu-id="b750e-254">각 가상 네트워크에는 가상 네트워크 게이트웨이가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-254">Each virtual network must have a virtual network gateway.</span></span> <span data-ttu-id="b750e-255">가상 네트워크 게이트웨이는 트래픽을 라우팅하고 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-255">The virtual network gateway routes and encrypts traffic.</span></span>

1. <span data-ttu-id="b750e-256">**새 VPN 연결** 블레이드에서 **게이트웨이 즉시 만들기** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-256">On the **New VPN Connection** blade, select the checkbox **Create gateway immediately**.</span></span>
2. <span data-ttu-id="b750e-257">**서브넷, 크기 및 라우팅 유형**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-257">Click **Subnet, size and routing type**.</span></span> <span data-ttu-id="b750e-258">**게이트웨이 구성** 블레이드에서 **서브넷**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-258">On the **Gateway configuration** blade, click **Subnet**.</span></span>
3. <span data-ttu-id="b750e-259">게이트웨이 서브넷 이름이 필요한 이름 'GatewaySubnet'으로 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-259">The gateway subnet name is filled in automatically with the required name 'GatewaySubnet'.</span></span> <span data-ttu-id="b750e-260">**주소 범위**는 VPN 게이트웨이 서비스에 할당된 IP 주소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-260">The **Address range** contains the IP addresses that are allocated to the VPN gateway services.</span></span> <span data-ttu-id="b750e-261">일부 구성은 게이트웨이 서브넷 /29를 허용하지만 게이트웨이 서비스에 IP 주소가 더 필요할 수 있는 향후 구성을 수용하기 위해 /28 또는 /27을 사용하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-261">Some configurations allow a gateway subnet of /29, but it's best to use a /28 or /27 to accommodate future configurations that may require more IP addresses for the gateway services.</span></span> <span data-ttu-id="b750e-262">여기의 예제에서는 10.11.1.0/27을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-262">In our example settings, we use 10.11.1.0/27.</span></span> <span data-ttu-id="b750e-263">주소 공간을 조정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-263">Adjust the address space, then click **OK**.</span></span>
4. <span data-ttu-id="b750e-264">**게이트웨이 크기**를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-264">Configure the **Gateway Size**.</span></span> <span data-ttu-id="b750e-265">이 설정은 [게이트웨이 SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b750e-265">This setting refers to the [Gateway SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>
5. <span data-ttu-id="b750e-266">**라우팅 유형**을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-266">Configure the **Routing Type**.</span></span> <span data-ttu-id="b750e-267">이 구성에 대한 라우팅 유형은 **동적**이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-267">The routing type for this configuration must be **Dynamic**.</span></span> <span data-ttu-id="b750e-268">게이트웨이를 없애고 새로 만들지 않는 한 나중에 라우팅 유형을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-268">You can't change the routing type later unless you tear down the gateway and create a new one.</span></span>
6. <span data-ttu-id="b750e-269">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-269">Click **OK**.</span></span>
7. <span data-ttu-id="b750e-270">**새 VPN 연결** 블레이드에서 **확인**을 클릭하여 가상 네트워크 게이트웨이 만들기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-270">On the **New VPN Connection** blade, click **OK** to begin creating the virtual network gateway.</span></span> <span data-ttu-id="b750e-271">종종 선택한 게이트웨이 SKU에 따라 게이트웨이를 만드는 데 45분 이상 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-271">Creating a gateway can often take 45 minutes or more, depending on the selected gateway SKU.</span></span>

## <span data-ttu-id="b750e-272"><a name="vnet4settings"></a>5단계 - TestVNet4 설정 구성</span><span class="sxs-lookup"><span data-stu-id="b750e-272"><a name="vnet4settings"></a>Step 5 - Configure TestVNet4 settings</span></span>

<span data-ttu-id="b750e-273">[로컬 사이트 만들기](#localsite)와 [가상 네트워크 게이트웨이 만들기](#gw) 단계를 반복하여 TestVNet4를 구성하고 필요한 경우 값을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-273">Repeat the steps to [Create a local site](#localsite) and [Create the virtual network gateway](#gw) to configure TestVNet4, substituting the values when necessary.</span></span> <span data-ttu-id="b750e-274">연습에서 수행하는 이 작업을 수행하는 경우 [예제 값](#vnetvalues)을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="b750e-274">If you are doing this as an exercise, use the [Example values](#vnetvalues).</span></span>

## <span data-ttu-id="b750e-275"><a name="updatelocal"></a>6단계 - 로컬 사이트 업데이트</span><span class="sxs-lookup"><span data-stu-id="b750e-275"><a name="updatelocal"></a>Step 6 - Update the local sites</span></span>

<span data-ttu-id="b750e-276">가상 네트워크 게이트웨이가 두 VNet에 대해 만들어진 후에는 로컬 사이트 **VPN 게이트웨이IP 주소** 값을 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-276">After your virtual network gateways have been created for both VNets, you must adjust the local sites **VPN gateway IP address** values.</span></span>

|<span data-ttu-id="b750e-277">VNet 이름</span><span class="sxs-lookup"><span data-stu-id="b750e-277">VNet name</span></span>|<span data-ttu-id="b750e-278">연결된 사이트</span><span class="sxs-lookup"><span data-stu-id="b750e-278">Connected site</span></span>|<span data-ttu-id="b750e-279">게이트웨이 IP 주소</span><span class="sxs-lookup"><span data-stu-id="b750e-279">Gateway IP address</span></span>|
|:--- |:--- |:--- |
|<span data-ttu-id="b750e-280">TestVNet1</span><span class="sxs-lookup"><span data-stu-id="b750e-280">TestVNet1</span></span>|<span data-ttu-id="b750e-281">VNet4Local</span><span class="sxs-lookup"><span data-stu-id="b750e-281">VNet4Local</span></span>|<span data-ttu-id="b750e-282">TestVNet4의 VPN 게이트웨이 IP 주소</span><span class="sxs-lookup"><span data-stu-id="b750e-282">VPN gateway IP address for TestVNet4</span></span>|
|<span data-ttu-id="b750e-283">TestVNet4</span><span class="sxs-lookup"><span data-stu-id="b750e-283">TestVNet4</span></span>|<span data-ttu-id="b750e-284">VNet1Local</span><span class="sxs-lookup"><span data-stu-id="b750e-284">VNet1Local</span></span>|<span data-ttu-id="b750e-285">TestVNet1의 VPN 게이트웨이 IP 주소</span><span class="sxs-lookup"><span data-stu-id="b750e-285">VPN gateway IP address for TestVNet1</span></span>|

### <a name="part-1---get-the-virtual-network-gateway-public-ip-address"></a><span data-ttu-id="b750e-286">1부 - 가상 네트워크 게이트웨이 공용 IP 주소 가져오기</span><span class="sxs-lookup"><span data-stu-id="b750e-286">Part 1 - Get the virtual network gateway public IP address</span></span>

1. <span data-ttu-id="b750e-287">Azure Portal에서 가상 네트워크를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-287">Locate your virtual network in the Azure portal.</span></span>
2. <span data-ttu-id="b750e-288">클릭하여 VNet **개요** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-288">Click to open the VNet **Overview** blade.</span></span> <span data-ttu-id="b750e-289">블레이드의 **VPN 연결**에서 가상 네트워크 게이트웨이의 IP 주소를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-289">On the blade, in **VPN connections**, you can view the IP address for your virtual network gateway.</span></span>

  ![공용 IP](./media/vpn-gateway-howto-vnet-vnet-portal-classic/publicIP.png)
3. <span data-ttu-id="b750e-291">IP 주소를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-291">Copy the IP address.</span></span> <span data-ttu-id="b750e-292">다음 섹션에서 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-292">You will use it in the next section.</span></span>
4. <span data-ttu-id="b750e-293">TestVNet4에 대해 이들 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-293">Repeat these steps for TestVNet4</span></span>

### <a name="part-2---modify-the-local-sites"></a><span data-ttu-id="b750e-294">2부 - 로컬 사이트 수정</span><span class="sxs-lookup"><span data-stu-id="b750e-294">Part 2 - Modify the local sites</span></span>

1. <span data-ttu-id="b750e-295">Azure Portal에서 가상 네트워크를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-295">Locate your virtual network in the Azure portal.</span></span>
2. <span data-ttu-id="b750e-296">VNet **개요** 블레이드에서 로컬 사이트를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-296">On the VNet **Overview** blade, click the local site.</span></span>

  ![생성된 로컬 사이트](./media/vpn-gateway-howto-vnet-vnet-portal-classic/local.png)
3. <span data-ttu-id="b750e-298">**사이트 간 VPN 연결** 블레이드에서 수정할 로컬 사이트의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-298">On the **Site-to-Site VPN Connections** blade, click the name of the local site that you want to modify.</span></span>

  ![로컬 사이트 열기](./media/vpn-gateway-howto-vnet-vnet-portal-classic/openlocal.png)
4. <span data-ttu-id="b750e-300">수정할 **로컬 사이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-300">Click the **Local site** that you want to modify.</span></span>

  ![사이트 수정](./media/vpn-gateway-howto-vnet-vnet-portal-classic/connections.png)
5. <span data-ttu-id="b750e-302">**VPN 게이트웨이 IP 주소**를 업데이트하고 **확인**을 클릭하여 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-302">Update the **VPN gateway IP address** and click **OK** to save the settings.</span></span>

  ![게이트웨이 IP](./media/vpn-gateway-howto-vnet-vnet-portal-classic/gwupdate.png)
6. <span data-ttu-id="b750e-304">다른 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-304">Close the other blades.</span></span>
7. <span data-ttu-id="b750e-305">TestVNet4에 대해 이들 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-305">Repeat these steps for TestVNet4.</span></span>

## <span data-ttu-id="b750e-306"><a name="getvalues"></a>7단계 - 네트워크 구성 파일에서 값 검색</span><span class="sxs-lookup"><span data-stu-id="b750e-306"><a name="getvalues"></a>Step 7 - Retrieve values from the network configuration file</span></span>

<span data-ttu-id="b750e-307">Azure Portal에서 클래식 VNet을 만드는 경우 볼 수 있는 이름은 PowerShell에 사용한 전체 이름이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-307">When you create classic VNets in the Azure portal, the name that you view is not the full name that you use for PowerShell.</span></span> <span data-ttu-id="b750e-308">예를 들어 포털에 **TestVNet1**이라는 이름으로 표시되는 VNet은 네트워크 구성 파일에서 훨씬 더 긴 이름이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-308">For example, a VNet that appears to be named **TestVNet1** in the portal, may have a much longer name in the network configuration file.</span></span> <span data-ttu-id="b750e-309">해당 이름은 **Group ClassicRG TestVNet1**과 같은 모양일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-309">The name might look something like: **Group ClassicRG TestVNet1**.</span></span> <span data-ttu-id="b750e-310">연결을 만드는 경우 네트워크 구성 파일에 있는 값을 사용하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-310">When you create your connections, it's important to use the values that you see in the network configuration file.</span></span>

<span data-ttu-id="b750e-311">다음 단계에서는 연결에 필요한 값을 확보하기 위해 Azure 계정에 연결하고 네트워크 구성 파일을 다운로드하여 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-311">In the following steps, you will connect to your Azure account and download and view the network configuration file to obtain the values that are required for your connections.</span></span>

1. <span data-ttu-id="b750e-312">최신 버전의 Azure SM(서비스 관리) PowerShell cmdlet을 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-312">Download and install the latest version of the Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="b750e-313">자세한 내용은 [Azure PowerShell 설치 및 구성하는 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b750e-313">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

2. <span data-ttu-id="b750e-314">상승된 권한으로 PowerShell 콘솔을 열고 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-314">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="b750e-315">연결에 도움이 되도록 다음 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-315">Use the following example to help you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="b750e-316">계정에 대한 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-316">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="b750e-317">둘 이상의 구독이 있는 경우 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-317">If you have more than one subscription, select the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
  ```

  <span data-ttu-id="b750e-318">다음 cmdlet을 사용하여 클래식 배포 모델용 PowerShell에 Azure 구독을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-318">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span></span>

  ```powershell
  Add-AzureAccount
  ```
3. <span data-ttu-id="b750e-319">네트워크 구성 파일을 내보내고 및 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-319">Export and view the network configuration file.</span></span> <span data-ttu-id="b750e-320">컴퓨터에 디렉터리를 만들고 디렉터리에 네트워크 구성 파일을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-320">Create a directory on your computer and then export the network configuration file to the directory.</span></span> <span data-ttu-id="b750e-321">이 예제에서는 네트워크 구성 파일을 **C:\AzureNet**으로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-321">In this example, the network configuration file is exported to **C:\AzureNet**.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
4. <span data-ttu-id="b750e-322">텍스트 편집기에서 파일을 열고 VNet과 사이트의 이름을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-322">Open the file with a text editor and view the names for your VNets and sites.</span></span> <span data-ttu-id="b750e-323">연결을 만들 때 사용한 이름을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-323">These will be the name you use when you create your connections.</span></span><br><span data-ttu-id="b750e-324">VNet 이름은 **VirtualNetworkSite name =**으로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-324">VNet names are listed as **VirtualNetworkSite name =**</span></span><br><span data-ttu-id="b750e-325">사이트 이름은 **LocalNetworkSiteRef name =**으로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-325">Site names are listed as **LocalNetworkSiteRef name =**</span></span>

## <span data-ttu-id="b750e-326"><a name="createconnections"></a>8단계 - VPN 게이트웨이 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="b750e-326"><a name="createconnections"></a>Step 8 - Create the VPN gateway connections</span></span>

<span data-ttu-id="b750e-327">위의 모든 단계를 완료한 후에는 IPsec/IKE 사전 공유 키를 설정하고 연결을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-327">When all the previous steps have been completed, you can set the IPsec/IKE pre-shared keys and create the connection.</span></span> <span data-ttu-id="b750e-328">이번 단계에서는 PowerShell을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-328">This set of steps uses PowerShell.</span></span> <span data-ttu-id="b750e-329">클래식 배포 모델을 위한 VNet-VNet 연결은 Azure Portal에서 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-329">VNet-to-VNet connections for the classic deployment model cannot be configured in the Azure portal.</span></span>

<span data-ttu-id="b750e-330">아래 예제에서 공유 키가 정확히 동일한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-330">In the examples, notice that the shared key is exactly the same.</span></span> <span data-ttu-id="b750e-331">공유 키는 항상 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-331">The shared key must always match.</span></span> <span data-ttu-id="b750e-332">이 예제의 값을 VNet과 로컬 네트워크 사이트의 정확한 이름으로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-332">Be sure to replace the values in these examples with the exact names for your VNets and Local Network Sites.</span></span>

1. <span data-ttu-id="b750e-333">TestVNet1 대 TestVNet4 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-333">Create the TestVNet1 to TestVNet4 connection.</span></span>

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet1' `
  -LocalNetworkSiteName '17BE5E2C_VNet4Local' -SharedKey A1b2C3D4
  ```
2. <span data-ttu-id="b750e-334">TestVNet4 대 TestVNet1 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-334">Create the TestVNet4 to TestVNet1 connection.</span></span>

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet4' `
  -LocalNetworkSiteName 'F7F7BFC7_VNet1Local' -SharedKey A1b2C3D4
  ```
3. <span data-ttu-id="b750e-335">연결이 초기화될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-335">Wait for the connections to initialize.</span></span> <span data-ttu-id="b750e-336">게이트웨이가 초기화된 후에는 상태가 ‘성공’입니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-336">Once the gateway has initialized, the Status is 'Successful'.</span></span>

  ```
  Error          :
  HttpStatusCode : OK
  Id             :
  Status         : Successful
  RequestId      :
  StatusCode     : OK
  ```

## <span data-ttu-id="b750e-337"><a name="faq"></a>클래식 VNet에 대한 VNet-VNet 고려 사항</span><span class="sxs-lookup"><span data-stu-id="b750e-337"><a name="faq"></a>VNet-to-VNet considerations for classic VNets</span></span>
* <span data-ttu-id="b750e-338">가상 네트워크는 같은 구독에 있을 수도 있고 다른 구독에 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-338">The virtual networks can be in the same or different subscriptions.</span></span>
* <span data-ttu-id="b750e-339">가상 네트워크는 같은 Azure 지역(위치)에 있을 수도 있고 다른 Azure 지역(위치)에 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-339">The virtual networks can be in the same or different Azure regions (locations).</span></span>
* <span data-ttu-id="b750e-340">클라우드 서비스 또는 부하 분산 끝점은 연결되어 있더라도 여러 가상 네트워크에 분산될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-340">A cloud service or a load balancing endpoint can't span across virtual networks, even if they are connected together.</span></span>
* <span data-ttu-id="b750e-341">여러 가상 네트워크를 연결할 때 VPN 장치는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-341">Connecting multiple virtual networks together doesn't require any VPN devices.</span></span>
* <span data-ttu-id="b750e-342">VNet 간 연결은 Azure 가상 네트워크 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-342">VNet-to-VNet supports connecting Azure Virtual Networks.</span></span> <span data-ttu-id="b750e-343">그러나 가상 네트워크에 배포되지 않은 가상 컴퓨터 또는 클라우드 서비스 연결은 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-343">It does not support connecting virtual machines or cloud services that are not deployed to a virtual network.</span></span>
* <span data-ttu-id="b750e-344">VNet-VNet을 위해서는 동적 라우팅 게이트웨이가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-344">VNet-to-VNet requires dynamic routing gateways.</span></span> <span data-ttu-id="b750e-345">Azure 정적 라우팅 게이트웨이는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-345">Azure static routing gateways are not supported.</span></span>
* <span data-ttu-id="b750e-346">가상 네트워크 연결을 다중 사이트 VPN과 동시에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-346">Virtual network connectivity can be used simultaneously with multi-site VPNs.</span></span> <span data-ttu-id="b750e-347">가상 네트워크 VPN 게이트웨이당 최대 10개의 VPN 터널을 다른 가상 네트워크 또는 온-프레미스 사이트에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-347">There is a maximum of 10 VPN tunnels for a virtual network VPN gateway connecting to either other virtual networks, or on-premises sites.</span></span>
* <span data-ttu-id="b750e-348">가상 네트워크 및 온-프레미스 로컬 네트워크 사이트의 주소 공간이 겹쳐서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-348">The address spaces of the virtual networks and on-premises local network sites must not overlap.</span></span> <span data-ttu-id="b750e-349">주소 공간이 겹치면 가상 네트워크 만들기 또는 netcfg 구성 파일 업로드가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-349">Overlapping address spaces will cause the creation of virtual networks or uploading netcfg configuration files to fail.</span></span>
* <span data-ttu-id="b750e-350">가상 네트워크 한 쌍 간의 중복 터널은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-350">Redundant tunnels between a pair of virtual networks are not supported.</span></span>
* <span data-ttu-id="b750e-351">P2S VPN을 비롯한 VNet의 모든 VPN 터널은 VPN 게이트웨이의 사용 가능한 대역폭 및 Azure의 동일 VPN 게이트웨이 작동 시간 SLA를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-351">All VPN tunnels for the VNet, including P2S VPNs, share the available bandwidth for the VPN gateway, and the same VPN gateway uptime SLA in Azure.</span></span>
* <span data-ttu-id="b750e-352">VNet-VNet 트래픽은 Azure 백본 전체에서 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-352">VNet-to-VNet traffic travels across the Azure backbone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b750e-353">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b750e-353">Next steps</span></span>
<span data-ttu-id="b750e-354">연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b750e-354">Verify your connections.</span></span> <span data-ttu-id="b750e-355">[VPN Gateway 연결 확인](vpn-gateway-verify-connection-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b750e-355">See [Verify a VPN Gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>
