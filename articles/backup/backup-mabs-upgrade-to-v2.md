---
title: "Azure 백업 서버 v2 aaaInstall | Microsoft Docs"
description: "Azure Backup Server v2에서는 VM, 파일 및 폴더, 워크로드 등을 보호하기 위한 향상된 백업 기능을 제공합니다. 자세한 내용은 방법 tooinstall 또는 업그레이드 tooAzure 백업 서버 v 2입니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: 5b1699dadd3a173f1c0ef91a1a600bc5e12f20ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-azure-backup-server-v2"></a>Azure Backup Server v2 설치

Azure Backup Server를 사용하여 VM(가상 컴퓨터), 워크로드, 파일 및 폴더 등을 보호할 수 있습니다. Azure Backup Server v2는 Azure Backup Server v1을 기반으로 빌드되고 v1에서 사용할 수 없는 새로운 기능을 제공합니다. v1 및 v2의 기능 비교에 대해서는 [Azure Backup Server 보호 매트릭스](backup-mabs-protection-matrix.md)를 참조하세요. 

백업 서버 v 2에서 추가 기능 hello는 백업 서버 v 1에서 업그레이드 합니다. 하지만 Backup Server v1은 Backup Server v2를 설치하기 위한 필수 구성 요소가 아닙니다. 백업 서버 v1 tooBackup 서버 v2에서에서 tooupgrade 원한다 면 hello 백업 서버 보호 서버에 백업 서버 v 2를 설치 합니다. 기존 Backup Server 설정은 그대로 유지됩니다.

Backup Server v2를 Windows Server 2012 R2 또는 Windows Server 2016에 설치할 수 있습니다. 새 기능을 활용 tootake 같은 System Center 2016 데이터 보호 Manager 최신 백업 저장소, Windows Server 2016에는 백업 서버 v 2를 설치 해야 합니다. 백업 서버 v2 tooor 설치를 업그레이드 하기 전에 hello에 대 한 읽기 [설치 필수 구성 요소](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites)합니다.

> [!NOTE]
> Azure 백업 서버 hello에 동일한 코드 베이스로 System Center Data Protection Manager. 백업 서버 v 1은 해당 tooData Protection Manager 2012 R2, 및 백업 서버 v 2는 해당 tooData Protection Manager 2016 합니다. 이 문서는 가끔 hello Data Protection Manager 설명서를 참조합니다.
>
>

## <a name="upgrade-backup-server-toov2"></a>백업 서버 toov2 업그레이드
tooupgrade 백업 서버 v1 tooBackup 서버 v 2에서에서 설치에 필요한 hello 업데이트가 설치 되었는지 확인 합니다.

- [Hello 보호 에이전트 업데이트](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) hello에 서버를 보호 합니다.
- Windows Server 2012 R2 tooWindows Server 2016 업그레이드 합니다.
- 모든 프로덕션 서버에서 Azure Backup Server 원격 관리자를 업그레이드합니다.
- 백업을 toocontinue 프로덕션 서버를 다시 시작 하지 않고 설정 되어 있는지 확인 합니다.


### <a name="upgrade-steps-for-backup-server-v2"></a>Backup Server v2에 대한 업그레이드 단계

