---
title: "Azure 자동화 작업 데이터 tooOMS 로그 분석 aaaForward | Microsoft Docs"
description: "이 문서에서는 toosend 작업 상태 및 runbook 작업 tooMicrosoft Operations Management Suite 로그 분석 toodeliver 추가 정보 및 관리를 스트림 하는 방법을 보여줍니다."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: c12724c6-01a9-4b55-80ae-d8b7b99bd436
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/02/2017
ms.author: magoedte
ms.openlocfilehash: e78b6c6677d6502711ce828e2d32b7a91922ae26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="forward-job-status-and-job-streams-from-automation-toolog-analytics-oms"></a>자동화 tooLog 분석 (OMS)에서 작업 상태 및 작업 스트림 전달
자동화는 runbook 작업 상태 및 작업 스트림을 tooyour Microsoft Operations Management Suite (OMS) 로그 분석 작업 영역을 보낼 수 있습니다.  작업 로그 및 작업 스트림 hello Azure 포털에에서 표시 되 나 powershell을 개별 작업 및이 대 한 사용 하면 tooperform 단순 조사를 수행 합니다. 이제 Log Anaytics를 사용하여 다음을 수행할 수 있습니다.

* 자동화 작업에 대한 통찰력 확보
* Runbook 작업 상태(예: 실패 또는 일시 중단)를 기반으로 전자 메일 또는 경고 트리거
* 작업 스트림에서 고급 쿼리 작성
* 자동화 계정 간에 작업 상호 연결
* 시간별 작업 기록 시각화     

## <a name="prerequisites-and-deployment-considerations"></a>필수 구성 요소 및 배포 고려 사항
자동화를 보내는 toostart tooLog 분석 로그 사용 해야 합니다.

1. 2016 년 11 월 hello 또는 나중에 릴리스를 [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) (v2.3.0).
2. Log Analytics 작업 영역. 자세한 내용은 [Log Analytics 시작](../log-analytics/log-analytics-get-started.md)을 참조하세요. 
3. Azure 자동화 계정에 대 한 hello ResourceId

Azure 자동화 계정 및 로그 분석 작업 영역에서 다음 PowerShell hello 실행에 대 한 toofind hello ResourceId:

```powershell
# Find hello ResourceId for hello Automation Account
Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"

# Find hello ResourceId for hello Log Analytics workspace
Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
```

작업 영역, hello 명령, 앞의 hello 출력에서 찾을 hello 또는 여러 자동화 계정이 있는 경우 *이름* tooconfigure 필요 하 고 hello 값을 복사 *ResourceId*합니다.

Toofind hello 해야 할 경우 *이름* 자동화 계정의 hello Azure 포털 자동화 계정에서에서 선택 hello **자동화 계정** 블레이드에 대 한 선택 **모든설정**.  Hello에서 **모든 설정을** 블레이드 아래 **계정 설정** 선택 **속성**합니다.  Hello에 **속성** 블레이드에서 이러한 값을 기록할 수 있습니다.<br> ![자동화 계정 속성](media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png)을 참조하세요.

## <a name="set-up-integration-with-log-analytics"></a>Log Analytics와의 통합 설정
1. 사용자 컴퓨터에서 시작 **Windows PowerShell** hello에서 **시작** 화면입니다.  
2. 복사 하거나 hello PowerShell에서 다음을 붙여 넣고 hello에 대 한 hello 값 편집 `$workspaceId` 및 `$automationAccountId`합니다.  Hello에 대 한 `-Environment` 매개 변수에 유효한 값은 *azure 클라우드* 또는 *AzureUSGovernment* 에서 작업 하는 hello 클라우드 환경에 따라 합니다.     

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }

# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $automationAccountId -WorkspaceId $workspaceId -Enabled $true

```

이 스크립트를 실행한 후 새 JobLogs 또는 쓰고 있는 JobStreams의 10분 이내에 Log Analytics에 레코드가 표시됩니다.

toosee hello 로그, hello 다음 로그 분석 로그 검색에 대 한 쿼리를 실행 합니다.`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`

### <a name="verify-configuration"></a>구성 확인
자동화 계정에서 보내는 tooconfirm tooyour 로그 분석 작업 영역을 로그, 진단 hello 다음 PowerShell을 사용 하 여 hello 자동화 계정에서 올바르게 설정 되어 있는지 확인:

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }
# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Get-AzureRmDiagnosticSetting -ResourceId $automationAccountId
```

Hello 출력을 확인.
+ 아래 *로그*, 값에 대 한 hello *Enabled* 은 *True*
+ 값을 hello *WorkspaceId* toohello ResourceId의 로그 분석 작업 영역 설정


