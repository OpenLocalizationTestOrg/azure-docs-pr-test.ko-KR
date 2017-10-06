---
title: "스트림 분석의 일반적인 사용 패턴에 대 한 예제 aaaQuery | Microsoft Docs"
description: "일반적인 Azure Stream Analytics 쿼리 패턴"
keywords: "쿼리 예제"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jenniehubbard
editor: cgronlun
ms.assetid: 6b9a7d00-fbcc-42f6-9cbb-8bbf0bbd3d0e
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/08/2017
ms.author: jenniehubbard
ms.openlocfilehash: c8f7a8ac661eaf0281f4140b02c42141b73040fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a>일반적인 Stream Analytics 사용 패턴에 대한 쿼리 예제
## <a name="introduction"></a>소개
Azure Stream Analytics에서 쿼리는 SQL 방식 쿼리 언어로 표현됩니다. 이러한 쿼리는 hello에 설명 되어 [Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx) 가이드입니다. 이 문서 윤곽선 솔루션 tooseveral 공통 패턴을 기반으로 실제 시나리오를 쿼리 합니다. 작업을 진행 중 이며 toobe 지속적으로 새 패턴을 사용 하 여 업데이트를 계속 합니다.

## <a name="query-example-convert-data-types"></a>쿼리 예제: 데이터 형식 변환
**설명**: hello 입력 스트림에서 hello 유형의 속성을 정의 합니다.
예를 들어 hello 자동차 가중치 문자열로 입력된 스트림을 hello에 나오는 하며 너무 변환 toobe**INT** tooperform **SUM** 설정 합니다.

**입력**:

| 계정을 | Time | 무게 |
| --- | --- | --- |
| Honda |2015-01-01T00:오전 12:01.0000000Z |"1000" |
| Honda |2015-01-01T00:오전 12:02.0000000Z |"2000" |

**출력**:

| 계정을 | 무게 |
| --- | --- |
| Honda |3000 |

**솔루션**:

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

