---
title: "Azure ExpressRoute 회로 만들기 및 수정: CLI | Microsoft Docs"
description: "이 문서에서는 어떻게 toocreate, 프로 비전, 확인, 업데이트, 삭제 및 CLI를 사용 하 여 ExpressRoute 회로 프로 비전 해제를 설명 합니다."
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
ms.openlocfilehash: 396e325658a59afadb209bb525cbb59ac775ae6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-cli"></a><span data-ttu-id="27e30-103">CLI를 사용하여 ExpressRoute 회로 만들기 및 수정</span><span class="sxs-lookup"><span data-stu-id="27e30-103">Create and modify an ExpressRoute circuit using CLI</span></span>


<span data-ttu-id="27e30-104">이 문서에서는 toocreate Azure ExpressRoute 회로 사용 하 여 명령줄 인터페이스 (CLI) hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-104">This article describes how toocreate an Azure ExpressRoute circuit by using hello Command Line Interface (CLI).</span></span> <span data-ttu-id="27e30-105">또한이 문서를 보면 어떻게 toocheck hello 상태 업데이트 또는 삭제 하 고, 회로 프로 비전 해제 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-105">This article also shows you how toocheck hello status, update, or delete and deprovision a circuit.</span></span> <span data-ttu-id="27e30-106">ExpressRoute 회로와 다른 방법 toowork toouse 원한다 면 hello 문서 hello 다음 목록에서에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-106">If you want toouse a different method toowork with ExpressRoute circuits, you can select hello article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="27e30-107">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="27e30-107">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="27e30-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="27e30-108">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="27e30-109">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="27e30-109">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="27e30-110">비디오 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="27e30-110">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="27e30-111">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="27e30-111">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
> 

## <a name="before-you-begin"></a><span data-ttu-id="27e30-112">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="27e30-112">Before you begin</span></span>

* <span data-ttu-id="27e30-113">시작 하기 전에 hello hello CLI 명령 (2.0 이상)의 최신 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-113">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="27e30-114">Hello CLI 명령 설치에 대 한 정보를 참조 하십시오. [Azure CLI 2.0 설치](/cli/azure/install-azure-cli) 및 [Azure CLI 2.0 시작](/cli/azure/get-started-with-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-114">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="27e30-115">검토 hello [필수 구성 요소](expressroute-prerequisites.md) 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="27e30-115">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="27e30-116">Express 경로 회로 만들기 및 프로비전</span><span class="sxs-lookup"><span data-stu-id="27e30-116">Create and provision an ExpressRoute circuit</span></span>

### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a><span data-ttu-id="27e30-117">1. Tooyour Azure 계정에에서 로그인 하 고 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-117">1. Sign in tooyour Azure account and select your subscription</span></span>

<span data-ttu-id="27e30-118">toobegin 구성, tooyour Azure 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-118">toobegin your configuration, sign in tooyour Azure account.</span></span> <span data-ttu-id="27e30-119">예제 toohelp 연결한 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-119">Use hello following examples toohelp you connect:</span></span>

```azurecli
az login
```

<span data-ttu-id="27e30-120">Hello 계정에 대 한 hello 구독을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-120">Check hello subscriptions for hello account.</span></span>

```azurecli
az account list
```

<span data-ttu-id="27e30-121">ExpressRoute 회로 toocreate 원하는 hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-121">Select hello subscription for which you want toocreate an ExpressRoute circuit.</span></span>

