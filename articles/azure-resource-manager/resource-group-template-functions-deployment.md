---
title: "aaaAzure 리소스 관리자 템플릿 함수 배포 | Microsoft Docs"
description: "Hello 함수 toouse는 Azure 리소스 관리자 템플릿 tooretrieve 배포 정보에 설명합니다."
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
ms.openlocfilehash: 458c3f740504fdd6799ed24cc386219726737636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a>Azure Resource Manager 템플릿용 배포 함수 

리소스 관리자는 hello 다음 hello 서식 파일의 섹션에서 값 가져오기에 대 한 함수 및 관련된 toohello 배포 값을 제공 합니다.

* [deployment](#deployment)
* [매개 변수](#parameters)
* [variables](#variables)

리소스, 리소스 그룹 또는 구독에서 tooget 값 참조 [리소스 함수](resource-group-template-functions-resource.md)합니다.

<a id="deployment" />

## <a name="deployment"></a>배포
`deployment()`

Hello 현재 배포 작업에 대 한 정보를 반환합니다.

### <a name="return-value"></a>반환 값

이 함수는 배포 중에 전달 되는 hello 개체를 반환 합니다. 개체를 반환 하는 hello에 hello 속성 hello 배포 개체를 전달 했는지 여부 또는 인라인 개체로 링크에 따라 다릅니다. Hello 배포 전달 경우 인라인와 같은 hello를 사용 하는 경우 **-TemplateFile** 매개 변수 hello Azure PowerShell toopoint tooa 로컬 파일에서 개체의 형식에 따라 hello을 반환 합니다.

```json
{
    "name": "",
    "properties": {
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [
            ],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

Hello 개체 때 hello를 사용 하 여 같은 링크로 전달 되 면 **-TemplateUri** 매개 변수 toopoint tooa 원격 개체 형식에 따라 hello에 hello 개체가 반환 됩니다. 

```json
{
    "name": "",
    "properties": {
        "templateLink": {
            "uri": ""
        },
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

### <a name="remarks"></a>설명

Hello hello 부모 템플릿의 URI에 따라 배포 선정 () toolink tooanother 템플릿을 사용할 수 있습니다.

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a>예제

hello 다음 예제에서는 개체를 반환 hello 배포:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[deployment()]",
            "type" : "object"
        }
    }
}
```

hello 위 예제에서는 반환 개체를 다음 hello:

```json
{
  "name": "deployment",
  "properties": {
    "template": {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "resources": [],
      "outputs": {
        "subscriptionOutput": {
          "type": "Object",
          "value": "[deployment()]"
        }
      }
    },
    "parameters": {},
    "mode": "Incremental",
    "provisioningState": "Accepted"
  }
}
```

<a id="parameters" />

## <a name="parameters"></a>매개 변수
`parameters(parameterName)`

매개 변수 값을 반환합니다. 지정한 매개 변수 이름이 hello hello 템플릿의 hello 매개 변수 섹션에서 정의 되어야 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| parameterName |예 |string |hello 매개 변수 tooreturn의 hello 이름입니다. |

### <a name="return-value"></a>반환 값

hello hello 값 매개 변수를 지정 합니다.

### <a name="remarks"></a>설명

일반적으로 매개 변수 tooset 리소스 값을 사용 합니다. hello 다음 예제에서는 설정 배포 중에 전달 하는 웹 사이트 toohello 매개 변수 값의 hello 이름입니다.

```json
"parameters": { 
  "siteName": {
      "type": "string"
  }
},
"resources": [
   {
      "apiVersion": "2016-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/Sites",
      ...
   }
]
```

### <a name="example"></a>예제

hello 다음 예제에서는 hello 매개 변수 함수를 사용 하는 단순화

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringParameter": {
            "type" : "string",
            "defaultValue": "option 1"
        },
        "intParameter": {
            "type": "int",
            "defaultValue": 1
        },
        "objectParameter": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b"}
        },
        "arrayParameter": {
            "type": "array",
            "defaultValue": [1, 2, 3]
        },
        "crossParameter": {
            "type": "string",
            "defaultValue": "[parameters('stringParameter')]"
        }
    },
    "variables": {},
    "resources": [],
    "outputs": {
        "stringOutput": {
            "value": "[parameters('stringParameter')]",
            "type" : "string"
        },
        "intOutput": {
            "value": "[parameters('intParameter')]",
            "type" : "int"
        },
        "objectOutput": {
            "value": "[parameters('objectParameter')]",
            "type" : "object"
        },
        "arrayOutput": {
            "value": "[parameters('arrayParameter')]",
            "type" : "array"
        },
        "crossOutput": {
            "value": "[parameters('crossParameter')]",
            "type" : "string"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| stringOutput | 문자열 | 옵션 1 |
| intOutput | int | 1 |
| objectOutput | Object | {“one”: “a”, “two”: “b”} |
| arrayOutput | 배열 | [1, 2, 3] |
| crossOutput | 문자열 | 옵션 1 |

<a id="variables" />

## <a name="variables"></a>variables
`variables(variableName)`

반환 hello 변수의 값입니다. 지정한 변수 이름이 hello hello 템플릿의 hello 변수 섹션에서 정의 되어야 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| variableName |예 |문자열 |hello 변수 tooreturn의 hello 이름입니다. |

### <a name="return-value"></a>반환 값

hello 지정 변수의 hello 값입니다.

### <a name="remarks"></a>설명

일반적으로 사용 하면 변수 toosimplify 서식 파일에 복잡 한 값을 한 번만 생성 됩니다. hello 다음 구성 예제는 저장소 계정에 대 한 고유 이름입니다.

```json
"variables": {
    "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
},
"resources": [
    {
        "type": "Microsoft.Storage/storageAccounts",
        "name": "[variables('storageName')]",
        ...
    },
    {
        "type": "Microsoft.Compute/virtualMachines",
        "dependsOn": [
            "[variables('storageName')]"
        ],
        ...
    }
],
```

### <a name="example"></a>예제

hello 예제 템플릿 각기 다른 변수 값을 반환합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "variables": {
        "var1": "myVariable",
        "var2": [ 1,2,3,4 ],
        "var3": "[ variables('var1') ]",
        "var4": {
            "property1": "value1",
            "property2": "value2"
        }
    },
    "resources": [],
    "outputs": {
        "exampleOutput1": {
            "value": "[variables('var1')]",
            "type" : "string"
        },
        "exampleOutput2": {
            "value": "[variables('var2')]",
            "type" : "array"
        },
        "exampleOutput3": {
            "value": "[variables('var3')]",
            "type" : "string"
        },
        "exampleOutput4": {
            "value": "[variables('var4')]",
            "type" : "object"
        }
    }
}
```

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| exampleOutput1 | 문자열 | myVariable |
| exampleOutput2 | 배열 | [1, 2, 3, 4] |
| exampleOutput3 | 문자열 | myVariable |
| exampleOutput4 |  Object | {“property1”: “value1”, “property2”: “value2”} |

## <a name="next-steps"></a>다음 단계
* Azure 리소스 관리자 템플릿의 hello 섹션에 대 한 참조 [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.
* toomerge 템플릿이 여러 개 참조 [Azure 리소스 관리자와 연결 된 템플릿을 사용 하 여](resource-group-linked-templates.md)합니다.
* 지정 된 횟수 만큼 tooiterate 리소스의 종류를 만들 때 참조 [Azure 리소스 관리자 리소스의 여러 인스턴스를 만들](resource-group-create-multiple.md)합니다.
* toosee toodeploy hello 서식 파일을 만든 참조 [Azure 리소스 관리자 템플릿 사용 하 여 응용 프로그램 배포](resource-group-template-deploy.md)합니다.

