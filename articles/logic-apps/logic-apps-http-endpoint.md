---
title: "aaaCall, 트리거 또는 중첩 된 HTTP 끝점-Azure 논리 앱 워크플로 | Microsoft Docs"
description: "Azure 논리 앱에 대 한 HTTP 끝점 toocall, 트리거 또는 중첩 워크플로를 설정 합니다."
services: logic-apps
keywords: "워크플로, HTTP 끝점"
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 73ba2a70-03e9-4982-bfc8-ebfaad798bc2
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 03/31/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 072a314c3bff75ab7696f86bb063bb7c03c4ae89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a>Logic Apps의 HTTP 끝점을 통해 워크플로 호출, 트리거 또는 중첩

URL을 통해 Logic Apps를 트리거 또는 호출할 수 있도록 동기식 HTTP 끝점을 기본적으로 논리 앱에 트리거로 표시할 수 있습니다. 또한 호출 가능 끝점의 패턴을 사용하여 Logic Apps에서 워크플로를 중첩할 수도 있습니다.

toocreate HTTP 끝점 논리 앱 들어오는 요청을 받을 수 있도록 이러한 트리거 추가할 수 있습니다.

* [요청](../connectors/connectors-native-reqres.md)

* [API 연결 웹후크](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [HTTP 웹후크](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > Hello를 사용 하는 예제 있지만 **요청** 트리거를 사용할 수 있습니다의 hello HTTP 트리거를 나열 하 고 모든 원칙 동일 하 게 toohello 다른 트리거 형식을 적용 합니다.

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a>논리 앱을 위해 HTTP 끝점 설정

HTTP 끝점을 toocreate 들어오는 요청을 받을 수 있는 트리거를 추가 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com "Azure 포털")합니다. Tooyour 논리 앱을 이동 하 고 논리 응용 프로그램 디자이너를 엽니다.

2. 논리 앱이 들어오는 요청을 받을 수 있도록 하는 트리거를 추가합니다. 예를 들어 hello 추가 **요청** 트리거 tooyour 논리 앱.

3.  아래 **요청 본문이 JSON 스키마**, hello 트리거 tooreceive 예상 하는 hello 페이로드 (데이터)에 대 한 JSON 스키마를 선택적으로 입력할 수 있습니다.

    hello 디자이너 tooconsume, parse 및 워크플로 통해 hello 트리거에서 패스 데이터 논리 앱 사용할 수는 토큰을 생성 하는 것에 대 한이 스키마를 사용 합니다. 
    [JSON 스키마에서 생성된 토큰](#generated-tokens)에 관한 추가 정보.

    예를 들어 hello 디자이너에 표시 하는 hello 스키마를 입력 합니다.

    ```json
    {
      "type": "object",
      "properties": {
        "address": {
          "type": "string"
        }
      },
      "required": [
        "address"
      ]
    }
    ```

    ![Hello 요청 동작 추가][1]

    > [!TIP]
    > 
    > 와 같은 도구에서 샘플 JSON 페이로드에 대 한 스키마를 생성할 수 있습니다 [jsonschema.net](http://jsonschema.net/), 또는 hello **요청** 선택 하 여 트리거 **사용 샘플 페이로드 toogenerate 스키마**합니다. 
    > 샘플 페이로드를 입력하고 **완료**를 선택합니다.

    예를 들어 다음 샘플 페이로드는:

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    다음 스키마를 생성합니다.

    ```json
    }
       "type": "object",
       "properties": {
          "address": {
             "type": "string" 
          }
       }
    }
    ```

4.  논리 앱을 저장합니다. **HTTP POST toothis URL**, 생성 된 콜백 URL이 예제에서와 같이 이제 찾아야 합니다.

    ![끝점에 대해 생성된 콜백 URL](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    이 URL 인증에 사용 되는 hello 쿼리 매개 변수에서 공유 액세스 서명 (SAS) 키를 포함 합니다. 
    또한 hello Azure 포털에서에서 논리 앱 개요에서 hello HTTP 끝점 URL을 가져올 수 있습니다. **트리거 기록** 아래에서 트리거를 선택합니다.

    ![Azure Portal에서 HTTP 끝점 URL 가져오기][2]

    또는이 호출 하 여 hello URL을 가져올 수 있습니다.

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-hello-http-method-for-your-trigger"></a>트리거에 대 한 hello HTTP 메서드를 변경 합니다.

기본적으로 hello **요청** 트리거 HTTP POST 요청을 하는데 다른 HTTP 메서드를 사용할 수 있습니다. 

> [!NOTE]
> 메서드 유형을 하나만 지정할 수 있습니다.

1. **요청** 트리거에서 **고급 옵션 표시**를 선택합니다.

2. 열기 hello **메서드** 목록입니다. 이 예의 경우 **GET**을 선택하면 HTTP 끝점의 URL을 나중에 테스트할 수 있습니다.

    > [!NOTE]
    > 다른 HTTP 메서드를 선택하거나 사용자의 고유한 논리 앱에 대한 사용자 지정 메서드를 지정할 수 있습니다.

    ![HTTP 메서드 변경](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a>HTTP 끝점 URL을 통해 매개 변수 허용

HTTP 끝점 URL tooaccept 매개 변수를 사용 하도록 하려는 경우 사용자 트리거의 상대 경로 지정 합니다.

1. **요청** 트리거에서 **고급 옵션 표시**를 선택합니다. 

2. 아래 **메서드**, 요청 toouse hello HTTP 메서드를 지정 합니다. 이 예에서는 선택 hello **가져오기** 메서드를 아직 없는 경우, HTTP 끝점의 URL을 테스트할 수 있도록 합니다.

      > [!NOTE]
      > 트리거에 대한 상대 경로를 지정하는 경우 트리거에 대한 HTTP 메서드도 명시적으로 지정해야 합니다.

3. 아래 **상대 경로**, 예를 들어 URL 허용 해야 하는 hello 매개 변수에 대 한 상대 경로 hello 지정 `customers/{customerID}`합니다.

    ![Hello HTTP 메서드 및 매개 변수에 대 한 상대 경로 지정 합니다.](./media/logic-apps-http-endpoint/relativeurl.png)

4. toouse hello 매개 변수를 추가 **응답** tooyour 논리 앱 작업 합니다. (트리거 아래에서 **새 단계** > **작업 추가** > **응답**을 선택) 

5. 사용자의 응답에 **본문**, trigger의 상대 경로에 지정 된 hello 매개 변수에 대 한 hello 토큰을 포함 합니다.

    예를 들어 tooreturn `Hello {customerID}`, 업데이트 응답의 **본문** 와 `Hello {customerID token}`합니다. 
    hello 동적 콘텐츠 목록을 표시 하 고 hello를 표시 해야 `customerID` tooselect 있습니다에 대 한 토큰입니다.

    ![Tooresponse 본문 매개 변수 추가](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    **본문**은 다음 예와 유사해야 합니다.

    ![매개 변수 포함 응답 본문](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. 논리 앱을 저장합니다. 

    HTTP 끝점 URL 포함 hello 상대 경로 지금 예: 

    https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...

7. 다른 브라우저 창에 업데이트 된 URL을 hello 있지만 대체할 HTTP 끝점, 복사 및 붙여넣기 tootest `{customerID}` 와 `123456`, Enter 키를 누릅니다.

    브라우저에 다음 텍스트가 표시되어야 합니다. 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a>논리 앱에 대한 JSON 스키마에서 생성된 토큰

JSON 스키마를 제공 하 여 **요청** 트리거, hello 논리가 응용 프로그램 디자이너에서 토큰을 생성 속성에 대 한 해당 스키마에 있습니다. 논리 앱 워크플로를 통해 데이터를 전달하는 데 해당 토큰을 사용할 수 있습니다.

예를 들어 hello를 추가 하는 경우 `title` 및 `name` 속성 tooyour JSON 스키마 토큰과 이후 워크플로 단계에서 사용 가능한 toouse 됩니다. 

Hello 완전 한 JSON 스키마는 다음과 같습니다.

```json
{
   "type": "object",
   "properties": {
      "address": {
         "type": "string"
      },
      "title": {
         "type": "string"
      },
      "name": {
         "type": "string"
      }
   },
   "required": [
      "address",
      "title",
      "name"
   ]
}
```

## <a name="create-nested-workflows-for-logic-apps"></a>Logic Apps에 대한 중첩 워크플로 만들기

요청을 받을 수 있는 다른 논리 앱을 추가하여 Logic Apps에서 워크플로를 중첩할 수 있습니다. tooinclude 이러한 논리 앱 추가 hello **Azure 논리 앱-선택 논리 앱 워크플로** tooyour 트리거 작업입니다. 그런 다음 자격이 있는 Logic Apps 중에서 선택할 수 있습니다.

![다른 논리 앱 추가](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a>HTTP 끝점을 통해 Logic Apps 호출 또는 트리거

HTTP 끝점을 만든 후를 통해 응용 프로그램 논리를 트리거할 수 있습니다는 `POST` 메서드 toohello 전체 URL입니다. Logic Apps는 직접 액세스 끝점에 대한 기본 제공 지원을 포함합니다.

## <a name="reference-content-from-an-incoming-request"></a>들어오는 요청의 콘텐츠 참조

Hello 콘텐츠의 종류를 `application/json`, hello 들어오는 요청에서 속성을 참조할 수 있습니다. 그렇지 않은 경우 콘텐츠는 tooother Api를 전달할 수 있습니다를 하나의 이진으로 처리 됩니다. tooreference hello 워크플로 내에 콘텐츠를 해당 콘텐츠를 변환 해야 합니다. 예를 들어, 전달 하는 경우 `application/xml` 콘텐츠를 사용할 수 있습니다 `@xpath()` 에서 XPath 추출에 대 한 또는 `@json()` XML tooJSON 변환 합니다. [콘텐츠 형식 사용](../logic-apps/logic-apps-content-type.md)에 대해 자세히 알아봅니다.

들어오는 요청에서 출력 tooget hello hello를 사용할 수 있습니다 `@triggerOutputs()` 함수입니다. 이 예제에서는 같은 hello 출력 형식입니다.

```json
{
    "headers": {
        "content-type" : "application/json"
    },
    "body": {
        "myProperty" : "property value"
    }
}
```

tooaccess hello `body` 속성 특히 있습니다 사용할 수 hello `@triggerBody()` 바로 가기 합니다. 

## <a name="respond-toorequests"></a>Toorequests 응답

Toorespond toocertain 요청 콘텐츠 toohello 호출자에 게 반환 하 여 논리 앱을 시작 하는 경우가 있습니다. hello tooconstruct hello 상태 코드, 헤더 및 응답 본문을 사용할 수 있습니다 **응답** 동작 합니다. 이 작업은 워크플로의 hello 끝 뿐 아니라 논리 앱에서 아무 곳 이나 나타날 수 있습니다.

> [!NOTE] 
> 논리 앱이 포함 되지 않은 경우는 **응답**, hello HTTP 끝점 응답 *즉시* 와 **202 수락 됨** 상태입니다. 또한 응답에 대 한 hello 원래 요청 tooget hello, hello 응답에 필요한 모든 단계 완료 해야 hello 내 [요청 시간 제한](./logic-apps-limits-and-config.md) hello 중첩된 논리 앱 워크플로 호출 하지 않으면 합니다. Hello 들어오는 요청 제한 시간이 초과 되며 hello HTTP 응답을 수신이 시간 동안 응답이 없는 경우 **408 클라이언트 시간 제한**합니다. 중첩 된 논리 앱에 대 한 hello 부모 논리 앱에 대 한 응답 시간을 필요에 관계 없이 완료 될 때까지 toowait를 계속 합니다.

### <a name="construct-hello-response"></a>Hello 응답 생성

Hello 응답 본문에 둘 이상의 헤더 및 모든 종류의 콘텐츠를 포함할 수 있습니다. 우리의 예제 응답 hello 헤더 지정 hello 응답의 콘텐츠 형식은 `application/json`합니다. hello 본문에 포함 하 고 `title` 및 `name`hello에 대 한 이전에 업데이트 된 hello JSON 스키마에 따라 **요청** 트리거.

![HTTP 응답 작업][3]

응답 속성:

| 속성 | 설명 |
| --- | --- |
| statusCode |응답 toohello 들어오는 요청에 대 한 hello HTTP 상태 코드를 지정합니다. 이 코드는 2xx, 4xx 또는 5xx로 시작하는 모든 유효한 상태 코드가 될 수 있습니다. 하지만 3xx 상태 코드는 허용되지 않습니다. |
| headers |Hello에 대 한 응답 헤더 tooinclude 개수에 관계 없이 정의합니다. |
| body |문자열, JSON 개체 또는 이전 단계에서 참조한 이진 콘텐츠일 수도 있는 본문 개체를 지정합니다. |

다음은 hello에 대 한 이제 처럼 보이지만 어떤 hello JSON 스키마 **응답** 동작:

``` json
"Response": {
   "inputs": {
      "body": {
         "title": "@{triggerBody()?['title']}",
         "name": "@{triggerBody()?['name']}"
      },
      "headers": {
           "content-type": "application/json"
      },
      "statusCode": 200
   },
   "runAfter": {},
   "type": "Response"
}
```

> [!TIP]
> 논리 앱 hello 논리가 응용 프로그램 디자이너에 대 한 tooview hello 전체 JSON 정의 선택 **코드 뷰**합니다.

## <a name="q--a"></a>질문과 대답

#### <a name="q-what-about-url-security"></a>Q: URL 보안이란 무엇입니까?

A: Azure는 공유 액세스 서명(SAS)을 사용하여 논리 앱 콜백 URL을 안전하게 생성합니다. 이 서명은 쿼리 매개 변수로 전달되고 논리 앱이 시작하기 전에 유효성이 검사되어야 합니다. Azure 논리 앱, hello 트리거 이름 및 hello 작업을 수행 하는 비밀 키의 고유 조합을 사용 하 여 hello 서명을 생성 합니다. 따라서은 사용자가 액세스 toohello 비밀 논리 응용 프로그램 키, 하지 않는 한 유효한 서명을 생성할 수 없습니다.

   > [!IMPORTANT]
   > 프로덕션 환경과 보안 시스템에서는 권장 하지 하기 때문에 hello 브라우저에서 직접 논리 앱을 호출 합니다.
   > 
   > * 공유 액세스 키 hello hello URL에 표시 됩니다.
   > * 여러 논리 앱 고객 tooshared 도메인 인해 콘텐츠 보안 정책을 관리할 수 없습니다.

#### <a name="q-can-i-configure-http-endpoints-further"></a>Q: HTTP 끝점을 추가로 구성할 수 있습니까?

A: 예, HTTP 끝점은 [**API Management**](../api-management/api-management-key-concepts.md)를 통해 고급 구성을 지원합니다. 이 서비스는 또한 hello 기능을 제공 하면 tooconsistently 논리 앱을 포함 하 여 모든 Api 관리에 대 한 하 고, 사용자 지정 도메인 이름을 설정 하 고, 인증 방법의 자세한 등에 사용 예:

* [Hello 요청 방법 변경](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [Hello 요청의 hello URL 세그먼트를 변경 합니다.](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* Hello에서 API 관리 도메인 설정 [Azure 포털](https://portal.azure.com/ "Azure 포털")
* 기본 인증에 대 한 정책 toocheck 설정

#### <a name="q-what-changed-when-hello-schema-migrated-from-hello-december-1-2014-preview"></a>Q: hello 스키마 hello 2014 년 12 월 1 일 미리 보기에서 마이그레이션할 때 변경?

A: 다음은 이러한 변경 내용에 대한 요약입니다.

| 2014 년 12 월 1 일 미리 보기 | 2016년 6월 1일 |
| --- | --- |
| **HTTP 수신기** API 앱 클릭 |**수동 트리거** 클릭(API 앱 필요 없음) |
| HTTP 수신기 설정 "*자동으로 응답 보내기*" |포함 된 **응답** 동작 또는 hello 워크플로 정의에 없는 |
| 기본 또는 OAuth 인증 구성 |API Management를 통해 |
| HTTP 메서드 구성 |**고급 옵션 표시** 아래에서 HTTP 메서드를 선택합니다. |
| 상대 경로 구성 |**고급 옵션 표시** 아래에서 상대 경로를 추가합니다. |
| 통해 참조 hello 들어오는 본문`@triggerOutputs().body.Content` |`@triggerOutputs().body`을 통해 참조합니다. |
| **HTTP 응답을 보냅니다** hello HTTP 수신기에 대 한 작업 |클릭 **응답 tooHTTP 요청** (API 앱 필요) |

## <a name="get-help"></a>도움말 보기

tooask 질문 질문에 답변 하 고 다른 Azure 논리 앱을 수행 하는 사용자가 방문 hello 자세한 [Azure 논리 앱 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)합니다.

Azure 논리 앱 및 커넥터 향상, 투표 하거나 hello에서 아이디어 제출 toohelp [Azure 논리 앱 사용자 의견 사이트](http://aka.ms/logicapps-wish)합니다.

## <a name="next-steps"></a>다음 단계

* [작성자 논리 앱 정의](./logic-apps-author-definitions.md)
* [오류 및 예외 처리](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
