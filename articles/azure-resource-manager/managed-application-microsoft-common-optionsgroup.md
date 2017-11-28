---
title: "관리 되는 응용 프로그램 OptionsGroup UI 요소 aaaAzure | Microsoft Docs"
description: "Azure 관리 되는 응용 프로그램에 대 한 hello Microsoft.Common.OptionsGroup UI 요소를 설명합니다."
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
ms.openlocfilehash: e222468009c8db567bdde9f42836a48fb791da00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonoptionsgroup-ui-element"></a><span data-ttu-id="61b92-103">Microsoft.Common.OptionsGroup UI 요소</span><span class="sxs-lookup"><span data-stu-id="61b92-103">Microsoft.Common.OptionsGroup UI element</span></span>
<span data-ttu-id="61b92-104">사용 가능한 옵션 행을 포함하는 선택 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="61b92-104">A selection control with a row of available options.</span></span> <span data-ttu-id="61b92-105">[Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="61b92-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="61b92-106">UI 샘플</span><span class="sxs-lookup"><span data-stu-id="61b92-106">UI sample</span></span>
![Microsoft.Common.OptionsGroup](./media/managed-application-elements/microsoft.common.optionsgroup.png)

## <a name="schema"></a><span data-ttu-id="61b92-108">스키마</span><span class="sxs-lookup"><span data-stu-id="61b92-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="61b92-109">설명</span><span class="sxs-lookup"><span data-stu-id="61b92-109">Remarks</span></span>
- <span data-ttu-id="61b92-110">에 대 한 hello 레이블 `constraints.allowedValues` 는 항목에 대 한 표시 텍스트 hello 이며 해당 값은 선택 하면 hello 요소의 hello 출력 값입니다.</span><span class="sxs-lookup"><span data-stu-id="61b92-110">hello label for `constraints.allowedValues` is hello display text for an item, and its value is hello output value of hello element when selected.</span></span>
- <span data-ttu-id="61b92-111">Hello 기본값에 레이블을 지정, 경우 해야 `constraints.allowedValues`합니다.</span><span class="sxs-lookup"><span data-stu-id="61b92-111">If specified, hello default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="61b92-112">지정 하지 않으면 첫 번째 항목 hello `constraints.allowedValues` 기본적으로 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61b92-112">If not specified, hello first item in `constraints.allowedValues` is selected by default.</span></span> <span data-ttu-id="61b92-113">hello 기본값은 **null**합니다.</span><span class="sxs-lookup"><span data-stu-id="61b92-113">hello default value is **null**.</span></span>
- <span data-ttu-id="61b92-114">`constraints.allowedValues`는 하나 이상의 항목을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61b92-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="61b92-115">이 요소는 hello를 지원 하지 않는 `constraints.required` 속성 항목이 선택한 toovalidate를 성공적으로 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61b92-115">This element doesn't support hello `constraints.required` property; an item must be selected toovalidate successfully.</span></span>

## <a name="sample-output"></a><span data-ttu-id="61b92-116">샘플 출력</span><span class="sxs-lookup"><span data-stu-id="61b92-116">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="61b92-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="61b92-117">Next steps</span></span>
* <span data-ttu-id="61b92-118">소개 toomanaged 응용 프로그램에 대 한 참조 [Azure 관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="61b92-118">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="61b92-119">소개 toocreating UI 정의 대 한 참조 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="61b92-119">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="61b92-120">UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="61b92-120">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
