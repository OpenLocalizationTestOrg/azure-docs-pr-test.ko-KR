---
title: "논리 앱에서 aaaAdd hello 되풀이 트리거 | Microsoft Docs"
description: "Hello 되풀이 트리거의 개요 및 방법을 toouse Azure 논리 앱으로 합니다."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 51dd4f22-7dc5-41af-a0a9-e7148378cd50
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e7c625c382a88a1e7cdfff4ddc0caf55727232bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-recurrence-trigger"></a>Hello 되풀이 트리거 시작
Hello 되풀이 트리거를 사용 하 여 hello 클라우드에서 강력한 워크플로 만들 수 있습니다.

예를 들어 다음을 수행할 수 있습니다.

* 매일 워크플로 toorun SQL 저장 프로시저를 예약 합니다.
* 모든 트 윗 hello에 대 한 특정 hashtag 지난 주에 대 한 요약 전자 메일입니다.

hello 되풀이 트리거를 사용 하 여 논리 앱의 시작 tooget 참조 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.

## <a name="use-a-recurrence-trigger"></a>되풀이 트리거 사용
트리거는 사용 되는 toostart hello 워크플로 논리 앱에 정의 된 일 수 있는 이벤트입니다. [트리거에 대해 자세히 알아보세요.](connectors-overview.md)

시퀀스 tooset 되풀이를 트리거할 논리 앱 방법의 예는 다음과 같습니다.

1. Hello 추가 **되풀이** 트리거 논리 앱의 첫 번째 단계로 hello 합니다.
2. Hello 되풀이 간격에 대 한 hello 매개 변수를 입력 합니다.

hello 논리 앱 각 시간 간격 이후에 실행을 시작합니다.

![HTTP 트리거](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a>트리거 세부 정보
hello 되풀이 트리거 hello 다음과 같은 구성할 수 있는 속성에 있습니다.

지정된 시간 간격 후 논리 앱을 실행합니다.
A*는 필수 필드 임을 의미합니다.

| 표시 이름 | 속성 이름 | 설명 |
| --- | --- | --- |
| 빈도* |frequency |시간 단위 hello: `Second`, `Minute`, `Hour`, `Day`, 또는 `Year`합니다. |
| 간격* |interval |hello 간격 hello 되풀이 빈도 지정 하는 hello입니다. |
| 표준 시간대 |timeZone |UTC 오프셋 없이 시작 시간이 제공될 경우 이 시간대가 사용됩니다. |
| 시작 시간 |startTime |hello 시작 시간 [ISO 8601 형식](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations)합니다. |

<br>

## <a name="next-steps"></a>다음 단계
이제 hello 플랫폼을 사용해 및 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다. 탐색할 수 확인 하 여 논리 앱에서 사용할 수 있는 다른 커넥터 hello 우리의 [Api 목록](apis-list.md)합니다.

