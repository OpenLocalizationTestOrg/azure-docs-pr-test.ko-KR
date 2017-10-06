---
title: "엔터프라이즈 Api 청구 aaaAzure | Microsoft Docs"
description: "Hello Enterprise Azure 고객 toopull 소비 데이터에 프로그래밍 방식으로 사용할 수 있는 보고 Api에 알아봅니다."
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
ms.openlocfilehash: 017cecc57ad6bdeb402b5d9d57fc95df9b033a42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a><span data-ttu-id="80129-103">기업 고객을 위한 보고 API 개요</span><span class="sxs-lookup"><span data-stu-id="80129-103">Overview of Reporting APIs for Enterprise customers</span></span>
<span data-ttu-id="80129-104">hello 보고 Api를 사용 Enterprise Azure 고객 tooprogrammatically 끌어오기 사용량과 청구 데이터를 기본 설정된 된 데이터 분석 도구.</span><span class="sxs-lookup"><span data-stu-id="80129-104">hello Reporting APIs enable Enterprise Azure customers tooprogrammatically pull consumption and billing data into preferred data analysis tools.</span></span> 

## <a name="enabling-data-access-toohello-api"></a><span data-ttu-id="80129-105">데이터 액세스 toohello API를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="80129-105">Enabling data access toohello API</span></span>
* <span data-ttu-id="80129-106">**생성 또는 hello API 키를 검색할** 도움말에서 toohello 엔터프라이즈 포털 및 따라 hello 자습서에서는 로그-보고 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="80129-106">**Generate or retrieve hello API key** - Log in toohello Enterprise portal and follow hello tutorial under Help - Reporting APIs.</span></span> <span data-ttu-id="80129-107">이 도움말 문서에서 첫 번째 섹션 hello toogenerate 또는 검색 hello API 키 hello에 대 한 등록을 지정 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="80129-107">hello first section under this help article explains how toogenerate or retrieve hello API key for hello specified enrollment.</span></span>
* <span data-ttu-id="80129-108">**Hello API에에서 키가 전달** -hello API 키 toobe 인증 및 권한 부여에 대 한 각 호출에 대해 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80129-108">**Passing keys in hello API** - hello API key needs toobe passed for each call for Authentication and Authorization.</span></span> <span data-ttu-id="80129-109">hello 다음 속성은 toobe toohello HTTP 헤더</span><span class="sxs-lookup"><span data-stu-id="80129-109">hello following property needs toobe toohello HTTP headers</span></span>

|<span data-ttu-id="80129-110">요청 헤더 키</span><span class="sxs-lookup"><span data-stu-id="80129-110">Request Header Key</span></span> | <span data-ttu-id="80129-111">값</span><span class="sxs-lookup"><span data-stu-id="80129-111">Value</span></span>|
|-|-|
|<span data-ttu-id="80129-112">권한 부여</span><span class="sxs-lookup"><span data-stu-id="80129-112">Authorization</span></span>| <span data-ttu-id="80129-113">Hello 값이 형식으로 지정: **전달자 {API_KEY}**</span><span class="sxs-lookup"><span data-stu-id="80129-113">Specify hello value in this format: **bearer {API_KEY}**</span></span> <br/> <span data-ttu-id="80129-114">예: bearer eyr....09</span><span class="sxs-lookup"><span data-stu-id="80129-114">Example: bearer eyr....09</span></span>|

