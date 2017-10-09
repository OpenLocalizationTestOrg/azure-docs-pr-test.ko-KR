---
title: "스냅숏 관리자 백업 카탈로그 aaaStorSimple | Microsoft Docs"
description: "Toouse StorSimple 스냅숏 관리자 MMC 스냅인 tooview hello 하 및 hello 백업 카탈로그를 관리 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 6abdbfd2-22ce-45a5-aa15-38fae4c8f4ec
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 173410095bcec7948d780d7fc258d2e3670bde8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toomanage-hello-backup-catalog"></a>StorSimple 스냅숏 관리자를 사용 하 여 toomanage hello 백업 카탈로그

## <a name="overview"></a>개요
hello 기본 기능은 StorSimple 스냅숏 관리자의 tooallow 있습니다 toocreate 응용 프로그램 일치 백업 사본을 스냅숏 형식의 hello에 StorSimple 볼륨입니다. 스냅숏은 *백업 카탈로그*라는 XML 파일에 나열됩니다. hello 백업 카탈로그는 스냅숏을 볼륨 그룹별로 한 다음 로컬 스냅숏 또는 클라우드 스냅숏을 구성합니다.

이 자습서에서는 hello를 사용 하는 방법을 설명 **백업 카탈로그** 노드 toocomplete hello 작업을 수행 합니다.

* 볼륨 복원
* 볼륨 또는 볼륨 그룹 복제
* 백업 삭제
* 파일 복구
* Hello Storsimple 스냅숏 관리자 데이터베이스 복원

Hello를 확장 하 여 hello 백업 카탈로그를 볼 수 **백업 카탈로그** hello에 대 한 노드 **범위** 창 및 다음 hello 볼륨 그룹을 확장 합니다.

* Hello 볼륨 그룹 이름을 클릭 hello **결과** 창 로컬 스냅숏과 클라우드 스냅숏 hello 볼륨 그룹에 사용할 수 있는 hello 수를 표시 합니다. 
* 클릭 하면 **로컬 스냅숏** 또는 **클라우드 스냅숏**, hello **결과** 창에는 다음 각 백업 스냅숏에 대 한 정보는 hello 표시 (사용자 에따라**보기** 설정):
  
  * **이름** – hello 시간 hello 스냅숏이 만들어진 합니다.
  * **유형** – 로컬 스냅숏인지 또는 클라우드 스냅숏인지.
  * **소유자** – hello 콘텐츠 소유자입니다. 
  * **사용 가능한** hello 스냅숏이 현재 사용할 수 있는지 여부를 – 합니다. **True** 나타내고 해당 hello 스냅숏을 ´ ï ´ 복원할 수 있습니다. **False** 해당 hello 스냅숏을 더 이상 사용할 수 있음을 나타냅니다. 
  * **가져온** – hello 백업을 가져왔는지 여부입니다. **True** hello 백업 hello 서비스 hello 시간 hello 장치에서 StorSimple 스냅숏 관리자에 구성 된 StorSimple 장치 관리자에서에서 가져온 나타냅니다. **False** 를 가져오지 못한 있지만 StorSimple 스냅숏 관리자가 만든 나타냅니다. (쉽게 식별할 수 있습니다는 가져온된 볼륨 그룹 이므로 hello 볼륨 그룹 가져온 hello 장치를 식별 하는 접미사가 추가 됩니다.)
    
    ![백업 카탈로그](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Backup_catalog.png)
* 확장 하는 경우 **로컬 스냅숏** 또는 **클라우드 스냅숏**, 누른 다음 개별 스냅숏 이름을 hello **결과** 창 hello 다음 hello에 대 한 정보를 보여 줍니다. 선택한 스냅숏:
  
  * **이름** – 드라이브 문자로 식별 되는 볼륨 hello 합니다. 
  * **로컬 이름** – hello hello 드라이브 (사용 가능한 경우)의 로컬 이름입니다. 
  * **장치** – hello는 hello에 볼륨이 있는 hello 장치의 이름입니다. 
  * **사용 가능한** hello 스냅숏이 현재 사용할 수 있는지 여부를 – 합니다. **True** 나타내고 해당 hello 스냅숏을 ´ ï ´ 복원할 수 있습니다. **False** 해당 hello 스냅숏을 더 이상 사용할 수 있음을 나타냅니다. 

