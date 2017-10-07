---
title: "aaaUse hello StorSimple 관리자 장치 대시보드 | Microsoft Docs"
description: "Hello StorSimple 관리자 서비스 장치 대시보드 설명 방법과 toouse 것 tooview 저장소 메트릭 및 연결 된 시작자 및 찾기 hello 일련 번호와 IQN 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 6c213969-a385-461f-b698-78ef5b8a79cc
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e213fc0a081c21b9d6b408a3dd845cc93a31e250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-dashboard-in-storsimple-manager-service"></a>StorSimple Manager 서비스에서 사용 하 여 hello 장치 대시보드  

## <a name="overview"></a>개요
hello StorSimple 관리자 장치 대시보드 특정 StorSimple 장치에 대 한 정보의 개요를 제공, 반대로 toohello 서비스 대시보드에서 모든 Microsoft Azure StorSimple 솔루션에 포함 된 hello 장치에 대 한 정보를 제공 합니다.

![장치 대시보드 페이지](./media/storsimple-device-dashboard/StorSimple_DeviceDashbaord1M.png)

hello 대시보드는 다음 정보는 hello를 포함 되어 있습니다.

* **차트 영역** – hello hello 대시보드 위쪽에 hello 차트 영역에 hello 관련 저장소 메트릭을 볼 수 있습니다. 이 차트를 볼 hello 총 기본 저장소 (hello 호스트 tooyour 장치 기록한 데이터의 양)에 대 한 메트릭을 있고 hello 총 클라우드 저장소 시간 동안 장치가 차지 합니다.
  
     이 컨텍스트에서 *주 저장소* hello 호스트에 의해 기록 된 데이터의 총 toohello 참조 하 고 볼륨 유형으로 세분화 될 수 있습니다: *주 저장소 계층* 모두 포함 데이터와 데이터를 로컬로 저장 계층화 된 toohello 클라우드; *기본 저장소에 로컬로 고정* 로컬에 저장 된 데이터만 포함 합니다. *클라우드 저장소*, 다른 손 hello, hello 클라우드에 저장 된 데이터의 총 금액 hello 측정 한 값입니다. 여기에는 계층화된 데이터 및 백업이 포함됩니다. Hello 클라우드에 저장 된 데이터 중복 제거 및 압축 된 경우 기본 저장소 hello hello 데이터가 이전에 사용한 저장소 양을 나타냅니다는 중복 제거 및 압축 된 합니다. (이러한 두 숫자 tooget hello 압축 비율의 관념 비교할 수 있습니다.) 모두 기본에 대 한 및 클라우드 저장소, hello 표시 된 hello 추적 구성한 빈도에 따라 달라 집니다. 예를 들어 1 주일 빈도 선택 하면 hello 차트 hello에 지난 주의 각 날에 대 한 데이터가 표시 됩니다.
  
     다음과 같이 hello 차트를 구성할 수 있습니다.
  
  * 시간, 선택 hello를 통해 사용한 클라우드 저장소의 toosee hello 양을 **클라우드 저장소 사용** 옵션입니다. 선택 hello hello 호스트에 의해 기록 된 toosee hello 총 저장소 **기본 계층으로 계층화 된 저장소 사용** 및 **기본 로컬로 고정 된 저장소 사용 됨** 옵션입니다. Hello 그림에 두 옵션이 선택 되어 있습니다. 따라서 hello 차트는 클라우드 및 기본 저장소의 저장소 용량이 표시 됩니다. 모든 기본 저장소 이전 tooinstalling 업데이트 2를 사용 하는 hello로 표시 됩니다 **기본 계층으로 계층화 된 저장소 사용** 선입니다.
  * Hello 드롭다운 메뉴를 사용 하 여 hello 차트 toospecify 기간 1 주, 1 개월, 3 개월 또는 1 년의 hello 오른쪽 위 모퉁이에 있습니다. 최상위 차트 hello 일 마다 한 번만 새로 고쳐집니다 않으며 반영 됩니다 전날의 총계가 hello 합니다.
    
    자세한 내용은 참조 [사용 하 여 StorSimple 장치를 StorSimple Manager 서비스 toomonitor hello](storsimple-monitor-device.md)합니다.
