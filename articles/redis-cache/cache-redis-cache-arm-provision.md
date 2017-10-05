---
title: "Azure Resource Manager를 사용하여 Redis Cache 프로비전 | Microsoft Docs"
description: "Azure 리소스 관리자 템플릿을 사용하여 Azure Redis Cache를 배포합니다."
services: app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: ce6f5372-7038-4655-b1c5-108f7c148282
ms.service: cache
ms.workload: web
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: cce5d63e8bad2dd066cb4c28e2a8a9cb16c47953
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-redis-cache-using-a-template"></a><span data-ttu-id="89c41-103">템플릿을 사용하여 Redis Cache 만들기</span><span class="sxs-lookup"><span data-stu-id="89c41-103">Create a Redis Cache using a template</span></span>
<span data-ttu-id="89c41-104">이 항목에서는 Azure Redis Cache를 배포하는 Azure Resource Manager 템플릿을 만드는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="89c41-104">In this topic, you learn how to create an Azure Resource Manager template that deploys an Azure Redis Cache.</span></span> <span data-ttu-id="89c41-105">기존 저장소 계정과 함께 캐시를 사용하여 진단 데이터를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89c41-105">The cache can be used with an existing storage account to keep diagnostic data.</span></span> <span data-ttu-id="89c41-106">어떤 리소스를 배포할지 정의하는 방법 및 배포를 실행할 때 매개 변수를 지정하는 방법도 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="89c41-106">You also learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="89c41-107">배포를 위해 이 템플릿을 사용하거나 요구 사항에 맞게 사용자 지정을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89c41-107">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="89c41-108">현재 진단 설정은 구독에 대한 동일한 지역의 모든 캐시에서 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="89c41-108">Currently, diagnostic settings are shared for all caches in the same region for a subscription.</span></span> <span data-ttu-id="89c41-109">지역의 캐시 하나를 업데이트하면 해당 지역의 다른 모든 캐시에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="89c41-109">Updating one cache in the region affects all other caches in the region.</span></span>

