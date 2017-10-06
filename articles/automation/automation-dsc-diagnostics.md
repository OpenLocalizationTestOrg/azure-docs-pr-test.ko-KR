---
title: "Azure 자동화 DSC 보고 데이터 tooOMS 로그 분석 aaaForward | Microsoft Docs"
description: "이 문서에서는 방법을 toosend 원하는 상태 구성 (DSC) 보고 데이터 tooMicrosoft Operations Management Suite 로그 분석 toodeliver 대 한 추가 정보 및 관리 합니다."
services: automation
documentationcenter: 
author: eslesar
manager: carmonm
editor: tysonn
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: eslesar
ms.openlocfilehash: 21f78d5549d53ba3d7e237f55d9086f380cf3351
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="forward-azure-automation-dsc-reporting-data-toooms-log-analytics"></a>Azure 자동화 DSC 로그 분석 데이터 tooOMS 보고 전달

자동화는 DSC 노드 상태 데이터 tooyour Microsoft Operations Management Suite (OMS) 로그 분석 작업 영역을 보낼 수 있습니다.  
준수 상태 표시 되지만 hello Azure 포털 또는 PowerShell을 사용 하 여 노드 및 노드 구성이 개별 DSC 리소스 Log Anaytics를 사용하여 다음을 수행할 수 있습니다.

* 관리되는 노드 및 개별 리소스에 대한 준수 정보 가져오기
* 준수 상태를 기준으로 전자 메일 또는 경고 트리거
* 관리되는 노드에서 고급 쿼리 작성
* Automation 계정에서 준수 상태 상호 연관
* 시간에 따른 노드 준수 내역 시각화

## <a name="prerequisites"></a>필수 조건

toostart 보내는 자동화 DSC 보고 tooLog 분석 해야 합니다.

* 2016 년 11 월 hello 또는 나중에 릴리스를 [Azure PowerShell](/powershell/azure/overview) (v2.3.0).
* Azure 자동화 계정. 자세한 내용은 [Azure Automation 시작](automation-offering-get-started.md)을 참조하세요.
* **Automation & Control** 서비스가 제공되는 Log Analytics 작업 공간 자세한 내용은 [Log Analytics 시작](../log-analytics/log-analytics-get-started.md)을 참조하세요.
* 하나 이상의 Azure Automation DSC 노드. 자세한 내용은 [Azure Automation DSC를 통한 관리를 위한 컴퓨터 온보드](automation-dsc-onboarding.md)를 참조하세요. 

## <a name="set-up-integration-with-log-analytics"></a>Log Analytics와의 통합 설정

Azure 자동화 DSC에서 로그 분석, 단계를 수행 하는 전체 hello로 데이터를 가져오는 toobegin:

