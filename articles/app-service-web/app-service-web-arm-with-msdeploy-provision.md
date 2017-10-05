---
title: "호스트 이름 및 ssl 인증서와 함께 MSDeploy를 사용하여 웹앱 배포"
description: "MSDeploy를 사용하고 사용자 지정 호스트 이름 및 SSL 인증서를 설정하는 웹앱을 배포하는 Azure 리소스 관리자 템플릿 사용"
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
ms.openlocfilehash: a0e944d0d74ecb72a919538d54db330cbbdeef64
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a><span data-ttu-id="8f356-103">MSDeploy, 사용자 지정 호스트 이름 및 SSL 인증서를 사용하여 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="8f356-103">Deploy a web app with MSDeploy, custom hostname and SSL certificate</span></span>
<span data-ttu-id="8f356-104">이 가이드에서는 Azure 웹앱에 대한 종단 간 배포 만들기, MSDeploy 활용과 사용자 지정 호스트 이름 및 SSL 인증서를 ARM 템플릿에 추가하는 작업에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-104">This guide walks through creating an end-to-end deployment for an Azure Web App, leveraging MSDeploy as well as adding a custom hostname and an SSL certificate to the ARM template.</span></span>

<span data-ttu-id="8f356-105">템플릿을 만드는 더 자세한 내용은 [Azure 리소스 관리자 템플릿 작성하기](../azure-resource-manager/resource-group-authoring-templates.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="8f356-105">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

### <a name="create-sample-application"></a><span data-ttu-id="8f356-106">응용 프로그램 예제 만들기</span><span class="sxs-lookup"><span data-stu-id="8f356-106">Create Sample Application</span></span>
<span data-ttu-id="8f356-107">ASP.NET 웹 응용 프로그램을 배포하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-107">You will be deploying an ASP.NET web application.</span></span> <span data-ttu-id="8f356-108">첫 번째 단계는 간단한 웹 응용 프로그램을 만드는 것입니다. 또는 기존 웹 응용 프로그램을 선택할 수 있습니다. 이 경우 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-108">The first step is to create a simple web application (or you could choose to use an existing one - in which case you can skip this step).</span></span>

<span data-ttu-id="8f356-109">Visual Studio 2015를 열고 파일 > 새 프로젝트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-109">Open Visual Studio 2015 and choose File > New Project.</span></span> <span data-ttu-id="8f356-110">표시되는 대화 상자에서 웹 > ASP.NET 웹 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-110">On the dialog that appears choose Web > ASP.NET Web Application.</span></span> <span data-ttu-id="8f356-111">템플릿 아래에서 웹을 선택하고 MVC 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-111">Under Templates choose Web and choose the MVC template.</span></span> <span data-ttu-id="8f356-112">*인증 형식 변경*을 *인증 안 함*으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-112">Select *Change authentication type* to *No Authentication*.</span></span> <span data-ttu-id="8f356-113">가능한 간단한 응용 프로그램 예제를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-113">This is just to make the sample application as simple as possible.</span></span>

<span data-ttu-id="8f356-114">이때 배포 프로세스의 일부로 사용하기 위해 기본 ASP.Net 웹앱을 준비해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-114">At this point you will have a basic ASP.Net web app ready to use as part of your deployment process.</span></span>

### <a name="create-msdeploy-package"></a><span data-ttu-id="8f356-115">MSDeploy 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="8f356-115">Create MSDeploy package</span></span>
<span data-ttu-id="8f356-116">다음 단계는 Azure에 웹앱을 배포하는 패키지를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-116">Next step is to create the package to deploy the web app to Azure.</span></span> <span data-ttu-id="8f356-117">이렇게 하려면 프로젝트를 저장한 후 명령줄에서 다음을 실행하세요.</span><span class="sxs-lookup"><span data-stu-id="8f356-117">To do this, save your project and then run the following from the command line:</span></span>

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

<span data-ttu-id="8f356-118">그러면 PackageLocation 폴더에 압축된 패키지가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-118">This will create a zipped package under the PackageLocation folder.</span></span> <span data-ttu-id="8f356-119">이제 응용 프로그램이 배포할 준비가 되었고 이 작업을 수행하기 위해 Azure 리소스 관리자 템플릿을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-119">The application is now ready to be deployed, which you can now build out an Azure Resource Manager template to do that.</span></span>

### <a name="create-arm-template"></a><span data-ttu-id="8f356-120">ARM 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="8f356-120">Create ARM Template</span></span>
<span data-ttu-id="8f356-121">먼저 웹 응용 프로그램 및 호스팅 계획을 만드는 기본 ARM 템플릿을 사용하여 시작해 보겠습니다(매개 변수 및 변수는 간단하게 표시되지 않음).</span><span class="sxs-lookup"><span data-stu-id="8f356-121">First, let's start with a basic ARM template that will create a web application and a hosting plan (note that parameters and variables are not shown for brevity).</span></span>

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

<span data-ttu-id="8f356-122">다음으로 중첩 MSDeploy 리소스를 가져오도록 웹앱 리소스를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-122">Next, you will need to modify the web app resource to take a nested MSDeploy resource.</span></span> <span data-ttu-id="8f356-123">이렇게 하면 이전에 만든 패키지를 참조하고 Azure 리소스 관리자가 MSDeploy를 사용하여 Azure WebApp에 패키지를 배포하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-123">This will allow you to reference the package created earlier and tell Azure Resource Manager to use MSDeploy to deploy the package to the Azure WebApp.</span></span> <span data-ttu-id="8f356-124">다음은 중첩 MSDeploy 리소스를 사용하는 Microsoft.Web/sites 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-124">The following shows the Microsoft.Web/sites resource with the nested MSDeploy resource:</span></span>

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

<span data-ttu-id="8f356-125">이제 MSDeploy 리소스는 다음과 같이 정의된 **packageUri** 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-125">Now you will notice that the MSDeploy resource takes a **packageUri** property which is defined as follows:</span></span>

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

<span data-ttu-id="8f356-126">이 **packageUri** 는 패키지 zip을 업로드할 저장소 계정을 가리키는 저장소 계정 uri를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-126">This **packageUri** takes the storage account uri which points to the storage account where you will upload your package zip to.</span></span> <span data-ttu-id="8f356-127">Azure 리소스 관리자는 템플릿 배포 시 저장소 계정에서 로컬로 패키지를 가져오는 데 [공유 액세스 서명](../storage/common/storage-dotnet-shared-access-signature-part-1.md) 을 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-127">The Azure Resource Manager will leverage [Shared Access Signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md) to pull the package down locally from the storage account when you deploy the template.</span></span> <span data-ttu-id="8f356-128">패키지를 업로드하고, 필요한 키를 만들고 템플릿에 매개 변수(*_artifactsLocation* 및 *_artifactsLocationSasToken*)로 전달하기 위해 Azure 관리 API를 호출하는 PowerShell 스크립트를 통해 이 프로세스를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-128">This process will be automated via a PowerShell script that will upload the package and call the Azure Management API to create the keys required and pass those into the template as parameters (*_artifactsLocation* and *_artifactsLocationSasToken*).</span></span> <span data-ttu-id="8f356-129">저장소 컨테이너에 업로드되는 패키지의 파일 이름 및 폴더에 대한 매개 변수를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-129">You will need to define parameters for the folder and filename the package is uploaded to under the storage container.</span></span>

<span data-ttu-id="8f356-130">다음으로 사용자 지정 도메인을 활용하도록 호스트 이름 바인딩을 설정하려면 다른 중첩된 리소스에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-130">Next you need to add in another nested resource to setup the hostname bindings to leverage a custom domain.</span></span> <span data-ttu-id="8f356-131">먼저 호스트 이름을 소유하고 소유한 Azure에서 확인하도록 설정해야 합니다. [Azure App Service에서 사용자 지정 도메인 이름 구성](app-service-web-tutorial-custom-domain.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f356-131">You will first need to ensure that you own the hostname and set it up to be verified by Azure that you own it - see [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span> <span data-ttu-id="8f356-132">이 작업을 완료했으면 Microsoft.Web/sites 리소스 섹션의 템플릿에 다음을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-132">Once that is done you can add the following to your template under the Microsoft.Web/sites resource section:</span></span>

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

<span data-ttu-id="8f356-133">마지막으로 다른 최상위 수준 리소스, Microsoft.Web/certificates를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-133">Finally you need to add another top level resource, Microsoft.Web/certificates.</span></span> <span data-ttu-id="8f356-134">이 리소스는 SSL 인증서를 포함하며 웹앱 및 호스팅 계획과 동일한 수준에 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-134">This resource will contain your SSL certificate and will exist at the same level as your web app and hosting plan.</span></span>

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

<span data-ttu-id="8f356-135">이 리소스를 설정하려면 유효한 SSL 인증서를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-135">You will need to have a valid SSL certificate in order to set up this resource.</span></span> <span data-ttu-id="8f356-136">유효한 인증서가 있는 경우 base64 문자열로 pfx 바이트를 추출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-136">Once you have that valid certificate then you need to extract the pfx bytes as a base64 string.</span></span> <span data-ttu-id="8f356-137">이를 추출하는 한 가지 옵션으로 다음 PowerShell 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-137">One option to extract this is to use the following PowerShell command:</span></span>

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

<span data-ttu-id="8f356-138">ARM 배포 템플릿에 매개 변수로 이를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-138">You could then pass this as a parameter to your ARM deployment template.</span></span>

<span data-ttu-id="8f356-139">이제 ARM 템플릿이 준비되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-139">At this point the ARM template is ready.</span></span>

### <a name="deploy-template"></a><span data-ttu-id="8f356-140">템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="8f356-140">Deploy Template</span></span>
<span data-ttu-id="8f356-141">마지막 단계는 이 모두를 전체 종단 간 배포로 종합하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-141">The final steps are to piece this all together into a full end-to-end deployment.</span></span> <span data-ttu-id="8f356-142">보다 쉬운 배포를 위해 템플릿에 필요한 모든 아티팩트를 업로드하는 데 도움이 되도록 Visual Studio에서 Azure 리소스 그룹 프로젝트를 만들 때 추가된 **Deploy-AzureResourceGroup.ps1** PowerShell 스크립트를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-142">To make deployment easier you can leverage the **Deploy-AzureResourceGroup.ps1** PowerShell script that is added when you create an Azure Resource Group project in Visual Studio to help with uploading of any artifacts required in the template.</span></span> <span data-ttu-id="8f356-143">사용하려는 저장소 계정을 미리 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-143">It requires you to have created a storage account you want to use ahead of time.</span></span> <span data-ttu-id="8f356-144">이 예제의 경우 업로드할 package.zip에 대한 공유 저장소 계정을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-144">For this example, I created a shared storage account for the package.zip to be uploaded.</span></span> <span data-ttu-id="8f356-145">스크립트는 저장소 계정에 패키지를 업로드하는 AzCopy를 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-145">The script will leverage AzCopy to upload the package to the storage account.</span></span> <span data-ttu-id="8f356-146">아티팩트 폴더 위치에 전달하면 스크립트는 저장소 컨테이너라는 해당 디렉터리 내의 모든 파일을 자동으로 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-146">You pass in your artifact folder location and the script will automatically upload all files within that directory to the named storage container.</span></span> <span data-ttu-id="8f356-147">Deploy-AzureResourceGroup.ps1을 호출한 후 SSL 인증서로 사용자 지정 호스트 이름에 매핑할 SSL 바인딩을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-147">After calling Deploy-AzureResourceGroup.ps1 you have to then update the SSL bindings to map the custom hostname with your SSL certificate.</span></span>

<span data-ttu-id="8f356-148">다음 PowerShell은 Deploy-AzureResourceGroup.ps1을 호출하는 전체 배포를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-148">The following PowerShell shows the complete deployment calling the Deploy-AzureResourceGroup.ps1:</span></span>

    #Set resource group name
    $rgName = "Name-of-resource-group"

    #call deploy-azureresourcegroup script to deploy web app

    .\Deploy-AzureResourceGroup.ps1 -ResourceGroupLocation "East US" `
                                    -ResourceGroupName $rgName `
                                    -UploadArtifacts `
                                    -StorageAccountName "name-of-storage-acct-for-package" `
                                    -StorageAccountResourceGroupName "resource-group-name-storage-acct" `
                                    -TemplateFile "web-app-deploy.json" `
                                    -TemplateParametersFile "web-app-deploy-parameters.json" `
                                    -ArtifactStagingDirectory "C:\path\to\packagefolder\"

    #update web app to bind ssl certificate to hostname. This has to be done after creation above.

    $cert = Get-PfxCertificate -FilePath C:\path\to\certificate.pfx

    $ar = Get-AzureRmResource -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -ApiVersion 2014-11-01

    $props = $ar.Properties

    $props.HostNameSslStates[2].'SslState' = 1
    $props.HostNameSslStates[2].'thumbprint' = $cert.Thumbprint
    $props.hostNameSslStates[2].'toUpdate' = $true

    Set-AzureRmResource -ApiVersion 2014-11-01 -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -PropertyObject $props

<span data-ttu-id="8f356-149">이제 응용 프로그램이 배포되었고 https://www.yourcustomdomain.com을 통해 탐색할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f356-149">At this point your application should have been deployed and you should be able to browse to it via https://www.yourcustomdomain.com</span></span>

