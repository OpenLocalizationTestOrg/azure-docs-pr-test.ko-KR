---
title: "백업에서 가상 컴퓨터는 aaaRestore | Microsoft Docs"
description: "Azure 가상 컴퓨터는 복구에서 지점을 하는 toorestore 방법에 대해 알아봅니다"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "백업으로 복원 어떻게 toorestore; 복구 지점입니다."
ms.assetid: fed877b3-b496-49fb-99e4-653be7c23e3a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: trinadhk; jimpark;
ms.openlocfilehash: 44c25f3248784accd1c2beaabb2c9a4dca3232d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-virtual-machines-in-azure"></a>Azure의 가상 컴퓨터 복원
> [!div class="op_single_selector"]
> * [Azure 포털에서 VM 복원](backup-azure-arm-restore-vms.md)
> * [클래식 포털에서 VM 복원](backup-azure-restore-vms.md)
>
>

단계를 수행 하는 hello로는 Azure 백업 자격 증명 모음에 저장 된 hello 백업에서 새 VM을 가상 컴퓨터 tooa를 복원 합니다.

> [!IMPORTANT]
> 이제 사용자 백업 자격 증명 모음 tooRecovery 서비스 자격 증명 모음을 업그레이드할 수 있습니다. 자세한 내용은 hello 문서 참조 [복구 서비스 자격 증명 모음에 백업 자격 증명 모음 tooa 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md)합니다. Microsoft는 것이 권장 tooupgrade 백업 tooRecovery 서비스 자격 증명 모음 자격 증명 모음입니다.<br/> **2017 년 10 월 15**, 수 toouse PowerShell toocreate 백업 자격 증명 모음은 더 이상 됩니다. <br/> **2017년 11월 1일 시작**:
>- 나머지 모든 백업 자격 증명 모음을 자동으로 업그레이드 된 tooRecovery 서비스 자격 증명 모음 됩니다.
>- 하면 hello 클래식 포털에서 수 tooaccess 백업 데이터 수 없습니다. 대신, 복구 서비스 자격 증명 모음에 hello Azure 포털 tooaccess 백업 데이터를 사용 합니다.
>

## <a name="restore-workflow"></a>워크플로 복원
### <a name="step-1-choose-an-item-toorestore"></a>1 단계: 선택 항목이 toorestore
1. Toohello 이동 **보호 된 항목** 탭 하 고 선택 hello toorestore tooa 가상 컴퓨터가 새 VM입니다.

    ![보호된 항목](./media/backup-azure-restore-vms/protected-items.png)

    hello **복구 지점** 열 hello에 **보호 된 항목** 페이지의 가상 컴퓨터에 대 한 복구 지점 수 hello 알 수 있습니다. hello **Newest 복구 지점** 열 가상 컴퓨터를 복원할 수 있는 hello 가장 최근 백업 시간을 hello를 나타냅니다.
2. 클릭 **복원** tooopen hello **항목 복원** 마법사.

    ![항목 복원](./media/backup-azure-restore-vms/restore-item.png)

### <a name="step-2-pick-a-recovery-point"></a>2단계: 복구 지점 선택
1. Hello에 **복구 지점을 선택** 화면 또는 복원할 수 있습니다 hello 최신 복구 지점에서 이전 시점에서 시간에서입니다. hello 마법사가 열릴 때 선택 된 기본 옵션은 *Newest 복구 지점*합니다.

    ![복구 지점 선택](./media/backup-azure-restore-vms/select-recovery-point.png)
