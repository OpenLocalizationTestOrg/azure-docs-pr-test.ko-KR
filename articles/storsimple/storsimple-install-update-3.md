---
title: "StorSimple 장치에서 업데이트 3 aaaInstall | Microsoft Docs"
description: "에 대해 설명 방법을 StorSimple 8000 시리즈 장치에 StorSimple 8000 시리즈 업데이트 3 tooinstall 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: c6c4634d-4f3a-4bc4-b307-a22bf18664e1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a156b8919639f1c7afb0fdef3d882d40d48f1c48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-3-on-your-storsimple-8000-series-device"></a>StorSimple 8000 시리즈 장치에 업데이트 3 설치

## <a name="overview"></a>개요

이 자습서를 통해 이전 소프트웨어 버전을 실행 하는 StorSimple 장치에 업데이트 3 tooinstall Azure 클래식 포털 및 hello 핫픽스 메서드를 사용 하 여 hello 하는 방법을 설명 합니다. hello 핫픽스 메서드 이외의 hello StorSimple 장치의 DATA 0 네트워크 인터페이스에는 게이트웨이 구성 하는 사전 업데이트 1 소프트웨어 버전에서 tooupdate 때 사용 됩니다.

업데이트 3에는 장치 소프트웨어, LSI 드라이버 및 펌웨어, Storport 및 Spaceport 업데이트가 포함됩니다. 이전 버전 또는 업데이트 2를 업데이트 하는 경우 또한 필요한 tooapply iSCSI, WMI를 선택한 경우에 따라 디스크 펌웨어 업데이트 합니다. 장치 소프트웨어, WMI, iSCSI, LSI 드라이버, Spaceport, 및 Storport hello 정기적인 업데이트는 픽스와 hello Azure 클래식 포털을 통해 적용할 수 있습니다. hello 디스크 펌웨어 업데이트가 중단 업데이트 되며 hello 장치의 hello Windows PowerShell 인터페이스를 통해 적용할 수 있습니다. 

> [!IMPORTANT]
> * 일련의 수동 및 자동 사전 검사에는 하드웨어 상태 및 네트워크 연결 측면에서 이전 toohello 설치 toodetermine hello 장치 상태를 수행 됩니다. 이러한 사전 검사 hello Azure 클래식 포털에서에서 hello 업데이트를 적용 하는 경우에 수행 됩니다.
> * Hello 소프트웨어를 설치 및 드라이버 업데이트를 통해 Azure 클래식 포털 hello 것이 좋습니다. Hello 포털에서 hello 게이트웨이 업데이트 사전 검사에 실패 하는 경우에 (tooinstall 업데이트) hello 장치의 toohello Windows PowerShell 인터페이스를 이동 해야 합니다. Hello 업데이트에서 업데이트 하는 hello 버전에 따라, tooinstall 1.5-2.5 시간을 걸릴 수 있습니다. hello 장치의 hello Windows PowerShell 인터페이스를 통해 hello 유지 관리 모드 업데이트를 설치 합니다. 유지 관리 모드 업데이트는 중단 업데이트입니다. 이는 장치에 중단 시간을 발생시킵니다.
> * 실행 hello 선택적 StorSimple 스냅숏 관리자, 스냅숏 관리자 버전 2 tooUpdate 이전 tooupdating hello 장치를 업그레이드를 확인 합니다.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-3-via-hello-azure-classic-portal"></a>Hello Azure 클래식 포털을 통해 업데이트 3을 설치 합니다.
다음 단계 tooupdate hello 장치 너무 수행[업데이트 3](storsimple-update3-release-notes.md)합니다.

> [!NOTE]
> 나중에 (포함 업데이트 2.1) 또는 업데이트 2를 적용 하는 경우 Microsoft hello 장치에서 추가 진단 정보 수 toopull 됩니다. 결과적으로, 운영 팀이 문제가 발생 하는 장치를 식별 하는 경우 hello 장치에서 더 나은 장착된 toocollect 정보 하 고 문제를 진단 합니다. 업데이트 2 이상를 수락 하면 우리 tooprovide이 사전 지원 합니다.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

장치가 **StorSimple 8000 시리즈 업데이트 3(6.3.9600.17759)**를 실행하고 있는지 확인합니다. hello **마지막 업데이트 날짜** 스페이스도 수정 해야 합니다. 
   - 버전 이전 tooUpdate 2에서에서 업데이트 하는 경우 표시 됩니다 hello 유지 관리 모드 업데이트를 사용할 수 있는지 (이 메시지는 too24를 설치한 후 시간 hello 업데이트에 대해 표시 되는 toobe 계속 될 수 있습니다).
     유지 관리 모드 업데이트 업데이트가 중단 장치 가동 중지 시간이 발생 하 고 장치의 hello Windows PowerShell 인터페이스를 통해 적용할 수 있습니다. 경우에 따라 업데이트 1.2를 실행 하는 디스크 펌웨어 최신 이미 있을 경우 tooinstall 필요 하지 않습니다는 경우 모든 유지 관리 모드 업데이트.
   - 업데이트 2 이상에서 업데이트하는 경우 이제 장치가 최신 상태입니다. Hello 다음 단계를 건너뛸 수 있습니다.

