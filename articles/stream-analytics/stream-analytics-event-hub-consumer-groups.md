---
title: "이벤트 허브 수신자를 사용하여 Azure Stream Analytics 디버그 | Microsoft Docs"
description: "Stream Analytics 작업에서 이벤트 허브 소비자 그룹을 고려하는 것에 대한 모범 사례를 쿼리합니다."
keywords: "이벤트 허브 제한, 소비자 그룹"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 145981d0b5eff0c574c5012c85f43a6318ba4126
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a><span data-ttu-id="605b5-104">이벤트 허브 수신자를 사용하여 Azure Stream Analytics 디버그</span><span class="sxs-lookup"><span data-stu-id="605b5-104">Debug Azure Stream Analytics with event hub receivers</span></span>

<span data-ttu-id="605b5-105">Azure Stream Analytics에서 Azure 이벤트 허브를 사용하여 작업에서 데이터를 수집하거나 출력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="605b5-105">You can use Azure Event Hubs in Azure Stream Analytics to ingest or output data from a job.</span></span> <span data-ttu-id="605b5-106">이벤트 허브 사용에 대한 모범 사례는 여러 소비자 그룹을 사용하여 작업 확장성을 보장하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="605b5-106">A best practice for using Event Hubs is to use multiple consumer groups, to ensure job scalability.</span></span> <span data-ttu-id="605b5-107">한 가지 이유는 특정 입력에 대한 Stream Analytics 작업의 판독기 수가 단일 소비자 그룹의 판독기 수에 영향을 준다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="605b5-107">One reason is that the number of readers in the Stream Analytics job for a specific input affects the number of readers in a single consumer group.</span></span> <span data-ttu-id="605b5-108">수신자의 정확한 수는 확장 토폴로지 논리에 대한 내부 구현 세부 정보를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="605b5-108">The precise number of receivers is based on internal implementation details for the scale-out topology logic.</span></span> <span data-ttu-id="605b5-109">수신자 수는 외부적으로 노출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="605b5-109">The number of receivers is not exposed externally.</span></span> <span data-ttu-id="605b5-110">판독기 수는 작업 시작 시간에 또는 작업을 업그레이드하는 동안에 바뀔 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="605b5-110">The number of readers can change either at the job start time or during job upgrades.</span></span>

> [!NOTE]
> <span data-ttu-id="605b5-111">작업을 업그레이드하는 동안 판독기 수가 변경되면 일시적인 경고가 감사 로그에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="605b5-111">When the number of readers changes during a job upgrade, transient warnings are written to audit logs.</span></span> <span data-ttu-id="605b5-112">Stream Analytics 작업은 자동으로 이러한 일시적인 문제를 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="605b5-112">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a><span data-ttu-id="605b5-113">파티션당 판독기 수가 5개 이벤트 허브 제한을 초과</span><span class="sxs-lookup"><span data-stu-id="605b5-113">Number of readers per partition exceeds Event Hubs limit of five</span></span>

<span data-ttu-id="605b5-114">파티션당 읽기 권한자 수가 5개 이벤트 허브 제한을 초과하는 시나리오에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="605b5-114">Scenarios in which the number of readers per partition exceeds the Event Hubs limit of five include the following:</span></span>

* <span data-ttu-id="605b5-115">여러 SELECT 문: **동일한** 이벤트 허브 입력을 참조하는 여러 SELECT 문을 사용하는 경우 각 SELECT 문으로 인해 새 수신기가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="605b5-115">Multiple SELECT statements: If you use multiple SELECT statements that refer to **same** event hub input, each SELECT statement causes a new receiver to be created.</span></span>
* <span data-ttu-id="605b5-116">UNION: UNION을 **동일한** 이벤트 허브 및 소비자 그룹을 참조하는 여러 입력이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="605b5-116">UNION: When you use a UNION, it's possible to have multiple inputs that refer to the **same** event hub and consumer group.</span></span>
* <span data-ttu-id="605b5-117">SELF JOIN: SELF JOIN 작업을 사용하면 **동일한** 이벤트 허브를 여러 번 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="605b5-117">SELF JOIN: When you use a SELF JOIN operation, it's possible to refer to the **same** event hub multiple times.</span></span>

## <a name="solution"></a><span data-ttu-id="605b5-118">해결 방법</span><span class="sxs-lookup"><span data-stu-id="605b5-118">Solution</span></span>

<span data-ttu-id="605b5-119">다음 모범 사례는 파티션당 읽기 권한자 수가 5개 이벤트 허브 제한을 초과하는 시나리오를 완화하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="605b5-119">The following best practices can help mitigate scenarios in which the number of readers per partition exceeds the Event Hubs limit of five.</span></span>

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a><span data-ttu-id="605b5-120">WITH 절을 사용하여 쿼리를 여러 단계로 분할</span><span class="sxs-lookup"><span data-stu-id="605b5-120">Split your query into multiple steps by using a WITH clause</span></span>

<span data-ttu-id="605b5-121">WITH 절은 쿼리의 FROM 절에서 참조할 수 있는 명명된 임시 결과 집합을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="605b5-121">The WITH clause specifies a temporary named result set that can be referenced by a FROM clause in the query.</span></span> <span data-ttu-id="605b5-122">단일 SELECT 문의 실행 범위에서 WITH 절을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="605b5-122">You define the WITH clause in the execution scope of a single SELECT statement.</span></span>

<span data-ttu-id="605b5-123">예를 들어 아래 쿼리 대신,</span><span class="sxs-lookup"><span data-stu-id="605b5-123">For example, instead of this query:</span></span>

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

<span data-ttu-id="605b5-124">다음 쿼리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="605b5-124">Use this query:</span></span>

```
WITH input (
   SELECT * FROM inputEventHub
) as data

SELECT foo
INTO output1
FROM data

SELECT bar
INTO output2
FROM data
…
```

### <a name="ensure-that-inputs-bind-to-different-consumer-groups"></a><span data-ttu-id="605b5-125">입력이 다른 소비자 그룹으로 바인딩되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="605b5-125">Ensure that inputs bind to different consumer groups</span></span>

<span data-ttu-id="605b5-126">세 개 이상의 입력이 동일한 이벤트 허브 소비자 그룹에 연결된 쿼리의 경우 개별 소비자 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="605b5-126">For queries in which three or more inputs are connected to the same Event Hubs consumer group, create separate consumer groups.</span></span> <span data-ttu-id="605b5-127">이를 위해서는 추가 Stream Analytics 입력을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="605b5-127">This requires the creation of additional Stream Analytics inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="605b5-128">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="605b5-128">Get help</span></span>
<span data-ttu-id="605b5-129">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="605b5-129">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="605b5-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="605b5-130">Next steps</span></span>
* [<span data-ttu-id="605b5-131">Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="605b5-131">Introduction to Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="605b5-132">Stream Analytics 시작</span><span class="sxs-lookup"><span data-stu-id="605b5-132">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="605b5-133">Stream Analytics 작업 크기 조정</span><span class="sxs-lookup"><span data-stu-id="605b5-133">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="605b5-134">Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="605b5-134">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="605b5-135">Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="605b5-135">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
