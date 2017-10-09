---
title: "aaaModify hello StorSimple 8000 시리즈 장치 구성 | Microsoft Docs"
description: "어떻게 toouse hello StorSimple 장치 관리자 서비스 tooreconfigure 이미 배포 된 StorSimple 장치에 설명 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 79711b45eafe732c1eed1e562b05e3837fbc9d03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomodify-your-storsimple-device-configuration"></a>사용 하 여 hello StorSimple 장치 관리자 서비스 toomodify StorSimple 장치 구성

## <a name="overview"></a>개요

Azure 포털 hello **장치 설정** hello 섹션인 **설정을** 블레이드는 StorSimple 장치 관리자에서 관리 되는 StorSimple 장치에는 다시 구성할 수 있는 모든 hello 장치 매개 변수가 포함 서비스입니다. 이 자습서에서는 hello를 사용 하는 방법에 대해 설명 **설정을** 블레이드 tooperform hello 장치 수준 태스크를 수행 합니다.

* 장치 이름 수정
* 장치 시간 설정 수정
* 보조 DNS 할당
* 네트워크 인터페이스 수정
* IP 교체 또는 재할당

## <a name="modify-device-friendly-name"></a>장치 이름 수정

Hello Azure 포털 toochange hello 장치 이름을 사용 하 고 원하는 고유한 이름을 지정할 수 있습니다. 사용 하 여 hello **일반 설정** 장치 toomodify hello 장치 친숙 한 이름을 블레이드입니다. hello 이름 모든 문자를 포함할 수 및 최대 64 자일 수 있습니다.

> [!NOTE] 
> Hello 장치 설치가 완료 되기 전에 hello Azure 포털에서에서 장치 이름을 hello 수정할 수 있습니다. Hello 최소 장치 설정 완료 되 면 hello 장치 이름을 변경할 수 없습니다.

![일반 설정의 장치 이름](./media/storsimple-8000-modify-device-config/modify-general-settings3.png)

StorSimple 장치에 연결 된 toohello StorSimple 장치 관리자 서비스는 기본 이름이 할당 됩니다. hello 기본 이름은 일반적으로 hello hello 장치 일련 번호를 반영합니다. 예를 들어, 기본 장치 이름이 15 자, 8600-SHX0991003G44HT 같은 hello 다음을 나타냅니다.

* **8600** – hello 장치 모델을 나타냅니다.
* **SHX** – hello 제조 사이트를 나타냅니다.
* **0991003** - 특정 제품을 나타냅니다.
* **G44HT**-hello 마지막 5 자리는 고유한 일련 번호가 증가 toocreate 합니다. 순차적인 집합이 아닐 수 있습니다.

## <a name="modify-device-description"></a>장치 설명 수정

사용 하 여 hello **일반 설정** 장치 toomodify hello 장치 설명에 블레이드 합니다.

![일반 설정의 장치 설명](./media/storsimple-8000-modify-device-config/modify-general-settings4.png)

일반적으로 장치 설명을 통해 hello 소유자 및 hello hello 장치의 물리적 위치를 식별 합니다. hello 설명 필드에는 256 자 미만을 포함 해야 합니다.

## <a name="modify-time-settings"></a>시간 설정 수정

장치는 클라우드 저장소 서비스 공급자와 순서 tooauthenticate에서 경과한 시간을 동기화 해야 합니다. 사용 하 여 hello **일반 설정** 블레이드 장치 toomodify hello 장치 시간 설정에 있습니다.

