---
title: "Azure Service Fabric에 대 한 자세한 aaaLearn | Microsoft Docs"
description: "Hello 핵심 개념 및 Azure 서비스 패브릭의 주요 영역에 알아봅니다. 서비스 패브릭의 확장된 개요를 제공 하 고 어떻게 toocreate microservices 합니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/14/2017
ms.author: ryanwi
ms.openlocfilehash: 7fe8de777755be11635912613bb5b970e3fe3ea3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="so-you-want-toolearn-about-service-fabric"></a>따라서 서비스 패브릭에 대 한 toolearn 시겠습니까?
Azure 서비스 패브릭은 분산된 시스템 플랫폼으로 쉽게 toopackage를 사용 하면을 배포 하 고 확장성과 안정성이 뛰어난 microservices 관리 합니다.  그러나 서비스 패브릭은 대형 노출 영역을 고 있는 toolearn을 너무 많이 있습니다.  이 문서는 서비스 패브릭의 개요를 제공 하 고 hello 핵심 개념, 프로그래밍 모델을 테스트, 클러스터 및 상태 모니터링의 응용 프로그램 수명 주기를 설명 합니다. 읽기 hello [개요](service-fabric-overview.md) 및 [microservices 이란?](service-fabric-overview-microservices.md) 대 한 소개 및 서비스 패브릭 사용된 toocreate microservices을 수 있는 방법에 대 한 합니다. 이 문서에 콘텐츠 목록은 없지만 toooverview 및 서비스 패브릭의 모든 영역에 대 한 시작된 문서를 가져오는 연결 합니다. 

## <a name="core-concepts"></a>핵심 개념
[서비스 패브릭 용어](service-fabric-technical-overview.md), [응용 프로그램 모델](service-fabric-application-model.md), 및 [프로그래밍 모델을 지원](service-fabric-choose-framework.md) 자세한 개념 및 설명을 제공 하지만 hello 기본 사항 다음과 같습니다.

<table><tr><th>핵심 개념</th><th>설계 시간</th><th>실행 시간</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">
<img src="./media/service-fabric-content-roadmap/CoreConceptsVid.png" WIDTH="240" HEIGHT="162"></a></td>
<td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tlkI046yC_2906218965"><img src="./media/service-fabric-content-roadmap/RunTimeVid.png" WIDTH="240" HEIGHT="162"></a></td>
<td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=x7CVH56yC_1406218965">
<img src="./media/service-fabric-content-roadmap/RunTimeVid.png" WIDTH="240" HEIGHT="162"></a></td></tr>
</table>

### <a name="design-time-application-type-service-type-application-package-and-manifest-service-package-and-manifest"></a>디자인 타임: 응용 프로그램 형식, 서비스 형식, 응용 프로그램 패키지 및 매니페스트, 서비스 패키지 및 매니페스트
응용 프로그램 형식은 hello 이름/버전 tooa 서비스 형식 컬렉션을 할당 합니다. 응용 프로그램 패키지 디렉터리에 포함된 *ApplicationManifest.xml* 파일에서 정의됩니다. hello 응용 프로그램 패키지 한 다음 복사 toohello 서비스 패브릭 클러스터 이미지 저장소입니다. 그런 다음 다음 hello 클러스터 내에서 실행 되는이 응용 프로그램 종류에서 명명된 된 응용 프로그램을 만들 수 있습니다. 

서비스 형식은 hello 이름/버전 tooa 서비스의 코드 패키지, 데이터 패키지 및 패키지 구성에 할당 합니다. 서비스 패키지 디렉터리에 포함된 ServiceManifest.xml 파일에서 정의됩니다. hello 서비스 패키지 디렉터리는 다음으로 참조 응용 프로그램 패키지 *ApplicationManifest.xml* 파일입니다. Hello 클러스터 내에서 명명된 된 응용 프로그램을 만든 후 만들 수 있습니다는 명명된 서비스 hello 중 하나에서 응용 프로그램 종류의 서비스 유형. 서비스 형식은 *ServiceManifest.xml* 파일로 설명되며, 런타임 시 로드 되는 실행 코드 서비스 구성 설정 및 hello 서비스에서 사용 되는 정적 데이터의 hello 서비스 유형으로 구성 됩니다.

![서비스 패브릭 응용 프로그램 유형 및 서비스 유형][cluster-imagestore-apptypes]

hello 응용 프로그램 패키지는 hello 응용 프로그램 종류를 포함 하는 디스크 디렉터리 *ApplicationManifest.xml* hello 응용 프로그램 종류를 구성 하는 각 서비스 유형에 대 한 hello 서비스 패키지를 참조 하는 파일입니다. 예를 들어 전자 메일 응용 프로그램 종류에 대 한 응용 프로그램 패키지 참조가 tooa 큐 서비스 패키지, 프런트 엔드 서비스 패키지 및 데이터베이스 서비스 패키지를 포함할 수 있습니다. hello 응용 프로그램 패키지 디렉터리의 hello 파일은 복사 toohello 서비스 패브릭 클러스터 이미지 저장소입니다. 

