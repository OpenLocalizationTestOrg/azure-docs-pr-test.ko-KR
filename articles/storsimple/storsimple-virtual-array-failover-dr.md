---
title: "aaaStorSimple 가상 배열 재해 복구 및 장치 장애 조치 | Microsoft Docs"
description: "에 대 한 자세한 방법에 대 한 toofailover StorSimple 가상 배열입니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 3c1f9c62-af57-4634-a0d8-435522d969aa
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5f125efd1ffb94489cdfa7cfaafae7d57cc10131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-and-device-failover-for-your-storsimple-virtual-array-via-azure-portal"></a>Azure Portal을 통해 StorSimple 가상 배열에 대한 재해 복구 및 장치 장애 조치

## <a name="overview"></a>개요
이 문서에서는 Microsoft Azure StorSimple 가상 배열 hello를 포함 하 여 자세한 단계를 통해 tooanother 가상 배열 toofail hello 재해 복구를 설명 합니다. 장애 조치 하면 toomove에서 데이터는 *소스* hello 데이터 센터 tooa에서 장치 *대상* 장치입니다. hello 대상 장치에 못할 동일 하거나 서로 다른 지리적 위치 hello에 있습니다. 장치 장애 조치 hello hello 전체 장치입니다. 장애 조치 중 hello 소스 장치에 대 한 클라우드 데이터 hello hello 대상 장치의 소유권 toothat을 변경합니다.

이 문서는 해당 tooStorSimple 가상 배열만 합니다. 8000 시리즈 장치를 통해 toofail 너무 이동[StorSimple 장치의 장치 장애 조치 및 재해 복구](storsimple-device-failover-disaster-recovery.md)합니다.

## <a name="what-is-disaster-recovery-and-device-failover"></a>재해 복구 및 장치 장애 조치(Failover)란 무엇인가요?

장애 복구 (DR) 시나리오에서 기본 장치 hello 작동이 중지 되었습니다. 이 시나리오에서는 실패 한 장치 tooanother 장치 hello와 관련 된 hello 클라우드 데이터를 이동할 수 있습니다. Hello 기본 장치를 사용 하 여 hello로 *소스* hello로 다른 장치를 지정 하 고 *대상*합니다. 이 프로세스는 참조 된 tooas hello *장애 조치*합니다. 장애 조치 중 모든 hello 볼륨 또는 hello 공유 hello 원본 장치의 소유권이 변경 되며 대상 장치에 전송 된 toohello 합니다. Hello 데이터의 필터링을 하지 않고 허용 됩니다.

DR은 hello 열 지도 기반 계층 구성 및 추적을 사용 하 여 전체 장치 복원으로 모델링 됩니다. 열 지도 기반으로 데이터를 읽고 쓰기 패턴이 열 값 toohello 할당 하 여 정의 됩니다. 이 열에는 계층 hello 가장 낮은 열 데이터 청크 toohello 클라우드 먼저 hello 로컬 계층의 hello (가장 사용 되는) 높은 열 데이터 청크를 유지 하면서 다음 매핑합니다. DR StorSimple 열 지도 toorestore hello를 사용 하 여 처리 도중과 hello 클라우드에서 hello 데이터 리하이드레이션 합니다. hello 장치 (내부적으로 결정)에 따라 모든 hello 볼륨/공유 hello 마지막 최근 백업에 인출 하 고 해당 백업에서 복원을 수행 합니다. hello 가상 배열 hello 전체 DR 프로세스를 조정합니다.

> [!IMPORTANT]
> 따라서 장애 복구는 지원 되지 않습니다 및 장치 장애 조치의 hello 끝에 hello 원본 장치가 삭제 됩니다.
> 
> 

재해 복구 hello 장치 장애 조치 기능을 통해 오케스트레이션 및 hello에서 시작 됩니다 **장치** 블레이드입니다. 이 블레이드 표로 모든 hello StorSimple 장치 연결 된 tooyour StorSimple 장치 관리자 서비스를 작성 합니다. 각 장치에 대 한 hello 이름, 상태, 프로 비전 된 / 최대 용량, 형식 및 모델을 볼 수 있습니다.

## <a name="prerequisites-for-device-failover"></a>장치 장애 조치에 대한 필수 조건

