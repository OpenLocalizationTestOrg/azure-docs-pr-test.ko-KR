---
title: "다른 VNet에 Azure Virtual Network 연결: PowerShell | Microsoft Docs"
description: "이 문서에서는 Azure 리소스 관리자 및 PowerShell을 사용하여 가상 네트워크를 함께 연결하는 과정을 안내합니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 8c42c0046ccaa98c572134042fbbb7e883ef93c3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a><span data-ttu-id="4d63f-103">PowerShell을 사용하여 VNet-VNet VPN Gateway 연결 구성</span><span class="sxs-lookup"><span data-stu-id="4d63f-103">Configure a VNet-to-VNet VPN gateway connection using PowerShell</span></span>

<span data-ttu-id="4d63f-104">이 문서에서는 가상 네트워크 간에 VPN Gateway 연결을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-104">This article shows you how to create a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="4d63f-105">가상 네트워크는 같은 또는 다른 구독의 같은 지역에 있을 수도 있고 다른 지역에 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-105">The virtual networks can be in the same or different regions, and from the same or different subscriptions.</span></span> <span data-ttu-id="4d63f-106">다른 구독의 VNet을 연결할 때 구독은 동일한 Active Directory 테넌트와 연결될 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-106">When connecting VNets from different subscriptions, the subscriptions do not need to be associated with the same Active Directory tenant.</span></span> 

<span data-ttu-id="4d63f-107">이 문서의 단계는 Resource Manager 배포 모델에 적용되며 PowerShell을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-107">The steps in this article apply to the Resource Manager deployment model and use PowerShell.</span></span> <span data-ttu-id="4d63f-108">다른 배포 도구 또는 배포 모델을 사용하는 경우 다음 목록에서 별도의 옵션을 선택하여 이 구성을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4d63f-109">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4d63f-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="4d63f-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d63f-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="4d63f-111">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4d63f-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="4d63f-112">Azure Portal(클래식)</span><span class="sxs-lookup"><span data-stu-id="4d63f-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="4d63f-113">다양한 배포 모델 간 연결 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4d63f-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="4d63f-114">다양한 배포 모델 간 연결 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d63f-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="4d63f-115">가상 네트워크를 다른 가상 네트워크에 연결(VNet-VNet)하는 것은 VNet을 온-프레미스 사이트 위치에 연결하는 것과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-115">Connecting a virtual network to another virtual network (VNet-to-VNet) is similar to connecting a VNet to an on-premises site location.</span></span> <span data-ttu-id="4d63f-116">두 연결 유형 모두 VPN 게이트웨이를 사용하여 IPsec/IKE를 통한 보안 터널을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-116">Both connectivity types use a VPN gateway to provide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="4d63f-117">VNet이 동일한 지역에 있는 경우 VNet 피어링을 사용하여 연결하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-117">If your VNets are in the same region, you may want to consider connecting them using VNet Peering.</span></span> <span data-ttu-id="4d63f-118">VNet 피어링은 VPN Gateway를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="4d63f-119">자세한 내용은 [VNet 피어링](../virtual-network/virtual-network-peering-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d63f-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="4d63f-120">VNet-VNet 통신을 다중 사이트 구성과 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="4d63f-121">이렇게 하면 다음 다이어그램에 표시된 것처럼 프레미스 간 연결을 가상 네트워크 간 연결과 결합하는 네트워크 토폴로지를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in the following diagram:</span></span>

