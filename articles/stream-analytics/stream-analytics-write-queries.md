---
title: "Stream Analytics에서 쿼리를 작성 하는 방법 | Microsoft Docs"
description: "Stream Analytics 및 쿼리 데이터 | 학습 경로 세그먼트에서 쿼리를 작성합니다."
keywords: "쿼리를 작성하는 방법, 쿼리 데이터, 쿼리 작성, 쿼리 작성하기"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0e9cdadd-0ee0-4bee-b65b-4a06fb863c95
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: b44b0658a06761a805708e7fdeba9e3b2cf9d3ab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-write-queries-in-stream-analytics"></a><span data-ttu-id="9eaa4-104">Stream Analytics에서 쿼리를 작성하는 방법</span><span class="sxs-lookup"><span data-stu-id="9eaa4-104">How to write queries in Stream Analytics</span></span>
<span data-ttu-id="9eaa4-105">Azure Stream Analytics의 스트림 처리 논리에 대한 쿼리 작성은 작업이 시작되기 전에 정의되고 데이터가 작업에 도착할 때 실행되는 "고정 쿼리"로 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="9eaa4-105">Writing queries for stream processing logic in Azure Stream Analytics is implemented as a "standing query" that is defined before a job starts and executed on data as it reaches the job.</span></span> <span data-ttu-id="9eaa4-106">데이터 변환은 대체로 임시 의미 체계를 나타내는 데 사용되는 [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) 과 같은 언어 확장이 추가된 T-SQL의 하위 집합인, SQL과 유사한 쿼리 언어로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="9eaa4-106">The data transformation is expressed in a SQL-like query language, which is largely a subset of T-SQL with some added language extensions like [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) used to express temporal semantics.</span></span>

## <a name="writing-queries"></a><span data-ttu-id="9eaa4-107">쿼리 작성:</span><span class="sxs-lookup"><span data-stu-id="9eaa4-107">Writing Queries:</span></span>
1. <span data-ttu-id="9eaa4-108">Azure 관리 포털의 Stream Analytics 작업에서 **쿼리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9eaa4-108">In your Stream Analytics Job in the Azure Management portal, click **Query**.</span></span>
   
    ![쿼리 선택](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    <span data-ttu-id="9eaa4-110">Azure 포털에서 **쿼리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9eaa4-110">In the Azure Portal, click **Query**.</span></span>
   
    ![쿼리 선택 미리 보기](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. <span data-ttu-id="9eaa4-112">새 작업에는 시작하는 데 도움이 되는 쿼리 템플릿이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eaa4-112">New jobs have a query template to help get you started.</span></span> <span data-ttu-id="9eaa4-113">쿼리 템플릿은 입력 이벤트의 모든 필드를 출력에 프로젝션하는 "통과" 쿼리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9eaa4-113">The query template performs a "pass-through" query that projects all fields from input events into the output.</span></span>  
   
   * <span data-ttu-id="9eaa4-114">작업에 대해 입력 및 출력을 하나 이상 정의한 경우 자리 표시자 "[YourOutputAlias]" 및 "[YourInputAlias]" 필드를 먼저 사용하려는 입력 및 출력의 별칭으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eaa4-114">If you have defined at least one input and output for your job, you can replace the placeholder "[YourOutputAlias]" and "[YourInputAlias]" fields with the aliases of the input and output that you wish use first.</span></span> <span data-ttu-id="9eaa4-115">또한 작업에 입력 및 출력을 정의하지 않고 Azure 클래식 포털에서 쿼리를 작성 및 테스트할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eaa4-115">In addition, you can still author and test your query in the Azure Classic Portal without defining inputs and outputs on the job.</span></span>
   * <span data-ttu-id="9eaa4-116">단순한 통과보다 더 많은 처리를 수행하려는 경우 쿼리 정의를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eaa4-116">If you wish to perform more processing than a simple pass-through, you can edit the query definition.</span></span> <span data-ttu-id="9eaa4-117">쿼리 작성을 시작하려면 [여기](stream-analytics-stream-analytics-query-patterns.md)에 캡처된 몇 가지 일반적인 쿼리 패턴을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="9eaa4-117">To get started with query authoring, take a look at some common query patterns are captured [here](stream-analytics-stream-analytics-query-patterns.md).</span></span>  
   
   ![쿼리 데이터 창](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="to-validate-query-data-is-working"></a><span data-ttu-id="9eaa4-119">쿼리 데이터 작동의 유효성을 검사하려면</span><span class="sxs-lookup"><span data-stu-id="9eaa4-119">To validate query data is working:</span></span>
<span data-ttu-id="9eaa4-120">브라우저에서 테스트 데이터가 포함된 하나 이상의 로컬 JSON 파일에 대해 쿼리를 실행하여 쿼리가 예상대로 동작하는지 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eaa4-120">You can test that your query behaves as expected by running it in the browser over one or more local JSON files containing test data.</span></span> <span data-ttu-id="9eaa4-121">이 경우 작업이 시작되거나 요금이 청구되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9eaa4-121">This will not start the job or have any billing implications.</span></span>

> [!NOTE]
> <span data-ttu-id="9eaa4-122">현재 Azure 포털에서 브라우저 내 쿼리 테스트는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9eaa4-122">Currently in-browser query testing is not supported in the Azure Portal.</span></span>  
> 
> 

1. <span data-ttu-id="9eaa4-123">쿼리에 오류가 없는지 확인하고(오류가 있으면 테스트 단추를 사용할 수 없음) 테스트 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9eaa4-123">Make sure that there are no errors in the query (otherwise the Test button will be disabled) and then click the Test button.</span></span>  
   
   ![쿼리 데이터 테스트](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. <span data-ttu-id="9eaa4-125">쿼리에서 참조된 각 입력에 대해 파일을 지정하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9eaa4-125">You will be prompted to specify files for each of the inputs referenced in the query.</span></span> <span data-ttu-id="9eaa4-126">이 예제에서는 템플릿 쿼리가 그대로 유지되므로 "yourinputalias"라는 입력을 요청하는 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9eaa4-126">In this example, the template query is left as-is, so the dialog is prompting for an input named "yourinputalias".</span></span>  
   
   ![테스트 데이터 쿼리](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. <span data-ttu-id="9eaa4-128">테스트 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9eaa4-128">Browse to a test file.</span></span> <span data-ttu-id="9eaa4-129">[github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data)에서 여러 샘플 파일을 사용할 수 있으며, 입력 탭에서 Sample Data 함수를 통해 사용자 고유의 데이터 스트림 입력에서 샘플 데이터를 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eaa4-129">Several sample files are available on [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) and you can also retrieve sample data from your own data stream inputs via the Sample Data function on the inputs tab.</span></span>  
   
   ![쿼리 입력](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. <span data-ttu-id="9eaa4-131">대화 상자를 닫으면 테스트 데이터에 대해 쿼리가 실행되고 쿼리 페이지의 맨 아래에 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9eaa4-131">After closing the dialog, your query will be run over the test data and you will see the results at the bottom of the Query page.</span></span>  
   
   ![쿼리 요약](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a><span data-ttu-id="9eaa4-133">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="9eaa4-133">Get help</span></span>
<span data-ttu-id="9eaa4-134">추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="9eaa4-134">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="9eaa4-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9eaa4-135">Next steps</span></span>
* [<span data-ttu-id="9eaa4-136">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="9eaa4-136">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="9eaa4-137">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="9eaa4-137">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="9eaa4-138">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="9eaa4-138">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="9eaa4-139">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="9eaa4-139">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="9eaa4-140">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="9eaa4-140">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

