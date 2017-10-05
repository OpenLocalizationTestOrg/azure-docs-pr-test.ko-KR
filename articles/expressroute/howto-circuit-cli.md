---
title: "Azure ExpressRoute 회로 만들기 및 수정: CLI | Microsoft Docs"
description: "이 문서에서는 CLI를 사용하여 ExpressRoute 회로를 만들고, 프로비전하고, 확인하고, 업데이트하고, 삭제하고, 프로비전을 해제하는 방법을 설명합니다."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman;cherylmc
ms.openlocfilehash: 1a1c9a96b772868e2c832e9ff57874038c0db2d4
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-cli"></a><span data-ttu-id="b8dfe-103">CLI를 사용하여 ExpressRoute 회로 만들기 및 수정</span><span class="sxs-lookup"><span data-stu-id="b8dfe-103">Create and modify an ExpressRoute circuit using CLI</span></span>


<span data-ttu-id="b8dfe-104">이 문서에서는 CLI(명령줄 인터페이스)를 사용하여 Azure ExpressRoute 회로를 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-104">This article describes how to create an Azure ExpressRoute circuit by using the Command Line Interface (CLI).</span></span> <span data-ttu-id="b8dfe-105">또한 이 문서에서는 회로의 상태를 확인하거나, 업데이트하거나, 삭제하고 프로비전을 해제하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-105">This article also shows you how to check the status, update, or delete and deprovision a circuit.</span></span> <span data-ttu-id="b8dfe-106">ExpressRoute 회로를 사용하는 다른 방법을 사용하려는 경우 다음 목록에서 문서를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-106">If you want to use a different method to work with ExpressRoute circuits, you can select the article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b8dfe-107">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="b8dfe-107">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="b8dfe-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8dfe-108">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="b8dfe-109">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b8dfe-109">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="b8dfe-110">비디오 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b8dfe-110">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="b8dfe-111">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="b8dfe-111">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
> 

## <a name="before-you-begin"></a><span data-ttu-id="b8dfe-112">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="b8dfe-112">Before you begin</span></span>

* <span data-ttu-id="b8dfe-113">시작하기 전에 최신 버전의 CLI 명령(2.0 이상)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-113">Before beginning, install the latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="b8dfe-114">CLI 명령 설치에 대한 자세한 내용은 [Azure CLI 2.0 설치](/cli/azure/install-azure-cli) 및 [Azure CLI 2.0 시작](/cli/azure/get-started-with-azure-cli)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-114">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="b8dfe-115">구성을 시작하기 전에 [필수 조건](expressroute-prerequisites.md) 및 [워크플로](expressroute-workflows.md)를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-115">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="b8dfe-116">Express 경로 회로 만들기 및 프로비전</span><span class="sxs-lookup"><span data-stu-id="b8dfe-116">Create and provision an ExpressRoute circuit</span></span>

### <a name="1-sign-in-to-your-azure-account-and-select-your-subscription"></a><span data-ttu-id="b8dfe-117">1. Azure 계정에 로그인하고 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-117">1. Sign in to your Azure account and select your subscription</span></span>

<span data-ttu-id="b8dfe-118">구성을 시작하려면, Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-118">To begin your configuration, sign in to your Azure account.</span></span> <span data-ttu-id="b8dfe-119">연결에 도움이 되도록 다음 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-119">Use the following examples to help you connect:</span></span>

```azurecli
az login
```

<span data-ttu-id="b8dfe-120">계정에 대한 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-120">Check the subscriptions for the account.</span></span>

```azurecli
az account list
```

<span data-ttu-id="b8dfe-121">ExpressRoute 회로를 만들려는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-121">Select the subscription for which you want to create an ExpressRoute circuit.</span></span>

```azurecli
az account set --subscription "<subscription ID>"
```

### <a name="2-get-the-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="b8dfe-122">2. 지원되는 공급자, 위치 및 대역폭 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-122">2. Get the list of supported providers, locations, and bandwidths</span></span>

<span data-ttu-id="b8dfe-123">Express 경로 회로를 만들기 전에 지원되는 연결 공급자, 위치 및 대역폭 옵션 목록이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-123">Before you create an ExpressRoute circuit, you need the list of supported connectivity providers, locations, and bandwidth options.</span></span> <span data-ttu-id="b8dfe-124">CLI 명령 'az network express-route list-service-providers'는 이 정보를 반환하고 이를 이후 단계에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-124">The CLI command 'az network express-route list-service-providers' returns this information, which you’ll use in later steps:</span></span>

