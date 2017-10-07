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
# <a name="microsoftcommontextbox-ui-element"></a>Microsoft.Common.TextBox UI 요소
사용 되는 tooedit 일 수 있는 컨트롤 서식 없는 텍스트입니다. [Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.

## <a name="ui-sample"></a>UI 샘플
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a>스키마
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

## <a name="remarks"></a>설명
- 경우 `constraints.required` 너무 설정**true**, hello 텍스트 상자 값 toovalidate를 성공적으로 포함 해야 합니다. hello 기본값은 **false**합니다.
- `constraints.regex`는 JavaScript 정규식 패턴입니다. 를 지정 하는 경우 다음 hello 텍스트 상자의 값 일치 해야 hello 패턴 toovalidate 성공적으로 합니다. 기본값은 **null**입니다.
- `constraints.validationMessage`문자열 toodisplay 때 hello 텍스트 상자의 값 유효성 검사에 실패 합니다. 그렇지 않은 경우 지정 하면 다음 hello 입력란의 기본 제공 유효성 검사 메시지에 사용 됩니다. hello 기본값은 **null**합니다.
- 가능한 toospecify 값에 대 한 `constraints.regex` 때 `constraints.required` 너무 설정**false**합니다. 이 경우에는 값은 필요 하지 텍스트 상자 toovalidate hello에 대 한 성공적으로 합니다. 지정 된 경우 hello 정규식 패턴과 일치 해야 합니다.

## <a name="sample-output"></a>샘플 출력

```json
"foobar"
```

## <a name="next-steps"></a>다음 단계
* 소개 toomanaged 응용 프로그램에 대 한 참조 [Azure 관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.
* 소개 toocreating UI 정의 대 한 참조 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)합니다.
* UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.
