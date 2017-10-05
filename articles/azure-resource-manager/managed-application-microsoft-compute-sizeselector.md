---
title: "Azure Managed Application SizeSelector UI 요소 | Microsoft Docs"
description: "Azure Managed Applications의 Microsoft.Compute.SizeSelector UI 요소에 대해 설명합니다."
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
ms.openlocfilehash: e54962f73028ada258a7faef271d66f0fbcef649
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a><span data-ttu-id="54fbb-103">Microsoft.Compute.SizeSelector UI 요소</span><span class="sxs-lookup"><span data-stu-id="54fbb-103">Microsoft.Compute.SizeSelector UI element</span></span>
<span data-ttu-id="54fbb-104">하나 이상의 가상 컴퓨터 인스턴스에 대한 크기를 선택하는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="54fbb-104">A control for selecting a size for one or more virtual machine instances.</span></span> <span data-ttu-id="54fbb-105">[Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="54fbb-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="54fbb-106">UI 샘플</span><span class="sxs-lookup"><span data-stu-id="54fbb-106">UI sample</span></span>
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a><span data-ttu-id="54fbb-108">스키마</span><span class="sxs-lookup"><span data-stu-id="54fbb-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.SizeSelector",
  "label": "Size",
  "toolTip": "",
  "recommendedSizes": [
    "Standard_D1",
    "Standard_D2",
    "Standard_D3"
  ],
  "constraints": {
    "allowedSizes": [],
    "excludedSizes": []
  },
  "osPlatform": "Windows",
  "imageReference": {
    "publisher": "MicrosoftWindowsServer",
    "offer": "WindowsServer",
    "sku": "2012-R2-Datacenter"
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="54fbb-109">설명</span><span class="sxs-lookup"><span data-stu-id="54fbb-109">Remarks</span></span>
- <span data-ttu-id="54fbb-110">`recommendedSizes`는 하나 이상의 크기를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54fbb-110">`recommendedSizes` should contain at least one size.</span></span> <span data-ttu-id="54fbb-111">권장되는 첫 번째 크기가 기본값으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="54fbb-111">The first recommended size is used as the default.</span></span>
- <span data-ttu-id="54fbb-112">선택한 위치에서 권장되는 첫 번째 크기를 사용할 수 없는 경우 해당 크기를 자동으로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="54fbb-112">If a recommended size is not available in the selected location, the size is automatically skipped.</span></span> <span data-ttu-id="54fbb-113">대신 권장되는 다음 크기가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="54fbb-113">Instead, the next recommended size is used.</span></span>
- <span data-ttu-id="54fbb-114">`constraints.allowedSizes`에 지정되지 않은 크기는 숨겨지며 `constraints.excludedSizes`에 지정되지 않은 크기가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="54fbb-114">Any size not specified in the `constraints.allowedSizes` is hidden, and any size not specified in `constraints.excludedSizes` is shown.</span></span>
<span data-ttu-id="54fbb-115">`constraints.allowedSizes`와 `constraints.excludedSizes`는 모두 선택 사항이지만 동시에 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="54fbb-115">`constraints.allowedSizes` and `constraints.excludedSizes` are both optional, but cannot be used simultaneously.</span></span> <span data-ttu-id="54fbb-116">사용 가능한 크기 목록은 [구독에 사용 가능한 가상 컴퓨터 크기 목록](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)을 호출하여 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54fbb-116">The list of available sizes can be determined by calling [List available virtual machine sizes for a subscription](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span></span>
- <span data-ttu-id="54fbb-117">`osPlatform`을 지정해야 하며 **Windows** 또는 **Linux**일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54fbb-117">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span> <span data-ttu-id="54fbb-118">가상 컴퓨터의 하드웨어 비용을 결정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="54fbb-118">It's used to determine the hardware costs of the virtual machines.</span></span>
- <span data-ttu-id="54fbb-119">`imageReference`은 자사 이미지에 대해 생략되지만, 타사 이미지에 대해서는 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="54fbb-119">`imageReference` is omitted for first-party images, but provided for third-party images.</span></span> <span data-ttu-id="54fbb-120">가상 컴퓨터의 소프트웨어 비용을 결정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="54fbb-120">It's used to determine the software costs of the virtual machines.</span></span>
- <span data-ttu-id="54fbb-121">`count`는 요소에 적절한 승수를 설정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="54fbb-121">`count` is used to set the appropriate multiplier for the element.</span></span> <span data-ttu-id="54fbb-122">**2**와 같은 정적 값 또는 `[steps('step1').vmCount]`와 같은 다른 요소의 동적 값을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="54fbb-122">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').vmCount]`.</span></span> <span data-ttu-id="54fbb-123">기본값은 **1**입니다.</span><span class="sxs-lookup"><span data-stu-id="54fbb-123">The default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="54fbb-124">샘플 출력</span><span class="sxs-lookup"><span data-stu-id="54fbb-124">Sample output</span></span>
```json
"Standard_D1"
```

## <a name="next-steps"></a><span data-ttu-id="54fbb-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="54fbb-125">Next steps</span></span>
* <span data-ttu-id="54fbb-126">관리되는 응용 프로그램에 대한 소개는 [Azure Managed Application 개요](managed-application-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54fbb-126">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="54fbb-127">UI 정의 만들기에 대한 소개는 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54fbb-127">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="54fbb-128">UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54fbb-128">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