1. PowerShell에서 Azure 계정 tooyour에 로그인 합니다. [Azure PowerShell을 사용하여 로그인](https://docs.microsoft.com/en-us/powershell/azure/authenticate-azureps?view=azurermps-4.0.0)을 참조하세요.
1. Hello 가져오기 _ResourceId_ hello 다음 PowerShell 명령을 실행 하 여 자동화 계정의: (자동화 계정이 여러 개 있는 경우 선택 hello _ResourceID_ 원하는 hello 계정에 대 한 tooconfigure)입니다.

  ```powershell
  # Find hello ResourceId for hello Automation Account
  Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"
  ```
1. Hello 가져오기 _ResourceId_ hello 다음 PowerShell 명령을 실행 하 여 로그 분석 작업 영역의: (둘 이상의 작업 영역을 사용 하는 경우 선택 hello _ResourceID_ hello 작업 영역에 대 한 tooconfigure)입니다.

  ```powershell
  # Find hello ResourceId for hello Log Analytics workspace
  Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
  ```
1. 다음 PowerShell 명령을, 대체 실행된 hello `<AutomationResourceId>` 및 `<WorkspaceResourceId>` hello로 _ResourceId_ 각 hello 이전 단계에서 값:

  ```powershell
  Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $true -Categories "DscNodeStatus"
  ```

Azure 자동화 DSC에서 로그 분석에 데이터를 가져오는 toostop 원한다 면 hello 다음 PowerShell 명령을 실행 합니다.

```powershell
Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $false -Categories "DscNodeStatus"
```

## <a name="view-hello-dsc-logs"></a>Hello DSC 로그 보기

자동화 DSC 데이터에 대 한 로그 분석와의 통합을 설정한 후는 **로그 검색** hello에 단추가 나타납니다 **DSC 노드** 블레이드 자동화 계정. Hello 클릭 **로그 검색** DSC 노드 데이터에 대 한 tooview hello 로그 단추입니다.

![로그 검색 단추](media/automation-dsc-diagnostics/log-search-button.png)

hello **로그 검색** 블레이드가 열리고 표시는 **DscNodeStatusData** 각 DSC 노드에 대 한 작업 및 **DscResourceStatusData** 각각에 대 한 작업이 [DSC 리소스](https://msdn.microsoft.com/powershell/dsc/resources) hello 노드 구성 적용 된 toothat에서에서 호출 합니다.

hello **DscResourceStatusData** 작업에 실패 한 모든 DSC 리소스에 대 한 오류 정보를 포함 합니다.

해당 작업에 대 한 hello 목록 toosee hello 데이터의 각 작업을 클릭 합니다.

[로그 분석에서 검색 하 여 hello 로그를 볼 수도 있습니다 합니다. [로그 검색을 사용하여 데이터 찾기](../log-analytics/log-analytics-log-searches.md)를 참조하세요.
형식 hello 다음 쿼리 toofind 프로그램 DSC 로그:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus"`

Hello 작업 이름으로 hello 쿼리를 좁힐 수도 있습니다. 예: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus" OperationName = "DscNodeStatusData"

### <a name="send-an-email-when-a-dsc-compliance-check-fails"></a>DSC 준수 확인이 실패할 때 전자 메일 보내기

고객 것 기능 toosend hello에 대 한 전자 메일 또는 텍스트는 DSC 구성에 문제가 발생 하는 경우.   

toocreate 경고 규칙을 만들어 hello 경고를 호출 해야 하는 hello DSC 보고서 레코드에 대 한 로그 검색을 시작 합니다.  Hello 클릭 **경고** toocreate 단추 및 hello 경고 규칙을 구성 합니다.

1. Hello 로그 분석 개요 페이지에서 클릭 **로그 검색**합니다.
1. Hello 검색 hello 쿼리 필드에 다음을 입력 하 여 경고에 대 한 로그 검색 쿼리를 만듭니다.`Type=AzureDiagnostics Category=DscNodeStatus NodeName_s=DSCTEST1 OperationName=DscNodeStatusData ResultType=Failed`

  에 둘 이상의 자동화 계정 또는 구독 tooyour 작업 영역에서 로그를 설정 하는 경우 구독 및 자동화 계정에서 경고를 그룹화 할 수 있습니다.  
  자동화 계정 이름 DscNodeStatusData의 hello 검색에서 hello 리소스 필드에서 파생 될 수 있습니다.  
1. tooopen hello **경고 규칙 추가** 화면 **경고** hello hello 페이지 위쪽에 있습니다. Hello 옵션 tooconfigure hello 경고에 대 한 자세한 내용은 참조 하십시오. [로그 분석에서 경고](../log-analytics/log-analytics-alerts.md#alert-rules)합니다.

### <a name="find-failed-dsc-resources-across-all-nodes"></a>모든 노드에서 실패한 DSC 리소스 찾기

Log Analytics를 사용할 때의 한 가지 이점은 노드에서 실패한 검사를 검색할 수 있다는 것입니다.
toofind 실패 한 DSC 리소스의 모든 인스턴스.

1. Hello 로그 분석 개요 페이지에서 클릭 **로그 검색**합니다.
1. Hello 검색 hello 쿼리 필드에 다음을 입력 하 여 경고에 대 한 로그 검색 쿼리를 만듭니다.`Type=AzureDiagnostics Category=DscNodeStatus OperationName=DscResourceStatusData ResultType=Failed`

### <a name="view-historical-dsc-node-status"></a>DSC 노드 상태 기록 보기

마지막으로 할 수 있습니다 toovisualize DSC 노드 상태 기록을 시간이 지남에 따라.  
시간이 지남에 따라이 쿼리 toosearch hello 상태의 DSC 노드 상태에 대 한 사용할 수 있습니다.

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=DscNodeStatus NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  

이 시간에 따른 hello 노드 상태 차트에 표시 됩니다.

## <a name="log-analytics-records"></a>Log Analytics 레코드

Azure Automation의 진단은 Log Analytics에 두 가지 범주의 레코드를 만듭니다.

### <a name="dscnodestatusdata"></a>DscNodeStatusData

| 속성 | 설명 |
| --- | --- |
| TimeGenerated |실행 날짜 / 시간 hello 규정 준수가 확인 하는 시간입니다. |
| OperationName |DscNodeStatusData |
| ResultType |규격 hello 노드 인지 여부입니다. |
| NodeName_s |hello 관리 되는 노드의 hello 이름입니다. |
| NodeComplianceStatus_s |규격 hello 노드 인지 여부입니다. |
| DscReportStatus |여부 hello 준수 확인 실행 되었습니다. |
| ConfigurationMode | 어떻게 hello 구성이 적용 된 toohello 노드 합니다. 사용 가능한 값은 __"ApplyOnly"__,__"ApplyandMonitior"__ 및 __"ApplyandAutoCorrect"__입니다. <ul><li>__ApplyOnly__: DSC가 hello 구성을 적용 하 고 새 구성을 대상 노드 toohello 또는 새 구성이 서버에서 끌어온 경우 밀어넣어 하지 않습니다. 새 구성이 초기에 적용된 후 DSC는 이전에 구성된 상태에서 달라졌는지 여부를 확인하지 않습니다. DSC 시도 tooapply hello 구성 하기 전에 성공할 때까지 __ApplyOnly__ 적용 됩니다. </li><li> __ApplyAndMonitor__: hello 기본값입니다. hello LCM이 새 구성을 적용 합니다. 새 구성의 초기 적용 후 hello 대상 노드의 상태가 필요한 hello 상태에서 변경 되는 경우 DSC에서 로그 hello 불일치를 보고 합니다. DSC 시도 tooapply hello 구성 하기 전에 성공할 때까지 __ApplyAndMonitor__ 적용 됩니다.</li><li>__ApplyAndAutoCorrect__: DSC는 모든 새 구성을 적용합니다. 새 구성의 초기 적용 후 hello 대상 노드의 상태가 필요한 hello 상태에서 변경 되는 경우 DSC 로그에 hello 불일치를 보고 하 고 hello 현재 구성을 다시 적용 합니다.</li></ul> |
| HostName_s | hello 관리 되는 노드의 hello 이름입니다. |
| IPAddress | hello의 IPv4 주소 hello 노드를 관리합니다. |
| Category | DscNodeStatus |
| 리소스 | Azure 자동화 계정 hello의 hello 이름입니다. |
| Tenant_g | 호출자에 게 hello에 대 한 hello 테 넌 트를 식별 하는 GUID입니다. |
| NodeId_g |Hello 관리 되는 노드를 식별 하는 GUID입니다. |
| DscReportId_g |Hello 보고서를 식별 하는 GUID입니다. |
| LastSeenTime_t |날짜 및 시간 hello 보고서를 마지막으로 본입니다. |
| ReportStartTime_t |날짜 및 hello 보고서 시작 된 시간입니다. |
| ReportEndTime_t |날짜 및 시간 hello 보고서 완료 하는 경우입니다. |
| NumberOfResources_d |DSC 리소스의 hello 수 hello 적용 된 구성 toohello 노드에서 호출 됩니다. |
| SourceSystem | 로그 분석 hello 데이터 수집 하는 방법입니다. Azure 진단의 경우 항상 *Azure*입니다. |
| ResourceId |Hello Azure 자동화 계정을 지정합니다. |
| ResultDescription | 이 작업에 대 한 hello 설명입니다. |
| SubscriptionId | hello hello 자동화 계정에 대 한 Azure 구독 Id (GUID)입니다. |
| ResourceGroup | Hello 자동화 계정에 대 한 hello 리소스 그룹의 이름입니다. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |
| CorrelationId |hello hello 규정 준수 보고서의 상관 관계 Id는 GUID입니다. |

### <a name="dscresourcestatusdata"></a>DscResourceStatusData

| 속성 | 설명 |
| --- | --- |
| TimeGenerated |실행 날짜 / 시간 hello 규정 준수가 확인 하는 시간입니다. |
| OperationName |DscResourceStatusData|
| ResultType |규격 hello 리소스 인지 여부입니다. |
| NodeName_s |hello 관리 되는 노드의 hello 이름입니다. |
| Category | DscNodeStatus |
| 리소스 | Azure 자동화 계정 hello의 hello 이름입니다. |
| Tenant_g | 호출자에 게 hello에 대 한 hello 테 넌 트를 식별 하는 GUID입니다. |
| NodeId_g |Hello 관리 되는 노드를 식별 하는 GUID입니다. |
| DscReportId_g |Hello 보고서를 식별 하는 GUID입니다. |
| DscResourceId_s |hello DSC 리소스 인스턴스의 hello 이름입니다. |
| DscResourceName_s |hello DSC 리소스의 hello 이름입니다. |
| DscResourceStatus_s |규정을 준수에서 hello DSC 리소스 인지 여부입니다. |
| DscModuleName_s |hello DSC 리소스를 포함 하는 hello PowerShell 모듈의 hello 이름입니다. |
| DscModuleVersion_s |hello DSC 리소스를 포함 하는 hello PowerShell 모듈의 hello 버전입니다. |
| DscConfigurationName_s |hello 구성의 hello 이름 toohello 노드를 적용 합니다. |
| ErrorCode_s | hello hello 리소스 실패 한 경우 오류 코드입니다. |
| ErrorMessage_s |hello hello 리소스 실패 한 경우 오류 메시지입니다. |
| DscResourceDuration_d |hello 시간 hello DSC 리소스에서 실행 되 던 (초)에서입니다. |
| SourceSystem | 로그 분석 hello 데이터 수집 하는 방법입니다. Azure 진단의 경우 항상 *Azure*입니다. |
| ResourceId |Hello Azure 자동화 계정을 지정합니다. |
| ResultDescription | 이 작업에 대 한 hello 설명입니다. |
| SubscriptionId | hello hello 자동화 계정에 대 한 Azure 구독 Id (GUID)입니다. |
| ResourceGroup | Hello 자동화 계정에 대 한 hello 리소스 그룹의 이름입니다. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |
| CorrelationId |hello hello 규정 준수 보고서의 상관 관계 Id는 GUID입니다. |

## <a name="summary"></a>요약

자동화 DSC 데이터 tooLog 분석을 전송 하 여 hello 하 여 자동화 DSC 노드 상태에 대 한 더 나은 정보를 얻을 수 있습니다.

* 설정 경고 toonotify 있습니다에 문제가 있을 때
* 사용자 지정 보기 및 검색 쿼리 toovisualize를 사용 하 여 프로그램 runbook 결과, runbook 작업 상태 및 기타 관련 주요 표시기 또는 메트릭.  

로그 분석 큰 operational 가시성 tooyour 자동화 DSC 데이터를 제공 하 고 주소 인시던트 보다 신속 하 게 합니다.  

## <a name="next-steps"></a>다음 단계

* 로그 분석을 사용 하 여 기록 방법을 tooconstruct 다른 검색 쿼리 및 검토 hello 자동화 DSC에 대 한 자세한 toolearn 참조 [로그 분석 검색 로그인](../log-analytics/log-analytics-log-searches.md)
* Azure 자동화 DSC를 사용 하 여에 대 한 더 toolearn 참조 [Azure 자동화 DSC 시작](automation-dsc-getting-started.md)
* OMS 로그 분석 및 데이터 컬렉션 원본에 대해 자세히 toolearn 참조 [로그 분석 개요에서 수집 하는 Azure 저장소 데이터](../log-analytics/log-analytics-azure-storage.md)

