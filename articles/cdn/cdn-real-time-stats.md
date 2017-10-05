---
title: "Azure CDN의 실시간 통계 | Microsoft Docs"
description: "실시간 통계는 클라이언트에 콘텐츠를 제공하는 경우 Azure CDN의 성능에 대한 실시간 데이터를 제공합니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c7989340-1172-4315-acbb-186ba34dd52a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e9b9522de6b2c54dc794b00100ffe358296ecfdd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a><span data-ttu-id="8540a-103">Microsoft Azure CDN의 실시간 통계</span><span class="sxs-lookup"><span data-stu-id="8540a-103">Real-time stats in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="8540a-104">개요</span><span class="sxs-lookup"><span data-stu-id="8540a-104">Overview</span></span>
<span data-ttu-id="8540a-105">이 문서에서는 Microsoft Azure CDN의 실시간 통계에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-105">This document explains real-time stats in Microsoft Azure CDN.</span></span>  <span data-ttu-id="8540a-106">이 기능은 클라이언트에 콘텐츠를 제공하는 경우 대역폭, 캐시 상태 및 CDN 프로필에 대한 동시 연결과 같은 실시간 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-106">This functionality provides real-time data, such as bandwidth, cache statuses, and concurrent connections to your CDN profile when delivering content to your clients.</span></span> <span data-ttu-id="8540a-107">따라서 라이브 이벤트를 포함하여 언제든지 서비스의 상태를 계속 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-107">This enables continuous monitoring of the health of your service at any time, including go-live events.</span></span>

<span data-ttu-id="8540a-108">사용할 수 있는 그래프는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-108">The following graphs are available:</span></span>

