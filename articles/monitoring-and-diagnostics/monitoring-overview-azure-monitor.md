---
title: "Azure Monitor 개요 | Microsoft Docs"
description: "Azure Monitor는 경고, webhook, 자동 크기 조정 및 자동화를 사용하기 위해 통계를 수집합니다. 또한 문서에서는 다른 Microsoft 모니터링 옵션을 나열합니다."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: robb
ms.openlocfilehash: 619a004b9aff99be68988e1f7be3ccad400a8a0e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="overview-of-azure-monitor"></a><span data-ttu-id="9f373-104">Azure Monitor 개요</span><span class="sxs-lookup"><span data-stu-id="9f373-104">Overview of Azure Monitor</span></span>
<span data-ttu-id="9f373-105">이 문서에서는 Microsoft Azure의 Azure Monitor 서비스에 대해 간략히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-105">This article provides an overview of the Azure Monitor service in Microsoft Azure.</span></span> <span data-ttu-id="9f373-106">Azure Monitor 기능에 대해 설명하고 Azure Monitor를 사용하는 방법에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-106">It discusses what Azure Monitor does and provides pointers to additional information on how to use Azure Monitor.</span></span>  <span data-ttu-id="9f373-107">소개하는 비디오를 사용하려면 이 문서의 아래쪽에 있는 다음 단계 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f373-107">If you prefer a video introduction, see Next steps links at the bottom of this article.</span></span> 

## <a name="why-monitor-your-application-or-system"></a><span data-ttu-id="9f373-108">응용 프로그램 또는 시스템을 모니터링해야 하는 이유</span><span class="sxs-lookup"><span data-stu-id="9f373-108">Why monitor your application or system</span></span>
<span data-ttu-id="9f373-109">클라우드 응용 프로그램은 이동하는 부분이 많아 복잡합니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-109">Cloud applications are complex with many moving parts.</span></span> <span data-ttu-id="9f373-110">모니터링은 응용 프로그램을 유지하고 정상 상태에서 실행할 수 있는 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-110">Monitoring provides data to ensure that your application stays up and running in a healthy state.</span></span> <span data-ttu-id="9f373-111">또한 잠재적 문제를 방지하거나 지난 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-111">It also helps you to stave off potential problems or troubleshoot past ones.</span></span> <span data-ttu-id="9f373-112">또한 응용 프로그램에 대해 깊이 이해하는 데 모니터링 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-112">In addition, you can use monitoring data to gain deep insights about your application.</span></span> <span data-ttu-id="9f373-113">이러한 정보를 통해 응용 프로그램 성능이나 유지 관리를 개선하거나 그렇지 않으면 수동 개입이 필요한 작업을 자동화하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-113">That knowledge can help you to improve application performance or maintainability, or automate actions that would otherwise require manual intervention.</span></span>


## <a name="azure-monitor-and-microsofts-other-monitoring-products"></a><span data-ttu-id="9f373-114">Azure Monitor 및 다른 Microsoft 모니터링 제품</span><span class="sxs-lookup"><span data-stu-id="9f373-114">Azure Monitor and Microsoft's other monitoring products</span></span>
<span data-ttu-id="9f373-115">Azure Monitor는 대부분의 Microsoft Azure 서비스에 대한 기본 수준의 인프라 메트릭과 로그를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-115">Azure Monitor provides base level infrastructure metrics and logs for most services in Microsoft Azure.</span></span> <span data-ttu-id="9f373-116">아직도 Azure Monitor에 데이터를 삽입하지 않는 Azure 서비스는 나중에 삽입할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-116">Azure services that do not yet put their data into Azure Monitor will put it there in the future.</span></span>

<span data-ttu-id="9f373-117">Microsoft는 온-프레미스 설치도 사용하는 개발자, DevOps 또는 IT 작업에 추가 모니터링 기능을 제공하는 추가 제품과 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-117">Microsoft ships additional products and services that provide additional monitoring capabilities for developers, DevOps, or IT Ops that also have on-premises installations.</span></span> <span data-ttu-id="9f373-118">이와 같이 다양한 제품과 서비스가 작동하는 방법에 대한 개요와 이해는 [Microsoft Azure 모니터링](monitoring-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f373-118">For an overview and understanding of how these different products and services work together, see [Monitoring in Microsoft Azure](monitoring-overview.md).</span></span>

