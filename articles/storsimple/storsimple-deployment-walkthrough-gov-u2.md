---
title: "정부 포털에서 StorSimple 장치 aaaDeploy | Microsoft Docs"
description: "Hello 단계와 배포 hello StorSimple 업데이트 2 장치와 hello Azure Government 포털에서 서비스에 대 한 모범 사례를 설명합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 5277538c-797e-4e8e-b613-31b5c10cf5a9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/16/2016
ms.author: v-sharos
ms.openlocfilehash: 68104988595341a49a87d78c4a9b1d2675759c27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device-in-hello-government-portal-update-2"></a>Hello 정부 포털 (업데이트 2)에서 온-프레미스 StorSimple 장치 배포
[!INCLUDE [storsimple-version-selector-deploy-gov](../../includes/storsimple-version-selector-deploy-gov.md)]

## <a name="overview"></a>개요
TooMicrosoft Azure StorSimple 장치 배포를 시작 합니다. 이러한 배포 자습서 toohello StorSimple 8000 시리즈 업데이트 2 소프트웨어를 실행 hello Azure Government 포털에에서 적용 됩니다. 이 자습서 시리즈에서는 StorSimple 장치를 구성하는 방법에 대해 설명하며 구성 검사 목록, 구성 필수 조건 목록 및 자세한 구성 단계를 포함합니다.

이 자습서에 hello 정보 hello 안전 조치 검토 하 고 압축을 풀, racked, 고 StorSimple 장치를 케이블로 연결를 가정 합니다. 검토 hello로 시작 하는 작업 tooperform를 여전히 필요 하면 [안전 조치](storsimple-safety.md)합니다. Toounpack, 랙 마운트, 및 장치 케이블 연결 hello 장치 관련 지침을 따릅니다.

* [8100 개봉, 랙 탑재, 케이블 연결](storsimple-8100-hardware-installation.md)
* [8600 개봉, 랙 탑재, 케이블 연결](storsimple-8600-hardware-installation.md)

관리자는 권한이 toocomplete hello 설정 및 구성 프로세스를 필요 합니다. 시작 하기 전에 hello 구성 검사 목록 검토 하는 것이 좋습니다. hello 배포 및 구성 프로세스는 몇 시간 toocomplete를 걸릴 수 있습니다.

