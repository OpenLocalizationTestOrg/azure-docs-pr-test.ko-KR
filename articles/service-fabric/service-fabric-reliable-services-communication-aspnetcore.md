---
title: "ASP.NET Core와 서비스 통신 | Microsoft Docs"
description: "상태 비저장 및 상태 저장 Reliable Services에서 ASP.NET Core를 사용하는 방법에 대해 알아봅니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 8aa4668d-cbb6-4225-bd2d-ab5925a868f2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/02/2017
ms.author: vturecek
ms.openlocfilehash: 8ac4d409f7363e8b4ae98be659a627ac8db8d787
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-core-in-service-fabric-reliable-services"></a><span data-ttu-id="4c601-103">Service Fabric Reliable Services의 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="4c601-103">ASP.NET Core in Service Fabric Reliable Services</span></span>

<span data-ttu-id="4c601-104">ASP.NET Core는 웹앱, IoT 앱 및 모바일 백 엔드와 같은 최신 클라우드 기반의 인터넷 연결 응용 프로그램을 빌드하기 위한 새로운 오픈 소스 겸 플랫폼 간 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-104">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based Internet-connected applications, such as web apps, IoT apps, and mobile backends.</span></span> 

<span data-ttu-id="4c601-105">이 문서는 NuGet 패키지의 **Microsoft.ServiceFabric.AspNetCore.*** 집합을 사용하여 Service Fabric Reliable Services에서 ASP.NET Core 서비스 호스팅에 대한 자세한 가이드입니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-105">This article is an in-depth guide to hosting ASP.NET Core services in Service Fabric Reliable Services using the **Microsoft.ServiceFabric.AspNetCore.*** set of NuGet packages.</span></span>

