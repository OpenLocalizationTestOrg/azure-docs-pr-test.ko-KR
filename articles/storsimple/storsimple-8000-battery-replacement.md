---
title: "Microsoft Azure StorSimple 8000 시리즈 장치에 배터리 aaaReplace | Microsoft Docs"
description: "Tooremove, 대체를 하 고 StorSimple 장치에서 백업 배터리 모듈 hello를 유지 관리 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 5ac767807e6c3fd817d8d522629db2aceaac9bdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a>StorSimple 장치에서 hello 백업 배터리 모듈 교체

## <a name="overview"></a>개요
hello 기본 인클로저 전원 및 냉각 모듈 (PCM) Microsoft Azure StorSimple 장치에는 추가적인 배터리 팩을 있습니다. 이 팩 hello StorSimple 장치 저장할 수 있도록 데이터의 기본 인클로저를 toohello AC 전원 손실이 발생 해도 power를 제공 합니다. 이 배터리 팩은 참조 tooas hello *백업 배터리 모듈*합니다. hello 백업 배터리 모듈 hello 기본 인클로저 StorSimple 장치에만 존재 하므로 (EBOD 인클로저 hello 백업 배터리 모듈을 포함 되지 않은).

이 자습서에서는 다음을 수행하는 방법을 설명합니다.

* Hello 백업 배터리 모듈을 제거 합니다.
* 새 백업 배터리 모듈 설치
* Hello 백업 배터리 모듈을 유지 관리

> [!IMPORTANT]
> 분리 및 교체 백업 배터리 모듈 hello hello 보안 정보를 검토 하기 전에 [소개 tooStorSimple 하드웨어 구성 요소 교체](storsimple-8000-hardware-component-replacement.md)합니다.


## <a name="remove-hello-backup-battery-module"></a>Hello 백업 배터리 모듈을 제거 합니다.
StorSimple 장치에 대 한 hello 백업 배터리 모듈은 현장 교체 장치입니다. Hello PCM에에서 설치 하기 전에 hello 배터리 모듈 원래 패키지에 저장 되어야 합니다. Hello 단계 tooremove hello 백업 배터리 다음을 수행 합니다.

#### <a name="tooremove-hello-backup-battery-module"></a>tooremove hello 백업 배터리 모듈
1. Azure 포털 hello tooyour StorSimple 장치 관리자 서비스 블레이드를 이동 합니다. 너무 이동**장치** hello 장치 목록에서 장치를 선택 합니다. 너무 이동**모니터** > **하드웨어 상태가**합니다. 아래 **공유 구성 요소의**, hello hello 배터리 상태를 확인 합니다.
2. 배터리는 hello에 실패 했습니다 hello PCM을 식별 합니다. 그림 1 hello hello StorSimple 장치의 후면을 보여 줍니다.
   
    ![장치 기본 엔클로저 모듈의 백플레인](./media/storsimple-battery-replacement/IC740994.png)
   
    **그림 1** PCM 및 컨트롤러 모듈을 표시하는 기본 장치 뒷면
   
   | 레이블 | 설명 |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |컨트롤러 0 |
   | 4 |컨트롤러 1 |
   
    표시기를 모니터링 하는 hello 너무 해당 하는 PCM 0에서 LED를 hello 그림 2에서에서 번호 3으로 표시 된 것과 같이**배터리 결함** 켜져야 합니다.
   
    ![장치 PCM 모니터링 표시기 LED의 백플레인](./media/storsimple-battery-replacement/IC740992.png)
   
    **그림 2** PCM의 후면 보여 주는 hello 모니터링 표시기 Led
   
   | 레이블 | 설명 |
   |:--- |:--- |
   | 1 |AC 전원 오류 |
   | 2 |팬 오류 |
   | 3 |배터리 결함 |
   | 4 |PCM 정상 |
   | 5 |DC 전원 오류 |
   | 6 |배터리 정상 |