![연결 정보](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a><span data-ttu-id="4d63f-123">가상 네트워크에 연결하는 이유</span><span class="sxs-lookup"><span data-stu-id="4d63f-123">Why connect virtual networks?</span></span>

<span data-ttu-id="4d63f-124">다음과 같은 이유로 가상 네트워크에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-124">You may want to connect virtual networks for the following reasons:</span></span>

* <span data-ttu-id="4d63f-125">**지역 간 지리적 중복 및 지리적 상태**</span><span class="sxs-lookup"><span data-stu-id="4d63f-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="4d63f-126">인터넷 연결 끝점으로 이동하지 않고도 보안 연결을 통해 지역에서 복제 또는 동기화를 직접 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="4d63f-127">Azure Traffic Manager 및 부하 분산 장치를 사용하여 여러 Azure 지역 간의 지리적 중복을 통해 워크로드의 가용성을 높게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="4d63f-128">이러한 작업의 한 가지 주요 예는 여러 Azure 지역에 분산된 가용성 그룹을 사용하여 SQL AlwaysOn을 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-128">One important example is to set up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="4d63f-129">**분리 또는 관리 경계를 가진 지역별 다중 계층 응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="4d63f-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="4d63f-130">같은 지역 내에서 분리 또는 관리 요구 사항 때문에 여러 가상 네트워크가 함께 연결된 다중 계층 응용 프로그램을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-130">Within the same region, you can set up multi-tier applications with multiple virtual networks connected together due to isolation or administrative requirements.</span></span>

<span data-ttu-id="4d63f-131">VNet 간 연결에 대한 자세한 내용은 이 문서의 끝에 있는 [VNet 간 FAQ](#faq)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d63f-131">For more information about VNet-to-VNet connections, see the [VNet-to-VNet FAQ](#faq) at the end of this article.</span></span>

## <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="4d63f-132">어느 단계 집합을 사용해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="4d63f-132">Which set of steps should I use?</span></span>

<span data-ttu-id="4d63f-133">이 문서에서는 서로 다른 두 집합의 단계를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="4d63f-134">일련의 단계는 [동일한 구독에 상주하는 VNet](#samesub)이고 다른 단계는 [다른 구독에 상주하는 VNet](#difsub)입니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-134">One set of steps for [VNets that reside in the same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span> <span data-ttu-id="4d63f-135">둘 사이의 주요 차이점은 동일한 PowerShell 세션 내에서 모든 가상 네트워크 및 게이트웨이 리소스를 생성하고 구성할 수 있는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-135">The key difference between the sets is whether you can create and configure all virtual network and gateway resources within the same PowerShell session.</span></span>

<span data-ttu-id="4d63f-136">이 문서의 단계는 각 섹션의 시작 부분에 선언된 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-136">The steps in this article use variables that are declared at the beginning of each section.</span></span> <span data-ttu-id="4d63f-137">기존 VNet을 이미 사용하는 경우 변수를 수정하여 고유한 환경에 설정을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-137">If you already are working with existing VNets, modify the variables to reflect the settings in your own environment.</span></span> <span data-ttu-id="4d63f-138">가상 네트워크의 이름 확인을 원하는 경우 [이름 확인](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d63f-138">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

## <span data-ttu-id="4d63f-139"><a name="samesub"></a>같은 구독에 있는 VNet을 연결하는 방법</span><span class="sxs-lookup"><span data-stu-id="4d63f-139"><a name="samesub"></a>How to connect VNets that are in the same subscription</span></span>

![v2v 다이어그램](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="4d63f-141">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="4d63f-141">Before you begin</span></span>

<span data-ttu-id="4d63f-142">시작하기 전에 최신 버전의 Azure Resource Manager PowerShell(최소 4.0 이상) cmdlet을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-142">Before beginning, you need to install the latest version of the Azure Resource Manager PowerShell cmdlets, at least 4.0 or later.</span></span> <span data-ttu-id="4d63f-143">PowerShell cmdlet 설치에 대한 자세한 내용은 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d63f-143">For more information about installing the PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="4d63f-144"><a name="Step1"></a>1단계 - IP 주소 범위 계획</span><span class="sxs-lookup"><span data-stu-id="4d63f-144"><a name="Step1"></a>Step 1 - Plan your IP address ranges</span></span>

<span data-ttu-id="4d63f-145">다음 단계에서는 두 개의 가상 네트워크와 해당 게이트웨이 서브넷 및 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-145">In the following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="4d63f-146">그런 다음 두 VNet 간의 VPN 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-146">We then create a VPN connection between the two VNets.</span></span> <span data-ttu-id="4d63f-147">네트워크 구성에 대한 IP 주소 범위를 계획하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-147">It’s important to plan the IP address ranges for your network configuration.</span></span> <span data-ttu-id="4d63f-148">따라서 VNet 범위 또는 로컬 네트워크 범위가 겹치지 않는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-148">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="4d63f-149">이 예에서는 DNS 서버를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-149">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="4d63f-150">가상 네트워크의 이름 확인을 원하는 경우 [이름 확인](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d63f-150">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="4d63f-151">예제에서 다음 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-151">We use the following values in the examples:</span></span>

<span data-ttu-id="4d63f-152">**TestVNet1에 대한 값:**</span><span class="sxs-lookup"><span data-stu-id="4d63f-152">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="4d63f-153">VNet 이름: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="4d63f-153">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="4d63f-154">리소스 그룹: TestRG1</span><span class="sxs-lookup"><span data-stu-id="4d63f-154">Resource Group: TestRG1</span></span>
* <span data-ttu-id="4d63f-155">위치: 미국 동부</span><span class="sxs-lookup"><span data-stu-id="4d63f-155">Location: East US</span></span>
* <span data-ttu-id="4d63f-156">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="4d63f-156">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="4d63f-157">프런트 엔드: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4d63f-157">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="4d63f-158">백 엔드: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4d63f-158">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="4d63f-159">게이트웨이 서브넷 = 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="4d63f-159">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="4d63f-160">게이트웨이 이름: VNet1GW</span><span class="sxs-lookup"><span data-stu-id="4d63f-160">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="4d63f-161">공용 IP: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="4d63f-161">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="4d63f-162">VpnType: 경로 기반</span><span class="sxs-lookup"><span data-stu-id="4d63f-162">VPNType: RouteBased</span></span>
* <span data-ttu-id="4d63f-163">연결(1 대 4): VNet1 대 VNet4</span><span class="sxs-lookup"><span data-stu-id="4d63f-163">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="4d63f-164">연결(1 대 5): VNet1 대 VNet5</span><span class="sxs-lookup"><span data-stu-id="4d63f-164">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="4d63f-165">연결 유형: VNet 간</span><span class="sxs-lookup"><span data-stu-id="4d63f-165">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="4d63f-166">**TestVNet4에 대한 값:**</span><span class="sxs-lookup"><span data-stu-id="4d63f-166">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="4d63f-167">VNet 이름: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="4d63f-167">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="4d63f-168">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="4d63f-168">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="4d63f-169">프런트 엔드: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4d63f-169">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="4d63f-170">백 엔드: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4d63f-170">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="4d63f-171">게이트웨이 서브넷: 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="4d63f-171">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="4d63f-172">리소스 그룹: TestRG4</span><span class="sxs-lookup"><span data-stu-id="4d63f-172">Resource Group: TestRG4</span></span>
* <span data-ttu-id="4d63f-173">위치: 미국 서부</span><span class="sxs-lookup"><span data-stu-id="4d63f-173">Location: West US</span></span>
* <span data-ttu-id="4d63f-174">게이트웨이 이름: VNet4GW</span><span class="sxs-lookup"><span data-stu-id="4d63f-174">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="4d63f-175">공용 IP: VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="4d63f-175">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="4d63f-176">VpnType: 경로 기반</span><span class="sxs-lookup"><span data-stu-id="4d63f-176">VPNType: RouteBased</span></span>
* <span data-ttu-id="4d63f-177">연결: VNet4 대 VNet1</span><span class="sxs-lookup"><span data-stu-id="4d63f-177">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="4d63f-178">연결 유형: VNet 간</span><span class="sxs-lookup"><span data-stu-id="4d63f-178">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="4d63f-179"><a name="Step2"></a>2단계 - TestVNet1 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="4d63f-179"><a name="Step2"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="4d63f-180">변수 선언.</span><span class="sxs-lookup"><span data-stu-id="4d63f-180">Declare your variables.</span></span> <span data-ttu-id="4d63f-181">이 예제에서는 이 연습에 대한 값을 사용하여 변수를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-181">This example declares the variables using the values for this exercise.</span></span> <span data-ttu-id="4d63f-182">대부분의 경우에 값을 고유한 값으로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-182">In most cases, you should replace the values with your own.</span></span> <span data-ttu-id="4d63f-183">그러나 이 구성 유형에 익숙해지기 위해 단계를 차례로 실행하는 경우 이 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-183">However, you can use these variables if you are running through the steps to become familiar with this type of configuration.</span></span> <span data-ttu-id="4d63f-184">필요한 경우 변수를 수정한 다음 복사하여 PowerShell 콘솔에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-184">Modify the variables if needed, then copy and paste them into your PowerShell console.</span></span>

  ```powershell
  $Sub1 = "Replace_With_Your_Subcription_Name"
  $RG1 = "TestRG1"
  $Location1 = "East US"
  $VNetName1 = "TestVNet1"
  $FESubName1 = "FrontEnd"
  $BESubName1 = "Backend"
  $GWSubName1 = "GatewaySubnet"
  $VNetPrefix11 = "10.11.0.0/16"
  $VNetPrefix12 = "10.12.0.0/16"
  $FESubPrefix1 = "10.11.0.0/24"
  $BESubPrefix1 = "10.12.0.0/24"
  $GWSubPrefix1 = "10.12.255.0/27"
  $GWName1 = "VNet1GW"
  $GWIPName1 = "VNet1GWIP"
  $GWIPconfName1 = "gwipconf1"
  $Connection14 = "VNet1toVNet4"
  $Connection15 = "VNet1toVNet5"
  ```

2. <span data-ttu-id="4d63f-185">계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-185">Connect to your account.</span></span> <span data-ttu-id="4d63f-186">연결에 도움이 되도록 다음 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-186">Use the following example to help you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="4d63f-187">계정에 대한 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-187">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="4d63f-188">사용할 구독을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-188">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. <span data-ttu-id="4d63f-189">새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-189">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. <span data-ttu-id="4d63f-190">TestVNet1에 대한 서브넷 구성 만들기.</span><span class="sxs-lookup"><span data-stu-id="4d63f-190">Create the subnet configurations for TestVNet1.</span></span> <span data-ttu-id="4d63f-191">이 예제에서는 TestVNet1이라는 가상 네트워크와 GatewaySubnet, FrontEnd 및 Backend라는 세 개의 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-191">This example creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="4d63f-192">값을 대체할 때 언제나 게이트웨이 서브넷 이름을 GatewaySubnet라고 명시적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-192">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="4d63f-193">다른 이름을 지정하는 경우 게이트웨이 만들기가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-193">If you name it something else, your gateway creation fails.</span></span>

  <span data-ttu-id="4d63f-194">다음 예제에서는 앞에서 설정한 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-194">The following example uses the variables that you set earlier.</span></span> <span data-ttu-id="4d63f-195">이 예제에서 게이트웨이 서브넷은 /27을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-195">In this example, the gateway subnet is using a /27.</span></span> <span data-ttu-id="4d63f-196">게이트웨이 서브넷을 /29만큼 작게 만들 수 있지만 적어도 /28 또는 /27을 선택하여 더 많은 주소를 포함하는 큰 서브넷을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-196">While it is possible to create a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="4d63f-197">이렇게 하면 나중에 필요할 수도 있는 추가 구성에 맞게 충분히 주소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-197">This will allow for enough addresses to accommodate possible additional configurations that you may want in the future.</span></span>

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. <span data-ttu-id="4d63f-198">TestVNet1 만들기.</span><span class="sxs-lookup"><span data-stu-id="4d63f-198">Create TestVNet1.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. <span data-ttu-id="4d63f-199">VNet용으로 만들 게이트웨이에 할당할 공용 IP 주소를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-199">Request a public IP address to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="4d63f-200">AllocationMethod가 동적인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-200">Notice that the AllocationMethod is Dynamic.</span></span> <span data-ttu-id="4d63f-201">사용할 IP 주소를 지정할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-201">You cannot specify the IP address that you want to use.</span></span> <span data-ttu-id="4d63f-202">IP 주소는 게이트웨이에 동적으로 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-202">It's dynamically allocated to your gateway.</span></span> 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="4d63f-203">게이트웨이 구성 만들기.</span><span class="sxs-lookup"><span data-stu-id="4d63f-203">Create the gateway configuration.</span></span> <span data-ttu-id="4d63f-204">게이트웨이 구성은 사용할 공용 IP 주소 및 서브넷을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-204">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="4d63f-205">예제를 사용하여 게이트웨이 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-205">Use the example to create your gateway configuration.</span></span>

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. <span data-ttu-id="4d63f-206">TestVNet1에 대한 게이트웨이 만들기.</span><span class="sxs-lookup"><span data-stu-id="4d63f-206">Create the gateway for TestVNet1.</span></span> <span data-ttu-id="4d63f-207">이 단계에서는 TestVNet1용 가상 네트워크 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-207">In this step, you create the virtual network gateway for your TestVNet1.</span></span> <span data-ttu-id="4d63f-208">VNet-VNet 구성에는 RouteBased VpnType이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-208">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="4d63f-209">종종 선택한 게이트웨이 SKU에 따라 게이트웨이를 만드는 데 45분 이상 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-209">Creating a gateway can often take 45 minutes or more, depending on the selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a><span data-ttu-id="4d63f-210">3단계 - TestVNet4 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="4d63f-210">Step 3 - Create and configure TestVNet4</span></span>

<span data-ttu-id="4d63f-211">TestVNet1 구성이 끝나면 TestVNet4를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-211">Once you've configured TestVNet1, create TestVNet4.</span></span> <span data-ttu-id="4d63f-212">아래 단계에 따라 필요한 경우 값을 사용자의 고유한 값으로 바꾸십시오.</span><span class="sxs-lookup"><span data-stu-id="4d63f-212">Follow the steps below, replacing the values with your own when needed.</span></span> <span data-ttu-id="4d63f-213">이 단계는 같은 구독에 있기 때문에 같은 PowerShell 세션 내에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-213">This step can be done within the same PowerShell session because it is in the same subscription.</span></span>

1. <span data-ttu-id="4d63f-214">변수 선언.</span><span class="sxs-lookup"><span data-stu-id="4d63f-214">Declare your variables.</span></span> <span data-ttu-id="4d63f-215">값을 구성에 사용할 값으로 바꾸어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-215">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

  ```powershell
  $RG4 = "TestRG4"
  $Location4 = "West US"
  $VnetName4 = "TestVNet4"
  $FESubName4 = "FrontEnd"
  $BESubName4 = "Backend"
  $GWSubName4 = "GatewaySubnet"
  $VnetPrefix41 = "10.41.0.0/16"
  $VnetPrefix42 = "10.42.0.0/16"
  $FESubPrefix4 = "10.41.0.0/24"
  $BESubPrefix4 = "10.42.0.0/24"
  $GWSubPrefix4 = "10.42.255.0/27"
  $GWName4 = "VNet4GW"
  $GWIPName4 = "VNet4GWIP"
  $GWIPconfName4 = "gwipconf4"
  $Connection41 = "VNet4toVNet1"
  ```
2. <span data-ttu-id="4d63f-216">새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-216">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. <span data-ttu-id="4d63f-217">TestVNet4에 대한 서브넷 구성 만들기.</span><span class="sxs-lookup"><span data-stu-id="4d63f-217">Create the subnet configurations for TestVNet4.</span></span>

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. <span data-ttu-id="4d63f-218">TestVNet4 만들기.</span><span class="sxs-lookup"><span data-stu-id="4d63f-218">Create TestVNet4.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. <span data-ttu-id="4d63f-219">공용 IP 주소를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-219">Request a public IP address.</span></span>

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. <span data-ttu-id="4d63f-220">게이트웨이 구성 만들기.</span><span class="sxs-lookup"><span data-stu-id="4d63f-220">Create the gateway configuration.</span></span>

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. <span data-ttu-id="4d63f-221">TestVNet4 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="4d63f-221">Create the TestVNet4 gateway.</span></span> <span data-ttu-id="4d63f-222">종종 선택한 게이트웨이 SKU에 따라 게이트웨이를 만드는 데 45분 이상 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-222">Creating a gateway can often take 45 minutes or more, depending on the selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-the-connections"></a><span data-ttu-id="4d63f-223">4단계 - 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="4d63f-223">Step 4 - Create the connections</span></span>

1. <span data-ttu-id="4d63f-224">두 개의 가상 네트워크 게이트웨이 모두 가져오기.</span><span class="sxs-lookup"><span data-stu-id="4d63f-224">Get both virtual network gateways.</span></span> <span data-ttu-id="4d63f-225">이 예제에서와 같이 두 게이트웨이가 동일한 구독에 있으면 동일한 PowerShell 세션에서 이 단계를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-225">If both of the gateways are in the same subscription, as they are in the example, you can complete this step in the same PowerShell session.</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. <span data-ttu-id="4d63f-226">TestVNet1 대 TestVNet4 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-226">Create the TestVNet1 to TestVNet4 connection.</span></span> <span data-ttu-id="4d63f-227">이 단계에서는 TestVNet1에서 TestVNet4까지 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-227">In this step, you create the connection from TestVNet1 to TestVNet4.</span></span> <span data-ttu-id="4d63f-228">예제에서 참조된 공유 키를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-228">You'll see a shared key referenced in the examples.</span></span> <span data-ttu-id="4d63f-229">공유 키에 대해 고유한 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-229">You can use your own values for the shared key.</span></span> <span data-ttu-id="4d63f-230">중요한 점은 두 연결에서 모두 공유 키가 일치해야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-230">The important thing is that the shared key must match for both connections.</span></span> <span data-ttu-id="4d63f-231">연결 만들기는 완료하는 데 꽤 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-231">Creating a connection can take a short while to complete.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. <span data-ttu-id="4d63f-232">TestVNet4 대 TestVNet1 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-232">Create the TestVNet4 to TestVNet1 connection.</span></span> <span data-ttu-id="4d63f-233">이 단계는 TestVNet4에서 TestVNet1까지 연결을 만드는 점을 제외하면 위의 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-233">This step is similar to the one above, except you are creating the connection from TestVNet4 to TestVNet1.</span></span> <span data-ttu-id="4d63f-234">공유된 키가 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-234">Make sure the shared keys match.</span></span> <span data-ttu-id="4d63f-235">몇 분 후 연결이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-235">The connection will be established after a few minutes.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="4d63f-236">연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-236">Verify your connection.</span></span> <span data-ttu-id="4d63f-237">[연결을 확인하는 방법](#verify)섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d63f-237">See the section [How to verify your connection](#verify).</span></span>

## <span data-ttu-id="4d63f-238"><a name="difsub"></a>다른 구독에 있는 VNet을 연결하는 방법</span><span class="sxs-lookup"><span data-stu-id="4d63f-238"><a name="difsub"></a>How to connect VNets that are in different subscriptions</span></span>

![v2v 다이어그램](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

<span data-ttu-id="4d63f-240">이 시나리오에서는 TestVNet1 및 TestVNet5를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-240">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="4d63f-241">TestVNet1 및 TestVNet5는 다른 구독에 상주합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-241">TestVNet1 and TestVNet5 reside in a different subscription.</span></span> <span data-ttu-id="4d63f-242">구독은 동일한 Active Directory 테넌트와 연결될 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-242">The subscriptions do not need to be associated with the same Active Directory tenant.</span></span> <span data-ttu-id="4d63f-243">이러한 단계와 이전 집합의 차이점은 일부 구성 단계가 두 번째 구독 환경에서 별도의 PowerShell 세션으로 수행되어야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-243">The difference between these steps and the previous set is that some of the configuration steps need to be performed in a separate PowerShell session in the context of the second subscription.</span></span> <span data-ttu-id="4d63f-244">특히 두 구독이 다른 조직에 속한 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-244">Especially when the two subscriptions belong to different organizations.</span></span>

### <a name="step-5---create-and-configure-testvnet1"></a><span data-ttu-id="4d63f-245">5단계 - TestVNet1 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="4d63f-245">Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="4d63f-246">TestVNet1 및 TestVNet1의 VPN Gateway를 만들고 구성하려면 이전 섹션에서 [1단계](#Step1) 및 [2단계](#Step2)를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-246">You must complete [Step 1](#Step1) and [Step 2](#Step2) from the previous section to create and configure TestVNet1 and the VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="4d63f-247">이 구성의 경우 이전 섹션에서 TestVNet4를 만들 필요가 없지만 만든다고 해도 이 단계와 충돌하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-247">For this configuration, you are not required to create TestVNet4 from the previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="4d63f-248">1단계와 2단계가 완료되면 6단계를 계속하여 TestVNet5를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-248">Once you complete Step 1 and Step 2, continue with Step 6 to create TestVNet5.</span></span> 

### <a name="step-6---verify-the-ip-address-ranges"></a><span data-ttu-id="4d63f-249">6단계 - IP 주소 범위 확인</span><span class="sxs-lookup"><span data-stu-id="4d63f-249">Step 6 - Verify the IP address ranges</span></span>

<span data-ttu-id="4d63f-250">새 가상 네트워크 TestVNet5의 IP 주소 공간이 VNet 범위 또는 로컬 네트워크 게이트웨이 범위와 겹치지 않는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-250">It is important to make sure that the IP address space of the new virtual network, TestVNet5, does not overlap with any of your VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="4d63f-251">이 예제에서 가상 네트워크는 서로 다른 조직에 속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-251">In this example, the virtual networks may belong to different organizations.</span></span> <span data-ttu-id="4d63f-252">이 연습에서는 TestVNet5에 대해 다음 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-252">For this exercise, you can use the following values for the TestVNet5:</span></span>

<span data-ttu-id="4d63f-253">**TestVNet5에 대한 값:**</span><span class="sxs-lookup"><span data-stu-id="4d63f-253">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="4d63f-254">VNet 이름: TestVNet5</span><span class="sxs-lookup"><span data-stu-id="4d63f-254">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="4d63f-255">리소스 그룹: TestRG5</span><span class="sxs-lookup"><span data-stu-id="4d63f-255">Resource Group: TestRG5</span></span>
* <span data-ttu-id="4d63f-256">위치: 일본 동부</span><span class="sxs-lookup"><span data-stu-id="4d63f-256">Location: Japan East</span></span>
* <span data-ttu-id="4d63f-257">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="4d63f-257">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="4d63f-258">프런트 엔드: 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4d63f-258">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="4d63f-259">백 엔드: 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4d63f-259">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="4d63f-260">게이트웨이 서브넷: 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="4d63f-260">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="4d63f-261">게이트웨이 이름: VNet5GW</span><span class="sxs-lookup"><span data-stu-id="4d63f-261">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="4d63f-262">공용 IP: VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="4d63f-262">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="4d63f-263">VpnType: 경로 기반</span><span class="sxs-lookup"><span data-stu-id="4d63f-263">VPNType: RouteBased</span></span>
* <span data-ttu-id="4d63f-264">연결: VNet5 대 VNet1</span><span class="sxs-lookup"><span data-stu-id="4d63f-264">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="4d63f-265">연결 유형: VNet 간</span><span class="sxs-lookup"><span data-stu-id="4d63f-265">ConnectionType: VNet2VNet</span></span>

### <a name="step-7---create-and-configure-testvnet5"></a><span data-ttu-id="4d63f-266">7단계 - TestVNet5 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="4d63f-266">Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="4d63f-267">이 단계는 새 구독의 상황에서 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-267">This step must be done in the context of the new subscription.</span></span> <span data-ttu-id="4d63f-268">이 부분은 구독을 소유한 다른 조직의 관리자가 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-268">This part may be performed by the administrator in a different organization that owns the subscription.</span></span>

1. <span data-ttu-id="4d63f-269">변수 선언.</span><span class="sxs-lookup"><span data-stu-id="4d63f-269">Declare your variables.</span></span> <span data-ttu-id="4d63f-270">값을 구성에 사용할 값으로 바꾸어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-270">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

  ```powershell
  $Sub5 = "Replace_With_the_New_Subcription_Name"
  $RG5 = "TestRG5"
  $Location5 = "Japan East"
  $VnetName5 = "TestVNet5"
  $FESubName5 = "FrontEnd"
  $BESubName5 = "Backend"
  $GWSubName5 = "GatewaySubnet"
  $VnetPrefix51 = "10.51.0.0/16"
  $VnetPrefix52 = "10.52.0.0/16"
  $FESubPrefix5 = "10.51.0.0/24"
  $BESubPrefix5 = "10.52.0.0/24"
  $GWSubPrefix5 = "10.52.255.0/27"
  $GWName5 = "VNet5GW"
  $GWIPName5 = "VNet5GWIP"
  $GWIPconfName5 = "gwipconf5"
  $Connection51 = "VNet5toVNet1"
  ```
2. <span data-ttu-id="4d63f-271">구독 5에 연결.</span><span class="sxs-lookup"><span data-stu-id="4d63f-271">Connect to subscription 5.</span></span> <span data-ttu-id="4d63f-272">PowerShell 콘솔을 열고 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-272">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="4d63f-273">연결에 도움이 되도록 다음 샘플을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-273">Use the following sample to help you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="4d63f-274">계정에 대한 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-274">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="4d63f-275">사용할 구독을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-275">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. <span data-ttu-id="4d63f-276">새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-276">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. <span data-ttu-id="4d63f-277">TestVNet5에 대한 서브넷 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-277">Create the subnet configurations for TestVNet5.</span></span>

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. <span data-ttu-id="4d63f-278">TestVNet5 만들기.</span><span class="sxs-lookup"><span data-stu-id="4d63f-278">Create TestVNet5.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. <span data-ttu-id="4d63f-279">공용 IP 주소를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-279">Request a public IP address.</span></span>

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="4d63f-280">게이트웨이 구성 만들기.</span><span class="sxs-lookup"><span data-stu-id="4d63f-280">Create the gateway configuration.</span></span>

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. <span data-ttu-id="4d63f-281">TestVNet5 게이트웨이 만들기.</span><span class="sxs-lookup"><span data-stu-id="4d63f-281">Create the TestVNet5 gateway.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-the-connections"></a><span data-ttu-id="4d63f-282">8단계 - 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="4d63f-282">Step 8 - Create the connections</span></span>

<span data-ttu-id="4d63f-283">이 예제에서는 게이트웨이가 다른 구독에 있기 때문에 이 단계를 [구독 1] 및 [구독 5]로 표시된 두 개의 PowerShell 세션으로 분할했습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-283">In this example, because the gateways are in the different subscriptions, we've split this step into two PowerShell sessions marked as [Subscription 1] and [Subscription 5].</span></span>

1. <span data-ttu-id="4d63f-284">**[구독 1]** 구독 1에 대한 가상 네트워크 게이트웨이 가져오기.</span><span class="sxs-lookup"><span data-stu-id="4d63f-284">**[Subscription 1]** Get the virtual network gateway for Subscription 1.</span></span> <span data-ttu-id="4d63f-285">다음 예제를 실행하기 전에 로그인하고 구독 1에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-285">Log in and connect to Subscription 1 before running the following example:</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  <span data-ttu-id="4d63f-286">다음 요소의 출력을 복사하고 전자 메일 또는 다른 방법을 통해 구독 5의 관리자에게 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-286">Copy the output of the following elements and send these to the administrator of Subscription 5 via email or another method.</span></span>

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  <span data-ttu-id="4d63f-287">이 두 요소는 다음 예제 출력과 유사한 값을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-287">These two elements will have values similar to the following example output:</span></span>

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. <span data-ttu-id="4d63f-288">**[구독 5]** 구독 5에 대한 가상 네트워크 게이트웨이 가져오기.</span><span class="sxs-lookup"><span data-stu-id="4d63f-288">**[Subscription 5]** Get the virtual network gateway for Subscription 5.</span></span> <span data-ttu-id="4d63f-289">다음 예제를 실행하기 전에 로그인하고 구독 5에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-289">Log in and connect to Subscription 5 before running the following example:</span></span>

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  <span data-ttu-id="4d63f-290">다음 요소의 출력을 복사하고 전자 메일 또는 다른 방법을 통해 구독 1의 관리자에게 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-290">Copy the output of the following elements and send these to the administrator of Subscription 1 via email or another method.</span></span>

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  <span data-ttu-id="4d63f-291">이 두 요소는 다음 예제 출력과 유사한 값을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-291">These two elements will have values similar to the following example output:</span></span>

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. <span data-ttu-id="4d63f-292">**[구독 1]** TestVNet1에서 TestVNet5에 연결 만들기.</span><span class="sxs-lookup"><span data-stu-id="4d63f-292">**[Subscription 1]** Create the TestVNet1 to TestVNet5 connection.</span></span> <span data-ttu-id="4d63f-293">이 단계에서는 TestVNet1에서 TestVNet5까지 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-293">In this step, you create the connection from TestVNet1 to TestVNet5.</span></span> <span data-ttu-id="4d63f-294">여기서 차이점은 $vnet5gw가 다른 구독에 있기 때문에 직접 가져올 수 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-294">The difference here is that $vnet5gw cannot be obtained directly because it is in a different subscription.</span></span> <span data-ttu-id="4d63f-295">위의 단계에서 구독 1에서 전달한 값을 사용하여 새 PowerShell 개체를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-295">You will need to create a new PowerShell object with the values communicated from Subscription 1 in the steps above.</span></span> <span data-ttu-id="4d63f-296">아래 예제를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="4d63f-296">Use the example below.</span></span> <span data-ttu-id="4d63f-297">이름, ID 및 공유 키를 사용자의 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-297">Replace the Name, Id, and shared key with your own values.</span></span> <span data-ttu-id="4d63f-298">중요한 점은 두 연결에서 모두 공유 키가 일치해야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-298">The important thing is that the shared key must match for both connections.</span></span> <span data-ttu-id="4d63f-299">연결 만들기는 완료하는 데 꽤 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-299">Creating a connection can take a short while to complete.</span></span>

  <span data-ttu-id="4d63f-300">다음 예제를 실행하기 전에 구독 1에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-300">Connect to Subscription 1 before running the following example:</span></span>

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="4d63f-301">**[구독 5]** TestVNet5에서 TestVNet1에 연결 만들기.</span><span class="sxs-lookup"><span data-stu-id="4d63f-301">**[Subscription 5]** Create the TestVNet5 to TestVNet1 connection.</span></span> <span data-ttu-id="4d63f-302">이 단계는 TestVNet5에서 TestVNet1까지 연결을 만드는 점을 제외하면 위의 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-302">This step is similar to the one above, except you are creating the connection from TestVNet5 to TestVNet1.</span></span> <span data-ttu-id="4d63f-303">구독 1에서 가져온 값을 기반으로 PowerShell 개체를 만드는 동일한 과정이 여기에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-303">The same process of creating a PowerShell object based on the values obtained from Subscription 1 applies here as well.</span></span> <span data-ttu-id="4d63f-304">이 단계에서는 공유된 키가 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-304">In this step, be sure that the shared keys match.</span></span>

  <span data-ttu-id="4d63f-305">다음 예제를 실행하기 전에 구독 5에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-305">Connect to Subscription 5 before running the following example:</span></span>

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <span data-ttu-id="4d63f-306"><a name="verify"></a>연결을 확인하는 방법</span><span class="sxs-lookup"><span data-stu-id="4d63f-306"><a name="verify"></a>How to verify a connection</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="4d63f-307"><a name="faq"></a>VNet 간 FAQ</span><span class="sxs-lookup"><span data-stu-id="4d63f-307"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="4d63f-308">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4d63f-308">Next steps</span></span>

* <span data-ttu-id="4d63f-309">연결이 완료되면 가상 네트워크에 가상 컴퓨터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d63f-309">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="4d63f-310">자세한 내용은 [Virtual Machines 설명서](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d63f-310">See the [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) for more information.</span></span>
* <span data-ttu-id="4d63f-311">BGP에 대한 내용은 [BGP 개요](vpn-gateway-bgp-overview.md) 및 [BGP를 구성하는 방법](vpn-gateway-bgp-resource-manager-ps.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d63f-311">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>