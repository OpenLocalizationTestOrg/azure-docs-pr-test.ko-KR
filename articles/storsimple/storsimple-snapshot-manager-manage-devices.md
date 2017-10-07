---
title: "StorSimple 스냅숏 관리자 aaaManage 장치 | Microsoft Docs"
description: "Toouse StorSimple 스냅숏 관리자 MMC 스냅인 tooconnect hello 하 고 StorSimple 장치를 관리 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 966ecbe3-a7fa-4752-825f-6694dd949946
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 7a2a2ca830e4ea6eb4b01f2542958df3871c1700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooconnect-and-manage-storsimple-devices"></a>StorSimple 스냅숏 관리자 tooconnect를 사용 하 고 StorSimple 장치를 관리 합니다.
## <a name="overview"></a>개요
Hello StorSimple 스냅숏 관리자에서에서 노드를 사용할 수 있습니다 **범위** 창 tooverify StorSimple 장치 데이터를 가져올 연결 된 저장소 장치를 새로 고칩니다. 또한 클릭할 때 hello **장치** 노드를 연결 된 장치 및 해당 상태 정보 hello의 목록을 볼 수 있습니다 **결과** 창.

![연결된 장치](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_connect_devices.png)

**그림 1: StorSimple 스냅숏 관리자 연결된 장치** 

