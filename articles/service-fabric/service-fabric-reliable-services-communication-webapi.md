---
title: "ASP.NET Web API hello와 aaaService 통신 | Microsoft Docs"
description: "사용 하 여 단계별 tooimplement 서비스 통신 ASP.NET Web API OWIN hello 신뢰할 수 있는 서비스 API에서에서 자체 호스트 된 hello 하는 방법에 대해 알아봅니다."
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
ms.date: 02/10/2017
ms.author: vturecek
redirect_url: /azure/service-fabric/service-fabric-reliable-services-communication-aspnetcore
ms.openlocfilehash: 3fb18fcb141ada0d79a0acda3dccbc7fb044346d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a><span data-ttu-id="f8de5-103">시작: OWIN 자체 호스팅을 사용하는 서비스 패브릭 Web API 서비스</span><span class="sxs-lookup"><span data-stu-id="f8de5-103">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>
<span data-ttu-id="f8de5-104">Azure 서비스 패브릭은 사용자와 및 다른 서비스 toocommunicate 원하는 결정할 때는 hello 전원을 손으로을 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-104">Azure Service Fabric puts hello power in your hands when you're deciding how you want your services toocommunicate with users and with each other.</span></span> <span data-ttu-id="f8de5-105">이 자습서에서는 서비스 패브릭의 Reliable Services API에서 자체 호스팅되는 OWIN(Open Web Interface for .NET)과 ASP.NET Web API를 사용하여 서비스 통신을 구현하는 방법을 중점적으로 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-105">This tutorial focuses on implementing service communication using ASP.NET Web API with Open Web Interface for .NET (OWIN) self-hosting in Service Fabric's Reliable Services API.</span></span> <span data-ttu-id="f8de5-106">Hello 신뢰할 수 있는 서비스 플러그형 통신 API에 밀접 하 게 자세히 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-106">We'll delve deeply into hello Reliable Services pluggable communication API.</span></span> <span data-ttu-id="f8de5-107">웹 API 단계별 예제 tooshow도 사용 해야 하면 방법을 사용자 지정 통신 수신기를 tooset 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-107">We'll also use Web API in a step-by-step example tooshow you how tooset up a custom communication listener.</span></span>

