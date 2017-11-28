---
title: "스트림 분석에서 작업 스트리밍 aaaHow toostart | Microsoft Docs"
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
ms.openlocfilehash: 67aa14860c38cbd0535d0ec4f23729445d0185c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-streaming-job-in-azure-stream-analytics"></a><span data-ttu-id="186b3-104">스트리밍 toorun Azure 스트림 분석에서 작업 하는 방법</span><span class="sxs-lookup"><span data-stu-id="186b3-104">How toorun a streaming job in Azure Stream Analytics</span></span>
<span data-ttu-id="186b3-105">작업 입력 될 때 쿼리 및 출력 모두 지정 된 hello 스트림 분석 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="186b3-105">When a job input, query and output have all been specified you can start hello Stream Analytics job.</span></span>

<span data-ttu-id="186b3-106">toostart 작업:</span><span class="sxs-lookup"><span data-stu-id="186b3-106">toostart your job:</span></span>

1. <span data-ttu-id="186b3-107">Hello 작업 대시보드에서 hello Azure 클래식 포털에서 클릭 **시작** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="186b3-107">In hello Azure Classic portal, from hello job dashboard, click **Start** at hello bottom of hello page.</span></span>
   
   ![작업 시작 단추](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   <span data-ttu-id="186b3-109">Hello Azure 포털에서에서 클릭 **시작** hello 작업 페이지 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="186b3-109">In hello Azure portal, click **Start** at hello top of your job page.</span></span>
   
   ![Azure Portal 작업 시작 단추](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. <span data-ttu-id="186b3-111">지정 된 **시작 출력** 값 toodetermine 때이 작업의 출력을 생성이 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="186b3-111">Specify a **Start Output** value toodetermine when this job will start producing output.</span></span> <span data-ttu-id="186b3-112">hello 이전에 시작 되지 않은 작업에 대 한 기본 설정값은 **작업 시작 시간**, 즉 hello 작업이 데이터를 처리 즉시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="186b3-112">hello default setting for jobs that have not previously been started is **Job Start Time**, which means that hello job will immediately start processing data.</span></span> <span data-ttu-id="186b3-113">지정할 수 있습니다는 **사용자 지정** hello에 시간이 과거 (소비에 대 한 기록 데이터) 또는 향후 hello (toodelay 이후의 시간이 될 때까지 처리).</span><span class="sxs-lookup"><span data-stu-id="186b3-113">You can also specify a **Custom** time in hello past (for consuming historical data) or hello future (toodelay processing until a future time).</span></span> <span data-ttu-id="186b3-114">작업에 이전에 시작 / 중지 하는 경우 사례 hello 옵션에 대 한 **마지막으로 중지 된 시간** hello 마지막 출력 시간에서에서 tooresume hello 작업 순서에서에서 사용할 수 있으며 데이터가 손실 되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="186b3-114">For cases when a job has been previously started and stopped, hello option **Last Stopped Time** is available in order tooresume hello job from hello last output time and avoid data loss.</span></span>  
   
   ![스트리밍 작업 시작 시간](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Azure Portal 스트리밍 작업 시작 시간](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. <span data-ttu-id="186b3-117">선택을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="186b3-117">Confirm your selection.</span></span> <span data-ttu-id="186b3-118">작업 상태 hello도 변경 됩니다*시작* 너무 곧 들어왔다 및*실행* hello 작업이 시작 되 면입니다.</span><span class="sxs-lookup"><span data-stu-id="186b3-118">hello job status will change too*Starting* and will shortly move too*Running* once hello job has started.</span></span> <span data-ttu-id="186b3-119">Hello의 hello 진행률을 모니터링할 수 있습니다 **시작** hello에 대 한 작업 **알림 허브**:</span><span class="sxs-lookup"><span data-stu-id="186b3-119">You can monitor hello progress of hello **Start** operation in hello **Notification Hub**:</span></span>
   
   ![스트림 작업 진행률](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Azure Portal 스트리밍 작업 진행률](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="186b3-122">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="186b3-122">Get help</span></span>
<span data-ttu-id="186b3-123">추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="186b3-123">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="186b3-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="186b3-124">Next steps</span></span>
* [<span data-ttu-id="186b3-125">스트림 분석 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="186b3-125">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="186b3-126">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="186b3-126">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="186b3-127">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="186b3-127">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="186b3-128">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="186b3-128">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="186b3-129">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="186b3-129">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

