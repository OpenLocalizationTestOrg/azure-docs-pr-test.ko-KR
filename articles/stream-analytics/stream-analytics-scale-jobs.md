---
title: "스트림 분석 작업 tooincrease 처리량 aaaScale | Microsoft Docs"
description: "입력된 파티션 구성 hello 쿼리 정의 조정 하 고 설정 하 여 스트림 분석 작업 tooscale 스트리밍 단위를 작업 하는 방법에 대해 알아봅니다."
keywords: "데이터 스트리밍, 스트리밍 데이터 처리, 분석 조정"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 7e857ddb-71dd-4537-b7ab-4524335d7b35
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/22/2017
ms.author: jeffstok
ms.openlocfilehash: 4ba8f6b2f8bfebd52cfa07696b501b42cda21f75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-stream-analytics-jobs-tooincrease-stream-data-processing-throughput"></a>배율 Azure 스트림 분석 작업 tooincrease 스트림 데이터 처리 처리량
이 문서 tootune 스트림 분석에서 스트리밍 분석 작업에 대 한 tooincrease 처리량을 쿼리 하는 방법을 보여 줍니다. 스트림 분석 tooscale 입력된 파티션을 구성 하 여 작업 하는 방법을 알아보려면, 튜닝 hello 분석 쿼리를 정의 및 계산 하 고 설정 작업 *스트리밍 단위* (SUs). 

## <a name="what-are-hello-parts-of-a-stream-analytics-job"></a>스트림 분석 작업의 hello 부분 이란?
Stream Analytics 작업 정의에는 입력, 쿼리 및 출력이 포함됩니다. 입력은 위치 hello 작업에서 데이터 스트림을 hello를 읽습니다. hello 쿼리 사용 되는 tootransform hello 데이터 입력된 스트림의 이며 hello 출력 hello 작업이 hello 작업 결과 보냅니다.  

작업에는 데이터 스트림에 대해 하나 이상의 입력 소스가 필요합니다. hello 데이터 스트림 입력된 소스가 저장할 수 있습니다 또는 Azure blob 저장소에 Azure 이벤트 허브에서. 자세한 내용은 참조 [스트림 분석 소개 tooAzure](stream-analytics-introduction.md) 및 [Azure 스트림 분석을 사용 하 여 시작](stream-analytics-real-time-fraud-detection.md)합니다.

## <a name="partitions-in-event-hubs-and-azure-storage"></a>이벤트 허브와 Azure Storage의 파티션
스트림 분석 작업 크기 조정에서는 hello 입력 또는 출력에 파티션 활용 합니다. 분할을 통해 데이터를 파티션 키에 따라 하위 집합으로 분할할 수 있습니다. Hello 데이터 (예: 스트리밍 분석 작업의 경우)를 사용 하는 프로세스는 소비 하며 처리량을 향상 시키는 동시에 서로 다른 파티션을 작성 합니다. Streaming Analytics로 작업할 때 이벤트 허브 및 Blob Storage에서 분할을 활용할 수 있습니다. 

파티션에 대 한 자세한 내용은 다음 문서는 hello 참조:

