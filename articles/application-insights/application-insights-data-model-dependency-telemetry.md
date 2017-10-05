---
title: "Azure Application Insights 원격 분석 데이터 모델 - 종속성 원격 분석 | Microsoft Docs"
description: "종속성 원격 분석을 위한 Azure Application Insights 데이터 모델"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/17/2017
ms.author: bwren
ms.openlocfilehash: 2e97c3f951f46c32802aea543b93d5ab1bb76228
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="dependency-telemetry-application-insights-data-model"></a><span data-ttu-id="97aa4-103">종속성 원격 분석: Application Insights 데이터 모델</span><span class="sxs-lookup"><span data-stu-id="97aa4-103">Dependency telemetry: Application Insights data model</span></span>

<span data-ttu-id="97aa4-104">[Application Insights](app-insights-overview.md)에서 종속성 원격 분석은 모니터링되는 구성 요소와 원격 구성 요소(예: SQL 또는 HTTP 끝점)의 상호 작용을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="97aa4-104">Dependency Telemetry (in [Application Insights](app-insights-overview.md)) represents an interaction of the monitored component with a remote component such as SQL or an HTTP endpoint.</span></span>

## <a name="name"></a><span data-ttu-id="97aa4-105">이름</span><span class="sxs-lookup"><span data-stu-id="97aa4-105">Name</span></span>

<span data-ttu-id="97aa4-106">이 종속성 호출을 사용하여 시작된 명령의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="97aa4-106">Name of the command initiated with this dependency call.</span></span> <span data-ttu-id="97aa4-107">낮은 카디널리티 값입니다.</span><span class="sxs-lookup"><span data-stu-id="97aa4-107">Low cardinality value.</span></span> <span data-ttu-id="97aa4-108">예로는 저장 프로시저 이름 및 URL 경로 템플릿이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97aa4-108">Examples are stored procedure name and URL path template.</span></span>

## <a name="id"></a><span data-ttu-id="97aa4-109">ID</span><span class="sxs-lookup"><span data-stu-id="97aa4-109">ID</span></span>

<span data-ttu-id="97aa4-110">종속성 호출 인스턴스의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="97aa4-110">Identifier of a dependency call instance.</span></span> <span data-ttu-id="97aa4-111">이 종속성 호출에 해당하는 요청 원격 분석 항목과의 상관 관계에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="97aa4-111">Used for correlation with the request telemetry item corresponding to this dependency call.</span></span> <span data-ttu-id="97aa4-112">자세한 내용은 [상관 관계](application-insights-correlation.md) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97aa4-112">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="data"></a><span data-ttu-id="97aa4-113">Data</span><span class="sxs-lookup"><span data-stu-id="97aa4-113">Data</span></span>

<span data-ttu-id="97aa4-114">이 종속성 호출로 시작되는 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="97aa4-114">Command initiated by this dependency call.</span></span> <span data-ttu-id="97aa4-115">예로 모든 쿼리 매개 변수를 포함하는 SQL 문 및 HTTP URL을 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97aa4-115">Examples are SQL statement and HTTP URL with all query parameters.</span></span>

## <a name="type"></a><span data-ttu-id="97aa4-116">형식</span><span class="sxs-lookup"><span data-stu-id="97aa4-116">Type</span></span>

<span data-ttu-id="97aa4-117">종속성 형식 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="97aa4-117">Dependency type name.</span></span> <span data-ttu-id="97aa4-118">다른 필드(예: commandName 및 resultCode)의 종속성 논리적 그룹에 대한 낮은 카디널리티 값 및 해석입니다.</span><span class="sxs-lookup"><span data-stu-id="97aa4-118">Low cardinality value for logical grouping of dependencies and interpretation of other fields like commandName and resultCode.</span></span> <span data-ttu-id="97aa4-119">예로 SQL, Azure 테이블 및 HTTP를 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97aa4-119">Examples are SQL, Azure table, and HTTP.</span></span>

## <a name="target"></a><span data-ttu-id="97aa4-120">대상</span><span class="sxs-lookup"><span data-stu-id="97aa4-120">Target</span></span>

<span data-ttu-id="97aa4-121">종속성 호출의 대상 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="97aa4-121">Target site of a dependency call.</span></span> <span data-ttu-id="97aa4-122">예로 서버 이름, 호스트 주소를 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97aa4-122">Examples are server name, host address.</span></span> <span data-ttu-id="97aa4-123">자세한 내용은 [상관 관계](application-insights-correlation.md) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97aa4-123">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="duration"></a><span data-ttu-id="97aa4-124">기간</span><span class="sxs-lookup"><span data-stu-id="97aa4-124">Duration</span></span>

<span data-ttu-id="97aa4-125">요청 기간은 `DD.HH:MM:SS.MMMMMM` 형식으로 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="97aa4-125">Request duration in format: `DD.HH:MM:SS.MMMMMM`.</span></span> <span data-ttu-id="97aa4-126">`1000`일보다 작아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97aa4-126">Must be less than `1000` days.</span></span>

## <a name="result-code"></a><span data-ttu-id="97aa4-127">결과 코드</span><span class="sxs-lookup"><span data-stu-id="97aa4-127">Result code</span></span>

<span data-ttu-id="97aa4-128">종속성 호출의 결과 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="97aa4-128">Result code of a dependency call.</span></span> <span data-ttu-id="97aa4-129">예로 SQL 오류 코드 및 HTTP 상태 코드를 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97aa4-129">Examples are SQL error code and HTTP status code.</span></span>

## <a name="success"></a><span data-ttu-id="97aa4-130">성공</span><span class="sxs-lookup"><span data-stu-id="97aa4-130">Success</span></span>

<span data-ttu-id="97aa4-131">성공 또는 실패한 호출을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="97aa4-131">Indication of successful or unsuccessful call.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="97aa4-132">사용자 지정 속성</span><span class="sxs-lookup"><span data-stu-id="97aa4-132">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="97aa4-133">사용자 지정 측정</span><span class="sxs-lookup"><span data-stu-id="97aa4-133">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]


## <a name="next-steps"></a><span data-ttu-id="97aa4-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="97aa4-134">Next steps</span></span>

- <span data-ttu-id="97aa4-135">[.NET](app-insights-asp-net-dependencies.md)에 대한 종속성 추적을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="97aa4-135">Set up dependency tracking for [.NET](app-insights-asp-net-dependencies.md).</span></span>
- <span data-ttu-id="97aa4-136">[Java](app-insights-java-agent.md)에 대한 종속성 추적을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="97aa4-136">Set up dependency tracking for [Java](app-insights-java-agent.md).</span></span>
- <span data-ttu-id="97aa4-137">[사용자 지정 종속성 원격 분석을 작성합니다](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="97aa4-137">[Write custom dependency telemetry](app-insights-api-custom-events-metrics.md#trackdependency)</span></span>
- <span data-ttu-id="97aa4-138">Application Insights 형식 및 데이터 모델에 대한 자세한 내용은 [데이터 모델](application-insights-data-model.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97aa4-138">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="97aa4-139">Application Insights에서 지원되는 [플랫폼](app-insights-platforms.md)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="97aa4-139">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
