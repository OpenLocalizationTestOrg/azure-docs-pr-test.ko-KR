---
title: "Microsoft Azure StorSimple 8600 aaaInstall 장치 | Microsoft Docs"
description: "Toounpack, 랙 마운트를 하 고 배포 하 고 hello 소프트웨어를 구성 하기 전에 StorSimple 8600 장치 케이블 연결 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3d82ba5f-3e34-40dc-9c33-50f952bc6be8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 10/24/2016
ms.author: alkohli
ms.openlocfilehash: 0fc0ddf076725fededdde33a260b950b72edc8db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="unpack-rack-mount-and-cable-your-storsimple-8600-device"></a>StorSimple 8600 장치 개봉, 랙 탑재, 케이블 연결
## <a name="overview"></a>개요
Microsoft Azure StorSimple 8600은 이중 인클로저 장치이며 기본 및 EBOD 인클로저로 구성되어 있습니다. 이 자습서에서는 방법 toounpack, 랙 탑재 및 케이블 hello StorSimple 8600 장치의 하드웨어 hello StorSimple 소프트웨어를 구성 하기 전에 설명 합니다.

## <a name="unpack-your-storsimple-8600-device"></a>StorSimple 8600 장치 개봉
hello 다음 단계를 제공 확실 하 고 자세한 방법은 toounpack StorSimple 8600 저장 장치입니다. 이 장치는 두 상자, hello 기본 인클로저 및 EBOD 인클로저 hello에 대 한 다른 제공 됩니다. 이러한 두 상자는 단일 상자에 배치됩니다.

### <a name="prepare-toounpack-your-device"></a>Toounpack 장치 준비
장치를 포장을 풀기 전에 hello 다음 정보를 검토 합니다.

![경고 아이콘](./media/storsimple-safety/IC740879.png)![무거움 아이콘](./media/storsimple-8600-hardware-installation/HCS_HeavyWeight_Icon.png) **경고!**

1. 하면 손으로 운반할 경우 hello 장치의 두 사람이 사용할 수 있는 toomanage hello 가중치 있는지 확인 합니다. Too32 kg (70 파운드)를 완전히 구성 된 인클로저의 무게는입니다.
2. Hello 상자를 평평한 바닥에 배치 합니다.

다음으로, 다음 단계 toounpack hello 장치를 완료 합니다.

#### <a name="toounpack-your-device"></a>toounpack 장치
1. Hello 상자 및 hello 패키지 발포 폼 충돌, 절단, 침수 또는 기타 명백한 손상이에 검사 합니다. Hello 상자나 패키지 심각 하 게 손상 되 면 hello 상자를 열지 마십시오. 하십시오 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md) toohelp hello 장치가 올바르게 작동 하는지 여부를 평가 합니다.
2. Hello 바깥쪽 상자를 열고 tooprimary 인클로저와 EBOD 인클로저에 해당 하는 hello 두 상자를 꺼내서 합니다. Hello 기본 인클로저와 EBOD 인클로저의 포장을 풀기 이제 수 있습니다. 다음 그림 hello hello 인클로저 중 하나의 포장을 푼 hello 뷰를 보여 줍니다.
   
    ![저장소 장치 개봉하기](./media/storsimple-8600-hardware-installation/HCSUnpackyour4Udevice.png)
   
    **저장소 장치가 개봉된 상태**
   
   | 레이블 | 설명 |
   | --- | --- |
   |   1 |포장 상자 |
   |   2 |SAS 케이블(보조 프로그램 및 케이블 트레이) |
   |   3 |하단 발포 폼 |
   |   4 |장치 |
   |   5 |상단 발포 폼 |
   |   6 |액세서리 상자 |