## <a name="log-analytics-records"></a>Log Analytics 레코드
Azure Automation의 진단은 Log Analytics에 두 가지 유형의 레코드를 만들고 **Type=AzureDiagnostic**로 태그가 지정됩니다.

### <a name="job-logs"></a>작업 로그
| 속성 | 설명 |
| --- | --- |
| TimeGenerated |날짜 및 hello runbook 작업 실행 시간입니다. |
| RunbookName_s |hello runbook의 hello 이름입니다. |
| Caller_s |Hello 작업을 시작한 사람입니다.  가능한 값은 전자 메일 주소 또는 예약된 작업의 시스템입니다. |
| Tenant_g | 호출자에 게 hello에 대 한 hello 테 넌 트를 식별 하는 GUID입니다. |
| JobId_g |hello hello runbook 작업의 Id는 GUID입니다. |
| ResultType |hello runbook 작업의 hello 상태입니다.  가능한 값은 다음과 같습니다.<br>- 시작됨<br>- 중지됨<br>- 일시 중단됨<br>- 실패<br>- 완료됨 |
| Category | Hello 종류의 데이터 분류 합니다.  자동화를 위해 hello 값은 JobLogs입니다. |
| OperationName | Azure에서 수행한 작업의 hello 유형을 지정 합니다.  자동화를 위해 hello 값은 작업입니다. |
| 리소스 | hello 자동화 계정 이름 |
| SourceSystem | 로그 분석 hello 데이터 수집 하는 방법입니다. Azure 진단의 경우 항상 *Azure*입니다. |
| ResultDescription |Hello runbook 작업 결과 상태를 설명합니다.  가능한 값은 다음과 같습니다.<br>- 작업 시작<br>- 작업 실패<br>- Job Completed입니다. |
| CorrelationId |hello hello runbook 작업의 상관 관계 Id는 GUID입니다. |
| ResourceId |Hello runbook의 hello Azure 자동화 계정 리소스 id를 지정합니다. |
| SubscriptionId | hello hello 자동화 계정에 대 한 Azure 구독 Id (GUID)입니다. |
| ResourceGroup | Hello 자동화 계정에 대 한 hello 리소스 그룹의 이름입니다. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |


### <a name="job-streams"></a>작업 스트림
| 속성 | 설명 |
| --- | --- |
| TimeGenerated |날짜 및 hello runbook 작업 실행 시간입니다. |
| RunbookName_s |hello runbook의 hello 이름입니다. |
| Caller_s |Hello 작업을 시작한 사람입니다.  가능한 값은 전자 메일 주소 또는 예약된 작업의 시스템입니다. |
| StreamType_s |작업 스트림의 hello 형식입니다. 가능한 값은 다음과 같습니다.<br>- 진행<br>- 출력<br>- 경고<br>- 오류<br>- 디버그<br>- Verbose입니다. |
| Tenant_g | 호출자에 게 hello에 대 한 hello 테 넌 트를 식별 하는 GUID입니다. |
| JobId_g |hello hello runbook 작업의 Id는 GUID입니다. |
| ResultType |hello runbook 작업의 hello 상태입니다.  가능한 값은 다음과 같습니다.<br>- 진행 중 |
| Category | Hello 종류의 데이터 분류 합니다.  자동화를 위해 hello 값은 JobStreams입니다. |
| OperationName | Azure에서 수행한 작업의 hello 유형을 지정 합니다.  자동화를 위해 hello 값은 작업입니다. |
| 리소스 | hello 자동화 계정 이름 |
| SourceSystem | 로그 분석 hello 데이터 수집 하는 방법입니다. Azure 진단의 경우 항상 *Azure*입니다. |
| ResultDescription |Hello runbook에서 출력 스트림에 hello 포함 되어 있습니다. |
| CorrelationId |hello hello runbook 작업의 상관 관계 Id는 GUID입니다. |
| ResourceId |Hello runbook의 hello Azure 자동화 계정 리소스 id를 지정합니다. |
| SubscriptionId | hello hello 자동화 계정에 대 한 Azure 구독 Id (GUID)입니다. |
| ResourceGroup | Hello 자동화 계정에 대 한 hello 리소스 그룹의 이름입니다. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |

## <a name="viewing-automation-logs-in-log-analytics"></a>Log Analytics에서 자동화 로그 보기
보내는 자동화 작업 로그 tooLog 분석을 시작 했으므로 이러한 로그 내 로그 분석으로 수행할 수 있는 확인해 보겠습니다.