```azurecli
az account set --subscription "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="27e30-122">2. 지원 되는 공급자, 위치 및 대역폭 hello 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-122">2. Get hello list of supported providers, locations, and bandwidths</span></span>

<span data-ttu-id="27e30-123">ExpressRoute 회로 만들기 전에 hello 지원 되는 연결 공급자, 위치 및 대역폭 옵션 목록이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-123">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span> <span data-ttu-id="27e30-124">CLI 명령 ' az 네트워크 express 경로 목록-서비스-공급자 ' hello 이후 단계에서 사용 하는이 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-124">hello CLI command 'az network express-route list-service-providers' returns this information, which you’ll use in later steps:</span></span>

```azurecli
az network express-route list-service-providers
```

<span data-ttu-id="27e30-125">hello 응답은 다음 예제와 비슷한 toohello입니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-125">hello response is similar toohello following example:</span></span>

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

<span data-ttu-id="27e30-126">연결 공급자가 나열 하는 경우에 hello 응답 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-126">Check hello response toosee if your connectivity provider is listed.</span></span> <span data-ttu-id="27e30-127">다음 정보는 회로 만들 때 필요 합니다 hello 기록해 두십시오.</span><span class="sxs-lookup"><span data-stu-id="27e30-127">Make a note of hello following information, which you will need when you create a circuit:</span></span>

* <span data-ttu-id="27e30-128">이름</span><span class="sxs-lookup"><span data-stu-id="27e30-128">Name</span></span>
* <span data-ttu-id="27e30-129">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="27e30-129">PeeringLocations</span></span>
* <span data-ttu-id="27e30-130">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="27e30-130">BandwidthsOffered</span></span>

<span data-ttu-id="27e30-131">이제 준비 toocreate ExpressRoute 회로 것입니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-131">You're now ready toocreate an ExpressRoute circuit.</span></span>

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="27e30-132">3. Express 경로 회로 만들기</span><span class="sxs-lookup"><span data-stu-id="27e30-132">3. Create an ExpressRoute circuit</span></span>

> [!IMPORTANT]
> <span data-ttu-id="27e30-133">ExpressRoute 회로 서비스 키를 발급 하는 hello 순간부터 요금이 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-133">Your ExpressRoute circuit is billed from hello moment a service key is issued.</span></span> <span data-ttu-id="27e30-134">Hello 연결 공급자가 준비 tooprovision hello 회로이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-134">Perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="27e30-135">아직 리소스 그룹이 없는 경우 Express 경로 회로를 만들기 전에 먼저 리소스 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-135">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="27e30-136">Hello 다음 명령을 실행 하 여 리소스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-136">You can create a resource group by running hello following command:</span></span>

```azurecli
az group create -n ExpressRouteResourceGroup -l "West US"
```

<span data-ttu-id="27e30-137">다음 예제는 hello Silicon Valley에 Equinix 통해 toocreate 200 50mbps ExpressRoute 회로 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-137">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="27e30-138">다른 공급자와 다른 설정을 사용하는 경우, 요청을 수행할 때 해당 정보를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-138">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> 

<span data-ttu-id="27e30-139">Hello 올바른 SKU 계층과 SKU 제품군을 지정 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-139">Make sure that you specify hello correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="27e30-140">SKU 계층은 Express 경로 표준 또는 Express 경로 Premium 추가 기능이 사용되는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-140">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="27e30-141">Hello premium 추가 기능에 대해 '표준' tooget hello 표준 SKU 또는 '프리미엄'를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-141">You can specify 'Standard' tooget hello standard SKU or 'Premium' for hello premium add-on.</span></span>
* <span data-ttu-id="27e30-142">SKU 제품군 hello 청구 유형을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-142">SKU family determines hello billing type.</span></span> <span data-ttu-id="27e30-143">데이터 요금제의 경우 'Metereddata'를 선택하고 무제한 데이터 요금제의 경우 'Unlimiteddata'를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-143">You can specify 'Metereddata' for a metered data plan and 'Unlimiteddata' for an unlimited data plan.</span></span> <span data-ttu-id="27e30-144">'Metereddata 'too'Unlimiteddata' 있지만 유형을 변경할 수 없습니다 hello too'Metereddata 'Unlimiteddata' 에서' hello 청구 유형을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-144">You can change hello billing type from 'Metereddata' too'Unlimiteddata', but you can't change hello type from 'Unlimiteddata' too'Metereddata'.</span></span>


<span data-ttu-id="27e30-145">ExpressRoute 회로 서비스 키를 발급 하는 hello 순간부터 요금이 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-145">Your ExpressRoute circuit is billed from hello moment a service key is issued.</span></span> <span data-ttu-id="27e30-146">다음 예제는 hello은 새 서비스 키에 대 한 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-146">hello following example is a request for a new service key:</span></span>

```azurecli
az network express-route create --bandwidth 200 -n MyCircuit --peering-location "Silicon Valley" -g ExpressRouteResourceGroup --provider "Equinix" -l "West US" --sku-family MeteredData --sku-tier Standard
```

<span data-ttu-id="27e30-147">hello 응답 hello 서비스 키를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-147">hello response contains hello service key.</span></span>

### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="27e30-148">4. 모든 Express 경로 회로 나열</span><span class="sxs-lookup"><span data-stu-id="27e30-148">4. List all ExpressRoute circuits</span></span>

<span data-ttu-id="27e30-149">사용자가 만든 모든 hello ExpressRoute 회로 목록을 tooget는 hello 'az 네트워크 express 경로 목록' 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-149">tooget a list of all hello ExpressRoute circuits that you created, run hello 'az network express-route list' command.</span></span> <span data-ttu-id="27e30-150">이 명령을 사용하여 이 정보를 언제든지 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-150">You can retrieve this information at any time by using this command.</span></span> <span data-ttu-id="27e30-151">toolist 모든 회로 hello 매개 변수 없이 호출을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-151">toolist all circuits, make hello call with no parameters.</span></span>

```azurecli
az network express-route list
```

<span data-ttu-id="27e30-152">서비스 키 hello에 나열 된 *ServiceKey* hello 응답의 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-152">Your service key is listed in hello *ServiceKey* field of hello response.</span></span>

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

<span data-ttu-id="27e30-153">Hello를 사용 하 여 hello 명령을 실행 하 여 모든 hello 매개 변수에 대 한 자세한 설명을 가져올 수 있습니다 '-h' 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-153">You can get detailed descriptions of all hello parameters by running hello command using hello '-h' parameter.</span></span>

```azurecli
az network express-route list -h
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="27e30-154">5. Hello 서비스 키 tooyour 연결 공급자를 프로 비전에 대 한 보내기</span><span class="sxs-lookup"><span data-stu-id="27e30-154">5. Send hello service key tooyour connectivity provider for provisioning</span></span>