서비스 패키지는 hello 서비스 형식이 포함 된 디스크 디렉터리 *ServiceManifest.xml* hello 코드, 정적 데이터 및 hello 서비스 유형에 대 한 구성 패키지를 참조 하는 파일입니다. hello 응용 프로그램 종류에서 참조 하는 hello 서비스 패키지 디렉터리에 파일 hello *ApplicationManifest.xml* 파일입니다. 예를 들어 서비스 패키지 toohello 코드, 정적 데이터 및 데이터베이스 서비스를 구성 하는 구성 패키지를 참조할 수 있습니다.

### <a name="run-time-clusters-and-nodes-named-applications-named-services-partitions-and-replicas"></a>런타임: 클러스터 및 노드, 명명된 응용 프로그램, 명명된 서비스, 파티션 및 복제본
[Service Fabric 클러스터](service-fabric-deploy-anywhere.md): 마이크로 서비스가 배포되고 관리되는 네트워크로 연결된 가상 또는 실제 컴퓨터 집합입니다. 클러스터의 컴퓨터 toothousands를 확장할 수 있습니다.

클러스터의 일부인 컴퓨터나 VM을 노드라고 합니다. 각 노드는 노드 이름(문자열)에 할당됩니다. 노드는 배치 속성과 같은 특징이 있습니다. 각 컴퓨터 또는 VM이 Windows 서비스인 `FabricHost.exe`를 자동으로 시작하여 부팅을 실행하기 시작한 다음 `Fabric.exe` 및 `FabricGateway.exe`이라는 두 개의 실행 파일을 시작합니다. 이러한 두 개의 실행 개체는 hello 노드를 확인합니다. 개발 또는 테스트 시나리오에서는 `Fabric.exe` 및 `FabricGateway.exe`와 같은 여러 인스턴스를 실행하여 단일 컴퓨터 또는 VM에 여러 노드를 호스트할 수 있습니다.

명명된 응용 프로그램은 하나 이상의 특정 기능을 수행하는 명명된 서비스 컬렉션입니다. 서비스는 완전한 독립 실행형 기능을 수행하며(서비스는 다른 서비스와 독립적으로 시작 및 실행 가능) 코드, 구성 및 데이터로 이루어집니다. 응용 프로그램 패키지를 복사한 toohello 이미지 저장소 후에 hello 응용 프로그램 패키지의 응용 프로그램 종류 (이름/버전 사용)를 지정 하 여 hello 클러스터 내에서 hello 응용 프로그램의 인스턴스를 만듭니다. 각 응용 프로그램 형식 인스턴스는 *fabric:/MyNamedApp*과 같은 URI 이름이 할당됩니다. 클러스터 내에서 단일 응용 프로그램 형식에서 여러 명명된 응용 프로그램을 만들 수 있습니다. 또한 다른 형식의 응용 프로그램에서 명명된 응용 프로그램을 만들 수 있습니다. 명명된 응용 프로그램은 각각 독립적으로 관리되고 버전이 지정됩니다.

명명된 된 응용 프로그램을 만든 후 hello 서비스 유형 (이름/버전 사용)를 지정 하 여 hello 클러스터 내에서 해당 서비스 형식의 (명명 된 서비스)의 인스턴스를 만들 수 있습니다. 각 서비스 형식 인스턴스는 명명된 응용 프로그램의 URI로 범위가 지정된 URI 이름이 할당됩니다. 예를 들어 "MyDatabase" 라는 이름은 응용 프로그램 "MyNamedApp" 내 서비스를 만들면 hello URI 같습니다: *패브릭: / MyNamedApp/MyDatabase*합니다. 명명된 응용 프로그램 내에서 하나 이상의 명명된 서비스를 만들 수 있습니다. 명명된 각 서비스는 고유한 파티션 구성표 및 복제본/인스턴스 수를 가질 수 있습니다. 

여기에는 상태 비저장과 상태 저장 등의 두 가지 서비스 형식이 있습니다. 상태 비저장 서비스는 Azure Storage, Azure SQL Database 또는 Azure Cosmos DB와 같은 외부 저장소 서비스에 영구 상태를 저장할 수 있습니다. 에 영구 저장소가 없는 전혀 hello 서비스 하는 경우에 상태 비저장 서비스를 사용 합니다. 상태 저장 서비스의 신뢰할 수 있는 컬렉션 또는 Reliable Actors 프로그래밍 모델을 통해 서비스의 상태 서비스 패브릭 toomanage를 사용 합니다. 

명명된 서비스를 만들 때 파티션 구성표를 지정합니다. 많은 양의 상태를 사용 하 여 서비스 파티션 간에 hello 데이터를 분할 합니다. 각 파티션에 일부 hello hello 클러스터 노드 전체에 분산 되어 있는 hello 서비스의 전체 상태를 담당 합니다. 상태 저장 서비스에 복제본이 있는 반면 파티션 내에서 명명된 상태 비저장 서비스에는 인스턴스가 있습니다. 일반적으로 명명된 상태 비저장 서비스는 내부 상태가 없기 때문에 하나의 파티션만을 가질 수 있습니다. 명명된 상태 저장 서비스는 복제본 내에서 해당 상태를 유지하고 각 파티션에는 고유한 복제본 세트가 있습니다. 하나의 복제본 (주 hello 라고 함)에서 읽기 및 쓰기 작업이 수행 됩니다. 쓰기 작업은 변경 내용을 toostate toomultiple (활성 보조 데이터베이스 라고 함) 다른 복제본을 복제 합니다. 

