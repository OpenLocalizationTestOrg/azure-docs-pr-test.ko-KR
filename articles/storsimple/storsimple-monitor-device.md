---
title: "aaaMonitor StorSimple 장치 | Microsoft Docs"
description: "StorSimple Manager 서비스 toomonitor I/O 성능, 용량 사용률, 네트워크 처리량 및 장치 성능 toouse hello 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: bd4f7704-4f6f-47d0-927a-b1c91eabc453
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/16/2016
ms.author: alkohli
ms.openlocfilehash: c1f614a7f52728650bfadb3335435b8b5a17e6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomonitor-your-storsimple-device"></a>StorSimple 장치의 StorSimple Manager 서비스 toomonitor hello를 사용 하 여
## <a name="overview"></a>개요
StorSimple 솔루션 내에서 hello toomonitor 특정 장치의 StorSimple Manager 서비스를 사용할 수 있습니다. I/O 성능, 용량 사용률, 네트워크 처리량 및 장치 성능 메트릭을 기준으로 사용자 지정 차트를 만들 수 있습니다. 

tooview hello hello Azure 클래식 포털 선택 hello StorSimple Manager 서비스에서에서 특정 장치에 대 한 정보를 모니터링 합니다. Hello 클릭 **모니터** 탭 한 다음 장치 hello 목록에서 선택 합니다. hello **모니터** 페이지 hello 다음 정보를 포함 합니다.

## <a name="io-performance"></a>I/O 성능
**I/O 성능** 메트릭을 추적 관련 읽기 toohello 번호 및에서 쓰기 작업 간에 어느 hello iSCSI 시작자 인터페이스 hello 호스트 서버 및 hello 장치 또는 hello 장치와 hello 클라우드입니다. 이 성능은 특정 볼륨, 특정 볼륨 컨테이너 또는 모든 볼륨 컨테이너에 대해 측정될 수 있습니다.

아래 hello 차트 프로덕션 장치에 대 한 모든 hello 볼륨에 대 한 hello 초기자 tooyour 장치에 대 한 hello I/O를 보여 줍니다. hello 메트릭을 그릴은 읽기 및 쓰기 바이트 수 / 초, 읽기 및 쓰기 초당 IO 작업 및 읽기 및 쓰기 대기 시간이 짧습니다.

![초기자 toodevice 한 IO 성능](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_InitiatorTODevice_For_AllVolumesM.png)

Hello에 대 한 동일한 장치, 모든 볼륨 컨테이너를 hello에 대 한 hello 장치 toohello 클라우드에서 hello 데이터에 대 한 hello I/O 작업이 표시 됩니다. 이 장치에서 hello 데이터는 hello 선형 계층만 있고 toohello 클라우드 유출 nothing입니다. 장치 toohello 클라우드에서 발생 읽기 / 쓰기 작업이 없습니다. 따라서 hello 최대치 hello 차트에서 해당 하는 hello 하트 비트 hello 장치와 hello 서비스 간에 확인란이 toohello 빈도 5 분의 간격에 않습니다. 

![장치 toocloud 한 IO 성능](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_DeviceTOCloud_For_AllVolumeContainersM.png)

Hello 동일한 장치, 클라우드 스냅숏은 수행 되었으나 오후 2시 시작 하는 볼륨 데이터에 대 한에. 이 hello 장치 toohello 클라우드에서 흐르는 데이터에서 발생 했습니다. 읽기 / 쓰기를이 기간 동안 toohello 클라우드를 제공 했습니다. hello IO 차트 표시에 최고를 기록 hello에 해당 하는 다양 한 메트릭이 hello 스냅숏을 만들 때 toohello 시간입니다. 

![클라우드 스냅숏 후 장치 toocloud에 대 한 IO 성능](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_DeviceTOCloud_For_AllVolumeContainers2M.png)

## <a name="capacity-utilization"></a>용량 사용률
**용량 사용률** hello 볼륨, 볼륨 컨테이너 또는 장치에서 사용 되는 데이터 저장 공간의 양을 메트릭 관련된 toohello 트랙입니다. 주 저장소, 클라우드 저장소, 또는 장치 저장소의 용량 사용률을 hello 기반으로 보고서를 만들 수 있습니다. 용량 사용률은 특정 볼륨, 특정 볼륨 컨테이너 또는 모든 볼륨 컨테이너에 대해 측정될 수 있습니다.

기본 hello, 클라우드 및 장치 저장소 용량 다음과 같이 설명할 수 있습니다.

### <a name="primary-storage-capacity-utilization"></a>기본 저장소 용량 사용률
이러한 차트 hello hello 데이터 중복 제거 되 고 압축 되기 전에 tooStorSimple 볼륨을 기록 하는 데이터 양을 보여 줍니다. 모든 볼륨 또는 단일 볼륨에 대 한 hello 기본 저장소 사용률을 볼 수 있습니다.

두 경우 모두 각 개별 볼륨 hello 및 hello 기본 데이터를 합계에 대 한 모든 볼륨에 대 한 hello 기본 저장소 볼륨 용량 사용률 차트를 볼 때에 hello 두 숫자 사이의 불일치로 나타날 수 있습니다. 모든 볼륨의 총 기본 데이터 hello toohello hello hello 개별 볼륨의 기본 데이터의 총 합계를 추가할 수 없습니다. 때문일 수 있으므로 tooone hello 다음 중:

