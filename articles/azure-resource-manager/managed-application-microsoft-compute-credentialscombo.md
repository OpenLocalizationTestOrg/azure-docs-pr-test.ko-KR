---
title: "Azure Managed Application CredentialsCombo UI 요소 | Microsoft Docs"
description: "Azure Managed Applications의 Microsoft.Compute.CredentialsCombo UI 요소에 대해 설명합니다."
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
ms.openlocfilehash: 254f383ee6f7cb9f7051fa135d85319a22c3c369
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputecredentialscombo-ui-element"></a><span data-ttu-id="19304-103">Microsoft.Compute.CredentialsCombo UI 요소</span><span class="sxs-lookup"><span data-stu-id="19304-103">Microsoft.Compute.CredentialsCombo UI element</span></span>
<span data-ttu-id="19304-104">Windows 및 Linux 암호와 SSH 공개 키에 대한 유효성 검사가 포함된 기본 제공 컨트롤 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="19304-104">A group of controls with built-in validation for Windows and Linux passwords and SSH public keys.</span></span> <span data-ttu-id="19304-105">[Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="19304-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="19304-106">UI 샘플</span><span class="sxs-lookup"><span data-stu-id="19304-106">UI sample</span></span>
![Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a><span data-ttu-id="19304-108">스키마</span><span class="sxs-lookup"><span data-stu-id="19304-108">Schema</span></span>
<span data-ttu-id="19304-109">`osPlatform`이 **Windows**이면 다음 스키마가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="19304-109">If `osPlatform` is **Windows**, then the following schema is used:</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": {
    "password": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "The password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false
  },
  "osPlatform": "Windows",
  "visible": true
}
```

<span data-ttu-id="19304-110">`osPlatform`이 **Linux**이면 다음 스키마가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="19304-110">If `osPlatform` is **Linux**, then the following schema is used:</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "authenticationType": "Authentication type",
    "password": "Password",
    "confirmPassword": "Confirm password",
    "sshPublicKey": "SSH public key"
  },
  "toolTip": {
    "authenticationType": "",
    "password": "",
    "sshPublicKey": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "The password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false,
    "hidePassword": false
  },
  "osPlatform": "Linux",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="19304-111">설명</span><span class="sxs-lookup"><span data-stu-id="19304-111">Remarks</span></span>
- <span data-ttu-id="19304-112">`osPlatform`을 지정해야 하며 **Windows** 또는 **Linux**일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19304-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="19304-113">`constraints.required`을 **true**로 설정하면 암호 또는 SSH 공개 키 텍스트 상자에서 유효성을 성공적으로 검사하기 위한 값을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19304-113">If `constraints.required` is set to **true**, then the password or SSH public key text boxes must contain values to validate successfully.</span></span> <span data-ttu-id="19304-114">기본값은 **true**입니다.</span><span class="sxs-lookup"><span data-stu-id="19304-114">The default value is **true**.</span></span>
- <span data-ttu-id="19304-115">`options.hideConfirmation`을 **true**로 설정하면 사용자의 암호를 확인하는 두 번째 텍스트 상자가 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="19304-115">If `options.hideConfirmation` is set to **true**, then the second text box for confirming the user's password is hidden.</span></span> <span data-ttu-id="19304-116">기본값은 **false**입니다.</span><span class="sxs-lookup"><span data-stu-id="19304-116">The default value is **false**.</span></span>
- <span data-ttu-id="19304-117">`options.hidePassword`를 **true**로 설정하면 암호 인증을 사용하는 옵션이 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="19304-117">If `options.hidePassword` is set to **true**, then the option to use password authentication is hidden.</span></span> <span data-ttu-id="19304-118">`osPlatform`이 **Linux**인 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19304-118">It can be used only when `osPlatform` is **Linux**.</span></span> <span data-ttu-id="19304-119">기본값은 **false**입니다.</span><span class="sxs-lookup"><span data-stu-id="19304-119">The default value is **false**.</span></span>
- <span data-ttu-id="19304-120">허용되는 암호에 대한 추가 제한 조건은 `customPasswordRegex` 속성을 사용하여 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19304-120">Additional constraints on the allowed passwords can be implemented by using the `customPasswordRegex` property.</span></span> <span data-ttu-id="19304-121">암호가 사용자 지정 유효성 검사에 실패하면 `customValidationMessage`의 문자열이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="19304-121">The string in `customValidationMessage` is displayed when a password fails custom validation.</span></span> <span data-ttu-id="19304-122">두 속성의 기본값은 **null**입니다.</span><span class="sxs-lookup"><span data-stu-id="19304-122">The default value for both properties is **null**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="19304-123">샘플 출력</span><span class="sxs-lookup"><span data-stu-id="19304-123">Sample output</span></span>
<span data-ttu-id="19304-124">`osPlatform`이 **Windows**이거나 사용자가 SSH 공개 키 대신 암호를 제공한 경우 예상되는 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="19304-124">If `osPlatform` is **Windows**, or the user provided a password instead of an SSH public key, then the following output is expected:</span></span>

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

<span data-ttu-id="19304-125">사용자가 SSH 공개 키를 제공한 경우 예상되는 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="19304-125">If the user provided an SSH public key, then the following output is expected:</span></span>
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a><span data-ttu-id="19304-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="19304-126">Next steps</span></span>
* <span data-ttu-id="19304-127">관리되는 응용 프로그램에 대한 소개는 [Azure Managed Application 개요](managed-application-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19304-127">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="19304-128">UI 정의 만들기에 대한 소개는 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19304-128">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="19304-129">UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19304-129">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
