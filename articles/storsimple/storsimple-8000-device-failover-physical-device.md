---
title: "장애 조치 aaaStorSimple 재해 복구 tooa StorSimple 8000 시리즈 실제 장치 | Microsoft Docs"
description: "자세한 방법을 StorSimple 8000 시리즈 실제 장치 tooanother 물리적 장치를 통해 toofail 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/03/2017
ms.author: alkohli
ms.openlocfilehash: 29d2576a96c446ff5ffcd98dcd0f5a07f1ab08ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooa-storsimple-8000-series-physical-device"></a>장애 조치 tooa StorSimple 8000 시리즈 실제 장치

## <a name="overview"></a>개요

이 자습서에서는 재해가 경우 hello 단계 필요한 toofail StorSimple 8000 시리즈 실제 장치 tooanother StorSimple 물리적 장치를 통해 설명 합니다. StorSimple 물리적 장치를 tooanother hello 데이터 센터에서 원본 물리적 장치의 hello 장치 장애 조치 기능 toomigrate 데이터를 사용합니다. 이 자습서의 지침에 hello tooStorSimple 8000 시리즈 실제 실행 하는 장치 소프트웨어 버전 업데이트 3 이상 적용 됩니다.

장치 장애 조치 및 재해를 사용 하는 toorecover는 방법에 대해 자세히 toolearn 너무 이동[StorSimple 8000 시리즈 장치에 대 한 장애 조치 및 재해 복구](storsimple-8000-device-failover-disaster-recovery.md)합니다.

StorSimple 물리적 장치 tooa StorSimple 클라우드 어플라이언스를 통해 toofail 너무 이동[tooa StorSimple 클라우드 어플라이언스에 장애 조치할](storsimple-8000-device-failover-cloud-appliance.md)합니다. 물리적 장치 tooitself 통해 toofail 너무 이동[장애 조치 toohello 동일 StorSimple 물리적 장치용](storsimple-8000-device-failover-same-device.md)합니다.


## <a name="prerequisites"></a>필수 조건

- 장치 장애 조치에 대 한 hello 고려 사항 검토 했음을 확인 합니다. 자세한 내용은 이동 너무[장치 장애 조치에 대 한 일반적인 고려 사항](storsimple-8000-device-failover-disaster-recovery.md)합니다.

- Hello 데이터 센터에 배포 하는 StorSimple 8000 시리즈 실제 장치에 있어야 합니다. hello 장치 업데이트 3 또는 이후 소프트웨어 버전을 실행 해야 합니다. 자세한 내용은 이동 너무[온-프레미스 StorSimple 장치 배포](storsimple-8000-deployment-walkthrough-u2.md)합니다.


## <a name="steps-toofail-over-tooa-physical-device"></a>Tooa 물리적 장치를 통해 단계 toofail

다음 단계 toorestore hello 장치 tooa 대상 물리적 장치를 수행 합니다.

1. 통해 toofail 하려는 해당 hello 볼륨 컨테이너에 연결 된 클라우드 스냅숏이 확인 합니다. 자세한 내용은 이동 너무[StorSimple 장치 관리자를 사용 하 여 서비스 toocreate 백업은](storsimple-8000-manage-backup-policies-u2.md)합니다.
2. StorSimple 장치 관리자 tooyour 이동한 다음 클릭 **장치**합니다. Hello에 **장치** 블레이드, 서비스와 연결 된 장치 이동 toohello 목록입니다.
    ![장치 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)
3. 원본 장치를 선택하고 클릭합니다. hello 원본 장치를 통해 toofail 하려는 hello 볼륨 컨테이너에 있습니다. 너무 이동**설정 > 볼륨 컨테이너**합니다.
4. 싶다는 의사를 toofail tooanother 장치에 대 한 볼륨 컨테이너를 선택 합니다. 이 컨테이너 내의 볼륨 hello 볼륨 컨테이너 toodisplay hello 목록을 클릭 합니다. 볼륨, 마우스 클릭 선택 **오프 라인으로 전환** tootake hello 볼륨을 오프 합니다. Hello 볼륨 컨테이너에서 모든 hello 볼륨에 대해이 프로세스를 반복 합니다.
5. 이전 단계를 반복 hello toofail tooanother 장치를 통해 하려는 모든 볼륨 컨테이너를 hello에 대 한 합니다.
6. Toohello 돌아가서 **장치** 블레이드입니다. Hello 명령 모음에서 클릭 **장애 조치**합니다.
    ![장애 조치(failover) 클릭](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev2.png)
    
7. Hello에 **장애 조치** 블레이드에서 hello 다음 단계를 수행 합니다.
   
   1. **원본**을 클릭합니다. 볼륨에 연결 된 클라우드 스냅숏이 있는 볼륨 컨테이너 hello 표시 됩니다. 표시 된 hello 컨테이너에만 장애 조치에 대상이 됩니다. 볼륨 컨테이너의 hello 목록에서 원하는 toofail 통해 hello 볼륨 컨테이너를 선택 합니다. **연결 된 클라우드 스냅숏이 있는 볼륨 컨테이너를 hello만 하 고 오프 라인 볼륨이 표시 됩니다.**

       ![원본 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev5.png)
   2. **대상**을 클릭합니다. Hello 이전 단계에서 선택한 hello 볼륨 컨테이너에 대 한 사용 가능한 장치 hello 드롭 다운 목록에서 대상 장치를 선택 합니다. 충분 한 용량 tooaccommodate 원본 볼륨 컨테이너에 있는 hello 장치만 hello 목록에 표시 됩니다.

        ![대상 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev6.png)

   3. 마지막으로 아래에서 모든 hello 장애 조치 설정을 검토 **요약**합니다. Hello 설정을 검토 한 후에 hello 확인란을 선택한 볼륨 컨테이너에서 hello 볼륨이 오프 라인 인지 나타내는 선택 합니다. **확인**을 클릭합니다.

       ![장애 조치(failover) 설정 검토](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev8.png)
  
8. StorSimple은 장애 조치 작업을 만듭니다. Hello 알림 toomonitor hello 장애 조치 작업을 통해 hello 클릭 **작업** 블레이드입니다.

    그런 다음 장애 조치 hello 볼륨 컨테이너에 볼륨이 로컬 각 로컬 볼륨 (하지 계층화 된 볼륨) hello 컨테이너에에 대 한 개별 복원 작업이 표시 됩니다. 이러한 복원 작업 시간 toocomplete 다소 걸릴 수 있습니다. 되었을 hello 장애 조치 작업 이전에 완료 될 수 있습니다. Hello 복원 작업이 완료 된 후에 이러한 볼륨에서 로컬 보장 해야 합니다.

    ![장애 조치(failover) 작업 모니터링](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

9. Hello 장애 조치가 완료 된 후 이동 toohello **장치** 블레이드입니다.
   
   1. Hello 장애 조치 프로세스에 대 한 hello 대상 장치로 사용 했던 hello 장치를 선택 합니다.

       ![장치 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

   2. Toohello 이동 **볼륨 컨테이너** 블레이드입니다. Hello hello 이전 장치의 볼륨과 함께 모든 hello 볼륨 컨테이너를 나열 합니다.

       ![대상 볼륨 컨테이너 보기](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev16.png)


## <a name="next-steps"></a>다음 단계

* 장애 조치를 수행한 후 해야 너무[비활성화 또는 삭제 StorSimple 장치](storsimple-8000-deactivate-and-delete-device.md)합니다.
* Toouse StorSimple 장치 관리자 hello 하는 방법에 대 한 정보에 대 한 서비스, 너무 이동[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-8000-manager-service-administration.md)합니다.

