---
title: "가상 네트워크 tooanother VNet 연결: Azure CLI | Microsoft Docs"
description: "이 문서에서는 Azure Resource Manager 및 Azure CLI를 사용하여 가상 네트워크를 함께 연결하는 과정을 안내합니다."
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
ms.openlocfilehash: 70113914bcae03c80f9ad133ff081d1cf37fc309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a><span data-ttu-id="64f5c-103">Azure CLI를 사용하여 VNet 간 VPN 게이트웨이 연결 구성</span><span class="sxs-lookup"><span data-stu-id="64f5c-103">Configure a VNet-to-VNet VPN gateway connection using Azure CLI</span></span>

<span data-ttu-id="64f5c-104">이 문서에서는 어떻게 toocreate 가상 네트워크 간의 VPN 게이트웨이 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-104">This article shows you how toocreate a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="64f5c-105">hello 가상 네트워크 수 같거나 다른 지역 hello와에서 동일 hello 또는 서로 다른 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-105">hello virtual networks can be in hello same or different regions, and from hello same or different subscriptions.</span></span> <span data-ttu-id="64f5c-106">Hello 구독이 다른 구독에서 연결 Vnet toobe hello와 관련 된 필요 하지 않는 경우 동일한 Active Directory 테 넌 트.</span><span class="sxs-lookup"><span data-stu-id="64f5c-106">When connecting VNets from different subscriptions, hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> 

<span data-ttu-id="64f5c-107">이 문서의 단계 hello toohello 리소스 관리자 배포 모델을 적용 하 고 Azure CLI를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-107">hello steps in this article apply toohello Resource Manager deployment model and use Azure CLI.</span></span> <span data-ttu-id="64f5c-108">또한 서로 다른 배포 도구 또는 배포 모델을 사용 하 여 hello 다음 목록에서에서 다른 옵션을 선택 하 여이 구성을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="64f5c-109">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="64f5c-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="64f5c-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="64f5c-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="64f5c-111">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="64f5c-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="64f5c-112">Azure Portal(클래식)</span><span class="sxs-lookup"><span data-stu-id="64f5c-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="64f5c-113">다양한 배포 모델 간 연결 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="64f5c-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="64f5c-114">다양한 배포 모델 간 연결 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="64f5c-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="64f5c-115">가상 네트워크 tooanother 가상 네트워크 (VNet 대 VNet) 연결 하는 유사한 tooconnecting VNet tooan 온-프레미스 사이트 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-115">Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="64f5c-116">두 연결 유형에서는 VPN 게이트웨이 tooprovide IPsec/IKE를 사용 하 여 보안 터널을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-116">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="64f5c-117">Vnet hello에 있는 경우 동일한 지역 VNet 피어 링을 사용 하 여 연결 tooconsider 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-117">If your VNets are in hello same region, you may want tooconsider connecting them using VNet Peering.</span></span> <span data-ttu-id="64f5c-118">VNet 피어링은 VPN Gateway를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="64f5c-119">자세한 내용은 [VNet 피어링](../virtual-network/virtual-network-peering-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="64f5c-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="64f5c-120">VNet-VNet 통신을 다중 사이트 구성과 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="64f5c-121">이렇게 하면 hello 다음 다이어그램에에서 나와 있는 것 처럼 가상 네트워크 간 연결 되 면 크로스-프레미스 연결을 결합 하는 네트워크 토폴로지를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in hello following diagram:</span></span>

