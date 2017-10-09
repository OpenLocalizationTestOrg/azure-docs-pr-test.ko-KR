---
title: "어떻게 tooconfigure Azure ExpressRoute 회로 대 한 라우팅: CLI | Microsoft Docs"
description: "이 문서를 사용 하 여 만들고 hello private, public 및 Microsoft 피어 링 express 경로 회로 프로 비전 할 수 있습니다. 또한이 문서를 보면 toocheck hello 상태 업데이트 또는 회로 대 한 피어 링 삭제 방법을 알 수 있습니다."
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
ms.date: 07/31/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 33130af050045527cdb316e77821c6d101b6a82a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a><span data-ttu-id="3167d-104">CLI를 사용하여 ExpressRoute 회로의 라우팅 만들기 및 수정</span><span class="sxs-lookup"><span data-stu-id="3167d-104">Create and modify routing for an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="3167d-105">이 문서를 사용 하 여 만들고 CLI를 사용 하 여 hello 리소스 관리자 배포 모델의 ExpressRoute 회로 대 한 라우팅 구성을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using CLI.</span></span> <span data-ttu-id="3167d-106">Hello 상태, 업데이트 또는 삭제를 확인 하 고 피어 링 express 경로 회로 대 한 프로 비전을 해제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="3167d-107">다른 방법 toowork toouse 회로 사용 하려는 경우 hello 다음 목록에서에서 아티클을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3167d-108">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="3167d-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="3167d-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3167d-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="3167d-110">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3167d-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="3167d-111">비디오 - 개인 피어링</span><span class="sxs-lookup"><span data-stu-id="3167d-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="3167d-112">비디오 - 공용 피어링</span><span class="sxs-lookup"><span data-stu-id="3167d-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="3167d-113">비디오 - Microsoft 피어링</span><span class="sxs-lookup"><span data-stu-id="3167d-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="3167d-114">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="3167d-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="3167d-115">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="3167d-115">Configuration prerequisites</span></span>

* <span data-ttu-id="3167d-116">시작 하기 전에 hello hello CLI 명령 (2.0 이상)의 최신 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-116">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="3167d-117">Hello CLI 명령 설치에 대 한 정보를 참조 하십시오. [Azure CLI 2.0 설치](/cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-117">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="3167d-118">Hello 검토 했는지 확인 [필수 구성 요소](expressroute-prerequisites.md), [라우팅 요구 사항](expressroute-routing.md), 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflow](expressroute-workflows.md) pages before you begin configuration.</span></span>
* <span data-ttu-id="3167d-119">활성화된 Express 경로 회로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="3167d-120">너무 hello 지침에 따라[ExpressRoute 회로 만들기](howto-circuit-cli.md) 있고 계속 hello 회로 하기 전에 연결 공급자가 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-120">Follow hello instructions too[Create an ExpressRoute circuit](howto-circuit-cli.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="3167d-121">hello ExpressRoute 회로이 문서의에 toobe 수 toorun hello 명령을 가능 하 고 프로 비전 된 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello commands in this article.</span></span>

<span data-ttu-id="3167d-122">이러한 지침은 계층 2 연결 서비스를 제공 하는 서비스 공급자를 사용 하 여 만든 toocircuits만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="3167d-123">관리된 3계층 서비스(일반적으로 MPLS와 같은 IPVPN)를 제공하는 서비스 공급자를 사용하는 경우 연결 공급자는 사용자를 위해 라우팅을 구성하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