<span data-ttu-id="4c601-106">Service Fabric에서 ASP.NET Core의 소개 자습서 및 개발 환경 설정을 가져오는 방법에 대한 지침은 [ASP.NET Core를 사용하여 응용 프로그램에 대한 웹 프런트 엔드 구축](service-fabric-add-a-web-frontend.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4c601-106">For an introductory tutorial on ASP.NET Core in Service Fabric and instructions on getting your development environment set up, see [Building a web front-end for your application using ASP.NET Core](service-fabric-add-a-web-frontend.md).</span></span>

<span data-ttu-id="4c601-107">이 문서의 나머지 부분에서는 ASP.NET Core를 잘 알고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-107">The rest of this article assumes you are already familiar with ASP.NET Core.</span></span> <span data-ttu-id="4c601-108">그렇지 않은 경우 [ASP.NET Core 기본 사항](https://docs.microsoft.com/aspnet/core/fundamentals/index)을 통해 읽어 보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-108">If not, we recommend reading through the [ASP.NET Core fundamentals](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span></span>

## <a name="aspnet-core-in-the-service-fabric-environment"></a><span data-ttu-id="4c601-109">Service Fabric 환경에서 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="4c601-109">ASP.NET Core in the Service Fabric environment</span></span>

<span data-ttu-id="4c601-110">ASP.NET Core 앱은 .NET Core 또는 전체 .NET Framework에서 실행될 수 있지만, Service Fabric 서비스는 현재 전체 .NET Framework에서만 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-110">While ASP.NET Core apps can run on .NET Core or on the full .NET Framework, Service Fabric services currently can only run on the full .NET Framework.</span></span> <span data-ttu-id="4c601-111">즉, ASP.NET Core Service Fabric 서비스를 빌드할 때에도 전체 .NET Framework를 대상으로 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-111">This means when you build an ASP.NET  Core Service Fabric service, you must still target the full .NET Framework.</span></span>

<span data-ttu-id="4c601-112">ASP.NET Core는 Service Fabric에서 다음 두 가지 방식으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-112">ASP.NET Core can be used in two different ways in Service Fabric:</span></span>
 - <span data-ttu-id="4c601-113">**게스트 실행 파일로 호스팅됨** -</span><span class="sxs-lookup"><span data-stu-id="4c601-113">**Hosted as a guest executable**.</span></span> <span data-ttu-id="4c601-114">주로 코드 변경 없이 Service Fabric에서 기존 ASP.NET Core 응용 프로그램을 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-114">This is primarily used to run existing ASP.NET Core applications on Service Fabric with no code changes.</span></span>
 - <span data-ttu-id="4c601-115">**Reliable Service에서 실행** -</span><span class="sxs-lookup"><span data-stu-id="4c601-115">**Run inside a Reliable Service**.</span></span> <span data-ttu-id="4c601-116">향상된 Service Fabric 런타임 통합과 상태 저장 ASP.NET Core 서비스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-116">This allows better integration with the Service Fabric runtime and allows stateful ASP.NET Core services.</span></span>

<span data-ttu-id="4c601-117">이 문서의 나머지 부분에서는 Service Fabric SDK와 함께 제공되는 ASP.NET Core 통합 구성 요소를 사용하여 Reliable Service 내에서 ASP.NET Core를 사용하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-117">The rest of this article explains how to use ASP.NET Core inside a Reliable Service using the ASP.NET Core integration components that ship with the Service Fabric SDK.</span></span> 

## <a name="service-fabric-service-hosting"></a><span data-ttu-id="4c601-118">Service Fabric 서비스 호스팅</span><span class="sxs-lookup"><span data-stu-id="4c601-118">Service Fabric service hosting</span></span>

<span data-ttu-id="4c601-119">Service Fabric에서 서비스의 인스턴스 및/또는 복제본이 하나 이상 *서비스 호스트 프로세스*(서비스 코드를 실행하는 실행 파일)에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-119">In Service Fabric, one or more instances and/or replicas of your service run in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="4c601-120">서비스 작성자는 서비스 호스트 프로세스를 소유하고, Service Fabric은 이 사용자를 위해 해당 프로세스를 활성화하고 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-120">You, as a service author, own the service host process and Service Fabric activates and monitors it for you.</span></span>

<span data-ttu-id="4c601-121">기존 ASP.NET(MVC 5 이하)은 System.Web.dll을 통해 IIS에 긴밀하게 결합됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-121">Traditional ASP.NET (up to MVC 5) is tightly coupled to IIS through System.Web.dll.</span></span> <span data-ttu-id="4c601-122">ASP.NET Core는 웹 서버와 웹 응용 프로그램 간의 분리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-122">ASP.NET Core provides a separation between the web server and your web application.</span></span> <span data-ttu-id="4c601-123">이렇게 하면 웹 응용 프로그램을 여러 웹 서버 간에 이동할 수 있으며 웹 서버를 *자체 호스팅*할 수도 있습니다. 즉, IIS와 같은 전용 웹 서버 소프트웨어에서 소유한 프로세스가 아니라 자신의 프로세스에서 웹 서버를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-123">This allows web applications to be portable between different web servers and also allows web servers to be *self-hosted*, which means you can start a web server in your own process, as opposed to a process that is owned by dedicated web server software such as IIS.</span></span> 

<span data-ttu-id="4c601-124">Service Fabric 서비스와 ASP.NET을 게스트 실행 파일로 또는 Reliable Service에서 결합하려면 서비스 호스트 프로세스 내에서 ASP.NET을 시작할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-124">In order to combine a Service Fabric service and ASP.NET, either as a guest executable or in a Reliable Service, you must be able to start ASP.NET inside your service host process.</span></span> <span data-ttu-id="4c601-125">ASP.NET Core 자체 호스팅을 사용하면 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-125">ASP.NET Core self-hosting allows you to do this.</span></span>

## <a name="hosting-aspnet-core-in-a-reliable-service"></a><span data-ttu-id="4c601-126">Reliable Service에서 ASP.NET Core 호스팅</span><span class="sxs-lookup"><span data-stu-id="4c601-126">Hosting ASP.NET Core in a Reliable Service</span></span>
<span data-ttu-id="4c601-127">일반적으로 자체 호스팅되는 ASP.NET Core 응용 프로그램은 `Program.cs`의 `static void Main()` 메서드와 같이 응용 프로그램의 진입점에 WebHost를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-127">Typically, self-hosted ASP.NET Core applications create a WebHost in an application's entry point, such as the `static void Main()` method in `Program.cs`.</span></span> <span data-ttu-id="4c601-128">이 경우 WebHost의 수명 주기는 프로세스의 수명 주기와 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-128">In this case, the lifecycle of the WebHost is bound to the lifecycle of the process.</span></span>

![프로세스에서 ASP.NET Core 호스팅][0]

<span data-ttu-id="4c601-130">그러나 응용 프로그램 진입점은 Reliable Service에서 WebHost를 만들 수 있는 적절한 위치가 아닙니다. 이는 응용 프로그램 진입점이 서비스 유형을 Service Fabric 런타임에 등록하는 데에만 사용되어 해당 서비스 유형의 인스턴스를 만들 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-130">However, the application entry point is not the right place to create a WebHost in a Reliable Service, because the application entry point is only used to register a service type with the Service Fabric runtime, so that it may create instances of that service type.</span></span> <span data-ttu-id="4c601-131">WebHost는 Reliable Service 자체에서 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-131">The WebHost should be created in a Reliable Service itself.</span></span> <span data-ttu-id="4c601-132">서비스 호스트 프로세스 내에서 서비스 인스턴스 및/또는 복제본은 여러 수명 주기를 거칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-132">Within the service host process, service instances and/or replicas can go through multiple lifecycles.</span></span> 

<span data-ttu-id="4c601-133">Reliable Service 인스턴스는 `StatelessService` 또는 `StatefulService`에서 파생되는 서비스 클래스로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-133">A Reliable Service instance is represented by your service class deriving from `StatelessService` or `StatefulService`.</span></span> <span data-ttu-id="4c601-134">서비스를 위한 통신 스택은 서비스 클래스의 `ICommunicationListener` 구현에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-134">The communication stack for a service is contained in an `ICommunicationListener` implementation in your service class.</span></span> <span data-ttu-id="4c601-135">`Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet 패키지에는 Reliable Service의 Kestrel 또는 WebListener에 대한 ASP.NET Core WebHost를 시작하고 관리하는 `ICommunicationListener` 구현이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-135">The `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages contain implementations of `ICommunicationListener` that start and manage the ASP.NET Core WebHost for either Kestrel or WebListener in a Reliable Service.</span></span>

![Reliable Service에서 ASP.NET Core 호스팅][1]

## <a name="aspnet-core-icommunicationlisteners"></a><span data-ttu-id="4c601-137">ASP.NET Core ICommunicationListeners</span><span class="sxs-lookup"><span data-stu-id="4c601-137">ASP.NET Core ICommunicationListeners</span></span>
<span data-ttu-id="4c601-138">`Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet 패키지의 Kestrel 및 WebListener에 대한 `ICommunicationListener` 구현은 비슷한 사용 패턴을 갖지만 각 웹 서버에 따라 약간 다른 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-138">The `ICommunicationListener` implementations for Kestrel and WebListener in the  `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages have similar use patterns but perform slightly different actions specific to each web server.</span></span> 

<span data-ttu-id="4c601-139">두 통신 수신기는 다음 인수를 사용하는 생성자를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-139">Both communication listeners provide a constructor that takes the following arguments:</span></span>
 - <span data-ttu-id="4c601-140">**`ServiceContext serviceContext`**: 실행 중인 서비스에 대한 정보가 포함된 `ServiceContext` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-140">**`ServiceContext serviceContext`**: The `ServiceContext` object that contains information about the running service.</span></span>
 - <span data-ttu-id="4c601-141">**`string endpointName`**: ServiceManifest.xml의 `Endpoint` 구성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-141">**`string endpointName`**: the name of an `Endpoint` configuration in ServiceManifest.xml.</span></span> <span data-ttu-id="4c601-142">이는 주로 두 통신 수신기가 다른 부분입니다. 즉 WebListener에는 `Endpoint` 구성이 **필요하지만**, Kestrel에는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-142">This is primarily where the two communication listeners differ: WebListener **requires** an `Endpoint` configuration, while Kestrel does not.</span></span>
 - <span data-ttu-id="4c601-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: `IWebHost`를 만들고 반환하는 사용자 구현 람다입니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: a lambda that you implement in which you create and return an `IWebHost`.</span></span> <span data-ttu-id="4c601-144">이렇게 하면 일반적으로 ASP.NET Core 응용 프로그램에서 구성하는 방식으로 `IWebHost`를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-144">This allows you to configure `IWebHost` the way you normally would in an ASP.NET Core application.</span></span> <span data-ttu-id="4c601-145">람다는 사용하는 Service Fabric 통합 옵션과 제공하는 `Endpoint` 구성에 따라 생성된 URL을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-145">The lambda provides a URL which is generated for you depending on the Service Fabric integration options you use and the `Endpoint` configuration you provide.</span></span> <span data-ttu-id="4c601-146">그런 다음 해당 URL을 수정하거나 그대로 사용하여 웹 서버를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-146">That URL can then be modified or used as-is to start the web server.</span></span>

## <a name="service-fabric-integration-middleware"></a><span data-ttu-id="4c601-147">Service Fabric 통합 미들웨어</span><span class="sxs-lookup"><span data-stu-id="4c601-147">Service Fabric integration middleware</span></span>
<span data-ttu-id="4c601-148">`Microsoft.ServiceFabric.Services.AspNetCore` NuGet 패키지에는 Service Fabric 인식 미들웨어를 추가하는 `IWebHostBuilder`의 `UseServiceFabricIntegration` 확장 메서드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-148">The `Microsoft.ServiceFabric.Services.AspNetCore` NuGet package includes the `UseServiceFabricIntegration` extension method on `IWebHostBuilder` that adds Service Fabric-aware middleware.</span></span> <span data-ttu-id="4c601-149">이 미들웨어는 Kestrel 또는 WebListener `ICommunicationListener`을(를) 구성하여 Service Fabric 명명 서비스에 고유한 서비스 URL을 등록한 다음, 클라이언트 요청의 유효성을 검사하여 클라이언트에서 적절한 서비스에 연결하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-149">This middleware configures the Kestrel or WebListener `ICommunicationListener` to register a unique service URL with the Service Fabric Naming Service and then validates client requests to ensure clients are connecting to the right service.</span></span> <span data-ttu-id="4c601-150">이는 Service Fabric과 같은 공유 호스트 환경에서 필요합니다. 여기서는 여러 웹 응용 프로그램이 동일한 물리적 컴퓨터 또는 가상 컴퓨터에서 실행될 수 있지만, 클라이언트에서 실수로 잘못된 서비스에 연결하지 못하도록 고유한 호스트 이름을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-150">This is necessary in a shared-host environment such as Service Fabric, where multiple web applications can run on the same physical or virtual machine but do not use unique host names, to prevent clients from mistakenly connecting to the wrong service.</span></span> <span data-ttu-id="4c601-151">이 시나리오에 대해서는 다음 섹션에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-151">This scenario is described in more detail in the next section.</span></span>

### <a name="a-case-of-mistaken-identity"></a><span data-ttu-id="4c601-152">잘못된 ID의 경우</span><span class="sxs-lookup"><span data-stu-id="4c601-152">A case of mistaken identity</span></span>
<span data-ttu-id="4c601-153">프로토콜에 관계없이 서비스 복제본은 고유한 IP:포트 조합에서 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-153">Service replicas, regardless of protocol, listen on a unique IP:port combination.</span></span> <span data-ttu-id="4c601-154">서비스 복제본이 IP:포트 끝점에서 수신 대기를 시작하면 클라이언트 또는 기타 서비스에서 검색할 수 있는 Service Fabric 명명 서비스에 해당 끝점 주소를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-154">Once a service replica has started listening on an IP:port endpoint, it reports that endpoint address to the Service Fabric Naming Service where it can be discovered by clients or other services.</span></span> <span data-ttu-id="4c601-155">서비스에서 동적으로 할당된 응용 프로그램 포트를 사용하는 경우 서비스 복제본은 이전에 동일한 물리적 컴퓨터 또는 가상 컴퓨터에 있었던 다른 서비스의 동일한 IP:포트 끝점을 우연히 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-155">If services use dynamically-assigned application ports, a service replica may coincidentally use the same IP:port endpoint of another service that was previously on the same physical or virtual machine.</span></span> <span data-ttu-id="4c601-156">이로 인해 클라이언트에서 실수로 잘못된 서비스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-156">This can cause a client to mistakely connect to the wrong service.</span></span> <span data-ttu-id="4c601-157">다음과 같은 일련의 이벤트가 발생하면 이러한 경우가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-157">This can happen if the following sequence of events occur:</span></span>

 1. <span data-ttu-id="4c601-158">서비스 A가 HTTP를 통해 10.0.0.1:30000에서 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-158">Service A listens on 10.0.0.1:30000 over HTTP.</span></span> 
 2. <span data-ttu-id="4c601-159">클라이언트가 서비스 A를 확인하고 10.0.0.1:30000 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-159">Client resolves Service A and gets address 10.0.0.1:30000</span></span>
 3. <span data-ttu-id="4c601-160">서비스 A가 다른 노드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-160">Service A moves to a different node.</span></span>
 4. <span data-ttu-id="4c601-161">서비스 B가 10.0.0.1에 위치하고 우연히 동일한 30000 포트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-161">Service B is placed on 10.0.0.1 and coincidentally uses the same port 30000.</span></span>
 5. <span data-ttu-id="4c601-162">클라이언트가 캐시된 10.0.0.1:30000 주소로 서비스 A에 연결하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-162">Client attempts to connect to service A with cached address 10.0.0.1:30000.</span></span>
 6. <span data-ttu-id="4c601-163">이제 클라이언트가 서비스 B에 성공적으로 연결되어 잘못된 서비스에 연결되었다는 것을 인식하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-163">Client is now successfully connected to service B not realizing it is connected to the wrong service.</span></span>

<span data-ttu-id="4c601-164">이로 인해 진단할 수 없는 버그가 임의의 시간에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-164">This can cause bugs at random times that can be difficult to diagnose.</span></span> 

### <a name="using-unique-service-urls"></a><span data-ttu-id="4c601-165">고유한 서비스 URL 사용</span><span class="sxs-lookup"><span data-stu-id="4c601-165">Using unique service URLs</span></span>
<span data-ttu-id="4c601-166">이를 방지하기 위해 서비스에서 고유 식별자로 끝점을 명명 서비스에 게시한 다음, 클라이언트 요청 중에 해당 고유 식별자의 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-166">To prevent this, services can post an endpoint to the Naming Service with a unique identifier, and then validate that unique identifier during client requests.</span></span> <span data-ttu-id="4c601-167">이 작업은 적대적이지 않은 테넌트가 신뢰할 수 있는 환경에서 서비스 간의 공동 작업이며,</span><span class="sxs-lookup"><span data-stu-id="4c601-167">This is a cooperative action between services in a non-hostile-tenant trusted environment.</span></span> <span data-ttu-id="4c601-168">적대적인 테넌트 환경에서는 보안 서비스 인증을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-168">This does not provide secure service authentication in a hostile-tenant environment.</span></span>

<span data-ttu-id="4c601-169">신뢰할 수 있는 환경에서 `UseServiceFabricIntegration` 메서드로 추가된 미들웨어는 명명 서비스에 게시된 주소에 고유 식별자를 자동으로 추가하고 각 요청에서 해당 식별자의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-169">In a trusted environment, the middleware that's added by the `UseServiceFabricIntegration` method automatically appends a unique identifier to the address that is posted to the Naming Service and validates that identifier on each request.</span></span> <span data-ttu-id="4c601-170">식별자가 일치하지 않으면 미들웨어에서 즉시 HTTP 410 없음 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-170">If the identifier does not match, the middleware immediately returns an HTTP 410 Gone response.</span></span>

<span data-ttu-id="4c601-171">동적으로 할당된 포트를 사용하는 서비스는 이 미들웨어를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-171">Services that use a dynamically-assigned port should make use of this middleware.</span></span>

<span data-ttu-id="4c601-172">고유한 고정 포트를 사용하는 서비스는 공동 작업 환경에서 이 문제를 가지고 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-172">Services that use a fixed unique port do not have this problem in a cooperative environment.</span></span> <span data-ttu-id="4c601-173">고유한 고정 포트는 일반적으로 클라이언트 응용 프로그램이 연결될 잘 알려진 포트가 필요한 외부 연결 서비스에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-173">A fixed unique port is typically used for externally-facing services that need a well-known port for client applications to connect to.</span></span> <span data-ttu-id="4c601-174">예를 들어 대부분의 인터넷 연결 웹 응용 프로그램은 웹 브라우저 연결에 80 또는 443 포트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-174">For example, most Internet-facing web applications will use port 80 or 443 for web browser connections.</span></span> <span data-ttu-id="4c601-175">이 경우에는 고유 식별자를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-175">In this case, the unique identifier should not be enabled.</span></span>

<span data-ttu-id="4c601-176">다음 다이어그램에서는 미들웨어를 사용하도록 설정된 요청 흐름을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-176">The following diagram shows the request flow with the middleware enabled:</span></span>

![Service Fabric ASP.NET Core 통합][2]

<span data-ttu-id="4c601-178">Kestrel과 WebListener `ICommunicationListener` 구현은 모두 똑같은 방식으로 이 메커니즘을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-178">Both Kestrel and WebListener `ICommunicationListener` implementations use this mechanism in exactly the same way.</span></span> <span data-ttu-id="4c601-179">WebListener는 기본 *http.sys* 포트 공유 기능을 사용하여 고유한 URL 경로에 따라 요청을 내부적으로 구분할 수 있지만, 이 기능은 앞에서 설명한 시나리오에서 HTTP 503 및 HTTP 404 오류 상태 코드가 발생하기 때문에 WebListener `ICommunicationListener` 구현에서 *사용되지 않습니다*.</span><span class="sxs-lookup"><span data-stu-id="4c601-179">Although WebListener can internally differentiate requests based on unique URL paths using the underlying *http.sys* port sharing feature, that functionality is *not* used by the WebListener `ICommunicationListener` implementation because that will result in HTTP 503 and HTTP 404 error status codes in the scenario described earlier.</span></span> <span data-ttu-id="4c601-180">HTTP 503 및 HTTP 404는 일반적으로 이미 다른 오류를 나타내는 데 사용되므로 클라이언트에서 오류의 의미를 확인하는 것이 매우 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-180">That in turn makes it very difficult for clients to determine the intent of the error, as HTTP 503 and HTTP 404 are already commonly used to indicate other errors.</span></span> <span data-ttu-id="4c601-181">따라서 Kestrel과 WebListener `ICommunicationListener` 구현은 모두 `UseServiceFabricIntegration` 확장 메서드로 제공되는 미들웨어에서 표준화되므로 클라이언트는 HTTP 410 응답에서 서비스 끝점 재확인 작업만 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-181">Thus, both Kestrel and WebListener `ICommunicationListener` implementations standardize on the middleware provided by the `UseServiceFabricIntegration` extension method so that clients only need to perform a service endpoint re-resolve action on HTTP 410 responses.</span></span>

## <a name="weblistener-in-reliable-services"></a><span data-ttu-id="4c601-182">Reliable Services의 WebListener</span><span class="sxs-lookup"><span data-stu-id="4c601-182">WebListener in Reliable Services</span></span>
<span data-ttu-id="4c601-183">WebListener는 **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet 패키지를 가져와서 신뢰할 수 있는 서비스에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-183">WebListener can be used in a Reliable Service by importing the **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet package.</span></span> <span data-ttu-id="4c601-184">이 패키지에는 `ICommunicationListener` 구현인 `WebListenerCommunicationListener`가 포함되어 있으므로 웹 서버로 WebListener를 사용하여 신뢰할 수 있는 서비스 내에 ASP.NET Core WebHost를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-184">This package contains `WebListenerCommunicationListener`, an implementation of `ICommunicationListener`, that allows you to create an ASP.NET Core WebHost inside a Reliable Service using WebListener as the web server.</span></span>

<span data-ttu-id="4c601-185">WebListener는 [Windows HTTP 서버 API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx)(영문)를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-185">WebListener is built on the [Windows HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span></span> <span data-ttu-id="4c601-186">IIS에서 사용하는 *http.sys* 커널 드라이버를 사용하여 HTTP 요청을 처리하고 이를 웹 응용 프로그램을 실행하는 프로세스로 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-186">This uses the *http.sys* kernel driver used by IIS to process HTTP requests and route them to processes running web applications.</span></span> <span data-ttu-id="4c601-187">이렇게 하면 동일한 물리적 컴퓨터 또는 가상 컴퓨터의 여러 프로세스가 동일한 포트에서 고유한 URL 경로 또는 호스트 이름으로 구분되는 웹 응용 프로그램을 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-187">This allows multiple processes on the same physical or virtual machine to host web applications on the same port, disambiguated by either a unique URL path or hostname.</span></span> <span data-ttu-id="4c601-188">이러한 기능은 동일한 클러스터에서 여러 웹 사이트를 호스팅하는 Service Fabric에서 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-188">These features are useful in Service Fabric for hosting multiple websites in the same cluster.</span></span>

<span data-ttu-id="4c601-189">다음 다이어그램에서는 WebListener가 포트 공유를 위해 Windows에서 *http.sys* 커널 드라이버를 사용하는 방식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-189">The following diagram illustrates how WebListener uses the *http.sys* kernel driver on Windows for port sharing:</span></span>

![http.sys][3]

### <a name="weblistener-in-a-stateless-service"></a><span data-ttu-id="4c601-191">상태 비저장 서비스의 WebListener</span><span class="sxs-lookup"><span data-stu-id="4c601-191">WebListener in a stateless service</span></span>
<span data-ttu-id="4c601-192">상태 비저장 서비스에서 `WebListener`를 사용하려면 `CreateServiceInstanceListeners` 메서드를 재정의하고 `WebListenerCommunicationListener` 인스턴스를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-192">To use `WebListener` in a stateless service, override the `CreateServiceInstanceListeners` method and return a `WebListenerCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseWebListener()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build()))
    };
}
```

### <a name="weblistener-in-a-stateful-service"></a><span data-ttu-id="4c601-193">상태 저장 서비스의 WebListener</span><span class="sxs-lookup"><span data-stu-id="4c601-193">WebListener in a stateful service</span></span>

<span data-ttu-id="4c601-194">현재 `WebListenerCommunicationListener`는 기본 *http.sys* 포트 공유 기능에 따른 복잡성 때문에 상태 저장 서비스에서 사용하도록 설계되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-194">`WebListenerCommunicationListener` is currently not designed for use in stateful services due to complications with the underlying *http.sys* port sharing feature.</span></span> <span data-ttu-id="4c601-195">자세한 내용은 WebListener를 통한 동적 포트 할당에 대한 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4c601-195">For more information, see the following section on dynamic port allocation with WebListener.</span></span> <span data-ttu-id="4c601-196">상태 저장 서비스의 경우 Kestrel이 권장되는 웹 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-196">For stateful services, Kestrel is the recommended web server.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="4c601-197">끝점 구성</span><span class="sxs-lookup"><span data-stu-id="4c601-197">Endpoint configuration</span></span>

<span data-ttu-id="4c601-198">WebListener를 포함하여 Windows HTTP 서버 API를 사용하는 웹 서버에는 `Endpoint` 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-198">An `Endpoint` configuration is required for web servers that use the Windows HTTP Server API, including WebListener.</span></span> <span data-ttu-id="4c601-199">Windows HTTP 서버 API를 사용하는 웹 서버는 먼저 *http.sys*로 URL을 예약해야 합니다(일반적으로 [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) 도구로 수행).</span><span class="sxs-lookup"><span data-stu-id="4c601-199">Web servers that use the Windows HTTP Server API must first reserve their URL with *http.sys* (this is normally accomplished with the [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) tool).</span></span> <span data-ttu-id="4c601-200">이 작업을 수행하려면 기본적으로 서비스에 없는 상승된 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-200">This action requires elevated privileges that your services by default do not have.</span></span> <span data-ttu-id="4c601-201">*ServiceManifest.xml*에 있는 `Endpoint` 구성의 `Protocol` 속성에 대한 "http" 또는 "https" 옵션은 특히 Service Fabric 런타임에서 [*강력한 와일드카드*](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL 접두사를 사용하는 대신 URL을 *http.sys*에 등록하도록 지시하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-201">The "http" or "https" options for the `Protocol` property of the `Endpoint` configuration in *ServiceManifest.xml* are used specifically to instruct the Service Fabric runtime to register a URL with *http.sys* on your behalf using the [*strong wildcard*](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL prefix.</span></span>

<span data-ttu-id="4c601-202">예를 들어 서비스에 대해 `http://+:80`을 예약하려면 ServiceManifest.xml에서 다음 구성을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-202">For example, to reserve `http://+:80` for a service, the following configuration should be used in ServiceManifest.xml:</span></span>

