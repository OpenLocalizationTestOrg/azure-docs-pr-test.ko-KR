---
title: "Azure Managed Application TextBox UI 요소 | Microsoft Docs"
description: "Azure Managed Applications의 Microsoft.Common.TextBox UI 요소에 대해 설명합니다."
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
ms.openlocfilehash: 5a0ac5b811812c8c03f7f63aae12b8699d248ebf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommontextbox-ui-element"></a><span data-ttu-id="cfcb3-103">Microsoft.Common.TextBox UI 요소</span><span class="sxs-lookup"><span data-stu-id="cfcb3-103">Microsoft.Common.TextBox UI element</span></span>
<span data-ttu-id="cfcb3-104">서식 없는 텍스트를 편집하는 데 사용할 수 있는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="cfcb3-104">A control that can be used to edit unformatted text.</span></span> <span data-ttu-id="cfcb3-105">[Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcb3-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="cfcb3-106">UI 샘플</span><span class="sxs-lookup"><span data-stu-id="cfcb3-106">UI sample</span></span>
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a><span data-ttu-id="cfcb3-108">스키마</span><span class="sxs-lookup"><span data-stu-id="cfcb3-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Halp!",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="cfcb3-109">설명</span><span class="sxs-lookup"><span data-stu-id="cfcb3-109">Remarks</span></span>
- <span data-ttu-id="cfcb3-110">`constraints.required`를 **true**로 설정하면 텍스트 상자에서 유효성을 성공적으로 검사할 수 있는 값을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcb3-110">If `constraints.required` is set to **true**, then the text box must contain a value to validate successfully.</span></span> <span data-ttu-id="cfcb3-111">기본값은 **false**입니다.</span><span class="sxs-lookup"><span data-stu-id="cfcb3-111">The default value is **false**.</span></span>
- <span data-ttu-id="cfcb3-112">`constraints.regex`는 JavaScript 정규식 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="cfcb3-112">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="cfcb3-113">지정하면 텍스트 상자의 값이 유효성을 성공적으로 검사하기 위한 패턴과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcb3-113">If specified, then the text box's value must match the pattern to validate successfully.</span></span> <span data-ttu-id="cfcb3-114">기본값은 **null**입니다.</span><span class="sxs-lookup"><span data-stu-id="cfcb3-114">The default value is **null**.</span></span>
- <span data-ttu-id="cfcb3-115">`constraints.validationMessage`는 텍스트 상자의 값이 유효성 검사에 실패할 때 표시할 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cfcb3-115">`constraints.validationMessage` is a string to display when the text box's value fails validation.</span></span> <span data-ttu-id="cfcb3-116">지정하지 않으면 텍스트 상자의 기본 제공 유효성 검사 메시지가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfcb3-116">If not specified, then the text box's built-in validation messages are used.</span></span> <span data-ttu-id="cfcb3-117">기본값은 **null**입니다.</span><span class="sxs-lookup"><span data-stu-id="cfcb3-117">The default value is **null**.</span></span>
- <span data-ttu-id="cfcb3-118">`constraints.required`를 **false**로 설정하면 `constraints.regex`에 대한 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfcb3-118">It's possible to specify a value for `constraints.regex` when `constraints.required` is set to **false**.</span></span> <span data-ttu-id="cfcb3-119">이 시나리오에서는 텍스트 상자에서 유효성을 성공적으로 검사하는 데 값이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cfcb3-119">In this scenario, a value is not required for the text box to validate successfully.</span></span> <span data-ttu-id="cfcb3-120">지정하는 경우 정규식 패턴과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcb3-120">If one is specified, it must match the regular expression pattern.</span></span>

## <a name="sample-output"></a><span data-ttu-id="cfcb3-121">샘플 출력</span><span class="sxs-lookup"><span data-stu-id="cfcb3-121">Sample output</span></span>

```json
"foobar"
```

## <a name="next-steps"></a><span data-ttu-id="cfcb3-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cfcb3-122">Next steps</span></span>
* <span data-ttu-id="cfcb3-123">관리되는 응용 프로그램에 대한 소개는 [Azure Managed Application 개요](managed-application-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cfcb3-123">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="cfcb3-124">UI 정의 만들기에 대한 소개는 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cfcb3-124">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="cfcb3-125">UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cfcb3-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
