---
title: "사이트 복구 자격 증명 모음 aaaUpgrade tooan Azure 복구 서비스 자격 증명 모음"
description: "어떻게 tooupgrade는 Azure Site Recovery 자격 증명 모음 tooa 복구 서비스 자격 증명 모음에 대해 알아봅니다."
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/31/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: a18a923ee3bad91873e654c9b9b5bf8b83acc123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-site-recovery-vault-tooan-azure-resource-manager-based-recovery-services-vault"></a>사이트 복구 자격 증명 모음 tooan Azure 리소스 관리자 기반 복구 서비스 자격 증명 모음 업그레이드

이 문서에서는 Azure Site Recovery tooupgrade 진행 중인 복제에 영향 주지 않고 tooAzure 리소스 관리자 기반 복구 서비스 자격 증명 모음 자격 증명 모음 방법을 설명 합니다. Azure Resource Manager 기능 및 이점에 대한 자세한 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.

## <a name="introduction"></a>소개
복구 서비스 자격 증명 모음에는 hello 클라우드에서 기본적으로 백업 및 재해 복구를 관리 하기 위한 Azure 리소스 관리자 리소스입니다. 사용할 수 있는 통합 된 자격 증명 모음 hello 새 Azure 포털에서 하 고 hello 클래식 백업 대체 이며 사이트 복구 자격 증명 모음입니다.

Recovery Services 자격 증명 모음은 다음을 포함하는 기능 배열을 제공합니다.

* Azure Resource Manager 지원: 가상 컴퓨터 및 물리적 컴퓨터를 Azure Resource Manager 스택으로 보호 및 장애 조치(failover)할 수 있습니다.

* 디스크는 제외: 임시 파일 또는 않도록 toouse에 대 한 모든 대역폭이 높은 변동 데이터, 있는 경우 볼륨을 복제에서 제외할 수 있습니다. 이 기능에서 현재 사용 된 *VMware tooAzure* 및 *Hyper-v tooAzure* tooother 시나리오에도 확장 됩니다.

* Premium 및 로컬 중복 저장소에 대 한 지원: 이제는 서버 보호할 프리미엄 저장소에서 높은 고객으로 tooprotect 응용 프로그램을 허용 하는 계정 입/출력 작업 / 초 (IOPS). 이 기능은 현재에서 사용할 수 있습니다. *VMware tooAzure*합니다.

* 간소화 되어 시작 환경: 향상 된 hello 시작 환경을 설계 되었습니다 쉽게 toomake 재해 복구 설치 합니다.

* 백업 및 사이트 복구 관리에서 같은 자격 증명 모음의 hello: 이제 재해 복구를 위해 서버를 보호 하거나 hello에서 백업을 수행할 수 같은 자격 증명 모음 관리 오버 헤드를 크게 줄일 수 있습니다.

업그레이드 하는 hello 환경과 기능에 대 한 자세한 내용은 참조 hello [저장소, 백업 및 복구 블로그](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/)합니다.

## <a name="salient-features"></a>핵심 기능

* 진행 중인 복제에 영향을 주지 않음: 진행 중인 복제는 업그레이드 중과 후에 중단 없이 계속됩니다.

* 추가 비용 없음: 추가 비용 없이 업데이트된 기능의 전체 집합을 가져올 수 있습니다.

* 데이터 손실 없음:이 프로세스는 업그레이드 및 마이그레이션 하지 이기 때문에 기존 복제 복구 지점 및 설정이 그대로 동안과 그 후 hello 업그레이드 합니다.


## <a name="what-happens-during-hello-vault-upgrade"></a>Hello 자격 증명 모음 업그레이드 하는 동안 어떻게 되나요?

Hello 업그레이드 하는 동안 새 서버 등록 또는 복제 가상 컴퓨터 (VM)를 사용 하는 등의 작업을 수행할 수 없습니다. 데이터 읽기 또는 쓰기 toohello 자격 증명 모음의 보호 항목, 진행 중인 복제와 같은 데이터 toohello 자격을 포함 하는 작업은 중단 없이 계속 합니다.

