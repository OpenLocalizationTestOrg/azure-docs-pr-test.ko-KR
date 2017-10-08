---
title: "aaaCreate 웹 Api 및 REST Api는 커넥터-Azure 논리 앱 | Microsoft Docs"
description: "Azure 논리 앱 시스템 통합에 대 한 워크플로의 웹 Api 및 REST Api toocall Api, 서비스 또는 시스템 만들기"
keywords: "웹 API, REST API, 커넥터, 워크플로, 시스템 통합"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: bd229179-7199-4aab-bae0-1baf072c7659
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/26/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 2792204d1d298a6f810e75211c1789ee204c2fdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-apis-as-connectors-for-logic-apps"></a>사용자 지정 API를 논리 앱용 커넥터로 만들기

Azure 논리 앱 제공 하지만 [100 + 기본 제공 커넥터](../connectors/apis-list.md) 논리 앱 워크플로에서 사용할 수 있는지 toocall 시스템, Api를 할 수 있습니다 및 커넥터로 사용할 수 없는 서비스입니다. 논리 앱의 동작 및 트리거 toouse 제공 하는 사용자 고유의 사용자 지정 Api를 만들 수 있습니다. 이유 toocreate 직접 다른 이유는 Api 너무 논리 앱에서 커넥터를 사용 하 여:

* 현재의 시스템 통합 및 데이터 통합 워크플로를 확장합니다.
* 서비스 toomanage 전문가 또는 개인 소유 작업을 사용 하는 데 도움이 됩니다.
* Hello 도달 범위, 검색 기능 및 서비스에 대 한 용도 확장 합니다.

