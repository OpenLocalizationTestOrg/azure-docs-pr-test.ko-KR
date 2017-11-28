---
title: "관리 되는 응용 프로그램 SizeSelector UI 요소 aaaAzure | Microsoft Docs"
description: "Azure 관리 되는 응용 프로그램에 대 한 hello Microsoft.Compute.SizeSelector UI 요소를 설명합니다."
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
ms.openlocfilehash: d93306135d9c6f9a83692766ce1ca7ea2b688086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a><span data-ttu-id="53e7f-103">Microsoft.Compute.SizeSelector UI 요소</span><span class="sxs-lookup"><span data-stu-id="53e7f-103">Microsoft.Compute.SizeSelector UI element</span></span>
<span data-ttu-id="53e7f-104">하나 이상의 가상 컴퓨터 인스턴스에 대한 크기를 선택하는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="53e7f-104">A control for selecting a size for one or more virtual machine instances.</span></span> <span data-ttu-id="53e7f-105">[Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="53e7f-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="53e7f-106">UI 샘플</span><span class="sxs-lookup"><span data-stu-id="53e7f-106">UI sample</span></span>
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a><span data-ttu-id="53e7f-108">스키마</span><span class="sxs-lookup"><span data-stu-id="53e7f-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="53e7f-109">설명</span><span class="sxs-lookup"><span data-stu-id="53e7f-109">Remarks</span></span>
- <span data-ttu-id="53e7f-110">`recommendedSizes`는 하나 이상의 크기를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53e7f-110">`recommendedSizes` should contain at least one size.</span></span> <span data-ttu-id="53e7f-111">hello 먼저 hello 기본값으로 사용 되는 크기 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="53e7f-111">hello first recommended size is used as hello default.</span></span>
- <span data-ttu-id="53e7f-112">Hello 선택한 위치에 권장 되는 크기를 사용할 수 없으면 hello 크기를 자동으로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="53e7f-112">If a recommended size is not available in hello selected location, hello size is automatically skipped.</span></span> <span data-ttu-id="53e7f-113">대신, hello 다음 권장된 크기가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53e7f-113">Instead, hello next recommended size is used.</span></span>
- <span data-ttu-id="53e7f-114">Hello에 지정 되지 않은 모든 크기 `constraints.allowedSizes` 숨겨져 있는 경우에 지정 되지 않은 모든 크기 및 `constraints.excludedSizes` 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53e7f-114">Any size not specified in hello `constraints.allowedSizes` is hidden, and any size not specified in `constraints.excludedSizes` is shown.</span></span>
<span data-ttu-id="53e7f-115">`constraints.allowedSizes`와 `constraints.excludedSizes`는 모두 선택 사항이지만 동시에 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="53e7f-115">`constraints.allowedSizes` and `constraints.excludedSizes` are both optional, but cannot be used simultaneously.</span></span> <span data-ttu-id="53e7f-116">호출 하 여 hello 목록이 사용 가능한 크기를 확인할 수 있습니다 [구독에 대 한 사용 가능한 가상 컴퓨터 크기 나열](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)합니다.</span><span class="sxs-lookup"><span data-stu-id="53e7f-116">hello list of available sizes can be determined by calling [List available virtual machine sizes for a subscription](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span></span>
- <span data-ttu-id="53e7f-117">`osPlatform`을 지정해야 하며 **Windows** 또는 **Linux**일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e7f-117">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span> <span data-ttu-id="53e7f-118">Toodetermine hello 하드웨어 비용 hello 가상 컴퓨터를 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="53e7f-118">It's used toodetermine hello hardware costs of hello virtual machines.</span></span>
- <span data-ttu-id="53e7f-119">`imageReference`은 자사 이미지에 대해 생략되지만, 타사 이미지에 대해서는 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="53e7f-119">`imageReference` is omitted for first-party images, but provided for third-party images.</span></span> <span data-ttu-id="53e7f-120">Toodetermine hello 소프트웨어 비용의 hello 가상 컴퓨터를 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="53e7f-120">It's used toodetermine hello software costs of hello virtual machines.</span></span>
- <span data-ttu-id="53e7f-121">`count`사용 되는 tooset hello hello 요소에 대 한 적절 한 승수가입니다.</span><span class="sxs-lookup"><span data-stu-id="53e7f-121">`count` is used tooset hello appropriate multiplier for hello element.</span></span> <span data-ttu-id="53e7f-122">**2**와 같은 정적 값 또는 `[steps('step1').vmCount]`와 같은 다른 요소의 동적 값을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="53e7f-122">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').vmCount]`.</span></span> <span data-ttu-id="53e7f-123">hello 기본값은 **1**합니다.</span><span class="sxs-lookup"><span data-stu-id="53e7f-123">hello default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="53e7f-124">샘플 출력</span><span class="sxs-lookup"><span data-stu-id="53e7f-124">Sample output</span></span>
```json
"Standard_D1"
```

## <a name="next-steps"></a><span data-ttu-id="53e7f-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="53e7f-125">Next steps</span></span>
* <span data-ttu-id="53e7f-126">소개 toomanaged 응용 프로그램에 대 한 참조 [Azure 관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="53e7f-126">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="53e7f-127">소개 toocreating UI 정의 대 한 참조 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="53e7f-127">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="53e7f-128">UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53e7f-128">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
