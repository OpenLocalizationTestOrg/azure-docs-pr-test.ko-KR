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
# <a name="deploy-a-web-app-linked-tooa-github-repository"></a><span data-ttu-id="bd780-103">웹 응용 프로그램 연결 tooa GitHub 리포지토리를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd780-103">Deploy a web app linked tooa GitHub repository</span></span>
<span data-ttu-id="bd780-104">이 항목은 웹 앱을 배포 하는 Azure 리소스 관리자 템플릿을 toocreate GitHub 리포지토리에 tooa 프로젝트를 연결 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="bd780-104">In this topic, you will learn how toocreate an Azure Resource Manager template that deploys a web app that is linked tooa project in a GitHub repository.</span></span> <span data-ttu-id="bd780-105">에 대해 설명 합니다 방법을 toodefine 리소스 배포 되 고 toodefine 매개 변수를 hello 배포를 실행 하는 경우 지정 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd780-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="bd780-106">배포를 위한이 서식 파일을 사용 하거나 toomeet 사용자 지정할 수 있습니다 프로그램 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="bd780-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="bd780-107">템플릿을 만드는 더 자세한 내용은 [Azure 리소스 관리자 템플릿 작성하기](../azure-resource-manager/resource-group-authoring-templates.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="bd780-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="bd780-108">Hello 전체 서식 파일을 참조 하십시오. [응용 프로그램에 연결 된 웹 tooGitHub 템플릿](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="bd780-108">For hello complete template, see [Web App Linked tooGitHub template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a><span data-ttu-id="bd780-109">배포할 내용</span><span class="sxs-lookup"><span data-stu-id="bd780-109">What you will deploy</span></span>
<span data-ttu-id="bd780-110">이 템플릿을 사용 하 여 GitHub의 프로젝트에서 hello 코드를 포함 하는 웹 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd780-110">With this template, you will deploy a web app that contains hello code from a project in GitHub.</span></span>

<span data-ttu-id="bd780-111">toorun 배포를 자동으로 hello, hello 다음 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd780-111">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="bd780-112">[![TooAzure 배포](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="bd780-112">[![Deploy tooAzure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="bd780-113">매개 변수</span><span class="sxs-lookup"><span data-stu-id="bd780-113">Parameters</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a><span data-ttu-id="bd780-114">repoURL</span><span class="sxs-lookup"><span data-stu-id="bd780-114">repoURL</span></span>
<span data-ttu-id="bd780-115">hello 프로젝트 toodeploy 포함 된 GitHub 리포지토리에 대 한 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="bd780-115">hello URL for GitHub repository that contains hello project toodeploy.</span></span> <span data-ttu-id="bd780-116">이 매개 변수에 기본값을 포함 하지만이 값은 의도 한 tooshow만 하면 tooprovide 저장소에 대 한 URL을 hello 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="bd780-116">This parameter contains a default value but this value is only intended tooshow you how tooprovide hello URL for repository.</span></span> <span data-ttu-id="bd780-117">Hello 템플릿 있지만 테스트는 하려면 tooprovide hello URL 사용자 고유의 저장소 hello 템플릿을 사용 하 여 작업 하는 경우이 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd780-117">You can use this value when testing hello template but you will want tooprovide hello URL your own repository when working with hello template.</span></span>

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a><span data-ttu-id="bd780-118">분기</span><span class="sxs-lookup"><span data-stu-id="bd780-118">branch</span></span>
<span data-ttu-id="bd780-119">hello 분기 hello 리포지토리 toouse hello 응용 프로그램을 배포 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="bd780-119">hello branch of hello repository toouse when deploying hello application.</span></span> <span data-ttu-id="bd780-120">hello 기본값은 master, 하지만 toodeploy 한다고 hello 리포지토리의 모든 분기의 hello 이름을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd780-120">hello default value is master, but you can provide hello name of any branch in hello repository that you wish toodeploy.</span></span>

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-toodeploy"></a><span data-ttu-id="bd780-121">리소스 toodeploy</span><span class="sxs-lookup"><span data-stu-id="bd780-121">Resources toodeploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a><span data-ttu-id="bd780-122">웹앱</span><span class="sxs-lookup"><span data-stu-id="bd780-122">Web app</span></span>
<span data-ttu-id="bd780-123">GitHub에 연결 된 toohello 프로젝트가 hello 웹 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bd780-123">Creates hello web app that is linked toohello project in GitHub.</span></span> 

<span data-ttu-id="bd780-124">Hello 통해 hello 웹 응용 프로그램의 hello 이름을 지정 하면 **siteName** 매개 변수 및 hello 통해 hello 웹 응용 프로그램의 hello 위치 **siteLocation** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="bd780-124">You specify hello name of hello web app through hello **siteName** parameter, and hello location of hello web app through hello **siteLocation** parameter.</span></span> <span data-ttu-id="bd780-125">Hello에 **dependsOn** 요소 hello 템플릿 hello 웹 응용 프로그램 호스팅 계획 hello 서비스에 종속로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd780-125">In hello **dependsOn** element, hello template defines hello web app as dependent on hello service hosting plan.</span></span> <span data-ttu-id="bd780-126">호스팅 계획 hello에 의존 하므로 hello 웹 앱 호스팅 계획 hello 생성이 완료 될 때까지 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bd780-126">Because it is dependent on hello hosting plan, hello web app is not created until hello hosting plan has finished being created.</span></span> <span data-ttu-id="bd780-127">hello **dependsOn** 요소는 사용 되는 toospecify 배포 순서일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="bd780-127">hello **dependsOn** element is only used toospecify deployment order.</span></span> <span data-ttu-id="bd780-128">Hello 호스팅 계획에 종속으로 hello 웹 앱으로 표시 하면 Azure 리소스 관리자는 시도 toocreate 리소스가 모두 hello에서 동일한 시간 및 오류 메시지가 나타날 수 hello 호스팅 계획 하기 전에 hello 웹 응용 프로그램을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd780-128">If you do not mark hello web app as dependent on hello hosting plan, Azure Resource Mananger will attempt toocreate both resources at hello same time and you may receive an error if hello web app is created before hello hosting plan.</span></span>

<span data-ttu-id="bd780-129">hello 웹 응용 프로그램에 정의 된 자식 리소스에 **리소스** 아래 섹션.</span><span class="sxs-lookup"><span data-stu-id="bd780-129">hello web app also has a child resource which is defined in **resources** section below.</span></span> <span data-ttu-id="bd780-130">이 자식 리소스 hello 웹 앱을 사용 하 여 배포 된 hello 프로젝트에 대 한 소스 제어를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd780-130">This child resource defines source control for hello project deployed with hello web app.</span></span> <span data-ttu-id="bd780-131">이 서식 파일에서 hello 소스 제어 연결된 tooa 특정 GitHub 리포지토리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd780-131">In this template, hello source control is linked tooa particular GitHub repository.</span></span> <span data-ttu-id="bd780-132">hello GitHub 리포지토리 hello 코드를 사용 하 여 정의 **"RepoUrl": "https://github.com/davidebbo-test/Mvc52Application.git"** toocreate 반복적으로 배포 하는 템플릿을 원하는 경우에 하드 코딩 hello 리포지토리 URL을 수 있습니다는 hello 최소 매개 변수 개수를 요구 하는 동안 단일 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="bd780-132">hello GitHub repository is defined with hello code **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"** You might hard-code hello repository URL when you want toocreate a template that repeatedly deploys a single project while requiring hello minimum number of parameters.</span></span>
<span data-ttu-id="bd780-133">리포지토리 URL을 hello 하드 코딩 하는 대신, hello 리포지토리 URL에 대 한 매개 변수를 추가 하 고 해당 값을 사용 하 여 hello에 대 한 **RepoUrl** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="bd780-133">Instead of hard-coding hello repository URL, you can add a parameter for hello repository URL and use that value for hello **RepoUrl** property.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="bd780-134">명령 toorun 배포</span><span class="sxs-lookup"><span data-stu-id="bd780-134">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="bd780-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd780-135">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="bd780-136">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bd780-136">Azure CLI</span></span>

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a><span data-ttu-id="bd780-137">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="bd780-137">Azure CLI 2.0</span></span>

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> <span data-ttu-id="bd780-138">Hello 매개 변수에 JSON 파일의 콘텐츠에 대 한 참조 [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="bd780-138">For content of hello parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span></span>
>
>

