---
title: "Azure 자동화에서 aaaSchedules | Microsoft Docs"
description: "자동화 일정 toostart Azure 자동화에에서 사용 되는 tooschedule runbook를 자동으로 됩니다. 설명 방법을 toocreate 및 특정 시간에 또는 되풀이 일정으로 runbook를 자동으로 시작할 수 있도록 일정에 따라 관리 합니다."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 1c2da639-ad20-4848-920b-88e471b2e1d9
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2016
ms.author: magoedte
ms.openlocfilehash: 888a5d15fd3442a2b8ab18dd8b0eb4ab9ad0c0d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a>Azure 자동화에서 Runbook 예약
tooschedule runbook에서 지정된 된 시간에 Azure 자동화 toostart을 연결한 tooone 또는 자세한 일정입니다. 일정에 따라 구성 된 tooeither 한 번 또는 발생 매시간 실행 될 수 있습니다 또는 hello Azure 클래식 포털의에서 runbook에 대해 및 hello Azure 포털의에서 runbook에 대해 일별 일정을 예약할 수도 있습니다을 매주, 매월, 특정 요일 hello 또는 며칠 분의 hello에 대 한 월 또는 hello 월, 일 합니다.  Runbook에 연결 된 toomultiple 일정 일 수 있습니다 및 일정에 따라 여러 개의 연결 된 runbook tooit 있을 수 있습니다.

> [!NOTE]
> 일정은 현재 Azure 자동화 DSC 구성을 지원하지 않습니다.
> 
> 

## <a name="windows-powershell-cmdlets"></a>Windows PowerShell cmdlet
다음 표에 hello의 hello cmdlet은 사용 되는 toocreate 하 고 Azure 자동화에서 Windows PowerShell을 사용 하 여 일정을 관리 합니다. Hello의 일부분으로 제공 [Azure PowerShell 모듈](/powershell/azure/overview)합니다.

