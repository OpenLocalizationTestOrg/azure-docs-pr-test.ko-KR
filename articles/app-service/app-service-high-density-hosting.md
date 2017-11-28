---
title: "Azure 앱 서비스에서 aaaHigh 밀도 호스팅 | Microsoft Docs"
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
ms.openlocfilehash: a10cb81ace13ba6992b572a44361061ecf72b266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="high-density-hosting-on-azure-app-service"></a><span data-ttu-id="d8c79-103">Azure App Service의 고밀도 호스팅</span><span class="sxs-lookup"><span data-stu-id="d8c79-103">High density hosting on Azure App Service</span></span>
<span data-ttu-id="d8c79-104">응용 프로그램 서비스를 사용할 때 응용 프로그램 hello 용량 tooit 두 가지 개념에 의해 할당에서 분리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-104">When using App Service, your application is decoupled from hello capacity allocated tooit by two concepts:</span></span>

* <span data-ttu-id="d8c79-105">**응용 프로그램 hello:** hello 앱 및 해당 런타임 구성을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-105">**hello Application:** Represents hello app and its runtime configuration.</span></span> <span data-ttu-id="d8c79-106">예를 들어 hello 포함 런타임 hello.NET 버전을 로드 해야 hello 앱 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-106">For example, it includes hello version of .NET that hello runtime should load, hello app settings.</span></span>
* <span data-ttu-id="d8c79-107">**앱 서비스 계획 hello:** hello 용량, 사용 가능한 기능 집합 및 hello 응용 프로그램의 위치 정확성 hello 특성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-107">**hello App Service Plan:** Defines hello characteristics of hello capacity, available feature set, and locality of hello application.</span></span> <span data-ttu-id="d8c79-108">예를 들어 특징은 큰(4코어) 컴퓨터, 인스턴스 4개, 미국 동부에서 프리미엄 기능일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-108">For example, characteristics might be large (four cores) machine, four instances, Premium features in East US.</span></span>

<span data-ttu-id="d8c79-109">응용 프로그램은 연결 된 앱 서비스 계획 tooan 항상 하지만 앱 서비스 계획 용량 tooone 또는 앱을 더 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-109">An app is always linked tooan App Service plan, but an App Service plan can provide capacity tooone or more apps.</span></span>

<span data-ttu-id="d8c79-110">결과적으로, hello 플랫폼 hello 유연성 tooisolate 단일 앱을 제공 하거나 여러 앱을 앱 서비스 계획을 공유 하 여 리소스를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-110">As a result, hello platform provides hello flexibility tooisolate a single app or have multiple apps share resources by sharing an App Service plan.</span></span>

<span data-ttu-id="d8c79-111">그러나 여러 앱이 앱 서비스 계획을 공유하는 경우 해당 앱의 인스턴스는 해당 앱 서비스 계획의 모든 인스턴스에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-111">However, when multiple apps share an App Service plan, an instance of that app runs on every instance of that App Service plan.</span></span>

## <a name="per-app-scaling"></a><span data-ttu-id="d8c79-112">앱 크기 조정당</span><span class="sxs-lookup"><span data-stu-id="d8c79-112">Per app scaling</span></span>
<span data-ttu-id="d8c79-113">*앱 크기 조정당* 은 앱 서비스 계획 수준에서 사용할 수 있는 기능이며 응용 프로그램마다 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-113">*Per app scaling* is a feature that can be enabled at the App Service plan level and then used per application.</span></span>

<span data-ttu-id="d8c79-114">앱 크기 조정당은 호스팅하는 앱 서비스 계획에서 독립적으로 앱을 크기 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-114">Per app scaling scales an app independently from the App Service plan that hosts it.</span></span> <span data-ttu-id="d8c79-115">이러한 방식으로 앱 서비스 계획 수 too10 인스턴스 크기가 조정 하지만 앱 toouse 5 개를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-115">This way, an App Service plan can be scaled too10 instances, but an app can be set toouse only five.</span></span>

   >[!NOTE]
   ><span data-ttu-id="d8c79-116">앱 크기 조정당은 **Premium** SKU App Service 계획에 대해서만 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-116">Per app scaling is available only for **Premium** SKU App Service plans</span></span>
   >

