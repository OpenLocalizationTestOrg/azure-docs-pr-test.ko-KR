---
title: "ExpressRoute 회로에 라우팅을 구성하는 방법(피어링): Resource Manager: PowerShell: Azure | Microsoft Docs"
description: "이 문서에서는 ExpressRoute 회로의 개인, 공용 및 Microsoft 피어링을 만들고 프로비전하는 단계를 안내합니다. 또한 회로의 상태를 확인하고 업데이트 또는 삭제하는 방법을 보여줍니다."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a036d51-77ae-4fee-9ddb-35f040fbdcdf
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: af68955b78239832e413e1b59e033d7d3da8d599
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="305e3-104">PowerShell을 사용하여 ExpressRoute 회로의 피어링 만들기 및 수정</span><span class="sxs-lookup"><span data-stu-id="305e3-104">Create and modify peering for an ExpressRoute circuit using PowerShell</span></span>

<span data-ttu-id="305e3-105">이 문서는 PowerShell을 사용하여 Resource Manager 배포 모델에서 ExpressRoute 회로에 라우팅 구성을 만들고 관리하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="305e3-106">ExpressRoute 회로에 대한 피어링의 상태를 확인, 업데이트 또는 삭제 및 프로비전 해제를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="305e3-107">회로를 사용하는 다른 메서드를 사용하려는 경우 다음 목록에서 문서를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="305e3-108">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="305e3-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="305e3-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="305e3-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="305e3-110">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="305e3-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="305e3-111">비디오 - 개인 피어링</span><span class="sxs-lookup"><span data-stu-id="305e3-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="305e3-112">비디오 - 공용 피어링</span><span class="sxs-lookup"><span data-stu-id="305e3-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="305e3-113">비디오 - Microsoft 피어링</span><span class="sxs-lookup"><span data-stu-id="305e3-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="305e3-114">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="305e3-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="305e3-115">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="305e3-115">Configuration prerequisites</span></span>

* <span data-ttu-id="305e3-116">최신 버전의 Azure Resource Manager PowerShell cmdlet을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-116">You will need the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="305e3-117">자세한 내용은 [Azure PowerShell 설치 및 구성하는 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="305e3-117">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> 
* <span data-ttu-id="305e3-118">구성을 시작하기 전에 [필수 구성 요소](expressroute-prerequisites.md) 페이지, [라우팅 요구 사항](expressroute-routing.md) 페이지 및 [워크플로](expressroute-workflows.md) 페이지를 검토했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-118">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="305e3-119">활성화된 ExpressRoute 회로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="305e3-120">지침을 수행하여 [ExpressRoute 회로를 만들고](expressroute-howto-circuit-arm.md) 진행하기 전에 연결 공급자를 통해 회로를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-120">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="305e3-121">ExpressRoute 회로는 이 문서에서 cmdlet을 실행할 수 있도록 프로비전되고 활성화된 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-121">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets in this article.</span></span>

<span data-ttu-id="305e3-122">이 지침은 2계층 연결 서비스를 제공하는 서비스 공급자를 사용하여 만든 회로에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-122">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="305e3-123">관리된 3계층 서비스(일반적으로 MPLS와 같은 IPVPN)를 제공하는 서비스 공급자를 사용하는 경우 연결 공급자는 사용자를 위해 라우팅을 구성하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="305e3-124">현재는 서비스 관리 포털을 통해 서비스 공급자가 구성한 피어링을 보급하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-124">We currently do not advertise peerings configured by service providers through the service management portal.</span></span> <span data-ttu-id="305e3-125">이 기능을 곧 사용할 수 있도록 개발 중입니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-125">We are working on enabling this capability soon.</span></span> <span data-ttu-id="305e3-126">BGP 피어링을 구성하기 전에 서비스 공급자에게 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="305e3-126">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="305e3-127">ExpressRoute 회로에 한 가지, 두 가지 또는 세 가지 피어링을 구성할 수 있습니다.(개인, Azure 공용 Azure 및 Microsoft)</span><span class="sxs-lookup"><span data-stu-id="305e3-127">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="305e3-128">선택한 순서로 피어링을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-128">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="305e3-129">그러나 각 피어링의 구성을 한 번에 하나 씩 완료하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-129">However, you must make sure that you complete the configuration of each peering one at a time.</span></span> 