<span data-ttu-id="3167d-124">ExpressRoute 회로에 한 가지, 두 가지 또는 세 가지 피어링을 구성할 수 있습니다(Azure 개인, Azure 공용 및 Microsoft).</span><span class="sxs-lookup"><span data-stu-id="3167d-124">You can configure one, two, or all three peerings (Azure private, Azure public, and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="3167d-125">선택한 순서로 피어링을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="3167d-126">그러나 한 번에 하나씩 피어 링의 hello 구성을 완료 되었는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-126">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="3167d-127">Azure 개인 피어링</span><span class="sxs-lookup"><span data-stu-id="3167d-127">Azure private peering</span></span>

<span data-ttu-id="3167d-128">이 섹션을 사용 하면 만들기, 가져오기, 업데이트 및 삭제 hello ExpressRoute 회로 대 한 개인 피어 링 구성을 Azure 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-128">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="3167d-129">Azure 개인 피어 링 toocreate</span><span class="sxs-lookup"><span data-stu-id="3167d-129">toocreate Azure private peering</span></span>

1. <span data-ttu-id="3167d-130">Hello Azure CLI의 최신 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-130">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="3167d-131">Hello hello Azure 명령줄 인터페이스 (CLI)의 최신 버전을 사용 해야 합니다. * 검토 hello [필수 구성 요소](expressroute-prerequisites.md) 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="3167d-131">You must use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="3167d-132">Toocreate ExpressRoute 회로 원하는 hello 구독 선택</span><span class="sxs-lookup"><span data-stu-id="3167d-132">Select hello subscription you want toocreate ExpressRoute circuit</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="3167d-133">Express 경로 회로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-133">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="3167d-134">Hello 지침 toocreate 따라는 [ExpressRoute 회로](howto-circuit-cli.md) hello 연결 공급자가 사용자를 프로 비전 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-134">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="3167d-135">관리 되는 계층 3 서비스를 제공 하는 연결 공급자, 경우에 연결 공급자 tooenable 있습니다에 대 한 피어 링 개인 Azure를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-135">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="3167d-136">이 경우 hello 다음 섹션에 나열 된 toofollow 지침 필요 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-136">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="3167d-137">그러나 연결 공급자 회로 만든 후,에 대 한 라우팅 관리 하지 않는 경우 계속 hello 다음 단계를 사용 하 여 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-137">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="3167d-138">Hello ExpressRoute 회로 toomake 프로 비전 되 고도 사용 하도록 설정 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-138">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="3167d-139">다음 예제는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-139">Use hello following example:</span></span>

  ```azurecli
  az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
  ```

  <span data-ttu-id="3167d-140">hello 응답은 다음 예제와 비슷한 toohello입니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-140">hello response is similar toohello following example:</span></span>

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="3167d-141">Azure 개인 피어 링 hello 회로 대 한 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-141">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="3167d-142">Hello 다음 단계를 진행 하기 전에 다음 항목 hello 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-142">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="3167d-143">/ 30 서브넷 hello 기본 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-143">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="3167d-144">hello 서브넷에 가상 네트워크에 대 한 예약 된 모든 주소 공간의 일부가 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-144">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="3167d-145">/ 30 서브넷 hello 보조 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-145">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="3167d-146">hello 서브넷에 가상 네트워크에 대 한 예약 된 모든 주소 공간의 일부가 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-146">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="3167d-147">유효한 VLAN ID tooestablish이 피어 링을 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-147">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="3167d-148">없는 다른 피어 링 되도록 hello 회로에 사용 하 여 hello 동일한 VLAN ID</span><span class="sxs-lookup"><span data-stu-id="3167d-148">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="3167d-149">피어링에 대한 AS 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-149">AS number for peering.</span></span> <span data-ttu-id="3167d-150">2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-150">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="3167d-151">이 피어링에 개인 AS 숫자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-151">You can use a private AS number for this peering.</span></span> <span data-ttu-id="3167d-152">65515를 사용하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-152">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="3167d-153">**선택 사항-** toouse 하나를 선택 하는 경우 MD5 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-153">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="3167d-154">다음 예에서는 tooconfigure 회로 대 한 피어 링 개인 Azure hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-154">Use hello following example tooconfigure Azure private peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  <span data-ttu-id="3167d-155">Toouse MD5 해시를 선택 하면 다음 예제는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-155">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="3167d-156">고객 ASN이 아닌 피어링 ASN로 AS 번호를 지정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-156">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  > 

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="3167d-157">세부 정보를 피어 링 개인 Azure tooview</span><span class="sxs-lookup"><span data-stu-id="3167d-157">tooview Azure private peering details</span></span>

<span data-ttu-id="3167d-158">다음 예제는 hello를 사용 하 여 구성 세부 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-158">You can get configuration details by using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

<span data-ttu-id="3167d-159">hello 비슷한 toohello 다음은 예제 출력:</span><span class="sxs-lookup"><span data-stu-id="3167d-159">hello output is similar toohello following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePrivatePeering",
  "ipv6PeeringConfig": null,
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePrivatePeering",
  "peerAsn": 7671,
  "peeringType": "AzurePrivatePeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="3167d-160">tooupdate Azure 개인 피어 링 구성</span><span class="sxs-lookup"><span data-stu-id="3167d-160">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="3167d-161">다음 예제는 hello를 사용 하 여 hello 구성의 어떠한 부분을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-161">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="3167d-162">이 예제에서는 100 too500에서 hello hello 회로의 VLAN ID를 업데이트 중입니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-162">In this example, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="3167d-163">Azure 개인 피어 링 toodelete</span><span class="sxs-lookup"><span data-stu-id="3167d-163">toodelete Azure private peering</span></span>

<span data-ttu-id="3167d-164">다음 예제는 hello를 실행 하 여 피어 링 구성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-164">You can remove your peering configuration by running hello following example:</span></span>

> [!WARNING]
> <span data-ttu-id="3167d-165">모든 가상 네트워크 없는지 hello ExpressRoute 회로에서 연결 된이 예제를 실행 하기 전에 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-165">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this example.</span></span> 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a><span data-ttu-id="3167d-166">Azure 공용 피어링</span><span class="sxs-lookup"><span data-stu-id="3167d-166">Azure public peering</span></span>

<span data-ttu-id="3167d-167">이 섹션을 사용 하면 생성, 가져오기, 업데이트 및 삭제 hello ExpressRoute 회로 대 한 Azure 공용 피어 링 구성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-167">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="3167d-168">Azure 공용 피어 링 toocreate</span><span class="sxs-lookup"><span data-stu-id="3167d-168">toocreate Azure public peering</span></span>

1. <span data-ttu-id="3167d-169">Hello Azure CLI의 최신 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-169">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="3167d-170">Hello hello Azure 명령줄 인터페이스 (CLI)의 최신 버전을 사용 해야 합니다. * 검토 hello [필수 구성 요소](expressroute-prerequisites.md) 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="3167d-170">You must use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="3167d-171">ExpressRoute 회로 toocreate 원하는 hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-171">Select hello subscription for which you want toocreate ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="3167d-172">Express 경로 회로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-172">Create an ExpressRoute circuit.</span></span>  <span data-ttu-id="3167d-173">Hello 지침 toocreate 따라는 [ExpressRoute 회로](howto-circuit-cli.md) hello 연결 공급자가 사용자를 프로 비전 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-173">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="3167d-174">연결 공급자가 관리된 3계층 서비스를 제공하는 경우 연결 공급자가 Azure 개인 피어링을 사용하도록 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-174">If your connectivity provider offers managed Layer 3 services, you can request that your connectivity provider enables Azure private peering for you.</span></span> <span data-ttu-id="3167d-175">이 경우 hello 다음 섹션에 나열 된 toofollow 지침 필요 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-175">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="3167d-176">그러나 연결 공급자 회로 만든 후,에 대 한 라우팅 관리 하지 않는 경우 계속 hello 다음 단계를 사용 하 여 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-176">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="3167d-177">Hello ExpressRoute 회로 tooensure 프로 비전 되며 사용 하도록 설정도 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-177">Check hello ExpressRoute circuit tooensure it is provisioned and also enabled.</span></span> <span data-ttu-id="3167d-178">다음 예제는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-178">Use hello following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="3167d-179">hello 응답은 다음 예제와 비슷한 toohello입니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-179">hello response is similar toohello following example:</span></span>

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="3167d-180">Azure 공용 피어 링 hello 회로 대 한 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-180">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="3167d-181">다음 정보를 계속 진행 하기 전에 hello 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-181">Make sure that you have hello following information before you proceed further.</span></span>

  * <span data-ttu-id="3167d-182">/ 30 서브넷 hello 기본 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-182">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="3167d-183">유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-183">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="3167d-184">/ 30 서브넷 hello 보조 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-184">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="3167d-185">유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-185">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="3167d-186">유효한 VLAN ID tooestablish이 피어 링을 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-186">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="3167d-187">없는 다른 피어 링 되도록 hello 회로에 사용 하 여 hello 동일한 VLAN ID</span><span class="sxs-lookup"><span data-stu-id="3167d-187">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="3167d-188">피어링에 대한 AS 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-188">AS number for peering.</span></span> <span data-ttu-id="3167d-189">2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-189">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="3167d-190">**선택 사항-** toouse 하나를 선택 하는 경우 MD5 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-190">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="3167d-191">다음 예에서는 tooconfigure 회로 대 한 피어 링 공용 Azure hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-191">Run hello following example tooconfigure Azure public peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  <span data-ttu-id="3167d-192">Toouse MD5 해시를 선택 하면 다음 예제는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-192">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="3167d-193">고객 ASN이 아닌 피어링 ASN로 AS 번호를 지정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-193">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="3167d-194">세부 정보를 피어 링 공용 Azure tooview</span><span class="sxs-lookup"><span data-stu-id="3167d-194">tooview Azure public peering details</span></span>

<span data-ttu-id="3167d-195">다음 예제는 hello를 사용 하 여 구성 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-195">You can get configuration details using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

<span data-ttu-id="3167d-196">hello 비슷한 toohello 다음은 예제 출력:</span><span class="sxs-lookup"><span data-stu-id="3167d-196">hello output is similar toohello following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePublicPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePublicPeering",
  "peerAsn": 7671,
  "peeringType": "AzurePublicPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="3167d-197">tooupdate Azure 공용 피어 링 구성</span><span class="sxs-lookup"><span data-stu-id="3167d-197">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="3167d-198">다음 예제는 hello를 사용 하 여 hello 구성의 어떠한 부분을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-198">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="3167d-199">이 예제에서는 200 too600에서 hello hello 회로의 VLAN ID를 업데이트 중입니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-199">In this example, hello VLAN ID of hello circuit is being updated from 200 too600.</span></span>

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="3167d-200">Azure 공용 피어 링 toodelete</span><span class="sxs-lookup"><span data-stu-id="3167d-200">toodelete Azure public peering</span></span>

<span data-ttu-id="3167d-201">다음 예제는 hello를 실행 하 여 피어 링 구성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-201">You can remove your peering configuration by running hello following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a><span data-ttu-id="3167d-202">Microsoft 피어링</span><span class="sxs-lookup"><span data-stu-id="3167d-202">Microsoft peering</span></span>

<span data-ttu-id="3167d-203">이 섹션을 사용 하면 생성, 가져오기, 업데이트 및 삭제 hello ExpressRoute 회로 대 한 Microsoft 피어 링 구성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-203">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3167d-204">이전 tooAugust 1에 구성 된 ExpressRoute 회로의 Microsoft 피어 링, 경로 필터 정의 되어 있지 않은 경우에 2017 hello Microsoft 피어 링을 통해 보급 되는 모든 서비스 접두사를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-204">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="3167d-205">Microsoft 또는 그 이후에 2017 년 8 월 1 구성한 ExpressRoute 회로의 피어 링 수는 없습니다 모든 접두사 필터는 연결 될 때까지 보급 toohello 회로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-205">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="3167d-206">자세한 내용은 [Microsoft 피어링에 경로 필터 구성](how-to-routefilter-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3167d-206">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="3167d-207">toocreate Microsoft 피어 링</span><span class="sxs-lookup"><span data-stu-id="3167d-207">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="3167d-208">Hello Azure CLI의 최신 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-208">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="3167d-209">사용 하 여 hello 최신 버전의 hello Azure 명령줄 인터페이스 (CLI). * 검토 hello [필수 구성 요소](expressroute-prerequisites.md) 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="3167d-209">Use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="3167d-210">ExpressRoute 회로 toocreate 원하는 hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-210">Select hello subscription for which you want toocreate ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="3167d-211">Express 경로 회로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-211">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="3167d-212">Hello 지침 toocreate 따라는 [ExpressRoute 회로](howto-circuit-cli.md) hello 연결 공급자가 사용자를 프로 비전 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-212">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="3167d-213">관리 되는 계층 3 서비스를 제공 하는 연결 공급자, 경우에 연결 공급자 tooenable 있습니다에 대 한 피어 링 개인 Azure를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-213">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="3167d-214">이 경우 hello 다음 섹션에 나열 된 toofollow 지침 필요 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-214">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="3167d-215">그러나 연결 공급자 회로 만든 후,에 대 한 라우팅 관리 하지 않는 경우 계속 hello 다음 단계를 사용 하 여 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-215">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>

3. <span data-ttu-id="3167d-216">Hello ExpressRoute 회로 toomake 프로 비전 되 고도 사용 하도록 설정 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-216">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="3167d-217">다음 예제는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-217">Use hello following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="3167d-218">hello 응답은 다음 예제와 비슷한 toohello입니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-218">hello response is similar toohello following example:</span></span>

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="3167d-219">Microsoft hello 회로 대 한 피어 링을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-219">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="3167d-220">계속 하기 전에 정보 다음 hello 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-220">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="3167d-221">/ 30 서브넷 hello 기본 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-221">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="3167d-222">사용자가 소유하고 RIR/IRR에 등록된 유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-222">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="3167d-223">/ 30 서브넷 hello 보조 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-223">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="3167d-224">사용자가 소유하고 RIR/IRR에 등록된 유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-224">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="3167d-225">유효한 VLAN ID tooestablish이 피어 링을 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-225">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="3167d-226">없는 다른 피어 링 되도록 hello 회로에 사용 하 여 hello 동일한 VLAN ID</span><span class="sxs-lookup"><span data-stu-id="3167d-226">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="3167d-227">피어링에 대한 AS 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-227">AS number for peering.</span></span> <span data-ttu-id="3167d-228">2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-228">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="3167d-229">접두사를 보급: 목록을 제공 해야 모든 접두사의 hello BGP 세션을 통해 tooadvertise 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-229">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="3167d-230">공용 IP 주소 접두사만 수락됩니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-230">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="3167d-231">Toosend 접두사를 사용 하도록 하려는 경우 쉼표로 구분 된 목록을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-231">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="3167d-232">이 접두사는 RIR에 등록 된 tooyou 여야 / IRR입니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-232">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="3167d-233">**선택 사항-** 고객 ASN: 광고 접두사 수로 등록 된 toohello 피어 링 되지 않은 경우 등록 된 숫자 toowhich로 hello를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-233">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="3167d-234">라우팅 레지스트리 이름을: hello RIR 지정할 수 있습니다는 hello에 대 한 번호 매기기로이 앞에 추가 IRR를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-234">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="3167d-235">**선택 사항-** toouse 하나를 선택 하는 경우 MD5 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-235">**Optional -** An MD5 hash if you choose toouse one.</span></span>

   <span data-ttu-id="3167d-236">다음 예에서는 tooconfigure Microsoft 피어 링 회로 대 한 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-236">Run hello following example tooconfigure Microsoft peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="tooget-microsoft-peering-details"></a><span data-ttu-id="3167d-237">tooget Microsoft 피어 링 세부 정보</span><span class="sxs-lookup"><span data-stu-id="3167d-237">tooget Microsoft peering details</span></span>

<span data-ttu-id="3167d-238">다음 예제는 hello를 사용 하 여 구성 세부 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-238">You can get configuration details by using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

<span data-ttu-id="3167d-239">hello 비슷한 toohello 다음은 예제 출력:</span><span class="sxs-lookup"><span data-stu-id="3167d-239">hello output is similar toohello following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzureMicrosoftPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": {
    "advertisedPublicPrefixes": [
        ""
      ],
     "advertisedPublicPrefixesState": "",
     "customerASN": ,
     "routingRegistryName": ""
  }
  "name": "AzureMicrosoftPeering",
  "peerAsn": ,
  "peeringType": "AzureMicrosoftPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="3167d-240">tooupdate Microsoft 피어 링 구성</span><span class="sxs-lookup"><span data-stu-id="3167d-240">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="3167d-241">Hello 구성의 어떠한 부분을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-241">You can update any part of hello configuration.</span></span> <span data-ttu-id="3167d-242">hello 보급 hello 다음 예제에서에서 123.1.0.0/24 too124.1.0.0/24에서 hello 회로의 접두사를 업데이트 하는 중:</span><span class="sxs-lookup"><span data-stu-id="3167d-242">hello advertised prefixes of hello circuit are being updated from 123.1.0.0/24 too124.1.0.0/24 in hello following example:</span></span>

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="3167d-243">toodelete Microsoft 피어 링</span><span class="sxs-lookup"><span data-stu-id="3167d-243">toodelete Microsoft peering</span></span>

<span data-ttu-id="3167d-244">다음 예제는 hello를 실행 하 여 피어 링 구성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-244">You can remove your peering configuration by running hello following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a><span data-ttu-id="3167d-245">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3167d-245">Next steps</span></span>

<span data-ttu-id="3167d-246">다음 단계 [연결할 ExpressRoute 회로 VNet tooan](howto-linkvnet-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3167d-246">Next step, [Link a VNet tooan ExpressRoute circuit](howto-linkvnet-cli.md).</span></span>

* <span data-ttu-id="3167d-247">Express 경로 워크플로에 대한 자세한 내용은 [Express 경로 워크플로](expressroute-workflows.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3167d-247">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="3167d-248">회로 피어링에 대한 자세한 내용은 [Express 경로 회로 및 라우팅 도메인](expressroute-circuit-peerings.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3167d-248">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="3167d-249">가상 네트워크 작업에 대한 자세한 내용은 [가상 네트워크 개요](../virtual-network/virtual-networks-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3167d-249">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>