---
title: "Azure 함수에서 함수 응용 프로그램에 대 한 리소스 배포 aaaAutomate | Microsoft Docs"
description: "자세한 내용은 방법 toobuild 함수 앱을 배포 하는 Azure 리소스 관리자 템플릿 합니다."
services: Functions
documtationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 함수, 서버 없는 아키텍처, 코드로서의 인프라, Azure Resource Manager"
ms.assetid: d20743e3-aab6-442c-a836-9bcea09bfd32
ms.server: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: b0df0d4ef9fe93213f7b1cb1d1e6b4e14f8b3a30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a>Azure Functions의 함수 앱에 대한 리소스 배포 자동화

Azure 리소스 관리자 템플릿 toodeploy 함수 응용 프로그램을 사용할 수 있습니다. 이 문서에서는 hello 필요한 리소스 및 작업에 대 한 매개 변수를 설명 합니다. Hello에 따라 toodeploy 추가 리소스를 할 수 있습니다 [트리거 및 바인딩](functions-triggers-bindings.md) 함수 응용 프로그램에서 합니다.

템플릿을 만드는 더 자세한 내용은 [Azure Resource Manager 템플릿 작성하기](../azure-resource-manager/resource-group-authoring-templates.md)를 참조하십시오.

샘플 템플릿은 다음을 참조하세요.
- [소비 계획의 함수 앱]
- [Azure App Service 계획의 함수 앱]

## <a name="required-resources"></a>필요한 리소스

함수 앱에는 다음 리소스가 필요합니다.

* [Azure Storage](../storage/index.md) 계정
* 호스팅 계획(소비 계획 또는 App Service 계획)
* 함수 앱 

### <a name="storage-account"></a>저장소 계정

