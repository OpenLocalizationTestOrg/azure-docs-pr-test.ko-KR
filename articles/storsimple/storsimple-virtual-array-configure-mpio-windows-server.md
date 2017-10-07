---
title: "호스트에 MPIO aaaConfigure 연결 tooStorSimple 가상 배열 | Microsoft Docs"
description: "Tooconfigure 다중 경로 I/O (MPIO) StorSimple 가상 배열에 대 한 Windows Server 2012 r 2를 실행 하는 tooa 호스트를 연결 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5b7a7f99-ee5b-4b7d-ab32-483a5a1fa504
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/01/2017
ms.author: alkohli
ms.openlocfilehash: 0e6df23bba29395329685cbf2c968675abb04cfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multipath-io-on-windows-server-host-for-hello-storsimple-virtual-array"></a>StorSimple 가상 배열 hello에 대 한 Windows Server 호스트에서 다중 경로 I/O를 구성 합니다.
## <a name="overview"></a>개요
이 문서에 tooinstall 다중 경로 I/O 기능 (MPIO) Windows Server 호스트에 StorSimple 전용 볼륨에 대 한 특정 구성 설정을 적용 하 고 다음 StorSimple 볼륨에 대 한 MPIO를 확인 하는 방법에 대해 설명 합니다. hello 프로시저 1200 StorSimple 가상 배열 두 네트워크 인터페이스가 있는 두 개의 네트워크 인터페이스와 연결 된 tooa Windows Server 호스트 있다고 가정 합니다. 이 문서에 포함 된 hello 정보 toohello 가상 배열만을 적용 됩니다. StorSimple 8000 시리즈 장치에 대 한 내용은 이동 너무[StorSimple 호스트에 대 한 MPIO 구성](storsimple-configure-mpio-windows-server.md)합니다. 

