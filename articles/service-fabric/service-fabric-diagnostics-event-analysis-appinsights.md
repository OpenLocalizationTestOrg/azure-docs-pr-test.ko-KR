---
title: "Application Insights를 사용 하 여 서비스 패브릭 이벤트 분석 aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 59bb5a409f2951e5b2034049e782dd0da67f933c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-analysis-and-visualization-with-application-insights"></a><span data-ttu-id="e10f0-103">Application Insights를 사용하여 이벤트 분석 및 시각화</span><span class="sxs-lookup"><span data-stu-id="e10f0-103">Event analysis and visualization with Application Insights</span></span>

<span data-ttu-id="e10f0-104">Azure Application Insights는 응용 프로그램 모니터링 및 진단을 위한 확장 가능한 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-104">Azure Application Insights is an extensible platform for application monitoring and diagnostics.</span></span> <span data-ttu-id="e10f0-105">여기에는 강력한 분석 및 쿼리 도구, 사용자 지정 가능한 대시보드 및 시각화, 자동화된 경고 등의 추가 옵션이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-105">It includes a powerful analytics and querying tool, customizable dashboard and visualizations, and further options including automated alerting.</span></span> <span data-ttu-id="e10f0-106">이 권장 모니터링 하기 위한 플랫폼 및 서비스 패브릭 응용 프로그램 및 서비스에 대 한 진단 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-106">It is hello recommended platform for monitoring and diagnostics for Service Fabric applications and services.</span></span>

## <a name="setting-up-application-insights"></a><span data-ttu-id="e10f0-107">Application Insights 설정</span><span class="sxs-lookup"><span data-stu-id="e10f0-107">Setting up Application Insights</span></span>

### <a name="creating-an-ai-resource"></a><span data-ttu-id="e10f0-108">AI 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="e10f0-108">Creating an AI Resource</span></span>

<span data-ttu-id="e10f0-109">Azure 마켓플레이스 toohello 및 "Application Insights" 검색을 통해 헤드는 AI toocreate 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-109">toocreate an AI resource, head over toohello Azure Marketplace, and search for "Application Insights".</span></span> <span data-ttu-id="e10f0-110">Hello 첫 번째 솔루션 (에 "웹 + 모바일" 범주 아래)으로 보입니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-110">It should show up as hello first solution (it is under category "Web + Mobile").</span></span> <span data-ttu-id="e10f0-111">클릭 **만들기** hello 오른쪽 리소스를 찾을 때 (사용자의 경로 아래 hello 이미지와 일치 하는지 확인).</span><span class="sxs-lookup"><span data-stu-id="e10f0-111">Click **Create** when you are looking at hello right resource (confirm that your path matches hello image below).</span></span>

![새 Application Insights 리소스](media/service-fabric-diagnostics-event-analysis-appinsights/create-new-ai-resource.png)

<span data-ttu-id="e10f0-113">몇 가지 정보 tooprovision hello 리소스 아웃 toofill 올바르게 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-113">You will need toofill out some information tooprovision hello resource correctly.</span></span> <span data-ttu-id="e10f0-114">Hello에 *응용 프로그램 종류* "ASP.NET 웹 응용 프로그램"를 사용 하 여 사용 하려는 서비스 패브릭의 경우의 프로그래밍 모델 또는 게시 하는.NET 응용 프로그램 toohello 클러스터에는 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-114">In hello *Application Type* field, use "ASP.NET web application" if you will be using any of Service Fabric's programming models or publishing a .NET application toohello cluster.</span></span> <span data-ttu-id="e10f0-115">게스트 실행 파일과 컨테이너를 배포하려면 "일반"을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-115">Use "General" if you will be deploying guest executables and containers.</span></span> <span data-ttu-id="e10f0-116">일반적으로 기본 toousing "ASP.NET 웹 응용 프로그램" tookeep 옵션에서에서 열기 이후 hello</span><span class="sxs-lookup"><span data-stu-id="e10f0-116">In general, default toousing "ASP.NET web application" tookeep your options open in hello future.</span></span> <span data-ttu-id="e10f0-117">hello 이름은 tooyour 우선, 위로 이며 hello 리소스 그룹 및 구독을 모두는 hello 리소스의 배포 후 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-117">hello name is up tooyour preference, and both hello resource group and subscription are changeable post-deployment of hello resource.</span></span> <span data-ttu-id="e10f0-118">AI 리소스가 hello 인지 하는 것이 좋습니다 클러스터와 동일한 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-118">We recommend that your AI resource is in hello same resource group as your cluster.</span></span> <span data-ttu-id="e10f0-119">자세한 내용은 [Application Insights 리소스 만들기](../application-insights/app-insights-create-new-resource.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e10f0-119">If you need more information, please see [Create an Application Insights resource](../application-insights/app-insights-create-new-resource.md)</span></span>

