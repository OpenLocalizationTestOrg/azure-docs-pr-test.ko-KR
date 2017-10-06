---
title: "aaaStorSimple 8000 시리즈 시스템 한계 | Microsoft Docs"
description: "StorSimple 8000 시리즈 구성 요소 및 연결에 대한 시스템 제한 및 권장 크기에 대해 설명합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: c7392678-0924-46c6-9c59-1665cb9b6586
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/28/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: def89a2c1d0ddc71f1743e592c5112b09d72e971
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-storsimple-8000-series-system-limits"></a>StorSimple 8000 시리즈 시스템 제한이란?

## <a name="overview"></a>개요

StorSimple는 데이터 센터에 대해 확장 가능하고 유연한 저장소를 제공합니다. 그러나 StorSimple 솔루션의 계획, 배포 및 작동 시 염두에 두어야 하는 일부 제한 사항이 있습니다. hello 다음 표에서 이러한 한도 및 StorSimple 솔루션에서 가장 hello를 얻을 수 있도록 몇 가지 권장 사항을 제공 합니다.

| 제한 식별자 | 제한 | 설명 |
| --- | --- | --- |
| 저장소 계정 자격 증명의 최대 수 |64 | |
| 볼륨 컨테이너의 최대 수 |64 | |
| 최대 볼륨 수 |255 | |
| 로컬로 고정된 볼륨의 최대 수 |32 | |
| 대역폭 템플릿당 일정의 최대 수 |168 |매시간, 매일 hello 주 (7 * 24)에 대 한 일정입니다. |
| 물리적 장치의 계층화된 볼륨 최대 크기 |8100 및 8600의 경우 64TB |8100과 8600은 물리적 장치입니다. |
| Azure 내 가상 장치의 계층화된 볼륨 최대 크기 |8010의 경우 30TB <br></br> 8020의 경우 64TB |8010과 8020은 각각 표준 저장소와 프리미엄 저장소를 사용하는 Azure의 가상 장치입니다. |
| 물리적 장치의 로컬로 고정된 볼륨 최대 크기 |8100의 경우 8.5TB <br></br> 8600의 경우 22.5TB |8100과 8600은 물리적 장치입니다. |
| iSCSI 연결의 최대 수 |512 | |
| 초기자에서 iSCSI 연결의 최대 수 |512 | |
| 장치당 액세스 제어 레코드의 최대 수 |64 | |
| 백업 정책당 볼륨의 최대 수 |20 | |
| 일정당 유지된 백업의 최대 수(백업 정책에서) |64 | |
| 백업 정책당 일정의 최대 수 |10 | |
| 볼륨당 유지할 수 있는 모든 형식의 최대 스냅숏 수 |256 |이 숫자에는 로컬 스냅숏과 클라우드 스냅숏이 포함됩니다. |
| 어느 장치에나 표시할 수 있는 최대 스냅숏 수 |10000 | |
| 백업, 복원 또는 복제를 위해 병렬로 처리할 수 있는 최대 볼륨 수 |16 |<ul><li>볼륨이 16개를 초과하는 경우, 처리 중인 슬롯을 사용할 수 있게 되면 순차적으로 처리됩니다.</li><li>복제는 새 백업 또는 복원 된 계층화 된 볼륨 hello 작업이 완료 될 때까지 발생할 수 없습니다. 그러나 로컬 볼륨에 대 한 hello 볼륨이 온라인 상태가 된 후 백업은 허용 됩니다.</li></ul> |
| 계층화된 볼륨의 복원 및 복제 복구 시간 |2분 미만 |<ul><li>hello 볼륨은 hello 볼륨 크기에 관계 없이 복원 또는 복제 작업의 2 분 이내 사용할 수 있습니다.</li><li>hello 볼륨 성능은 처음 hello 데이터 및 메타 데이터의 대부분 여전히 hello 클라우드에 있으므로 일반적인 경우 보다 낮을 수 있습니다. Hello 클라우드 toohello StorSimple 장치에서 데이터 흐름에 따라 높아질 수 있습니다.</li><li>hello 총 시간 toodownload 메타 데이터는 hello 할당 볼륨 크기에 따라 달라 집니다. 메타 데이터는 자동 할당 된 볼륨 데이터 1TB 당 5 분의 hello 속도로 hello 백그라운드에서 hello 장치도 전송 됩니다. 이 속도 인터넷 대역폭 toohello 클라우드에서 달라질 수 있습니다.</li><li>복원 hello 또는 hello 장치에 모든 hello 메타 데이터가 있으면 복제 작업이 완료 되었습니다.</li><li>Hello 복원 될 때까지 백업 작업을 수행할 수 없습니다 또는 복제 작업이 완전히 완료 되었습니다. |
| 로컬로 고정된 볼륨의 복원 복구 시간 |2분 미만 |<ul><li>hello 볼륨은 hello 볼륨 크기에 관계 없이 hello 복원 작업의 2 분 이내 사용할 수 있습니다.</li><li>hello 볼륨 성능은 처음 hello 데이터 및 메타 데이터의 대부분 여전히 hello 클라우드에 있으므로 일반적인 경우 보다 낮을 수 있습니다. Hello 클라우드 toohello StorSimple 장치에서 데이터 흐름에 따라 높아질 수 있습니다.</li><li>hello 총 시간 toodownload 메타 데이터는 hello 할당 볼륨 크기에 따라 달라 집니다. 메타 데이터는 자동 할당 된 볼륨 데이터 1TB 당 5 분의 hello 속도로 hello 백그라운드에서 hello 장치도 전송 됩니다. 이 속도 인터넷 대역폭 toohello 클라우드에서 달라질 수 있습니다.</li><li>로컬로 고정 된 볼륨을 계층화 된 볼륨 달리 hello 볼륨 데이터를 hello 장치에서 로컬로 다운로드도 합니다. 모든 hello 볼륨 데이터 toohello 장치 하 상태가 될 때 hello 복원 작업이 완료 되었습니다.</li><li>hello 복원 작업 걸릴 수 있습니다. hello 총 시간 toocomplete hello 복원 hello 프로 비전 로컬 볼륨, 인터넷 대역폭 및 hello hello 장치에서 기존 데이터의 hello 크기에 따라 달라 집니다. Hello 복원 작업이 진행 중인 동안 로컬로 고정 hello 볼륨에 백업 작업은 허용 됩니다. |
| 클라우드 스냅숏에 대한 처리 속도 |15분/TB |<ul><li>최소 시간 toomake hello 클라우드 스냅숏 백업에 할당 된 볼륨 데이터 1TB 당 업로드를 위해 준비 합니다. </li><li> 총 클라우드 스냅숏 시간이이 시간 toohello 스냅숏 업로드 시간을 인터넷 대역폭 toocloud hello로는 영향을 추가 하 여 계산 됩니다. |
| 최대 클라이언트 읽기/쓰기 처리량 (hello SSD 계층에서 제공) 하는 경우 * |단일 10GbE 네트워크 인터페이스와 함께 920/720MB/초 |MPIO 및 두 개의 네트워크 인터페이스와 too2x를. |
| 최대 클라이언트 읽기/쓰기 처리량 (에서 제공 될 경우 hello HDD 계층) * |120/250MB/초 | |
| 최대 클라이언트 읽기/쓰기 처리량 (hello 클라우드 계층에서 제공) 하는 경우 * 업데이트 3 이상 * * |계층화된 볼륨의 경우 40/60MB/s<br><br>볼륨을 만드는 동안 선택된 보관 옵션이 있는 계층화된 볼륨의 경우 60/80MB/s |읽기 처리량은 충분한 I/O 큐 깊이를 생성 및 유지 관리하는 클라이언트에 따라 달라집니다. <br><br>달성 속도 hello는 사용 되는 기본 저장소 계정 hello 속도에 따라 달라 집니다. |

&#42; I/O 형식당 최대 처리량은 100% 읽기 및 100% 쓰기 시나리오로 측정되었습니다. 실제 처리량은 낮을 수 있으며 I/O 조합 및 네트워크 상태에 따라 다릅니다.

&#42; &#42; 성능 숫자 이전 tooUpdate 3 낮아질 수 있습니다.

## <a name="next-steps"></a>다음 단계
검토 hello [StorSimple 시스템 요구 사항](storsimple-8000-system-requirements.md)합니다.