**설명**: 사용 하 여 한 **캐스트** hello에 문을 **가중치** toospecify 필드의 데이터 형식입니다. 지원 되는 데이터 형식 목록이 hello 참조 [데이터 형식 (Azure 스트림 분석)](https://msdn.microsoft.com/library/azure/dn835065.aspx)합니다.

## <a name="query-example-use-likenot-like-toodo-pattern-matching"></a>쿼리 예: Like/Not toodo 패턴 일치와 같은 사용
**설명**: hello 이벤트 필드 값을 특정 패턴과 일치 하는지 확인 하십시오.
예를 들어 hello 결과 번호판 A로 시작 하 고 9 끝나야 하는 반환 하는지 확인 합니다.

**입력**:

| 계정을 | LicensePlate | Time |
| --- | --- | --- |
| Honda |ABC-123 |2015-01-01T00:오전 12:01.0000000Z |
| Toyota |AAA-999 |2015-01-01T00:오전 12:02.0000000Z |
| Nissan |ABC-369 |2015-01-01T00:오전 12:03.0000000Z |

**출력**:

| 계정을 | LicensePlate | Time |
| --- | --- | --- |
| Toyota |AAA-999 |2015-01-01T00:오전 12:02.0000000Z |
| Nissan |ABC-369 |2015-01-01T00:오전 12:03.0000000Z |

**솔루션**:

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

**설명은**: 사용 하 여 hello **같은** 문 toocheck hello **LicensePlate** 필드 값입니다. A로 시작한 다음 0개 이상의 문자열을 포함하고 a9로 끝나야 합니다. 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a>쿼리 예제: 다른 사례/값(CASE 문)에 대한 논리를 지정합니다.
**설명**: 특정 조건에 따라 필드에 대해 다른 계산을 제공합니다.
예를 들어 1에 대 한 특별 한 경우와 함께 확인 동일 hello의 개수 자동차를 전달 하는 것에 대 한 설명 문자열을 제공 합니다.

**입력**:

| 계정을 | Time |
| --- | --- |
| Honda |2015-01-01T00:오전 12:01.0000000Z |
| Toyota |2015-01-01T00:오전 12:02.0000000Z |
| Toyota |2015-01-01T00:오전 12:03.0000000Z |

**출력**:

| CarsPassed | Time |
| --- | --- | --- |
| 1 Honda |2015-01-01T00:오전 12:10.0000000Z |
| 2 Toyotas |2015-01-01T00:오전 12:10.0000000Z |

**솔루션**:

    SELECT
        CASE
            WHEN COUNT(*) = 1 THEN CONCAT('1 ', Make)
            ELSE CONCAT(CAST(COUNT(*) AS NVARCHAR(MAX)), ' ', Make, 's')
        END AS CarsPassed,
        System.TimeStamp AS Time
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

**설명은**: hello **대/소문자** 절 (경우에는 hello 집계 창에 있는 hello 자동차의 hello 수)에 몇 가지 조건에 따라 다른 계산 tooprovide 수 있습니다.

## <a name="query-example-send-data-toomultiple-outputs"></a>쿼리 예: 데이터 toomultiple 출력 보내기
**설명**: 송신 데이터 toomultiple 단일 작업에서 대상 출력 합니다.
예를 들어 임계값 기반 경고에 대 한 데이터를 분석 하 고 모든 이벤트 tooblob 저장소를 보관 합니다.

**입력**:

| 계정을 | Time |
| --- | --- |
| Honda |2015-01-01T00:오전 12:01.0000000Z |
| Honda |2015-01-01T00:오전 12:02.0000000Z |
| Toyota |2015-01-01T00:오전 12:01.0000000Z |
| Toyota |2015-01-01T00:오전 12:02.0000000Z |
| Toyota |2015-01-01T00:오전 12:03.0000000Z |

**출력1**:

| 계정을 | Time |
| --- | --- |
| Honda |2015-01-01T00:오전 12:01.0000000Z |
| Honda |2015-01-01T00:오전 12:02.0000000Z |
| Toyota |2015-01-01T00:오전 12:01.0000000Z |
| Toyota |2015-01-01T00:오전 12:02.0000000Z |
| Toyota |2015-01-01T00:오전 12:03.0000000Z |

**출력2**:

| 계정을 | Time | 개수 |
| --- | --- | --- |
| Toyota |2015-01-01T00:오전 12:10.0000000Z |3 |

**솔루션**:

    SELECT
        *
    INTO
        ArchiveOutput
    FROM
        Input TIMESTAMP BY Time

    SELECT
        Make,
        System.TimeStamp AS Time,
        COUNT(*) AS [Count]
    INTO
        AlertOutput
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)
    HAVING
        [Count] >= 3

**설명은**: hello **INTO** 절이이 문에의 hello toowrite hello 데이터 toofrom 출력 하는 스트림 분석을 지시 합니다.
hello 첫 번째 쿼리는 이름을 tooan 출력을 수신 했습니다. hello 데이터의 통과 **ArchiveOutput**합니다.
hello 두 번째 쿼리는 몇 가지 간단한 집계 및 필터링 및 그 hello 결과 tooa 다운스트림 경고 시스템으로 보냅니다.

참고 hello 공통 테이블 식 (Cte)의 hello 결과 다시 사용할 수도 있습니다 (예: **WITH** 문) 여러 출력 문에서 합니다. 이 옵션에는 추가적인된 이점을 더 적은 판독기 toohello 입력된 소스를 열어 hello에 합니다.
예: 

    WITH AllRedCars AS (
        SELECT
            *
        FROM
            Input TIMESTAMP BY Time
        WHERE
            Color = 'red'
    )
    SELECT * INTO HondaOutput FROM AllRedCars WHERE Make = 'Honda'
    SELECT * INTO ToyotaOutput FROM AllRedCars WHERE Make = 'Toyota'

## <a name="query-example-count-unique-values"></a>쿼리 예제: 고유 값 계산
**설명**: hello hello 스트림의 시간 창 내에서 표시 되는 고유 필드 값 수를 계산 합니다.
예를 들어 개수 고유 하 게 2 초 창의 hello 요금 소 창구를 통과 하는 자동차의 사항

**입력**:

| 계정을 | Time |
| --- | --- |
| Honda |2015-01-01T00:오전 12:01.0000000Z |
| Honda |2015-01-01T00:오전 12:02.0000000Z |
| Toyota |2015-01-01T00:오전 12:01.0000000Z |
| Toyota |2015-01-01T00:오전 12:02.0000000Z |
| Toyota |2015-01-01T00:오전 12:03.0000000Z |

