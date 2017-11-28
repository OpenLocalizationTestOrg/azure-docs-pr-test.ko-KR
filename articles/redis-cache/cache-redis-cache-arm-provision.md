---
title: "Azure 리소스 관리자를 사용 하 여 Redis Cache aaaProvision | Microsoft Docs"
description: "Azure 리소스 관리자 템플릿 toodeploy Azure Redis Cache를 사용 합니다."
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
ms.openlocfilehash: 46e7b3b2493ac51dbe6bab0b086304802afc5d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-redis-cache-using-a-template"></a><span data-ttu-id="15696-103">템플릿을 사용하여 Redis Cache 만들기</span><span class="sxs-lookup"><span data-stu-id="15696-103">Create a Redis Cache using a template</span></span>
<span data-ttu-id="15696-104">이 항목에서는 설명 Azure Redis Cache toocreate Azure 리소스 관리자 템플릿을 배포 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="15696-104">In this topic, you learn how toocreate an Azure Resource Manager template that deploys an Azure Redis Cache.</span></span> <span data-ttu-id="15696-105">기존 저장소 계정 tookeep 진단 데이터와 hello 캐시를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15696-105">hello cache can be used with an existing storage account tookeep diagnostic data.</span></span> <span data-ttu-id="15696-106">또한 학습 방법을 toodefine 리소스 배포 되 고 toodefine 매개 변수를 hello 배포를 실행 하는 경우 지정 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="15696-106">You also learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="15696-107">배포를 위한이 서식 파일을 사용 하거나 toomeet 사용자 지정할 수 있습니다 프로그램 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="15696-107">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="15696-108">Hello에서 모든 캐시에 대 한 진단 설정을 공유 되는 현재 구독에 대 한 동일한 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="15696-108">Currently, diagnostic settings are shared for all caches in hello same region for a subscription.</span></span> <span data-ttu-id="15696-109">Hello 지역에서 하나의 캐시를 업데이트 hello 지역에서 다른 모든 캐시를 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15696-109">Updating one cache in hello region affects all other caches in hello region.</span></span>

