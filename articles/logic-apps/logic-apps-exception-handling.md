---
title: "aaaError & 예외 처리-Azure 논리 앱 | Microsoft Docs"
description: "Azure Logic Apps에서 오류 및 예외 처리 패턴"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: e50ab2f2-1fdc-4d2a-be40-995a6cc5a0d4
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 326a252310c8dfb154e583f91c9421675e448d1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a>Azure Logic Apps에서 예외 및 오류 처리

패턴 toohelp 수 있도록 사용자 통합은 강력 하 고 오류에 대 한 복원 력이 및 azure 논리 앱 풍부한 도구를 제공 합니다. 모든 통합 아키텍처 있는지 tooappropriately 핸들 가동 중지 시간 삼기 hello challenge로 인해 발생 하며 또는 종속 시스템의 문제입니다. 오류 처리 논리 앱 사용 하면 제공 하는 첫 번째 클래스 환경을 hello 워크플로에서 tooact 예외 및 오류에 필요한 도구입니다.

## <a name="retry-policies"></a>재시도 정책

다시 시도 정책은 hello 예외 및 오류 처리의 가장 기본적인 유형입니다. 초기 요청 시간 초과 또는 실패 한 경우 (429는 발생 하는 모든 요청 또는 5xx 응답),이 정책은 hello 작업을 다시 시도해 야 하는지 여부를 정의 합니다. 기본적으로 모든 작업은 20초 간격에 걸쳐 추가로 4회 재시도합니다. 따라서 hello 첫 번째 요청 수신 하는 경우는 `500 Internal Server Error` 시도 안녕 요청 및 응답으로 hello 워크플로 엔진 20 초 동안 일시 중지 합니다. Hello 워크플로에서 계속 하는 경우 모든 다시 시도한 후 hello 응답은 여전히 예외 또는 오류, 및 표시로 작업 상태를 hello `Failed`합니다.

Hello에 다시 시도 정책을 구성할 수 있습니다 **입력** 특정 작업에 대 한 합니다. 예를 들어 구성할 수 있습니다 다시 시도 정책 tootry 4 회까지 1 시간 간격에 걸쳐 있습니다. 입력 속성에 대한 자세한 내용은 [워크플로 작업 및 트리거][retryPolicyMSDN]를 참조하세요.

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

HTTP 동작 tooretry 4 번 려 하 고 각 시도 사이 10 분 정도 기다린 다음 정의 hello를 사용 합니다.

```json
"HTTP": 
{
    "inputs": {
        "method": "GET",
        "uri": "http://myAPIendpoint/api/action",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT10M",
            "count": 4
        }
    },
    "runAfter": {},
    "type": "Http"
}
```

지원 되는 구문에 대 한 자세한 내용은 참조 hello [워크플로 동작 및 트리거에 다시 시도 정책 섹션][retryPolicyMSDN]합니다.

## <a name="catch-failures-with-hello-runafter-property"></a>Hello RunAfter 속성으로 오류를 catch 합니다.

각 논리 앱 작업 선언 워크플로에 hello 단계 순서와 같은 hello 작업이 시작 되기 전에 작업을 마쳐야 합니다. Hello 작업 정의에이 순서 라고 hello `runAfter` 속성입니다. 이 속성은 hello 작업을 실행 하는 작업 및 작업 상태를 설명 하는 개체입니다. 기본적으로 hello 논리가 응용 프로그램 디자이너를 통해 추가 된 모든 작업은 설정 너무`runAfter` hello 이전 단계 경우 hello 이전 단계 `Succeeded`합니다. 그러나 이전 작업 해야 하는 경우이 값 toofire 동작을 사용자 지정할 수 `Failed`, `Skipped`, 또는 이러한 값의 가능한 집합입니다. 특정 작업 후 항목 tooa 서비스 버스 항목 지정 tooadd 려 `Insert_Row` 실패 하면 다음 hello를 사용할 수 있습니다 `runAfter` 구성:

```json
"Send_message": {
    "inputs": {
        "body": {
            "ContentData": "@{encodeBase64(body('Insert_Row'))}",
            "ContentType": "{ \"content-type\" : \"application/json\" }"
        },
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/servicebus"
            },
            "connection": {
                "name": "@parameters('$connections')['servicebus']['connectionId']"
            }
        },
        "method": "post",
        "path": "/@{encodeURIComponent('failures')}/messages"
    },
    "runAfter": {
        "Insert_Row": [
            "Failed"
        ]
    }
}
```