| Cmdlet | 설명 |
|:--- |:--- |
| **Azure Resource Manager cmdlet** | |
| [Get-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/get-azurermautomationschedule) |일정을 검색합니다. |
| [New-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/new-azurermautomationschedule) |새 일정을 만듭니다. |
| [Remove-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/remove-azurermautomationschedule) |일정을 제거합니다. |
| [Set-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/set-azurermautomationschedule) |기존 일정에 대 한 hello 속성을 설정합니다. |
| [Get-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/set-azurermautomationscheduledrunbook) |예약된 Runbook을 검색합니다. |
| [Register-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) |Runbook을 일정에 연결합니다. |
| [Unregister-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/unregister-azurermautomationscheduledrunbook) |일정에서 Runbook을 분리합니다. |
| **Azure Service Management cmdlet** | |
| [Get-AzureAutomationSchedule](/powershell/module/azure/get-azureautomationschedule?view=azuresmps-3.7.0) |일정을 검색합니다. |
| [New-AzureAutomationSchedule](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) |새 일정을 만듭니다. |
| [Remove-AzureAutomationSchedule](/powershell/module/azure/remove-azureautomationschedule?view=azuresmps-3.7.0) |일정을 제거합니다. |
| [Set-AzureAutomationSchedule](/powershell/module/azure/set-azureautomationschedule?view=azuresmps-3.7.0) |기존 일정에 대 한 hello 속성을 설정합니다. |
| [Get-AzureAutomationScheduledRunbook](/powershell/module/azure/get-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |예약된 Runbook을 검색합니다. |
| [Register-AzureAutomationScheduledRunbook](/powershell/module/azure/register-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |Runbook을 일정에 연결합니다. |
| [Unregister-AzureAutomationScheduledRunbook](/powershell/module/azure/unregister-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |일정에서 Runbook을 분리합니다. |

## <a name="creating-a-schedule"></a>일정 만들기
Hello 클래식 포털에서 또는 Windows PowerShell과 함께 hello Azure 포털에서에서 runbook에 대 한 새 일정을 만들 수 있습니다. Azure 포털 또는 Azure 클래식 hello를 사용 하 여 runbook tooa 일정을 연결 하면 새 일정을 만드는 hello 옵션이 있습니다.

> [!NOTE]
> Azure 자동화 새 예약 된 작업이 실행 될 때 자동화 계정에서 hello 최신 모듈을 사용 합니다.  runbook과 hello에 영향을 주지 tooavoid 자동화 프로세스, 먼저 모든 runbook 테스트를 위한 전용 자동화 계정으로 일정 연결을 테스트 해야 합니다.  이것은 유효성을 검사 하면 예약 된 runbook은 계속 toowork 올바르게 고 되기 전에 필요한 마이그레이션 업데이트 hello runbook 버전 tooproduction 모든 변경 내용이 경우 not, 추가로 문제를 해결 하 고 적용할 수 있습니다.  
>  자동화 계정을 자동으로 가져오지 것입니다 모듈의 새 버전을 모두 hello를 선택 하 여 수동으로 업데이트 한 경우가 아니면 [업데이트 Azure 모듈](automation-update-azure-modules.md) hello에서 옵션 **모듈** 블레이드입니다. 
>  

### <a name="toocreate-a-new-schedule-in-hello-azure-portal"></a>toocreate hello Azure 포털에서에서 새 일정
1. Hello 자동화 계정에서 Azure 포털에서에서 클릭 hello **자산** 타일 tooopen hello **자산** 블레이드입니다.
2. Hello 클릭 **일정** 타일 tooopen hello **일정** 블레이드입니다.
3. 클릭 **일정을 추가할** hello hello 블레이드 위쪽에 있습니다.
4. Hello에 **새 일정** 블레이드에서 입력 **이름** 및 필요에 따라 한 **설명** hello 새 일정에 대 한 합니다.
5. 선택 하 여 hello 일정이 한 번에 실행 될 여부 또는 일정에 따라 되풀이 해야 선택 **한 번** 또는 **되풀이**합니다.  **한 번**을 선택하는 경우 **시작 시간**을 지정한 다음 **만들기**를 클릭합니다.  선택 하는 경우 **되풀이**, 지정는 **시작 시간** 및 빈도 hello runbook toorepeat-의해 hello 빈도 **시간**, **일**, **주**, 또는 **월**합니다.  선택 하는 경우 **주** 또는 **월** hello 드롭 다운 목록에서 hello **되풀이 옵션** 표시 되며 hello 블레이드에서 선택 하면 hello **되풀이 옵션** 블레이드에 표시 되 고 선택 된 경우 hello 요일을 선택할 수 **주**합니다.  선택한 경우 **월**를 선택할 수 있습니다 **평일** 또는 특정 일에 hello 달의 hello 일정을 마지막으로, toorun 할 수 있습니다에 여부 hello 달의 마지막 날 hello 및 클릭 **확인** .   

### <a name="toocreate-a-new-schedule-in-hello-azure-classic-portal"></a>toocreate hello Azure 클래식 포털에서에서 새 일정
1. Hello Azure 클래식 포털에서에서 자동화를 선택 하 고 자동화 계정의 이름 hello를 선택 합니다.
2. 선택 hello **자산** 탭 합니다.
3. Hello hello 창의 아래쪽에 있는 클릭 **설정 추가**합니다.
4. **일정 추가**를 클릭합니다.
5. 입력 **이름** 및 필요에 따라 한 **설명** 새 schedule.your hello에 대 한 일정이 실행 될 **한 번**, **시간별**, **매일**, **매주**, 또는 **월별**합니다.
6. 지정 된 **시작 시간** 및 hello 선택한 일정 유형에 따라 다른 옵션입니다.

### <a name="toocreate-a-new-schedule-with-windows-powershell"></a>Windows PowerShell을 사용 하 여 새 일정 toocreate
Hello를 사용할 수 있습니다 [New-azureautomationschedule](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) cmdlet toocreate 클래식 runbook에 대 한 Azure 자동화에서 새 일정 또는 [새로 AzureRmAutomationSchedule](/powershell/module/azurerm.automation/new-azurermautomationschedule) hello Azure에서에서 runbook에 대 한 cmdlet 포털입니다. Hello 일정 및 실행 되는 hello 빈도 대 한 hello 시작 시간을 지정 해야 합니다.

hello 다음 샘플 명령은 표시 방법을 toocreate hello에 대 한 일정 15 및 Azure 리소스 관리자 cmdlet을 사용 하 여 매월 30입니다.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"

다음 명령 예제는 hello toocreate 새 일정 하는 실행 되는 방법을 각각 보여 일 오후 3시 30분 2015 년 1 월 20 일에 Azure 서비스 관리 cmdlet으로 시작 합니다.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

## <a name="linking-a-schedule-tooa-runbook"></a>일정 tooa runbook 연결
Runbook에 연결 된 toomultiple 일정 일 수 있습니다 및 일정에 따라 여러 개의 연결 된 runbook tooit 있을 수 있습니다. Runbook에 매개 변수가 있는 경우 값을 제공할 수 있습니다. 필수 매개 변수의 값은 반드시 제공해야 하며, 선택적 매개 변수의 값은 필요에 따라 제공할 수 있습니다.  이러한 값이이 일정에 따라 hello runbook이 시작 될 때마다 사용 됩니다.  연결할 수 같은 runbook tooanother 일정 hello 하 고 다른 매개 변수 값을 지정 합니다.

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-portal"></a>toolink hello Azure 포털을 사용 하 여 일정 tooa runbook
1. Hello 자동화 계정에서 Azure 포털에서에서 클릭 hello **Runbook** 타일 tooopen hello **Runbook** 블레이드입니다.
2. Hello runbook tooschedule의 hello 이름을 클릭 합니다.
3. Hello runbook tooa 현재 연결 된 일정이 없으면 지정 된 hello 옵션 toocreate 새 일정을 일 또는 tooan 기존 일정을 연결 합니다.  
4. Hello runbook에 매개 변수가 hello 옵션을 선택할 수 있습니다 **실행된 설정 (기본값: Azure) 수정** 및 hello **매개 변수** hello 정보를 적절 하 게 입력할 수 있는 블레이드 표시 됩니다.  

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-classic-portal"></a>toolink hello Azure 클래식 포털을 사용 하 여 일정 tooa runbook
1. Hello Azure 클래식 포털에서에서 선택 **자동화** 자동화 계정의 hello 이름을 클릭 하 고 있습니다.
2. 선택 hello **Runbook** 탭 합니다.
3. Hello runbook tooschedule의 hello 이름을 클릭 합니다.
4. Hello 클릭 **일정** 탭 합니다.
5. Hello runbook tooa 현재 연결 된 일정 않은 경우 주어 집니다 hello 옵션 너무 경우**tooa 새 일정을 연결** 또는 **tooan 기존 일정을 연결**합니다.  현재 연결 된 tooa 일정이 hello runbook을 사용 하는 경우 클릭 **링크** 에 hello hello 창 tooaccess 맨 이러한 옵션입니다.
6. Hello runbook에 매개 변수가 해당 값에 대 한 라는 메시지가 표시 됩니다.  

### <a name="toolink-a-schedule-tooa-runbook-with-windows-powershell"></a>Windows PowerShell을 사용 하 여 일정 tooa runbook toolink
Hello를 사용할 수 있습니다 [Register-azureautomationscheduledrunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) toolink 일정 tooa 클래식 runbook 또는 [레지스터 AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) hello Azure 포털에서에서 runbook에 대 한 cmdlet입니다.  Hello 매개 변수 매개 변수와 함께 hello runbook의 매개 변수 값을 지정할 수 있습니다. 매개 변수 값 지정에 대한 자세한 내용은 [Azure 자동화에서 Runbook 시작](automation-starting-a-runbook.md) 을 참조하세요.

hello 다음 샘플 명령은 표시 방법을 toolink 일정 tooa runbook에 매개 변수는 Azure 리소스 관리자 cmdlet을 사용 합니다.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"
hello 다음 샘플 명령은 표시 방법을 toolink Azure 서비스 관리 cmdlet을 사용 하 여 매개 변수를 사용 하는 일정입니다.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

## <a name="disabling-a-schedule"></a>일정 해제
일정을 비활성화 하면 모든 연결 된 runbook tooit 더 이상 해당 일정에서 실행 됩니다. 일정을 수동으로 해제하거나, 일정을 만들 때 빈도를 사용하여 일정에 대한 만료 시간을 설정할 수 있습니다. Hello 만료 시간에 도달 하면 hello 일정 비활성화 됩니다.

### <a name="toodisable-a-schedule-from-hello-azure-portal"></a>toodisable hello Azure 포털에서 일정
1. Hello 자동화 계정에서 Azure 포털에서에서 클릭 hello **자산** 타일 tooopen hello **자산** 블레이드입니다.
2. Hello 클릭 **일정** 타일 tooopen hello **일정** 블레이드입니다.
3. 일정 tooopen hello 세부 정보 블레이드에서의 hello 이름을 클릭 합니다.
4. 변경 **Enabled** 너무**아니요**합니다.

### <a name="toodisable-a-schedule-from-hello-azure-classic-portal"></a>toodisable hello Azure 클래식 포털에서 일정
Hello hello 일정에 대 한 hello 일정 세부 정보 페이지에서 Azure 클래식 포털에서에서 일정을 비활성화할 수 있습니다.

1. Hello Azure 클래식 포털에서에서 자동화를 선택 하 고 자동화 계정의 hello 이름을 클릭 합니다.
2. Hello 자산 탭을 선택 합니다.
3. 일정 tooopen hello 이름을 해당 세부 정보 페이지를 클릭 합니다.
4. 변경 **Enabled** 너무**아니요**합니다.

### <a name="toodisable-a-schedule-with-windows-powershell"></a>Windows PowerShell을 사용 하 여 일정 toodisable
Hello를 사용할 수 있습니다 [Set-azureautomationschedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) 클래식 runbook에 대 한 기존 일정의 cmdlet toochange hello 속성 또는 [집합 AzureRmAutomationSchedule](/powershell/module/azurerm.automation/set-azurermautomationschedule) hello Azure에서에서 runbook에 대 한 cmdlet 포털입니다. toodisable hello 예약을 지정 **false** hello에 대 한 **IsEnabled** 매개 변수입니다.

hello 다음 샘플 명령은 표시 방법을 toodisable Azure 리소스 관리자 cmdlet을 사용 하 여 runbook에 대 한 일정입니다.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"

다음 명령 예제는 hello 사용 하 여 예약 toodisable Azure 서비스 관리 cmdlet hello 하는 방법을 보여 줍니다.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

## <a name="next-steps"></a>다음 단계
* Azure 자동화에서 runbook 시작 tooget 참조 [Azure 자동화에서 Runbook 시작](automation-starting-a-runbook.md) 

