---
title: "Azure에서 서비스 패브릭의 aaaOverview | Microsoft Docs"
description: "서비스 패브릭에서 응용 프로그램을 구성 하는 많은 microservices tooprovide 크기 조정 및 복원 력을의 개요. 서비스 패브릭은 분산된 시스템 플랫폼 toobuild 확장 가능 하 고 신뢰할 수 있는, 사용 및 hello 클라우드 용 응용 프로그램을 쉽게 관리할입니다."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: masnider
ms.assetid: bbcc652a-a790-4bc4-926b-e8cd966587c0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: mfussell
ms.openlocfilehash: 427fcedf97e6b2aae42d240c63e9f85daed8d962
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-service-fabric"></a>Azure Service Fabric의 개요
Azure 서비스 패브릭은 쉽게 toopackage 수행 하는 분산된 시스템 플랫폼, 배포 및 확장 가능 하 고 신뢰할 수 있는 microservices 및 컨테이너를 관리 합니다. 또한 서비스 패브릭 hello 개발 하 고 클라우드 네이티브 응용 프로그램 관리에서 중요 한 문제를 해결 합니다. 개발자와 관리자가 복잡한 인프라 문제를 피하고 업무 수행에 필수적인 까다로운 워크로드를 확장 가능하고 신뢰할 수 있으며 관리가 가능하도록 구현하는 데 집중할 수 있습니다. 서비스 패브릭 빌드하고 이러한 엔터프라이즈 수준의 계층 1, 컨테이너에서 실행 되는 클라우드 규모 응용 프로그램을 관리 하기 위한 차세대 플랫폼을 hello를 나타냅니다.

이 짧은 비디오에서는 Service Fabric 및 마이크로 서비스를 소개합니다.<center><a target="_blank" href="https://aka.ms/servicefabricvideo">  
<img src="./media/service-fabric-overview/OverviewVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="applications-composed-of-microservices"></a>마이크로 서비스로 구성된 응용 프로그램 
서비스 패브릭 toobuild 있으며 microservices 컴퓨터의 공유 풀에서, 밀도가 높은 실행, tooas 클러스터 참조 되는 구성 하는 확장성과 안정성이 뛰어난 응용 프로그램을 관리 합니다. 배포 된 경우 컨테이너에서 실행 하는 확장 가능한 상태 비저장 및 상태 저장 microservices 정교 하 고 간단한 런타임 toobuild를 제공 합니다. 또한 포괄적인 응용 프로그램 관리 기능 tooprovision 제공, 배포, 모니터링, 업그레이드/패치 및 컨테이너 화 된 서비스를 포함 하 여 배포 된 응용 프로그램을 삭제 합니다.

Service Fabric은 Azure SQL Database, Azure Cosmos DB, Cortana, Microsoft Power BI, Microsoft Intune, Azure Event Hubs, Azure IoT Hub, Dynamics 365, 비즈니스용 Skype 및 여러 주요 Azure 서비스를 비롯한 오늘날의 여러 Microsoft 서비스를 지원합니다.

서비스 패브릭은 필요에 따라 작은 항목부터 시작 하 고 수백 또는 수천 대 컴퓨터에 toomassive 조정 증가할 수 있는 사용자 지정 된 toocreate 클라우드 네이티브 서비스입니다.

오늘날 인터넷 범위의 서비스는 마이크로 서비스를 토대로 빌드됩니다. 마이크로 서비스의 예로는 프로토콜 게이트웨이, 사용자 프로필, 쇼핑 카트, 인벤토리 처리, 큐, 캐시 등을 들 수 있습니다. Service Fabric은 모든 마이크로 서비스(또는 컨테이너)에 상태 비저장 또는 상태 저장 중 하나일 수 있는 고유한 이름을 제공하는 마이크로 서비스 플랫폼입니다.

서비스 패브릭 포괄적인 런타임 및 수명 주기 관리 기능 tooapplications 이러한 microservices로 구성 된를 제공 합니다. 배포 되 고 hello 서비스 패브릭 클러스터 전체에서 활성화 하는 컨테이너 내부 microservices를 호스팅합니다. 가상 컴퓨터 toocontainers에서 이동에서에서 가능 하 게 순서의 크기가 증가 하는 밀도입니다. 마찬가지로, 이러한 컨테이너에 컨테이너 toomicroservices에서 이동할 때 다른 작업량 밀도가 가능 합니다. 예를 들어, 단일 Azure SQL Database 클러스터는 수십만 개의 데이터베이스를 호스트하는 수만 개의 컨테이너를 실행하는 수백 대의 컴퓨터로 구성됩니다. 각 데이터베이스는 서비스 패브릭 상태 저장 마이크로 서비스입니다. 

