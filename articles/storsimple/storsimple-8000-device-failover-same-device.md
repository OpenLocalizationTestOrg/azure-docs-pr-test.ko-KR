---
title: "장애 조치 aaaStorSimple 8000 시리즈 장치에 대 한 재해 복구 | Microsoft Docs"
description: "자세한 방법을 통해 StorSimple 장치 toohello toofail 동일한 장치입니다."
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
ms.date: 06/23/2017
ms.author: alkohli
ms.openlocfilehash: b0b4216c7af6745ff68b85ca3d655691b43b4334
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-your-storsimple-physical-device-toosame-device"></a>장애 조치 StorSimple 물리적 장치 toosame 장치

## <a name="overview"></a>개요

이 자습서에서는 재해가 경우 StorSimple 8000 시리즈 실제 장치 tooitself 통해 hello 단계 필요한 toofail을 설명 합니다. StorSimple 물리적 장치를 tooanother hello 데이터 센터에서 원본 물리적 장치의 hello 장치 장애 조치 기능 toomigrate 데이터를 사용합니다. 이 자습서의 지침에 hello tooStorSimple 8000 시리즈 실제 실행 하는 장치 소프트웨어 버전 업데이트 3 이상 적용 됩니다.

장치 장애 조치 및 재해를 사용 하는 toorecover는 방법에 대해 자세히 toolearn 너무 이동[StorSimple 8000 시리즈 장치에 대 한 장애 조치 및 재해 복구](storsimple-8000-device-failover-disaster-recovery.md)합니다.

물리적 장치 tooanother 물리적 장치를 통해 toofail 너무 이동[장애 조치 toohello 동일 StorSimple 물리적 장치용](storsimple-8000-device-failover-physical-device.md)합니다. StorSimple 물리적 장치 tooa StorSimple 클라우드 어플라이언스를 통해 toofail 너무 이동[tooa StorSimple 클라우드 어플라이언스에 장애 조치할](storsimple-8000-device-failover-cloud-appliance.md)합니다.


## <a name="prerequisites"></a>필수 조건

- 장치 장애 조치에 대 한 hello 고려 사항 검토 했음을 확인 합니다. 자세한 내용은 이동 너무[장치 장애 조치에 대 한 일반적인 고려 사항](storsimple-8000-device-failover-disaster-recovery.md)합니다.


## <a name="steps-toofail-over-toohello-same-device"></a>단계 toofail toohello 통해 동일한 장치

Hello toofail toohello 조치 해야 할 경우 다음 단계를 수행 합니다. 동일한 장치입니다.

1. 클라우드 스냅숏을 모든 hello 볼륨의 장치에서 만듭니다. 자세한 내용은 이동 너무[StorSimple 장치 관리자를 사용 하 여 서비스 toocreate 백업은](storsimple-8000-manage-backup-policies-u2.md)합니다.
2. 장치 toofactory 기본값 다시 설정 합니다. 에 따라 hello에 필요한 세부 정보 [tooreset StorSimple 장치 toofactory 기본 설정 방법을](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings)합니다.
3. Toohello StorSimple 장치 관리자 서비스를 이동 하 고 다음 선택 **장치**합니다. Hello에 **장치** 블레이드에서 hello 이전 장치도 표시 되어야 **오프 라인**합니다.

    ![오프라인 상태의 원본 장치](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. 장치를 구성하고 StorSimple 장치 관리자 서비스에 다시 등록합니다. hello 새로 등록 된 장치도 표시 되어야 **를 tooset 준비**합니다. hello 새 장치에 대 한 hello 장치 이름을 hello toofactory 기본 설정인 다시 설정 하 고 다시 등록 hello 이전 장치 하지만 추가 된 숫자 tooindicate hello 장치와 동일 합니다.

    ![새로 등록 된 장치를 준비 tooset](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. Hello 새 장치에 대 한 hello 장치 설치를 완료 합니다. 자세한 내용은 이동 너무[4 단계: 최소 장치 설정 완료](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup)합니다. Hello에 **장치** 블레이드에서 hello 장치의 hello 상태 변경 너무**온라인**합니다.

   > [!IMPORTANT]
   > **Hello 최소 구성을 먼저 완료 또는 DR 실패할 수 있습니다.**

    ![온라인 상태의 새로 등록된 장치](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. Hello 오래 된 장치 (오프 라인 상태)를 선택 하 고 hello 명령 모음에서 클릭 **장애 조치**합니다. Hello에 **장애 조치** 블레이드에서 hello 소스로 오래 된 장치를 선택 하 고 hello 장치를 새로 등록 된 hello 대상 장치를 지정 합니다.

    ![장애 조치(failover) 요약](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    자세한 내용은 참조 너무[tooanother 물리적 장치를 장애 조치할](#fail-over-to-another-physical-device)합니다.

7. Hello에서 모니터링할 수 있는 장치 복원 작업이 만들어집니다 **작업** 블레이드입니다.

8. Hello 작업이 성공적으로 완료 되 면 hello 새 장치를 액세스 하 고 toohello 탐색 **볼륨 컨테이너** 블레이드입니다. Hello 오래 된 장치에서 모든 hello 볼륨 컨테이너 toohello 새 장치를 마이그레이션 되었는지 확인 합니다.

   ![마이그레이션된 볼륨 컨테이너](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. Hello 장애 조치가 완료 되 면 비활성화 하 고 hello 포털에서 hello 오래 된 장치를 삭제할 수 있습니다. Hello 오래 된 장치 (오프 라인) 마우스 오른쪽 단추를 선택한 다음 선택 **비활성화**합니다. Hello 장치를 비활성화 한 후 hello 장치의 hello 상태가 업데이트 됩니다.

     ![비활성화된 원본 장치](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. 장치, 마우스 오른쪽 단추로 클릭 한 다음 선택 select hello 비활성화 **삭제**합니다. 그러면 hello 장치 hello 장치 목록에서 삭제 됩니다.

    ![삭제된 원본 장치](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a>다음 단계

* 장애 조치를 수행한 후 해야 너무[비활성화 또는 삭제 StorSimple 장치](storsimple-8000-deactivate-and-delete-device.md)합니다.
* Toouse StorSimple 장치 관리자 hello 하는 방법에 대 한 정보에 대 한 서비스, 너무 이동[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-8000-manager-service-administration.md)합니다.

