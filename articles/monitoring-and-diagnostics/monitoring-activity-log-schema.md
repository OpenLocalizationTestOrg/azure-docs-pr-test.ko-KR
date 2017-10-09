---
title: "활동 로그 이벤트 스키마 aaaAzure | Microsoft Docs"
description: "Hello 활동 로그에 내보낸 데이터에 대 한 hello 이벤트 스키마 이해"
author: johnkemnetz
manager: robb
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: johnkem
ms.openlocfilehash: dfece949a20a4d9b4e8a4d488c1c34842d87d586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-activity-log-event-schema"></a>Azure 활동 로그 이벤트 스키마
hello **Azure 활동 로그** Azure에서 발생 한 모든 구독 수준 이벤트에 대 한 정보를 제공 하는 로그입니다. 이 문서에서는 데이터의 범주별 hello 이벤트 스키마를 설명 합니다.

## <a name="administrative"></a>관리
이 범주에 모든 hello 레코드 만들기, 업데이트, 삭제 및 작업 작업이 리소스 관리자를 통해 수행 합니다. 이 범주에 표시 되는 이벤트 유형을 포함 하는 hello의 예로 "가상 컴퓨터 만들기" 및 "삭제" 네트워크 보안 그룹 사용자가 수행한 동작 또는 리소스 관리자를 사용 하 여 응용 프로그램은 특정 리소스 종류에 대 한 작업으로 모델링 됩니다. Hello 작업 유형이 hello 시작과 성공의 hello 레코드를 삭제 또는 동작을 작성 하거나 hello 관리 범주에 해당 작업의 실패 기록 됩니다. 구독에 변경 내용을 toorole 기반 액세스 제어를 관리 범주 hello 포함 됩니다.

### <a name="sample-event"></a>샘플 이벤트
```json
{
  "authorization": {
    "action": "microsoft.support/supporttickets/write",
    "role": "Subscription Admin",
    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841"
  },
  "caller": "admin@contoso.com",
  "channels": "Operation",
  "claims": {
    "aud": "https://management.core.windows.net/",
    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
    "iat": "1421876371",
    "nbf": "1421876371",
    "exp": "1421880271",
    "ver": "1.0",
    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
    "puid": "20030000801A118C",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
    "name": "John Smith",
    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
    "appidacr": "2",
    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
    "http://schemas.microsoft.com/claims/authnclassreference": "1"
  },
  "correlationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "description": "",
  "eventDataId": "44ade6b4-3813-45e6-ae27-7420a95fa2f8",
  "eventName": {
    "value": "EndRequest",
    "localizedValue": "End request"
  },
  "httpRequest": {
    "clientRequestId": "27003b25-91d3-418f-8eb1-29e537dcb249",
    "clientIpAddress": "192.168.35.115",
    "method": "PUT"
  },
  "id": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841/events/44ade6b4-3813-45e6-ae27-7420a95fa2f8/ticks/635574752669792776",
  "level": "Informational",
  "resourceGroupName": "MSSupportGroup",
  "resourceProviderName": {
    "value": "microsoft.support",
    "localizedValue": "microsoft.support"
  },
  "resourceUri": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
  "operationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "operationName": {
    "value": "microsoft.support/supporttickets/write",
    "localizedValue": "microsoft.support/supporttickets/write"
  },
  "properties": {
    "statusCode": "Created"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": "Created",
    "localizedValue": "Created (HTTP Status Code: 201)"
  },
  "eventTimestamp": "2015-01-21T22:14:26.9792776Z",
  "submissionTimestamp": "2015-01-21T22:14:39.9936304Z",
  "subscriptionId": "s1"
}
```