3. Hello 두 상자 압축을 푼 후 했는지 확인 합니다.
   
   * 기본 인클로저 1 개 (hello 기본 인클로저 및 EBOD 인클로저에 두 개의 별도의 상자)
   * EBOD 인클로저 1개
   * 전원 코드 4개(각 상자에 2개씩)
   * SAS 케이블 2 개 (tooconnect hello 기본 인클로저 tooEBOD 인클로저)
   * 크로스 오버 이더넷 케이블 1개
   * 직렬 콘솔 케이블 2개
   * 직렬 액세스에 대한 직렬-USB 변환기 1개
   * 10GbE 네트워크 인터페이스와 함께 사용하기 위한 4개의 QSFP-대-SFP+어댑터
   * 2 랙 마운트 키트 (측면 레일 4 각 2 hello 기본 인클로저 및 EBOD 인클로저의 하드웨어 마운트), 각 상자에 1
   * 시작 설명서
     
     위에 나열 된 hello 항목을 수신 하지 않은 경우 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md)합니다.  

다음 단계 hello 장치 toorack 탑재 됩니다.

## <a name="rack-mount-your-storsimple-8600-device"></a>StorSimple 8600 장치 랙 탑재
다음 단계 tooinstall hello 전면 포스트와 후면 포스트가 있는 표준 19 인치 랙에에서 8600 StorSimple 저장소 장치를 따릅니다. 이 장치에는 기본 인클로저 및 EBOD 인클로저, 두 개의 인클로저가 있습니다. 둘 다 필요 toobe 랙 탑재 합니다.

hello 설치 hello 다음 절차에에서 설명 되어 있으며 각 하는 여러 단계로 구성 됩니다.

> [!IMPORTANT]
> StorSimple 장치는 올바른 작동을 위해 랙을 탑재해야 합니다.
> 
> 

### <a name="site-preparation"></a>사이트 준비
hello 인클로저 둘 다 전면 포스트와 후면 포스트가 있는 표준 19 인치 랙에 설치 되어야 합니다. 랙 설치에 대 한 프로시저 tooprepare 다음 hello를 사용 합니다.

#### <a name="tooprepare-hello-site-for-rack-installation"></a>랙 설치에 대 한 tooprepare hello 사이트
1. 해당 hello 주 및 확인 EBOD 인클로저는 평평 하 고 수준 안정 된 작업 바닥에 안전 하 게 저장 (또는 유사한 곳) 합니다.
2. 이점을 얻을 수를 tooset는 표준 AC hello 사이트 확인는 독립적인 소스 또는 무정전 전원 공급 장치 (UPS)가 있는 랙 배전 장치 (PDU)에서 전원 합니다.
3. 해당 한 4U (2 X 2U) 슬롯 toomount hello 엔클로저 하려는 hello 랙에서 사용할 수 있는 인지 확인 합니다.

![경고 아이콘](./media/storsimple-safety/IC740879.png)![무거움 아이콘](./media/storsimple-8600-hardware-installation/HCS_HeavyWeight_Icon.png) **경고!**

 Hello 장치 설치를 수동으로 처리 하는 경우 두 사람이 사용할 수 있는 toomanage hello 가중치 있는지 확인 합니다. Too32 kg (70 파운드)를 완전히 구성 된 인클로저의 무게는입니다.

### <a name="rack-prerequisites"></a>랙 필수 구성 요소
hello 엔클로저는 설치 된 표준 19 인치 랙 캐비닛와에서 설계 되었습니다.

* 최소 27.84 인치 랙에서 깊이 toopost 게시
* 최대 무게가 32kg hello 장치에 대 한
* 최대 역 압력은 5 파스칼(0.5mm 수면계)

### <a name="rack-mounting-rail-kit"></a>랙 탑재 레일 키트
Hello 19 인치 랙 캐비닛에 사용 하기 위해 일련의 탑재 레일이 제공 됩니다. hello 레일 된 toohandle hello 최대 인클로저 무게를 테스트 합니다. 이러한 레일은 hello 랙 내에 공간 손실 없이 여러 인클로저를 설치할 수 있게 수도 있습니다. Hello EBOD 인클로저를 먼저 설치 합니다.

