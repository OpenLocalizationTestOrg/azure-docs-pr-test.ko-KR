---
title: "aaaManage 리소스 관리자를 통해 배포 된 가상 컴퓨터 백업을 | Microsoft Docs"
description: "자세한 내용은 방법 toomanage 및 모니터 리소스 관리자를 통해 배포 된 가상 컴퓨터 백업"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: f3050283-d60f-472d-b464-cb844e70d67e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: trinadhk;markgal
ms.openlocfilehash: 241fc4b2a29c5cd8b8b0ee8efbf8ba4e96c6a7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-machine-backups"></a>Azure 가상 컴퓨터 백업 관리
> [!div class="op_single_selector"]
> * [Azure VM 백업 관리](backup-azure-manage-vms.md)
> * [클래식 VM 백업 관리](backup-azure-manage-vms-classic.md)
>
>

이 문서는 VM 백업이 관리에 대 한 지침을 제공 하 고 hello 포털 대시보드에서 사용할 수 있는 hello 백업 경고 정보를 설명 합니다. 이 문서에 대 한 hello 지침 toousing Vm을 복구 서비스 자격 증명 모음을 적용합니다. 이 문서는 hello 가상 컴퓨터 만들기를 다루지 않습니다 또는 설명지 않습니다 것 방법을 tooprotect 가상 컴퓨터. Azure에서 Azure 리소스 관리자를 통해 배포 된 Vm을 보호 하기 위해 복구 서비스 자격 증명 모음 primer, 참조 [소개: Vm tooa 복구 서비스 자격 증명 모음에 백업](backup-azure-vms-first-look-arm.md)합니다.

## <a name="manage-vaults-and-protected-virtual-machines"></a>자격 증명 모음 및 보호된 가상 컴퓨터 관리
Azure 포털 hello hello 복구 서비스 자격 증명 모음 대시보드 포함 하 여 hello 자격 증명 모음에 대 한 액세스 tooinformation을 제공합니다.

* hello 가장 최근의 백업 스냅숏을 hello 최근 복원 지점 이기도 < b r\>
* 백업 정책 hello < b r\>
* 모든 백업 스냅숏의 전체 크기 <br\>
* hello 자격 증명 모음으로 보호 되는 가상 컴퓨터 수 < b r\>

가상 컴퓨터 백업 사용 하 여 많은 관리 작업 hello 대시보드에 hello 자격 증명 모음을 열어로 시작 합니다. 그러나 자격 증명 모음에 사용 되는 tooprotect 여러 항목 (또는 여러 Vm)를 열고 특정 VM에 대 한 세부 정보 tooview 수 있기 때문에 자격 증명 모음 항목 대시보드 hello 합니다. hello 다음 단계에서는 tooopen hello *자격 증명 모음 대시보드* toohello 후 계속 *자격 증명 모음 항목 대시보드*합니다. 주는 tooadd 자격 증명 모음 hello 방법과 항목 toohello 자격 증명 모음 대시보드 Azure hello Pin toodashboard 명령을 사용 하 여 두 절차 모두에서 "팁"입니다. Pin toodashboard는 바로 가기 toohello 자격 증명 모음 또는 항목을 만드는 방법입니다. 또한 hello 바로 가기에서 일반적인 명령을 실행할 수 있습니다.

> [!TIP]
> 여러 개인 대시보드가 있는 경우 블레이드를 열고 hello 어둡게, 파랑 슬라이더를 사용 하 여 hello 창 tooslide hello Azure 대시보드 간에 hello 맨 아래에 있습니다.
>
>

