---
title: "aaaStorSimple 8000 시리즈 보안 | Microsoft Docs"
description: "Hello 보안 및 StorSimple 서비스, 장치 및 hello 클라우드 및 온-프레미스 데이터를 보호 하는 개인 정보 보호 기능을 설명 합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: a21d19c6-83b4-418c-9380-323bb9f76612
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/03/2016
ms.author: v-sharos
ms.openlocfilehash: b9e6c8b3371b4039549972cf507052312ed7cdaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-security-and-data-protection"></a>StorSimple 보안 및 데이터 보호
## <a name="overview"></a>개요
보안은 모든 사용자에 게는 특히 hello 기술이 기밀 또는 소유 데이터와 함께 사용 되는 경우는 새 기술을 채택 하 고 주요 관심사입니다. 다양한 기술을 평가하는 동안 데이터 보호에 대한 비용 및 위험 증가를 고려해야 합니다. Microsoft Azure StorSimple 보안 및 개인 정보 보호 솔루션 둘 다에 대 한 제공 데이터 보호 tooensure 수 있도록 지원: 

* **기밀성** – 권한 있는 엔터티만 데이터를 볼 수 있습니다. 
* **무결성** – 권한 있는 엔터티만 데이터를 수정하거나 삭제할 수 있습니다.

Microsoft Azure StorSimple 솔루션 hello 서로 상호 작용 하는 네 가지 주요 구성 요소가 구성 됩니다.

* **Microsoft Azure에서 호스팅되는 StorSimple Manager 서비스** – hello 관리 서비스 tooconfigure 및 프로 비전을 사용 하는 hello StorSimple 장치입니다.
* **StorSimple 장치** – 데이터 센터에 설치된 물리적 장치입니다. 모든 호스트와 데이터를 생성 하는 클라이언트 toohello StorSimple 장치를 연결한 hello 장치 hello 데이터를 관리 하 고 Azure 클라우드 toohello 이동 적절 하 게 합니다.
* **클라이언트/호스트 연결 toohello 장치** – toohello StorSimple 장치를 연결 하는 인프라에서 클라이언트 hello 및 toobe 보호 해야 하는 데이터를 생성 합니다.
* **클라우드 저장소** – hello 데이터가 저장 되는 Azure 클라우드 hello에 위치 합니다.

hello 다음 단원에서는 이러한 각 구성 요소 및에 저장 된 hello 데이터를 보호 하는 데 hello StorSimple 보안 기능. 또한 Microsoft Azure StorSimple 보안과 hello 해당 대답에 대 한 포함 된 질문의 목록도 포함 됩니다.

## <a name="storsimple-manager-service-protection"></a>StorSimple 관리자 서비스 보호
hello StorSimple Manager 서비스는 관리 서비스가 Microsoft Azure에서 호스트 되 고 toomanage 조직에서 조달 하는 모든 StorSimple 장치를 사용 합니다. Toohello 웹 브라우저를 통해 Azure 클래식 포털에서 조직 자격 증명 toolog를 사용 하 여 hello StorSimple Manager 서비스에 액세스할 수 있습니다. 

액세스 toohello StorSimple Manager 서비스 조직 StorSimple을 포함 하는 Azure 구독이 있어야 합니다. 구독은 hello Azure 클래식 포털에에서 액세스할 수 있는 hello 기능을 제어 합니다. 조직에 Azure 구독이 없는 경우에 대 한 자세한 toolearn 참조 [조직으로 Azure에 등록](../active-directory/sign-up-organization.md)합니다. 