![연결 정보](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <span data-ttu-id="64f5c-123"><a name="why"></a>가상 네트워크에 연결하는 이유</span><span class="sxs-lookup"><span data-stu-id="64f5c-123"><a name="why"></a>Why connect virtual networks?</span></span>

<span data-ttu-id="64f5c-124">다음 이유로 hello에 대 한 tooconnect 가상 네트워크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-124">You may want tooconnect virtual networks for hello following reasons:</span></span>

* <span data-ttu-id="64f5c-125">**지역 간 지리적 중복 및 지리적 상태**</span><span class="sxs-lookup"><span data-stu-id="64f5c-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="64f5c-126">인터넷 연결 끝점으로 이동하지 않고도 보안 연결을 통해 지역에서 복제 또는 동기화를 직접 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="64f5c-127">Azure Traffic Manager 및 부하 분산 장치를 사용하여 여러 Azure 지역 간의 지리적 중복을 통해 워크로드의 가용성을 높게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="64f5c-128">한 가지 중요 한 예는 SQL Always On 가용성 그룹이 여러 Azure 지역에 분산을 tooset 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-128">One important example is tooset up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="64f5c-129">**분리 또는 관리 경계를 가진 지역별 다중 계층 응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="64f5c-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="64f5c-130">내 동일한 hello 영역을 설정할 수 있습니다 다층 계층 응용 프로그램 기한 tooisolation 또는 관리 요구를 함께 연결 하는 여러 가상 네트워크가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-130">Within hello same region, you can set up multi-tier applications with multiple virtual networks connected together due tooisolation or administrative requirements.</span></span>

<span data-ttu-id="64f5c-131">VNet 대 VNet 연결에 대 한 자세한 내용은 참조 hello [VNet 대 VNet FAQ](#faq) hello이이 문서의 뒷부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-131">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span>

### <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="64f5c-132">어느 단계 집합을 사용해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="64f5c-132">Which set of steps should I use?</span></span>

<span data-ttu-id="64f5c-133">이 문서에서는 서로 다른 두 집합의 단계를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="64f5c-134">일련의 절차에 대 한 [Vnet에 상주 하는 동일한 구독 hello](#samesub), 용이고 다른 하나는 [서로 다른 구독에 있는 Vnet](#difsub)합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-134">One set of steps for [VNets that reside in hello same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span>

## <span data-ttu-id="64f5c-135"><a name="samesub"></a>Hello에 있는 Vnet 연결 동일한 구독</span><span class="sxs-lookup"><span data-stu-id="64f5c-135"><a name="samesub"></a>Connect VNets that are in hello same subscription</span></span>

![v2v 다이어그램](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="64f5c-137">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="64f5c-137">Before you begin</span></span>

<span data-ttu-id="64f5c-138">시작 하기 전에 hello hello CLI 명령 (2.0 이상)의 최신 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-138">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="64f5c-139">Hello CLI 명령 설치에 대 한 정보를 참조 하십시오. [Azure CLI 2.0 설치](/cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-139">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

### <span data-ttu-id="64f5c-140"><a name="Plan"></a>IP 주소 범위 계획</span><span class="sxs-lookup"><span data-stu-id="64f5c-140"><a name="Plan"></a>Plan your IP address ranges</span></span>

<span data-ttu-id="64f5c-141">다음 단계는 hello, 두 가상 네트워크와 해당 게이트웨이 서브넷 및 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-141">In hello following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="64f5c-142">Hello 간의 VPN 연결이 두 Vnet 다음 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-142">We then create a VPN connection between hello two VNets.</span></span> <span data-ttu-id="64f5c-143">네트워크 구성에 대 한 중요 한 tooplan hello IP 주소 범위는</span><span class="sxs-lookup"><span data-stu-id="64f5c-143">It’s important tooplan hello IP address ranges for your network configuration.</span></span> <span data-ttu-id="64f5c-144">따라서 VNet 범위 또는 로컬 네트워크 범위가 겹치지 않는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-144">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="64f5c-145">이 예에서는 DNS 서버를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-145">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="64f5c-146">가상 네트워크의 이름 확인을 원하는 경우 [이름 확인](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="64f5c-146">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="64f5c-147">다음 hello 예제에는 값에는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-147">We use hello following values in hello examples:</span></span>

<span data-ttu-id="64f5c-148">**TestVNet1에 대한 값:**</span><span class="sxs-lookup"><span data-stu-id="64f5c-148">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="64f5c-149">VNet 이름: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="64f5c-149">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="64f5c-150">리소스 그룹: TestRG1</span><span class="sxs-lookup"><span data-stu-id="64f5c-150">Resource Group: TestRG1</span></span>
* <span data-ttu-id="64f5c-151">위치: 미국 동부</span><span class="sxs-lookup"><span data-stu-id="64f5c-151">Location: East US</span></span>
* <span data-ttu-id="64f5c-152">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="64f5c-152">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="64f5c-153">프런트 엔드: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="64f5c-153">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="64f5c-154">백 엔드: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="64f5c-154">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="64f5c-155">게이트웨이 서브넷 = 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="64f5c-155">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="64f5c-156">게이트웨이 이름: VNet1GW</span><span class="sxs-lookup"><span data-stu-id="64f5c-156">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="64f5c-157">공용 IP: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="64f5c-157">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="64f5c-158">VpnType: 경로 기반</span><span class="sxs-lookup"><span data-stu-id="64f5c-158">VPNType: RouteBased</span></span>
* <span data-ttu-id="64f5c-159">연결(1 대 4): VNet1 대 VNet4</span><span class="sxs-lookup"><span data-stu-id="64f5c-159">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="64f5c-160">연결(1 대 5): VNet1 대 VNet5</span><span class="sxs-lookup"><span data-stu-id="64f5c-160">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="64f5c-161">연결 유형: VNet 간</span><span class="sxs-lookup"><span data-stu-id="64f5c-161">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="64f5c-162">**TestVNet4에 대한 값:**</span><span class="sxs-lookup"><span data-stu-id="64f5c-162">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="64f5c-163">VNet 이름: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="64f5c-163">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="64f5c-164">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="64f5c-164">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="64f5c-165">프런트 엔드: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="64f5c-165">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="64f5c-166">백 엔드: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="64f5c-166">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="64f5c-167">게이트웨이 서브넷: 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="64f5c-167">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="64f5c-168">리소스 그룹: TestRG4</span><span class="sxs-lookup"><span data-stu-id="64f5c-168">Resource Group: TestRG4</span></span>
* <span data-ttu-id="64f5c-169">위치: 미국 서부</span><span class="sxs-lookup"><span data-stu-id="64f5c-169">Location: West US</span></span>
* <span data-ttu-id="64f5c-170">게이트웨이 이름: VNet4GW</span><span class="sxs-lookup"><span data-stu-id="64f5c-170">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="64f5c-171">공용 IP: VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="64f5c-171">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="64f5c-172">VpnType: 경로 기반</span><span class="sxs-lookup"><span data-stu-id="64f5c-172">VPNType: RouteBased</span></span>
* <span data-ttu-id="64f5c-173">연결: VNet4 대 VNet1</span><span class="sxs-lookup"><span data-stu-id="64f5c-173">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="64f5c-174">연결 유형: VNet 간</span><span class="sxs-lookup"><span data-stu-id="64f5c-174">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="64f5c-175"><a name="Connect"></a>1 단계-tooyour 구독 연결</span><span class="sxs-lookup"><span data-stu-id="64f5c-175"><a name="Connect"></a>Step 1 - Connect tooyour subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <span data-ttu-id="64f5c-176"><a name="TestVNet1"></a>2단계 - TestVNet1 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="64f5c-176"><a name="TestVNet1"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="64f5c-177">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-177">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. <span data-ttu-id="64f5c-178">TestVNet1 용 TestVNet1 및 hello 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-178">Create TestVNet1 and hello subnets for TestVNet1.</span></span> <span data-ttu-id="64f5c-179">이 예제에서는 TestVNet1이라는 가상 네트워크와 FrontEnd라는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-179">This example creates a virtual network named TestVNet1 and a subnet named FrontEnd.</span></span>

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. <span data-ttu-id="64f5c-180">Hello 백 엔드 서브넷에 대 한 추가 주소 공간을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-180">Create an additional address space for hello backend subnet.</span></span> <span data-ttu-id="64f5c-181">이 단계에서는 앞에서 만든 두 hello 주소 공간을 지정 하 고 hello tooadd 한다고 추가 주소 공간을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-181">Notice that in this step, we specify both hello address space that we created earlier, and hello additional address space that we want tooadd.</span></span> <span data-ttu-id="64f5c-182">때문에 이것이 hello [az 네트워크 vnet 업데이트](https://docs.microsoft.com/cli/azure/network/vnet#update) hello 이전 설정을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-182">This is because hello [az network vnet update](https://docs.microsoft.com/cli/azure/network/vnet#update) command overwrites hello previous settings.</span></span> <span data-ttu-id="64f5c-183">모든 확인 하십시오 있는지 toospecify hello 주소 접두사의이 명령을 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="64f5c-183">Make sure toospecify all of hello address prefixes when using this command.</span></span>

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. <span data-ttu-id="64f5c-184">Hello 백 엔드 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-184">Create hello backend subnet.</span></span>
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. <span data-ttu-id="64f5c-185">Hello 게이트웨이 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-185">Create hello gateway subnet.</span></span> <span data-ttu-id="64f5c-186">Hello 게이트웨이 서브넷은 이라는 '를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-186">Notice that hello gateway subnet is named 'GatewaySubnet'.</span></span> <span data-ttu-id="64f5c-187">이 이름은 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-187">This name is required.</span></span> <span data-ttu-id="64f5c-188">이 예제에서는 hello 게이트웨이 서브넷에 / 27을 사용 중입니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-188">In this example, hello gateway subnet is using a /27.</span></span> <span data-ttu-id="64f5c-189">가능한 toocreate/29 수신자로 게이트웨이 서브넷 이지만, 적어도/28 또는/27 선택 하 여 더 많은 주소를 포함 하는 큰 서브넷을 만들어야 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-189">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="64f5c-190">이렇게 하면 충분 한 주소 tooaccommodate 가능한 추가 되는 구성에 만한 hello 이후 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-190">This will allow for enough addresses tooaccommodate possible additional configurations that you may want in hello future.</span></span>

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. <span data-ttu-id="64f5c-191">공용 IP 주소 toobe 할당 된 toohello 게이트웨이 만들려는 VNet에 대 한 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-191">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="64f5c-192">해당 hello AllocationMethod 동적 점에 유의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="64f5c-192">Notice that hello AllocationMethod is Dynamic.</span></span> <span data-ttu-id="64f5c-193">원하는 toouse hello IP 주소를 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-193">You cannot specify hello IP address that you want toouse.</span></span> <span data-ttu-id="64f5c-194">그는 동적으로 할당 된 tooyour 게이트웨이입니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-194">It's dynamically allocated tooyour gateway.</span></span>

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. <span data-ttu-id="64f5c-195">TestVNet1에 대 한 hello 가상 네트워크 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-195">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="64f5c-196">VNet-VNet 구성에는 RouteBased VpnType이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-196">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="64f5c-197">'대기 없음-' 매개 변수 hello를 사용 하 여이 명령을 실행 하면 피드백이 나 출력에 표시 되지 않으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-197">If you run this command using hello '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="64f5c-198">hello '대기 없음-' 매개 변수는 hello 게이트웨이 toocreate hello 백그라운드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-198">hello '--no-wait' parameter allows hello gateway toocreate in hello background.</span></span> <span data-ttu-id="64f5c-199">해당 hello VPN 게이트웨이 즉시 만들기를 완료 것을 의미 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-199">It does not mean that hello VPN gateway finishes creating immediately.</span></span> <span data-ttu-id="64f5c-200">한 게이트웨이 만드는 45 분에 따라 이상 hello 게이트웨이 SKU 있습니다를 사용 하는 종종 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-200">Creating a gateway can often take 45 minutes or more, depending on hello gateway SKU that you use.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="64f5c-201"><a name="TestVNet4"></a>3단계 - TestVNet4 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="64f5c-201"><a name="TestVNet4"></a>Step 3 - Create and configure TestVNet4</span></span>

1. <span data-ttu-id="64f5c-202">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-202">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. <span data-ttu-id="64f5c-203">TestVNet4 만들기.</span><span class="sxs-lookup"><span data-stu-id="64f5c-203">Create TestVNet4.</span></span>

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. <span data-ttu-id="64f5c-204">TestVNet4의 추가 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-204">Create additional subnets for TestVNet4.</span></span>

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. <span data-ttu-id="64f5c-205">Hello 게이트웨이 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-205">Create hello gateway subnet.</span></span>

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. <span data-ttu-id="64f5c-206">공용 IP 주소를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-206">Request a Public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. <span data-ttu-id="64f5c-207">Hello TestVNet4 가상 네트워크 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-207">Create hello TestVNet4 virtual network gateway.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="64f5c-208"><a name="createconnect"></a>4 단계-hello 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="64f5c-208"><a name="createconnect"></a>Step 4 - Create hello connections</span></span>

<span data-ttu-id="64f5c-209">이제 VPN 게이트웨이가 있는 VNet이 두 개 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-209">You now have two VNets with VPN gateways.</span></span> <span data-ttu-id="64f5c-210">hello 다음 단계는 hello 가상 네트워크 게이트웨이 간에 VPN 게이트웨이 연결을 toocreate입니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-210">hello next step is toocreate VPN gateway connections between hello virtual network gateways.</span></span> <span data-ttu-id="64f5c-211">위의 hello 예제를 사용 하는 경우 VNet 게이트웨이 다른 리소스 그룹에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-211">If you used hello examples above, your VNet gateways are in different resource groups.</span></span> <span data-ttu-id="64f5c-212">게이트웨이 다른 리소스 그룹에서을 tooidentify 필요 하 고 연결할 때 각 게이트웨이에 대 한 hello 리소스 Id를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-212">When gateways are in different resource groups, you need tooidentify and specify hello resource IDs for each gateway when making a connection.</span></span> <span data-ttu-id="64f5c-213">Vnet hello에 있는 경우 동일한 리소스 그룹 hello를 사용할 수 있습니다 [명령의 두 번째 집합](#samerg) toospecify hello 리소스 Id는 필요 하지 않으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-213">If your VNets are in hello same resource group, you can use hello [second set of instructions](#samerg) because you don't need toospecify hello resource IDs.</span></span>

### <span data-ttu-id="64f5c-214"><a name="diffrg"></a>다른 리소스 그룹에 상주 하는 Vnet tooconnect</span><span class="sxs-lookup"><span data-stu-id="64f5c-214"><a name="diffrg"></a>tooconnect VNets that reside in different resource groups</span></span>

1. <span data-ttu-id="64f5c-215">다음 명령을 hello의 hello 출력에서 hello를 VNet1GW의 리소스 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-215">Get hello Resource ID of VNet1GW from hello output of hello following command:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="64f5c-216">찾을 hello hello 출력에 "id:" 줄.</span><span class="sxs-lookup"><span data-stu-id="64f5c-216">In hello output, find hello "id:" line.</span></span> <span data-ttu-id="64f5c-217">hello 따옴표 안에 hello 값 hello 다음 섹션에서 필요한 toocreate hello 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-217">hello values within hello quotes are needed toocreate hello connection in hello next section.</span></span> <span data-ttu-id="64f5c-218">쉽게 붙여 넣을 수 있습니다 하 여 연결을 만들 때 이러한 값 tooa 텍스트 편집기, 메모장과 같은 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-218">Copy these values tooa text editor, such as Notepad, so that you can easily paste them when creating your connection.</span></span>

  <span data-ttu-id="64f5c-219">예제 출력:</span><span class="sxs-lookup"><span data-stu-id="64f5c-219">Example output:</span></span>

  ```
  "activeActive": false, 
  "bgpSettings": { 
    "asn": 65515, 
    "bgpPeeringAddress": "10.12.255.30", 
    "peerWeight": 0 
   }, 
  "enableBgp": false, 
  "etag": "W/\"ecb42bc5-c176-44e1-802f-b0ce2962ac04\"", 
  "gatewayDefaultSite": null, 
  "gatewayType": "Vpn", 
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW", 
  "ipConfigurations":
  ```

  <span data-ttu-id="64f5c-220">복사 후 hello 값 **"id":** hello 따옴표 안에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-220">Copy hello values after **"id":** within hello quotes.</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. <span data-ttu-id="64f5c-221">Hello VNet4GW의 리소스 ID 및 복사 hello 값 tooa 텍스트 편집기를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-221">Get hello Resource ID of VNet4GW and copy hello values tooa text editor.</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. <span data-ttu-id="64f5c-222">Hello TestVNet1 tooTestVNet4 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-222">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="64f5c-223">이 단계에서 TestVNet1 tooTestVNet4 hello 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-223">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="64f5c-224">Hello 예제에서 참조 하는 공유 키 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-224">There is a shared key referenced in hello examples.</span></span> <span data-ttu-id="64f5c-225">Hello 공유 키에 대 한 사용자 지정 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-225">You can use your own values for hello shared key.</span></span> <span data-ttu-id="64f5c-226">두 연결에 대 한 중요 한 점은 그 hello 공유 키 hello 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-226">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="64f5c-227">연결을 만드는 데 toocomplete 잠시 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-227">Creating a connection takes a short while toocomplete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. <span data-ttu-id="64f5c-228">Hello TestVNet4 tooTestVNet1 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-228">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="64f5c-229">이 단계에서 TestVNet4 tooTestVNet1 hello 연결을 만드는 점을 제외 하 고 위에 나온 비슷한 toohello 것입니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-229">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="64f5c-230">Hello 공유 키와 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-230">Make sure hello shared keys match.</span></span> <span data-ttu-id="64f5c-231">몇 분 tooestablish hello 연결을 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-231">It takes a few minutes tooestablish hello connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. <span data-ttu-id="64f5c-232">연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-232">Verify your connections.</span></span> <span data-ttu-id="64f5c-233">[연결 확인](#verify)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="64f5c-233">See [Verify your connection](#verify).</span></span>

### <span data-ttu-id="64f5c-234"><a name="samerg"></a>tooconnect Vnet 동일 hello에 상주 하는 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="64f5c-234"><a name="samerg"></a>tooconnect VNets that reside in hello same resource group</span></span>

1. <span data-ttu-id="64f5c-235">Hello TestVNet1 tooTestVNet4 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-235">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="64f5c-236">이 단계에서 TestVNet1 tooTestVNet4 hello 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-236">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="64f5c-237">공지 hello 리소스 그룹 hello 예제에서 동일한 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-237">Notice hello resource groups are hello same in hello examples.</span></span> <span data-ttu-id="64f5c-238">Hello 예제에서 참조 하는 공유 키를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-238">You also see a shared key referenced in hello examples.</span></span> <span data-ttu-id="64f5c-239">하지만 Hello 공유 키에 대 한 사용자 지정 값을 사용할 수 있는데, 두 연결에 대 한 hello 공유 키와 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-239">You can use your own values for hello shared key, however, hello shared key must match for both connections.</span></span> <span data-ttu-id="64f5c-240">연결을 만드는 데 toocomplete 잠시 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-240">Creating a connection takes a short while toocomplete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. <span data-ttu-id="64f5c-241">Hello TestVNet4 tooTestVNet1 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-241">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="64f5c-242">이 단계에서 TestVNet4 tooTestVNet1 hello 연결을 만드는 점을 제외 하 고 위에 나온 비슷한 toohello 것입니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-242">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="64f5c-243">Hello 공유 키와 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-243">Make sure hello shared keys match.</span></span> <span data-ttu-id="64f5c-244">몇 분 tooestablish hello 연결을 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-244">It takes a few minutes tooestablish hello connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. <span data-ttu-id="64f5c-245">연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-245">Verify your connections.</span></span> <span data-ttu-id="64f5c-246">[연결 확인](#verify)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="64f5c-246">See [Verify your connection](#verify).</span></span>

## <span data-ttu-id="64f5c-247"><a name="difsub"></a>다른 구독에 있는 VNet 연결</span><span class="sxs-lookup"><span data-stu-id="64f5c-247"><a name="difsub"></a>Connect VNets that are in different subscriptions</span></span>

![v2v 다이어그램](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

<span data-ttu-id="64f5c-249">이 시나리오에서는 TestVNet1 및 TestVNet5를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-249">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="64f5c-250">hello Vnet에 서로 다른 구독 상주 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-250">hello VNets reside different subscriptions.</span></span> <span data-ttu-id="64f5c-251">hello 구독 hello와 관련 된 toobe 불필요 동일한 Active Directory 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-251">hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> <span data-ttu-id="64f5c-252">이 구성에 대 한 hello 단계 순서 tooconnect TestVNet1 tooTestVNet5에에서 대 한 추가 VNet 대 VNet 연결을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-252">hello steps for this configuration add an additional VNet-to-VNet connection in order tooconnect TestVNet1 tooTestVNet5.</span></span>

### <span data-ttu-id="64f5c-253"><a name="TestVNet1diff"></a>5단계 - TestVNet1 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="64f5c-253"><a name="TestVNet1diff"></a>Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="64f5c-254">이러한 지침은 hello 이전 섹션의에서 hello 단계에서 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-254">These instructions continue from hello steps in hello preceding sections.</span></span> <span data-ttu-id="64f5c-255">완료 해야 [1 단계](#Connect) 및 [2 단계](#TestVNet1) toocreate TestVNet1를 구성 하 고 TestVNet1에 대 한 VPN 게이트웨이 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-255">You must complete [Step 1](#Connect) and [Step 2](#TestVNet1) toocreate and configure TestVNet1 and hello VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="64f5c-256">이 구성에 대 한 하지 않으므로 필요한 toocreate TestVNet4 hello 이전 섹션에서 다음이 단계와 충돌을 만들지 않는 경우 하지 않지만.</span><span class="sxs-lookup"><span data-stu-id="64f5c-256">For this configuration, you are not required toocreate TestVNet4 from hello previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="64f5c-257">1단계와 2단계를 완료하면 6단계(아래)를 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-257">Once you complete Step 1 and Step 2, continue with Step 6 (below).</span></span>

### <span data-ttu-id="64f5c-258"><a name="verifyranges"></a>6 단계-hello IP 주소 범위를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-258"><a name="verifyranges"></a>Step 6 - Verify hello IP address ranges</span></span>

<span data-ttu-id="64f5c-259">추가 연결을 만들 때 중요 한 tooverify hello 새 가상 네트워크의 IP 주소 공간을 hello 다른 VNet 범위 또는 로컬 네트워크 게이트웨이 범위와 겹치지 않는 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-259">When creating additional connections, it's important tooverify that hello IP address space of hello new virtual network does not overlap with any of your other VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="64f5c-260">이 연습에서는 다음 TestVNet5 hello에 대 한 값에는 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-260">For this exercise, you can use hello following values for hello TestVNet5:</span></span>

<span data-ttu-id="64f5c-261">**TestVNet5에 대한 값:**</span><span class="sxs-lookup"><span data-stu-id="64f5c-261">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="64f5c-262">VNet 이름: TestVNet5</span><span class="sxs-lookup"><span data-stu-id="64f5c-262">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="64f5c-263">리소스 그룹: TestRG5</span><span class="sxs-lookup"><span data-stu-id="64f5c-263">Resource Group: TestRG5</span></span>
* <span data-ttu-id="64f5c-264">위치: 일본 동부</span><span class="sxs-lookup"><span data-stu-id="64f5c-264">Location: Japan East</span></span>
* <span data-ttu-id="64f5c-265">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="64f5c-265">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="64f5c-266">프런트 엔드: 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="64f5c-266">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="64f5c-267">백 엔드: 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="64f5c-267">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="64f5c-268">게이트웨이 서브넷: 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="64f5c-268">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="64f5c-269">게이트웨이 이름: VNet5GW</span><span class="sxs-lookup"><span data-stu-id="64f5c-269">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="64f5c-270">공용 IP: VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="64f5c-270">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="64f5c-271">VpnType: 경로 기반</span><span class="sxs-lookup"><span data-stu-id="64f5c-271">VPNType: RouteBased</span></span>
* <span data-ttu-id="64f5c-272">연결: VNet5 대 VNet1</span><span class="sxs-lookup"><span data-stu-id="64f5c-272">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="64f5c-273">연결 유형: VNet 간</span><span class="sxs-lookup"><span data-stu-id="64f5c-273">ConnectionType: VNet2VNet</span></span>

### <span data-ttu-id="64f5c-274"><a name="TestVNet5"></a>7단계 - TestVNet5 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="64f5c-274"><a name="TestVNet5"></a>Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="64f5c-275">이 단계는 hello 새 구독을 구독 5의 hello 컨텍스트에서 수행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-275">This step must be done in hello context of hello new subscription, Subscription 5.</span></span> <span data-ttu-id="64f5c-276">Hello 구독을 소유 하는 다른 조직의 관리자에 게가이 부분을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-276">This part may be performed by hello administrator in a different organization that owns hello subscription.</span></span> <span data-ttu-id="64f5c-277">구독 사용 간의 tooswitch ' az 계정 목록-모든 ' toolist 구독 사용 가능한 tooyour 계정 hello 다음 사용 하 여 ' az 계정 세트-구독 <subscriptionID>' tooswitch toohello 구독 toouse 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-277">tooswitch between subscriptions use 'az account list --all' toolist hello subscriptions available tooyour account, then use 'az account set --subscription <subscriptionID>' tooswitch toohello subscription that you want toouse.</span></span>

1. <span data-ttu-id="64f5c-278">올바른지 확인 하는 연결 된 tooSubscription 5, 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-278">Make sure you are connected tooSubscription 5, then create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. <span data-ttu-id="64f5c-279">TestVNet5 만들기.</span><span class="sxs-lookup"><span data-stu-id="64f5c-279">Create TestVNet5.</span></span>

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. <span data-ttu-id="64f5c-280">서브넷을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-280">Add subnets.</span></span>

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. <span data-ttu-id="64f5c-281">Hello 게이트웨이 서브넷을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-281">Add hello gateway subnet.</span></span>

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. <span data-ttu-id="64f5c-282">공용 IP 주소를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-282">Request a public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. <span data-ttu-id="64f5c-283">Hello TestVNet5 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="64f5c-283">Create hello TestVNet5 gateway</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="64f5c-284"><a name="connections5"></a>8 단계-hello 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="64f5c-284"><a name="connections5"></a>Step 8 - Create hello connections</span></span>

<span data-ttu-id="64f5c-285">로 표시 하는 두 개의 CLI 세션에이 단계를 나눌 **[구독 1]**, 및 **[구독 5]** hello 게이트웨이 hello 서로 다른 구독에 있기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-285">We split this step into two CLI sessions marked as **[Subscription 1]**, and **[Subscription 5]** because hello gateways are in hello different subscriptions.</span></span> <span data-ttu-id="64f5c-286">구독 사용 간의 tooswitch ' az 계정 목록-모든 ' toolist 구독 사용 가능한 tooyour 계정 hello 다음 사용 하 여 ' az 계정 세트-구독 <subscriptionID>' tooswitch toohello 구독 toouse 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-286">tooswitch between subscriptions use 'az account list --all' toolist hello subscriptions available tooyour account, then use 'az account set --subscription <subscriptionID>' tooswitch toohello subscription that you want toouse.</span></span>

1. <span data-ttu-id="64f5c-287">**[1 구독]**  에 로그인 하 고 tooSubscription 1을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-287">**[Subscription 1]** Log in and connect tooSubscription 1.</span></span> <span data-ttu-id="64f5c-288">실행된 hello 다음 명령 hello hello 출력에서 게이트웨이의 tooget hello 이름 및 ID 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-288">Run hello following command tooget hello name and ID of hello Gateway from hello output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="64f5c-289">에 대 한 hello 출력 복사 "id:".</span><span class="sxs-lookup"><span data-stu-id="64f5c-289">Copy hello output for "id:".</span></span> <span data-ttu-id="64f5c-290">Hello ID 및 VNet 게이트웨이 (VNet1GW) toohello 관리자에 게 구독 5의 전자 메일 또는 다른 방법을 통해의 hello 이름을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-290">Send hello ID and hello name of hello VNet gateway (VNet1GW) toohello administrator of Subscription 5 via email or another method.</span></span>

  <span data-ttu-id="64f5c-291">예제 출력:</span><span class="sxs-lookup"><span data-stu-id="64f5c-291">Example output:</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. <span data-ttu-id="64f5c-292">**[구독 5]**  에 로그인 하 고 5 tooSubscription 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-292">**[Subscription 5]** Log in and connect tooSubscription 5.</span></span> <span data-ttu-id="64f5c-293">실행된 hello 다음 명령 hello hello 출력에서 게이트웨이의 tooget hello 이름 및 ID 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-293">Run hello following command tooget hello name and ID of hello Gateway from hello output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  <span data-ttu-id="64f5c-294">에 대 한 hello 출력 복사 "id:".</span><span class="sxs-lookup"><span data-stu-id="64f5c-294">Copy hello output for "id:".</span></span> <span data-ttu-id="64f5c-295">Hello ID 및 VNet 게이트웨이 (VNet5GW) toohello 관리자에 게 구독 1의 전자 메일 또는 다른 방법을 통해의 hello 이름을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-295">Send hello ID and hello name of hello VNet gateway (VNet5GW) toohello administrator of Subscription 1 via email or another method.</span></span>

3. <span data-ttu-id="64f5c-296">**[1 구독]**  이 단계에서 TestVNet1 tooTestVNet5 hello 연결 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-296">**[Subscription 1]** In this step, you create hello connection from TestVNet1 tooTestVNet5.</span></span> <span data-ttu-id="64f5c-297">하지만 Hello 공유 키에 대 한 사용자 지정 값을 사용할 수 있는데, 두 연결에 대 한 hello 공유 키와 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-297">You can use your own values for hello shared key, however, hello shared key must match for both connections.</span></span> <span data-ttu-id="64f5c-298">연결 만들기 toocomplete 잠시를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-298">Creating a connection can take a short while toocomplete.</span></span> <span data-ttu-id="64f5c-299">TooSubscription 1을 연결 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-299">Make sure you connect tooSubscription 1.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. <span data-ttu-id="64f5c-300">**[구독 5]**  TestVNet5 tooTestVNet1에서 hello 연결을 만드는 점을 제외 하 고이 단계는 위에 나온 toohello 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-300">**[Subscription 5]** This step is similar toohello one above, except you are creating hello connection from TestVNet5 tooTestVNet1.</span></span> <span data-ttu-id="64f5c-301">해당 hello 공유 키 일치 및 tooSubscription 5에 연결 해야 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-301">Make sure that hello shared keys match and that you connect tooSubscription 5.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <span data-ttu-id="64f5c-302"><a name="verify"></a>Hello 연결 되어 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="64f5c-302"><a name="verify"></a>Verify hello connections</span></span>
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <span data-ttu-id="64f5c-303"><a name="faq"></a>VNet 간 FAQ</span><span class="sxs-lookup"><span data-stu-id="64f5c-303"><a name="faq"></a>VNet-to-VNet FAQ</span></span>
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="64f5c-304">다음 단계</span><span class="sxs-lookup"><span data-stu-id="64f5c-304">Next steps</span></span>

* <span data-ttu-id="64f5c-305">연결이 완료 되 면 가상 컴퓨터 tooyour 가상 네트워크를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-305">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="64f5c-306">자세한 내용은 참조 hello [가상 컴퓨터 설명서](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-306">For more information, see hello [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="64f5c-307">BGP에 대 한 정보를 참조 hello [BGP 개요](vpn-gateway-bgp-overview.md) 및 [어떻게 tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="64f5c-307">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
