---
title: "aaaHow tooBuild 복잡 한 일정 및 Azure 스케줄러와 고급 되풀이"
description: "TooBuild 복잡 한 일정을 조정 하는 방법 및 Azure 스케줄러와 고급 되풀이"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 5c124986-9f29-4cbc-ad5a-c667b37fbe5a
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 02172791978b12be0ccb3078125d057b2efe8523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobuild-complex-schedules-and-advanced-recurrence-with-azure-scheduler"></a>TooBuild 복잡 한 일정을 조정 하는 방법 및 Azure 스케줄러와 고급 되풀이
## <a name="overview"></a>개요
Azure 스케줄러 hello 핵심 작업은 hello *일정*합니다. hello 일정 hello 스케줄러 hello 작업 실행 시기와 방법을 결정 합니다.

Azure 스케줄러 toospecify 다른 일회성 및 되풀이 일정을 작업에 대 한 있습니다. *일회성* 일정은 지정된 시간에 한 번만 실행됩니다. 실질적으로 이는 한 번만 실행되는 *되풀이* 일정입니다. 되풀이 일정은 미리 지정된 빈도로 실행됩니다.

Azure 스케줄러의 이러한 유연성을 활용하여 다양한 비즈니스 시나리오를 지원할 수 있습니다.

* 정기적인 데이터 정리 - 예를 들어 매일 3개월 이상 지난 트윗을 삭제
* 보관 – 모든 월, 푸시 송장 기록 toobackup 서비스 예:
* 외부 데이터 요청 - 예를 들어 NOAA에서 15분마다 새 ski 날씨 보고서 가져오기
* 클라우드 컴퓨팅 toocompress 이미지 업로드 해당 날짜를 사용 하 여를 처리-예: 주중 매일, 사용량이 많은 시간을 이미지합니다

