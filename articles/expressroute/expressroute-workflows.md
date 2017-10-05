---
title: "ExpressRoute로 회로를 구성하기 위한 워크플로 | Microsoft 문서"
description: "이 페이지는 Express 경로 회로 및 피어링을 구성하기 위한 워크플로를 안내합니다."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 55e0418c-e0bf-44a7-9aa1-720076df9297
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: cba1b2cfee379e7d2b079bcb3089981ef1044d66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a><span data-ttu-id="83f8c-103">회로에 대한 Express 경로 워크플로 프로비전 및 회로 상태</span><span class="sxs-lookup"><span data-stu-id="83f8c-103">ExpressRoute workflows for circuit provisioning and circuit states</span></span>
<span data-ttu-id="83f8c-104">이 페이지에서는 높은 수준에서 구성 워크플로 프로비전 및 라우팅 서비스를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-104">This page walks you through the service provisioning and routing configuration workflows at a high level.</span></span>

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

<span data-ttu-id="83f8c-105">다음 그림 및 해당 단계는 종단 간 프로비전된 Express 경로 회로를 보유하기 위해 수행해야 하는 작업을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-105">The following figure and corresponding steps show the tasks you must follow in order to have an ExpressRoute circuit provisioned end-to-end.</span></span> 

1. <span data-ttu-id="83f8c-106">PowerShell을 사용하여 Express 경로 회로를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-106">Use PowerShell to configure an ExpressRoute circuit.</span></span> <span data-ttu-id="83f8c-107">자세한 세부 사항은 [Express 경로 회로 만들기](expressroute-howto-circuit-classic.md) 문서의 지침을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-107">Follow the instructions in the [Create ExpressRoute circuits](expressroute-howto-circuit-classic.md) article for more details.</span></span>
2. <span data-ttu-id="83f8c-108">서비스 공급자에서 연결을 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-108">Order connectivity from the service provider.</span></span> <span data-ttu-id="83f8c-109">이 프로세스는 다양합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-109">This process varies.</span></span> <span data-ttu-id="83f8c-110">연결을 정렬하는 방법에 대한 자세한 내용은 연결 공급자에게 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-110">Contact your connectivity provider for more details about how to order connectivity.</span></span>
3. <span data-ttu-id="83f8c-111">PowerShell 통해 상태를 프로비전하는 Express 경로 회로를 확인하여 회로를 성공적으로 프로비전했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-111">Ensure that the circuit has been provisioned successfully by verifying the ExpressRoute circuit provisioning state through PowerShell.</span></span> 
4. <span data-ttu-id="83f8c-112">라우팅 도메인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-112">Configure routing domains.</span></span> <span data-ttu-id="83f8c-113">연결 공급자가 사용자를 위해 3계층을 관리하는 경우 회로에 라우팅을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-113">If your connectivity provider manages Layer 3 for you, they will configure routing for your circuit.</span></span> <span data-ttu-id="83f8c-114">연결 공급자가 2계층 서비스만을 제공하는 경우 [라우팅 요구 사항](expressroute-routing.md) 및 [라우팅 구성](expressroute-howto-routing-classic.md) 페이지에 설명된 지침에 따라 라우팅을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-114">If your connectivity provider only offers Layer 2 services, you must configure routing per guidelines described in the [routing requirements](expressroute-routing.md) and [routing configuration](expressroute-howto-routing-classic.md) pages.</span></span>
   
   * <span data-ttu-id="83f8c-115">Azure 개인 피어링 사용 - 이 피어링을 사용하여 가상 네트워크 내에 배포된 VM/클라우드 서비스에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-115">Enable Azure private peering - You must enable this peering to connect to VMs / cloud services deployed within virtual networks.</span></span>
   * <span data-ttu-id="83f8c-116">Azure 공용 피어링 사용 - 공용 IP 주소에 호스팅된 Azure 서비스에 연결하려는 경우 Azure 공용 피어링을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-116">Enable Azure public peering - You must enable Azure public peering if you wish to connect to Azure services hosted on public IP addresses.</span></span> <span data-ttu-id="83f8c-117">Azure 개인 피어링에 대한 기본 라우팅을 사용하도록 선택한 경우 Azure 리소스에 액세스하는 것이 요구됩니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-117">This is a requirement to access Azure resources if you have chosen to enable default routing for Azure private peering.</span></span>
   * <span data-ttu-id="83f8c-118">Microsoft 피어링 사용 - Office 365 및 Dynamics 365에 액세스하려면 이 기능을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-118">Enable Microsoft peering - You must enable this to access Office 365 and Dynamics 365.</span></span> 
     
     > [!IMPORTANT]
     > <span data-ttu-id="83f8c-119">인터넷에 사용하는 것 이외에 별도 프록시/Edge를 사용하여 Microsoft에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-119">You must ensure that you use a separate proxy / edge to connect to Microsoft than the one you use for the Internet.</span></span> <span data-ttu-id="83f8c-120">Express 경로 및 인터넷 모두에 동일한 Edge를 사용하면 비대칭 라우팅이 발생하고 네트워크에 대한 연결 중단이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-120">Using the same edge for both ExpressRoute and the Internet will cause asymmetric routing and cause connectivity outages for your network.</span></span>
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. <span data-ttu-id="83f8c-121">가상 네트워크를 Express 경로 회로에 연결 - 가상 네트워크를 Express 경로 회로에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-121">Linking virtual networks to ExpressRoute circuits - You can link virtual networks to your ExpressRoute circuit.</span></span> <span data-ttu-id="83f8c-122">지침을 수행하여 회로에 [VNet을 연결](expressroute-howto-linkvnet-arm.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-122">Follow instructions [to link VNets](expressroute-howto-linkvnet-arm.md) to your circuit.</span></span> <span data-ttu-id="83f8c-123">이러한 VNet은 Express 경로 회로로써 동일한 Azure 구독에 있거나 다른 구독에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-123">These VNets can either be in the same Azure subscription as the ExpressRoute circuit, or can be in a different subscription.</span></span>

