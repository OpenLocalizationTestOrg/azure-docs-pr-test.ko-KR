---
title: "서비스 패브릭 및 컨테이너의 aaaOverview | Microsoft Docs"
description: "서비스 패브릭 및 hello 개요 컨테이너 toodeploy 마이크로 서비스 응용 프로그램의 사용 합니다. 이 문서에서는 컨테이너 사용 될 수 있으며 서비스 패브릭에서 사용할 수 있는 기능을 hello 방법을 대 한 개요를 제공 합니다."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: c98b3fcb-c992-4dd9-b67d-2598a9bf8aab
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: fce94c4b476351c90f23f706aab8bc17319cce22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-and-containers"></a>Service Fabric 및 컨테이너
> [!NOTE]
> 이 기능은 Linux에서 미리 보기로 제공됩니다.  Windows 10에서 tooa 서비스 패브릭 클러스터에서 지원 되지 않습니다는 컨테이너 배포 아직 (출시 예정). 
>   

## <a name="introduction"></a>소개
Azure Service Fabric은 컴퓨터 클러스터에서 사용되는 여러 서비스의 [Orchestrator](service-fabric-cluster-resource-manager-introduction.md)로, Microsoft의 방대한 서비스에서 수년 동안 사용되면서 최적화 과정을 거친 기능입니다. 서비스는 hello를 사용 하 여 다양 한 방식에서 개발 될 수 있습니다 [프로그래밍 모델 서비스 패브릭](service-fabric-choose-framework.md) toodeploying [게스트 실행 파일](service-fabric-deploy-existing-app.md)합니다. 기본적으로 Service Fabric은 이러한 서비스를 프로세스로 배포하고 활성화합니다. 프로세스는 hello 가장 빠른 활성화 및 클러스터의 hello 리소스의 가장 높은 밀도 사용량을 제공합니다. Service Fabric도 컨테이너 이미지에 서비스를 배포할 수 있습니다. 프로세스의 서비스 및 서비스 컨테이너에서 hello 혼합할 수 중요 한 점은 같은 응용 프로그램입니다. 

## <a name="containers-and-service-fabric-roadmap"></a>컨테이너 및 Service Fabric 로드맵
향후 릴리스에서 많은 향상된 기능이 Service Fabric으로 컨테이너 오케스트레이션하도록 계획되어 있습니다. 향상된 기능에는 응용 프로그램, 보안 기능, 향상된 진단 및 도구 지원 내에서 가상 네트워크에 대한 지원으로 향상된 네트워킹에 대한 기능이 포함되어 있습니다. 서비스 패브릭 hello 서비스 패브릭 프로그래밍 모델을 사용 하 여 개발 하는 서비스와 함께 기존 코드 (예를 들어 IIS MVC 응용 프로그램) 패키지 컨테이너를 혼합 toocreate 응용 프로그램 수 있습니다.  단일 클러스터에서 이러한 여러 응용 프로그램을 실행할 수 있습니다. 

## <a name="what-are-containers"></a>컨테이너란?
컨테이너에서 캡슐화 됩니다, 그리고 개별적으로 배포 가능 구성 요소에서 격리 된 인스턴스로 실행 되는 운영 체제에서 제공 하는 가상화에 따른 동일한 커널 tootake 이점은 hello 합니다. 따라서 각 응용 프로그램 및 해당 런타임, 종속성 및 시스템 라이브러리 내에서 실행 컨테이너는 운영 체제 구문 전체, 개인 액세스 toohello 컨테이너의 고유한 격리 보기. 이식성을 이러한 수준의 보안 및 리소스 격리 컨테이너를 사용 하 여 서비스 패브릭 있는 프로세스에서 서비스를 실행 하는 것에 대 한 주요 혜택 hello입니다.

컨테이너는 응용 프로그램에서 기본 운영 체제 hello를 가상화 하는 가상화 기술입니다. 컨테이너는 다양 한 수준의 격리 된 응용 프로그램 toorun에 대 한 변경할 수 없는 환경을 제공합니다. 컨테이너는 hello 커널 기반으로 직접 실행 하 고 별도 hello 파일 시스템의 보기 및 기타 리소스. 컴퓨터 비교 toovirtual 컨테이너 장점 다음 hello 대 한:

