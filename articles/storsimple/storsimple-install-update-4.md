---
title: "StorSimple 장치에 업데이트 4 aaaInstall | Microsoft Docs"
description: "에 대해 설명 방법을 StorSimple 8000 시리즈 장치에 StorSimple 8000 시리즈 업데이트 4 tooinstall 합니다."
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
ms.date: 05/30/2017
ms.author: alkohli
ms.openlocfilehash: 62c0ae94afdbb1027d3075962afa04d49fd1f60a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-4-on-your-storsimple-device"></a>StorSimple 장치에 업데이트 4 설치

## <a name="overview"></a>개요

이 자습서를 통해 이전 소프트웨어 버전을 실행 하는 StorSimple 장치에 업데이트 4 tooinstall Azure 클래식 포털 및 hello 핫픽스 메서드를 사용 하 여 hello 하는 방법을 설명 합니다. hello 핫픽스 메서드 이외의 hello StorSimple 장치의 DATA 0 네트워크 인터페이스에는 게이트웨이 구성 하는 사전 업데이트 1 소프트웨어 버전에서 tooupdate 때 사용 됩니다.

업데이트 4는 장치 소프트웨어, USM 펌웨어, LSI 드라이버 및 펌웨어, Storport 및 Spaceport, OS 보안 업데이트 및 기타 OS 업데이트의 호스트를 포함합니다.  hello 장치 소프트웨어, USM 펌웨어, Spaceport, Storport, 및 기타 운영 체제 업데이트에는 정기적인 업데이트입니다. Azure 클래식 포털 hello 또는 hello 핫픽스 메서드를 통해 hello 무중단 또는 정기적인 업데이트를 적용할 수 있습니다. hello 디스크 펌웨어 업데이트가 중단 업데이트 되며 hello 장치의 hello Windows PowerShell 인터페이스를 사용 하 여 hello 핫픽스 메서드를 통해 적용할 수 있습니다. 

> [!IMPORTANT]
> * 일련의 수동 및 자동 사전 검사에는 하드웨어 상태 및 네트워크 연결 측면에서 이전 toohello 설치 toodetermine hello 장치 상태를 수행 됩니다. 이러한 사전 검사 hello Azure 클래식 포털에서에서 hello 업데이트를 적용 하는 경우에 수행 됩니다.
> * Hello 소프트웨어와 hello Azure 클래식 포털을 통해 정기적인 업데이트를 설치 하는 것이 좋습니다. Hello 포털에서 hello 게이트웨이 업데이트 사전 검사에 실패 하는 경우에 (tooinstall 업데이트) hello 장치의 toohello Windows PowerShell 인터페이스를 이동 해야 합니다. 업데이트 하는 hello 버전에 따라, hello 업데이트 시간이 걸릴 수 있습니다 4 (이상) tooinstall 합니다. hello 장치의 hello Windows PowerShell 인터페이스를 통해 hello 유지 관리 모드 업데이트도 설치 되어 있어야 합니다. 유지 관리 모드 업데이트는 중단 업데이트입니다. 이는 장치에 중단 시간을 발생시킵니다.
> * 실행 hello 선택적 StorSimple 스냅숏 관리자, 스냅숏 관리자 버전 4 tooUpdate 이전 tooupdating hello 장치를 업그레이드를 확인 합니다.