## <a name="monitoring-sources---compute"></a><span data-ttu-id="9f373-119">모니터링 소스 - Compute</span><span class="sxs-lookup"><span data-stu-id="9f373-119">Monitoring Sources - Compute</span></span>

![비 계산 리소스의 모니터링 및 진단을 위한 모델](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-compute_v6.png)

<span data-ttu-id="9f373-121">Compute 서비스에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-121">The Compute services include</span></span> 
- <span data-ttu-id="9f373-122">클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="9f373-122">Cloud Services</span></span> 
- <span data-ttu-id="9f373-123">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="9f373-123">Virtual Machines</span></span> 
- <span data-ttu-id="9f373-124">가상 컴퓨터 확장 집합</span><span class="sxs-lookup"><span data-stu-id="9f373-124">Virtual Machine scale sets</span></span> 
- <span data-ttu-id="9f373-125">서비스 패브릭</span><span class="sxs-lookup"><span data-stu-id="9f373-125">Service Fabric</span></span>

### <a name="application---diagnostics-logs-application-logs-and-metrics"></a><span data-ttu-id="9f373-126">응용 프로그램 - 진단 로그, 응용 프로그램 로그 및 메트릭</span><span class="sxs-lookup"><span data-stu-id="9f373-126">Application - Diagnostics Logs, Application Logs, and Metrics</span></span>
<span data-ttu-id="9f373-127">응용 프로그램은 계산 모델의 게스트 OS에서 실행될 수 있으며,</span><span class="sxs-lookup"><span data-stu-id="9f373-127">Applications can run on top of the Guest OS in the compute model.</span></span> <span data-ttu-id="9f373-128">고유한 로그 및 메트릭 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-128">They emit their own set of logs and metrics.</span></span> <span data-ttu-id="9f373-129">Azure Monitor는 Azure 진단 확장(Windows 또는 Linux)을 사용하여 대부분의 응용 프로그램 수준 메트릭과 로그를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-129">Azure Monitor relies on the Azure diagnostics extension (Windows or Linux) to collect most application level metrics and logs.</span></span> <span data-ttu-id="9f373-130">유형에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-130">The types include</span></span>

* <span data-ttu-id="9f373-131">성능 카운터</span><span class="sxs-lookup"><span data-stu-id="9f373-131">Performance counters</span></span>
* <span data-ttu-id="9f373-132">응용 프로그램 로그</span><span class="sxs-lookup"><span data-stu-id="9f373-132">Application Logs</span></span>
* <span data-ttu-id="9f373-133">Windows 이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="9f373-133">Windows Event Logs</span></span>
* <span data-ttu-id="9f373-134">.NET 이벤트 원본</span><span class="sxs-lookup"><span data-stu-id="9f373-134">.NET Event Source</span></span>
* <span data-ttu-id="9f373-135">IIS 로그</span><span class="sxs-lookup"><span data-stu-id="9f373-135">IIS Logs</span></span>
* <span data-ttu-id="9f373-136">매니페스트 기반 ETW</span><span class="sxs-lookup"><span data-stu-id="9f373-136">Manifest based ETW</span></span>
* <span data-ttu-id="9f373-137">크래시 덤프</span><span class="sxs-lookup"><span data-stu-id="9f373-137">Crash Dumps</span></span>
* <span data-ttu-id="9f373-138">고객 오류 로그</span><span class="sxs-lookup"><span data-stu-id="9f373-138">Customer Error Logs</span></span>

<span data-ttu-id="9f373-139">진단 확장이 없으면 CPU 사용량과 같은 몇 가지 메트릭만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-139">Without the diagnostics extension, only a few metrics like CPU usage are available.</span></span> 

