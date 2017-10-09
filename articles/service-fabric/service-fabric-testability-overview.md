---
title: "aaaFault Analysis Service 개요 | Microsoft Docs"
description: "이 문서에서는 오류를 발생 시켜 및 서비스에 대해 테스트 시나리오를 실행 하기 위한 hello 서비스 패브릭에서 오류 분석 서비스를 설명 합니다."
services: service-fabric
documentationcenter: .net
author: anmolah
manager: timlt
editor: vturecek
ms.assetid: 1f064276-293a-4989-a513-e0d0b9fdf703
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: anmola
ms.openlocfilehash: deac16ec830aa10d4e488e60691faa9ef2b6cd33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-fault-analysis-service"></a>소개 toohello 오류 분석 서비스
hello 오류 Analysis Service는 Microsoft Azure Service Fabric을 기반으로 하는 서비스를 테스트를 위해 설계 되었습니다. 오류 분석 서비스 hello로 의미 있는 오류를 유도 하 고 응용 프로그램에 대 한 전체 테스트 시나리오를 실행할 수 있습니다. 이러한 오류와 시나리오를 실행 하 고 유효성을 검사 hello 다양 한 상태 및 전환 하는 서비스는 제어 된, 안전 및 일관 된 방식으로 모두에 해당 수명 주기 동안 발생 합니다.

작업은 테스트에 대 한 서비스를 대상으로 하는 hello 개별 오류입니다. 서비스 개발자는이 방법으로 문서 블록 toowrite 복잡 한 시나리오를 사용할 수 있습니다. 예:

* 컴퓨터 또는 VM 다시 부팅 되는 경우 개수에 관계 없이 노드 toosimulate를 다시 시작 합니다.
* 상태 저장 서비스 toosimulate 부하 분산, 장애 조치 또는 응용 프로그램 업그레이드의 복제본을 이동 합니다.
* 상태 저장 서비스 toocreate 충분 한 "백업" 또는 "secondary" 복제본 tooaccept 새 데이터가 없기 때문 쓰기 작업을 계속할 수 없습니다 없는 상황에서 쿼럼이 손실 된를 호출 합니다.
* 상태 저장 서비스 toocreate 아웃 완전히 초기화 하는 모든 메모리 내 상태에 있는 상황에서 데이터 손실이 호출 합니다.

시나리오는 하나 이상의 작업으로 구성되는 복잡한 작업입니다. hello 오류 분석 서비스에서는 두 개의 기본 제공 완전 한 시나리오를 제공합니다.

* 비정상 상황 시나리오
* 장애 조치 시나리오

## <a name="testing-as-a-service"></a>Testing as a service
hello 오류 분석 서비스는 서비스 패브릭 시스템 서비스는 서비스 패브릭 클러스터를 자동으로 시작 됩니다. 이 서비스 오류 삽입, 테스트 시나리오 실행 및 상태 분석에 대 한 hello 호스트 역할을 합니다. 

![오류 분석 서비스  ][0]

오류 동작 또는 테스트 시나리오의 시작 된 경우에 명령이 toohello 오류 분석 서비스 toorun hello 오류 작업 또는 테스트 시나리오를 전송 됩니다. hello 오류 분석 서비스를 안정적으로 오류 및 시나리오를 실행 하 고 결과 확인 수 있도록 합니다. 예를 들어 hello 오류 분석 서비스에서 장기 실행 테스트 시나리오를 안정적으로 실행할 수 있습니다. 고 테스트 hello 클러스터 안에서 실행 되 고 있습니다, 때문에 hello 서비스 및 검사할 수 hello 클러스터의 hello 상태 서비스 tooprovide 실패에 대 한 자세한 내용은 합니다.

## <a name="testing-distributed-systems"></a>분산 시스템 테스트
서비스 패브릭 hello를 작성 하 고 작업을을 훨씬 쉽게 분산된 확장 가능한 응용 프로그램 관리를 만듭니다. 마찬가지로 보다 쉽게 배포 응용 프로그램을 테스트할 수 있습니다. hello 오류 분석 서비스입니다. Toobe 테스트 하는 동안 해결 해야 하는 세 가지 주요 문제 가지가 있습니다.

