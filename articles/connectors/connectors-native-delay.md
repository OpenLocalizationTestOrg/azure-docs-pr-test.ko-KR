---
title: "논리 앱의 지연 aaaAdd | Microsoft Docs"
description: "Hello 간략하게 지연 시간 및 지연을-동작, 방법과 toouse Azure 논리 앱을 사용 하 여 합니다."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 915f48bf-3bd8-4656-be73-91a941d0afcd
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e5bc9d639adbddc01ee0f6a4c68716f586d4344a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-delay-and-delay-until-actions"></a>Hello로 시작 지연 시간 및 지연을-동작
Hello 지연을 사용 하 여 및 "지연-될 때까지" 작업을 워크플로 시나리오를 완료할 수 있습니다.

예를 들어 다음을 수행할 수 있습니다.

* 전자 메일을 통해 평일 toosend 상태가 업데이트 될 때까지 기다립니다.
* HTTP 호출 될 때까지 지연 hello 워크플로 다시 시작 하 고 hello 결과 검색 하기 전에 시간 toofinish에 있습니다.

tooget hello 지연 작업을 사용 하 여 논리 앱에서 시작 참조 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.

## <a name="use-hello-delay-actions"></a>Hello 지연 작업을 사용 하 여
동작은 논리 앱에 정의 된 hello 워크플로 통해 수행 되는 작업입니다. [작업에 대해 자세히 알아봅니다.](connectors-overview.md)

시퀀스 toouse 지연 단계 논리 앱 방법의 예는 다음과 같습니다.

1. 트리거를 추가한 후 클릭 **새 단계** tooadd 동작 합니다.
2. 검색할 **지연** toobring hello 지연 동작을 합니다. 이 예제에서는 **지연**을 선택합니다.
   
    ![지연 작업](./media/connectors-native-delay/using-action-1.png)
3. Hello 동작 속성 tooconfigure hello 지연 중 하나를 완료 합니다.
   
    ![지연 구성](./media/connectors-native-delay/using-action-2.png)
4. 클릭 **저장** toopublish hello 논리 앱을 활성화 합니다.

## <a name="action-details"></a>작업 세부 정보
hello 되풀이 트리거 hello 다음과 같은 구성 될 수 있는 속성에 있습니다.

### <a name="delay-action"></a>지연 동작
이 작업 시간 지연 hello 특정 시간 간격에 대 한 실행 합니다.
*는 필수 필드임을 의미합니다.

| 표시 이름 | 속성 이름 | 설명 |
| --- | --- | --- |
| Count* |count |시간 단위 toodelay hello 수 |
| Unit* |단위 |시간 단위 hello: `Second`, `Minute`, `Hour`, 또는`Day` |

<br>

### <a name="delay-until-action"></a>다음 기간까지 지연 동작
이 작업에 지정된 된 날짜/시간까지 실행 하는 hello를 지연 됩니다.
*는 필수 필드임을 의미합니다.

| 표시 이름 | 속성 이름 | 설명 |
| --- | --- | --- |
| Year* |timestamp |hello 연도 toodelay (GMT)까지 |
| Month* |timestamp |hello 월 toodelay (GMT)까지 |
| Day* |timestamp |hello 일 toodelay (GMT)까지 |

<br>

## <a name="next-steps"></a>다음 단계
이제 hello 플랫폼을 사용해 및 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다. 탐색할 수 확인 하 여 논리 앱에서 사용할 수 있는 다른 커넥터 hello 우리의 [Api 목록](apis-list.md)합니다.

