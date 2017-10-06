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
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a>기업 고객을 위한 보고 API 개요
hello 보고 Api를 사용 Enterprise Azure 고객 tooprogrammatically 끌어오기 사용량과 청구 데이터를 기본 설정된 된 데이터 분석 도구. 

## <a name="enabling-data-access-toohello-api"></a>데이터 액세스 toohello API를 사용 하도록 설정
* **생성 또는 hello API 키를 검색할** 도움말에서 toohello 엔터프라이즈 포털 및 따라 hello 자습서에서는 로그-보고 Api입니다. 이 도움말 문서에서 첫 번째 섹션 hello toogenerate 또는 검색 hello API 키 hello에 대 한 등록을 지정 하는 방법을 설명 합니다.
* **Hello API에에서 키가 전달** -hello API 키 toobe 인증 및 권한 부여에 대 한 각 호출에 대해 전달 해야 합니다. hello 다음 속성은 toobe toohello HTTP 헤더

|요청 헤더 키 | 값|
|-|-|
|권한 부여| Hello 값이 형식으로 지정: **전달자 {API_KEY}** <br/> 예: bearer eyr....09|

## <a name="consumption-apis"></a>사용량 API
Swagger 끝점을 사용할 수 [여기](https://consumption.azure.com/swagger/ui/index) hello에 대 한 Api 이하로 해야 hello API 및 hello 기능 toogenerate 클라이언트 Sdk 사용 쉽게 검사 사용 하 여 설명 [AutoRest](https://github.com/Azure/AutoRest) 또는 [ Swagger CodeGen](http://swagger.io/swagger-codegen/)합니다. 2014년 5월 1일부터 시작하는 데이터는 이 API를 통해 사용할 수 있습니다. 

* **잔액 및 요약** -hello [균형 및 요약 API](billing-enterprise-api-balance-summary.md) 월별 요약 잔액, 새 구매, Azure 마켓플레이스 서비스 요금이, 조정 및 초과 요금에 대 한 정보를 제공 합니다.

* **사용 정보** -hello [사용 현황 세부 API](billing-enterprise-api-usage-detail.md) 소비 된 수량 및 등록 하 여 예상된 요금 일별로 구분을 제공 합니다. hello 결과는 인스턴스, 측정 단위 및 부서에 대 한 정보 포함 됩니다. 지정 된 시작 및 종료 날짜 또는 청구 기간에 의해 hello API를 쿼리할 수 있습니다. 

* **마켓플레이스 저장소 충전** -hello [마켓플레이스 저장소 충전 API](billing-enterprise-api-marketplace-storecharge.md) hello 지정한 시작 및 종료 날짜 (한 번 요금 포함 되지 않습니다.) 또는 대금 청구 기간에 대 한 일별 hello 마켓플레이스 사용량 기반 요금 분석 결과 반환 .

* **가격표** -hello [가격 시트 API](billing-enterprise-api-pricesheet.md) hello 등록 및 대금 청구 기간에 대 한 각 수준에 대 한 hello 적용 가능한 속도 제공 합니다. 

## <a name="helper-apis"></a>도우미 API
 **대금 청구 기간 목록** -hello [청구 기간 API](billing-enterprise-api-billing-periods.md) 기간 hello 역시간순에서 등록 지정한에 대 한 사용 데이터를 가진 청구의 목록을 반환 합니다. 각 기간에는 4 개의 집합이 데이터 요금-BalanceSummary, UsageDetails, 마켓플레이스 요금 및 가격표를 hello에 대 한 toohello API 경로 가리키는 속성을 포함 합니다.


## <a name="api-response-codes"></a>API 응답 코드  
|응답 상태 코드|Message|설명|
|-|-|-|
|200| 확인|오류 없음|
|401| 권한 없음| API 키를 찾을 수 없음, 유효하지 않음, 만료됨 등|
|404| 사용할 수 없음| 보고서 끝점을 찾을 수 없음|
|400| 잘못된 요청| 잘못된 매개 변수 - 날짜 범위, EA 숫자 등|
|500| 서버 오류| 예기치 않은 오류 처리 요청| 









