---
title: "Azure 자동화에 대 한 PowerShell 워크플로 aaaLearning | Microsoft Docs"
description: "이 문서는 PowerShell toounderstand hello PowerShell 및 PowerShell 워크플로 및 적용 가능한 tooAutomation runbook 개념 간의 구체적인 차이점에 잘 알고 저자에 대 한 간략 한 설명은로 제공 됩니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 84bf133e-5343-4e0e-8d6c-bb14304a70db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 362c504eb96d31b99a826b128e6a591beecaa084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a>Automation runbook에 대한 주요 Windows PowerShell 워크플로 개념 학습 
Azure 자동화의 Runbook은 Windows PowerShell 워크플로로 구현됩니다.  Windows PowerShell 워크플로 비슷한 tooa Windows PowerShell 스크립트 했으나 tooa 새 사용자를 혼동 될 수 있는 몇 가지 중요 한 차이점이 있습니다.  이 문서는 PowerShell 워크플로 사용 하 여 runbook을 작성 하는 의도 한 toohelp 상태인 동안에 검사점 필요 하지 않으면 PowerShell을 사용 하 여 runbook을 작성 하는 것이 좋습니다.  다음과 같이 차이가 구문 PowerShell 워크플로 runbook을 작성할 때 및 이러한 차이점 작업 toowrite 효과적인 워크플로 좀 더 필요 합니다.  

워크플로 장기 실행 작업을 수행 하거나 여러 장치 또는 관리 되는 노드 사이에서 여러 단계의 조정을 hello를 해야 하는 프로그래밍 방식의 연결 된 단계의 시퀀스입니다. hello의 표준 스크립트에서 워크플로의 점으로 hello 기능이 포함 toosimultaneously 여러 장치에 대해 작업을 수행 하 고 hello 기능 tooautomatically 오류를 복구 합니다. Windows PowerShell 워크플로는 Windows Workflow Foundation을 활용하는 Windows PowerShell 스크립트입니다. Hello 워크플로 Windows PowerShell 구문을 사용 하 여 작성 하 고 Windows PowerShell에서 실행 하는 동안 Windows Workflow Foundation에서 처리 됩니다.

