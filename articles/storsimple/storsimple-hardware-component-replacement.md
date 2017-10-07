---
title: "하드웨어 구성 요소 교체 aaaStorSimple | Microsoft Docs"
description: "Toosafely hello Pcm, 배터리, 컨트롤러 모듈, EBOD 컨트롤러, 디스크 드라이브 및 StorSimple 장치의 섀시 교체 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e8087ba7-0b66-4f59-8988-e53aad52ee21
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 472d9dc1c31b61550fe079cc9b9419510487db3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-hardware-component-on-your-storsimple-8000-series-device"></a>StorSimple 8000 시리즈 장치에서 하드웨어 구성 요소 교체

## <a name="overview"></a>개요
hello 하드웨어 구성 요소 교체 자습서에 Microsoft Azure StorSimple 8000 시리즈 장치와 hello 단계 필요한 tooremove hello 하드웨어 구성 요소에 설명 하 고 바꾸세요. 이 문서에 hello 안전 아이콘에 설명 하는 팁을 제공 하 고 목록 hello는 교체 될 수 있는 구성 요소는 toohello 자세한 자습서입니다.

> [!IMPORTANT]
> Tooremove 시도 하기 전에 모든 StorSimple 구성 요소 교체, hello 검토 해야 또는 [안전 아이콘 규칙](#safety-icon-conventions) 및 기타 [안전 조치](storsimple-safety.md)합니다.
> 
> 

### <a name="safety-icon-conventions"></a>안전성 아이콘 표시 규칙
hello 다음 표에 이러한 자습서에 사용 된 hello 안전 아이콘이 있습니다. 살펴보아야 toothese 안전 아이콘 hello 단계 tooremove를 통해 이동 하 고 장치 구성 요소를 바꿉니다.

| 아이콘 | 텍스트 | 추가 정보 |
|:--- |:--- |:--- |
| ![경고 아이콘](./media/storsimple-hardware-component-replacement/Warning.png) |**위험!** |피하지 않을 경우 사망 또는 심각한 부상을 당하는 위험한 상황을 나타냅니다. 이 신호 단어는 제한 된 toohello 가장 극단적인 상황입니다. |
| ![경고 아이콘](./media/storsimple-hardware-component-replacement/Warning.png) |**경고!** |피하지 않을 경우 사망 또는 심각한 부상을 당할 수 있는 위험한 상황을 나타냅니다. |
| ![주의 아이콘](./media/storsimple-hardware-component-replacement/Caution.png) |**주의!** |피하지 않을 경우 최소 또는 보통 수준의 부상을 당할 수 있는 위험한 상황을 나타냅니다. |
| ![고지 아이콘](./media/storsimple-hardware-component-replacement/NoticeIcon.png) |**고지:** |중요하지만 위험과 관련되지 않은 것으로 간주되는 정보를 나타냅니다. |
| ![감전 아이콘](./media/storsimple-hardware-component-replacement/Electric.png) |**감전 위험** |높은 전압을 나타냅니다. |
| ![무거운 무게 아이콘](./media/storsimple-hardware-component-replacement/Weight.png) |**무거운 무게** | |
| ![사용자 서비스 가능 부품 없음 아이콘](./media/storsimple-hardware-component-replacement/NoUserServiceableParts.png) |**사용자 서비스 가능 부품 없음** |제대로 교육을 받지 않은 경우 액세스하지 마세요. |
| ![지침 읽기 아이콘](./media/storsimple-hardware-component-replacement/ReadInstructions.png) |**먼저 모든 지침 읽기** | |
| ![기울어짐 위험 아이콘](./media/storsimple-hardware-component-replacement/TipHazard.png) |**기울어짐 위험** | |

### <a name="before-you-begin"></a>시작하기 전에
이 자습서에 사용 하 여 장치 및 안전 아이콘에 대 한 hello 안전 정보를 숙지 합니다. 너무 이동[안전 하 게 설치 하 고 StorSimple 장치를 작동](storsimple-safety.md) 완전 한 정보에 대 한 합니다. 수 있는지 tooreview hello [안전 조치](storsimple-safety.md#handling-precautions) StorSimple 장치를 처리 하기 전에. 

Tooreplace 구성 요소를 시도 하기 전에 hello 다음 정보를 고려 합니다.

![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png) ![Electrical Shock Icon](./media/storsimple-hardware-component-replacement/Electric.png) **경고!** 

* StorSimple 장치의 모듈 및 구성 요소를 처리할 때 정전기 방전 또는 정전기 방지 매트를 사용하여 올바르게 접지합니다.
* 회로를 만지지 마세요. 회로가 노출 되었을 수 있는 구성 요소를 처리 하는 동안 제공 된 hello 핸들 및 가이드를 사용 합니다.

![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png) ![Notice Icon](./media/storsimple-hardware-component-replacement/NoticeIcon.png) **고지:**

모듈을 교체할 때 **hello hello 인클로저 후면에 빈 베이 두어서는 안**합니다. Hello 문제가 있는 부품을 제거 하기 전에 교체 모듈 또는 빈 모듈을 가져옵니다.

## <a name="hardware-component-replacement-procedures"></a>하드웨어 구성 요소 교체 절차
여러 기본 hello에 플러그 인 모듈 및/또는 EBOD 인클로저 StorSimple 8000 시리즈 장치 구성 됩니다. 8100 hello는 hello 8600는 기본 인클로저와 EBOD 인클로저가 있는 이중 인클로저 장치 하는 반면는 단일 기본 인클로저가 있습니다.

장치 hello 기본 하드웨어 구성 요소는 다음 표는 hello에 요약 되어 있습니다. Hello hello 링크를 클릭 **교체 절차** 열 toogo toohello 자습서에 연결 합니다.

| 구성 요소 | 현재 개수 | 플러그 인 모듈 여부 | 교체 절차 |
|:--- |:--- |:--- |:--- |
| 섀시 |1 |아니요 |[StorSimple 장치에 hello 섀시 교체](storsimple-chassis-replacement.md) |
| 기본 컨트롤러 |2 |예 |[StorSimple 장치의 컨트롤러 모듈 교체](storsimple-controller-replacement.md) |
| 764W PCM(전원 및 냉각 모듈) |2 |예 |[StorSimple 장치의 전원 및 냉각 모듈 교체](storsimple-power-cooling-module-replacement.md) |
| 백업 배터리 |2 |예 |[StorSimple 장치에서 hello 백업 배터리 모듈 교체](storsimple-battery-replacement.md) |
| 디스크 드라이브 |12 |예 |[StorSimple 장치의 디스크 드라이브 교체](storsimple-disk-drive-replacement.md) |

**표 1** hello 기본 인클로저의 하드웨어 구성 요소

I/O 모듈 hello 기본 인클로저와 EBOD 인클로저 hello 다릅니다. 또한 hello Pcm 와트를 다릅니다. hello 기본 인클로저에서 hello Pcm은 764w, 백업 배터리 모듈에 인클로저 hello Pcm 기본 hello에 W. 580 hello EBOD 인클로저가 있는 반면도 포함 합니다.

| 구성 요소 | 현재 개수 | 플러그 인 모듈 여부 | 교체 절차 |
|:--- |:--- |:--- |:--- |
| 섀시 |1 |아니요 |[StorSimple 장치에 hello 섀시 교체](storsimple-chassis-replacement.md) |
| EBOD 컨트롤러 |2 |예 |[StorSimple 장치의 EBOD 컨트롤러 교체](storsimple-ebod-controller-replacement.md) |
| 580W PCM(전원 및 냉각 모듈) |2 |예 |[StorSimple 장치의 전원 및 냉각 모듈 교체](storsimple-power-cooling-module-replacement.md) |
| 디스크 드라이브 |12 |예 |[StorSimple 장치의 디스크 드라이브 교체](storsimple-disk-drive-replacement.md) |

**표 2** hello EBOD 인클로저의 하드웨어 구성 요소

hello 장치에서 플러그 인 모듈이 hello hello 다음 전면 및 후면 다이어그램에에서 강조 표시 됩니다. 대체 해야 하는 경우 다양 한 플러그 인 모듈의 hello 이러한 다이어그램 toodetermine hello 위치를 사용할 수 있습니다. hello 전면 다이어그램 보여줄 hello 디스크 드라이브 및 hello 후면 다이어그램의 hello EBOD 인클로저와 기본 인클로저 hello hello 플러그 인 모듈.

![디스크 드라이브가 있는 장치의 프런트플레인](./media/storsimple-hardware-component-replacement/IC741028.png)

**그림 1** hello 장치의 전면

| 레이블 | 설명 |
|:--- |:--- |
| 0 - 11 |디스크 드라이브(총 12개) |

Hello 기본 인클로저 및 EBOD 인클로저 hello 둘 다 다 드라이브 캐리어 모듈이 있습니다. hello 섀시 보관 12 개의 3.5 인치 디스크 드라이브에는 3 4 형식으로 정렬 합니다.

![장치 기본 엔클로저 모듈의 백플레인](./media/storsimple-hardware-component-replacement/IC740994.png)

**그림 2** hello 기본 엔클로저의 뒷면

| 레이블 | 설명 |
|:--- |:--- |
| 1 |PCM 0 |
| 2 |PCM 1 |
| 3 |컨트롤러 0 |
| 4 |컨트롤러 1 |

![장치 EBOD 엔클로저 플러그 인 모듈의 백플레인](./media/storsimple-hardware-component-replacement/IC769599.png)

**그림 3** hello EBOD 인클로저의 후면

| 레이블 | 설명 |
|:--- |:--- |
| 1 |PCM 0 |
| 2 |PCM 1 |
| 3 |EBOD 컨트롤러 0 |
| 4 |EBOD 컨트롤러 1 |

## <a name="field-replaceable-units"></a>FRU(필드 교체 장치)
다음 fru 교체 () hello StorSimple 장치에 사용할 수 있습니다.

* 섀시 (hello 통합된 운용 패널 포함)
* 764 W AC PCM
* 580 W AC PCM
* 드라이브 캐리어 모듈이 있는 하드 디스크 드라이브
* 컨트롤러 모듈
* EBOD 컨트롤러 모듈
* 백업 배터리 모듈
* 랙 탑재 레일 키트

하십시오 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md) tooorder 이러한 교체 장비입니다.

## <a name="next-steps"></a>다음 단계
모든 검토 [안전 정보](storsimple-safety.md) tooreplace StorSimple 하드웨어 구성 요소를 시도 하기 전에.

