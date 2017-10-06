---
title: "Azure microservices aaaSpecify 메트릭 및 배치 설정을 | Microsoft Docs"
description: "메트릭, 배치 제약 조건 및 기타 배치 정책을 지정하여 Service Fabric 서비스를 설명합니다."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 16e135c1-a00a-4c6f-9302-6651a090571a
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: c633518b5dbf0c7b84e0d46c06bf1f92365d184d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-cluster-resource-manager-settings-for-service-fabric-services"></a>Service Fabric 서비스에 대한 클러스터 리소스 관리자 설정 구성
서비스 패브릭 클러스터 리소스 관리자 hello service 라는 모든 개인을 제어 하는 hello 규칙 보다 세부적으로 제어할 수 있습니다. 명명 된 각 서비스는 hello 클러스터에 할당 되는 방법에 대 한 규칙을 지정할 수 있습니다. 명명 된 각 서비스 hello 메트릭 집합을 브로드캐스트하며 toothat 서비스는 얼마나 중요 한지를 포함 하 여 tooreport 정의할 수도 있습니다. 서비스 구성은 세 가지 작업으로 구분됩니다.

1. 배치 제약 조건 구성
2. 메트릭 구성
3. 고급 배치 정책 및 기타 규칙 구성(덜 일반적임)

## <a name="placement-constraints"></a>배치 제약 조건
배치 제약 조건은 hello 클러스터의 노드는 서비스 실제로 실행 수 toocontrol 사용된 됩니다. 일반적으로 특정 서비스 인스턴스 또는 노드는 특정 형식에서 제한 된 지정 된 형식 toorun의 모든 서비스의 이름은입니다. 배치 제약 조건은 확장할 수 있습니다. 노드 형식별로 모든 속성 집합을 정의한 다음 서비스를 만들 때 제약 조건이 포함된 속성을 선택할 수 있습니다. 또한 서비스가 실행되는 동안 서비스의 배치 제약 조건을 변경할 수도 있습니다. 이렇게 하면 toorespond toochanges hello 클러스터 또는 hello 서비스의 hello 요구 사항에 있습니다. 지정 된 노드의 hello 속성 hello 클러스터에 동적으로 업데이트 될 수도 있습니다. 배치 제약 조건 및 어떻게 tooconfigure 하에서 확인할 수 있습니다에 자세한 내용은 [이 문서](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints)

## <a name="metrics"></a>메트릭
메트릭은 hello에 지정된 된 명명 된 서비스에 필요한 리소스 집합이 있습니다. 서비스의 메트릭 구성에는 기본적으로 해당 서비스의 상태 저장 복제본 또는 상태 비저장 인스턴스 각각이 서비하는 리소스의 크기가 포함됩니다. 메트릭에 절충 작업 들이 필요한 경우에 toothat 서비스는 해당 메트릭이 분산 중요도 나타내는 가중치도 포함 합니다.

## <a name="advanced-placement-rules"></a>고급 배치 규칙
덜 일반적인 시나리오에서 유용한 다른 유형의 배치 규칙이 있습니다. 일부 사례:
- 지리적으로 분산된 클러스터를 지원하는 제약 조건
- 특정 응용 프로그램 아키텍처

다른 배치 규칙은 상관 관계 또는 정책을 통해 구성됩니다.

## <a name="next-steps"></a>다음 단계
- 메트릭은 hello 서비스 패브릭 클러스터 리소스 관리자에서 소비 되 고 hello 클러스터의 용량을 관리 하는 방식입니다. 메트릭에 대 한 자세한 toolearn 어떻게 tooconfigure, 체크 아웃 및 [이 문서](service-fabric-cluster-resource-manager-metrics.md)
- 선호도는 서비스에 대해 구성할 수 있는 하나의 모드입니다. 일반적이지 않지만 필요한 경우 [여기](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)
- 서비스 toohandle 추가 시나리오에서 구성할 수 있는 여러 다른 배치 규칙이 있습니다. 이러한 기타 배치 정책은 [여기](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)
- Hello 처음부터 시작 하 고 [소개 toohello 서비스 패브릭 클러스터 리소스 관리자 가져오기](service-fabric-cluster-resource-manager-introduction.md)
- toofind 아웃 hello 클러스터 리소스 관리자를 관리 하 고 hello 클러스터의 로드 균형을 조정 하는 방법에 체크 아웃 hello 문서에 [부하 분산](service-fabric-cluster-resource-manager-balancing.md)
- 클러스터 리소스 관리자 hello에 hello 클러스터를 설명 하는 많은 옵션이 있습니다. toofind에 대 한 자세한 내용을 확인해이 문서에 [서비스 패브릭 클러스터를 설명 하는](service-fabric-cluster-resource-manager-cluster-description.md)