### <a name="property-descriptions"></a>속성 설명
| 요소 이름 | 설명 |
| --- | --- |
| 권한 부여 |Hello 이벤트의 RBAC 속성의 blob입니다. 일반적으로 hello "action", "role" 및 "범위" 속성이 포함 됩니다. |
| caller |Hello 작업, UPN 클레임 또는 SPN 클레임 가용성에 따라 수행한 hello 사용자의 전자 메일 주소입니다. |
| channels |Hello 다음 값 중 하나: "Admin", "작업이" |
| claims |Active Directory tooauthenticate hello 사용자 또는 응용 프로그램 tooperform에서 리소스 관리자에서이 작업을 사용 하는 hello JWT 토큰입니다. |
| CorrelationId |일반적으로 hello 문자열 형식의 GUID입니다. CorrelationId를 공유 하는 이벤트가 속하는지 toohello 같은 uber 작업 합니다. |
| 설명 |이벤트의 정적 텍스트 설명입니다. |
| eventDataId |이벤트의 고유 식별자입니다. |
| httpRequest |Http 요청 번호를 설명 하는 blob입니다. 일반적으로 "clientRequestId" hello, "clientIpAddress" 및 "방법" (HTTP 메서드입니다 같습니다. HTTP 메서드) 포함. |
| level |Hello 이벤트의 수준입니다. Hello 다음 값 중 하나: "Critical", "Error", "Warning", "Informational" 및 "Verbose" |
| resourceGroupName |Hello에 대 한 hello 리소스 그룹의 이름을 리소스를 저하 됩니다. |
| resourceProviderName |리소스의 영향을 hello에 대 한 hello 리소스 공급자의 이름 |
| resourceId |Hello의 리소스 id 리소스를 저하 됩니다. |
| operationId |Hello 해당 하는 이벤트 tooa 단일 작업 간에 공유 하는 GUID입니다. |
| operationName |Hello 작업의 이름입니다. |
| properties |설정 `<Key, Value>` hello 이벤트의 hello 세부 정보를 설명 하는 쌍 (즉, 사전). |
| status |Hello 연산의 hello 상태를 설명 하는 문자열입니다. 일반적인 값: Started, In Progress, Succeeded, Failed, Active, Resolved. |
| subStatus |Hello hello 해당 REST 호출의 HTTP 상태 코드는 일반적으로 있지만 이러한 공통 값과 같은 하위 상태를 설명 하는 다른 문자열을 포함할 수도 있습니다: 확인 (HTTP 상태 코드: 200) 작성 (HTTP 상태 코드: 201) 허용 되는, (HTTP 상태 코드: 202), 아니요 콘텐츠 (HTTP 상태 코드: 204), 잘못 된 요청 (HTTP 상태 코드: 400), 찾을 수 없음 (HTTP 상태 코드: 404), 충돌 (HTTP 상태 코드: 409), 내부 서버 오류 (HTTP 상태 코드: 500), 서비스 사용할 수 없음 (HTTP 상태 코드: 503), 게이트웨이 시간 초과 (HTTP 상태 코드: 504). |
| eventTimestamp |Hello Azure 서비스 처리 hello에서 hello 이벤트가 생성 된 시점의 타임 스탬프는 해당 하는 hello 이벤트를 요청 합니다. |
| submissionTimestamp |Hello 이벤트를 쿼리 하기 위해 사용할 수 있게 하는 경우 타임 스탬프입니다. |
| subscriptionId |Azure 구독 ID입니다. |

## <a name="service-health"></a>서비스 상태
이 범주에는 Azure에서 발생 한 모든 서비스 상태 문제의 hello 레코드에 포함 합니다. Hello 유형의이 범주에 표시 되는 이벤트의 예로 "미국 동부에서 SQL Azure 가동 중지 시간이 발생 합니다." 서비스 상태 이벤트를 가져오는 다섯 가지 종류의: 필요한 작업, 복구 지원, 인시던트, 유지 관리, 정보 또는 보안을 hello 이벤트에 의해 영향을 받게 hello 구독에는 리소스를 사용할 경우에 표시 하 고 있습니다.

