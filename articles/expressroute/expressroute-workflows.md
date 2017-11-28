---
title: "ExpressRoute 회로 구성 하기 위한 aaaWorkflows | Microsoft Docs"
description: "이 페이지에서는 express 경로 회로 및 피어 링 구성 하기 위한 hello 워크플로 통해"
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
ms.openlocfilehash: 8e1dfc137401e0d6d53608ae6c8de0085e182eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a><span data-ttu-id="07b26-103">회로에 대한 Express 경로 워크플로 프로비전 및 회로 상태</span><span class="sxs-lookup"><span data-stu-id="07b26-103">ExpressRoute workflows for circuit provisioning and circuit states</span></span>
<span data-ttu-id="07b26-104">이 페이지에서는 hello 서비스 프로 비전 하 고 상위 수준에서 라우팅 구성 워크플로 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-104">This page walks you through hello service provisioning and routing configuration workflows at a high level.</span></span>

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

<span data-ttu-id="07b26-105">hello 다음 그림과 해당 단계 hello 작업 표시는 express 경로 회로 프로 비전 된 최종 간 순서 toohave에 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-105">hello following figure and corresponding steps show hello tasks you must follow in order toohave an ExpressRoute circuit provisioned end-to-end.</span></span> 

1. <span data-ttu-id="07b26-106">PowerShell tooconfigure ExpressRoute 회로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-106">Use PowerShell tooconfigure an ExpressRoute circuit.</span></span> <span data-ttu-id="07b26-107">Hello에 hello 지침에 따라 [만들 ExpressRoute 회로](expressroute-howto-circuit-classic.md) 을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="07b26-107">Follow hello instructions in hello [Create ExpressRoute circuits](expressroute-howto-circuit-classic.md) article for more details.</span></span>
2. <span data-ttu-id="07b26-108">Hello 서비스 공급자에서 연결을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-108">Order connectivity from hello service provider.</span></span> <span data-ttu-id="07b26-109">이 프로세스는 다양합니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-109">This process varies.</span></span> <span data-ttu-id="07b26-110">방법에 대 한 자세한 내용은 연결 공급자에 게 문의 tooorder 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-110">Contact your connectivity provider for more details about how tooorder connectivity.</span></span>
3. <span data-ttu-id="07b26-111">hello 회로가 프로 비전 되어 성공적으로 프로 비전 상태 PowerShell 통해 hello ExpressRoute 회로 확인 하 여 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-111">Ensure that hello circuit has been provisioned successfully by verifying hello ExpressRoute circuit provisioning state through PowerShell.</span></span> 
4. <span data-ttu-id="07b26-112">라우팅 도메인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-112">Configure routing domains.</span></span> <span data-ttu-id="07b26-113">연결 공급자가 사용자를 위해 3계층을 관리하는 경우 회로에 라우팅을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-113">If your connectivity provider manages Layer 3 for you, they will configure routing for your circuit.</span></span> <span data-ttu-id="07b26-114">연결 공급자 계층 2 서비스 제공을 구성 해야 hello에 설명 된 지침 당 라우팅 [라우팅 요구 사항](expressroute-routing.md) 및 [라우팅 구성을](expressroute-howto-routing-classic.md) 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-114">If your connectivity provider only offers Layer 2 services, you must configure routing per guidelines described in hello [routing requirements](expressroute-routing.md) and [routing configuration](expressroute-howto-routing-classic.md) pages.</span></span>
   
   * <span data-ttu-id="07b26-115">Azure 개인 피어 링을 사용 하도록 설정-클라우드 내 가상 네트워크에 배포 된 서비스 / 피어 링이 tooconnect tooVMs를 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-115">Enable Azure private peering - You must enable this peering tooconnect tooVMs / cloud services deployed within virtual networks.</span></span>
   * <span data-ttu-id="07b26-116">Azure 공용 피어 링-공용 IP 주소에 호스팅된 tooconnect tooAzure 서비스 하려는 경우 Azure 공용 피어 링 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-116">Enable Azure public peering - You must enable Azure public peering if you wish tooconnect tooAzure services hosted on public IP addresses.</span></span> <span data-ttu-id="07b26-117">Azure 개인 피어 링 용 tooenable 기본 라우팅 선택한 경우 요구 사항 tooaccess Azure 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-117">This is a requirement tooaccess Azure resources if you have chosen tooenable default routing for Azure private peering.</span></span>
   * <span data-ttu-id="07b26-118">Microsoft 피어 링-사용이 tooaccess Office 365, Dynamics 365 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-118">Enable Microsoft peering - You must enable this tooaccess Office 365 and Dynamics 365.</span></span> 
     
     > [!IMPORTANT]
     > <span data-ttu-id="07b26-119">별도 프록시를 사용 하 여 / 가장자리 tooconnect tooMicrosoft hello에 사용할 하나 보다 hello 인터넷 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-119">You must ensure that you use a separate proxy / edge tooconnect tooMicrosoft than hello one you use for hello Internet.</span></span> <span data-ttu-id="07b26-120">ExpressRoute와 인터넷 hello에 대 한 동일한 가장자리 비대칭 라우팅 되며 네트워크에 대 한 연결 중단을 일으킬 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-120">Using hello same edge for both ExpressRoute and hello Internet will cause asymmetric routing and cause connectivity outages for your network.</span></span>
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. <span data-ttu-id="07b26-121">연결 가상 네트워크를 회로 tooExpressRoute-가상 네트워크 tooyour ExpressRoute 회로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-121">Linking virtual networks tooExpressRoute circuits - You can link virtual networks tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="07b26-122">지침에 따라 [toolink Vnet](expressroute-howto-linkvnet-arm.md) tooyour 회로 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-122">Follow instructions [toolink VNets](expressroute-howto-linkvnet-arm.md) tooyour circuit.</span></span> <span data-ttu-id="07b26-123">이러한 Vnet 수 hello hello ExpressRoute 회로와 동일한 Azure 구독 또는 다른 구독에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-123">These VNets can either be in hello same Azure subscription as hello ExpressRoute circuit, or can be in a different subscription.</span></span>