다음 쿼리에서 hello 실행 toosee hello 로그:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`

### <a name="send-an-email-when-a-runbook-job-fails-or-suspends"></a>Runbook 작업이 실패하거나 일시 중단된 경우 전자 메일 보내기
Runbook 작업에 문제가 발생 하는 경우 전자 메일 또는 텍스트 기능 toosend hello에 대 한가 묻습니다 상위 고객 중 하나입니다.   

toocreate 경고 규칙 hello runbook에 대 한 로그 검색 hello 경고를 호출 해야 하는 작업 레코드를 만들어 시작 합니다.  Hello 클릭 **경고** toocreate 단추 및 hello 경고 규칙을 구성 합니다.

1. Hello 로그 분석 개요 페이지에서 클릭 **로그 검색**합니다.
2. Hello 검색 hello 쿼리 필드에 다음을 입력 하 여 경고에 대 한 로그 검색 쿼리를 만들어: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended)` 를 사용 하 여 hello RunbookName 기준으로 그룹화 수도 있습니다.`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended) | measure Count() by RunbookName_s`   

   에 둘 이상의 자동화 계정 또는 구독 tooyour 작업 영역에서 로그를 설정 하는 경우 구독 및 자동화 계정에서 경고를 그룹화 할 수 있습니다.  자동화 계정 이름 JobLogs의 hello 검색에서 hello 리소스 필드에서 파생 될 수 있습니다.  
3. tooopen hello **경고 규칙 추가** 화면 **경고** hello hello 페이지 위쪽에 있습니다. Hello 옵션 tooconfigure hello 경고에 자세한 내용은 참조 하십시오. [로그 분석에서 경고](../log-analytics/log-analytics-alerts.md#alert-rules)합니다.

### <a name="find-all-jobs-that-have-completed-with-errors"></a>오류와 함께 완료된 모든 작업 찾기
또한 오류에 tooalerting, runbook 작업에 종료 되지 않는 오류가 있을 때을 찾을 수 있습니다. 이러한 경우 PowerShell 오류 스트림에 생성 합니다. 하지만 hello 종료 되지 않은 오류 작업 toosuspend 발생 하지 않거나 실패 합니다.    

1. Log Analytics 작업 영역에서 **로그 검색**을 클릭합니다.
2. Hello 쿼리 필드에 입력 `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams StreamType_s=Error | measure count() by JobId_g` 클릭 하 고 **검색**합니다.

### <a name="view-job-streams-for-a-job"></a>작업에 대한 작업 스트림 보기
작업을 디버깅 하는 경우 수도 있습니다 toolook hello 작업 스트림으로 합니다.  hello 다음 쿼리 표시 GUID 2ebd22ea e05e-4eb9-9 차원 76 d73cbd4356e0 인 단일 작업에 대 한 모든 hello 스트림을 합니다.   

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams JobId_g="2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0" | sort TimeGenerated | select ResultDescription`

### <a name="view-historical-job-status"></a>기록 작업 상태 보기
마지막으로 할 수 있습니다 toovisualize 작업 기록 시간에 따라.  작업의 hello 상태에 대 한 시간에 따라이 쿼리 toosearch를 사용할 수 있습니다.

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  
<br> ![OMS 기록 작업 상태 차트](media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)<br>

## <a name="summary"></a>요약
프로그램 자동화 작업 상태 및 스트림 데이터 tooLog 분석을 전송 하 여 자동화 작업 하 여 hello 상태에 대 한 더 나은 정보를 얻을 수 있습니다.
+ 설정 경고 toonotify 있습니다에 문제가 있을 때
+ 사용자 지정 보기 및 검색 쿼리 toovisualize를 사용 하 여 프로그램 runbook 결과, runbook 작업 상태 및 기타 관련 주요 표시기 또는 메트릭.  

로그 분석 operational 띄도록 tooyour 자동화 작업을 제공 및 보다 신속한 주소 인시던트 있습니다.  

## <a name="next-steps"></a>다음 단계
* toolearn 어떻게 tooconstruct 다른 검색 쿼리 및 검토 hello 자동화 작업 로그 분석을 사용 하 여 로그에 대 한 자세한 참조 [로그 분석 검색 로그인](../log-analytics/log-analytics-log-searches.md)
* runbook에서 toocreate 및 검색 하 고 출력 및 오류 메시지를 확인 하려면 어떻게 toounderstand [Runbook 출력 및 메시지](automation-runbook-output-and-messages.md)
* toolearn toomonitor runbook 작업 및 기타 기술 정보가 참조 하는 방법 runbook 실행에 대 한 자세한 [runbook 작업을 추적 합니다.](automation-runbook-execution.md)
* OMS 로그 분석 및 데이터 컬렉션 원본에 대해 자세히 toolearn 참조 [로그 분석 개요에서 수집 하는 Azure 저장소 데이터](../log-analytics/log-analytics-azure-storage.md)
