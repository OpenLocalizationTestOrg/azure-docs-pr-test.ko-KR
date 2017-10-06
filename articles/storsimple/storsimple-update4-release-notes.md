---
title: "aaaStorSimple 8000 시리즈 업데이트 4 릴리스 정보 | Microsoft Docs"
description: "StorSimple 8000 시리즈 업데이트 4에 대 한 hello 새로운 기능, 문제 및 해결 방법에 설명 합니다."
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
ms.date: 04/04/2017
ms.author: alkohli
ms.openlocfilehash: 4bca8ca222e6706fd6eaf56b702b0d34b6ffd1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-4-release-notes"></a>StorSimple 8000 시리즈 업데이트 4 릴리스 정보

## <a name="overview"></a>개요

hello 다음 릴리스 정보 hello 새로운 기능에 설명 하 고 StorSimple 8000 시리즈 업데이트 4에 대 한 hello 중요 한 미해결 문제를 식별 합니다. 또한이 릴리스에 포함 된 hello StorSimple 소프트웨어 업데이트의 목록을 포함 합니다. 

업데이트 4에는 적용 된 tooany StorSimple 장치 업데이트 3.1 통해 릴리스 (GA) 또는 업데이트 0.1 실행 수 있습니다. 업데이트 4와 관련 된 hello 장치 버전 6.3.9600.17820입니다.

Hello 릴리스 노트 hello를 배포 하기 전에 StorSimple 솔루션의 업데이트에 포함 된 hello 정보를 검토 하십시오.

> [!IMPORTANT]
> * 업데이트 4는 장치 소프트웨어, USM 펌웨어, LSI 드라이버 및 펌웨어, 디스크 펌웨어, Storport 및 Spaceport, 보안 및 기타 OS 업데이트를 포함합니다. 이 업데이트 약 4 시간 tooinstall이 필요합니다. 디스크 펌웨어 업데이트는 중단 업데이트이며 사용자 장치에 대한 가동 중지 시간이 발생합니다. 적용 하는 업데이트 4 tookeep 장치를 최신 상태로 유지 하는 것이 좋습니다. 
> * 새 릴리스를 위한 나타나지 않을 수 있습니다 업데이트 hello 업데이트의 단계별된 공개를 수행 하는 것 때문에 즉시 합니다. 업데이트가 곧 제공될 예정이니 몇 일 후에 업데이트를 다시 검색하세요.

## <a name="whats-new-in-update-4"></a>업데이트 4의 새로운 기능

hello 다음 주요 개선 사항 및 버그 수정 내용이 업데이트 4에서.

* **더 효율적인 자동 공간 확보 알고리즘** – 업데이트 4에서는 hello 자동화 된 공간 확보는 알고리즘은 향상 된 tooadjust hello 공간 확보 hello 필요에 따라 주기 hello 클라우드에서 사용 가능한 공간을 회수 합니다. 

* **로컬 고정된 볼륨에 대 한 성능 향상** – 업데이트 4 높은 데이터 수집 (데이터 크기를 비교할 toovolume 크기)이 있는 시나리오에서 로컬로 고정 된 볼륨의 hello 성능이 향상 되었습니다.

