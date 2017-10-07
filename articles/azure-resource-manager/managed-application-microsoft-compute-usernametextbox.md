---
title: "관리 되는 응용 프로그램 UserNameTextBox UI 요소 aaaAzure | Microsoft Docs"
description: "Azure 관리 되는 응용 프로그램에 대 한 hello Microsoft.Compute.UserNameTextBox UI 요소를 설명합니다."
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
ms.openlocfilehash: 33092014e804c4aabd56ba49144d9cd4d6a5fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputeusernametextbox-ui-element"></a><span data-ttu-id="f6efc-103">Microsoft.Compute.UserNameTextBox UI 요소</span><span class="sxs-lookup"><span data-stu-id="f6efc-103">Microsoft.Compute.UserNameTextBox UI element</span></span>
<span data-ttu-id="f6efc-104">Windows 및 Linux 사용자 이름에 대한 기본 제공 유효성 검사가 포함된 텍스트 상자 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="f6efc-104">A text box control with built-in validation for Windows and Linux user names.</span></span> <span data-ttu-id="f6efc-105">[Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f6efc-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="f6efc-106">UI 샘플</span><span class="sxs-lookup"><span data-stu-id="f6efc-106">UI sample</span></span>
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a><span data-ttu-id="f6efc-108">스키마</span><span class="sxs-lookup"><span data-stu-id="f6efc-108">Schema</span></span>
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
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "osPlatform": "Windows",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="f6efc-109">설명</span><span class="sxs-lookup"><span data-stu-id="f6efc-109">Remarks</span></span>
- <span data-ttu-id="f6efc-110">경우 `constraints.required` 너무 설정**true**, hello 텍스트 상자 값 toovalidate를 성공적으로 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6efc-110">If `constraints.required` is set too**true**, then hello text box must contain a value toovalidate successfully.</span></span> <span data-ttu-id="f6efc-111">hello 기본값은 **true**합니다.</span><span class="sxs-lookup"><span data-stu-id="f6efc-111">hello default value is **true**.</span></span>
- <span data-ttu-id="f6efc-112">`osPlatform`을 지정해야 하며 **Windows** 또는 **Linux**일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6efc-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="f6efc-113">`constraints.regex`는 JavaScript 정규식 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="f6efc-113">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="f6efc-114">를 지정 하는 경우 다음 hello 텍스트 상자의 값 일치 해야 hello 패턴 toovalidate 성공적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6efc-114">If specified, then hello text box's value must match hello pattern toovalidate successfully.</span></span> <span data-ttu-id="f6efc-115">기본값은 **null**입니다.</span><span class="sxs-lookup"><span data-stu-id="f6efc-115">The default value is **null**.</span></span>
- <span data-ttu-id="f6efc-116">`constraints.validationMessage`문자열 toodisplay hello 텍스트 상자의 값으로 지정 된 hello 유효성 검사에 실패 하는 경우 `constraints.regex`합니다.</span><span class="sxs-lookup"><span data-stu-id="f6efc-116">`constraints.validationMessage` is a string toodisplay when hello text box's value fails hello validation specified by `constraints.regex`.</span></span> <span data-ttu-id="f6efc-117">그렇지 않은 경우 지정 하면 다음 hello 입력란의 기본 제공 유효성 검사 메시지에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6efc-117">If not specified, then hello text box's built-in validation messages are used.</span></span> <span data-ttu-id="f6efc-118">hello 기본값은 **null**합니다.</span><span class="sxs-lookup"><span data-stu-id="f6efc-118">hello default value is **null**.</span></span>
- <span data-ttu-id="f6efc-119">이 요소에 지정 된 hello 값을 기반으로 하는 기본 제공 유효성 검사에 `osPlatform`합니다.</span><span class="sxs-lookup"><span data-stu-id="f6efc-119">This element has built-in validation that is based on hello value specified for `osPlatform`.</span></span> <span data-ttu-id="f6efc-120">hello 기본 제공 유효성 검사는 사용자 지정 정규식을 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6efc-120">hello built-in validation can be used along with a custom regular expression.</span></span>
<span data-ttu-id="f6efc-121">값을 `constraints.regex` 를 지정 하면 둘 다 hello 기본 제공 및 사용자 지정 유효성 검사 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6efc-121">If a value for `constraints.regex` is specified, then both hello built-in and custom validations are triggered.</span></span>

## <a name="sample-output"></a><span data-ttu-id="f6efc-122">샘플 출력</span><span class="sxs-lookup"><span data-stu-id="f6efc-122">Sample output</span></span>
```json
"tabrezm"
```

## <a name="next-steps"></a><span data-ttu-id="f6efc-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f6efc-123">Next steps</span></span>
* <span data-ttu-id="f6efc-124">소개 toomanaged 응용 프로그램에 대 한 참조 [Azure 관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f6efc-124">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="f6efc-125">소개 toocreating UI 정의 대 한 참조 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f6efc-125">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="f6efc-126">UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6efc-126">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
