---
title: "StorSimple Linux 호스트에 MPIO aaaConfigure | Microsoft Docs"
description: "CentOS 6.6를 실행 하는 연결 된 StorSimple tooa Linux 호스트에 MPIO 구성"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: tysonn
ms.assetid: ca289eed-12b7-4e2e-9117-adf7e2034f2f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: alkohli
ms.openlocfilehash: d9f7e02903243494c909313fb2c33ac690764274
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a>CentOS를 실행하는 StorSimple 호스트에서 MPIO 구성
이 문서에서는 Centos 6.6 호스트 서버의 hello 단계 필요한 tooconfigure 다중 경로 IO (MPIO)를 설명 합니다. hello 호스트 서버는 iSCSI 초기자를 통해 고가용성을 위해 연결 된 tooyour Microsoft Azure StorSimple 장치. 다중 경로 장치 및 hello StorSimple 볼륨에 대 한 특정 설정의 세부 hello 자동 검색에서 설명합니다.

이 절차는 StorSimple 8000 시리즈 장치와의 적용 가능한 tooall hello 모델입니다.

> [!NOTE]
> StorSimple 가상 장치에 이 절차를 사용할 수 없습니다. 자세한 내용은 tooconfigure 가상 장치에 대 한 서버를 호스트 하는 방법을 참조 합니다.
> 
> 

## <a name="about-multipathing"></a>다중 경로에 대해
hello 다중 경로 제어 기능 tooconfigure을 사용 하면 호스트 서버와 저장소 장치 간에 여러 I/O 경로가 있습니다. 이러한 I/O 경로는 별도 케이블, 스위치, 네트워크 인터페이스 및 컨트롤러를 포함할 수 있는 물리적 SAN 연결입니다. 다중 경로 제어 hello I/O 경로 tooconfigure 모든 hello 집계 경로와 연결 된 새 장치를 집계 합니다.

다중 경로 제어의 hello 용도는 두 가지입니다.

* **고가용성**: hello I/O 경로 (예: 케이블, 스위치, 네트워크 인터페이스 또는 컨트롤러)의 요소가 실패할 경우에 대체 경로 제공 합니다.
* **부하 분산**: 저장소 장치의 hello 구성에 따라 hello I/O 경로 대 한 부하를 감지 하 고 동적으로 부하를 리 밸런스 hello 성능을 높일 수 있습니다.

### <a name="about-multipathing-components"></a>다중 경로 구성 요소에 대해
Linux에서 다중 경로는 아래에 정리된 커널 구성 요소 및 사용자 공간 구성 요소로 구성되어 있습니다.

* **커널**: hello 주 구성 요소는 hello *장치 매퍼* I/O를 조정 하 고 경로 및 경로 그룹에 대 한 장애 조치를 지원 합니다.

* **사용자 공간**: 이들은 *다중 경로 도구* 어떤 toodo hello 장치 매퍼 다중 경로 모듈 지시 하 여 경로가 장치를 관리 하는 합니다. hello 도구는 다음으로 구성 됩니다.
   
   * **다중 경로**: 다중 경로인 장치를 나열하고 구성합니다.
   * **Multipathd**: hello 경로 다중 경로 및 모니터를 실행 하는 디먼 합니다.
   * **Devmap 이름**: devmaps에 대 한 의미 있는 장치 이름을 tooudev를 제공 합니다.
   * **Kpartx**: 선형 devmaps toodevice 파티션을 toomake 다중 경로 맵 이러한 시스템이 매핑합니다.
   * **Multipath.conf**: 다중 경로 데몬을 사용 하는 toooverwrite hello 기본 제공 구성 테이블에 대 한 구성 파일입니다.

