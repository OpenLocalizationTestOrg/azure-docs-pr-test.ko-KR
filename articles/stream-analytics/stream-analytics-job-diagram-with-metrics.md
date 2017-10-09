---
title: "aaa Azure 스트림 분석 작업 다이어그램 hello를 사용 하 여 디버깅 데이터 기반 | Microsoft Docs"
description: "Hello 작업 다이어그램 및 메트릭을 사용 하 여 스트림 분석 작업을 해결 합니다."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/01/2017
ms.author: jeffstok
ms.openlocfilehash: 1af884d485bebb06b034da01a13f7f8240516571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="data-driven-debugging-by-using-hello-job-diagram"></a>데이터 기반 작업 다이어그램 hello를 사용 하 여 디버깅

hello에 hello 작업 다이어그램 **모니터링** 블레이드 hello Azure 포털에서에서 작업 파이프라인을 시각화 하는 데 도움이 수 있습니다. 입력, 출력 및 쿼리 단계를 보여 줍니다. 각 단계에 대 한 hello 작업 다이어그램 tooexamine hello 메트릭을 사용할 수 있는데, 문제를 해결할 때 신속 하 게 toomore hello 문제의 소스에 격리 합니다.

## <a name="using-hello-job-diagram"></a>Hello 작업 다이어그램을 사용 하 여

Hello Azure 포털에에서 아래에서 스트림 분석 작업에 있는 동안 **지원 + 문제 해결**선택, **작업 다이어그램**:

![메트릭이 있는 작업 다이어그램 - 위치](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

쿼리 편집 창에서에서 각 쿼리 단계 toosee hello 해당 섹션을 선택 합니다. Hello 단계에 대 한 메트릭 차트는 hello 페이지의 아래쪽 창에 표시 됩니다.

![메트릭이 있는 작업 다이어그램 - 기본 작업](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

hello Azure 이벤트 허브 입력의 toosee hello 파티션을 선택 **중...** 상황에 맞는 메뉴가 나타납니다. 또한 hello 입력된 병합기를 볼 수 있습니다.

![메트릭이 있는 작업 다이어그램 - 파티션 확장](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

만 단일 파티션의 경우 파티션 노드 선택 hello toosee hello의 메트릭 차트입니다. hello 메트릭 hello hello 페이지 맨 아래에 표시 됩니다.

![메트릭이 있는 작업 다이어그램 - 더 많은 메트릭](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

hello 메트릭 차트를 toosee 선택 hello 합병 노드 병합에 대 한 합니다. 다음 차트 hello 이벤트가 제거 되거나 조정 보여 줍니다.

![메트릭이 있는 작업 다이어그램 - 그리드](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

toosee hello hello 메트릭 값 및 시간을 지점 toohello 차트의 세부 정보입니다.

![메트릭이 있는 작업 다이어그램 - 커서 올리기](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a>메트릭을 사용하여 문제 해결

hello **QueryLastProcessedTime** 메트릭을 특정 단계에서 데이터를 수신 하는 때를 나타냅니다. Hello 토폴로지를 살펴보면에서 작업할 수 있습니다 뒤로 hello 출력 프로세서 toosee 단계 데이터를 받고 있지 않습니다. 단계 데이터를 수신 하지 않고 바로 앞 toohello 쿼리 단계를 이동 합니다. Hello 위의 쿼리 단계에는 시간 창 고에 대 한 충분 한 시간이 경과 하는 경우 toooutput 데이터입니다. (참고 당시 창이 있는 맞춰진된 toohello 시간입니다.)
 
이면 hello 이전 쿼리 단계에서 입력된 프로세서 사용 하 여 hello 입력된 된 메트릭 toohelp 응답 hello 다음 질문의 대상입니다. 이는 입력 소스에서 데이터를 가져오는 작업인지 판단하는 데 유용합니다. Hello 쿼리를 분할 하는 경우 각 파티션에 검사 합니다.
 
### <a name="how-much-data-is-being-read"></a>얼마나 많은 데이터를 읽습니까?

*   **InputEventsSourcesTotal** hello 읽을 데이터 단위 수입니다. 예를 들어 hello blob 수입니다.
*   **InputEventsTotal** hello 읽은 이벤트 수입니다. 이 메트릭은 각 파티션에 사용할 수 있습니다.
*   **InputEventsInBytesTotal** hello 읽은 바이트 수입니다.
*   **InputEventsLastArrivalTime**은 수신된 모든 이벤트의 큐에 넣은 시간과 함께 업데이트됩니다.
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a>시간은 앞으로 진행됩니까? 실제 이벤트를 읽는 경우 문장 부호가 발생하지 않을 수 있습니다.

*   **InputEventsLastPunctuationTime** 경우 문장 부호 명령이 실행 되었음을 나타냅니다 tookeep 시간 이동 앞으로 합니다. 문장 부호가 발생하지 않는 경우 데이터 흐름을 차단할 수 있습니다.
 
### <a name="are-there-any-errors-in-hello-input"></a>Hello 입력에 오류 사항이 있습니까?

*   **InputEventsEventDataNullTotal**은 null 데이터가 있는 이벤트의 개수입니다.
*   **InputEventsSerializerErrorsTotal**은 올바르게 deserialize할 수 없는 이벤트의 개수입니다.
*   **InputEventsDegradedTotal**은 deserialization이 아닌 다른 문제가 있는 이벤트의 개수입니다.
 
### <a name="are-events-being-dropped-or-adjusted"></a>이벤트 삭제되거나 조정됩니까?

*   **InputEventsEarlyTotal** hello hello 상위 워터 마크 하기 전에 응용 프로그램 타임 스탬프에 있는 이벤트 수입니다.
*   **InputEventsLateTotal** hello는 hello 상위 워터 마크 이후는 응용 프로그램 타임 스탬프를 제공 하는 이벤트 수입니다.
*   **InputEventsDroppedBeforeApplicationStartTimeTotal** hello 숫자 이벤트 hello 작업 시작 시간을 삭제 합니다.
 
### <a name="are-we-falling-behind-in-reading-data"></a>데이터를 읽을 때 뒤쳐지고 있습니까?

*   **InputEventsSourcesBackloggedTotal** 수가 더 많은 메시지 필요한 toobe 알려줍니다 Azure IoT Hub 및 이벤트 허브 입력에 대 한 합니다.


## <a name="get-help"></a>도움말 보기
추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.

## <a name="next-steps"></a>다음 단계
* [소개 tooStream 분석](stream-analytics-introduction.md)
* [Stream Analytics 시작](stream-analytics-real-time-fraud-detection.md)
* [Stream Analytics 작업 크기 조정](stream-analytics-scale-jobs.md)
* [Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)
