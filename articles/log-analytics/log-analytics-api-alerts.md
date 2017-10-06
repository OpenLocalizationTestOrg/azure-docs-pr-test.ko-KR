---
title: "aaaUsing OMS 로그 분석 경고 REST API"
description: "로그 분석 경고 REST API hello toocreate 있으며 Operations Management Suite (OMS)에 포함 된 로그 분석에서 경고를 관리 합니다.  이 문서는 다양 한 작업을 수행 하기 위한 hello API 및 몇 가지 예제에 대 한 세부 정보를 제공 합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 628ad256-7181-4a0d-9e68-4ed60c0f3f04
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 418dc7eb71d6151c6380b8925f1f147a0e13b178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a>REST API로 Log Analytics에서 경고 규칙 만들기 및 관리
로그 분석 경고 REST API hello toocreate 있으며 Operations Management Suite (OMS)에서 경고를 관리 합니다.  이 문서는 다양 한 작업을 수행 하기 위한 hello API 및 몇 가지 예제에 대 한 세부 정보를 제공 합니다.

hello 로그 분석 검색 REST API는 RESTful 이며 Azure 리소스 관리자 REST API hello를 통해 액세스할 수 있습니다. 이 문서의 예제를 확인할 수 hello API 사용 하 여 PowerShell 명령줄에서 액세스 되는 위치 [ARMClient](https://github.com/projectkudu/ARMClient), 호출을 간소화 하는 오픈 소스 명령줄 도구인 hello Azure 리소스 관리자 API입니다. ARMClient 및 PowerShell 사용 hello 많은 옵션 tooaccess hello 로그 분석 검색 API 중 하나입니다. 이러한 도구와 hello RESTful Azure 리소스 관리자 API toomake 호출 tooOMS 작업 영역을 사용 하 고 그 안에서 검색 명령을 수행할 수 있습니다. hello API은 JSON 형식으로 있도록 toouse hello 검색 결과 다양 한 방법으로 프로그래밍 방식으로 검색 결과 tooyou를 출력 됩니다.

## <a name="prerequisites"></a>필수 조건
현재 Log Analytics에 저장된 검색을 사용해서만 경고를 만들 수 있습니다.  Toohello 참조할 수 있습니다 [로그 검색 REST API](log-analytics-log-search-api.md) 자세한 정보에 대 한 합니다.

## <a name="schedules"></a>일정
저장된 검색은 하나 이상의 일정을 가질 수 있습니다. hello 일정 정의 얼마나 자주 hello 검색은를 실행 하 고 hello 기준 hello 시간 마다 식별 됩니다.
다음 표에 hello에 hello 속성을 포함 하는 예약 합니다.

| 속성 | 설명 |
|:--- |:--- |
| 간격 |얼마나 자주 hello 검색 실행 됩니다. 분 단위로 측정됩니다. |
| QueryTimeSpan |hello 시간 간격을 어떤 hello를 통해 조건 평가 됩니다. 간격 보다 클 같은 tooor를 이어야 합니다. 분 단위로 측정됩니다. |
| 버전 |사용 되는 API 버전 번호입니다.  현재이 항상 설정할 too1입니다. |

예를 들어 간격이 15 분이고 Timespan이 30 분인 이벤트 쿼리를 고려합니다. 이 경우 hello 쿼리 15 분 마다 실행 하 고 hello 조건 30 분 기간 동안 tooresolve tootrue 계속 하는 경우 경고를 트리거할 수 합니다.

### <a name="retrieving-schedules"></a>일정 검색
사용 하 여 hello 메서드 tooretrieve 저장된 된 검색에 대 한 모든 일정을 가져옵니다.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

사용 하 여 hello 저장된 된 검색에 대 한 특정 일정을 일정 ID tooretrieve 사용 하 여 메서드를 가져옵니다.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

다음은 일정에 대한 샘플 응답입니다.

```json
{
    "value": [{
        "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/MyWorkspace/savedSearches/0f0f4853-17f8-4ed1-9a03-8e888b0d16ec/schedules/a17b53ef-bd70-4ca4-9ead-83b00f2024a8",
        "etag": "W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\"",
        "properties": {
            "Interval": 15,
            "QueryTimeSpan": 15
        }
    }]
}
```

### <a name="creating-a-schedule"></a>일정 만들기
Hello Put 메서드를 사용 하 여 고유한 일정 ID toocreate 새 일정을 사용 합니다.  두 일정 없습니다는 hello 동일한 ID와 연결 된 다른 저장 된 검색 하는 경우에 참고 합니다.  Hello 일정 id는 GUID는 만들고 hello OMS 콘솔에서 일정을 만들 때

> [!NOTE]
> 저장 된 모든 검색, 일정 및 hello 로그 분석 API를 사용 하 여 만든 작업에 대 한 hello 이름은 소문자 여야 합니다.

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a>일정 편집
동일한 저장 hello에 대 한 ID 검색 toomodify 예약 하는 기존 일정과 hello Put 메서드를 사용 합니다.  hello hello 요청 본문 hello 일정의 hello etag를 포함 해야 합니다.

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a>일정 삭제
일정 ID toodelete 일정 hello Delete 메서드를 사용 합니다.

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a>작업
일정이 여러 작업을 가질 수 있습니다. 작업 하나 이상의 프로세스 tooperform 메일을 보내거나 runbook을 시작 하는 등을 정의할 수 있습니다 또는 hello 결과 검색 기준과 일치 하는 시기를 결정 하는 임계값을 정의할 수 있습니다.  Hello 임계값이 충족 되 면 hello 프로세스를 수행할 수 있도록 일부 작업을 모두 정의 합니다.

모든 작업에는 다음 표에 hello에 hello 속성이 있습니다.  서로 다른 유형의 경고는 아래에 설명하는 서로 다른 추가 속성을 가집니다.

| 속성 | 설명 |
|:--- |:--- |
| 형식 |Hello 작업 형식입니다.  현재 hello 가능한 값은 경고 및 Webhook 합니다. |
| 이름 |Hello 경고에 대 한 표시 이름입니다. |
| 버전 |사용 되는 API 버전 번호입니다.  현재이 항상 설정할 too1입니다. |

### <a name="retrieving-actions"></a>작업 검색
사용 하 여 hello 메서드 tooretrieve 일정에 대 한 모든 작업을 가져옵니다.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

사용 하 여 hello hello 동작 ID tooretrieve 메서드는 일정에 대 한 특정 동작을 가져옵니다.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a>작업 만들기 또는 편집
작업 id는 고유 toohello 일정 toocreate 새 동작 ID와 hello Put 메서드를 사용 합니다.  Hello 동작 id는 GUID는 hello OMS 콘솔에서 작업을 만들 때

> [!NOTE]
> 저장 된 모든 검색, 일정 및 hello 로그 분석 API를 사용 하 여 만든 작업에 대 한 hello 이름은 소문자 여야 합니다.

동일한 저장 hello에 대 한 ID toomodify 예약 하는 검색 하는 기존 작업을 통해 hello Put 메서드를 사용 합니다.  hello hello 요청 본문 hello 일정의 hello etag를 포함 해야 합니다.

이 예에서는 hello 섹션 아래에 제공 되어 있으므로 새 동작을 만들기 위한 hello 요청 형식 동작 유형에 따라 다릅니다.

### <a name="deleting-actions"></a>작업 삭제
Hello 동작 ID toodelete 동작 hello Delete 메서드를 사용 합니다.

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a>경고 작업
일정은 경고 작업을 한 개만 가져야 합니다.  경고 작업에는 다음 표에 hello에 hello 섹션 중 하나 이상을 해야 합니다.  아래에서 각 섹션을 자세히 설명합니다.

| 섹션 | 설명 |
|:--- |:--- |
| 임계값 |Hello 동작 실행 시기에 대 한 조건입니다. |
| EmailNotification |Toomultiple 받는 사람에 게 메일을 보냅니다. |
| 재구성 |Tooattempt toocorrect 식별 된 문제 Azure 자동화에서에서 runbook을 시작 합니다. |

#### <a name="thresholds"></a>임계값
경고 작업은 임계값을 한 개만 가져야 합니다.  저장된 된 검색의 hello 결과가 해당 검색과 관련 된 동작에서 hello 임계값 일치 하는 경우 해당 작업의 다른 프로세스가 실행 됩니다.  작업은 임계값을 포함하지 않은 다른 유형의 작업과 함께 사용할 수 있도록 하는 임계값만 포함할 수 있습니다.

임계값에는 다음 표에 hello에 hello 속성이 있습니다.

| 속성 | 설명 |
|:--- |:--- |
| 연산자 |Hello 임계값 비교 연산자입니다. <br> gt = 보다 큰 <br> lt = 보다 작은 |
| 값 |Hello 임계값에 대 한 값입니다. |

예를 들어 간격이 15 분이고 Timespan이 30 분이고 임계값이 10보다 큰 이벤트 쿼리를 고려합니다. 이 경우 hello 쿼리 15 분 마다 실행 하 고 30 분 기간 동안 생성 된 이벤트 10 개 반환 되 면 경고를 트리거할 수 합니다.

다음은 임계값만 가진 작업에 대한 샘플 응답입니다.  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My threshold action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Version": 1
    }

