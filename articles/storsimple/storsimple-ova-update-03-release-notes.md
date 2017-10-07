---
title: "aaaStorSimple 가상 배열 업데이트 릴리스 정보 | Microsoft Docs"
description: "중요 한 열에 설명 문제 및 해결 hello StorSimple 가상 배열 실행에 대 한 업데이트 0.3 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: b197651a-3c40-4185-b23d-4c8f22cfa8f4
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/15/2016
ms.author: alkohli
ms.openlocfilehash: 305e6419b248fde134abae65f3d2c241d72ffa18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-03-release-notes"></a>StorSimple 가상 배열 업데이트 0.3 릴리스 정보
## <a name="overview"></a>개요
hello 다음 릴리스 정보 hello 중요 한 미해결 문제를 식별 하 고 hello Microsoft Azure StorSimple 가상 배열 업데이트에 대 한 문제를 해결된 합니다.

hello 릴리스 정보 지속적으로 업데이트 되 고, 해결 방법이 필요한 중요 한 문제가 발견 되 면 추가 됩니다. StorSimple 가상 배열을 배포 하기 전에 신중 하 게 hello 릴리스 정보에 포함 된 hello 정보를 검토 합니다.

Toohello 소프트웨어 버전을 해당 하는 업데이트 0.3 **10.0.10288.0**합니다.

> [!NOTE]
> 업데이트는 작업 중단 업데이트이며 장치를 다시 시작합니다. I/O가 진행 중인 경우 hello 장치 가동 중지 시간이 발생 합니다.
> 
> 

## <a name="whats-new-in-hello-update-03"></a>Hello 업데이트 0.3의에서 새로운 기능
업데이트 0.3은 주로 버그 수정 빌드입니다. 이 버전에서는 hello 이전 버전에서 백업 오류를 일으키는 몇몇 버그가 해결 되었습니다.

## <a name="issues-fixed-in-hello-update-03"></a>Hello 업데이트 0.3에서에서 해결 된 문제
hello 다음 표에서이 릴리스에서 수정 된 문제에 대 한 요약.

| 아니요. | 기능 | 문제 |
| --- | --- | --- |
| 1 |백업 |문제가 hello 였던 이전 릴리스 hello 백업 파일 공유에 대 한 toocomplete를 실패 합니다. 이 문제가 발생 한 경우 hello 백업 작업은 실패 하 고 hello StorSimple 관리자 서비스 toonotify hello 사용자에서 중요 한 경고가 발생 합니다. 이 문제 hello 공유에 hello 데이터에 영향을 하지 않았거나 toohello 데이터에 액세스 합니다. hello 근본 원인은 파악 하 고이 릴리스에서 수정 되었습니다. <br></br> 이 문제를 표시 중 tooshares hello 수정 소급 적용 되지 않습니다. 고객에 게 표시 되 고이 문제를 먼저 업데이트 0.3, 적용 다음 Microsoft 지원 tooperform 전체 시스템 백업 toofix hello 문제를 문의 하십시오. Microsoft 지원에 문의 하는 대신 고객 영향을 받는 hello 공유에 대 한 정상 백업에서 tooa 새 공유를 복원할 수도 있습니다. |
| 2 |iSCSI |문제가 hello 였던 hello 볼륨 사라지고 여기서 데이터 tooa 볼륨 hello StorSimple 가상 배열에 복사 하는 경우 이전 릴리스 합니다. 이 문제는 이 릴리스에서 해결되었습니다. <br></br> hello 수정 내용이 적용의 경우에 새로 만든 볼륨. 이 문제를 표시 중 toovolumes hello 수정 소급 적용 되지 않습니다. 취해야 toobring hello 영향을 받는 볼륨을 온라인 hello Azure 클래식 포털을 통해 이러한 볼륨에 대 한 백업을 수행 하 고 이러한 볼륨 toonew 볼륨을 복원 합니다. |

## <a name="known-issues-in-hello-update-03"></a>Hello 업데이트 0.3의에서 알려진된 문제
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
| **8.** |공유에 사용된 용량 |표시 될 수 있습니다 hello 공유에 데이터가 없는 경우 소비를 공유 합니다. 즉, 사용 하는 hello 용량 공유에 대 한 메타 데이터가 포함 됩니다. | |
| **9.** |재해 복구 |파일 서버 toohello의 hello 재해 복구만 수행할 수 있습니다는 소스 장치 hello와 동일한 도메인입니다. 다른 도메인의 재해 복구 tooa 대상 장치는이 릴리스에서 지원 되지 않습니다. |이후 릴리스에서 구현됩니다. |
| **10.** |Azure PowerShell |이 릴리스에서 hello Azure PowerShell을 통해 hello StorSimple 가상 장치를 관리할 수 없습니다. |Hello 가상 장치의 모든 hello 관리 hello Azure 클래식 포털 및 hello 로컬 웹 UI 통해 수행 되어야 합니다. |
| **11.** |암호 변경 |hello 가상 배열 장치 콘솔 EN-US 키보드 형식으로 입력을 허용합니다. | |
| **12.** |CHAP |CHAP 자격 증명은 일단 한 번 만들면 제거할 수 없습니다. 또한 hello CHAP 자격 증명을 수정 하면 하면 필요한 tootake hello 볼륨이 오프 라인으로 전환한 다음 온라인 tootake 효과 변경 하는 hello에 대 한 합니다. |이 문제는 이후 릴리스에서 해결됩니다. |
| **13.** |iSCSI 서버 |iSCSI 볼륨에 대 한 표시 '저장소를 사용한' hello hello StorSimple Manager 서비스와 hello iSCSI 호스트에서 달라질 수 있습니다. |hello iSCSI 호스트에 hello 파일 시스템 보기가 있습니다.<br></br>hello 장치 hello 볼륨 hello 최대 크기로 때 할당 된 hello 블록을 볼 수 있습니다. |
| **14.** |파일 서버 |폴더에 파일에는 대체 데이터 스트림 (광고) 연결 되어 있는 경우 hello 광고를 백업 하지 또는 재해 복구, 복제, 및 항목 수준 복구를 통해 복원 되 합니다. | |

## <a name="next-step"></a>다음 단계
[업데이트 0.3을 설치](storsimple-ova-install-update-01.md) 합니다.

## <a name="references"></a>참조
이전 릴리스 정보를 찾으시나요? 다음으로 이동합니다. 

* [StorSimple 가상 배열 업데이트 0.1 및 0.2 릴리스 정보](storsimple-ova-update-01-release-notes.md)
* [StorSimple 가상 배열 일반 공급 릴리스 정보](storsimple-ova-pp-release-notes.md)

