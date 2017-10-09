---
title: "Azure Site Recovery 및 PowerShell (리소스 관리자)를 사용 하 여 VMM 클라우드에서 aaaReplicate Hyper-v 가상 컴퓨터 | Microsoft Docs"
description: "Azure Site Recovery 및 PowerShell을 사용하여 VMM 클라우드의 Hyper-V 가상 컴퓨터 복제"
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: raynew
ms.assetid: 6ac509ad-5024-43d8-b621-d8fec019b9a9
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: b0f641de4e10a600ead415ceb9bd488fb4d1659d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-powershell-and-azure-resource-manager"></a>PowerShell 및 Azure 리소스 관리자를 사용 하 여 VMM 클라우드에 tooAzure에서 Hyper-v 가상 컴퓨터 복제
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

hello 문서에서는 hello 시나리오에 대 한 필수 구성 요소를 포함 합니다.

* 어떻게 tooset 복구 서비스 자격 증명 모음을
* 소스 VMM 서버 hello에 hello Azure Site Recovery Provider 설치
* Hello 서버 hello 자격 증명 모음에 등록, Azure 저장소 계정 추가
* Hyper-v 호스트 서버에 hello Azure 복구 서비스 에이전트 설치
* 적용 된 tooall 보호 하는 가상 컴퓨터를 VMM 클라우드에 대 한 보호 설정 구성
* 이러한 가상 컴퓨터의 보호 활성화
* Hello 장애 조치 toomake 모든 것이 예상 대로 작동 하는지 테스트 합니다.

이 시나리오를 설정 하는 문제를 실행 하는 경우 hello에 질문을 게시할 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

> [!NOTE]
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 리소스 관리자 배포 모델을 사용 하 여 설명 합니다.
>
>

## <a name="before-you-start"></a>시작하기 전에
다음 필수 조건이 충족되었는지 확인합니다.

