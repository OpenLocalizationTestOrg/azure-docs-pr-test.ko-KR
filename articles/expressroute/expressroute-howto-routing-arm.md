---
title: "어떻게 tooconfigure (피어 링)에 대 한 라우팅 ExpressRoute 회로: 리소스 관리자: PowerShell: Azure | Microsoft Docs"
description: "이 문서를 만들고 hello private, public 및 Microsoft 피어 링 express 경로 회로 프로 비전에 대 한 hello 단계를 안내 합니다. 또한이 문서를 보면 toocheck hello 상태 업데이트 또는 회로 대 한 피어 링 삭제 방법을 알 수 있습니다."
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
ms.openlocfilehash: eb3ddf5c05a086ac3e22c64417e51381ef465921
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="77102-104">PowerShell을 사용하여 ExpressRoute 회로의 피어링 만들기 및 수정</span><span class="sxs-lookup"><span data-stu-id="77102-104">Create and modify peering for an ExpressRoute circuit using PowerShell</span></span>

<span data-ttu-id="77102-105">이 문서를 사용 하 여 만들고 hello PowerShell을 사용 하는 리소스 관리자 배포 모델에서 ExpressRoute 회로 대 한 라우팅 구성을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="77102-106">Hello 상태, 업데이트 또는 삭제를 확인 하 고 피어 링 express 경로 회로 대 한 프로 비전을 해제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="77102-107">다른 방법 toowork toouse 회로 사용 하려는 경우 hello 다음 목록에서에서 아티클을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="77102-108">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="77102-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="77102-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="77102-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="77102-110">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="77102-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="77102-111">비디오 - 개인 피어링</span><span class="sxs-lookup"><span data-stu-id="77102-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="77102-112">비디오 - 공용 피어링</span><span class="sxs-lookup"><span data-stu-id="77102-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="77102-113">비디오 - Microsoft 피어링</span><span class="sxs-lookup"><span data-stu-id="77102-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="77102-114">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="77102-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="77102-115">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="77102-115">Configuration prerequisites</span></span>

