---
title: "Azure 가상 컴퓨터 클래식 배포 tooa 백업 자격 증명 모음을 aaaBack | Microsoft Docs"
description: "Azure 가상 컴퓨터 백업에 대한 이 절차를 사용하여 가상 컴퓨터 검색, 등록 및 백업합니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "가상 컴퓨터 백업; 가상 컴퓨터 백업 백업; 백업 및 재해 복구; VM 백업"
ms.assetid: c0ab5469-65fd-4af5-ae9b-f5d183f82ce8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 048e32d9b2bd5bdd7a125225a71a6d805bb4fbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a>Azure Virtual Machines 백업(클래식 포털)
> [!div class="op_single_selector"]
> * [Vm tooRecovery 서비스 자격 증명 모음에 백업](backup-azure-arm-vms.md)
> * [Vm tooBackup 자격 증명 모음에 백업](backup-azure-vms.md)
>
>

이 문서는 클래식 배포 된 Azure 가상 컴퓨터 (VM) tooa 백업 자격 증명 모음에 백업에 대 한 hello 절차를 제공 합니다. Azure 가상 컴퓨터를 백업할 수 전에의 care tootake 필요한 몇 가지 작업이 있습니다. 따라서, 전체 hello 아직 수행 하지 않은 경우 [필수 구성 요소](backup-azure-vms-prepare.md) tooprepare Vm에 백업에 대 한 사용자 환경입니다.