Hello microservices 접근 방식에 대 한 자세한에 대 한 읽기 [microservices 접근 방식 toobuilding 응용 프로그램 이유?](service-fabric-overview-microservices.md)

## <a name="container-deployment-and-orchestration"></a>컨테이너 배포 및 오케스트레이션
Service Fabric은 컴퓨터 클러스터에 걸쳐 마이크로 서비스를 배포하는 Microsoft의 [컨테이너 조정자](service-fabric-cluster-resource-manager-introduction.md)입니다. Microservices hello를 사용 하 여 여러 가지 방법으로 개발 될 수 있습니다 [프로그래밍 모델 서비스 패브릭](service-fabric-choose-framework.md), [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md), toodeploying [사용자가 선택한 코드가](service-fabric-deploy-existing-app.md)합니다. 프로세스의 서비스와 서비스 컨테이너에서 hello 모두를 혼합할 수 중요 동일한 응용 프로그램입니다. 원한다 면 너무[배포 및 컨테이너 관리](service-fabric-containers-overview.md), 서비스 패브릭은 컨테이너 orchestrator로 완벽 한 선택입니다.

## <a name="any-os-any-cloud"></a>모든 OS, 모든 클라우드
Service Fabric은 어디에서나 실행됩니다. Azure 또는 온-프레미스, Windows Server 또는 Linux 등 수많은 환경에서 Service Fabric용 클러스터를 만들 수 있습니다. 다른 공용 클라우드에서 클러스터를 만들 수도 있습니다. 또한 hello SDK의에서 hello 개발 환경을 **동일한** toohello 프로덕션 환경과 관련 된 에뮬레이터가 없을 합니다. 즉, 로컬 개발 클러스터에서 실행 되는 어떤 다른 환경에서 toohello 클러스터를 배포 합니다.

![서비스 패브릭 플랫폼][Image1]

온-프레미스 클러스터를 만드는 방법에 대 한 자세한 내용은 참조 [Windows Server 또는 Linux에서 클러스터를 만드는](service-fabric-deploy-anywhere.md) 또는 클러스터를 만드는 azure [hello Azure 포털을 통해](service-fabric-cluster-creation-via-portal.md)합니다.

## <a name="stateless-and-stateful-microservices-for-service-fabric"></a>Service Fabric용 상태 비저장 및 상태 저장 마이크로 서비스
서비스 패브릭 microservices 또는 컨테이너의 구성 된 toobuild 응용 프로그램을 사용 합니다. (예: 프로토콜 게이트웨이 및 웹 프록시) 상태 비저장 microservices 요청과 해당 응답 hello 서비스에서 외부 변경 가능 상태를 유지 하지 않습니다. Azure 클라우드 서비스 작업자 역할이 상태 비저장 서비스의 예입니다. (예: 사용자 계정, 데이터베이스, 장치, 쇼핑 카트 및 큐) 상태 저장 microservices hello 요청 및 응답 이외의 변경할 수 있는 신뢰할 수 있는 상태로 유지합니다. 오늘날 인터넷 범위의 서비스는 상태 비저장 및 상태 저장 마이크로 서비스의 조합으로 구성됩니다. 

서비스 패브릭 키 differentation는 hello를 사용 하 여 상태 저장 서비스를 만드는 강력한 강화 [프로그래밍 모델을 기본 제공 ](service-fabric-choose-framework.md) 하거나 컨테이너 화 된 상태 저장 서비스를 사용 합니다. hello [응용 프로그램 시나리오](service-fabric-application-scenarios.md) hello 시나리오 상태 저장 서비스를 사용 하는 위치에 대해 설명 합니다.


## <a name="application-lifecycle-management"></a>응용 프로그램 수명 주기 관리
서비스 패브릭 hello 전체 응용 프로그램 수명 주기 및 컨테이너를 포함 하 여 클라우드 응용 프로그램의 CI/CD에 대 한 지원을 제공 합니다. 이 수명 배포, 일상적인 관리 및 유지 관리 tooeventual 서비스 해제를 통해 개발 포함 되어 있습니다.

서비스 패브릭 응용 프로그램 수명 주기 관리 기능 사용 응용 프로그램 관리자 및 IT 연산자 toouse 간단 하 고 낮은 터치 워크플로 tooprovision 패치를 배포 하 고 응용 프로그램을 모니터링 합니다. 이러한 기본 제공 워크플로 IT 연산자 tookeep 응용 프로그램에 지속적으로 사용 가능한 hello 부담을 크게 줄어듭니다.

