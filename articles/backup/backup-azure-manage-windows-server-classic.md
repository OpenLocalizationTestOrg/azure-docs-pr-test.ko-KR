---
title: "Azure 백업 자격 증명 모음 aaaManage hello 클래식 배포 모델을 사용 하 여 Azure 서버 및 | Microsoft Docs"
description: "이 자습서 toolearn toomanage Azure 백업 자격 증명 모음 및 서버를 사용 합니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: f175eb12-0905-437f-91fd-eaee03ab6e81
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: markgal;
ms.openlocfilehash: 6c38b04f4a76604bfd639a9b2d58237ce44e2386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-hello-classic-deployment-model"></a>Azure 백업 자격 증명 모음 및 hello 클래식 배포 모델을 사용 하 여 서버 관리
> [!div class="op_single_selector"]
> * [리소스 관리자](backup-azure-manage-windows-server.md)
> * [클래식](backup-azure-manage-windows-server-classic.md)
>
>

이 문서에서 hello Azure 클래식 포털을 통해 사용할 수 있는 hello 백업 관리 작업 및 hello Microsoft Azure 백업 에이전트의 개요를 찾을 수 있습니다.

> [!IMPORTANT]
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.

> [!IMPORTANT]
> 이제 사용자 백업 자격 증명 모음 tooRecovery 서비스 자격 증명 모음을 업그레이드할 수 있습니다. 자세한 내용은 hello 문서 참조 [복구 서비스 자격 증명 모음에 백업 자격 증명 모음 tooa 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md)합니다. Microsoft는 것이 권장 tooupgrade 백업 tooRecovery 서비스 자격 증명 모음 자격 증명 모음입니다.<br/> 2017 년 10 월 15 후 PowerShell toocreate 백업 자격 증명 모음을 사용할 수 없습니다. **2017년 11월 1일까지**:
>- 모든 나머지 백업 자격 증명 모음을 자동으로 업그레이드 된 tooRecovery 서비스 자격 증명 모음 됩니다.
>- 하면 hello 클래식 포털에서 수 tooaccess 백업 데이터 수 없습니다. 대신, 복구 서비스 자격 증명 모음에 hello Azure 포털 tooaccess 백업 데이터를 사용 합니다.
>

