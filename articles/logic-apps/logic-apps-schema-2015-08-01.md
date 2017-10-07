---
title: "aaaSchema 업데이트 2015-1 년 8 월-미리 보기-Azure 논리 앱 | Microsoft Docs"
description: "스키마 버전 2015-08-01-preview로 Azure Logic Apps에 대한 JSON 정의 만들기"
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 0d03a4d4-e8a8-4c81-aed5-bfd2a28c7f0c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 05/31/2016
ms.author: LADocs; stepsic
ms.openlocfilehash: 950cd18a27aa1859c4f0b6116de3fb8699d746c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a>Azure Logic Apps에 대한 스키마 업데이트 - 2015년 8월 1일 미리 보기

이 새로운 스키마 및 API 버전 Azure 논리 앱에 대 한 논리 앱을 추가 하는 주요 향상 기능이 포함 되어 신뢰할 수 있는 쉽고 toouse:

*   hello **APIApp** 동작 형식이 새 업데이트 tooa [ **APIConnection** ](#api-connections) 동작 유형입니다.
*   **반복** 너무 이름이[**Foreach**](#foreach)합니다.
*   hello [ **HTTP 수신기** API 앱](#http-listener) 는 더 이상 필요 합니다.
*   하위 워크플로 호출에 [새 스키마](#child-workflows)를 사용합니다.

<a name="api-connections"></a>
## <a name="move-tooapi-connections"></a>이동 tooAPI 연결

가장 크게 변화 된 hello 더 이상 있다고 toodeploy API 앱 Azure 구독에 Api를 사용할 수 있도록입니다. 여기 가지 hello Api를 사용할 수 있습니다.

* 관리되는 API
* 사용자 지정 Web API

이러한 각 방식은 관리 및 호스팅 모델이 다르므로 약간 다르게 처리됩니다. 이 모델의 장점 중 하나는 더 이상 제한 하는 Azure 리소스 그룹에 배포 되는 tooresources 합니다. 

### <a name="managed-apis"></a>관리되는 API

Microsoft는 사용자를 대신해서 Office 365, Salesforce, Twitter, FTP 등의 몇 가지 API를 관리합니다. 관리되는 일부 API를 Bing Translate처럼 있는 그대로 사용할 수도 있지만 구성이 필요한 경우도 있습니다. 이 구성을 *연결*이라고 합니다.

예를 들어 Office 365를 사용하는 경우 Office 365 로그인 토큰을 포함하는 연결을 만들어야 합니다. 이 토큰이 안전 하 게 저장 되 고 논리 앱에서 항상 hello Office 365 API를 호출할 수 있도록 새로 고쳐집니다. 또는 tooconnect tooyour SQL 또는 FTP 서버를 사용 하려는 경우 hello 연결 문자열이 연결을 만들어야 합니다. 

이 정의에서 이러한 작업을 `APIConnection`이라고 합니다. Office 365 toosend 전자 메일을 호출 하는 연결의 예는 다음과 같습니다.

```
{
    "actions": {
        "Send_Email": {
            "type": "ApiConnection",
            "inputs": {
                "host": {
                    "api": {
                        "runtimeUrl": "https://msmanaged-na.azure-apim.net/apim/office365"
                    },
                    "connection": {
                        "name": "@parameters('$connections')['shared_office365']['connectionId']"
                    }
                },
                "method": "post",
                "body": {
                    "Subject": "Reminder",
                    "Body": "Don't forget!",
                    "To": "me@contoso.com"
                },
                "path": "/Mail"
            }
        }
    }
}
```

hello `host` 개체는 고유한 tooAPI 연결 되며 행 부분이 포함 된 입력 부분: `api` 및 `connection`합니다.

hello `api` 에 hello 런타임 API를 관리 하의 URL 호스트 됩니다. 관리 되는 사용 가능한 모든 hello Api를 호출 하 여 볼 수 있습니다 `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`합니다.

Hello API 수 또는 되지 않았을 수 있는 API를 사용 하면 *연결 매개 변수* 정의 합니다. Hello API 표시 되지 않으면 없습니다 *연결* 가 필요 합니다. Hello API가 연결을 만들어야 합니다. hello 만든 연결에 사용자가 선택한 hello 이름이 있습니다. Hello 이름을 hello에 다음 참조 `connection` hello 내부 개체 `host` 개체입니다. toocreate 호출 리소스 그룹에 연결:

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

다음 본문 hello로:

```
{
  "properties": {
    "api": {
      "id": "/subscriptions/{subid}/providers/Microsoft.Web/managedApis/azureblob"
    },
    "parameterValues": {
        "accountName": "{hello name of hello storage account -- hello set of parameters is different for each API}"
    }
  },
  "location": "{Logic app's location}"
}
```

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a>Azure Resource Manager 템플릿에서 관리 API 배포

대화형 로그인이 필요하지 않다면 Azure Resource Manager 템플릿에서 전체 응용 프로그램을 만들 수 있습니다.
로그인이 필요한 경우 hello Azure 리소스 관리자 템플릿을 사용 하 여 모든 항목을 설정할 수 있지만 toovisit hello 포털 tooauthorize hello 연결 해야 합니다. 

```
    "resources": [{
        "apiVersion": "2015-08-01-preview",
        "name": "azureblob",
        "type": "Microsoft.Web/connections",
        "location": "[resourceGroup().location]",
        "properties": {
            "api": {
                "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
            },
            "parameterValues": {
                "accountName": "[parameters('storageAccountName')]",
                "accessKey": "[parameters('storageAccountKey')]"
            }
        }
    }, {
        "type": "Microsoft.Logic/workflows",
        "apiVersion": "2015-08-01-preview",
        "name": "[parameters('logicAppName')]",
        "location": "[resourceGroup().location]",
        "dependsOn": ["[resourceId('Microsoft.Web/connections', 'azureblob')]"
        ],
        "properties": {
            "sku": {
                "name": "[parameters('sku')]",
                "plan": {
                    "id": "[concat(resourceGroup().id, '/providers/Microsoft.Web/serverfarms/',parameters('svcPlanName'))]"
                }
            },
            "definition": {
                "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2015-08-01-preview/workflowdefinition.json#",
                "actions": {
                    "Create_file": {
                        "type": "apiconnection",
                        "inputs": {
                            "host": {
                                "api": {
                                    "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/azureblob"
                                },
                                "connection": {
                                    "name": "@parameters('$connections')['azureblob']['connectionId']"
                                }
                            },
                            "method": "post",
                            "queries": {
                                "folderPath": "[concat('/', parameters('containerName'))]",
                                "name": "helloworld.txt"
                            },
                            "body": "@decodeDataUri('data:, Hello+world!')",
                            "path": "/datasets/default/files"
                        },
                        "conditions": []
                    }
                },
                "contentVersion": "1.0.0.0",
                "outputs": {},
                "parameters": {
                    "$connections": {
                        "defaultValue": {},
                        "type": "Object"
                    }
                },
                "triggers": {
                    "recurrence": {
                        "type": "Recurrence",
                        "recurrence": {
                            "frequency": "Day",
                            "interval": 1
                        }
                    }
                }
            },
            "parameters": {
                "$connections": {
                    "value": {
                        "azureblob": {
                            "connectionId": "[concat(resourceGroup().id,'/providers/Microsoft.Web/connections/azureblob')]",
                            "connectionName": "azureblob",
                            "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
                        }

                    }
                }
            }
        }
    }]
```

Hello 연결은 정당한 리소스 리소스 그룹에 거주 하는이 예에서 볼 수 있습니다. 구독에 관리 되는 hello Api 사용 가능한 tooyou를 참조합니다.

### <a name="your-custom-web-apis"></a>사용자 지정 Web API

Microsoft 관리 텍스처 사용자 고유의 Api를 사용 하는 경우 사용 하 여 hello 기본 제공 **HTTP** 동작 toocall 해당 합니다. 이상적인 환경을 위해서는 API에 대한 Swagger 끝점을 노출해야 합니다. 이 끝점 hello 논리가 응용 프로그램 디자이너 toorender hello 입력 있으며 특정 API에 대 한 출력 합니다. Swagger, 없이 hello 디자이너 불투명 JSON 개체로 hello 입 / 출력을 표시할만 수 있습니다.

다음 예제에서는 표시 된 hello 새은 `metadata.apiDefinitionUrl` 속성:

```
{
   "actions": {
        "mycustomAPI": {
            "type": "http",
            "metadata": {
              "apiDefinitionUrl": "https://mysite.azurewebsites.net/api/apidef/"  
            },
            "inputs": {
                "uri": "https://mysite.azurewebsites.net/api/getsomedata",
                "method": "GET"
            }
        }
    }
}
```

Azure 앱 서비스 웹 API를 호스트 하는 경우 웹 API hello 디자이너에서 사용할 수 있는 작업의 hello 목록에 자동으로 나타납니다. 그렇지 않으면 직접 toopaste hello URL에 있을 수 있습니다. hello Swagger 끝점은 Swagger 지 원하는 모든 메서드를 사용 하 여 자체 hello API 보안을 유지할 수 있지만 인증 되지 않은 toobe hello 논리가 응용 프로그램 디자이너에서에서 사용할 수 있어야 합니다.

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a>2015-08-01-preview로 배포된 API 앱 호출

API 앱을 이전에 배포한 경우에 hello로 hello 응용 프로그램을 호출할 수 있습니다 **HTTP** 동작 합니다.

예를 들어, Dropbox toolist 파일을 사용 하는 경우 프로그램 **2014-12-01-미리 보기** 스키마 버전 정의 다음과 같이 있을 수 있습니다.

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2014-12-01-preview/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token": {
            "defaultValue": "eyJ0eX...wCn90",
            "type": "String",
            "metadata": {
                "token": {
                    "name": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token"
                }
            }
        }
    },
    "actions": {
        "dropboxconnector": {
            "type": "ApiApp",
            "inputs": {
                "apiVersion": "2015-01-14",
                "host": {
                    "id": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector",
                    "gateway": "https://avdemo.azurewebsites.net"
                },
                "operation": "ListFiles",
                "parameters": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

Hello 논리 앱 정의의 매개 변수 섹션 hello 그대로 유지 하는 동안 다음이 예제 처럼 hello 동일한 HTTP 동작을 구성할 수 있습니다.

```
{
    "actions": {
        "dropboxconnector": {
            "type": "Http",
            "metadata": {
              "apiDefinitionUrl": "https://avdemo.azurewebsites.net/api/service/apidef/dropboxconnector/?api-version=2015-01-14&format=swagger-2.0-standard"  
            },
            "inputs": {
                "uri": "https://avdemo.azurewebsites.net/api/service/invoke/dropboxconnector/ListFiles?api-version=2015-01-14",
                "method": "POST",
                "body": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

이러한 속성을 하나씩 연습합니다.

| 작업 속성 | 설명 |
| --- | --- |
| `type` |`Http`다음 위치 대신`APIapp` |
| `metadata.apiDefinitionUrl` |toouse hello 논리가 응용 프로그램 디자이너에서에서이 작업에서 생성 된 hello 메타 데이터 끝점을 포함:`{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard` |
| `inputs.uri` |생성된 위치: `{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14` |
| `inputs.method` |항상 `POST` |
| `inputs.body` |동일한 toohello API 응용 프로그램 매개 변수 |
| `inputs.authentication` |동일한 toohello API 앱 인증 |

이 방법은 모든 API App 작업에 대해 작동합니다. 하지만 이러한 이전 API Apps는 더 이상 지원되지 않습니다. 따라서 옮겨야의 hello tooone 다른 이전 두 옵션을 관리 되는 API 또는 사용자 지정 웹 API를 호스트 합니다.

<a name="foreach"></a>
## <a name="renamed-repeat-tooforeach"></a>'Repeat' too'foreach 이름이 변경 '

많은 고객 의견을 수신 했습니다. 이전 스키마 버전 hello에 대 한 하 **반복** 했습니다 및는 캡처 적절 하지 않은 **반복** 가 실제로 foreach 루프입니다. 이름을 결과적으로, `repeat` 너무`foreach`합니다. 예를 들어 이전에는 다음과 같이 작성해야 했습니다.

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "repeat": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{repeatItem()}"
            }
        }
    }
}
```

이제 다음과 같이 작성할 수 있습니다.

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "foreach": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{item()}"
            }
        }
    }
}
```

함수 hello `@repeatItem()` 가 이전에 사용한 tooreference hello에 대 한 현재 항목 반복 되 합니다. 이 함수는 이제 너무 단순화`@item()`합니다. 

### <a name="reference-outputs-from-foreach"></a>'foreach'의 참조 출력

출력 hello 간소화를 위한 `foreach` 동작 이라는 개체에 래핑되지 않은 `repeatItems`합니다. Hello 이전 hello에서 출력 하는 동안 `repeat` 예제가:

```
{
    "repeatItems": [
        {
            "name": "pingBing",
            "inputs": {
                "uri": "https://www.bing.com/search?q=0",
                "method": "GET"
            },
            "outputs": {
                "headers": { },
                "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
            }
            "status": "Succeeded"
        }
    ]
}
```

그렇지만 이제 이 출력은 다음과 같습니다.

```
[
    {
        "name": "pingBing",
        "inputs": {
            "uri": "https://www.bing.com/search?q=0",
            "method": "GET"
        },
        "outputs": {
            "headers": { },
            "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
        }
        "status": "Succeeded"
    }
]
```

이전에 tooget toohello 본문 이러한 출력 참조 시 hello 동작:

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "repeat": "@outputs('pingBing').repeatItems",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@repeatItem().outputs.body"
            }
        }
    }
}
```

이제 대신 다음을 수행하면 됩니다.

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "foreach": "@outputs('pingBing')",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@item().outputs.body"
            }
        }
    }
}
```

이러한 변경 내용으로 함수 hello `@repeatItem()`, `@repeatBody()`, 및 `@repeatOutputs()` 제거 됩니다.

<a name="http-listener"></a>
## <a name="native-http-listener"></a>네이티브 HTTP 수신기

hello HTTP 수신기 기능이 이제에서 빌드됩니다. 따라서 HTTP 수신기 API 앱 toodeploy 더 이상 필요 합니다. 참조 [방법에 대 한 전체 세부 정보를 hello toomake 논리 앱 끝점 호출 가능 여기](../logic-apps/logic-apps-http-endpoint.md)합니다. 

이러한 변경 내용으로 hello 제거 `@accessKeys()` hello로 교체 하는 함수를 `@listCallbackURL()` 필요한 경우 hello 끝점을 가져오기 위한 함수입니다. 또한 이제 논리 앱에서 트리거를 하나 이상 정의해야 합니다. 너무 하려는 경우`/run` 워크플로 hello, 이러한 트리거 중 하나가 있어야: `manual`, `apiConnectionWebhook`, 또는 `httpWebhook`합니다.

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a>하위 워크플로 호출

이전에 자식 워크플로 호출 toohello 워크플로 가져오는 hello 액세스 토큰 및 붙여넣기 hello 토큰 toocall 원하는 hello 논리 앱 정의에 자식 워크플로 이동 해야 합니다. Hello 새 스키마와 함께 hello 논리 앱 엔진에 대 한 런타임 시 SAS를 자동으로 생성 하지 않는 한 너무 붙여 있습니다 비밀이 hello 정의에 자식 워크플로 hello 합니다. 다음은 예제입니다.

```
"mynestedwf": {
    "type": "workflow",
    "inputs": {
        "host": {
            "id": "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName": "myendpointtrigger"
        },
        "queries": {
            "extrafield": "specialValue"
        },
        "headers": {
            "x-ms-date": "@utcnow()",
            "Content-type": "application/json"
        },
        "body": {
            "contentFieldOne": "value100",
            "anotherField": 10.001
        }
    },
    "conditions": []
}
```

두 번째 개선 하 게 조정할 수 hello 자식 워크플로에 대 한 모든 권한을 toohello 들어오는 요청입니다. 즉, hello에 매개 변수를 전달할 수 *쿼리* 섹션 및 hello *헤더* 개체와 완벽 하 게 정의할 수 있는 hello 전체 본문입니다.

마지막으로, toohello 하위 워크플로 필요한 변경 내용이 있습니다. 이전에 자식 워크플로 직접 호출할 수 있습니다, 동안 이제 끝점을 정의 해야는 트리거 부모 toocall hello에 대 한 hello 워크플로에서 합니다. 일반적으로 트리거를 추가 `manual` 입력 한 다음 해당 트리거를 사용 하 여 hello 부모 정의에 있습니다. 참고 hello `host` 속성은 구체적으로 `triggerName` 호출 하는 트리거는 항상 지정 해야 하기 때문에 있습니다.

## <a name="other-changes"></a>기타 변경 내용

### <a name="new-queries-property"></a>새 'queries' 속성

이제 모든 작업 유형에서 `queries`라는 새 입력을 지원합니다. 이 입력 tooassemble hello 문자열을 직접 필요가 아닌는 구조화 된 개체 일 수 있습니다.

### <a name="renamed-parse-function-toojson"></a>'Parse ()' 함수 too'json() 이름이 변경 '

이름을 각각 hello 하므로 더 많은 콘텐츠를 곧 형식을 추가 하 고 `parse()` 함수 에서도`json()`합니다.

## <a name="coming-soon-enterprise-integration-apis"></a>서비스 예정: 엔터프라이즈 통합 API

관리 되는 버전의 hello AS2 유사한 엔터프라이즈 통합 Api 아직 아직 합니다. 한편, hello HTTP 동작을 통해 배포 된 기존 BizTalk Api를 사용할 수 있습니다. 자세한 내용은 hello에 "이미 배포 된 API 앱 사용"을 참조 [통합 로드맵](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/)합니다. 
