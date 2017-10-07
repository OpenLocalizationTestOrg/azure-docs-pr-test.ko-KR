---
title: Azure vm aaaBack | Microsoft Docs
description: "검색 하 고, 등록 및 Azure 가상 컴퓨터 tooa 복구 서비스 자격 증명 모음에 백업 합니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "가상 컴퓨터 백업; 가상 컴퓨터 백업; 백업 및 재해 복구; ARM VM 백업"
ms.assetid: 5c68481d-7be3-4e68-b87c-0961c267053e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: trinadhk;jimpark;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a204a42726450a7fd89b5563a786b5070578b113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-tooa-recovery-services-vault"></a>Azure 가상 컴퓨터를 백업 tooa 복구 서비스 자격 증명 모음에
> [!div class="op_single_selector"]
> * [Vm tooRecovery 서비스 자격 증명 모음에 백업](backup-azure-arm-vms.md)
> * [Vm tooBackup 자격 증명 모음에 백업](backup-azure-vms.md)
>
>

이 문서 tooback를 Azure Vm (리소스 관리자를 통해 배포 및 클래식 배포) tooa 복구 서비스 자격 증명 모음에 대해 자세히 설명 합니다. 대부분의 Vm를 백업 하기 위한 hello 작업 hello 준비입니다. 백업 또는 VM 보호를 완료 해야 hello [필수 구성 요소](backup-azure-arm-vms-prepare.md) tooprepare Vm을 보호 하기 위한 사용자 환경입니다. Hello 필수 구성 요소를 완료 한 후 VM의 hello 백업 작업 tootake 스냅숏을 시작할 수 있습니다.


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

자세한 내용은에 hello 문서 참조 [Azure에서 VM 백업 인프라 계획](backup-azure-vms-introduction.md) 및 [Azure 가상 컴퓨터](https://azure.microsoft.com/documentation/services/virtual-machines/)합니다.

## <a name="triggering-hello-backup-job"></a>Hello 백업 작업 트리거
복구 서비스 자격 증명 모음에 hello와 연결 된 hello 백업 정책을 hello 백업 작업이 실행 되 고 빈도 및 시기를 정의 합니다. 기본적으로 첫 번째 예약 된 백업을 hello hello 초기 백업이입니다. Hello 초기 백업을 수행 될 때까지 hello에서 마지막 백업 상태 hello **백업 작업** 블레이드로 표시 **경고 (초기 백업 보류 중인)**합니다.

![보류 중인 백업](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

초기 백업 기간이 하지 않는 한 toobegin 곧 것이 좋습니다를 실행 하는 **지금 백업**합니다. hello 다음 절차에서에서 시작 hello 자격 증명 모음 대시보드 합니다. 이 절차는 모든 필수 구성 요소를 완료 한 후 hello 초기 백업 작업을 실행 하는 데 사용 됩니다. Hello 초기 백업 작업을 이미 실행 하는 경우이 절차 ´ ù. hello 연결 된 백업 정책에 따라 결정 hello 다음 백업 작업입니다.  

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

## <a name="troubleshooting-errors"></a>문제 해결 오류
가상 컴퓨터를 백업 하는 동안 문제를 실행 하면 참조 hello [VM 문제 해결 문서](backup-azure-vms-troubleshoot.md) 에 대 한 도움말입니다.

## <a name="next-steps"></a>다음 단계
지금 VM을 보호 하는 참조 문서 toolearn VM 관리 작업에 대 한 다음 hello와 방법을 toorestore Vm입니다.

* [가상 컴퓨터 관리 및 모니터링](backup-azure-manage-vms.md)
* [가상 컴퓨터 복원](backup-azure-arm-restore-vms.md)
