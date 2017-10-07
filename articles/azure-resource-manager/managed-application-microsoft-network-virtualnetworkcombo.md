---
title: "관리 되는 응용 프로그램 VirtualNetworkCombo UI 요소 aaaAzure | Microsoft Docs"
description: "Azure 관리 되는 응용 프로그램에 대 한 hello Microsoft.Network.VirtualNetworkCombo UI 요소를 설명합니다."
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
ms.openlocfilehash: 1b0fa5360d93306f7a814723f77e42540bdaaa9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a><span data-ttu-id="9cb1e-103">Microsoft.Network.VirtualNetworkCombo UI 요소</span><span class="sxs-lookup"><span data-stu-id="9cb1e-103">Microsoft.Network.VirtualNetworkCombo UI element</span></span>
<span data-ttu-id="9cb1e-104">새 또는 기존 가상 네트워크를 선택하는 컨트롤 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="9cb1e-104">A group of controls for selecting a new or existing virtual network.</span></span> <span data-ttu-id="9cb1e-105">[Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb1e-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="9cb1e-106">UI 샘플</span><span class="sxs-lookup"><span data-stu-id="9cb1e-106">UI sample</span></span>
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- <span data-ttu-id="9cb1e-108">Hello 상위 와이어 프레임으로 hello 사용자 하므로 hello 사용자 각 서브넷의 이름 및 주소 접두사를 사용자 지정할 수 새 가상 네트워크를 선택 했습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb1e-108">In hello top wireframe, hello user has picked a new virtual network, so hello user can customize each subnet's name and address prefix.</span></span> <span data-ttu-id="9cb1e-109">이 경우 서브넷을 구성하는 것은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="9cb1e-109">Configuring subnets in this case is optional.</span></span>
- <span data-ttu-id="9cb1e-110">Hello 아래쪽 와이어 프레임으로 hello 사용자가 기존 가상 네트워크를 선택, 각 서브넷 hello 배포 템플릿에 tooan 기존 서브넷 필요 하므로 hello 사용자를 매핑해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb1e-110">In hello bottom wireframe, hello user has picked an existing virtual network, so hello user must map each subnet hello deployment template requires tooan existing subnet.</span></span> <span data-ttu-id="9cb1e-111">이 경우 서브넷을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb1e-111">Configuring subnets in this case is required.</span></span>

## <a name="schema"></a><span data-ttu-id="9cb1e-112">스키마</span><span class="sxs-lookup"><span data-stu-id="9cb1e-112">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="9cb1e-113">설명</span><span class="sxs-lookup"><span data-stu-id="9cb1e-113">Remarks</span></span>
- <span data-ttu-id="9cb1e-114">를 지정 하는 경우 첫 번째 겹치지 않는 주소 접두사 크기 hello `defaultValue.addressPrefixSize` hello 사용자의 구독에서 기존 가상 네트워크에 따라 자동으로 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb1e-114">If specified, hello first non-overlapping address prefix of size `defaultValue.addressPrefixSize` is determined automatically based on the existing virtual networks in hello user's subscription.</span></span>
- <span data-ttu-id="9cb1e-115">에 대 한 기본값을 hello `defaultValue.name` 및 `defaultValue.addressPrefixSize` 은 **null**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb1e-115">hello default value for `defaultValue.name` and `defaultValue.addressPrefixSize` is **null**.</span></span>
- <span data-ttu-id="9cb1e-116">`constraints.minAddressPrefixSize`를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb1e-116">`constraints.minAddressPrefixSize` must be specified.</span></span> <span data-ttu-id="9cb1e-117">Hello 지정 된 값이 없는 선택할 수 있는 보다 작은 주소 공간과 기존 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="9cb1e-117">Any existing virtual networks with an address space smaller than hello specified value are unavailable for selection.</span></span>
- <span data-ttu-id="9cb1e-118">`subnets`를 지정해야 하며, 각 서브넷에 대해 `constraints.minAddressPrefixSize`를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb1e-118">`subnets` must be specified, and `constraints.minAddressPrefixSize` must be specified for each subnet.</span></span>
- <span data-ttu-id="9cb1e-119">새 가상 네트워크를 만들 때 각 서브넷의 주소 접두사는 기준으로 자동 계산 hello 가상 네트워크의 주소 접두사와 해당 `addressPrefixSize`합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb1e-119">When creating a new virtual network, each subnet's address prefix is calculated automatically based on hello virtual network's address prefix and the respective `addressPrefixSize`.</span></span>
- <span data-ttu-id="9cb1e-120">기존 가상 네트워크를 사용할 때 각각의 `constraints.minAddressPrefixSize`보다 작은 서브넷은 모두 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb1e-120">When using an existing virtual network, any subnets smaller than the respective `constraints.minAddressPrefixSize` are unavailable for selection.</span></span> <span data-ttu-id="9cb1e-121">또한 지정하는 경우 `minAddressCount` 값 이상의 사용 가능한 주소를 포함하지 않는 서브넷은 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb1e-121">Additionally, if specified, subnets that do not contain at least `minAddressCount` available addresses are unavailable for selection.</span></span>
<span data-ttu-id="9cb1e-122">hello 기본값은 **0**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb1e-122">hello default value is **0**.</span></span> <span data-ttu-id="9cb1e-123">사용 가능한 주소 hello tooensure 연속 되는, 지정 **true** 에 대 한 `requireContiguousAddresses`합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb1e-123">tooensure that hello available addresses are contiguous, specify **true** for `requireContiguousAddresses`.</span></span> <span data-ttu-id="9cb1e-124">hello 기본값은 **true**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb1e-124">hello default value is **true**.</span></span>
- <span data-ttu-id="9cb1e-125">기존 가상 네트워크에서 서브넷을 만드는 것은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb1e-125">Creating subnets in an existing virtual network is not supported.</span></span>
- <span data-ttu-id="9cb1e-126">경우 `options.hideExisting` 은 **true**, hello 사용자는 기존 가상 네트워크를 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb1e-126">If `options.hideExisting` is **true**, hello user can't choose an existing virtual network.</span></span> <span data-ttu-id="9cb1e-127">hello 기본값은 **false**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb1e-127">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="9cb1e-128">샘플 출력</span><span class="sxs-lookup"><span data-stu-id="9cb1e-128">Sample output</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="9cb1e-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9cb1e-129">Next steps</span></span>
* <span data-ttu-id="9cb1e-130">소개 toomanaged 응용 프로그램에 대 한 참조 [Azure 관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb1e-130">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="9cb1e-131">소개 toocreating UI 정의 대 한 참조 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb1e-131">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="9cb1e-132">UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cb1e-132">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
