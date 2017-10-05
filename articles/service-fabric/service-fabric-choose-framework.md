---
title: "Service Fabric 프로그래밍 모델 개요 | Microsoft Docs"
description: "서비스 패브릭은 서비스 빌드에 대해 행위자 프레임워크 및 서비스 프레임워크라는 두 가지 프레임워크를 제공합니다. 이 두 프레임 간에는 단순성과 제어 면에서 고유의 장단점이 있습니다."
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
ms.openlocfilehash: ca36f42897cd44d6da1a3cb6db53f656cf6256ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="service-fabric-programming-model-overview"></a><span data-ttu-id="d6b6a-104">서비스 패브릭 프로그래밍 모델 개요</span><span class="sxs-lookup"><span data-stu-id="d6b6a-104">Service Fabric programming model overview</span></span>
<span data-ttu-id="d6b6a-105">서비스 패브릭은 서비스의 작성 및 관리를 위한 여러 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b6a-105">Service Fabric offers multiple ways to write and manage your services.</span></span> <span data-ttu-id="d6b6a-106">서비스는 플랫폼의 기능과 응용 프로그램 프레임워크를 최대한 활용하기 위해 Service Fabric API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b6a-106">Services can choose to use the Service Fabric APIs to take full advantage of the platform's features and application frameworks.</span></span> <span data-ttu-id="d6b6a-107">서비스는 Service Fabric 클러스터에서 호스트되는 컨테이너에서 실행 중인 모든 언어 또는 코드로 작성된 컴파일된 실행 프로그램일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b6a-107">Services can also be any compiled executable program written in any language or code running in a container simply hosted on a Service Fabric cluster.</span></span>

## <a name="guest-executables"></a><span data-ttu-id="d6b6a-108">게스트 실행 파일</span><span class="sxs-lookup"><span data-stu-id="d6b6a-108">Guest executables</span></span>
<span data-ttu-id="d6b6a-109">[게스트 실행 파일](service-fabric-deploy-existing-app.md)은 응용 프로그램에서 서비스로 실행될 수 있는 임의의 기존 실행 파일(작성 언어는 관계없음)입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b6a-109">A [guest executable](service-fabric-deploy-existing-app.md) is an existing, arbitrary executable (written in any language) that can be run as a service in your application.</span></span> <span data-ttu-id="d6b6a-110">게스트 실행 파일은 Service Fabric SDK API를 직접 호출하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b6a-110">Guest executables do not call the Service Fabric SDK APIs directly.</span></span> <span data-ttu-id="d6b6a-111">그러나 Service Fabric에서 노출하는 REST API를 호출하여 서비스 검색 가능성, 사용자 지정 상태 및 로드 보고와 같이 플랫폼에서 제공하는 기능을 계속 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b6a-111">However they still benefit from features the platform offers, such as service discoverability, custom health and load reporting by calling REST APIs exposed by Service Fabric.</span></span> <span data-ttu-id="d6b6a-112">또한 전체 응용 프로그램 수명 주기 지원도 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b6a-112">They also have full application lifecycle support.</span></span>

<span data-ttu-id="d6b6a-113">첫 번째 [게스트 실행 파일 응용 프로그램](service-fabric-deploy-existing-app.md)을 배포하여 게스트 실행 파일을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b6a-113">Get started with guest executables by deploying your first [guest executable application](service-fabric-deploy-existing-app.md).</span></span>

