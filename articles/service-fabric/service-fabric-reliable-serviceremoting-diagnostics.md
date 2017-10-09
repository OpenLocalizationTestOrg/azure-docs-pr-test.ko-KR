---
title: "aaaAzure ServiceFabric 진단 및 모니터링 | Microsoft Docs"
description: "이 문서에서 내보낸 성능 카운터와 같은 hello 서비스 패브릭 신뢰할 수 있는 ServiceRemoting 런타임에서 hello 성능 모니터링 기능을 설명 합니다."
services: service-fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: suchiagicha
ms.assetid: 1c229923-670a-4634-ad59-468ff781ad18
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: suchiagicha
ms.openlocfilehash: 64db9a890bd59a1326e587d14b89c007b71a9059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-performance-monitoring-for-reliable-service-remoting"></a>Reliable Service Remoting에 대한 진단 및 성능 모니터링
hello 신뢰할 수 있는 ServiceRemoting 런타임에서 내보내는 [÷ ´ ֹ](https://msdn.microsoft.com/library/system.diagnostics.performancecounter.aspx)합니다. 이러한 hello ServiceRemoting 작동 방법에 대 한 정보를 제공 하 고 사용 하 여 문제 해결 및 성능 모니터링.


## <a name="performance-counters"></a>성능 카운터
hello 신뢰할 수 있는 ServiceRemoting 런타임 hello 다음 성능 카운터 범주를 정의 합니다.

| Category | 설명 |
| --- | --- |
| Service Fabric 서비스 |서비스 패브릭 원격 서비스의 특정 tooAzure 카운터, 평균 소요 시간 tooprocess 요청 하는 예를 들어 |
| Service Fabric 서비스 메서드 |특정 카운터 toomethods 구현한 서비스 패브릭 원격 서비스 예를 들어 서비스 메서드 호출 빈도 |

각 hello 범주 앞에 하나 이상의 카운터가 있습니다.

hello [Windows 성능 모니터](https://technet.microsoft.com/library/cc749249.aspx) hello Windows 운영 체제에서 기본적으로 사용할 수 있는 응용 프로그램에서 사용 하는 뷰와 toocollect 성능 카운터 데이터를 수 있습니다. [Azure 진단](../cloud-services/cloud-services-dotnet-diagnostics.md) 는 성능 카운터 데이터를 수집 및 업로드 tooAzure 테이블에 대 한 또 다른 옵션입니다.

### <a name="performance-counter-instance-names"></a>성능 카운터 인스턴스 이름
많은 수의 ServiceRemoting 서비스 또는 파티션이 있는 클러스터에는 성능 카운터 인스턴스 수가 많습니다. hello 성능 카운터 인스턴스가 해당 연결 된 hello 성능 카운터 인스턴스 이름 (있는 경우) hello 특정 파티션 및 서비스 메서드를 식별에 도움이 될 수 있습니다.

#### <a name="service-fabric-service-category"></a>Service Fabric 서비스 범주
Hello 범주에 대 한 `Service Fabric Service`, hello 카운터 인스턴스 이름이 형식에 따라 hello에 표시 됩니다.

`ServiceFabricPartitionID_ServiceReplicaOrInstanceId_ServiceRuntimeInternalID`

*ServiceFabricPartitionID* 의 성능 카운터 인스턴스 hello 서비스 패브릭 파티션 ID와 연결 된 hello hello 문자열 표현입니다. hello 파티션 ID는 GUID와 문자열 표현 hello를 통해 생성 된 [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) "D" 형식 지정자와 함께 메서드.

*ServiceReplicaOrInstanceId* 의 연관 된 성능 카운터 인스턴스 hello 서비스 패브릭 복제본/인스턴스 ID는 hello hello 문자열 표현입니다.

*ServiceRuntimeInternalID* 내부 사용에 대 한 hello 패브릭 서비스 런타임에 의해 생성 되는 64 비트 정수의 hello 문자열 표현입니다. 이것은 포함 hello 성능 카운터 인스턴스 이름을 tooensure 고유성 및 다른 성능 카운터 인스턴스 이름이와 충돌 하지 합니다. 사용자가 시도해 서는 안 toointerpret이이 부분의 hello 성능 카운터 인스턴스 이름입니다.

hello 다음은 toohello 속해 있는 카운터에 대 한 카운터 인스턴스 이름의 예 `Service Fabric Service` 범주:

`2740af29-78aa-44bc-a20b-7e60fb783264_635650083799324046_5008379932`

Hello 예제에서는 앞에서 `2740af29-78aa-44bc-a20b-7e60fb783264` hello 서비스 패브릭 파티션 ID의 hello 문자열 표현인 `635650083799324046` 복제본/InstanceId의 문자열 표현인 및 `5008379932` hello 런타임의 내부에 대해 생성 되는 hello 64 비트 id 사용 합니다.

#### <a name="service-fabric-service-method-category"></a>Service Fabric 서비스 메서드 범주
Hello 범주에 대 한 `Service Fabric Service Method`, hello 카운터 인스턴스 이름이 형식에 따라 hello에 표시 됩니다.

`MethodName_ServiceRuntimeMethodId_ServiceFabricPartitionID_ServiceReplicaOrInstanceId_ServiceRuntimeInternalID`

*MethodName* 연결 된 성능 카운터 인스턴스 hello hello 서비스 메서드의 hello 이름이 됩니다. hello 메서드 이름의 hello 형식은 windows hello hello 성능 카운터 인스턴스 이름이 최대 길이에 제약 조건이 있는 hello 이름의 hello 가독성의 균형을 hello 패브릭 서비스 런타임의 일부 논리에 따라 결정 됩니다.

*ServiceRuntimeMethodId* 내부 사용에 대 한 hello 패브릭 서비스 런타임에 의해 생성 되는 32 비트 정수 hello 문자열 표현입니다. 이것은 포함 hello 성능 카운터 인스턴스 이름을 tooensure 고유성 및 다른 성능 카운터 인스턴스 이름이와 충돌 하지 합니다. 사용자가 시도해 서는 안 toointerpret이이 부분의 hello 성능 카운터 인스턴스 이름입니다.

*ServiceFabricPartitionID* 의 성능 카운터 인스턴스 hello 서비스 패브릭 파티션 ID와 연결 된 hello hello 문자열 표현입니다. hello 파티션 ID는 GUID와 문자열 표현 hello를 통해 생성 된 [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) "D" 형식 지정자와 함께 메서드.

*ServiceReplicaOrInstanceId* 의 연관 된 성능 카운터 인스턴스 hello 서비스 패브릭 복제본/인스턴스 ID는 hello hello 문자열 표현입니다.

*ServiceRuntimeInternalID* 내부 사용에 대 한 hello 패브릭 서비스 런타임에 의해 생성 되는 64 비트 정수의 hello 문자열 표현입니다. 이것은 포함 hello 성능 카운터 인스턴스 이름을 tooensure 고유성 및 다른 성능 카운터 인스턴스 이름이와 충돌 하지 합니다. 사용자가 시도해 서는 안 toointerpret이이 부분의 hello 성능 카운터 인스턴스 이름입니다.

hello 다음은 toohello 속해 있는 카운터에 대 한 카운터 인스턴스 이름의 예 `Service Fabric Service Method` 범주:

`ivoicemailboxservice.leavemessageasync_2_89383d32-e57e-4a9b-a6ad-57c6792aa521_635650083804480486_5008380`

Hello 예제에서는 앞에서 `ivoicemailboxservice.leavemessageasync` hello 메서드 이름 `2` 는 hello 런타임의 내부에 대해 생성 하는 32 비트 ID가 사용 하 여 hello `89383d32-e57e-4a9b-a6ad-57c6792aa521` hello 서비스 패브릭 파티션 ID의 hello 문자열 표현인`635650083804480486` hello 문자열 hello 서비스 패브릭 복제본/인스턴스 ID의 표현 및 `5008380` hello 런타임의 내부에 대해 생성 하는 hello 64 비트 ID 사용 됩니다.

## <a name="list-of-performance-counters"></a>성능 카운터 목록
### <a name="service-method-performance-counters"></a>서비스 메서드 성능 카운터

hello 신뢰할 수 있는 서비스 런타임 hello 서비스 메서드의 성능 카운터 관련된 toohello 실행을 게시 합니다.

| 범주 이름 | 카운터 이름 | 설명 |
| --- | --- | --- |
| Service Fabric 서비스 메서드 |초당 호출 수 |Hello 서비스 메서드가 호출 된 초당 횟수 |
| Service Fabric 서비스 메서드 |호출당 평균 시간(밀리초) |밀리초 tooexecute hello 서비스 메서드는 데 걸린 시간 |
| Service Fabric 서비스 메서드 |초당 발생한 예외 수 |서비스 메서드에서 hello 횟수 초당 예외가 발생 했습니다. |

### <a name="service-request-processing-performance-counters"></a>서비스 요청 처리 성능 카운터
서비스 프록시 개체를 통해 메서드를 호출 하는 클라이언트 hello 네트워크 toohello 원격 서비스를 통해 전송 되는 요청 메시지에서 발생 합니다. hello 서비스는 hello 요청 메시지를 처리 하 고 응답 백 toohello 클라이언트에 보냅니다. hello 신뢰할 수 있는 ServiceRemoting 런타임 성능 카운터가 관련된 tooservice 요청 처리를 수행 하는 hello를 게시 합니다.

| 범주 이름 | 카운터 이름 | 설명 |
| --- | --- | --- |
| Service Fabric 서비스 |미해결 요청 수 |Hello 서비스에서 처리 중인 요청 수 |
| Service Fabric 서비스 |요청당 평균 시간(밀리초) |걸린 시간 (밀리초) hello 서비스 tooprocess 요청 |
| Service Fabric 서비스 |요청 deserialization에 걸린 평균 시간(밀리초) |Hello 서비스에서 수신 될 때 시간 (밀리초) 수행한 toodeserialize 서비스 요청 메시지 |
| Service Fabric 서비스 |요청 serialization에 걸린 평균 시간(밀리초) |Hello 응답 toohello 클라이언트에 전송 되기 전에 hello 서비스만 시간 (밀리초) 수행한 tooserialize hello 서비스 응답 메시지 |

## <a name="next-steps"></a>다음 단계
* [샘플 코드](https://github.com/Azure/servicefabric-samples)
* [PerfView의 EventSource 공급자](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
