---
title: "Log Analytics의 IIS 로그 | Microsoft Docs"
description: "IIS(인터넷 정보 서비스)는 Log Analytics에서 수집할 수 있는 로그 파일에 사용자 활동을 저장합니다.  이 문서에서는 IIS 로그 수집을 구성하는 방법을 설명하고, OMS 리포지토리에 생성되는 레코드에 대한 자세한 정보를 제공합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: cec5ff0a-01f5-4262-b2e8-e3db7b7467d2
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: bwren
ms.openlocfilehash: 2114bdafb3b9fe2eb0632271840b8b70a76d10f1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="iis-logs-in-log-analytics"></a><span data-ttu-id="f0c64-104">Log Analytics의 IIS 로그</span><span class="sxs-lookup"><span data-stu-id="f0c64-104">IIS logs in Log Analytics</span></span>
<span data-ttu-id="f0c64-105">IIS(인터넷 정보 서비스)는 Log Analytics에서 수집할 수 있는 로그 파일에 사용자 활동을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-105">Internet Information Services (IIS) stores user activity in log files that can be collected by Log Analytics.</span></span>  

![IIS 로그](media/log-analytics-data-sources-iis-logs/overview.png)

## <a name="configuring-iis-logs"></a><span data-ttu-id="f0c64-107">IIS 로그 구성</span><span class="sxs-lookup"><span data-stu-id="f0c64-107">Configuring IIS logs</span></span>
<span data-ttu-id="f0c64-108">Log Analytics는 IIS에서 생성된 로그 파일의 항목을 수집하므로 [로깅에 대해 IIS를 구성](https://technet.microsoft.com/library/hh831775.aspx)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-108">Log Analytics collects entries from log files created by IIS, so you must [configure IIS for logging](https://technet.microsoft.com/library/hh831775.aspx).</span></span>

<span data-ttu-id="f0c64-109">Log Analytics는 W3C 형식으로 저장된 IIS 로그 파일만 지원하며 사용자 지정 필드 또는 IIS 고급 로깅을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-109">Log Analytics only supports IIS log files stored in W3C format and does not support custom fields or IIS Advanced Logging.</span></span>  
<span data-ttu-id="f0c64-110">Log Analytics는 NCSA 또는 IIS 네이티브 형식의 로그를 수집하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-110">Log Analytics does not collect logs in NCSA or IIS native format.</span></span>

<span data-ttu-id="f0c64-111">[Log Analytics 설정의 데이터 메뉴](log-analytics-data-sources.md#configuring-data-sources)에서 Log Analytics의 IIS 로그를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-111">Configure IIS logs in Log Analytics from the [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>  <span data-ttu-id="f0c64-112">**W3C 형식 IIS 로그 파일 수집**을 선택하는 것 외에 다른 구성은 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-112">There is no configuration required other than selecting **Collect W3C format IIS log files**.</span></span>

<span data-ttu-id="f0c64-113">IIS 로그 수집을 사용하도록 설정하는 경우 각 서버에서 IIS 로그 롤오버 설정을 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-113">We recommend that when you enable IIS log collection, you should configure the IIS log rollover setting on each server.</span></span>

## <a name="data-collection"></a><span data-ttu-id="f0c64-114">데이터 수집</span><span class="sxs-lookup"><span data-stu-id="f0c64-114">Data collection</span></span>
<span data-ttu-id="f0c64-115">Log Analytics는 연결된 각 원본에서 대략 15분마다 IIS 로그 항목을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-115">Log Analytics collects IIS log entries from each connected source approximately every 15 minutes.</span></span>  <span data-ttu-id="f0c64-116">에이전트는 수집하는 각 이벤트 로그에 해당 위치를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-116">The agent records its place in each event log that it collects from.</span></span>  <span data-ttu-id="f0c64-117">에이전트가 오프라인 상태로 전환된 경우 Log Analytics는 마지막으로 오프라인 상태가 유지된 위치에서 이벤트를 수집하며, 이는 에이전트가 오프라인 상태에 있는 동안 해당 이벤트가 생성된 경우에도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-117">If the agent goes offline, then Log Analytics collects events from where it last left off, even if those events were created while the agent was offline.</span></span>

## <a name="iis-log-record-properties"></a><span data-ttu-id="f0c64-118">IIS 로그 레코드 속성</span><span class="sxs-lookup"><span data-stu-id="f0c64-118">IIS log record properties</span></span>
<span data-ttu-id="f0c64-119">IIS 로그 레코드는 **W3CIISLog** 형식이며, 다음 표의 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-119">IIS log records have a type of **W3CIISLog** and have the properties in the following table:</span></span>

| <span data-ttu-id="f0c64-120">속성</span><span class="sxs-lookup"><span data-stu-id="f0c64-120">Property</span></span> | <span data-ttu-id="f0c64-121">설명</span><span class="sxs-lookup"><span data-stu-id="f0c64-121">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f0c64-122">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="f0c64-122">Computer</span></span> |<span data-ttu-id="f0c64-123">이벤트가 수집된 컴퓨터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-123">Name of the computer that the event was collected from.</span></span> |
| <span data-ttu-id="f0c64-124">cIP</span><span class="sxs-lookup"><span data-stu-id="f0c64-124">cIP</span></span> |<span data-ttu-id="f0c64-125">클라이언트의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-125">IP address of the client.</span></span> |
| <span data-ttu-id="f0c64-126">csMethod</span><span class="sxs-lookup"><span data-stu-id="f0c64-126">csMethod</span></span> |<span data-ttu-id="f0c64-127">GET 또는 POST와 같은 요청 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-127">Method of the request such as GET or POST.</span></span> |
| <span data-ttu-id="f0c64-128">csReferer</span><span class="sxs-lookup"><span data-stu-id="f0c64-128">csReferer</span></span> |<span data-ttu-id="f0c64-129">사용자가 현재 사이트로 이동하는 데 사용된 링크가 있던 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-129">Site that the user followed a link from to the current site.</span></span> |
| <span data-ttu-id="f0c64-130">csUserAgent</span><span class="sxs-lookup"><span data-stu-id="f0c64-130">csUserAgent</span></span> |<span data-ttu-id="f0c64-131">클라이언트의 브라우저 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-131">Browser type of the client.</span></span> |
| <span data-ttu-id="f0c64-132">csUserName</span><span class="sxs-lookup"><span data-stu-id="f0c64-132">csUserName</span></span> |<span data-ttu-id="f0c64-133">서버에 액세스한 인증된 사용자의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-133">Name of the authenticated user that accessed the server.</span></span> <span data-ttu-id="f0c64-134">익명 사용자는 하이픈으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-134">Anonymous users are indicated by a hyphen.</span></span> |
| <span data-ttu-id="f0c64-135">csUriStem</span><span class="sxs-lookup"><span data-stu-id="f0c64-135">csUriStem</span></span> |<span data-ttu-id="f0c64-136">웹 페이지와 같은 요청의 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-136">Target of the request such as a web page.</span></span> |
| <span data-ttu-id="f0c64-137">csUriQuery</span><span class="sxs-lookup"><span data-stu-id="f0c64-137">csUriQuery</span></span> |<span data-ttu-id="f0c64-138">클라이언트가 수행하려고 한 쿼리입니다(있는 경우).</span><span class="sxs-lookup"><span data-stu-id="f0c64-138">Query, if any, that the client was trying to perform.</span></span> |
| <span data-ttu-id="f0c64-139">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="f0c64-139">ManagementGroupName</span></span> |<span data-ttu-id="f0c64-140">Operations Manager 에이전트의 관리 그룹 이름.</span><span class="sxs-lookup"><span data-stu-id="f0c64-140">Name of the management group for Operations Manager agents.</span></span>  <span data-ttu-id="f0c64-141">다른 에이전트의 경우 AOI-\<작업 영역 ID\>입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-141">For other agents, this is AOI-\<workspace ID\></span></span> |
| <span data-ttu-id="f0c64-142">RemoteIPCountry</span><span class="sxs-lookup"><span data-stu-id="f0c64-142">RemoteIPCountry</span></span> |<span data-ttu-id="f0c64-143">클라이언트의 IP 주소 국가입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-143">Country of the IP address of the client.</span></span> |
| <span data-ttu-id="f0c64-144">RemoteIPLatitude</span><span class="sxs-lookup"><span data-stu-id="f0c64-144">RemoteIPLatitude</span></span> |<span data-ttu-id="f0c64-145">클라이언트 IP 주소의 위도입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-145">Latitude of the client IP address.</span></span> |
| <span data-ttu-id="f0c64-146">RemoteIPLongitude</span><span class="sxs-lookup"><span data-stu-id="f0c64-146">RemoteIPLongitude</span></span> |<span data-ttu-id="f0c64-147">클라이언트 IP 주소의 경도입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-147">Longitude of the client IP address.</span></span> |
| <span data-ttu-id="f0c64-148">scStatus</span><span class="sxs-lookup"><span data-stu-id="f0c64-148">scStatus</span></span> |<span data-ttu-id="f0c64-149">HTTP 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-149">HTTP status code.</span></span> |
| <span data-ttu-id="f0c64-150">scSubStatus</span><span class="sxs-lookup"><span data-stu-id="f0c64-150">scSubStatus</span></span> |<span data-ttu-id="f0c64-151">하위 상태 오류 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-151">Substatus error code.</span></span> |
| <span data-ttu-id="f0c64-152">scWin32Status</span><span class="sxs-lookup"><span data-stu-id="f0c64-152">scWin32Status</span></span> |<span data-ttu-id="f0c64-153">Windows 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-153">Windows status code.</span></span> |
| <span data-ttu-id="f0c64-154">sIP</span><span class="sxs-lookup"><span data-stu-id="f0c64-154">sIP</span></span> |<span data-ttu-id="f0c64-155">웹 서버의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-155">IP address of the web server.</span></span> |
| <span data-ttu-id="f0c64-156">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="f0c64-156">SourceSystem</span></span> |<span data-ttu-id="f0c64-157">OpsMgr</span><span class="sxs-lookup"><span data-stu-id="f0c64-157">OpsMgr</span></span> |
| <span data-ttu-id="f0c64-158">sPort</span><span class="sxs-lookup"><span data-stu-id="f0c64-158">sPort</span></span> |<span data-ttu-id="f0c64-159">클라이언트가 연결된 서버의 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-159">Port on the server the client connected to.</span></span> |
| <span data-ttu-id="f0c64-160">sSiteName</span><span class="sxs-lookup"><span data-stu-id="f0c64-160">sSiteName</span></span> |<span data-ttu-id="f0c64-161">IIS 사이트의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-161">Name of the IIS site.</span></span> |
| <span data-ttu-id="f0c64-162">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="f0c64-162">TimeGenerated</span></span> |<span data-ttu-id="f0c64-163">항목이 로깅된 날짜 및 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-163">Date and time the entry was logged.</span></span> |
| <span data-ttu-id="f0c64-164">TimeTaken</span><span class="sxs-lookup"><span data-stu-id="f0c64-164">TimeTaken</span></span> |<span data-ttu-id="f0c64-165">요청을 처리할 시간의 길이(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-165">Length of time to process the request in milliseconds.</span></span> |

## <a name="log-searches-with-iis-logs"></a><span data-ttu-id="f0c64-166">IIS 로그로 로그 검색</span><span class="sxs-lookup"><span data-stu-id="f0c64-166">Log searches with IIS logs</span></span>
<span data-ttu-id="f0c64-167">다음 표에는 IIS 로그 레코드를 검색하는 로그 쿼리의 여러 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-167">The following table provides different examples of log queries that retrieve IIS log records.</span></span>

| <span data-ttu-id="f0c64-168">쿼리</span><span class="sxs-lookup"><span data-stu-id="f0c64-168">Query</span></span> | <span data-ttu-id="f0c64-169">설명</span><span class="sxs-lookup"><span data-stu-id="f0c64-169">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f0c64-170">Type=W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="f0c64-170">Type=W3CIISLog</span></span> |<span data-ttu-id="f0c64-171">모든 IIS 로그 레코드</span><span class="sxs-lookup"><span data-stu-id="f0c64-171">All IIS log records.</span></span> |
| <span data-ttu-id="f0c64-172">Type=W3CIISLog scStatus=500</span><span class="sxs-lookup"><span data-stu-id="f0c64-172">Type=W3CIISLog scStatus=500</span></span> |<span data-ttu-id="f0c64-173">반환 상태가 500인 모든 IIS 로그 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-173">All IIS log records with a return status of 500.</span></span> |
| <span data-ttu-id="f0c64-174">Type=W3CIISLog &#124; Measure count() by cIP</span><span class="sxs-lookup"><span data-stu-id="f0c64-174">Type=W3CIISLog &#124; Measure count() by cIP</span></span> |<span data-ttu-id="f0c64-175">클라이언트 IP 주소별 IIS 로그 항목 수</span><span class="sxs-lookup"><span data-stu-id="f0c64-175">Count of IIS log entries by client IP address.</span></span> |
| <span data-ttu-id="f0c64-176">Type=W3CIISLog csHost="www.contoso.com" &#124; Measure count() by csUriStem</span><span class="sxs-lookup"><span data-stu-id="f0c64-176">Type=W3CIISLog csHost="www.contoso.com" &#124; Measure count() by csUriStem</span></span> |<span data-ttu-id="f0c64-177">호스트 www.contoso.com의 URL별 IIS 로그 항목 수</span><span class="sxs-lookup"><span data-stu-id="f0c64-177">Count of IIS log entries by URL for the host www.contoso.com.</span></span> |
| <span data-ttu-id="f0c64-178">Type=W3CIISLog &#124; Measure Sum(csBytes) by Computer &#124; top 500000</span><span class="sxs-lookup"><span data-stu-id="f0c64-178">Type=W3CIISLog &#124; Measure Sum(csBytes) by Computer &#124; top 500000</span></span> |<span data-ttu-id="f0c64-179">각 IIS 컴퓨터에서 받은 총 바이트 수</span><span class="sxs-lookup"><span data-stu-id="f0c64-179">Total bytes received by each IIS computer.</span></span> |

>[!NOTE]
> <span data-ttu-id="f0c64-180">작업 영역을 [새 Log Analytics 쿼리 언어](log-analytics-log-search-upgrade.md)로 업그레이드한 경우에는 위의 쿼리가 다음과 같이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-180">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above queries would change to the following.</span></span>

> | <span data-ttu-id="f0c64-181">쿼리</span><span class="sxs-lookup"><span data-stu-id="f0c64-181">Query</span></span> | <span data-ttu-id="f0c64-182">설명</span><span class="sxs-lookup"><span data-stu-id="f0c64-182">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f0c64-183">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="f0c64-183">W3CIISLog</span></span> |<span data-ttu-id="f0c64-184">모든 IIS 로그 레코드</span><span class="sxs-lookup"><span data-stu-id="f0c64-184">All IIS log records.</span></span> |
| <span data-ttu-id="f0c64-185">W3CIISLog &#124; where scStatus==500</span><span class="sxs-lookup"><span data-stu-id="f0c64-185">W3CIISLog &#124; where scStatus==500</span></span> |<span data-ttu-id="f0c64-186">반환 상태가 500인 모든 IIS 로그 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-186">All IIS log records with a return status of 500.</span></span> |
| <span data-ttu-id="f0c64-187">W3CIISLog &#124; summarize count() by cIP</span><span class="sxs-lookup"><span data-stu-id="f0c64-187">W3CIISLog &#124; summarize count() by cIP</span></span> |<span data-ttu-id="f0c64-188">클라이언트 IP 주소별 IIS 로그 항목 수</span><span class="sxs-lookup"><span data-stu-id="f0c64-188">Count of IIS log entries by client IP address.</span></span> |
| <span data-ttu-id="f0c64-189">W3CIISLog &#124; where csHost=="www.contoso.com" &#124; summarize count() by csUriStem</span><span class="sxs-lookup"><span data-stu-id="f0c64-189">W3CIISLog &#124; where csHost=="www.contoso.com" &#124; summarize count() by csUriStem</span></span> |<span data-ttu-id="f0c64-190">호스트 www.contoso.com의 URL별 IIS 로그 항목 수</span><span class="sxs-lookup"><span data-stu-id="f0c64-190">Count of IIS log entries by URL for the host www.contoso.com.</span></span> |
| <span data-ttu-id="f0c64-191">W3CIISLog &#124; summarize sum(csBytes) by Computer &#124; take 500000</span><span class="sxs-lookup"><span data-stu-id="f0c64-191">W3CIISLog &#124; summarize sum(csBytes) by Computer &#124; take 500000</span></span> |<span data-ttu-id="f0c64-192">각 IIS 컴퓨터에서 받은 총 바이트 수</span><span class="sxs-lookup"><span data-stu-id="f0c64-192">Total bytes received by each IIS computer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f0c64-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f0c64-193">Next steps</span></span>
* <span data-ttu-id="f0c64-194">분석을 위해 다른 [데이터 원본](log-analytics-data-sources.md) 을 수집하도록 Log Analytics를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-194">Configure Log Analytics to collect other [data sources](log-analytics-data-sources.md) for analysis.</span></span>
* <span data-ttu-id="f0c64-195">데이터 원본 및 솔루션에서 수집한 데이터를 분석하기 위해 [로그 검색](log-analytics-log-searches.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-195">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span>
* <span data-ttu-id="f0c64-196">IIS 로그에서 발견된 중요한 조건을 사전에 알리도록 Log Analytics의 경고를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c64-196">Configure alerts in Log Analytics to proactively notify you of important conditions found in IIS logs.</span></span>