## <a name="expressroute-circuit-provisioning-states"></a><span data-ttu-id="83f8c-124">Express 경로 회로 상태 프로비전</span><span class="sxs-lookup"><span data-stu-id="83f8c-124">ExpressRoute circuit provisioning states</span></span>
<span data-ttu-id="83f8c-125">각 Express 경로 회로에는 두 가지 상태가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-125">Each ExpressRoute circuit has two states:</span></span>

* <span data-ttu-id="83f8c-126">서비스 공급자 프로비전 상태</span><span class="sxs-lookup"><span data-stu-id="83f8c-126">Service provider provisioning state</span></span>
* <span data-ttu-id="83f8c-127">가동 상태</span><span class="sxs-lookup"><span data-stu-id="83f8c-127">Status</span></span>

<span data-ttu-id="83f8c-128">상태는 Microsoft의 프로비전 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-128">Status represents Microsoft's provisioning state.</span></span> <span data-ttu-id="83f8c-129">Express 경로 회로를 만들 때는 이 속성이 Enabled로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-129">This property is set to Enabled when you create an Expressroute circuit</span></span>

<span data-ttu-id="83f8c-130">연결 공급자 프로비전 상태는 연결 공급자 측의 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-130">The connectivity provider provisioning state represents the state on the connectivity provider's side.</span></span> <span data-ttu-id="83f8c-131">*프로비전되지 않음*, *프로비전 중* 또는 *프로비전됨*일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-131">It can either be *NotProvisioned*, *Provisioning*, or *Provisioned*.</span></span> <span data-ttu-id="83f8c-132">Express 경로 회로는 사용할 수 있도록 프로비전됨 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-132">The ExpressRoute circuit must be in Provisioned state for you to be able to use it.</span></span>

### <a name="possible-states-of-an-expressroute-circuit"></a><span data-ttu-id="83f8c-133">Express 경로 회로의 가능한 상태</span><span class="sxs-lookup"><span data-stu-id="83f8c-133">Possible states of an ExpressRoute circuit</span></span>
<span data-ttu-id="83f8c-134">이 섹션은 Express 경로 회로에 대해 가능한 상태를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-134">This section lists out the possible states for an ExpressRoute circuit.</span></span>

<span data-ttu-id="83f8c-135">**만드는 경우**</span><span class="sxs-lookup"><span data-stu-id="83f8c-135">**At creation time**</span></span>

<span data-ttu-id="83f8c-136">PowerShell cmdlet을 실행하여 Express 경로 회로를 만드는 즉시 다음 상태의 Express 경로 회로가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-136">You will see the ExpressRoute circuit in the following state as soon as you run the PowerShell cmdlet to create the ExpressRoute circuit.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="83f8c-137">**연결 공급자에서 회로를 프로비전하고 있는 경우**</span><span class="sxs-lookup"><span data-stu-id="83f8c-137">**When connectivity provider is in the process of provisioning the circuit**</span></span>

<span data-ttu-id="83f8c-138">연결 공급자에 서비스 키를 전달하고 프로비전 프로세스를 시작하는 즉시 다음 상태의 Express 경로 회로가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-138">You will see the ExpressRoute circuit in the following state as soon as you pass the service key to the connectivity provider and they have started the provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


<span data-ttu-id="83f8c-139">**연결 공급자에서 프로비전 프로세스를 완료한 경우**</span><span class="sxs-lookup"><span data-stu-id="83f8c-139">**When connectivity provider has completed the provisioning process**</span></span>

<span data-ttu-id="83f8c-140">연결 공급자가 프로비전 프로세스를 완료하는 즉시 다음 상태의 Express 경로 회로가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-140">You will see the ExpressRoute circuit in the following state as soon as the connectivity provider has completed the provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

<span data-ttu-id="83f8c-141">프로비전됨 및 사용은 회로를 사용할 수 있는 유일한 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-141">Provisioned and Enabled is the only state the circuit can be in for you to be able to use it.</span></span> <span data-ttu-id="83f8c-142">2계층 공급자를 사용하는 경우 이 상태인 경우 회로에 라우팅을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-142">If you are using a Layer 2 provider, you can configure routing for your circuit only when it is in this state.</span></span>