## <a name="expressroute-circuit-provisioning-states"></a><span data-ttu-id="07b26-124">Express 경로 회로 상태 프로비전</span><span class="sxs-lookup"><span data-stu-id="07b26-124">ExpressRoute circuit provisioning states</span></span>
<span data-ttu-id="07b26-125">각 Express 경로 회로에는 두 가지 상태가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-125">Each ExpressRoute circuit has two states:</span></span>

* <span data-ttu-id="07b26-126">서비스 공급자 프로비전 상태</span><span class="sxs-lookup"><span data-stu-id="07b26-126">Service provider provisioning state</span></span>
* <span data-ttu-id="07b26-127">가동 상태</span><span class="sxs-lookup"><span data-stu-id="07b26-127">Status</span></span>

<span data-ttu-id="07b26-128">상태는 Microsoft의 프로비전 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-128">Status represents Microsoft's provisioning state.</span></span> <span data-ttu-id="07b26-129">이 속성은 tooEnabled Expressroute 회로 만들 때</span><span class="sxs-lookup"><span data-stu-id="07b26-129">This property is set tooEnabled when you create an Expressroute circuit</span></span>

<span data-ttu-id="07b26-130">hello 연결 공급자에 대 한 프로 비전 상태가 hello 연결 공급자 측 hello 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-130">hello connectivity provider provisioning state represents hello state on hello connectivity provider's side.</span></span> <span data-ttu-id="07b26-131">*프로비전되지 않음*, *프로비전 중* 또는 *프로비전됨*일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-131">It can either be *NotProvisioned*, *Provisioning*, or *Provisioned*.</span></span> <span data-ttu-id="07b26-132">hello ExpressRoute 회로에 있어야 하면 toobe 수 toouse에 대 한 프로 비전 됨 상태 것 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-132">hello ExpressRoute circuit must be in Provisioned state for you toobe able toouse it.</span></span>