* **사용 개요** – hello **사용 개요** 영역을 기본 저장소의 용량 hello 사용 되는 hello 크기의 프로 비전 된 저장소 및 장치에 대 한 hello 최대 저장소 용량을 볼 수 있습니다. 이러한 사용 숫자 toohello 최대 양을 사용 가능한 저장소를를 비교 하 여 tooobtain 추가 저장소가 필요한 경우 한 눈에 볼 수 있습니다. 이 개요 15 분 마다 업데이트 됩니다 하, hello 업데이트 빈도의 차이로 인해 나타날 수 있습니다 하는 것 보다 다른 숫자와 같이 hello 차트 영역에 위의 매일 업데이트 되는 note 합니다. 자세한 내용은 참조 [사용 하 여 StorSimple 장치를 StorSimple Manager 서비스 toomonitor hello](storsimple-monitor-device.md)합니다.
* **경고** – hello **경고** 영역에는 장치에 대 한 hello 경고의 개요가 포함 되어 있습니다. 경고 심각도 별로 그룹화 됩니다 하 고 각 심각도 수준의 경고 수가 hello 수 제공 됩니다. 클릭 hello 경고 심각도 hello의 한정된 된 뷰가 열려이 장치에 대 한 해당 심각도 수준의 경고를만 hello 탭 tooshow 경고 합니다.
* **작업** – hello **작업** 최근 작업의 결과 hello 영역 보여 줍니다. Hello 시스템이 예상 대로 작동 하거나 필요한 경우 수정 작업 tootake 있습니다 하도록 할 수 있습니다 확인할 수 있습니다. toosee 최근에 완료 된 작업에 대 한 자세한 내용을 보려면 클릭 **성공한 작업 hello 지난 24 시간 동안**합니다.
* hello **눈에 보는** hello 대시보드 오른쪽의 hello에 영역 장치 모델, 일련 번호, 상태, 설명 및 볼륨 수 등 유용한 정보를 제공 합니다.

장애 조치를 구성 하 고 hello 장치 대시보드에서 연결 된 시작자를 볼 수도 있습니다.

이 페이지에서 수행할 수 있는 일반적인 작업 hello 다음과 같습니다.

* 연결된 초기자 보기
* Hello 장치 일련 번호 찾기
* Hello 장치 대상 IQN 찾기

## <a name="view-connected-initiators"></a>연결된 초기자 보기
Hello를 클릭 하 여 연결 된 tooyour 장치는 hello iSCSI 초기자를 볼 수 있습니다 **연결 된 시작자 보기** hello에 제공 된 링크 **눈에 보는** 장치 대시보드의 영역입니다. 이 페이지를 성공적으로 연결 된 tooyour 장치 hello 초기자의 테이블 형식 목록을 제공 합니다. 각 초기자에 대해 다음을 확인할 수 있습니다.

* hello iSCSI 정규화 된 이름 (IQN) hello의 초기자를 연결 합니다.
* hello 액세스 제어 레코드 (ACR)이 연결 된 시작자를 허용 하의 hello 이름입니다.
* hello의 hello IP 주소는 시작자를 연결합니다.
* hello 네트워크 인터페이스는 hello 초기자가 연결 된 tooon 저장 장치입니다. 이러한 0 tooDATA 5 데이터에서 범위 수 있습니다.
* 연결 된 시작자 hello 모든 hello 볼륨 tooaccess toohello 현재 ACR 구성에 따라 허용 됩니다.

이 목록에 예기치 않은 시작 자가 하거나 hello를 예상 하는 스토리 나타나지 않는 경우 해당 ACR 구성을 확인 합니다. 최대 512 개의 초기자 tooyour 장치를 연결할 수 있습니다.

## <a name="find-hello-device-serial-number"></a>Hello 장치 일련 번호 찾기
Hello 장치에서 Microsoft 다중 경로 I/O (MPIO)를 구성할 때 hello 장치 일련 번호를 할 수 있습니다. Hello 단계 toofind hello 장치 일련 번호를 다음을 수행 합니다.

#### <a name="toofind-hello-device-serial-number"></a>toofind hello 장치 일련 번호
1. 너무 이동**장치** > **대시보드**합니다.
2. Hello 대시보드의 hello 오른쪽 창에서 찾을 hello **눈에 보는** 영역입니다.
3. 아래로 스크롤하여 hello 일련 번호를 찾습니다.

## <a name="find-hello-device-target-iqn"></a>Hello 장치 대상 IQN 찾기
StorSimple 장치에서 hello Challenge Handshake 인증 프로토콜 CHAP ()를 구성할 때 hello 장치 대상 IQN을 할 수 있습니다. Hello 단계 toofind hello 장치 대상 IQN 다음을 수행 합니다.

### <a name="toofind-hello-device-target-iqn"></a>toofind hello 장치 대상 IQN
1. 너무 이동**장치** > **대시보드**합니다.
2. Hello 대시보드의 hello 오른쪽 창에서 찾을 hello **눈에 보는** 영역입니다.
3. 아래로 스크롤하여 hello 대상 IQN을 찾습니다.

## <a name="next-steps"></a>다음 단계
* Hello에 대 한 자세한 [StorSimple Manager 서비스 대시보드](storsimple-service-dashboard.md)합니다.
* 에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple Manager 서비스 tooadminister를 hello를 사용 하 여](storsimple-manager-service-administration.md)합니다.

