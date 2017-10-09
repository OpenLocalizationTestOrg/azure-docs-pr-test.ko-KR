---
title: "aaaHandling 이벤트 순서와 Azure 스트림 분석에 포함 | Microsoft Docs"
description: "Stream Analytics가 데이터 스트림의 잘못된 순서 또는 지연 이벤트에 어떻게 작동하는지 알아봅니다."
keywords: "순서 비지정, 지연, 이벤트"
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
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 87c028662fbafbf4f72f57f215d017f65bb649f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-event-order-handling"></a>Azure Stream Analytics 이벤트 순서 처리

이벤트의 임시 데이터 스트림의 각 이벤트를 기록 해당 hello 이벤트를 받을 hello 시간을 사용 합니다. 일부 조건 보다는 전송 된 대로 다른 순서로 toooccasionally 수신 하는 이벤트 스트림을 일부 이벤트를 발생할 수 있습니다. 간단한 TCP 재전송 하거나 전송 장치와 이벤트 허브를 수신 하는 hello hello 간에 클럭 오차가이 toooccur 발생할 수 있습니다. "문장 부호"도 추가 된 이벤트 tooreceived 이벤트 스트림을 이벤트 도착 hello 없으면에서 tooadvance hello 시간입니다. 이러한 사항은 “3분 동안 로그인이 발생하지 않을 때 알림”과 같은 시나리오에 필요합니다.

순서가 올바르지 않은 입력 스트림은 다음 중 하나입니다.
* 정렬되었습니다(따라서 **지연됨**).
* 시스템 hello tooa 사용자 지정 정책에 따라 조정 됩니다.


## <a name="lateness-tolerance"></a>지연 허용 오차
Stream Analytics는 이러한 시나리오 형식을 허용합니다. Stream Analytics는 “잘못된 순서” 및 “지연” 이벤트를 처리합니다. 다음 방법으로 hello에서 이러한 이벤트를 처리 합니다.

* 잘못 된 순서로 도착 하지만 hello 내에서 허용 오차를 설정 하는 이벤트는 **타임 스탬프 순서를 조정할**합니다.
* 허용 오차보다 나중에 도착하는 이벤트는 **삭제 또는 조정**합니다.
    * **조정**: 조정 된 tooappear toohave 최신 허용 가능한 시간 hello에 도착 합니다.
    * **삭제**: 삭제합니다.

![Stream Analytics 이벤트 처리](media/stream-analytics-event-handling/stream-analytics-event-handling.png)

## <a name="reduce-hello-number-of-out-of-order-events"></a>이벤트의 순서가 hello 수 줄이기

Stream Analytics는 들어오는 이벤트를 처리할 때 임시 변환을 적용하기 때문에(예: 기간 이동 집계 또는 임시 연결) Stream Analytics는 들어오는 이벤트를 타임스탬프 순서대로 정렬합니다.

하 여 hello "timestamp" 키워드의 경우 **하지** 을 사용 하는 hello Azure 이벤트 허브 이벤트 큐에 넣지 시간이 기본적으로 사용 됩니다. 이벤트 허브 단 조성에 hello 이벤트 허브의 각 파티션에 대해 hello 타임 스탬프를 보장 합니다. 또한 모든 파티션의 이벤트가 타임스탬프 순서대로 병합되는 것을 보장합니다. 이러한 두 이벤트 허브 보증을 통해 잘못된 순서 이벤트를 없앨 수 있습니다.

경우에 따라이 하면 toouse hello 보낸 사람의 타임 스탬프 중요 합니다. "하 여 타임 스탬프입니다."를 사용 하 여 hello 이벤트 페이로드의 타임 스탬프를 선택 하는 경우 이러한 시나리오에서는 잘못 정렬된 이벤트의 원본이 하나 이상 도입될 수도 있습니다.

* 이벤트 생산자에 클록 오차가 있습니다. 이는 생산자가 다른 컴퓨터에 있어 다른 클록을 사용할 때 일반적입니다.
* Hello 이벤트 toohello 대상 이벤트 허브의 hello 소스에서 네트워크 지연이 있습니다.
* 클록 오차는 이벤트 허브 파티션 간에 존재합니다. Stream Analytics는 먼저 모든 이벤트 허브 파티션의 이벤트를 이벤트 큐에 넣기 시간으로 정렬합니다. 그런 다음 hello 데이터 스트림에 잘못 된 이벤트를 검사합니다.

Hello 구성 탭에서 다음 기본값 hello를 확인할 수 있습니다.

![Stream Analytics의 잘못된 순서 처리](media/stream-analytics-event-handling/stream-analytics-out-of-order-handling.png)

Hello 순서가의 허용 시간으로 0 초를 사용 하는 경우 모든 이벤트는 항상 hello에 순서 대로 어설션하는 합니다. 잘못 된 이벤트 hello 3 소스가 들어 그럴 가능성은 true 임을 합니다. 

tooallow 스트림 분석 toocorrect 이벤트 misorder, 0이 아닌 값의 순서가 허용 시간을 지정할 수 있습니다. 스트림 분석 버퍼 이벤트 toothat 창 및 다음 선택한 timestamp 안녕을 사용 하 여 순서를 재정렬 합니다. 다음 hello 임시 변환을 적용합니다. 3 초 창 시작 하며 hello 값 tooreduce hello 번호 시간 조정 된 이벤트를 튜닝할 수 있습니다. 

Hello 버퍼링의 부작용은 hello 출력 **hello 동일 지연 시간**합니다. 순서가 이벤트 hello 값 tooreduce hello 수를 조정 하 고 hello 작업 대기 시간을 낮게 유지 수 있습니다.

## <a name="get-help"></a>도움말 보기
추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.

## <a name="next-steps"></a>다음 단계
* [소개 tooStream 분석](stream-analytics-introduction.md)
* [Stream Analytics 시작](stream-analytics-real-time-fraud-detection.md)
* [Stream Analytics 작업 크기 조정](stream-analytics-scale-jobs.md)
* [Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)