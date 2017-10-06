---
title: "역할, 권한 및 보안 Azure 모니터로 aaaGet 시작 | Microsoft Docs"
description: "Toouse Azure 모니터의 기본 제공 역할 및 사용 권한 toorestrict toomonitoring 리소스에 액세스할 방법에 대해 알아봅니다."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 2686e53b-72f0-4312-bcd3-3dc1b4a9b912
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: johnkem
ms.openlocfilehash: 44fdf2a697050309480dfc164ebab51445b19bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-roles-permissions-and-security-with-azure-monitor"></a>Azure Monitor에서의 역할, 권한 및 보안 시작
많은 팀 필요 toostrictly toomonitoring 데이터 액세스 및 설정을 제어 합니다. 예를 들어 관리 되는 서비스 공급자를 사용할 경우 toogrant tooonly 자신의 능력 toocreate 제한 하면서 모니터링 데이터 액세스 권한을 (기술 지원 엔지니어, devops 엔지니어) 모니터링에 작업 하는 팀 멤버가 있는 경우 수정, 또는 리소스를 삭제 합니다. 이 문서에서는 tooquickly 기본 제공 모니터링 RBAC 역할 tooa 사용자가 Azure에서 적용 또는 고유한 사용자 지정 역할 모니터링 제한 된 권한이 필요로 하는 사용자에 대 한 빌드 방법을 보여 줍니다. Azure 모니터와 관련 된 리소스에 대 한 보안 고려 사항에 설명 합니다 하며 포함 방법 toohello 데이터 액세스를 제한할 수 있습니다.

## <a name="built-in-monitoring-roles"></a>기본 제공 모니터링 역할
Azure 모니터의 기본 제공 역할이 계속 하는 것을 사용 하도록 설정 하는 동안 구독에서 설계 된 toohelp 제한 액세스 tooresources tooobtain 인프라를 모니터링 하는 일을 담당 하 고 필요한 hello 데이터를 구성 합니다. Azure Monitor는 Monitoring Reader와Monitoring Contributor 등, 바로 사용할 수 있는 2가지 역할을 제공합니다.

### <a name="monitoring-reader"></a>Monitoring Reader
Hello 모니터링 읽기 역할에 할당 된 사용자 구독에서 모든 모니터링 데이터를 볼 수 있지만 모든 리소스를 수정할 하거나 모든 설정이 관련된 toomonitoring 리소스를 편집할 수 없습니다. 이 역할은 toobe 할 필요는 지원 또는 작업 엔지니어 같은 조직의 사용자에 게 적합 합니다.

