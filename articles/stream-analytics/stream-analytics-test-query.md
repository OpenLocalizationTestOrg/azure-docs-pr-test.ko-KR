---
title: "Azure Stream Analytics 쿼리 테스트 | Microsoft Docs"
description: "Stream Analytics 작업에서 쿼리를 테스트하는 방법"
keywords: "쿼리 테스트, 쿼리 문제 해결"
documentation center: 
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
ms.openlocfilehash: 16bb3f26ec3a69e5204162db9e54a186cf1ec6a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="test-azure-stream-analytics-queries-in-the-azure-portal"></a><span data-ttu-id="6e3f0-104">Azure Portal에서 Azure Stream Analytics 쿼리 테스트</span><span class="sxs-lookup"><span data-stu-id="6e3f0-104">Test Azure Stream Analytics queries in the Azure portal</span></span>

<span data-ttu-id="6e3f0-105">Azure Stream Analytics를 사용하면 작업을 시작하거나 중지하지 않고도 Azure Portal에서 쿼리를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e3f0-105">With Azure Stream Analytics, you can test queries in the Azure portal without needing to start or stop a job.</span></span>

## <a name="test-the-input"></a><span data-ttu-id="6e3f0-106">입력 테스트</span><span class="sxs-lookup"><span data-stu-id="6e3f0-106">Test the input</span></span>

1. <span data-ttu-id="6e3f0-107">샘플 입력 데이터를 테스트하려면 사용자 입력 중 하나를 마우스 오른쪽 단추로 클릭한 다음 **파일에서 샘플 데이터 업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e3f0-107">To test with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

    ![Stream Analytics 쿼리 편집기 쿼리 테스트](media/stream-analytics-test-query/stream-analytics-test-query-editor-upload.png)

2. <span data-ttu-id="6e3f0-109">업로드가 완료되면 **테스트**를 클릭하여 입력한 샘플 데이터에 대해 이 쿼리를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="6e3f0-109">After the upload is complete, click **Test** to test this query against the sample data you have provided.</span></span>

    ![Stream Analytics 쿼리 편집기 샘플 데이터 테스트](media/stream-analytics-test-query/stream-analytics-test-query-editor-test.png)

<span data-ttu-id="6e3f0-111">나중에 사용하기 위해 테스트 출력을 저장하려는 경우 사용자 쿼리의 출력이 다운로드 결과 링크와 함께 브라우저에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e3f0-111">The output of your query is displayed in the browser, with Download results link should you want to save the test output for later use.</span></span> <span data-ttu-id="6e3f0-112">이제 쉽고 반복적으로 쿼리를 수정하고 반복적으로 테스트하여 출력이 어떻게 변화하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e3f0-112">You can now easily and iteratively modify your query and test it repeatedly to see how the output changes.</span></span>

![Stream Analytics 쿼리 편집기 샘플 출력](media/stream-analytics-test-query/stream-analytics-test-query-editor-samples-output.png)

<span data-ttu-id="6e3f0-114">쿼리에서 사용된 여러 출력을 통해 두 출력에 대한 결과를 개별적으로 볼 수 있으며 서로 쉽게 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e3f0-114">With multiple outputs used in a query, you can see the results for both outputs separately and easily toggle between them.</span></span>

<span data-ttu-id="6e3f0-115">브라우저에 표시된 결과에 만족한다면 쿼리를 저장하고, 작업을 시작하여 오류 없이 이벤트를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e3f0-115">After you are satisfied with the results shown in the browser, you can save your query, start your job, and let it process events without error.</span></span>

## <a name="get-help"></a><span data-ttu-id="6e3f0-116">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="6e3f0-116">Get help</span></span>

<span data-ttu-id="6e3f0-117">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6e3f0-117">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e3f0-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6e3f0-118">Next steps</span></span>

* [<span data-ttu-id="6e3f0-119">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="6e3f0-119">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="6e3f0-120">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="6e3f0-120">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="6e3f0-121">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="6e3f0-121">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="6e3f0-122">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="6e3f0-122">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="6e3f0-123">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="6e3f0-123">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
