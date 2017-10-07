---
title: "Azure 자동화에서 runbook aaaScheduling | Microsoft Docs"
description: "설명 방법을 toocreate Azure 자동화의 일정에 따라 특정 시간에 또는 되풀이 일정으로 runbook를 자동으로 시작할 수 있도록 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 710979ff-99d8-41e4-ac6d-6bf26b8ea654
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/09/2016
ms.author: bwren
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: c215b7ff6aa200466f3be566facba3c0cffcc924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a>Azure 자동화에서 Runbook 예약
tooschedule runbook에서 지정된 된 시간에 Azure 자동화 toostart을 연결한 tooone 또는 자세한 일정입니다. 일정에 따라 구성 된 tooeither 한 번 실행 될 수 있습니다 하거나 된 일정에 따라 되풀이 해야 시간별 또는 일별로 hello Azure 클래식 포털의에서 runbook에 대해 및 hello Azure 포털의에서 runbook에 대해 예약할 수 있습니다 또한으로 hello 주의 매주, 매월, 특정 일 또는 요일에 대 한 hello 월 또는 hello 월, 일 합니다.  Runbook에 연결 된 toomultiple 일정 일 수 있습니다 및 일정에 따라 여러 개의 연결 된 runbook tooit 있을 수 있습니다.

## <a name="creating-a-schedule"></a>일정 만들기
Hello 클래식 포털에서 또는 Windows PowerShell과 함께 hello Azure 포털에서에서 runbook에 대 한 새 일정을 만들 수 있습니다. Azure 포털 또는 Azure 클래식 hello를 사용 하 여 runbook tooa 일정을 연결 하면 새 일정을 만드는 hello 옵션이 있습니다.

> [!NOTE]
> Runbook과 일정을 연결할 때 자동화 계정에 hello hello 모듈의 현재 버전을 저장 하 고 toothat 일정을 연결 하 합니다.  이 일정을 만들 때 계정에 버전 1.0 사용 하 여 모듈에 다음 hello 모듈 tooversion 2.0를 업데이트 하는 경우 hello 일정은 toouse 1.0 계속 것을 의미 합니다.  순서 toouse hello 모듈 업데이트 된 버전에서 새 일정을 만들어야 합니다. 
> 
> 

### <a name="toocreate-a-new-schedule-in-hello-azure-classic-portal"></a>toocreate hello Azure 클래식 포털에서에서 새 일정
1. Hello Azure 클래식 포털에서에서 자동화를 선택 하 고 자동화 계정의 이름 hello을 다음 선택 합니다.
2. 선택 hello **자산** 탭 합니다.
3. Hello hello 창의 아래쪽에 있는 클릭 **설정 추가**합니다.
4. **일정 추가**를 클릭합니다.
5. 입력 **이름** 및 필요에 따라 한 **설명** 새 schedule.your hello에 대 한 일정이 실행 될 **한 번**, **시간별**, **매일**, **매주**, 또는 **월별**합니다.
6. 지정 된 **시작 시간** 및 hello 선택한 일정 유형에 따라 다른 옵션입니다.

### <a name="toocreate-a-new-schedule-in-hello-azure-portal"></a>toocreate hello Azure 포털에서에서 새 일정
1. Hello 자동화 계정에서 Azure 포털에서에서 클릭 hello **자산** 타일 tooopen hello **자산** 블레이드입니다.
2. Hello 클릭 **일정** 타일 tooopen hello **일정** 블레이드입니다.
3. 클릭 **일정을 추가할** hello hello 블레이드 위쪽에 있습니다.
4. Hello에 **새 일정** 블레이드에서 입력 **이름** 및 필요에 따라 한 **설명** hello 새 일정에 대 한 합니다.
5. 선택 하 여 hello 일정이 한 번에 실행 될 여부 또는 일정에 따라 되풀이 해야 선택 **한 번** 또는 **되풀이**합니다.  **한 번**을 선택하는 경우 **시작 시간**을 지정한 다음 **만들기**를 클릭합니다.  선택 하는 경우 **되풀이**, 지정는 **시작 시간** 및 빈도 hello runbook toorepeat-의해 hello 빈도 **시간**, **일**, **주**, 또는 **월**합니다.  선택 하는 경우 **주** 또는 **월** hello 드롭 다운 목록에서 hello **되풀이 옵션** 표시 되며 hello 블레이드에서 선택 하면 hello **되풀이 옵션** 블레이드에 표시 되 고 선택 된 경우 hello 요일을 선택할 수 **주**합니다.  선택한 경우 **월**를 선택할 수 있습니다 **요일이** 또는 특정 일에 hello 달의 hello 일정을 마지막으로, toorun 할 수 있습니다에 여부 hello 달의 마지막 날 hello 및 클릭 **확인** .   

