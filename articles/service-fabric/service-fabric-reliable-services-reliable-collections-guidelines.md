---
title: "aaaGuidelines & Azure 서비스 패브릭에서 신뢰할 수 있는 컬렉션에 대 한 권장 사항 | Microsoft Docs"
description: "Service Fabric의 신뢰할 수 있는 컬렉션을 사용하기 위한 지침 및 권장 사항"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/3/2017
ms.author: mcoskun
ms.openlocfilehash: bcdbc9d013bc044e06c43761e7f515c7e4bf340c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="guidelines-and-recommendations-for-reliable-collections-in-azure-service-fabric"></a>Azure Service Fabric에서 신뢰할 수 있는 컬렉션에 대한 지침 및 권장 사항
이 섹션에서는 신뢰할 수 있는 상태 관리자 및 신뢰할 수 있는 컬렉션을 사용하기 위한 지침을 제공합니다. hello ´ ֲ toohelp 사용자가 일반적인 문제를 방지 합니다.

hello 지침 hello 용어 접두사로 추가 하는 간단한 권장 사항으로 구성 됩니다 *수행*, *고려*, *하지 말고* 및 *없는*합니다.

* 읽기 작업에 의해 반환되는 사용자 지정 형식의 개체(예: `TryPeekAsync` 또는 `TryGetValueAsync`)는 수정하지 마세요. 동시 컬렉션의 경우와 마찬가지로 신뢰할 수 있는 컬렉션 복사본이 아니라 참조 toohello 개체를 반환합니다.
* 수정 하기 전에 사용자 지정 된 형식의 개체를 반환 하는 전체 복사 hello를 수행 합니다. 구조체 및 기본 제공 형식 값으로 전달 되므로 toodo에 전체 복사본을 필요가 없습니다.
* 시간제한에 `TimeSpan.MaxValue` 를 사용하지 마세요. 제한 시간에 사용 되는 toodetect 교착 상태 여야 합니다.
* 트랜잭션을 커밋, 중단 또는 삭제한 후에는 사용하지 마십시오.
* 만든 hello 트랜잭션 범위 외부의 열거형을 사용 하지 마십시오.
* 다른 트랜잭션의 `using` 문 내에 트랜잭션을 만들지 마세요. 교착 상태가 발생할 수 있습니다.
* `IComparable<TKey>` 구현이 올바른지 확인하세요. hello 시스템 종속성은 `IComparable<TKey>` 검사점과 행을 병합 합니다.
* 업데이트 잠금을 사용 하 여 수행 함 tooupdate 있는 항목을 읽을 때 것 tooprevent 특정 유형의 교착 상태입니다.
* 80kb 아래 항목 (예: TKey + 신뢰할 수 있는 사전에 대 한 TValue) 유지를 하십시오: 더 작은 hello 합니다. 대형 개체 힙 사용량으로 디스크 및 네트워크 IO 요구 사항 hello 양을 감소 시킵니다. 종종 중복 데이터를 복제 하 여 작은 부분만 hello 값을 업데이트할 때 줄어듭니다. 일반적인 방법은 tooachieve이 신뢰할 수 있는 사전에는 toobreak에 행 toomultiple 행.
* 백업을 사용 하는 것이 좋습니다 하 고 toohave 재해 복구 기능을 복원 합니다.
* 단일 엔터티 작업 및 다중 엔터티 작업을 조합 하지 (예: `GetCountAsync`, `CreateEnumerableAsync`) hello에 toohello 다른 격리 수준이 인해 동일한 트랜잭션.
* InvalidOperationException을 처리합니다. 여러 가지 이유로 hello 시스템에 의해 사용자 트랜잭션은 중단할 수 있습니다. 예를 들어 hello 신뢰할 수 있는 상태 관리자가 해당 기본 역할을 변경 하는 경우 또는 장기 실행 트랜잭션이 hello 트랜잭션 로그의 잘림이 차단 합니다. 이러한 경우 트랜잭션이 이미 종료되었다는 InvalidOperationException이 표시될 수 있습니다. Hello 트랜잭션의 hello 종료 hello 사용자가 요청 되지 라고 가정할 경우, 가장 좋은 방법은 toohandle이이 예외는 toodispose hello 트랜잭션 hello 취소 토큰에서 신호 (또는 hello 복제본의 역할이 hello 변경 되었습니다) 되었는지 확인 하 고 없는 경우 새 트랜잭션을 만들고 다시 시도 합니다.  

유의 사항 tookeep 몇 가지 다음과 같습니다.

* hello 기본 제한 시간은 모든 hello 신뢰할 수 있는 컬렉션 Api에 대 한 4 초입니다. 대부분의 사용자는 hello 기본 제한 시간을 사용 해야 합니다.
* hello 기본 취소 토큰은 `CancellationToken.None` 신뢰할 수 있는 컬렉션의 모든 Api에서 합니다.
* 키 형식 매개 변수를 hello (*TKey*) 신뢰할 수 있는 사전 해야 올바르게 구현에 대 한 `GetHashCode()` 및 `Equals()`합니다. 키는 변경하지 않아야 합니다.
* hello 신뢰할 수 있는 컬렉션에 대 한 고가용성을 tooachieve, 각 서비스는 대상 및 최소 복제본 집합 크기의 3 이상 있어야 합니다.
* 보조 hello에 대 한 읽기 작업은 쿼럼 커밋 되지 않는 버전을 읽을 수 있습니다.
  즉, 단일 보조에서 읽은 데이터 버전은 거짓 처리될 수 있습니다.
  주에서 읽은 내용은 항상 안정적이며 거짓 처리될 수 없습니다.

### <a name="next-steps"></a>다음 단계
* [신뢰할 수 있는 컬렉션 작업](service-fabric-work-with-reliable-collections.md)
* [트랜잭션 및 잠금](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
* [신뢰할 수 있는 상태 관리자 및 컬렉션 내부](service-fabric-reliable-services-reliable-collections-internals.md)
* 데이터 관리
  * [백업 및 복원](service-fabric-reliable-services-backup-restore.md)
  * [Notifications](service-fabric-reliable-services-notifications.md)
  * [Serialization 및 업그레이드](service-fabric-application-upgrade-data-serialization.md)
  * [신뢰할 수 있는 상태 관리자 구성](service-fabric-reliable-services-configuration.md)
* 기타
  * [Reliable Services 빠른 시작](service-fabric-reliable-services-quick-start.md)
  * [신뢰할 수 있는 컬렉션에 대한 개발자 참조](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
