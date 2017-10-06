---
title: "aaaStorSimple 가상 배열 업데이트 0.5 릴리스 정보 | Microsoft Docs"
description: "중요 한 열에 설명 문제 및 해결 hello StorSimple 가상 배열 실행에 대 한 0.5를 업데이트 합니다."
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
ms.workload: NA
ms.date: 05/08/2017
ms.author: alkohli
ms.openlocfilehash: a249e2e8f0105dcf6cc02d3136dfa3e37ea615d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-05-release-notes"></a>StorSimple 가상 배열 업데이트 0.5 릴리스 정보

## <a name="overview"></a>개요

hello 다음 릴리스 정보 hello 중요 한 미해결 문제를 식별 하 고 hello Microsoft Azure StorSimple 가상 배열 업데이트에 대 한 문제를 해결된 합니다.

hello 릴리스 정보 지속적으로 업데이트 되 고, 해결 방법이 필요한 중요 한 문제가 발견 되 면 추가 됩니다. StorSimple 가상 배열을 배포 하기 전에 신중 하 게 hello 릴리스 정보에 포함 된 hello 정보를 검토 합니다.

Toohello 소프트웨어 버전을 해당 하는 업데이트 0.5 **10.0.10290.0**합니다.

> [!NOTE]
> 업데이트는 작업 중단 업데이트이며 장치를 다시 시작합니다. I/O가 진행 중인 경우 hello 장치 가동 중지 시간이 발생 합니다. Tooapply 업데이트 hello 하는 방법에 자세한 내용은 이동 너무[설치 업데이트 0.5](storsimple-virtual-array-install-update-05.md)합니다.


## <a name="whats-new-in-hello-update-05"></a>Hello 0.5 업데이트의에서 새로운 기능
업데이트 0.5는 주로 버그 수정 빌드입니다. hello 주 기능 향상 및 버그 수정 프로그램은 다음과 같습니다.

- **향상 된 복원 력 백업** -이 릴리스에 hello 백업 복원 력을 향상 된 수정 사항입니다. Hello에 특정 예외에 대 한 이전 버전에서 백업을 다시 시도한 합니다. 이 릴리스에서 모든 hello 백업 예외를 다시 시도 하 고는 hello 백업을 복원 성도 뛰어납니다.

- **저장소 사용 현황 모니터링에 대 한 업데이트** -저장소 사용 현황 모니터링 StorSimple 가상 장치 시리즈 사용 중지 된 hello 30 년 6 월 2017을 시작 합니다. 이 toohello 모니터링 차트 0.4 이하로 업데이트를 실행 중인 모든 hello 가상 배열에 적용 됩니다. 이 업데이트 하면 toocontinue hello 사용 모니터링 hello에 Azure 포털 저장소 사용에 필요한 hello 변경 포함 되어 있습니다. 2017 년 6 월 30 하기 전에 중요 업데이트를 설치 toocontinue hello 모니터링 기능을 사용 하 여 합니다.


## <a name="issues-fixed-in-hello-update-05"></a>Hello 0.5 업데이트에서에서 해결 된 문제

hello 다음 표에서이 릴리스에서 수정 된 문제에 대 한 요약.

| 아니요. | 기능 | 문제 |
| --- | --- | --- |
| 1 |백업 복원력| Hello에 특정 예외에 대 한 이전 버전에서 백업을 다시 시도한 합니다. 이 릴리스에 모든 hello 백업 예외를 다시 시도 하 여 복원 성도 뛰어납니다. 수정 toomake 백업을 포함 됩니다.|
| 2 |모니터링| StorSimple 가상 장치 시리즈에 대 한 저장소 사용 현황 모니터링 hello 2017 년 6 월 30 시작 중단 될 예정입니다. 이 작업에는 StorSimple 가상 배열에서 실행 되는 hello StorSimple 장치 관리자 서비스에 차트를 모니터링 하는 hello 영향을 줍니다. (1200 모델). 이 릴리스에 2017 년 6 월 30 이외의 hello 가상 배열에 저장소 사용 현황 모니터링의 hello 사용자 toocontinue hello 사용을 허용 하는 업데이트 합니다.|
| 3 |파일 서버| Hello에 이전 버전에서 사용자 toohello 가상 배열 암호화 된 파일을 실수로 복사할 수 있습니다. 이 릴리스에 toovirtual 배열 암호화 된 파일의 복사를 허용 하지 않았습니다 하는 수정 프로그램이 포함 되어 있습니다. 백업 장치에는 업데이트는 기존의 암호화 된 파일은 이전 toohello, 모든 암호화 hello 파일 hello 시스템에서 삭제 될 때까지 toofail을 계속 됩니다. |