3. 실패 한 배터리 tooremove hello PCM에서 다음과 같이 hello [PCM 제거](storsimple-power-cooling-module-replacement.md#remove-a-pcm)합니다.
4. PCM 제거 hello, 리프트 및 회전 hello 배터리 모듈 hello 다음 그림에에서 표시 된 대로 위쪽으로 처리 하 고 tooremove hello 배터리 꺼내 합니다.
   
    ![PCM에서 배터리 꺼내기](./media/storsimple-battery-replacement/IC741019.png)
   
    **그림 3** hello PCM에서에서 배터리 hello 제거
5. Hello 현장 교체 장치 패키지에 hello 모듈을 배치 합니다.
6. 적절 한 수리와 처리에 대 한 hello 결함 있는 장치 tooMicrosoft를 반환 합니다.

## <a name="install-a-new-backup-battery-module"></a>새 백업 배터리 모듈 설치
Hello 단계 tooinstall hello 교체 배터리 모듈 hello 기본 인클로저 StorSimple 장치에 PCM hello에서 다음을 수행 합니다.

#### <a name="tooinstall-hello-battery-module"></a>tooinstall hello 배터리 모듈
1. Hello PCM에서에서 적절 한 방향을 hello에 hello 백업 배터리 모듈을 배치 합니다.
2. 케이블 hello 배터리 모듈을 눌러 모든 hello 방식으로 tooseat hello 커넥터를 처리 합니다.
3. 대체 hello 지침에 따라 hello 기본 인클로저에서 PCM hello [StorSimple 장치에서 전원 및 냉각 모듈 교체](storsimple-power-cooling-module-replacement.md)합니다.
4. Hello 교체가 완료 되 면 후 tooyour 장치를 이동 하 고 이동 하 여 너무**모니터** > **하드웨어 상태가** hello Azure 포털의에서. Hello 상태의 hello 배터리 toomake hello 설치가 제대로 수행 되었는지 확인 합니다. 녹색 상태 hello 배터리 정상 임을 나타냅니다.

## <a name="maintain-hello-backup-battery-module"></a>Hello 백업 배터리 모듈을 유지 관리
StorSimple 장치 hello 백업 배터리 모듈 전원 손실 이벤트가 발생 하는 동안 전원 toohello 컨트롤러를 제공합니다. 제어 된 방식으로 hello StorSimple 장치 toosave 중요 한 데이터가 이전 tooshutting을 아래로 수 있습니다. Hello Pcm의에서 완전히 충전 된 배터리 두 hello 시스템 두 개의 연속 된 손실 이벤트를 처리할 수 있습니다.

Hello Azure 포털에서에서 hello **하드웨어 상태가** hello에서 **모니터** 블레이드 hello 배터리가 오작동 하거나 hello 수명 끝에 도달 하 고 있는지 여부를 나타냅니다. hello 배터리 상태를 나타냅니다 **PCM 0의에서 배터리** 또는 **PCM 1의 배터리** 아래 **공유 구성 요소의**합니다. 이 블레이드에서 사용 기간 종료가 임박한 경우 **DEGRADED** 상태가 표시되고 사용 기간이 종료된 경우 **FAILED** 상태가 표시됩니다.

> [!NOTE]
> hello 배터리를 보고할 수 **실패** 단순히 청구 toobe 필요 경우.


경우 hello **DEGRADED** 상태가 나타나면 다음 조치 hello 것이 좋습니다.

* hello 시스템 최근 전원 손실이 발생 했을 수 있습니다 또는 hello 배터리에서 정기적으로 유지 관리 모드로 전환 될 수 있습니다. 계속 하기 전에 12 시간 동안 hello 시스템을 확인 합니다.
  
  * Hello 상태가 여전히 **DEGRADED** 배터리 교체 toobe 필요한 hello 사용 하 여 지속적으로 연결 tooAC 전원 12 시간 컨트롤러와 pcm을 실행 하면서 다음 hello 후 합니다. 교체 백업 배터리 모듈에 대해서는 [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md) 하세요.
  * 12 시간 후 정상 hello 상태가 되 면 hello 배터리가 정상적으로 작동 하 고 유지 관리 비용이 청구만 필요 합니다.
* 발생 되지 않은 경우는 관련된 AC 전원 손실과 hello PCM 켜져 있고 연결 tooAC 전원, hello 배터리 교체 toobe가 필요 합니다. [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md) tooorder 교체 백업 배터리 모듈입니다.

> [!IMPORTANT]
> Hello의 dispose toonational 및 지역 규정에 따라 배터리에 실패 했습니다.

## <a name="next-steps"></a>다음 단계
[StorSimple 하드웨어 구성 요소 교체](storsimple-8000-hardware-component-replacement.md)에 대해 자세히 알아봅니다.

