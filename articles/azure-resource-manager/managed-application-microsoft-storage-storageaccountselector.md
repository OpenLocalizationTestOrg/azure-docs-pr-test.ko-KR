---
title: "Azure Managed Application StorageAccountSelector UI 요소 | Microsoft Docs"
description: "Azure Managed Applications의 Microsoft.Storage.StorageAccountSelector UI 요소에 대해 설명합니다."
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
ms.openlocfilehash: 15e69c0deb4bce64b7413b557eb69db5165bde73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftstoragestorageaccountselector-ui-element"></a><span data-ttu-id="4eadc-103">Microsoft.Storage.StorageAccountSelector UI 요소</span><span class="sxs-lookup"><span data-stu-id="4eadc-103">Microsoft.Storage.StorageAccountSelector UI element</span></span>
<span data-ttu-id="4eadc-104">새 또는 기존 저장소 계정을 선택하는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="4eadc-104">A control for selecting a new or existing storage account.</span></span> <span data-ttu-id="4eadc-105">[Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4eadc-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="4eadc-106">UI 샘플</span><span class="sxs-lookup"><span data-stu-id="4eadc-106">UI sample</span></span>
![Microsoft.Storage.StorageAccountSelector](./media/managed-application-elements/microsoft.storage.storageaccountselector.png)

## <a name="schema"></a><span data-ttu-id="4eadc-108">스키마</span><span class="sxs-lookup"><span data-stu-id="4eadc-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.StorageAccountSelector",
  "label": "Storage account",
  "toolTip": "",
  "defaultValue": {
    "name": "storageaccount01",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "options": {
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="4eadc-109">설명</span><span class="sxs-lookup"><span data-stu-id="4eadc-109">Remarks</span></span>
- <span data-ttu-id="4eadc-110">지정하는 경우 `defaultValue.name`의 고유성에 대한 유효성 검사가 자동으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="4eadc-110">If specified, `defaultValue.name` is automatically validated for uniqueness.</span></span> <span data-ttu-id="4eadc-111">저장소 계정 이름이 고유하지 않으면 사용자가 다른 이름을 지정하거나 기존 저장소 계정을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eadc-111">If the storage account name is not unique, the user must specify a different name or choose an existing storage account.</span></span>
- <span data-ttu-id="4eadc-112">`defaultValue.type`의 기본값은 **Premium_LRS**입니다.</span><span class="sxs-lookup"><span data-stu-id="4eadc-112">The default value for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="4eadc-113">`constraints.allowedTypes`에 지정되지 않은 형식은 숨겨지며, `constraints.excludedTypes`에 지정되지 않은 형식이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4eadc-113">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="4eadc-114">`constraints.allowedTypes`와 `constraints.excludedTypes`는 모두 선택 사항이지만 동시에 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4eadc-114">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="4eadc-115">`options.hideExisting`이 **true**이면 사용자가 기존 저장소 계정을 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4eadc-115">If `options.hideExisting` is **true**, the user can't choose an existing storage account.</span></span> <span data-ttu-id="4eadc-116">기본값은 **false**입니다.</span><span class="sxs-lookup"><span data-stu-id="4eadc-116">The default value is **false**.</span></span>


## <a name="sample-output"></a><span data-ttu-id="4eadc-117">샘플 출력</span><span class="sxs-lookup"><span data-stu-id="4eadc-117">Sample output</span></span>
```json
{
  "name": "storageaccount01",
  "resourceGroup": "rg01",
  "type": "Premium_LRS",
  "newOrExisting": "new"
}
```

## <a name="next-steps"></a><span data-ttu-id="4eadc-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4eadc-118">Next steps</span></span>
* <span data-ttu-id="4eadc-119">관리되는 응용 프로그램에 대한 소개는 [Azure Managed Application 개요](managed-application-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4eadc-119">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="4eadc-120">UI 정의 만들기에 대한 소개는 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4eadc-120">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="4eadc-121">UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4eadc-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