> [!NOTE]
> hello Microsoft Azure 웹 사이트에 게시 된 StorSimple 배포 정보를 hello tooStorSimple 8000 시리즈 장치에만 적용 됩니다. Hello 7000 시리즈 장치에 대 한 자세한 내용은 이동: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com)합니다. 7000 시리즈 배포 정보에 대 한 참조 hello [StorSimple 시스템 빠른 시작 가이드](http://onlinehelp.storsimple.com/111_Appliance/)합니다.
> 
> 

## <a name="deployment-steps"></a>배포 단계
이러한 단계가 tooconfigure StorSimple 장치 성능과 tooyour StorSimple Manager 서비스를 연결 합니다. 또한 toohello 필요한 단계를 가지는 선택적 단계와 절차가 hello 배포 하는 동안 toocomplete를 할 수 있습니다. hello 단계별 배포 지침은 각 선택적 단계를 수행 해야 하는 시기를 나타냅니다.

| 단계 | 설명 |
| --- | --- |
| **필수 조건** |이러한 toobe hello 향후 배포 준비 과정에서 완료 해야 합니다. |
| [배포 구성 검사 목록](#deployment-configuration-checklist) |Hello 배포 하는 동안이 검사 목록 toogather 및 기록 정보 이전 tooand를 사용 합니다. |
| [배포 필수 조건](#deployment-prerequisites) |해당 hello의 유효성을 검사 하는 이러한 환경에 배포할 준비가 되었습니다. |
|  | |
| **단계별 배포** |이러한 단계는 필요한 toodeploy 프로덕션 환경에서 StorSimple 장치입니다. |
| [1단계: 새 서비스 만들기](#step-1-create-a-new-service) |StorSimple 장치에 대한 클라우드 관리 및 저장소를 설정합니다. *다른 StorSimple 장치에 대해 기존 서비스가 있는 경우 이 단계를 건너뜁니다*. |
| [2 단계: hello 서비스 등록 키 가져오기](#step-2-get-the-service-registration-key) |이 키 tooregister를 사용 하 고 hello 관리 서비스와 StorSimple 장치를 연결 합니다. |
| [3 단계: 구성 및 StorSimple 용 Windows PowerShell을 통해 hello 장치 등록](#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |Hello 장치 tooyour 네트워크를 연결 하 고 Azure toocomplete hello hello 관리 서비스를 사용 하 여 설치 프로그램을 등록 합니다. |
| [4 단계: hello 최소 장치 설정 완료](#step-4-complete-minimum-device-setup) </br>선택 사항: StorSimple 장치를 업데이트합니다. |Hello 관리 서비스 toocomplete hello 장치 설치 프로그램을 사용 하 고 tooprovide 저장을 설정 합니다. |
| [5단계: 볼륨 컨테이너 만들기](#step-5-create-a-volume-container) |Tooprovision 볼륨 컨테이너를 만듭니다. 볼륨 컨테이너는 저장소 계정, 대역폭 및 암호화 설정에 포함 된 모든 hello 볼륨에 있습니다. |
| [6단계: 볼륨 만들기](#step-6-create-a-volume) |서버에 대 한 hello StorSimple 장치에 대 한 저장소 볼륨을 프로 비전 합니다. |
| [7단계: 볼륨 탑재, 초기화 및 포맷](#step-7-mount-initialize-and-format-a-volume) </br>선택 사항: MPIO를 구성합니다. |Hello 장치에서 제공 하 여 서버 toohello iSCSI 저장소를 연결 합니다. 필요에 따라 MPIO tooensure 링크, 네트워크 및 인터페이스 오류 서버 허용할 수를 구성 합니다. |
| [8단계: 백업 수행](#step-8-take-a-backup) |백업 정책 tooprotect 데이터 설정 |
|  | |
| **기타 절차** |솔루션을 배포 하는 경우 toorefer toothese 프로시저를 할 수 있습니다. |
| [Hello 서비스에 대 한 새 저장소 계정 구성](#configure-a-new-storage-account-for-the-service) | |
| [PuTTY tooconnect toohello 장치 직렬 콘솔을 사용 하 여](#use-putty-to-connect-to-the-device-serial-console) | |
| [업데이트 검색 및 적용](#scan-for-and-apply-updates) | |
| [Hello Windows Server 호스트의 IQN 가져오기](#get-the-iqn-of-a-windows-server-host) | |
| [수동 백업 만들기](#create-a-manual-backup) | |
| [MPIO 구성](#configure-mpio) | |

## <a name="deployment-configuration-checklist"></a>배포 구성 검사 목록
StorSimple 장치를 배포 하기 전에 toocollect 정보 tooconfigure hello 소프트웨어 장치에 필요 합니다. 사전에이 정보 중 일부를 준비 하 고 사용자 환경에서 hello StorSimple 장치 배포의 hello 과정을 간소화 하는 데 도움이 됩니다. 다운로드 하 고 장치를 배포 하는 경우이 검사 목록 toonote hello 구성 세부 정보를 사용 합니다.  

[StorSimple 배포 구성 검사 목록 다운로드](http://www.microsoft.com/download/details.aspx?id=49159)  

## <a name="deployment-prerequisites"></a>배포 필수 조건
hello 다음 섹션에서는 StorSimple Manager 서비스 및 StorSimple 장치에 대 한 hello 구성 필수 구성 요소에 설명 합니다.

### <a name="for-hello-storsimple-manager-service"></a>Hello StorSimple Manager 서비스에 대 한
시작하기 전에 다음 사항을 확인합니다.

* 액세스 자격 증명이 있는 Microsoft 계정이 있습니다.
* 액세스 자격 증명이 있는 Microsoft Azure 저장소 계정이 있습니다.
* Microsoft Azure 구독의 hello StorSimple Manager 서비스에 사용 됩니다. Hello를 통해 구독을 구입 해야 [기업 계약](https://azure.microsoft.com/pricing/enterprise-agreement/)합니다.
* PuTTY와 같은 액세스 tooterminal 에뮬레이션 소프트웨어를 해야합니다.

### <a name="for-hello-device-in-hello-datacenter"></a>Hello 데이터 센터에서 hello 장치에 대 한
Hello 장치를 구성 하기 전에 내용을 확인 하십시오.

* 다음에서 설명한 대로 장치가 완전히 개봉, 랙에 탑재되고 전원, 네트워크 및 직렬 액세스에 완전히 연결되었습니다.
  
  * [8100 장치 개봉, 랙 탑재, 케이블 연결](storsimple-8100-hardware-installation.md)
  * [8600 장치 개봉, 랙 탑재, 케이블 연결](storsimple-8600-hardware-installation.md)

### <a name="for-hello-network-in-hello-datacenter"></a>Hello 네트워크 hello 데이터 센터에 대 한
시작하기 전에 다음 사항을 확인합니다.

* hello 데이터 센터 방화벽에서 포트는 iSCSI 및 클라우드 트래픽에 대 한 열린된 tooallow에 설명 된 대로 [StorSimple 장치의 네트워킹 요구 사항](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device)합니다.

## <a name="step-by-step-deployment"></a>단계별 배포
Hello 데이터 센터에 대 한 단계별 지침 toodeploy 다음 hello StorSimple 장치를 사용 합니다.

## <a name="step-1-create-a-new-service"></a>1단계: 새 서비스 만들기
StorSimple 관리자 서비스는 여러 StorSimple 장치를 관리할 수 있습니다. Hello 단계 toocreate hello StorSimple 관리자 서비스의 새 인스턴스를 다음을 수행 합니다.

[!INCLUDE [storsimple-create-new-service-gov](../../includes/storsimple-create-new-service-gov.md)]

> [!IMPORTANT]
> Toocreate 할 서비스와 저장소 계정의 hello 자동 생성을 설정 하지 않은 경우 저장소 계정을 하나 이상 후 서비스를 성공적으로 만들었습니다. 이 저장소 계정은 볼륨 컨테이너를 만들 때 사용됩니다.
> 
> * 저장소 계정을 자동으로 만들 하지 않은 경우 너무 이동[hello 서비스에 대 한 새 저장소 계정 구성](#configure-a-new-storage-account-for-the-service) 자세한 지침에 대 한 합니다.
> * 저장소 계정의 hello 자동 생성을 사용 하도록 설정한 경우 너무 이동[2 단계: Get hello 서비스 등록 키](#step-2-get-the-service-registration-key)합니다.
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>2 단계: hello 서비스 등록 키 가져오기
Hello StorSimple Manager 서비스가 실행 되 고, tooget hello 서비스 등록 키가 필요 합니다. 이 키가 사용 되는 tooregister를 StorSimple 장치 toohello 서비스를 연결 합니다.

Hello hello 정부 포털의에서 단계를 수행 합니다.

[!INCLUDE [storsimple-get-service-registration-key-gov](../../includes/storsimple-get-service-registration-key-gov.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a>3 단계: 구성 및 StorSimple 용 Windows PowerShell을 통해 hello 장치 등록
Hello 절차 다음에 설명 된 대로 StorSimple 장치의 StorSimple toocomplete hello 초기 설치에 대 한 Windows PowerShell을 사용 합니다. Toouse 터미널 에뮬레이션 소프트웨어 toocomplete이이 단계가 필요 합니다. 자세한 내용은 참조 [PuTTY를 사용 하 여 장치 직렬 콘솔 tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console)합니다.

[!INCLUDE [storsimple-configure-and-register-device-gov](../../includes/storsimple-configure-and-register-device-gov-u2.md)]

## <a name="step-4-complete-minimum-device-setup"></a>4단계: 최소 장치 설정 완료
StorSimple 장치의 최소 장치 구성을 hello에 대 한 하면 됩니다.

* Hello 보조 DNS 서버를 설정 합니다.
* 하나 이상의 네트워크 인터페이스에서 iSCSI를 사용하도록 설정합니다.
* Tooboth hello 컨트롤러 고정된 IP 주소를 할당 합니다.

Hello 정부 포털 toocomplete hello 최소 장치 설치 단계를 수행 하는 hello를 수행 합니다.

[!INCLUDE [storsimple-complete-minimum-device-setup](../../includes/storsimple-complete-minimum-device-setup-u1.md)]

## <a name="step-5-create-a-volume-container"></a>5단계: 볼륨 컨테이너 만들기
볼륨 컨테이너는 저장소 계정, 대역폭 및 암호화 설정에 포함 된 모든 hello 볼륨에 있습니다. StorSimple 장치에서 볼륨 프로비저닝을 시작 하려면 먼저 볼륨 컨테이너 toocreate가 필요 합니다.

Hello hello 정부 포털 toocreate 볼륨 컨테이너에서에서 단계를 수행 합니다.

[!INCLUDE [storsimple-create-volume-container](../../includes/storsimple-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>6단계: 볼륨 만들기
볼륨 컨테이너를 만든 후에 서버에 대 한 hello StorSimple 장치에서 저장소 볼륨을 제공할 수 있습니다. Hello hello 정부 포털 toocreate 볼륨의에서 단계를 수행 합니다.

> [!IMPORTANT]
> Azure StorSimple은 씬 프로비저닝된 볼륨만 만들 수 있습니다.  Azure StorSimple 시스템에서 완전히 프로비전되거나 부분적으로 프로비전된 볼륨은 만들 수 없습니다.
> 
> 

[!INCLUDE [storsimple-create-volume](../../includes/storsimple-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>7단계: 볼륨 탑재, 초기화 및 포맷
Windows Server 호스트에서 이러한 단계를 수행합니다.

> [!IMPORTANT]
> * StorSimple 솔루션의 고가용성을 hello 위해 호스트 서버 (선택 사항) 이전 tooconfiguring iSCSI에서 MPIO를 구성 하는 것이 좋습니다. 호스트 서버에 MPIO 구성 링크, 네트워크 또는 인터페이스 오류 hello 서버 허용할 수 있는지 확인 합니다.
> * 에 대 한 iSCSI 및 MPIO 설치 및 구성 지침은 Windows Server 호스트를 이동 너무[StorSimple 장치에 대 한 MPIO 구성](storsimple-configure-mpio-windows-server.md)합니다. 이러한 hello 단계 toomount 포함, 초기화 및도 StorSimple 볼륨을 포맷 합니다.
> * 에 대 한 iSCSI 및 MPIO 설치 및 구성 지침은 Linux 호스트를 이동 너무[StorSimple Linux 호스트에 대 한 MPIO 구성](storsimple-configure-mpio-on-linux.md)
> 
> 

Hello 단계 toomount 다음을 수행 하지 tooconfigure MPIO를 결정 하는 경우 초기화 및 Windows Server 호스트에 StorSimple 볼륨을 포맷 합니다.

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a>8단계: 백업 수행
백업은 볼륨의 지정 시간 보호 기능을 제공하며 복원 시간을 최소화하면서 복구 기능을 개선합니다. StorSimple 장치에서 두 유형(로컬 스냅숏 및 클라우드 스냅숏)의 백업을 수행할 수 있습니다. 이러한 각 유형의 백업은 **예약됨** 또는 **수동**이 될 수 있습니다.

Hello hello 정부 포털 toocreate 예약된 된 백업에서에서 단계를 수행 합니다.

[!INCLUDE [storsimple-take-backup](../../includes/storsimple-take-backup.md)]

언제든지 수동 백업을 수행할 수 있습니다. 너무 절차를 보려면[수동 백업 만들기](#create-a-manual-backup)합니다.

## <a name="configure-a-new-storage-account-for-hello-service"></a>Hello 서비스에 대 한 새 저장소 계정 구성
이것이 서비스와 저장소 계정의 hello 자동 만들기를 활성화 하지 않은 경우에 tooperform를 필요한 단계는 선택 사항입니다. Microsoft Azure 저장소 계정에 필요한 toocreate StorSimple 볼륨 컨테이너입니다.

Toocreate Azure 저장소 계정을 다른 지역에 필요한 경우 참조 [Azure 저장소 계정에 대 한](../storage/common/storage-create-storage-account.md) 단계별 지침.

Hello 정부 포털 hello에 단계를 수행 하는 hello 수행 **StorSimple Manager 서비스** 페이지.

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-configure-new-storage-account-u1.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a>PuTTY tooconnect toohello 장치 직렬 콘솔을 사용 하 여
tooconnect tooWindows StorSimple 용 PowerShell PuTTY와 같은 터미널 에뮬레이션 소프트웨어 toouse 해야합니다. Hello 직렬 콘솔을 통해 직접 또는 원격 컴퓨터에서 텔넷 세션을 열어 hello 장치에 액세스할 때에 PuTTY를 사용할 수 있습니다.

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>업데이트 검색 및 적용
장치 업데이트는 몇 시간이 걸릴 수 있습니다. Hello에 대 한 단계 tooscan 다음을 수행 하 고 장치에서 업데이트를 적용 합니다.

<!--If you have a gateway configured on a network interface other than Data 0, you will need toodisable Data 2 and Data 3 network interfaces before installing hello update. Go too**Devices > Configure** and disable Data 2 and Data 3 interfaces. You should re-enable these interfaces after hello device is updated.-->

#### <a name="tooupdate-your-device"></a>tooupdate 장치
1. Hello 장치에서 **빠른 시작** 페이지 **장치**합니다. Hello 물리적 장치를 선택를 클릭 **유지 관리** 클릭 하 고 **업데이트 스캔**합니다.  
2. 사용 가능한 업데이트에 대 한 작업 tooscan 생성 됩니다. 사용 가능한 업데이트가 있으면 hello **업데이트 검색** 쪽 변경**업데이트 설치**합니다. **업데이트 설치**를 클릭합니다.
3. 업데이트 작업이 만들어집니다. 너무 이동 하 여 업데이트의 hello 상태를 모니터링**작업**합니다.
   
   > [!NOTE]
   > Hello 업데이트 작업이 시작 되 면 50%로 즉시 hello 상태를 표시 합니다. hello 상태 hello 업데이트 작업이 완료 된 후에 too100 비율을 변경 합니다. Hello 업데이트 프로세스에 대 한 실시간 상태가 없습니다.
   > 
   > 
4. Hello 장치를 업데이트 후 이러한 비활성화 된 경우 데이터 2 및 Data 3 네트워크 인터페이스가 사용 하도록 설정 합니다.

## <a name="get-hello-iqn-of-a-windows-server-host"></a>Hello Windows Server 호스트의 IQN 가져오기
다음 단계 tooget hello iSCSI hello 수행 정규화 된 이름 (IQN) Windows Server® 2012를 실행 중인 Windows 호스트의 합니다.

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>수동 백업 만들기
StorSimple 장치에서 단일 볼륨에 대 한 hello 정부 포털 toocreate 주문형 수동 백업 단계를 수행 하는 hello를 수행 합니다.

[!INCLUDE [Create a manual backup](../../includes/storsimple-create-manual-backup-gov.md)]

## <a name="configure-mpio"></a>MPIO 구성
MPIO(다중 경로 I/O)는 선택적 기능이며 Windows Server에 기본적으로 설치되지 않습니다. 서버 관리자를 통해 기능으로 설치해야 합니다. MPIO 설치 지침에 대 한 이동 너무[StorSimple 장치에 대 한 MPIO 구성](storsimple-configure-mpio-windows-server.md)합니다.

StorSimple 장치에 대 한 MPIO 설치 지침에 대 한 연결 된 tooa Linux 호스트 이동 너무[Linux 호스트에 대 한 MPIO 구성](storsimple-configure-mpio-on-linux.md)합니다.

> [!NOTE]
> MPIO는 Azure의 StorSimple 가상 장치에서 지원되지 않습니다.
> 
> 

## <a name="next-steps"></a>다음 단계
* [가상 장치](storsimple-virtual-device-u2.md)를 구성합니다.
* 사용 하 여 hello [StorSimple Manager 서비스](storsimple-manager-service-administration.md) toomanage StorSimple 장치입니다.

