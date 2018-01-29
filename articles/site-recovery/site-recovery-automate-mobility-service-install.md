---
title: "Azure Automation DSC를 사용하여 Site Recovery 모바일 서비스 배포 | Microsoft Docs"
description: "Azure Automation DSC를 사용하여 Azure Site Recovery 모바일 서비스 및 VMware VM과 물리적 서버 복제를 위한 Azure 에이전트를 자동으로 배포하는 방법에 대해 설명합니다."
services: site-recovery
documentationcenter: 
author: krnese
manager: lorenr
editor: 
ms.assetid: 1f8cd3ac-0522-48eb-a5f0-679ee9192ddb
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2017
ms.author: krnese
ms.openlocfilehash: 118a2e775ae3d036f58989d9778104e372e8c701
ms.sourcegitcommit: 310748b6d66dc0445e682c8c904ae4c71352fef2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2017
---
# <a name="deploy-the-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a>VM 복제를 위해 Azure Automation DSC를 사용하여 모바일 서비스 배포
Operations Management Suite에서는 무중단 업무 방식 계획의 일부분으로 사용 가능한 포괄적인 백업 및 재해 복구 솔루션이 제공됩니다.

처음에는 Hyper-V에서 Hyper-V 복제본을 통해 이러한 솔루션이 제공되었습니다. 하지만 고객의 클라우드에는 여러 하이퍼바이저와 플랫폼이 포함되어 있으므로, 다른 유형의 설정을 지원하도록 솔루션 범위가 확장되었습니다.

현재 VMware 작업 및/또는 실제 서버를 실행 중인 경우 관리 서버가 환경 내의 모든 Azure Site Recovery 구성 요소를 실행하여 Azure와의 통신 및 데이터 복제를 처리합니다(Azure가 대상인 경우).

## <a name="deploy-the-site-recovery-mobility-service-by-using-automation-dsc"></a>Automation DSC를 사용하여 Site Recovery 모바일 서비스 배포
먼저 이 관리 서버가 수행하는 작업을 간략하게 살펴보겠습니다.

관리 서버는 다양한 서버 역할을 실행합니다. 이러한 역할 중 하나인 *구성*은 통신을 조정하고 데이터 복제 및 복구 프로세스를 관리합니다.

그리고 *프로세스* 역할은 복제 게이트웨이 역할을 합니다. 이 역할은 보호된 소스 컴퓨터에서 복제 데이터를 수신하여 캐싱, 압축 및 암호화용으로 최적화한 다음 Azure 저장소 계정으로 전송합니다. 보호된 컴퓨터에 대한 모바일 서비스의 강제 설치를 실행하고 VMware VM의 자동 검색을 수행하는 것도 프로세스 역할의 기능 중 하나입니다.

Azure에서 장애 복구(failback)가 수행되면 *마스터 대상* 역할이 이 작업의 일부로 복제 데이터를 처리합니다.

보호된 컴퓨터의 경우에는 *모바일 서비스*를 사용합니다. 이 구성 요소는 Azure에 복제하려는 모든 컴퓨터(VMware VM 또는 실제 서버)에 배포되며, 컴퓨터에서 데이터 쓰기를 캡처하여 관리 서버(프로세스 역할)로 전달합니다.

무중단 업무 방식을 사용해야 하는 경우에는 작업, 인프라 및 관련 구성 요소를 파악해야 합니다. 그러면 RTO(복구 시간 목표) 및 RPO(복구 지점 목표) 관련 요구 사항을 충족할 수 있습니다. 이 컨텍스트에서는 작업을 원하는 방식으로 보호하는 데 핵심적인 요소는 모바일 서비스입니다.

몇 가지 Operations Management Suite 구성 요소를 활용하면 안정적인 보호 설정이 적용되어 있는지를 최적화된 방식으로 확인할 수 있습니다.

이 문서에서는 Azure Automation DSC(필요한 상태 구성)를 Site Recovery와 함께 사용하여 다음을 확인하는 방법의 예를 제공합니다.

* 모바일 서비스와 Azure VM 에이전트가 보호하려는 Windows 컴퓨터에 배포되어 있습니다.
* Azure가 복제 대상일 때 모바일 서비스와 Azure VM 에이전트가 항상 실행됩니다.