```azurecli
az network express-route list-service-providers
```

<span data-ttu-id="b8dfe-125">응답은 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-125">The response is similar to the following example:</span></span>

```azurecli
[
  {
    "bandwidthsOffered": [
      {
        "offerName": "50Mbps",
        "valueInMbps": 50
      },
      {
        "offerName": "100Mbps",
        "valueInMbps": 100
      },
      {
        "offerName": "200Mbps",
        "valueInMbps": 200
      },
      {
        "offerName": "500Mbps",
        "valueInMbps": 500
      },
      {
        "offerName": "1Gbps",
        "valueInMbps": 1000
      },
      {
        "offerName": "2Gbps",
        "valueInMbps": 2000
      },
      {
        "offerName": "5Gbps",
        "valueInMbps": 5000
      },
      {
        "offerName": "10Gbps",
        "valueInMbps": 10000
      }
    ],
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/expressRouteServiceProviders/",
    "location": null,
    "name": "AARNet",
    "peeringLocations": [
      "Melbourne",
      "Sydney"
    ],
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "tags": null,
    "type": "Microsoft.Network/expressRouteServiceProviders"
  },
```

<span data-ttu-id="b8dfe-126">연결 공급자가 나열되었는지 확인하려면 응답을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-126">Check the response to see if your connectivity provider is listed.</span></span> <span data-ttu-id="b8dfe-127">나중에 회로를 만들 때 필요한 다음 정보를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-127">Make a note of the following information, which you will need when you create a circuit:</span></span>

* <span data-ttu-id="b8dfe-128">이름</span><span class="sxs-lookup"><span data-stu-id="b8dfe-128">Name</span></span>
* <span data-ttu-id="b8dfe-129">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="b8dfe-129">PeeringLocations</span></span>
* <span data-ttu-id="b8dfe-130">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="b8dfe-130">BandwidthsOffered</span></span>

<span data-ttu-id="b8dfe-131">이제 Express 경로 회로를 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-131">You're now ready to create an ExpressRoute circuit.</span></span>

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="b8dfe-132">3. Express 경로 회로 만들기</span><span class="sxs-lookup"><span data-stu-id="b8dfe-132">3. Create an ExpressRoute circuit</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8dfe-133">ExpressRoute 회로는 서비스 키가 발급된 순간부터 비용이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-133">Your ExpressRoute circuit is billed from the moment a service key is issued.</span></span> <span data-ttu-id="b8dfe-134">연결 공급자가 회로를 프로비전할 준비가 되면 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-134">Perform this operation when the connectivity provider is ready to provision the circuit.</span></span>
> 
> 

<span data-ttu-id="b8dfe-135">아직 리소스 그룹이 없는 경우 Express 경로 회로를 만들기 전에 먼저 리소스 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-135">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="b8dfe-136">다음 명령을 실행하여 리소스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-136">You can create a resource group by running the following command:</span></span>

```azurecli
az group create -n ExpressRouteResourceGroup -l "West US"
```

<span data-ttu-id="b8dfe-137">아래 예제에서는 Equinix 실리콘밸리를 통해 200Mbps Express 경로 회로를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-137">The following example shows how to create a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="b8dfe-138">다른 공급자와 다른 설정을 사용하는 경우, 요청을 수행할 때 해당 정보를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-138">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> 

<span data-ttu-id="b8dfe-139">올바른 SKU 계층과 SKU 제품군을 지정하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-139">Make sure that you specify the correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="b8dfe-140">SKU 계층은 Express 경로 표준 또는 Express 경로 Premium 추가 기능이 사용되는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-140">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="b8dfe-141">'표준'을 지정하여 표준 SKU를 가져오거나 프리미엄 추가 기능을 위해 '프리미엄'을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-141">You can specify 'Standard' to get the standard SKU or 'Premium' for the premium add-on.</span></span>
* <span data-ttu-id="b8dfe-142">SKU 제품군은 청구서 유형을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-142">SKU family determines the billing type.</span></span> <span data-ttu-id="b8dfe-143">데이터 요금제의 경우 'Metereddata'를 선택하고 무제한 데이터 요금제의 경우 'Unlimiteddata'를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-143">You can specify 'Metereddata' for a metered data plan and 'Unlimiteddata' for an unlimited data plan.</span></span> <span data-ttu-id="b8dfe-144">청구서 유형을 'Metereddata'에서 'Unlimiteddata'로 변경할 수 있지만, 'Unlimiteddata'에서 'Metereddata'로는 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-144">You can change the billing type from 'Metereddata' to 'Unlimiteddata', but you can't change the type from 'Unlimiteddata' to 'Metereddata'.</span></span>


