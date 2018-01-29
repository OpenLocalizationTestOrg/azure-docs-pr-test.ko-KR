---
title: "Azure Managed Application PasswordBox UI 요소 | Microsoft Docs"
description: "Azure Managed Applications의 Microsoft.Common.PasswordBox UI 요소에 대해 설명합니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/12/2017
ms.author: tomfitz
ms.openlocfilehash: 6d9f2b7cf56375d3a609cff20e928307c13bf2b8
ms.sourcegitcommit: 3ab5ea589751d068d3e52db828742ce8ebed4761
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2017
---
# <a name="microsoftcommonpasswordbox-ui-element"></a>Microsoft.Common.PasswordBox UI 요소
암호를 제공하고 확인하는 데 사용할 수 있는 컨트롤입니다. [Azure 관리되는 응용 프로그램을 만드는](publish-service-catalog-app.md) 경우 이 요소를 사용합니다.

## <a name="ui-sample"></a>UI 샘플
![Microsoft.Common.PasswordBox](./media/managed-application-elements/microsoft.common.passwordbox.png)

## <a name="schema"></a>스키마
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

## <a name="remarks"></a>설명
- 이 요소는 `defaultValue` 속성을 지원하지 않습니다.
- `constraints`의 구현에 대한 자세한 내용은 [Microsoft.Common.TextBox](microsoft-common-textbox.md)를 참조하세요.
- `options.hideConfirmation`을 **true**로 설정하면 사용자의 암호를 확인하기 위한 두 번째 텍스트 상자가 숨겨집니다. 기본값은 **false**입니다.

## <a name="sample-output"></a>샘플 출력
```json
"p4ssw0rd"
```

## <a name="next-steps"></a>다음 단계
* 관리되는 응용 프로그램에 대한 소개는 [Azure Managed Application 개요](overview.md)를 참조하세요.
* UI 정의 만들기에 대한 소개는 [CreateUiDefinition 시작](create-uidefinition-overview.md)을 참조하세요.
* UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](create-uidefinition-elements.md)를 참조하세요.
