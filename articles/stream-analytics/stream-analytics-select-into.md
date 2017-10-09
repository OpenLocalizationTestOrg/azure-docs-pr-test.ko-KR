---
title: "SELECT INTO를 사용 하 여 aaaDebug Azure 스트림 분석 쿼리 | Microsoft Docs"
description: "Stream Analytics에서 SELECT INTO 문을 사용한 샘플 데이터 중간 쿼리"
keywords: 
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 27e41af1a6ea06b4509d07a3a67087490d0ec1fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a><span data-ttu-id="a8cfa-103">SELECT INTO 문을 사용하여 쿼리 디버그</span><span class="sxs-lookup"><span data-stu-id="a8cfa-103">Debug queries by using SELECT INTO statements</span></span>

<span data-ttu-id="a8cfa-104">실시간 데이터 처리에 hello 데이터를 알 같습니다. hello의 hello 중간 쿼리 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8cfa-104">In real-time data processing, knowing what hello data looks like in hello middle of hello query can be helpful.</span></span> <span data-ttu-id="a8cfa-105">Azure Stream Analytics 작업의 입력 또는 단계를 여러 번 읽을 수 있기 때문에 추가 SELECT INTO 문을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8cfa-105">Because inputs or steps of an Azure Stream Analytics job can be read multiple times, you can write extra SELECT INTO statements.</span></span> <span data-ttu-id="a8cfa-106">이렇게 중간 데이터 저장소에 출력 되 고 마찬가지로 hello 데이터의 hello 정확성을 검사할 수 있습니다 *변수를 조사할* 않습니다를 디버그할 때 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="a8cfa-106">Doing so outputs intermediate data into storage and lets you inspect hello correctness of hello data, just as *watch variables* do when you debug a program.</span></span>

## <a name="use-select-into-toocheck-hello-data-stream"></a><span data-ttu-id="a8cfa-107">Toocheck hello 데이터 스트림을 SELECT INTO 사용</span><span class="sxs-lookup"><span data-stu-id="a8cfa-107">Use SELECT INTO toocheck hello data stream</span></span>

<span data-ttu-id="a8cfa-108">hello Azure Stream Analytics 작업에서 다음 예제 쿼리에서 하나의 스트림 입력, 두 개의 참조 데이터 입력 및 출력 tooAzure 테이블 저장소 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8cfa-108">hello following example query in an Azure Stream Analytics job has one stream input, two reference data inputs, and an output tooAzure Table Storage.</span></span> <span data-ttu-id="a8cfa-109">hello 이벤트 허브 및 두 개의 참조는 blob tooget hello 이름 및 범주 정보 데이터를 조인 하는 hello 쿼리:</span><span class="sxs-lookup"><span data-stu-id="a8cfa-109">hello query joins data from hello event hub and two reference blobs tooget hello name and category information:</span></span>

