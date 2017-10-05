---
title: "OMS Log Analytics에서 Windows 이벤트 로그 수집 및 분석 | Microsoft Docs"
description: "Windows 이벤트 로그는 Log Analytics에서 사용되는 가장 일반적인 데이터 원본 중 하나입니다.  이 문서에서는 Windows 이벤트 로그 수집을 구성하는 방법을 설명하고, OMS 리포지토리에 생성되는 레코드에 대한 자세한 정보를 제공합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: ee52f564-995b-450f-a6ba-0d7b1dac3f32
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/15/2017
ms.author: bwren
ms.openlocfilehash: 1be8500ec2cb78ef0edf57f4d8561336cf00ebcb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="windows-event-log-data-sources-in-log-analytics"></a><span data-ttu-id="3e205-104">Log Analytics의 Windows 이벤트 로그 데이터 원본</span><span class="sxs-lookup"><span data-stu-id="3e205-104">Windows event log data sources in Log Analytics</span></span>
<span data-ttu-id="3e205-105">많은 응용 프로그램이 Windows 이벤트 로그에 기록되기 때문에 Windows 이벤트 로그는 Windows 에이전트를 사용하여 데이터를 수집하는 가장 일반적인 [데이터 원본](log-analytics-data-sources.md) 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-105">Windows Event logs are one of the most common [data sources](log-analytics-data-sources.md) for collecting data using Windows agents since many applications write to the Windows event log.</span></span>  <span data-ttu-id="3e205-106">모니터링해야 하는 응용 프로그램에서 만든 모든 사용자 지정 로그를 지정하는 것 외에 시스템 및 응용 프로그램 같은 표준 로그에서 이벤트를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-106">You can collect events from standard logs such as System and Application in addition to specifying any custom logs created by applications you need to monitor.</span></span>

![Windows 이벤트](media/log-analytics-data-sources-windows-events/overview.png)     

