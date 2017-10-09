---
title: "ExpressRoute 회로 만들기 및 수정: PowerShell: Azure Resource Manager | Microsoft Docs"
description: "이 문서에서는 어떻게 toocreate, 프로 비전, 확인, 업데이트, 삭제 및 ExpressRoute 회로 프로 비전 해제를 설명 합니다."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f997182e-9b25-4a7a-b079-b004221dadcc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8d76c577a9cffdd393abac1b76cccc27d92e9e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="bba0c-103">PowerShell을 사용하여 Express 경로 회로 만들기 및 수정</span><span class="sxs-lookup"><span data-stu-id="bba0c-103">Create and modify an ExpressRoute circuit using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bba0c-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="bba0c-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="bba0c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bba0c-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="bba0c-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bba0c-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="bba0c-107">비디오 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bba0c-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="bba0c-108">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="bba0c-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="bba0c-109">이 문서에서는 PowerShell cmdlet 및 hello Azure 리소스 관리자 배포 모델을 사용 하 여 toocreate Azure ExpressRoute 회로 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-109">This article describes how toocreate an Azure ExpressRoute circuit by using PowerShell cmdlets and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="bba0c-110">또한이 문서를 보면 hello 회로의 toocheck hello 상태를 업데이트 또는 삭제 및 프로 비전 해제 방법을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-110">This article also shows you how toocheck hello status of hello circuit, update it, or delete and deprovision it.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bba0c-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="bba0c-111">Before you begin</span></span>
* <span data-ttu-id="bba0c-112">Hello hello Azure 리소스 관리자 PowerShell cmdlet의 최신 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-112">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="bba0c-113">자세한 내용은 [Azure PowerShell 개요](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bba0c-113">For more information, see [Overview of Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="bba0c-114">검토 hello [필수 구성 요소](expressroute-prerequisites.md) 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="bba0c-114">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>


## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="bba0c-115">Express 경로 회로 만들기 및 프로비전</span><span class="sxs-lookup"><span data-stu-id="bba0c-115">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a><span data-ttu-id="bba0c-116">1. Tooyour Azure 계정에에서 로그인 하 고 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-116">1. Sign in tooyour Azure account and select your subscription</span></span>
<span data-ttu-id="bba0c-117">toobegin 구성, tooyour Azure 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-117">toobegin your configuration, sign in tooyour Azure account.</span></span> <span data-ttu-id="bba0c-118">예제 toohelp 연결한 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-118">Use hello following examples toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="bba0c-119">Hello 계정에 대 한 hello 구독을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-119">Check hello subscriptions for hello account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="bba0c-120">Hello 피드에 toocreate에 대 한 express 경로 회로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-120">Select hello subscription that you want toocreate an ExpressRoute circuit for:</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="bba0c-121">2. 지원 되는 공급자, 위치 및 대역폭 hello 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-121">2. Get hello list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="bba0c-122">ExpressRoute 회로 만들기 전에 hello 지원 되는 연결 공급자, 위치 및 대역폭 옵션 목록이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-122">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="bba0c-123">PowerShell cmdlet을 hello **Get AzureRmExpressRouteServiceProvider** 이후 단계에서 사용 하는이 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-123">hello PowerShell cmdlet **Get-AzureRmExpressRouteServiceProvider** returns this information, which you’ll use in later steps:</span></span>

```powershell
Get-AzureRmExpressRouteServiceProvider
```

<span data-ttu-id="bba0c-124">연결 공급자가 여기에 나열 된 경우 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-124">Check toosee if your connectivity provider is listed there.</span></span> <span data-ttu-id="bba0c-125">Hello 다음 정보를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-125">Make a note of hello following information.</span></span> <span data-ttu-id="bba0c-126">나중에 회로를 만들 때 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-126">You'll need it later when you create a circuit.</span></span>

* <span data-ttu-id="bba0c-127">이름</span><span class="sxs-lookup"><span data-stu-id="bba0c-127">Name</span></span>
* <span data-ttu-id="bba0c-128">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="bba0c-128">PeeringLocations</span></span>
* <span data-ttu-id="bba0c-129">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="bba0c-129">BandwidthsOffered</span></span>

<span data-ttu-id="bba0c-130">이제 준비 toocreate ExpressRoute 회로 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-130">You're now ready toocreate an ExpressRoute circuit.</span></span>   

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="bba0c-131">3. Express 경로 회로 만들기</span><span class="sxs-lookup"><span data-stu-id="bba0c-131">3. Create an ExpressRoute circuit</span></span>
<span data-ttu-id="bba0c-132">아직 리소스 그룹이 없는 경우 Express 경로 회로를 만들기 전에 먼저 리소스 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-132">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="bba0c-133">따라서 hello 다음 명령을 실행 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-133">You can do so by running hello following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


<span data-ttu-id="bba0c-134">다음 예제는 hello Silicon Valley에 Equinix 통해 toocreate 200 50mbps ExpressRoute 회로 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-134">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="bba0c-135">다른 공급자와 다른 설정을 사용하는 경우, 요청을 수행할 때 해당 정보를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-135">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> <span data-ttu-id="bba0c-136">hello 다음 새 서비스 키에 대 한 예제 요청은입니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-136">hello following is an example request for a new service key:</span></span>

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

<span data-ttu-id="bba0c-137">Hello 올바른 SKU 계층과 SKU 제품군을 지정 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-137">Make sure that you specify hello correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="bba0c-138">SKU 계층은 Express 경로 표준 또는 Express 경로 Premium 추가 기능이 사용되는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-138">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="bba0c-139">지정할 수 있습니다 *표준* tooget hello 표준 SKU 또는 *프리미엄* hello premium 추가 기능에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-139">You can specify *Standard* tooget hello standard SKU or *Premium* for hello premium add-on.</span></span>
* <span data-ttu-id="bba0c-140">SKU 제품군 hello 청구 유형을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-140">SKU family determines hello billing type.</span></span> <span data-ttu-id="bba0c-141">데이터 요금제의 경우 *Metereddata*를 선택하고 무제한 데이터 요금제의 경우 *Unlimiteddata*를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-141">You can specify *Metereddata* for a metered data plan and *Unlimiteddata* for an unlimited data plan.</span></span> <span data-ttu-id="bba0c-142">hello 청구 유형을 변경할 수 있습니다 *Metereddata* 너무*Unlimiteddata*에서 hello 형식은 변경할 수 있지만 *Unlimiteddata* 너무*Metereddata* .</span><span class="sxs-lookup"><span data-stu-id="bba0c-142">You can change hello billing type from *Metereddata* too*Unlimiteddata*, but you can't change hello type from *Unlimiteddata* too*Metereddata*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bba0c-143">ExpressRoute 회로 서비스 키를 발급 하는 hello 순간부터 요금이 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-143">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="bba0c-144">Hello 연결 공급자가 준비 tooprovision hello 회로이 작업을 수행할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-144">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="bba0c-145">hello 응답 hello 서비스 키를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-145">hello response contains hello service key.</span></span> <span data-ttu-id="bba0c-146">Hello 다음 명령을 실행 하 여 모든 hello 매개 변수에 대 한 자세한 설명을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-146">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="bba0c-147">4. 모든 Express 경로 회로 나열</span><span class="sxs-lookup"><span data-stu-id="bba0c-147">4. List all ExpressRoute circuits</span></span>
<span data-ttu-id="bba0c-148">모든 목록이 hello ExpressRoute 회로 사용자가 만든 tooget 실행 hello **Get AzureRmExpressRouteCircuit** 명령:</span><span class="sxs-lookup"><span data-stu-id="bba0c-148">tooget a list of all hello ExpressRoute circuits that you created, run hello **Get-AzureRmExpressRouteCircuit** command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

<span data-ttu-id="bba0c-149">hello 응답 다음 예제와 비슷한 toohello 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-149">hello response will look similar toohello following example:</span></span>

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
    CircuitProvisioningState          : Enabled
    ServiceProviderProvisioningState  : NotProvisioned
    ServiceProviderNotes              :
    ServiceProviderProperties         : {
                                          "ServiceProviderName": "Equinix",
                                          "PeeringLocation": "Silicon Valley",
                                          "BandwidthInMbps": 200
                                        }
    ServiceKey                        : **************************************
    Peerings                          : []

<span data-ttu-id="bba0c-150">Hello를 사용 하 여 언제 든 지가이 정보를 검색할 수 `Get-AzureRmExpressRouteCircuit` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bba0c-150">You can retrieve this information at any time by using hello `Get-AzureRmExpressRouteCircuit` cmdlet.</span></span> <span data-ttu-id="bba0c-151">Hello 매개 변수 없이 호출을 만드는 모든 hello 회로 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-151">Making hello call with no parameters lists all hello circuits.</span></span> <span data-ttu-id="bba0c-152">서비스 키 hello에 나열 될 *ServiceKey* 필드:</span><span class="sxs-lookup"><span data-stu-id="bba0c-152">Your service key will be listed in hello *ServiceKey* field:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="bba0c-153">hello 응답 다음 예제와 비슷한 toohello 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-153">hello response will look similar toohello following example:</span></span>

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
    ServiceProviderProvisioningState : NotProvisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


<span data-ttu-id="bba0c-154">Hello 다음 명령을 실행 하 여 모든 hello 매개 변수에 대 한 자세한 설명을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-154">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="bba0c-155">5. Hello 서비스 키 tooyour 연결 공급자를 프로 비전에 대 한 보내기</span><span class="sxs-lookup"><span data-stu-id="bba0c-155">5. Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="bba0c-156">*ServiceProviderProvisioningState* hello hello 서비스 공급자 쪽에 프로 비전의 현재 상태에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-156">*ServiceProviderProvisioningState* provides information about hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="bba0c-157">상태는 Microsoft의 hello에 hello 상태를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-157">Status provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="bba0c-158">상태를 프로 비전 하는 회로 대 한 자세한 내용은 참조 hello [워크플로](expressroute-workflows.md#expressroute-circuit-provisioning-states) 문서.</span><span class="sxs-lookup"><span data-stu-id="bba0c-158">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="bba0c-159">새 ExpressRoute 회로 만들 때 다음 상태 hello hello 회로가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-159">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



<span data-ttu-id="bba0c-160">hello 회로 toohello hello 연결 공급자를 사용 하면 hello 진행 중인 경우 뒤에 상태를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-160">hello circuit will change toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="bba0c-161">하면 toobe 수 toouse ExpressRoute 회로 hello 상태 뒤에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-161">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="bba0c-162">6. Hello 상태 및 hello 회로 키의 hello 상태를 주기적으로 확인</span><span class="sxs-lookup"><span data-stu-id="bba0c-162">6. Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="bba0c-163">Hello 상태 및 hello 회로 키의 hello 상태를 확인 하면 공급자가 회로 설정 하는 때를 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-163">Checking hello status and hello state of hello circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="bba0c-164">Hello 회로 구성한 후 *ServiceProviderProvisioningState* 로 표시 *프로 비전 됨*hello 다음 예제에에서 나온 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="bba0c-164">After hello circuit has been configured, *ServiceProviderProvisioningState* appears as *Provisioned*, as shown in hello following example:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="bba0c-165">hello 응답 다음 예제와 비슷한 toohello 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-165">hello response will look similar toohello following example:</span></span>

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

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="bba0c-166">7. 라우팅 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="bba0c-166">7. Create your routing configuration</span></span>
<span data-ttu-id="bba0c-167">단계별 지침은 hello [ExpressRoute 회로 라우팅 구성을](expressroute-howto-routing-arm.md) toocreate 문서 및 회로 피어 링을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-167">For step-by-step instructions, see hello [ExpressRoute circuit routing configuration](expressroute-howto-routing-arm.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bba0c-168">이러한 지침은 계층 2 연결 서비스를 제공 하는 서비스 공급자를 사용 하 여 만든 toocircuits만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-168">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="bba0c-169">관리된 3계층 서비스(일반적으로 MPLS와 같은 IP VPN)를 제공하는 서비스 공급자를 사용하는 경우 연결 공급자는 사용자를 위해 라우팅을 구성하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-169">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="bba0c-170">8. 가상 네트워크 tooan ExpressRoute 회로 연결</span><span class="sxs-lookup"><span data-stu-id="bba0c-170">8. Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="bba0c-171">다음으로, 가상 네트워크 tooyour ExpressRoute 회로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-171">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="bba0c-172">사용 하 여 hello [tooExpressRoute 회로 네트워크 연결 가상](expressroute-howto-linkvnet-arm.md) hello 리소스 관리자 배포 모델을 사용 하 여 작업할 때 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-172">Use hello [Linking virtual networks tooExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with hello Resource Manager deployment model.</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="bba0c-173">ExpressRoute 회로의 hello 상태를 가져오기</span><span class="sxs-lookup"><span data-stu-id="bba0c-173">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="bba0c-174">Hello를 사용 하 여 언제 든 지가이 정보를 검색할 수 **Get AzureRmExpressRouteCircuit** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bba0c-174">You can retrieve this information at any time by using hello **Get-AzureRmExpressRouteCircuit** cmdlet.</span></span> <span data-ttu-id="bba0c-175">Hello 매개 변수 없이 호출을 만드는 모든 hello 회로 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-175">Making hello call with no parameters lists all hello circuits.</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="bba0c-176">hello 응답에는 다음 예제와 비슷한 toohello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-176">hello response will be similar toohello following example:</span></span>

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


<span data-ttu-id="bba0c-177">Hello 리소스 그룹 이름 및 회로 이름 매개 변수 toohello 호출으로 전달 하 여 특정 ExpressRoute 회로 대 한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-177">You can get information on a specific ExpressRoute circuit by passing hello resource group name and circuit name as a parameter toohello call:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="bba0c-178">hello 응답 다음 예제와 비슷한 toohello 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-178">hello response will look similar toohello following example:</span></span>

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


<span data-ttu-id="bba0c-179">Hello 다음 명령을 실행 하 여 모든 hello 매개 변수에 대 한 자세한 설명을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-179">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <span data-ttu-id="bba0c-180"><a name="modify"></a>Express 경로 회로 수정</span><span class="sxs-lookup"><span data-stu-id="bba0c-180"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="bba0c-181">연결에 미치는 영향 없이 Express 경로 회로의 특정 속성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-181">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="bba0c-182">할 수 있는 가동 중지 시간 없이 사용 다음과 같습니다. hello:</span><span class="sxs-lookup"><span data-stu-id="bba0c-182">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="bba0c-183">Express 경로 회로에 대해 Express 경로 프리미엄 추가 기능을 사용하거나 사용하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-183">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="bba0c-184">증가 hello 대역폭의 ExpressRoute 회로 제공 된 hello 포트에서 용량입니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-184">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="bba0c-185">회로의 대역폭 hello를 다운 그레이드는 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-185">Downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="bba0c-186">데이터 요금 tooUnlimited 데이터에서에서 계획을 계량 hello를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-186">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="bba0c-187">무제한 데이터 요금 tooMetered 데이터가 지원 되지 않습니다에서 계획을 계량 hello를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-187">Changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="bba0c-188">*Allow Classic Operations*을 활성화하거나 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-188">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="bba0c-189">제한 및 제한 사항에 대 한 자세한 내용은 참조 toohello [express 경로 FAQ](expressroute-faqs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-189">For more information on limits and limitations, refer toohello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="bba0c-190">tooenable hello ExpressRoute premium 추가 기능</span><span class="sxs-lookup"><span data-stu-id="bba0c-190">tooenable hello ExpressRoute premium add-on</span></span>
<span data-ttu-id="bba0c-191">다음 PowerShell 코드 조각을 hello를 사용 하 여 기존 회로 대 한 hello ExpressRoute premium 추가 기능을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-191">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

<span data-ttu-id="bba0c-192">지금 hello 회로 사용 하도록 설정 하는 hello ExpressRoute premium 추가 기능을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-192">hello circuit will now have hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="bba0c-193">Hello 명령이 성공적으로 실행 되는 즉시 hello premium 추가 기능에 대 한 청구 하기 시작할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-193">We will begin billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="bba0c-194">toodisable hello ExpressRoute premium 추가 기능</span><span class="sxs-lookup"><span data-stu-id="bba0c-194">toodisable hello ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bba0c-195">이 작업은 hello 표준 회로 대 한 허용 되는 기능 보다 큰 리소스를 사용 하는 경우 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-195">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

<span data-ttu-id="bba0c-196">참고 hello 다음.</span><span class="sxs-lookup"><span data-stu-id="bba0c-196">Note hello following:</span></span>

* <span data-ttu-id="bba0c-197">연결 된 가상 네트워크의 해당 hello 수를 확인 해야 toostandard premium에서에서 다운 그레이드 먼저 toohello 회로 10 보다 작은 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-197">Before you downgrade from premium toostandard, you must ensure that hello number of virtual networks that are linked toohello circuit is less than 10.</span></span> <span data-ttu-id="bba0c-198">그렇게 하지 않으면 업데이트 요청이 실패하고, 프리미엄 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-198">If you don't do this, your update request fails, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="bba0c-199">다른 지리적 위치의 모든 가상 네트워크를 연결 해제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-199">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="bba0c-200">그렇게 하지 않으면 업데이트 요청이 실패하고, 프리미엄 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-200">If you don't do this, your update request will fail, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="bba0c-201">사설 피어링을 위해서는 경로 테이블의 경로가 4000개 미만이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-201">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="bba0c-202">경로 테이블 크기가 4, 000 경로 보다 큰 경우 hello BGP 세션 삭제 하 고 보급된 된 접두사의 hello 수가 4, 000 하위 메뉴를 클릭 될 때까지 했다가 다시 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-202">If your route table size is greater than 4,000 routes, hello BGP session drops and won't be reenabled until hello number of advertised prefixes goes below 4,000.</span></span>

<span data-ttu-id="bba0c-203">Hello 다음 PowerShell cmdlet을 사용 하 여 hello 기존 회로 대 한 hello ExpressRoute premium 추가 기능을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-203">You can disable hello ExpressRoute premium add-on for hello existing circuit by using hello following PowerShell cmdlet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="bba0c-204">tooupdate hello ExpressRoute 회로 대역폭</span><span class="sxs-lookup"><span data-stu-id="bba0c-204">tooupdate hello ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="bba0c-205">공급자에서 지원 되는 대역폭 옵션에 대 한 확인 hello [express 경로 FAQ](expressroute-faqs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-205">For supported bandwidth options for your provider, check hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="bba0c-206">기존 회로 hello 크기 보다 큰 모든 크기를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-206">You can pick any size greater than hello size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bba0c-207">Hello 기존 포트에서 부적절 한 용량이 있으면 toorecreate hello ExpressRoute 회로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-207">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="bba0c-208">해당 위치에서 사용할 수 없는 추가 용량 있으면 hello 회로 업그레이드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-208">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="bba0c-209">Hello 중단 없이 ExpressRoute 회로 대역폭을 줄일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-209">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="bba0c-210">대역폭을 다운 그레이드 toodeprovision hello ExpressRoute 회로 해야 하 고 새 ExpressRoute 회로 다시 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-210">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 

<span data-ttu-id="bba0c-211">필요한 크기를 결정 한 후 다음 명령 tooresize hello 회로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-211">After you decide what size you need, use hello following command tooresize your circuit:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


<span data-ttu-id="bba0c-212">회로 hello Microsoft 쪽에 조정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-212">Your circuit will be sized up on hello Microsoft side.</span></span> <span data-ttu-id="bba0c-213">다음 문의 해야 해당 측 toomatch 사용자 연결 공급자 tooupdate 구성을이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-213">Then you must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="bba0c-214">이 알림은 변경한 후 업데이트 하는 hello 대역폭 옵션에 대 한 청구 있습니다 하기 시작할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-214">After you make this notification, we will begin billing you for hello updated bandwidth option.</span></span>

### <a name="toomove-hello-sku-from-metered-toounlimited"></a><span data-ttu-id="bba0c-215">요금제 toounlimited에서 toomove hello SKU</span><span class="sxs-lookup"><span data-stu-id="bba0c-215">toomove hello SKU from metered toounlimited</span></span>
<span data-ttu-id="bba0c-216">다음 PowerShell 코드 조각을 hello를 사용 하 여 hello ExpressRoute 회로의 SKU를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-216">You can change hello SKU of an ExpressRoute circuit by using hello following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a><span data-ttu-id="bba0c-217">toocontrol 액세스 toohello 클래식 및 리소스 관리자 환경</span><span class="sxs-lookup"><span data-stu-id="bba0c-217">toocontrol access toohello classic and Resource Manager environments</span></span>
<span data-ttu-id="bba0c-218">지침에 hello 검토 [hello 클래식 toohello 리소스 관리자 배포 모델의 이동 ExpressRoute 회로](expressroute-howto-move-arm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-218">Review hello instructions in [Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="bba0c-219">Express 경로 회로 프로비전 해제 및 삭제</span><span class="sxs-lookup"><span data-stu-id="bba0c-219">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="bba0c-220">참고 hello 다음.</span><span class="sxs-lookup"><span data-stu-id="bba0c-220">Note hello following:</span></span>

* <span data-ttu-id="bba0c-221">ExpressRoute 회로 hello에서 모든 가상 네트워크 연결을 해제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-221">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="bba0c-222">이 작업이 실패 하면 가상 네트워크가 있는 경우 toosee toohello 회로 연결을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-222">If this operation fails, check toosee if any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="bba0c-223">Hello ExpressRoute 회로 서비스 공급자의 프로비저닝 상태 이면 **프로 비전** 또는 **프로 비전 됨** 편인 서비스 공급자 toodeprovision hello 회로 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-223">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="bba0c-224">Tooreserve 리소스를 계속 하 고 hello 서비스 공급자 프로 비전 해제 hello 회로 완료 하 고 알려주는 될 때까지 사용자를 청구 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-224">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="bba0c-225">Hello 서비스 공급자가 회로 hello를 프로 비전 해제 하는 경우 (hello 서비스 공급자 프로 비전 상태가 너무 설정 되어**프로 비전 되지**) hello 회로 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-225">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="bba0c-226">이렇게 되 면 hello 회로 대 한 청구</span><span class="sxs-lookup"><span data-stu-id="bba0c-226">This will stop billing for hello circuit</span></span>

<span data-ttu-id="bba0c-227">Hello 다음 명령을 실행 하 여 ExpressRoute 회로 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-227">You can delete your ExpressRoute circuit by running hello following command:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a><span data-ttu-id="bba0c-228">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bba0c-228">Next steps</span></span>

<span data-ttu-id="bba0c-229">회로 만든 후 다음 hello 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba0c-229">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="bba0c-230">Express 경로 회로의 라우팅 만들기 및 수정</span><span class="sxs-lookup"><span data-stu-id="bba0c-230">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="bba0c-231">가상 네트워크 tooyour ExpressRoute 회로 연결</span><span class="sxs-lookup"><span data-stu-id="bba0c-231">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