## <a name="prerequisites"></a>필수 조건
* 필수 설치 프로그램을 저장할 저장소
* 관리 서버에 등록하기 위해 필요한 암호를 저장할 저장소

  > [!NOTE]
  > 각 관리 서버에 대해 고유한 암호가 생성됩니다. 여러 관리 서버를 배포하려는 경우 올바른 암호가 passphrase.txt 파일에 저장되어 있는지 확인해야 합니다.
  >
  >
* 보호할 수 있도록 설정하려는 컴퓨터에 WMF(Windows Management Framework) 5.0 설치(Automation DSC의 요구 사항)

  > [!NOTE]
  > WMF 4.0이 설치되어 있는 Windows 컴퓨터에 대해 DSC를 사용하려는 경우 [연결이 끊어진 환경에서 DSC 사용](## Use DSC in disconnected environments) 섹션을 참조하세요.
  

모바일 서비스는 명령줄을 통해 설치할 수 있으며 여러 인수를 허용합니다. 그러므로 설치에서 이진 파일을 추출한 다음 DSC 구성을 사용하여 검색할 수 있는 위치에 저장해야 합니다.

## <a name="step-1-extract-binaries"></a>1단계: 이진 파일 추출
1. 이 설치에 필요한 파일을 추출하려면 관리 서버에서 다음 디렉터리로 이동합니다.

    **\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**

    이 폴더에 다음과 같은 이름의 MSI 파일이 표시됩니다.

    **Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**

    다음 명령을 사용하여 설치 관리자를 추출합니다.

    **.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**
2. 모든 파일을 선택하여 압축된(zip) 폴더로 전송합니다.

이제 자동화 DSC를 사용하여 모바일 서비스의 설치를 자동화하는 데 필요한 이진 파일이 준비되었습니다.

### <a name="passphrase"></a>암호
다음으로, 이 압축된 폴더를 배치할 위치를 결정해야 합니다. 이 문서의 뒷부분에서 설명하는 대로 Azure 저장소 계정을 사용하여 설치에 필요한 암호를 저장할 수 있습니다. 그러면 프로세스의 일부분으로 에이전트가 관리 서버에 등록됩니다.

관리 서버를 배포할 때 받은 암호를 텍스트 파일(passphrase.txt)로 저장할 수 있습니다.

zip 폴더와 암호를 모두 Azure 저장소 계정의 전용 컨테이너에 저장합니다.

![폴더 위치](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

이러한 파일은 네트워크의 공유에 보관해도 됩니다. 나중에 사용할 DSC 리소스에 액세스할 수 있으며 설치 프로그램과 암호를 가져올 수 있는지 확인하기만 하면 됩니다.

## <a name="step-2-create-the-dsc-configuration"></a>2단계: DSC 구성 만들기
설치에서는 WMF 5.0을 사용합니다. 컴퓨터가 Automation DSC를 통해 구성을 올바르게 적용하도록 하려면 WMF 5.0이 있어야 합니다.

이 환경에서는 다음과 같은 예제 DSC 구성을 사용합니다.

```powershell
configuration ASRMobilityService {

    $RemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    $RemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    $RemoteAzureAgent = 'http://go.microsoft.com/fwlink/p/?LinkId=394789'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node localhost {

        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
```
이 구성은 다음을 수행합니다.

* 변수를 통해 모바일 서비스 및 Azure VM 에이전트용 이진 파일 및 암호를 가져올 위치와 출력을 저장할 위치를 구성에서 지정합니다.
* `xRemoteFile` 을 사용하여 리포지토리에서 파일을 다운로드할 수 있도록 xPSDesiredStateConfiguration DSC 리소스를 가져옵니다.
* 이진 파일을 저장할 디렉터리를 만듭니다.
* 보관 리소스를 통해 zip 폴더에서 파일을 추출합니다.
* 패키지 Install 리소스를 통해 지정된 인수를 사용하여 UNIFIEDAGENT.EXE 설치 관리자에서 모바일 서비스를 설치합니다. 이때 인수를 생성하는 변수는 실제 환경을 반영하도록 변경해야 합니다.
* 패키지 AzureAgent 리소스를 통해 Azure VM 에이전트를 설치합니다. Azure에서 실행되는 모든 VM에서는 Azure VM 에이전트를 사용하는 것이 좋습니다. Azure VM 에이전트를 사용하면 장애 조치(failover) 이후 VM에 확장을 추가할 수도 있습니다.
* 하나 이상의 서비스 리소스를 통해 관련 모바일 서비스 및 Azure 서비스가 항상 실행되도록 합니다.

구성을 **ASRMobilityService**로 저장합니다.

> [!NOTE]
> 에이전트가 정상적으로 연결되고 올바른 암호를 사용하도록 하려면 실제 관리 서버를 반영하도록 구성의 CSIP를 바꾸세요.
>
>

## <a name="step-3-upload-to-automation-dsc"></a>3단계: Automation DSC 업로드
이전 단계에서 작성한 DSC 구성은 필수 DSC 리소스 모듈(xPSDesiredStateConfiguration)을 가져오므로 DSC 구성을 업로드하기 전에 Automation에서 해당 모듈을 가져와야 합니다.

Automation 계정에 로그인하여 **자산** > **모듈**로 이동한 다음 **갤러리 찾아보기**를 클릭합니다.

여기서 모듈을 검색하고 계정으로 가져올 수 있습니다.

![가져오기 모듈](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

이 작업이 완료되면 Azure Resource Manager 모듈이 설치된 컴퓨터로 이동하여 새로 만든 DSC 구성 가져오기를 계속 진행합니다.

### <a name="import-cmdlets"></a>Cmdlet 가져오기
PowerShell에서 Azure 구독에 로그인합니다. 그런 다음 실제 환경을 반영하도록 cmdlet을 수정하고 변수에서 Automation 계정 정보를 캡처합니다.

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

다음 cmdlet을 사용하여 구성을 Automation DSC에 업로드합니다.

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-the-configuration-in-automation-dsc"></a>Automation DSC의 구성 컴파일
다음으로는 노드를 구성에 등록할 수 있도록 Automation DSC의 구성을 컴파일해야 합니다. 다음 cmdlet을 실행하여 이 목적을 달성합니다.

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

기본적으로는 구성을 호스트된 DSC 끌어오기 서비스로 배포하므로 컴파일은 몇 분 정도 걸릴 수 있습니다.

구성을 컴파일한 후에는 PowerShell(Get-AzureRmAutomationDscCompilationJob) 또는 [Azure 포털](https://portal.azure.com/)을 사용하여 작업 정보를 검색할 수 있습니다.

![작업 검색](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

이제 DSC 구성을 Automation DSC에 게시 및 업로드했습니다.

## <a name="step-4-onboard-machines-to-automation-dsc"></a>4단계: Automation DSC에 컴퓨터 등록
> [!NOTE]
> 이 시나리오를 완료하기 위한 필수 구성 요소 중 하나는 WMF의 최신 버전을 설치하여 Windows 컴퓨터를 업데이트하는 것입니다. [다운로드 센터](https://www.microsoft.com/download/details.aspx?id=50395)에서 사용 중인 플랫폼에 적합한 버전을 다운로드하여 설치할 수 있습니다.
>
>

이제 노드에 적용할 DSC용 metaconfig를 만듭니다. 이 작업에 성공하려면 Azure에서 선택한 Automation 계정에 대한 끝점 URL과 기본 키를 검색해야 합니다. 이러한 값은 Automation 계정 **모든 설정** 블레이드의 **키** 아래에 나와 있습니다.

![키 값](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

이 예제에서는 Windows Server 2012 R2 실제 서버를 Site Recovery로 보호하려고 합니다.

### <a name="check-for-any-pending-file-rename-operations-in-the-registry"></a>레지스트리에서 보류 중인 파일 이름 바꾸기 작업 확인
Automation DSC 끝점과 서버 연결을 시작하기 전에 레지스트리에서 보류 중인 파일 이름 바꾸기 작업이 있는지 확인하는 것이 좋습니다. 이러한 작업이 있으면 보류 중인 다시 부팅으로 인해 설치 프로그램을 완료하지 못할 수 있습니다.

다음 cmdlet을 실행하여 서버에 보류 중인 다시 부팅이 없는지 확인:

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
결과에 아무 항목도 표시되지 않으면 계속 진행해도 됩니다. 그렇지 않은 경우 유지 관리 기간 동안 서버를 다시 부팅하여 이 상황을 해소해야 합니다.

서버에서 구성을 적용하려면 PowerShell ISE(통합 스크립팅 환경)를 시작하고 다음 스크립트를 실행합니다. 이 스크립트는 기본적으로 로컬 구성 관리자 엔진에 대해 Automation DSC 서비스에 등록하고 특정 구성(ASRMobilityService.localhost)을 검색하도록 지시하는 DSC 로컬 구성입니다.

```powershell
[DSCLocalConfigurationManager()]
configuration metaconfig {
    param (
        $URL,
        $Key
    )
    node localhost {
        Settings {
            RefreshFrequencyMins = '30'
            RebootNodeIfNeeded = $true
            RefreshMode = 'PULL'
            ActionAfterReboot = 'ContinueConfiguration'
            ConfigurationMode = 'ApplyAndMonitor'
            AllowModuleOverwrite = $true
        }

        ResourceRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }

        ConfigurationRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
            ConfigurationNames = 'ASRMobilityService.localhost'
        }

        ReportServerWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }
    }
}
metaconfig -URL 'https://we-agentservice-prod-1.azure-automation.net/accounts/<YOURAAAccountID>' -Key '<YOURAAAccountKey>'

Set-DscLocalConfigurationManager .\metaconfig -Force -Verbose
```

이 구성을 사용하는 경우 로컬 구성 관리자 엔진이 Automation DSC에 등록됩니다. 이 스크립트는 엔진 작동 방식, 구성 드리프트 발생 시에 수행할 작업(ApplyAndAutoCorrect), 그리고 다시 부팅이 필요한 경우 구성을 진행할 방법도 결정합니다.

이 스크립트를 실행하고 나면 Automation DSC에 노드가 등록되기 시작합니다.

![노드 등록 진행 중](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

Azure 포털로 돌아가면 새로 등록한 노드가 포털에 표시됩니다.

![포털에 등록된 노드](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

서버에서 다음 PowerShell cmdlet을 실행하여 노드가 올바르게 등록되었는지 확인할 수 있습니다.

```powershell
Get-DscLocalConfigurationManager
```

구성을 끌어와 서버에 적용한 후에는 다음 cmdlet을 실행하여 수행된 작업을 확인할 수 있습니다.

```powershell
Get-DscConfigurationStatus
```

출력에 서버가 해당 구성을 가져온 것으로 나타납니다.

![출력](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

또한 모바일 서비스 설정에는 *SystemDrive*\ProgramData\ASRSetupLogs에서 확인할 수 있는 자체의 로그가 있습니다.

지금까지 Site Recovery를 사용하여 보호하려는 컴퓨터에서 모바일 서비스를 배포하고 등록했습니다. DSC를 사용하면 필요한 서비스가 항상 실행되도록 할 수 있습니다.

![배포 정상 완료](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

관리 서버가 정상적으로 배포된 서비스를 검색하면 Site Recovery를 사용하여 컴퓨터에서 보호를 구성하고 복제를 사용하도록 설정할 수 있습니다.

## <a name="use-dsc-in-disconnected-environments"></a>연결이 끊어진 환경에서 DSC 사용
컴퓨터가 인터넷에 연결되어 있지 않은 경우에도 DSC를 사용하여 보호하려는 작업에 대해 모바일 서비스를 배포하고 구성할 수 있습니다.

환경에서 자체 DSC 끌어오기 서버를 인스턴스화하면 궁극적으로는 Automation DSC에서 제공되는 것과 같은 기능을 제공할 수 있습니다. 즉, 클라이언트가 등록된 구성을 DSC 끝점으로 끌어옵니다. DSC 구성을 로컬로 또는 원격으로 컴퓨터에 수동으로 밀어넣는 옵션도 있습니다.

이 예제에는 컴퓨터에 이름에 해당하는 매개 변수가 추가됩니다. 현재 원격 파일은 보호하려는 컴퓨터에서 액세스할 수 있어야 하는 원격 공유에 있습니다. 스크립트가 종료되면 구성이 작동하며, 그러면 대상 컴퓨터에 대한 DSC 구성 적용이 시작됩니다.

### <a name="prerequisites"></a>필수 조건
XPSDesiredStateConfiguration PowerShell 모듈이 설치되어 있는지 확인합니다. WMF 5.0이 설치된 Windows 컴퓨터의 경우 대상 컴퓨터에서 다음 cmdlet을 실행하여 xPSDesiredStateConfiguration 모듈을 설치할 수 있습니다.

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

WMF 4.0이 설치되어 있는 Windows 컴퓨터에 배포해야 하는 경우에는 모듈을 다운로드하여 저장할 수도 있습니다. PowerShellGet(WMF 5.0)이 설치되어 있는 컴퓨터에서는 다음 cmdlet을 실행합니다.

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

WMF 4.0의 경우에는 컴퓨터에 [Windows 8.1 업데이트 KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) 이 설치되어 있는지도 확인합니다.

WMF 5.0 및 WMF 4.0이 설치되어 있는 Windows 컴퓨터에 다음 구성을 밀어 넣을 수 있습니다.

```powershell
configuration ASRMobilityService {
    param (
        [Parameter(Mandatory=$true)]
        [ValidateNotNullOrEmpty()]
        [System.String] $ComputerName
    )

    $RemoteFile = '\\myfileserver\share\asr.zip'
    $RemotePassphrase = '\\myfileserver\share\passphrase.txt'
    $RemoteAzureAgent = '\\myfileserver\share\AzureVmAgent.msi'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node $ComputerName {      
        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
ASRMobilityService -ComputerName 'MyTargetComputerName'

Start-DscConfiguration .\ASRMobilityService -Wait -Force -Verbose
```

Automation DSC에서 제공되는 것과 비슷한 기능을 제공하기 위해 회사 네트워크에서 자체 DSC 끌어오기 서버를 인스턴스화하려는 경우 [DSC 웹 끌어오기 서버 설정](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396)을 참조하세요.

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a>선택 사항: Azure Resource Manager 템플릿을 사용하여 DSC 구성 배포
이 문서의 앞부분에서는 고유한 DSC 구성을 만들어 모바일 서비스 및 Azure VM 에이전트를 자동으로 배포하고, 보호하려는 컴퓨터에서 모바일 서비스와 에이전트가 실행되고 있는지를 확인하는 방법을 중점적으로 설명했습니다. 이 DSC 구성을 신규 또는 기존 Azure Automation 계정으로 배포하는 Azure Resource Manager 템플릿도 제공됩니다. 이 템플릿은 입력 매개 변수를 사용하여 실제 환경에 맞는 변수를 포함하는 Automation 자산을 만듭니다.

템플릿을 배포한 후에는 이 가이드의 4단계를 참조해 컴퓨터를 등록하면 됩니다.

템플릿은 다음 작업을 수행합니다.

1. 기존 Automation 계정을 사용하거나 새로운 계정을 만듭니다.
2. 다음에 해당하는 입력 매개 변수를 가져옵니다.
   * ASRRemoteFile - 모바일 서비스 설치 프로그램을 저장한 위치
   * ASRPassphrase - passphrase.txt 파일을 저장한 위치
   * ASRCSEndpoint - 관리 서버의 IP 주소
3. xPSDesiredStateConfiguration PowerShell 모듈을 가져옵니다.
4. DSC 구성을 만들고 컴파일합니다.

위의 모든 단계는 올바른 순서로 수행되므로 해당 단계가 완료되면 보호할 컴퓨터 등록을 시작할 수 있습니다.

배포 지침이 포함된 템플릿은 [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC)에 있습니다.

아래 PowerShell을 사용하여 템플릿을 배포합니다.

```powershell
$RGDeployArgs = @{
    Name = 'DSC3'
    ResourceGroupName = 'KNOMS'
    TemplateFile = 'https://raw.githubusercontent.com/krnese/AzureDeploy/master/OMS/MSOMS/DSC/azuredeploy.json'
    OMSAutomationAccountName = 'KNOMSAA'
    ASRRemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    ASRRemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    ASRCSEndpoint = '10.0.0.115'
    DSCJobGuid = [System.Guid]::NewGuid().ToString()
}
New-AzureRmResourceGroupDeployment @RGDeployArgs -Verbose
```

## <a name="next-steps"></a>다음 단계
모바일 서비스 에이전트를 배포한 후 가상 컴퓨터에 대해 [복제를 사용하도록 설정](site-recovery-vmware-to-azure.md) 할 수 있습니다.
