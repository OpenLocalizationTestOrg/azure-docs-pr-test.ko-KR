---
title: "aaaAzure 청구 엔터프라이즈 Api-사용량 세부 정보 | Microsoft Docs"
description: "Azure 리소스 소비 및 추세에 대 한 tooprovide 사용 되는 정보는 Azure 청구 사용량 및 RateCard Api에 알아봅니다."
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
ms.openlocfilehash: def0805008261df5872f015db3d2b26e47d25569
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---usage-details"></a>기업 고객을 위한 보고 API - 사용량 세부 정보

사용 현황 세부 API hello 소비 된 수량 및 등록 하 여 예상된 요금 일별로 구분을 제공합니다. hello 결과는 인스턴스, 측정 단위 및 부서에 대 한 정보 포함 됩니다. 지정 된 시작 및 종료 날짜 또는 청구 기간에 의해 hello API를 쿼리할 수 있습니다. 
## <a name="consumption-apis"></a>사용량 API


##<a name="request"></a>요청 
Toobe 추가 해야 하는 공통 헤더 속성이 지정 되어 [여기](billing-enterprise-api.md)합니다. 청구 기간 지정 하지 않으면 다음 hello 현재 청구에 대 한 데이터 기간 반환 됩니다. 사용자가 지정한 시간 범위 hello 시작 되 면 지정할 수 있습니다 및 종료 날짜의에서 매개 변수를 hello 형식 yyyy. hello 지원 되는 최대 시간 범위는 36 개월입니다.  

|메서드 | 요청 URI|
|-|-|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetails 
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/usagedetails|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetailsbycustomdate?startTime=2017-01-01&endTime=2017-01-10|

> [!Note]
> toouse hello 미리 보기 버전의 API, URL 위에 hello v1 v2를 대체 합니다.
>

## <a name="response"></a>응답

> Toohello 잠재적으로 많은 양의 데이터 hello 결과 인해 집합이 페이징 됩니다. hello nextLink 속성이 있는 경우 데이터의 다음 페이지 hello에 대 한 hello 링크를 지정 합니다. Hello 링크 비어 있으면 즉 hello 마지막 페이지를 나타냅니다. 
<br/>

    {
        "id": "string",
        "data": [
            {                       
            "accountId": 0,
            "productId": 0,
            "resourceLocationId": 0,
            "consumedServiceId": 0,
            "departmentId": 0,
            "accountOwnerEmail": "string",
            "accountName": "string",
            "serviceAdministratorId": "string",
            "subscriptionId": 0,
            "subscriptionGuid": "string",
            "subscriptionName": "string",
            "date": "2017-04-27T23:01:43.799Z",
            "product": "string",
            "meterId": "string",
            "meterCategory": "string",
            "meterSubCategory": "string",
            "meterRegion": "string",
            "meterName": "string",
            "consumedQuantity": 0,
            "resourceRate": 0,
            "Cost": 0,
            "resourceLocation": "string",
            "consumedService": "string",
            "instanceId": "string",
            "serviceInfo1": "string",
            "serviceInfo2": "string",
            "additionalInfo": "string",
            "tags": "string",
            "storeServiceIdentifier": "string",
            "departmentName": "string",
            "costCenter": "string",
            "unitOfMeasure": "string",
            "resourceGroup": "string"
            }
        ],
        "nextLink": "string"
    }

<br/>
**응답 속성 정의**

