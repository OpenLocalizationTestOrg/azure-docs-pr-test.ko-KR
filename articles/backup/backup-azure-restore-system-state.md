---
title: "Azure 백업: 시스템 상태 복원 tooa Windows Server | Microsoft Docs"
description: "Azure의 백업에서 Windows Server 시스템 상태를 복원하기 위한 단계별 설명입니다."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/18/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: a45506507f53e2744350d3b6b2e52f1db415de4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-system-state-toowindows-server"></a>시스템 상태 복원 tooWindows 서버

이 문서에서는 toorestore Windows 서버 시스템 상태 백업에서 Azure 복구 서비스 자격 증명 모음에 대해 설명 합니다. 시스템 상태 toorestore 시스템 상태 백업 필요 합니다 (의 hello 지침을 사용 하 여 만든 [시스템 상태 백업](backup-azure-system-state.md#back-up-windows-server-system-state-preview)), hello를 설치 했는지 확인 하 고 [최신 버전의 Microsoft Azure Recovery hello (MARS) 서비스 에이전트](http://aka.ms/azurebackup_agent)합니다. Azure Recovery Services 자격 증명 모음에서 Windows Server 시스템 상태 데이터를 복구하는 작업은 두 단계로 이루어집니다.

1. Azure Backup에서 파일로 시스템 상태 복원 Azure Backup에서 파일로 시스템 상태를 복원할 경우 다음을 수행할 수 있습니다.
  * 시스템 상태 복원 toohello hello 백업이 수행 된 동일한 서버 또는
  * 시스템 상태 복원 파일 tooan 대체 서버입니다.

2. 복원 하는 hello 시스템 상태 파일 tooa Windows Server를 적용 합니다.


## <a name="recover-system-state-files-toohello-same-server"></a>시스템 상태 복구 toohello 파일 같은 서버
단계를 수행 하는 hello tooroll Windows 서버 구성 tooa 이전 상태를 백업 하는 방법을 설명 합니다. 롤링 서버 백 tooa 알려진, 안정적인 상태를 구성 하는 것은 매우 효과적일 수 있습니다. hello 단계 복원 hello 서버 시스템 상태 복구 서비스 자격 증명 모음에서 수행 합니다. 

1. 열기 hello **Microsoft Azure 백업** 스냅인. 여기서 hello 스냅인 기능이 설치 된 모르는 경우 hello 컴퓨터 또는 서버에 대 한 검색 **Microsoft Azure 백업**합니다.

    hello를 데스크톱 응용 프로그램 hello 검색 결과에 표시 됩니다.

2. 클릭 **데이터 복구** toostart hello 마법사.

    ![데이터 복구](./media/backup-azure-restore-windows-server/recover.png)

3. Hello에 **시작** 창, toorestore hello 데이터 toohello 동일한 서버 또는 컴퓨터 선택 **이 서버 (`<server name>`)** 클릭 **다음**합니다.

    ![이 서버 옵션 toorestore hello 데이터 toohello 선택 동일한 컴퓨터](./media/backup-azure-restore-system-state/samemachine.png)

4. Hello에 **복구 모드 선택** 창 선택 **시스템 상태** 클릭 하 고 **다음**합니다.

    ![파일 찾아보기](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. Hello 일정에 **볼륨 및 날짜 선택** 지점 창에서 복구를 선택 합니다. 

    어떤 복구 시점에서라도 복원할 수 있습니다. 날짜 **굵게** 복구 지점이 하나 이상 hello 가용성을 나타냅니다. 여러 복구 지점을 사용할 수 있는 경우 날짜를 선택 하면 hello에서 hello 특정 복구 지점 선택 **시간** 드롭 다운 메뉴.

    ![볼륨 및 날짜](./media/backup-azure-restore-system-state/select-date.png)

6. 복구 지점 toorestore hello를 선택 하면 클릭 **다음**합니다.

    Azure 백업 탑재 hello 로컬 복구 지점으로 사용 하 여 복구 볼륨입니다.

7. Hello 다음 창에서 복구 된 시스템 상태 파일 hello에 대 한 hello 대상 지정 하 고 클릭 **찾아보기** 원하는 tooopen Windows 탐색기 및 찾기 hello 파일 및 폴더. 옵션을 hello **복사본 두 버전 모두 유지을 만들어**, hello 전체 시스템 상태 보관의 hello 복사본을 만드는 대신 기존의 시스템 상태 파일 보관 파일에서 개별 파일의 복사본을 만듭니다.

    ![복구 옵션](./media/backup-azure-restore-system-state/recover-as-files.png)

8. 복구 hello에 대 한 hello 세부 정보 확인 **확인** 창을 **복구**합니다.

   ![복구 tooacknowledge hello 복구 작업을 클릭 합니다.](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. 복사 hello *WindowsImageBackup* hello 복구 대상 tooa hello 서버에 중요 한 볼륨의에서 디렉터리입니다. 일반적으로 Windows 운영 체제 볼륨 hello hello 중요 한 볼륨입니다.

10. Hello 복구 되 면 되 면에서 다음과 같이 hello hello 섹션 [적용 Windows 서버 시스템 상태 파일 toohello 복원](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), toocomplete hello 시스템 상태 복구 프로세스입니다.

## <a name="recover-system-state-files-tooan-alternate-server"></a>시스템 상태 복구 파일 tooan 대체 서버

Windows Server 손상 되었거나 액세스할 수 없고 고 toorestore 원하는 것 tooa 안정적인 상태를 복구 하 여 hello Windows 서버 시스템 상태, 다른 서버에서 hello 손상 된 서버 시스템 상태를 복원할 수 있습니다. Hello 단계 toohello 복원 시스템 상태는 별도 서버에서 다음을 사용 합니다.  

다음이 단계에 사용 된 hello 용어에는 다음이 포함 됩니다.

- *원본 컴퓨터* – hello 원래 컴퓨터 hello 백업에서 백업 하 고 있는 현재 사용할 수 없는 합니다.
- *대상 컴퓨터* – hello 컴퓨터 toowhich hello 데이터 복구 되 고 있습니다.
- *샘플 자격 증명 모음* – hello 복구 서비스 자격 증명 모음 toowhich hello *원본 컴퓨터* 및 *대상 컴퓨터* 등록 됩니다. <br/>

> [!NOTE]
> 한 컴퓨터에서 만든 백업을 이전 버전의 hello 운영 체제를 실행 하는 복원 된 tooa 컴퓨터 일 수 없습니다. 예를 들어 컴퓨터 수 없는 Windows Server 2016에서 수행 된 백업을 복원 tooWindows Server 2012 r 2. 그러나 hello 역 수는 없습니다. Windows Server 2012 R2 toorestore Windows Server 2016에서에서 백업을 사용할 수 있습니다.
>

1. 열기 hello **Microsoft Azure 백업** hello에서 스냅인 *대상 컴퓨터*합니다.
2. 해당 hello 확인 *대상 컴퓨터* 및 hello *원본 컴퓨터* 동일한 복구 서비스 자격 증명 모음에 등록 된 toohello 됩니다.
3. 클릭 **데이터 복구** tooinitiate hello 워크플로 합니다.

    ![데이터 복구](./media/backup-azure-restore-windows-server-classic/recover.png)

4. **다른 서버**

    ![다른 서버](./media/backup-azure-restore-system-state/anotherserver.png)

5. Hello toohello 해당 하는 자격 증명 모음 자격 증명 파일을 제공 *샘플 자격 증명 모음*합니다. Hello 자격 증명 모음 자격 증명 파일을 잘못 된 (또는 만료 된) 경우 hello에서 새 자격 증명 모음 자격 증명 파일을 다운로드 *샘플 자격 증명 모음* hello Azure 포털의에서. Hello 자격 증명 모음 자격 증명 파일 제공 되 면 hello 자격 증명 모음 자격 증명 파일과 관련 된 hello 복구 서비스 자격 증명 모음에 나타납니다.

6. Hello 백업 서버 선택 창에서를 선택 hello *원본 컴퓨터* hello 목록이 표시 된 컴퓨터에서 합니다.

    ![컴퓨터 목록](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. Hello 복구 모드 선택 창에서 선택 **시스템 상태** 클릭 **다음**합니다. 

    ![검색](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. Hello에 달력 hello에 **볼륨 및 날짜 선택** 지점 창에서 복구를 선택 합니다. 어떤 복구 시점에서라도 복원할 수 있습니다. 날짜 **굵게** 복구 지점이 하나 이상 hello 가용성을 나타냅니다. 여러 복구 지점을 사용할 수 있는 경우 날짜를 선택 하면 hello에서 hello 특정 복구 지점 선택 **시간** 드롭 다운 메뉴. 

    ![검색 항목](./media/backup-azure-restore-system-state/select-date.png)

9. 복구 지점 toorestore hello를 선택 하면 클릭 **다음**합니다.

10. Hello에 **시스템 상태 복구 모드 선택** 창의 hello 대상을 시스템 상태 복구 toobe 파일을 지정 하 고 클릭 **다음**합니다.

    ![암호화](./media/backup-azure-restore-system-state/recover-as-files.png)

    옵션을 hello **복사본 두 버전 모두 유지을 만들어**, hello 전체 시스템 상태 보관의 hello 복사본을 만드는 대신 기존의 시스템 상태 파일 보관 파일에서 개별 파일의 복사본을 만듭니다.

11. Hello 확인 창에서 복구의 hello 세부 정보를 확인 하 고 클릭 **복구**합니다. 

    ![hello 복구 단추 tooconfirm hello 복구 프로세스를 클릭 합니다.](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. 복사 hello *WindowsImageBackup* hello 서버의 디렉터리 tooa 단순한 볼륨 (예: d:\)합니다. 일반적으로 Windows 운영 체제 볼륨 hello hello 중요 한 볼륨입니다.

13. toocomplete hello 복구 프로세스를 사용 하 여 hello 다음 섹션을 너무[Windows 서버에서 시스템 상태 파일을 복원 하는 hello 적용](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server)합니다.




## <a name="apply-restored-system-state-on-a-windows-server"></a>Windows Server에서 복원된 시스템 상태 적용

Azure 복구 서비스 에이전트를 사용 하 여 파일로 시스템 상태를 복구한 후 사용 하 여 hello Windows Server 백업 유틸리티 tooapply hello 시스템 상태 tooWindows 서버를 복구 합니다. Windows Server 백업 유틸리티 hello hello 서버에 이미 있는 합니다. 단계를 수행 하는 hello tooapply hello 시스템 상태를 복구 하는 방법을 설명 합니다.

1. 사용 하 여 hello 다음 명령을 tooreboot의 서버에 *디렉터리 서비스 복구 모드*합니다. 관리자 권한 명령 프롬프트에서 다음을 수행합니다.

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. Hello 다시 부팅 후 hello Windows Server 백업 스냅인을 엽니다. 여기서 hello 스냅인 기능이 설치 된 모르는 경우 hello 컴퓨터 또는 서버에 대 한 검색 **Windows Server 백업**합니다.

    hello를 데스크톱 응용 프로그램 hello 검색 결과에 표시 됩니다.

3. 스냅인 hello에서 선택 **로컬 백업**합니다.

    ![여기에서 로컬 백업 toorestore 선택](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. Hello 로컬 백업 콘솔을 열고 hello에 **작업 창**, 클릭 **복구** tooopen hello 복구 마법사.

5. Hello 옵션을 선택 **다른 위치에 저장 된 백업을**를 클릭 하 고 **다음**합니다.

   ![toorecover tooa 다른 서버를 선택 합니다.](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. 위치 유형에 hello를 지정할 때는 선택 **원격 공유 폴더** 시스템 상태 백업을 복구 된 tooanother 서버인 경우. 시스템 상태가 로컬로 복구된 경우 **로컬 드라이브**를 선택합니다. 

    ![선택 여부 또는 로컬 서버에서 toorecovery](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. Hello 경로 toohello 입력 *WindowsImageBackup* 디렉터리 hello Azure Recovery를 사용 하 여 hello 시스템 상태 파일 복구의 일부로 복구이 디렉터리 (예를 들어 D:\WindowsImageBackup)를 포함 하는 로컬 드라이브를 선택 하거나 서비스 에이전트 및 클릭 **다음**합니다.

    ![경로 toohello 공유 파일](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. 클릭 하 고 toorestore를 지정 하는 선택 hello 시스템 상태 버전 **다음**합니다.

9. Hello 복구 유형 선택 창에서 선택 **시스템 상태** 클릭 **다음**합니다.

10. 시스템 상태 복구 hello hello 위치, 선택 **원래 위치**를 클릭 하 고 **다음**합니다.

11. hello 확인 세부 정보를 검토 하 고, hello 다시 부팅 설정을 확인 하 고, 클릭 **복구** tooapplly hello 시스템 상태 파일을 복원 합니다.

    ![시스템 상태 파일을 복원 하는 시작 hello](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a>Active Directory 서버에서 시스템 상태 복구에 대한 특별 고려 사항

시스템 상태 백업은 Active Directory 데이터를 포함합니다. 현재 상태 tooa 이전 상태에서 단계 toorestore Active Directory 도메인 서비스 (AD DS)를 수행 하는 hello를 사용 합니다.

1. 에 디렉터리 서비스 복원 모드 (DSRM) hello 도메인 컨트롤러를 다시 시작 합니다.
2. Hello 단계에 따라 [여기](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toouse Windows Server 백업 cmdlet toorecover AD DS 합니다.


## <a name="troubleshoot-failed-system-state-restore"></a>실패한 시스템 상태 복원 문제 해결

시스템 상태를 적용 한 hello 이전 프로세스가 성공적으로 완료 되지 않으면 hello Windows 복구 환경 (Win RE) toorecover Windows Server를 사용 합니다. hello 다음 단계에서는 설명 방법을 toorecover Win 다시 사용 합니다. 시스템 상태 복원 후에 Windows Server가 정상적으로 부팅되지 않는 경우에만 이 옵션을 사용합니다. 다음 프로세스를 수행 하는 hello 비 시스템 데이터를 사용 하 여 주의 지웁니다. 

1. Windows 복구 환경 (Win RE) hello로 Windows Server를 부팅 합니다.

2. 문제 해결을 hello 3 개 사용할 수 있는 옵션 중에서 선택 합니다.

    ![메뉴 열기](./media/backup-azure-restore-system-state/winre-1.png)

3. Hello에서 **고급 옵션** 화면에서 **명령 프롬프트** hello 서버 관리자 사용자 이름 및 암호를 제공 합니다.

   ![메뉴 열기](./media/backup-azure-restore-system-state/winre-2.png)

4. Hello 서버 관리자 사용자 이름 및 암호를 제공 합니다.

    ![메뉴 열기](./media/backup-azure-restore-system-state/winre-3.png)

5. 관리자 모드에서 hello 명령 프롬프트를 여는 경우 다음 명령 tooget hello 시스템 상태 백업 버전을 실행 합니다.

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![시스템 상태 백업 버전 가져오기](./media/backup-azure-restore-system-state/winre-4.png)

6. 다음 명령은 tooget hello hello 백업에 사용할 수 있는 모든 볼륨을 실행 합니다.

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![시스템 상태 백업 버전 가져오기](./media/backup-azure-restore-system-state/winre-5.png)

7. hello 다음 명령을 복구 hello 시스템 상태 백업이 포함 된 모든 볼륨. 이 단계 hello 중요 한 볼륨만 부분이 hello 시스템 상태 복구 되는지 note 합니다. 모든 비 시스템 데이터가 지워집니다.

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![시스템 상태 백업 버전 가져오기](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a>다음 단계
* 파일과 폴더를 복구했으므로 [백업을 관리](backup-azure-manage-windows-server.md)할 수 있습니다.