## <a name="restore-a-volume"></a>볼륨 복원
Hello 프로시저 toorestore 볼륨을 백업에서 다음을 사용 합니다.

#### <a name="prerequisites"></a>필수 조건
이미 수행 하는 경우 볼륨 및 볼륨 그룹을 만들고 hello 볼륨을 삭제 합니다. 기본적으로 toobe 삭제를 허용 하기 전에 StorSimple 스냅숏 관리자 볼륨을 백업 합니다. 이 예방 조치로 hello 볼륨을 실수로 삭제 하거나 hello 데이터 toobe 어떤 이유로 든 복구할 경우 데이터 손실을 방지할 수 있습니다. 

StorSimple 스냅숏 관리자 hello hello 문제 예방용 백업을 생성 되는 동안 메시지의 뒤에 표시 됩니다.

![자동 스냅숏 메시지](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Automatic_snap.png) 

> [!IMPORTANT]
> 볼륨 그룹에 속해 있는 볼륨은 삭제할 수 없습니다. hello 삭제 옵션을 사용할 수 없습니다. <br>
> 
> 

#### <a name="toorestore-a-volume"></a>toorestore 볼륨
1. Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다. 
2. Hello에 **범위** 창의 hello 확장 **백업 카탈로그** 노드, 볼륨 그룹을 확장 하 고 클릭 **로컬 스냅숏** 또는 **클라우드 스냅숏**. 백업 스냅숏 목록이 hello에 표시 **결과** 창.
3. 찾기 hello 백업 toorestore 마우스 오른쪽 단추를 클릭 한 다음 원하는 **복원**합니다.
   
    ![백업 카탈로그 복원](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Restore_BU_catalog.png) 
4. Hello 확인 페이지에서 hello 세부 사항 입력 **확인**, 클릭 하 고 **확인**합니다. StorSimple 스냅숏 관리자 hello 백업 toorestore hello 볼륨을 사용합니다.
   
    ![확인 메시지 복원](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Restore_volume_msg.png) 
5. 실행할 때 hello 복원 작업을 모니터링할 수 있습니다. Hello에 **범위** 창의 hello 확장 **작업** 노드를 차례로 클릭 한 다음 **실행**합니다. hello에 hello 작업 세부 정보 표시 **결과** 창. Hello 작업 세부 정보는 전송 된 toohello hello 복원 작업이 완료 되 면 **마지막 24 시간** 목록입니다.

## <a name="clone-a-volume-or-volume-group"></a>볼륨 또는 볼륨 그룹 복제
다음 프로시저 toocreate 볼륨 또는 볼륨 그룹의 복제본 (클론) hello를 사용 합니다.

#### <a name="tooclone-a-volume-or-volume-group"></a>tooclone 볼륨 또는 볼륨 그룹
1. Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.
2. Hello에 **범위** 창의 hello 확장 **백업 카탈로그** 노드, 볼륨 그룹을 확장 하 고 클릭 **클라우드 스냅숏**합니다. Hello에 백업 목록이 표시 **결과** 창.
3. Hello 볼륨 또는 볼륨 그룹을 클릭 하 고 tooclone, 마우스 오른쪽 단추로 클릭 hello 볼륨 또는 볼륨 그룹 이름을 지정 하 찾기 **복제**합니다. hello **클라우드 스냅숏 복제** 대화 상자가 나타납니다.
   
    ![클라우드 스냅숏 복제](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Clone.png) 
4. 전체 hello **클라우드 스냅숏 복제** 다음과 같이 대화 상자: 
   
   1. Hello에 **이름** 입력란 hello에 대 한 이름 입력 볼륨을 복제 합니다. 이 이름은 hello에 나타납니다. **볼륨** 노드. 
   2. (선택 사항) 선택 **드라이브**, hello 드롭 다운 목록에서 드라이브 문자를 선택 합니다.
   3. (선택 사항) 선택 **폴더 (NTFS)**, 및 폴더 경로 입력 하거나 찾아보기를 클릭 하 고 hello 폴더에 대 한 위치를 선택 합니다. 
   4. **만들기**를 클릭합니다.
