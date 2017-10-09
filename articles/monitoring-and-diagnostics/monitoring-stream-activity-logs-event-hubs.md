---
title: "aaaStream hello Azure 활동 로그 tooEvent 허브 | Microsoft Docs"
description: "Toostream Azure 활동 로그 tooEvent 허브 hello 하는 방법에 대해 알아봅니다."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ec4c2d2c-8907-484f-a910-712403a06829
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/06/2017
ms.author: johnkem
ms.openlocfilehash: 336f92771b9d4379ad9dbcadc6997dfae7fae7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-hello-azure-activity-log-tooevent-hubs"></a>Hello Azure 활동 로그 tooEvent 허브 스트림
hello [ **Azure 활동 로그** ](monitoring-overview-activity-logs.md) 거의 실시간으로 tooany hello 기본 제공 "내보내기" 옵션을 사용 하 여 hello 포털에서 응용 프로그램에 스트리밍할 수 또는 사용 하 여 hello 통해 로그 프로필에서 서비스 버스 규칙 Id를 환영 Azure PowerShell Cmdlet 또는 Azure CLI 합니다.

## <a name="what-you-can-do-with-hello-activity-log-and-event-hubs"></a>Hello 활동 로그 및 이벤트 허브 사용 하 여 수행할 수 있는 작업
다음 몇 가지 방법으로 hello 스트리밍 hello 활동 로그에 대 한 기능을 사용할 수 있습니다.

* **Toothird 자 로깅 및 원격 분석 시스템 스트림** – 시간이 지남에 따라 이벤트 허브 스트리밍 됩니다 hello 메커니즘 toopipe 활동 로그 제 3 자 Siem에 해지고 분석 솔루션을 기록 합니다.
* **빌드 사용자 지정 원격 분석 및 로깅 플랫폼** 는 hello 수집 건물 하나, 확장성이 높은 hello 게시-구독에 대해 생각 방금 이벤트 허브의 특성 tooflexibly 수 있습니다. 또는 사용자가 작성 한 원격 분석 플랫폼을 이미 있는 경우- 활동 로그 합니다. [세계적인 규모 원격 분석 플랫폼 여기에서 Dan Rosanova 가이드 toousing 이벤트 허브를 참조 하십시오.](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-hello-activity-log"></a>Hello 활동 로그의 스트리밍을 사용합니다
프로그래밍 방식으로 또는 hello 포털을 통해 hello 활동 로그의 스트리밍을 사용할 수 있습니다. 서비스 버스 Namespace와 해당 네임 스페이스에 대 한 공유 액세스 정책을 선택 어떤 방법을 사용 하 고 hello 첫 번째 새 활동 로그 이벤트가 발생 하면 해당 네임 스페이스에서 이벤트 허브 만들어집니다. 서비스 버스 Namespace가 없는 경우 먼저 toocreate 하나 필요 합니다. 활동 로그 이벤트 toothis 서비스 버스 Namespace을 이전에 스트리밍할 hello 이전에 만든 이벤트 허브를 다시 사용 됩니다. hello 공유 액세스 정책 hello 스트리밍 메커니즘의 hello 권한을 정의 합니다. 오늘날 필요 tooan 이벤트 허브를 스트리밍 **관리**, **보낼**, 및 **수신** 사용 권한. 작성 하거나 서비스 버스 Namespace에 대 한 hello "구성" 탭에서 hello 클래식 포털에서 서비스 버스 Namespace 공유 액세스 정책을 수정할 수 있습니다. tooupdate 활동 로그 로그 프로필 tooinclude 스트리밍 hello hello 변경 내용을 hello 사용자는 해당 서비스 버스 권한 부여 규칙에서 hello ListKey 권한이 있어야 합니다.

hello 서비스 버스 또는 이벤트 허브 네임 스페이스가 없는 toobe hello hello 설정을 구성 하는 hello 사용자에 게 적합 한 RBAC 액세스 tooboth 구독으로 로그를 내보내는 hello 구독과 동일한 구독 합니다.

### <a name="via-azure-portal"></a>Azure 포털을 통해
1. Toohello 이동 **활동 로그** 블레이드 hello 메뉴를 사용 하 여 hello hello 포털의 왼쪽에 있습니다.
   
    ![포털에서 로그 tooActivity 이동](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. Hello 클릭 **내보내기** hello hello 블레이드 위쪽에 단추입니다.
   
    ![포털에서 내보내기 단추](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. 표시 되는 hello 블레이드에서 원하는 toostream 이벤트 및 이러한 이벤트 스트리밍에 대 한 생성 하는 이벤트 허브 toobe 시겠습니까 hello 서비스 버스 Namespace hello 영역을 선택할 수 있습니다.
   
    ![활동 로그 내보내기 블레이드](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. 클릭 **저장** toosave 이러한 설정 합니다. hello 설정이 적용된 tooyour 구독을 즉시 수는 있습니다.

### <a name="via-powershell-cmdlets"></a>PowerShell Cmdlet을 통해
로그 프로필에 이미 있으면 먼저 tooremove 해당 프로필입니다.

1. 사용 하 여 `Get-AzureRmLogProfile` tooidentify 로그 프로필이 존재 하는 경우
2. 이 경우 사용 하 여 `Remove-AzureRmLogProfile` tooremove 것입니다.
3. 사용 하 여 `Set-AzureRmLogProfile` toocreate 프로필:

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

이 형식 문자열 hello 서비스 버스 규칙 ID: {서비스 버스 리소스 ID} /authorizationrules/ {키 이름} 예: 

### <a name="via-azure-cli"></a>Azure CLI를 통해
로그 프로필에 이미 있으면 먼저 tooremove 해당 프로필입니다.

1. 사용 하 여 `azure insights logprofile list` tooidentify 로그 프로필이 존재 하는 경우
2. 이 경우 사용 하 여 `azure insights logprofile delete` tooremove 것입니다.
3. 사용 하 여 `azure insights logprofile add` toocreate 프로필:

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

hello 서비스 버스 규칙 ID는이 형식 문자열: `{service bus resource ID}/authorizationrules/{key name}`합니다.

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a>이벤트 허브에서 로그 데이터를 hello를 사용 어떻게 합니까?
[활동 로그 hello에 대 한 hello 스키마는 여기](monitoring-overview-activity-logs.md)합니다. 각 이벤트는 "레코드"라는 JSON Blob 배열입니다.

## <a name="next-steps"></a>다음 단계
* [보관 hello 활동 로그 tooa 저장소 계정](monitoring-archive-activity-log.md)
* [Hello Azure 활동 로그 읽기 hello 개요](monitoring-overview-activity-logs.md)
* [활동 로그 이벤트를 기반으로 경고 설정](insights-auditlog-to-webhook-email.md)