```xml
<ServiceManifest ... >
    ...
    <Resources>
        <Endpoints>
            <Endpoint Name="ServiceEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>

</ServiceManifest>
```

<span data-ttu-id="4c601-203">그리고 끝점 이름은 `WebListenerCommunicationListener` 생성자에 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-203">And the endpoint name must be passed to the `WebListenerCommunicationListener` constructor:</span></span>

```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     return new WebHostBuilder()
         .UseWebListener()
         .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
         .UseUrls(url)
         .Build();
 })
```

#### <a name="use-weblistener-with-a-static-port"></a><span data-ttu-id="4c601-204">정적 포트로 WebListener 사용</span><span class="sxs-lookup"><span data-stu-id="4c601-204">Use WebListener with a static port</span></span>
<span data-ttu-id="4c601-205">WebListener에서 정적 포트를 사용하려면 `Endpoint` 구성에 포트 번호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-205">To use a static port with WebListener, provide the port number in the `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-weblistener-with-a-dynamic-port"></a><span data-ttu-id="4c601-206">동적 포트로 WebListener 사용</span><span class="sxs-lookup"><span data-stu-id="4c601-206">Use WebListener with a dynamic port</span></span>
<span data-ttu-id="4c601-207">WebListener에서 동적으로 할당된 포트를 사용하려면 `Endpoint` 구성에서 `Port` 속성을 생략합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-207">To use a dynamically assigned port with WebListener, omit the `Port` property in the `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="4c601-208">`Endpoint` 구성으로 할당된 동적 포트는 *호스트 프로세스당* 하나의 포트만 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-208">Note that a dynamic port allocated by an `Endpoint` configuration only provides one port *per host process*.</span></span> <span data-ttu-id="4c601-209">현재 Service Fabric 호스팅 모델을 사용하면 동일한 프로세스에서 여러 서비스 인스턴스 및/또는 복제본을 호스팅할 수 있습니다. 즉, 각각 `Endpoint` 구성을 통해 할당될 때 동일한 포트를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-209">The current Service Fabric hosting model allows multiple service instances and/or replicas to be hosted in the same process, meaning that each one will share the same port when allocated through the `Endpoint` configuration.</span></span> <span data-ttu-id="4c601-210">여러 WebListener 인스턴스는 기본 *http.sys* 포트 공유 기능을 사용하여 포트를 공유할 수 있지만, 클라이언트 요청에 대해 발생하는 복잡성으로 인해 `WebListenerCommunicationListener`에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-210">Multiple WebListener instances can share a port using the underlying *http.sys* port sharing feature, but that is not supported by `WebListenerCommunicationListener` due to the complications it introduces for client requests.</span></span> <span data-ttu-id="4c601-211">동적 포트를 사용하는 경우 Kestrel이 권장되는 웹 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-211">For dynamic port usage, Kestrel is the recommended web server.</span></span>