#### <a name="tooinstall-hello-ebod-enclosure-on-hello-rails"></a>tooinstall hello hello 레일에 EBOD 인클로저
1. 내부 레일이 장치에 설치되지 않은 경우에만 이 단계를 수행합니다. 일반적으로 hello 내부 레일 hello 공장에서 설치 됩니다. 레일이 설치 되어 있지 않으면 hello 왼쪽 레일 및 오른쪽 레일 슬라이드 toohello hello 인클로저 섀시 측면에 설치 합니다. 각 면에서 6개의 미터 나사를 사용하여 연결합니다. hello 레일 슬라이드 표시 되어 있으며, 방향으로 toohelp **LH-전면** 및 **RH-전면**, hello hello 인클로저 후면을 향해 유선형 hello 끝에 늘어 지 끝 및 합니다.
   
    ![연결 레일 슬라이드 tooenclosure 섀시](./media/storsimple-8600-hardware-installation/HCSAttachingRailSlidestoEnclosureChassis.png)
   
    **연결 레일 슬라이드 toohello 부분의 hello 인클로저**
   
   | 레이블 | 설명 |
   | --- | --- |
   |  1 |M 3 x 4 단추 머리 나사 |
   |  2 |섀시 슬라이드 |
2. Hello 왼쪽된 레일 및 오른쪽 레일 어셈블리 toohello 랙 캐비닛 수직 재에 연결 합니다. hello 표시 되어 있어 **LH**, **RH**, 및 **이 쪽을** tooguide 올바른 방향을 알 안내 합니다.
3. Hello 전면 포스트와 후면 hello 레일 조립품의에서 hello 레일 핀을 찾습니다. Hello 레일 toofit hello 랙 포스트 사이 확장 하 고 hello pin hello 전면 및 후면 랙 포스트 수직 재 구멍에 삽입 합니다. Hello 레일 조립품이 평평해 수 있습니다.
4. 레일 어셈블리 toohello 랙 수직 재 hello 미터 나사 중 두 가지를 사용 하 여 제공 된 hello를 보호 합니다. Hello 전면 포스트와 후면 hello에 하나씩에서 나사 하나를 사용 합니다.
5. 다른 레일 조립품 hello에 대 한 이러한 단계를 반복 합니다.
   
     ![연결 레일 슬라이드 toorack 캐비닛](./media/storsimple-8600-hardware-installation/HCSAttachingRailSlidestoRackCabinet.png)
   
    **어셈블리 toohello 랙 레일 연결**
   
   | 레이블 | 설명 |
   | --- | --- |
   |   1 |고정 나사 |
   |   2 |정사각형 구멍 전면 랙 포스트 나사 |
   |   3 |왼쪽 전면 레일 위치 핀 |
   |   4 |고정 나사 |
   |   5 |왼쪽 후면 레일 위치 핀 |

### <a name="mounting-hello-ebod-enclosure-in-hello-rack"></a>Hello hello 랙에 EBOD 인클로저 탑재
방금 설치한 랙 레일 hello를 사용 하 여 hello hello 랙에 단계 toomount hello EBOD 인클로저를 다음을 수행 합니다.

#### <a name="toomount-hello-ebod-enclosure"></a>toomount hello EBOD 인클로저
1. 도우미와 hello 인클로저를 들어올려 및 hello 랙 레일에 맞춥니다.
2. 조심 스럽게 hello 인클로저 hello 레일에 삽입 하 고에 완전히 밀어 넣습니다 hello 랙 캐비닛 합니다.
   
    ![Hello 랙에 장치 삽입](./media/storsimple-8600-hardware-installation/HCSInsertingDeviceintheRack.png)
   
    **Hello hello 랙에 인클로저 탑재**
