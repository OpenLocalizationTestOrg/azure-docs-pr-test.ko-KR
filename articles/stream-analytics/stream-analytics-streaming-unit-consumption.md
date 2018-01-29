---
title: "Azure Stream Analytics: 스트리밍 단위 이해 및 조정 | Microsoft Docs"
description: "Azure Stream Analytics에서 성능 영향을 미치는 요소를 이해합니다."
keywords: "스트리밍 단위, 쿼리 성능"
services: stream-analytics
documentationcenter: 
author: JSeb225
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeanb
ms.openlocfilehash: e8812f10662ee7b571e8e353074c2537d1a3181b
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="understand-and-adjust-streaming-units"></a>스트리밍 단위 이해 및 조정

Azure Stream Analytics는 실행하는 작업의 성능 "가중치"를 SU(스트림 단위)에 집계합니다. SU는 작업을 실행하는 데 사용하는 컴퓨팅 리소스를 나타냅니다. SU는 CPU, 메모리의 혼합된 측정치 및 읽기/쓰기 속도를 기반으로 상대적 이벤트 처리 용량을 설명하는 방법을 제공합니다. 이 용량을 통해 사용자는 쿼리 논리에 집중할 수 있습니다. 또한 사용자가 저장소 계층 성능 고려 사항에 대해 알고, 작업에 대한 메모리를 수동으로 할당하고, 작업을 시기적절하게 실행하는 데 필요한 CPU 코어 수를 예상할 필요가 없어집니다.

Azure Stream Analytics 작업은 대기 시간이 짧은 스트리밍 처리를 위해 모든 처리를 메모리 안에서 수행합니다. 메모리가 부족하면 스트리밍 작업이 실패합니다. 결과적으로, 프로덕션 작업의 경우 스트리밍 작업의 리소스 사용을 모니터링하고 작업을 중단 없이 실행하기에 충분한 리소스가 할당되도록 확인해야 합니다.

메트릭은 0~100% 범위의 백분율 수치입니다. 최소 사용되는 스트리밍 작업의 경우 SU % 사용률 메트릭은 보통 10~20% 범위입니다. 경우에 따른 사용량 급증을 대비하여 메트릭을 80% 이하로 유지하는 것이 가장 좋습니다.  메트릭에 대한 경고를 설정할 수 있습니다(여기의 [메트릭 경고 설정 방법](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-alerts-portal) 참조).



