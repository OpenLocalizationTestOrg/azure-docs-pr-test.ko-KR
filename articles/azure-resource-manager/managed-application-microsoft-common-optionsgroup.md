---
title: "Azure Managed Application OptionsGroup UI 요소 | Microsoft Docs"
description: "Azure Managed Applications의 Microsoft.Common.OptionsGroup UI 요소에 대해 설명합니다."
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
ms.openlocfilehash: 6e147ed28c8248f7f17cb36fd7ae13468141dced
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonoptionsgroup-ui-element"></a><span data-ttu-id="3d142-103">Microsoft.Common.OptionsGroup UI 요소</span><span class="sxs-lookup"><span data-stu-id="3d142-103">Microsoft.Common.OptionsGroup UI element</span></span>
<span data-ttu-id="3d142-104">사용 가능한 옵션 행을 포함하는 선택 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="3d142-104">A selection control with a row of available options.</span></span> <span data-ttu-id="3d142-105">[Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3d142-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="3d142-106">UI 샘플</span><span class="sxs-lookup"><span data-stu-id="3d142-106">UI sample</span></span>
![Microsoft.Common.OptionsGroup](./media/managed-application-elements/microsoft.common.optionsgroup.png)

## <a name="schema"></a><span data-ttu-id="3d142-108">스키마</span><span class="sxs-lookup"><span data-stu-id="3d142-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.OptionsGroup",
  "label": "Some options group",
  "defaultValue": "Foo",
  "toolTip": "",
  "constraints": {
    "allowedValues": [
      {
        "label": "Foo",
        "value": "Bar"
      },
      {
        "label": "Baz",
        "value": "Qux"
      }
    ]
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="3d142-109">설명</span><span class="sxs-lookup"><span data-stu-id="3d142-109">Remarks</span></span>
- <span data-ttu-id="3d142-110">`constraints.allowedValues`의 레이블은 항목에 대한 표시 텍스트이며, 해당 값은 선택한 요소의 출력 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3d142-110">The label for `constraints.allowedValues` is the display text for an item, and its value is the output value of the element when selected.</span></span>
- <span data-ttu-id="3d142-111">이 값을 지정하면 기본값은 `constraints.allowedValues`에 있는 레이블이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d142-111">If specified, the default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="3d142-112">지정하지 않으면 `constraints.allowedValues`의 첫 번째 항목이 기본적으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d142-112">If not specified, the first item in `constraints.allowedValues` is selected by default.</span></span> <span data-ttu-id="3d142-113">기본값은 **null**입니다.</span><span class="sxs-lookup"><span data-stu-id="3d142-113">The default value is **null**.</span></span>
- <span data-ttu-id="3d142-114">`constraints.allowedValues`는 하나 이상의 항목을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d142-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="3d142-115">이 요소는 `constraints.required` 속성을 지원하지 않습니다. 유효성을 성공적으로 검사하기 위한 항목을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d142-115">This element doesn't support the `constraints.required` property; an item must be selected to validate successfully.</span></span>

## <a name="sample-output"></a><span data-ttu-id="3d142-116">샘플 출력</span><span class="sxs-lookup"><span data-stu-id="3d142-116">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="3d142-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3d142-117">Next steps</span></span>
* <span data-ttu-id="3d142-118">관리되는 응용 프로그램에 대한 소개는 [Azure Managed Application 개요](managed-application-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d142-118">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="3d142-119">UI 정의 만들기에 대한 소개는 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d142-119">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="3d142-120">UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d142-120">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
