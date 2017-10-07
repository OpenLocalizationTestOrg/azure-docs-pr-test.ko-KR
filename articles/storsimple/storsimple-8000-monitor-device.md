---
title: "aaaMonitor StorSimple 8000 시리즈 장치 | Microsoft Docs"
description: "StorSimple 장치 관리자 toouse hello toomonitor 사용량, I/O 성능 및 용량 사용률을 서비스 하는 방법을 설명 합니다."
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
ms.date: 08/02/2017
ms.author: alkohli
ms.openlocfilehash: 092dab8dd301c50fc12316b4031a8d1b34fab876
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomonitor-your-storsimple-device"></a>StorSimple 장치의 StorSimple 장치 관리자 서비스 toomonitor hello를 사용 하 여
## <a name="overview"></a>개요
StorSimple 솔루션 내에서 hello toomonitor 특정 장치 StorSimple 장치 관리자 서비스를 사용할 수 있습니다. I/O 성능, 용량 사용률, 네트워크 처리량 및 장치 성능 메트릭을 기준으로 하는 사용자 지정 차트를 만들고 해당 toohello 대시보드에 고정할 수 있습니다. 자세한 내용은 이동 너무[포털 대시보드를 사용자 지정할](/articles/azure-portal/azure-portal-dashboards.md)합니다.

hello tooview hello Azure 포털에서에서 특정 장치에 대 한 모니터링 정보가 hello StorSimple 장치 관리자 서비스를 선택 합니다. Hello 장치 목록에서 장치를 선택 하 고 이동 하 여 너무**모니터**합니다. Hello 확인할 수 있습니다 **용량**, **사용량**, 및 **성능** hello 선택한 장치에 대 한 차트입니다.

## <a name="capacity"></a>용량
**용량** 트랙 hello hello 장치에 남아 있는 hello 공간과 프로 비전 된 공간입니다. 남은 용량 hello 로컬로 고정 또는 계층으로 표시 됩니다.

hello를 프로 비전 된 디스크 크기 및 남은 용량 계층화 된 볼륨과 로컬로 고정 된 볼륨으로 구분 추가 됩니다. 각 볼륨에 대 한 hello 용량을 프로 비전 하 고 용량 hello 장치에 남아 있는 hello 표시 됩니다.

![IO 수용작업량](./media/storsimple-8000-monitor-device/device-capacity.png)



## <a name="usage"></a>사용
**사용 현황** hello 볼륨, 볼륨 컨테이너 또는 장치에서 사용 되는 데이터 저장 공간의 양을 메트릭 관련된 toohello 트랙입니다. 주 저장소, 클라우드 저장소, 또는 장치 저장소의 용량 사용률을 hello 기반으로 보고서를 만들 수 있습니다. 용량 사용률은 특정 볼륨, 특정 볼륨 컨테이너 또는 모든 볼륨 컨테이너에 대해 측정될 수 있습니다.
기본적으로 지난 24 시간에 대 한 hello 사용이 보고 됩니다. Hello 차트 toochange hello 기간은 hello를 통해 사용량이에서 선택 하 여 보고 편집할 수 있습니다.
* 지난 24시간
* 지난 7일간
* 지난 30일간
* 지난 90일간
* 지난해


기본 hello, 클라우드 및 사용 하는 로컬 저장소를 다음과 같이 설명할 수 있습니다.

### <a name="primary-storage-usage"></a>기본 저장소 사용량
이러한 차트 hello hello 데이터 중복 제거 되 고 압축 되기 전에 tooStorSimple 볼륨을 기록 하는 데이터 양을 보여 줍니다. 단일 볼륨 또는 볼륨 컨테이너에서 모든 볼륨에서 사용 하는 hello 주 저장소를 볼 수 있습니다. hello 기본 저장소 사용은 더 이상 기본 계층화 된 저장소 사용 되며 기본 로컬로 고정 된 저장소를 사용 하 여 나누어집니다.

