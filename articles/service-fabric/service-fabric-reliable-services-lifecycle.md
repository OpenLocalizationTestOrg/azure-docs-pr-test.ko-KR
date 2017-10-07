---
title: "Azure 서비스 패브릭 신뢰할 수 있는 서비스의 수명 주기 hello aaaOverview | Microsoft Docs"
description: "서비스 패브릭 신뢰할 수 있는 서비스의 hello 다른 수명 주기 이벤트에 알아보기"
services: Service-Fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: vturecek;
ms.assetid: 
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 0d75ed5ee7cda85ac9af6a02e160727277804a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-lifecycle-overview"></a>Reliable Services 수명 주기 개요
> [!div class="op_single_selector"]
> * [Windows에서 C#](service-fabric-reliable-services-lifecycle.md)
> * [Linux에서 Java](service-fabric-reliable-services-lifecycle-java.md)
>
>

신뢰할 수 있는 서비스의 hello 주기를 고려할 때는 hello 수명 주기의 hello 기본 사항 가장 중요 한 hello 됩니다. 일반적으로:

- 시작 중
  - 서비스가 생성됩니다.
  - 기회 tooconstruct 변수와 0 개 이상의 수신기를 반환 합니다.
  - 반환 된 모든 수신기 열려 hello 서비스와의 통신을 허용 합니다.
  - 메서드를 호출 하는 hello 서비스 RunAsync를 장기 실행 toodo 서비스 hello를 허용 하거나 백그라운드 작업
- 종료 중
  - hello 취소 토큰 전달된 tooRunAsync 취소 되 고 hello 수신기 닫혀 있습니다.
  - 완료 되 면 hello 서비스 개체 자체은 이벤트 소멸

이러한 이벤트의 순서 지정 정확한 hello 자세한 내용은 있습니다. 특히 이벤트 hello 순서 Stateless 또는 상태 저장 hello 신뢰할 수 있는 서비스 인지에 따라 약간 변경 될 수 있습니다. 또한 상태 저장 서비스에 대 한 주 스왑 시나리오 hello와 toodeal이 있는 합니다. 이 시퀀스 하는 동안 주 hello 역할은 전송 된 tooanother 복제 (또는 다시 시작) hello 서비스를 종료 하지 않고 있습니다. 마지막으로, 오류나 오류 조건에 대 한 toothink을 했습니다.

## <a name="stateless-service-startup"></a>상태 비저장 서비스 시작
상태 비저장 서비스의 hello 수명 주기는 매우 간단 합니다. 이벤트의 hello 순서는 다음과 같습니다.

1. hello 서비스가 생성 되
2. 그런 다음 두 가지 작업이 병렬로 수행됩니다.
    - `StatelessService.CreateServiceInstanceListeners()`가 호출되고 반환된 모든 수신기가 열립니다. `ICommunicationListener.OpenAsync()`가 각 수신기에서 호출됩니다.
    - 서비스의 hello `StatelessService.RunAsync()` 메서드는
3. 있는 경우 서비스의 hello `StatelessService.OnOpenAsync()` 메서드를 호출 합니다. 이는 일반적이지 않은 재정의이지만 사용 가능합니다.

것이 중요 한 toonote 한지 hello 호출 toocreate 및 열기 hello 수신기 및 RunAsync 간 순서가 없습니다. hello 수신기 RunAsync를 시작 하기 전에 열릴 수 있습니다. 마찬가지로, RunAsync 될 수 hello 통신 수신기 열려 있거나도 생성 되기 전에 호출 됩니다. 동기화가 필요한 경우 연습 toohello 구현자로 유지 됩니다. 일반적인 솔루션:

  - 경우에 따라 다른 정보를 만들거나 수행할 때까지 수신기는 작동할 수 없습니다. 상태 비저장 서비스의 경우 해당 작업은 일반적으로 다음과 같은 다른 위치에서 수행할 수 있습니다. 
    - hello 서비스의 생성자에서
    - hello 동안 `CreateServiceInstanceListeners()` 호출
    - 자체 hello 수신기의 hello 생성의 일부로
  - 경우에 따라 hello RunAsync의 코드를 원하지 않습니다 toostart hello 수신기 열려 있는 될 때까지. 이 경우에 추가 조정이 필요합니다. 일반적인 솔루션은 완료 될 때를 나타내는 hello 수신기 내에서 일부 플래그입니다. 이 플래그의 RunAsync tooactual 작업을 계속 하기 전에 확인 합니다.

## <a name="stateless-service-shutdown"></a>상태 비저장 서비스 종료
상태 비저장 서비스를 종료할 때 hello 동일한 패턴 뒤, 반대 방향으로 바로:

1. 병렬로
    - 열려 있는 수신기가 닫힙니다. `ICommunicationListener.CloseAsync()`가 각 수신기에서 호출됩니다.
    - hello 취소 토큰이 전달 너무`RunAsync()` 취소 됩니다. 검사의 hello 취소 토큰 `IsCancellationRequested` 속성 true를 반환 및 hello 토큰의 메서드를 호출 하면 `ThrowIfCancellationRequested` 메서드가 throw는 `OperationCanceledException`합니다.
2. 한 번 `CloseAsync()` 각 수신기에서 완료 되 고 `RunAsync()` 도 완료 되 면 hello 서비스의 `StatelessService.OnCloseAsync()` 있는 경우 메서드가 호출 됩니다. 일반적이 지 않은 toooverride `StatelessService.OnCloseAsync()`합니다.
3. 후 `StatelessService.OnCloseAsync()` 완료 되 면 서비스 개체 hello은 이벤트 소멸

## <a name="stateful-service-startup"></a>상태 저장 서비스 시작
상태 저장 서비스에는 몇 가지 변경 내용과 비슷한 패턴 toostateless 서비스를 가지고합니다. 상태 저장 서비스를 시작할 때 hello 이벤트 순서는 다음과 같습니다.

1. hello 서비스가 생성 되
2. `StatefulServiceBase.OnOpenAsync()`을 호출합니다. 이것은 정말 hello 서비스에서 무시 됩니다.
3. hello 다음 작업이 수행 병렬로
    - `StatefulServiceBase.CreateServiceReplicaListeners()`가 호출됩니다. 
      - Hello 서비스는 기본 반환 되는 모든 수신기는 열립니다. `ICommunicationListener.OpenAsync()`가 각 수신기에서 호출됩니다.
      - 이러한 수신기만로 표시 hello 서비스가 보조 복제본 인 경우 `ListenOnSecondary = true` 열립니다. 보조 복제본에서 수신기가 열려 있는 경우는 일반적이지 않습니다.
    - hello 서비스는 현재 주 영역 hello 서비스의 경우 hello `StatefulServiceBase.RunAsync()` 메서드는
4. 복제 수신기의 hello 모든 면 `OpenAsync()` 호출이 완료 및 `RunAsync()` 를 호출할 `StatefulServiceBase.OnChangeRoleAsync()` 호출 됩니다. 이것은 정말 hello 서비스에서 무시 됩니다.

마찬가지로 toostateless 서비스는 hello 수신기는 생성 하 고 열 hello 순서 없는 게이트웨이 않으며 RunAsync를 호출할 때입니다. 조정 해야 할 경우 hello 솔루션은 동일한 hello 훨씬 합니다. 추가 경우 하나의: hello 통신 수신기에 도착 하는 hello 호출 몇몇 내부 보관 된 정보는 말 [신뢰할 수 있는 컬렉션](service-fabric-reliable-services-reliable-collections.md)합니다. Hello 신뢰할 수 있는 컬렉션은 읽기 가능 인지 또는 쓰기 가능 하도록 하기 전에 hello 통신 수신기를 열 수 있고 RunAsync를 시작할 수 전에, 몇 가지 추가 조정이 필요 합니다. hello 단순 하 고 가장 일반적인 솔루션은 통신 수신기 tooreturn hello에 대 한 hello 클라이언트 사용 하 여 tooknow tooretry hello 요청 하는 일부 오류 코드입니다.

## <a name="stateful-service-shutdown"></a>상태 저장 서비스 종료
마찬가지로 tooStateless 서비스 종료 하는 동안 hello 수명 주기 이벤트 시작 하는 동안 대로 동일 hello는 하지만 반대로 변경 합니다. 상태 저장 서비스를 종료 하 고, hello 다음 이벤트가 발생 합니다.

1. 병렬로
    - 열려 있는 수신기가 닫힙니다. `ICommunicationListener.CloseAsync()`가 각 수신기에서 호출됩니다.
    - hello 취소 토큰이 전달 너무`RunAsync()` 취소 됩니다. 검사의 hello 취소 토큰 `IsCancellationRequested` 속성 true를 반환 및 hello 토큰의 메서드를 호출 하면 `ThrowIfCancellationRequested` 메서드가 throw는 `OperationCanceledException`합니다.
2. 한 번 `CloseAsync()` 각 수신기에서 완료 되 고 `RunAsync()` 도 완료 되 면 hello 서비스 `StatefulServiceBase.OnChangeRoleAsync()` 호출 됩니다. (이 프로토콜과에서 재정의 되 hello 서비스입니다.)
    - RunAsync를 기다리는 toocomplete를만이 서비스 복제본은 주 합니다.
3. 한 번 hello `StatefulServiceBase.OnChangeRoleAsync()` 메서드가 완료 되 면 hello `StatefulServiceBase.OnCloseAsync()` 메서드를 호출 합니다. 이는 일반적이지 않은 재정의이지만 사용 가능합니다.
3. 후 `StatefulServiceBase.OnCloseAsync()` 완료 되 면 서비스 개체 hello은 이벤트 소멸 합니다.

## <a name="stateful-service-primary-swaps"></a>상태 저장 서비스 주 교환
상태 저장 서비스 실행 되는 동안 hello 해당 상태 저장 서비스의 주 복제본을 하나만 열려 해당 통신 수신기 및 해당 RunAsync 메서드. 보조 복제본을 생성하지만 더 이상 호출하지 않습니다. 하지만 상태 저장 서비스 실행 되는 동안 복제본은 현재 주 hello를 변경할 수 있습니다. 그 복제본 볼 수 있는 hello 수명 주기 이벤트의 측면에서? hello 동작 hello 상태 저장 복제본에 게 표시 hello 복제본 강등 또는 hello 스왑 하는 동안 승격 되 고 인지에 따라 달라 집니다.

### <a name="for-hello-primary-being-demoted"></a>수준을 내리고 기본 hello에 대 한
서비스 패브릭이 복제본 toostop 메시지를 처리 하 고 수행 하는 백그라운드 작업을 종료 합니다. 결과적으로,이 단계 다음과 유사한 toowhen hello 서비스를 종료 하 고 있습니다. 한 가지 차이점은 해당 hello 서비스 이벤트 소멸 또는 보조로 그대로 남아 있으므로 종료 되지 않습니다. 다음 Api hello 호출 됩니다.

1. 병렬로
    - 열려 있는 수신기가 닫힙니다. `ICommunicationListener.CloseAsync()`가 각 수신기에서 호출됩니다.
    - hello 취소 토큰이 전달 너무`RunAsync()` 취소 됩니다. 검사의 hello 취소 토큰 `IsCancellationRequested` 속성 true를 반환 및 hello 토큰의 메서드를 호출 하면 `ThrowIfCancellationRequested` 메서드가 throw는 `OperationCanceledException`합니다.
2. 한 번 `CloseAsync()` 각 수신기에서 완료 되 고 `RunAsync()` 도 완료 되 면 hello 서비스 `StatefulServiceBase.OnChangeRoleAsync()` 호출 됩니다. 이것은 정말 hello 서비스에서 무시 됩니다.

### <a name="for-hello-secondary-being-promoted"></a>승격 중인 보조 hello에 대 한
마찬가지로, 서비스 패브릭이 복제본 toostart hello 통신 중에 메시지를 수신 대기 하며 모든 백그라운드 작업에 대 한 관심이 있는 시작 합니다. 결과적으로이 프로세스 다음과 비슷한 toowhen hello 서비스를 만들면 해당 hello 복제본 제외 하 고 자체 이미 있습니다. 다음 Api hello 호출 됩니다.

1. 병렬로
    - `StatefulServiceBase.CreateServiceReplicaListeners()`가 호출되고 반환된 모든 수신기가 열립니다. `ICommunicationListener.OpenAsync()`가 각 수신기에서 호출됩니다.
    - 서비스의 hello `StatefulServiceBase.RunAsync()` 메서드는
2. 복제 수신기의 hello 모든 면 `OpenAsync()` 호출이 완료 및 `RunAsync()` 가 호출 된 `StatefulServiceBase.OnChangeRoleAsync()` 호출 됩니다. 이것은 정말 hello 서비스에서 무시 됩니다.

### <a name="common-issues-during-stateful-service-shutdown-and-primary-demotion"></a>상태 저장 서비스 종료 및 기본 수준 내리기 동안의 일반적인 문제
서비스 패브릭 변경 hello 다양 한 이유 때문에 대 한 상태 저장 서비스의 주입니다. hello 가장 일반적으로는 [균형 조정 클러스터](service-fabric-cluster-resource-manager-balancing.md) 및 [응용 프로그램 업그레이드](service-fabric-application-upgrade.md)합니다. 이러한 작업 중 (뿐만 아니라 hello 서비스가 삭제 된 경우 표시와 같은 일반 서비스 종료 하는 동안), 반드시 해당 hello 서비스 관련 hello `CancellationToken`합니다. 취소를 완전히 처리하지 않는 서비스에는 몇 가지 문제가 발생합니다. 특히, 정상적으로 서비스 패브릭 서비스 toostop hello에 대 한 대기 하므로 이러한 작업은 저하 됩니다. 이 궁극적으로 toofailed 업그레이드 시간 초과 되는 및 롤백합니다. 노드 핫 가져오지만 hello 서비스 toomove 너무 오래 걸리므로 균형 조정 없습니다 때문에 오류 toohonor hello 취소 토큰 불균형 클러스터 발생할 수 있습니다 다른 위치에 있습니다. 

Hello 서비스와 상태 저장 되므로 이기도 hello 사용 하 고 있는지 [신뢰할 수 있는 컬렉션](service-fabric-reliable-services-reliable-collections.md)합니다. 서비스 패브릭에서 기본 강등 될 때 중 하나가 hello 중요 한 정보에서 발생 하는 경우 쓰기 액세스 toohello 기본 상태가 취소 됩니다. 이 두 번째 집합이 hello 서비스 수명 주기 영향을 줄 수 있는 문제를 tooa 이어집니다. hello 타이밍 및 hello 복제본 이동 하는 여부에 따라 반환 예외 hello 컬렉션 또는 종료 합니다. 이러한 예외는 올바르게 처리되어야 합니다. Service Fabric에서 발생한(throw) 예외는 영구[(`FabricException`)](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabricexception?view=azure-dotnet) 및 일시적[(`FabricTransientException`)](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabrictransientexception?view=azure-dotnet) 범주로 분류됩니다. 영구 예외를 기록 하 고 몇 가지 재시도 논리에 따라 hello 일시적 예외가 다시 시도할 수 하는 동안 throw 해야 합니다.

Hello 사용에서 제공 하는 hello 예외 처리 `ReliableCollections` 서비스 수명 주기 이벤트와 함께에서 테스트 및 신뢰할 수 있는 서비스 유효성 검사의 중요 한 부분입니다. 권장 사항 hello는 항상 toorun 부하 상태에서 서비스 업그레이드를 수행 하는 동안 및 [chaos 테스트](service-fabric-controlled-chaos.md) 적이 tooproduction를 배포 하기 전에. 이러한 기본 단계를 통해 서비스가 올바르게 구현되고 수명 주기 이벤트가 올바르게 처리되도록 할 수 있습니다.


## <a name="notes-on-service-lifecycle"></a>서비스 수명 주기에 대한 참고 사항
  - 두 hello `RunAsync()` 메서드와 hello `CreateServiceReplicaListeners/CreateServiceInstanceListeners` 호출은 선택 사항입니다. 서비스에는 이러한 항목이 있거나 없을 수도 있습니다. 예를 들어 응답 toouser 호출에는 모든 작업을 수행 하는 hello 서비스, 있는지 사용할 필요가 없다고 tooimplement `RunAsync()`합니다. Hello 통신 수신기만 및 해당 관련된 코드는 필요 합니다. 마찬가지로, 만들고 통신 수신기를 반환 hello 서비스 toodo를 작동 하는 배경만 있을 수 있습니다는 선택 사항, 하며만 tooimplement`RunAsync()`
  - 서비스 toocomplete에 대해 유효한 `RunAsync()` 성공적으로 및에서 반환 합니다. 완료는 실패 조건이 아닙니다. 완료 `RunAsync()` hello 서비스의 hello 백그라운드 작업이 완료 되었음을 나타냅니다. 상태 저장 신뢰할 수 있는 서비스에 대 한 `RunAsync()` hello 복제본에서 주 tooSecondary 강등 백 tooPrimary 올라갑니다 경우 다시 호출 됩니다.
  - 예기치 않은 예외가 발생(throw)되어 서비스가 `RunAsync()`에서 종료되는 경우 실패로 간주됩니다. hello 서비스 개체는 종료 하 고 상태 오류를 보고 합니다.
  - 이러한 방법 중에서 반환 하는 방법에 시간 제한이 없으며 상태인 동안 즉시 hello 기능 toowrite tooReliable 컬렉션으로 손실 되 고 모든 실제 작업을 완료할 수 없습니다. 가능한 한 빨리 hello 취소 요청을 받으면 반환 하는 것이 좋습니다. 서비스는 적절 한 시간 내에 서비스 패브릭 강제로 수 toothese API 호출 응답 하지 않을 경우 서비스를 종료 합니다. 이러한 상황은 일반적으로 응용 프로그램을 업그레이드하거나 서비스를 삭제할 때 발생합니다. 이 시간 제한은 기본적으로 15분입니다.
  - Hello에서 발생 한 실패 `OnCloseAsync()` path 결과에서 `OnAbort()` hello에 대 한 마지막 발생할 가능성이 있는 최상의 기회는 호출 되 고 tooclean를 서비스 하 고 요청할가 있는 모든 리소스를 해제 합니다.

## <a name="next-steps"></a>다음 단계
- [TooReliable 서비스 소개](service-fabric-reliable-services-introduction.md)
- [Reliable Services 빠른 시작](service-fabric-reliable-services-quick-start.md)
- [신뢰할 수 있는 서비스 고급 사용법](service-fabric-reliable-services-advanced-usage.md)
