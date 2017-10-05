---
title: "Azure Network Watcher 토폴로지 보기 - REST API | Microsoft Docs"
description: "이 문서에서는 REST API를 사용하여 네트워크 토폴로지를 쿼리하는 방법을 설명합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: de9af643-aea1-4c4c-89c5-21f1bf334c06
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 568f3060da372f4a08cec342e04359172522cb69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="view-network-watcher-topology-with-rest-api"></a><span data-ttu-id="a472e-103">REST API를 사용하여 Network Watcher 토폴로지 보기</span><span class="sxs-lookup"><span data-stu-id="a472e-103">View Network Watcher topology with REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a472e-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a472e-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="a472e-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a472e-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="a472e-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a472e-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="a472e-107">REST API</span><span class="sxs-lookup"><span data-stu-id="a472e-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="a472e-108">Network Watcher의 토폴로지 기능은 구독에 있는 네트워크 리소스의 시각적 표현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-108">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="a472e-109">포털에서 이 시각화가 자동으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-109">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="a472e-110">PowerShell을 통해 포털에 있는 토폴로지 보기 이외의 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-110">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="a472e-111">다른 도구에서 데이터를 사용하여 시각화를 빌드할 수 있는 것처럼 이 기능을 사용하면 토폴로지 정보를 다양하게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-111">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="a472e-112">상호 연결은 두 개의 관계에서 모델링됩니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-112">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="a472e-113">**포함** - 예: VNet은 서브넷을 포함하고 NIC를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="a472e-114">**연결됨** -예제: NIC는 VM과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="a472e-115">다음 목록은 토폴로지 REST API를 쿼리할 때 반환되는 속성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-115">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="a472e-116">**name** - 리소스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-116">**name** - The name of the resource</span></span>
* <span data-ttu-id="a472e-117">**id** - 리소스 그룹의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-117">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="a472e-118">**location** - 리소스가 있는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-118">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="a472e-119">**associations** - 참조되는 개체에 대한 연결 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-119">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="a472e-120">**name** - 참조되는 리소스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-120">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="a472e-121">**resourceId** - resourceId는 연결에서 참조되는 리소스의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-121">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="a472e-122">**associationType** - 이 값은 하위 개체 및 상위 개체 간의 관계를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-122">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="a472e-123">유효한 값은 **포함** 또는 **관련됨**입니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a472e-124">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="a472e-124">Before you begin</span></span>

<span data-ttu-id="a472e-125">이 시나리오에서는 토폴로지 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-125">In this scenario, you retrieve the topology information.</span></span> <span data-ttu-id="a472e-126">PowerShell을 사용하여 REST API를 호출하는 데 ARMclient가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-126">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="a472e-127">ARMClient는 [Chocolatey의 ARMClient](https://chocolatey.org/packages/ARMClient)에서 chocolatey에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-127">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="a472e-128">이 시나리오에서는 사용자가 Network Watcher를 만드는 [Network Watcher 만들기](network-watcher-create.md)의 단계를 이미 수행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-128">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="a472e-129">시나리오</span><span class="sxs-lookup"><span data-stu-id="a472e-129">Scenario</span></span>

<span data-ttu-id="a472e-130">이 문서에서 다루는 시나리오는 지정된 리소스 그룹에 대한 토폴로지 응답을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-130">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="a472e-131">ARMClient에 로그인</span><span class="sxs-lookup"><span data-stu-id="a472e-131">Log in with ARMClient</span></span>

<span data-ttu-id="a472e-132">Azure 자격 증명으로 armclient에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-132">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a><span data-ttu-id="a472e-133">토폴로지 검색</span><span class="sxs-lookup"><span data-stu-id="a472e-133">Retrieve topology</span></span>

<span data-ttu-id="a472e-134">다음 예제는 REST API에서 토폴로지를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-134">The following example requests the topology from the REST API.</span></span>  <span data-ttu-id="a472e-135">이 예제는 예제를 만드는 데 유연성을 허용하도록 매개 변수화됩니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-135">The example is parameterized to allow for flexibility in creating an example.</span></span>  <span data-ttu-id="a472e-136">모든 값을 \< \>로 둘러싸인 모든 값을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-136">Replace all values with \< \> surrounding them.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name to run topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

<span data-ttu-id="a472e-137">다음 응답은 리소스 그룹에 대해 토폴로지를 검색할 때 반환되는 축약된 응답의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="a472e-137">The following response is an example of a shortened response that is returned when retrieve topology for a resourcegroup:</span></span>

```json
{
  "id": "ecd6c860-9cf5-411a-bdba-512f8df7799f",
  "createdDateTime": "2017-01-18T04:13:07.1974591Z",
  "lastModified": "2017-01-17T22:11:52.3527348Z",
  "resources": [
    {
      "name": "virtualNetwork1",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/{virtualNetworkName}",
      "location": "westcentralus",
      "associations": [
        {
          "name": "{subnetName}",
          "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/(virtualNetworkName)/subnets
/{subnetName}",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "webtestnsg-wjplxls65qcto",
      "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}
s65qcto",
      "associationType": "Associated"
    },
    ...
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="a472e-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a472e-138">Next steps</span></span>

<span data-ttu-id="a472e-139">[PowerBI에서 NSG 흐름 로그 시각화](network-watcher-visualize-nsg-flow-logs-power-bi.md)에서 Power BI로 NSG 흐름 로그를 시각화하는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="a472e-139">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

