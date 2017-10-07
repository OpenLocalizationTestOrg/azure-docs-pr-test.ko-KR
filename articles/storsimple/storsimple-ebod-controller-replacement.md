---
title: "StorSimple EBOD 컨트롤러 aaaReplace | Microsoft Docs"
description: "에 대해 설명 방법을 tooremove StorSimple 8600 장치의 EBOD 컨트롤러를 하나 또는 둘 다를 바꿉니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8cbfa507-1a56-4e24-99dd-7db9abd3b850
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 5d29de2ee30bfdd70910050eee5cfa1d293d444f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a>StorSimple 장치의 EBOD 컨트롤러 교체
## <a name="overview"></a>개요
이 자습서에 설명 방법을 tooreplace Microsoft Azure StorSimple 장치에서 결함이 있는 EBOD 컨트롤러 모듈입니다. EBOD 컨트롤러 모듈 tooreplace 해야합니다.

* Hello 결함이 있는 EBOD 컨트롤러 제거
* 새 EBOD 컨트롤러 설치

Hello를 시작 하기 전에 다음 정보를 고려 합니다.

* 사용하지 않은 모든 슬롯에 빈 EBOD 모듈을 삽입해야 합니다. 슬롯을 남겨 둘지 hello 인클로저가 제대로 식 지 않습니다.
* hello EBOD 컨트롤러는 핫 스왑 가능한 제거 하거나 교체할 수 있습니다. 교체가 있을 때까지 오류가 발생한 모듈을 꺼내지 마세요. Hello 교체 프로세스를 시작 하면 10 분 내에 완료 해야 합니다.

> [!IMPORTANT]
> Tooremove 시도 하기 전에 모든 StorSimple 구성 요소 교체, hello 검토 해야 또는 [안전 아이콘 규칙](storsimple-safety.md#safety-icon-conventions) 및 기타 [안전 조치](storsimple-safety.md)합니다.
> 
> 

## <a name="remove-an-ebod-controller"></a>EBOD 컨트롤러 꺼내기
전에 hello을 바꾸지 못했으므로 StorSimple 장치에 EBOD 컨트롤러 모듈, 있어야 해당 hello 다른 EBOD 컨트롤러 모듈이 활성화 되어 실행 합니다. hello 다음 절차와 테이블에 설명 tooremove EBOD 컨트롤러 모듈을 hello 하는 방법입니다.

#### <a name="tooremove-an-ebod-module"></a>tooremove EBOD 모듈
1. Azure 클래식 포털 hello를 엽니다.
2. 너무 이동**장치** > **유지 관리** > **하드웨어 상태**, hello의 hello 상태에 대 한 원인이 있는지 확인 하 고 활성 EBOD hello 컨트롤러는 녹색 하 고 실패 hello EBOD 컨트롤러 모듈에 대 한 hello LED가 빨간색입니다.
3. Hello hello 장치 뒷면에서 실패 하는 hello EBOD 컨트롤러 모듈을 찾습니다.
4. Hello EBOD 모듈 hello 시스템 꺼내기 전에 EBOD 컨트롤러 모듈 toohello 컨트롤러 hello를 연결 하는 hello 케이블을 제거 합니다.
5. 연결 된 toohello 컨트롤러 hello EBOD 컨트롤러 모듈의 hello 정확한 SAS 포트를 기록해 둡니다. Hello EBOD 모듈을 교체한 후 필요한 toorestore hello 시스템 toothis 구성 됩니다. 
   
   > [!NOTE]
   > 일반적으로 포트 A로 표시 된 됩니다 **에서 호스팅할** hello 다이어그램 뒤에 있습니다.
   > 
   > 
   
    ![EBOD 컨트롤러의 백플레인](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     **그림 1** EBOD 모듈 뒷면
   
   | 레이블 | 설명 |
   |:--- |:--- |
   | 1 |오류 LED |
   | 2 |전원 LED |
   | 3 |SAS 커넥터 |
   | 4 |SAS LED |
   | 5 |팩터리 전용 직렬 포트 |
   | 6 |포트 A(호스트 인) |
   | 7 |포트 B(호스트 아웃) |
   | 8 |포트 C(팩터리 전용) |

## <a name="install-a-new-ebod-controller"></a>새 EBOD 컨트롤러 설치
hello 다음 절차와 테이블에 설명 방법을 tooinstall StorSimple 장치에 EBOD 컨트롤러 모듈입니다.

#### <a name="tooinstall-an-ebod-controller"></a>EBOD 컨트롤러 tooinstall
1. Hello EBOD 장치를 특히 toohello 인터페이스 커넥터 손상 되지 않았는지 확인 하십시오. 구부러진 핀 하는 경우에 hello 새 EBOD 컨트롤러를 설치 하지 마십시오.
2. Hello에 hello 래치 위치, 슬라이드 hello 모듈 hello 인클로저 hello 맞물릴 때까지으로 엽니다.
   
    ![EBOD 컨트롤러 설치](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    **그림 2** hello EBOD 컨트롤러 모듈 설치
3. 래치 닫기 hello 합니다. Hello 래치가 맞물릴 때 처럼 한 번의 클릭을 들려야 합니다.
   
    ![EBOD 래치 해제](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    **그림 3** hello EBOD 모듈 래치 닫기
4. Hello 케이블 다시 연결 합니다. Hello hello 교체 하기 전에 있었던 정확한 구성을 사용 합니다. Hello 다이어그램을 다음 참조 및 방법에 대 한 세부 정보에 대 한 테이블 tooconnect hello 케이블 합니다.
   
    ![전원에 4U 장치를 케이블로 연결](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    **그림 4**. 케이블 다시 연결
   
   | 레이블 | 설명 |
   |:--- |:--- |
   | 1 |기본 인클로저 |
   | 2 |PCM 0 |
   | 3 |PCM 1 |
   | 4 |컨트롤러 0 |
   | 5 |컨트롤러 1 |
   | 6 |EBOD 컨트롤러 0 |
   | 7 |EBOD 컨트롤러 1 |
   | 8 |EBOD 인클로저 |
   | 9 |전력 분배 장치 |

## <a name="next-steps"></a>다음 단계
[StorSimple 하드웨어 구성 요소 교체](storsimple-hardware-component-replacement.md)에 대해 자세히 알아봅니다.

