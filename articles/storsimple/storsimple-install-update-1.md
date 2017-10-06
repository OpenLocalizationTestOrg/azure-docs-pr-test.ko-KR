---
title: "StorSimple 장치에 업데이트 1.2 aaaInstall | Microsoft Docs"
description: "에 대해 설명 방법을 StorSimple 8000 시리즈 장치에 StorSimple 8000 시리즈 업데이트 1.2 tooinstall 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 7a513923-eb77-4078-b0ab-f8e90183796a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0a7601dc0b1ce60eb854227243ecb02d6fb2c678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-12-on-your-storsimple-8000-series-device"></a>StorSimple 8000 시리즈 장치에 업데이트 1.2 설치
## <a name="overview"></a>개요
이 자습서에서는 tooinstall 1.2에는 소프트웨어 버전 이전 tooUpdate 1을 실행 하는 StorSimple 장치를 업데이트 하는 방법을 설명 합니다. hello 자습서 이외의 hello StorSimple 장치의 DATA 0 네트워크 인터페이스에는 게이트웨이 구성 하는 경우 hello 업데이트에 대 한 필요한 hello 추가 단계에 대해서도 설명 합니다.

업데이트 1.2는 장치 소프트웨어 업데이트, LSI 드라이버 업데이트 및 디스크 펌웨어 업데이트를 포함합니다. hello 소프트웨어 및 LSI 드라이버 업데이트 정기적인 업데이트 되며 hello Azure 클래식 포털을 통해 적용할 수 있습니다. hello 디스크 펌웨어 업데이트가 중단 업데이트 되며 hello 장치의 hello Windows PowerShell 인터페이스를 통해 적용할 수 있습니다.

장치가 실행되는 버전에 따라 업데이트 1.2를 적용할지 결정할 수 있습니다. Toohello 이동 하 여 장치의 hello 소프트웨어 버전을 확인 하면 **눈에 보는** 장치 섹션 **대시보드**합니다.

</br>

| 소프트웨어 버전을 실행하는 경우... | Hello 포털에서 어떻게 되나요? |
| --- | --- |
| 릴리스 - GA |릴리스 버전(GA)을 실행하는 경우 이 업데이트를 적용하지 않습니다. 하십시오 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md) tooupdate 장치입니다. |
| 업데이트 0.1 |포털은 업데이트 1.2를 적용합니다. |
| 업데이트 0.2 |포털은 업데이트 1.2를 적용합니다. |
| 업데이트 0.3 |포털은 업데이트 1.2를 적용합니다. |
| 업데이트 1 |이 업데이트는 사용할 수 없습니다. |
| 업데이트 1.1 |이 업데이트는 사용할 수 없습니다. |

</br>

> [!IMPORTANT]
> * 업데이트 1.2 표시 되지 않을 수 hello 업데이트의 단계별된 공개를 수행 하는 것 때문에 즉시 합니다. 해당 업데이트를 곧 사용할 수 있게 되므로 몇 일 후에 업데이트를 스캔합니다.
> * 이 업데이트에는 하드웨어 상태 및 네트워크 연결 측면에서 수동 및 자동 사전 검사 toodetermine hello 장치 상태 집합이 포함 되어 있습니다. 이러한 사전 검사 hello Azure 클래식 포털에서에서 hello 업데이트를 적용 하는 경우에 수행 됩니다.
> * Hello 소프트웨어를 설치 및 드라이버 업데이트를 통해 Azure 클래식 포털 hello 것이 좋습니다. Hello 포털에서 hello 게이트웨이 업데이트 사전 검사에 실패 하는 경우에 (tooinstall 업데이트) hello 장치의 toohello Windows PowerShell 인터페이스를 이동 해야 합니다. hello 업데이트 (Windows 업데이트 hello 포함)는 5-10 시간 tooinstall을 걸릴 수 있습니다. hello 장치의 hello Windows PowerShell 인터페이스를 통해 hello 유지 관리 모드 업데이트를 설치 합니다. 유지 관리 모드 업데이트는 중단 업데이트입니다. 이는 장치에 중단 시간을 발생시킵니다.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-12-via-hello-azure-classic-portal"></a>Hello Azure 클래식 포털을 통해 업데이트 1.2 설치
다음 단계 tooupdate hello 장치 너무 수행[업데이트 1.2](storsimple-update1-release-notes.md)합니다. 장치에서 데이터 0 네트워크 인터페이스에 구성된 게이트웨이가 있는 경우 이 절차를 사용합니다.

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. 장치가 **StorSimple 8000 시리즈 업데이트 1.2(6.3.9600.17584)**를 실행하고 있는지 확인합니다. hello **마지막 업데이트 날짜** 스페이스도 수정 해야 합니다. 유지 관리 모드 업데이트를 사용할 수 있는지 표시 됩니다 (이 메시지는 too24를 설치한 후 시간 hello 업데이트에 대해 표시 되는 toobe 계속 될 수 있습니다).
   
   유지 관리 모드 업데이트 업데이트가 중단 장치 가동 중지 시간이 발생 하 고 장치의 hello Windows PowerShell 인터페이스를 통해 적용할 수 있습니다.
   
   ![유지 관리 페이지](./media/storsimple-install-update-1/InstallUpdate12_10M.png "유지 관리 페이지")
