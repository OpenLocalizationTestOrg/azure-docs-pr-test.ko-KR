---
title: "웹 응용 프로그램이 aaaDeploy tooa GitHub 리포지토리 연결 | Microsoft Docs"
description: "Azure 리소스 관리자 템플릿 toodeploy GitHub 리포지토리에서 프로젝트를 포함 하는 웹 앱을 사용 합니다."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 32739607-85fe-43c8-a4dc-1feb46d93a4d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: cephalin
ms.openlocfilehash: 8b23416c4c06a60991517e6ee4cd82bebc5a9d73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-linked-tooa-github-repository"></a>웹 응용 프로그램 연결 tooa GitHub 리포지토리를 배포 합니다.
이 항목은 웹 앱을 배포 하는 Azure 리소스 관리자 템플릿을 toocreate GitHub 리포지토리에 tooa 프로젝트를 연결 하는 방법을 배웁니다. 에 대해 설명 합니다 방법을 toodefine 리소스 배포 되 고 toodefine 매개 변수를 hello 배포를 실행 하는 경우 지정 된 합니다. 배포를 위한이 서식 파일을 사용 하거나 toomeet 사용자 지정할 수 있습니다 프로그램 요구 사항입니다.

템플릿을 만드는 더 자세한 내용은 [Azure 리소스 관리자 템플릿 작성하기](../azure-resource-manager/resource-group-authoring-templates.md)를 참조하십시오.

Hello 전체 서식 파일을 참조 하십시오. [응용 프로그램에 연결 된 웹 tooGitHub 템플릿](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json)합니다.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a>배포할 내용
이 템플릿을 사용 하 여 GitHub의 프로젝트에서 hello 코드를 포함 하는 웹 앱을 배포 합니다.

toorun 배포를 자동으로 hello, hello 다음 단추를 클릭 합니다.

[![TooAzure 배포](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)

## <a name="parameters"></a>매개 변수
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a>repoURL
hello 프로젝트 toodeploy 포함 된 GitHub 리포지토리에 대 한 hello URL입니다. 이 매개 변수에 기본값을 포함 하지만이 값은 의도 한 tooshow만 하면 tooprovide 저장소에 대 한 URL을 hello 하는 방법입니다. Hello 템플릿 있지만 테스트는 하려면 tooprovide hello URL 사용자 고유의 저장소 hello 템플릿을 사용 하 여 작업 하는 경우이 값을 사용할 수 있습니다.

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a>분기
hello 분기 hello 리포지토리 toouse hello 응용 프로그램을 배포 하는 경우입니다. hello 기본값은 master, 하지만 toodeploy 한다고 hello 리포지토리의 모든 분기의 hello 이름을 제공할 수 있습니다.

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-toodeploy"></a>리소스 toodeploy
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a>웹앱
GitHub에 연결 된 toohello 프로젝트가 hello 웹 앱을 만듭니다. 

Hello 통해 hello 웹 응용 프로그램의 hello 이름을 지정 하면 **siteName** 매개 변수 및 hello 통해 hello 웹 응용 프로그램의 hello 위치 **siteLocation** 매개 변수입니다. Hello에 **dependsOn** 요소 hello 템플릿 hello 웹 응용 프로그램 호스팅 계획 hello 서비스에 종속로 정의 합니다. 호스팅 계획 hello에 의존 하므로 hello 웹 앱 호스팅 계획 hello 생성이 완료 될 때까지 생성 되지 않습니다. hello **dependsOn** 요소는 사용 되는 toospecify 배포 순서일 뿐입니다. Hello 호스팅 계획에 종속으로 hello 웹 앱으로 표시 하면 Azure 리소스 관리자는 시도 toocreate 리소스가 모두 hello에서 동일한 시간 및 오류 메시지가 나타날 수 hello 호스팅 계획 하기 전에 hello 웹 응용 프로그램을 만들면 됩니다.

hello 웹 응용 프로그램에 정의 된 자식 리소스에 **리소스** 아래 섹션. 이 자식 리소스 hello 웹 앱을 사용 하 여 배포 된 hello 프로젝트에 대 한 소스 제어를 정의 합니다. 이 서식 파일에서 hello 소스 제어 연결된 tooa 특정 GitHub 리포지토리 됩니다. hello GitHub 리포지토리 hello 코드를 사용 하 여 정의 **"RepoUrl": "https://github.com/davidebbo-test/Mvc52Application.git"** toocreate 반복적으로 배포 하는 템플릿을 원하는 경우에 하드 코딩 hello 리포지토리 URL을 수 있습니다는 hello 최소 매개 변수 개수를 요구 하는 동안 단일 프로젝트입니다.
리포지토리 URL을 hello 하드 코딩 하는 대신, hello 리포지토리 URL에 대 한 매개 변수를 추가 하 고 해당 값을 사용 하 여 hello에 대 한 **RepoUrl** 속성입니다.

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
      ],
      "properties": {
        "serverFarmId": "[parameters('hostingPlanName')]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/Sites', parameters('siteName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('repoURL')]",
            "branch": "[parameters('branch')]",
            "IsManualIntegration": true
          }
        }
      ]
    }

## <a name="commands-toorun-deployment"></a>명령 toorun 배포
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a>Azure CLI

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a>Azure CLI 2.0

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> Hello 매개 변수에 JSON 파일의 콘텐츠에 대 한 참조 [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json)합니다.
>
>

