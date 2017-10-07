---
title: "리소스 관리자 템플릿 aaaAzure 함수-배열 및 개체가 | Microsoft Docs"
description: "Hello 함수 toouse 배열 및 개체 사용에 대 한 Azure 리소스 관리자 템플릿에 설명 합니다."
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
ms.date: 06/12/2017
ms.author: tomfitz
ms.openlocfilehash: e5f1a9b2a71039562eae7e48c2474a1fa59a7bea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a>Azure Resource Manager 템플릿에 대한 배열 및 개체 함수 

Resource Manager는 배열 및 개체 작업을 위한 여러 함수를 제공합니다.

* [array](#array)
* [coalesce](#coalesce)
* [concat](#concat)
* [contains](#contains)
* [createArray](#createarray)
* [empty](#empty)
* [first](#first)
* [intersection](#intersection)
* [json](#json)
* [last](#last)
* [length](#length)
* [min](#min)
* [max](#max)
* [range](#range)
* [skip](#skip)
* [take](#take)
* [union](#union)

tooget 값으로 구분 된 문자열 값의 배열을 참조 [분할](resource-group-template-functions-string.md#split)합니다.

<a id="array" />

## <a name="array"></a>array
`array(convertToArray)`

Hello, tooan 배열 값으로 변환합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| convertToArray |예 |int, 문자열, 배열 또는 개체 |hello tooconvert tooan 배열 값입니다. |

### <a name="return-value"></a>반환 값

배열입니다.

### <a name="example"></a>예제

hello 다음 예제에서는 어떻게 toouse hello 여러 형식으로 배열 함수

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "intToConvert": {
            "type": "int",
            "defaultValue": 1
        },
        "stringToConvert": {
            "type": "string",
            "defaultValue": "a"
        },
        "objectToConvert": {
            "type": "object",
            "defaultValue": {"a": "b", "c": "d"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "intOutput": {
            "type": "array",
            "value": "[array(parameters('intToConvert'))]"
        },
        "stringOutput": {
            "type": "array",
            "value": "[array(parameters('stringToConvert'))]"
        },
        "objectOutput": {
            "type": "array",
            "value": "[array(parameters('objectToConvert'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| intOutput | 배열 | [1] |
| stringOutput | 배열 | ["a"] |
| objectOutput | 배열 | [{"a": "b", "c": "d"}] |

<a id="coalesce" />

## <a name="coalesce"></a>coalesce
`coalesce(arg1, arg2, arg3, ...)`

Hello 매개 변수에서 첫 번째 null이 아닌 값을 반환합니다. 빈 문자열, 빈 배열 및 빈 개체는 null이 아닙니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |int, 문자열, 배열 또는 개체 |null에 대 한 첫 번째 값 tootest을 hello 합니다. |
| 추가 인수 |아니요 |int, 문자열, 배열 또는 개체 |Null에 대 한 추가 값 tootest 합니다. |

### <a name="return-value"></a>반환 값

hello hello 첫 번째 null이 아닌 매개 변수 값, 문자열, int, 배열 또는 개체 일 수 있습니다. 모든 매개 변수가 null이면 null입니다. 

### <a name="example"></a>예제

hello 다음 예제에서는 hello 출력을에서 보여 줍니다 coalesce의 서로 다른 사용 합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {
                "null1": null, 
                "null2": null,
                "string": "default",
                "int": 1,
                "object": {"first": "default"},
                "array": [1]
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').string)]"
        },
        "intOutput": {
            "type": "int",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').int)]"
        },
        "objectOutput": {
            "type": "object",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').object)]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').array)]"
        },
        "emptyOutput": {
            "type": "bool",
            "value": "[empty(coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| stringOutput | 문자열 | 기본값 |
| intOutput | int | 1 |
| objectOutput | Object | {"first": "default"} |
| arrayOutput | 배열 | [1] |
| emptyOutput | Bool | True |

<a id="concat" />

## <a name="concat"></a>concat
`concat(arg1, arg2, arg3, ...)`

여러 배열 및 연결 하는 hello 배열을 반환을 결합 또는 여러 개의 문자열 값을 결합 하 고 hello 연결 문자열을 반환 합니다. 

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |배열 또는 문자열 |첫 번째 배열 또는 문자열 연결에 대 한 hello 합니다. |
| 추가 인수 |아니요 |배열 또는 문자열 |연결 순서로 나타낸 추가 배열 또는 문자열입니다. |

이 함수는 변수 인수 수에 제한이 하며 문자열 또는 배열 hello 매개 변수에 대해 사용할 수 있습니다.

### <a name="return-value"></a>반환 값
연결된 값의 문자열 또는 배열입니다.

### <a name="example"></a>예제

다음 예제는 hello toocombine 두 배열 하는 방법을 보여 줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "firstArray": { 
            "type": "array", 
            "defaultValue": [ 
                "1-1", 
                "1-2", 
                "1-3" 
            ] 
        },
        "secondArray": {
            "type": "array", 
            "defaultValue": [ 
                "2-1", 
                "2-2",
                "2-3" 
            ] 
        }
    },
    "resources": [
    ],
    "outputs": {
        "return": {
            "type": "array",
            "value": "[concat(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| return | 배열 | ["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"] |

다음 예제는 hello toocombine 두 문자열 값 하 고 연결 된 문자열을 반환 하는 방법을 보여 줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "prefix": {
            "type": "string",
            "defaultValue": "prefix"
        }
    },
    "resources": [],
    "outputs": {
        "concatOutput": {
            "value": "[concat(parameters('prefix'), '-', uniqueString(resourceGroup().id))]",
            "type" : "string"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| concatOutput | 문자열 | prefix-5yj4yjf5mbg72 |

<a id="contains" />

## <a name="contains"></a>contains
`contains(container, itemToFind)`

배열에 값이 포함되는지, 개체에 키가 포함되는지 또는 문자열에 하위 문자열이 포함되는지를 확인합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| container |예 |배열, 개체 또는 문자열 |hello 값 toofind를 포함 하는 hello 값입니다. |
| itemToFind |예 |문자열 또는 int |hello 값 toofind 합니다. |

### <a name="return-value"></a>반환 값

**True 이면** hello 항목이 검색 되지 않으면 이면 **False**합니다.

### <a name="example"></a>예제

hello 다음 예제는 toouse 여러 형식으로 포함 하는 방법.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "OneTwoThree"
        },
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringTrue": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'e')]"
        },
        "stringFalse": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'z')]"
        },
        "objectTrue": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'one')]"
        },
        "objectFalse": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'a')]"
        },
        "arrayTrue": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'three')]"
        },
        "arrayFalse": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'four')]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| stringTrue | Bool | True |
| stringFalse | Bool | False |
| objectTrue | Bool | True |
| objectFalse | Bool | False |
| arrayTrue | Bool | True |
| arrayFalse | Bool | False |

<a id="createarray" />

## <a name="createarray"></a>createarray
`createArray (arg1, arg2, arg3, ...)`

Hello 매개 변수에서 배열을 만듭니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |문자열, 정수, 배열 또는 개체 |hello hello 배열의 첫 번째 값입니다. |
| 추가 인수 |아니요 |문자열, 정수, 배열 또는 개체 |Hello 배열에 추가 값입니다. |

### <a name="return-value"></a>반환 값

배열입니다.

### <a name="example"></a>예제

hello 방법을 예제와 다음 여러 형식으로 toouse createArray:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringArray": {
            "type": "array",
            "value": "[createArray('a', 'b', 'c')]"
        },
        "intArray": {
            "type": "array",
            "value": "[createArray(1, 2, 3)]"
        },
        "objectArray": {
            "type": "array",
            "value": "[createArray(parameters('objectToTest'))]"
        },
        "arrayArray": {
            "type": "array",
            "value": "[createArray(parameters('arrayToTest'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| stringArray | 배열 | ["a", "b", "c"] |
| intArray | 배열 | [1, 2, 3] |
| objectArray | 배열 | [{"one": "a", "two": "b", "three": "c"}] |
| arrayArray | 배열 | [["one", "two", "three"]] |

<a id="empty" />

## <a name="empty"></a>empty

`empty(itemToTest)`

배열, 개체 또는 문자열이 비어 있는지를 확인합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| itemToTest |예 |배열, 개체 또는 문자열 |비어 있는 경우 값 toocheck을 hello 합니다. |

### <a name="return-value"></a>반환 값

반환 **True** hello 값, 비어 있지 않으면이 **False**합니다.

### <a name="example"></a>예제

다음 예제는 hello는 배열, 개체 및 문자열 비어 있는지 여부를 확인 합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": []
        },
        "testObject": {
            "type": "object",
            "defaultValue": {}
        },
        "testString": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testArray'))]"
        },
        "objectEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testObject'))]"
        },
        "stringEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testString'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| arrayEmpty | Bool | True |
| objectEmpty | Bool | True |
| stringEmpty | Bool | True |

<a id="first" />

## <a name="first"></a>first
`first(arg1)`

반환은 hello 배열의 첫 번째 요소 또는 hello 문자열의 첫 번째 문자 hello 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |배열 또는 문자열 |문자 또는 hello 값 tooretrieve hello 첫 번째 요소입니다. |

### <a name="return-value"></a>반환 값

hello 형식 (string, int, 배열 또는 개체)의 배열 또는 문자열의 첫 번째 문자 hello hello 첫 번째 요소입니다.

### <a name="example"></a>예제

hello 다음 예제에서는 어떻게 toouse hello 배열 및 문자열을 사용 하는 첫 번째 함수

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[first(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[first('One Two Three')]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| arrayOutput | 문자열 | one |
| stringOutput | 문자열 | O |

<a id="intersection" />

## <a name="intersection"></a>교집합
`intersection(arg1, arg2, arg3, ...)`

Hello 매개 변수에서 단일 배열 또는 개체 hello 공통 요소를 반환합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |배열 또는 개체 |공통 요소를 찾기 위한 첫 번째 값 toouse를 hello 합니다. |
| arg2 |예 |배열 또는 개체 |공통 요소를 찾기 위한 두 번째 값 toouse를 hello 합니다. |
| 추가 인수 |아니요 |배열 또는 개체 |공통 요소를 찾기 위한 toouse 추가 값입니다. |

### <a name="return-value"></a>반환 값

배열 또는 hello 공통 요소를 가진 개체입니다.

### <a name="example"></a>예제

다음 예제는 hello toouse 교집합 배열 하는 방법을 보여 줍니다. 및 개체:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "z", "three": "c"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[intersection(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[intersection(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| objectOutput | Object | {"one": "a", "three": "c"} |
| arrayOutput | 배열 | ["two", "three"] |


## <a name="json"></a>json :
`json(arg1)`

JSON 개체를 반환합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |string |hello 값 tooconvert tooJSON 합니다. |


### <a name="return-value"></a>반환 값

문자열 또는 빈 개체 hello JSON 개체 hello에서 지정 된 경우 **null** 지정 됩니다.

### <a name="example"></a>예제

다음 예제는 hello toouse 교집합 배열 하는 방법을 보여 줍니다. 및 개체:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "jsonOutput": {
            "type": "object",
            "value": "[json('{\"a\": \"b\"}')]"
        },
        "nullOutput": {
            "type": "bool",
            "value": "[empty(json('null'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| jsonOutput | Object | {"a": "b"} |
| nullOutput | Boolean | True |

<a id="last" />

## <a name="last"></a>last
`last (arg1)`

반환은 hello 배열의 마지막 요소 또는 hello 문자열의 마지막 문자 hello 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |배열 또는 문자열 |문자 또는 hello 값 tooretrieve hello 마지막 요소입니다. |

### <a name="return-value"></a>반환 값

hello 형식 (string, int, 배열 또는 개체)에 배열 또는 문자열의 마지막 문자 hello hello 마지막 요소의입니다.

### <a name="example"></a>예제

hello 다음 예제에서는 어떻게 toouse hello 수 있는 배열 및 문자열 last 함수

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[last(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[last('One Two Three')]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| arrayOutput | 문자열 | three |
| stringOutput | 문자열 | e |

<a id="length" />

## <a name="length"></a>length
`length(arg1)`

배열 또는 문자열의 문자에 hello 수의 요소를 반환 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |배열 또는 문자열 |hello 수의 요소를 가져오기 위한 배열 toouse hello 또는 hello 개수의 문자를 가져오기 위한 문자열 toouse hello 합니다. |

### <a name="return-value"></a>반환 값

int입니다. 

### <a name="example"></a>예제

hello 방법을 예제와 다음 toouse 배열 및 문자열 길이:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "stringToTest": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "arrayLength": {
            "type": "int",
            "value": "[length(parameters('arrayToTest'))]"
        },
        "stringLength": {
            "type": "int",
            "value": "[length(parameters('stringToTest'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| arrayLength | int | 3 |
| stringLength | int | 13 |

리소스를 만들 때 배열 toospecify hello 수의 반복으로이 함수를 사용할 수 있습니다. 다음 예제는 hello에서 매개 변수를 hello **siteNames** hello 웹 사이트를 만들 때 이름 toouse tooan 배열을 참조 합니다.

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

배열과 함께 이 함수를 사용하는 방법의 예제는 [Azure Resource Manager에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요.

<a id="min" />

## <a name="min"></a>Min
`min(arg1)`

반환 hello 정수 배열 또는 정수 쉼표로 구분 된 목록에서 최소 값입니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |정수 배열 또는 쉼표로 구분된 정수 목록 |hello 컬렉션 tooget hello 최소값입니다. |

### <a name="return-value"></a>반환 값

Hello에 대 한 최소값 정보를 나타내는 int입니다.

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
`max(arg1)`

반환 hello 정수 배열 또는 정수 쉼표로 구분 된 목록에서 최대 값입니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |정수 배열 또는 쉼표로 구분된 정수 목록 |hello 컬렉션 tooget hello 최대값입니다. |

### <a name="return-value"></a>반환 값

Hello 최 댓 값을 나타내는 int입니다.

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

<a id="range" />

## <a name="range"></a>range
`range(startingInteger, numberOfElements)`

시작 정수 및 항목의 수를 포함하는 정수 배열을 만듭니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| startingInteger |예 |int |hello hello 배열의 첫 번째 정수입니다. |
| numberofElements |예 |int |hello 수 hello 배열에 있는 정수입니다. |

### <a name="return-value"></a>반환 값

정수 배열입니다.

### <a name="example"></a>예제

다음 예제는 hello toouse 범위 함수 hello 하는 방법을 보여 줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "startingInt": {
            "type": "int",
            "defaultValue": 5
        },
        "numberOfElements": {
            "type": "int",
            "defaultValue": 3
        }
    },
    "resources": [],
    "outputs": {
        "rangeOutput": {
            "type": "array",
            "value": "[range(parameters('startingInt'),parameters('numberOfElements'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| rangeOutput | 배열 | [5, 6, 7] |

<a id="skip" />

## <a name="skip"></a>skip
`skip(originalValue, numberToSkip)`

Hello hello 배열에 지정 된 번호 또는 hello hello 문자열에 숫자를 지정 된 후 모든 hello 문자로 이루어진 문자열을 반환 하는 후 모든 hello 요소가 있는 배열을 반환 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| originalValue |예 |배열 또는 문자열 |건너뛰기 위한 hello 배열 또는 문자열 toouse 합니다. |
| numberToSkip |예 |int |요소 또는 문자 tooskip hello 수입니다. 이 값이 0, 모든 요소를 hello 또는 hello 값의 문자 반환 됩니다. Hello 배열 또는 문자열의 hello 길이 보다 큰 경우 빈 배열 또는 문자열 반환 됩니다. |

### <a name="return-value"></a>반환 값

배열 또는 문자열입니다.

### <a name="example"></a>예제

다음 예에서는 건너뜁니다 hello hello hello 배열에서 요소 수를 지정 된 한 hello 문자열에 문자 수를 지정 합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToSkip": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToSkip": {
            "type": "int",
            "defaultValue": 4
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[skip(parameters('testArray'),parameters('elementsToSkip'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[skip(parameters('testString'),parameters('charactersToSkip'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| arrayOutput | 배열 | ["three"] |
| stringOutput | 문자열 | two three |

<a id="take" />

## <a name="take"></a>take
`take(originalValue, numberToTake)`

Hello로 배열에서 요소 수를 지정 된 반환 hello hello 배열의 시작 또는 hello로 문자열 hello hello 문자열 시작에서 문자 수를 지정 하십시오.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| originalValue |예 |배열 또는 문자열 |배열 또는 문자열 tootake hello 요소를 hello 합니다. |
| numberToTake |예 |int |요소 또는 문자 tootake hello 수입니다. 이 값이 0 이하이면 빈 배열 또는 문자열이 반환됩니다. 지정 된 배열 또는 문자열 hello의 hello 길이 보다 큰 경우 hello 배열 또는 문자열의 모든 hello 요소가 반환 됩니다. |

### <a name="return-value"></a>반환 값

배열 또는 문자열입니다.

### <a name="example"></a>예제

다음 예제는 hello hello hello 배열에서 요소 및 문자열에서 문자 수를 지정 합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToTake": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToTake": {
            "type": "int",
            "defaultValue": 2
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[take(parameters('testArray'),parameters('elementsToTake'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[take(parameters('testString'),parameters('charactersToTake'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| arrayOutput | 배열 | ["one", "two"] |
| stringOutput | 문자열 | on |

<a id="union" />

## <a name="union"></a>union
`union(arg1, arg2, arg3, ...)`

Hello 매개 변수에서 단일 배열 또는 모든 요소 개체를 반환합니다. 중복된 값 또는 키는 한 번만 포함됩니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |배열 또는 개체 |hello 첫 번째 값 toouse 요소를 연결 합니다. |
| arg2 |예 |배열 또는 개체 |요소에 추가 하기 위해 두 번째 값 toouse를 hello 합니다. |
| 추가 인수 |아니요 |배열 또는 개체 |요소에 추가 하기 위해 추가 값 toouse 합니다. |

### <a name="return-value"></a>반환 값

배열 또는 개체입니다.

### <a name="example"></a>예제

다음 예제는 hello toouse 공용 구조체 배열 하는 방법을 보여 줍니다. 및 개체:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"three": "c", "four": "d", "five": "e"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["three", "four"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[union(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[union(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| objectOutput | Object | {"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"} |
| arrayOutput | 배열 | ["one", "two", "three", "four"] |

## <a name="next-steps"></a>다음 단계
* Azure 리소스 관리자 템플릿의 hello 섹션에 대 한 참조 [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.
* toomerge 템플릿이 여러 개 참조 [Azure 리소스 관리자와 연결 된 템플릿을 사용 하 여](resource-group-linked-templates.md)합니다.
* 지정 된 횟수 만큼 tooiterate 리소스의 종류를 만들 때 참조 [Azure 리소스 관리자 리소스의 여러 인스턴스를 만들](resource-group-create-multiple.md)합니다.
* toosee toodeploy hello 서식 파일을 만든 참조 [Azure 리소스 관리자 템플릿 사용 하 여 응용 프로그램 배포](resource-group-template-deploy.md)합니다.

