---
title: "Azure 자동화 DSC의 aaaCompiling 구성 | Microsoft Docs"
description: "이 문서에서는 설명 방식을 Azure 자동화에 대 한 toocompile 구성 DSC (필요한 상태) 구성 합니다."
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
ms.assetid: 49f20b31-4fa5-4712-b1c7-8f4409f1aecc
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 02/07/2017
ms.author: magoedte; eslesar
ms.openlocfilehash: b195311318a2d7431c4d6b29f4b9a5f3a0a0a9a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a>Azure 자동화 DSC에서 구성을 컴파일

두 가지 방법으로 Azure 자동화 원하는 상태 구성 (DSC) 구성을 컴파일할 수 있습니다: hello Azure 포털에서에서 및 Windows PowerShell을 사용 합니다. hello 다음 표를 참조 시기를 결정 하 toouse 각 hello 특징을 기반으로 하는 방법:

### <a name="azure-portal"></a>Azure portal

* 대화형 사용자 인터페이스를 사용하는 간단한 방법
* 양식 tooprovide 간단한 매개 변수 값
* 작업 상태를 쉽게 추적
* Azure 로그온을 사용하여 액세스 인증

### <a name="windows-powershell"></a>Windows PowerShell

* Windows PowerShell cmdlet을 사용하여 명령줄에서 호출
* 여러 단계로 구성된 자동화된 솔루션에 포함할 수 있음
* 단순한 매개 변수 값 및 복잡한 매개 변수 값 제공
* 작업 상태 추적
* 필요한 클라이언트 toosupport PowerShell cmdlet
* ConfigurationData 전달
* 자격 증명을 사용하는 구성을 컴파일

컴파일 메서드에 결정 했으면, toostart 컴파일 아래 hello 해당 절차를 따를 수 있습니다.

## <a name="compiling-a-dsc-configuration-with-hello-azure-portal"></a>Azure 포털 hello로 DSC 구성 컴파일

