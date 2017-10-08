---
title: "테스트 용이성: 서비스 통신 | Microsoft Docs"
description: "서비스 간 통신은 서비스 패브릭 응용 프로그램의 중요 한 통합점입니다. 이 문서에서는 설계 고려 사항 및 테스트 기술에 대해 설명합니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 017557df-fb59-4e4a-a65d-2732f29255b8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 4a8f941c1e8e641384a9ee3a1149dabaaf9983cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-testability-scenarios-service-communication"></a>서비스 패브릭 테스트 용이성 시나리오: 서비스 통신
Azure 서비스 패브릭에서 마이크로 서비스 및 서비스 지향 아키텍처 스타일이 자연스럽게 드러납니다. 이러한 종류의 분산된 아키텍처에서 마이크로 서비스 구성 요소화 된 응용 프로그램 여러 해야 하는 서비스 tootalk tooeach 다른 일반적으로 구성 됩니다. 가장 간단한 경우에 hello 하면 일반적으로 상태 비저장 웹 서비스 및 toocommunicate 해야 하는 상태 저장 데이터 저장소 서비스.

서비스 간 통신 응용 프로그램의 중요 한 통합 지점이 되므로 각 서비스는 원격 API tooother 서비스를 노출 합니다. I/O와 관련된 API 경계 집합을 사용하여 작업하려면 일반적으로 적절한 테스트 및 유효성 검사가 필요합니다.

이러한 서비스 경계는 분산된 시스템에 함께 연결 하는 경우 다양 한 고려 사항 toomake 가지 있습니다.

* *전송 프로토콜*. 상호 운용성을 높이기 위해 HTTP를 사용할까요 아니면 처리량을 극대화하기 위해 사용자 지정 이진 프로토콜을 사용할까요?
* *오류 처리*. 영구 및 임시 오류는 어떻게 처리되나요? 서비스가 tooa 다른 노드로 이동 하는 경우 어떻게?
* *제한 시간 및 대기 시간*. 다중 계층 응용 프로그램에서 각 서비스 계층 처리 하는 방법을 통해 hello 스택과 toohello 사용자 대기 시간?

Hello 기본 제공 서비스 통신 구성 요소를 서비스 패브릭에서 제공 하는 중 하나를 사용 하거나 직접 작성에서 응용 프로그램에서 중요 한 tooensuring 복원 력을 서비스 간의 hello 상호 작용을 테스트 합니다.

## <a name="prepare-for-services-toomove"></a>서비스 toomove 준비
서비스 인스턴스는 시간이 지남에 따라 이동할 수 있습니다. 사용자 지정된 최적의 리소스 균형에 대한 부하 메트릭을 사용하여 구성된 경우에 특히 그렇습니다. 서비스 패브릭 서비스 인스턴스 toomaximize 가능성 업그레이드, 장애 조치, 수평 및 분산된 시스템 hello 기간 동안 발생 하는 기타 상황 중에 이동 합니다.

서비스는 hello 클러스터에서 이동, 클라이언트 및 기타 서비스 있어야 준비 toohandle 두 가지 시나리오 tooa 서비스를 설명 하는 경우:

* hello 서비스 인스턴스 또는 파티션의 복제본 hello tooit 설명이 마지막 시간 이후 이동 되었습니다. 서비스 기간의 정상적인 일부 이며 응용 프로그램의 hello 수명 동안 예상된 toohappen 이어야 합니다.
* hello 서비스 인스턴스 또는 파티션의 복제본이 이동 하는 hello 프로세스입니다. 장애 조치 노드 tooanother 하나에서 서비스의 서비스 패브릭에서 매우 빠르게 수행 하지만에 있을 수 있습니다 지연 가용성 느린 toostart 경우 서비스의 hello 통신 구성 요소입니다.

시스템이 원활하게 실행되도록 이러한 시나리오를 정상적으로 처리하는 것이 중요합니다. toodo 따라서 염두에입니다.

* 연결 된 toohas 일 수 있는 모든 서비스는 *주소* 를 (예: HTTP 또는 Websocket)에서 수신 대기 합니다. 서비스 인스턴스 또는 파티션이 이동하면 주소 끝점이 변경됩니다. (다른 IP 주소로 tooa 다른 노드로 이동 합니다.) Hello 기본 제공 통신 구성 요소를 사용 하는 경우 사용자에 대 한 서비스 주소를 확인 하 고 다시 처리 될 합니다.
* 있을 수 있습니다는 임시 해당 수신기를 hello 서비스 인스턴스가 시작 될 때 서비스 대기 시간 증가 다시 합니다. 이 hello 서비스 인스턴스를 이동한 후 hello 서비스 hello 수신기 열립니다 속도에 따라 다릅니다.
* 모든 기존 연결은 toobe hello 서비스에 새 노드를 연 후 닫았다가 필요 합니다. 정상적인 노드 종료 또는 다시 시작 하면 기존 연결 toobe 정상적으로 종료.