## <a name="configure-stream-analytics-streaming-units-sus"></a>Stream Analytics 스트리밍 단위(SU) 구성
1. [Azure Portal](http://portal.azure.com/)에 로그인합니다.
2. 리소스 목록에서 확장할 Stream Analytics 작업을 찾은 후 엽니다. 
3. 작업 페이지의 구성 아래에서 **비율 크기 조정**을 클릭합니다. 

    ![Azure Portal Stream Analytics 작업 구성][img.stream.analytics.preview.portal.settings.scale]
    
4. 슬라이더를 사용하여 작업에 대한 SU를 설정합니다. 특정 SU 설정으로 제한되는 것을 확인합니다. 


## <a name="monitor-job-performance"></a>작업 성능 모니터링
Azure Portal을 사용하여 작업 처리량을 추적할 수 있습니다.

![Azure Stream Analytics 모니터링 작업][img.stream.analytics.monitor.job]

워크로드의 예상 처리량을 계산합니다. 처리량이 예상보다 더 작은 경우 입력 파티션을 조정하고, 쿼리를 조정하고, 작업에 SU를 추가합니다.


## <a name="how-many-sus-are-required-for-a-job"></a>작업에 필요한 SU 수는?

특정 작업에 필요한 SU 수 선택은 입력에 대한 파티션 구성 및 작업에 정의된 쿼리에 따라 달라집니다. **비율 크기 조정** 블레이드를 사용하면 올바른 SU 수를 설정할 수 있습니다. 필요한 것보다 많은 SU를 할당하는 것이 좋습니다. Stream Analytics 처리 엔진은 메모리를 추가로 할당하는 비용으로 대기 시간과 처리량을 최적화합니다.

일반적으로 **파티션 기준**을 사용하지 않는 쿼리에 대해 6 SU로 시작하는 것이 좋습니다. 그런 다음 대표적인 데이터 양을 전달하고 SU % 사용률 메트릭을 시험한 후 SU 수를 수정하는 평가판 및 오류 메서드를 사용하여 가장 적절한 부분을 판단합니다.

올바른 SU 수 선택에 대한 자세한 내용은 [처리량을 높이기 위한 Azure Stream Analytic 작업 비율 크기 조정](stream-analytics-scale-jobs.md) 페이지를 참조하세요.

> [!Note]
> 특정 작업에 필요한 SU 수 선택은 입력에 대한 파티션 구성 및 작업에 정의된 쿼리에 따라 달라집니다. 작업에 대해 SU의 할당량까지 선택할 수 있습니다. 기본적으로 각 Azure 구독에는 특정 지역의 모든 분석 작업에 대해 최대 200개의 SU 할당량이 있습니다. 구독의 SU를 이 할당량을 초과하여 늘리려면 [Microsoft 지원](http://support.microsoft.com)에 문의하세요. 작업당 SU에 대한 유효한 값은 1, 3, 6이며 6 단위로 증가합니다.



## <a name="factors-increasing-su-utilization"></a>SU % 사용률이 증가하는 요인 
### <a name="stateful-query-logic"></a>상태 저장 쿼리 논리 
Azure Stream Analytics 작업의 고유한 기능 중 하나는 기간 이동 집계, 임시 조인 및 임시 분석 함수 등과 같은 상태 저장 처리를 수행하는 것입니다. 이 연산자 각각은 일부 상태를 유지합니다. 
#### <a name="windowed-aggregates"></a>기간 이동 집계
기간 이동 집계의 상태 크기는 그룹 x 연산자에서 그룹(카디널리티)의 수에 비례합니다. 예를 들어 다음 쿼리에서 clusterid와 연결된 수는 쿼리의 카디널리티입니다. 

    SELECT count(*)
    FROM input 
    GROUP BY  clusterid, tumblingwindow (minutes, 5)


앞의 쿼리에서 카디널리티가 커서 발생한 문제를 개선하기 위해 “clusterid”로 분할된 이벤트 허브에 이벤트를 보내고 아래 예제에서처럼 **PARTITION BY**를 사용하여 개별적으로 각 입력 파티션을 처리할 수 있습니다.


    SELECT count(*) 
    FROM PARTITION BY PartitionId
    GROUP BY PartitionId, clusterid, tumblingwindow (minutes, 5)

쿼리가 분할되면 여러 노드에 걸쳐 분산됩니다. 결과적으로, 각 노드로 들어오는 clusterid 수가 감소하여 그룹 x 연산자 카디널리티가 줄어듭니다. 

이벤트 허브 파티션은 단계를 줄이지 않아도 되도록 그룹 키로 분할되어야 합니다. 추가 세부 정보는 [여기](https://docs.microsoft.com/azure/event-hubs/event-hubs-overview)에서 다룹니다. 
#### <a name="temporal-join"></a>임시 조인
임시 조인의 상태 크기는 조인의 임시 위글 공간의 이벤트 수에 비례합니다. 즉 이벤트 입력 비율과 위글 공간 크기의 곱입니다. 

조인에서 일치하지 않는 이벤트 수는 쿼리에 대한 메모리 사용률에 영향을 줍니다. 다음 쿼리는 클릭을 유도하는 광고 노출을 찾는 것입니다.

    SELECT id
    FROM clicks 
    INNER JOIN, impressions ON impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10.

이 예제에서 광고는 많은 데 사용자가 거의 클릭하지 않는 경우 모든 이벤트를 timewindow에 있도록 해야 합니다. 사용된 메모리는 창 크기와 이벤트 속도에 비례합니다. 

이를 조치하기 위해 조인 키로 분할된 이벤트 허브에 이벤트를 보내고 다음과 같이 시스템이 **PARTITION BY**를 사용하여 별도로 각각의 입력 파티션을 처리할 수 있게 쿼리를 확장합니다.

    SELECT id
    FROM clicks PARTITION BY PartitionId
    INNER JOIN impressions PARTITION BY PartitionId 
    ON impression.PartitionId = clocks.PartitionId AND impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10 
</code>

쿼리가 분할되면 여러 노드에 걸쳐 분산됩니다. 결과적으로, 각 노드로 들어오는 이벤트 수가 감소하여 조인 창에 유지되는 상태 크기가 줄어듭니다. 
#### <a name="temporal-analytic-function"></a>임시 분석 함수
임시 분석 함수의 상태 크기는 이벤트 비율과 기간의 곱에 비례합니다. 조치는 임시 조인과 유사합니다. **PARTITION BY**를 사용하여 쿼리를 확장할 수 있습니다. 

### <a name="out-of-order-buffer"></a>잘못된 버퍼 
이벤트 순서 지정 구성 창에서 잘못된 버퍼 크기를 구성할 수 있습니다. 이 버퍼는 창의 기간에 대한 입력을 유지하고 순서를 재지정하는 데 사용됩니다. 버퍼 크기는 이벤트 입력 비율과 잘못된 창 크기의 곱에 비례합니다. 기본 창 크기는 0입니다. 

이를 조치하려면 **PARTITION BY**를 사용하여 쿼리를 확장합니다. 쿼리가 분할되면 여러 노드에 걸쳐 분산됩니다. 결과적으로, 각 노드로 들어오는 이벤트 수가 감소하여 각각의 순서 재지정 버퍼의 이벤트 수가 줄어듭니다. 

### <a name="input-partition-count"></a>입력 분할 개수  
작업 입력의 각 입력 파티션에는 버퍼가 있습니다. 입력 파티션 수가 클수록 이 작업이 더 많은 리소스를 소비합니다. 각 SU에 대해 Azure Stream Analytics는 대략 1MB/s를 처리할 수 있으므로 ASA SU 수와 이벤트 허브의 파티션 수에 맞추고자 할 수 있습니다. 일반적으로 1SU 작업은 파티션이 2개인 이벤트 허브에 적합합니다(이벤트 허브의 최소값). 이벤트 허브에 더 많은 파티션이 있으면 ASA 작업이 더 많은 리소스를 소비하지만 이벤트 허브에서 제공한 추가적인 처리량을 반드시 사용하는 것은 아닙니다. 6SU 작업의 경우 이벤트 허브에서 4 또는 8개 파티션이 필요할 수 있습니다. 파티션이 16개 이상인 이벤트 허브를 1SU 작업에서 사용하면 종종 과다한 리소스 사용으로 이어지므로 지양해야 합니다. 

### <a name="reference-data"></a>참조 데이터 
ASA의 참조 데이터는 빠른 조회를 위해 메모리에 로드됩니다. 현재 구현에서는 동일한 참조 데이터를 여러 번 조인하더라도 참조 데이터와의 각 조인 작업이 메모리에 참조 데이터의 사본을 유지합니다. **PARTITION BY**를 통한 쿼리의 경우 각 파티션은 참조 데이터의 사본을 유지하므로 파티션이 완전히 분리됩니다. 참조 데이터를 여러 파티션과 여러 차례 조인할 경우 승수 효과에 따라 메모리 사용이 갑자기 급증할 수 있습니다.  

#### <a name="use-of-udf-functions"></a>UDF 함수 사용
UDF 함수를 추가하면 Azure Stream Analytics가 JavaScript 런타임을 메모리에 로드합니다. 이것이 SU%에 영향을 주게 됩니다.


## <a name="get-help"></a>도움말 보기
추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.

## <a name="next-steps"></a>다음 단계
* [Azure Stream Analytics에서 병렬 처리 가능 쿼리 만들기](stream-analytics-parallelization.md)
* [처리량을 높이기 위한 Azure Stream Analytics 작업 비율 크기 조정](stream-analytics-scale-jobs.md)

<!--Image references-->

[img.stream.analytics.monitor.job]: ./media/stream-analytics-scale-jobs/StreamAnalytics.job.monitor-NewPortal.png
[img.stream.analytics.configure.scale]: ./media/stream-analytics-scale-jobs/StreamAnalytics.configure.scale.png
[img.stream.analytics.perfgraph]: ./media/stream-analytics-scale-jobs/perf.png
[img.stream.analytics.streaming.units.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsStreamingUnitsExample.jpg
[img.stream.analytics.preview.portal.settings.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsPreviewPortalJobSettings-NewPortal.png   