**출력:**

| 개수 | Time |
| --- | --- |
| 2 |2015-01-01T00:오전 12:02.000Z |
| 1 |2015-01-01T00:오전 12:04.000Z |

**해결 방법:**

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


**설명:**
**COUNT (DISTINCT 확인)** 반환 hello hello에 고유 값 수가 **확인** 시간 창 내의 열입니다.

## <a name="query-example-determine-if-a-value-has-changed"></a>쿼리 예제: 값이 변경되었는지 여부를 확인합니다.
**설명**: hello 현재 값과 다른 경우에 이전 값 toodetermine를 살펴봅니다.
예를 들어 켜져 hello 이전 자동차 hello 현재 자동차 만드는 동일 hello 유료도로 hello?

**입력**:

| 계정을 | Time |
| --- | --- |
| Honda |2015-01-01T00:오전 12:01.0000000Z |
| Toyota |2015-01-01T00:오전 12:02.0000000Z |

**출력**:

| 계정을 | Time |
| --- | --- |
| Toyota |2015-01-01T00:오전 12:02.0000000Z |

**솔루션**:

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

**설명은**: 사용 **지연** toopeek hello에 하나의 이벤트 다시 스트림 입력과 hello 가져올 **확인** 값입니다. Toohello 비교 **확인** 다른 경우 hello 현재 이벤트 및 출력 hello 이벤트 값입니다.

## <a name="query-example-find-hello-first-event-in-a-window"></a>쿼리 예제: 찾기 hello 창에서 첫 번째 이벤트
**설명**: 매 10 분 간격의 찾기 hello 첫 번째 자동차 합니다.

**입력**:

| LicensePlate | 계정을 | Time |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:오전 12:05.0000000Z |
| YZK 5704 |Ford |2015-07-27T00:오전 2:17.0000000Z |
| RMV 8282 |Honda |2015-07-27T00:오전 5:01.0000000Z |
| YHN 6970 |Toyota |2015-07-27T00:오전 6:00.0000000Z |
| VFE 1616 |Toyota |2015-07-27T00:오전 9:31.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:오후 12:02.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:오후 1:45.0000000Z |

**출력**:

| LicensePlate | 계정을 | Time |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:오전 12:05.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:오후 12:02.0000000Z |

**솔루션**:

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

이제 10 분 간격의 hello 문제 및 찾기 hello 첫 번째 자동차 보기는 특정 만들어 보겠습니다.

| LicensePlate | 계정을 | Time |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:오전 12:05.0000000Z |
| YZK 5704 |Ford |2015-07-27T00:오전 2:17.0000000Z |
| YHN 6970 |Toyota |2015-07-27T00:오전 6:00.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:오후 12:02.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:오후 1:45.0000000Z |

**솔루션**:

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-hello-last-event-in-a-window"></a>쿼리 예제: 찾기 hello 창의 마지막 이벤트
**설명**: 매 10 분 간격의 찾기 hello 마지막 자동차 합니다.

**입력**:

| LicensePlate | 계정을 | Time |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:오전 12:05.0000000Z |
| YZK 5704 |Ford |2015-07-27T00:오전 2:17.0000000Z |
| RMV 8282 |Honda |2015-07-27T00:오전 5:01.0000000Z |
| YHN 6970 |Toyota |2015-07-27T00:오전 6:00.0000000Z |
| VFE 1616 |Toyota |2015-07-27T00:오전 9:31.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:오후 12:02.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:오후 1:45.0000000Z |

**출력**:

| LicensePlate | 계정을 | Time |
| --- | --- | --- |
| VFE 1616 |Toyota |2015-07-27T00:오전 9:31.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:오후 1:45.0000000Z |

**솔루션**:

    WITH LastInWindow AS
    (
        SELECT 
            MAX(Time) AS LastEventTime
        FROM 
            Input TIMESTAMP BY Time
        GROUP BY 
            TumblingWindow(minute, 10)
    )
    SELECT 
        Input.LicensePlate,
        Input.Make,
        Input.Time
    FROM
        Input TIMESTAMP BY Time 
        INNER JOIN LastInWindow
        ON DATEDIFF(minute, Input, LastInWindow) BETWEEN 0 AND 10
        AND Input.Time = LastInWindow.LastEventTime

