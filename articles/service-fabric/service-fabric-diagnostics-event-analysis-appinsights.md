---
title: "Application Insights를 사용하여 Azure Service Fabric 이벤트 분석 | Microsoft Docs"
description: "Azure Service Fabric 클러스터의 모니터링 및 진단을 위해 Application Insights를 사용하여 이벤트를 시각화 및 분석하는 방법에 대해 알아봅니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 4085a607b800f4f4f155cdc266bc203b0858fd7c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="event-analysis-and-visualization-with-application-insights"></a><span data-ttu-id="595aa-103">Application Insights를 사용하여 이벤트 분석 및 시각화</span><span class="sxs-lookup"><span data-stu-id="595aa-103">Event analysis and visualization with Application Insights</span></span>

<span data-ttu-id="595aa-104">Azure Application Insights는 응용 프로그램 모니터링 및 진단을 위한 확장 가능한 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-104">Azure Application Insights is an extensible platform for application monitoring and diagnostics.</span></span> <span data-ttu-id="595aa-105">여기에는 강력한 분석 및 쿼리 도구, 사용자 지정 가능한 대시보드 및 시각화, 자동화된 경고 등의 추가 옵션이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-105">It includes a powerful analytics and querying tool, customizable dashboard and visualizations, and further options including automated alerting.</span></span> <span data-ttu-id="595aa-106">이는 Service Fabric 응용 프로그램 및 서비스에 대한 모니터링과 진단을 위해 권장되는 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-106">It is the recommended platform for monitoring and diagnostics for Service Fabric applications and services.</span></span>

## <a name="setting-up-application-insights"></a><span data-ttu-id="595aa-107">Application Insights 설정</span><span class="sxs-lookup"><span data-stu-id="595aa-107">Setting up Application Insights</span></span>

### <a name="creating-an-ai-resource"></a><span data-ttu-id="595aa-108">AI 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="595aa-108">Creating an AI Resource</span></span>

<span data-ttu-id="595aa-109">AI 리소스를 만들려면 Azure Marketplace로 이동하고 "Application Insights"를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-109">To create an AI resource, head over to the Azure Marketplace, and search for "Application Insights".</span></span> <span data-ttu-id="595aa-110">첫 번째 솔루션으로 표시되어야 합니다("웹 + 모바일" 범주 아래).</span><span class="sxs-lookup"><span data-stu-id="595aa-110">It should show up as the first solution (it is under category "Web + Mobile").</span></span> <span data-ttu-id="595aa-111">올바른 리소스가 표시되면 **만들기**를 클릭합니다. 경로가 아래 이미지와 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-111">Click **Create** when you are looking at the right resource (confirm that your path matches the image below).</span></span>

![새 Application Insights 리소스](media/service-fabric-diagnostics-event-analysis-appinsights/create-new-ai-resource.png)

<span data-ttu-id="595aa-113">리소스를 올바르게 프로비저닝하려면 몇 가지 정보를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-113">You will need to fill out some information to provision the resource correctly.</span></span> <span data-ttu-id="595aa-114">Service Fabric의 프로그래밍 모델을 사용하거나 클러스터에 .NET 응용 프로그램을 게시하려면 *응용 프로그램 유형* 필드에서 "ASP.NET 웹 응용 프로그램"을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-114">In the *Application Type* field, use "ASP.NET web application" if you will be using any of Service Fabric's programming models or publishing a .NET application to the cluster.</span></span> <span data-ttu-id="595aa-115">게스트 실행 파일과 컨테이너를 배포하려면 "일반"을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-115">Use "General" if you will be deploying guest executables and containers.</span></span> <span data-ttu-id="595aa-116">일반적으로 옵션이 계속 열린 상태로 유지되도록 "ASP.NET 웹 응용 프로그램"이 기본 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-116">In general, default to using "ASP.NET web application" to keep your options open in the future.</span></span> <span data-ttu-id="595aa-117">이름은 기본 설정에 따라 달라지며 리소스 그룹과 구독은 모두 리소스 배포 후 변경 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-117">The name is up to your preference, and both the resource group and subscription are changeable post-deployment of the resource.</span></span> <span data-ttu-id="595aa-118">AI 리소스가 클러스터와 동일한 리소스 그룹에 있는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-118">We recommend that your AI resource is in the same resource group as your cluster.</span></span> <span data-ttu-id="595aa-119">자세한 내용은 [Application Insights 리소스 만들기](../application-insights/app-insights-create-new-resource.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="595aa-119">If you need more information, please see [Create an Application Insights resource](../application-insights/app-insights-create-new-resource.md)</span></span>

