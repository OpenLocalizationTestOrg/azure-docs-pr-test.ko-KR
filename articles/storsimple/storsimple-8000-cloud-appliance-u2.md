---
title: "클라우드 Appliance Update 3 aaaStorSimple | Microsoft Docs"
description: "Toocreate, 배포 하 고 Microsoft Azure 가상 네트워크에 StorSimple 클라우드 어플라이언스를 관리 하는 방법에 대해 알아봅니다. (업데이트 3 이상 tooStorSimple 적용 됨)."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/10/2017
ms.author: alkohli
ms.openlocfilehash: ba60a629f1f4b8f0d4566eeb45bae8696f50d0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-a-storsimple-cloud-appliance-in-azure-update-3-and-later"></a>Azure에서 StorSimple Cloud Appliance 배포 및 관리(업데이트 3 이상)

## <a name="overview"></a>개요

hello StorSimple 8000 시리즈 클라우드 어플라이언스는 Microsoft Azure StorSimple 솔루션와 함께 제공 되는 추가 기능입니다. StorSimple 클라우드 어플라이언스에 hello Microsoft Azure 가상 네트워크의 가상 컴퓨터에서 실행 하 고 사용할 수 있습니다를 tooback 및 클론 데이터 호스트의 키를 누릅니다.

이 문서는 hello 단계별 프로세스 toodeploy에 설명 하 고 azure에서 StorSimple 클라우드 어플라이언스를 관리 합니다. 이 문서를 읽고 나면:

* Hello 클라우드 어플라이언스에 hello 물리적 장치에서 어떻게 다른 지 이해 합니다.
* 수 toocreate 수 하 고 hello 클라우드 어플라이언스를 구성 합니다.
* Toohello 클라우드 어플라이언스에 연결 합니다.
* Hello로 toowork 어플라이언스에 클라우드 하는 방법을 알아봅니다.

이 자습서 tooall hello 업데이트 3을 실행 하는 StorSimple 클라우드 어플라이언스에 적용 및 이후 버전입니다.

#### <a name="cloud-appliance-model-comparison"></a>클라우드 어플라이언스 모델 비교

hello StorSimple 클라우드 어플라이언스에 두 가지 모델에서 사용할 수 있는 (이전의 hello 1100) 표준 8010 및 프리미엄 8020 (업데이트 2에서 도입 됨). 다음 표에서 hello hello 두 모델의 비교를 제공 합니다.