## <a name="introduction-tooweb-api-in-service-fabric"></a><span data-ttu-id="f8de5-108">서비스 패브릭에서 소개 tooWeb API</span><span class="sxs-lookup"><span data-stu-id="f8de5-108">Introduction tooWeb API in Service Fabric</span></span>
<span data-ttu-id="f8de5-109">ASP.NET Web API는 HTTP Api hello.NET Framework를 기반으로 구축 하기 위한 널리 사용 되 고 강력한 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="f8de5-109">ASP.NET Web API is a popular and powerful framework for building HTTP APIs on top of hello .NET Framework.</span></span> <span data-ttu-id="f8de5-110">아닌 경우 이미 hello 프레임 워크에 잘 알고, 참조 [ASP.NET Web API 2 시작](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-110">If you're not already familiar with hello framework, see [Getting started with ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn more.</span></span>

<span data-ttu-id="f8de5-111">Web API 서비스 패브릭에서 동일한 ASP.NET Web API 알고 있고 즐겨 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-111">Web API in Service Fabric is hello same ASP.NET Web API you know and love.</span></span> <span data-ttu-id="f8de5-112">hello 차이점은 방법 있습니다 *호스트* Web API 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-112">hello difference is in how you *host* a Web API application.</span></span> <span data-ttu-id="f8de5-113">Microsoft IIS(인터넷 정보 서비스)를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-113">You won't be using Microsoft Internet Information Services (IIS).</span></span> <span data-ttu-id="f8de5-114">toobetter는 hello 차이 이해, 두 부분으로 분리 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-114">toobetter understand hello difference, let's break it into two parts:</span></span>

1. <span data-ttu-id="f8de5-115">hello Web API 응용 프로그램 (컨트롤러, 모델 등)</span><span class="sxs-lookup"><span data-stu-id="f8de5-115">hello Web API application (including controllers and models)</span></span>
2. <span data-ttu-id="f8de5-116">hello 호스트 (hello 웹 서버를 일반적으로 IIS)</span><span class="sxs-lookup"><span data-stu-id="f8de5-116">hello host (hello web server, usually IIS)</span></span>

<span data-ttu-id="f8de5-117">Web API 응용 프로그램 자체는 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-117">A Web API application itself doesn't change.</span></span> <span data-ttu-id="f8de5-118">Hello, 이전에 작성 한 Web API 응용 프로그램 다르지 이며 응용 프로그램 코드의 대부분에 대해 수 toosimply 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-118">It's no different from Web API applications you may have written in hello past, and you should be able toosimply move over most of your application code.</span></span> <span data-ttu-id="f8de5-119">하지만 경우 하 한 호스트 hello 응용 프로그램을 호스팅하는 IIS에서 기능에 사용한 경우와 약간 다릅니다 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-119">But if you've been hosting on IIS, where you host hello application may be a little different from what you're used to.</span></span> <span data-ttu-id="f8de5-120">일부 호스팅 toohello 들어가기 전에 것 보다 친숙 한부터 살펴보겠습니다: hello Web API 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-120">Before we get toohello hosting part, let's start with something more familiar: hello Web API application.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="f8de5-121">Hello 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="f8de5-121">Create hello application</span></span>
<span data-ttu-id="f8de5-122">Visual Studio 2015에서 단일 상태 비저장 서비스로 새 Service Fabric 응용 프로그램을 만드는 것으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-122">Start by creating a new Service Fabric application with a single stateless service in Visual Studio 2015.</span></span>

<span data-ttu-id="f8de5-123">Web API를 사용 하 여 상태 비저장 서비스에 대 한 Visual Studio 템플릿을 사용할 수 있는 tooyou입니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-123">A Visual Studio template for a stateless service using Web API is available tooyou.</span></span> <span data-ttu-id="f8de5-124">이 자습서에서는 이 템플릿을 선택한 경우에 제공되는 Web API 프로젝트를 처음부터 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-124">In this tutorial, we'll build a Web API project from scratch that results in what you'd get if you selected this template.</span></span>

<span data-ttu-id="f8de5-125">빈 상태 비저장 서비스 프로젝트 toolearn toobuild 처음부터 웹 API 프로젝트 hello 상태 비저장 서비스 Web API 템플릿으로 시작 하 고 하기만 하면 함께 진행할 수 방법을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-125">Select a blank Stateless Service project toolearn how toobuild a Web API project from scratch, or you can start with hello stateless service Web API template and simply follow along.</span></span>  

<span data-ttu-id="f8de5-126">hello 첫 번째 단계는 웹 API에 대 한 일부 NuGet 패키지가에 toopull입니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-126">hello first step is toopull in some NuGet packages for Web API.</span></span> <span data-ttu-id="f8de5-127">hello 패키지 toouse 원하는 Microsoft.AspNet.WebApi.OwinSelfHost입니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-127">hello package we want toouse is Microsoft.AspNet.WebApi.OwinSelfHost.</span></span> <span data-ttu-id="f8de5-128">이 패키지에 모든 hello 필요한 웹 API 패키지 및 hello *호스트* 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-128">This package includes all hello necessary Web API packages and hello *host* packages.</span></span> <span data-ttu-id="f8de5-129">호스트 패키지는 나중에 중요하게 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-129">This will be important later.</span></span>

<span data-ttu-id="f8de5-130">Hello 패키지를 설치한 후에 hello 기본 웹 API 프로젝트 구조 구축을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-130">After hello packages have been installed, you can begin building out hello basic Web API project structure.</span></span> <span data-ttu-id="f8de5-131">웹 API를 사용한 경우 hello 프로젝트 구조는 친숙 하 게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-131">If you've used Web API, hello project structure should look very familiar.</span></span> <span data-ttu-id="f8de5-132">먼저 `Controllers` 디렉터리 및 간단한 값 컨트롤러를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-132">Start by adding a `Controllers` directory and a simple values controller:</span></span>

<span data-ttu-id="f8de5-133">**ValuesController.cs**</span><span class="sxs-lookup"><span data-stu-id="f8de5-133">**ValuesController.cs**</span></span>

```csharp
using System.Collections.Generic;
using System.Web.Http;

namespace WebService.Controllers
{
    public class ValuesController : ApiController
    {
        // GET api/values 
        public IEnumerable<string> Get()
        {
            return new string[] { "value1", "value2" };
        }

        // GET api/values/5 
        public string Get(int id)
        {
            return "value";
        }

        // POST api/values 
        public void Post([FromBody]string value)
        {
        }

        // PUT api/values/5 
        public void Put(int id, [FromBody]string value)
        {
        }

        // DELETE api/values/5 
        public void Delete(int id)
        {
        }
    }
}

```

<span data-ttu-id="f8de5-134">다음으로 hello 프로젝트 루트 tooregister hello 라우팅, 포맷터 및 기타 구성 설정에서 시작 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-134">Next, add a Startup class at hello project root tooregister hello routing, formatters, and any other configuration setup.</span></span> <span data-ttu-id="f8de5-135">에이 있는 웹 API를 플러그 인 toohello *호스트*, 나중에 다시 revisited 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-135">This is also where Web API plugs in toohello *host*, which will be revisited again later.</span></span> 

<span data-ttu-id="f8de5-136">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="f8de5-136">**Startup.cs**</span></span>

```csharp
using System.Web.Http;
using Owin;

namespace WebService
{
    public static class Startup
    {
        public static void ConfigureApp(IAppBuilder appBuilder)
        {
            // Configure Web API for self-host. 
            HttpConfiguration config = new HttpConfiguration();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            appBuilder.UseWebApi(config);
        }
    }
}
```

<span data-ttu-id="f8de5-137">Hello 응용 프로그램 일부 작업이 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-137">That's it for hello application part.</span></span> <span data-ttu-id="f8de5-138">이 시점에서 방금 hello 기본적인 웹 API 프로젝트 레이아웃 설치 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-138">At this point, we've set up just hello basic Web API project layout.</span></span> <span data-ttu-id="f8de5-139">지금까지 hello 기본 Web API 템플릿을 또는 hello 이전에 기록한 웹 API 프로젝트에서에 훨씬 다르게 표시 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-139">So far, it shouldn't look much different from Web API projects you may have written in hello past or from hello basic Web API template.</span></span> <span data-ttu-id="f8de5-140">비즈니스 논리 hello 컨트롤러와 모델에서 일반적으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-140">Your business logic goes in hello controllers and models as usual.</span></span>

<span data-ttu-id="f8de5-141">이제 호스팅을 실제로 실행하려면 어떤 작업을 해야 할까요?</span><span class="sxs-lookup"><span data-stu-id="f8de5-141">Now what do we do about hosting so that we can actually run it?</span></span>

## <a name="service-hosting"></a><span data-ttu-id="f8de5-142">서비스 호스팅</span><span class="sxs-lookup"><span data-stu-id="f8de5-142">Service hosting</span></span>
<span data-ttu-id="f8de5-143">서비스 패브릭에서 서비스는 서비스 코드를 실행하는 실행 파일인 *서비스 호스트 프로세스*에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-143">In Service Fabric, your service runs in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="f8de5-144">Hello 신뢰할 수 있는 서비스 API를 사용 하 여 서비스를 작성 하는 경우 서비스 프로젝트는 방금 tooan 서비스 유형을 등록 하 고 코드를 실행 하는 실행 파일을 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-144">When you write a service by using hello Reliable Services API, your service project just compiles tooan executable file that registers your service type and runs your code.</span></span> <span data-ttu-id="f8de5-145">.NET의 서비스 패브릭에 서비스를 작성하는 대부분의 경우에도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-145">This is true in most cases when you write a service on Service Fabric in .NET.</span></span> <span data-ttu-id="f8de5-146">Hello 상태 비저장 서비스 프로젝트에서 Program.cs를 열 때 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-146">When you open Program.cs in hello stateless service project, you should see:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric.Services.Runtime;

internal static class Program
{
    private static void Main()
    {
        try
        {
            ServiceRuntime.RegisterServiceAsync("WebServiceType",
                context => new WebService(context)).GetAwaiter().GetResult();

            ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(WebService).Name);

            // Prevents this host process from terminating so services keeps running. 
            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

<span data-ttu-id="f8de5-147">처럼 보입니다. 의심 스러운 hello 입력 지점 tooa 콘솔 응용 프로그램, 하 이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-147">If that looks suspiciously like hello entry point tooa console application, that's because it is.</span></span>

<span data-ttu-id="f8de5-148">에 대 한 자세한 내용은 hello 서비스 호스트 프로세스 및 서비스 등록이 문서의 hello 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-148">Further details about hello service host process and service registration are beyond hello scope of this article.</span></span> <span data-ttu-id="f8de5-149">에 대 한 중요 한 tooknow 이지만 이제 *서비스 코드를 실행 하는 자체 프로세스에서*합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-149">But it's important tooknow for now that *your service code is running in its own process*.</span></span>

## <a name="self-host-web-api-with-an-owin-host"></a><span data-ttu-id="f8de5-150">OWIN 호스트로 자체 호스팅되는 Web API</span><span class="sxs-lookup"><span data-stu-id="f8de5-150">Self-host Web API with an OWIN host</span></span>
<span data-ttu-id="f8de5-151">Web API 응용 프로그램 코드를 자체 프로세스에서 호스팅되면을 어떻게 수행 연결 tooa 웹 서버?</span><span class="sxs-lookup"><span data-stu-id="f8de5-151">Given that your Web API application code is hosted in its own process, how do you hook it up tooa web server?</span></span> <span data-ttu-id="f8de5-152">[OWIN](http://owin.org/)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-152">Enter [OWIN](http://owin.org/).</span></span> <span data-ttu-id="f8de5-153">OWIN은 간단히 말해 .NET 웹 응용 프로그램 및 웹 서버 간의 계약입니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-153">OWIN is simply a contract between .NET web applications and web servers.</span></span> <span data-ttu-id="f8de5-154">일반적으로 (위쪽 tooMVC 5)는 ASP.NET을 사용 하는 경우 hello 웹 응용 프로그램은 System.Web 통해 밀접 하 게 결합 된 tooIIS 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-154">Traditionally when ASP.NET (up tooMVC 5) is used, hello web application is tightly coupled tooIIS through System.Web.</span></span> <span data-ttu-id="f8de5-155">그러나 웹 API 호스팅하고 있는 hello 웹 서버에서 분리 하는 웹 응용 프로그램을 작성할 수 있습니다 OWIN를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-155">However, Web API implements OWIN, so you can write a web application that is decoupled from hello web server that hosts it.</span></span> <span data-ttu-id="f8de5-156">이 때문에 사용자 고유의 프로세스에서 시작할 수 있는 *자체 호스팅* OWIN 웹 서버를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-156">Because of this, you can use a *self-hosted* OWIN web server that you can start in your own process.</span></span> <span data-ttu-id="f8de5-157">지금까지 언급 된 hello 서비스 패브릭 호스팅 모델을 완벽 하 게 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-157">This fits perfectly with hello Service Fabric hosting model we just described.</span></span>

<span data-ttu-id="f8de5-158">이 문서에서는 hello Web API 응용 프로그램에 대 한 Katana를 hello OWIN 호스트로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-158">In this article, we'll use Katana as hello OWIN host for hello Web API application.</span></span> <span data-ttu-id="f8de5-159">Katana는 기반으로 하는 오픈 소스 OWIN 호스트 구현 [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) Windows hello 및 [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-159">Katana is an open-source OWIN host implementation built on [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) and hello Windows [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="f8de5-160">Katana, 이동 toohello에 대 한 자세한 toolearn [Katana 사이트](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-160">toolearn more about Katana, go toohello [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span></span> <span data-ttu-id="f8de5-161">간략 한 개요는 방법에 대 한 toouse Katana tooself 호스트 웹 API 참조 [사용 OWIN tooSelf 호스트 ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-161">For a quick overview of how toouse Katana tooself-host Web API, see [Use OWIN tooSelf-Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span></span>
> 
> 

## <a name="set-up-hello-web-server"></a><span data-ttu-id="f8de5-162">Hello 웹 서버 설정</span><span class="sxs-lookup"><span data-stu-id="f8de5-162">Set up hello web server</span></span>
<span data-ttu-id="f8de5-163">사용자 및 클라이언트 tooconnect toohello 서비스를 허용 하는 통신 스택이 연결할 수 있는 통신 진입점을 제공 하는 hello 신뢰할 수 있는 서비스 API:</span><span class="sxs-lookup"><span data-stu-id="f8de5-163">hello Reliable Services API provides a communication entry point where you can plug in communication stacks that allow users and clients tooconnect toohello service:</span></span>

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

<span data-ttu-id="f8de5-164">hello 웹 서버 (및 hello Websocket 같은 향후에 사용 하 여 다른 통신 스택과) 사용 해야 hello ICommunicationListener 인터페이스 toointegrate 올바르게 hello 시스템과 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-164">hello web server (and any other communication stack you use in hello future, such as WebSockets) should use hello ICommunicationListener interface toointegrate correctly with hello system.</span></span> <span data-ttu-id="f8de5-165">이 hello 이유 단계를 수행 하는 hello에 더 분명 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-165">hello reasons for this will become more apparent in hello following steps.</span></span>

<span data-ttu-id="f8de5-166">먼저 ICommunicationListener를 구현하는 OwinCommunicationListener라는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-166">First, create a class called OwinCommunicationListener that implements ICommunicationListener:</span></span>

<span data-ttu-id="f8de5-167">**OwinCommunicationListener.cs**</span><span class="sxs-lookup"><span data-stu-id="f8de5-167">**OwinCommunicationListener.cs**</span></span>

```csharp
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;
using System;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        public void Abort()
        {
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
        }
    }
}
```

<span data-ttu-id="f8de5-168">hello ICommunicationListener 인터페이스 서비스에 대 한 세 가지 메서드 toomanage 통신 수신기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-168">hello ICommunicationListener interface provides three methods toomanage a communication listener for your service:</span></span>

* <span data-ttu-id="f8de5-169">*OpenAsync*.</span><span class="sxs-lookup"><span data-stu-id="f8de5-169">*OpenAsync*.</span></span> <span data-ttu-id="f8de5-170">요청에 대한 수신 대기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-170">Start listening for requests.</span></span>
* <span data-ttu-id="f8de5-171">*CloseAsync*.</span><span class="sxs-lookup"><span data-stu-id="f8de5-171">*CloseAsync*.</span></span> <span data-ttu-id="f8de5-172">요청에 대한 수신 대기를 중지하고, 진행 중인 모든 요청을 완료하고, 정상적으로 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-172">Stop listening for requests, finish any in-flight requests, and shut down gracefully.</span></span>
* <span data-ttu-id="f8de5-173">*Abort*.</span><span class="sxs-lookup"><span data-stu-id="f8de5-173">*Abort*.</span></span> <span data-ttu-id="f8de5-174">모든 것을 취소하고 즉시 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-174">Cancel everything and stop immediately.</span></span>

<span data-ttu-id="f8de5-175">tooget 시작 작업 hello 수신기 toofunction 할에 대 한 전용 클래스 멤버를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-175">tooget started, add private class members for things hello listener will need toofunction.</span></span> <span data-ttu-id="f8de5-176">이러한 hello 생성자를 통해 초기화 되며 URL을 수신 대기 하는 hello를 설정할 때 나중에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-176">These will be initialized through hello constructor and used later when you set up hello listening URL.</span></span>

```csharp
internal class OwinCommunicationListener : ICommunicationListener
{
    private readonly ServiceEventSource eventSource;
    private readonly Action<IAppBuilder> startup;
    private readonly ServiceContext serviceContext;
    private readonly string endpointName;
    private readonly string appRoot;

    private IDisposable webApp;
    private string publishAddress;
    private string listeningAddress;

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
        : this(startup, serviceContext, eventSource, endpointName, null)
    {
    }

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
    {
        if (startup == null)
        {
            throw new ArgumentNullException(nameof(startup));
        }

        if (serviceContext == null)
        {
            throw new ArgumentNullException(nameof(serviceContext));
        }

        if (endpointName == null)
        {
            throw new ArgumentNullException(nameof(endpointName));
        }

        if (eventSource == null)
        {
            throw new ArgumentNullException(nameof(eventSource));
        }

        this.startup = startup;
        this.serviceContext = serviceContext;
        this.endpointName = endpointName;
        this.eventSource = eventSource;
        this.appRoot = appRoot;
    }


    ...

```

## <a name="implement-openasync"></a><span data-ttu-id="f8de5-177">OpenAsync 구현</span><span class="sxs-lookup"><span data-stu-id="f8de5-177">Implement OpenAsync</span></span>
<span data-ttu-id="f8de5-178">tooset hello 웹 서버를, 두 가지 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-178">tooset up hello web server, you need two pieces of information:</span></span>

* <span data-ttu-id="f8de5-179">*URL 경로 접두사*.</span><span class="sxs-lookup"><span data-stu-id="f8de5-179">*A URL path prefix*.</span></span> <span data-ttu-id="f8de5-180">선택 사항 이지만 그는 tooset 하면이 이제 응용 프로그램에서 여러 웹 서비스를 안전 하 게 호스팅할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-180">Although this is optional, it's good for you tooset this up now so that you can safely host multiple web services in your application.</span></span>
* <span data-ttu-id="f8de5-181">*포트*.</span><span class="sxs-lookup"><span data-stu-id="f8de5-181">*A port*.</span></span>

<span data-ttu-id="f8de5-182">웹 서버 hello에 대 한 포트를 받으려면 먼저에 서비스 패브릭 응용 프로그램 사이 실행 하는 hello 기본 운영 체제 버퍼 역할을 하는 응용 프로그램 계층을 제공 하는지 이해 하는 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-182">Before you get a port for hello web server, it's important that you understand that Service Fabric provides an application layer that acts as a buffer between your application and hello underlying operating system that it runs on.</span></span> <span data-ttu-id="f8de5-183">따라서 서비스 패브릭 제공 방법을 tooconfigure *끝점* 서비스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-183">As such, Service Fabric provides a way tooconfigure *endpoints* for your services.</span></span> <span data-ttu-id="f8de5-184">서비스 패브릭 끝점은 서비스 toouse에 사용할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-184">Service Fabric ensures that endpoints are available for your service toouse.</span></span> <span data-ttu-id="f8de5-185">이러한 방식으로 없는 tooconfigure로 hello OS 환경 내부에서 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-185">This way, you don't have tooconfigure them yourself in hello underlying OS environment.</span></span> <span data-ttu-id="f8de5-186">모든 변경 내용을 tooyour 응용 프로그램 toomake 필요 없이 다양 한 환경에서 서비스 패브릭 응용 프로그램을 쉽게 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-186">You can easily host your Service Fabric application in different environments without having toomake any changes tooyour application.</span></span> <span data-ttu-id="f8de5-187">(호스팅할 수는 예를 들어 hello 자체 데이터 센터 또는 Azure에서 동일한 응용 프로그램입니다.)</span><span class="sxs-lookup"><span data-stu-id="f8de5-187">(For example, you can host hello same application in Azure or in your own datacenter.)</span></span>

<span data-ttu-id="f8de5-188">PackageRoot\ServiceManifest.xml에 HTTP 끝점을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-188">Configure an HTTP endpoint in PackageRoot\ServiceManifest.xml:</span></span>

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

<span data-ttu-id="f8de5-189">이 단계는 hello 서비스 호스트 프로세스는 제한 된 자격 증명 (Windows에서 네트워크 서비스)에서 실행 되기 때문에 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-189">This step is important because hello service host process runs under restricted credentials (Network Service on Windows).</span></span> <span data-ttu-id="f8de5-190">즉, 서비스 않습니다 액세스 tooset HTTP 끝점을 자체적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-190">This means that your service won't have access tooset up an HTTP endpoint on its own.</span></span> <span data-ttu-id="f8de5-191">Hello 끝점 구성을 사용 하 여, 서비스 패브릭 서비스 hello URL에서 수신 대기 하는 hello에 대 한 tooset hello 적절 한 액세스 제어 목록 (ACL)를 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-191">By using hello endpoint configuration, Service Fabric knows tooset up hello proper access control list (ACL) for hello URL that hello service will listen on.</span></span> <span data-ttu-id="f8de5-192">서비스 패브릭은 또한 표준 바로 가기를 tooconfigure 끝점 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-192">Service Fabric also provides a standard place tooconfigure endpoints.</span></span>

<span data-ttu-id="f8de5-193">다시 OwinCommunicationListener.cs에서 OpenAsync 구현을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-193">Back in OwinCommunicationListener.cs, you can start implementing OpenAsync.</span></span> <span data-ttu-id="f8de5-194">이 hello 웹 서버를 시작 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-194">This is where you start hello web server.</span></span> <span data-ttu-id="f8de5-195">첫째, hello 끝점 정보를 가져오고 hello 서비스에서 수신 대기 하는 hello URL을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-195">First, get hello endpoint information and create hello URL that hello service will listen on.</span></span> <span data-ttu-id="f8de5-196">hello URL hello 수신기 상태 비저장 서비스 또는 상태 저장 서비스에 사용 되는 여부에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-196">hello URL will be different depending on whether hello listener is used in a stateless service or a stateful service.</span></span> <span data-ttu-id="f8de5-197">상태 저장 서비스에 대 한 hello 수신기 toocreate는 고유한 주소 모든 상태 저장 서비스 복제본에 대해 수신에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-197">For a stateful service, hello listener needs toocreate a unique address for every stateful service replica it listens on.</span></span> <span data-ttu-id="f8de5-198">상태 비저장 서비스에 대 한 hello 주소 간단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-198">For stateless services, hello address can be much simpler.</span></span> 

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
    var protocol = serviceEndpoint.Protocol;
    int port = serviceEndpoint.Port;

    if (this.serviceContext is StatefulServiceContext)
    {
        StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}{3}/{4}/{5}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/',
            statefulServiceContext.PartitionId,
            statefulServiceContext.ReplicaId,
            Guid.NewGuid());
    }
    else if (this.serviceContext is StatelessServiceContext)
    {
        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/');
    }
    else
    {
        throw new InvalidOperationException();
    }

    ...

```

<span data-ttu-id="f8de5-199">여기에 "http://+"가 사용된 점에 주목하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-199">Note that "http://+" is used here.</span></span> <span data-ttu-id="f8de5-200">이 해당 hello 웹 서버는 localhost, FQDN 및 컴퓨터 IP hello 비롯 한 모든 사용 가능한 주소에서 수신 하는지 toomake입니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-200">This is toomake sure that hello web server is listening on all available addresses, including localhost, FQDN, and hello machine IP.</span></span>

<span data-ttu-id="f8de5-201">hello OpenAsync 구현 중 하나인 hello 가장 중요 한 이유에서 직접 방금 있어야 하는 것이 아니라는 ICommunicationListener 오픈 hello 웹 서버 (또는 모든 통신 스택을)가 구현 되는 이유 `RunAsync()` hello 서비스에서입니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-201">hello OpenAsync implementation is one of hello most important reasons why hello web server (or any communication stack) is implemented as an ICommunicationListener, rather than just having it open directly from `RunAsync()` in hello service.</span></span> <span data-ttu-id="f8de5-202">hello OpenAsync 반환 값은 웹 서버 hello hello 주소에서 수신 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-202">hello return value from OpenAsync is hello address that hello web server is listening on.</span></span> <span data-ttu-id="f8de5-203">이 주소는 toohello 시스템을 반환 하는 경우 hello 서비스와 hello 주소를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-203">When this address is returned toohello system, it registers hello address with hello service.</span></span> <span data-ttu-id="f8de5-204">서비스 패브릭 서비스 이름으로이 주소에 대 한 클라이언트 및 다른 서비스 toothen 허용 하는 API 요청을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-204">Service Fabric provides an API that allows clients and other services toothen ask for this address by service name.</span></span> <span data-ttu-id="f8de5-205">Hello 서비스 주소를 고정 없기 때문에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-205">This is important because hello service address is not static.</span></span> <span data-ttu-id="f8de5-206">서비스는 리소스 균형 조정 및 가용성 목적으로 hello 클러스터에 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-206">Services are moved around in hello cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="f8de5-207">클라이언트가 서비스에 대 한 주소를 수신 대기 tooresolve hello 있도록 hello 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-207">This is hello mechanism that allows clients tooresolve hello listening address for a service.</span></span>

<span data-ttu-id="f8de5-208">이 점을 염두에서 OpenAsync hello 웹 서버를 시작 하 고 hello 주소에서 수신 대기 중인를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-208">With that in mind, OpenAsync starts hello web server and returns hello address that it's listening on.</span></span> <span data-ttu-id="f8de5-209">"Http://+"에서 수신 대기 하도록 확인 하지만 OpenAsync hello 주소를 반환 하기 전에 hello "+" hello IP 또는 FQDN 현재 hello 노드의 아래 템플릿으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-209">Note that it listens on "http://+", but before OpenAsync returns hello address, hello "+" is replaced with hello IP or FQDN of hello node it is currently on.</span></span> <span data-ttu-id="f8de5-210">이 메서드에 의해 반환 되는 hello 주소 기능에 등록 된 hello 시스템은입니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-210">hello address that is returned by this method is what's registered with hello system.</span></span> <span data-ttu-id="f8de5-211">또는 클라이언트 및 기타 서비스가 서비스의 주소를 요청할 때 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-211">It's also what clients and other services see when they ask for a service's address.</span></span> <span data-ttu-id="f8de5-212">클라이언트 toocorrectly tooit 연결 hello 주소에서 실제 IP 또는 FQDN 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-212">For clients toocorrectly connect tooit, they need an actual IP or FQDN in hello address.</span></span>

```csharp
    ...

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    try
    {
        this.eventSource.Message("Starting web server on " + this.listeningAddress);

        this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

        this.eventSource.Message("Listening on " + this.publishAddress);

        return Task.FromResult(this.publishAddress);
    }
    catch (Exception ex)
    {
        this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

        this.StopWebServer();

        throw;
    }
}

```

<span data-ttu-id="f8de5-213">Note toohello OwinCommunicationListener hello 생성자에 전달 된 hello 시작 클래스를 참조 하는이 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-213">Note that this references hello Startup class that was passed in toohello OwinCommunicationListener in hello constructor.</span></span> <span data-ttu-id="f8de5-214">이 시작 인스턴스 hello 웹 서버 toobootstrap hello Web API 응용 프로그램에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-214">This startup instance is used by hello web server toobootstrap hello Web API application.</span></span>

<span data-ttu-id="f8de5-215">hello `ServiceEventSource.Current.Message()` 줄 나중 hello 진단 이벤트 창에 표시 될 응용 프로그램 tooconfirm hello를 실행할 때 해당 hello 웹 서버를 시작 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-215">hello `ServiceEventSource.Current.Message()` line will appear in hello Diagnostic Events window later, when you run hello application tooconfirm that hello web server has started successfully.</span></span>

## <a name="implement-closeasync-and-abort"></a><span data-ttu-id="f8de5-216">CloseAsync 및 Abort 구현</span><span class="sxs-lookup"><span data-stu-id="f8de5-216">Implement CloseAsync and Abort</span></span>
<span data-ttu-id="f8de5-217">마지막으로,와 둘 다 구현할 CloseAsync 중단 toostop hello 웹 서버.</span><span class="sxs-lookup"><span data-stu-id="f8de5-217">Finally, implement both CloseAsync and Abort toostop hello web server.</span></span> <span data-ttu-id="f8de5-218">웹 서버 hello OpenAsync 동안 생성 된 hello 서버 핸들을 삭제 하 여 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-218">hello web server can be stopped by disposing hello server handle that was created during OpenAsync.</span></span>

```csharp
public Task CloseAsync(CancellationToken cancellationToken)
{
    this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

    this.StopWebServer();

    return Task.FromResult(true);
}

public void Abort()
{
    this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

    this.StopWebServer();
}

private void StopWebServer()
{
    if (this.webApp != null)
    {
        try
        {
            this.webApp.Dispose();
        }
        catch (ObjectDisposedException)
        {
            // no-op
        }
    }
}
```

<span data-ttu-id="f8de5-219">이 구현은 예제 CloseAsync 및 Abort 모두 단순히 hello 웹 서버를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-219">In this implementation example, both CloseAsync and Abort simply stop hello web server.</span></span> <span data-ttu-id="f8de5-220">Tooperform CloseAsync hello 웹 서버의 더욱 원활 하 게 조정 된 종료를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-220">You may opt tooperform a more gracefully coordinated shutdown of hello web server in CloseAsync.</span></span> <span data-ttu-id="f8de5-221">예를 들어 hello 종료 진행 중인 요청 toobe hello 반환 하기 전에 완료를 대기할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-221">For example, hello shutdown could wait for in-flight requests toobe completed before hello return.</span></span>

## <a name="start-hello-web-server"></a><span data-ttu-id="f8de5-222">Hello 웹 서버를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-222">Start hello web server</span></span>
<span data-ttu-id="f8de5-223">이제 toocreate 준비 하 고 OwinCommunicationListener toostart hello 웹 서버 인스턴스를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-223">You're now ready toocreate and return an instance of OwinCommunicationListener toostart hello web server.</span></span> <span data-ttu-id="f8de5-224">서비스 클래스 (WebService.cs) hello에 다시 hello 재정의 `CreateServiceInstanceListeners()` 메서드:</span><span class="sxs-lookup"><span data-stu-id="f8de5-224">Back in hello Service class (WebService.cs), override hello `CreateServiceInstanceListeners()` method:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                           .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                           .Select(endpoint => endpoint.Name);

    return endpoints.Select(endpoint => new ServiceInstanceListener(
        serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
}
```

<span data-ttu-id="f8de5-225">이 웹 API를 hello 여기서은 *응용 프로그램* OWIN hello 및 *호스트* 마지막으로 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-225">This is where hello Web API *application* and hello OWIN *host* finally meet.</span></span> <span data-ttu-id="f8de5-226">hello 호스트 (OwinCommunicationListener) hello 인스턴스의 제공할지 *응용 프로그램* (웹 API) hello 시작 클래스를 통해 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-226">hello host (OwinCommunicationListener) is given an instance of hello *application* (Web API) via hello Startup class.</span></span> <span data-ttu-id="f8de5-227">그런 다음 서비스 패브릭이 수명 주기를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-227">Service Fabric then manages its lifecycle.</span></span> <span data-ttu-id="f8de5-228">일반적으로 모든 통신 스택 뒤에 이와 동일한 패턴이 올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-228">This same pattern can typically be followed with any communication stack.</span></span>

## <a name="put-it-all-together"></a><span data-ttu-id="f8de5-229">모든 요소 결합</span><span class="sxs-lookup"><span data-stu-id="f8de5-229">Put it all together</span></span>
<span data-ttu-id="f8de5-230">이 예제에서는 hello에 항목이 toodo 않아도 `RunAsync()` 메서드를 재정의 하는 제거 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-230">In this example, you don't need toodo anything in hello `RunAsync()` method, so that override can simply be removed.</span></span>

<span data-ttu-id="f8de5-231">hello 최종 서비스 구현 매우 간단해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-231">hello final service implementation should be very simple.</span></span> <span data-ttu-id="f8de5-232">또한 toocreate hello 통신 수신기만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-232">It only needs toocreate hello communication listener:</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Fabric;
using System.Fabric.Description;
using System.Linq;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace WebService
{
    internal sealed class WebService : StatelessService
    {
        public WebService(StatelessServiceContext context)
            : base(context)
        { }

        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
            var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                                   .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                                   .Select(endpoint => endpoint.Name);

            return endpoints.Select(endpoint => new ServiceInstanceListener(
                serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
        }
    }
}
```

<span data-ttu-id="f8de5-233">전체 hello `OwinCommunicationListener` 클래스:</span><span class="sxs-lookup"><span data-stu-id="f8de5-233">hello complete `OwinCommunicationListener` class:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        private readonly ServiceEventSource eventSource;
        private readonly Action<IAppBuilder> startup;
        private readonly ServiceContext serviceContext;
        private readonly string endpointName;
        private readonly string appRoot;

        private IDisposable webApp;
        private string publishAddress;
        private string listeningAddress;

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
            : this(startup, serviceContext, eventSource, endpointName, null)
        {
        }

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
        {
            if (startup == null)
            {
                throw new ArgumentNullException(nameof(startup));
            }

            if (serviceContext == null)
            {
                throw new ArgumentNullException(nameof(serviceContext));
            }

            if (endpointName == null)
            {
                throw new ArgumentNullException(nameof(endpointName));
            }

            if (eventSource == null)
            {
                throw new ArgumentNullException(nameof(eventSource));
            }

            this.startup = startup;
            this.serviceContext = serviceContext;
            this.endpointName = endpointName;
            this.eventSource = eventSource;
            this.appRoot = appRoot;
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
            var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
            var protocol = serviceEndpoint.Protocol;
            int port = serviceEndpoint.Port;

            if (this.serviceContext is StatefulServiceContext)
            {
                StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}{3}/{4}/{5}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/',
                    statefulServiceContext.PartitionId,
                    statefulServiceContext.ReplicaId,
                    Guid.NewGuid());
            }
            else if (this.serviceContext is StatelessServiceContext)
            {
                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/');
            }
            else
            {
                throw new InvalidOperationException();
            }

            this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

            try
            {
                this.eventSource.Message("Starting web server on " + this.listeningAddress);

                this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

                this.eventSource.Message("Listening on " + this.publishAddress);

                return Task.FromResult(this.publishAddress);
            }
            catch (Exception ex)
            {
                this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

                this.StopWebServer();

                throw;
            }
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
            this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

            this.StopWebServer();

            return Task.FromResult(true);
        }

        public void Abort()
        {
            this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

            this.StopWebServer();
        }

        private void StopWebServer()
        {
            if (this.webApp != null)
            {
                try
                {
                    this.webApp.Dispose();
                }
                catch (ObjectDisposedException)
                {
                    // no-op
                }
            }
        }
    }
}
```

<span data-ttu-id="f8de5-234">모든 hello 조각을 위치에 저장 했으므로 프로젝트에는 OWIN 호스트 및 신뢰할 수 있는 서비스 API 진입점 일반 Web API 응용 프로그램와 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-234">Now that you have put all hello pieces in place, your project should look like a typical Web API application with Reliable Services API entry points and an OWIN host.</span></span>

## <a name="run-and-connect-through-a-web-browser"></a><span data-ttu-id="f8de5-235">웹 브라우저를 통한 실행 및 연결</span><span class="sxs-lookup"><span data-stu-id="f8de5-235">Run and connect through a web browser</span></span>
<span data-ttu-id="f8de5-236">아직 하지 않았다면 [개발 환경을 설정](service-fabric-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-236">If you haven't done so, [set up your development environment](service-fabric-get-started.md).</span></span>

<span data-ttu-id="f8de5-237">이제 서비스를 빌드하고 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-237">You can now build and deploy your service.</span></span> <span data-ttu-id="f8de5-238">키를 눌러 **F5** toobuild Visual Studio에서에서 및 hello 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-238">Press **F5** in Visual Studio toobuild and deploy hello application.</span></span> <span data-ttu-id="f8de5-239">Hello 진단 이벤트 창에서 웹 서버 hello http://localhost:8281에서 열을 나타내는 메시지가 표시 되어야 / 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-239">In hello Diagnostic Events window, you should see a message that indicates that hello web server opened on http://localhost:8281/.</span></span>

> [!NOTE]
> <span data-ttu-id="f8de5-240">컴퓨터에 다른 프로세스에 의해 hello 포트를 이미 연 경우 다음 오류가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-240">If hello port has already been opened by another process on your machine, you may see an error here.</span></span> <span data-ttu-id="f8de5-241">이 해당 hello 수신기를 열 수 없습니다. 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-241">This indicates that hello listener couldn't be opened.</span></span> <span data-ttu-id="f8de5-242">않은 hello 경우 ServiceManifest.xml의 hello 끝점 구성에 대 한 다른 포트를 사용해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="f8de5-242">If that's hello case, try using a different port for hello endpoint configuration in ServiceManifest.xml.</span></span>
> 
> 

<span data-ttu-id="f8de5-243">Hello 서비스가 실행 되 면 브라우저를 열고 너무 이동[http://localhost:8281/api/값](http://localhost:8281/api/values) tootest 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-243">Once hello service is running, open a browser and navigate too[http://localhost:8281/api/values](http://localhost:8281/api/values) tootest it.</span></span>

## <a name="scale-it-out"></a><span data-ttu-id="f8de5-244">확장</span><span class="sxs-lookup"><span data-stu-id="f8de5-244">Scale it out</span></span>
<span data-ttu-id="f8de5-245">일반적으로 상태 비저장 웹 앱 확장은 더 많은 컴퓨터를 추가 하 고 hello 웹 앱에 스핀업을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-245">Scaling out stateless web apps typically means adding more machines and spinning up hello web apps on them.</span></span> <span data-ttu-id="f8de5-246">서비스 패브릭 오케스트레이션 엔진 이렇게 할 수 있습니다에 대 한 새 노드가 tooa 클러스터에 추가 될 때마다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-246">Service Fabric's orchestration engine can do this for you whenever new nodes are added tooa cluster.</span></span> <span data-ttu-id="f8de5-247">Hello 번호를 지정할 수는 상태 비저장 서비스의 인스턴스를 만들 때 원하는 toocreate 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="f8de5-247">When you create instances of a stateless service, you can specify hello number of instances you want toocreate.</span></span> <span data-ttu-id="f8de5-248">서비스 패브릭 hello 클러스터의 노드에 해당 인스턴스 수를 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-248">Service Fabric places that number of instances on nodes in hello cluster.</span></span> <span data-ttu-id="f8de5-249">수행 하면 노드 인스턴스 여러 개 toocreate 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-249">And it makes sure not toocreate more than one instance on any one node.</span></span> <span data-ttu-id="f8de5-250">서비스 패브릭 tooalways 모든 노드에 대해 지정 하 여 인스턴스를 만들 지정할 수도 있습니다 **-1** hello 인스턴스 수에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-250">You can also instruct Service Fabric tooalways create an instance on every node by specifying **-1** for hello instance count.</span></span> <span data-ttu-id="f8de5-251">이렇게 하면 클러스터 아웃 tooscale 노드를 추가할 때마다 상태 비저장 서비스의 인스턴스 hello 새 노드에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-251">This guarantees that whenever you add nodes tooscale out your cluster, an instance of your stateless service will be created on hello new nodes.</span></span> <span data-ttu-id="f8de5-252">이 값 hello 서비스 인스턴스의 속성 이므로 서비스 인스턴스를 만들 때 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-252">This value is a property of hello service instance, so it is set when you create a service instance.</span></span> <span data-ttu-id="f8de5-253">PowerShell을 통해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-253">You can do this through PowerShell:</span></span>

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

<span data-ttu-id="f8de5-254">또는 Visual Studio 상태 비저장 서비스 프로젝트의 기본 서비스를 정의할 때 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-254">You can also do this when you define a default service in a Visual Studio stateless service project:</span></span>

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

<span data-ttu-id="f8de5-255">Toocreate 응용 프로그램 및 서비스 인스턴스를 참조 하는 방법에 대 한 자세한 내용은 [응용 프로그램 배포](service-fabric-deploy-remove-applications.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8de5-255">For more information on how toocreate application and service instances, see [Deploy an application](service-fabric-deploy-remove-applications.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8de5-256">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f8de5-256">Next steps</span></span>
[<span data-ttu-id="f8de5-257">Visual Studio를 사용하여 서비스 패브릭 응용 프로그램 디버그</span><span class="sxs-lookup"><span data-stu-id="f8de5-257">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