### <a name="toocreate-a-new-schedule-with-windows-powershell"></a>Windows PowerShell을 사용 하 여 새 일정 toocreate
Hello를 사용할 수 있습니다 [New-azureautomationschedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) cmdlet toocreate 클래식 runbook에 대 한 Azure 자동화에서 새 일정 또는 [새로 AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx) hello Azure에서에서 runbook에 대 한 cmdlet 포털입니다. Hello 일정 및 실행 되는 hello 빈도 대 한 hello 시작 시간을 지정 해야 합니다.

다음 명령 예제는 hello toocreate 새 일정 하는 실행 되는 방법을 각각 보여 일 오후 3시 30분 2015 년 1 월 20 일에 Azure 서비스 관리 cmdlet으로 시작 합니다.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

hello 다음 샘플 명령은 표시 방법을 toocreate hello에 대 한 일정 15 및 Azure 리소스 관리자 cmdlet을 사용 하 여 매월 30입니다.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"


## <a name="linking-a-schedule-tooa-runbook"></a>일정 tooa runbook 연결
Runbook에 연결 된 toomultiple 일정 일 수 있습니다 및 일정에 따라 여러 개의 연결 된 runbook tooit 있을 수 있습니다. Runbook에 매개 변수가 있는 경우 값을 제공할 수 있습니다. 필수 매개 변수의 값은 반드시 제공해야 하며, 선택적 매개 변수의 값은 필요에 따라 제공할 수 있습니다.  이러한 값이이 일정에 따라 hello runbook이 시작 될 때마다 사용 됩니다.  연결할 수 같은 runbook tooanother 일정 hello 하 고 다른 매개 변수 값을 지정 합니다.

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-classic-portal"></a>toolink hello Azure 클래식 포털을 사용 하 여 일정 tooa runbook
1. Hello Azure 클래식 포털에서에서 선택 **자동화** 다음 자동화 계정 hello 이름을 클릭 하 고 있습니다.
2. 선택 hello **Runbook** 탭 합니다.
3. Hello runbook tooschedule의 hello 이름을 클릭 합니다.
4. Hello 클릭 **일정** 탭 합니다.
5. Hello runbook tooa 현재 연결 된 일정 않은 경우 주어 집니다 hello 옵션 너무 경우**tooa 새 일정을 연결** 또는 **tooan 기존 일정을 연결**합니다.  현재 연결 된 tooa 일정이 hello runbook을 사용 하는 경우 클릭 **링크** 에 hello hello 창 tooaccess 맨 이러한 옵션입니다.
6. Hello runbook에 매개 변수가 해당 값에 대 한 라는 메시지가 표시 됩니다.  

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-portal"></a>toolink hello Azure 포털을 사용 하 여 일정 tooa runbook
1. Hello 자동화 계정에서 Azure 포털에서에서 클릭 hello **Runbook** 타일 tooopen hello **Runbook** 블레이드입니다.
2. Hello runbook tooschedule의 hello 이름을 클릭 합니다.
3. Hello runbook tooa 현재 연결 된 일정이 없으면 지정 된 hello 옵션 toocreate 새 일정을 일 또는 tooan 기존 일정을 연결 합니다.  
4. Hello runbook에 매개 변수가 hello 옵션을 선택할 수 있습니다 **실행된 설정 (기본값: Azure) 수정** 및 hello **매개 변수** hello 정보를 적절 하 게 입력할 수 있는 블레이드 표시 됩니다.  

