---
title: "aaaDeploy 웹 응용 프로그램 호스트 이름 및 ssl 인증서와 함께 MSDeploy 사용"
description: "Azure 리소스 관리자 템플릿 toodeploy MSDeploy 사용 하 고 사용자 지정 호스트 이름 및 SSL 인증서를 설정에 웹 응용 프로그램 사용"
services: app-service\web
manager: erikre
documentationcenter: 
author: jodehavi
ms.assetid: 66366a72-cef7-4d75-8779-f4d32ed33cf7
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2016
ms.author: jodehavi
ms.openlocfilehash: ac13f4a7d14ae182e8e7ced5adff30491422d1e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a>MSDeploy, 사용자 지정 호스트 이름 및 SSL 인증서를 사용하여 웹앱 배포
이 가이드에서는 Azure 웹 앱에 대 한 종단 간 배포를 만들기, MSDeploy를 활용 하 여으로 사용자 지정 호스트 이름 및 SSL 인증서 toohello ARM 템플릿을 추가 안내 합니다.

템플릿을 만드는 더 자세한 내용은 [Azure 리소스 관리자 템플릿 작성하기](../azure-resource-manager/resource-group-authoring-templates.md)를 참조하십시오.

### <a name="create-sample-application"></a>응용 프로그램 예제 만들기
ASP.NET 웹 응용 프로그램을 배포하겠습니다. hello 첫 번째 단계는 toocreate 간단한 웹 응용 프로그램 (또는 기존 toouse를 선택할 수 있습니다-이 단계를 건너뛸 수 있는 경우).

Visual Studio 2015를 열고 파일 > 새 프로젝트를 선택합니다. 나타나는 hello 대화 상자에서 웹 선택 > ASP.NET 웹 응용 프로그램입니다. 템플릿 웹 선택한 hello MVC 템플릿을 선택 합니다. 선택 *인증 유형을 변경* 너무*인증 안 함*합니다. Toomake hello 샘플 응용 프로그램만 가능한 한 단순한 것입니다.

이 시점에서 배포 프로세스의 일부로 기본 ASP.Net 웹 응용 프로그램 준비 toouse를 갖습니다.

### <a name="create-msdeploy-package"></a>MSDeploy 패키지 만들기
다음 단계 toocreate hello 패키지 toodeploy hello 웹 응용 프로그램 tooAzure입니다. toodo이 프로젝트를 저장 하 고 hello 명령줄에서 hello 다음을 실행 하는 다음:

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

Hello PackageLocation 폴더 아래의 압축 된 패키지를 만듭니다. hello 응용 프로그램은 이제 Azure 리소스 관리자 템플릿 toodo 아웃 이제 빌드할 수 toobe 배포를 준비 하는 합니다.

### <a name="create-arm-template"></a>ARM 템플릿 만들기
먼저 웹 응용 프로그램 및 호스팅 계획을 만드는 기본 ARM 템플릿을 사용하여 시작해 보겠습니다(매개 변수 및 변수는 간단하게 표시되지 않음).

    {
        "name": "[parameters('appServicePlanName')]",
        "type": "Microsoft.Web/serverfarms",
        "location": "[resourceGroup().location]",
        "apiVersion": "2014-06-01",
        "dependsOn": [ ],
        "tags": {
            "displayName": "appServicePlan"
        },
        "properties": {
            "name": "[parameters('appServicePlanName')]",
            "sku": "[parameters('appServicePlanSKU')]",
            "workerSize": "[parameters('appServicePlanWorkerSize')]",
            "numberOfWorkers": 1
        }
    },
    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        }
    }

다음으로 toomodify hello 웹 응용 프로그램 리소스 tootake 중첩된 MSDeploy 리소스가 필요 합니다. 하면 tooreference hello 패키지 앞에서 만든 되 고 Azure 리소스 관리자 toouse MSDeploy toodeploy hello 패키지 toohello Azure WebApp 지시 합니다. hello 다음 중첩 hello MSDeploy 리소스를 사용 하 여 hello Microsoft.Web/sites 리소스를 보여 줍니다.

    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        },
        "resources": [
            {
                "name": "MSDeploy",
                "type": "extensions",
                "location": "[resourceGroup().location]",
                "apiVersion": "2015-08-01",
                "dependsOn": [
                    "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
                ],
                "tags": {
                    "displayName": "webDeploy"
                },
                "properties": {
                    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]",
                    "dbType": "None",
                    "connectionString": "",
                    "setParameters": {
                        "IIS Web Application Name": "[variables('webAppName')]"
                    }
                }
            }
        ]
    }

이제 해당 hello MSDeploy 리소스 사용을 확인할 수 있습니다는 **packageUri** 다음과 같이 정의 된 속성:

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

이 **packageUri** 사용 하 여 패키지 zip을 업로드 toohello 저장소 계정을 가리키는 저장소 계정 uri hello 합니다. hello Azure 리소스 관리자를 활용 [공유 액세스 서명](../storage/common/storage-dotnet-shared-access-signature-part-1.md) hello 서식 파일을 배포할 때 hello 저장소 계정에서 로컬로 아래로 toopull hello 패키지 합니다. 이 프로세스를 자동화 하 여 hello 패키지를 업로드 하 고 필요한 hello Azure 관리 API toocreate hello 키 호출 되며 이러한 hello 템플릿 매개 변수로 전달 하는 PowerShell 스크립트를 통해 됩니다 (*_artifactsLocation* 및 *_artifactsLocationSasToken*). Hello 폴더에 대 한 toodefine 매개 변수가 필요 하며 filename hello 패키지는 업로드 된 toounder hello 저장소 컨테이너입니다.

