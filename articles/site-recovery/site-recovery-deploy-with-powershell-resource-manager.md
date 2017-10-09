---
title: "PowerShell 및 Azure 리소스 관리자 사용 하 여 Hyper-v Vm aaaReplicate | Microsoft Docs"
description: "PowerShell 및 Azure 리소스 관리자를 사용 하 여 Azure 사이트 복구와 Hyper-v Vm tooAzure의 hello 복제를 자동화 합니다."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: 
ms.assetid: 05e0d76e-c3f5-4845-8052-094019b6d102
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: 4fb15ce2e9ad54f1dd6f54ff769eb912aa4b0272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a>PowerShell 및 Azure Resource Manager를 사용하여 온-프레미스 Hyper-V 가상 컴퓨터와 Azure 간 복제
> [!div class="op_single_selector"]
> * [Azure 포털](site-recovery-hyper-v-site-to-azure.md)
> * [PowerShell - Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
> * [클래식 포털](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a>개요
Azure Site Recovery는 복제, 장애 조치 및 다양 한 배포 시나리오에서에서 가상 컴퓨터의 복구를 오케스트레이션 하 여 tooyour 비즈니스 연속성 및 재해 복구 전략을 적용 합니다. 배포 시나리오의 전체 목록을 보려면 hello [Azure Site Recovery 개요](site-recovery-overview.md)합니다.

Azure PowerShell은 cmdlet toomanage Windows PowerShell을 통해 Azure를 제공 하는 모듈입니다. 두 가지 유형의 모듈에서 작동할 수: hello Azure 프로필 모듈 또는 hello Azure 리소스 관리자 모듈입니다.

Azure Resource Manager에 대한 Azure PowerShell과 함께 사용할 수 있는 사이트 복구 PowerShell cmdlet을 사용하여 Azure에서 서버를 보호하고 복구할 수 있습니다.

이 문서에서는 설명 방법을 toouse Windows PowerShell과 함께 Azure 리소스 관리자, toodeploy 사이트 복구 tooconfigure 고 서버 보호 tooAzure를 조정 합니다. 이 문서에서 사용 하는 hello 예제 tooprotect, 장애 조치 하 고 Azure 리소스 관리자와 Azure PowerShell을 사용 하 여 Hyper-v 호스트 tooAzure에 가상 컴퓨터를 복구 하는 방법을 보여줍니다.

> [!NOTE]
> hello 사이트 복구 PowerShell cmdlet 현재를 사용 하면 다음 tooconfigure hello: 하나의 가상 컴퓨터 관리자 사이트 tooanother, 가상 컴퓨터 관리자 사이트 tooAzure 및 Hyper-v 사이트 tooAzure 합니다.
>
>

Toounderstand hello 등의 기본 개념, 모듈, cmdlet 및 세션 필요는 없지만이 문서에서는 PowerShell 전문가 toouse toobe 필요 하지 않습니다. Windows PowerShell에 대한 자세한 내용은 [Windows PowerShell 시작](http://technet.microsoft.com/library/hh857337.aspx)(영문)을 참조하십시오.

자세한 내용은 [Azure Resource Manager에서 Azure PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.

> [!NOTE]
> Hello 클라우드 솔루션 공급자 (CSP) 프로그램의 일부인 Microsoft 파트너를 구성 하 고 해당 고객의 서버에 대 한 보호를 관리할 수 tootheir 고객의 각 CSP 구독 (테 넌 트 구독의 경우).
>
>

## <a name="before-you-start"></a>시작하기 전에
다음 필수 조건이 충족되었는지 확인합니다.

* [Microsoft Azure](https://azure.microsoft.com/) 계정. [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다. [Azure Site Recovery Manager 가격](https://azure.microsoft.com/pricing/details/site-recovery/)에 대해 알아볼 수도 있습니다.
* Azure PowerShell 1.0 이 릴리스에 대 한 내용은 방법과 tooinstall, 참조 [Azure PowerShell 1.0.](https://azure.microsoft.com/)
* hello [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) 및 [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) 모듈입니다. Hello에서 hello 이러한 모듈의 최신 버전을 얻을 수 있습니다 [PowerShell 갤러리](https://www.powershellgallery.com/)

이 문서에서는 설명 방법을 tooconfigure Azure 리소스 관리자와 Azure Powershell toouse 및 서버 보호를 관리 합니다. 이 문서에서 사용 하는 hello 예제 방법을 보여주는 tooprotect tooAzure Hyper-v 호스트에서 실행 되는 가상 컴퓨터. hello 다음 필수 구성 요소는 특정 toothis 예제입니다. Hello에 대 한 요구 사항 보다 포괄적인 집합에 대 한 다양 한 사이트 복구 시나리오 toothat 시나리오와 관련 된 toohello 설명서를 참조 하십시오.

* 하나 이상의 가상 컴퓨터가 포함된 Windows Server 2012 R2 또는 Microsoft Hyper-V Server 2012 R2를 실행하는 Hyper-V 호스트.
* 직접 또는 프록시를 통해 toohello 인터넷에 연결 하는 Hyper-v 서버.
* hello tooprotect 원하는 가상 컴퓨터에 맞아야 합니다 [가상 컴퓨터 필수 구성 요소](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)합니다.

## <a name="step-1-sign-in-tooyour-azure-account"></a>1 단계: tooyour Azure 계정에 로그인
1. PowerShell 콘솔을 열고이 명령 toosign tooyour Azure 계정에서에서 실행 합니다. hello cmdlet 계정 자격 증명을 요청 하는 웹 페이지를 엽니다.

        Login-AzureRmAccount

    매개 변수 toohello로 계정 자격 증명도 포함 될 수 또는 `Login-AzureRmAccount` hello를 사용 하 여 cmdlet `-Credential` 매개 변수입니다.

    CSP 파트너 테 넌 트를 대신 하 여 작업 인 경우에 tenantID 또는 테 넌 트 주 도메인 이름을 사용 하 여 hello 고객 테 넌 트로 지정 합니다.

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. 한 계정 hello 계정과 toouse hello 구독을 연결 해야 하므로 여러 구독 있을 수 있습니다.

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. 구독 등록된 toouse 인지 확인 hello 다음 명령을 사용 하 여 복구 서비스 및 사이트 복구를 위한 Azure 공급자 hello:

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   경우 hello 이러한 명령의 출력 hello에에서 **RegistrationState** 너무 설정**등록 된**, tooStep 2를 진행할 수 있습니다. 그렇지 않으면 구독에서 hello 누락 된 공급자를 등록 해야 합니다.

   tooregister hello Azure 사이트 복구 및 hello 다음 명령을 실행 하는 복구 서비스 공급자:

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   Hello 공급자 hello 다음 명령을 사용 하 여 성공적으로 등록 되었는지 확인: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` 및 `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`합니다.

## <a name="step-2-set-up-hello-recovery-services-vault"></a>2 단계: hello 복구 서비스 자격 증명 모음 설정
1. 합니다 hello 자격 증명 모음을 만들거나 기존 리소스 그룹을 사용 하 여 Azure 리소스 관리자 리소스 그룹을 만듭니다. 다음 명령을 hello를 사용 하 여 새 리소스 그룹을 만들 수 있습니다.

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    hello $ResourceGroupName 변수에 포함 hello 리소스 그룹의 이름을 hello toocreate, 원하는 hello $Geo 변수에 포함 hello Azure toocreate hello 리소스 그룹 (예: "브라질 남쪽")의 영역입니다.

    Hello를 사용 하 여 구독에서 리소스 그룹의 목록을 가져올 수 있습니다 `Get-AzureRmResourceGroup` cmdlet.
2. 다음과 같이 새 Azure 복구 서비스 자격 증명 모음을 만듭니다.

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    Hello를 사용 하 여 기존 자격 증명 모음 목록을 검색할 수 있습니다 `Get-AzureRmRecoveryServicesVault` cmdlet.

> [!NOTE]
> Hello를 사용 하 여 이러한 자격 증명 모음 목록을 검색 하 고 hello 클래식 포털 또는 hello Azure 서비스 관리 PowerShell 모듈을 사용 하 여 만든 사이트 복구 자격 증명에서 tooperform 작업 하려는 경우 `Get-AzureRmSiteRecoveryVault` cmdlet. 모든 새 작업에 대해 새 복구 서비스 자격 증명 모음을 만들어야 합니다. 앞서 만든 hello 사이트 복구 자격 증명 지원 되기는 하지만 hello 최신 기능에 없는 합니다.
>
>

## <a name="step-3-set-hello-recovery-services-vault-context"></a>3 단계: hello 복구 서비스 자격 증명 모음 컨텍스트 설정
1. Hello 다음 명령을 실행 하 여 hello 자격 증명 모음 컨텍스트를 설정 합니다.

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-hello-site"></a>4 단계: Hyper-v 사이트를 만들고 hello 사이트에 대 한 새 자격 증명 모음 등록 키를 생성 합니다.
1. 다음과 같이 새 Hyper-V 사이트를 만듭니다.

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    이 cmdlet은 사이트 복구 작업 toocreate hello 사이트를 시작 하 고 사이트 복구 작업 개체를 반환 합니다. Hello 작업 toocomplete 기다렸다가 hello 작업이 완료 되었는지 확인 합니다.

    Hello 작업 개체를 검색할 수 있으며 hello AzureRmSiteRecoveryJob Get cmdlet을 사용 하 여 hello hello 작업의 현재 상태를 확인 함으로써 수 있습니다.
2. 생성 하 고 다음과 같이 hello 사이트에 대 한 등록 키를 다운로드 합니다.

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    복사 hello 키 toohello Hyper-v 호스트를 다운로드 합니다. Hello 키 tooregister hello Hyper-v 호스트 toohello 사이트가 필요합니다.

## <a name="step-5-install-hello-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a>5 단계: Hyper-v 호스트에 hello Azure Site Recovery provider 및 Azure 복구 서비스 에이전트 설치
1. Hello hello 공급자의 최신 버전에 대 한 hello 설치 관리자 다운로드 [Microsoft](https://aka.ms/downloaddra)합니다.
2. Hello 설치 hello 종료 및 Hyper-v 호스트에서 실행된 hello installer toohello 등록 단계를 계속 합니다.
3. 메시지가 표시 되 면 hello hello Hyper-v 호스트 toohello 사이트의 등록을 완료 하 고 사이트 등록 키 다운로드를 제공 합니다.
4. 해당 hello Hyper-v 호스트 hello 다음 명령을 사용 하 여 등록 된 toohello 사이트는 확인 합니다.

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-hello-protection-container"></a>6 단계: 복제 정책을 만들고 hello 보호 컨테이너와 연결
1. 다음과 같이 복제 정책을 만듭니다.

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    검사 hello hello 복제 정책 만들기가 성공 하면 작업이 tooensure를 반환 합니다.

   > [!IMPORTANT]
   > hello 저장소 계정을 지정 해야에 복구 서비스 자격 증명 모음과 동일한 Azure 지역 hello 및 지역에서 복제를 사용 해야 합니다.
   >
   > * 저장소 계정 유형이 Azure 저장소 (기본)이 복구를 지정 하는 hello hello의 장애 조치 컴퓨터 복구 hello 컴퓨터 tooAzure IaaS (클래식)를 보호 합니다.
   > * 복구 저장소 계정 유형이 Azure 저장소 (Azure 리소스 관리자)이 지정 하는 hello, hello의 장애 조치 컴퓨터 복구 hello 컴퓨터 tooAzure IaaS (Azure 리소스 관리자)를 보호 합니다.
   >
   >
2. 다음과 같이 hello 보호 컨테이너 해당 toohello 사이트, 가져오기:

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. 다음과 같이 hello 복제 정책을 사용 하 여 hello 보호 컨테이너의 hello 연결을 시작 합니다.

     $Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer

   Hello 연관 작업 toocomplete 기다렸다가 성공적으로 완료 되었는지 확인 하십시오.

## <a name="step-7-enable-protection-for-virtual-machines"></a>7단계: 가상 컴퓨터의 보호 활성화
1. Hello 보호 엔터티 해당 toohello tooprotect를 다음과 같이 원하는 VM 가져오기:

        $VMFriendlyName = "Fabrikam-app"                    #Name of hello VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. 다음과 같이 hello 가상 컴퓨터 보호를 시작 합니다.

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > hello 저장소 계정을 지정 해야에 복구 서비스 자격 증명 모음과 동일한 Azure 지역 hello 및 지역에서 복제를 사용 해야 합니다.
   >
   > * 저장소 계정 유형이 Azure 저장소 (기본)이 복구를 지정 하는 hello hello의 장애 조치 컴퓨터 복구 hello 컴퓨터 tooAzure IaaS (클래식)를 보호 합니다.
   > * 복구 저장소 계정 유형이 Azure 저장소 (Azure 리소스 관리자)이 지정 하는 hello, hello의 장애 조치 컴퓨터 복구 hello 컴퓨터 tooAzure IaaS (Azure 리소스 관리자)를 보호 합니다.
   >
   > VM을 보호 하는 hello에 둘 이상의 연결 된 tooit 디스크로 hello를 사용 하 여 hello 운영 체제 디스크를 지정 하는 경우 *OSDiskName* 매개 변수입니다.
   >
   >
3. Hello 초기 복제 후 보호 되는 상태로 가상 컴퓨터 tooreach hello에 대 한 대기 합니다. 이렇게 복제 데이터 toobe hello 양 등의 요인에 따라 시간이 오래 걸릴 하 고 사용 가능한 업스트림 대역폭 tooAzure hello. hello 작업 상태 및 StateDescription hello 보호 된 상태에 도달 하는 VM에 다음과 같이 업데이트 됩니다.

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. VM 역할 크기 hello 및 hello Azure 네트워크 tooattach hello 가상 컴퓨터의 네트워크 인터페이스 카드 tooupon 장애 조치 같은 복구 속성을 업데이트 합니다.

        PS C:\> $nw1 = Get-AzureRmVirtualNetwork -Name "FailoverNw" -ResourceGroupName "MyRG"

        PS C:\> $VMFriendlyName = "Fabrikam-App"

        PS C:\> $VM = Get-AzureRmSiteRecoveryVM -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName

        PS C:\> $UpdateJob = Set-AzureRmSiteRecoveryVM -VirtualMachine $VM -PrimaryNic $VM.NicDetailsList[0].NicId -RecoveryNetworkId $nw1.Id -RecoveryNicSubnetName $nw1.Subnets[0].Name

        PS C:\> $UpdateJob = Get-AzureRmSiteRecoveryJob -Job $UpdateJob

        PS C:\> $UpdateJob

        Name             : b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        ID               : /Subscriptions/a731825f-4bf2-4f81-a611-c331b272206e/resourceGroups/MyRG/providers/Microsoft.RecoveryServices/vault
                           s/MyVault/replicationJobs/b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        Type             : Microsoft.RecoveryServices/vaults/replicationJobs
        JobType          : UpdateVmProperties
        DisplayName      : Update hello virtual machine
        ClientRequestId  : 805a22a3-be86-441c-9da8-f32685673112-2015-12-10 17:55:51Z-P
        State            : Succeeded
        StateDescription : Completed
        StartTime        : 10-12-2015 17:55:53 +00:00
        EndTime          : 10-12-2015 17:55:54 +00:00
        TargetObjectId   : 289682c6-c5e6-42dc-a1d2-5f9621f78ae6
        TargetObjectType : ProtectionEntity
        TargetObjectName : Fabrikam-App
        AllowedActions   : {Restart}
        Tasks            : {UpdateVmPropertiesTask}
        Errors           : {}



## <a name="step-8-run-a-test-failover"></a>8단계: 테스트 장애 조치 실행
1. 다음과 같이 테스트 장애 조치 작업을 실행합니다.

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. Azure에서 VM을 만든 hello 테스트를 확인 합니다. (hello 테스트 장애 조치 작업이 중지 됨, Azure의 hello 테스트 VM을 만든 후 합니다. hello 작업이 hello 다음 단계에 설명 된 대로 hello 작업을 다시 시작 시 hello 만든 artefacts을 정리 하 여 완료 됩니다.)
3. 테스트 장애 조치을 다음과 같이 전체 hello:

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a>다음 단계
[자세히 알아보세요](https://msdn.microsoft.com/library/azure/mt637930.aspx) .
