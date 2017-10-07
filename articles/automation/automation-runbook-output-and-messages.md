---
title: "aaaRunbook 출력과 Azure 자동화에서 메시지 | Microsoft Docs"
description: "Azure 자동화의 runbook에서 toocreate 및 검색 하 고 출력 및 오류 메시지 하는 방법을 설명."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 13a414f5-0e2c-4be2-9558-a3e3ec84b6b2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: magoedte;bwren
ms.openlocfilehash: c1505fa889473766bfa47e43aaed2449d60ad851
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-output-and-messages-in-azure-automation"></a>Azure Automation에서 Runbook 출력 및 메시지
대부분의 Azure 자동화 runbook 일종의 출력이 오류 메시지 toohello 사용자와 같은 있거나 toobe 다른 워크플로에서 사용을 위한 하는 복합 개체입니다. Windows PowerShell에는 [여러 스트림을](http://blogs.technet.com/heyscriptingguy/archive/2014/03/30/understanding-streams-redirection-and-write-host-in-powershell.aspx) toosend 스크립트나 워크플로에서 출력 합니다. Azure 자동화 이러한 스트림의 각와 다르게 작동 하 고 방법에 대 한 최상의 방법을 따라야 합니다. runbook을 만들 때 각 toouse 합니다.

hello 다음 표에서 각 hello 스트림과 hello Azure 관리 포털에서에서의 동작에 대 한 간략 한 설명을 게시 된 runbook을 실행할 때 및 [runbook을 테스트](automation-testing-runbook.md)합니다. 각 스트림에 대한 자세한 내용은 후속 섹션에 제공됩니다.

| Stream | 설명 | 게시됨 | 테스트 |
|:--- |:--- |:--- |:--- |
| 출력 |Toobe 다른 runbook에서 사용을 위한 개체입니다. |Toohello 작업 기록을 작성 합니다. |Hello 테스트 출력 창에에서 표시 합니다. |
| Warning |Hello 사용자를 위한 경고 메시지입니다. |Toohello 작업 기록을 작성 합니다. |Hello 테스트 출력 창에에서 표시 합니다. |
| 오류 |Hello 사용자를 위한 오류 메시지입니다. 예외와 달리 hello runbook는 기본적으로 오류 메시지가 표시 된 후 계속합니다. |Toohello 작업 기록을 작성 합니다. |Hello 테스트 출력 창에에서 표시 합니다. |
| 자세한 정보 표시 |일반 또는 디버깅 정보를 제공하는 메시지입니다. |Hello runbook에 대 한 자세한 정보 로깅이 켜 집니다 경우 toojob 기록만 기록 합니다. |$VerbosePreference tooContinue hello runbook에서 설정한 경우에 hello 테스트 출력 창에 표시 합니다. |
| 진행 |레코드가 hello runbook의 각 활동 전후에 자동으로 생성 됩니다. hello runbook 하지 않아야 toocreate 자체 진행률 레코드는 대화형 사용자 용는 이므로 합니다. |Hello runbook에 대 한 진행률 로깅이 켜 집니다 경우 toojob 기록만 기록 합니다. |Hello 테스트 출력 창에에서 표시 되지 않습니다. |
| 디버그 |대화형 사용자를 위한 메시지입니다. Runbook에서 사용하지 않아야 합니다. |Toojob 기록에 작성 되지 않습니다. |출력 창 tooTest 작성 되지 않습니다. |

## <a name="output-stream"></a>출력 스트림
hello 출력 스트림에 정상적으로 실행 되는 스크립트나 워크플로에 의해 생성 된 개체의 출력을 위한 것입니다. Azure 자동화에서이 스트림은 주로 사용 사용한 위한 개체 toobe [hello 현재 runbook을 호출 하는 부모 runbook](automation-child-runbooks.md)합니다. 때 있습니다 [인라인으로 runbook을 호출](automation-child-runbooks.md#invoking-a-child-runbook-using-inline-execution) 부모 runbook에서 출력 스트림이 toohello 부모 hello에서에서 데이터를 반환 합니다. 다른 runbook에서 hello runbook을 호출 하지 않음을 알고 있는 경우에 hello 출력 스트림 toocommunicate 일반 정보 백 toohello 사용자를 사용 해야 합니다. 그러나 모범 사례로, 일반적으로 사용 해야 hello [Verbose Stream](#Verbose) toocommunicate 일반 정보 toohello 사용자입니다.

Toohello 출력 스트림을 사용 하 여 데이터를 작성할 수 있습니다 [Write-output](http://technet.microsoft.com/library/hh849921.aspx) hello 개체 hello runbook의 자체 줄에 배치 하 여 합니다.

    #hello following lines both write an object toohello output stream.
    Write-Output –InputObject $object
    $object

### <a name="output-from-a-function"></a>함수에서 출력
Runbook에 포함 하는 함수에서 출력 스트림에 toohello를 작성 하면 뒤로 toohello runbook hello 출력에 전달 됩니다. Hello runbook이 해당 출력 tooa 변수를 할당 하는 경우 다음 작성 되지 않습니다 toohello 출력 스트림입니다. Tooany hello 함수 내에서 다른 스트림에 작성 toohello hello runbook에 대 한 해당 스트림에 데이터가 작성 됩니다.

다음 샘플 runbook hello를 것이 좋습니다.

    Workflow Test-Runbook
    {
        Write-Verbose "Verbose outside of function" -Verbose
        Write-Output "Output outside of function"
        $functionOutput = Test-Function
        $functionOutput

    Function Test-Function
     {
        Write-Verbose "Verbose inside of function" -Verbose
        Write-Output "Output inside of function"
      }
    }


hello hello runbook 작업 출력 스트림은 다음과 같습니다.

    Output inside of function
    Output outside of function

hello hello runbook 작업에 대 한 자세한 정보 스트림은 다음과 같습니다.

    Verbose outside of function
    Verbose inside of function

Hello runbook을 게시 한 후 및 시작 하기 전에 자세한 정보 로깅을 순서 tooget hello 자세한 정보 스트림 출력의에서 hello runbook 설정에서를 설정 해야 합니다.

### <a name="declaring-output-data-type"></a>출력 데이터 형식 선언
워크플로 hello를 사용 하 여 해당 출력의 hello 데이터 형식을 지정할 수 [OutputType 특성](http://technet.microsoft.com/library/hh847785.aspx)합니다. 이 특성은 런타임 중에 영향을 주지 않습니다 있지만 hello runbook의 hello 예상 출력 디자인 타임에 toohello runbook 작성자를 표시 합니다. Runbook에 대 한 hello 도구 집합 계속 tooevolve, 디자인 타임에 출력 데이터 형식을 선언의 hello 중요성 중요도 증가 합니다. 결과적으로,는 것이 좋습니다 tooinclude 만드는 모든 runbook이 선언 됩니다.

다음은 예제 출력 형식의 목록입니다.

* System.String
* System.Int32
* System.Collections.Hashtable
* Microsoft.Azure.Commands.Compute.Models.PSVirtualMachine

hello 다음 샘플 runbook은 문자열 개체를 출력 하 고 해당 출력 형식의 선언을 포함 합니다. Runbook이 특정 형식의 배열을 출력 하는 경우 지정 해야 합니다 여전히 hello 유형 hello 형식의 것과 반대로 tooan 배열로 합니다.

    Workflow Test-Runbook
    {
       [OutputType([string])]

       $output = "This is some string output."
       Write-Output $output
    }

toodeclare Grapical 또는 그래픽 PowerShell 워크플로 runbook에는 출력 유형, hello를 선택할 수 있습니다 **입력 및 출력** 출력 형식이 메뉴 옵션과 hello의 hello 이름 입력 합니다.  Hello 전체.NET 클래스 이름을 toomake를 사용 하는 것이 좋습니다 부모 runbook에서 참조 하는 경우 쉽게 식별할 수 있는 것입니다.  이 hello runbook에서 해당 클래스 toohello 데이터 버스의 모든 hello 속성을 표시 하 고 hello runbook 내에서 다른 작업에 대 한 값으로 참조 하 고 로깅을 조건부 논리를 사용 하는 경우 많은 유연성을 제공 합니다.<br> ![Runbook 입력 및 출력 옵션](media/automation-runbook-output-and-messages/runbook-menu-input-and-output-option.png)

다음 예제는 hello,이 기능이 두 그래픽 runbook toodemonstrate 포함 했습니다.  Hello로 사용 되는 하나의 runbook hello 모듈식 runbook 디자인 모델을 적용 했으므로 *인증 Runbook 템플릿* 실행 계정 hello를 사용 하 여 Azure 인증을 관리 합니다.  이 두 번째 runbook을이 hello 핵심 논리 tooautomate 지정된 된 시나리오를 일반적으로 수행,이 경우 진행 되는 tooexecute hello *인증 Runbook 템플릿을* hello 결과 tooyour 표시 **테스트** 출력 창.  정상적인 상황에서는 hello 자식 runbook에서 리소스 활용 hello 출력에 대해 작업을 수행 합니다.이 runbook에서는 것입니다.    

다음은 hello의 기본 논리 hello **AuthenticateTo Azure** runbook입니다.<br> ![Runbook 템플릿 예제 인증](media/automation-runbook-output-and-messages/runbook-authentication-template할 경우 Azure 관리 포털에서 각 스트림 및 동작에 대한 간략한 설명을 제공합니다.png)할 경우 Azure 관리 포털에서 각 스트림 및 동작에 대한 간략한 설명을 제공합니다.  

포함 hello 출력 유형을 *Microsoft.Azure.Commands.Profile.Models.PSAzureContext*, 하는 hello 인증 프로필 속성을 반환 합니다.<br> ![Runbook 출력 형식 예제](media/automation-runbook-output-and-messages/runbook-input-and-output-add-blade.png) 

이 runbook은 매우 단순 합니다, 여기서 하나의 구성 항목 toocall이 있습니다.  hello 마지막 활동이 실행 hello **Write-output** cmdlet 및 쓰기 hello PowerShell 식을 사용 하 여 hello에 대 한 프로필 데이터 tooa $_ 변수 **Inputobject** 하는 데 필요한 매개 변수 cmdlet 사용 합니다.  

이 예에서 두 번째 runbook hello에 대 한 명명 된 *테스트 ChildOutputType*, 두 개의 활동 하기만 했습니다.<br> ![예제 자식 출력 형식 Runbook](media/automation-runbook-output-and-messages/runbook-display-authentication-results-example.png) 

hello를 호출 하는 첫 번째 활동 hello **AuthenticateTo Azure** runbook과 hello 두 번째 활동 실행 hello **Write-verbose** hello 사용 하 여 cmdlet **데이터 원본** 의 **활동 출력** hello 값과 **필드 경로** 은 **Context.Subscription.SubscriptionName**, hello hello 상황에 맞는 출력을 지정 하는  **AuthenticateTo Azure** runbook입니다.<br> ![Write-Verbose cmdlet 매개 변수 데이터 원본](media/automation-runbook-output-and-messages/runbook-write-verbose-parameters-config.png)    

hello 결과 출력에는 hello 구독 hello 이름입니다.<br> ![Test-ChildOutputType Runbook 결과](media/automation-runbook-output-and-messages/runbook-test-childoutputtype-results.png)

참고로, hello 출력 형식 컨트롤의 hello 동작 합니다.  Hello 입력에 hello 출력 형식 필드의 값 및 출력 속성 블레이드를 입력 하는 경우 hello 컨트롤에서 인식 하 여 항목 toobe 하려면에서를 입력 한 후 tooclick hello 제어할 수 있습니다.  

## <a name="message-streams"></a>메시지 스트림
Hello 출력 스트림과 달리 메시지 스트림은 의도 한 toocommunicate 정보 toohello 사용자 있습니다. 다른 종류의 정보에 대한 여러 메시지 스트림이 있으며 각각 Azure Automation에서 다르게 처리됩니다.

### <a name="warning-and-error-streams"></a>경고 및 오류 스트림
hello 경고 및 오류 스트림은 runbook에서 발생 하는 의도 한 toolog 문제 됩니다. Runbook이 실행 되 고 runbook을 테스트할 때 hello Azure 관리 포털에에서 hello 테스트 출력 창에에서 포함 됩니다 때 toohello 작업 기록이 작성 됩니다. 기본적으로 hello runbook은 경고나 오류가 발생 한 후 실행 계속 됩니다. 해당 hello runbook이 일시 중단 경고 또는 오류에서 설정 하 여 지정할 수는 [기본 설정 변수](#PreferenceVariables) hello 메시지를 만들기 전에 hello runbook에서 합니다. 예를 들어 오류 발생 시 runbook toosuspend toocause 예외가 발생 한 것 처럼 설정 **$ErrorActionPreference** tooStop 합니다.

Hello를 사용 하 여 경고 또는 오류 메시지를 만들 [Write-warning](https://technet.microsoft.com/library/hh849931.aspx) 또는 [Write-error](http://technet.microsoft.com/library/hh849962.aspx) cmdlet. 활동은 toothese 스트림을 작성할 수도 있습니다.

    #hello following lines create a warning message and then an error message that will suspend hello runbook.

    $ErrorActionPreference = "Stop"
    Write-Warning –Message "This is a warning message."
    Write-Error –Message "This is an error message that will stop hello runbook because of hello preference variable."

### <a name="verbose-stream"></a>자세한 정보 표시 스트림
hello 자세한 정보 메시지 스트림은 runbook 작업 hello에 대 한 일반 정보입니다. Hello 이후 [디버그 스트림](#Debug) 사용할 수 없으면 runbook에서는 디버그 정보에 대 한 자세한 정보 메시지를 사용 합니다. 기본적으로 게시 된 runbook의 자세한 정보 메시지 hello 작업 기록에 저장 되지 않습니다. toostore 자세한 정보 메시지를 hello Azure 관리 포털에서에서 hello runbook의 hello 구성 탭에서 게시 된 runbook tooLog 상세 레코드를 구성 합니다. 대부분의 경우에서 성능상의 이유로 runbook에 대 한 상세 레코드를 기록 하지 않는 hello 기본 설정을 유지 해야 합니다. 이 옵션의 유일한 tootroubleshoot 하거나 runbook을 디버그 합니다.

때 [runbook을 테스트](automation-testing-runbook.md), hello runbook이 상세 레코드 toolog 구성 된 경우에 자세한 정보 메시지가 표시 되지 않습니다. 하는 동안 자세한 정보 메시지 toodisplay [runbook을 테스트](automation-testing-runbook.md), hello $VerbosePreference 변수 tooContinue 설정 해야 합니다. 해당 변수를 설정 하면 자세한 정보 메시지 hello hello Azure 포털의 테스트 출력 창에에서 표시 됩니다.

Hello를 사용 하 여 자세한 정보 메시지를 만들 [Write-verbose](http://technet.microsoft.com/library/hh849951.aspx) cmdlet.

    #hello following line creates a verbose message.

    Write-Verbose –Message "This is a verbose message."

### <a name="debug-stream"></a>디버그 스트림
hello 디버그 스트림은 대화형 사용자로 사용 하기 위한 및 runbook에 사용할 수 없습니다.

## <a name="progress-records"></a>진행률 레코드
구성 하는 경우 hello 구성 탭에서 hello Azure 포털에서에서 hello runbook의 runbook toolog 진행률 레코드를 후에 레코드가 작성 됩니다 toohello 작업 기록 각 활동 실행 전과 합니다. 대부분의 경우에서 주문 toomaximize 성능에는 runbook에 대 한 진행률 레코드를 기록 하지 않는 hello 기본 설정을 유지 해야 합니다. 이 옵션의 유일한 tootroubleshoot 하거나 runbook을 디버그 합니다. Runbook을 테스트할 때는 진행률 메시지가 hello runbook은 구성 된 toolog 진행률 레코드는 경우에 표시 되지 않습니다.

hello [Write-progress](http://technet.microsoft.com/library/hh849902.aspx) 은 대화형 사용자 용 cmdlet은 runbook에서는 유효 하지 않습니다.

## <a name="preference-variables"></a>기본 설정 변수
Windows PowerShell 사용 하 여 [기본 설정 변수](http://technet.microsoft.com/library/hh847796.aspx) toodetermine toorespond 전송 toodata toodifferent 출력 스트림 하는 방법입니다. 다른 스트림으로 전송 toodata 응답 방식을 runbook toocontrol에서 이러한 변수를 설정할 수 있습니다.

hello 다음 표 유효한 runbook과 기본 값에 사용할 수 있는 hello 기본 설정 변수입니다. 참고가이 표에 runbook에서 유효한 hello 값만 포함 합니다. 추가 값이 Azure 자동화 외부의 Windows PowerShell에서 사용 될 때 hello 기본 설정 변수에 대해 유효 합니다.

| 변수 | 기본값 | 유효한 값 |
|:--- |:--- |:--- |
| WarningPreference |계속 |중지<br>계속<br>SilentlyContinue |
| ErrorActionPreference |계속 |중지<br>계속<br>SilentlyContinue |
| VerbosePreference |SilentlyContinue |중지<br>계속<br>SilentlyContinue |

다음 표에서 hello runbook에서 사용할 수 있는 hello 기본 설정 변수 값에 대 한 hello 동작을 나열 합니다.

| 값 | 동작 |
|:--- |:--- |
| 계속 |Hello 메시지를 기록 하 고 hello runbook 실행을 계속 합니다. |
| SilentlyContinue |Hello 메시지를 기록 하지 않고 hello runbook 실행을 계속 합니다. 이 hello hello 메시지를 무시 합니다. |
| 중지 |Hello 메시지를 기록 하 고 hello runbook을 일시 중단 합니다. |

## <a name="retrieving-runbook-output-and-messages"></a>Runbook 출력 및 메시지 검색
### <a name="azure-portal"></a>Azure portal
Hello hello runbook 작업 탭에서 Azure 포털에서에서 runbook 작업의 hello 세부 정보를 볼 수 있습니다. hello 입력된 매개 변수 및 hello hello hello 작업의 요약이 표시 됩니다. [출력 스트림에](#Output) hello 작업 및 발생 한 경우에 모든 예외에 대 한 추가 toogeneral 정보입니다. hello 기록 hello 메시지에 포함 됩니다 [출력 스트림에](#Output) 및 [경고 및 오류 스트림](#WarningError) 더하기 toohello에 [Verbose Stream](#Verbose) 및 [진행 중 레코드](#Progress) hello runbook이 구성 된 toolog 자세한 정보 표시 레코드와 진행률 레코드입니다.

### <a name="windows-powershell"></a>Windows PowerShell
Windows PowerShell에서 검색할 수 있습니다 출력 및 메시지 hello를 사용 하 여 runbook에서 [Get-azureautomationjoboutput](https://msdn.microsoft.com/library/mt603476.aspx) cmdlet. 이 cmdlet에 hello hello 작업의 ID 매개 변수 스트림을 지정 하는 스트림 tooreturn 호출한 필요 합니다. 모든 tooreturn hello 작업에 대 한 모든 스트림을 지정할 수 있습니다.

다음 예제는 hello toocomplete 샘플 runbook 및 대기를 시작 합니다. 완료 되 면 해당 출력 스트림이 hello 작업에서 수집 됩니다.

    $job = Start-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook"

    $doLoop = $true
    While ($doLoop) {
       $job = Get-AzureRmAutomationJob -ResourceGroupName "ResourceGroup01" `
       –AutomationAccountName "MyAutomationAccount" -Id $job.JobId
       $status = $job.Status
       $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped")
    }

    Get-AzureRmAutomationJobOutput -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" -Id $job.JobId –Stream Output

### <a name="graphical-authoring"></a>그래픽 작성
그래픽 runbook에 대 한 추가 로깅은 활동 수준 추적의 hello 형식으로 사용할 수 있습니다.  추적에는 기본 추적과 자세히 추적이 있습니다.  기본 추적에서 시작 하는 hello를 볼 수 있습니다 및 정보와 함께 hello runbook의 각 작업의 종료 시간 관련 시도 횟수 및 hello 활동의 시작 시간과 같은 tooany 활동 다시 시도 합니다.  자세히 추적에서는 기본 추적 외에도 각 작업에 대한 입력 및 출력 데이터를 얻습니다.  Note는 현재 hello 추적 레코드가 기록 hello 자세한 정보 스트림을 사용 하 여 추적을 사용 하도록 설정 하면 자세한 정보 로깅을 활성화 해야 합니다.  그래픽 runbook 추적 사용에 대 한 않아도가 됩니다 toolog 진행률 레코드 고 때문에 hello 기본 추적 하는 데 사용 같은 목적으로 hello 자세한 정보를 제공 합니다.

![그래픽 작성 작업 스트림 보기](media/automation-runbook-output-and-messages/job-streams-view-blade.png)

자세한 정보 표시 로깅 및 그래픽 runbook에 대 한 추적을 사용 하도록 설정 하면 훨씬 더 많은 정보는 hello 프로덕션 작업 스트림 보기에서 사용할 수 있는 스크린 샷 위에 hello에서 볼 수 있습니다.  이러한 추가 정보는 Runbook을 사용하는 프로덕션 문제 해결에 필요할 수 있으므로 그 목적으로만 사용하고 일반적으로는 사용하지 않습니다.    
hello 추적 레코드는 특히 여러 개일 수 있습니다.  그래픽 runbook으로 추적 하면 기본 또는 자세한 추적을 구성 했는지 여부에 따라 활동 당 두 개의 toofour 레코드 가져올 수 있습니다.  이 정보 tootrack hello 진행 되는 runbook의 문제 해결을 위해 필요 하지 않으면 추적 해제 tookeep을 할 수 있습니다.

**tooenable 활동 수준 추적 hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 자동화 계정을 엽니다.
2. Hello 클릭 **Runbook** runbook의 타일 tooopen hello 목록입니다.
3. Hello Runbook 블레이드에서 tooselect 그래픽 runbook의 runbook 목록에서를 클릭 합니다.
4. Hello 선택한 runbook에 대 한 hello 설정 블레이드에서 클릭 **로깅 및 추적**합니다.
5. Hello에서 로깅 및 추적 블레이드 상세 레코드 기록에서 클릭 **에** tooenable 자세한 정보 로깅 및 udner 활동 수준 추적 hello 추적 수준을 변경**기본** 또는 **Detailed**  필요한 간 추적의 hello 수준을 기반으로 합니다.<br>
   
   ![그래픽 작성 로깅 및 추적 블레이드](media/automation-runbook-output-and-messages/logging-and-tracing-settings-blade.png)

### <a name="microsoft-operations-management-suite-oms-log-analytics"></a>Microsoft OMS(Operations Management Suite) Log Analytics
자동화는 runbook 작업 상태 및 작업 스트림을 tooyour Microsoft Operations Management Suite (OMS) 로그 분석 작업 영역을 보낼 수 있습니다.  Log Anaytics를 사용하여 다음을 수행할 수 있습니다.

* 자동화 작업에 대한 통찰력 확보 
* Runbook 작업 상태(예: 실패 또는 일시 중단)를 기반으로 전자 메일 또는 경고 트리거 
* 작업 스트림에서 고급 쿼리 작성 
* 자동화 계정 간에 작업 상호 연결 
* 시간별 작업 기록 시각화    

로그 분석 toocollect와 tooconfigure 통합 상관 관계를 지정 하 고 작업 데이터 작업을 수행 하는 방법에 대 한 자세한 내용은 참조 하십시오. [자동화 tooLog 분석 (OMS)에서 작업 상태 및 작업 스트림 전달](automation-manage-send-joblogs-log-analytics.md)합니다.

## <a name="next-steps"></a>다음 단계
* toolearn toomonitor runbook 작업 및 기타 기술 정보가 참조 하는 방법 runbook 실행에 대 한 자세한 [runbook 작업을 추적 합니다.](automation-runbook-execution.md)
* toodesign 및 사용 하 여 자식 runbook을 확인 하려면 어떻게 해야 toounderstand [Azure 자동화에서 자식 runbook](automation-child-runbooks.md)

