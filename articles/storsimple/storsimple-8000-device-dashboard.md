---
title: "요약 aaaUse StorSimple 8000 시리즈 장치 | Microsoft Docs"
description: "Hello StorSimple 장치 관리자 서비스 장치 요약 설명 및 방법을 toouse 것 tooview 저장소 메트릭 및 연결 된 시작자 및 찾기 hello 일련 번호와 IQN 합니다."
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: b45ffc6ec52ebb6549c25a00c68c62460b208b7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-summary-in-storsimple-device-manager-service"></a>Hello 장치를 StorSimple 장치 관리자 서비스에서 요약 정보를 사용 하 여

## <a name="overview"></a>개요
hello StorSimple 장치에 대 한 요약 블레이드 특정 StorSimple 장치에 대 한 정보를 간략하게 보여 줍니다., 반대로 toohello 서비스 요약 블레이드를 Microsoft Azure StorSimple 솔루션에 포함 된 모든 hello 장치에 대 한 정보를 제공 합니다.

hello 장치 요약 블레이드 다양 한 장치 문제는 시스템 관리자의 주의가 필요한를 강조 표시 하는 지정 된 StorSimple 장치 관리자와 등록 된 StorSimple 8000 시리즈 장치에 대 한 요약 보기를 제공 합니다. 이 자습서 hello 장치 요약 블레이드를 소개 하 고 hello 콘텐츠 및 함수를 설명 하며이 블레이드에서 수행할 수 있는 hello 작업에 설명 합니다.

hello 장치 요약 블레이드 hello를 다음 정보를 표시 합니다.

![장치 요약 블레이드](./media/storsimple-8000-device-dashboard/device-summary1.png)

## <a name="management-command-bar"></a>관리 명령 모음

Hello StorSimple 장치 블레이드에 StorSimple 장치를 관리 하기 위한 hello 옵션 표시 됩니다. Hello의 위쪽 hello 블레이드 및 hello 왼쪽에 걸쳐 hello 관리 명령을 볼 수 있습니다. 이러한 옵션 tooadd 공유 또는 볼륨을 사용 하 또는 업데이트 하거나 장애 조치 장치.

![관리 명령 모음](./media/storsimple-8000-device-dashboard/device-summary2.png)

## <a name="essentials"></a>Essentials

hello essentials 영역 hello와 같은 중요 한 속성, hello 상태, 모델, 대상 IQN 및 hello 소프트웨어 버전 중 일부를 캡처합니다. 

![장치 Essentials](./media/storsimple-8000-device-dashboard/device-summary3.png)

## <a name="monitoring"></a>모니터링

* hello **경고** 타일 경고 심각도 별로 그룹화 된 장치에 대 한 모든 hello 활성 경고의 스냅숏을 제공 합니다.

    ![경고 타일](./media/storsimple-8000-device-dashboard/device-summary4.png)

    Hello 타일 tooopen hello 클릭 **경고** 블레이드 및 클릭 한 다음 개별 경고 tooview 추가 권장 되는 작업을 포함 하 여 해당 경고에 대 한 세부 정보입니다. Hello 문제가 해결 된 경우에 hello 경고를 지울 수 있습니다.

    ![경고 타일 클릭](./media/storsimple-8000-device-dashboard/device-summary10.png)

* hello **상태 및 상태** 타일은 hello 장치 상태를 포함 하 여 장치에 대 한 hello 하드웨어 구성 요소 상태에 대 한 정보를 제공 합니다. hello 장치 상태를 오프 라인, 온라인, 비활성화 또는 준비 tooset 수 있습니다.

    ![상태 타일](./media/storsimple-8000-device-dashboard/device-summary5.png)

* hello **볼륨** 타일은 상태별으로 그룹화 된 장치에 볼륨 hello 수에 대 한 요약을 제공 합니다.

    ![볼륨 타일](./media/storsimple-8000-device-dashboard/device-summary6.png)

    Hello 타일 tooopen hello 클릭 **볼륨** 블레이드를 표시 한 다음 개별 볼륨 tooview 클릭 하거나 해당 속성을 수정 합니다.
    
    ![볼륨 타일 클릭](./media/storsimple-8000-device-dashboard/device-summary9.png)
    
    자세한 내용은 참조 방법을 너무[볼륨 관리](storsimple-8000-manage-volumes-u2.md)합니다.

