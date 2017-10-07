---
title: "데이터 0 aaaModify StorSimple 8000 시리즈 장치에 설정을 | Microsoft Docs"
description: "자세한 내용은 StorSimple tooreconfigure에 대 한 Windows PowerShell toouse StorSimple 장치에서 DATA 0 네트워크 인터페이스를 hello 하는 방법입니다."
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
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: 2d3bdd3675017be86def45a81d94b6c03fc61da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-data-0-network-interface-settings-on-your-storsimple-8000-series-device"></a>StorSimple 8000 시리즈 장치에 hello DATA 0 네트워크 인터페이스 설정을 수정 합니다.

## <a name="overview"></a>개요

Microsoft Azure StorSimple 장치에는 DATA 0에서에서 6 개의 네트워크 인터페이스 tooDATA 5입니다. hello DATA 0 인터페이스는 항상 hello Windows PowerShell 인터페이스 또는 hello 직렬 콘솔을 통해 구성 및 자동으로 클라우드 사용 됩니다. 참고 hello Azure 포털을 통해 DATA 0 네트워크 인터페이스를 구성할 수 없습니다.

hello DATA 0 인터페이스는 처음 hello StorSimple 장치의 초기 배포 시 hello 설치 마법사를 통해 구성 됩니다. 데이터 0 tooreconfigure hello 장치가 작동 모드에 있을 때 할 수 있습니다 설정 합니다. 이 자습서는 StorSimple 용 Windows PowerShell을 통해 모두 toomodify DATA 0 네트워크 설정을 두 개의 메서드를 제공합니다.

이 자습서를 읽은 후에 다음을 수행할 수 있습니다.

* 수정 DATA 0 네트워크 hello 설치 마법사를 통해 설정
* DATA 0 네트워크 설정을 hello 통해 수정 `Set-HcsNetInterface` cmdlet

## <a name="modify-data-0-network-settings-through-setup-wizard"></a>설정 마법사를 통해 DATA 0 네트워크 설정 수정
StorSimple 장치의 toohello Windows PowerShell 인터페이스를 연결 하 고 설치 마법사 세션을 시작 하 여 DATA 0 네트워크 설정을 재구성할 수 있습니다. 다음 단계 toomodify DATA 0 hello 수행 설정:

#### <a name="toomodify-data-0-network-settings-through-setup-wizard"></a>설치 마법사를 통해 toomodify DATA 0 네트워크 설정
1. Hello 직렬 콘솔 메뉴에서 옵션 1, 선택 **전체 권한으로 로그인**합니다. 메시지가 표시 되 면 hello 제공 **장치 관리자 암호**합니다. hello 기본 암호는 `Password1`합니다.
2. Hello 명령 프롬프트에서 다음을 입력 합니다.
   
    `Invoke-HcsSetupWizard`
3. 설치 마법사가 toohelp 나타나면 DATA 0 hello 구성 장치의 인터페이스입니다. Hello IP 주소, 게이트웨이 및 네트워크 마스크에 대 한 새 값을 제공 합니다.

> [!NOTE]
> 고정 컨트롤러 Ip toobe hello를 통해 다시 구성 해야 합니다는 hello **네트워크 설정** hello Azure 포털에에서 표시 되는 hello StorSimple 장치의 블레이드 합니다. 자세한 내용은 이동 너무[네트워크 인터페이스 수정](storsimple-8000-modify-device-config.md#modify-network-interfaces)합니다.

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a>Set-HcsNetInterface cmdlet을 통해 DATA 0 네트워크 설정 수정
대체 방식으로 tooreconfigure DATA 0 네트워크 인터페이스는 hello hello 사용을 통해 `Set-HcsNetInterface` cmdlet. hello cmdlet은 StorSimple 장치의 hello Windows PowerShell 인터페이스에서 실행 됩니다. 이 절차를 사용 하 여 hello 컨트롤러 고정 Ip 여기 구성할 수도 있습니다. 다음 단계 toomodify hello DATA 0 hello 수행 설정: 

#### <a name="toomodify-data-0-network-settings-through-hello-set-hcsnetinterface-cmdlet"></a>hello Set-hcsnetinterface cmdlet 통해 toomodify DATA 0 네트워크 설정
1. Hello 직렬 콘솔 메뉴에서 옵션 1, 선택 **전체 권한으로 로그인**합니다. 메시지가 표시 되 면 hello 장치 관리자 암호를 제공 합니다. hello 기본 암호는 `Password1`합니다.
2. Hello 명령 프롬프트에서 다음을 입력 합니다.
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    각 진 hello 대괄호로 hello DATA 0에 대 한 다음 값을 입력 합니다.
   
   * IPv4 주소
   * IPv4 게이트웨이
   * IPv4 서브넷 마스크
   * 컨트롤러 0에 대한 고정 IPv4 주소
   * 컨트롤러 1에 대한 고정 IPv4 주소
     
     이 cmdlet의 hello 사용에 자세한 내용은 이동 너무[용 Windows PowerShell StorSimple cmdlet 참조](https://technet.microsoft.com/library/dn688161.aspx)합니다.

## <a name="next-steps"></a>다음 단계
* 데이터 0 이외의 tooconfigure 네트워크 인터페이스, hello를 사용할 수 있습니다 [hello Azure 포털에서에서 네트워크 설정을 구성](storsimple-8000-modify-device-config.md)합니다. 
* 네트워크 인터페이스를 구성할 때 문제가 발생 하면 너무 참조[배포 문제를 해결](storsimple-troubleshoot-deployment.md)합니다.

