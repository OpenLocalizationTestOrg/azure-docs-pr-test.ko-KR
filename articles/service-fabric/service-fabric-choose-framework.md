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
# <a name="service-fabric-programming-model-overview"></a><span data-ttu-id="217d3-104">서비스 패브릭 프로그래밍 모델 개요</span><span class="sxs-lookup"><span data-stu-id="217d3-104">Service Fabric programming model overview</span></span>
<span data-ttu-id="217d3-105">서비스 패브릭 여러 방법으로 toowrite 소개 하며 서비스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="217d3-105">Service Fabric offers multiple ways toowrite and manage your services.</span></span> <span data-ttu-id="217d3-106">서비스는 toouse hello 서비스 패브릭 Api tootake 활용 hello 플랫폼의 기능 및 응용 프로그램 프레임 워크를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="217d3-106">Services can choose toouse hello Service Fabric APIs tootake full advantage of hello platform's features and application frameworks.</span></span> <span data-ttu-id="217d3-107">서비스는 Service Fabric 클러스터에서 호스트되는 컨테이너에서 실행 중인 모든 언어 또는 코드로 작성된 컴파일된 실행 프로그램일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="217d3-107">Services can also be any compiled executable program written in any language or code running in a container simply hosted on a Service Fabric cluster.</span></span>

## <a name="guest-executables"></a><span data-ttu-id="217d3-108">게스트 실행 파일</span><span class="sxs-lookup"><span data-stu-id="217d3-108">Guest executables</span></span>
<span data-ttu-id="217d3-109">[게스트 실행 파일](service-fabric-deploy-existing-app.md)은 응용 프로그램에서 서비스로 실행될 수 있는 임의의 기존 실행 파일(작성 언어는 관계없음)입니다.</span><span class="sxs-lookup"><span data-stu-id="217d3-109">A [guest executable](service-fabric-deploy-existing-app.md) is an existing, arbitrary executable (written in any language) that can be run as a service in your application.</span></span> <span data-ttu-id="217d3-110">게스트 실행 파일 hello 서비스 패브릭 SDK Api를 직접 호출 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="217d3-110">Guest executables do not call hello Service Fabric SDK APIs directly.</span></span> <span data-ttu-id="217d3-111">그러나 역시 기능 hello 플랫폼에서 도움이 제안, 서비스 검색 기능, 사용자 지정 상태 보고 서비스 패브릭에서 노출 하는 REST Api를 호출 하 여 부하 등입니다.</span><span class="sxs-lookup"><span data-stu-id="217d3-111">However they still benefit from features hello platform offers, such as service discoverability, custom health and load reporting by calling REST APIs exposed by Service Fabric.</span></span> <span data-ttu-id="217d3-112">또한 전체 응용 프로그램 수명 주기 지원도 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="217d3-112">They also have full application lifecycle support.</span></span>

<span data-ttu-id="217d3-113">첫 번째 [게스트 실행 파일 응용 프로그램](service-fabric-deploy-existing-app.md)을 배포하여 게스트 실행 파일을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="217d3-113">Get started with guest executables by deploying your first [guest executable application](service-fabric-deploy-existing-app.md).</span></span>

## <a name="containers"></a><span data-ttu-id="217d3-114">컨테이너</span><span class="sxs-lookup"><span data-stu-id="217d3-114">Containers</span></span>
<span data-ttu-id="217d3-115">기본적으로 Service Fabric은 이러한 서비스를 프로세스로 배포하고 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="217d3-115">By default, Service Fabric deploys and activates services as processes.</span></span> <span data-ttu-id="217d3-116">Service Fabric도 [컨테이너](service-fabric-containers-overview.md)에 서비스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="217d3-116">Service Fabric can also deploy services in [containers](service-fabric-containers-overview.md).</span></span> <span data-ttu-id="217d3-117">Service Fabric은 Windows Server 2016에서 Linux 컨테이너 및 Windows 컨테이너의 배포를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="217d3-117">Service Fabric supports deployment of Linux containers and Windows containers on Windows Server 2016.</span></span> <span data-ttu-id="217d3-118">컨테이너 이미지는 컨테이너 저장소에서 끌어올 수 있습니다 및 toohello 컴퓨터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="217d3-118">Container images can be pulled from any container repository and deployed toohello machine.</span></span> <span data-ttu-id="217d3-119">게스트 exectuables, 서비스 패브릭 상태 저장 또는 상태 비저장 신뢰할 수 있는 서비스를 기존 응용 프로그램을 배포할 수 있습니다 또는 컨테이너 및 있습니다에서 신뢰할 수 있는 작업자 프로세스의 서비스를 혼합할 수 및 서비스의 컨테이너에서 hello 동일한 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="217d3-119">You can deploy existing applications as guest exectuables, Service Fabric stateless or stateful Reliable services or Reliable Actors in containers, and you can mix services in processes and services in containers in hello same application.</span></span>

