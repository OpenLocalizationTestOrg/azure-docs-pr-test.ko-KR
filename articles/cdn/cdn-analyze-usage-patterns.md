---
title: "Azure CDN 사용 패턴 분석 | Microsoft Docs"
description: "다음과 같은 보고서를 사용하여 CDN 사용 패턴을 볼 수 있습니다. 대역폭, 전송되는 데이터, 적중 횟수, 캐시 상태, 캐시 적중률, 전송되는 IPv4/IPv6 데이터"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 5a0d9018-8bdb-48ff-84df-23648ebcf763
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: aadbe872dd3384c8d337b432fb3be69422ca322b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-azure-cdn-usage-patterns"></a><span data-ttu-id="8b1d0-103">Azure CDN 사용 패턴 분석</span><span class="sxs-lookup"><span data-stu-id="8b1d0-103">Analyze Azure CDN usage patterns</span></span>

[!INCLUDE[cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="8b1d0-104">아래 가이드에서는 Verizon 프로필에 대한 관리 포털을 통해 핵심 보고서를 확인하는 단계를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-104">The guide below goes through the steps to view the core reports via the Manage portal for Verizon profiles.</span></span> <span data-ttu-id="8b1d0-105">또한 Verizon 및 Akamai 프로필에 대한 핵심 분석 데이터를 [Azure Portal을 통해](cdn-log-analysis.md) 저장소, 이벤트 허브 또는 Log Analytics(OMS)로 내보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-105">You may also export core analytics data to storage, event hub, or log analytics (oms) for both Verizon and Akamai profiles [through the azure portal](cdn-log-analysis.md).</span></span>

<span data-ttu-id="8b1d0-106">다음과 같은 보고서를 사용하여 CDN 사용 패턴을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-106">You can view usage patterns for your CDN using the following reports:</span></span>

* <span data-ttu-id="8b1d0-107">대역폭</span><span class="sxs-lookup"><span data-stu-id="8b1d0-107">Bandwidth</span></span>
* <span data-ttu-id="8b1d0-108">전송되는 데이터</span><span class="sxs-lookup"><span data-stu-id="8b1d0-108">Data Transferred</span></span>
* <span data-ttu-id="8b1d0-109">적중 횟수</span><span class="sxs-lookup"><span data-stu-id="8b1d0-109">Hits</span></span>
* <span data-ttu-id="8b1d0-110">캐시 상태</span><span class="sxs-lookup"><span data-stu-id="8b1d0-110">Cache Statuses</span></span>
* <span data-ttu-id="8b1d0-111">캐시 적중률</span><span class="sxs-lookup"><span data-stu-id="8b1d0-111">Cache Hit Ratio</span></span>
* <span data-ttu-id="8b1d0-112">전송되는 IPv4/IPv6 데이터</span><span class="sxs-lookup"><span data-stu-id="8b1d0-112">IPV4/IPV6 Data Transferred</span></span>

## <a name="accessing-core-reports"></a><span data-ttu-id="8b1d0-113">핵심 보고서 액세스</span><span class="sxs-lookup"><span data-stu-id="8b1d0-113">Accessing Core Reports</span></span>
1. <span data-ttu-id="8b1d0-114">CDN 프로필 블레이드에서 **관리** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-114">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![CDN 프로필 블레이드 관리 단추](./media/cdn-reports/cdn-manage-btn.png)
   
    <span data-ttu-id="8b1d0-116">CDN 관리 포털이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-116">The CDN management portal opens.</span></span>
2. <span data-ttu-id="8b1d0-117">**분석** 탭을 마우스로 가리킨 후 **핵심 보고서** 플라이아웃을 마우스로 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-117">Hover over the **Analytics** tab, then hover over the **Core Reports** flyout.</span></span>  <span data-ttu-id="8b1d0-118">메뉴에서 원하는 보고서를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-118">Click on the desired report in the menu.</span></span>
   
    ![CDN 관리 포털 - 핵심 보고서 메뉴](./media/cdn-reports/cdn-core-reports.png)

## <a name="bandwidth"></a><span data-ttu-id="8b1d0-120">대역폭</span><span class="sxs-lookup"><span data-stu-id="8b1d0-120">Bandwidth</span></span>
<span data-ttu-id="8b1d0-121">대역폭 보고서는 특정 기간의 HTTP 및 HTTPS 대역폭 사용량을 나타내는 그래프와 데이터 테이블로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-121">The bandwidth report consists of a graph and data table indicating the bandwidth usage for HTTP and HTTPS over a particular time period.</span></span> <span data-ttu-id="8b1d0-122">모든 CDN POP 또는 특정 POP의 대역폭 사용량을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-122">You can view the bandwidth usage across all CDN POPs or a particular POP.</span></span> <span data-ttu-id="8b1d0-123">이렇게 하면 CDN POP 간에 트래픽 급증 및 분산을 Mbps 단위로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-123">This allows you to view the traffic spikes and distribution across CDN POPs in Mbps.</span></span>

* <span data-ttu-id="8b1d0-124">모든 에지 노드를 선택하여 모든 노드의 트래픽을 보거나 드롭다운 목록에서 특정 지역/노드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-124">Select All Edge Nodes to see traffic from all nodes or choose a specific region/node from the dropdown list.</span></span>
* <span data-ttu-id="8b1d0-125">날짜 범위를 선택하여 오늘/이번 주/이번 달 등의 데이터를 보거나 사용자 지정 날짜를 입력한 다음 "이동"을 클릭하여 선택 항목이 업데이트되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-125">Select Date range to view data for today/this week/this month, etc. or enter custom dates, then click "go" to make sure your selection is updated.</span></span>
* <span data-ttu-id="8b1d0-126">"이동" 옆에 있는 Excel 시트 아이콘을 클릭하여 데이터를 내보내고 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-126">You can export and download the data by clicking the excel sheet icon located next to "go".</span></span>

<span data-ttu-id="8b1d0-127">보고서는 5분마다 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-127">The report is updated every 5 minutes.</span></span>

![대역폭 보고서](./media/cdn-reports/cdn-bandwidth.png)

## <a name="data-transferred"></a><span data-ttu-id="8b1d0-129">전송되는 데이터</span><span class="sxs-lookup"><span data-stu-id="8b1d0-129">Data transferred</span></span>
<span data-ttu-id="8b1d0-130">이 보고서는 특정 기간의 HTTP 및 HTTPS 트래픽 사용량을 나타내는 그래프와 데이터 테이블로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-130">This report consists of a graph and data table indicating the traffic usage for HTTP and HTTPS over a particular time period.</span></span> <span data-ttu-id="8b1d0-131">모든 CDN POP 또는 특정 POP의 트래픽 사용량을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-131">You can view the traffic usage across all CDN POPs or a particular POP.</span></span> <span data-ttu-id="8b1d0-132">이렇게 하면 CDN POP 간에 트래픽 급증 및 분산을 GB 단위로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-132">This allows you to view the traffic spikes and distribution across CDN POPs in GB.</span></span>

* <span data-ttu-id="8b1d0-133">모든 에지 노드를 선택하여 모든 노드의 트래픽을 보거나 드롭다운 목록에서 특정 지역/노드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-133">Select All Edge Nodes to see traffic from all notes or choose a specific region/node from the dropdown list.</span></span>
* <span data-ttu-id="8b1d0-134">날짜 범위를 선택하여 오늘/이번 주/이번 달 등의 데이터를 보거나 사용자 지정 날짜를 입력한 다음 "이동"을 클릭하여 선택 항목이 업데이트되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-134">Select Date range to view data for today/this week/this month, etc. or enter custom dates, then click "go" to make sure your selection is updated.</span></span>
* <span data-ttu-id="8b1d0-135">"이동" 옆에 있는 Excel 시트 아이콘을 클릭하여 데이터를 내보내고 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-135">You can export and download the data by clicking the excel sheet icon located next to "go" .</span></span>

<span data-ttu-id="8b1d0-136">보고서는 5분마다 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-136">The report is updated every 5 minutes.</span></span>

![전송되는 데이터 보고서](./media/cdn-reports/cdn-data-transferred.png)

## <a name="hits-status-codes"></a><span data-ttu-id="8b1d0-138">적중 횟수(상태 코드)</span><span class="sxs-lookup"><span data-stu-id="8b1d0-138">Hits (status codes)</span></span>
<span data-ttu-id="8b1d0-139">이 보고서는 콘텐츠에 대한 요청 상태 코드의 분포를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-139">This report describes the distribution of request status codes for your content.</span></span> <span data-ttu-id="8b1d0-140">각 콘텐츠 요청에서 HTTP 상태 코드가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-140">Every request for content will generate an HTTP status code.</span></span> <span data-ttu-id="8b1d0-141">상태 코드는 에지 POP가 요청을 처리한 방식을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-141">The status code describes how edge POPs handled the request.</span></span> <span data-ttu-id="8b1d0-142">예를 들어 2xx 상태 코드는 요청이 클라이언트로 성공적으로 처리되었음을 나타내는 반면, 4xx 상태 코드는 오류가 발생했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-142">For example, 2xx status codes indicate that the request was successfully served to a client, while a 4xx status code indicates an error occurred.</span></span> <span data-ttu-id="8b1d0-143">HTTP 상태 코드에 대한 자세한 내용은 [상태 코드](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-143">For more details about HTTP status code, see [status codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes).</span></span>

* <span data-ttu-id="8b1d0-144">날짜 범위를 선택하여 오늘/이번 주/이번 달 등의 데이터를 보거나 사용자 지정 날짜를 입력한 다음 "이동"을 클릭하여 선택 항목이 업데이트되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-144">Select Date range to view data for today/this week/this month, etc. or enter custom dates, then click "go" to make sure your selection is updated.</span></span>
* <span data-ttu-id="8b1d0-145">"이동" 옆에 있는 Excel 시트를 클릭하여 데이터를 내보내고 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-145">You can export and download the data by clicking the excel sheet located next to "go".</span></span>

![적중 횟수 보고서](./media/cdn-reports/cdn-hits.png)

## <a name="cache-statuses"></a><span data-ttu-id="8b1d0-147">캐시 상태</span><span class="sxs-lookup"><span data-stu-id="8b1d0-147">Cache statuses</span></span>
<span data-ttu-id="8b1d0-148">이 보고서는 클라이언트 요청에 대한 캐시 적중 횟수 및 캐시 누락 수 분포를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-148">This report describes the distribution of cache hits and cache misses for client request.</span></span> <span data-ttu-id="8b1d0-149">캐시 적중 횟수에서 가장 빠른 성능이 제공되므로 캐시 누락 수를 최소화하여 데이터 전달 속도를 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-149">Since the fastest performance comes from cache hits, you can optimize data delivery speeds by minimizing cache misses and expired cache hits.</span></span> <span data-ttu-id="8b1d0-150">"no-cache" 응답 헤더를 방지하도록 원본 서버를 구성하고, 엄격하게 필요한 경우를 제외하고 쿼리 문자열 캐싱을 방지하고, 캐시할 수 없는 응답 코드를 방지하여 캐시 누락 수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-150">Cache misses can be reduced by configuring your origin server to avoid assigning "no-cache" response headers, by avoiding query-string caching except where strictly needed, and by avoiding non-cacheable response codes.</span></span> <span data-ttu-id="8b1d0-151">자산의 max-age를 최대한 길게 설정하여 원본 서버에 대한 요청 수를 최소화하면 만료된 캐시 적중 횟수를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-151">Expired cache hits can be avoided by making an asset's max-age as long as possible to minimize the number of requests to the origin server.</span></span>

![캐시 상태 보고서](./media/cdn-reports/cdn-cache-statuses.png)

### <a name="main-cache-statuses-include"></a><span data-ttu-id="8b1d0-153">기본 캐시 상태는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-153">Main cache statuses include:</span></span>
* <span data-ttu-id="8b1d0-154">TCP_HIT: 에지에서 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-154">TCP_HIT: Served from Edge.</span></span> <span data-ttu-id="8b1d0-155">개체가 캐시에 있었으며 max-age를 초과하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-155">The object was in cache and had not exceeded its max-age.</span></span>
* <span data-ttu-id="8b1d0-156">TCP_MISS: 원본에서 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-156">TCP_MISS: Served from Origin.</span></span> <span data-ttu-id="8b1d0-157">개체가 캐시에 없었으며 응답이 다시 원본으로 전송되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-157">The object was not in cache and the response was back to origin.</span></span>
* <span data-ttu-id="8b1d0-158">TCP_EXPIRED _MISS: 원본을 사용하여 유효성을 재검사한 후 원본에서 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-158">TCP_EXPIRED _MISS: Served from origin after revalidation with origin.</span></span> <span data-ttu-id="8b1d0-159">개체가 캐시에 있었지만 max-age를 초과했습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-159">The object was in cache but had exceeded its max-age.</span></span> <span data-ttu-id="8b1d0-160">원본을 사용하여 유효성을 재검사한 후 캐시 개체가 원본의 새 응답으로 대체되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-160">A revalidation with origin resulted in the cache object being replaced by a new response from origin.</span></span>
* <span data-ttu-id="8b1d0-161">TCP_EXPIRED _HIT: 원본을 사용하여 유효성을 재검사한 후 에지에서 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-161">TCP_EXPIRED _HIT: Served from Edge after revalidation with origin.</span></span> <span data-ttu-id="8b1d0-162">개체가 캐시에 있었지만 max-age를 초과했습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-162">The object was in cache but had exceeded its max-age.</span></span> <span data-ttu-id="8b1d0-163">원본 서버를 사용하여 유효성을 재검사한 후 캐시 개체가 수정되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-163">A revalidation with the origin server resulted in the cache object being unmodified.</span></span>
* <span data-ttu-id="8b1d0-164">날짜 범위를 선택하여 오늘/이번 주/이번 달 등의 데이터를 보거나 사용자 지정 날짜를 입력한 다음 "이동"을 클릭하여 선택 항목이 업데이트되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-164">Select Date range to view data for today/this week/this month, etc. or enter custom dates, then click "go" to make sure your selection is updated.</span></span>
* <span data-ttu-id="8b1d0-165">"이동" 옆에 있는 Excel 시트 아이콘을 클릭하여 데이터를 내보내고 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-165">You can export and download the data by clicking the excel sheet icon located next to "go".</span></span>

### <a name="full-list-of-cache-statuses"></a><span data-ttu-id="8b1d0-166">캐시 상태 전체 목록</span><span class="sxs-lookup"><span data-stu-id="8b1d0-166">Full list of cache statuses</span></span>
* <span data-ttu-id="8b1d0-167">TCP_HIT - 요청이 POP에서 클라이언트로 직접 처리된 경우 이 상태가 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-167">TCP_HIT - This status is reported when a request is served directly from the POP to the client.</span></span> <span data-ttu-id="8b1d0-168">클라이언트에 가장 가까운 POP에 캐시되고 활성 시간이 만료된 유효한 TTL이 있는 경우 POP에서 즉시 자산이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-168">An asset is immediately served from a POP when it is cached on the POP closest to the client and it has a valid time-to-live, or TTL.</span></span> <span data-ttu-id="8b1d0-169">TTL은 다음 응답 헤더에 의해 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-169">TTL is determined by the following response headers:</span></span>
  
  * <span data-ttu-id="8b1d0-170">Cache-Control: s-maxage</span><span class="sxs-lookup"><span data-stu-id="8b1d0-170">Cache-Control: s-maxage</span></span>
  * <span data-ttu-id="8b1d0-171">Cache-Control: max-age</span><span class="sxs-lookup"><span data-stu-id="8b1d0-171">Cache-Control: max-age</span></span>
  * <span data-ttu-id="8b1d0-172">만료</span><span class="sxs-lookup"><span data-stu-id="8b1d0-172">Expires</span></span>
* <span data-ttu-id="8b1d0-173">TCP_MISS - 이 상태는 클라이언트에 가장 가까운 POP에서 요청된 자산의 캐시된 버전을 찾을 수 없음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-173">TCP_MISS - This status indicates that a cached version of the requested asset was not found on the POP closest to the client.</span></span> <span data-ttu-id="8b1d0-174">원본 서버 또는 원본 보호 서버의 자산이 요청됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-174">The asset will be requested from either an origin server or an origin shield server.</span></span> <span data-ttu-id="8b1d0-175">원본 서버 또는 원본 보호 서버가 자산을 반환하면 클라이언트에 제공되고 클라이언트와 에지 서버 둘 다에 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-175">If the origin server or the origin shield server returns an asset, it will be served to the client and cached on both the client and the edge server.</span></span> <span data-ttu-id="8b1d0-176">그렇지 않으면 200 이외의 상태 코드(예: 403 사용할 수 없음, 404 찾을 수 없음 등)가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-176">Otherwise, a non-200 status code (e.g., 403 Forbidden, 404 Not Found, etc.) will be returned.</span></span>
* <span data-ttu-id="8b1d0-177">TCP_EXPIRED _HIT - 자산의 max-age가 만료된 경우 등 TTL이 만료된 자산을 대상으로 하는 요청이 POP에서 클라이언트로 직접 처리된 경우 이 상태가 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-177">TCP_EXPIRED _HIT -  This status is reported when a request that targeted an asset with an expired TTL, such as when the asset's max-age has expired, was served directly from the POP to the client.</span></span>
  
    <span data-ttu-id="8b1d0-178">요청이 만료된 경우 일반적으로 원본 서버에 대한 유효성 재검사 요청이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-178">An expired request typically results in a revalidation request to the origin server.</span></span> <span data-ttu-id="8b1d0-179">TCP_EXPIRED _HIT가 발생하려면 원본 서버에서 자산의 최신 버전이 없음을 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-179">In order for a TCP_EXPIRED _HIT to occur, the origin server must indicate that a newer version of the asset does not exist.</span></span> <span data-ttu-id="8b1d0-180">이러한 상황에서는 일반적으로 해당 자산의 Cache-Control 및 Expires 헤더가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-180">This type of situation will typically update that asset's Cache-Control and Expires headers.</span></span>
* <span data-ttu-id="8b1d0-181">TCP_EXPIRED _MISS - 만료된 캐시된 자산의 최신 버전이 POP에서 클라이언트에 제공된 경우 이 상태가 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-181">TCP_EXPIRED _MISS - This status is reported when a newer version of an expired cached asset is served from the POP to the client.</span></span> <span data-ttu-id="8b1d0-182">이러한 상황은 캐시된 자산의 TTL이 만료되었으며(예: 만료된 max-age) 원본 서버가 해당 자산의 최신 버전을 반환하는 경우에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-182">This occurs when the TTL for a cached asset has expired (e.g., expired max-age) and the origin server returns a newer version of that asset.</span></span> <span data-ttu-id="8b1d0-183">캐시된 버전 대신 이 새로운 버전의 자산이 클라이언트에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-183">This new version of the asset will be served to the client instead of the cached version.</span></span> <span data-ttu-id="8b1d0-184">또한 에지 서버와 클라이언트에 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-184">Additionally, it will be cached on the edge server and the client.</span></span>
* <span data-ttu-id="8b1d0-185">CONFIG_NOCACHE - 이 상태는 에지 POP의 고객별 구성에서 자산이 캐시되지 않도록 차단했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-185">CONFIG_NOCACHE - This status indicates that a customer-specific configuration on our edge POP prevented the asset from being cached.</span></span>
* <span data-ttu-id="8b1d0-186">NONE - 이 상태는 캐시 콘텐츠 새로 고침 검사가 수행되지 않았음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-186">NONE - This status indicates that a cache content freshness check was not performed.</span></span>
* <span data-ttu-id="8b1d0-187">TCP_ CLIENT_REFRESH _MISS - HTTP 클라이언트(예: 브라우저)에서 에지 POP가 원본 서버에서 부실 자산의 새 버전을 검색하도록 강제하는 경우 이 상태가 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-187">TCP_ CLIENT_REFRESH _MISS - This status is reported when an HTTP client (e.g., browser) forces an edge POP to retrieve a new version of a stale asset from the origin server.</span></span>
  
    <span data-ttu-id="8b1d0-188">기본적으로 서버는 HTTP 클라이언트에서 에지 서버가 원본 서버에서 자산의 새 버전을 검색하도록 강제할 수 없게 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-188">By default, our servers prevent an HTTP client from forcing our edge servers to retrieve a new version of the asset from the origin server.</span></span>
* <span data-ttu-id="8b1d0-189">TCP_ PARTIAL_HIT - 바이트 범위 요청에 의해 부분적으로 캐시된 자산이 적중되는 경우 이 상태가 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-189">TCP_ PARTIAL_HIT - This status is reported when a byte range request results in a hit for a partially cached asset.</span></span> <span data-ttu-id="8b1d0-190">요청된 바이트 범위는 POP에서 클라이언트에 즉시 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-190">The requested byte range is immediately served from the POP to the client.</span></span>
* <span data-ttu-id="8b1d0-191">UNCACHEABLE - 자산의 Cache-Control 및 Expires 헤더에서 POP 또는 HTTP 클라이언트에 캐시되지 않도록 표시하는 경우 이 상태가 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-191">UNCACHEABLE - This status is reported when an asset's Cache-Control and Expires headers indicate that it should not be cached on a POP or by the HTTP client.</span></span> <span data-ttu-id="8b1d0-192">이러한 유형의 요청은 원본 서버에서 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-192">These types of requests are served from the origin server</span></span>

## <a name="cache-hit-ratio"></a><span data-ttu-id="8b1d0-193">캐시 적중률</span><span class="sxs-lookup"><span data-stu-id="8b1d0-193">Cache Hit Ratio</span></span>
<span data-ttu-id="8b1d0-194">이 보고서는 캐시에서 직접 처리된 캐시된 요청 비율을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-194">This report indicates the percentage of cached requests that were served directly from cache.</span></span>

<span data-ttu-id="8b1d0-195">보고서는 다음과 같은 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-195">The report provides the following details:</span></span>

* <span data-ttu-id="8b1d0-196">요청한 콘텐츠가 요청자에게 가장 가까운 POP에 캐시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-196">The requested content was cached on the POP closest to the requester.</span></span>
* <span data-ttu-id="8b1d0-197">네트워크 에지에서 직접 요청이 처리되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-197">The request was served directly from the edge of our network.</span></span>
* <span data-ttu-id="8b1d0-198">요청에 원본 서버를 사용한 유효성 재검사가 필요하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-198">The request did not require revalidation with the origin server.</span></span>

<span data-ttu-id="8b1d0-199">보고서에 포함되지 않는 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-199">The report doesn't include:</span></span>

* <span data-ttu-id="8b1d0-200">국가 필터링 옵션으로 인해 거부된 요청</span><span class="sxs-lookup"><span data-stu-id="8b1d0-200">Requests that are denied due to country filtering options.</span></span>
* <span data-ttu-id="8b1d0-201">헤더에 캐시하지 않도록 표시된 자산에 대한 요청</span><span class="sxs-lookup"><span data-stu-id="8b1d0-201">Requests for assets whose headers indicate that they should not be cached.</span></span> <span data-ttu-id="8b1d0-202">예를 들어 Cache-Control: private, Cache-Control: no-cache 또는 Pragma: no-cache 헤더는 자산이 캐시되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-202">For example, Cache-Control: private, Cache-Control: no-cache, or Pragma: no-cache headers will prevent an asset from being cached.</span></span>
* <span data-ttu-id="8b1d0-203">부분적으로 캐시된 콘텐츠에 대한 바이트 범위 요청.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-203">Byte range requests for partially cached content.</span></span>

<span data-ttu-id="8b1d0-204">수식은 (TCP_ HIT/(TCP_ HIT+TCP_MISS))*100입니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-204">The formula is: (TCP_ HIT/(TCP_ HIT+TCP_MISS))*100</span></span>

* <span data-ttu-id="8b1d0-205">날짜 범위를 선택하여 오늘/이번 주/이번 달 등의 데이터를 보거나 사용자 지정 날짜를 입력한 다음 "이동"을 클릭하여 선택 항목이 업데이트되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-205">Select Date range to view data for today/this week/this month, etc. or enter custom dates, then click "go" to make sure your selection is updated.</span></span>
* <span data-ttu-id="8b1d0-206">"이동" 옆에 있는 Excel 시트 아이콘을 클릭하여 데이터를 내보내고 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-206">You can export and download the data by clicking the excel sheet icon located next to "go" .</span></span>

![캐시 적중률 보고서](./media/cdn-reports/cdn-cache-hit-ratio.png)

## <a name="ipv4ipv6-data-transferred"></a><span data-ttu-id="8b1d0-208">전송되는 IPv4/IPv6 데이터</span><span class="sxs-lookup"><span data-stu-id="8b1d0-208">IPV4/IPV6 Data transferred</span></span>
<span data-ttu-id="8b1d0-209">이 보고서는 IPv4 및 IPv6의 트래픽 사용량 분포를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-209">This report shows the traffic usage distribution in IPV4 vs IPV6.</span></span>

![전송되는 IPv4/IPv6 데이터](./media/cdn-reports/cdn-ipv4-ipv6.png)

* <span data-ttu-id="8b1d0-211">날짜 범위를 선택하여 오늘/이번 주/이번 달 등의 데이터를 보거나 사용자 지정 날짜를 입력한 다음</span><span class="sxs-lookup"><span data-stu-id="8b1d0-211">Select Date range to view data for today/this week/this month, etc. or enter custom dates.</span></span>
* <span data-ttu-id="8b1d0-212">"이동"을 클릭하여 선택 항목이 업데이트되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-212">Then, click "go" to make sure your selection is updated.</span></span>

## <a name="considerations"></a><span data-ttu-id="8b1d0-213">고려 사항</span><span class="sxs-lookup"><span data-stu-id="8b1d0-213">Considerations</span></span>
<span data-ttu-id="8b1d0-214">보고서는 최근 18개월 내에서만 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b1d0-214">Reports can only be generated within the last 18 months.</span></span>