### <a name="toolink-a-schedule-tooa-runbook-with-windows-powershell"></a>Windows PowerShell을 사용 하 여 일정 tooa runbook toolink
Hello를 사용할 수 있습니다 [Register-azureautomationscheduledrunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) toolink 일정 tooa 클래식 runbook 또는 [레지스터 AzureRmAutomationScheduledRunbook](https://msdn.microsoft.com/library/mt603575.aspx) hello Azure 포털에서에서 runbook에 대 한 cmdlet입니다.  Hello 매개 변수 매개 변수와 함께 hello runbook의 매개 변수 값을 지정할 수 있습니다. 매개 변수 값 지정에 대한 자세한 내용은 [Azure 자동화에서 Runbook 시작](automation-starting-a-runbook.md) 을 참조하세요.

hello 다음 샘플 명령은 표시 방법을 toolink Azure 서비스 관리 cmdlet을 사용 하 여 매개 변수를 사용 하는 일정입니다.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

hello 다음 샘플 명령은 표시 방법을 toolink 일정 tooa runbook에 매개 변수는 Azure 리소스 관리자 cmdlet을 사용 합니다.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"

## <a name="disabling-a-schedule"></a>일정 해제
일정을 비활성화 하면 모든 연결 된 runbook tooit 더 이상 해당 일정에서 실행 됩니다. 일정을 수동으로 해제하거나, 일정을 만들 때 빈도를 사용하여 일정에 대한 만료 시간을 설정할 수 있습니다. Hello 만료 시간에 도달 하면 hello 일정 비활성화 됩니다.

### <a name="toodisable-a-schedule-from-hello-azure-classic-portal"></a>toodisable hello Azure 클래식 포털에서 일정
Hello hello 일정에 대 한 hello 일정 세부 정보 페이지에서 Azure 클래식 포털에서에서 일정을 비활성화할 수 있습니다.

1. Hello Azure 클래식 포털에서에서 자동화를 선택 하 고 클릭 hello 자동화 계정의 이름입니다.
2. Hello 자산 탭을 선택 합니다.
3. 일정 tooopen hello 이름을 해당 세부 정보 페이지를 클릭 합니다.
4. 변경 **Enabled** 너무**아니요**합니다.

### <a name="toodisable-a-schedule-from-hello-azure-portal"></a>toodisable hello Azure 포털에서 일정
1. Hello 자동화 계정에서 Azure 포털에서에서 클릭 hello **자산** 타일 tooopen hello **자산** 블레이드입니다.
2. Hello 클릭 **일정** 타일 tooopen hello **일정** 블레이드입니다.
3. 일정 tooopen hello 세부 정보 블레이드에서의 hello 이름을 클릭 합니다.
4. 변경 **Enabled** 너무**아니요**합니다.

### <a name="toodisable-a-schedule-with-windows-powershell"></a>Windows PowerShell을 사용 하 여 일정 toodisable
Hello를 사용할 수 있습니다 [Set-azureautomationschedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) 클래식 runbook에 대 한 기존 일정의 cmdlet toochange hello 속성 또는 [집합 AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603566.aspx) hello Azure에서에서 runbook에 대 한 cmdlet 포털입니다. toodisable hello 예약을 지정 **false** hello에 대 한 **IsEnabled** 매개 변수입니다.

다음 명령 예제는 hello 사용 하 여 예약 toodisable Azure 서비스 관리 cmdlet hello 하는 방법을 보여 줍니다.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

hello 다음 샘플 명령은 표시 방법을 toodisable Azure 리소스 관리자 cmdlet을 사용 하 여 runbook에 대 한 일정입니다.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"


## <a name="next-steps"></a>다음 단계
* 일정을 작업에 대해 자세히 toolearn 참조 [Azure 자동화에서 일정 자산](http://msdn.microsoft.com/library/azure/dn940016.aspx)
* Azure 자동화에서 runbook 시작 tooget 참조 [Azure 자동화에서 Runbook 시작](automation-starting-a-runbook.md) 

