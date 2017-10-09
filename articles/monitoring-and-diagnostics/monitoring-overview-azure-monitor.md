---
title: "aaaAzure 모니터 개요 | Microsoft Docs"
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
ms.openlocfilehash: ffa304e7b158f0fceb7f60ab88fab291976aa0e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-monitor"></a><span data-ttu-id="3eeda-104">Azure Monitor 개요</span><span class="sxs-lookup"><span data-stu-id="3eeda-104">Overview of Azure Monitor</span></span>
<span data-ttu-id="3eeda-105">이 문서에서는 hello Azure 모니터 서비스를 Microsoft Azure에 대 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-105">This article provides an overview of hello Azure Monitor service in Microsoft Azure.</span></span> <span data-ttu-id="3eeda-106">Azure 모니터 않습니다 및 방법에 대해 포인터 tooadditional 설명에 대해 설명 toouse Azure 모니터입니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-106">It discusses what Azure Monitor does and provides pointers tooadditional information on how toouse Azure Monitor.</span></span>  <span data-ttu-id="3eeda-107">한 비디오 소개를 선호 하는 경우이 문서의 hello 맨 아래에 다음 단계 링크를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-107">If you prefer a video introduction, see Next steps links at hello bottom of this article.</span></span> 

## <a name="why-monitor-your-application-or-system"></a><span data-ttu-id="3eeda-108">응용 프로그램 또는 시스템을 모니터링해야 하는 이유</span><span class="sxs-lookup"><span data-stu-id="3eeda-108">Why monitor your application or system</span></span>
<span data-ttu-id="3eeda-109">클라우드 응용 프로그램은 이동하는 부분이 많아 복잡합니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-109">Cloud applications are complex with many moving parts.</span></span> <span data-ttu-id="3eeda-110">모니터링 없이 계속 응용 프로그램 데이터 tooensure 정상 상태에서 실행 되 고 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-110">Monitoring provides data tooensure that your application stays up and running in a healthy state.</span></span> <span data-ttu-id="3eeda-111">또한 있습니다 toostave 잠재적 문제를 해제 하거나 문제를 해결 하십시오. 지난 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-111">It also helps you toostave off potential problems or troubleshoot past ones.</span></span> <span data-ttu-id="3eeda-112">또한 응용 프로그램에 대 한 모니터링 데이터 toogain 깊은 통찰력을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-112">In addition, you can use monitoring data toogain deep insights about your application.</span></span> <span data-ttu-id="3eeda-113">이 정보는 tooimprove 응용 프로그램 성능이 나 유지 관리의 편의성 하는 데 도움이 하거나 수동 개입 해야 하는 작업을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-113">That knowledge can help you tooimprove application performance or maintainability, or automate actions that would otherwise require manual intervention.</span></span>


## <a name="azure-monitor-and-microsofts-other-monitoring-products"></a><span data-ttu-id="3eeda-114">Azure Monitor 및 다른 Microsoft 모니터링 제품</span><span class="sxs-lookup"><span data-stu-id="3eeda-114">Azure Monitor and Microsoft's other monitoring products</span></span>
<span data-ttu-id="3eeda-115">Azure Monitor는 대부분의 Microsoft Azure 서비스에 대한 기본 수준의 인프라 메트릭과 로그를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-115">Azure Monitor provides base level infrastructure metrics and logs for most services in Microsoft Azure.</span></span> <span data-ttu-id="3eeda-116">Azure 서비스를 Azure 모니터도 해당 데이터를 저장 하지 않는 것이 있으면에 넣습니다 hello 이후.</span><span class="sxs-lookup"><span data-stu-id="3eeda-116">Azure services that do not yet put their data into Azure Monitor will put it there in hello future.</span></span>

<span data-ttu-id="3eeda-117">Microsoft는 온-프레미스 설치도 사용하는 개발자, DevOps 또는 IT 작업에 추가 모니터링 기능을 제공하는 추가 제품과 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-117">Microsoft ships additional products and services that provide additional monitoring capabilities for developers, DevOps, or IT Ops that also have on-premises installations.</span></span> <span data-ttu-id="3eeda-118">이와 같이 다양한 제품과 서비스가 작동하는 방법에 대한 개요와 이해는 [Microsoft Azure 모니터링](monitoring-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3eeda-118">For an overview and understanding of how these different products and services work together, see [Monitoring in Microsoft Azure](monitoring-overview.md).</span></span>

