---
title: "서비스 패브릭 서비스의 aaaAvailability | Microsoft Docs"
description: "서비스에 대한 오류 검색, 장애 조치(Failover) 및 복구를 설명합니다."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 279ba4a4-f2ef-4e4e-b164-daefd10582e4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: c443aadfe31a1413359b08d34c4b7dd5db4edd16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-of-service-fabric-services"></a>서비스 패브릭 서비스의 가용성
이 문서에서는 Service Fabric이 서비스의 가용성을 유지하는 방법에 대한 개요를 설명합니다.

## <a name="availability-of-service-fabric-stateless-services"></a>서비스 패브릭 상태 비저장 서비스의 가용성
Azure 서비스 패브릭 서비스는 상태 저장 또는 상태 비저장이 모두 될 수 있습니다. 상태 비저장 서비스는 포함 하지 않는 응용 프로그램 서비스 [로컬 상태](service-fabric-concepts-state.md) 항상 사용할 수 있으며 신뢰할 수 있는 toobe 보내야 합니다.

상태 비저장 서비스를 만들려면 `InstanceCount`를 정의해야 합니다. hello 인스턴스 수는 hello hello 클러스터에서 실행 해야 하는 hello 상태 비저장 서비스의 응용 프로그램 논리의 인스턴스 수를 정의 합니다. Hello 인스턴스 수를 늘리면 hello 상태 비저장 서비스 확장 방법이 권장 됩니다.

상태 비저장 서비스 명명 된 인스턴스의 실패 한 경우 hello 클러스터의 적격 일부 노드는 새 인스턴스가 만들어집니다. 예를 들어 상태 비저장 서비스 인스턴스는 Node1에서 실패하고 Node5에서 다시 만들어질 수 있습니다.

## <a name="availability-of-service-fabric-stateful-services"></a>서비스 패브릭 상태 저장 서비스의 가용성
상태 저장 서비스에는 이와 관련된 일부 상태가 있습니다. 서비스 패브릭에서 상태 저장 서비스는 복제본 세트로 모델링됩니다. 각 복제본은 해당 서비스에 대 한 hello 상태의 복사본에도 있는 hello 서비스의 hello 코드의 실행 중인 인스턴스입니다. 하나의 복제본 (주 hello 라고 함)에서 읽기 및 쓰기 작업이 수행 됩니다. 쓰기 작업에서 변경 내용을 toostate는 *복제* toohello hello 복제 세트 (활성 보조 데이터베이스 라고 함)의 다른 복제본 적용 합니다. 

주 복제본은 하나만 있을 수 있지만 활성 보조 복제본은 여러 개가 있을 수 있습니다. 활성 보조 복제본의 hello 수, 구성 가능 하며 복제본 수가 많을 수록 동시 소프트웨어 및 하드웨어 오류 수를 더를 허용할 수 있습니다.

Hello 주 복제본의 작동이 서비스 패브릭 hello 활성 보조 복제본 hello 새로운 주 복제본 중 하나를 수행 합니다. 활성 보조 복제본이 이미 업데이트 hello 버전의 hello 상태가 (통해 *복제*), 계속 해 서 추가 읽기를 처리 하 고 쓰기 작업 수 및 합니다.

이 개념을 되는 주 가상 컴퓨터 또는 활성 보조 복제본의 복제 역할 hello 라고 합니다.

### <a name="replica-roles"></a>복제본 역할
복제본의 hello 역할은 해당 복제본에 의해 관리 되는 hello 상태의 사용 되는 toomanage hello 수명 주기 합니다. 주 역할의 복제본은 읽기 요청을 서비스합니다. 또한 hello 주 상태를 업데이트 한 hello 변경 내용을 복제 하 여 모든 쓰기 요청을 처리 합니다. 이러한 변경은 hello 복제 세트에 적용 된 toohello 활성 보조입니다. hello는 활성 보조는 주 복제본을 hello tooreceive 상태의 변경 내용을 복제 되었는지 및 hello 상태 보기를 업데이트 합니다.

> [!NOTE]
> 더 높은 수준의 프로그래밍와 같은 모델 [Reliable Actors](service-fabric-reliable-actors-introduction.md) 및 [신뢰할 수 있는 서비스](service-fabric-reliable-services-introduction.md) hello 개발자의 복제 역할의 hello 개념을 숨깁니다. 작업자 역할의 hello 개념은 거의 대부분의 시나리오에 대 한 간소화 된 서비스에서 하는 동안 필요 하지 않습니다.
>

## <a name="next-steps"></a>다음 단계
서비스 패브릭 개념에 대 한 자세한 내용은 다음 문서는 hello 참조:

- [Service Fabric 서비스 크기 조정](service-fabric-concepts-scalability.md)
- [서비스 패브릭 서비스 분할](service-fabric-concepts-partitioning.md)
- [상태 정의 및 관리](service-fabric-concepts-state.md)
- [Reliable Services](service-fabric-reliable-services-introduction.md)
