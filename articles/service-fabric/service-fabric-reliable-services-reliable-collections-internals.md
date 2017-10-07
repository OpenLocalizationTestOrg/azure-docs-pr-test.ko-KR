---
title: "서비스 패브릭 신뢰할 수 있는 상태 관리자 및 신뢰할 수 있는 컬렉션 내부 aaaAzure | Microsoft Docs"
description: "신뢰할 수 있는 컬렉션 개념 및 Azure Service Fabric의 디자인에 대해 자세히 알아봅니다."
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 651bfb52785a2475e4840cd471e87220d1936391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a>Azure Service Fabric 신뢰할 수 있는 상태 관리자 및 신뢰할 수 있는 컬렉션 내부
이 문서는 hello 백그라운드 핵심 구성 요소가 작동 하는 방법을 신뢰할 수 있는 상태 관리자 및 신뢰할 수 있는 컬렉션 toosee 내를 자세히 설명 합니다.

> [!NOTE]
> 이 문서는 진행 중입니다. 주석 toothis 문서 tootell us 추가 주제 선택에 대 한 자세한 toolearn 합니다.
>

##  <a name="local-persistence-model-log-and-checkpoint"></a>로컬 지속성 모델: 로그 및 검사점
신뢰할 수 있는 상태 관리자 hello 및 신뢰할 수 있는 컬렉션 로그 및 검사점 라고 하는 지 속성 모델을 따릅니다.
이 모델에서 각 상태 변경은 먼저 디스크에 기록된 후 메모리에 적용됩니다.
hello 완료 상태 자체 (규칙 하위 유지 가끔씩만 검사점).
hello 이점은 델타 순차적 추가 전용 디스크에 대 한 쓰기 성능 향상된으로 설정 되어입니다.

toobetter는 hello 로그 및 검사점 모델을 먼저 살펴보겠습니다 hello 무한 디스크 시나리오.
신뢰할 수 있는 상태 관리자 hello 복제 되기 전에 모든 작업을 기록 합니다.
로깅에는 메모리에만 hello 신뢰할 수 있는 컬렉션 tooapply hello 작업을 수 있습니다.
로그는 유지 않으므로 hello 복제 실패 하 고 다시 시작 되 면 toobe 필요한 경우에 hello 신뢰할 수 있는 상태 관리자는 작업이 충분 한 정보에서 해당 로그 tooreplay 모든 hello hello 복제본 끊어졌습니다입니다.
Hello 디스크 유한 아니므로 로그 레코드가 제거 toobe 필요 하며 hello 신뢰할 수 있는 컬렉션 toomanage 유일한 hello 메모리 상태 합니다.

이제 hello 유한 디스크 시나리오를 살펴보겠습니다.
로그 레코드가 누적 hello 신뢰할 수 있는 상태 관리자는 디스크 공간 부족 실행 됩니다.
먼저 발생 하는 hello 신뢰할 수 있는 상태 관리자 해야 tootruncate hello 최신 레코드를 위한 해당 로그 toomake 공간.
신뢰할 수 있는 컬렉션 toocheckpoint의 메모리 내 상태 toodisk을 hello 하는 안정성 상태 관리자 요청 합니다.
이 시점에서 hello 신뢰할 수 있는 컬렉션의 메모리 상태를 유지 합니다.
해당 검사점을 완료 하는 hello 신뢰할 수 있는 컬렉션 hello 신뢰할 수 있는 상태 관리자 hello 로그 toofree 디스크 공간을 자를 수 있습니다.
Hello 복제본 toobe 다시 시작 하면 신뢰할 수 있는 컬렉션 검사점 상태를 복구한 hello 신뢰할 수 있는 상태 관리자 복구 하 고 hello 마지막 검사점 이후에 발생 한 모든 hello 상태 변화를 재생 합니다.

검사점에 다른 값이 추가되면 일반적인 시나리오에서 복구 시간이 개선됩니다. 로그는 hello 마지막 검사점 이후 발생 한 모든 작업을 포함 합니다.
따라서 신뢰할 수 있는 사전에서 지정된 행에 대한 여러 값과 같이 항목의 여러 버전이 포함될 수 있습니다.
반면에 신뢰할 수 있는 컬렉션 검사점 키에 대 한 각 값의 최신 버전을만 hello 합니다.

## <a name="next-steps"></a>다음 단계
* [트랜잭션 및 잠금](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

