---
title: "Azure Application Insights 원격 분석 데이터 모델 - 예외 원격 분석 | Microsoft 문서"
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
ms.openlocfilehash: 6b220b0cb6719bac606f599d657d08ab847c7590
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="exception-telemetry-application-insights-data-model"></a><span data-ttu-id="06d63-103">예외 원격 분석: Application Insights 데이터 모델</span><span class="sxs-lookup"><span data-stu-id="06d63-103">Exception telemetry: Application Insights data model</span></span>

<span data-ttu-id="06d63-104">[Application Insights](app-insights-overview.md)에서 예외 인스턴스는 모니터링되는 응용 프로그램을 실행하는 동안 발생하여 처리되거나 처리되지 않은 예외를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="06d63-104">In [Application Insights](app-insights-overview.md), an instance of Exception represents a handled or unhandled exception that occurred during execution of the monitored application.</span></span>

## <a name="problem-id"></a><span data-ttu-id="06d63-105">문제 ID</span><span class="sxs-lookup"><span data-stu-id="06d63-105">Problem Id</span></span>

<span data-ttu-id="06d63-106">코드에서 throw된 예외의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="06d63-106">Identifier of where the exception was thrown in code.</span></span> <span data-ttu-id="06d63-107">예외 그룹화에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d63-107">Used for exceptions grouping.</span></span> <span data-ttu-id="06d63-108">일반적으로 예외 형식 및 호출 스택 기반 함수의 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="06d63-108">Typically a combination of exception type and a function from the call stack.</span></span>

<span data-ttu-id="06d63-109">최대 길이: 1024자</span><span class="sxs-lookup"><span data-stu-id="06d63-109">Max length: 1024 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="06d63-110">심각도 수준</span><span class="sxs-lookup"><span data-stu-id="06d63-110">Severity level</span></span>

<span data-ttu-id="06d63-111">추적 심각도 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="06d63-111">Trace severity level.</span></span> <span data-ttu-id="06d63-112">값은 `Verbose`, `Information`, `Warning`, `Error`, `Critical`일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d63-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="exception-details"></a><span data-ttu-id="06d63-113">예외 세부 정보</span><span class="sxs-lookup"><span data-stu-id="06d63-113">Exception details</span></span>

<span data-ttu-id="06d63-114">(확장 예정임)</span><span class="sxs-lookup"><span data-stu-id="06d63-114">(To be extended)</span></span>

## <a name="custom-properties"></a><span data-ttu-id="06d63-115">사용자 지정 속성</span><span class="sxs-lookup"><span data-stu-id="06d63-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="06d63-116">사용자 지정 측정</span><span class="sxs-lookup"><span data-stu-id="06d63-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="06d63-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="06d63-117">Next steps</span></span>

- <span data-ttu-id="06d63-118">Application Insights 형식 및 데이터 모델에 대한 자세한 내용은 [데이터 모델](application-insights-data-model.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06d63-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="06d63-119">[Application Insights를 사용하여 웹앱에서 예외를 진단](app-insights-asp-net-exceptions.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="06d63-119">Learn how to [diagnose exceptions in your web apps with Application Insights](app-insights-asp-net-exceptions.md).</span></span>
- <span data-ttu-id="06d63-120">Application Insights에서 지원되는 [플랫폼](app-insights-platforms.md)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="06d63-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