**설명은**: hello 쿼리에서 두 단계가 있습니다. hello 첫 번째 하나 찾습니다 hello 최신 타임 스탬프에서 windows 10 분입니다. 두 번째 단계 조인 hello hello hello 각 창에서 마지막 타임 스탬프와 일치 하는 hello 원래 스트림 toofind hello 이벤트와 함께 hello 첫 번째 쿼리의 결과입니다. 

## <a name="query-example-detect-hello-absence-of-events"></a>쿼리 예: hello 이벤트가 없는 경우를 검색 합니다.
**설명**: 스트림에 특정 조건에 일치하지 않는 값이 있는지 확인합니다.
예를 들어 hello 동일 확인의 연속 된 2 자동차 입력 한 hello 유료도로 hello 내에서 마지막 90 초?

**입력**:

| 계정을 | LicensePlate | Time |
| --- | --- | --- |
| Honda |ABC-123 |2015-01-01T00:오전 12:01.0000000Z |
| Honda |AAA-999 |2015-01-01T00:오전 12:02.0000000Z |
| Toyota |DEF-987 |2015-01-01T00:오전 12:03.0000000Z |
| Honda |GHI-345 |2015-01-01T00:오전 12:04.0000000Z |

**출력**:

| 계정을 | Time | CurrentCarLicensePlate | FirstCarLicensePlate | FirstCarTime |
| --- | --- | --- | --- | --- |
| Honda |2015-01-01T00:오전 12:02.0000000Z |AAA-999 |ABC-123 |2015-01-01T00:오전 12:01.0000000Z |

