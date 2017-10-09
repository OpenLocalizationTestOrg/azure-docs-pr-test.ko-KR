---
title: "aaaStorSimple 하드웨어 구성 요소 및 상태 | Microsoft Docs"
description: "Toomonitor hello StorSimple Manager 서비스를 통해 StorSimple 장치의 하드웨어 구성 요소를 hello 하는 방법에 대해 알아봅니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 0d56a2ba-daf0-45ad-9610-8b8712dd5750
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: 12a62c0ffc4a5b5e72a25e9e1d976009be03c598
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomonitor-hardware-components-and-status"></a>Hello StorSimple 관리자 서비스 toomonitor 하드웨어 구성 요소 및 상태를 사용 하 여
## <a name="overview"></a>개요
이 문서에서는 hello 설명 온-프레미스 StorSimple 장치에서 다양 한 물리적 및 논리적 구성 요소입니다. 또한 toomonitor hello를 사용 하 여 장치 구성 요소 상태를 hello 하는 방법을 설명 **유지 관리** hello StorSimple Manager 서비스에에서는 페이지입니다. 

hello **유지 관리** 페이지 모든 hello StorSimple 장치 구성 요소의 hello 하드웨어 상태를 표시 합니다. 

Hello 8100의 구성 요소 목록 아래에서 설명 하는 세 가지 섹션이 있습니다.

* **공유 구성 요소** -이러한의 일부분이 아닌 hello 컨트롤러와 같은 디스크 드라이브, 인클로저, PCM 구성 요소와 PCM 온도, 정격 전압, 선 전류 센서 합니다.
* **컨트롤러 0 구성 요소** – 네트워크 인터페이스 컨트롤러 온도 센서 등 컨트롤러, SAS 확장기 및 커넥터, 컨트롤러 0에 있는 다양 한 hello 하는 hello 구성 합니다.
* **컨트롤러 1 구성 요소** – hello 컨트롤러 1, 컨트롤러 0에 설명 하는 유사한 toothose를 구성 하는 구성 요소입니다.

8600 장치의 toohello의 디스크 EBOD (Extended Bunch) 인클로저에 해당 하는 추가 구성 요소에 있습니다. Hello 구성 요소 목록 아래에 5 개 섹션이 있습니다. 이 중에 hello hello 기본 인클로저의 구성 요소를 포함 하는 동일한 toohello 8100에 대 한 설명 된 것과 3 개 섹션이 있습니다. EBOD 인클로저 hello에 대 한 설명 하는 두 개의 추가 섹션이 있습니다.

* **EBOD 인클로저 공유 구성 요소** – hello EBOD 인클로저 및 PCM hello EBOD 컨트롤러의 일부분이 아닌에 hello 구성 요소를 표시 합니다.
* **EBOD 컨트롤러 0 구성 요소** – hello SAS 확장기 및 커넥터, 컨트롤러 온도 센서 hello EBOD 컨트롤러와 같이 EBOD 인클로저 0에 있는 구성 요소입니다.
* **EBOD 컨트롤러 1 구성 요소** – hello EBOD 인클로저 1을 구성 하는 구성 요소 유사한 toothose EBOD 인클로저 0에 대해 자세히 설명 합니다.

> [!NOTE]
> **hello 하드웨어 상태 섹션 (1100) StorSimple 가상 장치에 대 한 hello 유지 관리 페이지에 나타나지 않습니다.**
> 
> 

## <a name="monitor-hello-hardware-status"></a>Hello 하드웨어 상태 모니터링
Hello 장치 구성 요소 단계 tooview hello 하드웨어 상태를 다음을 수행 합니다.

