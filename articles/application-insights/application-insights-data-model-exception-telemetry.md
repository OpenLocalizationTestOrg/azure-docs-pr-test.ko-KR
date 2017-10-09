---
title: "응용 프로그램 Insights 원격 분석 데이터 모델-aaaAzure 예외 원격 분석 | Microsoft Docs"
description: "예외 원격 분석을 위한 Azure Application Insights 데이터 모델"
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
ms.openlocfilehash: 4c2b7d1ac3816d5623db9a35819a48a68a13a9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="exception-telemetry-application-insights-data-model"></a><span data-ttu-id="3669d-103">예외 원격 분석: Application Insights 데이터 모델</span><span class="sxs-lookup"><span data-stu-id="3669d-103">Exception telemetry: Application Insights data model</span></span>

<span data-ttu-id="3669d-104">[Application Insights](app-insights-overview.md), Exception 인스턴스의 hello 모니터링 응용 프로그램의 실행 중에 발생 한 처리 또는 처리 되지 않은 예외를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3669d-104">In [Application Insights](app-insights-overview.md), an instance of Exception represents a handled or unhandled exception that occurred during execution of hello monitored application.</span></span>

## <a name="problem-id"></a><span data-ttu-id="3669d-105">문제 ID</span><span class="sxs-lookup"><span data-stu-id="3669d-105">Problem Id</span></span>

<span data-ttu-id="3669d-106">Hello 예외가 throw 된 코드에서의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="3669d-106">Identifier of where hello exception was thrown in code.</span></span> <span data-ttu-id="3669d-107">예외 그룹화에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3669d-107">Used for exceptions grouping.</span></span> <span data-ttu-id="3669d-108">일반적으로 예외 형식 및 함수 호출 스택 hello에서의 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="3669d-108">Typically a combination of exception type and a function from hello call stack.</span></span>

<span data-ttu-id="3669d-109">최대 길이: 1024자</span><span class="sxs-lookup"><span data-stu-id="3669d-109">Max length: 1024 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="3669d-110">심각도 수준</span><span class="sxs-lookup"><span data-stu-id="3669d-110">Severity level</span></span>

<span data-ttu-id="3669d-111">추적 심각도 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="3669d-111">Trace severity level.</span></span> <span data-ttu-id="3669d-112">값은 `Verbose`, `Information`, `Warning`, `Error`, `Critical`일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3669d-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="exception-details"></a><span data-ttu-id="3669d-113">예외 세부 정보</span><span class="sxs-lookup"><span data-stu-id="3669d-113">Exception details</span></span>

<span data-ttu-id="3669d-114">(toobe 확장)</span><span class="sxs-lookup"><span data-stu-id="3669d-114">(toobe extended)</span></span>

## <a name="custom-properties"></a><span data-ttu-id="3669d-115">사용자 지정 속성</span><span class="sxs-lookup"><span data-stu-id="3669d-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="3669d-116">사용자 지정 측정</span><span class="sxs-lookup"><span data-stu-id="3669d-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="3669d-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3669d-117">Next steps</span></span>

- <span data-ttu-id="3669d-118">Application Insights 형식 및 데이터 모델에 대한 자세한 내용은 [데이터 모델](application-insights-data-model.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3669d-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="3669d-119">너무 방법에 대해 알아봅니다[Application Insights를 사용한 웹 응용 프로그램의 예외를 진단](app-insights-asp-net-exceptions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3669d-119">Learn how too[diagnose exceptions in your web apps with Application Insights](app-insights-asp-net-exceptions.md).</span></span>
- <span data-ttu-id="3669d-120">Application Insights에서 지원되는 [플랫폼](app-insights-platforms.md)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3669d-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
