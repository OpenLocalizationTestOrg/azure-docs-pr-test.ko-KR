---
title: "aaaAzure 리소스 관리자 템플릿 함수 비교 | Microsoft Docs"
description: "Hello 함수 toouse Azure 리소스 관리자 템플릿 toocompare 값에 설명합니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: tomfitz
ms.openlocfilehash: ebcfc9ed6c93f8b540ec4c066e9457c621800b7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a>Azure Resource Manager 템플릿용 비교 함수

Resource Manager는 템플릿에서 비교를 수행하기 위한 몇 가지 함수를 제공합니다.

* [equals](#equals)
* [greater](#greater)
* [greaterOrEquals](#greaterorequals)
* [less](#less)
* [lessOrEquals](#lessorequals)

## <a name="equals"></a>equals
`equals(arg1, arg2)`

두 값이 서로 일치하는지 여부를 확인합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |int, 문자열, 배열 또는 개체 |같음에 대 한 첫 번째 값 toocheck을 hello 합니다. |
| arg2 |예 |int, 문자열, 배열 또는 개체 |같음에 대 한 두 번째 값 toocheck을 hello 합니다. |

### <a name="return-value"></a>반환 값

반환 **True** hello 값이 같고, 그렇지 않으면 **False**합니다.

### <a name="remarks"></a>설명

hello equals 함수는 대개 hello로 `condition` 요소 tootest 리소스 배포 되었는지 여부.

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

### <a name="example"></a>예제

hello 예제 서식 파일에는 다양 한 유형의 값이 같은지 확인합니다. 모든 hello 기본값 True를 반환 합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 1
        },
        "firstString": {
            "type": "string",
            "defaultValue": "a"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "firstObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[equals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[equals(parameters('firstString'), parameters('secondString'))]"
        },
        "checkArrays": {
            "type": "bool",
            "value": "[equals(parameters('firstArray'), parameters('secondArray'))]"
        },
        "checkObjects": {
            "type": "bool",
            "value": "[equals(parameters('firstObject'), parameters('secondObject'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| checkInts | Bool | True |
| checkStrings | Bool | True |
| checkArrays | Bool | True |
| checkObjects | Bool | True |


hello 다음 예제에서는 [하지](resource-group-template-functions-logical.md#not) 와 **equals**합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "checkNotEquals": {
            "type": "bool",
            "value": "[not(equals(1, 2))]"
        }
    }
```

앞 예제는 hello hello 출력은:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| checkNotEquals | Bool | True |


## <a name="greater"></a>greater
`greater(arg1, arg2)`

첫 번째 값 hello hello 두 번째 값 보다 큰지 여부를 확인 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |int 또는 문자열 |hello hello 큰 비교에 대 한 첫 번째 값입니다. |
| arg2 |예 |int 또는 문자열 |hello hello 큰 비교에 대 한 두 번째 값입니다. |

### <a name="return-value"></a>반환 값

반환 **True** hello 첫 번째 값이 고, 그렇지 않으면 hello 두 번째 값 보다 큰 경우 **False**합니다.

### <a name="example"></a>예제

hello 예제 템플릿 hello 하나의 값 hello 다른 보다 큰지 여부를 확인 합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greater(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greater(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| checkInts | Bool | False |
| checkStrings | Bool | True |


## <a name="greaterorequals"></a>greaterOrEquals
`greaterOrEquals(arg1, arg2)`

Hello 첫 번째 값이 둘째 값 보다 크거나 같은 toohello 인지 확인 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |int 또는 문자열 |hello hello 크거나 같음 비교에 대 한 첫 번째 값입니다. |
| arg2 |예 |int 또는 문자열 |hello hello 크거나 같음 비교에 대 한 두 번째 값입니다. |

### <a name="return-value"></a>반환 값

반환 **True** hello 첫 번째 값이 둘째 값 보다 크거나 같은 toohello; 그렇지 않으면 **False**합니다.

### <a name="example"></a>예제

hello 예제 서식 파일 또는 다른 같은 toohello hello 하나의 값 보다 큰 인지 확인 합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| checkInts | Bool | False |
| checkStrings | Bool | True |



## <a name="less"></a>less
`less(arg1, arg2)`

여부 hello 첫 번째 값 보다 작은 hello 두 번째 값을 확인 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |int 또는 문자열 |hello 비교 덜 hello에 대 한 첫 번째 값입니다. |
| arg2 |예 |int 또는 문자열 |hello 비교 덜 hello에 대 한 두 번째 값입니다. |

### <a name="return-value"></a>반환 값

반환 **True** hello 첫 번째 값을 사용 하면 hello 보다 작으면 두 번째 값입니다; 그렇지 않으면 **False**합니다.

### <a name="example"></a>예제

hello 예제 템플릿 hello 하나의 값 hello 다른 보다 작은지 여부를 확인 합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[less(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[less(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| checkInts | Bool | True |
| checkStrings | Bool | False |


## <a name="lessorequals"></a>lessOrEquals
`lessOrEquals(arg1, arg2)`

Hello 첫 번째 값 보다 작거나 같은 인지를 확인 toohello 두 번째 값입니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |int 또는 문자열 |덜 hello에 대 한 첫 번째 값 hello 또는 같음 비교 합니다. |
| arg2 |예 |int 또는 문자열 |hello 적은 hello에 대 한 두 번째 값 또는 같음 비교 합니다. |

### <a name="return-value"></a>반환 값

반환 **True** hello 첫 번째 값 보다 작거나 같은 경우 toohello 두 번째 값, 그렇지 않으면 **False**합니다.

### <a name="example"></a>예제

hello 예제 서식 파일 인지를 확인 hello 하나의 값 보다 작거나 같은 다른 toohello 합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| checkInts | Bool | True |
| checkStrings | Bool | False |



## <a name="next-steps"></a>다음 단계
* Azure 리소스 관리자 템플릿의 hello 섹션에 대 한 참조 [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.
* toomerge 템플릿이 여러 개 참조 [Azure 리소스 관리자와 연결 된 템플릿을 사용 하 여](resource-group-linked-templates.md)합니다.
* 지정 된 횟수 만큼 tooiterate 리소스의 종류를 만들 때 참조 [Azure 리소스 관리자 리소스의 여러 인스턴스를 만들](resource-group-create-multiple.md)합니다.
* toosee toodeploy hello 서식 파일을 만든 참조 [Azure 리소스 관리자 템플릿 사용 하 여 응용 프로그램 배포](resource-group-template-deploy.md)합니다.