Windows Server는 데 도움이 됩니다 빌드 내결함성 / 고가용성 저장소 구성의 hello MPIO 기능입니다. 중복 된 실제 경로 구성 요소를 사용 하는 MPIO-어댑터, 케이블 및 스위치-hello 서버와 hello 저장소 장치 사이 toocreate 논리 경로입니다. 구성 요소 오류가 있으면 발생 논리 경로 toofail 다중 경로 제어 논리는 사용 대체 경로 I/O에 대 한 응용 프로그램 데이터에 계속 액세스할 수 있도록 합니다. 또한 구성에 따라 MPIO도 성능을 향상 시킬 수 이러한 모든 경로에서 다시 hello 부하 균형을 조정 합니다. 자세한 내용은 [MPIO 개요](https://technet.microsoft.com/library/cc725907.aspx "MPIO 개요 and features")을 참조하세요.

고가용성에 대 한 hello StorSimple 솔루션의, Windows Server 호스트 연결 된 tooyour StorSimple 가상 배열 (모델 1200) hello에서 MPIO를 구성 합니다. 호스트 서버 hello 링크, 네트워크 또는 인터페이스 오류에 다음 허용할 수 있습니다. 

이러한 단계 tooconfigure MPIO toofollow이 필요 합니다. 

* 필수 구성 요소
* 1 단계: hello Windows Server 호스트에 MPIO 설치
* 2단계: StorSimple 볼륨에 대한 MPIO 구성
* 3 단계:에 StorSimple 볼륨 탑재 hello 호스트

각 단계는 hello hello 다음 섹션에서에서 설명 합니다.

## <a name="prerequisites"></a>필수 조건
이 섹션 hello Windows Server 호스트 및 가상 배열에 대 한 hello 구성 필수 구성 요소에 자세히 설명 합니다.

### <a name="on-windows-server-host"></a>Windows Server 호스트
* Windows Server 호스트에 사용 가능한 2개의 네트워크 인터페이스가 있는지 확인합니다.

### <a name="on-storsimple-virtual-array"></a>StorSimple 가상 배열에서
* hello 가상 배열 iSCSI 서버로 구성 되어야 합니다. toolearn 더 참조 [iSCSI 서버와 가상 배열 설정](storsimple-virtual-array-deploy3-iscsi-setup.md)합니다. Hello 배열에서 하나 이상의 네트워크 인터페이스를 사용할 수 있어야 합니다.   
* 가상 배열에서 네트워크 인터페이스 hello hello Windows Server 호스트에서 연결할 수 있어야 합니다.
* StorSimple 가상 배열에 하나 이상의 볼륨을 만들어야 합니다. toolearn 더 참조 [볼륨 추가](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume) StorSimple 가상 배열에 있습니다. 이 절차에서는 hello 가상 배열에 3 볼륨 (1 로컬로 고정 된 볼륨 및 2 계층화 된 볼륨에 표시 된 대로 아래) 생성 합니다.
  
    ![mpio0](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio0.png)

### <a name="hardware-configuration-for-storsimple-virtual-array"></a>StorSimple 가상 배열에 대한 하드웨어 구성
아래 hello 그림 고가용성에 대 한 hello 하드웨어 구성 및 Windows Server 호스트와이 절차에 사용 되는 StorSimple 가상 배열에 대 한 다중 경로 제어 부하 분산을 보여 줍니다.

![mpio 하드웨어 구성](./media/storsimple-virtual-array-configure-mpio-windows-server/1200hardwareconfig.png)

와 같이 앞 그림 hello:

* Hyper-V에 프로비전된 StorSimple 가상 배열은 iSCSI 서버로 구성된 단일 노드 활성 장치입니다.
* 배열에 두 개의 가상 네트워크 인터페이스가 활성화되었습니다. Hello 로컬 웹 UI 가상 배열에서 너무 이동 하 여 두 개의 네트워크 인터페이스를 사용할 수 있는지를 확인**네트워크 설정을** 아래와 같이:
  
    ![1200에 활성화된 네트워크 인터페이스](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio9.png)
  
    참고 hello IPv4 주소를 사용 하도록 설정 하는 hello 네트워크 인터페이스 (이더넷, 기본적으로 Ethernet 2)을 나중에 사용할 hello 호스트에 저장 합니다.
* Windows Server 호스트에 두 개의 네트워크 인터페이스가 활성화되었습니다. 호스트 및 배열에 대 한 연결 된 인터페이스에는 경우 hello 동일한 서브넷을 사용할 수 있는 네 개의 경로 다음 hello 합니다. 이이 절차에서는 대/소문자 hello 이었습니다. 그러나 hello 배열과 호스트 인터페이스의 각 네트워크 인터페이스에 있고 다른 IP 서브넷 (라우팅할 수 없음), 2 경로 사용할 수 됩니다 합니다.

## <a name="step-1-install-mpio-on-hello-windows-server-host"></a>1 단계: hello Windows Server 호스트에 MPIO 설치
MPIO는 Windows Server에서 선택적 기능이며 기본적으로 설치되지 않습니다. 서버 관리자를 통해 기능으로 설치해야 합니다. Windows Server 호스트에서이 기능을 완료 tooinstall 프로시저 다음 hello 합니다.

[!INCLUDE [storsimple-install-mpio-windows-server-host](../../includes/storsimple-install-mpio-windows-server-host.md)]

## <a name="step-2-configure-mpio-for-storsimple-volumes"></a>2단계: StorSimple 볼륨에 대한 MPIO 구성
MPIO 구성 toobe tooidentify StorSimple 볼륨 필요합니다. tooconfigure MPIO toorecognize StorSimple 볼륨 hello 다음 단계를 수행 합니다.

[!INCLUDE [storsimple-configure-mpio-volumes](../../includes/storsimple-configure-mpio-volumes.md)]

## <a name="step-3-mount-storsimple-volumes-on-hello-host"></a>3 단계:에 StorSimple 볼륨 탑재 hello 호스트
Windows 서버에서 MPIO를 구성한 후 hello StorSimple 배열에서 만들었으며 탑재할 수 있으며 그러면 중복성을 위해 MPIO 활용을 수행할 수 있습니다. 볼륨을 toomount hello 다음 단계를 수행 합니다.

#### <a name="toomount-volumes-on-hello-host"></a>hello 호스트에서 toomount 볼륨
1. 열기 hello **iSCSI 초기자 속성** hello Windows Server 호스트에는 창입니다. 너무 이동**서버 관리자 > 대시보드 > 도구 > iSCSI 초기자**합니다.
2. Hello에 **iSCSI 초기자 속성** 대화 상자를 클릭 **검색**, 클릭 하 고 **대상 포털 검색**합니다.
3. Hello에 **대상 포털 검색** 대화 상자에서 다음 hello지 않습니다.
   
    1. StorSimple 가상 배열에 지원 되는 네트워크 인터페이스를 첫 번째 hello hello IP 주소를 입력 합니다. 기본적으로 **이더넷**이 됩니다. 
    2. 클릭 **확인** tooreturn toohello **iSCSI 초기자 속성** 대화 상자.
     
    > [!IMPORTANT]
    > ISCSI 연결에 대 한 개인 네트워크를 사용 하는 연결 된 toohello 개인 네트워크 hello 데이터 포트의 hello IP 주소를 입력 합니다.
     
4. 배열의 두 번째 네트워크 인터페이스(예: 이더넷 2)에 대해 2~3단계를 반복합니다. 
5. 선택 hello **대상** hello 탭 **iSCSI 초기자 속성** 대화 상자. 가상 배열의 경우 각 볼륨 서피스가 **검색된 대상**아래에 대상으로 표시될 것입니다. 이 경우 3 개의 대상 (해당 toothree 볼륨)는 검색 됩니다.
   
    ![mpio1](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio1.png)
6. 클릭 **연결** tooestablish StorSimple 가상 배열와 iSCSI 세션입니다. A **tooTarget 연결** 대화 상자가 표시 됩니다. 선택 hello **다중 경로 사용** 확인란 합니다. **고급**을 클릭합니다.
   
    ![mpio2](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio2.png)
7. Hello에 **고급 설정** 대화 상자에서 다음 hello지 않습니다.                                        
   
    1. Hello에 **로컬 어댑터** 드롭 다운 목록 **Microsoft iSCSI 초기자**합니다.
    2. Hello에 **초기자 IP** 드롭 다운 목록, hello 호스트의 IP 주소 선택 hello 합니다.
    3. Hello에 **대상 포털** IP 드롭 다운 목록, 배열 인터페이스의 선택 hello IP입니다.
    4. 클릭 **확인** tooreturn toohello **iSCSI 초기자 속성** 대화 상자.
     
        ![mpio3](./media/storsimple-ova-configure-mpio-windows-server/mpio3.png)

8. **속성**을 클릭합니다. 
   
    ![mpio4](./media/storsimple-ova-configure-mpio-windows-server/mpio4.png)

9. Hello에 **속성** 대화 상자를 클릭 **세션 추가**합니다.
   
   ![mpio5](./media/storsimple-ova-configure-mpio-windows-server/mpio5.png)
10. Hello에 **tooTarget 연결** 대화 상자, 선택 hello **다중 경로 사용** 확인란 합니다. **고급**을 클릭합니다.
11. Hello에 **고급 설정** 대화 상자:                                        
    
    1. Hello에 **로컬 어댑터** 드롭 다운 목록에서 선택 Microsoft iSCSI 초기자입니다.

    2. Hello에 **초기자 IP** 드롭 다운 목록, 선택 hello IP 주소 해당 toohello 호스트 합니다. 이 경우에 hello 호스트에 hello 배열 tooa 단일 네트워크 인터페이스에서 두 개의 네트워크 인터페이스를 연결 합니다. 따라서이 인터페이스는 첫 번째 세션 hello에 대 한 제공 된 것과 동일한 안녕 합니다.

    3. Hello에 **대상 포털 IP** 드롭 다운 목록, hello hello 배열에서 사용할 수는 두 번째 데이터 인터페이스에 대 한 선택 hello IP 주소입니다.

    4. 클릭 **확인** tooreturn toohello iSCSI 초기자 속성 대화 상자. 두 번째 세션 toohello 대상을 추가 했습니다.
      
       ![mpio11](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio11.png)
    
    5. Hello에 원하는 hello 세션 (경로)를 추가한 후 **iSCSI 초기자 속성** 대화 상자, 선택 hello 대상 및 클릭 **속성**합니다. Hello 세션 탭의 hello **속성** 대화 상자, 참고 hello 4 개 세션 식별자는 toohello 가능한 경로 순열에 해당 합니다. 세션을 toocancel hello 확인란 다음 tooa 세션 식별자를 선택한 다음 클릭 **연결 끊기**합니다.

    6. 선택 hello 세션 내에서 제공 되는 tooview 장치 **장치** 탭 tooconfigure hello 선택한 장치에 대해 MPIO 정책을 클릭 **MPIO**합니다.

    7. hello **세부 정보** 대화 상자가 표시 됩니다. Hello에 **MPIO** 탭을 적절 한 hello를 선택할 수 있습니다 **부하 분산 정책** 설정 합니다. Hello를 볼 수도 있습니다 **활성** 또는 **대기** 경로 유형입니다.
12. Tooadd 추가 세션 (경로) toohello 대상 8-11 단계를 반복 합니다. Hello 호스트에 두 개의 인터페이스 및 hello 가상 배열에 2 개 사용 하 여 각 대상에 대 한 4 개 세션의 합계를 추가할 수 있습니다. 
    
    ![mpio14](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio14.png)
13. 각 볼륨 (화면을 대상으로 표시)에 대해 이러한 단계 toorepeat를 해야 합니다.
    
    ![mpio15](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio15.png)
14. 열기 **컴퓨터 관리** 너무 이동 하 여**서버 관리자 > 대시보드 > 컴퓨터 관리**합니다. Hello 왼쪽된 창에서 클릭 **저장소 > 디스크 관리**합니다. hello는 표시 toothis 호스트 hello StorSimple 가상 배열에서 만든 볼륨 아래에 표시 될 **디스크 관리** 새 디스크로 합니다.
15. Hello 디스크를 초기화 하 고 새 볼륨을 만듭니다. Hello 포맷 프로세스 동안 64kb 할당 단위 크기 (AUS)를 선택 합니다. Hello 사용 가능한 모든 볼륨에 대 한 hello 프로세스를 반복 합니다.
    
    ![디스크 관리](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio20.png)
16. **디스크 관리**를 마우스 오른쪽 단추로 클릭 hello **디스크** 선택 **속성**합니다.
17. Hello에 **다중 경로 디스크 장치 속성** 대화 상자를 클릭 hello **MPIO** 탭 합니다.
    
    ![디스크 속성](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio21.png)
18. Hello에 **DSM 이름** 섹션에서 클릭 **세부 정보** hello 매개 변수 toohello 기본 매개 변수를 설정 되어 있는지 확인 합니다. hello 기본 매개 변수는:
    
    * 경로 확인 기간 = 30
    * 재시도 횟수 = 3
    * PDO 제거 기간 = 20
    * 재시도 간격 = 1
    * 경로 확인 사용 = 선택하지 않음
    
    > [!NOTE]
    > **Hello 기본 매개 변수를 수정 하지 마십시오.**
   
## <a name="next-steps"></a>다음 단계
에 대 한 자세한 내용은 [StorSimple 장치 관리자 서비스 tooadminister StorSimple 가상 배열 hello를 사용 하 여](storsimple-virtual-array-manager-service-administration.md)합니다.