1. 실제 시나리오에서 발생할 수 있는 오류를 시뮬레이션/생성: 다양 한 오류를 분산된 응용 프로그램 toorecover 수 있다는 점 hello 서비스 패브릭의 중요 한 측면 중 하나입니다. 그러나 응용 프로그램 hello tootest은 이러한 오류 로부터 수 toorecover, 필요는 메커니즘 toosimulate/생성 통제 된 테스트 환경에서 이러한 실제 오류가 발생 했습니다.
2. hello 기능 toogenerate 오류 상관 관계가 지정 된: 네트워크 오류 및 컴퓨터 오류 같은 hello 시스템의 기본 오류 쉽게 tooproduce를 개별적으로 않습니다. 많은 수의 이러한 개별 오류의 hello 상호 작용의 결과로 hello 실제 상황에서 발생할 수 있는 시나리오를 생성 하는 것은 특수입니다.
3. 다양한 개발 및 배포 수준에서 통합되지 않은 환경: 다양한 실패 유형을 테스트할 수 있는 여러 오류 주입 시스템이 있습니다. 그러나 프로덕션 환경에서 테스트를 동일한 테스트 toousing 큰 테스트 환경에서 자신에 게 한 toorunning hello 하나 상자 개발자 시나리오에서 이동할 때 이러한 항목 모두에 hello 경험 좋지 않습니다.

있지만 많은 메커니즘 toosolve 이러한 문제를 필요한 보증-는 한 상자 개발자 환경에서 모든 hello 방법으로 동일한 hello 않는 시스템 tootest 프로덕션 클러스터에이 없습니다. hello 오류 분석 서비스는 hello 응용 프로그램 개발자가 비즈니스 논리를 테스트 하는 데 집중할 수 있습니다. 오류 분석 서비스 hello 모든 hello 기능 필요한 tootest hello와의 상호 작용 hello 서비스의 hello 기본 분산된 시스템을 제공 합니다.

### <a name="simulatinggenerating-real-world-failure-scenarios"></a>실제 오류 시나리오 시뮬레이션/생성
오류에 대 한 분산된 시스템의 tootest hello 견고성 메커니즘 toogenerate 실패 해야합니다. 이론적으로에 있는 동안 아래쪽 노드 hello 적중 되는 것을 시작 하기 쉬운 것 처럼 실패 동일 집합 생성의 일관성 문제 서비스 패브릭 toosolve 시도 하 합니다. 예를 들어 tooshut 노드를 중지 하려면 hello 필요한 워크플로 hello 다음:

1. Hello 클라이언트로부터 노드 종료 요청을 실행 합니다.
2. Hello 요청 toohello 올바른 노드를 보냅니다.
   
    a. Hello 노드가 없는 경우 오류가 발생 합니다.
   
    b. Hello 노드가 있으면 반환 해야만 hello 노드가 종료 된 경우.

테스트 관점에서 tooverify hello 실패 hello 테스트 tooknow이이 오류로 인해 발생 하는 경우 hello 오류가 실제로 발생 한다고 필요 합니다. 서비스 패브릭에서 제공 하는 hello 보증에는 hello 노드 중 하나가 작동이 중지 될 있거나 hello 명령 hello 노드에 도달 하면 아래로 이미은 합니다. 두 사례 hello에 테스트 해야 hello 상태에 대 한 수 toocorrectly 이유 수와 성공 하거나 실패 올바르게 유효성 검사에 합니다. 서비스 패브릭 toodo hello 수 적중 많은 네트워크, 하드웨어 및 소프트웨어 문제에서 제공 되지 않습니다는 hello 이전 보장 오류의 설정 같은 외부에서 구현 하는 시스템입니다. 서비스 패브릭 hello 클러스터 상태 toowork hello 문제를 다시 구성 되며 따라서 오류 분석 서비스 hello 전에 명시 된 hello 문제의 hello 현재 상태에서 여전히 오른쪽 수 toogive hello 설정 됩니다 보장 합니다.

### <a name="generating-required-events-and-scenarios"></a>필요한 이벤트 및 시나리오 생성
실제 오류를 일관 되 게 시뮬레이션 된 까다로운 toostart 상태인 동안 hello 기능 toogenerate 상관 관계가 지정 된 오류도 강입니다. 예를 들어 데이터 손실을 hello 다음 작업이 발생 하는 경우 상태 저장 지속된 서비스에서 상황이 발생 합니다.