공지 hello `runAfter` 속성이 toofire 경우 hello `Insert_Row` 동작은 `Failed`합니다. toorun hello 동작 hello 작업 상태 이면 `Succeeded`, `Failed`, 또는 `Skipped`,이 구문을 사용 합니다.

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> 이전 작업이 실패한 후 실행되는 작업이 성공적으로 완료되면 `Succeeded`로 표시됩니다. 이 동작은 실행을 의미 hello 하면 워크플로에서 성공적으로 모든 catch 실패 하는 경우 자체로 표시 되어 `Succeeded`합니다.

## <a name="scopes-and-results-tooevaluate-actions"></a>범위 및 결과 tooevaluate 작업

비슷한 toohow 개별 작업 후에 실행할 수, 또한 함께 그룹화 할 수 작업 내는 [범위](../logic-apps/logic-apps-loops-and-scopes.md), 작업의 논리적 그룹으로 역할입니다. 범위는 범위의 hello 상태에서 집계 평가 수행 하기 위한 및 논리 앱 작업을 구성 하는 데 유용 합니다. 자체 hello 범위는 범위에서 작업을 모두 완료 한 후 상태를 수신 합니다. hello 범위 상태는 hello로 결정 됩니다. 동일한 기준으로 실행 합니다. 실행 분기의 마지막 작업에서는 hello 경우 `Failed` 또는 `Aborted`, hello 상태는 `Failed`합니다.

사용할 수 있습니다 toofire hello 범위 내에서 수행 된 모든 오류에 대 한 특정 작업을 `runAfter` 표시 된 범위를 갖는 `Failed`합니다. 경우 *모든* hello 범위에는 동작이 실패 하는 경우 범위를 사용 하면 실패 한 후에 실행 되도록 만들 단일 작업 toocatch 오류가 발생 했습니다.

### <a name="getting-hello-context-of-failures-with-results"></a>결과와 관련 된 오류 컨텍스트 hello 가져오기

범위에서 오류를 catch 하는 것은 유용, 있지만 컨텍스트 toohelp 실패 하는 작업을 정확 하 게 이해 하 고 오류 또는 반환 된 상태 코드도 할 수 있습니다. hello `@result()` 워크플로 함수는 범위에 있는 모든 작업의 결과 hello에 대 한 컨텍스트를 제공 합니다.

`@result()`단일 매개 변수, 범위 이름 하며 해당 범위 내에서 모든 hello 작업 결과의 배열을 반환 합니다. 이러한 작업 개체에 hello로 특성 동일 hello 포함 `@actions()` 작업 시작 시간, 작업 종료 시간, 작업 상태, 작업 입력, 작업 상관관계 Id 및 동작을 포함 하 여 개체를 출력 합니다. 범위 내에서 실패 한 작업 toosend 컨텍스트를 쉽게 연결할 수는 `@result()` 작동 한 `runAfter`합니다.

tooexecute 동작 *각* 범위에서 동작 하는 `Failed`, 필터 hello 배열을 결과 tooactions 배포 하지 못한, 페어링할 수 있는 `@result()` 와  **[필터 배열](../connectors/connectors-native-query.md)**  동작 및  **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**  루프입니다. Hello 필터링 된 결과 배열 고 hello를 사용 하 여 각 오류에 대 한 작업을 수행할 수 있습니다 **ForEach** 루프입니다. Hello 범위 내에서 실패 한 작업의 응답 본문 hello 함께 HTTP POST 요청을 전송 하는 자세한 설명이 나옵니다 예로 `My_Scope`합니다.

```json
"Filter_array": {
    "inputs": {
        "from": "@result('My_Scope')",
        "where": "@equals(item()['status'], 'Failed')"
    },
    "runAfter": {
        "My_Scope": [
            "Failed"
        ]
    },
    "type": "Query"
},
"For_each": {
    "actions": {
        "Log_Exception": {
            "inputs": {
                "body": "@item()['outputs']['body']",
                "method": "POST",
                "headers": {
                    "x-failed-action-name": "@item()['name']",
                    "x-failed-tracking-id": "@item()['clientTrackingId']"
                },
                "uri": "http://requestb.in/"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "foreach": "@body('Filter_array')",
    "runAfter": {
        "Filter_array": [
            "Succeeded"
        ]
    },
    "type": "Foreach"
}
```

어떤 일이 생기 자세한 연습 toodescribe 다음과 같습니다.

1. 내의 모든 작업의 tooget hello 결과 `My_Scope`, hello **필터 배열** 작업 필터 `@result('My_Scope')`합니다.

2. 에 대 한 조건 hello **필터 배열** 는 임의의 `@result()` 너무 상태를 가진 항목을`Failed`합니다. 이 상태 필터에서 모든 작업 결과 사용 하 여 hello 배열 `My_Scope` tooan 배열 된 작업 결과 실패 했습니다.

