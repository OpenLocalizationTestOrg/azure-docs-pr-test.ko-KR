---
title: "Azure Service Fabric 용어 aaaLearn | Microsoft Docs"
description: "서비스 패브릭의 용어에 대해 간략하게 소개하고 주요 용어 개념 및 hello 설명서의 hello 나머지 부분에 사용 된 용어에 설명 합니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: chackdan;subramar
ms.assetid: 3a970679-e19e-43b3-9be8-71773f307c57
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/02/2017
ms.author: ryanwi
ms.openlocfilehash: 4781fc0527b8a58e534183249bc2759aded2730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-terminology-overview"></a>서비스 패브릭 용어 개요
서비스 패브릭은 분산된 시스템 플랫폼으로 쉽게 toopackage를 사용 하면을 배포 하 고 확장성과 안정성이 뛰어난 microservices 관리 합니다. 서비스 패브릭 toounderstand hello 용어 hello 설명서에서 사용 하 여 사용 되는이 항목 세부 정보 hello 용어입니다.

hello이 섹션에 나열 된 개념 에서도 설명 Microsoft Virtual Academy 동영상을 따라 hello: <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">핵심 개념</a>, <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tlkI046yC_2906218965">디자인 타임 개념</a>, 및 <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=x7CVH56yC_1406218965">런타임에개념</a>.

## <a name="infrastructure-concepts"></a>인프라 개념
**클러스터**: 마이크로 서비스가 배포되고 관리되는 네트워크로 연결된 가상 또는 실제 컴퓨터 집합입니다.  클러스터의 컴퓨터 toothousands를 확장할 수 있습니다.

**노드**: 클러스터의 일부인 컴퓨터로 VM 노드라고 합니다. 각 노드는 노드 이름(문자열)에 할당됩니다. 노드는 배치 속성과 같은 특징이 있습니다. 각 컴퓨터 또는 VM이 Windows 서비스인 `FabricHost.exe`를 자동으로 시작하여 부팅을 실행하기 시작한 다음 `Fabric.exe` 및 `FabricGateway.exe`이라는 두 개의 실행 파일을 시작합니다. 이러한 두 개의 실행 개체는 hello 노드를 확인합니다. 테스트 시나리오에서는 `Fabric.exe` 및 `FabricGateway.exe`와 같은 여러 인스턴스를 실행하여 단일 컴퓨터 또는 VM에 여러 노드를 호스트할 수 있습니다.

## <a name="application-concepts"></a>응용 프로그램 개념
**응용 프로그램 종류**: hello 서비스 형식의 할당 된 이름/버전 tooa 컬렉션입니다. 에 정의 된는 `ApplicationManifest.xml` 파일, toohello 서비스 패브릭 클러스터 이미지 저장소 복사 다음에 응용 프로그램 패키지 디렉터리에 포함 합니다. 그런 다음 hello 클러스터 내에서이 응용 프로그램 종류에서 명명된 된 응용 프로그램을 만들 수 있습니다.

읽기 hello [응용 프로그램 모델](service-fabric-application-model.md) 대 한 자세한 내용은 문서.

**응용 프로그램 패키지**: hello 응용 프로그램 종류를 포함 하는 디스크 디렉터리 `ApplicationManifest.xml` 파일입니다. 참조 hello hello 응용 프로그램 종류를 구성 하는 각 서비스 유형에 대 한 서비스 패키지입니다. hello 응용 프로그램 패키지 디렉터리의 hello 파일은 복사 tooService 패브릭 클러스터 이미지 저장소입니다. 예를 들어 전자 메일 응용 프로그램 종류에 대 한 응용 프로그램 패키지 참조가 tooa 큐 서비스 패키지, 프런트 엔드 서비스 패키지 및 데이터베이스 서비스 패키지를 포함할 수 있습니다.

**이름은 응용 프로그램**: hello 응용 프로그램 패키지의 응용 프로그램 종류 (이름/버전 사용)를 지정 하 여 hello 클러스터 내에서 hello 응용 프로그램의 인스턴스를 만들 응용 프로그램 패키지를 복사한 toohello 이미지 저장소 후 합니다. 각 응용 프로그램 형식 인스턴스는 `"fabric:/MyNamedApp"`와 같은 URI 이름이 할당됩니다. 클러스터 내에서 단일 응용 프로그램 형식에서 여러 명명된 응용 프로그램을 만들 수 있습니다. 또한 다른 형식의 응용 프로그램에서 명명된 응용 프로그램을 만들 수 있습니다. 명명된 응용 프로그램은 각각 독립적으로 관리되고 버전이 지정됩니다.      

