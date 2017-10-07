---
title: "소개: Recovery Services 자격 증명 모음으로 Azure VM 보호 | Microsoft 문서"
description: "복구 서비스 자격 증명 모음으로 Azure VM 보호. 리소스 관리자를 통해 배포 된 Vm, Vm 클래식 배포 및 프리미엄 저장소 Vm, Vm 암호화 tooprotect 관리 하는 디스크에 있는 Vm의 백업 데이터를 사용 합니다. 복구 서비스 자격 증명 모음을 만들고 등록합니다. Azure에서 VM을 등록하고 정책을 만들며 VM을 보호합니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keyword: backups; vm backup
ms.assetid: 45e773d6-c91f-4501-8876-ae57db517cd1
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/15/2017
ms.author: markgal;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70e4700abb76e16e32e1ead06ce1dbe277e1f0e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-toorecovery-services-vaults"></a>Azure 가상 컴퓨터 tooRecovery 서비스 자격 증명 모음에 백업
> [!div class="op_single_selector"]
> * [복구 서비스 자격 증명 모음으로 VM 보호](backup-azure-vms-first-look-arm.md)
> * [백업 자격 증명으로 VM 보호](backup-azure-vms-first-look.md)
>
>

이 자습서에서는 복구 서비스 자격 증명 모음을 만들고 Azure 가상 컴퓨터 (VM)를 백업 하기 위한 hello 단계를 안내 합니다. 복구 서비스 자격 증명 모음이 보호하는 항목:

* Azure Resource Manager 배포 VM
* 클래식 VM
* 표준 저장소 VM
* 프리미엄 저장소 VM
* Managed Disks에서 실행 중인 VM
* Azure Disk Encryption와 BEK 및 KEK를 사용하여 암호화된 VM
* 사용자 지정 사전 스냅숏 및 사후 스냅숏 스크립트를 사용하는 VSS 및 Linux VM을 사용하여 Windows VM의 응용 프로그램 일치 백업

프리미엄 저장소 Vm 보호에 대 한 자세한 내용은 hello 문서 참조 [백업 및 복원 프리미엄 저장소 Vm](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup)합니다. Managed Disks VM 지원에 대한 자세한 내용은 [Managed Disks의 VM 백업 및 복원](backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup)을 참조하세요. Linux VM을 백업하기 위한 사전 및 사후 스크립트 프레임워크에 대한 자세한 내용은 [사전 및 사후 스크립트를 사용하여 응용 프로그램 일치 Linux VM 백업](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent)을 참조하세요.

더에 대 한 백업 있습니다 수 및 없습니다, toofind 참조 [여기](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)

> [!NOTE]
> 이 자습서를 수행 하 여 측정값 tooallow hello 백업 서비스 tooaccess hello VM 및 Azure 구독에서 이미 VM이 있는 가정 합니다.
>
>

[!INCLUDE [learn-about-Azure-Backup-deployment-models](../../includes/backup-deployment-models.md)]

가상 컴퓨터의 hello 수에 따라 tooprotect 5d; 여러 시작 지점에서 시작할 수 있습니다. 한 번에 여러 가상 컴퓨터를 tooback 원한다 면 이동 toohello 복구 서비스 자격 증명 모음 및 [hello 자격 증명 모음 대시보드에서 백업 작업 시작 hello](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-recovery-services-vault)합니다. 단일 가상 컴퓨터를 tooback 원한다 면 hello VM 관리 블레이드에서 백업 작업을 시작할 수 있습니다.

## <a name="configure-hello-backup-job-from-hello-vm-management-blade"></a>Hello hello VM 관리 블레이드에서 백업 작업 구성

