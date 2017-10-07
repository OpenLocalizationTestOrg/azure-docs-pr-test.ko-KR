---
title: "aaaReplace StorSimple 8000 시리즈 장치 컨트롤러 | Microsoft Docs"
description: "에 대해 설명 방법을 tooremove StorSimple 8000 시리즈 장치에 하나 또는 두 컨트롤러 모듈을 바꿉니다."
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
ms.openlocfilehash: 76d42529da42dff2a214fb840a52392a7f1a97ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-controller-module-on-your-storsimple-device"></a>StorSimple 장치의 컨트롤러 모듈 교체
## <a name="overview"></a>개요
이 자습서에 설명 어떻게 tooremove 하나 또는 두 컨트롤러 모듈에 StorSimple 장치를 바꿉니다. 또한 hello 기본 hello 단일 및 이중 컨트롤러 교체 시나리오에 대 한 논리를 설명 합니다.

> [!NOTE]
> 이전 tooperforming 컨트롤러 교체를 항상 컨트롤러 펌웨어 toohello 최신 버전을 업데이트 하는 것이 좋습니다.
> 
> tooprevent은 tooyour StorSimple 장치를 손상 시킬, hello Led가 hello 다음 중 하나로 표시 될 때까지 hello 컨트롤러를 꺼내지 마세요.
> 
> * 모든 표시등이 OFF입니다.
> * LED 3, ![녹색 확인 표시 아이콘](./media/storsimple-controller-replacement/HCS_GreenCheckIcon.png), ![빨간색 십자 아이콘](./media/storsimple-controller-replacement/HCS_RedCrossIcon.png) 이 깜박이고 LED 0 및 LED 7이 **켜짐**입니다.


다음 표에서 hello 지원 hello 컨트롤러 교체 시나리오를 보여 줍니다.

