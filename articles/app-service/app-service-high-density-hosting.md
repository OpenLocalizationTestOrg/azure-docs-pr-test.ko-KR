---
title: "Azure App Service의 고밀도 호스팅 | Microsoft Docs"
description: "Azure App Service의 고밀도 호스팅"
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: a903cb78-4927-47b0-8427-56412c4e3e64
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: byvinyal
ms.openlocfilehash: 459a310a719695f6366470976d857ec2f9d6f4a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="high-density-hosting-on-azure-app-service"></a><span data-ttu-id="ba308-103">Azure App Service의 고밀도 호스팅</span><span class="sxs-lookup"><span data-stu-id="ba308-103">High density hosting on Azure App Service</span></span>
<span data-ttu-id="ba308-104">App Service를 사용할 경우 응용 프로그램은 2가지 개념에 의해 할당된 용량에서 분리됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-104">When using App Service, your application is decoupled from the capacity allocated to it by two concepts:</span></span>

* <span data-ttu-id="ba308-105">**응용 프로그램:** 앱 및 해당 런타임 구성을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-105">**The Application:** Represents the app and its runtime configuration.</span></span> <span data-ttu-id="ba308-106">예를 들어 런타임이 로드해야 하는 .NET 버전, 앱 설정을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-106">For example, it includes the version of .NET that the runtime should load, the app settings.</span></span>
* <span data-ttu-id="ba308-107">**앱 서비스 계획:** 응용 프로그램의 용량, 사용 가능한 기능 집합 및 거주지에 대한 특징을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-107">**The App Service Plan:** Defines the characteristics of the capacity, available feature set, and locality of the application.</span></span> <span data-ttu-id="ba308-108">예를 들어 특징은 큰(4코어) 컴퓨터, 인스턴스 4개, 미국 동부에서 프리미엄 기능일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-108">For example, characteristics might be large (four cores) machine, four instances, Premium features in East US.</span></span>

<span data-ttu-id="ba308-109">앱이 앱 서비스 계획에 항상 연결되어 있지만 앱 서비스 계획은 하나 이상의 앱에 대한 용량을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-109">An app is always linked to an App Service plan, but an App Service plan can provide capacity to one or more apps.</span></span>

<span data-ttu-id="ba308-110">결과적으로 플랫폼에서는 App Service 계획을 공유하여 단일 앱을 격리하거나 여러 앱 공유 리소스를 가지도록 유연성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-110">As a result, the platform provides the flexibility to isolate a single app or have multiple apps share resources by sharing an App Service plan.</span></span>

<span data-ttu-id="ba308-111">그러나 여러 앱이 앱 서비스 계획을 공유하는 경우 해당 앱의 인스턴스는 해당 앱 서비스 계획의 모든 인스턴스에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-111">However, when multiple apps share an App Service plan, an instance of that app runs on every instance of that App Service plan.</span></span>

## <a name="per-app-scaling"></a><span data-ttu-id="ba308-112">앱 크기 조정당</span><span class="sxs-lookup"><span data-stu-id="ba308-112">Per app scaling</span></span>
<span data-ttu-id="ba308-113">*앱 크기 조정당* 은 앱 서비스 계획 수준에서 사용할 수 있는 기능이며 응용 프로그램마다 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-113">*Per app scaling* is a feature that can be enabled at the App Service plan level and then used per application.</span></span>

<span data-ttu-id="ba308-114">앱 크기 조정당은 호스팅하는 앱 서비스 계획에서 독립적으로 앱을 크기 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-114">Per app scaling scales an app independently from the App Service plan that hosts it.</span></span> <span data-ttu-id="ba308-115">이러한 방식으로 App Service 계획은 10개의 인스턴스로 확장될 수 있지만 앱은 5개만 사용하도록 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-115">This way, an App Service plan can be scaled to 10 instances, but an app can be set to use only five.</span></span>

   >[!NOTE]
   ><span data-ttu-id="ba308-116">앱 크기 조정당은 **Premium** SKU App Service 계획에 대해서만 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-116">Per app scaling is available only for **Premium** SKU App Service plans</span></span>
   >

### <a name="per-app-scaling-using-powershell"></a><span data-ttu-id="ba308-117">PowerShell을 사용하여 앱 크기 조정당</span><span class="sxs-lookup"><span data-stu-id="ba308-117">Per app scaling using PowerShell</span></span>