이 문서에서는 Azure 스케줄러로 만들 수 있는 작업의 예를 살펴보겠습니다. 각 일정을 설명 하는 hello JSON 데이터를 제공 합니다. Hello를 사용 하는 경우 [스케줄러 REST API](https://msdn.microsoft.com/library/mt629143.aspx)에 대 한 동일한이 JSON을 사용할 수 있습니다 [Azure 스케줄러 작업을 만드는](https://msdn.microsoft.com/library/mt629145.aspx)합니다.

## <a name="supported-scenarios"></a>지원되는 시나리오
이 항목의 많은 예제 hello 다양 한 시나리오를 지 원하는 Azure 스케줄러를 설명 하는 번호입니다. 광범위 하 게,이 예는 방법을 비롯 한 많은 동작 패턴에 대 한 일정 toocreate hello는 스토리 아래 보여 줍니다.

* 특정 날짜 및 시간에 한 번 실행
* 실행하고 명시된 횟수만큼 되풀이
* 즉시 실행하고 되풀이
* 실행하고 *n*분, 시간, 일, 주 또는 월마다 되풀이, 특정 시간에 시작
* 실행하고 주 또는 월마다 되풀이하지만 특정 일, 요일 또는 날짜에만 실행
* 실행하고 기간 내 여러 번 되풀이. 예를 들어 매월 마지막 금요일과 월요일, 매일 오전 5시 15분과 오후 5시 15분

## <a name="dates-and-datetimes"></a>날짜 및 날짜-시간
Azure 스케줄러 작업의 날짜에 따라 hello [ISO 8601 사양](http://en.wikipedia.org/wiki/ISO_8601) hello 날짜만 포함 됩니다.

Azure 스케줄러는 작업에 대 한 참조의 날짜 및 시간에 따라 hello [ISO 8601 사양](http://en.wikipedia.org/wiki/ISO_8601) 날짜와 시간 부분을 포함 합니다. UTC 오프셋을 지정 하지 않는 날짜 및 시간 toobe UTC 가정 합니다.  

## <a name="how-to-use-json-and-rest-api-for-creating-schedules"></a>방법: JSON 및 REST API를 사용하여 일정 만들기
사용 하 여 간단한 예약 toocreate hello [Azure 스케줄러 REST API](https://msdn.microsoft.com/library/mt629143), 첫 번째 [리소스 공급자에 구독을 등록](https://msdn.microsoft.com/library/azure/dn790548.aspx) (스케줄러에 대 한 hello 공급자 이름은  *Microsoft.Scheduler*), 다음 [작업 컬렉션을 만들](https://msdn.microsoft.com/library/mt629159.aspx), 마지막으로 [작업을 만드는](https://msdn.microsoft.com/library/mt629145.aspx)합니다. 작업을 만들 때에 일정 및 되풀이 아래 발췌 되었습니다 하나 hello와 같은 JSON을 사용 하 여 지정할 수 있습니다.

    {
        "startTime": "2012-08-04T00:00Z", // optional
         …
        "recurrence":                     // optional
        {
            "frequency": "week",     // can be "year" "month" "day" "week" "hour" "minute"
            "interval": 1,                // optional, how often toofire (default too1)
            "schedule":                   // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]                      
            },
            "count": 10,                  // optional (default toorecur infinitely)
            "endTime": "2012-11-04",      // optional (default toorecur infinitely)
        },
        …
    }

## <a name="overview-job-schema-basics"></a>개요: 작업 스키마 기본 사항
다음 표에서 hello hello 주요 요소에 대 한 관련된 toorecurrence 및 예약 된 작업에서 상위 수준 개요를 제공 합니다.

| **JSON 이름** | **설명** |
|:--- |:--- |
| ***startTime*** |*startTime*은 날짜-시간입니다. 단순 일정에 대 한 *startTime* hello 맨 처음 발견 되는 및 복잡 한 일정에 대 한 hello 작업이 즉시 시작 됩니다 *startTime*합니다. |
| ***recurrence*** |hello *되풀이* 개체 hello 작업과 hello 되풀이 hello 작업으로 실행 됩니다에 대 한 되풀이 규칙을 지정 합니다. hello 되풀이 개체가 지원 hello 요소 *빈도, 간격, endTime, 개수,* 및 *일정*합니다. 경우 *되풀이* 정의 된 *주파수* 필요 합니다; 다른 요소의 hello *되풀이* 는 선택 사항입니다. |
| ***frequency*** |hello *주파수* hello 빈도 단위는 hello 작업 되풀이 나타내는 문자열입니다. 지원되는 값은 *"minute", "hour", "day", "week"* 또는 *"month"*입니다. |
| ***interval*** |hello *간격* 는 양의 정수 이며 hello에 대 한 hello 간격 나타냅니다 *주파수* hello 작업은 실행 빈도 결정 하는 합니다. 예를 들어 경우 *간격* 3 및 *주파수* "주" hello 작업의 모든 3 주까지 반복 합니다. Azure Scheduler가 지원하는 최대 *interval*은 월 빈도로 18개월, 주 빈도로 78주, 일 빈도로 548일입니다. Hello 지원 범위는 1 시간 및 분 빈도 대 한 < = *간격* < = 1000입니다. |
| ***endTime*** |hello *endTime* 는 hello 지난 작업 하지에서 실행할 hello 날짜 시간을 지정 하는 문자열입니다. 유효한 toohave 않습니다는 *endTime* 지난 hello에 있습니다. 없는 경우 *endTime* 또는 count가 지정, hello 작업이 무한 실행 합니다. 둘 다 *endTime* 및 *count* hello에 대 한 포함할 수 없습니다 같은 작업입니다. |
| ***count*** |<p>hello *count* 양의 정수 (0 보다 큼)이이 작업을 완료 하기 전에 실행할 횟수 hello 수를 지정 하는 합니다.</p><p>hello *count* 나타냅니다 hello hello 작업이 완료 된 것으로 결정 하기 전에 실행 횟수입니다. 매일로 실행 되는 작업에 대 한 예를 들어 *count* 5 월요일의 시작 날짜, 금요일에 실행 된 후 hello 작업이 완료 되 고 있습니다. Hello 시작 날짜가 지난 hello 면 hello 첫 번째 실행 hello 만든 시간에서 계산 됩니다.</p><p>되지 않은 경우 *endTime* 또는 *count* hello 작업이 무한 실행 지정 됩니다. 둘 다 *endTime* 및 *count* hello에 대 한 포함할 수 없습니다 같은 작업입니다.</p> |
| ***schedule*** |작업에 빈도가 지정되면 되풀이 일정을 기반으로 되풀이가 변경됩니다. *schedule*에는 분, 시간, 요일, 날짜, 주차를 기반으로 하는 조건이 포함됩니다. |

## <a name="overview-job-schema-defaults-limits-and-examples"></a>개요: 작업 스키마 기본값, 제한 및 예
이 개요를 먼저 본 후, 각 요소에 대해 자세히 알아보겠습니다.

| **JSON 이름** | **값 형식** | **필수 여부** | **기본값** | **유효한 값** | **예제** |
|:--- |:--- |:--- |:--- |:--- |:--- |
| ***startTime*** |String |아니요 |없음 |ISO-8601 날짜-시간 |<code>"startTime" : "2013-01-09T09:30:00-08:00"</code> |
| ***recurrence*** |Object |아니요 |없음 |되풀이 개체 |<code>"recurrence" : { "frequency" : "monthly", "interval" : 1 }</code> |
| ***frequency*** |문자열 |예 |없음 |"minute", "hour", "day", "week", "month" |<code>"frequency" : "hour"</code> |
| ***interval*** |Number |아니요 |1 |1 too1000 합니다. |<code>"interval":10</code> |
| ***endTime*** |문자열 |아니요 |없음 |Hello 향후에 한 번을 나타내는 날짜 및 시간 값입니다. |<code>"endTime" : "2013-02-09T09:30:00-08:00"</code> |
| ***count*** |Number |아니요 |없음 |1 이상 |<code>"count": 5</code> |
| ***schedule*** |Object |아니요 |없음 |일정 개체 |<code>"schedule" : { "minute" : [30], "hour" : [8,17] }</code> |

## <a name="deep-dive-starttime"></a>자세히 알아보기: *startTime*
hello 다음 캡처를 어떻게 표에서 *startTime* 는 작업이 실행 되는 방식을 제어 합니다.

| **startTime 값** | **되풀이 없음** | **되풀이. 일정 없음** | **일정대로 되풀이** |
|:--- |:--- |:--- |:--- |
| **시작 시간 없음** |즉시 한 번 실행 |즉시 한 번 실행합니다. 마지막 실행 시간에서 계산된 값을 기반으로 후속 실행 수행 |<p>즉시 한 번 실행</p><p>되풀이 일정에 따라 후속 실행을 수행</p> |
| **시작 시간이 이전임** |즉시 한 번 실행 |<p>시작 시간 이후 첫 실행 시간을 계산하고 해당 시간에 실행</p><p>마지막 실행 시간에서 계산된 값을 기반으로 후속 실행 수행</p><p>자세한 설명은 이 테이블 다음에 있는 예제를 참조하세요.</p> |<p>시작 작업 *더 보다 빨리* hello 시작 시간을 지정 합니다. hello 첫 번째 hello 시작 시간에서 계산 된 hello 일정 기반</p><p>되풀이 일정에 따라 후속 실행을 수행</p> |
| **시작 시간이 이후이거나 현재임** |지정된 시작 시간에 한 번 실행 |<p>지정된 시작 시간에 한 번 실행</p><p>마지막 실행 시간에서 계산된 값을 기반으로 후속 실행 수행</p> |<p>시작 작업 *더 보다 빨리* hello 시작 시간을 지정 합니다. hello 첫 번째 hello 시작 시간에서 계산 된 hello 일정 기반</p><p>되풀이 일정에 따라 후속 실행을 수행</p> |

예를 들어 어떤 상황이 발생 하는지 살펴보겠습니다 여기서 *startTime* 전의 hello에으로 *되풀이* 없는 *일정*합니다.  해당 hello 현재 시간을 2015-04-08 가정 13시 *startTime* 2015-04-07은 14시 및 *되풀이* 은 2 일 마다 (정의 된 *주파수*: 요일과 *간격*: 2.) 해당 hello 참고 *startTime* hello 전의 이며 hello 현재 시간 전에 발생 합니다.

이러한 상황에서는 hello *첫 번째 실행* 14:00 2015-04-09 됩니다\. hello 스케줄러 엔진이 실행 발생에서 hello 시작 시간을 계산합니다.  지난 hello에서 모든 인스턴스는 무시 됩니다. hello 엔진 이후 hello에서 발생 하는 hello 다음 인스턴스를 사용 합니다.  따라서이 경우 *startTime* 관계는 2015-04-07 오후 2 시에 다음 인스턴스 hello 2015-04-09 오후 2 시에 해당 시간 로부터 2 일입니다.

첫 번째 실행 hello hello 될 것 같은 경우에도 hello startTime 2015-04-05 14시 또는 2015-04-01 14:00\ 합니다. Hello를 사용 하 여 후속 실행은 계산 하는 hello 첫 번째 실행 후 예약 – 길 바랍니다. 2015-04-11 다음 2015-04-13 오후 2시 오후 2 시에 다음 2015-04-15 오후 2 시에 되므로 등입니다.

마지막으로 때 (job)에 일정 시간 및/또는 분 각각 hello 일정은 기본 toohello 시간 및/또는 분 hello 첫 번째 실행에서 설정 되지 않은 경우.

## <a name="deep-dive-schedule"></a>자세히 알아보기: *schedule*
한편으로 *일정* 수 *제한* hello 작업 실행 수입니다.  예를 들어와 작업이 있는 경우 "month" 주파수가는 *일정* 유일한 31 일에서 실행 되는 31 있는 해당 월만에 hello 작업이 실행,<sup>st</sup> 일 합니다.

반면에 hello는 *일정* 수도 있습니다 *확장* hello 작업 실행 수입니다. 예를 들어와 작업이 있는 경우 "month" 주파수가는 *일정* 가 1과 2 월 일에서 실행 hello 작업에서 실행 되도록 hello 1<sup>st</sup> 2<sup>nd</sup> 대신 한 번만 hello 월의 일을 한 달입니다.

여러 일정 요소가 지정 된 경우 hello 평가 순서가 hello 가장 큰 toosmallest-주 번호, 월 일, 주 일, 시 및 분에서.

hello 다음 표에서 설명 *일정* 요소 자세히 설명에서 합니다.

| **JSON 이름** | **설명** | **유효한 값** |
|:--- |:--- |:--- |
| **minutes** |작업을 실행 하는 hello에 hello 시간 (분) |<ul><li>정수 또는</li><li>정수 배열</li></ul> |
| **hours** |작업을 실행 하는 hello에 hello 하루 중 시간 |<ul><li>정수 또는</li><li>정수 배열</li></ul> |
| **weekDays** |일 hello 주 hello 작업의 실행 됩니다. 빈도가 주인 경우에만 지정할 수 있습니다. |<ul><li>"Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday" 또는 "Sunday"</li><li>값 (최대 배열 크기 7) 위에 hello 엔터티의 배열</li></ul>대/소문자 구분 *안 함* |
| **monthlyOccurrences** |Hello 월 hello 작업의 날짜 실행할지를 결정 합니다. 빈도가 월인 경우에만 지정할 수 있습니다. |<ul><li>monthlyOccurrence 개체의 배열:</li></ul> <pre>{ "day": *day*,<br />  "occurrence": *occurrence*<br />}</pre><p> *day* hello 요일을 hello 주 hello 작업 실행, 예를 들어 {일요일}은 매주 일요일 hello 달의 합니다. 필수입니다.</p><p>*발생* hello 달간 hello 하루 중 예: {일요일,-1 (를) hello 월의 마지막 일요일 hello 됩니다. 선택 사항입니다.</p> |
| **monthDays** |일 hello 월 hello 작업의 실행 됩니다. 빈도가 월인 경우에만 지정할 수 있습니다. |<ul><li>-31 ~ -1 사이의 모든 값입니다.</li><li>1 ~ 31 사이의 모든 값입니다.</li><li>위 값의 배열</li></ul> |

## <a name="examples-recurrence-schedules"></a>예: 되풀이 일정
hello 다음은 되풀이 일정 – hello 일정 개체 및 해당 하위 요소에 중점을 두고 다양 한 예제입니다.

hello 아래 모든 일정 가정 해당 hello *간격* too1 설정\. 또한 하나 해야 오른쪽 빈도 따라 toowhat hello에에서 가정 hello *일정* -예: 하나 및 사용할 수 없습니다 "day" 주파수 hello 일정에 "되풀이할" 수정 했습니다. 이러한 제한 사항은 위에 설명되어 있습니다.

| **예제** | **설명** |
|:--- |:--- |
| <code>{"hours":[5]}</code> |매일 오전 5시에 실행합니다. Azure 스케줄러 "시간" 각 값이 "minutes", 개별적으로, 모든 hello 시간은 hello 작업 toobe 목록을 실행 toocreate의에서 각 값을 찾습니다. |
| <code>{"minutes":[15], "hours":[5]}</code> |매일 오전 5시 15분에 실행 |
| <code>{"minutes":[15], "hours":[5,17]}</code> |매일 오전 5시 15분과 오후 5시 15분에 실행 |
| <code>{"minutes":[15,45], "hours":[5,17]}</code> |매일 오전 5시 15분, 5시 45분, 오후 5시 15분, 5시 45분에 실행 |
| <code>{"minutes":[0,15,30,45]}</code> |15분마다 실행 |
| <code>{hours":[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23]}</code> |1시간마다 실행 이 작업은 매시간 실행됩니다. hello 분 hello에 의해 제어 됩니다 *startTime*, 지정 된 경우 또는 hello 생성 시간별에 지정 된 경우. 예를 들어 hello 시작 시간이 나 만든 시간 (적용 되) 오후 12시 25분 이면 hello 작업 수에 실행 됩니다 00:25, 25:01, 02:25,..., 23시 25분입니다. hello 일정은 해당 toohaving 작업이 *주파수* "시간"의 *간격* 1 및 0의 *일정*합니다. hello 차이점은 서로 다른이 일정을 사용할 수 없습니다 *주파수* 및 *간격* toocreate 다른 너무 작업 합니다. 예를 들어 경우 hello, *주파수* "month", hello 일정은 실행 된 매일 대신 한 달에 한 번만 경우 *주파수* "일" 되었습니다 |
| <code>{minutes:[0]}</code> |Hello 시간에서 1 시간 마다 실행 합니다. 이 작업은 또한 1 시간 마다 실행 되지만 hello 시간에 (예: 오전 12 시, 오전 1 시, 오전 2 등입니다.) Hello 주파수 "day" 되었다가 hello 주파수 "주" 또는 "month" 인 경우 hello 일정 하루 한 달, 주 또는 하루를 각각 실행 합니다 경우 주파수 "시간"가 해당 tooa 작업, 일정 없음 0 분와 startTime입니다. |
| <code>{"minutes":[15]}</code> |매시간 15분에 실행됩니다. 오전 0시 15분, 1시 15분, 2시 15분 등으로 시작하여 오후 10시 15분, 11시 15분에 완료됩니다. |
| <code>{"hours":[17], "weekDays":["saturday"]}</code> |매주 토요일 오후 5시에 실행 |
| <code>{hours":[17], "weekDays":["monday", "wednesday", "friday"]}</code> |매주 월요일, 수요일, 금요일 오후 5시에 실행 |
| <code>{"minutes":[15,45], "hours":[17], "weekDays":["monday", "wednesday", "friday"]}</code> |매주 월요일, 수요일, 금요일 오후 5시 15분과 5시 45분에 실행 |
| <code>{"hours":[5,17], "weekDays":["monday", "wednesday", "friday"]}</code> |매주 월요일, 수요일, 금요일 오전 5시와 오후 5시에 실행 |
| <code>{"minutes":[15,45], "hours":[5,17], "weekDays":["monday", "wednesday", "friday"]}</code> |매주 월요일, 수요일, 금요일 오전 5시 15분, 5시 45분, 오후 5시 15분, 5시 45분에 실행 |
| <code>{"minutes":[0,15,30,45], "weekDays":["monday", "tuesday", "wednesday", "thursday", "friday"]}</code> |월요일부터 금요일까지 15분마다 실행 |
| <code>{"minutes":[0,15,30,45], "hours": [9, 10, 11, 12, 13, 14, 15, 16] "weekDays":["monday", "tuesday", "wednesday", "thursday", "friday"]}</code> |월요일부터 금요일까지 오전 9시에서 오후 4시 45분 사이에 15분마다 실행 |
| <code>{"weekDays":["sunday"]}</code> |일요일 시작 시간에 실행 |
| <code>{"weekDays":["tuesday", "thursday"]}</code> |화요일과 목요일 시작 시간에 실행 |
| <code>{"minutes":[0], "hours":[6], "monthDays":[28]}</code> |오전 6 시에 실행 hello 28 일의 모든 월 (월의 주파수 가정) |
| <code>{"minutes":[0], "hours":[6], "monthDays":[-1]}</code> |Hello hello 달의 마지막 날에 오전 6 시에 실행 합니다. 원하는 경우 toorun hello에서 작업 한 달의 마지막 날을 28 이나 29, 30, 31 일 대신-1을 사용 합니다. |
| <code>{"minutes":[0], "hours":[6], "monthDays":[1,-1]}</code> |첫 번째 및 마지막 일의 모든 월 hello 오전 6 시에 실행 |
| <code>{monthDays":[1,-1]}</code> |Hello 첫 번째 및의 모든 월의 마지막 날에 실행 시작 시간 |
| <code>{monthDays":[1,14]}</code> |Hello 첫 번째 및의 모든 월의 열 네 번째 날에 실행 시작 시간 |
| <code>{monthDays":[2]}</code> |Hello hello 시작 시간에서 월의 두 번째 날에 실행 |
| <code>{"minutes":[0], "hours":[5], "monthlyOccurrences":[{"day":"friday", "occurrence":1}]}</code> |매월 첫 번째 금요일 오전 5시에 실행 |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":1}]}</code> |매월 첫 번째 금요일 시작 시간에 실행 |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":-3}]}</code> |매월 끝에서 세 번째 금요일 시작 시간에 실행 |
| <code>{"minutes":[15], "hours":[5], "monthlyOccurrences":[{"day":"friday", "occurrence":1},{"day":"friday", "occurrence":-1}]}</code> |매월 첫 번째와 마지막 금요일 오전 5시 15분에 실행 |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":1},{"day":"friday", "occurrence":-1}]}</code> |매월 첫 번째와 마지막 금요일 시작 시간에 실행 |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":5}]}</code> |매월 5번째 금요일 시작 시간에 실행됩니다. 없는 경우 없는 다섯 번째 금요일 한 달이 실행 되지이 않습니다, 이기 때문에 예약 된 toorun만 다섯 번째 금요일. 대신 사용 하 여-1 5 번째 hello hello 마지막 발생 hello 달의 금요일에 toorun hello 작업 하려는 경우를 고려할 수 있습니다. |
| <code>{"minutes":[0,15,30,45], "monthlyOccurrences":[{"day":"friday", "occurrence":-1}]}</code> |Hello 달의 마지막 금요일 15 분 마다 실행 |
| <code>{"minutes":[15,45], "hours":[5,17], "monthlyOccurrences":[{"day":"wednesday", "occurrence":3}]}</code> |오전 5 시 15 오전 5시 45분 실행 오후 5시 15분 오후 5시 45분 모든 월의 3 번째 수요일 hello |

## <a name="see-also"></a>참고 항목
 [스케줄러란?](scheduler-intro.md)

 [Azure 스케줄러 개념, 용어 및 엔터티 계층 구조](scheduler-concepts-terms.md)

 [Hello Azure 포털에서에서 스케줄러 사용 시작](scheduler-get-started-portal.md)

 [Azure 스케줄러의 버전 및 요금 청구](scheduler-plans-billing.md)

 [Azure 스케줄러 REST API 참조](https://msdn.microsoft.com/library/mt629143)

 [Azure 스케줄러 PowerShell cmdlet 참조](scheduler-powershell-reference.md)

 [Azure 스케줄러 고가용성 및 안정성](scheduler-high-availability-reliability.md)

 [Azure 스케줄러 제한, 기본값 및 오류 코드](scheduler-limits-defaults-errors.md)

 [Azure 스케줄러 아웃바운드 인증](scheduler-outbound-authentication.md)

