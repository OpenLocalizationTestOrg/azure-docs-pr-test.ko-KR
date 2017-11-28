---
title: "Microsoft Azure에서 메트릭 aaaOverview | Microsoft Docs"
description: "Azure에서 차트 toocustomize 모니터링 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 4196b2e9bda713e9a0abc349eed78685abcaf194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a><span data-ttu-id="95f21-103">Microsoft Azure의 메트릭 개요</span><span class="sxs-lookup"><span data-stu-id="95f21-103">Overview of Metrics in Microsoft Azure</span></span>
<span data-ttu-id="95f21-104">모든 Azure 서비스 toomonitor hello 상태, 성능, 가용성 및 서비스의 사용을 허용 하는 주요 메트릭을 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-104">All Azure services track key metrics that allow you toomonitor hello health, performance, availability and usage of your services.</span></span> <span data-ttu-id="95f21-105">Hello Azure 포털에서에서 이러한 메트릭을 볼 수 있으며 hello를 사용할 수도 있습니다 [REST API](https://msdn.microsoft.com/library/azure/dn931930.aspx) 또는 [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess hello 전체 메트릭 집합을 프로그래밍 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-105">You can view these metrics in hello Azure portal, and you can also use hello [REST API](https://msdn.microsoft.com/library/azure/dn931930.aspx) or [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess hello full set of metrics programmatically.</span></span>

<span data-ttu-id="95f21-106">일부 서비스에 대 한 모든 메트릭을 순서 toosee에서 진단에 tooturn을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-106">For some services, you may need tooturn on diagnostics in order toosee any metrics.</span></span> <span data-ttu-id="95f21-107">가상 컴퓨터와 같은 다른 사용자에 대 한 메트릭, 기본 집합이 받아볼 수 있지만 필요한 tooenable hello 일부만 고주파 메트릭.</span><span class="sxs-lookup"><span data-stu-id="95f21-107">For others, such as virtual machines, you will get a basic set of metrics, but need tooenable hello full set high-frequency metrics.</span></span> <span data-ttu-id="95f21-108">참조 [모니터링을 활성화 및 진단](insights-how-to-use-diagnostics.md) toolearn 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-108">See [Enable monitoring and diagnostics](insights-how-to-use-diagnostics.md) toolearn more.</span></span>

## <a name="using-monitoring-charts"></a><span data-ttu-id="95f21-109">모니터링 차트 사용</span><span class="sxs-lookup"><span data-stu-id="95f21-109">Using monitoring charts</span></span>
<span data-ttu-id="95f21-110">Hello 메트릭 중 하나를 차트 선택한 기간을 통해 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-110">You can chart any of hello metrics them over any time period you choose.</span></span>

1. <span data-ttu-id="95f21-111">Hello에 [Azure 포털](https://portal.azure.com/), 클릭 **찾아보기**, 다음 리소스에 관심이 모니터링 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-111">In hello [Azure Portal](https://portal.azure.com/), click **Browse**, and then a resource you're interested in monitoring.</span></span>
2. <span data-ttu-id="95f21-112">hello **모니터링** 섹션에는 각 Azure 리소스에 대 한 가장 중요 한 메트릭을 hello 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-112">hello **Monitoring** section contains hello most important metrics for each Azure resource.</span></span> <span data-ttu-id="95f21-113">예를 들어 웹앱에는 **요청 및 오류**가 있고, 가상 컴퓨터에는 **CPU 비율** 및 **디스크 읽기 및 쓰기**: ![모니터링 렌즈](./media/insights-how-to-customize-monitoring/Insights_MonitoringChart.png)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-113">For example, a web app has **Requests and Errors**, where as a virtual machine would have **CPU percentage** and **Disk read and write**: ![Monitoring lens](./media/insights-how-to-customize-monitoring/Insights_MonitoringChart.png)</span></span>
3. <span data-ttu-id="95f21-114">모든 차트에서 클릭 하면 hello 하면 표시 됩니다 **메트릭을** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-114">Clicking on any chart will show you hello **Metric** blade.</span></span> <span data-ttu-id="95f21-115">Hello 블레이드 뿐만 아니라 toohello 그래프는 hello 메트릭 (예: 평균, 최소 및 최대 선택한 hello 시간 범위 동안) 집계를 표시 하는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-115">On hello blade, in addition toohello graph, is a table that shows you aggregations of hello metrics (such as average, minimum and maximum, over hello time range you chose).</span></span> <span data-ttu-id="95f21-116">다음 hello hello 리소스에 대 한 경고 규칙은입니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-116">Below that are hello alert rules for hello resource.</span></span>
    <span data-ttu-id="95f21-117">![메트릭 블레이드](./media/insights-how-to-customize-monitoring/Insights_MetricBlade.png)</span><span class="sxs-lookup"><span data-stu-id="95f21-117">![Metric blade](./media/insights-how-to-customize-monitoring/Insights_MetricBlade.png)</span></span>
4. <span data-ttu-id="95f21-118">표시 되는 toocustomize hello 선을 클릭 hello **편집** hello 차트 단추 또는 환영 **차트 편집** hello 메트릭 블레이드 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-118">toocustomize hello lines that appear, click hello **Edit** button on hello chart, or, hello **Edit chart** command on hello Metric blade.</span></span>
5. <span data-ttu-id="95f21-119">Hello 쿼리 편집 블레이드에서 다음 세 가지 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-119">On hello Edit Query blade you can do three things:</span></span>
   
   * <span data-ttu-id="95f21-120">Hello 시간 범위를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-120">Change hello time range</span></span>
   * <span data-ttu-id="95f21-121">Hello 모양 사이 전환 막대 및 선</span><span class="sxs-lookup"><span data-stu-id="95f21-121">Switch hello appearance between Bar and Line</span></span>
   * <span data-ttu-id="95f21-122">다른 메트릭 ![쿼리 편집](./media/insights-how-to-customize-monitoring/Insights_EditQuery.png) 선택</span><span class="sxs-lookup"><span data-stu-id="95f21-122">Choose different metics ![Edit Query](./media/insights-how-to-customize-monitoring/Insights_EditQuery.png)</span></span>
6. <span data-ttu-id="95f21-123">Hello 시간 범위를 변경 하는 것은 다른 범위를 선택 하는 것 처럼 쉽게 (같은 **지난 시간**)를 클릭 하 고 **저장** hello hello 블레이드 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-123">Changing hello time range is as easy as selecting a different range (such as **Past Hour**) and clicking **Save** at hello bottom of hello blade.</span></span> <span data-ttu-id="95f21-124">선택할 수도 있습니다 **사용자 지정**, 있습니다 toochoose 얼마 hello를 통해 지난 2 주 동안 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-124">You can also choose **Custom**, which allows you toochoose any period of time over hello past 2 weeks.</span></span> <span data-ttu-id="95f21-125">예를 들어 hello 전체 2 주, 또는 어제부터 1 시간에만 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-125">For example, you can see hello whole two weeks, or, just 1 hour from yesterday.</span></span> <span data-ttu-id="95f21-126">다른 hello 텍스트 상자 tooenter 입력 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-126">Type in hello text box tooenter a different hour.</span></span>
    <span data-ttu-id="95f21-127">![사용자 지정 시간 범위](./media/insights-how-to-customize-monitoring/Insights_CustomTime.png)</span><span class="sxs-lookup"><span data-stu-id="95f21-127">![Custom time range](./media/insights-how-to-customize-monitoring/Insights_CustomTime.png)</span></span>
7. <span data-ttu-id="95f21-128">Hello 시간 범위를 아래 채널 있습니다 hello 차트에서 메트릭 tooshow 개수에 관계 없이 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-128">Below hello time range, you chan choose any number of metrics tooshow on hello chart.</span></span>
8. <span data-ttu-id="95f21-129">저장을 클릭하면 해당 리소스에 대해 변경 내용이 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-129">When you click Save your changes will be saved for that particular resource.</span></span> <span data-ttu-id="95f21-130">예를 들어 두 개의 가상 컴퓨터가 있고 하나에 차트를 변경 하는 경우 영향을 주지 않을 hello 다른 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-130">For example, if you have two virtual machines, and you change a chart on one, it will not impact hello other.</span></span>

## <a name="creating-side-by-side-charts"></a><span data-ttu-id="95f21-131">병렬 차트 만들기</span><span class="sxs-lookup"><span data-stu-id="95f21-131">Creating side-by-side charts</span></span>
<span data-ttu-id="95f21-132">Hello 포털에서 강력한 사용자 지정 hello와 원하는 만큼 많은 차트를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-132">With hello powerful customization in hello portal you can add as many charts as you want.</span></span>

1. <span data-ttu-id="95f21-133">Hello에 **...**  hello 블레이드 클릭의 hello 위쪽 메뉴 **타일 추가**:</span><span class="sxs-lookup"><span data-stu-id="95f21-133">In hello **...** menu at hello top of hello blade click **Add tiles**:</span></span>  
    <span data-ttu-id="95f21-134">![메뉴 추가](./media/insights-how-to-customize-monitoring/Insights_AddMenu.png)</span><span class="sxs-lookup"><span data-stu-id="95f21-134">![Add Menu](./media/insights-how-to-customize-monitoring/Insights_AddMenu.png)</span></span>
2. <span data-ttu-id="95f21-135">그런 다음, 선택에서에서 선택할 수 차트 hello **갤러리** hello 화면 오른쪽에: ![갤러리](./media/insights-how-to-customize-monitoring/Insights_Gallery.png)</span><span class="sxs-lookup"><span data-stu-id="95f21-135">Then, you can select select a chart from hello **Gallery** on hello right side of your screen:  ![Gallery](./media/insights-how-to-customize-monitoring/Insights_Gallery.png)</span></span>
3. <span data-ttu-id="95f21-136">Hello 메트릭을 보이지 않으면 언제 추가할 수 있습니다 중 hello 메트릭, 기본 설정 및 **편집** 해야 하는 차트 tooshow hello 메트릭을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-136">If you don't see hello metric you want, you can always add one of hello preset metrics, and **Edit** hello chart tooshow hello metric that you need.</span></span>

## <a name="monitoring-usage-quotas"></a><span data-ttu-id="95f21-137">사용 할당량 모니터링</span><span class="sxs-lookup"><span data-stu-id="95f21-137">Monitoring usage quotas</span></span>
<span data-ttu-id="95f21-138">대부분의 메트릭은 시간에 따른 추세를 보여 주지만 사용 할당량와 같은 특정 데이터는 임계값을 포함하는 지정 시간 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-138">Most metrics show you trends over time, but certain data, like usage quotas, are point-in-time information with a threshold.</span></span>

<span data-ttu-id="95f21-139">또한 hello 블레이드의 리소스 할당량에 대 한 사용 할당량을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-139">You can also see usage quotas on hello blade for resources that have quotas:</span></span>

![사용](./media/insights-how-to-customize-monitoring/Insights_UsageChart.png)

<span data-ttu-id="95f21-141">메트릭을 사용 하 여 hello을 사용할 수와 [REST API](https://msdn.microsoft.com/library/azure/dn931963.aspx) 또는 [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess 사용 할당량의 전체 집합을 프로그래밍 방식으로 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-141">Like with metrics, you can use hello [REST API](https://msdn.microsoft.com/library/azure/dn931963.aspx) or [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess hello full set of usage quotas programmatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95f21-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="95f21-142">Next steps</span></span>
* <span data-ttu-id="95f21-143">[경고 알림을 수신](insights-receive-alert-notifications.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-143">[Receive alert notifications](insights-receive-alert-notifications.md) whenever a metric crosses a threshold.</span></span>
* <span data-ttu-id="95f21-144">[모니터링을 활성화 및 진단](insights-how-to-use-diagnostics.md) toocollect 고주파 메트릭 서비스에서 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-144">[Enable monitoring and diagnostics](insights-how-to-use-diagnostics.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="95f21-145">[인스턴스 수를 자동으로 크기 조정](insights-how-to-scale.md) toomake 서비스를 사용 가능 하 고 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-145">[Scale instance count automatically](insights-how-to-scale.md) toomake sure your service is available and responsive.</span></span>
* <span data-ttu-id="95f21-146">[응용 프로그램 성능 모니터링](../application-insights/app-insights-azure-web-apps.md) toounderstand 하려면 정확 하 게 코드 작업 수행 방식을 hello 클라우드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-146">[Monitor application performance](../application-insights/app-insights-azure-web-apps.md) if you want toounderstand exactly how your code is performing in hello cloud.</span></span>
* <span data-ttu-id="95f21-147">사용 하 여 [JavaScript 앱과 웹 페이지에 대 한 Application Insights](../application-insights/app-insights-web-track-usage.md) 웹 페이지를 방문 하는 hello 브라우저에 대 한 tooget 클라이언트 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-147">Use [Application Insights for JavaScript apps and web pages](../application-insights/app-insights-web-track-usage.md) tooget client analytics about hello browsers that visit a web page.</span></span>
* <span data-ttu-id="95f21-148">[웹 페이지의 가용성 및 응답성을 모니터링](../application-insights/app-insights-monitor-web-app-availability.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f21-148">[Monitor availability and responsiveness of any web page](../application-insights/app-insights-monitor-web-app-availability.md) with Application Insights so you can find out if your page is down.</span></span>

