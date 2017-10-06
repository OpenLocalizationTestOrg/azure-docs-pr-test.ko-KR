---
title: " Azure에서 Recovery Services 자격 증명 모음 삭제 | Microsoft Docs "
description: "어떻게 toodelete Azure 백업 및 복구 서비스 자격 증명 모음입니다. 백업 자격 증명 모음은 Azure 클라우드 자격 증명 모음 또는 Azure 복구 자격 증명 모음이라고 할 수 있습니다. 문제 해결 hello 클래식 포털 또는 Azure 포털에서 백업 자격 증명 모음을 삭제할 수 없습니다."
services: service-name
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 5fa08157-2612-4020-bd90-f9e3c3bc1806
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: markgal;trinadhk
ms.openlocfilehash: 9047f50f4b2c991fbf2454ddcad08073ec7cd975
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-recovery-services-vault"></a>Recovery Services 자격 증명 모음 삭제
hello Azure 백업 서비스에는 두 가지 유형의 자격 증명 모음-hello 백업 자격 증명 모음 및 hello 복구 서비스 자격 증명 모음에 있습니다. hello 백업 자격 증명 모음 먼저 도착 합니다. 다음 복구 서비스 자격 증명 모음에 hello toosupport 확장 hello 리소스 관리자 배포와 함께 제공 되었습니다. Hello 때문에 확장 된 기능 및 hello 자격 증명 모음을 삭제 한 백업 또는 복구 서비스 자격 증명 모음에 저장 해야 하는 hello 정보 종속성 혼동 될 수 있습니다. 이 문서에서는 toodelete hello hello 클래식 포털 및 hello Azure 포털에서 자격 증명 모음는 방법을 설명 합니다.  

| **배포 유형** | **포털** | **자격 증명 모음 이름** |
| --- | --- | --- |
| 클래식 |클래식 |백업 자격 증명 모음 |
| 리소스 관리자 |Azure |복구 서비스 자격 증명 모음 |

> [!NOTE]
> 백업 자격 증명 모음을 사용하여 Resource Manager에서 배포한 솔루션을 보호할 수는 없습니다. 그러나 복구 서비스 자격 증명 모음을 사용할 수 tooprotect 일반적 서버 및 Vm을 배포 합니다.  
>

> [!IMPORTANT]
> 이제 사용자 백업 자격 증명 모음 tooRecovery 서비스 자격 증명 모음을 업그레이드할 수 있습니다. 자세한 내용은 hello 문서 참조 [복구 서비스 자격 증명 모음에 백업 자격 증명 모음 tooa 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md)합니다. Microsoft는 것이 권장 tooupgrade 백업 tooRecovery 서비스 자격 증명 모음 자격 증명 모음입니다.<br/> **2017 년 10 월 15**, 수 toouse PowerShell toocreate 백업 자격 증명 모음은 더 이상 됩니다. <br/> **2017년 11월 1일 시작**:
>- 나머지 모든 백업 자격 증명 모음을 자동으로 업그레이드 된 tooRecovery 서비스 자격 증명 모음 됩니다.
>- 하면 hello 클래식 포털에서 수 tooaccess 백업 데이터 수 없습니다. 대신, 복구 서비스 자격 증명 모음에 hello Azure 포털 tooaccess 백업 데이터를 사용 합니다.
>

이 문서에서는 hello 용어, 자격 증명 모음, toorefer toohello 제네릭 형식 hello 백업 자격 증명 모음 또는 복구 서비스 자격 증명 모음으로 사용합니다. Hello 자격 증명 모음 간에 필요한 toodistinguish 되었을 때 hello 정식 이름, 백업 자격 증명 모음 또는 복구 서비스 자격 증명 모음을 사용 합니다.

