---
title: "aaaStorSimple 장애 조치 및 재해 복구 | Microsoft Docs"
description: "자세한 방법을 통해 StorSimple 장치 tooitself, 다른 물리적 장치 또는 가상 장치 toofail 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5751598e-49c8-42b3-8121-fea5857a7d83
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/16/2016
ms.author: alkohli
ms.openlocfilehash: 00ce365f8a9095d1f0292e665d7f9eaa844b44ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="failover-and-disaster-recovery-for-your-storsimple-device"></a>StorSimple 장치에 대한 장애 조치 및 재해 복구
## <a name="overview"></a>개요
이 자습서에서는 재해의 hello 이벤트에서 StorSimple 장치에 대 hello 단계 필요한 toofail를 설명 합니다. 장애 조치 하면 toomigrate 동일 하거나 서로 다른 지리적 위치에서 실제 hello 데이터 센터 tooanother 소스 장치나 가상 장치로 데이터 hello에 있는 합니다. 

DR (재해 복구) hello 장치 장애 조치 기능을 통해 오케스트레이션 및 hello에서 시작 됩니다 **장치** 페이지. 이 페이지는 장치 연결 된 tooyour StorSimple Manager 서비스를 대 한 모든의 hello StorSimple 표 형식으로 만듭니다. 각 장치, hello 이름, 상태, 프로 비전 된 / 최대 용량, 형식 및 모델 표시 됩니다.

![장치 페이지](./media/storsimple-device-failover-disaster-recovery/IC740972.png)

이 자습서의 지침에 hello 모든 소프트웨어 버전에서 tooStorSimple 실제 및 가상 장치를 적용합니다.

## <a name="disaster-recovery-dr-and-device-failover"></a>DR(재해 복구) 및 장치 장애 조치
장애 복구 (DR) 시나리오에서 기본 장치 hello 작동이 중지 되었습니다. 이 경우 hello로 hello 기본 장치를 사용 하 여 hello 오류가 발생 한 장치 tooanother 장치와 연결 된 hello 클라우드 데이터를 이동할 수 있습니다 *소스* hello로 다른 장치를 지정 하 고 *대상*합니다. 하나 이상의 볼륨 컨테이너 toomigrate toohello 대상 장치를 선택할 수 있습니다. 이 프로세스는 참조 된 tooas hello *장애 조치*합니다. 

Hello 장애 조치 중 hello hello 원본 장치의 볼륨 컨테이너는 소유권이 변경 되며 대상 장치에 전송 된 toohello 합니다. 소유권을 변경 하는 hello 볼륨 컨테이너 이러한 hello 소스 장치에서 삭제 됩니다. Hello 삭제가 완료 되 면 hello 대상 장치 다시 장애 후 수 있습니다.

DR, 가장 최근의 백업 hello 일반적으로 다음은 사용 되는 toorestore hello 데이터 toohello 대상 장치입니다. 그러나 없는 경우 여러 백업 정책에 대 한 hello 동일한 볼륨, 다음 볼륨의 최대 hello와 hello 백업 정책을 선택 고 hello 가장 최근의 백업 정책에서는 hello 대상 장치에 사용 되는 toorestore hello 데이터.

예를 들어 백업 정책 (하나의 기본 및 하나의 사용자 지정)을 다음 두 가지가 경우 *defaultPol*, *customPol* hello 다음 세부 정보로:

* *defaultPol*: 하나의 볼륨(*vol1*)이 매일 오후 10시 30분부터 실행됩니다.
* *customPol*: 4개의 볼륨(*vol1*, *vol2*, *vol3*, *vol4*)이 매일 오후 10시부터 실행됩니다.

이 경우에 더 많은 볼륨을 포함하고 크래시 일관성에 대한 우선 순위를 지정한 *customPol* 을 사용합니다. 이 정책에서 가장 최근의 백업을 hello toorestore 사용 되는 데이터입니다.

## <a name="considerations-for-device-failover"></a>장치 장애 조치에 대한 고려 사항
재해의 hello 이벤트를 통해 StorSimple 장치 toofail를 선택할 수 있습니다.

* tooa 물리적 장치 
* tooitself
* tooa 가상 장치

모든 장치 장애 조치에 대해 유의 hello 다음에 유의 하십시오.