### <a name="per-app-scaling-using-powershell"></a><span data-ttu-id="d8c79-117">PowerShell을 사용하여 앱 크기 조정당</span><span class="sxs-lookup"><span data-stu-id="d8c79-117">Per app scaling using PowerShell</span></span>

<span data-ttu-id="d8c79-118">으로 구성 된 계획을 만들 수는 *앱 크기 조정 당* hello 전달 하 여 계획 ```-perSiteScaling $true``` toohello 특성 ```New-AzureRmAppServicePlan``` commandlet</span><span class="sxs-lookup"><span data-stu-id="d8c79-118">You can create a plan configured as a *Per app scaling* plan by passing in hello ```-perSiteScaling $true``` attribute toohello ```New-AzureRmAppServicePlan``` commandlet</span></span>

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

<span data-ttu-id="d8c79-119">Tooupdate 하려는 경우 기존 앱 서비스 계획 toouse이이 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-119">If you want tooupdate an existing App Service plan toouse this feature:</span></span> 

- <span data-ttu-id="d8c79-120">hello 대상 계획 가져오기```Get-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="d8c79-120">get hello target plan ```Get-AzureRmAppServicePlan```</span></span>
- <span data-ttu-id="d8c79-121">로컬로 hello 속성 수정```$newASP.PerSiteScaling = $true```</span><span class="sxs-lookup"><span data-stu-id="d8c79-121">modifying hello property locally ```$newASP.PerSiteScaling = $true```</span></span>
- <span data-ttu-id="d8c79-122">변경 내용을 다시 tooazure 게시```Set-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="d8c79-122">posting your changes back tooazure ```Set-AzureRmAppServicePlan```</span></span> 

```
# Get hello new App Service Plan and modify hello "PerSiteScaling" property.
$newASP = Get-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan
$newASP

#Modify hello local copy toouse "PerSiteScaling" property.
$newASP.PerSiteScaling = $true
$newASP
    
#Post updated app service plan back tooazure
Set-AzureRmAppServicePlan $newASP
```

<span data-ttu-id="d8c79-123">Hello 앱 수준에서 hello 앱 hello 앱 서비스 계획에서 사용할 수는 인스턴스의 tooconfigure hello 수가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-123">At hello app level, we need tooconfigure hello number of instances hello app can use in hello app service plan.</span></span>

<span data-ttu-id="d8c79-124">아래 hello 예에서 hello 응용 프로그램 인스턴스가 제한 tootwo 인스턴스 개수에 관계 없이 hello 기본 앱 서비스 계획 아웃 하도록 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-124">In hello example below, hello app is limited tootwo instances regardless of how many instances hello underlying app service plan scales out to.</span></span>