| 장치 모델 | 8010<sup>1</sup> | 8020 |
| --- | --- | --- |
| **최대 용량** |30TB |64TB |
| **Azure VM** |Standard_A3(4 코어, 7GB 메모리)| Standard_DS3 (4 코어, 14GB 메모리)|
| **지역 가용성** |모든 Azure 지역 |Premium Storage 및 DS3 Azure VM을 지원하는 Azure 지역<br></br>사용 하 여 [이 목록](https://azure.microsoft.com/regions/services/) toosee 모두 **가상 컴퓨터 > DS 시리즈** 및 **저장소 > 디스크 저장소** 해당 지역에서 사용할 수 있는 합니다. |
| **저장소 유형** |로컬 디스크에 Azure 표준 저장소 사용<br></br> 너무 방법에 대해 알아봅니다[표준 저장소 계정 만들기](../storage/common/storage-create-storage-account.md) |로컬 디스크<sup>2</sup> <br></br>너무 방법에 대해 알아봅니다[프리미엄 저장소 계정 만들기](../storage/common/storage-premium-storage.md) |
| **워크로드 지침** |백업으로부터 항목 수준 파일 읽어오기 |클라우드 개발 및 테스트 시나리오 <br></br>짧은 대기 시간 및 더 높은 성능 워크로드<br></br>재해 복구용 보조 장치 |

<sup>1</sup> *hello 1100 이전의*합니다.

<sup>2</sup> *8020 hello 클라우드 계층 hello 차이 hello hello 장치 내에서 로컬 계층에만 존재에 대 한 Azure 표준 저장소를 사용 하 고 8010 hello 둘 다*합니다.

## <a name="how-hello-cloud-appliance-differs-from-hello-physical-device"></a>Hello 클라우드 어플라이언스에 hello 물리적 장치에서 어떻게 다른 지

hello StorSimple 클라우드 어플라이언스는 Microsoft Azure 가상 컴퓨터의 단일 노드에서 실행 되는 StorSimple의 소프트웨어 전용 버전입니다. hello 클라우드 어플라이언스에 물리적 장치를 사용할 수 없습니다 재해 복구 시나리오를 지원 합니다. hello 클라우드 어플라이언스는 백업, 온-프레미스 재해 복구 및 클라우드 개발 및 테스트 시나리오에서 항목 수준의 검색에 사용 하기에 적합 합니다.

#### <a name="differences-from-hello-physical-device"></a>물리적 장치 hello과의 차이점

hello 다음 표에 StorSimple 클라우드 어플라이언스에 hello 및 hello StorSimple 물리적 장치 간의 몇 가지 주요 차이점이 있습니다.

|  | 물리적 장치 | 클라우드 어플라이언스 |
| --- | --- | --- |
| **위치**: |Hello 데이터 센터에 상주합니다. |Azure에서 실행됩니다. |
| **네트워크 인터페이스** |네트워크 인터페이스가 여섯 개(DATA 0에서 DATA 5까지 ) 있습니다. |네트워크 인터페이스가 하나만(DATA 0) 있습니다. |
| **등록** |Hello 초기 구성 단계 중에 등록 합니다. |등록은 별도의 작업입니다. |
| **서비스 데이터 암호화 키** |Hello 물리적 장치에 다시 생성 하 한 hello 클라우드 어플라이언스에 hello 새 키로 업데이트 합니다. |Hello 클라우드 기기에서 다시 생성할 수 없습니다. |
| **지원되는 볼륨 유형** |로컬로 고정된 볼륨과 계층화된 볼륨을 모두 지원합니다. |계층화된 볼륨만 지원합니다. |

## <a name="prerequisites-for-hello-cloud-appliance"></a>클라우드 어플라이언스에 hello에 대 한 필수 구성 요소

hello 다음 섹션에서는 StorSimple 클라우드 장비에 대 한 hello 구성 필수 구성 요소에 설명 합니다. 클라우드 어플라이언스에 배포 하기 전에 클라우드 장비를 사용 하 여 hello 보안 고려 사항을 검토 합니다.

[!INCLUDE [StorSimple Cloud Appliance security](../../includes/storsimple-8000-cloud-appliance-security.md)]

#### <a name="azure-requirements"></a>Azure 요구 사항

클라우드 어플라이언스에 hello를 프로 비전 하기 전에 toomake hello Azure 환경에서 준비 작업을 수행 해야 합니다.

* 데이터 센터에 StorSimple 8000 시리즈 물리적 장치(8100 또는 8600 모델)가 배포되어 실행되고 있는지 확인합니다. 이 장치를 동일한 StorSimple 장치 관리자 서비스는 hello 레지스터에 대 한 StorSimple 클라우드 어플라이언스에 a toocreate 합니다.
* Hello 클라우드 장비에 대 한 [Azure에서 가상 네트워크 구성](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)합니다. 프리미엄 저장소를 사용하는 경우 프리미엄 저장소를 지원하는 Azure 지역에 가상 네트워크를 만들어야 합니다. hello 프리미엄 저장소 영역은 디스크 저장소 hello에 대 한 toohello 행에 해당 하는 영역 [지역별 Azure 서비스 목록이](https://azure.microsoft.com/regions/services/)합니다.
* DNS 서버 이름을 지정 하는 대신 Azure에서 제공 하는 hello 기본 DNS 서버를 사용 하는 것이 좋습니다. DNS 서버 이름이 올바르지 않거나 hello DNS 서버 수 tooresolve IP 주소를 올바르게를 hello 클라우드 어플라이언스에 hello 만들기 실패 합니다.
* 지점 대 사이트간 및 사이트 대 사이트는 선택적이지만 필수는 아닙니다. 원하는 경우, 고급 시나리오에 대해 이 옵션을 구성할 수 있습니다.
* 만들 수 있습니다 [Azure 가상 컴퓨터](../virtual-machines/virtual-machines-windows-quick-create-portal.md) (호스트 서버) hello 클라우드 어플라이언스에에서 노출 하는 hello 볼륨을 사용할 수 있는 hello 가상 네트워크의 합니다. 이러한 서버 hello 요구 사항을 준수를 충족 해야 합니다.

  * iSCSI 초기자 소프트웨어가 설치된 Windows 또는 Linux VM입니다.
  * Hello에서 실행 되 고 hello 클라우드 장비와 같은 가상 네트워크입니다.
  * 수 tooconnect toohello iSCSI 대상 hello 클라우드 어플라이언스에 hello 내부 IP 주소를 통해 hello 클라우드 어플라이언스에의 수입니다.
  * ISCSI 및 클라우드 트래픽을 hello에 동일에 대 한 지원을 구성 했는지 확인 가상 네트워크입니다.

#### <a name="storsimple-requirements"></a>StorSimple 요구 사항

클라우드 어플라이언스에 만들기 전에 업데이트 tooyour StorSimple 장치 관리자 서비스를 수행 하는 hello를 확인 합니다.

* 추가 [액세스 제어 레코드](storsimple-8000-manage-acrs.md) hello Vm을 클라우드 장비에 대 한 지속적인 toobe hello 호스트 서버에 대 한 합니다.
* 사용 하 여 한 [저장소 계정](storsimple-8000-manage-storage-accounts.md#add-a-storage-account) hello에 hello 클라우드 장비와 같은 지역입니다. 다른 영역의 저장소 계정으로 성능이 저하될 수 있습니다. Hello 클라우드 기기와 표준 또는 프리미엄 저장소 계정을 사용할 수 있습니다. 방법에 대 한 자세한 내용은 toocreate는 [표준 저장소 계정이](../storage/common/storage-create-storage-account.md) 또는 [프리미엄 저장소 계정](../storage/common/storage-premium-storage.md)
* 사용자의 데이터에 사용 되는 hello에서는 클라우드 어플라이언스에 만들 다른 저장소 계정을 사용 합니다. Hello 동일한 저장소 계정을 성능이 저하 될 수 있습니다를 사용 합니다.

시작 하기 전에 정보 다음 hello 했는지 확인 합니다.

* 액세스 자격 증명이 있는 Azure Portal 계정
* Hello 물리적 장치의 서비스 데이터 암호화 키의 복사본 toohello StorSimple 장치 관리자 서비스를 등록 합니다.

## <a name="create-and-configure-hello-cloud-appliance"></a>만들기 및 hello 클라우드 어플라이언스를 구성 합니다.

이러한 절차를 수행 하기 전에 hello가 충족 되는지 확인 [hello 클라우드 장비에 대 한 필수 구성 요소](#prerequisites-for-the-cloud-appliance)합니다.

Hello 단계 toocreate StorSimple 클라우드 어플라이언스에 다음을 수행 합니다.

### <a name="step-1-create-a-cloud-appliance"></a>1단계: 클라우드 어플라이언스 만들기

Hello 단계 toocreate hello StorSimple 클라우드 어플라이언스에 다음을 수행 합니다.

[!INCLUDE [Create a cloud appliance](../../includes/storsimple-8000-create-cloud-appliance-u2.md)]

이 단계에서는 hello 클라우드 어플라이언스에의 hello 만들기에 실패 하면 인터넷 연결 toohello가 없을 수 있습니다. 자세한 내용은 이동 너무[인터넷 연결 오류 문제를 해결](#troubleshoot-internet-connectivity-errors) 클라우드 장비를 만들 때.

### <a name="step-2-configure-and-register-hello-cloud-appliance"></a>2 단계: 구성 및 hello 클라우드 장비를 등록 합니다.

이 절차를 시작 하기 전에 hello 서비스 데이터 암호화 키의 복사본을가지고 있는지 확인 합니다. hello 서비스 데이터 암호화 키는 StorSimple 장치 관리자 서비스 hello를 첫 번째 StorSimple 물리적 장치를 등록할 때 생성 됩니다. 지시 toosave 된 안전한 위치에 해당 합니다. Hello 서비스 데이터 암호화 키의 복사본이 없는 경우 지원에 대 한 Microsoft 지원에 문의 해야 있습니다.

Hello 단계 tooconfigure 다음을 수행 하 고 StorSimple 클라우드 장비를 등록 합니다.

[!INCLUDE [Configure and register a cloud appliance](../../includes/storsimple-8000-configure-register-cloud-appliance.md)]

### <a name="step-3-optional-modify-hello-device-configuration-settings"></a>3 단계: (선택 사항) hello 장치 구성 설정 수정

hello 다음 섹션에서는 설명 hello 장치 구성 설정 toouse CHAP를 StorSimple 스냅숏 관리자 하거나 hello 장치 관리자 암호를 변경 하는 경우에 StorSimple 클라우드 어플라이언스에 hello에 대 한 필요 합니다.

#### <a name="configure-hello-chap-initiator"></a>Hello CHAP 시작자 구성

이 매개 변수는 (대상) 하 여 클라우드 어플라이언스에 tooaccess hello 볼륨을 시도 하는 hello 초기자 (서버)에서 예상 하는 hello 자격 증명을 포함 합니다. hello 초기자 CHAP 사용자 이름 및 CHAP 암호 tooidentify 자체 tooyour 장치를 제공 이러한 인증 중입니다. 자세한 단계에 대 한 이동 너무[장치에 대 한 CHAP 구성](storsimple-8000-configure-chap.md#unidirectional-or-one-way-authentication)합니다.

#### <a name="configure-hello-chap-target"></a>Hello CHAP 대상 구성

이 매개 변수는 클라우드 어플라이언스에 CHAP 지원 시작 자가 상호 또는 양방향 인증을 요청할 때 사용 하는 hello 자격 증명을 포함 합니다. 클라우드 어플라이언스에 역방향 CHAP 사용자 이름 및 자체 역방향 CHAP 암호 tooidentify toohello 초기자가 인증 프로세스 동안 사용 됩니다.

> [!NOTE]
> CHAP 대상 설정은 전역 설정입니다. 이러한 설정을 적용 하는 경우 모든 hello 볼륨 연결 toohello 클라우드 어플라이언스에 CHAP 인증 사용.

자세한 단계에 대 한 이동 너무[장치에 대 한 CHAP 구성](storsimple-8000-configure-chap.md#bidirectional-or-mutual-authentication)합니다.

#### <a name="configure-hello-storsimple-snapshot-manager-password"></a>Hello StorSimple 스냅숏 관리자 암호 구성

StorSimple 스냅숏 관리자 소프트웨어는 Windows 호스트에 상주 하며 관리자 hello 형태의 로컬 및 클라우드 스냅숏 StorSimple 장치의 toomanage 백업을 허용 합니다.

> [!NOTE]
> Hello 클라우드 장비에 대 한 Windows 호스트가 Azure 가상 컴퓨터입니다.

Hello StorSimple 스냅숏 관리자에서에서 장치를 구성할 때는 메시지가 tooprovide hello StorSimple 장치 IP 주소와 암호 tooauthenticate 저장 장치입니다. 자세한 단계에 대 한 이동 너무[구성 StorSimple 스냅숏 관리자 암호](storsimple-8000-change-passwords.md#set-the-storsimple-snapshot-manager-password)합니다.

#### <a name="change-hello-device-administrator-password"></a>Hello 장치 관리자 암호 변경

사용 하는 경우 Windows PowerShell 인터페이스 tooaccess hello hello 클라우드 어플라이언스에, 필요한 tooenter 장치 관리자 암호는 합니다. 데이터의 hello 보안을 위해 클라우드 어플라이언스에 hello를 사용 하려면 먼저이 암호를 변경 해야 합니다. 자세한 단계에 대 한 이동 너무[구성 장치 관리자 암호](../storsimple/storsimple-8000-change-passwords.md#change-the-device-administrator-password)합니다.

## <a name="connect-remotely-toohello-cloud-appliance"></a>Toohello 클라우드 장비를 원격으로 연결

원격 액세스 tooyour 클라우드 어플라이언스에 hello Windows PowerShell 인터페이스를 통해 기본적으로 사용 되지 않습니다. Hello 클라우드 어플라이언스에 원격 관리를 먼저 활성화 해야 하 고 tooaccess hello 클라우드 어플라이언스에 사용 클라이언트 hello에 키를 누릅니다.

2 단계 절차를 수행 하는 hello 설명 방법을 tooconnect 원격으로 tooyour 클라우드 어플라이언스에 합니다.

### <a name="step-1-configure-remote-management"></a>1단계: 원격 관리 구성

Hello 단계 tooconfigure StorSimple 클라우드 장비에 대 한 원격 관리를 다음을 수행 합니다.

[!INCLUDE [Configure remote management via HTTP for cloud appliance](../../includes/storsimple-8000-configure-remote-management-http-device.md)]

### <a name="step-2-remotely-access-hello-cloud-appliance"></a>Hello 클라우드 장비를 원격으로 액세스 하는 2 단계:

Hello 내의 다른 가상 컴퓨터에서 Windows PowerShell remoting tooconnect toohello 어플라이언스를 사용 하 여 hello 클라우드 어플라이언스에 원격 관리를 활성화 한 후 동일한 가상 네트워크입니다. 예를 들어 hello 호스트 구성 하 고 tooconnect iSCSI를 사용 하는 VM에서에서 연결할 수 있습니다. 대부분의 배포에서는 공용 끝점 tooaccess hello 클라우드 어플라이언스에 액세스 하기 위해 사용할 수 있는 VM 호스트를 열 됩니다.

> [!WARNING]
> **보안 향상된을 위해이 toohello 끝점을 연결할 때 HTTPS를 사용 하 고 PowerShell 원격 세션을 완료 한 후 hello 끝점을 삭제 합니다.**

hello 절차를 수행 해야 [tooyour StorSimple 장치를 원격으로 연결](storsimple-8000-remote-connect.md) tooset 클라우드 장비에 대 한 원격을 합니다.

## <a name="connect-directly-toohello-cloud-appliance"></a>Toohello 클라우드 어플라이언스에 직접 연결

연결할 수도 있습니다 직접 toohello 클라우드 어플라이언스에 합니다. tooconnect toohello 클라우드 어플라이언스에 외부의 다른 컴퓨터에서 직접 hello 가상 네트워크 또는 외부 hello Microsoft Azure 환경, 추가 끝점을 만들어야 합니다.

Hello 단계 toocreate hello 클라우드 어플라이언스에 공용 끝점을 다음을 수행 합니다.

[!INCLUDE [Create public endpoints on a cloud appliance](../../includes/storsimple-8000-create-public-endpoints-cloud-appliance.md)]

연결 좋습니다 hello 내의 다른 가상 컴퓨터에서 동일한 가상 네트워크 hello 가상 네트워크에서 공용 끝점 수를 최소화 하는이 연습에 합니다. 이 경우 원격 데스크톱 세션을 통해 toohello 가상 컴퓨터를 연결 하 고 로컬 네트워크에 있는 다른 모든 Windows 클라이언트와 마찬가지로 사용 하기 위해 해당 가상 컴퓨터를 구성 합니다. Hello 포트는 이미 알려져 있으므로 tooappend hello 공용 포트 번호를 않아도 됩니다.

## <a name="work-with-hello-storsimple-cloud-appliance"></a>StorSimple 클라우드 어플라이언스에 hello 사용

생성 하 고 StorSimple 클라우드 어플라이언스에 hello 구성 작업을 준비 toostart 됩니다. 물리적 StorSimple 장치에서처럼 클라우드 어플라이언스에 볼륨 컨테이너, 볼륨 및 백업 정책으로 작업할 수 있습니다. hello 유일한 차이점은 해야 toomake hello 클라우드 어플라이언스에 장치 목록에서 선택 해야 합니다. 너무 참조[hello StorSimple 장치 관리자 서비스 toomanage 클라우드 장비를 사용 하 여](storsimple-8000-manager-service-administration.md) hello hello 클라우드 장비에 대 한 다양 한 관리 작업의 단계별 절차에 대 한 합니다.

hello 다음 섹션에서는 설명의 몇 가지 hello 차이점 hello 클라우드 어플라이언스에 작업할 때 발생 합니다.

### <a name="maintain-a-storsimple-cloud-appliance"></a>StorSimple Cloud Appliance 유지 관리

소프트웨어 전용 장치 이므로 hello 클라우드 장비에 대 한 유지 관리는 최소한의 경우 toomaintenance hello 물리적 장치에 대 한 비교 합니다.

클라우드 어플라이언스를 업데이트할 수 없습니다. Hello 소프트웨어 toocreate 새로운 클라우드 어플라이언스의 최신 버전을 사용 합니다.


### <a name="storage-accounts-for-a-cloud-appliance"></a>클라우드 어플라이언스에 대한 저장소 계정

StorSimple 장치 관리자 서비스 hello, hello 클라우드 어플라이언스에 및 hello 실제 장치에서 사용 하기 위해 저장소 계정은 만듭니다. 저장소 계정을 만들 때 hello 이름에 지역 식별자를 사용 하는 것이 좋습니다. 이렇게 하면 해당 hello 지역 hello 시스템 구성 요소를 모두 전체 일관 됩니다. 클라우드 어플라이언스에 것이 중요 hello에서 모든 hello 구성 요소가 같은 지역 tooprevent 성능 문제.

단계별 절차에 대 한 이동 너무[저장소 계정 추가](storsimple-8000-manage-storage-accounts.md#add-a-storage-account)합니다.

### <a name="deactivate-a-storsimple-cloud-appliance"></a>StorSimple Cloud Appliance 비활성화

클라우드 어플라이언스에 비활성화 하면 hello 작업 hello VM 및 프로 비전 된 경우 생성 된 hello 리소스를 삭제 합니다. 일 수 없습니다 hello 클라우드 어플라이언스에 비활성화 된 후 tooits 이전 상태로 복원 합니다. Hello 클라우드 어플라이언스에 비활성화 하기 전에 toostop 있는지 확인 하거나 클라이언트와 의존 하는 호스트를 삭제 합니다.

작업을 수행 하는 hello 결과 클라우드 어플라이언스에 비활성화 됩니다.

* hello 클라우드 어플라이언스에 제거 됩니다.
* hello OS 디스크 및 만든 클라우드 어플라이언스에 hello에 대 한 데이터 디스크 제거 됩니다.
* hello 호스팅된 서비스 및 가상 네트워크를 구축 하는 동안 만든 유지 됩니다. 사용하지 않는 경우 수동으로 삭제해야 합니다.
* 클라우드 어플라이언스에 hello에 대 한 만든 클라우드 스냅숏은 유지 됩니다.

단계별 절차에 대 한 이동 너무[비활성화 StorSimple 장치를 삭제 하 고](storsimple-8000-deactivate-and-delete-device.md)합니다.

Hello에 대 한 장치 목록에서 hello 클라우드 어플라이언스에 hello 클라우드 어플라이언스에 hello StorSimple 장치 관리자 서비스 블레이드 비활성화 된 것으로 표시 되는 즉시 삭제할 수 있습니다 **장치** 블레이드입니다.

### <a name="start-stop-and-restart-a-cloud-appliance"></a>클라우드 어플라이언스 시작, 중지 및 다시 시작
Hello StorSimple 물리적 장치를 달리 전원이 on 또는 off StorSimple 클라우드 어플라이언스에 단추 toopush 전원 합니다. 그러나 toostop 필요 하 고 클라우드 어플라이언스에 hello를 다시 시작 하는 경우가 있을 수 있습니다.

toostart 있습니다, 중지 및 다시 시작 하는 클라우드 어플라이언스 hello 가장 쉬운 방법은 가상 컴퓨터 서비스 블레이드 hello를 통해입니다. Hello 가상 컴퓨터 서비스를 이동 합니다. Vm의 hello 목록에서 hello VM 해당 tooyour 클라우드 어플라이언스에 (동일한 이름)을 식별 하 고 hello VM 이름을 클릭 합니다. Hello 클라우드 어플라이언스에 상태는 가상 컴퓨터 블레이드를 볼 때 **실행** 를 만든 후 기본적으로 시작 됩니다. 언제든지 가상 컴퓨터를 시작하고 중지하고 다시 시작할 수 있습니다.

[!INCLUDE [Stop and restart cloud appliance](../../includes/storsimple-8000-stop-restart-cloud-appliance.md)]

### <a name="reset-toofactory-defaults"></a>Toofactory 기본값 다시 설정
되도록 toostart을 통해 클라우드 기기와 결정 한 경우 비활성화 및 삭제 한 다음 새 구성표를 만들어야 합니다.

## <a name="fail-over-toohello-cloud-appliance"></a>장애 조치 toohello 클라우드 어플라이언스에
DR (재해 복구)는 하나의 hello StorSimple 클라우드 어플라이언스에 hello 주요 시나리오에 대 한 설계 되었습니다. 이 시나리오에서는 물리적 StorSimple 장치 hello 또는 전체 데이터 센터를 사용할 수 없습니다. 다행히 대체 위치에 클라우드 어플라이언스에 toorestore 작업을 사용할 수 있습니다. DR 동안 hello hello 원본 장치의 볼륨 컨테이너는 소유권이 변경 되며 전송된 toohello 클라우드 어플라이언스에 됩니다.

DR의 필요 조건 hello 됩니다.

* hello 클라우드 어플라이언스에 만들어지고 구성 됩니다.
* Hello 볼륨 컨테이너 내의 모든 hello 볼륨은 오프 라인 상태입니다.
* 장애 조치 hello 볼륨 컨테이너에 연결 된 클라우드 스냅숏이 있습니다.

> [!NOTE]
> * 클라우드 어플라이언스에 hello 보조 장치로 dr을 사용할 경우 hello 8010 표준 저장소 30TB 개이고 8020 64TB의 프리미엄 저장소에 염두에 둬야 합니다. hello 더 높은 용량 8020 클라우드 어플라이언스에 DR 시나리오에 적합 한 더 수 있습니다.

단계별 절차에 대 한 이동 너무[tooa 클라우드 어플라이언스에 장애 조치할](storsimple-8000-device-failover-cloud-appliance.md)합니다.

## <a name="delete-hello-cloud-appliance"></a>Hello 클라우드 어플라이언스에 삭제
이전에 구성 하 고 사용 StorSimple 클라우드 어플라이언스에 하지만 이제 toostop의 사용에 대 한 계산 요금 발생 이벤트를 시킬 hello 클라우드 어플라이언스에 중지 해야 합니다. 중지 hello 클라우드 어플라이언스에 hello VM의 할당을 취소 합니다. 이 작업은 구독에서 요금이 발생되지 않도록 합니다. 그러나 OS hello에 대 한 저장소 비용은 hello 및 데이터 디스크 계속 됩니다.

모든 hello toostop 요금 hello 클라우드 어플라이언스에 삭제 해야 합니다. hello 클라우드 어플라이언스에에서 생성 된 toodelete hello 백업을 비활성화 하거나 삭제할 수 있습니다 hello 장치입니다. 자세한 내용은 [StorSimple 장치 비활성화 및 삭제](storsimple-8000-deactivate-and-delete-device.md)를 참조하세요.

[!INCLUDE [Delete a cloud appliance](../../includes/storsimple-8000-delete-cloud-appliance.md)]

## <a name="troubleshoot-internet-connectivity-errors"></a>인터넷 연결 오류 문제 해결
클라우드 어플라이언스에 hello 만드는 동안 연결 toohello 인터넷에 없는 경우 hello 생성 단계 실패 합니다. tootroubleshoot 인터넷 연결 실패 hello hello Azure 포털의에서 단계를 수행 합니다.

1. [Azure에서 Windows Server 2012 가상 컴퓨터를 만듭니다](/articles/virtual-machines/windows/quick-create-portal.md). 이 가상 컴퓨터가 사용 하도록 hello 동일한 저장소 계정, VNet 및 클라우드 어플라이언스에에서 사용 되는 서브넷입니다. Windows Server 호스트에서 사용 하 여 Azure hello 동일한 저장소 계정, VNet 및 서브넷을 기존 선택한 경우 있습니다 사용할 수도 tootroubleshoot hello 인터넷에 연결 합니다.
2. Hello 앞 단계에서에서 만든 hello 가상 컴퓨터에 원격 로그인입니다.
3. Hello 가상 컴퓨터 내의 명령 창을 엽니다 (Win + R을 입력 한 후 `cmd`).
4. Hello cmd hello 프롬프트에서 다음을 실행 합니다.

    `nslookup windows.net`
5. 경우 `nslookup` 실패 하는 hello 클라우드 어플라이언스에 toohello StorSimple 장치 관리자 서비스를 등록 하는 중에서 때문에 인터넷 연결이 실패 합니다.
6. 변경 hello 필요한 클라우드 어플라이언스에 hello tooyour 가상 네트워크 tooensure은 수 tooaccess Azure 사이트와 같은 _windows.net_합니다.

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[hello StorSimple 장치 관리자 서비스 toomanage 클라우드 장비를 사용 하 여](storsimple-8000-manager-service-administration.md)합니다.
* 너무 방법을 이해[백업 세트에서 StorSimple 볼륨을 복원](storsimple-8000-restore-from-backup-set-u2.md)합니다.