## <a name="deleting-a-recovery-services-vault"></a>Recovery Services 자격 증명 모음 삭제
1 단계 프로세스-복구 서비스 자격 증명 모음을 삭제는 *hello 자격 증명 모음 리소스가 없습니다. 제공 된*합니다. 복구 서비스 자격 증명 모음을 삭제 하려면 먼저 제거 하거나 hello 자격 증명 모음에 있는 모든 리소스를 삭제 해야 합니다. Toodelete 리소스가 포함 된 자격 증명 모음을 시도 하면 다음 이미지는 hello와 같은 오류 메시지가.

![자격 증명 모음 삭제 오류](./media/backup-azure-delete-vault/vault-deletion-error.png) <br/>

Hello 리소스 hello 자격 증명 모음에서을 지우면 될 때까지 클릭 하면 **을 다시 시도** 생성 hello 동일한 오류가 발생 합니다. 이 오류 메시지에서 나올 수, 클릭 **취소** 및 사용 하 여 hello 다음 단계 hello 자격 증명 모음에 toodelete hello 리소스입니다.

### <a name="removing-hello-items-from-a-vault-protecting-a-vm"></a>VM을 보호 하는 자격 증명 모음에서 hello 항목 제거
Hello 복구 서비스 자격 증명 모음을 열고 이미 있는 경우 toohello 두 번째 단계를 건너뜁니다.

1. Hello Azure 포털을 열고 hello 대시보드에서에서 원하는 toodelete hello 자격 증명 모음을 엽니다.

   복구 서비스 자격 증명 모음에 hello hello 허브 메뉴에서 대시보드를 toohello 고정 없는 경우, 클릭 **더 서비스** hello 리소스 목록에 입력 하 고 **복구 서비스**합니다. 입력을 시작할 때 hello 사용자 입력에 따라 필터를 나열 합니다. **복구 서비스 자격 증명 모음**을 클릭합니다.

   ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-azure-delete-vault/open-recovery-services-vault.png) <br/>

   복구 서비스 자격 증명 모음 hello 목록이 표시 됩니다. Hello 목록에서 원하는 toodelete hello 자격 증명 모음을 선택 합니다.

   ![목록에서 자격 증명 모음 선택](./media/backup-azure-work-with-vaults/choose-vault-to-delete.png)
2. Hello에 자격 증명 모음 보기 봐 hello에 **Essentials** 창. 자격 증명 모음, toodelete 모든 보호 된 항목이 있을 수 없습니다. 아래에서 0이 아닌 숫자로 표시 되 면 **백업 항목** 또는 **관리 서버를 백업**, hello 자격 증명 모음을 삭제 하려면 먼저 해당 항목을 제거 해야 합니다.

    ![보호된 항목에 대한 필수 창 확인](./media/backup-azure-delete-vault/contoso-bkpvault-settings.png)

    백업 항목으로 간주 됩니다 hello에 나열 된 Vm 및 파일/폴더 **백업 항목** hello Essentials 창의 영역입니다. DPM 서버 hello에 나열 된 **백업 관리 서버** hello Essentials 창의 영역입니다. **복제 된 항목이** toohello Azure Site Recovery 서비스와 관련 됩니다.
3. hello 제거 toobegin hello 자격 증명 모음, hello 자격 증명 모음에 찾기 hello 항목에서에서 항목을 보호 합니다. Hello 자격 증명 모음 대시보드 클릭 **설정**, 클릭 하 고 **항목 백업** tooopen 해당 블레이드에 합니다.

    ![목록에서 자격 증명 모음 선택](./media/backup-azure-delete-vault/open-settings-and-backup-items.png)

    hello **백업 항목** 블레이드는 별도 목록, hello 항목 형식에 따라: Azure 가상 컴퓨터 또는 파일 폴더 (이미지 참조). hello 기본 항목 형식 표시 된 목록은 Azure 가상 컴퓨터입니다. tooview hello 파일 폴더의에서 항목 목록에 hello 자격 **파일 폴더** hello 드롭 다운 메뉴에서 합니다.