### <a name="about-hello-multipathconf-configuration-file"></a>Hello multipath.conf 구성 파일에 대 한
hello 구성 파일 `/etc/multipath.conf` 사용 하면 다양 한 hello 다중 경로 제어 기능 사용자가 구성할 수 있습니다. hello `multipath` 명령과 hello 커널 데몬 `multipathd` 이 파일에 있는 정보를 사용 합니다. hello 파일을 hello 다중 경로 장치 hello 구성 중에 참조 합니다. Hello를 실행 하기 전에 모든 변경 내용을 한 않았는지 확인 `multipath` 명령입니다. Hello 파일을 수정 하는 경우 이후에 toostop 필요를 multipathd hello 변경 tootake 효과 대 한 다시 시작 합니다.

hello multipath.conf에 5 개 섹션이 있습니다.

- **시스템 수준 기본값** *(기본값)*: 시스템 수준 기본값을 재정의할 수 있습니다.
- **장치 차단 목록에 포함할** *(블랙 리스트)*: hello 목록은 장치-맵 편집기에 의해 제어 되지 해야 하는 장치를 지정할 수 있습니다.
- **예외 블랙 리스트에 추가** *(blacklist_exceptions)*: hello 블랙 리스트에 나열 된 경우에 다중 경로 장치도 처리 하는 특정 장치 toobe를 식별할 수 있습니다.
- **저장소 컨트롤러에 대 한 특정 설정** *(장치)*: 공급 업체 및 제품 정보를 가진 적용된 toodevices 수 있는 구성 설정을 지정할 수 있습니다.
- **특정 장치 설정을** *(multipaths)*: 개별 Lun에 대 한이 섹션 toofine 조정 hello 구성 설정을 사용할 수 있습니다.

## <a name="configure-multipathing-on-storsimple-connected-toolinux-host"></a>StorSimple tooLinux 연결 된 호스트에서 다중 경로 제어 구성
StorSimple 장치 연결 tooa Linux 호스트는 고가용성을 위해 구성할 수 있습니다 및 부하 분산 합니다. 예를 들어 hello Linux 호스트의 두 인터페이스가 연결 된 toohello hello 및 SAN 장치에 두 개의 인터페이스 toohello SAN 연결 동일한 서브넷에 hello 등 이러한 인터페이스에 있는 다음 사용할 수 있는 네 개의 경로입니다. 그러나 hello 장치 및 호스트 인터페이스에서 각 데이터 인터페이스에 있고 다른 IP 서브넷 (라우팅할 수 없음), 2 경로 사용할 수 됩니다 합니다. 다중 경로 제어 tooautomatically를 구성할 수 있습니다 hello 사용 가능한 모든 경로 검색, 해당 경로 대 한 부하 분산 알고리즘을 선택, StorSimple 전용 볼륨에 대 한 특정 구성 설정을 적용 하 고 다음을 사용 하도록 설정 및 다중 경로 제어를 확인 합니다.

hello 다음 절차에서는 설명 방법을 때 두 개의 네트워크 인터페이스를 사용 하 여 StorSimple 장치 tooconfigure 다중 경로 제어는 두 개의 네트워크 인터페이스와 연결 된 tooa 호스트 합니다.

## <a name="prerequisites"></a>필수 조건
이 섹션 CentOS 서버 및 StorSimple 장치에 대 한 hello 구성 필수 구성 요소에 자세히 설명 합니다.

### <a name="on-centos-host"></a>CentOS 호스트에서
1. CentOS 호스트에 사용 가능한 2개의 네트워크 인터페이스가 있는지 확인합니다. 형식:
   
    `ifconfig`
   
    hello 다음 경우를 보여 줍니다 hello 출력 2 개의 네트워크 인터페이스 (`eth0` 및 `eth1`) hello 호스트에 있는 합니다.
   
        [root@centosSS ~]# ifconfig
        eth0  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:41  
          inet addr:10.126.162.65  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3341/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3341/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
         RX packets:36536 errors:0 dropped:0 overruns:0 frame:0
          TX packets:6312 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:13994127 (13.3 MiB)  TX bytes:645654 (630.5 KiB)
   
        eth1  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:42  
          inet addr:10.126.162.66  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3342/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3342/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:25962 errors:0 dropped:0 overruns:0 frame:0
          TX packets:11 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:2597350 (2.4 MiB)  TX bytes:754 (754.0 b)
   
        loLink encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:12 errors:0 dropped:0 overruns:0 frame:0
          TX packets:12 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:720 (720.0 b)  TX bytes:720 (720.0 b)