1. 쓰기 쿼럼 hello 복제본의 복제에 검색 됩니다. Hello 보조 복제본을 모두 기본 hello 뒤에 지연 합니다.
2. hello 쓰기 쿼럼 tooa 코드 패키지 또는 중지 될 노드) (인해 다운 될 hello 복제본으로 인해 중지 되었습니다.
3. hello 쓰기 쿼럼 hello 복제본에 대 한 hello 데이터 toodisk 손상 또는 컴퓨터를 이미지로 다시 설치) (인해 손실 되므로를 다시 시작 수 없습니다.

이러한 상호 관련 된 오류는 hello 실제에서 시 키 지 않고 자주 개별 실패로 발생 않으므로 합니다. 프로덕션 환경에서 발생 하기 전에 이러한 시나리오에 대 한 hello 기능 tootest이 중요 합니다. 더욱 중요 중인 hello 기능 toosimulate 제어 된 환경에서 프로덕션 작업을 사용 하는 이러한 시나리오 (데크에 모든 엔지니어 hello 날의 hello 가운데). 오전 2 시에 프로덕션에서 처음으로 hello에 대 한 실행 것 보다 훨씬 더

### <a name="unified-experience-across-different-environments"></a>여러 환경에서 통합되지 않은 경험
일반적으로 hello 연습 toocreate 세 상이한 환경, hello 개발 환경에 대해 각각 하나씩, 테스트에 대 한 및 프로덕션에 대 한 되었습니다. hello 모델이 했습니다.

1. Hello 개발 환경에서 개별 메서드의 단위 테스트를 사용할 수 있는 상태 전환을 생성 합니다.
2. Hello 테스트 환경에서 다양 한 오류 시나리오를 실행 하는 오류 tooallow 종단 간 테스트를 생성 합니다.
3. 모든 비 자연 오류 및 휴먼 매우 빠른 응답 toofailure 임을 tooensure hello 프로덕션 환경에 대 한 기본적인 tooprevent를 유지 합니다.

서비스 패브릭에서 hello 오류 분석 서비스를 통해 우리는 제안 tooturn 주위이 하 고 사용 하 여 hello 동일 개발자 환경 tooproduction에서 방법론 합니다. 두 가지 방법으로 tooachieve이

1. tooinduce 제어 오류를 사용 하 여 hello 오류 분석 서비스 Api는 1-(1-box) 환경에서 모든 hello 방식으로 tooproduction 클러스터입니다.
2. toogive hello 클러스터 오류를 사용 하 여 hello 오류 분석 서비스 toogenerate 자동 유도 자동 오류를 발생 시키는 자세히 알아보려면입니다. 구성을 통해 오류의 hello 속도 제어 hello를 다양 한 환경에서 동일한 서비스 toobe 다르게 테스트 수 있습니다.

서비스 패브릭 오류의 hello 소수 자릿수는 hello 서로 다른 환경에서 다를 수 있지만 hello 실제 메커니즘은 같습니다. 따라서 서비스에 대 한는 훨씬 더 빠르게 코드 배포 파이프라인 및 hello 기능 tootest hello 실제 부하 상태에서 수 있습니다.

## <a name="using-hello-fault-analysis-service"></a>Hello 오류 분석 서비스를 사용 하 여
**C#**

오류 분석 서비스 기능은 hello Microsoft.ServiceFabric NuGet 패키지의에서 hello System.Fabric 네임 스페이스에 있습니다. toouse hello 오류 분석 서비스 기능을 프로젝트에 대 한 참조로 hello nuget 패키지를 포함 합니다.

**PowerShell**

PowerShell toouse hello 서비스 패브릭 SDK를 설치 해야 합니다. 후 hello SDK가 설치 되어 hello ServiceFabric PowerShell 모듈은 자동으로 toouse 하기 위해 로드 합니다.

## <a name="next-steps"></a>다음 단계
toocreate 진정한 클라우드 규모 서비스 이기 중요 tooensure 서비스가 실제 오류를 견딜 수 있는 배포 전후. Hello 서비스 현재 환경에서 신속 하 게 기능 tooinnovate hello 하 고 코드 tooproduction 신속 하 게 매우 중요 한 것을 이동 합니다. hello 오류 분석 서비스는 정확 하 게 서비스 개발자가 toodo 수 있습니다.

테스트 응용 프로그램 및 기본 제공 hello를 사용 하 여 서비스를 시작 [시나리오를 테스트할](service-fabric-testability-scenarios.md), hello를 사용 하 여 사용자 고유의 테스트 시나리오를 작성 하거나 [작업 오류](service-fabric-testability-actions.md) hello 오류 분석 서비스에서 제공 합니다.

<!--Image references-->
[0]: ./media/service-fabric-testability-overview/faultanalysisservice.png
