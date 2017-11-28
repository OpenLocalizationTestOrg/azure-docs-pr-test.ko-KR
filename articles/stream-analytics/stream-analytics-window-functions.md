---
title: "aaaIntroduction tooStream 분석 Window 함수 | Microsoft Docs"
description: "스트림 분석 (텀블 링, 도약, 슬라이딩) hello 세 창 함수에 알아봅니다."
keywords: "연속 창, 슬라이딩 윈도우, 도약 창"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0d8d8717-5d23-43f0-b475-af078ab4627d
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 7fc36eb9afb2b28e2791d925d26923145eb38074
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toostream-analytics-window-functions"></a><span data-ttu-id="09fba-104">소개 tooStream 분석 Window 함수</span><span class="sxs-lookup"><span data-stu-id="09fba-104">Introduction tooStream Analytics Window functions</span></span>
<span data-ttu-id="09fba-105">여러 실시간 스트리밍 시나리오에서에서 임시 windows에 포함 된 hello 데이터에만 필요한 tooperform 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="09fba-105">In many real time streaming scenarios, it is necessary tooperform operations only on hello data contained in temporal windows.</span></span> <span data-ttu-id="09fba-106">창 작업 기능에 대 한 기본 지원에 Azure 스트림 분석 작업을 처리 하는 복잡 한 스트림 제작에 대 한 개발자 생산성에 hello 니 들을 이동 하는 주요 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="09fba-106">Native support for windowing functions is a key feature of Azure Stream Analytics that moves hello needle on developer productivity in authoring complex stream processing jobs.</span></span> <span data-ttu-id="09fba-107">스트림 분석을 사용 하 개발자 toouse [ **텀블 링**](https://msdn.microsoft.com/library/dn835055.aspx), [ **도약** ](https://msdn.microsoft.com/library/dn835041.aspx) 및 [ **슬라이딩** ](https://msdn.microsoft.com/library/dn835051.aspx) 스트리밍 데이터에서 windows tooperform 임시 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="09fba-107">Stream Analytics enables developers toouse [**Tumbling**](https://msdn.microsoft.com/library/dn835055.aspx), [**Hopping**](https://msdn.microsoft.com/library/dn835041.aspx) and [**Sliding**](https://msdn.microsoft.com/library/dn835051.aspx) windows tooperform temporal operations on streaming data.</span></span> <span data-ttu-id="09fba-108">주목할 하는 모든 [창](https://msdn.microsoft.com/library/dn835019.aspx) hello에 대 한 결과 출력 하는 작업 **끝** hello 창.</span><span class="sxs-lookup"><span data-stu-id="09fba-108">It is worth noting that all [Window](https://msdn.microsoft.com/library/dn835019.aspx) operations output results at hello **end** of hello window.</span></span> <span data-ttu-id="09fba-109">hello 창의 hello 출력을 사용 하는 hello 집계 함수에 기반 하 여 단일 이벤트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09fba-109">hello output of hello window will be single event based on hello aggregate function used.</span></span> <span data-ttu-id="09fba-110">hello 이벤트 hello 창의 hello 끝의 타임 스탬프 hello 있고 길이가 고정된 된 모든 창 함수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="09fba-110">hello event will have hello time stamp of hello end of hello window and all Window functions are defined with a fixed length.</span></span> <span data-ttu-id="09fba-111">중요 한 toonote에 모든 창 함수를 사용 해야 하는 마지막으로 [ **GROUP BY** ](https://msdn.microsoft.com/library/dn835023.aspx) 절.</span><span class="sxs-lookup"><span data-stu-id="09fba-111">Lastly it is important toonote that all Window functions should be used in a [**GROUP BY**](https://msdn.microsoft.com/library/dn835023.aspx) clause.</span></span>

![Stream Analytics 창 함수 개념](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a><span data-ttu-id="09fba-113">연속 창</span><span class="sxs-lookup"><span data-stu-id="09fba-113">Tumbling Window</span></span>
<span data-ttu-id="09fba-114">텀블 링 창 함수 사용 되는 toosegment 서로 다른 시간 세그먼트에 데이터 스트림이 되며 hello 감시할 같이,에 대 한 기능을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="09fba-114">Tumbling window functions are used toosegment a data stream into distinct time segments and perform a function against them, such as hello example below.</span></span> <span data-ttu-id="09fba-115">연속 창의 요소가 한 hello 핵심적인 차이점은은 반복 있음을, 겹치지 않고 및 이벤트에는 하나의 연속 창 보다 toomore 속할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="09fba-115">hello key differentiators of a Tumbling window are that they repeat, do not overlap and an event cannot belong toomore than one tumbling window.</span></span>

![Stream Analytics 창 함수 연속 소개](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a><span data-ttu-id="09fba-117">도약 창</span><span class="sxs-lookup"><span data-stu-id="09fba-117">Hopping Window</span></span>
<span data-ttu-id="09fba-118">도약 창 함수는 고정된 기간만큼 시간을 앞으로 건너 뜁니다.</span><span class="sxs-lookup"><span data-stu-id="09fba-118">Hopping window functions hop forward in time by a fixed period.</span></span> <span data-ttu-id="09fba-119">이벤트는 도약 창 결과 집합이 두 개 보다 toomore 속할 수 있으므로 겹칠 수 있는 연속 창으로 쉽게 toothink 그중에서 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09fba-119">It may be easy toothink of them as Tumbling windows that can overlap, so events can belong toomore than one Hopping window result set.</span></span> <span data-ttu-id="09fba-120">도약 창 toomake 동일 하나는 지정 하면 연속 창으로 hello hello 도약 크기 toobe hello hello 창 크기와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="09fba-120">toomake a Hopping window hello same as a Tumbling window one would simply specify hello hop size toobe hello same as hello window size.</span></span> 

![Stream Analytics 창 함수 도약 소개](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a><span data-ttu-id="09fba-122">슬라이딩 윈도우</span><span class="sxs-lookup"><span data-stu-id="09fba-122">Sliding Window</span></span>
<span data-ttu-id="09fba-123">연속 또는 도약 창과 달리 슬라이딩 윈도우 함수는 이벤트가 발생할 때 출력 **만** 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="09fba-123">Sliding window functions, unlike Tumbling or Hopping windows, produce an output **only**  when an event occurs.</span></span> <span data-ttu-id="09fba-124">모든 창 하나 이상의 이벤트에 있고 hello 창은 € (엡실론) 하 여 앞으로 지속적으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="09fba-124">Every window will have at least one event and hello window continuously moves forward by an € (epsilon).</span></span> <span data-ttu-id="09fba-125">도약 창과 마찬가지로 이벤트에는 하나의 슬라이딩 윈도우 보다 toomore를 속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09fba-125">Like Hopping Windows, events can belong toomore than one Sliding Window.</span></span>

![Stream Analytics 창 함수 슬라이딩 소개](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a><span data-ttu-id="09fba-127">창 함수 관련 도움말 보기</span><span class="sxs-lookup"><span data-stu-id="09fba-127">Getting help with Window functions</span></span>
<span data-ttu-id="09fba-128">추가 지원이 필요할 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="09fba-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="09fba-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="09fba-129">Next steps</span></span>
* [<span data-ttu-id="09fba-130">스트림 분석 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="09fba-130">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="09fba-131">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="09fba-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="09fba-132">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="09fba-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="09fba-133">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="09fba-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="09fba-134">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="09fba-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