hello 다음 다이어그램에서는 응용 프로그램 및 서비스 인스턴스, 파티션 및 복제본 간의 hello 관계

![서비스 내의 파티션 및 복제본][cluster-application-instances]

### <a name="partitioning-scaling-and-availability"></a>분할, 크기 조정 및 가용성
[분할](service-fabric-concepts-partitioning.md) 고유 tooService 패브릭 않습니다. 분할의 잘 알려진 양식은 데이터 분할 또는 분할이라고도 합니다. 많은 양의 상태를 사용 하 여 상태 저장 서비스 파티션 간에 hello 데이터를 분할 합니다. 각 파티션에 일부 hello hello 서비스의 전체 상태를 담당 합니다. 

각 파티션의 hello 복제본 hello 클러스터의 노드에 분산를 허용 하는 명명 된 서비스의 상태 너무[배율](service-fabric-concepts-scalability.md)합니다. Hello 데이터 요구 사항이 증가, 파티션을 증가 하 고 서비스 패브릭 노드 toomake 효율적으로 사용할 하드웨어 리소스 간에 파티션을 변경 합니다. 새 노드 toohello 클러스터를 추가 하면 서비스 패브릭은 균형을 다시 조정 hello 파티션 복제본 노드 수가 증가 하는 hello에서 합니다. 전체 응용 프로그램의 성능을 개선 하 고 액세스 toomemory에 대 한 경합이 감소 합니다. Hello 클러스터의 노드 hello 효율적으로 사용 되지 않는, hello hello 클러스터의 노드 수를 줄일 수 있습니다. 서비스 패브릭 감소 hello 수의 노드 toomake 효과적으로 사용할 각 노드에 하드웨어 hello hello 파티션 복제본을 다시 변경 합니다.

상태 저장 서비스에 복제본이 있는 반면 파티션 내에서 명명된 상태 비저장 서비스에는 인스턴스가 있습니다. 일반적으로 명명된 상태 비저장 서비스는 내부 상태가 없기 때문에 하나의 파티션만을 가질 수 있습니다. 에 대 한 hello 파티션 인스턴스가 제공 [가용성](service-fabric-availability-services.md)합니다. 하나의 인스턴스가 실패 하면 다른 인스턴스와 toooperate를 정상적으로 계속 하 한 다음 서비스 패브릭 새 인스턴스를 만듭니다. 명명된 상태 저장 서비스는 복제본 내에서 해당 상태를 유지하고 각 파티션에는 고유한 복제본 세트가 있습니다. 하나의 복제본 (주 hello 라고 함)에서 읽기 및 쓰기 작업이 수행 됩니다. 쓰기 작업은 변경 내용을 toostate toomultiple (활성 보조 데이터베이스 라고 함) 다른 복제본을 복제 합니다. 서비스 패브릭 복제 실패로 처리할지, hello 기존 복제본에서 새 복제 데이터베이스를 작성 합니다.

## <a name="stateless-and-stateful-microservices-for-service-fabric"></a>Service Fabric용 상태 비저장 및 상태 저장 마이크로 서비스
서비스 패브릭 microservices 또는 컨테이너의 구성 된 toobuild 응용 프로그램을 사용 합니다. (예: 프로토콜 게이트웨이 및 웹 프록시) 상태 비저장 microservices 요청과 해당 응답 hello 서비스에서 외부 변경 가능 상태를 유지 하지 않습니다. Azure 클라우드 서비스 작업자 역할이 상태 비저장 서비스의 예입니다. (예: 사용자 계정, 데이터베이스, 장치, 쇼핑 카트 및 큐) 상태 저장 microservices hello 요청 및 응답 이외의 변경할 수 있는 신뢰할 수 있는 상태로 유지합니다. 오늘날 인터넷 범위의 서비스는 상태 비저장 및 상태 저장 마이크로 서비스의 조합으로 구성됩니다. 

서비스 패브릭 키 differentation는 hello를 사용 하 여 상태 저장 서비스를 만드는 강력한 강화 [프로그래밍 모델에 기본 제공 ](service-fabric-choose-framework.md) 하거나 컨테이너 화 된 상태 저장 서비스를 사용 합니다. hello [응용 프로그램 시나리오](service-fabric-application-scenarios.md) hello 시나리오 상태 저장 서비스를 사용 하는 위치에 대해 설명 합니다.

상태 비저장 것과 함께 상태 저장 microservices 있는 이유는? hello 두 가지 주요 원인은 다음과 같습니다.

