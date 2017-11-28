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
# <a name="powershell-script-toocreate-an-application-insights-resource"></a><span data-ttu-id="90ba5-103">PowerShell 스크립트 toocreate Application Insights 리소스</span><span class="sxs-lookup"><span data-stu-id="90ba5-103">PowerShell script toocreate an Application Insights resource</span></span>


<span data-ttu-id="90ba5-104">하려는 경우 toomonitor 새 응용 프로그램 또는 응용 프로그램의 새 버전으로 [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), Microsoft Azure에서 새 리소스를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="90ba5-104">When you want toomonitor a new application - or a new version of an application - with [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), you set up a new resource in Microsoft Azure.</span></span> <span data-ttu-id="90ba5-105">이 리소스 응용 프로그램에서 hello 원격 분석 데이터는 분석 하 고 표시 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="90ba5-105">This resource is where hello telemetry data from your app is analyzed and displayed.</span></span> 

<span data-ttu-id="90ba5-106">PowerShell을 사용 하 여 hello 결과적으로 새 리소스를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90ba5-106">You can automate hello creation of a new resource by using PowerShell.</span></span>

<span data-ttu-id="90ba5-107">예를 들어 모바일 장치 앱을 개발하는 경우, 언제든지 고객이 사용 중인 앱에는 게시된 여러 버전이 있을 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90ba5-107">For example, if you are developing a mobile device app, it's likely that, at any time, there will be several published versions of your app in use by your customers.</span></span> <span data-ttu-id="90ba5-108">Tooget hello 원격 분석 결과 혼합 하는 서로 다른 버전의 되기를 원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90ba5-108">You don't want tooget hello telemetry results from different versions mixed up.</span></span> <span data-ttu-id="90ba5-109">따라서 사용자가 빌드 프로세스 toocreate 새 리소스 각 빌드에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="90ba5-109">So you get your build process toocreate a new resource for each build.</span></span>

> [!NOTE]
> <span data-ttu-id="90ba5-110">Toocreate에 모든 리소스 집합이 원하는 경우 hello 동일한 시간을 고려 하십시오 [Azure 템플릿을 사용 하 여 hello 리소스를 만드는](app-insights-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="90ba5-110">If you want toocreate a set of resources all at hello same time, consider [creating hello resources using an Azure template](app-insights-powershell.md).</span></span>
> 
> 

## <a name="script-toocreate-an-application-insights-resource"></a><span data-ttu-id="90ba5-111">스크립트 toocreate Application Insights 리소스</span><span class="sxs-lookup"><span data-stu-id="90ba5-111">Script toocreate an Application Insights resource</span></span>
<span data-ttu-id="90ba5-112">Hello 관련 cmdlet 사양을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="90ba5-112">See hello relevant cmdlet specs:</span></span>

* [<span data-ttu-id="90ba5-113">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="90ba5-113">New-AzureRmResource</span></span>](https://msdn.microsoft.com/library/mt652510.aspx)
* [<span data-ttu-id="90ba5-114">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="90ba5-114">New-AzureRmRoleAssignment</span></span>](https://msdn.microsoft.com/library/mt678995.aspx)

<span data-ttu-id="90ba5-115">*PowerShell 스크립트*</span><span class="sxs-lookup"><span data-stu-id="90ba5-115">*PowerShell Script*</span></span>  

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

## <a name="what-toodo-with-hello-ikey"></a><span data-ttu-id="90ba5-116">어떤 toodo hello iKey와</span><span class="sxs-lookup"><span data-stu-id="90ba5-116">What toodo with hello iKey</span></span>
<span data-ttu-id="90ba5-117">각 리소스는 해당 계측 키(iKey)로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="90ba5-117">Each resource is identified by its instrumentation key (iKey).</span></span> <span data-ttu-id="90ba5-118">hello iKey은 hello 리소스 생성 스크립트의 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="90ba5-118">hello iKey is an output of hello resource creation script.</span></span> <span data-ttu-id="90ba5-119">빌드 스크립트 hello iKey toohello 응용 프로그램에 포함 Application Insights SDK를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90ba5-119">Your build script should provide hello iKey toohello Application Insights SDK embedded in your app.</span></span>

<span data-ttu-id="90ba5-120">두 가지 방법으로 toomake hello iKey 사용 가능한 toohello SDK 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90ba5-120">There are two ways toomake hello iKey available toohello SDK:</span></span>

* <span data-ttu-id="90ba5-121">[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)에서:</span><span class="sxs-lookup"><span data-stu-id="90ba5-121">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span> 
  * <span data-ttu-id="90ba5-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span><span class="sxs-lookup"><span data-stu-id="90ba5-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span></span>
* <span data-ttu-id="90ba5-123">또는 [초기화 코드](app-insights-api-custom-events-metrics.md):</span><span class="sxs-lookup"><span data-stu-id="90ba5-123">Or in [initialization code](app-insights-api-custom-events-metrics.md):</span></span> 
  * <span data-ttu-id="90ba5-124">`Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span><span class="sxs-lookup"><span data-stu-id="90ba5-124">`Microsoft.ApplicationInsights.Extensibility.
TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span></span>

## <a name="see-also"></a><span data-ttu-id="90ba5-125">참고 항목</span><span class="sxs-lookup"><span data-stu-id="90ba5-125">See also</span></span>
* [<span data-ttu-id="90ba5-126">서식 파일에서 Application Insights 및 웹 테스트 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="90ba5-126">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="90ba5-127">PowerShell 사용한 Azure 진단의 모니터링 설정</span><span class="sxs-lookup"><span data-stu-id="90ba5-127">Set up monitoring of Azure diagnostics with PowerShell</span></span>](app-insights-powershell-azure-diagnostics.md) 
* [<span data-ttu-id="90ba5-128">PowerShell을 사용하여 경고 설정</span><span class="sxs-lookup"><span data-stu-id="90ba5-128">Set alerts by using PowerShell</span></span>](app-insights-powershell-alerts.md)