2. CentOS 서버에 *iSCSI-initiator-utils* 를 설치합니다. 다음 단계 tooinstall hello 수행 *iSCSI-초기자-유틸리티*합니다.
   
   1. CentOS 호스트에 `root` 로 로그온합니다.
   2. Hello 설치 *iSCSI-초기자-유틸리티*합니다. 형식:
      
       `yum install iscsi-initiator-utils`
   3. Hello 후 *iSCSI-초기자-유틸리티* 가 성공적으로 설치 hello iSCSI 서비스를 시작 합니다. 형식:
      
       `service iscsid start`
      
       경우에 `iscsid` 실제로 시작 하 고 hello 수 `--force` 옵션 필요할 수 있습니다
   4. iSCSI 초기자를 사용 하 여 hello 부팅 시 사용할 수 있음을 tooensure `chkconfig` tooenable hello 서비스 명령입니다.
      
       `chkconfig iscsi on`
   5. tooverify 하는 제대로 설치 프로그램에서는 hello 명령을 실행 합니다.
      
       `chkconfig --list | grep iscsi`
      
       샘플 출력은 다음과 같습니다.
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       위 예제는 hello, 2, 3, 4 및 5의 실행된 수준에서 iSCSI 환경 부팅 시간에 실행 됩니다 볼 수 있습니다.
3. *device-mapper-multipath*를 설치합니다. 형식:
   
    `yum install device-mapper-multipath`
   
    hello 설치가 시작 됩니다. 형식 **Y** toocontinue 확인 메시지가 나타나면 합니다.

### <a name="on-storsimple-device"></a>StorSimple 장치에서
StorSimple 장치에는 다음이 있어야 합니다.

