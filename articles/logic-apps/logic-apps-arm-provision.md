---
title: "Azure에서 서식 파일을 사용 하 여 논리 앱 aaaCreate | Microsoft Docs"
description: "워크플로 정의 하기 위한 Azure 리소스 관리자 템플릿 toodeploy 논리 앱을 사용 합니다."
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7574cc7c-e5a1-4b7c-97f6-0cffb1a5d536
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; mandia
ms.openlocfilehash: efbacb534fc7f11e9b593aae4383480ce3a1752f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-logic-app-using-a-template"></a>템플릿을 사용하여 논리 앱 만들기
템플릿은 신속 하 게 toouse 논리 앱 내에서 다른 커넥터를 제공합니다. 논리 앱 toocreate 사용된 toodefine 비즈니스 워크플로 수 있는 논리 앱에 대 한 Azure 리소스 관리자 템플릿을 포함 합니다. 배포 되는 리소스를 정의할 수 있습니다 및 방법을 논리 앱을 배포할 때 toodefine 매개 변수입니다. 실제 비즈니스 시나리오에이 템플릿을 사용 하거나 toomeet 사용자 지정할 수 있습니다 프로그램 요구 사항입니다.

Hello 논리 앱 속성에 대 한 자세한 내용은 참조 하십시오. [논리 앱 워크플로 관리 API](https://msdn.microsoft.com/library/azure/mt643788.aspx)합니다. 

Hello 정의 자체의 예 참조 [작성자 논리 앱 정의](logic-apps-author-definitions.md)합니다. 

템플릿을 만드는 더 자세한 내용은 [Azure 리소스 관리자 템플릿 작성하기](../azure-resource-manager/resource-group-authoring-templates.md)를 참조하십시오.

Hello 전체 서식 파일을 참조 하십시오. [논리 앱 템플릿은](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json)합니다.

## <a name="what-you-deploy"></a>배포할 내용
이 서식 파일로 논리 앱을 배포합니다:

toorun hello 배포는 자동으로 hello 다음 단추를 선택 합니다.  

[![TooAzure 배포](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)

## <a name="parameters"></a>매개 변수
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a>testUri
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-toodeploy"></a>리소스 toodeploy
### <a name="logic-app"></a>논리 앱
Hello 논리 앱을 만듭니다.

hello 템플릿 hello 논리가 응용 프로그램 이름에 대 한 매개 변수 값을 사용 합니다. Hello 논리 앱 toohello의 hello 위치를 설정 하는 것 같은 hello 리소스 그룹 위치입니다. 

이 특정 정의 한 시간에 한 번 실행 하 고 ping hello hello에 지정 된 위치 **testUri** 매개 변수입니다. 

    {
      "type": "Microsoft.Logic/workflows",
      "apiVersion": "2016-06-01",
      "name": "[parameters('logicAppName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "displayName": "LogicApp"
      },
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      }
    }


## <a name="commands-toorun-deployment"></a>명령 toorun 배포
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a>Azure CLI
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



