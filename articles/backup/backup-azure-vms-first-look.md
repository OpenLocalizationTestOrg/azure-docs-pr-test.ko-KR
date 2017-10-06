---
title: "소개 - 백업 자격 증명으로 Azure VM 백업 | Microsoft Docs"
description: "Hello 클래식 포털 tooback Azure Vm tooa 백업 자격 증명 모음을 사용 합니다. 이 자습서에서는 hello 백업 자격 증명 모음 만들기, Vm hello 등록, 백업 정책을 만드는 hello 초기 백업 작업 실행 등 모든 단계에 설명 합니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 722820dc-b65f-425c-a9e5-c1946e896a87
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;
ms.openlocfilehash: 77700e69eab9faccbc7ef923e1eb4e1f97be75d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a>소개: Azure 가상 컴퓨터 백업
> [!div class="op_single_selector"]
> * [복구 서비스 자격 증명 모음으로 VM 보호](backup-azure-vms-first-look-arm.md)
> * [백업 자격 증명으로 Azure VM 보호](backup-azure-vms-first-look.md)
>
>

이 자습서는 Azure 가상 컴퓨터 (VM) tooa 백업 자격 증명 모음에서 Azure 백업에 대 한 hello 단계를 안내 합니다. 이 문서에서는 hello 클래식 모델 또는 Vm을 백업에 대 한 Service Manager 배포 모델을 설명 합니다. hello 다음 단계 적용만 tooBackup 자격 증명 모음 hello 클래식 포털에서 생성 됩니다. 새 배포를 위해 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.

VM tooa 복구 서비스 자격 증명 모음 tooa 리소스 그룹에 속하는 백업에 관심이 있는 경우 참조 [소개: 복구 서비스 자격 증명 모음으로 보호 Vm](backup-azure-vms-first-look-arm.md)합니다.

toosuccessfully 완료 hello 다음 자습서에서는 이러한 필수 구성이 요소 존재 해야 합니다.