### <a name="test-it-move-service-instances"></a>테스트: 서비스 인스턴스 이동
서비스 패브릭의 테스트 용이성 도구를 사용 하 여 다양 한 방식에서 테스트 시나리오 tootest에 이러한 상황이 작성할 수 있습니다.:

1. 상태 저장 서비스의 주 복제본을 이동합니다.
   
    hello 주 복제본의 상태 저장 서비스의 파티션 이동할 수 있습니다에 대 한 여러 가지 이유로. 특정 파티션에 toosee 서비스 react toohello 매우 제어 된 방식으로 이동 하는 방법의이 tootarget hello 주 복제본을 사용 합니다.
   
    ```powershell
   
    PS > Move-ServiceFabricPrimaryReplica -PartitionId 6faa4ffa-521a-44e9-8351-dfca0f7e0466 -ServiceName fabric:/MyApplication/MyService
   
    ```
2. 노드를 중지합니다.
   
    노드 중지 되 면 hello의 모든 서비스 인스턴스 또는 해당 노드 tooone의에 있던 파티션을 이동 합니다. 서비스 패브릭 hello hello 클러스터의 다른 사용 가능한 노드. 이 경우 노드는 클러스터에서 손실 toomove가 모든 hello 서비스 인스턴스 및 해당 노드의 복제본이이 tootest를 사용 합니다.
   
    Hello PowerShell을 사용 하 여 노드를 중지할 수 있습니다 **중지 ServiceFabricNode** cmdlet:
   
    ```powershell
   
    PS > Restart-ServiceFabricNode -NodeName Node_1
   
    ```

## <a name="maintain-service-availability"></a>서비스 가용성 유지 관리
플랫폼 서비스 패브릭 설계 된 tooprovide 고가용성 서비스의 크기는입니다. 그러나 극단적인 상황에서 기본 인프라 문제로 인해 서비스 제공이 중단될 수 있습니다. 너무는 이러한 시나리오에 대 한 중요 한 tootest입니다.

상태 저장 서비스 가용성을 높이기 위한 쿼럼 기반 시스템 tooreplicate 상태를 사용합니다. 이 복제본의 쿼럼 toobe 사용할 수 있는 tooperform 쓰기 작업을 해야 함을 의미 합니다. 매우 드물기는 해도 광범위한 하드웨어 오류와 같이 복제본의 쿼럼을 사용할 수 없는 경우가 아주 가끔 있습니다. 이러한 경우 수 tooperform 쓰기 작업 수 있지만 읽기 작업 수 tooperform 계속 됩니다.

### <a name="test-it-write-operation-unavailability"></a>테스트: 쓰기 작업 사용 불가
서비스 패브릭에서 hello 테스트 용이성 도구를 사용해 테스트로 쿼럼 손실을 적용 하는 오류를 주입할 수 있습니다. 이러한 시나리오는 드물지만이 클라이언트와 상태 저장 서비스에 종속 된 서비스 요청 tooit 쓰기를 만들 수 없습니다 것 toohandle 상황에 준비 되어 있는지 중요 합니다. Hello 상태 저장 서비스 자체는이 가능성을 인식 하 고 정상적으로 통신할 수 것 toocallers 이기도 합니다.

쿼럼 손실 hello PowerShell을 사용 하 여 실행할 수 있습니다 **Invoke ServiceFabricPartitionQuorumLoss** cmdlet:

```powershell

PS > Invoke-ServiceFabricPartitionQuorumLoss -ServiceName fabric:/Myapplication/MyService -QuorumLossMode QuorumReplicas -QuorumLossDurationInSeconds 20

```

이 예제 설정 `QuorumLossMode` 너무`QuorumReplicas` tooinduce 쿼럼 손실 모든 복제를 중단 하지 않고 원하는 tooindicate 합니다. 이러한 방식으로 읽기 작업은 여전히 가능합니다. 전체 파티션을 사용할 수 없으면 시나리오 tootest 너무이 스위치를 설정할 수 있습니다`AllReplicas`합니다.

## <a name="next-steps"></a>다음 단계
[테스트 용이성 작업에 대한 자세한 정보](service-fabric-testability-actions.md)

[테스트 용이성 시나리오에 대한 자세한 정보](service-fabric-testability-scenarios.md)