StorSimple Manager 서비스 hello Azure에서 호스팅되므로 hello Azure 보안 기능을 통해 보호 됩니다. Microsoft Azure에서 제공 하는 hello 보안 기능에 대 한 자세한 내용을 보려면 이동 toohello [Microsoft Azure 보안 센터](https://azure.microsoft.com/support/trust-center/security/)합니다.

## <a name="storsimple-device-protection"></a>StorSimple 장치 보호
hello StorSimple 장치가 (Ssd) 반도체 드라이브와 하드 디스크 드라이브 (Hdd) 함께 중복 컨트롤러 및 자동 장애 조치 기능을 포함 하는 온-프레미스 하이브리드 저장 장치가입니다. hello 컨트롤러는 저장소 계층화, 현재 사용 되는 (또는 핫) 데이터 배치 (hello StorSimple 장치 또는 온-프레미스 서버)의 로컬 저장소에 toohello 클라우드 덜 사용 되는 데이터를 이동 하는 동안 관리 합니다.

StorSimple 장치에 toojoin hello Azure 구독에서 만든 StorSimple 관리자 서비스는 사용할 수 있는 권한이 부여 된 합니다. tooauthorize 장치를 등록 해야 StorSimple Manager 서비스 hello로 hello 서비스 등록 키를 제공 하 여 합니다. hello 서비스 등록 키는 hello Azure 클래식 포털에서에서 생성 하는 128 비트 임의 키가입니다. 

![서비스 등록 키](./media/storsimple-security/ServiceRegistrationKey.png)

toolearn 어떻게 서비스 등록 키, go 너무[2 단계: Get hello 서비스 등록 키](storsimple-deployment-walkthrough.md#step-2-get-the-service-registration-key)합니다.

hello 서비스 등록 키는 100 개 이상의 문자를 포함 하는 긴 키가입니다. Hello 키를 복사 하 고 필요에 따라 추가 장치 tooauthorize 사용할 수 있습니다를 안전한 위치에 텍스트 파일에 저장할 수 있습니다. 첫 번째 장치를 등록 한 후 hello 서비스 등록 키를 분실 한 경우에 hello StorSimple Manager 서비스에서에서 새 키를 생성할 수 있습니다. 기존 장치의 hello 작동에 영향을 주지 않습니다. 

장치를 등록 한 후에 토큰 toocommunicate을 사용 하 여 Microsoft Azure를 사용 합니다. 장치 등록 후 hello 서비스 등록 키를 사용 되지 않습니다.

> [!NOTE]
> 모든 사용 후 hello 서비스 등록 키를 다시 생성 하는 것이 좋습니다.
> 
> 

## <a name="protect-your-storsimple-solution-via-passwords"></a>암호를 통해 StorSimple 솔루션 보호
암호가 컴퓨터 보안의 중요 한 사항이 및 널리 사용 되며 toohelp hello StorSimple 솔루션에서 데이터를 액세스할 수 있는 tooauthorized 사용자만을 확인 합니다. StorSimple 암호 다음 tooconfigure hello가 있습니다.

* StorSimple 장치 관리자 암호
* 핸드셰이크 인증 프로토콜(CHAP) 초기자 및 대상 암호 문제
* StorSimple 스냅숏 관리자 암호

### <a name="windows-powershell-for-storsimple-and-hello-storsimple-device-administrator-password"></a>Hello StorSimple 장치 관리자 암호와 StorSimple 용 Windows PowerShell
StorSimple 용 Windows PowerShell은 명령줄 인터페이스 toomanage hello StorSimple 장치를 사용할 수 있습니다. StorSimple 용 Windows PowerShell에는 장치 tooregister 사용할 수 있는 기능, 장치에서 hello 네트워크 인터페이스 구성, 특정 형식의 업데이트를 설치, hello 지원 세션에 액세스 하 여 장치 문제 해결 및 hello 장치 상태 변경 . 연결 toohello hello 장치의 직렬 콘솔 또는 Windows PowerShell 원격을 사용 하 여 StorSimple 용 Windows PowerShell을 액세스할 수 있습니다.

PowerShell 원격은 HTTPS 또는 HTTP를 통해 수행할 수 있습니다. HTTPS 통한 원격 관리를 사용 하면 toodownload hello에 대 한 원격 관리 hello 장치에서 인증서를 hello 원격 클라이언트에 설치 합니다. PowerShell 원격 기능에 대 한 자세한 내용은 이동 너무[tooyour StorSimple 장치를 원격으로 연결](storsimple-remote-connect.md)합니다.

Windows PowerShell을 사용 하 여 StorSimple tooconnect toohello 장치용 tooprovide hello 장치 관리자 암호 toolog toohello 장치에 필요 합니다.

![장치 관리자 암호](./media/storsimple-security/DeviceAdminPW.png)

최선의 구현 방법을 고려에서 하는 hello에 유의 하십시오.

* 원격 관리는 기본적으로 꺼져 있습니다. StorSimple Manager 서비스 tooenable hello를 사용할 수 있습니다 것입니다. 보안 모범 사례로 hello 실제로 필요한 기간 동안에 원격 액세스를 활성화 해야 합니다.
* Hello 암호 변경 하면 예기치 않은 연결 끊김을 겪지 않도록 있는지 toonotify 모든 원격 액세스 사용자 수 있습니다.
* hello StorSimple Manager 서비스를 검색할 수 없습니다. 기존 암호: 재설정만 수 있습니다. 없는 tooreset 암호를 잊어버린 경우 있도록 안전한 장소에 모든 암호를 저장 하는 것이 좋습니다. Tooreset 암호를 해야 하는 경우 수 있는지 toonotify 모든 사용자가 다시 설정 하기 전에. 

직렬 연결 toohello 장치를 사용 하 여 hello Windows PowerShell 인터페이스에 액세스할 수 있습니다. 또한 보안이 강화된 HTTP 또는 HTTPS를 사용하여 원격으로 액세스할 수도 있습니다. HTTPS는 직렬 또는 HTTP 연결보다 더 높은 수준의 보안을 제공합니다. 그러나 toouse HTTPS를 먼저 설치 해야 인증서 hello 장치 액세스 하는 hello 클라이언트 컴퓨터에서. 원격 액세스 인증서 hello hello StorSimple Manager 서비스의에서 hello 장치 구성 페이지에서 다운로드할 수 있습니다. 원격 액세스에 대 한 hello 인증서를 잃어버린 경우 새 인증서를 다운로드 하 고 tooall 클라이언트 원격 관리 권한이 있는 toouse를 전파 해야 합니다.

### <a name="challenge-handshake-authentication-protocol-chap-initiator-and-target-passwords"></a>핸드셰이크 인증 프로토콜(CHAP) 초기자 및 대상 암호 문제
CHAP는 hello StorSimple 장치 toovalidate hello id 원격 클라이언트에서 사용 하는 인증 체계입니다. hello 확인은 공유 암호를 기반으로 합니다. CHAP는 일방(단방향)이거나 상호적(양방향)일 수 있습니다. 단방향 chap hello 대상 (hello StorSimple 장치)은 초기자 (호스트)를 인증 합니다. 상호 / 역방향 CHAP는 hello 대상을 hello 초기자 인증 hello 초기자를 인증 한 다음 hello 대상 필요 합니다. StorSimple 구성된 toouse 두 방법 중 하나를 수 있습니다.

CHAP를 구성할 때 hello 다음 유의 해야 합니다.

* hello CHAP 사용자 이름에 보다 적은 233 자 이어야 합니다.
* hello CHAP 암호는 12 ~ 16 자 사이 여야 합니다. Toouse 시도 더 긴 사용자 이름이 나 암호가 hello Windows 호스트에서 인증 실패가 발생 합니다.
* Hello를 사용할 수 없습니다 hello CHAP 초기자와 CHAP 대상 hello에 대 한 동일한 암호입니다.
* Hello 암호를 설정한 후 변경 될 수 있지만 검색할 수 없습니다. Hello 암호를 변경 하는 경우 할 수 있는지 toonotify 모든 원격 액세스 사용자 toohello StorSimple 장치를 성공적으로 연결할 수 있습니다.

CHAP에 대 한 자세한 내용은 방법 tooconfigure StorSimple 솔루션에 대해 이동 너무[StorSimple 장치에 대 한 CHAP 구성](storsimple-configure-chap.md)합니다.

### <a name="storsimple-snapshot-manager-password"></a>StorSimple 스냅숏 관리자 암호
StorSimple 스냅숏 관리자는 볼륨 그룹 및 hello Windows 볼륨 섀도 복사본 서비스 toogenerate 응용 프로그램에 일관 된 백업을 사용 하는 Microsoft 관리 콘솔 (MMC) 스냅인입니다. StorSimple 스냅숏 관리자 toocreate 백업 일정 및 복제를 사용 하거나 볼륨을 복원할 수 있습니다.

장치 toouse StorSimple 스냅숏 관리자를 구성할 때 필요한 tooprovide hello StorSimple 스냅숏 관리자 암호 수 있습니다. 이 암호는 등록 중 StorSimple에 대한 Windows PowerShell에서 먼저 설정됩니다. hello 암호도 수 설정할 수 있으며 hello StorSimple Manager 서비스에서에서 변경 되었습니다. StorSimple 스냅숏 관리자 hello 장치를 인증 합니다.

![StorSimple 스냅숏 관리자 암호](./media/storsimple-security/SnapshotMgrPassword.png)

hello StorSimple 스냅숏 관리자 암호 14 too15 자 이어야 하 고 3 개 이상의 대문자, 소문자, 숫자 및 특수 문자의 조합을 포함 해야 합니다. Hello StorSimple 스냅숏 관리자 암호를 설정한 후 변경 될 수 있지만 검색할 수 없습니다. Hello 암호를 변경 하는 경우 모든 원격 사용자가 있는지 toonotify 수 있습니다.

자세한 내용은 StorSimple 스냅숏 관리자에 대 한 이동 너무[StorSimple 스냅숏 관리자 란?](storsimple-what-is-snapshot-manager.md)

### <a name="password-best-practices"></a>암호 모범 사례
Hello 다음을 사용 하는 것이 좋습니다 지침 toohelp StorSimple 암호가 강력 하 고 잘 보호 되는지 확인 합니다.

* 3개월 마다 암호를 변경합니다. Hello 암호 변경 매년 적용 됩니다.
* 강력한 암호를 사용합니다. 자세한 내용은 이동 너무[강력한 암호 생성 후 보호](http://blogs.microsoft.com/cybertrust/2014/08/25/create-stronger-passwords-and-protect-them/)합니다.
* 항상 서로 다른 액세스 메커니즘;에 대해 다른 암호를 사용 지정한 hello 암호의 각 고유 해야 합니다.
* 권한 있는 tooaccess hello StorSimple 장치 되지 않은 모든 사용자와 암호를 공유 하지 않습니다.
* hello 암호 형식의 힌트 하거나 다른 사람 앞 암호에 관해 하지 마십시오.
* 계정이 나 암호가 손상 된 것 같으면 hello 인시던트 tooyour 정보 보안 부서를 보고 합니다.
* 모든 암호는 중요한 기밀 정보로 취급됩니다. 

## <a name="storsimple-data-protection"></a>StorSimple 데이터 보호
이 섹션에 전송 되는 데이터 및 저장 된 데이터를 보호 하는 hello StorSimple 보안 기능에 설명 합니다.

다른 섹션에서 설명 하는 대로 암호 사용 되는 tooauthorize 되며 액세스 tooyour StorSimple 솔루션에 한 권한을 얻을 수 있는 사용자를 인증 합니다. 다른 보안 고려 사항은 저장하는 동안 및 저장소 시스템 간에 전송되는 동안 권한이 없는 사용자로부터 데이터를 보호하기 위한 것입니다. hello 다음 섹션에서는 설명 hello StorSimple와 함께 제공 되는 데이터 보호 기능입니다.

> [!NOTE]
> 중복 제거는 hello StorSimple 장치에 Microsoft Azure 저장소에 저장 된 데이터에 대 한 추가 보호를 제공 합니다. Hello 데이터 개체 hello 사용 메타 데이터는 toomap에서 별도로 저장 및 액세스할 때 데이터는 중복 제거: 볼륨 구조, 파일 시스템 또는 파일 이름에 따라 사용 가능한 저장소 수준 컨텍스트 tooreconstruct hello 데이터가 없습니다.
> 
> 

## <a name="protect-data-flowing-through-hello-service"></a>Hello 서비스를 통해 흐르는 데이터를 보호 합니다.
hello StorSimple Manager 서비스의 주요 목적은 hello toomanage 이며 hello StorSimple 장치를 구성 합니다. Microsoft Azure의 hello StorSimple Manager 서비스를 실행합니다. Hello Azure 클래식 포털 tooenter 장치 구성 데이터를 사용 하 고 Microsoft Azure hello StorSimple 관리자 서비스 toosend hello 데이터 toohello 장치를 사용 하는 다음 합니다. StorSimple의 비대칭 키 쌍 toohelp 시스템의 hello Azure 서비스를 손상 발생 하지 것입니다 확인을 사용 하 여 정보를 저장 합니다. 

![기내 데이터 암호화](./media/storsimple-security/DataEncryption.png)

hello 비대칭 키 체계는 다음과 같이 hello 서비스를 통해 이동 하는 hello 데이터를 보호 합니다.

1. 비대칭 공개 및 개인 키 쌍을 사용 하 여 데이터 암호화 인증서를 hello 장치에서 생성 되 고 사용 되는 tooprotect hello 데이터입니다. hello 키는 hello 첫 번째 장치를 등록 하는 경우에 생성 됩니다. 
2. hello 데이터 암호화 인증서 키는 hello 서비스 데이터 암호화 키가 등록 하는 동안 hello 첫 번째 장치에서 임의로 생성 하는 강력한 128 비트 키로 보호 되는 개인 정보 교환 (.pfx) 파일로 내보내집니다.
3. hello hello 인증서의 공개 키가 사용 가능한 toohello StorSimple Manager 서비스를 안전 하 게 하 고 hello 개인 키 hello 장치와 함께 유지 됩니다.
4. 시작 중 hello 서비스를 사용 하 여 암호화 된 데이터는 공개 키를 hello hello 장치에 저장 된 hello 개인 키를 사용 하 여 암호를 해독 해당 hello Azure 서비스를 확인 없습니다 데이터 및 암호 해독 hello toohello 장치 이동 합니다.

hello 서비스 데이터 암호화 키만 hello 첫 번째 장치에서 hello 서비스에 등록 된 생성 됩니다. Hello 서비스에 등록 된 모든 후속 장치 해야 hello를 사용 하 여 같은 서비스 데이터 암호화 키입니다. 

> [!IMPORTANT]
> 매우 중요 한 toomake hello 서비스 데이터 암호화 키의 복사본을 안전한 위치에 저장 하십시오. Hello 서비스 데이터 암호화 키의 복사본은 권한 있는 사용자에 액세스할 수 쉽게 전달된 toohello 장치 관리자 일 수 있습니다 하는 방식으로 저장 되어야 합니다.
> 
> Hello 서비스 데이터 암호화 키를 분실 한 경우이 제공 되는 온라인 상태에서 장치가 하나 이상 있는지 tooretrieve Microsoft 지원 담당자에 수 있습니다. 검색 된 hello 서비스 데이터 암호화 키를 변경 하는 것이 좋습니다. 자세한 내용은 이동 너무[hello 서비스 데이터 암호화 키 변경](storsimple-service-dashboard.md#change-the-service-data-encryption-key)합니다.
> 
> 

Hello를 선택 하 여 hello 서비스 데이터 암호화 키 및 hello 해당 데이터 암호화 인증서를 변경할 수 있습니다 **서비스 데이터 암호화 키 변경** hello 서비스 대시보드에서 옵션입니다. 데이터 보안이 손상 되지 않도록 tooensure, 물리적 StorSimple 장치 toochange hello 서비스 데이터 암호화 키를 사용 해야 합니다. Hello 암호화 키를 변경 해야 hello 새 키로 모든 장치를 업데이트 해야 합니다. 따라서 모든 장치는 온라인 때 hello 키를 변경 하는 것이 좋습니다. 장치가 오프라인 상태인 경우 다른 시간에 해당 키를 변경할 수 있습니다. 오래 된 키를 사용 하 여 hello 장치 수 toorun 백업이 됩니다 하지만 hello 키를 업데이트할 때까지 수 toorestore 데이터 위치 하지 않습니다. 자세한 내용은 이동 너무[사용 가능한 hello StorSimple 관리자 서비스 대시보드](storsimple-service-dashboard.md)합니다.

hello 서비스 데이터 암호화 키 및 hello 데이터 암호화 인증서가 만료 되지 않습니다. 그러나 좋습니다 hello 서비스 데이터 암호화를 변경 하는 키 매년 toohelp 키 손상을 방지 합니다.

## <a name="protect-data-at-rest"></a>휴지 상태의 데이터 보호
hello StorSimple 장치 로컬과 사용 빈도에 따라 hello 클라우드에서 계층에 저장 하 여 데이터를 관리 합니다. 모든 호스트 컴퓨터가 있는 연결 된 toohello 장치 송신 데이터 toohello는 장치를 적절 하 게 데이터 toohello 클라우드를 이동 합니다. 데이터는 hello 인터넷을 통해 안전 하 게 hello 장치 toohello 클라우드에서 전송 됩니다. 각 장치에는 해당 장치의 모든 공유 볼륨을 표시하는 하나의 iSCSI 대상이 있습니다. Toocloud 저장소 전송 하기 전에 모든 데이터가 암호화 됩니다. 

![클라우드 저장소 암호화 키](./media/storsimple-security/CloudStorageEncryption.png)

toohelp hello 보안을 보장 및 데이터의 무결성 toohello 클라우드 이동, StorSimple 있습니다 toodefine 클라우드 저장소 암호화 키 다음과 같습니다.

* 볼륨 컨테이너를 만들 때 hello 클라우드 저장소 암호화 키를 지정 합니다. hello 키를 수정 하거나 나중에 추가할 수 없습니다. 
* 볼륨 컨테이너 공유의 모든 볼륨 hello 동일한 암호화 키입니다. 다른 형식의 특정 볼륨에 대 한 암호화 하려는 경우 만드는 새 볼륨 컨테이너 toohost 해당 볼륨 하는 것이 좋습니다.
* Hello StorSimple Manager 서비스에서에서 hello 클라우드 저장소 암호화 키를 입력 하면 hello hello 서비스 데이터 암호화 키의 공개 부분을 사용 하 여 보내고 다음 toohello 장치 hello 키가 암호화 됩니다.
* hello 클라우드 저장소 암호화 키 hello 서비스에 저장 되지 않습니다 및 toohello 장치에만 알려져 있습니다.
* 클라우드 저장소 암호화 키 지정은 선택 사항입니다. Hello 호스트 toohello 장치에서 암호화 된 데이터를 보낼 수 있습니다.

### <a name="additional-security-best-practices"></a>추가 보안 모범 사례
* 트래픽 분할: 완전히 분리된 네트워크를 배포하고 물리적 격리가 옵션이 아닌 VLAN을 사용하여 회사 LAN의 사용자 트래픽에서 iSCSI SAN을 격리합니다. ISCSI 저장소 전용된 네트워크 hello 안전 하 고 비즈니스에 중요 한 데이터의 성능이 보장 됩니다. 회사 LAN을 통한 저장소 및 사용자 트래픽 혼합은 권장하지 않으며 대기 시간이 증가하고 네트워크 오류를 일으킬 수 있습니다.
* 호스트 측 네트워크 보안은 TCP/IP 오프로드 엔진(TOE)을 지원하는 네트워크 인터페이스를 사용합니다. TOE는 hello 네트워크 어댑터에서 TCP가 처리 하는 CPU 부하를 줄입니다.

## <a name="protect-data-via-storage-accounts"></a>저장소 계정을 통해 데이터 보호
각 Microsoft Azure 구독에 하나 이상의 저장소 계정을 만들 수 있습니다. (저장소 계정 고유한 네임 스페이스 작업을 위한 제공 hello Azure 클라우드에에서 저장 된 데이터입니다.) Tooa 저장소 계정 액세스는 해당 저장소 계정과 연결 된 hello 구독 및 액세스 키에 의해 제어 됩니다. 

저장소 계정을 만들 때 Microsoft Azure StorSimple 장치 hello hello 저장소 계정에 액세스할 때 인증에 사용 되는 중 하나는 두 개의 512 비트 저장소 액세스 키를 생성 합니다. 이 키 중 하나만 사용 중입니다. hello 다른 키를 소집 비축 toorotate hello 키 주기적으로 합니다. 활성 상태 이면 hello 보조 키를 누른 다음 삭제 hello에 대 한 기본 키 toorotate 키를 확인합니다. Hello 다음 회전 하는 동안 사용 하기 위해 새 키를 만들 수 있습니다. (보안상의 이유로 많은 데이터 센터 키 회전이 필요합니다.) 

키 회전에 대해 이 모범 사례를 따르는 것이 좋습니다.

* 저장소 계정 키 정기적으로 저장소 계정의 권한이 없는 사용자가 액세스 되지 않으면 toohelp 확인 회전 해야 합니다.
* 주기적으로 Azure 관리자 변경 하거나 hello Azure 클래식 포털 toodirectly 액세스 hello 저장소 계정의 저장소 섹션 hello를 사용 하 여 hello 기본 또는 보조 키를 다시 생성 해야 합니다.

## <a name="protect-data-via-encryption"></a>암호화를 통해 데이터 보호
StorSimple는 tooprotect 데이터에 저장 된 암호화 알고리즘에 따라 또는 StorSimple 솔루션의 hello 구성 요소 간의 여행 hello를 사용 합니다.

| 알고리즘 | 키 길이 | 프로토콜/응용 프로그램/주석 |
| --- | --- | --- |
| RSA |2048 |RSA PKCS 1 v 1.5 hello toohello 장치 전송 되는 Azure 클래식 포털 tooencrypt 구성 데이터에서 사용 하는: 저장소 계정 자격 증명을 StorSimple 장치 구성 및 클라우드 저장소 암호화 키입니다. 예를 들어 있습니다. |
| AES |256 |CBC와는 AES toohello Azure 클래식 포털 hello StorSimple 장치에서 전송 하기 전에 사용 되는 tooencrypt hello hello 서비스 데이터 암호화 키의 공개 부분을는입니다. 또한 toohello 클라우드 저장소 계정에 hello 데이터 보내기 전에 hello StorSimple 장치 tooencrypt 데이터에서 사용 됩니다. |

## <a name="storsimple-virtual-device-security"></a>StorSimple 가상 장치 보안
[!INCLUDE [storsimple virtual device security](../../includes/storsimple-virtual-device-security.md)]

## <a name="frequently-asked-questions-faq"></a>질문과 대답(FAQ)
hello 다음 몇 가지 질문과 보안 및 Microsoft Azure StorSimple에 대 한 답변은입니다.

**Q:** 서비스가 손상되었습니다. 다음 단계에서 어떻게 해야 합니까?

**A:** hello 서비스 데이터 암호화 키 및 데이터를 계층화에 사용 되는 hello 저장소 계정에 대 한 hello 저장소 계정 키를 즉시 변경 해야 합니다. 자세한 내용은 다음을 참조하세요. 

* [Hello 서비스 데이터 암호화 키 변경](storsimple-service-dashboard.md#change-the-service-data-encryption-key)
* [저장소 계정의 키 회전](storsimple-manage-storage-accounts.md#key-rotation-of-storage-accounts)

**Q:** hello 서비스 등록 키를 요청 하는 새 StorSimple 장치 했습니다. 어떻게 장치를 검색하나요?

**A:** hello StorSimple Manager 서비스를 처음 만들 때이 키가 생성 됩니다. Hello StorSimple 관리자 서비스 tooconnect toohello 장치를 사용 하 여 hello 서비스 빠른 시작 페이지 tooview 또는 regenerate hello 서비스 등록 키를 사용할 수 있습니다. 새 서비스 등록 키를 생성 해도 hello 기존에 등록 된 장치는 영향을 주지 않습니다. 자세한 내용은 다음을 참조하세요.

* [보거나 hello 서비스 등록 키 다시 생성](storsimple-service-dashboard.md#view-or-regenerate-the-service-registration-key)

**Q:** 서비스 데이터 암호화 키를 잃어버렸습니다. 어떻게 해야 합니까?

**A:** Microsoft 지원에 문의하세요. 장치와 (제공 된 하나 이상의 장치는 온라인) hello 키를 검색 하는 도움말 tooa 지원 세션에 로그온 할 수 있습니다. Hello 서비스 데이터 암호화 키를 가져온 후 변경 해야 tooensure 즉시 그 hello 새 키만 tooyou를 알려져 있습니다. 자세한 내용은 다음을 참조하세요.

* [Hello 서비스 데이터 암호화 키 변경](storsimple-service-dashboard.md#change-the-service-data-encryption-key)

**Q:** 는 서비스 데이터 암호화 키 변경에 대 한 장치에 권한을 부여 했지만 hello 키 변경 프로세스를 시작 하지 못했습니다. 어떻게 해야 하나요?

**A:** hello 제한 시간이 만료 된 경우 tooreauthorize hello 장치 hello 서비스 데이터 암호화 키 변경에 대 한 필요 하 고 hello 프로세스를 다시 시작 합니다.

**Q:** hello 서비스 데이터 암호화 키를 변경 했지만 없었습니다 tooupdate 4 시간 이내에 다른 장치 hello 합니다. 용량은 toostart 다시

**A:** hello 4 시간 이라는 기간은 hello 변경 시작에 대해서만 합니다. 에 hello 업데이트 프로세스를 시작 하면 hello 권한이 StorSimple 장치에 대 hello 권한 부여는 모든 장치에서 업데이트 될 때까지 유효 합니다.

**Q:** Our StorSimple 관리자 hello 회사를 떠난 합니다. 어떻게 해야 하나요?

**A:** 변경 및 재설정 hello 액세스 toohello StorSimple 장치를 허용 하 고 hello 서비스 데이터 암호화 키 tooensure hello 새 정보 toounauthorized 담당자는 알려지지 않은 변경 하는 암호입니다. 자세한 내용은 다음을 참조하세요.

* [StorSimple Manager 서비스 toochange hello storsimple 암호 사용](storsimple-change-passwords.md)
* [Hello 서비스 데이터 암호화 키 변경](storsimple-service-dashboard.md#change-the-service-data-encryption-key)
* [StorSimple 장치에 대한 CHAP 구성](storsimple-configure-chap.md)

**Q:** tooprovide hello StorSimple 스냅숏 관리자 암호 tooa 호스트 toohello StorSimple 장치를 연결 하 고 싶지만 hello 암호를 사용할 수 없습니다. 어떻게 해야 하나요?

**A:** hello 암호를 잊어버린 경우 새로 만들어야 합니다. 그런 다음 tooinform 변경한 암호 hello 기존의 모든 사용자 및 해당 클라이언트 toouse을 업데이트 해야 새 암호를 hello 해야 합니다. 자세한 내용은 다음을 참조하세요.

* [Hello StorSimple 스냅숏 관리자 암호를 변경 합니다.](storsimple-change-passwords.md#change-the-storsimple-snapshot-manager-password)
* [장치 인증](storsimple-snapshot-manager-manage-devices.md#authenticate-a-device)

**Q:** hello 장치에서 원격 액세스 toohello StorSimple 용 Windows PowerShell에 대 한 hello 인증서가 변경 되었습니다. 내 원격 액세스 클라이언트를 업데이트하려면 어떻게 해야 하나요?

**A:** hello StorSimple Manager 서비스에서에서 hello 새 인증서를 다운로드 하 고 원격 액세스 클라이언트 hello 인증서 저장소에 설치 된 toobe 제공할 수 있습니다. 자세한 내용은 다음을 참조하세요.

* [가져오기-Certificate cmdlet](https://technet.microsoft.com/library/hh848630.aspx)

**Q:** 데이터가 hello StorSimple Manager 서비스에서 손상 된 경우 보호 됩니까?

**A:** 서비스 구성 데이터는 웹 브라우저에서 볼 때 항상 공용 키로 암호화 됩니다. Hello 서비스 하지는 hello 서비스 액세스 toohello 개인 키가 있으므로 수 toosee 데이터 수입니다. StorSimple Manager 서비스 hello 손상 되 면 영향을 주지 처럼입니다 hello StorSimple Manager 서비스에에서 저장 된 키가 있습니다.

**Q:** 액세스 toohello 데이터 암호화 인증서를 다른 사람이 데이터 저하 됩니다.

**A:** Microsoft Azure hello 고객의 데이터 암호화 키 (.pfx 파일)를 암호화 된 형식으로 저장 합니다. Hello.pfx 파일은 암호화 되어 있으므로 hello StorSimple 서비스가 hello 서비스 데이터 암호화 키 toodecrypt hello.pfx 파일을 간단히 access toohello.pfx 파일 노출 되지는 않습니다 된 비밀을 합니다.

**Q:** 정부 기관이 Microsoft에 내 데이터를 요청하는 경우 어떻게 되나요?

**A:** 모든 hello 데이터는 hello 서비스에서 암호화 및 hello 개인 키는 유지 hello 장치와 hello 정부 때문에 엔터티 hello 데이터에 대 한 hello 고객을 요청 해야 합니다. 

## <a name="next-steps"></a>다음 단계
[StorSimple 장치 배포](storsimple-deployment-walkthrough.md)