5. Hello 복제 프로세스가 완료 되 면 hello 복제 볼륨을 초기화 해야 합니다. 서버 관리자를 시작한 다음 디스크 관리를 시작합니다. 자세한 지침은 [볼륨 탑재](storsimple-snapshot-manager-manage-volumes.md#mount-volumes)를 참조하세요. 초기화 되 면 hello 볼륨 hello 나열 됩니다 **볼륨** hello에 대 한 노드 **범위** 창. Hello 볼륨이 나열 되어 표시 되지 않으면 hello 볼륨 목록을 새로 고칩니다 (마우스 오른쪽 단추 클릭 hello **볼륨** 노드를 차례로 클릭 한 다음 **새로 고침**).

## <a name="delete-a-backup"></a>백업 삭제
Hello 프로시저 toodelete 스냅숏으로 hello 백업 카탈로그에서 다음을 사용 합니다. 

> [!NOTE]
> Hello 스냅숏와 관련 된 데이터를 백업 하는 hello를 삭제에서 스냅숏을 삭제 합니다. 그러나 hello hello 클라우드에서 데이터 정리 프로세스는 다소 시간이 걸릴 수 있습니다.<br>


#### <a name="toodelete-a-backup"></a>toodelete 백업
1. Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.
2. Hello에 **범위** 창의 hello 확장 **백업 카탈로그** 노드, 볼륨 그룹을 확장 하 고 클릭 **로컬 스냅숏** 또는 **클라우드 스냅숏**. Hello에 스냅숏 목록이 표시 **결과** 창.
3. 마우스 오른쪽 단추로 클릭 hello 스냅숏 toodelete을 차례로 클릭 **삭제**합니다.
4. Hello 확인 메시지가 나타나면 클릭 **확인**합니다.

## <a name="recover-a-file"></a>파일 복구
볼륨에서 파일을 실수로 삭제 되는 경우 이전 hello 삭제, 스냅숏 toocreate hello를 사용 하 여 날짜 스냅숏 hello 볼륨의 복제본을 검색 하 여 hello 파일을 복구할 수 있습니다 및 복제 볼륨 toohello 원래 볼륨 hello hello 파일을 복사 하 여 합니다.

#### <a name="prerequisites"></a>필수 조건
시작 하기 전에 hello 볼륨 그룹의 최신 백업이 있는지 확인 합니다. 그런 다음 해당 볼륨 그룹의 hello 볼륨 중 하나에 저장 된 파일을 삭제 합니다. 마지막으로 사용 하 여 hello toorestore hello 단계를 수행 하려면 백업에서 파일을 삭제 합니다. 

#### <a name="toorecover-a-deleted-file"></a>toorecover 삭제 된 파일
1. 바탕 화면에 hello StorSimple 스냅숏 관리자 아이콘을 클릭 합니다. hello StorSimple 스냅숏 관리자 콘솔 창이 나타납니다. 
2. Hello에 **범위** 창 hello 확장 **백업 카탈로그** 노드와 찾아보기 tooa 스냅숏을 삭제 하는 hello 파일이 들어 있는입니다. 일반적으로 hello 삭제 되기 바로 전에 만든 스냅숏을 선택 해야 합니다.
3. 찾기 hello 볼륨 tooclone 마우스 오른쪽 단추를 클릭 하 여 원하는 **복제**합니다. hello **클라우드 스냅숏 복제** 대화 상자가 나타납니다.
   
    ![클라우드 스냅숏 복제](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Clone.png) 
4. 전체 hello **클라우드 스냅숏 복제** 다음과 같이 대화 상자: 
   
   1. Hello에 **이름** 입력란 hello에 대 한 이름 입력 볼륨을 복제 합니다. 이 이름은 hello에 나타납니다. **볼륨** 노드. 
   2. (선택 사항) 선택 **드라이브**, hello 드롭 다운 목록에서 드라이브 문자를 선택 합니다. 
   3. (선택 사항) 선택 **폴더 (NTFS)**, 폴더 경로 입력 하거나 클릭 하 고 **찾아보기** hello 폴더의 위치를 선택 합니다. 
   4. **만들기**를 클릭합니다. 
5. Hello 복제 프로세스가 완료 되 면 hello 복제 볼륨을 초기화 해야 합니다. 서버 관리자를 시작한 다음 디스크 관리를 시작합니다. 자세한 지침은 [볼륨 탑재](storsimple-snapshot-manager-manage-volumes.md#mount-volumes)를 참조하세요. 초기화 되 면 hello 볼륨 hello 나열 됩니다 **볼륨** hello에 대 한 노드 **범위** 창. 
   
    Hello 볼륨이 나열 되어 표시 되지 않으면 hello 볼륨 목록을 새로 고칩니다 (마우스 오른쪽 단추 클릭 hello **볼륨** 노드를 차례로 클릭 한 다음 **새로 고침**).
6. Hello 복제 볼륨을 포함 하는 hello open NTFS 폴더 확장 hello **볼륨** 노드를 차례로 연 다음 hello 복제 볼륨입니다. Toorecover, 원하는 toohello 기본 볼륨을 복사 하는 hello 파일을 찾습니다.
7. Hello 파일을 복원한 후에 hello 복제 볼륨을 포함 하는 hello NTFS 폴더를 삭제할 수 있습니다.

## <a name="restore-hello-storsimple-snapshot-manager-database"></a>Hello StorSimple 스냅숏 관리자 데이터베이스 복원
Hello StorSimple 스냅숏 관리자 데이터베이스 hello 호스트 컴퓨터에서 정기적으로 백업 해야 합니다. 재해가 발생 또는 hello 호스트 컴퓨터에서 어떤 이유로 든 오류가 발생 하는 경우 hello 백업에서 다음 복원할 수 있습니다. Hello 데이터베이스 백업 만들기는 수동 프로세스입니다.

#### <a name="tooback-up-and-restore-hello-database"></a>tooback 및 hello 데이터베이스 복원
1. Hello Microsoft StorSimple 관리 서비스를 중지 합니다.
   
   1. 서버 관리자를 시작합니다.
   2. Hello에 hello 서버 관리자 대시보드의 **도구** 메뉴 선택 **서비스**합니다.
   3. Hello에 **서비스** 창, 선택 hello **Microsoft StorSimple 관리 서비스**합니다.
   4. Hello에서 마우스 오른쪽 단추로 창 아래에서 **Microsoft StorSimple 관리 서비스**, 클릭 **hello 서비스 중지**합니다.
2. Hello 호스트 컴퓨터에서 tooC:\ProgramData\Microsoft\StorSimple\BACatalog를 찾습니다. 
   
   > [!NOTE]
   > ProgramData는 숨겨진 폴더입니다.
   > 
   > 
3. Hello 클라우드 또는 안전한 장소에 hello 카탈로그 XML 파일, 복사 hello 파일 및 저장소 hello 복사본을 찾습니다. Hello 호스트가 실패 하면이 백업 파일 toohelp 복구 hello 백업 만든 정책을 StorSimple 스냅숏 관리자를 사용할 수 있습니다.
   
    ![Azure StorSimple 백업 카탈로그 파일](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_bacatalog.png)
4. Hello Microsoft StorSimple 관리 서비스를 다시 시작 합니다. 
   
   1. Hello에 hello 서버 관리자 대시보드의 **도구** 메뉴 선택 **서비스**합니다.
   2. Hello에 **서비스** 창, 선택 hello **Microsoft StorSimple 관리 서비스**합니다.
   3. Hello에서 마우스 오른쪽 단추로 창 아래에서 **Microsoft StorSimple 관리 서비스**, 클릭 **hello 서비스를 다시 시작**합니다.
5. Hello 호스트 컴퓨터에서 tooC:\ProgramData\Microsoft\StorSimple\BACatalog를 찾습니다. 
6. Hello 카탈로그 XML 파일을 삭제 하 고 만든 hello 백업 버전으로 바꿉니다. 
7. Hello 데스크톱 StorSimple 스냅숏 관리자 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다. 

## <a name="next-steps"></a>다음 단계
* 에 대 한 자세한 내용은 [StorSimple 솔루션 tooadminister StorSimple 스냅숏 관리자를 사용 하 여](storsimple-snapshot-manager-admin.md)합니다.
* [StorSimple 스냅숏 관리자 작업 및 워크플로](storsimple-snapshot-manager-admin.md#storsimple-snapshot-manager-tasks-and-workflows)에 대해 자세히 알아봅니다.

