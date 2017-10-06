---
title: "Azure 활동 로그 경고에 대 한 webhook aaaCall | Microsoft Docs"
description: "사용자 지정 작업에 대 한 활동 로그 이벤트 tooother 서비스를 라우팅하십시오. 예를 들어 SMS를 전송하거나, 버그를 기록하거나, 채팅/메시징 서비스를 통해 팀에 알릴 수 있습니다."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 64d333d1-7f37-4a00-9d16-dda6e69a113b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: johnkem
ms.openlocfilehash: 9017ff3e5165857ec7084a8f07f4123552e55f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="call-a-webhook-on-azure-activity-log-alerts"></a>Azure 활동 로그 경고에 대한 webhook 호출
또한 Webhook 허용 tooroute Azure 사후 처리 또는 사용자 지정 작업에 대 한 알림 tooother 시스템 경고 합니다. webhook을 사용 하 여 경고 tooroute에 것 tooservices SMS를 전송 하는 버그를 로그, 채팅/메시징 서비스를 통해 팀에 게 알림 또는 여러 다른 동작을 수행 합니다. 이 문서에서는 webhook toobe tooset 때 Azure 활동 로그 경고 발생을 호출 하는 방법을 설명 합니다. 또한 다음과 같은 hello HTTP POST tooa webhook에 대 한 어떤 hello 페이로드를 보여 줍니다. Hello 설정 및 Azure 메트릭 경고에 대 한 스키마에 대 한 내용은 [이 페이지가 대신 표시](insights-webhooks-alerts.md)합니다. 활성화 될 때 경고 toosend 전자 메일 활동 로그를 설정할 수 있습니다.

> [!NOTE]
> 이 기능은 현재 미리 보기에서 이며 향후 hello 한 시점에서 제거 됩니다.
>
>