3. Hello 캡을 당겨 hello 왼쪽 및 오른쪽 전면 플랜지 캡을 제거 합니다. hello 플랜지 캡 hello 플랜지에 간단히 맞아 합니다.
4. Hello 랙에 hello 인클로저를 각 플랜지 왼쪽과 오른쪽을 통해 제공 된 십자 나사 하나를 설치 하 여 보호 합니다.
5. 위치에 키를 눌러 및 위치에 딸각 하 여 hello 플랜지 캡을 설치 합니다.
   
     ![플랜지 캡 설치](./media/storsimple-8600-hardware-installation/HCSInstallingFlangeCaps.png)
   
    **Hello 플랜지 캡 설치**
   
   | 레이블 | 설명 |
   | --- | --- |
   |   1 |인클로저 잠금 나사 |

### <a name="mounting-hello-primary-enclosure-in-hello-rack"></a>Hello hello 랙에 기본 인클로저 탑재
Toomount hello 기본 인클로저 해야는 hello EBOD 인클로저 탑재를 완료 한 후 다음 hello 동일한 단계입니다.

> [!NOTE]
> * 가능한 toohave hello에 빈 슬롯이 별로 랙 hello 기본 인클로저 및 EBOD 인클로저의 hello 사이 이며
> * Hello 제공 된 2m SAS 케이블 tooconnect hello 기본 인클로저 toohello EBOD 인클로저를 사용 합니다.
> * Hello hello 헤드 단위 toohello EBOD 단위의 상대 위치에 없는 제약 조건이 있습니다. 따라서 hello 맨 위 슬롯 및 hello EBOD 인클로저는 아래에 hello 기본 인클로저를 배치할 수 있습니다-또는 그 반대의 경우도 마찬가지입니다.
> 
> 

hello 다음 단계는 toocable 전원, 네트워크 및 직렬 액세스에 대 한 장치입니다.

## <a name="cable-your-storsimple-8600-device"></a>StorSimple 8600 장치 케이블 연결
hello 다음 절차에서는 설명 방법을 toocable 8600 StorSimple 장치를 전원, 네트워크 및 직렬 연결 합니다.

### <a name="prerequisites"></a>필수 조건
Toocable 장치를 시작 하기 전에 필요 합니다.

* 기본 인클로저 및 EBOD 인클로저 hello 완전히 포장을 푼
* 장치와 함께 제공 된 4 전원 케이블 (2 각 hello 기본 및 EBOD 인클로저 hello에 대 한)
* EBOD 인클로저가 기본 인클로저에 toohello hello 장치 tooconnect hello와 함께 제공 된 SAS 케이블 2 개
* 액세스 too2 전원 Pdu (배전) (권장)
* 네트워크 케이블
* 제공된 직렬 케이블
* 직렬-USB 변환기 (필요한 경우) 사용자 PC에 설치 하는 hello 적절 한 드라이버
* 10GbE 네트워크 인터페이스와 함께 사용하기 위해 제공된 4개의 QSFP-대-SFP+어댑터
* [StorSimple 장치에 hello 10 GbE 네트워크 인터페이스에 대 한 지원 되는 하드웨어](storsimple-supported-hardware-for-10-gbe-network-interfaces.md)

### <a name="sas-and-power-cabling"></a>SAS 및 전원 케이블 연결
이 장치에는 기본 인클로저 및 EBOD 인클로저가 있습니다. 그러려면 hello 단위 toobe SCSI SAS (Serial Attached) 연결 및 전원에 대해 함께 케이블로 연결 합니다.

을 설정할 때 hello에 대 한이 장치를 처음으로 먼저 SAS 케이블 연결 및 전원 케이블 연결에 대 한 다음 전체 hello 단계에 대 한 hello 단계를 수행 합니다.

[!INCLUDE [storsimple-cable-8600-for-SAS](../../includes/storsimple-sas-cable-8600.md)]

[!INCLUDE [storsimple-cable-8600-for-power](../../includes/storsimple-cable-8600-for-power.md)]

