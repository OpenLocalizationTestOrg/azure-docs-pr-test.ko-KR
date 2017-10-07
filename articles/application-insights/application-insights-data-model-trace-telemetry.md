---
title: "응용 프로그램 Insights 원격 분석 데이터 모델-aaaAzure 추적 원격 분석 | Microsoft Docs"
description: "추적 원격 분석을 위한 Azure Application Insights 데이터 모델"
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
ms.openlocfilehash: dfdee958e07d57448ff41abc5cd33bfd05dac090
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="trace-telemetry-application-insights-data-model"></a><span data-ttu-id="b8afd-103">추적 원격 분석: Application Insights 데이터 모델</span><span class="sxs-lookup"><span data-stu-id="b8afd-103">Trace telemetry: Application Insights data model</span></span>

<span data-ttu-id="b8afd-104">[Application Insights](app-insights-overview.md)에서 추적 원격 분석은 텍스트를 검색하는 `printf` 스타일 추적 문을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b8afd-104">Trace telemetry (in [Application Insights](app-insights-overview.md)) represents `printf` style trace statements that are text-searched.</span></span> <span data-ttu-id="b8afd-105">`Log4Net`, `NLog` 및 기타 텍스트 기반 로그 파일 항목이 이 형식의 인스턴스로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8afd-105">`Log4Net`, `NLog`, and other text-based log file entries are translated into instances of this type.</span></span> <span data-ttu-id="b8afd-106">hello 추적 확장성으로 측정 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b8afd-106">hello trace does not have measurements as an extensibility.</span></span>

## <a name="message"></a><span data-ttu-id="b8afd-107">Message</span><span class="sxs-lookup"><span data-stu-id="b8afd-107">Message</span></span>

<span data-ttu-id="b8afd-108">추적 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="b8afd-108">Trace message.</span></span>

<span data-ttu-id="b8afd-109">최대 길이: 32768자</span><span class="sxs-lookup"><span data-stu-id="b8afd-109">Max length: 32768 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="b8afd-110">심각도 수준</span><span class="sxs-lookup"><span data-stu-id="b8afd-110">Severity level</span></span>

<span data-ttu-id="b8afd-111">추적 심각도 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="b8afd-111">Trace severity level.</span></span> <span data-ttu-id="b8afd-112">값은 `Verbose`, `Information`, `Warning`, `Error`, `Critical`일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8afd-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="b8afd-113">사용자 지정 속성</span><span class="sxs-lookup"><span data-stu-id="b8afd-113">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="b8afd-114">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b8afd-114">Next steps</span></span>

- <span data-ttu-id="b8afd-115">[Application Insights에서 .NET 추적 로그 탐색](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="b8afd-115">[Explore .NET trace logs in Application Insights](app-insights-asp-net-trace-logs.md).</span></span>
- <span data-ttu-id="b8afd-116">[Application Insights에서 Java 추적 로그 탐색](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="b8afd-116">[Explore Java trace logs in Application Insights](app-insights-java-trace-logs.md).</span></span>
- <span data-ttu-id="b8afd-117">Application Insights 형식 및 데이터 모델에 대한 자세한 내용은 [데이터 모델](application-insights-data-model.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8afd-117">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="b8afd-118">[사용자 지정 추적 원격 분석을 작성합니다](app-insights-api-custom-events-metrics.md#tracktrace).</span><span class="sxs-lookup"><span data-stu-id="b8afd-118">[Write custom trace telemetry](app-insights-api-custom-events-metrics.md#tracktrace)</span></span>
- <span data-ttu-id="b8afd-119">Application Insights에서 지원되는 [플랫폼](app-insights-platforms.md)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b8afd-119">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
