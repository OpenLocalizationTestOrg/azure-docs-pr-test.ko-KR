---
title: "Azure Network Watcher 토폴로지 보기 - PowerShell | Microsoft Docs"
description: "이 문서에서는 PowerShell을 사용하여 네트워크 토폴로지를 쿼리하는 방법을 설명합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: bd0e882d-8011-45e8-a7ce-de231a69fb85
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 40e01a7a6a2ea6127ab725f04649cec47b9d9422
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a><span data-ttu-id="f91ce-103">PowerShell을 사용하여 Network Watcher 토폴로지 보기</span><span class="sxs-lookup"><span data-stu-id="f91ce-103">View Network Watcher topology with PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="f91ce-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f91ce-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="f91ce-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f91ce-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="f91ce-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f91ce-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="f91ce-107">REST API</span><span class="sxs-lookup"><span data-stu-id="f91ce-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="f91ce-108">Network Watcher의 토폴로지 기능은 구독에 있는 네트워크 리소스의 시각적 표현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f91ce-108">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="f91ce-109">포털에서 이 시각화가 자동으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f91ce-109">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="f91ce-110">PowerShell을 통해 포털에 있는 토폴로지 보기 이외의 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f91ce-110">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="f91ce-111">다른 도구에서 데이터를 사용하여 시각화를 빌드할 수 있는 것처럼 이 기능을 사용하면 토폴로지 정보를 다양하게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f91ce-111">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="f91ce-112">상호 연결은 두 개의 관계에서 모델링됩니다.</span><span class="sxs-lookup"><span data-stu-id="f91ce-112">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="f91ce-113">**포함** - 예: VNet은 서브넷을 포함하고 NIC를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f91ce-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="f91ce-114">**연결됨** -예제: NIC는 VM과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="f91ce-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="f91ce-115">다음 목록은 토폴로지 REST API를 쿼리할 때 반환되는 속성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f91ce-115">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="f91ce-116">**name** - 리소스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f91ce-116">**name** - The name of the resource</span></span>
* <span data-ttu-id="f91ce-117">**id** - 리소스 그룹의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="f91ce-117">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="f91ce-118">**location** - 리소스가 있는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="f91ce-118">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="f91ce-119">**associations** - 참조되는 개체에 대한 연결 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="f91ce-119">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="f91ce-120">**name** - 참조되는 리소스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f91ce-120">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="f91ce-121">**resourceId** - resourceId는 연결에서 참조되는 리소스의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="f91ce-121">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="f91ce-122">**associationType** - 이 값은 하위 개체 및 상위 개체 간의 관계를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="f91ce-122">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="f91ce-123">유효한 값은 **포함** 또는 **관련됨**입니다.</span><span class="sxs-lookup"><span data-stu-id="f91ce-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f91ce-124">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="f91ce-124">Before you begin</span></span>

<span data-ttu-id="f91ce-125">이 시나리오에서는 `Get-AzureRmNetworkWatcherTopology` cmdlet을 사용하여 토폴로지 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f91ce-125">In this scenario, you use the `Get-AzureRmNetworkWatcherTopology` cmdlet to retrieve the topology information.</span></span> <span data-ttu-id="f91ce-126">[REST API를 사용하여 네트워크 토폴로지를 검색](network-watcher-topology-rest.md)하는 방법에 대한 문서도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f91ce-126">There is also an article on how to [retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="f91ce-127">이 시나리오에서는 사용자가 Network Watcher를 만드는 [Network Watcher 만들기](network-watcher-create.md)의 단계를 이미 수행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f91ce-127">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="f91ce-128">시나리오</span><span class="sxs-lookup"><span data-stu-id="f91ce-128">Scenario</span></span>

<span data-ttu-id="f91ce-129">이 문서에서 다루는 시나리오는 지정된 리소스 그룹에 대한 토폴로지 응답을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f91ce-129">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="f91ce-130">Network Watcher 검색</span><span class="sxs-lookup"><span data-stu-id="f91ce-130">Retrieve Network Watcher</span></span>

<span data-ttu-id="f91ce-131">첫 번째 단계는 Network Watcher 인스턴스를 검색하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f91ce-131">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="f91ce-132">`$networkWatcher` 변수는 `Get-AzureRmNetworkWatcherTopology` cmdlet으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="f91ce-132">The `$networkWatcher` variable is passed to the `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a><span data-ttu-id="f91ce-133">토폴로지 검색</span><span class="sxs-lookup"><span data-stu-id="f91ce-133">Retrieve topology</span></span>

<span data-ttu-id="f91ce-134">`Get-AzureRmNetworkWatcherTopology` cmdlet은 지정된 리소스 그룹에 대한 토폴로지를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f91ce-134">The `Get-AzureRmNetworkWatcherTopology` cmdlet retrieves the topology for a given resource group.</span></span>

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a><span data-ttu-id="f91ce-135">결과</span><span class="sxs-lookup"><span data-stu-id="f91ce-135">Results</span></span>

<span data-ttu-id="f91ce-136">반환된 결과에는 "리소스" 속성 이름이 있으며 여기에는 `Get-AzureRmNetworkWatcherTopology` cmdlet에 대한 json 응답 본문이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f91ce-136">The results returned have a property name "Resources", which contains the json response body for the `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>  <span data-ttu-id="f91ce-137">응답은 네트워크 보안 그룹 및 해당 연결에 있는 리소스를 포함합니다(즉, 포함 및 연결됨).</span><span class="sxs-lookup"><span data-stu-id="f91ce-137">The response contains the resources in the Network Security Group and their associations (that is, Contains, Associated).</span></span>

```json
Id              : 00000000-0000-0000-0000-000000000000
CreatedDateTime : 2/1/2017 7:52:21 PM
LastModified    : 2/1/2017 7:46:18 PM
Resources       : [
                    {
                      "Name": "testrg-vnet",
                      "Id":
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet/subnets/default"
                        }
                      ]
                    },
                    {
                      "Name": "default",
                      "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testr
                  g-vnet/subnets/default",
                      "Location": "westcentralus",
                      "Associations": []
                    },
                    {
                      "Name": "testrg-vnet2",
                      "Id": 
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet2",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/default"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "GatewaySubnet",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/GatewaySubnet"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "gateway2",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworkGateways/gateway2"
                        }
                      ]
                    },
                    ...
                  ]
```

## <a name="next-steps"></a><span data-ttu-id="f91ce-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f91ce-138">Next steps</span></span>

<span data-ttu-id="f91ce-139">[PowerBI에서 NSG 흐름 로그 시각화](network-watcher-visualize-nsg-flow-logs-power-bi.md)에서 Power BI로 NSG 흐름 로그를 시각화하는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="f91ce-139">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


