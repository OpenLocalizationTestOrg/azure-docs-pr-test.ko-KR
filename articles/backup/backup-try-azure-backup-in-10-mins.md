---
title: "Windows 파일 및 폴더 tooAzure (리소스 관리자)를 aaaBack | Microsoft Docs"
description: "리소스 관리자 배포에서 Windows 파일 및 폴더 tooAzure tooback에 알아봅니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "어떻게 toobackup; 어떻게 tooback; 백업 파일 및 폴더"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 8/15/2017
ms.author: markgal;
ms.openlocfilehash: 07d6580a84d5092ed2c61bf86ff5fcb148423ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-back-up-files-and-folders-in-resource-manager-deployment"></a>먼저 보기: Resource Manager 배포에서 파일 및 폴더 백업
이 문서에서는 설명 어떻게 리소스 관리자 배포를 사용 하 여 Windows Server (또는 Windows 컴퓨터)을 tooback 파일 및 폴더 tooAzure 합니다. 자습서 의도 한 toowalk는 hello 기본 합니다. 원하는 tooget Azure 백업을 사용 하 여 시작 하는 경우 hello 올바른 위치에 있습니다.

Azure 백업에 대 한 자세한 tooknow 하려는 경우이 내용을 읽고 [개요](backup-introduction-to-azure-backup.md)합니다.