* 높은 처리량, 낮은 대기 시간, 내결함성 온라인 트랜잭션 처리 (OLTP) 코드를 유지 하 여 서비스를 제공 하며 데이터에 닫기 hello 동일한 시스템을 빌드할 수 있습니다. 대화형 인터넷 상점, 검색, IoT(사물 인터넷) 시스템, 거래 시스템, 신용 카드 처리 및 사기 감지 시스템,개인 레코드 관리를 몇 가지 예로 들 수 있습니다.
* 응용 프로그램 디자인을 간소화할 수 있습니다. 상태 저장 microservices 추가 큐에 대 한 hello 필요성을 제거 하 고, 일반적으로 캐시는 순수 하 게 상태 비저장 응용 프로그램의 tooaddress hello 가용성 및 대기 시간 요구 사항이 필요한 키를 누릅니다. 상태 저장 서비스는 자연스럽 게 고가용성 및 낮은 대기 시간을 전체적으로 응용 프로그램에서 움직이는 부품 toomanage hello 수가 감소 합니다.

## <a name="supported-programming-models"></a>지원되는 프로그래밍 모델
서비스 패브릭 여러 방법으로 toowrite 소개 하며 서비스를 관리 합니다. 서비스는 hello 서비스 패브릭 Api tootake 활용 hello 플랫폼의 기능 및 응용 프로그램 프레임 워크를 사용할 수 있습니다. 서비스는 모든 언어로 작성되고 Service Fabric 클러스터에서 호스트되는 컴파일된 실행 프로그램일 수도 있습니다. 자세한 내용은 [지원되는 프로그래밍 모델](service-fabric-choose-framework.md)을 참조하세요.

### <a name="containers"></a>컨테이너
기본적으로 Service Fabric은 이러한 서비스를 프로세스로 배포하고 활성화합니다. Service Fabric도 [컨테이너](service-fabric-containers-overview.md)에 서비스를 배포할 수 있습니다. 프로세스의 서비스 및 서비스 컨테이너에서 hello 혼합할 수 중요 한 점은 같은 응용 프로그램입니다. Service Fabric은 Windows Server 2016에서 Linux 컨테이너 및 Windows 컨테이너의 배포를 지원합니다. 컨테이너에서 기존 응용 프로그램, 상태 비저장 서비스 또는 상태 저장 서비스를 배포할 수 있습니다. 

### <a name="reliable-services"></a>Reliable Services
[신뢰할 수 있는 서비스](service-fabric-reliable-services-introduction.md) 는 hello 서비스 패브릭 플랫폼과 통합 하 고 플랫폼 기능 중 일부만 hello에서에서 활용 하는 서비스를 작성 하기 위한 경량 프레임 워크입니다. 신뢰할 수 있는 서비스는 상태 비저장 (유사한 toomost 서비스와 같은 플랫폼 웹 서버 또는 Azure 클라우드 서비스에서 작업자 역할), 수 Azure DB 나 Azure 테이블 저장소와 같은 외부 솔루션에서는 상태가 지속 되는 위치입니다. 신뢰할 수 있는 서비스 일 수도 있습니다 상태 저장, 신뢰할 수 있는 컬렉션을 사용 하 여 자체 hello 서비스에서 직접 상태가 지속 되는 위치. 상태는 복제를 통해 [고가용성](service-fabric-availability-services.md)이 유지되고 [분할](service-fabric-concepts-partitioning.md)을 통해 배포되며, 모두 Service Fabric에서 자동으로 관리합니다.

### <a name="reliable-actors"></a>Reliable Actors
신뢰할 수 있는 서비스에서 구현 hello [Reliable Actor](service-fabric-reliable-actors-introduction.md) 프레임 워크는 hello 행위자 디자인 패턴에 따라 hello Virtual Actor 패턴을 구현 하는 응용 프로그램 프레임 워크입니다. hello Reliable Actor 프레임 워크 행위자 호출 하는 단일 스레드 실행을 독립적인 단위 계산 및 상태를 사용 합니다. 프레임 워크를 제공 하는 Reliable Actor hello 행위자 및 미리 설정된 된 상태 지 속성 및 확장 구성에 대 한 통신에 빌드됩니다.

### <a name="aspnet-core"></a>ASP.NET Core
Service Fabric은 웹 및 API 응용 프로그램 빌드를 위한 첫 번째 클래스 프로그래밍 모델로 [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md)와 통합됩니다.

### <a name="guest-executables"></a>게스트 실행 파일
[게스트 실행 파일](service-fabric-deploy-existing-app.md)은 Service Fabric 클러스터에서 다른 서비스와 함께 호스트된 임의의 기존 실행 파일입니다. 게스트 실행 파일은 Service Fabric API와 직접 통합되지 않습니다. 그러나 여전히 이점을 얻는 기능에서 사용자 지정 상태와 같은 플랫폼 제공 hello 및 보고을 로드 REST Api를 호출 하 여 검색 기능을 서비스. 또한 전체 응용 프로그램 수명 주기 지원도 포함합니다. 

