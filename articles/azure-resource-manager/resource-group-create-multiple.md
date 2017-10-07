---
title: "aaaDeploy Azure 리소스를 여러 개 | Microsoft Docs"
description: "복사 작업 및 Azure 리소스 관리자 템플릿 tooiterate 배열은 여러 번 사용할 리소스를 배포 하는 경우."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 94d95810-a87b-460f-8e82-c69d462ac3ca
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/26/2017
ms.author: tomfitz
ms.openlocfilehash: a3bd42f694053317c30b639c33dc4efae41a9a9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a>Azure Resource Manager 템플릿에서 리소스 또는 속성의 여러 인스턴스 배포
표시 하는이 항목에서 Azure 리소스 관리자 템플릿 toocreate tooiterate, 리소스의 여러 인스턴스 또는 여러 개 리소스에는 속성입니다.

리소스 배포 되었는지 여부를 참조 toospecify를 사용 하는 tooadd 논리 tooyour 템플릿을 필요한 경우 [조건에 따라 리소스를 배포](#conditionally-deploy-resource)합니다.

## <a name="resource-iteration"></a>리소스 반복
toocreate 리소스 종류의 여러 인스턴스 추가 `copy` 요소 toohello 리소스 종류입니다. Hello copy 요소에서 hello 수가 반복 및이 루프에 대 한 이름을 지정합니다. hello 개수 값 양의 정수 여야 하 고 800을 초과할 수 없습니다. 리소스 관리자 병렬로 hello 리소스를 만듭니다. 따라서 생성 되는 hello 순서는 보장 되지 않습니다. 순서 대로 반복 toocreate 리소스 참조 [직렬 복사](#serial-copy)합니다. 

hello 리소스 toocreate 여러 번 형식에 따라 hello를 사용 합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        }
    ],
    "outputs": {}
}
```

해당 hello 확인 hello를 포함 하는 각 리소스의 이름 `copyIndex()` hello 루프에서 hello 현재 반복을 반환 하는 함수입니다. `copyIndex()`는 0부터 시작합니다. 다음 예에서는, hello:

```json
"name": "[concat('storage', copyIndex())]",
```

다음과 같은 이름을 만듭니다.

* storage0
* storage1
* storage2

toooffset hello 인덱스 값을 hello copyIndex() 함수에 값을 전달할 수 있습니다. hello 반복 tooperform 수가 지정 되어 hello copy 요소에서 있지만 copyIndex hello 값은 지정 된 hello 오프셋 값입니다. 다음 예에서는, hello:

```json
"name": "[concat('storage', copyIndex(1))]",
```

다음과 같은 이름을 만듭니다.

* storage1
* storage2
* storage3

hello 복사 작업이 hello 배열의 각 요소를 반복할 수 때문에 배열에서 작업할 때 유용 합니다. 사용 하 여 hello `length` , 반복에 대 한 hello 배열 toospecify hello 수에는 함수 및 `copyIndex` tooretrieve hello 현재 hello 배열의 인덱스입니다. 다음 예에서는, hello:

```json
"parameters": { 
  "org": { 
     "type": "array", 
     "defaultValue": [ 
         "contoso", 
         "fabrikam", 
         "coho" 
      ] 
  }
}, 
"resources": [ 
  { 
      "name": "[concat('storage', parameters('org')[copyIndex()])]", 
      "copy": { 
         "name": "storagecopy", 
         "count": "[length(parameters('org'))]" 
      }, 
      ...
  } 
]
```

다음과 같은 이름을 만듭니다.

* storagecontoso
* storagefabrikam
* storagecoho

## <a name="serial-copy"></a>직렬 복사

복사 요소 toocreate hello를 사용 하는 경우 리소스 종류, 리소스 관리자 기본적으로의 여러 인스턴스는 동시에 이러한 인스턴스를 배포 합니다. 그러나, 순서 대로 리소스를 배포 하는 hello toospecify를 설정할 수 있습니다. 예를 들어 프로덕션 환경으로 업데이트할 때 좋습니다 toostagger hello 업데이트에 특정 수를 한 번에 업데이트 됩니다.

리소스 관리자 여러 인스턴스를 배포 하는 hello copy 요소에서 tooserially 있습니다 사용할 수 있는 속성을 제공 합니다. Hello copy 요소에서 설정 `mode` 너무**직렬** 및 `batchSize` toohello 수가 한 번에 인스턴스 toodeploy 합니다. 직렬 모드에서는 리소스 관리자 hello 이전 일괄 처리가 완료 될 때까지 하나의 일괄 처리 시작 되지 않으면 하므로 hello 루프에 있는 이전 인스턴스에 종속성을 만듭니다.

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

hello 모드 속성 받기도 **병렬**, hello 기본값은입니다.

tootest 직렬 복사본 실제 리소스를 만들지 않고 다음 빈 중첩 된 서식 파일을 배포 하는 템플릿에 사용 하 여 hello:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "numberToDeploy": {
      "type": "int",
      "minValue": 2,
      "defaultValue": 5
    }
  },
  "resources": [
    {
      "apiVersion": "2015-01-01",
      "type": "Microsoft.Resources/deployments",
      "name": "[concat('loop-', copyIndex())]",
      "copy": {
        "name": "iterator",
        "count": "[parameters('numberToDeploy')]",
        "mode": "serial",
        "batchSize": 1
      },
      "properties": {
        "mode": "Incremental",
        "template": {
          "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {},
          "variables": {},
          "resources": [],
          "outputs": {
          }
        }
      }
    }
  ],
  "outputs": {
  }
}
```

