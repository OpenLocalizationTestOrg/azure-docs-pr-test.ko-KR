---
title: "클래식에서 Resource Manager로 ExpressRoute 연결된 가상 네트워크 마이그레이션: Azure: PowerShell | Microsoft Docs"
description: "이 페이지에서는 회로를 이동한 후에 Resource Manager로 연결된 가상 네트워크를 마이그레이션하는 방법을 설명합니다."
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
ms.openlocfilehash: 964ea38569062a7127f60dd6309b328db263bf6f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-expressroute-associated-virtual-networks-from-classic-to-resource-manager"></a><span data-ttu-id="aed2b-103">클래식에서 Resource Manager로 ExpressRoute 연결된 가상 네트워크 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="aed2b-103">Migrate ExpressRoute associated virtual networks from classic to Resource Manager</span></span>

<span data-ttu-id="aed2b-104">이 문서에서는 ExpressRoute 회로를 이동한 후에 클래식 배포 모델에서 Azure Resource Manager 배포 모델로 Azure ExpressRoute 연결된 가상 네트워크를 마이그레이션하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-104">This article explains how to migrate Azure ExpressRoute associated virtual networks from the classic deployment model to the Azure Resource Manager deployment model after moving your ExpressRoute circuit.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="aed2b-105">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="aed2b-105">Before you begin</span></span>
* <span data-ttu-id="aed2b-106">Azure PowerShell 모듈의 최신 버전이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-106">Verify that you have the latest version of the Azure PowerShell modules.</span></span> <span data-ttu-id="aed2b-107">자세한 내용은 [Azure PowerShell 설치 및 구성하는 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aed2b-107">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="aed2b-108">구성을 시작하기 전에 [필수 조건](expressroute-prerequisites.md), [라우팅 요구 사항](expressroute-routing.md) 및 [워크플로](expressroute-workflows.md)를 검토했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-108">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="aed2b-109">[클래식에서 Resource Manager로 ExpressRoute 회로 이동](expressroute-move.md)에서 제공되는 정보를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-109">Review the information that is provided under [Moving an ExpressRoute circuit from classic to Resource Manager](expressroute-move.md).</span></span> <span data-ttu-id="aed2b-110">제한 및 제한 사항을 완전히 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-110">Make sure that you fully understand the limits and limitations.</span></span>
* <span data-ttu-id="aed2b-111">클래식 배포 모델에서 회로가 완벽하게 작동되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-111">Verify that the circuit is fully operational in the classic deployment model.</span></span>
* <span data-ttu-id="aed2b-112">리소스 관리자 배포 모델에 만든 리소스 그룹이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-112">Ensure that you have a resource group that was created in the Resource Manager deployment model.</span></span>
* <span data-ttu-id="aed2b-113">다음 리소스 마이그레이션 설명서를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-113">Review the following resource-migration documentation:</span></span>

    * [<span data-ttu-id="aed2b-114">클래식에서 Azure Resource Manager로 IaaS 리소스의 플랫폼 지원 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="aed2b-114">Platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [<span data-ttu-id="aed2b-115">클래식에서 Azure Resource Manager로의 플랫폼 지원 마이그레이션에 대한 기술 정보</span><span class="sxs-lookup"><span data-stu-id="aed2b-115">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
    * [<span data-ttu-id="aed2b-116">FAQ: 클래식에서 Azure Resource Manager로 IaaS 리소스의 플랫폼 지원 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="aed2b-116">FAQs: Platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [<span data-ttu-id="aed2b-117">가장 일반적인 마이그레이션 오류 및 완화 방법 검토</span><span class="sxs-lookup"><span data-stu-id="aed2b-117">Review most common migration errors and mitigations</span></span>](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="supported-and-unsupported-scenarios"></a><span data-ttu-id="aed2b-118">지원되는 및 지원되지 않는 시나리오</span><span class="sxs-lookup"><span data-stu-id="aed2b-118">Supported and unsupported scenarios</span></span>

* <span data-ttu-id="aed2b-119">ExpressRoute 회로를 가동 중지 시간 없이 클래식에서 Resource Manager 환경으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-119">An ExpressRoute circuit can be moved from the classic to the Resource Manager environment without any downtime.</span></span> <span data-ttu-id="aed2b-120">ExpressRoute 회로를 클래식에서 Resource Manager 환경으로 가동 중지 시간 없이 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-120">You can move any ExpressRoute circuit from the classic to the Resource Manager environment with no downtime.</span></span> <span data-ttu-id="aed2b-121">[PowerShell을 사용하여 클래식에서 Resource Manager 배포 모델로 ExpressRoute 회로 이동](expressroute-howto-move-arm.md)의 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="aed2b-121">Follow the instructions in [moving ExpressRoute circuits from the classic to the Resource Manager deployment model using PowerShell](expressroute-howto-move-arm.md).</span></span> <span data-ttu-id="aed2b-122">가상 네트워크에 연결된 리소스를 이동하기 위한 필수 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-122">This is a prerequisite to move resources connected to the virtual network.</span></span>
* <span data-ttu-id="aed2b-123">동일한 구독에서 ExpressRoute 회로에 연결된 가상 네트워크, 게이트웨이 및 가상 네트워크 내 연결된 배포를 가동 중지 시간 없이 Resource Manager 환경으로 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-123">Virtual networks, gateways, and associated deployments within the virtual network that are attached to an ExpressRoute circuit in the same subscription can be migrated to the Resource Manager environment without any downtime.</span></span> <span data-ttu-id="aed2b-124">나중에 설명하는 단계에 따라 가상 네트워크, 게이트웨이 및 가상 네트워크 내 배포된 가상 컴퓨터와 같은 리소스를 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-124">You can follow the steps described later to migrate resources such as virtual networks, gateways, and virtual machines deployed within the virtual network.</span></span> <span data-ttu-id="aed2b-125">마이그레이션하기 전에 가상 네트워크가 올바르게 구성되어 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-125">You must ensure that the virtual networks are configured correctly before they are migrated.</span></span> 
* <span data-ttu-id="aed2b-126">ExpressRoute 회로와 다른 구독의 가상 네트워크, 게이트웨이 및 가상 네트워크 내 연결된 배포는 마이그레이션을 완료하는 데 가동 중지 시간이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-126">Virtual networks, gateways, and associated deployments within the virtual network that are not in the same subscription as the ExpressRoute circuit require some downtime to complete the migration.</span></span> <span data-ttu-id="aed2b-127">문서의 마지막 섹션에서는 리소스 마이그레이션을 위해 따라야 하는 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-127">The last section of the document describes the steps to be followed to migrate resources.</span></span>
* <span data-ttu-id="aed2b-128">ExpressRoute 게이트웨이와 VPN Gateway가 모두 있는 가상 네트워크는 마이그레이션할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-128">A virtual network with both ExpressRoute Gateway and VPN Gateway can't be migrated.</span></span>

## <a name="move-an-expressroute-circuit-from-classic-to-resource-manager"></a><span data-ttu-id="aed2b-129">클래식에서 Resource Manager로 ExpressRoute 회로 이동</span><span class="sxs-lookup"><span data-stu-id="aed2b-129">Move an ExpressRoute circuit from classic to Resource Manager</span></span>
<span data-ttu-id="aed2b-130">ExpressRoute 회로에 연결된 리소스를 마이그레이션하기 전에 ExpressRoute 회로를 클래식에서 Resource Manager 환경으로 이동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-130">You must move an ExpressRoute circuit from the classic to the Resource Manager environment before you try to migrate resources that are attached to the ExpressRoute circuit.</span></span> <span data-ttu-id="aed2b-131">이 작업을 완료하려면 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aed2b-131">To accomplish this task, see the following articles:</span></span>

* <span data-ttu-id="aed2b-132">[클래식에서 Resource Manager로 ExpressRoute 회로 이동](expressroute-move.md)에서 제공되는 정보를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-132">Review the information that is provided under [Moving an ExpressRoute circuit from classic to Resource Manager](expressroute-move.md).</span></span>
* <span data-ttu-id="aed2b-133">[Azure PowerShell을 사용하여 클래식에서 Resource Manager로 회로를 이동합니다](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="aed2b-133">[Move a circuit from classic to Resource Manager using Azure PowerShell](expressroute-howto-move-arm.md).</span></span>
* <span data-ttu-id="aed2b-134">Azure Service 관리 포털을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-134">Use the Azure Service Management portal.</span></span> <span data-ttu-id="aed2b-135">[새 ExpressRoute 회로 만들기](expressroute-howto-circuit-portal-resource-manager.md)에 대한 워크플로를 수행하고 가져오기 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-135">You can follow the workflow to [create a new ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and select the import option.</span></span> 

<span data-ttu-id="aed2b-136">이 작업에는 가동 중지 시간이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-136">This operation does not involve downtime.</span></span> <span data-ttu-id="aed2b-137">마이그레이션을 진행하는 동안 프레미스와 Microsoft 간 데이터 전송을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-137">You can continue to transfer data between your premises and Microsoft while the migration is in progress.</span></span>

## <a name="migrate-virtual-networks-gateways-and-associated-deployments"></a><span data-ttu-id="aed2b-138">가상 네트워크, 게이트웨이 및 연결된 배포 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="aed2b-138">Migrate virtual networks, gateways, and associated deployments</span></span>

<span data-ttu-id="aed2b-139">마이그레이션을 위해 수행하는 단계는 리소스가 동일한 구독에 있는지, 서로 다른 구독에 있는지 또는 둘 다에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-139">The steps you follow to migrate depend on whether your resources are in the same subscription, different subscriptions, or both.</span></span>

### <a name="migrate-virtual-networks-gateways-and-associated-deployments-in-the-same-subscription-as-the-expressroute-circuit"></a><span data-ttu-id="aed2b-140">ExpressRoute 회로와 동일한 구독의 가상 네트워크, 게이트웨이 및 연결된 배포 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="aed2b-140">Migrate virtual networks, gateways, and associated deployments in the same subscription as the ExpressRoute circuit</span></span>
<span data-ttu-id="aed2b-141">이 섹션에서는 ExpressRoute 회로와 동일한 구독의 가상 네트워크, 게이트웨이 및 연결된 배포를 배포하기 위한 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-141">This section describes the steps to be followed to migrate a virtual network, gateway, and associated deployments in the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="aed2b-142">이 마이그레이션은 가동 중지 시간이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-142">No downtime is associated with this migration.</span></span> <span data-ttu-id="aed2b-143">마이그레이션 프로세스 동안 모든 리소스를 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-143">You can continue to use all resources through the migration process.</span></span> <span data-ttu-id="aed2b-144">마이그레이션이 진행되는 동안에는 관리 평면이 잠겨 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-144">The management plane is locked while the migration is in progress.</span></span> 

1. <span data-ttu-id="aed2b-145">ExpressRoute 회로를 클래식에서 Resource Manager 환경으로 이동하였는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-145">Ensure that the ExpressRoute circuit has been moved from the classic to the Resource Manager environment.</span></span>
2. <span data-ttu-id="aed2b-146">가상 네트워크를 마이그레이션에 적합하게 준비하였는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-146">Ensure that the virtual network has been prepared appropriately for the migration.</span></span>
3. <span data-ttu-id="aed2b-147">리소스 마이그레이션을 위해 구독을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-147">Register your subscription for resource migration.</span></span> <span data-ttu-id="aed2b-148">리소스 마이그레이션을 위해 구독을 등록하려면 다음 PowerShell 코드 조각을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-148">To register your subscription for resource migration, use the following PowerShell snippet:</span></span>

  ```powershell 
  Select-AzureRmSubscription -SubscriptionName <Your Subscription Name>
  Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  ```
4. <span data-ttu-id="aed2b-149">유효성을 검사하고 준비한 후, 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-149">Validate, prepare, and migrate.</span></span> <span data-ttu-id="aed2b-150">가상 네트워크를 이동하려면 다음 PowerShell 코드 조작을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-150">To move the virtual network, use the following PowerShell snippet:</span></span>

  ```powershell
  Move-AzureVirtualNetwork -Prepare $vnetName  
  Move-AzureVirtualNetwork -Commit $vnetName
  ```

  <span data-ttu-id="aed2b-151">또한 다음 PowerShell cmdlet을 실행하여 마이그레이션을 중단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aed2b-151">You can also abort migration by running the following PowerShell cmdlet:</span></span>

  ```powershell
  Move-AzureVirtualNetwork -Abort $vnetName
  ```

## <a name="next-steps"></a><span data-ttu-id="aed2b-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aed2b-152">Next steps</span></span>
* [<span data-ttu-id="aed2b-153">클래식에서 Azure Resource Manager로 IaaS 리소스의 플랫폼 지원 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="aed2b-153">Platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [<span data-ttu-id="aed2b-154">클래식에서 Azure Resource Manager로의 플랫폼 지원 마이그레이션에 대한 기술 정보</span><span class="sxs-lookup"><span data-stu-id="aed2b-154">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
* [<span data-ttu-id="aed2b-155">FAQ: 클래식에서 Azure Resource Manager로 IaaS 리소스의 플랫폼 지원 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="aed2b-155">FAQs: Platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [<span data-ttu-id="aed2b-156">가장 일반적인 마이그레이션 오류 및 완화 방법 검토</span><span class="sxs-lookup"><span data-stu-id="aed2b-156">Review most common migration errors and mitigations</span></span>](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
