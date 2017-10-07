---
title: "관리 되는 응용 프로그램 드롭다운 UI 요소 aaaAzure | Microsoft Docs"
description: "Azure 관리 되는 응용 프로그램에 대 한 hello Microsoft.Common.DropDown UI 요소를 설명합니다."
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
ms.openlocfilehash: 1c07a48ad66b8e8b7fd8f59561776ecb1fc6224f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommondropdown-ui-element"></a>Microsoft.Common.DropDown UI 요소
드롭다운 목록을 포함하는 선택 컨트롤입니다. [Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.

## <a name="ui-sample"></a>UI 샘플
![Microsoft.Common.DropDown](./media/managed-application-elements/microsoft.common.dropdown.png)

## <a name="schema"></a>스키마
```json
{
  "name": "element1",
  "type": "Microsoft.Common.DropDown",
  "label": "Some drop down",
  "defaultValue": "Foo",
  "toolTip": "",
  "constraints": {
    "allowedValues": [
      {
        "label": "Foo",
        "value": "Bar"
      },
      {
        "label": "Baz",
        "value": "Qux"
      }
    ]
  },
  "visible": true
}
```

## <a name="remarks"></a>설명
- 에 대 한 hello 레이블 `constraints.allowedValues` 는 항목에 대 한 표시 텍스트 hello 이며 해당 값은 선택 하면 hello 요소의 hello 출력 값입니다.
- Hello 기본값에 레이블을 지정, 경우 해야 `constraints.allowedValues`합니다. 지정 하지 않으면 첫 번째 항목 hello `constraints.allowedValues` 을 선택 합니다. hello 기본값은 **null**합니다.
- `constraints.allowedValues`는 하나 이상의 항목을 포함해야 합니다.
- 이 요소는 hello를 지원 하지 않는 `constraints.required` 속성입니다. tooemulate이이 동작을 레이블과의 값을 가진 항목이 추가 `""` (빈 문자열) 너무`constraints.allowedValues`합니다.

## <a name="sample-output"></a>샘플 출력
```json
"Bar"
```

## <a name="next-steps"></a>다음 단계
* 소개 toomanaged 응용 프로그램에 대 한 참조 [Azure 관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.
* 소개 toocreating UI 정의 대 한 참조 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)합니다.
* UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.
