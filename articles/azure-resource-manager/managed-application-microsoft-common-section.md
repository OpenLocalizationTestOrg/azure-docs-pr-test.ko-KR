---
title: "Azure Managed Application Section UI 요소 | Microsoft Docs"
description: "Azure Managed Applications의 Microsoft.Common.Section UI 요소에 대해 설명합니다."
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
ms.openlocfilehash: 34c0f2f88e6af5a0f822ec116e7e2334e4e29e8d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonsection-ui-element"></a><span data-ttu-id="991ab-103">Microsoft.Common.Section UI 요소</span><span class="sxs-lookup"><span data-stu-id="991ab-103">Microsoft.Common.Section UI element</span></span>
<span data-ttu-id="991ab-104">제목 아래에 하나 이상의 요소를 그룹화하는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="991ab-104">A control that groups one or more elements under a heading.</span></span> <span data-ttu-id="991ab-105">[Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="991ab-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="991ab-106">UI 샘플</span><span class="sxs-lookup"><span data-stu-id="991ab-106">UI sample</span></span>
![Microsoft.Common.Section](./media/managed-application-elements/microsoft.common.section.png)

## <a name="schema"></a><span data-ttu-id="991ab-108">스키마</span><span class="sxs-lookup"><span data-stu-id="991ab-108">Schema</span></span>
```json
{
  "name": "section1",
  "type": "Microsoft.Common.Section",
  "label": "Some section",
  "elements": [
    {
      "name": "element1",
      "type": "Microsoft.Common.TextBox",
      "label": "Some text box 1"
    },
    {
      "name": "element2",
      "type": "Microsoft.Common.TextBox",
      "label": "Some text box 2"
    }
  ],
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="991ab-109">설명</span><span class="sxs-lookup"><span data-stu-id="991ab-109">Remarks</span></span>
- <span data-ttu-id="991ab-110">`elements`는 하나 이상의 요소를 포함해야 하며, `Microsoft.Common.Section`을 제외한 모든 요소 형식을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="991ab-110">`elements` must contain at least one element, and can contain all element types except `Microsoft.Common.Section`.</span></span>
- <span data-ttu-id="991ab-111">이 요소는 `toolTip` 속성을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="991ab-111">This element doesn't support the `toolTip` property.</span></span>

## <a name="sample-output"></a><span data-ttu-id="991ab-112">샘플 출력</span><span class="sxs-lookup"><span data-stu-id="991ab-112">Sample output</span></span>
<span data-ttu-id="991ab-113">`elements`에 있는 요소의 출력 값에 액세스하려면 [basics()](managed-application-createuidefinition-functions.md#basics) 또는 [steps()](managed-application-createuidefinition-functions.md#steps) 함수와 점 표기법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="991ab-113">To access the output values of elements in `elements`, use the [basics()](managed-application-createuidefinition-functions.md#basics) or [steps()](managed-application-createuidefinition-functions.md#steps) functions and dot notation:</span></span>

```json
basics('section1').element1
```

<span data-ttu-id="991ab-114">`Microsoft.Common.Section` 형식의 요소에는 출력 값 자체가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="991ab-114">Elements of type `Microsoft.Common.Section` have no output values themselves.</span></span>

## <a name="next-steps"></a><span data-ttu-id="991ab-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="991ab-115">Next steps</span></span>
* <span data-ttu-id="991ab-116">관리되는 응용 프로그램에 대한 소개는 [Azure Managed Application 개요](managed-application-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="991ab-116">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="991ab-117">UI 정의 만들기에 대한 소개는 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="991ab-117">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="991ab-118">UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="991ab-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