<span data-ttu-id="b8dfe-145">ExpressRoute 회로는 서비스 키가 발급된 순간부터 비용이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-145">Your ExpressRoute circuit is billed from the moment a service key is issued.</span></span> <span data-ttu-id="b8dfe-146">다음 예제는 새 서비스 키에 대한 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-146">The following example is a request for a new service key:</span></span>

```azurecli
az network express-route create --bandwidth 200 -n MyCircuit --peering-location "Silicon Valley" -g ExpressRouteResourceGroup --provider "Equinix" -l "West US" --sku-family MeteredData --sku-tier Standard
```

<span data-ttu-id="b8dfe-147">응답에 서비스 키가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-147">The response contains the service key.</span></span>

### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="b8dfe-148">4. 모든 Express 경로 회로 나열</span><span class="sxs-lookup"><span data-stu-id="b8dfe-148">4. List all ExpressRoute circuits</span></span>

<span data-ttu-id="b8dfe-149">만든 모든 ExpressRoute 회로 목록을 가져오려면 'az network express-route list' 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-149">To get a list of all the ExpressRoute circuits that you created, run the 'az network express-route list' command.</span></span> <span data-ttu-id="b8dfe-150">이 명령을 사용하여 이 정보를 언제든지 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-150">You can retrieve this information at any time by using this command.</span></span> <span data-ttu-id="b8dfe-151">모든 회로를 나열하려면 매개 변수 없이 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-151">To list all circuits, make the call with no parameters.</span></span>

```azurecli
az network express-route list
```

<span data-ttu-id="b8dfe-152">서비스 키는 응답의 *ServiceKey* 필드에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-152">Your service key is listed in the *ServiceKey* field of the response.</span></span>

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

<span data-ttu-id="b8dfe-153">'-h' 매개 변수를 사용하는 명령을 실행하여 모든 매개 변수에 대한 자세한 설명을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-153">You can get detailed descriptions of all the parameters by running the command using the '-h' parameter.</span></span>

```azurecli
az network express-route list -h
```

### <a name="5-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="b8dfe-154">5. 프로비전을 위해 연결 공급자에 서비스 키 보내기</span><span class="sxs-lookup"><span data-stu-id="b8dfe-154">5. Send the service key to your connectivity provider for provisioning</span></span>