### <a name="sample-event"></a>샘플 이벤트
```json
{
  "channels": "Admin",
  "correlationId": "c550176b-8f52-4380-bdc5-36c1b59d3a44",
  "description": "Active: Network Infrastructure - UK South",
  "eventDataId": "c5bc4514-6642-2be3-453e-c6a67841b073",
  "eventName": {
      "value": null
  },
  "category": {
      "value": "ServiceHealth",
      "localizedValue": "Service Health"
  },
  "eventTimestamp": "2017-07-20T23:30:14.8022297Z",
  "id": "/subscriptions/mySubscriptionID/events/c5bc4514-6642-2be3-453e-c6a67841b073/ticks/636361902148022297",
  "level": "Warning",
  "operationName": {
      "value": "Microsoft.ServiceHealth/incident/action",
      "localizedValue": "Microsoft.ServiceHealth/incident/action"
  },
  "resourceProviderName": {
      "value": null
  },
  "resourceType": {
      "value": null,
      "localizedValue": ""
  },
  "resourceId": "/subscriptions/mySubscriptionID",
  "status": {
      "value": "Active",
      "localizedValue": "Active"
  },
  "subStatus": {
      "value": null
  },
  "submissionTimestamp": "2017-07-20T23:30:34.7431946Z",
  "subscriptionId": "mySubscriptionID",
  "properties": {
    "title": "Network Infrastructure - UK South",
    "service": "Service Fabric",
    "region": "UK South",
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a>속성 설명
요소 이름 | 설명
-------- | -----------
channels | Hello 다음 값 중 하나: "Admin", "작업이"
CorrelationId | 일반적으로 hello 문자열 형식의 GUID입니다. 같은 uber 작업 대개 공유 toohello 속하는 이벤트는 같은 correlationId hello 합니다.
설명 | Hello 이벤트의 설명입니다.
eventDataId | hello 이벤트의 고유 식별자입니다.
eventName | hello 제목 hello 이벤트입니다.
level | Hello 이벤트의 수준입니다. Hello 다음 값 중 하나: "Critical", "Error", "Warning", "Informational" 및 "Verbose"
resourceProviderName | 리소스의 영향을 hello에 대 한 hello 리소스 공급자의 이름. 알 수 없는 경우 null로 설정됩니다.
resourceType| hello hello의 리소스 유형의 리소스를 저하 됩니다. 알 수 없는 경우 null로 설정됩니다.
subStatus | 서비스 상태 이벤트의 경우 대개 null입니다.
eventTimestamp | Hello 로그 이벤트를 생성 되었고 toohello 활동 로그를 전송 하는 경우 타임 스탬프입니다.
submissionTimestamp |   Hello 활동 로그에서에서 제공 된 hello 이벤트 타임 스탬프입니다.
subscriptionId | 이 이벤트가 기록 되는 Azure 구독을 hello 합니다.
status | Hello 연산의 hello 상태를 설명 하는 문자열입니다. 일반적인 값으로는 Active, Resolved 등이 있습니다.
operationName | Hello 작업의 이름입니다. 보통 Microsoft.ServiceHealth/incident/action입니다.
카테고리 | "ServiceHealth"
resourceId | Hello의 리소스 id의 리소스에 영향을 알 수 있는 경우. 확인되지 않은 경우에는 구독 ID가 제공됩니다.
Properties.title | 이 통신에 대 한 hello 지역화 된 제목입니다. 영어는 hello 기본 언어입니다.
Properties.communication | hello는 hello 통신할 때 HTML 태그의 세부 정보를 지역화 합니다. 영어는 hello 기본값입니다.
Properties.incidentType | 가능한 값: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security
Properties.trackingId | 이 이벤트와 연결 된 hello 인시던트를 식별 합니다. 이 toocorrelate hello 이벤트 관련된 tooan 인시던트에 사용 합니다.
Properties.impactedServices | Hello 서비스 및 hello 인시던트의 영향을 미치는 영역을 설명 하는 이스케이프 된 JSON blob입니다. 각각 ServiceName과 ImpactedRegions 목록을 포함하는 서비스 목록으로, 각 ImpactedRegions에는 RegionName이 포함됩니다.
Properties.defaultLanguageTitle | 영어로 hello 통신
Properties.defaultLanguageContent | html 태그 또는 일반 텍스트 영어로 hello 통신
Properties.stage | AssistedRecovery, ActionRequired, Information, Incident, Security에 대해 가능한 값: Active, Resolved. Maintenance에 대해 가능한 값: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete
Properties.communicationId | 이 이벤트는 연결 된 hello 통신 합니다.

## <a name="alert"></a>경고
이 범주는 hello 레코드의 Azure 경고의 모든 정품 인증을 포함합니다. Hello 유형의이 범주에 표시 되는 이벤트의 예로 "CPU (%)에서 myVM은 되었으며 80 hello에 대 한 지난 5 분" 다수의 Azure 시스템에서 경고 개념이 사용됩니다. 일종의 규칙을 정의하여 조건이 해당 규칙과 일치하면 알림을 수신할 수 있습니다. 될 때마다 지원 되는 Azure 경고 유형 '활성화,' 또는 hello 조건이 충족된 toogenerate 알림을, hello 정품 인증에 대 한 기록을 hello 활동 로그의 toothis 범주 푸시됩니다.

### <a name="sample-event"></a>샘플 이벤트

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in hello last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
  "eventDataId": "149d4baf-53dc-4cf4-9e29-17de37405cd9",
  "eventName": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "category": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle/events/149d4baf-53dc-4cf4-9e29-17de37405cd9/ticks/636362258535221920",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "Microsoft.ClassicCompute",
    "localizedValue": "Microsoft.ClassicCompute"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle",
  "resourceType": {
    "value": "Microsoft.ClassicCompute/domainNames/slots/roles",
    "localizedValue": "Microsoft.ClassicCompute/domainNames/slots/roles"
  },
  "operationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "operationName": {
    "value": "Microsoft.Insights/AlertRules/Resolved/Action",
    "localizedValue": "Microsoft.Insights/AlertRules/Resolved/Action"
  },
  "properties": {
    "RuleUri": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert",
    "RuleName": "myalert",
    "RuleDescription": "",
    "Threshold": "100000",
    "WindowSizeInMinutes": "5",
    "Aggregation": "Average",
    "Operator": "LessThan",
    "MetricName": "Disk read",
    "MetricUnit": "Count"
  },
  "status": {
    "value": "Resolved",
    "localizedValue": "Resolved"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T09:24:13.522192Z",
  "submissionTimestamp": "2017-07-21T09:24:15.6578651Z",
  "subscriptionId": "mySubscriptionID"
}
```