* **Heatmap 기반 복원** -hello 이전 버전에서는 재해 복구 (DR) hello 데이터 다음 느린 성능이 hello 액세스 패턴에 따라 hello 클라우드에서 복원 합니다. 

    트랙 hello 장치가 사용 하 여 이전 tooDR에 있을 때 자주 데이터 toocreate는 heatmap를 액세스 하는 새로운 기능이 업데이트 4에서 구현 됩니다 (가장 사용된 된 데이터 청크는 높은 열 작은 청크를 사용 하는 반면가 낮은 열)입니다. DR 후 StorSimple 사용 하 여 hello heatmap tooautomatically 복원 하 고 hello 클라우드에서 hello 데이터 리하이드레이션 합니다. 

    모든 hello 복원은 heatmap 기반 복원 됩니다. 너무 tooquery 및 취소 heatmap 복원 및 리하이드레이션 작업 기반 하는 방법에 자세한 내용을 보려면 이동[용 Windows PowerShell StorSimple cmdlet 참조](https://technet.microsoft.com/library/dn688168.aspx)합니다.

* **StorSimple 진단 도구** – 업데이트 4에서 도구 되 고 StorSimple 진단 쉽게 진단 하는 데 tooallow 릴리스되며 toosystem, 네트워크, 성능 및 하드웨어 구성 요소 상태 관련 문제를 해결 합니다. 이 도구는 StorSimple 용 Windows PowerShell hello를 통해 실행 됩니다. 자세한 내용은 이동 너무[StorSimple 진단 도구를 사용 하 여 문제를 해결](storsimple-8000-diagnostics.md)합니다.

* **StorSimple 마이그레이션 도구 UI 기반** -이전 toothis 릴리스, 5000 7000 시리즈에서 데이터를 마이그레이션하는 데 필요한 hello 사용자 tooexecute hello Azure PowerShell 인터페이스를 사용 하 여 hello 마이그레이션 워크플로의 일부입니다. 이 릴리스에서 사용 하기 쉬운-StorSimple 마이그레이션 UI 기반 도구 데 사용할 수 있는 지원 toofacilitate 동일한 마이그레이션 워크플로 hello 합니다. 이 도구는 복구 버킷 hello 통합을 위한 할 수도 있습니다. 

* **FIPS 관련 변경 사항이** -이 이후 릴리스, Azure 공용 클라우드 계정과 Microsoft Azure Government hello 둘 다에 대 한 FIPS 모든 hello StorSimple 8000 시리즈 장치에는 기본적으로 사용 됩니다.

* **변경 사항을 업데이트** -이 릴리스의 버그 관련된 tooupdate 오류가 수정 되었습니다.

* **디스크 오류에 대 한 경고** -새로운 경고가 발생할 수 있는 디스크 실패의 hello 사용자에 게 경고 하는이 릴리스에서 추가 됩니다. 이 경고를 발생 하는 경우 Microsoft 지원 tooship 대체 디스크를 문의 합니다. 자세한 내용은 이동 너무[StorSimple 장치에서 하드웨어 경고](storsimple-manage-alerts.md#hardware-alerts)합니다.

* **컨트롤러 교체 변경** -hello 사용자 tooquery hello hello 컨트롤러 교체 프로세스의 상태를 허용 하는 cmdlet이 릴리스에서 추가 됩니다. 자세한 내용은 toohello 이동 [cmdlet tooquery 컨트롤러 교체 상태](https://technet.microsoft.com/library/dn688168.aspx)합니다.


## <a name="issues-fixed-in-update-4"></a>업데이트 4에서 해결된 문제

hello 다음 표에서 업데이트 4에서 해결 된 문제에 대 한 요약 합니다.    

| 아니요 | 기능 | 문제 | Toophysical 장치를 적용 됩니다. | Toovirtual 장치를 적용 됩니다. |
| --- | --- | --- | --- | --- |
| 1 |장애 조치(failover) |Hello에 hello 장애 조치 발생 후의 이전 릴리스를 관련 된 문제가 toocleanup hello 고객 사이트에서 관찰 합니다. 이 문제는 이 릴리스에서 해결되었습니다. |예 |예 |
| 2 |로컬로 고정된 볼륨 |Hello 이전 릴리스에서 볼륨 만들기 실패 발생 하는 로컬 고정된 볼륨에 대 한 문제 toorelated 볼륨 작성이 했습니다. 이 문제는 근본 원인이 파악되었고 이 릴리스에서 수정되었습니다. |예 |아니요 |
| 3 |지원 패키지 |이전 릴리스에서 System.OutOfMemory 예외 또는 지원 패키지 만들기 오류에서 발생 한 다른 오류가 발생 하는 문제 관련된 tooSupport 패키지가 있었습니다. 이러한 버그는 이 릴리스에서 해결되었습니다. |예 |예 |
| 4 |모니터링 |이전 릴리스에서 있습니다 문제 관련 toomonitoring 차트 로컬 고정된 볼륨에 대 한 소비 EB에 표시 된 위치입니다. 이 버그는 이 릴리스에서 해결되었습니다. |예 |예 |
| 5 |마이그레이션 |이전 릴리스에서 마이그레이션 5000 7000 시리즈 too8000 시리즈 장치에서의 몇 가지 문제 관련된 toohello 안정성이 있었습니다. 이러한 문제는 이 릴리스에서 해결되었습니다. |예 |예 |
| 6 |업데이트 |이전 릴리스에서 업데이트에 실패 했습니다., hello 컨트롤러는 복구 모드로 전환 하 고 따라서 hello 사용자 hello 업데이트를 계속할 수 없습니다 toocontact Microsoft 지원에 필요 합니다. <br> 이번 릴리스에서는 이 동작이 바뀌었습니다. Hello 사용자에 게 두 hello 컨트롤러 후 업데이트에 실패 하는 경우 실행 hello 같은 버전 (업데이트 4) hello 컨트롤러가 복구 모드로 전환 되지 않습니다. 이 오류를 발생 하는 hello 사용자는 이러한 비트를 기다린 후 다시 시도 hello 업데이트 하는 것이 좋습니다. hello 재시도 성공할 수 있습니다. Hello 다시 시도 실패 하면 Microsoft 지원에 문의 해야 합니다. |예 |예 |


## <a name="known-issues-in-update-4-from-previous-releases"></a>이전 릴리스에서 업데이트 4의 알려진 문제

업데이트 4에 알려진 새로운 문제가 없습니다. 목록이 tooUpdate 4 이전 버전에서 전달 하는 문제에 대 한 이동 너무[업데이트 3 릴리스 정보](storsimple-update3-release-notes.md#known-issues-in-update-3)합니다.

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-update-4"></a>업데이트 4의 SAS(Serial attached SCSI) 컨트롤러 및 펌웨어 업데이트

이 릴리스에는 SAS 컨트롤러, LSI 드라이버 및 펌웨어 업데이트가 있습니다. Tooinstall 이러한 업데이트를 확인 하려면 어떻게 대 한 자세한 내용은 [업데이트 4를 설치](storsimple-install-update-4.md) StorSimple 장치에 있습니다.

## <a name="virtual-device-updates-in-update-4"></a>업데이트 4의 가상 장치 업데이트

이 업데이트는 적용 된 toohello StorSimple 클라우드 어플라이언스에 (라고도 hello 가상 장치) 일 수 없습니다. 새 가상 장치 생성 toobe가 필요 합니다. 

## <a name="next-step"></a>다음 단계

너무 방법에 대해 알아봅니다[업데이트 4를 설치](storsimple-install-update-4.md) StorSimple 장치에 있습니다.