* hello DR에 대 한 필수 구성 요소는 hello 볼륨 컨테이너 내의 모든 hello 볼륨을 오프 라인 및 hello 볼륨 컨테이너는 연결 된 클라우드 스냅숏이 있습니다. 
* DR에 대 한 hello 사용 가능한 대상 장치는 선택한 볼륨 컨테이너를 hello 충분 한 공간이 tooaccommodate 있는 장치입니다. 
* hello 연결된 tooyour는 장치에 서비스에서 하지만 충분 한의 hello 조건을 충족 하지 않는 공간 대상 장치로 사용할 수 없습니다.
* 제한 된 기간에 대 한 DR 다음 hello 데이터 액세스 성능이 크게 저하 될 수 있습니다, 그리고 hello 장치로 필요 tooaccess hello hello 클라우드에서 데이터를 로컬로 저장 합니다.

#### <a name="device-failover-across-software-versions"></a>여러 소프트웨어 버전 간의 장치 장애 조치(Failover)
배포의 StorSimple Manager 서비스에 서로 다른 소프트웨어 버전을 실행하는 여러 장치(물리적 및 가상)가 있을 수 있습니다. Hello 소프트웨어 버전에 따라, hello 장치의 hello 볼륨 유형에 다 수 있습니다. 예를 들어 업데이트 2 이상을 실행하는 장치에는 로컬로 고정된 볼륨과 계층화된 볼륨(아카이브 볼륨은 계층화된 볼륨의 하위 집합)이 있을 수 있습니다. 사전 업데이트 2 장치 hello에 다른 손을 계층 있을 수 있습니다 및 보관 볼륨입니다. 

DR 동안 볼륨 종류의 다른 소프트웨어 버전 및 hello 동작을 실행 하는 tooanother 장치 장애 조치할 수 있습니다 하는 경우 테이블 toodetermine 다음 hello를 사용 합니다.

| 장애 조치 대상 | 물리적 장치에 허용됨 | 가상 장치에 허용됨 |
| --- | --- | --- |
| 업데이트 2 toopre-업데이트 1 (릴리스, 0.1, 0.2, 0.3) |아니요 |아니요 |
| 업데이트 2 tooUpdate 1 (1, 1.1, 1.2) |예 <br></br>사용 하 여 로컬로 고정 된 또는 볼륨을 계층화 된 경우 또는 다양 한 볼륨은으로 장애 조치 항상 두, hello 계층입니다. |예<br></br>로컬로 고정된 볼륨을 사용하는 경우 계층화된 것으로 장애 조치(failover)됩니다. |
| 업데이트 2 tooUpdate 2 (이후 버전) |예<br></br>로컬로 고정 된 또는 계층화 된 볼륨 또는 2의 혼합을 사용 하는 경우 hello 볼륨 항상 장애 조치 됩니다 볼륨 종류가; 시작 hello로 로컬과 고정 계층 구성 및 로컬로 고정 된 계층입니다. |예<br></br>로컬로 고정된 볼륨을 사용하는 경우 계층화된 것으로 장애 조치(failover)됩니다. |

#### <a name="partial-failover-across-software-versions"></a>여러 소프트웨어 버전 간의 부분 장애 조치(failover)
Tooperform 전 업데이트 1 tooa 대상 업데이트 1 이상을 실행 하 고 실행 하는 StorSimple 원본 장치를 사용 하 여 부분 장애를 가져오려는 경우이 지침을 따릅니다. 

| 다음에서 부분 장애 조치(failover) | 물리적 장치에 허용됨 | 가상 장치에 허용됨 |
| --- | --- | --- |
| 사전 업데이트 1 (릴리스, 0.1, 0.2, 0.3) tooUpdate 1 이상 |예, 모범 사례 팁 hello에 대 한 아래의 참조 하십시오. |예, 모범 사례 팁 hello에 대 한 아래의 참조 하십시오. |

> [!TIP]
> 업데이트 1 이상 버전에서 클라우드 메타데이터 및 데이터 서식이 변경되었습니다. 따라서 권장 하지는 않습니다 전 업데이트 1 tooUpdate 1에서에서 부분 장애 조치 또는 이후 버전입니다. Tooperform 부분 장애 조치 해야 할 경우 먼저 업데이트 1 또는 나중에 두 hello 장치 (원본 및 대상)을 적용 하 고 다음 hello 장애 조치를 진행 하는 것이 좋습니다. 
> 
> 

## <a name="fail-over-tooanother-physical-device"></a>장애 조치 tooanother 물리적 장치
다음 단계 toorestore hello 장치 tooa 대상 물리적 장치를 수행 합니다.

