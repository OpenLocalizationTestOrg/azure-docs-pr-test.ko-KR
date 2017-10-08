---
title: "PowerShell과 함께 hello 클래식 포털의 Hyper-v Vm tooAzure aaaReplicate | Microsoft Docs"
description: "Hello 복제 hello 클래식 포털에서 사이트 복구 및 PowerShell을 사용 하 여 VMM 클라우드에 있는 Hyper-v 가상 컴퓨터의 자동화"
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: tysonn
ms.assetid: 9011f567-e0b4-4306-951a-b30da19f5db6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: d6847b46ac227209e6890de4ab603b23f827360f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-tooazure-with-powershell-in-hello-classic-portal"></a>Hello 클래식 포털에서 PowerShell로 Hyper-v Vm tooAzure 복제
> [!div class="op_single_selector"]
> * [Azure 포털](site-recovery-vmm-to-azure.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [클래식 포털](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell - 클래식](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a>개요
Azure Site Recovery는 복제, 장애 조치 및 다양 한 배포 시나리오에서에서 가상 컴퓨터의 복구를 오케스트레이션 하 여 tooyour 비즈니스 연속성 및 재해 복구 (BCDR) 전략을 적용 합니다. 배포의 전체 목록은 시나리오 참조 hello [Azure Site Recovery 개요](site-recovery-overview.md)합니다.

이 문서에서는 어떻게 toouse PowerShell tooautomate 일반적인 작업 tooperform 때 필요한 System Center VMM 클라우드에 tooAzure 저장소에서 Azure Site Recovery tooreplicate Hyper-v 가상 컴퓨터를 설정 합니다.

hello 시나리오와 hello 원본 VMM 서버에서 Azure Site Recovery Provider를 hello tooset 사이트 복구 자격 증명 모음을 설치 하는 방법을 보여 줍니다. 필수 구성 요소를 포함 하는 hello 문서, hello 서버 hello 자격 증명 모음에 등록, Azure 저장소 계정 추가, Azure hello를 설치 복구 서비스 에이전트가 Hyper-v 호스트 서버에 적용 된 tooall 보호 된 가상 컴퓨터 되며 다음 이러한 가상 컴퓨터에 대 한 보호를 사용 하도록 설정 하는 VMM 클라우드에 대 한 보호 설정을 구성 합니다. 모든 것이 예상 대로 작동 하는지 테스트 hello 장애 조치 toomake까지 완료 합니다.

이 시나리오를 설정 하는 문제를 실행 하는 경우 hello에 질문을 게시할 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

> [!NOTE]
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.
>
>

## <a name="before-you-start"></a>시작하기 전에
다음 필수 조건이 충족되었는지 확인합니다.

### <a name="azure-prerequisites"></a>Azure 필수 조건
* [Microsoft Azure](https://azure.microsoft.com/) 계정이 있어야 합니다. [평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다.
* Azure 저장소 계정 복제 toostore 데이터 필요 합니다. hello 계정에는 지역에서 복제를 사용 해야 합니다. Hello Azure Site Recovery 자격 증명 모음과 동일한 지역 hello와 관련 된 것 같은 구독 hello 합니다. [Azure 저장소에 대해 자세히 알아보세요](../storage/common/storage-introduction.md).
* Tooprotect 원하는 가상 컴퓨터 준수 하는지 toomake 해야 [Azure 가상 컴퓨터 필수 구성 요소](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)합니다.

### <a name="vmm-prerequisites"></a>VMM 필수 구성 요소
* System Center 2012 R2에서 실행되는 VMM 서버가 필요합니다.
* Hello tooprotect VMM 서버에 클라우드가 하나 이상 필요 합니다. hello 클라우드 포함 되어야 합니다.
  * 하나 이상의 VMM 호스트 그룹.
  * 각 호스트 그룹에 있는 하나 이상의 Hyper-V 호스트 서버 또는 클러스터.
  * Hello 원본 Hyper-v 서버에서 하나 이상의 가상 컴퓨터.

### <a name="hyper-v-prerequisites"></a>Hyper-V 필수 조건
* hello Hyper-v 호스트 서버 해야 이상을 실행 하 고 **Windows Server 2012** Hyper-v 역할과 또는 **Microsoft Hyper-v Server 2012** 최신 업데이트가 설치 되어 hello 있어야 하 고 있습니다.
* 클러스터에서 Hyper-V를 실행하는 경우 고정 IP 주소 기반 클러스터가 있으면 클러스터 브로커가 자동으로 만들어지지 않습니다. Tooconfigure hello 클러스터 브로커를 수동으로 필요 합니다. toodo이 서버 관리자에서 > 장애 조치 클러스터 관리자 toohello 클러스터에 연결을 클릭 **역할 구성** 선택 **Hyper-v 복제본 브로커** hello에 **역할 선택**hello 고가용성 마법사 화면입니다.
* 모든 Hyper-v 호스트 서버 또는 클러스터 toomanage 보호 하려는 VMM 클라우드에 포함 되어야 합니다.

### <a name="network-mapping-prerequisites"></a>네트워크 매핑 필수 조건
Azure 네트워크 매핑의 가상 컴퓨터를 보호 하는 경우 hello 원본 VMM 서버의 VM 네트워크와 대상 Azure 네트워크 tooenable hello 다음 간에 매핑합니다.

* 모든 컴퓨터를 장애 조치 hello에 동일한 네트워크 tooeach 기타에 복구 계획과 관계 없이 연결할 수 있습니다.
* 설치 프로그램 hello 대상 Azure 네트워크에 네트워크 게이트웨이가 사용 하는 경우 가상 컴퓨터 tooother 온-프레미스 가상 컴퓨터를 연결할 수 있습니다.
* 구성 하지 않으면 네트워크 매핑 장애 조치 hello에 동일한 가상 컴퓨터만 복구 계획 장애 조치 tooAzure 후에 다른 수 tooconnect tooeach 됩니다.

네트워크 매핑을 toodeploy 하려는 경우에 hello 다음이 필요 합니다.

* hello 원본 VMM 서버의 tooprotect 원하는 hello 가상 컴퓨터에 연결 된 tooa VM 네트워크 여야 합니다. 해당 네트워크 hello는 클라우드와 연결 된 논리 네트워크를 연결 된 tooa 이어야 합니다.
* Azure 네트워크 toowhich 복제 가상 컴퓨터는 장애 조치 후 연결할 수 있습니다. 장애 조치 hello 시간에이 네트워크를 선택 합니다. hello 네트워크 hello에 있어야 합니다. Azure Site Recovery 구독와 동일한 영역입니다.

### <a name="powershell-prerequisites"></a>PowerShell 필수 구성 요소
Azure PowerShell 준비 toogo 있는지 확인 합니다. PowerShell을 이미 사용 중인 tooupgrade tooversion 0.8.10 맞춰야 이상. PowerShell 설정 하는 방법에 대 한 정보를 참조 하십시오. [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azureps-cmdlets-docs)합니다. Hello hello 서비스에 대 한 사용 가능한 cmdlet의 모든 볼 수를 설정 하 고 PowerShell을 구성한 후 [여기](/powershell/azure/overview)합니다.

매개 변수 값, 입력 및 출력이 처리 되는 방법과 일반적으로 Azure PowerShell 같은 hello cmdlet을 사용 하는 데 도움이 되는 팁에 대 한 toolearn 참조 [Azure Cmdlet 시작](/powershell/azure/get-started-azureps)합니다.

## <a name="step-1-set-hello-subscription"></a>1 단계: hello 구독 설정
PowerShell에서 다음 cmdlet을 실행합니다.

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

특정 사용자 정보로 "< >" hello 내의 hello 요소를 대체 합니다.

## <a name="step-2-create-a-site-recovery-vault"></a>2단계: 사이트 복구 자격 증명 모음 만들기
PowerShell에서 특정 사용자 정보로 "< >" hello 내의 hello 요소 바꾼 다음이 명령을 실행:

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a>3단계: 자격 증명 모음 등록 키 생성
Hello 자격 증명 모음에 등록 키를 생성 합니다. Hello Azure Site Recovery Provider를 다운로드 하 고 hello VMM 서버에 설치 후에 hello 자격 증명 모음에이 키 tooregister hello VMM 서버를 사용 합니다.

1. Hello 자격 증명 모음 설정 파일을 가져오고 hello 컨텍스트를 설정 합니다.

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. Hello 다음 명령을 실행 하 여 hello 자격 증명 모음 컨텍스트를 설정 합니다.

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-hello-azure-site-recovery-provider"></a>4 단계: hello Azure Site Recovery Provider 설치
1. Hello VMM 컴퓨터에서 hello 다음 명령을 실행 하 여 디렉터리를 만듭니다.

   ```

   pushd C:\ASR\

   ```
2. 다운로드 한 hello 공급자를 사용 하 여 hello 다음 명령을 실행 하 여 hello 파일 추출

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. 다음 명령을 hello를 사용 하 여 hello 공급자를 설치 합니다.

   ```

   .\SetupDr.exe /i

   ```

   ```

   $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
   do
   {
     $isNotInstalled = $true;
     if(Test-Path $installationRegPath)
     {
         $isNotInstalled = $false;
     }
   }While($isNotInstalled)

   ```

   Hello 설치 toofinish 될 때까지 기다립니다.
4. Hello 서버 hello 다음 명령을 사용 하 여 hello 자격 증명 모음에 등록 합니다.

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a>5단계: Azure 저장소 계정 만들기
Azure 저장소 계정이 없으면 hello 다음 명령을 실행 하 여 지역 복제를 사용 계정을 만듭니다.

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

Hello 저장소 계정이 있어야 hello Azure Site Recovery 서비스와 동일한 지역 hello와 연결 된 동일한 구독 hello 합니다.

## <a name="step-6-install-hello-azure-recovery-services-agent"></a>6 단계: hello Azure 복구 서비스 에이전트 설치
Hello hello VMM 클라우드에 있는 각 Hyper-v 호스트 서버에 Azure 복구 서비스 에이전트 설치 hello Azure 포털에서에서 tooprotect을 할 수 있습니다.

Hello 모든 VMM 호스트에서 다음 명령을 실행 합니다.

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a>7단계: 클라우드 보호 설정 구성
1. 클라우드 보호 프로필 tooAzure hello 다음 명령을 실행 하 여 만듭니다.

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. Hello 다음 명령을 실행 하 여 보호 컨테이너를 가져옵니다.

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. Hello 클라우드와 hello 보호 컨테이너의 hello 연결을 시작 합니다.

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. Hello 작업이 완료 되 면 hello 다음 명령을 실행 합니다.

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. Hello 작업 처리를 완료 한 후에 hello 다음 명령을 실행 합니다.

        Do
        {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

        if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
        }While($isJobLeftForProcessing)



hello 작업의 toocheck hello 완료 hello 단계에 따라 [모니터 활동](#monitor)합니다.

## <a name="step-8-configure-network-mapping"></a>8단계: 네트워크 매핑 구성
시작 하기 전에 네트워크 매핑을 hello 원본 VMM 서버의 가상 컴퓨터가 연결 된 tooa VM 네트워크에 있는지 확인 합니다. 또한 Azure 가상 네트워크를 하나 이상 만듭니다. 여러 VM 네트워크에 매핑된 tooa 단일 Azure 네트워크 수 있는지 확인 합니다.

Note는 hello 대상 네트워크에 서브넷이 여러 hello에 이러한 서브넷 중 하나는 hello 원본 가상 컴퓨터는 서브넷 이름이 같은 있는 경우 hello 복제 가상 컴퓨터 장애 조치 후에 대상 서브넷 연결된 toothat 됩니다. 이름이 일치 하는 대상 서브넷 없는 경우 hello 가상 컴퓨터에 연결 된 toohello hello 네트워크의 첫 번째 서브넷 됩니다.

첫 번째 명령은 hello hello 현재 Azure Site Recovery 자격 증명 모음에 대 한 서버를 가져옵니다. hello 명령은 hello Microsoft Azure Site Recovery 서버 hello $Servers 배열 변수에 저장합니다.

    $Servers = Get-AzureSiteRecoveryServer


hello 두 번째 명령은 hello $Servers 배열의 첫 번째 서버 hello에 대 한 hello 사이트 복구 네트워크를 가져옵니다. hello 명령 hello $Networks 변수에 hello 네트워크를 저장합니다.

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

세 번째 명령은 hello hello Get-azuresubscription cmdlet을 사용 하 여 Azure 구독을 가져오고 hello $Subscriptions 변수에 해당 값을 저장 합니다.

    $Subscriptions = Get-AzureSubscription



네 번째 명령은 hello hello $AzureVmNetworks 변수에 hello Get AzureVNetSite cmdlet 및 해당 값을 사용 하 여 Azure 가상 네트워크를 가져옵니다.

    $AzureVmNetworks = Get-AzureVNetSite



hello 최종 cmdlet은 기본 네트워크 hello 및 hello Azure 가상 컴퓨터 네트워크 간의 매핑을 만듭니다. hello cmdlet $Networks의 hello 첫 번째 요소로 hello 주 네트워크를 지정합니다. hello cmdlet은 ID를 사용 하 여 hello $AzureVmNetworks의 첫 번째 요소와 가상 컴퓨터 네트워크를 지정 hello 명령은 포함 하 여 Azure 구독 id입니다.

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a>9단계: 가상 컴퓨터의 보호 활성화
서버, 클라우드 및 네트워크가 올바르게 구성 된 hello 클라우드의 가상 컴퓨터에 대 한 보호를 사용할 수 있습니다. 참고 hello 다음.

가상 컴퓨터에서 [Azure 가상 컴퓨터 필수 조건](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)을 충족해야 합니다.

tooenable 보호 hello 운영 체제 및 운영 체제 디스크 속성 hello 가상 컴퓨터에 대해 설정 되어야 합니다. 가상 컴퓨터 템플릿을 사용 하 여 VMM에서 가상 컴퓨터를 만들 때 hello 속성을 설정할 수 있습니다. Hello에 기존 가상 컴퓨터에 대 한 이러한 속성을 설정할 수도 있습니다 **일반** 및 **하드웨어 구성** hello 가상 컴퓨터 속성의 탭 합니다. VMM에서 이러한 속성을 설정 하지 않으면 수 수 tooconfigure hello Azure Site Recovery 포털에서 해당 합니다.

1. hello 명령 tooget hello 보호 컨테이너를 다음 실행 tooenable 보호:

     $ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName
2. Hello 다음 명령을 실행 하 여 hello 보호 엔터티를 (VM)를 가져옵니다.

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. Hello 다음 명령을 실행 하 여 hello VM에 대 한 DR hello 사용:

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a>배포 테스트
tootest 단일 가상 컴퓨터에 대 한 테스트 장애 조치를 실행 하거나 hello에 대 한 테스트 장애 조치를 실행 하 고 여러 가상 컴퓨터의 구성 된 복구 계획을 만들 수 있습니다 배포를 계획 합니다. 테스트 장애 조치(Failover)에서는 격리된 네트워크에서 장애 조치(Failover) 및 복구 메커니즘을 시뮬레이션합니다. 다음 사항에 유의하세요.

* Hello 장애 조치 후 원격 데스크톱을 사용 하 여 Azure에서 tooconnect toohello 가상 컴퓨터를 사용 하도록 하려는 경우는 hello 테스트 장애 조치를 실행 하기 전에 hello 가상 컴퓨터에서 원격 데스크톱 연결을 사용 합니다.
* 장애 조치 후 원격 데스크톱을 사용 하 여 Azure에서 공용 IP 주소 tooconnect toohello 가상 컴퓨터를 사용 합니다. Toodo이를 확인 하는 공용 주소를 사용 하 여 연결 tooa 가상 컴퓨터를 방해 하는 모든 도메인 정책 필요가 없습니다.

hello 작업의 toocheck hello 완료 hello 단계에 따라 [모니터 활동](#monitor)합니다.

### <a name="create-a-recovery-plan"></a>복구 계획 만들기
1. 아래의 hello 데이터를 사용 하 여 복구 계획에 대 한 템플릿으로.xml 파일을 만들고 "C:\RPTemplatePath.xml"로 저장 합니다.
2. Hello RecoveryPlan 노드 Id, 이름, PrimaryServerId, 및 SecondaryServerId 변경 합니다.
3. Hello ProtectionEntity 노드 PrimaryProtectionEntityId vmid (vmm에서)를 변경 합니다.
4. ProtectionEntity 노드를 추가하여 VM을 추가할 수 있습니다.

        <#
        <?xml version="1.0" encoding="utf-16"?>
        <RecoveryPlan Id="d0323b26-5be2-471b-addc-0a8742796610" Name="rp-test"     PrimaryServerId="9350a530-d5af-435b-9f2b-b941b5d9fcd5"     SecondaryServerId="21a9403c-6ec1-44f2-b744-b4e50b792387" Description=""     Version="V2014_07">
          <Actions />
          <ActionGroups>
            <ShutdownAllActionGroup Id="ShutdownAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </ShutdownAllActionGroup>
            <FailoverAllActionGroup Id="FailoverAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </FailoverAllActionGroup>
            <BootActionGroup Id="DefaultActionGroup">
              <PreActionSequence />
              <PostActionSequence />
              <ProtectionEntity PrimaryProtectionEntityId="d4c8ce92-a613-4c63-9b03-    cf163cc36ef8" />
            </BootActionGroup>
          </ActionGroups>
          <ActionGroupSequence>
            <ActionGroup Id="ShutdownAllActionGroup" ActionId="ShutdownAllActionGroup"     Before="FailoverAllActionGroup" />
            <ActionGroup Id="FailoverAllActionGroup" ActionId="FailoverAllActionGroup"     After="ShutdownAllActionGroup" Before="DefaultActionGroup" />
            <ActionGroup Id="DefaultActionGroup" ActionId="DefaultActionGroup" After="FailoverAllActionGroup"/>
          </ActionGroupSequence>
        </RecoveryPlan>
        #>



1. Hello hello 서식 파일에는 데이터를 입력 합니다.

        $TemplatePath = "C:\RPTemplatePath.xml";



1. Hello RecoveryPlan를 만듭니다.

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a>테스트 장애 조치(Failover) 실행
1. Hello 다음 명령을 실행 하 여 hello RecoveryPlan 개체를 가져옵니다.

     $RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;
2. Hello 다음 명령을 실행 하 여 hello 테스트 장애 조치를 시작 합니다.

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


## <a name=monitor></a> 작업 모니터
다음 명령을 toomonitor hello 활동 hello를 사용 합니다. Note toowait 사이 처리 toofinish hello에 대 한 작업을 해야 합니다.

    Do
    {
            $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
            Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
            if($job -eq $null -or $job.StateDescription -ne "Completed")
            {
                $isJobLeftForProcessing = $true;
            }

        if($isJobLeftForProcessing)
            {
                Start-Sleep -Seconds 60
            }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a>다음 단계
[자세히 알아보세요](/powershell/azure/overview) . </a>