<span data-ttu-id="ba308-118">```-perSiteScaling $true``` 속성에서 ```New-AzureRmAppServicePlan``` commandlet으로 전달하여 *앱 크기 조정당*으로 구성된 계획을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-118">You can create a plan configured as a *Per app scaling* plan by passing in the ```-perSiteScaling $true``` attribute to the ```New-AzureRmAppServicePlan``` commandlet</span></span>

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

<span data-ttu-id="ba308-119">기존 App Service 계획을 업데이트하여 이 기능을 사용하려는 경우:</span><span class="sxs-lookup"><span data-stu-id="ba308-119">If you want to update an existing App Service plan to use this feature:</span></span> 

- <span data-ttu-id="ba308-120">대상 계획 가져오기```Get-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="ba308-120">get the target plan ```Get-AzureRmAppServicePlan```</span></span>
- <span data-ttu-id="ba308-121">속성 로컬 수정```$newASP.PerSiteScaling = $true```</span><span class="sxs-lookup"><span data-stu-id="ba308-121">modifying the property locally ```$newASP.PerSiteScaling = $true```</span></span>
- <span data-ttu-id="ba308-122">변경 내용을 Azure에 다시 게시```Set-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="ba308-122">posting your changes back to azure ```Set-AzureRmAppServicePlan```</span></span> 

```
# Get the new App Service Plan and modify the "PerSiteScaling" property.
$newASP = Get-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan
$newASP

#Modify the local copy to use "PerSiteScaling" property.
$newASP.PerSiteScaling = $true
$newASP
    
#Post updated app service plan back to azure
Set-AzureRmAppServicePlan $newASP
```

<span data-ttu-id="ba308-123">앱 수준에서 앱이 앱 서비스 계획에서 사용할 수는 인스턴스 수를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-123">At the app level, we need to configure the number of instances the app can use in the app service plan.</span></span>

<span data-ttu-id="ba308-124">아래 예제에서 이 앱은 기본 앱 서비스 계획이 규모를 확장하는 인스턴스 수와 상관없이 2개 인스턴스로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-124">In the example below, the app is limited to two instances regardless of how many instances the underlying app service plan scales out to.</span></span>