![슬라이더가 있는 전체 보기](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-hello-dashboard"></a>복구 서비스 자격 증명 모음 hello 대시보드를 엽니다.
1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. Hello 허브 메뉴에서 클릭 **찾아보기** hello 리소스 목록에 입력 하 고 **복구 서비스**합니다. 입력을 시작할 때 hello 사용자 입력에 따라 필터를 나열 합니다. **복구 서비스 자격 증명 모음**을 클릭합니다.

    ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    복구 서비스 자격 증명 모음 hello 목록이 표시 됩니다.

    ![복구 서비스 자격 증명 모음 목록 ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > 자격 증명 모음 toohello Azure 대시보드를 고정 하는 경우 해당 자격 증명 모음이 hello Azure 포털을 열 때에 즉시 액세스할 수 있습니다. hello 자격 증명 모음 목록에는 자격 증명 모음 toohello 대시보드 toopin hello 자격 증명 모음을 마우스 오른쪽 단추로 클릭 하 고 선택 **Pin toodashboard**합니다.
   >
   >
3. 자격 증명 모음 hello 목록에서 대시보드 hello 자격 증명 모음 tooopen 선택 합니다. Hello 자격 증명 모음, 자격 증명 모음 대시보드 hello 및 hello 선택 **설정을** 블레이드를 엽니다. 다음 이미지는 hello에서 hello **Contoso-자격 증명 모음** 대시보드가 강조 표시 됩니다.

    ![자격 증명 모음 대시보드 열기 및 설정 블레이드](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a>자격 증명 모음 항목 대시보드 열기
Hello 이전 절차에서 hello 자격 증명 모음 대시보드를 열. tooopen hello 자격 증명 모음 항목 대시보드:

1. Hello 자격 증명 모음 대시보드 hello에서에서 **백업 항목** 타일을 클릭 하 여 **Azure 가상 컴퓨터**합니다.

    ![백업 항목 열기 타일](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    hello **백업 항목** 블레이드에 hello 각 항목에 대 한 마지막 백업 작업을 나열 합니다. 이 예제에는 자격 증명이 모음에 의해 보호되는 하나의 가상 컴퓨터인 demovm-markgal이 있습니다.  

    ![백업 항목 타일](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > 편리한 액세스에 대 한 자격 증명 모음 항목 toohello Azure 대시보드를 고정할 수 있습니다. toopin hello 자격 증명 모음 항목 목록, 오른쪽 클릭 hello 항목 및 선택에서 자격 증명 모음 항목을 **Pin toodashboard**합니다.
   >
   >
2. Hello에 **백업 항목** 블레이드에서 hello 항목 tooopen hello 자격 증명 모음 항목 대시보드를 클릭 합니다.

    ![백업 항목 타일](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    hello 자격 증명 모음 항목 대시보드 및 해당 **설정을** 블레이드를 엽니다.

    ![설정 블레이드에서 백업 항목 대시보드](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    Hello 자격 증명 모음 항목 대시보드에서 같은 여러 주요 관리 작업을 수행할 수 있습니다.

   * 정책 변경 또는 새 백업 정책 만들기 <br\>
   * 복원 지점 확인 및 해당 일관성 상태 확인 <br\>
   * 가상 컴퓨터의 주문형 백업<br\>
   * 가상 컴퓨터 보호 중지 <br\>
   * 가상 컴퓨터 보호 재개 <br\>
   * 백업 데이터(또는 복구 지점) 삭제 <br\>
   * [백업 디스크 복원](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\>

다음 절차를 수행 하는 hello에 대 한 시작 지점 hello는 hello 자격 증명 모음 항목 대시보드입니다.

## <a name="manage-backup-policies"></a>백업 정책 관리
1. Hello에 [자격 증명 모음 항목 대시보드](backup-azure-manage-vms.md#open-a-vault-item-dashboard), 클릭 **모든 설정을** tooopen hello **설정을** 블레이드입니다.

    ![백업 정책 블레이드](./media/backup-azure-manage-vms/all-settings-button.png)
2. Hello에 **설정** 블레이드에서 클릭 **백업 정책** tooopen 해당 블레이드에 합니다.

    Hello 블레이드에서 hello 백업 빈도 보존 범위 세부 정보가 표시 됩니다.

    ![백업 정책 블레이드](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. Hello에서 **백업 정책을 선택** 메뉴:

   * toochange 정책에 다른 정책을 선택 하 고 클릭 **저장**합니다. hello 새 정책이 즉시 적용 된 toohello 자격 증명 모음입니다. <br\>
   * 클라이언트는 정책을 toocreate 선택 **새로 만들기**합니다.

     ![가상 컴퓨터 백업](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     백업 정책을 만드는 지침은 [백업 정책 정의](backup-azure-manage-vms.md#defining-a-backup-policy)를 참조하세요.

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> 백업 정책, 관리 하는 동안 확인 되었는지 toofollow hello [모범 사례](backup-azure-vms-introduction.md#best-practices) 최적의 성능을 위해서는 백업
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a>가상 컴퓨터의 주문형 백업
보호를 위해 구성한 후에는 가상 컴퓨터의 주문형 백업을 수행할 수 있습니다. Hello 초기 백업을 보류 중이면 변경 집합 요청 시 백업을 hello 복구 서비스 자격 증명 모음에 hello 가상 컴퓨터의 전체 복사본을 만듭니다. Hello 초기 백업이 완료 되 면 요청 시 백업을 hello 이전 스냅숏 toohello 복구 서비스 자격 증명 모음에서에서 변경 내용을만 전송 합니다. 즉, 이후의 백업은 항상 증분형입니다.

> [!NOTE]
> 요청 시 백업에 대 한 보존 범위 hello은 hello 정책에 hello 일일 백업 지점에 대해 지정 된 hello 보존 값입니다. 일일 백업 지점 없는 선택 하는 경우 hello 주간 백업 지점 사용 됩니다.
>
>

가상 컴퓨터의 주문형 tootrigger 백업:

* Hello에 [자격 증명 모음 항목 대시보드](backup-azure-manage-vms.md#open-a-vault-item-dashboard), 클릭 **지금 백업**합니다.

    ![지금 백업 아이콘](./media/backup-azure-manage-vms/backup-now-button.png)

    hello 포털 toostart 주문형 백업 작업을 사용 하지 않겠다고 않았는지 확인 합니다. 클릭 **예** toostart hello에 대 한 백업 작업입니다.

    ![지금 백업 아이콘](./media/backup-azure-manage-vms/backup-now-check.png)

    hello 백업 작업에는 복구 지점을 만듭니다. hello 복구 지점의 보존 범위 hello hello 가상 컴퓨터와 연결 된 hello 정책에 지정 된 보존 범위와 같은 hello 됩니다. hello 자격 증명 모음 대시보드에서 hello 작업에 대 한 tootrack hello 진행률 클릭 hello **백업 작업이** 바둑판식으로 배열입니다.  

## <a name="stop-protecting-virtual-machines"></a>가상 컴퓨터 보호 중지
가상 컴퓨터 보호 toostop을 선택 하면 tooretain hello 복구 지점을 사용 하려는 경우 묻는 메시지가 표시 됩니다. 두 가지가 toostop 보호 가상 컴퓨터:

* 모든 미래의 백업 작업을 정지하고 모든 복구 지점을 삭제, 또는
* 이후의 모든 백업 작업을 중단 하지만 hello 복구 지점 유지 <br/>

저장소를 복구 지점 hello을 그대로 유지 하면서와 관련 된 비용이 듭니다. 그러나 복구 지점을 hello를 끝낼 hello 혜택은 나중 hello 가상 컴퓨터를 복원할 수 있습니다 원하는 경우. 복구 지점을 hello를 끝낼 hello 비용에 대 한 정보를 참조 hello [가격 정보](https://azure.microsoft.com/pricing/details/backup/)합니다. Toodelete 모든 복구 지점을 선택 하면 hello 가상 컴퓨터를 복원할 수 없습니다.

가상 컴퓨터에 대 한 toostop 보호:

1. Hello에 [자격 증명 모음 항목 대시보드](backup-azure-manage-vms.md#open-a-vault-item-dashboard), 클릭 **백업 중지**합니다.

    ![백업 중지 단추](./media/backup-azure-manage-vms/stop-backup-button.png)

    hello 백업 중지 블레이드를 엽니다.

    ![백업 중지 블레이드](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. Hello에 **백업 중지** 블레이드에서 tooretain 또는 delete 백업 데이터 hello 여부를 선택 합니다. hello 정보 상자 사용자가 선택한 방법에 대 한 세부 정보를 제공 합니다.

    ![보호 중지](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. Tooretain hello 백업 데이터를 선택한 경우에 4 toostep을 건너뜁니다. Toodelete 백업 데이터를 선택한 경우 toostop hello에 대 한 백업 작업을 원하는 hello 항목의 형식 hello 이름은-hello 복구 지점이 삭제를 확인 합니다.

    ![백업 확인](./media/backup-azure-manage-vms/item-verification-box.png)

    Hello 항목 이름이 확실 하지 않은 경우 hello 느낌표 tooview hello 이름 위로 이동 합니다. 또한 hello hello 항목 이름은 아래 **백업 중지** hello hello 블레이드 위쪽에 있습니다.
4. 필요에 따라 **이유** 또는 **주석**을 제공합니다.
5. hello toostop hello 현재 항목에 대 한 백업 작업 클릭 ![백업 중지 단추](./media/backup-azure-manage-vms/stop-backup-button-blue.png)

    알림 메시지를 사용 하면 hello 백업 작업이 중지 된 알 수 있습니다.

    ![보호 중지 확인](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a>가상 컴퓨터 보호 재개
경우 hello **백업 데이터 보관** 옵션이 hello 가상 컴퓨터에 대 한 보호 중지 되었을 때 가능한 tooresume 보호 됩니다. 경우 hello **백업 데이터 삭제** 옵션을 선택 했습니다. 다음 hello 가상 컴퓨터에 대 한 보호를 다시 시작할 수 없습니다.

hello 가상 컴퓨터에 대 한 tooresume 보호

1. Hello에 [자격 증명 모음 항목 대시보드](backup-azure-manage-vms.md#open-a-vault-item-dashboard), 클릭 **백업 다시 시작**합니다.

    ![보호 다시 시작](./media/backup-azure-manage-vms/resume-backup-button.png)

    hello 백업 정책 블레이드에서가 열립니다.

   > [!NOTE]
   > Hello 가상 컴퓨터를 다시 보호 된 가상 컴퓨터를 보호 처음 hello 정책 보다 다른 정책을 선택할 수 있습니다.
   >
   >
2. Hello 단계에 따라 [백업 정책 관리](backup-azure-manage-vms.md#manage-backup-policies) hello 가상 컴퓨터에 대 한 tooassign hello 정책입니다.

    Hello 백업 정책이 적용 된 toohello 가상 컴퓨터를 hello 메시지의 뒤에 표시 됩니다.

    ![성공적으로 보호된 VM](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a>백업 데이터 삭제
Hello 하는 동안 가상 컴퓨터와 연결 된 hello 백업 데이터를 삭제할 수 있습니다 **백업 중지** 작업, 백업 작업이 완료 된 hello 후 언제 든 지 또는 합니다. 유용한 toowait 일 또는 주로 hello 복구 지점도 삭제 하기 전에 못할 수도 있습니다. 백업 데이터를 삭제할 때 복구 지점, 복원와 달리 특정 복구 지점 toodelete를 선택할 수 없습니다. Toodelete 백업 데이터를 선택할 경우 hello 항목과 연결 된 모든 복구 지점을 삭제 합니다.

hello 다음 절차에서는 가정 hello 가상 컴퓨터에 대 한 백업 작업 hello 중지 되었거나 사용할 수 없습니다. Hello 백업 작업이 해제 되 면 hello **백업 다시 시작** 및 **Delete 백업** hello 자격 증명 모음 항목 대시보드에서 사용할 수 있는 옵션입니다.

![다시 시작 및 삭제 단추](./media/backup-azure-manage-vms/resume-delete-buttons.png)

hello로 가상 컴퓨터에서 백업 데이터 toodelete *백업 사용 안 함*:

1. Hello에 [자격 증명 모음 항목 대시보드](backup-azure-manage-vms.md#open-a-vault-item-dashboard), 클릭 **Delete 백업**합니다.

    ![VM 유형](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    hello **백업 데이터 삭제** 블레이드를 엽니다.

    ![VM 유형](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. 형식 hello 이름 toodelete hello 복구 지점을 만들려는 hello 항목 tooconfirm 합니다.

    ![백업 확인](./media/backup-azure-manage-vms/item-verification-box.png)

    Hello 항목 이름이 확실 하지 않은 경우 hello 느낌표 tooview hello 이름 위로 이동 합니다. 또한 hello hello 항목 이름은 아래 **백업 데이터 삭제** hello hello 블레이드 위쪽에 있습니다.
3. 필요에 따라 **이유** 또는 **주석**을 제공합니다.
4. hello toodelete hello 현재 항목에 대 한 백업 데이터 클릭 ![백업 중지 단추](./media/backup-azure-manage-vms/delete-button.png)

    알림 메시지를 사용 하면 hello 백업 데이터가 삭제 되었는지 알 수 있습니다.

## <a name="next-steps"></a>다음 단계
복구 지점에서 가상 컴퓨터를 다시 만드는 방법에 대한 내용은 [Azure VM 복원](backup-azure-restore-vms.md)을 확인하세요. 가상 컴퓨터 보호에 대 한 정보를 보려면 참고 [소개: Vm tooa 복구 서비스 자격 증명 모음에 백업](backup-azure-vms-first-look-arm.md)합니다. 이벤트 모니터링에 대한 자세한 내용은 [Azure 가상 컴퓨터 백업에 대한 경고 모니터링](backup-azure-monitor-vms.md)을 참조하세요.
