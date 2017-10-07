---
title: "aaaActors 진단 및 모니터링 | Microsoft Docs"
description: "이 문서에서는 hello 진단 및 성능 모니터링 hello 이벤트 및 성능 카운터를 내보내는 것을 포함 하 여 hello 서비스 패브릭 Reliable Actors 런타임에의 기능을 설명 합니다."
services: service-fabric
documentationcenter: .net
author: abhishekram
manager: timlt
editor: vturecek
ms.assetid: 1c229923-670a-4634-ad59-468ff781ad18
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: abhisram
ms.openlocfilehash: 5b266d67875722feef5c5be8861bda6d8132a7d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-performance-monitoring-for-reliable-actors"></a>Reliable Actors에 대한 진단 및 성능 모니터링
hello Reliable Actors 런타임에서 내보내는 [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) 이벤트 및 [÷ ´ ֹ](https://msdn.microsoft.com/library/system.diagnostics.performancecounter.aspx)합니다. 이러한 hello 런타임의 작동 방식에 대 한 정보를 제공 하 고 사용 하 여 문제 해결 및 성능 모니터링.

## <a name="eventsource-events"></a>EventSource 이벤트
hello EventSource 공급자 hello Reliable Actors 런타임 이름은 "Microsoft ServiceFabric 배우"입니다. 이 이벤트 원본의 이벤트가 hello에 표시 [진단 이벤트](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md#view-service-fabric-system-events-in-visual-studio) hello 행위자 응용 프로그램 중인 경우 창 [Visual Studio에서 디버깅](service-fabric-debugging-your-application.md)합니다.

도구 및 기술이 수집 및/또는 EventSource 이벤트 보기의 예는 [PerfView](http://www.microsoft.com/download/details.aspx?id=28567), [Azure 진단](../cloud-services/cloud-services-dotnet-diagnostics.md), [의미 체계 로깅](https://msdn.microsoft.com/library/dn774980.aspx), 및 hello [ Microsoft TraceEvent 라이브러리](http://www.nuget.org/packages/Microsoft.Diagnostics.Tracing.TraceEvent)합니다.

### <a name="keywords"></a>키워드
신뢰할 수 있는 작업자 EventSource toohello 속하는 모든 이벤트가 하나 이상의 키워드와 연결 됩니다. 이를 통해 수집된 이벤트를 필터링할 수 있습니다. 다음 키워드 비트 hello 정의 됩니다.

| Bit | 설명 |
| --- | --- |
| 0x1 |Hello 패브릭 행위자 런타임의 hello 작동을 요약 하는 중요 한 이벤트의 집합입니다. |
| 0x2 |행위자 메서드 호출을 설명하는 이벤트의 집합. 자세한 내용은 참조 hello [작업자에 대 한 소개 항목](service-fabric-reliable-actors-introduction.md)합니다. |
| 0x4 |관련된 tooactor 상태 이벤트의 집합입니다. 자세한 내용은 hello 항목을 참고 [행위자 상태 관리](service-fabric-reliable-actors-state-management.md)합니다. |
| 0x8 |Hello 행위자의 관련된 tooturn 기반 동시성 이벤트의 집합입니다. 자세한 내용은 hello 항목을 참고 [동시성](service-fabric-reliable-actors-introduction.md#concurrency)합니다. |

## <a name="performance-counters"></a>성능 카운터
hello Reliable Actors 런타임 hello 다음 성능 카운터 범주를 정의 합니다.

| Category | 설명 |
| --- | --- |
| 서비스 패브릭 행위자 |특정 tooAzure 서비스 패브릭 행위자 toosave 행위자 상태에 걸린 시간 등 카운터 |
| 서비스 패브릭 행위자 메서드 |예를 들어 서비스 패브릭 행위자가 구현 하는 특정 toomethods 카운터 행위자 메서드를 호출 하는 빈도 |

각 범주 위에 hello에 하나 이상의 카운터가 있습니다.

hello [Windows 성능 모니터](https://technet.microsoft.com/library/cc749249.aspx) hello Windows 운영 체제에서 기본적으로 사용할 수 있는 응용 프로그램에서 사용 하는 뷰와 toocollect 성능 카운터 데이터를 수 있습니다. [Azure 진단](../cloud-services/cloud-services-dotnet-diagnostics.md) 는 성능 카운터 데이터를 수집 및 업로드 tooAzure 테이블에 대 한 또 다른 옵션입니다.

### <a name="performance-counter-instance-names"></a>성능 카운터 인스턴스 이름
많은 수의 행위자 서비스 또는 행위자 서비스 파티션이 있는 클러스터에는 행위자 성능 카운터 인스턴스 수가 많습니다. hello 성능 카운터 인스턴스 이름이 수 식별에 도움이 되 hello 특정 [파티션](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors) 행위자 메서드 (있는 경우) 해당 hello 성능 카운터 인스턴스와 연결 됩니다.

#### <a name="service-fabric-actor-category"></a>서비스 패브릭 행위자 범주
Hello 범주에 대 한 `Service Fabric Actor`, hello 카운터 인스턴스 이름이 형식에 따라 hello에 표시 됩니다.

`ServiceFabricPartitionID_ActorsRuntimeInternalID`

*ServiceFabricPartitionID* 의 성능 카운터 인스턴스 hello 서비스 패브릭 파티션 ID와 연결 된 hello hello 문자열 표현입니다. hello 파티션 ID는 GUID와 문자열 표현 hello를 통해 생성 된 [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) "D" 형식 지정자와 함께 메서드.

*ActorRuntimeInternalID* 내부 사용에 대 한 hello 패브릭 행위자 런타임에 의해 생성 되는 64 비트 정수의 hello 문자열 표현입니다. 이것은 포함 hello 성능 카운터 인스턴스 이름을 tooensure 고유성 및 다른 성능 카운터 인스턴스 이름이와 충돌 하지 합니다. 사용자가 시도해 서는 안 toointerpret이이 부분의 hello 성능 카운터 인스턴스 이름입니다.

hello 다음은 toohello 속해 있는 카운터에 대 한 카운터 인스턴스 이름의 예 `Service Fabric Actor` 범주:

`2740af29-78aa-44bc-a20b-7e60fb783264_635650083799324046`

위의 hello 예에서 `2740af29-78aa-44bc-a20b-7e60fb783264` hello 서비스 패브릭 파티션 ID의 hello 문자열 표현인 및 `635650083799324046` hello 런타임의 내부에 대해 생성 되는 hello 64 비트 ID를 사용 합니다.

#### <a name="service-fabric-actor-method-category"></a>서비스 패브릭 행위자 메서드 범주
Hello 범주에 대 한 `Service Fabric Actor Method`, hello 카운터 인스턴스 이름이 형식에 따라 hello에 표시 됩니다.

`MethodName_ActorsRuntimeMethodId_ServiceFabricPartitionID_ActorsRuntimeInternalID`

*MethodName* 연결 된 성능 카운터 인스턴스 hello hello 행위자 메서드의 hello 이름이 됩니다. hello 메서드 이름의 hello 형식은 windows hello hello 성능 카운터 인스턴스 이름이 최대 길이에 제약 조건이 있는 hello 이름의 hello 가독성의 균형을 hello 패브릭 행위자 런타임의 일부 논리에 따라 결정 됩니다.

*ActorsRuntimeMethodId* 내부 사용에 대 한 hello 패브릭 행위자 런타임에 의해 생성 되는 32 비트 정수 hello 문자열 표현입니다. 이것은 포함 hello 성능 카운터 인스턴스 이름을 tooensure 고유성 및 다른 성능 카운터 인스턴스 이름이와 충돌 하지 합니다. 사용자가 시도해 서는 안 toointerpret이이 부분의 hello 성능 카운터 인스턴스 이름입니다.

*ServiceFabricPartitionID* 의 성능 카운터 인스턴스 hello 서비스 패브릭 파티션 ID와 연결 된 hello hello 문자열 표현입니다. hello 파티션 ID는 GUID와 문자열 표현 hello를 통해 생성 된 [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) "D" 형식 지정자와 함께 메서드.

*ActorRuntimeInternalID* 내부 사용에 대 한 hello 패브릭 행위자 런타임에 의해 생성 되는 64 비트 정수의 hello 문자열 표현입니다. 이것은 포함 hello 성능 카운터 인스턴스 이름을 tooensure 고유성 및 다른 성능 카운터 인스턴스 이름이와 충돌 하지 합니다. 사용자가 시도해 서는 안 toointerpret이이 부분의 hello 성능 카운터 인스턴스 이름입니다.

hello 다음은 toohello 속해 있는 카운터에 대 한 카운터 인스턴스 이름의 예 `Service Fabric Actor Method` 범주:

`ivoicemailboxactor.leavemessageasync_2_89383d32-e57e-4a9b-a6ad-57c6792aa521_635650083804480486`

위의 hello 예에서 `ivoicemailboxactor.leavemessageasync` hello 메서드 이름입니다 `2` 는 hello 런타임의 내부에 대해 생성 하는 32 비트 ID가 사용 하 여 hello `89383d32-e57e-4a9b-a6ad-57c6792aa521` hello 서비스 패브릭 파티션 ID의 hello 문자열 표현인 및 `635650083804480486` hello 64 비트 id hello 런타임의 내부 사용을 위해 생성 합니다.

## <a name="list-of-events-and-performance-counters"></a>이벤트 및 성능 카운터 목록
### <a name="actor-method-events-and-performance-counters"></a>행위자 메서드 이벤트 및 성능 카운터
hello Reliable Actors 런타임에서 내보내는 hello 너무 관련 된 이벤트를 다음[행위자 메서드](service-fabric-reliable-actors-introduction.md)합니다.

| 이벤트 이름 | 이벤트 ID | Level | 키워드 | 설명 |
| --- | --- | --- | --- | --- |
| ActorMethodStart |7 |자세한 정보 표시 |0x2 |행위자 런타임이 행위자 메서드 tooinvoke에 대 한 것입니다. |
| ActorMethodStop |8 |자세한 정보 표시 |0x2 |행위자 메서드가 실행을 완료했습니다. 즉, hello 런타임 비동기 호출 toohello 행위자 메서드가 반환 되었음 및 hello 행위자 메서드에 의해 반환 된 hello 작업을 마쳤습니다. |
| ActorMethodThrewException |9 |Warning |0x3 |Hello 행위자 메서드에 의해 반환 된 hello 런타임 비동기 호출 toohello 행위자 메서드 중 이나 hello hello 작업을 실행 하는 동안 hello 행위자 메서드를 실행 하는 동안 예외가 throw 되었습니다. 이 이벤트는 일종의 조사 해야 하는 hello 행위자 코드에서 오류를 나타냅니다. |

hello Reliable Actors 런타임 hello 행위자 메서드의 성능 카운터 관련된 toohello 실행을 게시 합니다.

| 범주 이름 | 카운터 이름 | 설명 |
| --- | --- | --- |
| 서비스 패브릭 행위자 메서드 |초당 호출 수 |Hello 행위자 서비스 메서드가 호출 된 초당 횟수 |
| 서비스 패브릭 행위자 메서드 |호출당 평균 시간(밀리초) |밀리초에서에 걸린 시간 tooexecute hello 행위자 서비스 메서드 |
| 서비스 패브릭 행위자 메서드 |초당 발생한 예외 수 |행위자 서비스 메서드가 hello 횟수 초당 예외가 발생 했습니다. |

### <a name="concurrency-events-and-performance-counters"></a>동시 이벤트 및 성능 카운터
hello Reliable Actors 런타임에서 내보내는 hello 너무 관련 된 이벤트를 다음[동시성](service-fabric-reliable-actors-introduction.md#concurrency)합니다.

| 이벤트 이름 | 이벤트 ID | Level | 키워드 | 설명 |
| --- | --- | --- | --- | --- |
| ActorMethodCallsWaitingForLock |12 |자세한 정보 표시 |0x8 |이 이벤트는 행위자에서 각 전환의 시작 부분 hello에 기록 됩니다. Hello tooacquire hello 행위자 별 잠금을 얻기 턴 기반 동시성을 적용 하는 대기 중인 행위자 호출 보류 중인 수를 포함 합니다. |

hello Reliable Actors 런타임 성능 카운터에 대 한 관련된 tooconcurrency 다음 hello를 게시 합니다.

| 범주 이름 | 카운터 이름 | 설명 |
| --- | --- | --- |
| 서비스 패브릭 행위자 |행위자 잠금을 기다리는 행위자 호출 수 |대기 중인 tooacquire hello 행위자 별 잠금을 얻기 턴 기반 동시성을 적용 하는 호출에 보류 중인 행위자의 수 |
| 서비스 패브릭 행위자 |잠금 대기당 평균 시간(밀리초) |시간 (밀리초) 수행한 tooacquire hello 행위자 별 잠금을 얻기 턴 기반 동시성을 적용 하는 |
| 서비스 패브릭 행위자 |평균 밀리초 행위자 잠금 보유됨 |행위자 당 잠금이 유지 되는 hello에 대 한 시간 (밀리초) |

### <a name="actor-state-management-events-and-performance-counters"></a>행위자 상태 관리 이벤트 및 성능 카운터
hello Reliable Actors 런타임에서 내보내는 hello 너무 관련 된 이벤트를 다음[행위자 상태 관리](service-fabric-reliable-actors-state-management.md)합니다.

| 이벤트 이름 | 이벤트 ID | Level | 키워드 | 설명 |
| --- | --- | --- | --- | --- |
| ActorSaveStateStart |10 |자세한 정보 표시 |0x4 |행위자 런타임이 toosave hello 작업자 상태에 대 한 것입니다. |
| ActorSaveStateStop |11 |자세한 정보 표시 |0x4 |행위자 런타임 hello 행위자 상태를 저장 했습니다. |

hello Reliable Actors 런타임 성능 카운터가 관련된 tooactor 상태 관리를 수행 하는 hello를 게시 합니다.

| 범주 이름 | 카운터 이름 | 설명 |
| --- | --- | --- |
| 서비스 패브릭 행위자 |상태 저장 작업당 평균 시간(밀리초) |밀리초에서 toosave 행위자 상태에 걸린 시간 |
| 서비스 패브릭 행위자 |로드 상태 작업당 평균 시간(밀리초) |밀리초에서 tooload 행위자 상태에 걸린 시간 |

### <a name="events-related-tooactor-replicas"></a>이벤트 관련된 tooactor 복제본
hello Reliable Actors 런타임에서 내보내는 hello 너무 관련 된 이벤트를 다음[행위자 복제본](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors)합니다.

| 이벤트 이름 | 이벤트 ID | Level | 키워드 | 설명 |
| --- | --- | --- | --- | --- |
| ReplicaChangeRoleToPrimary |1 |정보 제공 |0x1 |행위자 복제 역할 tooPrimary 변경 합니다. 이 안에이 복제본이이 파티션에 대 한 hello 행위자 만들어질 수를 의미 합니다. |
| ReplicaChangeRoleFromPrimary |2 |정보 제공 |0x1 |행위자 복제 toonon 주 역할을 변경 합니다. 이 의미이 파티션에 대 한 hello 작업 자가 더 이상이 복제 내부 만들 수 없습니다. 새 요청에이 복제 내에서 이미 만든 tooactors를 배달 됩니다. 모든 진행 중인 요청을 완료 한 후 hello 작업자는 제거 됩니다. |

### <a name="actor-activation-and-deactivation-events-and-performance-counters"></a>행위자 활성화 및 비활성화 이벤트와 성능 카운터
hello Reliable Actors 런타임에서 내보내는 hello 너무 관련 된 이벤트를 다음[행위자 활성화 및 비활성화](service-fabric-reliable-actors-lifecycle.md)합니다.

| 이벤트 이름 | 이벤트 ID | Level | 키워드 | 설명 |
| --- | --- | --- | --- | --- |
| ActorActivated |5 |정보 제공 |0x1 |행위자가 활성화되었습니다. |
| ActorDeactivated |6 |정보 제공 |0x1 |행위자가 비활성화되었습니다. |

hello Reliable Actors 런타임 게시 hello tooactor 활성화 및 비활성화 관련 성능 카운터를 수행 합니다.

| 범주 이름 | 카운터 이름 | 설명 |
| --- | --- | --- |
| 서비스 패브릭 행위자 |평균 OnActivateAsync(밀리초) |밀리초 tooexecute OnActivateAsync 메서드는 데 걸린 시간 |

### <a name="actor-request-processing-performance-counters"></a>행위자 요청 처리 성능 카운터
행위자 프록시 개체를 통해 메서드를 호출 하는 클라이언트를 hello 네트워크 toohello 행위자 서비스를 통해 전송 되는 요청 메시지에서 발생 합니다. hello 서비스는 hello 요청 메시지를 처리 하 고 응답 백 toohello 클라이언트에 보냅니다. hello Reliable Actors 런타임 성능 카운터가 관련된 tooactor 요청 처리를 수행 하는 hello를 게시 합니다.

| 범주 이름 | 카운터 이름 | 설명 |
| --- | --- | --- |
| 서비스 패브릭 행위자 |미해결 요청 수 |Hello 서비스에서 처리 중인 요청 수 |
| 서비스 패브릭 행위자 |요청당 평균 시간(밀리초) |걸린 시간 (밀리초) hello 서비스 tooprocess 요청 |
| 서비스 패브릭 행위자 |요청 deserialization에 걸린 평균 시간(밀리초) |Hello 서비스에서 수신 될 때 시간 (밀리초) 수행한 toodeserialize 행위자 요청 메시지 |
| 서비스 패브릭 행위자 |요청 serialization에 걸린 평균 시간(밀리초) |Hello 응답 toohello 클라이언트에 전송 되기 전에 hello 서비스에서 시간 (밀리초) 수행한 tooserialize hello 행위자 응답 메시지 |

## <a name="next-steps"></a>다음 단계
* [Reliable Actors hello 서비스 패브릭 플랫폼을 사용 하는 방법](service-fabric-reliable-actors-platform.md)
* [행위자 API 참조 설명서](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [샘플 코드](https://github.com/Azure/servicefabric-samples)
* [PerfView의 EventSource 공급자](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
