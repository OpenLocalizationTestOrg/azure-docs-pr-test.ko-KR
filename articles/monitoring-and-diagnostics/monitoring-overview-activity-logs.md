---
title: "hello Azure 활동 로그의 aaaOverview | Microsoft Docs"
description: "Azure 활동 로그는 어떤 hello 및 방법을 사용할 수 있습니다 Azure 구독 내에서 발생 하는 toounderstand 이벤트에 알아봅니다."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c274782f-039d-4c28-9ddb-f89ce21052c7
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: johnkem
ms.openlocfilehash: cba79b7f6dc0833ef588382e763761fd77d43307
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-subscription-activity-with-hello-azure-activity-log"></a>Azure 활동 로그 hello로 구독 작업을 모니터링 합니다.
hello **Azure 활동 로그** Azure에서 발생 한 구독 수준 이벤트에 대 한 정보를 제공 하는 구독 로그입니다. 서비스 상태 이벤트에 운영 데이터 tooupdates Azure 리소스 관리자에서에서 데이터의 범위를 포함 합니다. hello 활동 로그는 이전에 구독에 대 한 hello 관리 범주 보고서 제어 평면 이벤트 이후 "감사 로그" 또는 "작업 로그"로 알려졌습니다. Hello 활동 로그를 사용 하 여 hello를 확인할 수 ' 부분, who, 시기 및 ' hello 구독의 리소스에에서 대해 수행 하는 작업 (PUT, POST, DELETE) 쓰기에 대 한 합니다. Hello 작업 및 기타 관련 속성의 hello 상태를 이해할 수 있습니다. 읽기 (GET) 작업 또는 클래식 hello를 사용 하는 리소스에 대 한 작업 hello 활동 로그를 포함 하지 않는 / "RDFE" 모델입니다.

![활동 로그 및 다른 종류의 로그 ](./media/monitoring-overview-activity-logs/Activity_Log_vs_other_logs_v5.png)

그림 1: 활동 로그 및 다른 종류의 로그

hello 활동 로그에서 다릅니다 [진단 로그](monitoring-overview-of-diagnostic-logs.md)합니다. 활동 로그 hello 작업 hello (hello "제어 평면") 외부에서 리소스에 대 한 데이터를 제공합니다. 진단 로그 리소스에 의해 발생 하 고 해당 리소스 ("데이터 평면" hello)의 hello 작업에 대 한 정보를 제공 합니다.

Azure 포털 hello CLI, PowerShell cmdlet 사용 하 여 활동 로그에서 이벤트를 검색할 수 있습니다 및 Azure 모니터 REST API입니다.


> [!WARNING]
> Azure 활동 로그 hello은 주로 Azure 리소스 관리자에서 발생 하는 활동 됩니다. Hello 클래식/RDFE 모델을 사용 하 여 리소스를 추적 하지 않습니다. 일부 클래식 리소스 유형(예: Microsoft.ClassicCompute)에는 Azure Resource Manager의 프록시 리소스 공급자가 있습니다. 클래식 리소스 종류 Azure 리소스 관리자를 통해 이러한 프록시 리소스 공급자를 사용 하 여 상호 작용 하는 경우 hello 작업 hello 활동 로그에에서 나타납니다. 와 상호 작용 하는 경우 클래식 리소스 hello 클래식 포털에 입력 하거나 그렇지 않으면 hello Azure 리소스 관리자 프록시 외부에서 작업을 수행할 때만 기록 됩니다 hello 작업 로그에에서 합니다. hello 작업 로그는 hello 클래식 포털에만 액세스할 수 있습니다.
>
>