* Azure 구독에서 VM을 만들었습니다.
* hello VM에 연결 tooAzure 공용 IP 주소가 있습니다. 자세한 내용은 [네트워크 연결](backup-azure-vms-prepare.md#network-connectivity)을 참조하세요.


> [!NOTE]
> Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델인 [리소스 관리자와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)모델이 있습니다. 이 자습서는 hello 클래식 포털에서 만든 가상 컴퓨터와 함께 사용 합니다.
>
>

## <a name="create-a-backup-vault"></a>백업 자격 증명 모음 만들기
백업 자격 증명 모음에는 모든 hello 백업 및 시간에 따라 생성 된 복구 지점을 저장 하는 엔터티입니다. hello 백업 자격 증명 모음에는 적용 된 toohello 가상 컴퓨터를 백업 하는 hello 백업 정책을 포함 되어 있습니다.

> [!IMPORTANT]
> 2017 년 3 월 부터는 hello 클래식 포털 toocreate 백업 자격 증명 모음은 더 이상 사용할 수 없습니다.
> 에 백업 자격 증명 모음 tooRecovery 서비스 자격 증명 모음을 업그레이드할 수 있습니다. 자세한 내용은 hello 문서 참조 [복구 서비스 자격 증명 모음에 백업 자격 증명 모음 tooa 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md)합니다. Microsoft는 것이 권장 tooupgrade 백업 tooRecovery 서비스 자격 증명 모음 자격 증명 모음입니다.<br/> 2017 년 10 월 15 후 PowerShell toocreate 백업 자격 증명 모음을 사용할 수 없습니다. **2017년 11월 1일까지**:
>- 모든 나머지 백업 자격 증명 모음을 자동으로 업그레이드 된 tooRecovery 서비스 자격 증명 모음 됩니다.
>- 하면 hello 클래식 포털에서 수 tooaccess 백업 데이터 수 없습니다. 대신, 복구 서비스 자격 증명 모음에 hello Azure 포털 tooaccess 백업 데이터를 사용 합니다.
>

## <a name="discover-and-register-azure-virtual-machines"></a>Azure 가상 컴퓨터 검색 및 등록
Hello VM 자격 증명 모음을 등록 하기 전에 hello 검색 프로세스 tooidentify 새 Vm 실행 합니다. 이 hello 클라우드 서비스 이름 및 hello 지역 등과 같은 추가 정보와 함께 hello 구독에서 가상 컴퓨터의 목록을 반환합니다.

1. Toohello 로그인 [Azure 클래식 포털](http://manage.windowsazure.com/)
2. Hello Azure 클래식 포털에서에서 클릭 **복구 서비스** tooopen hello 목록이 복구 서비스 자격 증명 모음입니다.
    ![워크로드 선택](./media/backup-azure-vms-first-look/recovery-services-icon.png)
3. 자격 증명 모음 hello 목록에서 VM 자격 증명 모음 tooback hello를 선택 합니다.

    자격 증명 모음을 선택 하면 hello에서 열립니다 **빠른 시작** 페이지
4. Hello 자격 증명 모음의 메뉴에서 클릭 **등록 된 항목**합니다.

    ![워크로드 선택](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. Hello에서 **형식** 메뉴 선택 **Azure 가상 컴퓨터**합니다.

    ![워크로드 선택](./media/backup-azure-vms/discovery-select-workload.png)
6. 클릭 **DISCOVER** hello hello 페이지 맨 아래에 있습니다.
    ![검색 단추](./media/backup-azure-vms/discover-button-only.png)

    hello 검색 프로세스는 hello 가상 컴퓨터 정리 된 되는 동안 몇 분 정도 걸릴 수 있습니다. 알림을 hello hello 프로세스가 실행 되 고 있는지 알려 주는 hello 화면 맨 아래에 있습니다.

    ![VM 검색](./media/backup-azure-vms/discovering-vms.png)

    hello 알림이 hello 프로세스가 완료 되 면 변경 합니다.

    ![검색 완료](./media/backup-azure-vms-first-look/discovery-complete.png)
7. 클릭 **등록** hello hello 페이지 맨 아래에 있습니다.
    ![등록 단추](./media/backup-azure-vms-first-look/register-icon.png)
8. Hello에 **등록 항목** 바로 가기 메뉴, tooregister 않겠다고 선택 hello 가상 컴퓨터.

   > [!TIP]
   > 한 번에 여러 가상 컴퓨터를 등록할 수 있습니다.
   >
   >

    선택한 각 가상 컴퓨터에 대한 작업이 만들어집니다.
9. 클릭 **작업 보기** hello 알림 toogo toohello에 **작업** 페이지.

    ![작업 등록](./media/backup-azure-vms/register-create-job.png)

    hello 가상 컴퓨터도 hello 등록 작업의 hello 상태와 함께 등록 된 항목의 hello 목록에 나타납니다.

    ![등록 상태 1](./media/backup-azure-vms/register-status01.png)

    Hello 작업이 완료 되 면 hello 상태 변경 tooreflect hello *등록* 상태입니다.

    ![등록 상태 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Hello 가상 컴퓨터에 hello VM 에이전트 설치
Azure VM 에이전트 hello hello 백업 확장 toowork hello에 대 한 Azure 가상 컴퓨터에 설치 되어야 합니다. VM 에이전트 hello가 이미 hello VM;에 있는, hello Azure 갤러리에서에서 VM을 만든 경우 너무 건너뛸 수[Vm 보호](backup-azure-vms-first-look.md#create-the-backup-policy)합니다.

VM는 온-프레미스 데이터 센터에서 마이그레이션하는 경우 hello VM 아마도 않아도 hello VM 에이전트가 설치 됩니다. VM 에이전트 hello tooprotect hello VM 계속 진행 하기 전에 hello 가상 컴퓨터에 설치 해야 합니다. 설치에 자세한 단계는 VM 에이전트를 hello, hello 참조 [hello 백업 Vm 문서 VM 에이전트 섹션](backup-azure-vms-prepare.md#vm-agent)합니다.

## <a name="create-hello-backup-policy"></a>Hello 백업 정책 만들기
Hello 초기 백업 작업을 트리거 하기 전에 백업 스냅숏이 만들어질 때 hello 일정을 설정 합니다. 백업 스냅숏을 수행 되 고 시간의 길이 해당 스냅숏으로 hello hello 일정은 백업 정책 hello 유지입니다. hello 보존 정보 son-ब ा प ज-백업 회전 구성표를 기반으로 합니다.

1. 백업 자격 증명 모음을 toohello 이동 **복구 서비스** Azure 클래식 포털 hello와 클릭 **등록 된 항목**합니다.
2. 선택 **Azure 가상 컴퓨터** hello 드롭 다운 메뉴에서 합니다.

    ![포털에서 워크로드 선택](./media/backup-azure-vms/select-workload.png)
3. 클릭 **보호** hello hello 페이지 맨 아래에 있습니다.
    ![보호 클릭](./media/backup-azure-vms-first-look/protect-icon.png)

    hello **항목 보호 마법사** 나타나고 목록이 *만* 가상 컴퓨터를 등록 되 고 보호 되지 않습니다.

    ![규모로 보호 구성](./media/backup-azure-vms/protect-at-scale.png)
4. 원하는 tooprotect hello 가상 컴퓨터를 선택 합니다.

    Hello로 두 개 이상의 가상 컴퓨터가 있는 경우 동일한 이름, 사용 하 여 hello hello 가상 컴퓨터 간에 toodistinguish 클라우드 서비스입니다.
5. Hello에 **보호 구성** 메뉴 기존 정책을 선택 하거나 새 정책 tooprotect 식별 된 hello 가상 컴퓨터를 만듭니다.

    새 백업 자격 증명 모음은 hello 자격 증명 모음과 연결 된 기본 정책이 있어야 합니다. 이 정책은 각 저녁 스냅숏 매일 걸리며 hello 일일 스냅숏은 30 일 동안 유지 됩니다. 각 백업 정책 정책에는 해당 정책과 연관된 여러 가상 컴퓨터가 있을 수 있습니다. 그러나 한 번에 hello 가상 컴퓨터는 하나의 정책과 연결할 수만 있습니다.

    ![새 정책으로 보호](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > 백업 정책을 hello 예약 된 백업에 대 한 보존 규칙에 포함 됩니다. 기존 백업 정책을 선택 하는 경우 hello 다음 단계에서 없습니다 toomodify hello 보존 옵션 됩니다.
   >
   >
6. **보존 범위** 정의 hello hello 특정 백업 점에 대 한 매일, 매주, 매월 및 매년 범위입니다.

    ![가상 컴퓨터는 복구 지점으로 백업됨](./media/backup-azure-vms/long-term-retention.png)

    보존 정책은 백업 저장에 대해 hello 길이 지정 합니다. Hello 백업이 수행 되는 경우에 따라 서로 다른 보존 정책을 지정할 수 있습니다.
7. 클릭 **작업** tooview hello 목록이 **보호 구성** 작업 합니다.

    ![보호 작업 구성](./media/backup-azure-vms/protect-configureprotection.png)

    Hello 정책, 설정 했으므로 toohello 다음 단계로 이동 하 고 hello 초기 백업을 실행 합니다.

## <a name="initial-backup"></a>초기 백업
정책을 사용 하 여 보호 된 가상 컴퓨터를 면 hello에 해당 관계를 볼 수 있습니다 **보호 된 항목** 탭 합니다. 발생할 때까지 초기 백업을 hello, hello **보호 상태** 표시 **(보류 중 초기 백업) 보호 됨-**합니다. 기본적으로 첫 번째 예약 된 백업을 hello는 hello *초기 백업을*합니다.

![보류 중인 백업](./media/backup-azure-vms-first-look/protection-pending-border.png)

toostart hello 초기 지금 백업:

1. Hello에 **보호 된 항목** 페이지 **지금 백업** hello hello 페이지 맨 아래에 있습니다.
    ![지금 백업 아이콘](./media/backup-azure-vms-first-look/backup-now-icon.png)

    hello Azure 백업 서비스는 hello 초기 백업 작업에 대 한 백업 작업을 만듭니다.
2. Hello 클릭 **작업** 작업 목록이 tooview hello 탭 합니다.

    ![진행 중인 백업](./media/backup-azure-vms-first-look/protect-inprogress.png)

    초기 백업을 완료 되 면, hello에 hello 가상 컴퓨터의 hello 상태 **보호 된 항목** 탭은 *Protected*합니다.

    ![가상 컴퓨터는 복구 지점으로 백업됨](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > 가상 컴퓨터 백업은 로컬 프로세스입니다. 하나의 영역 tooa 백업 자격 증명 모음에서 다른 지역에서 가상 컴퓨터를 백업할 수 없습니다. 따라서 해당 지역에서 toobe 백업 해야 하는 Vm에 있는 모든 Azure 지역에 대 한 백업 자격 증명 모음을 하나 이상 만들 수 해야 합니다.
   >
   >

## <a name="next-steps"></a>다음 단계
이제 VM을 성공적으로 백업하면 도움이 될 수 있는 다음 단계가 있습니다. hello 가장 논리적인 단계는 toofamiliarize 직접 데이터 tooa VM를 복원 하 여입니다. 그러나 가지 이해 하는 데 도움이 되는 관리 작업 방법 tookeep 안전 데이터 비용을 최소화 하 고 있습니다.

* [가상 컴퓨터 관리 및 모니터링](backup-azure-manage-vms.md)
* [가상 컴퓨터 복원](backup-azure-restore-vms.md)
* [문제 해결 지침](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a>질문이 있으십니까?
기능의 경우 원하는 toosee 포함 또는 질문이 있는 경우 [피드백](http://aka.ms/azurebackup_feedback)합니다.
