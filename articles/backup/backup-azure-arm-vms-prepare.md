---
title: "Azure 백업: tooback 가상 컴퓨터를 준비 | Microsoft Docs"
description: "환경이 Azure의 가상 컴퓨터를 백업할 준비가 되었는지 확인합니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "백업; 백업;"
ms.assetid: e87e8db2-b4d9-40e1-a481-1aa560c03395
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 5c3a41b5d3bd56e62ca5f207442867913aa99816
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-environment-tooback-up-resource-manager-deployed-virtual-machines"></a>사용자 환경 tooback 리소스 관리자를 통해 배포 된 가상 컴퓨터를 준비 합니다.
> [!div class="op_single_selector"]
> * [Resource Manager 모델](backup-azure-arm-vms-prepare.md)
> * [클래식 모델](backup-azure-vms-prepare.md)
>
>

이 문서는 사용자 환경 tooback 리소스 관리자를 통해 배포 된 가상 컴퓨터 (VM)를 준비 하기 위한 hello 단계를 제공 합니다. hello 단계 hello 프로시저 사용 하 여 hello Azure 포털에에서 표시 된 것입니다.  

hello Azure 백업 서비스에는 두 가지 유형의 Vm을 보호 하기 위한 (백업 자격 증명 모음 및 복구 서비스 자격 증명 모음) 자격 증명 모음에 있습니다. 백업 자격 증명 모음 hello 클래식 배포 모델을 사용 하 여 배포 된 Vm을 보호 합니다. 복구 서비스 자격 증명 모음은 **클래식으로 배포되거나 Resource Manager 배포 VM을 양쪽 모두** 보호합니다. 복구 서비스 자격 증명 모음 tooprotect 리소스 관리자를 통해 배포 된 VM을 사용 해야 합니다.

> [!NOTE]
> Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델인 [리소스 관리자와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)모델이 있습니다. 참조 [Azure 가상 컴퓨터를 사용자 환경 tooback 준비](backup-azure-vms-prepare.md) 클래식 배포 작업에 대 한 자세한 내용은 Vm을 모델링 합니다.
>
>

Resource Manager 배포 VM(가상 컴퓨터)을 보호하거나 백업할 수 있으려면, 다음과 같은 필수 구성 요소가 있어야 합니다.

* 복구 서비스 자격 증명 모음 만들기 (또는 식별 된 기존 복구 서비스 자격 증명 모음) *hello에 VM와 동일한 위치*합니다.
* 시나리오를 선택 하 고 hello 백업 정책 정의 항목 tooprotect를 정의 합니다.
* 가상 컴퓨터에서 VM 에이전트의 hello 설치를 확인 합니다.
* 네트워크 연결 확인
* Linux Vm에 대 한 toocustomize를 원하는 경우에 응용 프로그램 일치 백업에 대 한 백업 환경을 따르십시오 hello [단계 tooconfigure 스냅숏 전 및 후 스크립트를 스냅숏](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent)

이러한 조건에서 이미 환경에 존재 하 다음 toohello 진행을 알고 있는 경우 [VMs 문서를 백업](backup-azure-vms.md)합니다. 이러한 필수 구성이 요소를 모두 선택 하거나, tooset 필요한 경우이 문서 안내 합니다 hello 단계 tooprepare 필수 조건이 있습니다.

