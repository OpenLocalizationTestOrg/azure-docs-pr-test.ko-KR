---
title: "Azure Managed Application VirtualNetworkCombo UI 요소 | Microsoft Docs"
description: "Azure Managed Applications의 Microsoft.Network.VirtualNetworkCombo UI 요소에 대해 설명합니다."
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 8bb255b76ac5c3de570fa569a1cfb3ee953f9687
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a><span data-ttu-id="ff730-103">Microsoft.Network.VirtualNetworkCombo UI 요소</span><span class="sxs-lookup"><span data-stu-id="ff730-103">Microsoft.Network.VirtualNetworkCombo UI element</span></span>
<span data-ttu-id="ff730-104">새 또는 기존 가상 네트워크를 선택하는 컨트롤 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="ff730-104">A group of controls for selecting a new or existing virtual network.</span></span> <span data-ttu-id="ff730-105">[Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ff730-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="ff730-106">UI 샘플</span><span class="sxs-lookup"><span data-stu-id="ff730-106">UI sample</span></span>
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- <span data-ttu-id="ff730-108">위쪽 와이어프레임에서 사용자가 새 가상 네트워크를 선택했으므로 사용자는 각 서브넷의 이름과 주소 접두사를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff730-108">In the top wireframe, the user has picked a new virtual network, so the user can customize each subnet's name and address prefix.</span></span> <span data-ttu-id="ff730-109">이 경우 서브넷을 구성하는 것은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="ff730-109">Configuring subnets in this case is optional.</span></span>
- <span data-ttu-id="ff730-110">아래쪽 와이어프레임에서 사용자가 기존 가상 네트워크를 선택했으므로 사용자는 배포 템플릿에 필요한 각 서브넷을 기존 서브넷에 매핑해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff730-110">In the bottom wireframe, the user has picked an existing virtual network, so the user must map each subnet the deployment template requires to an existing subnet.</span></span> <span data-ttu-id="ff730-111">이 경우 서브넷을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff730-111">Configuring subnets in this case is required.</span></span>

## <a name="schema"></a><span data-ttu-id="ff730-112">스키마</span><span class="sxs-lookup"><span data-stu-id="ff730-112">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Network.VirtualNetworkCombo",
  "label": {
    "virtualNetwork": "Virtual network",
    "subnets": "Subnets"
  },
  "toolTip": {
    "virtualNetwork": "",
    "subnets": ""
  },
  "defaultValue": {
    "name": "vnet01",
    "addressPrefixSize": "/16"
  },
  "constraints": {
    "minAddressPrefixSize": "/16"
  },
  "options": {
    "hideExisting": false
  },
  "subnets": {
    "subnet1": {
      "label": "First subnet",
      "defaultValue": {
        "name": "subnet-1",
        "addressPrefixSize": "/24"
      },
      "constraints": {
        "minAddressPrefixSize": "/24",
        "minAddressCount": 12,
        "requireContiguousAddresses": true
      }
    },
    "subnet2": {
      "label": "Second subnet",
      "defaultValue": {
        "name": "subnet-2",
        "addressPrefixSize": "/26"
      },
      "constraints": {
        "minAddressPrefixSize": "/26",
        "minAddressCount": 8,
        "requireContiguousAddresses": true
      }
    }
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="ff730-113">설명</span><span class="sxs-lookup"><span data-stu-id="ff730-113">Remarks</span></span>
- <span data-ttu-id="ff730-114">지정하는 경우 크기가 `defaultValue.addressPrefixSize`인 첫 번째 중복되지 않는 주소 접두사는 사용자의 구독에 있는 기존 가상 네트워크에 따라 자동으로 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff730-114">If specified, the first non-overlapping address prefix of size `defaultValue.addressPrefixSize` is determined automatically based on the existing virtual networks in the user's subscription.</span></span>
- <span data-ttu-id="ff730-115">`defaultValue.name` 및 `defaultValue.addressPrefixSize`의 기본값은 **null**입니다.</span><span class="sxs-lookup"><span data-stu-id="ff730-115">The default value for `defaultValue.name` and `defaultValue.addressPrefixSize` is **null**.</span></span>
- <span data-ttu-id="ff730-116">`constraints.minAddressPrefixSize`를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff730-116">`constraints.minAddressPrefixSize` must be specified.</span></span> <span data-ttu-id="ff730-117">지정한 값보다 작은 주소 공간이 있는 기존 가상 네트워크는 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ff730-117">Any existing virtual networks with an address space smaller than the specified value are unavailable for selection.</span></span>
- <span data-ttu-id="ff730-118">`subnets`를 지정해야 하며, 각 서브넷에 대해 `constraints.minAddressPrefixSize`를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff730-118">`subnets` must be specified, and `constraints.minAddressPrefixSize` must be specified for each subnet.</span></span>
- <span data-ttu-id="ff730-119">새 가상 네트워크를 만들 때 각 서브넷의 주소 접두사는 가상 네트워크의 주소 접두사와 각각의 `addressPrefixSize`에 따라 자동으로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff730-119">When creating a new virtual network, each subnet's address prefix is calculated automatically based on the virtual network's address prefix and the respective `addressPrefixSize`.</span></span>
- <span data-ttu-id="ff730-120">기존 가상 네트워크를 사용할 때 각각의 `constraints.minAddressPrefixSize`보다 작은 서브넷은 모두 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ff730-120">When using an existing virtual network, any subnets smaller than the respective `constraints.minAddressPrefixSize` are unavailable for selection.</span></span> <span data-ttu-id="ff730-121">또한 지정하는 경우 `minAddressCount` 값 이상의 사용 가능한 주소를 포함하지 않는 서브넷은 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ff730-121">Additionally, if specified, subnets that do not contain at least `minAddressCount` available addresses are unavailable for selection.</span></span>
<span data-ttu-id="ff730-122">기본값은 **0**입니다.</span><span class="sxs-lookup"><span data-stu-id="ff730-122">The default value is **0**.</span></span> <span data-ttu-id="ff730-123">사용 가능한 주소가 연속적인 주소가 되도록 하려면 `requireContiguousAddresses`에 대해 **true**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ff730-123">To ensure that the available addresses are contiguous, specify **true** for `requireContiguousAddresses`.</span></span> <span data-ttu-id="ff730-124">기본값은 **true**입니다.</span><span class="sxs-lookup"><span data-stu-id="ff730-124">The default value is **true**.</span></span>
- <span data-ttu-id="ff730-125">기존 가상 네트워크에서 서브넷을 만드는 것은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ff730-125">Creating subnets in an existing virtual network is not supported.</span></span>
- <span data-ttu-id="ff730-126">`options.hideExisting`이 **true**이면 사용자가 기존 가상 네트워크를 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ff730-126">If `options.hideExisting` is **true**, the user can't choose an existing virtual network.</span></span> <span data-ttu-id="ff730-127">기본값은 **false**입니다.</span><span class="sxs-lookup"><span data-stu-id="ff730-127">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="ff730-128">샘플 출력</span><span class="sxs-lookup"><span data-stu-id="ff730-128">Sample output</span></span>
```json
{
  "name": "vnet01",
  "resourceGroup": "rg01",
  "addressPrefixes": ["10.0.0.0/16"],
  "newOrExisting": "new",
  "subnets": {
    "subnet1": {
      "name": "subnet-1",
      "addressPrefix": "10.0.0.0/24",
      "startAddress": "10.0.0.1"
    },
    "subnet2": {
      "name": "subnet-2",
      "addressPrefix": "10.0.1.0/26",
      "startAddress": "10.0.1.1"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="ff730-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ff730-129">Next steps</span></span>
* <span data-ttu-id="ff730-130">관리되는 응용 프로그램에 대한 소개는 [Azure Managed Application 개요](managed-application-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff730-130">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="ff730-131">UI 정의 만들기에 대한 소개는 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff730-131">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="ff730-132">UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff730-132">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
