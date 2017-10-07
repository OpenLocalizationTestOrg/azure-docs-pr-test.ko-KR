---
title: "aaaDeploy hello Azure 자동화 dsc 사이트 복구 모바일 서비스 | Microsoft Docs"
description: "Toouse Azure 자동화 DSC tooautomatically 복제 tooAzure 물리적 서버와 VMware VM에 대 한 hello Azure 사이트 복구 모바일 서비스 및 Azure 에이전트를 배포 방법에 대해 설명"
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
ms.date: 08/01/2017
ms.author: krnese
ms.openlocfilehash: 52cdd13ceb61718a21137180c55db86919af5929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a>VM 복제 하기 위해 Azure 자동화 dsc hello 모바일 서비스를 배포 합니다.
Operations Management Suite에서는 무중단 업무 방식 계획의 일부분으로 사용 가능한 포괄적인 백업 및 재해 복구 솔루션이 제공됩니다.

처음에는 Hyper-V에서 Hyper-V 복제본을 통해 이러한 솔루션이 제공되었습니다. 했지만 확장 된 toosupport 다른 유형의 설치 프로그램 및 때문에 고객 여러 하이퍼바이저 플랫폼의 클라우드.

실행 하는 경우 VMware 작업 부하 및/또는 실제 서버 오늘, 관리 서버 hello의 모든 Azure Site Recovery 구성 요소 사용자 환경 toohandle hello 통신 및 데이터 복제에 Azure 통해가 있을 때 실행 Azure 대상입니다.

## <a name="deploy-hello-site-recovery-mobility-service-by-using-automation-dsc"></a>자동화 DSC를 사용 하 여 hello 사이트 복구 모바일 서비스 배포
먼저 이 관리 서버가 수행하는 작업을 간략하게 살펴보겠습니다.

hello 관리 서버는 여러 서버 역할을 실행합니다. 이러한 역할 중 하나인 *구성*은 통신을 조정하고 데이터 복제 및 복구 프로세스를 관리합니다.

또한 hello *프로세스* 역할은 게이트웨이 역할을 복제 합니다. 이 역할 보호 된 원본 컴퓨터에서 복제 데이터를 수신, 캐싱, 압축 및 암호화를 사용 하 여이 최적화 하 고 tooan Azure 저장소 계정 보냅니다. Hello 프로세스 역할에 대 한 hello 함수 중 하나는 또한 hello 이동성 서비스 tooprotected 컴퓨터의 toopush 설치 및 VMware Vm의 자동 검색을 수행 합니다.

Azure에서 장애 복구 이면 hello *마스터 대상* 역할이이 작업의 일부로 hello 복제 데이터를 처리 합니다.

Hello 보호 된 컴퓨터에 대 한 hello에 의존 *모바일 서비스*합니다. 이 구성 요소는 원하는 tooreplicate tooAzure tooevery 배포 된 컴퓨터 (VMware VM 또는 실제 서버). Hello 컴퓨터에 데이터 쓰기 캡처하고 toohello 관리 서버 (프로세스 역할)에 전달 합니다.

비즈니스 연속성을 다룰 때 중요 한 toounderstand 작업, 인프라 및 hello 구성 요소와 관련 됩니다. 그런 다음 복구 시간 목표 (RTO) 및 복구 지점 목표 (RPO)에 대 한 hello 요구 사항을 충족 시킬 수 있습니다. 이 컨텍스트에서 hello 모바일 서비스는 키 tooensuring 예상 작업 보호 되는 합니다.

몇 가지 Operations Management Suite 구성 요소를 활용하면 안정적인 보호 설정이 적용되어 있는지를 최적화된 방식으로 확인할 수 있습니다.

이 문서에서는 Azure 자동화 DSC 필요한 상태 구성 (), tooensure 사이트 복구와 함께 사용 하는 방법의 예입니다.

* hello 모바일 서비스와 Azure VM 에이전트는 원하는 tooprotect 배포 toohello Windows 컴퓨터입니다.
* hello 모바일 서비스와 Azure VM 에이전트는 항상 때 실행 중 Azure hello 복제 대상입니다.