## <a name="azure-private-peering"></a><span data-ttu-id="305e3-130">Azure 개인 피어링</span><span class="sxs-lookup"><span data-stu-id="305e3-130">Azure private peering</span></span>

<span data-ttu-id="305e3-131">이 섹션은 ExpressRoute 회로에 Azure 개인 피어링 구성을 만들고 가져오며 업데이트하고 삭제하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-131">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="305e3-132">Azure 개인 피어링을 만들려면</span><span class="sxs-lookup"><span data-stu-id="305e3-132">To create Azure private peering</span></span>

1. <span data-ttu-id="305e3-133">ExpressRoute에 대한 PowerShell 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-133">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="305e3-134">ExpressRoute cmdlet을 사용하려면 [PowerShell 갤러리](http://www.powershellgallery.com/) 에서 최신 Powershell 설치 관리자를 설치하고 PowerShell 세션으로 Azure 리소스 관리자 모듈을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-134">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="305e3-135">관리자 권한으로 PowerShell을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-135">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  <span data-ttu-id="305e3-136">알려진 의미 체계 버전 범위의 모든 AzureRM.* 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-136">Import all of the AzureRM.* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="305e3-137">또한 알려진 의미 체계 버전 범위의 선택 모듈만 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-137">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network 
  ```

  <span data-ttu-id="305e3-138">계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-138">Sign in to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="305e3-139">ExpressRoute 회로를 만들려는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-139">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="305e3-140">ExpressRoute 회로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-140">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="305e3-141">지침에 따라 [Express 경로 회로](expressroute-howto-circuit-arm.md) 를 만들고 연결 공급자를 통해 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-141">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="305e3-142">연결 공급자가 관리된 3계층 서비스를 제공하는 경우 연결 공급자를 요청하여 Azure 개인 피어링을 사용하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-142">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="305e3-143">이 경우에 다음 섹션에 나열된 지침에 따를 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-143">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="305e3-144">그러나 회로를 만든 후에 연결 공급자가 라우팅을 관리하지 않는 경우 다음 단계를 사용하여 구성을 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-144">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="305e3-145">먼저 ExpressRoute 회로가 프로비전되고 사용 가능한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-145">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="305e3-146">다음 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-146">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="305e3-147">응답은 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-147">The response is similar to the following example:</span></span>

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. <span data-ttu-id="305e3-148">회로에 Azure 개인 피어링을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-148">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="305e3-149">다음 단계를 계속 진행하기 전에 다음 항목이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-149">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="305e3-150">기본 링크에 대한 /30 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-150">A /30 subnet for the primary link.</span></span> <span data-ttu-id="305e3-151">서브넷은 가상 네트워크에 예약된 주소 공간의 일부가 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-151">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="305e3-152">보조 링크에 대한 /30 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-152">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="305e3-153">서브넷은 가상 네트워크에 예약된 주소 공간의 일부가 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-153">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="305e3-154">피어링을 설정할 유효한 VLAN ID입니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-154">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="305e3-155">회로에 다른 피어링이 동일한 VLAN ID를 사용하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-155">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="305e3-156">피어링에 대한 AS 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-156">AS number for peering.</span></span> <span data-ttu-id="305e3-157">2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-157">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="305e3-158">이 피어링에 개인 AS 숫자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-158">You can use a private AS number for this peering.</span></span> <span data-ttu-id="305e3-159">65515를 사용하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-159">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="305e3-160">**선택 사항 -** 사용하기로 선택한 경우 MD5 해시를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-160">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="305e3-161">다음 예제를 사용하여 회로에 Azure 개인 피어링을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-161">Use the following example to configure Azure private peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="305e3-162">MD5 해시를 사용하려는 경우 다음 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-162">If you choose to use an MD5 hash, use the following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="305e3-163">고객 ASN이 아닌 피어링 ASN로 AS 번호를 지정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-163">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="305e3-164">Azure 개인 피어링 세부 정보를 보려면</span><span class="sxs-lookup"><span data-stu-id="305e3-164">To view Azure private peering details</span></span>

<span data-ttu-id="305e3-165">다음 예제를 사용하여 구성 세부 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-165">You can get configuration details by using the following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="305e3-166">Azure 개인 피어링 구성을 업데이트하려면</span><span class="sxs-lookup"><span data-stu-id="305e3-166">To update Azure private peering configuration</span></span>

<span data-ttu-id="305e3-167">다음 예제를 사용하여 구성의 일부를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-167">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="305e3-168">이 예제에서는 회로의 VLAN ID를 100개에서 500개로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-168">In this example, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="305e3-169">Azure 개인 피어링을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="305e3-169">To delete Azure private peering</span></span>

<span data-ttu-id="305e3-170">다음 예제를 실행하여 피어링 구성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-170">You can remove your peering configuration by running the following example:</span></span>

> [!WARNING]
> <span data-ttu-id="305e3-171">이 예제를 실행하기 전에 모든 가상 네트워크가 ExpressRoute 회로에서 연결되지 않았는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-171">You must ensure that all virtual networks are unlinked from the ExpressRoute circuit before running this example.</span></span> 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a><span data-ttu-id="305e3-172">Azure 공용 피어링</span><span class="sxs-lookup"><span data-stu-id="305e3-172">Azure public peering</span></span>

<span data-ttu-id="305e3-173">이 섹션은 ExpressRoute 회로에 Azure 공용 피어링 구성을 만들고 가져오며 업데이트하고 삭제하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-173">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="305e3-174">Azure 공용 피어링을 만들려면</span><span class="sxs-lookup"><span data-stu-id="305e3-174">To create Azure public peering</span></span>

1. <span data-ttu-id="305e3-175">ExpressRoute에 대한 PowerShell 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-175">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="305e3-176">ExpressRoute cmdlet을 사용하려면 [PowerShell 갤러리](http://www.powershellgallery.com/) 에서 최신 Powershell 설치 관리자를 설치하고 PowerShell 세션으로 Azure 리소스 관리자 모듈을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-176">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="305e3-177">관리자 권한으로 PowerShell을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-177">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  <span data-ttu-id="305e3-178">알려진 의미 체계 버전 범위의 모든 AzureRM.* 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-178">Import all of the AzureRM.* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="305e3-179">또한 알려진 의미 체계 버전 범위의 선택 모듈만 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-179">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
```

  <span data-ttu-id="305e3-180">계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-180">Sign in to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="305e3-181">ExpressRoute 회로를 만들려는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-181">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="305e3-182">ExpressRoute 회로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-182">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="305e3-183">지침에 따라 [Express 경로 회로](expressroute-howto-circuit-arm.md) 를 만들고 연결 공급자를 통해 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-183">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="305e3-184">연결 공급자가 관리된 3계층 서비스를 제공하는 경우 연결 공급자를 요청하여 Azure 개인 피어링을 사용하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="305e3-185">이 경우에 다음 섹션에 나열된 지침에 따를 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-185">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="305e3-186">그러나 회로를 만든 후에 연결 공급자가 라우팅을 관리하지 않는 경우 다음 단계를 사용하여 구성을 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="305e3-187">먼저 ExpressRoute 회로가 프로비전되고 사용 가능한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-187">Check the ExpressRoute circuit to ensure it is provisioned and also enabled.</span></span> <span data-ttu-id="305e3-188">다음 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-188">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="305e3-189">응답은 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-189">The response is similar to the following example:</span></span>

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                      "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. <span data-ttu-id="305e3-190">회로에 Azure 공용 피어링을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-190">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="305e3-191">더 진행하기 전에 다음 정보가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-191">Make sure that you have the following information before you proceed further.</span></span>

  * <span data-ttu-id="305e3-192">기본 링크에 대한 /30 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-192">A /30 subnet for the primary link.</span></span> <span data-ttu-id="305e3-193">유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-193">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="305e3-194">보조 링크에 대한 /30 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-194">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="305e3-195">유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-195">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="305e3-196">피어링을 설정할 유효한 VLAN ID입니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-196">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="305e3-197">회로에 다른 피어링이 동일한 VLAN ID를 사용하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-197">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="305e3-198">피어링에 대한 AS 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-198">AS number for peering.</span></span> <span data-ttu-id="305e3-199">2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-199">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="305e3-200">**선택 사항 -** 사용하기로 선택한 경우 MD5 해시를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-200">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="305e3-201">다음 예제를 실행하여 회로에 Azure 공용 피어링을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-201">Run the following example to configure Azure public peering for your circuit</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="305e3-202">MD5 해시를 사용하려는 경우 다음 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-202">If you choose to use an MD5 hash, use the following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="305e3-203">고객 ASN이 아닌 피어링 ASN로 AS 번호를 지정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-203">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="305e3-204">Azure 공용 피어링 세부 정보를 보려면</span><span class="sxs-lookup"><span data-stu-id="305e3-204">To view Azure public peering details</span></span>