다음 또 다른 중첩 된 리소스 toosetup hello 호스트 이름 바인딩 tooleverage 사용자 지정 도메인에에서 tooadd를 해야합니다. 소유권을 Azure에서 첫 번째 필요 tooensure hello 호스트 이름을 소유 하 고 toobe 설정 확인-참조는 [Azure 앱 서비스에서 사용자 지정 도메인 이름을 구성](app-service-web-tutorial-custom-domain.md)합니다. 이 작업을 마쳤으면 hello Microsoft.Web/sites 리소스 섹션 아래에서 tooyour 템플릿을 다음 hello를 추가할 수 있습니다.

    {
        "apiVersion": "2015-08-01",
        "type": "hostNameBindings",
        "name": "www.yourcustomdomain.com",
        "dependsOn": [
            "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
        ],
        "properties": {
            "domainId": null,
            "hostNameType": "Verified",
            "siteName": "variables('webAppName')"
        }
    }

마지막으로 tooadd 다른 최상위 리소스에서 Microsoft.Web/certificates 있어야 합니다. 이 리소스 SSL 인증서 있고 hello 동일 수준 웹 앱으로 이동 하 고 호스팅 계획에 존재 합니다.

    {
        "name": "[parameters('certificateName')]",
        "apiVersion": "2014-04-01",
        "type": "Microsoft.Web/certificates",
        "location": "[resourceGroup().location]",
        "properties": {
            "pfxBlob": "pfx base64 blob",
            "password": "some pass"
        }
    }

Toohave이이 리소스를 순서 tooset에 유효한 SSL 인증서가 필요 합니다. 유효한 해당 인증서를 수행한 다음 해야 tooextract hello pfx 바이트 base64 문자열. 한 가지 옵션 tooextract이는 다음 PowerShell 명령을 toouse hello:

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

이 매개 변수 tooyour ARM 배포 템플릿으로 전달할 수 있습니다.

이 시점에서 hello ARM 템플릿이 준비 되었습니다.

### <a name="deploy-template"></a>템플릿 배포
마지막 단계는 hello는 toopiece이 모두 함께 전체에 종단 간 배포에 합니다. hello를 활용할 수 있습니다 더 쉽게 toomake 배포 **deploy-azureresourcegroup.ps1 스크립트로** 에 필요한 모든 아티팩트를 업로드와 toohelp Visual Studio에서에서 Azure 리소스 그룹 프로젝트를 만들 때 추가 된 PowerShell 스크립트 hello 템플릿입니다. Toohave toouse 보다 앞선 시간을 원하는 저장소 계정을 만든 필요 합니다. 예를 들어 hello package.zip toobe 업로드에 대 한 공유 저장소 계정을 만들었습니다. hello 스크립트 AzCopy tooupload hello 패키지 toohello 저장소 계정을 활용 됩니다. 아티팩트 폴더 위치에 전달 하 고 hello 스크립트 저장소 컨테이너 이름이 해당 디렉터리 toohello 내의 모든 파일을 자동으로 업로드 합니다. Deploy-azureresourcegroup.ps1 스크립트로 호출한 후 SSL 인증서와 함께 toothen 업데이트 hello SSL 바인딩 toomap hello 사용자 지정 호스트 이름이 있어야 합니다.

다음 PowerShell 표시 hello hello 배포 hello을 호출 하는 완전 한 배포-AzureResourceGroup.ps1:

    #Set resource group name
    $rgName = "Name-of-resource-group"

    #call deploy-azureresourcegroup script toodeploy web app

    .\Deploy-AzureResourceGroup.ps1 -ResourceGroupLocation "East US" `
                                    -ResourceGroupName $rgName `
                                    -UploadArtifacts `
                                    -StorageAccountName "name-of-storage-acct-for-package" `
                                    -StorageAccountResourceGroupName "resource-group-name-storage-acct" `
                                    -TemplateFile "web-app-deploy.json" `
                                    -TemplateParametersFile "web-app-deploy-parameters.json" `
                                    -ArtifactStagingDirectory "C:\path\to\packagefolder\"

    #update web app toobind ssl certificate toohostname. This has toobe done after creation above.

    $cert = Get-PfxCertificate -FilePath C:\path\to\certificate.pfx

    $ar = Get-AzureRmResource -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -ApiVersion 2014-11-01

    $props = $ar.Properties

    $props.HostNameSslStates[2].'SslState' = 1
    $props.HostNameSslStates[2].'thumbprint' = $cert.Thumbprint
    $props.hostNameSslStates[2].'toUpdate' = $true

    Set-AzureRmResource -ApiVersion 2014-11-01 -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -PropertyObject $props

이 시점에서 응용 프로그램은 배포 된 및 https://www.yourcustomdomain.com 통해 수 toobrowse tooit 있어야 합니다.

