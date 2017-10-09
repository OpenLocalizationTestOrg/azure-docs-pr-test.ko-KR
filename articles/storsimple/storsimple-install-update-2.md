---
title: "StorSimple 장치에서 업데이트 2 aaaInstall | Microsoft Docs"
description: "에 대해 설명 방법을 StorSimple 8000 시리즈 장치에 StorSimple 8000 시리즈 업데이트 2 tooinstall 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8c8981df-75d9-4d19-b137-d6c6ba39dcfb
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 33a0bea4358c944644563192f686af332d2ad7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-2-on-your-storsimple-device"></a>StorSimple 장치에 업데이트 2 설치
## <a name="overview"></a>개요
이 자습서에서는 tooinstall hello Azure 클래식 포털을 통해 이전 소프트웨어 버전을 실행 하는 StorSimple 장치에서 2를 업데이트 하는 방법을 설명 합니다. hello 자습서 이외의 hello StorSimple 장치의 DATA 0 네트워크 인터페이스에는 게이트웨이 구성 하 고 1 소프트웨어 업데이트 전 버전에서 tooupdate 고치려는 hello 업데이트에 필요한 hello 단계에 대해서도 설명 합니다.

업데이트 2는 장치 소프트웨어 업데이트, LSI 드라이버 업데이트 및 디스크 펌웨어 업데이트를 포함합니다. hello 장치 소프트웨어 및 LSI 업데이트가 정기적인 업데이트는 hello Azure 클래식 포털을 통해 적용할 수 있습니다. hello 디스크 펌웨어 업데이트가 중단 업데이트 되며 hello 장치의 hello Windows PowerShell 인터페이스를 통해 적용할 수 있습니다.

> [!IMPORTANT]
> * 업데이트 2를 표시 되지 않을 수 hello 업데이트의 단계별된 공개를 수행 하는 것 때문에 즉시 합니다. 해당 업데이트를 곧 사용할 수 있게 되므로 몇 일 후에 업데이트를 스캔합니다.
> * 일련의 수동 및 자동 사전 검사에는 하드웨어 상태 및 네트워크 연결 측면에서 이전 toohello 설치 toodetermine hello 장치 상태를 수행 됩니다. 이러한 사전 검사 hello Azure 클래식 포털에서에서 hello 업데이트를 적용 하는 경우에 수행 됩니다.
> * Hello 소프트웨어를 설치 및 드라이버 업데이트를 통해 Azure 클래식 포털 hello 것이 좋습니다. Hello 포털에서 hello 게이트웨이 업데이트 사전 검사에 실패 하는 경우에 (tooinstall 업데이트) hello 장치의 toohello Windows PowerShell 인터페이스를 이동 해야 합니다. hello 업데이트 (포함 hello Windows 업데이트) 4-7 시간 tooinstall을 걸릴 수 있습니다. hello 장치의 hello Windows PowerShell 인터페이스를 통해 hello 유지 관리 모드 업데이트를 설치 합니다. 유지 관리 모드 업데이트는 중단 업데이트입니다. 이는 장치에 중단 시간을 발생시킵니다.
> * 실행 hello 선택적 StorSimple 스냅숏 관리자, 스냅숏 관리자 버전 2 tooUpdate 이전 tooupdating hello 장치를 업그레이드를 확인 합니다.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-2-via-hello-azure-classic-portal"></a>Hello Azure 클래식 포털을 통해 업데이트 2 설치
다음 단계 tooupdate hello 장치 너무 수행[업데이트 2](storsimple-update2-release-notes.md)합니다.

> [!NOTE]
> 업데이트 2는 Microsoft toopull 추가 진단 정보 hello 장치에서 사용 하도록 설정 합니다. 결과적으로, 운영 팀이 문제가 발생 하는 장치를 식별 하는 경우 hello 장치에서 더 나은 장착된 toocollect 정보 하 고 문제를 진단 합니다. 업데이트 2를 수락 하면 우리 tooprovide이 사전 지원 합니다.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. 장치가 **StorSimple 8000 시리즈 업데이트 2(6.3.9600.17673)**를 실행하고 있는지 확인합니다. hello **마지막 업데이트 날짜** 스페이스도 수정 해야 합니다. 유지 관리 모드 업데이트를 사용할 수 있는지 표시 됩니다 (이 메시지는 too24를 설치한 후 시간 hello 업데이트에 대해 표시 되는 toobe 계속 될 수 있습니다).
   
   유지 관리 모드 업데이트 업데이트가 중단 장치 가동 중지 시간이 발생 하 고 장치의 hello Windows PowerShell 인터페이스를 통해 적용할 수 있습니다. 경우에 따라 업데이트 1.2를 실행 하는 디스크 펌웨어 최신 이미 있을 경우 tooinstall 필요 하지 않습니다는 경우 모든 유지 관리 모드 업데이트.