## <a name="known-issues-in-hello-update-05"></a>Hello 업데이트 0.5의에서 알려진된 문제

hello 다음 표에서 hello StorSimple 가상 배열에 대 한 알려진된 문제에 대해 간략하게 설명 하 고 hello 이전 버전에서 릴리스 언급 된 hello 문제가 포함 됩니다.

| 아니요. | 기능 | 문제 | 해결 방법/설명 |
| --- | --- | --- | --- |
| **1.** |업데이트 |hello 미리 보기 릴리스에서 만든 hello 가상 장치는 지원 되는 업데이트 된 tooa 일반 공급 버전 일 수 없습니다. |재해 복구 (DR) 워크플로 사용 하 여 일반 공급 릴리스 hello에 대 한 이러한 가상 장치를 장애 조치 해야 합니다. |
| **2.** |프로비전된 데이터 디스크 |지정된 된 특정 크기의 데이터 디스크를 프로 비전 한 번 및 hello 해당 StorSimple 가상 장치 생성을 확장 하거나 하며 hello 데이터 디스크를 축소 합니다. Hello hello 장치의 로컬 계층에 모든 hello 데이터의 손실에서 toodo 결과 시도합니다. | |
| **3.** |그룹 정책 |장치가 도메인에 가입 된 경우 그룹 정책을 적용 저하 될 수 있습니다 hello 장치 작업 합니다. |가상 배열 자체 Active Directory에 대 한 조직 구성 단위 (OU)에 그룹 정책 개체 (GPO)은 적용 된 tooit 확인. |
| **4.** |로컬 웹 UI |Internet Explorer (IE ESC)에서 향상된 보안 기능이 활성화된 경우 문제 해결 또는 유지 관리와 같은 일부 로컬 웹 UI 페이지가 적절하게 작동하지 않을 수 있습니다. 해당 페이지의 단추도 작동하지 않을 수 있습니다. |Internet Explorer의 보안 강화 기능을 해제하십시오. |
| **5.** |로컬 웹 UI |Hyper-v 가상 컴퓨터에서 안녕 네트워크 인터페이스 hello 웹 UI 10 g b p s 인터페이스도 표시 됩니다. |이러한 동작은 Hyper-V를 반영합니다. Hyper-V는 가상 네트워크 어댑터에 10Gbps를 항상 표시합니다. |
| **6.** |계층화된 볼륨 또는 공유 |계층화 된 볼륨을 StorSimple hello를 사용 하는 응용 프로그램에 대 한 잠금을 바이트 범위 지원 되지 않습니다. 바이트 범위 잠금을 사용하도록 설정하면 StorSimple 계층화가 실행되지 않습니다. |권장된 조치는 다음과 같습니다. <br></br>응용 프로그램 논리에서 바이트 범위 잠금을 해제합니다.<br></br>달리 tootiered 볼륨 로컬로 고정 된 볼륨에서이 응용 프로그램에 대 한 tooput 데이터를 선택 합니다.<br></br>*주의할*: 고정 된 볼륨을 로컬에서 사용 하 고 바이트 범위 잠금 사용 됨을 로컬로 고정 hello 볼륨 전에 있을 수 있는 온라인도 hello 복원이 완료 되었습니다. 이러한 경우 복원이 진행 중인 경우 다음 대기 해야 hello 복원 toocomplete 합니다. |
| **7.** |계층화된 공유 |큰 파일로 작업하면 계층화가 매우 느려질 수 있습니다. |큰 파일을 사용 하는 경우에 hello이 가장 큰 파일은 hello 공유 크기의 3% 보다 작은 것이 좋습니다. |
| **8.** |공유에 사용된 용량 |표시 될 수 있습니다 hello 공유에 데이터가 없는 경우 소비를 공유 합니다. 이 사용량이 메타 데이터를 포함 하는 공유에 대 한 용량 hello 사용 되기 때문입니다. | |
| **9.** |재해 복구 |파일 서버 toohello의 hello 재해 복구만 수행할 수 있습니다는 소스 장치 hello와 동일한 도메인입니다. 다른 도메인의 재해 복구 tooa 대상 장치는이 릴리스에서 지원 되지 않습니다. |이후 릴리스에서 구현됩니다. 자세한 내용은 이동 너무[StorSimple 가상 배열에 대 한 장애 조치 및 재해 복구](storsimple-virtual-array-failover-dr.md) |
| **10.** |Azure PowerShell |이 릴리스에서 hello Azure PowerShell을 통해 hello StorSimple 가상 장치를 관리할 수 없습니다. |Hello 가상 장치의 모든 hello 관리는 Azure 포털 및 hello 로컬 웹 UI hello를 통해 수행 해야 합니다. |
| **11.** |암호 변경 |hello 가상 배열 장치 콘솔만 입력을 허용 en에서-형식 키보드 주세요. | |
| **12.** |CHAP |CHAP 자격 증명은 일단 한 번 만들면 제거할 수 없습니다. 또한 hello CHAP 자격 증명을 수정 하면 하면 필요한 tootake hello 볼륨이 오프 라인으로 전환한 다음 온라인 tootake 효과 변경 하는 hello에 대 한 합니다. |이 문제는 이후 릴리스에서 해결됩니다. |
| **13.** |iSCSI 서버 |iSCSI 볼륨에 대 한 표시 '저장소를 사용한' hello hello StorSimple 장치 관리자 서비스와 hello iSCSI 호스트에서 달라질 수 있습니다. |hello iSCSI 호스트에 hello 파일 시스템 보기가 있습니다.<br></br>hello 장치 hello 볼륨 hello 최대 크기로 때 할당 된 hello 블록을 볼 수 있습니다. |
| **14.** |파일 서버 |폴더에 파일에는 대체 데이터 스트림 (광고) 연결 되어 있는 경우 hello 광고를 백업 하지 또는 재해 복구, 복제, 및 항목 수준 복구를 통해 복원 되 합니다. | |
| **15.** |파일 서버 |기호 링크는 지원되지 않습니다. | |
| **16.** |파일 서버 |파일에서 Windows 파일 시스템 EFS (암호화)을 통해 복사 하는 경우 보호 또는에 저장 된 hello StorSimple 가상 배열 파일 서버 결과 구성이 지원 합니다.  | |

## <a name="next-step"></a>다음 단계
StorSimple 가상 배열에 [업데이트 0.5를 설치](storsimple-virtual-array-install-update-05.md)합니다.

## <a name="references"></a>참조
이전 릴리스 정보를 찾으시나요? 다음으로 이동합니다.

* [StorSimple 가상 배열 업데이트 0.4 릴리스 정보](storsimple-virtual-array-update-04-release-notes.md)
* [StorSimple 가상 배열 업데이트 0.3 릴리스 정보](storsimple-ova-update-03-release-notes.md)
* [StorSimple 가상 배열 업데이트 0.1 및 0.2 릴리스 정보](storsimple-ova-update-01-release-notes.md)
* [StorSimple 가상 배열 일반 공급 릴리스 정보](storsimple-ova-pp-release-notes.md)

