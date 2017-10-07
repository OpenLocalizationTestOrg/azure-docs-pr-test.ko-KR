---
title: "관리 되는 응용 프로그램 StorageAccountSelector UI 요소 aaaAzure | Microsoft Docs"
description: "Azure 관리 되는 응용 프로그램에 대 한 hello Microsoft.Storage.StorageAccountSelector UI 요소를 설명합니다."
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
ms.openlocfilehash: a2c9545feed4c4afb3c64b30b42c94d5382a108d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftstoragestorageaccountselector-ui-element"></a><span data-ttu-id="8409a-103">Microsoft.Storage.StorageAccountSelector UI 요소</span><span class="sxs-lookup"><span data-stu-id="8409a-103">Microsoft.Storage.StorageAccountSelector UI element</span></span>
<span data-ttu-id="8409a-104">새 또는 기존 저장소 계정을 선택하는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="8409a-104">A control for selecting a new or existing storage account.</span></span> <span data-ttu-id="8409a-105">[Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8409a-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="8409a-106">UI 샘플</span><span class="sxs-lookup"><span data-stu-id="8409a-106">UI sample</span></span>
![Microsoft.Storage.StorageAccountSelector](./media/managed-application-elements/microsoft.storage.storageaccountselector.png)

## <a name="schema"></a><span data-ttu-id="8409a-108">스키마</span><span class="sxs-lookup"><span data-stu-id="8409a-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="8409a-109">설명</span><span class="sxs-lookup"><span data-stu-id="8409a-109">Remarks</span></span>
- <span data-ttu-id="8409a-110">지정하는 경우 `defaultValue.name`의 고유성에 대한 유효성 검사가 자동으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="8409a-110">If specified, `defaultValue.name` is automatically validated for uniqueness.</span></span> <span data-ttu-id="8409a-111">Hello 저장소 계정 이름이 고유 하지 않으면 hello 사용자 다른 이름을 지정 하거나 기존 저장소 계정을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8409a-111">If hello storage account name is not unique, hello user must specify a different name or choose an existing storage account.</span></span>
- <span data-ttu-id="8409a-112">에 대 한 기본값을 hello `defaultValue.type` 은 **Premium_LRS**합니다.</span><span class="sxs-lookup"><span data-stu-id="8409a-112">hello default value for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="8409a-113">`constraints.allowedTypes`에 지정되지 않은 형식은 숨겨지며, `constraints.excludedTypes`에 지정되지 않은 형식이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8409a-113">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="8409a-114">`constraints.allowedTypes`와 `constraints.excludedTypes`는 모두 선택 사항이지만 동시에 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8409a-114">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="8409a-115">경우 `options.hideExisting` 은 **true**, hello 사용자는 기존 저장소 계정을 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8409a-115">If `options.hideExisting` is **true**, hello user can't choose an existing storage account.</span></span> <span data-ttu-id="8409a-116">hello 기본값은 **false**합니다.</span><span class="sxs-lookup"><span data-stu-id="8409a-116">hello default value is **false**.</span></span>


## <a name="sample-output"></a><span data-ttu-id="8409a-117">샘플 출력</span><span class="sxs-lookup"><span data-stu-id="8409a-117">Sample output</span></span>
```json
{
  "name": "storageaccount01",
  "resourceGroup": "rg01",
  "type": "Premium_LRS",
  "newOrExisting": "new"
}
```

## <a name="next-steps"></a><span data-ttu-id="8409a-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8409a-118">Next steps</span></span>
* <span data-ttu-id="8409a-119">소개 toomanaged 응용 프로그램에 대 한 참조 [Azure 관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8409a-119">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="8409a-120">소개 toocreating UI 정의 대 한 참조 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8409a-120">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="8409a-121">UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8409a-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
