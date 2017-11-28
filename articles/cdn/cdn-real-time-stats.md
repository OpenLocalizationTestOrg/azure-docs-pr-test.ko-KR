---
title: "Azure CDN에서 aaaReal 시간 통계 | Microsoft Docs"
description: "실시간 통계 콘텐츠 tooyour 클라이언트 배달할 때 Azure CDN의 hello 성능에 대 한 실시간 데이터를 제공 합니다."
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
ms.openlocfilehash: 68900a5092b767e45c1fdf9cef2cd03f55f38a6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a><span data-ttu-id="6c66b-103">Microsoft Azure CDN의 실시간 통계</span><span class="sxs-lookup"><span data-stu-id="6c66b-103">Real-time stats in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="6c66b-104">개요</span><span class="sxs-lookup"><span data-stu-id="6c66b-104">Overview</span></span>
<span data-ttu-id="6c66b-105">이 문서에서는 Microsoft Azure CDN의 실시간 통계에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-105">This document explains real-time stats in Microsoft Azure CDN.</span></span>  <span data-ttu-id="6c66b-106">이 기능은 대역폭, 캐시 상태 및 동시 연결 tooyour CDN 프로필 콘텐츠 tooyour 클라이언트 배달할 때 같은 실시간 데이터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-106">This functionality provides real-time data, such as bandwidth, cache statuses, and concurrent connections tooyour CDN profile when delivering content tooyour clients.</span></span> <span data-ttu-id="6c66b-107">이렇게 하면 언제 든 지 go 라이브 이벤트를 포함 하 여 서비스의 hello 상태에 대 한 지속적인 모니터링입니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-107">This enables continuous monitoring of hello health of your service at any time, including go-live events.</span></span>

<span data-ttu-id="6c66b-108">다음 그래프 hello 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-108">hello following graphs are available:</span></span>