### <a name="host-and-guest-vm-metrics"></a><span data-ttu-id="9f373-140">호스트 및 게스트 VM 메트릭</span><span class="sxs-lookup"><span data-stu-id="9f373-140">Host and Guest VM metrics</span></span>
<span data-ttu-id="9f373-141">앞에 나열된 계산 리소스에는 상호 작용하는 전용 호스트 VM과 게스트 OS가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-141">The previously listed compute resources have a dedicated host VM and guest OS they interact with.</span></span> <span data-ttu-id="9f373-142">호스트 VM 및 게스트 OS는 Hyper-V 하이퍼바이저 모델에서 루트 VM 및 게스트 VM과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-142">The host VM and guest OS are the equivalent of root VM and guest VM in the Hyper-V hypervisor model.</span></span> <span data-ttu-id="9f373-143">둘 다에서 메트릭을 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-143">You can collect metrics on both.</span></span> <span data-ttu-id="9f373-144">또한 게스트 OS에서 진단 로그도 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-144">You can also collect diagnostics logs on the guest OS.</span></span>   

### <a name="activity-log"></a><span data-ttu-id="9f373-145">활동 로그</span><span class="sxs-lookup"><span data-stu-id="9f373-145">Activity Log</span></span>
<span data-ttu-id="9f373-146">Azure 인프라에 표시되는 대로 리소스에 대한 자세한 내용은 활동 로그(이전에 작업 또는 감사 로그라고도 함)를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-146">You can search the Activity Log (previously called Operational or Audit Logs) for information about your resource as seen by the Azure infrastructure.</span></span> <span data-ttu-id="9f373-147">이러한 로그는 리소스가 생성되거나 소멸된 시간과 같은 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-147">The log contains information such as times when resources are created or destroyed.</span></span>  <span data-ttu-id="9f373-148">자세한 내용은 [활동 로그 개요](monitoring-overview-activity-logs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f373-148">For more information, see [Overview of Activity Log](monitoring-overview-activity-logs.md).</span></span> 

## <a name="monitoring-sources---everything-else"></a><span data-ttu-id="9f373-149">모니터링 소스 - 기타 등등</span><span class="sxs-lookup"><span data-stu-id="9f373-149">Monitoring Sources - everything else</span></span>

![계산 리소스의 모니터링 및 진단을 위한 모델](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-non-compute_v6.png)


### <a name="resource---metrics-and-diagnostics-logs"></a><span data-ttu-id="9f373-151">리소스 - 메트릭 및 진단 로그</span><span class="sxs-lookup"><span data-stu-id="9f373-151">Resource - Metrics and Diagnostics Logs</span></span>
<span data-ttu-id="9f373-152">수집 가능한 메트릭과 진단 로그는 리소스 종류에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-152">Collectable metrics and diagnostics logs vary based on the resource type.</span></span> <span data-ttu-id="9f373-153">예를 들어 Web Apps는 디스크 IO 및 CPU 사용률에 대한 통계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-153">For example, Web Apps provides statistics on the Disk IO and Percent CPU.</span></span> <span data-ttu-id="9f373-154">이러한 메트릭은 큐 크기 및 메시지 처리량과 같은 메트릭을 대신 제공하는 Service Bus 큐에는 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-154">Those metrics don't exist for a Service Bus queue, which instead provides metrics like queue size and message throughput.</span></span> <span data-ttu-id="9f373-155">각 리소스에 대해 수집 가능한 메트릭 목록은 [지원되는 메트릭](monitoring-supported-metrics.md)에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-155">A list of collectable metrics for each resource is available at [supported metrics](monitoring-supported-metrics.md).</span></span> 

### <a name="host-and-guest-vm-metrics"></a><span data-ttu-id="9f373-156">호스트 및 게스트 VM 메트릭</span><span class="sxs-lookup"><span data-stu-id="9f373-156">Host and Guest VM metrics</span></span>
<span data-ttu-id="9f373-157">리소스와 특정 호스트 VM 또는 게스트 VM 간에는 일대일 매핑이 반드시 필요하지는 않으므로 메트릭을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-157">There is not necessarily a 1:1 mapping between your resource and a particular Host or Guest VM so metrics are not available.</span></span>

### <a name="activity-log"></a><span data-ttu-id="9f373-158">활동 로그</span><span class="sxs-lookup"><span data-stu-id="9f373-158">Activity Log</span></span>
<span data-ttu-id="9f373-159">활동 로그는 계산 리소스와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-159">The activity log is the same as for compute resources.</span></span>  

## <a name="uses-for-monitoring-data"></a><span data-ttu-id="9f373-160">모니터링 데이터 사용</span><span class="sxs-lookup"><span data-stu-id="9f373-160">Uses for Monitoring Data</span></span>
<span data-ttu-id="9f373-161">데이터를 수집하고 나면 Azure Monitor에서 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-161">Once you collect your data, you can do the following with it in Azure Monitor</span></span>

### <a name="route"></a><span data-ttu-id="9f373-162">라우팅</span><span class="sxs-lookup"><span data-stu-id="9f373-162">Route</span></span>
<span data-ttu-id="9f373-163">모니터링 데이터를 다른 위치에 실시간으로 스트리밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-163">You can stream monitoring data to other locations in real time.</span></span>

<span data-ttu-id="9f373-164">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-164">Examples include:</span></span>

- <span data-ttu-id="9f373-165">다양한 시각화 및 분석 도구를 사용할 수 있도록 Application Insights에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-165">Send to Application Insights so you can use its richer visualization and analysis tools.</span></span>
- <span data-ttu-id="9f373-166">타사 도구로 라우팅할 수 있도록 Event Hubs로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-166">Send to Event Hubs so you can route to third-party tools.</span></span> 

### <a name="store-and-archive"></a><span data-ttu-id="9f373-167">저장 및 보관</span><span class="sxs-lookup"><span data-stu-id="9f373-167">Store and Archive</span></span>
<span data-ttu-id="9f373-168">일부 모니터링 데이터는 이미 설정된 시간 동안 Azure Monitor에 저장되어 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-168">Some monitoring data is already stored and available in Azure Monitor for a set amount of time.</span></span> 
- <span data-ttu-id="9f373-169">메트릭은 30일 동안 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-169">Metrics are stored for 30 days.</span></span> 
- <span data-ttu-id="9f373-170">활동 로그 항목은 90일 동안 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-170">Activity log entries are stored for 90 days.</span></span> 
- <span data-ttu-id="9f373-171">진단 로그는 전혀 저장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-171">Diagnostics logs are not stored at all.</span></span> 

<span data-ttu-id="9f373-172">데이터를 위에 나열된 기간보다 더 오래 저장하려면 Azure 저장소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-172">If you want to store data longer than the time periods listed above, you can use an Azure storage.</span></span> <span data-ttu-id="9f373-173">모니터링 데이터는 설정한 보존 정책에 따라 저장소 계정에 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-173">Monitoring data is kept in your storage acccount based on a retention policy you set.</span></span> <span data-ttu-id="9f373-174">Azure 저장소에서 데이터가 차지하는 공간에 대해 비용을 지불해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-174">You do have to pay for the space the data takes up in Azure storage.</span></span> 

<span data-ttu-id="9f373-175">이 데이터를 사용하는 몇 가지 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-175">A few ways to use this data:</span></span>

- <span data-ttu-id="9f373-176">기록된 경우 Azure 내부 또는 외부의 다른 도구를 사용하여 데이터를 읽고 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-176">Once written, you can have other tools within or outside of Azure read it and process it.</span></span>
- <span data-ttu-id="9f373-177">로컬 보관을 위해 데이터를 로컬로 다운로드하거나, 연장된 기간 동안 데이터를 유지하기 위해 클라우드의 보존 정책을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-177">You download the data locally for a local archive or change your retention policy in the cloud to keep data for extended periods of time.</span></span>  
- <span data-ttu-id="9f373-178">보관을 위해 Azure 저장소에 데이터를 무한정 그대로 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-178">You leave the data in Azure storage indefinitely for archive purposes.</span></span> 

### <a name="query"></a><span data-ttu-id="9f373-179">쿼리</span><span class="sxs-lookup"><span data-stu-id="9f373-179">Query</span></span>
<span data-ttu-id="9f373-180">Azure Monitor REST API, 플랫폼 간 CLI(명령줄 인터페이스), PowerShell cmdlet 또는 .NET SDK를 사용하여 시스템 또는 Azure 저장소의 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-180">You can use the Azure Monitor REST API, cross platform Command-Line Interface (CLI) commands, PowerShell cmdlets, or the .NET SDK to access the data in the system or Azure storage</span></span>

<span data-ttu-id="9f373-181">이러한 예로 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-181">Examples include:</span></span>

* <span data-ttu-id="9f373-182">작성한 사용자 지정 모니터링 응용 프로그램에 대한 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="9f373-182">Getting data for a custom monitoring application you have written</span></span>
* <span data-ttu-id="9f373-183">사용자 지정 쿼리를 만들고 이 데이터를 타사 응용 프로그램으로 보내기</span><span class="sxs-lookup"><span data-stu-id="9f373-183">Creating custom queries and sending that data to a third-party application.</span></span>

### <a name="visualize"></a><span data-ttu-id="9f373-184">시각화</span><span class="sxs-lookup"><span data-stu-id="9f373-184">Visualize</span></span>
<span data-ttu-id="9f373-185">모니터링 데이터를 그래픽과 차트로 시각화하면 데이터 자체를 살펴보는 것보다 훨씬 빠르게 추세를 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-185">Visualizing your monitoring data in graphics and charts helps you find trends quicker than looking through the data itself.</span></span>  

<span data-ttu-id="9f373-186">몇 가지 시각화 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-186">A few visualization methods include:</span></span>

* <span data-ttu-id="9f373-187">Azure 포털 사용</span><span class="sxs-lookup"><span data-stu-id="9f373-187">Use the Azure portal</span></span>
* <span data-ttu-id="9f373-188">Azure Application Insights로 데이터 라우팅</span><span class="sxs-lookup"><span data-stu-id="9f373-188">Route data to Azure Application Insights</span></span>
* <span data-ttu-id="9f373-189">Microsoft PowerBI로 데이터 라우팅</span><span class="sxs-lookup"><span data-stu-id="9f373-189">Route data to Microsoft PowerBI</span></span>
* <span data-ttu-id="9f373-190">라이브 스트리밍 또는 Azure 저장소의 보관 파일에서 데이터를 읽는 도구를 사용하여 타사 시각화 도구로 데이터 라우팅</span><span class="sxs-lookup"><span data-stu-id="9f373-190">Route the data to a third-party visualization tool using either live streaming or by having the tool read from an archive in Azure storage</span></span>


### <a name="automate"></a><span data-ttu-id="9f373-191">자동화</span><span class="sxs-lookup"><span data-stu-id="9f373-191">Automate</span></span>
<span data-ttu-id="9f373-192">모니터링 데이터를 사용하여 경고를 트리거하거나 전체 프로세스를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-192">You can use monitoring data to trigger alerts or even whole processes.</span></span> <span data-ttu-id="9f373-193">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-193">Examples include:</span></span>

* <span data-ttu-id="9f373-194">데이터를 사용하여 응용 프로그램 부하에 따라 계산 인스턴스 크기를 자동으로 조정</span><span class="sxs-lookup"><span data-stu-id="9f373-194">Use data to autoscale compute instances up or down based on application load.</span></span>
* <span data-ttu-id="9f373-195">메트릭이 미리 결정된 임계값을 초과하는 경우 전자 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="9f373-195">Send emails when a metric crosses a predetermined threshold.</span></span>
* <span data-ttu-id="9f373-196">웹 URL(웹후크)을 호출하여 Azure 외부 시스템에서 동작 실행</span><span class="sxs-lookup"><span data-stu-id="9f373-196">Call a web URL (webhook) to execute an action in a system outside of Azure</span></span>
* <span data-ttu-id="9f373-197">Azure 자동화에서 runbook을 시작하여 다양한 태스크 수행</span><span class="sxs-lookup"><span data-stu-id="9f373-197">Start a runbook in Azure automation to perform any variety of tasks</span></span>

## <a name="methods-of-accessing-azure-monitor"></a><span data-ttu-id="9f373-198">Azure Monitor에 액세스하는 방법</span><span class="sxs-lookup"><span data-stu-id="9f373-198">Methods of accessing Azure Monitor</span></span>
<span data-ttu-id="9f373-199">일반적으로 다음 방법 중 하나를 사용하여 데이터 추적, 라우팅 및 검색을 조작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-199">In general, you can manipulate data tracking, routing, and retrieval using one of the following methods.</span></span> <span data-ttu-id="9f373-200">일부 방법은 일부 동작 및 데이터 형식에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-200">Not all methods are available for all actions or data types.</span></span>

* [<span data-ttu-id="9f373-201">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="9f373-201">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="9f373-202">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f373-202">PowerShell</span></span>](insights-powershell-samples.md)  
* [<span data-ttu-id="9f373-203">CLI(플랫폼 간 명령줄 인터페이스)</span><span class="sxs-lookup"><span data-stu-id="9f373-203">Cross-platform Command Line Interface (CLI)</span></span>](insights-cli-samples.md)
* [<span data-ttu-id="9f373-204">REST API</span><span class="sxs-lookup"><span data-stu-id="9f373-204">REST API</span></span>](https://docs.microsoft.com/rest/api/monitor/)
* [<span data-ttu-id="9f373-205">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="9f373-205">.NET SDK</span></span>](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor)

## <a name="next-steps"></a><span data-ttu-id="9f373-206">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9f373-206">Next steps</span></span>
<span data-ttu-id="9f373-207">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="9f373-207">Learn more about</span></span>
- <span data-ttu-id="9f373-208">Azure Monitor 비디오 연습은</span><span class="sxs-lookup"><span data-stu-id="9f373-208">A video walkthrough of just Azure Monitor is available at</span></span>  
<span data-ttu-id="9f373-209">[Azure Monitor 시작](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor)에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-209">[Get Started with Azure Monitor](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor).</span></span> <span data-ttu-id="9f373-210">Azure Monitor를 사용할 수 있는 시나리오를 설명하는 추가 비디오는 [Microsoft Azure 모니터링 및 진단 탐색](https://channel9.msdn.com/events/Ignite/2016/BRK2234)(영문) 및 [Azure Monitor(Ignite 2016 비디오)](https://myignite.microsoft.com/videos/4977)(영문)에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-210">An additional video explaining a scenario where you can use Azure Monitor is available at [Explore Microsoft Azure monitoring and diagnostics](https://channel9.msdn.com/events/Ignite/2016/BRK2234) and [Azure Monitor in a video from Ignite 2016](https://myignite.microsoft.com/videos/4977)</span></span>
- <span data-ttu-id="9f373-211">[Azure Monitor 시작](monitoring-get-started.md)에서 Azure Monitor 인터페이스를 통해 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-211">Run through the Azure Monitor interface in [Getting Started with Azure Monitor](monitoring-get-started.md)</span></span>
- <span data-ttu-id="9f373-212">클라우드 서비스, 가상 컴퓨터, 가상 컴퓨터 확장 집합 또는 Service Fabric 응용 프로그램에서 문제를 진단하려는 경우 [Azure 진단 확장](../azure-diagnostics.md)을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9f373-212">Set up the [Azure Diagnostics Extensions](../azure-diagnostics.md) if you are attempting to diagnose problems in your Cloud Service, Virtual Machine, Virtual machine scale sets, or Service Fabric application.</span></span>
- <span data-ttu-id="9f373-213">[Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) - 앱 서비스 웹앱에서 문제를 진단하려는 경우</span><span class="sxs-lookup"><span data-stu-id="9f373-213">[Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) if you are trying to diagnostic problems in your App Service Web app.</span></span>
- <span data-ttu-id="9f373-214">[Azure Storage 문제 해결](../storage/common/storage-e2e-troubleshooting.md) - 저장소 Blob, 테이블 및 큐를 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="9f373-214">[Troubleshooting Azure Storage](../storage/common/storage-e2e-troubleshooting.md) when using Storage Blobs, Tables, or Queues</span></span>
- <span data-ttu-id="9f373-215">[Log Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) 및 [Operations Management Suite](https://www.microsoft.com/oms/)</span><span class="sxs-lookup"><span data-stu-id="9f373-215">[Log Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) and the [Operations Management Suite](https://www.microsoft.com/oms/)</span></span>