hello 다음 차트 표시 하는 사용 하기 전에 StorSimple 장치의 클라우드 스냅숏을 만든 후 hello 기본 저장소입니다. 볼륨 데이터만 그대로 클라우드 스냅숏 hello 주 저장소를 변경 하지 마십시오. 알 수 없는 차이에 따라 hello 기본 계층 구성 또는 로컬로 고정 된 클라우드 스냅숏을 만드는 결과로 사용 hello 차트에 표시 됩니다. hello 클라우드 스냅숏 약 오후 11 시 50 분 해당 장치에서 시작 합니다.

![클라우드 스냅숏 후 기본 용량 사용률](./media/storsimple-8000-monitor-device/device-primary-storage-after-cloudsnapshot.png)

이제 hello 연결 호스트 tooyour StorSimple 장치에서 IO를 실행, 기본 계층화 된 저장소의 증가로 나타납니다 또는 기본 로컬 저장소 사용에 따라 고정 된 경우 계층 이동해 왔거나 로컬로 고정 볼륨에 있습니다 hello 데이터를 쓸 합니다. StorSimple 장치에 대 한 hello 기본 저장소 사용 차트는 다음과 같습니다. 이 장치에서 시작을 처리 하는 hello StorSimple 호스트 약 오후 2 시 30 분 hello 장치에 계층화 된 볼륨에 씁니다. Hello 쓰기 바이트/s toohello IO hello 호스트에서 실행 중에 해당 hello 피크를 볼 수 있습니다.

![계층화된 볼륨에서 IO를 실행 중인 경우 성능](./media/storsimple-8000-monitor-device/device-io-from-initiator.png)

Hello 기본 계층화 된 저장소를 사용 하는 수 만큼 로컬로 고정 hello 기본 사용 현황 변하지 않습니다 반면를 내려갔습니다를 보면 없습니다 쓰기 hello 장치에서 로컬로 고정 toohello 볼륨을 처리 합니다.

![계층화된 볼륨에서 IO를 실행 중인 경우 기본 수용작업량 사용률](./media/storsimple-8000-monitor-device/device-primary-storage-io-from-initiator.png)

실행 하는 경우 3를 업데이트 하거나 이상 나눌 수 있습니다 hello 주 저장소 용량 사용률이 개별 볼륨, 모든 볼륨을 계층화 된 볼륨을 모두 및 모든 로컬 고정된 볼륨에서 다음과 같이 합니다. 모든 로컬로 고정 된 볼륨을 하면 별로 분석 tooquickly 모두 사용 hello 로컬 계층의 양을 확인 합니다.

![모든 계층화된 볼륨에 대한 기본 수용작업량 사용률](./media/storsimple-8000-monitor-device/monitor-usage3.png)

![모든 로컬 고정 볼륨에 대한 기본 용량 사용률](./media/storsimple-8000-monitor-device/monitor-usage4.png)

하면 더욱의 hello 볼륨 hello 목록에서 클릭 하 고 hello 해당 사용법을 참조 하십시오.

![모든 로컬 고정 볼륨에 대한 기본 용량 사용률](./media/storsimple-8000-monitor-device/device-primary-storage-usage-by-volume.png)

### <a name="cloud-storage-usage"></a>클라우드 저장소 사용량
이러한 차트 hello 양을 클라우드 저장소 사용을 보여 줍니다. 이 데이터는 중복 제거되고 압축됩니다. 이 양에는 모든 기본 볼륨에 반영되지 않으며 레거시 또는 필수 보존 목적을 위해 유지되는 데이터를 포함할 수 있는 클라우드 스냅숏이 포함되어 있습니다. Hello 번호 정확한 수 없지만 기본 hello 및 클라우드 저장소 소비 수치 tooget hello 데이터 감소의 예측 등급을 비교할 수 있습니다.

hello 다음 차트 표시 hello 클라우드 저장소 사용 StorSimple 장치의 클라우드 스냅숏을 만들 때.

