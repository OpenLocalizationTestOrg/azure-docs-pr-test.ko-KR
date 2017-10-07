---
title: "장애 조치 aaaStorSimple 재해 복구 tooa StorSimple 클라우드 어플라이언스에 | Microsoft Docs"
description: "어떻게 하면 StorSimple 8000 시리즈 실제 장치 tooa 통해 toofail 클라우드 어플라이언스에 알아봅니다."
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: e8a0bca057024358e3a557fe85a42ddefea36cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooyour-storsimple-cloud-appliance"></a>장애 조치 tooyour 클라우드 StorSimple 어플라이언스

## <a name="overview"></a>개요

이 자습서에서는 재해가 경우 hello 단계 필요한 toofail StorSimple 8000 시리즈 실제 장치 tooa StorSimple 클라우드 어플라이언스를 통해 설명 합니다. StorSimple에서 hello 데이터 센터 tooa 클라우드 어플라이언스에 Azure에서 실행 되는 원본 물리적 장치에서 hello 장치 장애 조치 기능 toomigrate 데이터를 사용 합니다. 이 자습서의 지침에 hello tooStorSimple 8000 시리즈 실제 장치 및 3 이상 소프트웨어 업데이트 버전을 실행 하는 클라우드 어플라이언스에 적용 합니다.

장치 장애 조치 및 재해를 사용 하는 toorecover는 방법에 대해 자세히 toolearn 너무 이동[StorSimple 8000 시리즈 장치에 대 한 장애 조치 및 재해 복구](storsimple-8000-device-failover-disaster-recovery.md)합니다.

StorSimple 물리적 장치 tooanother 물리적 장치를 통해 toofail 너무 이동[tooa StorSimple 물리적 장치용 장애 조치할](storsimple-8000-device-failover-physical-device.md)합니다. 장치 tooitself 통해 toofail 너무 이동[장애 조치 toohello 동일 StorSimple 물리적 장치용](storsimple-8000-device-failover-same-device.md)합니다.

## <a name="prerequisites"></a>필수 조건

- 장치 장애 조치에 대 한 hello 고려 사항 검토 했음을 확인 합니다. 자세한 내용은 이동 너무[장치 장애 조치에 대 한 일반적인 고려 사항](storsimple-8000-device-failover-disaster-recovery.md)합니다.

- 이 절차를 수행하기에 앞서 StorSimple Cloud Appliance를 먼저 만들고 구성해야 합니다. 실행 중인 소프트웨어 버전 3을 업데이트 하거나 나중에 대 한 8020 클라우드 어플라이언스에 사용 하는 것이 좋습니다 hello DR. hello 8020 모델 64TB 개이고 프리미엄 저장소를 사용 합니다. 자세한 내용은 이동 너무[배포 및 StorSimple 클라우드 어플라이언스에 관리](storsimple-8000-cloud-appliance-u2.md)합니다.

## <a name="steps-toofail-over-tooa-cloud-appliance"></a>Tooa 클라우드 어플라이언스를 통해 단계 toofail

Hello 단계 toorestore hello 장치 tooa 대상 StorSimple 클라우드 어플라이언스에 다음을 수행 합니다.

1.  통해 toofail 하려는 해당 hello 볼륨 컨테이너에 연결 된 클라우드 스냅숏이 확인 합니다. 자세한 내용은 이동 너무[StorSimple 장치 관리자를 사용 하 여 서비스 toocreate 백업은](storsimple-8000-manage-backup-policies-u2.md)합니다.
2. Tooyour StorSimple 장치 관리자 서비스를 이동 하 고 클릭 **장치**합니다. Hello에 **장치** 블레이드, 서비스와 연결 된 장치 이동 toohello 목록입니다.
    ![장치 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)
3. 원본 장치를 선택하고 클릭합니다. hello 원본 장치를 통해 toofail 하려는 hello 볼륨 컨테이너에 있습니다. 너무 이동**설정 > 볼륨 컨테이너**합니다.

    ![장치 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. 싶다는 의사를 toofail tooanother 장치에 대 한 볼륨 컨테이너를 선택 합니다. 이 컨테이너 내의 볼륨 hello 볼륨 컨테이너 toodisplay hello 목록을 클릭 합니다. 볼륨, 마우스 클릭 선택 **오프 라인으로 전환** tootake hello 볼륨을 오프 합니다.

    ![장치 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. Hello 볼륨 컨테이너에서 모든 hello 볼륨에 대해이 프로세스를 반복 합니다.

     ![장치 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. 이전 단계를 반복 hello toofail tooanother 장치를 통해 하려는 모든 볼륨 컨테이너를 hello에 대 한 합니다.

7. Toohello 돌아가서 **장치** 블레이드입니다. Hello 명령 모음에서 클릭 **장애 조치**합니다.

    ![장애 조치(failover) 클릭](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. Hello에 **장애 조치** 블레이드에서 hello 다음 단계를 수행 합니다.
   
    1. **원본**을 클릭합니다. 통해 볼륨 컨테이너 toofail hello를 선택 합니다. **연결 된 클라우드 스냅숏이 있는 볼륨 컨테이너를 hello만 하 고 오프 라인 볼륨이 표시 됩니다.**
        ![원본 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)
    2. **대상**을 클릭합니다. 대상 클라우드 어플라이언스에 hello 사용 가능한 장치 드롭다운 목록에서 선택 합니다. **충분 한 용량 tooaccommodate 원본 볼륨 컨테이너에 있는 hello 장치만 hello 목록에 표시 됩니다.**

        ![대상 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. 장애 조치 설정을 hello 검토 **요약** hello 확인란을 선택한 볼륨 컨테이너에서 hello 볼륨이 오프 라인 인지 나타내는 선택 합니다. 

        ![장애 조치(failover) 설정 검토](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. 장애 조치(failover) 작업이 만들어집니다. toomonitor hello 장애 조치 작업를 작업 알림 hello를 클릭 합니다.

    ![장애 조치(failover) 작업 모니터링](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. Hello 장애 조치가 완료 되 면 toohello 돌아가서 **장치** 블레이드입니다.

    1. Hello 장애 조치에 대 한 hello 대상으로 사용 된 hello 장치를 선택 합니다.

       ![장치 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. **볼륨 컨테이너**를 클릭합니다. Hello hello 이전 장치의 볼륨과 함께 모든 hello 볼륨 컨테이너를 나열 합니다.

       장애 조치 hello 볼륨 컨테이너에 볼륨 고정 된 로컬로 하는 경우 이러한 볼륨은 장애 조치 계층화 된 볼륨으로. StorSimple Cloud Appliance에서는 로컬로 고정된 볼륨이 지원되지 않습니다.

       ![대상 볼륨 컨테이너 보기](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a>다음 단계

* 장애 조치를 수행한 후 해야 너무[비활성화 또는 삭제 StorSimple 장치](storsimple-8000-deactivate-and-delete-device.md)합니다.

* Toouse StorSimple 장치 관리자 hello 하는 방법에 대 한 정보에 대 한 서비스, 너무 이동[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-8000-manager-service-administration.md)합니다.

