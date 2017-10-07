---
title: "관리 되는 응용 프로그램 섹션 UI 요소 aaaAzure | Microsoft Docs"
description: "Azure 관리 되는 응용 프로그램에 대 한 hello Microsoft.Common.Section UI 요소를 설명합니다."
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
ms.openlocfilehash: d20b365b12fab66177e1a12db2ebbeefe507212e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonsection-ui-element"></a><span data-ttu-id="8e60a-103">Microsoft.Common.Section UI 요소</span><span class="sxs-lookup"><span data-stu-id="8e60a-103">Microsoft.Common.Section UI element</span></span>
<span data-ttu-id="8e60a-104">제목 아래에 하나 이상의 요소를 그룹화하는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="8e60a-104">A control that groups one or more elements under a heading.</span></span> <span data-ttu-id="8e60a-105">[Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e60a-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="8e60a-106">UI 샘플</span><span class="sxs-lookup"><span data-stu-id="8e60a-106">UI sample</span></span>
![Microsoft.Common.Section](./media/managed-application-elements/microsoft.common.section.png)

## <a name="schema"></a><span data-ttu-id="8e60a-108">스키마</span><span class="sxs-lookup"><span data-stu-id="8e60a-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="8e60a-109">설명</span><span class="sxs-lookup"><span data-stu-id="8e60a-109">Remarks</span></span>
- <span data-ttu-id="8e60a-110">`elements`는 하나 이상의 요소를 포함해야 하며, `Microsoft.Common.Section`을 제외한 모든 요소 형식을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e60a-110">`elements` must contain at least one element, and can contain all element types except `Microsoft.Common.Section`.</span></span>
- <span data-ttu-id="8e60a-111">이 요소는 hello를 지원 하지 않는 `toolTip` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="8e60a-111">This element doesn't support hello `toolTip` property.</span></span>

## <a name="sample-output"></a><span data-ttu-id="8e60a-112">샘플 출력</span><span class="sxs-lookup"><span data-stu-id="8e60a-112">Sample output</span></span>
<span data-ttu-id="8e60a-113">출력에 있는 요소의 값을 tooaccess hello `elements`, hello를 사용 하 여 [basics()](managed-application-createuidefinition-functions.md#basics) 또는 [steps()](managed-application-createuidefinition-functions.md#steps) 함수와 점 표기법:</span><span class="sxs-lookup"><span data-stu-id="8e60a-113">tooaccess hello output values of elements in `elements`, use hello [basics()](managed-application-createuidefinition-functions.md#basics) or [steps()](managed-application-createuidefinition-functions.md#steps) functions and dot notation:</span></span>

```json
basics('section1').element1
```

<span data-ttu-id="8e60a-114">`Microsoft.Common.Section` 형식의 요소에는 출력 값 자체가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8e60a-114">Elements of type `Microsoft.Common.Section` have no output values themselves.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e60a-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8e60a-115">Next steps</span></span>
* <span data-ttu-id="8e60a-116">소개 toomanaged 응용 프로그램에 대 한 참조 [Azure 관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e60a-116">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="8e60a-117">소개 toocreating UI 정의 대 한 참조 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e60a-117">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="8e60a-118">UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e60a-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