* **작은**: 컨테이너는 단일 저장소 공간 및 레이어 버전 및 업데이트 tooincrease 효율성을 사용 합니다.
* **빠른**: 컨테이너 없는 tooboot 전체 운영 체제를은 시작할 수 있도록 훨씬 더 빠르게 일반적으로 (초)에서입니다.
* **이식성**: 컨테이너 화 된 응용 프로그램 이미지 hello 클라우드에서 온-프레미스로 가상 컴퓨터 내 또는 물리적 컴퓨터에서 직접 가져온된 toorun 될 수 있습니다.
* **리소스 관리**: 컨테이너 호스트에서 사용할 수 있는 hello 물리적 리소스를 제한할 수 있습니다.

## <a name="container-types"></a>컨테이너 유형
서비스 패브릭 Linux와 Windows 컨테이너를 지원 하 고 후자 hello에서 Hyper-v 격리 모드도 지원 합니다. 

### <a name="docker-containers-on-linux"></a>Linux의 Docker 컨테이너
Docker 고급 Api toocreate 제공 하 고 Linux 커널 컨테이너 위에 컨테이너를 관리 합니다. Docker 허브 눈에 보는 toostore 이며 컨테이너 이미지를 검색 합니다.
자습서를 참조 하십시오. [Docker 컨테이너 tooService 패브릭 배포](service-fabric-get-started-containers-linux.md)합니다.

### <a name="windows-server-containers"></a>Windows Server 컨테이너
Windows Server 2016 두 가지 유형의 제공 된 격리 수준의 hello에 다른 컨테이너를 제공 합니다. Windows Server 컨테이너 및 Docker 컨테이너 되므로 서로 비슷합니다 둘 다 네임 스페이스 및 파일 시스템 격리 하지만 공유 hello 커널 hello 호스트에서 실행 됩니다. Linux에서, 이러한 격리는 일반적으로 `cgroups` 및 `namespaces`에 의해 제공되었으며 Windows Server 컨테이너도 유사하게 작동합니다.

Windows Hyper-v 컨테이너 hello 호스트 또는 컨테이너의 다른 각 컨테이너 hello 운영 체제 커널 공유 하지 않는 자세한 격리 및 보안을 제공 합니다. 이렇게 보안 격리 수준이 높은 Hyper-V 컨테이너는 적대적인 다중 테넌트 시나리오를 대상으로 합니다.
자습서를 참조 하십시오. [Windows 컨테이너 tooService 패브릭 배포](service-fabric-get-started-containers.md)합니다.

hello 다음 그림은 hello 다양 한 유형의 hello 운영 체제에서 사용할 수 있는 가상화 및 격리 수준.
![Service Fabric 플랫폼][Image1]

## <a name="scenarios-for-using-containers"></a>컨테이너 사용 시나리오
다음은 컨테이너가 적합한 일반적인 예입니다.