4. VM 보호 hello 자격 증명 모음에서 항목을 삭제할 수 있습니다, 전에 hello 항목의 백업 작업을 중지 하 고 hello 복구 지점 데이터를 삭제 합니다. 각 항목 hello 자격 증명 모음에 대해 다음이 단계를 따르십시오.

    a. Hello에 **백업 항목** 블레이드에서 마우스 오른쪽 단추로 클릭 hello 항목, hello 상황에 맞는 메뉴에서 선택 **백업 중지**합니다.

    ![hello 백업 작업을 중지 합니다.](./media/backup-azure-delete-vault/stop-the-backup-process.png)

    hello 백업 중지 블레이드를 엽니다.

    b. Hello에 **백업 중지** 블레이드 hello에서 **옵션을 선택** 메뉴 선택 **백업 데이터 삭제** > hello 항목의 형식 hello 이름 >을 클릭 하 고 **중지 백업**합니다.

    항목 hello tooverify toodelete를 원하는 형식 hello 이름을 것입니다. hello **백업 중지** hello 항목을 확인 한 후 단추를 활성화 합니다. Hello 선택한 hello 백업 항목의 hello 대화 상자 tootype hello 이름, 표시 되지 않으면 **백업 데이터 보관** 옵션입니다.

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/stop-backup-blade-delete-backup-data.png)

    필요에 따라 hello 데이터를 삭제 하는 이유와 설명을 추가 하는 이유를 제공할 수 있습니다. 클릭 한 후 **백업 중지**, toodelete hello 자격 증명 모음을 시도 하기 전에 hello 삭제 작업 toocomplete 허용 합니다. 완료 된 작업 hello tooverify, hello Azure 메시지 확인 ![백업 데이터를 삭제](./media/backup-azure-delete-vault/messages.png)합니다. <br/>
    Hello 작업이 완료 되 면 hello 백업 프로세스를 중지 했 고 해당 항목에 대 한 hello 백업 데이터가 삭제 되었다는 메시지가 나타납니다.

    c. Hello에 hello 목록에서 항목을 삭제 한 후 **백업 항목** 메뉴를 클릭 하 여 **새로 고침** hello 자격 증명 모음에 있는 항목에 남은 toosee hello 합니다.

      ![백업 데이터 삭제](./media/backup-azure-delete-vault/empty-items-list.png)

      Hello 목록에 항목이 없는 경우 스크롤 toohello **Essentials** hello 백업 자격 증명 모음 블레이드에서 창. 어떤 **백업 항목**, **백업 관리 서버** 또는 **복제된 항목**도 나열되지 않아야 합니다. 항목이 hello 자격 증명 모음에 여전히 나타날, toostep 3을 반환 하 고 다른 항목 유형 목록을 선택 합니다.  
5. Hello 자격 증명 모음 도구 모음에 항목이 더 이상 있을 때 클릭 **삭제**합니다.

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/delete-vault.png)
6. toodelete hello 자격 증명 모음을 사용 하지 않겠다고 tooverify 클릭 **예**합니다.

    hello 자격 증명 모음 삭제 되 고 hello 포털 반환 toohello **새로** 서비스 메뉴.

## <a name="what-if-i-stopped-hello-backup-process-but-retained-hello-data"></a>경우에 어떻게 hello 백업 프로세스를 중지 합니다.이 있지만 보관 된 hello 데이터?
하지만 실수로 hello 백업 프로세스를 중지 한 경우 *유지* hello 데이터 hello 자격 증명 모음을 삭제 하기 전에 hello 백업 데이터 삭제 해야 합니다. toodelete hello 백업 데이터:

1. Hello에 **백업 항목** 블레이드에서 마우스 오른쪽 단추로 클릭 hello 항목, hello 상황에 맞는 메뉴에서을 클릭 하 여 **백업 데이터를 삭제**합니다.

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/delete-backup-data-menu.png)

    hello **백업 데이터 삭제** 블레이드를 엽니다.