2. 에 나열 된 hello 단계를 사용 하 여 hello 유지 관리 모드 업데이트를 다운로드 [toodownload 핫픽스](#to-download-hotfixes) toosearch에 대 한 디스크 펌웨어 업데이트를 설치 하는 KB3063416 다운로드 (hello 다른 업데이트가 이미 설치 되어 있어야 지금까지).
3. 에 나열 된 hello 단계에 따라 [설치 하 고 유지 관리 모드 핫픽스 확인](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello 유지 관리 모드 업데이트 합니다.
4. Hello Azure 클래식 포털에서 탐색 toohello **유지 관리** 페이지 하단의 hello hello 페이지를 클릭 하 여 **업데이트 검색** 모든 Windows 업데이트 및 클릭 한 다음에 대 한 toocheck **업데이트 설치** . 하면 결국 hello의 업데이트를 성공적으로 설치 완료 된 것입니다.

## <a name="install-update-12-on-a-device-that-has-a-gateway-configured-for-a-non-data-0-network-interface"></a>비데이터 0 네트워크 인터페이스에 구성된 게이트웨이가 있는 장치에 업데이트 1.2 설치
Hello Azure 클래식 포털을 통해 tooinstall hello 업데이트 하려고 할 때 hello 게이트웨이 확인이 실패 하는 경우에이 절차를 사용 해야 합니다. 할당 tooa 비 DATA 0 네트워크 인터페이스 게이트웨이 있고 해당 장치에서 실행 하는 소프트웨어 버전 이전 tooUpdate 1을 실행 하는 대로 hello 확인이 실패 합니다. 장치는 비 DATA 0 네트워크 인터페이스에 게이트웨이가 없으면 hello Azure 클래식 포털에서 직접 장치를 업데이트할 수 있습니다. 참조 [hello Azure 클래식 포털을 통해 설치 업데이트 1.2](#install-update-1.2-via-the-azure-classic-portal)합니다.

이 메서드를 사용 하 여 업그레이드할 수 있는 hello 소프트웨어 버전 업데이트 0.1, 0.2, 업데이트 및 업데이트 0.3 됩니다.

> [!IMPORTANT]
> * 장치에서 릴리스 (GA) 버전을 실행 하는 경우 문의 [Microsoft 지원](storsimple-contact-microsoft-support.md) tooassist hello로 업데이트 합니다.
> * 이 절차 요구 toobe tooapply 업데이트 1.2 한 번만 수행 합니다. Hello Azure 클래식 포털 tooapply 후속 업데이트를 사용할 수 있습니다.
> 
> 

장치 업데이트 전 1 소프트웨어에서 실행 중인과 게이트웨이가 설정 이외의 DATA 0 네트워크 인터페이스에 대 한 업데이트 1.2 hello 다음 두 가지 방법에에서 적용할 수 있습니다.

* **옵션 1**: hello 업데이트를 다운로드 하 여 hello를 사용 하 여 적용 `Start-HcsHotfix` hello 장치의 hello Windows PowerShell 인터페이스에서 cmdlet. 이 hello 권장 되는 방법입니다. **장치에서 업데이트 1.0 또는 1.1 업데이트 실행 중인 경우이 메서드 tooapply 업데이트 1.2를 사용 하지 마십시오.**
* **옵션 2**: hello 게이트웨이 구성 제거 및 설치 hello hello Azure 클래식 포털에서 직접 업데이트 합니다.

이러한 각 항목에 대 한 자세한 지침은 hello 다음 섹션에에서 제공 됩니다.

## <a name="option-1-use-windows-powershell-for-storsimple-tooapply-update-12-as-a-hotfix"></a>옵션 1: 핫픽스로 StorSimple tooapply 업데이트 1.2에 대 한 Windows PowerShell 사용
업데이트 0.1, 0.2, 0.3 및 hello Azure 클래식 포털에서에서 tooinstall 업데이트 하려고 할 때 게이트웨이 검사에 실패 한 경우를 실행 하는 경우에이 절차를 사용 해야 합니다. 릴리스 (GA) 소프트웨어를 실행 하는 경우 다음 문의 [Microsoft 지원](storsimple-contact-microsoft-support.md) tooupdate 장치입니다.

핫픽스로 업데이트 1.2 tooinstall 다운로드 하 고 설치 해야 핫픽스 다음 hello:

| 순서 | KB | 설명 | 업데이트 유형 |
| --- | --- | --- | --- |
| 1 |KB3063418 |소프트웨어 업데이트 |일반 |
| 2 |KB3043005 |LSI SAS 컨트롤러 업데이트 |일반 |
| 3 |KB3063416 |디스크 펌웨어 |유지 관리 |

이 절차 tooapply hello를 사용 하기 전에 업데이트에 있는지 확인 하십시오.

* 두 장치 컨트롤러가 온라인 상태가 됩니다.

Hello 단계 tooapply 업데이트 1.2 다음을 수행 합니다. **hello 업데이트 약 2 시간 toocomplete (약 30 분 소프트웨어의 경우 45 분 디스크 펌웨어에 대 한 드라이버를 30 분)을 수행할 수 있습니다.**

[!INCLUDE [storsimple-install-update-option1](../../includes/storsimple-install-update-option1.md)]

## <a name="option-2-use-hello-azure-classic-portal-tooapply-update-12-after-removing-hello-gateway-configuration"></a>옵션 2: hello Azure 클래식 포털 tooapply 업데이트 1.2를 사용 하 여 hello 게이트웨이 구성을 제거한 후
이 절차를 실행 하는 소프트웨어 버전 이전 tooUpdate 1을 실행 하는 이외의 DATA 0 네트워크 인터페이스에서 설정 하는 게이트웨이 보유 하는 tooStorSimple 장치만 적용 됩니다. Tooclear hello 게이트웨이 설정을 이전 tooapplying hello 업데이트를 해야 합니다.

hello 업데이트에 몇 시간 toocomplete를 걸릴 수 있습니다. 서로 다른 서브넷에 있는 호스트에 iSCSI 인터페이스 hello hello 게이트웨이 구성을 제거 하는 가동 중지 시간이 될 수 있습니다. ISCSI 트래픽이 tooreduce hello 가동 중지 시간에 대 한 데이터 0을 구성 하는 것이 좋습니다.

Hello 단계 toodisable hello 네트워크 인터페이스 hello 게이트웨이 통해 다음을 수행 하 고 hello 업데이트를 적용 합니다.

[!INCLUDE [storsimple-install-update-option2](../../includes/storsimple-install-update-option2.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>다음 단계
Hello에 대 한 자세한 [업데이트 1.2 릴리스](storsimple-update1-release-notes.md)합니다.

