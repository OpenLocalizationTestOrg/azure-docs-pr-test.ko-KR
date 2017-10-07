---
title: "기술 사양 aaaStorSimple | Microsoft Docs"
description: "Hello 기술 사양 및 규제 표준 준수 정보 hello StorSimple 하드웨어 구성 요소를 설명합니다."
services: storsimple
documentationcenter: NA
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
ms.openlocfilehash: 98fa3307e2a929551c74e8b3179bb0fb61c0ab53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="technical-specifications-and-compliance-for-hello-storsimple-device"></a>기술 사양 및 규정 준수 hello StorSimple 장치에 대 한

## <a name="overview"></a>개요

Microsoft Azure StorSimple 장치의 하드웨어 구성 요소 hello toohello 기술 사양 및 규제 표준이이 문서에 설명 된 준수 합니다. hello 전원 및 냉각 모듈 (Pcm) 디스크 드라이브, 저장소 용량 및 엔클로저 hello 기술 사양에 설명합니다. hello 준수 정보 국제 표준, 안전성, 방출 및 케이블 연결 등의 작업에 설명 합니다.

## <a name="power-and-cooling-module-specifications"></a>전원 및 냉각 모듈 사양

hello StorSimple 장치에는 두 개의 100-240 V 이중 팬, SBB 규격 Pcm 전원 냉각 모듈 ()에 있습니다. 중복 전원 구성을 제공합니다. PCM에 오류가 발생할 경우 hello 장치에서 계속 해 서 toooperate 정상적으로 hello hello 모듈 실패 될 때까지 다른 PCM 대체 됩니다.

hello EBOD 인클로저는 580w PCM을 사용 하 고 기본 인클로저는 764w PCM을 사용 하 여 키를 누릅니다. hello 다음 테이블 목록 hello 기술 사양 hello Pcm에 연결 합니다.

| 사양 | 580 W PCM(EBOD) | 764 W PCM(기본) |
| --- | --- | --- |
| 최대 출력 전원 |580W |764 |
| Frequency(빈도) |50/60Hz |50/60Hz |
| 전압 범위 선택 |자동 범위 지정: 90-264V AC, 47/63Hz |자동 범위 지정: 90- 264 V AC, 47/63Hz |
| 최대 유입 전류 |20A |20A |
| 전원 요소 수정 |> 95% 정격 입력 전압 |> 95% 정격 입력 전압 |
| 고주파 |EN61000-3-2를 충족합니다. |EN61000-3-2를 충족합니다. |
| 출력 |5V 대기 전압 @ 2.0A |5V 대기 전압 @ 2.7A |
| +5V @ 42A |+5V @ 40A | |
| +12V @ 38A |+12V @ 38A | |
| 핫 플러그형 |예 |예 |
| 스위치 및 LED |AC ON/OFF 스위치와 4개의 상태 표시기 LED |AC ON/OFF 스위치와 6개의 상태 표시기 LED |
| 냉각 엔클로저 |가변 팬 속도 제어를 사용한 냉각팬 축 |가변 팬 속도 제어를 사용한 냉각팬 축 |

## <a name="power-consumption-statistics"></a>전원 소비 통계

다음 표에서 hello hello 일반적인 전원 소비 데이터 (실제 값은 게시 hello에서 달라질 수 있음) hello에 대 한 다양 한 모델이 나열 StorSimple 장치의 됩니다.

| 조건 | 240V AC | 240V AC | 240V AC | 110V AC | 110V AC | 110V AC |
| --- | --- | --- | --- | --- | --- | --- |
|  속도가 느린 팬 , 유휴 상태의 드라이브 |1.45 A |0.31 kW |1057.76 BTU/hr |3.19 A |0.34 kW |1160.13 BTU/hr |
|  속도가 느린 팬 , 드라이브 액세스 |1.54 A |0.33 kW |1126.01 BTU/hr |3.27 A |0.36 kW |1228.37 BTU/hr |
|  속도가 빠른 팬, 유휴 상태의 드라이브, 전원이 켜진 두 PSU |2.14 A |0.49 kW |1671.95 BTU/hr |4.99 A |0.54 kW |1842.56 BTU/hr |
|  속도가 빠른 팬, 유휴 상태의 드라이브, PSU 하나는 전원이 켜지고 하나는 유휴 상태 |2.05 A |0.48 kW |1637.83 BTU/hr |4.58 A |0.50 kW |1706.07 BTU/hr |
|  속도가 빠른 팬, 드라이브 액세스, 전원이 켜진 두 PSU |2.26 A |0.51 kW |1740.19 BTU/hr |4.95 A |0.54 kW |1842.56 BTU/hr |
|  속도가 빠른 팬, 드라이브 액세스, PSU 하나는 전원이 켜지고 하나는 유휴 상태 |2.14 A |0.49 kW |1671.95 BTU/hr |4.81 A |0.53 kW |1808.44 BTU/hr |

