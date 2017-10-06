---
title: "aaaAzure 리소스 관리자 템플릿 구조와 구문을 | Microsoft Docs"
description: "선언적 JSON 구문을 사용 하 여 Azure 리소스 관리자 템플릿의 hello 구조와 속성을 설명 합니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 19694cb4-d9ed-499a-a2cc-bcfc4922d7f5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/14/2017
ms.author: tomfitz
ms.openlocfilehash: b0709852f8777c91cc1704d6bca16257a017d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-structure-and-syntax-of-azure-resource-manager-templates"></a>Hello 구조 및 Azure 리소스 관리자 템플릿 구문을 이해합니다
이 항목에서는 Azure Resource Manager 템플릿의 hello 구조를 설명 합니다. 해당 섹션에서 사용할 수 있는 템플릿과 hello 속성의 여러 다른 섹션 hello를 표시 합니다. JSON 및 배포에 대 한 tooconstruct 값을 사용할 수 있는 식의 hello 템플릿은 구성 됩니다. 템플릿 만들기에 관한 단계별 연습은 [첫 번째 Azure Resource Manager 템플릿 만들기](resource-manager-create-first-template.md)를 참조하세요.

## <a name="template-format"></a>템플릿 형식
가장 간단한 구조로 서식 파일 요소 다음 hello를 포함 되어 있습니다.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  },
    "variables": {  },
    "resources": [  ],
    "outputs": {  }
}
```

| 요소 이름 | 필수 | 설명 |
|:--- |:--- |:--- |
| $schema |예 |Hello 버전의 hello 템플릿 언어를 설명 하는 hello JSON 스키마 파일의 위치입니다. Hello에에서 표시 된 URL 앞 예제는 hello를 사용 합니다. |
| contentVersion |예 |Hello 템플릿 (예: 1.0.0.0)의 버전입니다. 이 요소에 값을 제공할 수 있습니다. Hello 서식 파일을 사용 하 여 리소스를 배포 하는 경우이 값에 사용 되는 toomake hello 오른쪽 템플릿을 사용 되 고 있는지 수 있습니다. |
| 매개 변수 |아니요 |배포 되 면 제공 되는 값 toocustomize 리소스 배포를 실행 합니다. |
| variables |아니요 |Hello 템플릿 toosimplify 템플릿 언어 식에 JSON 조각을으로 사용 되는 값입니다. |
| 리소스 |예 |리소스 그룹에 배포 또는 업데이트되는 리소스 종류입니다. |
| outputs |아니요 |배포 후 반환되는 값입니다. |

각 요소에는 사용자가 설정할 수 있는 속성이 포함되어 있습니다. 다음 예제는 hello hello 템플릿에 대 한 전체 구문이 포함 되어 있습니다.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  
        "<parameter-name>" : {
            "type" : "<type-of-parameter-value>",
            "defaultValue": "<default-value-of-parameter>",
            "allowedValues": [ "<array-of-allowed-values>" ],
            "minValue": <minimum-value-for-int>,
            "maxValue": <maximum-value-for-int>,
            "minLength": <minimum-length-for-string-or-array>,
            "maxLength": <maximum-length-for-string-or-array-parameters>,
            "metadata": {
                "description": "<description-of-hello parameter>" 
            }
        }
    },
    "variables": {  
        "<variable-name>": "<variable-value>",
        "<variable-name>": { 
            <variable-complex-type-value> 
        }
    },
    "resources": [
      {
          "condition": "<boolean-value-whether-to-deploy>",
          "apiVersion": "<api-version-of-resource>",
          "type": "<resource-provider-namespace/resource-type-name>",
          "name": "<name-of-the-resource>",
          "location": "<location-of-resource>",
          "tags": {
              "<tag-name1>": "<tag-value1>",
              "<tag-name2>": "<tag-value2>"
          },
          "comments": "<your-reference-notes>",
          "copy": {
              "name": "<name-of-copy-loop>",
              "count": "<number-of-iterations>",
              "mode": "<serial-or-parallel>",
              "batchSize": "<number-to-deploy-serially>"
          },
          "dependsOn": [
              "<array-of-related-resource-names>"
          ],
          "properties": {
              "<settings-for-the-resource>",
              "copy": [
                  {
                      "name": ,
                      "count": ,
                      "input": {}
                  }
              ]
          },
          "resources": [
              "<array-of-child-resources>"
          ]
      }
    ],
    "outputs": {
        "<outputName>" : {
            "type" : "<type-of-output-value>",
            "value": "<output-value-expression>"
        }
    }
}
```

