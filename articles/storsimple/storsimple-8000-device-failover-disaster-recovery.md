---
title: "장애 조치 aaaStorSimple 8000 시리즈 장치에 대 한 재해 복구 | Microsoft Docs"
description: "자세한 방법을 통해 StorSimple 장치 tooitself, 다른 물리적 장치 또는 클라우드 어플라이언스에 toofail 합니다."
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
ms.openlocfilehash: 9d01ee30b15b77072b1d4dfe9a215abc83ffba28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="failover-and-disaster-recovery-for-your-storsimple-8000-series-device"></a>StorSimple 8000 시리즈 장치에 대한 장애 조치 및 재해 복구

## <a name="overview"></a>개요

이 문서에서는 hello StorSimple 8000 시리즈 장치에 대 한 hello 장치 장애 조치 기능 및이 기능은 수 있는 방법을 사용 하는 toorecover StorSimple 장치 재해가 발생 한 경우를 설명 합니다. StorSimple는 hello 데이터 센터 tooanother 대상 장치에서 원본 장치의 장치 장애 조치 toomigrate hello 데이터를 사용합니다. 이 문서에 대 한 hello 지침 tooStorSimple 8000 시리즈 실제 장치 및 3 이상 소프트웨어 업데이트 버전을 실행 하는 클라우드 어플라이언스에 적용 합니다.

StorSimple hello를 사용 하 여 **장치** 재해의 hello 이벤트에서 블레이드 toostart hello 장치 장애 조치 기능입니다. 이 블레이드는 모든 hello StorSimple 장치 연결 된 tooyour StorSimple 장치 관리자 서비스를 나열합니다.

![장치 블레이드](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)


## <a name="disaster-recovery-dr-and-device-failover"></a>DR(재해 복구) 및 장치 장애 조치

장애 복구 (DR) 시나리오에서 기본 장치 hello 작동이 중지 되었습니다. StorSimple hello 기본 장치를 사용 하 여 _소스_ hello 연결 된 클라우드 데이터 tooanother 이동 _대상_ 장치입니다. 이 프로세스는 참조 된 tooas hello *장애 조치*합니다. 다음 그래픽 hello hello 장애 조치 과정을 보여 줍니다.

![장치 장애 조치는 어떻게 되나요?](./media/storsimple-8000-device-failover-disaster-recovery/failover-dr-flow.png)

물리적 장치 또는 클라우드 어플라이언스에 hello 대상 장치 장애 조치를 수행할 수 있습니다. hello 대상 장치에 못할 같거나 hello 소스 장치와 다른 지리적 위치 hello에 있습니다.

Hello 장애 조치 중에 마이그레이션에 사용할 볼륨 컨테이너를 선택할 수 있습니다. 그런 다음 StorSimple hello 소스 장치 toohello 대상 장치에서 이러한 볼륨 컨테이너의 hello 소유권을 변경합니다. Hello 볼륨 컨테이너 소유권을 변경 되 면 StorSimple hello 소스 장치에서 이러한 컨테이너를 삭제 합니다. Hello 삭제가 완료 되 면 후 뒤로 hello 대상 장치를 실패할 수 있습니다. _장애 복구_ 전송 hello 소유권 백 toohello 원래의 원본 장치입니다.

### <a name="cloud-snapshot-used-during-device-failover"></a>장치 장애 조치 동안 사용된 클라우드 스냅숏