<span data-ttu-id="b8dfe-155">'ServiceProviderProvisioningState'는 서비스 공급자 쪽의 현재 프로비전 상태에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-155">'ServiceProviderProvisioningState' provides information about the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="b8dfe-156">상태는 Microsoft 쪽의 상태를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-156">The status provides the state on the Microsoft side.</span></span> <span data-ttu-id="b8dfe-157">자세한 내용은 [워크플로 문서](expressroute-workflows.md#expressroute-circuit-provisioning-states)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-157">For more information, see the [Workflows article](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span></span>

<span data-ttu-id="b8dfe-158">새 ExpressRoute 회로를 만들면 회로는 다음 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-158">When you create a new ExpressRoute circuit, the circuit is in the following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "NotProvisioned"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="b8dfe-159">연결 공급자가 사용자에 대해 활성화를 처리 중이면 회로가 다음 상태로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-159">The circuit changes to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioning"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="b8dfe-160">Express 경로 회로를 사용하려면 다음 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-160">For you to be able to use an ExpressRoute circuit, it must be in the following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioned"
"circuitProvisioningState": "Enabled
```

### <a name="6-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="b8dfe-161">6. 회로 키의 상태를 주기적으로 확인</span><span class="sxs-lookup"><span data-stu-id="b8dfe-161">6. Periodically check the status and the state of the circuit key</span></span>

<span data-ttu-id="b8dfe-162">회로 키의 상태를 확인하면 공급자가 회로를 사용하도록 설정한 시점을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-162">Checking the status and the state of the circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="b8dfe-163">회로가 구성된 후에는 'ServiceProviderProvisioningState'가 아래 예에서처럼 '프로비전됨'으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-163">After the circuit has been configured, 'ServiceProviderProvisioningState' appears as 'Provisioned', as shown in the following example:</span></span>

```azurecli
az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
```

<span data-ttu-id="b8dfe-164">응답은 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-164">The response is similar to the following example:</span></span>

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="b8dfe-165">7. 라우팅 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="b8dfe-165">7. Create your routing configuration</span></span>

<span data-ttu-id="b8dfe-166">회로 피어링을 만들고 수정하는 단계별 지침은 [Express 경로 회로 라우팅 구성](howto-routing-cli.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-166">For step-by-step instructions, see the [ExpressRoute circuit routing configuration](howto-routing-cli.md) article to create and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8dfe-167">이 지침은 2계층 연결 서비스를 제공하는 서비스 공급자를 사용하여 만든 회로에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-167">These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="b8dfe-168">관리된 3계층 서비스(일반적으로 MPLS와 같은 IP VPN)를 제공하는 서비스 공급자를 사용하는 경우 연결 공급자는 사용자를 위해 라우팅을 구성하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-168">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="b8dfe-169">8. 가상 네트워크를 Express 경로 회로에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-169">8. Link a virtual network to an ExpressRoute circuit</span></span>

<span data-ttu-id="b8dfe-170">그 다음 가상 네트워크를 Express 경로 회로에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-170">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="b8dfe-171">[ExpressRoute 회로에 가상 네트워크 연결](howto-linkvnet-cli.md) 문서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-171">Use the [Linking virtual networks to ExpressRoute circuits](howto-linkvnet-cli.md) article.</span></span>

## <span data-ttu-id="b8dfe-172"><a name="modify"></a>Express 경로 회로 수정</span><span class="sxs-lookup"><span data-stu-id="b8dfe-172"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>

<span data-ttu-id="b8dfe-173">연결에 미치는 영향 없이 Express 경로 회로의 특정 속성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-173">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span> <span data-ttu-id="b8dfe-174">중단 시간 없이 다음과 같이 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-174">You can make the following changes with no downtime:</span></span>

* <span data-ttu-id="b8dfe-175">ExpressRoute 회로에 대해 ExpressRoute Premium 추가 기능을 사용하거나 사용하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-175">You can enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="b8dfe-176">포트에 사용 가능한 수용작업량이 있는 경우 ExpressRoute 회로의 대역폭을 증가시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-176">You can increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="b8dfe-177">그러나, 회로의 대역폭 다운그레이드는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-177">However, downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="b8dfe-178">요금제를 데이터 요금에서 무제한 데이터 요금으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-178">You can change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="b8dfe-179">그러나 요금제를 무제한 데이터 요금에서 데이터 요금으로 변경하는 것은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-179">However, changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="b8dfe-180">*Allow Classic Operations*을 활성화하거나 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-180">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="b8dfe-181">제한 및 제한 사항에 대한 자세한 내용은 [ExpressRoute FAQ](expressroute-faqs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-181">For more information on limits and limitations, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="to-enable-the-expressroute-premium-add-on"></a><span data-ttu-id="b8dfe-182">Express 경로 Premium 추가 기능을 활성화하려면</span><span class="sxs-lookup"><span data-stu-id="b8dfe-182">To enable the ExpressRoute premium add-on</span></span>

<span data-ttu-id="b8dfe-183">다음 명령을 사용하여 기존 회로에 ExpressRoute Premium 추가 기능을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-183">You can enable the ExpressRoute premium add-on for your existing circuit by using the following command:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Premium
```

<span data-ttu-id="b8dfe-184">이제 ExpressRoute Premium 추가 기능을 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-184">The circuit now has the ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="b8dfe-185">명령이 성공적으로 실행되는 즉시 Premium 추가 기능에 대한 대금 청구가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-185">We begin billing you for the premium add-on capability as soon as the command has successfully run.</span></span>

### <a name="to-disable-the-expressroute-premium-add-on"></a><span data-ttu-id="b8dfe-186">Express 경로 Premium 추가 기능을 비활성화하려면</span><span class="sxs-lookup"><span data-stu-id="b8dfe-186">To disable the ExpressRoute premium add-on</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8dfe-187">표준 회로에 허용된 것보다 많은 리소스를 사용할 경우 이 작업이 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-187">This operation can fail if you're using resources that are greater than what is permitted for the standard circuit.</span></span>
> 
> 

<span data-ttu-id="b8dfe-188">ExpressRoute Premium 추가 기능을 해제하기 전에 다음 조건을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-188">Before disabling the ExpressRoute premium add-on, understand the following criteria:</span></span>

* <span data-ttu-id="b8dfe-189">프리미엄을 표준으로 다운그레이드하기 전에 회로에 연결된 가상 네트워크 수가 10개 미만인지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-189">Before you downgrade from premium to standard, you must make sure that you have fewer than 10 virtual networks linked to the circuit.</span></span> <span data-ttu-id="b8dfe-190">10개를 초과하면 업데이트 요청이 실패하고, 프리미엄 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-190">If you have more than 10, your update request fails, and we bill you at premium rates.</span></span>
* <span data-ttu-id="b8dfe-191">다른 지리적 위치의 모든 가상 네트워크를 연결 해제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-191">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="b8dfe-192">가상 네트워크의 연결을 해제하지 않으면 업데이트 요청이 실패하고, 프리미엄 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-192">If you don't unlink all your virtual networks, your update request fails and we bill you at premium rates.</span></span>
* <span data-ttu-id="b8dfe-193">사설 피어링을 위해서는 경로 테이블의 경로가 4000개 미만이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-193">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="b8dfe-194">경로 테이블 크기가 4,000개 경로보다 큰 경우 BGP 세션이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-194">If your route table size is greater than 4,000 routes, the BGP session drops.</span></span> <span data-ttu-id="b8dfe-195">보급된 접두사의 수가 4,000 미만이 될 때까지 세션을 다시 사용하도록 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-195">The session won't be reenabled until the number of advertised prefixes is below 4,000.</span></span>

<span data-ttu-id="b8dfe-196">다음 예제를 사용하여 기존 회로에 대해 ExpressRoute Premium 추가 기능을 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-196">You can disable the ExpressRoute premium add-on for the existing circuit by using the following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Standard
```

### <a name="to-update-the-expressroute-circuit-bandwidth"></a><span data-ttu-id="b8dfe-197">Express 경로 회로 대역폭을 업데이트하려면</span><span class="sxs-lookup"><span data-stu-id="b8dfe-197">To update the ExpressRoute circuit bandwidth</span></span>

<span data-ttu-id="b8dfe-198">공급자에 대해 지원되는 대역폭 옵션은 [ExpressRoute FAQ](expressroute-faqs.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-198">For the supported bandwidth options for your provider, check the [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="b8dfe-199">기존 회로의 크기보다 큰 모든 크기를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-199">You can pick any size greater than the size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8dfe-200">기존 포트에 적절한 수용작업량이 없는 경우 ExpressRoute 회로를 다시 만들어야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-200">If there is inadequate capacity on the existing port, you may have to recreate the ExpressRoute circuit.</span></span> <span data-ttu-id="b8dfe-201">해당 위치에서 사용 가능한 추가 용량이 없는 경우 해당 회로를 업그레이드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-201">You cannot upgrade the circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="b8dfe-202">그러나 중단 없이 Express 경로 회로의 대역폭을 줄일 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-202">You cannot reduce the bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="b8dfe-203">대역폭을 다운그레이드하려면 ExpressRoute 회로의 프로비전을 해제하고 새 ExpressRoute 회로를 다시 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-203">Downgrading bandwidth requires you to deprovision the ExpressRoute circuit, and then reprovision a new ExpressRoute circuit.</span></span>
>

<span data-ttu-id="b8dfe-204">필요한 크기를 선택한 후에 다음 명령을 사용하여 회로 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-204">After you decide the size you need, use the following command to resize your circuit:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --bandwidth 1000
```

<span data-ttu-id="b8dfe-205">회로의 크기는 Microsoft 쪽에서 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-205">Your circuit is sized up on the Microsoft side.</span></span> <span data-ttu-id="b8dfe-206">다음으로 변경 사항에 맞게 구성을 업데이트하려면 연결 공급자에게 연락해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-206">Next, you must contact your connectivity provider to update configurations on their side to match this change.</span></span> <span data-ttu-id="b8dfe-207">이 알림을 통보하고 나면, 업데이트된 대역폭 옵션에 대한 요금이 청구되기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-207">After you make this notification, we begin billing you for the updated bandwidth option.</span></span>

### <a name="to-move-the-sku-from-metered-to-unlimited"></a><span data-ttu-id="b8dfe-208">SKU를 요금제에서 무제한으로 이동하려면</span><span class="sxs-lookup"><span data-stu-id="b8dfe-208">To move the SKU from metered to unlimited</span></span>

<span data-ttu-id="b8dfe-209">다음 예제를 사용하여 ExpressRoute 회로의 SKU를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-209">You can change the SKU of an ExpressRoute circuit by using the following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-family UnlimitedData
```

### <a name="to-control-access-to-the-classic-and-resource-manager-environments"></a><span data-ttu-id="b8dfe-210">클래식 및 리소스 관리자 환경에 대한 액세스를 제어하려면</span><span class="sxs-lookup"><span data-stu-id="b8dfe-210">To control access to the classic and Resource Manager environments</span></span>

<span data-ttu-id="b8dfe-211">[클래식에서 Resource Manager 배포 모델로 Express 경로 회로 이동](expressroute-howto-move-arm.md)의 지침을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-211">Review the instructions in [Move ExpressRoute circuits from the classic to the Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="b8dfe-212">Express 경로 회로 프로비전 해제 및 삭제</span><span class="sxs-lookup"><span data-stu-id="b8dfe-212">Deprovisioning and deleting an ExpressRoute circuit</span></span>

<span data-ttu-id="b8dfe-213">ExpressRoute 회로의 프로비전을 해제하고 삭제하려면 다음 조건을 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-213">To deprovision and delete an ExpressRoute circuit, make sure you understand the following criteria:</span></span>

* <span data-ttu-id="b8dfe-214">모든 가상 네트워크를 Express 경로 회로에서 연결 해제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-214">You must unlink all virtual networks from the ExpressRoute circuit.</span></span> <span data-ttu-id="b8dfe-215">이 작업에 실패한 경우 회로에 연결된 가상 네트워크가 있는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-215">If this operation fails, check to see if any virtual networks are linked to the circuit.</span></span>
* <span data-ttu-id="b8dfe-216">ExpressRoute 회로 서비스 공급자 프로비전 상태가 **프로비전 중** 또는 **프로비전됨**인 경우에는 서비스 공급자에게 회로 프로비전 해제를 요청해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-216">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned**, you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="b8dfe-217">서비스 공급자가 회로의 프로비전을 해제한 다음 통지를 보낼 때까지 리소스가 계속 예약되며 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-217">We continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="b8dfe-218">서비스 공급자가 회로의 프로비전을 해제하는 경우 회로를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-218">You can delete the circuit if the service provider has deprovisioned the circuit.</span></span> <span data-ttu-id="b8dfe-219">회로의 프로비전이 해제되는 경우 서비스 공급자 프로비전 상태가 **프로비전되지 않음**으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-219">When a circuit is deprovisioned, the service provider provisioning state is set to **Not provisioned**.</span></span> <span data-ttu-id="b8dfe-220">그러면 회로에 대한 요금 청구가 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-220">This stops billing for the circuit.</span></span>

<span data-ttu-id="b8dfe-221">다음 명령을 실행하여 Express 경로 회로를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-221">You can delete your ExpressRoute circuit by running the following command:</span></span>

```azurecli
az network express-route delete  -n MyCircuit -g ExpressRouteResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="b8dfe-222">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b8dfe-222">Next steps</span></span>

<span data-ttu-id="b8dfe-223">회로를 만든 후에 다음 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dfe-223">After you create your circuit, make sure that you do the following tasks:</span></span>

* [<span data-ttu-id="b8dfe-224">Express 경로 회로의 라우팅 만들기 및 수정</span><span class="sxs-lookup"><span data-stu-id="b8dfe-224">Create and modify routing for your ExpressRoute circuit</span></span>](howto-routing-cli.md)
* [<span data-ttu-id="b8dfe-225">가상 네트워크를 Express 경로 회로에 연결</span><span class="sxs-lookup"><span data-stu-id="b8dfe-225">Link your virtual network to your ExpressRoute circuit</span></span>](howto-linkvnet-cli.md)