---
title: "StorSimple 장치 모드 aaaChange | Microsoft Docs"
description: "Hello StorSimple 장치 모드에 설명 하 고 설명 방법을 toochange StorSimple에 대 한 Windows PowerShell toouse hello 장치 모드입니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 058ca6cc38954bce3679cc21b39d341b10cb4dfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-device-mode-on-your-storsimple-device"></a>StorSimple 장치에 사용 되는 hello 장치 모드 변경

이 문서에서는 hello에 대 한 간략 한 설명을 StorSimple 장치 작동할 수 있는 다양 한 모드를 제공 합니다. StorSimple 장치는 표준, 유지 관리 및 복구의 세 가지 모드로 작동할 수 있습니다.

이 문서를 읽은 후 다음에 대해 알 수 있습니다.

* Hello StorSimple 장치 모드 이란
* 에 어떻게 모드 아웃 toofigure hello StorSimple 장치
* 어떻게 일반 toomaintenance 모드에서 toochange 및 *반대의*

관리 작업 위에 hello StorSimple 장치의 Windows PowerShell 인터페이스 hello 통해 수행할 수만 있습니다.

## <a name="about-storsimple-device-modes"></a>StorSimple 장치 모드

StorSimple 장치는 표준, 유지 관리 또는 복구 모드로 작동할 수 있습니다. 각 모드는 아래에 간단하게 설명되어 있습니다.

### <a name="normal-mode"></a>표준 모드

완전히 구성 된 StorSimple 장치에 대 한 hello 표준 작동 모드로 정의 됩니다. 기본적으로 장치는 표준 모드에 있어야 합니다.

### <a name="maintenance-mode"></a>유지 관리 모드

경우에 따라 hello StorSimple 장치 해야 toobe 유지 관리 모드로 설정 합니다. 이 모드 hello 장치에서 tooperform 유지 관리를 허용 하 고 관련 toodisk 펌웨어 같은 중단 업데이트를 설치 합니다.

StorSimple 용 Windows PowerShell hello 통해서만 유지 관리 모드로 hello 시스템을 넣을 수 있습니다. 모든 I/O 요청은 이 모드에서 일시 중지됩니다. 비휘발성 메모리 (NVRAM) 또는 서비스를 클러스터링 하는 hello와 같은 서비스 중지 됩니다. 이 모드를 종료 하거나 입력 하면 두 hello 컨트롤러 다시 시작 됩니다. Hello 유지 관리 모드를 종료 하면 모든 hello 서비스 다시 시작 됩니다 하 고 정상 상태 여야 합니다. 몇 분이 걸릴 수 있습니다.

> [!NOTE]
> **유지 관리 모드는 정상적으로 작동하는 장치에만 지원됩니다. hello 컨트롤러 중 하나 이상이 작동 하지 않는 장치에서 지원 되지 않습니다.**


### <a name="recovery-mode"></a>복구 모드

복구 모드는 "네트워크를 지원하는 Windows 안전 모드"로 설명될 수 있습니다. 복구 모드 hello Microsoft 지원 팀 있으며 hello 시스템에 tooperform 진단 있습니다. 복구 모드의 기본 목표는 hello tooretrieve hello 시스템 로그 됩니다.

시스템이 복구 모드로 전환되는 경우 Microsoft 지원에 다음 단계를 문의해야 합니다. 자세한 내용은 이동 너무[Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)합니다.

> [!NOTE]
> **복구 모드에서 hello 장치를 추가할 수 없습니다. Hello 장치가 비정상적인 상태 이면 복구 모드는 Microsoft 기술 지원 담당자가 검사할 수 상태로 tooget hello 장치를 시도 합니다.**

## <a name="determine-storsimple-device-mode"></a>StorSimple 장치 모드 확인

#### <a name="toodetermine-hello-current-device-mode"></a>toodetermine hello 현재 장치 모드

