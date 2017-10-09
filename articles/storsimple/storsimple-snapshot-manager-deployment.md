---
title: "StorSimple 스냅숏 관리자 aaaDeploy | Microsoft Docs"
description: "설치 하 고 toodownload hello StorSimple 스냅숏 관리자는 MMC 스냅인 StorSimple 데이터 보호 및 백업 기능을 관리 하기 위한 방법에 대해 알아봅니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: f0128f57-519e-49ec-9187-23575809cdbe
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: dd90cca2bbb3410bb8cd459fb1a3ff3fb5f2997b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-snapshot-manager-mmc-snap-in"></a>StorSimple 스냅숏 관리자 MMC 스냅인 hello 배포

## <a name="overview"></a>개요
StorSimple 스냅숏 관리자 hello 데이터 보호 및 Microsoft Azure StorSimple 환경에서 백업 관리를 간소화 하는 Microsoft 관리 콘솔 (MMC) 스냅인입니다. StorSimple 스냅숏 관리자를 사용하면 완전히 통합된 저장소 시스템인 것처럼 Microsoft Azure StorSimple 온-프레미스 및 클라우드 저장소를 관리할 수 있으므로 백업 및 복원 프로세스가 간소화되고 비용이 절감됩니다. 

이 자습서에서는 StorSimple 스냅숏 관리자 설치, 제거 및 업그레이드에 대한 절차와 더불어 구성 요구 사항도 설명합니다.

> [!NOTE]
> * StorSimple 스냅숏 관리자 toomanage Microsoft Azure StorSimple 가상 배열 (라고도 StorSimple 온-프레미스 가상 장치)를 사용할 수 없습니다.
> * StorSimple 장치에서 tooinstall StorSimple 업데이트 2를 계획할 수 있는지 toodownload hello 최신 버전의 StorSimple 스냅숏 관리자를 설치 **StorSimple 업데이트 2를 설치 하기 전에**합니다. hello 최신 버전의 StorSimple 스냅숏 관리자가 이전 버전과 호환 하며 모든 릴리스된 버전의 Microsoft Azure StorSimple과 작동 합니다. Tooupdate 할 hello 이전 버전의 StorSimple 스냅숏 관리자를 사용 하는 경우 it (않아도 toouninstall hello 이전 버전 hello 새 버전을 설치 하기 전에).


## <a name="storsimple-snapshot-manager-installation"></a>StorSimple 스냅숏 관리자 설치
StorSimple 스냅숏 관리자 hello Windows Server 2008 R2 SP1, Windows Server 2012 또는 Windows Server 2012 R2 운영 체제를 실행 하는 컴퓨터에 설치할 수 있습니다. Windows 2008 R2를 실행하는 서버에는 Windows Server 2008 SP1 및 Windows Management Framework 3.0도 설치해야 합니다.

를 설치 하거나 hello StorSimple 스냅숏 관리자 스냅인 콘솔 MMC (Microsoft Management) hello에 대 한 업그레이드 전에 호스트 서버가 제대로 구성 및 해당 hello Microsoft Azure StorSimple 장치를 확인 합니다.

## <a name="configure-prerequisites"></a>필수 조건 구성
hello 다음 단계를 제공 구성 작업에 대 한 고급 개요 hello StorSimple 스냅숏 관리자를 설치 하기 전에 완료 해야 합니다. 시스템 요구 사항 및 단계별 지침을 포함한 전체 Microsoft Azure StorSimple 구성 및 설치 정보는 [온-프레미스 StorSimple 장치 배포](storsimple-8000-deployment-walkthrough-u2.md)를 참조하세요.

