---
title: "aaaWorkflow 동작 및 트리거-Azure 논리 앱 | Microsoft Docs"
description: 
services: logic-apps
author: MandiOhlinger
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 86a53bb3-01ba-4e83-89b7-c9a7074cb159
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/17/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 857927b7d7df3fc9cdc4931ffdb613efde0db9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a>Azure Logic Apps의 워크플로 작업 및 트리거

논리 앱은 트리거와 작업으로 구성됩니다. 트리거에는 여섯 가지 유형이 있습니다. 각 유형마다 서로 다른 인터페이스 및 동작을 포함합니다. Hello의 hello 세부 정보를 확인 하 여 다른 세부 정보에 대해 알아볼 수 있습니다 [워크플로 정의 언어](logic-apps-workflow-definition-language.md)합니다.  
  
비즈니스 프로세스와 워크플로 트리거 및 동작 사용 하는 방법으로 toobuild 논리 앱 tooimprove에 대해 자세히 toolearn 계속 읽어 보십시오.  
  
### <a name="triggers"></a>트리거  

트리거 논리 앱 워크플로 실행을 시작할 수 있는 hello 호출을 지정 합니다. Hello 두 가지 방법으로 tooinitiate 워크플로 실행 하는 다음과 같습니다.  
  
-   폴링 트리거  

