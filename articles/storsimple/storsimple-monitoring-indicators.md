---
title: "모니터링 표시기 aaaStorSimple | Microsoft Docs"
description: "Hello 다이오드 Led 및 청각적 경보 사용 되는 toomonitor hello 상태 hello StorSimple 장치에 설명합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 59dee7b9-ca6d-4fd9-96e6-a0071e8d248e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: e690b8f4727272f5fbb8886a594a046f794a1380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-monitoring-indicators-toomanage-your-device"></a>StorSimple 모니터링 표시기 toomanage에서 장치 사용
## <a name="overview"></a>개요
모듈 및 hello StorSimple 장치의 전반적인 상태 toomonitor를 사용할 수 있는 경보 hello 및 StorSimple 장치에 다이오드 Led 포함 됩니다. 표시기를 모니터링 하는 hello hello 장치의 기본 인클로저 및 EBOD 인클로저 hello hello 하드웨어 구성 요소에서 확인할 수 있습니다. hello 모니터링 표시기는 Led 또는 청각적 경보 일 수 있습니다.

모듈의 세 가지 LED 상태 사용 tooindicate hello 상태는: 녹색, 깜박이 녹색 toored-주황색으로 변함 또는 빨간색-주황색입니다.  

* 녹색 LED는 정상 작동 상태를 나타냅니다.  
* 깜박이 녹색 toored-주황색 Led 사용자 개입이 필요할 수 있는 중요 하지 않은 조건의 hello 존재 여부를 나타냅니다.  
* 빨간색-주황색 Led hello 모듈 내에 있는 중요 한 결함이 있음을 나타냅니다.  

이 문서의 나머지 부분에서는 hello 설명 hello 다양 한 모니터링 표시기 Led, hello StorSimple 장치에서의 위치, hello에 따라 hello 장치 상태 LED 상태 및 연결 된 청각적 경보가 있습니다.

## <a name="front-panel-indicator-leds"></a>전면 패널 표시기 LED
hello 라고도 하는 hello 전면 패널, *작동 패널* 또는 *ops 패널*, 모든 hello 모듈의 집계 상태가 hello hello 시스템에 표시 됩니다. hello 전면 패널 hello StorSimple 기본 및 EBOD 인클로저 hello에 동일 하며 아래 그림에 나와 있습니다.  

   ![장치 전면 패널][1]

hello 전면 패널 표시기 뒤 hello를 포함 되어 있습니다.  

1. 음소거 단추
2. 전원 표시기 LED(녹색/빨간색-주황색)
3. 모듈 결함 표시기 LED(켜기 빨간색-주황색/끄기)
4. 논리 결함 표시기 LED(켜기 빨간색-주황색/끄기)
5. 장치 ID 디스플레이  

