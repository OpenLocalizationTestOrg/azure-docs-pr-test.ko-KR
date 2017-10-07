---
title: "PowerShell (Azure 리소스 관리자)과 함께 VMM tooa 보조 사이트의 Hyper-v Vm aaaReplicate | Microsoft Docs"
description: "Toodeploy Azure Site Recovery tooorchestrate 복제, 장애 조치 및 복구 VMM에서 Hyper-v Vm의 클라우드 tooa PowerShell (리소스 관리자)을 사용 하는 보조 VMM 사이트를 어떻게 설명"
services: site-recovery
documentationcenter: 
author: sujaytalasila
manager: rochakm
editor: raynew
ms.assetid: 9d38e9c3-217c-4e44-830c-575e9a4141f2
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: a769dcc68d66c18b9dc47539071f4d0e0f1db70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-powershell-resource-manager"></a>VMM 클라우드 tooa 보조 VMM 사이트에서 PowerShell (리소스 관리자)를 사용 하 여 Hyper-v 가상 컴퓨터 복제
> [!div class="op_single_selector"]
> * [Azure 포털](site-recovery-vmm-to-vmm.md)
> * [클래식 포털](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

TooAzure 사이트 복구를 시작! Tooreplicate 온-프레미스 System Center Virtual Machine Manager (VMM) 클라우드 tooa 보조 사이트의 관리 되는 Hyper-v 가상 컴퓨터를 원하는 경우이 문서를 사용 합니다.

이 문서에서는 어떻게 toouse PowerShell tooautomate 일반적인 작업 tooperform 때 필요한 보조 사이트에서 System Center VMM 클라우드에 tooSystem 센터 VMM 클라우드의 Azure Site Recovery tooreplicate Hyper-v 가상 컴퓨터를 설정 합니다.

hello 문서에서는 hello 시나리오에 대 한 필수 구성 요소를 포함 합니다.

* 어떻게 tooset 복구 서비스 자격 증명 모음을
* Hello 원본 VMM 서버와 대상 VMM 서버 hello에 hello Azure Site Recovery Provider를 설치 합니다.
* VMM 서버 hello hello 자격 증명 모음 등록
* VMM 클라우드 hello에 대 한 복제 정책을 구성 합니다. hello 복제 설정을 hello 정책에 적용 된 tooall 보호 된 가상 컴퓨터 수 있습니다.
* Hello 가상 컴퓨터에 대 한 보호를 사용 하도록 설정 합니다.
* 개별적으로 또는 복구의 일부로 Vm의 테스트 hello 장애 조치 계획 toomake 모든 기능이 예상 대로 작동 하는지 확인 합니다.
* 개별적으로 또는 모든 기능이 예상 대로 작동 하는지 확인 하는 복구 계획 toomake의 일환으로 계획 된 또는 Vm의 경우 계획 되지 않은 장애 조치를 수행 합니다.

이 시나리오를 설정 하는 문제를 실행 하는 경우 hello에 질문을 게시할 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

> [!NOTE]
> Azure에는 리소스를 만들고 작업하기 위한 두 가지 [배포 모델](../azure-resource-manager/resource-manager-deployment-model.md) 인 Azure Resource Manager 모델과 클래식 모델이 있습니다. Azure는 두 개의 포털 – hello 클래식 배포 모델을 지 원하는 Azure 클래식 포털 hello 및 두 가지 경우 모두 지원 하 여 Azure 포털 hello에 있습니다. 이 문서에서는 hello 리소스 관리자 배포 모델에 설명 합니다.
>
>

## <a name="on-premises-prerequisites"></a>온-프레미스 필수 조건
필요한 사항 hello에서 기본 및 보조 온-프레미스 사이트 toodeploy이이 시나리오:

| **필수 구성 요소** | **세부 정보** |
| --- | --- |
| **VMM** |Hello 기본 사이트에서 VMM 서버와 보조 사이트 hello에에서 VMM 서버를 배포 하는 것이 좋습니다.<br/><br/> [단일 VMM 서버의 클라우드 간에 복제](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment)에 문의 사항을 게시하세요. toodo이 해야 hello VMM 서버에 구성 된 둘 이상의 클라우드가 있습니다.<br/><br/> VMM 서버를 하나 이상 실행 해야 hello 최신 업데이트로 System Center 2012 SP1.<br/><br/> 각 VMM 서버 하나에 있어야 하거나 추가 클라우드를 구성 하 고 모든 클라우드 hello Hyper-v 용량 프로필이 설정 되어 있어야 합니다. <br/><br/>클라우드에 하나 이상의 VMM 호스트 그룹이 있어야 합니다.<br/><br/>VMM 클라우드를 설정 하는 방법에 대 한 자세한 정보 [구성 hello VMM 클라우드 패브릭](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), 및 [연습: System Center 2012 SP1 vmm 사설 클라우드를 만들어](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx)합니다.<br/><br/> VMM 서버는 인터넷에 연결되어야 합니다. |
| **Hyper-V** |Hyper-v 서버가 이상 실행 해야 hello Hyper-v 역할과 Windows Server 2012 및 최신 업데이트가 설치 되어 hello 있어야 합니다.<br/><br/> Hyper-V 서버에 VM이 하나 이상 있어야 합니다.<br/><br/>  Hyper-v 호스트 서버 hello 기본 및 보조 VMM 클라우드에 호스트 그룹에 들어 있어야 합니다.<br/><br/> Windows Server 2012 R2의 클러스터에서 Hyper-V를 실행하는 경우 [업데이트 2961977](https://support.microsoft.com/kb/2961977)을 설치해야 합니다.<br/><br/> Windows Server 2012의 클러스터에서 Hyper-V를 실행하는 경우 고정 IP 주소 기반 클러스터가 있으면 클러스터 브로커가 자동으로 만들어지지 않습니다. Tooconfigure hello 클러스터 브로커를 수동으로 필요 합니다. [자세히 알아보기](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx). |
| **공급자** |사이트 복구 배포 하는 동안 VMM 서버에 hello Azure Site Recovery Provider를 설치 합니다. hello 공급자 HTTPS 443 tooorchestrate 복제 통해 Site Recovery와 통신합니다. 데이터 복제 hello LAN 통해 hello 기본 및 보조 Hyper-v 서버 또는 VPN 연결 간에 발생합니다.<br/><br/> hello hello VMM 서버에서 실행 중인 공급자 필요한 액세스 toothese Url: *. hypervrecoverymanager.windowsazure.com; *. accesscontrol.windows.net; *. backup.windowsazure.com; *. blob.core.windows.net; *. store.core.windows.net 합니다.<br/><br/> 또한 VMM 서버 toohello hello에서에서 방화벽 통신을 허용 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653) hello HTTPS (443) 프로토콜을 허용 하 고 있습니다. |

### <a name="network-mapping-prerequisites"></a>네트워크 매핑 필수 조건
네트워크 매핑은 hello 기본 및 보조 VMM 서버를 VMM VM 네트워크 간에 매핑됩니다.

* 장애 조치(Failover) 후 보조 Hyper-V 호스트에 복제본 VM을 최적으로 배치합니다.
* 복제본 Vm tooappropriate VM 네트워크를 연결 합니다.
* 네트워크를 구성 하지 않으면 매핑 복제본 Vm 수 없습니다 연결된 tooany 네트워크 장애 조치 후.
* 네트워크를 tooset 하려는 경우 사이트 복구 시 매핑 배포 여기는 필요 합니다.

  * Hello 원본 Hyper-v 호스트 서버에 있는 Vm 연결된 tooa VMM VM 네트워크 인지 확인 합니다. 해당 네트워크 hello는 클라우드와 연결 된 논리 네트워크를 연결 된 tooa 이어야 합니다.
  * 복구에 사용할 보조 클라우드를 hello 구성 해당 VM 네트워크에 있는지 확인 합니다. 해당 VM 네트워크에 연결 된 tooa hello 보조 클라우드와 연결 된 논리 네트워크 여야 합니다.

Hello 문서 아래에서 VMM 네트워크를 구성 하는 방법에 대 한 자세한 정보

* [어떻게 tooconfigure VMM에서에서 논리 네트워크](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [어떻게 tooconfigure VM 네트워크 및 VMM에서 게이트웨이](http://go.microsoft.com/fwlink/p/?LinkId=386308)

[알아보세요](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) .

### <a name="powershell-prerequisites"></a>PowerShell 필수 구성 요소
Azure PowerShell 준비 toogo 있는지 확인 합니다. PowerShell을 이미 사용 중인 tooupgrade tooversion 0.8.10 맞춰야 이상. PowerShell 설정에 대 한 정보를 참조 hello [tooinstall 안내 하 고 Azure powershell](/powershell/azureps-cmdlets-docs)합니다. Hello hello 서비스에 대 한 사용 가능한 cmdlet의 모든 볼 수를 설정 하 고 PowerShell을 구성한 후 [여기](/powershell/azure/overview)합니다.

매개 변수 값, 입력 및 출력이 처리 되는 방법과 일반적으로 Azure PowerShell 같은 hello cmdlet을 사용 하는 데 도움이 되는 팁에 대 한 toolearn 참조 hello [tooget Azure cmdlet 시작 안내](/powershell/azure/get-started-azureps)합니다.

## <a name="step-1-set-hello-subscription"></a>1 단계: hello 구독 설정
1. Azure powershell, 로그인 tooyour Azure 계정에서에서: hello 다음 cmdlet을 사용 하 여

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. 구독 목록을 가져옵니다. 이 또한은 나열 hello subscriptionIDs 각 hello 구독에 대 한 합니다. Hello 구독의 toocreate hello 복구 서비스 자격 증명 모음 원하는 hello subscriptionID 다운 note    

        Get-AzureRmSubscription
3. hello에 복구 서비스 자격 증명 모음이 toobe hello 구독 ID를 언급 하 여 만든 hello 구독 설정

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a>2단계: 복구 서비스 자격 증명 모음 만들기
1. 또한 Azure Resource Manager 리소스 그룹이 없는 경우 만듭니다.

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. 새 복구 서비스 자격 증명 모음을 만들고 (됩니다 나중에 사용) 변수에 ASR 자격 증명 모음 개체를 만든 hello를 저장 합니다. Hello AzureRMRecoveryServicesVault Get cmdlet을 사용 하 여 hello ASR 자격 증명 모음 개체 post 만들기를 검색할 수도 있습니다.-

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a>3 단계: hello 복구 서비스 자격 증명 모음 컨텍스트를 설정 합니다.
1. 자격 증명 모음은 이미 만든 경우 명령 tooget hello 자격 증명 모음 아래 hello을 실행 합니다.

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. 아래의 명령 hello를 실행 하 여 hello 자격 증명 모음 컨텍스트를 설정 합니다.

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a>4 단계: hello Azure Site Recovery Provider 설치
1. Hello VMM 컴퓨터에서 hello 다음 명령을 실행 하 여 디렉터리를 만듭니다.

       New-Item c:\ASR -type directory
2. 다운로드 한 hello 공급자를 사용 하 여 hello 다음 명령을 실행 하 여 hello 파일 추출

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. 다음 명령을 hello를 사용 하 여 hello 공급자를 설치 합니다.

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   Hello 설치 toofinish 될 때까지 기다립니다.
4. Hello 서버 hello 다음 명령을 사용 하 여 hello 자격 증명 모음에 등록 합니다.

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a>5단계: 복제 정책 만들기 및 연결
1. Hyper-v 2012 R2 복제 정책을 hello 다음 명령을 실행 하 여 만듭니다.

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify hello number of hours tooretain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify hello frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify hello port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > VMM 클라우드 hello에 다른 버전의 Windows Server (했 듯이 hello Hyper-v 필수 구성 요소)를 실행 하는 Hyper-v 호스트 포함 될 수 있지만 hello 복제 정책 특정 OS 버전입니다. 운영 체제 버전마다 다른 호스트가 실행되고 있는 경우 각 형식의 OS 버전에 대해 별도의 복제 정책을 만듭니다. 예를 들어 Windows Server 2012에서 5개의 호스트가 실행되고 있고 Windows Server 2012 R2에서 3개의 호스트가 실행되고 있는 경우 각 운영 체제 버전 형식에 대해 하나씩 2개의 복제 정책을 만듭니다.

1. Hello 다음 명령을 실행 하 여 hello 주 보호 컨테이너 (기본 VMM 클라우드) 및 복구 보호 컨테이너 (복구 VMM 클라우드)를 가져옵니다.

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. 사용 하 여 1 단계에서 만든 hello 정책을 검색 하는 hello 정책의 hello 이름

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. Hello 복제 정책을 사용 하 여 hello 보호 컨테이너 (VMM 클라우드)의 hello 연결을 시작 합니다.

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. Hello 정책 연결 작업 toocomplete 될 때까지 기다립니다. 다음 PowerShell 코드 조각을 hello를 사용 하 여 hello 작업이 완료 된 경우를 확인할 수 있습니다.

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   Hello 작업 처리를 완료 한 후에 hello 다음 명령을 실행 합니다.

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

hello 작업의 toocheck hello 완료 hello 단계에 따라 [모니터 활동](#monitor)합니다.

## <a name="step-6-configure-network-mapping"></a>6단계: 네트워크 매핑 구성
1. 첫 번째 명령은 hello hello 현재 Azure Site Recovery 자격 증명 모음에 대 한 서버를 가져옵니다. hello 명령은 hello Microsoft Azure Site Recovery 서버 hello $Servers 배열 변수에 저장합니다.

        $Servers = Get-AzureRmSiteRecoveryServer
2. 아래 명령 hello hello 원본 VMM 서버와 대상 VMM 서버 hello에 대 한 hello 사이트 복구 네트워크를 가져옵니다.

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > 첫 번째 또는 두 번째에 한 hello 서버 배열 hello hello 원본 VMM 서버를 hello 수 있습니다. Hello hello VMM 서버 이름을 확인 하 고 hello 네트워크를 적절 하 게 가져올


1. hello 최종 cmdlet은 기본 네트워크 hello와 hello 복구 네트워크 간의 매핑을 만듭니다. hello cmdlet $RecoveryNetworks의 hello 첫 번째 요소로 $PrimaryNetworks 및 hello 복구 네트워크의 hello 첫 번째 요소로 hello 주 네트워크를 지정합니다.

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a>7단계: 저장소 매핑 구성
1. 아래의 명령 hello hello 목록이 $storageclassifications 변수로 저장소 분류를 가져옵니다.

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. 명령 아래 hello $SourceClassificaion 변수로 hello 소스 분류 및 대상 분류 $TargetClassification 변수로 가져옵니다.

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > hello 원본 및 대상 분류 hello 배열에 있는 모든 요소를 수 있습니다. Toohello 출력의 hello $storageclassifications 배열에 있는 원본 및 대상 분류의 명령 toofigure hello 인덱스 아래를 참조 하십시오.

    > Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table


1. hello cmdlet 아래에 hello 소스 분류 및 hello 대상 분류 간에 매핑을 만듭니다.

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a>8단계: 가상 컴퓨터의 보호 활성화
Hello 서버, 클라우드 및 네트워크가 올바르게 구성 된 hello 클라우드의 가상 컴퓨터에 대 한 보호를 사용할 수 있습니다.

1. hello 명령 tooget hello 보호 컨테이너를 다음 실행 tooenable 보호:

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. Hello 다음 명령을 실행 하 여 hello 보호 엔터티를 (VM)를 가져옵니다.

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. Hello 다음 명령을 실행 하 여 hello VM에 대 한 복제를 사용 합니다.

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a>배포 테스트
tootest 단일 가상 컴퓨터에 대 한 테스트 장애 조치를 실행 하거나 hello에 대 한 테스트 장애 조치를 실행 하 고 여러 가상 컴퓨터의 구성 된 복구 계획을 만들 수 있습니다 배포를 계획 합니다. 테스트 장애 조치(Failover)에서는 격리된 네트워크에서 장애 조치(Failover) 및 복구 메커니즘을 시뮬레이션합니다.

> [!NOTE]
> Azure 포털에서 응용 프로그램에 대한 복구 계획을 만들 수 있습니다.
>
>

hello 작업의 toocheck hello 완료 hello 단계에 따라 [모니터 활동](#monitor)합니다.

### <a name="run-a-test-failover"></a>테스트 장애 조치(Failover) 실행
1. Hello cmdlet tooget hello VM 네트워크 toowhich Vm을 tootest 장애 조치 하려면 아래를 실행 합니다.

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. Hello 다음을 수행 하 여 VM의 테스트 장애 조치를 수행 합니다.

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. Hello 다음을 수행 하 여 복구 계획의 테스트 장애 조치를 수행 합니다.

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a>계획된 장애 조치(Failover) 실행
1. Hello 다음을 수행 하 여 VM의 계획된 된 장애 조치를 수행 합니다.

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. Hello 다음을 수행 하 여 복구 계획의 계획된 된 장애 조치를 수행 합니다.

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a>계획되지 않은 장애 조치 실행
1. Hello 다음을 수행 하 여 VM의 경우 계획 되지 않은 장애 조치를 수행 합니다.

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

2. hello 다음을 수행 하 여 복구 계획의 계획 되지 않은 경우 장애 조치를 수행 합니다.

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

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
[자세히 알아보세요](/powershell/module/azurerm.recoveryservices.backup/#recovery) .
