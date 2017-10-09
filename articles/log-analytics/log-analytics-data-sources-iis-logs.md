---
title: "로그 분석에 aaaIIS 기록 | Microsoft Docs"
description: "IIS(인터넷 정보 서비스)는 Log Analytics에서 수집할 수 있는 로그 파일에 사용자 활동을 저장합니다.  이 문서는 hello 레코드의 세부 정보 및 IIS 로그 컬렉션 tooconfigure 작성 방법과 hello OMS 리포지토리에 대해 설명 합니다."
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
ms.openlocfilehash: c5575351090cdabaf651bcb49867794ee3a4b6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="iis-logs-in-log-analytics"></a><span data-ttu-id="516c1-104">Log Analytics의 IIS 로그</span><span class="sxs-lookup"><span data-stu-id="516c1-104">IIS logs in Log Analytics</span></span>
<span data-ttu-id="516c1-105">IIS(인터넷 정보 서비스)는 Log Analytics에서 수집할 수 있는 로그 파일에 사용자 활동을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-105">Internet Information Services (IIS) stores user activity in log files that can be collected by Log Analytics.</span></span>  

![IIS 로그](media/log-analytics-data-sources-iis-logs/overview.png)

## <a name="configuring-iis-logs"></a><span data-ttu-id="516c1-107">IIS 로그 구성</span><span class="sxs-lookup"><span data-stu-id="516c1-107">Configuring IIS logs</span></span>
<span data-ttu-id="516c1-108">Log Analytics는 IIS에서 생성된 로그 파일의 항목을 수집하므로 [로깅에 대해 IIS를 구성](https://technet.microsoft.com/library/hh831775.aspx)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-108">Log Analytics collects entries from log files created by IIS, so you must [configure IIS for logging](https://technet.microsoft.com/library/hh831775.aspx).</span></span>

<span data-ttu-id="516c1-109">Log Analytics는 W3C 형식으로 저장된 IIS 로그 파일만 지원하며 사용자 지정 필드 또는 IIS 고급 로깅을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-109">Log Analytics only supports IIS log files stored in W3C format and does not support custom fields or IIS Advanced Logging.</span></span>  
<span data-ttu-id="516c1-110">Log Analytics는 NCSA 또는 IIS 네이티브 형식의 로그를 수집하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-110">Log Analytics does not collect logs in NCSA or IIS native format.</span></span>

<span data-ttu-id="516c1-111">로그 분석에서 hello에서 IIS 로그를 구성 [로그 분석 설정의 데이터 메뉴](log-analytics-data-sources.md#configuring-data-sources)합니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-111">Configure IIS logs in Log Analytics from hello [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>  <span data-ttu-id="516c1-112">**W3C 형식 IIS 로그 파일 수집**을 선택하는 것 외에 다른 구성은 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-112">There is no configuration required other than selecting **Collect W3C format IIS log files**.</span></span>

<span data-ttu-id="516c1-113">IIS 로그 컬렉션을 사용 하도록 설정 하면 각 서버에서 hello IIS 로그 롤오버 설정을 구성 해야 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-113">We recommend that when you enable IIS log collection, you should configure hello IIS log rollover setting on each server.</span></span>

## <a name="data-collection"></a><span data-ttu-id="516c1-114">데이터 수집</span><span class="sxs-lookup"><span data-stu-id="516c1-114">Data collection</span></span>
<span data-ttu-id="516c1-115">Log Analytics는 연결된 각 원본에서 대략 15분마다 IIS 로그 항목을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-115">Log Analytics collects IIS log entries from each connected source approximately every 15 minutes.</span></span>  <span data-ttu-id="516c1-116">hello 에이전트를 수집 하는 각 이벤트 로그에 해당 위치를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-116">hello agent records its place in each event log that it collects from.</span></span>  <span data-ttu-id="516c1-117">Hello 에이전트 오프 라인인 경우 다음 로그 분석에서 이벤트를 수집 마지막 중단, 이러한 이벤트는 hello 에이전트 오프 라인 상태인 동안 생성 된 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-117">If hello agent goes offline, then Log Analytics collects events from where it last left off, even if those events were created while hello agent was offline.</span></span>

## <a name="iis-log-record-properties"></a><span data-ttu-id="516c1-118">IIS 로그 레코드 속성</span><span class="sxs-lookup"><span data-stu-id="516c1-118">IIS log record properties</span></span>
<span data-ttu-id="516c1-119">IIS 로그 레코드에는 형식이 **W3CIISLog** 한 hello 속성의 다음 표에 hello:</span><span class="sxs-lookup"><span data-stu-id="516c1-119">IIS log records have a type of **W3CIISLog** and have hello properties in hello following table:</span></span>

| <span data-ttu-id="516c1-120">속성</span><span class="sxs-lookup"><span data-stu-id="516c1-120">Property</span></span> | <span data-ttu-id="516c1-121">설명</span><span class="sxs-lookup"><span data-stu-id="516c1-121">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="516c1-122">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="516c1-122">Computer</span></span> |<span data-ttu-id="516c1-123">이벤트 hello hello 컴퓨터의 이름에서 수집 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-123">Name of hello computer that hello event was collected from.</span></span> |
| <span data-ttu-id="516c1-124">cIP</span><span class="sxs-lookup"><span data-stu-id="516c1-124">cIP</span></span> |<span data-ttu-id="516c1-125">Hello 클라이언트의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-125">IP address of hello client.</span></span> |
| <span data-ttu-id="516c1-126">csMethod</span><span class="sxs-lookup"><span data-stu-id="516c1-126">csMethod</span></span> |<span data-ttu-id="516c1-127">GET 또는 POST 등 hello 요청의 메서드.</span><span class="sxs-lookup"><span data-stu-id="516c1-127">Method of hello request such as GET or POST.</span></span> |
| <span data-ttu-id="516c1-128">csReferer</span><span class="sxs-lookup"><span data-stu-id="516c1-128">csReferer</span></span> |<span data-ttu-id="516c1-129">해당 hello 사이트 toohello 현재 사이트에서 사용자가 링크를 팔 로우.</span><span class="sxs-lookup"><span data-stu-id="516c1-129">Site that hello user followed a link from toohello current site.</span></span> |
| <span data-ttu-id="516c1-130">csUserAgent</span><span class="sxs-lookup"><span data-stu-id="516c1-130">csUserAgent</span></span> |<span data-ttu-id="516c1-131">Hello 클라이언트의 브라우저 종류입니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-131">Browser type of hello client.</span></span> |
| <span data-ttu-id="516c1-132">csUserName</span><span class="sxs-lookup"><span data-stu-id="516c1-132">csUserName</span></span> |<span data-ttu-id="516c1-133">Hello 서버에 액세스 하는 사용자를 인증 하는 hello의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-133">Name of hello authenticated user that accessed hello server.</span></span> <span data-ttu-id="516c1-134">익명 사용자는 하이픈으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-134">Anonymous users are indicated by a hyphen.</span></span> |
| <span data-ttu-id="516c1-135">csUriStem</span><span class="sxs-lookup"><span data-stu-id="516c1-135">csUriStem</span></span> |<span data-ttu-id="516c1-136">Hello 요청 웹 페이지 등의 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-136">Target of hello request such as a web page.</span></span> |
| <span data-ttu-id="516c1-137">csUriQuery</span><span class="sxs-lookup"><span data-stu-id="516c1-137">csUriQuery</span></span> |<span data-ttu-id="516c1-138">쿼리를 있는 경우 해당 hello 클라이언트 tooperform을 시도 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-138">Query, if any, that hello client was trying tooperform.</span></span> |
| <span data-ttu-id="516c1-139">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="516c1-139">ManagementGroupName</span></span> |<span data-ttu-id="516c1-140">Operations Manager 에이전트에 대 한 hello 관리 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-140">Name of hello management group for Operations Manager agents.</span></span>  <span data-ttu-id="516c1-141">다른 에이전트의 경우 AOI-\<작업 영역 ID\>입니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-141">For other agents, this is AOI-\<workspace ID\></span></span> |
| <span data-ttu-id="516c1-142">RemoteIPCountry</span><span class="sxs-lookup"><span data-stu-id="516c1-142">RemoteIPCountry</span></span> |<span data-ttu-id="516c1-143">Hello 클라이언트의 IP 주소 hello의 국가입니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-143">Country of hello IP address of hello client.</span></span> |
| <span data-ttu-id="516c1-144">RemoteIPLatitude</span><span class="sxs-lookup"><span data-stu-id="516c1-144">RemoteIPLatitude</span></span> |<span data-ttu-id="516c1-145">위도 hello 클라이언트 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-145">Latitude of hello client IP address.</span></span> |
| <span data-ttu-id="516c1-146">RemoteIPLongitude</span><span class="sxs-lookup"><span data-stu-id="516c1-146">RemoteIPLongitude</span></span> |<span data-ttu-id="516c1-147">경도 hello 클라이언트 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-147">Longitude of hello client IP address.</span></span> |
| <span data-ttu-id="516c1-148">scStatus</span><span class="sxs-lookup"><span data-stu-id="516c1-148">scStatus</span></span> |<span data-ttu-id="516c1-149">HTTP 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-149">HTTP status code.</span></span> |
| <span data-ttu-id="516c1-150">scSubStatus</span><span class="sxs-lookup"><span data-stu-id="516c1-150">scSubStatus</span></span> |<span data-ttu-id="516c1-151">하위 상태 오류 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-151">Substatus error code.</span></span> |
| <span data-ttu-id="516c1-152">scWin32Status</span><span class="sxs-lookup"><span data-stu-id="516c1-152">scWin32Status</span></span> |<span data-ttu-id="516c1-153">Windows 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-153">Windows status code.</span></span> |
| <span data-ttu-id="516c1-154">sIP</span><span class="sxs-lookup"><span data-stu-id="516c1-154">sIP</span></span> |<span data-ttu-id="516c1-155">Hello 웹 서버의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-155">IP address of hello web server.</span></span> |
| <span data-ttu-id="516c1-156">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="516c1-156">SourceSystem</span></span> |<span data-ttu-id="516c1-157">OpsMgr</span><span class="sxs-lookup"><span data-stu-id="516c1-157">OpsMgr</span></span> |
| <span data-ttu-id="516c1-158">sPort</span><span class="sxs-lookup"><span data-stu-id="516c1-158">sPort</span></span> |<span data-ttu-id="516c1-159">Hello 서버 hello 클라이언트에 연결 된 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-159">Port on hello server hello client connected to.</span></span> |
| <span data-ttu-id="516c1-160">sSiteName</span><span class="sxs-lookup"><span data-stu-id="516c1-160">sSiteName</span></span> |<span data-ttu-id="516c1-161">Hello IIS 사이트의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-161">Name of hello IIS site.</span></span> |
| <span data-ttu-id="516c1-162">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="516c1-162">TimeGenerated</span></span> |<span data-ttu-id="516c1-163">날짜 및 시간 hello 항목 기록 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-163">Date and time hello entry was logged.</span></span> |
| <span data-ttu-id="516c1-164">TimeTaken</span><span class="sxs-lookup"><span data-stu-id="516c1-164">TimeTaken</span></span> |<span data-ttu-id="516c1-165">시간 tooprocess hello의 길이 (밀리초)에 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-165">Length of time tooprocess hello request in milliseconds.</span></span> |

## <a name="log-searches-with-iis-logs"></a><span data-ttu-id="516c1-166">IIS 로그로 로그 검색</span><span class="sxs-lookup"><span data-stu-id="516c1-166">Log searches with IIS logs</span></span>
<span data-ttu-id="516c1-167">hello 다음 표에서 다른 로그 있는 쿼리 예의 IIS 로그 레코드를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-167">hello following table provides different examples of log queries that retrieve IIS log records.</span></span>

| <span data-ttu-id="516c1-168">쿼리</span><span class="sxs-lookup"><span data-stu-id="516c1-168">Query</span></span> | <span data-ttu-id="516c1-169">설명</span><span class="sxs-lookup"><span data-stu-id="516c1-169">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="516c1-170">Type=W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="516c1-170">Type=W3CIISLog</span></span> |<span data-ttu-id="516c1-171">모든 IIS 로그 레코드</span><span class="sxs-lookup"><span data-stu-id="516c1-171">All IIS log records.</span></span> |
| <span data-ttu-id="516c1-172">Type=W3CIISLog scStatus=500</span><span class="sxs-lookup"><span data-stu-id="516c1-172">Type=W3CIISLog scStatus=500</span></span> |<span data-ttu-id="516c1-173">반환 상태가 500인 모든 IIS 로그 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-173">All IIS log records with a return status of 500.</span></span> |
| <span data-ttu-id="516c1-174">Type=W3CIISLog &#124; Measure count() by cIP</span><span class="sxs-lookup"><span data-stu-id="516c1-174">Type=W3CIISLog &#124; Measure count() by cIP</span></span> |<span data-ttu-id="516c1-175">클라이언트 IP 주소별 IIS 로그 항목 수</span><span class="sxs-lookup"><span data-stu-id="516c1-175">Count of IIS log entries by client IP address.</span></span> |
| <span data-ttu-id="516c1-176">Type=W3CIISLog csHost="www.contoso.com" &#124; Measure count() by csUriStem</span><span class="sxs-lookup"><span data-stu-id="516c1-176">Type=W3CIISLog csHost="www.contoso.com" &#124; Measure count() by csUriStem</span></span> |<span data-ttu-id="516c1-177">Count의 IIS 로그 hello 호스트 www.contoso.com에 대 한 url 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-177">Count of IIS log entries by URL for hello host www.contoso.com.</span></span> |
| <span data-ttu-id="516c1-178">Type=W3CIISLog &#124; Measure Sum(csBytes) by Computer &#124; top 500000</span><span class="sxs-lookup"><span data-stu-id="516c1-178">Type=W3CIISLog &#124; Measure Sum(csBytes) by Computer &#124; top 500000</span></span> |<span data-ttu-id="516c1-179">각 IIS 컴퓨터에서 받은 총 바이트 수</span><span class="sxs-lookup"><span data-stu-id="516c1-179">Total bytes received by each IIS computer.</span></span> |

>[!NOTE]
> <span data-ttu-id="516c1-180">작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 쿼리 위에 hello toohello 다음 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-180">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above queries would change toohello following.</span></span>

> | <span data-ttu-id="516c1-181">쿼리</span><span class="sxs-lookup"><span data-stu-id="516c1-181">Query</span></span> | <span data-ttu-id="516c1-182">설명</span><span class="sxs-lookup"><span data-stu-id="516c1-182">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="516c1-183">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="516c1-183">W3CIISLog</span></span> |<span data-ttu-id="516c1-184">모든 IIS 로그 레코드</span><span class="sxs-lookup"><span data-stu-id="516c1-184">All IIS log records.</span></span> |
| <span data-ttu-id="516c1-185">W3CIISLog &#124; where scStatus==500</span><span class="sxs-lookup"><span data-stu-id="516c1-185">W3CIISLog &#124; where scStatus==500</span></span> |<span data-ttu-id="516c1-186">반환 상태가 500인 모든 IIS 로그 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-186">All IIS log records with a return status of 500.</span></span> |
| <span data-ttu-id="516c1-187">W3CIISLog &#124; summarize count() by cIP</span><span class="sxs-lookup"><span data-stu-id="516c1-187">W3CIISLog &#124; summarize count() by cIP</span></span> |<span data-ttu-id="516c1-188">클라이언트 IP 주소별 IIS 로그 항목 수</span><span class="sxs-lookup"><span data-stu-id="516c1-188">Count of IIS log entries by client IP address.</span></span> |
| <span data-ttu-id="516c1-189">W3CIISLog &#124; where csHost=="www.contoso.com" &#124; summarize count() by csUriStem</span><span class="sxs-lookup"><span data-stu-id="516c1-189">W3CIISLog &#124; where csHost=="www.contoso.com" &#124; summarize count() by csUriStem</span></span> |<span data-ttu-id="516c1-190">Count의 IIS 로그 hello 호스트 www.contoso.com에 대 한 url 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-190">Count of IIS log entries by URL for hello host www.contoso.com.</span></span> |
| <span data-ttu-id="516c1-191">W3CIISLog &#124; summarize sum(csBytes) by Computer &#124; take 500000</span><span class="sxs-lookup"><span data-stu-id="516c1-191">W3CIISLog &#124; summarize sum(csBytes) by Computer &#124; take 500000</span></span> |<span data-ttu-id="516c1-192">각 IIS 컴퓨터에서 받은 총 바이트 수</span><span class="sxs-lookup"><span data-stu-id="516c1-192">Total bytes received by each IIS computer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="516c1-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="516c1-193">Next steps</span></span>
* <span data-ttu-id="516c1-194">로그 분석 toocollect 다른 구성 [데이터 원본](log-analytics-data-sources.md) 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-194">Configure Log Analytics toocollect other [data sources](log-analytics-data-sources.md) for analysis.</span></span>
* <span data-ttu-id="516c1-195">에 대 한 자세한 내용은 [검색 로그](log-analytics-log-searches.md) tooanalyze hello 데이터가 데이터 원본 및 솔루션에서 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-195">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span>
* <span data-ttu-id="516c1-196">로그 분석 tooproactively 알려 IIS 로그에서 발견 되는 중요 한 조건을에서 경고를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="516c1-196">Configure alerts in Log Analytics tooproactively notify you of important conditions found in IIS logs.</span></span>
