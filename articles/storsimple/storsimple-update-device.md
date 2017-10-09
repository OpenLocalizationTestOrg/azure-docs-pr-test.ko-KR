---
title: "aaaUpdate StorSimple 장치 | Microsoft Docs"
description: "일반 기능 tooinstall 및 유지 관리 모드 업데이트 및 핫픽스 toouse hello StorSimple 업데이트 하는 방법에 대해 설명 합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 786059f5-2a38-4105-941d-0860ce4ac515
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: v-sharos
ms.openlocfilehash: 05acf05c8fc89bbb4343f67ad103235bbe3dba0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-storsimple-8000-series-device"></a>StorSimple 8000 시리즈 장치 업데이트
## <a name="overview"></a>개요
hello StorSimple 업데이트 기능을 사용 하면 tooeasily StorSimple 장치를 최신 상태로 유지 합니다. Hello 업데이트 종류에 따라 업데이트 toohello 장치 hello Azure 클래식 포털을 통해 또는 hello Windows PowerShell 인터페이스를 통해 적용할 수 있습니다. 이 자습서에서는 hello 업데이트 유형을 설명 방법과 각 tooinstall 그 중입니다.

두 종류의 장치 업데이트를 적용할 수 있습니다. 

* 일반(또는 표준 모드) 업데이트
* 유지 관리 모드 업데이트

Hello Azure 클래식 포털 또는 Windows PowerShell;를 통해 정기적으로 업데이트를 설치할 수 있습니다. 그러나 Windows PowerShell tooinstall 유지 관리 모드 업데이트를 사용 해야 합니다. 

각 업데이트 유형은 아래에 별도로 설명됩니다.

### <a name="regular-updates"></a>일반 업데이트
정기적인 업데이트는 hello 장치가 표준 모드일 때 설치할 수 있도록 정기적인 업데이트 합니다. 이러한 업데이트는 hello Microsoft Update 웹 사이트 tooeach 장치 컨트롤러를 통해 적용 됩니다. 

> [!IMPORTANT]
> 컨트롤러 장애 조치 hello 업데이트 프로세스 중 발생할 수 있습니다. 그러나 시스템 가용성 또는 작업에 영향을 주지 않습니다.
> 
> 

