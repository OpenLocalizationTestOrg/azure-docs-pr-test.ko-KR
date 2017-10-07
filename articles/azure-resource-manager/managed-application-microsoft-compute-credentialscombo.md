---
title: "관리 되는 응용 프로그램 CredentialsCombo UI 요소 aaaAzure | Microsoft Docs"
description: "Azure 관리 되는 응용 프로그램에 대 한 hello Microsoft.Compute.CredentialsCombo UI 요소를 설명합니다."
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
ms.openlocfilehash: d44a3929ebb7a5ff78b72f9eaeb6e52b098e266f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputecredentialscombo-ui-element"></a>Microsoft.Compute.CredentialsCombo UI 요소
Windows 및 Linux 암호와 SSH 공개 키에 대한 유효성 검사가 포함된 기본 제공 컨트롤 그룹입니다. [Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.

## <a name="ui-sample"></a>UI 샘플
![Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a>스키마
경우 `osPlatform` 은 **Windows**, hello 다음 스키마가 사용 됩니다.
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
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false
  },
  "osPlatform": "Windows",
  "visible": true
}
```

경우 `osPlatform` 은 **Linux**, hello 다음 스키마가 사용 됩니다.
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
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false,
    "hidePassword": false
  },
  "osPlatform": "Linux",
  "visible": true
}
```

## <a name="remarks"></a>설명
- `osPlatform`을 지정해야 하며 **Windows** 또는 **Linux**일 수 있습니다.
- 경우 `constraints.required` 너무 설정**true**, 한 다음 암호를 hello 또는 SSH 공개 키 텍스트 상자 값 toovalidate를 성공적으로 포함 해야 합니다. hello 기본값은 **true**합니다.
- 경우 `options.hideConfirmation` 너무 설정 되어**true**, 다음 hello 사용자 암호 확인에 대 한 두 번째 텍스트 상자 hello 숨겨집니다. hello 기본값은 **false**합니다.
- 경우 `options.hidePassword` 너무 설정 되어**true**, 다음 hello 옵션 toouse 암호 인증 숨겨집니다. `osPlatform`이 **Linux**인 경우에만 사용할 수 있습니다. 기본값은 **false**입니다.
- Hello 대 한 추가 제약 조건을 허용 hello를 사용 하 여 암호를 구현할 수 있습니다 `customPasswordRegex` 속성입니다. 문자열 hello `customValidationMessage` 암호를 사용자 지정 유효성 검사에 실패 하는 경우에 표시 됩니다. hello 두 속성 모두에 대 한 기본값은 **null**합니다.

## <a name="sample-output"></a>샘플 출력
경우 `osPlatform` 은 **Windows**, 또는 SSH 공개 키 대신 암호를 제공 하는 hello 사용자 한 hello 다음 예상 출력은:

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

Hello 사용자 SSH 공개 키를 제공 하는 경우 다음 hello 다음 예상 출력은:
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a>다음 단계
* 소개 toomanaged 응용 프로그램에 대 한 참조 [Azure 관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.
* 소개 toocreating UI 정의 대 한 참조 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)합니다.
* UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.
