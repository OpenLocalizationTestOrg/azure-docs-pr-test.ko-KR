---
title: "가상 장치 업데이트 2를 aaaStorSimple | Microsoft Docs"
description: "Toocreate, 배포 하 고 Microsoft Azure 가상 네트워크에 StorSimple 가상 장치를 관리 하는 방법에 대해 알아봅니다. (업데이트 2 tooStorSimple 적용 됨)."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: f37752a5-cd0c-479b-bef2-ac2c724bcc37
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: alkohli
ms.openlocfilehash: 8d2a0520f1ed30ebec929c2bdabb4838691b8ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-a-storsimple-virtual-device-in-azure"></a>Azure에서 StorSimple 가상 장치 배포 및 관리
## <a name="overview"></a>개요
hello StorSimple 8000 시리즈 가상 장치는 Microsoft Azure StorSimple 솔루션와 함께 제공 되는 추가 기능입니다. hello StorSimple 가상 장치는 Microsoft Azure 가상 네트워크의 가상 컴퓨터에서 실행 하 고 사용할 수 있습니다를 tooback 및 클론 데이터 호스트의 키를 누릅니다. 이 자습서에서는 설명 방법을 toodeploy Azure에서 가상 장치를 관리 하 고 적용 가능한 tooall 2 미만과 소프트웨어 버전 업데이트를 실행 하는 hello 가상 장치는 합니다.

#### <a name="virtual-device-model-comparison"></a>가상 장치 모델 비교
StorSimple 가상 장치는 두 가지 모델에서 사용할 수 있는 (이전의 hello 1100) 표준 8010 hello 및 프리미엄 8020 (업데이트 2에서 도입 됨). Hello 두 모델의 비교는 아래 표 형식으로 표시 합니다.

