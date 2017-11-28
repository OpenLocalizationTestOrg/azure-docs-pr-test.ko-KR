---
title: "응용 프로그램 Insights 원격 분석 데이터 모델-aaaAzure 이벤트 원격 분석 | Microsoft Docs"
description: "이벤트 원격 분석을 위한 Azure Application Insights 데이터 모델"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: cd7dc3c5f4f3df22b7a52ee79fcad566a27a9f4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-telemetry-application-insights-data-model"></a><span data-ttu-id="18909-103">이벤트 원격 분석: Application Insights 데이터 모델</span><span class="sxs-lookup"><span data-stu-id="18909-103">Event telemetry: Application Insights data model</span></span>

<span data-ttu-id="18909-104">원격 분석 항목 이벤트를 만들 수 있습니다 (에서 [Application Insights](app-insights-overview.md)) toorepresent 응용 프로그램에서 발생 하는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="18909-104">You can create event telemetry items (in [Application Insights](app-insights-overview.md)) toorepresent an event that occurred in your application.</span></span> <span data-ttu-id="18909-105">일반적으로 이 작업은 단추 클릭 또는 주문 체크 아웃과 같은 사용자 조작입니다.</span><span class="sxs-lookup"><span data-stu-id="18909-105">Typically it is a user interaction such as button click or order checkout.</span></span> <span data-ttu-id="18909-106">초기화 또는 구성 업데이트 같은 응용 프로그램 수명 주기 이벤트일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18909-106">It can also be an application life cycle event like initialization or configuration update.</span></span> 

<span data-ttu-id="18909-107">의미상으로 이벤트 수도 상관 관계가 지정 된 toorequests 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18909-107">Semantically, events may or may not be correlated toorequests.</span></span> <span data-ttu-id="18909-108">하지만 제대로 사용될 경우 이벤트 원격 분석은 요청이나 추적보다 더 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="18909-108">However, if used properly, event telemetry is more important than requests or traces.</span></span> <span data-ttu-id="18909-109">이벤트 비즈니스 원격 분석을 나타내고 보다 낮은 값 제목 tooseparate 해야 [샘플링](app-insights-api-filtering-sampling.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="18909-109">Events represent business telemetry and should be a subject tooseparate, less aggressive [sampling](app-insights-api-filtering-sampling.md).</span></span>

## <a name="name"></a><span data-ttu-id="18909-110">이름</span><span class="sxs-lookup"><span data-stu-id="18909-110">Name</span></span>

<span data-ttu-id="18909-111">이벤트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="18909-111">Event name.</span></span> <span data-ttu-id="18909-112">tooallow 적절 한 그룹화 및 유용한 메트릭 적은 수의 별도 이벤트 이름 생성 되도록 응용 프로그램을 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="18909-112">tooallow proper grouping and useful metrics, restrict your application so that it generates a small number of separate event names.</span></span> <span data-ttu-id="18909-113">예를 들어 생성된 이벤트 인스턴스마다 별도의 이름을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18909-113">For example, don't use a separate name for each generated instance of an event.</span></span>

<span data-ttu-id="18909-114">최대 길이: 512자</span><span class="sxs-lookup"><span data-stu-id="18909-114">Max length: 512 characters</span></span>

## <a name="custom-properties"></a><span data-ttu-id="18909-115">사용자 지정 속성</span><span class="sxs-lookup"><span data-stu-id="18909-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="18909-116">사용자 지정 측정</span><span class="sxs-lookup"><span data-stu-id="18909-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="18909-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="18909-117">Next steps</span></span>

- <span data-ttu-id="18909-118">Application Insights 형식 및 데이터 모델에 대한 자세한 내용은 [데이터 모델](application-insights-data-model.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18909-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="18909-119">[사용자 지정 이벤트 원격 분석을 작성합니다](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="18909-119">[Write custom event telemetry](app-insights-api-custom-events-metrics.md#trackevent)</span></span>
- <span data-ttu-id="18909-120">Application Insights에서 지원되는 [플랫폼](app-insights-platforms.md)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="18909-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
