---
title: "Azure 자동화에서 첫 번째 PowerShell 워크플로 runbook aaaMy | Microsoft Docs"
description: "Hello 개발, 테스트 및 PowerShell 워크플로 사용 하 여 간단한 텍스트 runbook의 게시 하는 과정을 안내 하는 자습서입니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "Powershell 워크플로, Powershell 워크플로 예제, 워크플로 Powershell"
ms.assetid: 0002d7f7-e2b5-46e3-b5eb-4596b84fd526
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/26/2017
ms.author: magoedte;bwren
ms.openlocfilehash: b5a34d363ef4865878f3f68119833367b5280f83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="my-first-powershell-workflow-runbook"></a>내 첫 번째 PowerShell 워크플로 Runbook

> [!div class="op_single_selector"]
> * [그래픽](automation-first-runbook-graphical.md)
> * [PowerShell](automation-first-runbook-textual-powershell.md)
> * [PowerShell 워크플로](automation-first-runbook-textual.md)
> 
> 

이 자습서에서는 hello 만드는 과정을 [PowerShell 워크플로 runbook](automation-runbook-types.md#powershell-workflow-runbooks) Azure 자동화에서 합니다. 테스트 및 tootrack hello runbook 작업의 상태를 hello 하는 방법을 설명 하는 동안 게시 하는 단순한 runbook으로 시작 합니다. 다음 hello runbook을 수정 했습니다 tooactually이 경우에 Azure 가상 컴퓨터를 시작 하는 Azure 리소스를 관리 합니다. 마지막으로 runbook 매개 변수를 추가 하 여 runbook 보다 강력한 hello으로 만듭니다.

## <a name="prerequisites"></a>필수 조건
toocomplete이이 자습서에서는 다음 hello 필요 합니다.

* 동작합니다. 계정이 아직 없는 경우 [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)하거나 <a href="/pricing/free-account/" target="_blank">[무료 계정을 등록](https://azure.microsoft.com/free/)할 수 있습니다.
* [자동화 계정](automation-sec-configure-azure-runas-account.md) toohold runbook hello 및 tooAzure 리소스를 인증 합니다.  이 계정은 권한 toostart 있고 hello 가상 컴퓨터를 중지 해야 합니다.
* Azure 가상 컴퓨터. 프로덕션 VM이 되지 않도록 이 가상 컴퓨터를 중지하고 시작합니다.

## <a name="step-1---create-new-runbook"></a>1 단계-새 runbook 만들기
Hello 텍스트를 출력 하는 단순한 runbook을 만들어 시작 하겠습니다 *Hello World*합니다.

1. Hello Azure 포털에서에서 자동화 계정을 엽니다.  
   hello 자동화 계정 페이지에서이 계정을 hello 리소스의 빠른 보기를 제공합니다. 사용자에게는 이미 일부 자산이 있어야 합니다. 그 중 대부분은 hello 모듈 새 자동화 계정에 자동으로 포함 됩니다. Hello에 나와 있는 hello 자격 증명 자산 있어야 [필수 구성 요소](#prerequisites)합니다.
2. Hello 클릭 **Runbook** runbook의 타일 tooopen hello 목록입니다.<br><br> ![Runbook 컨트롤](media/automation-first-runbook-textual/runbooks-control-tiles.png)
3. Hello를 클릭 하 여 새 runbook을 만들려면 **runbook을 추가할** 단추 차례로 **새 runbook을 만들**합니다.
4. Runbook hello 이름을 hello *MyFirstRunbook 워크플로*합니다.
5. 이 예에서 여기 toocreate는 [PowerShell 워크플로 runbook](automation-runbook-types.md#powershell-workflow-runbooks) 선택 **Powershell 워크플로** 에 대 한 **Runbook 형식**합니다.<br><br> ![새 runbook](media/automation-first-runbook-textual/new-runbook-properties.png)
6. 클릭 **만들기** toocreate hello runbook 및 열기 hello 텍스트 편집기입니다.

## <a name="step-2---add-code-toohello-runbook"></a>2 단계-코드 toohello runbook 추가
Hello runbook에 직접 중 하나가 형식 코드를 할 수 있습니다 또는 hello 라이브러리 컨트롤에서에서 cmdlet, runbook 및 자산을 선택할 수 있습니다 및 관련된 매개 변수를 사용 하 여 toohello runbook을 추가 했습니다. 이 연습에서는 hello runbook에 직접 입력할 수 있습니다.

1. 이 runbook은 필요한 hello만로 현재 비어 *워크플로* 키워드, runbook, 취급 하 고 hello 전체 워크플로 표시할는 hello 중괄호 hello 이름입니다.

   ```
   Workflow MyFirstRunbook-Workflow
   {
   }
   ```
2. 중괄호 안에 *Write-Output "Hello World."* hello 중괄호 합니다.

   ```
   Workflow MyFirstRunbook-Workflow
   {
   Write-Output "Hello World"
   }
   ```
3. 클릭 하 여 hello runbook을 저장 **저장**합니다.<br><br> ![Runbook을 저장 합니다.](media/automation-first-runbook-textual/automation-runbook-edit-controls-save.png)

## <a name="step-3---test-hello-runbook"></a>3 단계-hello runbook 테스트
Hello runbook toomake를 게시 하기 전에 것 tootest 원하는 프로덕션 환경에서 사용할 수 있는 것 toomake 제대로 작동 합니다. Runbook을 테스트할 때 **초안** 버전을 실행하고 해당 출력을 대화형으로 봅니다.

1. 클릭 **테스트 창** tooopen hello 테스트 창.<br><br> ![테스트 창](media/automation-first-runbook-textual/automation-runbook-edit-controls-test.png)
2. 클릭 **시작** toostart hello 테스트 합니다. 이 경우에 사용할 수는 hello 옵션 이어야 합니다.
3. 이 창에서 [runbook 작업](automation-runbook-execution.md) 이 생성되고 상태를 보여줍니다.  
   작업 상태 hello로 시작 됩니다 *큐 대기* hello 클라우드 toocome 사용할 수 있는에 runbook worker를 대기 하 고 있음을 나타내는입니다. 도 이동 후 됩니다*시작* 작업자 hello 작업 요구 한 경우 다음 *실행* hello runbook 실제로 실행을 시작한 경우.  
4. Hello runbook 작업이 완료 되 면 해당 출력이 표시 됩니다. 여기서는 *Hello World*할 수 있습니다.<br><br> ![Hello World](media/automation-first-runbook-textual/test-output-hello-world.png)
5. Hello 테스트 창 tooreturn toohello 캔버스를 닫습니다.

## <a name="step-4---publish-and-start-hello-runbook"></a>4 단계-게시 하 고 hello runbook을 시작
방금 만든 hello runbook 초안 모드입니다. Toopublish 필요 전에 프로덕션 환경에서 실행할 수 있습니다. Runbook을 게시 하는 경우 hello 초안 버전으로 hello 기존의 게시 된 버전을 덮어씁니다. 경우에에서는 없는 게시 됨 버전 hello runbook 방금 만든 때문에 있습니다.

1. 클릭 **게시** toopublish hello runbook 차례로 **예** 대화 상자가 나타나면 합니다.<br><br> ![게시](media/automation-first-runbook-textual/automation-runbook-edit-controls-publish.png)
2. Hello에 왼쪽된 tooview hello runbook 스크롤하면 **Runbook** 창 이제 표시 됩니다는 **작성 상태** 의 **게시 됨**합니다.
3. 에 대 한 스크롤 백 toohello 오른쪽 tooview hello 창 **MyFirstRunbook 워크플로**합니다.  
   hello hello 위쪽 옵션 toostart hello runbook 수 있도록 허용 hello 미래에 toostart 예약 하거나, 한 [webhook](automation-webhooks.md) 시작 될 수 있도록 HTTP 호출을 통해.
4. Toostart hello runbook 원하는 이므로 클릭 **시작** 차례로 **예** 대화 상자가 나타나면 합니다.<br><br> ![Runbook 시작](media/automation-first-runbook-textual/automation-runbook-controls-start.png)
5. 방금 만든 hello runbook 작업에 대 한 작업 창이 열립니다. म이 창을 닫을 수 있지만 경우 두겠습니다 것 열려 있도록 hello 작업의 진행 상황을 볼 수 있습니다.
6. hello 작업 상태에 표시 되어 **작업 요약** 및 일치 hello 상태는 hello runbook을 테스트 했습니다에 대해 살펴보았습니다.<br><br> ![작업 요약](media/automation-first-runbook-textual/job-pane-status-blade-jobsummary.png)
7. 한 번 runbook 상태 표시를 hello *Completed*, 클릭 **출력**합니다. hello 출력 창이 열리며 볼 수 있습니다이 *Hello World*합니다.<br><br> ![작업 요약](media/automation-first-runbook-textual/job-pane-status-blade-outputtile.png)  
8. 닫기 hello 출력 창입니다.
9. 클릭 **모든 로그** hello runbook 작업에 대 한 tooopen hello 스트림 창. 에서는 행만 볼 *Hello World* hello 출력에서 스트림에 하지만이 표시할 수 있습니다 Verbose 및 오류와 같은 runbook 작업에 대 한 다른 스트림을 hello runbook toothem에 씁니다.<br><br> ![작업 요약](media/automation-first-runbook-textual/job-pane-status-blade-alllogstile.png)
10. Hello 스트림 창 및 hello 작업 창 tooreturn toohello MyFirstRunbook 창을 닫습니다.
11. 클릭 **작업** 이 runbook에 대 한 tooopen hello 작업 창. 이 runbook에서 생성 된 hello 작업을 모두 나열 합니다. म만 했습니다 hello 작업이 한 번 나열 되는 하나의 작업만 나타나야 합니다.<br><br> ![작업](media/automation-first-runbook-textual/runbook-control-job-tile.png)
12. 클릭할 때이 작업 tooopen hello 동일 hello runbook을 시작 했습니다. 있을 때 볼 것으로 구성 된 작업 창. 이렇게 하면 있습니다 toogo 다시 특정 runbook에 대해 만들어진 모든 작업의 시간과 보기 hello 세부 있습니다.

## <a name="step-5---add-authentication-toomanage-azure-resources"></a>5 단계-인증 toomanage 추가 Azure 리소스
지금까지 runbook을 테스트 하고 게시했지만, 딱히 유용하지는 않습니다. Azure 리소스를 관리 하는 toohave 주시기 바랍니다. 인증 없는 한 있지만 tooin hello 참조 hello 자격 증명을 사용 하 여 수 toodo 조금만 기다려 [필수 구성 요소](#prerequisites)합니다. Hello로 할까요 **추가 AzureRMAccount** cmdlet.

1. 클릭 하 여 텍스트 편집기를 열고 hello **편집** hello MyFirstRunbook 워크플로 창.<br><br> ![Runbook 편집](media/automation-first-runbook-textual/automation-runbook-controls-edit.png)
2. Hello 필요 하지 않으므로 **Write-output** 더 이상 줄, 고 삭제 합니다.
3. Hello 중괄호 사이 빈 줄에 hello 커서를 놓습니다.
4. 입력 하거나 복사 하 hello 다음 자동화 계정으로 실행 계정으로 hello 인증을 처리 하는 코드를 붙여 넣습니다.

   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   ```
5. 클릭 **테스트 창** 를 hello runbook을 테스트할 수 있습니다.
6. 클릭 **시작** toostart hello 테스트 합니다. 완료 되 면 다음 계정에서 기본 정보를 표시, 비슷한 toohello 출력 받아야 합니다. 해당 hello 자격 증명이 올바른지 확인 합니다.<br><br> ![인증](media/automation-first-runbook-textual/runbook-auth-output.png)

## <a name="step-6---add-code-toostart-a-virtual-machine"></a>6 단계-코드 toostart 가상 컴퓨터를 추가 합니다.
이제는 runbook은 tooour Azure 구독을 인증 하는 리소스를 관리할 수 있습니다. 명령 toostart 가상 컴퓨터를 추가합니다. Azure 구독에서 모든 가상 컴퓨터를 선택할 수 있습니다 및 지금은 하드 코딩 hello runbook의 이름을 지정 하는 것입니다.

1. 후 *추가 AzureRmAccount*, 형식 *시작 AzureRmVM-이름 'VMName'-'NameofResourceGroup' ResourceGroupName* hello 이름 및 가상 컴퓨터 toostart hello의 리소스 그룹 이름을 제공 하 합니다.  

   ```
   workflow MyFirstRunbook-Workflow
   {
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name 'VMName' -ResourceGroupName 'ResourceGroupName'
   }
   ```
2. Hello runbook을 저장 한 다음 클릭 **테스트 창** 를 테스트할 수 있습니다.
3. 클릭 **시작** toostart hello 테스트 합니다. 완료 되 면 해당 hello 가상 컴퓨터가 시작 된 확인 합니다.

## <a name="step-7---add-an-input-parameter-toohello-runbook"></a>7 단계-입력된 매개 변수 toohello runbook을 추가
이 runbook을 현재 시작 hello 가상 컴퓨터 hello runbook에서 하드 코드 된 것 이지만 것 보다 유용 hello runbook을 시작할 때 hello 가상 컴퓨터를 지정할 수 있습니다. 이제 해당 기능 toohello runbook tooprovide 입력된 매개 변수를 추가 합니다 했습니다.

1. 매개 변수를 추가 *VMName* 및 *ResourceGroupName* toohello runbook 이러한 변수를 사용 하 여 hello로 **시작 AzureRmVM** hello 예제 아래와 같이 cmdlet.

   ```
   workflow MyFirstRunbook-Workflow
   {
    Param(
     [string]$VMName,
     [string]$ResourceGroupName
    )  
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name $VMName -ResourceGroupName $ResourceGroupName
   }
   ```
2. Hello runbook을 저장 하 고 hello 테스트 창을 엽니다. Note 이제를 제공할 수 있습니다 값 hello에 대 한 두 개의 입력된 변수 hello 테스트에 사용 됩니다.
3. 닫기 hello 테스트 창입니다.
4. 클릭 **게시** toopublish hello hello runbook의 새 버전입니다.
5. Hello 이전 단계에서 시작 하는 hello 가상 컴퓨터를 중지 합니다.
6. 클릭 **시작** toostart hello runbook입니다. Hello 입력 **VMName** 및 **ResourceGroupName** toostart 거 hello 가상 컴퓨터에 대 한 합니다.<br><br> ![Start Runbook](media/automation-first-runbook-textual/automation-pass-params.png)<br>  
7. Hello runbook이 완료 되 면 해당 hello 가상 컴퓨터가 시작 된 확인 합니다.  

## <a name="next-steps"></a>다음 단계
* 그래픽 runbook 시작 tooget 참조 [내 첫 번째 그래픽 runbook](automation-first-runbook-graphical.md)
* PowerShell runbook 시작 tooget 참조 [내 첫 번째 PowerShell runbook](automation-first-runbook-textual-powershell.md)
* runbook 형식이, 장점 및 제한 사항에 대해 자세히 toolearn 참조 [Azure 자동화 runbook 형식](automation-runbook-types.md)
* PowerShell 스크립트 지원 기능에 대한 자세한 내용은 [Azure 자동화에서 네이티브 PowerShell 스크립트 지원](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)
