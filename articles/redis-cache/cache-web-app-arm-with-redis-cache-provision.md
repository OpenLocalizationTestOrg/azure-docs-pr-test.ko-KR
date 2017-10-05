---
title: "Redis Cache가 포함된 웹앱 프로비전"
description: "Redis Cache가 포함된 웹앱을 배포하려면 Azure 리소스 관리자 템플릿을 사용합니다."
services: app-service
documentationcenter: 
author: steved0x
manager: erickson-doug
editor: 
ms.assetid: 6e99c71f-ef8e-4570-a307-e4c059e60c35
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: sdanie
ms.openlocfilehash: 810c1cedd4fe0bd6ecdf9bd32dfb241f5f345300
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-plus-redis-cache-using-a-template"></a><span data-ttu-id="6df91-103">템플릿을 사용하여 Redis Cache가 포함된 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="6df91-103">Create a Web App plus Redis Cache using a template</span></span>
<span data-ttu-id="6df91-104">이 항목에서는 Redis Cache가 포함된 Azure 웹앱을 배포하는 Azure 리소스 관리자 템플릿을 만드는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="6df91-104">In this topic, you will learn how to create an Azure Resource Manager template that deploys an Azure Web App with Redis cache.</span></span> <span data-ttu-id="6df91-105">어떤 리소스를 배포할지 정의하는 방법 및 배포를 실행할 때 매개 변수를 지정하는 방법을 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6df91-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="6df91-106">배포를 위해 이 템플릿을 사용하거나 요구 사항에 맞게 사용자 지정을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df91-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="6df91-107">템플릿을 만드는 더 자세한 내용은 [Azure 리소스 관리자 템플릿 작성하기](../azure-resource-manager/resource-group-authoring-templates.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="6df91-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="6df91-108">전체 템플릿은 [Redis Cache 템플릿이 포함된 웹앱](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6df91-108">For the complete template, see [Web App with Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span></span>

## <a name="what-you-will-deploy"></a><span data-ttu-id="6df91-109">배포할 내용</span><span class="sxs-lookup"><span data-stu-id="6df91-109">What you will deploy</span></span>
<span data-ttu-id="6df91-110">이 서식 파일에서 다음을 배포합니다:</span><span class="sxs-lookup"><span data-stu-id="6df91-110">In this template, you will deploy:</span></span>

* <span data-ttu-id="6df91-111">Azure 웹앱</span><span class="sxs-lookup"><span data-stu-id="6df91-111">Azure Web App</span></span>
* <span data-ttu-id="6df91-112">Azure Redis 캐시 사용을 시작하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6df91-112">Azure Redis Cache.</span></span>

<span data-ttu-id="6df91-113">배포를 자동으로 실행하려면 다음 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6df91-113">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="6df91-114">[![Azure에 배포](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="6df91-114">[![Deploy to Azure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters-to-specify"></a><span data-ttu-id="6df91-115">지정할 매개변수</span><span class="sxs-lookup"><span data-stu-id="6df91-115">Parameters to specify</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

[!INCLUDE [cache-deploy-parameters](../../includes/cache-deploy-parameters.md)]

## <a name="variables-for-names"></a><span data-ttu-id="6df91-116">이름에 대한 변수</span><span class="sxs-lookup"><span data-stu-id="6df91-116">Variables for names</span></span>
<span data-ttu-id="6df91-117">이 템플릿은 리소스 이름을 생성하기 위해 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6df91-117">This template uses variables to construct names for the resources.</span></span> <span data-ttu-id="6df91-118">[uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) 함수를 사용하여 리소스 그룹 ID에 기반한 값을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="6df91-118">It uses the [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) function to construct a value based on the resource group id.</span></span>

    "variables": {
      "hostingPlanName": "[concat('hostingplan', uniqueString(resourceGroup().id))]",
      "webSiteName": "[concat('webSite', uniqueString(resourceGroup().id))]",
      "cacheName": "[concat('cache', uniqueString(resourceGroup().id))]"
    },


## <a name="resources-to-deploy"></a><span data-ttu-id="6df91-119">배포할 리소스</span><span class="sxs-lookup"><span data-stu-id="6df91-119">Resources to deploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="redis-cache"></a><span data-ttu-id="6df91-120">Redis 캐시</span><span class="sxs-lookup"><span data-stu-id="6df91-120">Redis Cache</span></span>
<span data-ttu-id="6df91-121">웹앱과 함께 사용되는 Azure Redics Cache를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6df91-121">Creates the Azure Redis Cache that is used with the web app.</span></span> <span data-ttu-id="6df91-122">캐시 이름은 **cacheName** 변수에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6df91-122">The name of the cache is specified in the **cacheName** variable.</span></span>

<span data-ttu-id="6df91-123">템플릿은 리소스 그룹과 동일한 위치에 캐시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6df91-123">The template creates the cache in the same location as the resource group.</span></span>

    {
      "name": "[variables('cacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[resourceGroup().location]",
      "apiVersion": "2015-08-01",
      "dependsOn": [ ],
      "tags": {
        "displayName": "cache"
      },
      "properties": {
        "sku": {
          "name": "[parameters('cacheSKUName')]",
          "family": "[parameters('cacheSKUFamily')]",
          "capacity": "[parameters('cacheSKUCapacity')]"
        }
      }
    }


### <a name="web-app"></a><span data-ttu-id="6df91-124">웹앱</span><span class="sxs-lookup"><span data-stu-id="6df91-124">Web app</span></span>
<span data-ttu-id="6df91-125">**webSiteName** 변수에 지정된 이름으로 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6df91-125">Creates the web app with name specified in the **webSiteName** variable.</span></span>

<span data-ttu-id="6df91-126">웹앱은 Redis Cache를 사용할 수 있도록 하는 앱 설정 속성으로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df91-126">Notice that the web app is configured with app setting properties that enable it to work with the Redis Cache.</span></span> <span data-ttu-id="6df91-127">이 앱 설정은 배포 중에 제공된 값을 기반으로 동적으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="6df91-127">This app settings are dynamically created based on values provided during deployment.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[variables('webSiteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Web/serverFarms/', variables('hostingPlanName'))]",
        "[concat('Microsoft.Cache/Redis/', variables('cacheName'))]"
      ],
      "tags": {
        "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', variables('hostingPlanName'))]": "empty",
        "displayName": "Website"
      },
      "properties": {
        "name": "[variables('webSiteName')]",
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "type": "config",
          "name": "appsettings",
          "dependsOn": [
            "[concat('Microsoft.Web/Sites/', variables('webSiteName'))]",
            "[concat('Microsoft.Cache/Redis/', variables('cacheName'))]"
          ],
          "properties": {
            "CacheConnection": "[concat(variables('cacheName'),'.redis.cache.windows.net,abortConnect=false,ssl=true,password=', listKeys(resourceId('Microsoft.Cache/Redis', variables('cacheName')), '2015-08-01').primaryKey)]"
          }
        }
      ]
    }

## <a name="commands-to-run-deployment"></a><span data-ttu-id="6df91-128">배포 실행 명령</span><span class="sxs-lookup"><span data-stu-id="6df91-128">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="6df91-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6df91-129">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="6df91-130">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6df91-130">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -g ExampleDeployGroup
