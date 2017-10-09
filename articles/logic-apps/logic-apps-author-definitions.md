---
title: "json-Azure 논리 앱 워크플로 aaaDefine | Microsoft Docs"
description: "어떻게 논리 앱에 대 한 json에서 toowrite 워크플로 정의"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 03/29/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 0d69d334ecee9c3e7f8684cfde68ef0e85280358
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a>JSON을 사용하여 논리 앱용 워크플로 정의 만들기

간단하고 선언적인 JSON 언어로 [Azure Logic Apps](logic-apps-what-are-logic-apps.md)에 대한 워크플로 정의를 만들 수 있습니다. 아직 하지 않는 경우 먼저 검토 [어떻게 toocreate 논리가 응용 프로그램 디자이너를 사용 하 여 첫 번째 논리 앱](logic-apps-create-a-logic-app.md)합니다. 참고: hello [hello 워크플로 정의 언어에 대 한 참조를 전체](http://aka.ms/logicappsdocs)합니다.

## <a name="repeat-steps-over-a-list"></a>목록에 대한 단계 반복

가 too10, 000 항목 최대 고 각 항목에 대 한 작업 수행을 hello를 사용 하 여 배열 통한 tooiterate [foreach 유형](logic-apps-loops-and-scopes.md)합니다.

## <a name="handle-failures-if-something-goes-wrong"></a>문제가 발생한 경우의 오류 처리

원하는 tooinclude 일반적으로 *재구성 단계* -를 실행 하는 일부 논리 *경우에* 하나 이상의 호출이 실패 합니다. 이 예제에서는 다양 한 위치에서 데이터를 가져옵니다 하지만 hello 호출이 실패 한 경우 원하는 tooPOST 메시지 어딘가에 나중에 해당 오류를 추적할 수 있습니다.  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "postToErrorMessageQueue": {
      "type": "ApiConnection",
      "inputs": "...",
      "runAfter": {
        "readData": [
          "Failed"
        ]
      }
    }
  },
  "outputs": {}
}
```

toospecify 하 `postToErrorMessageQueue` 에 실행 `readData` 가 `Failed`, hello를 사용 하 여 `runAfter` 속성에 가능한 값 목록은 toospecify 예를 들어 있도록 `runAfter` 수 `["Succeeded", "Failed"]`합니다.

마지막으로,이 예제에서는 이제 hello 오류를 처리 하기 때문에에서는 더 이상 표시로 실행 하는 hello `Failed`합니다. 이 예제에서이 오류를 처리 하기 위한 hello 단계를 추가 했습니다 있기 때문에 실행 하는 hello 포함 `Succeeded` 있지만 한 번 `Failed`합니다.

## <a name="execute-two-or-more-steps-in-parallel"></a>둘 이상의 단계를 병렬로 실행

toorun 병렬로 여러 동작 hello `runAfter` 속성이 런타임 시 동등한 형식 이어야 합니다. 

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "kind": "http",
      "type": "Request"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

이 예제에서는 모두 `branch1` 및 `branch2` 후 toorun 설정 `readData`합니다. 따라서 두 분기가 병렬로 실행됩니다. 양쪽 분기에 대 한 hello 타임 스탬프는 동일 합니다.

![병렬](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a>두 병렬 분기의 조인

항목 toohello를 추가 하 여 toorun 동시에 설정 된 두 가지 동작을 조인할 수 `runAfter` hello 이전 예제와 같이 합니다.

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-04-01-preview/workflowdefinition.json#",
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {}
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "join": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "branch1": [
          "Succeeded"
        ],
        "branch2": [
          "Succeeded"
        ]
      }
    }
  },
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "Http",
      "inputs": {
        "schema": {}
      }
    }
  },
  "contentVersion": "1.0.0.0",
  "outputs": {}
}
```

![병렬](media/logic-apps-author-definitions/join.png)

## <a name="map-list-items-tooa-different-configuration"></a>맵 목록 항목 tooa 다른 구성

그런 다음, hello 속성 값에 따라 tooget 다른 내용을 한다고 가정해 보겠습니다. 매개 변수로 값 toodestinations의 맵을 만들 수 있습니다.  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "specialCategories": {
      "defaultValue": [
        "science",
        "google",
        "microsoft",
        "robots",
        "NSA"
      ],
      "type": "Array"
    },
    "destinationMap": {
      "defaultValue": {
        "science": "http://www.nasa.gov",
        "microsoft": "https://www.microsoft.com/en-us/default.aspx",
        "google": "https://www.google.com",
        "robots": "https://en.wikipedia.org/wiki/Robot",
        "NSA": "https://www.nsa.gov/"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "http"
    }
  },
  "actions": {
    "getArticles": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "https://ajax.googleapis.com/ajax/services/feed/load?v=1.0&q=http://feeds.wired.com/wired/index"
      }
    },
    "forEachArticle": {
      "type": "foreach",
      "foreach": "@body('getArticles').responseData.feed.entries",
      "actions": {
        "ifGreater": {
          "type": "if",
          "expression": "@greater(length(intersection(item().categories, parameters('specialCategories'))), 0)",
          "actions": {
            "getSpecialPage": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('destinationMap')[first(intersection(item().categories, parameters('specialCategories')))]"
              }
            }
          }
        }
      },
      "runAfter": {
        "getArticles": [
          "Succeeded"
        ]
      }
    }
  }
}
```

이 경우 먼저 문서 목록을 가져옵니다. 매개 변수로 정의 된 hello 범주에 따라, 두 번째 단계 hello hello 콘텐츠를 가져오기 위한 hello URL 맵 toolook를 사용 합니다.

일부 시간 toonote: 

*   hello [ `intersection()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) 함수 hello 범주 hello 알려진 정의 된 범주 중 하 나와 일치 하는 지 여부를 확인 합니다.

