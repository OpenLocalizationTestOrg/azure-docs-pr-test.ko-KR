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
# <a name="high-density-hosting-on-azure-app-service"></a>Azure App Service의 고밀도 호스팅
응용 프로그램 서비스를 사용할 때 응용 프로그램 hello 용량 tooit 두 가지 개념에 의해 할당에서 분리 됩니다.

* **응용 프로그램 hello:** hello 앱 및 해당 런타임 구성을 나타냅니다. 예를 들어 hello 포함 런타임 hello.NET 버전을 로드 해야 hello 앱 설정 합니다.
* **앱 서비스 계획 hello:** hello 용량, 사용 가능한 기능 집합 및 hello 응용 프로그램의 위치 정확성 hello 특성을 정의 합니다. 예를 들어 특징은 큰(4코어) 컴퓨터, 인스턴스 4개, 미국 동부에서 프리미엄 기능일 수 있습니다.

응용 프로그램은 연결 된 앱 서비스 계획 tooan 항상 하지만 앱 서비스 계획 용량 tooone 또는 앱을 더 제공할 수 있습니다.

결과적으로, hello 플랫폼 hello 유연성 tooisolate 단일 앱을 제공 하거나 여러 앱을 앱 서비스 계획을 공유 하 여 리소스를 공유 합니다.

그러나 여러 앱이 앱 서비스 계획을 공유하는 경우 해당 앱의 인스턴스는 해당 앱 서비스 계획의 모든 인스턴스에서 실행됩니다.

## <a name="per-app-scaling"></a>앱 크기 조정당
*앱 크기 조정당* 은 앱 서비스 계획 수준에서 사용할 수 있는 기능이며 응용 프로그램마다 사용됩니다.

앱 크기 조정당은 호스팅하는 앱 서비스 계획에서 독립적으로 앱을 크기 조정합니다. 이러한 방식으로 앱 서비스 계획 수 too10 인스턴스 크기가 조정 하지만 앱 toouse 5 개를 설정할 수 있습니다.

   >[!NOTE]
   >앱 크기 조정당은 **Premium** SKU App Service 계획에 대해서만 사용 가능합니다.
   >

### <a name="per-app-scaling-using-powershell"></a>PowerShell을 사용하여 앱 크기 조정당

으로 구성 된 계획을 만들 수는 *앱 크기 조정 당* hello 전달 하 여 계획 ```-perSiteScaling $true``` toohello 특성 ```New-AzureRmAppServicePlan``` commandlet

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

Tooupdate 하려는 경우 기존 앱 서비스 계획 toouse이이 기능을 사용 합니다. 

- hello 대상 계획 가져오기```Get-AzureRmAppServicePlan```
- 로컬로 hello 속성 수정```$newASP.PerSiteScaling = $true```
- 변경 내용을 다시 tooazure 게시```Set-AzureRmAppServicePlan``` 

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

Hello 앱 수준에서 hello 앱 hello 앱 서비스 계획에서 사용할 수는 인스턴스의 tooconfigure hello 수가 필요 합니다.

아래 hello 예에서 hello 응용 프로그램 인스턴스가 제한 tootwo 인스턴스 개수에 관계 없이 hello 기본 앱 서비스 계획 아웃 하도록 확장 합니다.

```
# Get hello app we want tooconfigure toouse "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify hello NumberOfWorkers setting toohello desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back tooazure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> $newapp.SiteConfig.NumberOfWorkers는 $newapp.MaxNumberOfWorkers와 다릅니다. 앱 당 배율 $newapp을 사용합니다. SiteConfig.NumberOfWorkers toodetermine hello 눈금의 특성 hello 앱입니다.

### <a name="per-app-scaling-using-azure-resource-manager"></a>Azure Resource Manager를 사용하여 앱 크기 조정당

hello 다음 *Azure 리소스 관리자 템플릿* 만듭니다.

- Too10 인스턴스 크기가 조정 되는 앱 서비스 계획
- 가 tooscale tooa 최대 5 개의 인스턴스를 구성 하는 응용 프로그램입니다.

hello 앱 서비스 계획은 설정 하는 hello **PerSiteScaling** 속성 tootrue ```"perSiteScaling": true```합니다. hello 앱 설정 하 고 hello **작업자 수가** toouse too5 ```"properties": { "numberOfWorkers": "5" }```합니다.

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

## <a name="recommended-configuration-for-high-density-hosting"></a>고밀도 호스팅에 대한 권장된 구성
앱 크기 조정당은 글로벌 Azure 지역 및 앱 서비스 환경 모두에서 사용할 수 있는 기능입니다. 그러나 hello 전략의 고급 기능을 앱 서비스 환경 tootake 활용 및 hello 더 큰 풀의 용량을 사용 하는 것이 좋습니다.  

이러한 단계 tooconfigure 고밀도 앱에 대 한 호스팅를 수행 합니다.

1. 앱 서비스 환경 hello를 구성 하 고 전용된 toohello 고밀도 호스팅 시나리오를 작업자 풀을 선택 합니다.
1. 단일 앱 서비스 계획을 만들고 toouse 확장 hello 작업자 풀에 사용할 수 있는 용량이 hello 모든 합니다.
1. Hello PerSiteScaling 플래그 tootrue hello 앱 서비스 계획에 설정 합니다.
1. 새로운 앱 작성 되어 toothat 앱 서비스 계획을 할당는 **작업자** 속성이 너무 설정**1**합니다. 이 구성을 사용 하 여 hello 가장 높은 밀도 가능한이 작업자 풀에 생성 됩니다.
1. 작업자 수가 hello 구성할 수 있습니다 독립적으로 응용 프로그램 toogrant 추가 리소스 당 필요에 따라 합니다. 예:
    - 사용량이 많은 응용 프로그램을 설정할 수 **작업자** 너무**3** toohave 더 많은 처리 용량 해당 앱에 대 한 합니다. 
    - 많이 사용 되지 않는 앱 설정 **작업자** 너무**1**합니다.

## <a name="next-steps"></a>다음 단계

- [Azure App Service 계획의 포괄 개요](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [소개 tooApp 서비스 환경](../app-service-web/app-service-app-service-environment-intro.md)