자세한 내용은 hello 문서를 참조 [Azure에서 VM 백업 인프라 계획](backup-azure-vms-introduction.md) 및 [Azure 가상 컴퓨터](https://azure.microsoft.com/documentation/services/virtual-machines/)합니다.

> [!NOTE]
> Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델인 [리소스 관리자와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)모델이 있습니다. 백업 자격 증명 모음은 클래식 배포 VM만 보호할 수 있습니다. 백업 자격 증명 모음을 사용하여 Resource Manager 배포 VM을 보호할 수 없습니다. 참조 [Vm tooRecovery 서비스 자격 증명 모음에 백업](backup-azure-arm-vms.md) 자격 증명 모음 복구 서비스 작업에 대 한 내용은 합니다.
>
>

Azure 가상 컴퓨터 백업에는 3가지 주요 단계가 포함됩니다.

![Azure IaaS VM을 tooback 세 단계](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> 가상 컴퓨터 백업은 로컬 프로세스입니다. 하나의 영역 tooa 백업 자격 증명 모음에 다른 지역에서 가상 컴퓨터를 백업할 수 없습니다. 따라서 백업할 VM이 있는 각 Azure 지역에 백업 자격 증명 모음을 만들어야 합니다.
>
> [!IMPORTANT]
> 2017 년 3 월 부터는 hello 클래식 포털 toocreate 백업 자격 증명 모음은 더 이상 사용할 수 없습니다.
> 이제 사용자 백업 자격 증명 모음 tooRecovery 서비스 자격 증명 모음을 업그레이드할 수 있습니다. 자세한 내용은 hello 문서 참조 [복구 서비스 자격 증명 모음에 백업 자격 증명 모음 tooa 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md)합니다. Microsoft는 것이 권장 tooupgrade 백업 tooRecovery 서비스 자격 증명 모음 자격 증명 모음입니다.<br/> 2017 년 10 월 15 후 PowerShell toocreate 백업 자격 증명 모음을 사용할 수 없습니다. **2017년 11월 1일까지**:
>- 모든 나머지 백업 자격 증명 모음을 자동으로 업그레이드 된 tooRecovery 서비스 자격 증명 모음 됩니다.
>- 하면 hello 클래식 포털에서 수 tooaccess 백업 데이터 수 없습니다. 대신, 복구 서비스 자격 증명 모음에 hello Azure 포털 tooaccess 백업 데이터를 사용 합니다.
>

## <a name="step-1---discover-azure-virtual-machines"></a>1단계 - Azure 가상 컴퓨터 검색
모든 새 가상 컴퓨터 (Vm) 추가 toohello 구독을 등록 하기 전에 식별 된 tooensure hello 검색 프로세스를 실행 합니다. 추가 정보와 함께 hello 구독에서 가상 컴퓨터의 hello 목록에 대 한 hello 프로세스 쿼리 Azure hello 클라우드 서비스 이름 및 hello 영역 같은입니다.

1. Toohello 로그인 [클래식 포털](http://manage.windowsazure.com/)
2. Hello Azure 서비스 목록에서 클릭 **복구 서비스** 의 백업 및 사이트 복구 자격 증명 모음 tooopen hello 목록입니다.
    ![자격 증명 모음 목록 열기](./media/backup-azure-vms/choose-vault-list.png)
3. 백업 자격 증명 모음은의 hello 목록의 hello 자격 증명 모음 tooback VM 선택 합니다.

    이 새로운 자격 증명 모음 hello 포털 toohello 열립니다 **빠른 시작** 페이지.

    ![등록된 항목 열기 메뉴](./media/backup-azure-vms/vault-quick-start.png)

    이전에 구성 된 자격 증명 모음 hello hello 포털 가장 최근에 사용한 toohello 메뉴를 엽니다.
4. Hello 자격 증명 모음의 메뉴에서 (hello 페이지의 위쪽 hello)를 클릭 **등록 된 항목**합니다.

    ![등록된 항목 열기 메뉴](./media/backup-azure-vms/vault-menu.png)
5. Hello에서 **형식** 메뉴 선택 **Azure 가상 컴퓨터**합니다.

    ![워크로드 선택](./media/backup-azure-vms/discovery-select-workload.png)
6. 클릭 **DISCOVER** hello hello 페이지 맨 아래에 있습니다.
    ![검색 단추](./media/backup-azure-vms/discover-button-only.png)

    hello 검색 프로세스는 hello 가상 컴퓨터 정리 된 되는 동안 몇 분 정도 걸릴 수 있습니다. 알림을 hello hello 프로세스가 실행 되 고 있는지 알려 주는 hello 화면 맨 아래에 있습니다.

    ![VM 검색](./media/backup-azure-vms/discovering-vms.png)

    hello 알림이 hello 프로세스가 완료 되 면 변경 합니다. Hello 검색 프로세스는 hello 가상 컴퓨터를 찾지 못했습니다 먼저 hello Vm 존재 확인 합니다. Hello Vm 존재 하는 경우 확인 hello Vm은에 hello 동일 지역 hello 백업 자격 증명 모음으로 합니다. 있으면 hello Vm에서 동일한 지역 hello 하 hello Vm은 아직 등록 된 tooa 백업 자격 증명 모음을 확인 합니다. VM은 할당 된 tooa 백업 자격 증명 모음의 경우 할당 된 사용 가능한 toobe tooother 백업 자격 증명 모음 않습니다.

    ![검색 완료](./media/backup-azure-vms/discovery-complete.png)

    Hello 새 항목을 검색 한 후 tooStep 2로 이동 하 고 Vm을 등록 합니다.

## <a name="step-2---register-azure-virtual-machines"></a>2단계 - Azure 가상 컴퓨터 등록
Azure 가상 컴퓨터 tooassociate 등록 사용 하 여 hello Azure 백업 서비스입니다. 일반적으로 일회성 작업입니다.

1. 백업 자격 증명 모음을 toohello 이동 **복구 서비스** Azure 포털 hello와 클릭 **등록 된 항목**합니다.
2. 선택 **Azure 가상 컴퓨터** hello 드롭 다운 메뉴에서 합니다.

    ![워크로드 선택](./media/backup-azure-vms/discovery-select-workload.png)
3. 클릭 **등록** hello hello 페이지 맨 아래에 있습니다.
    ![등록 단추](./media/backup-azure-vms/register-button-only.png)
4. Hello에 **등록 항목** 바로 가기 메뉴, tooregister 않겠다고 선택 hello 가상 컴퓨터. 두 개 이상의 가상 컴퓨터가 있는 경우 동일한 hello 이름을 서로 클라우드 서비스 toodistinguish hello를 사용 합니다.

   > [!TIP]
   > 한 번에 여러 가상 컴퓨터를 등록할 수 있습니다.
   >
   >

    선택한 각 가상 컴퓨터에 대한 작업이 만들어집니다.
5. 클릭 **작업 보기** hello 알림 toogo toohello에 **작업** 페이지.

    ![작업 등록](./media/backup-azure-vms/register-create-job.png)

    hello 가상 컴퓨터도 hello 등록 작업의 hello 상태와 함께 등록 된 항목의 hello 목록에 나타납니다.

    ![등록 상태 1](./media/backup-azure-vms/register-status01.png)

    Hello 작업이 완료 되 면 hello 상태 변경 tooreflect hello *등록* 상태입니다.

    ![등록 상태 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a>3단계 - Azure 가상 컴퓨터 보호
이제 hello 가상 컴퓨터에 대 한 백업 및 보존 정책을 설정할 수 있습니다. 단일 보호 작업을 사용하여 여러 가상 컴퓨터를 보호할 수 있습니다.

Azure 백업 자격 증명 모음은 함께 제공 2015 년 5 월 이후에 만들어진 hello 자격 증명 모음에 기본 제공 기본 정책. 이 기본 정책을 30일의 기본 보존 기간 및 하루 한 번 백업 일정과 함께 제공됩니다.

1. 백업 자격 증명 모음을 toohello 이동 **복구 서비스** Azure 포털 hello와 클릭 **등록 된 항목**합니다.
2. 선택 **Azure 가상 컴퓨터** hello 드롭 다운 메뉴에서 합니다.

    ![포털에서 워크로드 선택](./media/backup-azure-vms/select-workload.png)
3. 클릭 **보호** hello hello 페이지 맨 아래에 있습니다.

    hello **항목 보호 마법사** 나타납니다. hello 마법사만 등록 되 고 보호 되지 않는 가상 컴퓨터를 나열 합니다. 원하는 tooprotect hello 가상 컴퓨터를 선택 합니다.

    두 개 이상의 가상 컴퓨터가 있는 경우 동일한 hello 이름을 hello 가상 컴퓨터 간의 클라우드 서비스 toodistinguish hello를 사용 합니다.

   > [!TIP]
   > 한 번에 여러 가상 컴퓨터를 보호할 수 있습니다.
   >
   >

    ![규모로 보호 구성](./media/backup-azure-vms/protect-at-scale.png)

4. 선택 된 **백업 일정** tooback 선택한 hello 가상 컴퓨터를 합니다. 정책의 기존 집합에서 선택하거나 새로 정의할 수 있습니다.

    각 백업 정책 정책에는 해당 정책과 연관된 여러 가상 컴퓨터가 있을 수 있습니다. 그러나 시간에서 hello 가상 컴퓨터는 특정된 시점에서 하나의 정책과 연결할 수만 있습니다.

    ![새 정책으로 보호](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > 백업 정책을 hello 예약 된 백업에 대 한 보존 규칙에 포함 됩니다. 기존 백업 정책을 선택 하는 경우 hello 다음 단계에서 hello 보존 옵션을 수정할 수 없습니다.
   >
   >

5. 선택 된 **보존 범위** tooassociate hello 백업 합니다.

    ![유연한 보존으로 보호](./media/backup-azure-vms/policy-retention.png)

    보존 정책은 백업 저장에 대해 hello 길이 지정 합니다. Hello 백업이 수행 되는 경우에 따라 서로 다른 보존 정책을 지정할 수 있습니다. 예를 들어 매일 수행된 백업 지점(작업 복구 지점으로 사용됨)은 90일 동안 보존될 수도 있습니다. 이 비해 hello (감사 목적) 각 분기 끝에 수행 하는 백업 지점 toobe 많은 개월 또는 수 년에 대 한 유지 해야 합니다.

    ![가상 컴퓨터는 복구 지점으로 백업됨](./media/backup-azure-vms/long-term-retention.png)

    이 예제 이미지에서

   * **일 단위 보존 정책**: 매일 수행된 백업이 30일 동안 저장됩니다.
   * **주 단위 보존 정책**: 매주 일요일에 수행된 백업이 104주 동안 유지됩니다.
   * **매월 보존 정책**: 매월 마지막 일요일 hello에서 수행 된 백업을 120 개월 동안 유지 됩니다.
   * **연간 보존 정책**: 99 년 동안 매년 1 월의 첫 번째 일요일 hello에서 수행 된 백업을 유지 됩니다.

     작업에는 선택한 각 가상 컴퓨터에 대 한 hello 가상 컴퓨터 toothat 정책을 연결와 tooconfigure hello 보호 정책을 만들어집니다.
6. tooview hello 목록이 **보호 구성** hello 자격 증명 모음 메뉴에서 작업을 클릭 하 여 **작업** 선택 **보호 구성** hello에서 **작업**  필터입니다.

    ![보호 작업 구성](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a>초기 백업
정책을 사용 하 여 hello 가상 컴퓨터가 보호 되 고 나면 그 아래에 표시 hello **보호 된 항목** hello 상태와 함께 탭 *(보류 중 초기 백업) 보호 됨-*합니다. 기본적으로 첫 번째 예약 된 백업을 hello는 hello *초기 백업을*합니다.

보호 구성 직후 tootrigger hello의 초기 백업:

1. Hello hello 맨 아래에 **보호 된 항목** 페이지 **지금 백업**합니다.

    hello Azure 백업 서비스는 hello 초기 백업 작업에 대 한 백업 작업을 만듭니다.
2. Hello 클릭 **작업** 작업 목록이 tooview hello 탭 합니다.

    ![진행 중인 백업](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> Hello 백업 작업 동안 hello Azure 백업 서비스에서 모든 작업을 작성 하 고 일관 된 스냅숏을 각 가상 컴퓨터 tooflush 명령 toohello 백업 확장을 발급 합니다.
>
>

Hello 초기 백업을 완료 되 면 hello에 hello 가상 컴퓨터의 hello 상태 **보호 된 항목** 탭은 *Protected*합니다.

![가상 컴퓨터는 복구 지점으로 백업됨](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a>백업 상태 및 세부 정보 보기
가상 컴퓨터 개수 hello hello도 증가 보호 되 면 **대시보드** 페이지 요약 합니다. hello **대시보드** 페이지에 표시 된 지난 24 시간 동안 hello에서 작업의 hello 수 *성공*, 있어야 *실패*, 되며 *진행*. Hello에 **작업** 페이지에서 hello를 사용 하 여 **상태**, **작업**, 또는 **에서** 및 **를** 메뉴 toofilter hello 작업입니다.

![대시보드 페이지에서 백업 상태](./media/backup-azure-vms/dashboard-protectedvms.png)

Hello 대시보드의 값은 24 시간 마다 새로 고쳐집니다.

## <a name="troubleshooting-errors"></a>문제 해결 오류
가상 컴퓨터를 백업 하는 동안 문제를 실행 하면 확인 hello [VM 문제 해결 문서](backup-azure-vms-troubleshoot.md) 에 대 한 도움말입니다.

## <a name="next-steps"></a>다음 단계
* [가상 컴퓨터 관리 및 모니터링](backup-azure-manage-vms.md)
* [가상 컴퓨터 복원](backup-azure-restore-vms.md)