Hello 배포 기록에 중첩된 배포 hello 순서 대로 처리 됩니다.

![직렬 배포](./media/resource-group-create-multiple/serial-copy.png)

보다 실제적인 시나리오에 대 한 hello 다음 예에서는 중첩 된 템플릿에서 Linux VM의 한 번에 두 개의 인스턴스를 배포 합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "User name for hello Virtual Machine."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Password for hello Virtual Machine."
            }
        },
        "dnsLabelPrefix": {
            "type": "string",
            "metadata": {
                "description": "Unique DNS Name for hello Public IP used tooaccess hello Virtual Machine."
            }
        },
        "ubuntuOSVersion": {
            "type": "string",
            "defaultValue": "16.04.0-LTS",
            "allowedValues": [
                "12.04.5-LTS",
                "14.04.5-LTS",
                "15.10",
                "16.04.0-LTS"
            ],
            "metadata": {
                "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version."
            }
        }
    },
    "variables": {
        "templatelink": "https://raw.githubusercontent.com/rjmax/Build2017/master/Act1.TemplateEnhancements/Chapter03.LinuxVM.json"
    },
    "resources": [
        {
            "apiVersion": "2015-01-01",
            "name": "[concat('nestedDeployment',copyIndex())]",
            "type": "Microsoft.Resources/deployments",
            "copy": {
                "name": "myCopySet",
                "count": 4,
                "mode": "serial",
                "batchSize": 2
            },
            "properties": {
                "mode": "Incremental",
                "templateLink": {
                    "uri": "[variables('templatelink')]",
                    "contentVersion": "1.0.0.0"
                },
                "parameters": {
                    "adminUsername": {
                        "value": "[parameters('adminUsername')]"
                    },
                    "adminPassword": {
                        "value": "[parameters('adminPassword')]"
                    },
                    "dnsLabelPrefix": {
                        "value": "[parameters('dnsLabelPrefix')]"
                    },
                    "ubuntuOSVersion": {
                        "value": "[parameters('ubuntuOSVersion')]"
                    },
                    "index":{
                        "value": "[copyIndex()]"
                    }
                }
            }
        }
    ]
}
```

## <a name="property-iteration"></a>속성 반복

toocreate 리소스에 대 한 속성에 대 한 여러 값 추가 `copy` hello 속성 요소에 배열입니다. 이 배열에 개체를 포함 하 고 각 개체에는 다음과 같은 속성 hello:

* 이름-hello 이름에 대 한 여러 값의 hello 속성 toocreate
* -값 toocreate hello 수를 계산
* 입력-hello 값 tooassign toohello 속성을 포함 하는 개체  

hello 방법을 예제와 다음 tooapply `copy` 가상 컴퓨터에서 toohello dataDisks 속성:

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "copy": [{
          "name": "dataDisks",
          "count": 3,
          "input": {
              "lun": "[copyIndex('dataDisks')]",
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

사용 하는 경우 다음에 유의 `copyIndex` 속성 반복 내 hello 반복 hello 이름을 제공 해야 합니다. 리소스 반복와 함께 사용할 경우 tooprovide hello 이름이 없는 합니다.

리소스 관리자 확장 hello `copy` 배포 하는 동안 배열입니다. hello 배열 hello 이름에는 hello 속성의 hello 이름이 됩니다. hello 입력된 값은 hello 개체 속성이 됩니다. 배포 된 hello 템플릿이 됩니다.

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "dataDisks": [
          {
              "lun": 0,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 1,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 2,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

리소스 및 속성 반복을 함께 사용할 수 있습니다. 참조 hello 속성 이름으로 반복 합니다.

```json
{
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[concat(parameters('vnetname'), copyIndex())]",
    "apiVersion": "2016-06-01",
    "copy":{
        "count": 2,
        "name": "vnetloop"
    },
    "location": "[resourceGroup().location]",
    "properties": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "copy": [
            {
                "name": "subnets",
                "count": 2,
                "input": {
                    "name": "[concat('subnet-', copyIndex('subnets'))]",
                    "properties": {
                        "addressPrefix": "[variables('subnetAddressPrefix')[copyIndex('subnets')]]"
                    }
                }
            }
        ]
    }
}
```

각 리소스에 대 한 hello 속성에만 하나의 copy 요소를 포함할 수 있습니다. toospecify 둘 이상의 속성에 대 한 반복 루프는 hello 복사 배열에 있는 여러 개체를 정의 합니다. 각 개체는 개별적으로 반복됩니다. 예를 들어 toocreate 두 hello의 여러 인스턴스 `frontendIPConfigurations` 속성과 hello `loadBalancingRules` 단일 copy 요소에서 두 개체를 정의 하는 부하 분산 장치 속성: 

```json
{
    "name": "[variables('loadBalancerName')]",
    "type": "Microsoft.Network/loadBalancers",
    "properties": {
        "copy": [
          {
              "name": "frontendIPConfigurations",
              "count": 2,
              "input": {
                  "name": "[concat('loadBalancerFrontEnd', copyIndex('frontendIPConfigurations', 1))]",
                  "properties": {
                      "publicIPAddress": {
                          "id": "[variables(concat('publicIPAddressID', copyIndex('frontendIPConfigurations', 1)))]"
                      }
                  }
              }
          },
          {
              "name": "loadBalancingRules",
              "count": 2,
              "input": {
                  "name": "[concat('LBRuleForVIP', copyIndex('loadBalancingRules', 1))]",
                  "properties": {
                      "frontendIPConfiguration": {
                          "id": "[variables(concat('frontEndIPConfigID', copyIndex('loadBalancingRules', 1)))]"
                      },
                      "backendAddressPool": {
                          "id": "[variables('lbBackendPoolID')]"
                      },
                      "protocol": "tcp",
                      "frontendPort": "[variables(concat('frontEndPort' copyIndex('loadBalancingRules', 1))]",
                      "backendPort": "[variables(concat('backEndPort' copyIndex('loadBalancingRules', 1))]",
                      "probe": {
                          "id": "[variables('lbProbeID')]"
                      }
                  }
              }
          }
        ],
        ...
    }
}
```

## <a name="depend-on-resources-in-a-loop"></a>루프의 리소스에 따라 달라짐
리소스 hello를 사용 하 여 다른 리소스 후 배포 된 지정 `dependsOn` 요소입니다. toodeploy 루프에서 리소스의 hello 컬렉션에 종속 된 리소스에는 hello dependsOn 요소에 hello 복사 루프의 hello 이름을 제공 합니다. 다음 예제는 hello toodeploy 배포 하기 전에 3 개의 저장소 계정을 가상 컴퓨터를 hello 하는 방법을 보여 줍니다. 전체 가상 컴퓨터 정의 hello 표시 되지 않습니다. 해당 hello copy 요소 설정 이름이 너무 공지`storagecopy` hello 가상 컴퓨터에 대 한 hello dependsOn 요소 너무 설정`storagecopy`합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        },
        {
            "apiVersion": "2015-06-15", 
            "type": "Microsoft.Compute/virtualMachines", 
            "name": "[concat('VM', uniqueString(resourceGroup().id))]",  
            "dependsOn": ["storagecopy"],
            ...
        }
    ],
    "outputs": {}
}
```