### <a name="changes-tooautomation-and-tooling-after-hello-upgrade"></a>Tooautomation 및 hello 업그레이드 한 후 도구 변경
Hello 클래식 배포 모델 toohello 리소스 관리자 배포 모델에서 업그레이드 하는 hello 자격 증명 모음 유형 hello 기존 자동화 또는 도구 tooensure hello 업그레이드 후 toowork 계속 되도록 업데이트 합니다.

### <a name="prepare-your-environment-for-hello-upgrade"></a>Hello 업그레이드에 대 한 환경 준비

* [PowerShell을 설치 하거나 업그레이드할 tooversion 5 이상](https://www.microsoft.com/download/details.aspx?id=50395)
* [Hello 최신 버전의 Azure PowerShell MSI 설치](https://github.com/Azure/azure-powershell/releases)
* [Hello 복구 서비스 자격 증명 모음에 대 한 업그레이드 스크립트를 다운로드 합니다.](https://aka.ms/vaultupgradescript)

### <a name="prerequisites"></a>필수 조건
사이트 복구에서 tooupgrade tooAzure 리소스 관리자 기반 복구 서비스 자격 증명 모음 자격 증명 모음, hello 요구 사항을 준수를 충족 해야 합니다.

* 최소 에이전트 버전이: 서버에 설치 하는 Azure Site Recovery Provider의 hello 버전 5.1.1700.0 있어야 합니다. 이후 버전입니다.

* 지원되는 구성: SAN(저장 영역 네트워크) 또는 SQL Server AlwaysOn 가용성 그룹으로 자격 증명 모음을 구성할 수 없습니다. 다른 모든 구성은 지원됩니다.

    >[!NOTE]
    >Hello 업그레이드 후 PowerShell 통해 저장소 매핑을 관리할 수 있습니다.

* 지원 되는 배포 시나리오: 자격 증명 모음 hello 아니어야 *VMware tooAzure* 레거시 배포 모델입니다. 계속 진행 하기 전에 먼저 toohello 향상 된 배포 모델을 이동 합니다.

* 활성 사용자가 시작한 작업이 없습니다 관리와 관련 된 작업 평면: 업그레이드 하는 동안 액세스 toohello 관리 평면은 제한 되므로 hello 업그레이드를 트리거하기 전에 모든 관리 평면 동작을 완료 합니다. 이 프로세스에는 진행 중인 복제가 포함되지 않습니다.

## <a name="frequently-asked-questions"></a>질문과 대답

**이 업그레이드가 진행 중인 복제에 주는 영향은 무엇인가요?**

아니요. 진행 중인 복제 하는 동안 및 hello 업그레이드 한 후 중단 없이 계속 됩니다.

**사이트 간 VPN 및 IP 설정 같은 toonetwork 설정을 어떻게 되나요?**

hello 업그레이드 hello 네트워크 설정에 영향을 주지 않습니다. 모든 Azure-온-프레미스 연결은 그대로 유지됩니다.

**자격 증명 모음 toomy hello 가까운 미래에에서 tooupgrade 합니까 어떻게 됩니까?**

2017 년 9 월부터 hello 이전 Azure 포털에서 사이트 복구 자격 증명 모음에 대 한 지원이 중단 될 예정입니다. Hello 업그레이드 기능 toomove toohello 새 포털을 사용 하는 것이 좋습니다.

**이 마이그레이션 계획으로 기존 도구는 어떻게 되나요?**  

도구 toohello 리소스 관리자 배포 모델을 업데이트, 업그레이드 계획에 고려해 야 합니다 hello 가장 중요 한 변경 내용 중 하나입니다. hello 복구 서비스 자격 증명 모음 hello 리소스 관리자 배포 모델을 기반으로 합니다. 

**기간 않습니다 hello 관리 평면 가동 중지 시간이 마지막?**

일반적으로 hello 업그레이드 약 15 too30 분 정도 걸리며 최대 1 시간까지 tooa을 걸릴 수 있습니다.

**업그레이드한 후에 롤백할 수 있나요?**

아니요. Hello 리소스 성공적으로 업그레이드 된 후에 롤백이 지원 되지 않습니다.

**있습니까 있는지 확인할 수 내 구독 또는 리소스 toosee 업그레이드할 수 있습니다.**

예. Hello 플랫폼에서 지 원하는 업그레이드 옵션을 hello 업그레이드 hello 첫 번째 단계는 hello 리소스가 업그레이드 가능성을 toovalidate을 것입니다. Hello 유효성 검사에 실패 하는 경우 적절 한 오류 메시지나 경고 받습니다.

**Hello 업그레이드 문제를 보고 하려면 어떻게 해야 합니까?**

모든 오류의 경우 hello 업그레이드 하는 동안 hello 오류에 나열 된 hello 작업 ID를 확인 합니다. Microsoft 기술 지원 서비스는 hello 문제를 해결에서는 사전 실행 됩니다. 구독 ID로, 자격 증명 모음 이름, 작업 id입니다. 지원 팀 hello 문의할 수 있습니다. 지원은 tooresolve hello 문제를 가능한 한 신속 하 게 작동 합니다. 명시적으로 지시 toodo 있지 않은 경우 hello 작업을 다시 시도 하지 마세요 Microsoft에서 등입니다.

## <a name="run-hello-script"></a>Hello 스크립트 실행

PowerShell에서 다음 명령을 hello를 실행 합니다.

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionID <subscriptionID>  -VaultName <vaultname> -Location <location> -ResourceType HyperVRecoveryManagerVault -TargetResourceGroupName <rgname>

* 업그레이드 하는 hello 자격 증명 모음과 연결 된 구독 Id: hello 구독 ID입니다.

* 업그레이드 하는 hello 자격 증명 모음의 VaultName: hello 이름입니다.

* 업그레이드 하는 hello 자격 증명 모음의 위치: hello 위치입니다.

* ResourceType: Site Recovery 자격 증명 모음에 대한 HyperVRecoveryManagerVault입니다.

* TargetResourceGroupName: hello 넣을 hello 리소스 그룹에 배치 하는 자격 증명 모음 toobe를 업그레이드 합니다. TargetResourceGroupName은 Azure Resource Manager의 기존 리소스 그룹 또는 새 리소스 그룹일 수 있습니다. 제공 된 TargetResourceGroupName hello가 없는 경우 만들어집니다 hello 업그레이드의 일부로 hello에 동일한 hello 자격 증명 모음과 위치입니다. 자세한 내용은의 hello "리소스 그룹" 섹션을 참조 하십시오. [Azure 리소스 관리자 개요](../azure-resource-manager/resource-group-overview.md#resource-groups)합니다.

    >[!NOTE]
    >리소스 그룹 이름 지정 주체 toocertain 제약 조건입니다. tooprevent 자격 증명 모음 있는지 tooobserve hello 명명 규칙을 신중 하 게 될 실패를 업그레이드 합니다.
    >
    >예:
    >
    >.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc

또는 다음 스크립트는 hello를 실행할 수 있습니다. 필요한 hello 매개 변수에 대 한 hello 값을 입력 합니다.

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1
    cmdlet RecoveryServicesVaultUpgrade-1.0.0.ps1 at command pipeline position 1

    Supply values for hello following parameters:
    SubscriptionId:
    VaultName:
    Location:
    ResourceType:
    TargetResourceGroupName:

1. PowerShell 스크립트 hello 메시지 있습니다 tooenter 자격 증명을 표시합니다. 입력을 두 번 hello 클래식 배포 모델 계정에 대 한 한 번에 대해서 한 hello Azure 리소스 관리자 계정.

2. 자격 증명을 입력 한 후 사용자 인프라 설치 충족 hello 요구 사항에 앞에서 언급 한 hello 스크립트 실행 검사 toodetermine 됩니다.

3. Hello 필수 구성 요소를 검사 하 고 확인 한 후 메시지 표시 tooproceed hello 자격 증명 모음 업그레이드 됩니다. 업그레이드 자격 증명 모음 hello 업그레이드 프로세스를 시작 합니다. hello 전체 업그레이드는 15 too30 분 toocomplete를 걸릴 수 있습니다.

4. Hello 업그레이드가 성공적으로 완료 된 후 hello 새 Azure 포털의 hello 업그레이드 모음에 액세스할 수 있습니다.

## <a name="post-upgrade-vault-management"></a>업그레이드 후 자격 증명 모음 관리

### <a name="replicate-by-using-azure-site-recovery-in-hello-recovery-services-vault"></a>Hello 복구 서비스 자격 증명 모음에서 Azure Site Recovery를 사용 하 여 복제

* 이제 하나의 영역 tooanother에서 Azure Vm을 보호할 수 있습니다. 자세한 내용은 [Azure Site Recovery를 사용하여 지역 간 Azure VM 복제](site-recovery-azure-to-azure.md)를 참조하세요.

* VMware Vm tooAzure를 복제 하는 방법에 대 한 자세한 내용은 참조 [Site Recovery와 VMware Vm 복제 tooAzure](vmware-walkthrough-overview.md)합니다.

* Hyper-v Vm (VMM 없음) tooAzure를 복제 하는 방법에 대 한 자세한 내용은 참조 [복제 Hyper-v 가상 컴퓨터 (VMM 없음) tooAzure](hyper-v-site-walkthrough-overview.md)합니다.

* (VMM)과 Hyper-v Vm tooAzure를 복제 하는 방법에 대 한 자세한 내용은 참조 [복제 Hyper-v 가상 컴퓨터에서 사이트 복구를 사용 하 여 VMM 클라우드에 tooAzure hello Azure 포털](vmm-to-azure-walkthrough-overview.md)합니다.

* 하이퍼-VMs (VMM)과 tooa 보조 사이트를 복제 하는 방법에 대 한 자세한 내용은 참조 [복제 Hyper-v 가상 컴퓨터 VMM 클라우드에 tooa 보조 VMM 사이트를 사용 하 여 Azure 포털 hello](site-recovery-vmm-to-vmm.md)합니다.

* VMware Vm tooa 보조 사이트를 복제 하는 방법에 대 한 자세한 내용은 참조 [Replicate 온-프레미스 VMware 가상 컴퓨터 또는 실제 서버 hello 클래식 Azure 포털에서 보조 사이트 tooa](site-recovery-vmware-to-vmware.md)합니다.

### <a name="view-your-replicated-items"></a>복제된 항목 보기

hello 다음 이미지에서는 hello 자격 증명 모음에 대 한 주요 엔터티를 표시 하는 hello 복구 서비스 자격 증명 모음 대시보드 페이지 tooview hello 자격 증명 모음에 있는 보호 된 엔터티 목록을 선택 **사이트 복구** > **복제 항목**합니다.


![복제된 항목](./media/upgrade-site-recovery-vaults/replicateditems.png)

hello 다음 그림에 나와 복제 된 항목 및 hello를 보기 위한 hello 워크플로 **장애 조치** 장애 조치를 개시 하는 것에 대 한 명령입니다.

![복제된 항목](./media/upgrade-site-recovery-vaults/failover.png)

### <a name="view-your-replication-settings"></a>복제 설정 보기

Hello 사이트 복구 자격 증명 모음에 각 보호 그룹은 다른 복제 설정을 복사 빈도, 복구 지점 보존, 응용 프로그램 일관성 스냅숏 빈도와 구성 됩니다. Hello 복구 서비스 자격 증명 모음에 이러한 설정은 복제 정책으로 구성 됩니다. hello hello 정책 이름은 hello 보호 그룹이 나 hello hello 이름을 *primarycloud_Policy*합니다.

복제 정책에 대 한 자세한 내용은 참조 [VMware tooAzure에 대 한 복제 정책을 관리](site-recovery-setup-replication-settings-vmware.md)합니다.
