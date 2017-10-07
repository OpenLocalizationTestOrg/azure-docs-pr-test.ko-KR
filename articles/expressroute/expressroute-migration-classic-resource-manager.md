---
title: "클래식 tooResource 관리자에서에서 express 경로 연결 된 가상 네트워크 마이그레이션: Azure: PowerShell | Microsoft Docs"
description: "이 페이지에서는 toomigrate 회로 이동한 후 가상 네트워크 tooResource 관리자에 연결 하는 방법을 설명 합니다."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: e64506c6909296f98c5dd23b1437bc0b81f31c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-expressroute-associated-virtual-networks-from-classic-tooresource-manager"></a><span data-ttu-id="cff95-103">클래식 tooResource 관리자에서에서 express 경로 연결 된 가상 네트워크 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="cff95-103">Migrate ExpressRoute associated virtual networks from classic tooResource Manager</span></span>

<span data-ttu-id="cff95-104">이 문서에서는 toomigrate Azure ExpressRoute ExpressRoute 회로 이동한 후 hello 클래식 배포 모델 toohello Azure 리소스 관리자 배포 모델에서 가상 네트워크에 연결 하는 방식에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-104">This article explains how toomigrate Azure ExpressRoute associated virtual networks from hello classic deployment model toohello Azure Resource Manager deployment model after moving your ExpressRoute circuit.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="cff95-105">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="cff95-105">Before you begin</span></span>
* <span data-ttu-id="cff95-106">Hello Azure PowerShell 모듈의 최신 버전 hello 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-106">Verify that you have hello latest version of hello Azure PowerShell modules.</span></span> <span data-ttu-id="cff95-107">자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-107">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="cff95-108">Hello 검토 했는지 확인 [필수 구성 요소](expressroute-prerequisites.md), [라우팅 요구 사항](expressroute-routing.md), 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="cff95-108">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="cff95-109">제공 하는 hello 정보를 검토 [클래식 tooResource 관리자에서에서 ExpressRoute 회로 이동](expressroute-move.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-109">Review hello information that is provided under [Moving an ExpressRoute circuit from classic tooResource Manager](expressroute-move.md).</span></span> <span data-ttu-id="cff95-110">완전히 이해 하는 hello 제한 및 제한 사항이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-110">Make sure that you fully understand hello limits and limitations.</span></span>
* <span data-ttu-id="cff95-111">Hello 회로 hello 클래식 배포 모델에서 완전 하 게 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-111">Verify that hello circuit is fully operational in hello classic deployment model.</span></span>
* <span data-ttu-id="cff95-112">Hello 리소스 관리자 배포 모델에서 만든 리소스 그룹 가졌는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-112">Ensure that you have a resource group that was created in hello Resource Manager deployment model.</span></span>
* <span data-ttu-id="cff95-113">Hello 리소스 마이그레이션 설명서를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-113">Review hello following resource-migration documentation:</span></span>

    * [<span data-ttu-id="cff95-114">클래식 tooAzure 리소스 관리자에서에서 IaaS 리소스의 마이그레이션 플랫폼 지원</span><span class="sxs-lookup"><span data-stu-id="cff95-114">Platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [<span data-ttu-id="cff95-115">클래식 tooAzure 리소스 관리자에서에서 마이그레이션 플랫폼 지원에 기술 심층 분석</span><span class="sxs-lookup"><span data-stu-id="cff95-115">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
    * [<span data-ttu-id="cff95-116">클래식 tooAzure 리소스 관리자에서에서 IaaS 리소스의 플랫폼에서 지 원하는 마이그레이션 Faq:</span><span class="sxs-lookup"><span data-stu-id="cff95-116">FAQs: Platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [<span data-ttu-id="cff95-117">가장 일반적인 마이그레이션 오류 및 완화 방법 검토</span><span class="sxs-lookup"><span data-stu-id="cff95-117">Review most common migration errors and mitigations</span></span>](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="supported-and-unsupported-scenarios"></a><span data-ttu-id="cff95-118">지원되는 및 지원되지 않는 시나리오</span><span class="sxs-lookup"><span data-stu-id="cff95-118">Supported and unsupported scenarios</span></span>

* <span data-ttu-id="cff95-119">ExpressRoute 회로 중단 시간 없이 hello 클래식 toohello 리소스 관리자 환경에서 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-119">An ExpressRoute circuit can be moved from hello classic toohello Resource Manager environment without any downtime.</span></span> <span data-ttu-id="cff95-120">Hello 클래식 toohello 중단 시간 없이 리소스 관리자 환경에서에서 모든 ExpressRoute 회로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-120">You can move any ExpressRoute circuit from hello classic toohello Resource Manager environment with no downtime.</span></span> <span data-ttu-id="cff95-121">Hello 지침에 따라 [PowerShell을 사용 하 여 hello 클래식 toohello 리소스 관리자 배포 모델에서 ExpressRoute 회로 이동](expressroute-howto-move-arm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-121">Follow hello instructions in [moving ExpressRoute circuits from hello classic toohello Resource Manager deployment model using PowerShell](expressroute-howto-move-arm.md).</span></span> <span data-ttu-id="cff95-122">이 필수 구성 요소 toomove 리소스 toohello 연결 된 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-122">This is a prerequisite toomove resources connected toohello virtual network.</span></span>
* <span data-ttu-id="cff95-123">가상 네트워크, 게이트웨이 및 연결 된 배포 hello 가상 네트워크 내에서 연결 된 tooan hello 동일한 구독 수의 ExpressRoute 회로 중단 시간 없이 toohello 리소스 관리자 환경이 마이그레이션됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-123">Virtual networks, gateways, and associated deployments within hello virtual network that are attached tooan ExpressRoute circuit in hello same subscription can be migrated toohello Resource Manager environment without any downtime.</span></span> <span data-ttu-id="cff95-124">Hello 단계 설명된 이후 toomigrate 주고받는 가상 네트워크, 게이트웨이 및 hello 가상 네트워크 내에서 배포 된 가상 컴퓨터를 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-124">You can follow hello steps described later toomigrate resources such as virtual networks, gateways, and virtual machines deployed within hello virtual network.</span></span> <span data-ttu-id="cff95-125">마이그레이션된 전에 hello 가상 네트워크가 올바르게 구성 되어 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-125">You must ensure that hello virtual networks are configured correctly before they are migrated.</span></span> 
* <span data-ttu-id="cff95-126">가상 네트워크, 게이트웨이 및 hello에 없는 가상 네트워크 내에서 관련된 배포가 hello hello ExpressRoute 회로는 일부 가동 중지 시간 toocomplete hello 마이그레이션 필요에 따라 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-126">Virtual networks, gateways, and associated deployments within hello virtual network that are not in hello same subscription as hello ExpressRoute circuit require some downtime toocomplete hello migration.</span></span> <span data-ttu-id="cff95-127">hello 문서의 마지막 섹션 hello hello 단계 뒤에 toobe toomigrate 리소스에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-127">hello last section of hello document describes hello steps toobe followed toomigrate resources.</span></span>
* <span data-ttu-id="cff95-128">ExpressRoute 게이트웨이와 VPN Gateway가 모두 있는 가상 네트워크는 마이그레이션할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-128">A virtual network with both ExpressRoute Gateway and VPN Gateway can't be migrated.</span></span>

## <a name="move-an-expressroute-circuit-from-classic-tooresource-manager"></a><span data-ttu-id="cff95-129">클래식 tooResource 관리자에서에서 ExpressRoute 회로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-129">Move an ExpressRoute circuit from classic tooResource Manager</span></span>
<span data-ttu-id="cff95-130">Hello 클래식 toohello toomigrate 리소스를 시도 하기 전에 리소스 관리자 환경에서에서 ExpressRoute 회로 연결 toohello ExpressRoute 회로 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-130">You must move an ExpressRoute circuit from hello classic toohello Resource Manager environment before you try toomigrate resources that are attached toohello ExpressRoute circuit.</span></span> <span data-ttu-id="cff95-131">tooaccomplish 작업이 hello 다음 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="cff95-131">tooaccomplish this task, see hello following articles:</span></span>

* <span data-ttu-id="cff95-132">제공 하는 hello 정보를 검토 [클래식 tooResource 관리자에서에서 ExpressRoute 회로 이동](expressroute-move.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-132">Review hello information that is provided under [Moving an ExpressRoute circuit from classic tooResource Manager](expressroute-move.md).</span></span>
* <span data-ttu-id="cff95-133">[클래식 tooResource Azure PowerShell을 사용 하 여 관리자에서에서 회로 이동](expressroute-howto-move-arm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-133">[Move a circuit from classic tooResource Manager using Azure PowerShell](expressroute-howto-move-arm.md).</span></span>
* <span data-ttu-id="cff95-134">Hello Azure 서비스 관리 포털을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-134">Use hello Azure Service Management portal.</span></span> <span data-ttu-id="cff95-135">너무 hello 워크플로 따를 수[새 ExpressRoute 회로 만들기](expressroute-howto-circuit-portal-resource-manager.md) hello 가져오기 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-135">You can follow hello workflow too[create a new ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and select hello import option.</span></span> 

<span data-ttu-id="cff95-136">이 작업에는 가동 중지 시간이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-136">This operation does not involve downtime.</span></span> <span data-ttu-id="cff95-137">Hello 마이그레이션이 진행 중인 동안 프레미스와 Microsoft 간에 tootransfer 데이터를 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-137">You can continue tootransfer data between your premises and Microsoft while hello migration is in progress.</span></span>

## <a name="migrate-virtual-networks-gateways-and-associated-deployments"></a><span data-ttu-id="cff95-138">가상 네트워크, 게이트웨이 및 연결된 배포 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="cff95-138">Migrate virtual networks, gateways, and associated deployments</span></span>

<span data-ttu-id="cff95-139">hello toomigrate 수행 단계에 종속 hello에 리소스가 있는 여부 동일한 구독, 서로 다른 구독 또는 둘 다 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-139">hello steps you follow toomigrate depend on whether your resources are in hello same subscription, different subscriptions, or both.</span></span>

### <a name="migrate-virtual-networks-gateways-and-associated-deployments-in-hello-same-subscription-as-hello-expressroute-circuit"></a><span data-ttu-id="cff95-140">대로 hello ExpressRoute 회로에 연결 된 배포 hello 동일한 구독 및 가상 네트워크 게이트웨이 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="cff95-140">Migrate virtual networks, gateways, and associated deployments in hello same subscription as hello ExpressRoute circuit</span></span>
<span data-ttu-id="cff95-141">이 섹션에서는 hello 단계 뒤에 toobe toomigrate 설명 가상 네트워크, 게이트웨이 및 연결 된 배포에 동일한 구독으로 ExpressRoute 회로 hello hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-141">This section describes hello steps toobe followed toomigrate a virtual network, gateway, and associated deployments in hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="cff95-142">이 마이그레이션은 가동 중지 시간이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-142">No downtime is associated with this migration.</span></span> <span data-ttu-id="cff95-143">Toouse hello 마이그레이션 프로세스를 통해 모든 리소스를 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-143">You can continue toouse all resources through hello migration process.</span></span> <span data-ttu-id="cff95-144">hello 관리 평면 hello 마이그레이션이 진행 중인 동안 잠겨 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-144">hello management plane is locked while hello migration is in progress.</span></span> 

1. <span data-ttu-id="cff95-145">Hello ExpressRoute 회로 hello 클래식 toohello 리소스 관리자 환경에서 옮겨 졌음을 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-145">Ensure that hello ExpressRoute circuit has been moved from hello classic toohello Resource Manager environment.</span></span>
2. <span data-ttu-id="cff95-146">Hello 마이그레이션에 대 한 hello 가상 네트워크 적절 하 게 준비 된 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-146">Ensure that hello virtual network has been prepared appropriately for hello migration.</span></span>
3. <span data-ttu-id="cff95-147">리소스 마이그레이션을 위해 구독을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-147">Register your subscription for resource migration.</span></span> <span data-ttu-id="cff95-148">tooregister 리소스 마이그레이션-다음 PowerShell 코드 조각을 사용 하 여 hello에 대 한 구독:</span><span class="sxs-lookup"><span data-stu-id="cff95-148">tooregister your subscription for resource migration, use hello following PowerShell snippet:</span></span>

  ```powershell 
  Select-AzureRmSubscription -SubscriptionName <Your Subscription Name>
  Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  ```
4. <span data-ttu-id="cff95-149">유효성을 검사하고 준비한 후, 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-149">Validate, prepare, and migrate.</span></span> <span data-ttu-id="cff95-150">toomove hello 가상 네트워크, 다음 PowerShell 코드 조각을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="cff95-150">toomove hello virtual network, use hello following PowerShell snippet:</span></span>

  ```powershell
  Move-AzureVirtualNetwork -Prepare $vnetName  
  Move-AzureVirtualNetwork -Commit $vnetName
  ```

  <span data-ttu-id="cff95-151">또한 hello 다음 PowerShell cmdlet을 실행 하 여 마이그레이션을 중단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff95-151">You can also abort migration by running hello following PowerShell cmdlet:</span></span>

  ```powershell
  Move-AzureVirtualNetwork -Abort $vnetName
  ```

## <a name="next-steps"></a><span data-ttu-id="cff95-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cff95-152">Next steps</span></span>
* [<span data-ttu-id="cff95-153">클래식 tooAzure 리소스 관리자에서에서 IaaS 리소스의 마이그레이션 플랫폼 지원</span><span class="sxs-lookup"><span data-stu-id="cff95-153">Platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [<span data-ttu-id="cff95-154">클래식 tooAzure 리소스 관리자에서에서 마이그레이션 플랫폼 지원에 기술 심층 분석</span><span class="sxs-lookup"><span data-stu-id="cff95-154">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
* [<span data-ttu-id="cff95-155">클래식 tooAzure 리소스 관리자에서에서 IaaS 리소스의 플랫폼에서 지 원하는 마이그레이션 Faq:</span><span class="sxs-lookup"><span data-stu-id="cff95-155">FAQs: Platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [<span data-ttu-id="cff95-156">가장 일반적인 마이그레이션 오류 및 완화 방법 검토</span><span class="sxs-lookup"><span data-stu-id="cff95-156">Review most common migration errors and mitigations</span></span>](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
