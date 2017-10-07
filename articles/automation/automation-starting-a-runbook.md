---
title: "Azure 자동화에서 runbook aaaStarting | Microsoft Docs"
description: "Azure 자동화에서 runbook을 사용 하는 toostart 수 있으며 모두 사용 하 여에 대 한 내용은 hello Azure 포털 및 Windows PowerShell을 제공 하는 hello 다른 메서드를 요약 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6ee756b4-9200-4eb2-9bda-ec156853803b
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: e44bce5b56b8e803f9247fbb4f3d4db7ab35c913
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a>Azure Automation에서 Runbook 시작
다음 표에서 hello hello 메서드 toostart 가장 적합 한 tooyour 특정 시나리오는 Azure 자동화에서 runbook을 결정 하는 데 도움이 됩니다. 이 문서에는 hello Azure 포털 및 Windows PowerShell로 runbook 시작에 대 한 내용은 포함 되어 있습니다. 세부 정보 아래 hello 링크에서 액세스할 수 있는 기타 문서에 hello에 다른 메서드가 제공 됩니다.

| **방법** | **특성** |
| --- | --- |
| [Azure Portal](#starting-a-runbook-with-the-azure-portal) |<li>대화형 사용자 인터페이스를 사용하는 간단한 방법<br> <li>폼 tooprovide 간단한 매개 변수 값입니다.<br> <li>작업 상태를 쉽게 추적<br> <li>Azure 로그온을 사용하여 액세스 인증 |
| [Windows PowerShell](https://msdn.microsoft.com/library/dn690259.aspx) |<li>Windows PowerShell cmdlet을 사용하여 명령줄에서 호출<br> <li>여러 단계로 구성된 자동화된 솔루션에 포함할 수 있음<br> <li>인증서 또는 OAuth 사용자 계정/서비스 보안 주체를 사용하여 요청 인증<br> <li>단순한 매개 변수 값 및 복잡한 매개 변수 값 제공<br> <li>작업 상태 추적<br> <li>클라이언트는 toosupport PowerShell cmdlet을 필요합니다. |
| [Azure Automation API](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li>가장 유연하지만 가장 복잡한 방법<br> <li>HTTP 요청을 수행할 수 있는 모든 사용자 지정 코드에서 호출<br> <li>인증서 또는 OAuth 사용자 계정/서비스 보안 주체를 사용하여 요청 인증<br> <li>단순한 매개 변수 값 및 복잡한 매개 변수 값 제공<br> <li>작업 상태 추적 |
| [Webhook](automation-webhooks.md) |<li>단일 HTTP 요청에서 Runbook 시작<br> <li>URL의 보안 토큰으로 인증<br> <li>Webhook를 만들 때 지정된 매개 변수 값을 클라이언트에서 재정의할 수 없음 Runbook은 hello HTTP 요청 세부 정보로 채워진 단일 매개 변수를 정의할 수 있습니다.<br> <li>Webhook URL 통해 없음 기능 tootrack 작업 상태입니다. |
| [TooAzure 경고에 응답](../log-analytics/log-analytics-alerts.md) |<li>응답 tooAzure 경고에서 runbook을 시작 합니다.<br> <li>Runbook에 대 한 webhook을 구성 하 고 tooalert를 연결 합니다.<br> <li>URL의 보안 토큰으로 인증 |
| [일정](automation-schedules.md) |<li>매시간, 매일, 매주 또는 매월 일정에 따라 Runbook을 자동으로 시작<br> <li>Azure Portal, PowerShell cmdlet 또는 Azure API를 통해 일정 조작<br> <li>일정에 함께 사용 되는 매개 변수 값 toobe를 제공 합니다. |
| [다른 Runbook에서](automation-child-runbooks.md) |<li>Runbook을 다른 Runbook의 활동으로 사용<br> <li>여러 Runbook에서 사용하는 기능에 유용<br> <li>매개 변수 값 toochild runbook을 제공 하 고 부모 runbook에서 출력을 사용 합니다. |

hello 다음 이미지에서는 자세한 단계별 프로세스는 runbook의 hello 수명 주기에서 다른 방법으로 Azure 자동화에서 runbook 시작 Hybrid Runbook Worker tooexecute Azure 자동화 runbook 및 여러 구성 요소 간의 상호 작용에 필요한 구성 요소를 포함 합니다. 데이터 센터를에서 자동화 runbook을 실행 하는 방법에 대 한 toolearn 너무 참조[hybrid runbook worker](automation-hybrid-runbook-worker.md)

![Runbook 아키텍처](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-hello-azure-portal"></a>Azure 포털 hello로 runbook 시작
1. Hello Azure 포털에서에서 선택 **자동화** 다음 자동화 계정 hello 이름을 클릭 하 고 있습니다.
2. Hello 허브 메뉴에서 선택 **Runbook**합니다.
3. Hello에 **Runbook** 블레이드에서 runbook을 선택 하 고 클릭 **시작**합니다.
4. Hello runbook에 매개 변수가 있으면 각 매개 변수에 대 한 텍스트 상자를 사용 하 여 증명된 tooprovide 값 수 있습니다. 매개 변수에 대한 자세한 내용은 아래의 [Runbook 매개 변수](#Runbook-parameters)를 참조하세요.
5. Hello에 **작업** 블레이드에서 hello runbook 작업의 hello 상태를 볼 수 있습니다.

## <a name="starting-a-runbook-with-windows-powershell"></a>Windows PowerShell을 사용하여 Runbook 시작
Hello를 사용할 수 있습니다 [시작 AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart Windows PowerShell로 runbook입니다. hello 다음 샘플 코드 시작 runbook 테스트 Runbook을 호출 합니다.

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

사용할 수 있는 tootrack 상태 hello runbook이 시작 된 후 개체를 작업 시작 AzureRmAutomationRunbook 반환 합니다. 이 작업 개체를 사용할 수 있습니다 [Get AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) hello 작업의 toodetermine hello 상태 및 [Get AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget 출력 합니다. 다음 샘플 코드는 hello Runbook을 완료 된 다음 해당 출력을 표시 될 때까지 기다린 호출 되는 runbook을 시작 합니다.

```
$runbookName = "Test-Runbook"
$ResourceGroup = "ResourceGroup01"
$AutomationAcct = "MyAutomationAccount"

$job = Start-AzureRmAutomationRunbook –AutomationAccountName $AutomationAcct -Name $runbookName -ResourceGroupName $ResourceGroup

$doLoop = $true
While ($doLoop) {
   $job = Get-AzureRmAutomationJob –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup
   $status = $job.Status
   $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped"))
}

Get-AzureRmAutomationJobOutput –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup –Stream Output
```

Hello runbook에 매개 변수가 필요한 경우와 같이 제공 해야 합니다는 [hashtable](http://technet.microsoft.com/library/hh847780.aspx) hello 매개 변수 값은 hello 매개 변수 이름과 hello 값 hello 해시 테이블의 hello 키와 일치 하는 합니다. hello 다음 예제에서는 toostart 두 문자열 매개 변수를 사용 하 여 runbook의 이름을 지정 방법 FirstName 및 LastName, RepeatCount 라는 정수 및 Show 라는 부울 매개 변수 매개 변수에 대한 자세한 내용은 아래의 [Runbook 매개 변수](#Runbook-parameters)를 참조하세요.

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a>Runbook 매개 변수
Hello Azure 포털 또는 Windows PowerShell에서 runbook을 시작할 때 hello 명령이 hello Azure 자동화 웹 서비스를 통해 전송 됩니다. 이 서비스는 복잡한 데이터 형식을 가진 매개 변수를 지원하지 않습니다. Tooprovide 값 복잡 한 매개 변수를 사용 해야 경우 있습니다 인라인으로 호출 해야 다른 runbook에서에 설명 된 대로 [Azure 자동화에서 자식 runbook](automation-child-runbooks.md)합니다.

hello Azure 자동화 웹 서비스는 hello 다음 섹션에에서 설명 된 대로 특정 데이터 형식을 사용 하 여 매개 변수에 대 한 특별 한 기능을 제공 합니다.

### <a name="named-values"></a>명명된 값
Hello 매개 변수가 [object] 데이터 형식인 경우 hello 다음 JSON 형식을 toosend 것 목록은 명명 된 값을 사용할 수 있습니다: *{Name1: 'Value1', Name2: 'Value2', Name3: 'Value3'}*합니다. 이러한 값은 단순한 형식이어야 합니다. hello runbook으로 hello 매개 변수를 받게 됩니다는 [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) tooeach 명명 된 값을 해당 하는 속성을 사용 합니다.

Hello를 사용자 라는 매개 변수를 허용 하는 테스트 runbook을 따르는 것이 좋습니다.

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][object]$user
   )
    $userObject = $user | ConvertFrom-JSON
    if ($userObject.Show) {
        foreach ($i in 1..$userObject.RepeatCount) {
            $userObject.FirstName
            $userObject.LastName
        }
    }
}
```

hello 다음 텍스트를 사용할 수 hello user 매개 변수에 대 한 있습니다.

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

이 인해 hello 출력을 수행 합니다.

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a>배열
Hello 매개 변수가 [array]와 같은 배열이 면 또는 [string []]를 사용 하 여 hello JSON 형식 toosend 다음 그 값 목록이: *[Value1, Value2, Value3]*합니다. 이러한 값은 단순한 형식이어야 합니다.

Hello 다음 테스트 runbook을 호출 하는 매개 변수를 허용 하는 것이 좋습니다 *사용자*합니다.

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][array]$user
   )
    if ($user[3]) {
        foreach ($i in 1..$user[2]) {
            $ user[0]
            $ user[1]
        }
    }
}
```

hello 다음 텍스트를 사용할 수 hello user 매개 변수에 대 한 있습니다.

```
["Joe","Smith",2,true]
```

이 인해 hello 출력을 수행 합니다.

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a>자격 증명
Hello 매개 변수 데이터 형식이 면 **PSCredential**, Azure 자동화의 hello 이름을 제공할 수 있습니다 [자격 증명 자산](automation-credentials.md)합니다. hello runbook 지정 하는 hello 이름의 hello 자격 증명을 검색 합니다.

Hello를 라는 자격 증명 매개 변수를 허용 하는 테스트 runbook을 따르는 것이 좋습니다.

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

hello 다음 텍스트에 사용 될 수 있다고 가정할 때 이라는 자격 증명 자산이 hello user 매개 변수에 *내 자격 증명*합니다.

```
My Credential
```

Hello 자격 증명의 사용자 이름 hello 가정함 *jsmith*,이 인해 hello 다음 출력 합니다.

```
jsmith
```

## <a name="next-steps"></a>다음 단계
* 현재 문서의 hello runbook 아키텍처는 Azure 및 온-프레미스 하이브리드 Runbook 작업자 hello로에서 리소스 관리는 runbook의 대략적인 개요를 제공합니다.  데이터 센터를에서 자동화 runbook을 실행 하는 방법에 대 한 toolearn 너무 참조[Hybrid Runbook Worker](automation-hybrid-runbook-worker.md)합니다.
* 특정 또는 일반 함수에 대 한 다른 runbook에서 사용 되는 모듈식 runbook toobe 만드는 hello에 대 한 자세한 toolearn 너무 참조[자식 Runbook](automation-child-runbooks.md)합니다.

