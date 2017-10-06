---
title: "Azure 자동화 DSC에 의해 관리에 대 한 aaaOnboarding 컴퓨터 | Microsoft Docs"
description: "Azure 자동화 DSC를 사용 하 여 관리용 toosetup 컴퓨터 하는 방법"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
ms.assetid: da13e1f5-2a1c-443b-8e3b-9f0d6f9e4810
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 12/13/2016
ms.author: eslesar
ms.openlocfilehash: ef15801fec2ffea4ba62dcba2fbe9af09268e424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a>Azure 자동화 DSC를 통한 관리를 위한 컴퓨터 온보드

## <a name="why-manage-machines-with-azure-automation-dsc"></a>Azure 자동화 DSC로 컴퓨터를 관리하는 이유

[PowerShell 필요 상태 구성](https://technet.microsoft.com/library/dn249912.aspx)과 마찬가지로 Azure 자동화 필요 상태 구성은 클라우드나 온-프레미스 데이터 센터의 DSC 노드(물리적 및 가상 컴퓨터)를 위한 간단하지만 강력한 구성 관리 서비스입니다. 안전한 중앙 위치에서 수천 대의 컴퓨터를 빠르고 간편하게 확장할 수 있습니다. 선언적 구성 및 보고서 보기를 보여 주는 각 컴퓨터는 할당의 지정한 준수 원하는 toohello 시/도, 컴퓨터 쉽게 등록을 수 있습니다. hello Azure 자동화 DSC 관리 계층은 tooDSC 어떤 hello Azure 자동화 관리 계층은 tooPowerShell 스크립팅 합니다. 즉, Azure 자동화를 사용 하면는 동일한 방식으로 hello에 PowerShell 스크립트를 관리, 하기도 DSC 구성을 관리 합니다. Azure 자동화 DSC를 사용 하 여 hello 이점에 대 한 더 toolearn 참조 [Azure 자동화 DSC 개요](automation-dsc-overview.md)합니다.

Azure 자동화 DSC 사용된 toomanage 다양 한 컴퓨터 하나일 수 있습니다.

* Azure 가상 컴퓨터(기본)
* Azure 가상 컴퓨터
* AWS(Amazon Web Services) 가상 컴퓨터
* 온-프레미스나 Azure/AWS 이외의 클라우드에 있는 실제/가상 Windows 컴퓨터
* 온-프레미스, Azure 또는 Azure 이외의 클라우드에 있는 실제/가상 Linux 컴퓨터

또한 hello 클라우드에서 준비 toomanage 컴퓨터 구성이 없는 경우 Azure 자동화 DSC 보고서 전용 끝점으로 사용도 있습니다. 이 통해 DSC 온-프레미스를 통해 원하는 구성을 tooset (push) 하 고 풍부한 보고 세부 정보 보기 hello로 노드 규정 준수에 필요한 Azure 자동화에서 상태가 있습니다.

다음 섹션 hello 방법을 등록할 수 컴퓨터 tooAzure 자동화 DSC의 유형별로 간략하게 설명 합니다.

## <a name="azure-virtual-machines-classic"></a>Azure 가상 컴퓨터(기본)

Azure 자동화 dsc hello Azure 포털 또는 PowerShell을 사용 하 여 구성 관리용 쉽게 온보드 Azure 가상 컴퓨터 (클래식) 수 있습니다. Hello 내부적 및 tooremote hello VM에 있는 관리자가 없으면 hello VM이 Azure 자동화 DSC 등록 hello Azure VM 필요한 상태 구성 확장 합니다. Hello에 제공 됩니다 hello Azure VM 필요한 상태 구성 확장을 비동기적으로 실행, 단계 tootrack 진행 하거나 문제를 해결 하는 이후 [ **문제를 해결 하는 Azure 가상 컴퓨터의 온 보 딩** ](#troubleshooting-azure-virtual-machine-onboarding)아래 섹션.

### <a name="azure-portal"></a>Azure portal

Hello에 [Azure 포털](http://portal.azure.com/), 클릭 **찾아보기** -> **가상 컴퓨터 (클래식)**합니다. Hello tooonboard 원하는 Windows VM을 선택 합니다. Hello 가상 컴퓨터 대시보드 블레이드 클릭 **모든 설정을** -> **확장** -> **추가**  ->   **Azure 자동화 DSC** -> **만들**합니다. Hello 입력 [PowerShell DSC 로컬 구성 관리자 값](https://msdn.microsoft.com/powershell/dsc/metaconfig4) 사용 사례, 자동화 계정에 등록 키 및 등록 URL 및 필요에 따라 노드 구성 tooassign toohello VM에 필요한 합니다.

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

toofind hello 등록 URL 및 키, hello 자동화 계정 tooonboard hello 컴퓨터에 대 한 참조 hello [ **등록 Secure** ](#secure-registration) 아래 섹션.

### <a name="powershell"></a>PowerShell

```powershell
# log in tooboth Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in hello name of a Node Configuration in Azure Automation DSC, for this VM tooconform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use hello DSC extension tooonboard hello VM for management with Azure Automation DSC
$VM = Get-AzureVM -Name $VMName -ServiceName $ServiceName

$PublicConfiguration = ConvertTo-Json -Depth 8 @{
    SasToken = ""
    ModulesUrl = "https://eus2oaasibizamarketprod1.blob.core.windows.net/automationdscpreview/RegistrationMetaConfigV2.zip"
    ConfigurationFunction = "RegistrationMetaConfigV2.ps1\RegistrationMetaConfigV2"

# update these PowerShell DSC Local Configuration Manager defaults if they do not match your use case.
# See https://technet.microsoft.com/library/dn249922.aspx?f=255&MSPPError=-2147217396 for more details
    Properties = @{
    RegistrationKey = @{
        UserName = 'notused'
        Password = 'PrivateSettingsRef:RegistrationKey'
    }
    RegistrationUrl = $RegistrationInfo.Endpoint
    NodeConfigurationName = $NodeConfigName
    ConfigurationMode = "ApplyAndMonitor"
    ConfigurationModeFrequencyMins = 15
    RefreshFrequencyMins = 30
    RebootNodeIfNeeded = $False
    ActionAfterReboot = "ContinueConfiguration"
    AllowModuleOverwrite = $False
    }
}

$PrivateConfiguration = ConvertTo-Json -Depth 8 @{
    Items = @{
        RegistrationKey = $RegistrationInfo.PrimaryKey
    }
}

$VM = Set-AzureVMExtension `
    -VM $vm `
    -Publisher Microsoft.Powershell `
    -ExtensionName DSC `
    -Version 2.19 `
    -PublicConfiguration $PublicConfiguration `
    -PrivateConfiguration $PrivateConfiguration `
    -ForceUpdate

$VM | Update-AzureVM
```

## <a name="azure-virtual-machines"></a>Azure 가상 컴퓨터

Azure 자동화 DSC 사용 하면 구성 관리에 대 한 Azure 가상 컴퓨터를 쉽게 등록 hello Azure 포털, Azure 리소스 관리자 템플릿 또는 PowerShell을 사용 하 여. Hello 내부적 및 tooremote hello VM에 있는 관리자가 없으면 hello VM이 Azure 자동화 DSC 등록 hello Azure VM 필요한 상태 구성 확장 합니다. Hello에 제공 됩니다 hello Azure VM 필요한 상태 구성 확장을 비동기적으로 실행, 단계 tootrack 진행 하거나 문제를 해결 하는 이후 [ **문제를 해결 하는 Azure 가상 컴퓨터의 온 보 딩** ](#troubleshooting-azure-virtual-machine-onboarding)아래 섹션.

### <a name="azure-portal"></a>Azure portal

Hello에 [Azure 포털](https://portal.azure.com/), toohello Azure 자동화 계정을 저장할 tooonboard 가상 컴퓨터를 이동 합니다. Hello 자동화 계정 대시보드에서 **DSC 노드** -> **Azure VM 추가**합니다.

아래 **가상 컴퓨터 tooonboard 선택**하나를 선택 하거나 더 많은 Azure 가상 컴퓨터 tooonboard 합니다.

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

아래 **등록 데이터를 구성**, hello 입력 [PowerShell DSC 로컬 구성 관리자 값](https://msdn.microsoft.com/powershell/dsc/metaconfig4) 들어 사용 사례 및 필요에 따라 노드 구성 tooassign toohello VM에 필요한 합니다.

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a>Azure 리소스 관리자 템플릿

Azure 가상 컴퓨터를 배포할 수 있습니다 및 Azure 리소스 관리자 템플릿을 통해 자동화 DSC 등록 된 tooAzure 합니다. 참조 [DSC 확장을 통해 VM 및 Azure 자동화 DSC 구성](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) 는 예제 서식 파일에 대 한 해당 onboards 기존 VM tooAzure 자동화 DSC 합니다. toofind hello 등록 키 및 등록 가져온 URL이 서식이 파일을 입력으로 hello 참조 [ **등록 Secure** ](#secure-registration) 아래 섹션.

### <a name="powershell"></a>PowerShell

hello [레지스터 AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet hello PowerShell 통해 Azure 포털에서에서 가상 컴퓨터를 사용 하는 tooonboard 될 수 있습니다.

## <a name="amazon-web-services-aws-virtual-machines"></a>AWS(Amazon Web Services) 가상 컴퓨터

Hello AWS DSC 도구 키트를 사용 하 여 Azure 자동화 DSC에 의해 구성 관리용 Amazon 웹 서비스 가상 컴퓨터를 쉽게 등록할 수 있습니다. Hello 도구 키트에 대 한 자세히 알아볼 수 있습니다 [여기](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/)합니다.

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a>온-프레미스나 Azure/AWS 이외의 클라우드에 있는 실제/가상 Windows 컴퓨터

Windows 컴퓨터를 온-프레미스 및 Windows 컴퓨터 (예: Amazon 웹 서비스)-Azure 클라우드에서 수도 있습니다 전혀 tooAzure 자동화 DSC toohello 아웃 바운드 액세스를가지고 몇 가지 간단한 단계만 통해 인터넷:

1. 있는지 hello 최신 버전의 확인 [WMF 5](http://aka.ms/wmf5latest) 가 설치 되어 tooonboard tooAzure 자동화 DSC hello 컴퓨터에 원하는 합니다.
2. 섹션의 지시를 hello [ **생성 DSC metaconfigurations** ](#generating-dsc-metaconfigurations) toogenerate 아래 hello를 포함 하는 폴더는 DSC metaconfigurations 필요 합니다.
3. 원하는 tooonboard hello PowerShell DSC 메타 구성 toohello 컴퓨터를 원격으로 적용 됩니다. **이 명령을 실행 하는 hello 컴퓨터에 최신 버전의 hello 있어야 합니다. [WMF 5](http://aka.ms/wmf5latest) 설치**:

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. PowerShell DSC metaconfigurations hello를 원격으로 적용할 수 없습니다, 하는 경우 각 컴퓨터 tooonboard에 2 단계의 hello metaconfigurations 폴더를 복사 합니다. 그런 다음 호출 **Set-dsclocalconfigurationmanager** 각 컴퓨터 tooonboard에서 로컬로 합니다.
5. Hello Azure 포털 또는 cmdlet, Azure 자동화 계정에 등록 된 hello 컴퓨터 tooonboard 지금 표시 DSC 노드 검사를 사용 합니다.

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a>온-프레미스, Azure 또는 Azure 이외의 클라우드에 있는 실제/가상 Linux 컴퓨터

온-프레미스 Linux 컴퓨터의 경우 Azure에서 Linux 컴퓨터 되었고 비 Azure 클라우드에서 Linux 컴퓨터 수 있습니다, 자동화 DSC에 등록 된 tooAzure toohello 아웃 바운드 액세스를가지고 몇 가지 간단한 단계만 통해 인터넷:

1. 있는지 hello 최신 버전의 확인 [Linux 용 PowerShell 필요한 상태 구성](https://github.com/Microsoft/PowerShell-DSC-for-Linux) 가 설치 되어 tooonboard tooAzure 자동화 DSC hello 컴퓨터에 원하는 합니다.
2. 경우 hello [PowerShell DSC 로컬 구성 관리자 기본값](https://msdn.microsoft.com/powershell/dsc/metaconfig4) 들어 사용 사례를 일치 시키고 tooonboard 컴퓨터 등 원하는 **둘 다** 에서 끌어오도록 하 고 tooAzure 자동화 DSC 보고:

   + 각 Linux 컴퓨터 tooonboard tooAzure 자동화 DSC를 기본적으로 PowerShell DSC 로컬 구성 관리자는 hello를 사용 하 여 Register.py tooonboard를 사용 합니다.

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + toofind hello 등록 키 및 등록 URL 자동화 계정에 대 한 참조 hello [ **등록 Secure** ](#secure-registration) 아래 섹션.

     Hello PowerShell DSC 로컬 구성 관리자의 기본값 **않습니다** **하지** 들어 사용 사례를 찾거나 tooonboard 컴퓨터만 tooAzure 자동화 DSC 보고 되지만 끌어 오지 않고 수행 되도록 하려면 구성 또는 여기에서 PowerShell 모듈 3-6 단계를 수행 합니다. 6 toostep 직접 그렇지 않은 경우 진행 합니다.

3. Hello의 지시를 hello [ **생성 DSC metaconfigurations** ](#generating-dsc-metaconfigurations) 필요한 hello DSC metaconfigurations 들어 있는 폴더 toogenerate 아래의 섹션.
4. Tooonboard 원하는 hello PowerShell DSC 메타 구성 toohello 컴퓨터를 원격으로 적용 됩니다.

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine tooonboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

이 명령을 실행 하는 hello 컴퓨터에 최신 버전의 hello 있어야 합니다. [WMF 5](http://aka.ms/wmf5latest) 설치 합니다.

1. 각 Linux 컴퓨터 tooonboard에 대 한 PowerShell DSC metaconfigurations hello를 원격으로 적용할 수 없습니다 hello Linux 컴퓨터에 있는 5 단계에서 hello 폴더에서 hello 메타 구성은 해당 toothat 컴퓨터를 복사 합니다. 그런 다음 호출 `SetDscLocalConfigurationManager.py` tooonboard tooAzure 자동화 DSC을 원하는 각 Linux 컴퓨터에서 로컬로:

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path toometaconfiguration file>`

2. Hello Azure 포털 또는 cmdlet, Azure 자동화 계정에 등록 된 hello 컴퓨터 tooonboard 지금 표시 DSC 노드 검사를 사용 합니다.

## <a name="generating-dsc-metaconfigurations"></a>DSC 메타 구성 생성

toogenerically tooAzure 자동화 DSC 모든 컴퓨터 온보드는 [DSC 메타 구성](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) 수 tooAzure 자동화 DSC 보고 및/또는 DSC hello 에이전트에서 컴퓨터 toopull hello에 지시, 적용 하는 경우에 생성 합니다. Azure 자동화 DSC에 대 한 DSC metaconfigurations PowerShell DSC 구성을 또는 hello Azure 자동화 PowerShell cmdlet을 사용 하 여 생성할 수 있습니다.

> [!NOTE]
> DSC metaconfigurations hello 필요한 비밀 tooonboard 컴퓨터 tooan 관리에 대 한 자동화 계정 포함합니다. 있는지 tooproperly를 만들면 모든 DSC metaconfigurations 보호 하거나 사용 후 삭제를 확인 합니다.

### <a name="using-a-dsc-configuration"></a>DSC 구성 사용

1. 로컬 환경에서 컴퓨터에서 관리자 권한으로 PowerShell ISE hello를 엽니다. hello 컴퓨터에 최신 버전의 hello 있어야 [WMF 5](http://aka.ms/wmf5latest) 설치 합니다.
2. 다음 스크립트를 로컬로 hello를 복사 합니다. 이 스크립트는 metaconfigurations, 및 hello 메타 구성 만들기 오프 명령 tookick 만들기에 대 한 PowerShell DSC 구성을 포함 합니다.

    ```powershell
    # hello DSC configuration that will generate metaconfigurations
    [DscLocalConfigurationManager()]
    Configuration DscMetaConfigs
    {

        param
        (
            [Parameter(Mandatory=$True)]
            [String]$RegistrationUrl,

            [Parameter(Mandatory=$True)]
            [String]$RegistrationKey,

            [Parameter(Mandatory=$True)]
            [String[]]$ComputerName,

            [Int]$RefreshFrequencyMins = 30,

            [Int]$ConfigurationModeFrequencyMins = 15,

            [String]$ConfigurationMode = "ApplyAndMonitor",

            [String]$NodeConfigurationName,

            [Boolean]$RebootNodeIfNeeded= $False,

            [String]$ActionAfterReboot = "ContinueConfiguration",

            [Boolean]$AllowModuleOverwrite = $False,

            [Boolean]$ReportOnly
        )

        if(!$NodeConfigurationName -or $NodeConfigurationName -eq "")
        {
            $ConfigurationNames = $null
        }
        else
        {
            $ConfigurationNames = @($NodeConfigurationName)
        }

        if($ReportOnly)
        {
        $RefreshMode = "PUSH"
        }
        else
        {
        $RefreshMode = "PULL"
        }

        Node $ComputerName
        {

            Settings
            {
                RefreshFrequencyMins = $RefreshFrequencyMins
                RefreshMode = $RefreshMode
                ConfigurationMode = $ConfigurationMode
                AllowModuleOverwrite = $AllowModuleOverwrite
                RebootNodeIfNeeded = $RebootNodeIfNeeded
                ActionAfterReboot = $ActionAfterReboot
                ConfigurationModeFrequencyMins = $ConfigurationModeFrequencyMins
            }

            if(!$ReportOnly)
            {
            ConfigurationRepositoryWeb AzureAutomationDSC
                {
                    ServerUrl = $RegistrationUrl
                    RegistrationKey = $RegistrationKey
                    ConfigurationNames = $ConfigurationNames
                }

                ResourceRepositoryWeb AzureAutomationDSC
                {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
                }
            }

            ReportServerWeb AzureAutomationDSC
            {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
            }
        }
    }

    # Create hello metaconfigurations
    # TODO: edit hello below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM tooonboard>', '<some other VM tooonboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set too$True toohave machines only report tooAA DSC but not pull from it
    }

    # Use PowerShell splatting toopass parameters toohello DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. Hello 형태의 hello 컴퓨터 tooonboard 물론 자동화 계정에 대 한 hello 등록 키 및 URL 입력 합니다. 모든 다른 매개 변수는 선택 사항입니다. toofind hello 등록 키 및 등록 URL 자동화 계정에 대 한 참조 hello [ **등록 Secure** ](#secure-registration) 아래 섹션.
4. Hello 컴퓨터 tooreport DSC 상태 정보 tooAzure 자동화 DSC 하지만 구성 또는 PowerShell 모듈 끌어 오지 않고, 설정 hello **ReportOnly** tootrue 매개 변수입니다.
5. Hello 스크립트를 실행 합니다. 라는 폴더를 만들었습니다 **DscMetaConfigs** 포함 된 hello PowerShell DSC metaconfigurations (관리자 권한)으로 컴퓨터 tooonboard hello에 대 한 작업 디렉터리에서:

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-hello-azure-automation-cmdlets"></a>Hello Azure 자동화 cmdlet을 사용 하 여

Hello Azure 자동화 cmdlet hello DSC 생성 하는 간단한 방법을 제공 hello PowerShell DSC 로컬 구성 관리자 기본값 일치 들어 사용 사례에서 끌어오도록와 tooAzure 자동화 DSC 보고 되도록 tooonboard 컴퓨터를 사용할 경우 metaconfigurations 필요:

1. 로컬 환경에서 컴퓨터의 hello PowerShell 콘솔 또는 관리자 권한으로 PowerShell ISE를 엽니다.
2. TooAzure 리소스 관리자를 사용 하 여 연결 **AzureRmAccount 추가**
3. Hello 자동화에서에서 tooonboard hello 컴퓨터 tooonboard 노드가 toowhich 계정에 대 한 PowerShell DSC metaconfigurations hello를 다운로드 합니다.

    ```powershell
    # Define hello parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # hello name of hello ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # hello name of hello Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # hello names of hello computers that hello meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting toopass parameters toohello Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. 라는 폴더를 만들었습니다 ***DscMetaConfigs***, (관리자 권한)으로 컴퓨터 tooonboard hello에 대 한 PowerShell DSC metaconfigurations hello 포함:
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a>등록 보호

컴퓨터에 안전 하 게 온보드 tooan을 DSC 노드 tooauthenticate tooa PowerShell DSC V2 끌어오기 또는 보고 서버 (Azure 자동화 DSC 포함)를 사용 하면 hello WMF 5 DSC 등록 프로토콜을 통해 Azure 자동화 계정을 수 있습니다. hello 노드가 toohello 서버에 등록 한 **등록 URL**, 사용 하 여 인증 한 **등록 키**합니다. 등록 하는 동안 hello DSC 노드 및 DSC 끌어오기/보고 서버 인증 toohello 서버 후 등록에 대 한 노드 toouse이에 대 한 고유한 인증서를 협상합니다. 이 프로세스는 노드가 손상되어 악의적 동작을 수행하는 등, 온보드된 노드가 다른 노드를 가장하는 것을 방지합니다.  등록 후 hello 등록 키 다시 인증을 위해 사용 되지 않으며 hello 노드에서 삭제 됩니다.

Hello에서 DSC hello 등록 프로토콜에 필요한 hello 정보를 읽을 수 **키 관리** 블레이드 hello Azure 미리 보기 포털에서 합니다. Hello hello 키 아이콘을 클릭 하 여이 블레이드를 엽니다 **Essentials** hello 자동화 계정에 대 한 패널입니다.

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* 등록 URL에는 hello 키 관리 블레이드에서 hello URL 필드입니다.
* 등록 키가 hello 키 관리 블레이드 hello 기본 액세스 키 또는 보조 액세스 키입니다. 둘 중 하나를 사용할 수 있습니다.

추가 보안을 위해 자동화 계정의 hello 기본 및 보조 액세스 키 다시 생성 될 수 언제 든 지 (hello에 **키 관리** 블레이드) 이전 키를 사용 하 여 tooprevent 이후 노드 등록 합니다.

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a>Azure 가상 컴퓨터 온보드 문제 해결

Azure 자동화 DSC를 사용하면 구성 관리를 위해 간편하게 Azure Windows VM을 온보드할 수 있습니다. Hello 내부적 hello Azure VM 필요한 상태 구성 확장은 사용 되는 tooregister hello Azure 자동화 DSC를 사용 하 여 VM입니다. Hello Azure VM 필요한 상태 구성 확장을 비동기적으로 실행, 진행 상황을 추적 하 고 해당 실행 문제 해결 중요 될 수 있습니다.

> [!NOTE]
> 어떤 방법을 온 보 딩이 Azure 자동화에 등록 된 Windows Azure VM tooAzure hello Azure VM 필요한 상태 구성 확장을 사용 하는 자동화 DSC를 노드 tooshow hello에 대 한 tooan 시간 걸릴 수 있습니다. 필요한 tooonboard hello VM tooAzure 자동화 DSC hello Azure VM DSC 확장에 의해 hello VM에서 Windows Management Framework 5.0 toohello 설치 기한입니다.

hello hello Azure 포털에서에서 Azure VM 필요한 상태 구성 확장의 tootroubleshoot 또는 보기 hello 상태 탐색 toohello 등록 되 고 VM을 다음 클릭-> **모든 설정을** -> **확장**   ->  **DSC**합니다. 자세한 내용을 보려면 **자세한 상태 보기**를 클릭합니다.

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a>인증서 만료 및 다시 등록

등록 한 후 컴퓨터를 Azure 자동화 DSC에 DSC 노드로,는 다양 한 이유로 해야 tooreregister hello에서 해당 노드 이후

* 등록 후에는 1년 후 만료되는 인증에 대해 각 노드가 자동으로 고유의 인증서를 협상합니다. 현재 PowerShell DSC 등록 프로토콜 hello 필요 tooreregister hello 노드는 1 년의 시간이 지난 후, 만료가 가까운 될 때에 자동으로 인증서 갱신할 수 없습니다. 다시 등록하기 전에 각 노드가 Windows Management Framework 5.0 RTM을 실행 중인지 확인합니다. 노드 인증 인증서의 만료 날짜 hello 노드 하지 재등록 하는 경우 hello Azure 자동화에 없습니다 toocommunicate 됩니다. 노드와 'Unresponsive'으로 표시 됩니다. 다시 등록 90 일을 수행 하거나, hello 인증서 만료 시간에서 작거나 hello 인증서 만료 시간 이후 언제 라도 생성 하 고 사용 되 고 새 인증서.
* toochange 모든 [PowerShell DSC 로컬 구성 관리자 값](https://msdn.microsoft.com/powershell/dsc/metaconfig4) ConfigurationMode 같은 hello 노드 초기 등록 하는 동안 설정 된입니다. 현재 DSC 에이전트 값은 다시 등록을 통해 변경될 수 있습니다. hello 한 가지 예외는 hello 지정 된 toohello 노드의 노드 구성에 직접 Azure 자동화 DSC에서 변경할 수 있습니다.

이 문서에 설명 된 등록 hello 노드 처음에 hello 온 보 딩 방법 중 하나를 사용 하 여 동일한 방식으로 hello에 다시 등록을 수행할 수 있습니다. 이 다시 등록 하기 전에 Azure 자동화 DSC에서 노드 toounregister가 필요가 없습니다.

## <a name="related-articles"></a>관련 문서

* [Azure 자동화 DSC 개요](automation-dsc-overview.md)
* [Azure 자동화 DSC cmdlets](/powershell/module/azurerm.automation/#automation)
* [Azure 자동화 DSC 가격 책정](https://azure.microsoft.com/pricing/details/automation/)