일정에 대 한 고유한 작업 ID toocreate 새 임계값 동작으로 hello Put 메서드를 사용 합니다.  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

일정에 대 한 기존 동작 ID toomodify 임계값 동작으로 hello Put 메서드를 사용 합니다.  hello hello 요청 본문 hello 동작의 hello etag를 포함 해야 합니다.

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a>메일 알림
전자 메일 알림 메일 tooone 또는 더 많은 받는 사람에 게 보냅니다.  다음 표에 hello에 hello 속성 포함 합니다.

| 속성 | 설명 |
|:--- |:--- |
| 받는 사람 |메일 주소 목록입니다. |
| 제목 |hello 메일의 hello 제목입니다. |
| 첨부 파일 |첨부 파일은 현재 지원되지 않으므로이에 대한 값은 항상 "없음"입니다. |

다음은 임계값을 가진 전자 메일 알림 작업에 대한 샘플 응답입니다.  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My email action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "EmailNotification": {
            "Recipients": [
                "recipient1@contoso.com",
                "recipient2@contoso.com"
            ],
            "Subject": "This is hello subject",
            "Attachment": "None"
        },
        "Version": 1
    }

Hello Put 메서드는 일정에 대 한 고유한 작업 ID toocreate 새 전자 메일 작업을 사용 합니다.  hello 다음 예제에서는 만들므로 전자 메일 알림을 임계값과 hello 저장 된 검색의 hello 결과 hello 임계값을 초과 하는 경우 hello 메일이 전송 됩니다.

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