| 장치 모델 | 8010<sup>1</sup> | 8020 |
| --- | --- | --- |
| **최대 용량** |30TB |64TB |
| **Azure VM** |Standard_A3(4 코어, 7GB 메모리) |Standard_DS3 (4 코어, 14GB 메모리) |
| **버전 호환성** |사전 업데이트 2 이상을 실행하는 버전 |업데이트 2 이상을 실행하는 버전 |
| **지역 가용성** |모든 Azure 지역 |Premium Storage 및 DS3 Azure VM을 지원하는 모든 Azure 지역<br></br> 사용 하 여 [이 목록](https://azure.microsoft.com/en-us/regions/services) toosee 모두 *가상 컴퓨터 > DS 시리즈* 및 *저장소 > 디스크 저장소* 해당 지역에서 사용할 수 있는 합니다. |
| **저장소 유형** |로컬 디스크에 Azure 표준 저장소 사용<br></br> 너무 방법에 대해 알아봅니다[표준 저장소 계정 만들기](../storage/common/storage-create-storage-account.md) |로컬 디스크<sup>2</sup> <br></br>너무 방법에 대해 알아봅니다[프리미엄 저장소 계정 만들기](../storage/common/storage-premium-storage.md) |
| **워크로드 지침** |백업으로부터 항목 수준 파일 읽어오기 |클라우드 개발 및 테스트 시나리오, 짧은 대기 시간, 높은 성능 워크로드  <br></br>재해 복구용 보조 장치 |

<sup>1</sup> *hello 1100 이전의*합니다.

<sup>2</sup> *8020 hello 클라우드 계층 hello 차이 hello hello 장치 내에서 로컬 계층에만 존재에 대 한 Azure 표준 저장소를 사용 하 고 8010 hello 둘 다*합니다.

이 문서에서는 hello azure에서 StorSimple 가상 장치 배포의 단계별 프로세스를 설명 합니다. 이 문서를 읽고 나면:

* 가상 장치 hello hello 물리적 장치에서 어떻게 다른 지 이해 합니다.
* 수 toocreate 수 하 고 hello 가상 장치를 구성 합니다.
* Toohello 가상 장치를 연결 합니다.
* 자세한 방법을 toowork hello 가상 장치를 포함 합니다.

이 자습서는 tooall hello StorSimple 가상 장치 2 이상은 업데이트 실행을 적용 합니다.

## <a name="how-hello-virtual-device-differs-from-hello-physical-device"></a>가상 장치 hello hello 물리적 장치에서 어떻게 다른 지
hello StorSimple 가상 장치는 Microsoft Azure 가상 컴퓨터의 단일 노드에서 실행 되는 StorSimple의 소프트웨어 전용 버전. hello 가상 장치 재해 복구 시나리오를 지원 물리적 장치를 사용할 수 없으면 및 백업에서 항목 수준의 검색에 사용 하기에 적합 온-프레미스 재해 복구 및 클라우드 개발 및 시나리오를 테스트 합니다.

#### <a name="differences-from-hello-physical-device"></a>물리적 장치 hello과의 차이점
hello 다음 표에 hello StorSimple 가상 장치 하 고 hello StorSimple 물리적 장치 간의 몇 가지 주요 차이점이 있습니다.

|  | 물리적 장치 | 가상 장치 |
| --- | --- | --- |
| **위치**: |Hello 데이터 센터에 상주합니다. |Azure에서 실행됩니다. |
| **네트워크 인터페이스** |네트워크 인터페이스가 여섯 개(DATA 0에서 DATA 5까지 ) 있습니다. |네트워크 인터페이스가 하나만(DATA 0) 있습니다. |
| **등록** |Hello 구성 단계 중에 등록 합니다. |등록은 별도의 작업입니다. |
| **서비스 데이터 암호화 키** |Hello 물리적 장치에 다시 생성 하 한 hello 새 키로 hello 가상 장치를 업데이트 합니다. |Hello 가상 장치에서 다시 생성할 수 없습니다. |

## <a name="prerequisites-for-hello-virtual-device"></a>Hello 가상 장치에 대 한 필수 구성 요소
hello 다음 섹션에 설명 StorSimple 가상 장치에 대 한 hello 구성 필수 구성 요소입니다. 이전 toodeploying 가상 장치 검토 hello [가상 장치를 사용 하기 위한 보안 고려 사항](storsimple-security.md#storsimple-virtual-device-security)합니다.

#### <a name="azure-requirements"></a>Azure 요구 사항
Hello 가상 장치를 프로 비전 하기 전에 toomake hello Azure 환경에서 준비 작업을 수행 해야 합니다.

* Hello 가상 장치용 [Azure에서 가상 네트워크 구성](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)합니다. 프리미엄 저장소를 사용하는 경우 프리미엄 저장소를 지원하는 Azure 지역에 가상 네트워크를 만들어야 합니다. hello 프리미엄 저장소 영역은 toohello 행에 대 한에 해당 하는 영역 *디스크 저장소* hello 목록에 [지역별 Azure 서비스](https://azure.microsoft.com/en-us/regions/services)합니다.
* DNS 서버 이름을 지정 하는 대신 Azure에서 제공 하는 권장 toouse hello 기본 DNS 서버는 DNS 서버 이름이 올바르지 않습니다. 또는 hello DNS 서버 수 tooresolve IP 주소를 올바르게를 hello 가상 장치의 hello 생성 되지 것입니다.
* 지점 대 사이트간 및 사이트 대 사이트는 선택적이지만 필수는 아닙니다. 원하는 경우, 고급 시나리오에 대해 이 옵션을 구성할 수 있습니다.
* 만들 수 있습니다 [Azure 가상 컴퓨터](../virtual-machines/virtual-machines-linux-about.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (호스트 서버) hello 가상 장치에 의해 노출 되는 hello 볼륨을 사용할 수 있는 hello 가상 네트워크의 합니다. 이러한 서버 hello 요구 사항을 준수를 충족 해야 합니다.                             

  * iSCSI 초기자 소프트웨어가 설치된 Windows 또는 Linux VM입니다.
  * Hello에서 실행 되 고 hello 가상 장치와 동일한 가상 네트워크입니다.
  * Hello 가상 장치의 hello 내부 IP 주소를 통해 hello 가상 장치의 수 tooconnect toohello iSCSI 대상 수 있습니다.
* ISCSI 및 클라우드 트래픽을 hello에 동일에 대 한 지원을 구성 했는지 확인 가상 네트워크입니다.

#### <a name="storsimple-requirements"></a>StorSimple 요구 사항
가상 장치를 만들기 전에 업데이트 tooyour Azure StorSimple 서비스를 수행 하는 hello를 확인 합니다.

* 추가 [액세스 제어 레코드](storsimple-manage-acrs.md) hello 가상 장치에 대 한 복구 클라이드 toobe Vm에 대 한 합니다.
* 사용 하 여 한 [저장소 계정](storsimple-manage-storage-accounts.md#add-a-storage-account) hello에 hello 가상 장치를 사용 하 여 동일한 지역입니다. 다른 영역의 저장소 계정으로 성능이 저하될 수 있습니다. Hello 가상 장치에는 표준 또는 프리미엄 저장소 계정을 사용할 수 있습니다. 방법에 대 한 자세한 내용은 toocreate는 [표준 저장소 계정이](../storage/common/storage-create-storage-account.md) 또는 [프리미엄 저장소 계정](../storage/common/storage-premium-storage.md)
* 사용자의 데이터에 사용 되는 hello에서 가상 장치 생성을 위한 다른 저장소 계정을 사용 합니다. Hello 동일한 저장소 계정을 성능이 저하 될 수 있습니다를 사용 합니다.

시작 하기 전에 정보 다음 hello 했는지 확인 합니다.

* 액세스 자격 증명이 있는 Azure 클래식 포털 계정
* Hello 물리적 장치의 서비스 데이터 암호화 키의 복사본입니다.

## <a name="create-and-configure-hello-virtual-device"></a>만들기 및 hello 가상 장치를 구성 합니다.
이러한 절차를 수행 하기 전에 hello가 충족 되는지 확인 [hello 가상 장치에 대 한 필수 구성 요소](#prerequisites-for-the-virtual-device)합니다.

가상 네트워크를 만든, StorSimple Manager 서비스를 구성 하 고 hello 서비스와 물리적 StorSimple 장치를 등록 한, 후 다음 단계 toocreate hello를 사용 하 여 구성 하는 StorSimple 가상 장치입니다.

### <a name="step-1-create-a-virtual-device"></a>1단계: 가상 장치 만들기
Hello 단계 toocreate hello StorSimple 가상 장치를 다음을 수행 합니다.

[!INCLUDE [Create a virtual device](../../includes/storsimple-create-virtual-device-u2.md)]

이 단계에서는 hello 가상 장치의 hello 만들기에 실패 하면 인터넷 연결 toohello가 없을 수 있습니다. 자세한 내용은 이동 너무[인터넷 연결 오류 문제를 해결](#troubleshoot-internet-connectivity-errors) 가상 장치를 만들 때.

### <a name="step-2-configure-and-register-hello-virtual-device"></a>2 단계: 구성 및 hello 가상 장치를 등록 합니다.
이 절차를 시작 하기 전에 hello 서비스 데이터 암호화 키의 복사본을가지고 있는지 확인 합니다. hello 서비스 데이터 암호화 키를 만든 첫 번째 StorSimple 장치를 구성 하 고 지시 toosave 된 경우 안전한 위치에 해당 합니다. Hello 서비스 데이터 암호화 키의 복사본이 없는 경우 지원에 대 한 Microsoft 지원에 문의 해야 있습니다.

Hello 단계 tooconfigure 다음을 수행 하 고 StorSimple 가상 장치를 등록 합니다.

[!INCLUDE [Configure and register a virtual device](../../includes/storsimple-configure-register-virtual-device.md)]

### <a name="step-3-optional-modify-hello-device-configuration-settings"></a>3 단계: (선택 사항) hello 장치 구성 설정 수정
hello 다음 섹션에서는 설명 hello 장치 관리자 암호를 변경 하거나 toouse CHAP를 StorSimple 스냅숏 관리자를 사용할 경우 hello StorSimple 가상 장치에 필요한 hello 장치 구성 설정입니다.

#### <a name="configure-hello-chap-initiator"></a>Hello CHAP 시작자 구성
이 매개 변수에 tooaccess hello 볼륨을 시도 하는 hello 초기자 (서버)에서 가상 장치 (대상)으로 예상 하는 hello 자격 증명을 포함 합니다. hello 초기자는 CHAP 사용자 이름 및 CHAP 암호 tooidentify 자체 tooyour 장치 제공 이러한 인증 중. 자세한 단계에 대 한 이동 너무[장치에 대 한 CHAP 구성](storsimple-configure-chap.md#unidirectional-or-one-way-authentication)합니다.

#### <a name="configure-hello-chap-target"></a>Hello CHAP 대상 구성
이 매개 변수는 CHAP 지원 시작 자가 상호 또는 양방향 인증을 요청할 때 가상 장치를 사용 하는 hello 자격 증명을 포함 합니다. 가상 장치에서 사용할 역방향 CHAP 사용자 이름 및 자체 역방향 CHAP 암호 tooidentify toohello 초기자가 인증 프로세스 중입니다. CHAP 대상 설정은 전역 설정입니다. 이러한 설정이 적용 되는 경우 모든 hello 볼륨 연결 된 toohello 저장소 가상 장치에 CHAP 인증이 사용 됩니다. 자세한 단계에 대 한 이동 너무[장치에 대 한 CHAP 구성](storsimple-configure-chap.md#bidirectional-or-mutual-authentication)합니다.

#### <a name="configure-hello-storsimple-snapshot-manager-password"></a>Hello StorSimple 스냅숏 관리자 암호 구성
StorSimple 스냅숏 관리자 소프트웨어는 Windows 호스트에 상주 하며 관리자 hello 형태의 로컬 및 클라우드 스냅숏 StorSimple 장치의 toomanage 백업을 허용 합니다.

> [!NOTE]
> Hello 가상 장치에 대 한 Windows 호스트가 Azure 가상 컴퓨터입니다.
>
>

Hello StorSimple 스냅숏 관리자에서에서 장치를 구성할 때 메시지가 표시 됩니다 tooprovide hello StorSimple 장치 IP 주소와 암호 tooauthenticate 저장 장치입니다. 자세한 단계에 대 한 이동 너무[구성 StorSimple 스냅숏 관리자 암호](storsimple-change-passwords.md#change-the-storsimple-snapshot-manager-password)합니다.

#### <a name="change-hello-device-administrator-password"></a>Hello 장치 관리자 암호 변경
사용 하는 경우 Windows PowerShell 인터페이스 tooaccess hello hello 가상 장치, 필요한 tooenter 장치 관리자 암호를 사용할 수 있습니다. 데이터의 hello 보안, 사용자가 필요한 toochange 하기 전에이 암호 hello 가상 장치를 사용할 수 있습니다. 자세한 단계에 대 한 이동 너무[구성 장치 관리자 암호](storsimple-change-passwords.md#change-the-device-administrator-password)합니다.

## <a name="connect-remotely-toohello-virtual-device"></a>Toohello 가상 장치를 원격으로 연결
원격 액세스 tooyour hello Windows PowerShell 인터페이스를 통해 가상 장치는 기본적으로 사용 되지 않습니다. 하면 tooenable hello 가상 장치에서 원격 관리를 먼저, 필요한 한 후 다시 사용 되는 tooaccess 될 hello 클라이언트에 가상 장치입니다.

원격으로 hello 2 단계 프로세스 tooconnect 다음과 같습니다.

### <a name="step-1-configure-remote-management"></a>1단계: 원격 관리 구성
StorSimple 가상 장치에 대 한 단계 tooconfigure 원격 관리를 수행 하는 hello를 수행 합니다.

[!INCLUDE [Configure remote management via HTTP for virtual device](../../includes/storsimple-configure-remote-management-http-device.md)]

### <a name="step-2-remotely-access-hello-virtual-device"></a>2 단계: hello 가상 장치를 원격으로 액세스
Windows PowerShell remoting tooconnect toohello에서에서 가상 장치의 hello 내의 다른 가상 컴퓨터를 사용할 수 hello StorSimple 장치 구성 페이지에서 원격 관리를 사용 하도록 설정한 후 동일한 가상 네트워크입니다. 예를 들어 hello 호스트 구성 하 고 tooconnect iSCSI를 사용 하는 VM에서에서 연결할 수 있습니다. 대부분의 배포에서 하면 이미 연 공용 끝점 tooaccess hello 가상 장치에 액세스 하기 위해 사용할 수 있는 VM 호스트 합니다.

> [!WARNING]
> **보안 향상된을 위해이 toohello 끝점을 연결할 때 HTTPS를 사용 하 고 PowerShell 원격 세션을 완료 한 후 hello 끝점을 삭제 합니다.**
>
>

절차에서는 hello 따라야 [tooyour StorSimple 장치를 원격으로 연결](storsimple-remote-connect.md) tooset 가상 장치에 대 한 원격을 합니다.

## <a name="connect-directly-toohello-virtual-device"></a>Toohello 가상 장치에 직접 연결
연결할 수도 있습니다 직접 toohello 가상 장치입니다. Tooconnect hello 절차 다음에 설명 된 대로 toocreate 추가 끝점을 필요한 toohello hello 가상 네트워크 또는 외부 hello Microsoft Azure 환경 외부의 다른 컴퓨터에서 가상 장치를 직접 선택 합니다.

Hello 단계 toocreate 공용 끝점 hello 가상 장치에서 다음을 수행 합니다.

[!INCLUDE [Create public endpoints on a virtual device](../../includes/storsimple-create-public-endpoints-virtual-device.md)]

연결 좋습니다 hello 내의 다른 가상 컴퓨터에서 동일한 가상 네트워크 hello 가상 네트워크에서 공용 끝점 수를 최소화 하는이 연습에 합니다. 이 방법을 사용 하면 원격 데스크톱 세션을 통해 toohello 가상 컴퓨터를 연결 하기만 하 고 로컬 네트워크에 있는 다른 모든 Windows 클라이언트와 마찬가지로 사용 하기 위해 해당 가상 컴퓨터를 구성 합니다. Hello 포트는 이미 알려진 때문에 tooappend hello 공용 포트 번호가 필요 하지 않습니다.

## <a name="work-with-hello-storsimple-virtual-device"></a>Hello StorSimple 가상 장치 사용
생성 하 고 hello StorSimple 가상 장치를 구성 했으므로 작업을 준비 toostart 됩니다. 물리적 StorSimple 장치;에서 마찬가지로 가상 장치에서 볼륨 컨테이너, 볼륨 및 백업 정책을 작업 수 있습니다. hello 유일한 차이점은 toomake 장치 목록에서 hello 가상 장치를 선택 해야 합니다. 너무 참조[hello StorSimple 관리자 서비스 toomanage 가상 장치를 사용 하 여](storsimple-manager-service-administration.md) hello hello 가상 장치에 대 한 다양 한 관리 작업의 단계별 절차에 대 한 합니다.

hello 다음 섹션에서는 설명의 몇 가지 hello 차이점 hello 가상 장치를 작업할 때 발생 합니다.

### <a name="maintain-a-storsimple-virtual-device"></a>StorSimple 가상 장치 유지 관리
소프트웨어 전용 장치 이므로 hello 가상 장치에 대 한 유지 관리는 최소한의 경우 toomaintenance hello 물리적 장치에 대 한 비교 합니다. Hello 다음 옵션을 사용할 수 있습니다.

* **소프트웨어 업데이트** – hello 소프트웨어를 마지막으로 업데이트, 업데이트 상태 메시지와 함께 hello 날짜를 볼 수 있습니다. Hello를 사용할 수 있습니다 **업데이트 검색** 단추 hello 페이지 tooperform hello 맨 아래에 수동 검색이 toocheck 새 업데이트 하려는 경우. 업데이트를 사용할 수 있으면 클릭 **업데이트 설치** tooinstall 합니다. Hello 가상 장치에서 인터페이스가 하나 뿐 이기 때문에이 것 서비스가 잠시 중단 업데이트 적용 시기 의미 합니다. hello 가상 장치 종료 되며 (필요한 경우)를 다시 시작 tooapply 출시 된 업데이트 합니다. 단계별 절차에 대 한 이동 너무[장치 업데이트](storsimple-update-device.md#install-regular-updates-via-the-azure-classic-portal)합니다.
* **지원 패키지** – 만들 수 있습니다 및 업로드 지원 패키지 toohelp Microsoft 지원 가상 장치에 문제를 해결 합니다. 단계별 절차에 대 한 이동 너무[만들고 지원 패키지를 관리할](storsimple-create-manage-support-package.md)합니다.

### <a name="storage-accounts-for-a-virtual-device"></a>가상 장치에 대한 저장소 계정
Hello StorSimple Manager 서비스, hello 가상 장치 및 hello 실제 장치에서 사용 하기 위해 저장소 계정은 만듭니다. 저장소 계정을 만들 때 영역을 사용 하는 것이 좋습니다 hello 이름 toohelp의 식별자를 해당 hello 지역의 hello 시스템 구성 요소 중 전체 일관성을 유지 합니다. 가상 장치는 같은 지역 tooprevent 성능 문제를 hello hello 구성 요소에는 수의 모든 중요 합니다.

단계별 절차에 대 한 이동 너무[저장소 계정 추가](storsimple-manage-storage-accounts.md#add-a-storage-account)합니다.

### <a name="deactivate-a-storsimple-virtual-device"></a>StorSimple 가상 장치 비활성화
가상 장치를 비활성화 하면 VM hello 및 프로 비전 된 경우 생성 된 hello 리소스를 삭제 합니다. Hello 가상 장치를 비활성화 한 후 수 없습니다 tooits 이전 상태로 복원 합니다. Hello 가상 장치를 비활성화 하기 전에 toostop 있는지 확인 하거나 클라이언트와 의존 하는 호스트를 삭제 합니다.

작업을 수행 하는 hello에서는 가상 장치를 비활성화 합니다.

* hello 가상 장치가 제거 됩니다.
* hello OS 디스크 및 hello 가상 장치에 대해 생성 된 데이터 디스크 제거 됩니다.
* hello 호스팅된 서비스 및 가상 네트워크를 구축 하는 동안 만든 유지 됩니다. 사용하지 않는 경우 수동으로 삭제해야 합니다.
* Hello 가상 장치에 대해 만든 클라우드 스냅숏은 유지 됩니다.

단계별 절차에 대 한 이동 너무[비활성화 StorSimple 장치를 삭제 하 고](storsimple-deactivate-and-delete-device.md)합니다.

가상 장치 hello hello StorSimple 관리자 서비스 페이지 비활성화 된 것으로 표시 되는 즉시 hello 장치 목록에서 hello 가상 장치를 삭제할 수 있습니다 **장치** 페이지.

### <a name="start-stop-and-restart-a-virtual-device"></a>가상 장치 시작, 중지 및 다시 시작
Hello StorSimple 물리적 장치를 달리 전원이 on 또는 off StorSimple 가상 장치에서 단추 toopush 전원 합니다. 그러나 toostop 필요 하 고 hello 가상 장치를 다시 시작 하는 경우가 있을 수 있습니다. 예를 들어, 일부 업데이트가 VM 수는 hello toofinish hello 업데이트 프로세스를 다시 시작 해야 합니다. hello toostart 있습니다, 중지 및 다시 시작 가상 장치에 대 한 가장 쉬운 방법은 toouse hello 가상 컴퓨터 관리 콘솔입니다.

Hello 관리 콘솔을 보면 hello 가상 장치 상태는 **실행** 를 만든 후 기본적으로 시작 됩니다. 언제든지 가상 컴퓨터를 시작하고 중지하고 다시 시작할 수 있습니다.

[!INCLUDE [Stop and restart virtual device](../../includes/storsimple-stop-restart-virtual-device.md)]

### <a name="reset-toofactory-defaults"></a>Toofactory 기본값 다시 설정
방금 되도록 toostart을 통해 가상 장치를 결정 한 경우 이러한 서비스는 비활성화 및 삭제 한 다음 새를 만듭니다. 프로그램 물리적 장치를 다시 설정할 때와 마찬가지로 새 가상 장치에는 없습니다 모든 업데이트를 설치 해야 합니다. 따라서 있는지 toocheck 사용 하기 전에 업데이트를 확인 합니다.

## <a name="fail-over-toohello-virtual-device"></a>장애 조치 toohello 가상 장치
DR (재해 복구) StorSimple 가상 장치는 위해 설계 되었으므로 hello hello 주요 시나리오 중 하나입니다. 이 시나리오에서는 물리적 StorSimple 장치 hello 또는 전체 데이터 센터를 사용할 수 없습니다. 다행히 대체 위치에 가상 장치 toorestore 작업을 사용할 수 있습니다. DR 동안 hello hello 원본 장치의 볼륨 컨테이너는 소유권이 변경 되며 가상 장치에 전송 된 toohello 합니다. hello DR에 대 한 필수 구성 요소는는 hello 가상 장치를 만들고 구성, hello 볼륨 컨테이너 내의 모든 hello 볼륨을 오프 라인으로 전환, 및 hello 볼륨 컨테이너에 연결 된 클라우드 스냅숏이 있습니다.

> [!NOTE]
> * 가상 장치 hello 보조 장치로 dr을 사용할 경우 hello 8010 표준 저장소 30TB 개이고 8020 64TB의 프리미엄 저장소에 염두에 둬야 합니다. hello 더 높은 용량 8020 가상 장치는 DR 시나리오에 적합 한 더 수 있습니다.
> * 복제를 실행 하는 장치에서 사전 업데이트 1 소프트웨어를 실행 하는 2 tooa 장치를 업데이트 하거나 장애 조치를 수 없습니다. 그러나 장애 조치 (1.1 또는 1.2) 업데이트 1을 실행 하는 tooa 장치 업데이트 2를 실행 하는 장치 수 있습니다.
>
>

단계별 절차에 대 한 이동 너무[장애 조치 tooa 가상 장치](storsimple-device-failover-disaster-recovery.md#fail-over-to-a-storsimple-virtual-device)합니다.

## <a name="shut-down-or-delete-hello-virtual-device"></a>종료 또는 hello 가상 장치를 삭제 합니다.
이전에 구성 하 고 사용 StorSimple 가상 장치 하지만 이제 toostop의 사용에 대 한 계산 요금 발생 이벤트를 시킬 hello 가상 장치를 종료할 수 있습니다. Hello 가상 장치를 종료 하면 해당 운영 체제나 데이터 디스크 저장소에서 삭제 되지 않습니다. 요금이 발생 하 여 구독에 하지 않지만 데이터 디스크 및 운영 체제 hello에 대 한 저장소 비용은 계속 합니다.

으로 표시를 삭제 하거나 hello 가상 장치 종료 **오프 라인** hello StorSimple Manager 서비스의 hello 장치 페이지에 있습니다. 또한 원할 경우 toodelete hello 가상 장치에서 생성 된 hello 백업을 hello 장치를 삭제 하거나 toodeactivate 선택할 수 있습니다. 자세한 내용은 [StorSimple 장치 비활성화 및 삭제](storsimple-deactivate-and-delete-device.md)를 참조하세요.

[!INCLUDE [Shut down a virtual device](../../includes/storsimple-shutdown-virtual-device.md)]

[!INCLUDE [Delete a virtual device](../../includes/storsimple-delete-virtual-device.md)]

## <a name="troubleshoot-internet-connectivity-errors"></a>인터넷 연결 오류 문제 해결
없는 연결 toohello 인터넷, 경우에 가상 장치의 hello 만드는 동안 hello 생성 단계 실패 합니다. 인터넷에 연결 되어이 hello 실패 하는 경우 tootroubleshoot 수행 hello hello Azure 클래식 포털의에서 단계를 실행 합니다.

1. Azure에서 Windows Server 2012 가상 컴퓨터를 만듭니다. 이 가상 컴퓨터가 사용 하도록 hello 동일한 저장소 계정, VNet 및 가상 장치에서 사용 되는 서브넷입니다. 이미 있는 경우 기존 사용 하 여 Azure에서 Windows Server 호스트는 동일한 저장소 계정, Vnet 및 서브넷 hello, 있습니다 수 또한 tootroubleshoot hello 인터넷에 연결 합니다.
2. Hello 앞 단계에서에서 만든 hello 가상 컴퓨터에 원격 로그인입니다.
3. Hello 가상 컴퓨터 내의 명령 창을 엽니다 (Win + R을 입력 한 후 `cmd`).
4. Hello cmd hello 프롬프트에서 다음을 실행 합니다.

    `nslookup windows.net`
5. 경우 `nslookup` 실패 하는 인터넷 연결 실패 때문 hello 가상 장치 toohello StorSimple Manager 서비스를 등록 합니다.
6. 가상 장치 hello tooyour 가상 네트워크 tooensure는 hello 필요한 변경 내용 수 tooaccess "windows.net" 등의 Azure 사이트를 확인 합니다.

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[hello StorSimple 관리자 서비스 toomanage 가상 장치를 사용 하 여](storsimple-manager-service-administration.md)합니다.
* 너무 방법을 이해[백업 세트에서 StorSimple 볼륨을 복원](storsimple-restore-from-backup-set.md)합니다.
