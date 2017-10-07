---
title: "Windows 서버 또는 워크스테이션 tooAzure (클래식 모델)을 aaaBack | Microsoft Docs"
description: "Windows 서버 또는 클라이언트 tooa 백업 자격 증명 모음 Azure에 백업 합니다. Hello Azure 백업 에이전트를 사용 하 여 백업 자격 증명 모음 tooa 파일 및 폴더를 보호 하기 위한 기본 이동 합니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "백업 자격 증명 모음, Windows 서버 백업, Windows 백업"
ms.assetid: 3b543bfd-8978-4f11-816a-0498fe14a8ba
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: c8f2a9bed1e5885f5c272c65b9282ededc05850a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-workstation-tooazure-using-hello-classic-portal"></a>Hello 클래식 포털을 사용 하 여 Windows 서버 또는 워크스테이션 tooAzure 백업
> [!div class="op_single_selector"]
> * [클래식 포털](backup-configure-vault-classic.md)
> * [Azure 포털](backup-configure-vault.md)
>
>

이 문서는 사용자 환경 toofollow tooprepare 필요 하 고 Windows 서버 (또는 워크스테이션) tooAzure 백업 hello 절차를 다룹니다. 또한 백업 솔루션 배포 시 고려 사항에 대해서도 설명합니다. 처음으로 hello에 대 한 Azure 백업 시도에 관심이 있다면이 여기서 신속 하 게 과정을 보여 줍니다 hello 합니다.

Azure는 리소스를 만들고 작업하기 위한 두 가지 배포 모델로 리소스 관리자와 클래식을 제공합니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.

