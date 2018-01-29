---
title: "공급자 리소스 사용량 API | Microsoft Docs"
description: "Azure 스택 사용 정보를 검색 하는 API에서 리소스 사용량에 대 한 참조"
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: b6055923-b6a6-45f0-8979-225b713150ae
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: alfredop
ms.openlocfilehash: 0c45ce3bc93945ed8700464beebabcda07e8d77c
ms.sourcegitcommit: dfd49613fce4ce917e844d205c85359ff093bb9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/31/2017
---
# <a name="provider-resource-usage-api"></a>공급자 리소스 사용 API
용어 *공급자* 서비스 관리자와 위임 된 모든 공급자 적용 됩니다. Azure 스택 연산자 및 위임 된 공급자 API 공급자 사용을 사용 하 여 직접 테 넌 트의 사용량을 볼 수 있습니다. 예를 들어 다이어그램에 나와 있는 것 처럼 P0 수 p 1의에서 사용 정보를 보려면 API 공급자 호출 하 고 P1 및 p 2의 직접 사용 수 P3 및 P4 대 한 사용 정보에 대 한 합니다.

![공급자 계층 구조 개념적 모델](media/azure-stack-provider-resource-api/image1.png)

## <a name="api-call-reference"></a>API 호출 참조
### <a name="request"></a>요청
요청 요청 된 구독에 대 한 및 요청 된 시간 프레임에 대 한 사용량 세부 정보를 가져옵니다. 요청 본문이 없습니다.

이 사용량 API 공급자 API, 이므로 호출자에 게는 프로그램 소유자, 참가자 또는 판독기 역할 공급자의 구독에 할당 되어야 합니다.

| **메서드** | **요청 URI** |
| --- | --- |
| GET |https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/subscriberUsageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}& subscriberId {sub1.1} = & api 버전 2015-06-01-미리 보기 = & continuationToken = {value 토큰} |

### <a name="arguments"></a>인수
| **인수** | **설명** |
| --- | --- |
| *armendpoint* |Azure 스택 환경을 azure 리소스 관리자 끝점입니다. Azure 스택 규칙은 Azure 리소스 관리자 끝점의 이름이 형식에서 `https://adminmanagement.{domain-name}`합니다. 예를 들어 도메인 이름이 개발 키트에 대 한 *local.azurestack.external*, 리소스 관리자 끝점은 `https://adminmanagement.local.azurestack.external`합니다. |
| *subId* |호출을 수행 하는 사용자의 구독 ID입니다. |
| *reportedStartTime* |쿼리를 시작 합니다. 에 대 한 값 *DateTime* utc (협정 세계시) 및 예를 들어 13시 시간 시작 부분에 있어야 합니다. 매일 집계에 대 한이 값을 UTC 자정으로 설정 합니다. 형식은 *이스케이프* ISO 8601 합니다. 예를 들어 *2015-06-16T18% 3a53% 3a11% 2b00 %3a00Z*를 콜론은 이스케이프 여기서 *%3a* 더하기로 이스케이프 됩니다 및 *%2b* uri 되도록 합니다. |
| *reportedendtime의* |쿼리의 종료 시간입니다. 에 적용 되는 제약 조건은 *reportedStartTime* 이 인수에도 적용 합니다. 에 대 한 값 *reportedendtime의* 또는 현재 날짜는 미래 날짜 일 수 없습니다. 인 경우 결과로 설정 "처리 되지 완료 합니다." |
| *aggregationGranularity* |두 불연속 잠재적인 값을 포함 하는 선택적 매개 변수: 매일, 매시간 합니다. 값을 제안 하는 대로 매일 세분성의 데이터를 반환 하나 고 다른 하나는 시간별 해상도입니다. 일별 옵션이 기본 옵션입니다. |
| *subscriberId* |구독 ID가 표시됩니다. 필터링 된 데이터를 가져오려면 공급자의 직접 테 넌 트의 구독 ID가 필요 합니다. 지정 된 구독 ID 매개 호출에서 공급자의 모든 직접 테 넌 트에 대 한 사용 현황 데이터를 반환 합니다. |
| *api 버전* |이 요청에 사용 되는 프로토콜의 버전입니다. 이 값은로 설정 *2015-06-01-미리 보기*합니다. |
| *continuationToken* |사용량 API 공급자에 대 한 마지막 호출에서 토큰이 검색 합니다. 이 토큰 응답 줄 1, 000 보다 크면 하 고 동작 하는 진행률에 대 한 책갈피가 필요 합니다. 토큰이 없는 경우 일의 시작 부분에서 데이터를 검색 또는 시간, 세분성에 따라 전달 합니다. |

### <a name="response"></a>응답
/Subscriptions/sub1/providers/Microsoft.Commerce/subscriberUsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00 및 reportedendtime의 가져오기 2015-06-01T00% 3a00% 3a00% 2b00 %3a00 = & aggregationGranularity 매일 & subscriberId = = sub1.1 &에서 api-version = 1.0

```json
{
"value": [
{

"id":
"/subscriptions/sub1.1/providers/Microsoft.Commerce/UsageAggregate/sub1.1-

meterID1",
"name": "sub1.1-meterID1",
"type": "Microsoft.Commerce/UsageAggregate",

"properties": {
"subscriptionId":"sub1.1",
"usageStartTime": "2015-03-03T00:00:00+00:00",
"usageEndTime": "2015-03-04T00:00:00+00:00",
"instanceData":"{\"Microsoft.Resources\":{\"resourceUri\":\"resourceUri1\",\"location\":\"Alaska\",\"tags\":null,\"additionalInfo\":null}}",
"quantity":2.4000000000,
"meterId":"meterID1"

}
},

…
```

### <a name="response-details"></a>응답 세부 정보
| **인수** | **설명** |
| --- | --- |
| *id* |사용 현황 집계의 고유 ID입니다. |
| *name* |사용 현황 집계의 이름입니다. |
| *type* |리소스 정의 합니다. |
| *subscriptionId* |Azure 스택 사용자의 구독 id입니다. |
| *usageStartTime* |UTC 시작 시간이 사용 현황 집계가 속하는 사용 현황 버킷의입니다.|
| *usageEndTime* |이 사용 현황 집계가 속하는 사용 현황 버킷의 UTC 종료 시간입니다. |
| *instanceData* |인스턴스 세부 정보 (에 새 형식)의 키-값 쌍:<br> *resourceUri*: 정규화 된 리소스 그룹 및 인스턴스 이름을 포함 하는 리소스 ID입니다. <br> *위치*:이 서비스를 실행 하는 영역입니다. <br> *태그*: 사용자가 지정한 리소스 태그입니다. <br> *additionalInfo*: 세부 정보 등 사용 된 리소스에 대 한 OS 버전 또는 이미지 유형입니다. |
| *수량* |이 시간 내에 발생 한 리소스 사용의 양입니다. |
| *meterId* |사용 된 리소스에 대 한 고유 ID (호출 또한 *ResourceID*). |

## <a name="next-steps"></a>다음 단계
[테 넌 트 리소스 사용량 API 참조](azure-stack-tenant-resource-usage-api.md)

[사용 관련 FAQ](azure-stack-usage-related-faq.md)
