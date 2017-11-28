---
title: "관리 되는 응용 프로그램 MultiStorageAccountCombo UI 요소 aaaAzure | Microsoft Docs"
description: "Azure 관리 되는 응용 프로그램에 대 한 hello Microsoft.Storage.MultiStorageAccountCombo UI 요소를 설명합니다."
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
ms.openlocfilehash: 765be145b61c3dbf0a035a7a00aa18eee464a3eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a><span data-ttu-id="cc431-103">Microsoft.Storage.MultiStorageAccountCombo UI 요소</span><span class="sxs-lookup"><span data-stu-id="cc431-103">Microsoft.Storage.MultiStorageAccountCombo UI element</span></span>
<span data-ttu-id="cc431-104">공통 접두사로 시작하는 이름의 저장소 계정을 여러 개 만드는 컨트롤 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="cc431-104">A group of controls for creating multiple storage accounts, with names that start with a common prefix.</span></span> <span data-ttu-id="cc431-105">[Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cc431-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="cc431-106">UI 샘플</span><span class="sxs-lookup"><span data-stu-id="cc431-106">UI sample</span></span>
![Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a><span data-ttu-id="cc431-108">스키마</span><span class="sxs-lookup"><span data-stu-id="cc431-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="cc431-109">설명</span><span class="sxs-lookup"><span data-stu-id="cc431-109">Remarks</span></span>
- <span data-ttu-id="cc431-110">값에 대 한 hello `defaultValue.prefix` 저장소 계정 이름 하나 이상의 정수 toogenerate hello 순서와 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc431-110">hello value for `defaultValue.prefix` is concatenated with one or more integers toogenerate hello sequence of storage account names.</span></span> <span data-ttu-id="cc431-111">예를 들어 `defaultValue.prefix`가 **foobar**이고 `count`가 **2**이면 **foobar1** 및 **foobar2** 저장소 계정 이름이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc431-111">For example, if `defaultValue.prefix` is **foobar** and `count` is **2**, then storage account names **foobar1** and **foobar2** are generated.</span></span> <span data-ttu-id="cc431-112">생성된 저장소 계정 이름의 고유성에 대한 유효성 검사가 자동으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc431-112">Generated storage account names are validated for uniqueness automatically.</span></span>
- <span data-ttu-id="cc431-113">hello 저장소 계정 이름에 따라 사전순에 따라 생성 된 `count`합니다.</span><span class="sxs-lookup"><span data-stu-id="cc431-113">hello storage account names are generated lexicographically based on `count`.</span></span> <span data-ttu-id="cc431-114">예를 들어 경우 `count` 10, hello 저장소 계정 이름은 2 자리 정수 끝나야 합니다 (01, 02, 03, 등입니다.).</span><span class="sxs-lookup"><span data-stu-id="cc431-114">For example, if `count` is 10, then hello storage account names end with 2-digit integers (01, 02, 03, etc.).</span></span>
- <span data-ttu-id="cc431-115">기본값에 대 한 hello `defaultValue.prefix` 은 **null**, 및에 대 한 `defaultValue.type` 은 **Premium_LRS**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc431-115">hello default value for `defaultValue.prefix` is **null**, and for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="cc431-116">`constraints.allowedTypes`에 지정되지 않은 형식은 숨겨지며, `constraints.excludedTypes`에 지정되지 않은 형식이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc431-116">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="cc431-117">`constraints.allowedTypes`와 `constraints.excludedTypes`는 모두 선택 사항이지만 동시에 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cc431-117">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="cc431-118">또한 toogenerating 저장소 계정 이름에 `count` hello 요소에 대 한 적절 한 승수 tooset 사용된 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc431-118">In addition toogenerating storage account names, `count` is used tooset the appropriate multiplier for hello element.</span></span> <span data-ttu-id="cc431-119">**2**와 같은 정적 값 또는 `[steps('step1').storageAccountCount]`와 같은 다른 요소의 동적 값을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cc431-119">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').storageAccountCount]`.</span></span> <span data-ttu-id="cc431-120">hello 기본값은 **1**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc431-120">hello default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="cc431-121">샘플 출력</span><span class="sxs-lookup"><span data-stu-id="cc431-121">Sample output</span></span>
```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a><span data-ttu-id="cc431-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cc431-122">Next steps</span></span>
* <span data-ttu-id="cc431-123">소개 toomanaged 응용 프로그램에 대 한 참조 [Azure 관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cc431-123">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="cc431-124">소개 toocreating UI 정의 대 한 참조 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cc431-124">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="cc431-125">UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc431-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
