---
title: "Azure Functions의 함수 앱에 대한 리소스 배포 자동화 | Microsoft Docs"
description: "함수 앱을 배포하는 Azure Resource Manager 템플릿을 빌드하는 방법을 알아봅니다."
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
ms.openlocfilehash: 15496e4ab2858b2aa319d53f1c438a259a3d5e49
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a><span data-ttu-id="473f0-104">Azure Functions의 함수 앱에 대한 리소스 배포 자동화</span><span class="sxs-lookup"><span data-stu-id="473f0-104">Automate resource deployment for your function app in Azure Functions</span></span>

<span data-ttu-id="473f0-105">Azure Resource Manager 템플릿을 사용하여 함수 앱을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-105">You can use an Azure Resource Manager template to deploy a function app.</span></span> <span data-ttu-id="473f0-106">이 문서에서는 이 작업을 수행하는 데 필요한 리소스와 매개 변수를 간략히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-106">This article outlines the required resources and parameters for doing so.</span></span> <span data-ttu-id="473f0-107">함수 앱의 [트리거 및 바인딩](functions-triggers-bindings.md)에 따라 추가 리소스를 배포해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-107">You might need to deploy additional resources, depending on the [triggers and bindings](functions-triggers-bindings.md) in your function app.</span></span>

<span data-ttu-id="473f0-108">템플릿을 만드는 더 자세한 내용은 [Azure Resource Manager 템플릿 작성하기](../azure-resource-manager/resource-group-authoring-templates.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="473f0-108">For more information about creating templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="473f0-109">샘플 템플릿은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="473f0-109">For sample templates, see:</span></span>
- <span data-ttu-id="473f0-110">[소비 계획의 함수 앱]</span><span class="sxs-lookup"><span data-stu-id="473f0-110">[Function app on Consumption plan]</span></span>
- <span data-ttu-id="473f0-111">[Azure App Service 계획의 함수 앱]</span><span class="sxs-lookup"><span data-stu-id="473f0-111">[Function app on Azure App Service plan]</span></span>

## <a name="required-resources"></a><span data-ttu-id="473f0-112">필요한 리소스</span><span class="sxs-lookup"><span data-stu-id="473f0-112">Required resources</span></span>

<span data-ttu-id="473f0-113">함수 앱에는 다음 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-113">A function app requires these resources:</span></span>

* <span data-ttu-id="473f0-114">[Azure Storage](../storage/index.md) 계정</span><span class="sxs-lookup"><span data-stu-id="473f0-114">An [Azure Storage](../storage/index.md) account</span></span>
* <span data-ttu-id="473f0-115">호스팅 계획(소비 계획 또는 App Service 계획)</span><span class="sxs-lookup"><span data-stu-id="473f0-115">A hosting plan (Consumption plan or App Service plan)</span></span>
* <span data-ttu-id="473f0-116">함수 앱</span><span class="sxs-lookup"><span data-stu-id="473f0-116">A function app</span></span> 

### <a name="storage-account"></a><span data-ttu-id="473f0-117">저장소 계정</span><span class="sxs-lookup"><span data-stu-id="473f0-117">Storage account</span></span>

<span data-ttu-id="473f0-118">함수 앱에는 Azure Storage 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-118">An Azure storage account is required for a function app.</span></span> <span data-ttu-id="473f0-119">Blob, 테이블, 큐 및 파일을 지원하는 일반 용도의 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-119">You need a general purpose account that supports blobs, tables, queues, and files.</span></span> <span data-ttu-id="473f0-120">자세한 내용은 [Azure Functions 저장소 계정 요구 사항](functions-create-function-app-portal.md#storage-account-requirements)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="473f0-120">For more information, see [Azure Functions storage account requirements](functions-create-function-app-portal.md#storage-account-requirements).</span></span>

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

<span data-ttu-id="473f0-121">또한 속성 `AzureWebJobsStorage` 및 `AzureWebJobsDashboard`도 사이트 구성에서 앱 설정으로 지정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-121">In addition, the properties `AzureWebJobsStorage` and `AzureWebJobsDashboard` must be specified as app settings in the site configuration.</span></span> <span data-ttu-id="473f0-122">Azure Functions 런타임에서는 `AzureWebJobsStorage` 연결 문자열을 사용하여 내부 큐를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-122">The Azure Functions runtime uses the `AzureWebJobsStorage` connection string to create internal queues.</span></span> <span data-ttu-id="473f0-123">연결 문자열 `AzureWebJobsDashboard`는 Azure Table storage에 로그하고 포털에서 **모니터** 탭의 성능을 높이는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-123">The connection string `AzureWebJobsDashboard` is used to log to Azure Table storage and power the **Monitor** tab in the portal.</span></span>

<span data-ttu-id="473f0-124">이러한 속성은 `siteConfig` 개체의 `appSettings` 컬렉션에서 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-124">These properties are specified in the `appSettings` collection in the `siteConfig` object:</span></span>

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

### <a name="hosting-plan"></a><span data-ttu-id="473f0-125">호스팅 계획</span><span class="sxs-lookup"><span data-stu-id="473f0-125">Hosting plan</span></span>

<span data-ttu-id="473f0-126">호스팅 계획의 정의는 소비 계획을 사용하는지, App Service 계획을 사용하는지에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-126">The definition of the hosting plan varies, depending on whether you use a Consumption or App Service plan.</span></span> <span data-ttu-id="473f0-127">[소비 계획의 함수 앱 배포](#consumption) 및 [App Service 계획의 함수 앱 배포](#app-service-plan)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="473f0-127">See [Deploy a function app on the Consumption plan](#consumption) and [Deploy a function app on the App Service plan](#app-service-plan).</span></span>

### <a name="function-app"></a><span data-ttu-id="473f0-128">함수 앱</span><span class="sxs-lookup"><span data-stu-id="473f0-128">Function app</span></span>

<span data-ttu-id="473f0-129">함수 앱 리소스는 다음과 같이 **Microsoft.Web/Site** 유형과 **functionapp** 종류의 리소스를 사용하여 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-129">The function app resource is defined by using a resource of type **Microsoft.Web/Site** and kind **functionapp**:</span></span>

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

## <a name="deploy-a-function-app-on-the-consumption-plan"></a><span data-ttu-id="473f0-130">소비 계획의 함수 앱 배포</span><span class="sxs-lookup"><span data-stu-id="473f0-130">Deploy a function app on the Consumption plan</span></span>

<span data-ttu-id="473f0-131">함수 앱은 두 가지 모드 즉, 소비 계획 및 App Service 계획으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-131">You can run a function app in two different modes: the Consumption plan and the App Service plan.</span></span> <span data-ttu-id="473f0-132">소비 계획은 코드가 실행 중일 때 계산 용량을 자동으로 할당하고, 로드를 처리하는 데 필요한 만큼 확장한 다음 코드가 실행되지 않을 때 축소합니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-132">The Consumption plan automatically allocates compute power when your code is running, scales out as necessary to handle load, and then scales down when code is not running.</span></span> <span data-ttu-id="473f0-133">따라서 유휴 VM에 대한 요금을 지불하고 용량을 미리 예약할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-133">So, you don't have to pay for idle VMs, and you don't have to reserve capacity in advance.</span></span> <span data-ttu-id="473f0-134">호스팅 계획에 대해 자세히 알아보려면 [Azure Functions 소비 및 App Service 계획](functions-scale.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="473f0-134">To learn more about hosting plans, see [Azure Functions Consumption and App Service plans](functions-scale.md).</span></span>

<span data-ttu-id="473f0-135">샘플 Azure Resource Manager 템플릿은 [소비 계획의 함수 앱]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="473f0-135">For a sample Azure Resource Manager template, see [Function app on Consumption plan].</span></span>

### <a name="create-a-consumption-plan"></a><span data-ttu-id="473f0-136">소비 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="473f0-136">Create a Consumption plan</span></span>

<span data-ttu-id="473f0-137">소비 계획은 특수한 유형의 "서버 팜" 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-137">A Consumption plan is a special type of "serverfarm" resource.</span></span> <span data-ttu-id="473f0-138">`computeMode` 및 `sku` 속성에 `Dynamic` 값을 사용하여 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-138">You specify it by using the `Dynamic` value for the `computeMode` and `sku` properties:</span></span>

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

### <a name="create-a-function-app"></a><span data-ttu-id="473f0-139">함수 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="473f0-139">Create a function app</span></span>

<span data-ttu-id="473f0-140">또한 소비 계획은 사이트 구성에 두 가지 추가 설정 `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` 및 `WEBSITE_CONTENTSHARE`가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-140">In addition, a Consumption plan requires two additional settings in the site configuration: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` and `WEBSITE_CONTENTSHARE`.</span></span> <span data-ttu-id="473f0-141">이러한 속성은 함수 앱 코드와 구성이 저장되는 저장소 계정 및 파일 경로를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-141">These properties configure the storage account and file path where the function app code and configuration are stored.</span></span>

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

## <a name="deploy-a-function-app-on-the-app-service-plan"></a><span data-ttu-id="473f0-142">App Service 계획의 함수 앱 배포</span><span class="sxs-lookup"><span data-stu-id="473f0-142">Deploy a function app on the App Service plan</span></span>

<span data-ttu-id="473f0-143">App Service 계획에서 함수 앱은 웹앱과 유사하게 기본, 표준, 프리미엄 SKU의 전용 VM에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-143">In the App Service plan, your function app runs on dedicated VMs on Basic, Standard, and Premium SKUs, similar to web apps.</span></span> <span data-ttu-id="473f0-144">App Service 계획의 작동 원리에 대한 자세한 내용은 [Azure App Service 계획의 포괄 개요](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="473f0-144">For details about how the App Service plan works, see the [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

<span data-ttu-id="473f0-145">샘플 Azure Resource Manager 템플릿은 [Azure App Service 계획의 함수 앱]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="473f0-145">For a sample Azure Resource Manager template, see [Function app on Azure App Service plan].</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="473f0-146">App Service 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="473f0-146">Create an App Service plan</span></span>

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

### <a name="create-a-function-app"></a><span data-ttu-id="473f0-147">함수 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="473f0-147">Create a function app</span></span> 

<span data-ttu-id="473f0-148">규모 조정 옵션을 선택한 후에는 함수 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-148">After you've selected a scaling option, create a function app.</span></span> <span data-ttu-id="473f0-149">앱은 모든 함수를 포함하는 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-149">The app is the container that holds all your functions.</span></span>

<span data-ttu-id="473f0-150">함수 앱에는 앱 설정 및 소스 제어 옵션을 포함하여 배포에 사용할 수 있는 자식 리소스가 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-150">A function app has many child resources that you can use in your deployment, including app settings and source control options.</span></span> <span data-ttu-id="473f0-151">또한 **sourcecontrols** 자식 리소스를 제거하고 대신에 다른 [배포 옵션](functions-continuous-deployment.md)을 사용하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-151">You also might choose to remove the **sourcecontrols** child resource, and use a different [deployment option](functions-continuous-deployment.md) instead.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="473f0-152">Azure Resource Manager를 사용하여 응용 프로그램을 성공적으로 배포하려면 Azure에서 리소스가 배포되는 방식을 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-152">To successfully deploy your application by using Azure Resource Manager, it's important to understand how resources are deployed in Azure.</span></span> <span data-ttu-id="473f0-153">다음 예제에서는 **siteConfig**를 사용하여 최상위 수준 구성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-153">In the following example, top-level configurations are applied by using **siteConfig**.</span></span> <span data-ttu-id="473f0-154">Functions 런타임 및 배포 엔진에 정보를 전달하기 때문에 최상위 수준에서 이러한 구성을 설정하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-154">It's important to set these configurations at a top level, because they convey information to the Functions runtime and deployment engine.</span></span> <span data-ttu-id="473f0-155">**sourcecontrols/web** 자식 리소스를 적용하기 전에 최상위 수준 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-155">Top-level information is required before the child **sourcecontrols/web** resource is applied.</span></span> <span data-ttu-id="473f0-156">자식 수준 **config/appSettings** 리소스에 이러한 설정을 구성할 수 있지만 **config/appSettings**가 적용되기 *전에* 함수 앱이 배포되어야 하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-156">Although it's possible to configure these settings in the child-level **config/appSettings** resource, in some cases your function app must be deployed *before* **config/appSettings** is applied.</span></span> <span data-ttu-id="473f0-157">예를 들어 [Logic Apps](../logic-apps/index.md)에서 함수를 사용하는 경우 함수는 다른 리소스의 종속성입니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-157">For example, when you are using functions with [Logic Apps](../logic-apps/index.md), your functions are a dependency of another resource.</span></span>

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
> <span data-ttu-id="473f0-158">이 템플릿은 Functions 배포 엔진(Kudu)에서 배치할 수 있는 코드를 검색할 기본 디렉터리를 설정하는 [프로젝트](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) 앱 설정 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-158">This template uses the [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) app settings value, which sets the base directory in which the Functions deployment engine (Kudu) looks for deployable code.</span></span> <span data-ttu-id="473f0-159">리포지토리에서 함수는 **src** 폴더의 하위 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-159">In our repository, our functions are in a subfolder of the **src** folder.</span></span> <span data-ttu-id="473f0-160">따라서 앞의 예제에서 앱 설정 값은 `src`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-160">So, in the preceding example, we set the app settings value to `src`.</span></span> <span data-ttu-id="473f0-161">함수가 리포지토리의 루트에 있거나 소스 제어에서 배포하지 않는 경우 이 앱 설정 값을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-161">If your functions are in the root of your repository, or if you are not deploying from source control, you can remove this app settings value.</span></span>

## <a name="deploy-your-template"></a><span data-ttu-id="473f0-162">템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="473f0-162">Deploy your template</span></span>

<span data-ttu-id="473f0-163">다음 방법 중 하나를 사용하여 템플릿을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-163">You can use any of the following ways to deploy your template:</span></span>

* [<span data-ttu-id="473f0-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="473f0-164">PowerShell</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
* [<span data-ttu-id="473f0-165">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="473f0-165">Azure CLI</span></span>](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [<span data-ttu-id="473f0-166">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="473f0-166">Azure portal</span></span>](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [<span data-ttu-id="473f0-167">REST API</span><span class="sxs-lookup"><span data-stu-id="473f0-167">REST API</span></span>](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-to-azure-button"></a><span data-ttu-id="473f0-168">Azure 단추에 배포</span><span class="sxs-lookup"><span data-stu-id="473f0-168">Deploy to Azure button</span></span>

<span data-ttu-id="473f0-169">```<url-encoded-path-to-azuredeploy-json>```을 GitHub에 있는 `azuredeploy.json` 파일의 원시 경로에 대한 [URL 인코딩](https://www.bing.com/search?q=url+encode) 버전으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-169">Replace ```<url-encoded-path-to-azuredeploy-json>``` with a [URL-encoded](https://www.bing.com/search?q=url+encode) version of the raw path of your `azuredeploy.json` file in GitHub.</span></span>

<span data-ttu-id="473f0-170">markdown을 사용하는 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-170">Here is an example that uses markdown:</span></span>

```markdown
[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

<span data-ttu-id="473f0-171">HTML을 사용하는 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-171">Here is an example that uses HTML:</span></span>

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a><span data-ttu-id="473f0-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="473f0-172">Next steps</span></span>

<span data-ttu-id="473f0-173">Azure Functions를 개발하고 구성하는 방법에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="473f0-173">Learn more about how to develop and configure Azure Functions.</span></span>

* [<span data-ttu-id="473f0-174">Azure Functions 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="473f0-174">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="473f0-175">Azure 함수 앱 설정을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="473f0-175">How to configure Azure function app settings</span></span>](functions-how-to-use-azure-function-app-settings.md)
* [<span data-ttu-id="473f0-176">첫 번째 Azure Function 만들기</span><span class="sxs-lookup"><span data-stu-id="473f0-176">Create your first Azure function</span></span>](functions-create-first-azure-function.md)

<!-- LINKS -->

[소비 계획의 함수 앱]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json
[Azure App Service 계획의 함수 앱]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json