<span data-ttu-id="595aa-120">이벤트 집계 도구로 AI를 구성하려면 AI 계측 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-120">You need the AI Instrumentation Key to configure AI with your event aggregation tool.</span></span> <span data-ttu-id="595aa-121">AI 리소스가 설정되면(배포 유효성을 확인한 후 몇 분 걸림) 이 리소스로 이동하고 왼쪽 탐색 모음에서 **속성** 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-121">Once your AI resource is set up (takes a few minutes after the deployment is validated), navigate to it and find the **Properties** section on the left navigation bar.</span></span> <span data-ttu-id="595aa-122">*계측 키*를 보여 주는 새 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-122">A new blade will open up that shows an *INSTRUMENTATION KEY*.</span></span> <span data-ttu-id="595aa-123">리소스의 리소스 그룹 또는 구독을 변경해야 하는 경우 여기에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-123">If you need to change the subscription or resource group of the resource, it can be done here as well.</span></span>

### <a name="configuring-ai-with-wad"></a><span data-ttu-id="595aa-124">WAD를 사용하여 AI 구성</span><span class="sxs-lookup"><span data-stu-id="595aa-124">Configuring AI with WAD</span></span>

<span data-ttu-id="595aa-125">WAD에서 Azure AI로 데이터를 전송하는 두 가지 기본적인 방법이 있습니다. 이 방법은 [이 문서](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md)에 설명된 대로 AI 싱크를 WAD 구성에 추가하여 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-125">There are two primary ways to send data from WAD to Azure AI, which is achieved by adding an AI sink to the WAD configuration, as detailed in [this article](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).</span></span>

#### <a name="add-an-ai-instrumentation-key-when-creating-a-cluster-in-azure-portal"></a><span data-ttu-id="595aa-126">Azure Portal에서 클러스터를 만들 때 AI 계측 키 추가</span><span class="sxs-lookup"><span data-stu-id="595aa-126">Add an AI Instrumentation Key when creating a cluster in Azure portal</span></span>

![AIKey 추가](media/service-fabric-diagnostics-event-analysis-appinsights/azure-enable-diagnostics.png)

<span data-ttu-id="595aa-128">클러스터를 만들 때 진단이 "설정"으로 설정되면 Application Insights 계측 키를 입력할 수 있는 선택 필드가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-128">When creating a cluster, if Diagnostics is turned "On", an optional field to enter an Application Insights Instrumentation key will show.</span></span> <span data-ttu-id="595aa-129">여기에 AI IKey를 붙여넣으면 클러스터를 배포하는 데 사용되는 Resource Manager 템플릿에서 AI 싱크가 자동으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-129">If you paste your AI IKey here, the AI sink will be automatically configured for you in the Resource Manager template that is used to deploy your cluster.</span></span>

#### <a name="add-the-ai-sink-to-the-resource-manager-template"></a><span data-ttu-id="595aa-130">Resource Manager 템플릿에 AI 싱크 추가</span><span class="sxs-lookup"><span data-stu-id="595aa-130">Add the AI Sink to the Resource Manager template</span></span>

<span data-ttu-id="595aa-131">Resource Manager 템플릿의 "WadCfg"에서 다음 두 가지 변경 사항을 포함하여 "Sink"를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-131">In the "WadCfg" of the Resource Manager template, add a "Sink" by including the following two changes:</span></span>

1. <span data-ttu-id="595aa-132">싱크 구성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-132">Add the sink configuration:</span></span>

    ```json
    "SinksConfig": {
        "Sink": [
            {
                "name": "applicationInsights",
                "ApplicationInsights": "***ADD INSTRUMENTATION KEY HERE***"
            }
        ]
    }

    ```

2. <span data-ttu-id="595aa-133">"WadCfg"의 "DiagnosticMonitorConfiguration"에 다음 줄을 추가하여 DiagnosticMonitorConfiguration에 Sink를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-133">Include the Sink in the DiagnosticMonitorConfiguration by adding the following line in "DiagnosticMonitorConfiguration" of the "WadCfg":</span></span>

    ```json
    "sinks": "applicationInsights"
    ```

<span data-ttu-id="595aa-134">위의 두 코드 조각에서 "applicationInsights"라는 이름이 싱크를 설명하는 데 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-134">In both the code snippets above, the name "applicationInsights" was used to describe the sink.</span></span> <span data-ttu-id="595aa-135">이는 요구 사항은 아니며 싱크의 이름이 "sinks"에 포함되어 있는 한 이름을 임의의 문자열로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-135">This is not a requirement and as long as the name of the sink is included in "sinks", you can set the name to any string.</span></span>