[<span data-ttu-id="217d3-120">Windows 또는 Linux에서 서비스를 컨테이너화하는 방법에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="217d3-120">Learn more about containerizing your services in Windows or Linux</span></span>](service-fabric-deploy-container.md)

## <a name="reliable-services"></a><span data-ttu-id="217d3-121">Reliable Services</span><span class="sxs-lookup"><span data-stu-id="217d3-121">Reliable Services</span></span>
<span data-ttu-id="217d3-122">신뢰할 수 있는 서비스는 hello 서비스 패브릭 플랫폼과 통합 하 고 플랫폼 기능 중 일부만 hello에서에서 활용 하는 서비스를 작성 하기 위한 경량 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="217d3-122">Reliable Services is a light-weight framework for writing services that integrate with hello Service Fabric platform and benefit from hello full set of platform features.</span></span> <span data-ttu-id="217d3-123">신뢰할 수 있는 서비스는 hello 서비스 패브릭 런타임에서 toomanage hello의 수명 주기 서비스를 허용 하는 hello 런타임 서비스 toointeract 프로그램을 허용 하 고 Api의 최소 집합을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="217d3-123">Reliable Services provide a minimal set of APIs that allow hello Service Fabric runtime toomanage hello lifecycle of your services and that allow your services toointeract with hello runtime.</span></span> <span data-ttu-id="217d3-124">hello 응용 프로그램 프레임 워크는 최소한의 고 전체 제공 설계 및 구현 옵션이 제어할 수 toohost 사용 되는 모든 다른 응용 프로그램 프레임 워크, ASP.NET Core 등 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="217d3-124">hello application framework is minimal, giving you full control over design and implementation choices, and can be used toohost any other application framework, such as ASP.NET Core.</span></span>

<span data-ttu-id="217d3-125">신뢰할 수 있는 서비스는 상태 비저장, 비슷한 toomost 서비스 플랫폼 예: 웹 서버 hello 서비스의 각 인스턴스는 동일 하 게 생성 하 고 Azure DB 나 Azure 테이블 저장소와 같은 외부 솔루션은 상태가 유지 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="217d3-125">Reliable Services can be stateless, similar toomost service platforms, such as web servers, in which each instance of hello service is created equal and state is persisted in an external solution, such as Azure DB or Azure Table Storage.</span></span>

<span data-ttu-id="217d3-126">신뢰할 수 있는 서비스 일 수도 있습니다 상태 저장 되 고 고유한 tooService 패브릭에서 신뢰할 수 있는 컬렉션을 사용 하 여 자체 hello 서비스에서 직접 상태가 지속 되는 위치.</span><span class="sxs-lookup"><span data-stu-id="217d3-126">Reliable Services can also be stateful, exclusive tooService Fabric, where state is persisted directly in hello service itself using Reliable Collections.</span></span> <span data-ttu-id="217d3-127">상태는 복제를 통해 고가용성이 유지되고 분할을 통해 배포되며, 모두 서비스 패브릭에서 자동으로 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="217d3-127">State is made highly-available through replication and distributed through partitioning, all managed automatically by Service Fabric.</span></span>