**솔루션**:

    SELECT
        Make,
        Time,
        LicensePlate AS CurrentCarLicensePlate,
        LAG(LicensePlate, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarLicensePlate,
        LAG(Time, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarTime
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(second, 90)) = Make

**설명은**: 사용 **지연** toopeek hello에 하나의 이벤트 다시 스트림 입력과 hello 가져올 **확인** 값입니다. Toohello 비교 **확인** hello 현재 이벤트과 같은 hello는 이러한 경우 출력 hello 이벤트 값입니다. 사용할 수도 있습니다 **지연** hello 이전 자동차에 대 한 tooget 데이터입니다.

## <a name="query-example-detect-hello-duration-between-events"></a>쿼리 예: 이벤트 사이의 hello 기간 검색
**설명**: 지정된 된 이벤트의 hello 기간을 찾습니다. 예를 들어 웹 클릭 동향 들어 hello 시간 기능을 결정 합니다.

**입력**:  

| 사용자 | 기능 | 이벤트 | Time |
| --- | --- | --- | --- |
| user@location.com |RightMenu |시작 |2015-01-01T00:오전 12:01.0000000Z |
| user@location.com |RightMenu |끝 |2015-01-01T00:오전 12:08.0000000Z |

**출력**:  

| 사용자 | 기능 | 기간 |
| --- | --- | --- |
| user@location.com |RightMenu |7 |

**솔루션**:

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

**설명은**: 사용 하 여 hello **마지막** 마지막 tooretrieve hello 함수 **시간** hello 이벤트 형식이 값 **시작**합니다. hello **마지막** 함수는 **PARTITION BY [사용자]** 고유 사용자 당 결과 hello tooindicate 계산 됩니다. hello 쿼리에 1 시간 사이의 시간 차이 hello에 대 한 최대 임계값 **시작** 및 **중지** 이벤트, 필요에 따라 구성할 수 있지만 **(제한 DURATION(hour, 1)**합니다.

## <a name="query-example-detect-hello-duration-of-a-condition"></a>쿼리 예: 검색 조건의 hello 기간
**설명**: 조건이 발생한 기간을 알아봅니다.
예를 들어 버그가 생겨서 모든 자동차의 중량이 정확하지 않은 경우(20,000파운드 이상) 를 가정합니다. Hello 버그의 toocompute hello 기간을 주시기 바랍니다.

**입력**:

| 계정을 | Time | 무게 |
| --- | --- | --- |
| Honda |2015-01-01T00:오전 12:01.0000000Z |2000 |
| Toyota |2015-01-01T00:오전 12:02.0000000Z |25000 |
| Honda |2015-01-01T00:오전 12:03.0000000Z |26000 |
| Toyota |2015-01-01T00:오전 12:04.0000000Z |25000 |
| Honda |2015-01-01T00:오전 12:05.0000000Z |26000 |
| Toyota |2015-01-01T00:오전 12:06.0000000Z |25000 |
| Honda |2015-01-01T00:오전 12:07.0000000Z |26000 |
| Toyota |2015-01-01T00:오전 12:08.0000000Z |2000 |

**출력**:

| StartFault | EndFault |
| --- | --- |
| 2015-01-01T00:오전 12:02.000Z |2015-01-01T00:오전 12:07.000Z |

**솔루션**:

````
    WITH SelectPreviousEvent AS
    (
    SELECT
    *,
        LAG([time]) OVER (LIMIT DURATION(hour, 24)) as previousTime,
        LAG([weight]) OVER (LIMIT DURATION(hour, 24)) as previousWeight
    FROM input TIMESTAMP BY [time]
    )

    SELECT 
        LAG(time) OVER (LIMIT DURATION(hour, 24) WHEN previousWeight < 20000 ) [StartFault],
        previousTime [EndFault]
    FROM SelectPreviousEvent
    WHERE
        [weight] < 20000
        AND previousWeight > 20000
````

**설명은**: 사용 **지연** 을 24 시간 동안 tooview hello 입력된 스트림을 열고 where 인스턴스 **StartFault** 및 **StopFault** hello에 의해 확장 되는 < 20000 가중치를 부여 합니다.

## <a name="query-example-fill-missing-values"></a>쿼리 예제: 누락된 값 입력
**설명**: hello 스트림의 값이 누락 된 이벤트의 경우 정기적으로 포함 된 이벤트 스트림을 생성 합니다.
예를 들어 hello 가장 최근에 표시 데이터 요소를 보고 하는 이벤트 5 초 마다를 생성 합니다.

**입력**:

| t | value |
| --- | --- |
| "2014-01-01T06:01:00" |1 |
| "2014-01-01T06:오전 1:05" |2 |
| "2014-01-01T06:오전 1:10" |3 |
| "2014-01-01T06:오전 1:15" |4 |
| "2014-01-01T06:오전 1:30" |5 |
| "2014-01-01T06:오전 1:35" |6 |

**출력(처음 10개 행)**:

| windowend | lastevent.t | lastevent.value |
| --- | --- | --- |
| 2014-01-01T14:오전 1:00.000Z |2014-01-01T14:오전 1:00.000Z |1 |
| 2014-01-01T14:오전 1:05.000Z |2014-01-01T14:오전 1:05.000Z |2 |
| 2014-01-01T14:오전 1:10.000Z |2014-01-01T14:오전 1:10.000Z |3 |
| 2014-01-01T14:오전 1:15.000Z |2014-01-01T14:오전 1:15.000Z |4 |
| 2014-01-01T14:오전 1:20.000Z |2014-01-01T14:오전 1:15.000Z |4 |
| 2014-01-01T14:오전 1:25.000Z |2014-01-01T14:오전 1:15.000Z |4 |
| 2014-01-01T14:오전 1:30.000Z |2014-01-01T14:오전 1:30.000Z |5 |
| 2014-01-01T14:오전 1:35.000Z |2014-01-01T14:오전 1:35.000Z |6 |
| 2014-01-01T14:오전 1:40.000Z |2014-01-01T14:오전 1:35.000Z |6 |
| 2014-01-01T14:오전 1:45.000Z |2014-01-01T14:오전 1:35.000Z |6 |

**솔루션**:

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


**설명은**:이 쿼리가 5 초 마다 이벤트를 생성 하 고 출력 hello 이전에 수신 된 마지막 이벤트입니다. hello [도약 창](https://msdn.microsoft.com/library/dn835041.aspx "Azure Stream Analytics 도약 창-") 기간 백 hello 쿼리 toofind hello 최신 이벤트 (이 예제의 300 초)을 검색 하는 정도 결정 합니다.

## <a name="get-help"></a>도움말 보기
추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.

## <a name="next-steps"></a>다음 단계
* [스트림 분석 소개 tooAzure](stream-analytics-introduction.md)
* [Azure Stream Analytics 사용 시작](stream-analytics-real-time-fraud-detection.md)
* [Azure  Stream Analytics 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure  Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)