* Hello에 **사용** 차트에서는 장치 및 지난 7 일 hello 기본 시간 간격 동안 hello 사용 된 hello 클라우드 저장소에서 사용 되는 hello 주 저장소를 볼 수 있습니다.

     ![사용량 타일](./media/storsimple-8000-device-dashboard/device-summary7.png)
    
     toochoose 서로 다른 시간 단위를 사용 하 여 hello **편집** hello 차트의 hello 오른쪽 위 모서리에서 옵션입니다.

     ![사용 현황 차트 편집](./media/storsimple-8000-device-dashboard/device-summary12.png)

     이 차트를 볼 hello 총 기본 저장소 (hello 호스트 tooyour 장치 기록한 데이터의 양)에 대 한 메트릭을 있고 hello 총 클라우드 저장소 시간 동안 장치가 차지 합니다.
  
     이 컨텍스트에서 *주 저장소* hello 호스트에 의해 기록 된 데이터의 총 toohello 참조 하 고 볼륨 유형으로 세분화 될 수 있습니다: *주 저장소 계층* 모두 포함 데이터와 데이터를 로컬로 저장 계층화 된 toohello 클라우드입니다. *로컬로 고정된 기본 저장소*는 로컬로 저장된 데이터만 포함합니다. *클라우드 저장소*, 다른 손 hello, hello 클라우드에 저장 된 데이터의 총 금액 hello 측정 한 값입니다. 이 저장소에는 계층화된 데이터 및 백업이 포함됩니다. hello 클라우드에 저장 된 hello 데이터 중복 제거 된 이며 압축, 기본 저장소 hello hello 데이터 중복 제거 되 고 압축 하기 전에 사용 하는 저장소 양을 나타냅니다. (이러한 두 숫자 tooget hello 압축 비율의 관념 비교할 수 있습니다.) 모두 기본에 대 한 클라우드 저장소에 표시 된 구성한 빈도 추적 하는 hello를 기반으로 하는 hello 및 합니다. 예를 들어 1 주일 빈도 선택 하면 다음 hello 차트 표시 데이터 hello에 지난 주의 각 날에 대 한 됩니다.

     시간, 선택 hello를 통해 사용한 클라우드 저장소의 toosee hello 양을 **클라우드 저장소 사용** 옵션입니다. 선택 hello hello 호스트에 의해 기록 된 toosee hello 총 저장소 **기본 계층으로 계층화 된 저장소 사용** 및 **기본 로컬로 고정 된 저장소 사용 됨** 옵션입니다. 
     자세한 내용은 참조 [사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 toomonitor hello](storsimple-monitor-device.md)합니다.


* hello **용량** 프로 비전 된 타일 표시 hello 주 저장소 및 hello 장치 상대 toohello 총 저장소에서 남은 hello 동일 합니다. **사용자를 프로 비전** 준비 하 고 사용 하기 위해 할당 된 저장소 용량과 toohello 참조 **남은** 이 장치에서 프로 비전 할 수 있는 용량 남은 toohello 참조 합니다. 

    ![사용량 타일](./media/storsimple-8000-device-dashboard/device-summary8.png)

    이 타일 tooview hello 용량은 계층화 된 및 로컬 고정 볼륨에 걸쳐 프로 비전 하는 방법을 클릭 합니다. hello **나머지 계층** 용량이 hello 하는 동안 클라우드를 포함 하 여 프로 비전 할 수 있는 사용 가능한 용량 hello **나머지 로컬** hello 디스크에 남아 있는 hello 용량은 toothis 장치를 연결 합니다.

    ![사용 현황 차트 클릭](./media/storsimple-8000-device-dashboard/device-summary13.png)


## <a name="next-steps"></a>다음 단계
* Hello에 대 한 자세한 [StorSimple 서비스 요약 블레이드](storsimple-8000-service-dashboard.md)합니다.
* 에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple 장치 관리자 서비스 tooadminister를 hello를 사용 하 여](storsimple-8000-manager-service-administration.md)합니다.

