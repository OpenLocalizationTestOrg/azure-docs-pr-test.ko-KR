---
title: "스트림 분석에서 aaaHow toowrite 쿼리 | Microsoft Docs"
description: "Stream Analytics 및 쿼리 데이터 | 학습 경로 세그먼트에서 쿼리를 작성합니다."
keywords: "toowrite 쿼리, 데이터를 쿼리하거나, 쿼리를 작성 하는 쿼리를 작성 하는 방법"
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
ms.openlocfilehash: b943c34f10afd2b21789afbd341c471a5f168729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowrite-queries-in-stream-analytics"></a><span data-ttu-id="e23bd-104">스트림 분석의 toowrite 쿼리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="e23bd-104">How toowrite queries in Stream Analytics</span></span>
<span data-ttu-id="e23bd-105">Azure 스트림 분석에서 논리를 처리 하는 스트림에 대 한 쿼리를 작성 하는 쿼리로"고정" 작업을 시작 하 고 hello 작업에 도달할 때 데이터에서 실행 하기 전에 정의 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e23bd-105">Writing queries for stream processing logic in Azure Stream Analytics is implemented as a "standing query" that is defined before a job starts and executed on data as it reaches hello job.</span></span> <span data-ttu-id="e23bd-106">hello 데이터 변환 SQL 방식 쿼리 언어는 단위로 같은 언어 확장을 추가 주로 하위 집합인 T-SQL의 일부와 [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) tooexpress 임시 의미 체계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e23bd-106">hello data transformation is expressed in a SQL-like query language, which is largely a subset of T-SQL with some added language extensions like [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) used tooexpress temporal semantics.</span></span>

