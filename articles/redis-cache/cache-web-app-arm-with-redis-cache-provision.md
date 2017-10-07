---
title: "aaaProvision Redis 캐시와 웹 응용 프로그램"
description: "Redis 캐시와 Azure 리소스 관리자 템플릿 toodeploy 웹 응용 프로그램을 사용 합니다."
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
ms.openlocfilehash: b95b5e230dc40c1157940c2017cba836975b6930
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-plus-redis-cache-using-a-template"></a><span data-ttu-id="c5bc6-103">템플릿을 사용하여 Redis Cache가 포함된 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="c5bc6-103">Create a Web App plus Redis Cache using a template</span></span>
<span data-ttu-id="c5bc6-104">이 항목에서는 살펴보겠습니다 어떻게 toocreate Redis cache 사용 하 여 Azure 웹 앱을 배포 하는 Azure 리소스 관리자 템플릿 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5bc6-104">In this topic, you will learn how toocreate an Azure Resource Manager template that deploys an Azure Web App with Redis cache.</span></span> <span data-ttu-id="c5bc6-105">에 대해 설명 합니다 방법을 toodefine 리소스 배포 되 고 toodefine 매개 변수를 hello 배포를 실행 하는 경우 지정 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5bc6-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="c5bc6-106">배포를 위한이 서식 파일을 사용 하거나 toomeet 사용자 지정할 수 있습니다 프로그램 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="c5bc6-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="c5bc6-107">템플릿을 만드는 더 자세한 내용은 [Azure 리소스 관리자 템플릿 작성하기](../azure-resource-manager/resource-group-authoring-templates.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="c5bc6-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="c5bc6-108">Hello 전체 서식 파일을 참조 하십시오. [Redis Cache 템플릿 사용 하 여 웹 앱](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5bc6-108">For hello complete template, see [Web App with Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span></span>

## <a name="what-you-will-deploy"></a><span data-ttu-id="c5bc6-109">배포할 내용</span><span class="sxs-lookup"><span data-stu-id="c5bc6-109">What you will deploy</span></span>
<span data-ttu-id="c5bc6-110">이 서식 파일에서 다음을 배포합니다:</span><span class="sxs-lookup"><span data-stu-id="c5bc6-110">In this template, you will deploy:</span></span>

* <span data-ttu-id="c5bc6-111">Azure 웹앱</span><span class="sxs-lookup"><span data-stu-id="c5bc6-111">Azure Web App</span></span>
* <span data-ttu-id="c5bc6-112">Azure Redis 캐시 사용을 시작하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5bc6-112">Azure Redis Cache.</span></span>

<span data-ttu-id="c5bc6-113">toorun 배포를 자동으로 hello, hello 다음 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5bc6-113">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="c5bc6-114">[![TooAzure 배포](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="c5bc6-114">[![Deploy tooAzure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters-toospecify"></a><span data-ttu-id="c5bc6-115">매개 변수 toospecify</span><span class="sxs-lookup"><span data-stu-id="c5bc6-115">Parameters toospecify</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

[!INCLUDE [cache-deploy-parameters](../../includes/cache-deploy-parameters.md)]

## <a name="variables-for-names"></a><span data-ttu-id="c5bc6-116">이름에 대한 변수</span><span class="sxs-lookup"><span data-stu-id="c5bc6-116">Variables for names</span></span>
<span data-ttu-id="c5bc6-117">이 서식 파일에는 hello 리소스에 대 한 변수 tooconstruct 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5bc6-117">This template uses variables tooconstruct names for hello resources.</span></span> <span data-ttu-id="c5bc6-118">Hello를 사용 하 여 [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) tooconstruct 리소스 그룹 id에 따라 값을 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5bc6-118">It uses hello [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) function tooconstruct a value based on the resource group id.</span></span>

    "variables": {
      "hostingPlanName": "[concat('hostingplan', uniqueString(resourceGroup().id))]",
      "webSiteName": "[concat('webSite', uniqueString(resourceGroup().id))]",
      "cacheName": "[concat('cache', uniqueString(resourceGroup().id))]"
    },


## <a name="resources-toodeploy"></a><span data-ttu-id="c5bc6-119">리소스 toodeploy</span><span class="sxs-lookup"><span data-stu-id="c5bc6-119">Resources toodeploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="redis-cache"></a><span data-ttu-id="c5bc6-120">Redis 캐시</span><span class="sxs-lookup"><span data-stu-id="c5bc6-120">Redis Cache</span></span>
<span data-ttu-id="c5bc6-121">Azure Redis Cache hello 웹 앱과 함께 사용 되는 hello를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c5bc6-121">Creates hello Azure Redis Cache that is used with hello web app.</span></span> <span data-ttu-id="c5bc6-122">hello hello 캐시의 이름은 hello **cacheName** 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c5bc6-122">hello name of hello cache is specified in hello **cacheName** variable.</span></span>

<span data-ttu-id="c5bc6-123">hello 템플릿 hello에 hello 캐시를 만든 동일한 hello 리소스 그룹 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="c5bc6-123">hello template creates hello cache in hello same location as hello resource group.</span></span>

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


### <a name="web-app"></a><span data-ttu-id="c5bc6-124">웹앱</span><span class="sxs-lookup"><span data-stu-id="c5bc6-124">Web app</span></span>
<span data-ttu-id="c5bc6-125">Hello에 지정 된 이름을 가진 hello 웹 응용 프로그램을 만듭니다 **webSiteName** 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c5bc6-125">Creates hello web app with name specified in hello **webSiteName** variable.</span></span>

<span data-ttu-id="c5bc6-126">Toowork hello Redis Cache로 사용 하도록 설정 하는 속성을 설정 하는 앱과 해당 hello 웹 응용 프로그램은 구성 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5bc6-126">Notice that hello web app is configured with app setting properties that enable it toowork with hello Redis Cache.</span></span> <span data-ttu-id="c5bc6-127">이 앱 설정은 배포 중에 제공된 값을 기반으로 동적으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c5bc6-127">This app settings are dynamically created based on values provided during deployment.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="c5bc6-128">명령 toorun 배포</span><span class="sxs-lookup"><span data-stu-id="c5bc6-128">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="c5bc6-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5bc6-129">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="c5bc6-130">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c5bc6-130">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -g ExampleDeployGroup