1. Hello 단계를 수행 하 여 toohello 장치 직렬 콘솔에 로그온 [PuTTY를 사용 하 여 장치 직렬 콘솔 tooconnect toohello](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)합니다.
2. Hello 장치의 hello 직렬 콘솔 메뉴에서 hello 배너 메시지를 확인 합니다. 이 메시지는 명시적으로 hello 장치 유지 관리 나 복구 모드 인지 여부를 나타냅니다. Hello 메시지 toohello 시스템 모드와 관련 된 특정 정보 없으면 hello 장치가 표준 모드입니다.

## <a name="change-hello-storsimple-device-mode"></a>Hello StorSimple 장치 모드 변경

유지 관리 모드 업데이트를 설치 하거나 hello StorSimple 장치가 유지 관리 모드 (기본 모드)에서 tooperform 유지 관리에 배치할 수 있습니다. Hello 프로시저 tooenter 또는 끝내기 유지 관리 모드를 다음을 수행 합니다.

> [!IMPORTANT]
> 유지 관리 모드를 설정 하기 전에 hello에 액세스 하 여 두 장치 컨트롤러가 모두의 상태가 정상 인지 확인 **장치 설정 > 하드웨어 상태가** hello Azure 포털에서에서 장치에 대 한 합니다. 하나 또는 두 개의 hello 컨트롤러 요소가 비정상적인 경우 hello 다음 단계에 대 한 Microsoft 지원에 문의 합니다. 자세한 내용은 이동 너무[Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)합니다.
 

#### <a name="tooenter-maintenance-mode"></a>tooenter 유지 관리 모드

1. Hello 단계를 수행 하 여 toohello 장치 직렬 콘솔에 로그온 [PuTTY를 사용 하 여 장치 직렬 콘솔 tooconnect toohello](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)합니다.
2. Hello 직렬 콘솔 메뉴에서 옵션 1, 선택 **전체 권한으로 로그인**합니다. 메시지가 표시 되 면 제공 hello **장치 관리자 암호**합니다. hello 기본 암호는: `Password1`합니다.
3. Hello 명령 프롬프트에 입력 
   
    `Enter-HcsMaintenanceMode`
4. 유지 관리 모드를 사용 하는 알려 주는 경고 메시지가 모든 I/O 요청이 중단 되며 서버 hello 연결 toohello Azure 포털 및 확인을 묻는 메시지가 나타납니다. 형식 **Y** tooenter 유지 관리 모드입니다.
5. 두 컨트롤러가 모두 다시 시작됩니다. Hello를 다시 시작이 완료 되 면 hello 직렬 콘솔 배너 hello 장치가 유지 관리 모드에서 해당 표시 됩니다. 샘플 출력은 다음과 같습니다.

```
    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Controller0>Enter-HcsMaintenanceMode
    Checking device state...

    In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>

```

#### <a name="tooexit-maintenance-mode"></a>tooexit 유지 관리 모드

1. Toohello 장치 직렬 콘솔에 로그온 합니다. 장치가 유지 관리 모드에 있는 hello 배너 메시지에서 확인 하십시오.
2. Hello 명령 프롬프트에서 다음을 입력 합니다.
   
    `Exit-HcsMaintenanceMode`
3. 경고 메시지와 확인 메시지가 표시됩니다. 형식 **Y** tooexit 유지 관리 모드입니다.
4. 두 컨트롤러가 모두 다시 시작됩니다. Hello를 다시 시작이 완료 되 면 hello 직렬 콘솔 배너 해당 hello 장치가 표준 모드일에서 임을 나타냅니다. 샘플 출력은 다음과 같습니다.

```
    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0
    ---------------------------------------------------------------

    Controller0>Exit-HcsMaintenanceMode
    Checking device state...

    Before exiting maintenance mode, ensure that any updates that are required on both controllers have been applied. Failure tooinstall on each controller could result in data corruption. Exiting maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooexit maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Active
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>
```

## <a name="next-steps"></a>다음 단계

너무 방법에 대해 알아봅니다[normal 및 유지 관리 모드 업데이트를 적용](storsimple-update-device.md) StorSimple 장치에 있습니다.