기본적으로 커넥터는 플러그형 인터페이스에 대한 REST, 문서에 대한 [Swagger 메타데이터 형식](http://swagger.io/specification/) 및 JSON(데이터 교환 형식)을 사용하는 웹 API입니다. 커넥터는 HTTP 끝점을 통해 통신하는 REST API이므로 .NET, Java 또는 Node.js와 같은 언어를 사용하여 커넥터를 빌드할 수 있습니다. Api를 호스팅할 수도 있습니다 [Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md)는 플랫폼으로-서비스 (PaaS) API 호스팅을 위한 제공 하는 hello 가장 쉽고 가장 확장성이 뛰어난 방법 중 하나를 제공 합니다. 

논리 앱 사용자 지정 Api toowork, API를 제공할 수 [ *동작* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) 논리 앱 워크플로에서 특정 작업을 수행 하는 합니다. 또한 API는 [*트리거*](./logic-apps-what-are-logic-apps.md#logic-app-concepts)의 역할을 수행하여 새 데이터 또는 이벤트가 지정된 조건을 충족할 때 논리 앱 워크플로를 시작할 수도 있습니다. 이 항목에서는 동작 및 api에서 트리거를 구축 하기 위한 참고할 수 있는 일반적인 패턴을 설명 하려는 API tooprovide hello 동작에 따라 합니다.

> [!TIP] 
> 사용자 Api로 배포할 수 있지만 [웹 앱](../app-service-web/app-service-web-overview.md),으로 Api를 배포 하는 것이 좋습니다. [API 앱](../app-service-api/app-service-api-apps-why-best-platform.md)는 수 작업을 손쉽게 수행할 빌드, 호스팅 및 hello 클라우드 및 온-프레미스 Api를 사용 하는 경우. Toochange 모든 코드에에서 없는 Api-방금 코드 tooan API 앱을 배포 합니다. 너무 방법에 대해 알아봅니다 [ASP.NET을 사용 하 여 만든 API 앱을 빌드할](../app-service-api/app-service-api-dotnet-get-started.md), [Java](../app-service-api/app-service-api-java-api-app.md), 또는 [Node.js](../app-service-api/app-service-api-nodejs-api-app.md)합니다. 
>
> 논리 앱 용으로 작성 된 샘플 API 앱에 대 한 방문 hello [Azure 논리 앱 GitHub 리포지토리](http://github.com/logicappsio) 또는 [블로그](http://aka.ms/logicappsblog)합니다.

## <a name="helpful-tools"></a>유용한 도구

사용자 지정 API 때 가장 효과적인 논리 앱 hello API에는 [Swagger 문서](http://swagger.io/specification/) hello API의 작업 및 매개 변수를 설명 하는 합니다.
많은 라이브러리와 같은 [Swashbuckle](https://github.com/domaindrivendev/Swashbuckle), hello Swagger 파일을 자동으로 생성할 수 있습니다. 표시 이름, 속성 형식 등에 대 한 tooannotate hello Swagger 파일을 사용할 수도 있습니다 [TRex](https://github.com/nihaue/TRex) Swagger 파일 논리 앱와 잘 작동 하도록 합니다.

<a name="actions"></a>

## <a name="action-patterns"></a>동작 패턴

논리 앱 tooperform 작업에 대 한 사용자 지정 API를 제공 해야 [ *동작*](./logic-apps-what-are-logic-apps.md#logic-app-concepts)합니다. API의 각 작업 tooan 작업을 매핑합니다. 기본 동작은 HTTP 요청을 받아들이고 HTTP 응답을 반환하는 컨트롤러입니다. 예를 들어 논리 앱 HTTP 요청 tooyour 웹 응용 프로그램 또는 API 앱에 보냅니다. 응용 프로그램 논리를 hello 내용과 함께 처리할 수 있는, 앱 다음 HTTP 응답을 반환 합니다.

표준 동작의 경우 API에 HTTP 요청 메서드를 작성하고 해당 메서드를 Swagger 파일에 설명할 수 있습니다. 그런 다음 [HTTP 동작](../connectors/connectors-native-http.md) 또는 [HTTP + Swagger](../connectors/connectors-native-http-swagger.md) 동작을 사용하여 API를 직접 호출할 수 있습니다. 기본적으로 응답 해야 이내에 반환 되어야 hello [요청 시간 제한](./logic-apps-limits-and-config.md)합니다. 

![표준 동작 패턴](./media/logic-apps-create-api-app/standard-action.png)

<a name="pattern-overview"></a>논리 앱 API 긴 실행 작업을 완료 하는 동안 잠시 기다려 toomake, API hello를 따를 수 [비동기 폴링 패턴](#async-pattern) 또는 hello [비동기 webhook 패턴](#webhook-actions) 이 항목에서 설명 합니다. 이러한 패턴의 서로 다른 동작을 시각화 하는 데 도움이 되는 유추는 bakery에서 사용자 지정 케이크 순서에 대 한 hello 프로세스를 가정해 봅니다. hello 폴링 패턴 hello 동작을 호출 하는 위치 hello bakery 마다 20 분 toocheck hello 케이크 준비 되었는지 여부를 반영 합니다. hello webhook 패턴 여기서 hello bakery 묻는 전화 번호에 대 한 hello 케이크가 준비 되 면 있습니다를 호출할 수 있습니다 이러한 hello 동작을 미러링합니다.

샘플을 방문 hello [논리 앱 GitHub 리포지토리](https://github.com/logicappsio)합니다. 또한 [동작 사용량 측정](logic-apps-pricing.md)에 대해서도 자세히 알아보세요.

<a name="async-pattern"></a>

### <a name="perform-long-running-tasks-with-hello-polling-action-pattern"></a>폴링 작업 패턴 hello로 장기 실행 작업을 수행 합니다.

hello 보다 오래 실행 될 수 있는 작업을 수행 하는 API toohave [요청 시간 제한](./logic-apps-limits-and-config.md), hello 비동기 폴링 패턴을 사용할 수 있습니다. 이 패턴에는 별도 스레드에서 그대로 유지 하는 활성 연결 toohello 논리 앱 엔진에서 작동 하 여 API 수행 합니다. 이런 방식으로 hello 논리 앱 시간 제한이 실행 되지 않음 또는 API 작업을 완료 하기 전에 hello 워크플로 hello 다음 단계를 계속 진행 합니다.

Hello 일반적인 패턴은:

1. 해당 hello 엔진 API hello 요청을 수락 하 고 작업을 시작 알고 있는지 확인 합니다.
2. Hello 엔진 작업 상태에 대 한 후속 요청을 하면 API hello 작업 완료 되 면 hello 엔진을 알리는 합니다.
3. Hello 논리 앱 워크플로 계속할 수 있도록 관련성이 높은 데이터 toohello 엔진을 반환 합니다.

<a name="bakery-polling-action"></a>이제 hello 이전 bakery 비유 toohello 폴링 패턴을 적용 하 고 호출 하는 한 bakery 및 순서 사용자 지정 케이크 배달용 한다고 가정 합니다. hello 케이크 하기 위해 hello 프로세스 시간이 걸리고 hello bakery hello 케이크에서 작동 하는 동안 hello 전화에서 toowait 않을 합니다. hello bakery 주문을 확인 하 고 hello 케이크 상태에 대 일 분 마다을 호출할 수를 포함 합니다. 20 분 통과 hello bakery를 호출 하지만 케이크 수행 되지 않습니다 및 하면 호출 하는 다른 20 분 알 수 있습니다. 이 / 및-사후 프로세스를 호출 하 고 hello bakery 알려 주문 준비 되어 있고 케이크 배달 될 때까지 계속 됩니다. 

이제 폴링 패턴을 다시 매핑해 보겠습니다. hello bakery hello 논리 앱 엔진을 나타내는 hello 케이크 고객 있습니다 하는 동안 사용자 지정 API를 나타냅니다. 요청과 함께 API를 호출 하는 hello 엔진 API에서 hello 요청 확인 및 hello 엔진 작업 상태를 확인할 수 있는 경우 hello 시간 간격을 사용 하 여 응답 합니다. hello 엔진 계속 API 해당 hello 작업이 완료 되어 응답할 때까지 작업 상태 및 다음 워크플로 계속 반환 데이터 tooyour 논리 앱을 검사 합니다. 

![폴링 동작 패턴](./media/logic-apps-create-api-app/custom-api-async-action-pattern.png)

Hello API의 관점에서 설명 하 여 API toofollow hello 구체적인 단계는 다음과 같습니다.

1. 때 API 가져옵니다는 HTTP 요청 toostart 작업을 즉시 반환 HTTP `202 ACCEPTED` hello로 응답 `location` 헤더가이 단계의 뒷부분에서 설명 합니다. 이 응답에는 처리 및 엔진 API 내용이 있는지 알고 논리 앱 hello 요청을 수락 된 hello 요청 페이로드 (데이터 입력) hello를 있습니다. 
   
   hello `202 ACCEPTED` 응답 이러한 헤더를 포함 합니다.
   
   * *필요한*: A `location` hello 절대 경로 tooa URL hello 논리 앱 엔진 API의 작업 상태를 확인할 수를 지정 하는 헤더

   * *선택적*: A `retry-after` hello 엔진 hello 초 수를 지정 하는 헤더 hello를 검사 하기 전에 대기 해야 `location` 작업 상태에 대 한 URL입니다. 

     기본적으로 hello 엔진 20 초 마다 확인합니다. hello를 포함 하는 간격을 다르게 toospecify `retry-after` 머리글과 hello hello 다음 폴링 될 때까지 초 수입니다.

2. Hello 논리 앱 설문 hello 엔진 hello 지정 시간이 지남에 후 `location` URL toocheck 작업 상태입니다. API는 이러한 검사를 수행하고 다음과 같은 응답을 반환해야 합니다.
   
   * Hello 작업이 수행 되 면 반환 HTTP `200 OK` hello 응답 페이로드 (hello 다음 단계에 대 한 입력)와 함께 응답 합니다.

   * Hello 작업이 처리 되 고 다른 HTTP 반환 `202 ACCEPTED` hello 이지만 응답으로 hello 원래 응답으로 동일한 헤더입니다.

사용자가 API는이 패턴을 따르는 때 toodo 아무 것도에 없는 hello 논리 앱 워크플로 정의 toocontinue 작업 상태를 확인 합니다. Hello 엔진 HTTP 가져옵니다 하는 경우 `202 ACCEPTED` 응답 및 유효한 `location` 헤더, hello 엔진 측면 hello 비동기 패턴 및 검사 hello `location` API-202 응답을 반환할 때까지 헤더입니다.

> [!TIP]
> 비동기 패턴 예제는 [GitHub의 비동기 컨트롤러 응답 샘플](https://github.com/logicappsio/LogicAppsAsyncResponseSample)(영문)을 검토하세요.

<a name="webhook-actions"></a>

### <a name="perform-long-running-tasks-with-hello-webhook-action-pattern"></a>Hello webhook 작업 패턴으로 장기 실행 작업을 수행 합니다.

대신 장기 실행 작업 및 비동기 처리에 대 한 hello webhook 패턴을 사용할 수 있습니다. 이 패턴에는 hello 논리 앱을 일시 중지 하 고 워크플로 계속 하기 전에 처리 하 여 API toofinish에서 "callback" 때까지 대기 합니다. 이 콜백은 이벤트가 발생할 때 메시지 tooa URL 보내는 HTTP POST입니다. 

<a name="bakery-webhook-action"></a>이제 hello 이전 bakery 비유 toohello webhook 패턴을 적용 하 고 호출 하는 한 bakery 및 순서 사용자 지정 케이크 배달용 한다고 가정 합니다. hello 케이크 하기 위해 hello 프로세스 시간이 걸리고 hello bakery hello 케이크에서 작동 하는 동안 hello 전화에서 toowait 않을 합니다. hello bakery 주문 확인 하지만이 이번에 게 전화 번호가 hello 케이크 수행 되는 경우 있습니다를 호출할 수 있습니다. 이 시간 hello bakery 표시 때 주문 준비 케이크를 제공 합니다.

이 webhook 패턴을 다시 매핑할 있습니다 hello bakery 있습니다, hello 케이크 고객, 나타내는 hello 논리 앱 엔진 하는 동안 사용자 지정 API를 나타냅니다. hello 엔진은 요청과 함께 API를 호출 하 고 "callback" URL이 포함 됩니다.
Hello 작업이 수행 되는 경우 API hello URL toonotify hello 엔진을 사용 하 고 워크플로 계속 데이터 tooyour 논리 앱을 반환 합니다. 

이 패턴의 경우 컨트롤러에 두 개의 끝점(`subscribe` 및 `unsubscribe`)을 설정합니다.

*  `subscribe`끝점: hello 논리 앱 호출 hello 엔진 실행 hello 워크플로에서 API의 동작에 도달 하면 `subscribe` 끝점입니다. 이 단계를 수행 하면 hello 논리 앱 toocreate API를 저장 하 고 다음 API에서 hello 콜백에 대 한 대기 작업이 완료 되는 콜백 URL입니다. API 다음 HTTP POST toohello URL로 다시 호출 하 고 반환 된 모든 내용과 헤더 입력된 toohello 논리가 응용 프로그램으로 전달 합니다.

* `unsubscribe`끝점: hello 논리 앱 엔진 호출 hello hello 논리 앱을 실행 취소 될 경우 `unsubscribe` 끝점입니다. 다음 API hello 콜백 URL 등록을 취소 하 고 필요에 따라 모든 프로세스를 중지할 수 있습니다.

![웹후크 동작 패턴](./media/logic-apps-create-api-app/custom-api-webhook-action-pattern.png)

> [!NOTE]
> 현재 논리 응용 프로그램 디자이너 hello Swagger 통해 webhook 끝점 검색을 지원 하지 않습니다. 이 패턴에 대 한 tooadd 해야 하므로 [ **Webhook** 동작](../connectors/connectors-native-webhook.md) hello URL, 헤더 및 요청에 대 한 본문을 지정 합니다. [워크플로 작업 및 트리거](logic-apps-workflow-actions-triggers.md#api-connection-webhook-action)도 참조하세요. hello 콜백 URL에 toopass, hello를 사용할 수 있습니다 `@listCallbackUrl()` hello 이전 필드에 필요에 따라 워크플로 기능.

> [!TIP]
> 웹후크 패턴 예제는 [GitHub의 웹후크 트리거 샘플](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/WebhookTriggerController.cs)(영문)을 검토하세요.

<a name="triggers"></a>

## <a name="trigger-patterns"></a>트리거 패턴

사용자 지정 API는 [*트리거*](./logic-apps-what-are-logic-apps.md#logic-app-concepts)의 역할을 수행하여 새 데이터 또는 이벤트가 지정된 조건을 충족할 때 논리 앱을 시작할 수 있습니다. 이 트리거는 서비스 끝점에서 새 데이터 또는 이벤트를 정기적으로 확인하거나 대기 및 수신 대기할 수 있습니다. 새 데이터 또는 이벤트 충족 하는 경우 지정 된 조건 hello, hello 트리거가 발생 하 고 toothat 트리거를 수신 하는 hello 논리 앱을 시작 합니다. toostart 논리 앱이 방식이으로 API hello를 따를 수 [ *폴링 트리거* ](#polling-triggers) 또는 hello [ *webhook 트리거* ](#webhook-triggers) 패턴입니다. 이러한 패턴은 유사한 tootheir 대응 항목에 대 한 [작업 폴링](#async-pattern) 및 [webhook 작업](#webhook-actions)합니다. 또한 [트리거 사용량 측정](logic-apps-pricing.md)에 대해서도 자세히 알아보세요.

<a name="polling-triggers"></a>

### <a name="check-for-new-data-or-events-regularly-with-hello-polling-trigger-pattern"></a>트리거 패턴 폴링 hello로 정기적으로 새 데이터 또는 이벤트에 대 한 확인

A *폴링 트리거* hello와 비슷하게 작동 [작업 폴링](#async-pattern) 이전에이 항목에서 설명 합니다. hello 논리 앱 엔진은 주기적으로 호출 하 고 새 데이터 또는 이벤트에 대 한 hello 트리거 끝점을 확인 합니다. Hello 엔진에서 새 데이터 나 사용자 지정 된 조건을 충족 하는 이벤트를 찾으면 hello 트리거가 실행 됩니다. 그런 다음 hello 엔진 hello 데이터를 입력으로 처리 하는 논리 앱 인스턴스를 만듭니다. 

![폴링 트리거 패턴](./media/logic-apps-create-api-app/custom-api-polling-trigger-pattern.png)

> [!NOTE]
> 논리 앱 인스턴스를 만들지 않은 경우에도 각 폴링 요청은 동작 실행으로 간주됩니다. tooprevent 처리 동일한 데이터를 여러 번 hello, 트리거가 이미 읽기 / toohello 논리 앱을 전달 하는 데이터를 정리 해야 합니다.

Hello API의 관점에서 설명 하는 폴링 트리거에 대 한 구체적인 단계는 다음과 같습니다.

| 새 데이터 또는 이벤트가 있습니까?  | API 응답 | 
| ------------------------- | ------------ |
| 있음 | HTTP 반환 `200 OK` hello 응답 페이로드 (다음 단계에 대 한 입력)에 있는 상태입니다. <br/>이 응답 논리 앱 인스턴스를 만들고 hello 워크플로 시작 합니다. |
| 찾을 수 없음 | `location` 헤더 및 `retry-after` 헤더와 함께 HTTP `202 ACCEPTED` 상태를 반환합니다. <br/>트리거, hello `location` 헤더를 포함 해야는 `triggerState` "타임 스탬프."는 일반적으로 쿼리 매개 변수 API hello 논리는 마지막으로이 식별자 tootrack hello צ ְ ײ 앱 트리거 되었습니다. |

예를 들어 tooperiodically 새 파일에 대 한 서비스를 확인, 이러한 동작을 가진 폴링 트리거를 만들 수 있습니다.

| 요청에 `triggerState`가 있습니까? | API 응답 |
| -------------------------------- | -------------|
| 아니요 | HTTP 반환 `202 ACCEPTED` 상태 뒤에 `location` 헤더와 `triggerState` toohello 현재 시간을 설정 하 고 hello `retry-after` 간격 too15 (초)입니다. |
| 예 | Hello 뒤에 추가 하는 파일에 대 한 서비스를 확인 `DateTime` 에 대 한 `triggerState`합니다. |

| 검색된 파일의 수 | API 응답 |
| --------------------- | -------------|
| 단일 파일 | HTTP 반환 `200 OK` 상태 및 hello 콘텐츠 페이로드, 업데이트 `triggerState` toohello `DateTime` hello 파일을 반환 하 고 설정에 대 한 `retry-after` 간격 too15 (초)입니다. |
| 여러 파일 | HTTP 한 번에 하나의 파일 반환 `200 OK` 상태, 업데이트 `triggerState`, 및 집합 hello `retry-after` 간격 too0 (초)입니다. </br>다음이 단계에는 더 많은 데이터를 사용할 수 있으며 해당 hello 엔진 hello에 hello URL에서 hello 데이터를 즉시 요청 해야 hello 엔진 알리는 `location` 헤더입니다. |
| 파일 없음 | HTTP 반환 `202 ACCEPTED` 상태를 변경 하지 않습니다. `triggerState`, 및 집합 hello `retry-after` 간격 too15 (초)입니다. |

> [!TIP]
> 폴링 트리거 패턴 예제는 [GitHub의 폴 트리거 컨트롤러 샘플](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/PollTriggerController.cs)(영문)을 검토하세요.

<a name="webhook-triggers"></a>

### <a name="wait-and-listen-for-new-data-or-events-with-hello-webhook-trigger-pattern"></a>기다린 후 새 데이터 또는 hello webhook 트리거 패턴으로 이벤트를 수신 대기

웹후크 트리거는 서비스 끝점에서 새 데이터 또는 이벤트를 대기하고 수신 대기하는 *푸시 트리거*입니다. 새 데이터 또는 이벤트 충족 하는 경우 hello는 지정한 조건, hello 트리거가 발생 하 고 입력으로 hello 데이터를 처리 하는 논리 앱 인스턴스를 만듭니다.
Webhook 트리거 작동할 것과 마찬가지로 hello [webhook 작업](#webhook-actions) 이전에이 항목에서 설명 하 고 적절 한 `subscribe` 및 `unsubscribe` 끝점입니다. 

* `subscribe`끝점: hello 논리 앱 엔진 호출 hello 추가 논리가 응용 프로그램에 webhook 트리거를 저장할 때 `subscribe` 끝점입니다. 이 단계를 수행 하면 hello 논리 앱 toocreate API를 저장 하는 콜백 URL입니다. 새 데이터가 또는 충족 하는 이벤트가 hello 지정 된 조건, 사용자가 API는 HTTP POST toohello URL로 다시 호출 합니다. hello 콘텐츠 페이로드 및 헤더 입력된 toohello 논리 앱으로 전달합니다.

* `unsubscribe`끝점: hello 논리 앱 엔진 호출 hello hello webhook 트리거 또는 전체 논리 앱을 삭제 한 경우 `unsubscribe` 끝점입니다. 다음 API hello 콜백 URL 등록을 취소 하 고 필요에 따라 모든 프로세스를 중지할 수 있습니다.

![웹후크 트리거 패턴](./media/logic-apps-create-api-app/custom-api-webhook-trigger-pattern.png)

> [!NOTE]
> 현재 논리 응용 프로그램 디자이너 hello Swagger 통해 webhook 끝점 검색을 지원 하지 않습니다. 이 패턴에 대 한 tooadd 해야 하므로 [ **Webhook** 트리거](../connectors/connectors-native-webhook.md) hello URL, 헤더 및 요청에 대 한 본문을 지정 합니다. [HTTPWebhook 트리거](logic-apps-workflow-actions-triggers.md#httpwebhook-trigger)도 참조하세요. hello 콜백 URL에 toopass, hello를 사용할 수 있습니다 `@listCallbackUrl()` hello 이전 필드에 필요에 따라 워크플로 기능.
>
> tooprevent 처리 동일한 데이터를 여러 번 hello, 트리거가 이미 읽기 / toohello 논리 앱을 전달 하는 데이터를 정리 해야 합니다.

> [!TIP]
> 웹후크 패턴 예제는 [GitHub의 웹후크 트리거 컨트롤러 샘플](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/WebhookTriggerController.cs)(영문)을 검토하세요.

## <a name="deploy-call-and-secure-custom-apis"></a>사용자 지정 API 배포, 호출 및 보호

사용자 지정 API를 만든 후 배포를 위한 API를 설정하여 안전하게 호출할 수 있도록 합니다. 너무 방법에 대해 알아봅니다[배포를 호출 하 고 논리 앱에 대 한 사용자 지정 Api secure](./logic-apps-custom-hosted-api.md)합니다.

## <a name="publish-custom-apis-tooazure"></a>사용자 지정 Api tooAzure 게시

toomake 사용자 사용자 지정 Api에서에서 사용할 수 있는 공용 Azure 위한 추천 toohello 제출 [Microsoft Azure 인증 프로그램](https://azure.microsoft.com/marketplace/programs/certified/logic-apps/)합니다.

## <a name="get-help"></a>도움말 보기

사용자 지정 API에 대한 구체적인 지원은 [customapishelp@microsoft.com](mailto:customapishelp@microsoft.com)에 문의해 주세요.

tooask 질문과 대답 질문 참조를 수행 하는 다른 Azure 논리 앱 사용자가 방문 hello [Azure 논리 앱 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)합니다.

논리 앱 및 커넥터 향상, 투표 하거나 hello에서 아이디어 제출 toohelp [논리 앱 사용자 의견 사이트](http://aka.ms/logicapps-wish)합니다. 

## <a name="next-steps"></a>다음 단계

* [동작 및 트리거에 대한 사용량 측정](logic-apps-pricing.md)
* [콘텐츠 형식 처리](./logic-apps-content-type.md)
* [오류 및 예외 처리](./logic-apps-exception-handling.md)
* [Tooyour 논리 앱 액세스 보안](./logic-apps-securing-a-logic-app.md)
* [HTTP 끝점을 통해 논리 앱 호출, 트리거 또는 중첩](./logic-apps-http-endpoint.md)