에 따라 프로그램 **보기** 선택 항목, hello **결과** 창 hello 다음 각 장치에 대 한 정보를 표시 합니다. (너무 보기를 구성 하는 방법에 대 한 자세한 내용을 보려면 이동[보기 메뉴](storsimple-use-snapshot-manager.md#view-menu)합니다.

| 결과 열 | 설명 |
|:--- |:--- |
| 이름 |hello 장치 hello Azure 클래식 포털에에서 구성 된 대로 hello 이름 |
| 모델 |hello hello 장치 모델 번호 |
| 버전 |hello 장치에 설치 된 hello 소프트웨어 hello 버전 |
| 가동 상태 |Hello 장치를 사용할 수 있는지 여부 |
| 마지막 동기화 |날짜 및 시간 hello 장치에 마지막으로 동기화 |
| 일련 번호 |hello 장치에 대 한 hello 일련 번호 |

Hello를 마우스 오른쪽 단추로 클릭 하는 경우 **장치** hello에 대 한 노드 **범위** 창에서 작업을 수행 하는 hello에서 선택할 수 있습니다.

* 장치 추가 또는 교체
* 장치 연결 및 가져오기 확인
* 연결된 장치 새로 고침

Hello를 누르면 **장치** hello에 대 한 노드 마우스 오른쪽 단추로 장치 이름을 **결과** 창에서 작업을 수행 하는 hello에서 선택할 수 있습니다.

* 장치 인증
* 장치 세부 정보 보기
* 장치 새로 고침
* 장치 구성 삭제
* 장치 암호 변경

> [!NOTE]
> 이러한 모든 작업 에서도 제공 되 hello **동작** 창.


이 자습서에 설명 어떻게 toouse StorSimple 스냅숏 관리자 tooconnect 및 장치를 관리 하 고 hello 다음 작업을 수행 합니다.

* 장치 추가 또는 교체
* 장치 연결 및 가져오기 확인
* 연결된 장치 새로 고침
* 장치 인증
* 장치 세부 정보 보기
* 개별 장치 새로 고침
* 장치 구성 삭제
* 만료된 장치 암호 변경
* 실패한 장치 바꾸기

> [!NOTE]
> Hello StorSimple 스냅숏 관리자 인터페이스를 사용 하는 방법에 대 한 일반 정보에 대 한 이동 너무[StorSimple 스냅숏 관리자 사용자 인터페이스](storsimple-use-snapshot-manager.md)합니다.


## <a name="add-or-replace-a-device"></a>장치 추가 또는 교체
다음 프로시저 tooadd hello를 사용 하거나 StorSimple 장치를 교체 합니다.

#### <a name="tooadd-or-replace-a-device"></a>tooadd 또는 교체 장치
1. Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.
2. Hello에 **범위** 창에서 마우스 오른쪽 단추로 클릭 hello **장치** 노드를 차례로 클릭 한 다음 **장치 구성**합니다. hello **장치 구성** 대화 상자가 나타납니다.
   
    ![StorSimple 장치 구성](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_config_device.png) 
3. Hello에 **장치** 드롭다운 상자, hello 장치나 가상 장치로의 선택 hello IP 주소입니다. 
4. Hello에 **암호** 텍스트 상자, hello Azure 클래식 포털의에서 hello 장치에 대해 만든 형식 hello StorSimple 스냅숏 관리자 암호입니다. **확인**을 클릭합니다. StorSimple 스냅숏 관리자는 식별 된 hello 장치를 검색 합니다. 
   
   * Hello 장치 표시 되 면 StorSimple 스냅숏 관리자 연결을 추가 합니다.
   * 어떤 이유로 든 hello 장치를 사용할 수 없으면 StorSimple 스냅숏 관리자 오류 메시지를 반환 합니다. 클릭 **확인** tooclose hello 오류 메시지 및 클릭 **취소** tooclose hello **장치 구성** 대화 상자.

## <a name="connect-a-device-and-verify-imports"></a>장치 연결 및 가져오기 확인
프로시저 tooconnect StorSimple 장치를 다음 hello를 사용 하 고 연결 된 백업을 있는 모든 기존 볼륨 그룹을 가져오는지 확인 합니다.

#### <a name="tooconnect-a-device-and-verify-imports"></a>장치 tooconnect 고 가져오기를 확인 하려면
1. tooconnect 장치 tooStorSimple 스냅숏 관리자 추가의 hello 지침에 따라 또는 장치를 교체 합니다. 서버에 연결 tooa 장치 StorSimple 스냅숏 관리자 다음과 같이 응답 합니다.
   
   * 어떤 이유로 든 hello 장치를 사용할 수 없으면 StorSimple 스냅숏 관리자 오류 메시지를 반환 합니다. 
   
   * Hello 장치 표시 되 면 StorSimple 스냅숏 관리자 연결을 추가 합니다. Hello에 표시 하는 hello 장치를 선택 하면 **결과** 창의 hello 상태 필드에 해당 hello 장치가 표시 및 **사용 가능**합니다. StorSimple 스냅숏 관리자 hello 볼륨 그룹에 연결 된 백업을 있는 hello 장치에 대해 구성 된 모든 볼륨 그룹을 가져옵니다. 백업 정책은 가져오지 않습니다. 연결된 백업이 없는 볼륨 그룹은 가져오지 않습니다.
2. Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.
3. Hello에서 마우스 오른쪽 단추로 클릭 hello 최상위 노드 **범위** 창과 클릭 **가져오기 표시 토글**합니다.
   
    ![가져오기 표시 토글 선택](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Toggle_Imports_Display.png) 
4. hello **가져오기 표시 토글** 볼륨 그룹과 백업을 가져온 hello 상태 hello 보여 주는 대화 상자가 나타납니다. **확인**을 클릭합니다.

StorSimple 스냅숏 관리자 toomanage를 정당한 hello 볼륨 그룹 및 백업을 성공적으로 가져왔는지 후 사용할 수 있습니다 볼륨 그룹과 백업을 만들고 StorSimple 스냅숏 관리자를 구성 하는 관리 하는 경우 처럼 합니다. 

## <a name="refresh-connected-devices"></a>연결된 장치 새로 고침
다음 프로시저 toosynchronize hello 사용 하 여 hello StorSimple Snapshot Manager로 StorSimple 장치를 연결 했습니다.

#### <a name="toorefresh-connected-devices"></a>toorefresh 연결 된 장치
1. Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.
2. Hello에 **범위** 창에서 마우스 오른쪽 단추로 클릭 **장치**, 클릭 하 고 **장치 새로 고침**합니다. 이 동기화 hello 연결 된 장치 StorSimple 스냅숏 관리자를 사용 하 여 hello 볼륨 그룹과 백업을 최근에 추가한을 포함 하 여 볼 수 있도록 합니다. 
   
    ![Hello StorSimple 장치 새로 고침](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Refresh_devices.png)

hello **장치 새로 고침** 작업 연결 된 장치에서 모든 새 볼륨 그룹 및 연결 된 모든 백업을 검색 합니다. Hello와 달리 **볼륨 다시 검사** hello에 대 한 사용 가능한 동작 **볼륨** 노드를 **장치 새로 고침** hello 백업 레지스트리를 복원 하지 않습니다.

## <a name="authenticate-a-device"></a>장치 인증
다음 프로시저 tooauthenticate StorSimple 장치의 StorSimple 스냅숏 관리자 hello를 사용 합니다.

#### <a name="tooauthenticate-a-device"></a>tooauthenticate 장치
1. Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.
2. Hello에 **범위** 창에서 클릭 **장치**합니다.
3. Hello에 **결과** 창의 hello 장치의 hello 이름을 마우스 오른쪽 단추로 클릭 **Authenticate**합니다.
4. hello **Authenticate** 대화 상자가 나타납니다. Hello 장치 암호를 입력 한 다음 클릭 **확인**합니다.
   
    ![인증 대화 상자](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Authenticate.png) 

## <a name="view-device-details"></a>장치 세부 정보 보기
다음 프로시저 tooview hello 세부 정보는 StorSimple 장치의 hello를 사용 하 여 하 고 필요한 경우 hello 장치 StorSimple 스냅숏 관리자를 다시 동기화 합니다.

#### <a name="tooview-and-resynchronize-device-details"></a>tooview 여 다시 동기화 할 장치 세부 정보
1. Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.
2. Hello에 **범위** 창에서 클릭 **장치**합니다.
3. Hello에 **결과** 창의 hello 장치의 hello 이름을 마우스 오른쪽 단추로 클릭 **세부 정보**합니다.

4. hello **장치 세부 정보** 대화 상자가 나타납니다. 이 상자에 표시 hello 이름, 모델, 버전, 일련 번호, 상태, 대상 iSCSI 정규화 된 이름 (IQN) 마지막 동기화 날짜와 시간입니다.

* 클릭 **Resync** toosynchronize hello 장치입니다.
* 클릭 **확인** 또는 **취소** tooclose hello 대화 상자.
  
  ![장치 세부 정보](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Device_details.png) 

## <a name="refresh-an-individual-device"></a>개별 장치 새로 고침
다음 프로시저 tooresynchronize 개별 StorSimple 장치의 StorSimple 스냅숏 관리자 hello를 사용 합니다.

#### <a name="toorefresh-a-device"></a>toorefresh 장치
1. Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다. 
2. Hello에 **범위** 창에서 클릭 **장치**합니다. 
3. Hello에 **결과** 창의 hello 장치의 hello 이름을 마우스 오른쪽 단추로 클릭 **장치 새로 고침**합니다. Hello 장치를 StorSimple 스냅숏 관리자 동기화 설정.

## <a name="delete-a-device-configuration"></a>장치 구성 삭제
Hello 프로시저 toodelete 개별 StorSimple 장치 구성을 StorSimple 스냅숏 관리자에서 다음을 사용 합니다.

#### <a name="toodelete-a-device-configuration"></a>toodelete 장치 구성
1. Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.
2. Hello에 **범위** 창에서 클릭 **장치**합니다. 
3. Hello에 **결과** 창의 hello 장치의 hello 이름을 마우스 오른쪽 단추로 클릭 **삭제**합니다. 
4. hello 메시지의 뒤에 나타납니다. 클릭 **예** toodelete hello 구성 하거나 클릭 **아니요** toocancel hello 삭제 합니다.
   
    ![장치 구성 삭제](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_DeleteDevice.png)

## <a name="change-an-expired-device-password"></a>만료된 장치 암호 변경
암호 tooauthenticate StorSimple 장치의 StorSimple 스냅숏 관리자를 입력 해야 합니다. Hello 장치를 Windows PowerShell 인터페이스 tooset hello를 사용 하는 경우이 암호를 구성 합니다. 그러나 hello 암호 만료 될 수 있습니다. 이 경우에 hello Azure 클래식 포털 toochange hello 암호를 사용할 수 있습니다. 다음 hello 장치 hello 암호 만료 되기 전에 StorSimple 스냅숏 관리자 구성에 있으므로 hello StorSimple 스냅숏 관리자에서 장치를 다시 인증 해야 합니다.

#### <a name="toochange-hello-expired-password"></a>toochange hello 만료 된 암호
1. Azure 클래식 포털 hello hello StorSimple Manager 서비스를 시작 합니다.
2. 클릭 **장치** > **구성** hello 장치에 대 한 합니다.
3. StorSimple 스냅숏 관리자 섹션 toohello 아래로 스크롤하십시오. 14-15자로 암호를 입력합니다. 해당 hello 암호에 대문자, 소문자, 숫자 및 특수 문자의 조합을 포함 되어 있는지 확인 합니다.
4. Hello 암호 tooconfirm 재입력 것입니다.
5. 클릭 **저장** hello hello 페이지 맨 아래에 있습니다.

#### <a name="toore-authenticate-hello-device"></a>toore-hello 장치 인증
1. StorSimple 스냅숏 관리자를 시작합니다.
2. Hello에 **범위** 창에서 클릭 **장치**합니다. Hello에 구성 된 장치 목록을 표시 **결과** 창.
3. Hello 장치와 마우스 오른쪽 단추를 클릭 한 다음 선택 **Authenticate**합니다.
4. Hello에 **Authenticate** 창의 hello 새 암호를 입력 합니다.
5. Hello 장치, 마우스 선택 선택 **장치 새로 고침**합니다. Hello 장치를 StorSimple 스냅숏 관리자 동기화 설정.

## <a name="replace-a-failed-device"></a>실패한 장치 바꾸기
StorSimple 장치 실패 하 고이 경우 대기 (장애 조치) 장치를 사용 하 여 hello tooconnect 단계 다음으로 대체 toohello 새 장치 및 보기 hello 연결 된 백업입니다.

#### <a name="tooconnect-tooa-new-device-after-failover"></a>장애 조치 후 tooconnect tooa 새 장치
1. Hello iSCSI 연결 toohello 새 장치를 다시 구성 합니다. 자세한 내용은 이동 너무 "7 단계: 탑재, 초기화, 및 서식 볼륨"에서 [온-프레미스 StorSimple 장치 배포](storsimple-8000-deployment-walkthrough-u2.md)합니다.

> [!NOTE]
> StorSimple 장치를 새 hello 이전과 hello와 같은 IP 주소를 hello에, 수 tooconnect hello 이전 구성 수 있습니다.


1. Hello Microsoft StorSimple 관리 서비스를 중지 합니다.
   
   1. 서버 관리자를 시작합니다.
   2. Hello에 서버 관리자 대시보드 hello에 **도구** 메뉴 선택 **서비스**합니다.
   3. Hello에 **서비스** 창, 선택 hello **Microsoft StorSimple 관리 서비스**합니다.
   4. Hello에서 마우스 오른쪽 단추로 창 아래에서 **Microsoft StorSimple 관리 서비스**, 클릭 **hello 서비스 중지**합니다.
2. Hello 구성 정보 관련된 toohello 오래 된 장치를 제거 합니다.
   
   1. 파일 탐색기에서 tooC:\ProgramData\Microsoft\StorSimple\BACatalog를 찾습니다.
   2. Hello BACatalog 폴더의 hello 파일을 삭제 합니다.
3. Hello Microsoft StorSimple 관리 서비스를 다시 시작 합니다.
   
   1. Hello에 서버 관리자 대시보드 hello에 **도구** 메뉴 선택 **서비스**합니다.
   2. Hello에 **서비스** 창, 선택 hello **Microsoft StorSimple 관리 서비스**합니다.
   3. Hello에서 마우스 오른쪽 단추로 창 아래에서 **Microsoft StorSimple 관리 서비스**, 클릭 **hello 서비스를 다시 시작**합니다.
4. StorSimple 스냅숏 관리자를 시작합니다.
5. tooconfigure hello 새 StorSimple 장치 2 단계에서에서 단계를 완료 hello:에 StorSimple 장치를 연결할 [StorSimple 스냅숏 관리자 배포](storsimple-snapshot-manager-deployment.md)합니다.
6. 마우스 오른쪽 단추로 클릭 hello 최상위 노드를 hello **범위** 창 (StorSimple 스냅숏 관리자 hello 예제)을 마우스 클릭 한 다음 **가져오기 표시 토글**합니다. 
7. Hello 가져온 볼륨 그룹 및 백업을 StorSimple 스냅숏 관리자에 표시 되 면 메시지가 나타납니다. **확인**을 클릭합니다.

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[StorSimple 솔루션 tooadminister StorSimple 스냅숏 관리자를 사용 하 여](storsimple-snapshot-manager-admin.md)합니다.
* 너무 방법에 대해 알아봅니다[tooview StorSimple 스냅숏 관리자를 사용 하 고 볼륨 관리](storsimple-snapshot-manager-manage-volumes.md)합니다.

