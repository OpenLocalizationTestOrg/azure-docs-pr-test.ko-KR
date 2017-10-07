---
title: "aaaAzure 청구 엔터프라이즈 Api-가격표 | Microsoft Docs"
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
ms.openlocfilehash: 4cfe694c63fba266d117054b046d9caacb3b7197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a>기업 고객을 위한 보고 API - 가격표

hello 가격 시트 API hello 등록 및 대금 청구 기간에 대 한 각 수준에 대 한 hello 적용 가능한 속도 제공 합니다.

##<a name="request"></a>요청
Toobe 추가 해야 하는 공통 헤더 속성이 지정 되어 [여기](billing-enterprise-api.md)합니다. 청구 기간 지정 하지 않으면 다음 hello 현재 청구에 대 한 데이터 기간 반환 됩니다.

|메서드 | 요청 URI|
|-|-|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet|

> [!Note]
> toouse hello 미리 보기 버전의 API, URL 위에 hello v1 v2를 대체 합니다.
>

## <a name="response"></a>응답

    
        [
            {
                "id": "enrollments/57354989/billingperiods/201601/products/343/pricesheets",
                "billingPeriodId": "201704",
                "meterId": "dc210ecb-97e8-4522-8134-2385494233c0",
                "meterName": "A1 VM",
                "unitOfMeasure": "100 Hours",
                "includedQuantity": 0,
                "partNumber": "N7H-00015",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            {
                "id": "enrollments/57354989/billingperiods/201601/products/2884/pricesheets",
                "billingPeriodId": "201404",
                "meterId": "dc210ecb-97e8-4522-8134-5385494233c0",
                "meterName": "Locally Redundant Storage Premium Storage - Snapshots - AU East",
                "unitOfMeasure": "100 GB",
                "includedQuantity": 0,
                "partNumber": "N9H-00402",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            ...
        ]
    

> [!Note]
>Hello 미리 보기 API를 사용 하는 meterId 필드 ´ ù입니다.
>

**응답 속성 정의**

|속성 이름| 형식| 설명
|-|-|-|
|id| string| hello (청구 기간으로 미터) 특정 가격표 항목을 나타내는 고유 Id|
|billingPeriodId| string| hello 특정 요금 청구 기간을 나타내는 고유 Id|
|meterId| string| hello 식별자 hello 미터입니다. 매핑된 toohello 사용 meterId 수 있습니다.|
|meterName| string| hello 미터 이름|
|unitOfMeasure| string| hello 서비스를 측정 하기 위한 hello 측정 단위|
|includedQuantity| decimal| 포함된 수량 |
|partNumber| string| 측정기 hello와 관련 된 hello 부품 번호|
|unitPrice| decimal| 측정기 hello에 대 한 hello 단가|
|currencyCode| string| hello unitPrice에 대 한 hello 통화 코드|
<br/>
## <a name="see-also"></a>참고 항목

* [청구 기간 API](billing-enterprise-api-billing-periods.md)

* [사용량 세부 정보 API](billing-enterprise-api-usage-detail.md)

* [잔액 및 요약 API](billing-enterprise-api-balance-summary.md)

* [Marketplace 저장소 요금 API](billing-enterprise-api-marketplace-storecharge.md)
