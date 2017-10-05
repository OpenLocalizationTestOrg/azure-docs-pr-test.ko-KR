---
title: "Azure 청구 엔터프라이즈 API | Microsoft Docs"
description: "Azure 기업 고객이 사용량 데이터를 프로그래밍 방식으로 끌어올 수 있게 하는 보고 API에 대해 알아봅니다."
services: 
documentationcenter: 
author: aedwin
manager: aedwin
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/25/2017
ms.author: aedwin
ms.openlocfilehash: e3a5f9bcd6b54a51c29df649f1ae8ac185b153a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a><span data-ttu-id="4bbee-103">기업 고객을 위한 보고 API 개요</span><span class="sxs-lookup"><span data-stu-id="4bbee-103">Overview of Reporting APIs for Enterprise customers</span></span>
<span data-ttu-id="4bbee-104">Azure 기업 고객은 보고 API를 통해 사용량 및 청구 데이터를 기본 데이터 분석 도구로 프로그래밍 방식으로 끌어올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bbee-104">The Reporting APIs enable Enterprise Azure customers to programmatically pull consumption and billing data into preferred data analysis tools.</span></span> 

## <a name="enabling-data-access-to-the-api"></a><span data-ttu-id="4bbee-105">API에 대한 데이터 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="4bbee-105">Enabling data access to the API</span></span>
* <span data-ttu-id="4bbee-106">**API 키 생성/검색** - 엔터프라이즈 포털에 로그인하고, 도움말 - Reporting API 아래의 자습서를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4bbee-106">**Generate or retrieve the API key** - Log in to the Enterprise portal and follow the tutorial under Help - Reporting APIs.</span></span> <span data-ttu-id="4bbee-107">이 도움말 문서의 첫 번째 섹션에서는 지정된 등록에 대한 API 키를 생성하거나 검색하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbee-107">The first section under this help article explains how to generate or retrieve the API key for the specified enrollment.</span></span>
* <span data-ttu-id="4bbee-108">**API에서 키 전달** - API 키는 인증 및 권한 부여를 호출할 때마다 전달되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbee-108">**Passing keys in the API** - The API key needs to be passed for each call for Authentication and Authorization.</span></span> <span data-ttu-id="4bbee-109">HTTP 헤더에 있어야 하는 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4bbee-109">The following property needs to be to the HTTP headers</span></span>

|<span data-ttu-id="4bbee-110">요청 헤더 키</span><span class="sxs-lookup"><span data-stu-id="4bbee-110">Request Header Key</span></span> | <span data-ttu-id="4bbee-111">값</span><span class="sxs-lookup"><span data-stu-id="4bbee-111">Value</span></span>|
|-|-|
|<span data-ttu-id="4bbee-112">권한 부여</span><span class="sxs-lookup"><span data-stu-id="4bbee-112">Authorization</span></span>| <span data-ttu-id="4bbee-113">**bearer {API_KEY}** 형식의 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbee-113">Specify the value in this format: **bearer {API_KEY}**</span></span> <br/> <span data-ttu-id="4bbee-114">예: bearer eyr....09</span><span class="sxs-lookup"><span data-stu-id="4bbee-114">Example: bearer eyr....09</span></span>|

