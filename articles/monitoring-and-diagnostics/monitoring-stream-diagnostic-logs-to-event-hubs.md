---
title: "이벤트 허브 Namespace aaaStream Azure 진단 로그 tooan | Microsoft Docs"
description: "Azure 진단 toostream tooan 이벤트 허브 네임 스페이스를 기록 하는 방법에 대해 알아봅니다."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 42bc4845-c564-4568-b72d-0614591ebd80
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: 00092ea8f3fe4fa1476e3a697bf1e8645dd21e6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-azure-diagnostic-logs-tooan-event-hubs-namespace"></a>Azure 진단 로그 tooan 이벤트 허브 Namespace 스트림
**[Azure 진단 로그](monitoring-overview-of-diagnostic-logs.md)**  거의 실시간으로 tooany hello 포털에서에서 기본 제공 "tooEvent 허브 내보내기" 옵션 hello를 사용 하 여 응용 프로그램에 스트리밍할 수 또는 사용 하 여 hello Azure PowerShell을 통해 진단 설정에 서비스 버스 규칙 ID를 환영 Cmdlet 또는 Azure CLI 합니다.

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a>진단 로그 및 Event Hubs에서 수행할 수 있는 작업
다음 몇 가지 방법으로 hello 진단 로그에 대 한 기능을 스트리밍을 사용할 수 있습니다.