1. Hello 다운로드 센터에서에서 [hello 업그레이드 설치 관리자 다운로드](https://go.microsoft.com/fwlink/?LinkId=626082)합니다.

2. 설치 마법사 hello 압축을 푼 후 다음 사항을 확인 **setup.exe를 실행** 을 선택한 다음 선택 **마침**합니다.

  ![설치 관리자 - 설치 프로그램 실행](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. Hello Microsoft Azure 백업 서버 마법사에서 아래 **설치**선택, **Microsoft Azure 백업 서버**합니다.

  ![설치 관리자 - 설치 선택](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. Hello에 **시작** 페이지 hello 경고를 검토 한 다음 선택 **다음**합니다.

  ![설치 관리자 - 시작 페이지](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. hello 설치 마법사는 필수 구성 요소 검사 toomake 환경을 업그레이드할 수 있는지를 수행 합니다. Hello에 **Prerequisite Checks** 페이지에서 **확인**합니다.

  ![설치 관리자 - 필수 구성 요소 확인 페이지](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. 사용자 환경 hello 필수 구성 요소 검사를 통과 해야 합니다. 사용자 환경 hello 검사를 통과 하지 않는 hello 문제에 유의 수정 하십시오. 그다음에 **다시 확인**을 선택합니다. Hello 필수 구성 요소 검사를 통과 한 후 선택 **다음**합니다.

  ![설치 관리자 - 다시 확인 단추](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. Hello에 **SQL 설정** 페이지 hello SQL 설치를 위한 관련 옵션을 선택 하 고 다음 선택 **확인 후 설치**합니다.

  ![설치 관리자 - SQL 설정 페이지](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  hello 검사 몇 분 정도 걸릴 수 있습니다. Hello 검사는 완료, 선택 때 **다음**합니다.

  ![설치 관리자 - SQL 설정 확인 및 설치 단추](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and fix-settings.png)

8. Hello에 **설치 설정** 페이지에서 백업 서버 설치 되어 있는 모든 변경 내용 toohello 위치 또는 toohello 스크래치 위치를 확인 합니다. **다음**을 선택합니다.

  ![설치 관리자 - 설치 설정 페이지](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. toofinish hello 설치 마법사에서 선택 **마침**합니다.

  ![설치 관리자 - 마침](./media/backup-mabs-upgrade-to-v2/run-setup.png)



## <a name="add-storage-for-modern-backup-storage"></a>Modern Backup Storage에 대한 저장소 추가

tooimprove 백업 저장소 효율성을 백업 서버 v2 볼륨에 대 한 지원을 추가합니다. Backup Server v1처럼 Backup Server v2는 디스크를 지원합니다.

### <a name="add-volumes-and-disks"></a>볼륨 및 디스크 추가
Windows Server 2016의 백업 서버 v 2를 실행 하는 경우에 볼륨 toostore 백업 데이터를 사용할 수 있습니다. 볼륨을 사용하면 저장소가 절약되고 더 빠르게 백업할 수 있습니다. 볼륨은 새 tooBackup 서버 이기 때문에 추가 해야 합니다. 

볼륨 tooBackup 서버를 추가 하면 hello 볼륨을는 친숙 한 이름을 지정할 수 있습니다. Hello 클릭 **이름** 열 tooname hello 볼륨의 원하는 합니다. 필요한 경우 나중에 hello 이름을 변경할 수 있습니다. 또한 PowerShell tooadd 사용 하거나 변경할 수 있습니다 볼륨에 대 한 친숙 한 이름을 합니다.

tooadd hello 관리자 콘솔에서에서 볼륨:

1. Hello Azure 백업 서버 관리자 콘솔에서에서 선택 **관리** > **디스크 저장소** > **추가**합니다.

    ![열기 hello 디스크 저장소 추가 마법사](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

    Hello 디스크 저장소 추가 마법사를 엽니다.

2. Hello에 **디스크 저장소 추가** 페이지 hello **사용할 수 있는 볼륨** 상자 볼륨을 선택한 다음 선택 **추가**합니다.
3. Hello에 **볼륨 선택** 상자 hello 볼륨에 대 한 이름을 입력 한 다음 선택 **확인**합니다.

      ![디스크 저장소 추가 마법사 - 볼륨 추가](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  디스크 tooadd 원한다 면 hello 디스크는 tooa 보호 그룹 레거시 저장소에 속해 있어야 합니다. 이러한 디스크는 해당 보호 그룹에만 사용할 수 있습니다. 백업 서버에는 레거시 보호 된 원본의 없으면 hello 디스크 나열 되지 않습니다.

  디스크를 추가 하는 방법에 대 한 자세한 내용은 참조 [디스크 tooincrease 레거시 저장소 추가](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage)합니다. 디스크에는 이름을 지정할 수 없습니다.


### <a name="assign-workloads-toovolumes"></a>작업 부하 toovolumes 할당

백업 서버 작업이 toowhich 볼륨에 할당 된 지정 합니다. 예를 들어 비용이 많이 드는 볼륨을 지 원하는 많은 수의 두 번째 (IOPS) toostore 전용 작업 자주, 대용량 백업 해야 하는 초당 입력/출력 작업을 설정할 수 있습니다. 예를 들어 트랜잭션 로그가 포함된 SQL Server가 있습니다.

#### <a name="update-dpmdiskstorage"></a>Update-DPMDiskStorage

백업 서버 hello 저장소 풀의 볼륨의 tooupdate hello 속성 업데이트 DPMDiskStorage hello PowerShell cmdlet을 사용 합니다.

구문

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

PowerShell을 사용 하 여 수행한 모든 변경 내용은 hello UI에에서 반영 됩니다.


## <a name="protect-data-sources"></a>데이터 원본 보호
데이터 원본을 보호 하는 toobegin, 보호 그룹을 만듭니다. hello 강조 변경 또는 추가 사항을 toohello 새 보호 그룹 마법사 단계를 수행 합니다.

보호 그룹 toocreate:

1. Hello 백업 서버 관리자 콘솔에서에서 선택 **보호**합니다.

2. Hello 도구 리본에서 선택 **새로**합니다.

    Hello 새 보호 그룹 만들기 마법사를 엽니다.

  ![새 보호 그룹 만들기 마법사](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. Hello에 **시작** 페이지에서 **다음**합니다.
4. Hello에 **보호 그룹 종류 선택** 페이지에서 보호 그룹 toocreate, 한 다음 선택의 hello 유형을 선택 **다음**합니다.

  ![보호 그룹 형식 선택 페이지](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. Hello에 **그룹 구성원 선택** 페이지 hello **사용 가능한 구성원** 창, hello 구성원과 보호 에이전트와 같습니다. 예를 들어 D:\ 볼륨을 선택 하 고 E:\ toohello 추가할 **선택한 구성원** 창. **다음**을 선택합니다.

  ![그룹 구성원 선택 페이지](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. Hello에 **데이터 보호 방법 선택** 페이지에서 입력 한 **보호 그룹 이름이**hello 보호 방법을 선택한 다음 선택 **다음**합니다. 단기 보호 하려는 경우에 hello 선택 해야 **디스크** 메서드를 백업 합니다.

  ![데이터 보호 방법 선택 페이지](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. Hello에 **단기 목표 지정** 페이지에 대 한 세부 정보 선택 hello **보존 범위** 및 **동기화 빈도**합니다. 그다음에 **다음**을 선택합니다. 필요에 따라 toochange hello 일정을 작성, 선택 복구 지점이 표시 되는 경우 **수정**합니다.

  ![단기 목표 지정 페이지](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. Hello에 **디스크 저장소 할당 검토** 페이지 선택한 hello 데이터 원본에 대 한 세부 정보, 크기 및 hello 공간 toobe 프로 비전에 대 한 값을 검토 하 고 대상 저장소 볼륨 hello 합니다.

  ![디스크 저장소 할당 검토 페이지](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  저장소 볼륨 hello 작업 볼륨 할당 (PowerShell을 사용 하 여 설정)를 기반으로 하 고 사용 가능한 저장소 hello 합니다. Hello 드롭 다운 메뉴에서 다른 볼륨을 선택 하 여 hello 저장소 볼륨을 변경할 수 있습니다. Hello 값을 변경 하는 경우 **대상 저장소**, 값에 대 한 hello **사용 가능한 디스크 저장소** tooreflect 아래에 값을 동적으로 변경 **여유 공간이** 및 **공간 underprovisioned**합니다.

  데이터 원본 hello 증가 함에 따라 계획 한 대로 경우 hello hello에 대 한 값 **Underprovisioned 공간** 열에 **사용 가능한 디스크 저장소** hello 필요한 추가 저장소 크기를 반영 합니다. 저장소 요구량 부드러운 백업에 대 한이 값 toohelp 계획을 사용 합니다. Hello 값이 0 이면 많은 경우 저장소에 잠재적 문제가 없는지 hello 장래에 합니다. 할당 된 충분 한 저장소가 없는 hello 값이 0이 아닌 숫자 이면 (보호 된 멤버의 사용자 보호 정책 및 hello 데이터 크기에 따라).

  ![미달 할당된 디스크 저장소](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

   보호 그룹, 전체 hello 마법사 만들기 toofinish 합니다.

## <a name="migrate-legacy-storage-toomodern-backup-storage"></a>레거시 저장소 tooModern 백업 저장소 마이그레이션
백업 서버 v2 tooor 설치 및 업그레이드 hello 운영 체제 tooWindows Server 2016로 업그레이드 한 후 보호 그룹 toouse 최신 백업 저장소를 업데이트 합니다. 기본적으로 보호 그룹은 변경되지 않습니다. 처음 설정 된 것 처럼 toofunction을 계속 합니다. 

보호 그룹 toouse 최신 백업 저장소를 업데이트 하는 것은 선택 사항입니다. tooupdate hello 보호 그룹 데이터 옵션을 보관 하는 hello를 사용 하 여 모든 데이터 원본의 보호를 중지 합니다. Hello 데이터 원본 tooa 새 보호 그룹을 추가 합니다.

1. Hello 관리자 콘솔에서에서 선택 hello **보호** 기능입니다. Hello에 **보호 그룹 구성원** 목록 오른쪽 hello 멤버를 마우스 오른쪽 단추로 클릭 한 다음 선택 **구성원 보호 중지**합니다.

  ![구성원 보호 중지](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. Hello에 **그룹에서 제거** 대화 상자, 검토 hello 사용 되는 디스크 공간 및 hello hello 저장소 풀에 사용 가능한 공간이 있습니다. hello 기본 hello 디스크에 tooleave hello 복구 지점 이며 해당 관련된 보존 정책에 따라 tooexpire를 허용 합니다. **확인**을 클릭합니다.

  Tooimmediately 반환 hello 사용 되는 디스크 공간 toohello 사용 가능한 저장소 풀을 사용 하도록 하려는 경우 선택 hello **디스크에서 복제본 삭제** 해당 멤버와 연결 된 확인란 toodelete hello에 대 한 백업 데이터 (및 복구 지점)입니다.

  ![그룹에서 제거 대화 상자](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. Modern Backup Storage를 사용하는 보호 그룹을 만듭니다. 보호 되지 않은 상태로 hello 데이터 소스를 포함 합니다.


## <a name="add-disks-tooincrease-legacy-storage"></a>디스크 tooincrease 레거시 저장소 추가

백업 서버와 toouse 레거시 저장 하려는 경우 tooadd 디스크 tooincrease 레거시 저장소를 할 수 있습니다. 

tooadd 디스크 저장소:

1. Hello 관리자 콘솔에서에서 선택 **관리** > **디스크 저장소** > **추가**합니다.

    ![디스크 저장소 추가 대화 상자](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. Hello에 **디스크 저장소 추가** 대화 상자에서 **디스크 추가**합니다.

5. 사용 가능한 디스크의 hello 목록에서 선택 tooadd, hello 디스크 **추가**를 선택한 후 **확인**합니다.

## <a name="update-hello-data-protection-manager-protection-agent"></a>Hello Data Protection Manager 보호 에이전트를 업데이트 합니다.

백업 서버 업데이트에 대 한 hello System Center Data Protection Manager 보호 에이전트를 사용합니다. 연결 된 toohello 네트워크를 보호 에이전트를 업그레이드 하는 hello 관리자 콘솔 toocomplete 연결된 된 에이전트 업그레이드를 사용할 수 없습니다. 비활성 도메인 환경에서 hello 보호 에이전트를 업그레이드 해야 합니다. Hello 클라이언트 컴퓨터가 연결 된 toohello 네트워크 인 될 때까지 관리자 콘솔에서 해당 hello 보호 에이전트 업데이트 표시 hello 보류 중입니다.

hello 다음 섹션에서는 설명 어떻게 연결 되어 있는 클라이언트 컴퓨터와 연결 되지 않은 클라이언트 컴퓨터에 대 한 보호 에이전트 tooupdate 합니다.

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a>연결된 클라이언트 컴퓨터에 대한 보호 에이전트 업데이트

1. Hello 백업 서버 관리자 콘솔에서에서 선택 **관리** > **에이전트**합니다.

2. Hello 디스플레이 창에서 원하는 tooupdate hello 보호 에이전트를 hello 클라이언트 컴퓨터를 선택 합니다.

  > [!NOTE]
  > hello **에이전트 업데이트** 보호 에이전트 업데이트를 각 보호 된 컴퓨터에 사용할 수 있는 경우 열에 표시 합니다. Hello에 **동작** 창, hello **업데이트** 작업은 사용할 수 있고 경우에 보호 된 컴퓨터가 선택 된 업데이트를 사용할 수 있습니다.
  >
  >

3. tooinstall hello에 hello 선택한 컴퓨터에 보호 에이전트 업데이트 **동작** 창 선택 **업데이트**합니다.

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a>연결되지 않은 클라이언트 컴퓨터에 대한 보호 에이전트 업데이트

1. Hello 백업 서버 관리자 콘솔에서에서 선택 **관리** > **에이전트**합니다.

2. Hello 디스플레이 창에서 원하는 tooupdate hello 보호 에이전트를 hello 클라이언트 컴퓨터를 선택 합니다.

  > [!NOTE]
   > hello **에이전트 업데이트** 보호 에이전트 업데이트를 각 보호 된 컴퓨터에 사용할 수 있는 경우 열에 표시 합니다. Hello에 **동작** 창, hello **업데이트** 없는데 보호 된 컴퓨터에서 선택 된 업데이트를 사용할 수 있는 경우이 작업은 수행할 수 없습니다.
  >
  >

3. tooinstall hello 선택한 컴퓨터에 보호 에이전트 업데이트 **업데이트**합니다.

4. Hello 컴퓨터에 연결 된 toohello 네트워크 될 때까지 toohello 네트워크 연결 되지 않은 클라이언트 컴퓨터에 대 한 hello **에이전트 상태** 열 표시의 상태 **업데이트 보류 중**합니다.

  클라이언트 컴퓨터에 연결 된 toohello 네트워크 되 면 hello **에이전트 업데이트** hello 클라이언트 컴퓨터에 대 한 열에 상태가 표시 **업데이트**합니다.
  
### <a name="move-legacy-protection-groups-from-old-version-and-sync-hello-new-version-with-azure"></a>이전 버전 및 Azure 사용한 동기화 hello 새 버전에서 기존 보호 그룹 이동

Azure 백업 서버 및 운영 체제 hello 모두 업데이트 되 준비 tooprotect 최신 백업 저장소를 사용 하는 새 데이터 원본이 됩니다. 그러나 이미 보호 된 데이터 원본 toobe 방식으로 Azure 백업 서버에 있는 것 이지만 모든 새 보호 그룹에서 최신 백업 저장소를 사용 하는 레거시 hello에서 보호를 계속 합니다.

다음 단계는 toomigrate 데이터 소스 보호 tooModern 백업 저장소의 레거시 모드에서입니다.

•는 Hello 새 볼륨 toohello DPM 저장소 풀을 추가 하 고 원하는 경우 친숙 한 이름 및 데이터 소스 태그를 할당 합니다.
레거시 모드에서는 보호를 중지 하 고 "보호 된 데이터 보존" hello 데이터 원본에에서 있는 각 데이터 원본에 대 한 • 합니다.  이렇게 하면 마이그레이션 후 이전 복구 지점을 복구할 수 있게 됩니다.

• 새 PG 만들고 toobe 새 형식을 사용 하 여 저장 하는 hello 데이터 원본이 선택 합니다.
• DPM hello 최신 백업 저장소 볼륨을 로컬에 hello 레거시 백업 저장소에서 복제본 복사를 수행 합니다.
참고: 이 작업은 사후 복구 작업으로 간주됩니다. • 그런 다음 모든 새로운 동기화 및 복구 지점은 Modern Backup Storage에 저장됩니다.
• 이전 복구 지점이 만료 되 고 결국 hello 디스크 공간을 확보 아웃 정리 됩니다.
• 모든 hello 레거시 볼륨 hello 이전 저장소를 hello 디스크에서 삭제 한 후 Azure 백업 및 hello 시스템에서 제거할 수 있습니다.
•는 Hello Azure DPMDB의 백업을 수행 합니다.

2 부:-중요 한 항목 > 새 서버 hello toobe hello 원래 Azure 백업 서버와 같은 이름으로 지정 해야 합니다. Toouse 이전 저장소 풀에서 사용할 DPMDB tooretain 복구 지점-있어야 DPMDB의 백업을 복원 toobe 필요 하는 경우에 hello 이름을 hello 새 Azure 백업 서버를 변경할 수 없습니다.

1) 종료 원래 Azure 백업 서버 hello 또는 hello 와이어 오프 라인입니다.
2) Active directory의 hello 컴퓨터 계정 다시 설정 합니다.
3) 원래 Azure 백업 서버 hello와 동일한 컴퓨터 이름을 hello 이름과 새 컴퓨터에 서버 2016을 설치 합니다.
4) Hello 도메인 가입
5) Azure Backup Server V2 설치(DPM 저장소 풀 디스크를 이전 서버에서 이동 및 가져오기)
6) 2 부의 끝에서 가져온 DPMDB hello 복원
7) Hello 원본 서버 백업 toohello 새 서버에서 hello 저장소에 연결 합니다.
8) SQL 복원 hello DPMDB에서
9) 관리자의 새로운 서버 cd tooMicrosoft Azure 백업에서 명령줄 설치 위치 및 bin 폴더

경로 예: C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\
tooAzure 백업 실행 DPMSYNC-SYNC

10) Dpmsync-SYNC 참고 hello 이전 구성을 이동 하는 대신 새 toohello DPM 저장소 풀 디스크를 추가한 경우 DPMSYNC-Reallocatereplica 실행 한 다음

## <a name="new-powershell-cmdlets-in-v2"></a>v2의 새로운 PowerShell cmdlet

Azure Backup Server v2를 설치하면 두 개의 새로운 cmdlet을 사용할 수 있습니다. 
* [Mount-DPMRecoveryPoint](https://technet.microsoft.com/library/mt787159.aspx)
* [Dismount-DPMRecoveryPoint](https://technet.microsoft.com/library/mt787158.aspx)

## <a name="next-steps"></a>다음 단계

자세한 내용은 방법 tooprepare 서버 작업 보호를 시작 하거나:
- [Backup Server 워크로드 준비](backup-azure-microsoft-azure-backup.md)
- [백업 서버 tooback VMware 서버를 사용 하 여](backup-azure-backup-server-vmware.md)
- [SQL Server를 tooback 백업 서버를 사용 하 여](backup-azure-sql-mabs.md)
- [Backup Server에서 Modern Backup Storage 사용](backup-mabs-add-storage.md)