* [Event Hubs 기능 개요](../event-hubs/event-hubs-features.md#partitions)
* [데이터 분할](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a>SU(스트리밍 단위)
스트리밍 단위 (SUs) 나타내는 hello 리소스 및에서 필요한 컴퓨팅 tooexecute Azure 스트림 분석 작업 순서. SUs는 이벤트를 제공할 방법 toodescribe hello 상대 처리 용량은 CPU, 메모리의 복합된 측정에 기반 하 고 읽기 및 쓰기 속도로 합니다. SU를 각 해당 tooroughly 1 m B/초의 처리량입니다. 

개수 SUs 선택는 hello 작업에 대해 정의 된 hello 쿼리 및 hello 입력에 대 한 hello 파티션 구성에 따라 결정 하는 특정 작업에 필요 합니다. 작업에 대 한 SUs tooyour 할당량을 선택할 수 있습니다. 기본적으로 각 Azure 구독에는 특정 지역에서 모든 hello 분석 작업에 대 한 too50 SUs의 할당량이 있습니다. 연락처가이 할당량을 초과 하면 구독에 대 한 SUs tooincrease [Microsoft 지원](http://support.microsoft.com)합니다. 작업당 SU에 대한 유효한 값은 1, 3, 6이며 6 단위로 증가합니다.

## <a name="embarrassingly-parallel-jobs"></a>병렬 처리가 적합한 작업
*병렬* 작업은 Azure 스트림 분석에 있는 hello 가장 확장성이 높은 시나리오입니다. Hello 출력의 hello 쿼리 tooone 파티션의 hello 입력된 tooone 인스턴스 중 한 파티션에 연결 됩니다. 이 병렬 처리 요구 사항을 준수 하는 hello에 있습니다.

1. 같은 키 처리 되 고 hello에 종속 되는 쿼리 논리 인스턴스를 쿼리할 동일 hello에서, hello 이벤트 toohello 이동 하 고 있는지 확인 해야 입력의 같은 파티션을 합니다. 이벤트 허브에 대 한이 hello 이벤트 데이터가지고 있어야 함을 의미 hello **PartitionKey** 값이 설정 합니다. 또는 분할된 보낸 사람을 사용할 수 있습니다. Blob 저장소에 대 한 즉 hello 이벤트는 전송 toohello 같은 파티션 폴더입니다. 쿼리 논리 같은 키 처리 toobe hello 필요 하지 않은 경우 인스턴스를 쿼리할 동일 hello 하 여,이 요구 사항을 무시할 수 있습니다. 이 논리에 대한 예로 간단한 선택/프로젝트/필터 쿼리를 참조하세요.  

2. Hello 데이터 레이아웃을 hello 입력 쪽 되 면 쿼리 분할 되어 있는지 확인 해야 합니다. 이 옵션을 toouse **Partition By** 모든 hello 단계에 있습니다. 여러 단계 수 있지만 hello 분할 해야 모두 동일한 키입니다. 분할 키 hello를 너무 설정 되어 있어야 현재**PartitionId** hello 작업 toobe 병렬 완벽 하 게 하려면에서.  

3. 현재는 이벤트 허브 및 Blob Storage만 분할된 출력을 지원합니다. 이벤트 허브 출력에 대 한 파티션 키 toobe hello 구성 해야 **PartitionId**합니다. Blob 저장소 출력에 대 한 않아도 toodo 아무 것도 있습니다.  

4. hello 입력된 파티션 수와 hello 출력 파티션 수가 같아야 합니다. Blob Storage 출력은 현재 파티션을 지원하지 않습니다. 하지만 괜찮습니다, 파티션 구성표 hello 업스트림 쿼리의 hello 상속 되므로 합니다. 다음은 완전한 병렬 작업을 허용하는 파티션 값의 예입니다.  

   * 8개의 이벤트 허브 입력 파티션 및 8개의 이벤트 허브 출력 파티션
   * 8개의 이벤트 허브 입력 파티션 및 Blob Storage 출력  
   * 8개의 Blob Storage 입력 파티션 및 Blob Storage 출력  
   * 8개의 Blob Storage 입력 파티션 및 8개의 이벤트 허브 출력 파티션  

hello 다음 섹션에서는 설명 병렬는 몇 가지 예제 시나리오입니다.

### <a name="simple-query"></a>단순 쿼리

* 입력: 8개의 파티션이 있는 이벤트 허브
* 출력: 8개의 파티션이 있는 이벤트 허브

쿼리:

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

이 쿼리는 간단한 필터입니다. 따라서 tooworry toohello 이벤트 허브 전송 되는 hello 입력을 분할 하는 방법에 대 한 필요 하지 않습니다. 해당 hello 쿼리에 포함 되어 **파티션에 의해 PartitionId**앞에서 #2 요건을 충족 하기 때문입니다. Hello 출력에 대 한 필요 tooconfigure hello 이벤트 허브 출력 hello 작업 toohave hello 파티션 키 집합에 너무**PartitionId**합니다. 하나 이상의 마지막 검사 toomake hello 입력된 파티션 수가 출력 파티션의 수를 같은 toohello 인지입니다.

### <a name="query-with-a-grouping-key"></a>그룹화 키가 있는 쿼리

* 입력: 8개의 파티션이 있는 이벤트 허브
* 출력: Blob Storage

쿼리:

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

이 쿼리에 그룹화 키가 있습니다. 따라서 hello 같은 핵심 요구 toobe 같은 이벤트 보내야 한다고 toohello 이벤트 허브는 분할 방식에서 즉 인스턴스를 쿼리 하는 hello에서 처리 합니다. 하지만 어떤 키를 사용해야 하나요? **PartitionId**는 작업 논리 개념입니다. 실제로 신경을 hello 키가 **TollBoothId**, 따라서 hello **PartitionKey** hello 이벤트 데이터의 값은 **TollBoothId**합니다. 설정 하 여 hello 쿼리에서 수행할이 **Partition By** 너무**PartitionId**합니다. Hello 출력 blob 저장소 이므로 tooworry #4 요구 사항에 따라 파티션 키 값을 구성 하는 방법에 대 한 필요 하지 않습니다.

### <a name="multi-step-query-with-a-grouping-key"></a>그룹화 키가 있는 다중 단계 쿼리
* 입력: 8개의 파티션이 있는 이벤트 허브
* 출력: 8개의 파티션이 있는 이벤트 허브 인스턴스

쿼리:

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

이 쿼리에 그룹화 키, 같은 핵심 요구 toobe hello에 의해 처리 되므로 hello 동일한 쿼리 인스턴스에 있습니다. 사용 하는 hello hello 이전 예제와 같이 동일한 전략입니다. 이 경우 hello 쿼리는 여러 단계가 있습니다. 각 단계에 **Partition By PartitionId**가 있나요? 예, hello 쿼리 #3 요건을 충족 합니다. Hello 출력에 대 한 필요 tooset hello 파티션 키 너무**PartitionId**앞서 설명한 것 처럼, 합니다. Hello 있다는 것도 확인할 수 있습니다 hello 입력으로 동일한 수의 파티션 합니다.

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a>병렬 처리가 적합하지 *않은* 예제 시나리오

Hello 이전 섹션에서 몇 가지 병렬 시나리오 했죠. 이 섹션에서는 모든 hello 요구 사항 toobe 병렬 일치 하지 않는 시나리오에 설명 합니다. 

### <a name="mismatched-partition-count"></a>일치하지 않는 파티션 수
* 입력: 8개의 파티션이 있는 이벤트 허브
* 출력: 32개의 파티션이 있는 이벤트 허브

중요 하지 않습니다는 경우 어떤 hello 쿼리가 됩니다. Hello 입력된 파티션 수에는 hello 출력 파티션 수와 일치 하지 않으면, hello 토폴로지 병렬 하지 않습니다.

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a>이벤트 허브 또는 Blob Storage를 출력으로 사용하지 않음
* 입력: 8개의 파티션이 있는 이벤트 허브
* 출력: PowerBI

PowerBI 출력은 현재 분할을 지원하지 않습니다. 따라서 이 시나리오는 병렬 처리가 적합하지 않습니다.

### <a name="multi-step-query-with-different-partition-by-values"></a>서로 다른 Partition By 값이 있는 다중 단계 쿼리
* 입력: 8개의 파티션이 있는 이벤트 허브
* 출력: 8개의 파티션이 있는 이벤트 허브

쿼리:

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

Hello 두 번째 단계에 사용 하 여 볼 수 있듯이 **TollBoothId** hello 분할 키로 합니다. Hello 첫 번째 단계로, 동일를이 단계는 hello 하지 있으며 따라서 있어야 우리 toodo 한 순서 섞기 합니다. 

hello 앞의 예제에서는 일부 스트림 분석 작업을 보여 줍니다 병렬 토폴로지 너무 준수 (또는 안 함). 준수 수행 하는 경우 hello 잠재력을 최대한 갖습니다. 이러한 프로필 중 하나에 적합하지 않는 작업의 경우 향후 업데이트에서 크기 조정 지침이 제공될 예정입니다. 지금은 hello 다음 섹션에에서 hello 일반적인 지침을 사용 합니다.

## <a name="calculate-hello-maximum-streaming-units-of-a-job"></a>작업의 최대 스트리밍 단위를 hello를 계산 합니다.
hello 총 스트림 분석 작업에서 사용할 수 있는 스트리밍 단위 수가 hello 작업과 hello 각 단계에 대 한 파티션 수에 대 한 정의 된 hello 쿼리 단계 hello 수에 따라 달라 집니다.

### <a name="steps-in-a-query"></a>쿼리의 단계
하나의 쿼리에는 하나 이상의 단계가 있을 수 있습니다. 각 단계는 hello에 정의 된 하위 쿼리 **WITH** 키워드입니다. hello 밖에 있는 hello 쿼리 **WITH** 키워드 (하나의 쿼리에만 해당) hello 같은 단계로 계산 **선택** 다음 쿼리에서 hello에 문의:

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

이 쿼리에는 2개의 단계가 있습니다.

> [!NOTE]
> 이 쿼리는 hello 문서 뒷부분에 보다 자세히 설명 합니다.
>  

### <a name="partition-a-step"></a>단계 분할
분할 된 단계가 hello를 조건 다음 사항이 필요 합니다.

* hello 입력된 소스를 분할 되어야 합니다. 
* hello **선택** hello 쿼리 문은 분할 된 입력된 소스에서 읽어야 합니다.
* hello 단계 내에서 hello 쿼리 hello 있어야 **Partition By** 키워드입니다.

쿼리를 분할 hello 입력된 이벤트는 별도 파티션을 처리 하 고에서 집계 된 그룹 및 출력 이벤트는 각각 hello 그룹에 대해 생성 됩니다. 집계를 결합된 하려는 경우 두 번째 단계 분할 되지 않은 tooaggregate를 만들어야 합니다.

### <a name="calculate-hello-max-streaming-units-for-a-job"></a>Hello 최대 스트리밍 단위는 작업에 대 한 계산
분할 되지 않은 모든 단계는 함께 toosix 스트리밍 단위 (SUs) 스트림 분석 작업에 대 한를 확장할 수 있습니다. tooadd SUs는 한 단계를 분할 되어야 합니다. 각 파티션에는 6개의 SU가 있을 수 있습니다.

<table border="1">
<tr><th>쿼리</th><th>Hello 작업에 대 한 최대 SUs</th></td>

<tr><td>
<ul>
<li>hello 쿼리 한 단계를 포함합니다.</li>
<li>hello 단계 분할할 수 없습니다.</li>
</ul>
</td>
<td>6</td></tr>

<tr><td>
<ul>
<li>hello 입력된 데이터 스트림은 3으로 분할 됩니다.</li>
<li>hello 쿼리 한 단계를 포함합니다.</li>
<li>hello 단계 분할 됩니다.</li>
</ul>
</td>
<td>18</td></tr>

<tr><td>
<ul>
<li>hello 쿼리에 두 단계가 있습니다.</li>
<li>Hello 단계 모두 분할 됩니다.</li>
</ul>
</td>
<td>6</td></tr>

<tr><td>
<ul>
<li>hello 입력된 데이터 스트림은 3으로 분할 됩니다.</li>
<li>hello 쿼리에 두 단계가 있습니다. hello 입력된 단계를 분할 및 hello 두 번째 단계는 하지 않습니다.</li>
<li>hello <strong>선택</strong> 문은 분할 hello 입력에서 읽습니다.</li>
</ul>
</td>
<td>24(분할된 단계에 대한 18+분할되지 않은 단계에 대한 6)</td></tr>
</table>

### <a name="examples-of-scaling"></a>크기 조정 예제

hello 다음 쿼리 수를 계산 hello 자동차에 세 개의 tollbooths 유료 스테이션을 진행 하 고 3 분 창 내에서. 이 쿼리는 toosix SUs 확장할 수 있습니다.

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

더 많은 toouse SUs에 대 한 쿼리 hello, 입력된 데이터 스트림을 hello 둘 다 및 hello 쿼리를 분할 해야 합니다. Hello 데이터 스트림 파티션 too3, 설정 되었으므로 hello 다음 수정 된 쿼리를 확장할 수 있습니다 too18 SUs:

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

쿼리를 분할 hello 입력된 이벤트 처리 되 고 별도 파티션 그룹에 집계 합니다. 출력 이벤트의 각 hello 그룹에 대해 생성 됩니다. 분할 때 hello에 일부 예기치 않은 결과가 발생할 수 있습니다 **GROUP BY** hello 입력된 데이터 스트림에 hello 파티션 키 필드가 아닙니다. 예를 들어 hello **TollBoothId** hello 이전 쿼리에서 필드의 hello 파티션 키 않습니다 **Input1**합니다. hello 결과 해당 hello 여러 파티션에 톨게이트 # 1에서 데이터를 분산 시킬 수 있습니다.

각 hello **Input1** 스트림 분석 하 여 파티션을 별도로 처리 됩니다. 결과적으로, 여러 레코드의 hello 자동차 수 hello 동일한 요금에 hello 같은 텀블 링 창 생성 됩니다. Hello 입력된 파티션 키를 변경할 수 없는 경우에 다음 예제는 hello와 같이 아닌 파티션 단계를 추가 하 여이 문제를 해결할 수 있습니다.:

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

이 쿼리는 크기 조정 된 too24 SUs 될 수 있습니다.

> [!NOTE]
> 두 스트림을 조인 하는 경우는 hello 스트림을 분할 된 hello 열의 hello 파티션 키로 toocreate hello 조인을 사용 하 여 있는지 확인 합니다. 또한 hello 했는지를 확인 동일한 수의 파티션 두 스트림이 모두에 있습니다.
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a>Stream Analytics 스트리밍 단위 구성

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. 리소스의 hello 목록에서 tooscale 원하고 엽니다 hello 스트림 분석 작업을 찾습니다.
3. Hello 블레이드에서 아래에서 작업 **구성**, 클릭 **배율**합니다.

    ![Azure Portal Stream Analytics 작업 구성][img.stream.analytics.preview.portal.settings.scale]

4. Hello 작업에 대 한 hello 슬라이더 tooset hello SUs를 사용 합니다. 제한 된 toospecific SU 설정이 있는지 확인 합니다.


## <a name="monitor-job-performance"></a>작업 성능 모니터링
Hello Azure 포털을 사용 하는 작업의 hello 처리량을 추적할 수 있습니다.

![Azure Stream Analytics 모니터링 작업][img.stream.analytics.monitor.job]

Hello 워크 로드의 hello 예상 처리량을 계산 합니다. Hello 처리량 예상 보다 작은 경우 hello 입력된 파티션 튜닝 하 hello 쿼리를 조정 하 고 SUs tooyour 작업을 추가.


## <a name="visualize-stream-analytics-throughput-at-scale-hello-raspberry-pi-scenario"></a>최대 규모로 처리량 스트림 분석 시각화: hello 라스베리 Pi 시나리오
스트림 분석 작업 확장 하는 방법을 이해 toohelp, 라스베리 Pi 장치에서 입력을 기반으로 하는 실험을 수행 했습니다. 이 실험 사용 응 여러 스트리밍 단위와 파티션 처리량에 hello 결과 확인할 수 있습니다.

이 시나리오에서는 hello 장치 센서 데이터 (클라이언트) tooan 이벤트 허브를 보냅니다. 스트리밍 분석 hello 데이터를 처리 하 고 출력 tooanother 이벤트 허브로 경고나 통계를 보냅니다. 

클라이언트 hello JSON 형식의 센서 데이터를 보냅니다. hello 데이터 출력 JSON 형식 이기도합니다. hello 데이터는 다음과 같습니다.

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

다음 쿼리는 hello 광원이 해제 되어 사용 되는 toosend 경고입니다.

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a>처리량 측정

이 컨텍스트에서 처리량이 hello 용량 고정된 된 양의 시간에서 스트림 분석에서 처리 하는 입력된 데이터입니다. (측정 했습니다 10 분 동안.) hello에 대 한 tooachieve hello 최상의 처리 처리량 입력 데이터, 두 hello 데이터 스트림 입력 및 hello 쿼리 분할 되었습니다. 포함 **count ()** hello 쿼리 toomeasure 입력된 이벤트 수 처리 되었습니다. 입력된 이벤트 toocome toomake 있는지 hello 작업이 단순히 대기 하지, hello 입력된 이벤트 허브의 각 파티션에 약 300MB 입력된 데이터의 미리 채워진 되었습니다.

hello 다음 표에 hello 결과가 나와 hello 스트리밍 단위 수가 증가 하 고 hello 해당 파티션 수를 이벤트 허브에 살펴보았습니다.  

<table border="1">
<tr><th>입력 파티션</th><th>출력 파티션</th><th>스트리밍 단위</th><th>지속적인 처리량
</th></td>

<tr><td>12</td>
<td>12</td>
<td>6</td>
<td>4.06MB/초</td>
</tr>

<tr><td>12</td>
<td>12</td>
<td>12</td>
<td>8.06 MB/초</td>
</tr>

<tr><td>48</td>
<td>48</td>
<td>48</td>
<td>38.32 MB/초</td>
</tr>

<tr><td>192</td>
<td>192</td>
<td>192</td>
<td>172.67 MB/초</td>
</tr>

<tr><td>480</td>
<td>480</td>
<td>480</td>
<td>454.27 MB/초</td>
</tr>

<tr><td>720</td>
<td>720</td>
<td>720</td>
<td>609.69 MB/초</td>
</tr>
</table>

되며 hello 다음 그래프에서는 SUs 및 처리량 사이의 hello 관계를 시각화 합니다.

![img.stream.analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a>도움말 보기
추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.

## <a name="next-steps"></a>다음 단계
* [스트림 분석 소개 tooAzure](stream-analytics-introduction.md)
* [Azure Stream Analytics 사용 시작](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->

[img.stream.analytics.monitor.job]: ./media/stream-analytics-scale-jobs/StreamAnalytics.job.monitor-NewPortal.png
[img.stream.analytics.configure.scale]: ./media/stream-analytics-scale-jobs/StreamAnalytics.configure.scale.png
[img.stream.analytics.perfgraph]: ./media/stream-analytics-scale-jobs/perf.png
[img.stream.analytics.streaming.units.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsStreamingUnitsExample.jpg
[img.stream.analytics.preview.portal.settings.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsPreviewPortalJobSettings-NewPortal.png   

<!--Link references-->

[microsoft.support]: http://support.microsoft.com
[azure.management.portal]: http://manage.windowsazure.com
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