### <a name="property-descriptions"></a>속성 설명
| 요소 이름 | 설명 |
| --- | --- |
| caller | Always Microsoft.Insights/alertRules |
| channels | 항상 "Admin, Operation"입니다. |
| claims | Hello SPN (서비스 사용자 이름) 또는 리소스에 대 한 형식의 hello 경고 엔진이 사용 하 여 JSON blob입니다. |
| CorrelationId | Hello 문자열 형식의 GUID입니다. |
| 설명 |Hello 경고 이벤트의 정적 텍스트 설명입니다. |
| eventDataId |Hello 경고 이벤트의 고유 식별자입니다. |
| level |Hello 이벤트의 수준입니다. Hello 다음 값 중 하나: "Critical", "Error", "Warning", "Informational" 및 "Verbose" |
| resourceGroupName |Hello에 대 한 hello 리소스 그룹의 이름을 메트릭 경고 이면 리소스는 영향을 받습니다. 다른 경고 유형에 대 한 자체 hello 경고가 포함 된 hello 리소스 그룹의 hello 이름입니다. |
| resourceProviderName |Hello에 대 한 hello 리소스 공급자의 이름 메트릭 경고 이면 리소스는 영향을 받습니다. 다른 경고 유형에 대 한 자체 hello 경고에 대 한 hello 리소스 공급자의 hello 이름입니다. |
| resourceId | Hello에 대 한 hello 리소스 ID의 이름 메트릭 경고 이면 리소스는 영향을 받습니다. 다른 경고 유형에 대 한 hello 경고 리소스 자체의 hello 리소스 ID입니다. |
| operationId |Hello 해당 하는 이벤트 tooa 단일 작업 간에 공유 하는 GUID입니다. |
| operationName |Hello 작업의 이름입니다. |
| properties |설정 `<Key, Value>` hello 이벤트의 hello 세부 정보를 설명 하는 쌍 (즉, 사전). |
| status |Hello 연산의 hello 상태를 설명 하는 문자열입니다. 일반적인 값: Started, In Progress, Succeeded, Failed, Active, Resolved. |
| subStatus | 경고의 경우 대개 null입니다. |
| eventTimestamp |Hello Azure 서비스 처리 hello에서 hello 이벤트가 생성 된 시점의 타임 스탬프는 해당 하는 hello 이벤트를 요청 합니다. |
| submissionTimestamp |Hello 이벤트를 쿼리 하기 위해 사용할 수 있게 하는 경우 타임 스탬프입니다. |
| subscriptionId |Azure 구독 ID입니다. |