**서비스 유형**: hello 이름/버전 tooa 서비스의 코드 패키지, 데이터 패키지 및 패키지 구성에 할당 합니다. 에 정의 된 한 `ServiceManifest.xml` 파일을 서비스 패키지 디렉터리 및 hello 서비스 패키지 디렉터리에 포함 된 응용 프로그램 패키지에서 참조 한 다음 `ApplicationManifest.xml` 파일입니다. Hello 클러스터 내에서 명명된 된 응용 프로그램을 만든 후 만들 수 있습니다는 명명된 서비스 hello 중 하나에서 응용 프로그램 종류의 서비스 유형. 서비스 유형 hello `ServiceManifest.xml` 파일 hello 서비스에 설명 합니다.

읽기 hello [응용 프로그램 모델](service-fabric-application-model.md) 대 한 자세한 내용은 문서.

서비스의 두 가지 형식이 있습니다.

* **Stateless:** hello 서비스의 영구 상태와 같은 Azure 저장소, Azure SQL 데이터베이스 또는 Azure Cosmos DB는 외부 저장소 서비스에 저장 되 면 상태 비저장 서비스를 사용 합니다. 에 영구 저장소가 없는 전혀 hello 서비스 하는 경우에 상태 비저장 서비스를 사용 합니다. 예를 들어는 계산기 서비스 여기서 값 toohello 서비스에 전달 됩니다, 계산 이러한 값을 사용 하 여 수행 됩니다 결과가 반환 됩니다.
* **상태 저장:** 서비스 패브릭 toomanage의 신뢰할 수 있는 컬렉션 또는 Reliable Actors 프로그래밍 모델을 통해 서비스의 상태를 원하는 경우 상태 저장 서비스를 사용 합니다. Toospread 프로그램 상태를 통해 하려는 (확장성)에 대 한 경우는 파티션의 수를 지정 합니다. 명명 된 서비스 만들기. Tooreplicate 횟수를 지정할 수도 노드 (안정성)에 대 한 전체 상태입니다. 명명된 서비스 각각에는 하나의 기본 복제본과 여러 보조 복제본이 있습니다. Toohello 주 복제본을 작성 하 여 명명 된 서비스의 상태를 수정 합니다. 서비스 패브릭은이 상태 tooall hello 보조 복제본 동기화 상태를 유지 한 다음 복제 합니다. 서비스 패브릭 실패 하 고 기존 보조 복제본 tooa 주 복제본을 승격 하는 주 복제본에 자동으로 검색 합니다. 그러면 서비스 패브릭은 새로운 보조 복제본을 만듭니다.  

**서비스 패키지**: hello 서비스 형식이 포함 된 디스크 디렉터리 `ServiceManifest.xml` 파일입니다. 이 파일은 hello 코드, 정적 데이터 및 구성 패키지 hello 서비스 유형에 대 한 참조입니다. hello 응용 프로그램 종류에서 참조 하는 hello 서비스 패키지 디렉터리에 파일 hello `ApplicationManifest.xml` 파일입니다. 예를 들어 서비스 패키지 toohello 코드, 정적 데이터 및 데이터베이스 서비스를 구성 하는 구성 패키지를 참조할 수 있습니다.

**서비스 라는**: 명명된 된 응용 프로그램을 만든 후 hello 서비스 유형 (이름/버전 사용)를 지정 하 여 hello 클러스터 내에서 해당 서비스 형식의 인스턴스를 만들 수 있습니다. 각 서비스 형식 인스턴스는 명명된 응용 프로그램의 URI로 범위가 지정된 URI 이름이 할당됩니다. 예를 들어 "MyDatabase" 라는 이름은 응용 프로그램 "MyNamedApp" 내 서비스를 만들면 hello URI 같습니다: `"fabric:/MyNamedApp/MyDatabase"`합니다. 명명된 응용 프로그램 내에서 몇 가지 명명된 서비스를 만들 수 있습니다. 명명된 각 서비스는 고유한 파티션 구성표 및 복제본/인스턴스 수를 가질 수 있습니다.

**코드 패키지**: hello 서비스 유형을 실행 파일 (일반적으로 EXE/DLL 파일)를 포함 하는 디스크 디렉터리입니다. hello 서비스 종류에서 참조 하는 hello 코드 패키지 디렉터리에 파일 hello `ServiceManifest.xml` 파일입니다. 명명 된 서비스를 만들면 hello 코드 패키지는 복사한 toohello 노드 또는 노드 선택한 toorun hello 라는 서비스. 그런 다음 hello 코드 실행을 시작 합니다. 코드 패키지 실행 파일은 다음과 같은 두 종류가 있습니다.

