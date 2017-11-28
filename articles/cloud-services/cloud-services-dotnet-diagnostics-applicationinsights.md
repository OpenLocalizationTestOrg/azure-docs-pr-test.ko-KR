---
title: "Application Insights를 사용 하 여 클라우드 서비스 aaaTroubleshoot | Microsoft Docs"
description: "Azure 진단에서 Application Insights tooprocess 데이터를 사용 하 여 tootroubleshoot 클라우드 서비스가 발급 하는 방법에 대해 알아봅니다."
services: cloud-services
documentationcenter: .net
author: sbtron
manager: timlt
editor: tysonn
ms.assetid: e93f387b-ef29-4731-ae41-0676722accb6
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: saurabh
ms.openlocfilehash: 972924d9e6d1fe33d5c19b006d482de52ffb0ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-services-using-application-insights"></a><span data-ttu-id="0eade-103">Application Insights를 사용하여 클라우드 서비스 문제 해결</span><span class="sxs-lookup"><span data-stu-id="0eade-103">Troubleshoot Cloud Services using Application Insights</span></span>
<span data-ttu-id="0eade-104">와 [Azure SDK 2.8](https://azure.microsoft.com/downloads/) Azure 진단 확장 1.5를 클라우드 서비스에 대 한 Azure 진단 데이터를 보낼 수 있습니다 및 tooApplication Insights 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-104">With [Azure SDK 2.8](https://azure.microsoft.com/downloads/) and Azure diagnostics extension 1.5, you can send Azure Diagnostics data for your Cloud Service directly tooApplication Insights.</span></span> <span data-ttu-id="0eade-105">Azure 진단에서 수집 된 로그 hello&mdash;응용 프로그램 로그, Windows 이벤트 로그, ETW 로그 및 성능 카운터를 포함 하 여&mdash;tooApplication Insights 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-105">hello logs collected by Azure Diagnostics&mdash;including application logs, Windows Event Logs, ETW Logs, and performance counters&mdash;can be sent tooApplication Insights.</span></span> <span data-ttu-id="0eade-106">그런 다음 hello Application Insights 포털 UI에서에서이 정보를 시각화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-106">You can then visualize this information in hello Application Insights portal UI.</span></span> <span data-ttu-id="0eade-107">그런 다음 hello 메트릭 및 응용 프로그램으로 hello 시스템 및 인프라 수준에서 가져온 데이터를 Azure 진단에서 제공 하는 로그에 대 한 Application Insights SDK tooget 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-107">You can then use hello Application Insights SDK tooget insights into metrics and logs that come from your application, as well as hello system and infrastructure-level data that comes from Azure Diagnostics.</span></span>

## <a name="configure-azure-diagnostics-toosend-data-tooapplication-insights"></a><span data-ttu-id="0eade-108">Azure 진단 toosend 데이터 tooApplication Insights 구성</span><span class="sxs-lookup"><span data-stu-id="0eade-108">Configure Azure Diagnostics toosend data tooApplication Insights</span></span>
<span data-ttu-id="0eade-109">이러한 단계 tooset에 클라우드 서비스 프로젝트 toosend Azure 진단 데이터 tooApplication Insights 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-109">Follow these steps tooset up your cloud service project toosend Azure Diagnostics data tooApplication Insights.</span></span>

1. <span data-ttu-id="0eade-110">Visual Studio 솔루션 탐색기에서 역할을 마우스 오른쪽 단추로 클릭 하 고 선택 **속성** tooopen hello 역할 디자이너입니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-110">In Visual Studio Solution Explorer, right-click a role and select **Properties** tooopen hello Role designer.</span></span>

    ![솔루션 탐색기 역할 속성][1]

2. <span data-ttu-id="0eade-112">Hello에 **진단** 선택 hello hello 역할 디자이너의 섹션 **진단 데이터 tooApplication Insights 보낼** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-112">In hello **Diagnostics** section of hello Role designer, select hello **Send diagnostics data tooApplication Insights** option.</span></span>

    ![역할 디자이너 데이터 tooapplication 인 사이트 진단을 보낼합니다][2]

3. <span data-ttu-id="0eade-114">팝업 되 hello 대화 상자에서 toosend hello Azure 진단 데이터를 원하는 hello Application Insights 리소스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-114">In hello dialog box that pops up, select hello Application Insights resource that you want toosend hello Azure diagnostics data to.</span></span> <span data-ttu-id="0eade-115">hello 대화 상자에서는 tooselect 구독에서 기존 Application Insights 리소스 또는 toomanually Application Insights 리소스에 대 한 계측 키를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-115">hello dialog box allows you tooselect an existing Application Insights resource from your subscription or toomanually specify an instrumentation key for an Application Insights resource.</span></span> <span data-ttu-id="0eade-116">Application Insights 리소스 만들기에 대한 자세한 내용은 [새 Application Insights 리소스 만들기](../application-insights/app-insights-create-new-resource.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0eade-116">For more information on creating an Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md).</span></span>

    ![Application Insights 리소스 선택][3]

    <span data-ttu-id="0eade-118">Hello 이름으로 서비스 구성 설정으로 해당 리소스에 대 한 hello 계측 키가 저장 hello Application Insights 리소스를 추가 하면 **APPINSIGHTS_INSTRUMENTATIONKEY**합니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-118">Once you have added hello Application Insights resource, hello instrumentation key for that resource is stored as a service configuration setting with hello name **APPINSIGHTS_INSTRUMENTATIONKEY**.</span></span> <span data-ttu-id="0eade-119">각 서비스 구성 또는 환경에 대한 이 구성 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-119">You can change this configuration setting for each service configuration or environment.</span></span> <span data-ttu-id="0eade-120">toodo hello에서 서로 다른 구성의 따라서 선택 **서비스 구성** 나열 하 고 해당 구성에 대 한 새 계측 키를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-120">toodo so, select a different configuration from hello **Service Configuration** list and specify a new instrumentation key for that configuration.</span></span>

    ![서비스 구성 선택][4]

    <span data-ttu-id="0eade-122">hello **APPINSIGHTS_INSTRUMENTATIONKEY** 구성 설정을 게시 하는 동안 hello 적절 한 Application Insights 리소스 정보를 Visual Studio tooconfigure hello 진단 확장에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-122">hello **APPINSIGHTS_INSTRUMENTATIONKEY** configuration setting is used by Visual Studio tooconfigure hello diagnostics extension with hello appropriate Application Insights resource information during publishing.</span></span> <span data-ttu-id="0eade-123">hello 구성 설정에는 다른 서비스 구성에 대 한 다른 계측 키 정의 간단한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-123">hello configuration setting is a convenient way of defining different instrumentation keys for different service configurations.</span></span> <span data-ttu-id="0eade-124">Visual Studio는 해당 설정을 변환 하 고 hello 중 hello 진단 확장 공개 구성에 삽입할 프로세스를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-124">Visual Studio will translate that setting and insert it into hello diagnostics extension public configuration during hello publish process.</span></span> <span data-ttu-id="0eade-125">PowerShell을 사용 하 여 hello 진단 확장 구성의 toosimplify hello 프로세스, Visual Studio의 패키지 출력 hello hello 공용 구성 XML hello 적절 한 Application Insights 계측 키로도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-125">toosimplify hello process of configuring hello diagnostics extension with PowerShell, hello package output from Visual Studio also contains hello public configuration XML with hello appropriate Application Insights instrumentation key.</span></span> <span data-ttu-id="0eade-126">hello 공용 구성 파일 hello Extensions 폴더에 생성 되 고 hello 패턴을 따를 *PaaSDiagnostics.&lt; RoleName&gt;합니다. PubConfig.xml*합니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-126">hello public config files are created in hello Extensions folder and follow hello pattern *PaaSDiagnostics.&lt;RoleName&gt;.PubConfig.xml*.</span></span> <span data-ttu-id="0eade-127">모든 PowerShell 기반 배포는 각 구성 tooa 역할 패턴 toomap이 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-127">Any PowerShell-based deployments can use this pattern toomap each configuration tooa role.</span></span>

4) <span data-ttu-id="0eade-128">hello Azure 진단 에이전트가 tooApplication Insights에 의해 수집 된 모든 성능 카운터 및 오류 수준 로그 tooconfigure Azure 진단 toosend hello를 사용 하도록 설정 **진단 데이터 tooApplication Insights 보낼** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-128">tooconfigure Azure diagnostics toosend all performance counters and error-level logs collected by hello Azure diagnostics agent tooApplication Insights, enable hello **Send diagnostics data tooApplication Insights** option.</span></span> 

    <span data-ttu-id="0eade-129">Toofurther 하려는 경우 tooApplication Insights 전송 되는 데이터를 구성, hello를 수동으로 편집 해야 *diagnostics.wadcfgx* 각 역할에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-129">If you want toofurther configure what data is sent tooApplication Insights, you must manually edit hello *diagnostics.wadcfgx* file for each role.</span></span> <span data-ttu-id="0eade-130">참조 [Azure 진단 구성 toosend 데이터 tooApplication Insights](#configure-azure-diagnostics-to-send-data-to-application-insights) toolearn hello 구성을 수동으로 업데이트 하는 방법에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-130">See [Configure Azure Diagnostics toosend data tooApplication Insights](#configure-azure-diagnostics-to-send-data-to-application-insights) toolearn more about manually updating hello configuration.</span></span>

<span data-ttu-id="0eade-131">Hello 클라우드 서비스가 구성 된 toosend Azure 진단 데이터 tooapplication insights 경우 배포할 수 있습니다 tooAzure 일반적으로 이때 hello Azure 진단 확장을 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-131">When hello cloud service is configured toosend Azure diagnostics data tooapplication insights, you can deploy it tooAzure normally, making sure hello Azure diagnostics extension is enabled.</span></span> <span data-ttu-id="0eade-132">자세한 내용은 [Visual Studio를 사용하여 Cloud Service 게시](../vs-azure-tools-publishing-a-cloud-service.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0eade-132">For more information, see  [Publishing a Cloud Service using Visual Studio](../vs-azure-tools-publishing-a-cloud-service.md).</span></span>  

## <a name="viewing-azure-diagnostics-data-in-application-insights"></a><span data-ttu-id="0eade-133">Application Insights에서 Azure 진단 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="0eade-133">Viewing Azure diagnostics data in Application Insights</span></span>
<span data-ttu-id="0eade-134">Azure 진단 원격 분석 hello hello Application Insights 클라우드 서비스에 대해 구성 된 리소스에에서 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-134">hello Azure diagnostic telemetry shows up in hello Application Insights resource configured for your cloud service.</span></span>

<span data-ttu-id="0eade-135">Azure 진단 로그 형식이 매핑되는 다음과 같은이 방법으로 tooApplication Insights 개념:</span><span class="sxs-lookup"><span data-stu-id="0eade-135">Azure diagnostics log types map tooApplication Insights concepts in these ways:</span></span>

* <span data-ttu-id="0eade-136">성능 카운터는 Application Insights에서 사용자 지정 메트릭으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-136">Performance counters are displayed as Custom Metrics in Application Insights.</span></span>
* <span data-ttu-id="0eade-137">Windows 이벤트 로그는 Application Insights에서 추적 및 사용자 지정 이벤트로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-137">Windows Event Logs are shown as Traces and Custom Events in Application Insights.</span></span>
* <span data-ttu-id="0eade-138">응용 프로그램 로그, ETW 로그 및 진단 인프라 로그는 Application Insights에서 추적으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-138">Application logs, ETW logs, and any Diagnostics Infrastructure logs are shown as Traces in Application Insights.</span></span>

<span data-ttu-id="0eade-139">Application Insights에서 Azure 진단 데이터 tooview hello 다음 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-139">tooview Azure diagnostics data in Application Insights, do one of hello following:</span></span>

* <span data-ttu-id="0eade-140">사용 하 여 [메트릭 탐색기](../application-insights/app-insights-metrics-explorer.md) toovisualize 모든 사용자 지정 성능 카운터 또는 다른 유형의 Windows 이벤트 로그 이벤트의 수를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-140">Use [Metrics explorer](../application-insights/app-insights-metrics-explorer.md) toovisualize any custom performance counters or counts of different types of Windows Event Log events.</span></span>

    ![메트릭 탐색기의 사용자 지정 메트릭][5]

* <span data-ttu-id="0eade-142">사용 하 여 [검색](../application-insights/app-insights-diagnostic-search.md) Azure 진단에서 보낸 hello 추적 로그에서 toosearch 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-142">Use [Search](../application-insights/app-insights-diagnostic-search.md) toosearch across hello  trace logs sent by Azure Diagnostics.</span></span> <span data-ttu-id="0eade-143">예를 들어 hello 역할 toocrash 및 재활용 처리 되지 않은 예외 때문에, 경우 hello 예외에 대 한 정보에에서 표시 hello *응용 프로그램* 의 채널 *Windows 이벤트 로그*합니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-143">For example, if an unhandled exception has caused hello role toocrash and recycle, information about hello exception shows up in hello *Application* channel of *Windows Event Log*.</span></span> <span data-ttu-id="0eade-144">Windows 이벤트 로그 오류 hello에 검색 toolook를 사용할 수 있으며 hello 문제의 hello 예외 toohelp 찾기 hello 원인에 대 한 hello 전체 스택 추적이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-144">You can use search toolook at hello Windows Event Log error and get hello full stack trace for hello exception toohelp find hello cause of hello issue.</span></span>

    ![추적 검색][6]

## <a name="next-steps"></a><span data-ttu-id="0eade-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0eade-146">Next Steps</span></span>
* <span data-ttu-id="0eade-147">[Hello Application Insights SDK tooyour 클라우드 서비스를 추가](../application-insights/app-insights-cloudservices.md) toosend 데이터 요청, 예외, 종속성 및 응용 프로그램에서 모든 사용자 지정 원격 분석에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-147">[Add hello Application Insights SDK tooyour cloud service](../application-insights/app-insights-cloudservices.md) toosend data about requests, exceptions, dependencies, and any custom telemetry from your application.</span></span> <span data-ttu-id="0eade-148">Hello Azure 진단 데이터를 응용 프로그램 및 시스템에 대 한 전체 뷰를 가져올 수 있습니다이 정보를 함께 사용 하면 동일한 응용 프로그램 통찰력 리소스를 hello 모두에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eade-148">When combined with hello Azure Diagnostics data, this information you can get a complete view of your application and system, all in hello same Application Insight resource.</span></span>  

<!--Image references-->
[1]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/solution-explorer-properties.png
[2]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-sendtoappinsights.png
[3]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/select-appinsights-resource.png
[4]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-appinsights-serviceconfig.png
[5]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/metrics-explorer-custom-metrics.png
[6]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/search-windowseventlog-error.png
