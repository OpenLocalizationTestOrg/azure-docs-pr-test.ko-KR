---
title: "일괄 처리 이벤트-Azure의 진단 로깅 aaaEnable | Microsoft Docs"
description: "풀, 작업 등과 같은 Azure Batch 계정 리소스에 대해 진단 로그 이벤트를 기록 및 분석합니다."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: e14e611d-12cd-4671-91dc-bc506dc853e5
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9d03303a3e857e9303f40cc6de5c32b5a51d8f8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a><span data-ttu-id="dcb8e-103">Batch 솔루션의 진단 평가 및 모니터링에 대한 로그 이벤트</span><span class="sxs-lookup"><span data-stu-id="dcb8e-103">Log events for diagnostic evaluation and monitoring of Batch solutions</span></span>

<span data-ttu-id="dcb8e-104">여러 Azure 서비스와 마찬가지로 hello 일괄 처리 서비스는 특정 리소스 중 hello hello 리소스 수명을 이벤트를 로그를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dcb8e-104">As with many Azure services, hello Batch service emits log events for certain resources during hello lifetime of hello resource.</span></span> <span data-ttu-id="dcb8e-105">풀 및 작업을 같은 리소스에 대 한 Azure 배치 진단 로그 toorecord 이벤트를 활성화 하 고 진단 평가 및 모니터링에 대 한 hello 로그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcb8e-105">You can enable Azure Batch diagnostic logs toorecord events for resources like pools and tasks, and then use hello logs for diagnostic evaluation and monitoring.</span></span> <span data-ttu-id="dcb8e-106">풀 만들기, 풀 삭제, 작업 시작, 작업 완료, 기타 등의 이벤트는 Batch 진단 로그에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcb8e-106">Events like pool create, pool delete, task start, task complete, and others are included in Batch diagnostic logs.</span></span>

