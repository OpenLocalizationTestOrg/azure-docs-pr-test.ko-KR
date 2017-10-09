---
title: "aaaView Azure 네트워크 감시자 토폴로지-REST API | Microsoft Docs"
description: "이 문서는 어떻게 toouse REST API tooquery 네트워크 토폴로지에 대해 설명 합니다."
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
ms.openlocfilehash: 39292025bcd561f007c9e31271b1389be48ea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-rest-api"></a><span data-ttu-id="a58fe-103">REST API를 사용하여 Network Watcher 토폴로지 보기</span><span class="sxs-lookup"><span data-stu-id="a58fe-103">View Network Watcher topology with REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a58fe-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a58fe-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="a58fe-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a58fe-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="a58fe-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a58fe-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="a58fe-107">REST API</span><span class="sxs-lookup"><span data-stu-id="a58fe-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="a58fe-108">네트워크 감시자의 hello 토폴로지 기능 구독의 hello 네트워크 리소스의 시각적 표현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a58fe-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="a58fe-109">Hello 포털에서이 시각화에서 tooyou는 자동으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a58fe-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="a58fe-110">PowerShell을 통해 hello 포털에서 hello 토폴로지 보기 이면 hello 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a58fe-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="a58fe-111">이 기능을 사용 하면 hello 토폴로지 정보를 다양 하 게 만들 hello 데이터 hello 시각화 아웃 다른 도구 toobuild에서 소비 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a58fe-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="a58fe-112">hello 연결로 두 개의 관계에서 모델링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a58fe-112">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="a58fe-113">**포함** - 예: VNet은 서브넷을 포함하고 NIC를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a58fe-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="a58fe-114">**연결됨** -예제: NIC는 VM과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a58fe-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="a58fe-115">hello 다음 목록은 hello 토폴로지 REST API를 쿼리할 때 반환 되는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a58fe-115">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="a58fe-116">**이름** -hello hello 리소스의 이름</span><span class="sxs-lookup"><span data-stu-id="a58fe-116">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="a58fe-117">**id** -hello hello 리소스의 uri입니다.</span><span class="sxs-lookup"><span data-stu-id="a58fe-117">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="a58fe-118">**위치** -hello hello 리소스 있는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="a58fe-118">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="a58fe-119">**연결** -연결 toohello 목록이 참조 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a58fe-119">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="a58fe-120">**이름** -hello의 hello 이름이 리소스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="a58fe-120">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="a58fe-121">**resourceId** -hello resourceId hello 연결에서 참조 하는 hello 리소스의 hello uri입니다.</span><span class="sxs-lookup"><span data-stu-id="a58fe-121">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="a58fe-122">**associationType** -이 값 hello hello 자식 개체와 hello 부모 관계를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="a58fe-122">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="a58fe-123">유효한 값은 **포함** 또는 **관련됨**입니다.</span><span class="sxs-lookup"><span data-stu-id="a58fe-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a58fe-124">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="a58fe-124">Before you begin</span></span>

<span data-ttu-id="a58fe-125">이 시나리오에서는 hello 토폴로지 정보를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="a58fe-125">In this scenario, you retrieve hello topology information.</span></span> <span data-ttu-id="a58fe-126">ARMclient는 PowerShell을 사용 하 여 사용 되는 toocall hello REST API입니다.</span><span class="sxs-lookup"><span data-stu-id="a58fe-126">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="a58fe-127">ARMClient는 [Chocolatey의 ARMClient](https://chocolatey.org/packages/ARMClient)에서 chocolatey에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a58fe-127">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="a58fe-128">이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다.</span><span class="sxs-lookup"><span data-stu-id="a58fe-128">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="a58fe-129">시나리오</span><span class="sxs-lookup"><span data-stu-id="a58fe-129">Scenario</span></span>

<span data-ttu-id="a58fe-130">이 문서에서 다루는 hello 시나리오는 해당된 리소스 그룹에 대 한 hello 토폴로지 응답을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="a58fe-130">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="a58fe-131">ARMClient에 로그인</span><span class="sxs-lookup"><span data-stu-id="a58fe-131">Log in with ARMClient</span></span>

<span data-ttu-id="a58fe-132">Tooarmclient Azure 자격 증명으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a58fe-132">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a><span data-ttu-id="a58fe-133">토폴로지 검색</span><span class="sxs-lookup"><span data-stu-id="a58fe-133">Retrieve topology</span></span>

<span data-ttu-id="a58fe-134">다음 예제는 hello hello REST API에서에서 hello 토폴로지를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="a58fe-134">hello following example requests hello topology from hello REST API.</span></span>  <span data-ttu-id="a58fe-135">hello 예는 예제를 만들 유연성에 대 한 매개 변수가 있는 tooallow입니다.</span><span class="sxs-lookup"><span data-stu-id="a58fe-135">hello example is parameterized tooallow for flexibility in creating an example.</span></span>  <span data-ttu-id="a58fe-136">모든 값을 \< \>로 둘러싸인 모든 값을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="a58fe-136">Replace all values with \< \> surrounding them.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name toorun topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

<span data-ttu-id="a58fe-137">다음 응답 hello은는 리소스 그룹에 대 한 토폴로지를 검색 하는 경우 반환 되는 축약된 된 응답의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="a58fe-137">hello following response is an example of a shortened response that is returned when retrieve topology for a resourcegroup:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a58fe-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a58fe-138">Next steps</span></span>

<span data-ttu-id="a58fe-139">Toovisualize NSG 흐름 기록 하는 방법을 Power BI를 방문 하 여 자세한 [NSG 시각화할 Power BI를 사용 하 여 로그 전달](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="a58fe-139">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

