---
title: "aaaCreating 또는 Azure 자동화에서 runbook 가져오기"
description: "이 문서에서는 설명 방법을 toocreate 파일에서 가져오기 또는 Azure 자동화에서 새 runbook 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 24414362-b690-4474-8ca7-df18e30fc31d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: d45f44cf15fbcacdd0de2977668502c2e1671063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-or-importing-a-runbook-in-azure-automation"></a>Azure Automation에서 Runbook 만들기 또는 가져오기
runbook tooAzure 자동화를 추가할 수 있습니다 [을 새로 만드는](#creating-a-new-runbook) 하거나 hello 또는 파일에서 기존 runbook을 가져와 [Runbook 갤러리](automation-runbook-gallery.md)합니다. 이 문서에서는 파일로부터 Runbook을 만들고 가져오는 것과 관련한 정보를 제공합니다.  모든 액세스 커뮤니티 runbook 및 모듈에 대 한 hello 세부 정보를 얻을 수 [Azure 자동화 용 Runbook 및 모듈 갤러리](automation-runbook-gallery.md)합니다.

## <a name="creating-a-new-runbook"></a>새 Runbook 만들기
Hello Azure 중 하나를 사용 하 여 Azure 자동화에서 새 runbook을 만들 수 있습니다 포털 또는 Windows PowerShell입니다. Hello runbook을 만든 후에 정보를 사용 하 여 편집할 수 있습니다 [학습 PowerShell 워크플로](automation-powershell-workflow.md) 및 [Azure 자동화의 그래픽 제작](automation-graphical-authoring-intro.md)합니다.

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-classic-portal"></a>toocreate hello Azure 클래식 포털을 사용 하 여 새 Azure 자동화 runbook
만 처리할 수 있는 [PowerShell 워크플로 runbook](automation-runbook-types.md#powershell-workflow-runbooks) hello Azure 포털의에서.

1. Hello Azure 클래식 포털에서 클릭 하 고, **새로**, **응용 프로그램 서비스**, **자동화**, **Runbook**, **빨리만들기**.
2. Hello 필요한 정보를 입력 한 다음 클릭 **만들기**합니다. hello runbook 이름은 문자로 시작 해야 하며 문자, 숫자, 밑줄 및 대시만 사용할 수 있습니다.
3. Tooedit hello runbook을 하려는 경우 클릭 **Runbook 편집**합니다. 그렇지 않은 경우 **확인**을 클릭합니다.
4. 새 runbook hello에 나타납니다. **Runbook** 탭 합니다.

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-portal"></a>toocreate hello Azure 포털을 사용 하 여 새 Azure 자동화 runbook
1. Hello Azure 포털에서에서 자동화 계정을 엽니다.
2. Hello 허브에서에서 선택 **Runbook** runbook의 tooopen hello 목록입니다.
3. Hello 클릭 **runbook을 추가할** 단추 차례로 **새 runbook을 만들**합니다.
4. 입력 **이름** hello runbook 및 선택에 대 한 해당 [형식](automation-runbook-types.md)합니다. hello runbook 이름은 문자로 시작 해야 하며 문자, 숫자, 밑줄 및 대시만 사용할 수 있습니다.
5. 클릭 **만들기** toocreate hello runbook 및 열기 hello 편집기입니다.

### <a name="toocreate-a-new-azure-automation-runbook-with-windows-powershell"></a>Windows PowerShell을 사용 하 여 새 Azure 자동화 runbook toocreate
Hello를 사용할 수 있습니다 [새로 AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt619376.aspx) cmdlet toocreate 빈 [PowerShell 워크플로 runbook](automation-runbook-types.md#powershell-workflow-runbooks)합니다. Hello를 지정 하거나 **이름** toocreate 매개 변수는 비어 있는 runbook 나중에 편집할 수 있습니다, 또는 hello를 지정할 수 있습니다 **경로** 매개 변수 tooimport runbook 파일입니다. hello **형식** 매개 변수 포함된 toospecify 4 hello runbook 형식 중 하나 이어야 합니다.

hello 다음 샘플 명령은 표시 방법을 toocreate 새 빈 runbook 합니다.

    New-AzureRmAutomationRunbook -AutomationAccountName MyAccount `
    -Name NewRunbook -ResourceGroupName MyResourceGroup -Type PowerShell

## <a name="importing-a-runbook-from-a-file-into-azure-automation"></a>파일의 Runbook을 Azure Automation으로 가져오기
PowerShell 스크립트나 PowerShell 워크플로(.ps1 확장명) 또는 내보낸된 그래픽 Runbook(.graphrunbook)을 Azure Automation에 가져와서 새 Runbook을 만들 수 있습니다.  Hello를 지정 해야 [runbook의 형식을](automation-runbook-types.md) 고려 사항에 따라 계정 hello를 고려 하는 hello 가져오기에서 만들어집니다.

* .graphrunbook 파일은 새 [그래픽 Runbook](automation-runbook-types.md#graphical-runbooks)에만 가져올 수 있으며 그래픽 Runbook은 .graphrunbook 파일을 통해서만 만들 수 있습니다.
* PowerShell 워크플로를 포함하는.ps1 파일은 [PowerShell 워크플로 Runbook](automation-runbook-types.md#powershell-workflow-runbooks)에만 가져올 수 있습니다.  Hello 파일에 여러 PowerShell 워크플로 있으면 hello 가져오기가 실패 합니다. 각 워크플로 tooits 직접 파일을 저장 하며 개별적으로 가져와야 합니다.
* 워크플로를 포함하지 않은 .ps1 파일은 [PowerShell Runbook](automation-runbook-types.md#powershell-runbooks) 또는 [PowerShell Workflow Runbook](automation-runbook-types.md#powershell-workflow-runbooks)으로 가져올 수 있습니다.  변환 된 tooa 워크플로 됩니다 하 고 주석을 hello 변경 된 내용이 지정 하는 hello runbook에 포함 될 것에 PowerShell 워크플로 runbook으로 가져오므로 되지 않습니다.

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-classic-portal"></a>tooimport hello Azure 클래식 포털을 통한 파일에서 runbook
Azure 자동화로 프로시저 tooimport 스크립트 파일을 다음 hello를 사용할 수 있습니다.  이 포털을 사용하는 PowerShell 워크플로 Runbook에만 .ps1 파일을 가져올 수 있습니다.  다른 형식에 대 한 hello Azure 포털을 사용 해야 합니다.

1. Hello Azure 관리 포털에서 선택 **자동화** 선택한 다음 자동화 계정을 선택 합니다.
2. **가져오기**를 클릭합니다.
3. 클릭 **파일 찾아보기** hello 스크립트 파일 tooimport 찾습니다.
4. Tooedit hello runbook을 하려는 경우 클릭 **Runbook 편집**합니다. 그렇지 않은 경우 확인을 클릭합니다.
5. 새 runbook hello hello에 나타납니다. **Runbook** hello 자동화 계정에 대 한 탭 합니다.
6. 수행 해야 [hello runbook을 게시](#publishing-a-runbook) 전에 실행할 수 있습니다.

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-portal"></a>Azure 포털 hello로 파일에서 runbook tooimport
Azure 자동화로 프로시저 tooimport 스크립트 파일을 다음 hello를 사용할 수 있습니다.  

> [!NOTE]
> 참고 hello 포털을 사용 하는 PowerShell 워크플로 runbook에.ps1 파일을만 가져올 수 있습니다.
> 
> 

1. Hello Azure 포털에서에서 자동화 계정을 엽니다.
2. Hello 허브에서에서 선택 **Runbook** runbook의 tooopen hello 목록입니다.
3. Hello 클릭 **runbook을 추가할** 단추 차례로 **가져오기**합니다.
4. 클릭 **Runbook 파일** tooselect hello 파일 tooimport
5. 경우 hello **이름** hello 옵션 toochange 있는 다음 필드를 사용할 것입니다.  hello runbook 이름은 문자로 시작 해야 하며 문자, 숫자, 밑줄 및 대시만 사용할 수 있습니다.
6. hello [runbook 형식](automation-runbook-types.md) 이 자동으로 선택 되지만 hello 형식 hello 해당 제한을 고려해를 만든 후 변경할 수 있습니다. 
7. 새 runbook hello hello 자동화 계정에 대 한 runbook의 hello 목록에 표시 됩니다.
8. 수행 해야 [hello runbook을 게시](#publishing-a-runbook) 전에 실행할 수 있습니다.

> [!NOTE]
> 그래픽 runbook 또는 그래픽 PowerShell 워크플로 runbook을 가져온 후 hello 옵션 tooconvert toohello 다른 형식이 있을 경우. Tootextual을 변환할 수 없습니다.
> 
> 

### <a name="tooimport-a-runbook-from-a-script-file-with-windows-powershell"></a>Windows powershell 스크립트 파일에서 runbook tooimport
Hello를 사용할 수 있습니다 [가져오기 AzureRMAutomationRunbook](https://msdn.microsoft.com/library/mt603735.aspx) cmdlet tooimport PowerShell 워크플로 runbook 초안으로 스크립트 파일입니다. Hello를 사용 하지 않는 한 hello 가져오기 작업이 실패 hello runbook이 이미 있으면 *-Force* 매개 변수입니다. 

hello 다음 샘플 명령은 runbook에 tooimport 스크립트 파일 하는 방법을 보여 줍니다.

    $automationAccountName =  "AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $scriptPath = "C:\Runbooks\Sample_TestRunbook.ps1"
    $RGName = "ResourceGroup"

    Import-AzureRMAutomationRunbook -Name $runbookName -Path $scriptPath `
    -ResourceGroupName $RGName -AutomationAccountName $automationAccountName `
    -Type PowerShellWorkflow 


## <a name="publishing-a-runbook"></a>Runbook 게시
새 Runbook을 만들거나 가져올 때는 게시해야 실행할 수 있습니다.  Automation의 각 Runbook에는 초안 버전과 게시된 버전이 있습니다. Hello 게시 됨 버전만 실행 하는 사용 가능한 toobe 이며 hello 초안 버전만 편집할 수 있습니다. hello 게시 됨 버전이 모든 변경 내용 toohello 초안 버전의 영향을 받지 않습니다. Hello 초안 버전을 설정 해야 사용할 수 있는 경우 다음 게시 하면을 hello 초안 버전으로 hello 게시 됨 버전을 덮어씁니다.

## <a name="toopublish-a-runbook-using-hello-azure-classic-portal"></a>hello Azure 클래식 포털을 사용 하 여 runbook a toopublish
1. Hello Azure 클래식 포털의 hello runbook을 엽니다.
2. Hello 화면의 hello 위쪽 클릭 **작성자**합니다.
3. Hello 화면 아래쪽에 hello, 클릭 **게시** 차례로 **예** toohello 확인 메시지입니다.

## <a name="toopublish-a-runbook-using-hello-azure-portal"></a>hello Azure 포털을 사용 하 여 runbook a toopublish
1. Hello Azure 포털에서에서 hello runbook을 엽니다.
2. Hello 클릭 **편집** 단추입니다.
3. Hello 클릭 **게시** 단추 차례로 **예** toohello 확인 메시지입니다.

## <a name="toopublish-a-runbook-using-windows-powershell"></a>Windows PowerShell을 사용 하 여 runbook toopublish
Hello를 사용할 수 있습니다 [게시 AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603705.aspx) cmdlet toopublish Windows PowerShell로 runbook입니다. hello 다음 샘플 명령은 표시 방법을 toopublish 샘플 runbook입니다.

    $automationAccountName =  AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $RGName = "ResourceGroup"

    Publish-AzureRmAutomationRunbook -AutomationAccountName $automationAccountName `
    -Name $runbookName -ResourceGroupName $RGName


## <a name="next-steps"></a>다음 단계
* toolearn hello Runbook 및 PowerShell 모듈 갤러리에서 얻을 수 있는 방법에 대 한 참조 [Azure 자동화 용 Runbook 및 모듈 갤러리](automation-runbook-gallery.md)
* 텍스트 편집기를 사용 하 여 PowerShell 및 PowerShell 워크플로 runbook 편집에 대 한 더 toolearn 참조 [Azure 자동화의 텍스트 runbook 편집](automation-edit-textual-runbook.md)
* 그래픽 runbook 제작에 대 한 더 toolearn 참조 [Azure 자동화의 그래픽 제작](automation-graphical-authoring-intro.md)