이 항목의 뒷부분에 자세히 hello 템플릿의 hello 섹션을 살펴보겠습니다.

## <a name="expressions-and-functions"></a>식 및 함수
hello 기본 hello 서식 파일의 구문은 JSON입니다. 그러나 식과 함수 hello 템플릿 내에서 사용할 수 있는 hello JSON 값을 확장합니다.  식이 작성 JSON 문자열 리터럴 내에서 해당 첫 번째 및 마지막 문자는 hello 대괄호: `[` 및 `]`각각. hello 식의 hello 값 hello 템플릿이 배포 될 때 평가 됩니다. 문자열 리터럴로 작성 하는 동안 다른 JSON 형식의 배열 또는 정수 hello 실제 식에 따라 같은 hello 식의 계산 결과 hello 가능 합니다.  리터럴 문자열에 대괄호로 시작 하는 toohave `[`, 식으로 해석 하 게을 제외한 추가 대괄호 toostart hello 문자열을 추가 `[[`합니다.

일반적으로 식을 함수 tooperform 작업 hello 배포를 구성 하는 데 사용 합니다. JavaScript에서와 마찬가지로 함수 호출은 `functionName(arg1,arg2,arg3)`과 같이 형식이 지정됩니다. Hello 점 및 [index] 연산자를 사용 하 여 속성을 참조 합니다.

다음 예제는 hello를 생성할 때 동작 하는 여러 toouse 값 방법을 보여 줍니다.

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

Hello 전체 목록은 템플릿 함수를 참조 하십시오. [Azure 리소스 관리자 템플릿 함수](resource-group-template-functions.md)합니다. 

## <a name="parameters"></a>매개 변수
Hello hello 서식 파일의 매개 변수 섹션, 배포 하는 경우를 입력할 수 있는 값 hello 리소스 지정 합니다. 이러한 매개 변수 값 (예: 개발, 테스트 및 프로덕션) 환경에 맞는 값을 제공 하 여 toocustomize hello 배포를 사용 합니다. 템플릿에 tooprovide 매개 변수가 필요는 없지만 매개 변수 없이 서식 파일에는 항상 배포 hello와 같은 리소스 hello 동일한 이름, 위치 및 속성입니다.

