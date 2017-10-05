---
title: "Azure Network Watcher 토폴로지 보기 - Azure CLI 1.0 | Microsoft Docs"
description: "이 문서에서는 Azure CLI 1.0을 사용하여 네트워크 토폴로지를 쿼리하는 방법을 설명합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 5cd279d7-3ab0-4813-aaa4-6a648bf74e7b
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 9178c485a92e04564c95dae8073f045b5c639bb7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="view-network-watcher-topology-with-azure-cli-10"></a><span data-ttu-id="d3c1f-103">Azure CLI 1.0을 사용하여 Network Watcher 토폴로지 보기</span><span class="sxs-lookup"><span data-stu-id="d3c1f-103">View Network Watcher topology with Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="d3c1f-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3c1f-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="d3c1f-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d3c1f-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="d3c1f-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d3c1f-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="d3c1f-107">REST API</span><span class="sxs-lookup"><span data-stu-id="d3c1f-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="d3c1f-108">Network Watcher의 토폴로지 기능은 구독에 있는 네트워크 리소스의 시각적 표현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1f-108">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="d3c1f-109">포털에서 이 시각화가 자동으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1f-109">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="d3c1f-110">PowerShell을 통해 포털에 있는 토폴로지 보기 이외의 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1f-110">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="d3c1f-111">다른 도구에서 데이터를 사용하여 시각화를 빌드할 수 있는 것처럼 이 기능을 사용하면 토폴로지 정보를 다양하게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1f-111">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="d3c1f-112">이 문서에서는 Windows, Mac 및 Linux에 사용할 수 있는 플랫폼 간 Azure CLI 1.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1f-112">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> 

<span data-ttu-id="d3c1f-113">상호 연결은 두 개의 관계에서 모델링됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1f-113">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="d3c1f-114">**포함** - 예: VNet은 서브넷을 포함하고 NIC를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1f-114">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="d3c1f-115">**연결됨** -예제: NIC는 VM과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1f-115">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="d3c1f-116">다음 목록은 토폴로지 REST API를 쿼리할 때 반환되는 속성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1f-116">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="d3c1f-117">**name** - 리소스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1f-117">**name** - The name of the resource</span></span>
* <span data-ttu-id="d3c1f-118">**id** - 리소스 그룹의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1f-118">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="d3c1f-119">**location** - 리소스가 있는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1f-119">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="d3c1f-120">**associations** - 참조되는 개체에 대한 연결 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1f-120">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="d3c1f-121">**name** - 참조되는 리소스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1f-121">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="d3c1f-122">**resourceId** - resourceId는 연결에서 참조되는 리소스의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1f-122">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="d3c1f-123">**associationType** - 이 값은 하위 개체 및 상위 개체 간의 관계를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1f-123">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="d3c1f-124">유효한 값은 **포함** 또는 **관련됨**입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1f-124">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d3c1f-125">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="d3c1f-125">Before you begin</span></span>

<span data-ttu-id="d3c1f-126">이 시나리오에서는 `network watcher topology` cmdlet을 사용하여 토폴로지 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1f-126">In this scenario, you use the `network watcher topology` cmdlet to retrieve the topology information.</span></span> <span data-ttu-id="d3c1f-127">[REST API를 사용하여 네트워크 토폴로지를 검색](network-watcher-topology-rest.md)하는 방법에 대한 문서도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1f-127">There is also an article on how to [retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="d3c1f-128">이 시나리오에서는 사용자가 Network Watcher를 만드는 [Network Watcher 만들기](network-watcher-create.md)의 단계를 이미 수행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1f-128">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="d3c1f-129">시나리오</span><span class="sxs-lookup"><span data-stu-id="d3c1f-129">Scenario</span></span>

<span data-ttu-id="d3c1f-130">이 문서에서 다루는 시나리오는 지정된 리소스 그룹에 대한 토폴로지 응답을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1f-130">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="retrieve-topology"></a><span data-ttu-id="d3c1f-131">토폴로지 검색</span><span class="sxs-lookup"><span data-stu-id="d3c1f-131">Retrieve topology</span></span>

<span data-ttu-id="d3c1f-132">`network watcher topology` cmdlet은 지정된 리소스 그룹에 대한 토폴로지를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1f-132">The `network watcher topology` cmdlet retrieves the topology for a given resource group.</span></span> <span data-ttu-id="d3c1f-133">"-json" 인수를 추가하여 json 형식인 출력을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1f-133">Add the argument "--json" to view the oput in json format</span></span>

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a><span data-ttu-id="d3c1f-134">결과</span><span class="sxs-lookup"><span data-stu-id="d3c1f-134">Results</span></span>

<span data-ttu-id="d3c1f-135">반환된 결과에는 "리소스" 속성 이름이 있으며 여기에는 `network watcher topology` cmdlet에 대한 json 응답 본문이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1f-135">The results returned have a property name "Resources", which contains the json response body for the `network watcher topology` cmdlet.</span></span>  <span data-ttu-id="d3c1f-136">응답은 네트워크 보안 그룹 및 해당 연결에 있는 리소스를 포함합니다(즉, 포함 및 연결됨).</span><span class="sxs-lookup"><span data-stu-id="d3c1f-136">The response contains the resources in the Network Security Group and their associations (that is, Contains, Associated).</span></span>

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "createdDateTime": "2017-02-17T22:20:59.461Z",
  "lastModified": "2016-12-19T22:23:02.546Z",
  "resources": [
    {
      "name": "testrg-vnet",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
      "location": "westcentralus",
      "associations": [
        {
          "name": "default",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "default",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
      "location": "westcentralus",
      "associations": []
    },
    {
      "name": "testclient",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testclient",
      "location": "westcentralus",
      "associations": [
        {
          "name": "testNic",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testNic",
          "associationType": "Contains"
        }
      ]
    },
    ...    
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="d3c1f-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d3c1f-137">Next steps</span></span>

<span data-ttu-id="d3c1f-138">[보안 그룹 개요 보기](network-watcher-security-group-view-overview.md)를 방문하여 네트워크 리소스에 적용되는 보안 규칙에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1f-138">Learn more about the security rules that are applied to your network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