| 사례 | 교체 시나리오 | 해당 절차 |
|:--- |:--- |:--- |
| 1 |컨트롤러 하나 실패 상태 이면 hello 다른 컨트롤러는 정상 상태 이며 활성화 합니다. |[단일 컨트롤러 교체](#replace-a-single-controller)를 설명 하는 hello [단일 컨트롤러 교체 논리](#single-controller-replacement-logic), hello 뿐만 아니라 [교체 단계](#single-controller-replacement-steps)합니다. |
| 2 |Hello 두 컨트롤러가 모두 실패 했을 교체 해야 합니다. hello 섀시, 디스크 및 디스크 인클로저가 정상 됩니다. |[이중 컨트롤러 교체](#replace-both-controllers)를 설명 하는 hello [이중 컨트롤러 교체 논리](#dual-controller-replacement-logic), hello 뿐만 아니라 [교체 단계](#dual-controller-replacement-steps)합니다. |
| 3 |컨트롤러에서 동일한 장치 hello 또는 다양 한 장치에서를 교환 합니다. hello 섀시, 디스크 및 디스크 엔클로저는 정상 상태입니다. |슬롯 불일치 경고 메시지가 표시됩니다. |
| 4 |한 컨트롤러가 없고 다른 컨트롤러 실패 hello. |[이중 컨트롤러 교체](#replace-both-controllers)를 설명 하는 hello [이중 컨트롤러 교체 논리](#dual-controller-replacement-logic), hello 뿐만 아니라 [교체 단계](#dual-controller-replacement-steps)합니다. |
| 5 |하나 또는 두 개의 컨트롤러에서 모두 오류가 발생했습니다. Hello 장치 hello 직렬 콘솔 또는 Windows PowerShell 원격을 통해 액세스할 수 없습니다. |수동 컨트롤러 교체 절차는 [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)하세요. |
| 6 |로 인해 수 있는 다른 빌드 버전을 사용 하는 hello 컨트롤러:<ul><li>컨트롤러에는 다양한 소프트웨어 버전이 있습니다.</li><li>컨트롤러에는 다양한 펌웨어 버전이 있습니다.</li></ul> |Hello 컨트롤러 소프트웨어 버전이 다른 경우 hello 교체 논리 것을 감지 하 고 업데이트 hello hello 교체 컨트롤러에서 소프트웨어 버전입니다.<br><br>경우 hello 컨트롤러 펌웨어 버전이 서로 다르고 hello 이전 펌웨어 버전을 **하지** 자동으로 업그레이드할 수 경고 메시지가 hello Azure 포털에에서 표시 됩니다. 업데이트를 검색 하 여 hello 펌웨어 업데이트를 설치 해야 합니다.</br></br>Hello 컨트롤러 펌웨어 버전이 서로 hello 이전 펌웨어 버전을 자동으로 업그레이드 하는 경우 hello 컨트롤러 교체 논리가이 감지 하 고 hello 펌웨어 자동 hello 컨트롤러 시작 된 후 업데이트 됩니다. |

실패에 컨트롤러 모듈 tooremove가 필요 합니다. 단일 컨트롤러 교체 또는 이중 컨트롤러 교체 될 수 있습니다 하나 또는 둘 다 hello 컨트롤러 모듈이 실패할 수 있습니다. 교체 절차와 뒤에 hello 논리 hello 다음을 참조 합니다.

* [단일 컨트롤러 교체](#replace-a-single-controller)
* [두 컨트롤러 모두 교체](#replace-both-controllers)
* [컨트롤러 꺼내기](#remove-a-controller)
* [컨트롤러 삽입](#insert-a-controller)
* [Hello 장치에서 활성 컨트롤러 식별](#identify-the-active-controller-on-your-device)

> [!IMPORTANT]
> 분리 및 교체 컨트롤러를 hello 보안 정보를 검토 하기 전에 [StorSimple 하드웨어 구성 요소 교체](storsimple-8000-hardware-component-replacement.md)합니다.
> 
> 

## <a name="replace-a-single-controller"></a>단일 컨트롤러 교체
실패 하, 오작동 또는 없습니다 hello Microsoft Azure StorSimple 장치 hello 두 컨트롤러 중 하나가 경우 tooreplace 단일 컨트롤러 해야 합니다.

### <a name="single-controller-replacement-logic"></a>단일 컨트롤러 교체 논리
단일 컨트롤러 교체 시 먼저 hello 오류가 발생 한 컨트롤러를 제거 해야 합니다. (hello hello 장치의 나머지 컨트롤러는 활성 컨트롤러가 hello.) Hello 교체 컨트롤러가 삽입 하면 hello 다음 작업이 수행 됩니다.

1. hello 교체 컨트롤러가 즉시 hello StorSimple 장치와 통신을 시작 합니다.
2. Hello 가상 하드 디스크 (VHD) hello 활성 컨트롤러에 대 한 스냅숏은 hello 교체 컨트롤러에 복사 됩니다.
3. hello 교체 컨트롤러가이 VHD에서 시작 되 면 대기 컨트롤러로 인식 될 됩니다 되도록 hello 스냅숏이 수정 됩니다.
4. Hello 수정이 완료 되 면 hello 교체 컨트롤러가 hello 대기 컨트롤러로 시작 됩니다.
5. Hello 두 컨트롤러가 모두 실행 하는 경우 hello 클러스터 온라인 상태가 됩니다.

### <a name="single-controller-replacement-steps"></a>단일 컨트롤러 교체 단계
Hello Microsoft Azure StorSimple 장치에 hello 컨트롤러 중 하나에 오류가 발생 하는 경우 다음 단계를 완료 합니다. (hello 다른 컨트롤러 현재 실행 되 고 있어야 합니다. 두 컨트롤러가 모두 실패 하거나 제대로 작동 하지 않습니다, 너무 이동[이중 컨트롤러 교체 단계](#dual-controller-replacement-steps).)

> [!NOTE]
> Hello 컨트롤러 toorestart 30 ~ 45 분이 걸릴 하 고 hello 단일 컨트롤러 교체 절차에서 완전히 복구할 수 있습니다. hello 케이블 연결까지 포함 하 여 hello 전체 절차에 대 한 hello 총 시간은 약 2 시간입니다.


#### <a name="tooremove-a-single-failed-controller-module"></a>tooremove 단일 오류가 발생 한 컨트롤러 모듈
1. Hello Azure 포털, go toohello StorSimple 장치 관리자 서비스 클릭 **장치**, toomonitor hello 장치 hello 이름을 클릭 하 고 있습니다.
2. 너무 이동**모니터 > 하드웨어 상태가**합니다. 이 실패 했음을 의미 있는 컨트롤러 0 또는 컨트롤러 1의 hello 상태 빨간색 이어야 합니다.
   
   > [!NOTE]
   > 단일 컨트롤러 교체에서 오류가 발생 한 컨트롤러 hello은 항상 대기 컨트롤러입니다.
   
3. 그림 1과 테이블 toolocate hello 오류가 발생 한 컨트롤러 모듈을 다음 hello를 사용 합니다.
   
    ![장치 기본 엔클로저 모듈의 백플레인](./media/storsimple-controller-replacement/IC740994.png)
   
    **그림 1** StorSimple 장치 뒷면
   
   | 레이블 | 설명 |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |컨트롤러 0 |
   | 4 |컨트롤러 1 |
4. Hello 오류가 발생 한 컨트롤러에 hello 데이터 포트에서 모든 연결 된 hello 네트워크 케이블을 제거 합니다. 8600 모델을 사용 하는 경우 hello hello 컨트롤러 toohello EBOD 컨트롤러를 연결 하는 SAS 케이블을 제거 합니다.
5. Hello 단계에 따라 [컨트롤러 제거](#remove-a-controller) tooremove hello 컨트롤러 실패 했습니다.
6. 설치 hello 공장 교체품 hello는 hello 오류가 발생 한 컨트롤러의 동일한 슬롯에서 제거 되었습니다. 이 hello 단일 컨트롤러 교체 논리가 트리거됩니다. 자세한 내용은 [단일 컨트롤러 교체 논리](#single-controller-replacement-logic)를 참조하세요.
7. 단일 컨트롤러 교체 논리가 hello hello 백그라운드에서 진행 되, 동안 hello 케이블 다시 연결 합니다. 모든 hello 케이블 정확 하 게 hello 주의 tooconnect hello 교체 하기 전에 연결 되었던 동일한 방식으로 수행 합니다.
8. Hello 컨트롤러 다시 시작 되 면 확인 hello **컨트롤러 상태** 및 hello **상태 클러스터** hello Azure hello 컨트롤러 포털 tooverify는 뒤로 tooa 정상 상태가 고 대기 모드 인지 합니다.

> [!NOTE]
> Hello 직렬 콘솔을 통해 hello 장치를 모니터링 하는 경우에 hello 컨트롤러 hello 교체 절차에서 복구 되는 동안 여러 번 다시 시작 표시 될 수 있습니다. Hello 직렬 콘솔 메뉴에 표시 되 면 hello 교체가 완료 되 것 합니다. Hello 메뉴의 hello 컨트롤러 교체를 시작 하는 2 시간 이내에 표시 되지 않으면 경우 [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)합니다.
>
> 업데이트 4 부터는 사용할 수도 있습니다 hello cmdlet `Get-HCSControllerReplacementStatus` hello Windows PowerShell 인터페이스의 hello 장치 toomonitor hello hello 컨트롤러 교체 프로세스의 상태에 있습니다.
> 

## <a name="replace-both-controllers"></a>두 컨트롤러 모두 교체
Hello Microsoft Azure StorSimple 장치의 두 컨트롤러가 모두 실패 한 모두 오작동 하거나 없는, 하는 경우 두 컨트롤러 tooreplace 할 수 있습니다. 

### <a name="dual-controller-replacement-logic"></a>이중 컨트롤러 교체 논리
이중 컨트롤러 교체에서는 먼저 오류가 발생한 두 컨트롤러를 모두 제거하고 교체를 삽입합니다. Hello 두 교체 컨트롤러가 삽입 되는 경우 hello 다음 작업이 수행 됩니다.

1. 슬롯 0의에서 교체 컨트롤러가 hello hello 다음을 확인합니다.
   
   1. 사용 하 고 현재 버전의 hello 펌웨어 및 소프트웨어?
   2. 이제 끝났습니다 hello 클러스터의 일부가?
   3. Hello 피어 컨트롤러가 실행 중 이며 클러스터 입니까?
      
      이러한 조건 중 하나도 hello 컨트롤러 hello 최신 매일 백업 찾습니다 (hello에 **nonDOMstorage** S 드라이브에 있음). hello 컨트롤러 hello 백업에서 hello hello VHD의 최신 스냅숏을 복사합니다.
2. 슬롯 0의에서 컨트롤러 hello hello 스냅숏 tooimage 자체를 사용합니다.
3. 한편, 슬롯 1의에서 hello 컨트롤러 컨트롤러 0 toocomplete hello 이미징 및 시작 하는 동안 대기합니다.
4. 컨트롤러 0이 시작 된 후 컨트롤러 1 hello 단일 컨트롤러 교체 논리가 트리거됩니다 있는 컨트롤러 0에 의해 생성 되는 hello 클러스터를 검색 합니다. 자세한 내용은 [단일 컨트롤러 교체 논리](#single-controller-replacement-logic)를 참조하세요.
5. 그 후에 두 컨트롤러가 모두 실행 되 고 hello 클러스터가 온라인 상태가 됩니다.

> [!IMPORTANT]
> 이중 컨트롤러 교체 다음 hello StorSimple 장치를 구성한 후에 반드시 백업을 수행 하는 수동 hello 장치의 합니다. 24시간이 경과할 때까지 일별 장치 구성 백업이 트리거되지 않습니다. 작업할 [Microsoft 지원](storsimple-8000-contact-microsoft-support.md) toomake 장치의 수동 백업 합니다.


### <a name="dual-controller-replacement-steps"></a>이중 컨트롤러 교체 단계
이 워크플로 모두 Microsoft Azure StorSimple 장치에 있는 hello 컨트롤러의 실패 한 경우에 필요 합니다. 이 hello 냉각 시스템의 작동이 중지 하 고 hello 두 컨트롤러가 모두 짧은 기간 내에서 실패 하는 결과적으로, 데이터 센터에서 발생할 수 있습니다. 에 따라 여부 hello StorSimple 장치가 켜져, 설정 또는 해제 하 고 있는지 여부는 8600를 사용 하는 이거나 다른 일련의 단계에는 8100 모델을 필요 합니다.

> [!IMPORTANT]
> Hello 컨트롤러 toorestart 45 분 too1 시간 소요 하 고 이중 컨트롤러 교체 절차에서 완전히 복구할 수 있습니다. hello 케이블 연결까지 포함 하 여 hello 전체 절차에 대 한 hello 총 시간은 약 2.5 시간입니다.

#### <a name="tooreplace-both-controller-modules"></a>tooreplace 두 컨트롤러 모듈
1. Hello 장치 꺼져 있으면이 단계를 건너뛰고 toohello 다음 단계를 진행 합니다. Hello 장치가 켜져 hello 장치 해제 합니다.
   
   1. 8600 모델을 사용 하는 경우 hello 기본 인클로저를 먼저 끈 다음 hello EBOD 인클로저를 끕니다.
   2. Hello 장치가 완전히 종료 될 때까지 기다립니다. Hello 장치의 후면 hello에 모든 hello led가 꺼집니다.
2. 연결 된 toohello 데이터 포트가 있는 모든 hello 네트워크 케이블을 제거 합니다. 8600 모델을 사용 하는 경우 hello hello 기본 인클로저 toohello EBOD 인클로저를 연결 하는 SAS 케이블을 제거 합니다.
3. Hello StorSimple 장치에서 두 컨트롤러를 제거 합니다. 자세한 내용은 [컨트롤러 제거](#remove-a-controller)를 참조하세요.
4. 컨트롤러 0에 대 한 hello 팩터리 교체를 먼저 삽입 하 고 컨트롤러 1을 삽입 합니다. 자세한 내용은 [컨트롤러 삽입](#insert-a-controller)을 참조하세요. 이 hello 이중 컨트롤러 교체 논리가 트리거됩니다. 자세한 내용은 [이중 컨트롤러 교체 논리](#dual-controller-replacement-logic)를 참조하세요.
5. Hello 컨트롤러 교체 논리가 hello 백그라운드에서 진행 되, 동안 hello 케이블 다시 연결 합니다. 모든 hello 케이블 정확 하 게 hello 주의 tooconnect hello 교체 하기 전에 연결 되었던 동일한 방식으로 수행 합니다. Hello 자세한 hello 케이블에서에서 사용 중인 모델에 대 한 방법이 장치 섹션의 참조 [StorSimple 8100 장치 설치](storsimple-8100-hardware-installation.md) 또는 [8600 StorSimple 장치를 설치](storsimple-8600-hardware-installation.md)합니다.
6. Hello StorSimple 장치를 켭니다. 8600 모델을 사용하는 경우:
   
   1. EBOD 인클로저는 hello 먼저 켜져 있는지 확인 합니다.
   2. Hello EBOD 인클로저가 실행 될 때까지 기다립니다.
   3. Hello 기본 인클로저를 켭니다.
   4. Hello 첫 번째 컨트롤러 다시 시작 하는 정상 상태 후 hello 시스템 실행 됩니다.
      
      > [!NOTE]
      > Hello 직렬 콘솔을 통해 hello 장치를 모니터링 하는 경우에 hello 컨트롤러 hello 교체 절차에서 복구 되는 동안 여러 번 다시 시작 표시 될 수 있습니다. Hello 직렬 콘솔 메뉴가 표시 되 면 hello 교체가 완료 되는 것 다음 합니다. Hello 메뉴의 hello 컨트롤러 교체를 시작 2.5 시간 이내에 표시 되지 않으면 경우 [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)합니다.
     
## <a name="remove-a-controller"></a>컨트롤러 꺼내기
StorSimple 장치에서 결함이 있는 컨트롤러 모듈을 프로시저 tooremove 다음 hello를 사용 합니다.

> [!NOTE]
> 다음 일러스트레이션 hello는 컨트롤러 0 적용 됩니다. 컨트롤러 1의 경우 반대가 됩니다.


#### <a name="tooremove-a-controller-module"></a>tooremove 컨트롤러 모듈
1. 엄지와 집게 손가락 사이로 모듈 래치 hello를 파악 합니다.
2. 조심 스럽게 프로그램 엄지와 집게 함께 toorelease hello 컨트롤러 래치를 잡습니다.
   
    ![컨트롤러 래치 해제](./media/storsimple-controller-replacement/IC741047.png)
   
    **그림 2** 컨트롤러 래치 해제
3. Hello 섀시 밖으로 핸들 tooslide hello 컨트롤러로 hello 래치를 사용 합니다.
   
    ![섀시 밖으로 컨트롤러 밀기](./media/storsimple-controller-replacement/IC741048.png)
   
    **그림 3** hello 섀시 밖으로 슬라이딩 hello 컨트롤러

## <a name="insert-a-controller"></a>컨트롤러 삽입
StorSimple 장치에서 결함이 있는 모듈을 제거 후 프로시저 tooinstall 공장 제공 컨트롤러 모듈에 수행 하는 hello를 사용 합니다.

#### <a name="tooinstall-a-controller-module"></a>tooinstall 컨트롤러 모듈
1. 있는지 확인 하십시오. toosee 모든 손상 toohello 인터페이스 커넥터입니다. 손상 되거나 구부러진 커넥터 핀 hello의 경우에 hello 모듈을 설치 하지 마십시오.
2. Hello 래치가 완전히 해제 된 동안 hello 컨트롤러 모듈을 hello 섀시 밀어넣습니다.
   
    ![섀시 안으로 컨트롤러 밀기](./media/storsimple-controller-replacement/IC741053.png)
   
    **그림 4** hello 섀시 안으로 컨트롤러 슬라이딩
3. Hello 컨트롤러 모듈 삽입을 hello 섀시에 계속 toopush hello 컨트롤러 모듈 hello 래치를 닫기 시작 합니다. hello 래치가 제자리 tooguide hello 컨트롤러를 시키면서 맞물립니다.
   
    ![컨트롤러 래치 닫기](./media/storsimple-controller-replacement/IC741054.png)
   
    **그림 5** hello 컨트롤러 래치 닫기
4. 맞아 들어가면 다 hello 래치가 제자리에 있습니다. hello **확인** LED 이제에 있어야 합니다.
   
   > [!NOTE]
   > Hello 컨트롤러 및 LED tooactivate hello에 대 일 분까지 걸릴 수 있으므로 합니다.
  
5. hello 대체가 hello Azure 포털에서에서 성공적인 지 tooverify tooyour 장치 이동한 다음 너무 탐색**모니터** > **하드웨어 상태가**, 있는지 확인 하 고 두 컨트롤러 0 및 컨트롤러 1 요소가 정상 상태 (상태가 녹색).

## <a name="identify-hello-active-controller-on-your-device"></a>Hello 장치에서 활성 컨트롤러 식별
대부분의 경우 처음 장치 등록 하거나 컨트롤러 교체 등 toolocate hello StorSimple 장치에서 활성 컨트롤러를 필요로 하는 있습니다. hello 활성 컨트롤러는 모든 hello 디스크 펌웨어 및 네트워킹 작업을 처리 합니다. Hello 메서드 tooidentify hello 활성 컨트롤러를 다음 중 하나를 사용할 수 있습니다.

* [Hello Azure 포털 tooidentify hello 활성 컨트롤러를 사용 하 여](#use-the-azure-portal-to-identify-the-active-controller)
* [Windows PowerShell을 사용 하 여 StorSimple tooidentify hello 활성 컨트롤러에 대 한](#use-windows-powershell-for-storsimple-to-identify-the-active-controller)
* [Hello 물리적 장치 tooidentify hello 활성 컨트롤러를 확인 합니다.](#check-the-physical-device-to-identify-the-active-controller)

아래에서는 이러한 각 절차에 대해 설명합니다.

### <a name="use-hello-azure-portal-tooidentify-hello-active-controller"></a>Hello Azure 포털 tooidentify hello 활성 컨트롤러를 사용 하 여
Hello Azure 포털에서 장치 tooyour 탐색 한 다음 너무**모니터** > **하드웨어 상태가**, toohello 스크롤합니다 **컨트롤러** 섹션. 여기서 활성 컨트롤러를 확인할 수 있습니다.

![Azure Portal에서 활성 컨트롤러 식별](./media/storsimple-controller-replacement/IC752072.png)

**그림 6** Azure 포털 보여 주는 hello 활성 컨트롤러

### <a name="use-windows-powershell-for-storsimple-tooidentify-hello-active-controller"></a>Windows PowerShell을 사용 하 여 StorSimple tooidentify hello 활성 컨트롤러에 대 한
Hello 직렬 콘솔을 통해 장치에 액세스할 때는 배너 메시지가 표시 됩니다. hello 배너 메시지 hello 모델, 이름, 설치 된 소프트웨어 버전 및 액세스 하는 hello 컨트롤러의 상태와 같은 기본적인 장치 정보가 포함 됩니다. 다음 이미지는 hello는 배너 메시지의 예를 보여 줍니다.

![직렬 배너 메시지](./media/storsimple-controller-replacement/IC741098.png)

**그림 7** 컨트롤러 0을 활성으로 표시하는 배너 메시지

들은 hello 컨트롤러 hello 배너 메시지 toodetermine를 사용할 수 있습니다 toois 활성 또는 수동 연결 합니다.

### <a name="check-hello-physical-device-tooidentify-hello-active-controller"></a>Hello 물리적 장치 tooidentify hello 활성 컨트롤러를 확인 합니다.
사용자의 장치에 tooidentify hello 활성 컨트롤러 hello 파란색 LED를 찾습니다 hello 기본 엔클로저의 뒷면 hello hello DATA 5 포트 위에 있습니다.

이 LED가 깜박이고 있으면 hello 컨트롤러 활성 상태 이며 hello 다른 컨트롤러는 대기 모드에 있습니다. 보조 도구로 테이블 및 다이어그램을 다음 hello를 사용 합니다.

![데이터 포트가 있는 장치 기본 인클로저 백플레인](./media/storsimple-controller-replacement/IC741055.png)

**그림 8** 데이터 포트와 모니터링 LED가 있는 기본 엔클로저 뒷면

| 레이블 | 설명 |
|:--- |:--- |
| 1-6 |DATA 0 - 5 네트워크 포트 |
| 7 |파란색 LED |

## <a name="next-steps"></a>다음 단계
[StorSimple 하드웨어 구성 요소 교체](storsimple-8000-hardware-component-replacement.md)에 대해 자세히 알아봅니다.

