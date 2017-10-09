---
title: "StorSimple 8000 시리즈 장치에 PCM aaaReplace | Microsoft Docs"
description: "어떻게 tooremove 및 바꾸기 hello 전원 및 냉각 모듈 (PCM) StorSimple 장치에 설명"
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
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 474fd09787c5361a81efda4de74356027ac60f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a>StorSimple 장치의 전원 및 냉각 모듈 교체
## <a name="overview"></a>개요
hello 전원 및 냉각 모듈 (PCM)에서 Microsoft Azure StorSimple 장치에 전원 공급 장치 및 냉각 팬 hello 기본 인클로저와 EBOD 인클로저를 통해 제어 되는 이루어져 있습니다. 각 엔클로저마다 인증된 PCM 모델 하나만 있습니다. hello 기본 인클로저는 764w PCM에 대 한 인증 및 hello EBOD 인클로저는 580w PCM에 대해 인증 됩니다. Hello 기본 인클로저와 EBOD 인클로저 hello에 대 한 hello Pcm이 서로 다르기는 하지만 hello 교체 절차는 동일 합니다.

이 자습서에서는 다음을 수행하는 방법을 설명합니다.

* PCM 꺼내기
* 교체 PCM 설치

> [!IMPORTANT]
> 제거 하 고는 PCM을 교체 hello 보안 정보를 검토 하기 전에 [StorSimple 하드웨어 구성 요소 교체](storsimple-8000-hardware-component-replacement.md)합니다.


## <a name="before-you-replace-a-pcm"></a>PCM을 교체하기 전에
PCM을 교체 하기 전에 중요 한 문제를 따라 hello 유의 해야 합니다.

* Hello 전원 공급을 하는 경우 hello PCM에 오류가 발생 하면 hello 결함이 있는 모듈은 설치 된 가지만 hello 전원 코드를 제거 합니다. hello 팬 hello 인클로저에서 tooreceive 전원 고 tooprovide 적절 한 냉각을 계속 진행 됩니다. Hello 팬에 오류가 발생 하는 경우 즉시 바뀝니다 toobe hello PCM에 필요 합니다.
* Hello PCM을 제거 하기 전에 hello 기본 스위치 (있는 경우) 해제 하 여 또는 hello 전원 코드를 물리적으로 제거 하 여 hello 전원을 hello PCM에서에서 분리 합니다. 이 전원 공급이 중단 임박 임을 경고 tooyour 시스템을 제공 합니다.
* 있는지 확인 하십시오 다른 PCM이 작동 하는 hello 결함이 있는 PCM hello 교체 하기 전에 시스템 작업을 계속 합니다. 가능한 한 빨리 결함이 있는 PCM을 완벽하게 작동하는 PCM으로 교체해야 합니다.
* PCM 모듈 교체만 몇 분 toocomplete, 걸리지만 제거 하지 못했습니다 hello PCM tooprevent 과열 10 분 내에 완료 해야 합니다.
* Note hello 대체 764 PCM 모듈 hello 공장에서 출고 hello 백업 배터리 모듈에 포함 되지 않도록 합니다. 결함이 있는 PCM에서 tooremove hello 배터리 필요한 쿼리하고 hello 교체 모듈 이전 tooperforming hello 교체에 삽입 합니다. 자세한 내용은 참조 방법을 너무[제거 하 고 백업 배터리 모듈을 삽입](storsimple-8000-battery-replacement.md)합니다.

## <a name="remove-a-pcm"></a>PCM 꺼내기
Microsoft Azure StorSimple 장치에서 준비 tooremove 전원 및 냉각 모듈 (PCM) 있을 때는 다음이 지침을 따르세요.

> [!NOTE]
> PCM을 제거 하기 전에 올바른 교체품 (764w 기본 인클로저 hello) 또는 EBOD 인클로저의 hello에 대 한 580w 있는지 확인 합니다.

#### <a name="tooremove-a-pcm"></a>tooremove pcm 분리
1. Hello Azure 클래식 포털에서에서 클릭 **설정 > 모니터 > 하드웨어 상태가**합니다. PCM 구성 hello의 hello 상태를 확인 **공유 구성 요소** tooidentify PCM 실패 했습니다.
   
   * PCM 0의에서 전원 공급 장치에 실패 한 경우의 상태를 hello **PCM 0의에서 전원 공급 장치** 빨강으로 표시 됩니다.
   * PCM 1의 전원 공급 장치에 실패 한 경우의 상태를 hello **PCM 1의 전원 공급 장치** 빨강으로 표시 됩니다.
   * PCM 1의 hello 팬에 실패 한 경우의 상태를 hello **0 PCM 0의 냉각** 또는 **PCM 0의 냉각 1** 빨강으로 표시 됩니다.