> [!IMPORTANT]
> 시작 하기 전에 검토 hello [배포 구성 검사 목록](storsimple-8000-deployment-walkthrough-u2.md#deployment-configuration-checklist) 및 및 [배포 필수 구성 요소](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites) 에 [온-프레미스 StorSimple 장치 배포](storsimple-8000-deployment-walkthrough-u2.md)합니다.
> <br>
> 
> 

### <a name="before-you-install-storsimple-snapshot-manager"></a>StorSimple 스냅숏 관리자를 설치하기 전에
1. 압축 풀기 탑재 하 고에 설명 된 대로 hello Microsoft Azure StorSimple 장치를 연결 [StorSimple 8100 장치 설치](storsimple-8100-hardware-installation.md) 또는 [8600 StorSimple 장치 설치](storsimple-8600-hardware-installation.md)합니다.
2. 호스트 컴퓨터 hello 다음 운영 체제 중 하나를 실행 중인 있는지 확인 합니다.
   
   * Windows Server 2008 R2(Windows 2008 R2를 실행하는 서버에는 Windows Server 2008 SP1 및 Windows Management Framework 3.0도 설치해야 합니다.)
   * Windows Server 2012
   * Windows Server 2012 R2
     
     StorSimple 가상 장치에 대 한 hello 호스트에는 Microsoft Azure 가상 컴퓨터 여야 합니다.
3. 모든 hello Microsoft Azure StorSimple 구성 요구 사항을 충족 하는지 확인 합니다. 자세한 내용은 이동 너무[배포 필수 구성 요소](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites)합니다.
4. Hello 장치 toohello 호스트를 연결 하 고 hello 초기 구성을 수행 합니다. 자세한 내용은 이동 너무[배포 단계](storsimple-8000-deployment-walkthrough-u2.md#deployment-steps)합니다.
5. Hello 장치에 볼륨 만들기, toohello 호스트를 할당 하 고 해당 hello 호스트가 탑재 하 고 사용할 수를 확인 합니다. StorSimple 스냅숏 관리자 볼륨 유형만 hello를 지원 합니다.
   
   * 기본 볼륨
   * 단순 볼륨
   * 동적 볼륨
   * 미러된 동적 볼륨(RAID 1)
   * 클러스터 공유 볼륨
     
     너무 hello StorSimple 장치 또는 StorSimple 가상 장치에서 볼륨을 만드는 방법에 대 한 정보를 보려면, 이동[6 단계: 볼륨 만들기](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume)에 [온-프레미스 StorSimple 장치 배포](storsimple-8000-deployment-walkthrough-u2.md)합니다.

## <a name="install-a-new-storsimple-snapshot-manager"></a>새 StorSimple 스냅숏 관리자 설치
StorSimple 스냅숏 관리자를 설치 하기 전에 확인 된 hello StorSimple 장치 또는 StorSimple 가상 장치에 만든 hello 볼륨 탑재, 초기화, 이며에 설명 된 대로 형식이 지정 [필수 구성 요소 구성](#configure-prerequisites)합니다.

> [!IMPORTANT]
> * StorSimple 가상 장치에 대 한 hello 호스트에는 Microsoft Azure 가상 컴퓨터 여야 합니다. 
> * Windows 2008 R2, Windows Server 2012 또는 Windows Server 2012 R2 hello 호스트를 실행 합니다. 서버에서 Windows Server 2008 R2를 실행하는 경우에는 Windows Server 2008 SP1 및 Windows Management Framework 3.0도 설치해야 합니다.
> * Hello 장치 tooStorSimple 스냅숏 관리자 연결 하기 전에 hello 호스트 toohello StorSimple 장치에서 iSCSI 연결을 구성 해야 합니다.

이러한 단계 toocomplete StorSimple 스냅숏 관리자의 새로 설치를 수행 합니다. 업그레이드를 설치 하는 경우 너무 이동[업그레이드 StorSimple 스냅숏 관리자를 다시 설치 하거나](#upgrade-or-reinstall-storsimple-snapshot-manager)합니다.

* 1단계: StorSimple 스냅숏 관리자 설치 
* 2 단계: tooa StorSimple 스냅숏 관리자 장치 연결 
* 3 단계: hello 연결 toohello 장치를 확인 합니다. 

### <a name="step-1-install-storsimple-snapshot-manager"></a>1단계: StorSimple 스냅숏 관리자 설치
다음 단계 tooinstall StorSimple 스냅숏 관리자 hello를 사용 합니다.

#### <a name="tooinstall-storsimple-snapshot-manager"></a>StorSimple 스냅숏 관리자 tooinstall
1. Hello StorSimple 스냅숏 관리자 소프트웨어 다운로드 (너무 이동[StorSimple 스냅숏 관리자](https://www.microsoft.com/download/details.aspx?id=44220) hello Microsoft 다운로드 센터에서에서) hello 호스트에 로컬로 저장 합니다.
2. 파일 탐색기에서 폴더를 압축된 하는 hello를 마우스 오른쪽 단추로 클릭 하 고 클릭 **압축 풀기**합니다.
3. Hello에 **압축 (Zip) 폴더 풀기** 창의 hello **대상을 선택 하 고 파일 압축 풀기** 입력란에 입력 하거나 찾아보기 toofile toobe 추출 하려는 toohello 경로입니다.
   
    > [!IMPORTANT]
    > StorSimple 스냅숏 관리자 hello c: 드라이브에 설치 해야 합니다.
    
4. 선택 hello **완료 되 면 파일 압축을 푼 표시** 확인란을 선택한 다음 클릭 **추출**합니다.
   
    ![파일 추출 대화 상자](./media/storsimple-snapshot-manager-deployment/HCS_SSM_extract_files.png) 
5. Hello 추출 완료 되 면 hello 대상 폴더가 열립니다. Hello hello 대상 폴더에 표시 되는 응용 프로그램 설치 아이콘을 두 번 클릭 합니다.
6. Hello 때 **설치 완료** 메시지가 표시 되 면 클릭 **닫기**합니다. StorSimple 스냅숏 관리자 아이콘 hello 바탕 화면에 표시 됩니다.
   
    ![바탕 화면 아이콘](./media/storsimple-snapshot-manager-deployment/HCS_SSM_desktop_icon.png) 

### <a name="step-2-connect-storsimple-snapshot-manager-tooa-device"></a>2 단계: tooa StorSimple 스냅숏 관리자 장치 연결
다음 단계 tooconnect StorSimple 스냅숏 관리자 tooa StorSimple 장치 hello를 사용 합니다.

#### <a name="tooconnect-storsimple-snapshot-manager-tooa-device"></a>StorSimple 스냅숏 관리자 tooa 장치 tooconnect
1. 바탕 화면에 hello StorSimple 스냅숏 관리자 아이콘을 클릭 합니다. hello StorSimple 스냅숏 관리자 창이 나타납니다. hello 창에는 **범위** 창은 **결과** 창 및 **동작** 창. 
   
    ![StorSimple 스냅숏 관리자 사용자 인터페이스](./media/storsimple-snapshot-manager-deployment/HCS_SSM_gui_panes.png)
   
   * hello **범위** 창 (왼쪽된 창의 hello)를 트리 구조로 구성 된 노드 목록이 포함 되어 있습니다. 일부 노드 tooselect 뷰 또는 특정 데이터 관련된 toothat 노드를 확장할 수 있습니다. Hello 화살표 아이콘 tooexpand 클릭 하거나 노드를 축소 합니다. Hello에 있는 항목을 마우스 오른쪽 단추로 클릭 **범위** 창 toosee 해당 항목에 대 한 사용 가능한 작업 목록입니다.
   * hello **결과** hello 노드, 뷰 또는 hello에서 선택한 데이터에 대 한 자세한 상태 정보를 포함 하는 창 (가운데 창 hello) **범위** 창.
   * hello **동작** hello 노드, 뷰 또는 hello에서 선택한 데이터에서 수행할 수 있는 hello 작업을 표시 하는 창 **범위** 창.
     
     에 대 한 전체 설명은 hello StorSimple 스냅숏 관리자 사용자 인터페이스를 참조 하세요. [StorSimple 스냅숏 관리자 사용자 인터페이스](storsimple-use-snapshot-manager.md)합니다.
2. Hello에 **범위** 창에서 마우스 오른쪽 단추로 클릭 hello **장치** 노드를 차례로 클릭 한 다음 **장치 구성**합니다. hello **장치 구성** 대화 상자가 나타납니다.
   
    ![장치 구성](./media/storsimple-snapshot-manager-deployment/HCS_SSM_config_device.png) 
3. Hello에 **장치** 상자, 선택 hello hello Microsoft Azure StorSimple 장치 또는 가상 장치 IP 주소를 나열 합니다. Hello에 **암호** 텍스트 상자, hello Azure 포털의에서 hello 장치에 대해 만든 형식 hello StorSimple 스냅숏 관리자 암호입니다. **확인**을 클릭합니다.
4. StorSimple 스냅숏 관리자는 식별 된 hello 장치를 검색 합니다. Hello 장치 표시 되 면 StorSimple 스냅숏 관리자 연결을 추가 합니다. 할 수 있습니다 [hello 연결 toohello 장치 확인](#to-verify-the-connection) 연결 hello tooconfirm 성공적으로 추가 합니다.
   
    어떤 이유로 든 hello 장치를 사용할 수 없으면 StorSimple 스냅숏 관리자 오류 메시지를 반환 합니다. 클릭 **확인** tooclose hello 오류 메시지 및 클릭 **취소** tooclose hello **장치 구성** 대화 상자.
5. 서버에 연결 tooa 장치 StorSimple 스냅숏 관리자 hello 볼륨 그룹에 연결 된 백업이 있는 해당 장치에 대해 구성 된 각 볼륨 그룹을 가져옵니다. 연결된 백업이 없는 볼륨 그룹은 가져오지 않습니다. 또한 볼륨 그룹에 대해 만든 백업 정책도 가져오지 않습니다. toosee 가져온된 그룹 hello 마우스 오른쪽 단추로 hello 최상위 **볼륨 그룹** hello에 대 한 노드 **범위** 클릭 **가져온된 그룹을 설정/해제**합니다.

### <a name="step-3-verify-hello-connection-toohello-device"></a>3 단계: hello 연결 toohello 장치를 확인 합니다.
StorSimple 스냅숏 관리자 연결된 toohello StorSimple 장치 인지 단계 tooverify 다음 hello를 사용 합니다.

#### <a name="tooverify-hello-connection"></a>tooverify hello 연결
1. Hello에 **범위** 창의 hello 클릭 **장치** 노드.
   
    ![StorSimple 스냅숏 관리자 장치 상태](./media/storsimple-snapshot-manager-deployment/HCS_SSM_Device_status.png) 
2. Hello 확인 **결과** 창: 
   
   * Hello 장치 아이콘에 녹색 표시기가 표시 되 고 **사용 가능** hello에 나타납니다 **상태** 열에서 다음 hello 장치가 연결 되어 있습니다. 
   * Hello 장치 아이콘에 빨간색 표시기를 표시 하 고 hello에 사용할 수 없음 표시 **상태** 열에서 다음 hello 장치에 연결 되어 있지 않습니다. 
   * 경우 **고치** hello에 표시 **상태** 열에 있으면 StorSimple 스냅숏 관리자를 검색 하 고 볼륨 그룹 및 연결된 된 장치에 대 한 연결 된 백업입니다.

## <a name="upgrade-or-reinstall-storsimple-snapshot-manager"></a>StorSimple 스냅숏 관리자 업그레이드 또는 다시 설치
Hello 소프트웨어를 다시 설치 하거나 업그레이드 하기 전에 StorSimple 스냅숏 관리자를 완전히 제거 해야 합니다. 

StorSimple 스냅숏 관리자를 다시 설치 하기 전에 hello hello 호스트 컴퓨터에서 기존 StorSimple 스냅숏 관리자 데이터베이스를 백업 합니다. 이 백업에서이 데이터를 쉽게 복원할 수 있도록 hello 백업 정책 및 구성 정보를 저장 합니다.

StorSimple 스냅숏 관리자를 업그레이드하거나 다시 설치하는 경우 다음 단계를 따르세요.

* 1단계: StorSimple 스냅숏 관리자 제거 
* 2 단계: hello StorSimple 스냅숏 관리자 데이터베이스를 백업 합니다. 
* StorSimple 스냅숏 관리자를 다시 설치 하 고 hello 데이터베이스를 복원 하는 3 단계: 

### <a name="step-1-uninstall-storsimple-snapshot-manager"></a>1단계: StorSimple 스냅숏 관리자 제거
다음 단계 toouninstall StorSimple 스냅숏 관리자 hello를 사용 합니다.

#### <a name="toouninstall-storsimple-snapshot-manager"></a>StorSimple 스냅숏 관리자 toouninstall
1. Hello 호스트 컴퓨터에서 열고 hello **제어판**, 클릭 **프로그램**, 클릭 하 고 **프로그램 및 기능**합니다.
2. Hello 왼쪽된 창에서 클릭 **제거 또는 변경 프로그램**합니다.
3. **StorSimple Snapshot Manager**를 마우스 오른쪽 단추로 클릭하고 **제거**를 클릭합니다.
4. Hello StorSimple 스냅숏 관리자 설치 프로그램을 시작 합니다. **설치 수정**을 클릭하고 **제거**를 클릭합니다.
   
   > [!NOTE]
   > MMC 프로세스가 hello 백그라운드에서 실행 되는, StorSimple 스냅숏 관리자 또는 디스크 관리와 같은 hello 제거 실패 하 고 메시지 tooclose 받습니다 하기 전에 MMC의 모든 인스턴스 toouninstall hello 프로그램을 시도 합니다. 선택 **자동으로 응용 프로그램을 닫고 설치를 한 후에 완료 toorestart**, 클릭 하 고 **확인**합니다.
   > 
   > 
5. Hello 제거 프로세스가 완료 되 면 한 **설치 완료** 메시지가 나타납니다. **닫기**를 클릭합니다.

### <a name="step-2-back-up-hello-storsimple-snapshot-manager-database"></a>2 단계: hello StorSimple 스냅숏 관리자 데이터베이스를 백업 합니다.
다음 단계 toocreate hello를 사용 하 고 hello StorSimple 스냅숏 관리자 데이터베이스의 복사본을 저장 합니다.

#### <a name="tooback-up-hello-database"></a>tooback hello 데이터베이스를
1. Hello Microsoft StorSimple 관리 서비스를 중지 합니다.
   
   1. 서버 관리자를 시작합니다.
   2. Hello에 서버 관리자 대시보드 hello에 **도구** 메뉴 선택 **서비스**합니다.
   3. Hello에 **서비스** 페이지에서 **Microsoft StorSimple 관리 서비스**합니다.
   4. Hello에서 마우스 오른쪽 단추로 창 아래에서 **Microsoft StorSimple 관리 서비스**, 클릭 **hello 서비스 중지**합니다.
      
        ![Hello StorSimple 장치 관리자 서비스 중지](./media/storsimple-snapshot-manager-deployment/HCS_SSM_stop_service.png)
2. TooC:\ProgramData\Microsoft\StorSimple\BACatalog를 찾습니다. 
   
   > [!NOTE]
   > ProgramData는 숨겨진 폴더입니다.
  
3. Hello 클라우드 또는 안전한 장소에 hello 카탈로그 XML 파일, 복사 hello 파일 및 저장소 hello 복사본을 찾습니다.
   
    ![StorSimple 백업 카탈로그 파일](./media/storsimple-snapshot-manager-deployment/HCS_SSM_bacatalog.png)
4. Hello Microsoft StorSimple 관리 서비스를 다시 시작 합니다. 
   
   1. Hello에 서버 관리자 대시보드 hello에 **도구** 메뉴 선택 **서비스**합니다.
   2. Hello에 **서비스** 페이지, 선택 hello **Microsoft StorSimple 관리 알림**e입니다.
   3. Hello에서 마우스 오른쪽 단추로 창 아래에서 **Microsoft StorSimple 관리 서비스**, 클릭 **hello 서비스를 다시 시작**합니다. 

### <a name="step-3-reinstall-storsimple-snapshot-manager-and-restore-hello-database"></a>StorSimple 스냅숏 관리자를 다시 설치 하 고 hello 데이터베이스를 복원 하는 3 단계:
StorSimple 스냅숏 관리자 tooreinstall hello 단계에 따라 [새 StorSimple 스냅숏 관리자 설치](#install-a-new-storsimple-snapshot-manager)합니다. 그런 다음 프로시저 toorestore hello StorSimple 스냅숏 관리자 데이터베이스에 따라 hello를 사용 합니다.

#### <a name="toorestore-hello-database"></a>toorestore hello 데이터베이스
1. Hello Microsoft StorSimple 관리 서비스를 중지 합니다.
   
   1. 서버 관리자를 시작합니다.
   2. Hello에 서버 관리자 대시보드 hello에 **도구** 메뉴 선택 **서비스**합니다.
   3. Hello에 **서비스** 페이지에서 **Microsoft StorSimple 관리 서비스**합니다.
   4. Hello에서 마우스 오른쪽 단추로 창 아래에서 **Microsoft StorSimple 관리 서비스**, 클릭 **hello 서비스 중지**합니다.
2. TooC:\ProgramData\Microsoft\StorSimple\BACatalog를 찾습니다.
   
   > [!NOTE]
   > ProgramData는 숨겨진 폴더입니다.
   > 
   > 
3. Hello 카탈로그 XML 파일을 삭제 하 고 이전에 저장 된 hello 버전으로 바꾸십시오.
4. Hello Microsoft StorSimple 관리 서비스를 다시 시작 합니다. 
   
   1. Hello에 서버 관리자 대시보드 hello에 **도구** 메뉴 선택 **서비스**합니다.
   2. Hello에 **서비스** 페이지에서 **Microsoft StorSimple 관리 서비스**합니다.
   3. Hello에서 마우스 오른쪽 단추로 창 아래에서 **Microsoft StorSimple 관리 서비스**, 클릭 **hello 서비스를 다시 시작**합니다.

## <a name="next-steps"></a>다음 단계
* toolearn 더에 대 한 StorSimple 스냅숏 관리자를 너무 이동[StorSimple 스냅숏 관리자 란?](storsimple-what-is-snapshot-manager.md)합니다.
* hello StorSimple 스냅숏 관리자 사용자 인터페이스에 대해 자세히 toolearn 너무 이동[StorSimple 스냅숏 관리자 사용자 인터페이스](storsimple-use-snapshot-manager.md)합니다.
* StorSimple 스냅숏 관리자 사용에 대 한 더 toolearn 너무 이동[StorSimple 스냅숏 관리자를 사용 하 여 tooadminister StorSimple 솔루션](storsimple-snapshot-manager-admin.md)합니다.

