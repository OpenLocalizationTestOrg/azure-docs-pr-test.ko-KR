---
title: "배치 이벤트에 대한 진단 로깅 사용 - Azure | Microsoft Docs"
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
ms.openlocfilehash: b7bc6fd9921ab0f2374ace33ea5c1ab93a78f860
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a><span data-ttu-id="f1a1a-103">Batch 솔루션의 진단 평가 및 모니터링에 대한 로그 이벤트</span><span class="sxs-lookup"><span data-stu-id="f1a1a-103">Log events for diagnostic evaluation and monitoring of Batch solutions</span></span>

<span data-ttu-id="f1a1a-104">많은 Azure 서비스와 마찬가지로 Batch 서비스는 리소스 수명 주기 동안 특정 리소스에 대한 로그 이벤트를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f1a1a-104">As with many Azure services, the Batch service emits log events for certain resources during the lifetime of the resource.</span></span> <span data-ttu-id="f1a1a-105">Azure Batch 진단 로그를 사용하여 풀 및 작업 등의 리소스에 대한 이벤트를 기록하고 이 로그를 진단 평가와 모니터링에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1a1a-105">You can enable Azure Batch diagnostic logs to record events for resources like pools and tasks, and then use the logs for diagnostic evaluation and monitoring.</span></span> <span data-ttu-id="f1a1a-106">풀 만들기, 풀 삭제, 작업 시작, 작업 완료, 기타 등의 이벤트는 Batch 진단 로그에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1a1a-106">Events like pool create, pool delete, task start, task complete, and others are included in Batch diagnostic logs.</span></span>

