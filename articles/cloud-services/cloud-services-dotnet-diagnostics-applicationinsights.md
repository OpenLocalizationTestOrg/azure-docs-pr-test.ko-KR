---
title: "Application Insights를 사용하여 클라우드 서비스 문제 해결 | Microsoft Docs"
description: "Application Insights를 통해 Azure 진단의 데이터를 처리하여 클라우드 서비스 문제를 해결하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 4001ca908ff00b1a40829d687589080e9b07b18a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-cloud-services-using-application-insights"></a><span data-ttu-id="e23da-103">Application Insights를 사용하여 클라우드 서비스 문제 해결</span><span class="sxs-lookup"><span data-stu-id="e23da-103">Troubleshoot Cloud Services using Application Insights</span></span>
<span data-ttu-id="e23da-104">[Azure SDK 2.8](https://azure.microsoft.com/downloads/) 및 Azure 진단 확장 1.5를 사용하면 클라우드 서비스에 대한 Azure 진단 데이터를 Application Insights로 직접 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-104">With [Azure SDK 2.8](https://azure.microsoft.com/downloads/) and Azure diagnostics extension 1.5, you can send Azure Diagnostics data for your Cloud Service directly to Application Insights.</span></span> <span data-ttu-id="e23da-105">&mdash;응용 프로그램 로그, Windows 이벤트 로그, ETW 로그 및 성능 카운터를 포함하여&mdash; Azure 진단에서 수집된 로그를 Application Insights에 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-105">The logs collected by Azure Diagnostics&mdash;including application logs, Windows Event Logs, ETW Logs, and performance counters&mdash;can be sent to Application Insights.</span></span> <span data-ttu-id="e23da-106">그런 다음 Application Insights 포털 UI에서 이 정보를 시각화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-106">You can then visualize this information in the Application Insights portal UI.</span></span> <span data-ttu-id="e23da-107">Application Insights SDK를 사용하여 응용 프로그램의 메트릭 및 로그뿐만 아니라 Azure 진단에서 비롯된 시스템 및 인프라 수준 데이터를 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-107">You can then use the Application Insights SDK to get insights into metrics and logs that come from your application, as well as the system and infrastructure-level data that comes from Azure Diagnostics.</span></span>

## <a name="configure-azure-diagnostics-to-send-data-to-application-insights"></a><span data-ttu-id="e23da-108">Application Insights에 데이터를 보내도록 Azure 진단 구성</span><span class="sxs-lookup"><span data-stu-id="e23da-108">Configure Azure Diagnostics to send data to Application Insights</span></span>
<span data-ttu-id="e23da-109">Application Insights로 Azure 진단 데이터를 보내도록 클라우드 서비스 프로젝트를 설정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-109">Follow these steps to set up your cloud service project to send Azure Diagnostics data to Application Insights.</span></span>

1. <span data-ttu-id="e23da-110">Visual Studio 솔루션 탐색기에서 역할을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택하여 역할 디자이너를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-110">In Visual Studio Solution Explorer, right-click a role and select **Properties** to open the Role designer.</span></span>

    ![솔루션 탐색기 역할 속성][1]

2. <span data-ttu-id="e23da-112">역할 디자이너의 **진단** 섹션에서 **진단 데이터를 Application Insights로 보내기** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-112">In the **Diagnostics** section of the Role designer, select the **Send diagnostics data to Application Insights** option.</span></span>

    ![역할 디자이너에서 진단 데이터를 Application Insights로 보내기][2]

3. <span data-ttu-id="e23da-114">팝업으로 나타난 대화 상자에서 Azure 진단 데이터를 전송할 Application Insights 리소스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-114">In the dialog box that pops up, select the Application Insights resource that you want to send the Azure diagnostics data to.</span></span> <span data-ttu-id="e23da-115">이 대화 상자를 사용하면 구독에서 기존 Application Insights 리소스를 선택하거나 Application Insights 리소스에 대한 계측 키를 수동으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-115">The dialog box allows you to select an existing Application Insights resource from your subscription or to manually specify an instrumentation key for an Application Insights resource.</span></span> <span data-ttu-id="e23da-116">Application Insights 리소스 만들기에 대한 자세한 내용은 [새 Application Insights 리소스 만들기](../application-insights/app-insights-create-new-resource.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e23da-116">For more information on creating an Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md).</span></span>

    ![Application Insights 리소스 선택][3]

    <span data-ttu-id="e23da-118">Application Insights 리소스를 추가하고 나면 해당 리소스에 대한 계측 키가 **APPINSIGHTS_INSTRUMENTATIONKEY**라는 이름의 서비스 구성 설정으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-118">Once you have added the Application Insights resource, the instrumentation key for that resource is stored as a service configuration setting with the name **APPINSIGHTS_INSTRUMENTATIONKEY**.</span></span> <span data-ttu-id="e23da-119">각 서비스 구성 또는 환경에 대한 이 구성 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-119">You can change this configuration setting for each service configuration or environment.</span></span> <span data-ttu-id="e23da-120">이렇게 하려면 **서비스 구성** 목록에서 다른 구성을 선택하고 해당 구성에 대한 새 계측 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-120">To do so, select a different configuration from the **Service Configuration** list and specify a new instrumentation key for that configuration.</span></span>

    ![서비스 구성 선택][4]

    <span data-ttu-id="e23da-122">**APPINSIGHTS_INSTRUMENTATIONKEY** 구성 설정은 게시 중 Visual Studio에서 적절한 Application Insights 리소스 정보로 진단 확장을 구성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-122">The **APPINSIGHTS_INSTRUMENTATIONKEY** configuration setting is used by Visual Studio to configure the diagnostics extension with the appropriate Application Insights resource information during publishing.</span></span> <span data-ttu-id="e23da-123">구성 설정을 사용하면 각 서비스 구성에 대해 다른 계측 키를 편리하게 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-123">The configuration setting is a convenient way of defining different instrumentation keys for different service configurations.</span></span> <span data-ttu-id="e23da-124">Visual Studio는 해당 설정을 변환하여 게시 프로세스 중에 진단 확장 공용 구성에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-124">Visual Studio will translate that setting and insert it into the diagnostics extension public configuration during the publish process.</span></span> <span data-ttu-id="e23da-125">PowerShell을 사용한 진단 확장 구성 프로세스를 단순화하기 위해 Visual Studio의 패키지 출력에도 적절한 Application Insights 계측 키와 함께 공용 구성 XML이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-125">To simplify the process of configuring the diagnostics extension with PowerShell, the package output from Visual Studio also contains the public configuration XML with the appropriate Application Insights instrumentation key.</span></span> <span data-ttu-id="e23da-126">공용 config 파일이 Extensions 폴더에서 생성되고 *PaaSDiagnostics.&lt;RoleName&gt;.PubConfig.xml* 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-126">The public config files are created in the Extensions folder and follow the pattern *PaaSDiagnostics.&lt;RoleName&gt;.PubConfig.xml*.</span></span> <span data-ttu-id="e23da-127">모든 PowerShell 기반 배포에서 이 패턴을 사용하여 각 구성을 역할에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-127">Any PowerShell-based deployments can use this pattern to map each configuration to a role.</span></span>

4) <span data-ttu-id="e23da-128">Azure 진단 에이전트에 의해 수집된 모든 성능 카운터 및 오류 수준 로그를 Application Insights로 보내도록 Azure 진단이 자동으로 구성하려면 **진단 데이터를 Application Insights로 보내기** 옵션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-128">To configure Azure diagnostics to send all performance counters and error-level logs collected by the Azure diagnostics agent to Application Insights, enable the **Send diagnostics data to Application Insights** option.</span></span> 

    <span data-ttu-id="e23da-129">Application Insights로 보낼 데이터를 추가로 구성하려는 경우 각 역할에 대한 *diagnostics.wadcfgx* 파일을 수동으로 편집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-129">If you want to further configure what data is sent to Application Insights, you must manually edit the *diagnostics.wadcfgx* file for each role.</span></span> <span data-ttu-id="e23da-130">구성을 수동으로 업데이트하는 방법에 대한 자세한 내용은 [Application Insights에 데이터를 보내도록 Azure 진단 구성](#configure-azure-diagnostics-to-send-data-to-application-insights) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e23da-130">See [Configure Azure Diagnostics to send data to Application Insights](#configure-azure-diagnostics-to-send-data-to-application-insights) to learn more about manually updating the configuration.</span></span>

<span data-ttu-id="e23da-131">Azure 진단 데이터를 Application Insights로 보내도록 클라우드 서비스를 구성하면 일반적인 방법으로 Azure에 배포하여 Azure 진단 확장이 사용되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-131">When the cloud service is configured to send Azure diagnostics data to application insights, you can deploy it to Azure normally, making sure the Azure diagnostics extension is enabled.</span></span> <span data-ttu-id="e23da-132">자세한 내용은 [Visual Studio를 사용하여 Cloud Service 게시](../vs-azure-tools-publishing-a-cloud-service.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e23da-132">For more information, see  [Publishing a Cloud Service using Visual Studio](../vs-azure-tools-publishing-a-cloud-service.md).</span></span>  

## <a name="viewing-azure-diagnostics-data-in-application-insights"></a><span data-ttu-id="e23da-133">Application Insights에서 Azure 진단 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="e23da-133">Viewing Azure diagnostics data in Application Insights</span></span>
<span data-ttu-id="e23da-134">Azure 진단 원격 분석이 해당 클라우드 서비스에 대해 구성된 Application Insights 리소스에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-134">The Azure diagnostic telemetry shows up in the Application Insights resource configured for your cloud service.</span></span>

<span data-ttu-id="e23da-135">Azure 진단 로그 형식은 다음과 같은 방법으로 Application Insights 개념에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-135">Azure diagnostics log types map to Application Insights concepts in these ways:</span></span>

* <span data-ttu-id="e23da-136">성능 카운터는 Application Insights에서 사용자 지정 메트릭으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-136">Performance counters are displayed as Custom Metrics in Application Insights.</span></span>
* <span data-ttu-id="e23da-137">Windows 이벤트 로그는 Application Insights에서 추적 및 사용자 지정 이벤트로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-137">Windows Event Logs are shown as Traces and Custom Events in Application Insights.</span></span>
* <span data-ttu-id="e23da-138">응용 프로그램 로그, ETW 로그 및 진단 인프라 로그는 Application Insights에서 추적으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-138">Application logs, ETW logs, and any Diagnostics Infrastructure logs are shown as Traces in Application Insights.</span></span>

<span data-ttu-id="e23da-139">Application Insights에서 Azure 진단 데이터를 보려면 다음 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-139">To view Azure diagnostics data in Application Insights, do one of the following:</span></span>

* <span data-ttu-id="e23da-140">[메트릭 탐색기](../application-insights/app-insights-metrics-explorer.md) 를 사용하여 사용자 지정 성능 카운터 또는 다양한 형식의 Windows 이벤트 로그 이벤트 수를 시각화합니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-140">Use [Metrics explorer](../application-insights/app-insights-metrics-explorer.md) to visualize any custom performance counters or counts of different types of Windows Event Log events.</span></span>

    ![메트릭 탐색기의 사용자 지정 메트릭][5]

* <span data-ttu-id="e23da-142">[검색](../application-insights/app-insights-diagnostic-search.md)을 사용하여 Azure 진단에서 보낸 추적 로그를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-142">Use [Search](../application-insights/app-insights-diagnostic-search.md) to search across the  trace logs sent by Azure Diagnostics.</span></span> <span data-ttu-id="e23da-143">예를 들어 처리되지 않은 예외로 인해 역할에 충돌 및 재활용이 발생하는 경우 해당 정보가 *Windows 이벤트 로그*의 *응용 프로그램* 채널에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-143">For example, if an unhandled exception has caused the role to crash and recycle, information about the exception shows up in the *Application* channel of *Windows Event Log*.</span></span> <span data-ttu-id="e23da-144">검색을 사용하여 Windows 이벤트 로그 오류를 살펴보고 예외에 대한 전체 스택 추적을 가져와서 문제의 원인을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-144">You can use search to look at the Windows Event Log error and get the full stack trace for the exception to help find the cause of the issue.</span></span>

    ![추적 검색][6]

## <a name="next-steps"></a><span data-ttu-id="e23da-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e23da-146">Next Steps</span></span>
* <span data-ttu-id="e23da-147">[Application Insights SDK를 클라우드 서비스에 추가](../application-insights/app-insights-cloudservices.md) 하여 응용 프로그램에서 요청, 예외, 종속성 및 모든 사용자 지정 원격 분석에 대한 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-147">[Add the Application Insights SDK to your cloud service](../application-insights/app-insights-cloudservices.md) to send data about requests, exceptions, dependencies, and any custom telemetry from your application.</span></span> <span data-ttu-id="e23da-148">Azure 진단 데이터와 함께 사용하는 경우 이 정보를 통해 동일한 Application Insight 리소스에 있는 모든 응용 프로그램 및 시스템을 전체적으로 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23da-148">When combined with the Azure Diagnostics data, this information you can get a complete view of your application and system, all in the same Application Insight resource.</span></span>  

<!--Image references-->
[1]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/solution-explorer-properties.png
[2]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-sendtoappinsights.png
[3]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/select-appinsights-resource.png
[4]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-appinsights-serviceconfig.png
[5]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/metrics-explorer-custom-metrics.png
[6]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/search-windowseventlog-error.png
