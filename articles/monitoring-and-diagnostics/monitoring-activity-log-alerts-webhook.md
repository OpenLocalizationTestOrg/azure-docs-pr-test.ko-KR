---
title: "활동 로그 경고에 사용 된 aaaUnderstand hello webhook 스키마 | Microsoft Docs"
description: "Hello는 활동 로그 경고가 활성화 되는 경우 tooa webhook URL에 게시 하는 JSON의 hello 스키마에 알아봅니다."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: 75562e0589222d3e392ea73eacfd7414a422d115
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a>Azure 활동 로그 경고에 대한 웹후크
작업 그룹 hello 정의의 일부로 webhook 끝점 tooreceive 활동 로그 경고 알림을 구성할 수 있습니다. Webhook을 사용자 지정 또는 후 처리 작업에 대 한 이러한 알림을 tooother 시스템을 라우팅할 수 있습니다. 이 문서에서는 다음과 같은 hello HTTP POST tooa webhook에 대 한 어떤 hello 페이로드를 보여 줍니다.

활동 로그 경고에 대 한 자세한 내용은 참조 방법을 너무[Azure 활동 로그 알림을 만들](monitoring-activity-log-alerts.md)합니다.

동작 그룹에 대 한 자세한 내용은 참조 방법을 너무[동작 그룹을 만들](monitoring-action-groups.md)합니다.

## <a name="authenticate-hello-webhook"></a>Hello webhook 인증
선택적으로 hello webhook 인증에 대 한 토큰 기반 인증을 사용할 수 있습니다. 토큰 ID와 함께 URI 예를 들어 저장 하는 webhook hello `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`합니다.

## <a name="payload-schema"></a>페이로드 스키마
hello POST 작업에에서 포함 된 hello JSON 페이로드 hello 페이로드 data.context.activityLog.eventSource 필드에 따라 다릅니다.

###<a name="common"></a>일반
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "channels": "Operation",
                "correlationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "eventSource": "Administrative",
                "eventTimestamp": "2017-03-29T15:43:08.0019532+00:00",
                "eventDataId": "8195a56a-85de-4663-943e-1a2bf401ad94",
                "level": "Informational",
                "operationName": "Microsoft.Insights/actionGroups/write",
                "operationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "status": "Started",
                "subStatus": "",
                "subscriptionId": "52c65f65-0518-4d37-9719-7dbbfc68c57a",
                "submissionTimestamp": "2017-03-29T15:43:20.3863637+00:00",
                ...
            }
        },
        "properties": {}
    }
}
```
###<a name="administrative"></a>관리
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "authorization": {
                    "action": "Microsoft.Insights/actionGroups/write",
                    "scope": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions"
                },
                "claims": "{...}",
                "caller": "me@contoso.com",
                "description": "",
                "httpRequest": "{...}",
                "resourceId": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions",
                "resourceGroupName": "CONTOSO-TEST",
                "resourceProviderName": "Microsoft.Insights",
                "resourceType": "Microsoft.Insights/actionGroups"
            }
        },
        "properties": {}
    }
}

```
###<a name="servicehealth"></a>ServiceHealth
```json
{
    "schemaId": "unknown",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "properties": {
                    "title": "...",
                    "service": "...",
                    "region": "...",
                    "communication": "...",
                    "incidentType": "Incident",
                    "trackingId": "...",
                    "groupId": "...",
                    "impactStartTime": "3/29/2017 3:43:21 PM",
                    "impactMitigationTime": "3/29/2017 3:43:21 PM",
                    "eventCreationTime": "3/29/2017 3:43:21 PM",
                    "impactedServices": "[{...}]",
                    "defaultLanguageTitle": "...",
                    "defaultLanguageContent": "...",
                    "stage": "Active",
                    "communicationId": "...",
                    "version": "0.1"
                }
            }
        },
        "properties": {}
    }
}
```

서비스 상태 알림 활동 로그 경고에 대한 특정 스키마 세부 정보는 [서비스 상태 알림](monitoring-service-notifications.md)을 참조하세요.

다른 모든 활동 로그 경고 세부 정보를 특정 스키마를 참조 하십시오. [hello Azure 활동 로그 간략하게](monitoring-overview-activity-logs.md)합니다.