다음 비디오 소개 hello 활동 로그 보기 번호입니다.
> [!VIDEO https://channel9.msdn.com/Blogs/Seth-Juarez/Logs-John-Kemnetz/player]
> 
>

## <a name="categories-in-hello-activity-log"></a>Hello 활동 로그의 범주
활동 로그 hello 여러 종류의 데이터를 포함합니다. 자세한 내용은 hello schemata 이러한 범주에 대 한 [이 문서를 참조](monitoring-activity-log-schema.md)합니다. 내용은 다음과 같습니다.
* **관리** -모든 hello 레코드를 포함 하는이 범주 만들기, 업데이트, 삭제 및 작업 작업이 리소스 관리자를 통해 수행 합니다. 이 범주에 표시 되는 이벤트 유형을 포함 하는 hello의 예로 "가상 컴퓨터 만들기" 및 "삭제" 네트워크 보안 그룹 사용자가 수행한 동작 또는 리소스 관리자를 사용 하 여 응용 프로그램은 특정 리소스 종류에 대 한 작업으로 모델링 됩니다. Hello 작업 유형이 hello 시작과 성공의 hello 레코드를 삭제 또는 동작을 작성 하거나 hello 관리 범주에 해당 작업의 실패 기록 됩니다. 구독에 변경 내용을 toorole 기반 액세스 제어를 관리 범주 hello 포함 됩니다.
* **서비스 상태** -이 범주에는 Azure에서 발생 한 모든 서비스 상태 문제의 hello 레코드에 포함 합니다. Hello 유형의이 범주에 표시 되는 이벤트의 예로 "미국 동부에서 SQL Azure 가동 중지 시간이 발생 합니다." 서비스 상태 이벤트를 가져오는 다섯 가지 종류의: 필요한 작업, 복구 지원, 인시던트, 유지 관리, 정보 또는 보안을 hello 이벤트에 의해 영향을 받게 hello 구독에는 리소스를 사용할 경우에 표시 하 고 있습니다.
* **경고** -이 범주에 Azure 경고의 모든 활성화의 hello 레코드를 포함 합니다. Hello 유형의이 범주에 표시 되는 이벤트의 예로 "CPU (%)에서 myVM은 되었으며 80 hello에 대 한 지난 5 분" 다수의 Azure 시스템에서 경고 개념이 사용됩니다. 일종의 규칙을 정의하여 조건이 해당 규칙과 일치하면 알림을 수신할 수 있습니다. 될 때마다 지원 되는 Azure 경고 유형 '활성화,' 또는 hello 조건이 충족된 toogenerate 알림을, hello 정품 인증에 대 한 기록을 hello 활동 로그의 toothis 범주 푸시됩니다.
* **자동 크기 조정** -이 범주에 구독에 정의 된 자동 크기 조정 설정에 따라 hello 자동 크기 조정 엔진의 모든 이벤트 관련된 toohello 연산의 hello 레코드를 포함 합니다. Hello 유형의이 범주에 표시 되는 이벤트의 예로 "자동 크기 조정 수직 확장 작업이 실패 했습니다.." 자동 크기 조정을 사용 하 여 자동으로 확장 하거나 수의 크기를 조정 hello는 지원 되는 리소스 형식에 있는 인스턴스의 수는 자동 크기 조정 설정을 사용 하 여 날짜 및/또는 부하 (메트릭) 데이터는 시간에 따라 합니다. Hello 조건이 충족 되 면 tooscale 위로 또는 아래로, hello 시작 및 성공 또는 실패 이벤트는이 범주에 기록 됩니다.
* **권장 사항** - 이 범주에는 웹 사이트 및 SQL Server와 같은 특정 리소스 종류의 권장 이벤트가 포함됩니다. 이러한 이벤트는 toobetter 사용자 리소스를 활용 하는 방법에 대 한 권장 사항을 제공 합니다. 권장 사항을 내보내는 리소스가 있는 경우에만 이러한 형식의 이벤트가 수신됩니다.
* **정책, 보안 및 리소스 상태** - 이러한 범주는 이벤트를 포함하지 않으며 나중에 사용하도록 예약됩니다.

## <a name="event-schema-per-category"></a>범주별 이벤트 스키마
[범주별이 문서 toounderstand hello 활동 로그 이벤트 스키마를 참조 하십시오.](monitoring-activity-log-schema.md)

## <a name="what-you-can-do-with-hello-activity-log"></a>활동 로그 hello로 수행할 수 있는 작업
다음은 몇 hello 작업 활동 로그 hello로 수행할 수 있습니다.

![Azure 활동 로그](./media/monitoring-overview-activity-logs/Activity_Log_Overview_v3.png)


* 쿼리 및 hello에서 볼 **Azure 포털**합니다.
* [활동 로그 이벤트에서 경고 만들기](monitoring-activity-log-alerts.md)
* [Tooan 스트림 **이벤트 허브** ](monitoring-stream-activity-logs-event-hubs.md) 수집 제 3 자 서비스 또는 PowerBI 같은 사용자 지정 분석 솔루션에 대 한 합니다.
* PowerBI hello를 사용 하 여 분석할 [ **PowerBI 콘텐츠 팩**](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs/)합니다.
* [Tooa 저장 **저장소 계정** 보관 또는 수동 검사 하기 위해](monitoring-archive-activity-log.md)합니다. Hello 보존 기간 (일) hello를 사용 하 여 지정할 수 있습니다 **로그 프로필**합니다.
* PowerShell Cmdlet, CLI 또는 REST API를 통해 쿼리합니다.

## <a name="query-hello-activity-log-in-hello-azure-portal"></a>Hello Azure 포털에에서 쿼리 hello 활동 로그
Hello Azure 포털 내에서 여러 위치에서 활동 로그를 볼 수 있습니다.
* hello **활동 로그 블레이드**, hello 활동 로그에서 "더 서비스" hello 왼쪽의 탐색 창에서 검색 하 여 액세스할 수 있습니다.
* hello **모니터 블레이드**는 기본적으로 hello 왼쪽의 탐색 창에 나타납니다. 활동 로그 hello이 Azure 모니터 블레이드의 한 섹션입니다.
* 리소스의 **리소스 블레이드**, 예를 들어 가상 컴퓨터에 대 한 hello 구성 블레이드입니다. hello 활동 로그에서 대부분의 이러한 리소스 블레이드를 hello 섹션 중 하나 고 것 hello 이벤트를 필터링 자동으로 클릭할 toothose 관련 toothat 특정 리소스입니다.

Hello Azure 포털에서에서 이러한 필드에 의해 활동 로그를 필터링 할 수 있습니다.
* 이벤트에 대 한 Timespan-hello 시작 및 종료 시간입니다.
* 범주-이른바 hello 이벤트 범주입니다.
* 구독 - 하나 이상의 Azure 구독 이름입니다.
* 리소스 그룹 - 해당 구독 내에서 하나 이상의 리소스 그룹입니다.
* 리소스 (이름)-특정 리소스의 hello 이름입니다.
* 리소스 종류-리소스, 예를 들어 Microsoft.Compute/virtualmachines의 hello 유형.
* 작업 이름-예를 들어 Microsoft.SQL/servers/Write Azure 리소스 관리자 작업의 hello 이름입니다.
* 심각도-hello 이벤트 (정보, 경고, 오류, Critical)의 hello 심각도 수준입니다.
* -'호출자' hello 또는 hello 작업을 수행한 사용자로 시작 하는 이벤트입니다.
* 검색 열기 - 모든 이벤트의 모든 필드에서 해당 문자열을 검색하는 열려 있는 텍스트 검색 상자입니다.

필터 집합을 정의한 경우 tooperform 필요한 경우 세션 간에 유지 되는 쿼리도 저장할 수 있습니다 hello hello 나중에 다시 적용 된 필터와 같은 쿼리 합니다. 고정할 수도 있습니다 쿼리 tooyour Azure 대시보드 tooalways 유지 눈에 특정 이벤트입니다.

“적용”을 클릭하면 쿼리가 실행되고 일치하는 모든 이벤트를 표시합니다. 모든 이벤트 표시 해당 이벤트의 요약 hello 뿐만 아니라 해당 이벤트의 전체 raw JSON hello hello 목록에서 클릭 합니다.

더 많은 기능, 클릭 하 여 hello **로그 검색** hello의 활동 로그 데이터를 표시 하는 아이콘 [로그 분석 작업 로그 분석 솔루션](../log-analytics/log-analytics-activity.md)합니다. hello 활동 로그 블레이드 로그, 로그 분석 하면 toopivot, 쿼리 및 더 강력한 방식으로 데이터를 시각화에 기본 필터/탐색 환경을 제공 합니다.

## <a name="export-hello-activity-log-with-a-log-profile"></a>Hello 로그 프로필을 가진 활동 로그 내보내기
**로그 프로필**은 활동 로그를 내보내는 방식을 제어합니다. 로그 프로필을 사용하여 다음을 구성할 수 있습니다.

* (저장소 계정 또는 이벤트 허브) hello 활동 로그 보낼 위치
* 보낼 이벤트 범주(쓰기, 삭제, 작업) *로그 프로필 및 활동 로그 이벤트에 "범주"의 hello 의미는 다릅니다. 로그 프로필 hello, "범주" hello 작업 유형을 (쓰기, 삭제, 작업)을 나타냅니다. 활동 로그 이벤트에서 hello "category" 속성은 hello 원본 또는 이벤트 (예를 들어 관리, ServiceHealth, 경고 등)의 형식을 나타냅니다.*
* 내보낼 하위 지역(위치). Hello 활동 로그에서에서 대부분의 이벤트는 전역 이벤트 있는지 tooinclude "전역" 확인 합니다.
* Hello 활동 로그는 저장소 계정에 보관 해야 하는 기간
    - 보존이 0일이라는 것은 로그가 영원히 보관된다는 의미입니다. 그렇지 않으면 hello 값 개수에 관계 없이 1과 2147483647 사이의 일 수 있습니다.
    - 보존 정책이 설정 되어 있어도 로그를 저장소 계정에 저장 됩니다 (예를 들어 경우 비활성화 이벤트 허브 또는 OMS 옵션을 선택 하 고) hello 보존 정책이 효과가 없습니다.
    - 보존 정책이 적용 된 일, 이제 hello 보존 정책을 벗어납니다 hello 날짜 로부터 로그 종료 시간 (UTC) hello에 있으므로 삭제 됩니다입니다. 예를 들어 1 일의 보존 정책의 설치한 경우 hello 하루의 오늘 hello 시작 부분에 hello hello 이틀 전에서에서 로그 삭제 됩니다.

저장소 계정을 사용할 수 있습니다 또는 로그 내보내기 하나 hello으로 이벤트 허브 네임 스페이스에 속하지 않은 hello 동일한 구독 합니다. hello 설정을 구성 하는 hello 사용자 hello 적절 한 RBAC 액세스 tooboth 구독이 있어야 합니다.

이러한 설정은 hello 포털에서 활동 로그 블레이드에서 hello hello "Export" 옵션을 통해 구성할 수 있습니다. 프로그래밍 방식으로 구성할 수도 있습니다 있습니다 [Azure 모니터 REST API를 hello를 사용 하 여](https://msdn.microsoft.com/library/azure/dn931927.aspx), PowerShell cmdlet 또는 CLI 합니다. 하나의 구독에는 하나의 로그 프로필만 포함할 수 있습니다.

### <a name="configure-log-profiles-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 로그 프로필 구성
Hello 활동 로그 tooan 이벤트 허브를 스트림 또는 hello Azure 포털의에서 hello "내보내기" 옵션을 사용 하 여 저장소 계정에 저장할 수 있습니다.

1. Toohello 이동 **활동 로그** 블레이드 hello 메뉴를 사용 하 여 hello hello 포털의 왼쪽에 있습니다.

    ![포털에서 로그 tooActivity 이동](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. Hello 클릭 **내보내기** hello hello 블레이드 위쪽에 단추입니다.

    ![포털에서 내보내기 단추](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. 표시 되는 hello 블레이드에서 다음을 선택할 수 있습니다.  
  * 영역 하려는 tooexport 이벤트
  * 저장소 계정 toowhich toosave 이벤트 원하는 hello
  * tooretain 저장소에서 이러한 이벤트를 원하는 일 hello 수입니다. 0 일로 설정 hello 로그를 계속 유지합니다.
  * 서비스 버스 Namespace hello 스트리밍 이러한 이벤트에 대해 생성 하는 이벤트 허브 toobe 원할 것입니다.

     ![활동 로그 내보내기 블레이드](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. 클릭 **저장** toosave 이러한 설정 합니다. hello 설정이 적용된 tooyour 구독을 즉시 수는 있습니다.

### <a name="configure-log-profiles-using-hello-azure-powershell-cmdlets"></a>Hello Azure PowerShell Cmdlet을 사용 하 여 로그 프로필 구성
#### <a name="get-existing-log-profile"></a>기존 로그 프로필 가져오기
```
Get-AzureRmLogProfile
```

#### <a name="add-a-log-profile"></a>로그 프로필 추가
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

| 속성 | 필수 | 설명 |
| --- | --- | --- |
| 이름 |예 |로그 프로필의 이름입니다. |
| StorageAccountId |아니요 |Hello 저장소 계정 toowhich hello 활동 로그의 리소스 ID는 저장 해야 합니다. |
| serviceBusRuleId |아니요 |서비스 버스 규칙 toohave 이벤트 허브에서 만든 원하는 hello 서비스 버스 네임 스페이스에 대 한 ID입니다. `{service bus resource ID}/authorizationrules/{key name}` 형식의 문자열입니다. |
| 위치 |예 |쉼표로 구분 된 목록 하려는 toocollect 활동 로그 이벤트는 영역입니다. |
| RetentionInDays |예 |이벤트를 유지해야 하는 일 수는 1에서 2147483647 사이입니다. Hello 로그를 무기한으로 저장 값이 0 (무제한). |
| 범주 |아니요 |수집할 쉼표로 구분된 이벤트 범주 목록입니다. 가능한 값은 쓰기, 삭제 및 작업입니다. |

#### <a name="remove-a-log-profile"></a>로그 프로필 제거
```
Remove-AzureRmLogProfile -name my_log_profile
```

### <a name="configure-log-profiles-using-hello-azure-cross-platform-cli"></a>로그 프로필을 구성할 Azure 플랫폼 간 CLI를 사용 하 여 hello
#### <a name="get-existing-log-profile"></a>기존 로그 프로필 가져오기
```
azure insights logprofile list
```
```
azure insights logprofile get --name my_log_profile
```
hello `name` 속성에는 로그 프로필의 hello 이름 이어야 합니다.

#### <a name="add-a-log-profile"></a>로그 프로필 추가
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

| 속성 | 필수 | 설명 |
| --- | --- | --- |
| name |예 |로그 프로필의 이름입니다. |
| storageId |아니요 |Hello 저장소 계정 toowhich hello 활동 로그의 리소스 ID는 저장 해야 합니다. |
| serviceBusRuleId |아니요 |서비스 버스 규칙 toohave 이벤트 허브에서 만든 원하는 hello 서비스 버스 네임 스페이스에 대 한 ID입니다. `{service bus resource ID}/authorizationrules/{key name}` 형식의 문자열입니다. |
| 위치 |예 |쉼표로 구분 된 목록 하려는 toocollect 활동 로그 이벤트는 영역입니다. |
| RetentionInDays |예 |이벤트를 유지해야 하는 일 수는 1에서 2147483647 사이입니다. Hello 로그를 무기한으로 저장 값이 0 (무제한). |
| 범주 |아니요 |수집할 쉼표로 구분된 이벤트 범주 목록입니다. 가능한 값은 쓰기, 삭제 및 작업입니다. |

#### <a name="remove-a-log-profile"></a>로그 프로필 제거
```
azure insights logprofile delete --name my_log_profile
```

## <a name="next-steps"></a>다음 단계
* [활동 로그 (이전의 감사 로그) hello에 대 한 자세한 정보](../azure-resource-manager/resource-group-audit.md)
* [Hello Azure 활동 로그 tooEvent 허브 스트림](monitoring-stream-activity-logs-event-hubs.md)
