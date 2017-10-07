---
title: "관리 되는 응용 프로그램 PasswordBox UI 요소 aaaAzure | Microsoft Docs"
description: "Azure 관리 되는 응용 프로그램에 대 한 hello Microsoft.Common.PasswordBox UI 요소를 설명합니다."
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
ms.openlocfilehash: bcb1f54c0bee464075ed732ead9aa3f88697f49e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonpasswordbox-ui-element"></a>Microsoft.Common.PasswordBox UI 요소
암호를 확인 하 고 사용 하는 tooprovide 수 있는 컨트롤입니다. [Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.

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
- 이 요소는 hello를 지원 하지 않는 `defaultValue` 속성입니다.
- `constraints`의 구현에 대한 자세한 내용은 [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md)를 참조하세요.
- 경우 `options.hideConfirmation` 너무 설정**true**, hello 사용자 암호 확인에 대 한 두 번째 텍스트 상자 hello 숨겨집니다. hello 기본값은 **false**합니다.

## <a name="sample-output"></a>샘플 출력
```json
"p4ssw0rd"
```

## <a name="next-steps"></a>다음 단계
* 소개 toomanaged 응용 프로그램에 대 한 참조 [Azure 관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.
* 소개 toocreating UI 정의 대 한 참조 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)합니다.
* UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.