함수 앱에는 Azure Storage 계정이 필요합니다. Blob, 테이블, 큐 및 파일을 지원하는 일반 용도의 계정이 있어야 합니다. 자세한 내용은 [Azure Functions 저장소 계정 요구 사항](functions-create-function-app-portal.md#storage-account-requirements)을 참조하세요.

```json
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2015-06-15",
    "location": "[resourceGroup().location]",
    "properties": {
        "accountType": "[parameters('storageAccountType')]"
    }
}
```

또한 속성을 hello `AzureWebJobsStorage` 및 `AzureWebJobsDashboard` hello 사이트 구성에서 응용 프로그램 설정으로 지정 해야 합니다. hello Azure 함수 런타임은 hello를 사용 하 여 `AzureWebJobsStorage` 연결 문자열 toocreate 내부 큐. 연결 문자열 hello `AzureWebJobsDashboard` 는 사용 되는 toolog tooAzure 테이블 저장소 및 전원 hello **모니터** hello 포털에서 탭 합니다.

이러한 속성은 hello에 지정 된 `appSettings` hello에 대 한 컬렉션 `siteConfig` 개체:

```json
"appSettings": [
    {
        "name": "AzureWebJobsStorage",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    },
    {
        "name": "AzureWebJobsDashboard",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    }
```    

### <a name="hosting-plan"></a>호스팅 계획

hello 호스팅 계획의 hello 정의 소비 또는 앱 서비스 계획을 사용 하는지에 따라 달라 집니다. 참조 [hello 소비 계획에는 함수 앱을 배포할](#consumption) 및 [hello 앱 서비스 계획에는 함수 앱을 배포할](#app-service-plan)합니다.

### <a name="function-app"></a>함수 앱

hello 함수 응용 프로그램 리소스 유형의 리소스를 사용 하 여 정의 된 **Microsoft.Web/Site** 종류 및 **functionapp**:

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ]
```

<a name="consumption"></a>

## <a name="deploy-a-function-app-on-hello-consumption-plan"></a>Hello 소비 계획에 함수 앱 배포

두 가지 모드로 함수 응용 프로그램을 실행할 수 있습니다: hello 소비 계획과 hello 앱 서비스 계획 합니다. hello 소비 계획 코드 실행 되 고 필요한 toohandle 부하로 하 여 확장 하 고 그런 다음 코드를 실행 중이지 않을 때 확장 하는 경우 계산 능력을 자동으로 할당 합니다. 따라서 유휴 Vm에 대 한 toopay 없는 바뀌고 없는 tooreserve 용량 미리. 호스팅 계획에 대 한 더 toolearn 참조 [Azure 함수 소비와 앱 서비스 계획](functions-scale.md)합니다.

샘플 Azure Resource Manager 템플릿은 [소비 계획의 함수 앱]을 참조하세요.

### <a name="create-a-consumption-plan"></a>소비 계획 만들기

소비 계획은 특수한 유형의 "서버 팜" 리소스입니다. Hello를 사용 하 여 지정 `Dynamic` hello에 대 한 값 `computeMode` 및 `sku` 속성:

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "computeMode": "Dynamic",
        "sku": "Dynamic"
    }
}
```

### <a name="create-a-function-app"></a>함수 앱 만들기

또한 소비 계획 요구 hello 사이트 구성의 두 가지 추가 설정을: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` 및 `WEBSITE_CONTENTSHARE`합니다. 이러한 속성 hello 저장소 계정 및 파일 경로 hello 함수 응용 프로그램 코드와 구성이 저장 되는 위치를 구성 합니다.

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ],
    "properties": {
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "siteConfig": {
            "appSettings": [
                {
                    "name": "AzureWebJobsDashboard",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "AzureWebJobsStorage",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTAZUREFILECONNECTIONSTRING",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTSHARE",
                    "value": "[toLower(variables('functionAppName'))]"
                },
                {
                    "name": "FUNCTIONS_EXTENSION_VERSION",
                    "value": "~1"
                }
            ]
        }
    }
}
```                    

<a name="app-service-plan"></a> 

## <a name="deploy-a-function-app-on-hello-app-service-plan"></a>앱 서비스 계획 hello에 함수 앱 배포

앱 서비스 계획 hello 함수 앱은 Basic, Standard 및 Premium Sku 비슷한 tooweb 앱에 전용된 Vm에서 실행 됩니다. 앱 서비스 계획 hello 작동 하는 방법에 대 한 자세한 내용은 참조 hello [Azure 앱 서비스 계획 심도 깊은 개요](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)합니다. 

샘플 Azure Resource Manager 템플릿은 [Azure App Service 계획의 함수 앱]을 참조하세요.

### <a name="create-an-app-service-plan"></a>App Service 계획 만들기

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "sku": "[parameters('sku')]",
        "workerSize": "[parameters('workerSize')]",
        "hostingEnvironment": "",
        "numberOfWorkers": 1
    }
}
```

### <a name="create-a-function-app"></a>함수 앱 만들기 

규모 조정 옵션을 선택한 후에는 함수 앱을 만듭니다. hello 응용 프로그램은 모든 기능을 보유 하는 hello 컨테이너입니다.

함수 앱에는 앱 설정 및 소스 제어 옵션을 포함하여 배포에 사용할 수 있는 자식 리소스가 많이 있습니다. Tooremove hello 선택할 수 **sourcecontrols** 자식 리소스 및 사용 하 여 다른 [배포 옵션](functions-continuous-deployment.md) 대신 합니다.

> [!IMPORTANT]
> Azure 리소스 관리자를 사용 하 여 응용 프로그램을 배포 하는 toosuccessfully에 중요 한 toounderstand 리소스가 Azure에 배포 되는 방식을 합니다. 다음 예제는 hello에서 최상위 구성이 사용 하 여 적용 되는 **siteConfig**합니다. 정보 toohello 함수 런타임 및 배포 엔진 전달 때문 중요 tooset top에 이러한 구성 수준입니다. Hello 자식 항목 전에 최상위 정보가 필요 **sourcecontrols/웹** 리소스 적용 됩니다. 이러한 설정을 하위 수준 hello 가능한 tooconfigure 있지만 **구성/appSettings** 함수 앱을 배포 해야 하는 일부 경우에 리소스 *전에* **구성/appSettings**  적용 됩니다. 예를 들어 [Logic Apps](../logic-apps/index.md)에서 함수를 사용하는 경우 함수는 다른 리소스의 종속성입니다.

```json
{
  "apiVersion": "2015-08-01",
  "name": "[parameters('appName')]",
  "type": "Microsoft.Web/sites",
  "kind": "functionapp",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Web/serverfarms', parameters('appName'))]"
  ],
  "properties": {
     "serverFarmId": "[variables('appServicePlanName')]",
     "siteConfig": {
        "alwaysOn": true,
        "appSettings": [
            { "name": "FUNCTIONS_EXTENSION_VERSION", "value": "~1" },
            { "name": "Project", "value": "src" }
        ]
     }
  },
  "resources": [
     {
        "apiVersion": "2015-08-01",
        "name": "appsettings",
        "type": "config",
        "dependsOn": [
          "[resourceId('Microsoft.Web/Sites', parameters('appName'))]",
          "[resourceId('Microsoft.Web/Sites/sourcecontrols', parameters('appName'), 'web')]",
          "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
        ],
        "properties": {
          "AzureWebJobsStorage": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]",
          "AzureWebJobsDashboard": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
        }
     },
     {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/sites/', parameters('appName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('sourceCodeRepositoryURL')]",
            "branch": "[parameters('sourceCodeBranch')]",
            "IsManualIntegration": "[parameters('sourceCodeManualIntegration')]"
          }
     }
  ]
}
```
> [!TIP]
> 이 템플릿은 hello를 사용 하 여 [프로젝트](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) hello 기본 디렉터리는 hello 함수 배포 엔진 (Kudu)는 배포 가능한 코드에 대 한 검색을 설정 하는 응용 프로그램 설정 값입니다. 이 리포지토리에 우리의 함수 hello의 하위 폴더에서는 **src** 폴더입니다. 따라서 앞 예제는 hello, 설정 hello 응용 프로그램 설정 값 너무`src`합니다. 기능은 여 저장소의 루트 hello에에서 또는 소스 제어에서 배포 하지 않는 경우이 응용 프로그램 설정 값을 제거할 수 있습니다.

## <a name="deploy-your-template"></a>템플릿 배포

다음 방법으로 toodeploy hello의 서식 파일에 사용할 수 있습니다.:

* [PowerShell](../azure-resource-manager/resource-group-template-deploy.md)
* [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [Azure Portal](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [REST API](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-tooazure-button"></a>배포 tooAzure 단추

대체 ```<url-encoded-path-to-azuredeploy-json>``` 와 [URL로 인코딩된](https://www.bing.com/search?q=url+encode) 의 hello 원시 경로 버전 프로그램 `azuredeploy.json` GitHub의 파일에에서 있습니다.

markdown을 사용하는 예는 다음과 같습니다.

```markdown
[![Deploy tooAzure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

HTML을 사용하는 예는 다음과 같습니다.

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a>다음 단계

에 대 한 자세한 방법에 대 한 toodevelop 및 Azure 기능을 구성 합니다.

* [Azure Functions 개발자 참조](functions-reference.md)
* [어떻게 tooconfigure Azure 작동 앱 설정](functions-how-to-use-azure-function-app-settings.md)
* [첫 번째 Azure Function 만들기](functions-create-first-azure-function.md)

<!-- LINKS -->

[소비 계획의 함수 앱]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json
[Azure App Service 계획의 함수 앱]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json