* [<span data-ttu-id="6c66b-109">대역폭</span><span class="sxs-lookup"><span data-stu-id="6c66b-109">Bandwidth</span></span>](#bandwidth)
* [<span data-ttu-id="6c66b-110">상태 코드</span><span class="sxs-lookup"><span data-stu-id="6c66b-110">Status Codes</span></span>](#status-codes)
* [<span data-ttu-id="6c66b-111">캐시 상태</span><span class="sxs-lookup"><span data-stu-id="6c66b-111">Cache Statuses</span></span>](#cache-statuses)
* [<span data-ttu-id="6c66b-112">연결</span><span class="sxs-lookup"><span data-stu-id="6c66b-112">Connections</span></span>](#connections)

## <a name="accessing-real-time-stats"></a><span data-ttu-id="6c66b-113">실시간 통계에 액세스</span><span class="sxs-lookup"><span data-stu-id="6c66b-113">Accessing real-time stats</span></span>
1. <span data-ttu-id="6c66b-114">Hello에 [Azure 포털](https://portal.azure.com), tooyour CDN 프로필을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-114">In hello [Azure Portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>
   
    ![CDN 프로필 블레이드](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. <span data-ttu-id="6c66b-116">Hello CDN 프로필 블레이드에서 hello 클릭 **관리** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-116">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![CDN 프로필 블레이드 관리 단추](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    <span data-ttu-id="6c66b-118">hello CDN 관리 포털이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-118">hello CDN management portal opens.</span></span>
3. <span data-ttu-id="6c66b-119">마우스 포인터를 놓고 hello **분석** 누른 마우스 포인터를 놓고 hello **실시간 통계** 플라이 아웃입니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-119">Hover over hello **Analytics** tab, then hover over hello **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="6c66b-120">**HTTP 큰 개체**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-120">Click on **HTTP Large Object**.</span></span>
   
    ![CDN 관리 포털](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    <span data-ttu-id="6c66b-122">hello 실시간 통계 그래프가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-122">hello real-time stats graphs are displayed.</span></span>

<span data-ttu-id="6c66b-123">Hello 그래프의 각 hello 페이지가 로드 될 때 시작 시간 범위를 선택 하는 hello에 대 한 실시간 통계를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-123">Each of hello graphs displays real-time statistics for hello selected time span, starting when hello page loads.</span></span>  <span data-ttu-id="6c66b-124">hello 그래프는 몇 초 마다 자동으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-124">hello graphs update automatically every few seconds.</span></span>  <span data-ttu-id="6c66b-125">hello **새로 고침 그래프** 단추, 있는 경우 지워집니다 hello 그래프는 하나만 표시 됩니다 hello 선택한 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-125">hello **Refresh Graph** button, if present, will clear hello graph, after which it will only display hello selected data.</span></span>

## <a name="bandwidth"></a><span data-ttu-id="6c66b-126">대역폭</span><span class="sxs-lookup"><span data-stu-id="6c66b-126">Bandwidth</span></span>
![대역폭 그래프](./media/cdn-real-time-stats/cdn-bandwidth.png)

<span data-ttu-id="6c66b-128">hello **대역폭** hello hello 선택한 시간 범위를 통한 hello 현재 플랫폼에 사용 되는 대역폭 양을 그래프에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-128">hello **Bandwidth** graph displays hello amount of bandwidth used for hello current platform over hello selected time span.</span></span> <span data-ttu-id="6c66b-129">hello 그래프의 음영 처리 된 부분 hello 대역폭 사용량을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-129">hello shaded portion of hello graph indicates bandwidth usage.</span></span> <span data-ttu-id="6c66b-130">현재 사용 중인 대역폭의 hello 정확한 양은 hello 선 그래프 바로 아래에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-130">hello exact amount of bandwidth currently being used is displayed directly below hello line graph.</span></span>

## <a name="status-codes"></a><span data-ttu-id="6c66b-131">상태 코드</span><span class="sxs-lookup"><span data-stu-id="6c66b-131">Status Codes</span></span>
![상태 코드 그래프](./media/cdn-real-time-stats/cdn-status-codes.png)

<span data-ttu-id="6c66b-133">hello **상태 코드** 그래프 hello 선택한 시간 범위를 통해 특정 HTTP 응답 코드 발생 빈도 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-133">hello **Status Codes** graph indicates how often certain HTTP response codes are occurring over hello selected time span.</span></span>

> [!TIP]
> <span data-ttu-id="6c66b-134">각 HTTP 상태 코드 옵션에 대한 설명은 [Azure CDN HTTP 상태 코드](https://msdn.microsoft.com/library/mt759238.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c66b-134">For a description of each HTTP status code option, see [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx).</span></span>
> 
> 

<span data-ttu-id="6c66b-135">HTTP 상태 코드의 목록은 hello 그래프 바로 위에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-135">A list of HTTP status codes is displayed directly above hello graph.</span></span> <span data-ttu-id="6c66b-136">이 목록은 hello 선 그래프 및 hello 현재 해당 상태 코드에 대 한 초당 발생 수에 포함 될 수 있는 각 상태 코드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-136">This list indicates each status code that can be included in hello line graph and hello current number of occurrences per second for that status code.</span></span> <span data-ttu-id="6c66b-137">기본적으로 줄은 각각 hello 그래프에서이 상태 코드에 대해 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-137">By default, a line is displayed for each of these status codes in hello graph.</span></span> <span data-ttu-id="6c66b-138">그러나 CDN 구성에 대 한 특별 한 의미가 모니터 hello 상태 코드 tooonly를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-138">However, you can choose tooonly monitor hello status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="6c66b-139">toodo이 확인 hello 원하는 상태 코드 및 다른 모든 옵션의 선택을 취소 한 다음 클릭 **새로 고침 그래프**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-139">toodo this, check hello desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="6c66b-140">특정 상태 코드에 대해 기록된 데이터를 임시로 숨길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-140">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="6c66b-141">Hello hello 그래프 바로 아래 범례에서 원하는 toohide hello 상태 코드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-141">From hello legend directly below hello graph, click hello status code you want toohide.</span></span> <span data-ttu-id="6c66b-142">hello 상태 코드는 hello 그래프에서 즉시 표시 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-142">hello status code will be immediately hidden from hello graph.</span></span> <span data-ttu-id="6c66b-143">해당 상태 코드를 다시 클릭 하면 해당 옵션 toobe 다시 표시 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-143">Clicking that status code again will cause that option toobe displayed again.</span></span>

## <a name="cache-statuses"></a><span data-ttu-id="6c66b-144">캐시 상태</span><span class="sxs-lookup"><span data-stu-id="6c66b-144">Cache Statuses</span></span>
![캐시 상태 그래프](./media/cdn-real-time-stats/cdn-cache-status.png)

<span data-ttu-id="6c66b-146">hello **캐시 상태** 그래프 hello 선택한 시간 범위를 통해 특정 유형의 캐시 상태 발생 빈도 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-146">hello **Cache Statuses** graph indicates how often certain types of cache statuses are occurring over hello selected time span.</span></span> 

> [!TIP]
> <span data-ttu-id="6c66b-147">각 캐시 상태 코드 옵션에 대한 설명은 [Azure CDN 캐시 상태 코드](https://msdn.microsoft.com/library/mt759237.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c66b-147">For a description of each cache status code option, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx).</span></span>
> 
> 

<span data-ttu-id="6c66b-148">캐시 상태 코드의 목록은 hello 그래프 바로 위에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-148">A list of cache status codes is displayed directly above hello graph.</span></span> <span data-ttu-id="6c66b-149">이 목록은 hello 선 그래프 및 hello 현재 해당 상태 코드에 대 한 초당 발생 수에 포함 될 수 있는 각 상태 코드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-149">This list indicates each status code that can be included in hello line graph and hello current number of occurrences per second for that status code.</span></span> <span data-ttu-id="6c66b-150">기본적으로 줄은 각각 hello 그래프에서이 상태 코드에 대해 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-150">By default, a line is displayed for each of these status codes in hello graph.</span></span> <span data-ttu-id="6c66b-151">그러나 CDN 구성에 대 한 특별 한 의미가 모니터 hello 상태 코드 tooonly를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-151">However, you can choose tooonly monitor hello status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="6c66b-152">toodo이 확인 hello 원하는 상태 코드 및 다른 모든 옵션의 선택을 취소 한 다음 클릭 **새로 고침 그래프**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-152">toodo this, check hello desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="6c66b-153">특정 상태 코드에 대해 기록된 데이터를 임시로 숨길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-153">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="6c66b-154">Hello hello 그래프 바로 아래 범례에서 원하는 toohide hello 상태 코드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-154">From hello legend directly below hello graph, click hello status code you want toohide.</span></span> <span data-ttu-id="6c66b-155">hello 상태 코드는 hello 그래프에서 즉시 표시 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-155">hello status code will be immediately hidden from hello graph.</span></span> <span data-ttu-id="6c66b-156">해당 상태 코드를 다시 클릭 하면 해당 옵션 toobe 다시 표시 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-156">Clicking that status code again will cause that option toobe displayed again.</span></span>

## <a name="connections"></a><span data-ttu-id="6c66b-157">연결</span><span class="sxs-lookup"><span data-stu-id="6c66b-157">Connections</span></span>
![연결 그래프](./media/cdn-real-time-stats/cdn-connections.png)

<span data-ttu-id="6c66b-159">이 그래프는 연결 수 설정 된 tooyour에 지 서버 였을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-159">This graph indicates how many connections have been established tooyour edge servers.</span></span> <span data-ttu-id="6c66b-160">CDN을 통과하는 자산에 대한 각 요청은 연결을 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="6c66b-160">Each request for an asset that passes through our CDN results in a connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c66b-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6c66b-161">Next Steps</span></span>
* <span data-ttu-id="6c66b-162">[Azure CDN에서 실시간 경고](cdn-real-time-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="6c66b-162">Get notified with [Real-time alerts in Azure CDN](cdn-real-time-alerts.md)</span></span>
* <span data-ttu-id="6c66b-163">[고급 HTTP 보고서](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="6c66b-163">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="6c66b-164">[사용 패턴](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="6c66b-164">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

