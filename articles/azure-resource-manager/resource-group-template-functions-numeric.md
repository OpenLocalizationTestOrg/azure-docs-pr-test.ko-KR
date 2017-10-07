---
title: "aaaAzure 리소스 관리자 템플릿 함수-숫자 | Microsoft Docs"
description: "번호가 있는 hello 함수 toouse Azure 리소스 관리자 템플릿 toowork에 설명합니다."
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
ms.date: 06/13/2017
ms.author: tomfitz
ms.openlocfilehash: 855d5b354d094b9815edc160e3d72efbfd36ba77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="numeric-functions-for-azure-resource-manager-templates"></a>Azure Resource Manager 템플릿용 숫자 함수

리소스 관리자 hello를 뒤 정수가 포함 된 작업에 대 한 함수를 제공 합니다.

* [추가](#add)
* [copyIndex](#copyindex)
* [div](#div)
* [float](#float)
* [int](#int)
* [min](#min)
* [max](#max)
* [mod](#mod)
* [mul](#mul)
* [sub](#sub)

<a id="add" />

## <a name="add"></a>추가
`add(operand1, operand2)`

반환 hello hello 두 제공 된 정수의 합입니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- | 
|operand1 |예 |int |첫 번째 숫자 tooadd 합니다. |
|operand2 |예 |int |두 번째 숫자 tooadd 합니다. |

### <a name="return-value"></a>반환 값

Hello 매개 변수의 hello 합계를 포함 하는 정수입니다.

### <a name="example"></a>예제

다음 예제는 hello 두 개의 매개 변수를 추가 합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer tooadd"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer tooadd"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "addResult": {
            "type": "int",
            "value": "[add(parameters('first'), parameters('second'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| addResult | int | 8 |

<a id="copyindex" />

## <a name="copyindex"></a>copyIndex
`copyIndex(loopName, offset)`

반환 hello 반복 루프의 인덱스입니다. 

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| loopName | 아니요 | string | hello 반복을 가져오기 위한 hello 루프의 hello 이름입니다. |
| offset |아니요 |int |hello 숫자 tooadd toohello 0부터 시작 하는 반복 값입니다. |

### <a name="remarks"></a>설명

이 함수는 항상 **copy** 개체에 사용됩니다. 에 값이 제공 하는 경우 **오프셋**, hello 현재 반복 값이 반환 됩니다. hello 반복 값이 0에서 시작 합니다.

hello **loopName** 속성 하면 toospecify copyIndex 참조 tooa 리소스 반복 또는 속성 반복 여부. 에 값이 제공 하는 경우 **loopName**, hello 현재 리소스 형식을 반복 사용 됩니다. 속성에서 반복하는 경우 **loopName**의 값을 제공합니다. 
 
**copyIndex**를 사용하는 방법의 설명은 [Azure Resource Manager에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요.

### <a name="example"></a>예제

hello 다음 예제에서는 hello 이름에 포함 된 복사 루프 및 hello 인덱스 값 

```json
"resources": [ 
  { 
    "name": "[concat('examplecopy-', copyIndex())]", 
    "type": "Microsoft.Web/sites", 
    "copy": { 
      "name": "websitescopy", 
      "count": "[parameters('count')]" 
    }, 
    ...
  }
]
```

### <a name="return-value"></a>반환 값

Hello 반복의 hello 현재 인덱스를 나타내는 정수입니다.

<a id="div" />

## <a name="div"></a>div
`div(operand1, operand2)`

반환 hello hello 두 제공 된 정수의 정수 나누기입니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| operand1 |예 |int |나누어 사용 하는 hello 수입니다. |
| operand2 |예 |int |hello 숫자 사용된 toodivide입니다. 0일 수 없습니다. |

### <a name="return-value"></a>반환 값

정수 나타내는 hello 나누기입니다.

### <a name="example"></a>예제

다음 예제는 hello 다른 매개 변수에서 매개 변수 하나를 나눕니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 8,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used toodivide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "divResult": {
            "type": "int",
            "value": "[div(parameters('first'), parameters('second'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| divResult | int | 2 |

<a id="float" />

## <a name="float"></a>float
`float(arg1)`

Hello 값 tooa 부동 소수점 숫자로 변환 합니다. 논리 앱 같은 tooan 응용 프로그램을 사용자 지정 매개 변수를 전달할 때만이 함수를 사용 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |문자열 또는 int |hello 값 tooconvert tooa 부동 소수점 수입니다. |

### <a name="return-value"></a>반환 값
부동 소수점 수입니다.

### <a name="example"></a>예제

다음 예제는 hello toouse toopass 매개 변수 tooa 논리 앱을 배치 하는 방법을 보여 줍니다.

```json
{
    "type": "Microsoft.Logic/workflows",
    "properties": {
        ...
        "parameters": {
        "custom1": {
            "value": "[float('3.0')]"
        },
        "custom2": {
            "value": "[float(3)]"
        },
```

<a id="int" />

## <a name="int"></a>int
`int(valueToConvert)`

지정 된 값 tooan 정수 hello 변환합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| valueToConvert |예 |문자열 또는 int |hello tooconvert tooan 정수 값입니다. |

### <a name="return-value"></a>반환 값

Hello의 정수 값을 변환 합니다.

### <a name="example"></a>예제

hello 다음 예제에서는 변환 hello 사용자가 제공한 매개 변수 값 toointeger 합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToConvert": { 
            "type": "string",
            "defaultValue": "4"
        }
    },
    "resources": [
    ],
    "outputs": {
        "intResult": {
            "type": "int",
            "value": "[int(parameters('stringToConvert'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| intResult | int | 4 |


<a id="min" />

## <a name="min"></a>Min
`min (arg1)`

반환 hello 정수 배열 또는 정수 쉼표로 구분 된 목록에서 최소 값입니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |정수 배열 또는 쉼표로 구분된 정수 목록 |hello 컬렉션 tooget hello 최소값입니다. |

### <a name="return-value"></a>반환 값

Hello 컬렉션에서 최소 값을 나타내는 정수입니다.

### <a name="example"></a>예제

hello 방법을 예제와 다음 toouse min 배열 및 정수 목록:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[min(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[min(0,3,2,5,4)]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| arrayOutput | int | 0 |
| intOutput | int | 0 |

<a id="max" />

## <a name="max"></a>max
`max (arg1)`

반환 hello 정수 배열 또는 정수 쉼표로 구분 된 목록에서 최대 값입니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |정수 배열 또는 쉼표로 구분된 정수 목록 |hello 컬렉션 tooget hello 최대값입니다. |

### <a name="return-value"></a>반환 값

Hello 컬렉션에서 hello 최 댓 값을 나타내는 정수입니다.

### <a name="example"></a>예제

hello 방법을 예제와 다음 toouse 배열 및 정수 목록이 사용 하 여 최대:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[max(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[max(0,3,2,5,4)]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| arrayOutput | int | 5 |
| intOutput | int | 5 |

<a id="mod" />

## <a name="mod"></a>mod
`mod(operand1, operand2)`

제공 된 정수 두 개 hello를 사용 하 여 hello 정수 나누기의 hello 나머지를 반환 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| operand1 |예 |int |나누어 사용 하는 hello 수입니다. |
| operand2 |예 |int |hello를 사용 하는 toodivide 0 일 수 없습니다. |

### <a name="return-value"></a>반환 값
정수 나타내는 hello 나머지입니다.

### <a name="example"></a>예제

hello 다음 예제에서는 반환 hello 나눈 나머지를 다른 매개 변수는 하나의 매개 변수입니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used toodivide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "modResult": {
            "type": "int",
            "value": "[mod(parameters('first'), parameters('second'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| modResult | int | 1 |

<a id="mul" />

## <a name="mul"></a>mul
`mul(operand1, operand2)`

반환 hello hello 두 제공 된 정수의 곱입니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| operand1 |예 |int |첫 번째 숫자 toomultiply 합니다. |
| operand2 |예 |int |두 번째 숫자 toomultiply 합니다. |

### <a name="return-value"></a>반환 값

정수 나타내는 hello 곱하기.

### <a name="example"></a>예제

다음 예제는 hello 다른 매개 변수에서 매개 변수 하나를 곱합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer toomultiply"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer toomultiply"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "mulResult": {
            "type": "int",
            "value": "[mul(parameters('first'), parameters('second'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| mulResult | int | 15 |

<a id="sub" />

## <a name="sub"></a>sub
`sub(operand1, operand2)`

반환 hello 빼기 hello 두 개의 제공 된 정수입니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| operand1 |예 |int |hello 숫자에서 뺀입니다. |
| operand2 |예 |int |hello 숫자를 뺀입니다. |

### <a name="return-value"></a>반환 값
정수 나타내는 hello 빼기 합니다.

### <a name="example"></a>예제

다음 예제는 hello 다른 매개 변수에서 매개 변수를 하나를 뺍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer subtracted from"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer toosubtract"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "subResult": {
            "type": "int",
            "value": "[sub(parameters('first'), parameters('second'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| subResult | int | 4 |

## <a name="next-steps"></a>다음 단계
* Azure 리소스 관리자 템플릿의 hello 섹션에 대 한 참조 [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.
* toomerge 템플릿이 여러 개 참조 [Azure 리소스 관리자와 연결 된 템플릿을 사용 하 여](resource-group-linked-templates.md)합니다.
* 지정 된 횟수 만큼 tooiterate 리소스의 종류를 만들 때 참조 [Azure 리소스 관리자 리소스의 여러 인스턴스를 만들](resource-group-create-multiple.md)합니다.
* toosee toodeploy hello 서식 파일을 만든 참조 [Azure 리소스 관리자 템플릿 사용 하 여 응용 프로그램 배포](resource-group-template-deploy.md)합니다.

