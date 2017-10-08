---
title: "ASP.NET Core를 사용 하 여 Azure 서비스 패브릭 응용 프로그램에 대 한 웹 프런트 엔드 aaaCreate | Microsoft Docs"
description: "ASP.NET Core 프로젝트와 원격 서비스를 통해 서비스 통신을 사용 하 여 서비스 패브릭 응용 프로그램 toohello 웹을 노출 합니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: 0c4454d6cac4c2e343bd6e93e56d3d2f0ebfc4ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a><span data-ttu-id="70c34-103">ASP.NET Core를 사용하여 응용 프로그램에 대한 웹 서비스 프런트 엔드 구축</span><span class="sxs-lookup"><span data-stu-id="70c34-103">Build a web service front end for your application using ASP.NET Core</span></span>
<span data-ttu-id="70c34-104">기본적으로 Azure 서비스 패브릭 서비스는 공용 인터페이스 toohello 웹을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-104">By default, Azure Service Fabric services do not provide a public interface toohello web.</span></span> <span data-ttu-id="70c34-105">tooexpose toocreate 웹 tooact를 진입점으로 프로젝트를 마우스 다음 없어 tooyour에서 통신 해야 응용 프로그램의 기능 tooHTTP 클라이언트 개별 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-105">tooexpose your application's functionality tooHTTP clients, you have toocreate a web project tooact as an entry point and then communicate from there tooyour individual services.</span></span>

<span data-ttu-id="70c34-106">이 자습서에서는 가져갈부터 hello에 [Visual Studio에서 응용 프로그램 처음 만들기](service-fabric-create-your-first-application-in-visual-studio.md) 자습서 hello 카운터 상태 저장 서비스 앞에 ASP.NET Core 웹 서비스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-106">In this tutorial, we pick up where we left off in hello [Creating your first application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) tutorial and add an ASP.NET Core web service in front of hello stateful counter service.</span></span> <span data-ttu-id="70c34-107">아직 수행하지 않은 경우 다시 돌아가서 먼저 해당 자습서를 단계별로 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-107">If you have not already done so, you should go back and step through that tutorial first.</span></span>

## <a name="set-up-your-environment-for-aspnet-core"></a><span data-ttu-id="70c34-108">ASP.NET Core에 대한 환경 설정</span><span class="sxs-lookup"><span data-stu-id="70c34-108">Set up your environment for ASP.NET Core</span></span>