### <a name="prerequisites"></a>필수 조건

장치 장애 조치에 대 한 필수 구성 요소를 다음 해당 hello 충족 확인 합니다.

* hello 소스 장치에서 toobe 필요는 **Deactivated** 상태입니다.
* hello 대상 장치에 필요한 tooshow를으로 **를 tooset 준비** hello Azure 포털의에서. 대상 가상 배열의 hello 프로 비전 동일 하거나 더 높은 용량입니다. 로컬 웹 UI tooconfigure hello를 사용 하 고 성공적으로 hello 대상 가상 배열을 등록 합니다.
  
  > [!IMPORTANT]
  > Tooconfigure hello 등록 된 가상 장치를 hello 서비스를 통해 하지 마십시오. 장치 구성이 hello 서비스를 통해 수행 되어야 합니다.
  > 
  > 
* hello 대상 장치 hello hello 소스 장치로 이름과 같은 이름을 가질 수 없습니다.
* hello 소스 및 대상 장치에 없으면 toobe hello 같은 형식입니다. 파일 서버 tooanother 파일 서버로 구성 하는 가상 배열만 조치할 수 있습니다. hello에 마찬가지입니다 iSCSI 서버입니다.
* DR에는 파일 서버에 대 한 hello 대상 장치 toohello 참가 하는 권장 hello 소스와 같은 도메인입니다. 이 구성을 통해 hello 공유 사용 권한을 자동으로 확인 됩니다. Hello 장애 조치 tooa 대상 장치에만 hello에 동일한 도메인입니다.
* DR에 대 한 hello 사용 가능한 대상 장치는 장치에 있는 동일 hello 또는 용량이 더 큰 toohello 소스 장치 비교입니다. hello 연결된 tooyour는 장치에 서비스에서 하지만 hello에 맞지 않는 장치를 대상으로 사용할 수 없는 충분 한 공간 조건을 합니다.

### <a name="other-considerations"></a>기타 고려 사항

* 계획된 장애 조치(Failover)의 경우 
  
  * 모든 hello 볼륨 또는 공유가 오프 라인으로 hello 소스 장치에서 수행 하는 것이 좋습니다.
  * Hello 장치의 백업을 만들 다음 hello 장애 조치 toominimize 데이터 손실을 진행 하는 것이 좋습니다. 
* 계획 되지 않은 장애 조치의 경우 hello 장치 hello 가장 최근의 백업 toorestore hello 데이터를 사용합니다.

### <a name="device-failover-prechecks"></a>장치 장애 조치 사전 검사

DR을 시작 하는 hello, 하기 전에 hello 장치 prechecks를 수행 합니다. 이러한 검사는 DR이 시작된 후 오류가 발생하지 않도록 하는 데 도움이 됩니다. hello prechecks 다음과 같습니다.

* Hello 저장소 계정의 유효성을 검사 합니다.
* Hello 클라우드 연결 tooAzure 확인 중입니다.
* Hello 대상 장치에서 사용 가능한 공간을 확인 합니다.
* iSCSI 서버 원본 장치 볼륨에 다음 항목이 있는지 확인
  
  * 유효한 ACR 이름
  * 유효한 IQN(220자를 초과하지 않음)
  * 유효한 CHAP 암호(12-16자 길이)

Hello prechecks 앞에 실패할 경우 hello DR 계속할 수 없습니다. 해당 문제를 해결한 후 DR을 다시 시도합니다.

DR hello 성공적으로 완료 되 면 hello 소스 장치에서 클라우드 데이터 hello hello 소유권은 전송 된 toohello 대상 장치. hello 소스 장치를 다음 hello 포털에서 사용할 수 없습니다. 액세스 tooall hello 볼륨/공유 hello 소스 장치에서 차단 하 고 hello 대상 장치 활성화 됩니다.

> [!IMPORTANT]
> Hello 장치를 더 이상 사용할 수 있지만 hello 호스트 시스템에서 프로 비전 하는 hello 가상 컴퓨터는 여전히 리소스를 소비 합니다. DR hello 성공적으로 완료 되 면 호스트 시스템에서이 가상 컴퓨터를 삭제할 수 있습니다.
> 
> 

