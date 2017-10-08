---
title: "Azure 메트릭 경고 aaaConfigure webhook | Microsoft Docs"
description: "Azure 경고 tooother 비 Azure 시스템 경로 재정의 합니다."
author: johnkemnetz
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 8b3ae540-1d19-4f3d-a635-376042f8a5bb
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: johnkem
ms.openlocfilehash: bc4153ccdcff41c5b9d3c081e59a1bf260d8a283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-webhook-on-an-azure-metric-alert"></a>Azure 활동 메트릭 경고에 대한 웹후크 구성
또한 Webhook 허용 tooroute Azure 사후 처리 또는 사용자 지정 작업에 대 한 알림 tooother 시스템 경고 합니다. webhook을 사용 하 여 경고 tooroute에 것 tooservices SMS를 전송 하는 버그를 로그, 채팅/메시징 서비스를 통해 팀에 게 알림 또는 여러 다른 동작을 수행 합니다. 이 문서에서는 설명 방법을 tooset Azure 메트릭 경고 및 어떤 hello 페이로드 hello HTTP POST tooa webhook에 대 한 다음과 같은 webhook 합니다. Hello 설치와 Azure 활동 로그 경고 (경고) 이벤트에 대 한 스키마에 대 한 내용은 [이 페이지가 대신 표시](insights-auditlog-to-webhook-email.md)합니다.

Azure 경고 JSON 형식으로 HTTP POST hello 경고 내용 스키마 아래에 정의 된, tooa webhook hello 경고를 만들 때 제공 하는 URI입니다. 이 URI의 HTTP 또는 HTTPS 끝점은 유효해야 합니다. 경고가 활성화되면 Azure에서 요청당 항목 하나만 게시합니다.