* Tooinstall regular 업데이트 하는 방법을 통해 hello Azure 클래식 포털에 대 한 세부 정보를 참조 하십시오. [hello Azure 클래식 포털을 통해 정기적인 업데이트를 설치](#install-regular-updates-via-the-azure-classic-portal)합니다.
* StorSimple용 Windows PowerShell을 통해 일반 업데이트를 설치할 수도 있습니다. 자세한 내용은 [StorSimple용 Windows PowerShell을 통해 일반 업데이트 설치](#install-regular-updates-via-windows-powershell-for-storsimple)를 참조하세요.

### <a name="maintenance-mode-updates"></a>유지 관리 모드 업데이트
유지 관리 모드 업데이트는 디스크 펌웨어 업그레이드 등의 강제 업데이트입니다. 이러한 업데이트는 hello 장치 toobe 유지 관리 모드로 설정 해야 합니다. 자세한 내용은 [2단계: 입력 유지 관리 모드](#step2)를 참조하세요. Hello Azure 클래식 포털 tooinstall 유지 관리 모드 업데이트를 사용할 수 없습니다. 대신 StorSimple용 Windows PowerShell을 사용해야 합니다. 

Tooinstall 유지 관리 모드 업데이트 하는 방식에 대 한 세부 정보를 참조 하십시오. [StorSimple 용 Windows PowerShell을 통해 설치 유지 관리 모드 업데이트](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple)합니다.

> [!IMPORTANT]
> 유지 관리 모드 업데이트 해야 tooeach 컨트롤러 개별적으로 적용 합니다. 
> 
> 

## <a name="install-regular-updates-via-hello-azure-classic-portal"></a>Hello Azure 클래식 포털을 통해 정기적인 업데이트를 설치 합니다.
Hello Azure 클래식 포털 tooapply 업데이트 tooyour StorSimple 장치를 사용할 수 있습니다.

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a>StorSimple용 Windows PowerShell을 통해 일반 업데이트 설치
또는 StorSimple tooapply (기본 모드) 일반 업데이트에 대 한 Windows PowerShell을 사용할 수 있습니다.

> [!IMPORTANT]
> StorSimple 용 Windows PowerShell을 사용 하 여 정기적인 업데이트를 설치할 수 있지만 hello Azure 클래식 포털을 통해 정기적인 업데이트를 설치 하는 것이 좋습니다. 업데이트 1 부터는 사전 검사 hello 포털에서 수행된 된 이전 tooinstalling 업데이트를 수 있습니다. 이러한 검사는 오류의 사전 파악과 더 원활한 환경을 위한 것입니다. 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a>StorSimple용 Windows PowerShell을 통해 유지 관리 모드 업데이트 설치
StorSimple tooapply 유지 관리 모드 업데이트 tooyour StorSimple 장치에 대 한 Windows PowerShell을 사용합니다. 모든 I/O 요청은 이 모드에서 일시 중지됩니다. 비휘발성 메모리 (NVRAM) 또는 서비스를 클러스터링 하는 hello와 같은 서비스 중지 됩니다. 이 모드를 종료하거나 입력하면 두 컨트롤러 모두 다시 부팅됩니다. 이 모드를 종료 하면 모든 hello 서비스 다시 시작 됩니다 하 고 정상 상태 여야 합니다. (몇 분이 걸릴 수 있습니다.)

Tooapply 유지 관리 모드 업데이트 해야 할 경우 설치 해야 하는 업데이트가 있는지 hello Azure 클래식 포털을 통해 알림을 받게 됩니다. 이 경고에는 StorSimple tooinstall hello 업데이트에 대 한 Windows PowerShell을 사용 하기 위한 지침이 포함 됩니다. 장치를 업데이트 한 후 사용 하 여 hello 동일한 프로시저 toochange hello 장치 tooRegular 모드입니다. 단계별 지침은 [4단계: 유지 관리 모드를 종료](#step4)를 참조하세요.

> [!IMPORTANT]
> * 유지 관리 모드를 설정 하기 전에 hello를 확인 하 여 두 장치 컨트롤러가 모두의 상태가 정상 인지 확인 **하드웨어 상태** hello에 **유지 관리** hello Azure 클래식 포털에서에서 페이지입니다. Hello 컨트롤러 상태가 정상이 아닌 경우 hello 다음 단계에 대 한 Microsoft 지원에 문의 합니다. 자세한 내용은 Microsoft 기술 지원 서비스 tooContact 이동 합니다. 
> * Tooapply 유지 관리 모드에 있는 경우 해야 컨트롤러 하나에 업데이트를 먼저 hello 및 다음에 다른 컨트롤러를 hello 합니다.
> 
> 

### <a name="step-1-connect-toohello-serial-console-a-namestep1"></a>1 단계: toohello 직렬 콘솔에 연결<a name="step1">
PuTTY tooaccess 직렬 콘솔 hello와 같은 응용 프로그램을 먼저 사용 합니다. hello 다음 절차에 설명 방법을 toouse PuTTY tooconnect toohello 직렬 콘솔.

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a>2단계: 유지 관리 모드 시작 <a name="step2">
업데이트 tooinstall 있는지 여부를 결정 하 고 유지 관리 모드 tooinstall 입력 toohello 콘솔을 연결 하면 해당 합니다.

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a>3단계: 프로그램 업데이트 설치 <a name="step3">
다음으로 업데이트를 설치합니다.

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a>4단계: 유지 관리 모드 종료 <a name="step4">
마지막으로, 유지 관리 모드를 종료합니다.

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a>StorSimple용 Windows PowerShell을 통해 핫픽스를 설치합니다.
Microsoft Azure StorSimple에 대한 업데이트와 달리 핫픽스는 공유 폴더에서 설치됩니다. 업데이트와 마찬가지로 두 종류의 핫픽스가 있습니다. 

* 일반 핫픽스 
* 유지 관리 모드 핫픽스  

hello 다음 절차에서는 설명 어떻게 StorSimple tooinstall 일반 및 유지 관리 모드 핫픽스를 Windows PowerShell toouse 합니다.

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-tooupdates-if-you-perform-a-factory-reset-of-hello-device"></a>Hello 장치의 재설정 tooupdates 팩터리를 수행 하는 경우 어떻게 되나요?
장치 재설정 toofactory 설정 이면 모든 hello 업데이트가 손실 됩니다. Hello 공장 재설정 한 장치를 등록 및 구성한 후 StorSimple에 대 한 toomanually hello Azure 클래식 포털 및/또는 Windows PowerShell을 통해 업데이트를 설치 해야 합니다. 공장 기본 설정에 대 한 자세한 내용은 참조 [hello 장치 toofactory 기본 설정으로 초기화](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings)합니다.

## <a name="next-steps"></a>다음 단계
* 에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple tooadminister 용 Windows PowerShell을 사용한](storsimple-windows-powershell-administration.md)합니다.
* 에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple Manager 서비스 tooadminister를 hello를 사용 하 여](storsimple-manager-service-administration.md)합니다.