![SELECT INTO 쿼리 예제](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

<span data-ttu-id="a8cfa-111">Note hello 작업이 실행 되 고 있지만 hello 출력에서 생성 되는 이벤트가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8cfa-111">Note that hello job is running, but no events are being produced in hello output.</span></span> <span data-ttu-id="a8cfa-112">Hello에 **모니터링** hello 입력 데이터를 생성 하지만 hello의 단계를 알 수 없는 볼 수는 여기에 표시 된 타일 **조인** 삭제 이벤트 toobe hello 모두 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8cfa-112">On hello **Monitoring** tile, shown here, you can see that hello input is producing data, but you don’t know which step of hello **JOIN** caused all hello events toobe dropped.</span></span>

![hello 모니터링 타일](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
<span data-ttu-id="a8cfa-114">이 경우 몇 가지 추가 SELECT INTO 문의 너무 "로그인" hello 중간 조인 결과 hello 입력에서 읽은 hello 데이터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8cfa-114">In this situation, you can add a few extra SELECT INTO statements too“log” hello intermediate JOIN results and hello data that's read from hello input.</span></span>

<span data-ttu-id="a8cfa-115">이 예제에서는 두 개의 새로운 “임시 출력”을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="a8cfa-115">In this example, we've added two new “temporary outputs.”</span></span> <span data-ttu-id="a8cfa-116">사용자가 원하는 어떠한 싱크도 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8cfa-116">They can be any sink you like.</span></span> <span data-ttu-id="a8cfa-117">여기서는 Azure Storage를 예로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a8cfa-117">Here we use Azure Storage as an example:</span></span>

![추가 SELECT INTO 문 추가](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

<span data-ttu-id="a8cfa-119">그런 다음 다음과 같은 hello 쿼리를 다시 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8cfa-119">You can then rewrite hello query like this:</span></span>

![SELECT INTO 쿼리 다시 작성](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

<span data-ttu-id="a8cfa-121">이제 hello 작업을 다시 시작 하 고 몇 분 동안 실행 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8cfa-121">Now start hello job again, and let it run for a few minutes.</span></span> <span data-ttu-id="a8cfa-122">다음 표에서 Visual Studio 클라우드 탐색기 tooproduce hello로 temp1 및 temp2을 쿼리 한 다음:</span><span class="sxs-lookup"><span data-stu-id="a8cfa-122">Then query temp1 and temp2 with Visual Studio Cloud Explorer tooproduce hello following tables:</span></span>

<span data-ttu-id="a8cfa-123">**temp1 테이블**
![SELECT INTO temp1 테이블](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span><span class="sxs-lookup"><span data-stu-id="a8cfa-123">**temp1 table**
![SELECT INTO temp1 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span></span>

<span data-ttu-id="a8cfa-124">**temp2 테이블**
![SELECT INTO temp2 테이블](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span><span class="sxs-lookup"><span data-stu-id="a8cfa-124">**temp2 table**
![SELECT INTO temp2 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span></span>

<span data-ttu-id="a8cfa-125">볼 수 있듯이 temp1 및 temp2 데이터가 있고 고 hello 이름 열에서 temp2 올바르게 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="a8cfa-125">As you can see, temp1 and temp2 both have data, and hello name column is populated correctly in temp2.</span></span> <span data-ttu-id="a8cfa-126">그러나 여전히 출력에 데이터가 없기 때문에 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8cfa-126">However, because there is still no data in output, something is wrong:</span></span>

![데이터가 없는 SELECT INTO output1 테이블](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

<span data-ttu-id="a8cfa-128">Hello 데이터를 샘플링 하 여 제어할 수 있습니다 거의 hello로 hello 문제 인지 조인의 두 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="a8cfa-128">By sampling hello data, you can be almost certain that hello issue is with hello second JOIN.</span></span> <span data-ttu-id="a8cfa-129">Hello blob에서 hello 참조 데이터를 다운로드 하 고 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8cfa-129">You can download hello reference data from hello blob and take a look:</span></span>

![SELECT INTO 참조 테이블](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

<span data-ttu-id="a8cfa-131">볼 수 있듯이 hello이 참조 데이터에 hello GUID 형식이 hello 형식의 [temp2의 열에서] hello와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="a8cfa-131">As you can see, hello format of hello GUID in this reference data is different from hello format of hello [from] column in temp2.</span></span> <span data-ttu-id="a8cfa-132">바로 이러한 이유로 예상 대로 hello 데이터 output1에 도착 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="a8cfa-132">That’s why hello data didn’t arrive in output1 as expected.</span></span>

<span data-ttu-id="a8cfa-133">Hello 데이터 형식을 수정 지정, tooreference blob을 업로드 및 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a8cfa-133">You can fix hello data format, upload it tooreference blob, and try again:</span></span>

![SELECT INTO 임시 테이블](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

<span data-ttu-id="a8cfa-135">이 시간 hello의에서 데이터가 hello 출력 형식이 지정 되어 예상 대로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="a8cfa-135">This time, hello data in hello output is formatted and populated as expected.</span></span>

![SELECT INTO 최종 테이블](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a><span data-ttu-id="a8cfa-137">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="a8cfa-137">Get help</span></span>

<span data-ttu-id="a8cfa-138">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8cfa-138">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8cfa-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a8cfa-139">Next steps</span></span>

* [<span data-ttu-id="a8cfa-140">스트림 분석 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="a8cfa-140">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="a8cfa-141">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="a8cfa-141">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="a8cfa-142">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="a8cfa-142">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="a8cfa-143">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="a8cfa-143">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="a8cfa-144">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="a8cfa-144">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