> [!NOTE]
> <span data-ttu-id="dcb8e-107">이 문서에서는 작업과 작업 출력 데이터가 아닌 배치 계정 리소스 자체에 대한 이벤트 로깅을 논의합니다.</span><span class="sxs-lookup"><span data-stu-id="dcb8e-107">This article discusses logging events for Batch account resources themselves, not job and task output data.</span></span> <span data-ttu-id="dcb8e-108">작업 및 작업의 hello 출력 데이터 저장에 대 한 세부 정보를 참조 하십시오. [지속 Azure 일괄 처리 작업 및 태스크 출력](batch-task-output.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dcb8e-108">For details on storing hello output data of your jobs and tasks, see [Persist Azure Batch job and task output](batch-task-output.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="dcb8e-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="dcb8e-109">Prerequisites</span></span>
* [<span data-ttu-id="dcb8e-110">Azure Batch 계정</span><span class="sxs-lookup"><span data-stu-id="dcb8e-110">Azure Batch account</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="dcb8e-111">Azure Storage 계정</span><span class="sxs-lookup"><span data-stu-id="dcb8e-111">Azure Storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  <span data-ttu-id="dcb8e-112">toopersist 일괄 처리 진단 로그를 Azure hello 로그를 저장 하는 Azure 저장소 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcb8e-112">toopersist Batch diagnostic logs, you must create an Azure Storage account where Azure will store hello logs.</span></span> <span data-ttu-id="dcb8e-113">배치 계정에 [진단 로깅을 사용](#enable-diagnostic-logging)할 때 이 저장소 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dcb8e-113">You specify this Storage account when you [enable diagnostic logging](#enable-diagnostic-logging) for your Batch account.</span></span> <span data-ttu-id="dcb8e-114">연결 된 저장소 계정 참조 tooin hello로 동일를 hello 로그 수집을 사용 하면 지정한 저장소 계정이 hello 하지 [응용 프로그램 패키지](batch-application-packages.md) 및 [작업 출력 지 속성](batch-task-output.md) 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="dcb8e-114">hello Storage account you specify when you enable log collection is not hello same as a linked storage account referred tooin hello [application packages](batch-application-packages.md) and [task output persistence](batch-task-output.md) articles.</span></span>
  
  > [!WARNING]
  > <span data-ttu-id="dcb8e-115">**청구** Azure 저장소 계정에 저장 된 hello 데이터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcb8e-115">You are **charged** for hello data stored in your Azure Storage account.</span></span> <span data-ttu-id="dcb8e-116">이 문서에서 설명 하는 hello 진단 로그가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcb8e-116">This includes hello diagnostic logs discussed in this article.</span></span> <span data-ttu-id="dcb8e-117">[로그 보존 정책](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)을 설계할 때는 이 점을 염두에 둡니다.</span><span class="sxs-lookup"><span data-stu-id="dcb8e-117">Keep this in mind when designing your [log retention policy](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span></span>
  > 
  > 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="dcb8e-118">진단 로깅 사용</span><span class="sxs-lookup"><span data-stu-id="dcb8e-118">Enable diagnostic logging</span></span>
<span data-ttu-id="dcb8e-119">진단 로깅은 배치 계정에 기본적으로 활성화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dcb8e-119">Diagnostic logging is not enabled by default for your Batch account.</span></span> <span data-ttu-id="dcb8e-120">Toomonitor 원하는 각 일괄 처리 계정에 대 한 진단 로깅을 명시적으로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcb8e-120">You must explicitly enable diagnostic logging for each Batch account you want toomonitor:</span></span>

[<span data-ttu-id="dcb8e-121">어떻게 진단 로그의 tooenable 컬렉션</span><span class="sxs-lookup"><span data-stu-id="dcb8e-121">How tooenable collection of Diagnostic Logs</span></span>](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

<span data-ttu-id="dcb8e-122">Hello 전체를 읽는 것이 좋습니다 [개요의 Azure 진단 로그](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) 다양 한 Azure 서비스 hello에서 지 원하는 문서 toogain 뿐만 아니라 tooenable 로깅을 하지만 hello 로그 하는 방법은 범주를 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcb8e-122">We recommend that you read hello full [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article toogain an understanding of not only how tooenable logging, but hello log categories supported by hello various Azure services.</span></span> <span data-ttu-id="dcb8e-123">예를 들어, 현재 Azure Batch는 **서비스 로그** 카테고리 하나만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dcb8e-123">For example, Azure Batch currently supports one log category: **Service Logs**.</span></span>

## <a name="service-logs"></a><span data-ttu-id="dcb8e-124">서비스 로그</span><span class="sxs-lookup"><span data-stu-id="dcb8e-124">Service Logs</span></span>
<span data-ttu-id="dcb8e-125">Azure 일괄 처리 서비스 로그 풀 또는 작업 처럼 일괄 처리 리소스의 hello 수명 동안 hello Azure 배치 서비스에서 내보내는 이벤트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcb8e-125">Azure Batch Service Logs contain events emitted by hello Azure Batch service during hello lifetime of a Batch resource like a pool or task.</span></span> <span data-ttu-id="dcb8e-126">일괄 처리에 의해 발생 하는 각 이벤트는 지정 된 hello에 저장 된 JSON 형식으로 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="dcb8e-126">Each event emitted by Batch is stored in hello specified Storage account in JSON format.</span></span> <span data-ttu-id="dcb8e-127">예를 들어,이 샘플의 hello 본문 **풀 만들기 이벤트**:</span><span class="sxs-lookup"><span data-stu-id="dcb8e-127">For example, this is hello body of a sample **pool create event**:</span></span>

```json
{
    "poolId": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "4",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicatedComputeNodes": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoscale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

<span data-ttu-id="dcb8e-128">.Json<에 각 이벤트 본문이 있는 파일 hello에 Azure 저장소 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcb8e-128">Each event body resides in a .json file in hello specified Azure Storage account.</span></span> <span data-ttu-id="dcb8e-129">Tooaccess 로그를 직접 hello를 원하는 경우 tooreview hello을 지정할 수 있습니다 [hello 저장소 계정에 진단 로그의 스키마](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="dcb8e-129">If you want tooaccess hello logs directly, you may wish tooreview hello [schema of Diagnostic Logs in hello storage account](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span></span>

## <a name="service-log-events"></a><span data-ttu-id="dcb8e-130">서비스 로그 이벤트</span><span class="sxs-lookup"><span data-stu-id="dcb8e-130">Service Log events</span></span>
<span data-ttu-id="dcb8e-131">hello를 일괄 처리 서비스는 현재 hello를 다음 서비스 로그 이벤트를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dcb8e-131">hello Batch service currently emits hello following Service Log events.</span></span> <span data-ttu-id="dcb8e-132">이 목록은 전체가 아니며, 이 문서가 마지막으로 업데이트된 뒤 다른 이벤트가 추가되었을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcb8e-132">This list may not be exhaustive, since additional events may have been added since this article was last updated.</span></span>

| <span data-ttu-id="dcb8e-133">**서비스 로그 이벤트**</span><span class="sxs-lookup"><span data-stu-id="dcb8e-133">**Service Log events**</span></span> |
| --- |
| <span data-ttu-id="dcb8e-134">[풀 만들기][pool_create]</span><span class="sxs-lookup"><span data-stu-id="dcb8e-134">[Pool create][pool_create]</span></span> |
| <span data-ttu-id="dcb8e-135">[풀 삭제 시작][pool_delete_start]</span><span class="sxs-lookup"><span data-stu-id="dcb8e-135">[Pool delete start][pool_delete_start]</span></span> |
| <span data-ttu-id="dcb8e-136">[풀 삭제 완료][pool_delete_complete]</span><span class="sxs-lookup"><span data-stu-id="dcb8e-136">[Pool delete complete][pool_delete_complete]</span></span> |
| <span data-ttu-id="dcb8e-137">[풀 크기 조정 시작][pool_resize_start]</span><span class="sxs-lookup"><span data-stu-id="dcb8e-137">[Pool resize start][pool_resize_start]</span></span> |
| <span data-ttu-id="dcb8e-138">[풀 크기 조정 완료][pool_resize_complete]</span><span class="sxs-lookup"><span data-stu-id="dcb8e-138">[Pool resize complete][pool_resize_complete]</span></span> |
| <span data-ttu-id="dcb8e-139">[작업 시작][task_start]</span><span class="sxs-lookup"><span data-stu-id="dcb8e-139">[Task start][task_start]</span></span> |
| <span data-ttu-id="dcb8e-140">[작업 완료][task_complete]</span><span class="sxs-lookup"><span data-stu-id="dcb8e-140">[Task complete][task_complete]</span></span> |
| <span data-ttu-id="dcb8e-141">[작업 실패][task_fail]</span><span class="sxs-lookup"><span data-stu-id="dcb8e-141">[Task fail][task_fail]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dcb8e-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dcb8e-142">Next steps</span></span>
<span data-ttu-id="dcb8e-143">또한 toostoring 진단 로그는 Azure 저장소 계정에 이벤트, 스트리밍할 수도 있습니다 일괄 처리 서비스 로그 이벤트 tooan [Azure 이벤트 허브](../event-hubs/event-hubs-what-is-event-hubs.md), 너무 보내도록[Azure 로그 분석](../log-analytics/log-analytics-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dcb8e-143">In addition toostoring diagnostic log events in an Azure Storage account, you can also stream Batch Service Log events tooan [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md), and send them too[Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span>

* [<span data-ttu-id="dcb8e-144">Azure 진단 로그 tooEvent 허브 스트림</span><span class="sxs-lookup"><span data-stu-id="dcb8e-144">Stream Azure Diagnostic Logs tooEvent Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  <span data-ttu-id="dcb8e-145">일괄 처리 진단 이벤트 toohello 확장성이 높은 데이터 유입 서비스를, 이벤트 허브를 스트리밍하십시오.</span><span class="sxs-lookup"><span data-stu-id="dcb8e-145">Stream Batch diagnostic events toohello highly scalable data ingress service, Event Hubs.</span></span> <span data-ttu-id="dcb8e-146">이벤트 허브는 초당 수백 건의 이벤트를 수집하여 모든 실시간 분석 공급자를 통해 변환 및 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcb8e-146">Event Hubs can ingest millions of events per second, which you can then transform and store using any real-time analytics provider.</span></span>
* [<span data-ttu-id="dcb8e-147">Log Analytics를 사용하여 Azure 진단 로그 분석 </span><span class="sxs-lookup"><span data-stu-id="dcb8e-147">Analyze Azure diagnostic logs using Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
  
  <span data-ttu-id="dcb8e-148">사용자 진단 로그 tooLog hello Operations Management Suite (OMS) 포털에서이 분석 하거나 Power BI 또는 Excel에서 분석을 위해 내보낼 수 있는 분석을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dcb8e-148">Send your diagnostic logs tooLog Analytics where you can analyze them in hello Operations Management Suite (OMS) portal, or export them for analysis in Power BI or Excel.</span></span>

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
