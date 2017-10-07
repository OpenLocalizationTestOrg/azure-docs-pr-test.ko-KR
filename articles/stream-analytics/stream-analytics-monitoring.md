---
title: "스트림 분석 작업 모니터링 aaaUnderstanding | Microsoft Docs"
description: "Stream Analytics 작업 모니터링 이해"
keywords: "쿼리 모니터"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5f5cc00f-4a7b-491e-89e1-dbafea46d399
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 36819025c7b2ddbf4b9694522f1b4820407ca5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-toomonitor-queries"></a><span data-ttu-id="50d76-104">스트림 분석 작업 모니터링 이해 및 방법을 toomonitor 쿼리</span><span class="sxs-lookup"><span data-stu-id="50d76-104">Understand Stream Analytics job monitoring and how toomonitor queries</span></span>

## <a name="introduction-hello-monitor-page"></a><span data-ttu-id="50d76-105">소개: hello 모니터 페이지</span><span class="sxs-lookup"><span data-stu-id="50d76-105">Introduction: hello monitor page</span></span>
<span data-ttu-id="50d76-106">Azure 포털 둘 다 화면 쿼리 및 작업 성능 문제를 해결 하 고 사용 하는 toomonitor 수 있는 주요 성능 메트릭을 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="50d76-106">hello Azure portal both surface key performance metrics that can be used toomonitor and troubleshoot your query and job performance.</span></span> <span data-ttu-id="50d76-107">toosee 이러한 메트릭을 찾아보기 toohello 스트림 분석 작업에 대 한 메트릭을 보기 hello에 관심이 있는 **모니터링** hello 개요 페이지에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="50d76-107">toosee these metrics, browse toohello Stream Analytics job you are interested in seeing metrics for and view hello **Monitoring** section on hello Overview page.</span></span>  