## <a name="monitoring-sources---compute"></a><span data-ttu-id="3eeda-119">모니터링 소스 - Compute</span><span class="sxs-lookup"><span data-stu-id="3eeda-119">Monitoring Sources - Compute</span></span>

![비 계산 리소스의 모니터링 및 진단을 위한 모델](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-compute_v6.png)

<span data-ttu-id="3eeda-121">hello 계산 서비스 포함</span><span class="sxs-lookup"><span data-stu-id="3eeda-121">hello Compute services include</span></span> 
- <span data-ttu-id="3eeda-122">클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="3eeda-122">Cloud Services</span></span> 
- <span data-ttu-id="3eeda-123">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="3eeda-123">Virtual Machines</span></span> 
- <span data-ttu-id="3eeda-124">가상 컴퓨터 확장 집합</span><span class="sxs-lookup"><span data-stu-id="3eeda-124">Virtual Machine scale sets</span></span> 
- <span data-ttu-id="3eeda-125">서비스 패브릭</span><span class="sxs-lookup"><span data-stu-id="3eeda-125">Service Fabric</span></span>

### <a name="application---diagnostics-logs-application-logs-and-metrics"></a><span data-ttu-id="3eeda-126">응용 프로그램 - 진단 로그, 응용 프로그램 로그 및 메트릭</span><span class="sxs-lookup"><span data-stu-id="3eeda-126">Application - Diagnostics Logs, Application Logs, and Metrics</span></span>
<span data-ttu-id="3eeda-127">응용 프로그램 hello 계산 모델에 게스트 OS hello를 기반으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-127">Applications can run on top of hello Guest OS in hello compute model.</span></span> <span data-ttu-id="3eeda-128">고유한 로그 및 메트릭 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-128">They emit their own set of logs and metrics.</span></span> <span data-ttu-id="3eeda-129">대부분의 응용 프로그램 수준 메트릭 및 로그 azure 모니터 hello Azure 진단 확장 (Windows 또는 Linux) toocollect에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-129">Azure Monitor relies on hello Azure diagnostics extension (Windows or Linux) toocollect most application level metrics and logs.</span></span> <span data-ttu-id="3eeda-130">hello 유형에</span><span class="sxs-lookup"><span data-stu-id="3eeda-130">hello types include</span></span>

* <span data-ttu-id="3eeda-131">성능 카운터</span><span class="sxs-lookup"><span data-stu-id="3eeda-131">Performance counters</span></span>
* <span data-ttu-id="3eeda-132">응용 프로그램 로그</span><span class="sxs-lookup"><span data-stu-id="3eeda-132">Application Logs</span></span>
* <span data-ttu-id="3eeda-133">Windows 이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="3eeda-133">Windows Event Logs</span></span>
* <span data-ttu-id="3eeda-134">.NET 이벤트 원본</span><span class="sxs-lookup"><span data-stu-id="3eeda-134">.NET Event Source</span></span>
* <span data-ttu-id="3eeda-135">IIS 로그</span><span class="sxs-lookup"><span data-stu-id="3eeda-135">IIS Logs</span></span>
* <span data-ttu-id="3eeda-136">매니페스트 기반 ETW</span><span class="sxs-lookup"><span data-stu-id="3eeda-136">Manifest based ETW</span></span>
* <span data-ttu-id="3eeda-137">크래시 덤프</span><span class="sxs-lookup"><span data-stu-id="3eeda-137">Crash Dumps</span></span>
* <span data-ttu-id="3eeda-138">고객 오류 로그</span><span class="sxs-lookup"><span data-stu-id="3eeda-138">Customer Error Logs</span></span>

<span data-ttu-id="3eeda-139">Hello 진단 확장 없으면 CPU 사용량와 같은 몇 가지 메트릭만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-139">Without hello diagnostics extension, only a few metrics like CPU usage are available.</span></span> 