## <a name="configuring-windows-event-logs"></a><span data-ttu-id="3e205-108">Windows 이벤트 로그 수집</span><span class="sxs-lookup"><span data-stu-id="3e205-108">Configuring Windows Event logs</span></span>
<span data-ttu-id="3e205-109">[Log Analytics 설정의 데이터 메뉴](log-analytics-data-sources.md#configuring-data-sources)에서 Windows 이벤트 로그를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-109">Configure Windows Event logs from the [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>

<span data-ttu-id="3e205-110">Log Analytics에서는 설정에 지정된 Windows 이벤트 로그에서만 이벤트를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-110">Log Analytics only collects events from the Windows event logs that are specified in the settings.</span></span>  <span data-ttu-id="3e205-111">로그 이름을 입력하고 **+**를 클릭하여 이벤트 로그를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-111">You can add an event log by typing in the name of the log and clicking **+**.</span></span>  <span data-ttu-id="3e205-112">각 로그의 경우 선택한 심각도의 이벤트만 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-112">For each log, only the events with the selected severities are collected.</span></span>  <span data-ttu-id="3e205-113">수집하려는 특정 로그에 대한 심각도를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-113">Check the severities for the particular log that you want to collect.</span></span>  <span data-ttu-id="3e205-114">이벤트를 필터링할 추가 조건을 제공할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-114">You cannot provide any additional criteria to filter events.</span></span>

<span data-ttu-id="3e205-115">이벤트 로그 이름을 입력하면 Log Analytics는 일반적인 이벤트 로그 이름을 제안합니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-115">As you type the name of an event log, Log Analytics provides suggestions of common event log names.</span></span> <span data-ttu-id="3e205-116">추가하려는 로그가 목록에 나타나지 않으면 로그의 전체 이름을 입력하여 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-116">If the log you want to add does not appear in the list, you can still add it by typing in the full name of the log.</span></span> <span data-ttu-id="3e205-117">이벤트 뷰어를 사용하여 로그의 전체 이름을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-117">You can find the full name of the log by using event viewer.</span></span> <span data-ttu-id="3e205-118">이벤트 뷰어에서 로그의 *속성*을 열고 *전체 이름* 필드에서 문자열을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-118">In event viewer, open the *Properties* page for the log and copy the string from the *Full Name* field.</span></span>

![Windows 이벤트 구성](media/log-analytics-data-sources-windows-events/configure.png)

## <a name="data-collection"></a><span data-ttu-id="3e205-120">데이터 수집</span><span class="sxs-lookup"><span data-stu-id="3e205-120">Data collection</span></span>
<span data-ttu-id="3e205-121">Log Analytics에서는 이벤트가 생성될 때 모니터링되는 이벤트 로그에서 선택한 심각도와 일치하는 각 이벤트를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-121">Log Analytics collects each event that matches a selected severity from a monitored event log as the event is created.</span></span>  <span data-ttu-id="3e205-122">에이전트는 수집하는 각 이벤트 로그에 해당 위치를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-122">The agent records its place in each event log that it collects from.</span></span>  <span data-ttu-id="3e205-123">에이전트가 일정 기간 동안 오프라인 상태로 전환된 경우 Log Analytics는 마지막으로 오프라인 상태가 유지된 위치에서 이벤트를 수집하며, 이는 에이전트가 오프라인 상태에 있는 동안 해당 이벤트가 생성된 경우에도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-123">If the agent goes offline for a period of time, then Log Analytics collects events from where it last left off, even if those events were created while the agent was offline.</span></span>  <span data-ttu-id="3e205-124">에이전트가 오프라인 상태인 동안 이벤트 로그가 수집되지 않은 이벤트로 래핑하여 덮어쓰여지면 이벤트가 수집되지 않을 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-124">There is a potential for these events to not be collected if the event log wraps with uncollected events being overwritten while the agent is offline.</span></span>

>[!NOTE]
><span data-ttu-id="3e205-125">Log Analytics는 키워드 *클래식* 또는 *감사 성공* 및 키워드 *0xa0000000000000*을 포함하는 이벤트 ID 18453과 함께 원본 *MSSQLSERVER*의 SQL Server에서 생성되는 감사 이벤트를 수집하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-125">Log Analytics does not collect audit events created by SQL Server from source *MSSQLSERVER* with event ID 18453 that contains keywords - *Classic* or *Audit Success* and keyword *0xa0000000000000*.</span></span>
>

## <a name="windows-event-records-properties"></a><span data-ttu-id="3e205-126">Windows 이벤트 레코드 속성</span><span class="sxs-lookup"><span data-stu-id="3e205-126">Windows event records properties</span></span>
<span data-ttu-id="3e205-127">Windows 이벤트 레코드는 **이벤트** 형식이며, 다음 테이블에 있는 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-127">Windows event records have a type of **Event** and have the properties in the following table:</span></span>

| <span data-ttu-id="3e205-128">속성</span><span class="sxs-lookup"><span data-stu-id="3e205-128">Property</span></span> | <span data-ttu-id="3e205-129">설명</span><span class="sxs-lookup"><span data-stu-id="3e205-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3e205-130">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="3e205-130">Computer</span></span> |<span data-ttu-id="3e205-131">이벤트가 수집된 컴퓨터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-131">Name of the computer that the event was collected from.</span></span> |
| <span data-ttu-id="3e205-132">EventCategory</span><span class="sxs-lookup"><span data-stu-id="3e205-132">EventCategory</span></span> |<span data-ttu-id="3e205-133">이벤트의 범주.</span><span class="sxs-lookup"><span data-stu-id="3e205-133">Category of the event.</span></span> |
| <span data-ttu-id="3e205-134">EventData</span><span class="sxs-lookup"><span data-stu-id="3e205-134">EventData</span></span> |<span data-ttu-id="3e205-135">원시 형식의 모든 이벤트 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-135">All event data in raw format.</span></span> |
| <span data-ttu-id="3e205-136">EventID</span><span class="sxs-lookup"><span data-stu-id="3e205-136">EventID</span></span> |<span data-ttu-id="3e205-137">이벤트의 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-137">Number of the event.</span></span> |
| <span data-ttu-id="3e205-138">EventLevel</span><span class="sxs-lookup"><span data-stu-id="3e205-138">EventLevel</span></span> |<span data-ttu-id="3e205-139">숫자 형식으로 된 이벤트의 심각도입니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-139">Severity of the event in numeric form.</span></span> |
| <span data-ttu-id="3e205-140">EventLevelName</span><span class="sxs-lookup"><span data-stu-id="3e205-140">EventLevelName</span></span> |<span data-ttu-id="3e205-141">텍스트 형식으로 된 이벤트의 심각도입니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-141">Severity of the event in text form.</span></span> |
| <span data-ttu-id="3e205-142">EventLog</span><span class="sxs-lookup"><span data-stu-id="3e205-142">EventLog</span></span> |<span data-ttu-id="3e205-143">이벤트가 수집된 이벤트 로그의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-143">Name of the event log that the event was collected from.</span></span> |
| <span data-ttu-id="3e205-144">ParameterXml</span><span class="sxs-lookup"><span data-stu-id="3e205-144">ParameterXml</span></span> |<span data-ttu-id="3e205-145">XML 형식의 이벤트 매개 변수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-145">Event parameter values in XML format.</span></span> |
| <span data-ttu-id="3e205-146">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="3e205-146">ManagementGroupName</span></span> |<span data-ttu-id="3e205-147">System Center Operations Manager 에이전트의 관리 그룹 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-147">Name of the management group for System Center Operations Manager agents.</span></span>  <span data-ttu-id="3e205-148">다른 에이전트의 경우 이 값은 AOI-<workspace ID>입니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-148">For other agents, this value is AOI-<workspace ID></span></span> |
| <span data-ttu-id="3e205-149">RenderedDescription</span><span class="sxs-lookup"><span data-stu-id="3e205-149">RenderedDescription</span></span> |<span data-ttu-id="3e205-150">매개 변수 값을 포함하는 이벤트 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-150">Event description with parameter values</span></span> |
| <span data-ttu-id="3e205-151">원본</span><span class="sxs-lookup"><span data-stu-id="3e205-151">Source</span></span> |<span data-ttu-id="3e205-152">이벤트의 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-152">Source of the event.</span></span> |
| <span data-ttu-id="3e205-153">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="3e205-153">SourceSystem</span></span> |<span data-ttu-id="3e205-154">이벤트가 수집된 에이전트의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-154">Type of agent the event was collected from.</span></span> <br> <span data-ttu-id="3e205-155">OpsManager – Windows 에이전트, 직접 연결 또는 관리된 Operations Manager</span><span class="sxs-lookup"><span data-stu-id="3e205-155">OpsManager – Windows agent, either direct connect or Operations Manager managed</span></span> <br> <span data-ttu-id="3e205-156">Linux – 모든 Linux 에이전트</span><span class="sxs-lookup"><span data-stu-id="3e205-156">Linux – All Linux agents</span></span>  <br> <span data-ttu-id="3e205-157">AzureStorage – Azure 진단</span><span class="sxs-lookup"><span data-stu-id="3e205-157">AzureStorage – Azure Diagnostics</span></span> |
| <span data-ttu-id="3e205-158">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="3e205-158">TimeGenerated</span></span> |<span data-ttu-id="3e205-159">Windows에서 이벤트가 만들어진 날짜 및 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-159">Date and time the event was created in Windows.</span></span> |
| <span data-ttu-id="3e205-160">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="3e205-160">UserName</span></span> |<span data-ttu-id="3e205-161">이벤트를 로깅한 계정의 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-161">User name of the account that logged the event.</span></span> |

## <a name="log-searches-with-windows-events"></a><span data-ttu-id="3e205-162">Windows 이벤트 로그로 로그 검색</span><span class="sxs-lookup"><span data-stu-id="3e205-162">Log searches with Windows Events</span></span>
<span data-ttu-id="3e205-163">다음 표에서는 Windows 이벤트 레코드를 검색하는 로그 검색의 다양한 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-163">The following table provides different examples of log searches that retrieve Windows Event records.</span></span>

| <span data-ttu-id="3e205-164">쿼리</span><span class="sxs-lookup"><span data-stu-id="3e205-164">Query</span></span> | <span data-ttu-id="3e205-165">설명</span><span class="sxs-lookup"><span data-stu-id="3e205-165">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3e205-166">Type=Event</span><span class="sxs-lookup"><span data-stu-id="3e205-166">Type=Event</span></span> |<span data-ttu-id="3e205-167">모든 Windows 이벤트</span><span class="sxs-lookup"><span data-stu-id="3e205-167">All Windows events.</span></span> |
| <span data-ttu-id="3e205-168">Type=Event EventLevelName=error</span><span class="sxs-lookup"><span data-stu-id="3e205-168">Type=Event EventLevelName=error</span></span> |<span data-ttu-id="3e205-169">심각도가 오류인 모든 Windows 이벤트</span><span class="sxs-lookup"><span data-stu-id="3e205-169">All Windows events with severity of error.</span></span> |
| <span data-ttu-id="3e205-170">Type=Event &#124; Measure count() by Source</span><span class="sxs-lookup"><span data-stu-id="3e205-170">Type=Event &#124; Measure count() by Source</span></span> |<span data-ttu-id="3e205-171">원본별 Windows 이벤트 수</span><span class="sxs-lookup"><span data-stu-id="3e205-171">Count of Windows events by source.</span></span> |
| <span data-ttu-id="3e205-172">Type=Event EventLevelName=error &#124; Measure count() by Source</span><span class="sxs-lookup"><span data-stu-id="3e205-172">Type=Event EventLevelName=error &#124; Measure count() by Source</span></span> |<span data-ttu-id="3e205-173">원본별 Windows 오류 이벤트 수</span><span class="sxs-lookup"><span data-stu-id="3e205-173">Count of Windows error events by source.</span></span> |


>[!NOTE]
> <span data-ttu-id="3e205-174">작업 영역을 [새 Log Analytics 쿼리 언어](log-analytics-log-search-upgrade.md)로 업그레이드한 경우에는 위의 쿼리가 다음과 같이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-174">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above queries would change to the following.</span></span>
>
>| <span data-ttu-id="3e205-175">쿼리</span><span class="sxs-lookup"><span data-stu-id="3e205-175">Query</span></span> | <span data-ttu-id="3e205-176">설명</span><span class="sxs-lookup"><span data-stu-id="3e205-176">Description</span></span> |
|:---|:---|
| <span data-ttu-id="3e205-177">이벤트</span><span class="sxs-lookup"><span data-stu-id="3e205-177">Event</span></span> |<span data-ttu-id="3e205-178">모든 Windows 이벤트</span><span class="sxs-lookup"><span data-stu-id="3e205-178">All Windows events.</span></span> |
| <span data-ttu-id="3e205-179">Event &#124; where EventLevelName == "error"</span><span class="sxs-lookup"><span data-stu-id="3e205-179">Event &#124; where EventLevelName == "error"</span></span> |<span data-ttu-id="3e205-180">심각도가 오류인 모든 Windows 이벤트</span><span class="sxs-lookup"><span data-stu-id="3e205-180">All Windows events with severity of error.</span></span> |
| <span data-ttu-id="3e205-181">Event &#124; summarize count() by Source</span><span class="sxs-lookup"><span data-stu-id="3e205-181">Event &#124; summarize count() by Source</span></span> |<span data-ttu-id="3e205-182">원본별 Windows 이벤트 수</span><span class="sxs-lookup"><span data-stu-id="3e205-182">Count of Windows events by source.</span></span> |
| <span data-ttu-id="3e205-183">Event &#124; where EventLevelName == "error" &#124; summarize count() by Source</span><span class="sxs-lookup"><span data-stu-id="3e205-183">Event &#124; where EventLevelName == "error" &#124; summarize count() by Source</span></span> |<span data-ttu-id="3e205-184">원본별 Windows 오류 이벤트 수</span><span class="sxs-lookup"><span data-stu-id="3e205-184">Count of Windows error events by source.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="3e205-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3e205-185">Next steps</span></span>
* <span data-ttu-id="3e205-186">분석을 위해 다른 [데이터 원본](log-analytics-data-sources.md) 을 수집하도록 Log Analytics를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-186">Configure Log Analytics to collect other [data sources](log-analytics-data-sources.md) for analysis.</span></span>
* <span data-ttu-id="3e205-187">데이터 원본 및 솔루션에서 수집한 데이터를 분석하기 위해 [로그 검색](log-analytics-log-searches.md) 에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-187">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span>  
* <span data-ttu-id="3e205-188">[사용자 지정 필드](log-analytics-custom-fields.md)를 사용하여 이벤트 레코드를 개별 필드로 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-188">Use [Custom Fields](log-analytics-custom-fields.md) to parse the event records into individual fields.</span></span>
* <span data-ttu-id="3e205-189">Windows 에이전트에서 [성능 카운터 수집](log-analytics-data-sources-performance-counters.md)을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3e205-189">Configure [collection of performance counters](log-analytics-data-sources-performance-counters.md) from your Windows agents.</span></span>