대부분의 응용 프로그램은 함께 배포되는 상태 비저장 및 상태 저장 마이크로 서비스, 컨테이너 및 다른 실행 파일의 조합으로 구성됩니다. 강력한 형식 hello 응용 프로그램에 함으로써 서비스 패브릭 통해 여러 응용 프로그램 인스턴스가 hello 배포할을 수 있습니다. 각 인스턴스는 독립적으로 관리 및 업그레이드됩니다. 무엇보다도 Service Fabric은 컨테이너 또는 모든 실행 파일을 배포하고 안정적으로 만들 수 있습니다. 예를 들어 Service Fabric은 .NET, ASP.NET Core, node.js, Windows 컨테이너, Linux 컨테이너, Java 가상 컴퓨터, 스크립트, Angular 또는 응용 프로그램을 구성하는 다른 모든 항목을 배포할 수 있습니다.

Service Fabric은 [Visual Studio Team Services](https://www.visualstudio.com/team-services/), [Jenkins](https://jenkins.io/index.html) 및 [Octopus 배포](https://octopus.com/)와 같은 CI/CD 도구와 통합되고 다른 인기 있는 CI/CD 도구와 함께 사용할 수 있습니다.

응용 프로그램 수명 주기 관리에 대한 자세한 내용은 [응용 프로그램 수명 주기](service-fabric-application-lifecycle.md)를 참조하세요. 방법에 대 한 자세한 내용을 toodeploy 모든 코드 참조 [게스트 실행 파일을 배포](service-fabric-deploy-existing-app.md)합니다.

## <a name="key-capabilities"></a>주요 기능
서비스 패브릭을 사용하면 다음을 수행할 수 있습니다.

* 코드 변경 사항 없이 사용 Windows 또는 Linux를 실행 하는 tooAzure 또는 tooon 온-프레미스 데이터 센터를 배포 합니다. 한 번만 쓰기를 tooany 서비스 패브릭 클러스터에 아무 곳 이나 배포.
* 확장 가능한 응용 프로그램 구성 된 microservices의 hello 서비스 패브릭 프로그래밍 모델, 컨테이너 또는 모든 코드를 사용 하 여 개발 합니다.
* 매우 안정적인 상태 비저장 및 상태 저장 마이크로 서비스를 개발합니다. 상태 저장 microservices를 사용 하 여 응용 프로그램의 hello 설계를 간소화 합니다. 
* 자체 포함 된 코드와 상태에 있는 hello novel Reliable Actors 프로그래밍 모델 toocreate 클라우드 개체를 사용 합니다.
* Windows 컨테이너 및 Linux 컨테이너를 포함하는 컨테이너를 배포하고 조정합니다. Service Fabric은 데이터를 인식하는 상태 저장 컨테이너 조정자입니다.
* 수백 또는 수천 개의 응용 프로그램 또는 컴퓨터당 컨테이너를 사용하여 몇 초 내로 밀도가 높게 응용 프로그램을 배포합니다.
* 서로 다른 버전의 hello 동일한 응용 프로그램 쪽에서 측면 및 각 응용 프로그램을 개별적으로 업그레이드를 배포 합니다.
* 새로운 및 줄 바꿈하지 않는 업그레이드를 포함 하 여, 중단 시간 없이 응용 프로그램의 hello 수명 주기를 관리 합니다.
* 확장 또는 비율 크기 조정 하는 클러스터의 노드 수가 hello에 합니다. 노드의 크기를 조정하면 응용 프로그램이 자동으로 조정됩니다.
* 모니터링 및 응용 프로그램의 hello 상태를 진단 하 고 자동 복구를 수행 하기 위한 정책을 설정 합니다.
* 응용 프로그램의 hello 재배포 hello 클러스터 간의 조정 hello 리소스 분산 장치를 확인 하십시오. 서비스 패브릭 오류 로부터 복구 하의 사용 가능한 리소스에 따라 로드 hello 배포를 최적화 합니다.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>다음 단계
* 자세한 내용은 다음을 참조하세요.
  * [이유는 microservices toobuilding 응용 프로그램에 접근?](service-fabric-overview-microservices.md)
  * [용어 개요](service-fabric-technical-overview.md)
* 서비스 패브릭 [개발 환경](service-fabric-get-started.md)  
* [Service Fabric 지원 옵션](service-fabric-support.md) 알아보기

[Image1]: media/service-fabric-overview/Service-Fabric-Overview.png