* **게스트 실행 파일**:으로 실행 하는 실행 파일-hello 호스트 운영 체제 (Windows 또는 Linux)에 있습니다. 즉, 이러한 실행 파일 서비스 패브릭 런타임에서 파일 링크 tooor 참조 하지 않는 및 모든 서비스 패브릭 프로그래밍 모델을 사용 하지 마십시오. 이러한 실행 파일 이름 지정에 대 한 끝점 검색 서비스와 같은 일부 서비스 패브릭 기능 hello 없습니다 toouse 됩니다. 게스트 실행 파일 부하 메트릭을 특정 tooeach 서비스 인스턴스를 보고할 수 없습니다.
* **서비스 호스트 실행 파일**: 서비스 패브릭 기능을 사용 하도록 서비스 패브릭 tooService 패브릭 런타임 파일을 연결 하 여 프로그래밍 모델을 사용 하는 실행 파일입니다. 예를 들어 명명된 서비스 인스턴스는 서비스 패브릭의 이름 지정 서비스를 사용하여 끝점을 등록할 수 있고 부하 메트릭을 보고할 수도 있습니다.      

**데이터 패키지**: hello 서비스 유형이 정적, 읽기 전용 데이터 파일 (일반적으로: 사진, 소리 및 비디오 파일)를 포함 하는 디스크 디렉터리입니다. hello 서비스 종류에서 참조 하는 hello 데이터 패키지 디렉터리에 파일 hello `ServiceManifest.xml` 파일입니다. 명명 된 서비스를 만들면 hello 데이터 패키지는 복사한 toohello 노드 또는 노드 선택한 toorun hello 라는 서비스.  hello 코드 실행을 시작 하 고 이제 hello 데이터 파일에 액세스할 수 있습니다.

**구성 패키지**: hello 서비스 유형이 정적을 포함 하는 디스크 디렉터리, 읽기 전용으로 구성 파일 (일반적으로 텍스트 파일). hello 서비스 종류에서 참조 하는 hello 구성 패키지 디렉터리에서 파일 hello `ServiceManifest.xml` 파일입니다. 명명 된 서비스를 만들면 hello 구성 패키지의 hello 파일은 복사 toohello 하나 또는 더 많은 노드 선택한 toorun hello 라는 서비스입니다. 그런 다음 hello 코드 실행을 시작 하 고 이제 hello 구성 파일에 액세스할 수 있습니다.

**컨테이너**: 기본적으로 Service Fabric은 이러한 서비스를 프로세스로 배포하고 활성화합니다. Service Fabric도 컨테이너 이미지에 서비스를 배포할 수 있습니다. 컨테이너는 응용 프로그램에서 기본 운영 체제 hello를 가상화 하는 가상화 기술입니다. 응용 프로그램 및 해당 런타임, 종속성 및 시스템 라이브러리는 운영 체제 구문 전체, 개인 액세스 toohello 컨테이너의 고유한 격리 보기 컨테이너 내에서 실행 합니다. Service Fabric은 Linux 및 Windows Server 컨테이너에서 Docker 컨테이너를 지원합니다.  자세한 내용은 [Service Fabric 및 컨테이너](service-fabric-containers-overview.md)를 참조하세요.

**파티션 구성표**: 명명된 서비스를 만들 때 파티션 구성표를 지정합니다. 많은 양의 상태를 사용 하 여 서비스는 hello 상태 hello 클러스터의 노드 전체에 분산 하는 파티션 간에 hello 데이터를 분할 합니다. 이렇게 하면 명명 된 서비스의 상태 tooscale가 있습니다. 상태 저장 서비스에 복제본이 있는 반면 파티션 내에서 명명된 상태 비저장 서비스에는 인스턴스가 있습니다. 일반적으로 명명된 상태 비저장 서비스는 내부 상태가 없기 때문에 하나의 파티션만을 가질 수 있습니다. 가용성;에 대 한 hello 파티션 인스턴스 제공 하나의 인스턴스가 실패 하면 다른 인스턴스와 toooperate를 정상적으로 계속 하 고 그런 다음 서비스 패브릭은 새 인스턴스를 만듭니다. 명명 된 서비스 상태 저장 복제본 내에서 상태를 유지 하 고 각 파티션에 자체 복제본을 동기화 상태로 유지 되 고 모든 hello 상태로 설정 하는 합니다. 서비스 패브릭 복제 실패로 처리할지, hello 기존 복제본에서 새 복제 데이터베이스를 작성 합니다.

