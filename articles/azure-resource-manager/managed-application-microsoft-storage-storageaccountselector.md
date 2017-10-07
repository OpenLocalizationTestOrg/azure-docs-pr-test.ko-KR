---
title: "관리 되는 응용 프로그램 StorageAccountSelector UI 요소 aaaAzure | Microsoft Docs"
description: "Azure 관리 되는 응용 프로그램에 대 한 hello Microsoft.Storage.StorageAccountSelector UI 요소를 설명합니다."
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
ms.openlocfilehash: a2c9545feed4c4afb3c64b30b42c94d5382a108d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftstoragestorageaccountselector-ui-element"></a>Microsoft.Storage.StorageAccountSelector UI 요소
새 또는 기존 저장소 계정을 선택하는 컨트롤입니다. [Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.

## <a name="ui-sample"></a>UI 샘플
![Microsoft.Storage.StorageAccountSelector](./media/managed-application-elements/microsoft.storage.storageaccountselector.png)

## <a name="schema"></a>스키마
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.StorageAccountSelector",
  "label": "Storage account",
  "toolTip": "",
  "defaultValue": {
    "name": "storageaccount01",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "options": {
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a>설명
- 지정하는 경우 `defaultValue.name`의 고유성에 대한 유효성 검사가 자동으로 수행됩니다. Hello 저장소 계정 이름이 고유 하지 않으면 hello 사용자 다른 이름을 지정 하거나 기존 저장소 계정을 선택 해야 합니다.
- 에 대 한 기본값을 hello `defaultValue.type` 은 **Premium_LRS**합니다.
- `constraints.allowedTypes`에 지정되지 않은 형식은 숨겨지며, `constraints.excludedTypes`에 지정되지 않은 형식이 표시됩니다.
`constraints.allowedTypes`와 `constraints.excludedTypes`는 모두 선택 사항이지만 동시에 사용할 수는 없습니다.
- 경우 `options.hideExisting` 은 **true**, hello 사용자는 기존 저장소 계정을 선택할 수 없습니다. hello 기본값은 **false**합니다.


## <a name="sample-output"></a>샘플 출력
```json
{
  "name": "storageaccount01",
  "resourceGroup": "rg01",
  "type": "Premium_LRS",
  "newOrExisting": "new"
}
```

## <a name="next-steps"></a>다음 단계
* 소개 toomanaged 응용 프로그램에 대 한 참조 [Azure 관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.
* 소개 toocreating UI 정의 대 한 참조 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)합니다.
* UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.
