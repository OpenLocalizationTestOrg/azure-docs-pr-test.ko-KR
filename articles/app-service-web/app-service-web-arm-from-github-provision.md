---
title: "GitHub 리포지토리에 연결된 웹앱 배포 | Microsoft Docs"
description: "Azure 리소스 관리자 템플릿을 사용하여 GitHub 리포지토리에서 프로젝트가 포함된 웹앱을 배포합니다."
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
ms.openlocfilehash: 77064802814296d0c21f004534e4264d2f97252e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-web-app-linked-to-a-github-repository"></a><span data-ttu-id="8e43f-103">GitHub 리포지토리에 연결된 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="8e43f-103">Deploy a web app linked to a GitHub repository</span></span>
<span data-ttu-id="8e43f-104">이 항목에서는 GitHub 리포지토리의 프로젝트에 연결된 웹앱을 배포하는 Azure 리소스 관리자 템플릿을 만드는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="8e43f-104">In this topic, you will learn how to create an Azure Resource Manager template that deploys a web app that is linked to a project in a GitHub repository.</span></span> <span data-ttu-id="8e43f-105">어떤 리소스를 배포할지 정의하는 방법 및 배포를 실행할 때 매개 변수를 지정하는 방법을 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e43f-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="8e43f-106">배포를 위해 이 템플릿을 사용하거나 요구 사항에 맞게 사용자 지정을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e43f-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="8e43f-107">템플릿을 만드는 더 자세한 내용은 [Azure 리소스 관리자 템플릿 작성하기](../azure-resource-manager/resource-group-authoring-templates.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e43f-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="8e43f-108">전체 서식 파일을 보려면 [GitHub 템플릿에 연결된 웹앱](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e43f-108">For the complete template, see [Web App Linked to GitHub template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a><span data-ttu-id="8e43f-109">배포할 내용</span><span class="sxs-lookup"><span data-stu-id="8e43f-109">What you will deploy</span></span>
<span data-ttu-id="8e43f-110">이 템플릿을 사용하여 GitHub의 프로젝트에서 코드를 포함하는 웹앱을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="8e43f-110">With this template, you will deploy a web app that contains the code from a project in GitHub.</span></span>

<span data-ttu-id="8e43f-111">배포를 자동으로 실행하려면 다음 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e43f-111">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="8e43f-112">[![Azure에 배포](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="8e43f-112">[![Deploy to Azure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="8e43f-113">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8e43f-113">Parameters</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a><span data-ttu-id="8e43f-114">repoURL</span><span class="sxs-lookup"><span data-stu-id="8e43f-114">repoURL</span></span>
<span data-ttu-id="8e43f-115">배포하는 프로젝트를 포함하는 GitHub 리포지토리에 대한 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="8e43f-115">The URL for GitHub repository that contains the project to deploy.</span></span> <span data-ttu-id="8e43f-116">이 매개 변수는 기본값을 포함하지만 이 값은 어떻게 저장소에 대한 URL을 제공하는지 보여주기 위해 의도적으로 지정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8e43f-116">This parameter contains a default value but this value is only intended to show you how to provide the URL for repository.</span></span> <span data-ttu-id="8e43f-117">템플릿을 테스트할 때 이 값을 사용할 수 있지만, 템플릿을 사용하여 작업하는 경우 사용자 고유 저장소에 UIRL을 제공할 때도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8e43f-117">You can use this value when testing the template but you will want to provide the URL your own repository when working with the template.</span></span>

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a><span data-ttu-id="8e43f-118">분기</span><span class="sxs-lookup"><span data-stu-id="8e43f-118">branch</span></span>
<span data-ttu-id="8e43f-119">응용 프로그램을 배포할 때 사용하는 저장소의 분기입니다.</span><span class="sxs-lookup"><span data-stu-id="8e43f-119">The branch of the repository to use when deploying the application.</span></span> <span data-ttu-id="8e43f-120">기본값은 master, 하지만 배포 하고자 하는 저장소의 모든 분기의 이름을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e43f-120">The default value is master, but you can provide the name of any branch in the repository that you wish to deploy.</span></span>

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-to-deploy"></a><span data-ttu-id="8e43f-121">배포할 리소스</span><span class="sxs-lookup"><span data-stu-id="8e43f-121">Resources to deploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a><span data-ttu-id="8e43f-122">웹앱</span><span class="sxs-lookup"><span data-stu-id="8e43f-122">Web app</span></span>
<span data-ttu-id="8e43f-123">GitHub의 프로젝트에 연결된 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="8e43f-123">Creates the web app that is linked to the project in GitHub.</span></span> 

<span data-ttu-id="8e43f-124">**siteName** 매개 변수를 통해 웹앱의 이름을 지정하고 웹앱의 위치는 **siteLocation** 매개 변수를 통해 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8e43f-124">You specify the name of the web app through the **siteName** parameter, and the location of the web app through the **siteLocation** parameter.</span></span> <span data-ttu-id="8e43f-125">**dependsOn** 요소에서 템플릿은 서비스 호스팅 계획에 따라 웹앱을 달리 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="8e43f-125">In the **dependsOn** element, the template defines the web app as dependent on the service hosting plan.</span></span> <span data-ttu-id="8e43f-126">이것은 호스팅 계획에 따라 달라지기 때문에 호스팅 계획 만들기가 끝날 때까지 웹앱이 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8e43f-126">Because it is dependent on the hosting plan, the web app is not created until the hosting plan has finished being created.</span></span> <span data-ttu-id="8e43f-127">**dependsOn** 요소는 배포 순서를 지정하는 데만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e43f-127">The **dependsOn** element is only used to specify deployment order.</span></span> <span data-ttu-id="8e43f-128">호스팅을 계획하기 전에 웹앱을 만드는 경우 호스팅 계획에 따라 달라지는 웹앱을 표시하지 않으면 Azure 리소스 관리자가 동시에 두 리소스를 만들려 해서 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e43f-128">If you do not mark the web app as dependent on the hosting plan, Azure Resource Mananger will attempt to create both resources at the same time and you may receive an error if the web app is created before the hosting plan.</span></span>

<span data-ttu-id="8e43f-129">또한 웹앱에는 아래 **리소스** 섹션에 정의된 자식 리소스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e43f-129">The web app also has a child resource which is defined in **resources** section below.</span></span> <span data-ttu-id="8e43f-130">이 자식 리소스는 웹앱과 함께 배포된 프로젝트에 대한 소스 제어를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="8e43f-130">This child resource defines source control for the project deployed with the web app.</span></span> <span data-ttu-id="8e43f-131">이 템플릿에서 소스 제어는 특정 GitHub 리포지토리에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e43f-131">In this template, the source control is linked to a particular GitHub repository.</span></span> <span data-ttu-id="8e43f-132">GitHub 리포지토리에 코드 **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"**로 정의됩니다. 최소한의 매개 변수를 필요로 하는 동안 반복해서 단일 프로젝트를 배포하는 템플릿을 만드는 경우 리포지토리 URL를 하드 코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e43f-132">The GitHub repository is defined with the code **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"** You might hard-code the repository URL when you want to create a template that repeatedly deploys a single project while requiring the minimum number of parameters.</span></span>
<span data-ttu-id="8e43f-133">하드 코드한 리포지토리 URL 대신에 리포지토리 URL에 대한 매개 변수를 추가하고 해당 값을 **RepoUrl** 속성에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e43f-133">Instead of hard-coding the repository URL, you can add a parameter for the repository URL and use that value for the **RepoUrl** property.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="8e43f-134">배포 실행 명령</span><span class="sxs-lookup"><span data-stu-id="8e43f-134">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="8e43f-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8e43f-135">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="8e43f-136">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8e43f-136">Azure CLI</span></span>

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a><span data-ttu-id="8e43f-137">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8e43f-137">Azure CLI 2.0</span></span>

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> <span data-ttu-id="8e43f-138">JSON 파일의 매개 변수의 내용은 [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e43f-138">For content of the parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span></span>
>
>

