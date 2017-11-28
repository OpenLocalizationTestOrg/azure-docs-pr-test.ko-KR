---
title: "관리 되는 응용 프로그램 TextBox UI 요소 aaaAzure | Microsoft Docs"
description: "Azure 관리 되는 응용 프로그램에 대 한 hello Microsoft.Common.TextBox UI 요소를 설명합니다."
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
ms.openlocfilehash: 11771cd1d689b720384df98b8d1465703068af37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommontextbox-ui-element"></a><span data-ttu-id="7834c-103">Microsoft.Common.TextBox UI 요소</span><span class="sxs-lookup"><span data-stu-id="7834c-103">Microsoft.Common.TextBox UI element</span></span>
<span data-ttu-id="7834c-104">사용 되는 tooedit 일 수 있는 컨트롤 서식 없는 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="7834c-104">A control that can be used tooedit unformatted text.</span></span> <span data-ttu-id="7834c-105">[Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7834c-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="7834c-106">UI 샘플</span><span class="sxs-lookup"><span data-stu-id="7834c-106">UI sample</span></span>
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a><span data-ttu-id="7834c-108">스키마</span><span class="sxs-lookup"><span data-stu-id="7834c-108">Schema</span></span>
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
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="7834c-109">설명</span><span class="sxs-lookup"><span data-stu-id="7834c-109">Remarks</span></span>
- <span data-ttu-id="7834c-110">경우 `constraints.required` 너무 설정**true**, hello 텍스트 상자 값 toovalidate를 성공적으로 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7834c-110">If `constraints.required` is set too**true**, then hello text box must contain a value toovalidate successfully.</span></span> <span data-ttu-id="7834c-111">hello 기본값은 **false**합니다.</span><span class="sxs-lookup"><span data-stu-id="7834c-111">hello default value is **false**.</span></span>
- <span data-ttu-id="7834c-112">`constraints.regex`는 JavaScript 정규식 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="7834c-112">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="7834c-113">를 지정 하는 경우 다음 hello 텍스트 상자의 값 일치 해야 hello 패턴 toovalidate 성공적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7834c-113">If specified, then hello text box's value must match hello pattern toovalidate successfully.</span></span> <span data-ttu-id="7834c-114">기본값은 **null**입니다.</span><span class="sxs-lookup"><span data-stu-id="7834c-114">The default value is **null**.</span></span>
- <span data-ttu-id="7834c-115">`constraints.validationMessage`문자열 toodisplay 때 hello 텍스트 상자의 값 유효성 검사에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="7834c-115">`constraints.validationMessage` is a string toodisplay when hello text box's value fails validation.</span></span> <span data-ttu-id="7834c-116">그렇지 않은 경우 지정 하면 다음 hello 입력란의 기본 제공 유효성 검사 메시지에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7834c-116">If not specified, then hello text box's built-in validation messages are used.</span></span> <span data-ttu-id="7834c-117">hello 기본값은 **null**합니다.</span><span class="sxs-lookup"><span data-stu-id="7834c-117">hello default value is **null**.</span></span>
- <span data-ttu-id="7834c-118">가능한 toospecify 값에 대 한 `constraints.regex` 때 `constraints.required` 너무 설정**false**합니다.</span><span class="sxs-lookup"><span data-stu-id="7834c-118">It's possible toospecify a value for `constraints.regex` when `constraints.required` is set too**false**.</span></span> <span data-ttu-id="7834c-119">이 경우에는 값은 필요 하지 텍스트 상자 toovalidate hello에 대 한 성공적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7834c-119">In this scenario, a value is not required for hello text box toovalidate successfully.</span></span> <span data-ttu-id="7834c-120">지정 된 경우 hello 정규식 패턴과 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7834c-120">If one is specified, it must match hello regular expression pattern.</span></span>

## <a name="sample-output"></a><span data-ttu-id="7834c-121">샘플 출력</span><span class="sxs-lookup"><span data-stu-id="7834c-121">Sample output</span></span>

```json
"foobar"
```

## <a name="next-steps"></a><span data-ttu-id="7834c-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7834c-122">Next steps</span></span>
* <span data-ttu-id="7834c-123">소개 toomanaged 응용 프로그램에 대 한 참조 [Azure 관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7834c-123">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="7834c-124">소개 toocreating UI 정의 대 한 참조 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7834c-124">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="7834c-125">UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7834c-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
