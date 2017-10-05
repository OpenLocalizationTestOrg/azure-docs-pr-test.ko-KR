---
title: "Azure Managed Application DropDown UI 요소 | Microsoft Docs"
description: "Azure Managed Applications의 Microsoft.Common.DropDown UI 요소에 대해 설명합니다."
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
ms.openlocfilehash: a769e14efbae928b811fa1f1b1c2d4fba3c7692b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
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
- `constraints.allowedValues`의 레이블은 항목에 대한 표시 텍스트이며, 해당 값은 선택한 요소의 출력 값입니다.
- 이 값을 지정하면 기본값은 `constraints.allowedValues`에 있는 레이블이어야 합니다. 지정하지 않으면 `constraints.allowedValues`의 첫 번째 항목이 선택됩니다. 기본값은 **null**입니다.
- `constraints.allowedValues`는 하나 이상의 항목을 포함해야 합니다.
- 이 요소는 `constraints.required` 속성을 지원하지 않습니다. 이 동작을 에뮬레이트하려면 레이블과 값이 `""`(빈 문자열)인 항목을 `constraints.allowedValues`에 추가합니다.

## <a name="sample-output"></a>샘플 출력
```json
"Bar"
```

## <a name="next-steps"></a>다음 단계
* 관리되는 응용 프로그램에 대한 소개는 [Azure Managed Application 개요](managed-application-overview.md)를 참조하세요.
* UI 정의 만들기에 대한 소개는 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)을 참조하세요.
* UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.
