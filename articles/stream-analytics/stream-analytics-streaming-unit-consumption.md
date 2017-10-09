---
title: "Azure 스트림 분석: 사용자 작업 toouse 스트리밍 단위를 효율적으로 최적화 | Microsoft Docs"
description: "Azure Stream Analytics의 크기 조정 및 확장에 대한 모범 사례를 쿼리합니다."
keywords: "스트리밍 단위, 쿼리 성능"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 5ad98b34d625190a879260f54c9eff0294e230cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-job-toouse-streaming-units-efficiently"></a>사용자 작업 toouse 스트리밍 단위를 효율적으로 최적화

Azure 스트림 분석 집계 hello 성능 "weight"의 스트리밍 단위 (SUs)에 작업을 실행 합니다. SUs는 hello 컴퓨팅 리소스를 소비 된 tooexecute 작업을 나타냅니다. SUs는 이벤트를 제공할 방법 toodescribe hello 상대 처리 용량은 CPU, 메모리의 복합된 측정에 기반 하 고 읽기 및 쓰기 속도로 합니다. 이 용량 확인할 수 있습니다 쿼리 논리 hello 설정 하 고 수동으로 작업에 대 한 메모리를 할당 하 고 적절 하 게에서 hello CPU 필요한 core-count toorun 작업 대략적인 필요 tooknow 저장소 계층 성능 고려 사항에서를 제거 합니다.

## <a name="how-many-sus-are-required-for-a-job"></a>작업에 필요한 SU 수는?

특정 작업에 대 한 필수 sus hello 번호를 선택 하는 작업은 hello 입력과 hello 작업 내에서 정의 된 hello 쿼리에 대 한 hello 파티션 구성에 따라 다릅니다. hello **배율** 블레이드 있습니다 tooset hello SUs 오른쪽 횟수입니다. 되기는 것 보다 더 많은 SUs tooallocate이 좋습니다. 대기 시간 및 추가 메모리 할당의 hello 비용에는 처리량에 대 한 hello 스트림 분석 처리 엔진을 최적화 합니다.

일반적으로 hello 모범 사례는 사용 하지 않는 쿼리에 대 한 6 SUs와 toostart *PARTITION BY*합니다. 그런 다음 대표 양의 데이터를 전달 하 고 hello SU % 사용률 메트릭을 검사 후 SUs hello 수가 수정 하는 시행 착오 메서드를 사용 하 여 hello 부분은 결정 합니다.

Azure 스트림 분석 처리를 시작 하기 전에 "재주문 버퍼" hello 라는 창에서 이벤트를 유지 합니다. 시간까지 hello 재주문 창 내 정렬 되어 있는 이벤트 및 후속 작업이 일시적으로 정렬 하는 hello 이벤트에서 수행 됩니다. 이벤트 시간으로 다시 정렬. 그러면 해당 hello 연산자에 모든 열로 표시 유형 조건 hello의 hello 이벤트 기간으로 규정 합니다. 또한 hello 연산자를 hello 필수 처리를 수행 하 고 출력을 생성할 수 있습니다. 이 메커니즘의 부작용은 처리 hello 순서 바꾸기 창의 hello 기간으로 지연 됩니다. hello 작업 (SU 소비 영향을 줌)의 hello 메모리 공간에는 그 안에 포함 된 이벤트의이 순서 바꾸기 창과 hello 번호의 hello 크기의 함수입니다.

> [!NOTE]
> 업그레이드 작업 중 hello 판독기 수 변경 되 면 일시적인 경고 tooaudit 로그 기록 됩니다. Stream Analytics 작업은 자동으로 이러한 일시적인 문제를 복구합니다.

## <a name="common-high-memory-causes-for-high-su-usage-for-running-jobs"></a>높은 공용 메모리로 인해 실행 중인 작업에 높은 SU 사용량 유발

### <a name="high-cardinality-for-group-by"></a>그룹화 기준에 대한 높은 카디널리티

들어오는 이벤트의 hello 카디널리티 hello 작업에 대 한 메모리 사용량을 나타냅니다.

예를 들어, `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, 연결 된 번호 hello **클러스터형** hello 쿼리의 hello 카디널리티는 합니다.

카디널리티가 높은으로 인해 toomitigate 문제 사용 하 여 파티션을 증가 하 여 hello 쿼리 확장 **PARTITION BY**합니다.

```
Select count(*) from input
Partition By clusterid
GROUP BY clustered tumblingwindow (minutes, 5)
```

수가 hello *클러스터 된* hello의 카디널리티는 GROUP BY 여기 됩니다.

Hello 쿼리를 분한 후 여러 노드를 분산 시키는 됩니다. 결과적으로, 각 노드에으로 들어오는 이벤트 hello 수가 줄어듭니다 차례로 hello hello 다시 정렬 버퍼 크기를 줄여주는. 또한 partitionid에 따라 이벤트 허브 파티션을 분할해야 합니다.

### <a name="high-unmatched-event-count-for-join"></a>JOIN에 대해 일치하지 않는 이벤트 개수가 많음

조인에 일치 하지 않는 이벤트의 hello 수가 hello 메모리 사용률이 hello 쿼리의 영향을 줍니다. 예를 들어 toofind hello 광고 노출 수 번의 클릭을 생성 하는 검색 하는 쿼리를 수행 합니다.

```
SELECT id from clicks INNER JOIN,
impressions on impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10
```

이 시나리오에서 많은 광고가 표시되고 몇 번의 클릭이 생성될 수 있습니다. 이러한 결과 hello 시간 창 내의 모든 hello 이벤트 hello 작업 tookeep 필요 합니다. 사용 되는 메모리 양은 hello 비례 toohello 창 크기와 이벤트 속도입니다. 

toomitigate PARTITION BY를 사용 하 여 이러한 상황을 늘려 hello 쿼리 확장 분할 합니다. 

Hello 쿼리를 분한 후 여러 처리 노드를 분산 시키는 됩니다. 결과적으로, 각 노드에으로 들어오는 이벤트 hello 수가 줄어듭니다 차례로 hello hello 다시 정렬 버퍼 크기를 줄여주는.

### <a name="large-number-of-out-of-order-events"></a>순서가 잘못된 이벤트 수가 많음 

큰 시간 창 내의 순서가 틀린 이벤트 수가 많은 hello hello "버퍼 순서" toobe 더 큰 크기를 하면 됩니다. PARTITION BY를 사용 하 여 toomitigate 배율 hello 쿼리를 늘려 이러한 상황을 분할 합니다. Hello 쿼리를 분한 후 여러 노드를 분산 시키는 됩니다. 결과적으로, 각 노드에으로 들어오는 이벤트 hello 수가 줄어듭니다 차례로 hello hello 다시 정렬 버퍼 크기를 줄여주는. 


## <a name="get-help"></a>도움말 보기
추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.

## <a name="next-steps"></a>다음 단계
* [스트림 분석 소개 tooAzure](stream-analytics-introduction.md)
* [Azure Stream Analytics 사용 시작](stream-analytics-real-time-fraud-detection.md)
* [Azure 스트림 분석 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)