-   Hello 호출 하 여 밀어넣기 트리거- [워크플로 서비스 REST API](https://docs.microsoft.com/rest/api/logic/workflows)  
  
모든 트리거는 다음과 같은 상위 수준 요소를 포함합니다.  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property toocreate runs for>",
    "operationOptions": "<operation options on hello trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a>트리거 유형 및 해당 입력  

다음과 같은 트리거 유형을 사용할 수 있습니다.
  
-   **요청** \- toocall 있습니다에 대 한 끝점 hello 논리 앱을 사용 하면  
  
-   **Recurrence** \- 정의된 일정에 따라 실행합니다.  
  
-   **HTTP** \- HTTP 웹 끝점을 폴링합니다. hello HTTP 끝점 tooa 특정 트리거 계약을 준수 해야 \- 202를 사용 하 여\-비동기 패턴 또는 배열을 반환 하 여  
  
-   **그러나 ApiConnection** \- 설문 hello HTTP와 같은 트리거, 이용할 hello [Microsoft 관리 Api](https://docs.microsoft.com/azure/connectors/apis-list)  
  
-   **그러나 HTTPWebhook** \- 끝점의 경우 유사한 toohello 수동 트리거가 호출 tooa 아웃 URL tooregister 지정 및 등록 취소  
  
-   **ApiConnectionWebhook** \- HTTPWebhook 트리거 hello Microsoft 관리 Api 활용 하 여 hello 처럼 작동 합니다.       
    각 트리거 형식은 해당 동작을 정의하는 서로 다른 **입력** 집합을 포함합니다.  
  
## <a name="request-trigger"></a>요청 트리거  

이 트리거 논리 앱을 통해 HTTP 요청 tooinvoke 호출 하는 끝점으로 사용 됩니다. 요청 트리거는 다음 예제와 같이 표시됩니다.  
  
```json
"<name-of-the-trigger>" : {
    "type" : "request",
    "kind": "http",
    "inputs" : {
        "schema" : {
            "properties" : {
                "myInputProperty1" : { "type" : "string" },
                "myInputProperty2" : { "type" : "number" }
            },
        "required" : [ "myInputProperty1" ],
        "type" : "object"
        }
    }
} 
```

또한 **schema**라는 선택적 속성도 있습니다.  
  
|요소 이름|필수|설명|  
|----------------|------------|---------------|  
|schema|아니요|Hello 들어오는 요청을 확인 하는 JSON 스키마입니다. 이후 워크플로 단계 알고 있는 속성 tooreference 수 있도록 지 원하는 데 유용 합니다.|

tooinvoke이이 끝점 toocall hello 해야 *listCallbackUrl* API입니다. [워크플로 서비스 REST API](https://docs.microsoft.com/rest/api/logic/workflows)를 참조하세요.  
  
## <a name="recurrence-trigger"></a>되풀이 트리거  

되풀이 트리거는 정의된 일정에 따라 실행됩니다. 이러한 트리거는 다음 예제와 같이 표시될 수 있습니다.  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

볼 수 있듯이 간단한 방법을 toorun 워크플로 됩니다.  
  
|요소 이름|필수|설명|  
|----------------|------------|---------------|  
|frequency|예|얼마나 자주 hello 트리거 실행 됩니다. second, minute, hour, day, week, month 또는 year 중에 하나만 사용할 수 있습니다.|  
|interval|예|Hello 되풀이 빈도 지정 하는 hello의 간격|  
|startTime|아니요|UTC 오프셋 없이 startTime이 제공될 경우 이 timeZone이 사용됩니다.|  
|timeZone|no|UTC 오프셋 없이 startTime이 제공될 경우 이 timeZone이 사용됩니다.|  
  
특정 시점 이후 hello에서 트리거 toostart 실행을 예약할 수 있습니다. 예를 들어 toostart 주 단위 매주 월요일을 보고 하려는 경우 예약할 수 있습니다 hello 논리 앱 toostart 매주 월요일 hello 다음 트리거를 만들어:  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Week",
        "interval": "1",
        "startTime" : "2015-06-22T00:00:00Z"
    }
}
```

## <a name="http-trigger"></a>HTTP 트리거  

HTTP 트리거 폴링을 지정 된 끝점 및 hello 응답 toodetermine를 hello 워크플로 실행 해야 하는지 여부를 확인 합니다. 필요한 tooconstruct HTTP 호출을 매개 변수는 hello 집합을 사용 하는 hello 입력 개체:  
  
|요소 이름|필수|설명|형식|  
|----------------|------------|---------------|--------|  
|메서드|yes|Hello HTTP 메서드를 다음 중 하나일 수 있습니다: GET, POST, PUT, DELETE, 패치 또는 H e a d|문자열|  
|uri|yes|hello http 또는 https 끝점을 호출 합니다. 최대 2킬로바이트입니다.|string|  
|쿼리|아니요|Hello 쿼리 매개 변수 tooadd toohello URL을 나타내는 개체입니다. 예를 들어 `"queries" : { "api-version": "2015-02-01" }` 추가 `?api-version=2015-02-01` toohello URL입니다.|Object|  
|headers|아니요|각각의 toohello 요청이 발송 되 hello 머리글을 나타내는 개체입니다. 예를 들어 tooset hello 언어 및 요청에는 형식:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|Object|  
|body|아니요|Toohello 끝점으로 전송 되는 hello 페이로드를 나타내는 개체입니다.|Object|  
|retryPolicy|아니요|4xx 또는 5xx 오류에 대 한 hello 다시 시도 동작을 사용자 지정할 수 있는 개체입니다.|Object|  
|authentication|아니요|요청 hello 나타냅니다 hello 메서드를 인증 해야 합니다. 이 개체에 대한 자세한 내용은 [스케줄러 아웃바운드 인증](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)을 참조하세요. 스케줄러 이외에도 지원되는 속성이 하나 더 있습니다. `authority` 기본적으로 이 값은 지정되지 않은 경우 `https://login.windows.net`이지만 `https://login.windows\-ppe.net`과 같이 다른 대상 그룹을 사용할 수 있습니다.|Object|  
  
hello HTTP 트리거 논리 앱 함께 특정 패턴 toowork와 hello HTTP API tooconform이 필요합니다. 다음 필드는 hello 필요:  
  
|응답|설명|  
|------------|---------------|  
|상태 코드|상태 코드 200 \(확인\) toocause 실행 합니다. 다른 상태 코드이면 실행이 진행되지 않습니다.|  
|Retry\-after 헤더|Hello 논리 앱 hello 끝점을 다시 폴링하여 될 때까지 초 수입니다.|  
|위치 헤더|hello 다음 폴링 간격에 대 한 hello URL toocall 합니다. 지정 하지 않으면 hello 원래 URL이 사용 됩니다.|  
  
다양한 요청 유형의 다양한 동작에 대한 예는 다음과 같습니다.  
  
|응답 코드|Retry\-After|동작|  
|-----------------|----------------|------------|  
|200|\(없음\)|하지 유효한 트리거를 다시 시도\-필수 또는 다른 hello 엔진을는 후 hello 다음 요청에 대 한 폴링 되지 않습니다.|  
|202|60|Hello 워크플로 트리거하지 않습니다. hello 다음 시도가 1 분 후에 발생합니다.|  
|200|10|Hello 워크플로 실행 하 고 10 초 후에 더 많은 콘텐츠 다시 확인 합니다.|  
|400|\(없음\)|잘못 된 요청 hello 워크플로 실행 하지 마십시오. 없는 경우 없는 **을 다시 시도 정책** 정의 hello 기본 정책이 사용 됩니다. Hello 재시도 횟수에 도달 하면 hello 트리거를 더 이상 사용할 합니다.|  
|500|\(없음\)|서버 오류를 hello 워크플로 실행 하지 마십시오입니다.  없는 경우 없는 **을 다시 시도 정책** 정의 hello 기본 정책이 사용 됩니다. Hello 재시도 횟수에 도달 하면 hello 트리거를 더 이상 사용할 합니다.|  
  
hello 출력의 HTTP 트리거는이 예제와 같습니다.  
  
|요소 이름|설명|형식|  
|----------------|---------------|--------|  
|headers|hello http 응답의 hello 헤더입니다.|Object|  
|body|hello http 응답의 hello 본문입니다.|Object|  
  
## <a name="api-connection-trigger"></a>API 연결 트리거  

hello API 연결 트리거는 기본 기능에 비슷한 toohello HTTP 트리거입니다. 그러나 hello 동작을 식별 하는 것에 대 한 hello 매개 변수는 다릅니다. 다음은 예제입니다.  
  
```json
"dailyReport" : {
    "type": "ApiConnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://myarticles.example.com/"
            },
        }
        "connection": {
            "name": "@parameters('$connections')['myconnection'].name"
        }
    },  
    "method": "POST",
    "body": {
        "category": "awesomest"
    }
}
```

|요소 이름|필수|형식|설명|  
|----------------|------------|--------|---------------|  
|host|예||hello ApiApp 호스팅되는 게이트웨이 및 id입니다.|  
|메서드|예|문자열|Hello HTTP 메서드를 다음 중 하나일 수 있습니다: **가져오기**, **POST**, **배치**, **삭제**, **패치**, 또는  **H E A D**|  
|쿼리|아니요|Object|나타냅니다 hello 쿼리 매개 변수 toobe toohello URL을 추가 합니다. 예를 들어 `"queries" : { "api-version": "2015-02-01" }` 추가 `?api-version=2015-02-01` toohello URL입니다.|  
|headers|아니요|Object|각각의 toohello 요청이 발송 되 hello 머리글을 나타냅니다. 예를 들어 tooset hello 언어 및 요청에는 형식:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|body|아니요|Object|Toohello 끝점으로 전송 되는 hello 페이로드를 나타냅니다.|  
|retryPolicy|아니요|Object|4xx 또는 5xx 오류 toocustomize hello 다시 시도 동작이 있습니다.|  
|인증|아니요|Object|요청 hello 나타냅니다 hello 메서드를 인증 해야 합니다. 이 개체에 대한 자세한 내용은 [스케줄러 아웃바운드 인증](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)을 참조하세요.|  
  
호스트에 대 한 hello 속성은 같습니다.  
  
|요소 이름|필수|설명|  
|----------------|------------|---------------|  
|api runtimeUrl|예|관리 되는 API의 hello hello 끝점입니다.|  
|connection name||참조 tooa 매개 변수를 호출 해야 `$connection` hello 워크플로 사용 하 여 관리 하는 hello API 연결의 hello 이름입니다.|
  
API 연결 트리거의 hello 출력 됩니다.
  
|요소 이름|형식|설명|  
|----------------|--------|---------------|  
|headers|Object|hello http 응답의 hello 헤더입니다.|  
|body|Object|hello http 응답의 hello 본문입니다.|  
  
## <a name="httpwebhook-trigger"></a>HTTPWebhook 트리거  

hello HTTPWebhook 트리거는 끝점, 비슷한 toohello 수동 트리거 있지만 hello HTTPWebhook 트리거 tooa 아웃 계획도 URL tooregister 지정 열리고 등록을 취소 합니다. HTTPWebhook 트리거의 예는 다음과 같습니다.  

```json
"myappspottrigger": {
    "type": "httpWebhook",
    "inputs": {
        "subscribe": {
            "method": "POST",
            "uri": "https://pubsubhubbub.appspot.com/subscribe",
            "headers": { },
            "body": {
                "hub.callback": "@{listCallbackUrl()}",
                "hub.mode": "subscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "authentication": { },
            "retryPolicy": { }
        },
        "unsubscribe": {
            "url": "https://pubsubhubbub.appspot.com/subscribe",
            "body": {
                "hub.callback": "@{workflow().endpoint}@{listCallbackUrl()}",
                "hub.mode": "unsubscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "method": "POST",
            "authentication": { }
        }
    },
    "conditions": [ ]
    }
```

이 섹션에서는 다양 한 사항이 며 hello Webhook의 hello 동작 섹션을 제공 하거나 생략 됩니다에 따라 달라 집니다.  
Webhook의 hello 속성은 다음과 같습니다.  
  
|요소 이름|필수|설명|  
|----------------|------------|---------------|  
|subscribe|아니요|나가는 요청 hello 트리거가 만들어집니다 및 hello 초기 등록을 수행할 때 호출 되는 번호입니다.|  
|unsubscribe|아니요|hello hello 트리거를 삭제 요청을 송신 합니다.|  
  
-   **구독** hello toostart 수신 tooevents가 변경한 호출 나갑니다. 이 호출이 동일한 일반 HTTP 작업 hello 매개 변수 집합이 않습니다 hello로 시작 합니다. 나가는 호출이 만들어진 모든 시간 hello 어떤 방식으로든에서 워크플로 변경 내용을, 예를 들어 때마다 hello 자격 증명을 전달 하는, 또는 hello 트리거의 입력 매개 변수 변경 합니다.
  
    toosupport 호출이 새 함수가: `@listCallbackUrl()`합니다. 이 함수는 이 워크플로에서 특정 트리거에 대해 고유한 URL을 반환합니다. Hello hello 서비스 REST를 사용 하는 hello 끝점에 대 한 고유 식별자를 나타냅니다.  
  
-   **Unsubscribe**는 다음과 같이 작업에서 이 트리거를 무효화하도록 렌더링할 때 호출됩니다.  
  
    -   삭제 또는 hello 트리거 비활성화  
  
    -   삭제 또는 hello 워크플로 사용 하지 않도록 설정  
  
    -   삭제 하거나 hello 구독 해제 합니다.  
  
    hello를 자동으로 호출 하는 hello 논리 앱 작업 구독을 취소 합니다. hello 매개 변수 toothis 함수는 hello HTTP 트리거로 hello 동일 합니다.  
  
    hello hello HTTPWebhook 트리거의 출력은 hello 들어오는 요청의 hello 내용을:  
  
|요소 이름|형식|설명|  
|-----------------|--------|---------------|  
|headers|Object|hello http 요청의 hello 헤더입니다.|  
|body|Object|hello hello http 요청 본문입니다.|  

Hello webhook 작업에 대 한 제한을 지정할 수와 동일 하 게 [HTTP 비동기 제한](#asynchronous-limits)합니다.
  

## <a name="conditions"></a>조건  

모든 트리거 여부 hello 워크플로 실행 해야 하는지 여부를 하나 이상의 조건 toodetermine를 사용할 수 있습니다. 예:  

```json
"dailyReport" : {
    "type": "recurrence",
    "conditions": [ {
        "expression": "@parameters('sendReports')"
    } ],
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

이 경우 hello 워크플로 하는 동안 보고서만 트리거 hello `sendReports` 매개 변수가 tootrue 설정 됩니다. 마지막으로, 조건이 hello 트리거의 hello 상태 코드를 참조할 수 있습니다. 예를 들어 다음과 같이 웹 사이트에서 상태 코드 500을 반환하는 경우에만 워크플로를 시작할 수 있습니다.
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> 모든 식 hello 트리거의 hello 상태 코드를 참조 하는 경우 \(어떤 방식으로든에서\), 기본 동작을 hello \(200에 대해서만 트리거 \(확인\) \) 대체 됩니다. 예를 들어, 상태 코드 200와 상태 코드 201 tootrigger 원하는 있으면 tooinclude: `@or(equals(triggers().code, 200),equals(triggers().code,201))` 조건으로 합니다.  
  
## <a name="start-multiple-runs-for-a-request"></a>요청에 대해 여러 실행 시작

단일 요청에 대 한 여러 실행 오프 tookick `splitOn` 유용, 예를 들어 toopoll 폴링 간격 사이 여러 새 항목을 가질 수 있는 끝점을 사용 하려는 경우.
  
와 `splitOn`, 원하는 각 항목의 hello 배열이 포함 된 hello 응답 페이로드 내 hello 속성 지정 toouse toostart hello 트리거를 실행 하는 합니다. 예를 들어 hello 다음 응답을 반환 하는 API가 있는 같이 가정해 봅니다.  
  
```json
{
    "Status" : "success",
    "Rows" : [
        {  
            "id" : 938109380,
            "name" : "mycoolrow"
        },
        {
            "id" : 938109381,
            "name" : "another row"
        }
    ]
}
```
  
논리 앱 하기만 hello 행 콘텐츠이 예제에서와 같이 트리거가 작성할 수 있습니다.  
  
```json
"mysplitter" : {
    "type" : "http",
    "recurrence": {
        "frequency": "Minute",
        "interval": "1"
    },
    "intputs" : {
        "uri" : "https://mydomain.com/myAPI",
        "method" : "GET"
    },
    "splitOn" : "@triggerBody()?.Rows"
}
```
  
그런 다음, hello 워크플로 정의 `@triggerBody().name` 반환 `mycoolrow` 를 처음 실행 하는 hello에 대 한 및 `another row` hello 두 번째 실행에 대 한 합니다. 이 예제에서와 같이 hello 트리거 출력 보기:  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

사용 하는 경우에 따라서 `SplitOn`, 외부에 있는 hello 배열에이 예에서 hello hello 속성을 가져올 수 없는 `Status` 필드입니다.  
  
> [!NOTE]  
> 이 예제에서는 사용 하 여 hello `?` 연산자 toobe 수 tooavoid 문제일 경우 hello `Rows` 속성 나타나지 않습니다. 
  
## <a name="single-run-instance"></a>단일 실행 인스턴스

되풀이 속성 tooonly 화재 되어 모든 활성 실행 완료 하는 경우 트리거를 구성할 수 있습니다. 예약 된 되풀이 되는 경우 진행 중인 실행 중이면 hello 트리거를 건너뛰어 hello 다음 예약 된 되풀이 간격 toocheck 다시 될 때까지 대기 합니다.

Hello 작업 옵션을 통해이 설정을 구성할 수 있습니다.

```json
"triggers": {
    "mytrigger": {
        "type": "http",
        "inputs": { ... },
        "recurrence": { ... },
        "operationOptions": "singleInstance"
    }
}
```

## <a name="types-and-inputs"></a>형식 및 입력  

다양한 작업 형식이 있으며 각각 고유한 동작을 포함합니다. 컬렉션 작업은 자체적으로 여러 다른 작업을 포함할 수 있습니다.

### <a name="standard-actions"></a>표준 작업  

-   **HTTP** 이 작업은 HTTP 웹 끝점을 호출합니다.  
  
-   **ApiConnection** \- HTTP 동작 hello와 비슷하게 동작 하는이 작업 이지만 사용 하 여 hello Microsoft에서 관리 하는 Api입니다.  
  
-   **ApiConnectionWebhook** \- 같은 HTTPWebhook 하지만 사용 하 여 hello Microsoft 관리 Api입니다.  
  
-   **Response** \- 들어오는 호출에 대한 응답을 정의합니다.  
  
-   **Wait** \- 정해진 시간 동안 기다리거나 특정 시간까지 대기하는 단순한 작업입니다.  
  
-   **Workflow** \- 중첩된 워크플로를 나타냅니다.  

-   **Function** \- 이 작업은 Azure Function을 나타냅니다.

### <a name="collection-actions"></a>컬렉션 작업

-   **Scope** \- 다른 작업의 논리적 그룹화입니다.

-   **조건** \- 이 식을 계산 하는 작업과 hello 해당 결과 분기를 실행 합니다.

-   **ForEach** \- 이 루프 작업은 배열을 반복하고 각 항목에 대해 내부 작업을 수행합니다.

-   **될 때까지** \- 조건 결과 tootrue 될 때까지이 반복 작업 내부 작업을 실행 합니다.
  
각 작업 형식은 작업의 동작을 정의하는 서로 다른 **입력** 집합을 포함합니다.  
  
## <a name="http-action"></a>HTTP 동작  

지정 된 끝점을 호출 하 고 hello 워크플로 실행 해야 하는지 여부를 hello 응답 toodetermine를 확인 하는 HTTP 작업 합니다. hello **입력** 필요한 tooconstruct hello HTTP 호출 매개 변수는 hello 집합을 사용 하는 개체:  
  
|요소 이름|필수|형식|설명|  
|----------------|------------|--------|---------------|  
|메서드|예|문자열|Hello HTTP 메서드를 다음 중 하나일 수 있습니다: **가져오기**, **POST**, **배치**, **삭제**, **패치**, 또는  **H E A D**|  
|uri|예|문자열|hello http 또는 https 끝점을 호출 합니다. 최대 길이는 2킬로바이트입니다.|  
|쿼리|아니요|Object|Hello 쿼리 매개 변수 tooadd toohello URL을 나타냅니다. 예를 들어 `"queries" : { "api-version": "2015-02-01" }` 추가 `?api-version=2015-02-01` toohello URL입니다.|  
|headers|아니요|Object|각각의 toohello 요청이 발송 되 hello 머리글을 나타냅니다. 예를 들어 tooset hello 언어 및 요청에는 형식:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|body|아니요|Object|Toohello 끝점으로 전송 되는 hello 페이로드를 나타냅니다.|  
|retryPolicy|아니요|Object|4xx 또는 5xx 오류에 대 한 hello 다시 시도 동작을 사용자 지정할 수 있습니다.|  
|operationsOptions|아니요|문자열|특별 한 동작 toooverride hello 집합을 정의합니다.|  
|인증|아니요|Object|요청 hello 나타냅니다 hello 메서드를 인증 해야 합니다. 이 개체에 대한 자세한 내용은 [스케줄러 아웃바운드 인증](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)을 참조하세요. 스케줄러 이외에도 지원되는 속성이 하나 더 있습니다. `authority` 기본적으로 지정되지 않은 경우 `https://login.windows.net`이지만 `https://login.windows\-ppe.net`과 같이 다른 대상 그룹을 사용할 수 있습니다.|  
  
HTTP 작업 \(및 API 연결\) 작업은 다시 시도 정책을 지원합니다. 다시 시도 정책은 toointermittent 오류, HTTP 상태에 대 한 규정 적용 408, 429, 및 추가 tooany 연결 예외가 5xx 코드로 작성 합니다. 이 정책은 hello를 사용 하 여 설명 *retryPolicy* 다음과 같이 정의 된 개체:
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
hello 다시 시도 간격 hello ISO 8601 형식으로 지정 됩니다. Hello 최 댓 값은 1 시간 동안이 간격에 기본값 및 최소값 20 초 있습니다. hello 기본 및 최대 재시도 수는 4 시간입니다. Hello 재시도 정책 정의 지정 하지 않은 경우는 `fixed` 전략이 기본 다시 시도 횟수 및 간격 값으로 사용 합니다. toodisable hello 재시도 정책을 설정 타입이 너무`None`합니다.  
  
예를 들어 hello 다음 작업을 다시 시도 반입 hello 최신 뉴스를 두 번 시도 사이의 30 초의 지연 시간에 세 개의 실행 환경에서는 총 일시적인 오류가 발생 하는 경우:  
  
```json
"latestNews" : {
    "type": "http",
    "inputs": {
        "method": "GET",
        "uri": "https://mynews.example.com/latest",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT30S",
            "count": 2
        }
    }
}
```
### <a name="asynchronous-patterns"></a>비동기 패턴

기본적으로 모든 HTTP 기반 동작 hello 표준 비동기 작업 패턴을 지원 합니다. Hello 원격 서버 hello 요청을 나타내는 경우 202 사용 하 여 처리에 대 한 허용 됩니다 하므로 \("승인 됨"\) 응답으로 hello 논리 앱 엔진 터미널에 도달할 때까지 hello 응답의 위치 헤더에 지정 된 hello URL 폴링 유지 상태 \(비\-202 응답\)합니다.  
  
이전에 toodisable hello 비동기 동작에서 설명한 설정는 `DisableAsyncPattern` hello 작업 입력에 있는 옵션입니다. 이 경우 hello 작업의 출력 hello hello hello 서버에서 초기 202 응답은 기반으로 합니다.  
  
```json
"invokeLongRunningOperation" : {
    "type": "http",
    "inputs": {
        "method": "POST",
        "uri": "https://host.example.com/resources"
    },
    "operationOptions": "DisableAsyncPattern"
}
```

#### <a name="asynchronous-limits"></a>비동기 제한

비동기 패턴은 해당 기간 tooa 특정 시간 간격에 제한 될 수 있습니다.  Hello 동작의 hello 상태 표시될지 터미널 상태에 도달 하지 않고 hello 시간 간격이 지나면 `Cancelled` 코드 `ActionTimedOut`합니다.  hello 제한 시간 초과 ISO 8601 형식에 지정 됩니다.  제한 구문 다음 hello로 지정할 수 있습니다.

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a>API 연결  

API 연결은 Microsoft 관리 커넥터를 참조하는 작업입니다.
이 작업에 hello API 및 필요한 매개 변수 방법과 참조 tooa 유효한 연결이 필요 합니다.

|요소 이름|필수|형식|설명|  
|----------------|------------|--------|---------------|  
|host|예|Object|Hello runtimeUrl 및 참조 toohello connection 개체와 같은 hello 커넥터 정보를 나타냅니다.|
|메서드|예|문자열|Hello HTTP 메서드를 다음 중 하나일 수 있습니다: **가져오기**, **POST**, **배치**, **삭제**, **패치**, 또는  **H E A D**|  
|path|예|문자열|hello API 작업의 hello 경로입니다.|  
|쿼리|아니요|Object|Hello 쿼리 매개 변수 tooadd toohello URL을 나타냅니다. 예를 들어 `"queries" : { "api-version": "2015-02-01" }` 추가 `?api-version=2015-02-01` toohello URL입니다.|  
|headers|아니요|Object|각각의 toohello 요청이 발송 되 hello 머리글을 나타냅니다. 예를 들어 tooset hello 언어 및 요청에는 형식:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|body|아니요|Object|Toohello 끝점으로 전송 되는 hello 페이로드를 나타냅니다.|  
|retryPolicy|아니요|Object|4xx 또는 5xx 오류에 대 한 hello 다시 시도 동작을 사용자 지정할 수 있습니다.|  
|operationsOptions|아니요|문자열|특별 한 동작 toooverride hello 집합을 정의합니다.|  

```json
"Send_Email": {
    "type": "apiconnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "method": "post",
        "body": {
            "Subject": "New Tweet from @{triggerBody()['TweetedBy']}",
            "Body": "@{triggerBody()['TweetText']}",
            "To": "me@example.com"
        },
        "path": "/Mail"
    },
    "runAfter": {}
    }
```

## <a name="api-connection-webhook-action"></a>API 연결 웹후크 작업

```json
"Send_approval_email": {
    "type": "apiconnectionwebhook",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "body": {
            "Message": {
                "Subject": "Approval Request",
                "Options": "Approve, Reject",
                "Importance": "Normal",
                "To": "me@email.com"
            }
        },
        "path": "/approvalmail",
        "authentication": "@parameters('$authentication')"
    },
    "runAfter": {}
}
```

Hello webhook 작업에 대 한 제한을 지정할 수와 동일 하 게 [HTTP 비동기 제한](#asynchronous-limits)합니다.
  
## <a name="response-action"></a>응답 작업  

이 동작 형식이 HTTP 요청에서 hello 전체 응답 페이로드를 포함 하 고는 statusCode, 본문 및 헤더를 포함:  
  
```json
"myresponse" : {
    "type" : "response",
    "inputs" : {
        "statusCode" : 200,
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        },
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        }
    },
    "runAfter": {}
}
```
  
hello 응답 동작 tooother 동작이 적용 되지 않는 특별 한 제한이 있습니다. 구체적으로 살펴보면 다음과 같습니다.  
  
-   결정적 응답 toohello 들어오는 요청이 필요 하므로 응답 작업 정의에 병렬 일 수 없습니다.  
  
-   Hello 들어오는 요청에 응답을 받은 후 응답 동작에 도달 하면, hello 동작 것으로 간주 됩니다 실패 \(충돌\), 되며 결과적으로, 실행 하는 hello `Failed`합니다.  
  
-   응답 작업이 있는 워크플로는 한 번의 호출로 여러 개의 실행이 발생하므로 해당 트리거에 `splitOn`을 포함할 수 없습니다. 결과적으로,이 유효성을 검사 해야 hello 흐름은 PUT 및 원인은 잘못 된 요청 하는 경우.  
  
## <a name="wait-action"></a>대기 작업  

hello `wait` 동작 hello 지정 된 간격에 대 한 워크플로 실행을 일시 중단 합니다. 예를 들어, toowait 15 분이 코드이 조각을 사용할 수 있습니다.  
  
```json
"waitForFifteenMinutes" : {
    "type": "wait",
    "inputs": {
        "interval": {
            "unit" : "minute",
            "count" : 15
        }
    }
}
```  
  
또는 toowait를 특정 시점에에서 될 때까지이 예제를 사용할 수 있습니다.  
  
```json
"waitUntilOctober" : {
    "type": "wait",
    "inputs": {
        "until": {
            "timestamp" : "2016-10-01T00:00:00Z"
        }
    }
}
```
  
> [!NOTE]  
> hello 대기 시간이 하거나 지정할 수 hello를 사용 하 여 **간격** 개체나 hello **될 때까지** 개체가 아니라 둘 중 하나입니다.  
  
|이름|필수|형식|설명|  
|--------|------------|--------|---------------|  
|interval|아니요|Object|hello 대기 시간에 따라 기간.|  
|interval unit|예|String|second, minute, hour, day, week, month, year 간격 중 하나입니다.|  
|interval count|예|문자열|내부 단위를 지정 하는 hello에 따라 기간입니다.|  
|until|아니요|Object|hello 대기 시간에는 지점에 기반 하는 기간.|  
|until timestamp|예|문자열|문자열 &#124; hello 지정 hello 대기 만료 될 때 utc에서 시간입니다.|  

## <a name="query-action"></a>쿼리 작업

hello `query` 작업을 사용 하면 조건에 따라 배열을 필터링 합니다. 예를 들어 tooselect 2 보다 큰 숫자를 사용할 수 있습니다.

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

hello 출력 hello `query` 동작은 hello 조건을 만족 하는 hello 입력 배열에서 요소가 포함 된 배열입니다.

> [!NOTE]
> Hello를 만족 하는 값이 없는 경우 `where` 조건의 경우 hello 결과 빈 배열입니다.

|이름|필수|형식|설명|
|--------|------------|--------|---------------|
|from|예|배열|hello 소스 배열입니다.|
|여기서,|예|문자열|hello 조건 tooapply tooeach hello 소스 배열의 요소입니다.|

## <a name="select-action"></a>작업 선택

hello `select` 작업을 사용 하면 새 값으로는 배열의 각 요소를 프로젝션 합니다.
예를 들어, 개체의 배열에는 숫자의 배열을 tooconvert 다음을 사용할 수 있습니다.

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

출력의 hello hello `select` 동작은 hello 하 여 hello 동일한 카디널리티 변환 된 각 요소와 입력된 배열의 hello으로 정의 된 배열을 `select` 속성입니다. 빈 배열을 hello 입력을 사용 하는 경우 hello 출력 빈 배열을 이기도 합니다.

|이름|필수|형식|설명|
|--------|------------|--------|---------------|
|from|예|배열|hello 소스 배열입니다.|
|선택|예|모두|hello 프로젝션 tooapply tooeach hello 소스 배열의 요소입니다.|

## <a name="terminate-action"></a>종료 작업

hello 종결 동작 hello 워크플로 실행을 모든 진행 중인 작업을 중단 하 고 남은 작업도 건너뜁니다의 실행을 중지 합니다. Tooterminate 상태와 함께 실행 하는 예를 들어 **실패**, 다음 코드 조각 hello를 사용할 수 있습니다.

```json
"HandleUnexpectedResponse" : {
    "type": "terminate",
    "inputs": {
        "runStatus" : "failed",
        "runError": {
            "code": "UnexpectedResponse",
            "message": "Received an unexpected response.",
        }
    }
}
```

> [!NOTE]
> 작업을 이미 완료 hello 영향을 받지 않는 작업을 종료 합니다.

|이름|필수|형식|설명|
|--------|------------|--------|---------------|
|runStatus|예|문자열|hello 대상 실행 상태입니다. **Failed** 또는 **Cancelled**입니다.|
|runError|아니요|Object|hello 오류 세부 정보입니다. 실행할 수만 **runStatus** 너무 설정**실패**합니다.|
|runError code|아니요|문자열|오류 코드를 실행 하는 번호입니다.|
|runError message|아니요|문자열|오류 메시지를 실행 하는 번호입니다.|

## <a name="compose-action"></a>작성 작업

hello 작성 작업을 사용 하면 임의의 개체를 생성할 수 있습니다. hello의 hello 출력 작성 작업은 해당 입력 평가 hello 결과입니다. 예를 들어 hello를 사용할 수 있습니다 여러 동작의 작업 toomerge 출력을 작성 합니다.

```json
"composeUserRecord" : {
    "type": "compose",
    "inputs": {
        "firstName": "@actions('getUser').firstName",
        "alias": "@actions('getUser').alias",
        "thumbnailLink": "@actions('lookupThumbnail').url"
        }
    }
}
```

> [!NOTE]
> hello **Compose** 동작 개체, 배열 및 기본적으로 XML 및 이진 같은 논리 앱에서 지 원하는 다른 형식을 포함 하 여 출력을 사용 하는 tooconstruct를 수 있습니다.

## <a name="table-action"></a>테이블 작업

hello `table` tooconvert에 항목 배열을 사용 하면 한 **CSV** 또는 **HTML** 테이블입니다.

@triggerBody()을 다음으로 가정합니다

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

Hello 동작으로 정의할 수 있도록

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

위의 hello 생성

<table><thead><tr><th>id</th><th>name</th></tr></thead><tbody><tr><td>0</td><td>사과</td></tr><tr><td>1</td><td>오렌지</td></tr></tbody></table>"

순서 toocustomize hello 표에 hello 열을 명시적으로 지정할 수 있습니다. 예:

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html",
        "columns": [{
          "header": "produce id",
          "value": "@item().id"
        },{
          "header": "description",
          "value": "@concat('fresh ', item().name)"
        }]
    }
}
```

위의 hello 생성

<table><thead><tr><th>ID를 생성합니다</th><th>설명</th></tr></thead><tbody><tr><td>0</td><td>신선한 사과</td></tr><tr><td>1</td><td>신선한 오렌지</td></tr></tbody></table>"

경우 hello `from` hello 출력은 빈 테이블, 속성 값은 빈 배열입니다.

|이름|필수|형식|설명|
|--------|------------|--------|---------------|
|from|예|배열|hello 소스 배열입니다.|
|format|예|문자열|형식으로 하거나 hello **CSV** 또는 **HTML**합니다.|
|열|아니요|배열|hello 열입니다. Hello 표의 toooverride hello 기본 형태를 허용합니다.|
|열 머리글|아니요|문자열|hello 열의 hello 헤더입니다.|
|열 값|예|문자열|hello 열의 hello 값입니다.|

## <a name="workflow-action"></a>워크플로 작업   

|이름|필수|형식|설명|  
|--------|------------|--------|---------------|  
|host id|예|문자열|hello toocall hello 워크플로의 리소스 ID입니다.|  
|host triggerName|예|문자열|tooinvoke hello 트리거가의 hello 이름입니다.|  
|쿼리|아니요|Object|Hello 쿼리 매개 변수 tooadd toohello URL을 나타냅니다. 예를 들어 `"queries" : { "api-version": "2015-02-01" }` 추가 `?api-version=2015-02-01` toohello URL입니다.|  
|headers|아니요|Object|각각의 toohello 요청이 발송 되 hello 머리글을 나타냅니다. 예를 들어 tooset hello 언어 및 요청에는 형식:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|body|아니요|Object|Toohello 끝점으로 전송 하는 hello 페이로드를 나타냅니다.|  
  
```json
"mynestedwf" : {
    "type" : "workflow",
    "inputs" : {
        "host" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName " : "mytrigger001"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        },
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
    }
```
  
액세스 검사 hello 워크플로에서 만든 \(hello 트리거 보다 구체적으로,\), toohello 워크플로 액세스 할 수 있음을 의미 합니다.  
  
hello hello에서 출력 `workflow` hello에 정의 된에 기반한 동작 `response` hello 자식 워크플로에서 동작입니다. 정의 되지 않은 경우 `response` 작업과 차례로 hello 출력 비어 있습니다.  

## <a name="function-action"></a>Function 작업   

|이름|필수|형식|설명|  
|--------|------------|--------|---------------|  
|function id|예|문자열|hello tooinvoke hello 함수의 리소스 ID입니다.|  
|메서드|아니요|문자열|HTTP 메서드 hello tooinvoke hello 함수를 사용 했습니다. 기본적으로 지정되지 않은 경우 `POST`입니다.|  
|쿼리|아니요|Object|Hello 쿼리 매개 변수 tooadd toohello URL을 나타냅니다. 예를 들어 `"queries" : { "api-version": "2015-02-01" }` 추가 `?api-version=2015-02-01` toohello URL입니다.|  
|headers|아니요|Object|각각의 toohello 요청이 발송 되 hello 머리글을 나타냅니다. 예를 들어: tooset hello 언어와 요청에는 유형을: `"headers" : { "Accept-Language": "en-us" }`합니다.|  
|body|아니요|Object|Toohello 끝점으로 전송 하는 hello 페이로드를 나타냅니다.|  

```json
"myfunc" : {
    "type" : "Function",
    "inputs" : {
        "function" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Web/sites/myfuncapp/functions/myfunc"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()"
        },
        "method" : "POST",
    "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
}
```

Hello 논리 앱을 저장할 때 참조 된 hello 함수에 대 한 몇 가지 검사 수행:
-   Toohave access toohello 함수가 필요합니다.
-   표준 HTTP 트리거 또는 일반 JSON 웹후크 트리거만 허용됩니다.
-   경로를 정의하지 않아야 합니다.
-   "함수" 및 "익명" 권한 부여 수준만 허용됩니다.

hello 트리거 URL 검색, 캐시 및 런타임에 사용 합니다. 따라서 캐시 hello URL을 무효화 하는 모든 작업을 런타임 시 hello 작업이 실패 합니다. 이 문제를 해결 toowork hello 논리 다시 응용 프로그램, 논리 앱 tooretrieve 되며 hello 트리거 URL을 다시 캐시를 저장 합니다.

## <a name="collection-actions-scopes-and-loops"></a>컬렉션 작업(범위 및 루프)

일부 작업 유형은 자체 내에 작업을 포함할 수 있습니다. 컬렉션 내에서 동작 참조 hello 컬렉션 외부에서 직접 참조할 수 있습니다. 범위에 `http`를 정의한 경우 `@body('http')`는 워크플로 어느 곳에서나 여전히 유효합니다. 컬렉션 내에서 동작의 기능은 `runAfter` 내에서 다른 작업에만 hello 동일한 컬렉션입니다.

## <a name="scope-action"></a>범위 작업

hello `scope` 동작을 수행 하면 논리적으로 워크플로에서 그룹 작업 합니다.

|이름|필수|형식|설명|  
|--------|------------|--------|---------------|  
|actions|예|Object|내부 작업 tooexecute hello 범위 내에서|

```json
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```

## <a name="foreach-action"></a>ForEach 작업

이 루프 작업은 배열을 반복하고 각 항목에 대해 내부 작업을 수행합니다. 기본적으로 hello foreach 루프 (20 번 실행 동시에 한 번에) 병렬로 실행합니다. Hello를 사용 하 여 실행 규칙을 설정할 수 있습니다 `operationOptions` 매개 변수입니다.

|이름|필수|형식|설명|  
|--------|------------|--------|---------------|  
|actions|예|Object|내부 작업 tooexecute hello 루프 내에서|
|foreach|예|string|통해 배열 tooiterate hello|
|operationOptions|no|string|동작에 대한 모든 작업 옵션입니다. 현재 까지만 지원 `sequential` tooexecute 반복 순서 대로) (기본 동작은 병렬)|

```json
"forEach_email": {
    "type": "foreach",
    "foreach": "@body('email_filter')",
    "actions": {
        "send_email": {
            "type": "ApiConnection",
            "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                }
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                }
            }
        }
    },
    "runAfter":{
        "email_filter": [ "Succeeded" ]
    }
}
```

## <a name="until-action"></a>Until 작업

이 반복 작업 조건 결과 tootrue 될 때까지 내부 작업을 실행 합니다.

|이름|필수|형식|설명|  
|--------|------------|--------|---------------|  
|actions|예|Object|내부 작업 tooexecute hello 루프 내에서|
|식|예|string|반복할 때마다 식 tooevaluate hello|
|limit|yes|Object|hello 반복-하나 이상의 제한에 대 한 hello도 정의 해야 합니다.|
|count|no|int|수행할 수 있는 반복 횟수 제한 toohello hello|
|시간 제한|no|string|반복 기간에 대 한 hello 시간이 초과 되었습니다.  ISO 8601 형식|


```json
 "Until_succeeded": {
    "actions": {
        "Http": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "expression": "@equals(outputs('Http')['statusCode', 200)",
    "limit": {
        "count": 1000,
        "timeout": "PT1H"
    },
    "runAfter": {},
    "type": "Until"
}
```

## <a name="conditions---if-action"></a>조건 - If 작업

hello `If` 조건을 평가 하 고 hello 식이 너무 계산 여부에 따라 분기 실행 동작을 수행 하면`true`합니다.

|이름|필수|형식|설명|  
|--------|------------|--------|---------------|  
|actions|예|Object|내부 작업 tooexecute 식이 너무 평가 되 면`true`|
|식|예|string|hello 식 tooevaluate|
|else|no|Object|내부 작업 tooexecute 식이 너무 평가 되 면`false`|
  
```json
"My_condition": {
    "actions": {
        "If_true": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "else": {
        "actions": {
            "if_false": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://myurl"
                },
                "runAfter": {},
                "type": "Http"
            }
        }
    },
    "expression": "@equals(triggerBody(), json(true))",
    "runAfter": {},
    "type": "If"
}
```  
  
hello 다음 표에서 사용 방법의 조건 식 동작:  
  
|JSON 값|결과|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|Tootrue를 평가 하는 모든 값이 조건 toopass를 하면 됩니다. 부울 식만 지원됩니다. 다른 tooconvert tooBoolean를 사용 하 여 함수 형식 `empty`, `equals`합니다.|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|비교 함수는 지원됩니다. 예: hello 여기 hello 동작 act1의 hello 출력 hello 임계값 보다 큰 경우에 실행 합니다.|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|논리 함수는 또한 지원 되는 toocreate 중첩 부울 식입니다. 이 경우 hello 동작 act1 hello 출력은 100 이하일 hello 임계값을 초과 하는 경우를 실행 합니다.|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|배열에 항목이 있으면 배열 함수 toocheck를 사용할 수 있습니다. 이 경우 hello 동작 hello 오류 배열이 비어 있는 경우를 실행 합니다.| 
|`"expression": "parameters('hasSpecialAction')"`|오류 - 조건에 @이 필요하므로 유효한 조건이 아닙니다.|  
  
Hello 조건으로 표시 되어 조건이 성공적으로 확인 되 면 `Succeeded`합니다. 어느 hello 내의 동작 `actions` 또는 `else` 개체 너무 평가`Succeeded` 실행 한 성공한 경우 `Failed` 실행 한 실패 한 경우 또는 `Skipped` 해당 분기는 실행 되지 않습니다.

## <a name="next-steps"></a>다음 단계

[워크플로 서비스 REST API](https://docs.microsoft.com/rest/api/logic/workflows)