2. Hello에 **백업 데이터 삭제** hello 항목과 클릭의 hello 이름을 입력 합니다 블레이드 **삭제**합니다.

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/delete-retained-vault.png)

    Hello 데이터를 삭제 한 후 4 c toostep 돌아간 hello 프로세스를 계속 합니다.

## <a name="delete-a-vault-used-tooprotect-a-dpm-server"></a>사용 되는 자격 증명 모음 tooprotect DPM 서버를 삭제 합니다.
사용 되는 자격 증명 모음 tooprotect DPM 서버를 삭제 하기 전에 생성 된 모든 복구 지점이 선택을 취소 하 고 hello 서버 hello 자격 증명 모음에서 등록을 취소 합니다.

보호 그룹과 연결 된 toodelete hello 데이터:

1. Hello DPM 관리자 콘솔에서에서 클릭 **보호** > 보호 그룹을 선택 > 선택 hello 보호 그룹 구성원 > hello 도구 리본에서을 클릭 하 고 **제거**합니다.

  보호 그룹 구성원 tooactivate hello 선택 hello **제거** hello 도구 리본에서 단추입니다. Hello 예제 hello 멤버는 **dummyvm9**합니다. tooselect hello 보호 그룹의 여러 멤버 hello Ctrl 키를 누른 채 hello 멤버를 클릭 합니다.

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/az-portal-delete-protection-group.png)

    hello **보호 중지** 대화 상자가 열립니다.
2. Hello에 **보호 중지** 대화 상자에서 **보호 된 데이터 삭제**를 클릭 하 고 **보호 중지**합니다.

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/delete-dpm-protection-group.png)

    toodelete 자격 증명 모음을 선택 취소 하거나 삭제 해야, 보호 된 데이터의 hello 자격 증명 모음입니다. 복구 지점 및 hello 보호 그룹의 데이터를 hello 수에 따라 소요 아무 곳 이나 몇 초 tooseveral 분 toodelete hello 데이터에서. hello **보호 중지** hello 작업이 완료 되 면 hello 상태 대화 상자에 표시 합니다.

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/success-deleting-protection-group.png)
3. 모든 보호 그룹의 모든 멤버에 대해 이 프로세스를 계속합니다.

    모든 보호된 데이터와 보호 그룹을 제거합니다.