### <a name="possible-states-of-an-expressroute-circuit"></a><span data-ttu-id="07b26-133">Express 경로 회로의 가능한 상태</span><span class="sxs-lookup"><span data-stu-id="07b26-133">Possible states of an ExpressRoute circuit</span></span>
<span data-ttu-id="07b26-134">이 섹션 아웃 ExpressRoute 회로 대 한 hello 가능한 상태를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-134">This section lists out hello possible states for an ExpressRoute circuit.</span></span>

<span data-ttu-id="07b26-135">**만드는 경우**</span><span class="sxs-lookup"><span data-stu-id="07b26-135">**At creation time**</span></span>

<span data-ttu-id="07b26-136">Hello PowerShell cmdlet toocreate hello ExpressRoute 회로 실행 상태를 그 다음 hello에 hello ExpressRoute 회로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-136">You will see hello ExpressRoute circuit in hello following state as soon as you run hello PowerShell cmdlet toocreate hello ExpressRoute circuit.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="07b26-137">**연결 공급자 hello 프로세스 hello 회로 프로 비전 된 경우**</span><span class="sxs-lookup"><span data-stu-id="07b26-137">**When connectivity provider is in hello process of provisioning hello circuit**</span></span>

<span data-ttu-id="07b26-138">ExpressRoute 회로 hello 상태를 그 다음에 hello hello 서비스 키 toohello 연결 공급자를 전달 합니다. 표시 되 고 hello를 프로 비전 프로세스 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-138">You will see hello ExpressRoute circuit in hello following state as soon as you pass hello service key toohello connectivity provider and they have started hello provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


<span data-ttu-id="07b26-139">**연결 공급자 hello를 프로 비전 프로세스가 완료 되 면**</span><span class="sxs-lookup"><span data-stu-id="07b26-139">**When connectivity provider has completed hello provisioning process**</span></span>

<span data-ttu-id="07b26-140">나타납니다 hello ExpressRoute 회로 hello hello 연결 공급자 hello를 프로 비전 프로세스를 완료 하는 즉시 상태 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-140">You will see hello ExpressRoute circuit in hello following state as soon as hello connectivity provider has completed hello provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

<span data-ttu-id="07b26-141">프로 비전 하 고 사용할 수는 hello 상태 hello 회로 가능에서 있습니다 toobe 수 toouse에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-141">Provisioned and Enabled is hello only state hello circuit can be in for you toobe able toouse it.</span></span> <span data-ttu-id="07b26-142">2계층 공급자를 사용하는 경우 이 상태인 경우 회로에 라우팅을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-142">If you are using a Layer 2 provider, you can configure routing for your circuit only when it is in this state.</span></span>

<span data-ttu-id="07b26-143">**연결 공급자 hello 회로가 프로 비전 해제 되는 경우**</span><span class="sxs-lookup"><span data-stu-id="07b26-143">**When connectivity provider is deprovisioning hello circuit**</span></span>

<span data-ttu-id="07b26-144">Hello 서비스 공급자 toodeprovision hello ExpressRoute 회로 요청한 경우 hello 회로 서비스 공급자 hello hello 프로세스를 프로 비전 해제를 완료 된 후 상태를 다음 toohello 설정 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-144">If you requested hello service provider toodeprovision hello ExpressRoute circuit, you will see hello circuit set toohello following state after hello service provider has completed hello deprovisioning process.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="07b26-145">Toore 기능을 사용 하도록 선택할 수 필요에 따라 또는 toodelete hello 회로 PowerShell cmdlet을 실행 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="07b26-145">You can choose toore-enable it if needed, or run PowerShell cmdlets toodelete hello circuit.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="07b26-146">실행 하는 경우에 hello hello ServiceProviderProvisioningState는 프로 비전 또는 프로 비전 됨 hello 작업 하는 경우 PowerShell cmdlet toodelete hello 회로 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-146">If you run hello PowerShell cmdlet toodelete hello circuit when hello ServiceProviderProvisioningState is Provisioning or Provisioned hello operation will fail.</span></span> <span data-ttu-id="07b26-147">먼저 연결 공급자 toodeprovision hello ExpressRoute 회로와 협력 하세요 하 고 hello 회로 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-147">Please work with your connectivity provider toodeprovision hello ExpressRoute circuit first and then delete hello circuit.</span></span> <span data-ttu-id="07b26-148">Microsoft는 hello PowerShell cmdlet toodelete hello 회로 실행할 때까지 toobill hello 회로 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-148">Microsoft will continue toobill hello circuit until you run hello PowerShell cmdlet toodelete hello circuit.</span></span>
> 
> 