<span data-ttu-id="83f8c-143">**연결 공급자에서 회로 프로비전을 해제하는 경우**</span><span class="sxs-lookup"><span data-stu-id="83f8c-143">**When connectivity provider is deprovisioning the circuit**</span></span>

<span data-ttu-id="83f8c-144">서비스 공급자에게 Express 경로 회로 프로비전 해제를 요청한 경우 서비스 공급자가 프로비전 해제 프로세스를 완료하고 나면 회로가 다음 상태로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-144">If you requested the service provider to deprovision the ExpressRoute circuit, you will see the circuit set to the following state after the service provider has completed the deprovisioning process.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="83f8c-145">필요에 따라 PowerShell cmdlet을 다시 사용하거나 실행하여 회로를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-145">You can choose to re-enable it if needed, or run PowerShell cmdlets to delete the circuit.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="83f8c-146">ServiceProviderProvisioningState가 Provisioning 또는 Provisioned일 때 PowerShell cmdlet을 실행하여 회로를 삭제하면 작업이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-146">If you run the PowerShell cmdlet to delete the circuit when the ServiceProviderProvisioningState is Provisioning or Provisioned the operation will fail.</span></span> <span data-ttu-id="83f8c-147">이러한 경우에는 연결 공급자에게 요청하여 먼저 Express 경로 회로 프로비전을 해제한 후에 회로를 삭제하세요.</span><span class="sxs-lookup"><span data-stu-id="83f8c-147">Please work with your connectivity provider to deprovision the ExpressRoute circuit first and then delete the circuit.</span></span> <span data-ttu-id="83f8c-148">Microsoft는 PowerShell cmdlet을 실행하여 회로를 삭제할 때까지 회로에 요금을 계속 청구합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-148">Microsoft will continue to bill the circuit until you run the PowerShell cmdlet to delete the circuit.</span></span>
> 
> 

## <a name="routing-session-configuration-state"></a><span data-ttu-id="83f8c-149">라우팅 세션 구성 상태</span><span class="sxs-lookup"><span data-stu-id="83f8c-149">Routing session configuration state</span></span>
<span data-ttu-id="83f8c-150">BGP 프로비전 상태를 사용하면 Microsoft Edge에서 BGP 세션을 사용하는지를 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-150">The BGP provisioning state lets you know if the BGP session has been enabled on the Microsoft edge.</span></span> <span data-ttu-id="83f8c-151">상태는 피어링을 사용할 수 있도록 활성화되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-151">The state must be enabled for you to be able to use the peering.</span></span>

<span data-ttu-id="83f8c-152">특히 Microsoft 피어링의 경우 BGP 세션 상태를 확인하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-152">It is important to check the BGP session state especially for Microsoft peering.</span></span> <span data-ttu-id="83f8c-153">BGP 프로비전 상태 외에도 *보급된 공용 접두사 상태*를 호출하는 다른 상태가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-153">In addition to the BGP provisioning state, there is another state called *advertised public prefixes state*.</span></span> <span data-ttu-id="83f8c-154">BGP 세션이 가동되고 라우팅이 종단 간에 작동하기 위해 보급된 공용 접두사 상태는 *구성된* 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-154">The advertised public prefixes state must be in *configured* state, both for the BGP session to be up and for your routing to work end-to-end.</span></span> 

<span data-ttu-id="83f8c-155">보급된 공용 접두사 상태가 *유효성 검사가 필요한* 상태로 설정된 경우 보급된 접두사가 라우팅 레지스트리의의 AS 번호와 일치하지 않기 때문에 BGP 세션을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-155">If the advertised public prefix state is set to a *validation needed* state, the BGP session is not enabled, as the advertised prefixes did not match the AS number in any of the routing registries.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="83f8c-156">보급된 공용 접두사 상태가 *수동 유효성 검사* 상태인 경우 [Microsoft 지원](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) 으로 지원 티켓을 열고 사용자가 연관된 자치 시스템 번호와 함께 보급된 IP 주소를 소유한 증거를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-156">If the advertised public prefixes state is in *manual validation* state, you must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and provide evidence that you own the IP addresses advertised along with the associated Autonomous System number.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="83f8c-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="83f8c-157">Next steps</span></span>
* <span data-ttu-id="83f8c-158">Express 경로 연결을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="83f8c-158">Configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="83f8c-159">ExpressRoute 회로 만들기</span><span class="sxs-lookup"><span data-stu-id="83f8c-159">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-arm.md)
  * [<span data-ttu-id="83f8c-160">라우팅 구성</span><span class="sxs-lookup"><span data-stu-id="83f8c-160">Configure routing</span></span>](expressroute-howto-routing-arm.md)
  * [<span data-ttu-id="83f8c-161">VNet을 ExpressRoute 회로에 연결</span><span class="sxs-lookup"><span data-stu-id="83f8c-161">Link a VNet to an ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

