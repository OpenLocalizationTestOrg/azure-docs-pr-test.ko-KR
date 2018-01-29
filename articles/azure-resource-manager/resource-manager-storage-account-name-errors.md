---
title: "Azure 저장소 계정 이름 오류 | Microsoft Docs"
description: "저장소 계정 이름을 지정할 때 발생할 수 있는 오류를 설명합니다."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: support-article
ms.date: 09/13/2017
ms.author: tomfitz
ms.openlocfilehash: dc045827fbd38054a334ff22eb30e0db6a31bac8
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="resolve-errors-for-storage-account-names"></a>저장소 계정 이름 오류 해결

이 문서에서는 저장소 계정을 배포할 때 발생할 수 있는 명명 오류에 대해 설명합니다.

## <a name="symptom"></a>증상

저장소 계정 이름에 금지된 문자가 포함되면 다음 오류가 표시됩니다.

```
Code=AccountNameInvalid
Message=S!torageckrexph7isnoc is not a valid storage account name. Storage account name must be 
between 3 and 24 characters in length and use numbers and lower-case letters only.
```

저장소 계정에 대해서는 Azure에서 고유한 리소스 이름을 제공해야 합니다. 고유한 이름을 제공하지 않으면 다음과 같은 오류 메시지가 표시됩니다.

```
Code=StorageAccountAlreadyTaken
Message=The storage account named mystorage is already taken.
```

구독에서 기존 저장소 계정과 동일한 이름의 저장소 계정을 배포하지만 다른 위치를 제공하는 경우 해당 저장소 계정이 이미 다른 위치에 이미 있다고 나타내는 오류 메시지가 표시됩니다. 이 경우 기존 저장소 계정을 삭제하거나 기존 저장소 계정과 동일한 위치를 제공합니다.

## <a name="cause"></a>원인

저장소 계정 이름은 3자에서 24자 사이여야 하고 숫자 및 소문자만 사용해야 합니다. 고유한 이름이어야 합니다.

## <a name="solution"></a>해결 방법

### <a name="solution-1"></a>해결 방법 1

저장소 계정 이름이 고유한지 확인합니다. 명명 규칙과 [uniqueString](resource-group-template-functions-string.md#uniquestring) 함수 결과를 연결하여 고유한 이름을 만들 수 있습니다.

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

### <a name="solution-2"></a>해결 방법 2

저장소 계정 이름이 24자를 초과하지 않는지 확인합니다. [uniqueString](resource-group-template-functions-string.md#uniquestring) 함수는 13자를 반환합니다. **uniqueString** 결과에 접두사 또는 접미사를 연결하는 경우 11자 이하의 값을 제공합니다.

```json
"parameters": {
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "The value to use for starting the storage account name."
      }
    }
}
```

### <a name="solution-3"></a>해결 방법 3

저장소 계정 이름에 대문자 또는 특수 문자가 포함되지 않았는지 확인합니다.