## <a name="application-lifecycle"></a>응용 프로그램 수명 주기
다른 플랫폼과 응용 프로그램 서비스 패브릭에서 일반적으로 면 hello 다음 단계를 통해: 디자인, 개발, 테스트, 배포, 업그레이드, 유지 관리 및 제거 합니다. 서비스 패브릭 hello 전체 응용 프로그램 수명 주기에서 개발, 배포, 일상적인 관리 및 유지 관리 tooeventual 서비스 해제를 통해 클라우드 응용 프로그램의 기본 지원을 제공합니다. hello 서비스 모델에는 여러 가지 다양 한 역할 tooparticipate를 hello 응용 프로그램 수명 주기에서 독립적으로 수 있습니다. [서비스 패브릭 응용 프로그램 수명 주기](service-fabric-application-lifecycle.md) hello 단계의 hello 서비스 패브릭 응용 프로그램 수명 주기 전체에서 hello 다른 역할에서 어떻게 사용 되는지 및 hello Api의 개요를 제공 합니다. 

사용 하 여 hello 전체 응용 프로그램 수명 주기를 관리할 수 있습니다 [PowerShell cmdlet](/powershell/module/ServiceFabric/), [C# Api](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient), [Java Api](/java/api/system.fabric._application_management_client), 및 [REST Api](/rest/api/servicefabric/)합니다. [Visual Studio Team Services](service-fabric-set-up-continuous-integration.md) 또는 [Jenkins](service-fabric-cicd-your-linux-java-application-with-jenkins.md)와 같은 도구를 사용하여 지속적인 통합/지속적인 배포 파이프라인을 설정할 수도 있습니다.

hello 다음 Microsoft Virtual Academy 비디오 설명 방법을 toomanage 응용 프로그램 수명:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=My3Ka56yC_6106218965">
<img src="./media/service-fabric-content-roadmap/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="test-applications-and-services"></a>응용 프로그램 및 서비스 테스트
toocreate 진정한 클라우드 규모 서비스 것이 중요 한 tooverify 응용 프로그램 및 서비스 실제 오류 견딜 수 있습니다. hello 오류 분석 서비스는 서비스 패브릭 서비스를 기반으로 하는 테스트를 위해 설계 되었습니다. Hello로 [오류 분석 서비스](service-fabric-testability-overview.md), 의미 있는 오류를 유도 하 고 응용 프로그램에 대 한 전체 테스트 시나리오를 실행할 수 있습니다. 이러한 오류와 시나리오를 실행 하 고 유효성을 검사 hello 다양 한 상태 및 전환 하는 서비스는 제어 된, 안전 및 일관 된 방식으로 모두에 해당 수명 주기 동안 발생 합니다.

[작업](service-fabric-testability-actions.md)은 개별 오류를 사용하여 테스트할 서비스를 대상으로 합니다. 서비스 개발자는이 방법으로 문서 블록 toowrite 복잡 한 시나리오를 사용할 수 있습니다. 시뮬레이트된 오류의 예는 다음과 같습니다.

* 컴퓨터 또는 VM 다시 부팅 되는 경우 개수에 관계 없이 노드 toosimulate를 다시 시작 합니다.
* 상태 저장 서비스 toosimulate 부하 분산, 장애 조치 또는 응용 프로그램 업그레이드의 복제본을 이동 합니다.
* 상태 저장 서비스 toocreate 충분 한 "백업" 또는 "secondary" 복제본 tooaccept 새 데이터가 없기 때문 쓰기 작업을 계속할 수 없습니다 없는 상황에서 쿼럼이 손실 된를 호출 합니다.
* 상태 저장 서비스 toocreate 아웃 완전히 초기화 하는 모든 메모리 내 상태에 있는 상황에서 데이터 손실이 호출 합니다.

[시나리오](service-fabric-testability-scenarios.md)는 하나 이상의 작업으로 구성되는 복잡한 작업입니다. hello 오류 분석 서비스에서는 두 개의 기본 제공 완전 한 시나리오를 제공합니다.

* [Chaos 시나리오](service-fabric-controlled-chaos.md)-확장 된 긴 시간 동안 hello 클러스터 전체에서 인터리빙, 연속 오류 (정상 및 비정상)을 시뮬레이션 합니다.
* [장애 조치 시나리오](service-fabric-testability-scenarios.md#failover-test)-특정 서비스 파티션 다른 서비스를 영향을 받지 않고 그대로 유지 하면서 대상으로 하는 hello chaos 테스트 시나리오의 버전입니다.

## <a name="clusters"></a>클러스터
[Service Fabric 클러스터](service-fabric-deploy-anywhere.md): 마이크로 서비스가 배포되고 관리되는 네트워크로 연결된 가상 또는 실제 컴퓨터 집합입니다. 클러스터의 컴퓨터 toothousands를 확장할 수 있습니다. 클러스터의 일부인 컴퓨터나 VM을 클러스터 노드라고 합니다. 각 노드는 노드 이름(문자열)에 할당됩니다. 노드는 배치 속성과 같은 특징이 있습니다. 각 컴퓨터 또는 VM에는 자동 시작 서비스인 `FabricHost.exe`가 있습니다. 이 서비스는 부팅 시 실행된 다음 Fabric.exe, FabricGateway.exe 등의 두 실행 파일을 시작합니다. 이러한 두 개의 실행 개체는 hello 노드를 확인합니다. 테스트 시나리오에서는 `Fabric.exe` 및 `FabricGateway.exe`와 같은 여러 인스턴스를 실행하여 단일 컴퓨터 또는 VM에 여러 노드를 호스트할 수 있습니다.

Windows Server 또는 Linux를 실행하는 가상 또는 물리적 컴퓨터에 Service Fabric 클러스터를 만들 수 있습니다. Toodeploy 수 있고 상호 연결 되는 Windows Server 또는 Linux 컴퓨터 집합에 있는 모든 환경에서 서비스 패브릭 응용 프로그램을 실행: 온-프레미스, 모든 클라우드 공급자 또는 Microsoft Azure에서.

hello 다음 Microsoft Virtual Academy 비디오 설명 서비스 패브릭 클러스터:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">
<img src="./media/service-fabric-content-roadmap/ClusterOverview.png" WIDTH="360" HEIGHT="244">
</a></center>

### <a name="clusters-on-azure"></a>Azure의 클러스터
Azure에서 실행 중인 서비스 패브릭 클러스터 쉽고 안정적 작업 및 hello 클러스터의 관리는 다른 Azure 기능 및 서비스와의 통합을 제공 합니다. 클러스터는 Azure Resource Manager 리소스이므로 Azure에서 다른 리소스처럼 클러스터를 모델링할 수 있습니다. 리소스 관리자는 또한 하나의 단위로 hello 클러스터에서 사용 하는 모든 리소스의 간편한 관리를 제공 합니다. Azure에서 클러스터는 Azure 진단 및 Log Analytics와 통합됩니다. 클러스터 노드 형식은 [가상 컴퓨터 확장 집합](/azure/virtual-machine-scale-sets/index)이므로 자동 크기 조정 기능을 기본 제공합니다.

Hello를 통해 Azure에서 클러스터를 만들 수 있습니다 [Azure 포털](service-fabric-cluster-creation-via-portal.md)를에서 한 [템플릿](service-fabric-cluster-creation-via-arm.md), 또는 [Visual Studio](service-fabric-cluster-creation-via-visual-studio.md)합니다.

Linux에서 서비스 패브릭의 hello 미리 보기를 사용 하면 toobuild, 배포 및 Windows에서와 마찬가지로 Linux에서 고가용성, 확장성이 높은 응용 프로그램을 관리 합니다. hello 서비스 패브릭 프레임 워크 (신뢰할 수 있는 서비스 및 Reliable Actors)는 또한 tooC # (.NET Core)에서 Java linux에서 사용할 수 있습니다. 어떤 언어 또는 프레임워크에서도 [게스트 실행 서비스](service-fabric-deploy-existing-app.md) 를 빌드할 수 있습니다. 또한 hello 미리 보기는 오케스트레이션 Docker 컨테이너도 지원합니다. Docker 컨테이너 게스트 실행 파일 또는 hello 서비스 패브릭 프레임 워크를 사용 하는 기본 서비스 패브릭 서비스를 실행할 수 있습니다. 자세한 내용은 [Linux의 Service Fabric](service-fabric-linux-overview.md)을 참조하세요.

Linux의 Service Fabric이 미리 보기 상태이므로 Linux가 아닌 Windows에서만 지원되는 몇 가지 기능도 있습니다. toolearn 더 읽기 [서비스 패브릭 linux와 Windows 차이점](service-fabric-linux-windows-differences.md)합니다.

### <a name="standalone-clusters"></a>독립 실행형 클러스터
서비스 패브릭 있습니다 toocreate 독립 실행형 서비스 패브릭 클러스터에 온-프레미스 또는 모든 클라우드 공급자의 설치 패키지를 제공합니다. 독립 실행형 클러스터 원하는 위치에 자유롭게 toohost 클러스터 hello에 게 제공 합니다. 주체 toocompliance 또는 규정 제약 조건, 데이터를 tookeep 로컬 데이터를 원하는 경우 사용자 고유의 클러스터 및 응용 프로그램을 호스트할 수 있습니다. 서비스 패브릭 응용 프로그램 응용 프로그램을 구축에 대 한 정보를 통해 한 호스팅 환경 tooanother에서 수행 되므로 여러 호스팅 환경을 변경 하지 않고 실행할 수 있습니다. 

[첫 번째 Service Fabric 독립 실행형 클러스터 만들기](service-fabric-get-started-standalone-cluster.md)

Linux 독립 실행형 클러스터는 아직 지원되지 않습니다.

### <a name="cluster-security"></a>클러스터 보안
클러스터에서 실행 되는 프로덕션 작업 되었을 경우, 특히 tooyour 클러스터를 연결 하지 못하도록 보안된 tooprevent 권한이 없는 사용자가 있어야 합니다. 관리 끝점은 하는 경우 익명 사용자에 게 tooconnect tooit toohello 노출 가능한 toocreate 보안 되지 않은 클러스터는 아니지만 이렇게 하면 공용 인터넷 합니다. 보안 되지 않은 클러스터에서 security를 사용 가능한 toolater 아닙니다: 클러스터를 만들 때 클러스터 보안을 사용 합니다.

hello 클러스터 보안 시나리오입니다.
* 노드 간 보안
* 클라이언트-노드 보안
* RBAC(역할 기반 액세스 제어)

자세한 내용은 [클러스터에 보안 적용](service-fabric-cluster-security.md)을 참조하세요.

### <a name="scaling"></a>확장
새 노드 toohello 클러스터를 추가 하면 서비스 패브릭 hello 파티션 복제 되는 인스턴스와 노드 수가 증가 하는 hello 간에 변경 합니다. 전체 응용 프로그램의 성능을 개선 하 고 액세스 toomemory에 대 한 경합이 감소 합니다. Hello 클러스터의 노드 hello 효율적으로 사용 되지 않는, hello hello 클러스터의 노드 수를 줄일 수 있습니다. 서비스 패브릭 hello 파티션 복제를 다시 변경 하 고 노드 toomake 수가 감소 하는 hello에서 인스턴스 좋은 hello 하드웨어 각 노드에서 사용 하 여 키를 누릅니다. Azure에서 [수동으로](service-fabric-cluster-scale-up-down.md) 또는 [프로그래밍 방식으로](service-fabric-cluster-programmatic-scaling.md) 클러스터의 크기를 조정할 수 있습니다. 독립 실행형 클러스터는 [수동으로](service-fabric-cluster-windows-server-add-remove-nodes.md) 크기를 조정할 수 있습니다.

### <a name="cluster-upgrades"></a>클러스터 업그레이드
정기적으로 새 버전의 hello 서비스 패브릭 런타임이 릴리스됩니다. 항상 [지원되는 버전](service-fabric-support.md)을 실행하도록 클러스터의 런타임, 패브릭 또는 업그레이드를 수행합니다. 또한 toofabric 업그레이드, 인증서 또는 응용 프로그램 포트 같은 클러스터 구성을 업데이트할 수도 있습니다.

Service Fabric 클러스터는 개인이 소유하지만 Microsoft에서 부분적으로 관리하는 리소스입니다. Microsoft는 패치 hello 기본 OS 및 클러스터에 fabric 업그레이드를 수행 합니다. Microsoft에서 새 버전을 릴리스 하는 경우 클러스터 tooreceive 자동 패브릭 업그레이드 되 면를 설정 하거나 tooselect 원하는 패브릭 지원 되는 버전을 선택할 수 있습니다. 패브릭 및 구성 업그레이드 hello Azure 포털을 통해 또는 리소스 관리자를 통해 설정할 수 있습니다. 자세한 내용은 [Service Fabric 클러스터 업그레이드](service-fabric-cluster-upgrade.md)를 참조하세요. 

독립 실행형 클러스터는 사용자가 전적으로 소유하는 리소스입니다. 기본 OS 및 fabric 업그레이드를 시작 하는 패치 hello에 책임이 있습니다. 클러스터 너무 연결할 수 있는 경우[https://www.microsoft.com/download](https://www.microsoft.com/download), 클러스터 tooautomatically 다운로드를 설정할 수 있습니다 및 프로 비전 hello 새 서비스 패브릭 런타임 패키지 합니다. 그런 다음 hello 업그레이드를 시작 합니다. 클러스터에 액세스할 수 없는 경우 [https://www.microsoft.com/download](https://www.microsoft.com/download), 인터넷 연결 된 컴퓨터에서 수동으로 hello 새 런타임 패키지를 다운로드 하 고 hello 업그레이드를 시작 합니다. 자세한 내용은 [독립 실행형 Service Fabric 클러스터 업그레이드](service-fabric-cluster-upgrade-windows-server.md)를 참조하세요.

## <a name="health-monitoring"></a>상태 모니터링
서비스 패브릭 소개는 [상태 모델](service-fabric-health-introduction.md) tooflag 비정상 클러스터 및 응용 프로그램 (예: 클러스터 노드 및 서비스 복제본)는 특정 엔터티를 디자인 합니다. hello 상태 모델 상태 reporters (시스템 구성 요소 및 watchdogs)를 사용합니다. hello ´ ֲ 쉽고 빠르게 진단 및 복구 합니다. 서비스 작성자 필요 상태에 대 한 현상을 toothink 및 어떻게 너무[상태 보고 디자인](service-fabric-report-health.md#design-health-reporting)합니다. 특히 toohello 루트 닫기 플래그 문제를 손쉽게 경우 상태에 영향을 줄 수 있는 모든 조건, 보고 됩니다. hello 상태 정보는 디버깅 및 hello 서비스가 실행 중인지 후 조사 및 프로덕션 환경에서 눈금에서의 실행에 시간과 노력 저장할 수 있습니다.

hello 서비스 패브릭 reporters 모니터의 관심 조건에서 식별 합니다. 보고자는 각자 로컬 보기를 기반으로 이러한 조건에 대한 정보를 보고합니다. hello [상태 저장소](service-fabric-health-introduction.md#health-store) 엔터티는 전역적으로 정상 여부 모든 reporters toodetermine에서 보낸 상태 데이터를 집계 합니다. hello 모델은 의도 한 toobe 풍부한 유연 하며 쉽게 toouse입니다. hello 상태 보고서의 hello 품질 hello 클러스터의 hello 상태 보기의 hello 정확도 결정합니다. 비정상 이슈를 잘못 표시하는 거짓 긍정은 상태 데이터를 사용하는 업그레이드 또는 기타 서비스에 부정적인 영향을 미칠 수 있습니다. 이러한 서비스의 예로는 복구 서비스 및 경고 메커니즘이 있습니다. 따라서 일부 생각은 필요한 tooprovide 보고서 hello에 대 한 관심의 조건에는 최상의 가능한 방법을 합니다.

다음 위치에서 보고를 수행할 수 있습니다.
* hello는 서비스 패브릭 서비스 복제본 또는 인스턴스를 모니터링합니다.
* Service Fabric 서비스로 배포되는 내부 Watchdog(예: 조건 및 문제 보고서를 모니터링하는 Service Fabric 상태 비저장 서비스). hello watchdogs 모든 노드에서 배포 하거나 모니터링 하는 선호도 지정 된 toohello 서비스 일 수 있습니다.
* 내부 watchdogs hello 서비스 패브릭에서를 실행 하지만 서비스 패브릭 서비스도 구현 되지 않습니다.
* 외부 watchdogs 외부 hello 서비스 패브릭 클러스터 (예를 들어 Gomez 같은 모니터링 서비스)에서 해당 프로브 hello 리소스입니다.

Hello 초기 서비스 패브릭 구성 요소는 hello 클러스터의 모든 엔터티에 대 상태를 보고합니다. [시스템 상태 보고서](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)는 상태를 통해 클러스터 및 응용 프로그램의 기능 및 플래그 문제에 대한 가시성을 제공합니다. 응용 프로그램 및 서비스에 대 한 시스템 상태 보고서 엔터티 구현 되 고 hello 서비스 패브릭 런타임 hello 관점에서 제대로 동작을 확인 합니다. hello 보고서 hello 서비스의 hello 비즈니스 논리의 상태 모니터링을 제공 하지 않거나 응답 하지 않는 프로세스를 검색 합니다. tooadd 상태 정보 특정 tooyour 서비스 논리 [사용자 지정 상태 보고 구현](service-fabric-report-health.md) 서비스에서 합니다.

서비스 패브릭에서는 여러 가지 방법으로 너무[상태 보고서를 볼](service-fabric-view-entities-aggregated-health.md) hello health store에서 집계:
* [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) 또는 기타 시각화 도구
* 상태 쿼리 수 (통해 [PowerShell](/powershell/module/ServiceFabric/), hello [C# Api FabricClient](/api/system.fabric.fabricclient.healthclient) 및 [Java FabricClient Api](/java/api/system.fabric._health_client), 또는 [REST Api](/rest/api/servicefabric)).
* 일반 쿼리 하는 엔터티 목록을 반환 하는 PowerShell, hello API 또는 REST) (통해 hello 속성 중 하나로 상태는 포함 합니다.

hello 다음 Microsoft Virtual Academy 비디오 hello 서비스 패브릭 상태 모델 및 사용 방법에 대해 설명 합니다.<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tevZw56yC_1906218965">
<img src="./media/service-fabric-content-roadmap/HealthIntroVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="next-steps"></a>다음 단계
* 자세한 내용은 방법 toocreate는 [Azure의 클러스터](service-fabric-cluster-creation-via-portal.md) 또는 [Windows에서 독립 실행형 클러스터](service-fabric-cluster-creation-for-windows-server.md)합니다.
* Hello를 사용 하는 서비스를 만들어 보십시오 [신뢰할 수 있는 서비스](service-fabric-reliable-services-quick-start.md) 또는 [Reliable Actors](service-fabric-reliable-actors-get-started.md) 프로그래밍 모델입니다.
* 너무 방법에 대해 알아봅니다[클라우드 서비스에서 마이그레이션할](service-fabric-cloud-services-migration-differences.md)합니다.
* 너무 자세한[모니터링 및 진단 서비스](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)합니다. 
* 너무 자세한[앱 및 서비스를 테스트](service-fabric-testability-overview.md)합니다.
* 너무 자세한[관리 하 고 클러스터 리소스를 조정](service-fabric-cluster-resource-manager-introduction.md)합니다.
* Hello를 살펴보고 [서비스 패브릭 샘플](http://aka.ms/servicefabricsamples)합니다.
* [Service Fabric 지원 옵션](service-fabric-support.md)에 대해 알아봅니다.
* 읽기 hello [팀 블로그](https://blogs.msdn.microsoft.com/azureservicefabric/) 아티클과 공지에 대 한 합니다.


[cluster-application-instances]: media/service-fabric-content-roadmap/cluster-application-instances.png
[cluster-imagestore-apptypes]: ./media/service-fabric-content-roadmap/cluster-imagestore-apptypes.png