4. Hello 보호 그룹에서 모든 멤버를 삭제 한 후 Azure 포털 toohello를 전환 합니다. Hello 자격 증명 모음 대시보드를 열고 없는지 확인 없는 **백업 항목**, **관리 서버를 백업**, 또는 **복제 항목**합니다. Hello 자격 증명 모음 도구 모음에서 **삭제**합니다.

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/delete-vault.png)

    백업 관리 서버를 등록 toohello 자격 증명 모음에 있는 경우 hello 자격 증명 모음에 데이터가 없는 경우에 hello 자격 증명 모음을 삭제할 수 없습니다. Hello 자격 증명 모음에 연결 하는 hello 백업 관리 서버를 삭제 되었지만 hello에 나열 된 서버가 없는 경우 **Essentials** 창 참조 [찾기 hello 백업 관리 서버 등록된 toohello 자격 증명 모음](backup-azure-delete-vault.md#find-the-backup-management-servers-registered-to-the-vault) .
5. toodelete hello 자격 증명 모음을 사용 하지 않겠다고 tooverify 클릭 **예**합니다.

    hello 자격 증명 모음 삭제 되 고 hello 포털 반환 toohello **새로** 서비스 메뉴.

## <a name="delete-a-vault-used-tooprotect-a-production-server"></a>사용 되는 자격 증명 모음 tooprotect 프로덕션 서버를 삭제 합니다.
사용 되는 자격 증명 모음 tooprotect 프로덕션 서버를 삭제 하기 전에 삭제 하거나 hello 서버 hello 자격 증명 모음에서 등록을 취소 해야 합니다.

toodelete hello 프로덕션 hello 자격 증명 모음과 연결 된 서버:

1. Hello Azure 포털에서에서 자격 증명 모음 대시보드 hello 열고 클릭 **설정** > **백업 인프라** > **프로덕션 서버**합니다.

    ![프로덕션 서버 블레이드 열기](./media/backup-azure-delete-vault/delete-production-server.png)

    hello **프로덕션 서버** 블레이드가 열리고 hello 자격 증명 모음에 모든 프로덕션 서버를 나열 합니다.

    ![프로덕션 서버 목록](./media/backup-azure-delete-vault/list-of-production-servers.png)
2. Hello에 **프로덕션 서버** 블레이드에서 hello 서버를 마우스 오른쪽 단추로 클릭 하 고 클릭 **삭제**합니다.

    ![프로덕션 서버 삭제 ](./media/backup-azure-delete-vault/delete-server-on-production-server-blade.png)

    hello **삭제** 블레이드를 엽니다.

    ![프로덕션 서버 삭제 ](./media/backup-azure-delete-vault/delete-blade.png)
3. Hello에 **삭제** 블레이드에서 hello 서버 이름을 확인 하 고 클릭 **삭제**합니다. 서버 hello tooactivate hello 이름을 올바르게 지정 해야 **삭제** 단추입니다.

    Hello 자격 증명 모음 삭제 되 면 hello 자격 증명 모음 삭제 되었음을 알리는 메시지가 나타납니다. Hello 자격 증명 모음에 모든 서버를 삭제 한 후 뒤로 toohello Essentials 창을 hello 자격 증명 모음 대시보드를 스크롤하십시오.
4. Hello 자격 증명 모음 대시보드에 없는지 확인 없는 **백업 항목**, **관리 서버를 백업**, 또는 **복제 항목**합니다. Hello 자격 증명 모음 도구 모음에서 **삭제**합니다.
5. toodelete hello 자격 증명 모음을 사용 하지 않겠다고 tooverify 클릭 **예**합니다.

    hello 자격 증명 모음 삭제 되 고 hello 포털 반환 toohello **새로** 서비스 메뉴.

## <a name="delete-a-backup-vault-in-classic-portal"></a>클래식 포털에서 백업 자격 증명 모음 삭제
hello 다음 지침은에 hello 클래식 포털에서 백업 자격 증명 모음을 삭제 합니다. Hello 백업 자격 증명 모음을 삭제 하려면 먼저 있습니다 hello 복구 지점을 삭제 해야 또는 백업 항목 및 hello 등록 된 서버를 제거 합니다. hello 등록 된 서버를 Windows Server hello, 워크스테이션 또는 등록 된 toohello 자격 증명 모음에 있던 가상 컴퓨터가 있습니다.

1. 열기 hello [클래식 포털](https://manage.windowsazure.com)합니다.

2. 백업 자격 증명 모음의 hello 목록에서 원하는 toodelete hello 자격 증명 모음을 선택 합니다.

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/classic-portal-delete-vault-open-vault.png)

    hello 자격 증명 모음 대시보드를 엽니다. Hello 자격 증명 모음과 연결 하는 Windows 서버 및/또는 Azure 가상 컴퓨터의 hello 숫자를 확인 합니다. 또한 hello Azure에서 사용 되는 총 저장소를 살펴봅니다. 모든 백업 작업을 중지 하 고 hello 자격 증명 모음을 삭제 하기 전에 모든 데이터를 삭제 합니다.

3. Hello 클릭 **보호 된 항목** 탭을 클릭 한 다음 **보호 중지**

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/classic-portal-delete-vault-stop-protect.png)

    hello **'자격 증명 모음'의 보호를 중지** 대화 상자가 나타납니다.