## <a name="create-multiple-instances-of-a-child-resource"></a>자식 리소스의 여러 인스턴스 만들기
자식 리소스에 대해 복사 반복을 사용할 수 없습니다. toocreate 다른 리소스 내에 중첩 된으로 일반적으로 정의 하는 리소스의 여러 인스턴스를 대신 만들어야 해당 리소스를 최상위 리소스로 합니다. Hello 유형 및 이름 속성을 통해 hello 부모 리소스와 hello 관계를 정의 합니다.

예를 들어, 데이터 집합을 데이터 팩터리 내에 자식 리소스로 정의한다고 가정합니다.

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
    "resources": [
    {
        "type": "datasets",
        "name": "exampleDataSet",
        "dependsOn": [
            "exampleDataFactory"
        ],
        ...
    }
}]
```

toocreate 데이터 집합의 여러 인스턴스를 이동 hello 데이터 팩터리 외부에서. hello dataset hello hello 데이터 팩터리로 동일한 수준에 있어야 하지만 hello 데이터 팩터리의 자식 리소스 여전히 쉽습니다. 데이터 집합 및 hello 유형 및 이름 속성을 통해 데이터 팩터리 간의 hello 관계를 유지 합니다. Hello 형식으로 정규화 된 hello 형식을 제공 해야 hello 서식 파일에서 해당 위치에서 형식을 유추할 수 없습니다, 이후: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`합니다.