<span data-ttu-id="89c41-110">템플릿을 만드는 더 자세한 내용은 [Azure 리소스 관리자 템플릿 작성하기](../azure-resource-manager/resource-group-authoring-templates.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="89c41-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="89c41-111">전체 템플릿은 [Redis Cache 템플릿](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89c41-111">For the complete template, see [Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span></span>

> [!NOTE]
> <span data-ttu-id="89c41-112">새 [프리미엄 계층](cache-premium-tier-intro.md) 에 대한 Resource Manager 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89c41-112">Resource Manager templates for the new [Premium tier](cache-premium-tier-intro.md) are available.</span></span> 
> 
> * [<span data-ttu-id="89c41-113">클러스터링을 사용하여 프리미엄 Redis 캐시 만들기</span><span class="sxs-lookup"><span data-stu-id="89c41-113">Create a Premium Redis Cache with clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [<span data-ttu-id="89c41-114">지속성 데이터를 사용하여 프리미엄 Redis 캐시 만들기</span><span class="sxs-lookup"><span data-stu-id="89c41-114">Create Premium Redis Cache with data persistence</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [<span data-ttu-id="89c41-115">VNet과 선택적 클러스터링을 사용하여 프리미엄 Redis 캐시 만들기</span><span class="sxs-lookup"><span data-stu-id="89c41-115">Create Premium Redis Cache with VNet and optional clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> <span data-ttu-id="89c41-116">최신 템플릿을 확인하려면 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/) 및 `Redis Cache`에 대한 검색을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89c41-116">To check for the latest templates, see [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/) and search for `Redis Cache`.</span></span>
> 
> 

## <a name="what-you-will-deploy"></a><span data-ttu-id="89c41-117">배포할 내용</span><span class="sxs-lookup"><span data-stu-id="89c41-117">What you will deploy</span></span>
<span data-ttu-id="89c41-118">이 템플릿에서 진단 데이터에 기존 저장소 계정을 사용하는 Azure Redis Cache를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="89c41-118">In this template, you will deploy an Azure Redis Cache that uses an existing storage account for diagnostic data.</span></span>

<span data-ttu-id="89c41-119">배포를 자동으로 실행하려면 다음 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89c41-119">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="89c41-120">[![Azure에 배포](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="89c41-120">[![Deploy to Azure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="89c41-121">매개 변수</span><span class="sxs-lookup"><span data-stu-id="89c41-121">Parameters</span></span>
<span data-ttu-id="89c41-122">Azure 리소스 관리자와 함께 템플릿을 배포할 때 지정하고자 하는 값으로 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="89c41-122">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="89c41-123">템플릿은 모든 매개 변수 값이 포함 된 매개 변수라는 섹션을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="89c41-123">The template includes a section called Parameters that contains all of the parameter values.</span></span>
<span data-ttu-id="89c41-124">배포하는 프로젝트에 따라 또는 환경에 따라 달라지는 이러한 값에 대한 매개 변수를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89c41-124">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="89c41-125">항상 동일하게 유지되는 값으로 매개 변수를 정의하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="89c41-125">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="89c41-126">각 매개 변수 값은 배포되는 리소스를 정의하는 템플릿에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="89c41-126">Each parameter value is used in the template to define the resources that are deployed.</span></span> 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a><span data-ttu-id="89c41-127">redisCacheLocation</span><span class="sxs-lookup"><span data-stu-id="89c41-127">redisCacheLocation</span></span>
<span data-ttu-id="89c41-128">Redics Cache의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="89c41-128">The location of the Redis Cache.</span></span> <span data-ttu-id="89c41-129">최상의 성능을 위해 캐시와 함께 사용될 앱과 동일한 위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="89c41-129">For best performance, use the same location as the app to be used with the cache.</span></span>

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a><span data-ttu-id="89c41-130">existingDiagnosticsStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="89c41-130">existingDiagnosticsStorageAccountName</span></span>
<span data-ttu-id="89c41-131">진단에 사용할 기존 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="89c41-131">The name of the existing storage account to use for diagnostics.</span></span> 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a><span data-ttu-id="89c41-132">enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="89c41-132">enableNonSslPort</span></span>
<span data-ttu-id="89c41-133">비 SSL 포트를 통한 액세스를 허용할지 여부를 나타내는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="89c41-133">A boolean value that indicates whether to allow access via non-SSL ports.</span></span>

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a><span data-ttu-id="89c41-134">diagnosticsStatus</span><span class="sxs-lookup"><span data-stu-id="89c41-134">diagnosticsStatus</span></span>
<span data-ttu-id="89c41-135">진단을 사용하도록 설정할지 여부를 나타내는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="89c41-135">A value that indicates whether diagnostics is enabled.</span></span> <span data-ttu-id="89c41-136">ON 또는 OFF를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="89c41-136">Use ON or OFF.</span></span>

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-to-deploy"></a><span data-ttu-id="89c41-137">배포할 리소스</span><span class="sxs-lookup"><span data-stu-id="89c41-137">Resources to deploy</span></span>
### <a name="redis-cache"></a><span data-ttu-id="89c41-138">Redis 캐시</span><span class="sxs-lookup"><span data-stu-id="89c41-138">Redis Cache</span></span>
<span data-ttu-id="89c41-139">Azure Redis Cache를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="89c41-139">Creates the Azure Redis Cache.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('redisCacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[parameters('redisCacheLocation')]",
      "properties": {
        "enableNonSslPort": "[parameters('enableNonSslPort')]",
        "sku": {
          "capacity": "[parameters('redisCacheCapacity')]",
          "family": "[parameters('redisCacheFamily')]",
          "name": "[parameters('redisCacheSKU')]"
        }
      },
      "resources": [
        {
          "apiVersion": "2015-07-01",
          "type": "Microsoft.Cache/redis/providers/diagnosticsettings",
          "name": "[concat(parameters('redisCacheName'), '/Microsoft.Insights/service')]",
          "location": "[parameters('redisCacheLocation')]",
          "dependsOn": [
            "[concat('Microsoft.Cache/Redis/', parameters('redisCacheName'))]"
          ],
          "properties": {
            "status": "[parameters('diagnosticsStatus')]",
            "storageAccountName": "[parameters('existingDiagnosticsStorageAccountName')]"
          }
        }
      ]
    }



## <a name="commands-to-run-deployment"></a><span data-ttu-id="89c41-140">배포 실행 명령</span><span class="sxs-lookup"><span data-stu-id="89c41-140">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="89c41-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="89c41-141">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a><span data-ttu-id="89c41-142">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="89c41-142">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


