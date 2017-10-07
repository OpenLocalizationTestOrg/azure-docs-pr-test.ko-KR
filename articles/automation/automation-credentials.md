---
title: "Azure 자동화에서 aaaCredential 자산 | Microsoft Docs"
description: "Azure 자동화에서 자격 증명 자산 사용된 tooauthenticate tooresources hello runbook 또는 DSC 구성에 액세스할 수 있는 보안 자격 증명을 포함 합니다. 이 문서에서는 toocreate 자산 자격 증명 하 고 runbook 또는 DSC 구성을 사용 하는 방법을 설명 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 3209bf73-c208-425e-82b6-df49860546dd
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/14/2017
ms.author: bwren
ms.openlocfilehash: 46f23a8f79d5863265af9cf84f6003e30f8e7d39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="credential-assets-in-azure-automation"></a>Azure 자동화의 자격 증명 자산
자동화 자격 증명 자산은 사용자 이름과 암호 등의 보안 자격 증명을 포함하는 [PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) 개체를 보유합니다. Hello 사용자 이름 및 hello PSCredential 개체 tooprovide toosome 응용 프로그램의 암호 또는 인증을 요구 하는 서비스를 추출할 수 있습니다 또는 Runbook 및 DSC 구성을 인증용으로 PSCredential 개체를 허용 하는 cmdlet을 사용할 수 있습니다. hello 자격 증명에 대 한 Azure 자동화에 안전 하 게 저장 된 속성과 hello runbook 또는 hello로 DSC 구성에 액세스할 수 [Get-automationpscredential](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) 활동입니다.

> [!NOTE]
> Azure 자동화의 안전한 자산에는 자격 증명, 인증서, 연결, 암호화된 변수 등이 있습니다. 이러한 자산 암호화 및 hello 각 자동화 계정에 대해 생성 되는 고유 키를 사용 하 여 Azure 자동화에에서 저장 됩니다. 이 키는 마스터 인증서로 암호화되어 Azure 자동화에 저장됩니다. 보안 자산을 저장 하기 전에 hello 자동화 계정에 대 한 hello 키 hello 마스터 인증서를 사용 하 여 암호가 해독 됩니다와 tooencrypt hello 자산을 사용 합니다.  

## <a name="windows-powershell-cmdlets"></a>Windows PowerShell cmdlet
다음 표에 hello의 hello cmdlet 사용 되는 toocreate 됩니다 하 고 Windows PowerShell을 사용 하 여 자동화 자격 증명 자산을 관리 합니다.  Hello의 일부분으로 제공 [Azure PowerShell 모듈](/powershell/azure/overview) 자동화 runbook 및 DSC 구성에 사용 하기 위해 사용할 수 있습니다.