### <a name="host-and-guest-vm-metrics"></a><span data-ttu-id="3eeda-140">호스트 및 게스트 VM 메트릭</span><span class="sxs-lookup"><span data-stu-id="3eeda-140">Host and Guest VM metrics</span></span>
<span data-ttu-id="3eeda-141">hello 앞에 나열 된 계산 된 리소스 VM 전용된 호스트와 게스트 OS 상호 작용 하는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-141">hello previously listed compute resources have a dedicated host VM and guest OS they interact with.</span></span> <span data-ttu-id="3eeda-142">VM hello 호스트와 게스트 OS는 VM 루트의 hello 서로 동일 하며 hello Hyper-v 하이퍼바이저 모델에서 게스트 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-142">hello host VM and guest OS are hello equivalent of root VM and guest VM in hello Hyper-V hypervisor model.</span></span> <span data-ttu-id="3eeda-143">둘 다에서 메트릭을 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-143">You can collect metrics on both.</span></span> <span data-ttu-id="3eeda-144">Hello 게스트 OS에 진단 로그를 수집할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-144">You can also collect diagnostics logs on hello guest OS.</span></span>   

### <a name="activity-log"></a><span data-ttu-id="3eeda-145">활동 로그</span><span class="sxs-lookup"><span data-stu-id="3eeda-145">Activity Log</span></span>
<span data-ttu-id="3eeda-146">Hello Azure 인프라와 같이 리소스에 대 한 자세한 내용은 hello (이전에 운영 또는 감사 로그 호출) 활동 로그를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-146">You can search hello Activity Log (previously called Operational or Audit Logs) for information about your resource as seen by hello Azure infrastructure.</span></span> <span data-ttu-id="3eeda-147">hello 로그 리소스는 만들거나 제거할 시간 등의 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-147">hello log contains information such as times when resources are created or destroyed.</span></span>  <span data-ttu-id="3eeda-148">자세한 내용은 [활동 로그 개요](monitoring-overview-activity-logs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3eeda-148">For more information, see [Overview of Activity Log](monitoring-overview-activity-logs.md).</span></span> 

## <a name="monitoring-sources---everything-else"></a><span data-ttu-id="3eeda-149">모니터링 소스 - 기타 등등</span><span class="sxs-lookup"><span data-stu-id="3eeda-149">Monitoring Sources - everything else</span></span>

![계산 리소스의 모니터링 및 진단을 위한 모델](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-non-compute_v6.png)


### <a name="resource---metrics-and-diagnostics-logs"></a><span data-ttu-id="3eeda-151">리소스 - 메트릭 및 진단 로그</span><span class="sxs-lookup"><span data-stu-id="3eeda-151">Resource - Metrics and Diagnostics Logs</span></span>
<span data-ttu-id="3eeda-152">수집 가능한 메트릭 및 진단 로그 hello 리소스 종류에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-152">Collectable metrics and diagnostics logs vary based on hello resource type.</span></span> <span data-ttu-id="3eeda-153">예를 들어 웹 응용 프로그램 hello 디스크 IO 및 %CPU 통계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-153">For example, Web Apps provides statistics on hello Disk IO and Percent CPU.</span></span> <span data-ttu-id="3eeda-154">이러한 메트릭은 큐 크기 및 메시지 처리량과 같은 메트릭을 대신 제공하는 Service Bus 큐에는 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-154">Those metrics don't exist for a Service Bus queue, which instead provides metrics like queue size and message throughput.</span></span> <span data-ttu-id="3eeda-155">각 리소스에 대해 수집 가능한 메트릭 목록은 [지원되는 메트릭](monitoring-supported-metrics.md)에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-155">A list of collectable metrics for each resource is available at [supported metrics](monitoring-supported-metrics.md).</span></span> 

### <a name="host-and-guest-vm-metrics"></a><span data-ttu-id="3eeda-156">호스트 및 게스트 VM 메트릭</span><span class="sxs-lookup"><span data-stu-id="3eeda-156">Host and Guest VM metrics</span></span>
<span data-ttu-id="3eeda-157">리소스와 특정 호스트 VM 또는 게스트 VM 간에는 일대일 매핑이 반드시 필요하지는 않으므로 메트릭을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-157">There is not necessarily a 1:1 mapping between your resource and a particular Host or Guest VM so metrics are not available.</span></span>

### <a name="activity-log"></a><span data-ttu-id="3eeda-158">활동 로그</span><span class="sxs-lookup"><span data-stu-id="3eeda-158">Activity Log</span></span>
<span data-ttu-id="3eeda-159">hello 활동 로그 계산 리소스와 같지만 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-159">hello activity log is hello same as for compute resources.</span></span>  

## <a name="uses-for-monitoring-data"></a><span data-ttu-id="3eeda-160">모니터링 데이터 사용</span><span class="sxs-lookup"><span data-stu-id="3eeda-160">Uses for Monitoring Data</span></span>
<span data-ttu-id="3eeda-161">데이터를 수집한 후 할 수 있는 Azure 모니터에서 함께 다음 hello</span><span class="sxs-lookup"><span data-stu-id="3eeda-161">Once you collect your data, you can do hello following with it in Azure Monitor</span></span>

### <a name="route"></a><span data-ttu-id="3eeda-162">라우팅</span><span class="sxs-lookup"><span data-stu-id="3eeda-162">Route</span></span>
<span data-ttu-id="3eeda-163">실시간으로 모니터링 데이터 tooother 위치를 스트리밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-163">You can stream monitoring data tooother locations in real time.</span></span>

<span data-ttu-id="3eeda-164">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-164">Examples include:</span></span>

- <span data-ttu-id="3eeda-165">다양 한 시각화 및 분석 도구를 사용할 수 있도록 tooApplication Insights를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-165">Send tooApplication Insights so you can use its richer visualization and analysis tools.</span></span>
- <span data-ttu-id="3eeda-166">Toothird 타사 도구를 라우팅할 수 있도록 tooEvent 허브를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-166">Send tooEvent Hubs so you can route toothird-party tools.</span></span> 

### <a name="store-and-archive"></a><span data-ttu-id="3eeda-167">저장 및 보관</span><span class="sxs-lookup"><span data-stu-id="3eeda-167">Store and Archive</span></span>
<span data-ttu-id="3eeda-168">일부 모니터링 데이터는 이미 설정된 시간 동안 Azure Monitor에 저장되어 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-168">Some monitoring data is already stored and available in Azure Monitor for a set amount of time.</span></span> 
- <span data-ttu-id="3eeda-169">메트릭은 30일 동안 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-169">Metrics are stored for 30 days.</span></span> 
- <span data-ttu-id="3eeda-170">활동 로그 항목은 90일 동안 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-170">Activity log entries are stored for 90 days.</span></span> 
- <span data-ttu-id="3eeda-171">진단 로그는 전혀 저장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-171">Diagnostics logs are not stored at all.</span></span> 

<span data-ttu-id="3eeda-172">위에 나열 된 기간 동안 hello 보다 길게 toostore 데이터 하려는 경우에 Azure 저장소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-172">If you want toostore data longer than hello time periods listed above, you can use an Azure storage.</span></span> <span data-ttu-id="3eeda-173">모니터링 데이터는 설정한 보존 정책에 따라 저장소 계정에 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-173">Monitoring data is kept in your storage acccount based on a retention policy you set.</span></span> <span data-ttu-id="3eeda-174">사용자에 게 Azure 저장소의 데이터가 차지 하는 hello 공간 hello에 대 한 toopay.</span><span class="sxs-lookup"><span data-stu-id="3eeda-174">You do have toopay for hello space hello data takes up in Azure storage.</span></span> 

<span data-ttu-id="3eeda-175">몇 가지 방법으로 toouse이이 데이터:</span><span class="sxs-lookup"><span data-stu-id="3eeda-175">A few ways toouse this data:</span></span>

- <span data-ttu-id="3eeda-176">기록된 경우 Azure 내부 또는 외부의 다른 도구를 사용하여 데이터를 읽고 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-176">Once written, you can have other tools within or outside of Azure read it and process it.</span></span>
- <span data-ttu-id="3eeda-177">로컬 보관에 대 한 로컬 hello 데이터 다운로드 또는 오랜 시간에 대 한 hello 클라우드 tookeep 데이터에서 보존 정책을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-177">You download hello data locally for a local archive or change your retention policy in hello cloud tookeep data for extended periods of time.</span></span>  
- <span data-ttu-id="3eeda-178">무한정 보관을 위해 Azure 저장소에 hello 데이터를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-178">You leave hello data in Azure storage indefinitely for archive purposes.</span></span> 

### <a name="query"></a><span data-ttu-id="3eeda-179">쿼리</span><span class="sxs-lookup"><span data-stu-id="3eeda-179">Query</span></span>
<span data-ttu-id="3eeda-180">Hello Azure 모니터 REST API, 크로스 플랫폼 명령줄 인터페이스 (CLI) 명령, PowerShell cmdlet을 사용할 수 있습니다 또는 hello.NET SDK tooaccess hello 시스템 또는 Azure 저장소에 데이터를 환영</span><span class="sxs-lookup"><span data-stu-id="3eeda-180">You can use hello Azure Monitor REST API, cross platform Command-Line Interface (CLI) commands, PowerShell cmdlets, or hello .NET SDK tooaccess hello data in hello system or Azure storage</span></span>

<span data-ttu-id="3eeda-181">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-181">Examples include:</span></span>

* <span data-ttu-id="3eeda-182">작성한 사용자 지정 모니터링 응용 프로그램에 대한 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="3eeda-182">Getting data for a custom monitoring application you have written</span></span>
* <span data-ttu-id="3eeda-183">사용자 지정 쿼리를 만들고 해당 데이터 tooa 타사 응용 프로그램 보내는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-183">Creating custom queries and sending that data tooa third-party application.</span></span>

### <a name="visualize"></a><span data-ttu-id="3eeda-184">시각화</span><span class="sxs-lookup"><span data-stu-id="3eeda-184">Visualize</span></span>
<span data-ttu-id="3eeda-185">그래픽 및 차트에 모니터링 데이터를 시각화 하면 추세를 hello 데이터 자체를 통해 보고 보다 더 빠르게 찾을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-185">Visualizing your monitoring data in graphics and charts helps you find trends quicker than looking through hello data itself.</span></span>  

<span data-ttu-id="3eeda-186">몇 가지 시각화 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-186">A few visualization methods include:</span></span>

* <span data-ttu-id="3eeda-187">Hello Azure 포털을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="3eeda-187">Use hello Azure portal</span></span>
* <span data-ttu-id="3eeda-188">경로 데이터 tooAzure Application Insights</span><span class="sxs-lookup"><span data-stu-id="3eeda-188">Route data tooAzure Application Insights</span></span>
* <span data-ttu-id="3eeda-189">경로 데이터 tooMicrosoft PowerBI</span><span class="sxs-lookup"><span data-stu-id="3eeda-189">Route data tooMicrosoft PowerBI</span></span>
* <span data-ttu-id="3eeda-190">라이브 스트리밍 하거나 경로 hello 데이터 tooa 제 3 자 시각화 도구를 사용 하 여 함으로써 hello 도구에서에서 또는 Azure 저장소에 보관</span><span class="sxs-lookup"><span data-stu-id="3eeda-190">Route hello data tooa third-party visualization tool using either live streaming or by having hello tool read from an archive in Azure storage</span></span>


### <a name="automate"></a><span data-ttu-id="3eeda-191">자동화</span><span class="sxs-lookup"><span data-stu-id="3eeda-191">Automate</span></span>
<span data-ttu-id="3eeda-192">모니터링 데이터 tootrigger 경고를 사용 하거나 포함 하 여 전체 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-192">You can use monitoring data tootrigger alerts or even whole processes.</span></span> <span data-ttu-id="3eeda-193">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-193">Examples include:</span></span>

* <span data-ttu-id="3eeda-194">사용 데이터 tooautoscale 계산 인스턴스 위로 또는 아래로 응용 프로그램 부하에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-194">Use data tooautoscale compute instances up or down based on application load.</span></span>
* <span data-ttu-id="3eeda-195">메트릭이 미리 결정된 임계값을 초과하는 경우 전자 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="3eeda-195">Send emails when a metric crosses a predetermined threshold.</span></span>
* <span data-ttu-id="3eeda-196">Azure 외부 시스템의 웹 URL (webhook) tooexecute 동작을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-196">Call a web URL (webhook) tooexecute an action in a system outside of Azure</span></span>
* <span data-ttu-id="3eeda-197">다양 한 작업 tooperform Azure 자동화에서에서 runbook을 시작</span><span class="sxs-lookup"><span data-stu-id="3eeda-197">Start a runbook in Azure automation tooperform any variety of tasks</span></span>

## <a name="methods-of-accessing-azure-monitor"></a><span data-ttu-id="3eeda-198">Azure Monitor에 액세스하는 방법</span><span class="sxs-lookup"><span data-stu-id="3eeda-198">Methods of accessing Azure Monitor</span></span>
<span data-ttu-id="3eeda-199">일반적으로 추적 데이터, 라우팅 및 hello 메서드를 다음 중 하나를 사용 하 여 검색을 조작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-199">In general, you can manipulate data tracking, routing, and retrieval using one of hello following methods.</span></span> <span data-ttu-id="3eeda-200">일부 방법은 일부 동작 및 데이터 형식에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-200">Not all methods are available for all actions or data types.</span></span>

* [<span data-ttu-id="3eeda-201">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="3eeda-201">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="3eeda-202">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3eeda-202">PowerShell</span></span>](insights-powershell-samples.md)  
* [<span data-ttu-id="3eeda-203">CLI(플랫폼 간 명령줄 인터페이스)</span><span class="sxs-lookup"><span data-stu-id="3eeda-203">Cross-platform Command Line Interface (CLI)</span></span>](insights-cli-samples.md)
* [<span data-ttu-id="3eeda-204">REST API</span><span class="sxs-lookup"><span data-stu-id="3eeda-204">REST API</span></span>](https://docs.microsoft.com/rest/api/monitor/)
* [<span data-ttu-id="3eeda-205">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="3eeda-205">.NET SDK</span></span>](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor)

## <a name="next-steps"></a><span data-ttu-id="3eeda-206">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3eeda-206">Next steps</span></span>
<span data-ttu-id="3eeda-207">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="3eeda-207">Learn more about</span></span>
- <span data-ttu-id="3eeda-208">Azure Monitor 비디오 연습은</span><span class="sxs-lookup"><span data-stu-id="3eeda-208">A video walkthrough of just Azure Monitor is available at</span></span>  
<span data-ttu-id="3eeda-209">[Azure Monitor 시작](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor)에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-209">[Get Started with Azure Monitor](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor).</span></span> <span data-ttu-id="3eeda-210">Azure Monitor를 사용할 수 있는 시나리오를 설명하는 추가 비디오는 [Microsoft Azure 모니터링 및 진단 탐색](https://channel9.msdn.com/events/Ignite/2016/BRK2234)(영문) 및 [Azure Monitor(Ignite 2016 비디오)](https://myignite.microsoft.com/videos/4977)(영문)에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-210">An additional video explaining a scenario where you can use Azure Monitor is available at [Explore Microsoft Azure monitoring and diagnostics](https://channel9.msdn.com/events/Ignite/2016/BRK2234) and [Azure Monitor in a video from Ignite 2016](https://myignite.microsoft.com/videos/4977)</span></span>
- <span data-ttu-id="3eeda-211">hello Azure 모니터 인터페이스를 통해 실행 [Azure 모니터 시작](monitoring-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="3eeda-211">Run through hello Azure Monitor interface in [Getting Started with Azure Monitor](monitoring-get-started.md)</span></span>
- <span data-ttu-id="3eeda-212">Hello 설정 [Azure 진단 확장](../azure-diagnostics.md) toodiagnose 문제 클라우드 서비스, 가상 컴퓨터에서에서 시도 하는 경우 가상 컴퓨터의 크기를 조정 하거나 설정 또는 서비스 패브릭 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="3eeda-212">Set up hello [Azure Diagnostics Extensions](../azure-diagnostics.md) if you are attempting toodiagnose problems in your Cloud Service, Virtual Machine, Virtual machine scale sets, or Service Fabric application.</span></span>
- <span data-ttu-id="3eeda-213">[Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) 앱 서비스 웹 앱의 toodiagnostic 문제를 사용 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="3eeda-213">[Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) if you are trying toodiagnostic problems in your App Service Web app.</span></span>
- <span data-ttu-id="3eeda-214">[Azure Storage 문제 해결](../storage/common/storage-e2e-troubleshooting.md) - 저장소 Blob, 테이블 및 큐를 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="3eeda-214">[Troubleshooting Azure Storage](../storage/common/storage-e2e-troubleshooting.md) when using Storage Blobs, Tables, or Queues</span></span>
- <span data-ttu-id="3eeda-215">[로그 분석](https://azure.microsoft.com/documentation/services/log-analytics/) 및 hello [Operations Management Suite](https://www.microsoft.com/oms/)</span><span class="sxs-lookup"><span data-stu-id="3eeda-215">[Log Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) and hello [Operations Management Suite](https://www.microsoft.com/oms/)</span></span>