## <a name="containers"></a><span data-ttu-id="d6b6a-114">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d6b6a-114">Containers</span></span>
<span data-ttu-id="d6b6a-115">기본적으로 Service Fabric은 이러한 서비스를 프로세스로 배포하고 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b6a-115">By default, Service Fabric deploys and activates services as processes.</span></span> <span data-ttu-id="d6b6a-116">Service Fabric도 [컨테이너](service-fabric-containers-overview.md)에 서비스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b6a-116">Service Fabric can also deploy services in [containers](service-fabric-containers-overview.md).</span></span> <span data-ttu-id="d6b6a-117">Service Fabric은 Windows Server 2016에서 Linux 컨테이너 및 Windows 컨테이너의 배포를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b6a-117">Service Fabric supports deployment of Linux containers and Windows containers on Windows Server 2016.</span></span> <span data-ttu-id="d6b6a-118">컨테이너 이미지는 컨테이너 저장소에서 가져오고 컴퓨터에 배포될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b6a-118">Container images can be pulled from any container repository and deployed to the machine.</span></span> <span data-ttu-id="d6b6a-119">기존 응용 프로그램을 컨테이너에서 게스트 실행 파일, Service Fabric 상태 비저장 또는 상태 저장 서비스, Reliable Actors로 배포할 수 있으며, 프로세스의 서비스와 컨테이너의 서비스를 동일한 응용 프로그램에서 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b6a-119">You can deploy existing applications as guest exectuables, Service Fabric stateless or stateful Reliable services or Reliable Actors in containers, and you can mix services in processes and services in containers in the same application.</span></span>

[<span data-ttu-id="d6b6a-120">Windows 또는 Linux에서 서비스를 컨테이너화하는 방법에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="d6b6a-120">Learn more about containerizing your services in Windows or Linux</span></span>](service-fabric-deploy-container.md)

## <a name="reliable-services"></a><span data-ttu-id="d6b6a-121">Reliable Services</span><span class="sxs-lookup"><span data-stu-id="d6b6a-121">Reliable Services</span></span>
<span data-ttu-id="d6b6a-122">Reliable Services는 서비스 패브릭 플랫폼과 통합하여 전체 플랫폼 기능을 활용하는 서비스 작성을 위한 간단한 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b6a-122">Reliable Services is a light-weight framework for writing services that integrate with the Service Fabric platform and benefit from the full set of platform features.</span></span> <span data-ttu-id="d6b6a-123">Reliable Services는 서비스 패브릭 런타임이 서비스의 수명 주기를 관리하고 서비스가 런타임과 상호 작용할 수 있도록 하는 최소한의 API 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b6a-123">Reliable Services provide a minimal set of APIs that allow the Service Fabric runtime to manage the lifecycle of your services and that allow your services to interact with the runtime.</span></span> <span data-ttu-id="d6b6a-124">응용 프로그램 프레임워크는 최소한의 부담으로 완전한 설계 및 구현 제어를 제공하며, 이를 통해 ASP.NET Core 등의 다른 응용 프로그램 프레임워크를 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b6a-124">The application framework is minimal, giving you full control over design and implementation choices, and can be used to host any other application framework, such as ASP.NET Core.</span></span>

<span data-ttu-id="d6b6a-125">Reliable Services는 웹 서버나 등, 대부분의 서비스 플랫폼과 유사하게 상태 비저장이 될 수 있습니다. 여기서는 서비스의 각 인스턴스가 동등하게 생성되고 상태가 Azure DB나 Azure Table Storage 같은 외부 솔루션에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b6a-125">Reliable Services can be stateless, similar to most service platforms, such as web servers, in which each instance of the service is created equal and state is persisted in an external solution, such as Azure DB or Azure Table Storage.</span></span>

<span data-ttu-id="d6b6a-126">Reliable Services는 서비스 패브릭 단독으로 상태를 저장할 수도 있습니다. 여기서는 Reliable Collections를 사용하여 서비스 자체에 상태가 직접적으로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b6a-126">Reliable Services can also be stateful, exclusive to Service Fabric, where state is persisted directly in the service itself using Reliable Collections.</span></span> <span data-ttu-id="d6b6a-127">상태는 복제를 통해 고가용성이 유지되고 분할을 통해 배포되며, 모두 서비스 패브릭에서 자동으로 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b6a-127">State is made highly-available through replication and distributed through partitioning, all managed automatically by Service Fabric.</span></span>

