---
title: "Azure 진단 로그 aaaArchive | Microsoft Docs"
description: "어떻게 tooarchive 프로그램 Azure 로그 진단 로그를 저장소 계정에 대 한 장기 보존을 위해에 대해 알아봅니다."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 3a55c73f-2ef3-45f3-8956-bcf9c0cb7e05
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: bc9edbd3a649023a728b7fe77130dba2b6e6370d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="archive-azure-diagnostic-logs"></a>Azure 진단 로그 보관
CLI hello Azure 포털, PowerShell Cmdlet을 사용 하거나 REST API tooarchive 하는 방법 알아보겠습니다이 문서에서는 프로그램 [Azure 진단 로그](monitoring-overview-of-diagnostic-logs.md) 저장소 계정에 있습니다. 이 옵션은 감사, 정적 분석 또는 백업에 대 한 선택적 보존 정책을 사용 하 여 진단 기록 tooretain 원하는 경우에 유용 합니다. 저장소 계정 hello이 없는 toobe hello hello 설정을 구성 하는 hello 사용자에 게 적합 한 RBAC 액세스 tooboth 구독으로 로그를 내보내는 hello 리소스와 같은 구독 합니다.

## <a name="prerequisites"></a>필수 조건
시작 하기 전에 해야 너무[저장소 계정 만들기](../storage/storage-create-storage-account.md) toowhich 진단 로그를 보관할 수 있습니다. Toomonitoring 데이터 액세스를 더 잘 제어할 수 있도록에 저장 된 다른, 비 모니터링 데이터가 있는 기존 저장소 계정을 사용 하지 않는 것이 좋습니다. 그러나 또한 보관 하는 경우 작업 로그 및 진단 메트릭은 tooa 저장소 계정, 사항이 감지 toouse 해당 저장소 계정에 진단 로그에 tookeep 모든 모니터링 데이터를 중앙 위치에. hello 사용 하는 저장소 계정에는 일반적인 용도의 스토리지 계정, blob 저장소 계정 이어야 합니다.

## <a name="diagnostic-settings"></a>진단 설정
tooarchive 아래 hello 방법 중 하나를 사용 하 여 진단 로그, 설정한 한 **진단 설정** 특정 리소스에 대 한 합니다. 메트릭 데이터 전송 (저장소 계정, 이벤트 허브 네임 스페이스 또는 로그 분석) tooa 대상 및 리소스에 대 한 진단 설정을 hello 범주의 로그를 정의 합니다. 또한 각 로그 범주와 저장소 계정에 저장 된 메트릭 데이터의 이벤트에 대 한 hello 보존 정책 (tooretain 일 수)을 정의 합니다. Toozero 보존 정책이 설정 되어 해당 로그 범주에 대 한 이벤트는 무기한 저장 (즉, toosay 영원히). 그렇지 않은 경우 보존 정책은 1에서 2147483647 사이의 숫자일 수 있습니다. [진단 설정에 대한 자세한 내용은 여기에서 확인할 수 있습니다](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings). 보존 정책이 적용 된 매일 많으면 hello 때 종료 시간 (UTC)는 이제 hello 보존 정책을 불가능 hello 날짜 로부터 기록 되므로 삭제 됩니다. 예를 들어 1 일의 보존 정책의 설치한 경우 hello 하루의 오늘 hello 시작 부분에 hello hello 이틀 전에서에서 로그 삭제 됩니다.

## <a name="archive-diagnostic-logs-using-hello-portal"></a>Hello 포털을 사용 하 여 진단 로그를 보관
1. Hello 포털 tooAzure 모니터를 탐색 하 고 클릭 **진단 설정**

    ![Azure Monitor의 모니터링 섹션](media/monitoring-archive-diagnostic-logs/diagnostic-settings-blade.png)

2. 필요에 따라 리소스 그룹 또는 리소스 유형으로 hello 목록을 필터링 하려는 진단 설정 tooset hello 리소스 클릭 합니다.

3. 선택한 hello 리소스에 설정이 없는 있으면 증명된 toocreate 설정 됩니다. “진단 켜기”를 클릭합니다.

   ![진단 설정 추가 - 기존 설정 없음](media/monitoring-archive-diagnostic-logs/diagnostic-settings-none.png)

   Hello 리소스에 대 한 기존 설정을 없을 경우이 리소스에서 이미 구성 되어 있는 설정 목록이 표시 됩니다. “진단 설정 추가”를 클릭합니다.

   ![진단 설정 추가 - 기존 설정](media/monitoring-archive-diagnostic-logs/diagnostic-settings-multiple.png)

3. 사용자 설정 이름을 지정 하 고 hello 확인란에 대 한 **tooStorage 계정 내보내기**, 저장소 계정을 선택 합니다. Hello를 사용 하 여 다양 한 일 tooretain 이러한 로그를 필요에 따라 설정 **보존 (일)** 슬라이더 합니다. 0 일의 보존 hello 로그를 무기한으로 저장 합니다.
   
   ![진단 설정 추가 - 기존 설정](media/monitoring-archive-diagnostic-logs/diagnostic-settings-configure.png)
    
4. **Save**를 클릭합니다.

몇 분 후 hello 새 설정이이 리소스에 대 한 설정의 목록에 표시 되며 진단 로그 보관 된 toothat 저장소 계정으로 새 이벤트 데이터를 생성 합니다.