![모니터링 링크](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

<span data-ttu-id="50d76-109">hello 창에 표시 된 것 처럼 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="50d76-109">hello window will appear as shown:</span></span>

![작업 모니터링 대시보드](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a><span data-ttu-id="50d76-111">Stream Analytics에 사용 가능한 메트릭</span><span class="sxs-lookup"><span data-stu-id="50d76-111">Metrics available for Stream Analytics</span></span>
| <span data-ttu-id="50d76-112">메트릭</span><span class="sxs-lookup"><span data-stu-id="50d76-112">Metric</span></span>                 | <span data-ttu-id="50d76-113">정의</span><span class="sxs-lookup"><span data-stu-id="50d76-113">Definition</span></span>                               |
| ---------------------- | ---------------------------------------- |
| <span data-ttu-id="50d76-114">SU % 사용률</span><span class="sxs-lookup"><span data-stu-id="50d76-114">SU % Utilization</span></span>       | <span data-ttu-id="50d76-115">hello의 hello 사용률이 스트리밍 단위 tooa 작업 hello 작업의 hello 크기 조정 탭에서 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="50d76-115">hello utilization of hello Streaming Unit(s) assigned tooa job from hello Scale tab of hello job.</span></span> <span data-ttu-id="50d76-116">이 표시가 80% 이상에 도달하면 이벤트 처리가 지연되거나 진행을 중단할 가능성이 큽니다.</span><span class="sxs-lookup"><span data-stu-id="50d76-116">Should this indicator reach 80%, or above, there is high probability that event processing may be delayed or stopped making progress.</span></span> |
| <span data-ttu-id="50d76-117">입력 이벤트</span><span class="sxs-lookup"><span data-stu-id="50d76-117">Input Events</span></span>           | <span data-ttu-id="50d76-118">이벤트 수의 hello 스트림 분석 작업에서 받은 데이터의 양입니다.</span><span class="sxs-lookup"><span data-stu-id="50d76-118">Amount of data received by hello Stream Analytics job, in number of events.</span></span> <span data-ttu-id="50d76-119">이 이벤트는 toohello 입력된 소스 전송 되 고 사용 하는 toovalidate 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50d76-119">This can be used toovalidate that events are being sent toohello input source.</span></span> |
| <span data-ttu-id="50d76-120">출력 이벤트</span><span class="sxs-lookup"><span data-stu-id="50d76-120">Output Events</span></span>          | <span data-ttu-id="50d76-121">Hello 스트림 분석 작업 toohello 출력 대상에서 이벤트의 수에 전송 되는 데이터의 양입니다.</span><span class="sxs-lookup"><span data-stu-id="50d76-121">Amount of data sent by hello Stream Analytics job toohello output target, in number of events.</span></span> |
| <span data-ttu-id="50d76-122">순서 비지정 이벤트</span><span class="sxs-lookup"><span data-stu-id="50d76-122">Out-of-Order Events</span></span>    | <span data-ttu-id="50d76-123">삭제 했거나 hello 이벤트 순서 정책에 따라는 조정 된 타임 스탬프를 지정 하는 순서가 틀리게 수신 하는 이벤트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="50d76-123">Number of events received out of order that were either dropped or given an adjusted timestamp, based on hello Event Ordering Policy.</span></span> <span data-ttu-id="50d76-124">Hello Out of 순서 허용 시간 설정의 hello 구성에 의해 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50d76-124">This can be impacted by hello configuration of hello Out of Order Tolerance Window setting.</span></span> |
| <span data-ttu-id="50d76-125">데이터 변환 오류</span><span class="sxs-lookup"><span data-stu-id="50d76-125">Data Conversion Errors</span></span> | <span data-ttu-id="50d76-126">Stream Analytics 작업에 의해 발생하는 데이터 변환 오류 수입니다.</span><span class="sxs-lookup"><span data-stu-id="50d76-126">Number of data conversion errors incurred by a Stream Analytics job.</span></span> |
| <span data-ttu-id="50d76-127">런타임 오류</span><span class="sxs-lookup"><span data-stu-id="50d76-127">Runtime Errors</span></span>         | <span data-ttu-id="50d76-128">hello 스트림 분석 작업을 실행 하는 동안 발생 하는 오류의 총 수입니다.</span><span class="sxs-lookup"><span data-stu-id="50d76-128">hello total number of errors that happen during execution of a Stream Analytics job.</span></span> |
| <span data-ttu-id="50d76-129">늦은 입력 이벤트</span><span class="sxs-lookup"><span data-stu-id="50d76-129">Late Input Events</span></span>      | <span data-ttu-id="50d76-130">Hello 늦게 도착 허용 시간 설정의 hello 이벤트 순서 정책 구성에 따라 하거나 삭제 된 hello 소스 또는 타임 스탬프에서 늦게 도착 하는 이벤트 수가 조정 되었습니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="50d76-130">Number of events arriving late from hello source which have either been dropped or their timestamp has been adjusted, based on hello Event Ordering Policy configuration of hello Late Arrival Tolerance Window setting.</span></span> |
| <span data-ttu-id="50d76-131">기능 요청</span><span class="sxs-lookup"><span data-stu-id="50d76-131">Function Requests</span></span>      | <span data-ttu-id="50d76-132">호출 toohello Azure 기계 학습 함수 (있는 경우)의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="50d76-132">Number of calls toohello Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="50d76-133">실패한 기능 요청</span><span class="sxs-lookup"><span data-stu-id="50d76-133">Failed Function Requests</span></span> | <span data-ttu-id="50d76-134">실패한 Azure Machine Learning 함수 호출(있는 경우) 수입니다.</span><span class="sxs-lookup"><span data-stu-id="50d76-134">Number of failed Azure Machine Learning function calls (if present).</span></span> |
| <span data-ttu-id="50d76-135">함수 이벤트</span><span class="sxs-lookup"><span data-stu-id="50d76-135">Function Events</span></span>        | <span data-ttu-id="50d76-136">(있는 경우) toohello Azure 기계 학습 함수를 전송 하는 이벤트의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="50d76-136">Number of events sent toohello Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="50d76-137">입력 이벤트 바이트</span><span class="sxs-lookup"><span data-stu-id="50d76-137">Input Event Bytes</span></span>      | <span data-ttu-id="50d76-138">바이트의 hello 스트림 분석 작업에서 받은 데이터의 양입니다.</span><span class="sxs-lookup"><span data-stu-id="50d76-138">Amount of data received by hello Stream Analytics job, in bytes.</span></span> <span data-ttu-id="50d76-139">이 이벤트는 toohello 입력된 소스 전송 되 고 사용 하는 toovalidate 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50d76-139">This can be used toovalidate that events are being sent toohello input source.</span></span> |


## <a name="customizing-monitoring-in-hello-azure-portal"></a><span data-ttu-id="50d76-140">Hello Azure 포털에서에서 모니터링을 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="50d76-140">Customizing Monitoring in hello Azure portal</span></span>
<span data-ttu-id="50d76-141">Hello 종류의 차트를 표시 하는 메트릭 조정할 수 있으며 시간 hello 차트 편집 설정에서 범위 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50d76-141">You can adjust hello type of chart, metrics shown, and time range in hello Edit Chart settings.</span></span> <span data-ttu-id="50d76-142">자세한 내용은 참조 [어떻게 tooCustomize 모니터링](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="50d76-142">For details, see [How tooCustomize Monitoring](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

  ![쿼리 모니터 시간 그래프](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a><span data-ttu-id="50d76-144">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="50d76-144">Get help</span></span>
<span data-ttu-id="50d76-145">추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="50d76-145">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="50d76-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="50d76-146">Next steps</span></span>
* [<span data-ttu-id="50d76-147">스트림 분석 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="50d76-147">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="50d76-148">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="50d76-148">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="50d76-149">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="50d76-149">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="50d76-150">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="50d76-150">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="50d76-151">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="50d76-151">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