이 문서의 hello 항목에 대 한 자세한 내용은 참조 하십시오. [Windows PowerShell 워크플로 시작](http://technet.microsoft.com/library/jj134242.aspx)합니다.

## <a name="basic-structure-of-a-workflow"></a>워크플로의 기본 구조
hello 첫 번째 단계 tooconverting PowerShell 스크립트 tooa PowerShell 워크플로 빠뜨렸거나 hello **워크플로** 키워드입니다.  워크플로 hello로 시작 **워크플로** 키워드 다음에 오는 중괄호 hello 스크립트의 hello 본문입니다. hello 워크플로의 hello 이름은 hello **워크플로** hello 구문 다음에 표시 된 대로 키워드:

    Workflow Test-Workflow
    {
       <Commands>
    }

hello 워크플로의 hello 이름을 hello 자동화 runbook의 hello 이름이 일치 해야 합니다. Hello runbook을 가져오는 경우 hello filename hello 워크플로 이름과 일치 해야 하 고 끝나야 합니다. *.ps1*합니다.

tooadd 매개 변수 toohello 워크플로 사용 하 여 hello **Param** tooa 스크립트와 마찬가지로 키워드입니다.

## <a name="code-changes"></a>코드 변경 내용
PowerShell 워크플로 코드에서는 몇 가지 중요 한 변경 제외 하 고 거의 동일한 tooPowerShell 스크립트 코드를 찾습니다.  hello 다음 섹션에서는 할 toomake tooa PowerShell 스크립트에 대 한 워크플로에서 toorun 변경에 설명 합니다.

### <a name="activities"></a>활동
활동은 워크플로의 특정 작업입니다. 하나 이상의 명령으로 구성된 스크립트와 마찬가지로 워크플로는 시퀀스로 수행되는 하나 이상의 활동으로 구성됩니다. Windows PowerShell 워크플로 자동으로 다양 한 Windows PowerShell cmdlet tooactivities hello 때 변환는 워크플로 실행 합니다. Runbook에서 이러한 cmdlet 중 하나를 지정 하면 Windows Workflow foundation hello 해당 작업이 실행 됩니다. 해당 하는 활동 없이 이러한 cmdlet에 대 한 Windows PowerShell 워크플로 자동으로 실행 내에서 hello cmdlet는 [InlineScript](#inlinescript) 활동입니다. InlineScript 블록에 명시적으로 포함하지 않으면 워크플로에서 제외되고 사용할 수 없는 cmdlet 집합이 있습니다. 이러한 개념에 자세한 내용은 [스크립트 워크플로에서 활동 사용](http://technet.microsoft.com/library/jj574194.aspx)을 참조하세요.

워크플로 활동 일반 매개 변수 tooconfigure 집합이 자신의 작업을 공유합니다. Hello 워크플로 일반 매개 변수에 대 한 세부 정보를 참조 하십시오. [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx)합니다.

### <a name="positional-parameters"></a>위치 매개 변수
워크플로에서 위치매개 변수는 활동 및 cmdlets와 같이 사용할 수 없습니다.  사용자가 매개 변수 이름을 사용해야 한다는 뜻입니다.

예를 들어, 코드를 실행 중인 모든 서비스를 가져오는 다음 hello를 것이 좋습니다.

     Get-Service | Where-Object {$_.Status -eq "Running"}

"지정 된 hello를 사용 하 여 집합을 확인할 수 없는 매개 변수 명명 된 매개 변수입니다."와 같은 메시지가 나타나면이 동일한 코드 워크플로에서 toorun 하면  toocorrect이 hello 다음과 같이 hello 매개 변수 이름을 지정 합니다.

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a>역직렬화된 개체
개체는 워크플로에서 역직렬화됩니다.  즉, 이 말은 해당 속성은 사용할수 있지만 메서드는 사용할 수 없다는 의미입니다.  예를 들어 hello를 hello 서비스 개체의 hello Stop 메서드를 사용 하 여 서비스를 중지 하는 PowerShell 코드를 따르는 것이 좋습니다.

    $Service = Get-Service -Name MyService
    $Service.Stop()

이 작업을 수행할 toorun 워크플로에서 "메서드 호출에서 Windows PowerShell 워크플로 지원 되지 않습니다." 라는 오류가 나타납니다.  

한 가지 옵션은 toowrap이 두 줄의 코드는 [InlineScript](#inlinescript) 어떤 $Service 되는 경우가 hello 블록 내에서 서비스 개체의 블록입니다.

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

두 번째 방법은 toouse 사용 가능한 경우 hello 메서드와 같은 기능을 수행 하는 또 다른 cmdlet에 hello 합니다.  이 샘플에서는 hello Stop-service cmdlet 제공 hello hello 중지 메서드를와 동일한 기능을 워크플로에 대 한 hello 다음을 사용할 수 있습니다.

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a>InlineScript
hello **InlineScript** 활동은 PowerShell 워크플로 대신 기존 PowerShell 스크립트로 toorun 명령을 하나 이상 필요한 경우에 유용 합니다.  워크플로의 명령을 처리를 위해 tooWindows Workflow Foundation 보내는 동안 InlineScript 블록의 명령은 Windows PowerShell에서 처리 됩니다.

InlineScript는 아래 표시 된 구문 다음 hello를 사용 합니다.

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

InlineScript에서 hello 출력 tooa 변수를 할당 하 여 출력을 반환할 수 있습니다. hello 다음 예제에서는 서비스를 중지 하 고 출력 hello 서비스 이름.

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


값을 InlineScript 블록으로 전달할 수 있지만, **$Using** 범위 한정자를 사용해야 합니다.  hello 다음 예제는 이전 예제와 동일한 toohello hello 서비스 이름이 제공 된 변수에서 있습니다.

    Workflow Stop-MyService
    {
        $ServiceName = "MyService"

        $Output = InlineScript {
            $Service = Get-Service -Name $Using:ServiceName
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


InlineScript 활동 특정 워크플로가에 중요 한 수 있지만, 워크플로 구성체를 지원 하지 않습니다 하며 이유 뒤 hello에 대 한 필요한 경우에 사용 해야 합니다.

* InlineScript 블록 내에서는 [검사점](#checkpoints)을 사용할 수 없습니다. Hello 블록 내에서 실패 한 경우 hello 블록의 hello 시작 부분에서 재개 해야 합니다.
* InlineScriptBlock 내부에서는 [병렬 실행](#parallel-processing)을 사용할 수 없습니다.
* InlineScript은 hello hello InlineScript 블록의 전체 길이 대 한 hello Windows PowerShell 세션을 유지 하므로 hello 워크플로의 확장성을 영향을 줍니다.

InlineScript 사용에 대한 자세한 내용은 [워크플로에서 Windows PowerShell 명령 실행](http://technet.microsoft.com/library/jj574197.aspx) 및 [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx)를 참조하세요.

## <a name="parallel-processing"></a>병렬 처리
Windows PowerShell 워크플로의 장점 중 하나는 hello 기능 tooperform 대신 병렬로 명령 집합을 순차적으로 일반적인 스크립트와 마찬가지로 합니다.

Hello를 사용할 수 있습니다 **병렬** 키워드 toocreate 여러 명령 동시에 실행 되는 스크립트 블록입니다. 이 구문 아래에 표시 된 다음 hello를 사용 합니다. Y 1과 Activity2 hello에서 시작 하는 경우에 한 번입니다. Activity3는 Activity1과 Activity2가 모두 완료된 후에만 시작됩니다.

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


예를 들어 hello를 다음 PowerShell 명령을 여러 파일 tooa 네트워크 대상에 복사 하는 것이 좋습니다.  이 명령은 순차적으로 실행 되므로 파일 하나만 다음 hello를 시작 하기 전에 복사 완료 되어야 합니다.     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

hello 다음 워크플로 실행를 모두 복사를 시작할 hello 동일 동시에 명령을 동일 이러한 시간입니다.  모든 후에 복사 hello 완료 메시지가 표시 됩니다.

    Workflow Copy-Files
    {
        Parallel
        {
            Copy-Item -Path "C:\LocalPath\File1.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File2.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File3.txt" -Destination "\\NetworkPath"
        }

        Write-Output "Files copied."
    }


Hello를 사용할 수 있습니다 **ForEach-Parallel** 동시에 컬렉션의 각 항목에 대 한 tooprocess 명령을 생성 합니다. hello 컬렉션의 항목 hello hello 스크립트 블록의 hello 명령은 순차적으로 실행 하는 반면 병렬로 처리 됩니다. 이 구문 아래에 표시 된 다음 hello를 사용 합니다. 이 경우 Activity1부터 hello에 대해 동일한 시간 hello 컬렉션의 모든 항목이 있습니다. 각 항목에 대해 Activity2는 Activity1이 완료된 후에 시작됩니다. Activity3는 모든 항목에 대해 Activity1과 Activity2가 모두 완료된 후에만 시작됩니다.

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

다음 예제는 hello는 동시에 파일을 복사 하는 유사한 toohello 이전 예입니다.  이 경우 복사한 후 각 파일에 대 한 메시지가 표시 됩니다.  모든 후에 완전히 복사 hello 최종 완료 메시지가 표시 됩니다.

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach -Parallel ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
        }

        Write-Output "All files copied."
    }

> [!NOTE]
> Toogive 신뢰할 수 없는 결과 표시 된이 이후 동시에 자식 runbook을 실행 하는 것은 좋지 않습니다.  hello 때로는 hello 자식 runbook의 출력 표시 되지 않으면, 한 자식 runbook의 설정에 영향을 줄 수 및 기타 병렬 자식 runbook hello
>

## <a name="checkpoints"></a>검사점
A *검사점* hello hello 변수에 대 한 현재 값을 포함 하는 hello 워크플로의 현재 상태 스냅숏을 이며 생성 된 toothat 지점 출력 합니다. 워크플로 오류에서 종료 되거나 일시 중단, 한 다음 hello 다음 그가 실행 될 때 시작 됩니다 hello 워크플로의 hello 시작 하는 대신, 마지막 검사점.  Hello 사용 하 여 워크플로에서 검사점을 설정할 수 있습니다 **Checkpoint-workflow** 활동입니다.

다음 샘플 코드는 hello, 워크플로 tooend hello Activity2 발생 후 예외가 발생 합니다. Hello 워크플로 다시 실행 하는 경우 마지막 검사점 hello 설정 후에 바로이 된 이후 Activity2를 실행 하 여 시작 합니다.

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

Hello 워크플로 다시 시작한 경우 발생 하기 쉬운 tooexception 수 있으며 되지 않아야 하는 활동 반복 후 워크플로에서 검사점을 설정 해야 합니다. 예를 들어 Runbook에서 가상 컴퓨터를 만들 수 있습니다. 이전과 이후에 hello 명령 toocreate hello 가상 컴퓨터 검사점을 설정할 수 있습니다. Hello 만들기에 실패 하면 다음 hello 명령은 반복 될 hello 워크플로 다시 시작 하는 경우. Hello 워크플로 hello 만들기가 성공 후 오류가 발생 하면 다음 hello 가상 컴퓨터가 만들어지지 않습니다 다시 hello 워크플로 다시 시작할 때입니다.

다음 예제는 hello 여러 파일 tooa 네트워크 위치에 복사 하 고 각 파일 다음 검사점을 설정 합니다.  Hello 네트워크 위치를 잃어버린 경우 hello 워크플로 오류에서 종료 됩니다.  다시 시작 되 면 이미 복사 된 hello 파일만 건너뜁니다 의미 hello 마지막 검사점에서 다시 시작 됩니다.

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
            Checkpoint-Workflow
        }

        Write-Output "All files copied."
    }

Username 자격 증명은 hello를 호출한 후 지속 되지 않으므로 [Suspend-workflow](https://technet.microsoft.com/library/jj733586.aspx) 활동 hello 마지막 검사점 이후에 tooset hello 자격 증명 toonull 필요 하 고이 다음 검색 하 다시 hello 자산 저장소에서 후또는 **Suspend-workflow** 또는 검사점을 호출 합니다.  그렇지 않으면 hello 다음과 같은 오류 메시지가 나타날 수 있습니다: *hello 워크플로 작업을 다시 시작할 수 없습니다, 하거나 지 속성 데이터를 완전히 저장 하거나 저장할 수 없습니다 때문에 지 속성 데이터 손상 되었습니다. Hello 워크플로 다시 시작 해야 합니다.*

동일한 코드 다음 hello 보여 줍니다. 방법을 toohandle PowerShell 워크플로 runbook의이 있습니다.

    workflow CreateTestVms
    {
       $Cred = Get-AzureAutomationCredential -Name "MyCredential"
       $null = Add-AzureRmAccount -Credential $Cred

       $VmsToCreate = Get-AzureAutomationVariable -Name "VmsToCreate"

       foreach ($VmName in $VmsToCreate)
         {
          # Do work first toocreate hello VM (code not shown)

          # Now add hello VM
          New-AzureRmVm -VM $Vm -Location "WestUs" -ResourceGroupName "ResourceGroup01"

          # Checkpoint so that VM creation is not repeated if workflow suspends
          $Cred = $null
          Checkpoint-Workflow
          $Cred = Get-AzureAutomationCredential -Name "MyCredential"
          $null = Add-AzureRmAccount -Credential $Cred
         }
     }


서비스 주체로 구성된 실행 계정을 사용하여 인증하는 경우에는 필요하지 않습니다.  

검사점에 대 한 자세한 내용은 참조 [스크립트 워크플로에 검사점 추가 tooa](http://technet.microsoft.com/library/jj574114.aspx)합니다.

## <a name="next-steps"></a>다음 단계
* PowerShell 워크플로 runbook 시작 tooget 참조 [내 첫 번째 PowerShell 워크플로 runbook](automation-first-runbook-textual.md)