* [<span data-ttu-id="8540a-109">대역폭</span><span class="sxs-lookup"><span data-stu-id="8540a-109">Bandwidth</span></span>](#bandwidth)
* [<span data-ttu-id="8540a-110">상태 코드</span><span class="sxs-lookup"><span data-stu-id="8540a-110">Status Codes</span></span>](#status-codes)
* [<span data-ttu-id="8540a-111">캐시 상태</span><span class="sxs-lookup"><span data-stu-id="8540a-111">Cache Statuses</span></span>](#cache-statuses)
* [<span data-ttu-id="8540a-112">연결</span><span class="sxs-lookup"><span data-stu-id="8540a-112">Connections</span></span>](#connections)

## <a name="accessing-real-time-stats"></a><span data-ttu-id="8540a-113">실시간 통계에 액세스</span><span class="sxs-lookup"><span data-stu-id="8540a-113">Accessing real-time stats</span></span>
1. <span data-ttu-id="8540a-114">[Azure 포털](https://portal.azure.com)에서 CDN 프로필로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-114">In the [Azure Portal](https://portal.azure.com), browse to your CDN profile.</span></span>
   
    ![CDN 프로필 블레이드](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. <span data-ttu-id="8540a-116">CDN 프로필 블레이드에서 **관리** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-116">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![CDN 프로필 블레이드 관리 단추](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    <span data-ttu-id="8540a-118">CDN 관리 포털이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-118">The CDN management portal opens.</span></span>
3. <span data-ttu-id="8540a-119">**분석** 탭을 마우스로 가리킨 후 **실시간 통계** 플라이아웃을 마우스로 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-119">Hover over the **Analytics** tab, then hover over the **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="8540a-120">**HTTP 큰 개체**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-120">Click on **HTTP Large Object**.</span></span>
   
    ![CDN 관리 포털](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    <span data-ttu-id="8540a-122">실시간 통계 그래프가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-122">The real-time stats graphs are displayed.</span></span>

<span data-ttu-id="8540a-123">페이지가 로드될 때 시작되는 그래프 각각은 선택한 시간 범위에 대한 실시간 통계를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-123">Each of the graphs displays real-time statistics for the selected time span, starting when the page loads.</span></span>  <span data-ttu-id="8540a-124">그래프는 몇 초 마다 자동으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-124">The graphs update automatically every few seconds.</span></span>  <span data-ttu-id="8540a-125">**그래프 새로 고침** 단추가 있는 경우 그래프를 지우고 이후 선택한 데이터만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-125">The **Refresh Graph** button, if present, will clear the graph, after which it will only display the selected data.</span></span>

## <a name="bandwidth"></a><span data-ttu-id="8540a-126">대역폭</span><span class="sxs-lookup"><span data-stu-id="8540a-126">Bandwidth</span></span>
![대역폭 그래프](./media/cdn-real-time-stats/cdn-bandwidth.png)

<span data-ttu-id="8540a-128">**대역폭** 그래프는 선택한 시간 범위 동안 현재 플랫폼에 사용된 대역폭의 양을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-128">The **Bandwidth** graph displays the amount of bandwidth used for the current platform over the selected time span.</span></span> <span data-ttu-id="8540a-129">그래프의 음영 처리된 부분은 대역폭 사용량을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-129">The shaded portion of the graph indicates bandwidth usage.</span></span> <span data-ttu-id="8540a-130">현재 사용 중인 대역폭의 정확한 양이 꺾은선형 그래프 바로 아래 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-130">The exact amount of bandwidth currently being used is displayed directly below the line graph.</span></span>

## <a name="status-codes"></a><span data-ttu-id="8540a-131">상태 코드</span><span class="sxs-lookup"><span data-stu-id="8540a-131">Status Codes</span></span>
![상태 코드 그래프](./media/cdn-real-time-stats/cdn-status-codes.png)

<span data-ttu-id="8540a-133">**상태 코드** 그래프는 특정 HTTP 응답 코드가 선택한 시간 범위에 발생한 빈도를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-133">The **Status Codes** graph indicates how often certain HTTP response codes are occurring over the selected time span.</span></span>

> [!TIP]
> <span data-ttu-id="8540a-134">각 HTTP 상태 코드 옵션에 대한 설명은 [Azure CDN HTTP 상태 코드](https://msdn.microsoft.com/library/mt759238.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8540a-134">For a description of each HTTP status code option, see [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx).</span></span>
> 
> 

<span data-ttu-id="8540a-135">HTTP 상태 코드의 목록은 그래프 바로 위에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-135">A list of HTTP status codes is displayed directly above the graph.</span></span> <span data-ttu-id="8540a-136">이 목록은 꺾은선형 그래프에 포함할 수 있는 각 상태 코드와 해당 상태 코드에 대한 현재 초당 발생 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-136">This list indicates each status code that can be included in the line graph and the current number of occurrences per second for that status code.</span></span> <span data-ttu-id="8540a-137">기본적으로 선은 그래프에서 이 상태 코드 각각에 대해 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-137">By default, a line is displayed for each of these status codes in the graph.</span></span> <span data-ttu-id="8540a-138">그러나 CDN 구성에 대해 특별한 의미가 있는 상태 코드만 모니터하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-138">However, you can choose to only monitor the status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="8540a-139">이렇게 하려면 원하는 상태 코드를 확인하고 다른 모든 옵션의 선택을 취소한 다음 **그래프 새로 고침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-139">To do this, check the desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="8540a-140">특정 상태 코드에 대해 기록된 데이터를 임시로 숨길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-140">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="8540a-141">그래프 바로 아래 범례에서 숨길 상태 코드를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-141">From the legend directly below the graph, click the status code you want to hide.</span></span> <span data-ttu-id="8540a-142">상태 코드는 그래프에서 즉시 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-142">The status code will be immediately hidden from the graph.</span></span> <span data-ttu-id="8540a-143">해당 상태 코드를 다시 클릭하면 해당 옵션이 다시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-143">Clicking that status code again will cause that option to be displayed again.</span></span>

## <a name="cache-statuses"></a><span data-ttu-id="8540a-144">캐시 상태</span><span class="sxs-lookup"><span data-stu-id="8540a-144">Cache Statuses</span></span>
![캐시 상태 그래프](./media/cdn-real-time-stats/cdn-cache-status.png)

<span data-ttu-id="8540a-146">**캐시 상태** 그래프는 특정 유형의 캐시 상태가 선택한 시간 범위에 발생한 빈도를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-146">The **Cache Statuses** graph indicates how often certain types of cache statuses are occurring over the selected time span.</span></span> 

> [!TIP]
> <span data-ttu-id="8540a-147">각 캐시 상태 코드 옵션에 대한 설명은 [Azure CDN 캐시 상태 코드](https://msdn.microsoft.com/library/mt759237.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8540a-147">For a description of each cache status code option, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx).</span></span>
> 
> 

<span data-ttu-id="8540a-148">캐시 상태 코드 목록이 그래프 바로 위에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-148">A list of cache status codes is displayed directly above the graph.</span></span> <span data-ttu-id="8540a-149">이 목록은 꺾은선형 그래프에 포함할 수 있는 각 상태 코드와 해당 상태 코드에 대한 현재 초당 발생 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-149">This list indicates each status code that can be included in the line graph and the current number of occurrences per second for that status code.</span></span> <span data-ttu-id="8540a-150">기본적으로 선은 그래프에서 이 상태 코드 각각에 대해 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-150">By default, a line is displayed for each of these status codes in the graph.</span></span> <span data-ttu-id="8540a-151">그러나 CDN 구성에 대해 특별한 의미가 있는 상태 코드만 모니터하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-151">However, you can choose to only monitor the status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="8540a-152">이렇게 하려면 원하는 상태 코드를 확인하고 다른 모든 옵션의 선택을 취소한 다음 **그래프 새로 고침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-152">To do this, check the desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="8540a-153">특정 상태 코드에 대해 기록된 데이터를 임시로 숨길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-153">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="8540a-154">그래프 바로 아래 범례에서 숨길 상태 코드를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-154">From the legend directly below the graph, click the status code you want to hide.</span></span> <span data-ttu-id="8540a-155">상태 코드는 그래프에서 즉시 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-155">The status code will be immediately hidden from the graph.</span></span> <span data-ttu-id="8540a-156">해당 상태 코드를 다시 클릭하면 해당 옵션이 다시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-156">Clicking that status code again will cause that option to be displayed again.</span></span>

## <a name="connections"></a><span data-ttu-id="8540a-157">연결</span><span class="sxs-lookup"><span data-stu-id="8540a-157">Connections</span></span>
![연결 그래프](./media/cdn-real-time-stats/cdn-connections.png)

<span data-ttu-id="8540a-159">이 그래프는 에지 서버에 설정된 연결 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-159">This graph indicates how many connections have been established to your edge servers.</span></span> <span data-ttu-id="8540a-160">CDN을 통과하는 자산에 대한 각 요청은 연결을 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="8540a-160">Each request for an asset that passes through our CDN results in a connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8540a-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8540a-161">Next Steps</span></span>
* <span data-ttu-id="8540a-162">[Azure CDN에서 실시간 경고](cdn-real-time-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="8540a-162">Get notified with [Real-time alerts in Azure CDN](cdn-real-time-alerts.md)</span></span>
* <span data-ttu-id="8540a-163">[고급 HTTP 보고서](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="8540a-163">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="8540a-164">[사용 패턴](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="8540a-164">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