[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-4-via-hello-azure-classic-portal"></a>Hello Azure 클래식 포털을 통해 업데이트 4를 설치 합니다.
다음 단계 tooupdate hello 장치 너무 수행[업데이트 4](storsimple-update4-release-notes.md)합니다.

> [!NOTE]
> 나중에 (포함 업데이트 2.1) 또는 업데이트 2를 적용 하는 경우 Microsoft hello 장치에서 추가 진단 정보 수 toopull 됩니다. 결과적으로, 운영 팀이 문제가 발생 하는 장치를 식별 하는 경우 hello 장치에서 더 나은 장착된 toocollect 정보 하 고 문제를 진단 합니다. 업데이트 2 이상를 수락 하면 우리 tooprovide이 사전 지원 합니다. 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

장치가 **StorSimple 8000 시리즈 업데이트 4(6.3.9600.17820)**를 실행하고 있는지 확인합니다. hello **마지막 업데이트 날짜** 스페이스도 수정 해야 합니다. 

* Hello 유지 관리 모드 업데이트를 사용할 수 있는지 표시 됩니다 (이 메시지는 too24를 설치한 후 시간 hello 업데이트에 대해 표시 되는 toobe 계속 될 수 있습니다). 유지 관리 모드 업데이트 업데이트가 중단 장치 가동 중지 시간이 발생 하 고 장치의 hello Windows PowerShell 인터페이스를 통해 적용할 수 있습니다.
 
* 에 나열 된 hello 단계를 사용 하 여 hello 유지 관리 모드 업데이트를 다운로드 [toodownload 핫픽스](#to-download-hotfixes) toosearch에 대 한 디스크 펌웨어 업데이트를 설치 하는 KB4011837 다운로드 (hello 다른 업데이트가 이미 설치 되어 있어야 지금까지). 에 나열 된 hello 단계에 따라 [설치 하 고 유지 관리 모드 핫픽스 확인](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello 유지 관리 모드 업데이트 합니다. 

## <a name="install-update-4-as-a-hotfix"></a>핫픽스로 업데이트 4 설치
hello는 메서드 tooinstall을 hello Azure 클래식 포털을 통해 업데이트 4는 것이 좋습니다.

Hello Azure 클래식 포털을 통해 tooinstall hello 업데이트 하려고 할 때 hello 게이트웨이 확인이 실패 하는 경우이 절차를 사용 합니다. 할당 tooa 비 DATA 0 네트워크 인터페이스 게이트웨이 있고 해당 장치에서 실행 하는 소프트웨어 버전 이전 tooUpdate 1을 실행 하는 대로 hello 확인이 실패 합니다.

hello 핫픽스 메서드를 사용 하 여 업그레이드할 수 있는 hello 소프트웨어 버전이 됩니다.

* 업데이트 0.1, 0.2, 0.3
* 업데이트 1, 1.1, 1.2
* 업데이트 2, 2.1, 2.2
* 업데이트 3, 3.1 


hello 핫픽스 메서드 3 개 단계를 수행 하는 hello 포함 됩니다.

1. Hello Microsoft Update 카탈로그에서에서 hello 핫픽스를 다운로드 합니다.
2. 설치 하 고 hello 일반 모드 핫픽스를 확인 하십시오.
3. 설치 하 고 hello 유지 관리 모드 핫픽스를 확인 하십시오.

#### <a name="download-updates-for-your-device"></a>장치에 대한 업데이트 다운로드

다운로드 하 고 hello 다음을 설치 해야 사전 설정 된 hello에 핫픽스를 주문 및 제안 된 폴더를 hello:

| 순서 | KB | 설명 | 업데이트 유형 | 설치 시간 |폴더에 설치|
| --- | --- | --- | --- | --- | --- |
| 1. |KB4011839 <br> (2개 파일) |장치 소프트웨어 업데이트 <br> CiS/MDS 에이전트 업데이트 |일반 <br></br>중단 없음 |~ 25분 |FirstOrderUpdate <br> _CiS/MDS 에이전트를 업데이트하기 전에 장치 소프트웨어 업데이트 설치_|
| 2A. |KB4011841 <br> KB4011842 |LSI 드라이버 및 펌웨어 업데이트 <br> USM 펌웨어 업데이트(버전 3.38) |일반 <br></br>중단 없음 |~ 3시간 <br> (2A. + 2B. + 2C 포함)|SecondOrderUpdate|
| 2B. |KB3139398, KB3108381 <br> KB3205400, KB3142030 <br> KB3197873, KB3192392  <br> KB3153704, KB3174644 <br> KB3139914  |OS 보안 업데이트 패키지 |일반 <br></br>중단 없음 |- |SecondOrderUpdate|
| 2C. |KB3210083, KB3103616 <br> KB3146621, KB3121261 <br> KB3123538 |OS 업데이트 패키지 |일반 <br></br>중단 없음 |- |SecondOrderUpdate|

Tooinstall 디스크 펌웨어 업데이트 hello 이전 테이블에에서 표시 된 모든 hello 업데이트를 기반으로 할 수도 있습니다. Hello를 실행 하 여 디스크 펌웨어 업데이트 hello 필요 여부를 확인할 수 있습니다 `Get-HcsFirmwareVersion` cmdlet. 이러한 펌웨어 버전을 실행 하는 경우: `XMGJ`, `XGEG`, `KZ50`, `F6C2`, `VR08`, `N002`, `0106`, 이러한 업데이트 tooinstall를 불필요 합니다.

| 순서 | KB | 설명 | 업데이트 유형 | 설치 시간 | 폴더에 설치|
| --- | --- | --- | --- | --- | --- |
| 3. |KB4011837 |디스크 펌웨어 |유지 관리 <br></br>중단 |~ 30분 | ThirdOrderUpdate |

<br></br>

> [!IMPORTANT]
> * 이 절차 요구 toobe tooapply 업데이트 4를 한 번만 수행 합니다. Hello Azure 클래식 포털 tooapply 후속 업데이트를 사용할 수 있습니다.
> * 업데이트 3 또는 3.1을 업데이트 하는 경우 hello 총 설치 시간 닫기 too4 시간입니다.
> * 이 절차 tooapply hello를 사용 하기 전에 업데이트 된 hello 두 장치 컨트롤러가 모두 온라인 이며 모든 hello 하드웨어 구성 요소가 정상 상태에 있는지 확인 합니다.

Hello 단계 toodownload 다음을 수행 하 고 hello 핫픽스를 설치 합니다.

[!INCLUDE [storsimple-install-update4-hotfix](../../includes/storsimple-install-update4-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>다음 단계
Hello에 대 한 자세한 [업데이트 4 릴리스](storsimple-update4-release-notes.md)합니다.