<span data-ttu-id="70c34-109">이 자습서와 함께 Visual Studio 2017 toofollow가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-109">You need Visual Studio 2017 toofollow along with this tutorial.</span></span> <span data-ttu-id="70c34-110">모든 버전에서 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-110">Any edition will do.</span></span> 

 - [<span data-ttu-id="70c34-111">Visual Studio 2017 설치</span><span class="sxs-lookup"><span data-stu-id="70c34-111">Install Visual Studio 2017</span></span>](https://www.visualstudio.com/)

<span data-ttu-id="70c34-112">toodevelop ASP.NET Core 서비스 패브릭 응용 프로그램 설치 작업을 수행 하는 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-112">toodevelop ASP.NET Core Service Fabric applications, you should have hello following workloads installed:</span></span>
 - <span data-ttu-id="70c34-113">**Azure 개발**(*웹 및 클라우드* 아래)</span><span class="sxs-lookup"><span data-stu-id="70c34-113">**Azure development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="70c34-114">**ASP.NET 및 웹 개발**(*웹 및 클라우드* 아래)</span><span class="sxs-lookup"><span data-stu-id="70c34-114">**ASP.NET and web development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="70c34-115">**.NET Core 플랫폼 간 개발**(*다른 도구 집합* 아래)</span><span class="sxs-lookup"><span data-stu-id="70c34-115">**.NET Core cross-platform development** (under *Other Toolsets*)</span></span>

>[!Note] 
><span data-ttu-id="70c34-116">hello Visual Studio 2015 용.NET Core 도구는 더 이상 업데이트 toohave 필요한 Visual Studio 2015를 아직 사용 중인 경우 [.NET Core VS 2015 Tooling 미리 보기 2](https://www.microsoft.com/net/download/core) 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-116">hello .NET Core tools for Visual Studio 2015 are no longer being updated, however if you are still using Visual Studio 2015, you need toohave [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) installed.</span></span>

## <a name="add-an-aspnet-core-service-tooyour-application"></a><span data-ttu-id="70c34-117">ASP.NET Core 서비스 tooyour 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="70c34-117">Add an ASP.NET Core service tooyour application</span></span>
<span data-ttu-id="70c34-118">ASP.NET Core는 플랫폼 간 경량 웹 개발 프레임 워크 toocreate 최신 웹 UI를 사용할 수 있으며 웹 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-118">ASP.NET Core is a lightweight, cross-platform web development framework that you can use toocreate modern web UI and web APIs.</span></span> 

<span data-ttu-id="70c34-119">ASP.NET Web API 프로젝트 tooour 기존 응용 프로그램을 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-119">Let's add an ASP.NET Web API project tooour existing application.</span></span>

1. <span data-ttu-id="70c34-120">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 **서비스** 내 응용 프로그램 프로젝트 hello 및 선택 **추가 > 새 서비스 패브릭 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-120">In Solution Explorer, right-click **Services** within hello application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![새 서비스 tooan 기존 응용 프로그램 추가][vs-add-new-service]
2. <span data-ttu-id="70c34-122">Hello에 **서비스를 만들** 페이지에서 선택 **ASP.NET Core** 에 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-122">On hello **Create a Service** page, choose **ASP.NET Core** and give it a name.</span></span>
   
    ![Hello 새 서비스 대화 상자에서 ASP.NET 웹 서비스를 선택합니다.][vs-new-service-dialog]

3. <span data-ttu-id="70c34-124">hello 다음 페이지는 ASP.NET Core 집합이 프로젝트 템플릿을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-124">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="70c34-125">동일한 hello는 이러한 참고를 만들면 서비스 패브릭 응용 프로그램, 외부 프로그램 ASP.NET Core 프로젝트 적은 양의 추가 코드 tooregister 볼 수는 선택 사항 hello 서비스 hello 서비스 패브릭 런타임 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-125">Note that these are hello same choices that you would see if you created an ASP.NET Core project outside of a Service Fabric application, with a small amount of additional code tooregister hello service with hello Service Fabric runtime.</span></span> <span data-ttu-id="70c34-126">이 자습서에서는 **Web API**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-126">For this tutorial, choose **Web API**.</span></span> <span data-ttu-id="70c34-127">적용할 수 있습니다는 전체 웹 응용 프로그램에 동일한 개념 toobuilding hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-127">However, you can apply hello same concepts toobuilding a full web application.</span></span>
   
    ![ASP.NET 프로젝트 유형 선택][vs-new-aspnet-project-dialog]
   
    <span data-ttu-id="70c34-129">Web API 프로젝트를 만들었으면 응용 프로그램에 두 개의 서비스가 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-129">Once your Web API project is created, you should have two services in your application.</span></span> <span data-ttu-id="70c34-130">정확 하 게 hello에서 더 많은 서비스를 추가할 수 toobuild 응용 프로그램을 계속 하면서 동일한 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-130">As you continue toobuild your application, you can add more services in exactly hello same way.</span></span> <span data-ttu-id="70c34-131">각 서비스를 독립적으로 버전 지정 및 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-131">Each can be independently versioned and upgraded.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="70c34-132">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="70c34-132">Run hello application</span></span>
<span data-ttu-id="70c34-133">tooget 하겠습니다, 보겠습니다의 의미를 살펴보면 ASP.NET Core 웹 API 템플릿을 hello hello 기본 동작을 제공 하는 내용이 및 hello 새 응용 프로그램 배포.</span><span class="sxs-lookup"><span data-stu-id="70c34-133">tooget a sense of what we've done, let's deploy hello new application and take a look at hello default behavior that hello ASP.NET Core Web API template provides.</span></span>

1. <span data-ttu-id="70c34-134">Visual Studio toodebug hello 응용 프로그램에서 F5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-134">Press F5 in Visual Studio toodebug hello app.</span></span>
2. <span data-ttu-id="70c34-135">배포가 완료 되 면 Visual Studio는 브라우저 toohello 루트 hello ASP.NET Web API 서비스의 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-135">When deployment is complete, Visual Studio launches a browser toohello root of hello ASP.NET Web API service.</span></span> <span data-ttu-id="70c34-136">hello ASP.NET Core 웹 API 템플릿을 404 오류 hello 브라우저에 표시 되어야 하므로 hello 루트에 대 한 기본 동작을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-136">hello ASP.NET Core Web API template doesn't provide default behavior for hello root, so you should see a 404 error in hello browser.</span></span>
3. <span data-ttu-id="70c34-137">추가 `/api/values` hello 브라우저에서 toohello 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-137">Add `/api/values` toohello location in hello browser.</span></span> <span data-ttu-id="70c34-138">그러면 호출 hello `Get` hello Web API 템플릿에 ValuesController hello에 메서드.</span><span class="sxs-lookup"><span data-stu-id="70c34-138">This invokes hello `Get` method on hello ValuesController in hello Web API template.</span></span> <span data-ttu-id="70c34-139">Hello 템플릿--두 문자열을 포함 하는 JSON 배열에서 제공 하는 hello 기본 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-139">It returns hello default response that is provided by hello template--a JSON array that contains two strings:</span></span>
   
    ![ASP.NET Core Web API 템플릿에서 반환되는 기본값][browser-aspnet-template-values]
   
    <span data-ttu-id="70c34-141">Hello 자습서의 hello 결과적으로 기본 문자열이이 페이지 hello hello 대신 상태 저장 서비스에서 가장 최근의 카운터 값 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-141">By hello end of hello tutorial, this page will show hello most recent counter value from our stateful service instead of hello default strings.</span></span>

## <a name="connect-hello-services"></a><span data-ttu-id="70c34-142">Hello 서비스 연결</span><span class="sxs-lookup"><span data-stu-id="70c34-142">Connect hello services</span></span>
<span data-ttu-id="70c34-143">서비스 패브릭은 신뢰할 수 있는 서비스와 유연하게 통신할 수 있는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-143">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="70c34-144">단일 응용 프로그램 내에 TCP를 통해 액세스할 수 있는 서비스, HTTP REST API를 통해 액세스할 수 있는 다른 서비스 및 웹 소켓을 통해 액세스할 수 있는 다른 서비스가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-144">Within a single application, you might have services that are accessible via TCP, other services that are accessible via an HTTP REST API, and still other services that are accessible via web sockets.</span></span> <span data-ttu-id="70c34-145">참조에 대 한 배경 사용할 수 있는 hello 옵션 및 hello 보완, [서비스와 통신](service-fabric-connect-and-communicate-with-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-145">For background on hello options available and hello tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span> <span data-ttu-id="70c34-146">이 자습서에서는 사용 하 여 [서비스 패브릭 원격 서비스](service-fabric-reliable-services-communication-remoting.md)hello SDK에서에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-146">In this tutorial, we use [Service Fabric Service Remoting](service-fabric-reliable-services-communication-remoting.md), provided in hello SDK.</span></span>

<span data-ttu-id="70c34-147">원격 서비스 접근 방식 (원격 프로시저 호출 또는 Rpc에서 모델링) hello 인터페이스 tooact hello hello 서비스에 대 한 공용 계약으로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-147">In hello Service Remoting approach (modeled on remote procedure calls or RPCs), you define an interface tooact as hello public contract for hello service.</span></span> <span data-ttu-id="70c34-148">그런 다음 hello 서비스와 상호 작용 하기 위한 해당 인터페이스 toogenerate 프록시 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-148">Then, you use that interface toogenerate a proxy class for interacting with hello service.</span></span>

### <a name="create-hello-remoting-interface"></a><span data-ttu-id="70c34-149">Hello 원격 인터페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="70c34-149">Create hello remoting interface</span></span>
<span data-ttu-id="70c34-150">상태 저장 서비스의 hello와이 case hello ASP.NET Core 웹 프로젝트의에서 다른 서비스 간의 hello 계약으로 hello 인터페이스 tooact를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-150">Let's start by creating hello interface tooact as hello contract between hello stateful service and other services, in this case hello ASP.NET Core web project.</span></span> <span data-ttu-id="70c34-151">이 인터페이스는 자체 클래스 라이브러리 프로젝트에 만들겠습니다 하므로 toomake RPC 호출을 사용 하는 모든 서비스에서 공유 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-151">This interface must be shared by all services that use it toomake RPC calls, so we'll create it in its own Class Library project.</span></span>

1. <span data-ttu-id="70c34-152">솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭하고 **브라우저에서 해당 위치에** > **새 프로젝트**해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-152">In Solution Explorer, right-click your solution and choose **Add** > **New Project**.</span></span>

2. <span data-ttu-id="70c34-153">Hello 선택 **Visual C#** 왼쪽 탐색 창 및 선택 hello hello에 항목 **클래스 라이브러리** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="70c34-153">Choose hello **Visual C#** entry in hello left navigation pane and then select hello **Class Library** template.</span></span> <span data-ttu-id="70c34-154">해당 hello.NET Framework 버전 너무 설정 되어 있는지 확인**4.5.2**합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-154">Ensure that hello .NET Framework version is set too**4.5.2**.</span></span>
   
    ![상태 저장 서비스에 대한 인터페이스 프로젝트 만들기][vs-add-class-library-project]

3. <span data-ttu-id="70c34-156">Hello 설치 **Microsoft.ServiceFabric.Services.Remoting** NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-156">Install hello **Microsoft.ServiceFabric.Services.Remoting** NuGet package.</span></span> <span data-ttu-id="70c34-157">검색할 **Microsoft.ServiceFabric.Services.Remoting** hello NuGet에서에서 관리자를 패키지 하 고 원격 서비스를 사용 하는 hello 솔루션의 모든 프로젝트에 대 한 설치 포함 하 여:</span><span class="sxs-lookup"><span data-stu-id="70c34-157">Search for  **Microsoft.ServiceFabric.Services.Remoting** in hello NuGet package manager and install it for all projects in hello solution that use Service Remoting, including:</span></span>
   - <span data-ttu-id="70c34-158">hello 서비스 인터페이스를 포함 하는 hello 클래스 라이브러리 프로젝트</span><span class="sxs-lookup"><span data-stu-id="70c34-158">hello Class Library project that contains hello service interface</span></span>
   - <span data-ttu-id="70c34-159">hello 상태 저장 서비스 프로젝트</span><span class="sxs-lookup"><span data-stu-id="70c34-159">hello Stateful Service project</span></span>
   - <span data-ttu-id="70c34-160">hello ASP.NET Core 웹 서비스 프로젝트</span><span class="sxs-lookup"><span data-stu-id="70c34-160">hello ASP.NET Core web service project</span></span>
   
    ![Hello 서비스 NuGet 패키지를 추가합니다.][vs-services-nuget-package]

4. <span data-ttu-id="70c34-162">Hello 클래스 라이브러리의 단일 메서드와 인터페이스를 만듭니다 `GetCountAsync`에서 hello 인터페이스를 확장 하 고 `Microsoft.ServiceFabric.Services.Remoting.IService`합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-162">In hello class library, create an interface with a single method, `GetCountAsync`, and extend hello interface from `Microsoft.ServiceFabric.Services.Remoting.IService`.</span></span> <span data-ttu-id="70c34-163">hello 원격 인터페이스는 원격 서비스 인터페이스는이 인터페이스 tooindicate에서 파생 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-163">hello remoting interface must derive from this interface tooindicate that it is a Service Remoting interface.</span></span>
   
    ```c#
    using Microsoft.ServiceFabric.Services.Remoting;
    using System.Threading.Tasks;
        
    ...

    namespace MyStatefulService.Interface
    {
        public interface ICounter: IService
        {
            Task<long> GetCountAsync();
        }
    }
    ```

### <a name="implement-hello-interface-in-your-stateful-service"></a><span data-ttu-id="70c34-164">상태 저장 서비스의 hello 인터페이스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-164">Implement hello interface in your stateful service</span></span>
<span data-ttu-id="70c34-165">이제 hello 인터페이스를 정의한 필요한 tooimplement hello 상태 저장 서비스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-165">Now that we have defined hello interface, we need tooimplement it in hello stateful service.</span></span>

1. <span data-ttu-id="70c34-166">상태 저장 서비스에 hello 인터페이스를 포함 하는 참조 toohello 클래스 라이브러리 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-166">In your stateful service, add a reference toohello class library project that contains hello interface.</span></span>
   
    ![상태 저장 서비스의 hello에 참조 toohello 클래스 라이브러리 프로젝트를 추가합니다.][vs-add-class-library-reference]
2. <span data-ttu-id="70c34-168">Hello 클래스에서 상속 되는 위치를 찾을 `StatefulService`와 같은 `MyStatefulService`, 고 tooimplement hello 확장 `ICounter` 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-168">Locate hello class that inherits from `StatefulService`, such as `MyStatefulService`, and extend it tooimplement hello `ICounter` interface.</span></span>
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. <span data-ttu-id="70c34-169">이제 hello에 정의 된 hello 단일 메서드를 구현 `ICounter` 인터페이스 `GetCountAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-169">Now implement hello single method that is defined in hello `ICounter` interface, `GetCountAsync`.</span></span>
   
    ```c#
    public async Task<long> GetCountAsync()
    {
        var myDictionary = 
            await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
   
        using (var tx = this.StateManager.CreateTransaction())
        {          
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");
            return result.HasValue ? result.Value : 0;
        }
    }
    ```

### <a name="expose-hello-stateful-service-using-a-service-remoting-listener"></a><span data-ttu-id="70c34-170">서비스 remoting 수신기를 사용 하 여 hello 상태 저장 서비스를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-170">Expose hello stateful service using a service remoting listener</span></span>
<span data-ttu-id="70c34-171">Hello로 `ICounter` 인터페이스 구현 hello 마지막 단계는 tooopen hello 원격 서비스 통신 채널입니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-171">With hello `ICounter` interface implemented, hello final step is tooopen hello Service Remoting communication channel.</span></span> <span data-ttu-id="70c34-172">상태 저장 서비스의 경우 서비스 패브릭은 `CreateServiceReplicaListeners`라는 재정의 가능한 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-172">For stateful services, Service Fabric provides an overridable method called `CreateServiceReplicaListeners`.</span></span> <span data-ttu-id="70c34-173">이 방법으로 통신 서비스에 대 한 tooenable 되도록의 hello 형식을 기반으로 하나 이상의 통신 수신기를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-173">With this method, you can specify one or more communication listeners, based on hello type of communication that you want tooenable for your service.</span></span>

> [!NOTE]
> <span data-ttu-id="70c34-174">통신 채널 toostateless 서비스를 열기 위한 동등한 방법이 hello 라고 `CreateServiceInstanceListeners`합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-174">hello equivalent method for opening a communication channel toostateless services is called `CreateServiceInstanceListeners`.</span></span>

<span data-ttu-id="70c34-175">이 경우 기존 hello 대체 하겠습니다 `CreateServiceReplicaListeners` 메서드의 인스턴스를 제공 하 고 `ServiceRemotingListener`를 통해 클라이언트에서 호출 되는 RPC 끝점 만듦 `ServiceProxy`합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-175">In this case, we replace hello existing `CreateServiceReplicaListeners` method and provide an instance of `ServiceRemotingListener`, which creates an RPC endpoint that is callable from clients through `ServiceProxy`.</span></span>  

<span data-ttu-id="70c34-176">hello `CreateServiceRemotingListener` hello에 대 한 확장 메서드 `IService` 인터페이스 있습니다 tooeasily 만들기는 `ServiceRemotingListener` 모든 기본 설정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-176">hello `CreateServiceRemotingListener` extension method on hello `IService` interface allows you tooeasily create a `ServiceRemotingListener` with all default settings.</span></span> <span data-ttu-id="70c34-177">toouse이 확장 메서드를 hello 해야 `Microsoft.ServiceFabric.Services.Remoting.Runtime` 가져온 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-177">toouse this extension method, ensure you have hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace imported.</span></span> 

```c#
using Microsoft.ServiceFabric.Services.Remoting.Runtime;

...

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new List<ServiceReplicaListener>()
    {
        new ServiceReplicaListener(
            (context) =>
                this.CreateServiceRemotingListener(context))
    };
}
```


### <a name="use-hello-serviceproxy-class-toointeract-with-hello-service"></a><span data-ttu-id="70c34-178">Hello ServiceProxy 클래스 toointeract hello 서비스와 함께 사용</span><span class="sxs-lookup"><span data-stu-id="70c34-178">Use hello ServiceProxy class toointeract with hello service</span></span>
<span data-ttu-id="70c34-179">상태 저장 서비스는 RPC를 통해 이제 다른 서비스에서 준비 tooreceive 트래픽입니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-179">Our stateful service is now ready tooreceive traffic from other services over RPC.</span></span> <span data-ttu-id="70c34-180">따라서 모든 작업을 계속은 hello ASP.NET 웹 서비스에서에서 된 hello 코드 toocommunicate를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-180">So all that remains is adding hello code toocommunicate with it from hello ASP.NET web service.</span></span>

1. <span data-ttu-id="70c34-181">ASP.NET 프로젝트에서 hello를 포함 하는 참조 toohello 클래스 라이브러리 추가 `ICounter` 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-181">In your ASP.NET project, add a reference toohello class library that contains hello `ICounter` interface.</span></span>

2. <span data-ttu-id="70c34-182">Hello 추가한 이전 **Microsoft.ServiceFabric.Services.Remoting** NuGet 패키지 toohello ASP.NET 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="70c34-182">Earlier you added hello **Microsoft.ServiceFabric.Services.Remoting** NuGet package toohello ASP.NET project.</span></span> <span data-ttu-id="70c34-183">이 패키지는 hello 제공 `ServiceProxy` 사용할 수 있는 클래스 toomake RPC toohello 상태 저장 서비스를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-183">This package provides hello `ServiceProxy` class which you use toomake RPC calls toohello stateful service.</span></span> <span data-ttu-id="70c34-184">Hello ASP.NET Core 웹 서비스 프로젝트에서에서이 NuGet 패키지가 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-184">Ensure this NuGet package is installed in hello ASP.NET Core web service project.</span></span>

4. <span data-ttu-id="70c34-185">Hello에 **컨트롤러** 폴더, 열기 hello `ValuesController` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-185">In hello **Controllers** folder, open hello `ValuesController` class.</span></span> <span data-ttu-id="70c34-186">해당 hello 참고 `Get` 메서드는 현재 방금 "value1" 및 "value2"-hello 브라우저 앞에서 살펴본에 일치 하는 하드 코드 된 문자열 배열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-186">Note that hello `Get` method currently just returns a hard-coded string array of "value1" and "value2"--which matches what we saw earlier in hello browser.</span></span> <span data-ttu-id="70c34-187">이 구현을 코드 다음 hello로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-187">Replace this implementation with hello following code:</span></span>
   
    ```c#
    using MyStatefulService.Interface;
    using Microsoft.ServiceFabric.Services.Client;
    using Microsoft.ServiceFabric.Services.Remoting.Client;
   
    ...

    [HttpGet]
    public async Task<IEnumerable<string>> Get()
    {
        ICounter counter =
            ServiceProxy.Create<ICounter>(new Uri("fabric:/MyApplication/MyStatefulService"), new ServicePartitionKey(0));
   
        long count = await counter.GetCountAsync();
   
        return new string[] { count.ToString() };
    }
    ```
   
    <span data-ttu-id="70c34-188">hello 첫 번째 코드 줄은 hello 키 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-188">hello first line of code is hello key one.</span></span> <span data-ttu-id="70c34-189">두 가지 정보를 tooprovide 해야 toocreate hello ICounter 프록시 toohello 상태 저장 서비스를: hello 서비스의 파티션 ID와 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-189">toocreate hello ICounter proxy toohello stateful service, you need tooprovide two pieces of information: a partition ID and hello name of hello service.</span></span>
   
    <span data-ttu-id="70c34-190">고객 ID 또는 우편 번호와 같은 정의 하는 키에 따라 상태로 다른 버킷으로 분할 하 여 분할 tooscale 상태 저장 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-190">You can use partitioning tooscale stateful services by breaking up their state into different buckets, based on a key that you define, such as a customer ID or postal code.</span></span> <span data-ttu-id="70c34-191">Trivial 응용 프로그램에서는 상태 저장 서비스의 hello은 하나만 포함 한 파티션에만 하므로 hello 키 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-191">In our trivial application, hello stateful service only has one partition, so hello key doesn't matter.</span></span> <span data-ttu-id="70c34-192">사용자가 제공한 아무 키나 toohello 일으킵니다 같은 파티션에 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-192">Any key that you provide will lead toohello same partition.</span></span> <span data-ttu-id="70c34-193">서비스를 분할에 대 한 더 toolearn 참조 [어떻게 toopartition 서비스 패브릭 신뢰할 수 있는 서비스](service-fabric-concepts-partitioning.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-193">toolearn more about partitioning services, see [How toopartition Service Fabric Reliable Services](service-fabric-concepts-partitioning.md).</span></span>
   
    <span data-ttu-id="70c34-194">hello 서비스 이름은 hello 양식 패브릭의 URI입니다. /&lt;i o n _&gt;/&lt;service_name&gt;합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-194">hello service name is a URI of hello form fabric:/&lt;application_name&gt;/&lt;service_name&gt;.</span></span>
   
    <span data-ttu-id="70c34-195">이러한 두 가지 정보를 서비스 패브릭 hello 컴퓨터에 요청을 보내야 하는 고유 하 게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-195">With these two pieces of information, Service Fabric can uniquely identify hello machine that requests should be sent to.</span></span> <span data-ttu-id="70c34-196">hello `ServiceProxy` 클래스도 원활 하 게 처리 프로그램이 hello 상태 저장 서비스의 파티션을 호스팅하는 hello 컴퓨터에서 오류가 발생 하 고 다른 컴퓨터에는 승격 된 tootake 있어야 합니다. hello 경우 그 자리입니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-196">hello `ServiceProxy` class also seamlessly handles hello case where hello machine that hosts hello stateful service partition fails and another machine must be promoted tootake its place.</span></span> <span data-ttu-id="70c34-197">이 추상화 쓰기를 사용 하면 더 간단 다른 서비스와 클라이언트 코드 toodeal hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-197">This abstraction makes writing hello client code toodeal with other services significantly simpler.</span></span>
   
    <span data-ttu-id="70c34-198">Hello hello 프록시, 있으면 호출 하면 됩니다 `GetCountAsync` 메서드 해당 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-198">Once we have hello proxy, we simply invoke hello `GetCountAsync` method and return its result.</span></span>

5. <span data-ttu-id="70c34-199">F5 키를 눌러 다시 toorun hello 응용 프로그램을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-199">Press F5 again toorun hello modified application.</span></span> <span data-ttu-id="70c34-200">로 이전에 Visual Studio를 자동으로 시작 hello 웹 프로젝트의 hello 브라우저 toohello 루트입니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-200">As before, Visual Studio automatically launches hello browser toohello root of hello web project.</span></span> <span data-ttu-id="70c34-201">Hello "api/값" 경로 추가 하 고 반환 된 hello 현재 카운터 값이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-201">Add hello "api/values" path, and you should see hello current counter value returned.</span></span>
   
    ![hello 브라우저에 표시 되는 hello 상태 저장 카운터 값][browser-aspnet-counter-value]
   
    <span data-ttu-id="70c34-203">Hello 브라우저를 새로 고치려면 주기적으로 toosee hello 카운터 값 업데이트입니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-203">Refresh hello browser periodically toosee hello counter value update.</span></span>

## <a name="kestrel-and-weblistener"></a><span data-ttu-id="70c34-204">Kestrel 및 WebListener</span><span class="sxs-lookup"><span data-stu-id="70c34-204">Kestrel and WebListener</span></span>

<span data-ttu-id="70c34-205">hello Kestrel, 이라는 기본 ASP.NET Core 웹 서버는 [현재 지원 되지 않는 직접 인터넷 트래픽을 처리 하기 위한](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel)합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-205">hello default ASP.NET Core web server, known as Kestrel, is [not currently supported for handling direct internet traffic](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span></span> <span data-ttu-id="70c34-206">결과적으로, hello 서비스 패브릭 용 ASP.NET Core 상태 비저장 서비스 템플릿을 사용 하 여 [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) 기본적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-206">As a result, hello ASP.NET Core stateless service template for Service Fabric uses [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) by default.</span></span> 

<span data-ttu-id="70c34-207">서비스 패브릭 서비스에 대 한 자세한 정보 Kestrel 및 WebListener toolearn 너무 참조 하십시오[서비스 패브릭 신뢰할 수 있는 서비스에서 ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-207">toolearn more about Kestrel and WebListener in Service Fabric services, please refer too[ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

## <a name="connecting-tooa-reliable-actor-service"></a><span data-ttu-id="70c34-208">Tooa Reliable Actor 서비스 연결</span><span class="sxs-lookup"><span data-stu-id="70c34-208">Connecting tooa Reliable Actor service</span></span>
<span data-ttu-id="70c34-209">이 자습서는 상태 저장 서비스와 통신하는 웹 프런트 엔드를 추가하는 방법에 초점을 맞추고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-209">This tutorial focused on adding a web front end that communicated with a stateful service.</span></span> <span data-ttu-id="70c34-210">그러나 매우 유사한 모델 tootalk tooactors를 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-210">However, you can follow a very similar model tootalk tooactors.</span></span> <span data-ttu-id="70c34-211">사용자가 Reliable Actor 프로젝트를 만들면 Visual Studio에서 자동으로 인터페이스 프로젝트를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-211">When you create a Reliable Actor project, Visual Studio automatically generates an interface project for you.</span></span> <span data-ttu-id="70c34-212">Hello 행위자가 포함 된 웹 프로젝트 toocommunicate hello에서에서 해당 인터페이스 toogenerate 행위자 프록시를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-212">You can use that interface toogenerate an actor proxy in hello web project toocommunicate with hello actor.</span></span> <span data-ttu-id="70c34-213">hello 통신 채널을 자동으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-213">hello communication channel is provided automatically.</span></span> <span data-ttu-id="70c34-214">해당 tooestablishing toodo은 어느 것에 필요 하지 않은 한 `ServiceRemotingListener` 이 자습서에서는 상태 저장 서비스의 hello 했던 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-214">So you do not need toodo anything that is equivalent tooestablishing a `ServiceRemotingListener` like you did for hello stateful service in this tutorial.</span></span>

## <a name="how-web-services-work-on-your-local-cluster"></a><span data-ttu-id="70c34-215">웹 서비스가 로컬 클러스터에서 작동하는 방식</span><span class="sxs-lookup"><span data-stu-id="70c34-215">How web services work on your local cluster</span></span>
<span data-ttu-id="70c34-216">일반적으로 동일한 서비스 패브릭 응용 프로그램 tooa 다중 컴퓨터 로컬 클러스터에 배포 하는 클러스터 및 예상 대로 작동 하는지 항상 확신 hello 정확 하 게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-216">In general, you can deploy exactly hello same Service Fabric application tooa multi-machine cluster that you deployed on your local cluster and be highly confident that it works as you expect.</span></span> <span data-ttu-id="70c34-217">즉, 로컬 클러스터 된 다섯 개 노드 구성을 단순히 tooa 단일 컴퓨터 축소 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-217">This is because your local cluster is simply a five-node configuration that is collapsed tooa single machine.</span></span>

<span data-ttu-id="70c34-218">그러나 Tooweb 서비스를 때는,는 하나의 키 미묘한 차이입니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-218">When it comes tooweb services, however, there is one key nuance.</span></span> <span data-ttu-id="70c34-219">클러스터와 Azure에서 부하 분산 장치 뒤에 배치를 확인 해야 hello 부하 분산 장치 이후 웹 서비스에 모든 컴퓨터에 배포 되 hello 컴퓨터 간에 트래픽을 단순히 라운드 robins 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-219">When your cluster sits behind a load balancer, as it does in Azure, you must ensure that your web services are deployed on every machine since hello load balancer simply round-robins traffic across hello machines.</span></span> <span data-ttu-id="70c34-220">Hello 설정 하 여 이렇게 하려면 `InstanceCount` hello 서비스 toohello 특수 값 "-1"에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-220">You can do this by setting hello `InstanceCount` for hello service toohello special value of "-1".</span></span>

<span data-ttu-id="70c34-221">반면, 웹 서비스를 로컬로 실행할 때 필요한 tooensure hello 서비스의 인스턴스를 하나만 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-221">By contrast, when you run a web service locally, you need tooensure that only one instance of hello service is running.</span></span> <span data-ttu-id="70c34-222">충돌에서 수신 하는 hello 동일 하는 여러 프로세스에서 실행, 경로 및 포트.</span><span class="sxs-lookup"><span data-stu-id="70c34-222">Otherwise, you run into conflicts from multiple processes that are listening on hello same path and port.</span></span> <span data-ttu-id="70c34-223">Hello 웹 서비스 인스턴스 수가 너무 하 여 설정 해야 결과적으로, 로컬 배포에 대 한 "1".</span><span class="sxs-lookup"><span data-stu-id="70c34-223">As a result, hello web service instance count should be set too"1" for local deployments.</span></span>

<span data-ttu-id="70c34-224">서로 다른 환경에 대 한 서로 다른 값 tooconfigure 참조 toolearn [여러 환경에 대 한 응용 프로그램 매개 변수 관리](service-fabric-manage-multiple-environment-app-configuration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-224">toolearn how tooconfigure different values for different environment, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="70c34-225">다음 단계</span><span class="sxs-lookup"><span data-stu-id="70c34-225">Next steps</span></span>
<span data-ttu-id="70c34-226">이제 ASP.NET Core를 통해 웹 프런트가 응용 프로그램에 사용할 수 있게 설정되었으므로 ASP.NET Core가 Service Fabric과 작동하는 방식을 깊이 있게 이해하도록 [Service Fabric Reliable Services의 ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="70c34-226">Now that you have a web front end set up for your application with ASP.NET Core, learn more about [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) for an in-depth understanding of how ASP.NET Core works with Service Fabric.</span></span>

<span data-ttu-id="70c34-227">그런 다음, [서비스와 통신 하는 방법에 대 한 자세한 정보](service-fabric-connect-and-communicate-with-services.md) 일반적 완전 한 tooget 그림 어떻게 서비스의 통신 서비스 패브릭에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-227">Next, [learn more about communicating with services](service-fabric-connect-and-communicate-with-services.md) in general tooget a complete picture of how service communication works in Service Fabric.</span></span>

<span data-ttu-id="70c34-228">서비스 통신의 작동 방식을 잘 알고 있으면 [Azure에서 클러스터를 만들고 응용 프로그램 toohello 클라우드 배포](service-fabric-cluster-creation-via-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="70c34-228">Once you have a good understanding of how service communication works, [create a cluster in Azure and deploy your application toohello cloud](service-fabric-cluster-creation-via-portal.md).</span></span>

<!-- Image References -->

[vs-add-new-service]: ./media/service-fabric-add-a-web-frontend/vs-add-new-service.png
[vs-new-service-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-service-dialog.png
[vs-new-aspnet-project-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-aspnet-project-dialog.png
[browser-aspnet-template-values]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-template-values.png
[vs-add-class-library-project]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-project.png
[vs-add-class-library-reference]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-reference.png
[vs-services-nuget-package]: ./media/service-fabric-add-a-web-frontend/vs-services-nuget-package.png
[browser-aspnet-counter-value]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-counter-value.png
[vs-create-platform]: ./media/service-fabric-add-a-web-frontend/vs-create-platform.png


<!-- external links -->
[dotnetcore-install]: https://www.microsoft.com/net/core#windows