* <span data-ttu-id="77102-116">Hello 최신 버전의 hello Azure 리소스 관리자 PowerShell cmdlet 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-116">You will need hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="77102-117">자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-117">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 
* <span data-ttu-id="77102-118">Hello 검토 했는지 확인 [필수 구성 요소](expressroute-prerequisites.md) 페이지 hello [라우팅 요구 사항](expressroute-routing.md) 페이지 및 hello [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="77102-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="77102-119">활성화된 Express 경로 회로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="77102-120">너무 hello 지침에 따라[ExpressRoute 회로 만들기](expressroute-howto-circuit-arm.md) 있고 계속 hello 회로 하기 전에 연결 공급자가 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-120">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="77102-121">hello ExpressRoute 회로이 문서의 toobe 수 toorun hello cmdlet을 가능 하 고 프로 비전 된 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets in this article.</span></span>

<span data-ttu-id="77102-122">이러한 지침은 계층 2 연결 서비스를 제공 하는 서비스 공급자를 사용 하 여 만든 toocircuits만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77102-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="77102-123">관리된 3계층 서비스(일반적으로 MPLS와 같은 IPVPN)를 제공하는 서비스 공급자를 사용하는 경우 연결 공급자는 사용자를 위해 라우팅을 구성하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77102-124">에서는 현재 보급 되지 않고 피어 링 hello 서비스 관리 포털을 통해 서비스 공급자가 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-124">We currently do not advertise peerings configured by service providers through hello service management portal.</span></span> <span data-ttu-id="77102-125">이 기능을 곧 사용할 수 있도록 개발 중입니다.</span><span class="sxs-lookup"><span data-stu-id="77102-125">We are working on enabling this capability soon.</span></span> <span data-ttu-id="77102-126">BGP 피어링을 구성하기 전에 서비스 공급자에게 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="77102-126">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="77102-127">ExpressRoute 회로에 한 가지, 두 가지 또는 세 가지 피어링을 구성할 수 있습니다.(개인, Azure 공용 Azure 및 Microsoft)</span><span class="sxs-lookup"><span data-stu-id="77102-127">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="77102-128">선택한 순서로 피어링을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-128">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="77102-129">그러나 한 번에 하나씩 피어 링의 hello 구성을 완료 되었는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-129">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span> 

## <a name="azure-private-peering"></a><span data-ttu-id="77102-130">Azure 개인 피어링</span><span class="sxs-lookup"><span data-stu-id="77102-130">Azure private peering</span></span>

<span data-ttu-id="77102-131">이 섹션을 사용 하면 만들기, 가져오기, 업데이트 및 삭제 hello ExpressRoute 회로 대 한 개인 피어 링 구성을 Azure 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-131">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="77102-132">Azure 개인 피어 링 toocreate</span><span class="sxs-lookup"><span data-stu-id="77102-132">toocreate Azure private peering</span></span>

1. <span data-ttu-id="77102-133">ExpressRoute에 대 한 hello PowerShell 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="77102-133">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="77102-134">Hello 최신에서 PowerShell 설치 관리자를 설치 해야 [PowerShell 갤러리](http://www.powershellgallery.com/) hello Azure 리소스 관리자 모듈 hello ExpressRoute cmdlet을 사용 하 여 순서 toostart에 hello PowerShell 세션으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="77102-134">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="77102-135">관리자 권한으로 PowerShell toorun이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-135">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  <span data-ttu-id="77102-136">모든 의미 체계의 버전 범위 알려진 hello 내의 hello AzureRM.* 모듈만 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="77102-136">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="77102-137">클릭할 수도 hello 알려진 의미 체계의 버전 범위 내의 select 모듈을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-137">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network 
  ```

  <span data-ttu-id="77102-138">Tooyour 계정에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-138">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="77102-139">ExpressRoute 회로 toocreate hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-139">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="77102-140">Express 경로 회로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77102-140">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="77102-141">Hello 지침 toocreate 따라는 [ExpressRoute 회로](expressroute-howto-circuit-arm.md) hello 연결 공급자가 사용자를 프로 비전 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-141">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="77102-142">관리 되는 계층 3 서비스를 제공 하는 연결 공급자, 경우에 연결 공급자 tooenable 있습니다에 대 한 피어 링 개인 Azure를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-142">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="77102-143">이 경우 hello 다음 섹션에 나열 된 toofollow 지침 필요 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-143">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="77102-144">그러나 연결 공급자 회로 만든 후,에 대 한 라우팅 관리 하지 않는 경우 계속 hello 다음 단계를 사용 하 여 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77102-144">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="77102-145">Hello ExpressRoute 회로 toomake 프로 비전 되 고도 사용 하도록 설정 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-145">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="77102-146">다음 예제는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-146">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="77102-147">hello 응답은 다음 예제와 비슷한 toohello입니다.</span><span class="sxs-lookup"><span data-stu-id="77102-147">hello response is similar toohello following example:</span></span>

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
4. <span data-ttu-id="77102-148">Azure 개인 피어 링 hello 회로 대 한 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-148">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="77102-149">Hello 다음 단계를 진행 하기 전에 다음 항목 hello 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-149">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="77102-150">/ 30 서브넷 hello 기본 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-150">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="77102-151">hello 서브넷에 가상 네트워크에 대 한 예약 된 모든 주소 공간의 일부가 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-151">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="77102-152">/ 30 서브넷 hello 보조 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-152">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="77102-153">hello 서브넷에 가상 네트워크에 대 한 예약 된 모든 주소 공간의 일부가 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-153">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="77102-154">유효한 VLAN ID tooestablish이 피어 링을 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-154">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="77102-155">없는 다른 피어 링 되도록 hello 회로에 사용 하 여 hello 동일한 VLAN ID</span><span class="sxs-lookup"><span data-stu-id="77102-155">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="77102-156">피어링에 대한 AS 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="77102-156">AS number for peering.</span></span> <span data-ttu-id="77102-157">2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-157">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="77102-158">이 피어링에 개인 AS 숫자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-158">You can use a private AS number for this peering.</span></span> <span data-ttu-id="77102-159">65515를 사용하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-159">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="77102-160">**선택 사항-** toouse 하나를 선택 하는 경우 MD5 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="77102-160">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="77102-161">다음 예에서는 tooconfigure 회로 대 한 피어 링 개인 Azure hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-161">Use hello following example tooconfigure Azure private peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="77102-162">Toouse MD5 해시를 선택 하면 다음 예제는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-162">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="77102-163">고객 ASN이 아닌 피어링 ASN로 AS 번호를 지정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-163">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="77102-164">세부 정보를 피어 링 개인 Azure tooview</span><span class="sxs-lookup"><span data-stu-id="77102-164">tooview Azure private peering details</span></span>

<span data-ttu-id="77102-165">다음 예제는 hello를 사용 하 여 구성 세부 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-165">You can get configuration details by using hello following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="77102-166">tooupdate Azure 개인 피어 링 구성</span><span class="sxs-lookup"><span data-stu-id="77102-166">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="77102-167">다음 예제는 hello를 사용 하 여 hello 구성의 어떠한 부분을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-167">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="77102-168">이 예제에서는 100 too500에서 hello hello 회로의 VLAN ID를 업데이트 중입니다.</span><span class="sxs-lookup"><span data-stu-id="77102-168">In this example, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="77102-169">Azure 개인 피어 링 toodelete</span><span class="sxs-lookup"><span data-stu-id="77102-169">toodelete Azure private peering</span></span>

<span data-ttu-id="77102-170">다음 예제는 hello를 실행 하 여 피어 링 구성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-170">You can remove your peering configuration by running hello following example:</span></span>

> [!WARNING]
> <span data-ttu-id="77102-171">모든 가상 네트워크 없는지 hello ExpressRoute 회로에서 연결 된이 예제를 실행 하기 전에 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-171">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this example.</span></span> 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a><span data-ttu-id="77102-172">Azure 공용 피어링</span><span class="sxs-lookup"><span data-stu-id="77102-172">Azure public peering</span></span>

<span data-ttu-id="77102-173">이 섹션을 사용 하면 생성, 가져오기, 업데이트 및 삭제 hello ExpressRoute 회로 대 한 Azure 공용 피어 링 구성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-173">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="77102-174">Azure 공용 피어 링 toocreate</span><span class="sxs-lookup"><span data-stu-id="77102-174">toocreate Azure public peering</span></span>

1. <span data-ttu-id="77102-175">ExpressRoute에 대 한 hello PowerShell 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="77102-175">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="77102-176">Hello 최신에서 PowerShell 설치 관리자를 설치 해야 [PowerShell 갤러리](http://www.powershellgallery.com/) hello Azure 리소스 관리자 모듈 hello ExpressRoute cmdlet을 사용 하 여 순서 toostart에 hello PowerShell 세션으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="77102-176">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="77102-177">관리자 권한으로 PowerShell toorun이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-177">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  <span data-ttu-id="77102-178">모든 의미 체계의 버전 범위 알려진 hello 내의 hello AzureRM.* 모듈만 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="77102-178">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="77102-179">클릭할 수도 hello 알려진 의미 체계의 버전 범위 내의 select 모듈을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-179">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
```

  <span data-ttu-id="77102-180">Tooyour 계정에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-180">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="77102-181">ExpressRoute 회로 toocreate hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-181">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="77102-182">Express 경로 회로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77102-182">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="77102-183">Hello 지침 toocreate 따라는 [ExpressRoute 회로](expressroute-howto-circuit-arm.md) hello 연결 공급자가 사용자를 프로 비전 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-183">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="77102-184">관리 되는 계층 3 서비스를 제공 하는 연결 공급자, 경우에 연결 공급자 tooenable 있습니다에 대 한 피어 링 개인 Azure를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="77102-185">이 경우 hello 다음 섹션에 나열 된 toofollow 지침 필요 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-185">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="77102-186">그러나 연결 공급자 회로 만든 후,에 대 한 라우팅 관리 하지 않는 경우 계속 hello 다음 단계를 사용 하 여 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77102-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="77102-187">Hello ExpressRoute 회로 tooensure 프로 비전 되며 사용 하도록 설정도 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-187">Check hello ExpressRoute circuit tooensure it is provisioned and also enabled.</span></span> <span data-ttu-id="77102-188">다음 예제는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-188">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="77102-189">hello 응답은 다음 예제와 비슷한 toohello입니다.</span><span class="sxs-lookup"><span data-stu-id="77102-189">hello response is similar toohello following example:</span></span>

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
4. <span data-ttu-id="77102-190">Azure 공용 피어 링 hello 회로 대 한 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-190">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="77102-191">다음 정보를 계속 진행 하기 전에 hello 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-191">Make sure that you have hello following information before you proceed further.</span></span>

  * <span data-ttu-id="77102-192">/ 30 서브넷 hello 기본 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-192">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="77102-193">유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-193">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="77102-194">/ 30 서브넷 hello 보조 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-194">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="77102-195">유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-195">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="77102-196">유효한 VLAN ID tooestablish이 피어 링을 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-196">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="77102-197">없는 다른 피어 링 되도록 hello 회로에 사용 하 여 hello 동일한 VLAN ID</span><span class="sxs-lookup"><span data-stu-id="77102-197">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="77102-198">피어링에 대한 AS 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="77102-198">AS number for peering.</span></span> <span data-ttu-id="77102-199">2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-199">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="77102-200">**선택 사항-** toouse 하나를 선택 하는 경우 MD5 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="77102-200">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="77102-201">다음 예에서는 tooconfigure 회로 대 한 피어 링 공용 Azure hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-201">Run hello following example tooconfigure Azure public peering for your circuit</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="77102-202">Toouse MD5 해시를 선택 하면 다음 예제는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-202">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="77102-203">고객 ASN이 아닌 피어링 ASN로 AS 번호를 지정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-203">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="77102-204">세부 정보를 피어 링 공용 Azure tooview</span><span class="sxs-lookup"><span data-stu-id="77102-204">tooview Azure public peering details</span></span>

<span data-ttu-id="77102-205">Cmdlet을 다음 hello를 사용 하 여 구성 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-205">You can get configuration details using hello following cmdlet:</span></span>

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="77102-206">tooupdate Azure 공용 피어 링 구성</span><span class="sxs-lookup"><span data-stu-id="77102-206">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="77102-207">다음 예제는 hello를 사용 하 여 hello 구성의 어떠한 부분을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-207">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="77102-208">이 예제에서는 200 too600에서 hello hello 회로의 VLAN ID를 업데이트 중입니다.</span><span class="sxs-lookup"><span data-stu-id="77102-208">In this example, hello VLAN ID of hello circuit is being updated from 200 too600.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="77102-209">Azure 공용 피어 링 toodelete</span><span class="sxs-lookup"><span data-stu-id="77102-209">toodelete Azure public peering</span></span>

<span data-ttu-id="77102-210">다음 예제는 hello를 실행 하 여 피어 링 구성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-210">You can remove your peering configuration by running hello following example:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a><span data-ttu-id="77102-211">Microsoft 피어링</span><span class="sxs-lookup"><span data-stu-id="77102-211">Microsoft peering</span></span>

<span data-ttu-id="77102-212">이 섹션을 사용 하면 생성, 가져오기, 업데이트 및 삭제 hello ExpressRoute 회로 대 한 Microsoft 피어 링 구성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-212">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77102-213">이전 tooAugust 1에 구성 된 ExpressRoute 회로의 Microsoft 피어 링, 경로 필터 정의 되어 있지 않은 경우에 2017 hello Microsoft 피어 링을 통해 보급 되는 모든 서비스 접두사를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-213">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="77102-214">Microsoft 또는 그 이후에 2017 년 8 월 1 구성한 ExpressRoute 회로의 피어 링 수는 없습니다 모든 접두사 필터는 연결 될 때까지 보급 toohello 회로 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-214">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="77102-215">자세한 내용은 [Microsoft 피어링에 경로 필터 구성](how-to-routefilter-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77102-215">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="77102-216">toocreate Microsoft 피어 링</span><span class="sxs-lookup"><span data-stu-id="77102-216">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="77102-217">ExpressRoute에 대 한 hello PowerShell 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="77102-217">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="77102-218">Hello 최신에서 PowerShell 설치 관리자를 설치 해야 [PowerShell 갤러리](http://www.powershellgallery.com/) hello Azure 리소스 관리자 모듈 hello ExpressRoute cmdlet을 사용 하 여 순서 toostart에 hello PowerShell 세션으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="77102-218">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="77102-219">관리자 권한으로 PowerShell toorun이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-219">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  <span data-ttu-id="77102-220">모든 의미 체계의 버전 범위 알려진 hello 내의 hello AzureRM.* 모듈만 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="77102-220">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="77102-221">클릭할 수도 hello 알려진 의미 체계의 버전 범위 내의 select 모듈을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-221">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
  ```

  <span data-ttu-id="77102-222">Tooyour 계정에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-222">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="77102-223">ExpressRoute 회로 toocreate hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-223">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="77102-224">Express 경로 회로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77102-224">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="77102-225">Hello 지침 toocreate 따라는 [ExpressRoute 회로](expressroute-howto-circuit-arm.md) hello 연결 공급자가 사용자를 프로 비전 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-225">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="77102-226">관리 되는 계층 3 서비스를 제공 하는 연결 공급자, 경우에 연결 공급자 tooenable 있습니다에 대 한 피어 링 개인 Azure를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-226">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="77102-227">이 경우 hello 다음 섹션에 나열 된 toofollow 지침 필요 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-227">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="77102-228">그러나 연결 공급자 회로 만든 후,에 대 한 라우팅 관리 하지 않는 경우 계속 hello 다음 단계를 사용 하 여 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77102-228">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="77102-229">Hello ExpressRoute 회로 toomake 프로 비전 되 고도 사용 하도록 설정 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-229">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="77102-230">다음 예제는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-230">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="77102-231">hello 응답은 다음 예제와 비슷한 toohello입니다.</span><span class="sxs-lookup"><span data-stu-id="77102-231">hello response is similar toohello following example:</span></span>

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
4. <span data-ttu-id="77102-232">Microsoft hello 회로 대 한 피어 링을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-232">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="77102-233">계속 하기 전에 정보 다음 hello 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-233">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="77102-234">/ 30 서브넷 hello 기본 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-234">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="77102-235">사용자가 소유하고 RIR/IRR에 등록된 유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-235">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="77102-236">/ 30 서브넷 hello 보조 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-236">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="77102-237">사용자가 소유하고 RIR/IRR에 등록된 유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-237">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="77102-238">유효한 VLAN ID tooestablish이 피어 링을 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-238">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="77102-239">없는 다른 피어 링 되도록 hello 회로에 사용 하 여 hello 동일한 VLAN ID</span><span class="sxs-lookup"><span data-stu-id="77102-239">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="77102-240">피어링에 대한 AS 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="77102-240">AS number for peering.</span></span> <span data-ttu-id="77102-241">2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-241">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="77102-242">접두사를 보급: 목록을 제공 해야 모든 접두사의 hello BGP 세션을 통해 tooadvertise 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-242">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="77102-243">공용 IP 주소 접두사만 수락됩니다.</span><span class="sxs-lookup"><span data-stu-id="77102-243">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="77102-244">Toosend 접두사를 사용 하도록 하려는 경우 쉼표로 구분 된 목록을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-244">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="77102-245">이 접두사는 RIR에 등록 된 tooyou 여야 / IRR입니다.</span><span class="sxs-lookup"><span data-stu-id="77102-245">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="77102-246">**선택 사항-** 고객 ASN: 광고 접두사 수로 등록 된 toohello 피어 링 되지 않은 경우 등록 된 숫자 toowhich로 hello를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-246">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="77102-247">라우팅 레지스트리 이름을: hello RIR 지정할 수 있습니다는 hello에 대 한 번호 매기기로이 앞에 추가 IRR를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-247">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="77102-248">**선택 사항-** toouse 하나를 선택 하는 경우 MD5 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="77102-248">**Optional -** An MD5 hash if you choose toouse one.</span></span>

   <span data-ttu-id="77102-249">다음 예에서는 tooconfigure Microsoft 피어 링 회로 대 한 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-249">Use hello following example tooconfigure Microsoft peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="tooget-microsoft-peering-details"></a><span data-ttu-id="77102-250">tooget Microsoft 피어 링 세부 정보</span><span class="sxs-lookup"><span data-stu-id="77102-250">tooget Microsoft peering details</span></span>

<span data-ttu-id="77102-251">다음 예제는 hello를 사용 하 여 구성 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-251">You can get configuration details using hello following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="77102-252">tooupdate Microsoft 피어 링 구성</span><span class="sxs-lookup"><span data-stu-id="77102-252">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="77102-253">다음 예제는 hello를 사용 하 여 hello 구성의 어떠한 부분을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-253">You can update any part of hello configuration using hello following example:</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="77102-254">toodelete Microsoft 피어 링</span><span class="sxs-lookup"><span data-stu-id="77102-254">toodelete Microsoft peering</span></span>

<span data-ttu-id="77102-255">Hello 다음 cmdlet을 실행 하 여 피어 링 구성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77102-255">You can remove your peering configuration by running hello following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a><span data-ttu-id="77102-256">다음 단계</span><span class="sxs-lookup"><span data-stu-id="77102-256">Next steps</span></span>

<span data-ttu-id="77102-257">다음 단계 [연결할 ExpressRoute 회로 VNet tooan](expressroute-howto-linkvnet-arm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="77102-257">Next step, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

* <span data-ttu-id="77102-258">Express 경로 워크플로에 대한 자세한 내용은 [Express 경로 워크플로](expressroute-workflows.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77102-258">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="77102-259">회로 피어링에 대한 자세한 내용은 [Express 경로 회로 및 라우팅 도메인](expressroute-circuit-peerings.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77102-259">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="77102-260">가상 네트워크 작업에 대한 자세한 내용은 [가상 네트워크 개요](../virtual-network/virtual-networks-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77102-260">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