## <a name="management-portal-tasks"></a>관리 포털 작업
1. Toohello 로그인 [관리 포털](https://manage.windowsazure.com)합니다.
2. 클릭 **복구 서비스**, 백업 자격 증명 모음 tooview hello 빠른 시작 페이지의 hello 이름을 클릭 합니다.

    ![복구 서비스](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

Hello 빠른 시작 페이지의 hello 위쪽 hello 옵션을 선택 하면 hello 사용 가능한 관리 작업을 볼 수 있습니다.

![관리 탭](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a>대시보드
선택 **대시보드** toosee hello 사용 개요에 대 한 hello 서버입니다. hello **사용 개요** 포함 됩니다.

* Windows 서버 hello 수 toocloud 등록
* 클라우드에서 보호 되는 Azure 가상 컴퓨터의 hello 수
* hello Azure에서 사용 되는 총 저장소
* 최근 작업의 hello 상태

Hello hello 대시보드 맨 아래에 hello 다음 작업을 수행할 수 있습니다.

* **인증서 관리** -인증서를 사용 하는 tooregister hello 서버 인지 다음이 tooupdate hello 인증서를 사용 하 여 하는 경우. 저장소 자격 증명을 사용하는 경우에는 **인증서 관리**를 사용해서는 안 됩니다.
* **삭제** -삭제 hello 현재 백업 자격 증명 모음입니다. 백업 자격 증명 모음이 더 이상 사용 중인 경우 toofree 저장 공간을 삭제할 수 없습니다. **삭제** hello 자격 증명 모음에서 등록 된 모든 서버를 삭제 한 후에 사용할 수 있습니다.

![백업 대시보드 작업](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a>등록된 항목
선택 **등록 된 항목** 한 hello 서버 tooview hello 이름을 toothis 자격 증명 모음을 등록 합니다.

![등록된 항목](./media/backup-azure-manage-windows-server-classic/registered-items.png)

hello **형식** 필터 tooAzure 가상 컴퓨터의 기본값입니다. 자격 증명 모음 등록된 toothis hello 서버 tooview hello 이름 선택 **Windows server** hello에서 드롭다운 메뉴.

여기에서 hello 다음 작업을 수행할 수 있습니다.

* **재등록을 허용** -사용할 수는 서버에 대해이 옵션을 선택 하는 경우 hello **등록 마법사** hello 온-프레미스 Microsoft Azure 백업 에이전트 tooregister hello 서버를 두 번째로 hello 백업 자격 증명 모음에 . Hello 인증서 또는 서버를 다시 작성 toobe를 갖는 경우에 tooan 오류가 인해 toore 레지스터를 할 수 있습니다.
* **삭제** -hello 백업 자격 증명 모음에서 서버를 삭제 합니다. 모든 hello 서버와 관련 된 hello 저장 데이터가 즉시 삭제 됩니다.

    ![등록된 항목 작업](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a>보호된 항목
선택 **보호 된 항목** hello 서버에서 백업 된 tooview hello 항목입니다.

![보호된 항목](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a>구성
Hello에서 **구성** 탭 hello 적절 한 저장소 중복 옵션을 선택할 수 있습니다. hello 최상의 시간 tooselect hello 저장소 중복 옵션은 자격 증명 모음을 만드는 바로 뒤와 모든 컴퓨터는 등록 된 tooit 전에 합니다.

> [!WARNING]
> 항목에 대 한 자격 증명 모음 등록된 toohello를 수행한 후 hello 저장소 중복 옵션이 잠겨 있으며 수정할 수 없습니다.
>
>

![구성](./media/backup-azure-manage-windows-server-classic/configure.png)

[저장소 중복](../storage/common/storage-redundancy.md)에 대한 자세한 내용은 이 문서를 참조하세요.

## <a name="microsoft-azure-backup-agent-tasks"></a>Microsoft Azure 백업 에이전트 작업
### <a name="console"></a>콘솔
열기 hello **Microsoft Azure 백업 에이전트** (에 대 한 컴퓨터를 검색 하 여 찾을 수 있습니다 *Microsoft Azure 백업*).

![백업 에이전트](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

Hello에서 **동작** hello hello 백업 에이전트가 있는 경우 콘솔의 오른쪽에 사용할 수 있는 수행할 수 있습니다 관리 작업을 수행 하는 hello:

* 서버 등록
* 백업 예약
* 지금 백업
* 속성 변경

![에이전트 콘솔 작업](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> 너무**데이터 복구**, 참조 [파일 tooa Windows server 또는 Windows 클라이언트 컴퓨터 복원](backup-azure-restore-windows-server.md)합니다.
>
>

### <a name="modify-an-existing-backup"></a>기존 백업 수정
1. Hello Microsoft Azure 백업 에이전트에서 클릭 **백업 예약**합니다.

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. Hello에 **백업 예약 마법사** hello 둡니다 **toobackup 항목 또는 시간 변경** 옵션을 선택 하 고 클릭 **다음**합니다.

    ![예약된 백업 수정](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. Tooadd 원하는 하거나 hello에 항목을 변경 하면 **항목 선택 tooBackup** 화면 클릭 **항목 추가**합니다.

    설정할 수도 있습니다 **제외 설정** hello 마법사의이 페이지에서. Tooexclude 파일 또는 파일 형식을 추가 하기 위한 hello 프로시저를 읽을 경우 [제외 설정](#exclusion-settings)합니다.
4. Hello 파일 및 폴더를 누르고 tooback를 원하는 선택 **알겠습니다**합니다.

    ![항목 추가](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. Hello 지정 **백업 일정** 클릭 **다음**합니다.

    매일(하루에 최대 3회) 또는 매주 백업을 예약할 수 있습니다.

    ![백업 일정 변경](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > Hello 백업 일정은이에 자세히 설명 되어 지정 [문서](backup-azure-backup-cloud-as-tape.md)합니다.
   >
   >
6. 선택 hello **보존 정책** hello 백업 복사본 및 클릭에 대 한 **다음**합니다.

    ![재방문 주기 정책 선택](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. Hello에 **확인** 화면 hello 정보를 검토 하 고 클릭 **마침**합니다.
8. Hello 마법사 hello 만들기가 완료 되 면 **백업 일정**, 클릭 **닫기**합니다.

    보호를 수정한 후 확인할 수 있습니다 toohello 이동 하 여 백업을 올바르게 트리거될 **작업** 백업 작업을 탭 하 고 hello에 변경 내용이 반영 되었는지 확인 합니다.

### <a name="enable-network-throttling"></a>네트워크 제한 사용
hello Azure 백업 에이전트 데이터 전송 시 네트워크 대역폭을 어떻게 사용 되는지 toocontrol 수 있는 조정 탭을 제공 합니다. 이 컨트롤 근무 시간 동안 데이터를 tooback 필요 하지만 다른 인터넷 트래픽과 hello 백업 프로세스 toointerfere 하지 않을 경우에 유용 합니다. 데이터의 제한 전송 tooback를 적용 하 고 활동을 복원 합니다.  

tooenable 제한:

1. Hello에 **백업 에이전트**, 클릭 **속성 변경**합니다.
2. 선택 hello **백업 작업에 대 한 인터넷 대역폭 제한을 사용 하도록 설정** 확인란을 선택 합니다.

    ![네트워크 제한](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. 제한을 사용 하도록 설정 하는 동안 백업 데이터 전송에 대 한 대역폭을 허용 하는 hello 지정 **근무 시간** 및 **휴무 시간**합니다.

    hello 대역폭 값 512kbps (초당) 크기는 512kb부터 시작 하 고 too1023 m b / 초 (Mbps)을 이동할 수 있습니다. Hello 시작을 지정 하 고 완료를 수도 있습니다 **근무 시간**, hello 요일을 어떤 작업 것으로 간주 됩니다 (일)입니다. 근무 시간을 지정 하는 hello 외부 hello 시간은 간주 toobe 비 작업 시간입니다.
4. **확인**을 클릭합니다.

## <a name="exclusion-settings"></a>제외 설정
1. 열기 hello **Microsoft Azure 백업 에이전트** (에 대 한 컴퓨터를 검색 하 여 찾을 수 있습니다 *Microsoft Azure 백업*).

    ![백업 에이전트 열기](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. Hello Microsoft Azure 백업 에이전트에서 클릭 **백업 예약**합니다.

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. 백업 예약 마법사 hello hello를 그대로 둡니다 **toobackup 항목 또는 시간 변경** 옵션을 선택 하 고 클릭 **다음**합니다.

    ![일정 수정](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. **제외 설정**을 클릭합니다.

    ![선택 항목 tooexclude](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. **제외 추가**를 클릭합니다.

    ![제외 추가](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. Hello 위치를 선택 하 고 클릭 **확인**합니다.

    ![제외할 위치 선택](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. Hello에 hello 파일 확장명 추가 **파일 형식을** 필드입니다.

    ![파일 형식별 제외](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    .mp3 확장명 추가

    ![파일 형식 예](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    tooadd 다른 확장 클릭 **제외 추가** 하 고 다른 파일 형식 확장명 (.jpeg 확장명을 추가 합니다.)을 입력 합니다.

    ![다른 파일 형식 예](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. 모든 hello 확장을 추가 했으므로 클릭 **확인**합니다.
9. 클릭 하 여 hello 백업 예약 마법사를 통해 계속 **다음** hello까지 **확인 페이지**, 클릭 **마침**합니다.

    ![제외 확인](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a>다음 단계
* [Azure에서 Windows Server 또는 Windows 클라이언트 복원](backup-azure-restore-windows-server.md)
* Azure 백업에 대해 자세히 toolearn 참조 [Azure 백업 개요](backup-introduction-to-azure-backup.md)
* Hello 방문 [Azure 백업 포럼](http://go.microsoft.com/fwlink/p/?LinkId=290933)