```
# Get the app we want to configure to use "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify the NumberOfWorkers setting to the desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back to azure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> <span data-ttu-id="ba308-125">$newapp.SiteConfig.NumberOfWorkers는 $newapp.MaxNumberOfWorkers와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-125">$newapp.SiteConfig.NumberOfWorkers is different form $newapp.MaxNumberOfWorkers.</span></span> <span data-ttu-id="ba308-126">앱 크기 조정당 $newapp.SiteConfig.NumberOfWorkers를 사용하여 앱의 크기 조정 특성을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-126">Per app scaling uses $newapp.SiteConfig.NumberOfWorkers to determine the scale characteristics of the app.</span></span>

### <a name="per-app-scaling-using-azure-resource-manager"></a><span data-ttu-id="ba308-127">Azure Resource Manager를 사용하여 앱 크기 조정당</span><span class="sxs-lookup"><span data-stu-id="ba308-127">Per app scaling using Azure Resource Manager</span></span>

<span data-ttu-id="ba308-128">다음 *Azure Resource Manager 템플릿*이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-128">The following *Azure Resource Manager template* creates:</span></span>

- <span data-ttu-id="ba308-129">10개 인스턴스로 규모를 확장하는 App Service 계획</span><span class="sxs-lookup"><span data-stu-id="ba308-129">An App Service plan that's scaled out to 10 instances</span></span>
- <span data-ttu-id="ba308-130">최대 5개 인스턴스로 확장하도록 구성된 앱</span><span class="sxs-lookup"><span data-stu-id="ba308-130">an app that's configured to scale to a max of five instances.</span></span>

<span data-ttu-id="ba308-131">App Service 계획은 **PerSiteScaling** 속성을 true(```"perSiteScaling": true```)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-131">The App Service plan is setting the **PerSiteScaling** property to true ```"perSiteScaling": true```.</span></span> <span data-ttu-id="ba308-132">앱은 **작업자 수**를 5(```"properties": { "numberOfWorkers": "5" }```)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-132">The app is setting the **number of workers** to use to 5 ```"properties": { "numberOfWorkers": "5" }```.</span></span>

```
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters":{
        "appServicePlanName": { "type": "string" },
        "appName": { "type": "string" }
        },
    "resources": [
    {
        "comments": "App Service Plan with per site perSiteScaling = true",
        "type": "Microsoft.Web/serverFarms",
        "sku": {
            "name": "P1",
            "tier": "Premium",
            "size": "P1",
            "family": "P",
            "capacity": 10
            },
        "name": "[parameters('appServicePlanName')]",
        "apiVersion": "2015-08-01",
        "location": "West US",
        "properties": {
            "name": "[parameters('appServicePlanName')]",
            "perSiteScaling": true
        }
    },
    {
        "type": "Microsoft.Web/sites",
        "name": "[parameters('appName')]",
        "apiVersion": "2015-08-01-preview",
        "location": "West US",
        "dependsOn": [ "[resourceId('Microsoft.Web/serverFarms', parameters('appServicePlanName'))]" ],
        "properties": { "serverFarmId": "[resourceId('Microsoft.Web/serverFarms', parameters('appServicePlanName'))]" },
        "resources": [ {
                "comments": "",
                "type": "config",
                "name": "web",
                "apiVersion": "2015-08-01",
                "location": "West US",
                "dependsOn": [ "[resourceId('Microsoft.Web/Sites', parameters('appName'))]" ],
                "properties": { "numberOfWorkers": "5" }
            } ]
        }]
}
```

## <a name="recommended-configuration-for-high-density-hosting"></a><span data-ttu-id="ba308-133">고밀도 호스팅에 대한 권장된 구성</span><span class="sxs-lookup"><span data-stu-id="ba308-133">Recommended configuration for high density hosting</span></span>
<span data-ttu-id="ba308-134">앱 크기 조정당은 글로벌 Azure 지역 및 앱 서비스 환경 모두에서 사용할 수 있는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-134">Per app scaling is a feature that is enabled in both global Azure regions and App Service Environments.</span></span> <span data-ttu-id="ba308-135">그러나 권장되는 전략은 해당 고급 기능 및 큰 용량의 풀을 활용하도록 앱 서비스 환경을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-135">However, the recommended strategy is to use App Service Environments to take advantage of their advanced features and the larger pools of capacity.</span></span>  

<span data-ttu-id="ba308-136">앱에 대해 고밀도 호스팅을 구성하려면 이 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-136">Follow these steps to configure high density hosting for your apps:</span></span>

1. <span data-ttu-id="ba308-137">App Service 환경을 구성하고 고밀도 호스팅 시나리오에 전용으로 사용되는 작업자 풀을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-137">Configure the App Service Environment and choose a worker pool that is dedicated to the high density hosting scenario.</span></span>
1. <span data-ttu-id="ba308-138">단일 앱 서비스 계획을 만들고 확장하여 작업자 풀에서 모든 사용 가능한 용량을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-138">Create a single App Service plan, and scale it to use all the available capacity on the worker pool.</span></span>
1. <span data-ttu-id="ba308-139">App Service 계획에서 PerSiteScaling 플래그를 true로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-139">Set the PerSiteScaling flag to true on the App Service plan.</span></span>
1. <span data-ttu-id="ba308-140">새 앱이 만들어지고 **1**로 설정된 **numberOfWorkers** 속성이 있는 해당 App Service 계획에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-140">New apps are created and assigned to that App Service plan with the **numberOfWorkers** property set to **1**.</span></span> <span data-ttu-id="ba308-141">이 구성을 사용하면 작업자 풀에서 고밀도가 가능해 집니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-141">Using this configuration yields the highest density possible on this worker pool.</span></span>
1. <span data-ttu-id="ba308-142">작업자 수는 앱마다 독립적으로 구성되어 필요에 따라 추가 리소스를 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-142">The number of workers can be configured independently per app to grant additional resources as needed.</span></span> <span data-ttu-id="ba308-143">예:</span><span class="sxs-lookup"><span data-stu-id="ba308-143">For example:</span></span>
    - <span data-ttu-id="ba308-144">사용량이 많은 앱은 해당 앱에 대한 더 많은 처리 용량을 갖도록 **numberOfWorkers**를 **3**으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-144">A high-use app can set **numberOfWorkers** to **3** to have more processing capacity for that app.</span></span> 
    - <span data-ttu-id="ba308-145">많이 사용되지 않는 앱은 **numberOfWorkers**를 **1**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba308-145">Low-use apps would set **numberOfWorkers** to **1**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba308-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ba308-146">Next Steps</span></span>

- [<span data-ttu-id="ba308-147">Azure App Service 계획의 포괄 개요</span><span class="sxs-lookup"><span data-stu-id="ba308-147">Azure App Service plans in-depth overview</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [<span data-ttu-id="ba308-148">앱 서비스 환경 소개</span><span class="sxs-lookup"><span data-stu-id="ba308-148">Introduction to App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)