읽기 hello [신뢰할 수 있는 파티션 서비스 패브릭 서비스](service-fabric-concepts-partitioning.md) 대 한 자세한 내용은 문서.

## <a name="system-services"></a>시스템 서비스
서비스 패브릭의 hello 플랫폼 기능을 제공 하는 모든 클러스터에서 만들어진 시스템 서비스가 있습니다.

**서비스 이름 지정**: 각 서비스 패브릭 클러스터에 hello 클러스터에서 서비스 이름을 tooa 위치를 확인 하는 명명 서비스를 합니다. Hello 서비스 이름, 속성, 비슷한 tooan 관리 인터넷 서비스 DNS (Domain Name) hello 클러스터에 대 한 합니다. 클라이언트는 서비스 이름 및 해당 위치에 안전 하 게 명명 서비스 tooresolve hello를 사용 하 여 hello 클러스터에 있는 모든 노드 통신 합니다.  예를 들어 기한 toofailures, 리소스 분산 또는 hello 클러스터의 크기 조정 hello hello 클러스터 내에서 응용 프로그램 이동 합니다. 서비스와 클라이언트 hello 현재 네트워크 위치를 확인 있는 개발할 수 있습니다. 클라이언트는 hello 실제 컴퓨터 IP 주소와 현재 실행 중인 포트를 가져옵니다.

읽기 [서비스와 통신](service-fabric-connect-and-communicate-with-services.md) hello 클라이언트와 서비스 통신 hello 명명 서비스를 사용 하는 Api에 대 한 자세한 내용은 합니다.

**이미지 저장소 서비스**: 각 서비스 패브릭 클러스터에는 배포되어 버전이 지정된 응용 프로그램 패키지가 보관되는 이미지 저장소 서비스가 있습니다. 응용 프로그램 패키지 toohello 이미지 저장소를 복사한 다음 해당 응용 프로그램 패키지 내에 포함 된 hello 응용 프로그램 종류를 등록 합니다. Hello 응용 프로그램 유형을 프로 비전 되 면 여기에서 명명된 된 응용 프로그램을 만듭니다. 명명 된 모든 응용 프로그램을 삭제 한 후 hello 이미지 저장소 서비스에서에서 응용 프로그램 종류를 등록 취소할 수 있습니다.

읽기 [hello ImageStoreConnectionString 설정 이해](service-fabric-image-store-connection-string.md) hello 이미지 저장소 서비스에 대 한 자세한 내용은 합니다.

읽기 hello [응용 프로그램 배포](service-fabric-deploy-remove-applications.md) 응용 프로그램 toohello 이미지 저장소 서비스를 배포 하는 방법에 대 한 자세한 내용은 문서입니다.

## <a name="built-in-programming-models"></a>기본 제공 프로그래밍 모델
Toobuild 서비스 패브릭 서비스를 사용할 수 있는.NET Framework 프로그래밍 모델은:

**신뢰할 수 있는 서비스**: API toobuild 상태 비저장 및 상태 저장 서비스입니다. 상태 저장 서비스는 신뢰할 수 있는 컬렉션(예: 사전 또는 큐)에 자신의 상태를 저장합니다. 웹 API 및 Windows Communication Foundation (WCF)와 같은 다양 한 통신 스택에 tooplug를 가져올 수도 있습니다.

**Reliable Actors**: hello 가상 행위자 프로그래밍 모델을 통해 API toobuild 상태 비저장 및 상태 저장 개체입니다. 이 모델은 계산/상태의 독립적인 단위가 많은 경우 유용할 수 있습니다. 되기 때문에이 모델 턴 기반 스레딩 모델을 사용 하는 경우 개별 행위자의 아웃 바운드 요청을 모두 완료 될 때까지 다른 들어오는 요청을 처리할 수 없습니다 이후 tooother 행위자 또는 서비스를 호출 하는 가장 좋은 tooavoid 코드.

읽기 hello [서비스에 대 한 프로그래밍 모델 선택](service-fabric-choose-framework.md) 대 한 자세한 내용은 문서.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>다음 단계
서비스 패브릭에 대 한 자세한 toolearn:

* [서비스 패브릭의 개요](service-fabric-overview.md)
* [이유는 microservices toobuilding 응용 프로그램에 접근?](service-fabric-overview-microservices.md)
* [응용 프로그램 시나리오](service-fabric-application-scenarios.md)