* hello 클라우드 스냅숏 약 오전 11시 50분 해당 장치에에서 시작 하 고 hello 클라우드 스냅숏 전에 볼 수 없는 클라우드 저장소를 사용 했습니다. 
* 한 번 hello 클라우드 스냅숏 완료, hello 클라우드 저장소 사용률 샷 0.89 GB를 합니다. 
* Hello 클라우드 스냅숏 진행 중인 동안에 없는 경우 또한 해당 최대 장치 toocloud에서 IO hello

    ![클라우드 스냅숏 이전 클라우드 저장소 사용률](./media/storsimple-8000-monitor-device/device-cloud-storage-before-cloudsnapshot.png)

    ![클라우드 스냅숏 이후 클라우드 저장소 사용률](./media/storsimple-8000-monitor-device/device-cloud-storage-after-cloudsnapshot.png)

    ![클라우드 스냅숏 중 장치 toocloud에서 IO](./media/storsimple-8000-monitor-device/device-io-to-cloud-during-cloudsnapshot.png)


### <a name="local-storage-usage"></a>로컬 저장소 사용량
이러한 차트는 hello 보다 더 큽니다 기본 저장소 사용량 hello SSD 선형 계층을 포함 하기 때문에 hello 장치에 대 한 총 사용률을 보여 줍니다. 이 계층에도 있는 hello 다른 계층에 장치의 데이터를 포함 합니다. hello 이전 데이터를 이동된 toohello HDD 계층 (이때 것은 중복 제거 및 압축 된) 및 이후에 toohello 클라우드 내에 새 데이터가 들어오면 있도록 hello 용량 hello SSD 선형 계층에 유지 됩니다.

시간이 지남에 따라 사용 되는 및 로컬 저장소 사용 향상 시킵니다 함께 hello 데이터 toobe 시작 될 때까지 주 저장소 toohello 클라우드를 계층입니다. 해당 시점에 사용 하는 hello 로컬 저장소 tooplateau, 시작 아마도 하지만 더 많은 데이터를 기록할 때 사용 된 hello 기본 저장소 증가 합니다.

hello 다음 차트 표시 hello 기본 저장소 클라우드 스냅숏을 만들 때 StorSimple 장치에 사용 됩니다. hello 클라우드 스냅숏 오전 11시 50분에 시작 하 고 hello 로컬 저장소 감소 해당 시간에 시작 됩니다. 1.445 GB too1.09 GB에서에서 떨어졌다 hello 로컬 저장소를 사용 합니다. 이 가능성이 hello hello 선형 SSD 계층에 압축 되지 않은 데이터 중복 제거 된, 압축 못하고 나타냅니다 hello HDD 계층으로 이동 합니다. 참고는 hello 장치에 많은 양의 hello SSD 및 HDD 계층 데이터를 이미 있으면 나타나지 않을 수 있습니다이 감소 합니다. 이 예제에서는 hello 장치 적은 양의 데이터에 있습니다.

![클라우드 스냅숏 이후 로컬 저장소 사용률](./media/storsimple-8000-monitor-device/device-local-storage-after-cloudsnapshot.png)

## <a name="performance"></a>성능
**성능** 메트릭을 추적 관련 읽기 toohello 번호 및에서 쓰기 작업 간에 어느 hello iSCSI 시작자 인터페이스 hello 호스트 서버 및 hello 장치 또는 hello 장치와 hello 클라우드입니다. 이 성능은 특정 볼륨, 특정 볼륨 컨테이너 또는 모든 볼륨 컨테이너에 대해 측정될 수 있습니다. 성능 및도 포함 되어 CPU 사용률 hello에 대 한 네트워크 처리량 장치에서 다양 한 네트워크 인터페이스.

### <a name="io-performance-for-initiator-toodevice"></a>초기자 toodevice에 대 한 I/O 성능
아래 hello 차트 프로덕션 장치에 대 한 모든 hello 볼륨에 대 한 hello 초기자 tooyour 장치에 대 한 hello I/O를 보여 줍니다. hello 메트릭을 그릴 읽고 초당 바이트 수를 작성 합니다. 또한 읽기, 쓰기 및 미해결 IO 또는 읽기 및 쓰기 대기 시간을 차트로 만들 수 있습니다.