Azure 구독이 없는 경우 모든 Azure 서비스에 액세스할 수 있는 [무료 계정](https://azure.microsoft.com/free/) 을 만듭니다.

## <a name="create-a-recovery-services-vault"></a>복구 서비스 자격 증명 모음 만들기
파일 및 폴더를 tooback, toocreate hello 지역 toostore hello 데이터를 원하는 위치에 복구 서비스 자격 증명 모음 필요 합니다. Toodetermine 원하는 저장소를 복제 해야 합니다.

### <a name="toocreate-a-recovery-services-vault"></a>복구 서비스 자격 증명 모음 toocreate
1. 그렇게 이미 하지 않은 경우 toohello 로그인 [Azure 포털](https://portal.azure.com/) Azure 구독을 사용 하 여 합니다.
2. Hello 허브 메뉴에서 클릭 **더 많은 서비스** hello 리소스 목록에 입력 하 고 **복구 서비스** 클릭 **복구 서비스 자격 증명 모음**합니다.

    ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    Hello 구독에서 복구 서비스 자격 증명 모음 인 경우 hello 자격 증명 모음 나열 됩니다.
3. Hello에 **복구 서비스 자격 증명 모음** 메뉴를 클릭 하 여 **추가**합니다.

    ![복구 서비스 자격 증명 모음 만들기 2단계](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    hello 복구 서비스 자격 증명 모음에 블레이드에서 열립니다 tooprovide 묻는 **이름**, **구독**, **리소스 그룹**, 및 **위치**합니다.

    ![Recovery Services 자격 증명 모음 만들기 3단계](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. 에 대 한 **이름**, 이름 tooidentify hello 자격 증명 모음을 입력 합니다. hello 이름이 필요 toobe 고유 hello Azure 구독에 대 한 합니다. 이름을 2~50자 사이로 입력합니다. 문자로 시작해야 하며, 문자, 숫자, 하이픈만 사용할 수 있습니다.

5. Hello에 **구독** 섹션 hello 드롭 다운 메뉴 toochoose hello Azure 구독을 사용 합니다. 단일 구독을 사용 하는 경우 해당 구독 표시 되 고 toohello 다음 단계를 건너뛸 수 있습니다. 어떤 구독이 toouse 해야 할지 잘 모를 경우 hello 기본값을 사용 하 여 (또는 제안) 구독 합니다. 조직 계정이 여러 Azure 구독과 연결된 경우에만 여러 항목을 선택할 수 있습니다.

6. Hello에 **리소스 그룹** 섹션:

    * 선택 **새로 만들기** toocreate 새 리소스 그룹에 들어 있습니다.
    또는
    * 선택 **기존 항목 사용** hello 드롭 다운 메뉴 toosee hello 사용 가능한 리소스 그룹의 목록을 클릭 합니다.

  리소스 그룹에 대 한 자세한 내용은 참조 hello [Azure 리소스 관리자 개요](../azure-resource-manager/resource-group-overview.md)합니다.

7. 클릭 **위치** tooselect hello hello 자격 증명 모음에 대 한 지리적 영역입니다. 여기에서이 선택한 hello 지리적 지역에 백업 데이터를 보내는 위치를 결정 합니다.

8. Hello 복구 서비스 자격 증명 모음 블레이드의 hello 아래쪽 클릭 **만들기**합니다.

    복구 서비스 자격 증명 모음에 만든 toobe hello에 대 일 분 정도 걸릴 수 있습니다. Hello 포털의 상단 오른쪽 영역 hello에서에서 hello 상태 알림을 모니터링 합니다. 자격 증명 모음을 만든 후의 복구 서비스 자격 증명 모음 hello 목록에 나타납니다. 몇 분이 지나도 자격 증명 모음이 보이지 않으면 **새로 고침**을 클릭합니다.

    ![새로 고침 단추 클릭](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    자격 증명 모음 자격 증명 모음은 복구 서비스의 hello 목록에 표시 되는 경우 준비 tooset hello 저장소 중복 됩니다.

### <a name="set-storage-redundancy-for-hello-vault"></a>Hello 자격 증명 모음에 대 한 저장소 중복성을 설정 합니다.
복구 서비스 자격 증명 모음을 만들 때 저장소 중복 구성 된 hello 방식으로 원하는 인지 확인 합니다.

1. Hello에서 **복구 서비스 자격 증명 모음** 블레이드에서 hello 새 자격 증명 모음을 클릭 합니다.

    ![복구 서비스 자격 증명 모음의 hello 목록에서 hello 새 자격 증명 모음을 선택 합니다.](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    Hello 자격 증명 모음을 선택 하면 hello **복구 서비스 자격 증명 모음** 블레이드 좁힐 및 hello 설정 블레이드에서 (*hello hello 자격 증명 모음의 이름을 hello 위쪽에 있는*) 및 hello 자격 증명 모음 세부 정보 블레이드에서 엽니다.

    ![새 자격 증명 모음에 대 한 hello 저장소 구성 보기](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. Hello 새 자격 증명 모음의 설정 블레이드에서 toohello 관리 섹션 아래로 수직 슬라이드 tooscroll hello를 사용 하 여 마우스 클릭 **백업 인프라**합니다.
    hello 백업 인프라 블레이드를 엽니다.
3. Hello 백업 인프라 블레이드에서 클릭 **백업 구성** tooopen hello **백업 구성** 블레이드입니다.

    ![새 자격 증명 모음에 대 한 저장소 구성을 hello 설정](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. 자격 증명 모음에 대 한 hello 적절 한 저장소 복제 옵션을 선택 합니다.

    ![저장소 구성 선택 항목](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    기본적으로 사용자 자격 증명 모음에는 지역 중복 저장소가 있습니다. 기본 백업 저장소 끝점으로 Azure를 사용 하는 경우 계속 toouse **지리적 중복**합니다. 기본 백업 저장소 끝점으로 Azure를 사용 하지 않는 경우 선택할 **로컬 중복**, hello Azure 저장소 비용을 줄입니다. [지역 중복](../storage/common/storage-redundancy.md#geo-redundant-storage) 및 [로컬 중복](../storage/common/storage-redundancy.md#locally-redundant-storage) 저장소 옵션에 대한 자세한 내용은 [저장소 중복 개요](../storage/common/storage-redundancy.md)를 참조하세요.

이제 자격 증명 모음을 만들었으므로 파일과 폴더를 백업하도록 자격 증명 모음을 구성합니다.

## <a name="configure-hello-vault"></a>Hello 자격 증명 모음 구성
1. Hello 시작 섹션에 복구 서비스 자격 증명 모음 블레이드 (hello 모음 방금 만든)에 대 한 hello, 클릭 **백업**, 그 다음에 hello **백업 시작** 블레이드를  **백업 목표**합니다.

    ![백업 목표 블레이드 열기](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    hello **백업 목표** 블레이드를 엽니다.

    ![백업 목표 블레이드 열기](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. Hello에서 **여기서 작업이 실행 되는?** 드롭 다운 메뉴 **온-프레미스**합니다.

    Windows Server 또는 Windows 컴퓨터가 Azure에 있지 않은 실제 컴퓨터이므로 **온-프레미스**를 선택합니다.

3. Hello에서 **하 신 toobackup 원하는?** 메뉴 선택 **파일 및 폴더**, 클릭 하 고 **확인**합니다.

    ![파일 및 폴더 구성](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

    확인을 클릭 하면 확인 표시가 나타납니다 다음 너무**백업 목표**, 및 hello **준비 인프라** 블레이드를 엽니다.

    ![백업 목표 구성, 다음으로 인프라 준비](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. Hello에 **준비 인프라** 블레이드에서 클릭 **Windows Server 용 에이전트 다운로드 또는 Windows Client**합니다.

    ![Windows Server 또는 Windows 클라이언트의 에이전트 다운로드](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    Windows Server 필수 항목을 사용 하는, 용 Windows Server 필수 toodownload hello 에이전트를 선택 합니다. 팝업 메뉴 toorun 묻는 또는 MARSAgentInstaller.exe 저장 합니다.

    ![MARSAgentInstaller 대화 상자](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. Hello 다운로드 팝업 메뉴에서 클릭 **저장**합니다.

    기본적으로 hello **MARSagentinstaller.exe** 파일이 tooyour Downloads 폴더에 저장 됩니다. Hello 설치 관리자가 완료 되 면 toorun hello installer 또는 hello 폴더를 열 경우 묻는 팝업이 표시 됩니다.

    ![Windows Server 또는 Windows 클라이언트의 에이전트 다운로드](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    Tooinstall hello 에이전트를 아직 필요 하지 않습니다. Hello 자격 증명 모음 자격 증명을 다운로드 한 후 hello 에이전트를 설치할 수 있습니다.

6. Hello에 **준비 인프라** 블레이드에서 클릭 **다운로드**합니다.

    ![자격 증명 모음 자격 증명 다운로드](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    자격 증명 모음 hello tooyour 다운로드 폴더를 다운로드합니다. Hello 자격 증명 모음 자격 증명 다운로드를 완료 한 후 tooopen 원하는 또는 hello 자격 증명을 저장 하는 경우 요청 팝업이 표시 됩니다. **Save**를 클릭합니다. 실수로 누르면 **열려**, tooopen hello에 대 한 자격 증명 모음 자격 증명을 시도 하는 hello 대화 상자, 실패 합니다. Hello 자격 증명 모음을 열 수 없습니다. Toohello 다음 단계를 진행 합니다. hello 자격 증명 모음 자격 증명이 hello Downloads 폴더에 있습니다.   

    ![자격 증명 모음 자격 증명 다운로드 완료](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a>설치 하 고 hello 에이전트 등록

> [!NOTE]
> Hello Azure 포털을 통해 사용할 수 있도록 백업을 사용할 수 없는 경우, 아직 파일 및 폴더를 Microsoft Azure 복구 서비스 에이전트 tooback hello를 사용 합니다.
>

1. Hello를 두 번 클릭 **MARSagentinstaller.exe** hello 다운로드 폴더 (또는 다른 저장된 위치).

    hello 설치 관리자는 일련의 메시지를, 추출할 때는 설치 및 hello 복구 서비스 에이전트 등록을 제공 합니다.

    ![Recovery Services 에이전트 설치 관리자 자격 증명을 실행](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. Hello Microsoft Azure 복구 서비스 에이전트 설치 마법사를 완료 합니다. toocomplete hello 마법사 해야합니다.

   * Hello 설치 및 캐시 폴더의 위치를 선택 합니다.
   * 프록시 서버 tooconnect toohello를 사용 하는 경우 프록시 서버 정보를 제공 인터넷 합니다.
   * 인증된 프록시를 사용하는 경우에는 사용자 이름 및 암호 세부 정보를 입력합니다.
   * Hello 다운로드 한 자격 증명 모음 자격 증명을 제공 합니다.
   * Hello 암호화의 암호를 안전한 위치에 저장 합니다.

     > [!NOTE]
     > 끊어지거나 hello 암호를 잊은 경우 Microsoft hello 백업 데이터를 복구할 수 없습니다. Hello 파일을 안전한 위치에 저장 합니다. 것이 필수 toorestore 백업 합니다.
     >
     >

hello 에이전트를 지금 설치 하 고 등록 된 toohello 자격 증명 모음입니다. 준비 tooconfigure 하 고 백업을 예약 합니다.

## <a name="network-and-connectivity-requirements"></a>네트워크 및 연결 요구 사항

컴퓨터/프록시는 인터넷에 연결을 제한 한 경우 hello mcahine/프록시에 방화벽 설정이 다음 Url 구성된 tooallow hello 되는지 확인 합니다. <br>
    1. www.msftncsi.com
    2. *.Microsoft.com
    3. *.WindowsAzure.com
    4. *.microsoftonline.com
    5. *.windows.ne

## <a name="back-up-your-files-and-folders"></a>파일 및 폴더 백업
초기 백업을 hello 두 가지 주요 작업이 포함 됩니다.

* Hello 백업 예약
* 처음으로 파일 및 hello에 대 한 폴더를 백업

toocomplete hello 초기 백업을 사용 하 여 hello Microsoft Azure 복구 서비스 에이전트입니다.

### <a name="tooschedule-hello-backup-job"></a>tooschedule hello에 대 한 백업 작업
1. Hello Microsoft Azure 복구 서비스 에이전트를 엽니다. **Microsoft Azure 백업**에 대한 컴퓨터를 검색하여 찾을 수 있습니다.

    ![Hello Azure 복구 서비스 에이전트를 시작 합니다.](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)
2. Hello 복구 서비스 에이전트에서 클릭 **백업 예약**합니다.

    ![Windows Server 백업 예약](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)
3. Hello에 시작 hello 백업 예약 마법사의 페이지를 클릭 **다음**합니다.
4. Hello 항목 선택 tooBackup 페이지에서 클릭 **항목 추가**합니다.
5. Hello 파일 및 폴더, tooback 원하는 클릭 한 다음 선택 **알겠습니다**합니다.
6. **다음**을 누릅니다.
7. Hello에 **백업 일정 지정** 페이지에서 지정 하는 hello **백업 일정** 클릭 **다음**합니다.

    매일(하루에 최대 속도로 3회) 또는 매주 백업을 예약할 수 있습니다.

    ![Windows Server 백업 항목](./media/backup-try-azure-backup-in-10-mins/specify-backup-schedule-close.png)

   > [!NOTE]
   > Toospecify 백업 일정을 hello 하는 방법에 대 한 자세한 내용은 hello 문서 참조 [사용 하 여 Azure 백업 tooreplace 테이프 인프라](backup-azure-backup-cloud-as-tape.md)합니다.
   >

8. Hello에 **보존 정책 선택** 페이지, 선택 hello **보존 정책** hello 백업 복사본에 대 한 합니다.

    hello 보존 정책은 hello 백업 데이터 저장 기간을 지정 합니다. 모든 백업 지점에 대 한 "플랫 정책을"를 지정 하는 대신 hello 백업이 발생 하는 경우에 따라 서로 다른 보존 정책을 지정할 수 있습니다. 매일, 매주, 매월 및 매년 보존 정책을 toomeet hello 요구에 맞게 수정할 수 있습니다.
9. Hello 초기 백업 유형 선택 페이지에서 hello 초기 백업 유형을 선택 합니다. Hello 옵션인 **hello 네트워크를 통해 자동으로** 을 선택한 다음 클릭 **다음**합니다.

    Hello 네트워크를 통해 자동으로를 백업할 수 있습니다 또는 오프 라인으로 백업할 수 있습니다. 이 문서의 나머지 부분에서는 hello 자동으로 백업에 대 한 hello 프로세스를 설명 합니다. 오프 라인 백업을 toodo 원한다 면 hello 문서를 검토 [Azure 백업에서 오프 라인 백업 워크플로](backup-azure-backup-import-export.md) 추가 정보에 대 한 합니다.
10. Hello 확인 페이지에서 hello 정보를 검토 한 다음 클릭 **마침**합니다.
11. Hello 마법사 hello 백업 예약 만들기를 완료 한 후 클릭 **닫기**합니다.

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a>파일 및 처음으로 hello에 대 한 폴더를 tooback
1. Hello 복구 서비스 에이전트에서 클릭 **지금 백업** toocomplete hello 시드 hello 네트워크를 통해 초기 합니다.

    ![Windows Server 지금 백업](./media/backup-try-azure-backup-in-10-mins/backup-now.png)
2. Hello 확인 페이지에서 지금 백업 마법사 hello hello 설정 검토 tooback hello 컴퓨터를 사용 합니다. 그런 다음 **백업**을 클릭합니다.
3. 클릭 **닫기** tooclose hello 마법사. Hello 백업 프로세스를 완료 전에 hello 마법사를 닫으면 hello 마법사 toorun hello 백그라운드에서 계속 됩니다.

Hello 초기 백업을 완료 되 면 hello **작업을 완료 했지만** hello 백업 콘솔에 상태가 표시 됩니다.

![IR 완료](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="questions"></a>질문이 있으십니까?
기능의 경우 원하는 toosee 포함 또는 질문이 있는 경우 [피드백](http://aka.ms/azurebackup_feedback)합니다.

## <a name="next-steps"></a>다음 단계
* [Windows 컴퓨터 백업](backup-configure-vault.md)에 대해 자세히 알아보세요.
* 파일과 폴더를 백업했으므로 이제 [자격 증명 모음 및 서버](backup-azure-manage-windows-server.md)를 관리할 수 있습니다.
* Toorestore 백업 해야 할 경우 사용 하 여이 문서 너무[tooa Windows 컴퓨터 파일을 복원](backup-azure-restore-windows-server.md)합니다.