* **스트림에 기록 too3rd 파티 로깅 및 원격 분석 시스템** – 시간이 지남에 따라 이벤트 허브는 hello 메커니즘 toopipe toothird 파티 Siem에서 진단 로그에 될 스트리밍과 로그 분석 솔루션입니다.
* **"실행 부하 과다 경로" 데이터 tooPowerBI 스트리밍하여 서비스 상태를 보려면** – 이벤트 허브를 사용 하 여, 스트림 분석 및 PowerBI, Azure 서비스에 toonear 실시간 insights에서 진단 데이터를 쉽게 변형할 수 있습니다. [이 설명서 문서에서는 이벤트 허브를 tooset 스트림 분석을 사용 하 여 데이터를 처리 하 고 출력을 출력으로 PowerBI를 사용 하는 방법에 대 한 훌륭한 개괄적](../stream-analytics/stream-analytics-power-bi-dashboard.md)합니다. 다음은 진단 로그로 설정하는 방법에 대한 몇 가지 팁입니다.
  
  * 진단 로그의 범주에 대 한 이벤트 허브는 hello 포털 hello 옵션을 확인 하거나 tooselect hello 이름의 네임 스페이스가 hello로 시작 되 면 hello 이벤트 허브를 원하는 PowerShell을 통해 설정할 때 자동으로 생성 됩니다 **insights**.
  * hello SQL 코드 다음은 샘플 스트림 분석 쿼리를 사용할 수 있는 tooparse hello 로그 데이터를 모두 tooa PowerBI 테이블에서:

    ```sql
    SELECT
    records.ArrayValue.[Properties you want tootrack]
    INTO
    [OutputSourceName – hello PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* **빌드 사용자 지정 원격 분석 및 로깅 플랫폼** 는 진단 수집 건물 하나, 확장성이 높은 hello 게시-구독에 대해 생각 방금 이벤트 허브의 특성 tooflexibly 수 있습니다. 또는 사용자가 작성 한 원격 분석 플랫폼을 이미 있는 경우- 기록합니다. [Dan Rosanova 가이드 toousing 이벤트 허브는 세계적인 규모 원격 분석 플랫폼 여기에 참조](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)합니다.

## <a name="enable-streaming-of-diagnostic-logs"></a>진단 로그의 스트리밍 사용
Hello 포털을 통해 프로그래밍 방식으로 진단 로그의 스트리밍 또는 hello를 사용 하 여 사용 하도록 설정할 수 [Azure 모니터 REST Api](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings)합니다. 진단 설정을 만드는 두 가지 경우 모두 지정 하는 이벤트 허브 네임 스페이스 및 hello 로그 범주 및 메트릭을 toosend toohello 네임 스페이스에 있습니다. 이벤트 허브를 사용 하도록 설정 하면 로그 범주별 hello 네임 스페이스에 생성 됩니다. 진단 **로그 범주**는 리소스가 수집할 수 있는 로그 형식입니다.

> [!WARNING]
> 계산 리소스(예: VM 또는 서비스 패브릭)에서 진단 로그를 사용 및 스트리밍하려면 [여러 단계 집합을 거쳐야 합니다](../event-hubs/event-hubs-streaming-azure-diags-data.md).
> 
> 

서비스 버스 hello 또는 이벤트 허브 네임 스페이스가 없는 toobe hello hello 설정을 구성 하는 hello 사용자에 게 적합 한 RBAC 액세스 tooboth 구독으로 로그를 내보내는 hello 리소스와 동일한 구독 합니다.

## <a name="stream-diagnostic-logs-using-hello-portal"></a>Hello 포털을 사용 하 여 스트림 진단 로그
1. Hello 포털 tooAzure 모니터를 탐색 하 고 클릭 **진단 설정**

    ![Azure Monitor의 모니터링 섹션](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. 필요에 따라 리소스 그룹 또는 리소스 유형으로 hello 목록을 필터링 하려는 진단 설정 tooset hello 리소스 클릭 합니다.

3. 선택한 hello 리소스에 설정이 없는 있으면 증명된 toocreate 설정 됩니다. “진단 켜기”를 클릭합니다.

   ![진단 설정 추가 - 기존 설정 없음](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   Hello 리소스에 대 한 기존 설정을 없을 경우이 리소스에서 이미 구성 되어 있는 설정 목록이 표시 됩니다. “진단 설정 추가”를 클릭합니다.

   ![진단 설정 추가 - 기존 설정](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. 사용자 설정 이름을 지정 하 고 hello 확인란에 대 한 **스트림 tooan 이벤트 허브**, 프로그램에서 이벤트 허브 네임 스페이스를 선택 합니다.
   
   ![진단 설정 추가 - 기존 설정](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   hello 네임 스페이스 선택 됩니다 여기서 hello 이벤트 허브 (처음으로 스트리밍 진단 로그 경우) 만들어지거나 너무 스트리밍 (많은 경우 이미 해당 로그 범주 toothis 네임 스페이스는 스트리밍 리소스), hello을 정의 하는 hello 정책 hello 스트리밍 메커니즘에 있는 권한입니다. 이벤트 허브 관리, 송신, 수신 대기 권한을 오늘 필요 tooan 스트리밍 합니다. 작성 하거나 네임 스페이스에 대 한 hello 포털 hello 구성 탭에서 이벤트 허브 네임 스페이스 공유 액세스 정책을 수정할 수 있습니다. tooupdate 이러한 진단 설정 중 하나를 hello 클라이언트 hello 이벤트 허브 권한 부여 규칙에 hello ListKey 권한이 있어야 합니다.

4. **Save**를 클릭합니다.

몇 분 후 hello 새 설정이이 리소스에 대 한 설정의 목록에 나타나고 새 이벤트 데이터는 생성 되는 즉시 진단 로그 toothat 저장소 계정 스트리밍됩니다.

### <a name="via-powershell-cmdlets"></a>PowerShell Cmdlet을 통해
hello를 통해 스트리밍 tooenable [Azure PowerShell Cmdlet](insights-powershell-samples.md), hello를 사용할 수 있습니다 `Set-AzureRmDiagnosticSetting` 이러한 매개 변수를 사용 하 여 cmdlet:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

hello 서비스 버스 규칙 ID는이 형식의 문자열로: `{Service Bus resource ID}/authorizationrules/{key name}`, 예를 들어 `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`합니다.

### <a name="via-azure-cli"></a>Azure CLI를 통해
hello를 통해 스트리밍 tooenable [Azure CLI](insights-cli-samples.md), hello를 사용할 수 있습니다 `insights diagnostic set` 이와 같은 명령을:

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

Hello PowerShell Cmdlet에 대 한 설명 된 대로 서비스 버스 규칙 ID에 대 한 동일한 형식 hello를 사용 합니다.

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a>이벤트 허브에서 로그 데이터를 hello를 사용 어떻게 합니까?
다음은 Event Hubs의 샘플 출력 데이터입니다.

```json
{
    "records": [
        {
            "time": "2016-07-15T18:00:22.6235064Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330013509921957/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Error",
            "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T17:58:55.048482Z",
                "endTime": "2016-07-15T18:00:22.4109204Z",
                "status": "Failed",
                "code": "BadGateway",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330013509921957",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "29a9862f-969b-4c70-90c4-dfbdc814e413",
                    "clientTrackingId": "08587330013509921958"
                }
            }
        },
        {
            "time": "2016-07-15T18:01:15.7532989Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330012106702630/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Information",
            "operationName": "Microsoft.Logic/workflows/workflowActionStarted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T18:01:15.5828115Z",
                "status": "Running",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330012106702630",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "042fb72c-7bd4-439e-89eb-3cf4409d429e",
                    "clientTrackingId": "08587330012106702632"
                }
            }
        }
    ]
}
```

| 요소 이름 | 설명 |
| --- | --- |
| 레코드 |이 페이로드에 있는 모든 로그 이벤트의 배열입니다. |
| 실시간 |Hello 이벤트가 발생 한 시간입니다. |
| 카테고리 |이 이벤트에 대한 로그 범주입니다. |
| resourceId |이 이벤트를 생성 하는 hello 리소스의 리소스 ID입니다. |
| operationName |Hello 작업의 이름입니다. |
| level |선택 사항입니다. Hello 로그 이벤트 수준을 나타냅니다. |
| properties |Hello 이벤트의 속성입니다. |

TooEvent 허브 스트리밍을 지원 되는 모든 리소스 공급자의 목록을 볼 수 있습니다 [여기](monitoring-overview-of-diagnostic-logs.md)합니다.

## <a name="stream-data-from-compute-resources"></a>계산 리소스의 스트림 데이터
Windows Azure 진단 에이전트가 hello를 사용 하 여 계산 리소스에서 진단 로그를 스트리밍할 수 있습니다. [이 문서를 참조](../event-hubs/event-hubs-streaming-azure-diags-data.md) 방법에 대 한 tooset 위쪽에 해당 합니다.

## <a name="next-steps"></a>다음 단계
* [Azure 진단 로그에 대해 자세히 알아보기](monitoring-overview-of-diagnostic-logs.md)
* [이벤트 허브 시작](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