> [!NOTE]
> <span data-ttu-id="f1a1a-107">이 문서에서는 작업과 작업 출력 데이터가 아닌 배치 계정 리소스 자체에 대한 이벤트 로깅을 논의합니다.</span><span class="sxs-lookup"><span data-stu-id="f1a1a-107">This article discusses logging events for Batch account resources themselves, not job and task output data.</span></span> <span data-ttu-id="f1a1a-108">작업 및 태스크의 출력 데이터 저장에 대한 자세한 내용은 [Azure Batch 작업 및 태스크 보관](batch-task-output.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f1a1a-108">For details on storing the output data of your jobs and tasks, see [Persist Azure Batch job and task output](batch-task-output.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="f1a1a-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f1a1a-109">Prerequisites</span></span>
* [<span data-ttu-id="f1a1a-110">Azure Batch 계정</span><span class="sxs-lookup"><span data-stu-id="f1a1a-110">Azure Batch account</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="f1a1a-111">Azure Storage 계정</span><span class="sxs-lookup"><span data-stu-id="f1a1a-111">Azure Storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  <span data-ttu-id="f1a1a-112">배치 진단 로그를 유지하려면 Azure가 로드를 저장하는 Azure Storage 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1a1a-112">To persist Batch diagnostic logs, you must create an Azure Storage account where Azure will store the logs.</span></span> <span data-ttu-id="f1a1a-113">배치 계정에 [진단 로깅을 사용](#enable-diagnostic-logging)할 때 이 저장소 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f1a1a-113">You specify this Storage account when you [enable diagnostic logging](#enable-diagnostic-logging) for your Batch account.</span></span> <span data-ttu-id="f1a1a-114">로그 수집을 사용할 때 지정하는 저장소 계정은 [응용 프로그램 패키지](batch-application-packages.md) 및 [작업 출력 지속성](batch-task-output.md) 문서에서 설명한 연결된 저장소 계정과는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f1a1a-114">The Storage account you specify when you enable log collection is not the same as a linked storage account referred to in the [application packages](batch-application-packages.md) and [task output persistence](batch-task-output.md) articles.</span></span>
  
  > [!WARNING]
  > <span data-ttu-id="f1a1a-115">Azure Storage 계정에 저장된 데이터에 대해 요금이 **청구**됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1a1a-115">You are **charged** for the data stored in your Azure Storage account.</span></span> <span data-ttu-id="f1a1a-116">여기에는 이 문서에서 논의하는 진단 로그가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1a1a-116">This includes the diagnostic logs discussed in this article.</span></span> <span data-ttu-id="f1a1a-117">[로그 보존 정책](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)을 설계할 때는 이 점을 염두에 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f1a1a-117">Keep this in mind when designing your [log retention policy](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span></span>
  > 
  > 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="f1a1a-118">진단 로깅 사용</span><span class="sxs-lookup"><span data-stu-id="f1a1a-118">Enable diagnostic logging</span></span>
<span data-ttu-id="f1a1a-119">진단 로깅은 배치 계정에 기본적으로 활성화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1a1a-119">Diagnostic logging is not enabled by default for your Batch account.</span></span> <span data-ttu-id="f1a1a-120">모니터링할 각각의 배치 계정에 대해 진단 로그를 명시적으로 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1a1a-120">You must explicitly enable diagnostic logging for each Batch account you want to monitor:</span></span>

[<span data-ttu-id="f1a1a-121">진단 로그의 컬렉션을 사용하도록 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="f1a1a-121">How to enable collection of Diagnostic Logs</span></span>](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

<span data-ttu-id="f1a1a-122">전체 [Azure Diagnostic Logs 개요](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) 문서를 읽고 로깅 사용뿐 아니라 여러 Azure 서비스에서 지원하는 로그 카테고리에 대해서도 파악하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f1a1a-122">We recommend that you read the full [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article to gain an understanding of not only how to enable logging, but the log categories supported by the various Azure services.</span></span> <span data-ttu-id="f1a1a-123">예를 들어, 현재 Azure Batch는 **서비스 로그** 카테고리 하나만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f1a1a-123">For example, Azure Batch currently supports one log category: **Service Logs**.</span></span>

## <a name="service-logs"></a><span data-ttu-id="f1a1a-124">서비스 로그</span><span class="sxs-lookup"><span data-stu-id="f1a1a-124">Service Logs</span></span>
<span data-ttu-id="f1a1a-125">Azure Batch 서비스 로그는 풀이나 작업 같은 배치 리소스의 수명 주기 동안 Azure Batch 서비스가 내보낸 이벤트를 포함합니다. </span><span class="sxs-lookup"><span data-stu-id="f1a1a-125">Azure Batch Service Logs contain events emitted by the Azure Batch service during the lifetime of a Batch resource like a pool or task.</span></span> <span data-ttu-id="f1a1a-126">배치에서 내보낸 각각의 이벤트는 JSON 형식으로 지정된 저장소 계정에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1a1a-126">Each event emitted by Batch is stored in the specified Storage account in JSON format.</span></span> <span data-ttu-id="f1a1a-127">예를 들어 샘플 **풀 만들기 이벤트**의 본문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f1a1a-127">For example, this is the body of a sample **pool create event**:</span></span>

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

<span data-ttu-id="f1a1a-128">각 이벤트 본문은 지정된 Azure Storage 계정의 .json 파일 안에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1a1a-128">Each event body resides in a .json file in the specified Azure Storage account.</span></span> <span data-ttu-id="f1a1a-129">로그에 직접 액세스하려면 [저장소 계정의 진단 로그 스키마](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account)를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1a1a-129">If you want to access the logs directly, you may wish to review the [schema of Diagnostic Logs in the storage account](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span></span>

## <a name="service-log-events"></a><span data-ttu-id="f1a1a-130">서비스 로그 이벤트</span><span class="sxs-lookup"><span data-stu-id="f1a1a-130">Service Log events</span></span>
<span data-ttu-id="f1a1a-131">배치 서비스는 현재 다음과 같은 서비스 로그 이벤트를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f1a1a-131">The Batch service currently emits the following Service Log events.</span></span> <span data-ttu-id="f1a1a-132">이 목록은 전체가 아니며, 이 문서가 마지막으로 업데이트된 뒤 다른 이벤트가 추가되었을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1a1a-132">This list may not be exhaustive, since additional events may have been added since this article was last updated.</span></span>

| <span data-ttu-id="f1a1a-133">**서비스 로그 이벤트**</span><span class="sxs-lookup"><span data-stu-id="f1a1a-133">**Service Log events**</span></span> |
| --- |
| <span data-ttu-id="f1a1a-134">[풀 만들기][pool_create]</span><span class="sxs-lookup"><span data-stu-id="f1a1a-134">[Pool create][pool_create]</span></span> |
| <span data-ttu-id="f1a1a-135">[풀 삭제 시작][pool_delete_start]</span><span class="sxs-lookup"><span data-stu-id="f1a1a-135">[Pool delete start][pool_delete_start]</span></span> |
| <span data-ttu-id="f1a1a-136">[풀 삭제 완료][pool_delete_complete]</span><span class="sxs-lookup"><span data-stu-id="f1a1a-136">[Pool delete complete][pool_delete_complete]</span></span> |
| <span data-ttu-id="f1a1a-137">[풀 크기 조정 시작][pool_resize_start]</span><span class="sxs-lookup"><span data-stu-id="f1a1a-137">[Pool resize start][pool_resize_start]</span></span> |
| <span data-ttu-id="f1a1a-138">[풀 크기 조정 완료][pool_resize_complete]</span><span class="sxs-lookup"><span data-stu-id="f1a1a-138">[Pool resize complete][pool_resize_complete]</span></span> |
| <span data-ttu-id="f1a1a-139">[작업 시작][task_start]</span><span class="sxs-lookup"><span data-stu-id="f1a1a-139">[Task start][task_start]</span></span> |
| <span data-ttu-id="f1a1a-140">[작업 완료][task_complete]</span><span class="sxs-lookup"><span data-stu-id="f1a1a-140">[Task complete][task_complete]</span></span> |
| <span data-ttu-id="f1a1a-141">[작업 실패][task_fail]</span><span class="sxs-lookup"><span data-stu-id="f1a1a-141">[Task fail][task_fail]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f1a1a-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f1a1a-142">Next steps</span></span>
<span data-ttu-id="f1a1a-143">Azure Storage 계정에 진단 로그를 저장하는 것 외에도 [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md)에 배치 서비스 로그 이벤트를 스트림하고 [Azure Log Analytics](../log-analytics/log-analytics-overview.md)로 보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1a1a-143">In addition to storing diagnostic log events in an Azure Storage account, you can also stream Batch Service Log events to an [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md), and send them to [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span>

* [<span data-ttu-id="f1a1a-144">이벤트 허브로 Azure 진단 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="f1a1a-144">Stream Azure Diagnostic Logs to Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  <span data-ttu-id="f1a1a-145">배치 진단 이벤트를 확장성 높은 데이터 수집 서비스인 이벤트 허브에 스트림합니다.</span><span class="sxs-lookup"><span data-stu-id="f1a1a-145">Stream Batch diagnostic events to the highly scalable data ingress service, Event Hubs.</span></span> <span data-ttu-id="f1a1a-146">이벤트 허브는 초당 수백 건의 이벤트를 수집하여 모든 실시간 분석 공급자를 통해 변환 및 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1a1a-146">Event Hubs can ingest millions of events per second, which you can then transform and store using any real-time analytics provider.</span></span>
* [<span data-ttu-id="f1a1a-147">Log Analytics를 사용하여 Azure 진단 로그 분석 </span><span class="sxs-lookup"><span data-stu-id="f1a1a-147">Analyze Azure diagnostic logs using Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
  
  <span data-ttu-id="f1a1a-148">OMS(Operations Management Suite) 포털에서 분석할 수 있게 진단 로그를 Log Analytics로 보내거나, Power BI 또는 Excel에서의 분석을 위해 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f1a1a-148">Send your diagnostic logs to Log Analytics where you can analyze them in the Operations Management Suite (OMS) portal, or export them for analysis in Power BI or Excel.</span></span>

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