<span data-ttu-id="217d3-128">[Reliable Actors에 대해 자세히 알아보거나](service-fabric-reliable-services-introduction.md) [첫 번째 Reliable Services를 작성해 보세요.](service-fabric-reliable-services-quick-start.md)</span><span class="sxs-lookup"><span data-stu-id="217d3-128">[Learn more about Reliable Services](service-fabric-reliable-services-introduction.md) or get started by [writing your first Reliable Service](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="reliable-actors"></a><span data-ttu-id="217d3-129">Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="217d3-129">Reliable Actors</span></span>
<span data-ttu-id="217d3-130">Hello Reliable Actor 프레임 워크에 응용 프로그램 프레임 워크 hello 행위자 디자인 패턴에 따라 hello Virtual Actor 패턴을 구현 하는 신뢰할 수 있는 서비스에서 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="217d3-130">Built on top of Reliable Services, hello Reliable Actor framework is an application framework that implements hello Virtual Actor pattern, based on hello actor design pattern.</span></span> <span data-ttu-id="217d3-131">hello Reliable Actor 프레임 워크 행위자 호출 하는 단일 스레드 실행을 독립적인 단위 계산 및 상태를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="217d3-131">hello Reliable Actor framework uses independent units of compute and state with single-threaded execution called actors.</span></span> <span data-ttu-id="217d3-132">hello Reliable Actor 프레임 워크는 행위자와 미리 설정된 된 상태 지 속성 및 확장 구성에 대 한 기본 제공 통신을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="217d3-132">hello Reliable Actor framework provides built-in communication for actors and pre-set state persistence and scale-out configurations.</span></span>

<span data-ttu-id="217d3-133">자체 Reliable Actors 신뢰할 수 있는 서비스에 구축 된 응용 프로그램 프레임 워크 그대로 완벽 하 게 서비스 패브릭 플랫폼과 hello 전체 집합이 hello 플랫폼에서 제공 하는 기능에서 혜택 hello와 통합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="217d3-133">As Reliable Actors itself is an application framework built on Reliable Services, it is fully integrated with hello Service Fabric platform and benefits from hello full set of features offered by hello platform.</span></span>

<span data-ttu-id="217d3-134">[Reliable Actors에 대해 자세히 알아보거나](service-fabric-reliable-actors-introduction.md) [첫 번째 Reliable Actor 서비스 작성](service-fabric-reliable-actors-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="217d3-134">[Learn more about Reliable Actors](service-fabric-reliable-actors-introduction.md) or get started by [writing your first Reliable Actor service](service-fabric-reliable-actors-get-started.md)</span></span>

## <a name="aspnet-core"></a><span data-ttu-id="217d3-135">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="217d3-135">ASP.NET Core</span></span>
<span data-ttu-id="217d3-136">Service Fabric은 응용 프로그램의 일부로 포함될 수 있는 웹 및 API 서비스를 빌드하기 위해 [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md)와 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="217d3-136">Service Fabric integrates with [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) for building Web and API services that can be included as part of your application.</span></span> 

[<span data-ttu-id="217d3-137">ASP.NET Core를 사용하여 프런트 엔드 서비스 빌드</span><span class="sxs-lookup"><span data-stu-id="217d3-137">Build a front end service using ASP.NET Core</span></span>](service-fabric-add-a-web-frontend.md)

## <a name="next-steps"></a><span data-ttu-id="217d3-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="217d3-138">Next steps</span></span>
[<span data-ttu-id="217d3-139">Service Fabric 및 컨테이너 개요</span><span class="sxs-lookup"><span data-stu-id="217d3-139">Service Fabric and containers overview</span></span>](service-fabric-containers-overview.md)

[<span data-ttu-id="217d3-140">Reliable Services 개요</span><span class="sxs-lookup"><span data-stu-id="217d3-140">Reliable Services overview</span></span>](service-fabric-reliable-services-introduction.md)

[<span data-ttu-id="217d3-141">Reliable Services 개요</span><span class="sxs-lookup"><span data-stu-id="217d3-141">Reliable Services overview</span></span>](service-fabric-reliable-actors-introduction.md)

[<span data-ttu-id="217d3-142">Service Fabric 및 ASP.NET Core </span><span class="sxs-lookup"><span data-stu-id="217d3-142">Service Fabric and ASP.NET Core </span></span>](service-fabric-reliable-services-communication-aspnetcore.md)