## <a name="configuring-webhooks-via-hello-portal"></a>Webhook hello 포털을 통해 구성
추가 하거나 hello webhook URI hello 만들기/업데이트 경고 화면 hello에서 업데이트할 수 있습니다 [포털](https://portal.azure.com/)합니다.

![경고 규칙 추가](./media/insights-webhooks-alerts/Alertwebhook.png)

경고 toopost tooa webhook URI를 구성할 수도 있습니다 hello를 사용 하 여 [Azure PowerShell Cmdlet](insights-powershell-samples.md#create-metric-alerts), [플랫폼 간 CLI](insights-cli-samples.md#work-with-alerts), 또는 [Azure 모니터 REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx)합니다.

## <a name="authenticating-hello-webhook"></a>Hello webhook 인증
hello webhook 토큰 기반 인증을 사용 하 여 인증할 수 있습니다. hello webhook URI와 함께 저장 됩니다 토큰 ID를 제외 합니다. `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`

## <a name="payload-schema"></a>페이로드 스키마
POST 작업 hello hello JSON 페이로드 및 모든 메트릭을 기반 경고에 대 한 스키마를 포함 합니다.

```JSON
{
"status": "Activated",
"context": {
            "timestamp": "2015-08-14T22:26:41.9975398Z",
            "id": "/subscriptions/s1/resourceGroups/useast/providers/microsoft.insights/alertrules/ruleName1",
            "name": "ruleName1",
            "description": "some description",
            "conditionType": "Metric",
            "condition": {
                        "metricName": "Requests",
                        "metricUnit": "Count",
                        "metricValue": "10",
                        "threshold": "10",
                        "windowSize": "15",
                        "timeAggregation": "Average",
                        "operator": "GreaterThanOrEqual"
                },
            "subscriptionId": "s1",
            "resourceGroupName": "useast",                                
            "resourceName": "mysite1",
            "resourceType": "microsoft.foo/sites",
            "resourceId": "/subscriptions/s1/resourceGroups/useast/providers/microsoft.foo/sites/mysite1",
            "resourceRegion": "centralus",
            "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/useast/providers/microsoft.foo/sites/mysite1"
},
"properties": {
              "key1": "value1",
              "key2": "value2"
              }
}
```


| 필드 | 필수 | 고정된 값 집합 | 참고 사항 |
|:--- |:--- |:--- |:--- |
| status |Y |“Activated”, “Resolved” |Hello 경고 hello 조건을 기반으로 설정한 경우에 대 한 상태입니다. |
| context |Y | |hello 경고 컨텍스트입니다. |
| timestamp |Y | |hello 시간은 hello에 경고가 발생 합니다. |
| id |Y | |모든 경고 규칙에는 고유한 ID가 있습니다. |
| name |Y | |hello 경고 이름입니다. |
| 설명 |Y | |Hello 경고의 설명입니다. |
| conditionType |Y |“Metric”, “Event” |두 형식의 경고가 지원됩니다. 메트릭 조건과 hello 다른 hello 활동 로그에서에서 이벤트를 기준에 따라 하나입니다. Hello 경고 메트릭 또는 이벤트를 기반으로 하는 경우이 값 toocheck를 사용 합니다. |
| condition |Y | |에 대 한 특정 필드 toocheck hello hello conditionType 기반으로 합니다. |
| metricName |메트릭 경고의 경우 | |어떤 hello 규칙을 정의 하는 hello 메트릭의 이름 hello를 모니터링 합니다. |
| metricUnit |메트릭 경고의 경우 |"Bytes", "BytesPerSecond", "Count", "CountPerSecond", "Percent", "Seconds" |hello 메트릭에 허용 되는 hello 단위입니다. [허용되는 값은 여기에 나열되어 있습니다](https://msdn.microsoft.com/library/microsoft.azure.insights.models.unit.aspx). |
| metricValue |메트릭 경고의 경우 | |hello hello 경고를 발생 시킨 hello 메트릭의 실제 값입니다. |
| threshold |메트릭 경고의 경우 | |hello 임계값은 hello 경고가 활성화 될입니다. |
| windowSize |메트릭 경고의 경우 | |hello 기간 hello 임계값에 따라 사용 되는 toomonitor 경보 활동입니다. 5분에서 하루 사이여야 합니다. ISO 8601 기간 형식입니다. |
| timeAggregation |메트릭 경고의 경우 |"Average", "Last", "Maximum", "Minimum", "None", "Total" |Hello 수집 된 데이터를 시간에 따라 결합 해야 하는 방법을 hello 기본값은 평균입니다. [허용되는 값은 여기에 나열되어 있습니다](https://msdn.microsoft.com/library/microsoft.azure.insights.models.aggregationtype.aspx). |
| operator |메트릭 경고의 경우 | |hello 연산자 toocompare hello 현재 메트릭 데이터 toohello 설정한 임계값을 사용합니다. |
| subscriptionId |Y | |Azure 구독 ID입니다. |
| resourceGroupName |Y | |Hello에 대 한 hello 리소스 그룹의 이름을 리소스를 저하 됩니다. |
| resourceName |Y | |리소스 이름 hello 리소스를 저하 됩니다. |
| resourceType |Y | |Hello 리소스 유형의 리소스를 저하 됩니다. |
| resourceId |Y | |Hello의 리소스 ID 리소스를 저하 됩니다. |
| resourceRegion |Y | |지역 또는 hello 위치의 리소스에 영향을 받습니다. |
| portalLink |Y | |직접 링크 toohello 포털 리소스 요약 페이지입니다. |
| properties |N |옵션 |설정 `<Key, Value>` 쌍 (예: `Dictionary<String, String>`) hello 이벤트에 대 한 세부 정보를 포함 하는 합니다. hello 속성 필드는 선택 사항입니다. 워크플로에서 사용자 지정 UI 또는 논리 앱 기반 hello 페이로드를 통해 전달 될 수 있는 키/값을 입력할 수 있습니다. (쿼리 매개 변수)으로 자체 hello webhook uri를 통해 hello 대체 방법을 toopass 사용자 지정 속성 백 toohello webhook은 |

> [!NOTE]
> hello 속성 필드에만 설정할 수 hello를 사용 하 여 [Azure 모니터 REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx)합니다.
>
>

## <a name="next-steps"></a>다음 단계
* Azure 경고 및 hello 비디오에서 webhook에 대 한 자세한 정보 [Azure 경고와 PagerDuty 통합](http://go.microsoft.com/fwlink/?LinkId=627080)
* [Azure 경고에 대한 Azure Automation 스크립트 실행 (Runbooks)](http://go.microsoft.com/fwlink/?LinkId=627081)
* [Azure 경고에서 논리 앱 toosend Twilio 통해 SMS를 사용 하 여](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
* [논리 앱 toosend Azure 경고에서 Slack 메시지를 사용 하 여](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
* [논리 앱 toosend Azure 경고에서 메시지 tooan Azure 큐를 사용 하 여](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)