Hello를 사용 하 여 활동 로그 경고를 설정할 수 있습니다 [Azure PowerShell Cmdlet](insights-powershell-samples.md#create-metric-alerts), [플랫폼 간 CLI](insights-cli-samples.md#work-with-alerts), 또는 [Azure 모니터 REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx)합니다. 현재 hello Azure 포털을 사용 하 여 하나를 설정할 수 없습니다.

## <a name="authenticating-hello-webhook"></a>Hello webhook 인증
hello webhook 이러한 방법 중 하나를 사용 하 여 인증할 수 있습니다.

1. **권한 부여 토큰 기반** -hello webhook 토큰 ID와 함께 URI 예를 들어 저장`https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`
2. **기본 권한 부여** -예를 들어 사용자 이름 및 암호를 사용 하 여 저장 된 URI는 webhook hello`https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`

## <a name="payload-schema"></a>페이로드 스키마
POST 작업 hello hello JSON 페이로드를 수행 하는 모든 활동 로그 기반 경고에 대 한 스키마를 포함 합니다. 이 스키마는 비슷한 toohello 하나의 메트릭을 기반 경고에 사용 합니다.

```
{
        "status": "Activated",
        "context": {
                "resourceProviderName": "Microsoft.Web",
                "event": {
                        "$type": "Microsoft.WindowsAzure.Management.Monitoring.Automation.Notifications.GenericNotifications.Datacontracts.InstanceEventContext, Microsoft.WindowsAzure.Management.Mon.Automation",
                        "authorization": {
                                "action": "Microsoft.Web/sites/start/action",
                                "scope": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest"
                        },
                        "eventDataId": "327caaca-08d7-41b1-86d8-27d0a7adb92d",
                        "category": "Administrative",
                        "caller": "myname@mycompany.com",
                        "httpRequest": {
                                "clientRequestId": "f58cead8-c9ed-43af-8710-55e64def208d",
                                "clientIpAddress": "104.43.166.155",
                                "method": "POST"
                        },
                        "status": "Succeeded",
                        "subStatus": "OK",
                        "level": "Informational",
                        "correlationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "eventDescription": "",
                        "operationName": "Microsoft.Web/sites/start/action",
                        "operationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "properties": {
                                "$type": "Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage",
                                "statusCode": "OK",
                                "serviceRequestId": "f7716681-496a-4f5c-8d14-d564bcf54714"
                        }
                },
                "timestamp": "Friday, March 11, 2016 9:13:23 PM",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/alertonevent2",
                "name": "alertonevent2",
                "description": "test alert on event start",
                "conditionType": "Event",
                "subscriptionId": "s1",
                "resourceId": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest",
                "resourceGroupName": "rg1"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```

| 요소 이름 | 설명 |
| --- | --- |
| status |메트릭 경고에 사용됩니다. 항상 너무 "활성화 된" 작업 로그 경고에 대 한 설정 됩니다. |
| context |Hello 이벤트의 컨텍스트입니다. |
| resourceProviderName |hello 리소스 공급자의 hello 리소스를 저하 됩니다. |
| conditionType |항상 "Event"입니다. |
| name |Hello 경고 규칙의 이름입니다. |
| id |Hello 경고의 리소스 ID입니다. |
| 설명 |Hello 경고를 만드는 동안 설정 된 대로 경고 설명 합니다. |
| subscriptionId |Azure 구독 ID입니다. |
| timestamp |hello 이벤트가 hello hello 요청을 처리 하는 Azure 서비스에서 생성 된 시간입니다. |
| resourceId |Hello의 리소스 ID 리소스를 저하 됩니다. |
| resourceGroupName |리소스의 영향을 hello에 대 한 hello 리소스 그룹의 이름 |
| properties |설정 `<Key, Value>` 쌍 (예: `Dictionary<String, String>`) hello 이벤트에 대 한 세부 정보를 포함 하는 합니다. |
| event |Hello 이벤트에 대 한 메타 데이터를 포함 하는 요소입니다. |
| 권한 부여 |hello hello 이벤트의 RBAC 속성입니다. 일반적으로 여기에 hello "action", "role" 및 hello "범위입니다." |
| 카테고리 |Hello 이벤트의 범주입니다. 지원되는 값으로 Administrative, Alert, Security, ServiceHealth, Recommendation이 있습니다. |
| caller |Hello 작업, UPN 클레임 또는 SPN 클레임 가용성에 따라 수행한 hello 사용자의 전자 메일 주소입니다. 특정 시스템 호출의 경우 null일 수 있습니다. |
| CorrelationId |일반적으로 문자열 형식의 GUID. 상관 관계 Id와 함께 이벤트 속해 toohello 같은 더 큰 작업 하 고 일반적으로 correlationId를 공유 합니다. |
| eventDescription |Hello 이벤트의 정적 텍스트 설명입니다. |
| eventDataId |Hello 이벤트에 대 한 고유 식별자입니다. |
| eventSource |이름에 해당 생성 된 hello 이벤트 인프라 또는 Azure 서비스 hello 합니다. |
| httpRequest |일반적으로 "clientRequestId" hello, "clientIpAddress" 및 "method" 같습니다 (HTTP 메서드 PUT 예:). |
| level |Hello 다음 값 중 하나: "Critical", "Error", "Warning", "Informational" 및 "Verbose"입니다. |
| operationId |일반적으로 GUID toosingle 작업에 해당 하는 hello 이벤트 간에 공유 합니다. |
| operationName |Hello 작업의 이름입니다. |
| properties |Hello 이벤트의 속성입니다. |
| status |문자열입니다. Hello 작업의 상태입니다. 일반적인 값으로 "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved"가 포함됩니다. |
| subStatus |일반적으로 hello 해당 REST 호출의 hello HTTP 상태 코드를 포함합니다. 하위 상태를 설명하는 다른 문자열을 포함할 수도 있습니다. 일반적인 하위 상태 값으로 OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504)이 있습니다. |

## <a name="next-steps"></a>다음 단계
* [활동 로그 hello에 대 한 자세한 정보](monitoring-overview-activity-logs.md)
* [Azure 경고에 대한 Azure Automation 스크립트 실행 (Runbooks)](http://go.microsoft.com/fwlink/?LinkId=627081)
* [Azure 경고에서 논리 앱 toosend Twilio 통해 SMS를 사용 하 여](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)합니다. 이 예제에서는 메트릭 경고에 대 한 않으며 활동 로그 경고와 수정 된 toowork 수입니다.
* [논리 앱 toosend Azure 경고에서 Slack 메시지를 사용 하 여](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)합니다. 이 예제에서는 메트릭 경고에 대 한 않으며 활동 로그 경고와 수정 된 toowork 수입니다.
* [논리 앱 toosend Azure 경고에서 메시지 tooan Azure 큐를 사용 하 여](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)합니다. 이 예제에서는 메트릭 경고에 대 한 않으며 활동 로그 경고와 수정 된 toowork 수입니다.
