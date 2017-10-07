---
title: "Azure 리소스에 대 한 배포 순서 aaaSet | Microsoft Docs"
description: "설명 hello 올바른 순서로 tooset 하나의 리소스 배포 tooensure 리소스 중 다른 리소스에 종속으로 배포 되는 방법입니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 34ebaf1e-480c-4b4d-9bf6-251bd3f8f2cf
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: tomfitz
ms.openlocfilehash: 2f658f4c85236966c46b34a65aafb8426c92806c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="define-hello-order-for-deploying-resources-in-azure-resource-manager-templates"></a>Azure 리소스 관리자 템플릿의 리소스를 배포 하기 위한 hello 순서 정의
지정된 된 리소스에 대 한 hello 리소스를 배포 하기 전에 있어야 하는 다른 리소스가 있을 수 있습니다. 예를 들어 SQL server toodeploy SQL 데이터베이스를 시도 하기 전에 존재 해야 합니다. 다른 리소스에이 관계 hello에 종속으로 한 리소스를 표시 하 여 정의 합니다. Hello로 종속성 정의 **dependsOn** 요소 또는 hello를 사용 하 여 **참조** 함수입니다. 

리소스 관리자 리소스 간의 종속성을 hello 평가 하 고 종속 순서에 배포 합니다. 리소스가 서로 종속되어 있지 않은 경우 Resource Manager는 이를 병렬로 배포합니다. Hello에 배포 되는 리소스에 대 한 toodefine 종속성만 하면 같은 서식 파일입니다. 

## <a name="dependson"></a>dependsOn
서식 파일에 내 hello dependsOn 요소 활성화 하면 toodefine 하나의 리소스 하나 이상의 리소스에 의존 하는입니다. 값은 리소스 이름의 쉼표로 구분된 목록일 수 있습니다. 

hello 다음 예제에서는 부하 분산 장치, 가상 네트워크 및 저장소 계정을 여러 개 만드는 루프에 의존 하는 가상 컴퓨터 크기 집합 이러한 다른 리소스는 다음 예제를 hello에 표시 되지 않습니다 되지만 tooexist hello 서식 파일의 다른 위치에서 필요한 것입니다.

```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "name": "[variables('namingInfix')]",
  "location": "[variables('location')]",
  "apiVersion": "2016-03-30",
  "tags": {
    "displayName": "VMScaleSet"
  },
  "dependsOn": [
    "[variables('loadBalancerName')]",
    "[variables('virtualNetworkName')]",
    "storageLoop",
  ],
  ...
}
```