2. Hello를 hello 기본 인클로저의 백업 hello에 오류가 발생 한 PCM을 찾습니다. 8600 모델을 실행 하는 경우 hello hello 전면 패널 LED 디스플레이에 표시 된 시스템 장치 식별 번호를 확인 하 여 hello 기본 인클로저를 식별 합니다. 기본 장치 ID hello 기본 인클로저에 표시 되는 hello **00**, hello 기본 단위 ID EBOD 인클로저 hello에 표시 되는 반면, **01**합니다. hello 다음 다이어그램과 테이블 설명 hello LED 디스플레이의 전면 패널 hello 합니다.
   
    ![전면 OPS 패널의 시스템 ID](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     **그림 1** hello 장치의 전면 패널  
   
   | 레이블 | 설명 |
   |:--- |:--- |
   | 1 |음소거 단추 |
   | 2 |시스템 전원 |
   | 3 |모듈 결함 |
   | 4 |논리적 결함 |
   | 5 |장치 ID 디스플레이 |
3. 모니터링 표시기 Led hello hello 기본 인클로저 후면의 hello는 tooidentify hello 결함이 있는 PCM 합니다. Hello 다음 다이어그램 및 toounderstand 어떻게 테이블을 참조 toouse hello Led toolocate hello 결함이 있는 PCM 합니다. 예를 들어 경우 hello 초래한 해당 toohello **팬 오류** 가 켜지 면 hello 팬 실패 했습니다. 마찬가지로, 경우 hello 초래한 너무 해당**AC 오류** 가 켜지 면 전원 공급 장치 hello 실패 했습니다. 
   
    ![장치 PCM 모니터링 표시기 LED의 백플레인](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     **그림 2** 표시기 LED가 있는 PCM 뒷면
   
   | 레이블 | 설명 |
   |:--- |:--- |
   | 1 |AC 전원 오류 |
   | 2 |팬 오류 |
   | 3 |배터리 결함 |
   | 4 |PCM 정상 |
   | 5 |DC 전원 오류 |
   | 6 |배터리 정상 |
4. Toohello hello hello StorSimple 장치 toolocate 실패 hello PCM 모듈 뒷면의 다이어그램을 다음을 참조 하십시오. PCM 0 hello 왼쪽에 있고 PCM 1은 오른쪽 hello 합니다. hello 표는 hello 모듈에 설명 합니다.
   
     ![장치 기본 엔클로저 모듈의 백플레인](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     **그림 3** 플러그 인 모듈이 있는 장치 뒷면 
   
   | 레이블 | 설명 |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |컨트롤러 0 |
   | 4 |컨트롤러 1 |
5. 설정 해제 결함이 있는 PCM hello 및 hello 전원 공급 장치 코드를 분리 합니다. 이제 PCM hello를 제거할 수 있습니다.
6. 엄지와 집게, PCM을 처리 하는 hello의 hello 래치 및 hello 잡고 함께 tooopen hello 핸들에 동시에 누르면 합니다.
   
    ![PCM 핸들 열기](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    **그림 4** Opening hello PCM 처리
7. Hello 핸들을 잡고 PCM hello를 제거 합니다.
   
    ![장치 PCM 꺼내기](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    **그림 5** PCM 제거 하는 hello

## <a name="install-a-replacement-pcm"></a>교체 PCM 설치
이러한 지침은 tooinstall StorSimple 장치에서 PCM을 따릅니다. Hello 백업 배터리 모듈 이전 tooinstalling hello 교체 PCM (too764 W Pcm만 적용 됨)를 삽입 했는지 확인 합니다. 자세한 내용은 참조 방법을 너무[제거 하 고 백업 배터리 모듈을 삽입](storsimple-8000-battery-replacement.md)합니다.

#### <a name="tooinstall-a-pcm"></a>tooinstall pcm 분리
1. Hello 올바른 교체용 PCM이 인클로저의 수 있는지 확인 하십시오. hello 기본 인클로저는 764w PCM 되어야 하며 hello EBOD 인클로저는 580w PCM 필요 합니다. Toouse 해서는 안 hello 580w PCM hello 기본 인클로저에서 또는 EBOD 인클로저 hello에 764w PCM 환영 합니다. 다음 이미지는 hello hello에 대 한이 정보 즉 레이블을 tooidentify toohello PCM을 추가 하는 위치를 보여 줍니다.
   
    ![장치 PCM 레이블](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    **그림 6** PCM 레이블
2. 손상 toohello 인클로저, 특히 주의 toohello 커넥터를 확인 합니다. 
   
   > [!NOTE]
   > **구부러진 핀이 있는 경우에 hello 모듈을 설치 하지 마십시오.**
   > 
   > 
3. Hello에 PCM을 처리 하는 hello 위치, 슬라이드 hello 모듈 hello 인클로저도을 엽니다.
   
    ![장치 PCM 설치](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    **그림 7** 설치 hello PCM
4. 수동으로 hello PCM 핸들을 닫습니다. Hello 핸들 래치가 맞물릴 때 처럼 한 번의 클릭을 들려야 합니다.
   
   > [!NOTE]
   > 커넥터 핀 hello tooensure 있습니다 부드럽게 잡아당겨 보면 hello 핸들 hello 래치를 해제 하지 않고 참여 했습니다. Hello PCM이 빼내 참여 하는 hello 커넥터 하기 전에 해당 hello 래치 닫혔습니다 의미 합니다.
   
5. Hello 전원 케이블 toohello 전원과 PCM toohello 연결 합니다.
6. 릴리프 베일을 고정 hello 부담을 보호 합니다.
7. Hello PCM 켭니다.
8. Hello 교체에 성공 했는지 확인: hello StorSimple 장치 관리자 서비스의 Azure 포털에서에서 tooyour 장치 이동 했다가 너무**설정 > 모니터 > 하드웨어 상태가**합니다. Hello에서 **공유 구성 요소**, hello PCM의 hello 상태가 녹색으로 바뀝니다.
   
   > [!NOTE]
   > Hello 교체 PCM toocompletely initialize 몇 분 정도 걸릴 수 있습니다.

## <a name="next-steps"></a>다음 단계
[StorSimple 하드웨어 구성 요소 교체](storsimple-8000-hardware-component-replacement.md)에 대해 자세히 알아봅니다.