1. 통해 toofail 하려는 해당 hello 볼륨 컨테이너에 연결 된 클라우드 스냅숏이 확인 합니다.
2. Hello에 **장치** 페이지에서 hello **볼륨 컨테이너** 탭 합니다.
3. 싶다는 의사를 toofail tooanother 장치에 대 한 볼륨 컨테이너를 선택 합니다. 이 컨테이너 내의 볼륨 hello 볼륨 컨테이너 toodisplay hello 목록을 클릭 합니다. 볼륨을 선택 하 고 클릭 **오프 라인으로 전환** tootake hello 볼륨을 오프 합니다. Hello 볼륨 컨테이너에서 모든 hello 볼륨에 대해이 프로세스를 반복 합니다.
4. 이전 단계를 반복 hello toofail tooanother 장치를 통해 하려는 모든 볼륨 컨테이너를 hello에 대 한 합니다.
5. Hello에 **장치** 페이지 **장애 조치**합니다.
6. 열리면 hello 마법사에서 **볼륨 컨테이너 toofail 선택**:
   
   1. 볼륨 컨테이너의 hello 목록에서 원하는 toofail 통해 hello 볼륨 컨테이너를 선택 합니다.
      **연결 된 클라우드 스냅숏이 있는 볼륨 컨테이너를 hello만 하 고 오프 라인 볼륨이 표시 됩니다.**
   2. 아래 **대상 장치 선택** hello 선택 컨테이너에서 hello 볼륨의 사용 가능한 장치 hello 드롭 다운 목록에서 대상 장치를 선택 합니다. Hello 사용 가능한 용량이 있는 장치만 hello hello 드롭 다운 목록에 표시 됩니다.
   3. 마지막으로 아래에서 모든 hello 장애 조치 설정을 검토 **장애 조치를 확인**합니다. Hello 확인 아이콘을 클릭 ![확인 아이콘](./media/storsimple-device-failover-disaster-recovery/IC740895.png)합니다.
7. 장애 조치 작업이 만들어집니다 hello를 통해 모니터링할 수 있습니다 **작업** 페이지. 장애 조치 hello 볼륨 컨테이너에 볼륨이 로컬 각 로컬 볼륨 (하지 계층화 된 볼륨) hello 컨테이너에에 대 한 개별 복원 작업이 표시 됩니다. 이러한 복원 작업 시간 toocomplete 다소 걸릴 수 있습니다. 되었을 hello 장애 조치 작업 이전에 완료 될 수 있습니다. 이러한 볼륨을 들 수 있는 로컬 보장 hello 복원 작업이 완료 된 후에 확인 합니다. Hello 장애 조치가 완료 된 후 이동 toohello **장치** 페이지.                                            
   
   1. Hello 장애 조치 프로세스에 대 한 hello 대상 장치로 사용 했던 hello 장치를 선택 합니다.
   2. Toohello 이동 **볼륨 컨테이너** 페이지. Hello hello 이전 장치의 볼륨과 함께 모든 hello 볼륨 컨테이너를 나열 합니다.

## <a name="failover-using-a-single-device"></a>단일 장치를 사용하여 장애 조치
Hello만 있는 단일 장치와 필요 tooperform 장애 조치 하는 경우 다음 단계를 수행 합니다.

1. 클라우드 스냅숏을 모든 hello 볼륨의 장치에서 만듭니다.
2. 장치 toofactory 기본값 다시 설정 합니다. 에 따라 hello에 필요한 세부 정보 [tooreset StorSimple 장치 toofactory 기본 설정 방법을](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings)합니다.
3. 장치를 구성하고 StorSimple 관리자 서비스로 다시 등록 합니다.
4. Hello에 **장치** 페이지에서 이전 장치 hello로 표시 해야 **오프 라인**합니다. hello 새로 등록 된 장치도 표시 되어야 **온라인**합니다.
5. Hello 새 장치에 대 한 hello 장치의 최소 구성 hello을 먼저 완료 되어야 합니다. 
   
   > [!IMPORTANT]
   > **Hello 최소 구성을 먼저 완료 하지 않으면 hello 현재 구현의 버그로 인해 DR이 실패 합니다. 이 동작은 이후 릴리스에서 수정될 예정입니다.**
   > 
   > 
