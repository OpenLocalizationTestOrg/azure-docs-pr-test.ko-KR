---
title: "aaaAzure 이벤트 표 형태 배달 및 다시 시도"
description: "Azure Event Grid에서 이벤트를 배달하는 방법 및 배달되지 않은 메시지를 처리하는 방법을 설명합니다."
services: event-grid
author: djrosanova
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/11/2017
ms.author: darosa
ms.openlocfilehash: 874b3bf8892fbf803ef40f29d0ec10eb50150916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-message-delivery-and-retry"></a>Event Grid 메시지 배달 및 다시 시도 

이 문서에서는 Azure Event Grid에서 배달이 승인되지 않는 경우 이벤트를 처리하는 방법을 설명합니다.

Event Grid는 지속성이 있는 배달을 제공합니다. 각 메시지를 각 구독에 대해 최소 한 번 배달합니다. 이벤트 등록 toohello webhook 각 구독을 즉시 전송 됩니다. webhook 이벤트 수신을 확인 하지 않습니다 hello 첫 번째 배달의 60 초 이내 시도, 이벤트 표 형태 hello 이벤트의 배달을 다시 시도 합니다.

## <a name="message-delivery-status"></a>메시지 배달 상태

이벤트 표 형태는 HTTP 응답 코드 tooacknowledge 수신 이벤트를 사용합니다. 

### <a name="success-codes"></a>성공 코드

hello HTTP 응답 코드를 다음 표시 하는 이벤트에 성공적으로 배달 되었습니다 tooyour webhook 합니다. Event Grid는 배달이 완료되었다고 간주합니다.

- 200 정상
- 202 수락됨

### <a name="failure-codes"></a>실패 코드

HTTP 응답 코드를 다음 hello 이벤트 배달 시도가 실패 했음을 나타냅니다. 이벤트 표 형태 toosend hello 이벤트를 다시 시도합니다. 

- 400 잘못된 요청
- 401 권한 없음
- 404 찾을 수 없음
- 408 요청 시간 초과
- 414 URI가 너무 김
- 500 내부 서버 오류
- 503 서비스를 사용할 수 없음
- 504 게이트웨이 시간 초과

다른 모든 응답 코드 또는 응답의 부족은 오류가 발생했음을 나타냅니다. Event Grid는 배달을 다시 시도합니다. 

## <a name="retry-intervals"></a>재시도 간격

Event Grid는 이벤트 배달에 대해 지수 백오프 재시도 정책을 사용합니다. 프로그램 webhook 응답 하지 않으면 오류 코드가 반환, 이벤트 표 형태 일정에 따라 hello에서 배달을 다시 시도:

1. 10초
2. 30초
3. 1분
4. 5분
5. 10분
6. 30분
7. 1시간

작은 임의 tooall 다시 시도 간격을 추가 하는 이벤트 표 형태입니다.

## <a name="retry-duration"></a>다시 시도 기간

Azure 이벤트 표 형태 hello 미리 보기 기간 동안 2 시간 이내에 배달 되지 않는 모든 이벤트에 만료 됩니다. 일반 공급 전에이 시간 증가 too24 시간 수 있습니다. 

## <a name="next-steps"></a>다음 단계

* 눈금에는 소개 tooEvent 참조 [이벤트 표 형태에 대 한](overview.md)합니다.
* tooquickly 이벤트 표 형태를 사용 하 여 시작 하려면 다음을 참조 하십시오 [Azure 이벤트 표 형태를 사용자 지정 이벤트 만들기 및 경로](custom-event-quickstart.md)합니다.