|속성 이름| 형식| 설명
|-|-|-|
|id| string| hello hello API 호출에 대 한 고유 Id입니다. |
|데이터| JSON 배열| hello 모든 instance\meter에 대 한 사용 정보를 매일의 배열입니다.|
|nextLink| string| 페이지 데이터 hello nextLink 포인트 toohello URL tooreturn hello 다음 데이터 페이지를 더 많이 있는 경우. |
|accountId| int| 사용되지 않는 필드입니다. 이전 버전과의 호환성을 위해 존재합니다. |
|productId| int| 사용되지 않는 필드입니다. 이전 버전과의 호환성을 위해 존재합니다. |
|resourceLocationId| int| 사용되지 않는 필드입니다. 이전 버전과의 호환성을 위해 존재합니다. |
|consumedServiceID| int| 사용되지 않는 필드입니다. 이전 버전과의 호환성을 위해 존재합니다. |
|departmentId| int| 사용되지 않는 필드입니다. 이전 버전과의 호환성을 위해 존재합니다. |
|accountOwnerEmail| string| Hello 계정 소유자의 전자 메일 계정입니다. |
|accountName| string| 입력 한 고객 이름 hello 계정입니다. |
|serviceAdministratorId| string| 서비스 관리자의 전자 메일 주소입니다. |
|subscriptionId| int| 사용되지 않는 필드입니다. 이전 버전과의 호환성을 위해 존재합니다. |
|subscriptionGuid| string| Hello 구독에 대 한 전역 고유 식별자입니다. |
|subscriptionName| string| Hello 구독의 이름입니다. |
|date| string| hello 날짜 소비 발생 했습니다. |
|product| string| Hello 수준에 추가 세부 정보입니다. 예: A1(VM)Windows - 아시아 태평양 동부|
|meterId| string| hello 식별자 사용 내보내집니다는 hello 미터입니다. |
|meterCategory| string| 번호 사용 된 Azure 플랫폼 서비스입니다. |
|meterSubCategory| string| Hello 속도 영향을 줄 수 있는 hello Azure 서비스 유형을 정의 합니다. 예: A1 VM(Windows 외)|
|meterRegion| string| 데이터 센터 위치에 따라 가격이 책정 됩니다 하는 특정 서비스에 대 한 hello 데이터 센터의 hello 위치를 식별 합니다. |
|meterName| string| Hello 표시기의 이름입니다. |
|consumedQuantity| double| 소비 된 hello 미터의 hello 양입니다. |
|resourceRate| double| 청구 가능 단위당 적용 가능한 hello 속도입니다. |
|cost| double| hello 충전량 hello 미터에 대 한 발생 되었습니다. |
|resourceLocation| string| Hello 측정기 실행 되 고 있는 hello 데이터 센터를 식별 합니다. |
|consumedService| string| 번호 사용 된 Azure 플랫폼 서비스입니다. |
|instanceId| string| 이 식별자는 hello 리소스의 hello 이름 또는 hello 정규화 된 리소스 id입니다. 자세한 내용은 [Azure Resource Manager API](https://docs.microsoft.com/rest/api/resources/resources)를 참조하세요. |
|serviceInfo1| string| 내부 Azure 서비스 메타데이터입니다. |
|serviceInfo2| string| 예를 들어, 가상 컴퓨터의 이미지 형식 및 ExpressRoute의 ISP 이름입니다. |
|additionalInfo| string| 서비스 특정 메타데이터입니다. 예를 들어 가상 컴퓨터용 이미지 형식입니다. |
|tags| string| 태그를 추가한 고객입니다. 자세한 내용은 [태그를 사용하여 Azure 리소스 구성](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-using-tags)을 참조하세요. |
|storeServiceIdentifier| string| 이 열이 사용되지 않습니다. 이전 버전과의 호환성을 위해 존재합니다. |
|departmentName| string| Hello 부서의 이름입니다. |
|costCenter| string| hello 사용과 연관 hello 비용 센터 |
|unitOfMeasure| string| Hello 서비스에 청구 되는 hello 단위를 식별 합니다. 예: GB, 시간, 10,000초 |
|resourceGroup| string| hello 리소스 그룹에서 실행 중인 배포 된 미터는 hello에 있습니다. 자세한 내용은 [Azure Resource Manager 개요](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)를 참조하세요. |
<br/>
## <a name="see-also"></a>참고 항목

* [청구 기간 API](billing-enterprise-api-billing-periods.md)

* [잔액 및 요약 API](billing-enterprise-api-balance-summary.md)

* [Marketplace 저장소 요금 API](billing-enterprise-api-marketplace-storecharge.md) 

* [가격표 API](billing-enterprise-api-pricesheet.md)