6. Hello 오래 된 장치 (오프 라인 상태)를 선택 하 고 클릭 **장애 조치**합니다. 제공 되는 hello 마법사에서이 장치를 장애 조치할 고 hello 새로 등록 된 장치로 hello 대상 장치를 지정 합니다. 자세한 내용은 참조 너무[tooanother 물리적 장치를 장애 조치할](#fail-over-to-another-physical-device)합니다.
7. Hello에서 모니터링할 수 있는 장치 복원 작업을 만들 수는 **작업** 페이지.
8. Hello 작업이 성공적으로 완료 되 면 hello 새 장치를 액세스 하 고 toohello 탐색 **볼륨 컨테이너** 페이지. Hello 오래 된 장치에서 모든 hello 볼륨 컨테이너를 마이그레이션된 toohello 새 장치를 수 있습니다.

## <a name="fail-over-tooa-storsimple-virtual-device"></a>장애 조치 tooa StorSimple 가상 장치
StorSimple 가상 장치를 만들고 이전 toorunning를 구성한 경우이 절차입니다. 업데이트 2를 실행 하는 경우에 hello 64TB 고 프리미엄 저장소를 사용 하 여 DR에 대 한 8020 가상 장치를 사용 하는 것이 좋습니다. 

Hello 단계 toorestore hello 장치 tooa 대상 StorSimple 가상 장치를 다음을 수행 합니다.

1. 통해 toofail 하려는 해당 hello 볼륨 컨테이너에 연결 된 클라우드 스냅숏이 확인 합니다.
2. Hello에 **장치** 페이지에서 hello **볼륨 컨테이너** 탭 합니다.
3. 싶다는 의사를 toofail tooanother 장치에 대 한 볼륨 컨테이너를 선택 합니다. 이 컨테이너 내의 볼륨 hello 볼륨 컨테이너 toodisplay hello 목록을 클릭 합니다. 볼륨을 선택 하 고 클릭 **오프 라인으로 전환** tootake hello 볼륨을 오프 합니다. Hello 볼륨 컨테이너에서 모든 hello 볼륨에 대해이 프로세스를 반복 합니다.
4. 이전 단계를 반복 hello toofail tooanother 장치를 통해 하려는 모든 볼륨 컨테이너를 hello에 대 한 합니다.
5. Hello에 **장치** 페이지 **장애 조치**합니다.
6. 열리면 hello 마법사에서 **볼륨 컨테이너 toofailover 선택**, hello 다음을 수행 합니다.
   
    a. 볼륨 컨테이너의 hello 목록에서 원하는 toofail 통해 hello 볼륨 컨테이너를 선택 합니다.
   
    **연결 된 클라우드 스냅숏이 있는 볼륨 컨테이너를 hello만 하 고 오프 라인 볼륨이 표시 됩니다.**
   
    b. 아래 **hello 선택 컨테이너에서 hello 볼륨에 대 한 대상 장치 선택**, 선택 hello hello 드롭다운 목록에서 사용 가능한 장치에서 StorSimple 가상 장치입니다. **충분 한 용량이 있는 장치만 hello hello 드롭 다운 목록에 표시 됩니다.**  
7. 마지막으로 아래에서 모든 hello 장애 조치 설정을 검토 **장애 조치를 확인**합니다. Hello 확인 아이콘을 클릭 ![확인 아이콘](./media/storsimple-device-failover-disaster-recovery/IC740895.png)합니다.
8. Hello 장애 조치가 완료 된 후 이동 toohello **장치** 페이지.
   
    a. Hello 장애 조치 프로세스에 대 한 hello 대상 장치로 사용 된 hello StorSimple 가상 장치를 선택 합니다.
   
    b. Toohello 이동 **볼륨 컨테이너** 페이지. 이제 hello hello 이전 장치의 볼륨과 함께 모든 hello 볼륨 컨테이너를 나열 합니다.

![동영상 사용 가능](./media/storsimple-device-failover-disaster-recovery/Video_icon.png) **동영상 사용 가능**

복원 하는 방법을 통해 오류가 발생 한 물리적 장치 hello 클라우드에서 tooa 가상 장치를 통해 보여 주는 비디오에서 toowatch 클릭 [여기](https://azure.microsoft.com/documentation/videos/storsimple-and-disaster-recovery/)합니다.

## <a name="failback"></a>장애 복구
업데이트 3 이상 버전의 경우 StorSimple도 장애 복구를 지원합니다. Hello 장애 조치가 완료 되 면 hello 다음 작업이 수행 됩니다.

* 장애 조치 됩니다 hello 볼륨 컨테이너를 hello 소스 장치에서 청소 됩니다.
* Hello 원본 장치의 볼륨 컨테이너 (장애 조치) 당 백그라운드 작업 시작 됩니다. Hello 작업이 진행 중인 동안 toofailback를 시도 하면 알림 toothat 효과 받게 됩니다. Hello 작업이 완료 toostart hello 장애 복구가 수행 될 때까지 toowait이 필요 합니다. 
  
    볼륨 컨테이너 hello 시간 toocomplete hello 삭제 하는 데이터의 양을, hello 작업에 대 한 hello 데이터, 백업 및 사용 가능한 네트워크 대역폭을 hello 수의 보존 기간 등의 다양 한 요인에 따라 다릅니다. 테스트 장애 조치/장애 복구를 계획 중인 경우 적은 양의 데이터(Gbs)가 있는 볼륨 컨테이너를 테스트하는 것이 좋습니다. 대부분의 경우에서 hello 장애 복구 hello 장애 조치가 완료 된 후 24 시간을 시작할 수 있습니다. 

## <a name="frequently-asked-questions"></a>질문과 대답
Q. **DR hello 실패 하거나 부분적으로 성공에 어떻게 되나요?**

A. Hello DR이 실패 하면 다시 시도 하는 것이 좋습니다. hello, 두 번째로 DR 알고 어떤 모든 구현 되었으며 때 hello 프로세스 중단 hello 처음으로 합니다. 해당 지점 부터는 hello DR 프로세스를 시작합니다. 

Q. **장치 장애 조치 hello 진행 중인 동안 장치 삭제 하나요?**

A. DR을 진행 중인 동안에는 장치를 삭제할 수 없습니다. DR hello 완료 된 후에 장치를 삭제할 수 있습니다.

Q.    **경우는 hello 가비지 수집 hello 소스 장치에 있는 시작 hello 로컬 데이터 소스 장치에서 삭제 됩니다?**

A. 가비지 수집 hello 장치 완전히 정리 후에 hello 소스 장치에서 활성화 됩니다. hello 정리는 장애 조치 hello 원본 장치의 볼륨, 백업 개체 (데이터), 볼륨 컨테이너 및 정책과 같은 개체를 정리 하는 포함 되어 있습니다.

Q. **실패 hello hello 소스 장치에서 hello 볼륨 컨테이너와 연결 된 작업을 삭제 하면 어떻게 되나요?**

A.  Hello 작업 실패를 삭제 해야 합니다 toomanually 트리거 hello hello 볼륨 컨테이너를 삭제 합니다. Hello에 **장치** 페이지 소스 장치를 선택 하 고 클릭 **볼륨 컨테이너**합니다. 장애 조치 및 hello hello 페이지 아래에서 선택 hello 볼륨 컨테이너를 클릭 **삭제**합니다. 모든 hello를 삭제 한 후 장애 조치 hello 원본 장치의 볼륨 컨테이너 hello 장애 복구를 시작할 수 있습니다.

## <a name="business-continuity-disaster-recovery-bcdr"></a>비즈니스 연속성 재해 복구(BCDR)
비즈니스 연속성 장애 복구 (BCDR) 시나리오에는 hello 전체 Azure 데이터 센터가 작동 중지 될 때 발생 합니다. StorSimple Manager 서비스에 영향을 줄 수 있습니다 및 hello StorSimple 장치에 연결 합니다.

재해가 발생 하기 직전에 등록 된 StorSimple 장치가 없을 경우 이러한 StorSimple 장치 tooundergo 공장 기본 설정 해야 할 수 있습니다. Hello 재해 발생 후 hello StorSimple 장치가 나타납니다 오프 라인으로. hello 포털에서 hello StorSimple 장치를 삭제 해야 하며 등록 뒤 공장 재설정을 해야 합니다.

## <a name="next-steps"></a>다음 단계
* 장애 조치를 수행한 후 해야 너무[비활성화 또는 삭제 StorSimple 장치](storsimple-deactivate-and-delete-device.md)합니다.
* 어떻게 toouse hello StorSimple Manager에 대 한 정보에 대 한 서비스, 너무 이동[사용 하 여 StorSimple 장치를 StorSimple Manager 서비스 tooadminister hello](storsimple-manager-service-administration.md)합니다.