<span data-ttu-id="595aa-136">현재 클러스터의 로그는 AI의 로그 뷰어에 추적으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-136">Currently, logs from the cluster will show up as traces in AI's log viewer.</span></span> <span data-ttu-id="595aa-137">플랫폼에서 발생하는 대부분의 추적은 "정보" 수준이므로 "위험" 또는 "오류" 유형의 로그만 보내도록 싱크 구성을 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-137">Since most of the traces coming from the platform are of level "Informational", you can also consider changing the sink configuration to only send logs of type "Critical" or "Error".</span></span> <span data-ttu-id="595aa-138">이 작업은 [이 문서](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md)에서 설명한 것처럼 싱크에 "채널"을 추가하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-138">This can be done by adding "Channels" to your sink, as demonstrated in [this article](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).</span></span>

>[!NOTE]
><span data-ttu-id="595aa-139">포털 또는 Resource Manager 템플릿에서 잘못된 AI IKey를 사용하는 경우 수동으로 키를 변경하고 클러스터를 업데이트/재배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-139">If you use an incorrect AI IKey either in portal or in your Resource Manager template, you will have to manually change the key and update the cluster / redeploy it.</span></span> 

### <a name="configuring-ai-with-eventflow"></a><span data-ttu-id="595aa-140">EventFlow를 사용하여 AI 구성</span><span class="sxs-lookup"><span data-stu-id="595aa-140">Configuring AI with EventFlow</span></span>

<span data-ttu-id="595aa-141">EventFlow를 사용하여 이벤트를 집계하는 경우 `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`NuGet 패키지를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-141">If you are using EventFlow to aggregate events, make sure to import the `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`NuGet package.</span></span> <span data-ttu-id="595aa-142">*eventFlowConfig.json*의 *outputs* 섹션에 다음이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-142">The following has to be included in the *outputs* section of the *eventFlowConfig.json*:</span></span>

```json
"outputs": [
    {
        "type": "ApplicationInsights",
        // (replace the following value with your AI resource's instrumentation key)
        "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
]
```

<span data-ttu-id="595aa-143">필터를 필요한 대로 변경하고 다른 입력(각각의 NuGet 패키지와 함께)도 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-143">Make sure to make the required changes in your filters, as well as include any other inputs (along with their respective NuGet packages).</span></span>

## <a name="aisdk"></a><span data-ttu-id="595aa-144">AI.SDK</span><span class="sxs-lookup"><span data-stu-id="595aa-144">AI.SDK</span></span>