<span data-ttu-id="305e3-205">다음 cmdlet을 사용하여 구성 세부 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-205">You can get configuration details using the following cmdlet:</span></span>

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="305e3-206">Azure 공용 피어링 구성을 업데이트하려면</span><span class="sxs-lookup"><span data-stu-id="305e3-206">To update Azure public peering configuration</span></span>

<span data-ttu-id="305e3-207">다음 예제를 사용하여 구성의 일부를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-207">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="305e3-208">이 예제에서는 회로의 VLAN ID를 200개에서 600개로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-208">In this example, the VLAN ID of the circuit is being updated from 200 to 600.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="305e3-209">Azure 공용 피어링을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="305e3-209">To delete Azure public peering</span></span>

<span data-ttu-id="305e3-210">다음 예제를 실행하여 피어링 구성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-210">You can remove your peering configuration by running the following example:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a><span data-ttu-id="305e3-211">Microsoft 피어링</span><span class="sxs-lookup"><span data-stu-id="305e3-211">Microsoft peering</span></span>

<span data-ttu-id="305e3-212">이 섹션은 ExpressRoute 회로에 Microsoft 피어링 구성을 만들고 가져오며 업데이트하고 삭제하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-212">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="305e3-213">경로 필터를 정의하지 않은 경우에도 2017년 8월 1일 이전에 구성된 ExpressRoute 회로의 Microsoft 피어링에는 Microsoft 피어링을 통해 보급된 모든 서비스 접두사가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-213">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="305e3-214">2017년 8월 1일 이후에 구성된 ExpressRoute 회로의 Microsoft 피어링에는 경로 필터가 회로에 연결될 때까지 접두사가 보급되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-214">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span> <span data-ttu-id="305e3-215">자세한 내용은 [Microsoft 피어링에 경로 필터 구성](how-to-routefilter-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="305e3-215">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="305e3-216">Microsoft 피어링을 만들려면</span><span class="sxs-lookup"><span data-stu-id="305e3-216">To create Microsoft peering</span></span>

