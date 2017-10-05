---
title: "Azure Managed Application UserNameTextBox UI 요소 | Microsoft Docs"
description: "Azure Managed Applications의 Microsoft.Compute.UserNameTextBox UI 요소에 대해 설명합니다."
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
ms.openlocfilehash: c90be5a0ed3aadda81d7ec9b5388a96472f69af0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputeusernametextbox-ui-element"></a><span data-ttu-id="5a633-103">Microsoft.Compute.UserNameTextBox UI 요소</span><span class="sxs-lookup"><span data-stu-id="5a633-103">Microsoft.Compute.UserNameTextBox UI element</span></span>
<span data-ttu-id="5a633-104">Windows 및 Linux 사용자 이름에 대한 기본 제공 유효성 검사가 포함된 텍스트 상자 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="5a633-104">A text box control with built-in validation for Windows and Linux user names.</span></span> <span data-ttu-id="5a633-105">[Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a633-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="5a633-106">UI 샘플</span><span class="sxs-lookup"><span data-stu-id="5a633-106">UI sample</span></span>
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a><span data-ttu-id="5a633-108">스키마</span><span class="sxs-lookup"><span data-stu-id="5a633-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.UserNameTextBox",
  "label": "User name",
  "defaultValue": "",
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-30 characters long."
  },
  "osPlatform": "Windows",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="5a633-109">설명</span><span class="sxs-lookup"><span data-stu-id="5a633-109">Remarks</span></span>
- <span data-ttu-id="5a633-110">`constraints.required`를 **true**로 설정하면 텍스트 상자에서 유효성을 성공적으로 검사할 수 있는 값을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a633-110">If `constraints.required` is set to **true**, then the text box must contain a value to validate successfully.</span></span> <span data-ttu-id="5a633-111">기본값은 **true**입니다.</span><span class="sxs-lookup"><span data-stu-id="5a633-111">The default value is **true**.</span></span>
- <span data-ttu-id="5a633-112">`osPlatform`을 지정해야 하며 **Windows** 또는 **Linux**일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a633-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="5a633-113">`constraints.regex`는 JavaScript 정규식 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="5a633-113">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="5a633-114">지정하면 텍스트 상자의 값이 유효성을 성공적으로 검사하기 위한 패턴과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a633-114">If specified, then the text box's value must match the pattern to validate successfully.</span></span> <span data-ttu-id="5a633-115">기본값은 **null**입니다.</span><span class="sxs-lookup"><span data-stu-id="5a633-115">The default value is **null**.</span></span>
- <span data-ttu-id="5a633-116">`constraints.validationMessage`는 텍스트 상자의 값이 `constraints.regex`에 지정된 유효성 검사에 실패할 때 표시할 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="5a633-116">`constraints.validationMessage` is a string to display when the text box's value fails the validation specified by `constraints.regex`.</span></span> <span data-ttu-id="5a633-117">지정하지 않으면 텍스트 상자의 기본 제공 유효성 검사 메시지가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a633-117">If not specified, then the text box's built-in validation messages are used.</span></span> <span data-ttu-id="5a633-118">기본값은 **null**입니다.</span><span class="sxs-lookup"><span data-stu-id="5a633-118">The default value is **null**.</span></span>
- <span data-ttu-id="5a633-119">이 요소에는 `osPlatform`에 지정된 값을 기반으로 하는 기본 제공 유효성 검사가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a633-119">This element has built-in validation that is based on the value specified for `osPlatform`.</span></span> <span data-ttu-id="5a633-120">기본 제공 유효성 검사는 사용자 지정 정규식과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a633-120">The built-in validation can be used along with a custom regular expression.</span></span>
<span data-ttu-id="5a633-121">`constraints.regex`에 대한 값을 지정하면 기본 제공 및 사용자 지정 유효성 검사가 모두 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a633-121">If a value for `constraints.regex` is specified, then both the built-in and custom validations are triggered.</span></span>

## <a name="sample-output"></a><span data-ttu-id="5a633-122">샘플 출력</span><span class="sxs-lookup"><span data-stu-id="5a633-122">Sample output</span></span>
```json
"tabrezm"
```

## <a name="next-steps"></a><span data-ttu-id="5a633-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5a633-123">Next steps</span></span>
* <span data-ttu-id="5a633-124">관리되는 응용 프로그램에 대한 소개는 [Azure Managed Application 개요](managed-application-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a633-124">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="5a633-125">UI 정의 만들기에 대한 소개는 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a633-125">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="5a633-126">UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a633-126">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