일정에 대 한 기존 동작 ID toomodify 전자 메일 동작으로 hello Put 메서드를 사용 합니다.  hello hello 요청 본문 hello 동작의 hello etag를 포함 해야 합니다.

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a>수정 작업
재구성은 hello 경고도 식별 된 toocorrect hello 문제를 시도 하는 Azure 자동화에서 runbook을 시작 합니다.  수정 작업에 사용 된 hello runbook에 대 한 webhook을 만들고 hello WebhookUri 속성에서에서 hello URI를 지정 해야 합니다.  Hello OMS 콘솔을 사용 하 여이 작업을 만들 때 새 webhook hello runbook에 대 한 자동으로 만들어집니다.

다음 표에 hello에 hello 속성을 포함 하는 재구성 합니다.

| 속성 | 설명 |
|:--- |:--- |
| RunbookName |Hello runbook의 이름입니다. 이 hello OMS 작업 영역에서 자동화 솔루션에에서 구성 된 hello 자동화 계정에서 게시 된 runbook을 일치 해야 합니다. |
| WebhookUri |Hello webhook의 URI입니다. |
| Expiry |hello 만료 날짜 및 시간 hello webhook입니다.  Hello webhook 없는 경우 만료 날짜, 유효한 모든 이후 날짜를 수 있습니다이 합니다. |

