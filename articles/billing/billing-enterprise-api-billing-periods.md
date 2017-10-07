---
title: "청구 기간 청구 엔터프라이즈 Api aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: d4e17f25b22729a7f213306fb019ee0dbeca87ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a>기업 고객을 위한 보고 API - 청구 기간

대금 청구 기간 API hello 시간 순서에 등록에 대 한 hello에 대 한 데이터를 소비 하는 기간을 청구의 목록이 지정을 반환 합니다. 각 기간에는 4 개의 집합이 데이터 요금-BalanceSummary, UsageDetails, Marktplace 요금 및 가격표를 hello에 대 한 toohello API 경로 가리키는 속성을 포함 합니다. Hello 기간에 데이터가 없는 hello 해당 하는 속성은 null입니다. 


##<a name="request"></a>요청 
Toobe 추가 해야 하는 공통 헤더 속성이 지정 되어 [여기](billing-enterprise-api.md)합니다. 

|메서드 | 요청 URI|
|-|-|
|GET| https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods|

> [!Note]
> toouse hello 미리 보기 버전의 API, URL 위에 hello v1 v2를 대체 합니다.
>

## <a name="response"></a>응답
 
    
    
      [
            {
                "billingPeriodId": "201704",
                "billingStart": "2017-04-01T00:00:00Z",
                "billingEnd": "2017-04-30T11:59:59Z",
                "balanceSummary": "/v1/enrollments/100/billingperiods/201704/balancesummary",
                "usageDetails": "/v1/enrollments/100/billingperiods/201704/usagedetails",
                "marketplaceCharges": "/v1/enrollments/100/billingperiods/201704/marketplacecharges",
                "priceSheet": "/v1/enrollments/100/billingperiods/201704/pricesheet"
            },          
            ....
      ]
    

**응답 속성 정의**

|속성 이름| 형식| 설명
|-|-|-|
|billingPeriodId| string| hello 특정 요금 청구 기간을 나타내는 고유 Id|
|billingStart| datetime| Hello 기간 시작 날짜를 나타내는 ISO 8601 문자열입니다.|
|billingEnd| datetime| Hello 기간 종료 날짜를 나타내는 ISO 8601 문자열입니다.|
|balanceSummary| string| hello URL 경로입니다.이 기간에 대 한 toohello 균형 요약 데이터의 경로|
|usageDetails| string| hello URL 경로입니다.이 기간에 대 한 toohello 사용 정보 데이터의 경로|
|marketplaceCharges| string| hello URL 경로입니다.이 기간에 대 한 toohello 마켓플레이스 요금 데이터의 경로|
|priceSheet| string| hello URL 경로입니다.이 기간에 대 한 toohello 가격표 데이터의 경로|

<br/>
## <a name="see-also"></a>참고 항목

* [잔액 및 요약 API](billing-enterprise-api-balance-summary.md)

* [사용량 세부 정보 API](billing-enterprise-api-usage-detail.md) 

* [Marketplace 저장소 요금 API](billing-enterprise-api-marketplace-storecharge.md) 

* [가격표 API](billing-enterprise-api-pricesheet.md)