![초기자 toodevice에 대 한 IO 성능](./media/storsimple-8000-monitor-device/device-io-from-initiator.png)

### <a name="io-performance-for-device-toocloud"></a>장치 toocloud에 대 한 I/O 성능
Hello에 대 한 동일한 장치, 모든 볼륨 컨테이너를 hello에 대 한 hello 장치 toohello 클라우드에서 hello 데이터에 대 한 hello I/O 작업이 표시 됩니다. 이 장치에서 hello 데이터는 hello 선형 계층만 있고 toohello 클라우드 유출 nothing입니다. 장치 toohello 클라우드에서 발생 읽기 / 쓰기 작업이 없습니다. 따라서 hello 최대치 hello 차트에서 해당 하는 hello 하트 비트 hello 장치와 hello 서비스 간에 확인란이 toohello 빈도 5 분의 간격에 않습니다.

Hello 동일한 장치, 클라우드 스냅숏은 수행 되었으나 오전 11시 50분에서 시작 하는 볼륨 데이터에 대 한에. 이 hello 장치 toohello 클라우드에서 흐르는 데이터에서 발생 했습니다. 이 기간 동안 기록 된 toohello 클라우드를 제공 됩니다. hello IO 차트 hello 쓰기 바이트/s 해당 toohello 시간 hello 스냅숏을 만들 때에 최고를 표시 됩니다.

![클라우드 스냅숏 중 장치 toocloud에서 IO](./media/storsimple-8000-monitor-device/device-io-to-cloud-during-cloudsnapshot.png)

### <a name="network-throughput-for-device-network-interfaces"></a>장치 네트워크 인터페이스의 네트워크 처리량
**그 결과 네트워크 처리량** hello iSCSI 초기자 네트워크 인터페이스 hello 호스트 서버와 hello 장치 및 hello 장치와 hello 클라우드 간에 전송 되는 데이터 양을 메트릭 관련된 toohello 트랙입니다. 장치에서 각 hello iSCSI 네트워크 인터페이스에 대해이 메트릭을 모니터링할 수 있습니다.

GbE 네트워크 모두 클라우드 사용 (기본값)가 사용자의 장치에 Data 0, 1 1 hello에 대 한 차트 표시 hello 네트워크 처리량 다음 hello 및 iSCSI를 지원 합니다. 약 9 오후 6 월 14에이 장치에 대해 toohello 클라우드를 제공 하는 IO 했으며 hello 클라우드 (에 스냅숏이 만들어진 지점 tootiering 되는 시간 없음 클라우드 hello 클라우드로 메커니즘 toomove hello 데이터 hello)로 데이터 계층이 되었습니다. 에 없는 경우 해당 최대 hello 네트워크 처리량 그래프에 대 한 hello 시간과 대부분의 hello 네트워크 트래픽이 동일한 아웃 바운드 toohello 클라우드

![Data 0에 대한 네트워크 처리량](./media/storsimple-8000-monitor-device/device-network-throughput-data0.png)

Data 1 hello 인터페이스 처리량 차트를 보면 다른 1 GbE 네트워크 인터페이스를만 iSCSI를 사용 후이 기간 동안 네트워크 트래픽이 없음 거의 없었습니다.

![Data 1에 대한 네트워크 처리량](./media/storsimple-8000-monitor-device/device-network-throughput-data1.png)


## <a name="cpu-utilization-for-device"></a>장치의 CPU 사용률
**CPU 사용률** toohello CPU 사용률 장치에서을 관련 된 메트릭을 추적 합니다. hello 다음 차트에서는 장치에 대 한 CPU 사용률 통계 hello 프로덕션.

![장치의 CPU 사용률](./media/storsimple-8000-monitor-device/device-cpu-utilization.png)



## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[hello StorSimple 장치 관리자 서비스 장치 대시보드를 사용 하 여](storsimple-device-dashboard.md)합니다.
* 너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-manager-service-administration.md)합니다.

