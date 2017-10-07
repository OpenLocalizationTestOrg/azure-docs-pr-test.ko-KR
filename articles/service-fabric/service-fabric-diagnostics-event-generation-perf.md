---
title: "서비스 패브릭 성능 모니터링 aaaAzure | Microsoft Docs"
description: "Azure Service Fabric 클러스터를 모니터링하고 진단하기 위한 성능 카운터에 대해 알아봅니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 54d4c62b7250a1f70b0898ba07ae5a37716f4cf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-metrics"></a>성능 메트릭

메트릭 수집된 toounderstand hello 성능 클러스터 수 뿐만 아니라 hello 응용 프로그램에서 실행 해야 합니다. 서비스 패브릭 클러스터에 대 한 hello 다음 성능 카운터를 수집 하는 것이 좋습니다.

## <a name="nodes"></a>노드

클러스터의 hello 컴퓨터용 hello 다음 toobetter 배율을 결정 하는 적절 한 클러스터를 만들고 각 컴퓨터에 부하를 hello를 이해 하는 성능 카운터를 수집 하는 것이 좋습니다.

| 카운터 범주 | 카운터 이름 |
| --- | --- |
| PhysicalDisk(디스크당) | 평균 디스크 읽기 큐 길이 |
| PhysicalDisk(디스크당) | 평균 디스크 쓰기 큐 길이 |
| PhysicalDisk(디스크당) | 평균 디스크 초/읽기 |
| PhysicalDisk(디스크당) | 평균 디스크 초/쓰기 |
| PhysicalDisk(디스크당) | 디스크 읽기/초  |
| PhysicalDisk(디스크당) | 디스크 읽기 바이트/초  |
| PhysicalDisk(디스크당) | 디스크 쓰기/초 |
| PhysicalDisk(디스크당) | 디스크 쓰기 바이트/초 |
| 메모리 | Available MBytes |
| PagingFile | % 사용량 |
| 프로세스(합계) | % Processor Time |
| 프로세스(서비스당) | % Processor Time |
| 프로세스(서비스당) | ID 프로세스 |
| 프로세스(서비스당) | 프로세스 바이트 |
| 프로세스(서비스당) | 스레드 개수 |
| 프로세스(서비스당) | 가상 바이트 |
| 프로세스(서비스당) | 작업 집합 |
| 프로세스(서비스당) | 작업 집합 - 개인 |

## <a name="net-applications-and-services"></a>.NET 응용 프로그램 및 서비스

.NET 서비스 tooyour 클러스터를 배포 하는 경우 카운터를 따라 hello를 수집 합니다. 

| 카운터 범주 | 카운터 이름 |
| --- | --- |
| .NET CLR 메모리(서비스당) | 프로세스 ID |
| .NET CLR 메모리(서비스당) | #커밋된 전체 바이트 |
| .NET CLR 메모리(서비스당) | #예약된 전체 바이트 |
| .NET CLR 메모리(서비스당) | #모든 힙의 바이트 |
| .NET CLR 메모리(서비스당) | #0 컬렉션 생성 |
| .NET CLR 메모리(서비스당) | #1 컬렉션 생성 |
| .NET CLR 메모리(서비스당) | #2 컬렉션 생성 |
| .NET CLR 메모리(서비스당) | % Time in GC |

### <a name="service-fabrics-custom-performance-counters"></a>Service Fabric 사용자 지정 성능 카운터

Service Fabric은 상당한 양의 사용자 지정 성능 카운터를 생성합니다. Hello SDK가 설치 되어 있는 경우 목록을 볼 수 있습니다 hello 포괄적인 Windows 컴퓨터에 성능 모니터 응용 프로그램에서 (시작 > 성능 모니터). 

Hello 응용 프로그램에서 배포 하는 tooyour 클러스터, Reliable Actors를 사용 하는 경우 추가에서 countes `Service Fabric Actor` 및 `Service Fabric Actor Method` 범주 (참조 [서비스 패브릭 신뢰할 수 있는 작업 자가 진단](service-fabric-reliable-actors-diagnostics.md)).

마찬가지로 Reliable Services를 사용하는 경우 카운터를 수집해야 하는 `Service Fabric Service` 및 `Service Fabric Service Method` 카운터 범주가 있습니다. 

신뢰할 수 있는 컬렉션을 사용 하는 경우 hello 추가 하는 것이 좋습니다 `Avg. Transaction ms/Commit` hello에서 `Service Fabric Transactional Replicator` 트랜잭션 메트릭에 당 toocollect hello 평균 커밋 대기 시간입니다.


## <a name="next-steps"></a>다음 단계

* 에 대 한 자세한 내용은 [hello 플랫폼 수준에서 이벤트 생성](service-fabric-diagnostics-event-generation-infra.md) 서비스 패브릭에서
* [Azure 진단](service-fabric-diagnostics-event-aggregation-wad.md)을 통해 성능 메트릭 수집