Hello Azure 포털에서에서 가상 컴퓨터 관리 블레이드 hello에서에서 단계 tooconfigure hello에 대 한 백업 작업을 수행 하는 hello를 사용 합니다. 이러한 단계는 hello 클래식 포털에서 가상 컴퓨터 toohello 적용 되지 않습니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. Hello 허브 메뉴에서 클릭 **더 서비스** hello 필터 대화 상자에서 입력 **가상 컴퓨터**합니다. 입력 하는 동안 리소스의 hello 목록을 필터링 합니다. 가상 컴퓨터가 표시되면 선택합니다.

  ![허브 메뉴에서 서비스 보다 tooopen 텍스트 대화 상자에서를 클릭 하 고 가상 컴퓨터를 입력 합니다.](./media/backup-azure-vms-first-look-arm/open-vm-from-hub.png)

  hello 구독에서 가상 컴퓨터 (VM) hello 목록이 표시 됩니다.

  ![hello 구독에서 Vm의 hello 목록이 나타납니다.](./media/backup-azure-vms-first-look-arm/list-of-vms.png)

3. Hello 목록에서 VM tooback를 선택 합니다.

  ![hello 구독에서 Vm의 hello 목록이 나타납니다.](./media/backup-azure-vms-first-look-arm/list-of-vms-selected.png)

  Hello VM을 선택 하면 가상 컴퓨터의 목록을 hello 프로비저닝으로 전환 toohello 왼쪽 및 hello 가상 컴퓨터 관리 블레이드 hello 가상 컴퓨터 대시보드를 엽니다. </br>
 ![VM 관리 블레이드](./media/backup-azure-vms-first-look-arm/vm-management-blade.png)