### <a name="network-cabling"></a>네트워크 케이블 연결
장치는 활성-대기 구성 상태: 지정된 된 시간에 컨트롤러 모듈 하나가 활성 상태 이며 대기 다른 컨트롤러 모듈은 hello 모든 디스크 및 네트워크 작업을 처리 합니다. 컨트롤러 오류가 발생할 경우 hello 대기 컨트롤러가 즉시 활성화 되 고이 모든 hello 디스크 및 네트워킹 작업을 계속 됩니다.

toosupport hello 다음 단계에에서 나와 있는 것 처럼 장치 네트워크 toocable 해야이 중복 컨트롤러 장애 조치 합니다.

#### <a name="toocable-for-network-connection"></a>네트워크 연결에 대 한 toocable
1. 장치에는 각 컨트롤러에 4개의 1Gbps 이더넷 포트와 2개의 10Gbps 이더넷 포트, 모두 6개의 네트워크 인터페이스가 있습니다. 에 나오는 그림 tooidentify hello 데이터 포트에 따라 장치의 백플레인에서 hello toohello를 참조 하십시오.
   
     ![8600 장치의 백플레인](./media/storsimple-8600-hardware-installation/HCSBackplaneof2UDevicewithPortsLabeled.jpg)
   
    **Hello 데이터 포트가 표시 된 장치의 후면**
   
   | 레이블 | 설명 |
   | --- | --- |
   |   0,1,4,5 |1GbE 네트워크 인터페이스 |
   |   2,3 |10GbE 네트워크 인터페이스 |
   |   6 |직렬 포트 |
2. 네트워크 케이블 연결에 대 한 다이어그램을 다음 hello를 참조 하십시오. (hello 최소 네트워크 구성은 파란색 실선으로 표시 됩니다. 높은 가용성과 성능을 위해 필요한 추가 구성을 점선으로 표시했습니다.)

![4U 장치를 네트워크에 케이블 연결](./media/storsimple-8600-hardware-installation/HCSCableYour4UDeviceforNetwork.png)

**장치에 네트워크 케이블 연결**

| 레이블 | 설명 |
| --- | --- |
| 문자열(UTF-8 형식) 또는 |인터넷 액세스 LAN |
| B |컨트롤러 0 |
| C |PCM 0 |
| D |컨트롤러 1 |
| E |PCM 1 |
| F |EBOD 컨트롤러 0 |
| G |EBOD 컨트롤러 1 |
| H, I |호스트(예: 파일 서버) |
| 0-5 |네트워크 인터페이스 |
| 6 |기본 인클로저 |
| 7 |EBOD 인클로저 |

Hello 장치 케이블 연결 하는 경우에 최소 구성을 적용 hello 필요 합니다.

* 클라우드 액세스에 대한 하나의 네트워크 인터페이스 및 iSCSI에 대한 하나의 네트워크 인터페이스로 각 컨트롤러에 연결된 적어도 두 개의 네트워크 인터페이스. 데이터 0 포트가 자동으로 활성화 되어 있으며 hello hello 장치의 직렬 콘솔을 통해 구성 된 번호입니다. DATA 0 제외한 다른 데이터 포트는 toobe hello Azure 클래식 포털을 통해 구성도 필요 합니다. 이 경우에 DATA 0 포트 toohello 기본 LAN (인터넷에 연결 된 네트워크)을 연결 합니다. hello 다른 데이터 포트 수 연결 hello 의도 한 역할에 따라 hello 네트워크의 tooSAN/iSCSI LAN (VLAN) 세그먼트입니다.
* 각 연결 컨트롤러 toohello의 동일한 인터페이스 동일 네트워크 컨트롤러 장애 조치가 발생 tooensure 가용성입니다. 예를 들어, tooconnect DATA 0 선택 하 고 tooconnect hello에 DATA 0 및 DATA 3에 해당 해야 hello 컨트롤러 중 하나에 대 한 데이터 3, 경우에 다른 컨트롤러를 hello 합니다.