DR 다음 hello 최신 클라우드 백업 장치가 사용 되는 toorestore hello 데이터 toohello 대상입니다. 클라우드 스냅숏에 대 한 자세한 내용은 참조 하십시오. [hello StorSimple 장치 관리자 서비스 tootake 수동 백업을 사용 하 여](storsimple-8000-manage-backup-policies-u2.md#take-a-manual-backup)합니다.

StorSimple 8000 시리즈에서 백업 정책을 백업에 연결합니다. 여러 백업 정책이 있으면 hello 동일한 볼륨을 다음 선택 합니다. StorSimple hello 백업 볼륨의 최대 hello 정책에 대 한 합니다. StorSimple는 hello 대상 장치에서 선택한 hello 백업 정책 toorestore hello 데이터에서 가장 최근의 백업 hello를 사용합니다.

*defaultPol* 및 *customPol*이라는 두 개의 백업 정책이 있는 경우를 가정합니다.

* *defaultPol*: 하나의 볼륨(*vol1*)이 매일 오후 10시 30분부터 실행됩니다.
* *customPol*: 4개의 볼륨(*vol1*, *vol2*, *vol3*, *vol4*)이 매일 오후 10시부터 실행됩니다.

이 경우에 StorSimple에서는 더 많은 볼륨을 포함하는 크래시 일관성에 대한 우선 순위를 지정하고 *customPol*을 사용합니다. 이 정책에서 가장 최근의 백업을 hello toorestore 사용 되는 데이터입니다. 방법에 대 한 자세한 내용은 toocreate 및 백업 정책 관리, 너무 이동[hello StorSimple 장치 관리자 서비스 toomanage 백업 정책을 사용 하 여](storsimple-8000-manage-backup-policies-u2.md)합니다.

## <a name="common-considerations-for-device-failover"></a>장치 장애 조치에 대한 일반 고려 사항

장치를 통해 실패 전에 hello 다음 정보를 검토 하세요.

* 장치 장애 조치를 시작 하기 전에 hello 볼륨 컨테이너 내의 모든 hello 볼륨 오프 라인 이어야 합니다. 계획되지 않은 장애 조치에서 StotSimple 볼륨은 자동으로 오프라인 상태가 됩니다. 하지만 모든 hello 볼륨을 오프 라인으로 수행 해야 계획된 된 장애 조치 (tootest DR)를 수행 하는 경우.
* 만 연결 되어 있는 볼륨 컨테이너를 hello DR에 대 한 클라우드 스냅숏을 나열 됩니다. 연결 된 클라우드 스냅숏 toorecover 데이터를 사용 하 여 볼륨 컨테이너를 하나 이상 있어야 합니다.
* 클라우드 스냅숏이 여러 볼륨 컨테이너에 걸쳐 있는 경우 StorSimple은 이러한 볼륨 컨테이너를 집합으로 장애 조치합니다. 여러 볼륨 컨테이너에 걸쳐 로컬 스냅숏을 표시 되지만 연결 된 클라우드 스냅숏은 그렇지 않습니다 StorSimple 않습니다 hello 로컬 스냅숏 장애 조치할 드문 인스턴스 및 DR 이후의 hello 로컬 데이터가 손실 됩니다.
* DR에 대 한 hello 사용 가능한 대상 장치는 선택한 볼륨 컨테이너를 hello 충분 한 공간이 tooaccommodate 있는 장치입니다. 충분한 공간이 없는 장치는 대상 장치로 나열되지 않습니다.
* (제한 된 기간 동안)에 대 한 DR 후 hello 데이터 액세스 성능이 크게 저하 될 수 있습니다, 그리고 hello 장치로 필요한 tooaccess hello 클라우드에서 데이터 hello 로컬로 저장 합니다.

#### <a name="device-failover-across-software-versions"></a>여러 소프트웨어 버전 간의 장치 장애 조치(Failover)

배포의 StorSimple 장치 관리자 서비스에는 다른 소프트웨어 버전을 실행하는 여러 물리적 장치 및 클라우드 장치가 있을 수 있습니다.

장애 조치 하거나 다른 소프트웨어 버전 및 DR 중 hello 볼륨 종류의 작동 방식을 실행 하는 백 tooanother 장치 실패 수 있으면 테이블 toodetermine 다음 hello를 사용 합니다.

#### <a name="failover-and-failback-across-software-versions"></a>소프트웨어 버전 간에 장애 조치(failover) 및 장애 복구(failback)

| 장애 조치(Failover)/장애 복구(failback) 원본 | 물리적 장치 | 클라우드 어플라이언스 |
| --- | --- | --- |
| 업데이트 3 tooUpdate 4 |계층화된 볼륨은 계층화된 볼륨으로 장애 조치됩니다. <br></br>로컬 고정 볼륨은 로컬 고정 볼륨으로 장애 조치됩니다. <br></br> 업데이트 4 hello 장치에서 스냅숏을 수행할 때 장애 조치 이후에 [heatmap 기반 추적](storsimple-update4-release-notes.md#whats-new-in-update-4) 시작 하기 전에. |로컬 고정 볼륨은 계층화된 볼륨으로 장애 조치됩니다. |
| 업데이트 4 tooUpdate 3 |계층화된 볼륨은 계층화된 볼륨으로 장애 조치됩니다. <br></br>로컬 고정 볼륨은 로컬 고정 볼륨으로 장애 조치됩니다. <br></br> 백업만 사용 하는 toorestore heatmap 메타 데이터를 유지 합니다. <br></br>heatmap 기반 추적은 장애 복구를 수행하는 업데이트 3에서 사용할 수 없습니다. |로컬 고정 볼륨은 계층화된 볼륨으로 장애 조치됩니다. |


## <a name="device-failover-scenarios"></a>장치 장애 조치 시나리오

재해가 발생 하는 경우에 StorSimple 장치를 통해 toofail를 선택할 수 있습니다.

* [물리적 장치 tooa](storsimple-8000-device-failover-physical-device.md)합니다.
* [tooitself](storsimple-8000-device-failover-same-device.md)합니다.
* [tooa 클라우드 어플라이언스에](storsimple-8000-device-failover-cloud-appliance.md)합니다.

hello 이전 문서를 제공 하는 자세한 단계 각 장애 조치의 경우 위의 hello에 대 한 합니다.


## <a name="failback"></a>장애 복구

업데이트 3 이상 버전의 경우 StorSimple도 장애 복구를 지원합니다. 장애 복구는 장애 조치의 정당한 hello 역방향, hello 대상은 hello 소스 및 이제 hello 장애 조치 중에 원래 소스 장치 hello hello 대상 장치가 됩니다. 

장애 복구 하는 동안 StorSimple 다시 동기화 hello 데이터 백 toohello 기본 위치, I/O hello 및 응용 프로그램 작업을 중지 하 고 백 toohello 원래 위치를 전환 합니다.

장애 조치가 완료 되 면 StorSimple hello 다음 작업을 수행 합니다.

* StorSimple는 hello 소스 장치에서 장애 조치 하는 hello 볼륨 컨테이너를 정리 합니다.
* StorSimple (장애 조치) hello 원본 장치의 볼륨 컨테이너 당 백그라운드 작업을 시작 합니다. Toofail을 hello 작업이 진행 중인 동안에 다시 시도 하면 알림 toothat 효과 수신 합니다. Hello 작업이 완료 toostart hello 장애 복구 될 때까지 기다립니다.
* 볼륨 컨테이너의 toocomplete hello 삭제를 수행 하는 hello 시간 데이터의 양을, hello 작업에 대 한 hello 데이터, 백업 및 사용 가능한 네트워크 대역폭을 hello 수의 보존 기간 등의 다양 한 요인에 따라 달라 집니다.

테스트 장애 조치 또는 테스트 장애 복구를 계획 중인 경우 적은 양의 데이터(Gbs)가 있는 볼륨 컨테이너를 테스트하는 것이 좋습니다. 일반적으로 24 시간 동안 hello 장애 조치를 완료 한 후 hello 장애 복구를 시작할 수 있습니다.

## <a name="frequently-asked-questions"></a>질문과 대답

Q. **DR hello 실패 하거나 부분적으로 성공에 어떻게 되나요?**

A. Hello DR이 실패 하면 다시 시도 하는 것이 좋습니다. 두 번째 장치 장애 조치 작업 hello hello 첫 번째 작업의 hello 진행 상태를 인식 하 고 해당 지점 부터는 시작 합니다.

Q. **장치 장애 조치 hello 진행 중인 동안 장치 삭제 하나요?**

A. DR을 진행 중인 동안에는 장치를 삭제할 수 없습니다. DR hello 완료 된 후에 장치를 삭제할 수 있습니다. Hello hello 장치 장애 조치 작업 진행률을 모니터링할 수 있습니다 **작업** 블레이드입니다.

Q. **경우는 hello 가비지 수집 hello 소스 장치에 있는 시작 hello 로컬 데이터 소스 장치에서 삭제 됩니다?**

A. 가비지 컬렉션은 hello 장치를 완전히 정리 후에 hello 소스 장치에서 사용 됩니다. hello 정리는 장애 조치 hello 원본 장치의 볼륨, 백업 개체 (데이터), 볼륨 컨테이너 및 정책과 같은 개체를 정리 하는 포함 되어 있습니다.

Q. **실패 hello hello 소스 장치에서 hello 볼륨 컨테이너와 연결 된 작업을 삭제 하면 어떻게 되나요?**

A.  Hello 삭제 작업이 실패 하면, hello 볼륨 컨테이너 수동으로 삭제할 수 합니다. Hello에 **장치** 블레이드에서 소스 장치를 선택 하 고 클릭 **볼륨 컨테이너**합니다. 장애 조치 및 hello 블레이드 맨 hello에에서 선택 hello 볼륨 컨테이너를 클릭 **삭제**합니다. 모든 hello를 삭제 한 후 장애 조치 hello 원본 장치의 볼륨 컨테이너 hello 장애 복구를 시작할 수 있습니다. 자세한 내용은 이동 너무[볼륨 컨테이너 삭제](storsimple-8000-manage-volume-containers.md#delete-a-volume-container)합니다.

## <a name="business-continuity-disaster-recovery-bcdr"></a>비즈니스 연속성 재해 복구(BCDR)

비즈니스 연속성 장애 복구 (BCDR) 시나리오에는 hello 전체 Azure 데이터 센터가 작동 중지 될 때 발생 합니다. 이 시나리오는 StorSimple 장치 관리자 서비스에 영향을 줄 수 있습니다 및 hello StorSimple 장치에 연결 합니다.

StorSimple 장치 재해가 발생 하기 직전에 등록 된 경우이 장치 tooundergo 공장 기본 설정 해야 할 수 있습니다. Hello 재해 발생 후 hello StorSimple 장치에에서 표시 hello 오프 라인으로 Azure 포털입니다. Hello 포털에서이 장치를 삭제 해야 합니다. Hello 장치 toofactory 기본값을 다시 설정 하 고 hello 서비스에 다시 등록 합니다.

## <a name="next-steps"></a>다음 단계

장치 장애 조치 준비 tooperform 인 경우 hello 다음 대 한 자세한 지침은 시나리오 중 하나를 선택 합니다.

- [장애 조치 tooanother 물리적 장치](storsimple-8000-device-failover-physical-device.md)
- [장애 조치 toohello 동일한 장치](storsimple-8000-device-failover-same-device.md)
- [장애 조치 tooStorSimple 클라우드 어플라이언스에](storsimple-8000-device-failover-cloud-appliance.md)

및 장치를 통해 실패 한 hello 다음 옵션 중 하나를 선택 합니다.

* [StorSimple 장치 비활성화 및 삭제](storsimple-8000-deactivate-and-delete-device.md)
* [사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-8000-manager-service-administration.md)합니다.

