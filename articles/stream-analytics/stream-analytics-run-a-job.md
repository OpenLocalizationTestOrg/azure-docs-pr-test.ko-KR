---
title: "Stream Analytics에서 스트리밍 작업을 시작 하는 방법 | Microsoft Docs"
description: "Azure Stream Analytics에서 스트리밍 작업을 실행 하는 방법 | 학습 경로 세그먼트"
keywords: "스트리밍 작업"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9d46950f-2b69-49ce-a567-df558c5dd820
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 9a3ff37a893b0f29a2ac2eda6cd50687ee779ead
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-run-a-streaming-job-in-azure-stream-analytics"></a><span data-ttu-id="9f3d5-104">Azure Stream Analytics에서 스트리밍 작업을 실행 하는 방법</span><span class="sxs-lookup"><span data-stu-id="9f3d5-104">How to run a streaming job in Azure Stream Analytics</span></span>
<span data-ttu-id="9f3d5-105">작업 입력, 쿼리 및 출력을 모두 지정했으면 Stream Analytics 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f3d5-105">When a job input, query and output have all been specified you can start the Stream Analytics job.</span></span>

<span data-ttu-id="9f3d5-106">작업을 시작하려면</span><span class="sxs-lookup"><span data-stu-id="9f3d5-106">To start your job:</span></span>

1. <span data-ttu-id="9f3d5-107">Azure 클래식 포털의 작업 대시보드의 페이지 아래쪽에서 **시작** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f3d5-107">In the Azure Classic portal, from the job dashboard, click **Start** at the bottom of the page.</span></span>
   
   ![작업 시작 단추](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   <span data-ttu-id="9f3d5-109">Azure Portal의 작업 페이지 맨 위에서 **시작** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f3d5-109">In the Azure portal, click **Start** at the top of your job page.</span></span>
   
   ![Azure Portal 작업 시작 단추](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. <span data-ttu-id="9f3d5-111">**출력 시작** 값을 지정하여 이 작업이 출력 생성을 시작하는 시기를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="9f3d5-111">Specify a **Start Output** value to determine when this job will start producing output.</span></span> <span data-ttu-id="9f3d5-112">이전에 시작되지 않은 작업에 대한 기본 설정은 **작업 시작 시간**으로 이는 작업이 즉시 데이터 처리를 시작함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="9f3d5-112">The default setting for jobs that have not previously been started is **Job Start Time**, which means that the job will immediately start processing data.</span></span> <span data-ttu-id="9f3d5-113">과거(기록 데이터 사용을 위해) 또는 미래(미래 시간까지 처리 지연을 위해)의 **사용자 지정** 시간을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f3d5-113">You can also specify a **Custom** time in the past (for consuming historical data) or the future (to delay processing until a future time).</span></span> <span data-ttu-id="9f3d5-114">작업이 이전에 시작 및 중지된 경우 마지막 출력 시간부터 작업을 다시 시작하고 데이터 손실을 방지하기 위해 **마지막 중지 시간** 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f3d5-114">For cases when a job has been previously started and stopped, the option **Last Stopped Time** is available in order to resume the job from the last output time and avoid data loss.</span></span>  
   
   ![스트리밍 작업 시작 시간](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Azure Portal 스트리밍 작업 시작 시간](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. <span data-ttu-id="9f3d5-117">선택을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9f3d5-117">Confirm your selection.</span></span> <span data-ttu-id="9f3d5-118">작업 상태가 *시작 중*으로 변경되었다가 작업이 시작되면 곧 *실행 중*으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f3d5-118">The job status will change to *Starting* and will shortly move to *Running* once the job has started.</span></span> <span data-ttu-id="9f3d5-119">**알림 허브**에서 **시작** 작업의 진행률을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f3d5-119">You can monitor the progress of the **Start** operation in the **Notification Hub**:</span></span>
   
   ![스트림 작업 진행률](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Azure Portal 스트리밍 작업 진행률](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="9f3d5-122">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="9f3d5-122">Get help</span></span>
<span data-ttu-id="9f3d5-123">추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="9f3d5-123">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f3d5-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9f3d5-124">Next steps</span></span>
* [<span data-ttu-id="9f3d5-125">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="9f3d5-125">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="9f3d5-126">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="9f3d5-126">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="9f3d5-127">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="9f3d5-127">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="9f3d5-128">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="9f3d5-128">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="9f3d5-129">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="9f3d5-129">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