## <a name="consumption-apis"></a><span data-ttu-id="80129-115">사용량 API</span><span class="sxs-lookup"><span data-stu-id="80129-115">Consumption APIs</span></span>
<span data-ttu-id="80129-116">Swagger 끝점을 사용할 수 [여기](https://consumption.azure.com/swagger/ui/index) hello에 대 한 Api 이하로 해야 hello API 및 hello 기능 toogenerate 클라이언트 Sdk 사용 쉽게 검사 사용 하 여 설명 [AutoRest](https://github.com/Azure/AutoRest) 또는 [ Swagger CodeGen](http://swagger.io/swagger-codegen/)합니다.</span><span class="sxs-lookup"><span data-stu-id="80129-116">A Swagger endpoint is available [here](https://consumption.azure.com/swagger/ui/index) for hello APIs described below which should enable easy introspection of hello API and hello ability toogenerate client SDKs using [AutoRest](https://github.com/Azure/AutoRest) or [Swagger CodeGen](http://swagger.io/swagger-codegen/).</span></span> <span data-ttu-id="80129-117">2014년 5월 1일부터 시작하는 데이터는 이 API를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80129-117">Data beginning May 1, 2014 is available through this API.</span></span> 

* <span data-ttu-id="80129-118">**잔액 및 요약** -hello [균형 및 요약 API](billing-enterprise-api-balance-summary.md) 월별 요약 잔액, 새 구매, Azure 마켓플레이스 서비스 요금이, 조정 및 초과 요금에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="80129-118">**Balance and Summary** - hello [Balance and Summary API](billing-enterprise-api-balance-summary.md) offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments and overage charges.</span></span>

* <span data-ttu-id="80129-119">**사용 정보** -hello [사용 현황 세부 API](billing-enterprise-api-usage-detail.md) 소비 된 수량 및 등록 하 여 예상된 요금 일별로 구분을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="80129-119">**Usage Details** - hello [Usage Detail API](billing-enterprise-api-usage-detail.md) offers a daily breakdown of consumed quantities and estimated charges by an Enrollment.</span></span> <span data-ttu-id="80129-120">hello 결과는 인스턴스, 측정 단위 및 부서에 대 한 정보 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80129-120">hello result also includes information on instances, meters and departments.</span></span> <span data-ttu-id="80129-121">지정 된 시작 및 종료 날짜 또는 청구 기간에 의해 hello API를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80129-121">hello API can be queried by Billing period or by a specified start and end date.</span></span> 

* <span data-ttu-id="80129-122">**마켓플레이스 저장소 충전** -hello [마켓플레이스 저장소 충전 API](billing-enterprise-api-marketplace-storecharge.md) hello 지정한 시작 및 종료 날짜 (한 번 요금 포함 되지 않습니다.) 또는 대금 청구 기간에 대 한 일별 hello 마켓플레이스 사용량 기반 요금 분석 결과 반환 .</span><span class="sxs-lookup"><span data-stu-id="80129-122">**Marketplace Store Charge** - hello [Marketplace Store Charge API](billing-enterprise-api-marketplace-storecharge.md) returns hello usage-based marketplace charges breakdown by day for hello specified Billing Period or start and end dates (one time fees are not included).</span></span>

* <span data-ttu-id="80129-123">**가격표** -hello [가격 시트 API](billing-enterprise-api-pricesheet.md) hello 등록 및 대금 청구 기간에 대 한 각 수준에 대 한 hello 적용 가능한 속도 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="80129-123">**Price Sheet** - hello [Price Sheet API](billing-enterprise-api-pricesheet.md) provides hello applicable rate for each Meter for hello given Enrollment and Billing Period.</span></span> 

## <a name="helper-apis"></a><span data-ttu-id="80129-124">도우미 API</span><span class="sxs-lookup"><span data-stu-id="80129-124">Helper APIs</span></span>
 <span data-ttu-id="80129-125">**대금 청구 기간 목록** -hello [청구 기간 API](billing-enterprise-api-billing-periods.md) 기간 hello 역시간순에서 등록 지정한에 대 한 사용 데이터를 가진 청구의 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="80129-125">**List Billing Periods** - hello [Billing Periods API](billing-enterprise-api-billing-periods.md) returns a list of billing periods that have consumption data for hello specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="80129-126">각 기간에는 4 개의 집합이 데이터 요금-BalanceSummary, UsageDetails, 마켓플레이스 요금 및 가격표를 hello에 대 한 toohello API 경로 가리키는 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="80129-126">Each Period contains a property pointing toohello API route for hello four sets of data - BalanceSummary, UsageDetails, Marketplace Charges, and Price Sheet.</span></span>


## <a name="api-response-codes"></a><span data-ttu-id="80129-127">API 응답 코드</span><span class="sxs-lookup"><span data-stu-id="80129-127">API Response Codes</span></span>  
|<span data-ttu-id="80129-128">응답 상태 코드</span><span class="sxs-lookup"><span data-stu-id="80129-128">Response Status Code</span></span>|<span data-ttu-id="80129-129">Message</span><span class="sxs-lookup"><span data-stu-id="80129-129">Message</span></span>|<span data-ttu-id="80129-130">설명</span><span class="sxs-lookup"><span data-stu-id="80129-130">Description</span></span>|
|-|-|-|
|<span data-ttu-id="80129-131">200</span><span class="sxs-lookup"><span data-stu-id="80129-131">200</span></span>| <span data-ttu-id="80129-132">확인</span><span class="sxs-lookup"><span data-stu-id="80129-132">OK</span></span>|<span data-ttu-id="80129-133">오류 없음</span><span class="sxs-lookup"><span data-stu-id="80129-133">No error</span></span>|
|<span data-ttu-id="80129-134">401</span><span class="sxs-lookup"><span data-stu-id="80129-134">401</span></span>| <span data-ttu-id="80129-135">권한 없음</span><span class="sxs-lookup"><span data-stu-id="80129-135">Unauthorized</span></span>| <span data-ttu-id="80129-136">API 키를 찾을 수 없음, 유효하지 않음, 만료됨 등</span><span class="sxs-lookup"><span data-stu-id="80129-136">API Key not found, Invalid, Expired etc.</span></span>|
|<span data-ttu-id="80129-137">404</span><span class="sxs-lookup"><span data-stu-id="80129-137">404</span></span>| <span data-ttu-id="80129-138">사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="80129-138">Unavailable</span></span>| <span data-ttu-id="80129-139">보고서 끝점을 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="80129-139">Report endpoint not found</span></span>|
|<span data-ttu-id="80129-140">400</span><span class="sxs-lookup"><span data-stu-id="80129-140">400</span></span>| <span data-ttu-id="80129-141">잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="80129-141">Bad Request</span></span>| <span data-ttu-id="80129-142">잘못된 매개 변수 - 날짜 범위, EA 숫자 등</span><span class="sxs-lookup"><span data-stu-id="80129-142">Invalid params – Date ranges, EA numbers etc.</span></span>|
|<span data-ttu-id="80129-143">500</span><span class="sxs-lookup"><span data-stu-id="80129-143">500</span></span>| <span data-ttu-id="80129-144">서버 오류</span><span class="sxs-lookup"><span data-stu-id="80129-144">Server Error</span></span>| <span data-ttu-id="80129-145">예기치 않은 오류 처리 요청</span><span class="sxs-lookup"><span data-stu-id="80129-145">Unexoected error processing request</span></span>| 









