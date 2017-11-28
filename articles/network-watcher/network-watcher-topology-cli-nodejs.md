---
title: "aaaView Azure 네트워크 감시자 토폴로지-Azure CLI 1.0 | Microsoft Docs"
description: "에서는이 문서에 설명 방법을 toouse Azure CLI 1.0 tooquery 네트워크 토폴로지입니다."
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
ms.openlocfilehash: 30679d6dc74e85bacfc86c63bd1afa873893c772
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-azure-cli-10"></a><span data-ttu-id="d08e6-103">Azure CLI 1.0을 사용하여 Network Watcher 토폴로지 보기</span><span class="sxs-lookup"><span data-stu-id="d08e6-103">View Network Watcher topology with Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="d08e6-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d08e6-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="d08e6-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d08e6-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="d08e6-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d08e6-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="d08e6-107">REST API</span><span class="sxs-lookup"><span data-stu-id="d08e6-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="d08e6-108">네트워크 감시자의 hello 토폴로지 기능 구독의 hello 네트워크 리소스의 시각적 표현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d08e6-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="d08e6-109">Hello 포털에서이 시각화에서 tooyou는 자동으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d08e6-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="d08e6-110">PowerShell을 통해 hello 포털에서 hello 토폴로지 보기 이면 hello 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d08e6-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="d08e6-111">이 기능을 사용 하면 hello 토폴로지 정보를 다양 하 게 만들 hello 데이터 hello 시각화 아웃 다른 도구 toobuild에서 소비 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d08e6-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="d08e6-112">이 문서에서는 Windows, Mac 및 Linux에 사용할 수 있는 플랫폼 간 Azure CLI 1.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d08e6-112">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> 

<span data-ttu-id="d08e6-113">hello 연결로 두 개의 관계에서 모델링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d08e6-113">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="d08e6-114">**포함** - 예: VNet은 서브넷을 포함하고 NIC를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d08e6-114">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="d08e6-115">**연결됨** -예제: NIC는 VM과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="d08e6-115">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="d08e6-116">hello 다음 목록은 hello 토폴로지 REST API를 쿼리할 때 반환 되는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d08e6-116">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="d08e6-117">**이름** -hello hello 리소스의 이름</span><span class="sxs-lookup"><span data-stu-id="d08e6-117">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="d08e6-118">**id** -hello hello 리소스의 uri입니다.</span><span class="sxs-lookup"><span data-stu-id="d08e6-118">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="d08e6-119">**위치** -hello hello 리소스 있는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="d08e6-119">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="d08e6-120">**연결** -연결 toohello 목록이 참조 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d08e6-120">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="d08e6-121">**이름** -hello의 hello 이름이 리소스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="d08e6-121">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="d08e6-122">**resourceId** -hello resourceId hello 연결에서 참조 하는 hello 리소스의 hello uri입니다.</span><span class="sxs-lookup"><span data-stu-id="d08e6-122">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="d08e6-123">**associationType** -이 값 hello hello 자식 개체와 hello 부모 관계를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="d08e6-123">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="d08e6-124">유효한 값은 **포함** 또는 **관련됨**입니다.</span><span class="sxs-lookup"><span data-stu-id="d08e6-124">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d08e6-125">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="d08e6-125">Before you begin</span></span>

<span data-ttu-id="d08e6-126">이 시나리오에서는 사용 하 여 hello `network watcher topology` cmdlet tooretrieve hello 토폴로지 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d08e6-126">In this scenario, you use hello `network watcher topology` cmdlet tooretrieve hello topology information.</span></span> <span data-ttu-id="d08e6-127">이기도 아티클을 방법에 너무[REST API와 네트워크 토폴로지 검색](network-watcher-topology-rest.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d08e6-127">There is also an article on how too[retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="d08e6-128">이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다.</span><span class="sxs-lookup"><span data-stu-id="d08e6-128">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="d08e6-129">시나리오</span><span class="sxs-lookup"><span data-stu-id="d08e6-129">Scenario</span></span>

<span data-ttu-id="d08e6-130">이 문서에서 다루는 hello 시나리오는 해당된 리소스 그룹에 대 한 hello 토폴로지 응답을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d08e6-130">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="retrieve-topology"></a><span data-ttu-id="d08e6-131">토폴로지 검색</span><span class="sxs-lookup"><span data-stu-id="d08e6-131">Retrieve topology</span></span>

<span data-ttu-id="d08e6-132">hello `network watcher topology` cmdlet는 지정 된 리소스 그룹에 대 한 hello 토폴로지를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d08e6-132">hello `network watcher topology` cmdlet retrieves hello topology for a given resource group.</span></span> <span data-ttu-id="d08e6-133">Hello 인수 추가 "-json" tooview hello oput json 형식</span><span class="sxs-lookup"><span data-stu-id="d08e6-133">Add hello argument "--json" tooview hello oput in json format</span></span>

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a><span data-ttu-id="d08e6-134">결과</span><span class="sxs-lookup"><span data-stu-id="d08e6-134">Results</span></span>

<span data-ttu-id="d08e6-135">hello 반환 된 결과는 속성이 이름 "리소스" hello에 대 한 hello json 응답 본문을 포함 하는 `network watcher topology` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d08e6-135">hello results returned have a property name "Resources", which contains hello json response body for hello `network watcher topology` cmdlet.</span></span>  <span data-ttu-id="d08e6-136">hello 응답 hello 네트워크 보안 그룹 및 해당 연결 (즉, Contains, 연결 됨)의 hello 리소스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d08e6-136">hello response contains hello resources in hello Network Security Group and their associations (that is, Contains, Associated).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d08e6-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d08e6-137">Next steps</span></span>

<span data-ttu-id="d08e6-138">Hello 보안 규칙을 방문 하 여 적용 된 tooyour 네트워크 리소스에 대 한 자세한 [보안 그룹, 개요 보기](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d08e6-138">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