tooestablish hello 데이터 팩터리의 인스턴스로 부모/자식 관계는 hello 부모 리소스 이름을 포함 하는 hello 데이터 집합에 대 한 이름을 제공 합니다. 형식을 사용 하 여 hello: `{parent-resource-name}/{child-resource-name}`합니다.  

hello 다음 예제는 hello 구현.

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
},
{
    "type": "Microsoft.DataFactory/datafactories/datasets",
    "name": "[concat('exampleDataFactory', '/', 'exampleDataSet', copyIndex())]",
    "dependsOn": [
        "exampleDataFactory"
    ],
    "copy": { 
        "name": "datasetcopy", 
        "count": "3" 
    } 
    ...
}]
```

## <a name="conditionally-deploy-resource"></a>조건부 리소스 배포

toospecify 리소스 배포 여부를 사용 하 여 hello `condition` 요소입니다. 이 요소에 대 한 hello 값 tootrue 또는 false를 확인합니다. Hello 값이 true 이면 hello 리소스 배포 됩니다. Hello 값이 false 이면 hello 리소스 배포 되지 않았습니다. 예를 들어 toospecify 사용 하는지 여부를 새 저장소 계정을 배포 되었거나 기존 저장소 계정을 사용 됩니다.

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

암호 또는 SSH 키 toodeploy 가상 컴퓨터를 사용 하 여 예제를 보려면 [사용자 이름 또는 SSH 조건 템플릿](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json)합니다.

## <a name="next-steps"></a>다음 단계
* 서식 파일의 섹션 hello에 대 한 toolearn 참조 [Azure 리소스 관리자 템플릿 제작](resource-group-authoring-templates.md)합니다.
* toolearn 어떻게 toodeploy 서식 파일에 참조 [Azure 리소스 관리자 템플릿을 사용 하 여 응용 프로그램 배포](resource-group-template-deploy.md)합니다.

