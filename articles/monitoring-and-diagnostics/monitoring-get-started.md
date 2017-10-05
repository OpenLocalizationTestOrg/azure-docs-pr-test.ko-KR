---
title: "Azure Monitor 시작 | Microsoft Docs"
description: "Azure Monitor로 리소스 작업에 대한 정보를 확보하고 데이터 기반 조치를 취합니다."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ce2930aa-fc41-4b81-b0cb-e7ea922467e1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: johnkem
ms.openlocfilehash: a4871cdee882fae8e43f84ce4f2fa0b4c0a8e1de
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-monitor"></a><span data-ttu-id="5da67-103">Azure Monitor 시작</span><span class="sxs-lookup"><span data-stu-id="5da67-103">Get started with Azure Monitor</span></span>
<span data-ttu-id="5da67-104">Azure Monitor는 Azure 리소스를 모니터링하는 단일 원본이 되는 플랫폼 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-104">Azure Monitor is the platform service that provides a single source for monitoring Azure resources.</span></span> <span data-ttu-id="5da67-105">Azure에서 Azure Monitor를 통해 리소스의 메트릭과 로그에 대해 시각화, 쿼리, 라우팅, 보관 및 조치를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-105">With Azure Monitor, you can visualize, query, route, archive, and take action on the metrics and logs coming from resources in Azure.</span></span> <span data-ttu-id="5da67-106">모니터 포털 블레이드, [Monitor PowerShell Cmdlet](insights-powershell-samples.md), [플랫폼 간 CLI](insights-cli-samples.md) 또는 [Azure Monitor REST API](https://msdn.microsoft.com/library/dn931943.aspx)를 사용하는 데이터를 통해 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-106">You can work with this data using the Monitor portal blade, [Monitor PowerShell Cmdlets](insights-powershell-samples.md), [Cross-Platform CLI](insights-cli-samples.md), or [Azure Monitor REST APIs](https://msdn.microsoft.com/library/dn931943.aspx).</span></span> <span data-ttu-id="5da67-107">이 문서에서는 데모용 포털을 사용하여 Azure Monitor의 몇 가지 주요 구성 요소에 대해 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-107">In this article, we walk through a few of the key components of Azure Monitor, using the portal for demonstration.</span></span>

1. <span data-ttu-id="5da67-108">포털에서 **더 많은 서비스**로 이동하고 **모니터** 옵션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-108">In the portal, navigate to **More services** and find the **Monitor** option.</span></span> <span data-ttu-id="5da67-109">왼쪽 탐색 표시줄에서 항상 쉽게 액세스할 수 있게 별 모양 아이콘을 클릭하여 이 옵션을 즐겨찾기 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-109">Click the star icon to add this option to your favorites list so that it is always easily accessible from the left-hand navigation bar.</span></span>
   
    ![서비스 목록의 모니터 ](./media/monitoring-get-started/monitor-more-services.png)
2. <span data-ttu-id="5da67-111">**모니터** 옵션을 클릭하여 **모니터** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-111">Click the **Monitor** option to open up the **Monitor** blade.</span></span> <span data-ttu-id="5da67-112">이 블레이드에서는 모든 모니터링 설정과 데이터를 하나의 통합 보기로 모읍니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-112">This blade brings together all your monitoring settings and data into one consolidated view.</span></span> <span data-ttu-id="5da67-113">처음에는 **활동 로그** 섹션이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-113">It first opens to the **Activity log** section.</span></span>
   
    ![모니터 블레이드 탐색](./media/monitoring-get-started/monitor-blade-nav.png)
   
    <span data-ttu-id="5da67-115">Azure Monitor에는 데이터 모니터링의 3가지 기본 범주, 즉 **활동 로그**, **메트릭** 및 **진단 로그**가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-115">Azure Monitor has three basic categories of monitoring data: The **activity log**, **metrics**, and **diagnostic logs**.</span></span>
3. <span data-ttu-id="5da67-116">**활동 로그** 를 클릭하여 활동 로그 섹션이 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-116">Click **Activity log** to ensure that the activity log section is displayed.</span></span>
   
    ![활동 로그 블레이드](./media/monitoring-get-started/monitor-act-log-blade.png)
   
    <span data-ttu-id="5da67-118">[**활동 로그**](monitoring-overview-activity-logs.md)는 구독에서 리소스에 대해 수행한 모든 작업을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-118">The [**activity log**](monitoring-overview-activity-logs.md) describes all operations performed on resources in your subscription.</span></span> <span data-ttu-id="5da67-119">구독에서 활동 로그를 통해 리소스에 수행된 만들기, 업데이트 또는 삭제 작업에 대해 ‘누가, 무엇을, 언제’를 판단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-119">Using the Activity Log, you can determine the ‘what, who, and when’ for any create, update, or delete operations on resources in your subscription.</span></span> <span data-ttu-id="5da67-120">예를 들어 활동 로그를 통해 웹앱이 중지된 시기와 웹앱을 중지한 사람을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-120">For example, the Activity Log tells you when a web app was stopped and who stopped it.</span></span> <span data-ttu-id="5da67-121">활동 로그 이벤트는 90일 동안 플랫폼에 저장되어 쿼리에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-121">Activity Log events are stored in the platform and available to query for 90 days.</span></span>
   
    <span data-ttu-id="5da67-122">공통 필터에 대한 쿼리를 만들어 저장한 다음 가장 중요한 쿼리를 포털 대시보드에 고정하면 기준에 부합하는 이벤트가 발생할 경우 항상 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-122">You can create and save queries for common filters, then pin the most important queries to a portal dashboard so you'll always know if events that meet your criteria have occurred.</span></span>
4. <span data-ttu-id="5da67-123">지난 주의 특정 리소스 그룹에 대해 보기를 필터링한 다음 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-123">Filter the view to a particular resource group over the last week, then click the **Save** button.</span></span>
   
    ![활동 로그 쿼리 저장](./media/monitoring-get-started/monitor-act-log-save.png)
5. <span data-ttu-id="5da67-125">이제 **고정** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-125">Now, click the **Pin** button.</span></span>
   
    ![활동 로그에 대한 고정 클릭](./media/monitoring-get-started/monitor-act-log-pin.png)
   
    <span data-ttu-id="5da67-127">이 연습의 보기 대부분을 대시보드에 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-127">Most of the views in this walkthrough can be pinned to a dashboard.</span></span> <span data-ttu-id="5da67-128">이렇게 하면 서비스에 대한 운영 데이터 정보를 제공하는 단일 출처를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-128">This helps you create a single source of information for operational data on your services.</span></span> 
6. <span data-ttu-id="5da67-129">대시보드로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-129">Return to your dashboard.</span></span> <span data-ttu-id="5da67-130">이제 쿼리(및 결과 수)가 대시보드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-130">You can now see that the query (and number of results) is displayed in your dashboard.</span></span> <span data-ttu-id="5da67-131">신속 하 게에서 발생 한 최근 구독, 예: 높은 작업을 확인 하려는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-131">This is useful if you want to quickly see any high-profile actions that have occurred recently in your subscription, eg.</span></span> <span data-ttu-id="5da67-132">새 역할 할당 또는 VM 삭제 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-132">a new role was assigned or a VM was deleted.</span></span>
   
    ![대시보드에 고정된 활동 로그](./media/monitoring-get-started/monitor-act-log-db.png)
7. <span data-ttu-id="5da67-134">**모니터** 타일로 돌아가 **메트릭** 섹션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-134">Return to the **Monitor** tile and click the **Metrics** section.</span></span> <span data-ttu-id="5da67-135">먼저 블레이드 맨 위에 있는 드롭다운 옵션을 통해 필터링하고 선택하여 리소스를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-135">You first need to select a resource by filtering and selecting using the drop down options at the top of the blade.</span></span>
   
    ![메트릭에 대한 리소스 필터링](./media/monitoring-get-started/monitor-met-filter.png)
   
    <span data-ttu-id="5da67-137">모든 Azure 리소스에서 [**메트릭**](monitoring-overview-metrics.md)을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-137">All Azure resources emit [**metrics**](monitoring-overview-metrics.md).</span></span> <span data-ttu-id="5da67-138">이 보기는 리소스에서 수행하는 방식을 쉽게 이해할 수 있도록 모든 메트릭을 단일 창에 모아 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-138">This view brings together all metrics in a single pane of glass so you can easily understand how your resources are performing.</span></span>
8. <span data-ttu-id="5da67-139">사용자가 리소스를 선택하면 모든 사용 가능한 메트릭이 블레이드의 왼쪽에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-139">Once you have selected a resource, all available metrics appear on the left side of the blade.</span></span> <span data-ttu-id="5da67-140">메트릭을 선택하고 그래프 형식 및 시간 범위를 수정하면 여러 메트릭을 한 번에 차트로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-140">You can chart multiple metrics at once by selecting metrics and modify the graph type and time range.</span></span> <span data-ttu-id="5da67-141">이 리소스에 대해 설정한 모든 메트릭 경로도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-141">You can also view all metric alerts set on this resource.</span></span>
   
    ![메트릭 블레이드](./media/monitoring-get-started/monitor-metric-blade.png)
   
   > [!NOTE]
   > <span data-ttu-id="5da67-143">일부 메트릭은 리소스에 대해 [Application Insights](../application-insights/app-insights-overview.md) 및/또는 Windows/Linux Azure 진단을 사용하도록 설정한 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-143">Some metrics are only available by enabling [Application Insights](../application-insights/app-insights-overview.md) and/or Windows or Linux Azure Diagnostics on your resource.</span></span>
   > 
   > 
9. <span data-ttu-id="5da67-144">차트가 만족스러우면 **고정** 단추를 사용하여 대시보드에 고정합니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-144">When you are happy with your chart, you can use the **Pin** button to pin it to your dashboard.</span></span>
10. <span data-ttu-id="5da67-145">**모니터** 블레이드로 돌아가 **진단 로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-145">Return to the **Monitor** blade and click **Diagnostic logs**.</span></span>
    
    ![진단 로그 블레이드](./media/monitoring-get-started/monitor-diaglogs-blade.png)
    
    <span data-ttu-id="5da67-147">[**진단 로그**](monitoring-overview-of-diagnostic-logs.md)는 특정 리소스의 작업 관련 데이터를 제공하는 *리소스에서* 내보낸 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-147">[**Diagnostic logs**](monitoring-overview-of-diagnostic-logs.md) are logs emitted *by* a resource that provide data about the operation of that particular resource.</span></span> <span data-ttu-id="5da67-148">예를 들어 네트워크 보안 그룹 규칙 카운터와 논리 앱 워크플로 로그는 모두 진단 로그의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-148">For example, Network Security Group Rule Counters and Logic App Workflow Logs are both types of diagnostic logs.</span></span> <span data-ttu-id="5da67-149">이러한 로그는 저장소 계정에 저장되고, 이벤트 허브로 스트리밍되며, [Log Analytics](../log-analytics/log-analytics-overview.md)로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-149">These logs can be stored in a storage account, streamed to an Event Hub, and/or sent to [Log Analytics](../log-analytics/log-analytics-overview.md).</span></span> <span data-ttu-id="5da67-150">Log Analytics는 고급 검색 및 경고를 위한 Microsoft의 운영 인텔리전스 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-150">Log Analytics is Microsoft's operational intelligence product for advanced searching and alerting.</span></span>
    
    <span data-ttu-id="5da67-151">포털에서는 구독의 모든 리소스 목록을 확인 및 필터링하여 활성화된 진단 로그 유무를 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-151">In the portal you can view and filter a list of all resources in your subscription to identify if they have diagnostic logs enabled.</span></span>
11. <span data-ttu-id="5da67-152">진단 로그 블레이드에서 리소스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-152">Click a resource in the diagnostic logs blade.</span></span> <span data-ttu-id="5da67-153">진단 로그가 저장소 계정에 저장된 경우 직접 다운로드할 수 있는 시간별 로그 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-153">If diagnostic logs are being stored in a storage account, you will see a list of hourly logs that you can directly download.</span></span>
    
    ![하나의 리소스에 대한 진단 로그](./media/monitoring-get-started/monitor-diaglogs-detail.png)
    
    <span data-ttu-id="5da67-155">저장소 계정에 대한 보관, Event Hubs로의 스트리밍 또는 Log Analytics 작업 영역에 보내기를 설정하거나 해당 설정을 수정할 수 있는 **진단 설정**를 클릭할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-155">You can also click **Diagnostic Settings**, which allows you to set up or modify your settings for archival to a storage account, streaming to Event Hubs, or sending to a Log Analytics workspace.</span></span>
    
    ![진단 로그 활성화](./media/monitoring-get-started/monitor-diaglogs-enable.png)
    
    <span data-ttu-id="5da67-157">Log Analytics에 대한 진단 로그를 설정한 후에는 포털의 **로그 검색** 섹션에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-157">If you have set up diagnostic logs to Log Analytics, you can then search them in the **Log search** section of the portal.</span></span>
12. <span data-ttu-id="5da67-158">모니터 블레이드의 **경고** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-158">Navigate to the **Alerts** section of the Monitor blade.</span></span>
    
    ![공용 경고 블레이드](./media/monitoring-get-started/monitor-alerts-nopp.png)
    
    <span data-ttu-id="5da67-160">여기서 Azure 리소스에 대한 모든 [**경고**](monitoring-overview-alerts.md)를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-160">Here you can manage all [**alerts**](monitoring-overview-alerts.md) on your Azure resources.</span></span> <span data-ttu-id="5da67-161">여기에는 메트릭, 활동 로그 이벤트, Application Insights 웹 테스트(위치) 및 Application Insights 사전 진단에 대한 경고가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-161">This includes alerts on metrics, activity log events, Application Insights web tests (Locations), and Application Insights proactive diagnostics.</span></span> <span data-ttu-id="5da67-162">경고는 전송될 이메일 또는 웹후크 URL에 대한 HTTP POST를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-162">Alerts can trigger an email to be sent or an HTTP POST to a webhook URL.</span></span>
13. <span data-ttu-id="5da67-163">경고를 만들려면 **메트릭 경고 추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-163">Click **Add metric alert** to create an alert.</span></span>
    
    ![메트릭 경고 추가](./media/monitoring-get-started/monitor-alerts-add.png)
    
    <span data-ttu-id="5da67-165">그런 다음 대시보드에 경고를 고정하여 언제든 간편하게 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-165">You can then pin an alert to your dashboard to easily see its state at any time.</span></span>
14. <span data-ttu-id="5da67-166">모니터 섹션에는 [Application Insights](../application-insights/app-insights-overview.md) 응용 프로그램 및 [Log Analytics](../log-analytics/log-analytics-overview.md) 관리 솔루션에 대한 링크도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-166">The Monitor section also includes links to [Application Insights](../application-insights/app-insights-overview.md) applications and [Log Analytics](../log-analytics/log-analytics-overview.md) management solutions.</span></span> <span data-ttu-id="5da67-167">이러한 다른 Microsoft 제품은 Azure Monitor와 자연스럽게 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-167">These other Microsoft products have deep integration with Azure Monitor.</span></span>
15. <span data-ttu-id="5da67-168">Application Insights나 Log Analytics를 사용하지 않을 경우 기존 모니터링, 로깅, 경고 제품과 Azure Monitor를 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-168">If you are not using Application Insights or Log Analytics, chances are that Azure Monitor has a partnership with your current monitoring, logging, and alerting products.</span></span> <span data-ttu-id="5da67-169">통합 방법에 대한 지침 및 전체 목록은 [파트너 페이지](monitoring-partners.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5da67-169">See our [partners page](monitoring-partners.md) for a full list and instructions for how to integrate.</span></span>

<span data-ttu-id="5da67-170">다음 단계를 수행하고 모든 관련 타일을 대시보드에 고정하면 다음과 같이 응용 프로그램 및 인프라에 대한 통합 보기를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5da67-170">By following these steps and pinning all relevant tiles to a dashboard, you can create comprehensive views of your application and infrastructure like this one:</span></span>

![Azure Monitor 대시보드](./media/monitoring-get-started/monitor-final-dash.png)

## <a name="next-steps"></a><span data-ttu-id="5da67-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5da67-172">Next Steps</span></span>
* <span data-ttu-id="5da67-173">[Azure Monitor 개요](monitoring-overview.md)</span><span class="sxs-lookup"><span data-stu-id="5da67-173">Read the [Overview of Azure Monitor](monitoring-overview.md)</span></span>