## <a name="disk-drive-specifications"></a>디스크 드라이브 사양

StorSimple 장치 too12 3.5 인치 폼 팩터 연결 된 SAS (Serial SCSI) 디스크 드라이브를 지원합니다. hello 실제 드라이브는 Ssd (반도체 드라이브) 또는 hello 제품 구성에 따라 하드 디스크 드라이브 (Hdd) 혼합 될 수 있습니다. hello 12 개의 디스크 드라이브 슬롯 hello 인클로저 앞에 3으로 4로 구성에 있습니다. hello EBOD 인클로저의 다른 12 개의 디스크 드라이브에 대 한 추가 저장소를 허용합니다. 항상 HDD입니다.

## <a name="storage-specifications"></a>저장소 사양

hello StorSimple 장치에는 하드 디스크 드라이브 및 반도체 드라이브 8100 및 8600 두 hello에 대 한 혼합이 되어 있습니다. 8100 및 8600 hello에 대 한 총 사용 가능한 용량과 hello은 약 15 TB 및 38 TB 각각입니다. 다음 표에서 hello SSD 및 HDD, hello StorSimple 솔루션 용량의 hello 컨텍스트에서 클라우드 용량 hello 세부 정보를 설명 합니다.

| 장치 모델 / 용량 | 8100 | 8600 |
| --- | --- | --- |
| HDD(하드 디스크 드라이브)의 수 |8 |19 |
| SSD(반도체 드라이브)의 수 |4 |5 |
| 단일 HDD 용량 |4TB |4TB |
| 단일 SSD 용량 |400GB |800GB |
| 예비 용량 |4TB |4TB |
| 사용 가능한 HDD 용량 |14TB |36TB |
| 사용 가능한 SSD 용량 |800GB |2TB |
| 총 사용 가능한 용량 * |최대 15TB |최대 38TB |
| 최대 솔루션 용량(클라우드 포함) |200TB |500TB |

<sup>* </sup>- *hello 총 사용 가능한 용량과 hello 데이터, 메타 데이터 및 버퍼에 대 한 사용 가능한 용량을 포함합니다.*

## <a name="enclosure-dimensions-and-weight-specifications"></a>엔클로저 차원과 가중치 사양

다음 테이블 목록 hello hello 다양 한 인클로저 사양의 치수 및 무게에 대 한 합니다.

### <a name="enclosure-dimensions"></a>엔클로저 크기

hello 다음 표 밀리미터 및 인치 단위로 hello 인클로저의 hello 크기입니다.

| 인클로저 | 밀리미터 | 인치 |
| --- | --- | --- |
| 높이 |87.9 |3.46 |
| 장착 플랜지 너비 |483 |19.02 |
| 엔클로저 본체 너비 |443 |17.44 |
| 인클로저 본문의 전면 탑재 플랜지 tooextremity에서 깊이 |577 |22.72 |
| 수준 작업에서 인클로저 맨 끝 까지의 toofurthest 패널 |630.5 |24.82 |
| 탑재 플랜지 toofurthest 본체 인클로저 맨 끝에서 깊이 |603 |23.74 |

### <a name="enclosure-weight"></a>엔클로저 무게

Hello 구성에 따라 완전히 로드 될된 기본 인클로저 무게는 21 too33 kgs에서 이루어지며 두 개의 persons toohandle 것입니다.

| 인클로저 | 무게 |
| --- | --- |
| 최대 무게 (hello 구성에 따라 다름) |30kg – 33kg |
| 비어 있음(맞는 드라이브가 없음) |21-23kg |

## <a name="enclosure-environment-specifications"></a>엔클로저 환경 사양

이 섹션에서는 hello 사양 관련된 toohello 인클로저 환경을 나열 합니다. hello 온도, 습도, 고도, 충격, 진동, 방향, 안전 및 전자기 EMC ()는이 범주에 포함 됩니다.

### <a name="temperature-and-humidity"></a>온도 및 습도

| 인클로저 | 주변 온도 범위 | 주변 상대 습도 | 최대 습구 |
| --- | --- | --- | --- |
| 작동 |5°C - 35°C(41°F - 95°F) |20%-80% 비압축 |28°C (82°F) |
| 작동 불가능 |-40°C - 70°C(40°F - 158°F) |5% - 100% 비압축 |29°C(84°F) |

### <a name="airflow-altitude-shock-vibration-orientation-safety-and-emc"></a>기류, 고도, 충격, 진동, 방향, 안전성 및 EMC