다음은 임계값을 가진 수정 작업에 대한 샘플 응답입니다.

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My remediation action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Remediation": {
            "RunbookName": "My-Runbook",
            "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d",
            "Expiry": "2018-02-25T18:27:20"
            },
        "Version": 1
    }

일정에 대 한 고유한 작업 ID toocreate 새 재구성 작업으로 hello Put 메서드를 사용 합니다.  hello 다음 예제에서는 만들므로 업데이트 관리 임계값과 hello 저장 된 검색의 hello 결과 hello 임계값을 초과 하는 경우 hello runbook이 시작 됩니다.

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

일정에 대 한 기존 동작 ID toomodify 재구성 작업으로 hello Put 메서드를 사용 합니다.  hello hello 요청 본문 hello 동작의 hello etag를 포함 해야 합니다.

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a>예제
다음은 전체 예제 toocreate 새 전자 메일 경고입니다.  이는 임계값 및 전자 메일을 포함하는 작업과 함께 새 일정을 만듭니다.

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a>웹후크 작업
Webhook 작업 URL을 호출 하 여 선택적으로 전송 되는 페이로드 toobe 제공 하는 프로세스를 시작 합니다.  Azure 자동화 runbook 이외의 프로세스를 호출할 수 있는 webhook에 대 한 보관 점을 제외 하 고 서로 유사한 tooRemediation 동작입니다.  또한 hello 페이로드 배달 toobe toohello 원격 프로세스를 제공 하는 중 추가 옵션을 제공 합니다.

Webhook 작업 임계값 필요는 없지만 대신 추가할지 임계값과 경고 동작이 있는 tooa 일정입니다.  모두 실행 되는 hello 임계값이 충족 하는 경우 여러 Webhook 작업을 추가할 수 있습니다.

다음 표에 hello에 hello 속성을 포함 하는 Webhook 작업 합니다.

| 속성 | 설명 |
|:--- |:--- |
| WebhookUri |hello 메일의 hello 제목입니다. |
| CustomPayload |사용자 지정 페이로드 toobe toohello webhook을 전송 합니다.  hello 형식 어떤 hello webhook 예상에 따라 달라 집니다. |

다음은 웹후크 작업 및 임계값을 가진 연결된 경고에 대한 샘플 응답입니다.

    {
        "__metadata": {},
        "value": [
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/72884702-acf9-4653-bb67-f42436b342b4",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"",
                "properties": {
                    "Type": "Webhook",
                    "Name": "My Webhook Action",
                    "WebhookUri": "https://oaaswebhookdf.cloudapp.net/webhooks?token=VfkYTIlpk%2fc%2bJBP",
                    "CustomPayload": "{\"fielld1\":\"value1\",\"field2\":\"value2\"}",
                    "Version": 1
                }
            },
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/90a27cf8-71b7-4df2-b04f-54ed01f1e4b6",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.565204Z'\"",
                "properties": {
                    "Type": "Alert",
                    "Name": "Threshold for my webhook action",
                    "Threshold": {
                        "Operator": "gt",
                        "Value": 10
                    },
                    "Version": 1
                }
            }
        ]
    }

#### <a name="create-or-edit-a-webhook-action"></a>웹후크 작업 만들기 또는 편집
일정에 대 한 고유한 작업 ID toocreate 새 webhook 동작으로 hello Put 메서드를 사용 합니다.  hello 다음 예제에서는 Webhook 작업와 생성 경고 동작 임계값과 hello webhook hello 저장 된 검색의 hello 결과 hello 임계값을 초과할 때 트리거됩니다.

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

일정에 대 한 기존 동작 ID toomodify webhook 작업으로 hello Put 메서드를 사용 합니다.  hello hello 요청 본문 hello 동작의 hello etag를 포함 해야 합니다.

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a>다음 단계
* 사용 하 여 hello [REST API tooperform 로그 검색](log-analytics-log-search-api.md) 로그 분석에 있습니다.