1. Automation 계정에서 **DSC 구성**을 클릭합니다.
2. 구성 tooopen 해당 블레이드를 클릭 합니다.
3. **컴파일**을 클릭합니다.
4. Toocompile 할지 여부 증명된 tooconfirm hello 구성 매개 변수가 없는 경우, 될 것입니다. Hello 구성 매개 변수가 있으면 hello **구성 컴파일** 매개 변수 값을 제공할 수 있도록 블레이드가 열립니다. Hello 참조 [ **기본 매개 변수** ](#basic-parameters) 매개 변수에 대 한 자세한 내용은 아래 섹션.
5. hello **컴파일 작업** hello 노드 구성 (구성 MOF 문서)를 유발 하기 toobe hello Azure 자동화 DSC 끌어오기 서버에 배치 하 고 hello 컴파일 작업의 상태를 추적할 수 있도록 블레이드가 열립니다.

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a>Windows PowerShell을 사용하여 DSC 구성을 컴파일

사용할 수 있습니다 [ `Start-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart Windows PowerShell을 사용 하 여 컴파일할 합니다. 다음 샘플 코드는 hello 이라고 하는 DSC 구성의 컴파일을 시작 **SampleConfig**합니다.

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

`Start-AzureRmAutomationDscCompilationJob`컴파일 반환 작업 개체를 사용할 수 있는 tootrack 상태입니다. 이 컴파일 작업 개체를 사용할 수 있습니다 [ `Get-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) hello 컴파일 작업의 toodetermine hello 상태 및 [ `Get-AzureRmAutomationDscCompilationJobOutput` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview 해당 스트림 (output). 다음 샘플 코드는 hello hello의 컴파일을 시작 **SampleConfig** 구성, 완료 된 후 해당 스트림을 표시 될 때까지 대기 합니다.

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a>기본 매개 변수
매개 변수 형식 및 속성을 작동을 비롯 한 DSC 구성에서 매개 변수 선언 Azure 자동화 runbook에서와 같이 동일한 hello 합니다. 참조 [Azure 자동화에서 runbook 시작](automation-starting-a-runbook.md) toolearn runbook 매개 변수에 대 한 자세한 합니다.

hello 다음 예제에서는 라는 두 개의 매개 변수가 **FeatureName** 및 **IsPresent**, toodetermine hello 속성 값에 hello **ParametersExample.sample** 노드 구성 컴파일 중에 생성 합니다.

```powershell
Configuration ParametersExample
{
    param(
        [Parameter(Mandatory=$true)]

        [string] $FeatureName,

        [Parameter(Mandatory=$true)]
        [boolean] $IsPresent
    )

    $EnsureString = "Present"
    if($IsPresent -eq $false)
    {
        $EnsureString = "Absent"
    }

    Node "sample"
    {
        WindowsFeature ($FeatureName + "Feature")
        {
            Ensure = $EnsureString
            Name = $FeatureName
        }
    }
}
```

기본 매개 변수를 사용 하 여 hello Azure 자동화 DSC 포털에서 또는 Azure PowerShell을 사용 하는 DSC 구성을 컴파일할 수 있습니다.

### <a name="portal"></a>포털

Hello 포털에서 입력할 수 있는 매개 변수 값을 클릭 한 후 **컴파일**합니다.

![대체 텍스트](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a>PowerShell

PowerShell에서 매개 변수를 필요는 [hashtable](http://technet.microsoft.com/library/hh847780.aspx) 여기서 hello 키는 hello 매개 변수 이름과 일치 하 고 hello 매개 변수 값과 같은 hello 값입니다.

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

PSCredentials을 매개 변수로 전달하는 방법에 대한 정보는 아래의 <a href="#credential-assets">**자격 증명 자산**</a> 을 참조하세요.

## <a name="configurationdata"></a>ConfigurationData
**ConfigurationData** PowerShell DSC를 사용 하는 동안 모든 환경 특정 구성에서 구조적 구성 tooseparate 있습니다. 참조 [PowerShell DSC에 있는 "Where"에서 "작업" 분리](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn에 대 한 자세한 **ConfigurationData**합니다.

> [!NOTE]
> 사용할 수 있습니다 **ConfigurationData** hello Azure 포털 있지만 Azure PowerShell을 사용 하 여 Azure 자동화 DSC에 컴파일할 때.

hello 다음 예제에서는 DSC 구성을 사용 하 여 **ConfigurationData** hello를 통해 **$ConfigurationData** 및 **$AllNodes** 키워드입니다. 또한 hello 해야 [ **xWebAdministration** 모듈](https://www.powershellgallery.com/packages/xWebAdministration/) 이 예제에 대 한 합니다.

```powershell
Configuration ConfigurationDataSample
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite

    Write-Verbose $ConfigurationData.NonNodeData.SomeMessage

    Node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        xWebsite Site
        {
            Name = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure   = "Present"
        }
    }
}
```

PowerShell 사용한 위의 hello DSC 구성을 컴파일할 수 있습니다. 두 개의 노드 구성을 toohello Azure 자동화 DSC 끌어오기 서버를 추가 하는 PowerShell 아래의 hello: **ConfigurationDataSample.MyVM1** 및 **ConfigurationDataSample.MyVM3**:

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "MyVM1"
            Role = "WebServer"
        },
        @{
            NodeName = "MyVM2"
            Role = "SQLServer"
        },
        @{
            NodeName = "MyVM3"
            Role = "WebServer"
        }
    )

    NonNodeData = @{
        SomeMessage = "I love Azure Automation DSC!"
    }
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ConfigurationDataSample" -ConfigurationData $ConfigData
```

## <a name="assets"></a>자산

자산 참조의 경우 Azure 자동화 DSC 구성 및 runbook 동일 hello 됩니다. Hello 자세한 내용은 다음을 참조 하십시오.

* [인증서](automation-certificates.md)
* [연결](automation-connections.md)
* [자격 증명](automation-credentials.md)
* [변수](automation-variables.md)

### <a name="credential-assets"></a>자격 증명 자산

Azure Automation에서 DSC 구성은 **Get-AzureRmAutomationCredential**을 사용하여 자격 증명 자산을 참조할 수 있지만 원하는 경우 자격 증명 자산은 매개 변수를 통해 전달될 수 있습니다. 구성 매개 변수를 사용 하는 경우 **PSCredential** 형식, PSCredential 개체를 사용 하지 않고 해당 매개 변수의 값은 Azure 자동화 자격 증명 자산의 toopass hello 문자열 이름이 필요 합니다. Hello 백그라운드 해당 이름의 hello Azure 자동화 자격 증명 자산 검색 하 고 toohello 구성을 전달 합니다.

자격 증명을 유지 노드 구성 (구성 MOF 문서)에서 보안 필요 hello 노드 구성 MOF 파일에 hello 자격 증명을 암호화 합니다. Azure 자동화는이 한 단계를 더 이상 사용 하 고 hello 전체 MOF 파일을 암호화 합니다. 그러나 현재 알려야 PowerShell DSC 괜찮습니다 자격 증명 toobe 노드 구성 MOF 생성 하는 동안 일반 텍스트로 출력에 대 한 PowerShell DSC Azure 자동화 후 hello 전체 MOF 파일 암호화 될 알 없기 때문 해당 컴파일 작업을 통해 생성 됩니다.

생성 된 hello 노드 구성 Mof에에서 일반 텍스트로 출력 하는 자격 증명 toobe 두어도 되는 PowerShell DSC 알 수 있습니다를 사용 하 여 [ **ConfigurationData**](#configurationdata)합니다. 전달 해야 `PSDscAllowPlainTextPassword = $true` 통해 **ConfigurationData** hello DSC 구성에 표시 되 고 자격 증명을 사용 하는 각 노드 블록의 이름에 대 한 합니다.

hello 다음 예제에서는 자동화 자격 증명 자산을 사용 하는 DSC 구성

```powershell
Configuration CredentialSample
{
    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -AutomationAccountName "AutomationAcct" -Name "SomeCredentialAsset"

    Node $AllNodes.NodeName
    {
        File ExampleFile
        {
            SourcePath = "\\Server\share\path\file.ext"
            DestinationPath = "C:\destinationPath"
            Credential = $Cred
        }
    }
}
```

PowerShell 사용한 위의 hello DSC 구성을 컴파일할 수 있습니다. 두 개의 노드 구성을 toohello Azure 자동화 DSC 끌어오기 서버를 추가 하는 PowerShell 아래의 hello: **CredentialSample.MyVM1** 및 **CredentialSample.MyVM2**합니다.

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "*"
            PSDscAllowPlainTextPassword = $True
        },
        @{
            NodeName = "MyVM1"
        },
        @{
            NodeName = "MyVM2"
        }
    )
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "CredentialSample" -ConfigurationData $ConfigData
```

## <a name="importing-node-configurations"></a>노드 구성 가져오기

Azure 외부에서 컴파일한 노드 구성(MOF)을 가져올 수도 있습니다. 이 경우 장점 중 하나는 노드 구성을 서명할 수 있다는 것입니다.
서명 된 노드 구성 적용된 toohello 노드 되 고 해당 hello 구성 인증된 된 출처에서 제공 되었는지 확인 하는 hello DSC 에이전트에 의해 관리 되는 노드에서 로컬로 확인 됩니다.

> [!NOTE]
> 서명된 구성을 Azure Automation 계정으로 가져오기를 사용할 수 있지만 Azure Automation에서는 현재 서명된 구성의 컴파일을 지원하지 않습니다.

> [!NOTE]
> 노드 구성 파일을 1MB tooallow 보다 작은 해야 것 Azure 자동화에 가져와서 toobe 합니다.

학습할 수 있는 방법을 toosign 노드 구성을 https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module에 있습니다.

### <a name="importing-a-node-configuration-in-hello-azure-portal"></a>Hello Azure 포털에서에서 노드 구성을 가져오기

1. Automation 계정에서 **DSC 노드 구성**을 클릭합니다.

    ![DSC 노드 구성](./media/automation-dsc-compile/node-config.png)
2. Hello에 **DSC 노드 구성을** 블레이드에서 클릭 **는 NodeConfiguration 추가**합니다.
3. Hello에 **가져오기** 블레이드에서 hello 폴더 아이콘 다음 toohello 클릭 **노드 구성 파일** 로컬 컴퓨터에는 노드 구성 파일 (MOF)에 대 한 textbox toobrowse 합니다.

    ![로컬 파일 찾기](./media/automation-dsc-compile/import-browse.png)
4. Hello에 이름을 입력 **구성 이름** 텍스트 상자에 붙여넣습니다. 이 이름은 hello 노드 구성을 컴파일한 hello 구성의 hello 이름을 일치 해야 합니다.
5. **확인**을 클릭합니다.

### <a name="importing-a-node-configuration-with-powershell"></a>PowerShell을 사용하여 노드 구성 가져오기

Hello를 사용할 수 있습니다 [가져오기 AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet tooimport 자동화 계정으로 노드 구성 합니다.

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