구조를 다음 hello로 매개 변수를 정의 합니다.

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": "<default-value-of-parameter>",
        "allowedValues": [ "<array-of-allowed-values>" ],
        "minValue": <minimum-value-for-int>,
        "maxValue": <maximum-value-for-int>,
        "minLength": <minimum-length-for-string-or-array>,
        "maxLength": <maximum-length-for-string-or-array-parameters>,
        "metadata": {
            "description": "<description-of-hello parameter>" 
        }
    }
}
```

| 요소 이름 | 필수 | 설명 |
|:--- |:--- |:--- |
| parameterName |예 |Hello 매개 변수의 이름입니다. 유효한 JavaScript 식별자여야 합니다. |
| type |예 |Hello 매개 변수 값의 형식입니다. 이 표 다음 허용된 유형 목록을 hello를 참조 하십시오. |
| defaultValue |아니요 |Hello 매개 변수를 값이 없는 hello 매개 변수에 대해 제공 하는 경우에 대 한 기본값입니다. |
| allowedValues |아니요 |Hello 매개 변수 toomake hello 오른쪽 값을 제공 하 고 있는지에 대 한 허용 되는 값의 배열입니다. |
| minValue |아니요 |int 형식 매개 변수에 대 한 최소값을 hello로이 값은 포함 합니다. |
| maxValue |아니요 |int 형식 매개 변수에 대해 hello 최대 값이이 값은 포함 합니다. |
| minLength |아니요 |hello 문자열과 secureString, 형식 매개 변수 배열에 대 한 최소 길이,이 값은 포함 합니다. |
| maxLength |아니요 |hello 문자열과 secureString, 형식 매개 변수 배열에 대 한 최대 길이이 값은 포함 합니다. |
| 설명 |아니요 |Hello 포털을 통해 toousers를 표시 하는 설명은 hello 매개 변수입니다. |

hello 허용된 유형 및 값은:

* **string**
* **secureString**
* **int**
* **bool**
* **object** 
* **secureObject**
* **array**

선택적으로 매개 변수 toospecify defaultValue (빈 문자열일 수 있음)를 제공 합니다. 

Hello 명령 toodeploy hello 서식 파일의 매개 변수와 일치 하는 서식 파일에서 매개 변수 이름을 지정 하면 사용자가 제공한 hello 값에 대 한 잠재적 모호성이 있습니다. 리소스 관리자는 hello 접미사를 추가 하 여 이러한 혼동을 해결 **FromTemplate** toohello 템플릿 매개 변수입니다. 예를 들어, 명명 된 매개 변수를 포함 하는 경우 **ResourceGroupName** hello와 충돌 템플릿에 **ResourceGroupName** hello에 대 한 매개 변수 [ 새 AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet. 배포 하는 동안는 tooprovide 입력 정보 요청된에 대 한 값 **ResourceGroupNameFromTemplate**합니다. 일반적으로 이러한 혼동 하지 배포 작업에 사용 되는 매개 변수로 이름과 같은 이름을 hello로 매개 변수 이름을 지정 하지 마십시오.

> [!NOTE]
> 모든 암호, 키 및 기타 암호 hello를 사용 해야 **secureString** 유형입니다. Hello를 사용 하 여 JSON 개체에 중요 한 데이터를 전달 하는 경우 **secureObject** 유형입니다. 리소스 배포 후에는 secureString 또는 secureObject 형식의 템플릿 매개 변수를 읽을 수 없습니다. 
> 
> 예를 들어 hello hello 배포 기록의 다음 항목 hello 값을 표시 문자열 및 개체에 대 한 있지만 secureString 및 secureObject 대 한 합니다.
>
> ![배포 값 표시](./media/resource-group-authoring-templates/show-parameters.png)  
>

hello 방법을 예제와 다음 toodefine 매개 변수:

```json
"parameters": {
    "siteName": {
        "type": "string",
        "defaultValue": "[concat('site', uniqueString(resourceGroup().id))]"
    },
    "hostingPlanName": {
        "type": "string",
        "defaultValue": "[concat(parameters('siteName'),'-plan')]"
    },
    "skuName": {
        "type": "string",
        "defaultValue": "F1",
        "allowedValues": [
          "F1",
          "D1",
          "B1",
          "B2",
          "B3",
          "S1",
          "S2",
          "S3",
          "P1",
          "P2",
          "P3",
          "P4"
        ]
    },
    "skuCapacity": {
        "type": "int",
        "defaultValue": 1,
        "minValue": 1
    }
}
```

방법을 배포 하는 동안 tooinput hello 매개 변수 값, 참조 [Azure 리소스 관리자 템플릿 사용 하 여 응용 프로그램 배포](resource-group-template-deploy.md)합니다. 

## <a name="variables"></a>variables
Hello 변수 섹션에서 서식 파일에 전체에서 사용할 수 있는 값을 생성 합니다. Toodefine 변수 필요는 없지만 종종 서식 파일에는 복잡 한 식을 줄여서 간소화 합니다.

구조를 다음 hello로 변수를 정의 합니다.

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

hello 방법을 예제와 다음 두 개의 매개 변수 값에서 생성 된 변수 toodefine:

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

hello 다음 예제에서는 다른 변수에서 생성 되는 변수 및 변수는 복합 JSON 유형를 보여 줍니다.

```json
"parameters": {
    "environmentName": {
        "type": "string",
        "allowedValues": [
          "test",
          "prod"
        ]
    }
},
"variables": {
    "environmentSettings": {
        "test": {
            "instancesSize": "Small",
            "instancesCount": 1
        },
        "prod": {
            "instancesSize": "Large",
            "instancesCount": 4
        }
    },
    "currentEnvironmentSettings": "[variables('environmentSettings')[parameters('environmentName')]]",
    "instancesSize": "[variables('currentEnvironmentSettings').instancesSize]",
    "instancesCount": "[variables('currentEnvironmentSettings').instancesCount]"
}
```

## <a name="resources"></a>리소스
Hello 리소스 섹션에 배포 또는 업데이트할지 여부를 지정 하는 hello 리소스를 정의 합니다. 이 섹션 hello 형식 이해 해야 하기 때문에 복잡 해질 수 있습니다 tooprovide hello 오른쪽 값을 배포 하는 합니다. Hello 리소스별 값 (apiVersion, 유형 및 속성) tooset 해야 하는, 참조 [Azure 리소스 관리자 템플릿을에 리소스를 정의](/azure/templates/)합니다. 

구조를 다음 hello로 리소스를 정의 합니다.

```json
"resources": [
  {
      "condition": "<boolean-value-whether-to-deploy>",
      "apiVersion": "<api-version-of-resource>",
      "type": "<resource-provider-namespace/resource-type-name>",
      "name": "<name-of-the-resource>",
      "location": "<location-of-resource>",
      "tags": {
          "<tag-name1>": "<tag-value1>",
          "<tag-name2>": "<tag-value2>"
      },
      "comments": "<your-reference-notes>",
      "copy": {
          "name": "<name-of-copy-loop>",
          "count": "<number-of-iterations>",
          "mode": "<serial-or-parallel>",
          "batchSize": "<number-to-deploy-serially>"
      },
      "dependsOn": [
          "<array-of-related-resource-names>"
      ],
      "properties": {
          "<settings-for-the-resource>",
          "copy": [
              {
                  "name": ,
                  "count": ,
                  "input": {}
              }
          ]
      },
      "resources": [
          "<array-of-child-resources>"
      ]
  }
]
```

| 요소 이름 | 필수 | 설명 |
|:--- |:--- |:--- |
| condition | 아니요 | Hello 리소스 배포 되는지 여부를 나타내는 부울 값입니다. |
| apiVersion |예 |Hello 리소스를 만들기 위한 REST API toouse hello의 버전입니다. |
| type |예 |Hello 리소스의 형식입니다. 이 값은 hello 리소스 공급자 및 hello 리소스 종류의 hello 네임 스페이스의 조합 (예: **/storageaccounts**). |
| name |예 |Hello 리소스의 이름입니다. hello 이름은 RFC3986에 정의 된 URI 구성 요소 제한을 따라야 합니다. Hello 리소스 이름 toooutside 파티를 노출 하는 Azure 서비스 hello 이름 toomake 시도 toospoof 아닌지 유효성 검사는 또한 다른 id입니다. |
| location |다름 |Hello의 지원 되는 지리적 위치는 리소스를 제공합니다. Hello 사용 가능한 위치 중 하나를 선택할 수 되지만 일반적으로 의미 toopick 닫기 tooyour 사용자가 되는 것입니다. 일반적으로 만드는 것도 좋습니다 서로 상호 작용 hello에 동일한 tooplace 리소스 영역입니다. 대부분의 리소스 종류에는 위치가 필요하지만 일부 종류(예: 역할 할당)에는 위치가 필요하지 않습니다. [Azure Resource Manager 템플릿에서 리소스 위치 설정](resource-manager-template-location.md)을 참조하세요. |
| tags |아니요 |Hello 리소스와 연결 된 태그입니다. [Azure Resource Manager 템플릿에서 리소스에 태그 지정](resource-manager-template-tags.md)을 참조하세요. |
| 설명 |아니요 |에 대 한 서식 파일에 hello 리소스 설명서 노트 |
| 복사 |아니요 |둘 이상의 인스턴스가 필요한 경우 hello toocreate 리소스의 수입니다. hello 기본 모드는 병렬입니다. 일부 또는 hello에 대 한 리소스 toodeploy hello 하지 않는 경우 직렬 모드를 지정 합니다. 같은 시간입니다. 자세한 내용은 [Azure Resource Manager에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요. |
| dependsOn |아니요 |이 리소스를 배포하기 전에 배포해야 하는 리소스입니다. 리소스 관리자 리소스 간의 종속성을 hello 평가 하 고 hello 올바른 순서에 배포 합니다. 리소스는 서로 종속되지 않을 경우 병렬로 배포됩니다. hello 값 목록이 될 수 쉼표로 구분 된 리소스의 이름 또는 리소스의 고유 식별자입니다. 이 템플릿에 배포된 리소스만 나열합니다. 이 템플릿에 정의되지 않은 리소스는 이미 존재해야 합니다. 불필요한 종속성은 배포 속도를 느리게 만들고 순환 종속성을 만들기 때문에 추가하지 않습니다. 종속성 설정에 대한 지침은 [Azure Resource Manager 템플릿에서 종속성 정의](resource-group-define-dependencies.md)를 참조하세요. |
| properties |아니요 |리소스별 구성 설정입니다. hello 속성에 대 한 hello 값은 hello REST API 작업 (PUT 메서드) toocreate hello 리소스에 대 한 hello 요청 본문에 제공 하는 hello 값으로 hello 동일 합니다. 또한 속성의 여러 인스턴스 복사본 배열 toocreate를 지정할 수 있습니다. 자세한 내용은 [Azure Resource Manager에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요. |
| 리소스 |아니요 |정의 중인 hello 리소스에 종속 된 자식 리소스입니다. 만 hello 부모 리소스의 hello 스키마에서 허용 하는 리소스 종류를 제공 합니다. hello hello 자식 리소스의 정규화 된 형식 hello 부모 리소스 종류와 같은 포함 **Microsoft.Web/sites/extensions**합니다. Hello 부모 리소스에 대 한 종속성이 포함 되지 않습니다. 해당 종속성을 명시적으로 정의해야 합니다. |

hello 리소스 섹션에는 hello 리소스 toodeploy 배열을 포함 합니다. 각 리소스 내에서 자식 리소스의 배열도 정의할 수 있습니다. 따라서 리소스 섹션에는 다음과 같은 구조가 있을 수 있습니다.

```json
"resources": [
  {
      "name": "resourceA",
  },
  {
      "name": "resourceB",
      "resources": [
        {
            "name": "firstChildResourceB",
        },
        {   
            "name": "secondChildResourceB",
        }
      ]
  },
  {
      "name": "resourceC",
  }
]
```      

자식 리소스를 정의하는 방법에 대한 자세한 내용은 [Resource Manager 템플릿에서 자식 리소스에 대한 이름 및 형식 설정](resource-manager-template-child-resource.md)을 참조하세요.

hello **조건** 요소 hello 리소스 배포 되는지 여부를 지정 합니다. 이 요소에 대 한 hello 값 tootrue 또는 false를 확인합니다. 예를 들어 toospecify 새 저장소 계정에 배포 하는지 여부를 사용 합니다.

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

기존 또는 새 리소스 사용 예제는 [신규 또는 기존 조건 템플릿](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json)을 참조하세요.

toospecify 정의할 수 있는지 여부를 암호 또는 SSH 키로는 가상 컴퓨터가 배포 된 두 가지 버전의 hello 가상 컴퓨터 템플릿을를 사용 하 여 **조건** toodifferentiate 사용 합니다. 어떤 시나리오 toodeploy를 지정 하는 매개 변수를 전달 합니다.

```json
{
    "condition": "[equals(parameters('passwordOrSshKey'),'password')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'password')]",
    "properties": {
        "osProfile": {
            "computerName": "[variables('vmName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
        },
        ...
    },
    ...
},
{
    "condition": "[equals(parameters('passwordOrSshKey'),'sshKey')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'ssh')]",
    "properties": {
        "osProfile": {
            "linuxConfiguration": {
                "disablePasswordAuthentication": "true",
                "ssh": {
                    "publicKeys": [
                        {
                            "path": "[variables('sshKeyPath')]",
                            "keyData": "[parameters('adminSshKey')]"
                        }
                    ]
                }
            }
        },
        ...
    },
    ...
}
``` 

암호 또는 SSH 키 toodeploy 가상 컴퓨터를 사용 하 여 예제를 보려면 [사용자 이름 또는 SSH 조건 템플릿](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json)합니다.

## <a name="outputs"></a>outputs
Hello 출력 섹션의 배포에서 반환 된 값을 지정 합니다. 예를 들어 배포 된 리소스 URI tooaccess hello를 반환할 수 있습니다.

hello 다음 예제에서는 구조를 보여 줍니다 hello 출력 정의:

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| 요소 이름 | 필수 | 설명 |
|:--- |:--- |:--- |
| outputName |예 |Hello 출력 값의 이름입니다. 유효한 JavaScript 식별자여야 합니다. |
| type |예 |Hello 출력 값의 형식입니다. 출력 값에는 동일한 형식 템플릿 입력된 매개 변수로 hello를 지원 합니다. |
| 값 |예 |출력 값으로 계산되어 반환되는 템플릿 언어 식입니다. |

hello 다음 예제에서는 hello 출력 섹션에서 반환 되는 값

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

출력 작업에 대한 자세한 내용은 [Azure Resource Manager 템플릿에서 상태 공유](best-practices-resource-manager-state.md)를 참조하세요.

## <a name="template-limits"></a>템플릿 제한

Hello 크기 제한의 템플릿 too1 MB 이며 각 매개 변수에 파일 too64 (KB)입니다. hello 1MB 제한을 반복 리소스 정 및 변수 및 매개 변수를 사용 하 여 확장 된 후 toohello hello 서식 파일의 최종 상태를 적용 합니다. 

또한 다음으로 제한됩니다.

* 매개 변수 256개
* 변수 256개
* 리소스 800개(인쇄 매수 포함)
* 출력 값 64개
* 템플릿 식의 문자 24,576자

중첩된 템플릿을 사용하여 일부 템플릿 제한을 초과할 수 있습니다. 자세한 내용은 [Azure 리소스를 배포할 때 연결된 템플릿 사용](resource-group-linked-templates.md)을 참조하세요. tooreduce hello 수의 매개 변수, 변수 또는 출력을 개체에 여러 값을 결합할 수 있습니다. 자세한 내용은 [매개 변수로 개체 사용](resource-manager-objects-as-parameters.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계
* 다양 한 유형의 솔루션에 대 한 전체 템플릿을 tooview 참조 hello [Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/)합니다.
* 템플릿 내에서 사용 가능한 hello 함수에 대 한 세부 정보를 참조 하십시오. [Azure 리소스 관리자 템플릿 함수](resource-group-template-functions.md)합니다.
* toocombine 여러 템플릿을 배포 하는 동안 참조 [Azure 리소스 관리자와 연결 된 템플릿을 사용 하 여](resource-group-linked-templates.md)합니다.
* 다른 리소스 그룹 내에 있는 toouse 리소스를 할 수 있습니다. 이 시나리오에서는 일반적으로 여러 리소스 그룹에서 공유하는 저장소 계정 또는 가상 네트워크에서 작업합니다. 자세한 내용은 참조 hello [resourceId 함수](resource-group-template-functions-resource.md#resourceid)합니다.