* iSCSI에 사용 가능한 두 개의 최소 인터페이스입니다. 두 인터페이스는 StorSimple 장치에서 iSCSI 사용 tooverify hello StorSimple 장치에 대 한 Azure 클래식 포털의에서 단계를 실행 하는 hello를 수행 합니다.
  
  1. StorSimple 장치에 대 한 hello 클래식 포털에 로그인 합니다.
  2. StorSimple Manager 서비스를 선택를 클릭 **장치** hello 특정 StorSimple 장치를 선택 합니다. 클릭 **구성** hello 네트워크 인터페이스 설정을 확인 하십시오. 두 가지 iSCSI를 사용하는 네트워크 인터페이스가 있는 스크린샷은 아래와 같습니다. 여기서 데이터 2와 데이터 3은 모두 iSCSI에 10GbE 인터페이스를 사용할 수 있습니다.
     
      ![MPIO StorsSimple 데이터 2 구성](./media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![MPIO StorSimple 데이터 3 구성](./media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      Hello에 **구성** 페이지
     
     1. 네트워크 인터페이스가 둘 모두  iSCSI를 사용할 수 있는지 확인합니다. hello **iSCSI 사용** 너무 필드를 설정 해야**예**합니다.
     2. Hello 네트워크 인터페이스가 hello 갖도록 동일한 속도 1gbe 또는 10gbe 둘 다에 있어야 합니다.
     3. Hello iSCSI 사용 인터페이스의 hello IPv4 주소를 확인 하 고 나중에 사용할 hello 호스트에 저장 합니다.
* StorSimple 장치에 iSCSI 인터페이스 hello hello CentOS 서버에서 연결할 수 있어야 합니다.
      tooverify이 호스트 서버에서 StorSimple iSCSI 사용 네트워크 인터페이스의 tooprovide hello IP 주소를 사용 해야 합니다. 사용 되는 명령을 hello 및 DATA2 사용 하 여 해당 출력 hello (10.126.162.25) 및 data 3 (10.126.162.26)는 다음과 같습니다.
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a>하드웨어 구성
중복성을 위해 별도 경로에 hello 두 iSCSI 네트워크 인터페이스에 연결 해야 하는 것이 좋습니다. 아래 hello 그림에는 CentOS 서버와 StorSimple 장치에 대 한 다중 경로 제어 부하 분산 및 고가용성에 대 한 hello 권장된 하드웨어 구성을 보여 줍니다.

![StorSimple tooLinux 호스트에 대 한 MPIO 하드웨어 구성](./media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

와 같이 앞 그림 hello:

* StorSimple 장치가 두 개의 컨트롤러를 사용하여 활성-수동 구성 중입니다.
* 두 개의 SAN 스위치는 연결 된 tooyour 장치 컨트롤러입니다.
* 두 개의 iSCSI 초기자를 StorSimple 장치에서 사용 가능합니다.
* 두 개의 네트워크 인터페이스를 CentOS 호스트에서 사용 가능합니다.

hello 호스트와 데이터 인터페이스는 라우팅할 수 있는 경우 구성 이상 hello 장치와 hello 호스트 사이의 4의 개별 경로 생성 합니다.

> [!IMPORTANT]
> * 다중 경로에 1GbE 및 10GbE 네트워크 인터페이스를 혼용하지 않는 것이 좋습니다. 두 개의 네트워크 인터페이스를 사용할 때 두 hello 인터페이스 hello 동일한 유형 이어야 합니다.
> * StorSimple 장치에서 DATA0, DATA1, DATA4 및 DATA5는 1GbE 인터페이스인 반면 DATA2 및 DATA3은 10GbE 네트워크 인터페이스입니다. |
> 
> 

## <a name="configuration-steps"></a>구성 단계
다중 경로 제어에 대 한 구성 단계 hello hello hello 부하 분산 알고리즘 toouse, 다중 경로 제어를 사용 하도록 설정 하 고 마지막으로 hello 구성을 확인 하는 지정 하는 자동 검색에 사용할 수 있는 경로 구성 작업이 포함 됩니다. 이러한 각 단계는 hello 다음 섹션에서에서 자세히 설명 합니다.

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a>1단계: 자동 검색에 다중 경로 구성
hello 다중 경로 지 원하는 장치를 자동으로 검색 및 구성 될 수 있습니다.

1. `/etc/multipath.conf` 파일을 초기화합니다. 형식:
   
     `mpathconf --enable`
   
    명령 위에 hello 만들어집니다는 `sample/etc/multipath.conf` 파일입니다.
2. 다중 경로 서비스를 시작합니다. 형식:
   
    `service multipathd start`
   
    다음 출력 hello를 표시 됩니다.
   
    `Starting multipathd daemon:`
3. 다중 경로의 자동 검색을 사용하도록 설정합니다. 형식:
   
    `mpathconf --find_multipaths y`
   
    hello 기본값 섹션을 수정 합니다이 프로그램 `multipath.conf` 아래와 같이:
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a>2단계: StorSimple 볼륨에 대한 다중 경로 구성
기본적으로 모든 장치는 검은색 hello multipath.conf 파일에 나열 하 고 사용 되지 않습니다. StorSimple 장치에서 볼륨에 대 한 toocreate 블랙 리스트 예외 tooallow 다중 경로 제어를 할 수 있습니다.

1. Hello 편집 `/etc/mulitpath.conf` 파일입니다. 형식:
   
    `vi /etc/multipath.conf`
2. Hello multipath.conf 파일에 hello blacklist_exceptions 섹션을 찾습니다. StorSimple 장치에는이 섹션의 블랙 리스트 예외로 표시 toobe가 필요 합니다. 관련 된 줄이 파일 toomodify 것 (사용 하 여만 hello 특정 모델의 사용 중인 hello 장치) 아래와 같이 주석 처리 제거:
   
        blacklist_exceptions {
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8100*"
            }
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8600*"
            }
           }

### <a name="step-3-configure-round-robin-multipathing"></a>3단계: 라운드 로빈 다중 경로 구성
이 부하 분산 알고리즘 균형 잡힌 고 라운드 로빈 방식으로 모든 hello 사용 가능한 multipaths toohello 활성 컨트롤러를 사용합니다.

1. Hello 편집 `/etc/multipath.conf` 파일입니다. 형식:
   
    `vi /etc/multipath.conf`
2. Hello에서 `defaults` 섹션, 집합 hello `path_grouping_policy` 너무`multibus`합니다. hello `path_grouping_policy` hello 기본 경로 그룹화 정책 tooapply toounspecified multipaths를 지정 합니다. hello 기본값 섹션 아래와 같이 표시 됩니다.
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> 가장 일반적인 값 hello `path_grouping_policy` 포함:
> 
> * 장애 조치 = 우선 순위 그룹 당 1개의 경로
> * multibus = 1개의 우선 순위 그룹에서 모든 유효한 경로
> 
> 

### <a name="step-4-enable-multipathing"></a>4단계: 다중 경로 사용하도록 설정
1. Hello를 다시 시작 `multipathd` 데몬 합니다. 형식:
   
    `service multipathd restart`
2. 아래와 같이 hello 출력이 됩니다.
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a>5단계: 다중 경로 확인
1. 먼저 iSCSI 연결이 hello StorSimple 장치도 다음과 같이 설정 되어 있는지 확인 합니다.
   
   a. StorSimple 장치를 검색합니다. 형식:
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on hello device>:<iSCSI port on StorSimple device>
    ```
    
    hello 출력 DATA0 IP 주소는 10.126.162.25 및 아웃 바운드 iSCSI 트래픽에 대 한 hello StorSimple 장치에 포트 3260 열릴 때 아래 표시 된 것과 같이입니다.
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    StorSimple 장치의 IQN 복사 hello `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, hello 출력 앞에서 합니다.

   b. Toohello 장치 대상 IQN을 사용 하 여 연결 합니다. hello StorSimple 장치가 여기 hello iSCSI 대상입니다. 형식:

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    hello 다음 예제에서는 대상 IQN 사용 하 여 출력의 `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`합니다. hello 출력 장치에 toohello 두 iSCSI 사용 네트워크 인터페이스를 성공적으로 연결 있는지를 나타냅니다.

    ```
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    ```

    호스트가 하나 밖에 인터페이스와 여기에 두 개의 경로 표시 해야 합니다 tooenable 두 hello 인터페이스 호스트에서 iSCSI에 대 한 합니다. Hello를 따르면 [Linux 설명서의에서 지침을 자세히](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html)합니다.

2. 볼륨은 hello StorSimple 장치에서 노출 된 toohello CentOS 서버입니다. 자세한 내용은 참조 [6 단계: 볼륨 만들기](storsimple-deployment-walkthrough.md#step-6-create-a-volume) hello StorSimple 장치에서 Azure 클래식 포털을 통해.

3. Hello 사용 가능한 경로 확인 합니다. 형식:

      ```
      multipath –l
      ```

      다음 예제는 hello 두 개의 사용 가능한 경로 있는 StorSimple 장치 연결 된 tooa 단일 호스트 네트워크 인터페이스에서 두 개의 네트워크 인터페이스에 대 한 hello 출력을 보여 줍니다.

        ```
        mpathb (36486fd20cc081f8dcd3fccb992d45a68) dm-3 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 7:0:0:1 sdc 8:32 active undef running
        `- 6:0:0:1 sdd 8:48 active undef running
        ```

        hello following example shows hello output for two network interfaces on a StorSimple device connected tootwo host network interfaces with four available paths.

        ```
        mpathb (36486fd27a23feba1b096226f11420f6b) dm-2 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 17:0:0:0 sdb 8:16 active undef running
        |- 15:0:0:0 sdd 8:48 active undef running
        |- 14:0:0:0 sdc 8:32 active undef running
        `- 16:0:0:0 sde 8:64 active undef running
        ```

        After hello paths are configured, refer toohello specific instructions on your host operating system (Centos 6.6) toomount and format this volume.

## <a name="troubleshoot-multipathing"></a>다중 경로 문제 해결
이 섹션에서는 다중 경로를 구성하는 동안 문제가 발생하는 경우 유용한 팁을 제공합니다.

Q. hello 변경 내용을 볼 수 없는 `multipath.conf` 파일 내용이 적용 됩니다.

A. 제공한 경우 모든 변경 내용을 toohello `multipath.conf` 파일인 toorestart hello 다중 경로 제어 서비스가 필요 합니다. Hello 다음 명령을 입력 합니다.

    service multipathd restart

Q. Hello StorSimple 장치에 두 개의 네트워크 인터페이스 및 두 개의 네트워크 인터페이스 hello 호스트에서 사용할 수 있습니다. Hello 사용 가능한 경로 나열 하는 경우 두 개의 경로 참조 합니다. 4 개의 사용 가능한 경로 toosee 예상 합니다.

A. Hello 두 경로 hello에 있는지 확인 동일한 서브넷 및 라우팅 가능 합니다. Hello 네트워크 인터페이스에 있고 서로 다른 Vlan 라우팅할 수 없음, 두 경로만 표시 됩니다. 한 가지 방법은 tooverify toomake hello StorSimple 장치에서 네트워크 인터페이스에서 두 hello 호스트 인터페이스를 연결할 수 있는지입니다. 너무 해야[Microsoft 지원에 문의](storsimple-contact-microsoft-support.md) 으로이 확인이 지원 세션을 통해 수행할 수 있습니다.

Q. 사용 가능한 경로를 나열하는 경우 어떤 출력도 나타나지 않습니다.

A. 일반적으로 hello 다중 경로 제어 데몬과 문제가 소개 모든 경로가 경로 표시 되지 하 고는 모든 문제가 여기의 hello에서 찾을 가능성이 높으며 `multipath.conf` 파일입니다.

볼 수 있는 실제로 일부 디스크 toohello 대상에 연결한 후 hello 다중 경로 목록에서 응답이 의미할 수도 디스크 없는으로 확인해 수도 있습니다.

* 다음 명령 toorescan hello SCSI 버스 hello를 사용 합니다.
  
    `$ rescan-scsi-bus.sh `(sg3_utils 패키지의 일부)
* Hello 다음 명령을 입력 합니다.
  
    `$ dmesg | grep sd*`
     
     또는
  
    `$ fdisk –l`
  
    최근에 추가된 디스크의 세부 정보를 반환합니다.
* StorSimple 디스크 인지 toodetermine는 hello 명령 다음에 사용 합니다.
  
    `cat /sys/block/<DISK>/device/model`
  
    StorSimple 디스크인지를 확인하는 문자열을 반환합니다.

또한 가능성이 적지만 가능한 원인은 iscsid pid일 수 있습니다. Hello iSCSI 세션에서 명령을 toolog 오프 다음 hello를 사용 합니다.

    iscsiadm -m node --logout -p <Target_IP>

StorSimple 장치 hello iSCSI 대상에 대해 모든 hello 연결 된 네트워크 인터페이스에 대해이 명령을 반복 합니다. 로그인 하면 모든 hello iSCSI 세션에서 hello iSCSI 대상 IQN tooreestablish hello iSCSI 세션을 사용 합니다. Hello 다음 명령을 입력 합니다.

    iscsiadm -m node --login -T <TARGET_IQN>


Q. 장치를 허용 목록에 추가되었는지 잘 모릅니다.

A. tooverify 장치 허용 목록, 인지 hello 다음 문제 해결 대화형 명령을 사용 합니다.

    multipathd –k
    multipathd> show devices
    available block devices:
    ram0 devnode blacklisted, unmonitored
    ram1 devnode blacklisted, unmonitored
    ram2 devnode blacklisted, unmonitored
    ram3 devnode blacklisted, unmonitored
    ram4 devnode blacklisted, unmonitored
    ram5 devnode blacklisted, unmonitored
    ram6 devnode blacklisted, unmonitored
    ram7 devnode blacklisted, unmonitored
    ram8 devnode blacklisted, unmonitored
    ram9 devnode blacklisted, unmonitored
    ram10 devnode blacklisted, unmonitored
    ram11 devnode blacklisted, unmonitored
    ram12 devnode blacklisted, unmonitored
    ram13 devnode blacklisted, unmonitored
    ram14 devnode blacklisted, unmonitored
    ram15 devnode blacklisted, unmonitored
    loop0 devnode blacklisted, unmonitored
    loop1 devnode blacklisted, unmonitored
    loop2 devnode blacklisted, unmonitored
    loop3 devnode blacklisted, unmonitored
    loop4 devnode blacklisted, unmonitored
    loop5 devnode blacklisted, unmonitored
    loop6 devnode blacklisted, unmonitored
    loop7 devnode blacklisted, unmonitored
    sr0 devnode blacklisted, unmonitored
    sda devnode whitelisted, monitored
    dm-0 devnode blacklisted, unmonitored
    dm-1 devnode blacklisted, unmonitored
    dm-2 devnode blacklisted, unmonitored
    sdb devnode whitelisted, monitored
    sdc devnode whitelisted, monitored
    dm-3 devnode blacklisted, unmonitored


자세한 내용은 이동 너무[다중 경로 제어에 대 한 대화형 명령 문제 해결을 사용 하 여](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html)합니다.

## <a name="list-of-useful-commands"></a>유용한 명령 목록
| 확인하라는 메시지가 표시되면  | 명령 | 설명 |
| --- | --- | --- |
| **iSCSI** |`service iscsid start` |iSCSI 서비스 시작 |
| &nbsp; |`service iscsid stop` |iSCSI 서비스 중지 |
| &nbsp; |`service iscsid restart` |iSCSI 서비스 다시 시작 |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |검색에 지정 된 hello 사용 가능한 대상 주소 |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |Toohello iSCSI 대상에 로그인 |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |Hello iSCSI 대상에서 로그 아웃 |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |iSCSI 초기자 이름 인쇄 |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |Hello iSCSI 세션 및 hello 호스트에서 검색 된 볼륨의 hello 상태 확인 |
| &nbsp; |`iscsi –m session` |Hello 호스트와 hello StorSimple 장치 간에 설정 된 모든 hello iSCSI 세션을 보여 줍니다. |
|  | | |
| **다중 경로 지정** |`service multipathd start` |다중 경로 디먼 시작 |
| &nbsp; |`service multipathd stop` |다중 경로 디먼 중지 |
| &nbsp; |`service multipathd restart` |다중 경로 디먼 다시 시작 |
| &nbsp; |`chkconfig multipathd on` </br> 또는 </br> `mpathconf –with_chkconfig y` |다중 경로 데몬 toostart 부팅 시 사용 하도록 설정 |
| &nbsp; |`multipathd –k` |문제 해결에 대 한 hello 대화형 콘솔 시작 |
| &nbsp; |`multipath –l` |다중 경로 연결 및 장치 나열 |
| &nbsp; |`mpathconf --enable` |`/etc/mulitpath.conf` |
|  | | |

## <a name="next-steps"></a>다음 단계
Linux 호스트에서 MPIO를 구성 하는 대로 다음 CentoS 6.6 문서 toorefer toohello를 할 수도 있습니다.

* [CentOS에 MPIO 설정](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [Linux 교육 가이드](http://linux-training.be/files/books/LinuxAdm.pdf)