## <a name="before-you-start"></a>시작하기 전에
서버 또는 클라이언트 tooAzure tooback, Azure 계정이 필요 합니다. 계정이 없는 경우 몇 분 만에 [무료 계정](https://azure.microsoft.com/free/) 을 만들 수 있습니다.

## <a name="create-a-backup-vault"></a>백업 자격 증명 모음 만들기
서버 또는 클라이언트에서 파일 및 폴더를 tooback, toocreate toostore hello 데이터 hello 지리적 지역에 백업 자격 증명 필요 합니다.

> [!IMPORTANT]
> 2017 년 3 월 부터는 hello 클래식 포털 toocreate 백업 자격 증명 모음은 더 이상 사용할 수 없습니다.
>
> 이제 사용자 백업 자격 증명 모음 tooRecovery 서비스 자격 증명 모음을 업그레이드할 수 있습니다. 자세한 내용은 hello 문서 참조 [복구 서비스 자격 증명 모음에 백업 자격 증명 모음 tooa 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md)합니다. Microsoft는 것이 권장 tooupgrade 백업 tooRecovery 서비스 자격 증명 모음 자격 증명 모음입니다.<br/> **2017 년 10 월 15**, 수 toouse PowerShell toocreate 백업 자격 증명 모음은 더 이상 됩니다. <br/> **2017년 11월 1일 시작**:
>- 나머지 모든 백업 자격 증명 모음을 자동으로 업그레이드 된 tooRecovery 서비스 자격 증명 모음 됩니다.
>- 하면 hello 클래식 포털에서 수 tooaccess 백업 데이터 수 없습니다. 대신, 복구 서비스 자격 증명 모음에 hello Azure 포털 tooaccess 백업 데이터를 사용 합니다.
>


## <a name="download-hello-vault-credential-file"></a>Hello 자격 증명 모음 자격 증명 파일을 다운로드
hello 온-프레미스 컴퓨터 toobe tooAzure 데이터를 백업할 수 전에 백업 자격 증명 인증에 필요 합니다. hello 인증 누군가가 *자격 증명을 자격 증명 모음*합니다. hello 클래식 포털에서 보안 채널을 통해 hello 자격 증명 모음 자격 증명 파일이 다운로드 됩니다. hello 인증서 개인 키 hello 포털 또는 hello 서비스에 유지 되지 않습니다.

### <a name="toodownload-hello-vault-credential-file-tooa-local-machine"></a>toodownload hello 자격 증명 모음 자격 증명 파일 tooa 로컬 컴퓨터
1. Hello 왼쪽된 탐색 창에서 클릭 **복구 서비스**, 한 다음 만든 된 자격 증명 hello 백업 모음을 선택 합니다.

    ![IR 완료](./media/backup-configure-vault-classic/rs-left-nav.png)
2. Hello 빠른 시작 페이지에서 클릭 **자격 증명 모음 다운로드**합니다.

   hello 클래식 포털에서는 hello 및 hello 자격 증명 모음 이름과 현재 날짜를 조합 하 여 자격 증명 모음 자격 증명을 생성 합니다. hello 자격 증명 모음 자격 증명 파일 hello 등록 워크플로 중에 사용 되며 48 시간 후 만료 됩니다.

   hello 포털에서 hello 자격 증명 모음 자격 증명 파일을 다운로드할 수 있습니다.
3. 클릭 **저장** toodownload hello 자격 증명 모음 자격 증명 파일 toohello 다운로드 폴더의 hello 로컬 계정. 선택할 수도 있습니다 **다른 이름으로 저장** hello에서 **저장** 메뉴 toospecify hello 자격 증명 모음 자격 증명 파일의 위치입니다.

   > [!NOTE]
   > Hello 자격 증명 모음 자격 증명 파일은 컴퓨터에서 액세스할 수 있는 위치에 저장 하 고 있는지 확인 합니다. 파일 공유 또는 서버 메시지 블록에 저장 되는지를 hello 권한을 tooaccess 있는지 확인 하기.
   >
   >

## <a name="download-install-and-register-hello-backup-agent"></a>다운로드, 설치 및 hello 백업 에이전트를 등록 합니다.
Hello 백업 자격 증명 모음 및 다운로드 hello 자격 증명 모음 자격 증명 파일을 만든 후 각각의 Windows 컴퓨터에서 에이전트를 설치 합니다.

### <a name="toodownload-install-and-register-hello-agent"></a>toodownload, 설치 및 hello 에이전트 등록
1. 클릭 **복구 서비스**, 한 다음 원하는 서버와 tooregister hello 백업 자격 증명을 선택 합니다.
2. Hello 빠른 시작 페이지에서 클릭 hello 에이전트 **에이전트에 대 한 Windows Server 또는 System Center Data Protection Manager 또는 Windows client**합니다. 그런 다음 **Save**를 클릭합니다.

    ![에이전트 저장](./media/backup-configure-vault-classic/agent.png)
3. Hello MARSagentinstaller.exe 파일을 다운로드 한 후 클릭 **실행** (두 번 클릭 하거나 **MARSAgentInstaller.exe** hello 저장 위치에서).
4. Hello 설치 폴더 및 hello 에이전트에 필요한 캐시 폴더를 선택 하 고 클릭 한 다음 **다음**합니다. 지정한 hello 캐시 위치는 hello 백업 데이터의 최소 5% 같은 tooat 여유 공간이 있어야 합니다.
5. Hello 기본 프록시 설정을 통해 tooconnect toohello 인터넷을 계속할 수 있습니다.             Hello 프록시 구성 페이지에서 프록시 서버 tooconnect toohello 인터넷을 사용 하는 경우 선택 hello **사용자 지정 프록시 설정을 사용 하 여** 확인란을 선택한 다음 hello 프록시 서버 정보를 입력 합니다. 인증 된 프록시를 사용 하 여 hello 사용자 이름 및 암호 세부 정보를 입력 하 고 클릭 **다음**합니다.
6. 클릭 **설치** toobegin hello 에이전트를 설치 합니다. hello 백업 에이전트 설치.NET Framework 4.5 및 Windows PowerShell (설치 되어 있지 않음) 하는 경우 toocomplete hello 설치 합니다.
7. Hello 에이전트를 설치한 후 클릭 **tooRegistration 계속** hello 워크플로와 toocontinue 합니다.
8. Hello Id 자격 증명 모음 페이지에서 이전에 다운로드 한 tooand 선택 hello 자격 증명 모음 자격 증명 파일을 검색 합니다.

    hello 자격 증명 모음 자격 증명 파일은 hello 포털에서 다운로드 된 후 48 시간 동안만 유효 합니다. 에 오류가 발생 하는 경우 (예: "자격 증명 모음 자격 증명 제공 된 파일이 만료 되었습니다."),이 페이지 toohello 포털에 로그인 하 고 hello 자격 증명 모음 자격 증명 파일을 다시 다운로드 합니다.

    Hello 설치 응용 프로그램에서 액세스할 수 있는 위치에 해당 hello 자격 증명 모음 자격 증명 파일을 사용할 수 있는지 확인 합니다. 액세스와 관련 된 오류가 발생 하는 경우 복사 hello 자격 증명 모음 자격 증명 파일 tooa 임시 위치에 hello 동일 컴퓨터 하 고 hello 작업을 다시 시도 합니다.

    "잘못 된 자격 증명 모음 자격 증명을 제공"와 같은 자격 증명 모음 자격 증명 오류가 발생 하면 hello 파일이 손상 되었거나 hello 복구 서비스와 연결 된 최신 자격도 hello가 없습니다. Hello hello 포털에서 새 자격 증명 모음 자격 증명 파일을 다운로드 한 후 작업을 다시 시도 하십시오. Hello를 클릭 하는 경우에이 오류가 발생할 수 **자격 증명 모음 다운로드** 연속적으로 여러 번 옵션입니다. 이 경우에 hello 마지막 자격 증명 모음 자격 증명 파일이 유효한 합니다.
9. Hello 암호화 설정 페이지에서 암호를 생성 하거나 (최소 16 자)와 암호를 제공 합니다. 안전한 위치에 toosave hello 암호를 기억 합니다.
10. **마침**을 클릭합니다. 서버 등록 마법사 hello 백업을 사용 하 여 hello 서버를 등록합니다.

    > [!WARNING]
    > 끊어지거나 hello 암호를 잊은 경우 Microsoft hello 백업 데이터를 복구할 수 수 없습니다. 소유 하 고 암호화 암호는 hello 및 사용 하는 hello 암호에 대 한 가시성 갖고 있지 않습니다. 복구 작업 중 필요한 수 있으므로 hello 파일을 안전한 위치에 저장 합니다.
    >
    >

11. Hello 암호화 키가 설정 hello 유지 **Microsoft Azure 복구 서비스 에이전트 시작** 확인란을 선택 하 고 클릭 **닫기**합니다.

## <a name="complete-hello-initial-backup"></a>초기 백업을 완료 hello
초기 백업을 hello 두 가지 주요 작업이 포함 됩니다.

* Hello 백업 예약 만들기
* 처음으로 파일 및 hello에 대 한 폴더를 백업

백업 정책 hello hello 초기 백업을 완료 된 후 백업 지점을 toorecover hello 데이터 유지 해야 하는 경우 사용할 수 있는 만듭니다. hello 백업 정책을 정의 하는 hello 일정에 따라이 작업을 수행 합니다.

### <a name="tooschedule-hello-backup"></a>tooschedule hello 백업
1. Hello Microsoft Azure 백업 에이전트를 엽니다. (자동으로 열립니다 hello 두 었으 면 **Microsoft Azure 복구 서비스 에이전트를 시작** hello 서버 등록 마법사를 닫을 때 선택.) **Microsoft Azure 백업**에 대한 컴퓨터를 검색하여 찾을 수 있습니다.

    ![Hello Azure 백업 에이전트를 시작 합니다.](./media/backup-configure-vault-classic/snap-in-search.png)
2. Hello 백업 에이전트에서 클릭 **백업 예약**합니다.

    ![Windows Server 백업 예약](./media/backup-configure-vault-classic/schedule-backup-close.png)
3. Hello에 시작 hello 백업 예약 마법사의 페이지를 클릭 **다음**합니다.
4. Hello 항목 선택 tooBackup 페이지에서 클릭 **항목 추가**합니다.
5. Hello 파일 및 폴더, tooback 원하는 클릭 한 다음 선택 **알겠습니다**합니다.
6. **다음**을 누릅니다.
7. Hello에 **백업 일정 지정** 페이지에서 지정 하는 hello **백업 일정** 클릭 **다음**합니다.

    매일(하루에 최대 속도로 3회) 또는 매주 백업을 예약할 수 있습니다.

    ![Windows Server 백업에 대한 항목](./media/backup-configure-vault-classic/specify-backup-schedule-close.png)

   > [!NOTE]
   > Toospecify 백업 일정을 hello 하는 방법에 대 한 자세한 내용은 hello 문서 참조 [사용 하 여 Azure 백업 tooreplace 테이프 인프라](backup-azure-backup-cloud-as-tape.md)합니다.
   >
   >

8. Hello에 **보존 정책 선택** 페이지, 선택 hello **보존 정책** hello 백업 복사본에 대 한 합니다.

    hello 보존 정책 hello 백업이 저장 될 hello 기간을 지정 합니다. 모든 백업 지점에 대 한 "플랫 정책을"를 방금 지정 하는 대신 hello 백업이 발생 하는 경우에 따라 서로 다른 보존 정책을 지정할 수 있습니다. 매일, 매주, 매월 및 매년 보존 정책을 toomeet hello 요구에 맞게 수정할 수 있습니다.
9. Hello 초기 백업 유형 선택 페이지에서 hello 초기 백업 유형을 선택 합니다. Hello 옵션인 **hello 네트워크를 통해 자동으로** 을 선택한 다음 클릭 **다음**합니다.

    Hello 네트워크를 통해 자동으로를 백업할 수 있습니다 또는 오프 라인으로 백업할 수 있습니다. 이 문서의 나머지 부분에서는 hello 자동으로 백업에 대 한 hello 프로세스를 설명 합니다. 오프 라인 백업을 toodo 원한다 면 hello 문서를 검토 [Azure 백업에서 오프 라인 백업 워크플로](backup-azure-backup-import-export.md) 추가 정보에 대 한 합니다.
10. Hello 확인 페이지에서 hello 정보를 검토 한 다음 클릭 **마침**합니다.
11. Hello 마법사 hello 백업 예약 만들기를 완료 한 후 클릭 **닫기**합니다.

### <a name="enable-network-throttling-optional"></a>네트워크 제한 사용(선택 사항)
네트워크 제한 hello 백업 에이전트를 제공합니다. 제한 기능은 데이터 전송 중에 사용되는 네트워크 대역폭의 양을 제어합니다. 이 컨트롤 근무 시간 동안 데이터를 tooback 필요 하지만 다른 인터넷 트래픽과 hello 백업 프로세스 toointerfere 하지 않을 경우에 유용 합니다. 제한 tooback를 적용 하 고 복원 작업입니다.

**tooenable 네트워크 제한**

1. Hello 백업 에이전트에서 클릭 **속성 변경**합니다.

    ![속성 변경](./media/backup-configure-vault-classic/change-properties.png)
2. Hello에 **제한** 탭, 선택 hello **백업 작업에 대 한 인터넷 대역폭 제한을 사용 하도록 설정** 확인란 합니다.

    ![네트워크 제한](./media/backup-configure-vault-classic/throttling-dialog.png)
3. 제한을 사용 하도록 설정 하는 동안 백업 데이터 전송에 대 한 대역폭을 허용 하는 hello 지정 **근무 시간** 및 **휴무 시간**합니다.

    hello 대역폭 값 (Kbps) 초당 킬로 비트부터 시작 하 고 too1, 023 m b / 초 (MBps) 위로 이동할 수 있습니다. 또한 hello 시작을 지정 하 고 완료 수 **근무 시간**, hello 요일을 작업일 수로 간주 되며 합니다. 지정된 작업 시간 이외의 시간은 비 작업 시간으로 간주됩니다.
4. **확인**을 클릭합니다.

### <a name="tooback-up-now"></a>지금을 tooback
1. Hello 백업 에이전트에서 클릭 **지금 백업** toocomplete hello 시드 hello 네트워크를 통해 초기 합니다.

    ![지금 Windows Server 백업](./media/backup-configure-vault-classic/backup-now.png)
2. Hello 확인 페이지에서 지금 백업 마법사 hello hello 설정 검토 tooback hello 컴퓨터를 사용 합니다. 그런 다음 **백업**을 클릭합니다.
3. 클릭 **닫기** tooclose hello 마법사. 이렇게 하면 hello 백업 프로세스를 완료 하기 전에 hello 마법사 toorun hello 백그라운드에서 계속 됩니다.

Hello 초기 백업을 완료 되 면 hello **작업을 완료 했지만** hello 백업 콘솔에 상태가 표시 됩니다.

![IR 완료](./media/backup-configure-vault-classic/ircomplete.png)

## <a name="next-steps"></a>다음 단계
* [무료 Azure 계정](https://azure.microsoft.com/free/)을 등록합니다.

VM 또는 다른 워크로드를 백업하는 방법에 대한 자세한 내용은 다음을 참조하세요.

* [IaaS VM 백업](backup-azure-vms-prepare.md)
* [Microsoft Azure 백업 서버 워크 로드 tooAzure 백업](backup-azure-microsoft-azure-backup.md)
* [Dpm 작업 부하 tooAzure 백업](backup-azure-dpm-introduction.md)