4. Hello VM 관리 블레이드의 hello **설정** 섹션에서 클릭 **백업**합니다. </br>

  ![VM 관리 블레이드의 백업 옵션](./media/backup-azure-vms-first-look-arm/backup-option-vm-management-blade.png)

  hello 사용 백업 블레이드를 엽니다.

  ![VM 관리 블레이드의 백업 옵션](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

5. Hello 복구 서비스 자격 증명 모음에 대 한 클릭 **기존 선택** hello 드롭 다운 목록에서 hello 자격 증명 모음을 선택 합니다.

  ![백업 마법사 사용](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

  복구 서비스 자격 증명 모음는 않거나 toouse 새 자격 증명 모음을 클릭 하 여 **새로 만들기** hello hello 새 자격 증명 모음 이름을 제공 합니다. 새 자격 증명 모음에서에서 만든 hello 동일한 리소스 그룹 및 hello 가상 컴퓨터와 동일한 위치입니다. Toocreate 값이 서로 다른 복구 서비스 자격 증명 모음을 사용 하도록 하려는 경우 hello에 섹션을 참조 방법을 너무[복구 서비스 자격 증명 모음 만들기](backup-azure-vms-first-look-arm.md#create-a-recovery-services-vault-for-a-vm)합니다.

6. 백업 정책 hello의 tooview hello 세부 정보 클릭 **백업 정책**합니다.

  hello **백업 정책** 블레이드가 열리고 선택한 hello 정책 hello 세부 정보를 제공 합니다. 다른 정책이 있는 경우에 hello 드롭 다운 메뉴 toochoose 다른 백업 정책을 사용 합니다. Toocreate 정책을 선택 **새로 만들기** hello 드롭 다운 메뉴에서 합니다. 백업 정책 정의에 대한 지침은 [백업 정책 정의](backup-azure-vms-first-look-arm.md#defining-a-backup-policy)를 참조하세요. toosave hello 변경 toohello 백업 정책 및 반환 toohello 사용 백업 블레이드 클릭 **확인**합니다.

  ![백업 정책 선택](./media/backup-azure-vms-first-look-arm/setting-rs-backup-policy-new-2.png)

7. Hello 사용 백업 블레이드에서 클릭 **백업 사용** toodeploy hello 정책입니다. Hello 정책을 배포 하는 hello 자격 증명 모음 및 hello 가상 컴퓨터와 연결 합니다.

  ![백업 사용 단추](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-button.png)

8. Hello 포털에 표시 되는 hello 알림을 통해 hello 구성 진행률을 추적할 수 있습니다. 다음 예제는 hello 배포 시작 되었음을 보여 줍니다.

  ![백업 사용 알림](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-notification.png)

9. Hello VM 관리 블레이드의 hello 구성 진행률 완료 되 면 클릭 **백업** tooopen hello 백업 항목 블레이드 뷰와 hello 세부 정보입니다.

  ![VM 백업 항목 보기](./media/backup-azure-vms-first-look-arm/backup-item-view.png)

  Hello 초기 백업을 완료 되기 전 까지는 **마지막 백업 상태** 표시 **경고 (초기 백업 보류 중인)**합니다. toosee hello 다음 백업 작업을 예약 하는 경우 발생 **백업 정책** hello 정책 hello 이름을 클릭 합니다. hello 백업 정책 블레이드에서 열리고 hello hello 예약 된 백업 시간을 표시 합니다.

10. toorun 백업 작업 및 hello 초기 복구 지점 만들기, 백업 hello에 블레이드 클릭 자격 증명 모음에 **지금 백업**합니다.

  ![백업 지금 toorun hello 초기 백업을 클릭합니다](./media/backup-azure-vms-first-look-arm/backup-now.png)

  hello 지금 백업 블레이드를 엽니다.

  ![hello 지금 백업 블레이드를 표시합니다.](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

11. Hello 지금 백업 블레이드의 hello 달력 아이콘을 hello 달력 컨트롤 tooselect hello 마지막 날이 복구 지점을 유지 하 고 클릭을 사용 하 여 **백업**합니다.

  ![hello 마지막 날 hello 지금 백업 복구 지점을 유지 되는 설정](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  배포 알림 hello 백업 작업 트리거 되었으며 hello 작업 hello 백업 작업 페이지의 hello 진행률을 모니터링할 수 있습니다 알 수 있습니다.

## <a name="configure-hello-backup-job-from-hello-recovery-services-vault"></a>Hello hello 복구 서비스 자격 증명 모음에서 백업 작업 구성
tooconfigure hello 백업 작업을 마친 hello 단계를 수행 합니다.  

1. 가상 컴퓨터에 대한 Recovery Services 자격 증명 모음을 만듭니다.
2. 사용 하 여 hello Azure 포털 tooselect 시나리오에서는 백업 정책을 설정 하 고 항목 tooprotect를 식별 합니다.
3. Hello 초기 백업을 실행 합니다.

## <a name="create-a-recovery-services-vault-for-a-vm"></a>VM에 대한 복구 서비스 자격 증명 모음 만들기
복구 서비스 자격 증명 모음에는 모든 hello 백업 및 시간에 따라 생성 된 복구 지점을 저장 하는 엔터티입니다. hello 복구 서비스 자격 증명 모음도 포함 hello 백업 정책이 적용 toohello Vm을 보호 합니다.

> [!NOTE]
> VM 백업은 로컬 프로세스입니다. 다른 위치에 있는 한 위치 tooa 복구 서비스 자격 증명 모음에서 Vm 백업할 수 없습니다. 따라서 Vm toobe 백업에 있는 모든 Azure 위치에 대 한 해당 위치에 복구 서비스 자격 증명 모음을 하나 이상 존재 해야 합니다.
>
>

toocreate 복구 서비스 자격 증명 모음:

1. 그렇게 이미 하지 않은 경우 toohello 로그인 [Azure 포털](https://portal.azure.com/) Azure 구독을 사용 하 여 합니다.
2. Hello 허브 메뉴에서 클릭 **더 많은 서비스** 및 필터 대화 상자 유형 hello **복구 서비스**합니다. 입력 하는 동안 리소스의 hello 목록을 필터링 합니다. 복구 서비스 자격 증명 모음 hello 목록에 표시 되는 경우 클릭 합니다.

    ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    Hello 구독에서 복구 서비스 자격 증명 모음 인 경우 hello 자격 증명 모음 나열 됩니다.

    ![복구 서비스 자격 증명 모음 만들기 2단계](./media/backup-azure-vms-first-look-arm/list-of-rs-vault.png)
3. Hello에 **복구 서비스 자격 증명 모음** 메뉴를 클릭 하 여 **추가**합니다.

    ![복구 서비스 자격 증명 모음 만들기 2단계](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    hello 복구 서비스 자격 증명 모음에 블레이드에서 열립니다 tooprovide 묻는 **이름**, **구독**, **리소스 그룹**, 및 **위치**합니다.

    ![Recovery Services 자격 증명 모음 만들기 3단계](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. 에 대 한 **이름**, 이름 tooidentify hello 자격 증명 모음을 입력 합니다. hello 이름이 필요 toobe 고유 hello Azure 구독에 대 한 합니다. 이름을 2~50자 사이로 입력합니다. 문자로 시작해야 하며, 문자, 숫자, 하이픈만 사용할 수 있습니다.

5. Hello에 **구독** 섹션 hello 드롭 다운 메뉴 toochoose hello Azure 구독을 사용 합니다. 단일 구독을 사용 하는 경우 해당 구독 표시 되 고 toohello 다음 단계를 건너뛸 수 있습니다. 어떤 구독이 toouse 해야 할지 잘 모를 경우 hello 기본값을 사용 하 여 (또는 제안) 구독 합니다. 조직 계정이 여러 Azure 구독과 연결된 경우에만 여러 항목을 선택할 수 있습니다.

6. Hello에 **리소스 그룹** 섹션:

    * 선택 **새로 만들기** toocreate 리소스 그룹에 들어 있습니다.
    또는
    * 선택 **기존 항목 사용** hello 드롭 다운 메뉴 toosee hello 사용 가능한 리소스 그룹의 목록을 클릭 합니다.

  리소스 그룹에 대 한 자세한 내용은 참조 hello [Azure 리소스 관리자 개요](../azure-resource-manager/resource-group-overview.md)합니다.

7. 클릭 **위치** tooselect hello hello 자격 증명 모음에 대 한 지리적 영역입니다. 여기에서이 선택한 hello 지리적 지역에 백업 데이터를 보내는 위치를 결정 합니다.

  > [!IMPORTANT]
  > VM 존재 하는 hello 위치의 확실 하지 않은, hello 자격 증명 모음 만들기 대화 상자를 닫은 hello 포털에서 가상 컴퓨터의 toohello 목록을 이동 합니다. 가상 컴퓨터가 여러 지역에 있는 경우 각 지역에 Recovery Services 자격 증명 모음을 만듭니다. Toohello 다음 위치를 진행 하기 전에 hello 첫 번째 위치에 hello 자격 증명 모음을 만듭니다. Toostore hello 백업 데이터-hello 복구 서비스 자격 증명 모음을 사용 하는 필요성 toospecify hello 저장소 계정이 없습니다 않으며 hello Azure 백업 서비스는 hello 저장소를 자동으로 처리 합니다.
  >

8. Hello 복구 서비스 자격 증명 모음 블레이드의 hello 아래쪽 클릭 **만들기**합니다.

    복구 서비스 자격 증명 모음에 만든 toobe hello에 대 일 분 정도 걸릴 수 있습니다. Hello 포털의 상단 오른쪽 영역 hello에서에서 hello 상태 알림을 모니터링 합니다. 자격 증명 모음을 만든 후의 복구 서비스 자격 증명 모음 hello 목록에 나타납니다. 몇 분이 지나도 자격 증명 모음이 보이지 않으면 **새로 고침**을 클릭합니다.

    ![새로 고침 단추 클릭](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    자격 증명 모음 자격 증명 모음은 복구 서비스의 hello 목록에 표시 되는 경우 준비 tooset hello 저장소 중복 됩니다.

자격 증명 모음을 만든 했으므로 tooset 저장소 복제 hello 하는 방법을 알아봅니다.

### <a name="set-storage-replication"></a>저장소 복제 설정
hello 저장소 복제 옵션 지역 중복 저장소와 로컬 중복 저장소는 toochoose가 있습니다. 기본적으로 사용자 자격 증명 모음에는 지역 중복 저장소가 있습니다. 복구 서비스 자격 증명 모음에 hello 기본 백업을 이면 hello 저장소 복제 옵션 집합 toogeo 중복 저장소를 둡니다. 오래 지속되지 않는 저렴한 옵션을 원하는 경우에는 로컬 중복 저장소를 선택합니다. 에 대해 자세히 알아보세요 [지리적 중복](../storage/common/storage-redundancy.md#geo-redundant-storage) 및 [로컬 중복](../storage/common/storage-redundancy.md#locally-redundant-storage) hello에 대 한 저장소 옵션 [Azure 저장소 복제 개요](../storage/common/storage-redundancy.md)합니다.

tooedit hello 저장소 복제 설정입니다.

1. Hello에서 **복구 서비스 자격 증명 모음** 블레이드, 선택 hello 새 자격 증명 모음입니다.

  ![복구 서비스 자격 증명 모음의 hello 목록에서 hello 새 자격 증명 모음을 선택 합니다.](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

  Hello 자격 증명 모음을 선택 하면 hello 설정 블레이드에서 (*hello 자격 증명 모음의 이름을 hello 위쪽에 있는*) 및 hello 자격 증명 모음 세부 정보 블레이드에서 엽니다.

  ![새 자격 증명 모음에 대 한 hello 저장소 구성 보기](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. Hello 새 자격 증명 모음의 설정 블레이드에서 toohello 관리 섹션 아래로 수직 슬라이드 tooscroll hello를 사용 하 여 마우스 클릭 **백업 인프라**합니다.
    hello 백업 인프라 블레이드를 엽니다.
3. Hello 백업 인프라 블레이드에서 클릭 **백업 구성** tooopen hello **백업 구성** 블레이드입니다.

    ![새 자격 증명 모음에 대 한 저장소 구성을 hello 설정](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. 자격 증명 모음에 대 한 hello 적절 한 저장소 복제 옵션을 선택 합니다.

    ![저장소 구성 선택 항목](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    기본적으로 사용자 자격 증명 모음에는 지역 중복 저장소가 있습니다. 기본 백업 저장소 끝점으로 Azure를 사용 하는 경우 계속 toouse **지리적 중복**합니다. 기본 백업 저장소 끝점으로 Azure를 사용 하지 않는 경우 선택할 **로컬 중복**, hello Azure 저장소 비용을 줄입니다. [지역 중복](../storage/common/storage-redundancy.md#geo-redundant-storage) 및 [로컬 중복](../storage/common/storage-redundancy.md#locally-redundant-storage) 저장소 옵션에 대한 자세한 내용은 [저장소 중복 개요](../storage/common/storage-redundancy.md)를 참조하세요.


## <a name="select-a-backup-goal-set-policy-and-define-items-tooprotect"></a>백업 목표를 선택 하 고 정책 설정 항목 tooprotect 정의
자격 증명 모음으로 VM을 등록 하기 전에 실행 hello 검색 프로세스 tooensure toohello 구독에 추가 된 모든 새 가상 컴퓨터를 식별 됩니다. 추가 정보와 함께 hello 구독에서 가상 컴퓨터의 hello 목록에 대 한 hello 프로세스 쿼리 Azure hello 클라우드 서비스 이름 및 hello 영역 같은입니다. Hello Azure 포털, 시나리오는 toowhat hello 복구 서비스 자격 증명 모음에 tooput는 것을 의미 합니다. 정책에는 복구 지점을 수행 빈도 및 시기에 대 한 hello 일정입니다. 또한 정책은 hello 복구 지점에 대 한 hello 보존 범위를 포함합니다.

1. 자격 증명 모음을 열고 복구 서비스를 이미 있는 경우에 2 toostep을 진행 합니다. 그렇지 않은 경우 hello 허브 메뉴에서 클릭 **더 많은 서비스** hello 리소스 목록에 입력 하 고 **복구 서비스** 클릭 **복구 서비스 자격 증명 모음**합니다.

    ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    복구 서비스 자격 증명 모음 hello 목록이 표시 됩니다.

    ![Hello 복구 서비스의 보기 목록 자격 증명 모음](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

    복구 서비스 자격 증명 모음의 hello 목록에서 자격 증명 모음 tooopen 대시보드를 선택 합니다.

     ![자격 증명 모음 블레이드 열기](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)

2. Hello 자격 증명 모음 대시보드 메뉴를 클릭 **백업** tooopen hello 백업 블레이드입니다.

    ![백업 블레이드 열기](./media/backup-azure-arm-vms-prepare/backup-button.png)

    hello 백업 및 백업 목표 블레이드를 엽니다.

    ![시나리오 블레이드 열기](./media/backup-azure-arm-vms-prepare/select-backup-goal-1.png)
3. Hello에서 hello 백업 목표 블레이드에서 **여기서 작업이 실행 되는** 드롭 다운 메뉴에서 Azure를 선택 합니다. Hello에서 **하 신 toobackup 원하는** 드롭 다운을 가상 컴퓨터를 선택한 다음 클릭 **확인**합니다.

    이러한 동작은 hello 자격 증명 모음과 hello VM 확장을 등록합니다. hello 블레이드를 닫고 백업 목표 및 hello **백업 정책** 블레이드를 엽니다.

    ![시나리오 블레이드 열기](./media/backup-azure-arm-vms-prepare/select-backup-goal-2.png)

4. Hello 백업 정책 블레이드에서 hello 백업 정책을 원하는 tooapply toohello 자격 증명 모음을 선택 합니다.

    ![백업 정책 선택](./media/backup-azure-arm-vms-prepare/setting-rs-backup-policy-new.png)

    hello 기본 정책의 hello 세부 정보는 hello 드롭 다운 메뉴 아래에 나열 됩니다. Toocreate 정책을 선택 **새로 만들기** hello 드롭 다운 메뉴에서 합니다. 백업 정책 정의에 대한 지침은 [백업 정책 정의](backup-azure-vms-first-look-arm.md#defining-a-backup-policy)를 참조하세요.
    클릭 **확인** tooassociate hello 백업 정책을 hello 자격 증명 모음입니다.

    백업 정책 블레이드 닫히고 hello hello **가상 컴퓨터 선택** 블레이드를 엽니다.
5. Hello에 **가상 컴퓨터 선택** 블레이드에서 hello로 가상 컴퓨터 tooassociate hello 정책 지정 및 클릭 선택 **확인**합니다.

    ![워크로드 선택](./media/backup-azure-arm-vms-prepare/select-vms-to-backup.png)

    가상 컴퓨터를 선택 하는 hello 유효성이 검사 됩니다. Hello 가상 표시 되지 않으면 toosee에 존재 하는 검사를 예상 하는 컴퓨터 hello 복구 서비스 자격 증명 모음으로 동일한 Azure 위치를 hello 합니다. 복구 서비스 자격 증명 모음에 hello의 hello 위치 hello 자격 증명 모음 대시보드에 표시 됩니다.

6. 이제 hello 자격 증명 모음에 대 한 모든 설정을 hello 백업 블레이드에서 정의한 클릭 **백업 사용** toodeploy hello 정책 toohello 자격 증명 모음 및 Vm hello 합니다. Hello 백업 정책을 배포 하는 hello 가상 컴퓨터에 대 한 hello 초기 복구 지점을 만들지 않습니다.

    ![백업 사용](./media/backup-azure-arm-vms-prepare/vm-validated-click-enable.png)

Hello 백업을 성공적으로 활성화 한 다음 백업 정책 일정에 따라 실행 됩니다. 그러나 tooinitiate hello 첫 번째 백업 작업을 진행 합니다.

## <a name="initial-backup"></a>초기 백업
백업 정책을 의미가 있는 hello 가상 컴퓨터에 배포 된 hello 데이터가 백업 되었습니다. 기본적으로 첫 번째 예약 된 백업을 hello (정의 된 대로 hello 백업 정책에)는 hello 초기 백업 합니다. Hello 초기 백업을 수행 될 때까지 hello에서 마지막 백업 상태 hello **백업 작업** 블레이드로 표시 **경고 (초기 백업 보류 중인)**합니다.

![보류 중인 백업](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

초기 백업 기간이 하지 않는 한 toobegin 곧 것이 좋습니다를 실행 하는 **지금 백업**합니다.

toorun hello 초기 백업 작업:

1. Hello 자격 증명 모음 대시보드에서 hello 숫자 아래를 클릭 합니다. **백업 항목**, 하거나 클릭 hello **백업 항목** 바둑판식으로 배열 합니다. <br/>
  ![설정 아이콘](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)

  hello **백업 항목** 블레이드를 엽니다.

  ![항목 백업](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. Hello에 **백업 항목** 블레이드, hello 선택 항목입니다.

  ![설정 아이콘](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  hello **백업 항목** 목록 열립니다. <br/>

  ![백업 작업 트리거됨](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. Hello에 **백업 항목** 목록에서 줄임표 hello **...**  tooopen hello 상황에 맞는 메뉴입니다.

  ![상황에 맞는 메뉴](./media/backup-azure-vms-first-look-arm/context-menu.png)

  hello 상황에 맞는 메뉴가 나타납니다.

  ![상황에 맞는 메뉴](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. Hello 상황에 맞는 메뉴에서 클릭 **지금 백업**합니다.

  ![상황에 맞는 메뉴](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  hello 지금 백업 블레이드를 엽니다.

  ![hello 지금 백업 블레이드를 표시합니다.](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. Hello 지금 백업 블레이드의 hello 달력 아이콘을 hello 달력 컨트롤 tooselect hello 마지막 날이 복구 지점을 유지 하 고 클릭을 사용 하 여 **백업**합니다.

  ![hello 마지막 날 hello 지금 백업 복구 지점을 유지 되는 설정](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  배포 알림 hello 백업 작업 트리거 되었으며 hello 작업 hello 백업 작업 페이지의 hello 진행률을 모니터링할 수 있습니다 알 수 있습니다. VM의 hello 크기에 따라 hello 초기 백업을 만드는 시간이 걸릴 수 있습니다.

6. hello에 hello 자격 증명 모음 대시보드에서 hello 초기 백업 tooview 또는 트랙 hello 상태 **백업 작업** 타일 클릭 **진행에서**합니다.

  ![백업 작업 타일](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  hello 백업 작업이 블레이드를 엽니다.

  ![백업 작업 타일](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  Hello에 **백업 작업** 블레이드에서 모든 작업의 hello 상태를 확인할 수 있습니다. Hello VM에 대 한 백업 작업이 아직 진행 중인 경우, 또는 마친 경우 확인 하십시오. 백업 작업이 완료 되 면 hello 상태는 *Completed*합니다.

  > [!NOTE]
  > Hello 백업 작업의 일부로 hello Azure 백업 서비스에 모두 작성 하 고 일관 된 스냅숏을 각 VM tooflush 명령 toohello 백업 확장을 발급 합니다.
  >
  >


[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Hello 가상 컴퓨터에 hello VM 에이전트 설치
필요한 경우 이 정보가 제공됩니다. Azure VM 에이전트 hello hello 백업 확장 toowork hello에 대 한 Azure 가상 컴퓨터에 설치 되어야 합니다. 그러나, hello Azure 갤러리에서에서 VM을 만든 경우 다음 hello VM 에이전트는 이미에 hello 가상 컴퓨터. Hello VM 에이전트가 설치 되어 있지는 온-프레미스 데이터 센터에서 마이그레이션하는 하는 Vm을 선택 합니다. 이 경우 hello VM 에이전트 설치 toobe 제공 되어야 합니다. Azure VM 에이전트 hello 검사 hello 가상 컴퓨터에 제대로 설치 hello Azure VM을 백업 하는 데 문제가 있으면 (hello 다음 표 참조). 사용자 지정 VM을 만들 경우 [hello 확인 **VM 에이전트 설치 hello** 확인란이 선택 되어](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) hello 가상 컴퓨터 프로 비전 하기 전에.

Hello에 대 한 자세한 내용은 [VM 에이전트](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) 및 [어떻게 tooinstall 것](../virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.

다음 표에서 hello hello VM 에이전트에 대 한 Windows 및 Linux Vm에 대 한 추가 정보를 제공 합니다.

| **작업** | **Windows** | **Linux** |
| --- | --- | --- |
| Hello VM 에이전트를 설치합니다. |<li>다운로드 및 설치 hello [에이전트 MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)합니다. 관리자 권한 toocomplete hello 설치를 해야합니다. <li>[Hello VM 속성을 업데이트](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) 에이전트 hello tooindicate가 설치 되어 있습니다. |<li> Hello 최신 설치 [Linux 에이전트](https://github.com/Azure/WALinuxAgent) GitHub에서 합니다. 관리자 권한 toocomplete hello 설치를 해야합니다. <li> [Hello VM 속성을 업데이트](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) 에이전트 hello tooindicate가 설치 되어 있습니다. |
| Hello VM 에이전트를 업데이트합니다. |업데이트 hello VM 에이전트를 다시 설치 하는 hello [VM 에이전트 이진 파일](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)합니다. <br>Hello VM 에이전트를 업데이트 하는 동안 백업 작업이 수행 되지 실행 되 고 있는지 확인 합니다. |Hello 지침에 따라 [Linux VM 에이전트를 hello 업데이트](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. <br>백업 작업이 수행 되지 hello VM 에이전트를 업데이트 하는 동안 실행 되 고 있는지 확인 합니다. |
| Hello VM 에이전트 설치 유효성 검사 |<li>Toohello 이동 *C:\WindowsAzure\Packages* hello Azure VM에서에서 폴더입니다. <li>Hello WaAppAgent.exe 파일이 없는 찾아야 합니다.<li> Hello 파일을 마우스 오른쪽 단추로 클릭 한 다음 너무 이동 하십시오**속성**를 선택한 후 hello **세부 정보** 탭 hello 제품 버전 필드 2.6.1198.718 이루어져야 합니다. 이상. |해당 없음 |

### <a name="backup-extension"></a>백업 확장
한 번 hello 가상 컴퓨터를 hello Azure 백업 서비스에 VM 에이전트가 설치 되어 hello hello 예비 내선 번호 toohello VM 에이전트를 설치 합니다. hello Azure 백업 서비스에 원활 하 게 업그레이드 및 추가 사용자 개입 없이 hello 예비 내선 번호를 패치 합니다.

hello 백업 서비스는 hello VM이 실행 되지 않는 경우에 hello 예비 내선 번호를 설치 합니다. 실행 중인 VM 응용 프로그램 일치 복구 지점의 얻을의 hello 가장 큰 기회를 제공 합니다. 그러나 hello Azure 백업 서비스를 해제 되어 있으면 및 hello 확장을 설치할 수 하는 경우에 tooback hello VM 계속 합니다. 이러한 유형의 백업 오프 라인 VM 이라고 하며 hello 복구 지점은 *크래시 일관성이 있는*합니다.

## <a name="troubleshooting-information"></a>문제 해결 정보
이 문서에서 hello 작업을 수행 하는 문제를 사용 하는 경우 참조는 [문제 해결 지침](backup-azure-vms-troubleshoot.md)합니다.

## <a name="pricing"></a>가격
Azure Vm 백업의 hello 비용 hello 보호 된 인스턴스 수를 기반으로 합니다. 보호된 인스턴스에 대한 정의는 [보호된 인스턴스란 무엇인가요?](backup-introduction-to-azure-backup.md#what-is-a-protected-instance)를 참조하세요. 가상 컴퓨터를 백업 hello 비용 계산의 예제를 보려면 [보호 된 인스턴스 계산 되는 방식을](backup-azure-vms-introduction.md#calculating-the-cost-of-protected-instances)합니다. Azure 백업 가격 hello 참조에 대 한 정보에 대 한 페이지 [백업 가격](https://azure.microsoft.com/pricing/details/backup/)합니다.

## <a name="questions"></a>질문이 있으십니까?
기능의 경우 원하는 toosee 포함 또는 질문이 있는 경우 [피드백](http://aka.ms/azurebackup_feedback)합니다.