2. 에 나열 된 hello 단계를 사용 하 여 hello 유지 관리 모드 업데이트를 다운로드 [toodownload 핫픽스](#to-download-hotfixes) toosearch에 대 한 디스크 펌웨어 업데이트를 설치 하는 KB3121899 다운로드 (hello 다른 업데이트가 이미 설치 되어 있어야 지금까지).
3. 에 나열 된 hello 단계에 따라 [설치 하 고 유지 관리 모드 핫픽스 확인](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello 유지 관리 모드 업데이트 합니다.

## <a name="install-update-2-as-a-hotfix"></a>핫픽스로 업데이트 2 설치
Hello Azure 클래식 포털을 통해 tooinstall hello 업데이트 하려고 할 때 hello 게이트웨이 확인이 실패 하는 경우이 절차를 사용 합니다. 할당 tooa 비 DATA 0 네트워크 인터페이스 게이트웨이 있고 해당 장치에서 실행 하는 소프트웨어 버전 이전 tooUpdate 1을 실행 하는 대로 hello 확인이 실패 합니다.

hello 핫픽스 메서드를 사용 하 여 업그레이드할 수 있는 hello 소프트웨어 버전 업데이트 0.1, 0.2, 업데이트 및 업데이트 0.3, 업데이트 1, 업데이트 1.1 및 1.2 업데이트 됩니다. hello 핫픽스 메서드 3 개 단계를 수행 하는 hello 포함 됩니다.

* Hello Microsoft Update 카탈로그에서에서 hello 핫픽스를 다운로드 합니다.
* 설치 하 고 hello 일반 모드 핫픽스를 확인 하십시오.
* 설치 하 고 hello 유지 관리 모드 핫픽스를 확인 하십시오.

tooinstall 핫픽스로 업데이트 2를 다운로드 하 고 설치 해야 핫픽스 다음 hello:

| 순서 | KB | 설명 | 업데이트 유형 |
| --- | --- | --- | --- |
| 1 |KB3121901 |소프트웨어 업데이트 |일반 |
| 2 |KB3121900 |LSI 드라이버 |일반 |
| 3 |KB3080728 |Storport 픽스  </br> Windows Server 2012 R2 |일반 |
| 4 |KB3090322 |Spaceport 픽스  </br> Windows Server 2012 R2 |일반 |
| 5 |KB3121899 |디스크 펌웨어 |유지 관리 |

> [!IMPORTANT]
> * 장치에서 릴리스 (GA) 버전을 실행 하는 경우 문의 [Microsoft 지원](storsimple-contact-microsoft-support.md) tooassist hello로 업데이트 합니다.
> * 이 절차 요구 toobe tooapply 업데이트 2를 한 번만 수행 합니다. Hello Azure 클래식 포털 tooapply 후속 업데이트를 사용할 수 있습니다.
> * 각 핫픽스 설치 toocomplete 약 20 분 정도 걸릴 수 있습니다. 총 설치 시간은 닫기 too2 시간입니다.
> * 이 절차 tooapply hello를 사용 하기 전에 업데이트 된 두 장치 컨트롤러가 모두 온라인 이며 모든 hello 하드웨어 구성 요소가 정상 상태에 있는지 확인 합니다.
> 
> 

핫픽스로 hello 단계 tooapply 다음이 업데이트를 수행 합니다.

[!INCLUDE [storsimple-install-update2-hotfix](../../includes/storsimple-install-update2-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>다음 단계
Hello에 대 한 자세한 [업데이트 2를 릴리스](storsimple-update2-release-notes.md)합니다.