* Hello 포털에서 모니터링 대시보드를 확인 하 고 자신의 개인 모니터링 대시보드를 만듭니다.
* Hello를 사용 하 여 메트릭에 대 한 쿼리 [Azure 모니터 REST API](https://msdn.microsoft.com/library/azure/dn931930.aspx), [PowerShell cmdlet](insights-powershell-samples.md), 또는 [플랫폼 간 CLI](insights-cli-samples.md)합니다.
* 쿼리 hello hello 포털, Azure 모니터 REST API, PowerShell cmdlet 또는 플랫폼 간 CLI를 사용 하 여 작업 로그입니다.
* 보기 hello [진단 설정을](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) 리소스에 대 한 합니다.
* 보기 hello [프로필 로그](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) 구독에 대 한 합니다.
* 자동 크기 조정 설정을 봅니다.
* 경고 활동 및 설정을 봅니다.
* Application Insights 데이터에 액세스하고 AI Analytics에서 데이터를 봅니다.
* Hello 작업 영역에 대 한 사용 현황 데이터를 포함 한 로그 분석 (OMS) 작업 영역 데이터를 검색 합니다.
* Log Analytics(OMS) 관리 그룹을 봅니다.
* Hello 로그 분석 (OMS) 검색 스키마를 검색 합니다.
* Log Analytics(OMS) 인텔리전스 팩을 나열합니다.
* Log Analytics(OMS) 저장된 검색을 검색 및 실행합니다.
* Hello 로그 분석 (OMS) 저장소 구성을 검색 합니다.

> [!NOTE]
> 이 역할에서 저장소 계정에 저장 또는 스트리밍된 tooan 이벤트 허브 된 toolog 데이터 읽기 액세스를 부여 하지 않습니다. [아래 참조](#security-considerations-for-monitoring-data) toothese 리소스에 액세스를 구성 하는 방법에 대 한 정보에 대 한 합니다.
> 
> 

### <a name="monitoring-contributor"></a>Monitoring Contributor
할당 된 사람 hello 모니터링 참가자 역할 수는 구독에서 모든 모니터링 데이터를 볼 만들기는 또는 모니터링 설정을 수정 하지만 다른 모든 리소스를 수정할 수 없습니다. 이 역할 hello 모니터링 읽기 역할의 상위 집합 인지 그리고 조직 모니터링 팀 또는 또한 toohello 필요한 사용 권한은 위의 toobe 수 하는 관리 되는 서비스 공급자의 여러 멤버에 대 한 적절 한:

* 공유 대시보드로 모니터링 대시보드를 게시합니다.
* 리소스에 대한 [진단 설정](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) 을 구성합니다.*
* 집합 hello [프로필 로그](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) 는 subscription.*에 대 한
* 경고 활동 및 설정을 구성합니다.
* Application Insights 웹 테스트 및 구성 요소를 만듭니다.
* Log Analytics(OMS) 작업 공간 공유 키를 나열합니다.
* Log Analytics(OMS) 인텔리전스 팩을 사용하거나 사용하지 않도록 설정합니다.
* Log Analytics(OMS) 저장된 검색을 만들고 삭제합니다.
* 만들고 hello 로그 분석 (OMS) 저장소 구성을 삭제 합니다.

* 또한 별도로 사용자 hello 대상 리소스 (저장소 계정 또는 이벤트 허브 네임 스페이스) tooset 로그 프로필 또는 진단 설정에 대 한 Listkey 권한이 부여 되어야 합니다.

> [!NOTE]
> 이 역할에서 저장소 계정에 저장 또는 스트리밍된 tooan 이벤트 허브 된 toolog 데이터 읽기 액세스를 부여 하지 않습니다. [아래 참조](#security-considerations-for-monitoring-data) toothese 리소스에 액세스를 구성 하는 방법에 대 한 정보에 대 한 합니다.
> 
> 

## <a name="monitoring-permissions-and-custom-rbac-roles"></a>권한 및 사용자 지정 RBAC 역할 모니터링
기본 제공 역할 위에 hello 팀의 정확한 요구 hello 없으면 다음을 할 수 있습니다 [사용자 지정 RBAC 역할](../active-directory/role-based-access-control-custom-roles.md) 보다 세부적인 권한을 사용 합니다. 일반적인 Azure 모니터 RBAC 작업과 해당 설명을 보려면 hello는 다음과 같습니다.

| 작업 | 설명 |
| --- | --- |
| Microsoft.Insights/AlertRules/[Read, Write, Delete] |경고 규칙 읽기/쓰기/삭제 |
| Microsoft.Insights/AlertRules/Incidents/Read |경고 규칙에 대 한 인시던트 (트리거된 hello 경고 규칙의 기록)를 나열 합니다. 이 toohello 포털만을 적용 됩니다. |
| Microsoft.Insights/AutoscaleSettings/[Read, Write, Delete] |자동 크기 조정 설정 읽기/쓰기/삭제 |
| Microsoft.Insights/DiagnosticSettings/[Read, Write, Delete] |진단 설정 읽기/쓰기/삭제 |
| Microsoft.Insights/eventtypes/digestevents/Read |이 권한은 tooActivity 로그 hello 포털을 통해 액세스 해야 하는 사용자에 대 한 필요한입니다. |
| Microsoft.Insights/eventtypes/values/Read |구독에서 활동 로그 이벤트(관리 이벤트)를 나열합니다. 이 권한은 해당 tooboth 프로그래밍 및 포털 액세스 toohello 활동 로그입니다. |
| Microsoft.Insights/LogDefinitions/Read |이 권한은 tooActivity 로그 hello 포털을 통해 액세스 해야 하는 사용자에 대 한 필요한입니다. |
| Microsoft.Insights/MetricDefinitions/Read |메트릭 정의(리소스에 사용 가능한 메트릭 형식 목록)를 읽습니다. |
| Microsoft.Insights/Metrics/Read |리소스에 대한 메트릭을 읽습니다. |

> [!NOTE]
> 액세스 tooalerts, 진단 설정 및 리소스에 대 한 메트릭을 해당 hello 사용자에 대 한 읽기 액세스 toohello 리소스 종류 및 해당 리소스의 범위를 필요 합니다. ("쓰기")을 만드는 아카이브 tooa 저장소 계정 또는 스트림 tooevent 허브 hello 사용자 tooalso 필요 하다는 진단 설정 또는 로그 프로필 Listkey에 권한이 hello 대상 리소스 합니다.
> 
> 

예를 들어 테이블 위에 hello를 사용 하 여 만들 수 있습니다는 사용자 지정 RBAC 역할 판독기에 대 한"활동 로그" 다음과 같이:

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Activity Log Reader"
$role.Description = "Can view activity logs."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Insights/eventtypes/*")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription")
New-AzureRmRoleDefinition -Role $role 
```

## <a name="security-considerations-for-monitoring-data"></a>모니터링 데이터에 대한 보안 고려 사항
모니터링 데이터, 특히 로그 파일에는 IP 주소나 사용자 이름 같은 중요 정보가 포함될 수 있습니다. Azure의 모니터링 데이터는 다음 3가지 기본 형태로 제공됩니다.

1. Azure 구독에서 모든 제어 평면 작업을 설명 하는 활동 로그 번호입니다.
2. 진단 로그. 리소스가 내보낸 로그입니다.
3. 메트릭. 리소스가 내보낸 항목입니다.

이러한 데이터 형식의 세 가지 모두 저장소 계정에 저장할 수 있습니다 또는 범용 Azure 리소스는 둘 다 허브 tooEvent 스트리밍. 범용 리소스이기 때문에 이 항목의 만들기, 삭제 및 액세스는 권한이 필요한 작업이며 일반적으로 관리자에게 예약됩니다. 모니터링 관련 리소스 tooprevent 오용 사례 hello를 사용 하는 하는 것이 좋습니다.

* 모니터링 데이터에는 단일 전용 저장소 계정을 사용합니다. Tooseparate 모니터링 데이터를 여러 저장소 계정에 필요한 경우 모니터링 간의 저장소 계정 사용을 공유 하지 않습니다 이며이 아닌 모니터링 데이터만 toomonitoring 데이터 (예: 액세스 해야 하는 사용자를 제공할 실수로 수 있습니다. 제 3 자 SIEM) toonon 모니터링 데이터에 액세스 합니다.
* 위와 같은 이유로 hello에 대 한 모든 진단 설정에서 단일, 전용 서비스 버스 또는 이벤트 허브 네임 스페이스를 사용 합니다.
* 별도 리소스 그룹에 보관 하면 액세스 toomonitoring와 관련 된 저장소 계정 또는 이벤트 허브를 제한 하 고 [범위를 사용 하 여](../active-directory/role-based-access-control-what-is.md#basics-of-access-management-in-azure) 모니터링 역할 toolimit 액세스할 tooonly 해당 리소스 그룹입니다.
* 사용자에만 toomonitoring 데이터에 액세스 해야 하는 경우 저장소 계정 또는 구독 범위에서 이벤트 허브에 대 한 hello Listkey 권한을 부여 안 됩니다. (있는 경우 전용된 모니터링 리소스 그룹) 리소스 또는 리소스 그룹에 이러한 사용 권한을 toohello 사용자를 대신 제공 범위입니다.

### <a name="limiting-access-toomonitoring-related-storage-accounts"></a>Toomonitoring와 관련 된 저장소 계정 액세스를 제한합니다.
사용자 또는 응용 프로그램 저장소 계정에 toomonitoring 데이터에 액세스 해야 하는 경우 수행 해야 [계정 SAS를 생성할](https://msdn.microsoft.com/library/azure/mt584140.aspx) tooblob 저장소 서비스 수준 읽기 전용 액세스를 사용 하 여 모니터링 데이터를 포함 하는 hello 저장소 계정에 있습니다. PowerShell에서는 다음과 같습니다.

```powershell
$context = New-AzureStorageContext -ConnectionString "[connection string for your monitoring Storage Account]"
$token = New-AzureStorageAccountSASToken -ResourceType Service -Service Blob -Permission "rl" -Context $context
```

그런 다음 해당 저장소 계정에서 tooread 필요한 hello 토큰 toohello 엔터티를 제공할 수 있습니다 및 나열 하 고 해당 저장소 계정에서 모든 blob에서 읽을 수 있습니다.

또는이 사용 권한은 RBAC와 toocontrol 해야 할 경우 해당 엔터티 hello 해당 특정 저장소 계정에서 Microsoft.Storage/storageAccounts/listkeys/action 권한을 부여할 수 있습니다. 이 작업이 toobe 수 tooset 진단 설정 또는 로그 프로필 tooarchive tooa 저장소 계정에 게 필요 합니다. 예를 들어 다음 사용자 또는 한 저장소 계정에서 tooread만 하면 되는 응용 프로그램에 대 한 사용자 지정 RBAC 역할 hello를 만들 수 있습니다.

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Monitoring Storage Account Reader"
$role.Description = "Can get hello storage account keys for a monitoring storage account."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/storageAccounts/listkeys/action")
$role.Actions.Add("Microsoft.Storage/storageAccounts/Read")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/myMonitoringStorageAccount")
New-AzureRmRoleDefinition -Role $role 
```

> [!WARNING]
> hello Listkey 권한 hello 사용자 toolist hello 기본 및 보조 저장소 계정 키를 수 있습니다. 이러한 키를 사용자에 게 부여 hello 서명 된 모든 사용 권한 (읽기, 쓰기, blob 만들기, 삭제 blob 등)에 모든 해당 저장소 계정에서 서비스 (blob, 큐, 테이블, 파일)을 서명 합니다. 가능한 경우 위에서 설명한 계정 SAS를 사용하는 것이 좋습니다.
> 
> 

### <a name="limiting-access-toomonitoring-related-event-hubs"></a>액세스 toomonitoring 관련 이벤트 허브를 제한합니다.
이벤트 허브는 유사한 패턴을 줄 수 있지만 toocreate 전용된 수신 권한 부여 규칙을 먼저 합니다. Toolisten toomonitoring 관련 이벤트 허브는 toogrant access tooan 응용 프로그램을 사용 하도록 하려는 경우 다음 hello지 않습니다.

1. Listen 클레임만을 사용 하 여 모니터링 데이터를 스트리밍에 대 한 생성 된 hello 이벤트 허브에서 공유 액세스 정책을 만듭니다. Hello 포털에서이 작업을 수행할 수 있습니다. 예를 들어, 이 정책을 “monitoringReadOnly”라고 할 수 있습니다. 가능 하면 toogive hello 다음 단계를 건너뛰고 toohello 소비자 키 직접를 사용 합니다.
2. Hello 소비자 toobe 수 tooget hello 키 임시 경우, 해당 이벤트 허브에 대 한 hello 사용자 hello Listkey 작업 권한을 부여 합니다. 사용자에 게 필요한 toobe 수 tooset 진단 설정 또는 프로필 toostream tooevent 허브 로그에 필요한 이기도 합니다. 예를 들어, RBAC 규칙을 만들 수 있습니다.
   
   ```powershell
   $role = Get-AzureRmRoleDefinition "Reader"
   $role.Id = $null
   $role.Name = "Monitoring Event Hub Listener"
   $role.Description = "Can get hello key toolisten tooan event hub streaming monitoring data."
   $role.Actions.Clear()
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/authorizationrules/listkeys/action")
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/Read")
   $role.AssignableScopes.Clear()
   $role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.ServiceBus/namespaces/mySBNameSpace")
   New-AzureRmRoleDefinition -Role $role 
   ```

## <a name="next-steps"></a>다음 단계
* [Resource Manager의 RBAC 및 권한에 대해 읽기](../active-directory/role-based-access-control-what-is.md)
* [Azure에서 모니터링 읽기 hello 개요](monitoring-overview.md)

