---
title: "이벤트 허브 수신기와 함께 Azure 스트림 분석 aaaDebug | Microsoft Docs"
description: "Stream Analytics 작업에서 이벤트 허브 소비자 그룹을 고려하는 것에 대한 모범 사례를 쿼리합니다."
keywords: "이벤트 허브 제한, 소비자 그룹"
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
ms.openlocfilehash: 89821e6273151de43b5e42d907e547c939e24824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a>이벤트 허브 수신자를 사용하여 Azure Stream Analytics 디버그

작업에서 Azure 스트림 분석 tooingest 또는 출력 데이터에서 Azure 이벤트 허브를 사용할 수 있습니다. 이벤트 허브를 사용 하기 위한 가장 좋은 방법은 toouse 여러 소비자 그룹, tooensure 작업 확장성. 그러한 이유 중 하나는 특정 입력에 대 한 hello Stream Analytics 작업에서 독자 수 hello hello는 하나의 소비자 그룹의 판독기 수에 영향을 줍니다. 수신자의 정확한 수 hello hello 확장 기술 논리에 대 한 내부 구현 세부 정보를 기반으로 합니다. 수신자 수가 hello 외부적으로 노출 되지 않습니다. hello 작업 시작 시간에 또는 업그레이드 작업 동안 판독기의 hello 변호가 달라질 수 있습니다.

> [!NOTE]
> 작업 업그레이드 하는 동안 hello 판독기 수 변경 되 면 일시적인 경고 tooaudit 로그 기록 됩니다. Stream Analytics 작업은 자동으로 이러한 일시적인 문제를 복구합니다.

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a>파티션당 판독기 수가 5개 이벤트 허브 제한을 초과

Hello 다음 포함 하는 시나리오는 hello 파티션당 독자 수 hello 이벤트 허브 제한 5 개를 초과 했습니다.

* 여러 SELECT 문이: 너무 참조 하는 여러 SELECT 문을 사용 하는 경우**동일한** 이벤트 허브 입력 하 고, 각 SELECT 문은 만든 새 수신기 toobe 발생 합니다.
* UNION: 공용 구조체를 사용할 경우에 가능한 toohave toohello 참조 하는 여러 개의 입력 **동일한** 이벤트 허브 및 소비자 그룹입니다.
* 셀프 조인은: 자체 조인 작업을 사용 하면 경우에 가능한 toorefer toohello **동일한** 이벤트 허브 여러 번입니다.

## <a name="solution"></a>해결 방법

hello 다음 모범 사례 완화 시킬 수 있습니다 시나리오는 hello에 파티션당 독자 수는 5 개의 hello 이벤트 허브 제한을 초과 합니다.

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a>WITH 절을 사용하여 쿼리를 여러 단계로 분할

hello WITH 절 hello 쿼리의 FROM 절에서 참조 될 수 있는 임시로 명명 된 결과 집합을 지정 합니다. Hello 실행 범위는 단일 SELECT 문이 hello WITH 절을 정의합니다.

예를 들어 아래 쿼리 대신,

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

다음 쿼리를 사용합니다.

```
WITH input (
   SELECT * FROM inputEventHub
) as data

SELECT foo
INTO output1
FROM data

SELECT bar
INTO output2
FROM data
…
```

### <a name="ensure-that-inputs-bind-toodifferent-consumer-groups"></a>입력 toodifferent 소비자 그룹을 바인딩하는 확인

3 개 이상의 입력은 연결 된 toohello는 쿼리에 대 한 동일한 이벤트 허브 소비자 그룹에서 별도 소비자 그룹을 만듭니다. 이렇게 하려면 추가 스트림 분석 입력 hello 생성 합니다.


## <a name="get-help"></a>도움말 보기
추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.

## <a name="next-steps"></a>다음 단계
* [소개 tooStream 분석](stream-analytics-introduction.md)
* [Stream Analytics 시작](stream-analytics-real-time-fraud-detection.md)
* [Stream Analytics 작업 크기 조정](stream-analytics-scale-jobs.md)
* [Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)
