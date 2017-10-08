---
title: "aaaService 패브릭 프로그래밍 모델 개요 | Microsoft Docs"
description: "서비스 패브릭 서비스를 구축 하기 위한 두 프레임 워크를 제공: hello 행위자 프레임 워크 및 hello 서비스 프레임 워크입니다. 이 두 프레임 간에는 단순성과 제어 면에서 고유의 장단점이 있습니다."
services: service-fabric
documentationcenter: .net
author: seanmck
manager: timlt
editor: vturecek
ms.assetid: 974b2614-014e-4587-a947-28fcef28b382
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: vturecek
ms.openlocfilehash: b48af2a7b41935bdf0e4594c765f363e520c254e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-programming-model-overview"></a>서비스 패브릭 프로그래밍 모델 개요
서비스 패브릭 여러 방법으로 toowrite 소개 하며 서비스를 관리 합니다. 서비스는 toouse hello 서비스 패브릭 Api tootake 활용 hello 플랫폼의 기능 및 응용 프로그램 프레임 워크를 선택할 수 있습니다. 서비스는 Service Fabric 클러스터에서 호스트되는 컨테이너에서 실행 중인 모든 언어 또는 코드로 작성된 컴파일된 실행 프로그램일 수도 있습니다.

## <a name="guest-executables"></a>게스트 실행 파일
[게스트 실행 파일](service-fabric-deploy-existing-app.md)은 응용 프로그램에서 서비스로 실행될 수 있는 임의의 기존 실행 파일(작성 언어는 관계없음)입니다. 게스트 실행 파일 hello 서비스 패브릭 SDK Api를 직접 호출 하지 않습니다. 그러나 역시 기능 hello 플랫폼에서 도움이 제안, 서비스 검색 기능, 사용자 지정 상태 보고 서비스 패브릭에서 노출 하는 REST Api를 호출 하 여 부하 등입니다. 또한 전체 응용 프로그램 수명 주기 지원도 포함합니다.

첫 번째 [게스트 실행 파일 응용 프로그램](service-fabric-deploy-existing-app.md)을 배포하여 게스트 실행 파일을 시작합니다.

## <a name="containers"></a>컨테이너
기본적으로 Service Fabric은 이러한 서비스를 프로세스로 배포하고 활성화합니다. Service Fabric도 [컨테이너](service-fabric-containers-overview.md)에 서비스를 배포할 수 있습니다. Service Fabric은 Windows Server 2016에서 Linux 컨테이너 및 Windows 컨테이너의 배포를 지원합니다. 컨테이너 이미지는 컨테이너 저장소에서 끌어올 수 있습니다 및 toohello 컴퓨터를 배포 합니다. 게스트 exectuables, 서비스 패브릭 상태 저장 또는 상태 비저장 신뢰할 수 있는 서비스를 기존 응용 프로그램을 배포할 수 있습니다 또는 컨테이너 및 있습니다에서 신뢰할 수 있는 작업자 프로세스의 서비스를 혼합할 수 및 서비스의 컨테이너에서 hello 동일한 응용 프로그램입니다.

[Windows 또는 Linux에서 서비스를 컨테이너화하는 방법에 대해 자세히 알아보기](service-fabric-deploy-container.md)

## <a name="reliable-services"></a>Reliable Services
신뢰할 수 있는 서비스는 hello 서비스 패브릭 플랫폼과 통합 하 고 플랫폼 기능 중 일부만 hello에서에서 활용 하는 서비스를 작성 하기 위한 경량 프레임 워크입니다. 신뢰할 수 있는 서비스는 hello 서비스 패브릭 런타임에서 toomanage hello의 수명 주기 서비스를 허용 하는 hello 런타임 서비스 toointeract 프로그램을 허용 하 고 Api의 최소 집합을 제공 합니다. hello 응용 프로그램 프레임 워크는 최소한의 고 전체 제공 설계 및 구현 옵션이 제어할 수 toohost 사용 되는 모든 다른 응용 프로그램 프레임 워크, ASP.NET Core 등 일 수 있습니다.

신뢰할 수 있는 서비스는 상태 비저장, 비슷한 toomost 서비스 플랫폼 예: 웹 서버 hello 서비스의 각 인스턴스는 동일 하 게 생성 하 고 Azure DB 나 Azure 테이블 저장소와 같은 외부 솔루션은 상태가 유지 될 수 있습니다.

신뢰할 수 있는 서비스 일 수도 있습니다 상태 저장 되 고 고유한 tooService 패브릭에서 신뢰할 수 있는 컬렉션을 사용 하 여 자체 hello 서비스에서 직접 상태가 지속 되는 위치. 상태는 복제를 통해 고가용성이 유지되고 분할을 통해 배포되며, 모두 서비스 패브릭에서 자동으로 관리합니다.

[Reliable Actors에 대해 자세히 알아보거나](service-fabric-reliable-services-introduction.md) [첫 번째 Reliable Services를 작성해 보세요.](service-fabric-reliable-services-quick-start.md)

## <a name="reliable-actors"></a>Reliable Actors
Hello Reliable Actor 프레임 워크에 응용 프로그램 프레임 워크 hello 행위자 디자인 패턴에 따라 hello Virtual Actor 패턴을 구현 하는 신뢰할 수 있는 서비스에서 구현 합니다. hello Reliable Actor 프레임 워크 행위자 호출 하는 단일 스레드 실행을 독립적인 단위 계산 및 상태를 사용 합니다. hello Reliable Actor 프레임 워크는 행위자와 미리 설정된 된 상태 지 속성 및 확장 구성에 대 한 기본 제공 통신을 제공합니다.

자체 Reliable Actors 신뢰할 수 있는 서비스에 구축 된 응용 프로그램 프레임 워크 그대로 완벽 하 게 서비스 패브릭 플랫폼과 hello 전체 집합이 hello 플랫폼에서 제공 하는 기능에서 혜택 hello와 통합 됩니다.

[Reliable Actors에 대해 자세히 알아보거나](service-fabric-reliable-actors-introduction.md) [첫 번째 Reliable Actor 서비스 작성](service-fabric-reliable-actors-get-started.md)

## <a name="aspnet-core"></a>ASP.NET Core
Service Fabric은 응용 프로그램의 일부로 포함될 수 있는 웹 및 API 서비스를 빌드하기 위해 [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md)와 통합됩니다. 

[ASP.NET Core를 사용하여 프런트 엔드 서비스 빌드](service-fabric-add-a-web-frontend.md)

## <a name="next-steps"></a>다음 단계
[Service Fabric 및 컨테이너 개요](service-fabric-containers-overview.md)

[Reliable Services 개요](service-fabric-reliable-services-introduction.md)

[Reliable Services 개요](service-fabric-reliable-actors-introduction.md)

[Service Fabric 및 ASP.NET Core ](service-fabric-reliable-services-communication-aspnetcore.md)




