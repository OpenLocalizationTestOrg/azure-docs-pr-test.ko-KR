---
title: "Application Insights 리소스 aaaPowerShell 스크립트 toocreate | Microsoft Docs"
description: "Application Insights 리소스의 생성을 자동화합니다."
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: f0082c9b-43ad-4576-a417-4ea8e0daf3d9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/19/2016
ms.author: bwren
ms.openlocfilehash: 2ac00376d38026d64c2c5deabfaca60588924510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-script-toocreate-an-application-insights-resource"></a>PowerShell 스크립트 toocreate Application Insights 리소스


하려는 경우 toomonitor 새 응용 프로그램 또는 응용 프로그램의 새 버전으로 [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), Microsoft Azure에서 새 리소스를 설정 합니다. 이 리소스 응용 프로그램에서 hello 원격 분석 데이터는 분석 하 고 표시 되는 합니다. 

PowerShell을 사용 하 여 hello 결과적으로 새 리소스를 자동화할 수 있습니다.

예를 들어 모바일 장치 앱을 개발하는 경우, 언제든지 고객이 사용 중인 앱에는 게시된 여러 버전이 있을 가능성이 있습니다. Tooget hello 원격 분석 결과 혼합 하는 서로 다른 버전의 되기를 원하지 않습니다. 따라서 사용자가 빌드 프로세스 toocreate 새 리소스 각 빌드에 대 한 합니다.

> [!NOTE]
> Toocreate에 모든 리소스 집합이 원하는 경우 hello 동일한 시간을 고려 하십시오 [Azure 템플릿을 사용 하 여 hello 리소스를 만드는](app-insights-powershell.md)합니다.
> 
> 

## <a name="script-toocreate-an-application-insights-resource"></a>스크립트 toocreate Application Insights 리소스
Hello 관련 cmdlet 사양을 참조 하십시오.

* [New-AzureRmResource](https://msdn.microsoft.com/library/mt652510.aspx)
* [New-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt678995.aspx)

*PowerShell 스크립트*  

```PowerShell


###########################################
# Set Values
###########################################

# If running manually, uncomment before hello first 
# execution toologin toohello Azure Portal:

# Add-AzureRmAccount / Login-AzureRmAccount

# Set hello name of hello Application Insights Resource

$appInsightsName = "TestApp"

# Set hello application name used for hello value of hello Tag "AppInsightsApp" 

$applicationTagName = "MyApp"

# Set hello name of hello Resource Group toouse.  
# Default is hello application name.
$resourceGroupName = "MyAppResourceGroup"

###################################################
# Create hello Resource and Output hello name and iKey
###################################################

# Select hello azure subscription
Select-AzureSubscription -SubscriptionName "MySubscription"

# Create hello App Insights Resource


$resource = New-AzureRmResource `
  -ResourceName $appInsightsName `
  -ResourceGroupName $resourceGroupName `
  -Tag @{ applicationType = "web"; applicationName = $applicationTagName} `
  -ResourceType "Microsoft.Insights/components" `
  -Location "East US" `  # or North Europe, West Europe, South Central US
  -PropertyObject @{"Application_Type"="web"} `
  -Force

# Give owner access toohello team

New-AzureRmRoleAssignment `
  -SignInName "myteam@fabrikam.com" `
  -RoleDefinitionName Owner `
  -Scope $resource.ResourceId 


# Display iKey
Write-Host "App Insights Name = " $resource.Name
Write-Host "IKey = " $resource.Properties.InstrumentationKey

```

## <a name="what-toodo-with-hello-ikey"></a>어떤 toodo hello iKey와
각 리소스는 해당 계측 키(iKey)로 식별됩니다. hello iKey은 hello 리소스 생성 스크립트의 출력입니다. 빌드 스크립트 hello iKey toohello 응용 프로그램에 포함 Application Insights SDK를 제공 해야 합니다.

두 가지 방법으로 toomake hello iKey 사용 가능한 toohello SDK 가지가 있습니다.

* [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)에서: 
  * `<instrumentationkey>`*ikey*`</instrumentationkey>`
* 또는 [초기화 코드](app-insights-api-custom-events-metrics.md): 
  * `Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`

## <a name="see-also"></a>참고 항목
* [서식 파일에서 Application Insights 및 웹 테스트 리소스 만들기](app-insights-powershell.md)
* [PowerShell 사용한 Azure 진단의 모니터링 설정](app-insights-powershell-azure-diagnostics.md) 
* [PowerShell을 사용하여 경고 설정](app-insights-powershell-alerts.md)