## <a name="prerequisites"></a>필수 조건
* 리포지토리 toostore hello 필수 설정
* 리포지토리 toostore hello hello 관리 서버와 공유 암호 tooregister 필요

  > [!NOTE]
  > 각 관리 서버에 대해 고유한 암호가 생성됩니다. 보아야 toodeploy 여러 관리 서버, 해야 tooensure 해당 hello 올바른 암호 hello passphrase.txt 파일에 저장 됩니다.
  >
  >
* Windows Management Framework (WMF) 5.0 (자동화 DSC에 대 한 요구 사항) 보호를 위해 tooenable 되도록 hello 컴퓨터에 설치 되어

  > [!NOTE]
  > WMF 4.0이 설치 되어 있는 toouse DSC에 대 한 Windows 컴퓨터를 원하는 경우 hello 섹션을 참조 하세요. [연결이 끊어진된 환경에서 사용 하 여 DSC](## Use DSC in disconnected environments)합니다.
  

hello 모바일 서비스 hello 명령줄을 통해 설치할 수 있으며 여러 인수를 허용 합니다. 바로 이러한 이유로 toohave hello 이진 파일 (설치에서 압축을 풀어) 이후 필요 하 고 DSC 구성을 사용 하 여 검색할 수 있습니다 장소에 보관 합니다.

## <a name="step-1-extract-binaries"></a>1단계: 이진 파일 추출
1. tooextract hello 필요한 파일을이 설치 프로그램에 대 한 관리 서버에 디렉터리를 다음 toohello를 이동 합니다.

    **\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**

    이 폴더에 다음과 같은 이름의 MSI 파일이 표시됩니다.

    **Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**

    사용 하 여 hello 다음 명령은 tooextract hello 설치 관리자:

    **.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**
2. 모든 파일을 선택 하 고 tooa 압축된 (zip) 폴더를 보내야 합니다.

자동화 DSC를 사용 하 여 hello 모바일 서비스의 tooautomate hello 설치 해야 하는 hello 바이너리 생깁니다.

### <a name="passphrase"></a>암호
다음으로, 저장할 tooplace이 zip 폴더 toodetermine를 해야 합니다. 표시 된 나중에 toostore hello 암호 hello 설치에 필요한 Azure 저장소 계정에 사용할 수 있습니다. hello 에이전트는 hello 프로세스의 일부로 hello 관리 서버를 등록 합니다.

hello 관리 서버를 배포할 때 가져온 hello 암호 passphrase.txt로 tooa 텍스트 파일로 저장할 수 있습니다.

Hello Azure 저장소 계정에서에서 전용된 컨테이너에서 hello 압축 된 폴더와 hello 암호를 배치 합니다.

![폴더 위치](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

원하는 경우 tookeep 이러한 파일 공유에 네트워크에서이 수행할 수 있습니다. 나중에 사용할 계획 hello DSC 리소스 액세스 개이고 hello 설정 및 암호를 가져올 수 tooensure를 하기만 하면 됩니다.

## <a name="step-2-create-hello-dsc-configuration"></a>2 단계: hello DSC 구성 만들기
hello 설치 WMF 5.0에 따라 달라 집니다. WMF 5.0 필요 없는 toobe, 컴퓨터 toosuccessfully hello에 대 한 자동화 DSC를 통해 hello 구성을 적용 합니다.

hello 환경에서는 다음 예제에서는 DSC 구성을 hello를 사용 합니다.

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
hello 구성 작업을 수행 합니다 hello 다음:

* hello 변수 tooget hello 암호와 toostore hello 출력 tooget가 그 hello 모바일 서비스와 hello Azure VM 에이전트에 대 한 이진을 hello hello 구성을 확인할 수 있습니다.
* hello 구성 가져옵니다 hello xPSDesiredStateConfiguration DSC 리소스를 사용할 수 있도록 `xRemoteFile` hello 리포지토리에서 toodownload hello 파일입니다.
* hello 구성 toostore hello 이진 파일의 압축을 풀려면는 디렉터리로 만들어집니다.
* hello 보관 리소스는 hello zip 폴더에서 hello 파일을 추출 합니다.
* hello 패키지 설치 리소스 hello UNIFIEDAGENT에서에서 hello 모바일 서비스를 설치 합니다. EXE installer hello 특정 인수를 사용 합니다. (hello 인수를 생성 하는 hello 변수 할 변경 toobe tooreflect 환경.)
* hello 패키지 AzureAgent 리소스에서는 Azure에서 실행 되는 모든 VM에 권장 hello Azure VM 에이전트를 설치 합니다. hello Azure VM 에이전트를 사용 가능한 tooadd 확장 toohello VM 장애 조치 후.
* hello 서비스 리소스 또는 리소스는 확인 hello 관련 모바일 서비스 및 hello Azure 서비스는 항상 실행 되어야 합니다.

으로 hello 구성을 저장 **ASRMobilityService**합니다.

> [!NOTE]
> Tooreplace hello CSIP 구성 tooreflect hello 실제 관리 서버에서를 기억 hello 에이전트 올바르게 연결 하 고 있도록 hello 올바른 암호를 사용 합니다.
>
>

## <a name="step-3-upload-tooautomation-dsc"></a>3 단계: 업로드 tooAutomation DSC
때문에 변경한 hello DSC 구성에서 필요한 DSC 리소스 모듈 (xPSDesiredStateConfiguration)을 가져옵니다, 해야 tooimport 자동화에서 해당 모듈 hello DSC 구성에 업로드 하기 전에.

자동화 계정 tooyour 로그인 너무 찾아보기**자산** > **모듈**를 클릭 하 고 **찾아보기 갤러리**합니다.

Hello 모듈에 대 한 검색할 수는 여기 tooyour 계정을 가져옵니다.

![가져오기 모듈](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

이 완료 하면 tooyour 컴퓨터 hello Azure 리소스 관리자 모듈 설치 되어 있는 이동한 다음 tooimport 새로 만든 hello DSC 구성을 계속 진행 합니다.

### <a name="import-cmdlets"></a>Cmdlet 가져오기
PowerShell에서 tooyour Azure 구독에에서 로그인 합니다. 수정 hello cmdlet tooreflect 사용자 환경 및 변수에 자동화 계정 정보를 캡처:

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

Hello 다음 cmdlet을 사용 하 여 tooAutomation DSC를 구성 하는 hello를 업로드 합니다.

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-hello-configuration-in-automation-dsc"></a>자동화 DSC에서 hello 구성 컴파일
다음으로, 해야 자동화 DSC에서 toocompile hello 구성 tooregister 노드 tooit를 시작할 수 있도록 합니다. Hello 다음 cmdlet을 실행 하 여를 수행 합니다.

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

이 작업에 hello 구성 호스팅된 toohello DSC 끌어오기 서비스를 기본적으로 배포 하는 때문에 몇 분 정도 걸릴 수 있습니다.

PowerShell (Get AzureRmAutomationDscCompilationJob)를 사용 하 여 또는 hello를 사용 하 여 hello 작업 정보를 검색할 수 hello 구성을 컴파일한 후 [Azure 포털](https://portal.azure.com/)합니다.

![작업 검색](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

이제 성공적으로 게시 및 있는 DSC 구성 tooAutomation DSC를 업로드 합니다.

## <a name="step-4-onboard-machines-tooautomation-dsc"></a>4 단계: 컴퓨터 등록 tooAutomation DSC
> [!NOTE]
> 이 시나리오를 완료 하기 위한 hello 필수 구성 요소 중 하나는 Windows 컴퓨터의 WMF hello 최신 버전으로 업데이트 됩니다. 다운로드 하 여 hello에서 플랫폼에 대 한 hello 올바른 버전을 설치 [다운로드 센터](https://www.microsoft.com/download/details.aspx?id=50395)합니다.
>
>

이제 만들게 됩니다는 metaconfig dsc tooyour 노드를 적용 합니다. 이 toosucceed, tooretrieve hello 끝점 URL과 hello 기본 키가 필요 Azure에서 선택한 자동화 계정에 대 한 합니다. 이러한 값을 찾을 수 **키** hello에 **모든 설정을** 블레이드 hello 자동화 계정에 대 한 합니다.

![키 값](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

이 예제에서는 Windows Server 2012 R2 실제 서버 Site Recovery를 사용 하 여 tooprotect 되도록 해야 합니다.

### <a name="check-for-any-pending-file-rename-operations-in-hello-registry"></a>보류 된 파일 이름 바꾸기 작업이 hello 레지스트리에 있는지 확인
Hello 자동화 DSC 끝점과 tooassociate hello 서버를 시작 하기 전에 hello 레지스트리에 파일 이름 바꾸기 작업이 보류 중인를 확인 하는 것이 좋습니다. Hello 설치 기한 마무리에서 인해은 tooa 다시 부팅 보류 중입니다.

Hello cmdlet tooverify hello 서버에서 보류 중인 재부팅 하지 않아도 있는지 다음을 실행 합니다.

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
이 빈 표시 되 면 확인 tooproceed 됩니다. 파일이 없으면 hello 서버 유지 관리 기간 동안 다시 부팅 하 여 해결 해야 합니다.

hello PowerShell 스크립팅 환경을 ISE (통합)를 시작 하 고 hello 다음 스크립트를 실행 하는 hello 서버의 tooapply hello 구성 합니다. 이 기본적으로 DSC 로컬 구성을 자동화 DSC 서비스 hello로 hello 로컬 구성 관리자 엔진 tooregister 지시 및 hello 특정 구성 (ASRMobilityService.localhost)를 검색 합니다.

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

이 구성을 자동화 dsc 로컬 구성 관리자 hello 엔진 tooregister 자체를 발생 합니다. 또한 hello 엔진 작동 방식, 수행할 경우 구성 드리프트 (ApplyAndAutoCorrect) 및 어떻게 진행 되는 것 hello 구성으로 다시 부팅 해야 하는 경우를 결정 합니다.

이 스크립트를 실행 한 후 hello 노드 자동화 dsc tooregister를 시작 해야 합니다.

![노드 등록 진행 중](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

Azure 포털 toohello 돌아가서 hello 새로 등록 된 노드에 hello 포털에서 이제 나타난 것을 볼 수 있습니다.

![Hello 포털에서 등록 된 노드](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

Hello 서버에서 다음 PowerShell 노드 hello cmdlet tooverify 제대로 등록 되었는지 hello를 실행할 수 있습니다.

```powershell
Get-DscLocalConfigurationManager
```

Hello 구성에 대 한 가져온 및 적용 된 toohello 서버를 수행한 후 hello 다음 cmdlet을 실행 하 여이 확인할 수 있습니다.

```powershell
Get-DscConfigurationStatus
```

hello 출력이 해당 hello 서버에 해당 구성을 끌어온 성공적으로 표시 됩니다.

![출력](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

또한 hello Mobility service 설치에는 자체 로그에서 찾을 수 있는 *SystemDrive*\ProgramData\ASRSetupLogs 합니다.

지금까지 이제 성공적으로 배포 및 등록 한 hello 컴퓨터에서 모바일 서비스 hello Site Recovery를 사용 하 여 tooprotect 되도록 합니다. DSC는 hello 필요한 서비스가 항상 실행 되 고 있는지 확인 합니다.

![배포 정상 완료](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

Hello 관리 서버에서 배포 된 hello를 발견 하면 후 보호를 구성할 수 있으며 사이트 복구를 사용 하 여 hello 컴퓨터에서 복제를 설정할 수 있습니다.

## <a name="use-dsc-in-disconnected-environments"></a>연결이 끊어진 환경에서 DSC 사용
컴퓨터에 연결 된 toohello 인터넷 하지 않으면 DSC toodeploy에 의존 하 고 수 있습니다 tooprotect hello 작업에서 hello 이동성 서비스를 구성 합니다.

사용자 환경에서 직접 DSC 끌어오기 서버를 인스턴스화할 수 tooessentially hello 자동화 DSC에서 얻을 수 있는 동일한 기능을 제공 합니다. 즉, 클라이언트 hello 끌어오고 hello 구성 (등록) 한 후 toohello DSC 끝점입니다. 그러나 또 다른 옵션은 로컬 또는 원격으로 toomanually 푸시 hello DSC 구성 tooyour 컴퓨터.

이 예에서 hello 컴퓨터 이름에는 추가 된 매개 변수는 참고 합니다. 이제 원하는 tooprotect hello 컴퓨터별 hello 원격 파일에 액세스할 수 있어야 하는 원격 공유에 있습니다. hello 스크립트 끝에 hello hello 구성 시행 하 고 tooapply hello DSC 구성 toohello 대상 컴퓨터를 시작 합니다.

### <a name="prerequisites"></a>필수 조건
해당 hello xPSDesiredStateConfiguration PowerShell 모듈이 설치 되어 있는지 확인 합니다. WMF 5.0이 설치 되어 있는 Windows 컴퓨터에 대 한 hello cmdlet hello 대상 컴퓨터에서 다음을 실행 하 여 hello xPSDesiredStateConfiguration 모듈을 설치할 수 있습니다.

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

또한 다운로드 하 고 toodistribute이 필요할 경우 hello 모듈을 저장할 수 것 WMF 4.0이 있는 tooWindows 컴퓨터입니다. PowerShellGet(WMF 5.0)이 설치되어 있는 컴퓨터에서는 다음 cmdlet을 실행합니다.

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

또한 WMF 4.0에 대 한 해당 hello 확인 [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) hello 컴퓨터에 설치 되어 있습니다.

hello 다음 구성을 처리할 수 있는 WMF 4.0 및 WMF 5.0 되어 tooWindows 컴퓨터:

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

자동화 DSC에서 얻을 수 있는 여 회사 네트워크 toomimic hello 기능에서 직접 DSC 끌어오기 서버 tooinstantiate 경우 참조 [DSC 웹 끌어오기 서버 설정](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396)합니다.

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a>선택 사항: Azure Resource Manager 템플릿을 사용하여 DSC 구성 배포
이 문서 DSC 구성 tooautomatically 직접 만드는 방법을 중점적 hello 모바일 서비스와 Azure VM 에이전트-hello를 배포 하 고 tooprotect 원하는 hello 컴퓨터에서 실행 중인 있는지 확인 합니다. 이 DSC 구성 tooa 새로운 또는 기존 Azure 자동화 계정을 배포 하는 Azure 리소스 관리자 템플릿을 했습니다. hello 템플릿을 환경에 대 한 hello 변수를 포함 하는 입력된 매개 변수 toocreate 자동화 자산을 사용 합니다.

Hello 서식 파일을 배포한 후에이 가이드 tooonboard toostep 4를 컴퓨터에 단순히 참조할 수 있습니다.

hello 템플릿을 처리 해 hello 다음:

1. 기존 자동화 계정을 사용하거나 새로운 계정을 만듭니다.
2. 다음에 해당하는 입력 매개 변수를 가져옵니다.
   * ASRRemoteFile-hello Mobility service 설치 프로그램을 저장 한 hello 위치
   * ASRPassphrase-hello passphrase.txt 파일을 저장 한 hello 위치
   * ASRCSEndpoint-관리 서버 hello IP 주소
3. Hello xPSDesiredStateConfiguration PowerShell 모듈을 가져옵니다
4. 만들고 hello DSC 구성을 컴파일하합니다

이전 단계는 모든 hello 컴퓨터 보호를 위해 온 보 딩을 시작할 수 있도록 hello 올바른 순서로 수행 됩니다.

배포에 대 한 지침이 포함 된 hello 서식 파일에 있는 [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC)합니다.

PowerShell을 사용 하 여 hello 템플릿을 배포 합니다.

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
Hello 이동성 서비스 에이전트를 배포한 후 다음을 할 수 있습니다 [복제 사용](site-recovery-vmware-to-azure.md) hello 가상 컴퓨터에 대 한 합니다.
