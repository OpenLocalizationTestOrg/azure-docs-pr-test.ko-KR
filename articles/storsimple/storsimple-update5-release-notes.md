---
title: "aaaStorSimple 8000 시리즈 업데이트 5 릴리스 정보 | Microsoft Docs"
description: "StorSimple 8000 시리즈 업데이트 5에 대 한 hello 새로운 기능, 문제 및 해결 방법에 설명 합니다."
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
ms.date: 08/23/2017
ms.author: alkohli
ms.openlocfilehash: 9eb8ffb97b41ce3d4f1ffdf2975f904d0a2958e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-5-release-notes"></a>StorSimple 8000 시리즈 업데이트 5 릴리스 정보

## <a name="overview"></a>개요

hello 다음 릴리스 정보 hello 새로운 기능에 설명 하 고 StorSimple 8000 시리즈 업데이트 5에 대 한 hello 중요 한 미해결 문제를 식별 합니다. 또한이 릴리스에 포함 된 hello StorSimple 소프트웨어 업데이트의 목록을 포함 합니다.

업데이트 5에는 업데이트 4를 통해 업데이트 0.1을 실행 하는 적용 된 tooany StorSimple 장치 수 있습니다. 업데이트 5와 관련 된 hello 장치 버전 6.3.9600.17845입니다.

Hello 릴리스 노트 hello를 배포 하기 전에 StorSimple 솔루션의 업데이트에 포함 된 hello 정보를 검토 합니다.

> [!IMPORTANT]
> * 업데이트 5에는 장치 소프트웨어, 디스크 펌웨어, OS 보안 및 기타 OS 업데이트가 있습니다. 이 업데이트 약 4 시간 tooinstall이 필요합니다. 디스크 펌웨어 업데이트는 중단 업데이트이며 사용자 장치에 대한 가동 중지 시간이 발생합니다. 적용 하는 업데이트 5 tookeep 장치를 최신 상태로 유지 하는 것이 좋습니다.
> * 새 릴리스를 위한 나타나지 않을 수 있습니다 업데이트 hello 업데이트의 단계별된 공개를 수행 하는 것 때문에 즉시 합니다. 이러한 업데이트가 곧 제공될 예정이니 몇 일 후에 업데이트를 다시 검색하세요.

## <a name="whats-new-in-update-5"></a>업데이트 5의 새로운 기능

hello 다음 주요 개선 사항 및 버그 수정에에서 대 업데이트 5입니다.

* **StorSimple 장치 관리자 서비스와 Azure Active Directory (AAD) tooauthenticate 사용** –에서 업데이트 5부터 Azure Active Directory는 hello StorSimple 장치 관리자 서비스와 함께 사용 되는 tooauthenticate 합니다. hello 이전 인증 메커니즘 2017 년 12 월에 지원이 중지 됩니다. 모든 hello 사용자가 해당 방화벽 규칙에 hello 새 인증 Url을 포함 해야 합니다. 자세한 내용은 이동 너무[네트워킹 StorSimple 장치에 대 한 요구 사항이 hello에 나열 된 인증 Url](storsimple-8000-system-requirements.md#url-patterns-for-azure-portal)합니다.

    Hello 인증 URL hello 방화벽 규칙에 포함 되지 않은, hello 사용자가 자신의 StorSimple 장치 hello 서비스를 인증할 수 없음을 중요 한 알림이 표시 됩니다. Hello 사용자가이 경고를 볼 경우 tooinclude hello 새 인증 URL 해야 합니다. 자세한 내용은 이동 너무[경고 네트워킹 StorSimple](storsimple-8000-manage-alerts.md#networking-alerts)합니다.

* **새 버전의 StorSimple Snapshot Manager** - 새 버전의 StorSimple Snapshot Manager가 업데이트 5와 함께 출시됩니다. Toothis 버전을 업데이트 하는 것이 좋습니다. 이 버전은 업데이트 3을 실행 하는 모든 hello StorSimple 장치에 호환 이상입니다. 자세한 내용은 이동 너무[StorSimple 스냅숏 관리자 배포](storsimple-snapshot-manager-deployment.md)합니다.


## <a name="issues-fixed-in-update-5"></a>업데이트 5에서 해결된 문제

hello 다음 표에서 업데이트 5에서 해결 된 문제에 대 한 요약 합니다.

| 아니요 | 기능 | 문제 | Toophysical 장치를 적용 됩니다. | Toovirtual 장치를 적용 됩니다. |
| --- | --- | --- | --- | --- |
| 1 |Windows PowerShell 원격 기능 |Hello 이전 릴리스에서 사용자가 원격 연결 toohello Windows PowerShell을 통해 StorSimple 클라우드 어플라이언스에 tooestablish 하는 동안 오류가 발생을 받게 됩니다. 이 문제는 근본 원인이 파악되었고 이 릴리스에서 수정되었습니다. |아니요 |예 |
| 2 |대역폭 템플릿 |이전 릴리스에서 hello 장치에 대해 구성 된 보다 낮은 대역폭에서 발생 하는 대역폭 템플릿은 문제가 발생 했습니다. 이 문제는 이 릴리스에서 해결되었습니다. |예 |예 |
| 3 |장애 조치(failover) |이전 릴리스에서 업데이트 4를 실행 하는 tooanother 장치를 통해 여러 볼륨을 사용 하 여 장치를 실패 한 경우 hello 프로세스가 못합니다 tooapply hello 액세스 제어 레코드를 시도할 때. 이 문제는 이 릴리스에서 해결되었습니다. |예 |예 |



## <a name="known-issues-in-update-5-from-previous-releases"></a>업데이트 5의 알려진 이전 릴리스 문제

업데이트 5에 알려진 새로운 문제는 없습니다. 목록이 tooUpdate 5에서 이전 버전으로 이전 하는 문제에 대 한 이동 너무[업데이트 3 릴리스 정보](storsimple-update3-release-notes.md#known-issues-in-update-3)합니다.

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-update-5"></a>업데이트 5의 SAS(Serial attached SCSI) 컨트롤러 및 펌웨어 업데이트

이 릴리스에는 SAS 컨트롤러, LSI 드라이버 및 펌웨어 업데이트가 있습니다. Tooinstall 이러한 업데이트를 확인 하려면 어떻게 대 한 자세한 내용은 [업데이트 5 설치](storsimple-8000-install-update-5.md) StorSimple 장치에 있습니다.

## <a name="storsimple-cloud-appliance-updates-in-update-5"></a>업데이트 5의 StorSimple Cloud Appliance 업데이트

이 업데이트는 적용 된 toohello StorSimple 클라우드 어플라이언스에 (라고도 hello 가상 장치) 일 수 없습니다. 새 클라우드 어플라이언스에 hello 업데이트 5 이미지를 사용 하 여 만든 toobe가 필요 합니다. 방법에 대 한 StorSimple 클라우드 어플라이언스에 toocreate 너무 이동[배포 하 고 StorSimple 클라우드 어플라이언스에 관리](storsimple-8000-cloud-appliance-u2.md)합니다.

## <a name="next-step"></a>다음 단계

너무 방법에 대해 알아봅니다[업데이트 5 설치](storsimple-8000-install-update-5.md) StorSimple 장치에 있습니다.