3. 수행는 **각** hello에 대 한 작업 **필터링 배열** 를 출력 합니다. 이 단계는 이전에 필터링된 실패한 작업 결과 *각각에 대해* 작업을 수행합니다.

    Hello 범위에 단일 작업에 실패 한 경우 hello hello에서 동작 `foreach` 한 번만 실행 합니다. 
    많은 실패한 작업에서 오류당 하나의 작업이 발생합니다.

4. Hello에 HTTP POST를 보낼 `foreach` 응답 본문 항목 또는 `@item()['outputs']['body']`합니다. hello `@result()` 항목 셰이프는 동일 hello로 hello `@actions()` , 모양 지정 및 구문 분석할 수 있는 hello 동일한 방식으로 합니다.

5. Hello 실패 한 동작 이름 가진 두 개의 사용자 지정 헤더 포함 `@item()['name']` hello 실패 추적 ID는 실행된 된 클라이언트 및 `@item()['clientTrackingId']`합니다.

참조용으로 다음은 예제는 단일 `@result()` hello를 보여 주는 항목 `name`, `body`, 및 `clientTrackingId` hello 이전 예제에서 구문 분석 되는 속성입니다. `foreach`의 외부에서 `@result()`가 이러한 개체의 배열을 반환합니다.

```json
{
    "name": "Example_Action_That_Failed",
    "inputs": {
        "uri": "https://myfailedaction.azurewebsites.net",
        "method": "POST"
    },
    "outputs": {
        "statusCode": 404,
        "headers": {
            "Date": "Thu, 11 Aug 2016 03:18:18 GMT",
            "Server": "Microsoft-IIS/8.0",
            "X-Powered-By": "ASP.NET",
            "Content-Length": "68",
            "Content-Type": "application/json"
        },
        "body": {
            "code": "ResourceNotFound",
            "message": "/docs/folder-name/resource-name does not exist"
        }
    },
    "startTime": "2016-08-11T03:18:19.7755341Z",
    "endTime": "2016-08-11T03:18:20.2598835Z",
    "trackingId": "bdd82e28-ba2c-4160-a700-e3a8f1a38e22",
    "clientTrackingId": "08587307213861835591296330354",
    "code": "NotFound",
    "status": "Failed"
}
```

tooperform 다른 예외 처리 패턴 앞에 표시 된 hello 식을 사용할 수 있습니다. 작업 실패의 전체 필터링 된 배열을 hello를 허용 하는 hello 다루지 처리 예외 하나 tooexecute을 선택 하 고 hello 제거 수 `foreach`합니다. Hello에서 다른 유용한 속성을 포함할 수도 있습니다 `@result()` 앞에 표시 된 응답입니다.

## <a name="azure-diagnostics-and-telemetry"></a>Azure 진단 및 원격 분석

hello 이전 패턴은 훌륭한 방법 toohandle 오류와 예외는 실행 내에서 하지만 또한 식별 하 고 자체적으로 실행 하는 hello와 무관 tooerrors 응답할 수 있습니다. 
[Azure 진단](../logic-apps/logic-apps-monitor-your-logic-apps.md) 모든 워크플로 (실행 및 작업에 대 한 모든 상태를 포함 하 여) 이벤트 tooan Azure 저장소 계정 또는 Azure 이벤트 허브는 간단한 방법을 toosend를 제공 합니다. tooevaluate 실행 상태, hello 로그 및 메트릭, 모니터링 하거나 원하는 모니터링 도구에 게시할 수 있습니다. 한 가지 가능한 옵션은 toostream에 Azure 이벤트 허브를 통해 모든 hello 이벤트 [스트림 분석](https://azure.microsoft.com/services/stream-analytics/)합니다. 스트림 분석에서 작성할 수 있습니다 모든 비정상, 평균 또는 오류 오프 라이브 쿼리 hello에서 진단 로그. 스트림 분석에는 큐, 항목, SQL, Azure Cosmos DB 및 Power BI와 같은 데이터 원본 tooother 출력할 쉽게 수 있습니다.

## <a name="next-steps"></a>다음 단계

* [고객이 Azure Logic Apps의 오류 처리를 빌드하는 방법을 참조하세요.](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [논리 앱 예제 및 시나리오 더 찾아보기](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Toocreate 논리 앱에 대 한 배포를 자동화 하는 방법을 알아봅니다](../logic-apps/logic-apps-create-deploy-template.md)
* [Visual Studio에서 논리 앱 빌드 및 배포](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