![일반 설정의 장치 설명](./media/storsimple-8000-modify-device-config/modify-general-settings2.png)

 Hello 드롭 다운 목록에서 표준 시간대를 선택 합니다. Tootwo 시간이 NTP (Network Protocol) 서버를 지정할 수 있습니다.

 - **기본 NTP 서버** -hello 구성이 필수 이기에 사용 하면 Windows PowerShell StorSimple tooconfigure 장치 지정 됩니다. Hello 기본 Windows 서버를 지정할 수 있습니다 **time.windows.com** NTP 서버와 합니다. Hello 주 NTP 서버 구성은 hello Azure 포털을 통해 볼 수는 있지만 Windows PowerShell 인터페이스 toochange hello를 사용 해야 것입니다. 사용 하 여 hello `Set-HcsNTPClientServerAddress` 장치의 cmdlet toomodify hello 기본 NTP 서버입니다. 자세한 내용은 [Set-hcsntpclientserveraddress] (https://technet.microsoft.com/library/dn688138.aspx) cmdlet에 대 한 toosynxtax를 이동 합니다.

- **보조 NTP 서버** -hello 구성은 선택 사항입니다. Hello 포털 tooconfigure 보조 NTP 서버를 사용할 수 있습니다.

Hello NTP 서버를 구성할 때 네트워크 사용자 데이터 센터 toohello 인터넷에서에서 NTP 트래픽이 toopass hello 허용 되는지 확인 합니다. 공용 NTP 서버를 지정할 때는 네트워크 방화벽 및 기타 보안 장치가 구성된 tooallow hello 네트워크 외부에서 NTP 트래픽이 tootravel tooand가 있는지 확인 해야 합니다. 양방향 NTP 트래픽이 허용되지 않는 경우 내부 NTP 서버(Windows 도메인 컨트롤러가 이 기능을 제공)를 사용해야 합니다. 장치 시간을 동기화 할 수 없습니다, 클라우드 저장소 공급자와 수 toocommunicate 되지 않을 수 있습니다.

공용 NTP 서버를 이동 toohello 목록이 toosee [NTP 서버 웹](http://support.ntp.org/bin/view/Servers/WebHome)합니다.

### <a name="what-happens-if-hello-device-is-deployed-in-a-different-time-zone"></a>Hello 장치는 다른 표준 시간대에 배포 하는 경우 어떻게 됩니까?

Hello 장치가 다른 표준 시간대에 배포 하는 경우에 hello 장치 표준 시간대 변경 됩니다. Hello 장치 표준 시간대를 사용 하는 모든 hello 백업 정책, 있다고 가정 hello 백업 정책 hello 새 표준 시간대에 따라 자동으로 조정 됩니다. 사용자 개입이 필요 없습니다.

## <a name="modify-dns-settings"></a>DNS 설정 수정

DNS 서버는 장치가 클라우드 저장소 서비스 공급자와 toocommunicate을 시도할 때 사용 됩니다. 사용 하 여 hello **네트워크 설정** 블레이드 장치 tooview에서 DNS 설정을 구성 하는 hello 하 고 수정 합니다. 

![네트워크 설정에서 DNS 설정](./media/storsimple-8000-modify-device-config/modify-network-settings1.png)

고가용성을 위해 필요한 tooconfigure 기본 두 hello 하 고 hello 초기 장치 배포 하는 동안 보조 DNS 서버 hello 합니다.

**기본 DNS 서버** -Windows PowerShell hello를 사용 하 여 StorSimple toofirst hello 초기 설치 작업 동안 hello 주 DNS 서버를 지정 합니다. Hello Windows PowerShell 인터페이스를 통해서만 hello 주 DNS 서버를 다시 구성할 수 있습니다. 사용 하 여 hello `Set-HcsDNSClientServerAddress` 장치의 cmdlet toomodify hello 주 DNS 서버입니다. 에 대 한 자세한 내용은 이동 toosynxtax [Set-hcsdnsclientserveraddress](https://technet.microsoft.com/library/dn688138.aspx) cmdlet.

**보조 DNS 서버** -toomodify hello 보조 DNS 서버를 사용 하 여 hello `Set-HcsDNSClientServerAddress` hello 장치의 hello Windows PowerShell 인터페이스에서 cmdlet 또는 **네트워크 설정** hello Azure StorSimple 장치의의 블레이드 포털입니다.

Azure 포털에서 toomodify hello 보조 DNS 서버 hello 다음 단계를 수행 합니다.

1. Tooyour StorSimple 장치 관리자 서비스를 이동 합니다. Hello 장치 목록에서 선택 하 고 장치를 클릭 합니다.

2. Hello에 **설정** 블레이드에서 너무 이동**장치 설정 > 네트워크**합니다. Hello를 열어서이 **네트워크 설정** 블레이드입니다. **DNS 설정** 타일을 클릭합니다. Hello 보조 DNS 서버 IP 주소를 수정 합니다.

    ![보조 DNS 서버 IP 주소 수정](./media/storsimple-8000-modify-device-config/modify-secondary-dns1.png)

4. Hello 명령 모음에서 클릭 **저장** 확인 메시지가 나타나면 클릭 하 고 **확인**합니다.

    ![변경 내용 저장 및 확인](./media/storsimple-8000-modify-device-config/modify-secondary-dns-2.png)



## <a name="modify-network-interfaces"></a>네트워크 인터페이스 수정

장치에는 6개의 장치 네트워크 인터페이스가 있으며, 그 중 4개는 1GbE, 2개는 10GbE입니다. 이러한 인터페이스는 DATA 0부터 DATA 5로 레이블이 지정됩니다. DATA 0, DATA 1, DATA 4 및 DATA 5는 1GbE인 반면, DATA 2 및 DATA 3은 10GbE 네트워크 인터페이스입니다.

사용 하 여 hello **네트워크 설정** 블레이드 tooconfigure 각의 hello toobe 사용 되는 인터페이스입니다.

![네트워크 설정을 통해 네트워크 인터페이스 구성](./media/storsimple-8000-modify-device-config/modify-network-settings3.png)

tooensure 고가용성을 두 개 이상의 iSCSI 인터페이스 및 클라우드 지원 인터페이스를 두 개의 장치에 있는 두는 것이 좋습니다. 권장 사항이지만 사용하지 않는 인터페이스를 사용하지 않도록 설정할 필요는 없습니다.

각 네트워크 인터페이스에 대 한 매개 변수 뒤 hello 표시 됩니다.

* **속도** – 사용자가 구성할 수 있는 매개 변수가 아닙니다. DATA 0, DATA 1, DATA 4 및 DATA 5는 1GbE인 반면, DATA 2 및 DATA 3은 10GbE 인터페이스입니다.
  
  > [!NOTE]
  > 속도 및 이중 교환 패턴은 항상 자동으로 협상합니다. Jumbo 프레임이 지원되지 않습니다.
  
* **인터페이스 상태** – 인터페이스를 설정하거나 해제할 수 있습니다. 사용 하도록 설정 하는 경우 hello 장치 toouse hello 인터페이스를 시도 합니다. 연결 된 toohello 네트워크 고 사용 하는 인터페이스에만 사용할 수 있도록 하는 것이 좋습니다. 사용하지 않는 모든 인터페이스는 해제합니다.
* **인터페이스 형식** –이 매개 변수는 클라우드 저장소 트래픽에서 iSCSI 트래픽을 tooisolate 허용 합니다. 이 매개 변수는 hello 다음 중 하나일 수 있습니다.
  
  * **클라우드 사용** -사용 하도록 설정 하면 hello 장치 hello 클라우드와 인터페이스 toocommunicate이를 사용 합니다.
  * **iSCSI 사용** – hello 장치에서 hello iSCSI 호스트와이 인터페이스 toocommunicate 사용할 사용 하도록 설정 합니다.
    
    클라우드 저장소 트래픽에서 iSCSI 트래픽을 격리하는 것이 좋습니다. 또한 참고 경우 호스트 hello 내에서 동일한 서브넷을 장치로 않아도 tooassign 게이트웨이; 그러나 호스트 장치는 다른 서브넷에 있으면 게이트웨이 tooassign을 해야 합니다.
* **IP 주소** – hello 네트워크 인터페이스 중 하나를 구성 하는 경우 가상 IP (VIP)를 구성 해야 합니다. IPv4나 IPv6 또는 둘 다가 될 수 있습니다. Hello 개의 장치 네트워크 인터페이스가 hello IPv4 및 IPv6 주소 모음이 모두 지원 됩니다. IPv4를 사용하는 경우 십진수 표기법으로 32비트 IP 주소(*xxx.xxx.xxx.xxx*)를 지정합니다. IPv6를 사용하는 경우 4자리 접두사를 제공하면 해당 접두사를 기반으로 사용자의 장치 네트워크 인터페이스에 대해 128비트 주소가 자동으로 생성됩니다.
* **서브넷** –이 toohello 서브넷 마스크를 나타내며 hello Windows PowerShell 인터페이스를 통해 구성 됩니다.
* **게이트웨이** –이 hello에 있지 않은 노드와 toocommunicate을 시도할 때이 인터페이스에서 사용 해야 하는 hello 기본 게이트웨이 동일한 IP 주소 공간 (서브넷). hello 기본 게이트웨이 있어야 hello에 같은 주소 공간 (서브넷) hello 인터페이스 IP 주소로 hello 서브넷 마스크를 기준으로 합니다.
* **고정 IP 주소** –이 필드는 DATA 0 hello를 구성 하는 동안에 사용할 수 있는 인터페이스입니다. Tooconnect 업데이트나 hello 장치 문제 해결 등의 작업을 할 수 있습니다 직접 toohello 장치 컨트롤러입니다. 고정 IP 주소는 hello 사용된 tooaccess 수 활성 hello와 장치에서 hello 수동 컨트롤러입니다.

> [!NOTE]
> * tooensure 적절 한 작업이 hello 인터페이스 속도 이중 hello 스위치에 연결 된 각 장치 인터페이스를 확인 합니다. 스위치 인터페이스는 기가비트 이더넷(1000Mbps)과 협상하거나 이에 대해 구성되며 전이중입니다. 더 느린 속도 또는 반이중에서의 인터페이스 운영은 성능 문제를 야기합니다.
> * toominimize 작업 중단과 가동 중지 시간에는 각각 hello 장치의 iSCSI 네트워크 인터페이스 포트에 연결 하는 hello 스위치에서 portfast를 사용 하는 것이 좋습니다. 이렇게 하면 장애 조치의 hello 이벤트에서 네트워크 연결을 신속 하 게 설정할 수 있습니다.

### <a name="configure-data-0"></a>DATA 0 구성

DATA 0은 기본적으로 클라우드가 지원됩니다. 데이터 0을 구성할 때 인 필수 tooconfigure 두 개의 고정된 IP 주소를 각 컨트롤러에 하나씩 있습니다. 고정 IP 주소 이러한 직접 사용 하는 tooaccess hello 장치 컨트롤러를 수 있습니다 및는 hello 장치 또는 문제 해결을 위한 hello 목적 hello 컨트롤러를 액세스 하는 경우에 업데이트를 설치 하는 경우에 유용 합니다.

데이터 0 설정 블레이드에서 hello 통해 IP 컨트롤러 고정 hello를 다시 구성할 수 있습니다.

![네트워크 인터페이스 구성 - DATA 0](./media/storsimple-8000-modify-device-config/modify-network-settings2.png)

> [!NOTE]
> 고정 IP 주소 hello 컨트롤러에 대 한 hello hello 업데이트 toohello 장치를 서비스에 사용 됩니다. 따라서 hello 고정 Ip는 라우팅 가능 하 고 수 tooconnect toohello 인터넷 이어야 합니다.

### <a name="configure-data-1---data-5"></a>DATA 1~DATA 5 구성

1-DATA 5 네트워크 인터페이스가 데이터에 대 한 hello 스크린 샷 뒤에 표시 된 대로 모든 hello 네트워크 설정을 구성할 수 있습니다.

![네트워크 인터페이스 구성 DATA 1~DATA 5](./media/storsimple-8000-modify-device-config/modify-network-settings4.png)


## <a name="swap-or-reassign-ips"></a>IP 교체 또는 재할당

현재, 네트워크 인터페이스에 hello 컨트롤러 할당 된 사용 중인 VIP (hello 하 여 같은 장치 또는 hello 네트워크의 다른 장치), hello 컨트롤러 장애 조치를 실행 합니다. 장치 네트워크 인터페이스의 VIP를 교환하거나 다시 할당하는 경우 중복 IP 상황을 만들 수 있는 만큼 적절한 절차를 따라야 합니다.

다음 단계 tooswap hello 수행 또는 hello 네트워크 인터페이스에 대 한 hello Vip 재할당:

#### <a name="tooreassign-ips"></a>tooreassign Ip

1. 두 인터페이스에 대 한 지우기 hello IP 주소입니다.
2. Hello IP 주소를 지운 후 개별 인터페이스 toohello hello 새 IP 주소 할당 합니다.

## <a name="next-steps"></a>다음 단계

* 너무 방법에 대해 알아봅니다[StorSimple 장치에 대 한 MPIO 구성](storsimple-8000-configure-mpio-windows-server.md)합니다.
* 너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-8000-manager-service-administration.md)합니다.

