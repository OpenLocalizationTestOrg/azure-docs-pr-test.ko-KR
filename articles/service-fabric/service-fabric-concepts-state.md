---
title: "aaaDefinine Azure microservices에서 상태를 관리 하 고 | Microsoft Docs"
description: "어떻게 toodefine 서비스 패브릭에서 서비스 상태를 관리 하 고"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f5e618a5-3ea3-4404-94af-122278f91652
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 4a24696da71753d0f343a86df3556b5b7c964834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-state"></a>서비스 상태
**서비스 상태** toohello 메모리 나 디스크 데이터 서비스 toofunction 필요 함을 의미 합니다. 포함, 예를 들어 hello 데이터 구조와 멤버 변수가 해당 hello 서비스 읽기 및 쓰기 toodo 작업 합니다. Hello 서비스의 구성 방식에 따라 파일이 나 디스크에 저장 되어 있는 다른 리소스도 포함할 수 있습니다. 예를 들어 데이터베이스 파일을 hello toostore 데이터와 트랜잭션 로그를 사용 합니다.

예제 서비스로 계산기를 생각해 보겠습니다. 기본 계산기 서비스는 두 개의 숫자를 받아 그 합계를 반환합니다. 이러한 계산 수행에는 멤버 변수나 기타 정보가 관련되지 않습니다.

이제 고려해 동일한 계산기 hello 하지만 계산 않은 저장 및 hello 마지막 합계를 반환 하기 위한 추가 메서드를 사용 합니다. 이 서비스는 이제 상태를 저장합니다. 상태 저장 toowhen 새 합을 계산 하 고 tooreturn hello 마지막 계산 된 합계를 요청할 때에서 읽고 쓸 수 있는 몇 가지 상태를 포함 하는 것을 의미 합니다.

Azure 서비스 패브릭 hello 첫 번째 서비스는 상태 비저장 서비스를 라고 합니다. hello 두 번째 서비스는 상태 저장 서비스를 라고 합니다.

## <a name="storing-service-state"></a>서비스 상태 저장
상태는 표면화 또는 hello 상태를 조작 하는 hello 코드와 함께 있을 수 있습니다. 상태의 표면화는 일반적으로 외부 데이터베이스를 사용 하 여 수행 하거나 hello 네트워크를 통해 또는 out of process에 서로 다른 컴퓨터에서 실행 hello 동일한 컴퓨터를 다른 데이터 저장소. 계산기 예에서 hello 데이터 저장소에 SQL 데이터베이스 또는 Azure 테이블 저장소의 인스턴스 수 있습니다. 모든 요청 toocompute hello sum이이 데이터에 대 한 업데이트를 수행 하 고 hello 저장소에서 인출 되 고 hello 현재 값에서 toohello 서비스 tooreturn hello 값 결과 요청 합니다. 

상태는 hello 상태를 조작 하는 hello 코드 함께 배치할 수도 있습니다. Service Fabric의 상태 저장 서비스는 일반적으로 이 모델을 사용하여 빌드됩니다. 서비스 패브릭 hello 인프라 tooensure이이 상태는 항상 사용 가능한 일관성 및 내 구성을 가집니다 및 hello 서비스를 이러한 방식으로 작성할 수 있는지 쉽게 확장할 수를 제공 합니다.

## <a name="next-steps"></a>다음 단계
서비스 패브릭 개념에 대 한 자세한 내용은 다음 문서는 hello 참조:

* [서비스 패브릭 서비스의 가용성](service-fabric-availability-services.md)
* [서비스 패브릭 서비스의 확장성](service-fabric-concepts-scalability.md)
* [서비스 패브릭 서비스 분할](service-fabric-concepts-partitioning.md)
* [Service Fabric Reliable Services](service-fabric-reliable-services-introduction.md)
