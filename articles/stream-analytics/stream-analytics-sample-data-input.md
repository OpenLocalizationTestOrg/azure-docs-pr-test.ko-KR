---
title: "Azure 스트림 분석을 위한 aaa 샘플링 입력 | Microsoft Docs"
description: "Stream Analytics 작업의 문제를 해결할 때 문제를 정확히 찾아냅니다."
keywords: "입력, 입력 샘플링 문제 해결"
documentationcenter: 
services: stream-analytics
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
ms.openlocfilehash: 9637a8664de099eebb8f5654036d2957f4c6b7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-input-stream-sampling"></a><span data-ttu-id="c0c1d-104">Azure Stream Analytics 입력 스트림 샘플링</span><span class="sxs-lookup"><span data-stu-id="c0c1d-104">Azure Stream Analytics input-stream sampling</span></span>

<span data-ttu-id="c0c1d-105">Azure Stream Analytics를 사용 하 여 toostart 필요 없이 hello 포털에서 쿼리를 테스트 또는 작업을 중지 하 고 파일에서 제공 하는 입력된 이벤트를 샘플링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c1d-105">By using Azure Stream Analytics, you can sample input events that come from a file and test queries in hello portal without needing toostart or stop a job.</span></span>

## <a name="testing-your-query"></a><span data-ttu-id="c0c1d-106">쿼리 테스트</span><span class="sxs-lookup"><span data-stu-id="c0c1d-106">Testing your query</span></span>

<span data-ttu-id="c0c1d-107">Hello 스트림 분석 작업 세부 정보 창에서 엽니다 hello **쿼리 편집기** 아래 hello 쿼리 이름을 클릭 하 여 블레이드 **쿼리**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c1d-107">In hello Stream Analytics job details pane, open hello **Query editor** blade by clicking hello query name under **Query**.</span></span> <span data-ttu-id="c0c1d-108">(예제 시나리오에서는 쿼리가 아직 생성 되었으므로 클릭 하 여 hello **< >** 자리 표시자입니다.)</span><span class="sxs-lookup"><span data-stu-id="c0c1d-108">(In our example scenario, because no query has been created yet, click hello **< >** placeholder.)</span></span>

![hello 스트림 분석 쿼리 편집기](media/stream-analytics-sample-data-input/stream-analytics-query-editor.png)

<span data-ttu-id="c0c1d-110">쿼리를 만들기 위한 풍부한 편집기 블레이드 hello hello 이전 버전에 포함 되어 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0c1d-110">hello rich editor blade for creating your query is displayed as it was in hello previous release.</span></span> <span data-ttu-id="c0c1d-111">해당 표시 hello 입 / 출력 하는 hello 쿼리에서 사용 하는이 작업에 대해 정의 된 hello 블레이드 새으로 업데이트 되었지만 이제 왼쪽 창입니다.</span><span class="sxs-lookup"><span data-stu-id="c0c1d-111">Now hello blade has been updated with a new left pane that shows hello inputs and outputs that are used by hello query and defined for this job.</span></span>

![hello 스트림 분석 쿼리 편집기는 입력 값과 출력 목록](media/stream-analytics-sample-data-input/stream-analytics-query-editor-highlight.png)

<span data-ttu-id="c0c1d-113">또한 정의되지 않은 추가 입력 및 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0c1d-113">Also shown are an additional input and output, which are not defined.</span></span> <span data-ttu-id="c0c1d-114">로 시작 하는 hello 새 쿼리 템플릿을에서 온 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c1d-114">They come from hello new query template that you start with.</span></span> <span data-ttu-id="c0c1d-115">이러한 변경 또는 심지어 hello 쿼리를 편집할 때 완전히 사라집니다.</span><span class="sxs-lookup"><span data-stu-id="c0c1d-115">They change, or even disappear altogether, as you edit hello query.</span></span> <span data-ttu-id="c0c1d-116">지금은 무시해도 무방합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c1d-116">You can safely ignore them for now.</span></span>

<span data-ttu-id="c0c1d-117">샘플 입력 데이터로 tootest 입력을 중 하나를 마우스 오른쪽 단추로 클릭 한 다음 선택 **파일에서 샘플 데이터 업로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c1d-117">tootest with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

![hello 스트림 분석 쿼리 편집기 샘플 데이터를에서 업로드 파일 명령](media/stream-analytics-sample-data-input/stream-analytics-query-editor-upload.png)

<span data-ttu-id="c0c1d-119">Hello 업로드가 완료 되 면 클릭 **테스트** tootest hello에 대해이 쿼리 예제 데이터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c1d-119">After hello upload is complete, click **Test** tootest this query against hello sample data you have just provided.</span></span>

![hello 스트림 분석 쿼리 편집기 테스트 단추](media/stream-analytics-sample-data-input/stream-analytics-query-editor-test.png)

<span data-ttu-id="c0c1d-121">나중에 사용할 toosave hello 테스트 출력을 원하는 경우 쿼리의 hello 출력 링크 toohello 다운로드 결과 사용 하 여 hello 브라우저에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0c1d-121">If you want toosave hello test output for later use, hello output of your query is displayed in hello browser with a link toohello download results.</span></span> <span data-ttu-id="c0c1d-122">이제 쉽고 반복적으로 쿼리를 수정 하 고 테스트할 수 것 반복 해 서 toosee 어떻게 변경 되는지 hello 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c1d-122">You can now easily and iteratively modify your query and test it repeatedly toosee how hello output changes.</span></span>

![Stream Analytics 쿼리 편집기 샘플 출력](media/stream-analytics-sample-data-input/stream-analytics-query-editor-samples-output.png)

<span data-ttu-id="c0c1d-124">Hello 이미지 앞에, 두 번째 출력 추가 되어, 호출 **HighAvgTempOutput**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c1d-124">In hello preceding image, a second output has been added, called **HighAvgTempOutput**.</span></span>

<span data-ttu-id="c0c1d-125">쿼리에서 여러 출력을 사용 하는 경우 각 출력에 대 한 hello 결과 개별적으로 볼 수 있으며 서로 쉽게 설정/해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c1d-125">When you use multiple outputs in a query, you can see hello results for each output separately and easily toggle between them.</span></span>

<span data-ttu-id="c0c1d-126">Hello 결과 만족 하는 후 쿼리 저장, 작업, 지켜봅니다을 시작한 스트림 분석의 hello 매직을 감시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c1d-126">After you are satisfied with hello results, you can save your query, start your job, sit back and watch hello magic of Stream Analytics.</span></span>

## <a name="get-help"></a><span data-ttu-id="c0c1d-127">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="c0c1d-127">Get help</span></span>

<span data-ttu-id="c0c1d-128">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c0c1d-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0c1d-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c0c1d-129">Next steps</span></span>
* [<span data-ttu-id="c0c1d-130">스트림 분석 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="c0c1d-130">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="c0c1d-131">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="c0c1d-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="c0c1d-132">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="c0c1d-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="c0c1d-133">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="c0c1d-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="c0c1d-134">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="c0c1d-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