1. 너무 이동**장치**, 특정 StorSimple 장치를 선택 합니다. Toogo hello 장치 수준 메뉴를 클릭 한 다음 클릭 **유지 관리**합니다. 
2. Hello 찾을 **하드웨어 상태** 섹션 하 고 (위에서 설명한) hello 사용 가능한 구성 요소에서 선택 합니다. 다양 한 장치 구성 요소 앞에 hello 구성 요소 레이블 tooexpand hello 목록 및 보기 hello 상태 hello의 화살표 키를 누르기만 합니다. Hello 참조 [기본 인클로저 hello에 대 한 자세한 구성 요소 목록](#component-list-for-primary-enclosure-of-storsimple-device) 및 hello [EBOD 인클로저 hello에 대 한 자세한 구성 요소 목록](#component-list-for-ebod-enclosure-of-storsimple-device)합니다.
3. 색 구성표 toointerpret 구분 hello 구성 요소 상태에 따라 hello를 사용 합니다.
   
   * **녹색 확인 표시** – **정상** 또는 **확인** 구성 요소를 표시합니다.
   * **노란색** – **경고** 상태의 구성 요소를 표시합니다.
   * **빨간색 느낌표** – **실패** 또는 **주의 필요** 상태인 구성 요소를 표시합니다.
   * **검정 텍스트에 흰색** – 존재하지 않는 구성 요소를 표시합니다.
4. **정상** 상태가 아닌 구성 요소가 있는 경우 Microsoft 지원에 문의하세요. 장치에서 경고를 설정한 경우, 메일 경고를 받게 됩니다. Tooreplace 장애가 발생 한 하드웨어 구성 요소를 보려면 참고 [StorSimple 하드웨어 구성 요소 교체](storsimple-hardware-component-replacement.md)합니다.

## <a name="component-list-for-primary-enclosure-of-storsimple-device"></a>StorSimple 장치의 기본 인클로저에 대한 구성 요소 목록
hello 다음 표에 정리 되어 hello 온-프레미스 StorSimple 장치의 기본 인클로저에 hello에 포함 된 물리적 및 논리적 구성 요소입니다.

| 구성 요소 | 모듈 | 형식 | 위치 | FRU(Field replaceable unit)? | 설명 |
| --- | --- | --- | --- | --- | --- |
| 슬롯 [0-11]의 드라이브 |디스크 드라이브 |물리적 |공유됨 |예 |Hello 기본 인클로저 내의 hello HDD 드라이브에 있거나 각 SSD hello에 대 한 한 줄이 표시 됩니다. |
| 주변 온도 센서 |엔클로저 |물리적 |공유됨 |아니요 |측정값 hello hello 섀시 내의 온도 합니다. |
| 중간 평면 온도 센서 |엔클로저 |물리적 |공유됨 |아니요 |측정값의 hello 중간 평면 온도 hello 합니다. |
| 청각적 경고 |엔클로저 |물리적 |공유됨 |아니요 |Hello 섀시 내의 hello 청각적 경보 하위 시스템 작동 여부를 나타냅니다. |
| 인클로저 |엔클로저 |물리적 |공유됨 |예 |Hello 섀시 유무를 나타냅니다. |
| 인클로저 설정 |엔클로저 |물리적 |공유됨 |아니요 |Toohello hello 섀시 전면 패널을 나타냅니다. |
| 정격 전압 센서 |PCM |물리적 |공유됨 |아니요 |다양 한 정격 전압 센서가 허용 오차 이내 인지 hello 측정 하는지 여부를 나타내는 상태를 표시 합니다. |
| 정격 전류 센서 |PCM |물리적 |공유됨 |아니요 |다양 한 선 전류 센서 있는 인지 여부를 나타내는 hello 측정 허용 오차 이내 상태를 표시 합니다. |
| PCM의 온도 센서 |PCM |물리적 |공유됨 |아니요 |다양 한 온도 센서 유입 및 핫스폿 센서는 hello 온도 측정 하는지 여부를 나타내는 상태를 표시와 같은 허용 오차 이내 인지 합니다. |
| 전원 공급 장치 [0-1] |PCM |물리적 |공유됨 |예 |한 줄 hello hello 장치의 후면에 있는 두 개의 Pcm 각각 hello에 hello 전원 공급 장치에 대해 표시 됩니다. |
| 냉각 장치 [0-1] |PCM |물리적 |공유됨 |예 |한 줄 두 Pcm hello에 있는 4 개 냉각 팬 각각 hello에 대 한 표시 됩니다. |
| 배터리 [0-1] |PCM |물리적 |공유됨 |예 |한 줄 각 hello PCM에에서 장착 된 hello 백업 배터리 모듈에 대해 표시 됩니다. |
| Metis |해당 없음 |논리 |공유됨 |해당 없음 |Hello 배터리 hello 상태가 표시 됩니다: 다했는지 및 수명 끝에 도달 하 고 있는지 여부. |
| 프로비전 |해당 없음 |논리 |공유됨 |해당 없음 |표시 hello hello 두 통합된 컨트롤러 모듈 간에 만들어지는 hello 클러스터의 상태입니다. |
| 클러스터 노드 |해당 없음 |논리 |공유됨 |해당 없음 |Hello 클러스터의 일부로 hello 컨트롤러의 hello 상태를 나타냅니다. |
| 클러스터 쿼럼 |해당 없음 |논리 | |해당 없음 |Hello로 HDD 저장소 풀의 과반수 디스크 멤버 자격 hello의 hello 존재 여부를 나타냅니다. |
| HDD 데이터 공간 |해당 없음 |논리 |공유됨 |해당 없음 |hello 하드 디스크 드라이브 (HDD) 저장소 풀의 데이터에 사용 되는 hello 저장소 공간입니다. |
| HDD 관리 공간 |해당 없음 |논리 |공유됨 |해당 없음 |hello 공간 hello 관리 작업용으로 HDD 저장소 풀에에서 예약 되어 있습니다. |
| HDD 쿼럼 공간 |해당 없음 |논리 |공유됨 |해당 없음 |클러스터 쿼럼에 대 한 HDD 저장소 풀에 hello hello 공간이 예약 합니다. |
| HDD 교체 공간 |해당 없음 |논리 |공유됨 |해당 없음 |hello 공간 hello 컨트롤러 교체용으로 HDD 저장소 풀에에서 예약 되어 있습니다. |
| SSD 데이터 공간 |해당 없음 |논리 |공유됨 |해당 없음 |hello 저장 공간이 hello 반도체 드라이브 (SSD) 저장소 풀의 데이터에 사용 합니다. |
| SSD NVRAM 공간 |해당 없음 |논리 |공유됨 |해당 없음 |hello hello NVRAM 논리 전용 SSD 저장소 풀에서에서 저장소 공간입니다. |
| HDD 저장소 풀 |해당 없음 |논리 |공유됨 |해당 없음 |표시 hello 장치 Hdd에서에서 작성 하는 hello 논리적 저장소 풀의 상태입니다. |
| SSD 저장소 풀 |해당 없음 |논리 |공유됨 |해당 없음 |표시 hello 장치 Ssd에서에서 작성 하는 hello 논리적 저장소 풀의 상태입니다. |
| 컨트롤러 [0-1] [state] |I/O |물리적 |Controller |예 |Hello 컨트롤러의 hello 상태를 표시 및 hello 섀시 내에서 활성 또는 대기 모드 인지 합니다. |
| 컨트롤러의 온도 센서 |I/O |물리적 |Controller |아니요 |I/O 모듈, CPU 온도, DIMM 및 PCIe 센서와 같은 다양 한 온도 센서 있는 hello 확인 된 온도가 허용 오차 이내 인지 여부를 나타내는 상태를 표시 합니다. |
| SAS 확장기 |I/O |물리적 |Controller |아니요 |Hello 직렬 연결 된 SAS (SCSI) 확장기의 사용 되는 tooconnect hello 통합된 저장소 toohello 컨트롤러는 hello 상태를 나타냅니다. |
| SAS 커넥터 [0-1] |I/O |물리적 |Controller |아니요 |각 SAS 커넥터를 사용 하는 tooconnect 통합 저장소 toohello SAS 확장기의 hello 상태를 나타냅니다. |
| SBB 중간 평면 상호 연결 |I/O |물리적 |Controller |아니요 |각 컨트롤러 toohello 중간 평면 tooconnect 사용된 되는 hello 중간 평면 커넥터의 hello 상태를 나타냅니다. |
| 프로세서 코어 |I/O |물리적 |Controller |아니요 |각 컨트롤러 내의 hello 프로세서 코어의 hello 상태를 나타냅니다. |
| 인클로저 전자 기기 전원 |I/O |물리적 |Controller |아니요 |Hello 인클로저에서 사용 하는 hello 전원 시스템의 hello 상태를 나타냅니다. |
| 인클로저 전자 기기 진단 |I/O |물리적 |Controller |아니요 |Hello 컨트롤러에서 제공 하는 hello 진단 하위 시스템의 hello 상태를 나타냅니다. |
| 베이스 보드 관리 컨트롤러(BMC) |I/O |물리적 |Controller |아니요 |Hello 베이스 보드 관리 컨트롤러의 (BMC) 센서를 통해 hello 하드웨어 장치를 모니터링 하 고 독립 연결을 통해 시스템 관리자에 게와 통신 하는 특수 서비스 프로세서인은 hello 상태를 나타냅니다. |
| 이더넷 |I/O |물리적 |Controller |아니요 |각 hello 네트워크 인터페이스, 즉, hello 관리 및 hello 컨트롤러에서 제공 하는 데이터 포트의 hello 상태를 나타냅니다. |
| NVRAM |I/O |물리적 |Controller |아니요 |Hello 상태를 NVRAM hello 배터리 전원 오류의 hello 이벤트에 tooretain 응용 프로그램에 중요 한 정보를 제공 하 여 백업 비휘발성 임의 액세스 메모리를 나타냅니다. |

## <a name="component-list-for-ebod-enclosure-of-storsimple-device"></a>StorSimple 장치의 EBOD 인클로저에 대한 구성 요소 목록
hello 다음 표에 정리 되어 hello 온-프레미스 StorSimple 장치의 EBOD 인클로저 hello에 포함 된 물리적 및 논리적 구성 요소입니다.

| 구성 요소 | 모듈 | 형식 | 위치 | FRU? | 설명 |
| --- | --- | --- | --- | --- | --- |
| 슬롯 [0-11]의 드라이브 |디스크 드라이브 |물리적 |공유됨 |예 |한 줄 각 HDD 드라이브 hello hello EBOD 인클로저 앞면에 hello에 대 한 표시 됩니다. |
| 주변 온도 센서 |엔클로저 |물리적 |공유됨 |아니요 |측정값 hello hello 섀시 내의 온도 합니다. |
| 중간 평면 온도 센서 |엔클로저 |물리적 |공유됨 |아니요 |측정값의 hello 중간 평면 온도 hello 합니다. |
| 청각적 경고 |엔클로저 |물리적 |공유됨 |아니요 |Hello 섀시 내의 hello 청각적 경보 하위 시스템 작동 여부를 나타냅니다. |
| 인클로저 |엔클로저 |물리적 |공유됨 |예 |Hello 섀시 유무를 나타냅니다. |
| 인클로저 설정 |엔클로저 |물리적 |공유됨 |아니요 |Hello hello 섀시 전면 패널 또는 OPS toohello 참조합니다. |
| 정격 전압 센서 |PCM |물리적 |공유됨 |아니요 |다양 한 정격 전압 센서가 허용 오차 이내 인지 hello 측정 하는지 여부를 나타내는 상태를 표시 합니다. |
| 정격 전류 센서 |PCM |물리적 |공유됨 |아니요 |다양 한 선 전류 센서 있는 인지 여부를 나타내는 hello 측정 허용 오차 이내 상태를 표시 합니다. |
| PCM의 온도 센서 |PCM |물리적 |공유됨 |아니요 |다양 한 온도 센서 유입 및 핫스폿 센서는 hello 온도 측정 하는지 여부를 나타내는 상태를 표시와 같은 허용 오차 이내 인지 합니다. |
| 전원 공급 장치 [0-1] |PCM |물리적 |공유됨 |예 |한 줄 hello hello 장치의 후면에 있는 두 개의 Pcm 각각 hello에 hello 전원 공급 장치에 대해 표시 됩니다. |
| 냉각 장치 [0-1] |PCM |물리적 |공유됨 |예 |한 줄 두 Pcm hello에 있는 4 개 냉각 팬 각각 hello에 대 한 표시 됩니다. |
| 로컬 저장소 [HDD] |해당 없음 |논리 |공유됨 |해당 없음 |표시 hello 장치 Hdd에서에서 작성 하는 hello 논리적 저장소 풀의 상태입니다. |
| 컨트롤러 [0-1] [state] |I/O |물리적 |Controller |예 |표시 hello hello EBOD 모듈의 hello 컨트롤러 상태입니다. |
| EBOD의 온도 센서 |I/O |물리적 |Controller |아니요 |각 컨트롤러에서 다양 한 온도 센서 있는 hello 확인 된 온도가 허용 오차 이내 인지 여부를 나타내는 상태를 표시 합니다. |
| SAS 확장기 |I/O |물리적 |Controller |아니요 |사용 되는 tooconnect hello 통합된 저장소 toohello 컨트롤러는 hello SAS 확장기의 hello 상태를 나타냅니다. |
| SAS 커넥터 [0-2] |I/O |물리적 |Controller |아니요 |각 SAS 커넥터를 사용 하는 tooconnect 통합 저장소 toohello SAS 확장기의 hello 상태를 나타냅니다. |
| SBB 중간 평면 상호 연결 |I/O |물리적 |Controller |아니요 |각 컨트롤러 toohello 중간 평면 tooconnect 사용된 되는 hello 중간 평면 커넥터의 hello 상태를 나타냅니다. |
| 인클로저 전자 기기 전원 |I/O |물리적 |Controller |아니요 |Hello 인클로저에서 사용 하는 hello 전원 시스템의 hello 상태를 나타냅니다. |
| 인클로저 전자 기기 진단 |I/O |물리적 |Controller |아니요 |Hello 컨트롤러에서 제공 하는 hello 진단 하위 시스템의 hello 상태를 나타냅니다. |
| 연결 toodevice 컨트롤러 |I/O |물리적 |Controller |아니요 |Hello EBOD I/O 모듈과 장치 컨트롤러 hello 간의 hello 연결의 hello 상태를 나타냅니다. |

## <a name="next-steps"></a>다음 단계
* toouse hello StorSimple 관리자 서비스 tooadminister 장치를 이동 너무[사용 하 여 StorSimple 장치를 StorSimple Manager 서비스 tooadminister hello](storsimple-manager-service-administration.md)합니다.
* Tootroubleshoot 저하 또는 실패 상태에 있는 장치 구성 요소, 필요한 경우 너무 참조 [StorSimple 모니터링 표시기](storsimple-monitoring-indicators.md)합니다. 
* tooreplace 장애가 발생 한 하드웨어 구성 요소 참조 [StorSimple 하드웨어 구성 요소 교체](storsimple-hardware-component-replacement.md)합니다.
* Tooexperience 장치 문제를 계속 하면 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md)합니다.