hello hello 장치에 대 한 hello 전면 패널 Led와 EBOD 인클로저 hello에 대 한 가장 큰 차이점은 hello **시스템 장치 식별 번호** hello LED 디스플레이에 표시 합니다. hello 장치 표시 ID는 hello 기본 단위 **00**hello 기본 장치 ID EBOD 인클로저 hello에 표시 되는 반면, **01**합니다. 이렇게 하면 hello 장치를 켤 때 tooquickly hello 장치와 hello EBOD 인클로저 사이 구분 합니다. 장치가 꺼져 있으면에 제공 된 hello 정보를 사용 하 여 [새 장치 켜기](storsimple-turn-device-on-or-off.md#turn-on-a-new-device) hello EBOD 인클로저에서에서 toodifferentiate hello 장치입니다.  

## <a name="front-panel-led-status"></a>전면 패널 LED 상태
Hello hello 장치 또는 hello EBOD 인클로저 전면 패널에 hello Led가 나타내는 테이블 tooidentify hello 상태 다음 hello를 사용 합니다.  

| 시스템 전원 | 모듈 결함 | 논리적 결함 | 경보 | 가동 상태 |
| --- | --- | --- | --- | --- |
| 빨간색-주황색 |끄기 |끄기 |해당 없음 |AC 전원 손실, 백업 전원 또는 AC 전원으로 작동 하 고 hello 컨트롤러 모듈이 제거 되었음. |
| 녹색 |켜기 |켜기 |해당 없음 |ops 패널 전원 켜기(5초) 상태 테스트 |
| 녹색 |끄기 |끄기 |해당 없음 |전원이 켜짐, 모든 기능이 정상 상태임 |
| 녹색 |켜기 |해당 없음 |PCM 결함 LED, 팬 결함 LED |모든 PCM 결함, 팬 결함, 온도 초과 또는 미만 |
| 녹색 |켜기 |해당 없음 |I/O 모듈 LED |모든 컨트롤러 모듈 결함 |
| 녹색 |켜기 |해당 없음 |해당 없음 |인클로저 논리적 결함 |
| 녹색 |깜박임 |해당 없음 |컨트롤러 모듈의 모듈 상태 LED. PCM 결함 LED, 팬 결함 LED |알 수 없는 컨트롤러 모듈 유형이 설치됨, I2C 버스 오류, 컨트롤러 모듈 VPD(Vital Product Data) 구성 오류 |

## <a name="power-cooling-module-pcm-indicator-leds"></a>PCM(전원 냉각 모듈) 표시기 LED
전원 냉각 모듈 (PCM) 표시기 Led hello hello 기본 인클로저 또는 EBOD 인클로저의 각 PCM 모듈의 뒷면에 있습니다. 이 항목에서는 방법을 StorSimple 장치의 toomonitor hello 상태 led가 다음 toouse hello 합니다.  

* Hello 기본 인클로저의 PCM Led
* Hello EBOD 인클로저의 PCM Led

## <a name="pcm-leds-for-hello-primary-enclosure"></a>Hello 기본 인클로저의 PCM Led
hello StorSimple 장치에는 764W PCM 모듈과 추가 배터리가 있습니다. hello 다음은 hello 장치에 대 한 hello LED 패널입니다.  

   ![Hello 기본 인클로저의 PCM Led][2]

LED 범례

1. AC 전원 오류
2. 팬 오류
3. 배터리 결함
4. PCM 정상
5. DC 오류
6. 배터리 정상  

패널을 LED를 hello 상태의 hello PCM hello에 표시 됩니다. hello 장치 PCM LED 패널에 6 개의 led가 있습니다. 이러한 Led 중 4 개 hello 전원 공급 장치 및 hello 팬의 hello 상태를 표시 합니다. 두 개의 Led 남은 hello hello PCM에서에서 백업 배터리 모듈 hello의 hello 상태를 나타냅니다. 다음 테이블 toodetermine hello 상태 hello PCM의 hello를 사용할 수 있습니다.  

### <a name="pcm-indicator-leds-for-power-supply-and-fan"></a>전원 공급 장치 및 팬의 PCM 표시기 LED
| 가동 상태 | PCM 정상(녹색) | AC 오류(주황색) | 팬 오류(주황색) | DC 오류(주황색) |
| --- | --- | --- | --- | --- |
| AC 전원 없음 (tooenclosure) |끄기 |끄기 |끄기 |끄기 |
| AC 전원 없음(이 PCM만 해당) |끄기 |켜기 |끄기 |켜기 |
| AC 있음 PCM 켜짐-정상 |켜기 |끄기 |끄기 |끄기 |
| PCM 오류(팬 오류) |끄기 |끄기 |켜기 |해당 없음 |
| PCM 결함(과도 진폭, 과전압, 과전류) |끄기 |켜기 |켜기 |켜기 |
| PCM(팬이 허용 오차를 벗어남) |켜기 |끄기 |끄기 |켜기 |
| 대기 모드 |깜박임 |끄기 |끄기 |끄기 |
| PCM 펌웨어 다운로드 |끄기 |깜박임 |깜박임 |깜박임 |

### <a name="pcm-indicator-leds-for-hello-backup-battery"></a>Hello 백업 배터리의 PCM 표시기 Led
| 가동 상태 | 배터리 정상(녹색) | 배터리 결함(주황색) |
| --- | --- | --- |
| 배터리 없음 |끄기 |끄기 |
| 배터리가 있고 충전됨 |켜기 |끄기 |
| 배터리 충전 중 또는 유지 관리를 위한 방전 |깜박임 |끄기 |
| 배터리 "소프트" 결함(복구 가능) |끄기 |깜박임 |
| 배터리 "하드" 결함(복구 불가능) |끄기 |켜기 |
| 배터리 해제됨 |깜박임 |끄기 |

## <a name="pcm-leds-for-hello-ebod-enclosure"></a>Hello EBOD 인클로저의 PCM Led
hello EBOD 인클로저는 580W PCM 있고 추가 배터리는 없습니다. EBOD 인클로저 hello에 대 한 hello PCM 패널 표시기 Led만 hello 전원 공급 장치 및 팬 hello에 있습니다. hello 다음 그림에서는 이러한 Led

   ![Hello EBOD 인클로저의 PCM Led][3] 

Hello PCM의 테이블 toodetermine hello 상태 다음 hello를 사용할 수 있습니다.  

| 가동 상태 | PCM 정상(녹색) | AC 오류(주황색) | 팬 오류(주황색) | DC 오류(주황색) |
| --- | --- | --- | --- | --- |
| AC 전원 없음 (tooenclosure) |끄기 |끄기 |끄기 |끄기 |
| AC 전원 없음(이 PCM만 해당) |끄기 |켜기 |끄기 |켜기 |
| AC 있음 PCM 켜짐 - 정상 |켜기 |끄기 |끄기 |끄기 |
| PCM 오류(팬 오류) |끄기 |끄기 |켜기 |X |
| PCM 결함(과도 진폭, 과전압, 과전류) |끄기 |켜기 |켜기 |켜기 |
| PCM(팬이 허용 오차를 벗어남) |켜기 |끄기 |끄기 |켜기 |
| 대기 모드 |깜박임 |끄기 |끄기 |끄기 |
| PCM 펌웨어 다운로드 |끄기 |깜박임 |깜박임 |깜박임 |

## <a name="controller-module-indicator-leds"></a>컨트롤러 모듈 표시기 LED
hello StorSimple 장치에 hello 기본 컨트롤러 및 EBOD 컨트롤러 모듈 hello led가 포함 되어 있습니다.   

### <a name="monitoring-leds-for-hello-primary-controller"></a>Hello 기본 컨트롤러의 모니터링 Led
hello 다음 그림을 사용 하면 hello 기본 컨트롤러에서 hello Led를 식별 합니다. (Hello 구성 요소 모두 나열된 tooaid 방향에서입니다.)  

   ![LED -기본 컨트롤러 모니터링][4]

Hello 컨트롤러 모듈이 제대로 작동 하는지 여부를 테이블 toodetermine 다음 hello를 사용 합니다.  

### <a name="controller-indicator-leds"></a>컨트롤러 표시기 LED
| LED | 설명 |
| --- | --- |
| ID LED(파란색) |식별 되 고 해당 hello 모듈을 나타냅니다. Hello 파란색 LED가 깜박이고 있으면 실행 중인 컨트롤러에, 다음 hello 컨트롤러 hello 활성 컨트롤러 이며 hello 다른 노드로 hello 대기 컨트롤러입니다. 자세한 내용은 참조 [식별 hello 장치에서 활성 컨트롤러](storsimple-8000-controller-replacement.md#identify-the-active-controller-on-your-device)합니다. |
| 오류 LED(주황색) |Hello 컨트롤러의 결함을 나타냅니다. |
| 정상 LED(녹색) |안정적인 녹색 해당 hello 컨트롤러가 정상 상태임을 나타냅니다. 깜박이는 녹색은 컨트롤러 VPD 구성 오류를 나타냅니다. |
| SAS 활동 LED(녹색) |녹색은 현재 활동이 없는 연결을 나타냅니다. 깜박이 며 녹색 hello 연결에 진행 중인 활동을 나타냅니다. |
| 이더넷 상태 LED |링크/네트워크 활동을 나타내는 오른쪽: 링크 활동(녹색), 네트워크 활동(깜박이는 녹색) 네트워크 속도를 나타내는 왼쪽: 1000Mb/s(노란색), 100Mb/s(녹색) 및 10Mb/s(꺼짐) Hello 구성 요소 모델에 따라 hello 네트워크 인터페이스 사용 하지 않는 경우에이 표시등이 깜박일 수 있습니다. |
| POST LED |Hello 컨트롤러를 켤 때 hello 부팅 진행률을 나타냅니다. Hello StorSimple 장치 tooboot 못하면이 LED hello hello 부팅 프로세스 중에서 hello 오류가 발생 한 지점을 식별 하는 Microsoft 지원 데 도움이 됩니다. |

> [!IMPORTANT]
> Hello 결함 LED가 켜지 면 hello 컨트롤러 다시 시작 하 여 해결할 수 있는 hello 컨트롤러 모듈에 문제가 있습니다. Hello 컨트롤러 다시 시작이 문제가 해결 되지 않으면 Microsoft 지원에 문의 하십시오.  
> 
> 

### <a name="monitoring-leds-for-hello-ebod-ebod-enclosure"></a>Led (EBOD 인클로저) EBOD hello에 대 한 모니터링
각각의 hello 6gb/s SAS EBOD 컨트롤러에 hello 다음 그림에에서 나와 있는 것 처럼 해당 상태를 나타내는 led가 있습니다.  

  ![LED - EBOD 엔클로저 모니터링][5]

Hello EBOD 컨트롤러 모듈이 정상적으로 작동 하는지 여부를 테이블 toodetermine 다음 hello를 사용 합니다.  

### <a name="ebod-controller-module-indicator-leds"></a>EBOD 컨트롤러 모듈 표시기 LED
| 가동 상태 | I/O 모듈 정상(녹색) | I/O 모듈 결함(주황색) | 호스트 포트 활동(녹색) |
| --- | --- | --- | --- |
| 컨트롤러 모듈 정상 |켜기 |끄기 |- |
| 컨트롤러 모듈 결함 |끄기 |켜기 |- |
| 외부 호스트 포트 연결 없음 |- |- |끄기 |
| 외부 호스트 포트 연결 - 작업 없음 |- |- |켜기 |
| 외부 호스트 포트 연결 - 작업 |- |- |깜박임 |
| 컨트롤러 모듈 메타데이터 오류 |깜박임 |- |- |

## <a name="disk-drive-indicator-leds-for-hello-primary-enclosure-and-ebod-enclosure"></a>Hello 기본 인클로저 및 EBOD 인클로저의 디스크 드라이브 표시기 Led
hello StorSimple 장치 hello 기본 인클로저 및 EBOD 인클로저 hello 모두에 있는 디스크 드라이브에 있습니다. 이 섹션에서 설명한 대로 각 디스크 드라이브에는 모니터링 표시기 LED가 포함됩니다. 

Hello 디스크 드라이브에 대 한 hello 드라이브 상태를 나타냅니다 녹색 LED와 주황색 LED hello 각 드라이브 캐리어 모듈 앞면에 탑재 합니다. hello 다음 그림에서는 이러한 Led

  ![디스크 드라이브 LED][6]

다음 테이블 toodetermine hello 상태 차례로 hello 전체 전면 패널 LED 상태에 영향을 주는 각 디스크 드라이브의 hello를 사용 합니다.  

### <a name="disk-drive-indicator-leds-for-hello-ebod-enclosure"></a>EBOD 인클로저 hello에 대 한 디스크 드라이브 표시기 Led
| 가동 상태 | 활동 정상 LED(녹색) | 오류 LED(빨간색-주황색) | 연결된 ops 패널 LED |
| --- | --- | --- | --- |
| 설치된 드라이브 없음 |끄기 |끄기 |없음 |
| 드라이브 설치됨 및 작동 |활동 시 깜박임 켜기/끄기 |X |없음 |
| SES(SCSI 인클로저 서비스) 장치 ID 집합 |켜기 |깜박임 1초 켜기/1초 끄기 |없음 |
| SES 장치 결함 비트 집합 |켜기 |켜기 |논리적 결함(빨간색) |
| 전원 제어 회로 오류 |끄기 |켜기 |모듈 결함(빨간색) |

## <a name="audible-alarms"></a>청각적 경보
StorSimple 장치 hello 기본 인클로저 및 EBOD 인클로저 hello와 관련 된 청각적 경보가 있습니다. 청각적 경보는 두 인클로저에서 hello 전면 패널 (hello ops 패널이 라고도)에 있습니다. hello 청각적 경보는 오류 조건이 있는 경우를 나타냅니다. hello 조건 다음 hello 경보를 활성화 합니다.  

* 팬 결함 또는 오류
* 전압 범위 벗어남
* 과열 또는 저온 상태
* 열 오버런
* 시스템 결함
* 논리적 결함
* 전원 공급 결함
* PCM(전원 냉각 모듈) 제거  

hello 다음 표에서 hello 다양 한 경보 상태입니다.  

### <a name="alarm-states"></a>경보 상태
| 경보 상태 | 작업 | 음소거 단추를 누르면 작업 |
| --- | --- | --- |
| S0 |정상 모드: 무음 |경고음 두 번 |
| S1 |결함 모드: 1초 켜기/1초 끄기 |TooS2 또는 S3 전환 (설명 참조) |
| S2 |알림 모드: 간헐적 경고음 |없음 |
| S3 |음소거 모드: 무음 |없음 |
| S4 |심각한 결함 모드: 경보 지속 |사용할 수 없음: 음소거가 활성화 되어있지 않음 |

> [!NOTE]
> * S1 경보 상태일 경우 누르지 않으면 음소거 2 분 내 hello 상태가 자동으로 전환 tooS2 또는 s 3입니다.  
> * 경보 상태 S1 tooS4 hello 오류 조건이 지워진 후 tooS0를 반환 합니다.  
> * 다른 상태에서 심각한 결함 상태 S4를 입력할 수 있습니다.  


Hello ops 패널의 hello 음소거 단추를 눌러 hello 청각적 경보를 음소거 할 수 있습니다. Hello 음소거 스위치가 수동으로 작동 되지 않는 경우 2 분 후 자동으로 음소거 발생 합니다. Hello 경보가 음소거 되는 경우 여전히 문제가 발생 하는 짧은 간헐적인 경고음이 tooindicate와 toosound를 계속 됩니다. hello 경보 모든 hello 문제가 되 면 무음 상태가 됩니다.

hello 다음 표에서 hello 다양 한 경보 조건입니다.

### <a name="alarm-conditions"></a>경보 조건
| 가동 상태 | 심각도 | 경보 | Ops 패널 LED |
| --- | --- | --- | --- |
| PCM 경보 – 단일 PCM에서 DC 전원 손실 |결함 - 중복 손실 없음 |S1 |모듈 결함 |
| PCM 경보 – 단일 PCM에서 DC 전원 손실 |결함 - 중복 손실 |S1 |모듈 결함 |
| PCM 팬 오류 |결함 - 중복 손실 |S1 |모듈 결함 |
| SBB 모듈이 PCM 오류 발견 |오류 |S1 |모듈 결함 |
| PCM 제거됨 |구성 오류 |없음 |모듈 결함 |
| 인클로저 구성 오류 |결함 - 중요 |S1 |모듈 결함 |
| 저온 경보 |Warning |S1 |모듈 결함 |
| 고온 경보 |Warning |S1 |모듈 결함 |
| 과열 경보 |결함 - 중요 |S1 |모듈 결함 |
| I2C 버스 오류 |결함 - 중복 손실 |S1 |모듈 결함 |
| Ops 패널 통신 오류(I2C) |결함 - 중요 |S1 |모듈 결함 |
| 컨트롤러 오류 |결함 - 중요 |S1 |모듈 결함 |
| SBB 인터페이스 모듈 결함 |결함 - 중요 |S1 |모듈 결함 |
| SBB 인터페이스 모듈 결함 - 남은 기능 모듈 없음 |결함 - 중요 |S4 |모듈 결함 |
| SBB 인터페이스 모듈 제거됨 |Warning |없음 |모듈 결함 |
| 드라이브 전원 컨트롤 결함 |경고 - 드라이브 전원 손실 없음 |S1 |모듈 결함 |
| 드라이브 전원 컨트롤 결함 |결함 - 중요, 드라이브 전원 손실 |S1 |모듈 결함 |
| 드라이브 제거됨 |Warning |없음 |모듈 결함 |
| 전원 부족 |Warning |없음 |모듈 결함 |

## <a name="next-steps"></a>다음 단계
[StorSimple 하드웨어 구성 요소 및 상태](storsimple-8000-monitor-hardware-status.md)에 대해 자세히 알아봅니다.

[1]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE01.png
[2]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE02.png
[3]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE03.png
[4]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE04.png
[5]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE05.png
[6]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE06.png