| Cmdlet | 설명 |
|:--- |:--- |
| [Get-AzureAutomationCredential](/powershell/module/azure/get-azureautomationcredential?view=azuresmps-3.7.0) |자격 증명 자산에 대한 정보를 검색합니다. Hello 자격 증명 자체에 정보만 검색할 수 있습니다에서 **Get-automationpscredential** 활동입니다. |
| [New-AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |새 자동화 자격 증명을 만듭니다. |
| [Remove- AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |자동화 자격 증명을 제거합니다. |
| [Set- AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |집합 hello 기존 자동화 자격 증명에 대 한 속성. |

## <a name="runbook-activities"></a>Runbook 활동
hello 활동 hello 표 다음에 runbook 및 DSC 구성에 사용 되는 tooaccess 자격 증명.

| 활동 | 설명 |
|:--- |:--- |
| Get-AutomationPSCredential |Runbook 또는 DSC 구성에서 자격 증명 toouse를 가져옵니다. [System.Management.Automation.PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) 개체를 반환합니다. |

> [!NOTE]
> 변수를 사용 하면 안 hello – Get-automationpscredential runbook 또는 DSC 구성 간의 종속성을 검색 하기가 어려워질 하 고 자격 증명 자산을 디자인 타임에이의 Name 매개 변수입니다.
> 
> 

## <a name="creating-a-new-credential-asset"></a>새 자격 증명 자산 만들기

### <a name="toocreate-a-new-credential-asset-with-hello-azure-portal"></a>Azure 포털 hello로 새 자격 증명 자산 toocreate
1. 자동화 계정에서 클릭 hello **자산** 부분 tooopen hello **자산** 블레이드입니다.
2. Hello 클릭 **자격 증명** 부분 tooopen hello **자격 증명** 블레이드입니다.
3. 클릭 **자격 증명 추가** hello hello 블레이드 위쪽에 있습니다.
4. Hello 양식을 작성 하 고 클릭 **만들기** toosave hello 새 자격 증명입니다.

### <a name="toocreate-a-new-credential-asset-with-windows-powershell"></a>Windows PowerShell과 함께 새 자격 증명 자산 toocreate
hello 다음 명령 예제에서는 toocreate 새 자동화 자격 증명 하는 방법 PSCredential 개체를 먼저 hello 이름 및 암호 만들어지고 toocreate hello 자격 증명 자산을 사용 합니다. 또는 hello를 사용할 수 있습니다 **Get-credential** cmdlet toobe tootype 이름 및 암호를 묻는 메시지가 표시 됩니다.

    $user = "MyDomain\MyUser"
    $pw = ConvertTo-SecureString "PassWord!" -AsPlainText -Force
    $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $user, $pw
    New-AzureAutomationCredential -AutomationAccountName "MyAutomationAccount" -Name "MyCredential" -Value $cred

### <a name="toocreate-a-new-credential-asset-with-hello-azure-classic-portal"></a>Azure 클래식 포털 hello로 새 자격 증명 자산 toocreate
1. 자동화 계정에서 클릭 **자산** hello 창의 위쪽에 hello 합니다.
2. Hello hello 창의 아래쪽에 있는 클릭 **설정 추가**합니다.
3. **자격 증명 추가**를 클릭합니다.
4. Hello에 **자격 증명 형식을** 드롭다운 **PowerShell 자격 증명**합니다.
5. Hello 마법사를 완료 하 고 hello 확인란 toosave hello 새 자격 증명을 클릭 합니다.

## <a name="using-a-powershell-credential"></a>PowerShell 자격 증명 사용
Runbook 또는 hello로 DSC 구성에서 자격 증명 자산을 검색할 **Get-automationpscredential** 활동입니다. 그러면 PSCredential 매개 변수가 필요한 활동 또는 cmdlet에서 사용할 수 있는 [PSCredential 개체](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) 가 반환됩니다. 또한 hello 자격 증명 개체 toouse의 hello 속성을 개별적으로 검색할 수 있습니다. hello 개체에 대 한 속성이 hello 사용자 이름과 암호를 보안 하는 hello 하거나 hello를 사용할 수 있습니다 **GetNetworkCredential** 메서드 tooreturn는 [NetworkCredential](http://msdn.microsoft.com/library/system.net.networkcredential.aspx) 는 보안 되지 않은 제공 하는 개체 hello 암호의 버전입니다.

### <a name="textual-runbook-sample"></a>텍스트 Runbook 샘플
hello 다음 명령 예제에서는 toouse는 PowerShell runbook에서 자격 증명 하는 방법 이 예제에서는 hello 자격 증명 검색 되 고 해당 사용자 이름과 암호가 toovariables 할당 합니다.

    $myCredential = Get-AutomationPSCredential -Name 'MyCredential'
    $userName = $myCredential.UserName
    $securePassword = $myCredential.Password
    $password = $myCredential.GetNetworkCredential().Password


### <a name="graphical-runbook-sample"></a>그래픽 Runbook 샘플
추가한는 **Get-automationpscredential** hello 자격 증명을 선택 하 고 hello 그래픽 편집기의 hello 라이브러리 창에서 마우스 오른쪽 단추로 클릭 하 여 활동 tooa 그래픽 runbook **toocanvas 추가**합니다.

![자격 증명 toocanvas 추가](media/automation-credentials/credential-add-canvas.png)

hello 다음 이미지의 예가 나와 그래픽 runbook에서 자격 증명을 사용 합니다.  이 경우에 있어 runbook tooAzure 리소스에 대 한 사용된 tooprovide 인증에 설명 된 대로 [Azure AD 사용자 계정으로 인증 Runbook](automation-create-aduser-account.md)합니다.  첫 번째 활동 hello 액세스 toohello Azure 구독 hello 자격 증명을 검색 합니다.  hello **Add-azureaccount** 작업 뒤에 오는 모든 활동에 대 한 다음이 자격 증명 tooprovide 인증을 사용 합니다.  [Get-AutomationPSCredential](automation-graphical-authoring-intro.md#links-and-workflow) 에는 단일 개체가 필요하기 때문에 여기에서는 **파이프라인 링크** 를 사용합니다.  

![자격 증명 toocanvas 추가](media/automation-credentials/get-credential.png)

## <a name="using-a-powershell-credential-in-dsc"></a>DSC에서 PowerShell 자격 증명을 사용
Azure 자동화에서 DSC 구성은 **Get-AutomationPSCredential**을 사용하여 자격 증명 자산을 참조할 수 있지만 원하는 경우 자격 증명 자산은 매개 변수를 통해 전달될 수 있습니다. 자세한 내용은 [Azure 자동화 DSC에서 구성을 컴파일](automation-dsc-compile.md#credential-assets)을 참조하세요.

## <a name="next-steps"></a>다음 단계
* 참조 링크 그래픽 제작에 대 한 자세한 정보는 toolearn [그래픽 제작에 대 한 링크](automation-graphical-authoring-intro.md#links-and-workflow)
* 자동화를 toounderstand hello 다른 인증 방법을 참조 [Azure 자동화의 보안](automation-security-overview.md)
* 그래픽 runbook 시작 tooget 참조 [내 첫 번째 그래픽 runbook](automation-first-runbook-graphical.md)
* PowerShell 워크플로 runbook 시작 tooget 참조 [내 첫 번째 PowerShell 워크플로 runbook](automation-first-runbook-textual.md) 