## <a name="routing-session-configuration-state"></a><span data-ttu-id="07b26-149">라우팅 세션 구성 상태</span><span class="sxs-lookup"><span data-stu-id="07b26-149">Routing session configuration state</span></span>
<span data-ttu-id="07b26-150">hello BGP 프로 비전 상태를 사용 하면 Microsoft edge hello에서 hello BGP 세션을 사용 하는지 여부를 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-150">hello BGP provisioning state lets you know if hello BGP session has been enabled on hello Microsoft edge.</span></span> <span data-ttu-id="07b26-151">hello 상태를 설정 해야 하면 toobe 수 toouse hello 피어 링입니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-151">hello state must be enabled for you toobe able toouse hello peering.</span></span>

<span data-ttu-id="07b26-152">Microsoft 피어 링에 대 한 특히 중요 한 toocheck hello BGP 세션 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-152">It is important toocheck hello BGP session state especially for Microsoft peering.</span></span> <span data-ttu-id="07b26-153">또한 toohello BGP 프로 비전 상태에 라는 다른 상태 *공용 접두사 상태 보급*합니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-153">In addition toohello BGP provisioning state, there is another state called *advertised public prefixes state*.</span></span> <span data-ttu-id="07b26-154">hello 공용 접두사 상태에 있어야 합니다. 보급 *구성* 모두 사용자 라우팅 toowork에 종단 간 및를 BGP 세션 toobe hello에 대 한 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-154">hello advertised public prefixes state must be in *configured* state, both for hello BGP session toobe up and for your routing toowork end-to-end.</span></span> 

<span data-ttu-id="07b26-155">Hello 공용 접두사 상태는 tooa 설정 알린 경우 *필요한 유효성 검사* 상태 이면 hello BGP 세션을 설정 하지 않으면 hello 알리는 접두사 hello와 일치 하지 않습니다 hello 라우팅 레지스트리 중 하나에 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-155">If hello advertised public prefix state is set tooa *validation needed* state, hello BGP session is not enabled, as hello advertised prefixes did not match hello AS number in any of hello routing registries.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="07b26-156">Hello 상태 공용 접두사를 보급 하는 경우에 *수동 유효성 검사* 상태 이면 지원 티켓을 열어야 [Microsoft 지원](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) hello IP 주소를 따라 보급을 소유 하 고 있는 증거를 제공 하 고 hello로 익명 시스템 번호를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-156">If hello advertised public prefixes state is in *manual validation* state, you must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and provide evidence that you own hello IP addresses advertised along with hello associated Autonomous System number.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="07b26-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="07b26-157">Next steps</span></span>
* <span data-ttu-id="07b26-158">Express 경로 연결을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="07b26-158">Configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="07b26-159">ExpressRoute 회로 만들기</span><span class="sxs-lookup"><span data-stu-id="07b26-159">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-arm.md)
  * [<span data-ttu-id="07b26-160">라우팅 구성</span><span class="sxs-lookup"><span data-stu-id="07b26-160">Configure routing</span></span>](expressroute-howto-routing-arm.md)
  * [<span data-ttu-id="07b26-161">VNet tooan ExpressRoute 회로 연결</span><span class="sxs-lookup"><span data-stu-id="07b26-161">Link a VNet tooan ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