* **IIS 리프트 및 이동**: 기존 있는 경우 [ASP.NET MVC](https://www.asp.net/mvc) toocontinue toouse 앱 아닌 컨테이너에 저장 하 코어 tooASP.NET 마이그레이션. 이러한 ASP.NET MVC 앱은 IIS(인터넷 정보 서비스)에 따라 다릅니다. Hello precreated IIS 이미지에서에서 컨테이너 이미지를 이러한 응용 프로그램을 패키지 하 고 서비스 패브릭와 함께 배포할 수 있습니다. 참조 [에 Windows Server 컨테이너 이미지](https://msdn.microsoft.com/virtualization/windowscontainers/quick_start/quick_start_images) 방법에 대 한 정보에 대 한 toocreate IIS 이미지입니다.
* **컨테이너와 Service Fabric 마이크로 서비스의 혼합**: 기존 컨테이너 이미지를 응용 프로그램의 일부에 사용합니다. 예를 들어 hello를 사용할 수 있습니다 [NGINX 컨테이너](https://hub.docker.com/_/nginx/) hello hello에 대 한 상태 저장 서비스 및 응용 프로그램의 웹 프런트 엔드에 대 한 백 엔드 계산을 더 많이 사용 합니다.
* **"시끄러운 이웃" 서비스의 영향을 줄이려면**: 서비스 호스트에서 사용 하는 컨테이너 toorestrict hello 리소스의 hello 리소스 거 버 넌 스 기능을 사용할 수 있습니다. 서비스는 많은 리소스를 소비 하 고 (예: 장기 실행 쿼리 like 연산) 다른 사용자의 hello 성능에 영향을 수 있습니다, 리소스 관리에 있는 컨테이너에 이러한 서비스를 배치 하는 것이 좋습니다.

## <a name="service-fabric-support-for-containers"></a>컨테이너에 대한 Service Fabric 지원
Service Fabric은 현재 Linux에서 Docker 컨테이너의 배포를 지원하고 Hyper-V 격리 모드에 대한 지원과 함께 Windows Server 2016에서 Windows Server 컨테이너의 배포를 지원합니다. 

서비스 패브릭 hello에 [응용 프로그램 모델](service-fabric-application-model.md), 컨테이너 되는 여러 서비스 복제본을 배치 하는 응용 프로그램 호스트를 나타냅니다. 서비스 패브릭 모든 컨테이너를 실행할 수 있으며 hello 시나리오는 비슷한 toohello [게스트 실행 시나리오](service-fabric-deploy-existing-app.md)컨테이너 내부 기존 응용 프로그램을 패키징할 수 있습니다. 이 시나리오는 hello 일반적인 사용 사례, 컨테이너에 대 한 및 예로 모든 언어 또는 프레임 워크를 사용 하 여 hello 기본 제공 서비스 패브릭 프로그래밍 모델을 사용 하지 않고 작성 된 응용 프로그램을 실행 합니다.

또한 컨테이너 내에서 Service Fabric 서비스를 실행할 수도 있습니다. 컨테이너 내부의 실행 중인 서비스 패브릭 서비스에 대 한 지원이 곧 출시 예정인 릴리스에서 향상 된 toobe 하지만 현재 제한 됩니다.

* **신뢰할 수 있는 상태 비저장 서비스 컨테이너 내부의**: 프로그래밍 모델은 Linux 에서만 지원 됩니다. hello 신뢰할 수 있는 서비스를 사용 하 여 신뢰할 수 있는 상태 비저장 서비스입니다. Windows 컨테이너의 Reliable 상태 비저장 서비스에 대한 지원은 향후 릴리스에 예정되어 있습니다.
* **상태 저장 서비스 컨테이너 내부의**: 이러한 서비스 hello Reliable Actors 또는 신뢰할 수 있는 서비스 프로그래밍 모델을 사용 합니다. 컨테이너에서 상태 저장 서비스 실행에 대한 지원은 향후 릴리스에 추가될 예정입니다.

Service Fabric에는 컨테이너화된 마이크로 서비스로 구성된 응용 프로그램을 빌드하는 데 도움을 주는 몇 가지 컨테이너 기능이 있습니다. 서비스 패브릭 hello 다음 컨테이너 화 된 서비스에 대 한 기능을 제공 합니다.

* 컨테이너 이미지 배포 및 활성화
* 리소스 관리
* 리포지토리 인증
* 컨테이너 포트 toohost 포트 매핑을 합니다.
* 컨테이너 간 검색 및 통신
* 기능 tooconfigure 환경 변수를 설정 합니다.

## <a name="next-steps"></a>다음 단계
이 문서에서는 Service Fabric이 컨테이너 오케스트레이터인 컨테이너와 Service Fabric이 컨테이너를 지원하기 위해 제공하는 기능에 대해 알아보았습니다. 다음 단계로 이동지 것입니다 hello 기능 tooshow 가지의 예제를 통해 있습니다 어떻게 toouse 해당 합니다.

[Windows 컨테이너 tooService 패브릭 Windows Server 2016 배포](service-fabric-get-started-containers.md)

[Docker 컨테이너 tooService 패브릭 linux 배포](service-fabric-get-started-containers-linux.md)

[Image1]: media/service-fabric-containers/Service-Fabric-Types-of-Isolation.png