| 인클로저 | 운영 사양 |
| --- | --- |
| 기류 |시스템 기류는 전면 toorear 합니다. 압력이 낮고, 후면 배기가 설치된 시스템을 작동할 수 있어야 합니다. 랙 문 및 장애물때문에 생성된 역 압력은 5 파스칼(0.5mm 수면계)을 초과해서는 안됩니다. |
| 작동 가능 고도 |-30 미터 작동 온도 최대 too3045 미터 (-100 피트 too10, 000 피트) 7000 피트 이상의 5 ° c 취소 등급이 지정 합니다. |
| 작동 불가능 고도 |-305 미터 ~ too12, 192 미터 (-1 too40, 000 피트) |
| 충격, 작동 |5g 10 ms ½ sine |
| 충격, 작동 불가능 |30g 10 ms ½ sine |
| 진동, 작동 |0.21g RMS 5-500Hz 임의 |
| 진동, 작동 불가능 |1.04g RMS 2-200Hz 임의 |
| 진동, 재배치 |3g 2-200Hz sine |
| 방향 및 탑재 |19"랙 탑재(2 EIA 단위) |
| 랙 레일 |toofit 최소 700mm (31.50 인치) 깊이 랙이 IEC 297을 준수 |
| 안전성 및 승인 |CE 및 UL EN 61000-3, IEC 61000-3, UL 61000 3 |
| EMC |EN55022(CISPR - A), FCC A |

## <a name="international-standards-compliance"></a>국제 표준 준수

Microsoft Azure StorSimple 장치 hello 다음 국제 표준을 준수 합니다.  

* CE - EN 60950 - 1
* CB 보고서 tooIEC 60950-1
* UL 및 cUL tooUL 60950-1

## <a name="safety-compliance"></a>안전 규정 준수

Microsoft Azure StorSimple 장치 hello 다음 안전 등급을 충족 합니다.

* 시스템 제품 유형 승인: UL, cUL, CE
* 보안 준수: UL 60950, IEC 60950, EN 60950

## <a name="emc-compliance"></a>EMC 규정 준수

Microsoft Azure StorSimple 장치 hello 다음 EMC 등급을 충족 합니다.

### <a name="emissions"></a>배출

hello 장치는 전도성 및 복사 성 방출 수준에 대 한 EMC 규정을 준수 합니다.

* 전도성 배출 제한 수준: CFR 47 Part 15B Class A EN55022 Class A CISPR Class A
* 복사성 배출 제한 수준: CFR 47 Part 15B Class A EN55022 Class A CISPR Class A

### <a name="harmonics-and-flicker"></a>고주파 및 깜박임

hello 장치 EN61000-3-2/3을 준수합니다.

### <a name="immunity-limit-levels"></a>면역 제한 수준

e n 55024를 준수 하는 hello 장치입니다.

## <a name="ac-power-cord-compliance"></a>AC 전원 코드 규정 준수

hello 플러그와 전체 전원 코드 조립품 hello 국가 hello 장치가 사용 되 고, 적합 hello 표준을 충족 해야 하 고 해당 국가에서 허용 되는 안전 승인을 해야 하는 hello 합니다. hello 다음 테이블 목록 표준 hello 미국과 유럽에 합니다.

### <a name="ac-power-cords---usa-must-be-nrtl-listed"></a>AC 전원 코드-미국(나열된 NRTL이어야 함)

| 구성 요소 | 사양 |
| --- | --- |
| 코드 형식 |SV 또는 SVT, 최소 18 AWG, 3선, 최대 2.0m 길이 |
| 플러그 |NEMA 5-15P 첨부 파일 형식 접지 플러그  등급 120V, 10A 또는 IEC 320 C14, 250V, 10A |
| 소켓 |IEC 320 C-13, 250V, 10A |

### <a name="ac-power-cords---europe"></a>AC 전원 코드-유럽

| 구성 요소 | 사양 |
| --- | --- |
| 코드 형식 |고주파, H05-VVF-3G1.0 |
| 소켓 |IEC 320 C-13, 250V, 10A |

## <a name="supported-network-cables"></a>지원되는 네트워크 케이블

Hello 10 GbE 네트워크 인터페이스, DATA 2 및 DATA 3 참조 toohello [지원 되는 네트워크 케이블 및 모듈 목록은](storsimple-supported-hardware-for-10-gbe-network-interfaces.md)합니다.

## <a name="next-steps"></a>다음 단계

데이터 센터에 StorSimple 장치 준비 toodeploy 됩니다. 자세한 내용은 [온-프레미스 장치 배포](storsimple-8000-deployment-walkthrough-u2.md)를 참조하세요.

