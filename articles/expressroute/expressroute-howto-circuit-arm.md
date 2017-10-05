---
title: "ExpressRoute 회로 만들기 및 수정: PowerShell: Azure Resource Manager | Microsoft Docs"
description: "이 문서에서는 Express 경로 회로를 만들고, 프로비전하고, 확인하고, 업데이트하고, 삭제하고, 프로비전을 해제하는 방법을 설명합니다."
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
ms.openlocfilehash: 8bfae39d84aaac3b9527084df9dcfbd51f591dfe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="0480d-103">PowerShell을 사용하여 Express 경로 회로 만들기 및 수정</span><span class="sxs-lookup"><span data-stu-id="0480d-103">Create and modify an ExpressRoute circuit using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0480d-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="0480d-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="0480d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0480d-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="0480d-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0480d-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="0480d-107">비디오 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0480d-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="0480d-108">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="0480d-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="0480d-109">이 문서에서는 PowerShell cmdlet 및 Azure Resource Manager 배포 모델을 사용하여 Azure ExpressRoute 회로를 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-109">This article describes how to create an Azure ExpressRoute circuit by using PowerShell cmdlets and the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="0480d-110">이 문서에는 회로의 상태 확인, 업데이트 또는 삭제 및 프로비전 해제를 수행하는 방법도 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-110">This article also shows you how to check the status of the circuit, update it, or delete and deprovision it.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0480d-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="0480d-111">Before you begin</span></span>
* <span data-ttu-id="0480d-112">최신 버전의 Azure Resource Manager PowerShell cmdlet을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-112">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="0480d-113">자세한 내용은 [Azure PowerShell 개요](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0480d-113">For more information, see [Overview of Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="0480d-114">구성을 시작하기 전에 [필수 조건](expressroute-prerequisites.md) 및 [워크플로](expressroute-workflows.md)를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-114">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>


## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="0480d-115">Express 경로 회로 만들기 및 프로비전</span><span class="sxs-lookup"><span data-stu-id="0480d-115">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-to-your-azure-account-and-select-your-subscription"></a><span data-ttu-id="0480d-116">1. Azure 계정에 로그인하고 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-116">1. Sign in to your Azure account and select your subscription</span></span>
<span data-ttu-id="0480d-117">구성을 시작하려면, Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-117">To begin your configuration, sign in to your Azure account.</span></span> <span data-ttu-id="0480d-118">연결에 도움이 되도록 다음 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-118">Use the following examples to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="0480d-119">계정에 대한 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-119">Check the subscriptions for the account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="0480d-120">Express 경로 회로를 만들려는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-120">Select the subscription that you want to create an ExpressRoute circuit for:</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-the-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="0480d-121">2. 지원되는 공급자, 위치 및 대역폭 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-121">2. Get the list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="0480d-122">Express 경로 회로를 만들기 전에 지원되는 연결 공급자, 위치 및 대역폭 옵션 목록이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-122">Before you create an ExpressRoute circuit, you need the list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="0480d-123">PowerShell cmdlet **Get-AzureRmExpressRouteServiceProvider**는 이후 단계에서 사용할 이 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-123">The PowerShell cmdlet **Get-AzureRmExpressRouteServiceProvider** returns this information, which you’ll use in later steps:</span></span>

```powershell
Get-AzureRmExpressRouteServiceProvider
```

<span data-ttu-id="0480d-124">연결 공급자가 여기에 나열되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-124">Check to see if your connectivity provider is listed there.</span></span> <span data-ttu-id="0480d-125">다음 정보를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-125">Make a note of the following information.</span></span> <span data-ttu-id="0480d-126">나중에 회로를 만들 때 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-126">You'll need it later when you create a circuit.</span></span>

* <span data-ttu-id="0480d-127">이름</span><span class="sxs-lookup"><span data-stu-id="0480d-127">Name</span></span>
* <span data-ttu-id="0480d-128">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="0480d-128">PeeringLocations</span></span>
* <span data-ttu-id="0480d-129">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="0480d-129">BandwidthsOffered</span></span>

<span data-ttu-id="0480d-130">이제 Express 경로 회로를 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-130">You're now ready to create an ExpressRoute circuit.</span></span>   

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="0480d-131">3. Express 경로 회로 만들기</span><span class="sxs-lookup"><span data-stu-id="0480d-131">3. Create an ExpressRoute circuit</span></span>
<span data-ttu-id="0480d-132">아직 리소스 그룹이 없는 경우 Express 경로 회로를 만들기 전에 먼저 리소스 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-132">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="0480d-133">다음 명령을 실행하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-133">You can do so by running the following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


<span data-ttu-id="0480d-134">아래 예제에서는 Equinix 실리콘밸리를 통해 200Mbps Express 경로 회로를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-134">The following example shows how to create a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="0480d-135">다른 공급자와 다른 설정을 사용하는 경우, 요청을 수행할 때 해당 정보를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-135">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> <span data-ttu-id="0480d-136">다음은 새 서비스 키에 대한 예제 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-136">The following is an example request for a new service key:</span></span>

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

<span data-ttu-id="0480d-137">올바른 SKU 계층과 SKU 제품군을 지정하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-137">Make sure that you specify the correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="0480d-138">SKU 계층은 Express 경로 표준 또는 Express 경로 Premium 추가 기능이 사용되는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-138">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="0480d-139">*표준*을 지정하여 표준 SKU를 가져오거나 프리미엄 추가 기능을 위해 *프리미엄*을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-139">You can specify *Standard* to get the standard SKU or *Premium* for the premium add-on.</span></span>
* <span data-ttu-id="0480d-140">SKU 제품군은 청구서 유형을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-140">SKU family determines the billing type.</span></span> <span data-ttu-id="0480d-141">데이터 요금제의 경우 *Metereddata*를 선택하고 무제한 데이터 요금제의 경우 *Unlimiteddata*를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-141">You can specify *Metereddata* for a metered data plan and *Unlimiteddata* for an unlimited data plan.</span></span> <span data-ttu-id="0480d-142">청구서 유형을 *Metereddata*에서 *Unlimiteddata*로 변경할 수 있지만, *Unlimiteddata*에서 *Metereddata*로는 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-142">You can change the billing type from *Metereddata* to *Unlimiteddata*, but you can't change the type from *Unlimiteddata* to *Metereddata*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0480d-143">Express 경로 회로는 서비스 키가 발급된 순간부터 비용이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-143">Your ExpressRoute circuit will be billed from the moment a service key is issued.</span></span> <span data-ttu-id="0480d-144">연결 공급자가 회로를 프로비전할 준비가 된 후에 이 작업을 수행하도록 하십시오.</span><span class="sxs-lookup"><span data-stu-id="0480d-144">Ensure that you perform this operation when the connectivity provider is ready to provision the circuit.</span></span>
> 
> 

<span data-ttu-id="0480d-145">응답에 서비스 키가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-145">The response contains the service key.</span></span> <span data-ttu-id="0480d-146">다음 명령을 실행하여 모든 매개 변수에 대한 자세한 설명을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-146">You can get detailed descriptions of all the parameters by running the following command:</span></span>

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="0480d-147">4. 모든 Express 경로 회로 나열</span><span class="sxs-lookup"><span data-stu-id="0480d-147">4. List all ExpressRoute circuits</span></span>
<span data-ttu-id="0480d-148">만들어 놓은 모든 ExpressRoute 회로 목록을 가져오려면 **Get-AzureRmExpressRouteCircuit** 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-148">To get a list of all the ExpressRoute circuits that you created, run the **Get-AzureRmExpressRouteCircuit** command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

<span data-ttu-id="0480d-149">응답은 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-149">The response will look similar to the following example:</span></span>

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

<span data-ttu-id="0480d-150">`Get-AzureRmExpressRouteCircuit` cmdlet을 사용하여 이 정보를 언제든지 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-150">You can retrieve this information at any time by using the `Get-AzureRmExpressRouteCircuit` cmdlet.</span></span> <span data-ttu-id="0480d-151">매개 변수 없이 호출을 수행하면 모든 회로가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-151">Making the call with no parameters lists all the circuits.</span></span> <span data-ttu-id="0480d-152">서비스 키는 *ServiceKey* 필드에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-152">Your service key will be listed in the *ServiceKey* field:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="0480d-153">응답은 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-153">The response will look similar to the following example:</span></span>

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


<span data-ttu-id="0480d-154">다음 명령을 실행하여 모든 매개 변수에 대한 자세한 설명을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-154">You can get detailed descriptions of all the parameters by running the following command:</span></span>

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="0480d-155">5. 프로비전을 위해 연결 공급자에 서비스 키 보내기</span><span class="sxs-lookup"><span data-stu-id="0480d-155">5. Send the service key to your connectivity provider for provisioning</span></span>
<span data-ttu-id="0480d-156">*ServiceProviderProvisioningState* 는 서비스 공급자 측의 현재 프로비전 상태에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-156">*ServiceProviderProvisioningState* provides information about the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="0480d-157">상태는 Microsoft 측의 상태를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-157">Status provides the state on the Microsoft side.</span></span> <span data-ttu-id="0480d-158">회로 프로비전 상태에 대한 자세한 내용은 [워크플로](expressroute-workflows.md#expressroute-circuit-provisioning-states) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0480d-158">For more information about circuit provisioning states, see the [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="0480d-159">새 Express 경로 회로를 만들면 회로는 다음 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-159">When you create a new ExpressRoute circuit, the circuit will be in the following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



<span data-ttu-id="0480d-160">연결 공급자가 사용자에 대해 활성화를 처리 중이면 회로가 다음 상태로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-160">The circuit will change to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="0480d-161">Express 경로 회로를 사용하려면 다음 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-161">For you to be able to use an ExpressRoute circuit, it must be in the following state:</span></span>

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="0480d-162">6. 회로 키의 상태를 주기적으로 확인</span><span class="sxs-lookup"><span data-stu-id="0480d-162">6. Periodically check the status and the state of the circuit key</span></span>
<span data-ttu-id="0480d-163">회로 키의 상태를 확인하면 공급자가 회로를 사용하도록 설정한 시점을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-163">Checking the status and the state of the circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="0480d-164">회로가 구성된 후에는 *ServiceProviderProvisioningState*가 아래 예에서처럼 *Provisioned*로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-164">After the circuit has been configured, *ServiceProviderProvisioningState* appears as *Provisioned*, as shown in the following example:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="0480d-165">응답은 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-165">The response will look similar to the following example:</span></span>

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

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="0480d-166">7. 라우팅 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="0480d-166">7. Create your routing configuration</span></span>
<span data-ttu-id="0480d-167">회로 피어링을 만들고 수정하는 단계별 지침은 [Express 경로 회로 라우팅 구성](expressroute-howto-routing-arm.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0480d-167">For step-by-step instructions, see the [ExpressRoute circuit routing configuration](expressroute-howto-routing-arm.md) article to create and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0480d-168">이 지침은 2계층 연결 서비스를 제공하는 서비스 공급자를 사용하여 만든 회로에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-168">These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="0480d-169">관리된 3계층 서비스(일반적으로 MPLS와 같은 IP VPN)를 제공하는 서비스 공급자를 사용하는 경우 연결 공급자는 사용자를 위해 라우팅을 구성하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-169">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="0480d-170">8. 가상 네트워크를 Express 경로 회로에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-170">8. Link a virtual network to an ExpressRoute circuit</span></span>
<span data-ttu-id="0480d-171">그 다음 가상 네트워크를 Express 경로 회로에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-171">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="0480d-172">Resource Manager 배포 모델을 작업하는 경우에는 [Express 경로 회로에 가상 네트워크 연결](expressroute-howto-linkvnet-arm.md) 문서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-172">Use the [Linking virtual networks to ExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with the Resource Manager deployment model.</span></span>

## <a name="getting-the-status-of-an-expressroute-circuit"></a><span data-ttu-id="0480d-173">Express 경로 회로의 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="0480d-173">Getting the status of an ExpressRoute circuit</span></span>
<span data-ttu-id="0480d-174">**Get-AzureRmExpressRouteCircuit** cmdlet을 사용하여 언제든지 이 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-174">You can retrieve this information at any time by using the **Get-AzureRmExpressRouteCircuit** cmdlet.</span></span> <span data-ttu-id="0480d-175">매개 변수 없이 호출을 수행하면 모든 회로가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-175">Making the call with no parameters lists all the circuits.</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="0480d-176">응답은 다음 예와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-176">The response will be similar to the following example:</span></span>

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


<span data-ttu-id="0480d-177">리소스 그룹 이름 및 회로 이름을 매개 변수 형태로 호출에 전달하면 특정 Express 경로 회로에 대한 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-177">You can get information on a specific ExpressRoute circuit by passing the resource group name and circuit name as a parameter to the call:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="0480d-178">응답은 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-178">The response will look similar to the following example:</span></span>

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


<span data-ttu-id="0480d-179">다음 명령을 실행하여 모든 매개 변수에 대한 자세한 설명을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-179">You can get detailed descriptions of all the parameters by running the following command:</span></span>

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <span data-ttu-id="0480d-180"><a name="modify"></a>Express 경로 회로 수정</span><span class="sxs-lookup"><span data-stu-id="0480d-180"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="0480d-181">연결에 미치는 영향 없이 Express 경로 회로의 특정 속성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-181">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="0480d-182">가동 중지 시간 없이 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-182">You can do the following with no downtime:</span></span>

* <span data-ttu-id="0480d-183">Express 경로 회로에 대해 Express 경로 프리미엄 추가 기능을 사용하거나 사용하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-183">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="0480d-184">포트에 사용 가능한 용량이 있는 경우 ExpressRoute 회로의 대역폭을 증가시킵니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-184">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="0480d-185">회로 대역폭 다운그레이드는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-185">Downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="0480d-186">요금제를 데이터 요금에서 무제한 데이터 요금으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-186">Change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="0480d-187">요금제를 무제한 데이터 요금에서 데이터 요금으로 변경하는 것은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-187">Changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="0480d-188">*Allow Classic Operations*을 활성화하거나 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-188">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="0480d-189">제한 및 제한 사항에 대한 자세한 내용은 [Express 경로 FAQ](expressroute-faqs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0480d-189">For more information on limits and limitations, refer to the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="to-enable-the-expressroute-premium-add-on"></a><span data-ttu-id="0480d-190">Express 경로 Premium 추가 기능을 활성화하려면</span><span class="sxs-lookup"><span data-stu-id="0480d-190">To enable the ExpressRoute premium add-on</span></span>
<span data-ttu-id="0480d-191">다음 PowerShell 코드 조각을 사용하여 기존 회로에 대해 Express 경로 프리미엄 추가 기능을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-191">You can enable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

<span data-ttu-id="0480d-192">이제 Express 경로 프리미엄 추가 기능을 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-192">The circuit will now have the ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="0480d-193">명령이 성공적으로 실행되는 즉시 프리미엄 추가 기능에 대한 과금이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-193">We will begin billing you for the premium add-on capability as soon as the command has successfully run.</span></span>

### <a name="to-disable-the-expressroute-premium-add-on"></a><span data-ttu-id="0480d-194">Express 경로 Premium 추가 기능을 비활성화하려면</span><span class="sxs-lookup"><span data-stu-id="0480d-194">To disable the ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0480d-195">표준 회로에 허용된 것보다 많은 리소스를 사용할 경우 이 작업이 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-195">This operation can fail if you're using resources that are greater than what is permitted for the standard circuit.</span></span>
> 
> 

<span data-ttu-id="0480d-196">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="0480d-196">Note the following:</span></span>

* <span data-ttu-id="0480d-197">프리미엄을 표준으로 다운그레이드하기 전에 회로에 연결된 가상 네트워크 수가 10개 미만인지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-197">Before you downgrade from premium to standard, you must ensure that the number of virtual networks that are linked to the circuit is less than 10.</span></span> <span data-ttu-id="0480d-198">그렇게 하지 않으면 업데이트 요청이 실패하고, 프리미엄 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-198">If you don't do this, your update request fails, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="0480d-199">다른 지리적 위치의 모든 가상 네트워크를 연결 해제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-199">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="0480d-200">그렇게 하지 않으면 업데이트 요청이 실패하고, 프리미엄 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-200">If you don't do this, your update request will fail, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="0480d-201">사설 피어링을 위해서는 경로 테이블의 경로가 4000개 미만이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-201">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="0480d-202">경로 테이블 크기가 4000개 경로 이상이면 BGP 세션이 폐기되고 게시된 프리픽스 수가 4000개 미만이 될 때까지 다시 활성화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-202">If your route table size is greater than 4,000 routes, the BGP session drops and won't be reenabled until the number of advertised prefixes goes below 4,000.</span></span>

<span data-ttu-id="0480d-203">다음 PowerShell cmdlet을 사용하여 기존 회로에 대해 Express 경로 프리미엄 추가 기능을 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-203">You can disable the ExpressRoute premium add-on for the existing circuit by using the following PowerShell cmdlet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-update-the-expressroute-circuit-bandwidth"></a><span data-ttu-id="0480d-204">Express 경로 회로 대역폭을 업데이트하려면</span><span class="sxs-lookup"><span data-stu-id="0480d-204">To update the ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="0480d-205">공급자에 대해 지원되는 대역폭 옵션은 [Express 경로 FAQ](expressroute-faqs.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="0480d-205">For supported bandwidth options for your provider, check the [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="0480d-206">기존 회로의 크기보다 큰 모든 크기를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-206">You can pick any size greater than the size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0480d-207">기존 포트에 적절한 용량이 없는 경우 ExpressRoute 회로를 다시 만들어야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-207">You may have to recreate the ExpressRoute circuit if there is inadequate capacity on the existing port.</span></span> <span data-ttu-id="0480d-208">해당 위치에서 사용 가능한 추가 용량이 없는 경우 해당 회로를 업그레이드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-208">You cannot upgrade the circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="0480d-209">그러나 중단 없이 Express 경로 회로의 대역폭을 줄일 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-209">You cannot reduce the bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="0480d-210">대역폭을 다운그레이드하려면 Express 경로 회로의 프로비전을 해제하고 새 Express 경로 회로를 다시 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-210">Downgrading bandwidth requires you to deprovision the ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 

<span data-ttu-id="0480d-211">필요한 크기를 선택하면, 다음 명령을 사용하여 회로 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-211">After you decide what size you need, use the following command to resize your circuit:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


<span data-ttu-id="0480d-212">회로의 크기는 Microsoft 쪽에서 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-212">Your circuit will be sized up on the Microsoft side.</span></span> <span data-ttu-id="0480d-213">그런 다음 변경 사항에 맞게 구성을 업데이트하려면 해당 공급자에게 연락해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-213">Then you must contact your connectivity provider to update configurations on their side to match this change.</span></span> <span data-ttu-id="0480d-214">이 알림을 통보하고 나면, 업데이트된 대역폭 옵션에 대한 요금이 청구되기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-214">After you make this notification, we will begin billing you for the updated bandwidth option.</span></span>

### <a name="to-move-the-sku-from-metered-to-unlimited"></a><span data-ttu-id="0480d-215">SKU를 요금제에서 무제한으로 이동하려면</span><span class="sxs-lookup"><span data-stu-id="0480d-215">To move the SKU from metered to unlimited</span></span>
<span data-ttu-id="0480d-216">다음 PowerShell 코드 조각을 사용하여 Express 경로 회로의 SKU를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-216">You can change the SKU of an ExpressRoute circuit by using the following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-control-access-to-the-classic-and-resource-manager-environments"></a><span data-ttu-id="0480d-217">클래식 및 리소스 관리자 환경에 대한 액세스를 제어하려면</span><span class="sxs-lookup"><span data-stu-id="0480d-217">To control access to the classic and Resource Manager environments</span></span>
<span data-ttu-id="0480d-218">[클래식에서 Resource Manager 배포 모델로 Express 경로 회로 이동](expressroute-howto-move-arm.md)의 지침을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-218">Review the instructions in [Move ExpressRoute circuits from the classic to the Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="0480d-219">Express 경로 회로 프로비전 해제 및 삭제</span><span class="sxs-lookup"><span data-stu-id="0480d-219">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="0480d-220">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="0480d-220">Note the following:</span></span>

* <span data-ttu-id="0480d-221">모든 가상 네트워크를 Express 경로 회로에서 연결 해제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-221">You must unlink all virtual networks from the ExpressRoute circuit.</span></span> <span data-ttu-id="0480d-222">이 작업에 실패한 경우 회로에 연결된 가상 네트워크가 있는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="0480d-222">If this operation fails, check to see if any virtual networks are linked to the circuit.</span></span>
* <span data-ttu-id="0480d-223">ExpressRoute 회로 서비스 공급자 프로비전 상태가 **프로비전 중** 또는 **프로비전됨**인 경우에는 서비스 공급자에게 회로 프로비전 해제를 요청해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-223">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="0480d-224">서비스 공급자가 회로의 프로비전을 해제한 다음 통지를 보낼 때까지 리소스가 계속 예약되며 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-224">We will continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="0480d-225">서비스 공급자가 회로 프로비전을 해제하여 서비스 공급자 프로비전 상태가 **프로비전되지 않음**이 되면 회로를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-225">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**) you can then delete the circuit.</span></span> <span data-ttu-id="0480d-226">그러면 회로에 대한 요금 청구가 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-226">This will stop billing for the circuit</span></span>

<span data-ttu-id="0480d-227">다음 명령을 실행하여 Express 경로 회로를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-227">You can delete your ExpressRoute circuit by running the following command:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a><span data-ttu-id="0480d-228">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0480d-228">Next steps</span></span>

<span data-ttu-id="0480d-229">회로를 만든 후 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0480d-229">After you create your circuit, make sure that you do the following:</span></span>

* [<span data-ttu-id="0480d-230">Express 경로 회로의 라우팅 만들기 및 수정</span><span class="sxs-lookup"><span data-stu-id="0480d-230">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="0480d-231">가상 네트워크를 Express 경로 회로에 연결</span><span class="sxs-lookup"><span data-stu-id="0480d-231">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