<span data-ttu-id="27e30-155">'ServiceProviderProvisioningState' hello hello 서비스 공급자 쪽에 프로 비전의 현재 상태에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-155">'ServiceProviderProvisioningState' provides information about hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="27e30-156">hello 상태는 Microsoft의 hello에 hello 상태를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-156">hello status provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="27e30-157">자세한 내용은 참조 hello [워크플로 문서](expressroute-workflows.md#expressroute-circuit-provisioning-states)합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-157">For more information, see hello [Workflows article](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span></span>

<span data-ttu-id="27e30-158">새 ExpressRoute 회로 만들 때 hello 회로 hello 다음 상태는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-158">When you create a new ExpressRoute circuit, hello circuit is in hello following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "NotProvisioned"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="27e30-159">hello 회로 toohello hello 연결 공급자를 사용 하면 hello 진행 중인 경우 뒤에 상태를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-159">hello circuit changes toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioning"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="27e30-160">하면 toobe 수 toouse ExpressRoute 회로 hello 상태 뒤에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-160">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioned"
"circuitProvisioningState": "Enabled
```

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="27e30-161">6. Hello 상태 및 hello 회로 키의 hello 상태를 주기적으로 확인</span><span class="sxs-lookup"><span data-stu-id="27e30-161">6. Periodically check hello status and hello state of hello circuit key</span></span>

<span data-ttu-id="27e30-162">Hello 상태 및 hello 회로 키의 hello 상태를 확인 하면 공급자가 회로 설정 하는 때를 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-162">Checking hello status and hello state of hello circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="27e30-163">Hello 회로 구성한 후에 'ServiceProviderProvisioningState' hello 다음 예제와 같이 '프로 비전 됨'으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-163">After hello circuit has been configured, 'ServiceProviderProvisioningState' appears as 'Provisioned', as shown in hello following example:</span></span>

```azurecli
az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
```

<span data-ttu-id="27e30-164">hello 응답은 다음 예제와 비슷한 toohello입니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-164">hello response is similar toohello following example:</span></span>

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

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="27e30-165">7. 라우팅 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="27e30-165">7. Create your routing configuration</span></span>

<span data-ttu-id="27e30-166">단계별 지침은 hello [ExpressRoute 회로 라우팅 구성을](howto-routing-cli.md) toocreate 문서 및 회로 피어 링을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-166">For step-by-step instructions, see hello [ExpressRoute circuit routing configuration](howto-routing-cli.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="27e30-167">이러한 지침은 계층 2 연결 서비스를 제공 하는 서비스 공급자를 사용 하 여 만든 toocircuits만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-167">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="27e30-168">관리된 3계층 서비스(일반적으로 MPLS와 같은 IP VPN)를 제공하는 서비스 공급자를 사용하는 경우 연결 공급자는 사용자를 위해 라우팅을 구성하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-168">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="27e30-169">8. 가상 네트워크 tooan ExpressRoute 회로 연결</span><span class="sxs-lookup"><span data-stu-id="27e30-169">8. Link a virtual network tooan ExpressRoute circuit</span></span>

<span data-ttu-id="27e30-170">다음으로, 가상 네트워크 tooyour ExpressRoute 회로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-170">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="27e30-171">사용 하 여 hello [tooExpressRoute 회로 네트워크 가상 연결](howto-linkvnet-cli.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="27e30-171">Use hello [Linking virtual networks tooExpressRoute circuits](howto-linkvnet-cli.md) article.</span></span>

## <span data-ttu-id="27e30-172"><a name="modify"></a>Express 경로 회로 수정</span><span class="sxs-lookup"><span data-stu-id="27e30-172"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>

<span data-ttu-id="27e30-173">연결에 미치는 영향 없이 Express 경로 회로의 특정 속성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-173">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span> <span data-ttu-id="27e30-174">Hello 가동 중지 시간 없이 변경 내용을 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-174">You can make hello following changes with no downtime:</span></span>

* <span data-ttu-id="27e30-175">ExpressRoute 회로에 대해 ExpressRoute Premium 추가 기능을 사용하거나 사용하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-175">You can enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="27e30-176">제공 된 hello 포트에서 용량은 hello 대역폭의 ExpressRoute 회로 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-176">You can increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="27e30-177">그러나 회로의 대역폭 hello를 다운 그레이드도 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-177">However, downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="27e30-178">데이터 요금 tooUnlimited 데이터에서에서 hello 계량 계획을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-178">You can change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="27e30-179">그러나 hello 계량 데이터가 지원 되지 않습니다 무제한 데이터 요금 tooMetered에서 계획을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-179">However, changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="27e30-180">*Allow Classic Operations*을 활성화하거나 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-180">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="27e30-181">제한 및 제한 사항에 대 한 자세한 내용은 참조 hello [express 경로 FAQ](expressroute-faqs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-181">For more information on limits and limitations, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="27e30-182">tooenable hello ExpressRoute premium 추가 기능</span><span class="sxs-lookup"><span data-stu-id="27e30-182">tooenable hello ExpressRoute premium add-on</span></span>

<span data-ttu-id="27e30-183">다음 명령을 hello를 사용 하 여 기존 회로 대 한 hello ExpressRoute premium 추가 기능을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-183">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following command:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Premium
```

<span data-ttu-id="27e30-184">hello 회로 hello ExpressRoute premium 추가 기능 사용 하도록 설정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-184">hello circuit now has hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="27e30-185">Hello 명령이 성공적으로 실행 되는 즉시 hello premium 추가 기능에 대 한 청구 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-185">We begin billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="27e30-186">toodisable hello ExpressRoute premium 추가 기능</span><span class="sxs-lookup"><span data-stu-id="27e30-186">toodisable hello ExpressRoute premium add-on</span></span>

> [!IMPORTANT]
> <span data-ttu-id="27e30-187">이 작업은 hello 표준 회로 대 한 허용 되는 기능 보다 큰 리소스를 사용 하는 경우 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-187">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

<span data-ttu-id="27e30-188">Hello ExpressRoute premium 추가 기능을 해제 하기 전에 다음 조건을 hello 이해:</span><span class="sxs-lookup"><span data-stu-id="27e30-188">Before disabling hello ExpressRoute premium add-on, understand hello following criteria:</span></span>

* <span data-ttu-id="27e30-189">Toostandard premium에서에서 다운 그레이드 먼저 10 개 미만의 가상 네트워크 연결 된 toohello 회로 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-189">Before you downgrade from premium toostandard, you must make sure that you have fewer than 10 virtual networks linked toohello circuit.</span></span> <span data-ttu-id="27e30-190">10개를 초과하면 업데이트 요청이 실패하고, 프리미엄 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-190">If you have more than 10, your update request fails, and we bill you at premium rates.</span></span>
* <span data-ttu-id="27e30-191">다른 지리적 위치의 모든 가상 네트워크를 연결 해제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-191">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="27e30-192">가상 네트워크의 연결을 해제하지 않으면 업데이트 요청이 실패하고, 프리미엄 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-192">If you don't unlink all your virtual networks, your update request fails and we bill you at premium rates.</span></span>
* <span data-ttu-id="27e30-193">사설 피어링을 위해서는 경로 테이블의 경로가 4000개 미만이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-193">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="27e30-194">경로 테이블 크기가 4, 000 경로 보다 큰 경우 hello BGP 세션을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-194">If your route table size is greater than 4,000 routes, hello BGP session drops.</span></span> <span data-ttu-id="27e30-195">보급된 된 접두사의 hello 수가 4, 000 아래 될 때까지 hello 세션 했다가 다시 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-195">hello session won't be reenabled until hello number of advertised prefixes is below 4,000.</span></span>

<span data-ttu-id="27e30-196">다음 예제는 hello를 사용 하 여 hello 기존 회로 대 한 hello ExpressRoute premium 추가 기능을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-196">You can disable hello ExpressRoute premium add-on for hello existing circuit by using hello following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Standard
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="27e30-197">tooupdate hello ExpressRoute 회로 대역폭</span><span class="sxs-lookup"><span data-stu-id="27e30-197">tooupdate hello ExpressRoute circuit bandwidth</span></span>

<span data-ttu-id="27e30-198">공급자에 대 한 지원 hello 대역폭 옵션에 대 한 확인 hello [express 경로 FAQ](expressroute-faqs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-198">For hello supported bandwidth options for your provider, check hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="27e30-199">기존 회로 hello 크기 보다 큰 모든 크기를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-199">You can pick any size greater than hello size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="27e30-200">기존 포트 hello에 용량이 부족 하면 toorecreate hello ExpressRoute 회로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-200">If there is inadequate capacity on hello existing port, you may have toorecreate hello ExpressRoute circuit.</span></span> <span data-ttu-id="27e30-201">해당 위치에서 사용할 수 없는 추가 용량 있으면 hello 회로 업그레이드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-201">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="27e30-202">Hello 중단 없이 ExpressRoute 회로 대역폭을 줄일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-202">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="27e30-203">대역폭을 다운 그레이드 하면 toodeprovision hello ExpressRoute 회로 차지 하며 다음 새 ExpressRoute 회로 다시 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-203">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit, and then reprovision a new ExpressRoute circuit.</span></span>
>

<span data-ttu-id="27e30-204">필요한 hello 크기를 결정 한 후 다음 명령 tooresize hello 회로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-204">After you decide hello size you need, use hello following command tooresize your circuit:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --bandwidth 1000
```

<span data-ttu-id="27e30-205">회로 hello Microsoft 쪽에서 크기가 조정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-205">Your circuit is sized up on hello Microsoft side.</span></span> <span data-ttu-id="27e30-206">다음으로 문의 해야 해당 측 toomatch 사용자 연결 공급자 tooupdate 구성을이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-206">Next, you must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="27e30-207">이 알림은 변경한 후 업데이트 하는 hello 대역폭 옵션에 대 한 청구 있습니다을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-207">After you make this notification, we begin billing you for hello updated bandwidth option.</span></span>

### <a name="toomove-hello-sku-from-metered-toounlimited"></a><span data-ttu-id="27e30-208">요금제 toounlimited에서 toomove hello SKU</span><span class="sxs-lookup"><span data-stu-id="27e30-208">toomove hello SKU from metered toounlimited</span></span>

<span data-ttu-id="27e30-209">다음 예제는 hello를 사용 하 여 hello ExpressRoute 회로의 SKU를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-209">You can change hello SKU of an ExpressRoute circuit by using hello following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-family UnlimitedData
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a><span data-ttu-id="27e30-210">toocontrol 액세스 toohello 클래식 및 리소스 관리자 환경</span><span class="sxs-lookup"><span data-stu-id="27e30-210">toocontrol access toohello classic and Resource Manager environments</span></span>

<span data-ttu-id="27e30-211">지침에 hello 검토 [hello 클래식 toohello 리소스 관리자 배포 모델의 이동 ExpressRoute 회로](expressroute-howto-move-arm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-211">Review hello instructions in [Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="27e30-212">Express 경로 회로 프로비전 해제 및 삭제</span><span class="sxs-lookup"><span data-stu-id="27e30-212">Deprovisioning and deleting an ExpressRoute circuit</span></span>

<span data-ttu-id="27e30-213">toodeprovision 및 delete ExpressRoute 회로 다음 조건을 hello 이해 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-213">toodeprovision and delete an ExpressRoute circuit, make sure you understand hello following criteria:</span></span>

* <span data-ttu-id="27e30-214">ExpressRoute 회로 hello에서 모든 가상 네트워크 연결을 해제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-214">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="27e30-215">이 작업이 실패 하면 가상 네트워크가 있는 경우 toosee toohello 회로 연결을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-215">If this operation fails, check toosee if any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="27e30-216">Hello ExpressRoute 회로 서비스 공급자의 프로비저닝 상태 이면 **프로 비전** 또는 **프로 비전 됨**, 편인 서비스 공급자 toodeprovision hello 회로 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-216">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned**, you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="27e30-217">Tooreserve 리소스를 계속 하 고 hello 서비스 공급자 프로 비전 해제 hello 회로 완료 하 고 알려주는 될 때까지 사용자를 청구 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-217">We continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="27e30-218">Hello 서비스 공급자가 회로 hello를 프로 비전 해제 하는 경우 hello 회로 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-218">You can delete hello circuit if hello service provider has deprovisioned hello circuit.</span></span> <span data-ttu-id="27e30-219">Hello 서비스 공급자 프로 비전 상태가 너무 회로 프로 비전이 해제 될 때 설정 됩니다**프로 비전 되지**합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-219">When a circuit is deprovisioned, hello service provider provisioning state is set too**Not provisioned**.</span></span> <span data-ttu-id="27e30-220">그러면 hello 회로 대 한 청구 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-220">This stops billing for hello circuit.</span></span>

<span data-ttu-id="27e30-221">Hello 다음 명령을 실행 하 여 ExpressRoute 회로 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-221">You can delete your ExpressRoute circuit by running hello following command:</span></span>

```azurecli
az network express-route delete  -n MyCircuit -g ExpressRouteResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="27e30-222">다음 단계</span><span class="sxs-lookup"><span data-stu-id="27e30-222">Next steps</span></span>

<span data-ttu-id="27e30-223">회로 만든 후 다음 작업 hello 수행 하면 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e30-223">After you create your circuit, make sure that you do hello following tasks:</span></span>

* [<span data-ttu-id="27e30-224">Express 경로 회로의 라우팅 만들기 및 수정</span><span class="sxs-lookup"><span data-stu-id="27e30-224">Create and modify routing for your ExpressRoute circuit</span></span>](howto-routing-cli.md)
* [<span data-ttu-id="27e30-225">가상 네트워크 tooyour ExpressRoute 회로 연결</span><span class="sxs-lookup"><span data-stu-id="27e30-225">Link your virtual network tooyour ExpressRoute circuit</span></span>](howto-linkvnet-cli.md)
