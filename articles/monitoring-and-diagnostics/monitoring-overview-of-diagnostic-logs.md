---
title: "Azure 진단 로그의 aaaOverview | Microsoft Docs"
description: "Azure 진단 로그 정의 및 사용 하는 방법으로 Azure 리소스 내에서 발생 하는 toounderstand 이벤트에 알아봅니다."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem; magoedte
ms.openlocfilehash: e38991c540626b4bb5b5b9a995276881ee58f368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a>Azure 리소스에서 로그 데이터 수집 및 소비

## <a name="what-are-azure-resource-diagnostic-logs"></a>Azure 리소스 진단 로그란?
**Azure 리소스 수준 진단 로그** 는 해당 리소스의 hello 작업에 대 한 데이터를 다양 하 고 자주 제공 하는 리소스에서 내보낸 로그입니다. 이러한 로그의 hello 콘텐츠 리소스 유형에 따라 달라 집니다. 예를 들어 네트워크 보안 그룹 규칙 카운터와 Key Vault 감사는 리소스 로그의 두 범주입니다.

리소스 수준 진단 로그 hello에서 다 [활동 로그](monitoring-overview-activity-logs.md)합니다. 활동 로그 hello 구독의 리소스 관리자를 사용 하 여, 예를 들어 가상 컴퓨터를 만들거나 삭제 논리 앱 리소스에에서 대해 수행 된 hello 작업에 대 한 정보를 제공 합니다. 활동 로그 hello은 구독 수준 로그입니다. 리소스 수준 진단 로그는 Key Vault에서 암호 가져오기 등과 같이 리소스 자체에서 수행된 작업에 대한 정보를 제공합니다.

리소스 수준 진단 로그도 게스트 OS 수준 진단 로그와 다릅니다. 게스트 OS 진단 로그는 가상 컴퓨터나 다른 지원되는 리소스 유형 안에서 실행되는 에이전트가 수집합니다. 게스트 운영 체제 수준 진단 로그 hello 운영 체제 및 가상 컴퓨터에서 실행 중인 응용 프로그램에서 데이터를 캡처하는 동안 리소스 수준 진단 로그 hello 자체를 Azure 플랫폼에서에서 없는 에이전트 및 캡처 리소스 관련 데이터를 필요 합니다.

일부 리소스는 hello 새로운 유형의 여기에서 설명 하는 리소스 진단 로그를 지원 합니다. 이 문서는 섹션 목록 hello 새 리소스 수준 진단 로그를 지원 하는 리소스 형식을 포함 합니다.