## <a name="fail-over-tooa-virtual-array"></a>장애 조치 tooa 가상 배열

이 절차를 실행하기 전에 StorSimple 장치 관리자 서비스에 다른 StorSimple 가상 배열을 프로비전, 구성 및 등록하는 것이 좋습니다.

> [!IMPORTANT]
> 
> * StorSimple 8000 시리즈 장치 tooa 1200 가상 장치에서 조치할 수 없습니다.
> * Federal FIPS Information Processing Standard () 사용 하도록 설정 가상 장치 tooanother FIPS 사용 장치 또는 hello 정부 포털에 배포 된 tooa 비 FIPS 장치에서 조치할 수 있습니다.


Hello 단계 toorestore hello 장치 tooa 대상 StorSimple 가상 장치를 다음을 수행 합니다.

1. 프로 비전 및 구성 hello를 충족 하는 대상 장치 [장치 장애 조치에 대 한 필수 구성 요소](#prerequisites)합니다. Hello 로컬 웹 UI 통해 hello 장치 구성을 완료 하 고 tooyour StorSimple 장치 관리자 서비스를 등록 합니다. 파일 서버를 만드는 경우 이동의 1 toostep [파일 서버로 설정](storsimple-virtual-array-deploy3-fs-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device)합니다. ISCSI 서버를 만드는 경우 이동의 1 toostep [iSCSI 서버로 설정](storsimple-virtual-array-deploy3-iscsi-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device)합니다.

2. Hello 호스트에서 오프 라인 볼륨/공유를 수행 합니다. tootake hello 볼륨/공유 오프 라인으로 hello 호스트에 대 한 toohello 운영 체제 관련 지침을 참조 하십시오. 이미 오프 하지 해야 tootake 모든 hello 볼륨/공유 오프 라인으로 hello 장치에서 hello 다음을 수행 하 여 합니다.
   
    1. 너무 이동**장치** 블레이드 하 고 장치를 선택 합니다.
   
    2. 너무 이동**설정 > 관리 > 공유** (또는 **설정 > 관리 > 볼륨**). 
   
    3. 공유/볼륨을 선택하고 **오프라인으로 전환**을 마우스 오른쪽 단추로 클릭하고 선택합니다. 
   
    4. 확인 메시지가 표시 되 면 확인 **오프 라인으로이 공유의 hello 영향을 이해 합니다.** 
   
    5. **오프라인으로 전환**을 클릭합니다.

3. StorSimple 장치 관리자 서비스에 이동 너무**관리 > 장치**합니다. Hello에 **장치** 블레이드를 선택 하 고 원본 장치를 클릭 합니다.

4. **장치 대시보드** 블레이드에서 **비활성화**를 클릭합니다.

5. Hello에 **비활성화** 블레이드를 확인 메시지가 표시 됩니다. 장치 비활성화는 *영구적인* 프로세스이며 취소할 수 없습니다. 사용자는 또한 알림을 tootake 공유/볼륨 오프 라인으로 hello 호스트에 있습니다. 장치 이름 tooconfirm hello를 입력 하 고 클릭 **비활성화**합니다.
   
    ![](./media/storsimple-virtual-array-failover-dr/failover1.png)
6. hello 비활성화가 시작 됩니다. Hello 비활성화 성공적으로 완료 된 후에 알림을 받습니다.
   
    ![](./media/storsimple-virtual-array-failover-dr/failover2.png)
7. Hello 장치 페이지 hello 장치 상태는 이제 바뀝니다 너무**Deactivated**합니다.
    ![](./media/storsimple-virtual-array-failover-dr/failover3.png)
8. Hello에 **장치** 장애 조치에 대 한 hello 비활성화 된 소스 장치 블레이드 선택 하 고을 클릭 합니다. 
9. Hello에 **장치 대시보드** 블레이드에서 클릭 **장애 조치**합니다. 
10. Hello에 **장치 장애 조치할** 블레이드에서 다음 hello지 않습니다.
    
    1. hello 소스 장치 필드가 자동으로 채워집니다. Note hello 소스 장치에 대 한 hello 총 데이터 크기입니다. hello 데이터 크기는 hello hello 대상 장치에서 사용 가능한 용량 보다 더 작은 값 이어야 합니다. 장치 이름, 전체 용량 및 장애 조치 됩니다 hello 공유 hello 이름과 같은 hello 원본 장치와 관련 된 hello 세부 정보를 검토 합니다.

    2. 사용 가능한 장치 hello 드롭다운 목록에서 선택 된 **대상 장치**합니다. 충분 한 용량이 있는 장치만 hello hello 드롭다운 목록에 표시 됩니다.

    3. 확인 **데이터 toohello 대상 장치를 통해이 작업을 수행할 이해**합니다. 

    4. **장애 조치**를 클릭합니다.
    
        ![](./media/storsimple-virtual-array-failover-dr/failover4.png)
11. 장애 조치 작업을 시작하면 알림이 표시됩니다. 너무 이동**장치 > 작업** toomonitor hello 장애 조치 합니다.
    
     ![](./media/storsimple-virtual-array-failover-dr/failover5.png)
12. Hello에 **작업** 블레이드에 hello 소스 장치에 대해 만든 장애 조치 작업을 표시 합니다. 이 작업은 DR prechecks hello를 수행 합니다.
    
    ![](./media/storsimple-virtual-array-failover-dr/failover6.png)
    
     DR hello prechecks 성공 후 hello 장애 조치 작업에는 소스 장치에 있는 각 공유/볼륨에 대 한 복원 작업이 배치 됩니다.
    
    ![](./media/storsimple-virtual-array-failover-dr/failover7.png)
13. Hello 장애 조치가 완전 하 고 이동 toohello 후 **장치** 블레이드입니다.
    
    1. 선택한 hello 장애 조치 프로세스에 대 한 hello 대상 장치로 사용 했던 hello StorSimple 장치를 클릭 합니다.
    2. 너무 이동**설정 > 관리 > 공유** (또는 **볼륨** 경우 iSCSI 서버). Hello에 **공유** 블레이드에서 hello 오래 된 장치에서 모든 hello 공유 (볼륨)를 볼 수 있습니다.
        ![](./media/storsimple-virtual-array-failover-dr/failover9.png)
14. 너무 필요 합니다[DNS 별칭 만들기](https://support.microsoft.com/kb/168322) 를 시도 하 고 있는 응용 프로그램을 hello 모든 tooconnect 리디렉션된 toohello 새 장치를 가져올 수 있습니다.

## <a name="errors-during-dr"></a>DR 중 오류

**DR 중 클라우드 연결 중단**

후 hello 클라우드 연결에 문제가 있을 경우 DR을 시작 하 고 hello 장치 복원이 완료 되 면 전에 hello DR 실패 합니다. 장애 조치 알림을 받게 됩니다. DR에 대 한 대상 장치 hello로 표시 되어 *사용할 수 없게 됩니다.* Hello를 사용할 수 없는 이후 DRs에 대 한 동일한 대상 장치입니다.

**호환되는 대상 장치 없음**

Hello 사용 가능한 대상 장치에 충분 한 공간이 없는 경우 호환 되는 대상 장치가 없는 오류 toohello 효과 표시 됩니다.

**사전 검사 실패**

Hello prechecks 중 하나가 충족 되지 않은 경우 precheck 실패가 표시 있습니다.

## <a name="business-continuity-disaster-recovery-bcdr"></a>비즈니스 연속성 재해 복구(BCDR)

비즈니스 연속성 장애 복구 (BCDR) 시나리오에는 hello 전체 Azure 데이터 센터가 작동 중지 될 때 발생 합니다. StorSimple 장치 관리자 서비스에 영향을 줄 수 있습니다 및 hello StorSimple 장치에 연결 합니다.

재해가 발생 하기 직전에 등록 된 StorSimple 장치가 없을 경우 이러한 StorSimple 장치 toobe 삭제 해야 할 수 있습니다. Hello 재해 발생 후 다시 만들고 해당 장치를 구성할 수 있습니다.

## <a name="next-steps"></a>다음 단계

너무 방법에 대 한 자세한[hello 로컬 웹 UI를 사용 하 여 StorSimple 가상 배열 관리](storsimple-ova-web-ui-admin.md)합니다.

