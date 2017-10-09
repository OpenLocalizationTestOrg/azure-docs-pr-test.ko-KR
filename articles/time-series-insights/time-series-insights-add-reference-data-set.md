---
title: "aaaAdd 참조 데이터 집합 tooyour Azure 시간 계열 Insights 환경 | Microsoft Docs"
description: "이 자습서에서는 참조 데이터 집합 tooyour 시간 계열 Insights 환경 추가"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: venkatja
ms.openlocfilehash: 05e626ed81a22f2a8710b23a931ccd17c0f38ca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a><span data-ttu-id="912e2-103">Hello Ibiza 포털을 사용 하 여 시간 시계열 Insights 환경에 대 한 참조 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="912e2-103">Create a reference data set for your Time Series Insights environment using hello Ibiza portal</span></span>

<span data-ttu-id="912e2-104">참조 데이터 집합은 이벤트 소스를 hello 이벤트와 보강 하는 항목의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="912e2-104">A Reference Data Set is a collection of items that are augmented with hello events from your event source.</span></span> <span data-ttu-id="912e2-105">Time Series Insights 수신 엔진은 이벤트 원본의 이벤트와 참조 데이터 집합의 항목을 조인합니다.</span><span class="sxs-lookup"><span data-stu-id="912e2-105">Time Series Insights ingress engine joins an event from your event source with an item in your reference data set.</span></span> <span data-ttu-id="912e2-106">이렇게 보강된 이벤트는 쿼리에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="912e2-106">This augmented event is then available for query.</span></span> <span data-ttu-id="912e2-107">이 조인은 참조 데이터 집합에 정의 된 hello 키를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="912e2-107">This join is based on hello keys defined in your reference data set.</span></span>

## <a name="steps-tooadd-a-reference-data-set-tooyour-environment"></a><span data-ttu-id="912e2-108">단계 tooadd 참조 데이터 집합 tooyour 환경</span><span class="sxs-lookup"><span data-stu-id="912e2-108">Steps tooadd a reference data set tooyour environment</span></span>

1. <span data-ttu-id="912e2-109">Toohello 로그인 [Ibiza 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="912e2-109">Sign in toohello [Ibiza portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="912e2-110">Hello hello Ibiza 포털의 왼쪽에 hello 메뉴에서 "모든 리소스"를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="912e2-110">Click “All resources” in hello menu on hello left side of hello Ibiza portal.</span></span>
3. <span data-ttu-id="912e2-111">Time Series Insights 환경을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="912e2-111">Select your Time Series Insights environment.</span></span>

    ![Hello 시간 계열 Insights 참조 데이터 집합 만들기](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. <span data-ttu-id="912e2-113">“참조 데이터 집합”을 선택하고, “+ 추가”를 합니다.</span><span class="sxs-lookup"><span data-stu-id="912e2-113">Select “Reference Data Sets”, click “+ Add.”</span></span>

    ![Hello 시간 계열 Insights 참조 데이터 집합 세부 정보 만들기](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. <span data-ttu-id="912e2-115">Hello hello 참조 데이터 집합 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="912e2-115">Specify hello name of hello reference data set.</span></span>
6. <span data-ttu-id="912e2-116">Hello 키 이름 및 해당 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="912e2-116">Specify hello key name and its type.</span></span> <span data-ttu-id="912e2-117">이 이름과 유형의 이벤트 소스에 hello 이벤트에서 사용 되는 toopick hello 올바른 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="912e2-117">This name and type is used toopick hello correct property from hello event in your event source.</span></span> <span data-ttu-id="912e2-118">예를 들어, 키 이름으로 "DeviceId"과 "String" 형식이 제공 하는 경우 시간 시계열 Insights 수신 엔진이 hello 들어오는 이벤트에 "String" 형식의 "DeviceId" hello 이름의 속성을 찾아 다음 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="912e2-118">For instance, if you provide key name as “DeviceId” and type as “String”, then hello Time Series Insights ingress engine looks for a property with hello name “DeviceId” of type “String” in hello incoming event.</span></span> <span data-ttu-id="912e2-119">Hello 이벤트와 둘 이상의 키 toojoin를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="912e2-119">You can provide more than one key toojoin with hello event.</span></span> <span data-ttu-id="912e2-120">일치 하는 hello 속성 이름이 대/소문자 구분입니다.</span><span class="sxs-lookup"><span data-stu-id="912e2-120">hello property name match is case-sensitive.</span></span>

     ![Hello 시간 계열 Insights 참조 데이터 집합 세부 정보 만들기](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. <span data-ttu-id="912e2-122">“만들기”를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="912e2-122">Click “Create.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="912e2-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="912e2-123">Next steps</span></span>

* <span data-ttu-id="912e2-124">프로그래밍 방식으로 [참조 데이터를 관리](time-series-insights-manage-reference-data-csharp.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="912e2-124">[Manage reference data](time-series-insights-manage-reference-data-csharp.md) programmatically.</span></span>
* <span data-ttu-id="912e2-125">Hello 전체 API 참조에 대 한 참조 [참조 데이터 API](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) 문서.</span><span class="sxs-lookup"><span data-stu-id="912e2-125">For hello complete API reference, see [Reference Data API](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) document.</span></span>