## <a name="writing-queries"></a><span data-ttu-id="e23bd-107">쿼리 작성:</span><span class="sxs-lookup"><span data-stu-id="e23bd-107">Writing Queries:</span></span>
1. <span data-ttu-id="e23bd-108">스트림 분석 hello Azure 관리 포털에서 작업을 클릭 **쿼리**합니다.</span><span class="sxs-lookup"><span data-stu-id="e23bd-108">In your Stream Analytics Job in hello Azure Management portal, click **Query**.</span></span>
   
    ![쿼리 선택](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    <span data-ttu-id="e23bd-110">Hello Azure 포털에서에서 클릭 **쿼리**합니다.</span><span class="sxs-lookup"><span data-stu-id="e23bd-110">In hello Azure Portal, click **Query**.</span></span>
   
    ![쿼리 선택 미리 보기](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. <span data-ttu-id="e23bd-112">새 작업을 시작 하는 쿼리 템플릿 toohelp을 서로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23bd-112">New jobs have a query template toohelp get you started.</span></span> <span data-ttu-id="e23bd-113">서식 파일 "통과"을 수행 하는 hello 쿼리 프로젝트는 입력된 이벤트의 모든 필드가 hello 출력으로 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e23bd-113">hello query template performs a "pass-through" query that projects all fields from input events into hello output.</span></span>  
   
   * <span data-ttu-id="e23bd-114">작업에 대 한 입력 및 출력을 하나 이상 정의한 경우 hello 자리 표시자 "[YourOutputAlias]" 및 "[YourInputAlias]" 필드의 입력 및 출력 처음 사용 하 여 원하는 hello hello 별칭으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23bd-114">If you have defined at least one input and output for your job, you can replace hello placeholder "[YourOutputAlias]" and "[YourInputAlias]" fields with hello aliases of hello input and output that you wish use first.</span></span> <span data-ttu-id="e23bd-115">또한 여전히 작성 고 hello 작업에서 입력 및 출력을 정의 하지 않고 hello Azure 클래식 포털에서에서 쿼리를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23bd-115">In addition, you can still author and test your query in hello Azure Classic Portal without defining inputs and outputs on hello job.</span></span>
   * <span data-ttu-id="e23bd-116">간단한 통과 보다 더 많은 처리가 tooperform을 원할 경우 hello 쿼리 정의 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23bd-116">If you wish tooperform more processing than a simple pass-through, you can edit hello query definition.</span></span> <span data-ttu-id="e23bd-117">쿼리를 작성 작업을 시작 하는 tooget 패턴 캡처됩니다 몇 가지 일반적인 쿼리 살펴보세요 [여기](stream-analytics-stream-analytics-query-patterns.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e23bd-117">tooget started with query authoring, take a look at some common query patterns are captured [here](stream-analytics-stream-analytics-query-patterns.md).</span></span>  
   
   ![쿼리 데이터 창](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="toovalidate-query-data-is-working"></a><span data-ttu-id="e23bd-119">데이터를 쿼리 하는 toovalidate 작동:</span><span class="sxs-lookup"><span data-stu-id="e23bd-119">toovalidate query data is working:</span></span>
<span data-ttu-id="e23bd-120">쿼리 하나 이상의 로컬 JSON 파일에서 테스트 데이터가 포함 된 hello 브라우저에서 실행 하 여 예상한 대로 작동 하는지 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23bd-120">You can test that your query behaves as expected by running it in hello browser over one or more local JSON files containing test data.</span></span> <span data-ttu-id="e23bd-121">Hello 작업을 시작 되거나 청구를 나타내는 것 되지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e23bd-121">This will not start hello job or have any billing implications.</span></span>

> [!NOTE]
> <span data-ttu-id="e23bd-122">현재 브라우저에서 쿼리 테스트 hello Azure 포털에서에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e23bd-122">Currently in-browser query testing is not supported in hello Azure Portal.</span></span>  
> 
> 

1. <span data-ttu-id="e23bd-123">(그렇지 않으면 hello 테스트 단추가 비활성화 됩니다) hello 쿼리에서 오류가 없는지 확인 다음 hello 테스트 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e23bd-123">Make sure that there are no errors in hello query (otherwise hello Test button will be disabled) and then click hello Test button.</span></span>  
   
   ![쿼리 데이터 테스트](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. <span data-ttu-id="e23bd-125">각 hello 쿼리에서 참조 하는 hello 입력에 대 한 증명된 toospecify 파일 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e23bd-125">You will be prompted toospecify files for each of hello inputs referenced in hello query.</span></span> <span data-ttu-id="e23bd-126">이 예제에서는 hello 템플릿 쿼리 그대로 유지 되므로-이므로, "yourinputalias" 이라는 입력에 사용 하는 hello 대화에서 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e23bd-126">In this example, hello template query is left as-is, so hello dialog is prompting for an input named "yourinputalias".</span></span>  
   
   ![테스트 데이터 쿼리](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. <span data-ttu-id="e23bd-128">Tooa 테스트 파일을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e23bd-128">Browse tooa test file.</span></span> <span data-ttu-id="e23bd-129">몇 가지 샘플 파일에서 사용할 수 있는 [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) 및 hello hello 입력 탭에서 예제 데이터 함수를 통해 사용자 고유의 데이터 스트림 입력에서 샘플 데이터를 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23bd-129">Several sample files are available on [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) and you can also retrieve sample data from your own data stream inputs via hello Sample Data function on hello inputs tab.</span></span>  
   
   ![쿼리 입력](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. <span data-ttu-id="e23bd-131">Hello 대화 상자를 닫은 후에 쿼리 hello 테스트 데이터에 대해 실행 되 고 hello 결과가 hello hello 쿼리 페이지 맨 아래에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e23bd-131">After closing hello dialog, your query will be run over hello test data and you will see hello results at hello bottom of hello Query page.</span></span>  
   
   ![쿼리 요약](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a><span data-ttu-id="e23bd-133">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="e23bd-133">Get help</span></span>
<span data-ttu-id="e23bd-134">추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="e23bd-134">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e23bd-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e23bd-135">Next steps</span></span>
* [<span data-ttu-id="e23bd-136">스트림 분석 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="e23bd-136">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="e23bd-137">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="e23bd-137">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="e23bd-138">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="e23bd-138">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="e23bd-139">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="e23bd-139">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="e23bd-140">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="e23bd-140">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

