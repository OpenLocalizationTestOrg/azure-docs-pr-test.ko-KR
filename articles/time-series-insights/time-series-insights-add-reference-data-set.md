---
title: "Azure Time Series Insights 환경에 참조 데이터 집합 추가 | Microsoft Docs"
description: "이 자습서에서는 Time Series Insights 환경에 참조 데이터 집합을 추가합니다."
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
ms.openlocfilehash: 23444297b5231e6a026bcd9ce3ee9f943bf05867
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-the-ibiza-portal"></a><span data-ttu-id="c7649-103">Ibiza 포털을 사용하여 Time Series Insights 환경에 대한 참조 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="c7649-103">Create a reference data set for your Time Series Insights environment using the Ibiza portal</span></span>

<span data-ttu-id="c7649-104">참조 데이터 집합은 이벤트 원본의 이벤트로 보강된 항목의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="c7649-104">A Reference Data Set is a collection of items that are augmented with the events from your event source.</span></span> <span data-ttu-id="c7649-105">Time Series Insights 수신 엔진은 이벤트 원본의 이벤트와 참조 데이터 집합의 항목을 조인합니다.</span><span class="sxs-lookup"><span data-stu-id="c7649-105">Time Series Insights ingress engine joins an event from your event source with an item in your reference data set.</span></span> <span data-ttu-id="c7649-106">이렇게 보강된 이벤트는 쿼리에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7649-106">This augmented event is then available for query.</span></span> <span data-ttu-id="c7649-107">이 조인은 참조 데이터 집합에서 정의된 키를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7649-107">This join is based on the keys defined in your reference data set.</span></span>

## <a name="steps-to-add-a-reference-data-set-to-your-environment"></a><span data-ttu-id="c7649-108">환경에 참조 데이터 집합을 추가하는 단계</span><span class="sxs-lookup"><span data-stu-id="c7649-108">Steps to add a reference data set to your environment</span></span>

1. <span data-ttu-id="c7649-109">[Ibiza portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c7649-109">Sign in to the [Ibiza portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c7649-110">Ibiza 포털의 왼쪽에 있는 메뉴에서 “All resources(모든 리소스)”를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7649-110">Click “All resources” in the menu on the left side of the Ibiza portal.</span></span>
3. <span data-ttu-id="c7649-111">Time Series Insights 환경을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7649-111">Select your Time Series Insights environment.</span></span>

    ![Time Series Insights 참조 데이터 집합 만들기](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. <span data-ttu-id="c7649-113">“참조 데이터 집합”을 선택하고, “+ 추가”를 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7649-113">Select “Reference Data Sets”, click “+ Add.”</span></span>

    ![Time Series Insights 참조 데이터 집합 만들기 - 세부 정보](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. <span data-ttu-id="c7649-115">참조 데이터 집합의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c7649-115">Specify the name of the reference data set.</span></span>
6. <span data-ttu-id="c7649-116">키 이름과 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c7649-116">Specify the key name and its type.</span></span> <span data-ttu-id="c7649-117">이 이름과 형식은 이벤트 원본의 이벤트에서 올바른 속성을 선택하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7649-117">This name and type is used to pick the correct property from the event in your event source.</span></span> <span data-ttu-id="c7649-118">예를 들어, 키 이름을 “DeviceId”, 형식을 “String”으로 제공한 경우 Time Series Insights 수신 엔진은 들어오는 이벤트에서 “DeviceId”라는 이름과 “String” 형식의 속성을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c7649-118">For instance, if you provide key name as “DeviceId” and type as “String”, then the Time Series Insights ingress engine looks for a property with the name “DeviceId” of type “String” in the incoming event.</span></span> <span data-ttu-id="c7649-119">이벤트와 조인하는 키를 둘 이상 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7649-119">You can provide more than one key to join with the event.</span></span> <span data-ttu-id="c7649-120">속성 이름 일치는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="c7649-120">The property name match is case-sensitive.</span></span>

     ![Time Series Insights 참조 데이터 집합 만들기 - 세부 정보](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. <span data-ttu-id="c7649-122">“만들기”를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7649-122">Click “Create.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7649-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c7649-123">Next steps</span></span>

* <span data-ttu-id="c7649-124">프로그래밍 방식으로 [참조 데이터를 관리](time-series-insights-manage-reference-data-csharp.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c7649-124">[Manage reference data](time-series-insights-manage-reference-data-csharp.md) programmatically.</span></span>
* <span data-ttu-id="c7649-125">전체 API 참조는 [참조 데이터 API](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c7649-125">For the complete API reference, see [Reference Data API](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) document.</span></span>