##<a name="supported-operating-system-for-backup"></a>지원되는 백업용 운영 체제
 * **Linux**: Azure Backup은 Core OS Linux를 제외한 [Azure 인증 배포 목록](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 지원합니다. _도 하 게 다른 Bring-Your-소유-Linux 배포판 hello VM 에이전트는 hello 가상 컴퓨터에서 사용할 수 있는 정상적으로 작동 못할 수도 있으며 Python에 대 한 지원. 그러나 이러한 배포판을 백업에 대해서는 보증하지 않습니다._
 * **Windows Server**: Windows Server 2008 R2 이전 버전은 지원되지 않습니다.

## <a name="limitations-when-backing-up-and-restoring-a-vm"></a>VM 백업 및 복원 시의 제한 사항
환경을 준비 하기 전에 hello 제한 사항을 이해 해야 합니다.

* 16개 이상의 데이터 디스크가 있는 가상 컴퓨터의 백업은 지원되지 않습니다.
* 데이터 디스크 크기가 1023GB보다 큰 가상 컴퓨터를 백업하는 것은 지원되지 않습니다.
* 예약된 IP 주소가 있고 정의된 끝점이 없는 가상 컴퓨터의 백업은 지원되지 않습니다.
* 방금 BEK를 사용하여 암호화된 VM의 백업을 지원하지 않습니다. LUKS를 사용하여 암호화된 Linux VM의 백업을 지원하지 않습니다.
* 규모 확장 파일 서버 구성에서 VM을 백업하는 것은 권장되지 않습니다.
* 백업 데이터는 탑재 된 네트워크 연결 된 드라이브 tooVM 포함 되지 않습니다.
* 복원하는 동안 기존 가상 컴퓨터의 교체는 지원되지 않습니다. Hello VM 있을 때 toorestore hello VM을 가져오려고 하면 hello 복원 작업이 실패 합니다.
* 지역 간 백업 및 복원은 지원되지 않습니다.
* Azure의 모든 공용 영역에서 가상 컴퓨터를 백업할 수 있습니다 (hello 참조 [검사 목록](https://azure.microsoft.com/regions/#services) 지원 되는 지역). 원하는 hello 영역 지원 되지 않는 오늘 경우 자격 증명 모음을 만드는 동안 hello 드롭다운 목록에서 표시 되지 않습니다.
* 다중 DC 구성의 일부인 도메인 컨트롤러(DC) VM 복원은 PowerShell을 통해서만 지원됩니다. [다중 DC 도메인 컨트롤러 복원](backup-azure-restore-vms.md#restoring-domain-controller-vms)에 대해 자세히 알아보세요.
* 특수 한 네트워크 구성을 따르고 hello에 있는 가상 컴퓨터를 복원 PowerShell 통해만 지원 됩니다. Hello hello 복원 워크플로 사용 하 여 만든 Vm hello 복원 작업이 완료 된 후 UI가 이러한 구성을는 하지 않습니다. toolearn 더 참조 [특수 한 네트워크 구성으로 복원 Vm](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations)합니다.
  * 부하 분산 장치 구성에서의 가상 컴퓨터(내부 및 외부)
  * 다중의 예약된 IP 주소가 있는 가상 컴퓨터
  * 다중 네트워크 어댑터가 있는 가상 컴퓨터

## <a name="create-a-recovery-services-vault-for-a-vm"></a>VM에 대한 복구 서비스 자격 증명 모음 만들기
복구 서비스 자격 증명 모음에는 hello 백업 및 시간에 따라 생성 된 복구 지점을 저장 하는 엔터티입니다. hello 복구 서비스 자격 증명 모음에는 hello 보호 된 가상 컴퓨터와 연결 된 hello 백업 정책을 포함 되어 있습니다.

toocreate 복구 서비스 자격 증명 모음:

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. Hello 허브 메뉴에서 클릭 **찾아보기** hello 리소스 목록에 입력 하 고 **복구 서비스**합니다. Hello 목록이 필터링 됩니다 입력을 시작 하면 사용자의 입력에 기반 합니다. **복구 서비스 자격 증명 모음**을 클릭합니다.

    ![복구 서비스를 hello 찾아보기 단추를 클릭 합니다. Hello 복구 서비스 자격 증명 모음에 옵션 단추를 클릭 tooopen hello 표시 되 면 블레이드 복구 서비스 자격 증명 모음입니다.](./media/backup-azure-arm-vms-prepare/browse-to-rs-vaults-updated.png) <br/>

    복구 서비스 자격 증명 모음 hello 목록이 표시 됩니다.
3. Hello에 **복구 서비스 자격 증명 모음** 메뉴를 클릭 하 여 **추가**합니다.

    ![복구 서비스 자격 증명 모음 만들기 2단계](./media/backup-azure-arm-vms-prepare/rs-vault-menu.png)

    hello 복구 서비스 자격 증명 모음에 블레이드에서 열립니다 tooprovide 묻는 **이름**, **구독**, **리소스 그룹**, 및 **위치**합니다.

    ![복구 서비스 자격 증명 모음 만들기 5단계](./media/backup-azure-arm-vms-prepare/rs-vault-attributes.png)
4. 에 대 한 **이름**, 이름 tooidentify hello 자격 증명 모음을 입력 합니다. hello 이름이 필요 toobe 고유 hello Azure 구독에 대 한 합니다. 이름을 2~50자 사이로 입력합니다. 문자로 시작해야 하며, 문자, 숫자, 하이픈만 사용할 수 있습니다.
5. 클릭 **구독** toosee hello 사용 가능한 구독 목록입니다. 어떤 구독이 toouse 해야 할지 잘 모를 경우 hello 기본값을 사용 하 여 (또는 제안) 구독 합니다. 조직 계정이 여러 Azure 구독과 연결된 경우에만 여러 항목을 선택할 수 있습니다.
6. 클릭 **리소스 그룹** toosee 리소스 그룹의 사용 가능한 목록 hello 하거나 클릭 **새로** toocreate 새 리소스 그룹입니다. 리소스 그룹에 대한 전체 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.
7. 클릭 **위치** tooselect hello hello 자격 증명 모음에 대 한 지리적 영역입니다. hello 자격 증명 모음 **해야** hello에 원하는 tooprotect hello 가상 컴퓨터와 동일한 영역입니다.

   > [!IMPORTANT]
   > VM 존재 하는 hello 위치의 확실 하지 않은, hello 자격 증명 모음 만들기 대화 상자를 닫은 hello 포털에서 가상 컴퓨터의 toohello 목록을 이동 합니다. 가상 컴퓨터를 여러 지역에 있으면 각 지역에 복구 서비스 자격 증명 모음 toocreate를 해야 합니다. Toohello 다음 위치를 진행 하기 전에 hello 첫 번째 위치에 hello 자격 증명 모음을 만듭니다. 필요 toospecify 저장소 계정이 없습니다 toostore hello 백업 데이터-hello 복구 서비스 자격 증명 모음 없으며 hello Azure 백업 서비스가를 자동으로 처리 합니다.
   >
   >

8. **만들기**를 클릭합니다. 복구 서비스 자격 증명 모음에 만든 toobe hello에 대 한 시간이 걸릴 수 있습니다. Hello hello 포털의 상단 오른쪽 영역에서 상태 알림 hello를 모니터링 합니다. 자격 증명 모음을 만든 후의 복구 서비스 자격 증명 모음 hello 목록에 나타납니다. 자격 증명 모음이 보이지 않으면 **새로 고침**을 클릭합니다.

    ![백업 자격 증명 모음 목록](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

    자격 증명 모음을 만든 했으므로 tooset 저장소 복제 hello 하는 방법을 알아봅니다.

## <a name="set-storage-replication"></a>저장소 복제 설정
hello 저장소 복제 옵션 지역 중복 저장소와 로컬 중복 저장소는 toochoose가 있습니다. 기본적으로 사용자 자격 증명 모음에는 지역 중복 저장소가 있습니다. 이것이 기본 백업 hello 옵션 집합 toogeo 중복 저장소를 둡니다. 오래 지속되지 않는 저렴한 옵션을 원하는 경우에는 로컬 중복 저장소를 선택합니다.

tooedit hello 저장소 복제 설정입니다.

1. Hello에 **복구 서비스 자격 증명 모음** 블레이드에서 자격 증명 모음을 선택 합니다.
    자격 증명 모음을 클릭할 때 hello 설정 블레이드에서 (*hello hello 자격 증명 모음의 이름을 hello 위쪽에 있는*) hello 자격 증명 모음을 세부적으로 블레이드에서 열립니다.

    ![백업 자격 증명 모음의 hello 목록에서 자격 증명 모음을 선택 합니다.](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)

2. Hello에 **설정** 블레이드를 사용 하 여 hello 세로 슬라이더 tooscroll toohello 아래로 **관리** 섹션. 클릭 **백업 인프라** tooopen 리라 합니다. Hello에 **일반** 섹션 클릭 **백업 구성** tooopen 리라 합니다. Hello에 **백업 구성** 블레이드에서 자격 증명 모음에 대 한 hello 저장소 복제 옵션을 선택 합니다. 기본적으로 사용자 자격 증명 모음에는 지역 중복 저장소가 있습니다. Hello 저장소 복제 유형을 변경 하면 클릭 **저장**합니다.

    ![백업 자격 증명 모음 목록](./media/backup-azure-arm-vms-prepare/full-blade.png)

     Azure를 기본 백업 저장소 끝점으로 사용하는 경우 계속해서 지역 중복 저장소를 사용합니다. Azure를 주가 아닌 백업 저장소 끝점으로 사용하는 경우 로컬 중복 저장소를 선택합니다. 에 대해 자세히 알아보세요 [지리적 중복](../storage/common/storage-redundancy.md#geo-redundant-storage) 및 [로컬 중복](../storage/common/storage-redundancy.md#locally-redundant-storage) hello에 대 한 저장소 옵션 [Azure 저장소 복제 개요](../storage/common/storage-redundancy.md)합니다.
    자격 증명 모음에 대 한 hello 저장소 옵션을 선택한 후 hello 자격 증명 모음과 준비 tooassociate hello VM 됩니다. toobegin hello 연결 하면 검색 하 고 하는지 등록 hello Azure 가상 컴퓨터.

## <a name="select-a-backup-goal-set-policy-and-define-items-tooprotect"></a>백업 목표를 선택 하 고 정책 설정 항목 tooprotect 정의
자격 증명 모음으로 VM을 등록 하기 전에 실행 hello 검색 프로세스 tooensure toohello 구독에 추가 된 모든 새 가상 컴퓨터를 식별 됩니다. 추가 정보와 함께 hello 구독에서 가상 컴퓨터의 hello 목록에 대 한 hello 프로세스 쿼리 Azure hello 클라우드 서비스 이름 및 hello 영역 같은입니다. Hello Azure 포털, 시나리오는 toowhat hello 복구 서비스 자격 증명 모음에 tooput는 것을 의미 합니다. 정책에는 복구 지점을 수행 빈도 및 시기에 대 한 hello 일정입니다. 또한 정책은 hello 복구 지점에 대 한 hello 보존 범위를 포함합니다.

1. 복구 서비스 자격 증명 모음 열고 이미 있는 경우 2 toostep을 진행 합니다. 복구 서비스 자격 증명 모음 열이 없는 경우 다음 hello 엽니다 [Azure 포털](https://portal.azure.com/) hello 허브 메뉴에서를 클릭 하 고 **더 많은 서비스**합니다.

   * Hello 리소스 목록에 입력 **복구 서비스**합니다.
   * Hello 목록이 필터링 됩니다 입력을 시작 하면 사용자의 입력에 기반 합니다. **복구 서비스 자격 증명 모음**이 표시되면 클릭합니다.

     ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-azure-arm-vms-prepare/browse-to-rs-vaults-updated.png) <br/>

     복구 서비스 자격 증명 모음 hello 목록이 표시 됩니다. 구독에 자격 증명 모음이 없으면 이 목록은 비어 있습니다.

    ![Hello 복구 서비스의 보기 목록 자격 증명 모음](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

   * 복구 서비스 자격 증명 모음 hello 목록에서 자격 증명 모음 tooopen 대시보드를 선택 합니다.

     hello 설정 블레이드 및 hello hello 선택한 자격 증명 모음, 열립니다에 대 한 대시보드를 자격 증명 모음입니다.

     ![자격 증명 모음 블레이드 열기](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)
2. Hello 자격 증명 모음 대시보드 메뉴를 클릭 **백업** tooopen hello 백업 블레이드입니다.

    ![백업 블레이드 열기](./media/backup-azure-arm-vms-prepare/backup-button.png)

    hello 백업 및 백업 목표 블레이드를 엽니다.

    ![시나리오 블레이드 열기](./media/backup-azure-arm-vms-prepare/select-backup-goal-1.png)

3. Hello 백업 목표 블레이드에서 설정 **여기서 작업이 실행 되는** tooAzure 및 **어떻게 하 시겠습니까 toobackup 원하는** tooVirtual 클릭 한 다음 컴퓨터을 **확인**합니다.

    이 VM 확장 hello hello 자격 증명 모음에 등록합니다. hello 블레이드를 닫고 백업 목표 및 hello **백업 정책** 블레이드를 엽니다.

    ![시나리오 블레이드 열기](./media/backup-azure-arm-vms-prepare/select-backup-goal-2.png)
4. Hello 백업 정책 블레이드에서 hello 백업 정책을 원하는 tooapply toohello 자격 증명 모음을 선택 합니다.

    ![백업 정책 선택](./media/backup-azure-arm-vms-prepare/setting-rs-backup-policy-new.png)

    hello 기본 정책의 hello 세부 정보는 hello 드롭 다운 메뉴 아래에 나열 됩니다. 새 정책을 toocreate 선택 **새로 만들기** hello 드롭 다운 메뉴에서 합니다. 백업 정책 정의에 대한 지침은 [백업 정책 정의](backup-azure-vms-first-look-arm.md#defining-a-backup-policy)를 참조하세요.
    클릭 **확인** tooassociate hello 백업 정책을 hello 자격 증명 모음입니다.

    백업 정책 블레이드 닫히고 hello hello **가상 컴퓨터 선택** 블레이드를 엽니다.
5. Hello에 **가상 컴퓨터 선택** 블레이드에서 hello로 가상 컴퓨터 tooassociate hello 정책 지정 및 클릭 선택 **확인**합니다.

    ![워크로드 선택](./media/backup-azure-arm-vms-prepare/select-vms-to-backup.png)

    가상 컴퓨터를 선택 하는 hello 유효성이 검사 됩니다. Toosee 예상 했던 hello 가상 컴퓨터를 표시 되지 않으면 다른 자격 증명 모음에서 보호 되는 동일한 Azure 복구 서비스 자격 증명 모음 및 아직 hello 위치 hello에 존재 하는지 확인 합니다. 복구 서비스 자격 증명 모음에 hello의 hello 위치 hello 자격 증명 모음 대시보드에 표시 됩니다.

6. 이제 hello 자격 증명 모음에 대 한 모든 설정을 정의한 hello 백업 블레이드에서에서 클릭 **백업 사용**합니다. Hello 정책 toohello 자격 증명 모음 및 hello Vm에 배포 합니다. Hello 가상 컴퓨터에 대 한 hello 초기 복구 지점을 만들지 않습니다.

    ![백업 사용](./media/backup-azure-arm-vms-prepare/vm-validated-click-enable.png)

Hello 백업을 성공적으로 활성화 한 다음 백업 정책 일정에 따라 실행 됩니다. 원하는 경우 toogenerate hello 가상 컴퓨터를 주문형으로 백업 작업 tooback는 이제, 참조 [Triggering hello 백업 작업](./backup-azure-arm-vms.md#triggering-the-backup-job)합니다.

Hello 가상 컴퓨터를 등록 하는 데 문제가 있으면 hello hello VM 에이전트를 설치 하는 방법 및 네트워크 연결에 다음 정보를 참조 하십시오. 아마도 hello Azure에서 만든 가상 컴퓨터를 보호 하는 경우 다음 정보를 필요 하지 않습니다. 그러나 Azure에 가상 컴퓨터를 마이그레이션하는 경우 다음 해야 hello VM 에이전트 및 가상 컴퓨터 hello 가상 네트워크와 통신할 수 있는지를 올바로 설치 합니다.

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Hello 가상 컴퓨터에 hello VM 에이전트 설치
Azure VM 에이전트 hello hello 백업 확장 toowork hello에 대 한 Azure 가상 컴퓨터에 설치 되어야 합니다. Hello Azure 갤러리에서에서 VM을 만든 경우 VM 에이전트가 hello는 hello 가상 컴퓨터에 이미 있습니다. 여기서는 hello 상황에 대 한이 정보는 제공 *하지* hello Azure 갤러리에서에서 만들어진 VM을 사용 하는 온-프레미스 데이터 센터에서 VM을 마이그레이션한 예를 들어-합니다. 이 경우 hello VM 에이전트 toobe 순서 tooprotect hello 가상 컴퓨터에 설치 해야 합니다. Hello에 대 한 자세한 내용은 [VM 에이전트](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux)합니다.

Azure VM 에이전트 hello 검사 hello 가상 컴퓨터에 제대로 설치 hello Azure VM을 백업 하는 데 문제가 있으면 (아래 hello 표 참조). 다음 표에서 hello hello VM 에이전트에 대 한 Windows 및 Linux Vm에 대 한 추가 정보를 제공 합니다.

| **작업** | **Windows** | **Linux** |
| --- | --- | --- |
| Hello VM 에이전트를 설치합니다. |다운로드 및 설치 hello [에이전트 MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)합니다. 관리자 권한 toocomplete hello 설치를 해야 합니다. |<li> Hello 최신 설치 [Linux 에이전트](../virtual-machines/linux/agent-user-guide.md)합니다. 관리자 권한 toocomplete hello 설치를 해야 합니다. 리포지토리에서 배포 에이전트를 설치하는 것이 좋습니다. GitHub에서 직접 Linux VM 에이전트를 설치하는 것은 **좋지 않습니다**.  |
| Hello VM 에이전트를 업데이트합니다. |업데이트 hello VM 에이전트를 다시 설치 하는 hello [VM 에이전트 이진 파일](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)합니다. <br>Hello VM 에이전트를 업데이트 하는 동안 백업 작업이 수행 되지 실행 되 고 있는지 확인 합니다. |Hello 지침에 따라 [Linux VM 에이전트를 hello 업데이트](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. 리포지토리에서 배포 에이전트를 업데이트하는 것이 좋습니다. GitHub에서 직접 Linux VM 에이전트를 업데이트하는 것은 **좋지 않습니다**.<br>백업 작업이 수행 되지 hello VM 에이전트를 업데이트 하는 동안 실행 되 고 있는지 확인 합니다. |
| Hello VM 에이전트 설치 유효성 검사 |<li>Toohello 이동 *C:\WindowsAzure\Packages* hello Azure VM에서에서 폴더입니다. <li>Hello WaAppAgent.exe 파일이 없는 찾아야 합니다.<li> Hello 파일을 마우스 오른쪽 단추로 클릭 한 다음 너무 이동 하십시오**속성**를 선택한 후 hello **세부 정보** 탭 hello 제품 버전 필드 2.6.1198.718 이루어져야 합니다. 이상. |해당 없음 |

### <a name="backup-extension"></a>백업 확장
한 번 hello 가상 컴퓨터를 hello Azure 백업 서비스에 VM 에이전트가 설치 되어 hello hello 예비 내선 번호 toohello VM 에이전트를 설치 합니다. hello Azure 백업 서비스에 원활 하 게 업그레이드 및 패치 hello 예비 내선 번호입니다.

hello 예비 내선 번호 hello VM에서 실행 되 고 여부 hello 백업 서비스에 의해 설치 됩니다. 실행 중인 VM 응용 프로그램 일치 복구 지점의 얻을의 hello 가장 큰 기회를 제공 합니다. 그러나 hello Azure 백업 서비스를 해제 되어 있으면 및 hello 확장을 설치할 수 하는 경우에 tooback hello VM 계속 합니다. 오프라인 VM이라고 합니다. 이 경우 hello 복구 지점 수는 *크래시 일관성이 있는*합니다.

## <a name="network-connectivity"></a>네트워크 연결
순서 toomanage hello VM 스냅숏 백업 확장 hello 필요 연결 toohello Azure 공용 IP 주소입니다. Hello 오른쪽 인터넷에 연결 하지 않고 hello 가상 컴퓨터의 HTTP 요청 시간 제한 및 hello 백업 작업이 실패합니다. 배포에 액세스 제한이 있다면(예: 네트워크 보안 그룹(NSG)을 통해), 백업 트래픽에 대해 명확한 경로를 제공하기 위해 이 옵션 중 하나를 선택합니다.

* [화이트 리스트 hello Azure 데이터 센터 IP 범위](http://www.microsoft.com/en-us/download/details.aspx?id=41653) -어떻게 toowhitelist hello IP 주소에 대 한 지침은 hello 문서를 참조 합니다.
* 트래픽 라우팅을 위해 HTTP 프록시 서버를 배포합니다.

어떤 옵션 toouse를 결정할 때는 hello 장단점은 관리 효율성, 세분화 된 제어 및 비용 까지입니다.

| 옵션 | 장점 | 단점 |
| --- | --- | --- |
| 허용 목록 IP 범위 |추가 비용 없음<br><br>NSG에 대 한 액세스를 열기 위한 hello를 사용 하 여 <i>집합 AzureNetworkSecurityRule</i> cmdlet. |시간에 따른 영향을 받음 hello IP 범위 변경으로 복잡 한 toomanage 합니다.<br><br>Azure 및 뿐 아니라 저장소의 toohello 전체 액세스를 제공합니다. |
| HTTP 프록시 |Url 허용 hello 저장소 hello 프록시에 세부적으로 제어 합니다.<br>단일 지점 인터넷 액세스 tooVMs 합니다.<br>IP 주소 변경 내용을 tooAzure 대상이 아닙니다. |Hello 프록시 소프트웨어와 함께 VM을 실행 하기 위한 추가 비용이 있습니다. |

### <a name="whitelist-hello-azure-datacenter-ip-ranges"></a>화이트 리스트 hello Azure 데이터 센터 IP 범위
toowhitelist hello Azure 데이터 센터 IP 범위를 참조 하십시오. hello [Azure 웹 사이트](http://www.microsoft.com/en-us/download/details.aspx?id=41653) hello IP 범위 및 지침에 대 한 자세한 내용은 합니다.

### <a name="using-an-http-proxy-for-vm-backups"></a>VM 백업에 HTTP 프록시 사용
VM을 백업할 때 hello VM에 예비 내선 번호 hello hello 스냅숏 관리 명령을 tooAzure HTTPS API를 사용 하 여 저장소를 보냅니다. 액세스 toohello에 대해 구성 된 hello 유일한 구성 요소 이므로 hello HTTP 프록시를 통해 hello 예비 내선 번호 트래픽을 라우팅할 공용 인터넷 합니다.

> [!NOTE]
> 사용 해야 하는 hello 프록시 소프트웨어에 대 한 권장 사항 없음 있습니다. 다음 hello 구성 단계와 호환 되는 프록시를 선택 하면 확인 합니다.
>
>

아래 예제에서는 이미지 hello hello 세 가지 구성 단계가 필요한 toouse HTTP 프록시를 보여 줍니다.

* 응용 프로그램 VM 경로 대 한 모든 HTTP 트래픽이 바인딩된 hello 공용 인터넷을 통해 프록시 VM입니다.
* 프록시 VM hello 가상 네트워크의 Vm에서 들어오는 트래픽을 허용합니다.
* hello 그룹 NSG (네트워크 보안) 라는 NSF 잠금에는 보안 규칙 아웃 바운드 인터넷 트래픽을 허용 프록시 VM에서 필요 합니다.

![HTTP 프록시 배포 다이어그램을 사용하는 NSG](./media/backup-azure-vms-prepare/nsg-with-http-proxy.png)

toouse HTTP 프록시 toocommunicating toohello 공용 인터넷을 다음이 단계를 수행 합니다.

#### <a name="step-1-configure-outgoing-network-connections"></a>1단계. 나가는 네트워크 연결 구성
###### <a name="for-windows-machines"></a>Windows 컴퓨터의 경우
로컬 시스템 계정에 대한 프록시 서버 구성을 설정합니다.

1. [PsExec](https://technet.microsoft.com/sysinternals/bb897553)
2. 관리자 권한 프롬프트에서 다음 명령을 실행합니다.

     ```
     psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe"
     ```
     Internet Explorer 창이 열립니다.
3. 이동 tooTools-> 인터넷 옵션-> 연결-> LAN 설정 합니다.
4. 시스템 계정에 대한 프록시 설정을 확인합니다. 프록시 IP 및 포트를 설정합니다.
5. Internet Explorer를 닫습니다.

시스템 수준의 프록시 구성을 설정하고 나가는 HTTP/HTTPS 트래픽에 사용됩니다.

설치 프로그램 프록시 서버에 있으면 현재 사용자 계정 (로컬 시스템 계정이 아닌 함)를 사용 하 여 hello 스크립트 tooapply 다음 해당 tooSYSTEMACCOUNT:

```
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name DefaultConnectionSettings -Value $obj.DefaultConnectionSettings
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name SavedLegacySettings -Value $obj.SavedLegacySettings
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name ProxyEnable -Value $obj.ProxyEnable
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name Proxyserver -Value $obj.Proxyserver
```

> [!NOTE]
> 프록시 서버 로그에 "(407)프록시 인증 필요"가 발견되면, 인증이 제대로 설정되었는지 확인합니다.
>
>

###### <a name="for-linux-machines"></a>Linux 컴퓨터의 경우
다음 줄 toohello hello 추가 ```/etc/environment``` 파일:

```
http_proxy=http://<proxy IP>:<proxy port>
```

다음 줄 toohello hello 추가 ```/etc/waagent.conf``` 파일:

```
HttpProxy.Host=<proxy IP>
HttpProxy.Port=<proxy port>
```

#### <a name="step-2-allow-incoming-connections-on-hello-proxy-server"></a>2단계. Hello 프록시 서버에서 들어오는 연결을 허용 합니다.
1. Hello 프록시 서버에서 Windows 방화벽을 엽니다. hello 가장 쉬운 방법은 tooaccess hello 방화벽은 고급 보안이 포함 된 Windows 방화벽에 대 한 toosearch입니다.

    ![Hello 방화벽을 열으십시오](./media/backup-azure-vms-prepare/firewall-01.png)
2. Hello Windows 방화벽 대화 상자에서 마우스 오른쪽 단추로 클릭 **인바운드 규칙** 클릭 **새 규칙...** .

    ![새 규칙 만들기](./media/backup-azure-vms-prepare/firewall-02.png)
3. Hello에 **새 인바운드 규칙 마법사**, hello 선택 **사용자 지정** hello에 대 한 옵션 **규칙 유형** 클릭 **다음**합니다.
4. Hello 페이지 tooselect hello에 **프로그램**, 선택 **모든 프로그램** 클릭 **다음**합니다.
5. Hello에 **프로토콜 및 포트** 페이지 hello 다음 정보를 입력 하 고 클릭 **다음**:

    ![새 규칙 만들기](./media/backup-azure-vms-prepare/firewall-03.png)

   * *프로토콜 유형*에서 *TCP*를 선택합니다.
   * 에 대 한 *로컬 포트* 선택 *특정 포트*, 아래의 hello 필드에 지정 hello ```<Proxy Port>``` 구성 된 합니다.
   * *원격 포트*에서 *모든 포트*를 선택합니다.

     Hello 마법사의 나머지에서는 hello 모든 hello 방식으로 toohello 종료를 클릭 하 고이 규칙 이름을 지정 합니다.

#### <a name="step-3-add-an-exception-rule-toohello-nsg"></a>3단계. 예외 규칙 toohello NSG를 추가 합니다.
Azure PowerShell 명령 프롬프트를 hello 다음 명령을 입력 합니다.

다음 명령을 hello 예외 toohello NSG를 추가 합니다. 이 예외 10.0.0.5에서 모든 포트에서의 TCP 트래픽을 허용 tooany 포트 80 (HTTP) 또는 443 (HTTPS)에 대 한 인터넷 주소입니다. 특정 포트가 필요한 경우 hello 공용 인터넷을 toohello 포트 있는지 tooadd 수 ```-DestinationPortRange``` 도 합니다.

```
Get-AzureNetworkSecurityGroup -Name "NSG-lockdown" |
Set-AzureNetworkSecurityRule -Name "allow-proxy " -Action Allow -Protocol TCP -Type Outbound -Priority 200 -SourceAddressPrefix "10.0.0.5/32" -SourcePortRange "*" -DestinationAddressPrefix Internet -DestinationPortRange "80-443"
```


*이 단계에서는 이 예제에 대해 특정 이름과 값을 사용합니다. 프로그램 배포를 입력할 때 또는 잘라내기 및 붙여넣기 세부 정보를 코드에 대 한 hello 이름 및 값을 사용 하십시오.*

네트워크 연결을 설정한 파악 했으므로 VM을 준비 tooback 됩니다. [Resource Manager 배포 VM 백업](backup-azure-arm-vms.md)을 참조하세요.

## <a name="questions"></a>질문이 있으십니까?
기능의 경우 원하는 toosee 포함 또는 질문이 있는 경우 [피드백](http://aka.ms/azurebackup_feedback)합니다.

## <a name="next-steps"></a>다음 단계
VM를 백업 하기 위한 환경을 준비 했으면, 했으므로 다음 논리 단계는 toocreate 백업 합니다. 문서를 계획 하는 hello Vm을 백업 하는 방법에 대 한 자세한 정보를 제공 합니다.

* [가상 컴퓨터 설정](backup-azure-vms.md)
* [VM 백업 인프라 계획](backup-azure-vms-introduction.md)
* [가상 컴퓨터 백업 관리](backup-azure-manage-vms.md)
