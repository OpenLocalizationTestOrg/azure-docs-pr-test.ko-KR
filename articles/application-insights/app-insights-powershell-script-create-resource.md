---
title: "Application Insights 리소스를 만들기 위한 PowerShell 스크립트 | Microsoft Docs"
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
ms.openlocfilehash: a828af9c7d207dd84cc626fc70206018fd67e2dd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="powershell-script-to-create-an-application-insights-resource"></a><span data-ttu-id="1721a-103">Application Insights 리소스를 만들기 위한 PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="1721a-103">PowerShell script to create an Application Insights resource</span></span>


<span data-ttu-id="1721a-104">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/)으로 새 응용 프로그램 또는 응용 프로그램의 새 버전을 모니터링 하려는 경우, Microsoft Azure에서 새 리소스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1721a-104">When you want to monitor a new application - or a new version of an application - with [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), you set up a new resource in Microsoft Azure.</span></span> <span data-ttu-id="1721a-105">이 리소스는 앱이 분석하고 표시한 원격 분석 데이터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1721a-105">This resource is where the telemetry data from your app is analyzed and displayed.</span></span> 

<span data-ttu-id="1721a-106">PowerShell을 사용하여 새 리소스의 생성을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1721a-106">You can automate the creation of a new resource by using PowerShell.</span></span>

<span data-ttu-id="1721a-107">예를 들어 모바일 장치 앱을 개발하는 경우, 언제든지 고객이 사용 중인 앱에는 게시된 여러 버전이 있을 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1721a-107">For example, if you are developing a mobile device app, it's likely that, at any time, there will be several published versions of your app in use by your customers.</span></span> <span data-ttu-id="1721a-108">혼합된 서로 다른 버전의 원격 분석 결과를 가져오지 않으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1721a-108">You don't want to get the telemetry results from different versions mixed up.</span></span> <span data-ttu-id="1721a-109">따라서 각 빌드에 대한 새 리소스를 만드는 빌드 프로세스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1721a-109">So you get your build process to create a new resource for each build.</span></span>

> [!NOTE]
> <span data-ttu-id="1721a-110">모든 리소스 집합을 동시에 만들려면 [Azure 템플릿을 사용하여 리소스를 만드는](app-insights-powershell.md) 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1721a-110">If you want to create a set of resources all at the same time, consider [creating the resources using an Azure template](app-insights-powershell.md).</span></span>
> 
> 

## <a name="script-to-create-an-application-insights-resource"></a><span data-ttu-id="1721a-111">Application Insights 리소스를 만들기 위한 스크립트</span><span class="sxs-lookup"><span data-stu-id="1721a-111">Script to create an Application Insights resource</span></span>
<span data-ttu-id="1721a-112">관련 cmdlet 사양을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1721a-112">See the relevant cmdlet specs:</span></span>

* [<span data-ttu-id="1721a-113">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="1721a-113">New-AzureRmResource</span></span>](https://msdn.microsoft.com/library/mt652510.aspx)
* [<span data-ttu-id="1721a-114">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="1721a-114">New-AzureRmRoleAssignment</span></span>](https://msdn.microsoft.com/library/mt678995.aspx)

<span data-ttu-id="1721a-115">*PowerShell 스크립트*</span><span class="sxs-lookup"><span data-stu-id="1721a-115">*PowerShell Script*</span></span>  

```PowerShell


###########################################
# Set Values
###########################################

# If running manually, uncomment before the first 
# execution to login to the Azure Portal:

# Add-AzureRmAccount / Login-AzureRmAccount

# Set the name of the Application Insights Resource

$appInsightsName = "TestApp"

# Set the application name used for the value of the Tag "AppInsightsApp" 

$applicationTagName = "MyApp"

# Set the name of the Resource Group to use.  
# Default is the application name.
$resourceGroupName = "MyAppResourceGroup"

###################################################
# Create the Resource and Output the name and iKey
###################################################

# Select the azure subscription
Select-AzureSubscription -SubscriptionName "MySubscription"

# Create the App Insights Resource


$resource = New-AzureRmResource `
  -ResourceName $appInsightsName `
  -ResourceGroupName $resourceGroupName `
  -Tag @{ applicationType = "web"; applicationName = $applicationTagName} `
  -ResourceType "Microsoft.Insights/components" `
  -Location "East US" `  # or North Europe, West Europe, South Central US
  -PropertyObject @{"Application_Type"="web"} `
  -Force

# Give owner access to the team

New-AzureRmRoleAssignment `
  -SignInName "myteam@fabrikam.com" `
  -RoleDefinitionName Owner `
  -Scope $resource.ResourceId 


# Display iKey
Write-Host "App Insights Name = " $resource.Name
Write-Host "IKey = " $resource.Properties.InstrumentationKey

```

## <a name="what-to-do-with-the-ikey"></a><span data-ttu-id="1721a-116">iKey로 수행할 작업</span><span class="sxs-lookup"><span data-stu-id="1721a-116">What to do with the iKey</span></span>
<span data-ttu-id="1721a-117">각 리소스는 해당 계측 키(iKey)로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="1721a-117">Each resource is identified by its instrumentation key (iKey).</span></span> <span data-ttu-id="1721a-118">iKey는 리소스 생성 스크립트의 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="1721a-118">The iKey is an output of the resource creation script.</span></span> <span data-ttu-id="1721a-119">빌드 스크립트는 앱에 포함된 Application Insights SDK에 iKey를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1721a-119">Your build script should provide the iKey to the Application Insights SDK embedded in your app.</span></span>

<span data-ttu-id="1721a-120">SDK에 사용할 수 있는 iKey에는 두 가지가 있습니다:</span><span class="sxs-lookup"><span data-stu-id="1721a-120">There are two ways to make the iKey available to the SDK:</span></span>

* <span data-ttu-id="1721a-121">[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)에서:</span><span class="sxs-lookup"><span data-stu-id="1721a-121">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span> 
  * <span data-ttu-id="1721a-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span><span class="sxs-lookup"><span data-stu-id="1721a-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span></span>
* <span data-ttu-id="1721a-123">또는 [초기화 코드](app-insights-api-custom-events-metrics.md):</span><span class="sxs-lookup"><span data-stu-id="1721a-123">Or in [initialization code](app-insights-api-custom-events-metrics.md):</span></span> 
  * <span data-ttu-id="1721a-124">`Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span><span class="sxs-lookup"><span data-stu-id="1721a-124">`Microsoft.ApplicationInsights.Extensibility.
TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span></span>

## <a name="see-also"></a><span data-ttu-id="1721a-125">참고 항목</span><span class="sxs-lookup"><span data-stu-id="1721a-125">See also</span></span>
* [<span data-ttu-id="1721a-126">서식 파일에서 Application Insights 및 웹 테스트 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="1721a-126">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="1721a-127">PowerShell 사용한 Azure 진단의 모니터링 설정</span><span class="sxs-lookup"><span data-stu-id="1721a-127">Set up monitoring of Azure diagnostics with PowerShell</span></span>](app-insights-powershell-azure-diagnostics.md) 
* [<span data-ttu-id="1721a-128">PowerShell을 사용하여 경고 설정</span><span class="sxs-lookup"><span data-stu-id="1721a-128">Set alerts by using PowerShell</span></span>](app-insights-powershell-alerts.md)

