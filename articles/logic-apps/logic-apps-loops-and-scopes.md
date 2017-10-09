---
title: "aaaCreate 루프를 실행 하 고, 범위를 지정 하거나 워크플로-Azure 논리 앱의 데이터를 debatch | Microsoft Docs"
description: "데이터를 범위에 그룹 작업을 통해 루프 tooiterate 만들거나 Azure 논리 앱에서 더 많은 워크플로 데이터 toostart debatch 합니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 75b52eeb-23a7-47dd-a42f-1351c6dfebdc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: e612ec2e83541f028916a07bf12c44e7b1f57ad1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-loops-scopes-and-debatching"></a>논리 앱 루프, 범위 및 분할
  
논리 앱 다양 한 방법으로 toowork 배열, 컬렉션, 일괄 처리 및 워크플로 내에서 루프를 제공합니다.
  
## <a name="foreach-loop-and-arrays"></a>ForEach 루프 및 배열
  
논리 앱 tooloop 데이터 집합에 대해 있으며 각 항목에 대 한 작업을 수행 합니다.  이 hello를 통해 가능 `foreach` 동작 합니다.  Hello 디자이너에서 tooadd를 지정할 수 있습니다는 for each 루프입니다.  Hello 배열 tooiterate 통해 원하는 선택한 후 작업을 추가 시작할 수 있습니다.  현재 제한 tooonly foreach 루프 당 하나의 작업만 있지만 주 들어오는 hello에이 제한 사항은 변경 합니다.  한 번 hello 루프 내 toospecify hello 배열의 각 값에 발생 하는 것을 시작할 수 있습니다.

코드 보기를 사용하는 경우 아래와 같이 각 루프에 지정할 수 있습니다.  다음은 'microsoft.com'을 포함하는 각 전자 메일 주소에 대해 전자 메일을 보내는 각 루프의 예입니다.

``` json
{
    "email_filter": {
        "type": "query",
        "inputs": {
            "from": "@triggerBody()['emails']",
            "where": "@contains(item()['email'], 'microsoft.com')"
        }
    },
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
                },
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                },
                }
            }
        },
        "runAfter":{
            "email_filter": [ "Succeeded" ]
        }
    }
}
```
  
  A `foreach` 동작 배열 too5, 000 행을 반복할 수 있습니다.  각 반복은 기본적으로 병렬로 실행 됩니다.  

### <a name="sequential-foreach-loops"></a>순차적 ForEach 루프

foreach 루프 tooexecute 순차적으로 hello tooenable `Sequential` 작업 옵션을 추가 해야 합니다.

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a>Until 루프
  
  조건이 충족될 때까지 작업 또는 일련의 작업을 수행할 수 있습니다.  hello이 대 한 가장 일반적인 시나리오 호출 하는 끝점에 대 한 원하는 hello 응답에 도달할 때까지 합니다.  Hello 디자이너에서 tooadd를 지정할 수 있습니다는 until 루프입니다.  Hello 루프 내의 액션을 추가한 후 있습니다 수 hello 종료 조건을 설정으로 hello 루프 제한 합니다.  루프 주기 사이에는 1분의 지연이 발생합니다.
  
  코드 보기를 사용하는 경우 아래와 같이 Until 루프를 지정할 수 있습니다.  이것이 hello 응답 본문에 hello 값 'Completed' 때까지 HTTP 끝점을 호출 하는 예입니다.  다음과 같은 경우에 완료됩니다. 
  
  * HTTP 응답의 상태가 'Completed'임
  * 1시간 동안 시도됨
  * 100번 반복됨
  
  ``` json
  {
      "until_successful":{
        "type": "until",
        "expression": "@equals(actions('http')['status'], 'Completed')",
        "limit": {
            "count": 100,
            "timeout": "PT1H"
        },
        "actions": {
            "create_resource": {
                "type": "http",
                "inputs": {
                    "url": "http://provisionRseource.com",
                    "body": {
                        "resourceId": "@triggerBody()"
                    }
                }
            }
        }
      }
  }
  ```
  
## <a name="spliton-and-debatching"></a>SplitOn 및 분리

경우에 따라 트리거 toodebatch 원하고 항목당 워크플로 시작 하는 항목의 배열을 나타날 수 있습니다.  Hello를 통해 이렇게 `spliton` 명령입니다.  기본적으로 트리거 swagger가 배열에 해당하는 페이로드를 지정하는 경우 `spliton`이 추가되고 항목당 실행이 시작됩니다.  SplitOn는 tooa 트리거만 추가할 수 있습니다.  정의 코드 보기에서 수동으로 구성하거나 재정의할 수 있습니다.  현재 SplitOn too5, 000 항목을 배열 debatch 수 있습니다.  사용할 수 없는 `spliton` 도 hello 동기 응답 패턴을 구현 합니다.  호출 하는 모든 워크플로에 `response` 또한 동작 너무`spliton` 비동기적으로 실행 되 고 즉시 보낼 `202 Accepted` 응답 합니다.  

다음 예제는 hello로 코드 뷰에서 SplitOn은 지정할 수 있습니다.  이렇게 하면 항목의 배열이 수신되고 각 행에서 분리됩니다.

```
{
    "myDebatchTrigger": {
        "type": "Http",
        "inputs": {
            "url": "http://getNewCustomers",
        },
        "recurrence": {
            "frequencey": "Second",
            "interval": 15
        },
        "spliton": "@triggerBody()['rows']"
    }
}
```

## <a name="scopes"></a>범위

것이 가능한 toogroup 일련의 동작 범위를 사용 하 여 결합 합니다.  이 기능은 예외 처리를 구현하는 데 특히 유용합니다.  Hello 디자이너에서 새 범위를 추가할 수 있으며 내부 작업을 추가 하기 시작 키를 누릅니다.  Hello 다음과 같은 코드 보기에서 범위를 정의할 수 있습니다.


```
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