### <a name="properties-field-per-alert-type"></a>경고 유형별 속성 필드
hello 속성 필드 hello 경고 이벤트의 hello 소스에 따라 다른 값이 포함 됩니다. 일반적으로 사용되는 두 경고 이벤트 공급자는 활동 로그 경고와 메트릭 경고입니다.

#### <a name="properties-for-activity-log-alerts"></a>활동 로그 경고의 속성
| 요소 이름 | 설명 |
| --- | --- |
| properties.subscriptionId | hello 활성화이 활동 로그 경고 규칙 toobe를 일으킨 hello 활동 로그 이벤트를 구독 ID입니다. |
| properties.eventDataId | 활성화 되는이 활동 로그 경고 규칙 toobe를 일으킨 hello 활동 로그 이벤트에서 hello 이벤트 데이터 ID입니다. |
| properties.resourceGroup | hello 리소스 그룹에서 활성화 되는이 활동 로그 경고 규칙 toobe를 일으킨 hello 활동 로그 이벤트. |
| properties.resourceId | 활성화 되는이 활동 로그 경고 규칙 toobe를 일으킨 hello 활동 로그 이벤트에서 hello 리소스 ID입니다. |
| properties.eventTimestamp | 활성화 되는이 활동 로그 경고 규칙 toobe를 일으킨 hello 활동 로그 이벤트의 hello 이벤트 타임 스탬프입니다. |
| properties.operationName | 활성화 되는이 활동 로그 경고 규칙 toobe를 일으킨 hello 활동 로그 이벤트 hello 작업 이름입니다. |
| properties.status | 활성화 되는이 활동 로그 경고 규칙 toobe를 일으킨 hello 활동 로그 이벤트에서 hello 상태입니다.|