## <a name="kestrel-in-reliable-services"></a><span data-ttu-id="4c601-212">Reliable Services의 Kestrel</span><span class="sxs-lookup"><span data-stu-id="4c601-212">Kestrel in Reliable Services</span></span>
<span data-ttu-id="4c601-213">Kestrel은 **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet 패키지를 가져와서 신뢰할 수 있는 서비스에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-213">Kestrel can be used in a Reliable Service by importing the **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet package.</span></span> <span data-ttu-id="4c601-214">이 패키지에는 `ICommunicationListener` 구현인 `KestrelCommunicationListener`가 포함되어 있으므로 웹 서버로 Kestrel을 사용하여 신뢰할 수 있는 서비스 내에 ASP.NET Core WebHost를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-214">This package contains `KestrelCommunicationListener`, an implementation of `ICommunicationListener`, that allows you to create an ASP.NET Core WebHost inside a Reliable Service using Kestrel as the web server.</span></span>

<span data-ttu-id="4c601-215">Kestrel은 libuv(플랫폼 간 비동기 I/O 라이브러리)를 기반으로 하는 ASP.NET Core용 플랫폼 간 웹 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-215">Kestrel is a cross-platform web server for ASP.NET Core based on libuv, a cross-platform asynchronous I/O library.</span></span> <span data-ttu-id="4c601-216">WebListener와 달리 Kestrel은 *http.sys*와 같은 중앙 집중식 끝점 관리자를 사용하지 않으며,</span><span class="sxs-lookup"><span data-stu-id="4c601-216">Unlike WebListener, Kestrel does not use a centralized endpoint manager such as *http.sys*.</span></span> <span data-ttu-id="4c601-217">여러 프로세스 간의 포트 공유도 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-217">And unlike WebListener, Kestrel does not support port sharing between multiple processes.</span></span> <span data-ttu-id="4c601-218">Kestrel의 각 인스턴스는 고유한 포트를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-218">Each instance of Kestrel must use a unique port.</span></span>

![Kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a><span data-ttu-id="4c601-220">상태 비저장 서비스의 Kestrel</span><span class="sxs-lookup"><span data-stu-id="4c601-220">Kestrel in a stateless service</span></span>
<span data-ttu-id="4c601-221">상태 비저장 서비스에서 `Kestrel`을 사용하려면 `CreateServiceInstanceListeners` 메서드를 재정의하고 `KestrelCommunicationListener` 인스턴스를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-221">To use `Kestrel` in a stateless service, override the `CreateServiceInstanceListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

### <a name="kestrel-in-a-stateful-service"></a><span data-ttu-id="4c601-222">상태 저장 서비스의 Kestrel</span><span class="sxs-lookup"><span data-stu-id="4c601-222">Kestrel in a stateful service</span></span>
<span data-ttu-id="4c601-223">상태 저장 서비스에서 `Kestrel`을 사용하려면 `CreateServiceReplicaListeners` 메서드를 재정의하고 `KestrelCommunicationListener` 인스턴스를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-223">To use `Kestrel` in a stateful service, override the `CreateServiceReplicaListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new ServiceReplicaListener[]
    {
        new ServiceReplicaListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                         services => services
                             .AddSingleton<StatefulServiceContext>(serviceContext)
                             .AddSingleton<IReliableStateManager>(this.StateManager))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

<span data-ttu-id="4c601-224">이 예제에서는 WebHost 종속성 삽입 컨테이너에 `IReliableStateManager`의 singleton 인스턴스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-224">In this example, a singleton instance of `IReliableStateManager` is provided to the WebHost dependency injection container.</span></span> <span data-ttu-id="4c601-225">이는 반드시 필요한 것이 아니지만 MVC 컨트롤러 작업 메서드에서 `IReliableStateManager` 및 신뢰할 수 있는 컬렉션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-225">This is not strictly necessary, but it allows you to use `IReliableStateManager` and Reliable Collections in your MVC controller action methods.</span></span>

<span data-ttu-id="4c601-226">상태 저장 서비스에서는 `Endpoint` 구성 이름이 `KestrelCommunicationListener`에 제공되지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="4c601-226">Note that an `Endpoint` configuration name is **not** provided to `KestrelCommunicationListener` in a stateful service.</span></span> <span data-ttu-id="4c601-227">자세한 내용은 다음 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-227">This is explained in more detail in the following section.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="4c601-228">끝점 구성</span><span class="sxs-lookup"><span data-stu-id="4c601-228">Endpoint configuration</span></span>
<span data-ttu-id="4c601-229">`Endpoint` 구성은 Kestrel을 사용하는 데 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-229">An `Endpoint` configuration is not required to use Kestrel.</span></span> 

<span data-ttu-id="4c601-230">Kestrel은 간단한 독립 실행형 웹 서버입니다. WebListener(또는 HttpListener)와는 달리 시작하기 전에 URL을 등록할 필요가 없기 때문에 *ServiceManifest.xml*에서 `Endpoint` 구성이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-230">Kestrel is a simple stand-alone web server; unlike WebListener (or HttpListener), it does not need an `Endpoint` configuration in *ServiceManifest.xml* because it does not require URL registration prior to starting.</span></span> 

#### <a name="use-kestrel-with-a-static-port"></a><span data-ttu-id="4c601-231">정적 포트로 Kestrel 사용</span><span class="sxs-lookup"><span data-stu-id="4c601-231">Use Kestrel with a static port</span></span>
<span data-ttu-id="4c601-232">Kestrel에서 정적 포트를 사용하려면 ServiceManifest.xml의 `Endpoint` 구성에 해당 포트를 구성하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-232">A static port can be configured in the `Endpoint` configuration of ServiceManifest.xml for use with Kestrel.</span></span> <span data-ttu-id="4c601-233">이는 반드시 필요한 것이 아니지만 잠재적인 두 가지 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-233">Although this is not strictly necessary, it provides two potential benefits:</span></span>
 1. <span data-ttu-id="4c601-234">포트가 응용 프로그램 포트 범위에 속하지 않으면 Service Fabric에서 OS 방화벽을 통해 해당 포트가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-234">If the port does not fall in the application port range, it is opened through the OS firewall by Service Fabric.</span></span>
 2. <span data-ttu-id="4c601-235">`KestrelCommunicationListener`를 통해 제공된 URL은 이 포트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-235">The URL provided to you through `KestrelCommunicationListener` will use this port.</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="4c601-236">`Endpoint`가 구성되면 해당 이름을 `KestrelCommunicationListener` 생성자로 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-236">If an `Endpoint` is configured, its name must be passed into the `KestrelCommunicationListener` constructor:</span></span> 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

<span data-ttu-id="4c601-237">`Endpoint` 구성을 사용하지 않으면 `KestrelCommunicationListener` 생성자에서 이름을 생략합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-237">If an `Endpoint` configuration is not used, omit the name in the `KestrelCommunicationListener` constructor.</span></span> <span data-ttu-id="4c601-238">이 경우 동적 포트가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-238">In this case, a dynamic port will be used.</span></span> <span data-ttu-id="4c601-239">자세한 내용은 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4c601-239">See the next section for more information.</span></span>

#### <a name="use-kestrel-with-a-dynamic-port"></a><span data-ttu-id="4c601-240">동적 포트로 Kestrel 사용</span><span class="sxs-lookup"><span data-stu-id="4c601-240">Use Kestrel with a dynamic port</span></span>
<span data-ttu-id="4c601-241">`Endpoint` 구성의 자동 포트 할당에서 *호스트 프로세스*당 고유한 포트를 하나씩 할당하고 단일 호스트 프로세스에 여러 Kestrel 인스턴스가 포함될 수 있기 때문에, Kestrel은 ServiceManifest.xml의 `Endpoint` 구성에서 자동 포트 할당을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-241">Kestrel cannot use the automatic port assignment from the `Endpoint` configuration in ServiceManifest.xml, because automatic port assignment from an `Endpoint` configuration assigns a unique port per *host process*, and a single host process can contain multiple Kestrel instances.</span></span> <span data-ttu-id="4c601-242">각 Kestrel 인스턴스를 고유한 포트에서 열어야 하지만 Kestrel에서 포트 공유를 지원하지 않기 때문에 이 기능은 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-242">Since Kestrel does not support port sharing, this does not work as each Kestrel instance must be opened on a unique port.</span></span>

<span data-ttu-id="4c601-243">Kestrel에서 동적 포트 할당을 사용하려면 ServiceManifest.xml에서 `Endpoint` 구성을 완전히 생략하고 `KestrelCommunicationListener` 생성자에 끝점 이름을 전달하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-243">To use dynamic port assignment with Kestrel, simply omit the `Endpoint` configuration in ServiceManifest.xml entirely, and do not pass an endpoint name to the `KestrelCommunicationListener` constructor:</span></span>

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

<span data-ttu-id="4c601-244">이 구성에서 `KestrelCommunicationListener`는 응용 프로그램 포트 범위에서 사용되지 않는 포트를 자동으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-244">In this configuration, `KestrelCommunicationListener` will automatically select an unused port from the application port range.</span></span>

## <a name="scenarios-and-configurations"></a><span data-ttu-id="4c601-245">시나리오 및 구성</span><span class="sxs-lookup"><span data-stu-id="4c601-245">Scenarios and configurations</span></span>
<span data-ttu-id="4c601-246">이 섹션에서는 다음 시나리오에 대해 설명하고, 웹 서버, 포트 구성, Service Fabric 통합 옵션 및 기타 설정에 권장되는 조합을 제공하여 적절하게 작동하는 서비스를 달성합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-246">This section describes the following scenarios and provides the recommended combination of web server, port configuration, Service Fabric integration options, and miscellaneous settings to achieve a properly functioning service:</span></span>
 - <span data-ttu-id="4c601-247">외부에 노출된 ASP.NET Core 상태 비저장 서비스</span><span class="sxs-lookup"><span data-stu-id="4c601-247">Externally exposed ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="4c601-248">내부 전용 ASP.NET Core 상태 비저장 서비스</span><span class="sxs-lookup"><span data-stu-id="4c601-248">Internal-only ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="4c601-249">내부 전용 ASP.NET Core 상태 저장 서비스</span><span class="sxs-lookup"><span data-stu-id="4c601-249">Internal-only ASP.NET Core stateful service</span></span>

<span data-ttu-id="4c601-250">**외부에 노출된** 서비스는 일반적으로 부하 분산 장치를 통해 클러스터 외부에서 연결할 수 있는 끝점을 제공하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-250">An **externally exposed** service is one that exposes an endpoint reachable from outside the cluster, usually through a load balancer.</span></span>

<span data-ttu-id="4c601-251">**내부 전용** 서비스는 끝점이 클러스터 내에서만 연결할 수 있는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-251">An **internal-only** service is one whose endpoint is only reachable from within the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="4c601-252">상태 저장 서비스 끝점은 일반적으로 인터넷에 노출되어서는 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-252">Stateful service endpoints generally should not be exposed to the Internet.</span></span> <span data-ttu-id="4c601-253">부하 분산 장치에서 트래픽을 찾아 적절한 상태 저장 서비스 복제본으로 라우팅할 수 없기 때문에 Azure Load Balancer와 같이 Service Fabric 서비스 확인을 인식하지 못하는 부하 분산 장치 뒤에 있는 클러스터는 상태 저장 서비스를 노출할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-253">Clusters that are behind load balancers that are unaware of Service Fabric service resolution, such as the Azure Load Balancer, will be unable to expose stateful services because the load balancer will not be able to locate and route traffic to the appropriate stateful service replica.</span></span> 

### <a name="externally-exposed-aspnet-core-stateless-services"></a><span data-ttu-id="4c601-254">외부에 노출된 ASP.NET Core 상태 비저장 서비스</span><span class="sxs-lookup"><span data-stu-id="4c601-254">Externally exposed ASP.NET Core stateless services</span></span>
<span data-ttu-id="4c601-255">WebListener는 Windows에서 외부 인터넷 연결 HTTP 끝점을 노출하는 프런트 엔드 서비스에 권장되는 웹 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-255">WebListener is the recommended web server for front-end services that expose external, Internet-facing HTTP endpoints on Windows.</span></span> <span data-ttu-id="4c601-256">공격에 대한 더 나은 보호를 제공하고, Windows 인증 및 포트 공유와 같이 Kestrel에서 지원하지 않는 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-256">It provides better protection against attacks and supports features that Kestrel does not, such as Windows Authentication and port sharing.</span></span> 

<span data-ttu-id="4c601-257">현재 Kestrel은 에지(인터넷 연결) 서버로 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-257">Kestrel is not supported as an edge (Internet-facing) server at this time.</span></span> <span data-ttu-id="4c601-258">공용 인터넷에서 트래픽을 처리하려면 IIS 또는 Nginx와 같은 역방향 프록시 서버를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-258">A reverse proxy server such as IIS or Nginx must be used to handle traffic from the public Internet.</span></span>
 
<span data-ttu-id="4c601-259">인터넷에 노출되면 상태 비저장 서비스에서 부하 분산 장치를 통해 연결할 수 있는 잘 알려진 안정적인 끝점을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-259">When exposed to the Internet, a stateless service should use a well-known and stable endpoint that is reachable through a load balancer.</span></span> <span data-ttu-id="4c601-260">이 끝점은 응용 프로그램 사용자에게 제공할 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-260">This is the URL you will provide to users of your application.</span></span> <span data-ttu-id="4c601-261">권장되는 구성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-261">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="4c601-262">**참고 사항**</span><span class="sxs-lookup"><span data-stu-id="4c601-262">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4c601-263">웹 서버</span><span class="sxs-lookup"><span data-stu-id="4c601-263">Web server</span></span> | <span data-ttu-id="4c601-264">WebListener</span><span class="sxs-lookup"><span data-stu-id="4c601-264">WebListener</span></span> | <span data-ttu-id="4c601-265">서비스가 인트라넷과 같은 신뢰할 수 있는 네트워크에만 노출되는 경우 Kestrel을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-265">If the service is only exposed to a trusted network, such an intranet, Kestrel may be used.</span></span> <span data-ttu-id="4c601-266">그렇지 않으면 WebListener가 기본 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-266">Otherwise, WebListener is the preferred option.</span></span> |
| <span data-ttu-id="4c601-267">포트 구성</span><span class="sxs-lookup"><span data-stu-id="4c601-267">Port configuration</span></span> | <span data-ttu-id="4c601-268">정적</span><span class="sxs-lookup"><span data-stu-id="4c601-268">static</span></span> | <span data-ttu-id="4c601-269">잘 알려진 정적 포트는 ServiceManifest.xml의 `Endpoints` 구성에 구성해야 합니다(예: HTTP의 경우 80, HTTPS의 경우 443).</span><span class="sxs-lookup"><span data-stu-id="4c601-269">A well-known static port should be configured in the `Endpoints` configuration of ServiceManifest.xml, such as 80 for HTTP or 443 for HTTPS.</span></span> |
| <span data-ttu-id="4c601-270">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="4c601-270">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="4c601-271">없음</span><span class="sxs-lookup"><span data-stu-id="4c601-271">None</span></span> | <span data-ttu-id="4c601-272">서비스에서 들어오는 고유 식별자 요청의 유효성을 검사하지 않도록 Service Fabric 통합 미들웨어를 구성할 때 `ServiceFabricIntegrationOptions.None` 옵션을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-272">The `ServiceFabricIntegrationOptions.None` option should be used when configuring Service Fabric integration middleware so that the service does not attempt to validate incoming requests for a unique identifier.</span></span> <span data-ttu-id="4c601-273">응용 프로그램의 외부 사용자는 미들웨어에서 사용되는 고유한 식별 정보를 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-273">External users of your application will not know the unique identifying information used by the middleware.</span></span> |
| <span data-ttu-id="4c601-274">인스턴스 수</span><span class="sxs-lookup"><span data-stu-id="4c601-274">Instance Count</span></span> | <span data-ttu-id="4c601-275">-1</span><span class="sxs-lookup"><span data-stu-id="4c601-275">-1</span></span> | <span data-ttu-id="4c601-276">일반적인 사용 사례에서는 인스턴스 수 설정을 "-1"로 설정하여 부하 분산 장치에서 트래픽을 수신하는 모든 노드에서 인스턴스를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-276">In typical use cases, the instance count setting should be set to "-1" so that an instance is available on all nodes that receive traffic from a load balancer.</span></span> |

<span data-ttu-id="4c601-277">외부에 노출된 여러 서비스에서 동일한 노드 집합을 공유하는 경우 고유하지만 안정된 URL 경로를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-277">If multiple externally exposed services share the same set of nodes, a unique but stable URL path should be used.</span></span> <span data-ttu-id="4c601-278">이는 IWebHost를 구성할 때 제공된 URL을 수정하여 수행할 수 있으며,</span><span class="sxs-lookup"><span data-stu-id="4c601-278">This can be accomplished by modifying the URL provided when configuring IWebHost.</span></span> <span data-ttu-id="4c601-279">WebListener에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-279">Note this applies to WebListener only.</span></span>

 ```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     url += "/MyUniqueServicePath";
 
     return new WebHostBuilder()
         .UseWebListener()
         ...
         .UseUrls(url)
         .Build();
 })
 ```

### <a name="internal-only-stateless-aspnet-core-service"></a><span data-ttu-id="4c601-280">내부 전용 ASP.NET Core 상태 비저장 서비스</span><span class="sxs-lookup"><span data-stu-id="4c601-280">Internal-only stateless ASP.NET Core service</span></span>
<span data-ttu-id="4c601-281">클러스터 내에서만 호출되는 상태 비저장 서비스는 고유한 URL과 동적으로 할당된 포트를 사용하여 여러 서비스 간의 공동 작업을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-281">Stateless services that are only called from within the cluster should use unique URLs and dynamically assigned ports to ensure cooperation between multiple services.</span></span> <span data-ttu-id="4c601-282">권장되는 구성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-282">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="4c601-283">**참고 사항**</span><span class="sxs-lookup"><span data-stu-id="4c601-283">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4c601-284">웹 서버</span><span class="sxs-lookup"><span data-stu-id="4c601-284">Web server</span></span> | <span data-ttu-id="4c601-285">Kestrel</span><span class="sxs-lookup"><span data-stu-id="4c601-285">Kestrel</span></span> | <span data-ttu-id="4c601-286">WebListener는 내부 상태 비저장 서비스에 사용될 수 있지만, Kestrel은 여러 서비스 인스턴스에서 호스트를 공유할 수 있도록 권장되는 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-286">Although WebListener may be used for internal stateless services, Kestrel is the recommended server to allow multiple service instances to share a host.</span></span>  |
| <span data-ttu-id="4c601-287">포트 구성</span><span class="sxs-lookup"><span data-stu-id="4c601-287">Port configuration</span></span> | <span data-ttu-id="4c601-288">동적으로 할당</span><span class="sxs-lookup"><span data-stu-id="4c601-288">dynamically assigned</span></span> | <span data-ttu-id="4c601-289">상태 저장 서비스의 여러 복제본에서 호스트 프로세스 또는 호스트 운영 체제를 공유할 수 있으므로 고유한 포트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-289">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="4c601-290">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="4c601-290">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="4c601-291">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="4c601-291">UseUniqueServiceUrl</span></span> | <span data-ttu-id="4c601-292">동적 포트 할당으로 인해 이 설정은 앞에서 설명한 잘못된 ID 문제를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-292">With dynamic port assignment, this setting prevents the mistaken identity issue described earlier.</span></span> |
| <span data-ttu-id="4c601-293">InstanceCount</span><span class="sxs-lookup"><span data-stu-id="4c601-293">InstanceCount</span></span> | <span data-ttu-id="4c601-294">모든</span><span class="sxs-lookup"><span data-stu-id="4c601-294">any</span></span> | <span data-ttu-id="4c601-295">인스턴스 수 설정은 서비스를 작동하는 데 필요한 모든 값으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-295">The instance count setting can be set to any value necessary to operate the service.</span></span> |

### <a name="internal-only-stateful-aspnet-core-service"></a><span data-ttu-id="4c601-296">내부 전용 ASP.NET Core 상태 저장 서비스</span><span class="sxs-lookup"><span data-stu-id="4c601-296">Internal-only stateful ASP.NET Core service</span></span>
<span data-ttu-id="4c601-297">클러스터 내에서만 호출되는 상태 저장 서비스는 동적으로 할당된 포트를 사용하여 여러 서비스 간의 공동 작업을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-297">Stateful services that are only called from within the cluster should use dynamically assigned ports to ensure cooperation between multiple services.</span></span> <span data-ttu-id="4c601-298">권장되는 구성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-298">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="4c601-299">**참고 사항**</span><span class="sxs-lookup"><span data-stu-id="4c601-299">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4c601-300">웹 서버</span><span class="sxs-lookup"><span data-stu-id="4c601-300">Web server</span></span> | <span data-ttu-id="4c601-301">Kestrel</span><span class="sxs-lookup"><span data-stu-id="4c601-301">Kestrel</span></span> | <span data-ttu-id="4c601-302">`WebListenerCommunicationListener`는 복제본에서 호스트 프로세스를 공유하는 상태 저장 서비스에서 사용하도록 설계되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-302">The `WebListenerCommunicationListener` is not designed for use by stateful services in which replicas share a host process.</span></span> |
| <span data-ttu-id="4c601-303">포트 구성</span><span class="sxs-lookup"><span data-stu-id="4c601-303">Port configuration</span></span> | <span data-ttu-id="4c601-304">동적으로 할당</span><span class="sxs-lookup"><span data-stu-id="4c601-304">dynamically assigned</span></span> | <span data-ttu-id="4c601-305">상태 저장 서비스의 여러 복제본에서 호스트 프로세스 또는 호스트 운영 체제를 공유할 수 있으므로 고유한 포트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-305">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="4c601-306">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="4c601-306">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="4c601-307">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="4c601-307">UseUniqueServiceUrl</span></span> | <span data-ttu-id="4c601-308">동적 포트 할당으로 인해 이 설정은 앞에서 설명한 잘못된 ID 문제를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="4c601-308">With dynamic port assignment, this setting prevents the mistaken identity issue described earlier.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4c601-309">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4c601-309">Next steps</span></span>
[<span data-ttu-id="4c601-310">Visual Studio를 사용하여 서비스 패브릭 응용 프로그램 디버그</span><span class="sxs-lookup"><span data-stu-id="4c601-310">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:./media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:./media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:./media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png