| 요소 이름 | 설명 |
| --- | --- |
| status |메트릭 경고에 사용됩니다. 항상 너무 "활성화 된" 작업 로그 경고에 대 한 설정 됩니다. |
| context |Hello 이벤트의 컨텍스트입니다. |
| resourceProviderName |hello 리소스 공급자의 hello 리소스를 저하 됩니다. |
| conditionType |항상 "Event"입니다. |
| name |Hello 경고 규칙의 이름입니다. |
| id |Hello 경고의 리소스 ID입니다. |
| 설명 |경고 설명 hello 경고를 만들 때 설정 합니다. |
| subscriptionId |Azure 구독 ID입니다. |
| timestamp |hello 이벤트가 hello hello 요청을 처리 하는 Azure 서비스에서 생성 된 시간입니다. |
| resourceId |Hello의 리소스 ID 리소스를 저하 됩니다. |
| resourceGroupName |Hello에 대 한 hello 리소스 그룹의 이름을 리소스를 저하 됩니다. |
| properties |설정 `<Key, Value>` 쌍 (즉, `Dictionary<String, String>`) hello 이벤트에 대 한 세부 정보를 포함 하는 합니다. |
| event |Hello 이벤트에 대 한 메타 데이터가 포함 된 요소입니다. |
| 권한 부여 |hello hello 이벤트의 역할 기반 액세스 제어 속성입니다. 이러한 속성에는 일반적으로 hello 작업과 hello 역할 hello 범위 포함 됩니다. |
| 카테고리 |Hello 이벤트의 범주입니다. 지원되는 값으로 Administrative, Alert, Security, ServiceHealth, Recommendation이 있습니다. |
| caller |Hello 작업, UPN 클레임 또는 SPN 클레임 가용성에 따라 수행한 hello 사용자의 전자 메일 주소입니다. 특정 시스템 호출의 경우 null일 수 있습니다. |
| CorrelationId |일반적으로 문자열 형식의 GUID. 상관 관계 Id와 함께 이벤트 속해 toohello 같은 더 큰 작업 하 고 일반적으로 correlationId를 공유 합니다. |
| eventDescription |Hello 이벤트의 정적 텍스트 설명입니다. |
| eventDataId |Hello 이벤트에 대 한 고유 식별자입니다. |
| eventSource |이름에 해당 생성 된 hello 이벤트 인프라 또는 Azure 서비스 hello 합니다. |
| httpRequest |hello 요청 일반적으로 hello clientRequestId, 포함 clientIpAddress, HTTP 메서드 (예를 들어 PUT). |
| level |Hello 다음 값 중 하나: 중요, 오류, 경고, 정보, 및 자세한 정보 표시 합니다. |
| operationId |일반적으로 GUID toosingle 작업에 해당 하는 hello 이벤트 간에 공유 합니다. |
| operationName |Hello 작업의 이름입니다. |
| properties |Hello 이벤트의 속성입니다. |
| status |문자열입니다. Hello 작업의 상태입니다. 일반적인 값으로 Started, In Progress, Succeeded, Failed, Active 및 Resolved가 포함됩니다. |
| subStatus |일반적으로 hello 해당 REST 호출의 hello HTTP 상태 코드를 포함합니다. 하위 상태를 설명하는 다른 문자열을 포함할 수도 있습니다. 일반적인 하위 상태 값으로 OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503) 및 Gateway Timeout (HTTP Status Code: 504)이 있습니다. |

## <a name="next-steps"></a>다음 단계
* [Hello 활동 로그에 대 한 자세한](monitoring-overview-activity-logs.md)합니다.
* [Azure 경고에 대한 Azure Automation 스크립트(Runbook)를 실행하세요](http://go.microsoft.com/fwlink/?LinkId=627081).
* [Azure 경고에서 논리 앱 toosend Twilio 통해 SMS를 사용 하 여](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)합니다. 이 예제는 메트릭 경고에 대 한 활동 로그 경고와 수정 된 toowork 수 없지만 합니다.
* [논리 앱 toosend Azure 경고에서 Slack 메시지를 사용 하 여](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)합니다. 이 예제는 메트릭 경고에 대 한 활동 로그 경고와 수정 된 toowork 수 없지만 합니다.
* [Azure 경고에서 큐에 메시지 tooan Azure 논리 앱 toosend를 사용 하 여](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)합니다. 이 예제는 메트릭 경고에 대 한 활동 로그 경고와 수정 된 toowork 수 없지만 합니다.
