---
title: "StorSimple 장치에 대 한 MPIO aaaConfigure | Microsoft Docs"
description: "StorSimple 장치에 대 한 다중 경로 I/O (MPIO) tooconfigure Windows Server 2012 r 2를 실행 하는 tooa 호스트를 연결 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 879fd0f9-c763-4fa0-a5ba-f589a825b2df
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/03/2017
ms.author: alkohli
ms.openlocfilehash: 08cd53039b3868217c7d28e97d7c3c695c06e399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multipath-io-for-your-storsimple-device"></a>StorSimple 장치에 대한 다중 경로 I/O 구성
Microsoft Windows Server toohelp의 hello 다중 경로 I/O (MPIO) 기능에 대 한 지원 작성 된 항상 사용 가능, 내결함성 / SAN 구성 빌드합니다. 중복 된 실제 경로 구성 요소를 사용 하는 MPIO-어댑터, 케이블 및 스위치-hello 서버와 hello 저장소 장치 사이 toocreate 논리 경로입니다. 구성 요소 오류가 있으면 발생 논리 경로 toofail 다중 경로 제어 논리는 사용 대체 경로 I/O에 대 한 응용 프로그램 데이터에 계속 액세스할 수 있도록 합니다. 또한 구성에 따라 MPIO도 성능을 향상 시킬 수 이러한 모든 경로에서 다시 hello 부하 균형을 조정 합니다. 자세한 내용은 [MPIO 개요](https://technet.microsoft.com/library/cc725907.aspx "MPIO 개요 and features")을 참조하세요.  

고가용성에 대 한 hello StorSimple 솔루션의, StorSimple 장치에서 MPIO는 구성 합니다. MPIO Windows Server 2012 r 2를 실행 하는 호스트 서버에 설치 되 면 링크, 네트워크 또는 인터페이스 오류 hello 서버 다음 허용할 수 있습니다. 

MPIO는 Windows Server에서 선택적 기능이며 기본적으로 설치되지 않습니다. 서버 관리자를 통해 기능으로 설치해야 합니다. 이 항목에서는 tooinstall를 수행 하 고 Windows Server 2012 r 2와 연결 된 tooa StorSimple 물리적 장치를 실행 하는 호스트에 hello MPIO 기능을 사용 해야 hello 단계를 설명 합니다.

> [!NOTE]
> **이 절차는 StorSimple 8000 시리즈에만 적용됩니다. MPIO는 현재 StorSimple 가상 장치에서 지원되지 않습니다.**
> 
> 

StorSimple 장치에서 이러한 단계 tooconfigure MPIO toofollow이 필요 합니다.

* 1 단계: hello Windows Server 호스트에 MPIO 설치
* 2단계: StorSimple 볼륨에 대한 MPIO 구성
* 3 단계:에 StorSimple 볼륨 탑재 hello 호스트
* 4단계: 고가용성 및 부하 분산을 위해 MPIO 구성

각 단계는 hello hello 다음 섹션에서에서 설명 합니다.

## <a name="step-1-install-mpio-on-hello-windows-server-host"></a>1 단계: hello Windows Server 호스트에 MPIO 설치
Windows Server 호스트에서이 기능을 완료 tooinstall 프로시저 다음 hello 합니다.

#### <a name="tooinstall-mpio-on-hello-host"></a>hello 호스트에 MPIO tooinstall
1. Windows Server 호스트에서 서버 관리자를 엽니다. 기본적으로 서버 관리자 hello Administrators 그룹의 멤버인 Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 tooa 컴퓨터 로그온 할 때 시작 됩니다. 서버 관리자 hello 열려 있지 않으면 클릭 **시작 > 서버 관리자**합니다.
   ![서버 관리자](./media/storsimple-configure-mpio-windows-server/IC740997.png)
2. **서버 관리자 > 대시보드 > 역할 및 기능 추가**를 클릭합니다. 그러면 시작 hello **역할 및 기능 추가** 마법사.
   ![역할 및 기능 추가 마법사 1](./media/storsimple-configure-mpio-windows-server/IC740998.png)
3. Hello에 **역할 및 기능 추가** 마법사에서 다음 hello지 않습니다.
   
   * Hello에 **시작 하기 전에** 페이지 **다음**합니다.
   * Hello에 **설치 유형 선택** 페이지에서의 hello 기본 설정을 그대로 적용 **역할 기반 또는 기능 기반** 설치 합니다. **다음**를 참조하세요.![역할 및 기능 추가 마법사 2](./media/storsimple-configure-mpio-windows-server/IC740999.png)
   * Hello에 **대상 서버 선택** 페이지에서 선택 **hello 서버 풀에서 서버 선택**합니다. 호스트 서버가 자동으로 검색됩니다. **다음**을 누릅니다.
   * Hello에 **서버 역할 선택** 페이지 **다음**합니다.
   * Hello에 **기능 선택** 페이지 **다중 경로 I/O**를 클릭 하 고 **다음**.![ 역할 및 기능 추가 마법사 5](./media/storsimple-configure-mpio-windows-server/IC741000.png)
   * Hello에 **설치 선택 확인** 페이지 hello 선택 영역을 확인 한 다음 선택 **필요한 경우 자동으로 hello 대상 서버 다시 시작**다음과 같이 합니다. **설치**를 클릭합니다.![역할 및 기능 추가 마법사 8](./media/storsimple-configure-mpio-windows-server/IC741001.png)
   * Hello 설치가 완료 되 면 알림이 표시 됩니다. 클릭 **닫기** tooclose hello 마법사.![ 역할 및 기능 추가 마법사 9](./media/storsimple-configure-mpio-windows-server/IC741002.png)

## <a name="step-2-configure-mpio-for-storsimple-volumes"></a>2단계: StorSimple 볼륨에 대한 MPIO 구성
MPIO 구성 toobe tooidentify StorSimple 볼륨 필요합니다. tooconfigure MPIO toorecognize StorSimple 볼륨 hello 다음 단계를 수행 합니다.

#### <a name="tooconfigure-mpio-for-storsimple-volumes"></a>StorSimple 볼륨에 대 한 MPIO tooconfigure
1. 열기 hello **MPIO 구성**합니다. **서버 관리자 > 대시보드 > 도구 > MPIO**를 클릭합니다.
2. Hello에 **MPIO 속성** 대화 상자, 선택 hello **다중 경로 찾기** 탭 합니다.
3. **iSCSI 장치에 대한 지원 추가**를 선택한 다음 **추가**를 클릭합니다.  
   ![MPIO 속성 다중 경로 검색](./media/storsimple-configure-mpio-windows-server/IC741003.png)
4. 메시지가 표시 되 면 hello 서버를 다시 부팅 합니다.
5. Hello에 **MPIO 속성** 대화 상자를 클릭 hello **MPIO 장치** 탭 합니다. 클릭 **추가**합니다.
    </br>![MPIO 속성 MPIO 장치](./media/storsimple-configure-mpio-windows-server/IC741004.png)
6. Hello에 **MPIO 지원 추가** 대화 상자의 **장치 하드웨어 ID**, 장치 일련 번호를 입력 합니다. StorSimple Manager 서비스에 액세스 하 여 너무 탐색 hello 장치 일련 번호를 가져올 수 있습니다**장치 > 대시보드**합니다. hello 장치 일련 번호 hello 오른쪽에 표시 됩니다 **빠른 보기** hello 장치 대시보드에서의 창.
    </br>![MPIO 지원 추가](./media/storsimple-configure-mpio-windows-server/IC741005.png)
7. 메시지가 표시 되 면 hello 서버를 다시 부팅 합니다.

## <a name="step-3-mount-storsimple-volumes-on-hello-host"></a>3 단계:에 StorSimple 볼륨 탑재 hello 호스트
Windows 서버에서 MPIO를 구성한 후 hello StorSimple 장치에서 만들었으며 탑재할 수 있으며 그러면 중복성을 위해 MPIO 활용을 수행할 수 있습니다. 볼륨을 toomount hello 다음 단계를 수행 합니다.

#### <a name="toomount-volumes-on-hello-host"></a>hello 호스트에서 toomount 볼륨
1. 열기 hello **iSCSI 초기자 속성** hello Windows Server 호스트에는 창입니다. **서버 관리자 > 대시보드 > 도구 > iSCSI 초기자**를 클릭합니다.
2. Hello에 **iSCSI 초기자 속성** 대화 상자에서 hello 검색 탭을 클릭 한 다음 클릭 **대상 포털 검색**합니다.
3. Hello에 **대상 포털 검색** 대화 상자에서 다음 hello지 않습니다.
   
   * Hello StorSimple 장치의 데이터 포트의 hello IP 주소를 입력 하십시오 (예를 들어 DATA 0 입력).
   * 클릭 **확인** tooreturn toohello **iSCSI 초기자 속성** 대화 상자.
     
     > [!IMPORTANT]
     > **ISCSI 연결에 대 한 개인 네트워크를 사용 하는 연결 된 toohello 개인 네트워크 hello 데이터 포트의 hello IP 주소를 입력 합니다.**
     > 
     > 
4. 장치에서 두 번째 네트워크 인터페이스(예: 데이터 1)에 대해 2~3단계를 반복합니다. ISCSI에 대해 이러한 인터페이스를 사용해야 합니다. 이 참조 하는 방법에 대 한 자세한 toolearn [네트워크 인터페이스 수정](storsimple-modify-device-config.md#modify-network-interfaces)합니다.
5. 선택 hello **대상** hello 탭 **iSCSI 초기자 속성** 대화 상자. 표시 되어야 hello StorSimple 장치 대상 IQN 아래 **검색 된 대상**합니다.

   ![iSCSI 초기자 속성 대상 탭](./media/storsimple-configure-mpio-windows-server/IC741007.png)
   
6. 클릭 **연결** tooestablish StorSimple 장치에 iSCSI 세션입니다. A **tooTarget 연결** 대화 상자가 표시 됩니다.
7. Hello에 **tooTarget 연결** 대화 상자, 선택 hello **다중 경로 사용** 확인란 합니다. **고급**을 클릭합니다.
8. Hello에 **고급 설정** 대화 상자에서 다음 hello지 않습니다.                                        
   
   * Hello에 **로컬 어댑터** 드롭 다운 목록 **Microsoft iSCSI 초기자**합니다.
   * Hello에 **초기자 IP** 드롭 다운 목록, hello 호스트의 IP 주소 선택 hello 합니다.
   * Hello에 **대상 포털** IP 드롭 다운 목록에서 장치 인터페이스의 선택 hello IP입니다.
   * 클릭 **확인** tooreturn toohello **iSCSI 초기자 속성** 대화 상자.
9. **속성**을 클릭합니다. Hello에 **속성** 대화 상자를 클릭 **세션 추가**합니다.
10. Hello에 **tooTarget 연결** 대화 상자, 선택 hello **다중 경로 사용** 확인란 합니다. **고급**을 클릭합니다.
11. Hello에 **고급 설정** 대화 상자:                                        
    
    * Hello에 **로컬 어댑터** 드롭 다운 목록에서 선택 Microsoft iSCSI 초기자입니다.
    * Hello에 **초기자 IP** 드롭 다운 목록, 선택 hello IP 주소 해당 toohello 호스트 합니다. 이 경우에 hello 호스트에 hello 장치 tooa 단일 네트워크 인터페이스에서 두 개의 네트워크 인터페이스를 연결 합니다. 따라서이 인터페이스는 첫 번째 세션 hello에 대 한 제공 된 것과 동일한 안녕 합니다.
    * Hello에 **대상 포털 IP** 드롭 다운 목록, hello hello 장치에서 사용할 수는 두 번째 데이터 인터페이스에 대 한 선택 hello IP 주소입니다.
    * 클릭 **확인** tooreturn toohello iSCSI 초기자 속성 대화 상자. 두 번째 세션 toohello 대상을 추가 했습니다.
12. 열기 **컴퓨터 관리** 너무 이동 하 여**서버 관리자 > 대시보드 > 컴퓨터 관리**합니다. Hello 왼쪽된 창에서 클릭 **저장소 > 디스크 관리**합니다. hello는 표시 toothis 호스트 hello StorSimple 장치에서 만든 볼륨 아래에 표시 될 **디스크 관리** 새 디스크로 합니다.
13. Hello 디스크를 초기화 하 고 새 볼륨을 만듭니다. Hello 형식 과정에서 64kb 블록 크기를 선택 합니다.
    ![디스크 관리](./media/storsimple-configure-mpio-windows-server/IC741008.png)
14. **디스크 관리**를 마우스 오른쪽 단추로 클릭 hello **디스크** 선택 **속성**합니다.
15. StorSimple 모델 hello에 # # # **다중 경로 디스크 장치 속성** 대화 상자를 클릭 hello **MPIO** 탭 합니다. ![StorSimple 8100 다중 경로 디스크 장치 속성입니다.](./media/storsimple-configure-mpio-windows-server/IC741009.png)
16. Hello에 **DSM 이름** 섹션에서 클릭 **세부 정보** hello 매개 변수 toohello 기본 매개 변수를 설정 되어 있는지 확인 합니다. hello 기본 매개 변수는:
    
    * 경로 확인 기간 = 30
    * 재시도 횟수 = 3
    * PDO 제거 기간 = 20
    * 재시도 간격 = 1
    * 경로 확인 사용 = 선택하지 않음

> [!NOTE]
> **Hello 기본 매개 변수를 수정 하지 마십시오.**


## <a name="step-4-configure-mpio-for-high-availability-and-load-balancing"></a>4단계: 고가용성 및 부하 분산을 위해 MPIO 구성
다중 경로 기반 고가용성 및 부하 분산, 여러 개의 세션이 수동으로 추가 해야 toodeclare hello 다른 사용할 수 있는 경로입니다. 예를 들어 hello 호스트에 연결 하는 두 가지 인터페이스 경우 tooSAN 및 hello 장치에 연결 된 두 개의 인터페이스 tooSAN, 4 개 세션 (세션이 두 개만 있으면 됩니다 각 DATA 인터페이스 및 호스트 인터페이스가 경우 적절 한 경로 순열을 사용 하 여 구성 해야 합니다. 다른 IP 서브넷에 라우팅할 수 있는있지 않습니다).

**Hello 장치 및 응용 프로그램 호스트 사이의 적어도 8 활성 병렬 세션을 해야 하는 것이 좋습니다.** 이를 위해 Windows Server 시스템에서 4개의 네트워크 인터페이스를 사용하도록 설정하면 됩니다. Windows Server 호스트에서 하드웨어 또는 운영 체제 수준 hello에 실제 네트워크 인터페이스 또는 네트워크 가상화 기술을 통해 가상 인터페이스를 사용 합니다. Hello 두 네트워크 인터페이스가 hello 장치 있는이 구성은 8 활성 세션으로 반환 됩니다. 이 구성은 hello 장치와 클라우드 처리량을 최적화 하는 데 도움이 됩니다.

> [!IMPORTANT]
> **1GbE 및 10GbE 네트워크 인터페이스는 혼용하지 않는 것이 좋습니다. 두 개의 네트워크 인터페이스를 사용 하는 경우 두 인터페이스가 hello 동일한 형식 이어야 합니다.**

hello 다음 절차에서는 두 네트워크 인터페이스가 있는 경우 두 개의 네트워크 인터페이스를 사용 하 여 StorSimple 장치는 연결 된 tooa tooadd 세션을 호스트 하는 방법입니다. 이 경우 활성 세션은 2개뿐입니다. 이 절차를 사용 하 여 4 개의 네트워크 인터페이스와 두 개의 네트워크 인터페이스 연결된 tooa 호스트와 StorSimple 장치를 포함 합니다. 여기에 설명 된 4 세션 hello 대신 tooconfigure 8 필요 합니다.

### <a name="tooconfigure-mpio-for-high-availability-and-load-balancing"></a>고가용성 및 부하 분산에 대 한 MPIO tooconfigure
1. Hello 대상의 검색을 수행: hello에 **iSCSI 초기자 속성** 대화 상자의 hello **검색** 탭을 클릭 **포털 검색**합니다.
2. Hello에 **tooTarget 연결** 대화 상자에서 hello 장치 네트워크 인터페이스 중 하나의 hello IP 주소를 입력 합니다.
3. 클릭 **확인** tooreturn toohello **iSCSI 초기자 속성** 대화 상자.
4. Hello에 **iSCSI 초기자 속성** 대화 상자, 선택 hello **대상** 탭 hello 검색 대상을 선택한 다음 클릭 **연결**합니다. hello **tooTarget 연결** 대화 상자가 나타납니다.
5. Hello에 **tooTarget 연결** 대화 상자:
   
   * Leave hello 기본적으로 선택에 대 한 대상 설정 **이 연결 추가** toohello 즐겨 찾는 대상 목록입니다. 이 컴퓨터를 다시 시작할 때마다 자동으로 toorestart hello 연결을 시도 하는 hello 장치를 확인 합니다.
   * 선택 hello **다중 경로 사용** 확인란 합니다.
   * **고급**을 클릭합니다.
6. Hello에 **고급 설정** 대화 상자:
   
   * Hello에 **로컬 어댑터** 드롭 다운 목록 **Microsoft iSCSI 초기자**합니다.
   * Hello에 **초기자 IP** 드롭 다운 목록, hello 호스트의 IP 주소 선택 hello 합니다.
   * Hello에 **대상 포털 IP** 드롭 다운 목록, hello 장치에서 사용 하도록 설정 하는 hello 데이터 인터페이스의 IP 주소 선택 hello 합니다.
   * 클릭 **확인** tooreturn toohello iSCSI 초기자 속성 대화 상자.
7. 클릭 **속성**, 및 hello **속성** 대화 상자를 클릭 **세션 추가**합니다.
8. Hello에 **tooTarget 연결** 대화 상자, 선택 hello **다중 경로 사용** 확인란을 선택한 다음 클릭 **고급**합니다.
9. Hello에 **고급 설정** 대화 상자:
   
   1. Hello에 **로컬 어댑터** 드롭 다운 목록 **Microsoft iSCSI 초기자**합니다.
   2. Hello에 **초기자 IP** 드롭 다운 목록, 선택 hello IP 주소 해당 toohello 두 번째 인터페이스에 hello 호스트 합니다.
   3. Hello에 **대상 포털 IP** 드롭 다운 목록, hello hello 장치에서 사용할 수는 두 번째 데이터 인터페이스에 대 한 선택 hello IP 주소입니다.
   4. 클릭 **확인** tooreturn toohello **iSCSI 초기자 속성** 대화 상자. 이제 두 번째 세션 toohello 대상을 추가 되었습니다.
10. Tooadd 추가 세션 (경로) toohello 대상 8 ~ 10 단계를 반복 합니다. Hello 호스트에 두 개의 인터페이스 및 hello 장치에 2 개를 4 개 세션의 합계를 추가할 수 있습니다.
11. Hello에 원하는 hello 세션 (경로)를 추가한 후 **iSCSI 초기자 속성** 대화 상자, 선택 hello 대상 및 클릭 **속성**합니다. Hello 세션 탭의 hello **속성** 대화 상자, 참고 hello 4 개 세션 식별자는 toohello 가능한 경로 순열에 해당 합니다. 세션을 toocancel hello 확인란 다음 tooa 세션 식별자를 선택한 다음 클릭 **연결 끊기**합니다.
12. 선택 hello 세션 내에서 제공 되는 tooview 장치 **장치** 탭 tooconfigure hello 선택한 장치에 대해 MPIO 정책을 클릭 **MPIO**합니다. hello **장치 세부 정보** 대화 상자가 표시 됩니다. Hello에 **MPIO** 탭을 적절 한 hello를 선택할 수 있습니다 **부하 분산 정책** 설정 합니다. Hello를 볼 수도 있습니다 **활성** 또는 **대기** 경로 유형입니다.

## <a name="next-steps"></a>다음 단계
에 대 한 자세한 내용은 [StorSimple 관리자 서비스 toomodify StorSimple 장치 구성 hello를 사용 하 여](storsimple-modify-device-config.md)합니다.

