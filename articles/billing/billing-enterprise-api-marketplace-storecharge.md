---
title: "마켓플레이스 요금 청구 엔터프라이즈 Api-aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: cdf2836b52df06a4bf5ed71a476fe33662c5363c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a>기업 고객을 위한 보고 API - Marketplace 스토어 요금(미리 보기)

hello hello에 대 한 일별 마켓플레이스 저장 충전 API 반환 hello 마켓플레이스 사용량 기반 요금 분석 대금 청구 기간 또는 시작 및 종료 날짜 (한 번 요금 포함 되지 않습니다.)를 지정 합니다.

##<a name="request"></a>요청 
Toobe 추가 해야 하는 공통 헤더 속성이 지정 되어 [여기](billing-enterprise-api.md)합니다. 청구 기간 지정 하지 않으면 다음 hello 현재 청구에 대 한 데이터 기간 반환 됩니다. 사용자가 지정한 시간 범위 hello 시작 되 면 지정할 수 있으며 hello 형식 yyyy-월-일 지원 hello 최대 시간 범위는 36 개월에에서 있는 날짜 매개 변수를 종료 합니다.  

|메서드 | 요청 URI|
|-|-|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10|

> [!Note]
> toouse hello 미리 보기 버전의 API, URL 위에 hello v1 v2를 대체 합니다.
>

## <a name="response"></a>응답
 
    
        [
            {
                "id": "id",
                "subscriptionGuid": "00000000-0000-0000-0000-000000000000",
                "subscriptionName": "subName",
                "meterId": "2core",
                "usageStartDate": "2015-09-17T00:00:00Z",
                "usageEndDate": "2015-09-17T23:59:59Z",
                "offerName": "Virtual LoadMaster™ (VLM) for Azure",
                "resourceGroup": "Res group",
                "instanceId": "id",
                "additionalInfo": "{\"ImageType\":null,\"ServiceType\":\"Medium\"}",
                "tags": "",
                "orderNumber": "order",
                "unitOfMeasure": "",
                "costCenter": "100",
                "accountId": 100,
                "accountName": "Account Name",
                "accountOwnerId": "account@live.com",
                "departmentId": 101,
                "departmentName": "Department 1",
                "publisherName": "Publisher 1",
                "planName": "Plan name",
                "consumedQuantity": 1.15,
                "resourceRate": 0.1,
                "extendedCost": 1.11
            },
            ...
        ]
    

**응답 속성 정의**

|속성 이름| 형식| 설명
|-|-|-|
|id|string|Hello 마켓플레이스 요금 항목에 대 한 고유 Id|
|subscriptionGuid|Guid|hello 구독 Guid|
|subscriptionName|string|hello 구독 이름|
|meterId|string|측정기를 내보내는 hello에 대 한 id|
|usageStartDate|DateTime|Hello 사용량 레코드에 대 한 시작 시간|
|usageEndDate|DateTime|Hello 사용량 레코드에 대 한 종료 시간|
|offerName|string|hello 제안 이름|
|resourceGroup|string|hello 리소스 그룹|
|instanceId|string|인스턴스 ID|
|additionalInfo|string|추가 정보 JSON 문자열|
|tags|string|태그 JSON 문자열|
|orderNumber|string|hello 주문 번호|
|unitOfMeasure|string|측정기 hello에 대 한 측정 단위|
|costCenter|string|hello 비용 센터|
|accountId|int|hello 계정 Id|
|accountName|string |hello 계정 이름|
|accountOwnerId|string|hello 계정 소유자 Id|
|departmentId|int|hello 부서 Id|
|departmentName|string|hello 부서 이름|
|publisherName|string|hello 게시자 이름|
|planName|string|hello 계획 이름|
|consumedQuantity|decimal|이 기간 동안의 사용량|
|resourceRate|decimal|측정기 hello에 대 한 단위 가격|
|extendedCost|decimal|사용량 및 확장 비용에 따른 예상 요금|
<br/>
## <a name="see-also"></a>참고 항목

* [청구 기간 API](billing-enterprise-api-billing-periods.md)

* [사용량 세부 정보 API](billing-enterprise-api-usage-detail.md) 

* [잔액 및 요약 API](billing-enterprise-api-balance-summary.md)

* [가격표 API](billing-enterprise-api-pricesheet.md)