## <a name="archive-diagnostic-logs-via-azure-powershell"></a>Azure PowerShell을 통한 진단 로그 보관
```
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg -StorageAccountId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Categories networksecuritygroupevent,networksecuritygrouprulecounter -Enabled $true -RetentionEnabled $true -RetentionInDays 90
```

| 속성 | 필수 | 설명 |
| --- | --- | --- |
| ResourceId |예 |진단 설정을 tooset 원하는 hello 리소스의 리소스 ID입니다. |
| StorageAccountId |아니요 |Hello 저장소 계정 toowhich 진단 로그의 리소스 ID는 저장 해야 합니다. |
| 범주 |아니요 |쉼표로 구분 된 목록 로그 범주 tooenable입니다. |
| 사용 |예 |이 리소스에 대한 진단 활성화 여부를 나타내는 부울입니다. |
| RetentionEnabled |아니요 |이 리소스에 대한 보존 정책 활성화 여부를 나타내는 부울입니다. |
| RetentionInDays |아니요 |이벤트를 유지해야 하는 일 수는 1에서 2147483647 사이입니다. 값이 0 hello 로그를 무기한으로 저장 합니다. |

## <a name="archive-diagnostic-logs-via-hello-cross-platform-cli"></a>플랫폼 간 CLI hello 통해 진단 로그 보관
```
azure insights diagnostic set --resourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg --storageId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage –categories networksecuritygroupevent,networksecuritygrouprulecounter --enabled true
```

| 속성 | 필수 | 설명 |
| --- | --- | --- |
| ResourceId |예 |진단 설정을 tooset 원하는 hello 리소스의 리소스 ID입니다. |
| storageId |아니요 |Hello 저장소 계정 toowhich 진단 로그의 리소스 ID는 저장 해야 합니다. |
| 범주 |아니요 |쉼표로 구분 된 목록 로그 범주 tooenable입니다. |
| 사용 |예 |이 리소스에 대한 진단 활성화 여부를 나타내는 부울입니다. |

## <a name="archive-diagnostic-logs-via-hello-rest-api"></a>Hello REST API를 통해 진단 로그 보관
[이 문서를 참조 하십시오.](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings) hello Azure 모니터 REST API를 사용 하 여 진단 설정을 설정 하는 방법에 대 한 내용은 합니다.

## <a name="schema-of-diagnostic-logs-in-hello-storage-account"></a>Hello 저장소 계정에 진단 로그의 스키마
한 아카이브를 설정한 후 사용 하도록 설정한 hello 로그 범주 중 하나에서 이벤트가 발생 하는 즉시 hello 저장소 계정에서 저장소 컨테이너가 만들어집니다. hello 컨테이너 내 blob hello 진단 로그에서 동일한 형식 hello 및 hello 활동 로그를 따릅니다. 이러한 blob의 hello 구조는.

> insights-logs-{log category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/RESOURCEGROUPS/{resource group name}/PROVIDERS/{resource provider name}/{resource type}/{resource name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
> 
> 

또는 더 간단하게

> insights-logs-{log category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
> 
> 

예를 들어 Blob 이름은 다음과 같습니다.

> insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json
> 
> 

각 PT1H.json blob hello blob URL에 지정 된 hello 시간 이내에 발생 한 이벤트의 JSON blob에 포함 (예를 들어, h = 12). 현재 시간 hello 하는 동안 이벤트는 나타나는 순서 대로 추가 toohello PT1H.json 파일입니다. 분 값 hello (m 00 =)는 항상 00, 이후 진단 로그 이벤트 1 시간 마다 각 blob으로 나뉩니다.

Hello PT1H.json 파일 내에서 각 이벤트는이 형식에 따라 레코드"hello" 배열에 저장 됩니다.

```
{
    "records": [
        {
            "time": "2016-07-01T00:00:37.2040000Z",
            "systemId": "46cdbb41-cb9c-4f3d-a5b4-1d458d827ff1",
            "category": "NetworkSecurityGroupRuleCounter",
            "resourceId": "/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/TESTNSG",
            "operationName": "NetworkSecurityGroupCounters",
            "properties": {
                "vnetResourceGuid": "{12345678-9012-3456-7890-123456789012}",
                "subnetPrefix": "10.3.0.0/24",
                "macAddress": "000123456789",
                "ruleName": "/subscriptions/ s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg/securityRules/default-allow-rdp",
                "direction": "In",
                "type": "allow",
                "matchedConnections": 1988
            }
        }
    ]
}
```

| 요소 이름 | 설명 |
| --- | --- |
| 실시간 |Hello Azure 서비스 처리 hello에서 hello 이벤트가 생성 된 시점의 타임 스탬프는 해당 하는 hello 이벤트를 요청 합니다. |
| resourceId |Hello의 리소스 ID 리소스를 저하 됩니다. |
| operationName |Hello 작업의 이름입니다. |
| 카테고리 |Hello 이벤트의 로그 범주입니다. |
| properties |설정 `<Key, Value>` hello 이벤트의 hello 세부 정보를 설명 하는 쌍 (예: 사전). |

> [!NOTE]
> hello 속성 및 해당 속성의 사용 현황 hello 리소스에 따라 달라질 수 있습니다.
> 
> 

## <a name="next-steps"></a>다음 단계
* [분석을 위한 Blob 다운로드](../storage/storage-dotnet-how-to-use-blobs.md)
* [스트림 진단 tooan 이벤트 허브 네임 스페이스를 기록합니다.](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [진단 로그에 대해 자세히 알아보기](monitoring-overview-of-diagnostic-logs.md)