에 나열 된 hello 단계를 사용 하 여 hello 유지 관리 모드 업데이트를 다운로드 [toodownload 핫픽스](#to-download-hotfixes) toosearch에 대 한 디스크 펌웨어 업데이트를 설치 하는 KB3121899 다운로드 (hello 다른 업데이트가 이미 설치 되어 있어야 지금까지). 에 나열 된 hello 단계에 따라 [설치 하 고 유지 관리 모드 핫픽스 확인](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello 유지 관리 모드 업데이트 합니다. 

## <a name="install-update-3-as-a-hotfix"></a>핫픽스로 업데이트 3 설치
Hello Azure 클래식 포털을 통해 tooinstall hello 업데이트 하려고 할 때 hello 게이트웨이 확인이 실패 하는 경우이 절차를 사용 합니다. 할당 tooa 비 DATA 0 네트워크 인터페이스 게이트웨이 있고 해당 장치에서 실행 하는 소프트웨어 버전 이전 tooUpdate 1을 실행 하는 대로 hello 확인이 실패 합니다.

hello 핫픽스 메서드를 사용 하 여 업그레이드할 수 있는 hello 소프트웨어 버전이 됩니다.

* 업데이트 0.1, 0.2, 0.3
* 업데이트 1, 1.1, 1.2
* 업데이트 2, 2.1, 2.2 

> [!IMPORTANT]
> * 장치에서 릴리스 (GA) 버전을 실행 하는 경우 문의 [Microsoft 지원](storsimple-contact-microsoft-support.md) tooassist hello로 업데이트 합니다.
> 
> 

hello 핫픽스 메서드 3 개 단계를 수행 하는 hello 포함 됩니다.

1. Hello Microsoft Update 카탈로그에서에서 hello 핫픽스를 다운로드 합니다.
2. 설치 하 고 hello 일반 모드 핫픽스를 확인 하십시오.
3. 설치 하 고 (경우에에서 사전 업데이트 2 소프트웨어 업데이트) hello 유지 관리 모드 핫픽스를 확인 합니다.

#### <a name="download-updates-for-your-device"></a>장치에 대한 업데이트 다운로드
**장치 업데이트 2.1 또는 2.2에서 실행 중인 경우**를 다운로드 하 여 hello 다음 순서를 지정 하는 hello에 핫픽스를 설치 해야 합니다.

| 순서 | KB | 설명 | 업데이트 유형 | 설치 시간 |
| --- | --- | --- | --- | --- |
| 1. |KB3186843 |소프트웨어 업데이트 &#42; |일반  <br></br>중단 없음 |~ 45분 |
| 2. |KB3186859 |LSI 드라이버 및 펌웨어 |일반 <br></br>중단 없음 |~ 20분 |
| 3. |KB3121261 |Storport 및 Spaceport 픽스  </br> Windows Server 2012 R2 |일반 <br></br>중단 없음 |~ 20분 |

&#42;  *두 이진 파일의 해당 hello 소프트웨어 업데이트 구성 됩니다. 참고: 앞에 추가 소프트웨어 업데이트 장치 `all-hcsmdssoftwareupdate` Ci hello 및 Mds 에이전트 앞에 추가 하 고 `all-cismdsagentupdatebundle`. hello Ci 및 Mds 하기 전에 hello 장치 소프트웨어 업데이트를 설치 해야 합니다 에이전트입니다. 또한 hello hello 통해 활성 컨트롤러를 다시 시작 해야 `Restart-HcsController` cmdlet hello Ci 및 Mds 에이전트 업데이트를 적용 한 후 (및 hello 남아 있는 업데이트를 적용 하기 전에).* 

**장치 업데이트 0.1, 0.2, 0.3, 1.0, 1.1, 1.2 또는 2.0에서 실행 중인 경우**와 펌웨어에 순서를 지정 하는 hello (에 표시 된 hello 앞에 테이블), 업데이트 하, 다운로드 하 고 hello 다음 추가 toohello 소프트웨어 LSI 드라이버에에서 핫픽스를 설치 해야 합니다.

| 순서 | KB | 설명 | 업데이트 유형 | 설치 시간 |
| --- | --- | --- | --- | --- |
| 4. |KB3146621 |iSCSI 패키지 |일반 <br></br>중단 없음 |~ 20분 |
| 5. |KB3103616 |WMI 패키지 |일반 <br></br>중단 없음 |~ 12분 |

<br></br>

**장치 0.2, 0.3, 1.0, 1.1 및 1.2 버전에서 실행 중인 경우**, tooinstall 디스크 펌웨어 업데이트 hello 이전 테이블에에서 표시 된 모든 hello 업데이트를 기반으로 할 수도 있습니다. Hello를 실행 하 여 디스크 펌웨어 업데이트 hello 필요 여부를 확인할 수 있습니다 `Get-HcsFirmwareVersion` cmdlet. 이러한 펌웨어 버전을 실행 하는 경우: `XMGG`, `XGEG`, `KZ50`, `F6C2`, `VR08`, 이러한 업데이트 tooinstall를 불필요 합니다.

| 순서 | KB | 설명 | 업데이트 유형 | 설치 시간 |
| --- | --- | --- | --- | --- |
| 6. |KB3121899 |디스크 펌웨어 |유지 관리 <br></br>중단 |~ 30분 |

<br></br>

> [!IMPORTANT]
> * 이 절차 요구 toobe tooapply 업데이트 3 한 번만 수행 합니다. Hello Azure 클래식 포털 tooapply 후속 업데이트를 사용할 수 있습니다.
> * 업데이트 2.2를 업데이트 하는 경우 hello 총 설치 시간 닫기 too1.1 시간입니다.
> * 이 절차 tooapply hello를 사용 하기 전에 업데이트 된 hello 두 장치 컨트롤러가 모두 온라인 이며 모든 hello 하드웨어 구성 요소가 정상 상태에 있는지 확인 합니다.
> 
> 

Hello 단계 toodownload 다음을 수행 하 고 hello 핫픽스를 설치 합니다.

[!INCLUDE [storsimple-install-update3-hotfix](../../includes/storsimple-install-update3-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>다음 단계
Hello에 대 한 자세한 [업데이트 3 릴리스](storsimple-update3-release-notes.md)합니다.