<span data-ttu-id="e10f0-120">이벤트 집계 도구와 hello AI 계측 키 tooconfigure AI 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-120">You need hello AI Instrumentation Key tooconfigure AI with your event aggregation tool.</span></span> <span data-ttu-id="e10f0-121">AI 리소스가 (hello 배포의 유효성을 검사 한 후 몇 분이 걸립니다) 설정 되 고 나면 tooit 이동한 hello **속성** hello 왼쪽된 탐색 모음에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="e10f0-121">Once your AI resource is set up (takes a few minutes after hello deployment is validated), navigate tooit and find hello **Properties** section on hello left navigation bar.</span></span> <span data-ttu-id="e10f0-122">*계측 키*를 보여 주는 새 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-122">A new blade will open up that shows an *INSTRUMENTATION KEY*.</span></span> <span data-ttu-id="e10f0-123">Toochange hello 구독 또는 hello 리소스의 리소스 그룹을 해야 하는 경우 수행할 수 있습니다 여기 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-123">If you need toochange hello subscription or resource group of hello resource, it can be done here as well.</span></span>

### <a name="configuring-ai-with-wad"></a><span data-ttu-id="e10f0-124">WAD를 사용하여 AI 구성</span><span class="sxs-lookup"><span data-stu-id="e10f0-124">Configuring AI with WAD</span></span>