```
# Get hello app we want tooconfigure toouse "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify hello NumberOfWorkers setting toohello desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back tooazure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> <span data-ttu-id="d8c79-125">$newapp.SiteConfig.NumberOfWorkers는 $newapp.MaxNumberOfWorkers와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-125">$newapp.SiteConfig.NumberOfWorkers is different form $newapp.MaxNumberOfWorkers.</span></span> <span data-ttu-id="d8c79-126">앱 당 배율 $newapp을 사용합니다. SiteConfig.NumberOfWorkers toodetermine hello 눈금의 특성 hello 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-126">Per app scaling uses $newapp.SiteConfig.NumberOfWorkers toodetermine hello scale characteristics of hello app.</span></span>

### <a name="per-app-scaling-using-azure-resource-manager"></a><span data-ttu-id="d8c79-127">Azure Resource Manager를 사용하여 앱 크기 조정당</span><span class="sxs-lookup"><span data-stu-id="d8c79-127">Per app scaling using Azure Resource Manager</span></span>

<span data-ttu-id="d8c79-128">hello 다음 *Azure 리소스 관리자 템플릿* 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-128">hello following *Azure Resource Manager template* creates:</span></span>

- <span data-ttu-id="d8c79-129">Too10 인스턴스 크기가 조정 되는 앱 서비스 계획</span><span class="sxs-lookup"><span data-stu-id="d8c79-129">An App Service plan that's scaled out too10 instances</span></span>
- <span data-ttu-id="d8c79-130">가 tooscale tooa 최대 5 개의 인스턴스를 구성 하는 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-130">an app that's configured tooscale tooa max of five instances.</span></span>

<span data-ttu-id="d8c79-131">hello 앱 서비스 계획은 설정 하는 hello **PerSiteScaling** 속성 tootrue ```"perSiteScaling": true```합니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-131">hello App Service plan is setting hello **PerSiteScaling** property tootrue ```"perSiteScaling": true```.</span></span> <span data-ttu-id="d8c79-132">hello 앱 설정 하 고 hello **작업자 수가** toouse too5 ```"properties": { "numberOfWorkers": "5" }```합니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-132">hello app is setting hello **number of workers** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.</span></span>

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

## <a name="recommended-configuration-for-high-density-hosting"></a><span data-ttu-id="d8c79-133">고밀도 호스팅에 대한 권장된 구성</span><span class="sxs-lookup"><span data-stu-id="d8c79-133">Recommended configuration for high density hosting</span></span>
<span data-ttu-id="d8c79-134">앱 크기 조정당은 글로벌 Azure 지역 및 앱 서비스 환경 모두에서 사용할 수 있는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-134">Per app scaling is a feature that is enabled in both global Azure regions and App Service Environments.</span></span> <span data-ttu-id="d8c79-135">그러나 hello 전략의 고급 기능을 앱 서비스 환경 tootake 활용 및 hello 더 큰 풀의 용량을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-135">However, hello recommended strategy is to use App Service Environments tootake advantage of their advanced features and hello larger pools of capacity.</span></span>  

<span data-ttu-id="d8c79-136">이러한 단계 tooconfigure 고밀도 앱에 대 한 호스팅를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-136">Follow these steps tooconfigure high density hosting for your apps:</span></span>

1. <span data-ttu-id="d8c79-137">앱 서비스 환경 hello를 구성 하 고 전용된 toohello 고밀도 호스팅 시나리오를 작업자 풀을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-137">Configure hello App Service Environment and choose a worker pool that is dedicated toohello high density hosting scenario.</span></span>
1. <span data-ttu-id="d8c79-138">단일 앱 서비스 계획을 만들고 toouse 확장 hello 작업자 풀에 사용할 수 있는 용량이 hello 모든 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-138">Create a single App Service plan, and scale it toouse all hello available capacity on hello worker pool.</span></span>
1. <span data-ttu-id="d8c79-139">Hello PerSiteScaling 플래그 tootrue hello 앱 서비스 계획에 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-139">Set hello PerSiteScaling flag tootrue on hello App Service plan.</span></span>
1. <span data-ttu-id="d8c79-140">새로운 앱 작성 되어 toothat 앱 서비스 계획을 할당는 **작업자** 속성이 너무 설정**1**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-140">New apps are created and assigned toothat App Service plan with the **numberOfWorkers** property set too**1**.</span></span> <span data-ttu-id="d8c79-141">이 구성을 사용 하 여 hello 가장 높은 밀도 가능한이 작업자 풀에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-141">Using this configuration yields hello highest density possible on this worker pool.</span></span>
1. <span data-ttu-id="d8c79-142">작업자 수가 hello 구성할 수 있습니다 독립적으로 응용 프로그램 toogrant 추가 리소스 당 필요에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-142">hello number of workers can be configured independently per app toogrant additional resources as needed.</span></span> <span data-ttu-id="d8c79-143">예:</span><span class="sxs-lookup"><span data-stu-id="d8c79-143">For example:</span></span>
    - <span data-ttu-id="d8c79-144">사용량이 많은 응용 프로그램을 설정할 수 **작업자** 너무**3** toohave 더 많은 처리 용량 해당 앱에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-144">A high-use app can set **numberOfWorkers** too**3** toohave more processing capacity for that app.</span></span> 
    - <span data-ttu-id="d8c79-145">많이 사용 되지 않는 앱 설정 **작업자** 너무**1**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8c79-145">Low-use apps would set **numberOfWorkers** too**1**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8c79-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d8c79-146">Next Steps</span></span>

- [<span data-ttu-id="d8c79-147">Azure App Service 계획의 포괄 개요</span><span class="sxs-lookup"><span data-stu-id="d8c79-147">Azure App Service plans in-depth overview</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [<span data-ttu-id="d8c79-148">소개 tooApp 서비스 환경</span><span class="sxs-lookup"><span data-stu-id="d8c79-148">Introduction tooApp Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
