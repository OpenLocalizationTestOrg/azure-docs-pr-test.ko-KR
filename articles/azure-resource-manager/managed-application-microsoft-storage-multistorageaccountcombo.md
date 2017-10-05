---
title: "Azure Managed Application MultiStorageAccountCombo UI 요소 | Microsoft Docs"
description: "Azure Managed Applications의 Microsoft.Storage.MultiStorageAccountCombo UI 요소에 대해 설명합니다."
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
ms.openlocfilehash: 27843b116d949899e4eae65f342324f77ebca70b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a><span data-ttu-id="ed2f2-103">Microsoft.Storage.MultiStorageAccountCombo UI 요소</span><span class="sxs-lookup"><span data-stu-id="ed2f2-103">Microsoft.Storage.MultiStorageAccountCombo UI element</span></span>
<span data-ttu-id="ed2f2-104">공통 접두사로 시작하는 이름의 저장소 계정을 여러 개 만드는 컨트롤 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="ed2f2-104">A group of controls for creating multiple storage accounts, with names that start with a common prefix.</span></span> <span data-ttu-id="ed2f2-105">[Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2f2-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="ed2f2-106">UI 샘플</span><span class="sxs-lookup"><span data-stu-id="ed2f2-106">UI sample</span></span>
![Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a><span data-ttu-id="ed2f2-108">스키마</span><span class="sxs-lookup"><span data-stu-id="ed2f2-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.MultiStorageAccountCombo",
  "label": {
    "prefix": "Storage account prefix",
    "type": "Storage account type"
  },
  "toolTip": {
    "prefix": "",
    "type": ""
  },
  "defaultValue": {
    "prefix": "sa",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="ed2f2-109">설명</span><span class="sxs-lookup"><span data-stu-id="ed2f2-109">Remarks</span></span>
- <span data-ttu-id="ed2f2-110">`defaultValue.prefix`의 값은 하나 이상의 정수와 연결되어 저장소 계정 이름의 시퀀스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2f2-110">The value for `defaultValue.prefix` is concatenated with one or more integers to generate the sequence of storage account names.</span></span> <span data-ttu-id="ed2f2-111">예를 들어 `defaultValue.prefix`가 **foobar**이고 `count`가 **2**이면 **foobar1** 및 **foobar2** 저장소 계정 이름이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed2f2-111">For example, if `defaultValue.prefix` is **foobar** and `count` is **2**, then storage account names **foobar1** and **foobar2** are generated.</span></span> <span data-ttu-id="ed2f2-112">생성된 저장소 계정 이름의 고유성에 대한 유효성 검사가 자동으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed2f2-112">Generated storage account names are validated for uniqueness automatically.</span></span>
- <span data-ttu-id="ed2f2-113">저장소 계정 이름은 `count`에 따라 사전순으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed2f2-113">The storage account names are generated lexicographically based on `count`.</span></span> <span data-ttu-id="ed2f2-114">예를 들어 `count`가 10이면 저장소 계정 이름은 2자리 정수로 끝납니다(01, 02, 03 등).</span><span class="sxs-lookup"><span data-stu-id="ed2f2-114">For example, if `count` is 10, then the storage account names end with 2-digit integers (01, 02, 03, etc.).</span></span>
- <span data-ttu-id="ed2f2-115">`defaultValue.prefix`의 기본값은 **null**이고, `defaultValue.type`의 기본값은 **Premium_LRS**입니다.</span><span class="sxs-lookup"><span data-stu-id="ed2f2-115">The default value for `defaultValue.prefix` is **null**, and for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="ed2f2-116">`constraints.allowedTypes`에 지정되지 않은 형식은 숨겨지며, `constraints.excludedTypes`에 지정되지 않은 형식이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed2f2-116">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="ed2f2-117">`constraints.allowedTypes`와 `constraints.excludedTypes`는 모두 선택 사항이지만 동시에 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2f2-117">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="ed2f2-118">저장소 계정 이름을 생성하는 것 외에도 `count`는 요소에 적절한 승수를 설정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed2f2-118">In addition to generating storage account names, `count` is used to set the appropriate multiplier for the element.</span></span> <span data-ttu-id="ed2f2-119">**2**와 같은 정적 값 또는 `[steps('step1').storageAccountCount]`와 같은 다른 요소의 동적 값을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2f2-119">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').storageAccountCount]`.</span></span> <span data-ttu-id="ed2f2-120">기본값은 **1**입니다.</span><span class="sxs-lookup"><span data-stu-id="ed2f2-120">The default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="ed2f2-121">샘플 출력</span><span class="sxs-lookup"><span data-stu-id="ed2f2-121">Sample output</span></span>
```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a><span data-ttu-id="ed2f2-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ed2f2-122">Next steps</span></span>
* <span data-ttu-id="ed2f2-123">관리되는 응용 프로그램에 대한 소개는 [Azure Managed Application 개요](managed-application-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed2f2-123">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="ed2f2-124">UI 정의 만들기에 대한 소개는 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed2f2-124">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="ed2f2-125">UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed2f2-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