## <a name="consumption-apis"></a><span data-ttu-id="4bbee-115">사용량 API</span><span class="sxs-lookup"><span data-stu-id="4bbee-115">Consumption APIs</span></span>
<span data-ttu-id="4bbee-116">Swagger 끝점은 [AutoRest](https://github.com/Azure/AutoRest) 또는 [Swagger CodeGen](http://swagger.io/swagger-codegen/)을 사용하여 손쉬운 API 검사와 클라이언트 SDK 생성 기능을 사용할 수 있게 하는 아래에서 설명하는 API에 대해 [여기](https://consumption.azure.com/swagger/ui/index)에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4bbee-116">A Swagger endpoint is available [here](https://consumption.azure.com/swagger/ui/index) for the APIs described below which should enable easy introspection of the API and the ability to generate client SDKs using [AutoRest](https://github.com/Azure/AutoRest) or [Swagger CodeGen](http://swagger.io/swagger-codegen/).</span></span> <span data-ttu-id="4bbee-117">2014년 5월 1일부터 시작하는 데이터는 이 API를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bbee-117">Data beginning May 1, 2014 is available through this API.</span></span> 

* <span data-ttu-id="4bbee-118">**잔액 및 요약** - [잔액 및 요약 API](billing-enterprise-api-balance-summary.md)는 잔액, 신규 구매, Azure Marketplace 서비스 요금, 조정 및 초과 요금에 대한 월별 정보 요약을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbee-118">**Balance and Summary** - The [Balance and Summary API](billing-enterprise-api-balance-summary.md) offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments and overage charges.</span></span>

* <span data-ttu-id="4bbee-119">**사용량 세부 정보** - [사용량 세부 정보 API](billing-enterprise-api-usage-detail.md)는 등록에 따른 사용량과 예상 요금 의 일별 분석 결과를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbee-119">**Usage Details** - The [Usage Detail API](billing-enterprise-api-usage-detail.md) offers a daily breakdown of consumed quantities and estimated charges by an Enrollment.</span></span> <span data-ttu-id="4bbee-120">이 결과에는 인스턴스, 측정기 및 부서에 대한 정보도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4bbee-120">The result also includes information on instances, meters and departments.</span></span> <span data-ttu-id="4bbee-121">API는 청구 기간 또는 지정된 시작 날짜와 종료 날짜를 기준으로 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bbee-121">The API can be queried by Billing period or by a specified start and end date.</span></span> 

* <span data-ttu-id="4bbee-122">**Marketplace 저장소 요금** - [Marketplace 저장소 요금 API](billing-enterprise-api-marketplace-storecharge.md)는 지정된 청구 기간 또는 시작 날짜 및 종료 날짜(1회 요금은 포함되지 않음)에 대한 일별 사용량 기반 Marketplace 요금 분석 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbee-122">**Marketplace Store Charge** - The [Marketplace Store Charge API](billing-enterprise-api-marketplace-storecharge.md) returns the usage-based marketplace charges breakdown by day for the specified Billing Period or start and end dates (one time fees are not included).</span></span>

* <span data-ttu-id="4bbee-123">**가격표** - [가격표 API](billing-enterprise-api-pricesheet.md)는 지정된 등록 및 청구 기간에 대한 각 측정기에 적용할 수 있는 가격을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbee-123">**Price Sheet** - The [Price Sheet API](billing-enterprise-api-pricesheet.md) provides the applicable rate for each Meter for the given Enrollment and Billing Period.</span></span> 

## <a name="helper-apis"></a><span data-ttu-id="4bbee-124">도우미 API</span><span class="sxs-lookup"><span data-stu-id="4bbee-124">Helper APIs</span></span>
 <span data-ttu-id="4bbee-125">**청구 기간 나열** - [청구 기간 API](billing-enterprise-api-billing-periods.md)는 지정된 등록에 대한 사용량 데이터를 역방향 시간 순서로 표시한 청구 기간 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbee-125">**List Billing Periods** - The [Billing Periods API](billing-enterprise-api-billing-periods.md) returns a list of billing periods that have consumption data for the specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="4bbee-126">각 기간에는 4개의 데이터 집합(잔액 요약, 사용량 세부 정보, Marketplace 요금 및 가격표)에 대한 API 경로를 가리키는 속성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bbee-126">Each Period contains a property pointing to the API route for the four sets of data - BalanceSummary, UsageDetails, Marketplace Charges, and Price Sheet.</span></span>


## <a name="api-response-codes"></a><span data-ttu-id="4bbee-127">API 응답 코드</span><span class="sxs-lookup"><span data-stu-id="4bbee-127">API Response Codes</span></span>  
|<span data-ttu-id="4bbee-128">응답 상태 코드</span><span class="sxs-lookup"><span data-stu-id="4bbee-128">Response Status Code</span></span>|<span data-ttu-id="4bbee-129">Message</span><span class="sxs-lookup"><span data-stu-id="4bbee-129">Message</span></span>|<span data-ttu-id="4bbee-130">설명</span><span class="sxs-lookup"><span data-stu-id="4bbee-130">Description</span></span>|
|-|-|-|
|<span data-ttu-id="4bbee-131">200</span><span class="sxs-lookup"><span data-stu-id="4bbee-131">200</span></span>| <span data-ttu-id="4bbee-132">확인</span><span class="sxs-lookup"><span data-stu-id="4bbee-132">OK</span></span>|<span data-ttu-id="4bbee-133">오류 없음</span><span class="sxs-lookup"><span data-stu-id="4bbee-133">No error</span></span>|
|<span data-ttu-id="4bbee-134">401</span><span class="sxs-lookup"><span data-stu-id="4bbee-134">401</span></span>| <span data-ttu-id="4bbee-135">권한 없음</span><span class="sxs-lookup"><span data-stu-id="4bbee-135">Unauthorized</span></span>| <span data-ttu-id="4bbee-136">API 키를 찾을 수 없음, 유효하지 않음, 만료됨 등</span><span class="sxs-lookup"><span data-stu-id="4bbee-136">API Key not found, Invalid, Expired etc.</span></span>|
|<span data-ttu-id="4bbee-137">404</span><span class="sxs-lookup"><span data-stu-id="4bbee-137">404</span></span>| <span data-ttu-id="4bbee-138">사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="4bbee-138">Unavailable</span></span>| <span data-ttu-id="4bbee-139">보고서 끝점을 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="4bbee-139">Report endpoint not found</span></span>|
|<span data-ttu-id="4bbee-140">400</span><span class="sxs-lookup"><span data-stu-id="4bbee-140">400</span></span>| <span data-ttu-id="4bbee-141">잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="4bbee-141">Bad Request</span></span>| <span data-ttu-id="4bbee-142">잘못된 매개 변수 - 날짜 범위, EA 숫자 등</span><span class="sxs-lookup"><span data-stu-id="4bbee-142">Invalid params – Date ranges, EA numbers etc.</span></span>|
|<span data-ttu-id="4bbee-143">500</span><span class="sxs-lookup"><span data-stu-id="4bbee-143">500</span></span>| <span data-ttu-id="4bbee-144">서버 오류</span><span class="sxs-lookup"><span data-stu-id="4bbee-144">Server Error</span></span>| <span data-ttu-id="4bbee-145">예기치 않은 오류 처리 요청</span><span class="sxs-lookup"><span data-stu-id="4bbee-145">Unexoected error processing request</span></span>| 









