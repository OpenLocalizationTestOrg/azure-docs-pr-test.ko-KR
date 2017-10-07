---
title: "aaaUse 요청 및 응답 동작 | Microsoft Docs"
description: "Hello 요청 및 응답 트리거와 작업이 바뀐 Azure 논리 앱에서의 개요"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 566924a4-0988-4d86-9ecd-ad22507858c0
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: 24c378cc12d5f3f65116d5e59278236186a99662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-request-and-response-components"></a>Hello 요청 및 응답 구성 요소 시작
Hello 요청 및 응답의에서 구성 요소와 논리 앱을 실시간으로 tooevents에 응답할 수 있습니다.

예를 들어 다음을 수행할 수 있습니다.

* 논리 앱을 통해 온-프레미스 데이터베이스에서 데이터 tooan HTTP 요청에 응답 합니다.
* 외부 웹후크 이벤트에서 논리 앱을 트리거합니다.
* 다른 논리 앱 내에서 요청 및 응답 작업으로 논리 앱을 호출합니다.

hello 요청 및 응답 작업을 사용 하 여 논리 앱의 시작 tooget 참조 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.

## <a name="use-hello-http-request-trigger"></a>HTTP 요청 트리거 hello를 사용 하 여
트리거는 사용 되는 toostart hello 워크플로 논리 앱에 정의 된 일 수 있는 이벤트입니다. [트리거에 대해 자세히 알아보세요.](connectors-overview.md)

시퀀스는 HTTP tooset hello 논리가 응용 프로그램 디자이너에서에서 요청 하는 방법을의 예는 다음과 같습니다.

1. Hello 트리거 추가 **요청-때 HTTP 요청을 받으면** 논리 앱에서 합니다. JSON 스키마를 선택적으로 제공할 수 있습니다 (같은 도구를 사용 하 여 [JSONSchema.net](http://jsonschema.net)) hello 요청 본문에 대 한 합니다. 따라서 hello HTTP 요청에서 속성에 대 한 hello 디자이너 toogenerate 토큰 수 있습니다.
2. Hello 논리 앱을 저장할 수 있도록 다른 동작을 추가 합니다.
3. Hello 논리 앱을 저장 한 후 hello 요청 카드에서 hello HTTP 요청 URL을 가져올 수 있습니다.
4. HTTP POST (같은 도구를 사용할 수 있습니다 [우체부](https://www.getpostman.com/)) toohello URL 트리거 hello 논리 앱.

> [!NOTE]
> 응답 작업을 정의 하지 않으면 한 `202 ACCEPTED` 응답 toohello 호출자에 게 즉시 반환 됩니다. Hello 응답 동작 toocustomize 응답을 사용할 수 있습니다.
> 
> 

![응답 트리거](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-hello-http-response-action"></a>HTTP 응답 동작 hello를 사용 하 여
HTTP 응답 동작 hello HTTP 요청에 의해 트리거되는 워크플로에서 사용 하는 경우에 유효 합니다. 응답 작업을 정의 하지 않으면 한 `202 ACCEPTED` 응답 toohello 호출자에 게 즉시 반환 됩니다.  Hello 워크플로 내에서 모든 단계에서 응답 동작을 추가할 수 있습니다. hello 논리 앱만 hello 들어오는 요청을 열어 둡니다 응답에 대 일 분이 걸립니다.  Hello 워크플로에서 보낸 응답이 없는 (응답 동작에에서 있는 경우 hello 정의), 1 분 후에 `504 GATEWAY TIMEOUT` toohello 호출자에 게 반환 됩니다.

다음은 어떻게 tooadd HTTP 응답 동작:

1. 선택 hello **새 단계** 단추입니다.
2. **작업 추가**를 선택합니다.
3. Hello 동작 검색 상자에 입력 **응답** toolist hello 응답 동작 합니다.
   
    ![Hello 응답 동작을 선택 합니다.](./media/connectors-native-reqres/using-action-1.png)
4. Hello HTTP 응답 메시지에 필요한 매개 변수를 추가 합니다.
   
    ![전체 hello 응답 동작](./media/connectors-native-reqres/using-action-2.png)
5. Hello 도구 모음 toosave와 여 논리 앱에서 모두 저장 hello 왼쪽 위 모퉁이 클릭 하 고 게시 (활성화).

## <a name="request-trigger"></a>요청 트리거
이 커넥터가 지 원하는 hello 트리거에 대 한 hello 세부 정보는 다음과 같습니다. 단일 요청 트리거가 있습니다.

| 트리거 | 설명 |
| --- | --- |
| 요청 |HTTP 요청을 받을 때 발생합니다. |

## <a name="response-action"></a>응답 작업
이 커넥터가 지 원하는 hello 동작에 대 한 hello 세부 정보는 다음과 같습니다. 요청 트리거와 함께 나올 때만 사용할 수 있는 단일 응답 작업이 있습니다.

| 작업 | 설명 |
| --- | --- |
| 응답 |응답 toohello HTTP 요청 상관 관계를 반환 합니다. |

### <a name="trigger-and-action-details"></a>트리거 및 작업 세부 정보
hello 다음 표에서 hello hello 트리거 및 작업에 대 한 입력된 필드에 설명 하 고 해당 출력 세부 정보를 hello 합니다.

#### <a name="request-trigger"></a>요청 트리거
hello 다음은 들어오는 HTTP 요청에서 트리거 hello에 대 한 입력된 필드입니다.

| 표시 이름 | 속성 이름 | 설명 |
| --- | --- | --- |
| JSON 스키마 |schema |hello HTTP 요청 본문의 hello JSON 스키마 |

<br>

**출력 세부 정보**

hello 요청에 대 한 출력 세부 내용은 hello 다음과가 같습니다.

| 속성 이름 | 데이터 형식 | 설명 |
| --- | --- | --- |
| headers |object |헤더 요청 |
| 본문 |object |요청 개체 |

#### <a name="response-action"></a>응답 작업
hello 다음은 HTTP 응답 동작 hello에 대 한 입력된 필드입니다. *는 필수 필드임을 의미합니다.

| 표시 이름 | 속성 이름 | 설명 |
| --- | --- | --- |
| 상태 코드* |statusCode |hello HTTP 상태 코드 |
| 헤더 |headers |모든 응답 헤더 tooinclude의 JSON 개체 |
| body |body |hello 응답 본문 |

## <a name="next-steps"></a>다음 단계
이제 hello 플랫폼을 사용해 및 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다. 탐색할 수 확인 하 여 논리 앱에서 사용할 수 있는 다른 커넥터 hello 우리의 [Api 목록](apis-list.md)합니다.

