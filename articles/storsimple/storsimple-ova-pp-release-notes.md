---
title: "aaaStorSimple 가상 배열 릴리스 정보 | Microsoft Docs"
description: "중요 한 미해결 문제 및 StorSimple 가상 배열 hello에 대 한 해결 방법을 설명합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 84908160-2b8b-4f4f-a674-f39aaa0bd4de
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/13/2016
ms.author: alkohli
ms.openlocfilehash: ca7b543f95cf5787b7fef39f53887161ebfa7fcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-release-notes"></a>StorSimple 가상 배열 릴리스 정보
## <a name="overview"></a>개요
hello 다음 릴리스 정보 식별 hello hello Microsoft Azure StorSimple 가상 배열 (라고도 hello StorSimple 온-프레미스 가상 장치 또는 StorSimple 가상 hello의 hello 2016 년 3 월 GA (일반 공급) 릴리스에 대 한 중요 한 미해결 문제 장치)입니다. 이 릴리스 toosoftware 버전 10.0.10271.0 해당합니다.

hello 릴리스 정보 지속적으로 업데이트 되 고, 해결 방법이 필요한 중요 한 문제가 발견 되 면 추가 됩니다. StorSimple 가상 장치를 배포 하기 전에 신중 하 게 hello 릴리스 정보에 포함 된 hello 정보를 검토 합니다. 

다음 표에서 hello이이 릴리스의 알려진된 문제에에서 대 한 요약을 제공 합니다.

| 아니요. | 기능 | 문제 | 해결 방법/설명 |
| --- | --- | --- | --- |
| **1.** |업데이트 |hello 미리 보기 릴리스에서 만든 hello 가상 장치는 지원 되는 업데이트 된 tooa 일반 공급 버전 일 수 없습니다. |재해 복구 (DR) 워크플로 사용 하 여 일반 공급 릴리스 hello에 대 한 이러한 가상 장치를 장애 조치 해야 합니다. |
| **2.** |프로비전된 데이터 디스크 |지정된 된 특정 크기의 데이터 디스크를 프로 비전 한 번 및 hello 해당 StorSimple 가상 장치 생성을 확장 하거나 하며 hello 데이터 디스크를 축소 합니다. Toodo 하므로 발생 합니다 hello hello 장치의 로컬 계층에 모든 hello 데이터의 손실입니다. | |
| **3.** |그룹 정책 |장치가 도메인에 가입 된 경우 그룹 정책을 적용 저하 될 수 있습니다 hello 장치 작업 합니다. |가상 배열 자체 Active Directory에 대 한 조직 구성 단위 (OU)에 그룹 정책 개체 (GPO)은 적용 된 tooit 확인. |
| **4.** |로컬 웹 UI |Internet Explorer (IE ESC)에서 향상된 보안 기능이 활성화된 경우 문제 해결 또는 유지 관리와 같은 일부 로컬 웹 UI 페이지가 적절하게 작동하지 않을 수 있습니다. 해당 페이지의 단추도 작동하지 않을 수 있습니다. |Internet Explorer의 보안 강화 기능을 해제하십시오. |
| **5.** |로컬 웹 UI |Hyper-v 가상 컴퓨터에서 안녕 네트워크 인터페이스 hello 웹 UI 10 g b p s 인터페이스도 표시 됩니다. |이러한 동작은 Hyper-V를 반영합니다. Hyper-V는 가상 네트워크 어댑터에 10Gbps를 항상 표시합니다. |
| **6.** |계층화된 볼륨 또는 공유 |계층화 된 볼륨을 StorSimple hello를 사용 하는 응용 프로그램에 대 한 잠금을 바이트 범위 지원 되지 않습니다. 바이트 범위 잠금을 사용하도록 설정하면 StorSimple 계층화가 실행되지 않습니다. |권장된 조치는 다음과 같습니다. <br></br>응용 프로그램 논리에서 바이트 범위 잠금을 해제합니다.<br></br>달리 tootiered 볼륨 로컬로 고정 된 볼륨에서이 응용 프로그램에 대 한 tooput 데이터를 선택 합니다.<br></br>*주의할*: 고정 된 볼륨을 로컬에서 사용 하 고 바이트 범위 잠금이 설정 하는 경우 hello 복원 작업이 완료 되기 전에 hello 로컬로 고정 볼륨 수 온라인 수 주의 해야 합니다. 이러한 경우 복원이 진행 중인 경우 다음 대기 해야 hello 복원 toocomplete 합니다. |
| **7.** |계층화된 공유 |큰 파일로 작업하면 계층화가 매우 느려질 수 있습니다. |큰 파일을 사용 하는 경우에 hello이 가장 큰 파일은 hello 공유 크기의 3% 보다 작은 것이 좋습니다. |
| **8.** |공유에 사용된 용량 |표시 될 수 있습니다 hello 없는 경우 hello 공유에 있는 모든 데이터 소비를 공유 합니다. 즉, 사용 하는 hello 용량 공유에 대 한 메타 데이터가 포함 됩니다. | |
| **9.** |재해 복구 |파일 서버 toohello의 hello 재해 복구만 수행할 수 있습니다는 소스 장치 hello와 동일한 도메인입니다. 다른 도메인의 재해 복구 tooa 대상 장치는이 릴리스에서 지원 되지 않습니다. |이후 릴리스에서 구현될 예정입니다. |
| **10.** |Azure PowerShell |이 릴리스에서 hello Azure PowerShell을 통해 hello StorSimple 가상 장치를 관리할 수 없습니다. |Hello 가상 장치의 모든 hello 관리 hello Azure 클래식 포털 및 hello 로컬 웹 UI 통해 수행 되어야 합니다. |
| **11.** |암호 변경 |hello 가상 배열 장치 콘솔 EN-US 키보드 형식으로 입력을 허용합니다. | |
| **12.** |CHAP |CHAP 자격 증명은 일단 한 번 만들면 제거할 수 없습니다. 또한 hello CHAP 자격 증명을 수정 하면 tootake hello 볼륨이 오프 라인 필요를 tootake 효과 변경 하는 hello에 대 한 온라인 상태로 전환 합니다. |이것은 이후 릴리스에서 해결될 예정입니다. |
| **13.** |iSCSI 서버 |iSCSI 볼륨에 대 한 표시 '저장소를 사용한' hello hello StorSimple Manager 서비스와 hello iSCSI 호스트에서 달라질 수 있습니다. |hello iSCSI 호스트에 hello 파일 시스템 보기가 있습니다.<br></br>hello 장치 hello 볼륨 hello 최대 크기로 때 할당 된 hello 블록을 볼 수 있습니다. |

