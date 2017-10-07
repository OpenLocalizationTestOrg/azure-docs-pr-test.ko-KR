---
title: "Azure 백업: hello Azure 포털을 사용 하 여 가상 컴퓨터를 복원 | Microsoft Docs"
description: "Azure 포털을 사용하여 복구 지점에서 Azure 가상 컴퓨터 복원"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "백업으로 복원 어떻게 toorestore; 복구 지점입니다."
ms.assetid: 372b87c6-3544-4dc5-bbc9-c742ca502159
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: f4f75d1da73c7760d2952afe80ff94918a08351c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-toorestore-virtual-machines"></a>Azure 포털 toorestore 가상 컴퓨터를 사용 하 여
> [!div class="op_single_selector"]
> * [클래식 포털에서 VM 복원](backup-azure-restore-vms.md)
> * [Azure 포털에서 VM 복원](backup-azure-arm-restore-vms.md)
>
>

정의된 간격으로 데이터의 스냅숏을 찍어 데이터를 보호합니다. 이러한 스냅숏은 복구 지점이라고 하며 복구 서비스 자격 증명 모음에 저장됩니다. 하는 경우 또는 필요한 toorepair 또는 VM을 다시 작성 시에 복구 지점을 저장 하는 hello 중 어디에서 든 hello VM을 복원할 수 있습니다. 복구 지점을 복원 하는 경우 백업 VM의 지정 시간 표현인 새 VM을 만들 또는 디스크를 복원 하 수 함께 제공 되는 hello 서식 파일을 사용 하 여 toocustomize hello VM을 복원 하거나 개별 파일 복구를 수행 합니다. 이 문서에서는 설명 방법을 toorestore VM tooa 새 VM 또는 복원 된 모든 백업 된 디스크. 개별 파일 복구에 대 한 참조 너무[Azure VM 백업에서 파일을 복구 합니다.](backup-azure-restore-files-from-vm.md)

![3-ways-restore-from-vm-backup](./media/backup-azure-arm-restore-vms/azure-vm-backup-restore.png)

> [!NOTE]
> Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델인 [리소스 관리자와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)모델이 있습니다. 이 문서에서는 hello 리소스 관리자 모델을 사용 하 여 배포 된 Vm을 복원 하기 위한 hello 정보 및 절차를 제공 합니다.
>
>

VM 백업에서 VM 또는 모든 디스크를 복원하는 작업은 다음과 같은 두 가지 단계를 포함합니다.

1. 복원을 위해 복원 지점 선택
2. Hello를 선택 하면 형식을 복원-새 VM을 만들 복원 디스크 하 고 필수 매개 변수를 지정 합니다. 

