---
title: "Windows 시스템 상태 tooAzure aaaBack | Microsoft Docs"
description: "Windows Server 및/또는 Windows 컴퓨터 tooAzure hello 시스템 상태를 tooback에 알아봅니다."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: carmonm
editor: 
keywords: "어떻게 toobackup; 어떻게 tooback; 백업 파일 및 폴더"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: saurse;markgal
ms.openlocfilehash: be5d4be81af981c10de82add9fe962a730753cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a>Resource Manager 배포에서 Windows 시스템 상태 백업
이 문서에서는 Windows 서버 시스템을 tooback tooAzure를 명시 하는 방법을 설명 합니다. 자습서 의도 한 toowalk는 hello 기본 합니다.

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

    * 선택 **새로 만들기** toocreate 리소스 그룹에 들어 있습니다.
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

이제 자격 증명 모음을 만들었으므로 Windows 시스템 상태를 백업하도록 구성합니다.

## <a name="configure-hello-vault"></a>Hello 자격 증명 모음 구성
1. Hello 시작 섹션에 복구 서비스 자격 증명 모음 블레이드 (hello 모음 방금 만든)에 대 한 hello, 클릭 **백업**, 그 다음에 hello **백업 시작** 블레이드를  **백업 목표**합니다.

    ![백업 목표 블레이드 열기](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    hello **백업 목표** 블레이드를 엽니다.

    ![백업 목표 블레이드 열기](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. Hello에서 **여기서 작업이 실행 되는?** 드롭 다운 메뉴 **온-프레미스**합니다.

    Windows Server 또는 Windows 컴퓨터가 Azure에 있지 않은 실제 컴퓨터이므로 **온-프레미스**를 선택합니다.

3. Hello에서 **하 신 toobackup 원하는?** 메뉴 선택 **시스템 상태**, 클릭 하 고 **확인**합니다.

    ![파일 및 폴더 구성](./media/backup-azure-system-state/backup-goal-system-state.png)

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
> Hello Azure 포털을 통해 사용할 수 있도록 백업을 사용할 수 없는 경우, 아직 Windows 서버 시스템 상태를 Microsoft Azure 복구 서비스 에이전트 tooback hello를 사용 합니다.
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

## <a name="back-up-windows-server-system-state-preview"></a>Windows Server 시스템 상태 백업(미리 보기)
hello 초기 백업에는 세 가지 작업이 포함 됩니다.

* Hello Azure 백업 에이전트를 사용 하 여 시스템 상태 백업을 사용 하도록 설정
* Hello 백업 예약
* 처음으로 파일 및 hello에 대 한 폴더를 백업

toocomplete hello 초기 백업을 사용 하 여 hello Microsoft Azure 복구 서비스 에이전트입니다.

### <a name="tooenable-system-state-backup-using-hello-azure-backup-agent"></a>hello Azure 백업 에이전트를 사용 하 여 tooenable 시스템 상태 백업

1. PowerShell 세션에서 다음 명령 toostop hello Azure 백업 엔진 hello를 실행 합니다.

  ```
  PS C:\> Net stop obengine
  ```

2. Hello Windows 레지스트리를 엽니다.

  ```
  PS C:\> regedit.exe
  ```

3. DWord 값을 지정 하는 hello 다음 hello로 레지스트리 키를 추가 합니다.

  | 레지스트리 경로 | 레지스트리 키 | DWord 값 |
  |---------------|--------------|-------------|
  | HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider | TurnOffSSBFeature | 2 |

4. Hello 다음 관리자 권한 명령 프롬프트에서 명령을 실행 하 여 hello 백업 엔진을 다시 시작 합니다.

  ```
  PS C:\> Net start obengine
  ```

### <a name="tooschedule-hello-backup-job"></a>tooschedule hello에 대 한 백업 작업

1. Hello Microsoft Azure 복구 서비스 에이전트를 엽니다. **Microsoft Azure 백업**에 대한 컴퓨터를 검색하여 찾을 수 있습니다.

    ![Hello Azure 복구 서비스 에이전트를 시작 합니다.](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. Hello 복구 서비스 에이전트에서 클릭 **백업 예약**합니다.

    ![Windows Server 백업 예약](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. Hello에 시작 hello 백업 예약 마법사의 페이지를 클릭 **다음**합니다.

4. Hello 항목 선택 tooBackup 페이지에서 클릭 **항목 추가**합니다.

5. **시스템 상태**를 선택하고 **확인**을 클릭합니다.

6. **다음**을 누릅니다.

7. hello 시스템 상태 백업 및 보존 일정 자동으로 설정 되어 tooback 매주 일요일을 현지 시간으로 오후 9시에 hello 보존 기간을 설정 및 too60 일 수 있습니다.

   > [!NOTE]
   > 시스템 상태 백업 및 보존 정책이 자동으로 구성됩니다. 파일 및 폴더 또한 toohello Windows 서버 시스템 상태를 백업할 경우 hello 마법사에서 파일 백업에 대 한 유일한 hello 백업 및 보존 정책을 지정 합니다. 
   >

8. Hello 확인 페이지에서 hello 정보를 검토 한 다음 클릭 **마침**합니다.

9. Hello 마법사 hello 백업 예약 만들기를 완료 한 후 클릭 **닫기**합니다.

### <a name="tooback-up-windows-server-system-state-for-hello-first-time"></a>처음으로 hello에 대 한 Windows 서버 시스템 상태를 tooback

1. 다시 부팅해야 하는 Windows Server에 보류 중인 업데이트가 없어야 합니다.

2. Hello 복구 서비스 에이전트에서 클릭 **지금 백업** toocomplete hello 시드 hello 네트워크를 통해 초기 합니다.

    ![Windows Server 지금 백업](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. Hello 확인 페이지에서 지금 백업 마법사 hello hello 설정 검토 tooback hello 컴퓨터를 사용 합니다. 그런 다음 **백업**을 클릭합니다.

4. 클릭 **닫기** tooclose hello 마법사. Hello 백업 프로세스를 완료 전에 hello 마법사를 닫으면 hello 마법사 toorun hello 백그라운드에서 계속 됩니다.

5. 백업할 파일 및 폴더를 서버의 또한 toohello Windows 서버 시스템 상태, hello 지금 백업 마법사는 백업 파일입니다. tooperform 없는 임시 시스템 상태를 백업, 다음 PowerShell 명령을 사용 하 여 hello:

    ```
    PS C:\> Start-OBSystemStateBackup
    ```

  Hello 초기 백업을 완료 되 면 hello **작업을 완료 했지만** hello 백업 콘솔에 상태가 표시 됩니다.

  ![IR 완료](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="frequently-asked-questions"></a>질문과 대답

hello 다음 질문과 대답을 제공 보충 정보입니다.

### <a name="what-is-hello-staging-volume"></a>Hello 준비 볼륨 란?

hello 준비 볼륨 hello 중간 위치가 hello 고유 하 게 사용할 수 있는 Windows Server 백업 hello 시스템 상태 백업을 준비 하는 위치를 나타냅니다. Azure 백업 에이전트 다음 압축 및이 중간 백업을 암호화 하 고 복구 서비스 자격 증명 모음 구성 보안 HTTPS 프로토콜 toohello 통해 보냅니다. **비-Windows-OS 볼륨에서 hello 준비 볼륨을 설정 하는 것이 좋습니다. 시스템 상태 백업에 문제가 발견 될 경우 hello 첫 번째 문제 해결 단계는 준비 볼륨의 hello 위치를 확인 하는 중입니다.** 

### <a name="how-can-i-change-hello-staging-volume-path-specified-in-hello-azure-backup-agent"></a>Hello hello Azure 백업 에이전트에서 지정 된 준비 볼륨 경로 변경 하려면 어떻게 해야 합니까?

기본적으로 hello 준비 볼륨 hello 캐시 폴더에 있습니다. 

1. toochange이이 위치를 사용 하 여 hello 다음 명령을 관리자 권한 명령 프롬프트) (에:
  ```
  PS C:\> Net stop obengine
  ```

2. Hello 다음 hello 경로 toohello 새 볼륨 준비 폴더와 레지스트리 항목을 업데이트 합니다.

  |레지스트리 경로|레지스트리 키|값|
  |-------------|------------|-----|
  |HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider | SSBStagingPath | 새 스테이징 볼륨 위치 |

hello 준비 경로 대/소문자 구분 및 hello 정확히 동일한 대/소문자 hello 서버에 존재 하는 기능으로 이어야 합니다. 

3. Hello 준비 볼륨 경로 변경한 후에 hello 백업 엔진 다시 시작 합니다.
  ```
  PS C:\> Net start obengine
  ```
4. hello 변경 된 경로, 열기 hello Microsoft Azure 복구 서비스 에이전트 및 시스템 상태의 임시 백업 트리거를 toopick 합니다.

### <a name="why-is-hello-system-state-default-retention-set-too60-days"></a>기본 보존 설정 too60 일 hello 시스템 상태 이유는 무엇입니까?

시스템 상태 백업의 연수 hello hello Windows Server Active Directory 역할에 대 한 "삭제 표시 수명" hello 설정으로 동일한 hello 됩니다. hello hello 삭제 표시 수명 항목에 대 한 기본값은 60 일입니다. Hello 디렉터리 서비스 (NTDS) 구성 개체에서이 값을 설정할 수 있습니다.

### <a name="how-do-i-change-hello-default-backup-and-retention-policy-for-system-state"></a>Hello 기본 백업 및 시스템 상태에 대 한 보존 정책을 변경 하려면 어떻게 해야 합니까?

toochange hello 기본 백업 및 보존 정책에 대 한 시스템 상태:
1. Hello 백업 엔진을 중지 합니다. Hello 상승된 된 명령 프롬프트에서 다음 명령을 실행 합니다.

  ```
  PS C:\> Net stop obengine
  ```

2. 추가 하거나 hello 다음 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider에서 레지스트리 키 항목을 업데이트 합니다.

  |레지스트리 이름|설명|값|
  |-------------|-----------|-----|
  |SSBScheduleTime|Tooconfigure hello 백업 시간을 hello 사용 합니다. 기본값은 현지 시간으로 오후 9시입니다.|DWord: HHMM 형식(10진수)으로 예를 들어 2130은 현지 시간으로 오후 9시 30분입니다.|
  |SSBScheduleDays|시스템 상태 백업의 hello에 수행 해야 하는 경우 사용 되는 tooconfigure hello 일 시간을 지정 합니다. 개별 숫자 hello 주의 일을 지정합니다. 0은 일요일, 1은 월요일 등입니다. 백업의 기본 요일은 일요일입니다.|Hello 주 toorun 백업 (10 진수) 예를 들어 월요일, 화요일, 수요일 및 일요일에 백업 일정을 1230 DWord: 요일입니다.|
  |SSBRetentionDays|사용 되는 tooconfigure hello 일 tooretain 백업입니다. 기본값은 60입니다. 허용되는 최대값은 180입니다.|DWord: 일 tooretain 백업 (10 진수)입니다.|

3. 다음 명령 toorestart hello 백업 엔진 hello를 사용 합니다.
    ```
    PS C:\> Net start obengine
    ```

4. Hello Microsoft 복구 서비스 에이전트를 엽니다.

5. 클릭 **백업 예약** 클릭 하 고 **다음** 반영 된 hello 변경 될 때까지 합니다.

6. 클릭 **마침** tooapply hello 변경 합니다.


## <a name="questions"></a>질문이 있으십니까?
기능의 경우 원하는 toosee 포함 또는 질문이 있는 경우 [피드백](http://aka.ms/azurebackup_feedback)합니다.

## <a name="next-steps"></a>다음 단계
* [Windows 컴퓨터 백업](backup-configure-vault.md)에 대해 자세히 알아보세요.
* 파일과 폴더를 백업했으므로 이제 [자격 증명 모음 및 서버](backup-azure-manage-windows-server.md)를 관리할 수 있습니다.
* Toorestore 백업 해야 할 경우 사용 하 여이 문서 너무[tooa Windows 컴퓨터 파일을 복원](backup-azure-restore-windows-server.md)합니다.