1. <span data-ttu-id="305e3-217">ExpressRoute에 대한 PowerShell 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-217">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="305e3-218">ExpressRoute cmdlet을 사용하려면 [PowerShell 갤러리](http://www.powershellgallery.com/) 에서 최신 Powershell 설치 관리자를 설치하고 PowerShell 세션으로 Azure 리소스 관리자 모듈을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-218">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="305e3-219">관리자 권한으로 PowerShell을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-219">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  <span data-ttu-id="305e3-220">알려진 의미 체계 버전 범위의 모든 AzureRM.* 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-220">Import all of the AzureRM.* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="305e3-221">또한 알려진 의미 체계 버전 범위의 선택 모듈만 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-221">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
  ```

  <span data-ttu-id="305e3-222">계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-222">Sign in to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="305e3-223">ExpressRoute 회로를 만들려는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-223">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="305e3-224">ExpressRoute 회로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-224">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="305e3-225">지침에 따라 [Express 경로 회로](expressroute-howto-circuit-arm.md) 를 만들고 연결 공급자를 통해 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-225">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="305e3-226">연결 공급자가 관리된 3계층 서비스를 제공하는 경우 연결 공급자를 요청하여 Azure 개인 피어링을 사용하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-226">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="305e3-227">이 경우에 다음 섹션에 나열된 지침에 따를 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-227">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="305e3-228">그러나 회로를 만든 후에 연결 공급자가 라우팅을 관리하지 않는 경우 다음 단계를 사용하여 구성을 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-228">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="305e3-229">먼저 ExpressRoute 회로가 프로비전되고 사용 가능한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-229">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="305e3-230">다음 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-230">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="305e3-231">응답은 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-231">The response is similar to the following example:</span></span>

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. <span data-ttu-id="305e3-232">회로에 Microsoft 피어링을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-232">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="305e3-233">진행하기 전에 다음 정보가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-233">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="305e3-234">기본 링크에 대한 /30 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-234">A /30 subnet for the primary link.</span></span> <span data-ttu-id="305e3-235">사용자가 소유하고 RIR/IRR에 등록된 유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-235">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="305e3-236">보조 링크에 대한 /30 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-236">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="305e3-237">사용자가 소유하고 RIR/IRR에 등록된 유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-237">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="305e3-238">피어링을 설정할 유효한 VLAN ID입니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-238">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="305e3-239">회로에 다른 피어링이 동일한 VLAN ID를 사용하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-239">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="305e3-240">피어링에 대한 AS 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-240">AS number for peering.</span></span> <span data-ttu-id="305e3-241">2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-241">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="305e3-242">보급된 접두사: BGP 세션을 통해 보급하려는 모든 접두사 목록을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-242">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="305e3-243">공용 IP 주소 접두사만 수락됩니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-243">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="305e3-244">접두사 집합을 보내려는 경우 쉼표로 구분된 목록을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-244">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="305e3-245">이 접두사는 RIR/IRR에 등록되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-245">These prefixes must be registered to you in an RIR / IRR.</span></span>
  * <span data-ttu-id="305e3-246">**선택 사항 -** 고객 ASN: 피어링 AS 숫자에 등록되지 않은 광고 접두사인 경우 등록된 AS 번호를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-246">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
  * <span data-ttu-id="305e3-247">라우팅 레지스트리 이름: AS 번호 및 접두사가 등록된 RIR/ IRR를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-247">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="305e3-248">**선택 사항 -** 사용하기로 선택한 경우 MD5 해시를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-248">**Optional -** An MD5 hash if you choose to use one.</span></span>

   <span data-ttu-id="305e3-249">다음 예제를 실행하여 회로에 Microsoft 피어링을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-249">Use the following example to configure Microsoft peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="to-get-microsoft-peering-details"></a><span data-ttu-id="305e3-250">Microsoft 피어링 정보를 가져오려면</span><span class="sxs-lookup"><span data-stu-id="305e3-250">To get Microsoft peering details</span></span>

<span data-ttu-id="305e3-251">다음 예제를 사용하여 구성 세부 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-251">You can get configuration details using the following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="305e3-252">Microsoft 피어링 구성을 업데이트하려면</span><span class="sxs-lookup"><span data-stu-id="305e3-252">To update Microsoft peering configuration</span></span>

<span data-ttu-id="305e3-253">다음 예제를 사용하여 구성의 일부를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-253">You can update any part of the configuration using the following example:</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="305e3-254">Microsoft 피어링을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="305e3-254">To delete Microsoft peering</span></span>

<span data-ttu-id="305e3-255">다음 cmdlet을 실행하여 피어링 구성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-255">You can remove your peering configuration by running the following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a><span data-ttu-id="305e3-256">다음 단계</span><span class="sxs-lookup"><span data-stu-id="305e3-256">Next steps</span></span>

<span data-ttu-id="305e3-257">다음 단계에서는 [VNet을 Express 경로 회로에 연결](expressroute-howto-linkvnet-arm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="305e3-257">Next step, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

* <span data-ttu-id="305e3-258">Express 경로 워크플로에 대한 자세한 내용은 [Express 경로 워크플로](expressroute-workflows.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="305e3-258">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="305e3-259">회로 피어링에 대한 자세한 내용은 [Express 경로 회로 및 라우팅 도메인](expressroute-circuit-peerings.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="305e3-259">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="305e3-260">가상 네트워크 작업에 대한 자세한 내용은 [가상 네트워크 개요](../virtual-network/virtual-networks-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="305e3-260">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
