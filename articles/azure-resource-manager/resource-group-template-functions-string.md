---
title: "리소스 관리자 템플릿 함수 aaaAzure-문자열 | Microsoft Docs"
description: "Hello 함수 toouse 문자열이 포함 된 Azure 리소스 관리자 템플릿 toowork 프로그램에 대해 설명합니다."
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
ms.openlocfilehash: 27f7f6a52cbe4e9915718184433e92ca92999346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="string-functions-for-azure-resource-manager-templates"></a>Azure Resource Manager 템플릿용 문자열 함수

리소스 관리자는 다음 문자열 작업에 대 한 함수 hello를 제공 합니다.

* [base64](#base64)
* [base64ToJson](#base64tojson)
* [base64ToString](#base64tostring)
* [concat](#concat)
* [contains](#contains)
* [dataUri](#datauri)
* [dataUriToString](#datauritostring)
* [empty](#empty)
* [endsWith](#endswith)
* [first](#first)
* [indexOf](#indexof)
* [last](#last)
* [lastIndexOf](#lastindexof)
* [length](#length)
* [padLeft](#padleft)
* [replace](#replace)
* [skip](#skip)
* [분할](#split)
* [startsWith](resource-group-template-functions-string.md#startswith)
* [string](#string)
* [substring](#substring)
* [take](#take)
* [toLower](#tolower)
* [toUpper](#toupper)
* [trim](#trim)
* [uniqueString](#uniquestring)
* [uri](#uri)
* [uriComponent](resource-group-template-functions-string.md#uricomponent)
* [uriComponentToString](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a>base64
`base64(inputString)`

반환 hello hello 입력된 문자열의 base64 표현입니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| inputString |예 |string |base64 표현으로 hello 값 tooreturn 합니다. |

### <a name="return-value"></a>반환 값

Hello base64 표현을 포함 하는 문자열입니다.

### <a name="examples"></a>예

다음 예제는 hello toouse base64 함수 hello 하는 방법을 보여 줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| base64Output | 문자열 | b25lLCB0d28sIHRocmVl |
| toStringOutput | 문자열 | one, two, three |
| toJsonOutput | Object | {“one”: “a”, “two”: “b”} |

<a id="base64tojson" />

## <a name="base64tojson"></a>base64ToJson
`base64tojson`

Base64 표현을 tooa JSON 개체로 변환합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| base64Value |예 |string |hello base64 표현 tooconvert tooa JSON 개체입니다. |

### <a name="return-value"></a>반환 값

JSON 개체입니다.

### <a name="examples"></a>예

hello 다음 예제에서는 hello base64ToJson 함수 tooconvert base64 값:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| base64Output | 문자열 | b25lLCB0d28sIHRocmVl |
| toStringOutput | 문자열 | one, two, three |
| toJsonOutput | Object | {“one”: “a”, “two”: “b”} |

<a id="base64tostring" />

## <a name="base64tostring"></a>base64ToString
`base64ToString(base64Value)`

Base64 표현을 tooa 문자열로 변환합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| base64Value |예 |string |hello base64 표현 tooconvert tooa 문자열입니다. |

### <a name="return-value"></a>반환 값

Base64 값을 변환 하는 hello의 문자열입니다.

### <a name="examples"></a>예

hello 다음 예제에서는 hello base64ToString 함수 tooconvert base64 값:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| base64Output | 문자열 | b25lLCB0d28sIHRocmVl |
| toStringOutput | 문자열 | one, two, three |
| toJsonOutput | Object | {“one”: “a”, “two”: “b”} |



<a id="concat" />

## <a name="concat"></a>concat
`concat (arg1, arg2, arg3, ...)`

여러 개의 문자열 값을 결합 하 고 hello 연결 문자열을 반환 하 또는 여러 배열을 결합 하 고 연결 하는 hello 배열을 반환 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |문자열 또는 배열 |hello 연결에 대 한 첫 번째 값입니다. |
| 추가 인수 |아니요 |string |연결할 추가 값(순서대로)입니다. |

### <a name="return-value"></a>반환 값
연결된 값의 문자열 또는 배열입니다.

### <a name="examples"></a>예

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

<a id="contains" />

## <a name="contains"></a>contains
`contains (container, itemToFind)`

배열에 값이 포함되는지, 개체에 키가 포함되는지 또는 문자열에 하위 문자열이 포함되는지를 확인합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| container |예 |배열, 개체 또는 문자열 |hello 값 toofind를 포함 하는 hello 값입니다. |
| itemToFind |예 |문자열 또는 int |hello 값 toofind 합니다. |

### <a name="return-value"></a>반환 값

**True 이면** hello 항목이 검색 되지 않으면 이면 **False**합니다.

### <a name="examples"></a>예

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

<a id="datauri" />

## <a name="datauri"></a>dataUri
`dataUri(stringToConvert)`

값 tooa 데이터 URI를 변환합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| stringToConvert |예 |string |hello 값 tooconvert tooa 데이터 URI입니다. |

### <a name="return-value"></a>반환 값

데이터 URI로 형식이 지정된 문자열입니다.

### <a name="examples"></a>예

다음 예제는 hello 값 tooa 데이터 URI를 변환 하는 데이터 URI tooa 문자열:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| dataUriOutput | 문자열 | data:text/plain;charset=utf8;base64,SGVsbG8= |
| toStringOutput | 문자열 | Hello, World! |

<a id="datauritostring" />

## <a name="datauritostring"></a>dataUriToString
`dataUriToString(dataUriToConvert)`

데이터 URI는 형식의 값 tooa 문자열입니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| dataUriToConvert |예 |string |hello 데이터 URI 값 tooconvert입니다. |

### <a name="return-value"></a>반환 값

Hello를 포함 하는 문자열 값을 변환 합니다.

### <a name="examples"></a>예

다음 예제는 hello 값 tooa 데이터 URI를 변환 하는 데이터 URI tooa 문자열:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| dataUriOutput | 문자열 | data:text/plain;charset=utf8;base64,SGVsbG8= |
| toStringOutput | 문자열 | Hello, World! |

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

### <a name="examples"></a>예

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

<a id="endswith" />

## <a name="endswith"></a>endsWith
`endsWith(stringToSearch, stringToFind)`

문자열이 값으로 끝나는지 여부를 결정합니다. hello 비교는 대/소문자 구분 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| stringToSearch |예 |string |hello 항목 toofind를 포함 하는 hello 값입니다. |
| stringToFind |예 |string |hello 값 toofind 합니다. |

### <a name="return-value"></a>반환 값

**True** hello 기본 동작은 일치 하는 hello 마지막 문자 또는 문자 hello 문자열의 경우 이렇게 하지 않으면 **False**합니다.

### <a name="examples"></a>예

다음 예제는 hello toouse startsWith 및 endsWith 함수 hello 하는 방법을 보여 줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| startsTrue | Bool | True |
| startsCapTrue | Bool | True |
| startsFalse | Bool | False |
| endsTrue | Bool | True |
| endsCapTrue | Bool | True |
| endsFalse | Bool | False |

<a id="first" />

## <a name="first"></a>first
`first(arg1)`

반환은 hello 문자열의 첫 번째 문자 또는 hello 배열의 첫 번째 요소 hello 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |배열 또는 문자열 |문자 또는 hello 값 tooretrieve hello 첫 번째 요소입니다. |

### <a name="return-value"></a>반환 값

Hello 첫 번째 문자 또는 배열에 hello 첫 번째 요소의 hello 형식 (string, int, 배열 또는 개체)는 문자열입니다.

### <a name="examples"></a>예

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

<a id="indexof" />

## <a name="indexof"></a>indexof
`indexOf(stringToSearch, stringToFind)`

반환 hello 문자열 내 값의 첫 번째 위치입니다. hello 비교는 대/소문자 구분 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| stringToSearch |예 |string |hello 항목 toofind를 포함 하는 hello 값입니다. |
| stringToFind |예 |string |hello 값 toofind 합니다. |

### <a name="return-value"></a>반환 값

Hello 항목 toofind의 hello 위치를 나타내는 정수입니다. hello 값은 0부터 시작 합니다. Hello 항목이 발견 되지 않으면-1이 반환 됩니다.

### <a name="examples"></a>예

다음 예제는 hello toouse indexOf 및 lastIndexOf 함수 hello 하는 방법을 보여 줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| firstT | int | 0 |
| lastT | int | 3 |
| firstString | int | 2 |
| lastString | int | 0 |
| notFound | int | -1 |

<a id="last" />

## <a name="last"></a>last
`last (arg1)`

마지막 hello 문자열의 문자 또는 hello hello 배열의 마지막 요소를 반환 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |배열 또는 문자열 |문자 또는 hello 값 tooretrieve hello 마지막 요소입니다. |

### <a name="return-value"></a>반환 값

문자열 hello 마지막 문자 또는 hello 유형의 (string, int, 배열 또는 개체) hello 배열에서 마지막 요소입니다.

### <a name="examples"></a>예

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

<a id="lastindexof" />

## <a name="lastindexof"></a>lastindexof
`lastIndexOf(stringToSearch, stringToFind)`

반환 된 문자열 내에서 값의 마지막 위치를 hello 합니다. hello 비교는 대/소문자 구분 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| stringToSearch |예 |string |hello 항목 toofind를 포함 하는 hello 값입니다. |
| stringToFind |예 |string |hello 값 toofind 합니다. |

### <a name="return-value"></a>반환 값

Hello hello 항목 toofind의 마지막 위치를 나타내는 정수입니다. hello 값은 0부터 시작 합니다. Hello 항목이 발견 되지 않으면-1이 반환 됩니다.

### <a name="examples"></a>예

다음 예제는 hello toouse indexOf 및 lastIndexOf 함수 hello 하는 방법을 보여 줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| firstT | int | 0 |
| lastT | int | 3 |
| firstString | int | 2 |
| lastString | int | 0 |
| notFound | int | -1 |

<a id="length" />

## <a name="length"></a>length
`length(string)`

문자열 또는 배열 요소에 hello 문자 수를 반환합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |배열 또는 문자열 |hello 수의 요소를 가져오기 위한 배열 toouse hello 또는 hello 개수의 문자를 가져오기 위한 문자열 toouse hello 합니다. |

### <a name="return-value"></a>반환 값

int입니다. 

### <a name="examples"></a>예

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

<a id="padleft" />

## <a name="padleft"></a>padLeft
`padLeft(valueToPad, totalLength, paddingCharacter)`

Hello 총 지정 된 길이 도달할 때까지 toohello 남은 문자를 추가 하 여 오른쪽 맞춤 문자열을 반환 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| valueToPad |예 |문자열 또는 int |값 tooright hello-정렬 합니다. |
| totalLength |예 |int |hello에 있는 문자의 총 수를 hello 문자열을 반환 했습니다. |
| paddingCharacter |아니요 |단일 문자 |hello 총 길이 도달할 때까지 왼쪽 여백에 대 한 hello 문자 toouse 합니다. hello 기본값은 공백입니다. |

Hello 원래 문자열 문자 toopad hello 개수 보다 긴 경우에 문자가 더 추가 됩니다.

### <a name="return-value"></a>반환 값

문자열을 지정 된 문자 수를 최소한 hello 합니다.

### <a name="examples"></a>예

다음 예제는 hello 방법을 toopad hello 사용자가 제공한 매개 변수 값 hello를 추가 하 여 0 문자 hello 총 문자 수에 도달할 때까지 보여 줍니다. 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123"
        }
    },
    "resources": [],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[padLeft(parameters('testString'),10,'0')]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| stringOutput | 문자열 | 0000000123 |

<a id="replace" />

## <a name="replace"></a>바꾸기
`replace(originalString, oldString, newString)`

다른 문자열로 대체한 어떤 문자열의 인스턴스를 포함한 새 문자열을 반환합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| originalString |예 |string |다른 문자열에 의해 대체 되는 한 문자열의 모든 인스턴스가 포함 된 hello 값입니다. |
| oldString |예 |string |hello 문자열 toobe hello 원래 문자열에서 제거 됩니다. |
| newString |예 |string |hello 문자열 tooadd hello 대신 문자열을 제거 합니다. |

### <a name="return-value"></a>반환 값

Hello로 문자열로 문자를 대체 합니다.

### <a name="examples"></a>예

다음 예제는 hello hello 사용자가 제공한 문자열에서 모든 tooremove 대시 하는 방법 및 다른 문자열로 문자열 hello의 tooreplace 일부로 되는 방법을 보여 줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123-123-1234"
        }
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'-', '')]"
        },
        "secodeOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'1234', 'xxxx')]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| firstOutput | 문자열 | 1231231234 |
| secodeOutput | 문자열 | 123-123-xxxx |

<a id="skip" />

## <a name="skip"></a>skip
`skip(originalValue, numberToSkip)`

Hello 지정한 수 만큼의 문자 또는 배열 hello 요소가 모두 hello 요소 수를 지정한 후 후 모든 hello 문자로 이루어진 문자열을 반환 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| originalValue |예 |배열 또는 문자열 |건너뛰기 위한 hello 배열 또는 문자열 toouse 합니다. |
| numberToSkip |예 |int |요소 또는 문자 tooskip hello 수입니다. 이 값이 0, 모든 요소를 hello 또는 hello 값의 문자 반환 됩니다. Hello 배열 또는 문자열의 hello 길이 보다 큰 경우 빈 배열 또는 문자열 반환 됩니다. |

### <a name="return-value"></a>반환 값

배열 또는 문자열입니다.

### <a name="examples"></a>예

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

<a id="split" />

## <a name="split"></a>분할
`split(inputString, delimiter)`

구분 기호를 지정 하는 hello 구분 되는 입력 문자열의 hello hello 하위 문자열이 포함 된 문자열의 배열을 반환 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| inputString |예 |string |hello 문자열 toosplit 합니다. |
| 구분 기호 |예 |문자열 또는 문자열 배열 |구분 기호 toouse hello 문자열을 분할 하는 데 hello 합니다. |

### <a name="return-value"></a>반환 값

문자열 배열입니다.

### <a name="examples"></a>예

hello 다음 예제에서는 분할 hello 입력된 문자열에 쉼표와 쉼표 또는 세미콜론입니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstString": {
            "type": "string",
            "defaultValue": "one,two,three"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "one;two,three"
        }
    },
    "variables": {
        "delimiters": [ ",", ";" ]
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "array",
            "value": "[split(parameters('firstString'),',')]"
        },
        "secondOutput": {
            "type": "array",
            "value": "[split(parameters('secondString'),variables('delimiters'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| firstOutput | 배열 | [“one”, “two”, “three”] |
| secondOutput | 배열 | [“one”, “two”, “three”] |

<a id="startswith" />

## <a name="startswith"></a>startswith
`startsWith(stringToSearch, stringToFind)`

문자열이 값으로 시작하는지 여부를 결정합니다. hello 비교는 대/소문자 구분 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| stringToSearch |예 |string |hello 항목 toofind를 포함 하는 hello 값입니다. |
| stringToFind |예 |string |hello 값 toofind 합니다. |

### <a name="return-value"></a>반환 값

**True** hello 기본 동작은 일치 하는 hello 첫 번째 문자 또는 문자 hello 문자열의 경우 이렇게 하지 않으면 **False**합니다.

### <a name="examples"></a>예

다음 예제는 hello toouse startsWith 및 endsWith 함수 hello 하는 방법을 보여 줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| startsTrue | Bool | True |
| startsCapTrue | Bool | True |
| startsFalse | Bool | False |
| endsTrue | Bool | True |
| endsCapTrue | Bool | True |
| endsFalse | Bool | False |

<a id="string" />

## <a name="string"></a>string
`string(valueToConvert)`

변환 hello tooa 문자열 값을 지정 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| valueToConvert |예 | 모두 |hello 값 tooconvert toostring 합니다. 개체 및 배열을 비롯하여 모든 값 형식을 변환할 수 있습니다. |

### <a name="return-value"></a>반환 값

Hello 변환 된 값의 문자열입니다.

### <a name="examples"></a>예

다음 예제는 hello tooconvert 다양 한 유형의 toostrings 값 하는 방법을 보여 줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testObject": {
            "type": "object",
            "defaultValue": {
                "valueA": 10,
                "valueB": "Example Text"
            }
        },
        "testArray": {
            "type": "array",
            "defaultValue": [
                "a",
                "b",
                "c"
            ]
        },
        "testInt": {
            "type": "int",
            "defaultValue": 5
        }
    },
    "resources": [],
    "outputs": {
        "objectOutput": {
            "type": "string",
            "value": "[string(parameters('testObject'))]"
        },
        "arrayOutput": {
            "type": "string",
            "value": "[string(parameters('testArray'))]"
        },
        "intOutput": {
            "type": "string",
            "value": "[string(parameters('testInt'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| objectOutput | 문자열 | {“valueA”:10,“valueB”:“Example Text”} |
| arrayOutput | 문자열 | [“a”,“b”,“c”] |
| intOutput | 문자열 | 5 |

<a id="substring" />

## <a name="substring"></a>substring
`substring(stringToParse, startIndex, length)`

지정한 문자 수를 지정 하는 hello에서 문자 위치 및 hello가 포함 되어 하위 문자열을 반환 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| stringToParse |예 |string |부분 문자열을 추출할는 hello에서 원래 문자열 hello입니다. |
| startIndex |아니요 |int |hello 부분 문자열에 대 한 0부터 시작할 문자 위치를 hello입니다. |
| length |아니요 |int |hello 부분 문자열에 대 한 문자 hello 수입니다. Hello 문자열 내의 tooa 위치를 참조 해야 합니다. |

### <a name="return-value"></a>반환 값

hello 부분 문자열입니다.

### <a name="remarks"></a>설명

hello 함수 hello 부분 문자열 hello 문자열 hello 끝을 넘어 확장 작업이 실패 합니다. 다음 예제는 hello 실패 hello 오류 "hello 인덱스 및 길이 매개 변수가 참조 해야 hello 문자열 내의 tooa 위치 합니다. hello 인덱스 매개 변수: '0' hello 길이 매개 변수: '11' hello hello 문자열 매개 변수의 길이: '10'. "입니다.

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a>예

다음 예제는 hello 매개 변수에서 하위 문자열을 추출 합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        }
    },
    "resources": [],
    "outputs": {
        "substringOutput": {
            "value": "[substring(parameters('testString'), 4, 3)]",
            "type": "string"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| substringOutput | 문자열 | two |


<a id="take" />

## <a name="take"></a>take
`take(originalValue, numberToTake)`

Hello로 문자열의 시작 부분 hello에서에서 문자 수가 지정 된 반환 문자열 hello 또는 hello로 배열에서 hello 시작 hello 배열의 요소 수를 지정 하십시오.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| originalValue |예 |배열 또는 문자열 |배열 또는 문자열 tootake hello 요소를 hello 합니다. |
| numberToTake |예 |int |요소 또는 문자 tootake hello 수입니다. 이 값이 0 이하이면 빈 배열 또는 문자열이 반환됩니다. 지정 된 배열 또는 문자열 hello의 hello 길이 보다 큰 경우 hello 배열 또는 문자열의 모든 hello 요소가 반환 됩니다. |

### <a name="return-value"></a>반환 값

배열 또는 문자열입니다.

### <a name="examples"></a>예

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

<a id="tolower" />

## <a name="tolower"></a>toLower
`toLower(stringToChange)`

변환 hello 문자열 toolower 대/소문자를 지정 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| stringToChange |예 |string |hello 값 tooconvert toolower 케이스입니다. |

### <a name="return-value"></a>반환 값

toolower 대/소문자를 변환 하는 hello 문자열입니다.

### <a name="examples"></a>예

다음 예제는 hello 매개 변수 값 toolower 대/소문자 및 tooupper 대/소문자 변환 합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| toLowerOutput | 문자열 | one two three |
| toUpperOutput | 문자열 | ONE TWO THREE |

<a id="toupper" />

## <a name="toupper"></a>toUpper
`toUpper(stringToChange)`

변환 hello 문자열 tooupper 대/소문자를 지정 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| stringToChange |예 |string |hello 값 tooconvert tooupper 케이스입니다. |

### <a name="return-value"></a>반환 값

tooupper 대/소문자를 변환 하는 hello 문자열입니다.

### <a name="examples"></a>예

다음 예제는 hello 매개 변수 값 toolower 대/소문자 및 tooupper 대/소문자 변환 합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| toLowerOutput | 문자열 | one two three |
| toUpperOutput | 문자열 | ONE TWO THREE |

<a id="trim" />

## <a name="trim"></a>trim
`trim (stringToTrim)`

지정 된 모든 선행 및 후행 공백 문자 hello에서 제거.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| stringToTrim |예 |string |hello 값 tootrim 합니다. |

### <a name="return-value"></a>반환 값

선행 및 후행 공백 문자 없이 hello 문자열입니다.

### <a name="examples"></a>예

hello 다음 예제에서는 트림 hello 매개 변수에서 공백 문자 hello 합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "    one two three   "
        }
    },
    "resources": [],
    "outputs": {
        "return": {
            "type": "string",
            "value": "[trim(parameters('testString'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| return | 문자열 | one two three |

<a id="uniquestring" />

## <a name="uniquestring"></a>uniqueString
`uniqueString (baseString, ...)`

매개 변수로 제공 되는 hello 값에 따라 결정적 해시 문자열을 만듭니다. 

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| baseString |예 |string |hello 해시 함수 toocreate 고유한 문자열 hello 값 사용. |
| 필요에 따라 추가하는 매개 변수 |아니요 |string |Hello 수준의 고유성을 지정 하는 필요한 toocreate hello 값으로 만큼 문자열을 추가할 수 있습니다. |

### <a name="remarks"></a>설명

이 함수는 리소스에 대 한 고유한 이름을 toocreate 할 때 유용 합니다. Hello 결과 대 한 고유성 hello 범위를 제한 하는 매개 변수 값을 제공 합니다. Hello 이름이 고유 toosubscription, 리소스 그룹 또는 배포 인지 여부를 지정할 수 있습니다. 

값은 임의의 문자열이 아니지만 대신 해시 함수의 결과 hello hello 반환 됩니다. hello 반환 값은 13 자입니다. 전역적으로 고유하지 않습니다. 프로그램 명명 규칙 toocreate 의미 있는 이름에서에서 접두사로 toocombine hello 값을 할 수 있습니다. hello 다음 예제 hello 형식의 hello 값을 반환 했습니다. 제공 된 매개 변수는 hello hello 실제 값이 다릅니다.

    tcvhiyu5h2o5o

다음 예제는 hello 어떻게 toouse uniqueString toocreate 고유 값을 일반적으로 사용 되는 수준의 보여 줍니다.

범위 지정 된 고유 toosubscription

```json
"[uniqueString(subscription().subscriptionId)]"
```

범위 지정 된 고유 tooresource 그룹

```json
"[uniqueString(resourceGroup().id)]"
```

리소스 그룹에 대 한 범위 지정 된 고유 toodeployment

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

다음 예제는 hello 방법을 toocreate 저장소 계정에 대 한 고유한 이름을 기반으로 리소스 그룹을 보여 줍니다. Hello 리소스 그룹의 내부 hello 이름이 고유 하지 않은 hello를 생성 하는 경우 동일한 방식으로 합니다.

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a>반환 값

13개의 문자를 포함하는 문자열입니다.

### <a name="examples"></a>예

다음 예에서는 hello uniquestring에서 결과 반환 합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "uniqueRG": {
            "value": "[uniqueString(resourceGroup().id)]",
            "type" : "string"
        },
        "uniqueDeploy": {
            "value": "[uniqueString(resourceGroup().id, deployment().name)]",
            "type" : "string"
        }
    }
}
```

<a id="uri" />

## <a name="uri"></a>uri
`uri (baseUri, relativeUri)`

Hello baseUri 및 hello 될 문자열을 결합 하 여 절대 URI를 만듭니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| baseUri |예 |string |hello 기본 uri 문자열입니다. |
| relativeUri |예 |string |hello 상대 uri 문자열 tooadd toohello 기본 uri 문자열입니다. |

hello에 대 한 값을 hello **baseUri** 매개 변수는 특정 파일을 포함할 수 있지만 hello 기본 경로만 hello URI를 구성할 때 사용 됩니다. 예를 들어 전달 `http://contoso.com/resources/azuredeploy.json` 의 기본 URI에 baseUri 매개 변수에 결과 hello로 `http://contoso.com/resources/`합니다.

### <a name="return-value"></a>반환 값

Hello 기본 및 상대 값에 대 한 절대 URI를 hello 나타내는 문자열입니다.

### <a name="examples"></a>예

다음 예제는 hello 방법을 tooconstruct 링크 tooa 중첩 된 템플릿 값을 기반 hello hello 부모 템플릿의 보여 줍니다.

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

hello 방법을 예제와 다음 toouse uri, uriComponent, 및 uriComponentToString:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| uriOutput | 문자열 | http://contoso.com/resources/nested/azuredeploy.json |
| componentOutput | 문자열 | http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json |
| toStringOutput | 문자열 | http://contoso.com/resources/nested/azuredeploy.json |

<a id="uricomponent" />

## <a name="uricomponent"></a>uriComponent
`uricomponent(stringToEncode)`

URI를 인코딩합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| stringToEncode |예 |string |hello 값 tooencode 합니다. |

### <a name="return-value"></a>반환 값

Hello URI의 문자열 값을 인코딩됩니다.

### <a name="examples"></a>예

hello 방법을 예제와 다음 toouse uri, uriComponent, 및 uriComponentToString:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| uriOutput | 문자열 | http://contoso.com/resources/nested/azuredeploy.json |
| componentOutput | 문자열 | http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json |
| toStringOutput | 문자열 | http://contoso.com/resources/nested/azuredeploy.json |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a>uriComponentToString
`uriComponentToString(uriEncodedString)`

URI로 인코딩된 값의 문자열을 반환합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| uriEncodedString |예 |string |hello URI 인코딩된 tooconvert tooa 문자열 값입니다. |

### <a name="return-value"></a>반환 값

URI로 인코딩된 값의 디코딩된 문자열입니다.

### <a name="examples"></a>예

hello 방법을 예제와 다음 toouse uri, uriComponent, 및 uriComponentToString:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| uriOutput | 문자열 | http://contoso.com/resources/nested/azuredeploy.json |
| componentOutput | 문자열 | http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json |
| toStringOutput | 문자열 | http://contoso.com/resources/nested/azuredeploy.json |


## <a name="next-steps"></a>다음 단계
* Azure 리소스 관리자 템플릿의 hello 섹션에 대 한 참조 [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.
* toomerge 템플릿이 여러 개 참조 [Azure 리소스 관리자와 연결 된 템플릿을 사용 하 여](resource-group-linked-templates.md)합니다.
* 지정 된 횟수 만큼 tooiterate 리소스의 종류를 만들 때 참조 [Azure 리소스 관리자 리소스의 여러 인스턴스를 만들](resource-group-create-multiple.md)합니다.
* toosee toodeploy hello 서식 파일을 만든 참조 [Azure 리소스 관리자 템플릿 사용 하 여 응용 프로그램 배포](resource-group-template-deploy.md)합니다.