높은 가용성과 성능을 위해 유의하십시오.

* 가능하면 각 컨트롤러에서 클라우드 액세스(1GbE)에 대한 네트워크 인터페이스의 쌍 및 iSCSI(10GbE 권장)에 대한 다른 쌍을 구성합니다.
* 가능 하면 여 스위치 오류에 대 한 각 컨트롤러 tootwo 서로 다른 스위치 tooensure 가용성에서 네트워크 인터페이스를 연결 합니다. hello 그림 hello 두 개의 10 GbE 네트워크 인터페이스를, DATA 2 및 DATA 3의 경우 각 연결 컨트롤러 tootwo 서로 다른 스위치를 보여 줍니다. 자세한 내용은 참조 toohello **네트워크 인터페이스** hello에서 [StorSimple 장치의 고가용성 요구 사항을](storsimple-system-requirements.md#high-availability-requirements-for-storsimple)합니다.

> [!NOTE]
> 10 GbE 네트워크 인터페이스와 SFP + 송수신 장치를 사용 하는 경우 사용 하 여 hello 제공 QSFP-+ 어댑터. 자세한 내용은 이동 너무[hello 10 GbE 네트워크 인터페이스에서 StorSimple 장치에 대 한 지원 되는 하드웨어](storsimple-supported-hardware-for-10-gbe-network-interfaces.md)합니다.
> 
> 

### <a name="serial-port-cabling"></a>직렬 포트 케이블 연결
직렬 포트 hello 단계 toocable 다음을 수행 합니다.

#### <a name="toocable-for-serial-connection"></a>toocable 직렬 연결
1. 장치에는 각 컨트롤러에 렌치 아이콘으로 식별되는 직렬 포트가 있습니다. toolocate hello 직렬 포트에 장치의 후면 hello hello 데이터 포트를 보여 주는 예시를 toohello를 참조 하십시오.
2. Hello에 장치 백플레인에서 활성 컨트롤러를 식별 합니다. 깜박이 파란색 LED는 hello 컨트롤러가 활성 상태임을 나타냅니다.
3. Hello 제공 된 직렬 케이블 (필요한 경우, 랩톱에 대 한 hello USB-직렬 변환기)을 사용 하 고 (장치와 터미널 에뮬레이션 toohello) 콘솔 또는 컴퓨터를 연결 toohello hello 활성 컨트롤러의 직렬 포트입니다.
4. 컴퓨터에 (hello 장치와 함께 제공) hello 직렬-USB 드라이버를 설치 합니다.
5. 다음과 같이 hello 직렬 연결을 설정 합니다.
   
   * 115,200 baud
   * 8 데이터 비트
   * 1 정지 비트
   * 패리티 없음
   * 흐름 제어 설정 너무**없음**
6. Hello 콘솔에 Enter 키를 눌러 hello 연결이 작동 하는지 확인 합니다. 그러면 직렬 콘솔 메뉴가 나타납니다.

> [!NOTE]
> **Lights-Out Management:** hello 장치는 원격 데이터 센터에서 또는 액세스가 제한 된 컴퓨터실에 설치 되 면 hello 직렬 연결을 tooboth 컨트롤러는 연결 된 tooa 직렬 콘솔 스위치 또는 유사한 장비 항상 확인 합니다. 이렇게 하면 네트워크 중단 또는 예기치 않은 장애 발생 시 대역 외 원격 제어 및 지원 작업이 허용됩니다.
> 
> 

전원, 네트워크 액세스에 대 한 장치 케이블 연결을 완료 하 고 직렬 connection.hello 다음 단계는 장치에서 tooconfigure hello 소프트웨어입니다.

## <a name="next-steps"></a>다음 단계
이제 준비가 너무[배포 하 고 온-프레미스 StorSimple 장치 구성](storsimple-deployment-walkthrough-u2.md)합니다.

