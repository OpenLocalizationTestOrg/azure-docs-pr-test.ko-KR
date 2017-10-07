---
title: "Azure 자동화의 aaaEditing 텍스트 runbook"
description: "이 문서에서는 hello 텍스트 편집기를 사용 하 여 Azure 자동화의 PowerShell 및 PowerShell 워크플로 runbook 작업에 대 한 절차가 다릅니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: 6f5b48fb-6f30-4e99-9e14-9061b5554b08
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 3fd87d457838f300ca6c94bc345e82c679a0e011
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="editing-textual-runbooks-in-azure-automation"></a>Azure 자동화에서 텍스트 Runbook 편집
hello Azure 자동화의 텍스트 편집기 수 사용된 tooedit [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) 및 [PowerShell 워크플로 runbook](automation-runbook-types.md#powershell-workflow-runbooks)합니다. 이 hello 다른 코드 편집기의 intellisense에서 코드 색상 지정 추가 특수 기능 tooassist 사용 하면 일반적인 toorunbooks 리소스에 액세스 등의 일반적인 기능.  이 문서에서는 이 편집기를 사용하여 다양한 기능을 수행하기 위한 상세 단계를 제공합니다.

runbook에 작업, 자산, 및 자식 runbook에 대 한 기능 tooinsert 코드를 포함 하는 hello 텍스트 편집기입니다. 직접 입력 하지 않고 hello 코드, 사용 가능한 리소스 목록에서 선택 하 고 hello 적절 한 코드가 hello runbook에 삽입 되도록 할 수 있습니다.

Azure 자동화의 각 Runbook에는 초안과 게시 등 두 버전이 있습니다. Hello runbook의 초안 버전 hello 편집한 다음 실행할 수 있도록 게시 합니다. hello 게시 됨 버전은 편집할 수 없습니다. 자세한 내용은 [Runbook 게시](automation-creating-importing-runbook.md#publishing-a-runbook) 를 참조하세요.

와 toowork [그래픽 Runbook](automation-runbook-types.md#graphical-runbooks), 참조 [Azure 자동화의 그래픽 제작](automation-graphical-authoring-intro.md)합니다.

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a>tooedit hello Azure 포털을 사용 하 여 runbook
다음 프로시저 tooopen hello 텍스트 편집기에서 편집할 runbook hello를 사용 합니다.

1. Hello Azure 포털에서에서 자동화 계정을 선택 합니다.
2. Hello 클릭 **Runbook** runbook의 타일 tooopen hello 목록입니다.
3. Hello 이름을 클릭 hello runbook의 tooedit을 누른 다음 hello **편집** 단추입니다.
4. Hello 필요한 편집을 수행 합니다.
5. 편집이 완료되면 **저장** 을 클릭합니다.
6. 클릭 **게시** hello hello runbook toobe 게시의 최신 초안 버전을 선택 합니다.

### <a name="tooinsert-a-cmdlet-into-a-runbook"></a>tooinsert runbook에는 cmdlet
1. Hello hello 텍스트 편집기의 캔버스에서에서 tooplace hello cmdlet 저장할 hello 커서를 놓습니다.
2. Hello 확장 **Cmdlet** hello 라이브러리 컨트롤에서에서 노드.
3. 원하는 toouse hello cmdlet을 포함 하는 hello 모듈을 확장 합니다.
4. Hello cmdlet tooinsert 마우스 오른쪽 단추로 클릭 하 고 선택 **toocanvas 추가**합니다.  Hello cmdlet에 둘 이상의 매개 변수를 설정한 경우 기본 집합 hello 추가 됩니다.  또한 hello cmdlet tooselect 다른 매개 변수를 확장할 수 있습니다 설정 합니다.
5. hello 코드 hello cmdlet에 대 한 매개 변수 전체 목록을 삽입 됩니다.
6. 모든 필수 매개 변수에 대해 중괄호 <>로 묶은 hello 데이터 형식 자리에 해당 값을 제공 합니다.  필요가 없는 매개 변수는 제거합니다.

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a>runbook에는 자식 runbook에 대 한 tooinsert 코드
1. Hello hello 텍스트 편집기의 캔버스에서에서의 위치를 hello 커서 tooplace hello 코드 hello에 대 한 [자식 runbook](automation-child-runbooks.md)합니다.
2. Hello 확장 **Runbook** hello 라이브러리 컨트롤에서에서 노드.
3. Hello runbook tooinsert 마우스 오른쪽 단추로 클릭 하 고 선택 **toocanvas 추가**합니다.
4. 모든 runbook 매개 변수에 대 한 모든 자리 표시자와 hello 자식 runbook에 대 한 hello 코드 삽입 됩니다.
5. 각 매개 변수에 대해 적절 한 값으로 hello 자리 표시자를 대체 합니다.

### <a name="tooinsert-an-asset-into-a-runbook"></a>runbook에 자산 tooinsert
1. Hello hello 텍스트 편집기의 캔버스에서에서 원하는 위치 tooplace hello 코드 hello 자식 runbook에 대 한 hello 커서를 놓습니다.
2. Hello 확장 **자산** hello 라이브러리 컨트롤에서에서 노드.
3. Hello 유형의 원하는 자산에 대 한 hello 노드를 확장 합니다.
4. Hello 자산 tooinsert 마우스 오른쪽 단추로 클릭 하 고 선택 **toocanvas 추가**합니다.  에 대 한 [변수 자산](automation-variables.md), 중 하나를 선택 **"변수 가져오기" toocanvas 추가** 또는 **"변수 설정" toocanvas 추가** 있는지에 따라 원하는 tooget hello 변수를 설정 합니다.
5. hello 자산에 대 한 hello 코드 hello runbook에 삽입 됩니다.

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a>tooedit hello Azure 포털을 사용 하 여 runbook
다음 프로시저 tooopen hello 텍스트 편집기에서 편집할 runbook hello를 사용 합니다.

1. Hello Azure 포털에서에서 선택 **자동화** 다음 자동화 계정 hello 이름을 클릭 하 고 있습니다.
2. 선택 hello **Runbook** 탭 합니다.
3. Hello 이름을 클릭 hello runbook의 tooedit 한 다음 선택 hello **작성자** 탭 합니다.
4. Hello 클릭 **편집** hello hello 화면 맨 아래에 단추입니다.
5. Hello 필요한 편집을 수행 합니다.
6. 편집이 완료되면 **저장** 을 클릭합니다.
7. 클릭 **게시** hello hello runbook toobe 게시의 최신 초안 버전을 선택 합니다.

### <a name="tooinsert-an-activity-into-a-runbook"></a>Runbook에 활동 tooinsert
1. Hello hello 텍스트 편집기의 캔버스에서에서 원하는 tooplace hello 활동 위치 hello 커서를 놓습니다.
2. Hello 화면 아래쪽에 hello, 클릭 **삽입** 차례로 **활동**합니다.
3. Hello에 **통합 모듈** 열, hello 활동을 포함 하는 select hello 모듈입니다.
4. Hello에 **활동** 창에서 활동을 선택 합니다.
5. Hello에 **설명** 열 hello 활동의 참고 hello 설명 합니다. 자세히 보기를 클릭 하면 필요에 따라 toolaunch 도움말 hello 활동 hello 브라우저에 대 한 도움말입니다.
6. Hello 오른쪽 화살표를 클릭 합니다.  Hello 활동 매개 변수가 있으면 정보용 나열 됩니다.
7. Hello 확인 단추를 클릭 합니다.  코드 toorun hello 활동 hello runbook에 삽입 됩니다.
8. Hello 활동에 매개 변수가 필요한 경우 중괄호 <>로 묶은 hello 데이터 형식 자리에 적절 한 값을 제공 합니다.

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a>runbook에는 자식 runbook에 대 한 tooinsert 코드
1. Hello hello 텍스트 편집기의 캔버스에서에서의 위치를 hello 커서 tooplace hello [자식 runbook](automation-child-runbooks.md)합니다.
2. Hello 화면 아래쪽에 hello, 클릭 **삽입** 차례로 **Runbook**합니다.
3. Hello runbook tooinsert hello 가운데 열에서 선택한 hello 오른쪽 화살표를 클릭 합니다.
4. Hello runbook에 매개 변수가 있으면 정보용 나열 됩니다.
5. Hello 확인 단추를 클릭 합니다.  코드 toorun hello 선택한 runbook hello 현재 runbook에 삽입 됩니다.
6. Hello runbook에 매개 변수가 필요한 경우 중괄호 <>로 묶은 hello 데이터 형식 자리에 적절 한 값을 제공 합니다.

### <a name="tooinsert-an-asset-into-a-runbook"></a>runbook에 자산 tooinsert
1. Hello hello 텍스트 편집기의 캔버스에서에서 tooplace hello 활동 tooretrieve hello 자산 저장할 hello 커서를 놓습니다.
2. Hello 화면 아래쪽에 hello, 클릭 **삽입** 차례로 **설정**합니다.
3. Hello에 **설정 작업** 열, 선택 hello 원하는 동작을 합니다.
4. Hello hello 가운데 열의 사용 가능한 자산 중에서 선택 합니다.
5. Hello 확인 단추를 클릭 합니다.  Tooget 코드 또는 집합 hello 자산 hello runbook에 삽입 됩니다.

## <a name="tooedit-an-azure-automation-runbook-using-windows-powershell"></a>Windows PowerShell을 사용 하 여 Azure 자동화 runbook tooedit
runbook tooedit Windows PowerShell과 함께 hello 원하는 편집기를 사용 하 고이 tooa.ps1 파일을 저장 합니다. Hello를 사용할 수 있습니다 [Get-azureautomationrunbookdefinition](http://aka.ms/runbookauthor/cmdlet/getazurerunbookdefinition) hello runbook의 cmdlet tooretrieve hello 내용을 다음 [Set-azureautomationrunbookdefinition](http://aka.ms/runbookauthor/cmdlet/setazurerunbookdefinition) cmdlet tooreplace hello 기존 초안 runbook hello로 하나를 수정합니다.

### <a name="tooretrieve-hello-contents-of-a-runbook-using-windows-powershell"></a>tooRetrieve hello Runbook Using Windows PowerShell의 내용
다음 명령 예제는 hello tooretrieve hello runbook에 대 한 스크립트 하 고 tooa 스크립트 파일을 저장 하는 방법을 보여 줍니다. 이 예제에서는 hello 초안 버전이 검색 됩니다. 또한 hello runbook의 가능한 tooretrieve hello 게시 됨 버전 있지만이 버전을 변경할 수 없습니다.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    $runbookDefinition = Get-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Slot Draft
    $runbookContent = $runbookDefinition.Content

    Out-File -InputObject $runbookContent -FilePath $scriptPath

### <a name="toochange-hello-contents-of-a-runbook-using-windows-powershell"></a>tooChange hello Runbook Using Windows PowerShell의 내용
hello 다음 샘플 명령은 표시 방법을 tooreplace hello 스크립트 파일의 hello 콘텐츠로 runbook의 기존 내용을 합니다. 참고 동일 hello는이 예제에서 같이 프로시저 [tooimport Windows powershell 스크립트 파일에서 runbook](automation-creating-importing-runbook.md)합니다.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    Set-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Path $scriptPath -Overwrite
    Publish-AzureAutomationRunbook –AutomationAccountName $automationAccountName –Name $runbookName

## <a name="related-articles"></a>관련 문서
* [Azure 자동화에서 Runbook 만들기 또는 가져오기](automation-creating-importing-runbook.md)
* [PowerShell 워크플로 학습](automation-powershell-workflow.md)
* [Azure 자동화에서 그래픽 작성](automation-graphical-authoring-intro.md)
* [인증서](automation-certificates.md)
* [연결](automation-connections.md)
* [자격 증명](automation-credentials.md)
* [일정](automation-schedules.md)
* [변수](automation-variables.md)
