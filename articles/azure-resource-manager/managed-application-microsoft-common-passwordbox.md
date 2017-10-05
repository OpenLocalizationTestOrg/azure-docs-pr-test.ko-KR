---
title: "Azure Managed Application PasswordBox UI 요소 | Microsoft Docs"
description: "Azure Managed Applications의 Microsoft.Common.PasswordBox UI 요소에 대해 설명합니다."
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
ms.openlocfilehash: 196a4b8f77145f83e46b4b23e148bb3a9dffc1b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonpasswordbox-ui-element"></a><span data-ttu-id="c3816-103">Microsoft.Common.PasswordBox UI 요소</span><span class="sxs-lookup"><span data-stu-id="c3816-103">Microsoft.Common.PasswordBox UI element</span></span>
<span data-ttu-id="c3816-104">암호를 제공하고 확인하는 데 사용할 수 있는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="c3816-104">A control that can be used to provide and confirm a password.</span></span> <span data-ttu-id="c3816-105">[Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3816-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="c3816-106">UI 샘플</span><span class="sxs-lookup"><span data-stu-id="c3816-106">UI sample</span></span>
![Microsoft.Common.PasswordBox](./media/managed-application-elements/microsoft.common.passwordbox.png)

## <a name="schema"></a><span data-ttu-id="c3816-108">스키마</span><span class="sxs-lookup"><span data-stu-id="c3816-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.PasswordBox",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "",
    "validationMessage": ""
  },
  "options": {
    "hideConfirmation": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="c3816-109">설명</span><span class="sxs-lookup"><span data-stu-id="c3816-109">Remarks</span></span>
- <span data-ttu-id="c3816-110">이 요소는 `defaultValue` 속성을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3816-110">This element doesn't support the `defaultValue` property.</span></span>
- <span data-ttu-id="c3816-111">`constraints`의 구현에 대한 자세한 내용은 [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3816-111">For implementation details of `constraints`, see [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span></span>
- <span data-ttu-id="c3816-112">`options.hideConfirmation`을 **true**로 설정하면 사용자의 암호를 확인하기 위한 두 번째 텍스트 상자가 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="c3816-112">If `options.hideConfirmation` is set to **true**, the second text box for confirming the user's password is hidden.</span></span> <span data-ttu-id="c3816-113">기본값은 **false**입니다.</span><span class="sxs-lookup"><span data-stu-id="c3816-113">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="c3816-114">샘플 출력</span><span class="sxs-lookup"><span data-stu-id="c3816-114">Sample output</span></span>
```json
"p4ssw0rd"
```

## <a name="next-steps"></a><span data-ttu-id="c3816-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c3816-115">Next steps</span></span>
* <span data-ttu-id="c3816-116">관리되는 응용 프로그램에 대한 소개는 [Azure Managed Application 개요](managed-application-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3816-116">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="c3816-117">UI 정의 만들기에 대한 소개는 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3816-117">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="c3816-118">UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3816-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