<span data-ttu-id="d6b6a-128">[Reliable Actors에 대해 자세히 알아보거나](service-fabric-reliable-services-introduction.md) [첫 번째 Reliable Services를 작성해 보세요.](service-fabric-reliable-services-quick-start.md)</span><span class="sxs-lookup"><span data-stu-id="d6b6a-128">[Learn more about Reliable Services](service-fabric-reliable-services-introduction.md) or get started by [writing your first Reliable Service](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="reliable-actors"></a><span data-ttu-id="d6b6a-129">Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="d6b6a-129">Reliable Actors</span></span>
<span data-ttu-id="d6b6a-130">Reliable Services의 최상위에 구축되는 Reliable Actor 프레임워크는 행위자 설계 패턴을 기준으로 가상 행위자 패턴을 구현하는 응용 프로그램 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b6a-130">Built on top of Reliable Services, the Reliable Actor framework is an application framework that implements the Virtual Actor pattern, based on the actor design pattern.</span></span> <span data-ttu-id="d6b6a-131">Reliable Actor 프레임워크는 행위자라고 하는 단일 스레드 실행을 통해 독립적인 계산 단위 및 상태를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b6a-131">The Reliable Actor framework uses independent units of compute and state with single-threaded execution called actors.</span></span> <span data-ttu-id="d6b6a-132">Reliable Actor 프레임워크는 행위자와 사전 설정 상태 지속성 및 확장 구성에 대해 기본 포함된 통신을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b6a-132">The Reliable Actor framework provides built-in communication for actors and pre-set state persistence and scale-out configurations.</span></span>

<span data-ttu-id="d6b6a-133">Reliable Actors 자체는 Reliable Services에 구축된 응용 프로그램 프레임워크이므로 서비스 패브릭 플랫폼과 완전히 통합되며 플랫폼이 제공하는 모든 기능을 완벽히 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b6a-133">As Reliable Actors itself is an application framework built on Reliable Services, it is fully integrated with the Service Fabric platform and benefits from the full set of features offered by the platform.</span></span>

<span data-ttu-id="d6b6a-134">[Reliable Actors에 대해 자세히 알아보거나](service-fabric-reliable-actors-introduction.md) [첫 번째 Reliable Actor 서비스 작성](service-fabric-reliable-actors-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="d6b6a-134">[Learn more about Reliable Actors](service-fabric-reliable-actors-introduction.md) or get started by [writing your first Reliable Actor service](service-fabric-reliable-actors-get-started.md)</span></span>

## <a name="aspnet-core"></a><span data-ttu-id="d6b6a-135">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="d6b6a-135">ASP.NET Core</span></span>
<span data-ttu-id="d6b6a-136">Service Fabric은 응용 프로그램의 일부로 포함될 수 있는 웹 및 API 서비스를 빌드하기 위해 [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md)와 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b6a-136">Service Fabric integrates with [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) for building Web and API services that can be included as part of your application.</span></span> 

[<span data-ttu-id="d6b6a-137">ASP.NET Core를 사용하여 프런트 엔드 서비스 빌드</span><span class="sxs-lookup"><span data-stu-id="d6b6a-137">Build a front end service using ASP.NET Core</span></span>](service-fabric-add-a-web-frontend.md)

## <a name="next-steps"></a><span data-ttu-id="d6b6a-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d6b6a-138">Next steps</span></span>
[<span data-ttu-id="d6b6a-139">Service Fabric 및 컨테이너 개요</span><span class="sxs-lookup"><span data-stu-id="d6b6a-139">Service Fabric and containers overview</span></span>](service-fabric-containers-overview.md)

[<span data-ttu-id="d6b6a-140">Reliable Services 개요</span><span class="sxs-lookup"><span data-stu-id="d6b6a-140">Reliable Services overview</span></span>](service-fabric-reliable-services-introduction.md)

[<span data-ttu-id="d6b6a-141">Reliable Services 개요</span><span class="sxs-lookup"><span data-stu-id="d6b6a-141">Reliable Services overview</span></span>](service-fabric-reliable-actors-introduction.md)

[<span data-ttu-id="d6b6a-142">Service Fabric 및 ASP.NET Core </span><span class="sxs-lookup"><span data-stu-id="d6b6a-142">Service Fabric and ASP.NET Core </span></span>](service-fabric-reliable-services-communication-aspnetcore.md)