![리소스 진단 로그와 다른 로그 유형 비교 ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a>리소스 수준 진단 로그로 수행할 수 있는 작업
다음은 몇 hello 작업 리소스 진단 로그를 수행할 수 있습니다.

![리소스 진단 로그의 논리적 배치](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* Tooa 저장해 [ **저장소 계정** ](monitoring-archive-diagnostic-logs.md) 감사 또는 수동 검사 합니다. 사용 하 여 hello 보존 기간 (일)을 지정할 수 있습니다 **리소스 진단 설정을**합니다.
* [파일을 스트리밍할 너무**이벤트 허브** ](monitoring-stream-diagnostic-logs-to-event-hubs.md) 수집 제 3 자 서비스 또는 PowerBI 같은 사용자 지정 분석 솔루션에 대 한 합니다.
* [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)

저장소 계정을 사용할 수 있습니다 또는 로그 내보내기 하나 hello으로 이벤트 허브 네임 스페이스에 속하지 않은 hello 동일한 구독 합니다. hello 설정을 구성 하는 hello 사용자 hello 적절 한 RBAC 액세스 tooboth 구독이 있어야 합니다.

## <a name="resource-diagnostic-settings"></a>리소스 진단 설정
리소스 진단 설정을 사용하여 비-계산 리소스에 대한 리소스 진단 로그를 구성합니다. 리소스 제어를 위한 **리소스 진단 설정**은 다음과 같습니다.

* 리소스 진단 로그 및 메트릭을 보내는 위치(Storage 계정, Event Hubs 및/또는 OMS Log Analytics).
* 전송되는 로그 범주 및 메트릭 데이터의 전송 여부.
* 각 로그 항목을 저장소 계정에 유지해야 하는 기간.
    - 보존이 0일이라는 것은 로그가 영원히 보관된다는 의미입니다. 그렇지 않으면 hello 값 개수에 관계 없이 1과 2147483647 사이의 일 수 있습니다.
    - 보존 정책이 설정 되어 있어도 로그를 저장소 계정에 저장 됩니다 (예를 들어 경우 비활성화 이벤트 허브 또는 OMS 옵션을 선택 하 고) hello 보존 정책이 효과가 없습니다.
    - 보존 정책이 적용 된 일, 이제 hello 보존 정책을 벗어납니다 hello 날짜 로부터 로그 종료 시간 (UTC) hello에 있으므로 삭제 됩니다입니다. 예를 들어 1 일의 보존 정책의 설치한 경우 hello 하루의 오늘 hello 시작 부분에 hello hello 이틀 전에서에서 로그 삭제 됩니다.

이러한 설정은 hello hello Azure 포털에서에서 리소스에 대 한 진단 설정을 통해, Azure PowerShell 및 CLI 명령을 또는 hello를 통해 구성 쉽게 됩니다 [Azure 모니터 REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx)합니다.

> [!WARNING]
> 진단 로그 및 메트릭에 대 한 계산 리소스 (예를 들어 Vm 또는 서비스 패브릭) 사용 하는 hello 게스트 OS 레이어에서 [구성 및 출력의 선택에 대 한 별도 메커니즘](../azure-diagnostics.md)합니다.
>
>

## <a name="how-tooenable-collection-of-resource-diagnostic-logs"></a>어떻게 리소스 진단 로그의 tooenable 컬렉션
리소스 진단 로그의 컬렉션을 사용할 수 [리소스 관리자 서식 파일에서 리소스 만들기의 일부로](./monitoring-enable-diagnostic-logs-using-template.md) 또는 리소스 hello 포털에서 해당 리소스의 페이지에서 만들어진 후 합니다. 또한 Azure PowerShell 또는 CLI 명령을 사용 하 여 또는 hello Azure 모니터 REST API를 사용 하 여 특정 시점 컬렉션을 사용할 수 있습니다.

> [!TIP]
> 이러한 지침은 적용 되지 않을 직접 tooevery 리소스. Hello toocertain 리소스 유형에 적용 될 수 있는 페이지 toounderstand 특별 한 단계가이 맨 아래에 hello 스키마 링크를 참조 하십시오.
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-hello-portal"></a>Hello 포털에서 리소스 진단 로그의 컬렉션을 사용 하도록 설정
리소스 hello Azure에서에서 진단 로그의 컬렉션을 사용 하도록 설정할 수 tooa 특정 리소스 이동 하거나 tooAzure 모니터를 탐색 하 여 리소스가 만들어진 후 포털입니다. tooenable Azure 모니터를 통해이:

1. Hello에 [Azure 포털](http://portal.azure.com)tooAzure 모니터 이동한 클릭 **진단 설정**

    ![Azure Monitor의 모니터링 섹션](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. 필요에 따라 리소스 그룹 또는 리소스 유형으로 hello 목록을 필터링 하려는 진단 설정 tooset hello 리소스 클릭 합니다.

3. 선택한 hello 리소스에 설정이 없는 있으면 증명된 toocreate 설정 됩니다. “진단 켜기”를 클릭합니다.

   ![진단 설정 추가 - 기존 설정 없음](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   Hello 리소스에 대 한 기존 설정을 없을 경우이 리소스에서 이미 구성 되어 있는 설정 목록이 표시 됩니다. “진단 설정 추가”를 클릭합니다.

   ![진단 설정 추가 - 기존 설정](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. 사용자 설정 이름을 제공 하, 각 대상 toowhich toosend 데이터와 같은 및 어떤 리소스를 구성 하는 각 대상에 대 한 사용 되는 hello 확인란을 선택 합니다. Hello를 사용 하 여 다양 한 일 tooretain 이러한 로그를 필요에 따라 설정 **보존 (일)** 슬라이더 (만 적용 가능한 toohello 저장소 계정 대상). 0 일의 보존 hello 로그를 무기한으로 저장 합니다.
   
   ![진단 설정 추가 - 기존 설정](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. **Save**를 클릭합니다.

몇 분 후 새 설정이이 리소스에 대 한 설정의 목록에 표시 하 고 진단 로그 toohello 보내집니다 hello 새 이벤트 데이터는 생성 되는 즉시 대상을 지정 합니다.

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a>PowerShell을 통한 리소스 진단 로그 컬렉션 활성화
다음 명령을 사용 하 여 hello Azure PowerShell을 통해 리소스 진단 로그의 tooenable 컬렉션:

저장소 계정에 진단 로그의 tooenable 저장소에는이 명령을 사용 합니다.

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

hello 저장소 계정 toowhich toosend hello를 원하는 로그 hello 저장소 계정 ID는 리소스 ID를 hello 합니다.

이 명령을 사용 하 여 진단 로그 tooan 이벤트 허브의 tooenable 스트리밍:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

hello 서비스 버스 규칙 ID는이 형식 문자열: `{Service Bus resource ID}/authorizationrules/{key name}`합니다.

tooenable 보내는 진단 로그 tooa 로그 분석 작업 영역에서이 명령을 사용 합니다.

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
```

다음 명령을 hello를 사용 하 여 로그 분석 작업 영역의 hello 리소스 ID를 가져올 수 있습니다.

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

이러한 매개 변수 tooenable 여러 출력 옵션 결합할 수 있습니다.

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a>CLI를 통해 리소스 진단 로그 컬렉션 활성화
hello Azure CLI를 통해 리소스 진단 로그의 tooenable 컬렉션 hello 다음 명령을 사용 합니다.

저장소 계정에 진단 로그의 tooenable 저장소에는이 명령을 사용 합니다.

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

hello 저장소 계정 toowhich toosend hello를 원하는 로그 hello 저장소 계정 ID는 리소스 ID를 hello 합니다.

이 명령을 사용 하 여 진단 로그 tooan 이벤트 허브의 tooenable 스트리밍:

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

hello 서비스 버스 규칙 ID는이 형식 문자열: `{Service Bus resource ID}/authorizationrules/{key name}`합니다.

tooenable 보내는 진단 로그 tooa 로그 분석 작업 영역에서이 명령을 사용 합니다.

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
```

이러한 매개 변수 tooenable 여러 출력 옵션 결합할 수 있습니다.

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a>REST API를 통해 리소스 진단 로그 컬렉션 활성화
hello Azure 모니터 REST API를 사용 하 여 toochange 진단 설정을 참조 [이 문서](https://msdn.microsoft.com/library/azure/dn931931.aspx)합니다.

## <a name="manage-resource-diagnostic-settings-in-hello-portal"></a>Hello 포털에서 리소스 진단 설정 관리
리소스를 모두 진단 설정으로 설정했는지 확인합니다. 너무 이동**모니터** hello 포털 및 open의 **진단 설정을**합니다.

![Hello 포털에서 진단 로그 블레이드](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

"더 많은 서비스" toofind hello 모니터 섹션 tooclick를 할 수 있습니다.

여기 볼 수 있습니다 및 진단을 사용 하는 경우 진단 설정을 toosee를 지 원하는 모든 리소스를 필터링 합니다. 드릴 다운 하 toosee 설정이 여러 리소스에 설정 된 경우 하 고는 저장소 계정, 이벤트 허브 네임 스페이스 및/또는 데이터를 이동 하는 로그 분석 작업 영역을 확인할 수도 있습니다.

![포털의 진단 로그 결과](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

진단 설정을 진단 설정 보기, 여기서 있습니다 수 설정, 해제 또는 hello에 대 한 진단 설정을 수정 hello 표시 되며 추가 리소스를 선택 합니다.

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a>리소스 진단 로그에 대해 지원되는 서비스, 범주 및 스키마
[이 문서를 참조 하십시오.](monitoring-diagnostic-logs-schema.md) 전체 목록은 지원 되는 서비스 및 hello 로그 범주 및 해당 서비스에서 사용 되는 스키마에 대 한 합니다.

## <a name="next-steps"></a>다음 단계

* [진단 로그 리소스를 너무 스트림**이벤트 허브**](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Hello Azure 모니터 REST API를 사용 하 여 리소스 진단 설정 변경](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [Azure Storage에서 Log Analytics를 사용하여 로그 분석](../log-analytics/log-analytics-azure-storage.md)