2. 시간 내에 이전 시점 toopick 선택 hello **날짜 선택** hello를 클릭 하 여 hello 달력 컨트롤에서 날짜를 선택 하 고 hello 드롭다운에서 옵션 **달력 아이콘**합니다. Hello 컨트롤에서 복구 지점에 있는 모든 날짜 밝은 회색 음영으로 채워져 및 hello 사용자가 선택할 수 있습니다.

    ![날짜 선택](./media/backup-azure-restore-vms/select-date.png)

    Hello calendar 컨트롤에서 날짜를 클릭 한 후 hello 복구 지점에서 사용할 수 있는 날짜 복구 지점 테이블 아래에 나타납니다. hello **시간** 열은 hello에 스냅숏이 만들어진 hello 시간을 나타냅니다. hello **형식** 열 표시 hello [일관성](https://azure.microsoft.com/documentation/articles/backup-azure-vms/#consistency-of-recovery-points) hello 복구 지점입니다. hello 테이블 머리글 괄호 안에 해당 날짜에 사용할 수 있는 복구 지점이 hello 수를 표시합니다.

    ![복구 지점](./media/backup-azure-restore-vms/recovery-points.png)
3. Hello에서 hello 복구 지점을 선택 **복구 지점을** 테이블 마우스 hello 다음 화살표 toogo toohello 다음 화면을 클릭 합니다.

### <a name="step-3-specify-a-destination-location"></a>3단계: 대상 위치 지정
1. Hello에 **복원 인스턴스 선택** 화면 위치 toorestore hello 가상 컴퓨터의 세부 정보를 지정 합니다.

   * Hello 가상 컴퓨터 이름 지정: 지정 된 클라우드 서비스에 hello 가상 컴퓨터 이름은 고유 해야 합니다. 기본 VM 덮어쓰기를 지원하지 않습니다.
   * Hello VM에 대 한 클라우드 서비스를 선택: VM을 만들기 위한 필수 항목입니다. Tooeither 사용 하 여 기존 클라우드 서비스를 선택 하거나 새 클라우드 서비스를 만들 수 있습니다.

        선택한 클라우드 서비스 이름은 전역적으로 고유해야 합니다. 일반적으로 hello 클라우드 서비스 이름 hello [cloudservice] 형식의 공용 URL과 통해 연결 됩니다. cloudapp.net에 합니다. Azure는 수 없습니다 toocreate 새 클라우드 서비스는 hello 이름이 이미 사용 하는 경우. 됩니다 toocreate 새 클라우드 서비스를 선택 하면 선택 이름은 hello hello 가상 컴퓨터로-어떤 사례 hello VM에서에서 이름과 같은 이름을 지정한 적용 하는 고유한 toobe toohello 연결 된 클라우드 서비스 수입니다.

        클라우드 서비스만 표시 하 고 hello에서 모든 선호도 그룹과 연결 되지 않은 가상 네트워크 인스턴스 세부 정보를 복원 합니다. [자세한 정보](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
2. Hello VM에 대 한 저장소 계정을 선택: hello VM을 만들기 위한 필수 항목입니다. 에서 선택할 수 있습니다 기존 저장소 계정에서 hello 동일 지역 hello Azure 백업 자격 증명 모음으로 합니다. 영역 중복 또는 프리미엄 저장소 형식의 저장소 계정은 지원되지 않습니다.

    지원 되는 구성 된 저장소 계정이 없는 경우 지원 되는 구성은 이전 toostarting 복원 작업의 저장소 계정을 만드세요.

    ![가상 네트워크 선택](./media/backup-azure-restore-vms/restore-sa.png)
3. 가상 네트워크 선택: hello VM을 만들 때 hello hello 가상 컴퓨터를 선택 해야 hello 가상 네트워크 (VNET). hello UI에서는 사용할 수 있는이 구독 내에서 모든 hello Vnet을 복원 합니다. 필수는 아닙니다 tooselect VNET hello 복원 VM – 수 tooconnect 복원 toohello 가상 컴퓨터를 통해 됩니다에 대 한 hello 인터넷 hello VNET 적용 되지 않는 경우에 합니다.

    Hello 클라우드 경우 선택한 서비스에 있으면 가상 네트워크와 연결 hello 가상 네트워크를 변경할 수 없습니다.

    ![가상 네트워크 선택](./media/backup-azure-restore-vms/restore-cs-vnet.png)
4. 서브넷을 선택: 경우 hello VNET 서브넷에 있는 경우 기본적으로 첫 번째 서브넷 hello 선택 됩니다. Hello 드롭다운 옵션 중에서 원하는 hello 서브넷을 선택 합니다. 서브넷 세부 정보에 대 한 hello에서 tooNetworks 확장 이동 [포털 홈 페이지](https://manage.windowsazure.com/), 너무 이동**가상 네트워크** 선택 hello 가상 네트워크 및 구성 toosee 서브넷 세부 정보로 드릴 다운 합니다.

    ![서브넷 선택](./media/backup-azure-restore-vms/select-subnet.png)
5. Hello 클릭 **전송** hello 마법사 toosubmit 아이콘 hello 세부 정보 및 복원 작업을 만듭니다.

## <a name="track-hello-restore-operation"></a>Hello 복원 작업을 추적 합니다.
Hello 복원 마법사에 모든 hello 정보를 입력 하 고 보고서를 제출한 후 Azure 백업 toocreate 작업 tootrack hello 복원 작업을 시도 합니다.

![복원 작업 생성 중](./media/backup-azure-restore-vms/create-restore-job.png)

Hello 작업이 성공적으로 만들어지면 해당 hello ְ  함을 나타내는 알림을 알림이 나타납니다. Hello를 클릭 하 여 자세한 내용을 확인할 수 **작업 보기** 아래쪽에는 너무**작업** 탭 합니다.

![복원 작업이 생성됨](./media/backup-azure-restore-vms/restore-job-created.png)

Hello 복원 작업이 완료 되 면 표시 됩니다에서 완료 된 것으로 **작업** 탭 합니다.

![복원 작업 완료](./media/backup-azure-restore-vms/restore-job-complete.png)

가상 컴퓨터에 기존 toore 설치 hello 확장 해야 할 수 있습니다 hello 복원 후 원본 VM hello 및 [hello 끝점 수정](../virtual-machines/windows/classic/setup-endpoints.md) hello Azure 포털에서에서 가상 컴퓨터 hello에 대 한 합니다.

## <a name="post-restore-steps"></a>복원 후 단계
Ubuntu와 같은 클라우드 초기화 기반 Linux 배포를 사용하는 경우 보안상의 이유로 복원 후 암호를 차단합니다. 하십시오 hello에 VMAccess 확장을 사용 하 여 복원 된 VM 너무[hello 암호 재설정](../virtual-machines/linux/classic/reset-access.md)합니다. 이러한 분포 tooavoid post 복원 암호 재설정에 SSH 키를 사용 하는 것이 좋습니다.

## <a name="backup-for-restored-vms"></a>복원된 VM에 대한 백업
이름이 같은 VM 원래 백업 hello로 VM toosame 클라우드 서비스를 복원 하는 경우에 VM post 복원으로 hello에 백업은 계속 됩니다. 가 중 VM tooa 다른 클라우드 서비스를 복원 하거나 복원 된 VM에 대 한 다른 이름을 지정한 경우 새 VM으로 간주 되며이 및 복원 된 VM toosetup 백업 해야 합니다.

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a>Azure 데이터 센터 재해 중 VM 복원
Azure 백업 hello 주 데이터 센터 위치 경험 재해를 실행 중인 Vm 및 백업 자격 증명 모음 toobe 지리적 중복을 구성 하는 경우 Vm toohello 쌍 이룬된 데이터 센터 백업 복원할 수 있습니다. 이러한 시나리오 중 tooselect 쌍 이룬된 데이터 센터에 있는 저장소 계정 및 hello 복원 프로세스의 나머지 부분과 동일한 상태를 유지 합니다. Azure 백업에는 계산 서비스 쌍 이룬된 지역 toocreate 복원 hello 가상 컴퓨터에서 사용 됩니다. [Azure 데이터 센터 복원력](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)에 대한 자세한 정보

## <a name="restoring-domain-controller-vms"></a>도메인 컨트롤러 VM 복원
DC(도메인 컨트롤러) 가상 컴퓨터 백업은 Azure 백업을 사용하는 지원되는 시나리오입니다. 그러나 주의 해야 hello 복원 프로세스 중입니다. hello 올바른 복원 프로세스 hello 도메인의 hello 구조에 따라 달라 집니다. 가장 간단한 경우 hello에서에서 단일 도메인에 있는 단일 DC 수 있습니다. 일반적으로 프로덕션 로드에서는 단일 도메인에 여러 DC가 있고, 일부 DC는 온-프레미스에 있을 수 있습니다. 여러 도메인이 있는 포리스트도 있을 수 있습니다.

Active Directory 관점 hello에서 Azure VM에서 지원 되는 최신 하이퍼바이저 다른 VM과 같습니다. hello 주요 차이점 온-프레미스 하이퍼바이저와은 Azure에서 사용할 수 없는 VM 콘솔 임을입니다. BMR(완전 복구) 유형 백업을 사용한 복구와 같은 특정 시나리오에서는 콘솔이 필요합니다. 그러나 VM 복원 hello 백업 자격 증명 모음에서 BMR에 대 한 대체입니다. Active Directory 복원 모드(DSRM)도 사용할 수 있으므로 모든 Active Directory 복구 모드를 실행할 수 있습니다. 자세한 배경 정보는 [Backup and Restore considerations for virtualized Domain Controllers](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers)(가상화된 도메인 컨트롤러에 대한 백업 및 복원 고려 사항) 및 [Planning for Active Directory Forest Recovery](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx)(Active Directory 포리스트 복구 계획)를 참조하세요.

### <a name="single-dc-in-a-single-domain"></a>단일 도메인의 단일 DC
hello VM에서에서 복원할 수 있습니다 (예: 다른 VM) hello Azure 포털 또는 PowerShell을 사용 하 여 합니다.

### <a name="multiple-dcs-in-a-single-domain"></a>단일 도메인의 여러 DC
Hello 통해 동일한 도메인에 연결할 수의 다른 Dc hello 네트워크, 하는 경우 모든 VM 같은 hello DC를 복원할 수 있습니다. 이면 hello 도메인의 마지막 남은 DC hello 또는 격리 된 네트워크에서 복구 수행 될 포리스트 복구 절차를 따라야 합니다.

### <a name="multiple-domains-in-one-forest"></a>한 포리스트의 여러 도메인
Hello 통해 동일한 도메인에 연결할 수의 다른 Dc hello 네트워크, 하는 경우 모든 VM 같은 hello DC를 복원할 수 있습니다. 그러나 다른 모든 경우에 포리스트 복구를 사용하는 것이 좋습니다.

<!--- WK: this following original supportability statement is incorrect, taking it out.
hello challenge arises because DSRM mode is not present in Azure. So toorestore such a VM, you cannot use hello Azure portal. hello only supported restore mechanism is disk-based restore using PowerShell.

> [!WARNING]
> For Domain Controller VMs in a multi-DC environment, do not use hello Azure portal for restore! Only PowerShell based restore is supported
>
>

Read more about hello [USN rollback problem](https://technet.microsoft.com/library/dd363553) and hello strategies suggested toofix it.
--->

## <a name="restoring-vms-with-special-network-configurations"></a>특수 네트워크 구성을 가진 Vm 복원
Azure 백업은 다음 가상 컴퓨터의 특수 네트워크 구성에 대한 백업을 지원합니다.

* 부하 분산 장치에서의 VM(내부 및 외부)
* 다중의 예약된 IP가 있는 VM
* 다중 NIC가 있는 VM

이러한 구성은 복원 중 다음의 고려 사항을 위임합니다.

> [!TIP]
> PowerShell 기반 복원 흐름 toorecreate hello 특수 한 네트워크 구성의 Vm post 복원 사용 하십시오.
>
>

### <a name="restoring-from-hello-ui"></a>Hello UI에서에서 복원:
UI에서 복원하는 동안 **항상 새 클라우드 서비스를 선택**합니다. 하십시오 복원 것을 확인만 포털 흐름 복원 하는 동안 필수 매개 변수를 사용, 이후 Vm UI를 사용 하 여이 회사는 hello 특수 한 네트워크 구성을 손실 됩니다. 즉, 복원 VM은 부하 분산 장치 또는 다중 NIC 또는 다중 예약된 IP의 구성이 없는 기본 VM입니다.

### <a name="restoring-from-powershell"></a>PowerShell에서 복원:
PowerShell은 hello 기능 toojust hello VM 디스크 백업에서 복원 하 고 hello 가상 컴퓨터를 만들에 있습니다. 이는 앞에서 언급된 특수 네트워크 구성을 요구하는 가상 컴퓨터를 복원하는 경우에 유용합니다.

순서 대로 toofully 디스크를 복원 하는 hello 가상 컴퓨터 게시를 다시 만듭니다. 다음이 단계를 수행 하십시오.

1. Hello 디스크를 사용 하 여 백업 자격 증명 모음에서 복원 [Azure 백업 PowerShell](backup-azure-vms-classic-automation.md#restore-an-azure-vm)
2. 부하 분산 장치에 필요한 hello VM 구성을 만듭니다/다중 NIC/다중 예약 된 IP를 사용 하 여 hello PowerShell cmdlet 및 toocreate hello 원하는 구성의 VM을 사용 합니다.

   * [내부 부하 분산 장치 ](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)
   * VM tooconnect 너무 만들기[인터넷에 부하 분산 장치를 연결 합니다.](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)
   * [다중 NIC](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)
   * [다중의 예약된 IP](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)

## <a name="next-steps"></a>다음 단계
* [문제 해결](backup-azure-vms-troubleshoot.md#restore)
* [가상 컴퓨터 관리](backup-azure-manage-vms.md)