* **모든 볼륨에 대해 포함된 스냅숏 데이터**: 이 동작은 업데이트 3 이전 버전을 실행하는 경우에만 나타납니다. hello 모든 hello 볼륨에 대해 표시 되는 기본 데이터에는 각 볼륨에 대 한 hello 주 데이터 및 hello 스냅숏 데이터 hello 합계입니다. 지정된 된 볼륨에 대해 표시 된 hello 주 데이터 tooonly hello 양을 hello 볼륨에 할당 된 데이터를 해당 (하 고 hello 해당 볼륨 스냅숏 데이터를 포함 하지 않습니다).
  
    이 hello 다음 수식으로도 설명할 수 있습니다.
  
    *Primary data (All volumes) = Sum of (Primary data (volume i) + Size of snapshot data (volume i))*
  
    *where, 기본 데이터 (볼륨 i)의 할당 된 기본 데이터 toovolume 크기 = i*
  
    Hello 서비스를 통해 hello 스냅숏이 삭제 되 면 hello 삭제 hello 백그라운드에서 비동기적으로 수행 됩니다. Hello 볼륨 데이터 크기 toobe hello 스냅숏 삭제 하는 다음 업데이트에 대 한 다소 시간이 걸릴 수 있습니다. 
  
    업데이트를 3 이상을 실행 하는 경우 hello 스냅숏 데이터 hello 볼륨 데이터에 포함 되지 않습니다. 및 hello 기본 사용률은 다음과 같이 계산 됩니다.
  
    *Primary data (All volumes) = Sum of (Primary data (volume i)
  
    *where, 기본 데이터 (볼륨 i)의 할당 된 기본 데이터 toovolume 크기 = i*
* **모든 볼륨에 포함 된 모니터링 사용 하지 않도록 설정 된 볼륨**:는 대 한 모니터링이 해제 장치에서 볼륨을 설정한 경우 이러한 개별 볼륨에 대 한 데이터를 모니터링 하는 hello 제공 됩니다 hello 막대형 차트에서입니다. 그러나 hello 차트에서 모든 볼륨에 대 한 hello 데이터 포함 hello 볼륨을 모니터링이 해제 됩니다. 
* **모든 볼륨에 대해 포함 하는 라이브 연결 된 백업을 사용 하 여 볼륨을 삭제**: 스냅숏 데이터를 포함 하는 볼륨을 삭제는 않지만 hello 연결 된 스냅숏이 여전히 존재 경우 불일치로 표시 될 수 있습니다.
* **모든 볼륨에 대해 포함된 볼륨이 삭제됨**: 일부 경우 구 볼륨이 삭제 후에도 존재할 수 있습니다. 삭제가 hello 효과 표시 되지 않습니다 및 hello 장치 낮은 사용 가능한 용량을 표시할 수 있습니다. 이러한 볼륨 toocontact Microsoft 지원 tooremove 필요합니다.

hello 다음 차트 표시 클라우드 스냅숏을 만든 후 및 하기 전에 StorSimple 장치의 기본 저장소 용량 사용률이 hello 합니다. 볼륨 데이터만 그대로 클라우드 스냅숏 hello 주 저장소를 변경 하지 마십시오. 볼 수 있듯이 hello 차트 hello 기본 용량 사용률이 클라우드 스냅숏을 만드는 결과로 아무런 차이가 표시 됩니다. hello 클라우드 스냅숏 약 오후 2 시 00 분 해당 장치에서 시작 합니다.

![클라우드 스냅숏 전 기본 용량 사용률](./media/storsimple-monitor-device/StorSimple_PrimaryCapacityUtil_For_AllVolumes2M.png)

![클라우드 스냅숏 후 기본 용량 사용률](./media/storsimple-monitor-device/StorSimple_PrimaryCapacityUtil_For_AllVolumes1M.png)

실행 하는 경우 2를 업데이트 하거나 이상 나눌 수 있습니다 hello 주 저장소 용량 사용률이 개별 볼륨, 모든 볼륨을 계층화 된 볼륨을 모두 및 모든 로컬 고정된 볼륨에서 다음과 같이 합니다. 모든 로컬로 고정 된 볼륨을 하면 별로 분석 tooquickly 모두 사용 hello 로컬 계층의 양을 확인 합니다.

![모든 로컬 고정 볼륨에 대한 기본 용량 사용률](./media/storsimple-monitor-device/localvolumes.png)

### <a name="cloud-storage-capacity-utilization"></a>클라우드 저장소 용량 사용률
이러한 차트 hello 양을 클라우드 저장소 사용을 보여 줍니다. 이 데이터는 중복 제거되고 압축됩니다. 이 양에는 모든 기본 볼륨에 반영되지 않으며 레거시 또는 필수 보존 목적을 위해 유지되는 데이터를 포함할 수 있는 클라우드 스냅숏이 포함되어 있습니다. Hello 번호 정확한 수 없지만 기본 hello 및 클라우드 저장소 소비 수치 tooget hello 데이터 감소의 예측 등급을 비교할 수 있습니다. hello 다음 차트 표시 하기 전에 StorSimple 장치의 및 클라우드 스냅숏을 만든 후 hello 클라우드 저장소 용량 사용률이 됩니다. hello 클라우드 스냅숏 시작에 약 2시 pm 해당 장치에 보 이죠 hello 클라우드 용량 사용률에 촬영 hello 동일 5.73 MB too4.04 GB에서에서 증가 시간입니다.

![클라우드 스냅숏 전 클라우드 용량 사용률](./media/storsimple-monitor-device/StorSimple_CloudCapacityUtil_For_AllVolumeContainers2M.png)

![클라우드 스냅숏 후 클라우드 용량 사용률](./media/storsimple-monitor-device/StorSimple_CloudCapacityUtil_For_AllVolumeContainers1M.png)

### <a name="device-storage-capacity-utilization"></a>장치 저장소 용량 사용률
이러한 차트는 hello 보다 더 큽니다 기본 저장소 사용률 hello SSD 선형 계층을 포함 하기 때문에 hello 장치에 대 한 총 사용률을 보여 줍니다. 이 계층에도 있는 hello 다른 계층에 장치의 데이터를 포함 합니다. hello 이전 데이터를 이동된 toohello HDD 계층 (이때 것은 중복 제거 및 압축 된) 및 이후에 toohello 클라우드 내에 새 데이터가 들어오면 있도록 hello 용량 hello SSD 선형 계층에 유지 됩니다.

시간이 지남에 따라 기본 용량 사용률 및 장치 용량 사용률을 향상 시킵니다 함께 hello 데이터 toobe 시작 될 때까지 toohello 클라우드 계층입니다. 해당 시점에 hello 장치 용량 사용률 tooplateau, 시작할 하지만 더 많은 데이터를 기록할 때 hello 기본 용량 사용률 증가 합니다.

hello 다음 차트 표시 클라우드 스냅숏을 만든 후 및 하기 전에 StorSimple 장치의 기본 저장소 용량 사용률이 hello 합니다. hello 클라우드 스냅숏 2시 pm에 시작 하 고 hello 장치 용량 사용률을 줄이면 당시에 시작 됩니다. hello 장치 저장소 용량 사용률이 11.58 GB too7.48 GB에서에서 다운 되었습니다. 이 가능성이 hello hello 선형 SSD 계층에 압축 되지 않은 데이터 중복 제거 된, 압축 못하고 나타냅니다 hello HDD 계층으로 이동 합니다. 참고는 hello 장치에 많은 양의 hello SSD 및 HDD 계층 데이터를 이미 있으면 나타나지 않을 수 있습니다이 감소 합니다. 이 예제에서는 hello 장치 적은 양의 데이터에 있습니다.

![클라우드 스냅숏 전 장치 용량 사용률](./media/storsimple-monitor-device/StorSimple_DeviceCapacityUtil2M.png)

![클라우드 스냅숏 후 장치 용량 사용률](./media/storsimple-monitor-device/StorSimple_DeviceCapacityUtil1M.png)

## <a name="network-throughput"></a>네트워크 처리량
**그 결과 네트워크 처리량** hello iSCSI 초기자 네트워크 인터페이스 hello 호스트 서버와 hello 장치 및 hello 장치와 hello 클라우드 간에 전송 되는 데이터 양을 메트릭 관련된 toohello 트랙입니다. 장치에서 각 hello iSCSI 네트워크 인터페이스에 대해이 메트릭을 모니터링할 수 있습니다.

hello hello Data 0 및 Data 4 장치에서 모두 1 GbE 네트워크 인터페이스에 대 한 표시 hello 네트워크 처리량 차트를 수행 합니다. 이 경우 데이터 0은 클라우드를 사용하고 데이터 4는 iSCSI를 사용합니다. 인바운드 및 아웃 바운드 트래픽을 StorSimple 장치에 대 한 hello 두 hello를 볼 수 있습니다. hello 일직선 3시 24분 pm에서 시작 하는 hello 차트에는에서는 5 분 마다 데이터를 수집 및 무시 해야 toohello 팩트 소유 하 고 있는 합니다. 

![Data4에 대한 네트워크 처리량](./media/storsimple-monitor-device/StorSimple_NetworkThroughput_Data0M.png)

![Data4에 대한 네트워크 처리량](./media/storsimple-monitor-device/StorSimple_NetworkThroughput_Data4M.png)

## <a name="device-performance"></a>장치 성능
**장치 성능** 메트릭을 추적 관련 장치의 toohello 성능입니다. hello 다음 차트에서는 장치에 대 한 CPU 사용률 통계 hello 프로덕션.

![장치의 CPU 사용률](./media/storsimple-monitor-device/StorSimple_DeviceMonitor_DevicePerformance1M.png)

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[hello StorSimple 관리자 서비스 장치 대시보드를 사용 하 여](storsimple-device-dashboard.md)합니다.
* 너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple Manager 서비스 tooadminister hello](storsimple-manager-service-administration.md)합니다.