4. Hello에 **'자격 증명 모음'의 보호를 중지** 대화 상자에서 확인 **연결 된 백업 데이터 삭제** 클릭 ![확인 표시](./media/backup-azure-delete-vault/checkmark.png)합니다. <br/>
    필요에 따라 보호를 중지하는 이유를 선택하고 메모를 제공할 수 있습니다.

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/classic-portal-delete-vault-verify-stop-protect.png)

    Hello 자격 증명 모음의 hello 항목을 삭제 한 후 자격 증명 모음 hello 비어 있게 됩니다.

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/classic-portal-delete-vault-post-delete-data.png)
5. 탭의 hello 목록에서 클릭 **등록 된 항목**합니다. hello **형식** 드롭 다운 메뉴에서 등록 된 서버 toohello 자격 증명 모음의 toochoose hello 입력 수 있습니다. hello 형식은 Windows Server 또는 Azure 가상 컴퓨터를 수 있습니다. 다음 예제는 hello에서 hello 가상 컴퓨터 등록된 toohello 자격 증명 모음을 선택 하 고 클릭 **등록 취소**합니다.

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/classic-portal-unregister.png)

  Windows 서버 hello에 대 한 toodelete hello 등록 하려는 경우 **형식** 드롭 다운 메뉴 **Windows Server**, 클릭 ![확인 표시](./media/backup-azure-delete-vault/checkmark.png) toorefresh hello 화면 클릭 하 고 **삭제**합니다. <br/>

  ![Windows Server 선택](./media/backup-azure-delete-vault/select-windows-server.png)

6. 탭의 hello 목록에서 클릭 **대시보드** tooopen 탭입니다. 등록 된 서버 또는 hello 클라우드에서 보호 되는 Azure 가상 컴퓨터에 없는지 확인 합니다. 또한 저장소에 데이터가 없는지도 확인합니다. 클릭 **삭제** toodelete hello 자격 증명 모음입니다.

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/classic-portal-list-of-tabs-dashboard.png)

    hello 삭제 백업 자격 증명 모음 확인 화면이 열립니다. Hello 자격 증명 모음을 삭제 하는 이유는 옵션을 선택 하 고 클릭 ![확인 표시](./media/backup-azure-delete-vault/checkmark.png)를 입력합니다. <br/>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/classic-portal-delete-vault-confirmation-1.png)

    hello 자격 증명 모음 삭제 되 고, toohello 클래식 포털 대시보드를 반환 합니다.

### <a name="find-hello-backup-management-servers-registered-toohello-vault"></a>자격 증명 모음 백업을 관리 서버 등록된 toohello hello 찾기
자격 증명 모음 tooa 등록 된 서버를 여러 개 있는 경우는 것이 어려운 tooremember 해당 합니다. toosee hello 서버 toohello 자격 증명 모음에 등록 하 고 삭제 합니다.

1. 자격 증명 모음 대시보드 열기 hello 합니다.
2. Hello에 **Essentials** 창에서 클릭 **설정을** tooopen 해당 블레이드에 합니다.

    ![설정 블레이드 열기](./media/backup-azure-delete-vault/backup-vault-click-settings.png)
3. Hello에 **설정 블레이드에서**, 클릭 **백업 인프라**합니다.
4. Hello에 **백업 인프라** 블레이드에서 클릭 **백업 관리 서버를**합니다. hello 백업 관리 서버를 블레이드를 엽니다.

    ![백업 관리 서버 목록](./media/backup-azure-delete-vault/list-of-backup-management-servers.png)
5. toodelete hello 목록에서 서버 hello hello 서버 이름을 마우스 오른쪽 단추로 클릭 **삭제**합니다.
    hello **삭제** 블레이드를 엽니다.
6. Hello에 **삭제** 블레이드에서 hello hello 서버 이름을 제공 합니다. 긴 이름인 경우 다음에 복사 및 hello 백업 관리 서버 목록에서 붙여 수 있습니다. 그런 다음 **삭제**를 클릭합니다.  