### <a name="azure-prerequisites"></a>Azure 필수 조건
* [Microsoft Azure](https://azure.microsoft.com/) 계정이 있어야 합니다. 계정이 없는 분은 [무료 계정](https://azure.microsoft.com/free)으로 시작할 수 있습니다. Hello에 대 한 읽을 수는 또한 [Azure Site Recovery 관리자 가격](https://azure.microsoft.com/pricing/details/site-recovery/)합니다.
* Hello 복제 tooa CSP 구독 시나리오를 시도 하는 경우에 CSP 구독을 해야 합니다. Hello CSP 프로그램에 대 한 자세한 [어떻게 hello CSP 프로그램에서 tooenroll](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx)합니다.
* Azure v2 저장소 (리소스 관리자) 계정 toostore 복제 된 데이터 tooAzure 필요 합니다. hello 계정에는 지역에서 복제를 사용 해야 합니다. Hello Azure Site Recovery 서비스와 동일한 지역 hello와 hello 연관 될 것 같은 구독 또는 hello CSP 구독 합니다. Azure 저장소 설정에 대 한 더 toolearn 참조 hello [Azure 저장소 소개 tooMicrosoft](../storage/common/storage-introduction.md) 참조에 대 한 합니다.
* 가상 컴퓨터 tooprotect 원하는 hello 준수 하는지 toomake 필요 합니다 [Azure 가상 컴퓨터 필수 구성 요소](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)합니다.

> [!NOTE]
> 현재, VM 수준 작업만 Powershell을 통해 수행할 수 있습니다. 복구 계획 수준 작업에 대한 지원이 곧 제공될 것입니다.  지금은 제한 tooperforming 실패-있음만 단위는 'protected VM' 및 복구 계획 수준에서 되지 됩니다.
>
>

### <a name="vmm-prerequisites"></a>VMM 필수 구성 요소
* System Center 2012 R2에서 실행되는 VMM 서버가 필요합니다.
* 가상 컴퓨터가 포함 된 모든 VMM 서버 원하는 tooprotect hello Azure Site Recovery Provider를 실행 해야 합니다. 이 hello Azure 사이트 복구 배포 하는 동안 설치 됩니다.
* Hello tooprotect VMM 서버에 클라우드가 하나 이상 필요 합니다. hello 클라우드 포함 되어야 합니다.
  * 하나 이상의 VMM 호스트 그룹.
  * 각 호스트 그룹에 있는 하나 이상의 Hyper-V 호스트 서버 또는 클러스터
  * Hello 원본 Hyper-v 서버에서 하나 이상의 가상 컴퓨터.
* VMM 클라우드 설정에 대해 자세히 알아봅니다.
  * 사설 클라우드를 VMM에 대해 자세히 읽어보세요 [What's New in System Center 2012 R2 VMM 사설 클라우드의](http://go.microsoft.com/fwlink/?LinkId=324952) 및 [VMM 2012 및 hello 클라우드](http://go.microsoft.com/fwlink/?LinkId=324956)합니다.
  * 에 대 한 자세한 내용은 [구성 hello VMM 클라우드 패브릭](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)
  * 클라우드 패브릭 요소가 구현되면 [VMM에서 사설 클라우드 만들기](http://go.microsoft.com/fwlink/p/?LinkId=324953) 및 [연습: System Center 2012 SP1 VMM으로 사설 클라우드 만들기](http://go.microsoft.com/fwlink/p/?LinkId=324954)에 대해 알아보세요.

### <a name="hyper-v-prerequisites"></a>Hyper-V 필수 조건
* hello Hyper-v 호스트 서버 해야 이상을 실행 하 고 **Windows Server 2012** Hyper-v 역할과 또는 **Microsoft Hyper-v Server 2012** 최신 업데이트가 설치 되어 hello 있어야 하 고 있습니다.
* 클러스터에서 Hyper-V를 실행하는 경우 고정 IP 주소 기반 클러스터가 있으면 클러스터 브로커가 자동으로 만들어지지 않습니다. Tooconfigure hello 클러스터 브로커를 수동으로 필요 합니다. 자세한
* 에 대 한 참조 [어떻게 tooConfigure Hyper-v 복제본 브로커](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx)합니다.
* 모든 Hyper-v 호스트 서버 또는 클러스터 toomanage 보호 하려는 VMM 클라우드에 포함 되어야 합니다.

### <a name="network-mapping-prerequisites"></a>네트워크 매핑 필수 조건
Azure의 가상 컴퓨터를 보호 하는 경우 네트워크 매핑 hello hello hello 원본 VMM 서버와 대상 Azure 네트워크 tooenable hello 다음 가상 컴퓨터 네트워크를 매핑합니다.

* 모든 컴퓨터를 장애 조치 hello에 동일한 네트워크 tooeach 기타에 복구 계획과 관계 없이 연결할 수 있습니다.
* 설치 프로그램 hello 대상 Azure 네트워크에 네트워크 게이트웨이가 사용 하는 경우 가상 컴퓨터 tooother 온-프레미스 가상 컴퓨터를 연결할 수 있습니다.
* Hello에 장애 조치 hello 동일한 가상 컴퓨터만 네트워크 매핑을 구성 하지 않으면, 복구 계획 장애 조치 tooAzure 후에 다른 수 tooconnect tooeach 됩니다.

네트워크 매핑을 toodeploy 하려는 경우에 hello 다음이 필요 합니다.

* hello 원본 VMM 서버의 tooprotect 원하는 hello 가상 컴퓨터에 연결 된 tooa VM 네트워크 여야 합니다. 해당 네트워크 hello는 클라우드와 연결 된 논리 네트워크를 연결 된 tooa 이어야 합니다.
* Azure 네트워크 toowhich 복제 가상 컴퓨터 장애 조치 후 연결할 수 있습니다. 장애 조치 hello 시간에이 네트워크를 선택 합니다. hello 네트워크 hello에 있어야 합니다. Azure Site Recovery 구독와 동일한 영역입니다.

네트워크 매핑에 대해 자세히 알아보기

* [어떻게 tooconfigure VMM에서에서 논리 네트워크](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [어떻게 tooconfigure VM 네트워크 및 VMM에서 게이트웨이](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [어떻게 Azure에서 가상 네트워크 tooconfigure 및 모니터링](https://azure.microsoft.com/documentation/services/virtual-network/)

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
1. 또한 Azure Resource Manager에 리소스 그룹이 없는 경우 만듭니다.

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. 새 복구 서비스 자격 증명 모음을 만들고 (됩니다 나중에 사용) 변수에 ASR 자격 증명 모음 개체를 만든 hello를 저장 합니다. Hello AzureRMRecoveryServicesVault Get cmdlet을 사용 하 여 hello ASR 자격 증명 모음 개체 post 만들기를 검색할 수도 있습니다.-

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a>3 단계: hello 복구 서비스 자격 증명 모음 컨텍스트를 설정 합니다.

아래의 명령 hello를 실행 하 여 hello 자격 증명 모음 컨텍스트를 설정 합니다.

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

## <a name="step-5-create-an-azure-storage-account"></a>5단계: Azure 저장소 계정 만들기

Azure 저장소 계정이 없는 경우 지역에서 복제를 사용 계정을 만들 hello에 hello 지역 자격 증명 모음에 hello 다음 명령을 실행 하 여:

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

Hello 저장소 계정이 있어야 hello Azure Site Recovery 서비스와 동일한 지역 hello와 연결 된 동일한 구독 hello 합니다.

## <a name="step-6-install-hello-azure-recovery-services-agent"></a>6 단계: hello Azure 복구 서비스 에이전트 설치
1. hello Azure 복구 서비스 에이전트 다운로드 [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) tooprotect 있습니다 클라우드 hello VMM에에서 있는 각 Hyper-v 호스트 서버에 설치 하 고 있습니다.
2. Hello 모든 VMM 호스트에서 다음 명령을 실행 합니다.

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a>7단계: 클라우드 보호 설정 구성
1. 복제 정책 tooAzure hello 다음 명령을 실행 하 여 만듭니다.

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. Hello 다음 명령을 실행 하 여 보호 컨테이너를 가져옵니다.

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. 생성 된 hello 작업을 사용 하 고 hello 친숙 한 정책 이름에 언급 hello 정책 세부 정보 tooa 변수 가져오기:

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. Hello 복제 정책을 사용 하 여 hello 보호 컨테이너의 hello 연결을 시작 합니다.

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. Hello 작업이 완료 되 면 hello 다음 명령을 실행 합니다.

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. Hello 작업 처리를 완료 한 후에 hello 다음 명령을 실행 합니다.

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

hello 작업의 toocheck hello 완료 hello 단계에 따라 [모니터 활동](#monitor)합니다.

## <a name="step-8-configure-network-mapping"></a>8단계: 네트워크 매핑 구성
시작 하기 전에 네트워크 매핑을 hello 원본 VMM 서버의 가상 컴퓨터가 연결 된 tooa VM 네트워크에 있는지 확인 합니다. 또한 Azure 가상 네트워크를 하나 이상 만듭니다.

Toocreate a 가상 네트워크에서 Azure 리소스 관리자 및 PowerShell을 사용 하는 방법에 대 한 자세한 [Azure 리소스 관리자 및 PowerShell을 사용 하는 사이트 간 VPN 연결으로 가상 네트워크 만들기](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

Note 여러 가상 컴퓨터 네트워크는 매핑된 tooa 단일 Azure 네트워크 될 수 있습니다. Hello 대상 네트워크에 서브넷이 여러 hello에 이러한 서브넷 중 하나는 hello 원본 가상 컴퓨터는 서브넷 이름이 같은 있는 경우 hello 복제 가상 컴퓨터 장애 조치 후에 대상 서브넷 연결된 toothat 됩니다. 이름이 일치 하는 대상 서브넷 이면 hello 가상 컴퓨터 연결된 toohello hello 네트워크의 첫 번째 서브넷 됩니다.

1. 첫 번째 명령은 hello hello 현재 Azure Site Recovery 자격 증명 모음에 대 한 서버를 가져옵니다. hello 명령은 hello Microsoft Azure Site Recovery 서버 hello $Servers 배열 변수에 저장합니다.

        $Servers = Get-AzureRmSiteRecoveryServer
2. hello 두 번째 명령은 hello $Servers 배열의 첫 번째 서버 hello에 대 한 hello 사이트 복구 네트워크를 가져옵니다. hello 명령 hello $Networks 변수에 hello 네트워크를 저장합니다.

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. 세 번째 명령은 hello hello $AzureVmNetworks 변수에 Azure 가상 네트워크 및 해당 값을 가져옵니다.

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. hello 최종 cmdlet은 기본 네트워크 hello 및 hello Azure 가상 컴퓨터 네트워크 간의 매핑을 만듭니다. hello cmdlet $Networks의 hello 첫 번째 요소로 hello 주 네트워크를 지정합니다. hello cmdlet hello $AzureVmNetworks의 첫 번째 요소와 가상 컴퓨터 네트워크를 지정합니다.

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a>9단계: 가상 컴퓨터의 보호 활성화
Hello 서버, 클라우드 및 네트워크가 올바르게 구성 된 hello 클라우드의 가상 컴퓨터에 대 한 보호를 사용할 수 있습니다.

 참고 hello 다음.

* 가상 컴퓨터는 Azure 요구 사항을 충족해야 합니다. 이러한 체크 인 [필수 구성 요소 및 지원](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) hello 계획 가이드에서입니다.
* tooenable 보호, hello 운영 체제 및 운영 체제 디스크 속성 hello 가상 컴퓨터에 대해 설정 되어야 합니다. 가상 컴퓨터 템플릿을 사용 하 여 VMM에서 가상 컴퓨터를 만들 때 hello 속성을 설정할 수 있습니다. Hello에 기존 가상 컴퓨터에 대 한 이러한 속성을 설정할 수도 있습니다 **일반** 및 **하드웨어 구성** hello 가상 컴퓨터 속성의 탭 합니다. VMM에서 이러한 속성을 설정 하지 않으면 수 수 tooconfigure hello Azure Site Recovery 포털에서 해당 합니다.

1. hello 명령 tooget hello 보호 컨테이너를 다음 실행 tooenable 보호:

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. Hello 다음 명령을 실행 하 여 hello 보호 엔터티를 (VM)를 가져옵니다.

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. Hello 다음 명령을 실행 하 여 hello VM에 대 한 DR hello 사용:

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a>배포 테스트
tootest 배포 테스트를 실행할 수는 단일 가상 컴퓨터에 대 한 장애 조치 또는 여러 가상 컴퓨터의 구성 된 복구 계획을 만들고 실행 hello 계획에 대 한 테스트 장애 조치 합니다. 테스트 장애 조치(Failover)에서는 격리된 네트워크에서 장애 조치(Failover) 및 복구 메커니즘을 시뮬레이션합니다. 다음 사항에 유의하세요.

* Hello 장애 조치 후 원격 데스크톱을 사용 하 여 Azure에서 tooconnect toohello 가상 컴퓨터를 원하는 경우는 hello 테스트 장애 조치를 실행 하기 전에 hello 가상 컴퓨터에서 원격 데스크톱 연결을 사용 합니다.
* 장애 조치 후 원격 데스크톱을 사용 하 여 Azure에서 공용 IP 주소 tooconnect toohello 가상 컴퓨터를 사용 합니다. Toodo이를 확인 하는 공용 주소를 사용 하 여 연결 tooa 가상 컴퓨터를 방해 하는 모든 도메인 정책 필요가 없습니다.

hello 작업의 toocheck hello 완료 hello 단계에 따라 [모니터 활동](#monitor)합니다.

### <a name="run-a-test-failover"></a>테스트 장애 조치(Failover) 실행
- Hello 다음 명령을 실행 하 여 hello 테스트 장애 조치를 시작 합니다.

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a>계획된 장애 조치(Failover) 실행
- Hello 다음 명령을 실행 하 여 hello 계획 된 장애 조치를 시작 합니다.

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a>계획되지 않은 장애 조치 실행
- 시작 계획 되지 않은 장애 조치 hello 다음 명령을 실행 하 여 hello:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

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