## <a name="select-restore-point-for-restore"></a>복원을 위해 복원 지점 선택
1. Toohello 로그인 [Azure 포털](http://portal.azure.com/)
2. Azure 메뉴 hello 클릭 **찾아보기** hello 서비스 목록에서 입력 **복구 서비스**합니다. 서비스 목록이 hello 입력 toowhat를 조정 합니다. **복구 서비스 자격 증명 모음**이 표시되면 이를 선택합니다.

    ![복구 서비스 자격 증명 모음 열기](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    hello hello 구독에서 자격 증명 모음 목록이 표시 됩니다.

    ![복구 서비스 자격 증명 모음 목록](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
3. Hello 목록에서 선택 hello 자격 증명 모음 hello toorestore 원하는 VM 연관 됩니다. Hello 자격 증명 모음을 클릭 하면 해당 대시보드가 열립니다.

    ![복구 서비스 자격 증명 모음 목록](./media/backup-azure-arm-restore-vms/select-vault-open-vault-blade.png)
4. 이제 했으므로 hello 자격 증명 모음 대시보드에서. Hello에 **백업 항목** 타일을 클릭 하 여 **Azure 가상 컴퓨터** toodisplay hello Vm hello 자격 증명 모음과 연결 합니다.

    ![자격 증명 모음 대시보드](./media/backup-azure-arm-restore-vms/vault-dashboard.png)

    hello **백업 항목** 블레이드가 열리고 hello Azure 가상 컴퓨터 목록이 표시 됩니다.

    ![자격 증명 모음의 VM 목록](./media/backup-azure-arm-restore-vms/list-of-vms-in-vault.png)
5. Hello 목록에서 VM tooopen hello 대시보드를 선택 합니다. hello VM 대시보드 toohello hello 복원 지점 타일이 포함 된 모니터링 영역을 엽니다.

    ![자격 증명 모음의 VM 목록](./media/backup-azure-arm-restore-vms/vm-blade.png)
6. Hello VM 대시보드 메뉴를 클릭 **복원**

    ![자격 증명 모음의 VM 목록](./media/backup-azure-arm-restore-vms/vm-blade-menu-restore.png)

    hello 블레이드를 엽니다.

    ![복원 블레이드](./media/backup-azure-arm-restore-vms/restore-blade.png)
7. Hello에 **복원** 블레이드에서 클릭 **복원 지점을** tooopen hello **복원할 선택 지점** 블레이드입니다.

    ![복원 블레이드](./media/backup-azure-arm-restore-vms/recovery-point-selector.png)

    기본적으로 hello 대화는 지난 30 일 동안 hello에서 모든 복원 지점 표시 됩니다. 사용 하 여 hello **필터** hello tooalter hello는 시간 범위 복원 지점을 표시 합니다. 기본적으로, 모든 일관성의 복원 지점이 표시됩니다. 수정 **모든 복원 지점** tooselect 복원 지점의 특정 일관성을 필터링 합니다. 각 유형의 복원 지점에 대 한 자세한 내용은 참조 hello 설명은 [데이터 일관성](backup-azure-vms-introduction.md#data-consistency)합니다.  

   * **복원 지점 일관성** 은 다음을 선택합니다.
     * 충돌 일관성 복원 지점,
     * 응용 프로그램 일관성 복원 지점,
     * 파일 시스템 일관성 복원 지점,
     * 모든 복원 지점.  
8. 복원 지점을 선택하고 **확인**을 클릭합니다.

    ![복원 지점 선택](./media/backup-azure-arm-restore-vms/select-recovery-point.png)

    hello **복원** hello 복원 지점을 설정 블레이드를 보여 줍니다.

    ![복원 지점이 설정됨](./media/backup-azure-arm-restore-vms/recovery-point-set.png)
9. Hello에 **복원** 블레이드에서 **구성 복원** 복원 지점을 설정 된 후 자동으로 열립니다.

## <a name="choosing-a-vm-restore-configuration"></a>VM 복원 구성 선택
Hello 복원 지점을 선택 했으므로 복원 VM에 대 한 구성을 선택 합니다. Hello 구성에 대 한 선택 사항을 복원 VM toouse 됩니다: Azure 포털 또는 PowerShell입니다.

1. 가 아닌 이미 있는 경우 이동 toohello **복원** 블레이드입니다. 확인 한 [복원 지점을 선택](#select-restore-point-for-restore)를 클릭 하 고 **구성 복원** tooopen hello **복구 구성** 블레이드입니다.

    ![복구 구성 마법사가 설정됩니다](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard-recovery-type.png)
2. Hello에 **구성 복원** 블레이드에서 두 가지 옵션이 있습니다.
   * 전체 가상 컴퓨터 복원
   * 백업된 디스크 복원

포털은 복원된 VM에 대해 빨리 만들기 옵션을 제공합니다. PowerShell을 사용 하려는 경우 toocustomize hello VM 구성 또는의 일부로 생성 된 hello 리소스의 이름을 선택 하는 새 VM 만들기, 포털 toorestore 백업 또는 디스크 및 사용 하 여 PowerShell 명령 tooattach 해당 VM 구성 또는 사용 하 여 서식 파일의 toochoice입니다 제공 디스크 toocustomize hello 복원 된 VM을 복원 합니다. 참조 [특수 한 네트워크 구성 사용 하 여 VM을 복원](#restoring-vms-with-special-network-configurations) 방법에 대 한 자세한 내용은 toorestore 여러 Nic가 또는 부하 분산 장치 아래의 VM입니다. Windows VM에서 사용 하는 경우 [허브 라이선스](../virtual-machines/windows/hybrid-use-benefit-licensing.md), toorestore 디스크가 필요 하 고 toocreate hello VM 아래 지정 된 대로 PowerShell/템플릿을 사용 하 고 VM tooavail 허브를 만드는 동안 LicenseType "Windows_Server"으로 지정 하는 있는지 확인 복원 된 VM의 이점입니다. 
 
## <a name="create-a-new-vm-from-restore-point"></a>복원 지점에서 새 VM 만들기
없는 경우 이미 여기 [복원 지점을 선택](#restoring-vms-with-special-network-configurations) 계속 toocreating 복원에서 새 VM 하기 전에 지점입니다. Hello에 복원 지점을 선택한 후 **구성 복원** 블레이드를 입력 하거나 각 필드가 다음 hello에 대 한 값을 선택 합니다.

* **복원 유형** - 가상 컴퓨터를 만듭니다.
* **가상 컴퓨터 이름** -hello VM에 대 한 이름을 제공 합니다. (리소스 관리자를 통해 배포 된 VM)에 대 한 고유 toohello 리소스 그룹 또는 클라우드 서비스 (클래식 VM)에 대 한 hello 이름 이어야 합니다. Hello 구독에 이미 있는 경우에 hello 가상 컴퓨터를 바꿀 수 없습니다.
* **리소스 그룹** – 기존 리소스 그룹을 사용하거나 새 리소스 그룹을 만듭니다. 기존 VM을 복원 하는 경우에 새로운 클라우드 서비스의이 필드 toospecify hello 이름을 사용 합니다. 새 리소스 그룹/클라우드 서비스를 만드는 경우 hello 이름은 전역적으로 고유 해야 합니다. 일반적으로 클라우드 서비스 이름 hello 연관 된 공용 URL-예: [cloudservice]. cloudapp.net에 합니다. Toouse 이미 사용 하는 hello 클라우드 리소스 그룹/클라우드 서비스에 대 한 이름을 사용 하려는 경우 Azure 할당 hello 리소스 그룹/클라우드 서비스 VM hello 대로 이름이 같은 hello 합니다. Azure는 선호도 그룹에 연결되지 않은 리소스 그룹/클라우드 서비스 및 VM을 표시합니다. 자세한 내용은 참조 [어떻게 선호도 그룹 tooa 지역 가상 네트워크 (VNet)에서 toomigrate](../virtual-network/virtual-networks-migrate-to-regional-vnet.md)합니다.
* **가상 네트워크** -선택 hello 가상 네트워크 (VNET)을 만들 때 VM hello 합니다. hello 필드 hello 구독과 관련 된 모든 Vnet을 제공 합니다. Hello VM의 리소스 그룹은 괄호 안에 표시 됩니다.
* **서브넷** -hello VNET 서브넷, 경우 hello 첫 번째 서브넷이 기본적으로 선택 합니다. 추가 서브넷에 있는 경우 원하는 hello 서브넷을 선택 합니다.
* **저장소 계정** -이 메뉴에는 hello에 hello 저장소 계정을 나열 hello와 동일한 위치 복구 서비스 자격 증명 모음입니다. 영역이 중복된 저장소 계정은 지원되지 않습니다. 와 저장소 계정이 없습니다 hello hello와 동일한 위치 복구 서비스 자격 증명 모음 면 hello 복원 작업을 시작 하기 전에 하나 만들어야 합니다. 괄호 안에 hello 저장소 계정 복제 형식이 언급 되어 있습니다.

![복원 구성 마법사가 설정됨](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard.png)

> [!NOTE]
> 1. Resource Manager 배포 VM을 복원하는 경우 VNET(가상 네트워크)을 식별해야 합니다. 클래식 VM의 경우 VNET(가상 네트워크)은 선택 사항입니다.
> 2. 관리 디스크를 사용하여 VM을 복원하는 경우 선택한 저장소 계정이 해당 수명 동안 SSE(저장소 서비스 암호화)에 대해 활성화되어 있지 않은지 확인하세요.
> 3. 저장소 계정 선택 (프리미엄 또는 표준)의 hello 저장소 형식에 기반을 복원 하는 모든 디스크 됩니다 프리미엄 또는 표준 디스크. 현재는 복원할 때 디스크 모드를 혼합해서 사용할 수 없습니다.  
>
>

Hello에 **구성 복원** 블레이드에서 클릭 **확인** toofinalize hello 구성 복원 합니다. Hello에 **복원** 블레이드에서 클릭 **복원** tootrigger hello 복원 작업입니다.

## <a name="restore-backed-up-disks"></a>백업된 디스크 복원
Toocustomize hello 가상 컴퓨터가 원하는 경우을에서 toocreate 구성 블레이드 선택에 보다 디스크 백업 **복원** 값 **복원 유형**합니다. 이렇게 선택하면 백업 디스크를 복사할 저장소 계정을 요청합니다. 저장소 계정의 선택할 때는 공유 hello 복구 서비스 자격 증명 모음으로 같은 위치 hello는 계정을 선택 합니다. 영역이 중복된 저장소 계정은 지원되지 않습니다. 와 저장소 계정이 없습니다 hello hello와 동일한 위치 복구 서비스 자격 증명 모음 면 hello 복원 작업을 시작 하기 전에 하나 만들어야 합니다. 괄호 안에 hello 저장소 계정 복제 형식이 언급 되어 있습니다.

복원 작업이 완료된 후에 다음을 수행할 수 있습니다.
* [사용 하 여 템플릿 toocustomize hello VM 복원](#use-templates-to-customize-restore-vm)
* [복원 된 디스크 tooattach tooan 기존 가상 컴퓨터를 사용 하 여 hello](../virtual-machines/windows/attach-managed-disk-portal.md)
* [PowerShell을 사용하여 복원된 디스크에서 새 가상 컴퓨터를 만듭니다.](./backup-azure-vms-automation.md#restore-an-azure-vm)

Hello에 **구성 복원** 블레이드에서 클릭 **확인** toofinalize hello 구성 복원 합니다. Hello에 **복원** 블레이드에서 클릭 **복원** tootrigger hello 복원 작업입니다.

![복구 구성 완료](./media/backup-azure-arm-restore-vms/trigger-restore-operation.png)

## <a name="track-hello-restore-operation"></a>Hello 복원 작업을 추적 합니다.
Hello 복원 작업을 트리거할 되 면 hello 백업 서비스는 hello 복원 작업을 추적 하기 위한 작업을 만듭니다. 백업 서비스 hello.dgml 파일을 및 일시적으로 hello 알림을 포털의 알림 영역에 표시 합니다. Hello 알림, 표시 되지 않으면 hello 알림을 아이콘 tooview를 알림을 항상 클릭 수 있습니다.

![트리거된 복원](./media/backup-azure-arm-restore-vms/restore-notification.png)

처리 하는 동안 tooview hello 작업 또는 완료 되 면 tooview hello 백업 작업 목록을 엽니다.

1. Azure 메뉴 hello 클릭 **찾아보기** hello 서비스 목록에서 입력 **복구 서비스**합니다. 서비스 목록이 hello 입력 toowhat를 조정 합니다. **복구 서비스 자격 증명 모음**이 표시되면 이를 선택합니다.

    ![복구 서비스 자격 증명 모음 열기](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    hello hello 구독에서 자격 증명 모음 목록이 표시 됩니다.

    ![복구 서비스 자격 증명 모음 목록](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
2. Hello 목록에서 선택 hello 자격 증명 모음 hello 복원한 VM 연관 됩니다. Hello 자격 증명 모음을 클릭 하면 해당 대시보드가 열립니다.
3. Hello hello 자격 증명 모음 대시보드에서 **백업 작업이** 타일을 클릭 **Azure 가상 컴퓨터** hello 자격 증명 모음과 연결 된 toodisplay hello 작업도 있습니다.

    ![자격 증명 모음 대시보드](./media/backup-azure-arm-restore-vms/vault-dashboard-jobs.png)

    hello **백업 작업이** 블레이드가 열리고 hello 작업 목록이 표시 됩니다.

    ![자격 증명 모음의 VM 목록](./media/backup-azure-arm-restore-vms/restore-job-in-progress.png)
    
## <a name="use-templates-toocustomize-restore-vm"></a>Toocustomize 복원 vm 템플릿을 사용 하 여
한 번 [디스크 복원이 완료 되 면](#Track-the-restore-operation), 복원 작업 toocreate 리소스의 백업 구성 또는 toocustomize 이름과 다른 구성 사용 하 여 새 VM의 일부로 생성 되는 hello 서식 파일을 사용할 수 있습니다 복원 지점에서 새 vm을 만들 때 만들어집니다. 

> [!NOTE]
> 템플릿은 2017년 3월 1일 이후에 만든 복구 지점에 디스크 복원의 일부로 추가됩니다. 암호화되지 않고 관리되지 않는 디스크 VM에 해당합니다. 암호화된 VM 및 Managed Disk VM에 대한 지원은 곧 출시될 릴리스에서 제공됩니다. 
>
>

복원 디스크 옵션의 일부로 생성 tooget hello 서식 파일

1. Toohello 작업에 해당 toorestore 작업 세부 정보를 이동 합니다. 
2. Hello 복원 작업 세부 정보 화면에서를 클릭 *배포 템플릿* tooinitiate 템플릿 배포 단추입니다. 

     ![복원 작업 드릴 다운](./media/backup-azure-arm-restore-vms/restore-job-drill-down.png)
   
사용자 지정 배포에 대 한 템플릿 블레이드를 배포 하는 hello 사용 하 여 템플릿 배포 너무[편집 하 고 hello 템플릿을 배포](../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template) 또는 사용자 지정 하 여 추가 [템플릿으로 작성](../azure-resource-manager/resource-group-authoring-templates.md) 배포 하기 전에. 

   ![템플릿 배포 로딩](./media/backup-azure-arm-restore-vms/loading-template.png)
   
Hello 필요한 값을 입력 한 후 동의 hello *약관* 을 클릭할 **구매**합니다.

   ![템플릿 배포 제출](./media/backup-azure-arm-restore-vms/submitting-template.png)

## <a name="post-restore-steps"></a>복원 후 단계
* Ubuntu와 같은 클라우드 초기화 기반 Linux 배포를 사용하는 경우 보안상의 이유로 복원 후 암호를 차단합니다. 하십시오 hello에 VMAccess 확장을 사용 하 여 복원 된 VM 너무[hello 암호 재설정](../virtual-machines/linux/classic/reset-access.md)합니다. 이러한 분포 tooavoid post 복원 암호 재설정에 SSH 키를 사용 하는 것이 좋습니다.
* 사용할 수 없습니다 되지만 확장 hello 백업 구성 중 설치 됩니다. 문제가 있는 경우 확장을 다시 설치하세요. 
* Hello 백업 하는 경우 VM에 고정 IP post 복원, 복원 된 VM을 만들 때 복원 된 VM 동적 IP tooavoid 충돌 하 게 됩니다. 자세한 내용은 하는 방법에 대 한 자세한 [정적 IP toorestored VM 추가](../virtual-network/virtual-networks-reserved-private-ip.md#how-to-add-a-static-internal-ip-to-an-existing-vm)
* 복원된 VM에는 가용성 값 집합이 없습니다. 복원된 디스크를 사용하여 PowerShell 또는 템플릿에서 VM을 만드는 경우 복원 디스크 옵션을 사용하고 [가용성 집합을 추가](../virtual-machines/windows/tutorial-availability-sets.md)하는 것이 좋습니다. 


## <a name="backup-for-restored-vms"></a>복원된 VM에 대한 백업
이름이 같은 VM 원래 백업 hello로 VM toosame 리소스 그룹을 복원 하는 경우 백업에서 계속 해 서 hello VM post 복원 합니다. 가 중 VM tooa 다른 리소스 그룹을 복원 하거나 복원 된 VM에 대 한 다른 이름을 지정한 경우이 새 VM으로 처리 하 고 복원 된 VM에 대 한 toosetup 백업을 해야 합니다.

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a>Azure 데이터 센터 재해 중 VM 복원
Azure 백업 hello 주 데이터 센터 위치 경험 재해를 실행 중인 Vm 및 백업 자격 증명 모음 toobe 지리적 중복을 구성 하는 경우 Vm toohello 쌍 이룬된 데이터 센터 백업 복원할 수 있습니다. 이러한 시나리오는 동안 tooselect 쌍 이룬된 데이터 센터에 있는 저장소 계정이 필요 하 고 hello 복원 프로세스의 나머지 부분과 동일한 상태로 유지 됩니다. Azure 백업에는 계산 서비스 쌍 이룬된 지역 toocreate 복원 hello 가상 컴퓨터에서 사용 됩니다. [Azure 데이터 센터 복원력](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)에 대한 자세한 정보

## <a name="restoring-domain-controller-vms"></a>도메인 컨트롤러 VM 복원
DC(도메인 컨트롤러) 가상 컴퓨터 백업은 Azure 백업을 사용하는 지원되는 시나리오입니다. 그러나 주의 해야 hello 복원 프로세스 중입니다. hello 올바른 복원 프로세스 hello 도메인의 hello 구조에 따라 달라 집니다. 가장 간단한 경우 hello에서에서 단일 도메인에 있는 단일 DC 수 있습니다. 일반적으로 프로덕션 로드에서는 단일 도메인에 여러 DC가 있고, 일부 DC는 온-프레미스에 있을 수 있습니다. 여러 도메인이 있는 포리스트도 있을 수 있습니다. 

Active Directory 관점 hello에서 Azure VM에서 지원 되는 최신 하이퍼바이저 다른 VM과 같습니다. hello 주요 차이점 온-프레미스 하이퍼바이저와은 Azure에서 사용할 수 없는 VM 콘솔 임을입니다. BMR(완전 복구) 유형 백업을 사용한 복구와 같은 특정 시나리오에서는 콘솔이 필요합니다. 그러나 VM 복원 hello 백업 자격 증명 모음에서 BMR에 대 한 대체입니다. Active Directory 복원 모드(DSRM)도 사용할 수 있으므로 모든 Active Directory 복구 모드를 실행할 수 있습니다. 자세한 배경 정보는 [Backup and Restore considerations for virtualized Domain Controllers](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers)(가상화된 도메인 컨트롤러에 대한 백업 및 복원 고려 사항) 및 [Planning for Active Directory Forest Recovery](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx)(Active Directory 포리스트 복구 계획)를 참조하세요.

### <a name="single-dc-in-a-single-domain"></a>단일 도메인의 단일 DC
hello VM에서에서 복원할 수 있습니다 (예: 다른 VM) hello Azure 포털 또는 PowerShell을 사용 하 여 합니다.

### <a name="multiple-dcs-in-a-single-domain"></a>단일 도메인의 여러 DC
Hello 통해 동일한 도메인에 연결할 수의 다른 Dc hello 네트워크, 하는 경우 모든 VM 같은 hello DC를 복원할 수 있습니다. 이면 hello 도메인의 마지막 남은 DC hello 또는 격리 된 네트워크에서 복구 수행 될 포리스트 복구 절차를 따라야 합니다.

### <a name="multiple-domains-in-one-forest"></a>한 포리스트의 여러 도메인
Hello 통해 동일한 도메인에 연결할 수의 다른 Dc hello 네트워크, 하는 경우 모든 VM 같은 hello DC를 복원할 수 있습니다. 그러나 다른 모든 경우에 포리스트 복구를 사용하는 것이 좋습니다.

## <a name="restoring-vms-with-special-network-configurations"></a>특수 네트워크 구성을 가진 Vm 복원
구성 가능한 tooback 및 특수 한 네트워크 구성을 따르고 hello 사용 하 여 Vm 복원을 않습니다. 그러나 이러한 구성 hello 복원 프로세스를 통해 이동 하는 동안 몇 가지 특별 한 주의가 필요 합니다.

* 부하 분산 장치에서의 VM(내부 및 외부)
* 다중의 예약된 IP가 있는 VM
* 다중 NIC가 있는 VM

> [!IMPORTANT]
> Vm에 대 한 hello 특수 한 네트워크 구성을 만들 때 hello 디스크 복원 PowerShell toocreate Vm을 사용 해야 합니다.
>
>

toodisk를 복원한 후 toofully hello 가상 컴퓨터를 다시 만든 후 다음이 단계를 따르십시오.

1. 사용 하 여 복구 서비스 자격 증명 모음에서 hello 디스크 복원 [PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm)
2. 부하 분산 장치에 필요한 hello VM 구성 만들기/여러 NIC/다중 예약 된 IP를 사용 하 여 hello PowerShell cmdlet 및 toocreate hello 원하는 구성의 VM을 사용 합니다.

   * [내부 부하 분산 장치 ](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)
   * VM tooconnect 너무 만들기[인터넷에 부하 분산 장치를 연결 합니다.](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)
   * [다중 NIC](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)
   * [다중의 예약된 IP](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)

## <a name="next-steps"></a>다음 단계
Vm을 복원할 수 있습니다, 했으므로 hello 문제 해결 문서 Vm이 있는 일반적인 오류에 대 한 내용은 참조 하십시오. 또한 Vm 사용 하 여 작업 관리에 hello 문서 확인해 보세요.

* [문제 해결](backup-azure-vms-troubleshoot.md#restore)
* [가상 컴퓨터 관리](backup-azure-manage-vms.md)