<span data-ttu-id="15696-110">템플릿을 만드는 더 자세한 내용은 [Azure 리소스 관리자 템플릿 작성하기](../azure-resource-manager/resource-group-authoring-templates.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="15696-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="15696-111">Hello 전체 서식 파일을 참조 하십시오. [Redis Cache 템플릿](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="15696-111">For hello complete template, see [Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span></span>

> [!NOTE]
> <span data-ttu-id="15696-112">새 hello에 대 한 리소스 관리자 템플릿을 [Premium 계층](cache-premium-tier-intro.md) 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15696-112">Resource Manager templates for hello new [Premium tier](cache-premium-tier-intro.md) are available.</span></span> 
> 
> * [<span data-ttu-id="15696-113">클러스터링을 사용하여 프리미엄 Redis 캐시 만들기</span><span class="sxs-lookup"><span data-stu-id="15696-113">Create a Premium Redis Cache with clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [<span data-ttu-id="15696-114">지속성 데이터를 사용하여 프리미엄 Redis 캐시 만들기</span><span class="sxs-lookup"><span data-stu-id="15696-114">Create Premium Redis Cache with data persistence</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [<span data-ttu-id="15696-115">VNet과 선택적 클러스터링을 사용하여 프리미엄 Redis 캐시 만들기</span><span class="sxs-lookup"><span data-stu-id="15696-115">Create Premium Redis Cache with VNet and optional clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> <span data-ttu-id="15696-116">hello 최신 템플릿용으로 toocheck 참조 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/) 검색 한 `Redis Cache`합니다.</span><span class="sxs-lookup"><span data-stu-id="15696-116">toocheck for hello latest templates, see [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/) and search for `Redis Cache`.</span></span>
> 
> 

## <a name="what-you-will-deploy"></a><span data-ttu-id="15696-117">배포할 내용</span><span class="sxs-lookup"><span data-stu-id="15696-117">What you will deploy</span></span>
<span data-ttu-id="15696-118">이 템플릿에서 진단 데이터에 기존 저장소 계정을 사용하는 Azure Redis Cache를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="15696-118">In this template, you will deploy an Azure Redis Cache that uses an existing storage account for diagnostic data.</span></span>

<span data-ttu-id="15696-119">toorun 배포를 자동으로 hello, hello 다음 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="15696-119">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="15696-120">[![TooAzure 배포](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="15696-120">[![Deploy tooAzure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="15696-121">매개 변수</span><span class="sxs-lookup"><span data-stu-id="15696-121">Parameters</span></span>
<span data-ttu-id="15696-122">Azure 리소스 관리자와 정의한 매개 변수 값에 대 한 원하는 toospecify hello 서식 파일을 배포할 때.</span><span class="sxs-lookup"><span data-stu-id="15696-122">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="15696-123">hello 템플릿은 모든 hello 매개 변수 값이 포함 된 매개 변수 라는 섹션을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="15696-123">hello template includes a section called Parameters that contains all of hello parameter values.</span></span>
<span data-ttu-id="15696-124">에 배포 하는 hello 환경에 따라 또는 배포 하는 hello 프로젝트에 따라 달라 지는 해당 값에 대 한 매개 변수를 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15696-124">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="15696-125">동일한 값을 항상 유지 hello에 대 한 매개 변수를 정의 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15696-125">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="15696-126">각 매개 변수 값은 배포 된 hello 템플릿 toodefine hello 리소스에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15696-126">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span> 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a><span data-ttu-id="15696-127">redisCacheLocation</span><span class="sxs-lookup"><span data-stu-id="15696-127">redisCacheLocation</span></span>
<span data-ttu-id="15696-128">hello Redis Cache의 hello 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="15696-128">hello location of hello Redis Cache.</span></span> <span data-ttu-id="15696-129">최상의 성능을 위해 사용 하 여 동일한 hello hello 캐시 사용 응용 프로그램 toobe hello 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="15696-129">For best performance, use hello same location as hello app toobe used with hello cache.</span></span>

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a><span data-ttu-id="15696-130">existingDiagnosticsStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="15696-130">existingDiagnosticsStorageAccountName</span></span>
<span data-ttu-id="15696-131">진단에 대 한 기존 저장소 계정 toouse hello의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="15696-131">hello name of hello existing storage account toouse for diagnostics.</span></span> 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a><span data-ttu-id="15696-132">enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="15696-132">enableNonSslPort</span></span>
<span data-ttu-id="15696-133">나타내는 부울 값을 tooallow 비 SSL 포트를 통해 액세스할 지 여부를 합니다.</span><span class="sxs-lookup"><span data-stu-id="15696-133">A boolean value that indicates whether tooallow access via non-SSL ports.</span></span>

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a><span data-ttu-id="15696-134">diagnosticsStatus</span><span class="sxs-lookup"><span data-stu-id="15696-134">diagnosticsStatus</span></span>
<span data-ttu-id="15696-135">진단을 사용하도록 설정할지 여부를 나타내는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="15696-135">A value that indicates whether diagnostics is enabled.</span></span> <span data-ttu-id="15696-136">ON 또는 OFF를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="15696-136">Use ON or OFF.</span></span>

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-toodeploy"></a><span data-ttu-id="15696-137">리소스 toodeploy</span><span class="sxs-lookup"><span data-stu-id="15696-137">Resources toodeploy</span></span>
### <a name="redis-cache"></a><span data-ttu-id="15696-138">Redis 캐시</span><span class="sxs-lookup"><span data-stu-id="15696-138">Redis Cache</span></span>
<span data-ttu-id="15696-139">Azure Redis Cache hello를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15696-139">Creates hello Azure Redis Cache.</span></span>

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



## <a name="commands-toorun-deployment"></a><span data-ttu-id="15696-140">명령 toorun 배포</span><span class="sxs-lookup"><span data-stu-id="15696-140">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="15696-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="15696-141">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a><span data-ttu-id="15696-142">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="15696-142">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