앞 예제는 hello, 종속성 라는 복사 루프를 통해 만들어진 hello 리소스에 포함 되어 **storageLoop**합니다. 예제는 [Azure 리소스 관리자에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요.

종속성을 정의할 때는 hello 리소스 공급자 네임 스페이스 및 리소스 유형을 tooavoid 모호성을 포함할 수 있습니다. 부하 분산 장치 및 hello 다른 리소스를 사용 하 여 hello 다음 동일한 이름을 가질 수 있는 가상 네트워크 형식 tooclarify 예를 들어:

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

저장할된 toouse dependsOn toomap 관계 수 있습니다 프로그램 리소스 간의 중요 한 toounderstand 하 고 이유는. 예를 들어, 리소스는 연결 되는 방식 toodocument dependsOn 않습니다 hello 적합 한 접근 방식을. 배포 후 리소스 hello dependsOn 요소에 정의 된 쿼리할 수 없습니다. dependsOn을 사용하면 Resource Manager는 종속성이 있는 두 리소스를 병렬로 배포하지 않으므로 배포 시간에 잠재적으로 영향을 줍니다. toodocument 관계 리소스를 대신 사용 하 여 [리소스를 연결](/rest/api/resources/resourcelinks)합니다.

## <a name="child-resources"></a>자식 리소스
hello 리소스 속성 정의 하 고 관련된 toohello 리소스 toospecify 자식 리소스가 있습니다. 자식 리소스는 5개 수준 깊이까지만 정의할 있습니다. 암시적 종속성이 없어서 toonote hello 부모 리소스와 자식 리소스 간에 만들어진 유용 합니다. 자식 리소스 toobe hello 부모 리소스 후 배포 된 hello 필요, 해당 종속성 hello dependsOn 속성으로 명시적 해야 합니다. 

각 부모 리소스는 특정 리소스 종류만 자식 리소스로 허용합니다. 리소스 종류 hello에 지정 된 hello 허용 [템플릿 스키마](https://github.com/Azure/azure-resource-manager-schemas) hello 부모 리소스의 합니다. 자식 리소스 종류의 hello 이름 같은 hello 부모 리소스 종류의 hello 이름이 포함 됩니다 **Microsoft.Web/sites/config** 및 **Microsoft.Web/sites/extensions** hello 의자식리소스가두 **Microsoft.Web/sites**합니다.

다음 예제는 hello SQL server와 SQL 데이터베이스를 보여 줍니다. Hello 데이터베이스 hello 서버의 자식인 경우에 명시적 종속성 hello SQL 데이터베이스와 SQL server에 정의 되어 있는지 확인 합니다.

```json
"resources": [
  {
    "name": "[variables('sqlserverName')]",
    "type": "Microsoft.Sql/servers",
    "location": "[resourceGroup().location]",
    "tags": {
      "displayName": "SqlServer"
    },
    "apiVersion": "2014-04-01-preview",
    "properties": {
      "administratorLogin": "[parameters('administratorLogin')]",
      "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
    },
    "resources": [
      {
        "name": "[parameters('databaseName')]",
        "type": "databases",
        "location": "[resourceGroup().location]",
        "tags": {
          "displayName": "Database"
        },
        "apiVersion": "2014-04-01-preview",
        "dependsOn": [
          "[variables('sqlserverName')]"
        ],
        "properties": {
          "edition": "[parameters('edition')]",
          "collation": "[parameters('collation')]",
          "maxSizeBytes": "[parameters('maxSizeBytes')]",
          "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
        }
      }
    ]
  }
]
```

## <a name="reference-function"></a>reference 함수
hello [함수를 참조](resource-group-template-functions-resource.md#reference) 식 tooderive 다른 JSON 이름 및 값 쌍 이나 런타임 리소스에서 해당 값을 사용 합니다. 참조 식은 한 리소스가 다른 리소스에 종속되어 있음을 암시적으로 선언합니다. hello 일반 형식은 다음과 같습니다.

```json
reference('resourceName').propertyPath
```

다음 예제는 hello에서 CDN 끝점 hello CDN 프로필을 명시적으로 의존 하 고 암시적으로 웹 응용 프로그램에 따라 달라 집니다.

```json
{
    "name": "[variables('endpointName')]",
    "type": "endpoints",
    "location": "[resourceGroup().location]",
    "apiVersion": "2016-04-02",
    "dependsOn": [
            "[variables('profileName')]"
    ],
    "properties": {
        "originHostHeader": "[reference(variables('webAppName')).hostNames[0]]",
        ...
    }
```

이 요소 또는 hello dependsOn 요소 toospecify 종속성을 사용할 수 있지만 hello에 대 한 불필요 toouse 모두 같은 종속 리소스입니다. 가능 하면 불필요 한 종속성을 추가 하는 암시적 참조 tooavoid를 사용 합니다.

toolearn 더 참조 [함수를 참조](resource-group-template-functions-resource.md#reference)합니다.

## <a name="recommendations-for-setting-dependencies"></a>종속성 설정 권장 사항

어떤 종속성 tooset를 결정할 때는 hello 지침을 사용 합니다.

* 종속성을 최대한 적게 설정합니다.
* 자식 리소스가 부모 리소스에 종속되도록 설정합니다.
* 사용 하 여 hello **참조** tooshare 속성을 필요로 하는 리소스 간의 암시적 종속성 tooset 작동 합니다. 암시적 종속성을 이미 정의한 경우에는 명시적 종속성(**dependsOn**)을 추가하지 않습니다. 이 방법의 불필요 한 종속 hello 위험을 줄입니다. 
* 다른 리소스의 기능을 사용하지 않고 리소스를 **만들** 수 없는 경우 종속성을 설정합니다. 배포 후에 hello 리소스만 상호 작용 하는 경우에 종속성을 설정 하지 마십시오.
* 종속성을 명시적으로 설정하지 않고 계단식으로 배열되도록 합니다. 예를 들어 가상 컴퓨터가 가상 네트워크 인터페이스에 따라 달라 집니다 및 hello 가상 네트워크 인터페이스를 가상 네트워크와 공용 IP 주소에 따라 달라 집니다. 따라서 hello 가상 컴퓨터가 배포 된 모든 세 가지 리소스 있지만 모든 세 가지 리소스에 종속으로 hello 가상 컴퓨터를 명시적으로 설정 하지 마십시오. 이 방법은 hello 종속성 순서를 명확히 고 보다 쉽게 toochange hello 템플릿 나중에 있습니다.
* 값을 확인할 수 없는 배포 하기 전에 한 종속성 없이 hello 리소스를 배포 하십시오. 예를 들어 구성 값 hello 이름 다른 리소스의 경우, 종속성이 필요 하지 수도 있습니다. 이 설명서는 일부 리소스가 있는지 확인 합니다. hello hello 다른 리소스 때문에 항상 작동 하지 않습니다. 오류가 표시되면 종속성을 추가합니다. 

Resource Manager는 템플릿의 유효성을 검사하는 동안 순환적 종속성을 식별합니다. 순환 종속성이 존재 한다는 오류가 나타나면 템플릿 toosee 있는지 여부를 평가할 종속성은 필요 하지 않으며 제거할 수 있습니다. 종속성 제거 작동 하지 않는 경우에 일부 배포 작업 후 hello 순환 종속성을 포함 하는 hello 리소스가 배포 되는 자식 리소스를 이동 하 여 순환 종속성을 방지할 수 있습니다. 예를 들어, 두 가상 컴퓨터를 배포 하는 하지만 다른 toohello 참조 하는 각 항목에 속성을 설정 해야 합니다. 순서에 따라 hello에 배포할 수 있습니다.

1. vm1
2. vm2
3. vm1의 확장은 vm1 및 vm2에 종속됩니다. hello 확장 v m 2에서 가져오는 v m 1의 값을 설정 합니다.
4. vm2의 확장은 vm1 및 vm2에 종속됩니다. hello 확장 v m 1에서 가져오는 v m 2에 값을 설정 합니다.

Hello 배포 순서를 평가 하 고 종속성 오류를 해결 하는 방법에 대 한 정보를 참조 하십시오. [Azure 리소스 관리자와 일반적인 Azure 배포 오류 문제 해결](resource-manager-common-deployment-errors.md)합니다.

## <a name="next-steps"></a>다음 단계
* 배포 하는 동안 종속성 문제를 해결 하는 방법에 대 한 toolearn 참조 [Azure 리소스 관리자와 일반적인 Azure 배포 오류 문제 해결](resource-manager-common-deployment-errors.md)합니다.
* Azure 리소스 관리자 템플릿을 만드는 방법에 대해 toolearn 참조 [템플릿을 작성](resource-group-authoring-templates.md)합니다. 
* 목록이 hello 서식 파일에 사용할 수 있는 함수에 대 한 참조 [템플릿 함수](resource-group-template-functions.md)합니다.

