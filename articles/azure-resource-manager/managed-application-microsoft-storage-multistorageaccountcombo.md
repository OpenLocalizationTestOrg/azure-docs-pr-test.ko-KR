---
title: "관리 되는 응용 프로그램 MultiStorageAccountCombo UI 요소 aaaAzure | Microsoft Docs"
description: "Azure 관리 되는 응용 프로그램에 대 한 hello Microsoft.Storage.MultiStorageAccountCombo UI 요소를 설명합니다."
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
ms.openlocfilehash: 765be145b61c3dbf0a035a7a00aa18eee464a3eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a>Microsoft.Storage.MultiStorageAccountCombo UI 요소
공통 접두사로 시작하는 이름의 저장소 계정을 여러 개 만드는 컨트롤 그룹입니다. [Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.

## <a name="ui-sample"></a>UI 샘플
![Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a>스키마
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.MultiStorageAccountCombo",
  "label": {
    "prefix": "Storage account prefix",
    "type": "Storage account type"
  },
  "toolTip": {
    "prefix": "",
    "type": ""
  },
  "defaultValue": {
    "prefix": "sa",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a>설명
- 값에 대 한 hello `defaultValue.prefix` 저장소 계정 이름 하나 이상의 정수 toogenerate hello 순서와 연결 됩니다. 예를 들어 `defaultValue.prefix`가 **foobar**이고 `count`가 **2**이면 **foobar1** 및 **foobar2** 저장소 계정 이름이 생성됩니다. 생성된 저장소 계정 이름의 고유성에 대한 유효성 검사가 자동으로 수행됩니다.
- hello 저장소 계정 이름에 따라 사전순에 따라 생성 된 `count`합니다. 예를 들어 경우 `count` 10, hello 저장소 계정 이름은 2 자리 정수 끝나야 합니다 (01, 02, 03, 등입니다.).
- 기본값에 대 한 hello `defaultValue.prefix` 은 **null**, 및에 대 한 `defaultValue.type` 은 **Premium_LRS**합니다.
- `constraints.allowedTypes`에 지정되지 않은 형식은 숨겨지며, `constraints.excludedTypes`에 지정되지 않은 형식이 표시됩니다.
`constraints.allowedTypes`와 `constraints.excludedTypes`는 모두 선택 사항이지만 동시에 사용할 수는 없습니다.
- 또한 toogenerating 저장소 계정 이름에 `count` hello 요소에 대 한 적절 한 승수 tooset 사용된 됩니다. **2**와 같은 정적 값 또는 `[steps('step1').storageAccountCount]`와 같은 다른 요소의 동적 값을 지원합니다. hello 기본값은 **1**합니다.

## <a name="sample-output"></a>샘플 출력
```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a>다음 단계
* 소개 toomanaged 응용 프로그램에 대 한 참조 [Azure 관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.
* 소개 toocreating UI 정의 대 한 참조 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)합니다.
* UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.
