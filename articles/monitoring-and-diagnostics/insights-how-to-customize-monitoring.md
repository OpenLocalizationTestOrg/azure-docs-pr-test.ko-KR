---
title: "Microsoft Azure의 메트릭 개요 | Microsoft 문서"
description: "Azure에서 모니터링 차트를 사용자 지정하는 방법에 대해 알아봅니다."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c36031eb-4df5-4cd5-9479-311d493a40d2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: robb
ms.openlocfilehash: 3f9ebb0f5737714dd685f0dcc1ff4b1c0c89528f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a><span data-ttu-id="8f7a4-103">Microsoft Azure의 메트릭 개요</span><span class="sxs-lookup"><span data-stu-id="8f7a4-103">Overview of Metrics in Microsoft Azure</span></span>
<span data-ttu-id="8f7a4-104">모든 Azure 서비스는 서비스의 상태, 성능, 가용성 및 사용량을 모니터링할 수 있게 해주는 주요 메트릭을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-104">All Azure services track key metrics that allow you to monitor the health, performance, availability and usage of your services.</span></span> <span data-ttu-id="8f7a4-105">Azure 포털에서 이러한 메트릭을 볼 수 있으며, [REST API](https://msdn.microsoft.com/library/azure/dn931930.aspx) 또는 [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor)를 사용하여 프로그래밍 방식으로 전체 메트릭 집합에 액세스할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-105">You can view these metrics in the Azure portal, and you can also use the [REST API](https://msdn.microsoft.com/library/azure/dn931930.aspx) or [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) to access the full set of metrics programmatically.</span></span>

<span data-ttu-id="8f7a4-106">일부 서비스의 경우 메트릭을 확인하기 위해 진단을 켜야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-106">For some services, you may need to turn on diagnostics in order to see any metrics.</span></span> <span data-ttu-id="8f7a4-107">가상 컴퓨터와 같은 기타 서비스의 경우 기본 메트릭 집합이 표시되지만 전체 집합 고빈도 메트릭을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-107">For others, such as virtual machines, you will get a basic set of metrics, but need to enable the full set high-frequency metrics.</span></span> <span data-ttu-id="8f7a4-108">자세히 알아보려면 [모니터링 및 진단 사용](insights-how-to-use-diagnostics.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-108">See [Enable monitoring and diagnostics](insights-how-to-use-diagnostics.md) to learn more.</span></span>

## <a name="using-monitoring-charts"></a><span data-ttu-id="8f7a4-109">모니터링 차트 사용</span><span class="sxs-lookup"><span data-stu-id="8f7a4-109">Using monitoring charts</span></span>
<span data-ttu-id="8f7a4-110">선택한 기간에 대한 메트릭을 차트로 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-110">You can chart any of the metrics them over any time period you choose.</span></span>

1. <span data-ttu-id="8f7a4-111">[Azure 포털](https://portal.azure.com/)에서 **찾아보기**를 클릭한 후 모니터링할 리소스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-111">In the [Azure Portal](https://portal.azure.com/), click **Browse**, and then a resource you're interested in monitoring.</span></span>
2. <span data-ttu-id="8f7a4-112">**모니터링** 섹션에는 각 Azure 리소스에 대한 가장 중요한 메트릭이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-112">The **Monitoring** section contains the most important metrics for each Azure resource.</span></span> <span data-ttu-id="8f7a4-113">예를 들어 웹앱에는 **요청 및 오류**가 있고, 가상 컴퓨터에는 **CPU 비율** 및 **디스크 읽기 및 쓰기**: ![모니터링 렌즈](./media/insights-how-to-customize-monitoring/Insights_MonitoringChart.png)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-113">For example, a web app has **Requests and Errors**, where as a virtual machine would have **CPU percentage** and **Disk read and write**: ![Monitoring lens](./media/insights-how-to-customize-monitoring/Insights_MonitoringChart.png)</span></span>
3. <span data-ttu-id="8f7a4-114">차트를 클릭하면 **메트릭** 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-114">Clicking on any chart will show you the **Metric** blade.</span></span> <span data-ttu-id="8f7a4-115">블레이드에는 그래프 외에도 선택한 시간 범위의 메트릭 집계(예: 평균, 최소값 및 최대값)를 보여 주는 테이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-115">On the blade, in addition to the graph, is a table that shows you aggregations of the metrics (such as average, minimum and maximum, over the time range you chose).</span></span> <span data-ttu-id="8f7a4-116">그 아래에는 리소스에 대한 경고 규칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-116">Below that are the alert rules for the resource.</span></span>
    <span data-ttu-id="8f7a4-117">![메트릭 블레이드](./media/insights-how-to-customize-monitoring/Insights_MetricBlade.png)</span><span class="sxs-lookup"><span data-stu-id="8f7a4-117">![Metric blade](./media/insights-how-to-customize-monitoring/Insights_MetricBlade.png)</span></span>
4. <span data-ttu-id="8f7a4-118">표시되는 선을 사용자 지정하려면 차트의 **편집** 단추 또는 메트릭 블레이드의 **차트 편집** 명령을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-118">To customize the lines that appear, click the **Edit** button on the chart, or, the **Edit chart** command on the Metric blade.</span></span>
5. <span data-ttu-id="8f7a4-119">쿼리 편집 블레이드에서 다음 세 가지 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-119">On the Edit Query blade you can do three things:</span></span>
   
   * <span data-ttu-id="8f7a4-120">시간 범위 변경</span><span class="sxs-lookup"><span data-stu-id="8f7a4-120">Change the time range</span></span>
   * <span data-ttu-id="8f7a4-121">막대와 선 간에 모양 전환</span><span class="sxs-lookup"><span data-stu-id="8f7a4-121">Switch the appearance between Bar and Line</span></span>
   * <span data-ttu-id="8f7a4-122">다른 메트릭 ![쿼리 편집](./media/insights-how-to-customize-monitoring/Insights_EditQuery.png) 선택</span><span class="sxs-lookup"><span data-stu-id="8f7a4-122">Choose different metics ![Edit Query](./media/insights-how-to-customize-monitoring/Insights_EditQuery.png)</span></span>
6. <span data-ttu-id="8f7a4-123">시간 범위를 변경하는 것은 다른 범위(예: **지난 시간**)를 선택하고 블레이드 맨 아래에 있는 **저장**을 클릭하는 것만큼 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-123">Changing the time range is as easy as selecting a different range (such as **Past Hour**) and clicking **Save** at the bottom of the blade.</span></span> <span data-ttu-id="8f7a4-124">**사용자 지정**을 통해 지난 2주간에 걸친 기간을 임의로 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-124">You can also choose **Custom**, which allows you to choose any period of time over the past 2 weeks.</span></span> <span data-ttu-id="8f7a4-125">예를 들어 2주 전체를 확인하거나 어제부터 1시간만 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-125">For example, you can see the whole two weeks, or, just 1 hour from yesterday.</span></span> <span data-ttu-id="8f7a4-126">다른 시간을 입력하려면 텍스트 상자에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-126">Type in the text box to enter a different hour.</span></span>
    <span data-ttu-id="8f7a4-127">![사용자 지정 시간 범위](./media/insights-how-to-customize-monitoring/Insights_CustomTime.png)</span><span class="sxs-lookup"><span data-stu-id="8f7a4-127">![Custom time range](./media/insights-how-to-customize-monitoring/Insights_CustomTime.png)</span></span>
7. <span data-ttu-id="8f7a4-128">시간 범위 아래에서 차트에 표시할 메트릭 수를 제한 없이 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-128">Below the time range, you chan choose any number of metrics to show on the chart.</span></span>
8. <span data-ttu-id="8f7a4-129">저장을 클릭하면 해당 리소스에 대해 변경 내용이 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-129">When you click Save your changes will be saved for that particular resource.</span></span> <span data-ttu-id="8f7a4-130">예를 들어 두 개의 가상 컴퓨터가 있고 한 가상 컴퓨터에서 차트를 변경하는 경우 다른 가상 컴퓨터에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-130">For example, if you have two virtual machines, and you change a chart on one, it will not impact the other.</span></span>

## <a name="creating-side-by-side-charts"></a><span data-ttu-id="8f7a4-131">병렬 차트 만들기</span><span class="sxs-lookup"><span data-stu-id="8f7a4-131">Creating side-by-side charts</span></span>
<span data-ttu-id="8f7a4-132">포털의 강력한 사용자 지정 기능을 통해 차트를 원하는 개수만큼 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-132">With the powerful customization in the portal you can add as many charts as you want.</span></span>

1. <span data-ttu-id="8f7a4-133">블레이드 맨 위에 있는 **...** 메뉴에서 **타일 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-133">In the **...** menu at the top of the blade click **Add tiles**:</span></span>  
    <span data-ttu-id="8f7a4-134">![메뉴 추가](./media/insights-how-to-customize-monitoring/Insights_AddMenu.png)</span><span class="sxs-lookup"><span data-stu-id="8f7a4-134">![Add Menu](./media/insights-how-to-customize-monitoring/Insights_AddMenu.png)</span></span>
2. <span data-ttu-id="8f7a4-135">그런 다음 ![갤러리](./media/insights-how-to-customize-monitoring/Insights_Gallery.png) 화면 오른쪽에 있는 **갤러리**에서 차트를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-135">Then, you can select select a chart from the **Gallery** on the right side of your screen:  ![Gallery](./media/insights-how-to-customize-monitoring/Insights_Gallery.png)</span></span>
3. <span data-ttu-id="8f7a4-136">원하는 메트릭이 표시되지 않는 경우 언제든지 미리 설정된 메트릭 중 하나를 추가하고 차트를 **편집** 하여 필요한 메트릭을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-136">If you don't see the metric you want, you can always add one of the preset metrics, and **Edit** the chart to show the metric that you need.</span></span>

## <a name="monitoring-usage-quotas"></a><span data-ttu-id="8f7a4-137">사용 할당량 모니터링</span><span class="sxs-lookup"><span data-stu-id="8f7a4-137">Monitoring usage quotas</span></span>
<span data-ttu-id="8f7a4-138">대부분의 메트릭은 시간에 따른 추세를 보여 주지만 사용 할당량와 같은 특정 데이터는 임계값을 포함하는 지정 시간 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-138">Most metrics show you trends over time, but certain data, like usage quotas, are point-in-time information with a threshold.</span></span>

<span data-ttu-id="8f7a4-139">할당량이 있는 리소스에 대한 블레이드에서 사용 할당량을 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-139">You can also see usage quotas on the blade for resources that have quotas:</span></span>

![사용 현황](./media/insights-how-to-customize-monitoring/Insights_UsageChart.png)

<span data-ttu-id="8f7a4-141">메트릭과 마찬가지로, [REST API](https://msdn.microsoft.com/library/azure/dn931963.aspx) 또는 [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor)를 사용하여 프로그래밍 방식으로 사용 할당량의 전체 집합에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-141">Like with metrics, you can use the [REST API](https://msdn.microsoft.com/library/azure/dn931963.aspx) or [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) to access the full set of usage quotas programmatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f7a4-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8f7a4-142">Next steps</span></span>
* <span data-ttu-id="8f7a4-143">[경고 알림을 수신](insights-receive-alert-notifications.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-143">[Receive alert notifications](insights-receive-alert-notifications.md) whenever a metric crosses a threshold.</span></span>
* <span data-ttu-id="8f7a4-144">[모니터링 및 진단을 사용](insights-how-to-use-diagnostics.md) 하여 서비스의 자세한 고빈도 메트릭을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-144">[Enable monitoring and diagnostics](insights-how-to-use-diagnostics.md) to collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="8f7a4-145">[인스턴스 개수를 자동으로 조정](insights-how-to-scale.md) 하여 서비스를 사용 가능하며 응답할 수 있는 상태로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-145">[Scale instance count automatically](insights-how-to-scale.md) to make sure your service is available and responsive.</span></span>
* <span data-ttu-id="8f7a4-146">[응용 프로그램 성능을 모니터링](../application-insights/app-insights-azure-web-apps.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-146">[Monitor application performance](../application-insights/app-insights-azure-web-apps.md) if you want to understand exactly how your code is performing in the cloud.</span></span>
* <span data-ttu-id="8f7a4-147">[JavaScript 앱 및 웹 페이지용 Application Insights](../application-insights/app-insights-web-track-usage.md) 를 사용하여 웹 페이지를 방문하는 브라우저에 대한 클라이언트 분석을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-147">Use [Application Insights for JavaScript apps and web pages](../application-insights/app-insights-web-track-usage.md) to get client analytics about the browsers that visit a web page.</span></span>
* <span data-ttu-id="8f7a4-148">[웹 페이지의 가용성 및 응답성을 모니터링](../application-insights/app-insights-monitor-web-app-availability.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f7a4-148">[Monitor availability and responsiveness of any web page](../application-insights/app-insights-monitor-web-app-availability.md) with Application Insights so you can find out if your page is down.</span></span>