<span data-ttu-id="e10f0-125">두 가지 기본 단계에서 설명한 대로 AI 싱크 toohello WAD 구성을 추가 하 여 이루어집니다 WAD tooAzure AI에서에서 toosend 데이터 [이 여기서](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-125">There are two primary ways toosend data from WAD tooAzure AI, which is achieved by adding an AI sink toohello WAD configuration, as detailed in [this article](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).</span></span>

#### <a name="add-an-ai-instrumentation-key-when-creating-a-cluster-in-azure-portal"></a><span data-ttu-id="e10f0-126">Azure Portal에서 클러스터를 만들 때 AI 계측 키 추가</span><span class="sxs-lookup"><span data-stu-id="e10f0-126">Add an AI Instrumentation Key when creating a cluster in Azure portal</span></span>

![AIKey 추가](media/service-fabric-diagnostics-event-analysis-appinsights/azure-enable-diagnostics.png)

<span data-ttu-id="e10f0-128">클러스터 진단 "on"으로 설정 되어 있으면를 만들 때 필드는 선택 사항 tooenter 응용 프로그램 Insights 계측 키가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-128">When creating a cluster, if Diagnostics is turned "On", an optional field tooenter an Application Insights Instrumentation key will show.</span></span> <span data-ttu-id="e10f0-129">여기에 AI IKey에 붙여 넣으면 hello AI 싱크에 자동으로 지워집니다 자동으로 구성에 사용 되는 toodeploy hello 리소스 관리자 템플릿을 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-129">If you paste your AI IKey here, hello AI sink will be automatically configured for you in hello Resource Manager template that is used toodeploy your cluster.</span></span>

#### <a name="add-hello-ai-sink-toohello-resource-manager-template"></a><span data-ttu-id="e10f0-130">Hello AI 싱크 toohello 리소스 관리자 템플릿 추가</span><span class="sxs-lookup"><span data-stu-id="e10f0-130">Add hello AI Sink toohello Resource Manager template</span></span>

<span data-ttu-id="e10f0-131">리소스 관리자 템플릿 hello "WadCfg" hello에서 다음 두 가지 변경 내용이 hello를 포함 하 여 "Sink"를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-131">In hello "WadCfg" of hello Resource Manager template, add a "Sink" by including hello following two changes:</span></span>

1. <span data-ttu-id="e10f0-132">Hello 싱크 구성 추가:</span><span class="sxs-lookup"><span data-stu-id="e10f0-132">Add hello sink configuration:</span></span>

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

2. <span data-ttu-id="e10f0-133">다음 줄에 "DiagnosticMonitorConfiguration" hello "WadCfg" hello의 추가 하 여 hello를 싱크 DiagnosticMonitorConfiguration hello에 포함 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-133">Include hello Sink in hello DiagnosticMonitorConfiguration by adding hello following line in "DiagnosticMonitorConfiguration" of hello "WadCfg":</span></span>

    ```json
    "sinks": "applicationInsights"
    ```

<span data-ttu-id="e10f0-134">Hello 위의 두 hello 코드 조각에 사용 되는 toodescribe hello 싱크 된 이름은 "applicationInsights"입니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-134">In both hello code snippets above, hello name "applicationInsights" was used toodescribe hello sink.</span></span> <span data-ttu-id="e10f0-135">필요 하지 않습니다 및 hello 이름 tooany 문자열 hello 싱크의 hello 이름을 "싱크" ´ â,으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-135">This is not a requirement and as long as hello name of hello sink is included in "sinks", you can set hello name tooany string.</span></span>

<span data-ttu-id="e10f0-136">현재 로그 hello 클러스터에서로 표시 됩니다 AI의 로그 뷰어에서 추적을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="e10f0-136">Currently, logs from hello cluster will show up as traces in AI's log viewer.</span></span> <span data-ttu-id="e10f0-137">대부분의 hello 플랫폼에서 들어오는 hello 추적 수준 "Informational" 이므로 "Critical" 또는 "Error" 유형의 hello 싱크 구성 tooonly 송신 로그 변경을 고려해볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-137">Since most of hello traces coming from hello platform are of level "Informational", you can also consider changing hello sink configuration tooonly send logs of type "Critical" or "Error".</span></span> <span data-ttu-id="e10f0-138">이렇게 "채널" tooyour 싱크를 추가 하 여에서 같이 [이 여기서](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-138">This can be done by adding "Channels" tooyour sink, as demonstrated in [this article](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).</span></span>

>[!NOTE]
><span data-ttu-id="e10f0-139">잘못 된 AI IKey을 포털에서 또는 리소스 관리자 템플릿을 사용 하면 toomanually hello 키 변경 / 업데이트 hello 클러스터 및 다시 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-139">If you use an incorrect AI IKey either in portal or in your Resource Manager template, you will have toomanually change hello key and update hello cluster / redeploy it.</span></span> 

### <a name="configuring-ai-with-eventflow"></a><span data-ttu-id="e10f0-140">EventFlow를 사용하여 AI 구성</span><span class="sxs-lookup"><span data-stu-id="e10f0-140">Configuring AI with EventFlow</span></span>

<span data-ttu-id="e10f0-141">EventFlow tooaggregate 이벤트를 사용 하는 경우 확인 되었는지 tooimport hello `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-141">If you are using EventFlow tooaggregate events, make sure tooimport hello `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`NuGet package.</span></span> <span data-ttu-id="e10f0-142">hello 다음에 hello에 포함 된 toobe *출력* hello 섹션 *eventFlowConfig.json*:</span><span class="sxs-lookup"><span data-stu-id="e10f0-142">hello following has toobe included in hello *outputs* section of hello *eventFlowConfig.json*:</span></span>

```json
"outputs": [
    {
        "type": "ApplicationInsights",
        // (replace hello following value with your AI resource's instrumentation key)
        "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
]
```

<span data-ttu-id="e10f0-143">필터를 있는지 toomake hello 필요한 변경 작업을 수행할으로 해당 NuGet 패키지) (함께 다른 입력을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-143">Make sure toomake hello required changes in your filters, as well as include any other inputs (along with their respective NuGet packages).</span></span>

## <a name="aisdk"></a><span data-ttu-id="e10f0-144">AI.SDK</span><span class="sxs-lookup"><span data-stu-id="e10f0-144">AI.SDK</span></span>

<span data-ttu-id="e10f0-145">일반적으로 toouse EventFlow 좋습니다 및 집계 솔루션으로 WAD 모듈식 방법 toodiagnostics을 허용 하 고 실제 변경 tooyour 없습니다 필요한 경우에 모니터링, 즉, toochange EventFlow 프로그램 출력을 원하는, 때문에 계측을 간단히 수정 tooyour config 파일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-145">It is generally recommended toouse EventFlow and WAD as aggregation solutions, because they allow for a more modular approach toodiagnostics and monitoring, i.e. if you want toochange your outputs from EventFlow, it requires no change tooyour actual instrumentation, just a simple modification tooyour config file.</span></span> <span data-ttu-id="e10f0-146">하지만 tooinvest Application Insights를 사용 하 여 결정 없는 가능성이 toochange tooa 다른 플랫폼을 하는 경우 AI의 새 SDK를 사용 하 여 이벤트를 집계 하 고 tooAI 보내 살펴보아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-146">If, however, you decide tooinvest in using Application Insights and are not likely toochange tooa different platform, you should look into using AI's new SDK for aggregating events and sending them tooAI.</span></span> <span data-ttu-id="e10f0-147">즉, 사용자가 더 이상 tooconfigure EventFlow toosend 사용자 데이터 tooAI 있지만 대신 hello ApplicationInsight 서비스 패브릭 NuGet 패키지 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-147">This means that you will no longer have tooconfigure EventFlow toosend your data tooAI, but instead will install hello ApplicationInsight's Service Fabric NuGet package.</span></span> <span data-ttu-id="e10f0-148">Hello 패키지에 대 한 자세한 내용은 [여기](https://github.com/Microsoft/ApplicationInsights-ServiceFabric)합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-148">Details on hello package can be found [here](https://github.com/Microsoft/ApplicationInsights-ServiceFabric).</span></span>

<span data-ttu-id="e10f0-149">[Application Insights Microservices 및 컨테이너에 대 한 지원](https://azure.microsoft.com/app-insights-microservices/) 일부를 보여 줍니다 (여전히 현재 베타) 작업 중인 하는 새로운 기능 hello, 수 있도록 허용 하기 AI와 toohave 제공 하는 기본적으로 다양 한 모니터링 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-149">[Application Insights support for Microservices and Containers](https://azure.microsoft.com/app-insights-microservices/) shows you some of hello new features that are being worked on (currently still in beta), which allow you toohave richer out-of-the-box monitoring options with AI.</span></span> <span data-ttu-id="e10f0-150">여기에 추적 (더 나은 매크로나 hello에서 문제에 사용 하면 서비스에서 오는의 더 나은 상관 관계 및 종속성 추적 (모든 서비스 및 응용 프로그램 간에 클러스터 및 hello 통신의 AppMap 작성에 사용 됨) 워크플로 응용 프로그램 또는 서비스의)입니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-150">These include dependency tracking (used in building an AppMap of all your services and applications in a cluster and hello communication between them), and better correlation of traces coming from your services (helps in better pinpointing an issue in hello workflow of an app or service).</span></span>

<span data-ttu-id="e10f0-151">.NET에서 개발 하는 고 될 경우 일부 서비스 패브릭 프로그래밍 모델을 사용 하며 기꺼이 toouse AI를 시각화 하는 이동 hello를 통해 모니터링으로 AI SDK 경로 것이 좋습니다 이벤트 및 로그 데이터를 분석 하기 위한 플랫폼 및 진단 워크플로입니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-151">If you are developing in .NET and will likely be using some of Service Fabric's programming models, and are willing toouse AI as your platform for visualizing and analyzing event and log data, then we recommend that you go via hello AI SDK route as your monitoring and diagnostics workflow.</span></span> <span data-ttu-id="e10f0-152">읽기 [이](../application-insights/app-insights-asp-net-more.md) 및 [이](../application-insights/app-insights-asp-net-trace-logs.md) tooget AI toocollect를 사용 하 여 시작 하 고 로그를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-152">Read [this](../application-insights/app-insights-asp-net-more.md) and [this](../application-insights/app-insights-asp-net-trace-logs.md) tooget started with using AI toocollect and display your logs.</span></span>

## <a name="navigating-hello-ai-resource-in-azure-portal"></a><span data-ttu-id="e10f0-153">Hello AI 리소스가 Azure 포털에서 탐색</span><span class="sxs-lookup"><span data-stu-id="e10f0-153">Navigating hello AI resource in Azure portal</span></span>

<span data-ttu-id="e10f0-154">AI 이벤트 및 로그에 대 한 출력으로 구성한 후 정보 시작 해야 tooshow AI 리소스가 몇 분 후에서입니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-154">Once you have configured AI as an output for your events and logs, information should start tooshow up in your AI resource in a few minutes.</span></span> <span data-ttu-id="e10f0-155">이 하면 toohello AI 리소스 대시보드를 toohello AI 리소스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-155">Navigate toohello AI resource, which will take you toohello AI resource dashboard.</span></span> <span data-ttu-id="e10f0-156">클릭 **검색** hello AI 작업 표시줄 toosee hello 최신 하는 추적, 수신한 및 toobe 수 toofilter 표시가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-156">Click **Search** in hello AI taskbar toosee hello latest traces that it has received, and toobe able toofilter through them.</span></span>

<span data-ttu-id="e10f0-157">*메트릭 탐색기*는 응용 프로그램, 서비스 및 클러스터가 보고할 수 있는 메트릭을 기반으로 사용자 지정 대시보드를 만드는 데 유용한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-157">*Metrics Explorer* is a useful tool for creating custom dashboards based on metrics that your applications, services, and cluster may be reporting.</span></span> <span data-ttu-id="e10f0-158">참조 [Application Insights에서 메트릭을 탐색](../application-insights/app-insights-metrics-explorer.md) 자신에 대 한 몇 가지 차트를 tooset hello 데이터를 수집 하는 기준입니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-158">See [Exploring Metrics in Application Insights](../application-insights/app-insights-metrics-explorer.md) tooset up a few charts for yourself based on hello data you are collecting.</span></span>

<span data-ttu-id="e10f0-159">클릭 하면 **분석** 걸립니다 toohello 응용 프로그램 통찰력 분석 포털 이벤트 및 큰 범위 및 옵션을 사용 하 여 추적을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e10f0-159">Clicking **Analytics** will take you toohello Application Insights Analytics portal, where you can query events and traces with greater scope and optionality.</span></span> <span data-ttu-id="e10f0-160">자세한 내용은 [Application Insights의 분석](../application-insights/app-insights-analytics.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e10f0-160">Read more about this at [Analytics in Application Insights](../application-insights/app-insights-analytics.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e10f0-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e10f0-161">Next steps</span></span>

* <span data-ttu-id="e10f0-162">[AI에서 경고를 설정](../application-insights/app-insights-alerts.md) toobe 변경 성능 및 사용 현황에 대 한 알림이 표시</span><span class="sxs-lookup"><span data-stu-id="e10f0-162">[Set up Alerts in AI](../application-insights/app-insights-alerts.md) toobe notified about changes in performance or usage</span></span>
* <span data-ttu-id="e10f0-163">[Application Insights에서 검색을 스마트](../application-insights/app-insights-proactive-diagnostics.md) 사전 분석 tooAI toowarn 송신할 hello 원격 분석을 수행 하면 잠재적 성능 문제</span><span class="sxs-lookup"><span data-stu-id="e10f0-163">[Smart Detection in Application Insights](../application-insights/app-insights-proactive-diagnostics.md) performs a proactive analysis of hello telemetry being sent tooAI toowarn you of potential performance problems</span></span>
