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
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a><span data-ttu-id="aee9b-104">Azure Functions의 함수 앱에 대한 리소스 배포 자동화</span><span class="sxs-lookup"><span data-stu-id="aee9b-104">Automate resource deployment for your function app in Azure Functions</span></span>

<span data-ttu-id="aee9b-105">Azure 리소스 관리자 템플릿 toodeploy 함수 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-105">You can use an Azure Resource Manager template toodeploy a function app.</span></span> <span data-ttu-id="aee9b-106">이 문서에서는 hello 필요한 리소스 및 작업에 대 한 매개 변수를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-106">This article outlines hello required resources and parameters for doing so.</span></span> <span data-ttu-id="aee9b-107">Hello에 따라 toodeploy 추가 리소스를 할 수 있습니다 [트리거 및 바인딩](functions-triggers-bindings.md) 함수 응용 프로그램에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-107">You might need toodeploy additional resources, depending on hello [triggers and bindings](functions-triggers-bindings.md) in your function app.</span></span>

<span data-ttu-id="aee9b-108">템플릿을 만드는 더 자세한 내용은 [Azure Resource Manager 템플릿 작성하기](../azure-resource-manager/resource-group-authoring-templates.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="aee9b-108">For more information about creating templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="aee9b-109">샘플 템플릿은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aee9b-109">For sample templates, see:</span></span>
- <span data-ttu-id="aee9b-110">[소비 계획의 함수 앱]</span><span class="sxs-lookup"><span data-stu-id="aee9b-110">[Function app on Consumption plan]</span></span>
- <span data-ttu-id="aee9b-111">[Azure App Service 계획의 함수 앱]</span><span class="sxs-lookup"><span data-stu-id="aee9b-111">[Function app on Azure App Service plan]</span></span>

## <a name="required-resources"></a><span data-ttu-id="aee9b-112">필요한 리소스</span><span class="sxs-lookup"><span data-stu-id="aee9b-112">Required resources</span></span>

<span data-ttu-id="aee9b-113">함수 앱에는 다음 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-113">A function app requires these resources:</span></span>

* <span data-ttu-id="aee9b-114">[Azure Storage](../storage/index.md) 계정</span><span class="sxs-lookup"><span data-stu-id="aee9b-114">An [Azure Storage](../storage/index.md) account</span></span>
* <span data-ttu-id="aee9b-115">호스팅 계획(소비 계획 또는 App Service 계획)</span><span class="sxs-lookup"><span data-stu-id="aee9b-115">A hosting plan (Consumption plan or App Service plan)</span></span>
* <span data-ttu-id="aee9b-116">함수 앱</span><span class="sxs-lookup"><span data-stu-id="aee9b-116">A function app</span></span> 

### <a name="storage-account"></a><span data-ttu-id="aee9b-117">저장소 계정</span><span class="sxs-lookup"><span data-stu-id="aee9b-117">Storage account</span></span>

<span data-ttu-id="aee9b-118">함수 앱에는 Azure Storage 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-118">An Azure storage account is required for a function app.</span></span> <span data-ttu-id="aee9b-119">Blob, 테이블, 큐 및 파일을 지원하는 일반 용도의 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-119">You need a general purpose account that supports blobs, tables, queues, and files.</span></span> <span data-ttu-id="aee9b-120">자세한 내용은 [Azure Functions 저장소 계정 요구 사항](functions-create-function-app-portal.md#storage-account-requirements)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aee9b-120">For more information, see [Azure Functions storage account requirements](functions-create-function-app-portal.md#storage-account-requirements).</span></span>

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

<span data-ttu-id="aee9b-121">또한 속성을 hello `AzureWebJobsStorage` 및 `AzureWebJobsDashboard` hello 사이트 구성에서 응용 프로그램 설정으로 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-121">In addition, hello properties `AzureWebJobsStorage` and `AzureWebJobsDashboard` must be specified as app settings in hello site configuration.</span></span> <span data-ttu-id="aee9b-122">hello Azure 함수 런타임은 hello를 사용 하 여 `AzureWebJobsStorage` 연결 문자열 toocreate 내부 큐.</span><span class="sxs-lookup"><span data-stu-id="aee9b-122">hello Azure Functions runtime uses hello `AzureWebJobsStorage` connection string toocreate internal queues.</span></span> <span data-ttu-id="aee9b-123">연결 문자열 hello `AzureWebJobsDashboard` 는 사용 되는 toolog tooAzure 테이블 저장소 및 전원 hello **모니터** hello 포털에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-123">hello connection string `AzureWebJobsDashboard` is used toolog tooAzure Table storage and power hello **Monitor** tab in hello portal.</span></span>

<span data-ttu-id="aee9b-124">이러한 속성은 hello에 지정 된 `appSettings` hello에 대 한 컬렉션 `siteConfig` 개체:</span><span class="sxs-lookup"><span data-stu-id="aee9b-124">These properties are specified in hello `appSettings` collection in hello `siteConfig` object:</span></span>

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

### <a name="hosting-plan"></a><span data-ttu-id="aee9b-125">호스팅 계획</span><span class="sxs-lookup"><span data-stu-id="aee9b-125">Hosting plan</span></span>

<span data-ttu-id="aee9b-126">hello 호스팅 계획의 hello 정의 소비 또는 앱 서비스 계획을 사용 하는지에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-126">hello definition of hello hosting plan varies, depending on whether you use a Consumption or App Service plan.</span></span> <span data-ttu-id="aee9b-127">참조 [hello 소비 계획에는 함수 앱을 배포할](#consumption) 및 [hello 앱 서비스 계획에는 함수 앱을 배포할](#app-service-plan)합니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-127">See [Deploy a function app on hello Consumption plan](#consumption) and [Deploy a function app on hello App Service plan](#app-service-plan).</span></span>

### <a name="function-app"></a><span data-ttu-id="aee9b-128">함수 앱</span><span class="sxs-lookup"><span data-stu-id="aee9b-128">Function app</span></span>

<span data-ttu-id="aee9b-129">hello 함수 응용 프로그램 리소스 유형의 리소스를 사용 하 여 정의 된 **Microsoft.Web/Site** 종류 및 **functionapp**:</span><span class="sxs-lookup"><span data-stu-id="aee9b-129">hello function app resource is defined by using a resource of type **Microsoft.Web/Site** and kind **functionapp**:</span></span>

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

## <a name="deploy-a-function-app-on-hello-consumption-plan"></a><span data-ttu-id="aee9b-130">Hello 소비 계획에 함수 앱 배포</span><span class="sxs-lookup"><span data-stu-id="aee9b-130">Deploy a function app on hello Consumption plan</span></span>

<span data-ttu-id="aee9b-131">두 가지 모드로 함수 응용 프로그램을 실행할 수 있습니다: hello 소비 계획과 hello 앱 서비스 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-131">You can run a function app in two different modes: hello Consumption plan and hello App Service plan.</span></span> <span data-ttu-id="aee9b-132">hello 소비 계획 코드 실행 되 고 필요한 toohandle 부하로 하 여 확장 하 고 그런 다음 코드를 실행 중이지 않을 때 확장 하는 경우 계산 능력을 자동으로 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-132">hello Consumption plan automatically allocates compute power when your code is running, scales out as necessary toohandle load, and then scales down when code is not running.</span></span> <span data-ttu-id="aee9b-133">따라서 유휴 Vm에 대 한 toopay 없는 바뀌고 없는 tooreserve 용량 미리.</span><span class="sxs-lookup"><span data-stu-id="aee9b-133">So, you don't have toopay for idle VMs, and you don't have tooreserve capacity in advance.</span></span> <span data-ttu-id="aee9b-134">호스팅 계획에 대 한 더 toolearn 참조 [Azure 함수 소비와 앱 서비스 계획](functions-scale.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-134">toolearn more about hosting plans, see [Azure Functions Consumption and App Service plans](functions-scale.md).</span></span>

<span data-ttu-id="aee9b-135">샘플 Azure Resource Manager 템플릿은 [소비 계획의 함수 앱]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aee9b-135">For a sample Azure Resource Manager template, see [Function app on Consumption plan].</span></span>

### <a name="create-a-consumption-plan"></a><span data-ttu-id="aee9b-136">소비 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="aee9b-136">Create a Consumption plan</span></span>

<span data-ttu-id="aee9b-137">소비 계획은 특수한 유형의 "서버 팜" 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-137">A Consumption plan is a special type of "serverfarm" resource.</span></span> <span data-ttu-id="aee9b-138">Hello를 사용 하 여 지정 `Dynamic` hello에 대 한 값 `computeMode` 및 `sku` 속성:</span><span class="sxs-lookup"><span data-stu-id="aee9b-138">You specify it by using hello `Dynamic` value for hello `computeMode` and `sku` properties:</span></span>

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

### <a name="create-a-function-app"></a><span data-ttu-id="aee9b-139">함수 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="aee9b-139">Create a function app</span></span>

<span data-ttu-id="aee9b-140">또한 소비 계획 요구 hello 사이트 구성의 두 가지 추가 설정을: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` 및 `WEBSITE_CONTENTSHARE`합니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-140">In addition, a Consumption plan requires two additional settings in hello site configuration: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` and `WEBSITE_CONTENTSHARE`.</span></span> <span data-ttu-id="aee9b-141">이러한 속성 hello 저장소 계정 및 파일 경로 hello 함수 응용 프로그램 코드와 구성이 저장 되는 위치를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-141">These properties configure hello storage account and file path where hello function app code and configuration are stored.</span></span>

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

## <a name="deploy-a-function-app-on-hello-app-service-plan"></a><span data-ttu-id="aee9b-142">앱 서비스 계획 hello에 함수 앱 배포</span><span class="sxs-lookup"><span data-stu-id="aee9b-142">Deploy a function app on hello App Service plan</span></span>

<span data-ttu-id="aee9b-143">앱 서비스 계획 hello 함수 앱은 Basic, Standard 및 Premium Sku 비슷한 tooweb 앱에 전용된 Vm에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-143">In hello App Service plan, your function app runs on dedicated VMs on Basic, Standard, and Premium SKUs, similar tooweb apps.</span></span> <span data-ttu-id="aee9b-144">앱 서비스 계획 hello 작동 하는 방법에 대 한 자세한 내용은 참조 hello [Azure 앱 서비스 계획 심도 깊은 개요](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-144">For details about how hello App Service plan works, see hello [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

<span data-ttu-id="aee9b-145">샘플 Azure Resource Manager 템플릿은 [Azure App Service 계획의 함수 앱]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aee9b-145">For a sample Azure Resource Manager template, see [Function app on Azure App Service plan].</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="aee9b-146">App Service 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="aee9b-146">Create an App Service plan</span></span>

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

### <a name="create-a-function-app"></a><span data-ttu-id="aee9b-147">함수 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="aee9b-147">Create a function app</span></span> 

<span data-ttu-id="aee9b-148">규모 조정 옵션을 선택한 후에는 함수 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-148">After you've selected a scaling option, create a function app.</span></span> <span data-ttu-id="aee9b-149">hello 응용 프로그램은 모든 기능을 보유 하는 hello 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-149">hello app is hello container that holds all your functions.</span></span>

<span data-ttu-id="aee9b-150">함수 앱에는 앱 설정 및 소스 제어 옵션을 포함하여 배포에 사용할 수 있는 자식 리소스가 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-150">A function app has many child resources that you can use in your deployment, including app settings and source control options.</span></span> <span data-ttu-id="aee9b-151">Tooremove hello 선택할 수 **sourcecontrols** 자식 리소스 및 사용 하 여 다른 [배포 옵션](functions-continuous-deployment.md) 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-151">You also might choose tooremove hello **sourcecontrols** child resource, and use a different [deployment option](functions-continuous-deployment.md) instead.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aee9b-152">Azure 리소스 관리자를 사용 하 여 응용 프로그램을 배포 하는 toosuccessfully에 중요 한 toounderstand 리소스가 Azure에 배포 되는 방식을 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-152">toosuccessfully deploy your application by using Azure Resource Manager, it's important toounderstand how resources are deployed in Azure.</span></span> <span data-ttu-id="aee9b-153">다음 예제는 hello에서 최상위 구성이 사용 하 여 적용 되는 **siteConfig**합니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-153">In hello following example, top-level configurations are applied by using **siteConfig**.</span></span> <span data-ttu-id="aee9b-154">정보 toohello 함수 런타임 및 배포 엔진 전달 때문 중요 tooset top에 이러한 구성 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-154">It's important tooset these configurations at a top level, because they convey information toohello Functions runtime and deployment engine.</span></span> <span data-ttu-id="aee9b-155">Hello 자식 항목 전에 최상위 정보가 필요 **sourcecontrols/웹** 리소스 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-155">Top-level information is required before hello child **sourcecontrols/web** resource is applied.</span></span> <span data-ttu-id="aee9b-156">이러한 설정을 하위 수준 hello 가능한 tooconfigure 있지만 **구성/appSettings** 함수 앱을 배포 해야 하는 일부 경우에 리소스 *전에* **구성/appSettings**  적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-156">Although it's possible tooconfigure these settings in hello child-level **config/appSettings** resource, in some cases your function app must be deployed *before* **config/appSettings** is applied.</span></span> <span data-ttu-id="aee9b-157">예를 들어 [Logic Apps](../logic-apps/index.md)에서 함수를 사용하는 경우 함수는 다른 리소스의 종속성입니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-157">For example, when you are using functions with [Logic Apps](../logic-apps/index.md), your functions are a dependency of another resource.</span></span>

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
> <span data-ttu-id="aee9b-158">이 템플릿은 hello를 사용 하 여 [프로젝트](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) hello 기본 디렉터리는 hello 함수 배포 엔진 (Kudu)는 배포 가능한 코드에 대 한 검색을 설정 하는 응용 프로그램 설정 값입니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-158">This template uses hello [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) app settings value, which sets hello base directory in which hello Functions deployment engine (Kudu) looks for deployable code.</span></span> <span data-ttu-id="aee9b-159">이 리포지토리에 우리의 함수 hello의 하위 폴더에서는 **src** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-159">In our repository, our functions are in a subfolder of hello **src** folder.</span></span> <span data-ttu-id="aee9b-160">따라서 앞 예제는 hello, 설정 hello 응용 프로그램 설정 값 너무`src`합니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-160">So, in hello preceding example, we set hello app settings value too`src`.</span></span> <span data-ttu-id="aee9b-161">기능은 여 저장소의 루트 hello에에서 또는 소스 제어에서 배포 하지 않는 경우이 응용 프로그램 설정 값을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-161">If your functions are in hello root of your repository, or if you are not deploying from source control, you can remove this app settings value.</span></span>

## <a name="deploy-your-template"></a><span data-ttu-id="aee9b-162">템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="aee9b-162">Deploy your template</span></span>

<span data-ttu-id="aee9b-163">다음 방법으로 toodeploy hello의 서식 파일에 사용할 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="aee9b-163">You can use any of hello following ways toodeploy your template:</span></span>

* [<span data-ttu-id="aee9b-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aee9b-164">PowerShell</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
* [<span data-ttu-id="aee9b-165">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="aee9b-165">Azure CLI</span></span>](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [<span data-ttu-id="aee9b-166">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="aee9b-166">Azure portal</span></span>](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [<span data-ttu-id="aee9b-167">REST API</span><span class="sxs-lookup"><span data-stu-id="aee9b-167">REST API</span></span>](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-tooazure-button"></a><span data-ttu-id="aee9b-168">배포 tooAzure 단추</span><span class="sxs-lookup"><span data-stu-id="aee9b-168">Deploy tooAzure button</span></span>

<span data-ttu-id="aee9b-169">대체 ```<url-encoded-path-to-azuredeploy-json>``` 와 [URL로 인코딩된](https://www.bing.com/search?q=url+encode) 의 hello 원시 경로 버전 프로그램 `azuredeploy.json` GitHub의 파일에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-169">Replace ```<url-encoded-path-to-azuredeploy-json>``` with a [URL-encoded](https://www.bing.com/search?q=url+encode) version of hello raw path of your `azuredeploy.json` file in GitHub.</span></span>

<span data-ttu-id="aee9b-170">markdown을 사용하는 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-170">Here is an example that uses markdown:</span></span>

```markdown
[![Deploy tooAzure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

<span data-ttu-id="aee9b-171">HTML을 사용하는 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-171">Here is an example that uses HTML:</span></span>

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a><span data-ttu-id="aee9b-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aee9b-172">Next steps</span></span>

<span data-ttu-id="aee9b-173">에 대 한 자세한 방법에 대 한 toodevelop 및 Azure 기능을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee9b-173">Learn more about how toodevelop and configure Azure Functions.</span></span>

* [<span data-ttu-id="aee9b-174">Azure Functions 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="aee9b-174">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="aee9b-175">어떻게 tooconfigure Azure 작동 앱 설정</span><span class="sxs-lookup"><span data-stu-id="aee9b-175">How tooconfigure Azure function app settings</span></span>](functions-how-to-use-azure-function-app-settings.md)
* [<span data-ttu-id="aee9b-176">첫 번째 Azure Function 만들기</span><span class="sxs-lookup"><span data-stu-id="aee9b-176">Create your first Azure function</span></span>](functions-create-first-azure-function.md)

<!-- LINKS -->

[소비 계획의 함수 앱]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json
[Azure App Service 계획의 함수 앱]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json