#### <a name="properties-for-metric-alerts"></a>메트릭 경고의 속성
| 요소 이름 | 설명 |
| --- | --- |
| properties.RuleUri | Hello 메트릭 경고 규칙 자체의 리소스 ID입니다. |
| properties.RuleName | hello 메트릭 경고 규칙의 hello 이름입니다. |
| properties.RuleDescription | hello 경고 규칙에 정의 된) (대로 hello 메트릭 경고 규칙의 hello 설명입니다. |
| properties.Threshold | hello 임계값 hello 메트릭 경고 규칙의 hello 평가에 사용 된입니다. |
| properties.WindowSizeInMinutes | hello 메트릭 경고 규칙의 hello 평가에 사용 된 hello 창 크기입니다. |
| properties.Aggregation | hello 메트릭 경고 규칙에 정의 된 hello 집계 유형입니다. |
| properties.Operator | hello 메트릭 경고 규칙의 hello 평가에 사용 된 hello 조건부 연산자입니다. |
| properties.MetricName | hello hello 메트릭 경고 규칙의 hello 평가에 사용 된 hello 메트릭의 메트릭 이름입니다. |
| properties.MetricUnit | hello hello 메트릭 경고 규칙의 hello 평가에 사용 된 hello 메트릭의 메트릭 단위입니다. |

## <a name="autoscale"></a>Autoscale
이 범주에는 구독에 정의 된 자동 크기 조정 설정에 따라 hello 자동 크기 조정 엔진의 모든 이벤트 관련된 toohello 연산의 hello 레코드에 포함 합니다. Hello 유형의이 범주에 표시 되는 이벤트의 예로 "자동 크기 조정 수직 확장 작업이 실패 했습니다.." 자동 크기 조정을 사용 하 여 자동으로 확장 하거나 수의 크기를 조정 hello는 지원 되는 리소스 형식에 있는 인스턴스의 수는 자동 크기 조정 설정을 사용 하 여 날짜 및/또는 부하 (메트릭) 데이터는 시간에 따라 합니다. Hello 조건이 충족 되 면 tooscale 위나 아래로 시작 hello 및 성공 또는 실패 한 이벤트는이 범주에 기록 됩니다.

### <a name="sample-event"></a>샘플 이벤트
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
  "eventDataId": "a5b92075-1de9-42f1-b52e-6f3e4945a7c7",
  "eventName": {
    "value": "AutoscaleAction",
    "localizedValue": "AutoscaleAction"
  },
  "category": {
    "value": "Autoscale",
    "localizedValue": "Autoscale"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup/events/a5b92075-1de9-42f1-b52e-6f3e4945a7c7/ticks/636361956518681572",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "microsoft.insights",
    "localizedValue": "microsoft.insights"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup",
  "resourceType": {
    "value": "microsoft.insights/autoscalesettings",
    "localizedValue": "microsoft.insights/autoscalesettings"
  },
  "operationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "operationName": {
    "value": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action",
    "localizedValue": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action"
  },
  "properties": {
    "Description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
    "ResourceName": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource",
    "OldInstancesCount": "3",
    "NewInstancesCount": "2",
    "LastScaleActionTime": "Fri, 21 Jul 2017 01:00:51 GMT"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T01:00:51.8681572Z",
  "submissionTimestamp": "2017-07-21T01:00:52.3008754Z",
  "subscriptionId": "mySubscriptionID"
}

```

### <a name="property-descriptions"></a>속성 설명
| 요소 이름 | 설명 |
| --- | --- |
| caller | 항상 Microsoft.Insights/autoscaleSettings입니다. |
| channels | 항상 "Admin, Operation"입니다. |
| claims | Hello hello 자동 크기 조정 엔진의 SPN (서비스 사용자 이름) 또는 리소스 유형 사용 하 여 JSON blob입니다. |
| CorrelationId | Hello 문자열 형식의 GUID입니다. |
| 설명 |Hello 자동 크기 조정 이벤트의 정적 텍스트 설명입니다. |
| eventDataId |Hello 자동 크기 조정 이벤트의 고유 식별자입니다. |
| level |Hello 이벤트의 수준입니다. Hello 다음 값 중 하나: "Critical", "Error", "Warning", "Informational" 및 "Verbose" |
| resourceGroupName |Hello 자동 크기 조정 설정에 대 한 hello 리소스 그룹의 이름입니다. |
| resourceProviderName |Hello 자동 크기 조정 설정에 대 한 hello 리소스 공급자의 이름입니다. |
| resourceId |Hello 자동 크기 조정 설정의 리소스 id입니다. |
| operationId |Hello 해당 하는 이벤트 tooa 단일 작업 간에 공유 하는 GUID입니다. |
| operationName |Hello 작업의 이름입니다. |
| properties |설정 `<Key, Value>` hello 이벤트의 hello 세부 정보를 설명 하는 쌍 (즉, 사전). |
| properties.Description | 어떤 hello 자동 크기 조정 엔진에 수행 되 던의 자세한 설명입니다. |
| properties.ResourceName | 리소스의 영향을 hello의 리소스 ID (리소스 크기 조정 작업이 수행 되 고 있는 hello에 hello) |
| properties.OldInstancesCount | hello hello 자동 크기 조정 작업 전에 인스턴스 수에 적용이 될 합니다. |
| properties.NewInstancesCount | hello 자동 크기 조정 작업에 적용 될 후 인스턴스의 hello 수입니다. |
| properties.LastScaleActionTime | hello 자동 크기 조정 작업이 발생 했을 때의 타임 스탬프를 hello입니다. |
| status |Hello 연산의 hello 상태를 설명 하는 문자열입니다. 일반적인 값: Started, In Progress, Succeeded, Failed, Active, Resolved. |
| subStatus | 자동 크기 조정의 경우 대개 null입니다. |
| eventTimestamp |Hello Azure 서비스 처리 hello에서 hello 이벤트가 생성 된 시점의 타임 스탬프는 해당 하는 hello 이벤트를 요청 합니다. |
| submissionTimestamp |Hello 이벤트를 쿼리 하기 위해 사용할 수 있게 하는 경우 타임 스탬프입니다. |
| subscriptionId |Azure 구독 ID입니다. |

## <a name="next-steps"></a>다음 단계
* [활동 로그 (이전의 감사 로그) hello에 대 한 자세한 정보](monitoring-overview-activity-logs.md)
* [Hello Azure 활동 로그 tooEvent 허브 스트림](monitoring-stream-activity-logs-event-hubs.md)
