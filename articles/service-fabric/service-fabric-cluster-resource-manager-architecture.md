---
title: "관리자 아키텍처 aaaResource | Microsoft Docs"
description: "서비스 패브릭 클러스터 리소스 관리자의 아키텍처 개요"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 6c4421f9-834b-450c-939f-1cb4ff456b9b
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 9ea80273d0566a2ac25143ada3662875656b57b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="cluster-resource-manager-architecture-overview"></a>클러스터 리소스 관리자 아키텍처 개요
hello 서비스 패브릭 클러스터 리소스 관리자는 hello 클러스터에서 실행 되는 중앙 서비스입니다. 존중 tooresource 소비 및 모든 배치 규칙을 사용한 특히 hello 클러스터에서 hello 서비스의 원하는 hello 상태를 관리합니다. 

toomanage hello 클러스터 리소스를, hello 서비스 패브릭 클러스터 리소스 관리자는 여러 가지 정보가 있어야 합니다.

- 현재 존재하는 서비스
- 각 서비스의 현재(또는 기본) 리소스 소비량 
- hello 남아 있는 클러스터 용량 
- hello 용량 hello hello 클러스터 노드 
- 각 노드에서 사용 되는 리소스의 hello 양

지정된 된 서비스의 리소스 소비량 hello 시간이 지남에 따라 변경 하 고 서비스는 일반적으로 한 가지 이상 유형의 리소스에 대 한 처리. 다른 서비스에 있는 실제 물리적 리소스와 물리적 리소스를 모두 측정하고 있을 수 있습니다. 서비스는 메모리 및 디스크 소비와 같은 물리적 메트릭을 추적할 수 있습니다. 일반적으로 서비스는 "WorkQueueDepth" 또는 "TotalRequests"와 같은 논리 메트릭을 고려할 수 있습니다. 논리 / 물리 메트릭 hello에 사용할 수 있습니다 동일한 클러스터입니다. 메트릭 많은 서비스에서 공유할 수 또는 특정 tooa 특정 서비스 여야 합니다.

## <a name="other-considerations"></a>기타 고려 사항
hello 소유자 및 hello 클러스터의 연산자 다를 수 있습니다 서비스 및 응용 프로그램 작성자 hello 또는 최소 a가에서 환영 같은 다른 hats 착용 사람입니다. 응용 프로그램을 개발할 때는 필요한 사항을 알 것입니다. 예상 있는 hello의을 사용 하는 리소스 및 여러 서비스를 배포 해야 합니다. 예를 들어 hello 웹 계층 hello 데이터베이스 서비스 하지 않아야 하는 동안 인터넷에 노출 하는 노드 toohello에 toorun이 필요 합니다. 또 다른 예로, CPU 및 메모리 및 디스크 사용량에 대 한 hello 데이터 계층 서비스 주의 하는 동안 네트워크에서 hello 웹 서비스 아마도 제한 됩니다. 그러나 프로덕션 환경에서 해당 서비스에 대 한 라이브 사이트 인시던트 또는 업그레이드 toohello 서비스를 관리 하는 사용자를 처리 하는 hello 사람이 서로 다른 작업 toodo 개이고 다양 한 도구를 필요로 합니다. 

Hello 클러스터와 서비스 둘 다은 고정 되지 않고

- hello hello 클러스터의 노드 수가 수 확장 및 축소
- 다양한 크기 및 형식의 노드는 오갈 수 있습니다.
- 서비스를 생성, 제거할 수 있고 원하는 리소스 할당 및 배치 규칙을 변경할 수 있습니다.
- 업그레이드 또는 기타 관리 작업 hello 응용 프로그램에서 hello 클러스터 통해 인프라 수준에서 롤백될 수 있습니다.
- 언제든지 실패할 수 있습니다.

## <a name="cluster-resource-manager-components-and-data-flow"></a>클러스터 리소스 관리자 구성 요소 및 데이터 흐름
hello 클러스터 리소스 관리자는 해당 서비스 내에서 각 서비스 개체에 의해 리소스의 각 서비스 및 hello 소비의 tootrack hello 요구 사항에 있습니다. hello 클러스터 리소스 관리자는 개념적 두 부분으로 이루어져: 노드마다 및 내결함성 / 서비스에서 실행 되는 에이전트입니다. 각 노드 트랙 부하에 hello 에이전트, 서비스, 집계에서 보고 하 고 주기적으로 보고 합니다. hello 클러스터 리소스 관리자 서비스는 hello 로컬 에이전트에서 모든 hello 정보를 수집 및 현재 구성에 따라 반응 합니다.

다음 다이어그램 hello를 살펴보겠습니다.

<center>
![리소스 분산 장치 아키텍처][Image1]
</center>

런타임 중에 많은 내용이 변경될 수 있습니다. 예를 들어 hello 양 가정해 일부 서비스 리소스의 변경 내용을 일부 서비스 장애를 사용 하 고 일부 노드가 참가 하 고 hello 클러스터를 떠날 합니다. 노드의 모든 hello 변경 집계 하 고 주기적으로 toohello 클러스터 리소스 관리자 서비스 (1, 2)를 다시 집계, 분석 되며 저장 됩니다. 서비스 hello 변경 찾은 동작이 필요 여부를 결정 하는 몇 초 마다 (3). 예를 들어 비어 있는 일부 노드는 toohello 클러스터 추가 되었음을 확인할 수 없습니다. 결과적으로, toomove 일부 서비스 toothose 노드 결정합니다. hello 클러스터 리소스 관리자 수도 확인 특정 노드의 오버 로드 되었거나 특정 서비스가 실패 했거나 삭제 되었거나, 다른 위치에서 리소스를 확보 합니다.

보겠습니다 다이어그램을 다음 hello와 다음을 참조 하십시오. 보겠습니다 예를 들어 해당 hello 클러스터 리소스 관리자 결정 변경 내용이 필요 합니다. 다른 시스템 (특정 hello Failover Manager)에서 서비스 toomake hello 필요한 변경 내용으로 조정합니다. 그런 다음 필요한 명령은 hello toohello 적절 한 노드 (4) 전송 됩니다. 예를 들어 리소스 관리자 발견 Node5가 오버 로드 하 고 있으므로 Node5 tooNode4에서 toomove 서비스 B를 결정 하는 hello를 가정해 봅니다. Hello 재구성 (5)의 hello 끝 hello 클러스터는 다음과 같습니다.

<center>
![리소스 분산 장치 아키텍처][Image2]
</center>

## <a name="next-steps"></a>다음 단계
- 클러스터 리소스 관리자 hello에 hello 클러스터를 설명 하는 많은 옵션이 있습니다. toofind에 대 한 자세한 내용을 확인해이 문서에 [서비스 패브릭 클러스터를 설명 하는](./service-fabric-cluster-resource-manager-cluster-description.md)
- hello 클러스터 리소스 관리자의 기본 임무는 hello 클러스터를 리 밸런스 및 배치 규칙을 적용 합니다. 이러한 동작은 구성하는 방법에 대한 자세한 내용은 [Service Fabric 클러스터 부하 분산](./service-fabric-cluster-resource-manager-balancing.md)을 참조하세요.

[Image1]:./media/service-fabric-cluster-resource-manager-architecture/Service-Fabric-Resource-Manager-Architecture-Activity-1.png
[Image2]:./media/service-fabric-cluster-resource-manager-architecture/Service-Fabric-Resource-Manager-Architecture-Activity-2.png
