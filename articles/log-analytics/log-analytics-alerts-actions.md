---
title: "OMS 로그 분석에서 aaaResponses tooalerts | Microsoft Docs"
description: "로그 분석에 OMS 리포지토리에 중요 한 정보를 식별 및 수 사전 문제점을 알려 경고나 작업 tooattempt toocorrect 호출을 합니다.  이 문서에서는 어떻게 toocreate 경고 규칙 및 세부 정보 hello 다양 한 작업 취할 수를 설명 합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d24bb726a96e7143985f111c0599dc4e7898b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-actions-tooalert-rules-in-log-analytics"></a>로그 분석의 동작 tooalert 규칙 추가
때는 [로그 분석에 경고가 생성 됩니다](log-analytics-alerts.md), hello 옵션이 [구성 hello 경고 규칙](log-analytics-alerts.md) tooperform 하나 이상의 동작 합니다.  이 문서에서는 각 종류를 구성 하는 방법에 사용할 수 있는 다른 작업 hello 및 세부 정보를 설명 합니다.

| 동작 | 설명 |
|:--|:--|
| [Email](#email-actions) | Hello 경고 tooone 또는 더 많은 수신자 한 hello 세부 정보가 포함 된 전자 메일을 보냅니다. |
| [웹후크](#webhook-actions) | 단일 HTTP POST 요청을 통해 외부 프로세스를 호출합니다. |
| [Runbook](#runbook-actions) | Azure Automation에서 Runbook을 시작합니다. |


## <a name="email-actions"></a>전자 메일 작업
전자 메일 작업 hello 경고 tooone 또는 더 많은 수신자 한 hello 세부 정보가 포함 된 전자 메일을 보냅니다.  Hello 메일의 hello 주체를 지정할 수는 있지만 콘텐츠는 로그 분석에 의해 생성 되는 표준 형식입니다.  Hello 로그 검색에서 반환 된 tooten 레코드를의 추가 toodetails에 hello 경고의 hello 이름과 같은 요약 정보를 포함 합니다.  또한 해당 쿼리에서 hello 레코드의 전체 집합을 반환 하는 로그 분석에 링크 tooa 로그 검색을 포함 합니다.   hello 메일의 보낸 사람이 hello *Microsoft Operations Management Suite 팀 &lt; noreply@oms.microsoft.com &gt;* 합니다. 

전자 메일 작업 hello 속성 hello 표 다음에 필요 합니다.

| 속성 | 설명 |
|:--- |:--- |
| 제목 |Hello 전자 메일의 제목입니다.  Hello 메일의 본문 hello를 수정할 수 없습니다. |
| 받는 사람 |모든 전자 메일 받는 사람의 주소입니다.  세미콜론 (;)를 사용 하 여 여러 개의 주소가 다음 별도 hello 주소를 지정 합니다. |


## <a name="webhook-actions"></a>웹후크 작업

Webhook 작업 tooinvoke 단일 HTTP POST 요청을 통해 외부 프로세스를 허용 합니다.  호출 중인 hello 서비스 webhook을 지원 하 고 모든 페이로드 사용 방식 결정 해야 수신 합니다.  또한 webhook hello 요청은 형식 API에 대 한 이해는 hello로 특별히 지원 하지 않는 REST API를 호출할 수 있습니다.  응답 tooan 경고에는 webhook을 사용 하는 예제는 메시지를 보내도록 [Slack](http://slack.com) 에서 인시던트를 만들거나 [PagerDuty](http://pagerduty.com/)합니다.  제공 되는 전체 연습은 webhook toocall 여유 시간을 사용 하 여 경고 규칙을 만드는 [로그 분석 경고에 대 한 Webhook](log-analytics-alerts-webhooks.md)합니다.

Webhook 작업 hello 속성 hello 표 다음에 필요 합니다.

| 속성 | 설명 |
|:--- |:--- |
| Webhook URL |hello webhook의 hello URL입니다. |
| 사용자 지정 JSON 페이로드 |사용자 지정 페이로드 toosend hello webhook 사용 합니다.  자세한 내용은 다음을 참조하세요. |


Webhook URL을 포함 하 고 hello 데이터가 JSON으로 서식이 지정 된 페이로드 toohello 외부 서비스를 전송 합니다.  기본적으로 hello 페이로드는 다음 표에 hello에 hello 값을 포함 합니다.  사용자 고유의 중 하나를 사용자 지정이 페이로드의 tooreplace를 선택할 수 있습니다.  이 경우 사용할 수 있습니다 hello 테이블에 있는 hello 변수에 각 매개 변수 tooinclude hello에 대 한 해당 값에 사용자 지정 페이로드.

| 매개 변수 | 변수 | 설명 |
|:--- |:--- |:--- |
| AlertRuleName |#alertrulename |Hello 경고 규칙의 이름입니다. |
| AlertThresholdOperator |#thresholdoperator |Hello 경고 규칙에 대 한 임계값 연산자입니다.  *보다 큼* 또는 *보다 작음*. |
| AlertThresholdValue |#thresholdvalue |Hello 경고 규칙에 대 한 임계값입니다. |
| LinkToSearchResults |#linktosearchresults |Hello 경고를 생성 하는 hello 쿼리에서 hello 레코드를 반환 하는 tooLog 분석 로그 검색에 연결 합니다. |
| ResultCount |#searchresultcount |Hello 검색 결과에서 레코드 수입니다. |
| SearchIntervalEndtimeUtc |#searchintervalendtimeutc |Hello 쿼리 UTC 형식에서에 대 한 종료 시간입니다. |
| SearchIntervalInSeconds |#searchinterval |Hello 경고 규칙에 대 한 시간 창입니다. |
| SearchIntervalStartTimeUtc |#searchintervalstarttimeutc |Hello 쿼리에 대 한 시간을 UTC 형식에서 시작 합니다. |
| SearchQuery |#searchquery |로그 검색 쿼리 hello 경고 규칙으로 사용 합니다. |
| SearchResults |아래 참조 |JSON 형식의 hello 쿼리에서 반환 된 레코드입니다.  제한 된 toohello 먼저 5, 000 레코드입니다. |
| WorkspaceID |#workspaceid |OMS 작업 영역의 ID입니다. |

예를 들어 다음 라는 단일 매개 변수를 포함 하는 사용자 지정 페이로드 hello를 지정할 수 있습니다 *텍스트*합니다.  이 webhook 호출 hello 서비스는이 매개 변수를 예상 합니다.

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

이 예에서는 페이로드를 hello 때 다음 같은 toosomething 전송 toohello webhook 해결 합니다.

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

검색 결과 사용자 지정 페이로드를 tooinclude hello hello json 페이로드에서 최상위 속성으로 다음 줄을 추가 합니다.  

    "IncludeSearchResults":true

예를 들어 방금 hello 경고 이름 및 hello 검색 결과 포함 하는 사용자 지정 페이로드 toocreate hello 다음을 사용할 수 있습니다. 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


외부 서비스 webhook toostart를 사용 하 여 경고 규칙을 만드는 전체 예제를 진행할 수 [toosend 메시지 tooSlack OMS 로그 분석에서에서 경고 webhook 작업을 만들](log-analytics-alerts-webhooks.md)합니다.

## <a name="runbook-actions"></a>Runbook 작업
Runbook 작업은 Azure 자동화에서 Runbook을 시작합니다.  주문 toouse 이런이 종류의 동작, hello 있어야 [자동화 솔루션](log-analytics-add-solutions.md) OMS 작업 영역에 설치 및 구성 합니다.  Hello 자동화 솔루션에서에서 구성한 hello 자동화 계정에서 hello runbook에서 선택할 수 있습니다.

Runbook 작업에는 다음 표에 hello에 hello 속성 필요 합니다.

| 속성 | 설명 |
|:--- |:---|
| Runbook | 경고를 만들 때 toostart 되도록 Runbook입니다. |
| 실행 | 지정 **Azure** hello 클라우드에서 toorun hello runbook입니다.  지정 **Hybrid worker** 와 에이전트에서 toorun hello runbook [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) 설치 합니다.  |

Runbook 작업을 사용 하 여 hello runbook 시작는 [webhook](../automation/automation-webhooks.md)합니다.  Hello 경고 규칙을 만들 때 자동으로 만들어집니다 hello runbook에 대 한 새 webhook hello 이름의 **OMS 경고 재구성** GUID가 차례로 포함 합니다.  

직접 hello runbook의 모든 매개 변수를 채울 하지만 hello 없습니다 [$WebhookData 매개 변수](../automation/automation-webhooks.md) hello를 만든 hello 로그 검색 결과 포함 하 여 hello 알림의 hello 세부 정보가 포함 됩니다.  hello runbook toodefine 할 **$WebhookData** 것에 대 한 매개 변수로 tooaccess hello hello 경고의 속성입니다.  hello 경고 데이터는 라는 단일 속성에 대 한 json 형식으로 사용할 수 있는 **SearchResults** hello에 **RequestBody** 속성 **$WebhookData**합니다.  다음 표에 hello hello 속성과 함께이 갖습니다.

| 노드 | 설명 |
|:--- |:--- |
| id |경로 hello 검색의 GUID입니다. |
| __metadata |Hello 경고 포함 하 여 hello 레코드의 수 및 hello 검색 결과의 상태에 대 한 정보입니다. |
| 값 |Hello 검색 결과의 각 레코드에 대 한 별도 항목입니다.  hello 항목의 hello 세부 정보에는 hello 레코드의 hello 속성 및 값과 일치 합니다. |

예를 들어 hello 다음 runbook은 hello 로그 검색에서 반환 되는 hello 레코드를 추출 하 고 각 레코드의 hello 형식을 기반으로 하는 다른 속성을 할당 합니다.  변환 하 여 해당 hello runbook 시작 **RequestBody** 에서 json 한다는 PowerShell의 개체와 작동할 수 있도록 합니다.

    param ( 
        [object]$WebhookData
    )

    $RequestBody = ConvertFrom-JSON -InputObject $WebhookData.RequestBody
    $Records     = $RequestBody.SearchResults.value

    foreach ($Record in $Records)
    {
        $Computer = $Record.Computer

        if ($Record.Type -eq 'Event')
        {
            $EventNo    = $Record.EventID
            $EventLevel = $Record.EventLevelName
            $EventData  = $Record.EventData
        }

        if ($Record.Type -eq 'Perf')
        {
            $Object    = $Record.ObjectName
            $Counter   = $Record.CounterName
            $Instance  = $Record.InstanceName
            $Value     = $Record.CounterValue
        }
    }


## <a name="next-steps"></a>다음 단계
- 경고 규칙을 사용하여 [웹후크를 구성](log-analytics-alerts-webhooks.md) 하는 연습을 완료합니다.  
- 자세한 내용은 어떻게 toowrite [Azure 자동화의 runbook](https://azure.microsoft.com/documentation/services/automation) tooremediate 문제를 경고로 식별 합니다.