<span data-ttu-id="595aa-145">일반적으로 EventFlow 및 WAD는 진단 및 모니터링에 좀 더 모듈 방식으로 접근할 수 있으므로 집계 솔루션으로 사용하는 것이 좋습니다. 즉, EventFlow의 출력을 변경하려는 경우 실제 계측을 변경할 필요 없이 구성 파일을 간단히 수정하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-145">It is generally recommended to use EventFlow and WAD as aggregation solutions, because they allow for a more modular approach to diagnostics and monitoring, i.e. if you want to change your outputs from EventFlow, it requires no change to your actual instrumentation, just a simple modification to your config file.</span></span> <span data-ttu-id="595aa-146">그러나 Application Insights를 사용하기로 결정하고 다른 플랫폼으로 변경할 가능성이 없는 경우 이벤트를 집계하여 AI에 보내는 작업에 대해 AI의 새 SDK 사용에 대해 살펴봐야 합니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-146">If, however, you decide to invest in using Application Insights and are not likely to change to a different platform, you should look into using AI's new SDK for aggregating events and sending them to AI.</span></span> <span data-ttu-id="595aa-147">즉, 데이터를 AI로 보내도록 EventFlow를 구성할 필요가 없으며 대신 ApplicationInsight의 Service Fabric NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-147">This means that you will no longer have to configure EventFlow to send your data to AI, but instead will install the ApplicationInsight's Service Fabric NuGet package.</span></span> <span data-ttu-id="595aa-148">패키지에 대한 자세한 내용은 [여기](https://github.com/Microsoft/ApplicationInsights-ServiceFabric)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="595aa-148">Details on the package can be found [here](https://github.com/Microsoft/ApplicationInsights-ServiceFabric).</span></span>

<span data-ttu-id="595aa-149">[Application Insights support for Microservices and Containers](https://azure.microsoft.com/app-insights-microservices/)(마이크로 서비스 및 컨테이너에 대한 Application Insights 지원)에서는 작업 중인 새로운 기능 중 일부(현재 베타 버전)를 보여 주며 이를 통해 AI에서 보다 풍부한 기본 모니터링 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-149">[Application Insights support for Microservices and Containers](https://azure.microsoft.com/app-insights-microservices/) shows you some of the new features that are being worked on (currently still in beta), which allow you to have richer out-of-the-box monitoring options with AI.</span></span> <span data-ttu-id="595aa-150">여기에는 종속성 추적(클러스터의 모든 서비스 및 응용 프로그램의 AppMap을 빌드하고 그 사이의 통신을 설정하는 데 사용됨) 및 서비스에서 발생한 추적의 상관 관계가 포함됩니다(앱 또는 서비스의 워크플로 문제를 정확히 발견 가능).</span><span class="sxs-lookup"><span data-stu-id="595aa-150">These include dependency tracking (used in building an AppMap of all your services and applications in a cluster and the communication between them), and better correlation of traces coming from your services (helps in better pinpointing an issue in the workflow of an app or service).</span></span>

<span data-ttu-id="595aa-151">.NET에서 개발 중이고 Service Fabric의 프로그래밍 모델 중 일부를 사용하고 있으며 이벤트 및 로그 데이터를 시각화하고 분석하기 위한 플랫폼으로 AI를 사용하려는 경우 모니터링 및 진단 워크플로인 AI SDK 경로를 통해 이동하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-151">If you are developing in .NET and will likely be using some of Service Fabric's programming models, and are willing to use AI as your platform for visualizing and analyzing event and log data, then we recommend that you go via the AI SDK route as your monitoring and diagnostics workflow.</span></span> <span data-ttu-id="595aa-152">AI를 사용하여 로그를 수집 및 표시하려면 [이 문서](../application-insights/app-insights-asp-net-more.md) 및 [이 문서](../application-insights/app-insights-asp-net-trace-logs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="595aa-152">Read [this](../application-insights/app-insights-asp-net-more.md) and [this](../application-insights/app-insights-asp-net-trace-logs.md) to get started with using AI to collect and display your logs.</span></span>

## <a name="navigating-the-ai-resource-in-azure-portal"></a><span data-ttu-id="595aa-153">Azure Portal에서 AI 리소스 탐색</span><span class="sxs-lookup"><span data-stu-id="595aa-153">Navigating the AI resource in Azure portal</span></span>

<span data-ttu-id="595aa-154">AI를 이벤트 및 로그의 출력으로 구성했으면 몇 분 내에 AI 리소스에 정보가 표시되기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-154">Once you have configured AI as an output for your events and logs, information should start to show up in your AI resource in a few minutes.</span></span> <span data-ttu-id="595aa-155">AI 리소스로 이동하면 AI 리소스 대시보드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-155">Navigate to the AI resource, which will take you to the AI resource dashboard.</span></span> <span data-ttu-id="595aa-156">AI 작업 표시줄에서 **검색**을 클릭하여 수신한 최신 추적을 보고 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-156">Click **Search** in the AI taskbar to see the latest traces that it has received, and to be able to filter through them.</span></span>

<span data-ttu-id="595aa-157">*메트릭 탐색기*는 응용 프로그램, 서비스 및 클러스터가 보고할 수 있는 메트릭을 기반으로 사용자 지정 대시보드를 만드는 데 유용한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-157">*Metrics Explorer* is a useful tool for creating custom dashboards based on metrics that your applications, services, and cluster may be reporting.</span></span> <span data-ttu-id="595aa-158">수집 중인 데이터를 기반으로 직접 몇 가지 차트를 설정하려면 [Application Insights에서 메트릭 탐색](../application-insights/app-insights-metrics-explorer.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="595aa-158">See [Exploring Metrics in Application Insights](../application-insights/app-insights-metrics-explorer.md) to set up a few charts for yourself based on the data you are collecting.</span></span>

<span data-ttu-id="595aa-159">**분석**을 클릭하면 Application Insights 분석 포털로 이동합니다. 이 포털에서는 보다 넓은 범위 및 다양한 옵션으로 이벤트 및 추적을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="595aa-159">Clicking **Analytics** will take you to the Application Insights Analytics portal, where you can query events and traces with greater scope and optionality.</span></span> <span data-ttu-id="595aa-160">자세한 내용은 [Application Insights의 분석](../application-insights/app-insights-analytics.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="595aa-160">Read more about this at [Analytics in Application Insights](../application-insights/app-insights-analytics.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="595aa-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="595aa-161">Next steps</span></span>

* <span data-ttu-id="595aa-162">[AI에 경고 설정](../application-insights/app-insights-alerts.md) - 성능 또는 사용 변경에 대한 알림 받기</span><span class="sxs-lookup"><span data-stu-id="595aa-162">[Set up Alerts in AI](../application-insights/app-insights-alerts.md) to be notified about changes in performance or usage</span></span>
* <span data-ttu-id="595aa-163">[Application Insights의 스마트 감지](../application-insights/app-insights-proactive-diagnostics.md) - 잠재적인 성능 문제를 경고하기 위해 AI에 전송되는 원격 분석에 대한 사전 분석 수행</span><span class="sxs-lookup"><span data-stu-id="595aa-163">[Smart Detection in Application Insights](../application-insights/app-insights-proactive-diagnostics.md) performs a proactive analysis of the telemetry being sent to AI to warn you of potential performance problems</span></span>