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
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a><span data-ttu-id="c6e35-103">MSDeploy, 사용자 지정 호스트 이름 및 SSL 인증서를 사용하여 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="c6e35-103">Deploy a web app with MSDeploy, custom hostname and SSL certificate</span></span>
<span data-ttu-id="c6e35-104">이 가이드에서는 Azure 웹 앱에 대 한 종단 간 배포를 만들기, MSDeploy를 활용 하 여으로 사용자 지정 호스트 이름 및 SSL 인증서 toohello ARM 템플릿을 추가 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-104">This guide walks through creating an end-to-end deployment for an Azure Web App, leveraging MSDeploy as well as adding a custom hostname and an SSL certificate toohello ARM template.</span></span>

<span data-ttu-id="c6e35-105">템플릿을 만드는 더 자세한 내용은 [Azure 리소스 관리자 템플릿 작성하기](../azure-resource-manager/resource-group-authoring-templates.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="c6e35-105">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

### <a name="create-sample-application"></a><span data-ttu-id="c6e35-106">응용 프로그램 예제 만들기</span><span class="sxs-lookup"><span data-stu-id="c6e35-106">Create Sample Application</span></span>
<span data-ttu-id="c6e35-107">ASP.NET 웹 응용 프로그램을 배포하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-107">You will be deploying an ASP.NET web application.</span></span> <span data-ttu-id="c6e35-108">hello 첫 번째 단계는 toocreate 간단한 웹 응용 프로그램 (또는 기존 toouse를 선택할 수 있습니다-이 단계를 건너뛸 수 있는 경우).</span><span class="sxs-lookup"><span data-stu-id="c6e35-108">hello first step is toocreate a simple web application (or you could choose toouse an existing one - in which case you can skip this step).</span></span>

<span data-ttu-id="c6e35-109">Visual Studio 2015를 열고 파일 > 새 프로젝트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-109">Open Visual Studio 2015 and choose File > New Project.</span></span> <span data-ttu-id="c6e35-110">나타나는 hello 대화 상자에서 웹 선택 > ASP.NET 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-110">On hello dialog that appears choose Web > ASP.NET Web Application.</span></span> <span data-ttu-id="c6e35-111">템플릿 웹 선택한 hello MVC 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-111">Under Templates choose Web and choose hello MVC template.</span></span> <span data-ttu-id="c6e35-112">선택 *인증 유형을 변경* 너무*인증 안 함*합니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-112">Select *Change authentication type* too*No Authentication*.</span></span> <span data-ttu-id="c6e35-113">Toomake hello 샘플 응용 프로그램만 가능한 한 단순한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-113">This is just toomake hello sample application as simple as possible.</span></span>

<span data-ttu-id="c6e35-114">이 시점에서 배포 프로세스의 일부로 기본 ASP.Net 웹 응용 프로그램 준비 toouse를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-114">At this point you will have a basic ASP.Net web app ready toouse as part of your deployment process.</span></span>

### <a name="create-msdeploy-package"></a><span data-ttu-id="c6e35-115">MSDeploy 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="c6e35-115">Create MSDeploy package</span></span>
<span data-ttu-id="c6e35-116">다음 단계 toocreate hello 패키지 toodeploy hello 웹 응용 프로그램 tooAzure입니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-116">Next step is toocreate hello package toodeploy hello web app tooAzure.</span></span> <span data-ttu-id="c6e35-117">toodo이 프로젝트를 저장 하 고 hello 명령줄에서 hello 다음을 실행 하는 다음:</span><span class="sxs-lookup"><span data-stu-id="c6e35-117">toodo this, save your project and then run hello following from hello command line:</span></span>

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

<span data-ttu-id="c6e35-118">Hello PackageLocation 폴더 아래의 압축 된 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-118">This will create a zipped package under hello PackageLocation folder.</span></span> <span data-ttu-id="c6e35-119">hello 응용 프로그램은 이제 Azure 리소스 관리자 템플릿 toodo 아웃 이제 빌드할 수 toobe 배포를 준비 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-119">hello application is now ready toobe deployed, which you can now build out an Azure Resource Manager template toodo that.</span></span>

### <a name="create-arm-template"></a><span data-ttu-id="c6e35-120">ARM 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="c6e35-120">Create ARM Template</span></span>
<span data-ttu-id="c6e35-121">먼저 웹 응용 프로그램 및 호스팅 계획을 만드는 기본 ARM 템플릿을 사용하여 시작해 보겠습니다(매개 변수 및 변수는 간단하게 표시되지 않음).</span><span class="sxs-lookup"><span data-stu-id="c6e35-121">First, let's start with a basic ARM template that will create a web application and a hosting plan (note that parameters and variables are not shown for brevity).</span></span>

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

<span data-ttu-id="c6e35-122">다음으로 toomodify hello 웹 응용 프로그램 리소스 tootake 중첩된 MSDeploy 리소스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-122">Next, you will need toomodify hello web app resource tootake a nested MSDeploy resource.</span></span> <span data-ttu-id="c6e35-123">하면 tooreference hello 패키지 앞에서 만든 되 고 Azure 리소스 관리자 toouse MSDeploy toodeploy hello 패키지 toohello Azure WebApp 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-123">This will allow you tooreference hello package created earlier and tell Azure Resource Manager toouse MSDeploy toodeploy hello package toohello Azure WebApp.</span></span> <span data-ttu-id="c6e35-124">hello 다음 중첩 hello MSDeploy 리소스를 사용 하 여 hello Microsoft.Web/sites 리소스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-124">hello following shows hello Microsoft.Web/sites resource with hello nested MSDeploy resource:</span></span>

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

<span data-ttu-id="c6e35-125">이제 해당 hello MSDeploy 리소스 사용을 확인할 수 있습니다는 **packageUri** 다음과 같이 정의 된 속성:</span><span class="sxs-lookup"><span data-stu-id="c6e35-125">Now you will notice that hello MSDeploy resource takes a **packageUri** property which is defined as follows:</span></span>

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

<span data-ttu-id="c6e35-126">이 **packageUri** 사용 하 여 패키지 zip을 업로드 toohello 저장소 계정을 가리키는 저장소 계정 uri hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-126">This **packageUri** takes hello storage account uri which points toohello storage account where you will upload your package zip to.</span></span> <span data-ttu-id="c6e35-127">hello Azure 리소스 관리자를 활용 [공유 액세스 서명](../storage/common/storage-dotnet-shared-access-signature-part-1.md) hello 서식 파일을 배포할 때 hello 저장소 계정에서 로컬로 아래로 toopull hello 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-127">hello Azure Resource Manager will leverage [Shared Access Signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md) toopull hello package down locally from hello storage account when you deploy hello template.</span></span> <span data-ttu-id="c6e35-128">이 프로세스를 자동화 하 여 hello 패키지를 업로드 하 고 필요한 hello Azure 관리 API toocreate hello 키 호출 되며 이러한 hello 템플릿 매개 변수로 전달 하는 PowerShell 스크립트를 통해 됩니다 (*_artifactsLocation* 및 *_artifactsLocationSasToken*).</span><span class="sxs-lookup"><span data-stu-id="c6e35-128">This process will be automated via a PowerShell script that will upload hello package and call hello Azure Management API toocreate hello keys required and pass those into hello template as parameters (*_artifactsLocation* and *_artifactsLocationSasToken*).</span></span> <span data-ttu-id="c6e35-129">Hello 폴더에 대 한 toodefine 매개 변수가 필요 하며 filename hello 패키지는 업로드 된 toounder hello 저장소 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-129">You will need toodefine parameters for hello folder and filename hello package is uploaded toounder hello storage container.</span></span>

<span data-ttu-id="c6e35-130">다음 또 다른 중첩 된 리소스 toosetup hello 호스트 이름 바인딩 tooleverage 사용자 지정 도메인에에서 tooadd를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-130">Next you need tooadd in another nested resource toosetup hello hostname bindings tooleverage a custom domain.</span></span> <span data-ttu-id="c6e35-131">소유권을 Azure에서 첫 번째 필요 tooensure hello 호스트 이름을 소유 하 고 toobe 설정 확인-참조는 [Azure 앱 서비스에서 사용자 지정 도메인 이름을 구성](app-service-web-tutorial-custom-domain.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-131">You will first need tooensure that you own hello hostname and set it up toobe verified by Azure that you own it - see [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span> <span data-ttu-id="c6e35-132">이 작업을 마쳤으면 hello Microsoft.Web/sites 리소스 섹션 아래에서 tooyour 템플릿을 다음 hello를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-132">Once that is done you can add hello following tooyour template under hello Microsoft.Web/sites resource section:</span></span>

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

<span data-ttu-id="c6e35-133">마지막으로 tooadd 다른 최상위 리소스에서 Microsoft.Web/certificates 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-133">Finally you need tooadd another top level resource, Microsoft.Web/certificates.</span></span> <span data-ttu-id="c6e35-134">이 리소스 SSL 인증서 있고 hello 동일 수준 웹 앱으로 이동 하 고 호스팅 계획에 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-134">This resource will contain your SSL certificate and will exist at hello same level as your web app and hosting plan.</span></span>

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

<span data-ttu-id="c6e35-135">Toohave이이 리소스를 순서 tooset에 유효한 SSL 인증서가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-135">You will need toohave a valid SSL certificate in order tooset up this resource.</span></span> <span data-ttu-id="c6e35-136">유효한 해당 인증서를 수행한 다음 해야 tooextract hello pfx 바이트 base64 문자열.</span><span class="sxs-lookup"><span data-stu-id="c6e35-136">Once you have that valid certificate then you need tooextract hello pfx bytes as a base64 string.</span></span> <span data-ttu-id="c6e35-137">한 가지 옵션 tooextract이는 다음 PowerShell 명령을 toouse hello:</span><span class="sxs-lookup"><span data-stu-id="c6e35-137">One option tooextract this is toouse hello following PowerShell command:</span></span>

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

<span data-ttu-id="c6e35-138">이 매개 변수 tooyour ARM 배포 템플릿으로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-138">You could then pass this as a parameter tooyour ARM deployment template.</span></span>

<span data-ttu-id="c6e35-139">이 시점에서 hello ARM 템플릿이 준비 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-139">At this point hello ARM template is ready.</span></span>

### <a name="deploy-template"></a><span data-ttu-id="c6e35-140">템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="c6e35-140">Deploy Template</span></span>
<span data-ttu-id="c6e35-141">마지막 단계는 hello는 toopiece이 모두 함께 전체에 종단 간 배포에 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-141">hello final steps are toopiece this all together into a full end-to-end deployment.</span></span> <span data-ttu-id="c6e35-142">hello를 활용할 수 있습니다 더 쉽게 toomake 배포 **deploy-azureresourcegroup.ps1 스크립트로** 에 필요한 모든 아티팩트를 업로드와 toohelp Visual Studio에서에서 Azure 리소스 그룹 프로젝트를 만들 때 추가 된 PowerShell 스크립트 hello 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-142">toomake deployment easier you can leverage hello **Deploy-AzureResourceGroup.ps1** PowerShell script that is added when you create an Azure Resource Group project in Visual Studio toohelp with uploading of any artifacts required in hello template.</span></span> <span data-ttu-id="c6e35-143">Toohave toouse 보다 앞선 시간을 원하는 저장소 계정을 만든 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-143">It requires you toohave created a storage account you want toouse ahead of time.</span></span> <span data-ttu-id="c6e35-144">예를 들어 hello package.zip toobe 업로드에 대 한 공유 저장소 계정을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-144">For this example, I created a shared storage account for hello package.zip toobe uploaded.</span></span> <span data-ttu-id="c6e35-145">hello 스크립트 AzCopy tooupload hello 패키지 toohello 저장소 계정을 활용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-145">hello script will leverage AzCopy tooupload hello package toohello storage account.</span></span> <span data-ttu-id="c6e35-146">아티팩트 폴더 위치에 전달 하 고 hello 스크립트 저장소 컨테이너 이름이 해당 디렉터리 toohello 내의 모든 파일을 자동으로 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-146">You pass in your artifact folder location and hello script will automatically upload all files within that directory toohello named storage container.</span></span> <span data-ttu-id="c6e35-147">Deploy-azureresourcegroup.ps1 스크립트로 호출한 후 SSL 인증서와 함께 toothen 업데이트 hello SSL 바인딩 toomap hello 사용자 지정 호스트 이름이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-147">After calling Deploy-AzureResourceGroup.ps1 you have toothen update hello SSL bindings toomap hello custom hostname with your SSL certificate.</span></span>

<span data-ttu-id="c6e35-148">다음 PowerShell 표시 hello hello 배포 hello을 호출 하는 완전 한 배포-AzureResourceGroup.ps1:</span><span class="sxs-lookup"><span data-stu-id="c6e35-148">hello following PowerShell shows hello complete deployment calling hello Deploy-AzureResourceGroup.ps1:</span></span>

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

<span data-ttu-id="c6e35-149">이 시점에서 응용 프로그램은 배포 된 및 https://www.yourcustomdomain.com 통해 수 toobrowse tooit 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6e35-149">At this point your application should have been deployed and you should be able toobrowse tooit via https://www.yourcustomdomain.com</span></span>