*   Hello 범주 구했습니다 후 대괄호를 사용 하 여 hello 맵에서 hello 항목을 끌어올 수 있습니다.`parameters[...]`

## <a name="process-strings"></a>문자열 처리

다양 한 기능 toomanipulate 문자열을 사용할 수 있습니다. 예를 들어 toopass tooa 시스템 원하는 하지만 문자 인코딩에 대 한 적절 한 처리에 대 한 확신 하지 못해 문자열로 있다고 가정 합니다. 한 가지 방법은 toobase64이이 문자열을 인코딩합니다. 그러나 URL에서 이스케이프 tooavoid 하겠습니다 tooreplace 일부 문자입니다. 

또한 hello 처음 5 문자가 사용 되지 않는 있으므로 hello 순서 이름 부분 문자열이 선택 합니다.

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1",
        "orderer": "NAME=Contoso"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{replace(replace(base64(substring(parameters('order').orderer,5,sub(length(parameters('order').orderer), 5) )),'+','-') ,'/' ,'_' )}"
      }
    }
  },
  "outputs": {}
}
```

Toooutside 내에서 작동 합니다.

1. Hello 가져오기 [ `length()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) hello orderer 이름에 대 한 하므로 구했습니다 다시 hello 총 문자 수입니다.

2. 더 짧은 문자열을 원하므로 5를 뺍니다.

3. Hello, 내용이 [ `substring()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring)합니다. 인덱스에서 시작 `5` hello hello 문자열의 나머지 부분을 이동 합니다.

4. 이 부분 문자열 tooa 변환 [ `base64()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) 문자열입니다.

5. [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)모든 hello `+` 와 문자 `-` 문자입니다.

6. [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)모든 hello `/` 와 문자 `_` 문자입니다.

## <a name="work-with-date-times"></a>날짜 시간을 사용한 작업

날짜 시간 자연스럽 게 지원 하지 않는 데이터 원본의 toopull 데이터를 시도할 경우에 특히 유용할 수 있습니다 *트리거*합니다. 날짜 시간은 다양한 단계에 소요되는 시간을 파악하는 데에도 사용할 수 있습니다.

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{parameters('order').id}"
      }
    },
    "ifTimingWarning": {
      "type": "If",
      "expression": "@less(actions('order').startTime,addseconds(utcNow(),-1))",
      "actions": {
        "timingWarning": {
          "type": "Http",
          "inputs": {
            "method": "GET",
            "uri": "http://www.example.com/?recordLongOrderTime=@{parameters('order').id}&currentTime=@{utcNow('r')}"
          }
        }
      },
      "runAfter": {
        "order": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

이 예제에서는 hello 추출 `startTime` hello 이전 단계에서 합니다. 그런 다음 hello 현재 시간을 가져올 하 고 1 초를 뺍니다.

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

`minutes` 또는 `hours`와 같은 다른 시간 단위를 사용할 수 있습니다. 마지막으로 이 두 값을 비교할 수 있습니다. Hello 첫 번째 값이 2 초 이상 hello 두 번째 값 보다 작으면 경과한 hello 먼저 주문을 합니다.

tooformat 날짜, 문자열 포맷터를 사용할 수 있습니다. 예를 들어, tooget hello RFC1123 사용 하 여 [ `utcnow('r')` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow)합니다. 날짜 서식 지정에 대 한 toolearn 참조 [워크플로 정의 언어](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow)합니다.

## <a name="deployment-parameters-for-different-environments"></a>다른 환경에 대한 배포 매개 변수

일반적으로 배포 주기는 배포 환경, 스테이징 환경 및 프로덕션 환경으로 구성됩니다. 예를 들어 사용할 수 있습니다 이러한 환경 모두에서 동일한 정의 hello 하지만 서로 다른 데이터베이스를 사용 합니다. 마찬가지로, toouse 경우가 고가용성에 대 한 서로 다른 영역에서 동일한 정의 hello 하지만 각 논리 앱 인스턴스 tootalk toothat 지역의 데이터베이스입니다.
이 시나리오에서 매개 변수에서 다른 *런타임* 를 대신 사용 해야 hello `trigger()` hello 이전 예제와 같이 작동 합니다.

다음 예제와 같은 기본적인 정의로 시작할 수 있습니다.

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "uri": {
            "type": "string"
        }
    },
    "triggers": {
        "request": {
          "type": "request",
          "kind": "http"
        }
    },
    "actions": {
        "readData": {
            "type": "Http",
            "inputs": {
                "method": "GET",
                "uri": "@parameters('uri')"
            }
        }
    },
    "outputs": {}
}
```

실제 hello에 `PUT` hello 매개 변수를 제공할 수 있습니다 hello 논리 앱에 대 한 요청 `uri`합니다. 기본값을 더 이상 존재 하기 때문에이 매개 변수를 hello 논리가 응용 프로그램 페이로드에 필요 합니다.

```
{
    "properties": {},
        "definition": {
          // Use hello definition from above here
        },
        "parameters": {
            "connection": {
                "value": "https://my.connection.that.is.per.enviornment"
            }
        }
    },
    "location": "westus"
}
``` 

각 환경에 hello에 대 한 다른 값을 제공할 수 있습니다 `connection` 매개 변수입니다. 

만들기 및 논리 앱 관리에 대 한 옵션을 hello 모든 hello 참조 [REST API 문서](https://msdn.microsoft.com/library/azure/mt643787.aspx)합니다. 
