---
title: "Azure Stream Analytics의 입력 샘플링 | Microsoft Docs"
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
ms.openlocfilehash: 0bb66090b5025d57f5ca8f30713aef4e444fa8e7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-stream-analytics-input-stream-sampling"></a><span data-ttu-id="fe41b-104">Azure Stream Analytics 입력 스트림 샘플링</span><span class="sxs-lookup"><span data-stu-id="fe41b-104">Azure Stream Analytics input-stream sampling</span></span>

<span data-ttu-id="fe41b-105">Azure Stream Analytics를 사용하면 작업을 시작 또는 중지할 필요 없이 파일에서 제공하는 입력 이벤트를 샘플링하고, 포털에서 쿼리를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe41b-105">By using Azure Stream Analytics, you can sample input events that come from a file and test queries in the portal without needing to start or stop a job.</span></span>

## <a name="testing-your-query"></a><span data-ttu-id="fe41b-106">쿼리 테스트</span><span class="sxs-lookup"><span data-stu-id="fe41b-106">Testing your query</span></span>

<span data-ttu-id="fe41b-107">Stream Analytics 작업 세부 정보 창에서 **쿼리** 아래에 있는 쿼리 이름을 클릭하여 **쿼리 편집기** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fe41b-107">In the Stream Analytics job details pane, open the **Query editor** blade by clicking the query name under **Query**.</span></span> <span data-ttu-id="fe41b-108">(예제 시나리오에서는 쿼리가 아직 생성되지 않았으므로 **< >** 자리 표시자를 클릭합니다.)</span><span class="sxs-lookup"><span data-stu-id="fe41b-108">(In our example scenario, because no query has been created yet, click the **< >** placeholder.)</span></span>

![Stream Analytics 쿼리 편집기](media/stream-analytics-sample-data-input/stream-analytics-query-editor.png)

<span data-ttu-id="fe41b-110">이전 릴리스에서와 마찬가지로 쿼리를 만들기 위한 다양한 편집기 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe41b-110">The rich editor blade for creating your query is displayed as it was in the previous release.</span></span> <span data-ttu-id="fe41b-111">이제 쿼리에 사용되고 이 작업에 대해 정의된 입력 및 출력을 보여 주는 새로운 왼쪽 창으로 블레이드가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe41b-111">Now the blade has been updated with a new left pane that shows the inputs and outputs that are used by the query and defined for this job.</span></span>

![Stream Analytics 쿼리 편집기 입력 및 출력 목록](media/stream-analytics-sample-data-input/stream-analytics-query-editor-highlight.png)

<span data-ttu-id="fe41b-113">또한 정의되지 않은 추가 입력 및 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe41b-113">Also shown are an additional input and output, which are not defined.</span></span> <span data-ttu-id="fe41b-114">이는 시작할 때 사용하는 새 쿼리 템플릿에서 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fe41b-114">They come from the new query template that you start with.</span></span> <span data-ttu-id="fe41b-115">사용자가 쿼리를 편집함에 따라 변경되거나 심지어 완전히 사라집니다.</span><span class="sxs-lookup"><span data-stu-id="fe41b-115">They change, or even disappear altogether, as you edit the query.</span></span> <span data-ttu-id="fe41b-116">지금은 무시해도 무방합니다.</span><span class="sxs-lookup"><span data-stu-id="fe41b-116">You can safely ignore them for now.</span></span>

<span data-ttu-id="fe41b-117">샘플 입력 데이터를 테스트하려면 사용자 입력 중 하나를 마우스 오른쪽 단추로 클릭한 다음 **파일에서 샘플 데이터 업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fe41b-117">To test with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

![Stream Analytics 쿼리 편집기 파일에서 샘플 데이터 업로드 명령](media/stream-analytics-sample-data-input/stream-analytics-query-editor-upload.png)

<span data-ttu-id="fe41b-119">업로드가 완료되면 **테스트**를 클릭하여 방금 입력한 샘플 데이터에 대해 이 쿼리를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="fe41b-119">After the upload is complete, click **Test** to test this query against the sample data you have just provided.</span></span>

![Stream Analytics 쿼리 편집기 테스트 단추](media/stream-analytics-sample-data-input/stream-analytics-query-editor-test.png)

<span data-ttu-id="fe41b-121">나중에 사용하기 위해 테스트 출력을 저장하려는 경우 사용자 쿼리의 출력이 다운로드 결과에 대한 링크와 함께 브라우저에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe41b-121">If you want to save the test output for later use, the output of your query is displayed in the browser with a link to the download results.</span></span> <span data-ttu-id="fe41b-122">이제 쉽고 반복적으로 쿼리를 수정하고 반복적으로 테스트하여 출력이 어떻게 변화하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe41b-122">You can now easily and iteratively modify your query and test it repeatedly to see how the output changes.</span></span>

![Stream Analytics 쿼리 편집기 샘플 출력](media/stream-analytics-sample-data-input/stream-analytics-query-editor-samples-output.png)

<span data-ttu-id="fe41b-124">위 이미지에서 **HighAvgTempOutput**이라는 두 번째 출력이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fe41b-124">In the preceding image, a second output has been added, called **HighAvgTempOutput**.</span></span>

<span data-ttu-id="fe41b-125">쿼리에서 여러 출력을 사용하면 각 출력에 대한 결과를 개별적으로 볼 수 있으며 서로 쉽게 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe41b-125">When you use multiple outputs in a query, you can see the results for each output separately and easily toggle between them.</span></span>

<span data-ttu-id="fe41b-126">결과에 만족한다면 쿼리를 저장하고, 작업을 시작하고, 앉아서 Stream Analytics의 마법을 지켜볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe41b-126">After you are satisfied with the results, you can save your query, start your job, sit back and watch the magic of Stream Analytics.</span></span>

## <a name="get-help"></a><span data-ttu-id="fe41b-127">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="fe41b-127">Get help</span></span>

<span data-ttu-id="fe41b-128">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe41b-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe41b-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fe41b-129">Next steps</span></span>
* [<span data-ttu-id="fe41b-130">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="fe41b-130">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="fe41b-131">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="fe41b-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="fe41b-132">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="fe41b-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="fe41b-133">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="fe41b-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="fe41b-134">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="fe41b-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
