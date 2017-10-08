---
title: "신뢰할 수 있는 서비스의 aaaAdvanced 사용 | Microsoft Docs"
description: "서비스에 유연성을 더해 주는 서비스 패브릭의 Reliable Services 고급 사용법에 대해 알아봅니다."
services: Service-Fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: masnider
ms.assetid: f2942871-863d-47c3-b14a-7cdad9a742c7
ms.service: Service-Fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: e6d6310a4deae9edcfcd76551e1337f0e39e9e5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-usage-of-hello-reliable-services-programming-model"></a>고급 프로그래밍 모델 hello 신뢰할 수 있는 서비스의 사용
Azure 서비스 패브릭은 신뢰할 수 있는 상태 비저장 및 상태 저장 서비스의 작성과 관리를 단순화합니다. 이 가이드 발언 toogain 신뢰할 수 있는 서비스의 고급 사용에 대 한 보다 많은 제어 및 유연성에 서비스를 대신 합니다. 이전 tooreading 안내이 잘 이해 [hello 신뢰할 수 있는 서비스 프로그래밍 모델](service-fabric-reliable-services-introduction.md)합니다.

상태 저장 서비스와 상태 비저장 서비스 모두 사용자 코드에 대한 두 개의 기본 진입점이 있습니다.

* `RunAsync(C#) / runAsync(Java)` 는 서비스 코드에 대한 범용 진입점입니다.
* `CreateServiceReplicaListeners(C#)` 및 `CreateServiceInstanceListeners(C#) / createServiceInstanceListeners(Java)`는 클라이언트 요청에 대한 통신 수신기를 여는 데 사용됩니다.

대부분의 서비스에는 이 두 진입점만 있으면 됩니다. 드문 경우이지만 서비스의 수명 주기에 대한 제어를 강화해야 하는 경우 추가 수명 주기 이벤트를 사용할 수 있습니다.

## <a name="stateless-service-instance-lifecycle"></a>상태 비저장 서비스 인스턴스 수명 주기
상태 비저장 서비스의 수명 주기는 매우 간단합니다. 상태 비저장 서비스는 열리거나, 닫히거나, 중단될 수만 있습니다. `RunAsync`는 서비스 인스턴스가 열리면 실행되고 서비스 인스턴스가 닫히거나 중단되면 취소됩니다.

하지만 `RunAsync` 충분 해야에서 거의 모든 경우 hello open, close, 및 중단 이벤트는 상태 비저장 서비스에는 또한 사용할 수 있습니다.

* `Task OnOpenAsync(IStatelessServicePartition, CancellationToken) - C# / CompletableFuture<String> onOpenAsync(CancellationToken) - Java`OnOpenAsync는 toobe 사용에 대 한 hello 상태 비저장 서비스 인스턴스가 되는 경우 호출 됩니다. 이때 확장된 서비스 초기화 작업을 시작할 수 있습니다.
* `Task OnCloseAsync(CancellationToken) - C# / CompletableFuture onCloseAsync(CancellationToken) - Java`Hello 상태 비저장 서비스 인스턴스 toobe 때 OnCloseAsync 호출은 정상적으로 종료 합니다. 이 hello 서비스 코드를 업그레이드 하는 중, tooload 분산 인해 hello 서비스 인스턴스를 이동 하는 일시적인 오류 검색 될 때 발생할 수 있습니다. OnCloseAsync 수 수 사용된 toosafely 닫고 모든 리소스, 백그라운드 처리를 중지, 외부 상태를 저장 또는 기존 연결을 종료 합니다.
* `void OnAbort() - C# / void onAbort() - Java`OnAbort는 hello 상태 비저장 서비스 인스턴스가 강제로 종료 될 때 호출 됩니다. 이 서비스 패브릭 toointernal 오류 인해 hello 서비스 인스턴스 수명 주기를 안정적으로 관리할 수 없는 경우 또는 hello 노드 영구 오류가 발견 되 면 일반적으로 호출 됩니다.

## <a name="stateful-service-replica-lifecycle"></a>상태 저장 서비스 복제본 수명 주기

> [!NOTE]
> 상태 저장 Reliable Services는 Java에서 아직 지원되지 않습니다.
>
>

상태 저장 서비스 복제본의 수명 주기는 상태 비저장 서비스 인스턴스보다 훨씬 더 복잡합니다. 또한 tooopen, 닫고, 중단할 이벤트, 상태 저장 서비스 복제본의 수명 동안 역할 변경 수행 합니다. 상태 저장 서비스 복제본 역할 변경 되 면 hello `OnChangeRoleAsync` 이벤트가 발생 합니다.

* `Task OnChangeRoleAsync(ReplicaRole, CancellationToken)`OnChangeRoleAsync는 hello 상태 저장 서비스 복제본 역할, 예: tooprimary 또는 보조 복제본이 변경 될 때 호출 됩니다. 주 복제본에는 쓰기 상태가 제공 됩니다 (toocreate 수 및 tooReliable 컬렉션 쓰기). 보조 복제본에는 읽기 상태가 지정됩니다(신뢰할 수 있는 기존 컬렉션에서 읽기만 가능). 상태 저장 서비스에서 대부분 작업 hello 주 복제본에서 수행 됩니다. 보조 복제본은 읽기 전용 유효성 검사, 보고서 생성, 데이터 마이닝 또는 다른 읽기 전용 작업을 수행할 수 있습니다.

상태 저장 서비스의 hello 주 복제본만 toostate 쓰기 권한을 가지 며 따라서 hello 서비스에서 실제 작업을 수행할 때 일반적으로 hello `RunAsync` hello 상태 저장 서비스 복제본이 주 하는 경우에 상태 저장 서비스의 메서드를 실행 합니다. hello `RunAsync` 메서드 hello 중은 물론에서 기본 데이터베이스로 주 복제본의 역할 변경 닫고 이벤트를 중단 하는 경우 취소 됩니다.

Hello를 사용 하 여 `OnChangeRoleAsync` 이벤트 하면 복제본의 역할에 따라도 응답 toorole 변경 에서처럼 tooperform 작업 수 있습니다.

상태 저장 서비스도도 제공 동일한 4 hello 수명 주기 이벤트는 상태 비저장 서비스와 동일한 의미 체계 hello 및 사용 사례:

```csharp
* Task OnOpenAsync(IStatefulServicePartition, CancellationToken)
* Task OnCloseAsync(CancellationToken)
* void OnAbort()
```

## <a name="next-steps"></a>다음 단계
고급 항목 관련된 tooService 패브릭, hello 다음 문서를 참조 하십시오.

* [상태 저장 Reliable Services 구성](service-fabric-reliable-services-configuration.md)
* [서비스 패브릭 상태 소개](service-fabric-health-introduction.md)
* [문제 해결을 위해 시스템 상태 보고서 사용](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [Hello 서비스 패브릭 클러스터 리소스 관리자를 사용 하 여 서비스 구성](service-fabric-cluster-resource-manager-configure-services.md)
